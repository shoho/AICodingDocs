# AICodingDocs

AI コーディング(主に Claude Code)のための設定・ルール・参考資料を管理するリポジトリ。

## 構成

### Claude Code 設定

| ファイル | 内容 |
|---|---|
| [CLAUDE.md](CLAUDE.md) | 汎用ワークフロー方針(計画・サブエージェント・実装・継続的改善) |
| [.claude/rules/workflow.md](.claude/rules/workflow.md) | Spec 駆動開発の詳細フロー(Mini Spec / AC / リスク分類 / 報告フォーマット) |
| [.claude/rules/ui.md](.claude/rules/ui.md) | UI デザイン原則(UI 関連ファイルを扱うときのみ読み込まれる path-scoped rule) |

これらは他プロジェクトへコピーまたはシンボリックリンクして使う汎用テンプレート。公式ドキュメント([Best practices](https://code.claude.com/docs/en/best-practices) / [Memory](https://code.claude.com/docs/en/memory))の推奨(200行未満・具体的・重複なし)に準拠。

### 参考資料(docs/)

| ファイル | 出典 | 備考 |
|---|---|---|
| The-Complete-Guide-to-Building-Skill-for-Claude.pdf | Anthropic 公式「The Complete Guide to Building Skills for Claude」 | Skills(SKILL.md)の設計・テスト・配布ガイド |

### プロンプト設計の公式ガイド

外部ドキュメントのコピーは置かず、常に最新の公式ガイドを参照する:

- Claude: [Prompting best practices](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-4-best-practices)
- Gemini: [Prompt design strategies](https://ai.google.dev/gemini-api/docs/prompting-strategies)

## メンテナンス方針

- ルールへの追記は「同じ修正指示を2回受けたとき」を目安にする
- 外部ドキュメントを追加する場合は、出典 URL・取得日・ライセンスをファイル冒頭または本 README に明記する
