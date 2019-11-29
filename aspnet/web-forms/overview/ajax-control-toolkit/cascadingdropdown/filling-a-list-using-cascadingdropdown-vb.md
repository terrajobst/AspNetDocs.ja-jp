---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/filling-a-list-using-cascadingdropdown-vb
title: CascadingDropDown を使用してリストに入力する (VB) |Microsoft Docs
author: wenz
description: AJAX コントロールツールキットの CascadingDropDown コントロールは、dropdownlist コントロールを拡張して、1つの DropDownList の変更によって anoth に関連付けられた値が読み込まれるようにします。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 5236695e-5c70-4887-baee-0bfb0afb3448
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/filling-a-list-using-cascadingdropdown-vb
msc.type: authoredcontent
ms.openlocfilehash: 8dd9ef8a4bdf705ba4451b7fd240e4de8618221c
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599579"
---
# <a name="filling-a-list-using-cascadingdropdown-vb"></a><span data-ttu-id="5f4e2-103">CascadingDropDown を使用して一覧に入力する (VB)</span><span class="sxs-lookup"><span data-stu-id="5f4e2-103">Filling a List Using CascadingDropDown (VB)</span></span>

<span data-ttu-id="5f4e2-104">[Christian Wenz](https://github.com/wenz)別</span><span class="sxs-lookup"><span data-stu-id="5f4e2-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="5f4e2-105">[コードのダウンロード](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown0.vb.zip)または[PDF のダウンロード](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown0VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="5f4e2-105">[Download Code](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown0.vb.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown0VB.pdf)</span></span>

> <span data-ttu-id="5f4e2-106">AJAX コントロールツールキットの CascadingDropDown コントロールは、dropdownlist コントロールを拡張して、1つの DropDownList の変更によって別の DropDownList に関連付けられた値が読み込まれるようにします。</span><span class="sxs-lookup"><span data-stu-id="5f4e2-106">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="5f4e2-107">(たとえば、1つのリストに米国の州の一覧が表示され、その州の主要都市が次の一覧に入力されます)。最初の問題は、このコントロールを使用して、ドロップダウンリストに実際に入力することです。</span><span class="sxs-lookup"><span data-stu-id="5f4e2-107">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) The first challenge to solve is to actually fill a dropdown list using this control.</span></span>

## <a name="overview"></a><span data-ttu-id="5f4e2-108">の概要</span><span class="sxs-lookup"><span data-stu-id="5f4e2-108">Overview</span></span>

<span data-ttu-id="5f4e2-109">AJAX コントロールツールキットの CascadingDropDown コントロールは、dropdownlist コントロールを拡張して、1つの DropDownList の変更によって別の DropDownList に関連付けられた値が読み込まれるようにします。</span><span class="sxs-lookup"><span data-stu-id="5f4e2-109">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="5f4e2-110">(たとえば、1つのリストに米国の州の一覧が表示され、その州の主要都市が次の一覧に入力されます)。最初の問題は、このコントロールを使用して、ドロップダウンリストに実際に入力することです。</span><span class="sxs-lookup"><span data-stu-id="5f4e2-110">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) The first challenge to solve is to actually fill a dropdown list using this control.</span></span>

## <a name="steps"></a><span data-ttu-id="5f4e2-111">手順</span><span class="sxs-lookup"><span data-stu-id="5f4e2-111">Steps</span></span>

<span data-ttu-id="5f4e2-112">ASP.NET AJAX と Control Toolkit の機能をアクティブ化するには、ページの任意の場所に `ScriptManager` コントロールを配置する必要があります (`<form>` 要素内)。</span><span class="sxs-lookup"><span data-stu-id="5f4e2-112">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample1.aspx)]

<span data-ttu-id="5f4e2-113">次に、DropDownList コントロールが必要です。</span><span class="sxs-lookup"><span data-stu-id="5f4e2-113">Then, a DropDownList control is required:</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample2.aspx)]

<span data-ttu-id="5f4e2-114">この一覧では、CascadingDropDown extender が追加されます。</span><span class="sxs-lookup"><span data-stu-id="5f4e2-114">For this list, a CascadingDropDown extender is added.</span></span> <span data-ttu-id="5f4e2-115">非同期要求が web サービスに送信され、リストに表示されるエントリの一覧が返されます。</span><span class="sxs-lookup"><span data-stu-id="5f4e2-115">It will send an asynchronous request to a web service which will then return a list of entries to be displayed in the list.</span></span> <span data-ttu-id="5f4e2-116">これを機能させるには、次の CascadingDropDown 属性を設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5f4e2-116">For this to work, the following CascadingDropDown attributes need to be set:</span></span>

