---
uid: web-api/overview/security/authentication-and-authorization-in-aspnet-web-api
title: ASP.NET Web API での認証と承認 |Microsoft Docs
author: MikeWasson
description: ASP.NET Web API での認証と承認の概要について説明します。
ms.author: riande
ms.date: 11/27/2012
ms.assetid: 6dfb51ea-9f4d-4e70-916c-8ef8344a88d6
msc.legacyurl: /web-api/overview/security/authentication-and-authorization-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 368d2b9456d12b2bb4063a23333e5c8837faa3b8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484420"
---
# <a name="authentication-and-authorization-in-aspnet-web-api"></a>ASP.NET Web API での認証と承認

[Mike Wasson](https://github.com/MikeWasson)

Web API を作成しましたが、それへのアクセスを制御する必要があります。 この一連の記事では、承認されていないユーザーから web API をセキュリティで保護するためのオプションについて説明します。 このシリーズでは、認証と承認の両方について説明します。

- *認証*は、ユーザーの id を認識しています。 たとえば、Alice はユーザー名とパスワードを使用してログインし、サーバーはパスワードを使用して Alice を認証します。
- *承認*は、ユーザーがアクションの実行を許可されているかどうかを判断するためのものです。 たとえば、Alice はリソースを取得するためのアクセス許可を持っていますが、リソースを作成することはできません。

このシリーズの最初の記事では、ASP.NET Web API での認証と承認の概要について説明します。 その他のトピックでは、Web API の一般的な認証シナリオについて説明します。

> [!NOTE]
> このシリーズをレビューし、Rick Anderson、Levi Broderick、Dorrans、Tom Dykstra、Hongmei Ge、David Matson、Daniel Roth、Tim Teebken のお客様のご意見をお寄せいただき、ありがとうございます。

## <a name="authentication"></a>認証

Web API は、ホストで認証が行われることを前提としています。 Web ホストの場合、ホストは IIS で、認証に HTTP モジュールを使用します。 IIS または ASP.NET に組み込まれている認証モジュールのいずれかを使用するようにプロジェクトを構成するか、独自の HTTP モジュールを記述してカスタム認証を実行することができます。

ホストがユーザーを認証すると、*プリンシパル*が作成されます。これは、コードが実行されているセキュリティコンテキストを表す[IPrincipal](https://msdn.microsoft.com/library/System.Security.Principal.IPrincipal.aspx)オブジェクトです。 ホストは、 **thread.currentprincipal**を設定することによって、プリンシパルを現在のスレッドにアタッチします。 プリンシパルには、ユーザーに関する情報を含む、関連付けられた**id**オブジェクトが含まれています。 ユーザーが認証されると、 **IsAuthenticated**プロパティは**true**を返します。 匿名要求の場合、 **Isauthenticated**は**false**を返します。 プリンシパルの詳細については、「[ロールベースのセキュリティ](https://msdn.microsoft.com/library/shz8h065.aspx)」を参照してください。

### <a name="http-message-handlers-for-authentication"></a>認証用の HTTP メッセージハンドラー

認証にはホストを使用するのではなく、 [HTTP メッセージハンドラー](../advanced/http-message-handlers.md)に認証ロジックを配置することができます。 この場合、メッセージハンドラーは HTTP 要求を調べ、プリンシパルを設定します。

認証にメッセージハンドラーを使用する必要があるのはいつですか。 いくつかのトレードオフを次に示します。

- HTTP モジュールは、ASP.NET パイプラインを経由するすべての要求を認識します。 メッセージハンドラーには、Web API にルーティングされる要求のみが表示されます。
- ルートごとのメッセージハンドラーを設定できます。これにより、特定のルートに認証スキームを適用できます。
- HTTP モジュールは IIS に固有のものです。 メッセージハンドラーは、ホストに依存しないため、web ホストと自己ホストの両方で使用できます。
- HTTP モジュールは、IIS のログ記録や監査などに関与します。
- HTTP モジュールは、パイプラインで以前に実行されています。 メッセージハンドラーで認証を処理する場合、プリンシパルはハンドラーが実行されるまで設定されません。 さらに、応答がメッセージハンドラーから外れると、プリンシパルは前のプリンシパルに戻ります。

一般に、自己ホストをサポートする必要がない場合は、HTTP モジュールを使用することをお勧めします。 自己ホストをサポートする必要がある場合は、メッセージハンドラーを検討してください。

### <a name="setting-the-principal"></a>プリンシパルの設定

アプリケーションでカスタム認証ロジックを実行する場合は、次の2つの場所でプリンシパルを設定する必要があります。

- **Thread.currentprincipal**。 このプロパティは、.NET でスレッドのプリンシパルを設定するための標準的な方法です。
- **HttpContext. Current. User**. このプロパティは、ASP.NET に固有です。

次のコードは、プリンシパルを設定する方法を示しています。

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample1.cs)]

