# フェーズ2詳細実行ガイド（Cursor Composer用）

**作成日**: 2025年11月9日
**目的**: CORE/BIZ/PERSONALのフラット化を確実に実行するための詳細手順書

---

## ⚠️ 実行前の重要注意事項

### 1. フェーズ1の完了確認
```bash
# フェーズ1が完了していることを確認
git log --oneline -5
# 「フェーズ1完了」のコミットがあることを確認
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

## 📋 実行の全体フロー

```
Step 1: 事前準備（SKコーム問題の解決）
  ↓
Step 2: CORE_戦略的パートナーのフラット化（3クライアント）
  ↓
Step 3: BIZ_業種別クライアントのフラット化（15クライアント）
  ↓
Step 4: PERSONAL_個人顧客のフラット化（5クライアント）
  ↓
Step 5: 旧構造フォルダの_ARCHIVEへの移動
  ↓
Step 6: 検証
```

---

## Step 1: 事前準備（SKコーム問題の解決）

### 問題の説明
SKコームが2箇所に存在：
- `CORE_戦略的パートナー/SKコーム/`（新規作成、顧問契約プロジェクトのみ）
- `BIZ_業種別クライアント/建設・リフォーム/SKコーム/`（既存、大量データあり）

### 解決策
既存SKコーム（BIZ配下）をメインとし、CORE配下の顧問契約プロジェクトをマージ

### 1-1. 既存SKコームをトップレベルへ移動

```bash
# BIZ配下のSKコームをトップレベルへ移動
mv "/Volumes/G-TECH/02_クライアント情報/BIZ_業種別クライアント/建設・リフォーム/SKコーム" \
   "/Volumes/G-TECH/02_クライアント情報/SKコーム"
```

### 1-2. CORE配下の顧問契約プロジェクトをマージ

```bash
# CORE配下の顧問契約プロジェクトを既存SKコームへ移動
mv "/Volumes/G-TECH/02_クライアント情報/CORE_戦略的パートナー/SKコーム/顧問契約" \
   "/Volumes/G-TECH/02_クライアント情報/SKコーム/"
```

### 1-3. 空になったCORE配下のSKコームフォルダを削除

```bash
# 空フォルダを削除
rmdir "/Volumes/G-TECH/02_クライアント情報/CORE_戦略的パートナー/SKコーム"
```

### 1-4. 検証

```bash
# SKコームがトップレベルに存在することを確認
ls -la "/Volumes/G-TECH/02_クライアント情報/SKコーム/"

# 顧問契約プロジェクトが存在することを確認
ls -la "/Volumes/G-TECH/02_クライアント情報/SKコーム/顧問契約/"
```

---

## Step 2: CORE_戦略的パートナーのフラット化

### 移動対象クライアント（3社）

```bash
# 黒澤工務店
mv "/Volumes/G-TECH/02_クライアント情報/CORE_戦略的パートナー/黒澤工務店" \
   "/Volumes/G-TECH/02_クライアント情報/黒澤工務店"

# DOA
mv "/Volumes/G-TECH/02_クライアント情報/CORE_戦略的パートナー/DOA" \
   "/Volumes/G-TECH/02_クライアント情報/DOA"

# 翼ビジョン（堀内さん）
mv "/Volumes/G-TECH/02_クライアント情報/CORE_戦略的パートナー/翼ビジョン（堀内さん）" \
   "/Volumes/G-TECH/02_クライアント情報/翼ビジョン（堀内さん）"
```

### 検証

```bash
# 移動したクライアントが存在することを確認
ls -la "/Volumes/G-TECH/02_クライアント情報/" | grep "黒澤工務店\|DOA\|翼ビジョン"

# CORE_戦略的パートナーにREADME.mdのみが残っていることを確認
ls "/Volumes/G-TECH/02_クライアント情報/CORE_戦略的パートナー/"
```

---

## Step 3: BIZ_業種別クライアントのフラット化

### 3-1. 建設・リフォーム（3社）※SKコームは既に移動済み

```bash
# ジューテクノ
mv "/Volumes/G-TECH/02_クライアント情報/BIZ_業種別クライアント/建設・リフォーム/ジューテクノ" \
   "/Volumes/G-TECH/02_クライアント情報/ジューテクノ"

