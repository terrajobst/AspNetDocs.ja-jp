---
uid: mvc/overview/older-versions-1/nerddinner/secure-applications-using-authentication-and-authorization
title: 認証と承認を使用してアプリケーションをセキュリティで保護する |Microsoft Docs
author: microsoft
description: 手順 9. では、ユーザーが登録してサイトにログインして、作成する必要があるように、このアプリケーションをセキュリティで保護するための認証と承認を追加する方法を示します。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 9e4d5cac-b071-440c-b044-20b6d0c964fb
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/secure-applications-using-authentication-and-authorization
msc.type: authoredcontent
ms.openlocfilehash: 8d509c5f15bb4d5014e53b8dc2a736454238e72c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486424"
---
# <a name="secure-applications-using-authentication-and-authorization"></a><span data-ttu-id="554fb-103">認証と承認を利用した安全なアプリケーション</span><span class="sxs-lookup"><span data-stu-id="554fb-103">Secure Applications Using Authentication and Authorization</span></span>

<span data-ttu-id="554fb-104">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="554fb-104">by [Microsoft](https://github.com/microsoft)</span></span>

<span data-ttu-id="554fb-105">[[Download PDF]\(PDF をダウンロード\)](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)</span><span class="sxs-lookup"><span data-stu-id="554fb-105">[Download PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)</span></span>

> <span data-ttu-id="554fb-106">これは、ASP.NET MVC 1 を使用して小規模で完成した web アプリケーションを構築する方法を説明する、無料の["" アプリケーションのチュートリアル](introducing-the-nerddinner-tutorial.md)の手順9です。</span><span class="sxs-lookup"><span data-stu-id="554fb-106">This is step 9 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="554fb-107">手順 9. では、ユーザーが登録してサイトにログインして新しいディナーを作成する必要があり、ディナーをホストしているユーザーのみが後で編集できるようにするために、認証と承認を追加して、そのアプリケーションをセキュリティで保護する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="554fb-107">Step 9 shows how to add authentication and authorization to secure our NerdDinner application, so that users need to register and login to the site to create new dinners, and only the user who is hosting a dinner can edit it later.</span></span>
> 
> <span data-ttu-id="554fb-108">ASP.NET MVC 3 を使用している場合は、MVC 3 または[Mvc ミュージックストア](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)[のチュートリアルではじめに](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)に従うことをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="554fb-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-9-authentication-and-authorization"></a><span data-ttu-id="554fb-109">ステップ 9: 認証と承認</span><span class="sxs-lookup"><span data-stu-id="554fb-109">NerdDinner Step 9: Authentication and Authorization</span></span>

<span data-ttu-id="554fb-110">現在、このアプリケーションでは、サイトにアクセスするすべてのユーザーに、ディナーの詳細を作成および編集する権限を付与しています。</span><span class="sxs-lookup"><span data-stu-id="554fb-110">Right now our NerdDinner application grants anyone visiting the site the ability to create and edit the details of any dinner.</span></span> <span data-ttu-id="554fb-111">これを変更して、新しいディナーを作成するためにユーザーがサイトに登録してログインする必要があるようにして、ディナーをホストしているユーザーのみが後で編集できるように制限を追加してみましょう。</span><span class="sxs-lookup"><span data-stu-id="554fb-111">Let's change this so that users need to register and login to the site to create new dinners, and add a restriction so that only the user who is hosting a dinner can edit it later.</span></span>

<span data-ttu-id="554fb-112">これを有効にするには、アプリケーションをセキュリティで保護するために認証と承認を使用します。</span><span class="sxs-lookup"><span data-stu-id="554fb-112">To enable this we'll use authentication and authorization to secure our application.</span></span>

### <a name="understanding-authentication-and-authorization"></a><span data-ttu-id="554fb-113">認証と承認について</span><span class="sxs-lookup"><span data-stu-id="554fb-113">Understanding Authentication and Authorization</span></span>

<span data-ttu-id="554fb-114">*認証*は、アプリケーションにアクセスするクライアントの id を識別および検証するプロセスです。</span><span class="sxs-lookup"><span data-stu-id="554fb-114">*Authentication* is the process of identifying and validating the identity of a client accessing an application.</span></span> <span data-ttu-id="554fb-115">もっと簡単に説明すると、エンドユーザーが web サイトにアクセスしたときの "だれ" を特定することになります。</span><span class="sxs-lookup"><span data-stu-id="554fb-115">Put more simply, it is about identifying "who" the end-user is when they visit a website.</span></span> <span data-ttu-id="554fb-116">ASP.NET は、ブラウザーユーザーを認証するための複数の方法をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="554fb-116">ASP.NET supports multiple ways to authenticate browser users.</span></span> <span data-ttu-id="554fb-117">インターネット web アプリケーションの場合、使用される最も一般的な認証方法は "フォーム認証" と呼ばれます。</span><span class="sxs-lookup"><span data-stu-id="554fb-117">For Internet web applications, the most common authentication approach used is called "Forms Authentication".</span></span> <span data-ttu-id="554fb-118">フォーム認証を使用すると、開発者はアプリケーション内に HTML ログインフォームを作成し、エンドユーザーがデータベースまたは他のパスワード資格情報ストアに対して送信したユーザー名とパスワードを検証できます。</span><span class="sxs-lookup"><span data-stu-id="554fb-118">Forms Authentication enables a developer to author an HTML login form within their application, and then validate the username/password an end-user submits against a database or other password credential store.</span></span> <span data-ttu-id="554fb-119">ユーザー名とパスワードの組み合わせが正しい場合、開発者は、今後の要求でユーザーを識別するために、暗号化された HTTP クッキーを発行するように ASP.NET に要求できます。</span><span class="sxs-lookup"><span data-stu-id="554fb-119">If the username/password combination is correct, the developer can then ask ASP.NET to issue an encrypted HTTP cookie to identify the user across future requests.</span></span> <span data-ttu-id="554fb-120">フォーム認証を使用して、このアプリケーションを使用します。</span><span class="sxs-lookup"><span data-stu-id="554fb-120">We'll by using forms authentication with our NerdDinner application.</span></span>

<span data-ttu-id="554fb-121">*承認*とは、認証されたユーザーが特定の URL またはリソースにアクセスする権限を持っているか、何らかのアクションを実行する権限を持っているかどうかを判断するプロセスです。</span><span class="sxs-lookup"><span data-stu-id="554fb-121">*Authorization* is the process of determining whether an authenticated user has permission to access a particular URL/resource or to perform some action.</span></span> <span data-ttu-id="554fb-122">たとえば、世界中のアプリケーションでは、ログインしているユーザーのみが */Dins/create* URL にアクセスでき、新しいディナーを作成できることを承認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="554fb-122">For example, within our NerdDinner application we'll want to authorize that only users who are logged in can access the */Dinners/Create* URL and create new Dinners.</span></span> <span data-ttu-id="554fb-123">また、ディナーをホストしているユーザーのみが編集できるように承認ロジックを追加し、他のすべてのユーザーへの編集アクセスを拒否します。</span><span class="sxs-lookup"><span data-stu-id="554fb-123">We'll also want to add authorization logic so that only the user who is hosting a dinner can edit it – and deny edit access to all other users.</span></span>

### <a name="forms-authentication-and-the-accountcontroller"></a><span data-ttu-id="554fb-124">フォーム認証と AccountController</span><span class="sxs-lookup"><span data-stu-id="554fb-124">Forms Authentication and the AccountController</span></span>

<span data-ttu-id="554fb-125">新しい ASP.NET MVC アプリケーションが作成されると、ASP.NET MVC の既定の Visual Studio プロジェクトテンプレートによってフォーム認証が自動的に有効になります。</span><span class="sxs-lookup"><span data-stu-id="554fb-125">The default Visual Studio project template for ASP.NET MVC automatically enables forms authentication when new ASP.NET MVC applications are created.</span></span> <span data-ttu-id="554fb-126">また、事前に構築されたアカウントログインページの実装がプロジェクトに自動的に追加されるため、サイト内でのセキュリティの統合が非常に簡単になります。</span><span class="sxs-lookup"><span data-stu-id="554fb-126">It also automatically adds a pre-built account login page implementation to the project – which makes it really easy to integrate security within a site.</span></span>

<span data-ttu-id="554fb-127">既定のサイトのマスターページでは、アクセスしているユーザーが認証されていない場合に、サイトの右上に [ログオン] リンクが表示されます。</span><span class="sxs-lookup"><span data-stu-id="554fb-127">The default Site.master master page displays a "Log On" link at the top-right of the site when the user accessing it is not authenticated:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image1.png)

