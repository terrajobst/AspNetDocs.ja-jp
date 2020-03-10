---
uid: signalr/overview/older-versions/hub-authorization
title: SignalR Hub の認証と承認 (SignalR 1.x) |Microsoft Docs
author: bradygaster
description: このトピックでは、ハブメソッドにアクセスできるユーザーまたはロールを制限する方法について説明します。
ms.author: bradyg
ms.date: 10/17/2013
ms.assetid: 3d2dfc0e-eac2-4076-a468-325d3d01cc7b
msc.legacyurl: /signalr/overview/older-versions/hub-authorization
msc.type: authoredcontent
ms.openlocfilehash: 8182677c8931f060d98d17008b16ad545bee4e69
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78450040"
---
# <a name="authentication-and-authorization-for-signalr-hubs-signalr-1x"></a><span data-ttu-id="63f49-103">SignalR ハブの認証と承認 (SignalR 1.x)</span><span class="sxs-lookup"><span data-stu-id="63f49-103">Authentication and Authorization for SignalR Hubs (SignalR 1.x)</span></span>

<span data-ttu-id="63f49-104">[Fletcher (パトリック](https://github.com/pfletcher))、 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="63f49-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="63f49-105">このトピックでは、ハブメソッドにアクセスできるユーザーまたはロールを制限する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="63f49-105">This topic describes how to restrict which users or roles can access hub methods.</span></span>

## <a name="overview"></a><span data-ttu-id="63f49-106">概要</span><span class="sxs-lookup"><span data-stu-id="63f49-106">Overview</span></span>

<span data-ttu-id="63f49-107">このトピックには、次のセクションが含まれます。</span><span class="sxs-lookup"><span data-stu-id="63f49-107">This topic contains the following sections:</span></span>

- [<span data-ttu-id="63f49-108">属性の承認</span><span class="sxs-lookup"><span data-stu-id="63f49-108">Authorize attribute</span></span>](#authorizeattribute)
- [<span data-ttu-id="63f49-109">すべてのハブに認証を要求する</span><span class="sxs-lookup"><span data-stu-id="63f49-109">Require authentication for all hubs</span></span>](#requireauth)
- [<span data-ttu-id="63f49-110">カスタマイズされた承認</span><span class="sxs-lookup"><span data-stu-id="63f49-110">Customized authorization</span></span>](#custom)
- [<span data-ttu-id="63f49-111">クライアントに認証情報を渡す</span><span class="sxs-lookup"><span data-stu-id="63f49-111">Pass authentication information to clients</span></span>](#passauth)
- [<span data-ttu-id="63f49-112">.NET クライアントの認証オプション</span><span class="sxs-lookup"><span data-stu-id="63f49-112">Authentication options for .NET clients</span></span>](#authoptions)

    - [<span data-ttu-id="63f49-113">フォーム認証を使用した Cookie</span><span class="sxs-lookup"><span data-stu-id="63f49-113">Cookie with Forms Authentication</span></span>](#cookie)
    - <span data-ttu-id="63f49-114">[[Windows 認証]](#windows)</span><span class="sxs-lookup"><span data-stu-id="63f49-114">[Windows Authentication](#windows)</span></span>
    - [<span data-ttu-id="63f49-115">接続ヘッダー</span><span class="sxs-lookup"><span data-stu-id="63f49-115">Connection header</span></span>](#header)
    - <span data-ttu-id="63f49-116">[[MSSQLSERVER のプロトコルのプロパティ]](#certificate)</span><span class="sxs-lookup"><span data-stu-id="63f49-116">[Certificate](#certificate)</span></span>

<a id="authorizeattribute"></a>

## <a name="authorize-attribute"></a><span data-ttu-id="63f49-117">属性の承認</span><span class="sxs-lookup"><span data-stu-id="63f49-117">Authorize attribute</span></span>

<span data-ttu-id="63f49-118">SignalR は、hub またはメソッドへのアクセス権を持つユーザーまたはロールを指定するための[承認](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx)属性を提供します。</span><span class="sxs-lookup"><span data-stu-id="63f49-118">SignalR provides the [Authorize](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx) attribute to specify which users or roles have access to a hub or method.</span></span> <span data-ttu-id="63f49-119">この属性は `Microsoft.AspNet.SignalR` 名前空間にあります。</span><span class="sxs-lookup"><span data-stu-id="63f49-119">This attribute is located in the `Microsoft.AspNet.SignalR` namespace.</span></span> <span data-ttu-id="63f49-120">`Authorize` 属性はハブのハブまたは特定のメソッドのいずれかに適用します。</span><span class="sxs-lookup"><span data-stu-id="63f49-120">You apply the `Authorize` attribute to either a hub or particular methods in a hub.</span></span> <span data-ttu-id="63f49-121">`Authorize` 属性をハブクラスに適用すると、指定された承認要件がハブのすべてのメソッドに適用されます。</span><span class="sxs-lookup"><span data-stu-id="63f49-121">When you apply the `Authorize` attribute to a hub class, the specified authorization requirement is applied to all of the methods in the hub.</span></span> <span data-ttu-id="63f49-122">適用できるさまざまな種類の承認要件を以下に示します。</span><span class="sxs-lookup"><span data-stu-id="63f49-122">The different types of authorization requirements that you can apply are shown below.</span></span> <span data-ttu-id="63f49-123">`Authorize` 属性を指定しない場合、ハブのすべてのパブリックメソッドを、ハブに接続されているクライアントで使用できます。</span><span class="sxs-lookup"><span data-stu-id="63f49-123">Without the `Authorize` attribute, all public methods on the hub are available to a client that is connected to the hub.</span></span>

<span data-ttu-id="63f49-124">Web アプリケーションで "Admin" という名前のロールを定義している場合は、次のコードを使用して、そのロールのユーザーのみがハブにアクセスできるように指定できます。</span><span class="sxs-lookup"><span data-stu-id="63f49-124">If you have defined a role named "Admin" in your web application, you could specify that only users in that role can access a hub with the following code.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample1.cs)]

<span data-ttu-id="63f49-125">または、次に示すように、すべてのユーザーが使用できる1つのメソッドと、認証されたユーザーのみが使用できる2番目のメソッドをハブに含めるように指定できます。</span><span class="sxs-lookup"><span data-stu-id="63f49-125">Or, you can specify that a hub contains one method that is available to all users, and a second method that is only available to authenticated users, as shown below.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample2.cs)]

<span data-ttu-id="63f49-126">次の例では、さまざまな承認シナリオに対処します。</span><span class="sxs-lookup"><span data-stu-id="63f49-126">The following examples address different authorization scenarios:</span></span>

- <span data-ttu-id="63f49-127">`[Authorize]`-認証されたユーザーのみ</span><span class="sxs-lookup"><span data-stu-id="63f49-127">`[Authorize]` – only authenticated users</span></span>
- <span data-ttu-id="63f49-128">`[Authorize(Roles = "Admin,Manager")]`-指定したロール内の認証されたユーザーのみ</span><span class="sxs-lookup"><span data-stu-id="63f49-128">`[Authorize(Roles = "Admin,Manager")]` – only authenticated users in the specified roles</span></span>
- <span data-ttu-id="63f49-129">`[Authorize(Users = "user1,user2")]` –指定されたユーザー名を持つ認証済みユーザーのみ</span><span class="sxs-lookup"><span data-stu-id="63f49-129">`[Authorize(Users = "user1,user2")]` – only authenticated users with the specified user names</span></span>
- <span data-ttu-id="63f49-130">`[Authorize(RequireOutgoing=false)]`: 認証されたユーザーのみがハブを呼び出すことができますが、サーバーからクライアントへの呼び出しは、特定のユーザーのみがメッセージを送信できるが、他のユーザーがメッセージを受信できる場合など、承認によって制限されません。</span><span class="sxs-lookup"><span data-stu-id="63f49-130">`[Authorize(RequireOutgoing=false)]` – only authenticated users can invoke the hub, but calls from the server back to clients are not limited by authorization, such as, when only certain users can send a message but all others can receive the message.</span></span> <span data-ttu-id="63f49-131">RequireOutgoing プロパティは、ハブ内の個々のメソッドではなく、ハブ全体にのみ適用できます。</span><span class="sxs-lookup"><span data-stu-id="63f49-131">The RequireOutgoing property can only be applied to the entire hub, not on individuals methods within the hub.</span></span> <span data-ttu-id="63f49-132">RequireOutgoing が false に設定されていない場合、承認要件を満たすユーザーのみがサーバーから呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="63f49-132">When RequireOutgoing is not set to false, only users that meet the authorization requirement are called from the server.</span></span>

<a id="requireauth"></a>

## <a name="require-authentication-for-all-hubs"></a><span data-ttu-id="63f49-133">すべてのハブに認証を要求する</span><span class="sxs-lookup"><span data-stu-id="63f49-133">Require authentication for all hubs</span></span>

<span data-ttu-id="63f49-134">アプリケーションの起動時に[requireauthentication](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubpipelineextensions.requireauthentication(v=vs.111).aspx)メソッドを呼び出すことにより、アプリケーション内のすべてのハブおよびハブメソッドに対して認証を要求できます。</span><span class="sxs-lookup"><span data-stu-id="63f49-134">You can require authentication for all hubs and hub methods in your application by calling the [RequireAuthentication](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubpipelineextensions.requireauthentication(v=vs.111).aspx) method when the application starts.</span></span> <span data-ttu-id="63f49-135">複数のハブがあり、そのすべてに対して認証要件を強制する場合は、この方法を使用できます。</span><span class="sxs-lookup"><span data-stu-id="63f49-135">You might use this method when you have multiple hubs and want to enforce an authentication requirement for all of them.</span></span> <span data-ttu-id="63f49-136">この方法では、ロール、ユーザー、または送信の承認を指定することはできません。</span><span class="sxs-lookup"><span data-stu-id="63f49-136">With this method, you cannot specify role, user, or outgoing authorization.</span></span> <span data-ttu-id="63f49-137">ハブメソッドへのアクセスが認証されたユーザーに制限されることのみを指定できます。</span><span class="sxs-lookup"><span data-stu-id="63f49-137">You can only specify that access to the hub methods is restricted to authenticated users.</span></span> <span data-ttu-id="63f49-138">ただし、承認属性をハブまたはメソッドに適用して、追加の要件を指定することもできます。</span><span class="sxs-lookup"><span data-stu-id="63f49-138">However, you can still apply the Authorize attribute to hubs or methods to specify additional requirements.</span></span> <span data-ttu-id="63f49-139">属性で指定する要件は、認証の基本要件に加えて適用されます。</span><span class="sxs-lookup"><span data-stu-id="63f49-139">Any requirement you specify in attributes is applied in addition to the basic requirement of authentication.</span></span>

<span data-ttu-id="63f49-140">次の例は、すべてのハブメソッドを認証されたユーザーに制限する global.asax ファイルを示しています。</span><span class="sxs-lookup"><span data-stu-id="63f49-140">The following example shows a Global.asax file which restricts all hub methods to authenticated users.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample3.cs)]

<span data-ttu-id="63f49-141">SignalR 要求が処理された後に `RequireAuthentication()` メソッドを呼び出すと、SignalR は例外 `InvalidOperationException` をスローします。</span><span class="sxs-lookup"><span data-stu-id="63f49-141">If you call the `RequireAuthentication()` method after a SignalR request has been processed, SignalR will throw a `InvalidOperationException` exception.</span></span> <span data-ttu-id="63f49-142">パイプラインが呼び出された後にモジュールを HubPipeline に追加することはできないため、この例外がスローされます。</span><span class="sxs-lookup"><span data-stu-id="63f49-142">This exception is thrown because you cannot add a module to the HubPipeline after the pipeline has been invoked.</span></span> <span data-ttu-id="63f49-143">前の例では、最初の要求を処理する前に1回実行される `Application_Start` メソッドで `RequireAuthentication` メソッドを呼び出しています。</span><span class="sxs-lookup"><span data-stu-id="63f49-143">The previous example shows calling the `RequireAuthentication` method in the `Application_Start` method which is executed one time prior to handling the first request.</span></span>

<a id="custom"></a>

## <a name="customized-authorization"></a><span data-ttu-id="63f49-144">カスタマイズされた承認</span><span class="sxs-lookup"><span data-stu-id="63f49-144">Customized authorization</span></span>

<span data-ttu-id="63f49-145">承認を決定する方法をカスタマイズする必要がある場合は、`AuthorizeAttribute` から派生したクラスを作成し、 [userauthorized](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute.userauthorized(v=vs.111).aspx)メソッドをオーバーライドできます。</span><span class="sxs-lookup"><span data-stu-id="63f49-145">If you need to customize how authorization is determined, you can create a class that derives from `AuthorizeAttribute` and override the [UserAuthorized](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute.userauthorized(v=vs.111).aspx) method.</span></span> <span data-ttu-id="63f49-146">このメソッドは、要求を完了する権限がユーザーに与えられているかどうかを判断するために、各要求に対して呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="63f49-146">This method is called for each request to determine whether the user is authorized to complete the request.</span></span> <span data-ttu-id="63f49-147">オーバーライドされたメソッドには、承認シナリオに必要なロジックを指定します。</span><span class="sxs-lookup"><span data-stu-id="63f49-147">In the overridden method, you provide the necessary logic for your authorization scenario.</span></span> <span data-ttu-id="63f49-148">次の例は、クレームベースの id を通じて承認を強制する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="63f49-148">The following example shows how to enforce authorization through claims-based identity.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample4.cs)]

<a id="passauth"></a>

## <a name="pass-authentication-information-to-clients"></a><span data-ttu-id="63f49-149">クライアントに認証情報を渡す</span><span class="sxs-lookup"><span data-stu-id="63f49-149">Pass authentication information to clients</span></span>

<span data-ttu-id="63f49-150">場合によっては、クライアントで実行されるコードで認証情報を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="63f49-150">You may need to use authentication information in the code that runs on the client.</span></span> <span data-ttu-id="63f49-151">クライアントでメソッドを呼び出すときに、必要な情報を渡します。</span><span class="sxs-lookup"><span data-stu-id="63f49-151">You pass the required information when calling the methods on the client.</span></span> <span data-ttu-id="63f49-152">たとえば、次に示すように、チャットアプリケーションのメソッドは、メッセージを投稿する人のユーザー名をパラメーターとして渡すことができます。</span><span class="sxs-lookup"><span data-stu-id="63f49-152">For example, a chat application method could pass as a parameter the user name of the person posting a message, as shown below.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample5.cs)]

<span data-ttu-id="63f49-153">または、次に示すように、認証情報を表すオブジェクトを作成し、そのオブジェクトをパラメーターとして渡すことができます。</span><span class="sxs-lookup"><span data-stu-id="63f49-153">Or, you can create an object to represent the authentication information and pass that object as a parameter, as shown below.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample6.cs)]

