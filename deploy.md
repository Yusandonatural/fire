# FIREへの道 — 公開手順

`index.html` は単体で完結しています。サーバー処理はなく、計算はすべて閲覧者のブラウザの中で動きます。
入力データは localStorage に保存され、外部には送信されません（URLのハッシュで共有することは可能）。

## Cloudflare Pages で公開する（おすすめ・無料）

1. GitHub にリポジトリを作り、このフォルダの中身（`index.html` と `_headers`）を push する。
2. Cloudflare ダッシュボード → Workers & Pages → Create → Pages → Connect to Git。
   - Build command: なし（空欄）
   - Build output directory: `/`
3. Deploy 後、Custom domains から `fire.yusando.com` を追加。
   yusando.com のDNSがすでに Cloudflare にあるなら CNAME は自動で設定されます。

## GitHub Pages で公開する場合

1. リポジトリの Settings → Pages → Source を `main` / `root` に。
2. `fire.yusando.com` を使うなら、リポジトリ直下に `CNAME` ファイル（中身は `fire.yusando.com`）を置き、
   DNS に `fire` の CNAME → `<ユーザー名>.github.io` を追加。

## 更新のしかた

`index.html` を差し替えて push するだけです。ビルド工程はありません。

## 未対応のもの（必要になったら）

- `ogp.png`（1200×630）を同じフォルダに置くと、SNSでリンクを貼ったときの画像になります。
- アクセス解析を入れるなら、Cloudflare Web Analytics のスニペットを `</body>` の直前に追加。
- 複数端末での記録の同期は、この構成では行いません（ブラウザごとの保存です）。
  必要になったら Cloudflare Workers + D1 でログインと保存を足す形になります。

## 外部から読み込んでいるもの

- Google Fonts（Zen Maru Gothic / Nunito）
- cdnjs（html2canvas / jsPDF — PDF書き出しのときだけ使用）

どちらも閲覧者のブラウザが直接取得します。完全に自己完結させたい場合は、
フォントと2つのライブラリをローカルに置いて参照を書き換えてください。
