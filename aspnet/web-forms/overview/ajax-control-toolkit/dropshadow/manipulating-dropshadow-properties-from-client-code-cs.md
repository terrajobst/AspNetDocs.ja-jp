---
uid: web-forms/overview/ajax-control-toolkit/dropshadow/manipulating-dropshadow-properties-from-client-code-cs
title: クライアントコードから DropShadow プロパティを操作C#する () |Microsoft Docs
author: wenz
description: DataList の編集インターフェイスのカスタマイズ
ms.author: riande
ms.date: 06/02/2008
ms.assetid: c83ca3e6-c0bf-4158-a166-40c1ab0f33da
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dropshadow/manipulating-dropshadow-properties-from-client-code-cs
msc.type: authoredcontent
ms.openlocfilehash: 790f0d881e43518600968d6c175d4eaa53d0e5f9
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74574087"
---
# <a name="manipulating-dropshadow-properties-from-client-code-c"></a><span data-ttu-id="54554-103">クライアント コードから DropShadow プロパティを操作する (C#)</span><span class="sxs-lookup"><span data-stu-id="54554-103">Manipulating DropShadow Properties from Client Code (C#)</span></span>

<span data-ttu-id="54554-104">[Christian Wenz](https://github.com/wenz)別</span><span class="sxs-lookup"><span data-stu-id="54554-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="54554-105">[コードのダウンロード](https://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow2.cs.zip)または[PDF のダウンロード](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow2CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="54554-105">[Download Code](https://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow2.cs.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow2CS.pdf)</span></span>

> <span data-ttu-id="54554-106">AJAX コントロールツールキットの DropShadow コントロールは、ドロップシャドウを持つパネルを拡張します。</span><span class="sxs-lookup"><span data-stu-id="54554-106">The DropShadow control in the AJAX Control Toolkit extends a panel with a drop shadow.</span></span> <span data-ttu-id="54554-107">このエクステンダーのプロパティは、クライアントの JavaScript コードを使用して変更することもできます。</span><span class="sxs-lookup"><span data-stu-id="54554-107">Properties of this extender can also be changed using client JavaScript code.</span></span>

## <a name="overview"></a><span data-ttu-id="54554-108">の概要</span><span class="sxs-lookup"><span data-stu-id="54554-108">Overview</span></span>

<span data-ttu-id="54554-109">AJAX コントロールツールキットの DropShadow コントロールは、ドロップシャドウを持つパネルを拡張します。</span><span class="sxs-lookup"><span data-stu-id="54554-109">The DropShadow control in the AJAX Control Toolkit extends a panel with a drop shadow.</span></span> <span data-ttu-id="54554-110">このエクステンダーのプロパティは、クライアントの JavaScript コードを使用して変更することもできます。</span><span class="sxs-lookup"><span data-stu-id="54554-110">Properties of this extender can also be changed using client JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="54554-111">手順</span><span class="sxs-lookup"><span data-stu-id="54554-111">Steps</span></span>

<span data-ttu-id="54554-112">コードは、次のようなテキスト行を含むパネルから始まります。</span><span class="sxs-lookup"><span data-stu-id="54554-112">The code starts with a panel containing some lines of text:</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample1.aspx)]

<span data-ttu-id="54554-113">関連付けられている CSS クラスは、パネルに優れた背景色を与えます。</span><span class="sxs-lookup"><span data-stu-id="54554-113">The associated CSS class gives the panel a nice background color:</span></span>

[!code-css[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample2.css)]

<span data-ttu-id="54554-114">ドロップシャドウ効果を設定し、不透明度を50% に設定して、パネルを拡張する `DropShadowExtender` が追加されます。</span><span class="sxs-lookup"><span data-stu-id="54554-114">The `DropShadowExtender` is added to extend the panel with a drop shadow effect, opacity set to 50%:</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample3.aspx)]

<span data-ttu-id="54554-115">次に、ASP.NET AJAX `ScriptManager` コントロールを使用して、コントロールツールキットを機能させることができます。</span><span class="sxs-lookup"><span data-stu-id="54554-115">Then, the ASP.NET AJAX `ScriptManager` control enables the Control Toolkit to work:</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample4.aspx)]

<span data-ttu-id="54554-116">別のパネルには、ドロップシャドウの不透明度を設定するための JavaScript リンクが2つあります。マイナスリンクを使用すると影の不透明度が下がり、プラスリンクを使用すると、影の不透明度が上がります。</span><span class="sxs-lookup"><span data-stu-id="54554-116">Another panel contains two JavaScript links for setting the opacity of the drop shadow: the minus link decreases the shadow's opacity, the plus link increases it.</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample5.aspx)]

<span data-ttu-id="54554-117">JavaScript 関数 `changeOpacity()` は、まずページの `DropShadowExtender` コントロールを検索する必要があります。</span><span class="sxs-lookup"><span data-stu-id="54554-117">The JavaScript function `changeOpacity()` must then first find the `DropShadowExtender` control on the page.</span></span> <span data-ttu-id="54554-118">ASP.NET AJAX は、そのタスクの `$find()` メソッドを定義します。</span><span class="sxs-lookup"><span data-stu-id="54554-118">ASP.NET AJAX defines the `$find()` method for exactly that task.</span></span> <span data-ttu-id="54554-119">次に、`get_Opacity()` メソッドは現在の不透明度を取得し、`set_Opacity()` メソッドはそれを設定します。</span><span class="sxs-lookup"><span data-stu-id="54554-119">Then, the `get_Opacity()` method retrieves the current opacity, the `set_Opacity()` method sets it.</span></span> <span data-ttu-id="54554-120">次に、JavaScript コードによって、現在の不透明度の値が `<label>` 要素に配置されます。</span><span class="sxs-lookup"><span data-stu-id="54554-120">The JavaScript code then puts the current opacity value in the `<label>` element:</span></span>

[!code-html[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample6.html)]

<span data-ttu-id="54554-121">[不透明度がクライアント側で変更さ ![](manipulating-dropshadow-properties-from-client-code-cs/_static/image2.png)](manipulating-dropshadow-properties-from-client-code-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="54554-121">[![The opacity is changed on the client side](manipulating-dropshadow-properties-from-client-code-cs/_static/image2.png)](manipulating-dropshadow-properties-from-client-code-cs/_static/image1.png)</span></span>

<span data-ttu-id="54554-122">不透明度がクライアント側で変更されます ([クリックすると、フルサイズの画像が表示](manipulating-dropshadow-properties-from-client-code-cs/_static/image3.png)されます)</span><span class="sxs-lookup"><span data-stu-id="54554-122">The opacity is changed on the client side ([Click to view full-size image](manipulating-dropshadow-properties-from-client-code-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="54554-123">[前へ](adjusting-the-z-index-of-a-dropshadow-cs.md)
> [次へ](adjusting-the-z-index-of-a-dropshadow-vb.md)</span><span class="sxs-lookup"><span data-stu-id="54554-123">[Previous](adjusting-the-z-index-of-a-dropshadow-cs.md)
[Next](adjusting-the-z-index-of-a-dropshadow-vb.md)</span></span>