<span data-ttu-id="554fb-128">[ログオン] リンクをクリックすると、ユーザーは */アカウントのログオン*URL に移動します。</span><span class="sxs-lookup"><span data-stu-id="554fb-128">Clicking the "Log On" link takes a user to the */Account/LogOn* URL:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image2.png)

<span data-ttu-id="554fb-129">登録されていない訪問者は、"Register" リンクをクリックすることによってこれを行うことができます。これにより、/アカウント/*レジスタ*の URL に移動し、アカウントの詳細を入力できます。</span><span class="sxs-lookup"><span data-stu-id="554fb-129">Visitors who haven't registered can do so by clicking the "Register" link – which will take them to the */Account/Register* URL and allow them to enter account details:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image3.png)

<span data-ttu-id="554fb-130">[Register] \ (登録 \) ボタンをクリックすると、ASP.NET メンバーシップシステム内に新しいユーザーが作成され、フォーム認証を使用してユーザーがサイトで認証されます。</span><span class="sxs-lookup"><span data-stu-id="554fb-130">Clicking the "Register" button will create a new user within the ASP.NET Membership system, and authenticate the user onto the site using forms authentication.</span></span>

<span data-ttu-id="554fb-131">ユーザーがログインすると、ページの右上にある "Welcome [username]!" を出力するように変更されます。</span><span class="sxs-lookup"><span data-stu-id="554fb-131">When a user is logged-in, the Site.master changes the top-right of the page to output a "Welcome [username]!"</span></span> <span data-ttu-id="554fb-132">メッセージを表示し、"ログオン" ではなく "ログオフ" リンクを表示します。</span><span class="sxs-lookup"><span data-stu-id="554fb-132">message and renders a "Log Off" link instead of a "Log On" one.</span></span> <span data-ttu-id="554fb-133">[ログオフ] リンクをクリックすると、ユーザーがログアウトします。</span><span class="sxs-lookup"><span data-stu-id="554fb-133">Clicking the "Log Off" link logs out the user:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image4.png)

