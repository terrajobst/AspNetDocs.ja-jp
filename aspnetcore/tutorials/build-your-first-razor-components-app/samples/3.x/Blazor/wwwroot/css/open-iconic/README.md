---
ms.openlocfilehash: 3965884c8e0d7116f5d8a42e6aefb0dc5be94f1e
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57054219"
---
<a name="open-iconic-v111httpuseiconiccomopen"></a>[<span data-ttu-id="4c134-101">Open Iconic v1.1.1</span><span class="sxs-lookup"><span data-stu-id="4c134-101">Open Iconic v1.1.1</span></span>](http://useiconic.com/open)
===========

### <a name="open-iconic-is-the-open-source-sibling-of-iconichttpuseiconiccom-it-is-a-hyper-legible-collection-of-223-icons-with-a-tiny-footprintmdashready-to-use-with-bootstrap-and-foundation-view-the-collectionhttpuseiconiccomopenicons"></a><span data-ttu-id="4c134-102">Open Iconic は、[Iconic](http://useiconic.com) のオープン ソース版です。</span><span class="sxs-lookup"><span data-stu-id="4c134-102">Open Iconic is the open source sibling of [Iconic](http://useiconic.com).</span></span> <span data-ttu-id="4c134-103">これは、メモリ占有領域の小さい、とても見やすい 223 個のアイコンのコレクションです&mdash;Bootstrap と Foundation ですぐに使えます。</span><span class="sxs-lookup"><span data-stu-id="4c134-103">It is a hyper-legible collection of 223 icons with a tiny footprint&mdash;ready to use with Bootstrap and Foundation.</span></span> [<span data-ttu-id="4c134-104">コレクションを確認する</span><span class="sxs-lookup"><span data-stu-id="4c134-104">View the collection</span></span>](http://useiconic.com/open#icons)



## <a name="whats-in-open-iconic"></a><span data-ttu-id="4c134-105">Open Iconic とは</span><span class="sxs-lookup"><span data-stu-id="4c134-105">What's in Open Iconic?</span></span>

* <span data-ttu-id="4c134-106">8 ピクセルまで下げても見やすいように設計された 223 個のアイコン</span><span class="sxs-lookup"><span data-stu-id="4c134-106">223 icons designed to be legible down to 8 pixels</span></span>
* <span data-ttu-id="4c134-107">超軽量の SVG ファイル (セット全体で 61.8)</span><span class="sxs-lookup"><span data-stu-id="4c134-107">Super-light SVG files - 61.8 for the entire set</span></span> 
* <span data-ttu-id="4c134-108">SVG スプライト&mdash;アイコン フォントに代わる最新の機能</span><span class="sxs-lookup"><span data-stu-id="4c134-108">SVG sprite&mdash;the modern replacement for icon fonts</span></span>
* <span data-ttu-id="4c134-109">Web フォント (EOT、OTF、SVG、TTF、WOFF)、PNG、および WebP 形式</span><span class="sxs-lookup"><span data-stu-id="4c134-109">Webfont (EOT, OTF, SVG, TTF, WOFF), PNG and WebP formats</span></span>
* <span data-ttu-id="4c134-110">CSS、LESS、SCSS、および Stylus 形式の Web フォント スタイル シート (Bootstrap と Foundation 用のバージョンを含む)</span><span class="sxs-lookup"><span data-stu-id="4c134-110">Webfont stylesheets (including versions for Bootstrap and Foundation) in CSS, LESS, SCSS and Stylus formats</span></span>
* <span data-ttu-id="4c134-111">8px、16px、24px、32px、48px、64px の PNG および WebP ラスター イメージ。</span><span class="sxs-lookup"><span data-stu-id="4c134-111">PNG and WebP raster images in 8px, 16px, 24px, 32px, 48px and 64px.</span></span>


## <a name="getting-started"></a><span data-ttu-id="4c134-112">作業の開始</span><span class="sxs-lookup"><span data-stu-id="4c134-112">Getting Started</span></span>

#### <a name="for-code-samples-and-everything-else-you-need-to-get-started-with-open-iconic-check-out-our-iconshttpuseiconiccomopenicons-and-referencehttpuseiconiccomopenreference-sections"></a><span data-ttu-id="4c134-113">コード サンプルや、Open Iconic の使用開始に必要なその他すべてのことについては、[アイコン](http://useiconic.com/open#icons)と[参照](http://useiconic.com/open#reference)に関するセクションをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="4c134-113">For code samples and everything else you need to get started with Open Iconic, check out our [Icons](http://useiconic.com/open#icons) and [Reference](http://useiconic.com/open#reference) sections.</span></span>

### <a name="general-usage"></a><span data-ttu-id="4c134-114">一般的な使用法</span><span class="sxs-lookup"><span data-stu-id="4c134-114">General Usage</span></span>

#### <a name="using-open-iconics-svgs"></a><span data-ttu-id="4c134-115">Open Iconic の SVG の使用</span><span class="sxs-lookup"><span data-stu-id="4c134-115">Using Open Iconic's SVGs</span></span>

<span data-ttu-id="4c134-116">Web 上でアイコンを表示するための最適な方法として、SVG をお勧めします。</span><span class="sxs-lookup"><span data-stu-id="4c134-116">We like SVGs and we think they're the way to display icons on the web.</span></span> <span data-ttu-id="4c134-117">Open Iconic は基本的な SVG に過ぎないため、その他の画像と同じようにこれを表示することをお勧めします (`alt` 属性を忘れないようにします)。</span><span class="sxs-lookup"><span data-stu-id="4c134-117">Since Open Iconic are just basic SVGs, we suggest you display them like you would any other image (don't forget the `alt` attribute).</span></span>

