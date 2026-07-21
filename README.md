# costia-lp

建築板金業向け 現場・原価管理システム **Costia** のランディングページ。

静的な `index.html` 1枚のみ。ビルド不要で、GitHub Pages からそのまま配信します。

## 構成

- `index.html` — LP本体(CSSはインライン)
- `assets/` — ロゴ画像
- `.nojekyll` — GitHub Pages の Jekyll 処理を無効化

## ローカルで確認する

ブラウザで `index.html` を開くだけです。

## 公開

GitHub の Settings → Pages で、Source を `main` ブランチのルートに設定します。

## リンク先

アプリ本体は Vercel 上の https://costia-next.vercel.app で稼働しています。
LP からのリンク(サインアップ・料金・規約類)はすべてそちらを指しています。

## 検索避けについて

`index.html` に `<meta name="robots" content="noindex, nofollow">` を入れています。
URL を知っている人だけに見せる運用のためで、アプリ側 (costia-next) の
`robots.txt` が `Disallow: /` であることに合わせています。

一般公開に踏み切るときは、この meta を消し、アプリ側の `robots.txt` も
併せて見直してください。片方だけ変えると意図と食い違います。

なお `robots.txt` での `Disallow` は併用しないでください。クロール自体を止めると
クローラーが noindex を読めず、かえって検索結果に URL が残ることがあります。

## 表記の更新について

料金・事業者情報・利用上限などは、アプリ側の `src/lib/legal.ts` が正です。
値を変更したときは、このLPの記載も合わせて更新してください。