<span data-ttu-id="554fb-134">上記のログイン、ログアウト、および登録機能は、プロジェクトの作成時に Visual Studio によってプロジェクトに追加された AccountController クラス内に実装されます。</span><span class="sxs-lookup"><span data-stu-id="554fb-134">The above login, logout, and registration functionality is implemented within the AccountController class that was added to our project by Visual Studio when it created the project.</span></span> <span data-ttu-id="554fb-135">AccountController の UI は、\Views\Account ディレクトリ内のビューテンプレートを使用して実装されます。</span><span class="sxs-lookup"><span data-stu-id="554fb-135">The UI for the AccountController is implemented using view templates within the \Views\Account directory:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image5.png)

<span data-ttu-id="554fb-136">AccountController クラスは、暗号化された認証 cookie を発行するために ASP.NET Forms 認証システムを使用し、ユーザー名/パスワードを格納して検証するために ASP.NET Membership API を使用します。</span><span class="sxs-lookup"><span data-stu-id="554fb-136">The AccountController class uses the ASP.NET Forms Authentication system to issue encrypted authentication cookies, and the ASP.NET Membership API to store and validate usernames/passwords.</span></span> <span data-ttu-id="554fb-137">ASP.NET Membership API は拡張可能であり、任意のパスワード資格情報ストアを使用できます。</span><span class="sxs-lookup"><span data-stu-id="554fb-137">The ASP.NET Membership API is extensible and enables any password credential store to be used.</span></span> <span data-ttu-id="554fb-138">ASP.NET には、SQL データベース内、または Active Directory 内にユーザー名とパスワードを格納する、組み込みのメンバーシッププロバイダーの実装が付属しています。</span><span class="sxs-lookup"><span data-stu-id="554fb-138">ASP.NET ships with built-in membership provider implementations that store username/passwords within a SQL database, or within Active Directory.</span></span>

