# フェーズ1詳細実行ガイド（Cursor Composer用）

**作成日**: 2025年11月8日
**目的**: _共通資料フォルダの仕分けを確実に実行するための詳細手順書

---

## ⚠️ 実行前の重要注意事項

### 1. バックアップ確認
```bash
# 実行前に必ず旧構造をバックアップ
cp -r "/Volumes/G-TECH/02_クライアント情報/_共通資料" \
      "/Volumes/G-TECH/02_クライアント情報/_BACKUP_共通資料_20251108"
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
Step 1: 新規クライアントフォルダ作成
  ↓
Step 2: ビジネス書類の移動（見積書・請求書・契約書）
  ↓
Step 3: 個人データの_ARCHIVEへの移動
  ↓
Step 4: 特定クライアント名フォルダの移動
  ↓
Step 5: 仕分け待ちフォルダへの移動
  ↓
Step 6: 検証
```

---

## Step 1: 新規クライアントフォルダ作成

### 1-1. 法人クライアント（10社）

```bash
# SKコーム
mkdir -p "/Volumes/G-TECH/02_クライアント情報/CORE_戦略的パートナー/SKコーム/顧問契約"/{00_INPUT,01_OUTPUT,02_ARCHIVE}
mkdir -p "/Volumes/G-TECH/02_クライアント情報/CORE_戦略的パートナー/SKコーム/顧問契約/01_OUTPUT"/{クライアント向け,内部用}
cp "/Volumes/G-TECH/02_クライアント情報/_TEMPLATE/PROJECT_TEMPLATE/PROJECT.md" \
   "/Volumes/G-TECH/02_クライアント情報/CORE_戦略的パートナー/SKコーム/顧問契約/"

# 東京医療商事
mkdir -p "/Volumes/G-TECH/02_クライアント情報/BIZ_業種別クライアント/卸売・小売・商社/東京医療商事/事務所内装工事"/{00_INPUT,01_OUTPUT,02_ARCHIVE}
mkdir -p "/Volumes/G-TECH/02_クライアント情報/BIZ_業種別クライアント/卸売・小売・商社/東京医療商事/事務所内装工事/01_OUTPUT/クライアント向け/見積書"
cp "/Volumes/G-TECH/02_クライアント情報/_TEMPLATE/PROJECT_TEMPLATE/PROJECT.md" \
   "/Volumes/G-TECH/02_クライアント情報/BIZ_業種別クライアント/卸売・小売・商社/東京医療商事/事務所内装工事/"

# アストライズ（既存クライアントだが、プロジェクトフォルダは新規）
mkdir -p "/Volumes/G-TECH/02_クライアント情報/BIZ_業種別クライアント/不動産管理/アストライズ/池田山コープ改修工事"/{00_INPUT,01_OUTPUT,02_ARCHIVE}
mkdir -p "/Volumes/G-TECH/02_クライアント情報/BIZ_業種別クライアント/不動産管理/アストライズ/池田山コープ改修工事/01_OUTPUT/クライアント向け/見積書"
cp "/Volumes/G-TECH/02_クライアント情報/_TEMPLATE/PROJECT_TEMPLATE/PROJECT.md" \
   "/Volumes/G-TECH/02_クライアント情報/BIZ_業種別クライアント/不動産管理/アストライズ/池田山コープ改修工事/"

# ジューテクノ（2プロジェクト）
mkdir -p "/Volumes/G-TECH/02_クライアント情報/BIZ_業種別クライアント/建設・リフォーム/ジューテクノ/takaraキッチン工事"/{00_INPUT,01_OUTPUT,02_ARCHIVE}
mkdir -p "/Volumes/G-TECH/02_クライアント情報/BIZ_業種別クライアント/建設・リフォーム/ジューテクノ/takaraキッチン工事/01_OUTPUT/クライアント向け/見積書"
cp "/Volumes/G-TECH/02_クライアント情報/_TEMPLATE/PROJECT_TEMPLATE/PROJECT.md" \
   "/Volumes/G-TECH/02_クライアント情報/BIZ_業種別クライアント/建設・リフォーム/ジューテクノ/takaraキッチン工事/"

mkdir -p "/Volumes/G-TECH/02_クライアント情報/BIZ_業種別クライアント/建設・リフォーム/ジューテクノ/練馬区リフォーム工事"/{00_INPUT,01_OUTPUT,02_ARCHIVE}
mkdir -p "/Volumes/G-TECH/02_クライアント情報/BIZ_業種別クライアント/建設・リフォーム/ジューテクノ/練馬区リフォーム工事/01_OUTPUT/クライアント向け/見積書"
cp "/Volumes/G-TECH/02_クライアント情報/_TEMPLATE/PROJECT_TEMPLATE/PROJECT.md" \
   "/Volumes/G-TECH/02_クライアント情報/BIZ_業種別クライアント/建設・リフォーム/ジューテクノ/練馬区リフォーム工事/"

# ネクストドア
mkdir -p "/Volumes/G-TECH/02_クライアント情報/BIZ_業種別クライアント/不動産管理/ネクストドア/ユニビル2階事務所改修工事"/{00_INPUT,01_OUTPUT,02_ARCHIVE}
mkdir -p "/Volumes/G-TECH/02_クライアント情報/BIZ_業種別クライアント/不動産管理/ネクストドア/ユニビル2階事務所改修工事/01_OUTPUT/クライアント向け/見積書"
cp "/Volumes/G-TECH/02_クライアント情報/_TEMPLATE/PROJECT_TEMPLATE/PROJECT.md" \
   "/Volumes/G-TECH/02_クライアント情報/BIZ_業種別クライアント/不動産管理/ネクストドア/ユニビル2階事務所改修工事/"

# 猛建設
mkdir -p "/Volumes/G-TECH/02_クライアント情報/BIZ_業種別クライアント/建設・リフォーム/猛建設/ラ・アトレ横濱鶴見Ⅱ 6階改修工事"/{00_INPUT,01_OUTPUT,02_ARCHIVE}
mkdir -p "/Volumes/G-TECH/02_クライアント情報/BIZ_業種別クライアント/建設・リフォーム/猛建設/ラ・アトレ横濱鶴見Ⅱ 6階改修工事/01_OUTPUT/クライアント向け/見積書"
cp "/Volumes/G-TECH/02_クライアント情報/_TEMPLATE/PROJECT_TEMPLATE/PROJECT.md" \
   "/Volumes/G-TECH/02_クライアント情報/BIZ_業種別クライアント/建設・リフォーム/猛建設/ラ・アトレ横濱鶴見Ⅱ 6階改修工事/"

# 青柳不動産
mkdir -p "/Volumes/G-TECH/02_クライアント情報/BIZ_業種別クライアント/不動産管理/青柳不動産/フォレストコート小竹104号室改修工事"/{00_INPUT,01_OUTPUT,02_ARCHIVE}
mkdir -p "/Volumes/G-TECH/02_クライアント情報/BIZ_業種別クライアント/不動産管理/青柳不動産/フォレストコート小竹104号室改修工事/01_OUTPUT/クライアント向け/見積書"
cp "/Volumes/G-TECH/02_クライアント情報/_TEMPLATE/PROJECT_TEMPLATE/PROJECT.md" \
   "/Volumes/G-TECH/02_クライアント情報/BIZ_業種別クライアント/不動産管理/青柳不動産/フォレストコート小竹104号室改修工事/"

# 信濃商事
mkdir -p "/Volumes/G-TECH/02_クライアント情報/BIZ_業種別クライアント/不動産管理/信濃商事/信濃ビル8階漏電ブレーカー交換工事"/{00_INPUT,01_OUTPUT,02_ARCHIVE}
mkdir -p "/Volumes/G-TECH/02_クライアント情報/BIZ_業種別クライアント/不動産管理/信濃商事/信濃ビル8階漏電ブレーカー交換工事/01_OUTPUT/クライアント向け/請求書"
cp "/Volumes/G-TECH/02_クライアント情報/_TEMPLATE/PROJECT_TEMPLATE/PROJECT.md" \
   "/Volumes/G-TECH/02_クライアント情報/BIZ_業種別クライアント/不動産管理/信濃商事/信濃ビル8階漏電ブレーカー交換工事/"

# チア
mkdir -p "/Volumes/G-TECH/02_クライアント情報/BIZ_業種別クライアント/店舗・飲食/チア/チア2号店改修工事"/{00_INPUT,01_OUTPUT,02_ARCHIVE}
mkdir -p "/Volumes/G-TECH/02_クライアント情報/BIZ_業種別クライアント/店舗・飲食/チア/チア2号店改修工事/00_INPUT/工程表"
cp "/Volumes/G-TECH/02_クライアント情報/_TEMPLATE/PROJECT_TEMPLATE/PROJECT.md" \
   "/Volumes/G-TECH/02_クライアント情報/BIZ_業種別クライアント/店舗・飲食/チア/チア2号店改修工事/"

# cocomate（2プロジェクト）
mkdir -p "/Volumes/G-TECH/02_クライアント情報/BIZ_業種別クライアント/Web・IT/cocomate/ロゴデザイン・ブランディング"/{00_INPUT,01_OUTPUT,02_ARCHIVE}
mkdir -p "/Volumes/G-TECH/02_クライアント情報/BIZ_業種別クライアント/Web・IT/cocomate/ロゴデザイン・ブランディング/00_INPUT/ロゴ・デザイン素材"
cp "/Volumes/G-TECH/02_クライアント情報/_TEMPLATE/PROJECT_TEMPLATE/PROJECT.md" \
   "/Volumes/G-TECH/02_クライアント情報/BIZ_業種別クライアント/Web・IT/cocomate/ロゴデザイン・ブランディング/"

mkdir -p "/Volumes/G-TECH/02_クライアント情報/BIZ_業種別クライアント/Web・IT/cocomate/ROBOT PAYMENT決済サービス導入"/{00_INPUT,01_OUTPUT,02_ARCHIVE}
mkdir -p "/Volumes/G-TECH/02_クライアント情報/BIZ_業種別クライアント/Web・IT/cocomate/ROBOT PAYMENT決済サービス導入/01_OUTPUT/クライアント向け"/{契約書,請求書}
cp "/Volumes/G-TECH/02_クライアント情報/_TEMPLATE/PROJECT_TEMPLATE/PROJECT.md" \
   "/Volumes/G-TECH/02_クライアント情報/BIZ_業種別クライアント/Web・IT/cocomate/ROBOT PAYMENT決済サービス導入/"
```

