---
uid: mvc/overview/getting-started/mvc-learning-sequence
title: MVC の推奨チュートリアルと記事 |Microsoft Docs
author: Rick-Anderson
description: このページには、ASP.NET MVC チュートリアルへのリンクと、それらに従うための推奨される手順が含まれています。
ms.author: riande
ms.date: 05/22/2015
ms.assetid: 8513a57a-2d45-4d6b-881c-15a01c5cbb1c
msc.legacyurl: /mvc/overview/getting-started/mvc-learning-sequence
msc.type: authoredcontent
ms.openlocfilehash: 46b089a896c6b1b92437ff1f5488214a3a0a9838
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78487738"
---
# <a name="mvc-recommended-tutorials-and-articles"></a>MVC 推奨チュートリアルと推奨記事

[Rick Anderson](https://twitter.com/RickAndMSFT)

<a id="pwd"></a>
## <a name="getting-started"></a>作業の開始

- [ASP.NET MVC 5 でのはじめに](introduction/getting-started.md)この11パートシリーズは、開始するのに適しています。
- [Pluralsight ASP.NET MVC 5 の基礎](https://pluralsight.com/training/Player?author=scott-allen&amp;name=aspdotnet-mvc5-fundamentals-m1-introduction&amp;mode=live&amp;clip=0&amp;course=aspdotnet-mvc5-fundamentals)(ビデオコース)
- [ASP.NET MVC の概要](https://channel9.msdn.com/Series/Introduction-to-ASP-NET-MVC)(Jon Galloway と Christopher Harrison)
- [ASP.NET MVC 5 アプリケーションのライフサイクル](lifecycle-of-an-aspnet-mvc-5-application.md)ASP.NET MVC 5 アプリのライフサイクルをグラフ化した PDF ドキュメント。

<a id="con"></a>
## <a name="working-with-data"></a>データの操作

- [MVC 5 を使用した EF 6 Code First のはじめに](getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)Tom Dykstra の受賞歴シリーズは、EF に深くダイブしています。

<a id="wj"></a>
## <a name="security"></a>Security

- [Auth と SQL DB を使用して ASP.NET MVC アプリを作成し、Azure にデプロイする](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/)この人気のあるチュートリアルでは、簡単なアプリを作成し、メンバーシップとロールを追加する手順について説明します。
- [Facebook、Twitter、LinkedIn、Google OAuth2 サインオンを使用して ASP.NET MVC 5 アプリを作成](../security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)するこのチュートリアルでは、ユーザーが Facebook、Twitter、LinkedIn、Microsoft、Google などの外部認証プロバイダーからの資格情報を使用して OAuth 2.0 を使用してログインできるようにする、ASP.NET MVC 5 web アプリケーションを構築する方法について説明します。
- [ログイン、電子メール確認、パスワードリセットを使用して secure ASP.NET MVC 5 web アプリを作成する](../security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md)最初に Id のシリーズでは、[確認リンクを再送信](../security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md#rsend)するためのコードが含まれています。
- [SMS と電子メール2要素認証を使用した ASP.NET MVC 5 アプリ](../security/aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md)2番目は Id シリーズです。
- [ASP.NET と Azure App Service にパスワードやその他の機密データを展開するためのベスト プラクティス](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)
- ASP.NET Identity `isPersistent` とセキュリティ cookie を使用した[SMS と電子メールを使用した2要素認証](../../../identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity.md)。ログオンする前にユーザーに検証済みの電子メールアカウントを要求するコード、SignInManager が2fa 要件を確認する方法などがあります。
- [ASP.NET Identity を使用したアカウントの確認とパスワードの回復](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)「ログインを使用して secure ASP.NET MVC 5 web アプリを作成する」で見つからない Id と、ユーザーが忘れたパスワードをリセットする方法など[、電子メール確認とパスワードリセット](../security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md)の詳細について説明します。

<a id="da"></a>
## <a name="azure"></a>Azure

- [Azure での ASP.NET web アプリの作成](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/)Azure にデプロイするための簡単で簡単なチュートリアルです。
- [Auth と SQL DB を使用して ASP.NET MVC アプリを作成し、Azure にデプロイする](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/)

<a id="perf"></a>
## <a name="performance-and-debugging"></a>パフォーマンスとデバッグ

- [Glimpse で ASP.NET MVC アプリをプロファイリングし、デバッグする](../performance/profile-and-debug-your-aspnet-mvc-app-with-glimpse.md)
