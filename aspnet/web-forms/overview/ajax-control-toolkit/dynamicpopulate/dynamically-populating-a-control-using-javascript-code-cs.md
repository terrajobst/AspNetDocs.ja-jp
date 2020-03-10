---
uid: web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-using-javascript-code-cs
title: JavaScript コードを使用してコントロールをC#動的に設定する () |Microsoft Docs
author: wenz
description: ASP.NET AJAX Control Toolkit の DynamicPopulate コントロールは、web サービス (またはページメソッド) を呼び出し、結果の値を t... のターゲットコントロールに入力します。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: cc4c2def-e88c-4456-ae8b-a6ae0ff8cc2d
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-using-javascript-code-cs
msc.type: authoredcontent
ms.openlocfilehash: 24dc358427dec3ffcba16d00041c9a2db657e7e2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78430504"
---
# <a name="dynamically-populating-a-control-using-javascript-code-c"></a><span data-ttu-id="b373a-103">JavaScript コードを使用してコントロールに動的に入力する (C#)</span><span class="sxs-lookup"><span data-stu-id="b373a-103">Dynamically Populating a Control Using JavaScript Code (C#)</span></span>

<span data-ttu-id="b373a-104">[Christian Wenz](https://github.com/wenz)別</span><span class="sxs-lookup"><span data-stu-id="b373a-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="b373a-105">[コードのダウンロード](https://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate1.cs.zip)または[PDF のダウンロード](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="b373a-105">[Download Code](https://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate1.cs.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate1CS.pdf)</span></span>

> <span data-ttu-id="b373a-106">ASP.NET AJAX Control Toolkit の DynamicPopulate コントロールは、web サービス (またはページメソッド) を呼び出し、結果の値をページのターゲットコントロールに入力します。ページの更新は行われません。</span><span class="sxs-lookup"><span data-stu-id="b373a-106">The DynamicPopulate control in the ASP.NET AJAX Control Toolkit calls a web service (or page method) and fills the resulting value into a target control on the page, without a page refresh.</span></span> <span data-ttu-id="b373a-107">また、カスタムクライアント側の JavaScript コードを使用して、作成をトリガーすることもできます。</span><span class="sxs-lookup"><span data-stu-id="b373a-107">It is also possible to trigger the population using custom client-side JavaScript code.</span></span>

## <a name="overview"></a><span data-ttu-id="b373a-108">概要</span><span class="sxs-lookup"><span data-stu-id="b373a-108">Overview</span></span>

<span data-ttu-id="b373a-109">ASP.NET AJAX Control Toolkit の `DynamicPopulate` コントロールは、web サービス (またはページメソッド) を呼び出し、結果の値をページのターゲットコントロールに入力します。ページの更新は行われません。</span><span class="sxs-lookup"><span data-stu-id="b373a-109">The `DynamicPopulate` control in the ASP.NET AJAX Control Toolkit calls a web service (or page method) and fills the resulting value into a target control on the page, without a page refresh.</span></span> <span data-ttu-id="b373a-110">また、カスタムクライアント側の JavaScript コードを使用して、作成をトリガーすることもできます。</span><span class="sxs-lookup"><span data-stu-id="b373a-110">It is also possible to trigger the population using custom client-side JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="b373a-111">手順</span><span class="sxs-lookup"><span data-stu-id="b373a-111">Steps</span></span>

<span data-ttu-id="b373a-112">まず、`DynamicPopulateExtender` コントロールによって呼び出されるメソッドを実装する ASP.NET Web サービスが必要です。</span><span class="sxs-lookup"><span data-stu-id="b373a-112">First of all, you need an ASP.NET Web Service which implements the method to be called by the `DynamicPopulateExtender` control.</span></span> <span data-ttu-id="b373a-113">この web サービスは、`contextKey`と呼ばれる文字列型の引数を1つ必要とするメソッド `getDate()` を実装しています。これは、`DynamicPopulate` コントロールが各 web サービス呼び出しに1つのコンテキスト情報を送信するためです。</span><span class="sxs-lookup"><span data-stu-id="b373a-113">The web service implements the method `getDate()` that expects one argument of type string, called `contextKey`, since the `DynamicPopulate` control sends one piece of context information with each web service call.</span></span> <span data-ttu-id="b373a-114">次に示すコード (ファイル `DynamicPopulate.cs.asmx`) は、次の3つの形式のいずれかで現在の日付を取得します。</span><span class="sxs-lookup"><span data-stu-id="b373a-114">Here is the code (file `DynamicPopulate.cs.asmx`) which retrieves the current date in one of three formats:</span></span>

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-cs/samples/sample1.aspx)]

<span data-ttu-id="b373a-115">次の手順で、新しい ASP.NET サイトを作成し、ASP.NET AJAX ScriptManager コントロールから開始します。</span><span class="sxs-lookup"><span data-stu-id="b373a-115">In the next step, create a new ASP.NET site and start with the ASP.NET AJAX ScriptManager control:</span></span>

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-cs/samples/sample2.aspx)]

<span data-ttu-id="b373a-116">次に、label コントロールを追加します (たとえば、同じ名前の HTML コントロールまたは `<asp:Label />` web コントロールを使用する場合)。この場合、後で web サービス呼び出しの結果が表示されます。</span><span class="sxs-lookup"><span data-stu-id="b373a-116">Then, add a label control (for instance using the HTML control of the same name, or the `<asp:Label />` web control) which will later show the result of the web service call.</span></span>

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-cs/samples/sample3.aspx)]