<span data-ttu-id="554fb-139">ここでは、プロジェクトのルートにある "web.config" ファイルを開き、その中の &lt;メンバーシップ&gt; セクションを検索することで、このアプリケーションで使用する必要があるメンバーシッププロバイダーを構成できます。</span><span class="sxs-lookup"><span data-stu-id="554fb-139">We can configure which membership provider our NerdDinner application should use by opening the "web.config" file at the root of the project and looking for the &lt;membership&gt; section within it.</span></span> <span data-ttu-id="554fb-140">プロジェクトの作成時に追加された既定の web.config は、SQL メンバーシッププロバイダーを登録し、データベースの場所を指定するために "ApplicationServices" という接続文字列を使用するように構成します。</span><span class="sxs-lookup"><span data-stu-id="554fb-140">The default web.config added when the project was created registers the SQL membership provider, and configures it to use a connection-string named "ApplicationServices" to specify the database location.</span></span>

<span data-ttu-id="554fb-141">Web.config ファイルの &lt;connectionStrings&gt; セクション内で指定されている既定の "ApplicationServices" 接続文字列は、SQL Express を使用するように構成されています。</span><span class="sxs-lookup"><span data-stu-id="554fb-141">The default "ApplicationServices" connection string (which is specified within the &lt;connectionStrings&gt; section of the web.config file) is configured to use SQL Express.</span></span> <span data-ttu-id="554fb-142">"ASPNETDB.MDF" という名前の SQL Express データベースを指します。MDF "アプリケーションの" App\_Data "ディレクトリにあります。</span><span class="sxs-lookup"><span data-stu-id="554fb-142">It points to a SQL Express database named "ASPNETDB.MDF" under the application's "App\_Data" directory.</span></span> <span data-ttu-id="554fb-143">アプリケーション内でメンバーシップ API を初めて使用するときに、このデータベースが存在しない場合、ASP.NET は自動的にデータベースを作成し、その中に適切なメンバーシップデータベーススキーマをプロビジョニングします。</span><span class="sxs-lookup"><span data-stu-id="554fb-143">If this database doesn't exist the first time the Membership API is used within the application, ASP.NET will automatically create the database and provision the appropriate membership database schema within it:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image6.png)

<span data-ttu-id="554fb-144">SQL Express を使用する代わりに、完全な SQL Server インスタンス (またはリモートデータベースへの接続) を使用する場合は、web.config ファイル内の "ApplicationServices" 接続文字列を更新して、適切なメンバーシップスキーマを確認するだけで済みます。は、が指すデータベースに追加されています。</span><span class="sxs-lookup"><span data-stu-id="554fb-144">If instead of using SQL Express we wanted to use a full SQL Server instance (or connect to a remote database), all we'd need to-do is to update the "ApplicationServices" connection string within the web.config file and make sure that the appropriate membership schema has been added to the database it points at.</span></span> <span data-ttu-id="554fb-145">\Windows\Microsoft.NET\Framework\v2.0.50727\ ディレクトリ内で "aspnet\_regsql .exe" ユーティリティを実行すると、メンバーシップとその他の ASP.NET アプリケーションサービスに適したスキーマをデータベースに追加できます。</span><span class="sxs-lookup"><span data-stu-id="554fb-145">You can run the "aspnet\_regsql.exe" utility within the \Windows\Microsoft.NET\Framework\v2.0.50727\ directory to add the appropriate schema for membership and the other ASP.NET application services to a database.</span></span>

### <a name="authorizing-the-dinnerscreate-url-using-the-authorize-filter"></a><span data-ttu-id="554fb-146">[承認] フィルターを使用して、/Dins/create URL を承認しています</span><span class="sxs-lookup"><span data-stu-id="554fb-146">Authorizing the /Dinners/Create URL using the [Authorize] filter</span></span>

