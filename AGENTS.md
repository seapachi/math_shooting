# AGENTS.md

## 目的
このリポジトリでのAI作業ルールと制約を定義する。

## 必須ドキュメント
- ソースコード（`index.html`, `styles.css`, `*.js` など）に変更を加えるたびに、必ず `EXPLANATION.md` を更新する。
- `README.md` や `AGENTS.md` のみを変更する場合、`EXPLANATION.md` の更新は必須ではない。
- `EXPLANATION.md` には、プロジェクト全体を平易な日本語で説明する。

## 作業範囲
- 変更して良い: `index.html`, `styles.css`, `EXPLANATION.md`, `README.md`, `AGENTS.md`
- 変更しない: `node_modules/`、ビルド/生成物（例: `dist/`, `build/`）

## コーディング規約
- 既存の命名とスタイルに合わせる。
- 明瞭さを優先し、最小限で目的に沿った変更を行う。

## テスト / ビルド
- 利用可能で変更に関係する場合のみ、テストやビルドを実行する。

## コミット方針
- コミットメッセージは日本語にする。
- コミットは小さく、目的を一つに絞る。
- コミット実行前にユーザーへ確認し、承認後に実行する。

## 注意事項
- 機密情報やAPIキーは追加しない。
- 外部ネットワークアクセスが必要な場合は事前に相談する。

## 事前確認ルール（必須）
- 機能追加・仕様変更・挙動変更の相談時は、修正前に要件（目的、対象ファイル、期待動作、完了条件）を確認する。
- 不明点がある間は編集せず、要件整理後に「この内容で修正を開始してよいですか？」と確認し、ユーザーの明示的な承認後に着手する。

## 文字コードルール（重要）
- テキストファイルは必ず UTF-8 で保存する（BOMなし推奨）。
- `Shift_JIS / CP932 / UTF-16` で保存しない。
- 対象: `*.html`, `*.css`, `*.md`, `*.js`, `*.json`
- 文字化けしている状態でコミットしない。
- GitHub Pages で `invalid characters for the used encoding UTF-8` が出た場合は、該当ファイルをUTF-8で再保存して再デプロイする。

## 事前チェック（推奨）
PowerShell でコミット前に実行:

```powershell
$bad=@()
foreach($f in (git ls-files)){
  $bytes=[System.IO.File]::ReadAllBytes((Resolve-Path $f))
  try{
    $enc=[System.Text.UTF8Encoding]::new($false,$true)
    $null=$enc.GetString($bytes)
  } catch {
    $bad += $f
  }
}
if($bad.Count){ "Non-UTF8 files:"; $bad } else { "All tracked files are valid UTF-8." }
```