### 1-2. 個人顧客（3名）

```bash
# 吉沼
mkdir -p "/Volumes/G-TECH/02_クライアント情報/PERSONAL_個人顧客/吉沼/クレーヌ吉沼505号室改修工事"/{00_INPUT,01_OUTPUT,02_ARCHIVE}
mkdir -p "/Volumes/G-TECH/02_クライアント情報/PERSONAL_個人顧客/吉沼/クレーヌ吉沼505号室改修工事/01_OUTPUT/クライアント向け/見積書"
cp "/Volumes/G-TECH/02_クライアント情報/_TEMPLATE/PROJECT_TEMPLATE/PROJECT.md" \
   "/Volumes/G-TECH/02_クライアント情報/PERSONAL_個人顧客/吉沼/クレーヌ吉沼505号室改修工事/"

# 富田みよこ
mkdir -p "/Volumes/G-TECH/02_クライアント情報/PERSONAL_個人顧客/富田みよこ/富田邸リフォーム工事"/{00_INPUT,01_OUTPUT,02_ARCHIVE}
mkdir -p "/Volumes/G-TECH/02_クライアント情報/PERSONAL_個人顧客/富田みよこ/富田邸リフォーム工事/01_OUTPUT/クライアント向け/見積書"
cp "/Volumes/G-TECH/02_クライアント情報/_TEMPLATE/PROJECT_TEMPLATE/PROJECT.md" \
   "/Volumes/G-TECH/02_クライアント情報/PERSONAL_個人顧客/富田みよこ/富田邸リフォーム工事/"

# 東野真由美
mkdir -p "/Volumes/G-TECH/02_クライアント情報/PERSONAL_個人顧客/東野真由美/東野邸玄関鏡設置工事"/{00_INPUT,01_OUTPUT,02_ARCHIVE}
mkdir -p "/Volumes/G-TECH/02_クライアント情報/PERSONAL_個人顧客/東野真由美/東野邸玄関鏡設置工事/01_OUTPUT/クライアント向け/見積書"
cp "/Volumes/G-TECH/02_クライアント情報/_TEMPLATE/PROJECT_TEMPLATE/PROJECT.md" \
   "/Volumes/G-TECH/02_クライアント情報/PERSONAL_個人顧客/東野真由美/東野邸玄関鏡設置工事/"
```