<span data-ttu-id="554fb-147">セキュリティで保護された認証とアカウント管理の実装を、このアプリケーションに対して有効にするためのコードを作成する必要はありませんでした。</span><span class="sxs-lookup"><span data-stu-id="554fb-147">We didn't have to write any code to enable a secure authentication and account management implementation for the NerdDinner application.</span></span> <span data-ttu-id="554fb-148">ユーザーは、アプリケーションに新しいアカウントを登録し、サイトのログイン/ログアウトを行うことができます。</span><span class="sxs-lookup"><span data-stu-id="554fb-148">Users can register new accounts with our application, and login/logout of the site.</span></span>

<span data-ttu-id="554fb-149">これで、承認ロジックをアプリケーションに追加し、訪問者の認証状態とユーザー名を使用して、サイト内で実行できることとできないことを制御できます。</span><span class="sxs-lookup"><span data-stu-id="554fb-149">Now we can add authorization logic to the application, and use the authentication status and username of visitors to control what they can and can't do within the site.</span></span> <span data-ttu-id="554fb-150">最初に、Dinのコントローラークラスの "作成" アクションメソッドに承認ロジックを追加します。</span><span class="sxs-lookup"><span data-stu-id="554fb-150">Let's begin by adding authorization logic to the "Create" action methods of our DinnersController class.</span></span> <span data-ttu-id="554fb-151">具体的には、 */dinurl*にアクセスするユーザーがログインしている必要があります。</span><span class="sxs-lookup"><span data-stu-id="554fb-151">Specifically, we will require that users accessing the */Dinners/Create* URL must be logged in.</span></span> <span data-ttu-id="554fb-152">ログインしていない場合は、ログインページにリダイレクトして、サインインできるようにします。</span><span class="sxs-lookup"><span data-stu-id="554fb-152">If they aren't logged in we'll redirect them to the login page so that they can sign-in.</span></span>

<span data-ttu-id="554fb-153">このロジックの実装は非常に簡単です。</span><span class="sxs-lookup"><span data-stu-id="554fb-153">Implementing this logic is pretty easy.</span></span> <span data-ttu-id="554fb-154">必要なのは、次のように、Create アクションメソッドに [承認] フィルター属性を追加することだけです。</span><span class="sxs-lookup"><span data-stu-id="554fb-154">All we need to-do is to add an [Authorize] filter attribute to our Create action methods like so:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample1.cs)]

<span data-ttu-id="554fb-155">ASP.NET MVC では、アクションメソッドに宣言的に適用できる再利用可能なロジックを実装するために使用できる "アクションフィルター" を作成する機能がサポートされています。</span><span class="sxs-lookup"><span data-stu-id="554fb-155">ASP.NET MVC supports the ability to create "action filters" that can be used to implement re-usable logic that can be declaratively applied to action methods.</span></span> <span data-ttu-id="554fb-156">[承認] フィルターは、ASP.NET MVC によって提供される組み込みアクションフィルターの1つであり、開発者は、アクションメソッドとコントローラークラスに承認規則を宣言によって適用できます。</span><span class="sxs-lookup"><span data-stu-id="554fb-156">The [Authorize] filter is one of the built-in action filters provided by ASP.NET MVC, and it enables a developer to declaratively apply authorization rules to action methods and controller classes.</span></span>

<span data-ttu-id="554fb-157">パラメーターを指定せずに適用した場合 (上記のように)、[承認] フィルターによって、アクションメソッド要求を行うユーザーがログインする必要があることが強制されます。そうでない場合は、ブラウザーがログイン URL に自動的にリダイレクトされます。</span><span class="sxs-lookup"><span data-stu-id="554fb-157">When applied without any parameters (like above) the [Authorize] filter enforces that the user making the action method request must be logged in – and it will automatically redirect the browser to the login URL if they aren't.</span></span> <span data-ttu-id="554fb-158">このリダイレクトを実行すると、最初に要求された URL が querystring 引数として渡されます (例:/Account/LogOn)。ReturnUrl =% 2fDinners% 2fCreate)。</span><span class="sxs-lookup"><span data-stu-id="554fb-158">When doing this redirect the originally requested URL is passed as a querystring argument (for example: /Account/LogOn?ReturnUrl=%2fDinners%2fCreate).</span></span> <span data-ttu-id="554fb-159">その後、ユーザーがログインすると、AccountController は最初に要求された URL にリダイレクトします。</span><span class="sxs-lookup"><span data-stu-id="554fb-159">The AccountController will then redirect the user back to the originally requested URL once they login.</span></span>

