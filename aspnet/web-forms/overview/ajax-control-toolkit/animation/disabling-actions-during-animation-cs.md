---
uid: web-forms/overview/ajax-control-toolkit/animation/disabling-actions-during-animation-cs
title: アニメーション中のアクションをC#無効にする () |Microsoft Docs
author: wenz
description: ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。 また、操作もサポートしています...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 918026b4-2f63-421d-8546-df12856960a8
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/disabling-actions-during-animation-cs
msc.type: authoredcontent
ms.openlocfilehash: e91205ad2f9e6ee1fdd869ceb7587c3a82754772
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599723"
---
# <a name="disabling-actions-during-animation-c"></a><span data-ttu-id="26940-104">アニメーション中のアクションを無効にする (C#)</span><span class="sxs-lookup"><span data-stu-id="26940-104">Disabling Actions during Animation (C#)</span></span>

<span data-ttu-id="26940-105">[Christian Wenz](https://github.com/wenz)別</span><span class="sxs-lookup"><span data-stu-id="26940-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="26940-106">[コードのダウンロード](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation7.cs.zip)または[PDF のダウンロード](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation7CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="26940-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation7.cs.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation7CS.pdf)</span></span>

> <span data-ttu-id="26940-107">ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。</span><span class="sxs-lookup"><span data-stu-id="26940-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="26940-108">また、マウスクリックなどの操作もサポートしています。</span><span class="sxs-lookup"><span data-stu-id="26940-108">It also supports actions, like mouse clicks.</span></span> <span data-ttu-id="26940-109">ただし、マウスクリックでアニメーションを開始する場合は、アニメーション中にマウスのクリックを無効にすることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="26940-109">However when a mouse click starts an animation, it is desirable to disable mouse clicks during the animation.</span></span>

## <a name="overview"></a><span data-ttu-id="26940-110">の概要</span><span class="sxs-lookup"><span data-stu-id="26940-110">Overview</span></span>

<span data-ttu-id="26940-111">ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。</span><span class="sxs-lookup"><span data-stu-id="26940-111">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="26940-112">また、マウスクリックなどの操作もサポートしています。</span><span class="sxs-lookup"><span data-stu-id="26940-112">It also supports actions, like mouse clicks.</span></span> <span data-ttu-id="26940-113">ただし、マウスクリックでアニメーションを開始する場合は、アニメーション中にマウスのクリックを無効にすることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="26940-113">However when a mouse click starts an animation, it is desirable to disable mouse clicks during the animation.</span></span>

## <a name="steps"></a><span data-ttu-id="26940-114">手順</span><span class="sxs-lookup"><span data-stu-id="26940-114">Steps</span></span>

<span data-ttu-id="26940-115">まず、ページに `ScriptManager` を含めます。次に、ASP.NET AJAX ライブラリが読み込まれ、Control Toolkit を使用できるようになります。</span><span class="sxs-lookup"><span data-stu-id="26940-115">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](disabling-actions-during-animation-cs/samples/sample1.aspx)]

<span data-ttu-id="26940-116">アニメーションは、次のような HTML ボタンに適用されます。</span><span class="sxs-lookup"><span data-stu-id="26940-116">The animation will be applied to an HTML button like this:</span></span>

[!code-aspx[Main](disabling-actions-during-animation-cs/samples/sample2.aspx)]

<span data-ttu-id="26940-117">ボタンがポストバックを作成しないようにするため、Web コントロールの代わりに HTML コントロールが使用されていることに注意してください。ここでは、クライアント側のアニメーションを起動します。</span><span class="sxs-lookup"><span data-stu-id="26940-117">Note that an HTML Control is used instead of a Web Control since we do not want the button to create a postback; it shall just launch the client-side animation for us.</span></span>

<span data-ttu-id="26940-118">次に、`ID`、`TargetControlID` 属性、および加える `runat="server"`を指定して、ページに `AnimationExtender` を追加します。</span><span class="sxs-lookup"><span data-stu-id="26940-118">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`:</span></span>

[!code-aspx[Main](disabling-actions-during-animation-cs/samples/sample3.aspx)]

<span data-ttu-id="26940-119">`<Animations>` ノード内では、`<OnClick>` はマウスクリックを処理する右側の要素です。</span><span class="sxs-lookup"><span data-stu-id="26940-119">Within the `<Animations>` node, `<OnClick>` is the right element to handle the mouse click.</span></span> <span data-ttu-id="26940-120">ただし、アニメーション中にボタンをクリックすることもできます。</span><span class="sxs-lookup"><span data-stu-id="26940-120">However, the button could be clicked during the animation, as well.</span></span> <span data-ttu-id="26940-121">`<EnableAction>` 要素は、そのような処理を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="26940-121">The `<EnableAction>` element can take care of that.</span></span> <span data-ttu-id="26940-122">`Enabled="false"` 設定すると、アニメーションの一部としてボタンが無効になります。</span><span class="sxs-lookup"><span data-stu-id="26940-122">Setting `Enabled="false"` disables the button as part of the animation.</span></span> <span data-ttu-id="26940-123">複数の個別のアニメーション (ボタンと実際のアニメーションを無効にする) を使用しているため、1つのアニメーションを1つに連結するには、`<Parallel>` 要素が必要です。</span><span class="sxs-lookup"><span data-stu-id="26940-123">Since we are using several individual animations (disabling the button and the actual animations), the `<Parallel>` element is required to glue the single animations together into one.</span></span> <span data-ttu-id="26940-124">`AnimationExtender`の完全なマークアップを次に示します。</span><span class="sxs-lookup"><span data-stu-id="26940-124">Here is the complete markup for `AnimationExtender`:</span></span>

[!code-aspx[Main](disabling-actions-during-animation-cs/samples/sample4.aspx)]

<span data-ttu-id="26940-125">また、リストの末尾にある次の XML 要素を使用して、アニメーションの後にボタンを再び有効にすることもできます。</span><span class="sxs-lookup"><span data-stu-id="26940-125">It would also be possible to re-enable to button after the animation, using the following XML element at the end of the list:</span></span>

[!code-xml[Main](disabling-actions-during-animation-cs/samples/sample5.xml)]

<span data-ttu-id="26940-126">ただし、このようなシナリオでは、ボタンがフェードアウトし、アニメーションの最後に表示されないため、これは役に立ちません。</span><span class="sxs-lookup"><span data-stu-id="26940-126">However in the given scenario this would be useless since the button fades out and is not visible at the end of the animation.</span></span>

<span data-ttu-id="26940-127">[アニメーションが実行されるとすぐにボタンが無効に ![](disabling-actions-during-animation-cs/_static/image2.png)](disabling-actions-during-animation-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="26940-127">[![The button is disabled as soon as the animation runs](disabling-actions-during-animation-cs/_static/image2.png)](disabling-actions-during-animation-cs/_static/image1.png)</span></span>

<span data-ttu-id="26940-128">このボタンは、アニメーションが実行されるとすぐに無効になります ([クリックすると、フルサイズの画像が表示](disabling-actions-during-animation-cs/_static/image3.png)されます)</span><span class="sxs-lookup"><span data-stu-id="26940-128">The button is disabled as soon as the animation runs ([Click to view full-size image](disabling-actions-during-animation-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="26940-129">[前へ](animating-in-response-to-user-interaction-cs.md)
> [次へ](triggering-an-animation-in-another-control-cs.md)</span><span class="sxs-lookup"><span data-stu-id="26940-129">[Previous](animating-in-response-to-user-interaction-cs.md)
[Next](triggering-an-animation-in-another-control-cs.md)</span></span>
