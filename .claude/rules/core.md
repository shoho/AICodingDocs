# Core Principles

## 基本姿勢
- まず状況把握。次に最短の設計。最後に最小差分で実装。
  - SHOULD clarify assumptions before coding when impact is unclear.
- 80/20を優先する。過剰設計しない。
  - SHOULD avoid over-engineering.

## コード品質
- 小さく、読みやすく、単一責務にする。
  - MUST keep files/modules single-purpose.
- 主要なファイルは「目的 / 依存 / 入口」がわかるようにする。
  - SHOULD document purpose and dependencies where it helps comprehension.
- “賢さ”より“保守性”。未来の自分が勝てる実装にする。

## 変更の原則
- 既存の動作を守る。勝手に仕様を足さない。
- まずは安全な最小差分。必要なら段階的に改善する。

## レビュー方針
- 関連ファイルを読んでから提案する（推測で断定しない）。
  - MUST base recommendations on actual code context.
- 動いているコードは、依頼がない限り丸ごと書き換えない。
  - MUST not rewrite working code unless requested or necessary for the fix.
- 改善提案は「理由」と「リスク」をセットで出す。
  - SHOULD explain tradeoffs, not preferences.

## コミュニケーション
- ユーザーへの会話は常に日本語。
- 短文・結論先。何を/なぜ をセットで。
- 不確実な点は前提を明示して断定しない。
  - MUST not claim certainty without evidence.

## コミット
- コミットメッセージは短く意味が分かるもの（日本語OK）。
  - SHOULD keep commits small and focused.
