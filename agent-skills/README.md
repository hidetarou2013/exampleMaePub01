# agent-skills

全 AI エージェント共通のスキルライブラリ。
各エージェントで再利用できるプロンプトテンプレート・作業手順を管理する。

## ディレクトリ構成

```
agent-skills/
├── common/                 # 全エージェント共通テンプレート
│   ├── plan-template.md    # 計画書テンプレート
│   ├── review-checklist.md # レビューチェックリスト
│   └── commit-template.md  # コミットメッセージルール
├── claudecode/             # Claude Code への適用ガイド・固有スキル
├── codex/                  # Codex への適用ガイド・固有スキル
├── copilot/                # GitHub Copilot への適用ガイド・固有スキル
└── kiro/                   # AWS Kiro への適用ガイド・固有スキル
```

## スキルの追加ルール

1. まず `common/` に汎用テンプレートを作成する
2. エージェント固有の実装・変換が必要な場合は `{agent}/` に配置する
3. Claude Code のスラッシュコマンドとして登録する場合は `.claude/commands/` にコピーする

## エージェントとスキル定義の対応

| エージェント | スキル定義場所 | 呼び出し方 |
|---|---|---|
| Claude Code | `.claude/commands/*.md` | `/コマンド名` |
| Codex | `.codex/instructions/` | システムプロンプトに組み込み |
| GitHub Copilot | `.github/copilot-instructions.md` | Copilot Chat で参照 |
| AWS Kiro | `.kiro/steering/` | ステアリングファイルとして読み込み |
