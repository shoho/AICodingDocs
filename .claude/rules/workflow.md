# Workflow

## 標準フロー
1) 要件を1〜3行で言い換える（ズレやすい前提だけ潰す）
2) 実装方針：最小案 + 代替があるなら1つだけ
3) 実装：最小差分（影響が広ければ分割）
4) 検証：型/Lint/単体テスト/主要導線（iPhone+iPad）
5) 報告：何を変えた / なぜ / どう確認したか

- 提案と実装は分ける。
  - SHOULD present options, then implement only the chosen scope.

## バグ修正（共通）
- 再現 → 原因切り分け → 修正方針 → 修正 → 再発防止（テスト/ガード）

## 事前に明示的OKが必要（High Risk）
- 互換性破壊（API互換・データ構造・認証・課金）
- Firestore既存データに影響する変更（マイグレーション等）
- 本番設定変更
  - MUST get explicit approval before high-risk changes.

進め方：
1) 原因を特定して短く説明
2) 修正案（最小案）とリスクを提示
3) OK後に着手

## OKなしで進めてよい（Low/Medium）
- ローカルなバグ修正、UI崩れ、タイポ、ログ追加、軽微リファクタ
  - MAY proceed without approval if scope is clearly low-risk.

ただし報告に必ず入れる：
- 影響範囲
- 確認方法（再現手順/動作確認）
- 戻し方（ロールバック/変更点の要約）

## Definition of Done（完了条件）
- 依頼範囲を満たす
- 既存機能を壊していない（主要導線の確認）
- 失敗時の挙動（表示 or ログ）が最低限ある
- 必要ならドキュメント更新
  - MUST update docs when behavior/contract changes.

## 単体テスト
- 関数を追加・修正したら、対応する単体テストを追加する
  - SHOULD add unit tests when adding or modifying functions.
- テスト対象：外部依存のないユーティリティ、バリデーション、ビジネスロジック