# 柳屋関連
mv "/Volumes/G-TECH/02_クライアント情報/BIZ_業種別クライアント/建設・リフォーム/柳屋関連" \
   "/Volumes/G-TECH/02_クライアント情報/柳屋関連"

# 猛建設
mv "/Volumes/G-TECH/02_クライアント情報/BIZ_業種別クライアント/建設・リフォーム/猛建設" \
   "/Volumes/G-TECH/02_クライアント情報/猛建設"
```

### 3-2. 不動産管理（5社）

```bash
# アストライズ
mv "/Volumes/G-TECH/02_クライアント情報/BIZ_業種別クライアント/不動産管理/アストライズ" \
   "/Volumes/G-TECH/02_クライアント情報/アストライズ"

# エトワール
mv "/Volumes/G-TECH/02_クライアント情報/BIZ_業種別クライアント/不動産管理/エトワール" \
   "/Volumes/G-TECH/02_クライアント情報/エトワール"

# ネクストドア
mv "/Volumes/G-TECH/02_クライアント情報/BIZ_業種別クライアント/不動産管理/ネクストドア" \
   "/Volumes/G-TECH/02_クライアント情報/ネクストドア"

# 信濃商事
mv "/Volumes/G-TECH/02_クライアント情報/BIZ_業種別クライアント/不動産管理/信濃商事" \
   "/Volumes/G-TECH/02_クライアント情報/信濃商事"

# 青柳不動産
mv "/Volumes/G-TECH/02_クライアント情報/BIZ_業種別クライアント/不動産管理/青柳不動産" \
   "/Volumes/G-TECH/02_クライアント情報/青柳不動産"
```

### 3-3. 店舗・飲食（3社）

```bash
# その他進行中プロジェクト
mv "/Volumes/G-TECH/02_クライアント情報/BIZ_業種別クライアント/店舗・飲食/その他進行中プロジェクト" \
   "/Volumes/G-TECH/02_クライアント情報/その他進行中プロジェクト"

# チア
mv "/Volumes/G-TECH/02_クライアント情報/BIZ_業種別クライアント/店舗・飲食/チア" \
   "/Volumes/G-TECH/02_クライアント情報/チア"

# AOMI100クリニック
mv "/Volumes/G-TECH/02_クライアント情報/BIZ_業種別クライアント/店舗・飲食/AOMI100クリニック" \
   "/Volumes/G-TECH/02_クライアント情報/AOMI100クリニック"
```

### 3-4. Web・IT（3社）

```bash
# 樋口様
mv "/Volumes/G-TECH/02_クライアント情報/BIZ_業種別クライアント/Web・IT/樋口様" \
   "/Volumes/G-TECH/02_クライアント情報/樋口様"

# cocomate
mv "/Volumes/G-TECH/02_クライアント情報/BIZ_業種別クライアント/Web・IT/cocomate" \
   "/Volumes/G-TECH/02_クライアント情報/cocomate"

# WEB屋喜作
mv "/Volumes/G-TECH/02_クライアント情報/BIZ_業種別クライアント/Web・IT/WEB屋喜作" \
   "/Volumes/G-TECH/02_クライアント情報/WEB屋喜作"
```

### 3-5. 卸売・小売・商社（1社）

```bash
# 東京医療商事
mv "/Volumes/G-TECH/02_クライアント情報/BIZ_業種別クライアント/卸売・小売・商社/東京医療商事" \
   "/Volumes/G-TECH/02_クライアント情報/東京医療商事"
```

### 検証

```bash
# BIZの各業種フォルダが空であることを確認
ls "/Volumes/G-TECH/02_クライアント情報/BIZ_業種別クライアント/建設・リフォーム/"
ls "/Volumes/G-TECH/02_クライアント情報/BIZ_業種別クライアント/不動産管理/"
ls "/Volumes/G-TECH/02_クライアント情報/BIZ_業種別クライアント/店舗・飲食/"
ls "/Volumes/G-TECH/02_クライアント情報/BIZ_業種別クライアント/Web・IT/"
ls "/Volumes/G-TECH/02_クライアント情報/BIZ_業種別クライアント/卸売・小売・商社/"
# 期待値: 空（0ファイル・0フォルダ）
```

---

## Step 4: PERSONAL_個人顧客のフラット化

### 移動対象クライアント（5名）

```bash
# ムラカミリョウ
mv "/Volumes/G-TECH/02_クライアント情報/PERSONAL_個人顧客/ムラカミリョウ" \
   "/Volumes/G-TECH/02_クライアント情報/ムラカミリョウ"

