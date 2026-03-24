# branch-commit-push-cleanup

指定ディレクトリの未追跡ファイルをブランチにコミット・PUSH し、ユーザー承認後にブランチを削除します。

## 使い方

```
/branch-commit-push-cleanup
```

## 手順

### 1. 対象ファイルの確認

対象ディレクトリ（デフォルト: `exampleDocs/markdown`）に md ファイルが存在するか確認する:

```bash
ls exampleDocs/markdown/*.md 2>/dev/null || echo "md ファイルが存在しません"
```

md ファイルが存在しない場合はここで終了し、その旨をユーザーに報告する。

### 2. ブランチ名の決定

- CLAUDE.md のルールに従う場合: `ai-claudecode/{作業内容}` を使う
- ユーザーが明示的に指定した場合: 指定されたブランチ名を使う

### 3. ブランチ作成・チェックアウト

```bash
git checkout -b {ブランチ名}
```

### 4. ファイルのステージング・コミット

```bash
git add {対象ファイルのパス}
git commit -m "docs: add md files to exampleDocs/markdown

Co-Authored-By: Claude Sonnet 4.6 <noreply@anthropic.com>"
```

### 5. リモートへ PUSH

```bash
git push --set-upstream origin {ブランチ名}
```

### 6. ユーザーへの承認依頼（必須）

以下のメッセージを出力してユーザーの応答を待つ:

```
ローカル及びremoteの{ブランチ名}ブランチを削除しますがいいですか？
```

### 7. 承認後: ブランチ削除

ユーザーが承認した場合のみ実行する:

```bash
# main ブランチに戻る
git checkout main

# ローカルブランチを削除
git branch -d {ブランチ名}

# リモートブランチを削除
git push origin --delete {ブランチ名}
```

## 注意事項

- ブランチ削除は破壊的操作のため、**必ずユーザーの承認を得てから実施**すること
- 承認が得られない場合はブランチを削除せず、そのままにする
- コミット対象は `exampleDocs/markdown/` 配下の `.md` ファイルのみ（`.gitkeep` 等は含まない）