```
<img src="/open-iconic/svg/icon-name.svg" alt="icon name">
```

#### <a name="using-open-iconics-svg-sprite"></a><span data-ttu-id="4c134-118">Open Iconic の SVG スプライトの使用</span><span class="sxs-lookup"><span data-stu-id="4c134-118">Using Open Iconic's SVG Sprite</span></span>

<span data-ttu-id="4c134-119">SVG スプライトとして Open Iconic を使うこともできます。これを使うと、セット内のすべてのアイコンを 1 つの要求で表示できます。</span><span class="sxs-lookup"><span data-stu-id="4c134-119">Open Iconic also comes in a SVG sprite which allows you to display all the icons in the set with a single request.</span></span> <span data-ttu-id="4c134-120">これは、複雑さをなくしたアイコン フォントのようなものです。</span><span class="sxs-lookup"><span data-stu-id="4c134-120">It's like an icon font, without being a hack.</span></span>

<span data-ttu-id="4c134-121">SVG スプライトからアイコンを追加する方法は、使い慣れた方法とは少し異なりますが、やはりとても簡単です。</span><span class="sxs-lookup"><span data-stu-id="4c134-121">Adding an icon from an SVG sprite is a little different than what you're used to, but it's still a piece of cake.</span></span> <span data-ttu-id="4c134-122">"*ヒント:アイコンのスタイルを設定しやすくするために、*" `<svg>` "*タグに汎用クラスを追加し、*" `<use>` "*タグに異なるアイコンごとに一意のクラス名を追加することをお勧めします。*"</span><span class="sxs-lookup"><span data-stu-id="4c134-122">*Tip: To make your icons easily style able, we suggest adding a general class to the* `<svg>` *tag and a unique class name for each different icon in the* `<use>` *tag.*</span></span>  

```
<svg class="icon">
  <use xlink:href="open-iconic.svg#account-login" class="icon-account-login"></use>
</svg>
```

<span data-ttu-id="4c134-123">アイコンをサイズ変更するために必要なのは、基本的な CSS のみです。</span><span class="sxs-lookup"><span data-stu-id="4c134-123">Sizing icons only needs basic CSS.</span></span> <span data-ttu-id="4c134-124">アイコンの形式はすべて正方形であるため、単純に同じ幅と高さで `<svg>` タグを設定します。</span><span class="sxs-lookup"><span data-stu-id="4c134-124">All the icons are in a square format, so just set the `<svg>` tag with equal width and height dimensions.</span></span>

```
.icon {
  width: 16px;
  height: 16px;
}
```

<span data-ttu-id="4c134-125">アイコンの色分けはさらに簡単です。</span><span class="sxs-lookup"><span data-stu-id="4c134-125">Coloring icons is even easier.</span></span> <span data-ttu-id="4c134-126">必要な操作は、`<use>` タグの `fill` ルールを設定することだけです。</span><span class="sxs-lookup"><span data-stu-id="4c134-126">All you need to do is set the `fill` rule on the `<use>` tag.</span></span>

