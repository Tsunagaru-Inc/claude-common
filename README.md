# ツナガル × Claude 共通設定リポジトリ

このリポジトリは、ツナガル株式会社のメンバー全員が Claude をより効果的に使えるよう、
共通の設定・スキル・コンテキストを管理するためのものです。

---

## このリポジトリに含まれるもの

| パス | 内容 |
|------|------|
| `CLAUDE.md` | Claude への共通指示（トーン・判断基準・ガードレール） |
| `context/tsunagaru-company.md` | 会社情報・用語集・事業理解のコンテキスト |
| `skills/brand-guideline-ppt/` | ブランドガイドライン準拠のスライド作成スキル |
| `setup/first-time-setup.md` | Claude に貼り付けるだけの対話型セットアップガイド |

---

## はじめてのセットアップ

### ステップ 1 — Claude Code をインストール・起動

まだの場合は [claude.ai/code](https://claude.ai/code) からインストールしてください。

### ステップ 2 — 以下の一行を Claude に貼り付けて送信する

```
このURLのファイルを取得して、その中の指示に従ってください：https://raw.githubusercontent.com/Tsunagaru-Inc/claude-common/main/setup/first-time-setup.md
```

Claude が日本語でステップごとに案内します。スキルのインストールから設定完了まで約 3〜5 分です。

---

## 使い方のヒント

- **`/` を入力するとスキル一覧が表示されます。** 例：`/pptx`、`/copywriting`
- **`/find-skills`** で追加スキルを検索・インストールできます
- わからないことは Claude に日本語で聞いてください。このリポジトリの設定により、ツナガルの文脈を理解した上で回答します

---

## メンテナンス

- スキルや設定の追加・変更は PR を通じて行ってください
- 会社情報の更新は `context/tsunagaru-company.md` を編集してください
- 質問・提案は Slack の `#ai-tools` チャンネルへ
