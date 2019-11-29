---
uid: web-forms/overview/ajax-control-toolkit/animation/dynamically-controlling-updatepanel-animations-cs
title: UpdatePanel アニメーションを動的にC#制御する () |Microsoft Docs
author: wenz
description: ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。 ... の内容
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 5138b8fe-98ff-4e73-a00b-e263fc3ff11d
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/dynamically-controlling-updatepanel-animations-cs
msc.type: authoredcontent
ms.openlocfilehash: 183974564764aab9c0d8a4e577995f3c444bf2d3
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74606793"
---
# <a name="dynamically-controlling-updatepanel-animations-c"></a><span data-ttu-id="98658-104">UpdatePanel アニメーションを動的に制御する (C#)</span><span class="sxs-lookup"><span data-stu-id="98658-104">Dynamically Controlling UpdatePanel Animations (C#)</span></span>

<span data-ttu-id="98658-105">[Christian Wenz](https://github.com/wenz)別</span><span class="sxs-lookup"><span data-stu-id="98658-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="98658-106">[コードのダウンロード](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation2.cs.zip)または[PDF のダウンロード](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation2CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="98658-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation2.cs.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation2CS.pdf)</span></span>

> <span data-ttu-id="98658-107">ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。</span><span class="sxs-lookup"><span data-stu-id="98658-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="98658-108">UpdatePanel の内容については、animation framework: Updateパネルアニメーションに大きく依存する特別な extender が存在します。</span><span class="sxs-lookup"><span data-stu-id="98658-108">For the contents of an UpdatePanel, a special extender exists that relies heavily on the animation framework: UpdatePanelAnimation.</span></span> <span data-ttu-id="98658-109">また、UpdatePanel トリガーと共に使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="98658-109">It can also work together with UpdatePanel triggers.</span></span>

## <a name="overview"></a><span data-ttu-id="98658-110">の概要</span><span class="sxs-lookup"><span data-stu-id="98658-110">Overview</span></span>

<span data-ttu-id="98658-111">ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。</span><span class="sxs-lookup"><span data-stu-id="98658-111">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="98658-112">`UpdatePanel`の内容については、`UpdatePanelAnimation`のアニメーションフレームワークに大きく依存する特別な extender が存在します。</span><span class="sxs-lookup"><span data-stu-id="98658-112">For the contents of an `UpdatePanel`, a special extender exists that relies heavily on the animation framework: `UpdatePanelAnimation`.</span></span> <span data-ttu-id="98658-113">また、`UpdatePanel` トリガーと共に使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="98658-113">It can also work together with `UpdatePanel` triggers.</span></span>

## <a name="steps"></a><span data-ttu-id="98658-114">手順</span><span class="sxs-lookup"><span data-stu-id="98658-114">Steps</span></span>

<span data-ttu-id="98658-115">最初の手順は通常どおり、ASP.NET AJAX ライブラリが読み込まれ、Control Toolkit を使用できるように、ページに `ScriptManager` を含めることです。</span><span class="sxs-lookup"><span data-stu-id="98658-115">The first step is as usual to include the `ScriptManager` in the page so that the ASP.NET AJAX library is loaded and the Control Toolkit can be used:</span></span>

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-cs/samples/sample1.aspx)]

<span data-ttu-id="98658-116">このシナリオのアニメーションは、現在の時刻の表示に適用されます。</span><span class="sxs-lookup"><span data-stu-id="98658-116">The animation in this scenario will be applied to a display of the current time.</span></span> <span data-ttu-id="98658-117">この情報は、`Page_Load()` メソッドを使用してラベルに書き込むことができます (わかりやすくするために、次のインラインコードが使用されます)。</span><span class="sxs-lookup"><span data-stu-id="98658-117">This information can be written into a label using the `Page_Load()` method, or (for the sake of simplicity) the following inline code is used:</span></span>

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-cs/samples/sample2.aspx)]

<span data-ttu-id="98658-118">また、時間の更新をトリガーするボタンが作成されます。</span><span class="sxs-lookup"><span data-stu-id="98658-118">Also, a button to trigger updating the time is created:</span></span>

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-cs/samples/sample3.aspx)]

