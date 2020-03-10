---
uid: signalr/overview/security/hub-authorization
title: SignalR Hub の認証と承認 |Microsoft Docs
author: bradygaster
description: このトピックでは、ハブメソッドにアクセスできるユーザーまたはロールを制限する方法について説明します。 このトピックで使用されているソフトウェアのバージョン Visual Studio 2013 .NET 4.5 SignalR ve...
ms.author: bradyg
ms.date: 01/05/2015
ms.assetid: a610c796-c131-473c-baef-2e6c568cb2a2
msc.legacyurl: /signalr/overview/security/hub-authorization
msc.type: authoredcontent
ms.openlocfilehash: 5006af5e623da6958a6d59949c6f2cf776c77fc3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467512"
---
# <a name="authentication-and-authorization-for-signalr-hubs"></a><span data-ttu-id="b9985-104">SignalR ハブの認証と承認</span><span class="sxs-lookup"><span data-stu-id="b9985-104">Authentication and Authorization for SignalR Hubs</span></span>

<span data-ttu-id="b9985-105">[Fletcher (パトリック](https://github.com/pfletcher))、 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="b9985-105">by [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="b9985-106">このトピックでは、ハブメソッドにアクセスできるユーザーまたはロールを制限する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="b9985-106">This topic describes how to restrict which users or roles can access hub methods.</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="b9985-107">このトピックで使用されているソフトウェアのバージョン</span><span class="sxs-lookup"><span data-stu-id="b9985-107">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="b9985-108">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="b9985-108">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="b9985-109">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="b9985-109">.NET 4.5</span></span>
> - <span data-ttu-id="b9985-110">SignalR バージョン2</span><span class="sxs-lookup"><span data-stu-id="b9985-110">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="b9985-111">このトピックの前のバージョン</span><span class="sxs-lookup"><span data-stu-id="b9985-111">Previous versions of this topic</span></span>
>
> <span data-ttu-id="b9985-112">以前のバージョンの SignalR の詳細については、「[古いバージョンの SignalR](../older-versions/index.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="b9985-112">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="b9985-113">質問とコメント</span><span class="sxs-lookup"><span data-stu-id="b9985-113">Questions and comments</span></span>
>
> <span data-ttu-id="b9985-114">このチュートリアルの良い点に関するフィードバックや、ページ下部にあるコメントで改善できる点をお知らせください。</span><span class="sxs-lookup"><span data-stu-id="b9985-114">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="b9985-115">チュートリアルに直接関係のない質問がある場合は、 [ASP.NET SignalR フォーラム](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)または[StackOverflow.com](http://stackoverflow.com/)に投稿できます。</span><span class="sxs-lookup"><span data-stu-id="b9985-115">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="overview"></a><span data-ttu-id="b9985-116">概要</span><span class="sxs-lookup"><span data-stu-id="b9985-116">Overview</span></span>

<span data-ttu-id="b9985-117">このトピックには、次のセクションが含まれます。</span><span class="sxs-lookup"><span data-stu-id="b9985-117">This topic contains the following sections:</span></span>

- [<span data-ttu-id="b9985-118">属性の承認</span><span class="sxs-lookup"><span data-stu-id="b9985-118">Authorize attribute</span></span>](#authorizeattribute)
- [<span data-ttu-id="b9985-119">すべてのハブに認証を要求する</span><span class="sxs-lookup"><span data-stu-id="b9985-119">Require authentication for all hubs</span></span>](#requireauth)
- [<span data-ttu-id="b9985-120">カスタマイズされた承認</span><span class="sxs-lookup"><span data-stu-id="b9985-120">Customized authorization</span></span>](#custom)
- [<span data-ttu-id="b9985-121">クライアントに認証情報を渡す</span><span class="sxs-lookup"><span data-stu-id="b9985-121">Pass authentication information to clients</span></span>](#passauth)
- [<span data-ttu-id="b9985-122">.NET クライアントの認証オプション</span><span class="sxs-lookup"><span data-stu-id="b9985-122">Authentication options for .NET clients</span></span>](#authoptions)

    - [<span data-ttu-id="b9985-123">フォーム認証を使用した Cookie</span><span class="sxs-lookup"><span data-stu-id="b9985-123">Cookie with Forms Authentication</span></span>](#cookie)
    - <span data-ttu-id="b9985-124">[[Windows 認証]](#windows)</span><span class="sxs-lookup"><span data-stu-id="b9985-124">[Windows Authentication](#windows)</span></span>
    - [<span data-ttu-id="b9985-125">接続ヘッダー</span><span class="sxs-lookup"><span data-stu-id="b9985-125">Connection header</span></span>](#header)
    - <span data-ttu-id="b9985-126">[[MSSQLSERVER のプロトコルのプロパティ]](#certificate)</span><span class="sxs-lookup"><span data-stu-id="b9985-126">[Certificate](#certificate)</span></span>

<a id="authorizeattribute"></a>

## <a name="authorize-attribute"></a><span data-ttu-id="b9985-127">属性の承認</span><span class="sxs-lookup"><span data-stu-id="b9985-127">Authorize attribute</span></span>

<span data-ttu-id="b9985-128">SignalR は、hub またはメソッドへのアクセス権を持つユーザーまたはロールを指定するための[承認](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx)属性を提供します。</span><span class="sxs-lookup"><span data-stu-id="b9985-128">SignalR provides the [Authorize](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx) attribute to specify which users or roles have access to a hub or method.</span></span> <span data-ttu-id="b9985-129">この属性は `Microsoft.AspNet.SignalR` 名前空間にあります。</span><span class="sxs-lookup"><span data-stu-id="b9985-129">This attribute is located in the `Microsoft.AspNet.SignalR` namespace.</span></span> <span data-ttu-id="b9985-130">`Authorize` 属性はハブのハブまたは特定のメソッドのいずれかに適用します。</span><span class="sxs-lookup"><span data-stu-id="b9985-130">You apply the `Authorize` attribute to either a hub or particular methods in a hub.</span></span> <span data-ttu-id="b9985-131">`Authorize` 属性をハブクラスに適用すると、指定された承認要件がハブのすべてのメソッドに適用されます。</span><span class="sxs-lookup"><span data-stu-id="b9985-131">When you apply the `Authorize` attribute to a hub class, the specified authorization requirement is applied to all of the methods in the hub.</span></span> <span data-ttu-id="b9985-132">このトピックでは、適用できるさまざまな種類の承認要件の例を示します。</span><span class="sxs-lookup"><span data-stu-id="b9985-132">This topic provides examples of the different types of authorization requirements that you can apply.</span></span> <span data-ttu-id="b9985-133">`Authorize` 属性を指定しない場合、接続されたクライアントはハブ上の任意のパブリックメソッドにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="b9985-133">Without the `Authorize` attribute, a connected client can access any public method on the hub.</span></span>

<span data-ttu-id="b9985-134">Web アプリケーションで "Admin" という名前のロールを定義している場合は、次のコードを使用して、そのロールのユーザーのみがハブにアクセスできるように指定できます。</span><span class="sxs-lookup"><span data-stu-id="b9985-134">If you have defined a role named "Admin" in your web application, you could specify that only users in that role can access a hub with the following code.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample1.cs)]

<span data-ttu-id="b9985-135">または、次に示すように、すべてのユーザーが使用できる1つのメソッドと、認証されたユーザーのみが使用できる2番目のメソッドをハブに含めるように指定できます。</span><span class="sxs-lookup"><span data-stu-id="b9985-135">Or, you can specify that a hub contains one method that is available to all users, and a second method that is only available to authenticated users, as shown below.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample2.cs)]

<span data-ttu-id="b9985-136">次の例では、さまざまな承認シナリオに対処します。</span><span class="sxs-lookup"><span data-stu-id="b9985-136">The following examples address different authorization scenarios:</span></span>

- <span data-ttu-id="b9985-137">`[Authorize]`-認証されたユーザーのみ</span><span class="sxs-lookup"><span data-stu-id="b9985-137">`[Authorize]` – only authenticated users</span></span>
- <span data-ttu-id="b9985-138">`[Authorize(Roles = "Admin,Manager")]`-指定したロール内の認証されたユーザーのみ</span><span class="sxs-lookup"><span data-stu-id="b9985-138">`[Authorize(Roles = "Admin,Manager")]` – only authenticated users in the specified roles</span></span>
- <span data-ttu-id="b9985-139">`[Authorize(Users = "user1,user2")]` –指定されたユーザー名を持つ認証済みユーザーのみ</span><span class="sxs-lookup"><span data-stu-id="b9985-139">`[Authorize(Users = "user1,user2")]` – only authenticated users with the specified user names</span></span>
- <span data-ttu-id="b9985-140">`[Authorize(RequireOutgoing=false)]`: 認証されたユーザーのみがハブを呼び出すことができますが、サーバーからクライアントへの呼び出しは、特定のユーザーのみがメッセージを送信できるが、他のユーザーがメッセージを受信できる場合など、承認によって制限されません。</span><span class="sxs-lookup"><span data-stu-id="b9985-140">`[Authorize(RequireOutgoing=false)]` – only authenticated users can invoke the hub, but calls from the server back to clients are not limited by authorization, such as, when only certain users can send a message but all others can receive the message.</span></span> <span data-ttu-id="b9985-141">RequireOutgoing プロパティは、ハブ内の個々のメソッドではなく、ハブ全体にのみ適用できます。</span><span class="sxs-lookup"><span data-stu-id="b9985-141">The RequireOutgoing property can only be applied to the entire hub, not on individuals methods within the hub.</span></span> <span data-ttu-id="b9985-142">RequireOutgoing が false に設定されていない場合、承認要件を満たすユーザーのみがサーバーから呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="b9985-142">When RequireOutgoing is not set to false, only users that meet the authorization requirement are called from the server.</span></span>

<a id="requireauth"></a>

## <a name="require-authentication-for-all-hubs"></a><span data-ttu-id="b9985-143">すべてのハブに認証を要求する</span><span class="sxs-lookup"><span data-stu-id="b9985-143">Require authentication for all hubs</span></span>

<span data-ttu-id="b9985-144">アプリケーションの起動時に[requireauthentication](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubpipelineextensions.requireauthentication(v=vs.111).aspx)メソッドを呼び出すことにより、アプリケーション内のすべてのハブおよびハブメソッドに対して認証を要求できます。</span><span class="sxs-lookup"><span data-stu-id="b9985-144">You can require authentication for all hubs and hub methods in your application by calling the [RequireAuthentication](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubpipelineextensions.requireauthentication(v=vs.111).aspx) method when the application starts.</span></span> <span data-ttu-id="b9985-145">複数のハブがあり、そのすべてに対して認証要件を強制する場合は、この方法を使用できます。</span><span class="sxs-lookup"><span data-stu-id="b9985-145">You might use this method when you have multiple hubs and want to enforce an authentication requirement for all of them.</span></span> <span data-ttu-id="b9985-146">この方法では、ロール、ユーザー、または送信の承認に関する要件を指定することはできません。</span><span class="sxs-lookup"><span data-stu-id="b9985-146">With this method, you cannot specify requirements for role, user, or outgoing authorization.</span></span> <span data-ttu-id="b9985-147">ハブメソッドへのアクセスが認証されたユーザーに制限されることのみを指定できます。</span><span class="sxs-lookup"><span data-stu-id="b9985-147">You can only specify that access to the hub methods is restricted to authenticated users.</span></span> <span data-ttu-id="b9985-148">ただし、承認属性をハブまたはメソッドに適用して、追加の要件を指定することもできます。</span><span class="sxs-lookup"><span data-stu-id="b9985-148">However, you can still apply the Authorize attribute to hubs or methods to specify additional requirements.</span></span> <span data-ttu-id="b9985-149">属性で指定する要件は、認証の基本要件に追加されます。</span><span class="sxs-lookup"><span data-stu-id="b9985-149">Any requirement you specify in an attribute is added to the basic requirement of authentication.</span></span>

<span data-ttu-id="b9985-150">次の例は、すべてのハブメソッドを認証されたユーザーに制限するスタートアップファイルを示しています。</span><span class="sxs-lookup"><span data-stu-id="b9985-150">The following example shows a Startup file which restricts all hub methods to authenticated users.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample3.cs)]

<span data-ttu-id="b9985-151">SignalR 要求が処理された後に `RequireAuthentication()` メソッドを呼び出すと、SignalR は例外 `InvalidOperationException` をスローします。</span><span class="sxs-lookup"><span data-stu-id="b9985-151">If you call the `RequireAuthentication()` method after a SignalR request has been processed, SignalR will throw a `InvalidOperationException` exception.</span></span> <span data-ttu-id="b9985-152">SignalR は、パイプラインが呼び出された後にモジュールを HubPipeline に追加することはできないため、この例外をスローします。</span><span class="sxs-lookup"><span data-stu-id="b9985-152">SignalR throws this exception because you cannot add a module to the HubPipeline after the pipeline has been invoked.</span></span> <span data-ttu-id="b9985-153">前の例では、最初の要求を処理する前に1回実行される `Configuration` メソッドで `RequireAuthentication` メソッドを呼び出しています。</span><span class="sxs-lookup"><span data-stu-id="b9985-153">The previous example shows calling the `RequireAuthentication` method in the `Configuration` method which is executed one time prior to handling the first request.</span></span>

<a id="custom"></a>

## <a name="customized-authorization"></a><span data-ttu-id="b9985-154">カスタマイズされた承認</span><span class="sxs-lookup"><span data-stu-id="b9985-154">Customized authorization</span></span>

<span data-ttu-id="b9985-155">承認を決定する方法をカスタマイズする必要がある場合は、`AuthorizeAttribute` から派生したクラスを作成し、 [userauthorized](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute.userauthorized(v=vs.111).aspx)メソッドをオーバーライドできます。</span><span class="sxs-lookup"><span data-stu-id="b9985-155">If you need to customize how authorization is determined, you can create a class that derives from `AuthorizeAttribute` and override the [UserAuthorized](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute.userauthorized(v=vs.111).aspx) method.</span></span> <span data-ttu-id="b9985-156">SignalR は、要求ごとにこのメソッドを呼び出して、要求を完了する権限がユーザーに与えられているかどうかを確認します。</span><span class="sxs-lookup"><span data-stu-id="b9985-156">For each request, SignalR invokes this method to determine whether the user is authorized to complete the request.</span></span> <span data-ttu-id="b9985-157">オーバーライドされたメソッドには、承認シナリオに必要なロジックを指定します。</span><span class="sxs-lookup"><span data-stu-id="b9985-157">In the overridden method, you provide the necessary logic for your authorization scenario.</span></span> <span data-ttu-id="b9985-158">次の例は、クレームベースの id を通じて承認を強制する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="b9985-158">The following example shows how to enforce authorization through claims-based identity.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample4.cs)]

<a id="passauth"></a>

## <a name="pass-authentication-information-to-clients"></a><span data-ttu-id="b9985-159">クライアントに認証情報を渡す</span><span class="sxs-lookup"><span data-stu-id="b9985-159">Pass authentication information to clients</span></span>

<span data-ttu-id="b9985-160">場合によっては、クライアントで実行されるコードで認証情報を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b9985-160">You may need to use authentication information in the code that runs on the client.</span></span> <span data-ttu-id="b9985-161">クライアントでメソッドを呼び出すときに、必要な情報を渡します。</span><span class="sxs-lookup"><span data-stu-id="b9985-161">You pass the required information when calling the methods on the client.</span></span> <span data-ttu-id="b9985-162">たとえば、次に示すように、チャットアプリケーションのメソッドは、メッセージを投稿する人のユーザー名をパラメーターとして渡すことができます。</span><span class="sxs-lookup"><span data-stu-id="b9985-162">For example, a chat application method could pass as a parameter the user name of the person posting a message, as shown below.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample5.cs)]

<span data-ttu-id="b9985-163">または、次に示すように、認証情報を表すオブジェクトを作成し、そのオブジェクトをパラメーターとして渡すことができます。</span><span class="sxs-lookup"><span data-stu-id="b9985-163">Or, you can create an object to represent the authentication information and pass that object as a parameter, as shown below.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample6.cs)]

<span data-ttu-id="b9985-164">悪意のあるユーザーがそのクライアントからの要求を模倣するために使用する可能性があるため、1つのクライアントの接続 id を他のクライアントに渡すことはできません。</span><span class="sxs-lookup"><span data-stu-id="b9985-164">You should never pass one client's connection id to other clients, as a malicious user could use it to mimic a request from that client.</span></span>

<a id="authoptions"></a>

## <a name="authentication-options-for-net-clients"></a><span data-ttu-id="b9985-165">.NET クライアントの認証オプション</span><span class="sxs-lookup"><span data-stu-id="b9985-165">Authentication options for .NET clients</span></span>

<span data-ttu-id="b9985-166">認証されたユーザーに限定されたハブと対話するコンソールアプリなどの .NET クライアントがある場合は、認証資格情報をクッキー、接続ヘッダー、または証明書に渡すことができます。</span><span class="sxs-lookup"><span data-stu-id="b9985-166">When you have a .NET client, such as a console app, which interacts with a hub that is limited to authenticated users, you can pass the authentication credentials in a cookie, the connection header, or a certificate.</span></span> <span data-ttu-id="b9985-167">このセクションの例では、これらの異なる方法を使用してユーザーを認証する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="b9985-167">The examples in this section show how to use those different methods for authenticating a user.</span></span> <span data-ttu-id="b9985-168">これらは、完全に機能している SignalR アプリではありません。</span><span class="sxs-lookup"><span data-stu-id="b9985-168">They are not fully-functional SignalR apps.</span></span> <span data-ttu-id="b9985-169">SignalR を使用した .NET クライアントの詳細については、「 [HUB API Guide-.Net Client](../guide-to-the-api/hubs-api-guide-net-client.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="b9985-169">For more information about .NET clients with SignalR, see [Hubs API Guide - .NET Client](../guide-to-the-api/hubs-api-guide-net-client.md).</span></span>

<a id="cookie"></a>

### <a name="cookie"></a><span data-ttu-id="b9985-170">Cookie</span><span class="sxs-lookup"><span data-stu-id="b9985-170">Cookie</span></span>

<span data-ttu-id="b9985-171">ASP.NET Forms 認証を使用するハブと .NET クライアントが通信する場合、接続で認証 cookie を手動で設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b9985-171">When your .NET client interacts with a hub that uses ASP.NET Forms Authentication, you will need to manually set the authentication cookie on the connection.</span></span> <span data-ttu-id="b9985-172">[HubConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.hubs.hubconnection(v=vs.111).aspx)オブジェクトの `CookieContainer` プロパティに cookie を追加します。</span><span class="sxs-lookup"><span data-stu-id="b9985-172">You add the cookie to the `CookieContainer` property on the [HubConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.hubs.hubconnection(v=vs.111).aspx) object.</span></span> <span data-ttu-id="b9985-173">次の例は、web ページから認証クッキーを取得し、その cookie を接続に追加するコンソールアプリを示しています。</span><span class="sxs-lookup"><span data-stu-id="b9985-173">The following example shows a console app that retrieves an authentication cookie from a web page and adds that cookie to the connection.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample7.cs)]

<span data-ttu-id="b9985-174">コンソールアプリによって資格情報が<strong>www.contoso.com/RemoteLogin</strong>にポストされ、次の分離コードファイルを含む空のページを参照できます。</span><span class="sxs-lookup"><span data-stu-id="b9985-174">The console app posts the credentials to <strong>www.contoso.com/RemoteLogin</strong> which could refer to an empty page that contains the following code-behind file.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample8.cs)]

<a id="windows"></a>

### <a name="windows-authentication"></a><span data-ttu-id="b9985-175">Windows 認証</span><span class="sxs-lookup"><span data-stu-id="b9985-175">Windows authentication</span></span>

<span data-ttu-id="b9985-176">Windows 認証を使用する場合は、 [DefaultCredentials](https://msdn.microsoft.com/library/system.net.credentialcache.defaultcredentials.aspx)プロパティを使用して、現在のユーザーの資格情報を渡すことができます。</span><span class="sxs-lookup"><span data-stu-id="b9985-176">When using Windows authentication, you can pass the current user's credentials by using the [DefaultCredentials](https://msdn.microsoft.com/library/system.net.credentialcache.defaultcredentials.aspx) property.</span></span> <span data-ttu-id="b9985-177">接続の資格情報を DefaultCredentials の値に設定します。</span><span class="sxs-lookup"><span data-stu-id="b9985-177">You set the credentials for the connection to the value of the DefaultCredentials.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample9.cs?highlight=6)]

<a id="header"></a>

### <a name="connection-header"></a><span data-ttu-id="b9985-178">接続ヘッダー</span><span class="sxs-lookup"><span data-stu-id="b9985-178">Connection header</span></span>

<span data-ttu-id="b9985-179">アプリケーションが cookie を使用していない場合は、接続ヘッダーにユーザー情報を渡すことができます。</span><span class="sxs-lookup"><span data-stu-id="b9985-179">If your application is not using cookies, you can pass user information in the connection header.</span></span> <span data-ttu-id="b9985-180">たとえば、接続ヘッダーにトークンを渡すことができます。</span><span class="sxs-lookup"><span data-stu-id="b9985-180">For example, you can pass a token in the connection header.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample10.cs?highlight=6)]

<span data-ttu-id="b9985-181">次に、ハブでユーザーのトークンを確認します。</span><span class="sxs-lookup"><span data-stu-id="b9985-181">Then, in the hub, you would verify the user's token.</span></span>

<a id="certificate"></a>

### <a name="certificate"></a><span data-ttu-id="b9985-182">Certificate</span><span class="sxs-lookup"><span data-stu-id="b9985-182">Certificate</span></span>

<span data-ttu-id="b9985-183">ユーザーを確認するために、クライアント証明書を渡すことができます。</span><span class="sxs-lookup"><span data-stu-id="b9985-183">You can pass a client certificate to verify the user.</span></span> <span data-ttu-id="b9985-184">接続の作成時に証明書を追加します。</span><span class="sxs-lookup"><span data-stu-id="b9985-184">You add the certificate when creating the connection.</span></span> <span data-ttu-id="b9985-185">次の例では、クライアント証明書を接続に追加する方法のみを示します。完全なコンソールアプリは表示されません。</span><span class="sxs-lookup"><span data-stu-id="b9985-185">The following example shows only how to add a client certificate to the connection; it does not show the full console app.</span></span> <span data-ttu-id="b9985-186">[X509Certificate](https://msdn.microsoft.com/library/system.security.cryptography.x509certificates.x509certificate.aspx)クラスを使用して、証明書を作成するいくつかの異なる方法を提供します。</span><span class="sxs-lookup"><span data-stu-id="b9985-186">It uses the [X509Certificate](https://msdn.microsoft.com/library/system.security.cryptography.x509certificates.x509certificate.aspx) class which provides several different ways to create the certificate.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample11.cs?highlight=6)]
