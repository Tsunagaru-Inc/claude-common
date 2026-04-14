# Project Handoff — ツナガル Claude Cowork オンボーディング

> このドキュメントは、別のエージェントがこのプロジェクトの作業を引き継げるよう、
> 現状・目標・未解決事項を整理したものです。

---

## プロジェクトの目標

ツナガル株式会社（観光・インバウンドマーケティングのプロデュース会社）の
**非技術系メンバー**が **Claude Cowork** を業務で使い始めるための、
共通設定リポジトリとオンボーディングガイドを整備すること。

ターゲットユーザー：IT リテラシーが高くないビジネス職のメンバー（企画・営業・制作など）

使用プラットフォーム：**Claude Cowork**（claude.com/download からインストールするデスクトップアプリ）
※ Claude Code（CLI）は対象外。

---

## リポジトリの場所

**GitHub（Public）:** `https://github.com/Tsunagaru-Inc/claude-common`

---

## 現時点で作成済みのファイル

### `README.md`
- リポジトリの概要と初回セットアップ手順
- ステップ 1: Claude Cowork をインストール
- ステップ 2: 以下の一行を Claude に貼り付けて送信（オンボーディングプロンプトを URL から取得させる）

```
このURLのファイルを取得して、その中の指示に従ってください：https://raw.githubusercontent.com/Tsunagaru-Inc/claude-common/main/setup/first-time-setup.md
```

- **現状の問題点:** `/pptx` や `/find-skills` などのスラッシュコマンドに言及している箇所が残っており、これらが Cowork で有効かどうか未確認。

---

### `CLAUDE.md`
- Claude への共通指示（トーン・判断基準・計画確認・プッシュバックのルールなど）
- **現状の問題点:** ファイル名が `CLAUDE.md` になっているが、これは Claude Code が自動読み込みする名前。Cowork では自動読み込みされない可能性が高い。
  - → 実際の使われ方は「プロジェクトのカスタム指示」に貼り付けるテキスト
  - → `custom-instructions.md` へのリネームを検討中（未実施）

---

### `context/tsunagaru-company.md`
- ツナガル株式会社の事業・用語・拠点・ミッションなどのコンテキストファイル
- セットアップ時に Claude が URL から取得して読み込む想定
- **現状：問題なし**

---

### `setup/first-time-setup.md`
- ユーザーが Claude に貼り付けることで、Claude 自身がオンボーディングをガイドするプロンプト
- **現状の問題点（要修正）:**
  1. `find-skills` スキルを使ったスキルインストール手順が含まれているが、これは Claude Code の機能であり Cowork で動作するか不明
  2. スキル一覧（pptx, copywriting, social-content 等）のインストール手順が Claude Code 前提で書かれている
  3. 「許可確認が出たときの案内」セクションが Claude Code のツール許可モデルを前提にしている

---

### `skills/brand-guideline-ppt/SKILL.md`
- ツナガルのブランドガイドライン準拠スライド作成スキル
- **現状の問題点:** Claude Code 形式（YAML frontmatter 付き Markdown）で書かれている。
  Claude Cowork のスキルは ZIP パッケージ形式が必要な可能性がある（要確認）。

---

## 未解決の重要な質問

以下の点が未確認のため、`setup/first-time-setup.md` と `README.md` を正確に完成させられていない。

### Q1. Cowork のスキルマーケットプレイスについて
Claude Cowork では **Customize → Skills** からスキルを追加できることは確認済み。
しかし以下が不明：

- Anthropic が提供する公式スキル（`pptx`, `copywriting`, `social-content`, `cold-email` など）は
  Cowork のスキルマーケットプレイスから直接インストールできるか？
- それともユーザーが ZIP ファイルを自分でアップロードする必要があるか？
- スキルの呼び出しはスラッシュコマンドか、それとも自動判定のみか？

**参照すべきドキュメント:**
- `https://support.claude.com/en/articles/12512198-how-to-create-custom-skills`
- Cowork のスキルマーケットプレイスの URL（未特定）

---

### Q2. コード実行の有効化
公式ドキュメントによると、スキルの使用には **コード実行が有効** である必要がある。

- ツナガルのプランでコード実行はデフォルトで ON か、それともユーザーが手動で有効にする必要があるか？
- Cowork ではコード実行の設定はどこにあるか？

---

### Q3. `CLAUDE.md` のリネームと配置
- Cowork のカスタム指示は「プロジェクトのカスタム指示」欄に貼り付ける運用になる想定
- `CLAUDE.md` を `custom-instructions.md` にリネームするか検討中
- 現在 `first-time-setup.md` 内のステップ 4 では、ユーザーに URL を開いてコピペするよう案内しているが、この URL が `CLAUDE.md` のままになっている

---

### Q4. ブランドスキルの Cowork 対応
`skills/brand-guideline-ppt/SKILL.md` を Cowork で使えるようにするには：
- ZIP パッケージへの変換が必要か？
- Cowork でのスキルフォーマット要件（`Skill.md` vs `SKILL.md`、フォルダ構成など）の確認が必要

---

## 次のエージェントへの作業依頼

以下の順番で作業を進めてください：

1. **Q1〜Q4 の調査**
   - `https://support.claude.com/en/articles/12512198-how-to-create-custom-skills` を読む
   - Cowork のスキルマーケットプレイスのドキュメントを探す
   - コード実行の設定方法を確認する

2. **`setup/first-time-setup.md` の修正**
   - 調査結果に基づいて、スキルインストール手順を Cowork の実際の操作に合わせて書き直す
   - スキルがマーケットプレイスから入れられるなら、その手順を記載する
   - スキルが ZIP アップロードのみなら、ブランドスキルの ZIP 作成も含めた手順にする

3. **`CLAUDE.md` のリネーム判断と `README.md` の整合**
   - Cowork でカスタム指示がどう設定されるかを確認した上でリネームを判断する
   - README のスラッシュコマンド言及を削除または修正する

4. **`skills/brand-guideline-ppt/` の Cowork 対応**
   - 必要であれば ZIP パッケージとして再構成する

---

## 参考：ツナガルについて

詳細は `context/tsunagaru-company.md` を参照。一言でいうと：
「日本の地域資源・文化・人の魅力を編集し、観光・体験・越境販売・共創事業として世界につなぐことで、地域に持続可能な収益を生み出すプロデュース会社」

メンバーの主な業務：提案書作成、SNS 運用、メール営業、行政向け報告書、インバウンド施策の企画など。
Claude に期待する用途：文章作成、スライド作成、SNS 投稿企画、メール下書き、情報整理。
