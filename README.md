# costia-lp

建設業向け 現場・原価管理システム **Costia** のランディングページ。

静的な `index.html` 1枚のみ。ビルド不要で、GitHub Pages からそのまま配信します。

## 構成

- `index.html` — LP本体(CSSはインライン)
- `assets/` — ロゴと画面キャプチャ
- `.nojekyll` — GitHub Pages の Jekyll 処理を無効化

### 画面キャプチャについて

`assets/screen-*.png` はデモ会社(サンプルデータ)の画面です。実在の会社・取引先・
金額は含みません。撮り直すときは costia-next 側の `docs/demo/` に元があります
(`scripts/seed-demo*.ts` でデモデータを作り、`docs/demo/in-person-demo.md` の
手順で撮影しています)。

差し替えるときの注意:

- **ライトモードで撮る**。ダーク表示でも浮かないよう白い枠で包む作りにしてある
- **ヘッダーのメールアドレスを消す**。ログイン中のアドレスがそのまま写る
- `index.html` の `width` / `height` 属性を実寸に合わせる。ずれると読み込み時に
  レイアウトががたつく

### 追加予定のキャプチャ(未撮影)

`index.html` にはコメントアウトした `<div class="shot">` を置いてある。撮影して
`assets/` に置いたら、コメント(`<!-- TODO(screenshot): ... -->`)を外すだけで出る。
`width` / `height` は実寸に合わせて直すこと。

| ファイル名 | 置く場所 | 写すもの | 注意 |
|---|---|---|---|
| `assets/screen-project-link.png` | オプション節(案件連携) | **Costia の工事詳細で「写真・書類」を開いた画面**と、**Drive の案件フォルダに 写真/ 書類/ 連絡メモ/ が並んだ画面**を横に並べる(片方だけなら Drive 側を採る。差別化は「実体が御社の Drive に入る」ことなので) | **Telegram は写さない**(2026-09-11。Costia の画面から送る方式に一本化したため、旧方式の画面は載せない)。**Drive 側もデモ会社のフォルダを撮る** — 実運用のフォルダには施主のお名前を含む案件名が並ぶ |
| `assets/screen-accounting.png` | オプション節(会計連携)。**外部提供を始めるまで載せない**(いまは準備中表記のみ) | 会計連携画面か、出力した Excel のサマリーシート | デモ会社のデータで。実在の仕入先名・金額を写さない |

デモデータの作り方・撮影手順は costia-next 側の `docs/demo/in-person-demo.md` を参照。

## ローカルで確認する

ブラウザで `index.html` を開くだけです。

## 公開

GitHub の Settings → Pages で、Source を `main` ブランチのルートに設定します。

現在の公開URL: https://kousakabankinkk-hub.github.io/costia-lp/

**このURLにはGitHubアカウント名(社名)が含まれます。** 一般公開に踏み切ったので、
下記のカスタムドメインへの移行を推奨します。

## カスタムドメインへの移行(未実施)

`teamcostia.com` は現在メール専用(MX が Google Workspace)で、Web のレコード
(A / CNAME)は1つもありません。そのため下記を追加してもメールには影響しません。

**順番を守ること。** `CNAME` ファイルを先に置くと、GitHub Pages が github.io の
URL をカスタムドメインへリダイレクトし始めるため、DNS が引けるようになるまで
LP が見られなくなります。XServer の DNS 反映には1時間ほどかかります。

1. XServer のDNSレコード設定で、`teamcostia.com` に次を追加する

   | 種別 | ホスト名 | 値 |
   |---|---|---|
   | A | (空欄=apex) | 185.199.108.153 |
   | A | (空欄=apex) | 185.199.109.153 |
   | A | (空欄=apex) | 185.199.110.153 |
   | A | (空欄=apex) | 185.199.111.153 |
   | CNAME | www | kousakabankinkk-hub.github.io. |

   MX レコードは触らないこと(メールが止まります)。

2. 反映を確認する。4つのIPが返れば完了

   ```
   nslookup -type=A teamcostia.com 8.8.8.8
   ```

3. このリポジトリのルートに `CNAME` ファイルを作り、1行だけ書いて push する

   ```
   teamcostia.com
   ```

4. GitHub の Settings → Pages で **Enforce HTTPS** を有効にする
   (証明書の発行に数分かかるため、すぐ有効化できないときは少し待つ)

5. 移行後、この README の公開URLと、名刺・チラシの記載を更新する

なお、アプリ本体(costia-next)のリンク先は Vercel のままで問題ありません。
LP とアプリでドメインを揃えたい場合は別途検討します。

## リンク先

アプリ本体は Vercel 上の https://costia-next.vercel.app で稼働しています。
LP からのリンク(サインアップ・料金・規約類)はすべてそちらを指しています。

## 検索避けについて(現在 noindex・一時的)

一度解除しましたが、**2026年8月に再び noindex を入れています**。理由は、LP から
リンクしている利用規約・プライバシーポリシーが弁護士のレビュー中(同月完了予定)で、
確定前の文面を検索結果に載せないためです。一度載ると、後から直しても古い版が
しばらく残り続けます。

noindex はクロールを止めるものではないので、**URLを知っている人は今までどおり
閲覧できます**。紹介や対面デモでURLを渡す運用には支障ありません。LINE などで
共有したときのプレビュー(OG画像)も従来どおり出ます。

**レビュー完了後に外すもの(2箇所。片方だけだと食い違います)**

1. このリポジトリの `index.html` の `<meta name="robots" content="noindex, nofollow">`
2. アプリ側 costia-next の `src/app/layout.tsx` の `robots: { index: false, follow: false }`

`robots.txt` での `Disallow` は併用しないでください。クロール自体を止めると
クローラーが noindex を読めず、かえって検索結果に URL が残ることがあります。

## 表記の更新について

料金・事業者情報・利用上限などは、アプリ側の `src/lib/legal.ts` が正です。
値を変更したときは、このLPの記載も合わせて更新してください。
