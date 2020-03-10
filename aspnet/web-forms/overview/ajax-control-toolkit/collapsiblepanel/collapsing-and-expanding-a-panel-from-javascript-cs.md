---
uid: web-forms/overview/ajax-control-toolkit/collapsiblepanel/collapsing-and-expanding-a-panel-from-javascript-cs
title: JavaScript からのパネルの折りたたみと展開C#() |Microsoft Docs
author: wenz
description: ASP.NET AJAX Control Toolkit の CollapsiblePanel コントロールは、パネルを拡張し、その内容を折りたたんで展開する機能を提供します...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: de5500be-75e5-461a-8064-b70ae52ea6a4
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/collapsiblepanel/collapsing-and-expanding-a-panel-from-javascript-cs
msc.type: authoredcontent
ms.openlocfilehash: bed14d82394d28336493bec10e31ddb4d411a192
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78497716"
---
# <a name="collapsing-and-expanding-a-panel-from-javascript-c"></a><span data-ttu-id="a8e17-103">JavaScript からパネルを折りたたむ/展開する (C#)</span><span class="sxs-lookup"><span data-stu-id="a8e17-103">Collapsing and Expanding a Panel from JavaScript (C#)</span></span>

<span data-ttu-id="a8e17-104">[Christian Wenz](https://github.com/wenz)別</span><span class="sxs-lookup"><span data-stu-id="a8e17-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="a8e17-105">[コードのダウンロード](https://download.microsoft.com/download/8/a/a/8aab3c3e-de6f-463f-805c-5fda567eef6e/CollapsiblePanel1.cs.zip)または[PDF のダウンロード](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/collapsiblepanel1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="a8e17-105">[Download Code](https://download.microsoft.com/download/8/a/a/8aab3c3e-de6f-463f-805c-5fda567eef6e/CollapsiblePanel1.cs.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/collapsiblepanel1CS.pdf)</span></span>

> <span data-ttu-id="a8e17-106">ASP.NET AJAX Control Toolkit の CollapsiblePanel コントロールは、パネルを拡張し、その内容を折りたたんでもう一度拡張する機能を提供します。</span><span class="sxs-lookup"><span data-stu-id="a8e17-106">The CollapsiblePanel control in the ASP.NET AJAX Control Toolkit extends a panel and provides it with the capability to collapse its contents and expand it again.</span></span> <span data-ttu-id="a8e17-107">これらの2つのアクションは、カスタム JavaScript コードからトリガーすることもできます。</span><span class="sxs-lookup"><span data-stu-id="a8e17-107">These two actions can also be triggered from custom JavaScript code.</span></span>

## <a name="overview"></a><span data-ttu-id="a8e17-108">概要</span><span class="sxs-lookup"><span data-stu-id="a8e17-108">Overview</span></span>

<span data-ttu-id="a8e17-109">ASP.NET AJAX Control Toolkit の CollapsiblePanel コントロールは、パネルを拡張し、その内容を折りたたんでもう一度拡張する機能を提供します。</span><span class="sxs-lookup"><span data-stu-id="a8e17-109">The CollapsiblePanel control in the ASP.NET AJAX Control Toolkit extends a panel and provides it with the capability to collapse its contents and expand it again.</span></span> <span data-ttu-id="a8e17-110">これらの2つのアクションは、カスタム JavaScript コードからトリガーすることもできます。</span><span class="sxs-lookup"><span data-stu-id="a8e17-110">These two actions can also be triggered from custom JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="a8e17-111">手順</span><span class="sxs-lookup"><span data-stu-id="a8e17-111">Steps</span></span>

<span data-ttu-id="a8e17-112">まず、新しい ASP.NET ページを作成し、1つの `<form>` 要素内に `ScriptManager` を含めます。</span><span class="sxs-lookup"><span data-stu-id="a8e17-112">First of all, create a new ASP.NET page and include the `ScriptManager` within the one `<form>` element.</span></span> <span data-ttu-id="a8e17-113">これにより、Control Toolkit で必要とされる ASP.NET AJAX ライブラリが読み込まれます。</span><span class="sxs-lookup"><span data-stu-id="a8e17-113">This loads the ASP.NET AJAX library which is required by the Control Toolkit:</span></span>

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample1.aspx)]

<span data-ttu-id="a8e17-114">次に、いくつかのテキストを含むパネルを作成して、折りたたみ/展開の効果を確認できるようにします。</span><span class="sxs-lookup"><span data-stu-id="a8e17-114">Then, create a panel with some text so that the collapse/expand effect can be seen:</span></span>

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample2.aspx)]

<span data-ttu-id="a8e17-115">ご覧のとおり、パネルはここに表示されている CSS クラスを参照しています (基本的に、背景色とパネルの幅を定義しています)。</span><span class="sxs-lookup"><span data-stu-id="a8e17-115">As you can see, the panel references a CSS class which is shown here (and basically defines a background color and the panel's width):</span></span>

[!code-css[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample3.css)]

<span data-ttu-id="a8e17-116">`CollapsiblePanelExtender` コントロールには、要求に応じて縮小または展開するパネルをツールキットが認識できるように、`TargetControlID` 属性が必要です。</span><span class="sxs-lookup"><span data-stu-id="a8e17-116">The `CollapsiblePanelExtender` control requires the `TargetControlID` attribute so that the toolkit knows which panel to collapse or expand upon request:</span></span>

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample4.aspx)]

