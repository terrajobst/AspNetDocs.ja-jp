---
uid: web-forms/overview/ajax-control-toolkit/dynamicpopulate/using-dynamicpopulate-with-a-user-control-and-javascript-vb
title: DynamicPopulate ユーザーコントロールと JavaScript を設定する (VB) |Microsoft Docs
author: wenz
description: ASP.NET AJAX Control Toolkit の DynamicPopulate コントロールは、web サービス (またはページメソッド) を呼び出し、結果の値を t... のターゲットコントロールに入力します。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 778b9009-76f2-4665-940e-afc0e35bc917
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dynamicpopulate/using-dynamicpopulate-with-a-user-control-and-javascript-vb
msc.type: authoredcontent
ms.openlocfilehash: ee5923ad6d8b101f689a0564aef8b1e0e00a7639
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78497302"
---
# <a name="using-dynamicpopulate-with-a-user-control-and-javascript-vb"></a><span data-ttu-id="c745c-103">ユーザー コントロールと JavaScript で DynamicPopulate を使用する (VB)</span><span class="sxs-lookup"><span data-stu-id="c745c-103">Using DynamicPopulate with a User Control And JavaScript (VB)</span></span>

<span data-ttu-id="c745c-104">[Christian Wenz](https://github.com/wenz)別</span><span class="sxs-lookup"><span data-stu-id="c745c-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="c745c-105">[コードのダウンロード](https://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate2.vb.zip)または[PDF のダウンロード](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate2VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="c745c-105">[Download Code](https://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate2.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate2VB.pdf)</span></span>

> <span data-ttu-id="c745c-106">ASP.NET AJAX Control Toolkit の DynamicPopulate コントロールは、web サービス (またはページメソッド) を呼び出し、結果の値をページのターゲットコントロールに入力します。ページの更新は行われません。</span><span class="sxs-lookup"><span data-stu-id="c745c-106">The DynamicPopulate control in the ASP.NET AJAX Control Toolkit calls a web service (or page method) and fills the resulting value into a target control on the page, without a page refresh.</span></span> <span data-ttu-id="c745c-107">また、カスタムクライアント側の JavaScript コードを使用して、作成をトリガーすることもできます。</span><span class="sxs-lookup"><span data-stu-id="c745c-107">It is also possible to trigger the population using custom client-side JavaScript code.</span></span> <span data-ttu-id="c745c-108">ただし、extender がユーザーコントロールに存在する場合は、特別な注意が必要です。</span><span class="sxs-lookup"><span data-stu-id="c745c-108">However special care has to be taken when the extender resides in a user control.</span></span>

## <a name="overview"></a><span data-ttu-id="c745c-109">概要</span><span class="sxs-lookup"><span data-stu-id="c745c-109">Overview</span></span>

<span data-ttu-id="c745c-110">ASP.NET AJAX Control Toolkit の `DynamicPopulate` コントロールは、web サービス (またはページメソッド) を呼び出し、結果の値をページのターゲットコントロールに入力します。ページの更新は行われません。</span><span class="sxs-lookup"><span data-stu-id="c745c-110">The `DynamicPopulate` control in the ASP.NET AJAX Control Toolkit calls a web service (or page method) and fills the resulting value into a target control on the page, without a page refresh.</span></span> <span data-ttu-id="c745c-111">また、カスタムクライアント側の JavaScript コードを使用して、作成をトリガーすることもできます。</span><span class="sxs-lookup"><span data-stu-id="c745c-111">It is also possible to trigger the population using custom client-side JavaScript code.</span></span> <span data-ttu-id="c745c-112">ただし、extender がユーザーコントロールに存在する場合は、特別な注意が必要です。</span><span class="sxs-lookup"><span data-stu-id="c745c-112">However special care has to be taken when the extender resides in a user control.</span></span>

## <a name="steps"></a><span data-ttu-id="c745c-113">手順</span><span class="sxs-lookup"><span data-stu-id="c745c-113">Steps</span></span>

<span data-ttu-id="c745c-114">まず、`DynamicPopulateExtender` コントロールによって呼び出されるメソッドを実装する ASP.NET Web サービスが必要です。</span><span class="sxs-lookup"><span data-stu-id="c745c-114">First of all, you need an ASP.NET Web Service which implements the method to be called by the `DynamicPopulateExtender` control.</span></span> <span data-ttu-id="c745c-115">この web サービスは、`contextKey`と呼ばれる文字列型の引数を1つ必要とするメソッド `getDate()` を実装しています。これは、`DynamicPopulate` コントロールが各 web サービス呼び出しに1つのコンテキスト情報を送信するためです。</span><span class="sxs-lookup"><span data-stu-id="c745c-115">The web service implements the method `getDate()` that expects one argument of type string, called `contextKey`, since the `DynamicPopulate` control sends one piece of context information with each web service call.</span></span> <span data-ttu-id="c745c-116">次に示すコード (files `DynamicPopulate.vb.asmx`) は、次の3つの形式のいずれかで現在の日付を取得します。</span><span class="sxs-lookup"><span data-stu-id="c745c-116">Here is the code (files `DynamicPopulate.vb.asmx`) which retrieves the current date in one of three formats:</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample1.aspx)]

