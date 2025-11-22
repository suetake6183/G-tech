# フェーズ3詳細実行ガイド（Cursor Composer用）

**作成日**: 2025年11月9日
**目的**: 各クライアントの構造統一を確実に実行するための詳細手順書

---

## ⚠️ 実行前の重要注意事項

### 1. フェーズ2の完了確認
```bash
# フェーズ2が完了していることを確認
git log --oneline -5
# 「フェーズ2完了」のコミットがあることを確認
```

### 2. git status確認
```bash
cd "/Volumes/G-TECH/02_クライアント情報"
git status
```
- 未コミットの変更がある場合、先にコミット

### 3. ディスク容量確認
```bash
df -h "/Volumes/G-TECH"
```
- 最低5GB以上の空き容量があることを確認

---

## 📋 基本方針

### 統一構造の定義
```
クライアント名/
├── README.md                    # クライアント基本情報
├── [プロジェクト名]/
│   ├── PROJECT.md               # プロジェクトダッシュボード
│   ├── 00_INPUT/                # 収集した情報
│   ├── 01_OUTPUT/               # 生成した書類
│   │   ├── クライアント向け/
│   │   ├── 外注先向け/
│   │   └── 内部用/
│   └── 02_ARCHIVE/              # 不要になったファイル
└── 00_CORE/                     # 判断が必要なファイルの一時保管
```

### 処理方針
1. **既に統一構造のもの** → 何もしない（フェーズ1で作成した16プロジェクト）
2. **明確に移動できるもの** → 統一構造に変換
3. **判断が必要なもの** → `00_CORE/` に保管（後で手動整理）

---

## 📋 実行の全体フロー

```
Step 1: 既に統一構造のクライアント確認（何もしない）
  ↓
Step 2: 黒澤工務店の構造統一
  ↓
Step 3: SKコームの構造統一
  ↓
Step 4: その他既存クライアントの整理
  ↓
Step 5: 全クライアントへのREADME.md追加
  ↓
Step 6: 検証
```

---

## Step 1: 既に統一構造のクライアント確認

### フェーズ1で作成した16プロジェクト（何もしない）

以下のプロジェクトは既に統一構造になっているため、**何もしません**：

**法人クライアント（12プロジェクト）:**
1. SKコーム/顧問契約/
2. 東京医療商事/事務所内装工事/
3. アストライズ/池田山コープ改修工事/
4. ジューテクノ/takaraキッチン工事/
5. ジューテクノ/練馬区リフォーム工事/
6. ネクストドア/ユニビル2階事務所改修工事/
7. 猛建設/ラ・アトレ横濱鶴見Ⅱ 6階改修工事/
8. 青柳不動産/フォレストコート小竹104号室改修工事/
9. 信濃商事/信濃ビル8階漏電ブレーカー交換工事/
10. チア/チア2号店改修工事/
11. cocomate/ロゴデザイン・ブランディング/
12. cocomate/ROBOT PAYMENT決済サービス導入/

**個人顧客（3プロジェクト）:**
13. 吉沼/クレーヌ吉沼505号室改修工事/
14. 富田みよこ/富田邸リフォーム工事/
15. 東野真由美/東野邸玄関鏡設置工事/

**AGO（1プロジェクト）:**
16. AGO/就業規則作成支援/

**AOMI100クリニック（1プロジェクト）:**
17. AOMI100クリニック/2025/サイン・床・壁張り替え工事/

### 確認のみ実施
```bash
# 統一構造のプロジェクト数確認
find "/Volumes/G-TECH/02_クライアント情報" -name "PROJECT.md" -type f | wc -l
# 期待値: 17以上（既存プロジェクトが追加されている可能性あり）
```

---

## Step 2: 黒澤工務店の構造統一

### 現在の構造
```
黒澤工務店/
├── 01_プロジェクト/
│   ├── AI導入・DX推進/
│   ├── 業務提携（SKコーム）/
│   ├── 情報システム刷新/
│   ├── 人材・ビジネスマッチング/
│   └── ミラリズム提案（不採用）/
├── 02_コミュニケーション記録/
├── 03_ナレッジベース/
├── 04_契約・請求/
├── 2024/
├── 2025/
├── 99_アーカイブ/
├── _緊急/
├── 資料/
├── 会議議事録/
├── 戦略提案_2025年11月_*.md（複数）
├── CLIENT_PROFILE.md
├── DEEP_ANALYSIS_*.md
└── README.md
```

### 2-1. 00_COREフォルダの作成

```bash
mkdir -p "/Volumes/G-TECH/02_クライアント情報/黒澤工務店/00_CORE"
```

