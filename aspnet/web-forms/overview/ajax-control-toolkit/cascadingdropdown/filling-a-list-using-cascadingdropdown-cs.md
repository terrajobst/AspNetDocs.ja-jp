---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/filling-a-list-using-cascadingdropdown-cs
title: CascadingDropDown (C#) を使用してリストに入力するMicrosoft Docs
author: wenz
description: AJAX コントロールツールキットの CascadingDropDown コントロールは、dropdownlist コントロールを拡張して、1つの DropDownList の変更によって anoth に関連付けられた値が読み込まれるようにします。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: f949aafa-fe57-43b0-b722-f0dd33a900be
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/filling-a-list-using-cascadingdropdown-cs
msc.type: authoredcontent
ms.openlocfilehash: b5e9874fb5b6d3e55c8af5b85d12bf1ffacc116b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78497764"
---
# <a name="filling-a-list-using-cascadingdropdown-c"></a><span data-ttu-id="5452a-103">CascadingDropDown を使用して一覧に入力する (C#)</span><span class="sxs-lookup"><span data-stu-id="5452a-103">Filling a List Using CascadingDropDown (C#)</span></span>

<span data-ttu-id="5452a-104">[Christian Wenz](https://github.com/wenz)別</span><span class="sxs-lookup"><span data-stu-id="5452a-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="5452a-105">[コードのダウンロード](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown0.cs.zip)または[PDF のダウンロード](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown0CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="5452a-105">[Download Code](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown0.cs.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown0CS.pdf)</span></span>

> <span data-ttu-id="5452a-106">AJAX コントロールツールキットの CascadingDropDown コントロールは、dropdownlist コントロールを拡張して、1つの DropDownList の変更によって別の DropDownList に関連付けられた値が読み込まれるようにします。</span><span class="sxs-lookup"><span data-stu-id="5452a-106">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="5452a-107">(たとえば、1つのリストに米国の州の一覧が表示され、その州の主要都市が次の一覧に入力されます)。最初の問題は、このコントロールを使用して、ドロップダウンリストに実際に入力することです。</span><span class="sxs-lookup"><span data-stu-id="5452a-107">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) The first challenge to solve is to actually fill a dropdown list using this control.</span></span>

## <a name="overview"></a><span data-ttu-id="5452a-108">概要</span><span class="sxs-lookup"><span data-stu-id="5452a-108">Overview</span></span>

<span data-ttu-id="5452a-109">AJAX コントロールツールキットの CascadingDropDown コントロールは、dropdownlist コントロールを拡張して、1つの DropDownList の変更によって別の DropDownList に関連付けられた値が読み込まれるようにします。</span><span class="sxs-lookup"><span data-stu-id="5452a-109">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="5452a-110">(たとえば、1つのリストに米国の州の一覧が表示され、その州の主要都市が次の一覧に入力されます)。最初の問題は、このコントロールを使用して、ドロップダウンリストに実際に入力することです。</span><span class="sxs-lookup"><span data-stu-id="5452a-110">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) The first challenge to solve is to actually fill a dropdown list using this control.</span></span>

## <a name="steps"></a><span data-ttu-id="5452a-111">手順</span><span class="sxs-lookup"><span data-stu-id="5452a-111">Steps</span></span>

<span data-ttu-id="5452a-112">ASP.NET AJAX と Control Toolkit の機能をアクティブ化するには、ページの任意の場所に `ScriptManager` コントロールを配置する必要があります (`<form>` 要素内)。</span><span class="sxs-lookup"><span data-stu-id="5452a-112">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample1.aspx)]

<span data-ttu-id="5452a-113">次に、DropDownList コントロールが必要です。</span><span class="sxs-lookup"><span data-stu-id="5452a-113">Then, a DropDownList control is required:</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample2.aspx)]

<span data-ttu-id="5452a-114">この一覧では、CascadingDropDown extender が追加されます。</span><span class="sxs-lookup"><span data-stu-id="5452a-114">For this list, a CascadingDropDown extender is added.</span></span> <span data-ttu-id="5452a-115">非同期要求が web サービスに送信され、リストに表示されるエントリの一覧が返されます。</span><span class="sxs-lookup"><span data-stu-id="5452a-115">It will send an asynchronous request to a web service which will then return a list of entries to be displayed in the list.</span></span> <span data-ttu-id="5452a-116">これを機能させるには、次の CascadingDropDown 属性を設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5452a-116">For this to work, the following CascadingDropDown attributes need to be set:</span></span>

