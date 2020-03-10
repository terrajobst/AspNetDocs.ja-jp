---
uid: web-api/overview/security/forms-authentication
title: ASP.NET Web API | のフォーム認証Microsoft Docs
author: MikeWasson
description: ASP.NET Web API でのフォーム認証の使用について説明します。
ms.author: riande
ms.date: 12/12/2012
ms.assetid: 9f06c1f2-ffaa-4831-94a0-2e4a3befdf07
msc.legacyurl: /web-api/overview/security/forms-authentication
msc.type: authoredcontent
ms.openlocfilehash: 147bfab76e48497f35a72b28cd935f40ec4193bf
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484378"
---
# <a name="forms-authentication-in-aspnet-web-api"></a>ASP.NET Web API でのフォーム認証

[Mike Wasson](https://github.com/MikeWasson)

フォーム認証では、HTML フォームを使用してユーザーの資格情報をサーバーに送信します。 インターネット標準ではありません。 ユーザーが HTML フォームを操作できるように、フォーム認証は web、web アプリケーションから呼び出される API の適切なのみ。

| 長所 | 短所 |
| --- | --- |
| -実装が簡単: ASP.NET に組み込まれています。 -ASP.NET メンバーシッププロバイダーを使用します。これにより、ユーザーアカウントの管理が容易になります。 | -標準の HTTP 認証機構ではありません。では、標準の Authorization ヘッダーではなく HTTP クッキーが使用されます。 -ブラウザークライアントが必要です。 -資格情報はプレーンテキストとして送信されます。 -クロスサイト要求偽造 (CSRF) に対して脆弱です。CSRF 対策が必要です。 -ブラウザー以外のクライアントから使用するのは困難です。 ログインにはブラウザーが必要です。 -ユーザー資格情報は、要求で送信されます。 -Cookie を無効にするユーザーもいます。 |

について簡単に、ASP.NET フォーム認証は、次のように動作します。

1. クライアントは、認証を必要とするリソースを要求します。
2. ユーザーが認証されていない場合は、サーバーから HTTP 302 (検出) が返され、ログインページにリダイレクトされます。
3. ユーザーは資格情報を入力し、フォームを送信します。
4. サーバーは、元の URI にリダイレクトする別の HTTP 302 を返します。 この応答には、認証クッキーが含まれます。
5. クライアントはリソースを再度要求します。 要求に認証クッキーが含まれているため、サーバーは要求を許可します。

![](forms-authentication/_static/image1.png)

詳細については、「[フォーム認証の概要](../../../web-forms/overview/older-versions-security/introduction/an-overview-of-forms-authentication-cs.md)」を参照してください。

## <a name="using-forms-authentication-with-web-api"></a>Web API でフォーム認証を使用する

フォーム認証を使用するアプリケーションを作成するには、MVC 4 プロジェクトウィザードで [インターネットアプリケーション] テンプレートを選択します。 このテンプレートは、アカウント管理用の MVC コントローラーを作成します。 ASP.NET フォール2012更新プログラムで利用可能な "シングルページアプリケーション" テンプレートを使用することもできます。

Web API コントローラーでは、「 [[承認] 属性の使用](authentication-and-authorization-in-aspnet-web-api.md#auth3)」で説明されているように、`[Authorize]` 属性を使用してアクセスを制限できます。

フォーム認証では、セッション cookie を使用して要求を認証します。 ブラウザーは、関連するすべての cookie を送信先の web サイトに自動的に送信します。 この機能により、クロスサイト要求偽造 (CSRF) 攻撃に対してフォーム認証が脆弱になる可能性があります。「[クロスサイト要求偽造 (csrf) 攻撃の防止](preventing-cross-site-request-forgery-csrf-attacks.md)」を参照してください。

フォーム認証では、ユーザーの資格情報は暗号化されません。 そのため、SSL で使用しない限り、フォーム認証は安全ではありません。 「 [WEB API での SSL の](working-with-ssl-in-web-api.md)使用」を参照してください。