<span data-ttu-id="c745c-117">次の手順では、新しいユーザーコントロール (`.ascx` ファイル) を作成します。最初の行には次の宣言が示されています。</span><span class="sxs-lookup"><span data-stu-id="c745c-117">In the next step, create a new user control (`.ascx` file), denoted by the following declaration in its first line:</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample2.aspx)]

<span data-ttu-id="c745c-118">&lt;`label`&gt; 要素を使用して、サーバーからのデータが表示されます。</span><span class="sxs-lookup"><span data-stu-id="c745c-118">A &lt;`label`&gt; element will be used to display the data coming from the server.</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample3.aspx)]

<span data-ttu-id="c745c-119">また、ユーザーコントロールファイルでは、3つのラジオボタンを使用します。各ボタンは、web サービスでサポートされる3つの日付形式のいずれかを表します。</span><span class="sxs-lookup"><span data-stu-id="c745c-119">Also in the user control file, we will use three radio buttons, each one representing one of the three possible date formats supported by the web service.</span></span> <span data-ttu-id="c745c-120">ユーザーがいずれかのオプションボタンをクリックすると、ブラウザーは次のような JavaScript コードを実行します。</span><span class="sxs-lookup"><span data-stu-id="c745c-120">When the user clicks on one of the radio buttons, the browser will execute JavaScript code which looks like this:</span></span>

[!code-powershell[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample4.ps1)]

<span data-ttu-id="c745c-121">このコードは、`DynamicPopulateExtender` にアクセスします (奇妙な ID について心配する必要はありません。これについては後で説明します)。動的な作成をデータでトリガーします。</span><span class="sxs-lookup"><span data-stu-id="c745c-121">This code accesses the `DynamicPopulateExtender` (do not worry about the strange ID yet, this will be covered later on) and triggers the dynamic population with data.</span></span> <span data-ttu-id="c745c-122">現在のオプションボタンのコンテキストでは、`this.value` は `format1`、`format2` また `format3` は web メソッドが期待する内容を示します。</span><span class="sxs-lookup"><span data-stu-id="c745c-122">In the context of the current radio button, `this.value` refers to its value which is `format1`, `format2` or `format3` exactly what the web method expects.</span></span>

<span data-ttu-id="c745c-123">ユーザーコントロールにまだ存在しないのは、オプションボタンを web サービスにリンクする `DynamicPopulateExtender` コントロールです。</span><span class="sxs-lookup"><span data-stu-id="c745c-123">The only thing missing in the user control yet is the `DynamicPopulateExtender` control which links the radio buttons to the web service.</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample5.aspx)]

