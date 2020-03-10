---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-1
title: Entity Framework 6 | で Web API 2 を使用するMicrosoft Docs
author: MikeWasson
description: このチュートリアルでは、ASP.NET Web API バックエンドを使用して web アプリケーションを作成する方法の基本について説明します。 このチュートリアルでは、データのレイアウトに Entity Framework 6 を使用します。
ms.author: riande
ms.date: 01/17/2019
ms.assetid: e879487e-dbcd-4b33-b092-d67c37ae768c
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-1
msc.type: authoredcontent
ms.openlocfilehash: 0f5dc960f494af5bd4ce87863a510d1892319908
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78504838"
---
# <a name="using-web-api-2-with-entity-framework-6"></a><span data-ttu-id="c0e34-104">Web API 2 と Entity Framework 6 を使用する</span><span class="sxs-lookup"><span data-stu-id="c0e34-104">Using Web API 2 with Entity Framework 6</span></span>

[<span data-ttu-id="c0e34-105">完成したプロジェクトのダウンロード</span><span class="sxs-lookup"><span data-stu-id="c0e34-105">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

> <span data-ttu-id="c0e34-106">このチュートリアルでは、ASP.NET Web API バックエンドを使用して web アプリケーションを作成する方法の基本について説明します。</span><span class="sxs-lookup"><span data-stu-id="c0e34-106">This tutorial teaches you the basics of creating a web application with an ASP.NET Web API back end.</span></span> <span data-ttu-id="c0e34-107">このチュートリアルでは、データ層に Entity Framework 6 を使用し、クライアント側の JavaScript アプリケーションにはノックアウトを使用します。</span><span class="sxs-lookup"><span data-stu-id="c0e34-107">The tutorial uses Entity Framework 6 for the data layer, and Knockout.js for the client-side JavaScript application.</span></span> <span data-ttu-id="c0e34-108">このチュートリアルでは、Azure App Service Web Apps にアプリを展開する方法についても説明します。</span><span class="sxs-lookup"><span data-stu-id="c0e34-108">The tutorial also shows how to deploy the app to Azure App Service Web Apps.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="c0e34-109">このチュートリアルで使用されているソフトウェアのバージョン</span><span class="sxs-lookup"><span data-stu-id="c0e34-109">Software versions used in the tutorial</span></span>
>
> - <span data-ttu-id="c0e34-110">Web API 2.1</span><span class="sxs-lookup"><span data-stu-id="c0e34-110">Web API 2.1</span></span>
> - <span data-ttu-id="c0e34-111">Visual Studio 2017 (Visual Studio 2017 を[こちら](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)からダウンロード)</span><span class="sxs-lookup"><span data-stu-id="c0e34-111">Visual Studio 2017 (download Visual Studio 2017 [here](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017))</span></span>
> - <span data-ttu-id="c0e34-112">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="c0e34-112">Entity Framework 6</span></span>
> - <span data-ttu-id="c0e34-113">.NET 4.7</span><span class="sxs-lookup"><span data-stu-id="c0e34-113">.NET 4.7</span></span>
> - <span data-ttu-id="c0e34-114">[ノックアウト](http://knockoutjs.com/)3.1</span><span class="sxs-lookup"><span data-stu-id="c0e34-114">[Knockout.js](http://knockoutjs.com/) 3.1</span></span>

<span data-ttu-id="c0e34-115">このチュートリアルでは、ASP.NET Web API 2 と Entity Framework 6 を使用して、バックエンドデータベースを操作する Web アプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="c0e34-115">This tutorial uses ASP.NET Web API 2 with Entity Framework 6 to create a web application that manipulates a back-end database.</span></span> <span data-ttu-id="c0e34-116">ここでは、作成するアプリケーションのスクリーンショットを示します。</span><span class="sxs-lookup"><span data-stu-id="c0e34-116">Here is a screen shot of the application that you will create.</span></span>

[![](part-1/_static/image2.png)](part-1/_static/image1.png)

<span data-ttu-id="c0e34-117">アプリでは、シングルページアプリケーション (SPA) 設計が使用されます。</span><span class="sxs-lookup"><span data-stu-id="c0e34-117">The app uses a single-page application (SPA) design.</span></span> <span data-ttu-id="c0e34-118">"シングルページアプリケーション" とは、1つの HTML ページを読み込み、新しいページを読み込むのではなく、ページを動的に更新する web アプリケーションの一般的な用語です。</span><span class="sxs-lookup"><span data-stu-id="c0e34-118">"Single-page application" is the general term for a web application that loads a single HTML page and then updates the page dynamically, instead of loading new pages.</span></span> <span data-ttu-id="c0e34-119">最初のページの読み込み後、アプリは AJAX 要求を通じてサーバーと通信します。</span><span class="sxs-lookup"><span data-stu-id="c0e34-119">After the initial page load, the app talks with the server through AJAX requests.</span></span> <span data-ttu-id="c0e34-120">AJAX 要求は、アプリが UI を更新するために使用する JSON データを返します。</span><span class="sxs-lookup"><span data-stu-id="c0e34-120">The AJAX requests return JSON data, which the app uses to update the UI.</span></span>

<span data-ttu-id="c0e34-121">AJAX は新しく追加されたものではありませんが、今日では、大規模な高度な SPA アプリケーションの構築と保守を容易にする JavaScript フレームワークが用意されています。</span><span class="sxs-lookup"><span data-stu-id="c0e34-121">AJAX isn't new, but today there are JavaScript frameworks that make it easier to build and maintain a large sophisticated SPA application.</span></span> <span data-ttu-id="c0e34-122">このチュートリアルでは、[ノックアウト](http://knockoutjs.com/)を使用しますが、任意の JavaScript クライアントフレームワークを使用できます。</span><span class="sxs-lookup"><span data-stu-id="c0e34-122">This tutorial uses [Knockout.js](http://knockoutjs.com/), but you can use any JavaScript client framework.</span></span>

<span data-ttu-id="c0e34-123">このアプリの主な構成要素は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="c0e34-123">Here are the main building blocks for this app:</span></span>

- <span data-ttu-id="c0e34-124">ASP.NET MVC では、HTML ページが作成されます。</span><span class="sxs-lookup"><span data-stu-id="c0e34-124">ASP.NET MVC creates the HTML page.</span></span>
- <span data-ttu-id="c0e34-125">ASP.NET Web API は、AJAX 要求を処理し、JSON データを返します。</span><span class="sxs-lookup"><span data-stu-id="c0e34-125">ASP.NET Web API handles the AJAX requests and returns JSON data.</span></span>
- <span data-ttu-id="c0e34-126">ノックアウトデータ-HTML 要素を JSON データにバインドします。</span><span class="sxs-lookup"><span data-stu-id="c0e34-126">Knockout.js data-binds the HTML elements to the JSON data.</span></span>
- <span data-ttu-id="c0e34-127">Entity Framework データベースと対話します。</span><span class="sxs-lookup"><span data-stu-id="c0e34-127">Entity Framework talks to the database.</span></span>

## <a name="see-this-app-running-on-azure"></a><span data-ttu-id="c0e34-128">このアプリが Azure で実行されていることを確認する</span><span class="sxs-lookup"><span data-stu-id="c0e34-128">See this app running on Azure</span></span>

<span data-ttu-id="c0e34-129">完成したサイトがライブ web アプリとして実行されていることを確認しますか?</span><span class="sxs-lookup"><span data-stu-id="c0e34-129">Would you like to see the finished site running as a live web app?</span></span> <span data-ttu-id="c0e34-130">次のボタンを選択すると、アプリの完全なバージョンを Azure アカウントにデプロイできます。</span><span class="sxs-lookup"><span data-stu-id="c0e34-130">You can deploy a complete version of the app to your Azure account by selecting the following button.</span></span>

[![](http://azuredeploy.net/deploybutton.png)](https://azuredeploy.net/?WT.mc_id=deploy_azure_aspnet&repository=https://github.com/tfitzmac/BookService)

<span data-ttu-id="c0e34-131">このソリューションを Azure にデプロイするには、Azure アカウントが必要です。</span><span class="sxs-lookup"><span data-stu-id="c0e34-131">You need an Azure account to deploy this solution to Azure.</span></span> <span data-ttu-id="c0e34-132">まだアカウントを持っていない場合は、次のオプションがあります。</span><span class="sxs-lookup"><span data-stu-id="c0e34-132">If you do not already have an account, you have the following options:</span></span>

- <span data-ttu-id="c0e34-133">[無料で azure アカウントを開く](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604)-有料の azure サービスを試用するために使用できるクレジットが得られます。また、使用した後でも、アカウントを保持し、無料の azure サービスを使用できます。</span><span class="sxs-lookup"><span data-stu-id="c0e34-133">[Open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) - You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services.</span></span>
- <span data-ttu-id="c0e34-134">[Msdn サブスクライバーの特典を有効](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604)にする-msdn サブスクリプションでは、有料の Azure サービスに使用できるクレジットが毎月提供されます。</span><span class="sxs-lookup"><span data-stu-id="c0e34-134">[Activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) - Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>

## <a name="create-the-project"></a><span data-ttu-id="c0e34-135">プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="c0e34-135">Create the project</span></span>

<span data-ttu-id="c0e34-136">Visual Studio を開きます。</span><span class="sxs-lookup"><span data-stu-id="c0e34-136">Open Visual Studio.</span></span> <span data-ttu-id="c0e34-137">**[ファイル]** メニューの **[新規作成]** をポイントし、 **[プロジェクト]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="c0e34-137">From the **File** menu, select **New**, then select **Project**.</span></span> <span data-ttu-id="c0e34-138">(または、スタートページで **[新しいプロジェクト]** を選択します)。</span><span class="sxs-lookup"><span data-stu-id="c0e34-138">(Or select **New Project** on the Start page.)</span></span>

<span data-ttu-id="c0e34-139">**[新しいプロジェクト]** ダイアログボックスの左ペインで **[web]** を選択し、中央のペインで**ASP.NET web アプリケーション (.NET Framework)** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c0e34-139">In the **New Project** dialog, select **Web** in the left pane and **ASP.NET Web Application (.NET Framework)** in the middle pane.</span></span> <span data-ttu-id="c0e34-140">プロジェクトに「 **Bookservice** 」という名前を指定し、[ **OK]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="c0e34-140">Name the project **BookService** and select **OK**.</span></span>

[![](part-1/_static/image11.png)](part-1/_static/image11.png)

<span data-ttu-id="c0e34-141">**[New ASP.NET Project]** ダイアログで、 **[Web API]** テンプレートを選択します。</span><span class="sxs-lookup"><span data-stu-id="c0e34-141">In the **New ASP.NET Project** dialog, select the **Web API** template.</span></span>

[![](part-1/_static/image12.png)](part-1/_static/image12.png)

<span data-ttu-id="c0e34-142">**[OK]** を選択すると、プロジェクトが作成されます。</span><span class="sxs-lookup"><span data-stu-id="c0e34-142">Select **OK** to create the project.</span></span>

## <a name="configure-azure-settings-optional"></a><span data-ttu-id="c0e34-143">Azure の設定を構成する (省略可能)</span><span class="sxs-lookup"><span data-stu-id="c0e34-143">Configure Azure settings (optional)</span></span>

<span data-ttu-id="c0e34-144">プロジェクトを作成した後、いつでも Azure App Service Web Apps にデプロイすることを選択できます。</span><span class="sxs-lookup"><span data-stu-id="c0e34-144">After you create the project, you can choose to deploy to Azure App Service Web Apps at any time.</span></span> 

1. <span data-ttu-id="c0e34-145">ソリューションエクスプローラーで、プロジェクトを右クリックし、 **[発行]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="c0e34-145">In Solution Explorer, right-click on your project and select **Publish**.</span></span>

2. <span data-ttu-id="c0e34-146">表示されるウィンドウで、 **[開始]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="c0e34-146">In the window that appears, select **Start**.</span></span> <span data-ttu-id="c0e34-147">**[発行先の選択]** ダイアログボックスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="c0e34-147">The **Pick a publish target** dialog box appears.</span></span>

   [![](part-1/_static/image14.png)](part-1/_static/image14.png)

3. <span data-ttu-id="c0e34-148">**[プロファイルの作成]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="c0e34-148">Select **Create Profile**.</span></span> <span data-ttu-id="c0e34-149">**[App Service の作成]** ダイアログ ボックスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="c0e34-149">The **Create App Service** dialog box appears.</span></span>

   [![](part-1/_static/image15.png)](part-1/_static/image15.png)

   <span data-ttu-id="c0e34-150">既定値をそのまま使用するか、アプリケーション名、リソースグループ、ホスティングプラン、Azure サブスクリプション、地理的リージョンに異なる値を入力します。</span><span class="sxs-lookup"><span data-stu-id="c0e34-150">Accept the defaults, or enter different values for the application name, resource group, hosting plan, Azure subscription, and geographical region.</span></span> 

4. <span data-ttu-id="c0e34-151">**[SQL データベースの作成]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="c0e34-151">Select **Create a SQL database**.</span></span> <span data-ttu-id="c0e34-152">**[SQL Server の構成]** ダイアログボックスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="c0e34-152">The **Configure SQL Server** dialog box appears.</span></span> 

   [![](part-1/_static/image16.png)](part-1/_static/image16.png)

   <span data-ttu-id="c0e34-153">既定値をそのまま使用するか、別の値を入力します。</span><span class="sxs-lookup"><span data-stu-id="c0e34-153">Accept the defaults or enter different values.</span></span> <span data-ttu-id="c0e34-154">新しいデータベースの**管理者のユーザー名**と**管理者パスワード**を入力します。</span><span class="sxs-lookup"><span data-stu-id="c0e34-154">Enter an **Administrator Username** and **Administrator Password** for your new database.</span></span> <span data-ttu-id="c0e34-155">完了したら、[ **OK]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="c0e34-155">Select **OK** when you're done.</span></span> <span data-ttu-id="c0e34-156">**[App Service の作成]** ページが再び表示されます。</span><span class="sxs-lookup"><span data-stu-id="c0e34-156">The **Create App Service** page reappears.</span></span>

5. <span data-ttu-id="c0e34-157">**[作成]** を選択して、プロファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="c0e34-157">Select **Create** to create your profile.</span></span> <span data-ttu-id="c0e34-158">展開が進行中であることを示すメッセージが右下隅に表示されます。</span><span class="sxs-lookup"><span data-stu-id="c0e34-158">A message appears in the lower-right corner indicating that deployment is in progress.</span></span> <span data-ttu-id="c0e34-159">しばらくすると、 **[発行]** ウィンドウが再び表示されます。</span><span class="sxs-lookup"><span data-stu-id="c0e34-159">After a short while, the **Publish** window reappears.</span></span>

    [![](part-1/_static/image17.png)](part-1/_static/image17.png)
   
    <span data-ttu-id="c0e34-160">これで、アプリをデプロイするために作成したプロファイルが使用できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="c0e34-160">The profile you created to deploy the app is now available.</span></span> 

> [!div class="step-by-step"]
> [<span data-ttu-id="c0e34-161">Next</span><span class="sxs-lookup"><span data-stu-id="c0e34-161">Next</span></span>](part-2.md)
