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
# <a name="aspnet-webhooks-source-code-and-nuget-packages"></a>ASP.NET Webhook のソースコードと NuGet パッケージ

Microsoft ASP.NET Webhook は、Microsoft ASP.NET のモジュールファミリに含まれており、 [GitHub でオープンソースプロジェクト](https://github.com/aspnet/WebHooks)としてホストされています。 これは投稿を受け入れることを意味しますが、プル要求を送信する前に[投稿のガイドライン](https://github.com/aspnet/Home/blob/master/CONTRIBUTING.md)を参照してください。

ここで読んでいるこのオンラインドキュメントは、 [GitHub のオープンソース](http://docs.asp.net/en/latest/contribute/style-guide.html#style-guide)としてもホストされており、投稿も受け入れます。

## <a name="nuget-packages"></a>NuGet パッケージ

[NuGet パッケージ](https://nuget.org/packages?q=Microsoft.AspNet.WebHooks)は、次の3つの部分に分かれています。

* [共通](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Common): 送信側と受信側の間で共有される共通のパッケージ。

* [Sender](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Custom): 独自の webhook を他のユーザーに送信することをサポートするパッケージのセット。 Webhook を送信する機能の詳細については、 [webhook の送信](sending/senders.md)に関するページを参照してください。

* [レシーバー](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers): 他のユーザーから webhook を受け取ることをサポートするパッケージのセット。 Webhook を受信する機能の詳細については、 [webhook の受信](receiving/index.md)に関するページを参照してください。
