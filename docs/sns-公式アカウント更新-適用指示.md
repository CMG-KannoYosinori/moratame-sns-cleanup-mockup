# 公式SNS更新 適用指示

モック（このリポジトリ）の見た目を本番テンプレートへ反映するための指示です。チケット番号は `3028`。追加クラスの接頭辞は `mtd-3028-` です。

## 対象

| 画面 | 本番の目安 | モック |
| --- | --- | --- |
| PCトップ フッター「モラタメ公式アカウント」 | トップのフッター | `index.html` |
| PC「モラタメとは」フッター、同ページの「モラタメ公式SNS」 | `/contents/about.html` | `contents/about.html` |
| スマホトップ ドロワー「モラタメ公式ソーシャルメディア」 | `/s/` のドロワー | `s/index.html` |
| スマホ「モラタメとは」ドロワー、同ページの「モラタメ公式SNS」 | `/s/contents/about.html` | `s/contents/about.html` |
| 共通CSS | `/css/style--common-sp-and-pc-2.css` | `css/style--common-sp-and-pc-2.css` |

フッターとドロワーが共通インクルードなら、その1箇所を直せば足りる。ページごとにHTMLが複製されている場合は、上の4テンプレートすべてを直す。

## 対象外

次は今回変えない。

- スマホトップ本文中の「モラタメ公式SNS」カード（`s/index.html` 内の `p9255-p-sns`）。Facebook のカードが残っているのは未対応であり、削除しない。
- Facebook のメタタグ、SDK、ドメイン確認。
- LINE のアイコン、リンク、文言。
- 広告枠。

## 画像

モックの `images/common/` にある次の2ファイルを、本番の共通画像ディレクトリへ置く。参照パスは各テンプレートの階層に合わせる。

| ファイル | 用途 | サイズ |
| --- | --- | --- |
| `logo-x.svg` | X の白いロゴ | 430バイト |
| `Instagram_Glyph_Gradient.svg` | Instagram 公式グリフ | 約10MB |

`Instagram_Glyph_Gradient.svg` は公式データのまま約10MBある。本番へ置く前に、見た目を変えずに軽くできるか確認する。色や形の変更、余白のトリミングはしない。

X のロゴは引き伸ばさない。黒地のタイルの中に、タイル幅の64%で置く。これが周囲の余白になる。

## 共通CSS

`/css/style--common-sp-and-pc-2.css` の、次のコメントの間に書く。コメントが無ければ、このブロックごと追加する。

```css
/* SNS 公式アカウント 更新 20261117 */
.mtd-3028-x-logo {
  align-items: center;
  background-color: #000;
  box-sizing: border-box;
  display: inline-flex;
  justify-content: center;
  line-height: 0;
}

.mtd-3028-x-logo__mark {
  display: block;
  flex: 0 0 auto;
  height: auto;
  max-width: 64%;
  min-width: 0;
  width: 64%;
}

.mtd-3028-x-logo--account {
  height: 32px;
  width: 32px;
}

.mtd-3028-x-logo--drawer {
  height: 44px;
  margin-top: 10px;
  width: 44px;
}

.mtd-3028-x-logo--card {
  display: flex;
  height: 102px;
  margin-left: auto;
  margin-right: auto;
  width: 102px;
}

.mtd-3028-x-logo--card .mtd-3028-x-logo__mark {
  height: auto;
  max-width: 64%;
  width: 64%;
}

.mtd-3028-sns-card__label {
  color: #000;
}

.p9255-p-sns .p9255-p-sns__card.p9255-p-sns__card--twitter .mtd-3028-sns-card__label.p9225-c-button__text::before {
  background-color: #000;
}

.mtd-3028-sns-drawer {
  display: flex;
}

.mtd-3028-sns-drawer > li.type3 {
  border-bottom: 0;
  border-right: 0;
  float: none;
  width: calc(100% / 3);
}

.mtd-3028-sns-drawer > li.type3 + li.type3 {
  border-left: 1px solid #c9cab7;
}
/* /SNS 公式アカウント 更新 20261117 */
```

再生アイコンの青（`#1d9bf0`）は `css/contents/p9255-about.css` にある。このCSSは共通CSSより後に読まれる。上の `::before` 指定は、その指定より詳細度を高くして黒にしている。共通CSSへ移すときは、詳細度を落とさない。

再生アイコンの三角（`::after`）は白のままにする。丸だけ黒にする。

## 1. PCフッター「モラタメ公式アカウント」

PCトップとPC「モラタメとは」の両方。

やること:

