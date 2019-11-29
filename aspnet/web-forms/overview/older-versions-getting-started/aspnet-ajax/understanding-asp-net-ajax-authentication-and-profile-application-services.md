---
uid: web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-authentication-and-profile-application-services
title: ASP.NET AJAX 認証とプロファイルアプリケーションサービスについて |Microsoft Docs
author: scottcate
description: 認証サービスを使用すると、ユーザーは認証 cookie を受信するための資格情報を入力できます。また、カスタムユーザーを許可するゲートウェイサービスです...
ms.author: riande
ms.date: 03/14/2008
ms.assetid: 6ab4efb6-aab6-45ac-ad2c-bdec5848ef9e
msc.legacyurl: /web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-authentication-and-profile-application-services
msc.type: authoredcontent
ms.openlocfilehash: cab9acb1ffd75cca87f6c575a6abdd000235828e
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74635690"
---
# <a name="understanding-aspnet-ajax-authentication-and-profile-application-services"></a><span data-ttu-id="9c9dd-103">ASP.NET AJAX 認証とプロファイル アプリケーション サービスについて理解する</span><span class="sxs-lookup"><span data-stu-id="9c9dd-103">Understanding ASP.NET AJAX Authentication and Profile Application Services</span></span>

<span data-ttu-id="9c9dd-104">[Scott Cate](https://github.com/scottcate)</span><span class="sxs-lookup"><span data-stu-id="9c9dd-104">by [Scott Cate](https://github.com/scottcate)</span></span>

[<span data-ttu-id="9c9dd-105">PDF のダウンロード</span><span class="sxs-lookup"><span data-stu-id="9c9dd-105">Download PDF</span></span>](https://download.microsoft.com/download/C/1/9/C19A3451-1D14-477C-B703-54EF22E197EE/AJAX_tutorial03_MSAjax_ASP.NET_Services_cs.pdf)

> <span data-ttu-id="9c9dd-106">認証サービスを使用すると、ユーザーは認証 cookie を受信するために資格情報を提供できます。また、ASP.NET によって提供されるカスタムユーザープロファイルを許可するゲートウェイサービスです。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-106">The Authentication service allows users to provide credentials in order to receive an authentication cookie, and is the gateway service to allow custom user profiles provided by ASP.NET.</span></span> <span data-ttu-id="9c9dd-107">ASP.NET AJAX 認証サービスの使用は標準の ASP.NET フォーム認証と互換性があるため、現在フォーム認証を使用しているアプリケーション (ログインコントロールなど) は AJAX 認証サービスにアップグレードしても破損しません。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-107">Use of the ASP.NET AJAX authentication service is compatible with standard ASP.NET Forms authentication, so applications currently using Forms authentication (such as with the Login control) will not be broken by upgrading to the AJAX authentication service.</span></span>

## <a name="introduction"></a><span data-ttu-id="9c9dd-108">はじめに</span><span class="sxs-lookup"><span data-stu-id="9c9dd-108">Introduction</span></span>

<span data-ttu-id="9c9dd-109">.NET Framework 3.5 の一部として、Microsoft は、さまざまな環境のアップグレードを提供しています。新しい開発環境が利用可能になるだけでなく、新しい統合言語クエリ (LINQ) 機能やその他の言語の機能強化が予定されています。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-109">As part of the .NET Framework 3.5, Microsoft is delivering a sizable environment upgrade; not only is a new development environment available, but the new Language-Integrated Query (LINQ) features and other language enhancements are forthcoming.</span></span> <span data-ttu-id="9c9dd-110">さらに、他のツールセットのいくつかの使い慣れた機能 (特に ASP.NET AJAX 拡張機能) は、基本クラスライブラリ .NET Framework のファーストクラスメンバーとして含まれています。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-110">In addition, some familiar features of other toolsets, notably the ASP.NET AJAX Extensions, are being included as first-class members of the .NET Framework Base Class Library.</span></span> <span data-ttu-id="9c9dd-111">これらの拡張機能により、ページの完全な更新を必要としないページの部分的なレンダリング、クライアントスクリプト (ASP.NET プロファイリング API を含む) を使用した Web サービスへのアクセス機能、広範なクライアント側 API など、多くの豊富なクライアント機能が有効になります。ASP.NET のサーバー側コントロールセットで見られる多くのコントロールスキームをミラー化するように設計されています。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-111">These extensions enable many new rich client features, including partial rendering of pages without requiring a full page refresh, the ability to access Web Services via client script (including the ASP.NET profiling API), and an extensive client-side API designed to mirror many of the control schemes seen in the ASP.NET server-side control set.</span></span>

<span data-ttu-id="9c9dd-112">このホワイトペーパーでは、ASP.NET プロファイリングとフォーム認証サービスの実装と使用方法について考察しています。これらは Microsoft ASP.NET AJAX ExtensionsThe よって公開されており、AJAX 拡張機能によってフォーム認証が非常に簡単にサポートされるようになります (また、プロファイルサービス) は、Web サービスプロキシスクリプトを通じて公開されます。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-112">This whitepaper looks at the implementation and use of the ASP.NET Profiling and Forms Authentication services as they are exposed by the Microsoft ASP.NET AJAX ExtensionsThe AJAX Extensions make Forms authentication incredibly easy to support, as it (as well as the Profiling Service) is exposed through a Web Service proxy script.</span></span> <span data-ttu-id="9c9dd-113">AJAX 拡張は、AuthenticationServiceManager クラスを使用したカスタム認証もサポートしています。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-113">The AJAX Extensions also support custom authentication through the AuthenticationServiceManager class.</span></span>

<span data-ttu-id="9c9dd-114">このホワイトペーパーは、Visual Studio 2008 のベータ2リリースと .NET Framework 3.5 に基づいています。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-114">This whitepaper is based on the Beta 2 release of the Visual Studio 2008 and the .NET Framework 3.5.</span></span> <span data-ttu-id="9c9dd-115">また、このホワイトペーパーでは、visual Web Developer Express ではなく Visual Studio 2008 Beta 2 を使用することを前提としています。また、Visual Studio のユーザーインターフェイスに従ってチュートリアルを提供します。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-115">This whitepaper also assumes that you will be working with Visual Studio 2008 Beta 2, not Visual Web Developer Express, and will provide walkthroughs according to the user interface of Visual Studio.</span></span> <span data-ttu-id="9c9dd-116">一部のコードサンプルでは、Visual Web Developer Express で使用できないプロジェクトテンプレートを使用する場合があります。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-116">Some code samples may utilize project templates unavailable in Visual Web Developer Express.</span></span>

## <a name="profiles-and-authentication"></a><span data-ttu-id="9c9dd-117">*プロファイルと認証*</span><span class="sxs-lookup"><span data-stu-id="9c9dd-117">*Profiles and Authentication*</span></span>

<span data-ttu-id="9c9dd-118">Microsoft ASP.NET のプロファイルと認証サービスは ASP.NET Forms 認証システムによって提供され、ASP.NET の標準コンポーネントです。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-118">The Microsoft ASP.NET Profiles and Authentication services are provided by the ASP.NET Forms Authentication system, and are standard components of ASP.NET.</span></span> <span data-ttu-id="9c9dd-119">ASP.NET AJAX 拡張機能は、クライアント AJAX ライブラリの Sys. Services 名前空間の下にある非常に単純なモデルを使用して、これらのサービスへのスクリプトアクセスをスクリプトプロキシを介して提供します。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-119">The ASP.NET AJAX Extensions provide script access to these services via script proxies, through a fairly straightforward model under the Sys.Services namespace of the client AJAX library.</span></span>

<span data-ttu-id="9c9dd-120">認証サービスを使用すると、ユーザーは認証 cookie を受信するために資格情報を提供できます。また、ASP.NET によって提供されるカスタムユーザープロファイルを許可するゲートウェイサービスです。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-120">The Authentication service allows users to provide credentials in order to receive an authentication cookie, and is the gateway service to allow custom user profiles provided by ASP.NET.</span></span> <span data-ttu-id="9c9dd-121">ASP.NET AJAX 認証サービスの使用は標準の ASP.NET フォーム認証と互換性があるため、現在フォーム認証を使用しているアプリケーション (ログインコントロールなど) は AJAX 認証サービスにアップグレードしても破損しません。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-121">Use of the ASP.NET AJAX authentication service is compatible with standard ASP.NET Forms authentication, so applications currently using Forms authentication (such as with the Login control) will not be broken by upgrading to the AJAX authentication service.</span></span>

<span data-ttu-id="9c9dd-122">プロファイルサービスを使用すると、認証サービスによって提供されるメンバーシップに基づいて、ユーザーデータを自動統合および格納できます。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-122">The Profile service allows the automatic integration and storage of user data based on membership as provided by the Authentication service.</span></span> <span data-ttu-id="9c9dd-123">格納されているデータは web.config ファイルによって指定され、さまざまなプロファイリングサービスプロバイダーがデータ管理を処理します。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-123">The stored data is specified by the web.config file, and the various profiling service providers handle the data management.</span></span> <span data-ttu-id="9c9dd-124">認証サービスと同様に、AJAX プロファイルサービスは標準の ASP.NET profile service と互換性があるため、ASP.NET Profile service の機能が現在組み込まれているページは、AJAX サポートを含むことによって破損しないようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-124">As with the Authentication service, the AJAX Profile service is compatible with the standard ASP.NET profile service, so that pages currently incorporating features of the ASP.NET Profile service should not be broken by including AJAX support.</span></span>

<span data-ttu-id="9c9dd-125">ASP.NET 認証とプロファイルサービスをアプリケーションに組み込むことは、このホワイトペーパーの範囲外です。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-125">Incorporating the ASP.NET Authentication and Profiling services themselves into an application is outside of the scope of this whitepaper.</span></span> <span data-ttu-id="9c9dd-126">トピックの詳細については、MSDN ライブラリリファレンス記事「 [https://msdn.microsoft.com/library/tw292whz.aspx](https://msdn.microsoft.com/library/tw292whz.aspx)でメンバーシップを使用してユーザーを管理する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-126">For more information on the topic, see the MSDN Library reference article Managing Users by Using Membership at [https://msdn.microsoft.com/library/tw292whz.aspx](https://msdn.microsoft.com/library/tw292whz.aspx).</span></span> <span data-ttu-id="9c9dd-127">また、ASP.NET には、ASP.NET メンバーシップの既定の認証サービスプロバイダーである SQL Server のメンバーシップを自動的に設定するユーティリティも含まれています。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-127">ASP.NET also includes a utility to automatically set up Membership with a SQL Server, which is the default authentication service provider for ASP.NET Membership.</span></span> <span data-ttu-id="9c9dd-128">詳細については、 [https://msdn.microsoft.com/library/ms229862(vs.80).aspx](https://msdn.microsoft.com/library/ms229862(vs.80).aspx)の「ASP.NET SQL Server Registration Tool (Aspnet\_ regsql)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-128">For more information, see the article ASP.NET SQL Server Registration Tool (Aspnet\_regsql.exe) at [https://msdn.microsoft.com/library/ms229862(vs.80).aspx](https://msdn.microsoft.com/library/ms229862(vs.80).aspx).</span></span>

## <a name="using-the-aspnet-ajax-authentication-service"></a><span data-ttu-id="9c9dd-129">*ASP.NET AJAX 認証サービスの使用*</span><span class="sxs-lookup"><span data-stu-id="9c9dd-129">*Using the ASP.NET AJAX Authentication Service*</span></span>

<span data-ttu-id="9c9dd-130">Web.config ファイルで ASP.NET AJAX Authentication service が有効になっている必要があります。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-130">The ASP.NET AJAX Authentication service must be enabled in the web.config file:</span></span>

[!code-xml[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample1.xml)]

<span data-ttu-id="9c9dd-131">認証サービスでは、ASP.NET フォーム認証を有効にし、クライアントブラウザーでクッキーを有効にする必要があります (クッキーレスセッションでは URL パラメーターが必要であるため、スクリプトでクッキーレスセッションを有効にすることはできません)。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-131">The Authentication service requires ASP.NET Forms authentication to be enabled and requires cookies to be enabled on the client browser (a script cannot enable a cookieless session since cookieless sessions require URL parameters).</span></span>

<span data-ttu-id="9c9dd-132">AJAX 認証サービスが有効化され、構成されると、クライアントスクリプトはすぐに AuthenticationService オブジェクトを利用できます。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-132">Once the AJAX authentication service is enabled and configured, client script can immediately take advantage of the Sys.Services.AuthenticationService object.</span></span> <span data-ttu-id="9c9dd-133">主に、クライアントスクリプトは、`login` メソッドと `isLoggedIn` プロパティを利用します。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-133">Primarily, client script will want to take advantage of the `login` method and `isLoggedIn` property.</span></span> <span data-ttu-id="9c9dd-134">Login メソッドの既定値を提供するいくつかのプロパティが用意されています。これは、多数のパラメーターを受け取ることができます。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-134">Several properties exist to provide defaults for the login method, which can accept a large number of parameters.</span></span>

<span data-ttu-id="9c9dd-135">*AuthenticationService のメンバー*</span><span class="sxs-lookup"><span data-stu-id="9c9dd-135">*Sys.Services.AuthenticationService members*</span></span>

<span data-ttu-id="9c9dd-136">*ログイン方法:*</span><span class="sxs-lookup"><span data-stu-id="9c9dd-136">*login method:*</span></span>

<span data-ttu-id="9c9dd-137">Login () メソッドは、ユーザーの資格情報の認証要求を開始します。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-137">The login() method begins a request to authenticate the user's credentials.</span></span> <span data-ttu-id="9c9dd-138">このメソッドは非同期であり、実行をブロックしません。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-138">This method is asynchronous and does not block execution.</span></span>

<span data-ttu-id="9c9dd-139">*パラメータ*</span><span class="sxs-lookup"><span data-stu-id="9c9dd-139">*Parameters:*</span></span>

| <span data-ttu-id="9c9dd-140">**パラメーター名**</span><span class="sxs-lookup"><span data-stu-id="9c9dd-140">**Parameter Name**</span></span> | <span data-ttu-id="9c9dd-141">**通用**</span><span class="sxs-lookup"><span data-stu-id="9c9dd-141">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="9c9dd-142">userName</span><span class="sxs-lookup"><span data-stu-id="9c9dd-142">userName</span></span> | <span data-ttu-id="9c9dd-143">必須です。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-143">Required.</span></span> <span data-ttu-id="9c9dd-144">認証するユーザー名。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-144">The username to authenticate.</span></span> |
| <span data-ttu-id="9c9dd-145">のパスワード</span><span class="sxs-lookup"><span data-stu-id="9c9dd-145">password</span></span> | <span data-ttu-id="9c9dd-146">省略可能 (既定値は null)。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-146">Optional (defaults to null).</span></span> <span data-ttu-id="9c9dd-147">ユーザーのパスワード。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-147">The user's password.</span></span> |
| <span data-ttu-id="9c9dd-148">isPersistent</span><span class="sxs-lookup"><span data-stu-id="9c9dd-148">isPersistent</span></span> | <span data-ttu-id="9c9dd-149">省略可能 (既定値は false)。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-149">Optional (defaults to false).</span></span> <span data-ttu-id="9c9dd-150">ユーザーの認証クッキーをセッション間で保持する必要があるかどうか。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-150">Whether the user's authentication cookie should persist across sessions.</span></span> <span data-ttu-id="9c9dd-151">False の場合、ブラウザーが終了したとき、またはセッションの有効期限が切れたときに、ユーザーがログアウトします。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-151">If false, the user will log out when the browser is closed or the session expires.</span></span> |
| <span data-ttu-id="9c9dd-152">redirectUrl</span><span class="sxs-lookup"><span data-stu-id="9c9dd-152">redirectUrl</span></span> | <span data-ttu-id="9c9dd-153">省略可能 (既定値は null)。認証が成功したときにブラウザーをリダイレクトする URL。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-153">Optional (defaults to null).The URL to redirect the browser to upon successful authentication.</span></span> <span data-ttu-id="9c9dd-154">このパラメーターが null または空の文字列の場合、リダイレクトは実行されません。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-154">If this parameter is null or an empty string, no redirection occurs.</span></span> |
| <span data-ttu-id="9c9dd-155">customInfo</span><span class="sxs-lookup"><span data-stu-id="9c9dd-155">customInfo</span></span> | <span data-ttu-id="9c9dd-156">省略可能 (既定値は null)。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-156">Optional (defaults to null).</span></span> <span data-ttu-id="9c9dd-157">このパラメーターは現在使用されていないため、将来使用するために予約されています。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-157">This parameter is currently unused and is reserved for future use.</span></span> |
| <span data-ttu-id="9c9dd-158">loginCompletedCallback</span><span class="sxs-lookup"><span data-stu-id="9c9dd-158">loginCompletedCallback</span></span> | <span data-ttu-id="9c9dd-159">省略可能 (既定値は null)。ログインが正常に完了したときに呼び出す関数。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-159">Optional (defaults to null).The function to call when the login has successfully completed.</span></span> <span data-ttu-id="9c9dd-160">指定した場合、このパラメーターは defaultLoginCompleted プロパティよりも優先されます。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-160">If specified, this parameter overrides the defaultLoginCompleted property.</span></span> |
| <span data-ttu-id="9c9dd-161">失敗したコールバック</span><span class="sxs-lookup"><span data-stu-id="9c9dd-161">failedCallback</span></span> | <span data-ttu-id="9c9dd-162">省略可能 (既定値は null)。ログインが失敗したときに呼び出す関数。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-162">Optional (defaults to null).The function to call when the login has failed.</span></span> <span data-ttu-id="9c9dd-163">指定した場合、このパラメーターは Defaultの Callback プロパティよりも優先されます。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-163">If specified, this parameter overrides the defaultFailedCallback property.</span></span> |
| <span data-ttu-id="9c9dd-164">userContext</span><span class="sxs-lookup"><span data-stu-id="9c9dd-164">userContext</span></span> | <span data-ttu-id="9c9dd-165">省略可能 (既定値は null)。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-165">Optional (defaults to null).</span></span> <span data-ttu-id="9c9dd-166">コールバック関数に渡される必要があるカスタムユーザーコンテキストデータ。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-166">Custom user context data that should be passed to the callback functions.</span></span> |

<span data-ttu-id="9c9dd-167">*戻り値:*</span><span class="sxs-lookup"><span data-stu-id="9c9dd-167">*Return Value:*</span></span>

<span data-ttu-id="9c9dd-168">この関数には、戻り値は含まれません。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-168">This function does not include a return value.</span></span> <span data-ttu-id="9c9dd-169">ただし、この関数の呼び出しの完了時には、いくつかの動作が含まれます。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-169">However, a number of behaviors are included upon completion of a call to this function:</span></span>

- <span data-ttu-id="9c9dd-170">`redirectUrl` パラメーターが null でも空の文字列でもない場合、現在のページは更新されるか、または変更されます。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-170">The current page will either be refreshed or be changed if the `redirectUrl` parameter was neither null nor an empty string.</span></span>
- <span data-ttu-id="9c9dd-171">ただし、パラメーターが null または空の文字列の場合は、`loginCompletedCallback` パラメーター、または `defaultLoginCompletedCallback` プロパティが呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-171">However, if the parameter was null or an empty string, the `loginCompletedCallback` parameter, or `defaultLoginCompletedCallback` property is called.</span></span>
- <span data-ttu-id="9c9dd-172">Web サービスへの呼び出しが失敗した場合、`defaultFailedCallback` プロパティの `failedCallback` パラメーターが呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-172">If the call to the web service fails, the `failedCallback` parameter of `defaultFailedCallback` property is called.</span></span>

<span data-ttu-id="9c9dd-173">*logout メソッド:*</span><span class="sxs-lookup"><span data-stu-id="9c9dd-173">*logout method:*</span></span>

<span data-ttu-id="9c9dd-174">Logout () メソッドは、資格情報の cookie を削除し、web アプリケーションから現在のユーザーをログアウトします。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-174">The logout() method removes the credentials cookie and logs out the current user from the web application.</span></span>

<span data-ttu-id="9c9dd-175">*パラメータ*</span><span class="sxs-lookup"><span data-stu-id="9c9dd-175">*Parameters:*</span></span>

| <span data-ttu-id="9c9dd-176">**パラメーター名**</span><span class="sxs-lookup"><span data-stu-id="9c9dd-176">**Parameter Name**</span></span> | <span data-ttu-id="9c9dd-177">**通用**</span><span class="sxs-lookup"><span data-stu-id="9c9dd-177">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="9c9dd-178">redirectUrl</span><span class="sxs-lookup"><span data-stu-id="9c9dd-178">redirectUrl</span></span> | <span data-ttu-id="9c9dd-179">省略可能 (既定値は null)。認証が成功したときにブラウザーをリダイレクトする URL。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-179">Optional (defaults to null).The URL to redirect the browser to upon successful authentication.</span></span> <span data-ttu-id="9c9dd-180">このパラメーターが null または空の文字列の場合、リダイレクトは実行されません。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-180">If this parameter is null or an empty string, no redirection occurs.</span></span> |
| <span data-ttu-id="9c9dd-181">logoutCompletedCallback</span><span class="sxs-lookup"><span data-stu-id="9c9dd-181">logoutCompletedCallback</span></span> | <span data-ttu-id="9c9dd-182">省略可能 (既定値は null)。ログアウトが正常に完了したときに呼び出す関数。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-182">Optional (defaults to null).The function to call when the logout has successfully completed.</span></span> <span data-ttu-id="9c9dd-183">指定した場合、このパラメーターは defaultLogoutCompleted プロパティよりも優先されます。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-183">If specified, this parameter overrides the defaultLogoutCompleted property.</span></span> |
| <span data-ttu-id="9c9dd-184">失敗したコールバック</span><span class="sxs-lookup"><span data-stu-id="9c9dd-184">failedCallback</span></span> | <span data-ttu-id="9c9dd-185">省略可能 (既定値は null)。ログインが失敗したときに呼び出す関数。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-185">Optional (defaults to null).The function to call when the login has failed.</span></span> <span data-ttu-id="9c9dd-186">指定した場合、このパラメーターは Defaultの Callback プロパティよりも優先されます。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-186">If specified, this parameter overrides the defaultFailedCallback property.</span></span> |
| <span data-ttu-id="9c9dd-187">userContext</span><span class="sxs-lookup"><span data-stu-id="9c9dd-187">userContext</span></span> | <span data-ttu-id="9c9dd-188">省略可能 (既定値は null)。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-188">Optional (defaults to null).</span></span> <span data-ttu-id="9c9dd-189">コールバック関数に渡される必要があるカスタムユーザーコンテキストデータ。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-189">Custom user context data that should be passed to the callback functions.</span></span> |

<span data-ttu-id="9c9dd-190">*戻り値:*</span><span class="sxs-lookup"><span data-stu-id="9c9dd-190">*Return Value:*</span></span>

<span data-ttu-id="9c9dd-191">この関数には、戻り値は含まれません。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-191">This function does not include a return value.</span></span> <span data-ttu-id="9c9dd-192">ただし、この関数の呼び出しの完了時には、いくつかの動作が含まれます。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-192">However, a number of behaviors are included upon completion of a call to this function:</span></span>

- <span data-ttu-id="9c9dd-193">`redirectUrl` パラメーターが null でも空の文字列でもない場合、現在のページは更新されるか、または変更されます。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-193">The current page will either be refreshed or be changed if the `redirectUrl` parameter was neither null nor an empty string.</span></span>
- <span data-ttu-id="9c9dd-194">ただし、パラメーターが null または空の文字列の場合は、`logoutCompletedCallback` パラメーター、または `defaultLogoutCompletedCallback` プロパティが呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-194">However, if the parameter was null or an empty string, the `logoutCompletedCallback` parameter, or `defaultLogoutCompletedCallback` property is called.</span></span>
- <span data-ttu-id="9c9dd-195">Web サービスへの呼び出しが失敗した場合、`defaultFailedCallback` プロパティの `failedCallback` パラメーターが呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-195">If the call to the web service fails, the `failedCallback` parameter of `defaultFailedCallback` property is called.</span></span>

<span data-ttu-id="9c9dd-196">*Default失敗コールバックプロパティ (get、set):*</span><span class="sxs-lookup"><span data-stu-id="9c9dd-196">*defaultFailedCallback property (get, set):*</span></span>

<span data-ttu-id="9c9dd-197">このプロパティは、web サービスとの通信エラーが発生した場合に呼び出される必要がある関数を指定します。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-197">This property specifies a function that should be called if a failure to communicate with the web service occurs.</span></span> <span data-ttu-id="9c9dd-198">デリゲート (または関数参照) を受け取る必要があります。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-198">It should receive a delegate (or function reference).</span></span>

<span data-ttu-id="9c9dd-199">このプロパティで指定される関数参照は、次のシグネチャを持つ必要があります。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-199">The function reference specified by this property should have the following signature:</span></span>

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample2.js)]

<span data-ttu-id="9c9dd-200">*パラメータ*</span><span class="sxs-lookup"><span data-stu-id="9c9dd-200">*Parameters:*</span></span>

| <span data-ttu-id="9c9dd-201">**パラメーター名**</span><span class="sxs-lookup"><span data-stu-id="9c9dd-201">**Parameter Name**</span></span> | <span data-ttu-id="9c9dd-202">**通用**</span><span class="sxs-lookup"><span data-stu-id="9c9dd-202">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="9c9dd-203">エラー</span><span class="sxs-lookup"><span data-stu-id="9c9dd-203">error</span></span> | <span data-ttu-id="9c9dd-204">エラー情報を指定します。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-204">Specifies the error information.</span></span> |
| <span data-ttu-id="9c9dd-205">userContext</span><span class="sxs-lookup"><span data-stu-id="9c9dd-205">userContext</span></span> | <span data-ttu-id="9c9dd-206">Login または logout 関数が呼び出されたときに指定されたユーザーコンテキスト情報を指定します。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-206">Specifies the user context information provided when the login or logout function was called.</span></span> |
| <span data-ttu-id="9c9dd-207">methodName</span><span class="sxs-lookup"><span data-stu-id="9c9dd-207">methodName</span></span> | <span data-ttu-id="9c9dd-208">呼び出し元のメソッドの名前。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-208">The name of the calling method.</span></span> |

<span data-ttu-id="9c9dd-209">*defaultLoginCompletedCallback プロパティ (get、set):*</span><span class="sxs-lookup"><span data-stu-id="9c9dd-209">*defaultLoginCompletedCallback property (get, set):*</span></span>

<span data-ttu-id="9c9dd-210">このプロパティは、ログイン web サービスの呼び出しが完了したときに呼び出される必要がある関数を指定します。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-210">This property specifies a function that should be called when the login web service call has completed.</span></span> <span data-ttu-id="9c9dd-211">デリゲート (または関数参照) を受け取る必要があります。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-211">It should receive a delegate (or function reference).</span></span>

<span data-ttu-id="9c9dd-212">このプロパティで指定される関数参照は、次のシグネチャを持つ必要があります。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-212">The function reference specified by this property should have the following signature:</span></span>

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample3.js)]

