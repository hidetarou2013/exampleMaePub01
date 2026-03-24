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
├── .claude/                    # Claude Code 設定・スキル・MCP 設定
│   ├── commands/               # Claude Code スラッシュコマンド（実行可能スキル）
│   ├── settings.json           # MCP サーバー設定（プロジェクトレベル）
│   └── settings.local.json     # ローカル固有設定（git 管理外）
├── .codex/                     # Codex 設定・カスタム命令
├── agent-skills/               # 全エージェント共通スキルライブラリ
│   ├── common/                 # 共通テンプレート（プラン・レビュー・コミット等）
│   ├── claudecode/             # Claude Code 向け適用ガイド
│   ├── codex/                  # Codex 向け適用ガイド
│   ├── copilot/                # GitHub Copilot 向け適用ガイド
│   └── kiro/                   # AWS Kiro 向け適用ガイド
├── plan/                       # 実装計画・設計ドキュメント
│   ├── claudecode/
│   ├── codex/
│   ├── copilot/
│   └── kiro/
├── prompt/                     # プロンプトテンプレート集
│   ├── claudecode/
│   │   ├── knowledge/
│   │   ├── howto/
│   │   ├── input/
│   │   ├── output/
│   │   ├── working/
│   │   └── review/
│   ├── codex/                  # (同上)
│   ├── copilot/                # (同上)
│   └── kiro/                   # (同上)
├── exampleDocs/                # サンプルドキュメント
│   ├── excel/ / html/ / markdown/ / mermaid/ / pdf/ / ppt/ / word/
└── .tmp/                       # 一時作業ディレクトリ（git 管理外）
```

---

## ファイル命名規則

### plan/
```
plan/{agent}/plan-{agent}-{YYYYMMDD}-{name}.md
```
例: `plan/claudecode/plan-claudecode-20260324-auth-refactor.md`

### prompt/
```
prompt/{agent}/{category}/prompt-{agent}-{YYYYMMDD}-{name}.md
```
例: `prompt/claudecode/input/prompt-claudecode-20260324-generate-er-diagram.md`

---

## 作業ルール

### 1. Plan モードの使用（必須）

- **非自明な実装タスクは必ず Plan モードを使うこと**
- Plan モード（`EnterPlanMode`）でアーキテクチャ・実装方針を設計し、ユーザー承認を得てから実装に入る
- 計画ドキュメントは `plan/claudecode/` に命名規則に従って保存する
- Plan の内容は実装前に明確にし、曖昧なまま進めない

### 2. ブランチ戦略（Claude Code 作業時必須）

- **Claude Code で作業を行う際は、必ず専用ブランチを作成してから開始すること**
- ブランチ命名規則:
  ```
  ai-claudecode/{作業内容を表す英単語}
  ```
  例: `ai-claudecode/add-mcp-config` / `ai-claudecode/refactor-auth` / `ai-claudecode/fix-typo`
- `{作業内容}` は内容が一目でわかる英単語・句を選ぶ（ハイフン区切り、小文字）
- 作業完了後は **Pull Request を作成してユーザーに承認を求める**（直接 main にマージしない）
- PR には変更内容・理由・確認ポイントを明記する

> **スラッシュコマンド**: `/new-branch` で対話的にブランチを作成できる（`.claude/commands/new-branch.md` 参照）

### 3. Agent Teams（専門職エージェント）の活用

- 専門的な作業は専門エージェントに委任する（Claude Code の `Agent` ツール使用）
- 推奨エージェント割り当て:
  - `Explore` エージェント: コードベース調査・ファイル探索
  - `Plan` エージェント: 設計・アーキテクチャ検討
  - `general-purpose` エージェント: 複数ステップの調査・実装タスク
- 独立した並行タスクは複数エージェントを同時起動して効率化する

### 4. タスク進捗管理

- 3 ステップ以上の作業は必ず `TodoWrite` ツールでタスクリストを作成する
- タスク完了直後に `completed` に更新する（まとめて更新しない）
- 同時に `in_progress` にできるタスクは 1 つのみ
- タスクが不要になったらリストから削除する

### 5. スキル・MCP の活用方針

- **作業前に利用可能なスキル（`.claude/commands/`）と MCP サービスを確認する**
- 定型作業はスキルを呼び出して実施する（例: `/new-branch`, `/plan-pr`, `/commit`）
- MCP サービスは `.claude/settings.json` で管理。使うたびに追加・充実させていく
- 新しいスキルのテンプレートは `agent-skills/common/` に追加し、各エージェント向け実装は `agent-skills/{agent}/` に配置する
- Claude Code 固有のスラッシュコマンドは `.claude/commands/` に追加する

### 6. その他

- サンプルファイルを追加する際は対応するフォーマットのディレクトリ（`exampleDocs/` 配下）に配置する
- `.tmp/` および `settings.local.json` はコミットしない
- `prompt/*/working/` の一時プロンプトは完成後に適切なカテゴリへ移動する

---

## MCP サービス一覧

`.claude/settings.json` で設定。詳細は同ファイルのコメントを参照。

| サービス | パッケージ | 用途 |
|---|---|---|
| filesystem | `@modelcontextprotocol/server-filesystem` | ローカルファイル操作 |
| github | `@modelcontextprotocol/server-github` | GitHub API（Issue/PR/Repo） |
| fetch | `@modelcontextprotocol/server-fetch` | Web ページ取得 |
| memory | `@modelcontextprotocol/server-memory` | 会話横断の永続メモリ |
| brave-search | `@modelcontextprotocol/server-brave-search` | Web 検索 |
| postgres | `@modelcontextprotocol/server-postgres` | PostgreSQL 操作 |
| slack | `@modelcontextprotocol/server-slack` | Slack 連携 |
| playwright | `@modelcontextprotocol/server-playwright` | ブラウザ自動化・スクレイピング |

---

## スキル一覧（Claude Code スラッシュコマンド）

`.claude/commands/` に定義。

| コマンド | 説明 |
|---|---|
| `/new-branch` | `ai-claudecode/{name}` ブランチを作成して作業開始 |
| `/plan-pr` | Plan モードで計画→実装→PR 作成までの一連フロー |
| `/commit` | コミットメッセージを生成してコミット |
| `/review-pr` | PR の差分をレビュー |