### 1-3. AGO（1プロジェクト）

```bash
# AGO/就業規則作成支援
mkdir -p "/Volumes/G-TECH/02_クライアント情報/AGO/就業規則作成支援"/{00_INPUT,01_OUTPUT,02_ARCHIVE}
mkdir -p "/Volumes/G-TECH/02_クライアント情報/AGO/就業規則作成支援/01_OUTPUT/クライアント向け/規程・規則"
cp "/Volumes/G-TECH/02_クライアント情報/_TEMPLATE/PROJECT_TEMPLATE/PROJECT.md" \
   "/Volumes/G-TECH/02_クライアント情報/AGO/就業規則作成支援/"
```

### 1-4. 個人データ用フォルダ

```bash
# 個人データ保管用
mkdir -p "/Volumes/G-TECH/02_クライアント情報/_ARCHIVE/個人データ/末武修平/税務関連/2022年度"
mkdir -p "/Volumes/G-TECH/02_クライアント情報/_ARCHIVE/個人データ/末武家/学童関連"/{さいたま市尾間木,うめ}
mkdir -p "/Volumes/G-TECH/02_クライアント情報/_ARCHIVE/個人データ/LINEトーク履歴/AGO関連"
```

### 1-5. 仕分け待ちフォルダ

```bash
mkdir -p "/Volumes/G-TECH/02_クライアント情報/_共通資料/_ARCHIVE/20251108_仕分け待ち"
```