<span data-ttu-id="9c9dd-213">*パラメータ*</span><span class="sxs-lookup"><span data-stu-id="9c9dd-213">*Parameters:*</span></span>

| <span data-ttu-id="9c9dd-214">**パラメーター名**</span><span class="sxs-lookup"><span data-stu-id="9c9dd-214">**Parameter Name**</span></span> | <span data-ttu-id="9c9dd-215">**通用**</span><span class="sxs-lookup"><span data-stu-id="9c9dd-215">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="9c9dd-216">validCredentials</span><span class="sxs-lookup"><span data-stu-id="9c9dd-216">validCredentials</span></span> | <span data-ttu-id="9c9dd-217">ユーザーが有効な資格情報を指定したかどうかを指定します。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-217">Specifies whether the user provided valid credentials.</span></span> <span data-ttu-id="9c9dd-218">ユーザーが正常にログインした場合は `true`。それ以外の場合は `false`。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-218">`true` if the user successfully logged in; otherwise `false`.</span></span> |
| <span data-ttu-id="9c9dd-219">userContext</span><span class="sxs-lookup"><span data-stu-id="9c9dd-219">userContext</span></span> | <span data-ttu-id="9c9dd-220">Login 関数が呼び出されたときに指定されたユーザーコンテキスト情報を指定します。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-220">Specifies the user context information provided when the login function was called.</span></span> |
| <span data-ttu-id="9c9dd-221">methodName</span><span class="sxs-lookup"><span data-stu-id="9c9dd-221">methodName</span></span> | <span data-ttu-id="9c9dd-222">呼び出し元のメソッドの名前。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-222">The name of the calling method.</span></span> |

