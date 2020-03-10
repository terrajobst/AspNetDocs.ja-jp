---
uid: webhooks/source
title: ASP.NET Webhook のソースコードと NuGet パッケージ |Microsoft Docs
author: rick-anderson
description: ASP.NET Webhook のソースコードと NuGet パッケージへのリンク
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 91a62bfa-ea3a-41f9-a2e1-e90d2c8fc8ca
ms.openlocfilehash: 8d07848754d9efda9c893b8ba54ac6d0c0214a53
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78513910"
---
# <a name="aspnet-webhooks-source-code-and-nuget-packages"></a><span data-ttu-id="27cc1-103">ASP.NET Webhook のソースコードと NuGet パッケージ</span><span class="sxs-lookup"><span data-stu-id="27cc1-103">ASP.NET WebHooks source code and NuGet packages</span></span>

<span data-ttu-id="27cc1-104">Microsoft ASP.NET Webhook は、Microsoft ASP.NET のモジュールファミリに含まれており、 [GitHub でオープンソースプロジェクト](https://github.com/aspnet/WebHooks)としてホストされています。</span><span class="sxs-lookup"><span data-stu-id="27cc1-104">Microsoft ASP.NET WebHooks is part of the Microsoft ASP.NET family of modules and is hosted as an [Open Source Project on GitHub](https://github.com/aspnet/WebHooks).</span></span> <span data-ttu-id="27cc1-105">これは投稿を受け入れることを意味しますが、プル要求を送信する前に[投稿のガイドライン](https://github.com/aspnet/Home/blob/master/CONTRIBUTING.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="27cc1-105">This means that we accept contributions, but please look at the [Contribution Guidelines](https://github.com/aspnet/Home/blob/master/CONTRIBUTING.md) before submitting a pull request.</span></span>

<span data-ttu-id="27cc1-106">ここで読んでいるこのオンラインドキュメントは、 [GitHub のオープンソース](http://docs.asp.net/en/latest/contribute/style-guide.html#style-guide)としてもホストされており、投稿も受け入れます。</span><span class="sxs-lookup"><span data-stu-id="27cc1-106">This online documentation which you are reading now is also hosted as [Open Source on GitHub](http://docs.asp.net/en/latest/contribute/style-guide.html#style-guide) and also accepts contributions.</span></span>

## <a name="nuget-packages"></a><span data-ttu-id="27cc1-107">NuGet パッケージ</span><span class="sxs-lookup"><span data-stu-id="27cc1-107">NuGet packages</span></span>

<span data-ttu-id="27cc1-108">[NuGet パッケージ](https://nuget.org/packages?q=Microsoft.AspNet.WebHooks)は、次の3つの部分に分かれています。</span><span class="sxs-lookup"><span data-stu-id="27cc1-108">The [NuGet packages](https://nuget.org/packages?q=Microsoft.AspNet.WebHooks) are divided into three parts:</span></span>

* <span data-ttu-id="27cc1-109">[共通](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Common): 送信側と受信側の間で共有される共通のパッケージ。</span><span class="sxs-lookup"><span data-stu-id="27cc1-109">[Common](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Common): A common package that is shared between senders and receivers.</span></span>

* <span data-ttu-id="27cc1-110">[Sender](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Custom): 独自の webhook を他のユーザーに送信することをサポートするパッケージのセット。</span><span class="sxs-lookup"><span data-stu-id="27cc1-110">[Sender](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Custom): A set of packages supporting sending your own WebHooks to others.</span></span> <span data-ttu-id="27cc1-111">Webhook を送信する機能の詳細については、 [webhook の送信](sending/senders.md)に関するページを参照してください。</span><span class="sxs-lookup"><span data-stu-id="27cc1-111">The functionality for sending WebHooks is described in more detail in [Sending WebHooks](sending/senders.md).</span></span>

* <span data-ttu-id="27cc1-112">[レシーバー](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers): 他のユーザーから webhook を受け取ることをサポートするパッケージのセット。</span><span class="sxs-lookup"><span data-stu-id="27cc1-112">[Receivers](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers): A set of packages supporting receiving WebHooks from others.</span></span> <span data-ttu-id="27cc1-113">Webhook を受信する機能の詳細については、 [webhook の受信](receiving/index.md)に関するページを参照してください。</span><span class="sxs-lookup"><span data-stu-id="27cc1-113">The functionality for receiving WebHooks is described in more detail in [Receiving WebHooks](receiving/index.md).</span></span>