---

## Step 2: ビジネス書類の移動

### 2-1. 見積書の移動

```bash
# サンフィールド医院（AOMI100クリニック）
mv "/Volumes/G-TECH/02_クライアント情報/_共通資料/ビジネス書類/見積書/サンフィールド医院御中_見積書_251007-1.pdf" \
   "/Volumes/G-TECH/02_クライアント情報/BIZ_業種別クライアント/店舗・飲食/AOMI100クリニック/2025/サイン・床・壁張り替え工事/01_OUTPUT/クライアント向け/見積書/"

# 吉沼様
mv "/Volumes/G-TECH/02_クライアント情報/_共通資料/ビジネス書類/見積書/吉沼様_クレーヌ吉沼505号室改修工事プラン_見積書_20241010_11 (1).pdf" \
   "/Volumes/G-TECH/02_クライアント情報/PERSONAL_個人顧客/吉沼/クレーヌ吉沼505号室改修工事/01_OUTPUT/クライアント向け/見積書/"

# 富田みよこ様
mv "/Volumes/G-TECH/02_クライアント情報/_共通資料/ビジネス書類/見積書/富田　みよこ様_富田邸リホーム工事_見積書_２４１１２９.pdf" \
   "/Volumes/G-TECH/02_クライアント情報/PERSONAL_個人顧客/富田みよこ/富田邸リフォーム工事/01_OUTPUT/クライアント向け/見積書/"

# 東京医療商事
mv "/Volumes/G-TECH/02_クライアント情報/_共通資料/ビジネス書類/見積書/東京医療商事　株式会社御中_事務所内装工事_見積書_240608-1 (1).pdf" \
   "/Volumes/G-TECH/02_クライアント情報/BIZ_業種別クライアント/卸売・小売・商社/東京医療商事/事務所内装工事/01_OUTPUT/クライアント向け/見積書/"

# 東野真由美様
mv "/Volumes/G-TECH/02_クライアント情報/_共通資料/ビジネス書類/見積書/東野真由美様_東野邸　玄関鏡設置工事　2024年12月_見積書_Q-0000000001.pdf" \
   "/Volumes/G-TECH/02_クライアント情報/PERSONAL_個人顧客/東野真由美/東野邸玄関鏡設置工事/01_OUTPUT/クライアント向け/見積書/"

# アストライズ
mv "/Volumes/G-TECH/02_クライアント情報/_共通資料/ビジネス書類/見積書/株式会社アストライズ御中_池田山コープ_見積書_２４１０１１－１.pdf" \
   "/Volumes/G-TECH/02_クライアント情報/BIZ_業種別クライアント/不動産管理/アストライズ/池田山コープ改修工事/01_OUTPUT/クライアント向け/見積書/"

# ジューテクノ（2件）
mv "/Volumes/G-TECH/02_クライアント情報/_共通資料/ビジネス書類/見積書/株式会社ジューテクノ御中_takaraキッチン_見積書_240822-3.pdf" \
   "/Volumes/G-TECH/02_クライアント情報/BIZ_業種別クライアント/建設・リフォーム/ジューテクノ/takaraキッチン工事/01_OUTPUT/クライアント向け/見積書/"

mv "/Volumes/G-TECH/02_クライアント情報/_共通資料/ビジネス書類/見積書/株式会社ジューテクノ御中_練馬区リフォーム工事_見積書_20240805_11 (1).pdf" \
   "/Volumes/G-TECH/02_クライアント情報/BIZ_業種別クライアント/建設・リフォーム/ジューテクノ/練馬区リフォーム工事/01_OUTPUT/クライアント向け/見積書/"

# ネクストドア
mv "/Volumes/G-TECH/02_クライアント情報/_共通資料/ビジネス書類/見積書/株式会社ネクストドア御中_ユニビル2階事務所改修工事_見積書_20241125_11 (1).pdf" \
   "/Volumes/G-TECH/02_クライアント情報/BIZ_業種別クライアント/不動産管理/ネクストドア/ユニビル2階事務所改修工事/01_OUTPUT/クライアント向け/見積書/"

# 猛建設（重複処理：最新版のみ移動）
mv "/Volumes/G-TECH/02_クライアント情報/_共通資料/ビジネス書類/見積書/株式会社猛建設_ラ・アトレ横濱鶴見Ⅱ　6階 2025年1月_見積書_Q-0000000002.pdf" \
   "/Volumes/G-TECH/02_クライアント情報/BIZ_業種別クライアント/建設・リフォーム/猛建設/ラ・アトレ横濱鶴見Ⅱ 6階改修工事/01_OUTPUT/クライアント向け/見積書/"

# 猛建設の旧見積書
mv "/Volumes/G-TECH/02_クライアント情報/_共通資料/ビジネス書類/見積書/ラ・アトレ横濱鶴見Ⅱ　6階見積もり.pdf" \
   "/Volumes/G-TECH/02_クライアント情報/BIZ_業種別クライアント/建設・リフォーム/猛建設/ラ・アトレ横濱鶴見Ⅱ 6階改修工事/02_ARCHIVE/"

# 青柳不動産（重複処理：最新版のみ移動）
mv "/Volumes/G-TECH/02_クライアント情報/_共通資料/ビジネス書類/見積書/青柳不動産株式会社御中_フォレストコート小竹104号室_改修工事_見積書_Q-0000000012.pdf" \
   "/Volumes/G-TECH/02_クライアント情報/BIZ_業種別クライアント/不動産管理/青柳不動産/フォレストコート小竹104号室改修工事/01_OUTPUT/クライアント向け/見積書/"

# 不明な見積書（仕分け待ちへ）
mv "/Volumes/G-TECH/02_クライアント情報/_共通資料/ビジネス書類/見積書/お見積書-1.pdf" \
   "/Volumes/G-TECH/02_クライアント情報/_共通資料/_ARCHIVE/20251108_仕分け待ち/"

# 重複ファイルの削除
rm "/Volumes/G-TECH/02_クライアント情報/_共通資料/ビジネス書類/見積書/株式会社猛建設_ラ・アトレ横濱鶴見Ⅱ　6階 2025年1月_見積書_Q-0000000002 (1).pdf"
rm "/Volumes/G-TECH/02_クライアント情報/_共通資料/ビジネス書類/見積書/青柳不動産株式会社御中_フォレストコート小竹104号室_改修工事_見積書_Q-0000000012 (1).pdf"
```