<span data-ttu-id="9c9dd-223">*defaultLogoutCompletedCallback プロパティ (get、set):*</span><span class="sxs-lookup"><span data-stu-id="9c9dd-223">*defaultLogoutCompletedCallback property (get, set):*</span></span>

<span data-ttu-id="9c9dd-224">このプロパティは、ログアウト web サービスの呼び出しが完了したときに呼び出される必要がある関数を指定します。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-224">This property specifies a function that should be called when the logout web service call has completed.</span></span> <span data-ttu-id="9c9dd-225">デリゲート (または関数参照) を受け取る必要があります。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-225">It should receive a delegate (or function reference).</span></span>

<span data-ttu-id="9c9dd-226">このプロパティで指定される関数参照は、次のシグネチャを持つ必要があります。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-226">The function reference specified by this property should have the following signature:</span></span>

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample4.js)]

<span data-ttu-id="9c9dd-227">*パラメータ*</span><span class="sxs-lookup"><span data-stu-id="9c9dd-227">*Parameters:*</span></span>

| <span data-ttu-id="9c9dd-228">**パラメーター名**</span><span class="sxs-lookup"><span data-stu-id="9c9dd-228">**Parameter Name**</span></span> | <span data-ttu-id="9c9dd-229">**通用**</span><span class="sxs-lookup"><span data-stu-id="9c9dd-229">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="9c9dd-230">result</span><span class="sxs-lookup"><span data-stu-id="9c9dd-230">result</span></span> | <span data-ttu-id="9c9dd-231">このパラメーターは常に `null`になります。将来使用するために予約されています。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-231">This parameter will always be `null`; it is reserved for future use.</span></span> |
| <span data-ttu-id="9c9dd-232">userContext</span><span class="sxs-lookup"><span data-stu-id="9c9dd-232">userContext</span></span> | <span data-ttu-id="9c9dd-233">Login 関数が呼び出されたときに指定されたユーザーコンテキスト情報を指定します。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-233">Specifies the user context information provided when the login function was called.</span></span> |
| <span data-ttu-id="9c9dd-234">methodName</span><span class="sxs-lookup"><span data-stu-id="9c9dd-234">methodName</span></span> | <span data-ttu-id="9c9dd-235">呼び出し元のメソッドの名前。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-235">The name of the calling method.</span></span> |

