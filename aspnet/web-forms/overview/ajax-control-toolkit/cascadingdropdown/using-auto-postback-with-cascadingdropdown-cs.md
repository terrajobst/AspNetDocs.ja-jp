---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-auto-postback-with-cascadingdropdown-cs
title: CascadingDropDown (C#) で自動ポストバックを使用するMicrosoft Docs
author: wenz
description: AJAX コントロールツールキットの CascadingDropDown コントロールは、dropdownlist コントロールを拡張して、1つの DropDownList の変更によって anoth に関連付けられた値が読み込まれるようにします。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 6755d8d9-14be-4a1d-86e5-1a6110f3dea8
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-auto-postback-with-cascadingdropdown-cs
msc.type: authoredcontent
ms.openlocfilehash: 8bccd716814e7de544798010cecbc148ec50b5cd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78430684"
---
# <a name="using-auto-postback-with-cascadingdropdown-c"></a><span data-ttu-id="502e9-103">CascadingDropDown で自動ポストバックを使用する (C#)</span><span class="sxs-lookup"><span data-stu-id="502e9-103">Using Auto-Postback with CascadingDropDown (C#)</span></span>

<span data-ttu-id="502e9-104">[Christian Wenz](https://github.com/wenz)別</span><span class="sxs-lookup"><span data-stu-id="502e9-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="502e9-105">[コードのダウンロード](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown3.cs.zip)または[PDF のダウンロード](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown3CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="502e9-105">[Download Code](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown3.cs.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown3CS.pdf)</span></span>

> <span data-ttu-id="502e9-106">AJAX コントロールツールキットの CascadingDropDown コントロールは、dropdownlist コントロールを拡張して、1つの DropDownList の変更によって別の DropDownList に関連付けられた値が読み込まれるようにします。</span><span class="sxs-lookup"><span data-stu-id="502e9-106">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="502e9-107">ただし、CascadingDropDown コントロールを使用する場合は ASP を使用します。リストにデータを非同期で読み込むと (不要な) ポストバック自体が生成されるため、ネットワークの DropDownList コントロールの AutoPostBack 機能は機能しません。</span><span class="sxs-lookup"><span data-stu-id="502e9-107">However when using the CascadingDropDown control, ASP.NET's DropDownList control's AutoPostBack feature does not work, since asynchronously loading data into the list generates an (unnecessary) postback itself.</span></span> <span data-ttu-id="502e9-108">一部の JavaScript コードでは、この影響を回避できます。</span><span class="sxs-lookup"><span data-stu-id="502e9-108">With some JavaScript code, this effect can be avoided.</span></span>

## <a name="overview"></a><span data-ttu-id="502e9-109">概要</span><span class="sxs-lookup"><span data-stu-id="502e9-109">Overview</span></span>

<span data-ttu-id="502e9-110">AJAX コントロールツールキットの CascadingDropDown コントロールは、dropdownlist コントロールを拡張して、1つの DropDownList の変更によって別の DropDownList に関連付けられた値が読み込まれるようにします。</span><span class="sxs-lookup"><span data-stu-id="502e9-110">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="502e9-111">(たとえば、1つのリストに米国の州の一覧が表示され、その州の主要都市が次の一覧に入力されます)。ただし、CascadingDropDown コントロールを使用する場合は ASP を使用します。リストにデータを非同期で読み込むと (不要な) ポストバック自体が生成されるため、ネットワークの DropDownList コントロールの AutoPostBack 機能は機能しません。</span><span class="sxs-lookup"><span data-stu-id="502e9-111">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) However when using the CascadingDropDown control, ASP.NET's DropDownList control's AutoPostBack feature does not work, since asynchronously loading data into the list generates an (unnecessary) postback itself.</span></span> <span data-ttu-id="502e9-112">一部の JavaScript コードでは、この影響を回避できます。</span><span class="sxs-lookup"><span data-stu-id="502e9-112">With some JavaScript code, this effect can be avoided.</span></span>

## <a name="steps"></a><span data-ttu-id="502e9-113">手順</span><span class="sxs-lookup"><span data-stu-id="502e9-113">Steps</span></span>

<span data-ttu-id="502e9-114">ASP.NET AJAX と Control Toolkit の機能をアクティブ化するには、ページの任意の場所に `ScriptManager` コントロールを配置する必要があります (&lt;`form`&gt; 要素内)。</span><span class="sxs-lookup"><span data-stu-id="502e9-114">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the &lt;`form`&gt; element):</span></span>

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample1.aspx)]

