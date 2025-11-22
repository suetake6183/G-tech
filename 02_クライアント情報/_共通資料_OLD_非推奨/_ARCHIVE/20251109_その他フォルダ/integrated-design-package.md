# 人間関係分析システム統合設計書パッケージ

このパッケージには、プロジェクトを成功に導くために必要なすべての設計が含まれています。

## 目次
1. システム概要
2. フォルダ構成  
3. データベース設計
4. 実装順序と優先度
5. 各機能の詳細設計
6. コード例とテストケース
7. エラーハンドリング

---

## 1. システム概要

### 目的
末武さんの議事録や思考メモをLLMが自律的に分析し、人間関係の洞察を提供するシステム

### 重要な制約
- **APIは使わない**（Claude Code内で直接分析）
- **非エンジニア向け**（エラーは日本語、操作は簡単）
- **段階的実装**（1日1機能）

### システムの流れ
1. inputフォルダにファイルを配置
2. AIがファイル種類を自動判別
3. 分析方法をAIが提案
4. ユーザーが承認/修正
5. 分析実行・結果保存
6. フィードバックで学習
7. ファイルを自動アーカイブ

---

## 2. フォルダ構成

```
project-root/
├── input/               # 分析対象ファイル（直接配置）
├── archive/             # 分析済みファイルの保管
│   ├── 2025/
│   │   └── 06/
│   └── index.db
├── output/              
│   ├── analysis/        # 分析結果
│   ├── profiles/        
│   │   ├── suetake/     # 末武さん専用
│   │   └── clients/     
│   └── insights/        
├── database/            
│   ├── learning.db      
│   ├── profiles.db      
│   └── archive-index.db 
├── scripts/             
│   ├── analyze.js       
│   ├── profile.js       
│   ├── feedback.js      
│   ├── archive.js       
│   └── db-setup.js      
├── config.json          # 設定ファイル
├── package.json         
└── README.md            
```

---

## 3. データベース設計

### 3.1 learning.db

