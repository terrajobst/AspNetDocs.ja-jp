---
uid: web-forms/overview/ajax-control-toolkit/nobot/fighting-bots-vb
title: 戦いボット (VB) |Microsoft Docs
author: wenz
description: 自動ボットは、ユーザー操作なしでコメントフォームを送信して、web サイトやスパムを plaster します。 ASP.NET AJAX Con の NoBot コントロール...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e9803150-452d-4521-97e3-d75d5599383c
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/nobot/fighting-bots-vb
msc.type: authoredcontent
ms.openlocfilehash: a8ca71b96cb84c97b1a60ae6a3d1a129cd1b0b10
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78509050"
---
# <a name="fighting-bots-vb"></a><span data-ttu-id="ef24e-104">ボットと戦う (VB)</span><span class="sxs-lookup"><span data-stu-id="ef24e-104">Fighting Bots (VB)</span></span>

<span data-ttu-id="ef24e-105">[Christian Wenz](https://github.com/wenz)別</span><span class="sxs-lookup"><span data-stu-id="ef24e-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="ef24e-106">[コードのダウンロード](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/NoBot0.vb.zip)または[PDF のダウンロード](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/nobot0VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="ef24e-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/NoBot0.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/nobot0VB.pdf)</span></span>

> <span data-ttu-id="ef24e-107">自動ボットは、ユーザー操作なしでコメントフォームを送信して、web サイトやスパムを plaster します。</span><span class="sxs-lookup"><span data-stu-id="ef24e-107">Automated bots plaster weblogs and other websites with spam, submitting comment forms without any user interaction.</span></span> <span data-ttu-id="ef24e-108">ASP.NET AJAX Control Toolkit の NoBot コントロールは、これらのボットを戦うのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="ef24e-108">The NoBot control in the ASP.NET AJAX Control Toolkit can help fight those bots.</span></span>

## <a name="overview"></a><span data-ttu-id="ef24e-109">概要</span><span class="sxs-lookup"><span data-stu-id="ef24e-109">Overview</span></span>

<span data-ttu-id="ef24e-110">自動ボットは、ユーザー操作なしでコメントフォームを送信して、web サイトやスパムを plaster します。</span><span class="sxs-lookup"><span data-stu-id="ef24e-110">Automated bots plaster weblogs and other websites with spam, submitting comment forms without any user interaction.</span></span> <span data-ttu-id="ef24e-111">ASP.NET AJAX Control Toolkit の NoBot コントロールは、これらのボットを戦うのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="ef24e-111">The NoBot control in the ASP.NET AJAX Control Toolkit can help fight those bots.</span></span>

## <a name="steps"></a><span data-ttu-id="ef24e-112">手順</span><span class="sxs-lookup"><span data-stu-id="ef24e-112">Steps</span></span>

<span data-ttu-id="ef24e-113">ボットを突破する一般的な方法の1つは、CAPTCHAs 完全に自動化されたパブリックチューリングテストを使用して、コンピューターと人間を区別することです。</span><span class="sxs-lookup"><span data-stu-id="ef24e-113">One common approach to defeat bots is to use CAPTCHAs Completely Automated Public Turing test to tell Computers and Humans Apart.</span></span> <span data-ttu-id="ef24e-114">チューリングテストはもともと、通信パートナーが人間とコンピューターのどちらであるかを判断する必要があるテストでした。</span><span class="sxs-lookup"><span data-stu-id="ef24e-114">A Turing test was originally a test where someone needed to decide whether a communication partner is a human or a machine.</span></span> <span data-ttu-id="ef24e-115">Web では、通常、CAPTCHA は、何らかの変形した文字を含むイメージで構成されます。</span><span class="sxs-lookup"><span data-stu-id="ef24e-115">In the web, a CAPTCHA usually consists of an image with some distorted letters on it.</span></span> <span data-ttu-id="ef24e-116">これは、人間だけが画像の文字を読み取ることができるのに対し、OCR アルゴリズムは失敗するということです。</span><span class="sxs-lookup"><span data-stu-id="ef24e-116">The idea is that only a human can read the letters on the image, whereas OCR algorithms will fail.</span></span>

<span data-ttu-id="ef24e-117">この方法にはいくつかの長所と短所がありますが、このチュートリアルでは説明しません。</span><span class="sxs-lookup"><span data-stu-id="ef24e-117">There are several advantages and disadvantages to this approach, but a discussion of this is beyond the scope of this tutorial.</span></span> <span data-ttu-id="ef24e-118">ただし、ASP.NET AJAX Control Toolkit には、`NoBot`と同様のアプローチを提供するコントロールがあります。</span><span class="sxs-lookup"><span data-stu-id="ef24e-118">There is however a control in the ASP.NET AJAX Control Toolkit which provides a similar approach: `NoBot`.</span></span> <span data-ttu-id="ef24e-119">CAPTCHA を克服する方が簡単ですが、ブログなどの web サイトで非常に使いやすく、高速に使用できます。これは、ほとんどのスパム試行が敗北した場合に成功と見なされ、`NoBot` 制御が可能です。</span><span class="sxs-lookup"><span data-stu-id="ef24e-119">It is easier to overcome than a CAPTCHA, but is very easy to use and fares extremely well on websites like blogs where it is considered a success if most spam attempts are defeated, which the `NoBot` control can do.</span></span>

<span data-ttu-id="ef24e-120">次の条件のうち少なくとも1つが満たされている場合、`NoBot` は現在の ASP.NET web フォームのポストバックをインターセプトします。</span><span class="sxs-lookup"><span data-stu-id="ef24e-120">`NoBot` intercepts the postback of the current ASP.NET web form if at least one of these conditions is met:</span></span>

- <span data-ttu-id="ef24e-121">ブラウザーが JavaScript パズルの解決に失敗する (JavaScript が非アクティブになった場合など)</span><span class="sxs-lookup"><span data-stu-id="ef24e-121">The browser fails to solve a JavaScript puzzle (for instance when JavaScript is deactivated)</span></span>
- <span data-ttu-id="ef24e-122">ユーザーがフォームを高速に送信しました</span><span class="sxs-lookup"><span data-stu-id="ef24e-122">The user submitted the form to fast</span></span>
- <span data-ttu-id="ef24e-123">クライアントの IP アドレスが、一定期間内にフォームを頻繁に送信しました。</span><span class="sxs-lookup"><span data-stu-id="ef24e-123">The client IP address submitted the form too often in a certain period of time.</span></span>

<span data-ttu-id="ef24e-124">これらの条件を確認するために、`NoBot` コントロールには次の属性が必要です (これらの属性はすべて省略可能です)。</span><span class="sxs-lookup"><span data-stu-id="ef24e-124">In order to check for these conditions, the `NoBot` control requires these attributes (all of them optional):</span></span>

- <span data-ttu-id="ef24e-125">ポストバックの間隔を `ResponseMinimumDelaySeconds` 最小値 (秒)</span><span class="sxs-lookup"><span data-stu-id="ef24e-125">`ResponseMinimumDelaySeconds` minimum amount of seconds between postbacks</span></span>
- <span data-ttu-id="ef24e-126">1つの IP からのポストバックが測定される時間間隔の長さ `CutoffWindowSeconds`</span><span class="sxs-lookup"><span data-stu-id="ef24e-126">`CutoffWindowSeconds` length of time interval in which postbacks from one IP are measures</span></span>
- <span data-ttu-id="ef24e-127">時間間隔 (秒単位) `CutoffMaximumInstances` 最大値</span><span class="sxs-lookup"><span data-stu-id="ef24e-127">`CutoffMaximumInstances` maximum amount of seconds per time interval</span></span>

<span data-ttu-id="ef24e-128">次のマークアップでは、ポストバックの間隔が2秒以上であることが要求されています。また、30秒間隔以内にポストバックが5回以下であることが必要です。</span><span class="sxs-lookup"><span data-stu-id="ef24e-128">The following markup demands that at least two seconds elapse between postbacks and that there are only five postbacks or less within a 30 seconds interval:</span></span>

[!code-aspx[Main](fighting-bots-vb/samples/sample1.aspx)]

<span data-ttu-id="ef24e-129">次に、通常どおり、ASP.NET AJAX ライブラリが読み込まれて Control Toolkit を使用できるように、ページに `ScriptManager` を含めます。</span><span class="sxs-lookup"><span data-stu-id="ef24e-129">Then as usual make sure to include the `ScriptManager` in the page so that the ASP.NET AJAX library is loaded and the Control Toolkit can be used:</span></span>

[!code-aspx[Main](fighting-bots-vb/samples/sample2.aspx)]

<span data-ttu-id="ef24e-130">ほとんどのチェック `NoBot` はサーバー側で行われるため、これらの検証の結果を確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ef24e-130">Since most of the checks `NoBot` is doing occur on the server side, you need to check the result of these validations.</span></span> <span data-ttu-id="ef24e-131">これは `NoBot`の `IsValid()` メソッドを呼び出すことによって行うことができます。</span><span class="sxs-lookup"><span data-stu-id="ef24e-131">This can be done by calling `NoBot`'s `IsValid()` method.</span></span> <span data-ttu-id="ef24e-132">これには、`NoBotState`型の1つの引数 (`out` パラメーター/`ByRef` パラメーター) があります。</span><span class="sxs-lookup"><span data-stu-id="ef24e-132">It has one argument (as an `out` parameter/`ByRef` parameter) which is of type `NoBotState`.</span></span> <span data-ttu-id="ef24e-133">この文字列形式には、チェックが失敗した理由が含まれており、それ以外の場合は `Valid` ます。</span><span class="sxs-lookup"><span data-stu-id="ef24e-133">Its string representation contains the reason when the check fails and `Valid` otherwise.</span></span> <span data-ttu-id="ef24e-134">次のコードは、`NoBot`の結果に従ってメッセージを出力します。</span><span class="sxs-lookup"><span data-stu-id="ef24e-134">The following code outputs a message according to `NoBot`'s result:</span></span>

[!code-aspx[Main](fighting-bots-vb/samples/sample3.aspx)]

<span data-ttu-id="ef24e-135">最後に、フォームを送信し、メッセージを出力するラベル要素を作成する必要があります。完了しました。</span><span class="sxs-lookup"><span data-stu-id="ef24e-135">Finally, you need a form to submit and a label element to output the message, and you are done!</span></span>

[!code-aspx[Main](fighting-bots-vb/samples/sample4.aspx)]

<span data-ttu-id="ef24e-136">このスクリプトを実行して JavaScript を非アクティブにしたり、最初の2秒以内にフォームを送信したり、30秒以内にフォームを送信したりすると、エラーメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="ef24e-136">When you run this script and deactivate JavaScript or submit the form within the first two seconds or submit the form seven times within thirty seconds, you will get an error message.</span></span> <span data-ttu-id="ef24e-137">ただし、このコントロールは適切に使用します。これは、ユーザーの約90-95% だけが JavaScript をアクティブにしているため、ユーザーの5-10% は `NoBot`のテストに失敗するためです。</span><span class="sxs-lookup"><span data-stu-id="ef24e-137">However use this control wisely, since only about 90-95% of users have JavaScript activated, therefore 5-10% of users will fail `NoBot`'s test.</span></span>

<span data-ttu-id="ef24e-138">[このエラーメッセージは、bot によって発生した ![ます。](fighting-bots-vb/_static/image2.png)](fighting-bots-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="ef24e-138">[![This error message could have been caused by a bot](fighting-bots-vb/_static/image2.png)](fighting-bots-vb/_static/image1.png)</span></span>

<span data-ttu-id="ef24e-139">このエラーメッセージは bot によって発生した可能性があります ([クリックすると、フルサイズの画像が表示](fighting-bots-vb/_static/image3.png)されます)</span><span class="sxs-lookup"><span data-stu-id="ef24e-139">This error message could have been caused by a bot ([Click to view full-size image](fighting-bots-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="ef24e-140">[[戻る]](fighting-bots-cs.md)</span><span class="sxs-lookup"><span data-stu-id="ef24e-140">[Previous](fighting-bots-cs.md)</span></span>