- Facebook のアイコンと「掲載情報はもちろんfacebookだけのキャンペーンも配信」を削除する。
- Twitter の鳥アイコンを X ロゴに差し替える。リンク先 `https://twitter.com/moratame/` はそのまま。
- 文言を「おすすめ商品の情報や「ツイ部」の開催情報をお届け！」にする。
- Instagram を、空いた右列へ上げる。画像を公式グリフにし、文言を「「フォト部」の開催情報をリアルタイムでお届け！」にする。リンク先 `https://instagram.com/moratame_net/` はそのまま。
- LINE を左列へ上げる。アイコン、リンク、文言は変えない。

並び:

1. 左が X、右が Instagram
2. 左が LINE

X の置き換え後:

```html
<span class="mtd-3028-x-logo mtd-3028-x-logo--account">
  <img class="mtd-3028-x-logo__mark" src="（共通画像）/logo-x.svg" alt="X">
</span>
```

Instagram は既存の `icon-insta` のまま、`src` だけ公式グリフにする。表示サイズは既存CSSの 32px。

## 2. スマホ ドロワー「モラタメ公式ソーシャルメディア」

スマホトップとスマホ「モラタメとは」の両方。

やること:

- Facebook のマスを削除する。
- 鳥アイコンを X ロゴにする。リンク先 `https://twitter.com/moratame/` はそのまま。
- Instagram の画像を公式グリフにする。リンク先 `https://instagram.com/moratame_net/` はそのまま。
- LINE はそのまま。リンク先は `https://line.me/ti/p/%40moratame`。
- `ul` に `mtd-3028-sns-drawer` を足し、3つを1行にする。既存の `type3` は幅50%なので、このクラスが無いと2列のままになる。

```html
<ul class="drwMnCtg bdrs5 mtd-3028-sns-drawer" data-role="none">
  <li class="type3 drwMnCtgBdrb bxz-bb">
    <a href="https://twitter.com/moratame/" rel="external" target="_blank" class="ui-link"><span class="mtd-3028-x-logo mtd-3028-x-logo--drawer"><img class="mtd-3028-x-logo__mark" src="（共通画像）/logo-x.svg" alt="X"></span></a>
  </li>
  <li class="type3 drwMnCtgBdb bxz-bb">
    <a href="https://instagram.com/moratame_net/" rel="external" target="_blank" class="ui-link"><img class="icon-sns mt_10" src="（共通画像）/Instagram_Glyph_Gradient.svg" alt="instagram"></a>
  </li>
  <li class="type3 bxz-bb line">
    <a href="https://line.me/ti/p/%40moratame" rel="external" target="_blank" class="ui-link"><img class="icon-sns mt_10" src="（既存のLINE画像）" alt="line"></a>
  </li>
</ul>
```

X と Instagram、LINE は各 44px。マスの高さ 65px は既存のまま。

## 3. 「モラタメとは」の「モラタメ公式SNS」カード

PCとスマホの「モラタメとは」だけ。スマホトップ本文の同名カードは対象外。

やること:

- Facebook のカード（アイコンと「公式Facebookはこちら」）を削除する。
- Twitter カードの画像を X ロゴにする。文言を「公式Xはこちら」にし、文字色と再生アイコンの丸を黒にする。リンク先 `https://twitter.com/moratame/` はそのまま。
- Instagram の画像を公式グリフにする。文言「公式Instagramはこちら」とリンク先 `https://www.instagram.com/moratame_net/` はそのまま。
- LINE カードはそのまま。

X カード:

```html
<div class="p9255-p-sns__card p9255-p-sns__card--twitter">
  <a link="" href="https://twitter.com/moratame/" target="_blank">
    <span class="mtd-3028-x-logo mtd-3028-x-logo--card">
      <img class="mtd-3028-x-logo__mark" src="（共通画像）/logo-x.svg" alt="X">
    </span>
    <p class="p9225-c-button__text mtd-3028-sns-card__label">公式Xはこちら</p>
  </a>
</div>
```

スマホ側の `a` には、既存どおり `data-role="none"` を残す。`p9255-p-sns__card--twitter` は残す。再生アイコンの形はこのクラスに依存している。

カードは横並びのまま、X、Instagram、LINE の3枚になる。

## 確認

- PCトップとPC「モラタメとは」のフッターに Facebook が無く、1段目が X と Instagram、2段目が LINE である。
- X は黒地に白いロゴで、ロゴが伸びていない。フッターは 32px、ドロワーは 44px、カードは 102px。
- Instagram は公式のグラデーションのグリフである。
- スマホの両ドロワーが3列1行である。他のドロワー項目の幅は50%のままである。
- 「モラタメとは」のSNSカードで、「公式Xはこちら」と再生アイコンの丸が黒、三角は白である。
- スマホトップ本文のSNSカードは、従来どおり Facebook が残っている。
- 各リンク先が、この指示に書いたURLから変わっていない。