<span data-ttu-id="9c9dd-236">*isLoggedIn プロパティ (get):*</span><span class="sxs-lookup"><span data-stu-id="9c9dd-236">*isLoggedIn property (get):*</span></span>

<span data-ttu-id="9c9dd-237">このプロパティは、ユーザーの現在の認証状態を取得します。これは、ページ要求中に ScriptManager オブジェクトによって設定されます。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-237">This property gets the current authentication state of the user; it is set by the ScriptManager object during a page request.</span></span>

<span data-ttu-id="9c9dd-238">このプロパティは、ユーザーが現在ログインしている場合に `true` を返します。それ以外の場合は `false`を返します。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-238">This property returns `true` if the user is currently logged in; otherwise, it returns `false`.</span></span>

<span data-ttu-id="9c9dd-239">*path プロパティ (get、set):*</span><span class="sxs-lookup"><span data-stu-id="9c9dd-239">*path property (get, set):*</span></span>

<span data-ttu-id="9c9dd-240">このプロパティは、認証 web サービスの場所をプログラムによって決定します。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-240">This property programmatically determines the location of the authentication web service.</span></span> <span data-ttu-id="9c9dd-241">既定の認証プロバイダー、および ScriptManager コントロールの AuthenticationService 子ノードの Path プロパティで宣言によって宣言された1つのセットをオーバーライドするために使用できます (詳細については、「カスタム認証サービスプロバイダーの使用」を参照してください)。次のトピックを参照してください。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-241">It can be used to override the default authentication provider, as well as one set declaratively in the Path property of the ScriptManager control's AuthenticationService child node (for more information, see the Using a Custom Authentication Service Provider topic below).</span></span>

