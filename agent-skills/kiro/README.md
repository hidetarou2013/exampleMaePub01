# agent-skills / kiro

AWS Kiro 向けのスキル適用ガイド。

## スキルの登録方法

`agent-skills/common/` のテンプレートを Kiro のステアリングファイルとして活用する。
Kiro のステアリングファイルは `.kiro/steering/` に配置する。

## 固有の仕組み

| 機能 | 場所 | 説明 |
|---|---|---|
| ステアリングファイル | `.kiro/steering/` | Kiro が常時参照する指示・コンテキスト |
| スペックファイル | `.kiro/specs/` | 機能仕様・要件定義 |
| フックファイル | `.kiro/hooks/` | 自動化トリガー定義 |

## ブランチ作業フロー

1. ブランチ `ai-kiro/{name}` を作成して作業
2. 計画ドキュメントを `plan/kiro/` に保存
3. PR 作成 → ユーザーに承認依頼
