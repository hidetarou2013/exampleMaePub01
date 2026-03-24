作業ブランチを作成します。

以下の手順で進めてください:

1. 今回の作業内容を一言で表す英単語・句をユーザーに確認する（例: `add-mcp-config`, `fix-readme`, `refactor-prompt-structure`）
2. 現在のブランチとリモートの状態を確認する（`git status`, `git branch -a`）
3. `main` ブランチが最新か確認し、必要であれば `git pull origin main` を実行する
4. ブランチを作成して切り替える:
   ```
   git checkout -b ai-claudecode/{入力された名前}
   ```
5. 作成されたブランチを確認して報告する

**注意**: ブランチ名は `ai-claudecode/` プレフィックスで始めること。作業完了後は必ず PR を作成してユーザーの承認を求めること。