### 2-2. プロジェクトフォルダの移動

```bash
# 01_プロジェクト配下の各プロジェクトをトップレベルへ移動
mv "/Volumes/G-TECH/02_クライアント情報/黒澤工務店/01_プロジェクト/AI導入・DX推進" \
   "/Volumes/G-TECH/02_クライアント情報/黒澤工務店/"

mv "/Volumes/G-TECH/02_クライアント情報/黒澤工務店/01_プロジェクト/業務提携（SKコーム）" \
   "/Volumes/G-TECH/02_クライアント情報/黒澤工務店/"

mv "/Volumes/G-TECH/02_クライアント情報/黒澤工務店/01_プロジェクト/情報システム刷新" \
   "/Volumes/G-TECH/02_クライアント情報/黒澤工務店/"

mv "/Volumes/G-TECH/02_クライアント情報/黒澤工務店/01_プロジェクト/人材・ビジネスマッチング" \
   "/Volumes/G-TECH/02_クライアント情報/黒澤工務店/"

mv "/Volumes/G-TECH/02_クライアント情報/黒澤工務店/01_プロジェクト/ミラリズム提案（不採用）" \
   "/Volumes/G-TECH/02_クライアント情報/黒澤工務店/"

# 空の01_プロジェクトフォルダを削除
rmdir "/Volumes/G-TECH/02_クライアント情報/黒澤工務店/01_プロジェクト"
```

### 2-3. 機能別フォルダを00_COREへ移動

```bash
# 判断が必要なフォルダを00_COREへ保管
mv "/Volumes/G-TECH/02_クライアント情報/黒澤工務店/02_コミュニケーション記録" \
   "/Volumes/G-TECH/02_クライアント情報/黒澤工務店/00_CORE/"

mv "/Volumes/G-TECH/02_クライアント情報/黒澤工務店/03_ナレッジベース" \
   "/Volumes/G-TECH/02_クライアント情報/黒澤工務店/00_CORE/"

mv "/Volumes/G-TECH/02_クライアント情報/黒澤工務店/04_契約・請求" \
   "/Volumes/G-TECH/02_クライアント情報/黒澤工務店/00_CORE/"

mv "/Volumes/G-TECH/02_クライアント情報/黒澤工務店/2024" \
   "/Volumes/G-TECH/02_クライアント情報/黒澤工務店/00_CORE/"

mv "/Volumes/G-TECH/02_クライアント情報/黒澤工務店/2025" \
   "/Volumes/G-TECH/02_クライアント情報/黒澤工務店/00_CORE/"

mv "/Volumes/G-TECH/02_クライアント情報/黒澤工務店/99_アーカイブ" \
   "/Volumes/G-TECH/02_クライアント情報/黒澤工務店/00_CORE/"

mv "/Volumes/G-TECH/02_クライアント情報/黒澤工務店/_緊急" \
   "/Volumes/G-TECH/02_クライアント情報/黒澤工務店/00_CORE/"

mv "/Volumes/G-TECH/02_クライアント情報/黒澤工務店/資料" \
   "/Volumes/G-TECH/02_クライアント情報/黒澤工務店/00_CORE/"

mv "/Volumes/G-TECH/02_クライアント情報/黒澤工務店/会議議事録" \
   "/Volumes/G-TECH/02_クライアント情報/黒澤工務店/00_CORE/"
```

### 2-4. ファイルを00_COREへ移動

```bash
# ルートレベルのファイルを00_COREへ移動（README.md以外）
mv "/Volumes/G-TECH/02_クライアント情報/黒澤工務店/戦略提案_2025年11月_"*.md \
   "/Volumes/G-TECH/02_クライアント情報/黒澤工務店/00_CORE/" 2>/dev/null || true

mv "/Volumes/G-TECH/02_クライアント情報/黒澤工務店/CLIENT_PROFILE.md" \
   "/Volumes/G-TECH/02_クライアント情報/黒澤工務店/00_CORE/" 2>/dev/null || true

mv "/Volumes/G-TECH/02_クライアント情報/黒澤工務店/DEEP_ANALYSIS_"*.md \
   "/Volumes/G-TECH/02_クライアント情報/黒澤工務店/00_CORE/" 2>/dev/null || true

mv "/Volumes/G-TECH/02_クライアント情報/黒澤工務店/提供価値マップ.md" \
   "/Volumes/G-TECH/02_クライアント情報/黒澤工務店/00_CORE/" 2>/dev/null || true
```

### 2-5. 各プロジェクトに統一構造を適用