<span data-ttu-id="63f49-154">悪意のあるユーザーがそのクライアントからの要求を模倣するために使用する可能性があるため、1つのクライアントの接続 id を他のクライアントに渡すことはできません。</span><span class="sxs-lookup"><span data-stu-id="63f49-154">You should never pass one client's connection id to other clients, as a malicious user could use it to mimic a request from that client.</span></span>

<a id="authoptions"></a>

## <a name="authentication-options-for-net-clients"></a><span data-ttu-id="63f49-155">.NET クライアントの認証オプション</span><span class="sxs-lookup"><span data-stu-id="63f49-155">Authentication options for .NET clients</span></span>

<span data-ttu-id="63f49-156">認証されたユーザーに限定されたハブと対話するコンソールアプリなどの .NET クライアントがある場合は、認証資格情報をクッキー、接続ヘッダー、または証明書に渡すことができます。</span><span class="sxs-lookup"><span data-stu-id="63f49-156">When you have a .NET client, such as a console app, which interacts with a hub that is limited to authenticated users, you can pass the authentication credentials in a cookie, the connection header, or a certificate.</span></span> <span data-ttu-id="63f49-157">このセクションの例では、これらの異なる方法を使用してユーザーを認証する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="63f49-157">The examples in this section show how to use those different methods for authenticating a user.</span></span> <span data-ttu-id="63f49-158">これらは、完全に機能している SignalR アプリではありません。</span><span class="sxs-lookup"><span data-stu-id="63f49-158">They are not fully-functional SignalR apps.</span></span> <span data-ttu-id="63f49-159">SignalR を使用した .NET クライアントの詳細については、「 [HUB API Guide-.Net Client](../guide-to-the-api/hubs-api-guide-net-client.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="63f49-159">For more information about .NET clients with SignalR, see [Hubs API Guide - .NET Client](../guide-to-the-api/hubs-api-guide-net-client.md).</span></span>

<a id="cookie"></a>

### <a name="cookie"></a><span data-ttu-id="63f49-160">Cookie</span><span class="sxs-lookup"><span data-stu-id="63f49-160">Cookie</span></span>

<span data-ttu-id="63f49-161">ASP.NET Forms 認証を使用するハブと .NET クライアントが通信する場合、接続で認証 cookie を手動で設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="63f49-161">When your .NET client interacts with a hub that uses ASP.NET Forms Authentication, you will need to manually set the authentication cookie on the connection.</span></span> <span data-ttu-id="63f49-162">[HubConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.hubs.hubconnection(v=vs.111).aspx)オブジェクトの `CookieContainer` プロパティに cookie を追加します。</span><span class="sxs-lookup"><span data-stu-id="63f49-162">You add the cookie to the `CookieContainer` property on the [HubConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.hubs.hubconnection(v=vs.111).aspx) object.</span></span> <span data-ttu-id="63f49-163">次の例は、web ページから認証クッキーを取得し、その cookie を接続に追加するコンソールアプリを示しています。</span><span class="sxs-lookup"><span data-stu-id="63f49-163">The following example shows a console app that retrieves an authentication cookie from a web page and adds that cookie to the connection.</span></span> <span data-ttu-id="63f49-164">この例の URL `https://www.contoso.com/RemoteLogin` は、作成する必要がある web ページを指しています。</span><span class="sxs-lookup"><span data-stu-id="63f49-164">The URL `https://www.contoso.com/RemoteLogin` in the example points to a web page that you would need to create.</span></span> <span data-ttu-id="63f49-165">このページでは、ポストされたユーザー名とパスワードを取得し、資格情報を使用してユーザーをログインしようとします。</span><span class="sxs-lookup"><span data-stu-id="63f49-165">The page would retrieve the posted user name and password, and attempt to log in the user with the credentials.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample7.cs)]

