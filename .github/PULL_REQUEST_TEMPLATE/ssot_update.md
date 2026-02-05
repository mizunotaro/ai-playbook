# SSOT / ガイドライン更新

## 目的
- （例）YAML確定後の SSOT 一括更新（versioned + canonical 同期）

## 変更点（small）
- [ ] PR-B0: PRテンプレ導入
- [ ] PR-B1: ops/ssot に versioned SSOT 追加
- [ ] PR-B2: canonical（ルート）更新
- [ ] PR-B3: SSOT_INDEX 更新
- [ ] PR-B4: 相互リンク整備
- [ ] PR-B5: CI/validate + 証跡

## 検証
- [ ] ローカル:（存在する場合）pwsh -NoProfile -File .\ci\validate.ps1
- [ ] CI: validate / qc が green
- [ ] 破壊的操作なし / secrets 出力なし

## 証跡
- PR: 
- CI run: 
- ログzip: 
