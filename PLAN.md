# PLAN.md

## タスク進捗
| ID | タスク | 状態 | 対象ファイル | メモ |
| --- | --- | --- | --- | --- |
| T0 | 進捗管理ルールの整備と移管 | 完了 | `AGENTS.md`, `README.md`, `PLAN.md` | 進捗管理を `README.md` から `PLAN.md` へ移管 |
| T1 | フォント改善のサンプルHTML作成と確認 | 完了 | `reference/font-size-compare.html`, `PLAN.md` | 改善案をユーザー確認済み |
| T2 | 問題文・敵数字フォントの本実装 | 完了 | `index.html`, `PLAN.md` | 問題文38px、敵数字28px、可読性向上スタイルを反映 |
| T3 | 早押し得点（+3〜+1）実装 | 完了 | `index.html`, `PLAN.md` | 0.9秒以内:+3 / 1.8秒以内:+2 / それ以降:+1 |
| T4 | 説明ドキュメント更新 | 完了 | `EXPLANATION.md`, `PLAN.md` | フォント改善と早押し得点ルールを追記 |
| T5 | エリア着弾ベース得点への置換 | 完了 | `index.html`, `PLAN.md` | 時間加点を削除し、Area3/2/1=3/2/1点へ変更 |
| T6 | エリア境界線・表示文言調整 | 完了 | `index.html`, `PLAN.md` | lockline基準の2本線、CORRECT表示ルール反映 |
| T7 | 説明ドキュメント更新（得点仕様差し替え） | 完了 | `EXPLANATION.md`, `PLAN.md` | 早押し説明をエリア得点仕様へ差し替え |
| T8 | iOS Chrome の viewport 高さ追従対応 | 完了 | `index.html`, `styles.css`, `PLAN.md` | `visualViewport` と `--app-height` で見切れを防止 |
| T9 | 説明ドキュメント更新（viewport対応） | 完了 | `EXPLANATION.md`, `PLAN.md` | 高さ同期と `scale.refresh()` の説明を追記 |
| T10 | `.gitignore` から `reference/` の除外を解除 | 完了 | `.gitignore`, `PLAN.md` | `reference/` を Git 管理対象に戻す |
| T11 | HUDパネル（SCORE/SPEED/LIFE）デザイン調整 | 完了 | `index.html`, `EXPLANATION.md`, `PLAN.md` | SVG寄せレイアウト・LIFEバー表示へ更新 |
| T12 | HUD上段パネルの重なり解消（狭幅対応） | 完了 | `index.html`, `EXPLANATION.md`, `PLAN.md` | 画面幅に応じてSCORE/LIFE幅と文字サイズを自動調整し、重なりを防止 |
| T13 | HUDパネルの縦幅縮小と横一列レイアウト化 | 完了 | `index.html`, `EXPLANATION.md`, `PLAN.md` | SCORE/SPEED/LIFEを上段1列へ再配置し、縦幅を縮小 |
| T14 | HUDラベル短縮（A案）と等幅パネル化 | 完了 | `index.html`, `EXPLANATION.md`, `PLAN.md` | SCR/SPD/LIFへ短縮し、上段3パネルを同じ幅に統一 |
| T15 | LIFE数値ラベルを削除してバー表示のみへ変更 | 完了 | `index.html`, `EXPLANATION.md`, `PLAN.md` | 右パネルの表示をライフバー専用にする |
| T16 | 画面変更時のプレビュー確認ルールをAGENTSへ追加 | 完了 | `AGENTS.md`, `PLAN.md` | 今後のUI変更でプレビュー表示を必須化 |
| T17 | マージ競合を防ぐ事前チェック手順を追加 | 完了 | `AGENTS.md`, `PLAN.md` | PR前の差分確認と競合時の解消方針を明文化 |
| T18 | LIFEパネルにLIFラベルを戻しバー減少方向を上からへ変更 | 完了 | `index.html`, `EXPLANATION.md`, `PLAN.md` | LIFラベル+右側バー、減少時は上から白抜き化 |
| T19 | LIFEパネルのフォントサイズを他HUDと統一 | 完了 | `index.html`, `EXPLANATION.md`, `PLAN.md` | LIFラベルの文字サイズを他パネルと合わせる |
| T20 | 問題表示パネルのサイバー演出強化 | 完了 | `index.html`, `EXPLANATION.md`, `PLAN.md` | 半透明枠・四隅L字・大きめフォント・シアングローへ更新 |
| T21 | 問題パネルのHUD非重なり対応（B+C） | 完了 | `index.html`, `EXPLANATION.md`, `PLAN.md` | HUD→問題の縦積み固定と狭画面での段階縮小を実装 |
| T22 | スクリーンショット取得手順の安定化ルールを追加 | 完了 | `AGENTS.md`, `PLAN.md` | サーバー疎通確認・保存パス統一・失敗時報告テンプレを明文化 |
| T23 | HUDと問題パネルの上寄せ調整 | 完了 | `index.html`, `EXPLANATION.md`, `PLAN.md` | HUD上端の隙間を縮め、問題パネルも連動して上へ移動 |
| T24 | 正解時のみスピードアップする挙動へ調整 | 完了 | `index.html`, `EXPLANATION.md`, `PLAN.md` | 不正解時は落下スピードを維持 |
| T25 | 敵数字フォントを32pxへ拡大し問題文バランスを調整 | 完了 | `index.html`, `EXPLANATION.md`, `PLAN.md` | 敵数字のみ `28px -> 32px`、問題文 `60/56/52px` は維持。390x844でプレビュー確認済み |
| T26 | 初回問題のフォント揺れ防止（Webフォント待機） | 完了 | `index.html`, `EXPLANATION.md`, `PLAN.md` | 起動前にRajdhani読込を最大2.5秒待機し、初回表示の見た目差を抑制。390x844で表示確認済み |
| T27 | スマホChromeのタップ無反応修正 | 完了 | `index.html`, `styles.css`, `EXPLANATION.md`, `PLAN.md` | viewport再計算の過剰実行を抑制し、canvasのタッチ入力設定を強化 |
| T28 | 設定ファイル追加と速度・出題範囲の設定化 | 完了 | `game-settings.js`, `index.html`, `AGENTS.md`, `EXPLANATION.md`, `PLAN.md` | 速度上昇幅、連続正解条件、出題範囲を設定ファイルで変更可能にする |
| T29 | タイトル画面のみ無反応の入力フォールバック修正（UA分岐なし） | 完了 | `index.html`, `EXPLANATION.md`, `PLAN.md` | StartSceneで`currentlyOver`優先 + 座標判定フォールバックを追加し、ゲーム画面ロジックは維持 |
| T30 | START押下後の遷移調査ログ追加（Chrome不具合切り分け） | 完了 | `index.html`, `EXPLANATION.md`, `PLAN.md` | START押下からscene.start到達までをコンソール出力し、詰まり箇所を可視化 |
| T31 | iPhone単体で確認できるデバッグログパネル追加 | 完了 | `index.html`, `styles.css`, `EXPLANATION.md`, `PLAN.md` | 画面右下にLOGトグルを追加し、START遷移ログを端末上で確認可能にした |
| T32 | スマホ共有向けログコピー機能追加 | 完了 | `index.html`, `styles.css`, `EXPLANATION.md`, `PLAN.md` | DebugOverlayにCOPYボタンを追加し、ログをクリップボード/プロンプト経由で共有可能にした |
| T33 | START遷移のaudio resume待機にタイムアウト導入 | 完了 | `index.html`, `EXPLANATION.md`, `PLAN.md` | ブラウザ分岐を除去し、`SFX.resume()`待機を350msで打ち切って遷移継続する |
| T34 | iPhone Chromeでタイトル欠けする問題の対策 | 完了 | `index.html`, `EXPLANATION.md`, `PLAN.md` | 起動前フォント待機にタイトル用フォントを追加し、描画時の字幅ズレを抑制する |

## 運用メモ
- 状態は `未着手 / 進行中 / 完了 / 保留` を使う。
- 複数タスクがある場合は 1 件ずつ進める。
- 実行開始前にこのファイルを確認し、対象タスクを明確にする。
