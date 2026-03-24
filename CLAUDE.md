# CLAUDE.md

このファイルは Claude Code がこのリポジトリで作業する際のガイドラインです。

---

## プロジェクト概要

各種ドキュメント形式のサンプルファイルを管理するリポジトリ。

---

## 対象 AI エージェント

| エージェント ID | サービス |
|---|---|
| `claudecode` | Claude Code (Anthropic) |
| `codex` | Codex (OpenAI) |
| `copilot` | GitHub Copilot |
| `kiro` | AWS Kiro |

---

## ディレクトリ構成

```
.
├── .claude/                    # Claude Code 設定・カスタム命令
├── .codex/                     # Codex 設定・カスタム命令
├── plan/                       # 実装計画・設計ドキュメント
│   ├── claudecode/             # Claude Code 用プラン
│   ├── codex/                  # Codex 用プラン
│   ├── copilot/                # GitHub Copilot 用プラン
│   └── kiro/                   # AWS Kiro 用プラン
├── prompt/                     # プロンプトテンプレート集
│   ├── claudecode/
│   │   ├── knowledge/          # ドメイン知識・前提情報
│   │   ├── howto/              # 手順・操作ガイド
│   │   ├── input/              # 入力プロンプトテンプレート
│   │   ├── output/             # 出力フォーマット定義
│   │   ├── working/            # 作業中・一時プロンプト
│   │   └── review/             # レビュー・検証プロンプト
│   ├── codex/                  # (同上、Codex 用)
│   ├── copilot/                # (同上、GitHub Copilot 用)
│   └── kiro/                   # (同上、AWS Kiro 用)
├── exampleDocs/                # サンプルドキュメント
│   ├── excel/
│   ├── html/
│   ├── markdown/
│   ├── mermaid/
│   ├── pdf/
│   ├── ppt/
│   └── word/
└── .tmp/                       # 一時作業ディレクトリ（git 管理外）
```

---

## ファイル命名規則

### plan/

```
plan/{agent}/plan-{agent}-{YYYYMMDD}-{name}.md
```

| 要素 | 説明 |
|---|---|
| `{agent}` | エージェント ID（`claudecode` / `codex` / `copilot` / `kiro`） |
| `{YYYYMMDD}` | 作成日（例: `20260324`） |
| `{name}` | 内容を表す短い名前（英数字・ハイフン、例: `auth-refactor`） |

**例:**
```
plan/claudecode/plan-claudecode-20260324-auth-refactor.md
plan/kiro/plan-kiro-20260324-api-design.md
```

### prompt/

```
prompt/{agent}/{category}/prompt-{agent}-{YYYYMMDD}-{name}.md
```

| 要素 | 説明 |
|---|---|
| `{agent}` | エージェント ID |
| `{category}` | `knowledge` / `howto` / `input` / `output` / `working` / `review` |
| `{YYYYMMDD}` | 作成日 |
| `{name}` | 内容を表す短い名前 |

**例:**
```
prompt/claudecode/input/prompt-claudecode-20260324-generate-er-diagram.md
prompt/copilot/review/prompt-copilot-20260324-code-review-checklist.md
```

---

## 作業ルール

### 1. Plan モードの使用（必須）

- **非自明な実装タスクは必ず Plan モードを使うこと**
- Plan モード（`EnterPlanMode`）でアーキテクチャ・実装方針を設計し、ユーザー承認を得てから実装に入る
- 計画ドキュメントは `plan/claudecode/` に命名規則に従って保存する
- Plan の内容は実装前に明確にし、曖昧なまま進めない

### 2. Agent Teams（専門職エージェント）の活用

- 専門的な作業は専門エージェントに委任する（Claude Code の `Agent` ツール使用）
- 推奨エージェント割り当て:
  - `Explore` エージェント: コードベース調査・ファイル探索
  - `Plan` エージェント: 設計・アーキテクチャ検討
  - `general-purpose` エージェント: 複数ステップの調査・実装タスク
- 独立した並行タスクは複数エージェントを同時起動して効率化する

### 3. タスク進捗管理

- 3 ステップ以上の作業は必ず `TodoWrite` ツールでタスクリストを作成する
- タスク完了直後に `completed` に更新する（まとめて更新しない）
- 同時に `in_progress` にできるタスクは 1 つのみ
- タスクが不要になったらリストから削除する

### 4. その他

- サンプルファイルを追加する際は対応するフォーマットのディレクトリ（`exampleDocs/` 配下）に配置する
- `.tmp/` はコミットしない
- `prompt/*/working/` の一時プロンプトは完成後に適切なカテゴリへ移動する