### 2-2. 請求書の移動

```bash
# 信濃商事
mv "/Volumes/G-TECH/02_クライアント情報/_共通資料/ビジネス書類/請求書/信濃商事　株式会社御中_信濃ビル8階　漏電ブレーカー交換工事_請求書_INV-0000000004.pdf" \
   "/Volumes/G-TECH/02_クライアント情報/BIZ_業種別クライアント/不動産管理/信濃商事/信濃ビル8階漏電ブレーカー交換工事/01_OUTPUT/クライアント向け/請求書/"

# 不明な請求書（仕分け待ちへ）
mv "/Volumes/G-TECH/02_クライアント情報/_共通資料/ビジネス書類/請求書/05008166_00428926_2025年03月31日請求分.pdf" \
   "/Volumes/G-TECH/02_クライアント情報/_共通資料/_ARCHIVE/20251108_仕分け待ち/"

mv "/Volumes/G-TECH/02_クライアント情報/_共通資料/ビジネス書類/請求書/4月度請求書.pdf" \
   "/Volumes/G-TECH/02_クライアント情報/_共通資料/_ARCHIVE/20251108_仕分け待ち/"

mv "/Volumes/G-TECH/02_クライアント情報/_共通資料/ビジネス書類/請求書/請求書202503.pdf" \
   "/Volumes/G-TECH/02_クライアント情報/_共通資料/_ARCHIVE/20251108_仕分け待ち/"

mv "/Volumes/G-TECH/02_クライアント情報/_共通資料/ビジネス書類/請求書/請求書_20250117(1).pdf" \
   "/Volumes/G-TECH/02_クライアント情報/_共通資料/_ARCHIVE/20251108_仕分け待ち/"
```

