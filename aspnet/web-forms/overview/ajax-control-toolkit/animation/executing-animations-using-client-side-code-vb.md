---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-animations-using-client-side-code-vb
title: クライアント側コードを使用してアニメーションを実行する (VB) |Microsoft Docs
author: wenz
description: ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。 アニメーションの実行...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: f7073f50-d765-456d-9957-926ce60f35f6
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-animations-using-client-side-code-vb
msc.type: authoredcontent
ms.openlocfilehash: 7ef36900d20d8d07c3c6f3b63ce96568a377a0ed
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74575475"
---
# <a name="executing-animations-using-client-side-code-vb"></a><span data-ttu-id="ef35f-104">クライアント側コードを使用してアニメーションを実行する (VB)</span><span class="sxs-lookup"><span data-stu-id="ef35f-104">Executing Animations Using Client-Side Code (VB)</span></span>

<span data-ttu-id="ef35f-105">[Christian Wenz](https://github.com/wenz)別</span><span class="sxs-lookup"><span data-stu-id="ef35f-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="ef35f-106">[コードのダウンロード](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation10.vb.zip)または[PDF のダウンロード](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation10VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="ef35f-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation10.vb.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation10VB.pdf)</span></span>

> <span data-ttu-id="ef35f-107">ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。</span><span class="sxs-lookup"><span data-stu-id="ef35f-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="ef35f-108">アニメーションの実行は、カスタムクライアント側の JavaScript コードを使用してトリガーすることもできます。</span><span class="sxs-lookup"><span data-stu-id="ef35f-108">The animation execution may also be triggered using custom client-side JavaScript code.</span></span>

## <a name="overview"></a><span data-ttu-id="ef35f-109">の概要</span><span class="sxs-lookup"><span data-stu-id="ef35f-109">Overview</span></span>

<span data-ttu-id="ef35f-110">ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。</span><span class="sxs-lookup"><span data-stu-id="ef35f-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="ef35f-111">アニメーションの実行は、カスタムクライアント側の JavaScript コードを使用してトリガーすることもできます。</span><span class="sxs-lookup"><span data-stu-id="ef35f-111">The animation execution may also be triggered using custom client-side JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="ef35f-112">手順</span><span class="sxs-lookup"><span data-stu-id="ef35f-112">Steps</span></span>

<span data-ttu-id="ef35f-113">まず、ページに `ScriptManager` を含めます。次に、ASP.NET AJAX ライブラリが読み込まれ、Control Toolkit を使用できるようになります。</span><span class="sxs-lookup"><span data-stu-id="ef35f-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](executing-animations-using-client-side-code-vb/samples/sample1.aspx)]

<span data-ttu-id="ef35f-114">アニメーションは、次のようなテキストパネルに適用されます。</span><span class="sxs-lookup"><span data-stu-id="ef35f-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](executing-animations-using-client-side-code-vb/samples/sample2.aspx)]

<span data-ttu-id="ef35f-115">パネルに関連付けられている CSS クラスで、優れた背景色を定義し、パネルに固定幅を設定します。</span><span class="sxs-lookup"><span data-stu-id="ef35f-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](executing-animations-using-client-side-code-vb/samples/sample3.css)]

<span data-ttu-id="ef35f-116">次に、`ID`、`TargetControlID` 属性、および加える `runat="server"`を指定して、ページに `AnimationExtender` を追加します。</span><span class="sxs-lookup"><span data-stu-id="ef35f-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`:</span></span>

[!code-aspx[Main](executing-animations-using-client-side-code-vb/samples/sample4.aspx)]

<span data-ttu-id="ef35f-117">`<Animations>` ノード内で `<OnClick>` を使用して、ユーザーがパネルをクリックした後にアニメーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="ef35f-117">Within the `<Animations>` node, use `<OnClick>` to run the animations once the user clicks on the panel.</span></span> <span data-ttu-id="ef35f-118">並列で実行される2つのアニメーションを追加します。</span><span class="sxs-lookup"><span data-stu-id="ef35f-118">Add two animations to be executed in parallel:</span></span>

[!code-xml[Main](executing-animations-using-client-side-code-vb/samples/sample5.xml)]

<span data-ttu-id="ef35f-119">このデモでは、ページが実行されると、JavaScript コードを使用して、このアニメーション (およびコントロールツールキットを使用して作成されたその他のアニメーション) を実行します。</span><span class="sxs-lookup"><span data-stu-id="ef35f-119">For the sake of demonstration, this animation (and any other animation created using the Control Toolkit) is executed using JavaScript code, once the page runs.</span></span> <span data-ttu-id="ef35f-120">まず、`AnimationExtender` コントロールにアクセスする必要があります。</span><span class="sxs-lookup"><span data-stu-id="ef35f-120">First of all we need access to the `AnimationExtender` control.</span></span> <span data-ttu-id="ef35f-121">ASP.NET AJAX ライブラリには、このタスクの `$find()` 関数が用意されています。</span><span class="sxs-lookup"><span data-stu-id="ef35f-121">The ASP.NET AJAX library provides the `$find()` function for this task:</span></span>

[!code-csharp[Main](executing-animations-using-client-side-code-vb/samples/sample6.cs)]

<span data-ttu-id="ef35f-122">`AnimationExtender` コントロールは、XML マークアップで使用されるイベントハンドラーと同じ名前のメソッド (`OnClick()`、`OnLoad()`など) を含む豊富な API を公開します。</span><span class="sxs-lookup"><span data-stu-id="ef35f-122">The `AnimationExtender` control exposes a rich API, including methods with names identical to the event handlers used in the XML markup: `OnClick()`, `OnLoad()`, and so on.</span></span> <span data-ttu-id="ef35f-123">たとえば、`OnClick()` メソッドを呼び出すと、`AnimationExtender` コントロールの `<OnClick>` 要素内でアニメーションが実行されます。</span><span class="sxs-lookup"><span data-stu-id="ef35f-123">For instance, a call of the `OnClick()` method executes the animation within the `<OnClick>` element of the `AnimationExtender` control:</span></span>

[!code-javascript[Main](executing-animations-using-client-side-code-vb/samples/sample7.js)]

<span data-ttu-id="ef35f-124">ページが完全に読み込まれた後にパネルをエミュレートする完全なクライアント側 JavaScript コードを次に示します。 `pageLoad()` 関数名が使用されていることに注意してください。これは、ページと含まれているすべての JavaScript ライブラリが読み込まれた後に ASP.NET AJAX によって呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="ef35f-124">Here is the complete client-side JavaScript code that emulates the click on the panel once the page has been fully loaded note that the `pageLoad()` function name is used which is called by ASP.NET AJAX once the page and all included JavaScript libraries have been loaded.</span></span>

[!code-html[Main](executing-animations-using-client-side-code-vb/samples/sample8.html)]

<span data-ttu-id="ef35f-125">[マウスをクリックせずに、アニメーションをすぐに実行 ![](executing-animations-using-client-side-code-vb/_static/image2.png)](executing-animations-using-client-side-code-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="ef35f-125">[![The animation runs immediately, without a mouse click](executing-animations-using-client-side-code-vb/_static/image2.png)](executing-animations-using-client-side-code-vb/_static/image1.png)</span></span>

<span data-ttu-id="ef35f-126">アニメーションは、マウスクリックなしですぐに実行されます ([クリックすると、フルサイズの画像が表示](executing-animations-using-client-side-code-vb/_static/image3.png)されます)</span><span class="sxs-lookup"><span data-stu-id="ef35f-126">The animation runs immediately, without a mouse click ([Click to view full-size image](executing-animations-using-client-side-code-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="ef35f-127">[前へ](modifying-animations-from-the-server-side-vb.md)
> [次へ](changing-an-animation-using-client-side-code-vb.md)</span><span class="sxs-lookup"><span data-stu-id="ef35f-127">[Previous](modifying-animations-from-the-server-side-vb.md)
[Next](changing-an-animation-using-client-side-code-vb.md)</span></span>