```bash
# 各プロジェクトにPROJECT.mdと標準フォルダを作成
for project in "AI導入・DX推進" "業務提携（SKコーム）" "情報システム刷新" "人材・ビジネスマッチング" "ミラリズム提案（不採用）"; do
  mkdir -p "/Volumes/G-TECH/02_クライアント情報/黒澤工務店/${project}/00_INPUT"
  mkdir -p "/Volumes/G-TECH/02_クライアント情報/黒澤工務店/${project}/01_OUTPUT/クライアント向け"
  mkdir -p "/Volumes/G-TECH/02_クライアント情報/黒澤工務店/${project}/01_OUTPUT/外注先向け"
  mkdir -p "/Volumes/G-TECH/02_クライアント情報/黒澤工務店/${project}/01_OUTPUT/内部用"
  mkdir -p "/Volumes/G-TECH/02_クライアント情報/黒澤工務店/${project}/02_ARCHIVE"

  # PROJECT.mdテンプレートをコピー
  cp "/Volumes/G-TECH/02_クライアント情報/_TEMPLATE/PROJECT_TEMPLATE/PROJECT.md" \
     "/Volumes/G-TECH/02_クライアント情報/黒澤工務店/${project}/"
done
```

### 検証

```bash
# 黒澤工務店のプロジェクト数確認
ls -d "/Volumes/G-TECH/02_クライアント情報/黒澤工務店"/*/ | grep -v "00_CORE" | wc -l
# 期待値: 5（5つのプロジェクト）

# 00_COREフォルダの存在確認
ls "/Volumes/G-TECH/02_クライアント情報/黒澤工務店/00_CORE/" | wc -l
# 期待値: 10以上（移動したフォルダとファイル）
```

---

## Step 3: SKコームの構造統一

### 現在の構造
```
SKコーム/
├── 顧問契約/                    # 既に統一構造（フェーズ1で作成）
├── 01_契約・見積/
├── 02_請求書/
├── 03_プロジェクト資料/
├── 04_連絡記録/
├── 05_写真・メディア/
├── 2024/
├── 2025/
├── SK印鑑/
├── TODO関連/
├── コミュニケーション記録/
├── マイナンバー/
├── ロゴ/
├── 会社基礎書類/
├── 会社書類/
├── 会計資料/
├── 個人顧客/
├── 動画/
├── 大橋邸/
├── 封筒用印刷/
├── 打合せ資料/
├── 書類/
├── 決算関係/
├── 現場写真/
├── 試算表/
├── 請求書/
├── 送付資料/
├── 領収書/
├── _緊急/
└── 各種ファイル
```

### 3-1. 00_COREフォルダの作成

```bash
mkdir -p "/Volumes/G-TECH/02_クライアント情報/SKコーム/00_CORE"
```

### 3-2. 既存フォルダを00_COREへ移動

```bash
# 顧問契約以外の全フォルダを00_COREへ移動
cd "/Volumes/G-TECH/02_クライアント情報/SKコーム/"

# フォルダ移動（顧問契約、00_CORE、隠しフォルダを除く）
for dir in */; do
  dirname=$(basename "$dir")
  if [ "$dirname" != "顧問契約" ] && [ "$dirname" != "00_CORE" ] && [[ "$dirname" != .* ]]; then
    mv "$dir" "00_CORE/"
  fi
done

# ルートレベルのファイルを00_COREへ移動
mv *.* "00_CORE/" 2>/dev/null || true
```

### 検証

```bash
# SKコームのトップレベル確認
ls "/Volumes/G-TECH/02_クライアント情報/SKコーム/"
# 期待値: 顧問契約, 00_CORE のみ（隠しフォルダ除く）

# 00_COREの内容確認
ls "/Volumes/G-TECH/02_クライアント情報/SKコーム/00_CORE/" | wc -l
# 期待値: 30以上（移動したフォルダとファイル）
```

---

## Step 4: その他既存クライアントの整理

### 対象クライアント
以下のクライアントは既存データがある可能性があります：

- DOA
- 翼ビジョン（堀内さん）
- ジューテクノ
- 柳屋関連
- アストライズ
- エトワール
- 青柳不動産
- WEB屋喜作
- 樋口様
- ムラカミリョウ
- 渡邉みい

### 4-1. 既存データを00_COREへ整理

