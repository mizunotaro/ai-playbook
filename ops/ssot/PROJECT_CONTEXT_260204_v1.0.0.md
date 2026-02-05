# PROJECT_CONTEXT（目的・分割方針・テンプレ） 260204 v1.0.0

## 0. このファイルの位置づけ（SSOT）
- プロジェクトの目的、分割方針、AI実行の“定型”を定義する。

## 1. 目的（Goal）
- AIチームが GitHub Issue → PR → CI → Triage → Daily report のループで開発できる環境を設計・改善する
- Judge は CI（greenのみmerge可）

## 2. 対象リポジトリと役割
- ai-playbook: reusable workflow + 教訓（運用知）
- crm-lab-sandbox: 実験/検証用のアプリ/テンプレ（playbook利用側）

## 3. 開発オペレーション（ループ）
1) Queue: GitHub Issues（label: ai:ready）
2) Delivery: Pull Requests（label: ai:in-progress）
3) Judge: CI（greenのみmerge可）
4) Automation: GitHub Actions（reusable workflow中心）
5) Report: AI Daily Report（要点/失敗/次アクション）

## 4. 分割方針（small PR）
- 1 PR = 1目的（IssueのACに対応）
- 段階化：PoC → 本実装 → 最適化
- 依存変更は ai:deps ラベルがない限りしない

## 5. “必ず守る前提”（設計原則）
- Secrets は GitHub Secrets（ローカル/Repoへ保存しない）
- 破壊的操作禁止（例外は人間承認）
- WSL2は使わない（Windows11 + PowerShell7 前提）
- 操作は PowerShell7 + ブラウザをフロントエンドとする

## 6. テンプレ（Issue / PR）
### 6.1 Issue テンプレ（例）
- Goal / AC
- Constraints（deps禁止、破壊操作禁止など）
- Evidence（ログ、スクショ、runリンク）
- Rollback

### 6.2 PR テンプレ（SSOT更新）
- 目的
- 変更点（small）
- 影響範囲
- 検証（ローカル/CI）
- 証跡リンク

## 7. 更新履歴
- 260204 v1.0.0: versioned SSOT 追加（初版）
