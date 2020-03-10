---
uid: web-api/overview/security/external-authentication-services
title: ASP.NET Web API (C#) を使用した外部認証サービスMicrosoft Docs
author: rmcmurray
description: ASP.NET Web API での外部認証サービスの使用について説明します。
ms.author: riande
ms.date: 01/28/2019
ms.assetid: 3bb8eb15-b518-44f5-a67d-a27e051aedc6
msc.legacyurl: /web-api/overview/security/external-authentication-services
msc.type: authoredcontent
ms.openlocfilehash: b2571552a3f8040ff42bfa0a9fa48981f71a1e4b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78447418"
---
# <a name="external-authentication-services-with-aspnet-web-api-c"></a><span data-ttu-id="1259b-103">ASP.NET Web API (C#) を使用した外部認証サービス</span><span class="sxs-lookup"><span data-stu-id="1259b-103">External Authentication Services with ASP.NET Web API (C#)</span></span>

<span data-ttu-id="1259b-104">Visual Studio 2017 と ASP.NET 4.7.2 は、[シングルページアプリケーション](../../../single-page-application/index.md)(SPA) と[Web API](../../index.md)サービスのセキュリティオプションを拡張して、複数の OAuth/OpenID およびソーシャルメディア認証サービス (Microsoft アカウント、Twitter、Facebook、Google) を含む外部認証サービスと統合します。</span><span class="sxs-lookup"><span data-stu-id="1259b-104">Visual Studio 2017 and ASP.NET 4.7.2 expand the security options for [Single Page Applications](../../../single-page-application/index.md) (SPA) and [Web API](../../index.md) services to integrate with external authentication services, which include several OAuth/OpenID and social media authentication services: Microsoft Accounts, Twitter, Facebook, and Google.</span></span>  

### <a name="in-this-walkthrough"></a><span data-ttu-id="1259b-105">このチュートリアルの手順</span><span class="sxs-lookup"><span data-stu-id="1259b-105">In this Walkthrough</span></span>

- [<span data-ttu-id="1259b-106">外部認証サービスの使用</span><span class="sxs-lookup"><span data-stu-id="1259b-106">Using External Authentication Services</span></span>](#USING)
- [<span data-ttu-id="1259b-107">サンプル Web アプリケーションの作成</span><span class="sxs-lookup"><span data-stu-id="1259b-107">Creating the Sample Web Application</span></span>](#SAMPLE)
- [<span data-ttu-id="1259b-108">Facebook 認証を有効にする</span><span class="sxs-lookup"><span data-stu-id="1259b-108">Enabling Facebook Authentication</span></span>](#FACEBOOK)
- [<span data-ttu-id="1259b-109">Google 認証を有効にする</span><span class="sxs-lookup"><span data-stu-id="1259b-109">Enabling Google Authentication</span></span>](#GOOGLE)
- [<span data-ttu-id="1259b-110">Microsoft 認証を有効にする</span><span class="sxs-lookup"><span data-stu-id="1259b-110">Enabling Microsoft Authentication</span></span>](#MICROSOFT)
- [<span data-ttu-id="1259b-111">Twitter 認証を有効にする</span><span class="sxs-lookup"><span data-stu-id="1259b-111">Enabling Twitter Authentication</span></span>](#TWITTER)
- [<span data-ttu-id="1259b-112">追加情報</span><span class="sxs-lookup"><span data-stu-id="1259b-112">Additional Information</span></span>](#MOREINFO)

    - [<span data-ttu-id="1259b-113">外部認証サービスの組み合わせ</span><span class="sxs-lookup"><span data-stu-id="1259b-113">Combining External Authentication Services</span></span>](#COMBINE)
    - [<span data-ttu-id="1259b-114">完全修飾ドメイン名を使用するように IIS Express を構成する</span><span class="sxs-lookup"><span data-stu-id="1259b-114">Configuring IIS Express to use a Fully Qualified Domain Name</span></span>](#FQDN)
    - [<span data-ttu-id="1259b-115">Microsoft 認証のアプリケーション設定を取得する方法</span><span class="sxs-lookup"><span data-stu-id="1259b-115">How to Obtain your Application Settings for Microsoft Authentication</span></span>](#OBTAIN)
    - [<span data-ttu-id="1259b-116">省略可能: ローカル登録を無効にする</span><span class="sxs-lookup"><span data-stu-id="1259b-116">Optional: Disable Local Registration</span></span>](#DISABLE)

### <a name="prerequisites"></a><span data-ttu-id="1259b-117">前提条件</span><span class="sxs-lookup"><span data-stu-id="1259b-117">Prerequisites</span></span>

<span data-ttu-id="1259b-118">このチュートリアルの例を実行するには、次のものが必要です。</span><span class="sxs-lookup"><span data-stu-id="1259b-118">To follow the examples in this walkthrough, you need to have the following:</span></span>

- <span data-ttu-id="1259b-119">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="1259b-119">Visual Studio 2017</span></span>
- <span data-ttu-id="1259b-120">次のいずれかのソーシャルメディア認証サービスのアプリケーション id とシークレットキーを持つ開発者アカウント:</span><span class="sxs-lookup"><span data-stu-id="1259b-120">A developer account with the application identifier and secret key for one of the following social media authentication services:</span></span>

  - <span data-ttu-id="1259b-121">Microsoft アカウント ([https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070))</span><span class="sxs-lookup"><span data-stu-id="1259b-121">Microsoft Accounts ([https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070))</span></span>
  - <span data-ttu-id="1259b-122">Twitter ([https://dev.twitter.com/](https://dev.twitter.com/))</span><span class="sxs-lookup"><span data-stu-id="1259b-122">Twitter ([https://dev.twitter.com/](https://dev.twitter.com/))</span></span>
  - <span data-ttu-id="1259b-123">Facebook ([https://developers.facebook.com/](https://developers.facebook.com/))</span><span class="sxs-lookup"><span data-stu-id="1259b-123">Facebook ([https://developers.facebook.com/](https://developers.facebook.com/))</span></span>
  - <span data-ttu-id="1259b-124">Google ([https://developers.google.com/](https://developers.google.com))</span><span class="sxs-lookup"><span data-stu-id="1259b-124">Google ([https://developers.google.com/](https://developers.google.com))</span></span>

<a id="USING"></a>
## <a name="using-external-authentication-services"></a><span data-ttu-id="1259b-125">外部認証サービスの使用</span><span class="sxs-lookup"><span data-stu-id="1259b-125">Using External Authentication Services</span></span>

<span data-ttu-id="1259b-126">Web 開発者が現在使用できる多数の外部認証サービスは、新しい web アプリケーションを作成するときの開発時間を短縮するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="1259b-126">The abundance of external authentication services that are currently available to web developers help to reduce development time when creating new web applications.</span></span> <span data-ttu-id="1259b-127">Web ユーザーは一般的に、一般的な web サービスとソーシャルメディア web サイト用にいくつかの既存のアカウントを持っています。そのため、web アプリケーションが外部 web サービスまたはソーシャルメディア web サイトから認証サービスを実装すると、開発時間が短縮されます。では、認証実装の作成に費やしました。</span><span class="sxs-lookup"><span data-stu-id="1259b-127">Web users typically have several existing accounts for popular web services and social media websites, therefore when a web application implements the authentication services from an external web service or social media website, it saves the development time that would have been spent creating an authentication implementation.</span></span> <span data-ttu-id="1259b-128">外部認証サービスを使用すると、エンドユーザーは web アプリケーション用に別のアカウントを作成する必要がなくなります。また、別のユーザー名とパスワードを覚えておく必要もありません。</span><span class="sxs-lookup"><span data-stu-id="1259b-128">Using an external authentication service saves end users from having to create another account for your web application, and also from having to remember another username and password.</span></span>

<span data-ttu-id="1259b-129">これまで、開発者には、独自の認証実装を作成する方法と、外部認証サービスをアプリケーションに統合する方法についての2つの選択肢がありました。</span><span class="sxs-lookup"><span data-stu-id="1259b-129">In the past, developers have had two choices: create their own authentication implementation, or learn how to integrate an external authentication service into their applications.</span></span> <span data-ttu-id="1259b-130">最も基本的なレベルでは、次の図は、外部認証サービスを使用するように構成された web アプリケーションの情報を要求しているユーザーエージェント (web ブラウザー) の単純な要求フローを示しています。</span><span class="sxs-lookup"><span data-stu-id="1259b-130">At the most basic level, the following diagram illustrates a simple request flow for a user agent (web browser) that is requesting information from a web application that is configured to use an external authentication service:</span></span>

[![](external-authentication-services/_static/image2.png "Click to Expand the Image")](external-authentication-services/_static/image1.png)

<span data-ttu-id="1259b-131">上の図では、ユーザーエージェント (この例では web ブラウザー) が web アプリケーションに要求を行い、web ブラウザーが外部認証サービスにリダイレクトされます。</span><span class="sxs-lookup"><span data-stu-id="1259b-131">In the preceding diagram, the user agent (or web browser in this example) makes a request to a web application, which redirects the web browser to an external authentication service.</span></span> <span data-ttu-id="1259b-132">ユーザーエージェントが外部認証サービスに資格情報を送信すると、ユーザーエージェントが正常に認証されると、外部認証サービスによってユーザーエージェントが元の web アプリケーションにリダイレクトされ、ユーザーエージェントが web アプリケーションに送信します。</span><span class="sxs-lookup"><span data-stu-id="1259b-132">The user agent sends its credentials to the external authentication service, and if the user agent has successfully authenticated, the external authentication service will redirect the user agent to the original web application with some form of token which the user agent will send to the web application.</span></span> <span data-ttu-id="1259b-133">Web アプリケーションは、トークンを使用して、ユーザーエージェントが外部認証サービスによって正常に認証されたことを確認します。また、web アプリケーションは、トークンを使用して、ユーザーエージェントに関する詳細情報を収集できます。</span><span class="sxs-lookup"><span data-stu-id="1259b-133">The web application will use the token to verify that the user agent has been successfully authenticated by the external authentication service, and the web application may use the token to gather more information about the user agent.</span></span> <span data-ttu-id="1259b-134">アプリケーションがユーザーエージェントの情報の処理を完了すると、web アプリケーションは、承認設定に基づいて、ユーザーエージェントに適切な応答を返します。</span><span class="sxs-lookup"><span data-stu-id="1259b-134">Once the application is done processing the user agent's information, the web application will return the appropriate response to the user agent based on its authorization settings.</span></span>

<span data-ttu-id="1259b-135">この2番目の例では、ユーザーエージェントが web アプリケーションと外部承認サーバーとネゴシエートし、web アプリケーションが外部承認サーバーとの追加の通信を実行して、ユーザーに関する追加情報を取得します。・</span><span class="sxs-lookup"><span data-stu-id="1259b-135">In this second example, the user agent negotiates with the web application and external authorization server, and the web application performs additional communication with the external authorization server to retrieve additional information about the user agent:</span></span>

[![](external-authentication-services/_static/image4.png "Click to Expand the Image")](external-authentication-services/_static/image3.png)

<span data-ttu-id="1259b-136">Visual Studio 2017 と ASP.NET 4.7.2 は、次の認証サービスの組み込み統合機能を提供することで、開発者にとって外部認証サービスとの統合を容易にします。</span><span class="sxs-lookup"><span data-stu-id="1259b-136">Visual Studio 2017 and ASP.NET 4.7.2 make integration with external authentication services easier for developers by providing built-in integration for the following authentication services:</span></span>

- <span data-ttu-id="1259b-137">Facebook</span><span class="sxs-lookup"><span data-stu-id="1259b-137">Facebook</span></span>
- <span data-ttu-id="1259b-138">Google</span><span class="sxs-lookup"><span data-stu-id="1259b-138">Google</span></span>
- <span data-ttu-id="1259b-139">Microsoft アカウント (Windows Live ID アカウント)</span><span class="sxs-lookup"><span data-stu-id="1259b-139">Microsoft Accounts (Windows Live ID accounts)</span></span>
- <span data-ttu-id="1259b-140">Twitter</span><span class="sxs-lookup"><span data-stu-id="1259b-140">Twitter</span></span>

<span data-ttu-id="1259b-141">このチュートリアルの例では、Visual Studio 2017 に付属している new ASP.NET Web アプリケーションテンプレートを使用して、サポートされている各外部認証サービスを構成する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="1259b-141">The examples in this walkthrough will demonstrate how to configure each of the supported external authentication services by using the new ASP.NET Web Application template that ships with Visual Studio 2017.</span></span>

> [!NOTE]
> <span data-ttu-id="1259b-142">必要に応じて、外部認証サービスの設定に FQDN を追加することが必要になる場合があります。</span><span class="sxs-lookup"><span data-stu-id="1259b-142">If necessary, you may need to add your FQDN to the settings for your external authentication service.</span></span> <span data-ttu-id="1259b-143">この要件は、アプリケーション設定の FQDN がクライアントによって使用される FQDN と一致する必要がある一部の外部認証サービスのセキュリティ制約に基づいています。</span><span class="sxs-lookup"><span data-stu-id="1259b-143">This requirement is based on security constraints for some external authentication services which require the FQDN in your application settings to match the FQDN that is used by your clients.</span></span> <span data-ttu-id="1259b-144">(この手順は、外部認証サービスごとに大きく異なります。各外部認証サービスのドキュメントを参照して、必要かどうか、およびこれらの設定を構成する方法を確認する必要があります)。この環境をテストするために FQDN を使用するように IIS Express を構成する必要がある場合は、このチュートリアルで後述[する「完全修飾ドメイン名を使用するための IIS Express の構成](#FQDN)」セクションを参照してください。</span><span class="sxs-lookup"><span data-stu-id="1259b-144">(The steps for this will vary greatly for each external authentication service; you will need to consult the documentation for each external authentication service to see if this is required and how to configure these settings.) If you need to configure IIS Express to use an FQDN for testing this environment, see the [Configuring IIS Express to use a Fully Qualified Domain Name](#FQDN) section later in this walkthrough.</span></span>

<a id="SAMPLE"></a>
## <a name="create-a-sample-web-application"></a><span data-ttu-id="1259b-145">サンプル Web アプリケーションを作成する</span><span class="sxs-lookup"><span data-stu-id="1259b-145">Create a Sample Web Application</span></span>

<span data-ttu-id="1259b-146">次の手順では、ASP.NET Web アプリケーションテンプレートを使用してサンプルアプリケーションを作成します。このサンプルアプリケーションは、このチュートリアルで後述する外部認証サービスのそれぞれに使用します。</span><span class="sxs-lookup"><span data-stu-id="1259b-146">The following steps will lead you through creating a sample application by using the ASP.NET Web Application template, and you will use this sample application for each of the external authentication services later in this walkthrough.</span></span>

<span data-ttu-id="1259b-147">Visual Studio 2017 を起動し、スタートページで **[新しいプロジェクト]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="1259b-147">Start Visual Studio 2017 and select **New Project** from the Start page.</span></span> <span data-ttu-id="1259b-148">または、 **[ファイル]** メニューの **[新規作成]** をポイントし、 **[プロジェクト]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="1259b-148">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<!-- [![](external-authentication-services/_static/image6.png "Click to Expand the Image")](external-authentication-services/_static/image5.png) -->

<span data-ttu-id="1259b-149">**[新しいプロジェクト]** ダイアログボックスが表示されたら、 **[インストール済み]** を選択し、 **[ C#ビジュアル]** を展開します。</span><span class="sxs-lookup"><span data-stu-id="1259b-149">When the **New Project** dialog box is displayed, select **Installed** and expand **Visual C#**.</span></span> <span data-ttu-id="1259b-150">**[ビジュアルC# ]** で **[Web]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="1259b-150">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="1259b-151">プロジェクトテンプレートの一覧で、 **[ASP.NET Web Application (.Net Framework)]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="1259b-151">In the list of project templates, select **ASP.NET Web Application (.Net Framework)**.</span></span> <span data-ttu-id="1259b-152">プロジェクトの名前を入力し、[ **OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="1259b-152">Enter a name for your project and click **OK**.</span></span>

[![](external-authentication-services/_static/image71.png "Click to Expand the Image")](external-authentication-services/_static/image71.png)

<span data-ttu-id="1259b-153">**新しい ASP.NET プロジェクト**が表示されたら、 **[シングルページアプリケーション]** テンプレートを選択し、 **[プロジェクトの作成]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="1259b-153">When the **New ASP.NET Project** is displayed, select the **Single Page Application** template and click **Create Project**.</span></span>

[![](external-authentication-services/_static/image72.png "Click to Expand the Image")](external-authentication-services/_static/image72.png)

<span data-ttu-id="1259b-154">Visual Studio 2017 によってプロジェクトが作成されるまで待ちます。</span><span class="sxs-lookup"><span data-stu-id="1259b-154">Wait as Visual Studio 2017 creates your project.</span></span>

<!-- [![](external-authentication-services/_static/image12.png "Click to Expand the Image")](external-authentication-services/_static/image11.png) -->

<span data-ttu-id="1259b-155">Visual Studio 2017 がプロジェクトの作成を完了したら、**アプリ\_** の [開始] フォルダーにある*Startup.Auth.cs*ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="1259b-155">When Visual Studio 2017 has finished creating your project, open the *Startup.Auth.cs* file that is located in the **App\_Start** folder.</span></span>

<span data-ttu-id="1259b-156">最初にプロジェクトを作成するときに、 *Startup.Auth.cs*ファイルで外部認証サービスが有効になっていません。次に、コードがどのようなものかを示します。ここでは、ASP.NET アプリケーションで Microsoft アカウント、Twitter、Facebook、または Google 認証を使用するために、外部認証サービスと関連する設定を有効にする場所のセクションを強調表示しています。</span><span class="sxs-lookup"><span data-stu-id="1259b-156">When you first create the project, none of the external authentication services are enabled in *Startup.Auth.cs* file; the following illustrates what your code might resemble, with the sections highlighted for where you would enable an external authentication service and any relevant settings in order to use Microsoft Accounts, Twitter, Facebook, or Google authentication with your ASP.NET application:</span></span>

[!code-csharp[Main](external-authentication-services/samples/sample1.cs)]

<span data-ttu-id="1259b-157">F5 キーを押して web アプリケーションをビルドおよびデバッグすると、ログイン画面が表示され、外部認証サービスが定義されていないことがわかります。</span><span class="sxs-lookup"><span data-stu-id="1259b-157">When you press F5 to build and debug your web application, it will display a login screen where you will see that no external authentication services have been defined.</span></span>

[![](external-authentication-services/_static/image73.png "Click to Expand the Image")](external-authentication-services/_static/image73.png)

<span data-ttu-id="1259b-158">以下のセクションでは、Visual Studio 2017 の ASP.NET で提供されている各外部認証サービスを有効にする方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="1259b-158">In the following sections, you will learn how to enable each of the external authentication services that are provided with ASP.NET in Visual Studio 2017.</span></span>

<a id="FACEBOOK"></a>
## <a name="enabling-facebook-authentication"></a><span data-ttu-id="1259b-159">Facebook 認証を有効にする</span><span class="sxs-lookup"><span data-stu-id="1259b-159">Enabling Facebook authentication</span></span>

<span data-ttu-id="1259b-160">Facebook 認証を使用するには、Facebook 開発者アカウントを作成する必要があります。また、プロジェクトで機能するためには、Facebook のアプリケーション ID とシークレットキーが必要です。</span><span class="sxs-lookup"><span data-stu-id="1259b-160">Using Facebook authentication requires you to create a Facebook developer account, and your project will require an application ID and secret key from Facebook in order to function.</span></span> <span data-ttu-id="1259b-161">Facebook 開発者アカウントを作成し、アプリケーション ID とシークレットキーを取得する方法の詳細については、「 [https://go.microsoft.com/fwlink/?LinkID=252166](https://go.microsoft.com/fwlink/?LinkID=252166)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="1259b-161">For information about creating a Facebook developer account and obtaining your application ID and secret key, see [https://go.microsoft.com/fwlink/?LinkID=252166](https://go.microsoft.com/fwlink/?LinkID=252166).</span></span>

<span data-ttu-id="1259b-162">アプリケーション ID とシークレットキーを取得したら、次の手順に従って、web アプリケーションの Facebook 認証を有効にします。</span><span class="sxs-lookup"><span data-stu-id="1259b-162">Once you have obtained your application ID and secret key, use the following steps to enable Facebook authentication for your web application:</span></span>

1. <span data-ttu-id="1259b-163">プロジェクトが Visual Studio 2017 で開かれている場合は、 *Startup.Auth.cs*ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="1259b-163">When your project is open in Visual Studio 2017, open the *Startup.Auth.cs* file.</span></span>

2. <span data-ttu-id="1259b-164">コードの [Facebook 認証] セクションを探します。</span><span class="sxs-lookup"><span data-stu-id="1259b-164">Locate the Facebook authentication section of code:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample2.cs)]
3. <span data-ttu-id="1259b-165">強調表示されているコード行のコメントを解除し、アプリケーション ID とシークレットキーを追加するには、&quot;//&quot; 文字を削除します。</span><span class="sxs-lookup"><span data-stu-id="1259b-165">Remove the &quot;//&quot; characters to uncomment the highlighted lines of code, and then add your application ID and secret key.</span></span> <span data-ttu-id="1259b-166">これらのパラメーターを追加したら、プロジェクトを再コンパイルできます。</span><span class="sxs-lookup"><span data-stu-id="1259b-166">Once you have added those parameters, you can recompile your project:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample3.cs)]
4. <span data-ttu-id="1259b-167">F5 キーを押して web ブラウザーで web アプリケーションを開くと、Facebook が外部認証サービスとして定義されていることがわかります。</span><span class="sxs-lookup"><span data-stu-id="1259b-167">When you press F5 to open your web application in your web browser, you will see that Facebook has been defined as an external authentication service:</span></span>

    [![](external-authentication-services/_static/image74.png "Click to Expand the Image")](external-authentication-services/_static/image74.png)
5. <span data-ttu-id="1259b-168">**Facebook**のボタンをクリックすると、ブラウザーが facebook のログインページにリダイレクトされます。</span><span class="sxs-lookup"><span data-stu-id="1259b-168">When you click the **Facebook** button, your browser will be redirected to the Facebook login page:</span></span>

    [![](external-authentication-services/_static/image22.png "Click to Expand the Image")](external-authentication-services/_static/image21.png)
6. <span data-ttu-id="1259b-169">Facebook の資格情報を入力して **[ログイン]** をクリックすると、web ブラウザーが web アプリケーションにリダイレクトされます。これにより、facebook アカウントに関連付ける**ユーザー名**の入力が求められます。</span><span class="sxs-lookup"><span data-stu-id="1259b-169">After you enter your Facebook credentials and click **Log in**, your web browser will be redirected back to your web application, which will prompt you for the **User name** that you want to associate with your Facebook account:</span></span>

    [![](external-authentication-services/_static/image24.png "Click to Expand the Image")](external-authentication-services/_static/image23.png)
7. <span data-ttu-id="1259b-170">ユーザー名を入力して **[サインアップ]** ボタンをクリックすると、web アプリケーションに Facebook アカウントの既定の**ホームページ**が表示されます。</span><span class="sxs-lookup"><span data-stu-id="1259b-170">After you have entered your user name and clicked the **Sign up** button, your web application will display the default **home page** for your Facebook account:</span></span>

    [![](external-authentication-services/_static/image26.png "Click to Expand the Image")](external-authentication-services/_static/image25.png)

<a id="GOOGLE"></a>
## <a name="enabling-google-authentication"></a><span data-ttu-id="1259b-171">Google 認証を有効にする</span><span class="sxs-lookup"><span data-stu-id="1259b-171">Enabling Google Authentication</span></span>

<span data-ttu-id="1259b-172">Google 認証を使用するには、Google developer アカウントを作成する必要があります。また、プロジェクトで機能するためには、Google のアプリケーション ID とシークレットキーが必要です。</span><span class="sxs-lookup"><span data-stu-id="1259b-172">Using Google authentication requires you to create a Google developer account, and your project will require an application ID and secret key from Google in order to function.</span></span> <span data-ttu-id="1259b-173">Google developer アカウントを作成し、アプリケーション ID とシークレットキーを取得する方法の詳細については、「 [https://developers.google.com](https://developers.google.com)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="1259b-173">For information about creating a Google developer account and obtaining your application ID and secret key, see [https://developers.google.com](https://developers.google.com).</span></span>

<span data-ttu-id="1259b-174">Web アプリケーションの Google 認証を有効にするには、次の手順に従います。</span><span class="sxs-lookup"><span data-stu-id="1259b-174">To enable Google authentication for your web application, use the following steps:</span></span>

1. <span data-ttu-id="1259b-175">プロジェクトが Visual Studio 2017 で開かれている場合は、 *Startup.Auth.cs*ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="1259b-175">When your project is open in Visual Studio 2017, open the *Startup.Auth.cs* file.</span></span>

2. <span data-ttu-id="1259b-176">コードの [Google authentication] セクションを探します。</span><span class="sxs-lookup"><span data-stu-id="1259b-176">Locate the Google authentication section of code:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample4.cs)]
3. <span data-ttu-id="1259b-177">強調表示されているコード行のコメントを解除し、アプリケーション ID とシークレットキーを追加するには、&quot;//&quot; 文字を削除します。</span><span class="sxs-lookup"><span data-stu-id="1259b-177">Remove the &quot;//&quot; characters to uncomment the highlighted lines of code, and then add your application ID and secret key.</span></span> <span data-ttu-id="1259b-178">これらのパラメーターを追加したら、プロジェクトを再コンパイルできます。</span><span class="sxs-lookup"><span data-stu-id="1259b-178">Once you have added those parameters, you can recompile your project:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample5.cs)]
4. <span data-ttu-id="1259b-179">F5 キーを押して web ブラウザーで web アプリケーションを開くと、Google が外部認証サービスとして定義されていることがわかります。</span><span class="sxs-lookup"><span data-stu-id="1259b-179">When you press F5 to open your web application in your web browser, you will see that Google has been defined as an external authentication service:</span></span>

    [![](external-authentication-services/_static/image75.png "Click to Expand the Image")](external-authentication-services/_static/image75.png)
5. <span data-ttu-id="1259b-180">**Google**ボタンをクリックすると、ブラウザーは google ログインページにリダイレクトされます。</span><span class="sxs-lookup"><span data-stu-id="1259b-180">When you click the **Google** button, your browser will be redirected to the Google login page:</span></span>

    [![](external-authentication-services/_static/image32.png "Click to Expand the Image")](external-authentication-services/_static/image31.png)
6. <span data-ttu-id="1259b-181">Google の資格情報を入力して **[サインイン]** をクリックすると、google アカウントにアクセスするためのアクセス許可が web アプリケーションにあるかどうかを確認するメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="1259b-181">After you enter your Google credentials and click **Sign in**, Google will prompt you to verify that your web application has permissions to access your Google account:</span></span>

    [![](external-authentication-services/_static/image34.png "Click to Expand the Image")](external-authentication-services/_static/image33.png)
7. <span data-ttu-id="1259b-182">[**同意**する] をクリックすると、web ブラウザーが web アプリケーションにリダイレクトされます。これにより、Google アカウントに関連付ける**ユーザー名**の入力が求められます。</span><span class="sxs-lookup"><span data-stu-id="1259b-182">When you click **Accept**, your web browser will be redirected back to your web application, which will prompt you for the **User name** that you want to associate with your Google account:</span></span>

    [![](external-authentication-services/_static/image36.png "Click to Expand the Image")](external-authentication-services/_static/image35.png)
8. <span data-ttu-id="1259b-183">ユーザー名を入力して **[サインアップ]** ボタンをクリックすると、web アプリケーションに Google アカウントの既定の**ホームページ**が表示されます。</span><span class="sxs-lookup"><span data-stu-id="1259b-183">After you have entered your user name and clicked the **Sign up** button, your web application will display the default **home page** for your Google account:</span></span>

    [![](external-authentication-services/_static/image38.png "Click to Expand the Image")](external-authentication-services/_static/image37.png)

<a id="MICROSOFT"></a>
## <a name="enabling-microsoft-authentication"></a><span data-ttu-id="1259b-184">Microsoft 認証を有効にする</span><span class="sxs-lookup"><span data-stu-id="1259b-184">Enabling Microsoft Authentication</span></span>

<span data-ttu-id="1259b-185">Microsoft 認証では、開発者アカウントを作成する必要があり、機能するためにはクライアント ID とクライアントシークレットが必要です。</span><span class="sxs-lookup"><span data-stu-id="1259b-185">Microsoft authentication requires you to create a developer account, and it requires a client ID and client secret in order to function.</span></span> <span data-ttu-id="1259b-186">Microsoft 開発者アカウントを作成し、クライアント ID とクライアントシークレットを取得する方法の詳細については、「 [https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="1259b-186">For information about creating a Microsoft developer account and obtaining your client ID and client secret, see [https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070).</span></span>

<span data-ttu-id="1259b-187">コンシューマーキーとコンシューマーシークレットを取得したら、次の手順に従って、web アプリケーションの Microsoft 認証を有効にします。</span><span class="sxs-lookup"><span data-stu-id="1259b-187">Once you have obtained your consumer key and consumer secret, use the following steps to enable Microsoft authentication for your web application:</span></span>

1. <span data-ttu-id="1259b-188">プロジェクトが Visual Studio 2017 で開かれている場合は、 *Startup.Auth.cs*ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="1259b-188">When your project is open in Visual Studio 2017, open the *Startup.Auth.cs* file.</span></span>

2. <span data-ttu-id="1259b-189">コードの [Microsoft 認証] セクションを探します。</span><span class="sxs-lookup"><span data-stu-id="1259b-189">Locate the Microsoft authentication section of code:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample6.cs)]
3. <span data-ttu-id="1259b-190">強調表示されているコード行のコメントを解除し、クライアント ID とクライアントシークレットを追加するには、&quot;//&quot; 文字を削除します。</span><span class="sxs-lookup"><span data-stu-id="1259b-190">Remove the &quot;//&quot; characters to uncomment the highlighted lines of code, and then add your client ID and client secret.</span></span> <span data-ttu-id="1259b-191">これらのパラメーターを追加したら、プロジェクトを再コンパイルできます。</span><span class="sxs-lookup"><span data-stu-id="1259b-191">Once you have added those parameters, you can recompile your project:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample7.cs)]
4. <span data-ttu-id="1259b-192">F5 キーを押して web ブラウザーで web アプリケーションを開くと、Microsoft が外部認証サービスとして定義されていることがわかります。</span><span class="sxs-lookup"><span data-stu-id="1259b-192">When you press F5 to open your web application in your web browser, you will see that Microsoft has been defined as an external authentication service:</span></span>

    [![](external-authentication-services/_static/image42.png "Click to Expand the Image")](external-authentication-services/_static/image41.png)
5. <span data-ttu-id="1259b-193">**[Microsoft]** ボタンをクリックすると、ブラウザーが microsoft ログインページにリダイレクトされます。</span><span class="sxs-lookup"><span data-stu-id="1259b-193">When you click the **Microsoft** button, your browser will be redirected to the Microsoft login page:</span></span>

    [![](external-authentication-services/_static/image44.png "Click to Expand the Image")](external-authentication-services/_static/image43.png)
6. <span data-ttu-id="1259b-194">Microsoft の資格情報を入力して **[サインイン]** をクリックすると、web アプリケーションに Microsoft アカウントにアクセスするためのアクセス許可があるかどうかを確認するメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="1259b-194">After you enter your Microsoft credentials and click **Sign in**, you will be prompted to verify that your web application has permissions to access your Microsoft account:</span></span>

    [![](external-authentication-services/_static/image46.png "Click to Expand the Image")](external-authentication-services/_static/image45.png)
7. <span data-ttu-id="1259b-195">**[はい]** をクリックすると、web ブラウザーが web アプリケーションにリダイレクトされ、Microsoft アカウントに関連付ける**ユーザー名**の入力が求められます。</span><span class="sxs-lookup"><span data-stu-id="1259b-195">When you click **Yes**, your web browser will be redirected back to your web application, which will prompt you for the **User name** that you want to associate with your Microsoft account:</span></span>

    [![](external-authentication-services/_static/image48.png "Click to Expand the Image")](external-authentication-services/_static/image47.png)
8. <span data-ttu-id="1259b-196">ユーザー名を入力して **[サインアップ]** ボタンをクリックすると、web アプリケーションに Microsoft アカウントの既定の**ホームページ**が表示されます。</span><span class="sxs-lookup"><span data-stu-id="1259b-196">After you have entered your user name and clicked the **Sign up** button, your web application will display the default **home page** for your Microsoft account:</span></span>

    [![](external-authentication-services/_static/image50.png "Click to Expand the Image")](external-authentication-services/_static/image49.png)

<a id="TWITTER"></a>
## <a name="enabling-twitter-authentication"></a><span data-ttu-id="1259b-197">Twitter 認証を有効にする</span><span class="sxs-lookup"><span data-stu-id="1259b-197">Enabling Twitter Authentication</span></span>

<span data-ttu-id="1259b-198">Twitter 認証では、開発者アカウントを作成する必要があり、機能するためにコンシューマーキーとコンシューマーシークレットが必要です。</span><span class="sxs-lookup"><span data-stu-id="1259b-198">Twitter authentication requires you to create a developer account, and it requires a consumer key and consumer secret in order to function.</span></span> <span data-ttu-id="1259b-199">Twitter 開発者アカウントを作成し、コンシューマーキーとコンシューマーシークレットを取得する方法の詳細については、「 [https://go.microsoft.com/fwlink/?LinkID=252166](https://go.microsoft.com/fwlink/?LinkID=252166)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="1259b-199">For information about creating a Twitter developer account and obtaining your consumer key and consumer secret, see [https://go.microsoft.com/fwlink/?LinkID=252166](https://go.microsoft.com/fwlink/?LinkID=252166).</span></span>

<span data-ttu-id="1259b-200">コンシューマーキーとコンシューマーシークレットを取得したら、次の手順に従って、web アプリケーションの Twitter 認証を有効にします。</span><span class="sxs-lookup"><span data-stu-id="1259b-200">Once you have obtained your consumer key and consumer secret, use the following steps to enable Twitter authentication for your web application:</span></span>

1. <span data-ttu-id="1259b-201">プロジェクトが Visual Studio 2017 で開かれている場合は、 *Startup.Auth.cs*ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="1259b-201">When your project is open in Visual Studio 2017, open the *Startup.Auth.cs* file.</span></span>

2. <span data-ttu-id="1259b-202">コードの [Twitter 認証] セクションを探します。</span><span class="sxs-lookup"><span data-stu-id="1259b-202">Locate the Twitter authentication section of code:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample8.cs)]
3. <span data-ttu-id="1259b-203">強調表示されているコード行のコメントを解除し、コンシューマーキーとコンシューマーシークレットを追加するには、&quot;//&quot; 文字を削除します。</span><span class="sxs-lookup"><span data-stu-id="1259b-203">Remove the &quot;//&quot; characters to uncomment the highlighted lines of code, and then add your consumer key and consumer secret.</span></span> <span data-ttu-id="1259b-204">これらのパラメーターを追加したら、プロジェクトを再コンパイルできます。</span><span class="sxs-lookup"><span data-stu-id="1259b-204">Once you have added those parameters, you can recompile your project:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample9.cs)]
4. <span data-ttu-id="1259b-205">F5 キーを押して web ブラウザーで web アプリケーションを開くと、Twitter が外部認証サービスとして定義されていることがわかります。</span><span class="sxs-lookup"><span data-stu-id="1259b-205">When you press F5 to open your web application in your web browser, you will see that Twitter has been defined as an external authentication service:</span></span>

    [![](external-authentication-services/_static/image54.png "Click to Expand the Image")](external-authentication-services/_static/image53.png)
5. <span data-ttu-id="1259b-206">**Twitter**ボタンをクリックすると、ブラウザーが twitter ログインページにリダイレクトされます。</span><span class="sxs-lookup"><span data-stu-id="1259b-206">When you click the **Twitter** button, your browser will be redirected to the Twitter login page:</span></span>

    [![](external-authentication-services/_static/image56.png "Click to Expand the Image")](external-authentication-services/_static/image55.png)
6. <span data-ttu-id="1259b-207">Twitter の資格情報を入力して **[アプリの承認]** をクリックすると、web ブラウザーが web アプリケーションにリダイレクトされます。これにより、twitter アカウントに関連付ける**ユーザー名**の入力が求められます。</span><span class="sxs-lookup"><span data-stu-id="1259b-207">After you enter your Twitter credentials and click **Authorize app**, your web browser will be redirected back to your web application, which will prompt you for the **User name** that you want to associate with your Twitter account:</span></span>

    [![](external-authentication-services/_static/image58.png "Click to Expand the Image")](external-authentication-services/_static/image57.png)
7. <span data-ttu-id="1259b-208">ユーザー名を入力して **[サインアップ]** ボタンをクリックすると、web アプリケーションに Twitter アカウントの既定の**ホームページ**が表示されます。</span><span class="sxs-lookup"><span data-stu-id="1259b-208">After you have entered your user name and clicked the **Sign up** button, your web application will display the default **home page** for your Twitter account:</span></span>

    [![](external-authentication-services/_static/image60.png "Click to Expand the Image")](external-authentication-services/_static/image59.png)

<a id="MOREINFO"></a>
## <a name="additional-information"></a><span data-ttu-id="1259b-209">追加情報</span><span class="sxs-lookup"><span data-stu-id="1259b-209">Additional Information</span></span>

<span data-ttu-id="1259b-210">OAuth および OpenID を使用するアプリケーションの作成の詳細については、次の Url を参照してください。</span><span class="sxs-lookup"><span data-stu-id="1259b-210">For additional information about creating applications that use OAuth and OpenID, see the following URLs:</span></span>

- [https://go.microsoft.com/fwlink/?LinkID=252166](https://go.microsoft.com/fwlink/?LinkID=252166)
- [https://go.microsoft.com/fwlink/?LinkID=243995](https://go.microsoft.com/fwlink/?LinkID=243995)

<a id="COMBINE"></a>
### <a name="combining-external-authentication-services"></a><span data-ttu-id="1259b-211">外部認証サービスの組み合わせ</span><span class="sxs-lookup"><span data-stu-id="1259b-211">Combining External Authentication Services</span></span>

<span data-ttu-id="1259b-212">柔軟性を高めるために、複数の外部認証サービスを同時に定義することができます。これにより、web アプリケーションのユーザーは、有効な外部認証サービスのいずれかのアカウントを使用できるようになります。</span><span class="sxs-lookup"><span data-stu-id="1259b-212">For greater flexibility, you can define multiple external authentication services at the same time - this allows your web application's users to use an account from any of the enabled external authentication services:</span></span>

[![](external-authentication-services/_static/image62.png "Click to Expand the Image")](external-authentication-services/_static/image61.png)

<a id="FQDN"></a>
### <a name="configure-iis-express-to-use-a-fully-qualified-domain-name"></a><span data-ttu-id="1259b-213">完全修飾ドメイン名を使用するように IIS Express を構成する</span><span class="sxs-lookup"><span data-stu-id="1259b-213">Configure IIS Express to use a fully qualified domain name</span></span>

<span data-ttu-id="1259b-214">一部の外部認証プロバイダーでは、`http://localhost:port/`などの HTTP アドレスを使用したアプリケーションのテストはサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="1259b-214">Some external authentication providers do not support testing your application by using an HTTP address like `http://localhost:port/`.</span></span> <span data-ttu-id="1259b-215">この問題を回避するには、ホストファイルに静的完全修飾ドメイン名 (FQDN) マッピングを追加し、テスト/デバッグで FQDN を使用するように Visual Studio 2017 でプロジェクトオプションを構成します。</span><span class="sxs-lookup"><span data-stu-id="1259b-215">To work around this issue, you can add a static Fully Qualified Domain Name (FQDN) mapping to your HOSTS file and configure your project options in Visual Studio 2017 to use the FQDN for testing/debugging.</span></span> <span data-ttu-id="1259b-216">そのためには、次の手順を実行してください。</span><span class="sxs-lookup"><span data-stu-id="1259b-216">To do so, use the following steps:</span></span>

- <span data-ttu-id="1259b-217">ホストファイルをマッピングする静的 FQDN を追加します。</span><span class="sxs-lookup"><span data-stu-id="1259b-217">Add a static FQDN mapping your HOSTS file:</span></span>

  1. <span data-ttu-id="1259b-218">Windows で管理者特権でのコマンドプロンプトを開きます。</span><span class="sxs-lookup"><span data-stu-id="1259b-218">Open an elevated command prompt in Windows.</span></span>
  2. <span data-ttu-id="1259b-219">次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="1259b-219">Type the following command:</span></span>

      <span data-ttu-id="1259b-220"><kbd>メモ帳%WinDir%\system32\drivers\etc\hosts</kbd></span><span class="sxs-lookup"><span data-stu-id="1259b-220"><kbd>notepad %WinDir%\system32\drivers\etc\hosts</kbd></span></span>
  3. <span data-ttu-id="1259b-221">HOSTS ファイルに次のようなエントリを追加します。</span><span class="sxs-lookup"><span data-stu-id="1259b-221">Add an entry like the following to the HOSTS file:</span></span>

      <span data-ttu-id="1259b-222"><kbd>127.0.0.1 www.wingtiptoys.com</kbd></span><span class="sxs-lookup"><span data-stu-id="1259b-222"><kbd>127.0.0.1 www.wingtiptoys.com</kbd></span></span>
  4. <span data-ttu-id="1259b-223">ホストファイルを保存して閉じます。</span><span class="sxs-lookup"><span data-stu-id="1259b-223">Save and close your HOSTS file.</span></span>

- <span data-ttu-id="1259b-224">FQDN を使用するように Visual Studio プロジェクトを構成します。</span><span class="sxs-lookup"><span data-stu-id="1259b-224">Configure your Visual Studio project to use the FQDN:</span></span>

  1. <span data-ttu-id="1259b-225">プロジェクトが Visual Studio 2017 で開かれている場合は、 **[プロジェクト]** メニューをクリックし、プロジェクトのプロパティを選択します。</span><span class="sxs-lookup"><span data-stu-id="1259b-225">When your project is open in Visual Studio 2017, click the **Project** menu, and then select your project's properties.</span></span> <span data-ttu-id="1259b-226">たとえば、 **[WebApplication1 Properties]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="1259b-226">For example, you might select **WebApplication1 Properties**.</span></span>
  2. <span data-ttu-id="1259b-227">**[Web]** タブを選択します。</span><span class="sxs-lookup"><span data-stu-id="1259b-227">Select the **Web** tab.</span></span>
  3. <span data-ttu-id="1259b-228"><strong>プロジェクト Url</strong>の FQDN を入力します。</span><span class="sxs-lookup"><span data-stu-id="1259b-228">Enter your FQDN for the <strong>Project Url</strong>.</span></span> <span data-ttu-id="1259b-229">たとえば、ホストファイルに追加した FQDN マッピングである場合は、 <kbd><http://www.wingtiptoys.com></kbd>を入力します。</span><span class="sxs-lookup"><span data-stu-id="1259b-229">For example, you would enter <kbd><http://www.wingtiptoys.com></kbd> if that was the FQDN mapping that you added to your HOSTS file.</span></span>

- <span data-ttu-id="1259b-230">アプリケーションの FQDN を使用するように IIS Express を構成します。</span><span class="sxs-lookup"><span data-stu-id="1259b-230">Configure IIS Express to use the FQDN for your application:</span></span>

    1. <span data-ttu-id="1259b-231">Windows で管理者特権でのコマンドプロンプトを開きます。</span><span class="sxs-lookup"><span data-stu-id="1259b-231">Open an elevated command prompt in Windows.</span></span>
    2. <span data-ttu-id="1259b-232">次のコマンドを入力して、IIS Express フォルダーに移動します。</span><span class="sxs-lookup"><span data-stu-id="1259b-232">Type the following command to change to your IIS Express folder:</span></span>

        <span data-ttu-id="1259b-233"><kbd>cd/d &quot;%ProgramFiles%\IIS Express&quot;</kbd></span><span class="sxs-lookup"><span data-stu-id="1259b-233"><kbd>cd /d &quot;%ProgramFiles%\IIS Express&quot;</kbd></span></span>
    3. <span data-ttu-id="1259b-234">次のコマンドを入力して、アプリケーションに FQDN を追加します。</span><span class="sxs-lookup"><span data-stu-id="1259b-234">Type the following command to add the FQDN to your application:</span></span>

        <span data-ttu-id="1259b-235"><kbd>appcmd.exe set config-section: system.string/sites/+&quot;[name = ' WebApplication1 ']. bindings.[protocol = ' http ', bindingInformation = ' \*:80:/commit '] の&quot;: apphost</kbd></span><span class="sxs-lookup"><span data-stu-id="1259b-235"><kbd>appcmd.exe set config -section:system.applicationHost/sites /+&quot;[name='WebApplication1'].bindings.[protocol='http',bindingInformation='\*:80:www.wingtiptoys.com']&quot; /commit:apphost</kbd></span></span>

  <span data-ttu-id="1259b-236">ここで、 **WebApplication1**はプロジェクトの名前です。 **bindingInformation**には、テストに使用するポート番号と FQDN が含まれています。</span><span class="sxs-lookup"><span data-stu-id="1259b-236">Where **WebApplication1** is the name of your project and **bindingInformation** contains the port number and FQDN that you want to use for your testing.</span></span>

<a id="OBTAIN"></a>
### <a name="how-to-obtain-your-application-settings-for-microsoft-authentication"></a><span data-ttu-id="1259b-237">Microsoft 認証のアプリケーション設定を取得する方法</span><span class="sxs-lookup"><span data-stu-id="1259b-237">How to Obtain your Application Settings for Microsoft Authentication</span></span>

<span data-ttu-id="1259b-238">アプリケーションを Windows Live for Microsoft 認証にリンクすることは、簡単なプロセスです。</span><span class="sxs-lookup"><span data-stu-id="1259b-238">Linking an application to Windows Live for Microsoft Authentication is a simple process.</span></span> <span data-ttu-id="1259b-239">アプリケーションを Windows Live にまだリンクしていない場合は、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="1259b-239">If you have not already linked an application to Windows Live, you can use the following steps:</span></span>

1. <span data-ttu-id="1259b-240">[https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070)を参照し、メッセージが表示されたら、Microsoft アカウント名とパスワードを入力し、 **[サインイン]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="1259b-240">Browse to [https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070) and enter your Microsoft account name and password when prompted, then click **Sign in**:</span></span>

   <!--  [![](external-authentication-services/_static/image64.png "Click to Expand the Image")](external-authentication-services/_static/image63.png) -->
2. <span data-ttu-id="1259b-241">**[アプリの追加]** を選択し、メッセージが表示されたらアプリケーションの名前を入力して、 **[作成]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="1259b-241">Select **Add an app** and enter the name of your application when prompted, and then click **Create**:</span></span>

    [![](external-authentication-services/_static/image79.png "Click to Expand the Image")](external-authentication-services/_static/image79.png)
3. <span data-ttu-id="1259b-242">**[名前]** でアプリを選択すると、アプリケーションのプロパティページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="1259b-242">Select your app under **Name** and its application properties page appears.</span></span>

4. <span data-ttu-id="1259b-243">アプリケーションのリダイレクトドメインを入力します。</span><span class="sxs-lookup"><span data-stu-id="1259b-243">Enter the redirect domain for your application.</span></span> <span data-ttu-id="1259b-244">**アプリケーション ID**をコピーし、 **[アプリケーションシークレット]** で **[パスワードの生成]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="1259b-244">Copy the **Application ID** and, under **Application Secrets**, select **Generate Password**.</span></span> <span data-ttu-id="1259b-245">表示されたパスワードをコピーします。</span><span class="sxs-lookup"><span data-stu-id="1259b-245">Copy the password that appears.</span></span> <span data-ttu-id="1259b-246">アプリケーション ID とパスワードは、クライアント ID とクライアントシークレットです。</span><span class="sxs-lookup"><span data-stu-id="1259b-246">The application ID and password are your client ID and client secret.</span></span> <span data-ttu-id="1259b-247">[ **Ok]** を選択し、 **[保存]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="1259b-247">Select **Ok** and then **Save**.</span></span>

    [![](external-authentication-services/_static/image77.png "Click to Expand the Image")](external-authentication-services/_static/image77.png)

<a id="DISABLE"></a>
### <a name="optional-disable-local-registration"></a><span data-ttu-id="1259b-248">省略可能: ローカル登録を無効にする</span><span class="sxs-lookup"><span data-stu-id="1259b-248">Optional: Disable Local Registration</span></span>

<span data-ttu-id="1259b-249">現在の ASP.NET ローカル登録機能では、自動プログラム (ボット) によるメンバーアカウントの作成が妨げられることはありません。たとえば、 [CAPTCHA](../../../web-pages/overview/security/16-adding-security-and-membership.md)のようなボット防止と検証テクノロジを使用します。</span><span class="sxs-lookup"><span data-stu-id="1259b-249">The current ASP.NET local registration functionality does not prevent automated programs (bots) from creating member accounts; for example, by using a bot-prevention and validation technology like [CAPTCHA](../../../web-pages/overview/security/16-adding-security-and-membership.md).</span></span> <span data-ttu-id="1259b-250">このため、ログインページでローカルログインフォームと登録リンクを削除する必要があります。</span><span class="sxs-lookup"><span data-stu-id="1259b-250">Because of this, you should remove the local login form and registration link on the login page.</span></span> <span data-ttu-id="1259b-251">これを行うには、プロジェクトの [ *\_のログイン*] ページを開き、[ローカルログイン] パネルと [登録] リンクの行をコメントアウトします。</span><span class="sxs-lookup"><span data-stu-id="1259b-251">To do so, open the *\_Login.cshtml* page in your project, and then comment out the lines for the local login panel and the registration link.</span></span> <span data-ttu-id="1259b-252">結果のページは、次のコードサンプルのようになります。</span><span class="sxs-lookup"><span data-stu-id="1259b-252">The resulting page should look like the following code sample:</span></span>

[!code-html[Main](external-authentication-services/samples/sample10.html)]

<span data-ttu-id="1259b-253">[ローカルログイン] パネルと登録リンクが無効になると、ログインページには、有効にした外部認証プロバイダーのみが表示されます。</span><span class="sxs-lookup"><span data-stu-id="1259b-253">Once the local login panel and the registration link have been disabled, your login page will only display the external authentication providers that you have enabled:</span></span>

[![](external-authentication-services/_static/image70.png "Click to Expand the Image")](external-authentication-services/_static/image69.png)