<span data-ttu-id="554fb-160">[承認] フィルターでは、必要に応じて、ユーザーがログインしていること、許可されているユーザーの一覧、または許可されているセキュリティロールのメンバーであることを要求するために使用できる "ユーザー" プロパティまたは "ロール" プロパティを指定する機能がサポートされています。</span><span class="sxs-lookup"><span data-stu-id="554fb-160">The [Authorize] filter optionally supports the ability to specify a "Users" or "Roles" property that can be used to require that the user is both logged in and within a list of allowed users or a member of an allowed security role.</span></span> <span data-ttu-id="554fb-161">たとえば、次のコードでは、"scottgu" と "billg" という2つの特定のユーザーのみが、/Dins/create URL にアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="554fb-161">For example, the code below only allows two specific users, "scottgu" and "billg", to access the /Dinners/Create URL:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample2.cs)]

<span data-ttu-id="554fb-162">コード内に特定のユーザー名を埋め込むことは、それによって保守が容易になる傾向があります。</span><span class="sxs-lookup"><span data-stu-id="554fb-162">Embedding specific user names within code tends to be pretty un-maintainable though.</span></span> <span data-ttu-id="554fb-163">より適切な方法は、コードがチェックする上位レベルの "ロール" を定義し、データベースまたは active directory システムを使用してユーザーをロールにマップすることです (実際のユーザーマッピングリストをコードから外部に格納できるようにします)。</span><span class="sxs-lookup"><span data-stu-id="554fb-163">A better approach is to define higher-level "roles" that the code checks against, and then to map users into the role using either a database or active directory system (enabling the actual user mapping list to be stored externally from the code).</span></span> <span data-ttu-id="554fb-164">ASP.NET には、組み込みのロール管理 API だけでなく、組み込みのロールプロバイダーのセット (SQL および Active Directory 用のロールプロバイダーを含む) が含まれており、このユーザー/ロールマッピングを実行するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="554fb-164">ASP.NET includes a built-in role management API as well as a built-in set of role providers (including ones for SQL and Active Directory) that can help perform this user/role mapping.</span></span> <span data-ttu-id="554fb-165">次に、特定の "管理者" ロール内のユーザーのみが/Dins/create URL にアクセスできるようにコードを更新できます。</span><span class="sxs-lookup"><span data-stu-id="554fb-165">We could then update the code to only allow users within a specific "admin" role to access the /Dinners/Create URL:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample3.cs)]

### <a name="using-the-useridentityname-property-when-creating-dinners"></a><span data-ttu-id="554fb-166">ディナーを作成するときに User.Identity.Name プロパティを使用する</span><span class="sxs-lookup"><span data-stu-id="554fb-166">Using the User.Identity.Name property when Creating Dinners</span></span>

<span data-ttu-id="554fb-167">コントローラーの基本クラスで公開されている User.Identity.Name プロパティを使用して、要求の現在ログインしているユーザーのユーザー名を取得できます。</span><span class="sxs-lookup"><span data-stu-id="554fb-167">We can retrieve the username of the currently logged-in user of a request using the User.Identity.Name property exposed on the Controller base class.</span></span>

<span data-ttu-id="554fb-168">前に、Create () アクションメソッドの HTTP POST バージョンを実装したので、ディナーの "HostedBy" プロパティを静的文字列にハードコーディングしました。</span><span class="sxs-lookup"><span data-stu-id="554fb-168">Earlier when we implemented the HTTP-POST version of our Create() action method we had hardcoded the "HostedBy" property of the Dinner to a static string.</span></span> <span data-ttu-id="554fb-169">次に、User.Identity.Name プロパティを使用するようにこのコードを更新できるようになりました。また、ディナーを作成したホストの RSVP を自動的に追加することもできます。</span><span class="sxs-lookup"><span data-stu-id="554fb-169">We can now update this code to instead use the User.Identity.Name property, as well as automatically add an RSVP for the host creating the Dinner:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample4.cs)]

