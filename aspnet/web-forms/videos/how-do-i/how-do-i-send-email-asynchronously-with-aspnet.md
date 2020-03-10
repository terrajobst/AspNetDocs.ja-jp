---
uid: web-forms/videos/how-do-i/how-do-i-send-email-asynchronously-with-aspnet
title: '[操作方法:]ASP.NET を使用して電子メールを非同期で送信する |Microsoft Docs'
author: rick-anderson
description: このビデオでは、ASP.NET のシステム .Net を使用して、非同期の電子メールメッセージを送信する方法を説明しています。 まず、「web si の構成方法」を参照してください。
ms.author: riande
ms.date: 09/24/2008
ms.assetid: 77a5c8fa-ebb2-426d-b56b-a5a98a46b516
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-send-email-asynchronously-with-aspnet
msc.type: video
ms.openlocfilehash: ea29823446cc1339003160bd3e945bde1af42473
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78516172"
---
# <a name="how-do-i-send-email-asynchronously-with-aspnet"></a><span data-ttu-id="98153-104">[操作方法:]ASP.NET を使用して電子メールを非同期で送信する</span><span class="sxs-lookup"><span data-stu-id="98153-104">[How Do I:] Send Email Asynchronously with ASP.NET</span></span>

<span data-ttu-id="98153-105">[Chris Pels](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="98153-105">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="98153-106">このビデオでは、ASP.NET のシステム .Net を使用して、非同期の電子メールメッセージを送信する方法を説明しています。</span><span class="sxs-lookup"><span data-stu-id="98153-106">In this video, Chris Pels shows how to use the System.Net.Mail classes in ASP.NET to send an asynchronous email message.</span></span> <span data-ttu-id="98153-107">まず、web.config ファイルの &lt;mailSettings&gt; 要素を使用して電子メールを送信するように web サイトを構成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="98153-107">First, see how to configure a web site to send email using the &lt;mailSettings&gt; element in the web.config file.</span></span> <span data-ttu-id="98153-108">次に、電子メール情報を入力するための簡単なユーザーインターフェイスを作成します。</span><span class="sxs-lookup"><span data-stu-id="98153-108">Next, create a simple user interface for entering email information.</span></span> <span data-ttu-id="98153-109">次に、Send-mailmessage クラスを使用して、ページの分離コードに電子メールメッセージを作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="98153-109">Then learn how to create use the MailMessage class to create an email message in the code behind for the page.</span></span> <span data-ttu-id="98153-110">このプロセスの一部として、電子メールの送信後に非同期コールバックのイベントハンドラーを作成します。</span><span class="sxs-lookup"><span data-stu-id="98153-110">As part of that process create an event handler for the asynchronous callback following the sending of the email.</span></span> <span data-ttu-id="98153-111">イベントハンドラーでは、電子メールの送信プロセスに関する情報を提供する AsynchCompletedEventArgs クラスのインスタンスの使用方法を参照してください。</span><span class="sxs-lookup"><span data-stu-id="98153-111">In the event handler see how to use the instance of the AsynchCompletedEventArgs class which provides information about the email sending process.</span></span> <span data-ttu-id="98153-112">最後に、デバッグモードの手順に従って、テスト電子メールを非同期的に送信し、プロセスから受信した実際の電子メールを表示します。</span><span class="sxs-lookup"><span data-stu-id="98153-112">Finally, send a test email asynchronously, following the steps in the debug mode, and view the actual email received from the process.</span></span>

[<span data-ttu-id="98153-113">&#9654;ビデオを見る (18 分)</span><span class="sxs-lookup"><span data-stu-id="98153-113">&#9654; Watch video (18 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-send-email-asynchronously-with-aspnet)
