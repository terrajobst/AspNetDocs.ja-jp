---
uid: web-forms/overview/ajax-control-toolkit/animation/changing-an-animation-using-client-side-code-cs
title: クライアント側コードを使用してアニメーションをC#変更する () |Microsoft Docs
author: wenz
description: ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。 アニメーションは、
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 2bfbc5cc-f942-44b7-a62d-a29520f1da9a
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/changing-an-animation-using-client-side-code-cs
msc.type: authoredcontent
ms.openlocfilehash: 84fc2d6646b89cfabb2193cdfca59462d6d7ef16
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484054"
---
# <a name="changing-an-animation-using-client-side-code-c"></a><span data-ttu-id="bdd3b-104">クライアント側コードを使用してアニメーションを変更する (C#)</span><span class="sxs-lookup"><span data-stu-id="bdd3b-104">Changing an Animation Using Client-Side Code (C#)</span></span>

<span data-ttu-id="bdd3b-105">[Christian Wenz](https://github.com/wenz)別</span><span class="sxs-lookup"><span data-stu-id="bdd3b-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="bdd3b-106">[コードのダウンロード](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation11.cs.zip)または[PDF のダウンロード](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation11CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="bdd3b-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation11.cs.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation11CS.pdf)</span></span>

> <span data-ttu-id="bdd3b-107">ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。</span><span class="sxs-lookup"><span data-stu-id="bdd3b-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="bdd3b-108">アニメーションは、カスタムクライアント側の JavaScript コードを使用して変更することもできます。</span><span class="sxs-lookup"><span data-stu-id="bdd3b-108">The animation can also be changed using custom client-side JavaScript code.</span></span>

## <a name="overview"></a><span data-ttu-id="bdd3b-109">概要</span><span class="sxs-lookup"><span data-stu-id="bdd3b-109">Overview</span></span>

<span data-ttu-id="bdd3b-110">ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。</span><span class="sxs-lookup"><span data-stu-id="bdd3b-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="bdd3b-111">アニメーションは、カスタムクライアント側の JavaScript コードを使用して変更することもできます。</span><span class="sxs-lookup"><span data-stu-id="bdd3b-111">The animation can also be changed using custom client-side JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="bdd3b-112">手順</span><span class="sxs-lookup"><span data-stu-id="bdd3b-112">Steps</span></span>

<span data-ttu-id="bdd3b-113">まず、ページに `ScriptManager` を含めます。次に、ASP.NET AJAX ライブラリが読み込まれ、Control Toolkit を使用できるようになります。</span><span class="sxs-lookup"><span data-stu-id="bdd3b-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](changing-an-animation-using-client-side-code-cs/samples/sample1.aspx)]

<span data-ttu-id="bdd3b-114">アニメーションは、次のようなテキストパネルに適用されます。</span><span class="sxs-lookup"><span data-stu-id="bdd3b-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](changing-an-animation-using-client-side-code-cs/samples/sample2.aspx)]

<span data-ttu-id="bdd3b-115">パネルに関連付けられている CSS クラスで、優れた背景色を定義し、パネルに固定幅を設定します。</span><span class="sxs-lookup"><span data-stu-id="bdd3b-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](changing-an-animation-using-client-side-code-cs/samples/sample3.css)]

<span data-ttu-id="bdd3b-116">実際のアニメーションは、HTML ボタンによって起動されます。</span><span class="sxs-lookup"><span data-stu-id="bdd3b-116">The actual animation is launched by an HTML button:</span></span>

[!code-aspx[Main](changing-an-animation-using-client-side-code-cs/samples/sample4.aspx)]

<span data-ttu-id="bdd3b-117">次に、`ID`、`TargetControlID` 属性、および加える `runat="server"`を指定して、ページに `AnimationExtender` を追加します。</span><span class="sxs-lookup"><span data-stu-id="bdd3b-117">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`:</span></span>

[!code-aspx[Main](changing-an-animation-using-client-side-code-cs/samples/sample5.aspx)]

<span data-ttu-id="bdd3b-118">`AnimationExtender` コントロール内に `<Animations>` ノードがないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="bdd3b-118">Note that there is no `<Animations>` node within the `AnimationExtender` control.</span></span> <span data-ttu-id="bdd3b-119">カスタム JavaScript コードを使用して、コントロールで使用されるアニメーションを提供します。</span><span class="sxs-lookup"><span data-stu-id="bdd3b-119">Custom JavaScript code is used to provide the animations to be used with the control.</span></span>

<span data-ttu-id="bdd3b-120">`AnimationExtender`のサーバー API と同様に、まだ extender にアニメーションを割り当てる簡単な方法はありません。</span><span class="sxs-lookup"><span data-stu-id="bdd3b-120">As with the server API of `AnimationExtender`, there is no easy way to assign an animation to the extender yet.</span></span> <span data-ttu-id="bdd3b-121">ただし、extender では、さまざまなイベント (`OnClick`、`OnLoad`など) に登録されたアニメーションの読み取りおよび書き込みを行うためのメソッドがいくつか公開されています。</span><span class="sxs-lookup"><span data-stu-id="bdd3b-121">However the extender does expose several methods to read and write animations registered with the various events (`OnClick`, `OnLoad`, and so on).</span></span> <span data-ttu-id="bdd3b-122">次に例をいくつか示します。</span><span class="sxs-lookup"><span data-stu-id="bdd3b-122">Here are some examples:</span></span>

- `get_OnClick()`
- `set_OnClick()`
- `get_OnLoad()`
- `set_OnLoad()`
- `...`

<span data-ttu-id="bdd3b-123">`get_*()` 関数の戻り値の形式と、`set_*()` 関数の引数の形式は JSON 文字列であり、XML マークアップの内容を表すオブジェクトを提供します。</span><span class="sxs-lookup"><span data-stu-id="bdd3b-123">The format of the return value of the `get_*()` functions and the format of the argument for the `set_*()` functions is a JSON string, providing an object representation of what the XML markup would be.</span></span> <span data-ttu-id="bdd3b-124">現在、でオブジェクトを渡す方法はありませんが、指定されたアニメーション (`get_OnXXXBehavior()` メソッド) からオブジェクトを読み取ることはできます。</span><span class="sxs-lookup"><span data-stu-id="bdd3b-124">Currently, there is no way to pass an object in, but it is possible to read an object from a given animation (`get_OnXXXBehavior()` methods).</span></span>

<span data-ttu-id="bdd3b-125">次に示すのは、ボタンによってトリガーされるアニメーションを表す JSON 文字列 (区切り引用符が不要で、適切に書式設定されたもの) ですが、パネルをアニメーション化し、同時にフェードアウトします。</span><span class="sxs-lookup"><span data-stu-id="bdd3b-125">Here is a JSON string (without the delimiting quotes and formatted nicely) representing an animation triggered by the button, but animating the panel by resizing it and fading it out at the same time:</span></span>

[!code-json[Main](changing-an-animation-using-client-side-code-cs/samples/sample6.json)]

<span data-ttu-id="bdd3b-126">次の JavaScript コードは、この JSON descripting を現在の extender の `OnClick` アニメーションに割り当てて実行します。</span><span class="sxs-lookup"><span data-stu-id="bdd3b-126">The following JavaScript code assigns this JSON descripting to the `OnClick` animation of the current extender and runs it:</span></span>

[!code-html[Main](changing-an-animation-using-client-side-code-cs/samples/sample7.html)]

<span data-ttu-id="bdd3b-127">[マウスをクリックしないで (そして、マークアップをほとんど行わずに) アニメーションをすぐに実行 ![](changing-an-animation-using-client-side-code-cs/_static/image2.png)](changing-an-animation-using-client-side-code-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="bdd3b-127">[![The animation runs immediately, without a mouse click (and with very little markup)](changing-an-animation-using-client-side-code-cs/_static/image2.png)](changing-an-animation-using-client-side-code-cs/_static/image1.png)</span></span>

<span data-ttu-id="bdd3b-128">アニメーションは、マウスをクリックすることなく (そして、マークアップが非常に少ない)、すぐに実行されます ([クリックすると、フルサイズの画像が表示](changing-an-animation-using-client-side-code-cs/_static/image3.png)されます)</span><span class="sxs-lookup"><span data-stu-id="bdd3b-128">The animation runs immediately, without a mouse click (and with very little markup) ([Click to view full-size image](changing-an-animation-using-client-side-code-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="bdd3b-129">[前へ](executing-animations-using-client-side-code-cs.md)
> [次へ](animating-an-updatepanel-control-cs.md)</span><span class="sxs-lookup"><span data-stu-id="bdd3b-129">[Previous](executing-animations-using-client-side-code-cs.md)
[Next](animating-an-updatepanel-control-cs.md)</span></span>
