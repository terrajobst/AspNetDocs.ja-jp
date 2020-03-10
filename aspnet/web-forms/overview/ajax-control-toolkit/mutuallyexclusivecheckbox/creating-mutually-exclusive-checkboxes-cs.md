---
uid: web-forms/overview/ajax-control-toolkit/mutuallyexclusivecheckbox/creating-mutually-exclusive-checkboxes-cs
title: 相互排他的なチェックC#ボックスを作成する () |Microsoft Docs
author: wenz
description: 選択できるオプションのセットが1つだけの場合は、通常、ラジオボタンが使用されます。 ただし、グループ内の1つのオプションボタンが選択されると、欠点があり,...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 8e11b813-ba0d-4c29-b0f8-f65db6dbef1e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/mutuallyexclusivecheckbox/creating-mutually-exclusive-checkboxes-cs
msc.type: authoredcontent
ms.openlocfilehash: ddc154601752cc856f00dd4f3207952ab7e0e3e0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78496786"
---
# <a name="creating-mutually-exclusive-checkboxes-c"></a><span data-ttu-id="3cb22-104">相互に排他的なチェックボックスを作成する (C#)</span><span class="sxs-lookup"><span data-stu-id="3cb22-104">Creating Mutually Exclusive Checkboxes (C#)</span></span>

<span data-ttu-id="3cb22-105">[Christian Wenz](https://github.com/wenz)別</span><span class="sxs-lookup"><span data-stu-id="3cb22-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="3cb22-106">[コードのダウンロード](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/MutuallyExclusiveCheckBox0.cs.zip)または[PDF のダウンロード](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/mutuallyexclusivecheckbox0CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="3cb22-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/MutuallyExclusiveCheckBox0.cs.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/mutuallyexclusivecheckbox0CS.pdf)</span></span>

> <span data-ttu-id="3cb22-107">選択できるオプションのセットが1つだけの場合は、通常、ラジオボタンが使用されます。</span><span class="sxs-lookup"><span data-stu-id="3cb22-107">When only one of a set of options may be selected, radio buttons are usually used.</span></span> <span data-ttu-id="3cb22-108">ただし、欠点があります。グループ内の1つのラジオボタンを選択すると、すべてのラジオボタンをオフにすることはできません。</span><span class="sxs-lookup"><span data-stu-id="3cb22-108">There is a drawback, though: Once one radio button in a group is selected, it is not possible to uncheck all radio buttons.</span></span> <span data-ttu-id="3cb22-109">チェックボックスは、いつでもオフにすることができますが、相互に排他的ではありません。</span><span class="sxs-lookup"><span data-stu-id="3cb22-109">Check boxes can be unchecked at any time, however are not mutually exclusive.</span></span> <span data-ttu-id="3cb22-110">このチュートリアルでは、2つのアプローチ (相互に排他的なチェックボックス) について説明します。</span><span class="sxs-lookup"><span data-stu-id="3cb22-110">This tutorial provides the best of both approaches: check boxes that are mutually exclusive.</span></span>

## <a name="overview"></a><span data-ttu-id="3cb22-111">概要</span><span class="sxs-lookup"><span data-stu-id="3cb22-111">Overview</span></span>

<span data-ttu-id="3cb22-112">選択できるオプションのセットが1つだけの場合は、通常、ラジオボタンが使用されます。</span><span class="sxs-lookup"><span data-stu-id="3cb22-112">When only one of a set of options may be selected, radio buttons are usually used.</span></span> <span data-ttu-id="3cb22-113">ただし、欠点があります。グループ内の1つのラジオボタンを選択すると、すべてのラジオボタンをオフにすることはできません。</span><span class="sxs-lookup"><span data-stu-id="3cb22-113">There is a drawback, though: Once one radio button in a group is selected, it is not possible to uncheck all radio buttons.</span></span> <span data-ttu-id="3cb22-114">チェックボックスは、いつでもオフにすることができますが、相互に排他的ではありません。</span><span class="sxs-lookup"><span data-stu-id="3cb22-114">Check boxes can be unchecked at any time, however are not mutually exclusive.</span></span> <span data-ttu-id="3cb22-115">このチュートリアルでは、2つのアプローチ (相互に排他的なチェックボックス) について説明します。</span><span class="sxs-lookup"><span data-stu-id="3cb22-115">This tutorial provides the best of both approaches: check boxes that are mutually exclusive.</span></span>

## <a name="steps"></a><span data-ttu-id="3cb22-116">手順</span><span class="sxs-lookup"><span data-stu-id="3cb22-116">Steps</span></span>

<span data-ttu-id="3cb22-117">ASP.NET AJAX Control Toolkit には、MutuallyExclusiveCheckBox extender が含まれています。</span><span class="sxs-lookup"><span data-stu-id="3cb22-117">The ASP.NET AJAX Control Toolkit contains the MutuallyExclusiveCheckBox extender.</span></span> <span data-ttu-id="3cb22-118">これにより、プログラマは任意のチェックボックスをグループ名 (`Key` 属性) に割り当てることができます。</span><span class="sxs-lookup"><span data-stu-id="3cb22-118">This enables programmers to assign any checkbox to a group name (`Key` attribute).</span></span> <span data-ttu-id="3cb22-119">同じグループ内のすべてのチェックボックスから、一度に選択できるのは1つだけです。</span><span class="sxs-lookup"><span data-stu-id="3cb22-119">From all check boxes within the same group, only one may be selected at one time.</span></span>

<span data-ttu-id="3cb22-120">2つのチェックボックスを新しい ASP.NET ページに配置してみましょう。</span><span class="sxs-lookup"><span data-stu-id="3cb22-120">Let's start with putting two check boxes on a new ASP.NET page.</span></span> <span data-ttu-id="3cb22-121">多くの場合もありますが、そのうちの2つは、原則を示すのに十分です。</span><span class="sxs-lookup"><span data-stu-id="3cb22-121">There can be more, but two of them suffice to demonstrate the principle:</span></span>

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-cs/samples/sample1.aspx)]