<span data-ttu-id="9c9dd-242">既定の認証サービスの場所は変更されないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-242">Note that the location of the default authentication service does not change.</span></span> <span data-ttu-id="9c9dd-243">ただし、ASP.NET AJAX では、ASP.NET AJAX authentication service プロキシと同じクラスインターフェイスを提供する web サービスの場所を指定できます。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-243">However, ASP.NET AJAX allows you to specify the location of a web service that provides the same class interface as the ASP.NET AJAX authentication service proxy.</span></span>

<span data-ttu-id="9c9dd-244">また、このプロパティは、現在のサイトからスクリプト要求を送信する値に設定しないでください。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-244">Note also that this property should not be set to a value that directs the script request off of the current site.</span></span> <span data-ttu-id="9c9dd-245">現在のアプリケーションは認証資格情報を受信しないため、役に立ちません。また、AJAX の基盤となるテクノロジは、クロスサイト要求を送信しないようにする必要があります。また、クライアントブラウザーでセキュリティ例外が発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-245">Because the current application would not receive the authentication credentials, it would be useless; also, the technology underlying AJAX should not post cross-site requests, and may generate a security exception in the client browser.</span></span>

<span data-ttu-id="9c9dd-246">このプロパティは、認証 web サービスへのパスを表す `String` オブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-246">This property is a `String` object representing the path to the authentication web service.</span></span>

<span data-ttu-id="9c9dd-247">*timeout プロパティ (get、set):*</span><span class="sxs-lookup"><span data-stu-id="9c9dd-247">*timeout property (get, set):*</span></span>

<span data-ttu-id="9c9dd-248">このプロパティは、ログイン要求が失敗したことを前提として、認証サービスを待機する時間の長さを決定します。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-248">This property determines the length of time to wait for the authentication service before assuming the login request has failed.</span></span> <span data-ttu-id="9c9dd-249">の呼び出しが完了するのを待機している間にタイムアウトが経過した場合、要求が失敗したコールバックが呼び出され、呼び出しは完了しません。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-249">If the timeout expires while waiting for a call to complete, the request-failed callback will be called, and the call will not complete.</span></span>

<span data-ttu-id="9c9dd-250">このプロパティは、認証サービスからの結果を待機するミリ秒数を表す `Number` オブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-250">This property is a `Number` object representing the number of milliseconds to wait for results from the authentication service.</span></span>

<span data-ttu-id="9c9dd-251">*コードサンプル: 認証サービスへのログイン*</span><span class="sxs-lookup"><span data-stu-id="9c9dd-251">*Code Sample: Logging into the Authentication Service*</span></span>

<span data-ttu-id="9c9dd-252">次のマークアップは、AuthenticationService クラスの login メソッドと logout メソッドへの単純なスクリプト呼び出しを含む ASP.NET ページの例です。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-252">The following markup is an example ASP.NET page with a simple script call to the login and logout methods of the AuthenticationService class.</span></span>

[!code-aspx[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample5.aspx)]

## <a name="accessing-aspnet-profiling-data-via-ajax"></a><span data-ttu-id="9c9dd-253">AJAX を使用した ASP.NET プロファイルデータへのアクセス</span><span class="sxs-lookup"><span data-stu-id="9c9dd-253">Accessing ASP.NET Profiling Data via AJAX</span></span>

<span data-ttu-id="9c9dd-254">ASP.NET プロファイリングサービスも ASP.NET AJAX 拡張機能を介して公開されます。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-254">The ASP.NET profiling service is also exposed through the ASP.NET AJAX Extensions.</span></span> <span data-ttu-id="9c9dd-255">ASP.NET プロファイルサービスは、ユーザーデータを格納および取得するための豊富で詳細な API を提供しているため、これは優れた生産性向上ツールになります。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-255">Since the ASP.NET profiling service provides a rich, granular API by which to store and retrieve user data, this can be an excellent productivity tool.</span></span>

<span data-ttu-id="9c9dd-256">Web.config でプロファイルサービスが有効になっている必要があります。既定ではありません。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-256">The profile service must be enabled in web.config; it is not by default.</span></span> <span data-ttu-id="9c9dd-257">これを行うには、`profileService` の子要素が web.config で指定されていることを確認し、次のように読み取りまたは書き込みが可能なプロパティを指定します。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-257">To do so, ensure that the `profileService` child element has enabled= true specified in web.config, and that you have specified which properties can be read or written as follows:</span></span>

[!code-xml[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample6.xml)]

<span data-ttu-id="9c9dd-258">プロファイルサービスも構成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-258">The profile service must also be configured.</span></span> <span data-ttu-id="9c9dd-259">プロファイルサービスの構成はこのホワイトペーパーの範囲外ですが、プロファイル構成設定で定義されているグループは、グループ名のサブプロパティとしてアクセスできることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-259">Although configuration of the profiling service is outside of the scope of this whitepaper, it is worthwhile to note that groups as defined in profile configuration settings will be accessible as sub-properties of the group name.</span></span> <span data-ttu-id="9c9dd-260">たとえば、次のプロファイルセクションが指定されているとします。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-260">For example, with the following profile section specified:</span></span>

[!code-xml[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample7.xml)]

<span data-ttu-id="9c9dd-261">クライアントスクリプトは、ProfileService クラスの properties フィールドのプロパティとして、Name、address... Line2、address. City、address. 市区町村、および BackgroundColor にアクセスできるようになります。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-261">Client script would be able to access Name, Address.Line1, Address.Line2, Address.City, Address.State, Address.Zip, and BackgroundColor as properties of the properties field of the ProfileService class.</span></span>

<span data-ttu-id="9c9dd-262">AJAX プロファイルサービスが構成されると、ページですぐに使用できるようになります。ただし、使用する前に1回読み込む必要があります。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-262">Once the AJAX Profiling Service is configured, it will be immediately available in pages; however, it will have to be loaded once before use.</span></span>

<span data-ttu-id="9c9dd-263">*サービスのメンバー*</span><span class="sxs-lookup"><span data-stu-id="9c9dd-263">*Sys.Services.ProfileService members*</span></span>

<span data-ttu-id="9c9dd-264">*プロパティフィールド:*</span><span class="sxs-lookup"><span data-stu-id="9c9dd-264">*properties field:*</span></span>

<span data-ttu-id="9c9dd-265">プロパティフィールドは、構成されているすべてのプロファイルデータを、ドット演算子名の規則で参照できる子プロパティとして公開します。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-265">The properties field exposes all configured profile data as child properties that can be referenced by the dot-operator-name convention.</span></span> <span data-ttu-id="9c9dd-266">プロパティグループの子であるプロパティは、GroupName. PropertyName と呼ばれます。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-266">Properties that are children of property groups are referred to as GroupName.PropertyName.</span></span> <span data-ttu-id="9c9dd-267">上記のプロファイル構成の例では、ユーザーの状態を取得するために、次の識別子を使用できます。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-267">In the example profile configuration presented above, to get the state of the user, you could use the following identifier:</span></span>

[!code-csharp[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample8.cs)]

<span data-ttu-id="9c9dd-268">*load メソッド:*</span><span class="sxs-lookup"><span data-stu-id="9c9dd-268">*load method:*</span></span>

<span data-ttu-id="9c9dd-269">サーバーから選択された一覧またはすべてのプロパティを読み込みます。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-269">Loads a selected list or all properties from the server.</span></span>