<span data-ttu-id="502e9-115">次に、DropDownList コントロールが必要です。</span><span class="sxs-lookup"><span data-stu-id="502e9-115">Then, a DropDownList control is required:</span></span>

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample2.aspx)]

<span data-ttu-id="502e9-116">この一覧では、web サービスの URL とメソッドの情報を提供する CascadingDropDown extender が追加されます。</span><span class="sxs-lookup"><span data-stu-id="502e9-116">For this list, a CascadingDropDown extender is added, providing web service URL and method information:</span></span>

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample3.aspx)]

<span data-ttu-id="502e9-117">次に、CascadingDropDown extender は、次のメソッドシグネチャを使用して web サービスを非同期に呼び出します。</span><span class="sxs-lookup"><span data-stu-id="502e9-117">The CascadingDropDown extender then asynchronously calls a web service with the following method signature:</span></span>

[!code-csharp[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample4.cs)]

<span data-ttu-id="502e9-118">このメソッドは、CascadingDropDown value 型の配列を返します。</span><span class="sxs-lookup"><span data-stu-id="502e9-118">The method returns an array of type CascadingDropDown value.</span></span> <span data-ttu-id="502e9-119">型のコンストラクターは、最初にリストエントリのキャプションを受け取り、次に値 (HTML `value` 属性) を必要とします。</span><span class="sxs-lookup"><span data-stu-id="502e9-119">The type's constructor expects first the list entry's caption and then the value (HTML `value` attribute).</span></span>

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample5.aspx)]

<span data-ttu-id="502e9-120">ブラウザーにページを読み込むと、ドロップダウンリストに3つのベンダが挿入され、2番目のベンダーが事前に選択されます。</span><span class="sxs-lookup"><span data-stu-id="502e9-120">Loading the page in the browser will fill the dropdown list with three vendors, the second one being preselected.</span></span> <span data-ttu-id="502e9-121">また、ASP.NET は `__doPostBack()` JavaScript メソッドを定義します。</span><span class="sxs-lookup"><span data-stu-id="502e9-121">Also, ASP.NET defines the `__doPostBack()` JavaScript method.</span></span> <span data-ttu-id="502e9-122">ページが読み込まれると、この JavaScript 呼び出しはドロップダウンリストに追加されますが、その中に要素がある場合に限ります。</span><span class="sxs-lookup"><span data-stu-id="502e9-122">Once the page has been loaded, this JavaScript call is added to the dropdown list, but only if there are elements in it.</span></span> <span data-ttu-id="502e9-123">リストに要素が存在しない場合、コントロールツールキットは現在それらを読み込んでいるため、JavaScript コードはタイムアウトを使用して、0.5 秒後にもう一度試行します。</span><span class="sxs-lookup"><span data-stu-id="502e9-123">If there are no elements in the list, the Control Toolkit is currently loading them, so the JavaScript code uses a timeout and tries again in a half second.</span></span>

[!code-html[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample6.html)]

<span data-ttu-id="502e9-124">このようにして、ポストバックは、リスト内に実際に要素が存在し、ユーザーがエントリを選択した場合にのみ実行されます。</span><span class="sxs-lookup"><span data-stu-id="502e9-124">This way, a postback is only executed when there are actually elements in the list and the user selects an entry.</span></span>

<span data-ttu-id="502e9-125">[リスト要素を選択するとポストバックが発生する ![](using-auto-postback-with-cascadingdropdown-cs/_static/image2.png)](using-auto-postback-with-cascadingdropdown-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="502e9-125">[![Selecting a list element causes a postback](using-auto-postback-with-cascadingdropdown-cs/_static/image2.png)](using-auto-postback-with-cascadingdropdown-cs/_static/image1.png)</span></span>

<span data-ttu-id="502e9-126">リスト要素を選択するとポストバックが発生します ([クリックすると、フルサイズの画像が表示](using-auto-postback-with-cascadingdropdown-cs/_static/image3.png)される)</span><span class="sxs-lookup"><span data-stu-id="502e9-126">Selecting a list element causes a postback ([Click to view full-size image](using-auto-postback-with-cascadingdropdown-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="502e9-127">[前へ](presetting-list-entries-with-cascadingdropdown-cs.md)
> [次へ](filling-a-list-using-cascadingdropdown-vb.md)</span><span class="sxs-lookup"><span data-stu-id="502e9-127">[Previous](presetting-list-entries-with-cascadingdropdown-cs.md)
[Next](filling-a-list-using-cascadingdropdown-vb.md)</span></span>