<span data-ttu-id="3cb22-122">両方のチェックボックスについて、MutuallyExclusiveCheckBoxExtender コントロールをページに配置する必要があります。</span><span class="sxs-lookup"><span data-stu-id="3cb22-122">For both checkboxes, a MutuallyExclusiveCheckBoxExtender control must be put on the page.</span></span> <span data-ttu-id="3cb22-123">両方のキー属性は、同じ値を持つ必要があります。これは、HTML ラジオボタン要素の値属性が所属するグループを示すのと同じである必要があるためです。</span><span class="sxs-lookup"><span data-stu-id="3cb22-123">Both Key attributes need to have the same value, just as the value attributes of HTML radio button elements must be identical to denote the group they belong to.</span></span> <span data-ttu-id="3cb22-124">エクステンダーの TargetControlID プロパティは、チェックボックスの ID を指します。</span><span class="sxs-lookup"><span data-stu-id="3cb22-124">The TargetControlID property of the extender points to the ID of the check box.</span></span>

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-cs/samples/sample2.aspx)]

<span data-ttu-id="3cb22-125">最後に、ASP.NET AJAX Control Toolkit のすべての要素に必要な ASP.NET AJAX `ScriptManager` を含めます。</span><span class="sxs-lookup"><span data-stu-id="3cb22-125">Finally, include the ASP.NET AJAX `ScriptManager` which is required by all elements of the ASP.NET AJAX Control Toolkit:</span></span>

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-cs/samples/sample3.aspx)]

<span data-ttu-id="3cb22-126">ページを保存して実行する: 両方のチェックボックスをオンまたはオフにできますが、両方のチェックボックスをオンにすることはできません。</span><span class="sxs-lookup"><span data-stu-id="3cb22-126">Save and run the page: You can check and uncheck both check boxes, however at no time can both check boxes be checked.</span></span>

<span data-ttu-id="3cb22-127">[一度にチェックできるチェックボックスは1つだけ ![](creating-mutually-exclusive-checkboxes-cs/_static/image2.png)](creating-mutually-exclusive-checkboxes-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="3cb22-127">[![Only one checkbox can be checked at a time](creating-mutually-exclusive-checkboxes-cs/_static/image2.png)](creating-mutually-exclusive-checkboxes-cs/_static/image1.png)</span></span>

<span data-ttu-id="3cb22-128">チェックボックスは一度に1つしかチェックできません ([クリックすると、フルサイズの画像が表示](creating-mutually-exclusive-checkboxes-cs/_static/image3.png)されます)</span><span class="sxs-lookup"><span data-stu-id="3cb22-128">Only one checkbox can be checked at a time ([Click to view full-size image](creating-mutually-exclusive-checkboxes-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="3cb22-129">Next</span><span class="sxs-lookup"><span data-stu-id="3cb22-129">Next</span></span>](creating-mutually-exclusive-checkboxes-vb.md)
