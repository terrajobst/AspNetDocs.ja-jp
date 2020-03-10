---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12
title: 'Visual Studio または Visual Web Developer を使用して SQL Server Compact で ASP.NET Web アプリケーションをデプロイする: コードのみの更新プログラムをデプロイする-8/12 |Microsoft Docs'
author: tdykstra
description: この一連のチュートリアルでは、Visual Stu... を使用して SQL Server Compact データベースを含む ASP.NET web アプリケーションプロジェクトをデプロイ (発行) する方法について説明します。
ms.author: riande
ms.date: 11/17/2011
ms.assetid: ddf6252f-9413-4c0c-a360-2cef8d231717
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12
msc.type: authoredcontent
ms.openlocfilehash: e4d094ef84a747c36ce05ddb0e3d1ce0391d5605
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78455074"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-a-code-only-update---8-of-12"></a><span data-ttu-id="8a702-103">Visual Studio または Visual Web Developer を使用した SQL Server Compact を使用した ASP.NET Web アプリケーションのデプロイ: コードのみの更新プログラムのデプロイ-8/12</span><span class="sxs-lookup"><span data-stu-id="8a702-103">Deploying an ASP.NET Web Application with SQL Server Compact using Visual Studio or Visual Web Developer: Deploying a Code-Only Update - 8 of 12</span></span>

