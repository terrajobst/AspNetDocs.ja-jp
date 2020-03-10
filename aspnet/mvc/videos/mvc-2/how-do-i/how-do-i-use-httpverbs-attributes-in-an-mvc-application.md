---
uid: mvc/videos/mvc-2/how-do-i/how-do-i-use-httpverbs-attributes-in-an-mvc-application
title: '操作方法: MVC アプリケーションで HttpVerbs 属性を使用する | Microsoft Docs'
author: rick-anderson
description: このビデオでは、HttpVerbs 属性を使用して MVC アクションへのアクセスを制御する方法を示します。 最初に、サンプルアプリケーションが既定の co...
ms.author: riande
ms.date: 12/30/2009
ms.assetid: d2488a1d-0f3f-4994-8fbe-4f59b8c9503e
msc.legacyurl: /mvc/videos/mvc-2/how-do-i/how-do-i-use-httpverbs-attributes-in-an-mvc-application
msc.type: video
ms.openlocfilehash: bda3b122aaf2970b9238d7120ad15fb06672c85b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78432004"
---
# <a name="how-do-i-use-httpverbs-attributes-in-an-mvc-application"></a><span data-ttu-id="151d6-105">操作方法: MVC アプリケーションで HttpVerbs 属性を使用する</span><span class="sxs-lookup"><span data-stu-id="151d6-105">How Do I: Use HttpVerbs Attributes in an MVC Application?</span></span>

<span data-ttu-id="151d6-106">[Chris Pels](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="151d6-106">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="151d6-107">このビデオでは、HttpVerbs 属性を使用して MVC アクションへのアクセスを制御する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="151d6-107">In this video Chris Pels shows how to use the HttpVerbs attributes to control access to MVC actions.</span></span> <span data-ttu-id="151d6-108">最初に、情報を編集するための既定のコントローラーとビューを備えたサンプルアプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="151d6-108">First, a sample application is created with a default controller and view for editing the information.</span></span> <span data-ttu-id="151d6-109">次に、HttpPost 属性を持つコントローラーに2番目のインデックスアクションを追加します。これにより、HTTP POST が使用された場合にのみ呼び出されるように制限されます。</span><span class="sxs-lookup"><span data-stu-id="151d6-109">Next, a second Index action is added to the controller which has an HttpPost attribute which restricts it to being called only when an HTTP POST is used.</span></span> <span data-ttu-id="151d6-110">フォローアップとして、AcceptVerbs () 属性は Visual Studio 2008 の代替構文として実装されます。</span><span class="sxs-lookup"><span data-stu-id="151d6-110">As a follow-up, the AcceptVerbs() attribute is implemented as an alternative syntax for Visual Studio 2008.</span></span> <span data-ttu-id="151d6-111">HTTP GET を使用したリンクからの削除の実行に関連するセキュリティリスクを回避するために HttpVerbs を使用すると、次に説明します。</span><span class="sxs-lookup"><span data-stu-id="151d6-111">A use of the HttpVerbs for preventing the security risk associated with using an HTTP GET to perform a delete from a link is then discussed.</span></span>

[<span data-ttu-id="151d6-112">&#9654;ビデオを見る (16 分)</span><span class="sxs-lookup"><span data-stu-id="151d6-112">&#9654; Watch video (16 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-use-httpverbs-attributes-in-an-mvc-application)

> [!div class="step-by-step"]
> <span data-ttu-id="151d6-113">[前へ](how-do-i-work-with-model-binders-in-an-mvc-application.md)
> [次へ](mvc2-html-encoding.md)</span><span class="sxs-lookup"><span data-stu-id="151d6-113">[Previous](how-do-i-work-with-model-binders-in-an-mvc-application.md)
[Next](mvc2-html-encoding.md)</span></span>
