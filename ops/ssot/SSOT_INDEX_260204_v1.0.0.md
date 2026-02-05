# SSOT_INDEX（読み順・カノニカル固定） 260204 v1.0.0

## 0. 目的
- “何を先に読むか” と “どれが正か” を機械的に固定し、差し替えを安全にする。

## 1. 読み順（SSOT）
1) PROJECT_ENV_SPEC（環境仕様・運用規格）
2) PROJECT_CONTEXT（目的・分割方針・テンプレ）
3) AGENTS（Hard Rules）
4) CHEATSHEET_COMMANDS（from scratch コマンド）
5) PS7_GUIDELINE（PS7規約）
6) LESSONS_KB（教訓集）

## 2. カノニカル（固定パス）
- PROJECT_ENV_SPEC.md = 最新の versioned を反映したカノニカル
- PROJECT_CONTEXT.md = 同上
- AGENTS.md = 同上
- CHEATSHEET_COMMANDS.md = 同上
- PS7_GUIDELINE.md = 同上（旧名からの移行を含む）
- LESSONS_KB.md = 同上（旧名からの移行を含む）

## 3. 差し替え手順（概要）
1) ops/ssot に versioned を追加（新規）
2) ルートのカノニカルを更新（内容同期）
3) SSOT_INDEX で “最新” を指す
4) CI green を確認
5) 証跡（PR/run/log）を添付して merge

## 4. 更新履歴
- 260204 v1.0.0: versioned SSOT 追加（初版）
