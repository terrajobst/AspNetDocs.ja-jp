---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-10
title: アプリを Azure Azure App Service | に発行します。Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 10fd812b-94d6-4967-be97-a31ce9c45e2c
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-10
msc.type: authoredcontent
ms.openlocfilehash: a9a7b74a07c71b47253c0af304c7a26ffa4eaae5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78504760"
---
# <a name="publish-the-app-to-azure-azure-app-service"></a><span data-ttu-id="bea95-102">アプリを Azure Azure App Service に発行する</span><span class="sxs-lookup"><span data-stu-id="bea95-102">Publish the App to Azure Azure App Service</span></span>

<span data-ttu-id="bea95-103">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="bea95-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="bea95-104">完成したプロジェクトのダウンロード</span><span class="sxs-lookup"><span data-stu-id="bea95-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="bea95-105">最後の手順として、アプリケーションを Azure に発行します。</span><span class="sxs-lookup"><span data-stu-id="bea95-105">As the last step, you will publish the application to Azure.</span></span> <span data-ttu-id="bea95-106">ソリューションエクスプローラーで、プロジェクトを右クリックし、 **[発行]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="bea95-106">In Solution Explorer, right-click the project and select **Publish**.</span></span>

![](part-10/_static/image1.png)

<span data-ttu-id="bea95-107">**[発行]** をクリックすると、 **[Web の発行]** ダイアログが呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="bea95-107">Clicking **Publish** invokes the **Publish Web** dialog.</span></span> <span data-ttu-id="bea95-108">最初にプロジェクトを作成したときに **[クラウドでホスト]** をオンにした場合、接続と設定は既に構成されています。</span><span class="sxs-lookup"><span data-stu-id="bea95-108">If you checked **Host in Cloud** when you first created the project, then the connection and settings are already configured.</span></span> <span data-ttu-id="bea95-109">その場合は、 **[設定]** タブをクリックし、Code First Migrations&quot;を実行 &quot;を確認します。</span><span class="sxs-lookup"><span data-stu-id="bea95-109">In that case, just click the **Settings** tab and check &quot;Execute Code First Migrations&quot;.</span></span> <span data-ttu-id="bea95-110">(最初に**クラウドのホスト**を確認していない場合は、[次のセクション](#new-website)の手順に従います)。</span><span class="sxs-lookup"><span data-stu-id="bea95-110">(If you didn't check **Host in Cloud** at the beginning, then follow the steps in the [next section](#new-website).)</span></span>

[![](part-10/_static/image3.png)](part-10/_static/image2.png)

<span data-ttu-id="bea95-111">アプリをデプロイするには、 **[発行]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="bea95-111">To deploy the app, click **Publish**.</span></span> <span data-ttu-id="bea95-112">発行の進行状況は、 **[Web 発行アクティビティ]** ウィンドウで確認できます。</span><span class="sxs-lookup"><span data-stu-id="bea95-112">You can view the publishing progress in the **Web Publish Activity** window.</span></span> <span data-ttu-id="bea95-113">( **[表示]** メニューの **[その他のウィンドウ]** を選択し、 **[Web 発行アクティビティ]** を選択します)。</span><span class="sxs-lookup"><span data-stu-id="bea95-113">(From the **View** menu, select **Other Windows**, then select **Web Publish Activity**.)</span></span>

![](part-10/_static/image4.png)

<span data-ttu-id="bea95-114">Visual Studio でアプリのデプロイが完了すると、既定のブラウザーが自動的に開き、デプロイされた web サイトの URL が表示され、作成したアプリケーションがクラウドで実行されるようになります。</span><span class="sxs-lookup"><span data-stu-id="bea95-114">When Visual Studio finishes deploying the app, the default browser automatically opens to the URL of the deployed website, and the application that you created is now running in the cloud.</span></span> <span data-ttu-id="bea95-115">ブラウザーのアドレスバーの URL は、サイトがインターネットから読み込まれていることを示しています。</span><span class="sxs-lookup"><span data-stu-id="bea95-115">The URL in the browser address bar shows that the site is being loaded from the Internet.</span></span>

[![](part-10/_static/image6.png)](part-10/_static/image5.png)

<a id="new-website"></a>
## <a name="deploying-to-a-new-website"></a><span data-ttu-id="bea95-116">新しい Web サイトへのデプロイ</span><span class="sxs-lookup"><span data-stu-id="bea95-116">Deploying to a New Website</span></span>

<span data-ttu-id="bea95-117">最初にプロジェクトを作成したときに**クラウドのホスト**を確認しなかった場合は、ここで新しい web アプリを構成できます。</span><span class="sxs-lookup"><span data-stu-id="bea95-117">If you did not check **Host in Cloud** when you first created the project, you can configure a new web app now.</span></span> <span data-ttu-id="bea95-118">ソリューションエクスプローラーで、プロジェクトを右クリックし、 **[発行]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="bea95-118">In Solution Explorer, right-click the project and select **Publish**.</span></span> <span data-ttu-id="bea95-119">**[プロファイル]** タブを選択し、 **[Microsoft Azure Websites]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="bea95-119">Select the **Profile** tab and click **Microsoft Azure Websites**.</span></span> <span data-ttu-id="bea95-120">現在 Azure にサインインしていない場合は、サインインするように求められます。</span><span class="sxs-lookup"><span data-stu-id="bea95-120">If you aren't currently signed in to Azure, you will be prompted to sign in.</span></span>

[![](part-10/_static/image8.png)](part-10/_static/image7.png)

<span data-ttu-id="bea95-121">**[既存の Web サイト]** ダイアログで、 **[新規]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="bea95-121">In the **Existing Websites** dialog, click **New**.</span></span>

![](part-10/_static/image9.png)

<span data-ttu-id="bea95-122">サイト名を入力してください。</span><span class="sxs-lookup"><span data-stu-id="bea95-122">Enter a site name.</span></span> <span data-ttu-id="bea95-123">Azure サブスクリプションとリージョンを選択します。</span><span class="sxs-lookup"><span data-stu-id="bea95-123">Select your Azure subscription and the region.</span></span> <span data-ttu-id="bea95-124">**[データベースサーバー]** で、 **[新しいサーバーの作成]** を選択するか、既存のサーバーを選択します。</span><span class="sxs-lookup"><span data-stu-id="bea95-124">Under **Database server**, select **Create New Server**, or select an existing server.</span></span> <span data-ttu-id="bea95-125">**Create** をクリックしてください。</span><span class="sxs-lookup"><span data-stu-id="bea95-125">Click **Create**.</span></span>

[![](part-10/_static/image11.png)](part-10/_static/image10.png)

<span data-ttu-id="bea95-126">**[設定]** タブをクリックし、Code First Migrations&quot;を実行 &quot;を確認します。</span><span class="sxs-lookup"><span data-stu-id="bea95-126">Click the **Settings** tab and check &quot;Execute Code First Migrations&quot;.</span></span> <span data-ttu-id="bea95-127">**[発行]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="bea95-127">Then click **Publish**.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="bea95-128">[[戻る]](part-9.md)</span><span class="sxs-lookup"><span data-stu-id="bea95-128">[Previous](part-9.md)</span></span>
