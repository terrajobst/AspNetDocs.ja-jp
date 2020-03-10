---
uid: mvc/overview/getting-started/lifecycle-of-an-aspnet-mvc-5-application
title: ASP.NET MVC 5 アプリケーションのライフサイクル |Microsoft Docs
author: cephalin
description: ASP.NET MVC 5 アプリケーションのライフサイクルをグラフ化した PDF ドキュメントをダウンロードします。 このライフサイクルドキュメントでは、MVC ライフサイクルの概要を示します...
ms.author: riande
ms.date: 02/28/2014
ms.assetid: 9c1e3a75-b644-4480-8326-11300b1ec4b3
msc.legacyurl: /mvc/overview/getting-started/lifecycle-of-an-aspnet-mvc-5-application
msc.type: authoredcontent
ms.openlocfilehash: f4a9b3fb61552b070db11fba617b5627fcd71cd5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78470326"
---
# <a name="lifecycle-of-an-aspnet-mvc-5-application"></a><span data-ttu-id="e550f-104">ASP.NET MVC 5 アプリケーションのライフサイクル</span><span class="sxs-lookup"><span data-stu-id="e550f-104">Lifecycle of an ASP.NET MVC 5 Application</span></span>

<span data-ttu-id="e550f-105">[Cephas リンク](https://github.com/cephalin)</span><span class="sxs-lookup"><span data-stu-id="e550f-105">by [Cephas Lin](https://github.com/cephalin)</span></span>

[<span data-ttu-id="e550f-106">PDF ドキュメントのダウンロード</span><span class="sxs-lookup"><span data-stu-id="e550f-106">Download PDF Document</span></span>](lifecycle-of-an-aspnet-mvc-5-application/_static/lifecycle-of-an-aspnet-mvc-5-application1.pdf)

<span data-ttu-id="e550f-107">ここでは、HTTP 要求の受信からクライアントへの HTTP 応答の送信まで、すべての ASP.NET MVC 5 アプリケーションのライフサイクルをグラフ化した PDF ドキュメントをダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="e550f-107">Here you can download a PDF document that charts the lifecycle of every ASP.NET MVC 5 application, from receiving the HTTP request to sending the HTTP response back to the client.</span></span> <span data-ttu-id="e550f-108">また、ASP.NET MVC を初めて使用するユーザー向けの教育ツールとしても、アプリケーションの特定の側面を掘り下げなければならないユーザーのための参考資料としても設計されています。</span><span class="sxs-lookup"><span data-stu-id="e550f-108">It is designed both as an educational tool for those who are new to ASP.NET MVC and also as a reference for those who need to drill into specific aspects of the application.</span></span> <span data-ttu-id="e550f-109">PDF ドキュメントには、次の機能があります。</span><span class="sxs-lookup"><span data-stu-id="e550f-109">The PDF document has the following features:</span></span>

- <span data-ttu-id="e550f-110">MVC が[ASP.NET アプリケーションライフサイクル](https://msdn.microsoft.com/library/bb470252.aspx)にどのように統合されるかを理解するのに役立つ、関連する[HttpApplication](https://msdn.microsoft.com/library/system.web.httpapplication.aspx)ステージ。</span><span class="sxs-lookup"><span data-stu-id="e550f-110">Relevant [HttpApplication](https://msdn.microsoft.com/library/system.web.httpapplication.aspx) stages to help you understand where MVC integrates into the [ASP.NET application lifecycle](https://msdn.microsoft.com/library/bb470252.aspx).</span></span>
- <span data-ttu-id="e550f-111">MVC アプリケーションのライフサイクルの概要です。このビューでは、すべての MVC アプリケーションが要求処理パイプラインで通過する主なステージを把握できます。</span><span class="sxs-lookup"><span data-stu-id="e550f-111">A high-level view of the MVC application lifecycle, where you can understand the major stages that every MVC application passes through in the request processing pipeline.</span></span>  
    ![](lifecycle-of-an-aspnet-mvc-5-application/_static/image1.jpg)
- <span data-ttu-id="e550f-112">要求処理パイプラインの詳細をドリルダウンする詳細ビュー。</span><span class="sxs-lookup"><span data-stu-id="e550f-112">A detail view that shows drills down into the details of the request processing pipeline.</span></span> <span data-ttu-id="e550f-113">高レベルビューと詳細ビューを比較して、ライフサイクルの詳細がさまざまな段階にどのように収集されるかを確認できます。</span><span class="sxs-lookup"><span data-stu-id="e550f-113">You can compare the high-level view and the detail view to see how the lifecycles details are collected into the various stages.</span></span> <span data-ttu-id="e550f-114">[PDF をダウンロード](lifecycle-of-an-aspnet-mvc-5-application/_static/lifecycle-of-an-aspnet-mvc-5-application1.pdf)して、より大きなビューを表示します。</span><span class="sxs-lookup"><span data-stu-id="e550f-114">[Download PDF](lifecycle-of-an-aspnet-mvc-5-application/_static/lifecycle-of-an-aspnet-mvc-5-application1.pdf) to see a larger view.</span></span>
    ![](lifecycle-of-an-aspnet-mvc-5-application/_static/image2.jpg)
- <span data-ttu-id="e550f-115">要求処理パイプライン内の[コントローラー](https://msdn.microsoft.com/library/system.web.mvc.controller.aspx)オブジェクトのオーバーライド可能なすべてのメソッドの配置と目的。</span><span class="sxs-lookup"><span data-stu-id="e550f-115">Placement and purpose of all overridable methods on the [Controller](https://msdn.microsoft.com/library/system.web.mvc.controller.aspx) object in the request processing pipeline.</span></span> <span data-ttu-id="e550f-116">1つのメソッドをオーバーライドする必要があるかもしれませんが、目的に応じて適切なライフサイクルステージでコードを記述できるように、アプリケーションのライフサイクルの役割を理解しておくことが重要です。</span><span class="sxs-lookup"><span data-stu-id="e550f-116">You may or may not have the need to override any one method, but it is important for you to understand their role in the application lifecycle so that you can write code at the appropriate life cycle stage for the effect you intend.</span></span>
- <span data-ttu-id="e550f-117">各フィルターの種類 (認証、承認、アクション、および結果) がどのように呼び出されるかを示す、不足している図。</span><span class="sxs-lookup"><span data-stu-id="e550f-117">Blown-up diagrams showing how each of the filter types (authentication, authorization, action, and result) is invoked.</span></span>
- <span data-ttu-id="e550f-118">詳細ビューで、関心のある各ポイントから役に立つ記事やブログにリンクします。</span><span class="sxs-lookup"><span data-stu-id="e550f-118">Link to a useful article or blog from each point of interest in the detail view.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e550f-119">次の手順</span><span class="sxs-lookup"><span data-stu-id="e550f-119">Next Steps</span></span>

<span data-ttu-id="e550f-120">このドキュメントはニーズを満たしていますか?</span><span class="sxs-lookup"><span data-stu-id="e550f-120">Does this document meet your need?</span></span> <span data-ttu-id="e550f-121">お客様からのフィードバックをお待ちしております。</span><span class="sxs-lookup"><span data-stu-id="e550f-121">We'd appreciate your feedback.</span></span> <span data-ttu-id="e550f-122">アプリケーションの ASP.NET MVC ライフサイクルに関して疑問がある場合は、 [Stackoverflow](http://stackoverflow.com/help)と[ASP.NET mvc フォーラム](https://forums.asp.net/1146.aspx)をお勧めします。</span><span class="sxs-lookup"><span data-stu-id="e550f-122">If you have any question on the ASP.NET MVC lifecycle in your application, [Stackoverflow](http://stackoverflow.com/help) and the [ASP.NET MVC forums](https://forums.asp.net/1146.aspx) are great places to ask.</span></span> <span data-ttu-id="e550f-123">最新[のチュートリアル](https://twitter.com/Cephas_MSFT)で更新プログラムを入手できるように、twitter でフォローします。</span><span class="sxs-lookup"><span data-stu-id="e550f-123">Follow [me](https://twitter.com/Cephas_MSFT) on twitter so you can get updates on my latest tutorials.</span></span>