- <span data-ttu-id="5452a-117">`ServicePath`: リストエントリを提供する web サービスの URL</span><span class="sxs-lookup"><span data-stu-id="5452a-117">`ServicePath`: URL of a web service delivering the list entries</span></span>
- <span data-ttu-id="5452a-118">`ServiceMethod`: リストエントリを配信する Web メソッド</span><span class="sxs-lookup"><span data-stu-id="5452a-118">`ServiceMethod`: Web method delivering the list entries</span></span>
- <span data-ttu-id="5452a-119">`TargetControlID`: ドロップダウンリストの ID</span><span class="sxs-lookup"><span data-stu-id="5452a-119">`TargetControlID`: ID of the dropdown list</span></span>
- <span data-ttu-id="5452a-120">`Category`: 呼び出されたときに web メソッドに送信されるカテゴリ情報</span><span class="sxs-lookup"><span data-stu-id="5452a-120">`Category`: Category information that is submitted to the web method when called</span></span>
- <span data-ttu-id="5452a-121">`PromptText`: サーバーからリストデータを非同期的に読み込むときに表示されるテキスト</span><span class="sxs-lookup"><span data-stu-id="5452a-121">`PromptText`: Text displayed when asynchronously loading list data from the server</span></span>

<span data-ttu-id="5452a-122">`CascadingDropDown` 要素のマークアップを次に示します。</span><span class="sxs-lookup"><span data-stu-id="5452a-122">Here is the markup for the `CascadingDropDown` element.</span></span> <span data-ttu-id="5452a-123">C#と VB の唯一の違いは、関連付けられた web サービスの名前です。</span><span class="sxs-lookup"><span data-stu-id="5452a-123">The only difference between C# and VB is the name of the associated web service:</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample3.aspx)]

<span data-ttu-id="5452a-124">`CascadingDropDown` エクステンダーからの JavaScript コードは、次のシグネチャを持つ web サービスメソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="5452a-124">The JavaScript code coming from the `CascadingDropDown` extender calls a web service method with the following signature:</span></span>

[!code-csharp[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample4.cs)]

<span data-ttu-id="5452a-125">重要な点は、メソッドが `CascadingDropDownNameValue` 型の配列を返す必要があることです (ASP.NET AJAX Control Toolkit によって定義されています)。</span><span class="sxs-lookup"><span data-stu-id="5452a-125">So the important aspect is that the method needs to return an array of type `CascadingDropDownNameValue` (defined by the ASP.NET AJAX Control Toolkit).</span></span> <span data-ttu-id="5452a-126">`CascadingDropDownNameValue` コンストラクターでは、最初にリストエントリのテキストを入力し、次に HTML の場合 `<option value="VALUE">NAME</option>` と同様に値を指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5452a-126">In the `CascadingDropDownNameValue` constructor, first the list entry's text and then its value must be provided, just as `<option value="VALUE">NAME</option>` would do in HTML.</span></span> <span data-ttu-id="5452a-127">いくつかのサンプルデータを次に示します。</span><span class="sxs-lookup"><span data-stu-id="5452a-127">Here is some sample data:</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample5.aspx)]

<span data-ttu-id="5452a-128">ブラウザーにページを読み込むと、3つの仕入先がリストに入力されます。</span><span class="sxs-lookup"><span data-stu-id="5452a-128">Loading the page in the browser will trigger the list to be filled with three vendors.</span></span>

<span data-ttu-id="5452a-129">[リストが自動的に入力される ![](filling-a-list-using-cascadingdropdown-cs/_static/image2.png)](filling-a-list-using-cascadingdropdown-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="5452a-129">[![The list is filled automatically](filling-a-list-using-cascadingdropdown-cs/_static/image2.png)](filling-a-list-using-cascadingdropdown-cs/_static/image1.png)</span></span>

<span data-ttu-id="5452a-130">リストが自動的に入力されます ([クリックすると、フルサイズの画像が表示](filling-a-list-using-cascadingdropdown-cs/_static/image3.png)されます)</span><span class="sxs-lookup"><span data-stu-id="5452a-130">The list is filled automatically ([Click to view full-size image](filling-a-list-using-cascadingdropdown-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="5452a-131">Next</span><span class="sxs-lookup"><span data-stu-id="5452a-131">Next</span></span>](using-cascadingdropdown-with-a-database-cs.md)
