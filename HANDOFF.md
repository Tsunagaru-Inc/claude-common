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

## ファイル構成と現状

### `README.md` — 更新済み ✅
- リポジトリ概要と初回セットアップ手順
- スラッシュコマンド（`/pptx` 等）の参照を削除
-「Claude Cowork」表記に統一
- 一行プロンプトによるオンボーディング起動フローを維持

### `CLAUDE.md` — 変更なし（問題なし） ✅
- Claude への共通指示（トーン・判断基準・プッシュバックルールなど）
- Cowork はデスクトップアプリだが内部で Claude Code エンジンを使っているため、
  プロジェクトフォルダに置いた `CLAUDE.md` は自動読み込みされる
- 「プロジェクトのカスタム指示」に貼り付けても機能する
- ファイル名は `CLAUDE.md` のままで問題ない（リネーム不要と判断）

### `context/tsunagaru-company.md` — 変更なし（問題なし） ✅
- セットアップ時に Claude が URL から取得して読み込む
- オンボーディングフロー（ステップ 3）に組み込み済み

### `setup/first-time-setup.md` — 全面書き直し済み ✅
主な変更点：
- 冒頭の「Claude Code のチャット画面に」→「Claude Cowork のチャット欄に」
- `find-skills` スキルを使ったスキルインストール手順を完全削除
- `pptx`, `copywriting`, `social-content`, `cold-email`, `gws-*` など CLI 前提のスキル一覧を削除
- スキルの説明を「自動選択される機能」として正確に説明
- 外部ツール連携は「別途設定が必要」として正確に案内
- 完了メッセージからスラッシュコマンドを削除
- FAQ への案内を追加（ステップ 7）

### `setup/faq.md` — 新規作成 ✅
社員向け Q&A。以下をカバー：
- Claude Cowork とは何か（Claude Code との違いを明示）
- できること・できないこと
- 機密情報の扱い方
- スキル・プロジェクトの説明
- 外部ツール連携の案内
- トラブル時の対応

### `.claude/settings.local.json` — 拡張済み ✅
変更前：`support.claude.com` のみ許可
変更後：以下を追加
- `raw.githubusercontent.com`（オンボーディング中に会社情報ファイルを取得するため）
- `docs.claude.com`（Claude の使い方調査のため）

### `skills/brand-guideline-ppt.skill/` — 変更なし
- ブランドガイドライン準拠スライド作成スキル
- Cowork のカスタムスキルとして機能する形式（`.skill` フォルダ）で格納済み
- ユーザーがこのリポジトリフォルダをワークスペースとして開くと利用可能

---

## 解決済みの課題

| 課題 | 解決策 |
|------|--------|
| `first-time-setup.md` が Claude Code CLI 前提で書かれていた | Cowork 専用に全面書き直し |
| `find-skills` など存在しないスキルのインストール手順が含まれていた | 削除。スキルは自動選択されることを説明 |
| スラッシュコマンドがエンドユーザー向けに案内されていた | 削除。自然言語での指示に変更 |
| README にスラッシュコマンドへの言及があった | 削除済み |
| `CLAUDE.md` のリネームを検討していた | 不要と判断（Cowork でも自動読み込みされる） |
| `settings.local.json` が `support.claude.com` のみ許可 | GitHub raw 等を追加 |
| 社員が疑問を持ったときの受け皿がなかった | `setup/faq.md` を新規作成 |

---

## 残課題・次のステップ

### 要確認事項

1. **GitHub リポジトリの公開設定** — ✅ 確認済み（Public）
   `https://raw.githubusercontent.com/Tsunagaru-Inc/claude-common/main/...` の URL は
   アクセストークン不要で利用可能。

2. **Slack `#ai-tools` チャンネルの整備**
   FAQ・オンボーディングで `#ai-tools` チャンネルを参照しているが、
   チャンネルが存在するか、誰が担当するかを確認・整備する。

3. **外部ツール連携手順の追加**
   Gmail・Slack・Google カレンダー・Notion などの連携設定手順が未作成。
   `setup/integrations.md` として別途作成することを推奨。

4. **`context/tsunagaru-company.md` の定期更新**
   会社情報・用語集はプロジェクトが変わるたびに陳腐化する。
   四半期ごとに担当者がレビューする運用を設計すること。

5. **ブランドスキルのテスト**
   `skills/brand-guideline-ppt.skill/` が実際の Cowork セッションで正しく動作するか、
   動作確認が必要。

---

## 参考：ツナガルについて

詳細は `context/tsunagaru-company.md` を参照。一言でいうと：
「日本の地域資源・文化・人の魅力を編集し、観光・体験・越境販売・共創事業として世界につなぐことで、地域に持続可能な収益を生み出すプロデュース会社」

メンバーの主な業務：提案書作成、SNS 運用、メール営業、行政向け報告書、インバウンド施策の企画など。
Claude に期待する用途：文章作成、スライド作成、SNS 投稿企画、メール下書き、情報整理。
