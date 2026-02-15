# EXPLANATION.md

## このファイルの目的
この文書は、`Math Lane Shooter` の全体構成を初心者向けに説明するためのガイドです。  
「どこを見れば何が分かるか」を短時間で把握できるように整理しています。

## プロジェクトの概要
`Math Lane Shooter` は、計算問題と4レーンシューティングを組み合わせたブラウザゲームです。

- レンダリングとゲーム進行: `Phaser 3`（CDN読み込み）
- 画面デザイン: `styles.css`
- 実行の中心: `index.html`（HTML + JavaScript）

## ファイル構成
- `index.html`
  - ゲーム本体（シーン、入力、描画、当たり判定、問題生成）
- `styles.css`
  - 背景、配色、UI装飾、レスポンシブ表示
- `reference/font-size-compare.html`
  - フォント調整前に見た目を比較する確認用サンプル
- `EXPLANATION.md`
  - この解説ドキュメント
- `README.md`
  - 利用者向けの概要説明
- `AGENTS.md`
  - AI作業ルール

## 画面とシーンの流れ
`index.html` 内で、Phaserのシーンを使って画面遷移しています。

1. `BootScene`
   - 共有テクスチャ（背景、弾、敵、宇宙船）を先に作る準備シーン
2. `StartScene`
   - タイトル画面
   - 機体デザイン切替（`sharp` / `flare`）
   - モード選択（`足し算 / 引き算 / 掛け算`）
   - `START` 押下で `GameScene` へ
3. `GameScene`
   - 問題表示、敵落下、発射、判定、スコア・ライフ管理
4. `ResultScene`
   - 最終スコア表示、再挑戦導線

## 計算問題の作り方
`makeQuestion(mode)` がモードに応じて次の関数を呼びます。

- `makeAddQuestion()`
  - 0〜9 + 0〜9（正解は0〜18）
- `makeSubQuestion()`
  - 引き算（負数を避けるように調整）
- `makeMulQuestion()`
  - 1〜9 × 1〜9

問題文と正解に加えて、誤答候補を作り、4レーンに割り当てます。

## ゲーム進行の考え方
- プレイヤーは4レーン間を移動
- 敵（数字入りブロック）が上から落下
- 正しい数字の敵にショットを当てると得点（着弾エリアで点数が変化）
- 不正解ヒットや見逃しでライフ減少
- ライフが0になると終了

### 正解時の得点ルール（着弾エリア）
`GameScene` では画面を縦3エリアに分け、弾が当たった位置で加点を決めています。

- Area3（上）: `+3`
- Area2（中央）: `+2`
- Area1（下）: `+1`

境界は次の2本線です。

- Area2/Area1 境界: 既存の `LOCK LINE`（`judgeY`）
- Area3/Area2 境界: `judgeY / 2`

※ AUTO判定（敵がLOCK LINE到達時の判定）は維持され、正解時は `+1` です。

## 入力操作
- タップ: レーン移動
- 左右スワイプ: レーン移動
- ダブルタップ: 発射
- 右上ボタン: 一時停止/再開

## デザインの役割分担
- `index.html`
  - Phaser内で描く文字・図形・座標・アニメーション
- `styles.css`
  - ページ背景、枠、グロー、全体トーン

### iOS Chrome の表示差分対策（上下見切れ防止）
iPhone の Chrome は、アドレスバーやツールバーの表示状態で「見えている高さ」が変わることがあります。  
この差分で `100vh` が実画面とずれると、上下が欠けて見える場合があります。

このプロジェクトでは、次の方法で高さを同期しています。

- `styles.css`
  - `:root` に `--app-height` を用意
  - `#game` は `height: 100vh;` の後に `height: var(--app-height);` を指定
- `index.html`
  - `syncAppHeight()` で `window.visualViewport?.height` を優先取得（未対応時は `window.innerHeight`）
  - 取得した高さを `--app-height` に反映
  - 高さ更新後に `game.scale.refresh()` を呼んで、Phaser の `FIT` レイアウトを再計算
  - `resize` / `orientationchange`（必要に応じて `visualViewport` の `resize` / `scroll`）で再同期

この変更はレイアウト制御のみで、得点・ライフ・入力操作などのゲームルールは変更していません。

### フォントの見やすさ改善
`GameScene` 内の表示を次のように調整しています。

- 問題文（上部）: `32px -> 38px`
- 敵数字（選択肢）: `24px -> 28px`
- 文字色は既存のまま（問題文 `#7dd3fc`、敵数字 `#fbbf24`）
- 暗い背景でも輪郭が埋もれにくいように、縁取りと影を調整

見た目を変えるときは、まず `styles.css` の色変数を確認し、次に `index.html` の Phaser描画色を合わせると管理しやすくなります。

## 初心者向けの読み順
1. `index.html` の定数（色、フォント、レーン設定）
2. `makeQuestion()` と各モード問題生成関数
3. `StartScene`（モード選択UI）
4. `GameScene`（生成・移動・衝突・スコア）
5. `styles.css`（最終的な見た目調整）

## 変更時の基本チェック
- モード選択UIと実際の出題内容が一致しているか
- スコア・ライフの増減条件が意図通りか
- モバイル表示でUIが重なっていないか
- 文字コードがUTF-8で保存されているか（GitHub Pages対策）