<span data-ttu-id="a8e17-117">残念ながら、現在のところ、extender は、パネルを折りたたんだり展開したりするための特定の API を公開していませんが、いくつかのドキュメントに記載されていないメソッドは、</span><span class="sxs-lookup"><span data-stu-id="a8e17-117">Unfortunately, the extender currently does not expose a specific API for collapsing or expanding the panel, but some undocumented methods will do.</span></span> <span data-ttu-id="a8e17-118">まず、3つの HTML ボタンをページに追加します。これにより、クライアント側の JavaScript がトリガーされ、パネルの内容が折りたたまれたり、展開されたりします。</span><span class="sxs-lookup"><span data-stu-id="a8e17-118">First of all, add three HTML buttons to the page which will then trigger the client-side JavaScript to collapse or expand the panel's contents:</span></span>

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample5.aspx)]

<span data-ttu-id="a8e17-119">クライアント側の JavaScript コード (`<script type="text/javascript">`で開始) では、`$find()` メソッドを使用して `CollapsiblePanelExtender`にアクセスする必要があります。</span><span class="sxs-lookup"><span data-stu-id="a8e17-119">In the client-side JavaScript code (started with `<script type="text/javascript">`), the `$find()` method needs to be used to access the `CollapsiblePanelExtender`.</span></span> <span data-ttu-id="a8e17-120">`$find("cpe")` はその参照を返します。</span><span class="sxs-lookup"><span data-stu-id="a8e17-120">`$find("cpe")` will return a reference to it.</span></span> <span data-ttu-id="a8e17-121">そこから、特定のメソッドによってタスクが手動で解決されます。</span><span class="sxs-lookup"><span data-stu-id="a8e17-121">From there on, specific methods will solve the task at hand.</span></span>

<span data-ttu-id="a8e17-122">パネルを開く (展開する) メソッドは `_doOpen()`と呼ばれます。次のコードは、最初のボタンがクリックされたときに呼び出される `doOpen()` 関数を実装しています。</span><span class="sxs-lookup"><span data-stu-id="a8e17-122">The method for opening (expanding) the panel is called `_doOpen()`; the following code implements the `doOpen()` function called when the first button is clicked:</span></span>

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample6.js)]

<span data-ttu-id="a8e17-123">パネルを閉じる、または折りたたむには、`_doClose()` メソッドを実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a8e17-123">For closing, or collapsing the panel, the `_doClose()` method needs to be executed.</span></span> <span data-ttu-id="a8e17-124">そのため、ユーザーが2番目のボタンをクリックすると、次の JavaScript コードが呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="a8e17-124">So when the user clicks on the second button, the following JavaScript code is called:</span></span>

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample7.js)]

<span data-ttu-id="a8e17-125">3番目のボタンは、パネルの状態を切り替えます。つまり、折りたたまれてから展開されます。逆の場合も同様です。</span><span class="sxs-lookup"><span data-stu-id="a8e17-125">The third button toggles the state of the panel: from collapsed to expanded, and vice versa.</span></span> <span data-ttu-id="a8e17-126">`CollapsiblePanelExtender` は、パネルの状態を元に戻す `toggle()` メソッドを公開します。</span><span class="sxs-lookup"><span data-stu-id="a8e17-126">The `CollapsiblePanelExtender` exposes the `toggle()` method which does exactly that: reverses the state of the panel.</span></span> <span data-ttu-id="a8e17-127">ただし、別の方法もあります (`toggle()` メソッドによって内部で使用されます)。 `CollapsiblePanelExtender()` の `get_Collapsed()` メソッドによって、パネルが折りたたまれているかどうかがわかります。</span><span class="sxs-lookup"><span data-stu-id="a8e17-127">However there is also another approach (which is internally used by the `toggle()` method): The `get_Collapsed()` method of the `CollapsiblePanelExtender()` tells us whether the panel is collapsed or not.</span></span> <span data-ttu-id="a8e17-128">この関数の戻り値に応じて、パネルは展開された (`_doOpen()` メソッド) か、折りたたまれた (`_doClose()`) メソッドになります。</span><span class="sxs-lookup"><span data-stu-id="a8e17-128">Depending on the return value of this function, the panel is then either expanded (`_doOpen()` method) or collapsed (`_doClose()`) method:</span></span>

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample8.js)]

<span data-ttu-id="a8e17-129">[3番目のボタン ![、パネルの状態を変更します。折りたたまれてから展開された状態に戻ります。](collapsing-and-expanding-a-panel-from-javascript-cs/_static/image2.png)](collapsing-and-expanding-a-panel-from-javascript-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="a8e17-129">[![The third button changes the state of the panel: from collapsed to expanded and back](collapsing-and-expanding-a-panel-from-javascript-cs/_static/image2.png)](collapsing-and-expanding-a-panel-from-javascript-cs/_static/image1.png)</span></span>

<span data-ttu-id="a8e17-130">3番目のボタンは、パネルの状態を変更します。折りたたまれてから展開されてから元に戻ります ([クリックすると、フルサイズの画像が表示](collapsing-and-expanding-a-panel-from-javascript-cs/_static/image3.png)されます)。</span><span class="sxs-lookup"><span data-stu-id="a8e17-130">The third button changes the state of the panel: from collapsed to expanded and back ([Click to view full-size image](collapsing-and-expanding-a-panel-from-javascript-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="a8e17-131">Next</span><span class="sxs-lookup"><span data-stu-id="a8e17-131">Next</span></span>](collapsing-and-expanding-a-panel-from-javascript-vb.md)
