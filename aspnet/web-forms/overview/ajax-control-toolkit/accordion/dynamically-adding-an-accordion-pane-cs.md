---
uid: web-forms/overview/ajax-control-toolkit/accordion/dynamically-adding-an-accordion-pane-cs
title: アコーディオンペインを動的に追加C#する () |Microsoft Docs
author: wenz
description: AJAX コントロールツールキットのアコーディオンコントロールは、複数のウィンドウを提供し、ユーザーが一度に1つずつ表示できるようにします。 通常、パネルは...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 66d88cfa-f26f-46b1-ad52-1c9e03c04a48
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/accordion/dynamically-adding-an-accordion-pane-cs
msc.type: authoredcontent
ms.openlocfilehash: 2834f56bd77c412923f4a8f382e670727f70eae4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78497980"
---
# <a name="dynamically-adding-an-accordion-pane-c"></a><span data-ttu-id="3948e-104">アコーディオンウィンドウを動的に追加C#する ()</span><span class="sxs-lookup"><span data-stu-id="3948e-104">Dynamically Adding An Accordion Pane (C#)</span></span>

<span data-ttu-id="3948e-105">[Christian Wenz](https://github.com/wenz)別</span><span class="sxs-lookup"><span data-stu-id="3948e-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="3948e-106">[コードのダウンロード](https://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion2.cs.zip)または[PDF のダウンロード](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion2CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="3948e-106">[Download Code](https://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion2.cs.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion2CS.pdf)</span></span>

> <span data-ttu-id="3948e-107">AJAX コントロールツールキットのアコーディオンコントロールは、複数のウィンドウを提供し、ユーザーが一度に1つずつ表示できるようにします。</span><span class="sxs-lookup"><span data-stu-id="3948e-107">The Accordion control in the AJAX Control Toolkit provides multiple panes and allows the user to display one of them at a time.</span></span> <span data-ttu-id="3948e-108">通常、パネルはページ内で宣言されますが、サーバー側のコードを使用して同じ結果を得ることができます。</span><span class="sxs-lookup"><span data-stu-id="3948e-108">Panels are usually declared within the page itself, but server-side code can be used to achieve the same result.</span></span>

## <a name="overview"></a><span data-ttu-id="3948e-109">概要</span><span class="sxs-lookup"><span data-stu-id="3948e-109">Overview</span></span>

<span data-ttu-id="3948e-110">AJAX コントロールツールキットのアコーディオンコントロールは、複数のウィンドウを提供し、ユーザーが一度に1つずつ表示できるようにします。</span><span class="sxs-lookup"><span data-stu-id="3948e-110">The Accordion control in the AJAX Control Toolkit provides multiple panes and allows the user to display one of them at a time.</span></span> <span data-ttu-id="3948e-111">通常、パネルはページ内で宣言されますが、サーバー側のコードを使用して同じ結果を得ることができます。</span><span class="sxs-lookup"><span data-stu-id="3948e-111">Panels are usually declared within the page itself, but server-side code can be used to achieve the same result.</span></span>

## <a name="steps"></a><span data-ttu-id="3948e-112">手順</span><span class="sxs-lookup"><span data-stu-id="3948e-112">Steps</span></span>

<span data-ttu-id="3948e-113">アコーディオンコントロールは、すべての重要なプロパティをサーバー側のコードに公開します。</span><span class="sxs-lookup"><span data-stu-id="3948e-113">The Accordion control exposes all important properties to server-side code.</span></span> <span data-ttu-id="3948e-114">特に、`Panes` プロパティは、アコーディオンを構成するペインのコレクションへのアクセスを許可します。</span><span class="sxs-lookup"><span data-stu-id="3948e-114">Among other things, the `Panes` property grants access to the collection of panes that make up the Accordion.</span></span> <span data-ttu-id="3948e-115">すべてのウィンドウには `AccordionPane`型があります。</span><span class="sxs-lookup"><span data-stu-id="3948e-115">Every pane there is of type `AccordionPane`.</span></span> <span data-ttu-id="3948e-116">そのため、このようなペインを作成するのは簡単です。</span><span class="sxs-lookup"><span data-stu-id="3948e-116">It is therefore trivial to create such a pane:</span></span>

[!code-csharp[Main](dynamically-adding-an-accordion-pane-cs/samples/sample1.cs)]

<span data-ttu-id="3948e-117">`AccordionPane` の `HeaderContainer` プロパティは、ペインのヘッダーセクション内の ASP.NET コントロールへのアクセスを提供します。`AccordionPane` の `ContentContainer` プロパティは、ペインのコンテンツセクションでも同じです。</span><span class="sxs-lookup"><span data-stu-id="3948e-117">The `HeaderContainer` property of `AccordionPane` provides access to the ASP.NET controls within the header section of the pane; the `ContentContainer` property of `AccordionPane` does the same for the content section of the pane.</span></span> <span data-ttu-id="3948e-118">これにより、ASP.NET コードで、ウィンドウにコンテンツを追加できます。</span><span class="sxs-lookup"><span data-stu-id="3948e-118">This allows ASP.NET code to add content to the panes:</span></span>

[!code-csharp[Main](dynamically-adding-an-accordion-pane-cs/samples/sample2.cs)]

<span data-ttu-id="3948e-119">最後に、ウィンドウをアコーディオンの `Panes` コレクションに追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="3948e-119">Finally, the pane(s) must be added to the `Panes` collection of the Accordion:</span></span>

[!code-csharp[Main](dynamically-adding-an-accordion-pane-cs/samples/sample3.cs)]

<span data-ttu-id="3948e-120">次に示すのは、アコーディオンコントロールに2つのペインを追加する完全なサーバー側コードです。</span><span class="sxs-lookup"><span data-stu-id="3948e-120">Here is a complete server-side code that adds two panes to an Accordion control:</span></span>

[!code-aspx[Main](dynamically-adding-an-accordion-pane-cs/samples/sample4.aspx)]

<span data-ttu-id="3948e-121">見つからない要素は、ASP.NET `ScriptManager` コントロールの存在に応じて、アコーディオン自体だけです。</span><span class="sxs-lookup"><span data-stu-id="3948e-121">The only missing element is the Accordion itself, which depends on the presence of the ASP.NET `ScriptManager` control:</span></span>

[!code-aspx[Main](dynamically-adding-an-accordion-pane-cs/samples/sample5.aspx)]

<span data-ttu-id="3948e-122">この例を完了するために、アコーディオンコントロールで参照される2つの CSS クラスでブラウザーのスタイル情報が提供されます。</span><span class="sxs-lookup"><span data-stu-id="3948e-122">To finish the example, the two CSS classes referenced in the Accordion control provide style information for the browser:</span></span>

[!code-css[Main](dynamically-adding-an-accordion-pane-cs/samples/sample6.css)]

<span data-ttu-id="3948e-123">[サーバー側のコードによって、アコーディオン内のデータが動的に追加された ![](dynamically-adding-an-accordion-pane-cs/_static/image2.png)](dynamically-adding-an-accordion-pane-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="3948e-123">[![The data in the accordion was dynamically added by server-side code](dynamically-adding-an-accordion-pane-cs/_static/image2.png)](dynamically-adding-an-accordion-pane-cs/_static/image1.png)</span></span>

<span data-ttu-id="3948e-124">アコーディオン内のデータはサーバー側のコードによって動的に追加されました ([クリックすると、フルサイズの画像が表示](dynamically-adding-an-accordion-pane-cs/_static/image3.png)されます)</span><span class="sxs-lookup"><span data-stu-id="3948e-124">The data in the accordion was dynamically added by server-side code ([Click to view full-size image](dynamically-adding-an-accordion-pane-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="3948e-125">[前へ](databinding-to-an-accordion-cs.md)
> [次へ](databinding-to-an-accordion-vb.md)</span><span class="sxs-lookup"><span data-stu-id="3948e-125">[Previous](databinding-to-an-accordion-cs.md)
[Next](databinding-to-an-accordion-vb.md)</span></span>