<span data-ttu-id="63f49-166">コンソールアプリによって資格情報が www.contoso.com/RemoteLogin にポストされ、次の分離コードファイルを含む空のページを参照できます。</span><span class="sxs-lookup"><span data-stu-id="63f49-166">The console app posts the credentials to www.contoso.com/RemoteLogin which could refer to an empty page that contains the following code-behind file.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample8.cs)]

<a id="windows"></a>

### <a name="windows-authentication"></a><span data-ttu-id="63f49-167">Windows 認証</span><span class="sxs-lookup"><span data-stu-id="63f49-167">Windows authentication</span></span>

<span data-ttu-id="63f49-168">Windows 認証を使用する場合は、 [DefaultCredentials](https://msdn.microsoft.com/library/system.net.credentialcache.defaultcredentials.aspx)プロパティを使用して、現在のユーザーの資格情報を渡すことができます。</span><span class="sxs-lookup"><span data-stu-id="63f49-168">When using Windows authentication, you can pass the current user's credentials by using the [DefaultCredentials](https://msdn.microsoft.com/library/system.net.credentialcache.defaultcredentials.aspx) property.</span></span> <span data-ttu-id="63f49-169">接続の資格情報を DefaultCredentials の値に設定します。</span><span class="sxs-lookup"><span data-stu-id="63f49-169">You set the credentials for the connection to the value of the DefaultCredentials.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample9.cs?highlight=6)]

<a id="header"></a>

### <a name="connection-header"></a><span data-ttu-id="63f49-170">接続ヘッダー</span><span class="sxs-lookup"><span data-stu-id="63f49-170">Connection header</span></span>

<span data-ttu-id="63f49-171">アプリケーションが cookie を使用していない場合は、接続ヘッダーにユーザー情報を渡すことができます。</span><span class="sxs-lookup"><span data-stu-id="63f49-171">If your application is not using cookies, you can pass user information in the connection header.</span></span> <span data-ttu-id="63f49-172">たとえば、接続ヘッダーにトークンを渡すことができます。</span><span class="sxs-lookup"><span data-stu-id="63f49-172">For example, you can pass a token in the connection header.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample10.cs?highlight=6)]