<span data-ttu-id="98658-119">このコードは、`UpdatePanel` 要素の `<ContentTemplate>` セクションに配置されます。</span><span class="sxs-lookup"><span data-stu-id="98658-119">This code is then put into the `<ContentTemplate>` section of an `UpdatePanel` element.</span></span> <span data-ttu-id="98658-120">パネルの `UpdateMode` 属性は、トリガーのみがパネルの内容を更新する可能性があるため、`"Conditional"`に設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="98658-120">The panel's `UpdateMode` attribute must be set to `"Conditional"`, since only triggers may update the panel's contents.</span></span> <span data-ttu-id="98658-121">`UpdatePanel`の `<Triggers>` セクションでは、非同期ポストバックトリガーが作成され、ボタンの `Click` イベントに関連付けられます。</span><span class="sxs-lookup"><span data-stu-id="98658-121">In the `<Triggers>` section of the `UpdatePanel`, an asynchronous postback trigger is created and tied to the `Click` event of the button.</span></span> <span data-ttu-id="98658-122">このため、ユーザーがボタンをクリックすると、`UpdatePanel` が更新されます。</span><span class="sxs-lookup"><span data-stu-id="98658-122">Thus, if the user clicks on the button, the `UpdatePanel` is refreshed.</span></span> <span data-ttu-id="98658-123">`UpdatePanel` コントロールのマークアップを次に示します。</span><span class="sxs-lookup"><span data-stu-id="98658-123">Here is the markup for the `UpdatePanel` control:</span></span>

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-cs/samples/sample4.aspx)]

<span data-ttu-id="98658-124">最後に、`UpdatePanelAnimationExtender` を構成する必要があります。 `TargetControlID` 属性をパネルの ID に設定し、extender 内でアニメーションを定義します。</span><span class="sxs-lookup"><span data-stu-id="98658-124">Finally, the `UpdatePanelAnimationExtender` must be configured: Set the `TargetControlID` attribute to the ID of the panel, and define an animation within the extender.</span></span> <span data-ttu-id="98658-125">でのフェードは意味があり、更新された時間を視覚的に強調表示します。</span><span class="sxs-lookup"><span data-stu-id="98658-125">Fading in makes sense, which creates a nice visual emphasis on the updated time.</span></span> <span data-ttu-id="98658-126">Extender マークアップは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="98658-126">Your extender markup may then look like this:</span></span>

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-cs/samples/sample5.aspx)]

<span data-ttu-id="98658-127">ブラウザーでファイルを実行します。</span><span class="sxs-lookup"><span data-stu-id="98658-127">Run the file in the browser.</span></span> <span data-ttu-id="98658-128">ボタンをクリックするたびに、現在の時刻がパネルに表示されます。1秒間は常にフェードします。</span><span class="sxs-lookup"><span data-stu-id="98658-128">Whenever you click on the button, the current time is shown in the panel, always fading in for the duration of one second.</span></span>

<span data-ttu-id="98658-129">[現在の時刻がフェードイン ![](dynamically-controlling-updatepanel-animations-cs/_static/image2.png)](dynamically-controlling-updatepanel-animations-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="98658-129">[![The current time is fading in](dynamically-controlling-updatepanel-animations-cs/_static/image2.png)](dynamically-controlling-updatepanel-animations-cs/_static/image1.png)</span></span>

<span data-ttu-id="98658-130">現在の時刻はフェードインします ([クリックすると、フルサイズの画像が表示](dynamically-controlling-updatepanel-animations-cs/_static/image3.png)されます)</span><span class="sxs-lookup"><span data-stu-id="98658-130">The current time is fading in ([Click to view full-size image](dynamically-controlling-updatepanel-animations-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="98658-131">[前へ](animating-an-updatepanel-control-cs.md)
> [次へ](adding-animation-to-a-control-vb.md)</span><span class="sxs-lookup"><span data-stu-id="98658-131">[Previous](animating-an-updatepanel-control-cs.md)
[Next](adding-animation-to-a-control-vb.md)</span></span>
