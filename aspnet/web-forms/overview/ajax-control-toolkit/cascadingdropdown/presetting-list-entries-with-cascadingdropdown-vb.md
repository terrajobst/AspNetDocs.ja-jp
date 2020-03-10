---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/presetting-list-entries-with-cascadingdropdown-vb
title: CascadingDropDown を使用してリストエントリを事前に事前に入力する (VB) |Microsoft Docs
author: wenz
description: AJAX コントロールツールキットの CascadingDropDown コントロールは、dropdownlist コントロールを拡張して、1つの DropDownList の変更によって anoth に関連付けられた値が読み込まれるようにします。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: ec61ced7-bbca-4bdd-aa3b-80878f295181
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/presetting-list-entries-with-cascadingdropdown-vb
msc.type: authoredcontent
ms.openlocfilehash: 58d675993777f9dcbe0ce1890a60046c91ee8907
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78483808"
---
# <a name="presetting-list-entries-with-cascadingdropdown-vb"></a><span data-ttu-id="c24b1-103">CascadingDropDown で一覧のエントリを事前設定する (VB)</span><span class="sxs-lookup"><span data-stu-id="c24b1-103">Presetting List Entries with CascadingDropDown (VB)</span></span>

<span data-ttu-id="c24b1-104">[Christian Wenz](https://github.com/wenz)別</span><span class="sxs-lookup"><span data-stu-id="c24b1-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="c24b1-105">[コードのダウンロード](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown2.vb.zip)または[PDF のダウンロード](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/CascadingDropDown2VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="c24b1-105">[Download Code](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown2.vb.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/CascadingDropDown2VB.pdf)</span></span>

> <span data-ttu-id="c24b1-106">AJAX コントロールツールキットの CascadingDropDown コントロールは、dropdownlist コントロールを拡張して、1つの DropDownList の変更によって別の DropDownList に関連付けられた値が読み込まれるようにします。</span><span class="sxs-lookup"><span data-stu-id="c24b1-106">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="c24b1-107">少量のコードを使用すると、データが動的に読み込まれた後でリスト要素が事前選択される可能性があります。</span><span class="sxs-lookup"><span data-stu-id="c24b1-107">With a little bit of code it is possible that a list element is preselected once the data has been dynamically loaded.</span></span>

## <a name="overview"></a><span data-ttu-id="c24b1-108">概要</span><span class="sxs-lookup"><span data-stu-id="c24b1-108">Overview</span></span>

<span data-ttu-id="c24b1-109">AJAX コントロールツールキットの CascadingDropDown コントロールは、dropdownlist コントロールを拡張して、1つの DropDownList の変更によって別の DropDownList に関連付けられた値が読み込まれるようにします。</span><span class="sxs-lookup"><span data-stu-id="c24b1-109">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="c24b1-110">(たとえば、1つのリストに米国の州の一覧が表示され、その州の主要都市が次の一覧に入力されます)。少量のコードを使用すると、データが動的に読み込まれた後でリスト要素が事前選択される可能性があります。</span><span class="sxs-lookup"><span data-stu-id="c24b1-110">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) With a little bit of code it is possible that a list element is preselected once the data has been dynamically loaded.</span></span>

## <a name="steps"></a><span data-ttu-id="c24b1-111">手順</span><span class="sxs-lookup"><span data-stu-id="c24b1-111">Steps</span></span>

<span data-ttu-id="c24b1-112">ASP.NET AJAX と Control Toolkit の機能をアクティブ化するには、ページの任意の場所に `ScriptManager` コントロールを配置する必要があります (`<form>` 要素内)。</span><span class="sxs-lookup"><span data-stu-id="c24b1-112">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-vb/samples/sample1.aspx)]

<span data-ttu-id="c24b1-113">次に、DropDownList コントロールが必要です。</span><span class="sxs-lookup"><span data-stu-id="c24b1-113">Then, a DropDownList control is required:</span></span>

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-vb/samples/sample2.aspx)]

<span data-ttu-id="c24b1-114">この一覧では、web サービスの URL とメソッドの情報を提供する CascadingDropDown extender が追加されます。</span><span class="sxs-lookup"><span data-stu-id="c24b1-114">For this list, a CascadingDropDown extender is added, providing web service URL and method information:</span></span>

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-vb/samples/sample3.aspx)]

<span data-ttu-id="c24b1-115">次に、CascadingDropDown extender は、次のメソッドシグネチャを使用して web サービスを非同期に呼び出します。</span><span class="sxs-lookup"><span data-stu-id="c24b1-115">The CascadingDropDown extender then asynchronously calls a web service with the following method signature:</span></span>

[!code-vb[Main](presetting-list-entries-with-cascadingdropdown-vb/samples/sample4.vb)]

<span data-ttu-id="c24b1-116">このメソッドは、CascadingDropDown value 型の配列を返します。</span><span class="sxs-lookup"><span data-stu-id="c24b1-116">The method returns an array of type CascadingDropDown value.</span></span> <span data-ttu-id="c24b1-117">型のコンストラクターは、最初にリストエントリのキャプションを受け取り、次に値 (HTML `value` 属性) を必要とします。</span><span class="sxs-lookup"><span data-stu-id="c24b1-117">The type's constructor expects first the list entry's caption and then the value (HTML `value` attribute).</span></span> <span data-ttu-id="c24b1-118">3番目の引数が true に設定されている場合、リスト要素はブラウザーで自動的に選択されます。</span><span class="sxs-lookup"><span data-stu-id="c24b1-118">If the third argument is set to true, the list element is automatically selected in the browser.</span></span>

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-vb/samples/sample5.aspx)]

<span data-ttu-id="c24b1-119">ブラウザーにページを読み込むと、ドロップダウンリストに3つのベンダが挿入され、2番目のベンダーが事前に選択されます。</span><span class="sxs-lookup"><span data-stu-id="c24b1-119">Loading the page in the browser will fill the dropdown list with three vendors, the second one being preselected.</span></span>

<span data-ttu-id="c24b1-120">[リストが自動的に入力されて事前選択される ![](presetting-list-entries-with-cascadingdropdown-vb/_static/image2.png)](presetting-list-entries-with-cascadingdropdown-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="c24b1-120">[![The list is filled and preselected automatically](presetting-list-entries-with-cascadingdropdown-vb/_static/image2.png)](presetting-list-entries-with-cascadingdropdown-vb/_static/image1.png)</span></span>

<span data-ttu-id="c24b1-121">リストが自動的に入力され、事前選択されます ([クリックすると、フルサイズの画像が表示](presetting-list-entries-with-cascadingdropdown-vb/_static/image3.png)されます)</span><span class="sxs-lookup"><span data-stu-id="c24b1-121">The list is filled and preselected automatically ([Click to view full-size image](presetting-list-entries-with-cascadingdropdown-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c24b1-122">[前へ](using-cascadingdropdown-with-a-database-vb.md)
> [次へ](using-auto-postback-with-cascadingdropdown-vb.md)</span><span class="sxs-lookup"><span data-stu-id="c24b1-122">[Previous](using-cascadingdropdown-with-a-database-vb.md)
[Next](using-auto-postback-with-cascadingdropdown-vb.md)</span></span>