### 2-3. 契約書の移動

```bash
# SKコーム
mv "/Volumes/G-TECH/02_クライアント情報/_共通資料/ビジネス書類/契約書/794 ㈱ＳＫコーム 顧問契約書_20250804.pdf" \
   "/Volumes/G-TECH/02_クライアント情報/CORE_戦略的パートナー/SKコーム/顧問契約/01_OUTPUT/クライアント向け/"

# 不明な契約書（仕分け待ちへ）
mv "/Volumes/G-TECH/02_クライアント情報/_共通資料/ビジネス書類/契約書/AI議事録講義_契約書.pdf" \
   "/Volumes/G-TECH/02_クライアント情報/_共通資料/_ARCHIVE/20251108_仕分け待ち/"

mv "/Volumes/G-TECH/02_クライアント情報/_共通資料/ビジネス書類/契約書/契約書.pdf" \
   "/Volumes/G-TECH/02_クライアント情報/_共通資料/_ARCHIVE/20251108_仕分け待ち/"

mv "/Volumes/G-TECH/02_クライアント情報/_共通資料/ビジネス書類/契約書/業務提携契約書.pdf" \
   "/Volumes/G-TECH/02_クライアント情報/_共通資料/_ARCHIVE/20251108_仕分け待ち/"

mv "/Volumes/G-TECH/02_クライアント情報/_共通資料/ビジネス書類/契約書/議事録AI活用マスタープログラム契約書_記名済.pdf" \
   "/Volumes/G-TECH/02_クライアント情報/_共通資料/_ARCHIVE/20251108_仕分け待ち/"

# 法的参考資料は共通資料に残す（移動しない）
# - 日本のリフォーム工事契約における実務的要素の包括的ガイド：標準工事・保証・地域規制.pdf
# - 日本のリフォーム工事契約に関する法的枠組みと実務ガイドライン：2025年最新動向.pdf
# - 日本のリフォーム工事請負契約書作成の包括的ガイド：法的要件と実務的アプローチ.pdf
```

---

## Step 3: 個人データの_ARCHIVEへの移動

```bash
# 末武修平 税務関連
mv "/Volumes/G-TECH/02_クライアント情報/_共通資料/ビジネス書類/請求書/20220313請求書（末武様）.pdf" \
   "/Volumes/G-TECH/02_クライアント情報/_ARCHIVE/個人データ/末武修平/税務関連/2022年度/"

mv "/Volumes/G-TECH/02_クライアント情報/_共通資料/ビジネス書類/請求書/末武　修平様_法律文書作成_請求書_INV-0000000268.pdf" \
   "/Volumes/G-TECH/02_クライアント情報/_ARCHIVE/個人データ/末武修平/法律関連/"

# 20220313（末武様）フォルダごと
mv "/Volumes/G-TECH/02_クライアント情報/_共通資料/20220313（末武様）" \
   "/Volumes/G-TECH/02_クライアント情報/_ARCHIVE/個人データ/末武修平/税務関連/2022年度/"

# 学童資料
mv "/Volumes/G-TECH/02_クライアント情報/_共通資料/学童資料（さい）" \
   "/Volumes/G-TECH/02_クライアント情報/_ARCHIVE/個人データ/末武家/学童関連/さいたま市尾間木/"

mv "/Volumes/G-TECH/02_クライアント情報/_共通資料/学童資料（うめ）" \
   "/Volumes/G-TECH/02_クライアント情報/_ARCHIVE/個人データ/末武家/学童関連/うめ/"

# LINEトーク履歴
mv "/Volumes/G-TECH/02_クライアント情報/_共通資料/LINEトーク履歴_四ノ宮" \
   "/Volumes/G-TECH/02_クライアント情報/_ARCHIVE/個人データ/LINEトーク履歴/AGO関連/"
```

