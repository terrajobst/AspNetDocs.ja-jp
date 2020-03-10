---
uid: web-forms/videos/aspnet-ajax/how-do-i-choose-between-methods-of-ajax-page-updates
title: '[How Do i:]AJAX のメソッド間を選択ページの更新しますか? | Microsoft Docs'
author: JoeStagner
description: このビデオでは、Joe Stagner は、ASP.NET アプリケーションで AJAX スタイルのページ更新を実行する2つの主要な方法を比較しています。 最初の方法では、Upd を使用します。
ms.author: riande
ms.date: 07/09/2007
ms.assetid: a5e33a7d-ccb2-483f-a955-3d39f72ba4ec
msc.legacyurl: /web-forms/videos/aspnet-ajax/how-do-i-choose-between-methods-of-ajax-page-updates
msc.type: video
ms.openlocfilehash: 56e3ebfbe0b5af4234791136725de79e38171cc1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78420154"
---
# <a name="how-do-i-choose-between-methods-of-ajax-page-updates"></a><span data-ttu-id="548c7-105">[How Do i:]AJAX のメソッド間を選択ページの更新しますか?</span><span class="sxs-lookup"><span data-stu-id="548c7-105">[How Do I:] Choose Between Methods of AJAX Page Updates?</span></span>

<span data-ttu-id="548c7-106">[Joe Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="548c7-106">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

<span data-ttu-id="548c7-107">このビデオでは、Joe Stagner は、ASP.NET アプリケーションで AJAX スタイルのページ更新を実行する2つの主要な方法を比較しています。</span><span class="sxs-lookup"><span data-stu-id="548c7-107">In this video Joe Stagner compares the two primary methods of performing AJAX-style page updates in an ASP.NET application.</span></span> <span data-ttu-id="548c7-108">最初の方法では、UpdatePanel を使用します。この場合、クライアント側とサーバー側のどちらでも追加のコードを記述する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="548c7-108">The first method is to use an UpdatePanel, where no additional code needs to be written on either the client side or the server side.</span></span> <span data-ttu-id="548c7-109">UpdatePanel を使用する利点は、すべてが自動的に動作することです。</span><span class="sxs-lookup"><span data-stu-id="548c7-109">The benefit of using the UpdatePanel is that everything works automatically.</span></span> <span data-ttu-id="548c7-110">クライアント側では、AJAX の要求と応答に大量のデータが含まれている必要があります。また、サーバーでは、完全なページライフサイクルが実行される必要があります。</span><span class="sxs-lookup"><span data-stu-id="548c7-110">The penalty is that at the client it requires a lot of data to be included in the AJAX request and response, and at the server it requires a full page lifecycle to be executed.</span></span> <span data-ttu-id="548c7-111">2つ目の方法では、ネットワークコールバックを使用します。この場合、クライアント側とサーバー側の両方で追加のコードを記述する必要があります。</span><span class="sxs-lookup"><span data-stu-id="548c7-111">The second method is to use network callbacks, where additional code needs to be written on both the client side and the server side.</span></span> <span data-ttu-id="548c7-112">ネットワークコールバックを使用する利点は、クライアントでは AJAX 要求と応答に含まれるデータが非常に少ないことです。サーバーでは、呼び出されたサービスメソッドのみを実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="548c7-112">The benefit of using network callbacks is that at the client it requires very little data to be included in the AJAX request and response, and at the server it requires only the called service method to be executed.</span></span> <span data-ttu-id="548c7-113">この場合、必要なコードを記述するのに要する時間と労力が必要です。</span><span class="sxs-lookup"><span data-stu-id="548c7-113">The penality is the time and effort it takes to write the necessary code.</span></span> <span data-ttu-id="548c7-114">Joe は、AJAX スタイルのページ更新の2つの主要な方法を選択するときに考慮する必要があることについて説明することで、ビデオを終了します。</span><span class="sxs-lookup"><span data-stu-id="548c7-114">Joe concludes the video by discussing what you should consider when choosing between the two primary methods of AJAX-style page updates.</span></span> <span data-ttu-id="548c7-115">(このビデオでは、 [ASP.NET ajax の使用を開始する方法に関する](how-do-i-get-started-with-aspnet-ajax.md)ビデオのコードを使用し、 [ASP.NET Ajax ビデオでクライアント側のネットワークコールバックを作成する方法について説明](how-do-i-make-client-side-network-callbacks-with-aspnet-ajax.md)しています)。</span><span class="sxs-lookup"><span data-stu-id="548c7-115">(This video uses the code from the [How Do I Get Started with ASP.NET AJAX](how-do-i-get-started-with-aspnet-ajax.md) video and the [How Do I Make Client-Side Network Callbacks with ASP.NET AJAX](how-do-i-make-client-side-network-callbacks-with-aspnet-ajax.md) video.)</span></span>

[<span data-ttu-id="548c7-116">&#9654;ビデオを見る (11 分)</span><span class="sxs-lookup"><span data-stu-id="548c7-116">&#9654; Watch video (11 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-choose-between-methods-of-ajax-page-updates)

> [!div class="step-by-step"]
> <span data-ttu-id="548c7-117">[前へ](how-do-i-update-multiple-regions-of-a-page-with-aspnet-ajax.md)
> [次へ](how-do-i-use-other-javascript-user-interface-libraries-with-aspnet-ajax.md)</span><span class="sxs-lookup"><span data-stu-id="548c7-117">[Previous](how-do-i-update-multiple-regions-of-a-page-with-aspnet-ajax.md)
[Next](how-do-i-use-other-javascript-user-interface-libraries-with-aspnet-ajax.md)</span></span>
