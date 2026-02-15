# AGENTS.md

## 目的
このリポジトリでのAI作業ルールと制約を定義する。

## 必須ドキュメント
- ソースコードに変更を加えるたびに、必ず `EXPLANATION.md` を更新する。
- `EXPLANATION.md` には、プロジェクト全体を平易な日本語で説明する。

## 作業範囲
- 変更して良い: `index.html`, `styles.css`, `EXPLANATION.md`, `README.md`, `AGENTS.md`
- 変更しない: ビルド成果物、`node_modules/`、生成物

## コーディング規約
- 既存の命名とスタイルに合わせる。
- 明瞭さを優先し、最小限で目的に沿った変更を行う。

## テスト / ビルド
- 利用可能で変更に関係する場合のみ、テストやビルドを実行する。

## コミット方針
- コミットメッセージは英語にする。
- コミットは小さく、目的を一つに絞る。

## 注意事項
- 機密情報やAPIキーは追加しない。
- 外部ネットワークアクセスが必要な場合は事前に相談する。

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
