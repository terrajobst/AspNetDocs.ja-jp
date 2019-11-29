---
uid: web-forms/overview/ajax-control-toolkit/animation/modifying-animations-from-the-server-side-vb
title: サーバー側からアニメーションを変更する (VB) |Microsoft Docs
author: wenz
description: ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。 アニメーションも...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: addcf4aa-340a-460b-9c64-506424a1f725
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/modifying-animations-from-the-server-side-vb
msc.type: authoredcontent
ms.openlocfilehash: ebc311d1a931ad611d9556799c94440d41a9cf49
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74575233"
---
# <a name="modifying-animations-from-the-server-side-vb"></a><span data-ttu-id="b31e2-104">サーバー側からアニメーションを変更する (VB)</span><span class="sxs-lookup"><span data-stu-id="b31e2-104">Modifying Animations From The Server Side (VB)</span></span>

<span data-ttu-id="b31e2-105">[Christian Wenz](https://github.com/wenz)別</span><span class="sxs-lookup"><span data-stu-id="b31e2-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="b31e2-106">[コードのダウンロード](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation9.vb.zip)または[PDF のダウンロード](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation9VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="b31e2-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation9.vb.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation9VB.pdf)</span></span>

> <span data-ttu-id="b31e2-107">ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。</span><span class="sxs-lookup"><span data-stu-id="b31e2-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="b31e2-108">アニメーションはサーバー側でも変更される可能性があります。</span><span class="sxs-lookup"><span data-stu-id="b31e2-108">The animations may also be changed on the server-side</span></span>

## <a name="overview"></a><span data-ttu-id="b31e2-109">の概要</span><span class="sxs-lookup"><span data-stu-id="b31e2-109">Overview</span></span>

<span data-ttu-id="b31e2-110">ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。</span><span class="sxs-lookup"><span data-stu-id="b31e2-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="b31e2-111">アニメーションはサーバー側でも変更される可能性があります。</span><span class="sxs-lookup"><span data-stu-id="b31e2-111">The animations may also be changed on the server-side</span></span>

## <a name="steps"></a><span data-ttu-id="b31e2-112">手順</span><span class="sxs-lookup"><span data-stu-id="b31e2-112">Steps</span></span>

<span data-ttu-id="b31e2-113">まず、ページに `ScriptManager` を含めます。次に、ASP.NET AJAX ライブラリが読み込まれ、Control Toolkit を使用できるようになります。</span><span class="sxs-lookup"><span data-stu-id="b31e2-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](modifying-animations-from-the-server-side-vb/samples/sample1.aspx)]

<span data-ttu-id="b31e2-114">アニメーションは、次のようなテキストパネルに適用されます。</span><span class="sxs-lookup"><span data-stu-id="b31e2-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](modifying-animations-from-the-server-side-vb/samples/sample2.aspx)]

<span data-ttu-id="b31e2-115">パネルに関連付けられている CSS クラスで、優れた背景色を定義し、パネルに固定幅を設定します。</span><span class="sxs-lookup"><span data-stu-id="b31e2-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](modifying-animations-from-the-server-side-vb/samples/sample3.css)]

<span data-ttu-id="b31e2-116">残りのコードはサーバー側で実行され、マークアップを使用しません。代わりに、コードを使用して `AnimationExtender` コントロールを作成します。</span><span class="sxs-lookup"><span data-stu-id="b31e2-116">The rest of the code runs on the server-side and does not use markup; instead, it uses code to create the `AnimationExtender` control:</span></span>

[!code-aspx[Main](modifying-animations-from-the-server-side-vb/samples/sample4.aspx)]

<span data-ttu-id="b31e2-117">ただし、Control Toolkit は、現在、個々のアニメーションを作成するための API アクセスを提供していません。</span><span class="sxs-lookup"><span data-stu-id="b31e2-117">However, the Control Toolkit currently does not provide an API access to create the individual animations.</span></span> <span data-ttu-id="b31e2-118">ただし、`AnimationExtender`のアニメーションプロパティを、アニメーションを宣言的に割り当てるときに使用する XML マークアップを含む文字列に設定することはできます。</span><span class="sxs-lookup"><span data-stu-id="b31e2-118">It is however possible to set the `AnimationExtender`'s Animations property to a string containing the XML markup used when assigning the animations declaratively.</span></span> <span data-ttu-id="b31e2-119">`<Animations>` 要素を含んでいない XML を作成するには、.NET Framework の XML サポートを使用するか、次のコードのように、文字列を指定するだけです。</span><span class="sxs-lookup"><span data-stu-id="b31e2-119">In order to create the XML which must not contain the `<Animations>` element you could use the .NET Framework's XML support or, as in the following code, just provide the string:</span></span>

[!code-vb[Main](modifying-animations-from-the-server-side-vb/samples/sample5.vb)]

<span data-ttu-id="b31e2-120">最後に、`<form runat="server">` 要素内の現在のページに `AnimationExtender` コントロールを追加し、アニメーションが含まれ、実行されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="b31e2-120">Finally, add the `AnimationExtender` control to the current page, within the `<form runat="server">` element, making sure that the animation is included and runs:</span></span>

[!code-vb[Main](modifying-animations-from-the-server-side-vb/samples/sample6.vb)]

<span data-ttu-id="b31e2-121">[アニメーションがサーバー側C#/VB コードを使用して作成される ![](modifying-animations-from-the-server-side-vb/_static/image2.png)](modifying-animations-from-the-server-side-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="b31e2-121">[![The animation is created using server-side C#/VB code](modifying-animations-from-the-server-side-vb/_static/image2.png)](modifying-animations-from-the-server-side-vb/_static/image1.png)</span></span>

<span data-ttu-id="b31e2-122">アニメーションは、サーバー側C#のコードまたは VB のコードを使用して作成されます ([クリックすると、フルサイズの画像が表示](modifying-animations-from-the-server-side-vb/_static/image3.png)されます)</span><span class="sxs-lookup"><span data-stu-id="b31e2-122">The animation is created using server-side C#/VB code ([Click to view full-size image](modifying-animations-from-the-server-side-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="b31e2-123">[前へ](triggering-an-animation-in-another-control-vb.md)
> [次へ](executing-animations-using-client-side-code-vb.md)</span><span class="sxs-lookup"><span data-stu-id="b31e2-123">[Previous](triggering-an-animation-in-another-control-vb.md)
[Next](executing-animations-using-client-side-code-vb.md)</span></span>
