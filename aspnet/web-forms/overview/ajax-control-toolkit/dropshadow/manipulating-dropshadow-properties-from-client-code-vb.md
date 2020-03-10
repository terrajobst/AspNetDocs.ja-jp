---
uid: web-forms/overview/ajax-control-toolkit/dropshadow/manipulating-dropshadow-properties-from-client-code-vb
title: クライアントコードから DropShadow プロパティを操作する (VB) |Microsoft Docs
author: wenz
description: AJAX コントロールツールキットの DropShadow コントロールは、ドロップシャドウを持つパネルを拡張します。 このエクステンダーのプロパティは、クライアント呼び出しを使用して変更することもできます。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 11be4211-2fb9-4e15-b6d4-2aa623d81f3e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dropshadow/manipulating-dropshadow-properties-from-client-code-vb
msc.type: authoredcontent
ms.openlocfilehash: a39adb9c06819f6f828add7d762effad430b8570
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78497410"
---
# <a name="manipulating-dropshadow-properties-from-client-code-vb"></a><span data-ttu-id="34438-104">クライアント コードから DropShadow プロパティを操作する (VB)</span><span class="sxs-lookup"><span data-stu-id="34438-104">Manipulating DropShadow Properties from Client Code (VB)</span></span>

<span data-ttu-id="34438-105">[Christian Wenz](https://github.com/wenz)別</span><span class="sxs-lookup"><span data-stu-id="34438-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="34438-106">[コードのダウンロード](https://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow2.vb.zip)または[PDF のダウンロード](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow2VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="34438-106">[Download Code](https://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow2.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow2VB.pdf)</span></span>

> <span data-ttu-id="34438-107">AJAX コントロールツールキットの DropShadow コントロールは、ドロップシャドウを持つパネルを拡張します。</span><span class="sxs-lookup"><span data-stu-id="34438-107">The DropShadow control in the AJAX Control Toolkit extends a panel with a drop shadow.</span></span> <span data-ttu-id="34438-108">このエクステンダーのプロパティは、クライアントの JavaScript コードを使用して変更することもできます。</span><span class="sxs-lookup"><span data-stu-id="34438-108">Properties of this extender can also be changed using client JavaScript code.</span></span>

## <a name="overview"></a><span data-ttu-id="34438-109">概要</span><span class="sxs-lookup"><span data-stu-id="34438-109">Overview</span></span>

<span data-ttu-id="34438-110">AJAX コントロールツールキットの DropShadow コントロールは、ドロップシャドウを持つパネルを拡張します。</span><span class="sxs-lookup"><span data-stu-id="34438-110">The DropShadow control in the AJAX Control Toolkit extends a panel with a drop shadow.</span></span> <span data-ttu-id="34438-111">このエクステンダーのプロパティは、クライアントの JavaScript コードを使用して変更することもできます。</span><span class="sxs-lookup"><span data-stu-id="34438-111">Properties of this extender can also be changed using client JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="34438-112">手順</span><span class="sxs-lookup"><span data-stu-id="34438-112">Steps</span></span>

<span data-ttu-id="34438-113">コードは、次のようなテキスト行を含むパネルから始まります。</span><span class="sxs-lookup"><span data-stu-id="34438-113">The code starts with a panel containing some lines of text:</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample1.aspx)]

<span data-ttu-id="34438-114">関連付けられている CSS クラスは、パネルに優れた背景色を与えます。</span><span class="sxs-lookup"><span data-stu-id="34438-114">The associated CSS class gives the panel a nice background color:</span></span>

[!code-css[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample2.css)]

<span data-ttu-id="34438-115">ドロップシャドウ効果を設定し、不透明度を50% に設定して、パネルを拡張する `DropShadowExtender` が追加されます。</span><span class="sxs-lookup"><span data-stu-id="34438-115">The `DropShadowExtender` is added to extend the panel with a drop shadow effect, opacity set to 50%:</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample3.aspx)]

<span data-ttu-id="34438-116">次に、ASP.NET AJAX `ScriptManager` コントロールを使用して、コントロールツールキットを機能させることができます。</span><span class="sxs-lookup"><span data-stu-id="34438-116">Then, the ASP.NET AJAX `ScriptManager` control enables the Control Toolkit to work:</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample4.aspx)]

<span data-ttu-id="34438-117">別のパネルには、ドロップシャドウの不透明度を設定するための JavaScript リンクが2つあります。マイナスリンクを使用すると影の不透明度が下がり、プラスリンクを使用すると、影の不透明度が上がります。</span><span class="sxs-lookup"><span data-stu-id="34438-117">Another panel contains two JavaScript links for setting the opacity of the drop shadow: the minus link decreases the shadow's opacity, the plus link increases it.</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample5.aspx)]

<span data-ttu-id="34438-118">JavaScript 関数 `changeOpacity()` は、まずページの `DropShadowExtender` コントロールを検索する必要があります。</span><span class="sxs-lookup"><span data-stu-id="34438-118">The JavaScript function `changeOpacity()` must then first find the `DropShadowExtender` control on the page.</span></span> <span data-ttu-id="34438-119">ASP.NET AJAX は、そのタスクの `$find()` メソッドを定義します。</span><span class="sxs-lookup"><span data-stu-id="34438-119">ASP.NET AJAX defines the `$find()` method for exactly that task.</span></span> <span data-ttu-id="34438-120">次に、`get_Opacity()` メソッドは現在の不透明度を取得し、`set_Opacity()` メソッドはそれを設定します。</span><span class="sxs-lookup"><span data-stu-id="34438-120">Then, the `get_Opacity()` method retrieves the current opacity, the `set_Opacity()` method sets it.</span></span> <span data-ttu-id="34438-121">次に、JavaScript コードによって、現在の不透明度の値が `<label>` 要素に配置されます。</span><span class="sxs-lookup"><span data-stu-id="34438-121">The JavaScript code then puts the current opacity value in the `<label>` element:</span></span>

[!code-html[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample6.html)]

<span data-ttu-id="34438-122">[不透明度がクライアント側で変更さ ![](manipulating-dropshadow-properties-from-client-code-vb/_static/image2.png)](manipulating-dropshadow-properties-from-client-code-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="34438-122">[![The opacity is changed on the client side](manipulating-dropshadow-properties-from-client-code-vb/_static/image2.png)](manipulating-dropshadow-properties-from-client-code-vb/_static/image1.png)</span></span>

<span data-ttu-id="34438-123">不透明度がクライアント側で変更されます ([クリックすると、フルサイズの画像が表示](manipulating-dropshadow-properties-from-client-code-vb/_static/image3.png)されます)</span><span class="sxs-lookup"><span data-stu-id="34438-123">The opacity is changed on the client side ([Click to view full-size image](manipulating-dropshadow-properties-from-client-code-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="34438-124">[[戻る]](adjusting-the-z-index-of-a-dropshadow-vb.md)</span><span class="sxs-lookup"><span data-stu-id="34438-124">[Previous](adjusting-the-z-index-of-a-dropshadow-vb.md)</span></span>