---

## Step 4: 特定クライアント名フォルダの移動

```bash
# cocomateロゴ（フォルダごと）
mv "/Volumes/G-TECH/02_クライアント情報/_共通資料/cocomateロゴ" \
   "/Volumes/G-TECH/02_クライアント情報/BIZ_業種別クライアント/Web・IT/cocomate/ロゴデザイン・ブランディング/00_INPUT/ロゴ・デザイン素材/"

# アストライズ（フォルダごと）
mv "/Volumes/G-TECH/02_クライアント情報/_共通資料/アストライズ" \
   "/Volumes/G-TECH/02_クライアント情報/BIZ_業種別クライアント/不動産管理/アストライズ/00_CORE/財務・会計/"

# AGO就業規則（フォルダごと）
mv "/Volumes/G-TECH/02_クライアント情報/_共通資料/【㈱AGOグループ様】就業規則-Draft版" \
   "/Volumes/G-TECH/02_クライアント情報/AGO/就業規則作成支援/01_OUTPUT/クライアント向け/規程・規則/"

# RP契約書_cocomate御中（フォルダごと）
mv "/Volumes/G-TECH/02_クライアント情報/_共通資料/RP契約書_cocomate御中" \
   "/Volumes/G-TECH/02_クライアント情報/BIZ_業種別クライアント/Web・IT/cocomate/ROBOT PAYMENT決済サービス導入/01_OUTPUT/クライアント向け/"

# チア2号店改修工事（フォルダごと）
mv "/Volumes/G-TECH/02_クライアント情報/_共通資料/チア2号店改修工事" \
   "/Volumes/G-TECH/02_クライアント情報/BIZ_業種別クライアント/店舗・飲食/チア/チア2号店改修工事/00_INPUT/工程表/"
```

---

## Step 5: 仕分け待ちフォルダへの移動

```bash
# 20241210現調（クライアント名不明）
mv "/Volumes/G-TECH/02_クライアント情報/_共通資料/20241210現調" \
   "/Volumes/G-TECH/02_クライアント情報/_共通資料/_ARCHIVE/20251108_仕分け待ち/"
```

---

## Step 6: 検証

### 6-1. ビジネス書類フォルダの確認

```bash
# 見積書フォルダが空になっているか確認（法的資料以外）
ls -la "/Volumes/G-TECH/02_クライアント情報/_共通資料/ビジネス書類/見積書/"
# 期待: 空

# 請求書フォルダが空になっているか確認
ls -la "/Volumes/G-TECH/02_クライアント情報/_共通資料/ビジネス書類/請求書/"
# 期待: 空

# 契約書フォルダに法的参考資料のみが残っているか確認
ls -la "/Volumes/G-TECH/02_クライアント情報/_共通資料/ビジネス書類/契約書/"
# 期待: 3つの法的ガイドPDFのみ
```

### 6-2. 新規プロジェクトフォルダの確認

```bash
# 各プロジェクトにPROJECT.mdが存在するか確認
find "/Volumes/G-TECH/02_クライアント情報/BIZ_業種別クライアント" -name "PROJECT.md" -type f | wc -l
# 期待: 新規作成したプロジェクト数と一致

# 各プロジェクトに00_INPUT, 01_OUTPUT, 02_ARCHIVEが存在するか確認
find "/Volumes/G-TECH/02_クライアント情報/BIZ_業種別クライアント" -type d -name "00_INPUT" | wc -l
# 期待: 新規作成したプロジェクト数と一致
```

### 6-3. 移動ファイル数の確認

