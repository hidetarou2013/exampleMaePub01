# exampleMaePub01

各種ドキュメント形式のサンプルファイルを管理するリポジトリ。

## 対象 AI エージェント

| エージェント ID | サービス |
|---|---|
| `claudecode` | Claude Code (Anthropic) |
| `codex` | Codex (OpenAI) |
| `copilot` | GitHub Copilot |
| `kiro` | AWS Kiro |

## ディレクトリ構成

```
.
├── .claude/                    # Claude Code 設定・カスタム命令
├── .codex/                     # Codex 設定・カスタム命令
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
│   ├── excel/
│   ├── html/
│   ├── markdown/
│   ├── mermaid/
│   ├── pdf/
│   ├── ppt/
│   └── word/
└── .tmp/                       # 一時作業ディレクトリ（git 管理外）
```

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

## 詳細ルール

詳細な作業ルール・命名規則は [CLAUDE.md](./CLAUDE.md) を参照してください。
