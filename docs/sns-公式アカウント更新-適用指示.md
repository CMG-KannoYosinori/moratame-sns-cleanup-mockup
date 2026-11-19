# 公式SNS更新 適用指示

モック（このリポジトリ）の見た目を本番テンプレートへ反映するための指示です。

## 確認用URL

GitHub Pages。

| 画面                   | URL                                                                                     |
| ---------------------- | --------------------------------------------------------------------------------------- |
| PCトップ               | https://cmg-kannoyosinori.github.io/moratame-sns-cleanup-mockup/                        |
| PC「モラタメとは」     | https://cmg-kannoyosinori.github.io/moratame-sns-cleanup-mockup/contents/about.html     |
| スマホトップ           | https://cmg-kannoyosinori.github.io/moratame-sns-cleanup-mockup/s/                      |
| スマホ「モラタメとは」 | https://cmg-kannoyosinori.github.io/moratame-sns-cleanup-mockup/s/contents/about.html   |

## 対象

| 画面                                                          | 本番の目安                           | モック                              |
| ------------------------------------------------------------- | ------------------------------------ | ----------------------------------- |
| PCトップ フッター「モラタメ公式アカウント」                   | トップのフッター                     | `index.html`                        |
| PC「モラタメとは」フッター、同ページの「モラタメ公式SNS」     | `/contents/about.html`               | `contents/about.html`               |
| スマホトップ ドロワー「モラタメ公式ソーシャルメディア」       | `/s/` のドロワー                     | `s/index.html`                      |
| スマホトップ 本文「モラタメ.net公式ソーシャルページ」         | `/s/` の本文                         | `s/index.html`                      |
| スマホトップ 本文「モラタメ公式SNS」                          | `/s/` の本文                         | `s/index.html`                      |
| スマホ「モラタメとは」ドロワー、同ページの「モラタメ公式SNS」 | `/s/contents/about.html`             | `s/contents/about.html`             |
| 共通CSS                                                       | `/css/style--common-sp-and-pc-2.css` | `css/style--common-sp-and-pc-2.css` |

## 要確認

公式アカウントとしての Facebook の表示は削除する。次は導線とは別の認証と読み込みなので、残すか外すかを確認する。

- ドメイン確認のメタタグ。4ページとも `<meta name="facebook-domain-verification" content="c0cie9dkuu426dpjng4owr5k68k8l3">`。
- Facebook SDK。PCトップとPC「モラタメとは」の `https://connect.facebook.net/ja_JP/sdk.js`（要素ID `facebook-jssdk`）。スマホの2ページには無い。

## 画像

モックの `images/common/` にある次の2ファイルを、本番の共通画像ディレクトリへ置く。参照パスは各テンプレートの階層に合わせる。

| ファイル                       | 用途                 | サイズ    |
| ------------------------------ | -------------------- | --------- |
| `logo-x.svg`                   | X の白いロゴ         | 430バイト |
| `logo-instagram.webp`          | Instagram 公式グリフ | 21KB      |

## 共通CSS

モックの `css/style--common-sp-and-pc-2.css` 102–213行目を、本番の `/css/style--common-sp-and-pc-2.css` の末尾に追加する。範囲は `/* SNS 公式アカウント 更新 20261117 */` から `/* /SNS 公式アカウント 更新 20261117 */` まで。

## 1. PCフッター「モラタメ公式アカウント」

PCトップとPC「モラタメとは」の両方。

やること:

- Facebook のアイコンと「掲載情報はもちろんfacebookだけのキャンペーンも配信」を削除する。
- Twitter の鳥アイコンを X ロゴに差し替える。
- 文言を「おすすめ商品の情報や「ツイ部」の開催情報をお届け！」にする。
- Instagram を、空いた右列へ上げる。画像を公式グリフにし、文言を「「フォト部」の開催情報をリアルタイムでお届け！」にする。
- LINE を左列へ上げる。

並び:

1. 左が X、右が Instagram
2. 左が LINE

X の置き換え後:

```html
<span class="mtd-3028-x-logo mtd-3028-x-logo--account">
  <img class="mtd-3028-x-logo__mark" src="（共通画像）/logo-x.svg" alt="X" />
</span>
```

Instagram の `src` を公式グリフにする。

## 2. スマホ ドロワー「モラタメ公式ソーシャルメディア」

スマホトップとスマホ「モラタメとは」の両方。

やること:

- Facebook のマスを削除する。
- 鳥アイコンを X ロゴにする。
- Instagram の画像を公式グリフにする。
- `ul` に `mtd-3028-sns-drawer` を足し、3つを1行にする。