Web ホストの場合、両方の場所でプリンシパルを設定する必要があります。そうしないと、セキュリティコンテキストが不整合になる可能性があります。 ただし、自己ホストの場合、 **HttpContext**は null になります。 コードがホストに依存しないようにするには、以下に示すように、null を確認してから**HttpContext**に割り当てます。

## <a name="authorization"></a>承認

承認は、後で、コントローラーに近いパイプラインで行われます。 これにより、リソースへのアクセスを許可するときにより詳細な選択を行うことができます。

- *承認フィルター*は、コントローラーアクションの前に実行されます。 要求が承認されていない場合、フィルターはエラー応答を返し、アクションは呼び出されません。
- コントローラーアクション内では、 **ApiController**プロパティから現在のプリンシパルを取得できます。 たとえば、ユーザー名に基づいてリソースの一覧をフィルター処理し、そのユーザーに属するリソースのみを返すことができます。

![](authentication-and-authorization-in-aspnet-web-api/_static/image1.png)

<a id="auth3"></a>
### <a name="using-the-authorize-attribute"></a>[承認] 属性の使用

Web API には、組み込みの承認フィルターである[Authorizeattribute](https://msdn.microsoft.com/library/system.web.http.authorizeattribute.aspx)が用意されています。 このフィルターは、ユーザーが認証されているかどうかを確認します。 そうでない場合は、アクションを呼び出さずに HTTP 状態コード 401 (未承認) が返されます。

フィルターは、グローバルに、コントローラーレベルで、または個々のアクションのレベルで適用できます。

**グローバル**: すべての Web API コントローラーのアクセスを制限するには、 **authorizeattribute**フィルターをグローバルフィルター一覧に追加します。

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample2.cs)]

**コントローラー**: 特定のコントローラーへのアクセスを制限するには、フィルターを属性としてコントローラーに追加します。

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample3.cs)]

**アクション**: 特定のアクションに対するアクセスを制限するには、属性をアクションメソッドに追加します。

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample4.cs)]

または、`[AllowAnonymous]` 属性を使用して、コントローラーを制限し、特定のアクションへの匿名アクセスを許可することもできます。 次の例では、`Post` メソッドが制限されていますが、`Get` メソッドは匿名アクセスを許可しています。

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample5.cs)]

前の例では、フィルターを使用して、認証されたユーザーが制限されたメソッドにアクセスすることを許可しています。匿名ユーザーのみが保持されます。特定のユーザーまたは特定のロールのユーザーへのアクセスを制限することもできます。

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample6.cs)]

> [!NOTE]
> Web API コントローラーの**Authorizeattribute**フィルター**は、system.web 名前空間**にあります。 **System.web 名前空間**には、web API コントローラーと互換性のない mvc コントローラーに似たフィルターがあります。

### <a name="custom-authorization-filters"></a>カスタム承認フィルター

カスタム承認フィルターを作成するには、次のいずれかの型から派生します。

- **Authorizeattribute**。 現在のユーザーとユーザーのロールに基づいて承認ロジックを実行するように、このクラスを拡張します。
- **Authorizationfilterattribute**。 このクラスを拡張して、現在のユーザーまたはロールに基づいているとは限らない同期承認ロジックを実行します。
- **IAuthorizationFilter**。 非同期承認ロジックを実行するには、このインターフェイスを実装します。たとえば、承認ロジックが非同期 i/o またはネットワーク呼び出しを行う場合です。 (認証ロジックが CPU にバインドされている場合は、 **Authorizationfilterattribute**から派生する方が簡単です。これは、非同期メソッドを記述する必要がないためです)。

次の図は、 **Authorizeattribute**クラスのクラス階層を示しています。

![](authentication-and-authorization-in-aspnet-web-api/_static/image2.png)

### <a name="authorization-inside-a-controller-action"></a>コントローラーアクション内の承認

場合によっては、要求の続行を許可しても、プリンシパルに基づいて動作を変更することがあります。 たとえば、返される情報は、ユーザーのロールによって変わる可能性があります。 コントローラーメソッド内では、 **ApiController**プロパティから現在のプリンシパルを取得できます。

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample7.cs)]
