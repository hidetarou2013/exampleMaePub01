Plan モードで実装計画を立て、承認後に実装し、PR を作成します。

以下の手順で進めてください:

1. **ブランチ確認**: 現在 `ai-claudecode/` ブランチにいるか確認する。いない場合は `/new-branch` を先に実行するよう案内する。

2. **Plan モード移行**: `EnterPlanMode` を使って計画フェーズに入る。
   - コードベース・要件を調査する
   - 実装方針を設計する
   - `agent-skills/common/plan-template.md` を参考に計画書を作成し `plan/claudecode/plan-claudecode-{YYYYMMDD}-{name}.md` に保存する
   - ユーザーに計画を提示して承認を求める（`ExitPlanMode`）

3. **実装**: 承認された計画に従って実装する。
   - `TodoWrite` でタスクを管理する
   - `agent-skills/common/commit-template.md` に従ってコミットする

4. **セルフレビュー**: `agent-skills/common/review-checklist.md` のチェックリストを確認する。

5. **PR 作成**:
   ```
   gh pr create --title "{変更内容}" --body "..."
   ```
   - PR 本文には: 変更概要・実装方針・確認ポイント・テスト方法を記載する
   - ユーザーに PR URL を報告して承認を依頼する
