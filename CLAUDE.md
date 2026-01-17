# CLAUDE.md

## Purpose
Ship clean, understandable, maintainable code — fast.

## TL;DR（非交渉）
- シンプルが正義。複雑は悪。
  - MUST prefer simple solutions over complex ones.
- 依頼された範囲だけ実装する（勝手に機能追加しない）。
  - MUST implement only what the user asked.
- 変更は最小差分。既存を壊さない。
  - MUST keep changes minimal and avoid breaking existing behavior.
- ユーザーへの返答は常に日本語（短文・結論先）。
  - MUST respond to the user in Japanese.

## 詳細ルール
`.claude/rules/` 以下を参照：
- `core.md` — コード品質・レビュー方針
- `project.md` — [Project] 固有の技術スタック・API・DB構造
- `ui.md` — UI/UXガイドライン
- `workflow.md` — 作業フロー・承認が必要な変更

