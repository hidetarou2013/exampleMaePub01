# コミットメッセージルール

> 全エージェント共通のコミットメッセージ規約。

---

## フォーマット

```
{type}: {summary}

{body（任意）}

Co-Authored-By: {Agent} <noreply@example.com>
```

## type 一覧

| type | 用途 |
|---|---|
| `feat` | 新機能の追加 |
| `fix` | バグ修正 |
| `docs` | ドキュメントのみの変更 |
| `style` | コードの意味に影響しない変更（フォーマット等） |
| `refactor` | バグ修正・機能追加を伴わないリファクタリング |
| `test` | テストの追加・修正 |
| `chore` | ビルドプロセス・補助ツール・設定の変更 |
| `ci` | CI 設定の変更 |

## ルール

- summary は命令形・現在形で書く（英語推奨）
- summary は 72 文字以内
- なぜその変更をしたかを body に書く（何を変えたかではなく）
- 破壊的変更がある場合は `BREAKING CHANGE:` を body に含める

## 例

```
feat: add agent-specific subfolder structure under plan/ and prompt/

Reorganize directories so each AI agent has its own namespace.
This makes it easier to identify which agent created which artifact
and avoids naming collisions between agents.

Co-Authored-By: Claude Sonnet 4.6 <noreply@anthropic.com>
```
