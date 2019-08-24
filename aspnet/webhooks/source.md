---
uid: webhooks/source
title: ASP.NET Webhook のソースコードと NuGet パッケージ |Microsoft Docs
author: rick-anderson
description: ASP.NET Webhook のソースコードと NuGet パッケージへのリンク
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 91a62bfa-ea3a-41f9-a2e1-e90d2c8fc8ca
ms.openlocfilehash: 8d07848754d9efda9c893b8ba54ac6d0c0214a53
ms.sourcegitcommit: b95316530fa51087d6c400ff91814fe37e73f7e8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/23/2019
ms.locfileid: "70000702"
---
# <a name="aspnet-webhooks-source-code-and-nuget-packages"></a><span data-ttu-id="cce01-103">ASP.NET Webhook のソースコードと NuGet パッケージ</span><span class="sxs-lookup"><span data-stu-id="cce01-103">ASP.NET WebHooks source code and NuGet packages</span></span>

<span data-ttu-id="cce01-104">Microsoft ASP.NET Webhook は、Microsoft ASP.NET のモジュールファミリに含まれており、 [GitHub でオープンソースプロジェクト](https://github.com/aspnet/WebHooks)としてホストされています。</span><span class="sxs-lookup"><span data-stu-id="cce01-104">Microsoft ASP.NET WebHooks is part of the Microsoft ASP.NET family of modules and is hosted as an [Open Source Project on GitHub](https://github.com/aspnet/WebHooks).</span></span> <span data-ttu-id="cce01-105">これは投稿を受け入れることを意味しますが、プル要求を送信する前に[投稿のガイドライン](https://github.com/aspnet/Home/blob/master/CONTRIBUTING.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="cce01-105">This means that we accept contributions, but please look at the [Contribution Guidelines](https://github.com/aspnet/Home/blob/master/CONTRIBUTING.md) before submitting a pull request.</span></span>

<span data-ttu-id="cce01-106">ここで読んでいるこのオンラインドキュメントは、 [GitHub のオープンソース](http://docs.asp.net/en/latest/contribute/style-guide.html#style-guide)としてもホストされており、投稿も受け入れます。</span><span class="sxs-lookup"><span data-stu-id="cce01-106">This online documentation which you are reading now is also hosted as [Open Source on GitHub](http://docs.asp.net/en/latest/contribute/style-guide.html#style-guide) and also accepts contributions.</span></span>

## <a name="nuget-packages"></a><span data-ttu-id="cce01-107">NuGet パッケージ</span><span class="sxs-lookup"><span data-stu-id="cce01-107">NuGet packages</span></span>

<span data-ttu-id="cce01-108">[NuGet パッケージ](https://nuget.org/packages?q=Microsoft.AspNet.WebHooks)は、次の3つの部分に分かれています。</span><span class="sxs-lookup"><span data-stu-id="cce01-108">The [NuGet packages](https://nuget.org/packages?q=Microsoft.AspNet.WebHooks) are divided into three parts:</span></span>

* <span data-ttu-id="cce01-109">[共通](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Common):送信側と受信側の間で共有される共通のパッケージ。</span><span class="sxs-lookup"><span data-stu-id="cce01-109">[Common](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Common): A common package that is shared between senders and receivers.</span></span>

* <span data-ttu-id="cce01-110">[送信者](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Custom):独自の Webhook を他のユーザーに送信することをサポートするパッケージのセット。</span><span class="sxs-lookup"><span data-stu-id="cce01-110">[Sender](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Custom): A set of packages supporting sending your own WebHooks to others.</span></span> <span data-ttu-id="cce01-111">Webhook を送信する機能の詳細については、 [webhook の送信](sending/senders.md)に関するページを参照してください。</span><span class="sxs-lookup"><span data-stu-id="cce01-111">The functionality for sending WebHooks is described in more detail in [Sending WebHooks](sending/senders.md).</span></span>

* <span data-ttu-id="cce01-112">[受信](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers)者:他のユーザーからの Webhook の受信をサポートするパッケージのセット。</span><span class="sxs-lookup"><span data-stu-id="cce01-112">[Receivers](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers): A set of packages supporting receiving WebHooks from others.</span></span> <span data-ttu-id="cce01-113">Webhook を受信する機能の詳細については、 [webhook の受信](receiving/index.md)に関するページを参照してください。</span><span class="sxs-lookup"><span data-stu-id="cce01-113">The functionality for receiving WebHooks is described in more detail in [Receiving WebHooks](receiving/index.md).</span></span>