<span data-ttu-id="9c9dd-270">*パラメータ*</span><span class="sxs-lookup"><span data-stu-id="9c9dd-270">*Parameters:*</span></span>

| <span data-ttu-id="9c9dd-271">**パラメーター名**</span><span class="sxs-lookup"><span data-stu-id="9c9dd-271">**Parameter Name**</span></span> | <span data-ttu-id="9c9dd-272">**通用**</span><span class="sxs-lookup"><span data-stu-id="9c9dd-272">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="9c9dd-273">propertyNames</span><span class="sxs-lookup"><span data-stu-id="9c9dd-273">propertyNames</span></span> | <span data-ttu-id="9c9dd-274">省略可能 (既定値は null)。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-274">Optional (defaults to null).</span></span> <span data-ttu-id="9c9dd-275">サーバーから読み込まれるプロパティ。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-275">The properties to be loaded from the server.</span></span> |
| <span data-ttu-id="9c9dd-276">loadCompletedCallback</span><span class="sxs-lookup"><span data-stu-id="9c9dd-276">loadCompletedCallback</span></span> | <span data-ttu-id="9c9dd-277">省略可能 (既定値は null)。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-277">Optional (defaults to null).</span></span> <span data-ttu-id="9c9dd-278">読み込みが完了したときに呼び出す関数。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-278">The function to call when loading has completed.</span></span> |
| <span data-ttu-id="9c9dd-279">失敗したコールバック</span><span class="sxs-lookup"><span data-stu-id="9c9dd-279">failedCallback</span></span> | <span data-ttu-id="9c9dd-280">省略可能 (既定値は null)。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-280">Optional (defaults to null).</span></span> <span data-ttu-id="9c9dd-281">エラーが発生した場合に呼び出される関数。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-281">The function to call if an error occurs.</span></span> |
| <span data-ttu-id="9c9dd-282">userContext</span><span class="sxs-lookup"><span data-stu-id="9c9dd-282">userContext</span></span> | <span data-ttu-id="9c9dd-283">省略可能 (既定値は null)。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-283">Optional (defaults to null).</span></span> <span data-ttu-id="9c9dd-284">コールバック関数に渡されるコンテキスト情報。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-284">Context information to be passed to the callback function.</span></span> |

<span data-ttu-id="9c9dd-285">Load 関数に戻り値がありません。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-285">The load function does not have a return value.</span></span> <span data-ttu-id="9c9dd-286">呼び出しが正常に完了した場合は、`loadCompletedCallback` パラメーターまたは `defaultLoadCompletedCallback` のいずれかのプロパティが呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-286">If the call completed successfully, it will call either the `loadCompletedCallback` parameter or `defaultLoadCompletedCallback` property.</span></span> <span data-ttu-id="9c9dd-287">呼び出しが失敗した場合、またはタイムアウトが経過した場合は、`failedCallback` パラメーターまたは `defaultFailedCallback` プロパティのいずれかが呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-287">If the call failed, or the timeout expired, either the `failedCallback` parameter or `defaultFailedCallback` property will be called.</span></span>

<span data-ttu-id="9c9dd-288">`propertyNames` パラメーターが指定されていない場合は、読み取りが構成されているすべてのプロパティがサーバーから取得されます。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-288">If the `propertyNames` parameter is not supplied, all read-configured properties are retrieved from the server.</span></span>

<span data-ttu-id="9c9dd-289">*メソッドの保存:*</span><span class="sxs-lookup"><span data-stu-id="9c9dd-289">*save method:*</span></span>

<span data-ttu-id="9c9dd-290">Save () メソッドは、指定されたプロパティリスト (またはすべてのプロパティ) をユーザーの ASP.NET プロファイルに保存します。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-290">The save() method saves the specified property list (or all properties) to the user's ASP.NET profile.</span></span>

<span data-ttu-id="9c9dd-291">*パラメータ*</span><span class="sxs-lookup"><span data-stu-id="9c9dd-291">*Parameters:*</span></span>

| <span data-ttu-id="9c9dd-292">**パラメーター名**</span><span class="sxs-lookup"><span data-stu-id="9c9dd-292">**Parameter Name**</span></span> | <span data-ttu-id="9c9dd-293">**通用**</span><span class="sxs-lookup"><span data-stu-id="9c9dd-293">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="9c9dd-294">propertyNames</span><span class="sxs-lookup"><span data-stu-id="9c9dd-294">propertyNames</span></span> | <span data-ttu-id="9c9dd-295">省略可能 (既定値は null)。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-295">Optional (defaults to null).</span></span> <span data-ttu-id="9c9dd-296">サーバーに保存するプロパティです。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-296">The properties to be saved to the server.</span></span> |
| <span data-ttu-id="9c9dd-297">saveCompletedCallback</span><span class="sxs-lookup"><span data-stu-id="9c9dd-297">saveCompletedCallback</span></span> | <span data-ttu-id="9c9dd-298">省略可能 (既定値は null)。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-298">Optional (defaults to null).</span></span> <span data-ttu-id="9c9dd-299">保存が完了したときに呼び出す関数。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-299">The function to call when saving has completed.</span></span> |
| <span data-ttu-id="9c9dd-300">失敗したコールバック</span><span class="sxs-lookup"><span data-stu-id="9c9dd-300">failedCallback</span></span> | <span data-ttu-id="9c9dd-301">省略可能 (既定値は null)。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-301">Optional (defaults to null).</span></span> <span data-ttu-id="9c9dd-302">エラーが発生した場合に呼び出される関数。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-302">The function to call if an error occurs.</span></span> |
| <span data-ttu-id="9c9dd-303">userContext</span><span class="sxs-lookup"><span data-stu-id="9c9dd-303">userContext</span></span> | <span data-ttu-id="9c9dd-304">省略可能 (既定値は null)。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-304">Optional (defaults to null).</span></span> <span data-ttu-id="9c9dd-305">コールバック関数に渡されるコンテキスト情報。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-305">Context information to be passed to the callback function.</span></span> |

<span data-ttu-id="9c9dd-306">Save 関数に戻り値がありません。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-306">The save function does not have a return value.</span></span> <span data-ttu-id="9c9dd-307">呼び出しが正常に完了した場合は、`saveCompletedCallback` パラメーターまたは `defaultSaveCompletedCallback` のいずれかのプロパティが呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-307">If the call completes successfully, it will call either the `saveCompletedCallback` parameter or `defaultSaveCompletedCallback` property.</span></span> <span data-ttu-id="9c9dd-308">呼び出しが失敗した場合、またはタイムアウトが経過した場合は、`failedCallback` または `defaultFailedCallback` のいずれかのプロパティが呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-308">If the call failed, or the timeout expired, either the `failedCallback` or `defaultFailedCallback` property will be called.</span></span>

<span data-ttu-id="9c9dd-309">`propertyNames` パラメーターが null の場合は、すべてのプロファイルプロパティがサーバーに送信され、サーバーは保存できるプロパティと実行できないプロパティを決定します。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-309">If the `propertyNames` parameter is null, all profile properties will be sent to the server, and the server will decide which properties can be saved and which cannot.</span></span>

<span data-ttu-id="9c9dd-310">*Default失敗コールバックプロパティ (get、set):*</span><span class="sxs-lookup"><span data-stu-id="9c9dd-310">*defaultFailedCallback property (get, set):*</span></span>

<span data-ttu-id="9c9dd-311">このプロパティは、web サービスとの通信エラーが発生した場合に呼び出される必要がある関数を指定します。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-311">This property specifies a function that should be called if a failure to communicate with the web service occurs.</span></span> <span data-ttu-id="9c9dd-312">デリゲート (または関数参照) を受け取る必要があります。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-312">It should receive a delegate (or function reference).</span></span>

<span data-ttu-id="9c9dd-313">このプロパティで指定される関数参照は、次のシグネチャを持つ必要があります。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-313">The function reference specified by this property should have the following signature:</span></span>

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample9.js)]

<span data-ttu-id="9c9dd-314">*パラメータ*</span><span class="sxs-lookup"><span data-stu-id="9c9dd-314">*Parameters:*</span></span>