<span data-ttu-id="554fb-170">Create () メソッドに [承認] 属性を追加したので、ASP.NET MVC では、ユーザーがサイトにログインしている場合にのみ、アクションメソッドが実行されるようにしています。</span><span class="sxs-lookup"><span data-stu-id="554fb-170">Because we have added an [Authorize] attribute to the Create() method, ASP.NET MVC ensures that the action method only executes if the user visiting the /Dinners/Create URL is logged in on the site.</span></span> <span data-ttu-id="554fb-171">そのため、User.Identity.Name プロパティの値には、常に有効なユーザー名が含まれます。</span><span class="sxs-lookup"><span data-stu-id="554fb-171">As such, the User.Identity.Name property value will always contain a valid username.</span></span>

### <a name="using-the-useridentityname-property-when-editing-dinners"></a><span data-ttu-id="554fb-172">ディナーを編集するときに User.Identity.Name プロパティを使用する</span><span class="sxs-lookup"><span data-stu-id="554fb-172">Using the User.Identity.Name property when Editing Dinners</span></span>

<span data-ttu-id="554fb-173">ここで、ユーザー自身がホストしているディナーのプロパティのみを編集できるように、ユーザーを制限する認証ロジックを追加してみましょう。</span><span class="sxs-lookup"><span data-stu-id="554fb-173">Let's now add some authorization logic that restricts users so that they can only edit the properties of dinners they themselves are hosting.</span></span>

<span data-ttu-id="554fb-174">この問題を解決するには、まず、先ほど作成した Dinner.cs 部分クラス内で、ディナーオブジェクトに "IsHostedBy (username)" ヘルパーメソッドを追加します。</span><span class="sxs-lookup"><span data-stu-id="554fb-174">To help with this, we'll first add an "IsHostedBy(username)" helper method to our Dinner object (within the Dinner.cs partial class we built earlier).</span></span> <span data-ttu-id="554fb-175">このヘルパーメソッドは、指定されたユーザー名がディナー HostedBy プロパティに一致するかどうかに応じて true または false を返し、大文字と小文字を区別しない文字列比較を実行するために必要なロジックをカプセル化します。</span><span class="sxs-lookup"><span data-stu-id="554fb-175">This helper method returns true or false depending on whether a supplied username matches the Dinner HostedBy property, and encapsulates the logic necessary to perform a case-insensitive string comparison of them:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample5.cs)]

<span data-ttu-id="554fb-176">次に、Dinの Scontroller クラス内の Edit () アクションメソッドに [承認] 属性を追加します。</span><span class="sxs-lookup"><span data-stu-id="554fb-176">We'll then add an [Authorize] attribute to the Edit() action methods within our DinnersController class.</span></span> <span data-ttu-id="554fb-177">これにより、ユーザーは、// *//[id]* の URL を要求するようにログインする必要があります。</span><span class="sxs-lookup"><span data-stu-id="554fb-177">This will ensure that users must be logged in to request a */Dinners/Edit/[id]* URL.</span></span>

<span data-ttu-id="554fb-178">次に、IsHostedBy (username) ヘルパーメソッドを使用して、ログインしているユーザーがディナーホストと一致することを確認するコードを Edit メソッドに追加できます。</span><span class="sxs-lookup"><span data-stu-id="554fb-178">We can then add code to our Edit methods that uses the Dinner.IsHostedBy(username) helper method to verify that the logged-in user matches the Dinner host.</span></span> <span data-ttu-id="554fb-179">ユーザーがホストでない場合は、"InvalidOwner" ビューを表示し、要求を終了します。</span><span class="sxs-lookup"><span data-stu-id="554fb-179">If the user is not the host, we'll display an "InvalidOwner" view and terminate the request.</span></span> <span data-ttu-id="554fb-180">このコードは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="554fb-180">The code to do this looks like below:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample6.cs)]