<span data-ttu-id="63f49-173">次に、ハブでユーザーのトークンを確認します。</span><span class="sxs-lookup"><span data-stu-id="63f49-173">Then, in the hub, you would verify the user's token.</span></span>

<a id="certificate"></a>

### <a name="certificate"></a><span data-ttu-id="63f49-174">Certificate</span><span class="sxs-lookup"><span data-stu-id="63f49-174">Certificate</span></span>

<span data-ttu-id="63f49-175">ユーザーを確認するために、クライアント証明書を渡すことができます。</span><span class="sxs-lookup"><span data-stu-id="63f49-175">You can pass a client certificate to verify the user.</span></span> <span data-ttu-id="63f49-176">接続の作成時に証明書を追加します。</span><span class="sxs-lookup"><span data-stu-id="63f49-176">You add the certificate when creating the connection.</span></span> <span data-ttu-id="63f49-177">次の例では、クライアント証明書を接続に追加する方法のみを示します。完全なコンソールアプリは表示されません。</span><span class="sxs-lookup"><span data-stu-id="63f49-177">The following example shows only how to add a client certificate to the connection; it does not show the full console app.</span></span> <span data-ttu-id="63f49-178">[X509Certificate](https://msdn.microsoft.com/library/system.security.cryptography.x509certificates.x509certificate.aspx)クラスを使用して、証明書を作成するいくつかの異なる方法を提供します。</span><span class="sxs-lookup"><span data-stu-id="63f49-178">It uses the [X509Certificate](https://msdn.microsoft.com/library/system.security.cryptography.x509certificates.x509certificate.aspx) class which provides several different ways to create the certificate.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample11.cs?highlight=6)]
