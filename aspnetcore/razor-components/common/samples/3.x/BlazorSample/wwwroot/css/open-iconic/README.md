---
ms.openlocfilehash: 3965884c8e0d7116f5d8a42e6aefb0dc5be94f1e
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57029659"
---
<a name="open-iconic-v111httpuseiconiccomopen"></a>[Open Iconic v1.1.1](http://useiconic.com/open)
===========

### <a name="open-iconic-is-the-open-source-sibling-of-iconichttpuseiconiccom-it-is-a-hyper-legible-collection-of-223-icons-with-a-tiny-footprintmdashready-to-use-with-bootstrap-and-foundation-view-the-collectionhttpuseiconiccomopenicons"></a>Open Iconic は、[Iconic](http://useiconic.com) のオープン ソース版です。 これは、メモリ占有領域の小さい、とても見やすい 223 個のアイコンのコレクションです&mdash;Bootstrap と Foundation ですぐに使えます。 [コレクションを確認する](http://useiconic.com/open#icons)



## <a name="whats-in-open-iconic"></a>Open Iconic とは

* 8 ピクセルまで下げても見やすいように設計された 223 個のアイコン
* 超軽量の SVG ファイル (セット全体で 61.8) 
* SVG スプライト&mdash;アイコン フォントに代わる最新の機能
* Web フォント (EOT、OTF、SVG、TTF、WOFF)、PNG、および WebP 形式
* CSS、LESS、SCSS、および Stylus 形式の Web フォント スタイル シート (Bootstrap と Foundation 用のバージョンを含む)
* 8px、16px、24px、32px、48px、64px の PNG および WebP ラスター イメージ。


## <a name="getting-started"></a>作業の開始

#### <a name="for-code-samples-and-everything-else-you-need-to-get-started-with-open-iconic-check-out-our-iconshttpuseiconiccomopenicons-and-referencehttpuseiconiccomopenreference-sections"></a>コード サンプルや、Open Iconic の使用開始に必要なその他すべてのことについては、[アイコン](http://useiconic.com/open#icons)と[参照](http://useiconic.com/open#reference)に関するセクションをご覧ください。

### <a name="general-usage"></a>一般的な使用法

#### <a name="using-open-iconics-svgs"></a>Open Iconic の SVG の使用

Web 上でアイコンを表示するための最適な方法として、SVG をお勧めします。 Open Iconic は基本的な SVG に過ぎないため、その他の画像と同じようにこれを表示することをお勧めします (`alt` 属性を忘れないようにします)。

```
<img src="/open-iconic/svg/icon-name.svg" alt="icon name">
```

#### <a name="using-open-iconics-svg-sprite"></a>Open Iconic の SVG スプライトの使用

SVG スプライトとして Open Iconic を使うこともできます。これを使うと、セット内のすべてのアイコンを 1 つの要求で表示できます。 これは、複雑さをなくしたアイコン フォントのようなものです。

SVG スプライトからアイコンを追加する方法は、使い慣れた方法とは少し異なりますが、やはりとても簡単です。 "*ヒント:アイコンのスタイルを設定しやすくするために、*" `<svg>` "*タグに汎用クラスを追加し、*" `<use>` "*タグに異なるアイコンごとに一意のクラス名を追加することをお勧めします。*"  

```
<svg class="icon">
  <use xlink:href="open-iconic.svg#account-login" class="icon-account-login"></use>
</svg>
```

アイコンをサイズ変更するために必要なのは、基本的な CSS のみです。 アイコンの形式はすべて正方形であるため、単純に同じ幅と高さで `<svg>` タグを設定します。

```
.icon {
  width: 16px;
  height: 16px;
}
```

アイコンの色分けはさらに簡単です。 必要な操作は、`<use>` タグの `fill` ルールを設定することだけです。

```
.icon-account-login {
  fill: #f00;
}
```

SVG スプライトについて詳しくは、[Chris Coyier によるガイド](http://css-tricks.com/svg-sprites-use-better-icon-fonts/)をご覧ください。

#### <a name="using-open-iconics-icon-font"></a>Open Iconic のアイコン フォントの使用...


##### <a name="with-bootstrap"></a>…Bootstrap と共に

Bootstrap のスタイル シートは、`font/css/open-iconic-bootstrap.{css, less, scss, styl}` で確認できます。


```
<link href="/open-iconic/font/css/open-iconic-bootstrap.css" rel="stylesheet">
```


```
<span class="oi oi-icon-name" title="icon name" aria-hidden="true"></span>
```

##### <a name="with-foundation"></a>…Foundation と共に

Foundation のスタイル シートは、`font/css/open-iconic-foundation.{css, less, scss, styl}` で確認できます。

```
<link href="/open-iconic/font/css/open-iconic-foundation.css" rel="stylesheet">
```


```
<span class="fi-icon-name" title="icon name" aria-hidden="true"></span>
```

##### <a name="on-its-own"></a>…そのままで

既定のスタイル シートは、`font/css/open-iconic.{css, less, scss, styl}` で確認できます。

```
<link href="/open-iconic/font/css/open-iconic.css" rel="stylesheet">
```

```
<span class="oi" data-glyph="icon-name" title="icon name" aria-hidden="true"></span>
```


## <a name="license"></a>ライセンス

### <a name="icons"></a>アイコン

すべてのコード (SVG マークアップを含む) は [MIT ライセンス](http://opensource.org/licenses/MIT)に従います。

### <a name="fonts"></a>フォント

すべてのフォントは [SIL ライセンス](http://scripts.sil.org/cms/scripts/page.php?item_id=OFL_web)に従います。
