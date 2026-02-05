# AGENTS（AI運用ハードルール） 260204 v1.0.0

## 0. このファイルの位置づけ（SSOT）
- このプロジェクトにおける **AIの絶対遵守ルール** を定義する。
- 迷ったら本ファイルを優先する（例外は明示的にSSOT_INDEXで指定）。

## 1. 目的（Why）
- GitHub Issues→PR→CI→Triage→Daily report のループを、**事故（秘密漏洩・破壊的操作・無限ループ・巨大PR）を最小化**して回す。
- 誰でも from scratch で再現できることを最優先する。

## 2. 固定カノニカル値（絶対にブレさせない）
- GitHub owner: mizunotaro
- Git global user.name: Taro Mizuno
- Git global user.email: mizuno.taro@gmail.com
- Local roots: C:\src\_sandbox / C:\src\crm-lab
- Primary model: zai/glm-4.7（fallback: zai/glm-4.6）
- WSL2: 不要（使わない）
- Secrets: GitHub Secrets がSSOT（ローカル/リポジトリへ保存しない）

## 3. Hard Rules（禁止・制限）
### 3.1 Secrets / 個人情報
- **秘密情報（API Key等）を出力・ログ・コミットしない**
- 必要時は「GitHub Secretsに保存する手順」だけ提示（値は扱わない）

### 3.2 破壊的操作
- 破壊的コマンド（権限/レジストリ/ディスク操作/force push/履歴改変）は原則禁止
- 例外は「人間の明示承認（Issue/PRコメント）」がある場合のみ

### 3.3 依存関係変更
- 依存変更は原則禁止（Issueに ai:deps ラベルがある場合のみ許可）
- 不明なら止めて提案に切り替える

### 3.4 PRのサイズ制限（small PR原則）
- 1 PR = 1 Issue（原則）
- “巨大PR” を避ける（ファイル数/行数/領域を最小化）
- 既存の動作に影響する変更は段階化（PoC→本実装）

### 3.5 ループ/無限実行の回避
- 同一エラー/同一操作を2回以上繰り返して進展がない場合は **解雇→入替** を推奨

## 4. ガードレール（Actions/Local 共通）
- AI_AUTOMATION_MODE: RUN / PAUSE / DRYRUN
- AI_MAX_OPEN_AI_PRS: 同時PR上限
- AI_MAX_ATTEMPTS_PER_ISSUE: 1 Issue あたりの試行上限
- これらは Workflow / Script の両方で参照できるようにする

## 5. “おかしなAIセッション”の解雇・入替（必須運用）
### 5.1 判定条件
- 同一エラー/同一操作を2回以上繰り返す
- Hard Rules抵触（秘密/破壊的操作/巨大PR/依存変更など）
- IssueのACに無関係、進捗がない、支離滅裂

### 5.2 Actions run の標準手順
1) 該当 run をキャンセル（gh run cancel）
2) 証跡（runリンク、失敗箇所）をIssueへコメント（秘密は伏せる）
3) Issue を ai:triage または ai:blocked にする
4) クリーンなコンテキストで再実行（gh run rerun / workflow_dispatch）
5) 必要なら AI_AUTOMATION_MODE=PAUSE で封じ込め

### 5.3 Local（OpenCode）標準手順
1) OpenCode停止
2) 新 worktree 作成
3) SSOT + issue本文だけの最小コンテキストで新セッション開始

## 6. ロギング方針（推奨）
- Start-Transcript は「ロック環境では非推奨」（追記ファイルロックで落ち得る）
- **1実行=1ログディレクトリ**（タイムスタンプ付）に分割出力する
- 失敗しても「証跡だけは残す」（例外を握りつぶさず、最後に要約を出す）

## 7. 更新履歴
- 260204 v1.0.0: versioned SSOT 追加（初版）
