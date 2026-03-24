現在の変更をコミットします。

以下の手順で進めてください:

1. `git status` と `git diff --staged` で変更内容を確認する
2. ステージングされていないファイルがあれば、コミット対象かユーザーに確認する
3. `agent-skills/common/commit-template.md` のルールに従ってコミットメッセージを作成する:
   - type: feat / fix / docs / style / refactor / test / chore / ci
   - summary: 72 文字以内、命令形・現在形
   - body: なぜその変更をしたか（任意）
4. コミットを実行する:
   ```
   git commit -m "$(cat <<'EOF'
   {type}: {summary}

   {body（必要な場合）}

   Co-Authored-By: Claude Sonnet 4.6 <noreply@anthropic.com>
   EOF
   )"
   ```
5. コミット結果を報告する

**注意**: `.env` や `settings.local.json` 等のシークレットを含むファイルはコミットしないこと。
