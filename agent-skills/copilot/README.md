# agent-skills / copilot

GitHub Copilot 向けのスキル適用ガイド。

## スキルの登録方法

`agent-skills/common/` のテンプレートを Copilot のカスタム指示として活用する。
リポジトリ全体への指示は `.github/copilot-instructions.md` に記載する。

## 固有の仕組み

| 機能 | 場所 | 説明 |
|---|---|---|
| リポジトリ指示 | `.github/copilot-instructions.md` | Copilot Chat が参照するリポジトリ全体指示 |
| ワークスペース設定 | `.vscode/settings.json` | Copilot 拡張の設定 |

## ブランチ作業フロー

1. ブランチ `ai-copilot/{name}` を作成して作業
2. 計画ドキュメントを `plan/copilot/` に保存
3. PR 作成 → ユーザーに承認依頼