```
.icon-account-login {
  fill: #f00;
}
```

<span data-ttu-id="4c134-127">SVG スプライトについて詳しくは、[Chris Coyier によるガイド](http://css-tricks.com/svg-sprites-use-better-icon-fonts/)をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="4c134-127">To learn more about SVG Sprites, read [Chris Coyier's guide](http://css-tricks.com/svg-sprites-use-better-icon-fonts/).</span></span>

#### <a name="using-open-iconics-icon-font"></a><span data-ttu-id="4c134-128">Open Iconic のアイコン フォントの使用...</span><span class="sxs-lookup"><span data-stu-id="4c134-128">Using Open Iconic's Icon Font...</span></span>


##### <a name="with-bootstrap"></a><span data-ttu-id="4c134-129">…Bootstrap と共に</span><span class="sxs-lookup"><span data-stu-id="4c134-129">…with Bootstrap</span></span>

<span data-ttu-id="4c134-130">Bootstrap のスタイル シートは、`font/css/open-iconic-bootstrap.{css, less, scss, styl}` で確認できます。</span><span class="sxs-lookup"><span data-stu-id="4c134-130">You can find our Bootstrap stylesheets in `font/css/open-iconic-bootstrap.{css, less, scss, styl}`</span></span>


```
<link href="/open-iconic/font/css/open-iconic-bootstrap.css" rel="stylesheet">
```


```
<span class="oi oi-icon-name" title="icon name" aria-hidden="true"></span>
```

##### <a name="with-foundation"></a><span data-ttu-id="4c134-131">…Foundation と共に</span><span class="sxs-lookup"><span data-stu-id="4c134-131">…with Foundation</span></span>

<span data-ttu-id="4c134-132">Foundation のスタイル シートは、`font/css/open-iconic-foundation.{css, less, scss, styl}` で確認できます。</span><span class="sxs-lookup"><span data-stu-id="4c134-132">You can find our Foundation stylesheets in `font/css/open-iconic-foundation.{css, less, scss, styl}`</span></span>

```
<link href="/open-iconic/font/css/open-iconic-foundation.css" rel="stylesheet">
```


```
<span class="fi-icon-name" title="icon name" aria-hidden="true"></span>
```

##### <a name="on-its-own"></a><span data-ttu-id="4c134-133">…そのままで</span><span class="sxs-lookup"><span data-stu-id="4c134-133">…on its own</span></span>

<span data-ttu-id="4c134-134">既定のスタイル シートは、`font/css/open-iconic.{css, less, scss, styl}` で確認できます。</span><span class="sxs-lookup"><span data-stu-id="4c134-134">You can find our default stylesheets in `font/css/open-iconic.{css, less, scss, styl}`</span></span>

```
<link href="/open-iconic/font/css/open-iconic.css" rel="stylesheet">
```

```
<span class="oi" data-glyph="icon-name" title="icon name" aria-hidden="true"></span>
```


## <a name="license"></a><span data-ttu-id="4c134-135">ライセンス</span><span class="sxs-lookup"><span data-stu-id="4c134-135">License</span></span>

### <a name="icons"></a><span data-ttu-id="4c134-136">アイコン</span><span class="sxs-lookup"><span data-stu-id="4c134-136">Icons</span></span>

<span data-ttu-id="4c134-137">すべてのコード (SVG マークアップを含む) は [MIT ライセンス](http://opensource.org/licenses/MIT)に従います。</span><span class="sxs-lookup"><span data-stu-id="4c134-137">All code (including SVG markup) is under the [MIT License](http://opensource.org/licenses/MIT).</span></span>

### <a name="fonts"></a><span data-ttu-id="4c134-138">フォント</span><span class="sxs-lookup"><span data-stu-id="4c134-138">Fonts</span></span>

<span data-ttu-id="4c134-139">すべてのフォントは [SIL ライセンス](http://scripts.sil.org/cms/scripts/page.php?item_id=OFL_web)に従います。</span><span class="sxs-lookup"><span data-stu-id="4c134-139">All fonts are under the [SIL Licensed](http://scripts.sil.org/cms/scripts/page.php?item_id=OFL_web).</span></span>
