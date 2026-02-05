# LESSONS_KB（教訓集） 260204 v1.0.0

## 0. 目的
- 失敗の再発防止と、AIチームの自己修復（self-healing）を目的に **“教訓をSSOT化”** する。

## 1. エントリ形式（必須）
- ID: L-YYYYMMDD-XXX
- Title
- Context（何をしていたか）
- Symptom（何が起きたか）
- Root Cause（確定 / Uncertain）
- Fix（恒久対応）
- Prevention（事前回避）
- Evidence（ログ/PR/runリンク）
- Related（SSOT/Workflow/Script）

## 2. 重要教訓（抜粋・要約）
### 2.1 Start-Transcript 非推奨
- 症状: 追記中の transcript ファイルが一時ロック → 追記失敗でスクリプトが停止
- 対策: 1実行=1ログディレクトリで分割ログ、ファイル書込はリトライ

### 2.2 param ブロックは先頭
- 症状: 実行時に落ちる/パーサーエラー
- 対策: param() は最初、ヘッダコメントの後

### 2.3 PR作成前の差分確認
- 症状: main に push してから PR を作ろうとして失敗（差分無し）
- 対策: origin/main..HEAD を必ず確認し、ブランチ運用を徹底

## 3. 教訓の追加フロー
1) 事象発生 → 証跡（ログ/スクショ/runリンク）保存
2) Root Cause を確定（Uncertain なら検証方法も記載）
3) Fix/Prevention を SSOT/Workflow/Script に反映（small PR）
4) KBへ登録、関連SSOTを更新

## 4. 更新履歴
- 260204 v1.0.0: versioned SSOT 追加（初版）