<span data-ttu-id="8a702-104">[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="8a702-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="8a702-105">スタートプロジェクトのダウンロード</span><span class="sxs-lookup"><span data-stu-id="8a702-105">Download Starter Project</span></span>](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> <span data-ttu-id="8a702-106">この一連のチュートリアルでは、Visual Studio 2012 RC または Visual Studio Express 2012 RC for Web を使用して SQL Server Compact データベースを含む ASP.NET web アプリケーションプロジェクトをデプロイ (発行) する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="8a702-106">This series of tutorials shows you how to deploy (publish) an ASP.NET web application project that includes a SQL Server Compact database by using Visual Studio 2012 RC or Visual Studio Express 2012 RC for Web.</span></span> <span data-ttu-id="8a702-107">Web 発行の更新をインストールする場合は、Visual Studio 2010 を使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="8a702-107">You can also use Visual Studio 2010 if you install the Web Publish Update.</span></span> <span data-ttu-id="8a702-108">シリーズの概要については、[シリーズの最初のチュートリアル](deployment-to-a-hosting-provider-introduction-1-of-12.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="8a702-108">For an introduction to the series, see [the first tutorial in the series](deployment-to-a-hosting-provider-introduction-1-of-12.md).</span></span>
> 
> <span data-ttu-id="8a702-109">Visual Studio 2012 の RC リリース後に導入された配置機能を示すチュートリアルについては、SQL Server Compact 以外の SQL Server のエディションをデプロイする方法、Azure App Service Web Apps にデプロイする方法については、「 [ASP.NET Web deployment Using Visual studio (Visual studio を使用した Web デプロイ](../../deployment/visual-studio-web-deployment/introduction.md)のデプロイ)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="8a702-109">For a tutorial that shows deployment features introduced after the RC release of Visual Studio 2012, shows how to deploy SQL Server editions other than SQL Server Compact, and shows how to deploy to Azure App Service Web Apps, see [ASP.NET Web Deployment using Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md).</span></span>

## <a name="overview"></a><span data-ttu-id="8a702-110">概要</span><span class="sxs-lookup"><span data-stu-id="8a702-110">Overview</span></span>

<span data-ttu-id="8a702-111">最初のデプロイの後、web サイトの保守と開発の作業が継続し、その前に更新プログラムを展開する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8a702-111">After the initial deployment, your work of maintaining and developing your web site continues, and before long you will want to deploy an update.</span></span> <span data-ttu-id="8a702-112">このチュートリアルでは、アプリケーションコードに更新プログラムをデプロイするプロセスについて順を追って紹介します。</span><span class="sxs-lookup"><span data-stu-id="8a702-112">This tutorial takes you through the process of deploying an update to your application code.</span></span> <span data-ttu-id="8a702-113">この更新プログラムには、データベースの変更は含まれません。次のチュートリアルでは、データベースの変更を配置する場合の違いについて説明します。</span><span class="sxs-lookup"><span data-stu-id="8a702-113">This update does not involve a database change; you'll see what's different about deploying a database change in the next tutorial.</span></span>

<span data-ttu-id="8a702-114">リマインダー: チュートリアルを実行しているときにエラーメッセージが表示されたり機能しない場合は、必ず[トラブルシューティングのページ](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)を確認してください。</span><span class="sxs-lookup"><span data-stu-id="8a702-114">Reminder: If you get an error message or something doesn't work as you go through the tutorial, be sure to check the [troubleshooting page](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md).</span></span>

## <a name="making-a-code-change"></a><span data-ttu-id="8a702-115">コード変更の作成</span><span class="sxs-lookup"><span data-stu-id="8a702-115">Making a Code Change</span></span>

<span data-ttu-id="8a702-116">アプリケーションの更新の簡単な例として **、インストラクターのページに**、選択したインストラクターが担当するコースの一覧を追加します。</span><span class="sxs-lookup"><span data-stu-id="8a702-116">As a simple example of an update to your application, you'll add to the **Instructors** page a list of courses taught by the selected instructor.</span></span>

<span data-ttu-id="8a702-117">**インストラクター**ページを実行すると、グリッドに**選択**リンクがあることがわかりますが、行の背景を灰色にする以外には何も行われません。</span><span class="sxs-lookup"><span data-stu-id="8a702-117">If you run the **Instructors** page, you'll notice that there are **Select** links in the grid, but they don't do anything other than make the row background turn gray.</span></span>

<span data-ttu-id="8a702-118">[![Instructors_page](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="8a702-118">[![Instructors_page](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image1.png)</span></span>

<span data-ttu-id="8a702-119">次に、 **[選択]** リンクがクリックされたときに実行されるコードを追加します。選択したインストラクターによって担当されるコースの一覧が表示されます。</span><span class="sxs-lookup"><span data-stu-id="8a702-119">Now you'll add code that runs when the **Select** link is clicked and displays a list of courses taught by the selected instructor .</span></span>

<span data-ttu-id="8a702-120">*講師*の**ErrorMessageLabel** `Label` コントロールの直後に、次のマークアップを追加します。</span><span class="sxs-lookup"><span data-stu-id="8a702-120">In *Instructors.aspx*, add the following markup immediately after the **ErrorMessageLabel** `Label` control:</span></span>

[!code-aspx[Main](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/samples/sample1.aspx)]

<span data-ttu-id="8a702-121">ページを実行し、インストラクターを選択します。</span><span class="sxs-lookup"><span data-stu-id="8a702-121">Run the page and select an instructor.</span></span> <span data-ttu-id="8a702-122">インストラクターがトレーニングしたコースの一覧が表示されます。</span><span class="sxs-lookup"><span data-stu-id="8a702-122">You see a list of courses taught by that instructor.</span></span>

<span data-ttu-id="8a702-123">[![Instructors_page_with_courses](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="8a702-123">[![Instructors_page_with_courses](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image3.png)</span></span>

## <a name="deploying-the-code-update-to-the-test-environment"></a><span data-ttu-id="8a702-124">テスト環境へのコード更新の配置</span><span class="sxs-lookup"><span data-stu-id="8a702-124">Deploying the Code Update to the Test Environment</span></span>

<span data-ttu-id="8a702-125">テスト環境への配置は、ワンクリックでの発行をもう一度実行するだけの簡単な方法です。</span><span class="sxs-lookup"><span data-stu-id="8a702-125">Deploying to the test environment is a simple matter of running one-click publish again.</span></span> <span data-ttu-id="8a702-126">この処理をより迅速に行うために、 **Web One の [発行**] ツールバーを使用できます。</span><span class="sxs-lookup"><span data-stu-id="8a702-126">To make this process quicker, you can use the **Web One Click Publish** toolbar.</span></span>

<span data-ttu-id="8a702-127">**[表示]** メニューの **[ツールバー]** をクリックし、[ **Web One] をクリック**します。</span><span class="sxs-lookup"><span data-stu-id="8a702-127">In the **View** menu, choose **Toolbars** and then select **Web One Click Publish**.</span></span>

![Selecting_One_Click_Publish_toolbar](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image5.png)

<span data-ttu-id="8a702-129">**ソリューションエクスプローラー**で、ContosoUniversity プロジェクトを選択します。</span><span class="sxs-lookup"><span data-stu-id="8a702-129">In **Solution Explorer**, select the ContosoUniversity project.</span></span>

<span data-ttu-id="8a702-130">**web で [発行**] ツールバーをクリックし、**テスト**発行プロファイルを選択して、 **[web の発行]** をクリックします (矢印が左と右にあるアイコン)。</span><span class="sxs-lookup"><span data-stu-id="8a702-130">the **Web One Click Publish** toolbar, choose the **Test** publish profile and then click **Publish Web** (the icon with arrows pointing left and right).</span></span>

![Web_One_Click_Publish_toolbar](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image6.png)

<span data-ttu-id="8a702-132">Visual Studio によって更新されたアプリケーションが配置され、ブラウザーが自動的にホームページに表示されます。</span><span class="sxs-lookup"><span data-stu-id="8a702-132">Visual Studio deploys the updated application, and the browser automatically opens to the home page.</span></span> <span data-ttu-id="8a702-133">インストラクターページを実行し、インストラクターを選択して、更新が正常に展開されたことを確認します。</span><span class="sxs-lookup"><span data-stu-id="8a702-133">Run the Instructors page and select an instructor to verify that the update was successfully deployed.</span></span>

<span data-ttu-id="8a702-134">[![Instructors_page_with_courses_Test](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image8.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="8a702-134">[![Instructors_page_with_courses_Test](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image8.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image7.png)</span></span>

<span data-ttu-id="8a702-135">通常は回帰テストも行います (つまり、サイトの他の部分をテストして、新しい変更によって既存の機能が破壊されていないことを確認します)。</span><span class="sxs-lookup"><span data-stu-id="8a702-135">You would normally also do regression testing (that is, test the rest of the site to make sure that the new change didn't break any existing functionality).</span></span> <span data-ttu-id="8a702-136">ただし、このチュートリアルでは、この手順をスキップして、運用環境への更新プログラムの展開に進みます。</span><span class="sxs-lookup"><span data-stu-id="8a702-136">But for this tutorial you'll skip that step and proceed to deploy the update to production.</span></span>

## <a name="preventing-redeployment-of-the-initial-database-state-to-production"></a><span data-ttu-id="8a702-137">初期データベースの状態を運用環境に再展開できないようにする</span><span class="sxs-lookup"><span data-stu-id="8a702-137">Preventing Redeployment of the Initial Database State to Production</span></span>

<span data-ttu-id="8a702-138">実際のアプリケーションでは、初期デプロイ後にユーザーが運用サイトと対話し、データベースにライブデータが入力されます。</span><span class="sxs-lookup"><span data-stu-id="8a702-138">In a real application, users interact with your production site after your initial deployment, and the databases are populated with live data.</span></span> <span data-ttu-id="8a702-139">そのため、メンバーシップデータベースを初期状態で再デプロイする必要はありません。これにより、すべてのライブデータが消去されます。</span><span class="sxs-lookup"><span data-stu-id="8a702-139">Therefore, you don't want to redeploy the membership database in its initial state, which would wipe out all of the live data.</span></span> <span data-ttu-id="8a702-140">SQL Server Compact データベースは*app\_data*フォルダー内のファイルなので、*アプリの\_データ*フォルダー内のファイルが展開されないように配置設定を変更することで、これを回避する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8a702-140">Since SQL Server Compact databases are files in the *App\_Data* folder, you have to prevent this by changing deployment settings so that files in the *App\_Data* folder aren't deployed.</span></span>

<span data-ttu-id="8a702-141">ContosoUniversity プロジェクトの**プロジェクトプロパティ**ウィンドウを開き、 **[パッケージ化/発行]** タブを選択します。 **[構成]** ドロップダウンボックスに **[アクティブ (リリース)]** または **[リリース]** が選択されていることを確認し、[**アプリ\_データフォルダーからファイルを除外**する] を選択します。</span><span class="sxs-lookup"><span data-stu-id="8a702-141">Open the **Project Properties** window for the ContosoUniversity project, and select the **Package/Publish Web** tab. Make sure that the **Configuration** drop-down box has either **Active (Release)** or **Release** selected, select **Exclude files from the App\_Data folder**.</span></span>

![Exclude_files_from_the_App_Data_folder](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image9.png)

<span data-ttu-id="8a702-143">デバッグビルドを後で配置する場合は、デバッグビルド構成に対して同じ変更を行うことをお勧めします。 **[構成]** を **[デバッグ]** に変更し、[**アプリ\_データフォルダーからファイルを除外**する] を選択します。</span><span class="sxs-lookup"><span data-stu-id="8a702-143">In case you decide to deploy a debug build in the future, it's a good idea to make the same change for the Debug build configuration: change **Configuration** to **Debug** and then select **Exclude files from the App\_Data folder**.</span></span>

<span data-ttu-id="8a702-144">**[パッケージ/発行 Web]** タブを保存して閉じます。</span><span class="sxs-lookup"><span data-stu-id="8a702-144">Save and close the **Package/Publish Web** tab.</span></span>

> [!NOTE] 
> 
> [!IMPORTANT]
> <span data-ttu-id="8a702-145">発行プロファイルで **ターゲットに追加ファイルを削除**しない。</span><span class="sxs-lookup"><span data-stu-id="8a702-145">Make sure that you don't have **Remove additional files at destination** selected in your publish profiles.</span></span> <span data-ttu-id="8a702-146">このオプションを選択すると、展開プロセスによって、展開されたサイトの [アプリ\_データ] にあるデータベースが削除され、アプリ\_データフォルダー自体が削除されます。</span><span class="sxs-lookup"><span data-stu-id="8a702-146">If you select that option, the deployment process will delete the databases that you have in App\_Data in the deployed site, and it will delete the App\_Data folder itself.</span></span>

## <a name="preventing-user-access-to-the-production-site-during-update"></a><span data-ttu-id="8a702-147">更新中に運用サイトへのユーザーアクセスを防止する</span><span class="sxs-lookup"><span data-stu-id="8a702-147">Preventing User Access to the Production Site During Update</span></span>

<span data-ttu-id="8a702-148">ここでデプロイしている変更は、1つのページに単純に変更されます。</span><span class="sxs-lookup"><span data-stu-id="8a702-148">The change you're deploying now is a simple change to a single page.</span></span> <span data-ttu-id="8a702-149">ただし、展開が完了する前にユーザーがページを要求すると、サイトの動作が変更される場合があります。</span><span class="sxs-lookup"><span data-stu-id="8a702-149">But sometimes you deploy larger changes, and in that case the site can behave strangely if a user requests a page before deployment is finished.</span></span> <span data-ttu-id="8a702-150">これを回避するには、*アプリ\_のオフライン .htm*ファイルを使用します。</span><span class="sxs-lookup"><span data-stu-id="8a702-150">To prevent this, you can use an *app\_offline.htm* file.</span></span> <span data-ttu-id="8a702-151">アプリケーションのルートフォルダーに*app\_offline .htm*という名前のファイルを配置すると、アプリケーションを実行する代わりに IIS によってそのファイルが自動的に表示されます。</span><span class="sxs-lookup"><span data-stu-id="8a702-151">When you put a file named *app\_offline.htm* in the root folder of your application, IIS automatically displays that file instead of running your application.</span></span> <span data-ttu-id="8a702-152">そのため、デプロイ中にアクセスできないようにするには、*アプリ\_offline .htm*をルートフォルダーに配置し、展開プロセスを実行してから、 *app\_offline. .htm*を削除します。</span><span class="sxs-lookup"><span data-stu-id="8a702-152">So to prevent access during deployment, you put *app\_offline.htm* in the root folder, run the deployment process, and then remove *app\_offline.htm*.</span></span>

<span data-ttu-id="8a702-153">**ソリューションエクスプローラー**で、(プロジェクトの1つではなく) ソリューションを右クリックし、 **[新しいソリューションフォルダー]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="8a702-153">In **Solution Explorer**, right-click the solution (not one of the projects) and select **New Solution Folder**.</span></span>

![Creating_a_solution_folder](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image10.png)

<span data-ttu-id="8a702-155">フォルダーに「 *Solutionfiles*」という名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="8a702-155">Name the folder *SolutionFiles*.</span></span>

<span data-ttu-id="8a702-156">新しいフォルダーで、 *app\_offline. .htm*という名前の HTML ページを作成します。</span><span class="sxs-lookup"><span data-stu-id="8a702-156">In the new folder create an HTML page named *app\_offline.htm*.</span></span> <span data-ttu-id="8a702-157">既存の内容を次のマークアップに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="8a702-157">Replace the existing contents with the following markup:</span></span>

[!code-html[Main](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/samples/sample2.html)]

<span data-ttu-id="8a702-158">FTP 接続またはホスティングプロバイダーのコントロールパネルにある**ファイルマネージャー**ユーティリティを使用して、*アプリケーション\_offline .htm*ファイルをサイトにコピーできます。</span><span class="sxs-lookup"><span data-stu-id="8a702-158">You can copy the *app\_offline.htm* file to the site by using an FTP connection or the **File Manager** utility in the hosting provider's control panel.</span></span> <span data-ttu-id="8a702-159">このチュートリアルでは、**ファイルマネージャー**を使用します。</span><span class="sxs-lookup"><span data-stu-id="8a702-159">For this tutorial, you'll use the **File Manager**.</span></span>

<span data-ttu-id="8a702-160">コントロールパネルを開き、「[運用環境にデプロイする](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)」チュートリアルで行ったように **[ファイルマネージャー]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="8a702-160">Open the control panel and select **File Manager** as you did in the [Deploying to the Production Environment](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) tutorial.</span></span> <span data-ttu-id="8a702-161">アプリケーションのルートフォルダーを取得するには、 **[contosouniversity.com]** 、 **[wwwroot]** の順に選択し、 **[アップロード]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8a702-161">Select **contosouniversity.com** and then **wwwroot** to get to your application's root folder, and then click **Upload**.</span></span>

<span data-ttu-id="8a702-162">[![Upload_button_in_File_Manager](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image12.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="8a702-162">[![Upload_button_in_File_Manager](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image12.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image11.png)</span></span>

<span data-ttu-id="8a702-163">**[ファイルのアップロード]** ダイアログボックスで、*アプリ\_offline .htm*ファイルを選択し、 **[アップロード]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8a702-163">In the **Upload File** dialog box, select the *app\_offline.htm* file and then click **Upload**.</span></span>

<span data-ttu-id="8a702-164">[![Upload_dialog_box_in_File_Manager](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image14.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="8a702-164">[![Upload_dialog_box_in_File_Manager](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image14.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image13.png)</span></span>

<span data-ttu-id="8a702-165">目的のサイトの URL に移動します。</span><span class="sxs-lookup"><span data-stu-id="8a702-165">Browse to your site's URL.</span></span> <span data-ttu-id="8a702-166">ホームページの代わりに、*アプリ\_offline .htm*ページが表示されるようになります。</span><span class="sxs-lookup"><span data-stu-id="8a702-166">You see that the *app\_offline.htm* page is now displayed instead of your home page.</span></span>

<span data-ttu-id="8a702-167">[![App_offline。 htm_page_in_production](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image16.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="8a702-167">[![App_offline.htm_page_in_production](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image16.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image15.png)</span></span>

<span data-ttu-id="8a702-168">これで、運用環境にデプロイする準備ができました。</span><span class="sxs-lookup"><span data-stu-id="8a702-168">You are now ready to deploy to production.</span></span>

## <a name="deploying-the-code-update-to-the-production-environment"></a><span data-ttu-id="8a702-169">運用環境へのコード更新の配置</span><span class="sxs-lookup"><span data-stu-id="8a702-169">Deploying the Code Update to the Production Environment</span></span>

<span data-ttu-id="8a702-170">Web 上の **[発行**] ツールバーで、 **[実稼働]** 発行プロファイル を選択し、 **[web の発行]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8a702-170">In the **Web One Click Publish** toolbar, choose the **Production** publish profile and then click **Publish Web**.</span></span>

<span data-ttu-id="8a702-171">更新されたアプリケーションが Visual Studio によって展開され、ブラウザーが開き、サイトのホームページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="8a702-171">Visual Studio deploys the updated application and opens the browser to the site's home page.</span></span> <span data-ttu-id="8a702-172">*アプリ\_のオフライン .htm*ファイルが表示されます。</span><span class="sxs-lookup"><span data-stu-id="8a702-172">The *app\_offline.htm* file is displayed.</span></span> <span data-ttu-id="8a702-173">展開が成功したことを確認するためにテストする前に、*アプリ\_のオフライン .htm*ファイルを削除する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8a702-173">Before you can test to verify successful deployment, you must remove the *app\_offline.htm* file.</span></span>

<span data-ttu-id="8a702-174">コントロールパネルの **[ファイルマネージャー]** アプリケーションに戻ります。</span><span class="sxs-lookup"><span data-stu-id="8a702-174">Return to the **File Manager** application in the control panel.</span></span> <span data-ttu-id="8a702-175">**Contosouniversity.com**と**wwwroot**を選択し、[ **app\_offline .htm**] を選択して、 **[削除]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8a702-175">Select **contosouniversity.com** and **wwwroot**, select **app\_offline.htm**, and then click **Delete**.</span></span>

<span data-ttu-id="8a702-176">[![Deleting_app_offline .htm](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image18.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="8a702-176">[![Deleting_app_offline.htm](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image18.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image17.png)</span></span>

<span data-ttu-id="8a702-177">ブラウザーで、パブリックサイトの [インストラクター] ページを開き、更新プログラムが正常に展開されたことを確認するインストラクターを選択します。</span><span class="sxs-lookup"><span data-stu-id="8a702-177">In the browser, open the Instructors page in the public site, and select an instructor to verify that the update was successfully deployed.</span></span>

<span data-ttu-id="8a702-178">[![Instructors_page_with_courses_Prod](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image20.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image19.png)</span><span class="sxs-lookup"><span data-stu-id="8a702-178">[![Instructors_page_with_courses_Prod](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image20.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image19.png)</span></span>

<span data-ttu-id="8a702-179">これで、データベースの変更が含まれていないアプリケーションの更新プログラムが展開されました。</span><span class="sxs-lookup"><span data-stu-id="8a702-179">You've now deployed an application update that did not involve a database change.</span></span> <span data-ttu-id="8a702-180">次のチュートリアルでは、データベースの変更を配置する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="8a702-180">The next tutorial shows you how to deploy a database change.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="8a702-181">[前へ](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)
> [次へ](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md)</span><span class="sxs-lookup"><span data-stu-id="8a702-181">[Previous](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)
[Next](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md)</span></span>
