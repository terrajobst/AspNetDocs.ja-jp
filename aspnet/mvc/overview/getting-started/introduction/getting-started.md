---
uid: mvc/overview/getting-started/introduction/getting-started
title: ASP.NET MVC 5 でのはじめに |Microsoft Docs
author: Rick-Anderson
ms.author: riande
ms.date: 10/04/2018
ms.assetid: f3d8adbe-55e7-4fd4-84a8-7155bc45c676
msc.legacyurl: /mvc/overview/getting-started/introduction/getting-started
msc.type: authoredcontent
ms.openlocfilehash: ca39bc37c757c0452cf56624c8e37c04df4b41f2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78487954"
---
# <a name="getting-started-with-aspnet-mvc-5"></a><span data-ttu-id="d5989-102">ASP.NET MVC 5 の概要</span><span class="sxs-lookup"><span data-stu-id="d5989-102">Getting started with ASP.NET MVC 5</span></span>

<span data-ttu-id="d5989-103">[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="d5989-103">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[!INCLUDE [consider RP](../../../../includes/razor.md)]

<span data-ttu-id="d5989-104">このチュートリアルでは、 [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)を使用して ASP.NET MVC 5 web アプリを構築するための基本について説明します。</span><span class="sxs-lookup"><span data-stu-id="d5989-104">This tutorial teaches you the basics of building an ASP.NET MVC 5 web app using [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017).</span></span> <span data-ttu-id="d5989-105">チュートリアルの最終的なソースコードは、 [GitHub](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/mvc/overview/getting-started/introduction/sample/MvcMovie/MvcMovie)にあります。</span><span class="sxs-lookup"><span data-stu-id="d5989-105">The final source code for the tutorial is located on [GitHub](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/mvc/overview/getting-started/introduction/sample/MvcMovie/MvcMovie).</span></span>

<span data-ttu-id="d5989-106">このチュートリアルは、 [Scott Guthrie](https://weblogs.asp.net/scottgu/) (twitter[@scottgu](https://twitter.com/scottgu) )、 [scott マン selman](http://www.hanselman.com/blog/) (Twitter: [@shanselman](https://twitter.com/shanselman) )、および[Rick Anderson](https://twitter.com/RickAndMSFT) ( [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) ) によって作成されました。</span><span class="sxs-lookup"><span data-stu-id="d5989-106">This tutorial was written by [Scott Guthrie](https://weblogs.asp.net/scottgu/) (twitter[@scottgu](https://twitter.com/scottgu) ), [Scott Hanselman](http://www.hanselman.com/blog/) (twitter: [@shanselman](https://twitter.com/shanselman) ), and [Rick Anderson](https://twitter.com/RickAndMSFT) ( [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) )</span></span>

<span data-ttu-id="d5989-107">このアプリを Azure にデプロイするには、Azure アカウントが必要です。</span><span class="sxs-lookup"><span data-stu-id="d5989-107">You need an Azure account to deploy this app to Azure:</span></span>

- <span data-ttu-id="d5989-108">無料で[azure アカウントを開く](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604)ことができます。有料の azure サービスを試用するために使用できるクレジットが得られます。また、使用した後でも、アカウントを保持し、無料の azure サービスを使用することができます。</span><span class="sxs-lookup"><span data-stu-id="d5989-108">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) - You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services.</span></span>
- <span data-ttu-id="d5989-109">[MSDN サブスクライバーの特典を有効にする](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) こともできます - MSDN サブスクリプションにより、有料の Azure のサービスを使用できるクレジットが毎月与えられます。</span><span class="sxs-lookup"><span data-stu-id="d5989-109">You can [activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) - Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>

## <a name="get-started"></a><span data-ttu-id="d5989-110">はじめに</span><span class="sxs-lookup"><span data-stu-id="d5989-110">Get started</span></span>

<span data-ttu-id="d5989-111">まず、 [Visual Studio 2017 をインストール](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)します。</span><span class="sxs-lookup"><span data-stu-id="d5989-111">Start by [installing Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017).</span></span> <span data-ttu-id="d5989-112">次に、Visual Studio を開きます。</span><span class="sxs-lookup"><span data-stu-id="d5989-112">Then, open Visual Studio.</span></span>

<span data-ttu-id="d5989-113">Visual Studio は、IDE または統合開発環境です。</span><span class="sxs-lookup"><span data-stu-id="d5989-113">Visual Studio is an IDE, or integrated development environment.</span></span> <span data-ttu-id="d5989-114">Microsoft Word を使用してドキュメントを記述するのと同じように、IDE を使用してアプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="d5989-114">Just like you use Microsoft Word to write documents, you'll use an IDE to create applications.</span></span> <span data-ttu-id="d5989-115">Visual Studio には、使用可能なさまざまなオプションを示す下部の一覧があります。</span><span class="sxs-lookup"><span data-stu-id="d5989-115">In Visual Studio, there's a list along the bottom showing various options available to you.</span></span> <span data-ttu-id="d5989-116">IDE でタスクを実行する別の方法を提供するメニューもあります。</span><span class="sxs-lookup"><span data-stu-id="d5989-116">There's also a menu that provides another way to perform tasks in the IDE.</span></span> <span data-ttu-id="d5989-117">たとえば、**スタートページ**で **[新しいプロジェクト]** を選択する代わりに、メニューバーを使用して [**ファイル** > **新しいプロジェクト**] を選択できます。</span><span class="sxs-lookup"><span data-stu-id="d5989-117">For example, instead of selecting **New Project** on the **Start page**, you can use the menu bar and select **File** > **New Project**.</span></span>

![](getting-started/_static/image1.png)

## <a name="create-your-first-app"></a><span data-ttu-id="d5989-118">最初のアプリを作成する</span><span class="sxs-lookup"><span data-stu-id="d5989-118">Create your first app</span></span>

<span data-ttu-id="d5989-119">[**開始] ページ**で、 **[新しいプロジェクト]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="d5989-119">On the **Start page**, select **New Project**.</span></span> <span data-ttu-id="d5989-120">**[新しいプロジェクト]** ダイアログボックスで、左側の **[ビジュアルC# ]** カテゴリ、 **[web]** の順に選択し、 **[ASP.NET Web Application (.NET Framework)]** プロジェクトテンプレートを選択します。</span><span class="sxs-lookup"><span data-stu-id="d5989-120">In the **New project** dialog box, select the **Visual C#** category on the left, then **Web**, and then select the **ASP.NET Web Application (.NET Framework)** project template.</span></span> <span data-ttu-id="d5989-121">プロジェクトに "MvcMovie" という名前を入力し、[ **OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="d5989-121">Name your project "MvcMovie" and then choose **OK**.</span></span>

![](getting-started/_static/image2.png)

<span data-ttu-id="d5989-122">**[New ASP.NET Web Application]** ダイアログボックスで **[MVC]** を選択し、[ **OK]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="d5989-122">In the **New ASP.NET Web Application** dialog, choose **MVC** and then choose **OK**.</span></span>

![](getting-started/_static/image3.png)

<span data-ttu-id="d5989-123">Visual Studio では、先ほど作成した ASP.NET MVC プロジェクトの既定のテンプレートが使用されているため、何もしなくても、すぐに動作するアプリケーションがあります。</span><span class="sxs-lookup"><span data-stu-id="d5989-123">Visual Studio used a default template for the ASP.NET MVC project you just created, so you have a working application right now without doing anything!</span></span> <span data-ttu-id="d5989-124">これは単純な "Hello World!" です。</span><span class="sxs-lookup"><span data-stu-id="d5989-124">This is a simple "Hello World!"</span></span> <span data-ttu-id="d5989-125">プロジェクトは、アプリケーションを起動するのに適した場所です。</span><span class="sxs-lookup"><span data-stu-id="d5989-125">project, and it's a good place to start your application.</span></span>

![](getting-started/_static/image4.png)

<span data-ttu-id="d5989-126">**F5** キーを押してデバッグを開始します。</span><span class="sxs-lookup"><span data-stu-id="d5989-126">Press **F5** to start debugging.</span></span> <span data-ttu-id="d5989-127">**F5**キーを押すと、Visual Studio が起動し[IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) 、web アプリが実行されます。</span><span class="sxs-lookup"><span data-stu-id="d5989-127">When you press **F5**, Visual Studio starts [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) and runs your web app.</span></span> <span data-ttu-id="d5989-128">その後、Visual Studio によってブラウザーが起動し、アプリケーションのホームページが開きます。</span><span class="sxs-lookup"><span data-stu-id="d5989-128">Visual Studio then launches a browser and opens the application's home page.</span></span> <span data-ttu-id="d5989-129">ブラウザーのアドレスバーには `localhost:port#` が表示され、`example.com`のようなものではないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="d5989-129">Notice that the address bar of the browser says `localhost:port#` and not something like `example.com`.</span></span> <span data-ttu-id="d5989-130">これは、`localhost` が常に独自のローカルコンピューターを指しているためです。この場合は、先ほど作成したアプリケーションが実行されています。</span><span class="sxs-lookup"><span data-stu-id="d5989-130">That's because `localhost` always points to your own local computer, which in this case is running the application you just built.</span></span> <span data-ttu-id="d5989-131">Visual Studio で web プロジェクトを実行する場合、web サーバーにはランダムなポートが使用されます。</span><span class="sxs-lookup"><span data-stu-id="d5989-131">When Visual Studio runs a web project, a random port is used for the web server.</span></span> <span data-ttu-id="d5989-132">次の図では、ポート番号は1234です。</span><span class="sxs-lookup"><span data-stu-id="d5989-132">In the image below, the port number is 1234.</span></span> <span data-ttu-id="d5989-133">アプリケーションを実行すると、別のポート番号が表示されます。</span><span class="sxs-lookup"><span data-stu-id="d5989-133">When you run the application, you'll see a different port number.</span></span>

![](getting-started/_static/image5.png)

<span data-ttu-id="d5989-134">すぐに使用できる既定のテンプレートでは、`Home`、`Contact`、および `About` の各ページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="d5989-134">Right out of the box this default template gives you `Home`, `Contact`, and `About` pages.</span></span> <span data-ttu-id="d5989-135">次の画像には、 **[ホーム]** 、 **[About]** 、 **[Contact]** のリンクは表示されません。</span><span class="sxs-lookup"><span data-stu-id="d5989-135">The image below doesn't show the **Home**, **About**, and **Contact** links.</span></span> <span data-ttu-id="d5989-136">ブラウザーウィンドウのサイズによっては、ナビゲーションアイコンをクリックしてこれらのリンクを表示することが必要になる場合があります。</span><span class="sxs-lookup"><span data-stu-id="d5989-136">Depending on the size of your browser window, you might need to click the navigation icon to see these links.</span></span>

![](getting-started/_static/image6.png)

<span data-ttu-id="d5989-137">アプリケーションでは、登録とログインもサポートされています。</span><span class="sxs-lookup"><span data-stu-id="d5989-137">The application also provides support to register and log in.</span></span> <span data-ttu-id="d5989-138">次の手順では、このアプリケーションの動作を変更し、ASP.NET MVC について少し説明します。</span><span class="sxs-lookup"><span data-stu-id="d5989-138">The next step is to change how this application works and learn a little bit about ASP.NET MVC.</span></span> <span data-ttu-id="d5989-139">ASP.NET MVC アプリケーションを閉じて、いくつかのコードを変更してみましょう。</span><span class="sxs-lookup"><span data-stu-id="d5989-139">Close the ASP.NET MVC application and let's change some code.</span></span>

<span data-ttu-id="d5989-140">現在のチュートリアルの一覧については、「MVC に関する[推奨事項](../mvc-learning-sequence.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="d5989-140">For a list of current tutorials, see [MVC recommended articles](../mvc-learning-sequence.md).</span></span>

## <a name="see-this-app-running-on-azure"></a><span data-ttu-id="d5989-141">このアプリが Azure で実行されていることを確認する</span><span class="sxs-lookup"><span data-stu-id="d5989-141">See this app running on Azure</span></span>

<span data-ttu-id="d5989-142">完成したサイトがライブ web アプリとして実行されていることを確認しますか?</span><span class="sxs-lookup"><span data-stu-id="d5989-142">Would you like to see the finished site running as a live web app?</span></span> <span data-ttu-id="d5989-143">次のボタンをクリックするだけで、アプリの完全なバージョンを Azure アカウントにデプロイできます。</span><span class="sxs-lookup"><span data-stu-id="d5989-143">You can deploy a complete version of the app to your Azure account by simply clicking the following button.</span></span>

[![](https://azuredeploy.net/deploybutton.png)](https://azuredeploy.net/?repository=https://github.com/dotnet/AspNetDocs/tree/master/aspnet/mvc/overview/getting-started/introduction/sample/MvcMovie&amp;WT.mc_id=deploy_azure_aspnet)

<span data-ttu-id="d5989-144">このソリューションを Azure にデプロイするには、Azure アカウントが必要です。</span><span class="sxs-lookup"><span data-stu-id="d5989-144">You need an Azure account to deploy this solution to Azure.</span></span> <span data-ttu-id="d5989-145">まだアカウントを持っていない場合は、次のいずれかのオプションを使用して作成します。</span><span class="sxs-lookup"><span data-stu-id="d5989-145">If you don't already have an account, use one of the following options to create one:</span></span>

- <span data-ttu-id="d5989-146">[無料で azure アカウントを開く](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604)-有料の azure サービスを試用するために使用できるクレジットが得られます。また、使用した後でも、アカウントを保持し、無料の azure サービスを使用できます。</span><span class="sxs-lookup"><span data-stu-id="d5989-146">[Open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) - You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services.</span></span>
- <span data-ttu-id="d5989-147">[Visual studio サブスクライバーの特典を有効](https://azure.microsoft.com/pricing/member-offers/credit-for-visual-studio-subscribers)にする-visual studio サブスクリプションでは、有料の Azure サービスに使用できるクレジットが毎月提供されます。</span><span class="sxs-lookup"><span data-stu-id="d5989-147">[Activate Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/credit-for-visual-studio-subscribers) - Your Visual Studio subscription gives you credits every month that you can use for paid Azure services.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="d5989-148">Next</span><span class="sxs-lookup"><span data-stu-id="d5989-148">Next</span></span>](adding-a-controller.md)
