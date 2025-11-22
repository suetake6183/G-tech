# MIRRALISM I/O設計とAIモデル戦略

## 1. インプット/アウトプット設計

### 1.1 インプット（統一窓口）

```yaml
入力インターフェース:
  場所: 単一の対話窓口
  
  受付可能な入力:
    - テキスト（直接入力）
    - 音声（Aqua Voice経由）
    - ファイル（PDF、画像、Excel等）
    - URL（Webページ）
    - メール転送
  
  入力時の自動識別:
    - クライアント名の自動認識
    - 案件種別の推定
    - 緊急度の判定
```

### 1.2 アウトプット（AI整理済み構造）

```
/MIRRALISM_OUTPUT/
├── 📁 Clients/                    # クライアント別
│   ├── 📁 黒澤工務店/
│   │   ├── 📄 Profile.md          # 基本情報・特徴
│   │   ├── 📁 Projects/           # 案件別
│   │   │   ├── 📁 2025-06_エコ住宅提案/
│   │   │   │   ├── 📄 Summary.md  # AI要約
│   │   │   │   ├── 📄 Insights.md # 洞察
│   │   │   │   ├── 📄 Proposal.md # 提案書
│   │   │   │   └── 📁 References/ # 元データ
│   │   │   └── 📁 2025-05_リフォーム相談/
│   │   ├── 📁 Insights/           # 蓄積された洞察
│   │   └── 📁 Communications/     # やり取り履歴
│   │
│   └── 📁 田中建設/
│       └── ...
│
├── 📁 Personal/                   # 自分関連
│   ├── 📁 Ideas/                  # アイデア・思考
│   ├── 📁 Learning/               # 学習メモ
│   └── 📁 Tasks/                  # タスク・TODO
│
├── 📁 Knowledge/                  # 知識ベース
│   ├── 📁 Industry/               # 業界知識
│   ├── 📁 Technology/             # 技術情報
│   └── 📁 Best_Practices/         # ベストプラクティス
│
└── 📁 Analytics/                  # 分析・レポート
    ├── 📄 Weekly_Summary.md       # 週次サマリー
    ├── 📄 Client_Trends.md        # クライアント動向
    └── 📄 Opportunity_Map.md      # 機会マップ
```

### 1.3 アウトプット生成ルール

```python
class OutputOrganizer:
    """AIが理解した内容を人間に分かりやすく整理"""
    
    async def process_input(self, input_data, ai_understanding):
        # 1. 文脈を特定
        context = await self.identify_context(ai_understanding)
        # 例: {"client": "黒澤工務店", "type": "相談", "topic": "エコ住宅"}
        
        # 2. 適切な場所を決定
        output_path = self.determine_path(context)
        # 例: "/Clients/黒澤工務店/Projects/2025-06_エコ住宅提案/"
        
        # 3. 構造化されたアウトプットを生成
        outputs = await self.generate_outputs(ai_understanding)
        
        # 4. 自動的に適切な場所に保存
        await self.save_outputs(output_path, outputs)
        
        # 5. 関連情報をリンク
        await self.link_related(output_path, context)
    
    def determine_path(self, context):
        """文脈から適切な保存先を決定"""
        if context.get("client"):
            return f"/Clients/{context['client']}/Projects/{context['project_id']}/"
        elif context.get("personal"):
            return f"/Personal/{context['category']}/"
        else:
            return f"/Knowledge/{context['domain']}/"
```

## 2. AIモデル戦略

### 2.1 現在の選定モデル

```yaml
メインモデル:
  名称: Claude 3.5 Sonnet
  理由:
    - 日本語理解力が高い
    - 長文脈対応（200k tokens）
    - 推論能力が優秀
    - APIが安定
  
  用途:
    - 対話理解
    - 洞察生成
    - 提案作成
    - 要約・整理

補助モデル:
  埋め込みモデル: text-embedding-3-small
  理由:
    - コスト効率が良い
    - 日本語対応
    - 高速
  
  用途:
    - 意味的検索
    - 類似性判定
    - クラスタリング

将来検討モデル:
  - GPT-4o（マルチモーダル対応時）
  - Gemini Pro（コスト最適化時）
  - Local LLM（プライバシー重視時）
```

### 2.2 モデル抽象化レイヤー