```bash
# 各クライアントに対して、フェーズ1で作成したプロジェクト以外を00_COREへ移動

# 例: ジューテクノ
if [ -d "/Volumes/G-TECH/02_クライアント情報/ジューテクノ" ]; then
  mkdir -p "/Volumes/G-TECH/02_クライアント情報/ジューテクノ/00_CORE"
  cd "/Volumes/G-TECH/02_クライアント情報/ジューテクノ/"

  # takaraキッチン工事と練馬区リフォーム工事以外を00_COREへ移動
  for dir in */; do
    dirname=$(basename "$dir")
    if [ "$dirname" != "takaraキッチン工事" ] && \
       [ "$dirname" != "練馬区リフォーム工事" ] && \
       [ "$dirname" != "00_CORE" ] && \
       [[ "$dirname" != .* ]]; then
      mv "$dir" "00_CORE/" 2>/dev/null || true
    fi
  done

  # ルートレベルのファイルを00_COREへ
  mv *.* "00_CORE/" 2>/dev/null || true
fi

# 同様の処理を他のクライアントにも実施
# （スクリプトで一括処理）
```

**注意**: このステップは、各クライアントの既存構造を確認してから実行します。
フェーズ1で作成したプロジェクトがないクライアントは、全て00_COREに保管します。

---

## Step 5: 全クライアントへのREADME.md追加

### 5-1. README.mdが存在しないクライアントを確認

```bash
# README.mdがないクライアントをリストアップ
for client in /Volumes/G-TECH/02_クライアント情報/*/; do
  if [ ! -f "${client}README.md" ]; then
    basename "$client"
  fi
done
```

### 5-2. README.mdテンプレートをコピー

```bash
# README.mdがないクライアントにテンプレートをコピー
for client in /Volumes/G-TECH/02_クライアント情報/*/; do
  clientname=$(basename "$client")

  # _で始まるフォルダと.gitフォルダを除外
  if [[ "$clientname" != _* ]] && [[ "$clientname" != .* ]] && [ "$clientname" != "ARCHIVE_完了・休眠" ]; then
    if [ ! -f "${client}README.md" ]; then
      cp "/Volumes/G-TECH/02_クライアント情報/_TEMPLATE/README.md" "${client}README.md"
    fi
  fi
done
```

### 検証

```bash
# README.mdの数を確認
find /Volumes/G-TECH/02_クライアント情報 -maxdepth 2 -name "README.md" -type f | \
  grep -v "_TEMPLATE" | grep -v "_共通資料" | grep -v "_ARCHIVE" | wc -l
# 期待値: 25（全クライアント）
```

---

## Step 6: 検証

### 6-1. 統一構造のプロジェクト数確認

```bash
# PROJECT.mdの総数確認
find "/Volumes/G-TECH/02_クライアント情報" -name "PROJECT.md" -type f | \
  grep -v "_TEMPLATE" | wc -l
# 期待値: 22以上（フェーズ1の17 + 黒澤工務店の5）
```

### 6-2. 00_COREフォルダの確認

```bash
# 00_COREフォルダが存在するクライアント数
find "/Volumes/G-TECH/02_クライアント情報" -maxdepth 2 -name "00_CORE" -type d | wc -l
# 期待値: 2以上（黒澤工務店、SKコーム、その他）
```

### 6-3. 代表的なクライアントの検証

```bash
# 黒澤工務店
ls "/Volumes/G-TECH/02_クライアント情報/黒澤工務店/" | head -10
# 期待値: 5プロジェクト + 00_CORE + README.md

# SKコーム
ls "/Volumes/G-TECH/02_クライアント情報/SKコーム/"
# 期待値: 顧問契約 + 00_CORE + README.md（存在する場合）

# AOMI100クリニック
ls "/Volumes/G-TECH/02_クライアント情報/AOMI100クリニック/"
# 期待値: 2025 + README.md
```

### 6-4. README.md配置確認

```bash
# 各クライアントにREADME.mdがあることを確認
for client in /Volumes/G-TECH/02_クライアント情報/*/; do
  clientname=$(basename "$client")
  if [[ "$clientname" != _* ]] && [[ "$clientname" != .* ]] && [ "$clientname" != "ARCHIVE_完了・休眠" ]; then
    if [ ! -f "${client}README.md" ]; then
      echo "README.md missing in: $clientname"
    fi
  fi
done
# 期待値: 何も出力されない（全クライアントにREADME.mdが存在）
```

---

## ✅ 完了チェックリスト

### Step 1: 既に統一構造のクライアント確認
- [ ] フェーズ1で作成した17プロジェクトの確認完了

