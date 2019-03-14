---
uid: web-forms/overview/ajax-control-toolkit/accordion/dynamically-adding-an-accordion-pane-cs
title: 動的に追加する、アコーディオン ウィンドウ (c#) |Microsoft Docs
author: wenz
description: AJAX Control Toolkit で、アコーディオン コントロールは、複数のペインを示し、うち 1 つを同時に表示できます。 パネルには、w を宣言は、通常は.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 66d88cfa-f26f-46b1-ad52-1c9e03c04a48
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/accordion/dynamically-adding-an-accordion-pane-cs
msc.type: authoredcontent
ms.openlocfilehash: 16cefadb7086a658b20558526757f9229a43fcc9
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57027309"
---
<a name="dynamically-adding-an-accordion-pane-c"></a><span data-ttu-id="5caf3-104">アコーディオン ウィンドウでは (c#) を動的に追加します。</span><span class="sxs-lookup"><span data-stu-id="5caf3-104">Dynamically Adding An Accordion Pane (C#)</span></span>
====================
<span data-ttu-id="5caf3-105">によって[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="5caf3-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="5caf3-106">[コードのダウンロード](http://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion2.cs.zip)または[PDF のダウンロード](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion2CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="5caf3-106">[Download Code](http://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion2.cs.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion2CS.pdf)</span></span>

> <span data-ttu-id="5caf3-107">AJAX Control Toolkit で、アコーディオン コントロールは、複数のペインを示し、うち 1 つを同時に表示できます。</span><span class="sxs-lookup"><span data-stu-id="5caf3-107">The Accordion control in the AJAX Control Toolkit provides multiple panes and allows the user to display one of them at a time.</span></span> <span data-ttu-id="5caf3-108">パネルがページ自体には、通常は宣言されているが、サーバー側のコードは、同じ結果を実現するために使用できます。</span><span class="sxs-lookup"><span data-stu-id="5caf3-108">Panels are usually declared within the page itself, but server-side code can be used to achieve the same result.</span></span>


## <a name="overview"></a><span data-ttu-id="5caf3-109">概要</span><span class="sxs-lookup"><span data-stu-id="5caf3-109">Overview</span></span>

<span data-ttu-id="5caf3-110">AJAX Control Toolkit で、アコーディオン コントロールは、複数のペインを示し、うち 1 つを同時に表示できます。</span><span class="sxs-lookup"><span data-stu-id="5caf3-110">The Accordion control in the AJAX Control Toolkit provides multiple panes and allows the user to display one of them at a time.</span></span> <span data-ttu-id="5caf3-111">パネルがページ自体には、通常は宣言されているが、サーバー側のコードは、同じ結果を実現するために使用できます。</span><span class="sxs-lookup"><span data-stu-id="5caf3-111">Panels are usually declared within the page itself, but server-side code can be used to achieve the same result.</span></span>

## <a name="steps"></a><span data-ttu-id="5caf3-112">手順</span><span class="sxs-lookup"><span data-stu-id="5caf3-112">Steps</span></span>

<span data-ttu-id="5caf3-113">アコーディオン コントロールは、サーバー側コードをすべての重要なプロパティを公開します。</span><span class="sxs-lookup"><span data-stu-id="5caf3-113">The Accordion control exposes all important properties to server-side code.</span></span> <span data-ttu-id="5caf3-114">その他のもの、`Panes`プロパティは、アコーディオンを構成するペインのコレクションへのアクセスを許可します。</span><span class="sxs-lookup"><span data-stu-id="5caf3-114">Among other things, the `Panes` property grants access to the collection of panes that make up the Accordion.</span></span> <span data-ttu-id="5caf3-115">型のあるすべてのウィンドウ`AccordionPane`します。</span><span class="sxs-lookup"><span data-stu-id="5caf3-115">Every pane there is of type `AccordionPane`.</span></span> <span data-ttu-id="5caf3-116">このようなウィンドウを作成する単純なしたがって。</span><span class="sxs-lookup"><span data-stu-id="5caf3-116">It is therefore trivial to create such a pane:</span></span>

[!code-csharp[Main](dynamically-adding-an-accordion-pane-cs/samples/sample1.cs)]

<span data-ttu-id="5caf3-117">`HeaderContainer`プロパティの`AccordionPane`; ウィンドウのヘッダー セクション内の ASP.NET コントロールへのアクセスを提供します、`ContentContainer`プロパティの`AccordionPane`ウィンドウのコンテンツ セクションに対しても同様です。</span><span class="sxs-lookup"><span data-stu-id="5caf3-117">The `HeaderContainer` property of `AccordionPane` provides access to the ASP.NET controls within the header section of the pane; the `ContentContainer` property of `AccordionPane` does the same for the content section of the pane.</span></span> <span data-ttu-id="5caf3-118">これにより、ASP.NET コード ウィンドウにコンテンツを追加します。</span><span class="sxs-lookup"><span data-stu-id="5caf3-118">This allows ASP.NET code to add content to the panes:</span></span>

[!code-csharp[Main](dynamically-adding-an-accordion-pane-cs/samples/sample2.cs)]

<span data-ttu-id="5caf3-119">最後に、pane(s) に追加する必要があります、`Panes`アコーディオンのコレクション。</span><span class="sxs-lookup"><span data-stu-id="5caf3-119">Finally, the pane(s) must be added to the `Panes` collection of the Accordion:</span></span>

[!code-csharp[Main](dynamically-adding-an-accordion-pane-cs/samples/sample3.cs)]

<span data-ttu-id="5caf3-120">アコーディオン コントロールに 2 つのペインを追加します。 完全なサーバー側コードを次に示します。</span><span class="sxs-lookup"><span data-stu-id="5caf3-120">Here is a complete server-side code that adds two panes to an Accordion control:</span></span>

[!code-aspx[Main](dynamically-adding-an-accordion-pane-cs/samples/sample4.aspx)]

<span data-ttu-id="5caf3-121">唯一の要素がありませんが、ASP.NET の存在に依存する自体、アコーディオン`ScriptManager`コントロール。</span><span class="sxs-lookup"><span data-stu-id="5caf3-121">The only missing element is the Accordion itself, which depends on the presence of the ASP.NET `ScriptManager` control:</span></span>

[!code-aspx[Main](dynamically-adding-an-accordion-pane-cs/samples/sample5.aspx)]

<span data-ttu-id="5caf3-122">例を完了するには、アコーディオン コントロールで参照されている 2 つの CSS クラスは、ブラウザーのスタイル情報を提供します。</span><span class="sxs-lookup"><span data-stu-id="5caf3-122">To finish the example, the two CSS classes referenced in the Accordion control provide style information for the browser:</span></span>

[!code-css[Main](dynamically-adding-an-accordion-pane-cs/samples/sample6.css)]


<span data-ttu-id="5caf3-123">[![アコーディオンにデータはサーバー側コードによって動的に追加されました](dynamically-adding-an-accordion-pane-cs/_static/image2.png)](dynamically-adding-an-accordion-pane-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="5caf3-123">[![The data in the accordion was dynamically added by server-side code](dynamically-adding-an-accordion-pane-cs/_static/image2.png)](dynamically-adding-an-accordion-pane-cs/_static/image1.png)</span></span>

<span data-ttu-id="5caf3-124">アコーディオンにデータはサーバー側コードによって動的に追加されました ([フルサイズの画像を表示する をクリックします](dynamically-adding-an-accordion-pane-cs/_static/image3.png))。</span><span class="sxs-lookup"><span data-stu-id="5caf3-124">The data in the accordion was dynamically added by server-side code ([Click to view full-size image](dynamically-adding-an-accordion-pane-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="5caf3-125">[前へ](databinding-to-an-accordion-cs.md)
> [次へ](databinding-to-an-accordion-vb.md)</span><span class="sxs-lookup"><span data-stu-id="5caf3-125">[Previous](databinding-to-an-accordion-cs.md)
[Next](databinding-to-an-accordion-vb.md)</span></span>
