# CHEATSHEET_COMMANDS（from scratch 実行コマンド集） 260204 v1.0.0

## 0. 目的
- “一本道”で再現できるように、PowerShell7 での標準手順をまとめる。

## 1. 前提
- Windows 11 + PowerShell 7
- Local roots: C:\src\_sandbox / C:\src\crm-lab
- gh CLI インストール済み、GitHubへログイン済み

## 2. PR-B（SSOT一括更新） small PR の切り方（推奨順）
> YAML確定後に「まとめて更新」する場合でも、レビュー/ロールバック容易性のために分割する

1) PR-B0: .github/PULL_REQUEST_TEMPLATE/ssot_update.md 導入（テンプレ固定）
2) PR-B1: ops/ssot/ に versioned SSOT を追加（新規ファイルのみ）
3) PR-B2: ルートの canonical（AGENTS.md 等）を versioned と同期（差分は最小）
4) PR-B3: SSOT_INDEX.md を更新（読み順・最新参照）
5) PR-B4: ドキュメント相互リンク（CHEATSHEET/PROJECT_CONTEXT から参照）
6) PR-B5: CI/validate を回して証跡採取（runリンク、ログ、生成物）

※ “一括”でやる場合は PR-B1〜B3 を同一PRにまとめてもよいが、手戻りが増えやすい。

## 3. 代表コマンド（例）
- git status --porcelain
- gh auth status
- gh pr create --title ... --body-file ...
- gh pr merge --auto --squash（必要時のみ）

## 4. 更新履歴
- 260204 v1.0.0: PR-B small PR順序を追記（初版）
