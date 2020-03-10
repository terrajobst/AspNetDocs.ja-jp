---
uid: web-forms/videos/aspnet-ajax/how-do-i-implement-the-persistent-communications-pattern-using-web-services
title: '[操作方法:]Web サービスを使用して永続的な通信パターンを実装しますか。 | Microsoft Docs'
author: JoeStagner
description: 従来の Web サイトでは、ブラウザーとサーバーは継続的な通信を維持していませんが、操作を実行するユーザーに応答する場合にのみ通信します...
ms.author: riande
ms.date: 08/22/2007
ms.assetid: 424c06cd-6d61-43cd-a1f2-d1a6b62e47b1
msc.legacyurl: /web-forms/videos/aspnet-ajax/how-do-i-implement-the-persistent-communications-pattern-using-web-services
msc.type: video
ms.openlocfilehash: de2eb281cd4bab46635af480ac2e8f07f60f1591
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78510214"
---
# <a name="how-do-i-implement-the-persistent-communications-pattern-using-web-services"></a><span data-ttu-id="255ef-104">[操作方法:]Web サービスを使用して永続的な通信パターンを実装しますか。</span><span class="sxs-lookup"><span data-stu-id="255ef-104">[How Do I:] Implement the Persistent Communications Pattern using Web Services?</span></span>

<span data-ttu-id="255ef-105">[Joe Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="255ef-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

<span data-ttu-id="255ef-106">従来の Web サイトでは、ブラウザーとサーバーは継続的な通信を維持しませんが、操作を実行するユーザーに応答してのみ通信します。</span><span class="sxs-lookup"><span data-stu-id="255ef-106">In a traditional Web site the browser and the server do not maintain an ongoing communication, but communicate only in response to the user performing an action.</span></span> <span data-ttu-id="255ef-107">ページがアプリケーションコンテナーになった最新の Web サイトでは、ユーザーが操作を実行することなくページの更新が発生するように、ブラウザーとサーバーが継続的な通信を維持することが有益な場合があります。</span><span class="sxs-lookup"><span data-stu-id="255ef-107">In a modern Web site where the page becomes an application container, it can be advantageous for the browser and the server to maintain an ongoing communication so that page updates can occur without the user performing an action.</span></span> <span data-ttu-id="255ef-108">これは、AJAX の永続的な通信パターンと呼ばれます。</span><span class="sxs-lookup"><span data-stu-id="255ef-108">This is known as the Persistent Communications Pattern for AJAX.</span></span> <span data-ttu-id="255ef-109">ASP.NET AJAX は、Web 開発者が永続的な通信パターンを実装するための主な2つの方法を提供します。</span><span class="sxs-lookup"><span data-stu-id="255ef-109">ASP.NET AJAX provides two main ways for Web developers to implement the Persistent Communications Pattern.</span></span> <span data-ttu-id="255ef-110">以前のビデオでは、実装の基礎として ASP.NET AJAX UpdatePanel を使用する方法を説明しました。</span><span class="sxs-lookup"><span data-stu-id="255ef-110">In an earlier video we saw how to use the ASP.NET AJAX UpdatePanel as the basis of the implementation.</span></span> <span data-ttu-id="255ef-111">このビデオでは、Web サービスへの JavaScrpt 呼び出しを使用して同じパターンを実装する方法について説明します。これにより、ASP.NET AJAX UpdatePanel が不要になります。</span><span class="sxs-lookup"><span data-stu-id="255ef-111">In this video we learn how to implement the same pattern using a JavaScrpt call to a Web service, which removes the need for an ASP.NET AJAX UpdatePanel.</span></span>

[<span data-ttu-id="255ef-112">&#9654;ビデオを見る (16 分)</span><span class="sxs-lookup"><span data-stu-id="255ef-112">&#9654; Watch video (16 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-implement-the-persistent-communications-pattern-using-web-services)

> [!div class="step-by-step"]
> <span data-ttu-id="255ef-113">[前へ](how-do-i-localize-an-aspnet-ajax-application.md)
> [次へ](how-do-i-trigger-an-updatepanel-refresh-from-a-dropdownlist-control.md)</span><span class="sxs-lookup"><span data-stu-id="255ef-113">[Previous](how-do-i-localize-an-aspnet-ajax-application.md)
[Next](how-do-i-trigger-an-updatepanel-refresh-from-a-dropdownlist-control.md)</span></span>
