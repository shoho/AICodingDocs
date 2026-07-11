# Spec-Driven Development

仕様で意図を明確にし、テストで正しさを検証し、最小差分で安全に進める。

## フロー

Explore → Plan → Spec → Test → 実装 → 検証 → 報告

リスク分類が Low の軽微な変更(差分を一文で説明できるもの)はフローを省略し、実装 → 検証 → 報告のみでよい。

1. **Explore**: 目的に必要な範囲だけ読む。不明点は仮説として扱う
2. **Plan**: 変更点の要約 / 影響範囲 / verify方法 / リスク分類を書く
3. **Spec**: Mini Spec + Acceptance Criteria を書く
4. **Test**: AC に基づきテストを先に書く
5. **実装**: 最小差分でコーディング
6. **検証**: 型 / Lint / テスト / 主要導線
7. **報告**: 報告フォーマットに従う

## Mini Spec

実装前に書く。1画面以内。曖昧語を排除し入出力を具体的に。

```
Goal: [1行]
Non-goals: [スコープ外]

Behavior:
  Input: [入力データ・トリガー]
  Process: [処理内容]
  Output: [出力・レスポンス]
  Example: [入出力例1〜2個]

Edge cases:
  - [条件]: [期待挙動]

Contract impact: [なし / あり → 影響対象とリスク]
Rollback: [戻し方1行]
```

## Acceptance Criteria

- 3〜7個。1項目 = 1検証観点
- Given/When/Then 形式推奨
- 各項目に verify 方法を紐づける（テスト名 / コマンド / 手順）

## テスト

テスト = AI生成コードの検証装置。

- 機能追加: テストを先に書く（Red → Green → Refactor）
- バグ修正: 先に落ちるテストを追加 → 修正 → Green
- テスト名は保証内容を文で書く（例: `test_expired_token_returns_401`）
- Unit テスト優先（外部依存なしのロジック）
- 外部I/Oは interface 化 + Fake/Stub

## リスク分類

### High（事前に明示的OKが必要）
互換性破壊（API / データ構造 / 認証・権限 / 課金 / 主要導線）

→ 原因説明 + 最小修正案 + リスク + Rollback を提示し承認を得る

### Low（承認なしで進めてよい）
タイポ、UI崩れ、ログ追加、軽微リファクタなど

→ 報告に影響範囲・確認方法・戻し方を含める

## Definition of Ready
- Mini Spec + AC + リスク分類 + verify手段が揃っている

## Definition of Done
- 依頼範囲 + AC を満たす
- 既存機能を壊していない
- バグ修正は回帰テスト追加済み
- contract変更時は docs 更新済み

## 報告フォーマット
- **変更点**: 何を変えたか
- **理由**: なぜそうしたか
- **確認**: どう確認したか
- **リスク**: 影響範囲 / Rollback
- **テスト**: 追加/更新したテスト
