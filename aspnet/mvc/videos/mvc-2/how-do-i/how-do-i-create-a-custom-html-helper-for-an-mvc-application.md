---
uid: mvc/videos/mvc-2/how-do-i/how-do-i-create-a-custom-html-helper-for-an-mvc-application
title: '操作方法: MVC アプリケーションのカスタム HTML ヘルパーを作成する | Microsoft Docs'
author: rick-anderson
description: このビデオでは、ユーザーが MVC アプリケーションの標準セットでは使用できないカスタム HtmlHelper を作成する方法を示します。 最初に、サンプルの MVC アプリケーション...
ms.author: riande
ms.date: 12/11/2009
ms.assetid: 58b5eb15-4160-4ce2-ae70-6ba94262ea73
msc.legacyurl: /mvc/videos/mvc-2/how-do-i/how-do-i-create-a-custom-html-helper-for-an-mvc-application
msc.type: video
ms.openlocfilehash: 60953243d3038667e4f729b1394e68f0c9d7c178
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78450478"
---
# <a name="how-do-i-create-a-custom-html-helper-for-an-mvc-application"></a><span data-ttu-id="70f63-105">操作方法: MVC アプリケーションのカスタム HTML ヘルパーを作成する</span><span class="sxs-lookup"><span data-stu-id="70f63-105">How Do I: Create a Custom HTML Helper for an MVC Application?</span></span>

<span data-ttu-id="70f63-106">[Chris Pels](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="70f63-106">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="70f63-107">このビデオでは、ユーザーが MVC アプリケーションの標準セットでは使用できないカスタム HtmlHelper を作成する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="70f63-107">In this video Chris Pels shows how to create a custom HtmlHelper that is not available in the standard set in an MVC application.</span></span> <span data-ttu-id="70f63-108">まず、デモコントローラーとビューを使用してサンプル MVC アプリケーションを作成し、カスタム HtmlHelper をテストします。</span><span class="sxs-lookup"><span data-stu-id="70f63-108">First, a sample MVC application is created with a demo controller and view to test the custom HtmlHelper.</span></span> <span data-ttu-id="70f63-109">次に、モジュールは、カスタム HtmlHelper の実装を表す拡張メソッドであるパブリック関数を使用して作成されます。</span><span class="sxs-lookup"><span data-stu-id="70f63-109">Next, a module is created with a public function that is an extension method which represents the implementation of the custom HtmlHelper.</span></span> <span data-ttu-id="70f63-110">カスタムヘルパーは、ページに `<img>` タグを作成するためのものであり、イメージタグの id、url、および alt テキストを含むいくつかの受信パラメーターを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="70f63-110">The custom helper is for creating `<img>` tags in a page and receives several inbound parameters including the id, url, and alt text for the image tag.</span></span> <span data-ttu-id="70f63-111">次に、指定された情報で完了した `<img>` タグを返すように、ロジックが関数に追加されます。</span><span class="sxs-lookup"><span data-stu-id="70f63-111">The logic is then added to the function for returning the completed `<img>` tag with the specified information.</span></span> <span data-ttu-id="70f63-112">次に、デモページでカスタム HtmlHelper を使用してイメージを表示します。</span><span class="sxs-lookup"><span data-stu-id="70f63-112">Then the custom HtmlHelper is used on the demo page to display an image.</span></span> <span data-ttu-id="70f63-113">最後に、カスタム HtmlHelper が拡張され、複数のコンストラクターのオーバーライドが含まれるようになり、さまざまな `<img>` タグをより簡単に作成できるようになります。</span><span class="sxs-lookup"><span data-stu-id="70f63-113">Finally, the custom HtmlHelper is expanded to include multiple constructor overrides which provide flexibility for more easily creating different `<img>` tags.</span></span>

[<span data-ttu-id="70f63-114">&#9654;ビデオを見る (18 分)</span><span class="sxs-lookup"><span data-stu-id="70f63-114">&#9654; Watch video (18 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-create-a-custom-html-helper-for-an-mvc-application)

> [!div class="step-by-step"]
> <span data-ttu-id="70f63-115">[前へ](how-do-i-implement-view-models-to-manage-data-for-aspnet-mvc-views.md)
> [次へ](how-do-i-work-with-model-binders-in-an-mvc-application.md)</span><span class="sxs-lookup"><span data-stu-id="70f63-115">[Previous](how-do-i-implement-view-models-to-manage-data-for-aspnet-mvc-views.md)
[Next](how-do-i-work-with-model-binders-in-an-mvc-application.md)</span></span>
