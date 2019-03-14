---
ms.openlocfilehash: 610b16b181422978dc143b95f28658bbdf177fdd
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57028279"
---
# <a name="jquery"></a><span data-ttu-id="a3a80-101">jQuery</span><span class="sxs-lookup"><span data-stu-id="a3a80-101">jQuery</span></span>

> <span data-ttu-id="a3a80-102">jQuery は、高速で軽量な、豊富な機能を備えた JavaScript ライブラリです。</span><span class="sxs-lookup"><span data-stu-id="a3a80-102">jQuery is a fast, small, and feature-rich JavaScript library.</span></span>

<span data-ttu-id="a3a80-103">jQuery の開始方法と使用方法については、[jQuery のドキュメント](http://api.jquery.com/)をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="a3a80-103">For information on how to get started and how to use jQuery, please see [jQuery's documentation](http://api.jquery.com/).</span></span>
<span data-ttu-id="a3a80-104">ソース ファイルと問題については、[jQuery のリポジトリ](https://github.com/jquery/jquery)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a3a80-104">For source files and issues, please visit the [jQuery repo](https://github.com/jquery/jquery).</span></span>

<span data-ttu-id="a3a80-105">アップグレードする場合は、[3.3.1 に向けたブログ記事](https://blog.jquery.com/2017/03/20/jquery-3.3.1-now-available/)をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="a3a80-105">If upgrading, please see the [blog post for 3.3.1](https://blog.jquery.com/2017/03/20/jquery-3.3.1-now-available/).</span></span> <span data-ttu-id="a3a80-106">これには、以前のバージョンからの重要な違いと、よりわかりやすい変更ログが含まれています。</span><span class="sxs-lookup"><span data-stu-id="a3a80-106">This includes notable differences from the previous version and a more readable changelog.</span></span>

## <a name="including-jquery"></a><span data-ttu-id="a3a80-107">jQuery のインクルード</span><span class="sxs-lookup"><span data-stu-id="a3a80-107">Including jQuery</span></span>

<span data-ttu-id="a3a80-108">jQuery をインクルードする最も一般的な方法を、次にいくつか示します。</span><span class="sxs-lookup"><span data-stu-id="a3a80-108">Below are some of the most common ways to include jQuery.</span></span>

### <a name="browser"></a><span data-ttu-id="a3a80-109">ブラウザー</span><span class="sxs-lookup"><span data-stu-id="a3a80-109">Browser</span></span>

#### <a name="script-tag"></a><span data-ttu-id="a3a80-110">スクリプト タグ</span><span class="sxs-lookup"><span data-stu-id="a3a80-110">Script tag</span></span>

```html
<script src="https://code.jquery.com/jquery-3.3.1.min.js"></script>
```

#### <a name="babel"></a><span data-ttu-id="a3a80-111">Babel</span><span class="sxs-lookup"><span data-stu-id="a3a80-111">Babel</span></span>

<span data-ttu-id="a3a80-112">[Babel](http://babeljs.io/) は次世代の JavaScript コンパイラです。</span><span class="sxs-lookup"><span data-stu-id="a3a80-112">[Babel](http://babeljs.io/) is a next generation JavaScript compiler.</span></span> <span data-ttu-id="a3a80-113">その特徴の 1 つは、ES6/ES2015 モジュールを使用できることです。ブラウザーでは、この機能はまだネイティブではサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="a3a80-113">One of the features is the ability to use ES6/ES2015 modules now, even though browsers do not yet support this feature natively.</span></span>

```js
import $ from "jquery";
```

#### <a name="browserifywebpack"></a><span data-ttu-id="a3a80-114">Browserify/Webpack</span><span class="sxs-lookup"><span data-stu-id="a3a80-114">Browserify/Webpack</span></span>

<span data-ttu-id="a3a80-115">[Browserify](http://browserify.org/) と [Webpack](https://webpack.github.io/) を使用する方法はいくつかあります。</span><span class="sxs-lookup"><span data-stu-id="a3a80-115">There are several ways to use [Browserify](http://browserify.org/) and [Webpack](https://webpack.github.io/).</span></span> <span data-ttu-id="a3a80-116">これらのツールの使用について詳しくは、対応するプロジェクトのドキュメントを参照してください。</span><span class="sxs-lookup"><span data-stu-id="a3a80-116">For more information on using these tools, please refer to the corresponding project's documention.</span></span> <span data-ttu-id="a3a80-117">スクリプトで jQuery をインクルードする場合は、通常、このようになります。</span><span class="sxs-lookup"><span data-stu-id="a3a80-117">In the script, including jQuery will usually look like this...</span></span>

```js
var $ = require("jquery");
```

#### <a name="amd-asynchronous-module-definition"></a><span data-ttu-id="a3a80-118">AMD (非同期モジュール定義)</span><span class="sxs-lookup"><span data-stu-id="a3a80-118">AMD (Asynchronous Module Definition)</span></span>

<span data-ttu-id="a3a80-119">AMD は、ブラウザー用にビルドされたモジュール形式です。</span><span class="sxs-lookup"><span data-stu-id="a3a80-119">AMD is a module format built for the browser.</span></span> <span data-ttu-id="a3a80-120">詳細については、[require.js のドキュメント](http://requirejs.org/docs/whyamd.html)をお勧めします。</span><span class="sxs-lookup"><span data-stu-id="a3a80-120">For more information, we recommend [require.js' documentation](http://requirejs.org/docs/whyamd.html).</span></span>

```js
define(["jquery"], function($) {

});
```

### <a name="node"></a><span data-ttu-id="a3a80-121">ノード</span><span class="sxs-lookup"><span data-stu-id="a3a80-121">Node</span></span>

<span data-ttu-id="a3a80-122">[Node](nodejs.org) に jQuery を含めるには、最初に npm でインストールします。</span><span class="sxs-lookup"><span data-stu-id="a3a80-122">To include jQuery in [Node](nodejs.org), first install with npm.</span></span>

```sh
npm install jquery
```

<span data-ttu-id="a3a80-123">jQuery を Node 内で動作させるには、ドキュメント ウィンドウが必要です。</span><span class="sxs-lookup"><span data-stu-id="a3a80-123">For jQuery to work in Node, a window with a document is required.</span></span> <span data-ttu-id="a3a80-124">Node にはそのようなウィンドウがネイティブで備わっていないため、[jsdom](https://github.com/tmpvar/jsdom) のようなツールで仮に用意されています。</span><span class="sxs-lookup"><span data-stu-id="a3a80-124">Since no such window exists natively in Node, one can be mocked by tools such as [jsdom](https://github.com/tmpvar/jsdom).</span></span> <span data-ttu-id="a3a80-125">これはテストのために役立ちます。</span><span class="sxs-lookup"><span data-stu-id="a3a80-125">This can be useful for testing purposes.</span></span>

```js
require("jsdom").env("", function(err, window) {
    if (err) {
        console.error(err);
        return;
    }

    var $ = require("jquery")(window);
});
```