<span data-ttu-id="c745c-124">ここでも、コントロールで使用されている奇妙な ID (`myDate`ではなく `mcd1$myDate`) に注意することができます。</span><span class="sxs-lookup"><span data-stu-id="c745c-124">Again you may note the strange ID used in the control: `mcd1$myDate` instead of `myDate`.</span></span> <span data-ttu-id="c745c-125">以前は、JavaScript コードは `dpe1`ではなく `DynamicPopulateExtender` にアクセスするために `mcd1_dpe1` 使用されていました。この名前付け方法は、ユーザーコントロール内で `DynamicPopulateExtender` を使用する場合に特別な要件となります。</span><span class="sxs-lookup"><span data-stu-id="c745c-125">Previously, the JavaScript code used `mcd1_dpe1` to access the `DynamicPopulateExtender` instead of `dpe1`.This naming strategy is a special requirement when using `DynamicPopulateExtender` within a user control.</span></span> <span data-ttu-id="c745c-126">さらに、すべての機能を使用するには、ユーザーコントロールを特定の方法で埋め込む必要があります。</span><span class="sxs-lookup"><span data-stu-id="c745c-126">Furthermore, you have to embed the user control in a specific way to make it all work.</span></span> <span data-ttu-id="c745c-127">新しい ASP.NET ページを作成し、先ほど実装したユーザーコントロールのタグプレフィックスを登録します。</span><span class="sxs-lookup"><span data-stu-id="c745c-127">Create a new ASP.NET page and register a tag prefix for the user control you have just implemented:</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample6.aspx)]

<span data-ttu-id="c745c-128">次に、ASP.NET AJAX `ScriptManager` コントロールを新しいページに追加します。</span><span class="sxs-lookup"><span data-stu-id="c745c-128">Then, include the ASP.NET AJAX `ScriptManager` control on the new page:</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample7.aspx)]

<span data-ttu-id="c745c-129">最後に、ユーザーコントロールをページに追加します。</span><span class="sxs-lookup"><span data-stu-id="c745c-129">Finally, add the user control to the page.</span></span> <span data-ttu-id="c745c-130">`ID` 属性を設定する必要があるだけです (もちろん `runat="server"`ます) が、これは JavaScript を使用してアクセスするためにユーザーコントロール内で使用されるプレフィックスであるため、`mcd1` を特定の名前に設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c745c-130">You only have to set its `ID` attribute (and `runat="server"`, of course), but you also have to set it to a specific name: `mcd1` since this is the prefix used within the user control to access it using JavaScript.</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample8.aspx)]

<span data-ttu-id="c745c-131">これで終了です。</span><span class="sxs-lookup"><span data-stu-id="c745c-131">And that's it!</span></span> <span data-ttu-id="c745c-132">ページは想定どおりに動作します。ユーザーがいずれかのオプションボタンをクリックすると、ツールキットのコントロールが web サービスを呼び出し、現在の日付を目的の形式で表示します。</span><span class="sxs-lookup"><span data-stu-id="c745c-132">The page behaves as expected: A user clicks on one of the radio buttons, the control in the Toolkit calls the web service and displays the current date in the desired format.</span></span>

<span data-ttu-id="c745c-133">[オプションボタンがユーザーコントロールに存在する ![](using-dynamicpopulate-with-a-user-control-and-javascript-vb/_static/image2.png)](using-dynamicpopulate-with-a-user-control-and-javascript-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="c745c-133">[![The radio buttons reside in a user control](using-dynamicpopulate-with-a-user-control-and-javascript-vb/_static/image2.png)](using-dynamicpopulate-with-a-user-control-and-javascript-vb/_static/image1.png)</span></span>

<span data-ttu-id="c745c-134">オプションボタンはユーザーコントロールに存在します ([クリックすると、フルサイズの画像が表示](using-dynamicpopulate-with-a-user-control-and-javascript-vb/_static/image3.png)されます)</span><span class="sxs-lookup"><span data-stu-id="c745c-134">The radio buttons reside in a user control ([Click to view full-size image](using-dynamicpopulate-with-a-user-control-and-javascript-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c745c-135">[[戻る]](dynamically-populating-a-control-using-javascript-code-vb.md)</span><span class="sxs-lookup"><span data-stu-id="c745c-135">[Previous](dynamically-populating-a-control-using-javascript-code-vb.md)</span></span>