| <span data-ttu-id="9c9dd-315">**パラメーター名**</span><span class="sxs-lookup"><span data-stu-id="9c9dd-315">**Parameter Name**</span></span> | <span data-ttu-id="9c9dd-316">**通用**</span><span class="sxs-lookup"><span data-stu-id="9c9dd-316">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="9c9dd-317">エラー</span><span class="sxs-lookup"><span data-stu-id="9c9dd-317">Error</span></span> | <span data-ttu-id="9c9dd-318">エラー情報を指定します。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-318">Specifies the error information.</span></span> |
| <span data-ttu-id="9c9dd-319">userContext</span><span class="sxs-lookup"><span data-stu-id="9c9dd-319">userContext</span></span> | <span data-ttu-id="9c9dd-320">Load または save 関数が呼び出されたときに指定されたユーザーコンテキスト情報を指定します。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-320">Specifies the user context information provided when the load or save function was called.</span></span> |
| <span data-ttu-id="9c9dd-321">methodName</span><span class="sxs-lookup"><span data-stu-id="9c9dd-321">methodName</span></span> | <span data-ttu-id="9c9dd-322">呼び出し元のメソッドの名前。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-322">The name of the calling method.</span></span> |

<span data-ttu-id="9c9dd-323">*defaultSaveCompleted プロパティ (get、set):*</span><span class="sxs-lookup"><span data-stu-id="9c9dd-323">*defaultSaveCompleted property (get, set):*</span></span>

<span data-ttu-id="9c9dd-324">このプロパティは、ユーザーのプロファイルデータの保存が完了したときに呼び出す必要がある関数を指定します。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-324">This property specifies a function that should be called upon the completion of saving the user's profile data.</span></span> <span data-ttu-id="9c9dd-325">デリゲート (または関数参照) を受け取る必要があります。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-325">It should receive a delegate (or function reference).</span></span>

<span data-ttu-id="9c9dd-326">このプロパティで指定される関数参照は、次のシグネチャを持つ必要があります。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-326">The function reference specified by this property should have the following signature:</span></span>

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample10.js)]

<span data-ttu-id="9c9dd-327">*パラメータ*</span><span class="sxs-lookup"><span data-stu-id="9c9dd-327">*Parameters:*</span></span>

| <span data-ttu-id="9c9dd-328">**パラメーター名**</span><span class="sxs-lookup"><span data-stu-id="9c9dd-328">**Parameter Name**</span></span> | <span data-ttu-id="9c9dd-329">**通用**</span><span class="sxs-lookup"><span data-stu-id="9c9dd-329">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="9c9dd-330">numPropsSaved</span><span class="sxs-lookup"><span data-stu-id="9c9dd-330">numPropsSaved</span></span> | <span data-ttu-id="9c9dd-331">保存されたプロパティの数を指定します。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-331">Specifies the number of properties that were saved.</span></span> |
| <span data-ttu-id="9c9dd-332">userContext</span><span class="sxs-lookup"><span data-stu-id="9c9dd-332">userContext</span></span> | <span data-ttu-id="9c9dd-333">Load または save 関数が呼び出されたときに指定されたユーザーコンテキスト情報を指定します。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-333">Specifies the user context information provided when the load or save function was called.</span></span> |
| <span data-ttu-id="9c9dd-334">methodName</span><span class="sxs-lookup"><span data-stu-id="9c9dd-334">methodName</span></span> | <span data-ttu-id="9c9dd-335">呼び出し元のメソッドの名前。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-335">The name of the calling method.</span></span> |

<span data-ttu-id="9c9dd-336">*defaultLoadCompleted プロパティ (get、set):*</span><span class="sxs-lookup"><span data-stu-id="9c9dd-336">*defaultLoadCompleted property (get, set):*</span></span>

<span data-ttu-id="9c9dd-337">このプロパティは、ユーザーのプロファイルデータの読み込みが完了したときに呼び出す必要がある関数を指定します。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-337">This property specifies a function that should be called upon the completion of loading of the user's profile data.</span></span> <span data-ttu-id="9c9dd-338">デリゲート (または関数参照) を受け取る必要があります。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-338">It should receive a delegate (or function reference).</span></span>

<span data-ttu-id="9c9dd-339">このプロパティで指定される関数参照は、次のシグネチャを持つ必要があります。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-339">The function reference specified by this property should have the following signature:</span></span>

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample11.js)]

<span data-ttu-id="9c9dd-340">*パラメータ*</span><span class="sxs-lookup"><span data-stu-id="9c9dd-340">*Parameters:*</span></span>

| <span data-ttu-id="9c9dd-341">**パラメーター名**</span><span class="sxs-lookup"><span data-stu-id="9c9dd-341">**Parameter Name**</span></span> | <span data-ttu-id="9c9dd-342">**通用**</span><span class="sxs-lookup"><span data-stu-id="9c9dd-342">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="9c9dd-343">numPropsLoaded</span><span class="sxs-lookup"><span data-stu-id="9c9dd-343">numPropsLoaded</span></span> | <span data-ttu-id="9c9dd-344">読み込まれるプロパティの数を指定します。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-344">Specifies the number of properties loaded.</span></span> |
| <span data-ttu-id="9c9dd-345">userContext</span><span class="sxs-lookup"><span data-stu-id="9c9dd-345">userContext</span></span> | <span data-ttu-id="9c9dd-346">Load または save 関数が呼び出されたときに指定されたユーザーコンテキスト情報を指定します。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-346">Specifies the user context information provided when the load or save function was called.</span></span> |
| <span data-ttu-id="9c9dd-347">methodName</span><span class="sxs-lookup"><span data-stu-id="9c9dd-347">methodName</span></span> | <span data-ttu-id="9c9dd-348">呼び出し元のメソッドの名前。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-348">The name of the calling method.</span></span> |

<span data-ttu-id="9c9dd-349">*path プロパティ (get、set):*</span><span class="sxs-lookup"><span data-stu-id="9c9dd-349">*path property (get, set):*</span></span>

<span data-ttu-id="9c9dd-350">このプロパティは、プロファイル web サービスの場所をプログラムによって決定します。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-350">This property programmatically determines the location of the profile web service.</span></span> <span data-ttu-id="9c9dd-351">これを使用すると、ScriptManager コントロールの ProfileService 子ノードの Path プロパティで宣言された1つの設定だけでなく、既定のプロファイルサービスプロバイダーをオーバーライドできます。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-351">It can be used to override the default profile service provider, as well as one set declaratively in the Path property of the ScriptManager control's ProfileService child node.</span></span>

<span data-ttu-id="9c9dd-352">既定のプロファイルサービスの場所は変更されないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-352">Note that the location of the default profile service does not change.</span></span> <span data-ttu-id="9c9dd-353">ただし、ASP.NET AJAX では、ASP.NET AJAX authentication service プロキシと同じクラスインターフェイスを提供する web サービスの場所を指定できます。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-353">However, ASP.NET AJAX allows you to specify the location of a web service that provides the same class interface as the ASP.NET AJAX authentication service proxy.</span></span>

<span data-ttu-id="9c9dd-354">また、このプロパティは、現在のサイトからスクリプト要求を送信する値に設定しないでください。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-354">Note also that this property should not be set to a value that directs the script request off of the current site.</span></span> <span data-ttu-id="9c9dd-355">AJAX の基盤となるテクノロジは、クロスサイト要求を送信しないでください。クライアントブラウザーでセキュリティ例外が発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-355">The technology underlying AJAX should not post cross-site requests, and may generate a security exception in the client browser.</span></span>

<span data-ttu-id="9c9dd-356">このプロパティは、プロファイル web サービスへのパスを表す `String` オブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-356">This property is a `String` object representing the path to the profile web service.</span></span>

<span data-ttu-id="9c9dd-357">*timeout プロパティ (get、set):*</span><span class="sxs-lookup"><span data-stu-id="9c9dd-357">*timeout property (get, set):*</span></span>

