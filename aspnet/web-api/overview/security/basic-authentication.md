---
uid: web-api/overview/security/basic-authentication
title: ASP.NET Web API の基本認証 |Microsoft Docs
author: MikeWasson
description: ASP.NET Web API での基本認証の使用について説明します。
ms.author: riande
ms.date: 10/02/2014
ms.assetid: 41423767-0021-47c3-9e53-0021b457c39f
msc.legacyurl: /web-api/overview/security/basic-authentication
msc.type: authoredcontent
ms.openlocfilehash: 1470bd4b5abd5199b9a5105973b053812d643351
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78447634"
---
# <a name="basic-authentication-in-aspnet-web-api"></a>ASP.NET Web API での基本認証

[Mike Wasson](https://github.com/MikeWasson)

基本認証は[、RFC 2617、HTTP 認証 (基本およびダイジェストアクセス認証)](http://www.ietf.org/rfc/rfc2617.txt)で定義されています。

短所

- ユーザーの資格情報は、要求で送信されます。
- 資格情報はプレーンテキストとして送信されます。
- 資格情報は、すべての要求と共に送信されます。
- ブラウザーセッションを終了する場合を除き、ログアウトすることはできません。
- クロスサイト要求偽造 (CSRF) に対して脆弱CSRF 対策が必要です。

長所

- インターネット標準。
- すべての主要なブラウザーでサポートされています。
- 比較的単純なプロトコル。

基本認証は次のように機能します。

1. 要求に認証が必要な場合、サーバーは 401 (権限のない) を返します。 応答には、サーバーが基本認証をサポートしていることを示す、WWW 認証ヘッダーが含まれています。
2. クライアントは、承認ヘッダーにクライアント資格情報を使用して別の要求を送信します。 資格情報は、base64 でエンコードされた文字列 "name: password" として書式設定されます。 資格情報は暗号化されません。

基本認証は、"領域" のコンテキスト内で実行されます。 サーバーには、WWW-認証ヘッダーに領域の名前が含まれています。 ユーザーの資格情報は、その領域内で有効です。 領域の正確なスコープは、サーバーによって定義されます。 たとえば、リソースをパーティション分割するために複数の領域を定義することができます。

![](basic-authentication/_static/image1.png)

資格情報は暗号化されずに送信されるため、基本認証は HTTPS 経由でのみセキュリティで保護されます。 「 [WEB API での SSL の](working-with-ssl-in-web-api.md)使用」を参照してください。

基本認証は CSRF 攻撃にも脆弱です。 ユーザーが資格情報を入力すると、ブラウザーは、セッションの間、同じドメインへの後続の要求でそれらを自動的に送信します。 これには、AJAX 要求が含まれます。 「[クロスサイト要求偽造 (CSRF) 攻撃の防止](preventing-cross-site-request-forgery-csrf-attacks.md)」を参照してください。

## <a name="basic-authentication-with-iis"></a>IIS を使用した基本認証

IIS は基本認証をサポートしていますが、注意が必要です。ユーザーは、Windows 資格情報に対して認証されます。 つまり、ユーザーは、サーバーのドメインのアカウントを持っている必要があります。 公開された web サイトの場合は、通常、ASP.NET メンバーシッププロバイダーに対して認証する必要があります。

IIS を使用して基本認証を有効にするには、ASP.NET プロジェクトの web.config で認証モードを "Windows" に設定します。

[!code-xml[Main](basic-authentication/samples/sample1.xml)]

このモードでは、IIS は Windows 資格情報を使用して認証を行います。 さらに、IIS で基本認証を有効にする必要があります。 IIS マネージャーで、[機能ビュー] にアクセスし、[認証] を選択して、基本認証を有効にします。

![](basic-authentication/_static/image2.png)

Web API プロジェクトで、認証を必要とするコントローラーアクションの `[Authorize]` 属性を追加します。

クライアントは、要求で Authorization ヘッダーを設定することによって自身を認証します。 ブラウザークライアントは、この手順を自動的に実行します。 ブラウザー以外のクライアントは、ヘッダーを設定する必要があります。

## <a name="basic-authentication-with-custom-membership"></a>カスタムメンバーシップを使用した基本認証

前述のように、IIS に組み込まれている基本認証では Windows 資格情報が使用されます。 つまり、ホスティングサーバーでユーザーのアカウントを作成する必要があります。 ただし、インターネットアプリケーションの場合、ユーザーアカウントは通常、外部データベースに格納されます。

次のコードは、基本認証を実行する HTTP モジュールを示しています。 この例のダミーメソッドである `CheckPassword` メソッドを置き換えることで、ASP.NET メンバーシッププロバイダーを簡単にプラグインできます。

Web API 2 では、HTTP モジュールの代わりに、[認証フィルター](authentication-filters.md)または[OWIN ミドルウェア](../../../aspnet/overview/owin-and-katana/index.md)を記述することを検討してください。

[!code-csharp[Main](basic-authentication/samples/sample2.cs)]

HTTP モジュールを有効にするには、次の内容を**system.webserver**セクションの web.config ファイルに追加します。

[!code-xml[Main](basic-authentication/samples/sample3.xml?highlight=4)]

"自分の Assemblyname" は、アセンブリの名前 ("dll" 拡張を含まない) に置き換えます。

フォームや Windows 認証など、他の認証方式を無効にする必要があります。