# 吉沼
mv "/Volumes/G-TECH/02_クライアント情報/PERSONAL_個人顧客/吉沼" \
   "/Volumes/G-TECH/02_クライアント情報/吉沼"

# 富田みよこ
mv "/Volumes/G-TECH/02_クライアント情報/PERSONAL_個人顧客/富田みよこ" \
   "/Volumes/G-TECH/02_クライアント情報/富田みよこ"

# 東野真由美
mv "/Volumes/G-TECH/02_クライアント情報/PERSONAL_個人顧客/東野真由美" \
   "/Volumes/G-TECH/02_クライアント情報/東野真由美"

# 渡邉みい
mv "/Volumes/G-TECH/02_クライアント情報/PERSONAL_個人顧客/渡邉みい" \
   "/Volumes/G-TECH/02_クライアント情報/渡邉みい"
```

### 検証

```bash
# PERSONAL_個人顧客にREADME.mdのみが残っていることを確認
ls "/Volumes/G-TECH/02_クライアント情報/PERSONAL_個人顧客/"
# 期待値: README.md のみ
```

---

## Step 5: 旧構造フォルダの_ARCHIVEへの移動

### 5-1. _ARCHIVE/旧構造フォルダの作成

```bash
mkdir -p "/Volumes/G-TECH/02_クライアント情報/_ARCHIVE/20251109_旧構造"
```

### 5-2. 旧構造フォルダの移動

```bash
# CORE_戦略的パートナー（README.mdのみ残っている）
mv "/Volumes/G-TECH/02_クライアント情報/CORE_戦略的パートナー" \
   "/Volumes/G-TECH/02_クライアント情報/_ARCHIVE/20251109_旧構造/"

# BIZ_業種別クライアント（空の業種フォルダとREADME.mdのみ）
mv "/Volumes/G-TECH/02_クライアント情報/BIZ_業種別クライアント" \
   "/Volumes/G-TECH/02_クライアント情報/_ARCHIVE/20251109_旧構造/"

# PERSONAL_個人顧客（README.mdのみ残っている）
mv "/Volumes/G-TECH/02_クライアント情報/PERSONAL_個人顧客" \
   "/Volumes/G-TECH/02_クライアント情報/_ARCHIVE/20251109_旧構造/"
