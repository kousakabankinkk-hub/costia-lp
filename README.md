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

## 表記の更新について

料金・事業者情報・利用上限などは、アプリ側の `src/lib/legal.ts` が正です。
値を変更したときは、このLPの記載も合わせて更新してください。
