# AUTO_MERGE_POLICY（自動マージ運用ポリシー） 260206 v1.0.2

## 0. 目的
- PR の auto-merge を **安全に段階導入**するための SSOT。
- 「機械的ゲート（決定論）」を主、AI は補助（助言）に限定し、暴発を防ぐ。

## 1. 基本方針（最重要）
1) **default = PAUSE**（原則停止）
2) auto-merge を許可する条件は **決定論ゲート**で固定（required checks / labels / deps例外 / 証跡）
3) AI（Z.AI GLM / OpenCode Coding Plan）は **レビュー・分類・提案**を最大化するが、単独で merge を決定しない
4) “同一失敗2回” で triage（解雇→入替）を促す（ループ防止）

## 2. 制御パラメータ（推奨: Repo Variables）
- `AI_AUTOMATION_MODE`: `RUN` / `PAUSE` / `TRIAGE_ONLY`
  - RUN: AI オーケストレーション実行可
  - PAUSE: 実行しない（証跡収集のみは可）
  - TRIAGE_ONLY: 変更提案のみ（PR作成まで）
- `AI_AUTO_MERGE_MODE`: `PAUSE` / `RULES_ONLY` / `RULES_PLUS_AI`
  - PAUSE: auto-merge attempt しない
  - RULES_ONLY: 決定論ゲートを満たす場合のみ auto-merge attempt
  - RULES_PLUS_AI: RULES_ONLY + AI-QC が “OK” の場合に attempt（ただしAI単独決定禁止）
- `AI_MAX_OPEN_AI_PRS`: 同時PR上限（例: 2）
- `AI_MAX_ATTEMPTS_PER_ISSUE`: 1 Issue あたりの試行上限（例: 2）

## 3. 決定論ゲート（RULES_ONLY）
### 3.1 必須条件（全て満たす）
- required checks が **すべて成功**（例: validate / AI_QC）
- PR が **draft ではない**
- **deps変更なし**（または `ai:deps` ラベルあり）
- **破壊的操作なし**（Hard Rules）
- 証跡 artifact が出力されている（最低限）
  - `gh_pr_view.json`
  - `gh_run_list.json`
  - 実行ログ（*.log）

### 3.2 追加条件（推奨）
- PR ラベルに `ai:automerge` がある
- PR 変更範囲が “低リスク” に限定（例: docs/ops/ssot/.github/workflows の一部）
  - 初期は docs-only に限定し、段階的に対象を拡張する

## 4. AI の役割（RULES_PLUS_AI）
- AI は以下を実施し、**PRコメント + JSON**で証跡化する
  - 変更意図 / 影響範囲の要約
  - secrets混入・deps変更・破壊的変更の疑い検知
  - テスト不足 / ロールバック欠如の指摘
  - コンフリクト発生時の解決方針（A/B）提示
- ただし、最終的な auto-merge attempt は **決定論ゲートの通過が前提**。

## 5. 段階導入（推奨ロードマップ）
- Phase 0: `AI_AUTO_MERGE_MODE=PAUSE`（完全停止）
- Phase 1: `RULES_ONLY`（docs-only のみ）
- Phase 2: `RULES_ONLY`（コード変更にも拡張、deps はラベル必須）
- Phase 3: `RULES_PLUS_AI`（AI-QC を informational → required に段階移行）

## 6. 例外・緊急停止
- 例外は “人間の明示承認” がある場合のみ
- 重大インシデント時は `AI_AUTOMATION_MODE=PAUSE` に落として封じ込め

## 7. 更新履歴
- 260206 v1.0.2: 初版（docs-only Issue 1）

