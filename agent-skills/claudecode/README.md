# agent-skills / claudecode

Claude Code 向けのスキル適用ガイド。

## スキルの登録方法

`agent-skills/common/` のテンプレートを Claude Code スラッシュコマンドとして使う場合は
`.claude/commands/{command-name}.md` にコピー・カスタマイズする。

## 固有の仕組み

| 機能 | 場所 | 説明 |
|---|---|---|
| スラッシュコマンド | `.claude/commands/` | `/コマンド名` で呼び出せる定型プロンプト |
| MCP サーバー | `.claude/settings.json` | 外部サービス連携（GitHub, DB, Web 等） |
| ローカル設定 | `.claude/settings.local.json` | 個人・環境固有設定（git 管理外） |

## ブランチ作業フロー

1. `/new-branch` でブランチ `ai-claudecode/{name}` を作成
2. Plan モードで計画 → ユーザー承認
3. 実装・コミット（`/commit` 活用）
4. `/review-pr` でセルフレビュー
5. PR 作成 → ユーザーに承認依頼