```python
from abc import ABC, abstractmethod
from typing import Dict, Any
import asyncio

class AIModel(ABC):
    """全てのAIモデルの基底クラス"""
    
    @abstractmethod
    async def understand(self, input_text: str) -> Dict[str, Any]:
        """入力を理解する"""
        pass
    
    @abstractmethod
    async def generate_insight(self, understanding: Dict) -> str:
        """洞察を生成する"""
        pass
    
    @abstractmethod
    async def create_proposal(self, context: Dict) -> str:
        """提案を作成する"""
        pass

class ClaudeModel(AIModel):
    """Claude 3.5 Sonnet実装"""
    
    def __init__(self, api_key: str):
        self.client = AsyncAnthropic(api_key=api_key)
        self.model = "claude-3-5-sonnet-20241022"
    
    async def understand(self, input_text: str) -> Dict[str, Any]:
        # Claude特有の実装
        response = await self.client.messages.create(...)
        return self.parse_response(response)

class GPT4Model(AIModel):
    """GPT-4実装（将来用）"""
    
    def __init__(self, api_key: str):
        self.client = AsyncOpenAI(api_key=api_key)
        self.model = "gpt-4-turbo"
    
    async def understand(self, input_text: str) -> Dict[str, Any]:
        # GPT-4特有の実装
        response = await self.client.chat.completions.create(...)
        return self.parse_response(response)

# モデルファクトリー
class ModelFactory:
    """設定に基づいて適切なモデルを返す"""
    
    @staticmethod
    def create_model(config: Dict) -> AIModel:
        model_type = config.get("model_type", "claude")
        
        if model_type == "claude":
            return ClaudeModel(config["api_key"])
        elif model_type == "gpt4":
            return GPT4Model(config["api_key"])
        else:
            raise ValueError(f"Unknown model type: {model_type}")
```

### 2.3 モデルアップデート戦略

```yaml
設定ファイル: /config/ai_models.yaml

current_model:
  type: "claude"
  version: "3.5-sonnet"
  api_key_env: "ANTHROPIC_API_KEY"
  
model_history:
  - date: "2025-06-14"
    model: "claude-3.5-sonnet"
    reason: "初期実装"
    
migration_rules:
  # 新モデル追加時の移行ルール
  compatibility_test:
    - 既存データでの動作確認
    - パフォーマンス比較
    - コスト試算
    
  rollback_plan:
    - 旧モデルへの即時切り替え
    - データ整合性の確保
```

```python
class ModelManager:
    """モデルのバージョン管理とアップデート"""
    
    def __init__(self, config_path: str):
        self.config = self.load_config(config_path)
        self.current_model = self.load_current_model()
        
    async def upgrade_model(self, new_model_config: Dict):
        """新しいモデルへのアップグレード"""
        # 1. 互換性テスト
        if await self.test_compatibility(new_model_config):
            # 2. 段階的移行
            await self.gradual_migration(new_model_config)
            # 3. 設定更新
            self.update_config(new_model_config)
        else:
            raise ValueError("新モデルは互換性テストに失敗")
    
    async def test_compatibility(self, new_config: Dict) -> bool:
        """標準テストセットで互換性確認"""
        test_cases = [
            "クライアント相談の理解",
            "提案書生成",
            "洞察の質"
        ]
        
        old_model = self.current_model
        new_model = ModelFactory.create_model(new_config)
        
        for test in test_cases:
            old_result = await old_model.process(test)
            new_result = await new_model.process(test)
            
            if not self.results_compatible(old_result, new_result):
                return False
        
        return True
```

## 3. 実装優先順位

### Phase 1: 基本I/Oシステム（1週目）

```python
# 最小限の実装
class MirralismCore:
    def __init__(self):
        self.ai_model = ClaudeModel(api_key=os.getenv("ANTHROPIC_API_KEY"))
        self.output_organizer = OutputOrganizer()
        
    async def process(self, input_text: str):
        # 1. AIが理解
        understanding = await self.ai_model.understand(input_text)
        
        # 2. 適切な場所に整理して保存
        await self.output_organizer.process_input(input_text, understanding)
        
        # 3. ユーザーに結果を表示
        return {
            "understood": understanding,
            "saved_to": output_path,
            "insights": insights
        }
```

### Phase 2: モデル抽象化（2週目）

- ModelFactoryの実装
- 設定ファイルベースの切り替え
- A/Bテスト機能

### Phase 3: 高度な整理機能（3週目）

- 自動クロスリファレンス
- 時系列分析
- トレンド検出

## 4. 使用イメージ

```bash
# ユーザーが何か入力
"黒澤工務店から、最近エコ住宅の相談が増えてきた。
コストの説明が難しいらしい。何か良い提案方法はないか？"

# システムの処理
1. AI理解: クライアント=黒澤工務店、課題=エコ住宅のコスト説明
2. 洞察生成: 初期投資vs長期メリットの可視化が重要
3. 自動保存先: /Clients/黒澤工務店/Projects/2025-06_エコ住宅提案/
4. 生成物:
   - Summary.md（要約）
   - Insights.md（洞察：補助金活用、他社事例など）
   - Proposal.md（提案：10年収支シミュレーション）

# ユーザーが後で確認
"黒澤工務店の最近の案件を見せて"
→ /Clients/黒澤工務店/Projects/ を表示
→ 時系列で整理された案件一覧
```