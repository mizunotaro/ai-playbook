# PS7_GUIDELINE（PowerShell 7 コーディング規約） 260204 v1.0.0

## 0. 目的
- “細かなコーディングミス”で止まらないための **事故りにくい PS7 スタイル** を定義する。
- CI/自動化で再現性を担保する。

## 1. 必須ヘッダ（最小）
- #requires -Version 7.0
- Set-StrictMode -Version Latest
- $ErrorActionPreference = 'Stop'
- **param は最初**（param前に実行コードを書かない）

## 2. 文字列/クォート規約（事故回避）
- --% の乱用禁止（意図せぬエスケープ無効化）
- JSON/YAMLのインライン生成は避け、可能ならファイルに出力して --body-file などを使う
- gh には --silent を安易に付けない（ボディが無くなり JSON parse が壊れる）

## 3. ロギング規約（推奨）
- Start-Transcript 非推奨（ロック環境で落ち得る）
- 1実行=1ログディレクトリ（timestamp）に分割出力
- Write-Host 乱用禁止：ログはファイルへ、重要点のみ標準出力へ

## 4. I/O とパス
- Join-Path を基本にする
- -LiteralPath を基本にする（ワイルドカード事故を防ぐ）
- Compress-Archive の '*' は「存在チェック」してから使う（存在しないと落ちる）

## 5. Git 操作の安全策
- 作業前に git status --porcelain を確認し clean を要求する
- 直接 main へ push しない（例外は明示承認）
- ブランチ名は timestamp を含めて衝突回避

## 6. gh CLI の安全策
- gh auth status を事前確認
- gh pr create の前に git log --oneline origin/main..HEAD を確認（差分が無いと失敗する）
- PR作成後の --auto はオプション扱い（ロールバック導線を残す）

## 7. 典型的な落とし穴（抜粋）
- else が “コマンド扱い” になる：直前の '}' の位置/改行/コメント崩れを疑う
- ']' / ')' の対応ミス：配列/サブ式のネストを最小化し、変数に分解する
- Get-Content / Set-Content のエンコーディング差：UTF-8（No BOM）に揃える

## 8. 更新履歴
- 260204 v1.0.0: versioned SSOT 追加（初版）