### Step 2: 黒澤工務店の構造統一
- [ ] 00_COREフォルダ作成
- [ ] 5プロジェクトをトップレベルへ移動
- [ ] 機能別フォルダを00_COREへ移動
- [ ] ファイルを00_COREへ移動
- [ ] 各プロジェクトに統一構造を適用
- [ ] 検証完了

### Step 3: SKコームの構造統一
- [ ] 00_COREフォルダ作成
- [ ] 既存フォルダを00_COREへ移動（顧問契約除く）
- [ ] 検証完了

### Step 4: その他既存クライアントの整理
- [ ] 既存データを00_COREへ整理
- [ ] 検証完了

### Step 5: 全クライアントへのREADME.md追加
- [ ] README.mdがないクライアントを確認
- [ ] README.mdテンプレートをコピー
- [ ] 検証完了

### Step 6: 検証
- [ ] 統一構造のプロジェクト数確認
- [ ] 00_COREフォルダの確認
- [ ] 代表的なクライアントの検証
- [ ] README.md配置確認

---

## ⚠️ エラーハンドリング

### エラー1: ファイルが見つからない

```
mv: cannot stat '/path/to/file': No such file or directory
```

**対処法:**
1. パスを確認
2. `ls`コマンドで実際のフォルダ名を確認
3. 既に移動済みでないか確認
4. 警告として記録して続行

### エラー2: 移動先に同名フォルダが存在

```
mv: cannot move to '/path/to/destination/': Directory not empty
```

**対処法:**
1. 既存フォルダの内容を確認
2. 必要に応じてリネームして移動
3. 停止して報告

### エラー3: 権限エラー

```
mv: cannot move '/path/': Permission denied
```

**対処法:**
1. ファイルが開かれていないか確認
2. 停止して報告

---

## 📝 実行後の確認事項

### 1. git status確認

```bash
cd "/Volumes/G-TECH/02_クライアント情報"
git status
```

### 2. プロジェクト総数の確認

```bash
# PROJECT.mdの総数
find "/Volumes/G-TECH/02_クライアント情報" -name "PROJECT.md" -type f | \
  grep -v "_TEMPLATE" | wc -l
# 期待値: 22以上
```

### 3. git commit

```bash
cd "/Volumes/G-TECH/02_クライアント情報"
git add .
git commit -m "フェーズ3完了: 各クライアントの構造統一

【Step 1: 既に統一構造のクライアント確認】
- フェーズ1で作成した17プロジェクトを確認（変更なし）

【Step 2: 黒澤工務店の構造統一】
- 5プロジェクトをトップレベルへ移動
  - AI導入・DX推進
  - 業務提携（SKコーム）
  - 情報システム刷新
  - 人材・ビジネスマッチング
  - ミラリズム提案（不採用）
- 機能別フォルダ・ファイルを00_COREへ移動
- 各プロジェクトに統一構造を適用（PROJECT.md + 00_INPUT/01_OUTPUT/02_ARCHIVE）

【Step 3: SKコームの構造統一】
- 既存フォルダを00_COREへ移動（顧問契約プロジェクトは保持）
- 顧問契約プロジェクトは既に統一構造

【Step 4: その他既存クライアントの整理】
- 各クライアントの既存データを00_COREへ整理
- フェーズ1で作成したプロジェクトは保持

【Step 5: 全クライアントへのREADME.md追加】
- 25クライアント全てにREADME.mdを配置

【Step 6: 検証】
- 全検証項目クリア
- PROJECT.md総数: 22以上
- README.md総数: 25

【成果】
- 全クライアントが基本的な統一構造に
- 判断が必要なファイルは00_COREに保管（後で手動整理）
- 22以上のプロジェクトが統一構造

次のステップ: フェーズ4（AGOの移動）またはフェーズ5（_共通資料の最終整理）"
```

---

## 📌 重要な注意事項

### 00_COREフォルダについて

**目的:**
- 判断が必要なファイル・フォルダの一時保管
- 後で手動で各プロジェクトへ振り分け

**内容:**
- 黒澤工務店: コミュニケーション記録、ナレッジベース、契約・請求、年度フォルダ等
- SKコーム: 大橋邸、現場写真、請求書、会計資料等

**後での作業:**
- 00_CORE内のファイルを確認
- 該当するプロジェクトが分かれば、そのプロジェクトの00_INPUT/または01_OUTPUTへ移動
- どのプロジェクトにも属さない場合は00_COREに保持

---

## 次のステップ

フェーズ3完了後：
1. フェーズ4（AGOの移動）→ 実質不要（既にトップレベルにある）
2. フェーズ5（_共通資料の最終整理）→ 実行可能
3. または、00_COREフォルダ内のファイルを手動で整理
