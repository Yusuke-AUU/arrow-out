# ARROW OUT - 矢印ぬけパズル

矢印をタップすると、その向きに線がスルスル抜ける。先がふさがっているとぶつかってライフ−1。全部抜いたらクリア。

- HTML/CSS/JS のみ（ビルド不要・外部ライブラリなし）
- 盤面はレベルごとに自動生成（シード固定・必ず解ける）
- スマホ優先（タッチ操作、devicePixelRatio 対応、セーフエリア対応）
- PWA対応（ホーム画面に追加・オフラインで遊べる）
- 到達レベルは localStorage に保存

## ファイル構成

| ファイル | 役割 |
|---|---|
| index.html | ゲーム本体（全コードここ） |
| manifest.webmanifest | PWA設定 |
| sw.js | オフライン用 Service Worker |
| icon.svg / icon-*.png | アイコン |
| netlify.toml | Netlify設定（ビルドなし・キャッシュ設定） |

## デプロイ手順（GitHub → Netlify）

1. GitHubで新規リポジトリ `arrow-out` を作成
2. このフォルダの中身をすべてアップロード（またはコマンド）
   ```bash
   git init
   git add .
   git commit -m "ARROW OUT v1"
   git branch -M main
   git remote add origin https://github.com/<ユーザー名>/arrow-out.git
   git push -u origin main
   ```
3. Netlify → Add new site → Import an existing project → GitHub → `arrow-out` を選択
4. Build command は空欄、Publish directory は `.`（netlify.toml で設定済み）→ Deploy
5. 以後は `git push` するたびに自動デプロイ

## 更新するとき

- `sw.js` の `VERSION`（例: `arrow-out-v1` → `v2`）を上げてから push すると、遊んでいる人の端末のキャッシュも確実に入れ替わる

## 調整ポイント（index.html 内）

| 変えたいこと | 場所 |
|---|---|
| 盤面サイズの伸び方 | `generate()` の `cols` / `rows` |
| 線の長さ | `generate()` の `maxLen` / `minLen` |
| 色 | 先頭の `COLORS` |
| ライフ・ヒント回数 | `startLevel()` の `lives=3;hints=3` |
| 抜ける速さ | `frame()` の `sn.v` の加速・上限 |
