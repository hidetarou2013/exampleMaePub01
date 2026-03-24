# agent-skills / codex

Codex (OpenAI) 向けのスキル適用ガイド。

## スキルの登録方法

`agent-skills/common/` のテンプレートを Codex のカスタム指示・システムプロンプトとして活用する。
Codex 固有のスキルは `.codex/instructions/` に配置する。

## 固有の仕組み

| 機能 | 場所 | 説明 |
|---|---|---|
| カスタム指示 | `.codex/instructions/` | システムプロンプトへ組み込むテンプレート |
| エージェント設定 | `.codex/config.json` | Codex エージェントの動作設定 |

## ブランチ作業フロー

1. ブランチ `ai-codex/{name}` を作成して作業
2. 計画ドキュメントを `plan/codex/` に保存
3. PR 作成 → ユーザーに承認依頼
