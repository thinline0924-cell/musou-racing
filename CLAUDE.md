# CLAUDE.md — このリポジトリで作業するときのルール

3Dレースゲーム「霧走 MUSOU ― Prototype Racing」。ブラウザで開くだけで動く静的サイト。
持ち主はプログラミング初心者。**説明は日本語で、専門用語には短い説明を付ける。**

## 持ち主の環境
- パソコンに Node.js は入っていない。ローカル実行や `npm install` を前提にしない
- 公開は Render の静的サイト(`render.yaml`)。`index.html` をダブルクリックしても遊べること(file:// で動くこと)を保つ

## 約束
1. **ビルドツールを入れない。** 素の HTML / CSS / JavaScript。React・bundler・TypeScript・ES modules(`import`)は使わない(file:// で動かなくなる)
2. 画像・音声ファイルは使わない。模様は `js/textures.js`、音は `js/audio.js` がその場で作る
3. 3D は `js/lib/three.min.js`(three.js r149 の UMD 版、MIT)を同梱して使う。`import` 形式の版に替えないこと
4. 配色は霧の白・淡い青+赤(参考画像の雰囲気)。タイトル画面は参考画像に似せすぎない
5. 乱数を使うのは見た目(木の位置など)と AI のばらつきだけ。コースの形は `data.js` の数値から毎回同じに作られる
6. 変更したら:4コースすべてでレースを最後まで走りきれるか確かめる(ブラウザで `window.__musou.autopilot()` を呼ぶと自分の車が自動運転になる。`window.__musouFast = 8` で早送り、`window.__musouNoRender = true` で描画を止めて高速化)
7. 車の挙動(physics.js)を変えたら、ステアリング補助オンのキーボード操作で全車・全コースがスピンせず走れるかを確かめる

## ファイル
| ファイル | 役割 |
|---|---|
| `index.html` | 画面の骨組み |
| `css/race.css` | 見た目 |
| `js/data.js` | マシンとコースの数値 |
| `js/track.js` | コースの形・縁石・壁・走行ライン・目標速度 |
| `js/physics.js` | 車の動き(タイヤ・空力・エンジン・ギア・運転補助) |
| `js/ai.js` | ライバル車の運転 |
| `js/carmodel.js` | 車の3Dモデル |
| `js/world.js` | コースの3D世界 |
| `js/textures.js` | 模様をキャンバスに描く |
| `js/audio.js` | エンジン音・効果音・音楽の合成 |
| `js/hud.js` | メーター4種・テレメトリー・ミニマップ |
| `js/main.js` | 全体の進行 |