```html
<ul class="drwMnCtg bdrs5 mtd-3028-sns-drawer" data-role="none">
  <li class="type3 drwMnCtgBdrb bxz-bb">
    <a
      href="https://twitter.com/moratame/"
      rel="external"
      target="_blank"
      class="ui-link"
      ><span class="mtd-3028-x-logo mtd-3028-x-logo--drawer"
        ><img
          class="mtd-3028-x-logo__mark"
          src="（共通画像）/logo-x.svg"
          alt="X" /></span
    ></a>
  </li>
  <li class="type3 drwMnCtgBdb bxz-bb">
    <a
      href="https://instagram.com/moratame_net/"
      rel="external"
      target="_blank"
      class="ui-link"
      ><img
        class="icon-sns mt_10"
        src="（共通画像）/logo-instagram.webp"
        alt="instagram"
    /></a>
  </li>
  <li class="type3 bxz-bb line">
    <a
      href="https://line.me/ti/p/%40moratame"
      rel="external"
      target="_blank"
      class="ui-link"
      ><img class="icon-sns mt_10" src="（既存のLINE画像）" alt="line"
    /></a>
  </li>
</ul>
```

## 3. 「モラタメ公式SNS」カード

PC「モラタメとは」、スマホ「モラタメとは」、スマホトップ本文。3箇所とも同じ内容にする。

やること:

- Facebook のカード（アイコンと「公式Facebookはこちら」）を削除する。
- Twitter カードの画像を X ロゴにする。文言を「公式Xはこちら」にし、文字色と再生アイコンの丸を黒にする。
- Instagram の画像を公式グリフにする。
- 「公式LINEはこちら」の文字と再生アイコンの丸を黒にする。

X カード:

```html
<div class="p9255-p-sns__card p9255-p-sns__card--twitter">
  <a link="" href="https://twitter.com/moratame/" target="_blank">
    <span class="mtd-3028-x-logo mtd-3028-x-logo--card">
      <img
        class="mtd-3028-x-logo__mark"
        src="（共通画像）/logo-x.svg"
        alt="X"
      />
    </span>
    <p class="p9225-c-button__text mtd-3028-sns-card__label">公式Xはこちら</p>
  </a>
</div>
```

`p9255-p-sns__card--twitter` は残す。再生アイコンの形はこのクラスに依存している。

カードは X、Instagram、LINE の3枚になる。

スマホトップ本文のカードは、モックの `s/index.html` ではまだ旧来の4枚のままである。本番ではこの節のとおり直し、モックに残っている Facebook には合わせない。

## 4. スマホトップ本文「モラタメ.net公式ソーシャルページ」

`s/index.html` の `snsList`。背景画像の4列を、X・Instagram・LINE の3列にする。

やること:

- Facebook（`icon_fb`、`https://m.facebook.com/moratame.net?...`）を削除する。
- 鳥アイコン（`icon_tw`）を X ロゴにする。
- Instagram（`icon_insta`）を公式グリフの `img` にする。
- `ul` に `mtd-3028-sns-list` を足す。

```html
<ul class="snsList mtd-3028-sns-list" data-role="none">
  <li class="fl-l">
    <a href="https://mobile.twitter.com/moratame/" rel="external" target="_blank">
      <span class="mtd-3028-x-logo mtd-3028-x-logo--sns">
        <img class="mtd-3028-x-logo__mark" src="（共通画像）/logo-x.svg" alt="X">
      </span>
    </a>
  </li>
  <li class="fl-l">
    <a href="https://instagram.com/moratame_net/" rel="external" target="_blank">
      <img class="mtd-3028-sns-glyph" src="（共通画像）/logo-instagram.webp" alt="Instagram">
    </a>
  </li>
  <li class="fl-l">
    <a href="https://line.me/ti/p/%40tug0345w" rel="external" target="_blank">
      <div class="icon-line"></div>
    </a>
  </li>
</ul>
```

## 確認

- PCトップとPC「モラタメとは」のフッターに Facebook が無く、1段目が X と Instagram、2段目が LINE である。
- X は黒地に白いロゴで、ロゴが伸びていない。フッターは 32px、ドロワーは 44px、カードは 102px。
- Instagram は公式のグラデーションのグリフである。
- スマホの両ドロワーが3列1行である。他のドロワー項目の幅は50%のままである。
- 「モラタメ公式SNS」カードは、PC「モラタメとは」、スマホ「モラタメとは」、スマホトップ本文の3箇所とも、X・Instagram・LINE の3枚である。「公式Xはこちら」と「公式LINEはこちら」の文字と再生アイコンの丸が黒、三角は白である。
- スマホトップ本文の「モラタメ.net公式ソーシャルページ」が、X・Instagram・LINE の1行である。