```

### 検証

```bash
# 旧構造フォルダが_ARCHIVEに存在することを確認
ls "/Volumes/G-TECH/02_クライアント情報/_ARCHIVE/20251109_旧構造/"
# 期待値: CORE_戦略的パートナー, BIZ_業種別クライアント, PERSONAL_個人顧客
```

---

## Step 6: 検証

### 6-1. トップレベルのクライアント数を確認

```bash
# トップレベルのクライアントフォルダ数をカウント
ls -d /Volumes/G-TECH/02_クライアント情報/*/ 2>/dev/null | \
  grep -v "^_" | \
  grep -v ".git" | \
  grep -v "CORE" | \
  grep -v "BIZ" | \
  grep -v "PERSONAL" | \
  grep -v "ARCHIVE" | \
  wc -l
# 期待値: 26（全クライアント）
```

### 6-2. 旧構造フォルダが存在しないことを確認

```bash
# CORE/BIZ/PERSONALフォルダが存在しないことを確認
ls /Volumes/G-TECH/02_クライアント情報/ | grep "^CORE\|^BIZ\|^PERSONAL"
# 期待値: 空（何も表示されない）
```

### 6-3. SKコームの検証

```bash
# SKコームがトップレベルに存在
ls -la "/Volumes/G-TECH/02_クライアント情報/SKコーム/"

# 顧問契約プロジェクトが存在
ls "/Volumes/G-TECH/02_クライアント情報/SKコーム/" | grep "顧問契約"

# 既存のプロジェクトフォルダも存在
ls "/Volumes/G-TECH/02_クライアント情報/SKコーム/" | grep -E "01_契約・見積|02_請求書|03_プロジェクト資料"
```

### 6-4. 代表的なクライアントの検証

```bash
# 黒澤工務店
ls "/Volumes/G-TECH/02_クライアント情報/黒澤工務店/" | head -5

# AOMI100クリニック
ls "/Volumes/G-TECH/02_クライアント情報/AOMI100クリニック/" | head -5

# ムラカミリョウ
ls "/Volumes/G-TECH/02_クライアント情報/ムラカミリョウ/" | head -5
```

---

## ✅ 完了チェックリスト

### Step 1: SKコーム問題の解決
- [ ] 既存SKコームをトップレベルへ移動
- [ ] CORE配下の顧問契約プロジェクトをマージ
- [ ] 空フォルダを削除
- [ ] 検証完了

### Step 2: CORE_戦略的パートナーのフラット化
- [ ] 黒澤工務店を移動
- [ ] DOAを移動
- [ ] 翼ビジョン（堀内さん）を移動
- [ ] 検証完了

### Step 3: BIZ_業種別クライアントのフラット化
- [ ] 建設・リフォーム（3社）を移動
- [ ] 不動産管理（5社）を移動
- [ ] 店舗・飲食（3社）を移動
- [ ] Web・IT（3社）を移動
- [ ] 卸売・小売・商社（1社）を移動
- [ ] 検証完了

### Step 4: PERSONAL_個人顧客のフラット化
- [ ] 5名を移動
- [ ] 検証完了

### Step 5: 旧構造フォルダの_ARCHIVEへの移動
- [ ] _ARCHIVE/20251109_旧構造フォルダ作成
- [ ] CORE/BIZ/PERSONALフォルダを移動
- [ ] 検証完了

### Step 6: 検証
- [ ] トップレベルのクライアント数: 26
- [ ] 旧構造フォルダが存在しない
- [ ] SKコームの検証
- [ ] 代表的なクライアントの検証

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

### エラー2: 移動先に同名フォルダが存在

```
mv: cannot move to '/path/to/destination/': Directory not empty
```

**対処法:**
1. 既存フォルダの内容を確認
2. 必要に応じてマージまたはリネーム
3. SKコーム以外でこのエラーが出た場合は停止して報告

### エラー3: 権限エラー

```
mv: cannot move '/path/': Permission denied
```

**対処法:**
1. ファイルが開かれていないか確認
2. 必要に応じて`sudo`を使用（非推奨）

---

## 📝 実行後の確認事項

### 1. git status確認

```bash
cd "/Volumes/G-TECH/02_クライアント情報"
git status
```

### 2. 移動したクライアント数の確認

```bash
# トップレベルのクライアント数
ls -d /Volumes/G-TECH/02_クライアント情報/*/ 2>/dev/null | \
  grep -v "^_" | grep -v ".git" | wc -l
# 期待値: 26
```

### 3. git commit

```bash
cd "/Volumes/G-TECH/02_クライアント情報"
git add .
git commit -m "フェーズ2完了: CORE/BIZ/PERSONALのフラット化

【Step 1: SKコーム問題の解決】
- 既存SKコーム（BIZ配下）をトップレベルへ移動
- CORE配下の顧問契約プロジェクトをマージ
- 空フォルダを削除

【Step 2: CORE_戦略的パートナーのフラット化】
- 3クライアントをトップレベルへ移動
  - 黒澤工務店
  - DOA
  - 翼ビジョン（堀内さん）

【Step 3: BIZ_業種別クライアントのフラット化】
- 15クライアントをトップレベルへ移動
  - 建設・リフォーム: 3社
  - 不動産管理: 5社
  - 店舗・飲食: 3社
  - Web・IT: 3社
  - 卸売・小売・商社: 1社

【Step 4: PERSONAL_個人顧客のフラット化】
- 5名をトップレベルへ移動

【Step 5: 旧構造フォルダの_ARCHIVEへの移動】
- CORE_戦略的パートナー → _ARCHIVE/20251109_旧構造/
- BIZ_業種別クライアント → _ARCHIVE/20251109_旧構造/
- PERSONAL_個人顧客 → _ARCHIVE/20251109_旧構造/

【Step 6: 検証】
- 全検証項目クリア
- トップレベルのクライアント数: 26

【成果】
- 全クライアントがトップレベルにフラット配置
- 旧構造フォルダを_ARCHIVEに保管
- SKコーム重複問題を解決

次のステップ: フェーズ3（各クライアントの構造統一）"
```

---

## 次のステップ

フェーズ2完了後：
1. `リポジトリ再構築計画.md` のフェーズ3へ進む
2. 各クライアントの構造統一を実行