<span data-ttu-id="554fb-181">次に、\Views\Dinners ディレクトリを右クリックし、[&gt;ビューの追加] メニューコマンドを選択して、新しい "InvalidOwner" ビューを作成します。</span><span class="sxs-lookup"><span data-stu-id="554fb-181">We can then right-click on the \Views\Dinners directory and choose the Add-&gt;View menu command to create a new "InvalidOwner" view.</span></span> <span data-ttu-id="554fb-182">これには、次のエラーメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="554fb-182">We'll populate it with the below error message:</span></span>

[!code-aspx[Main](secure-applications-using-authentication-and-authorization/samples/sample7.aspx)]

<span data-ttu-id="554fb-183">これで、ユーザーが所有していないディナーを編集しようとすると、次のエラーメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="554fb-183">And now when a user attempts to edit a dinner they don't own, they'll get an error message:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image7.png)

<span data-ttu-id="554fb-184">コントローラー内の Delete () アクションメソッドに対しても同じ手順を繰り返して、ディナーを削除するためのアクセス許可をロックダウンし、ディナーのホストだけが削除できるようにします。</span><span class="sxs-lookup"><span data-stu-id="554fb-184">We can repeat the same steps for the Delete() action methods within our controller to lock down permission to delete Dinners as well, and ensure that only the host of a Dinner can delete it.</span></span>

### <a name="showinghiding-edit-and-delete-links"></a><span data-ttu-id="554fb-185">編集と削除のリンクの表示/非表示</span><span class="sxs-lookup"><span data-stu-id="554fb-185">Showing/Hiding Edit and Delete Links</span></span>

<span data-ttu-id="554fb-186">この記事では、次のように、[詳細 URL] から Dinの Scontroller クラスの編集および削除アクションメソッドにリンクしています。</span><span class="sxs-lookup"><span data-stu-id="554fb-186">We are linking to the Edit and Delete action method of our DinnersController class from our Details URL:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image8.png)

<span data-ttu-id="554fb-187">現時点では、詳細 URL の訪問者がディナーのホストであるかどうかに関係なく、[編集] および [削除] アクションリンクが表示されています。</span><span class="sxs-lookup"><span data-stu-id="554fb-187">Currently we are showing the Edit and Delete action links regardless of whether the visitor to the details URL is the host of the dinner.</span></span> <span data-ttu-id="554fb-188">これを変更して、訪問しているユーザーがディナーの所有者である場合にのみリンクが表示されるようにしましょう。</span><span class="sxs-lookup"><span data-stu-id="554fb-188">Let's change this so that the links are only displayed if the visiting user is the owner of the dinner.</span></span>

<span data-ttu-id="554fb-189">Dinでの Details () アクションメソッドは、ディナーオブジェクトを取得し、それをモデルオブジェクトとしてビューテンプレートに渡します。</span><span class="sxs-lookup"><span data-stu-id="554fb-189">The Details() action method within our DinnersController retrieves a Dinner object and then passes it as the model object to our view template:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample8.cs)]

<span data-ttu-id="554fb-190">次のような IsHostedBy () ヘルパーメソッドを使用して、ビューテンプレートを更新して、条件に応じて編集と削除のリンクを表示/非表示にすることができます。</span><span class="sxs-lookup"><span data-stu-id="554fb-190">We can update our view template to conditionally show/hide the Edit and Delete links by using the Dinner.IsHostedBy() helper method like below:</span></span>

[!code-aspx[Main](secure-applications-using-authentication-and-authorization/samples/sample9.aspx)]

#### <a name="next-steps"></a><span data-ttu-id="554fb-191">次の手順</span><span class="sxs-lookup"><span data-stu-id="554fb-191">Next Steps</span></span>

<span data-ttu-id="554fb-192">ここで、AJAX を使用して、認証されたユーザーをディナーの RSVP に対して有効にする方法を見てみましょう。</span><span class="sxs-lookup"><span data-stu-id="554fb-192">Let's now look at how we can enable authenticated users to RSVP for dinners using AJAX.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="554fb-193">[前へ](implement-efficient-data-paging.md)
> [次へ](use-ajax-to-deliver-dynamic-updates.md)</span><span class="sxs-lookup"><span data-stu-id="554fb-193">[Previous](implement-efficient-data-paging.md)
[Next](use-ajax-to-deliver-dynamic-updates.md)</span></span>
