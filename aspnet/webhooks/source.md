---
uid: webhooks/source
title: ASP.NET Webhook のソース コードと NuGet パッケージ |Microsoft Docs
author: rick-anderson
description: ASP.NET Webhook のソース コードと NuGet パッケージへのリンク
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 91a62bfa-ea3a-41f9-a2e1-e90d2c8fc8ca
ms.openlocfilehash: f88d9247f9d8aa0c5edc1ffc462be21d9319a725
ms.sourcegitcommit: dd0dc556a3d99a31d8fdbc763e9a2e53f3441b70
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2019
ms.locfileid: "67410800"
---
# <a name="aspnet-webhooks-source-code-and-nuget-packages"></a>ASP.NET Webhook のソース コードと NuGet パッケージ

Microsoft ASP.NET Webhook はモジュールの Microsoft ASP.NET ファミリの一部でありとしてホストされる、 [GitHub でオープン ソース プロジェクト](https://github.com/aspnet/WebHooks)します。 つまり、投稿をそのまま使用しましたを参照してください、[投稿に関するガイドライン](https://github.com/aspnet/Home/blob/master/CONTRIBUTING.md)プル要求を送信する前にします。

このオンライン ドキュメントの読み取りを行うようになりましたがもとしてホストされる[GitHub でオープン ソース](http://docs.asp.net/en/latest/contribute/style-guide.html#style-guide)も投稿を受け入れるとします。

## <a name="nuget-packages"></a>NuGet パッケージ

[NuGet パッケージの](https://nuget.org/packages?q=Microsoft.AspNet.WebHooks)は 3 つの部分に分けられます。

* [一般的な](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Common):送信者と受信者の間で共有される一般的なパッケージです。

* [送信者](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Custom):他のユーザーに、独自の Webhook の送信をサポートしているパッケージのセット。 Webhook に送信するための機能がで詳しく説明されている[送信 Webhook](sending/senders)します。

* [受信側](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers):他のユーザーからの Webhook の受信をサポートしているパッケージのセット。 Webhook を受信するための機能がで詳しく説明されている[受信 Webhook](receiving/index.md)します。