- <span data-ttu-id="5f4e2-117">`ServicePath`: リストエントリを提供する web サービスの URL</span><span class="sxs-lookup"><span data-stu-id="5f4e2-117">`ServicePath`: URL of a web service delivering the list entries</span></span>
- <span data-ttu-id="5f4e2-118">`ServiceMethod`: リストエントリを配信する Web メソッド</span><span class="sxs-lookup"><span data-stu-id="5f4e2-118">`ServiceMethod`: Web method delivering the list entries</span></span>
- <span data-ttu-id="5f4e2-119">`TargetControlID`: ドロップダウンリストの ID</span><span class="sxs-lookup"><span data-stu-id="5f4e2-119">`TargetControlID`: ID of the dropdown list</span></span>
- <span data-ttu-id="5f4e2-120">`Category`: 呼び出されたときに web メソッドに送信されるカテゴリ情報</span><span class="sxs-lookup"><span data-stu-id="5f4e2-120">`Category`: Category information that is submitted to the web method when called</span></span>
- <span data-ttu-id="5f4e2-121">`PromptText`: サーバーからリストデータを非同期的に読み込むときに表示されるテキスト</span><span class="sxs-lookup"><span data-stu-id="5f4e2-121">`PromptText`: Text displayed when asynchronously loading list data from the server</span></span>

<span data-ttu-id="5f4e2-122">`CascadingDropDown` 要素のマークアップを次に示します。</span><span class="sxs-lookup"><span data-stu-id="5f4e2-122">Here is the markup for the `CascadingDropDown` element.</span></span> <span data-ttu-id="5f4e2-123">C#と VB の唯一の違いは、関連付けられた web サービスの名前です。</span><span class="sxs-lookup"><span data-stu-id="5f4e2-123">The only difference between C# and VB is the name of the associated web service:</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample3.aspx)]

<span data-ttu-id="5f4e2-124">`CascadingDropDown` エクステンダーからの JavaScript コードは、次のシグネチャを持つ web サービスメソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="5f4e2-124">The JavaScript code coming from the `CascadingDropDown` extender calls a web service method with the following signature:</span></span>

[!code-vb[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample4.vb)]

<span data-ttu-id="5f4e2-125">重要な点は、メソッドが `CascadingDropDownNameValue` 型の配列を返す必要があることです (ASP.NET AJAX Control Toolkit によって定義されています)。</span><span class="sxs-lookup"><span data-stu-id="5f4e2-125">So the important aspect is that the method needs to return an array of type `CascadingDropDownNameValue` (defined by the ASP.NET AJAX Control Toolkit).</span></span> <span data-ttu-id="5f4e2-126">`CascadingDropDownNameValue` コンストラクターでは、最初にリストエントリのテキストを入力し、次に HTML の場合 `<option value="VALUE">NAME</option>` と同様に値を指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5f4e2-126">In the `CascadingDropDownNameValue` constructor, first the list entry's text and then its value must be provided, just as `<option value="VALUE">NAME</option>` would do in HTML.</span></span> <span data-ttu-id="5f4e2-127">いくつかのサンプルデータを次に示します。</span><span class="sxs-lookup"><span data-stu-id="5f4e2-127">Here is some sample data:</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample5.aspx)]

<span data-ttu-id="5f4e2-128">ブラウザーにページを読み込むと、3つの仕入先がリストに入力されます。</span><span class="sxs-lookup"><span data-stu-id="5f4e2-128">Loading the page in the browser will trigger the list to be filled with three vendors.</span></span>

<span data-ttu-id="5f4e2-129">[リストが自動的に入力される ![](filling-a-list-using-cascadingdropdown-vb/_static/image2.png)](filling-a-list-using-cascadingdropdown-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="5f4e2-129">[![The list is filled automatically](filling-a-list-using-cascadingdropdown-vb/_static/image2.png)](filling-a-list-using-cascadingdropdown-vb/_static/image1.png)</span></span>

<span data-ttu-id="5f4e2-130">リストが自動的に入力されます ([クリックすると、フルサイズの画像が表示](filling-a-list-using-cascadingdropdown-vb/_static/image3.png)されます)</span><span class="sxs-lookup"><span data-stu-id="5f4e2-130">The list is filled automatically ([Click to view full-size image](filling-a-list-using-cascadingdropdown-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="5f4e2-131">[前へ](using-auto-postback-with-cascadingdropdown-cs.md)
> [次へ](using-cascadingdropdown-with-a-database-vb.md)</span><span class="sxs-lookup"><span data-stu-id="5f4e2-131">[Previous](using-auto-postback-with-cascadingdropdown-cs.md)
[Next](using-cascadingdropdown-with-a-database-vb.md)</span></span>