```sql
-- 分析パターンの学習
CREATE TABLE learning_patterns (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    pattern_description TEXT NOT NULL,
    pattern_details TEXT,
    success_count INTEGER DEFAULT 1,
    context TEXT,
    last_used TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- フィードバック履歴
CREATE TABLE feedback_history (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    original_method TEXT NOT NULL,
    user_feedback TEXT NOT NULL,
    improved_method TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- 分析結果へのフィードバック
CREATE TABLE analysis_results_feedback (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    analysis_id TEXT NOT NULL,
    result_section TEXT,
    original_conclusion TEXT,
    user_feedback TEXT,
    corrected_conclusion TEXT,
    feedback_type TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### 3.2 profiles.db

```sql
CREATE TABLE persons (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    name TEXT NOT NULL UNIQUE,
    role TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE personality_traits (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    person_id INTEGER,
    trait_type TEXT,
    trait_description TEXT,
    confidence_score REAL DEFAULT 0.5,
    observed_count INTEGER DEFAULT 1,
    last_observed TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (person_id) REFERENCES persons(id)
);
```

### 3.3 archive-index.db

```sql
CREATE TABLE archive_index (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    original_filename TEXT NOT NULL,
    archived_path TEXT NOT NULL,
    file_type TEXT,
    analysis_id TEXT,
    content_summary TEXT,
    archived_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    year INTEGER,
    month INTEGER
);
```

---

## 4. 実装順序と優先度

### Week 1: 基本機能
1. **Day 1**: プロジェクト初期化
   - フォルダ構造作成
   - npm install
   - DB初期化

2. **Day 2-3**: ファイル読み込み
   - scripts/analyze.js の基本部分
   - ファイル種別の自動判定

3. **Day 4-5**: 分析実行
   - 基本的な分析機能
   - 結果の保存

### Week 2: 学習機能
1. **Day 6-7**: フィードバック機能
   - 分析方法の提案
   - ユーザー承認/修正

2. **Day 8-9**: 学習の実装
   - DBへの保存
   - 次回への反映

### Week 3: 高度な機能
1. **Day 10-12**: プロファイル
   - 末武さんの特徴抽出
   - プロファイル更新

2. **Day 13-14**: アーカイブ
   - 自動アーカイブ
   - 検索機能

---

## 5. 各機能の詳細設計

### 5.1 ファイル種別判定（analyze.js）

```javascript
async function detectContentType(content) {
    // キーワードベースの判定
    const keywords = {
        meeting: ['会議', '議事録', '様：', '参加者'],
        personal: ['思う', '考える', '気づき'],
        proposal: ['提案', 'ご検討', '見積']
    };
    
    // スコアリング
    let scores = { meeting: 0, personal: 0, proposal: 0 };
    
    for (const [type, words] of Object.entries(keywords)) {
        words.forEach(word => {
            if (content.includes(word)) scores[type]++;
        });
    }
    
    // 最高スコアのタイプを返す
    return Object.entries(scores)
        .sort(([,a], [,b]) => b - a)[0][0];
}
```

### 5.2 分析提案機能

```javascript
async function proposeAnalysisMethod(content, fileType) {
    console.log('\n【分析方法の提案】');
    
    // 過去の成功パターンを取得
    const patterns = await getSuccessfulPatterns(fileType);
    
    if (patterns.length > 0) {
        console.log('過去の成功パターンから：');
        console.log(patterns[0].pattern_description);
    } else {
        // デフォルトの提案
        const defaults = {
            meeting: '1. 話題の分類\n2. 関係性分析\n3. アクションアイテム',
            personal: '1. 思考の整理\n2. 気づきの抽出\n3. 次のアクション',
            proposal: '1. 要件整理\n2. リスク分析\n3. スケジュール'
        };
        console.log(defaults[fileType]);
    }
    
    console.log('\nこの方法で分析してよろしいですか？ (y/n/修正内容)');
}
```

### 5.3 学習機能

```javascript
async function learnFromFeedback(originalMethod, feedback, wasApproved) {
    const db = await connectDB();
    
    if (wasApproved) {
        // 成功パターンとして記録
        await db.run(
            'INSERT INTO learning_patterns (pattern_description) VALUES (?)',
            [originalMethod]
        );
    } else {
        // フィードバックを記録
        await db.run(
            'INSERT INTO feedback_history (original_method, user_feedback) VALUES (?, ?)',
            [originalMethod, feedback]
        );
    }
}
```

### 5.4 アーカイブ機能

```javascript
async function archiveFile(filePath, analysisId) {
    const now = new Date();
    const archivePath = `archive/${now.getFullYear()}/${String(now.getMonth()+1).padStart(2,'0')}/`;
    
    // フォルダ作成
    await fs.mkdir(archivePath, { recursive: true });
    
    // ファイル移動
    const filename = path.basename(filePath);
    await fs.rename(filePath, path.join(archivePath, filename));
    
    console.log(`✓ アーカイブ完了: ${archivePath}${filename}`);
}
```

---

## 6. コード例とテストケース

### 6.1 db-setup.js（最初に実行）

```javascript
const sqlite3 = require('sqlite3');
const { open } = require('sqlite');

async function setupDatabases() {
    console.log('データベースを初期化中...');
    
    // learning.db
    const learningDb = await open({
        filename: './database/learning.db',
        driver: sqlite3.Database
    });
    
    await learningDb.exec(`
        CREATE TABLE IF NOT EXISTS learning_patterns (
            id INTEGER PRIMARY KEY AUTOINCREMENT,
            pattern_description TEXT NOT NULL,
            pattern_details TEXT,
            success_count INTEGER DEFAULT 1,
            context TEXT,
            last_used TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
            created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
        );
        
        CREATE TABLE IF NOT EXISTS feedback_history (
            id INTEGER PRIMARY KEY AUTOINCREMENT,
            original_method TEXT NOT NULL,
            user_feedback TEXT NOT NULL,
            improved_method TEXT,
            created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
        );
    `);
    
    console.log('✓ learning.db 作成完了');
    
    // 他のDBも同様に作成...
    
    console.log('すべてのデータベースの初期化が完了しました！');
}

setupDatabases().catch(console.error);
```

### 6.2 テスト用サンプルファイル

**input/test-meeting.txt**
```
日時：2025年6月16日 14:00-15:00
参加者：末武様、A社山田様、A社鈴木様

議題：新システムの要件確認

山田様：先日お送りいただいた提案書を確認しました。
末武様：ありがとうございます。ご不明な点はございますか？
鈴木様：価格面について詳しく教えていただけますか。
末武様：初期費用は50万円、月額は3万円を想定しています。

【決定事項】
- 来週までに詳細見積もりを提出
- 技術仕様書を作成

【次回】
6月23日 14:00
```

---

## 7. エラーハンドリング

### 7.1 共通エラー処理

```javascript
function handleError(error, context) {
    const errorMessages = {
        'ENOENT': 'ファイルが見つかりません',
        'EACCES': 'ファイルへのアクセス権限がありません',
        'ENOSPC': 'ディスク容量が不足しています',
        'SQLITE_ERROR': 'データベースエラーが発生しました'
    };
    
    const message = errorMessages[error.code] || error.message;
    console.error(`エラー（${context}）: ${message}`);
    
    // デバッグ情報
    if (process.env.DEBUG) {
        console.error('詳細:', error);
    }
}
```

### 7.2 使用例

```javascript
try {
    const content = await fs.readFile(filePath, 'utf-8');
} catch (error) {
    handleError(error, 'ファイル読み込み');
    return;
}
```

---

## 実装開始チェックリスト

- [ ] Node.jsがインストールされている
- [ ] プロジェクトフォルダを作成した
- [ ] この設計書を理解した
- [ ] Claude Codeの準備ができた

準備ができたら、プロンプトと一緒にこの設計書をClaude Codeに渡してください。

頑張ってください！🚀