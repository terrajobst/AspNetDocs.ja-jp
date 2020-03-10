---
uid: web-forms/overview/ajax-control-toolkit/numericupdown/creating-a-numeric-up-down-control-with-a-web-service-backend-vb
title: Web サービスバックエンドを使用した数値のアップダウンコントロールの作成 (VB) |Microsoft Docs
author: wenz
description: ユーザーがチェックボックスに値を入力するのではなく、(Windows およびその他のオペレーティングシステムに存在する) 数値のアップ/ダウンコントロールで、さらに c...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: afa59dfa-fef1-43d3-8fdd-aea3be36ed3c
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/numericupdown/creating-a-numeric-up-down-control-with-a-web-service-backend-vb
msc.type: authoredcontent
ms.openlocfilehash: 2bf6e1b27180589d39e308de62b5be1f47fa8fe2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78496720"
---
# <a name="creating-a-numeric-updown-control-with-a-web-service-backend-vb"></a><span data-ttu-id="15aee-103">Web サービス バックエンドで数値を上げ下げするコントロールを作成する (VB)</span><span class="sxs-lookup"><span data-stu-id="15aee-103">Creating a Numeric Up/Down Control with a Web Service Backend (VB)</span></span>

<span data-ttu-id="15aee-104">[Christian Wenz](https://github.com/wenz)別</span><span class="sxs-lookup"><span data-stu-id="15aee-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="15aee-105">[コードのダウンロード](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/numericupdown1.vb.zip)または[PDF のダウンロード](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/numericupdown1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="15aee-105">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/numericupdown1.vb.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/numericupdown1VB.pdf)</span></span>

> <span data-ttu-id="15aee-106">ユーザーがチェックボックスに値を入力する代わりに、数値のアップ/ダウンコントロール (Windows およびその他のオペレーティングシステムに存在) を確認することで、より快適に証明できます。</span><span class="sxs-lookup"><span data-stu-id="15aee-106">Instead of letting a user type a value into a check box, a numeric up/down control (that exists on Windows and other operating systems) could prove as more comfortable.</span></span> <span data-ttu-id="15aee-107">既定では、NumericUpDown コントロールの値は常に1ずつ増加または減少しますが、web サービスの方が柔軟性が高くなります。</span><span class="sxs-lookup"><span data-stu-id="15aee-107">By default, the NumericUpDown control always increases or decreases a value by 1, but a web service proves more flexibility.</span></span>

## <a name="overview"></a><span data-ttu-id="15aee-108">概要</span><span class="sxs-lookup"><span data-stu-id="15aee-108">Overview</span></span>

<span data-ttu-id="15aee-109">ユーザーがチェックボックスに値を入力する代わりに、数値のアップ/ダウンコントロール (Windows およびその他のオペレーティングシステムに存在) を確認することで、より快適に証明できます。</span><span class="sxs-lookup"><span data-stu-id="15aee-109">Instead of letting a user type a value into a check box, a numeric up/down control (that exists on Windows and other operating systems) could prove as more comfortable.</span></span> <span data-ttu-id="15aee-110">既定では、`NumericUpDown` コントロールの値は常に1ずつ増加または減少しますが、web サービスの方が柔軟性が高くなります。</span><span class="sxs-lookup"><span data-stu-id="15aee-110">By default, the `NumericUpDown` control always increases or decreases a value by 1, but a web service proves more flexibility.</span></span>

## <a name="steps"></a><span data-ttu-id="15aee-111">手順</span><span class="sxs-lookup"><span data-stu-id="15aee-111">Steps</span></span>

<span data-ttu-id="15aee-112">ASP.NET AJAX Control Toolkit には、テキストボックスに2つのボタンが自動的に追加される `NumericUpDown` extender が含まれています。1つは値を大きくするためのボタンで、もう1つは値を小さくするためのものです。</span><span class="sxs-lookup"><span data-stu-id="15aee-112">The ASP.NET AJAX Control Toolkit contains the `NumericUpDown` extender which automatically adds two buttons to a text box: One for increasing its value, one for decreasing it.</span></span> <span data-ttu-id="15aee-113">ただし、コントロールでは、web サービス呼び出し (またはページメソッド呼び出し) もサポートされています。</span><span class="sxs-lookup"><span data-stu-id="15aee-113">However the control also supports a web service call (or page method call).</span></span> <span data-ttu-id="15aee-114">上矢印または下矢印ボタンがクリックされるたびに、JavaScript コードは web サーバーに接続し、そこでメソッドを実行します。</span><span class="sxs-lookup"><span data-stu-id="15aee-114">Whenever the up or down button is clicked, the JavaScript code connects to the web server and executes a method there.</span></span> <span data-ttu-id="15aee-115">メソッドシグネチャは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="15aee-115">The method signature is the following one:</span></span>

[!code-vb[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/samples/sample1.vb)]

<span data-ttu-id="15aee-116">`current` 引数は、テキストボックス内の現在の値です。`tag` 属性は、`NumericUpDown` extender のプロパティとして設定できる追加のコンテキストデータです (ただし、必須ではありません)。</span><span class="sxs-lookup"><span data-stu-id="15aee-116">The `current` argument is the current value in the text box; the `tag` attribute is additional context data that can be set as a property of the `NumericUpDown` extender (but is not required).</span></span>

<span data-ttu-id="15aee-117">このサンプルでは、数値のアップダウンコントロールでは、2の累乗値 (1、2、4、8、16、32、64など) のみを許可する必要があります。</span><span class="sxs-lookup"><span data-stu-id="15aee-117">For this sample, the numeric up/down control shall only allow values that are powers of two: 1, 2, 4, 8, 16, 32, 64, and so on.</span></span> <span data-ttu-id="15aee-118">そのため、ユーザーが値を大きくするときに実行されるメソッドは、古い値を2倍にする必要があります。もう1つの方法では、値を2で割る必要があります。</span><span class="sxs-lookup"><span data-stu-id="15aee-118">Therefore, the method executed when the user wants to increase the value must double the old value; the other method must divide value by two.</span></span> <span data-ttu-id="15aee-119">完全な web サービスを次に示します。</span><span class="sxs-lookup"><span data-stu-id="15aee-119">So here is the complete web service:</span></span>

[!code-aspx[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/samples/sample2.aspx)]

<span data-ttu-id="15aee-120">最後に、新しい ASP.NET ページを作成します。</span><span class="sxs-lookup"><span data-stu-id="15aee-120">Finally, create a new ASP.NET page.</span></span> <span data-ttu-id="15aee-121">通常どおり、`ScriptManager` コントロール、`TextBox` コントロール、および `NumericUpDownExtender` コントロールが必要です。</span><span class="sxs-lookup"><span data-stu-id="15aee-121">As usual, you need a `ScriptManager` control, a `TextBox` control and a `NumericUpDownExtender` control.</span></span> <span data-ttu-id="15aee-122">後者の場合は、web サービスの情報を提供する必要があります。</span><span class="sxs-lookup"><span data-stu-id="15aee-122">For the latter, you have to provide the web service information:</span></span>

- <span data-ttu-id="15aee-123">ダウン web メソッドまたはページメソッドの `ServiceDownMethod` 名</span><span class="sxs-lookup"><span data-stu-id="15aee-123">`ServiceDownMethod` name of the down web method or page method</span></span>
- <span data-ttu-id="15aee-124">down service メソッドを使用して web サービスへのパスを `ServiceDownPath` します。page メソッドを使用している場合は省略する</span><span class="sxs-lookup"><span data-stu-id="15aee-124">`ServiceDownPath` path to the web service with the down service method; omit if you are using a page method</span></span>
- <span data-ttu-id="15aee-125">アップ web メソッドまたはページメソッドの `ServiceUpMethod` 名</span><span class="sxs-lookup"><span data-stu-id="15aee-125">`ServiceUpMethod` name of the up web method or page method</span></span>
- <span data-ttu-id="15aee-126">up service メソッドを使用して web サービスへのパスを `ServiceUpPath` します。page メソッドを使用している場合は省略する</span><span class="sxs-lookup"><span data-stu-id="15aee-126">`ServiceUpPath` path to the web service with the up service method; omit if you are using a page method</span></span>

<span data-ttu-id="15aee-127">ページの完全なマークアップを次に示します。</span><span class="sxs-lookup"><span data-stu-id="15aee-127">Here is the complete markup for the page:</span></span>

[!code-aspx[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/samples/sample3.aspx)]

<span data-ttu-id="15aee-128">ページを実行すると、上部のボタンをクリックしたときにテキストボックス内の値が常に2倍になり、下部のボタンをクリックすると、その値が半分になります。</span><span class="sxs-lookup"><span data-stu-id="15aee-128">If you run the page, notice how the value in the text box always doubles when you click on the upper button, and is halved when you click on the lower button.</span></span>

<span data-ttu-id="15aee-129">[2の累乗の数値のみが表示される ![](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/_static/image2.png)](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="15aee-129">[![Only numbers that are a power of 2 appear](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/_static/image2.png)](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/_static/image1.png)</span></span>

<span data-ttu-id="15aee-130">2の累乗の数値のみが表示されます ([クリックすると、フルサイズの画像が表示](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/_static/image3.png)されます)</span><span class="sxs-lookup"><span data-stu-id="15aee-130">Only numbers that are a power of 2 appear ([Click to view full-size image](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="15aee-131">[[戻る]](creating-a-numeric-up-down-control-with-a-web-service-backend-cs.md)</span><span class="sxs-lookup"><span data-stu-id="15aee-131">[Previous](creating-a-numeric-up-down-control-with-a-web-service-backend-cs.md)</span></span>
