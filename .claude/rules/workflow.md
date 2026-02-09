# .claude/rules/workflow.md
# Rules: Spec-Driven + Test-Driven Workflow

目的：仕様（Spec）を先に固め、テスト（Test）で期待を固定し、最小差分で安全に進める。

## 0) 原則
- SIMPLE = GOOD, COMPLEX = BAD
- 提案（設計/選択肢）と実装（コード変更）は分ける
- 迷うポイントを先に潰す（後工程での手戻りを最小化）
- Verify を先に用意する（テスト/コマンド/手順。無いなら先に提案/作る）

## 1) 標準フロー（Explore → Plan → SDD → TDD → 実装）

### 1.1 Explore（探索）
- 目的の確認に必要な範囲だけ読む（最小の関連ファイル / 既存仕様 / ログ）
- 不明点は仮説として扱い、断定しない

### 1.2 Plan（計画）
- 小変更（タイポ、コメント、ログ1行、明確なlint修正）以外は Plan を書いてから着手
- Plan には以下を含める：
  - 変更点の要約（1〜5行）
  - 影響範囲
  - verify 方法（テスト/コマンド/手順）
  - リスク分類（High/Low）

### 1.3 SDD → TDD → 実装
1. 要件確認: 要件を1〜3行で言い換える（ズレやすい前提だけ潰す）
2. Mini Spec作成: 仕様を書く（短く、迷う点だけ）
3. Acceptance Criteria作成: 受け入れ条件を書く（3〜7個）
4. 実装方針決定: 最小案 + 代替があるなら1つだけ提示
5. TDD: テストで期待を先に固定（可能な範囲で Red → Green → Refactor）
6. 実装: 最小差分でコーディング（影響が広ければ分割）
7. 検証: 型/Lint/単体テスト/主要導線（iPhone+iPad）
8. 報告: 何を変えた / なぜ / どう確認したか

## 2) Mini Spec（必須）
実装前に以下を短く書く（長くしない。1画面を目安）：
- Goal: 目的 / 何を達成するか
- Non-goals: やらないこと / 今回スコープ外
- Behavior: 期待挙動
  - 入力→出力 / 状態遷移 / 表示・レスポンス例を1〜2個
- Edge cases: 例外・失敗時
  - バリデーション / エラー表示 or ログ / リトライ方針
- Contract impact: 契約への影響
  - API互換 / データ構造 / 認証(App Check/ID Token/Claims) / 課金 / 主要導線 / 権限
  - ありの場合は High Risk（明示OK必須）
- Rollback: 戻し方
  - フラグ・設定・revertなど、戻せる手段を1行

## 3) Acceptance Criteria（必須）
- MUST 箇条書きで3〜7個
- MUST 曖昧語を避ける（「いい感じに」ではなく「〜ができる/〜になる」）
- SHOULD 1項目＝1検証観点（テストに落ちる粒度）
- MUST それぞれに verify 方法を紐づける（テスト名 / コマンド / 手動手順のどれか）

## 4) TDD Rules
### 4.1 機能追加・仕様変更
- MUST 期待挙動をテスト（またはテストに相当する検証可能な形）で先に書く
- SHOULD Red → Green → Refactor の順で進める
- SHOULD テスト名は「何が保証されるか」を文で書く

### 4.2 バグ修正
- MUST 再現 → 原因切り分け → 修正方針 → 修正 → 再発防止（回帰テスト）
- MUST 先に「落ちるテスト（回帰テスト）」を追加してから修正する

### 4.3 テスト優先順位
1. Unit: 外部依存なしのロジック（ユーティリティ、モデル、バリデーション、変換、ビジネスロジック）

### 4.4 外部依存の扱い
- SHOULD 外部I/Oは interface 化し、Fake/Stub で unit を安定させる
- SHOULD Integration は emulator / ローカルで再現可能にする

## 5) リスク分類（明示OKが必要）
### 5.1 High Risk（事前に明示的OKが必要）
- 互換性破壊（API互換・データ構造・認証/権限・課金・主要導線）

進め方：
1. 原因/背景を短く説明
2. 修正案（最小案）とリスクを提示
3. Rollback を明記
4. MUST get explicit approval before high-risk changes.
5. OK後に着手

### 5.2 Low/Medium（OKなしで進めてよい）
- ローカルなバグ修正、UI崩れ、タイポ、ログ追加、軽微リファクタ
- MAY proceed without approval if scope is clearly low-risk.

ただし報告に必ず入れる：
- 影響範囲
- 確認方法（再現手順/動作確認）
- 戻し方（ロールバック/変更点の要約）

## 6) Definition of Ready（着手条件）
- MUST Mini Spec がある
- MUST Acceptance Criteria がある
- MUST リスク分類（High/Low）が明確
- MUST verify 手段（テスト/コマンド/手順）が1つ以上ある
- SHOULD 影響範囲とRollbackが1行で書ける

## 7) Definition of Done（完了条件）
- MUST 依頼範囲を満たす
- MUST Acceptance Criteria を満たす（テスト or 検証手順がある）
- MUST 既存機能を壊していない（主要導線の確認）
- MUST 失敗時の挙動（表示 or ログ）が最低限ある
- MUST バグ修正は回帰テストが追加されている
- MUST behavior/contract が変わるなら docs 更新

## 8) 単体テスト（iOS）
- MUST 関数を追加・修正したら、対応する単体テストを追加する
- テスト対象: 外部依存のないユーティリティ、モデル、ビジネスロジック

## 9) 単体テスト（Server）
- MUST 関数を追加・修正したら、対応する単体テストを追加する
- テスト対象: 外部依存のないユーティリティ、バリデーション、ビジネスロジック

## 10) 報告フォーマット（必須）
- 変更点: 何を変えたか（箇条書き）
- 理由: なぜそうしたか（Mini SpecのGoalに紐づける）
- 確認: どう確認したか（コマンド/手順/導線）
- リスク: 影響範囲 / Rollback
- テスト: 追加/更新したテスト（該当ファイル名とテスト内容）