<span data-ttu-id="9c9dd-358">このプロパティは、読み込み要求または保存要求が失敗したことを前提として、プロファイルサービスを待機する時間を指定します。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-358">This property determines the length of time to wait for the profile service before assuming the load or save request has failed.</span></span> <span data-ttu-id="9c9dd-359">の呼び出しが完了するのを待機している間にタイムアウトが経過した場合、要求が失敗したコールバックが呼び出され、呼び出しは完了しません。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-359">If the timeout expires while waiting for a call to complete, the request-failed callback will be called, and the call will not complete.</span></span>

<span data-ttu-id="9c9dd-360">このプロパティは、プロファイルサービスからの結果を待機するミリ秒数を表す `Number` オブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-360">This property is a `Number` object representing the number of milliseconds to wait for results from the profile service.</span></span>

<span data-ttu-id="9c9dd-361">*コードサンプル: ページ読み込み時のプロファイルデータの読み込み*</span><span class="sxs-lookup"><span data-stu-id="9c9dd-361">*Code sample: Loading profile data at page load*</span></span>

<span data-ttu-id="9c9dd-362">次のコードは、ユーザーが認証されているかどうかを確認し、存在する場合は、ユーザーの適切な背景色をページのとして読み込みます。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-362">The following code will check to see whether a user is authenticated, and if so, will load the user's preferred background color as the page's.</span></span>

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample12.js)]

## <a name="using-a-custom-authentication-service-provider"></a><span data-ttu-id="9c9dd-363">*カスタム認証サービスプロバイダーの使用*</span><span class="sxs-lookup"><span data-stu-id="9c9dd-363">*Using a Custom Authentication Service Provider*</span></span>

<span data-ttu-id="9c9dd-364">ASP.NET AJAX 拡張機能を使用すると、カスタム web サービスを使用して機能を公開することにより、カスタムスクリプト認証サービスプロバイダーを作成できます。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-364">The ASP.NET AJAX Extensions allow you to create a custom script authentication service provider by exposing your functionality through a custom web service.</span></span> <span data-ttu-id="9c9dd-365">使用するには、web サービスが2つのメソッド、`Login` と `Logout`を公開する必要があります。これらのメソッドは、既定の ASP.NET AJAX 認証 web サービスと同じメソッドシグネチャを使用して指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-365">In order to be used, your web service must expose two methods, `Login` and `Logout`; and these methods must be specified with the same method signatures as the default ASP.NET AJAX Authentication web service.</span></span>

<span data-ttu-id="9c9dd-366">カスタム web サービスを作成したら、そのサービスへのパスを指定する必要があります。これは、ページで宣言されているか、コード内でプログラムによって実行されるか、クライアントスクリプトを使用して行います。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-366">Once you have created the custom web service, you will need to specify the path to it, either declaratively on your page, programmatically in code, or via the client script.</span></span>

<span data-ttu-id="9c9dd-367">*パスを宣言によって設定するには*</span><span class="sxs-lookup"><span data-stu-id="9c9dd-367">*To set the path declaratively:*</span></span>

<span data-ttu-id="9c9dd-368">パスを宣言によって設定するには、ScriptManager オブジェクトの AuthenticationService 子を ASP.NET ページに追加します。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-368">To set the path declaratively, include the AuthenticationService child of the ScriptManager object on your ASP.NET page:</span></span>

[!code-aspx[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample13.aspx)]

<span data-ttu-id="9c9dd-369">*コードでパスを設定するには、次のようにします。*</span><span class="sxs-lookup"><span data-stu-id="9c9dd-369">*To set the path in code:*</span></span>

<span data-ttu-id="9c9dd-370">プログラムによってパスを設定するには、スクリプトマネージャーのインスタンスを使用してパスを指定します。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-370">To set the path programmatically, specify the path via the instance of your script manager:</span></span>

[!code-csharp[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample14.cs)]

<span data-ttu-id="9c9dd-371">*スクリプトでパスを設定するには、次のようにします。*</span><span class="sxs-lookup"><span data-stu-id="9c9dd-371">*To set the path in script:*</span></span>

<span data-ttu-id="9c9dd-372">スクリプトでパスをプログラムで設定するには、AuthenticationService クラスの `path` プロパティを使用します。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-372">To set the path programmatically in script, utilize the `path` property of the AuthenticationService class:</span></span>

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample15.js)]

<span data-ttu-id="9c9dd-373">*カスタム認証用のサンプル Web サービス*</span><span class="sxs-lookup"><span data-stu-id="9c9dd-373">*Sample Web Service for Custom Authentication*</span></span>

[!code-aspx[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample16.aspx)]

## <a name="summary"></a><span data-ttu-id="9c9dd-374">要約</span><span class="sxs-lookup"><span data-stu-id="9c9dd-374">Summary</span></span>

<span data-ttu-id="9c9dd-375">ASP.NET services-特に、プロファイル、メンバーシップ、および認証サービスは、クライアントブラウザーで JavaScript に簡単に公開されます。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-375">ASP.NET services - specifically the profiling, membership, and authentication services - are easily exposed to JavaScript on the client browser.</span></span> <span data-ttu-id="9c9dd-376">これにより、開発者はクライアント側のコードを認証メカニズムとシームレスに統合できます。これにより、UpdatePanels などのコントロールに依存せずに、大量の処理を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-376">This allows developers to integrate their client-side code with the authentication mechanism seamlessly, without depending on controls such as UpdatePanels to do the heavy lifting.</span></span> <span data-ttu-id="9c9dd-377">Web 構成設定を利用することで、プロファイルデータをクライアントからも保護できます。既定ではデータは使用できず、開発者はプロファイルプロパティをオプトインする必要があります。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-377">Profile data can be protected from the client as well, by utilizing web configuration settings; no data is available by default, and developers must opt-in to profile properties.</span></span>

<span data-ttu-id="9c9dd-378">さらに、同等のメソッドシグネチャを使用して簡略化された web サービス実装を作成することにより、開発者は、これらの組み込み ASP.NET サービス用のカスタムスクリプトプロバイダーを作成できます。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-378">Furthermore, by creating simplified web service implementations with equivalent method signatures, developers can create custom script providers for these intrinsic ASP.NET services.</span></span> <span data-ttu-id="9c9dd-379">これらの手法をサポートすることで、豊富なクライアントアプリケーションの開発が簡素化され、開発者は特定のニーズに合わせて幅広い柔軟性を得ることができます。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-379">Support for these techniques simplifies the development of rich client applications, while providing developers with a wide range of flexibility to meet specific needs.</span></span>

## <a name="bio"></a><span data-ttu-id="9c9dd-380">*略歴*</span><span class="sxs-lookup"><span data-stu-id="9c9dd-380">*Bio*</span></span>

<span data-ttu-id="9c9dd-381">Scott Cate は1997以来 Microsoft の Web テクノロジを使用しています。また、myKB.com ([www.myKB.com](http://www.myKB.com)) の大統領で、サポート技術情報のソフトウェアソリューションに重点を置いた ASP.NET ベースのアプリケーションを作成することを専門としています。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-381">Scott Cate has been working with Microsoft Web technologies since 1997 and is the President of myKB.com ([www.myKB.com](http://www.myKB.com)) where he specializes in writing ASP.NET based applications focused on Knowledge Base Software solutions.</span></span> <span data-ttu-id="9c9dd-382">Scott は、 [scott.cate@myKB.com](mailto:scott.cate@myKB.com)または彼のブログ ( [ScottCate.com](http://ScottCate.com) ) で、電子メールで連絡を受けることができます。</span><span class="sxs-lookup"><span data-stu-id="9c9dd-382">Scott can be contacted via email at [scott.cate@myKB.com](mailto:scott.cate@myKB.com) or his blog at [ScottCate.com](http://ScottCate.com)</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="9c9dd-383">[前へ](understanding-asp-net-ajax-updatepanel-triggers.md)
> [次へ](understanding-asp-net-ajax-localization.md)</span><span class="sxs-lookup"><span data-stu-id="9c9dd-383">[Previous](understanding-asp-net-ajax-updatepanel-triggers.md)
[Next](understanding-asp-net-ajax-localization.md)</span></span>