<span data-ttu-id="b373a-117">次に、`DynamicPopulateExtender` コントロールを含め、web サービス情報、ターゲットコントロールを指定します。ただし、作成をトリガーするコントロールの名前は、後でカスタム JavaScript を使用して実行します。</span><span class="sxs-lookup"><span data-stu-id="b373a-117">Next, include a `DynamicPopulateExtender` control and provide web service information, target control, but not the name of the control which triggers the population this will be done later on, using custom JavaScript!</span></span>

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-cs/samples/sample4.aspx)]

<span data-ttu-id="b373a-118">ここで、JavaScript の部分にします。</span><span class="sxs-lookup"><span data-stu-id="b373a-118">Now to the JavaScript part.</span></span> <span data-ttu-id="b373a-119">`$find()` 関数は、ASP.NET AJAX ライブラリによって定義され、`DynamicPopulateExtender`などの ASP.NET AJAX Control Toolkit のサーバー側オブジェクトへの参照を返します。</span><span class="sxs-lookup"><span data-stu-id="b373a-119">The `$find()` function, defined by the ASP.NET AJAX library, returns a reference to server-side objects of the ASP.NET AJAX Control Toolkit such as `DynamicPopulateExtender`.</span></span> <span data-ttu-id="b373a-120">現在のファイルでは、`$find("dpe")` はページ内の1つの `DynamicPopulateExtender` コントロールへの参照を返します。</span><span class="sxs-lookup"><span data-stu-id="b373a-120">In the current file, `$find("dpe")` returns a reference to the one `DynamicPopulateExtender` control in the page.</span></span> <span data-ttu-id="b373a-121">動的な作成プロセスをトリガーする `populate()` と呼ばれるメソッドを公開します。</span><span class="sxs-lookup"><span data-stu-id="b373a-121">It exposes a method called `populate()` which triggers the dynamic population process.</span></span> <span data-ttu-id="b373a-122">`populate()` メソッドには1つの引数が必要です。これは、`getDate()` web メソッドの引数として機能するコンテキストキーです。</span><span class="sxs-lookup"><span data-stu-id="b373a-122">The `populate()` method requires one argument: the context key which will serve as argument to the `getDate()` web method.</span></span> <span data-ttu-id="b373a-123">たとえば、`$find("dpe").populate("format1")` では、ラベルに月-日-年形式の現在の日付が設定されます。</span><span class="sxs-lookup"><span data-stu-id="b373a-123">So for instance, `$find("dpe").populate("format1")` would populate the label with the current date in month-day-year format.</span></span>

<span data-ttu-id="b373a-124">このサンプルを少し柔軟にするために、ユーザーは複数の日付形式を選択できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="b373a-124">In order to make the sample a bit more flexible, the user may now choose between several date formats.</span></span> <span data-ttu-id="b373a-125">それぞれに対して、ラジオボタンが表示されます。</span><span class="sxs-lookup"><span data-stu-id="b373a-125">For each one of them, a radio button is displayed.</span></span> <span data-ttu-id="b373a-126">ユーザーがラジオボタンをクリックすると、JavaScript コードによって、選択した日付形式でラベルが動的に設定されます。</span><span class="sxs-lookup"><span data-stu-id="b373a-126">Once the user clicks on a radio button, JavaScript code dynamically populates the label with the selected date format.</span></span> <span data-ttu-id="b373a-127">これらのオプションボタンは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="b373a-127">Here are those radio buttons:</span></span>

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-cs/samples/sample5.aspx)]

<span data-ttu-id="b373a-128">オプションボタンのコンテキスト内では、JavaScript 式 `this.value` が現在のボタンの値を参照することに注意してください。これは、`getDate()` メソッドが使用できる情報とまったく同じです。</span><span class="sxs-lookup"><span data-stu-id="b373a-128">Note that within the context of a radio button, the JavaScript expression `this.value` refers to the value of the current button, which happens to be exactly the same information the `getDate()` method can work with.</span></span>

<span data-ttu-id="b373a-129">[![ボタンをクリックすると、指定した形式でサーバーから日付が取得されます。](dynamically-populating-a-control-using-javascript-code-cs/_static/image2.png)](dynamically-populating-a-control-using-javascript-code-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="b373a-129">[![A click on the button retrieves the date from the server, in the format specified](dynamically-populating-a-control-using-javascript-code-cs/_static/image2.png)](dynamically-populating-a-control-using-javascript-code-cs/_static/image1.png)</span></span>

<span data-ttu-id="b373a-130">このボタンをクリックすると、指定した形式でサーバーから日付が取得されます ([クリックすると、フルサイズの画像が表示](dynamically-populating-a-control-using-javascript-code-cs/_static/image3.png)されます)。</span><span class="sxs-lookup"><span data-stu-id="b373a-130">A click on the button retrieves the date from the server, in the format specified ([Click to view full-size image](dynamically-populating-a-control-using-javascript-code-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="b373a-131">[前へ](dynamically-populating-a-control-cs.md)
> [次へ](using-dynamicpopulate-with-a-user-control-and-javascript-cs.md)</span><span class="sxs-lookup"><span data-stu-id="b373a-131">[Previous](dynamically-populating-a-control-cs.md)
[Next](using-dynamicpopulate-with-a-user-control-and-javascript-cs.md)</span></span>
