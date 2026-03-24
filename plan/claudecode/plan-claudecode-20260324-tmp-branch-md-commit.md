# Plan: exampleDocs/markdown の md ファイルを f/tmp ブランチにコミット・PUSH し、ブランチ削除する

- **作成日**: 2026-03-24
- **担当エージェント**: claudecode
- **ブランチ**: f/tmp（ユーザー指定）
- **ステータス**: 完了

## 背景・目的

exampleDocs/markdown に md ファイルが存在する場合、f/tmp ブランチを作成してコミット・PUSH し、
ユーザー承認後にローカル・リモート両方のブランチを削除する。

## 確認事項

- 対象ファイル: `exampleDocs/markdown/test.md`（untracked）
- 現在のブランチ: `main`
- `f/tmp` ブランチ: 未存在（新規作成）

## タスクブレークダウン

- [x] exampleDocs/markdown に md ファイルが存在するか確認
- [x] plan ファイルを作成
- [x] f/tmp ブランチを作成してチェックアウト
- [x] test.md をステージング・コミット
- [x] リモートに PUSH
- [x] ユーザーにブランチ削除の承認を求める
- [x] 承認後: ローカルおよびリモートの f/tmp ブランチを削除

### 追加タスク（2026-03-24）

- [x] 上記ワークフローを Skill 化（`.claude/commands/branch-commit-push-cleanup.md`）
- [x] Skill の使い方を knowledge に作成（`prompt/claudecode/knowledge/`）

## 注意事項

- 今回は CLAUDE.md のブランチ命名規則（ai-claudecode/xxx）ではなく、ユーザー指定の `f/tmp` を使用
- 削除は破壊的操作のため、必ずユーザー承認を得てから実施する
