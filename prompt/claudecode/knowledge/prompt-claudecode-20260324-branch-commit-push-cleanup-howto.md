# Knowledge: branch-commit-push-cleanup スキルの使い方

- **作成日**: 2026-03-24
- **対象スキル**: `/branch-commit-push-cleanup`（`.claude/commands/branch-commit-push-cleanup.md`）
- **カテゴリ**: ブランチ管理 / ファイルコミット

---

## 概要

`exampleDocs/markdown/` 配下の未追跡 `.md` ファイルを専用ブランチにコミット・PUSH し、
ユーザーの承認を得てからブランチを削除する一連の作業を自動化するスキル。

---

## 典型的なユースケース

- 新しい Markdown ファイルを一時ブランチで共有したい
- 試作ドキュメントをリモートに上げてレビューしてもらいたい
- 確認後にブランチをきれいに片付けたい

---

## 呼び出し方

Claude Code のチャット上で以下を入力:

```
/branch-commit-push-cleanup
```

または、ブランチ名を明示する場合はチャットで指示を添える:

```
/branch-commit-push-cleanup を使って、f/tmp ブランチで実施してください
```

---

## 実行フロー

```
1. 対象ファイルの確認
   └─ exampleDocs/markdown/*.md が存在しなければ終了

2. ブランチ作成
   └─ ai-claudecode/{name}（または指定ブランチ名）

3. git add → git commit

4. git push --set-upstream origin {branch}

5. ユーザーへ確認メッセージ出力
   「ローカル及びremoteの{branch}ブランチを削除しますがいいですか？」

6. 承認 → git checkout main
         → git branch -d {branch}
         → git push origin --delete {branch}

   非承認 → ブランチはそのまま保持
```

---

## ブランチ命名ルール

| ケース | ブランチ名 |
|---|---|
| 通常（CLAUDE.md 準拠） | `ai-claudecode/{作業内容}` |
| ユーザー指定 | 指定された名前をそのまま使用 |

---

## 注意事項

- **ブランチ削除はユーザー承認が必須**。承認なしには実行しない。
- コミット対象は `.md` ファイルのみ（`.gitkeep` 等の管理ファイルは除外）。
- 削除前に必ず `main` ブランチへ戻ること（削除対象ブランチ上では `branch -d` が実行できないため）。

---

## 関連ファイル

| ファイル | 役割 |
|---|---|
| [.claude/commands/branch-commit-push-cleanup.md](../../../../.claude/commands/branch-commit-push-cleanup.md) | スキル定義（スラッシュコマンド本体） |
| [agent-skills/common/commit-template.md](../../../../agent-skills/common/commit-template.md) | コミットメッセージ規約 |
| [agent-skills/common/plan-template.md](../../../../agent-skills/common/plan-template.md) | 計画書テンプレート |
| [plan/claudecode/plan-claudecode-20260324-tmp-branch-md-commit.md](../../../../plan/claudecode/plan-claudecode-20260324-tmp-branch-md-commit.md) | このスキルが生まれた元の作業計画 |
