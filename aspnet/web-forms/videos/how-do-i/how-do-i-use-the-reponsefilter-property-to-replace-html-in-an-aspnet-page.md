---
uid: web-forms/videos/how-do-i/how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page
title: '[操作方法:]ASP.NET ページ内の HTML を置き換えるには、Filter プロパティを使用します。Microsoft Docs'
author: rick-anderson
description: このビデオでは、ページに送信される HTML をインターセプトおよび変更するために、Filter プロパティを使用する方法を示しています。 まず、サンプルページが作成されます。
ms.author: riande
ms.date: 01/29/2009
ms.assetid: 3e5ae74a-9798-47d8-a2b3-0d8ad42dd4bc
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page
msc.type: video
ms.openlocfilehash: 2ebd9162f81f5270c92c6b8d55e2d2dad4660701
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78487996"
---
# <a name="how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page"></a><span data-ttu-id="90f3e-104">[操作方法:]ASP.NET ページ内の HTML を置き換えるには、Filter プロパティを使用します。</span><span class="sxs-lookup"><span data-stu-id="90f3e-104">[How Do I:] Use the Reponse.Filter Property to Replace HTML in an ASP.NET Page</span></span>

<span data-ttu-id="90f3e-105">[Chris Pels](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="90f3e-105">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="90f3e-106">このビデオでは、ページに送信される HTML をインターセプトおよび変更するために、Filter プロパティを使用する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="90f3e-106">In this video Chris Pels shows how to use the Reponse.Filter property to intercept and alter the HTML being sent to a page.</span></span> <span data-ttu-id="90f3e-107">まず、いくつかの単純なテキストを使用してサンプルページを作成します。</span><span class="sxs-lookup"><span data-stu-id="90f3e-107">First, a sample page is created with some simple text.</span></span> <span data-ttu-id="90f3e-108">次に、ユーザーのブラウザーに送信されている現在のストリームの置換ストリームとして機能するカスタムストリームクラスが作成されます。</span><span class="sxs-lookup"><span data-stu-id="90f3e-108">Then, a custom Stream class is created which serves as the replacement stream for the current stream being sent to the user's browser.</span></span> <span data-ttu-id="90f3e-109">このカスタムストリームクラスでは、ページの内容がストリームから取得され、変更されて、応答ストリームに書き込まれます。</span><span class="sxs-lookup"><span data-stu-id="90f3e-109">In that custom stream class the contents of the page are retrieved from the stream, altered, and then written out to the response stream.</span></span> <span data-ttu-id="90f3e-110">このカスタムストリームクラスでは、基本応答ストリームの HTML を置き換えるように書き込みメソッドをカスタマイズして、ユーザーのブラウザーに送信される内容を変更します。</span><span class="sxs-lookup"><span data-stu-id="90f3e-110">In this custom Stream class the Write method is customized to replace the HTML in the base Response stream, thereby altering what is sent to the user's browser.</span></span> <span data-ttu-id="90f3e-111">最後に、新しいストリームクラスが Response に割り当てられます。これにより、ページの\_読み込みイベントによって、ページコンテンツを変更するためのメカニズムが提供されます。</span><span class="sxs-lookup"><span data-stu-id="90f3e-111">Finally, the new stream class is assigned to the Response.Filter property in the Page\_Load event, thereby, providing the mechanism for altering the page content.</span></span>

[<span data-ttu-id="90f3e-112">&#9654;ビデオを見る (13 分)</span><span class="sxs-lookup"><span data-stu-id="90f3e-112">&#9654; Watch video (13 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page)