```bash
# AOMI100クリニック/サイン・床・壁張り替え工事/01_OUTPUT/クライアント向け/見積書/ にファイルがあるか
ls "/Volumes/G-TECH/02_クライアント情報/BIZ_業種別クライアント/店舗・飲食/AOMI100クリニック/サイン・床・壁張り替え工事/01_OUTPUT/クライアント向け/見積書/"
# 期待: サンフィールド医院御中_見積書_251007-1.pdf が存在

# 個人データの移動確認
ls "/Volumes/G-TECH/02_クライアント情報/_ARCHIVE/個人データ/末武修平/税務関連/2022年度/"
# 期待: 複数のPDFファイルが存在
```

---

## ✅ 完了チェックリスト

### Step 1
- [ ] 新規クライアントフォルダ作成（13社・個人）
- [ ] 新規プロジェクトフォルダ作成（約25件）
- [ ] 各プロジェクトにPROJECT.md配置
- [ ] 各プロジェクトに00_INPUT/01_OUTPUT/02_ARCHIVE作成

### Step 2
- [ ] 見積書15件の移動（重複2件削除、不明1件仕分け待ち）
- [ ] 請求書7件の移動（不明4件仕分け待ち、個人2件_ARCHIVEへ）
- [ ] 契約書8件の処理（移動1件、参考資料3件保持、不明4件仕分け待ち）

### Step 3
- [ ] 個人データ（末武修平 税務関連）移動
- [ ] 学童資料移動
- [ ] LINEトーク履歴移動

### Step 4
- [ ] cocomateロゴフォルダ移動
- [ ] アストライズフォルダ移動
- [ ] AGO就業規則フォルダ移動
- [ ] RP契約書フォルダ移動
- [ ] チア2号店フォルダ移動

### Step 5
- [ ] 20241210現調フォルダ移動（仕分け待ちへ）

### Step 6
- [ ] ビジネス書類フォルダの確認
- [ ] 新規プロジェクトフォルダの確認
- [ ] 移動ファイル数の確認

---

## ⚠️ エラーハンドリング

### エラー1: ファイルが見つからない

```
mv: cannot stat '/path/to/file': No such file or directory
```

**対処法:**
1. ファイル名のスペースや特殊文字を確認
2. パスを引用符で囲む
3. `ls "/path/to/directory/"` で実際のファイル名を確認

### エラー2: 移動先フォルダが存在しない

```
mv: cannot move to '/path/to/destination/': No such file or directory
```

**対処法:**
1. 移動先フォルダが作成されているか確認
2. Step 1のフォルダ作成コマンドを再実行

### エラー3: ファイルが既に存在

```
mv: overwrite '/path/to/file'?
```

**対処法:**
1. 既存ファイルを確認
2. 古いバージョンなら`02_ARCHIVE/`へ移動
3. 新しいバージョンを保持

---

## 📝 実行後の確認事項

### 1. git status確認

```bash
cd "/Volumes/G-TECH/02_クライアント情報"
git status
```

### 2. 移動ファイル数の確認

```bash
# _共通資料に残ったファイル数
find "/Volumes/G-TECH/02_クライアント情報/_共通資料" -type f | wc -l
# 期待: 大幅に減少（法的参考資料、営業資料、テンプレートのみ）

# 新規作成したプロジェクトのファイル数
find "/Volumes/G-TECH/02_クライアント情報/BIZ_業種別クライアント" -type f -name "*.pdf" | wc -l
# 期待: 移動したPDFファイル数と一致
```

### 3. git commit

```bash
cd "/Volumes/G-TECH/02_クライアント情報"
git add .
git commit -m "フェーズ1完了: _共通資料の仕分け

- ビジネス書類（見積書・請求書・契約書）を各プロジェクトへ移動
- 新規クライアント13社・個人、新規プロジェクト約25件作成
- 個人データを_ARCHIVEへ移動
- 特定クライアント名フォルダを各クライアントへ移動
- クライアント名不明ファイルを仕分け待ちへ移動

詳細: フェーズ1_詳細実行ガイド_Composer用.md 参照"
```

---

## 次のステップ

フェーズ1完了後：
1. `リポジトリ再構築計画.md` のフェーズ2へ進む
2. CORE/BIZ/PERSONALのフラット化を実行
