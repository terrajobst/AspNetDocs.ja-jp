---
uid: web-forms/videos/how-do-i/how-do-i-implement-error-handling-when-sending-email-with-aspnet
title: '[操作方法:]ASP.NET を使用して電子メールを送信するときにエラー処理を実装する |Microsoft Docs'
author: rick-anderson
description: Chris Pels は、ASP.NET で電子メールを送信するときにエラー処理を実装する方法を示しています。 ASP.NET の web ページを作成して電子メールを送信し、& の構成方法を示しています。
ms.author: riande
ms.date: 11/06/2008
ms.assetid: c02ffd50-aa19-4cdc-b1bf-760989979a61
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-implement-error-handling-when-sending-email-with-aspnet
msc.type: video
ms.openlocfilehash: faa0daa2ffe71e58cd18bb8bed4e476ffcb1852e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78457936"
---
# <a name="how-do-i-implement-error-handling-when-sending-email-with-aspnet"></a><span data-ttu-id="cc388-104">[操作方法:]ASP.NET を使用して電子メールを送信するときにエラー処理を実装する</span><span class="sxs-lookup"><span data-stu-id="cc388-104">[How Do I:] Implement Error Handling when Sending Email with ASP.NET</span></span>

<span data-ttu-id="cc388-105">[Chris Pels](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="cc388-105">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="cc388-106">Chris Pels は、ASP.NET で電子メールを送信するときにエラー処理を実装する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="cc388-106">Chris Pels shows how to implement error handling when sending an email with ASP.NET.</span></span> <span data-ttu-id="cc388-107">彼は、電子メールを送信するための ASP.NET web ページを作成し、web.config ファイルの &lt;mailSettings&gt; の構成方法を示します。また、このクラスを使用して、電子メールメッセージを作成および送信する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="cc388-107">He creates an ASP.NET web page to send email, shows how to configure &lt;mailSettings&gt; in the web.config file, describes the System.Net.Mail class and how it's used to create and send email messages.</span></span> <span data-ttu-id="cc388-108">次に、電子メールの送信時に発生する可能性のあるエラーに関する情報を提供し、SmtpStatusCode 列挙を確認する、システム .Net の例外クラスを使用してエラー処理を追加します。これにより、電子メールをSmtpclient.send.</span><span class="sxs-lookup"><span data-stu-id="cc388-108">He then adds error handling using System.Net.Mail exception classes, which provide information about errors that can occur when sending email, and reviews the SmtpStatusCode enumeration, which provides a list of possible outcomes when sending an email with the SmtpClient.</span></span> <span data-ttu-id="cc388-109">最後に、例外を発生させ、Visual Studio デバッガーのエラー処理情報を確認するテスト電子メールを送信します。</span><span class="sxs-lookup"><span data-stu-id="cc388-109">Finally, he sends a test email that raises an exception and reviews the error handling information in the Visual Studio debugger.</span></span>

[<span data-ttu-id="cc388-110">&#9654;ビデオを見る (24 分)</span><span class="sxs-lookup"><span data-stu-id="cc388-110">&#9654; Watch video (24 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-implement-error-handling-when-sending-email-with-aspnet)
