---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/setting-up-the-contact-manager-solution
title: Contact Manager ソリューションを設定する |Microsoft Docs
author: jrjlee
description: このトピックでは、Contact Manager ソリューションをダウンロードし、開発者のワークステーションでローカルに実行するように構成する方法について説明します。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 200b973c-776b-4a9b-9e82-39fda6120a52
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/setting-up-the-contact-manager-solution
msc.type: authoredcontent
ms.openlocfilehash: d9774ee01cb0515d7e733b24baa661f2648bd7c4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78511162"
---
# <a name="setting-up-the-contact-manager-solution"></a><span data-ttu-id="c5010-103">連絡先マネージャー ソリューションを設定する</span><span class="sxs-lookup"><span data-stu-id="c5010-103">Setting Up the Contact Manager Solution</span></span>

<span data-ttu-id="c5010-104">[Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="c5010-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

<span data-ttu-id="c5010-105">[[Download PDF]\(PDF をダウンロード\)](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)</span><span class="sxs-lookup"><span data-stu-id="c5010-105">[Download PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)</span></span>

> <span data-ttu-id="c5010-106">このトピックでは、Contact Manager ソリューションをダウンロードし、開発者のワークステーションでローカルに実行するように構成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="c5010-106">This topic describes how to download and configure the Contact Manager solution to run locally on a developer workstation.</span></span>

## <a name="system-requirements"></a><span data-ttu-id="c5010-107">システム要件</span><span class="sxs-lookup"><span data-stu-id="c5010-107">System Requirements</span></span>

<span data-ttu-id="c5010-108">Contact Manager ソリューションをローカルで実行し、このチュートリアルで説明されている他のタスクを実行するには、このソフトウェアを developer ワークステーションにインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="c5010-108">To run the Contact Manager solution locally and to perform the other tasks described in this tutorial, you'll need to install this software on your developer workstation:</span></span>

- <span data-ttu-id="c5010-109">Visual Studio 2010 Service Pack 1、Premium、または Ultimate Edition</span><span class="sxs-lookup"><span data-stu-id="c5010-109">Visual Studio 2010 Service Pack 1, Premium or Ultimate Edition</span></span>
- <span data-ttu-id="c5010-110">インターネット インフォメーション サービス (IIS) 7.5 Express</span><span class="sxs-lookup"><span data-stu-id="c5010-110">Internet Information Services (IIS) 7.5 Express</span></span>
- <span data-ttu-id="c5010-111">SQL Server Express 2008 R2</span><span class="sxs-lookup"><span data-stu-id="c5010-111">SQL Server Express 2008 R2</span></span>
- <span data-ttu-id="c5010-112">IIS Web 配置ツール (Web 配置) 2.1 以降</span><span class="sxs-lookup"><span data-stu-id="c5010-112">IIS Web Deployment Tool (Web Deploy) 2.1 or later</span></span>
- <span data-ttu-id="c5010-113">ASP.NET 4.0</span><span class="sxs-lookup"><span data-stu-id="c5010-113">ASP.NET 4.0</span></span>
- <span data-ttu-id="c5010-114">ASP.NET MVC 3</span><span class="sxs-lookup"><span data-stu-id="c5010-114">ASP.NET MVC 3</span></span>
- <span data-ttu-id="c5010-115">.NET Framework 4</span><span class="sxs-lookup"><span data-stu-id="c5010-115">.NET Framework 4</span></span>
- <span data-ttu-id="c5010-116">.NET Framework 3.5 SP1</span><span class="sxs-lookup"><span data-stu-id="c5010-116">.NET Framework 3.5 SP1</span></span>

<span data-ttu-id="c5010-117">Visual Studio 2010 を除き、 [Web Platform Installer](https://go.microsoft.com/?linkid=9805118)を使用して、これらの製品とコンポーネントの最新バージョンをダウンロードしてインストールすることができます。</span><span class="sxs-lookup"><span data-stu-id="c5010-117">With the exception of Visual Studio 2010, you can download and install the latest versions of all of these products and components through the [Web Platform Installer](https://go.microsoft.com/?linkid=9805118).</span></span>

## <a name="download-and-extract-the-solution"></a><span data-ttu-id="c5010-118">ソリューションのダウンロードと抽出</span><span class="sxs-lookup"><span data-stu-id="c5010-118">Download and Extract the Solution</span></span>

<span data-ttu-id="c5010-119">Contact Manager サンプル[アプリケーションは、MSDN コードギャラリーから](https://code.msdn.microsoft.com/Deploying-Web-Applications-9d9093c0)ダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="c5010-119">You can download the Contact Manager sample application from the MSDN Code Gallery [here](https://code.msdn.microsoft.com/Deploying-Web-Applications-9d9093c0).</span></span>

## <a name="configure-and-run-the-solution"></a><span data-ttu-id="c5010-120">ソリューションを構成して実行する</span><span class="sxs-lookup"><span data-stu-id="c5010-120">Configure and Run the Solution</span></span>

<span data-ttu-id="c5010-121">ローカルコンピューターで Contact Manager ソリューションを構成して実行するには、次の大まかな手順を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c5010-121">To configure and run the Contact Manager solution on your local machine, you'll need to perform these high-level steps:</span></span>

1. <span data-ttu-id="c5010-122">まだ持っていない場合は、メンバーシップとロールの管理機能が有効になっているローカルの ASP.NET アプリケーションサービスデータベースを作成します。</span><span class="sxs-lookup"><span data-stu-id="c5010-122">If you don't have one already, create a local ASP.NET application services database with the membership and role management features enabled.</span></span>
2. <span data-ttu-id="c5010-123">ローカル SQL Server Express インスタンスを指すように、web.config ファイル内の接続文字列を編集*します。*</span><span class="sxs-lookup"><span data-stu-id="c5010-123">Edit connection strings in the *web.config* files to point to your local SQL Server Express instance.</span></span>
3. <span data-ttu-id="c5010-124">Visual Studio 2010 からソリューションを実行します。</span><span class="sxs-lookup"><span data-stu-id="c5010-124">Run the solution from Visual Studio 2010.</span></span>

<span data-ttu-id="c5010-125">このセクションの残りの部分では、これらの各タスクを実行する方法について詳しく説明します。</span><span class="sxs-lookup"><span data-stu-id="c5010-125">The remainder of this section provides more guidance on how to complete each of these tasks.</span></span>

<span data-ttu-id="c5010-126">**アプリケーションサービスデータベースを作成するには**</span><span class="sxs-lookup"><span data-stu-id="c5010-126">**To create the application services database**</span></span>

1. <span data-ttu-id="c5010-127">Visual Studio 2010 コマンド プロンプトを開きます。</span><span class="sxs-lookup"><span data-stu-id="c5010-127">Open a Visual Studio 2010 command prompt.</span></span> <span data-ttu-id="c5010-128">これを行うには、 **[スタート]** ボタンをクリックし、 **[すべてのプログラム]** をポイントし、 **[Microsoft Visual Studio 2010]** をクリックし、 **[Visual Studio Tools]** をクリックして、 **[Visual Studio コマンドプロンプト (2010)]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c5010-128">To do this, on the **Start** menu, point to **All Programs**, click **Microsoft Visual Studio 2010**, click **Visual Studio Tools**, and then click **Visual Studio Command Prompt (2010)**.</span></span>
2. <span data-ttu-id="c5010-129">コマンドプロンプトで、次のコマンドを入力し、enter キーを押します。</span><span class="sxs-lookup"><span data-stu-id="c5010-129">At the command prompt, type this command, and then press Enter:</span></span>

    [!code-console[Main](setting-up-the-contact-manager-solution/samples/sample1.cmd)]

    1. <span data-ttu-id="c5010-130">**– C**スイッチを使用して、データベースサーバーの接続文字列を指定します。</span><span class="sxs-lookup"><span data-stu-id="c5010-130">Use the **–C** switch to specify the connection string for your database server.</span></span>
    2. <span data-ttu-id="c5010-131">**– A**スイッチを使用して、データベースに追加するアプリケーションサービスの機能を指定します。</span><span class="sxs-lookup"><span data-stu-id="c5010-131">Use the **–A** switch to specify the application services features you want to add to the database.</span></span> <span data-ttu-id="c5010-132">この場合、 **m**はメンバーシッププロバイダーのサポートを追加することを示し、 **r**はロールマネージャーのサポートを追加することを示します。</span><span class="sxs-lookup"><span data-stu-id="c5010-132">In this case, **m** indicates that you want to add support for the membership provider and **r** indicates that you want to add support for the role manager.</span></span>
    3. <span data-ttu-id="c5010-133">アプリケーションサービスデータベースの名前を指定するには、 **– d**スイッチを使用します。</span><span class="sxs-lookup"><span data-stu-id="c5010-133">Use the **–d** switch to specify a name for your application services database.</span></span> <span data-ttu-id="c5010-134">このスイッチを省略すると、既定の名前が**aspnetdb.mdf**のデータベースが作成されます。</span><span class="sxs-lookup"><span data-stu-id="c5010-134">If you omit this switch, the utility will create a database with the default name of **aspnetdb**.</span></span>
3. <span data-ttu-id="c5010-135">データベースが正常に作成されると、コマンドプロンプトに確認メッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="c5010-135">When the database has been created successfully, the command prompt will show a confirmation.</span></span>

    ![](setting-up-the-contact-manager-solution/_static/image1.png)

> [!NOTE]
> <span data-ttu-id="c5010-136">Aspnet\_regsql ユーティリティの詳細については、「 [ASP.NET SQL Server Registration Tool (aspnet\_regsql .exe)](https://msdn.microsoft.com/library/ms229862(v=vs.100).aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c5010-136">For more information on the aspnet\_regsql utility, see [ASP.NET SQL Server Registration Tool (Aspnet\_regsql.exe)](https://msdn.microsoft.com/library/ms229862(v=vs.100).aspx).</span></span>

<span data-ttu-id="c5010-137">次の手順では、Contact Manager ソリューション内の接続文字列が SQL Server Express のローカルインスタンスを指していることを確認します。</span><span class="sxs-lookup"><span data-stu-id="c5010-137">The next step is to make sure that the connection strings in the Contact Manager solution point to your local instance of SQL Server Express.</span></span>

<span data-ttu-id="c5010-138">**接続文字列を更新するには**</span><span class="sxs-lookup"><span data-stu-id="c5010-138">**To update the connection strings**</span></span>

1. <span data-ttu-id="c5010-139">Visual Studio 2010 で Contact Manager ソリューションを開きます。</span><span class="sxs-lookup"><span data-stu-id="c5010-139">Open the Contact Manager solution in Visual Studio 2010.</span></span>
2. <span data-ttu-id="c5010-140">**[ソリューションエクスプローラー]** ウィンドウで、 **[Contactmanager. Mvc]** プロジェクトを展開し、 **[web.config]** ノードをダブルクリックします。</span><span class="sxs-lookup"><span data-stu-id="c5010-140">In the **Solution Explorer** window, expand the **ContactManager.Mvc** project, and then double-click the **Web.config** node.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c5010-141">ContactManager Mvc プロジェクトには *、2つの web.config ファイル*が含まれています。</span><span class="sxs-lookup"><span data-stu-id="c5010-141">The ContactManager.Mvc project includes two *web.config* files.</span></span> <span data-ttu-id="c5010-142">プロジェクトレベルのファイルを編集する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c5010-142">You need to edit the project-level file.</span></span>

    ![](setting-up-the-contact-manager-solution/_static/image2.png)
3. <span data-ttu-id="c5010-143">**ConnectionStrings**要素で、 **applicationservices**という名前の接続文字列がローカルの ASP.NET アプリケーションサービスデータベースを指していることを確認します。</span><span class="sxs-lookup"><span data-stu-id="c5010-143">In the **connectionStrings** element, verify that the connection string named **ApplicationServices** points to your local ASP.NET application services database.</span></span>

    [!code-xml[Main](setting-up-the-contact-manager-solution/samples/sample2.xml)]
4. <span data-ttu-id="c5010-144">**[ソリューションエクスプローラー]** ウィンドウで、 **[Contactmanager. サービス]** プロジェクトを展開し、 **[web.config]** ノードをダブルクリックします。</span><span class="sxs-lookup"><span data-stu-id="c5010-144">In the **Solution Explorer** window, expand the **ContactManager.Service** project, and then double-click the **Web.config** node.</span></span>

    ![](setting-up-the-contact-manager-solution/_static/image3.png)
5. <span data-ttu-id="c5010-145">**ConnectionStrings**要素の**contactmanagercontext**という名前の接続文字列で、**データソース**プロパティが SQL Server Express のローカルインスタンスに設定されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="c5010-145">In the **connectionStrings** element, in the connection string named **ContactManagerContext**, verify that the **Data Source** property is set to your local instance of SQL Server Express.</span></span> <span data-ttu-id="c5010-146">接続文字列内の他のものを変更する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="c5010-146">You don't need to change anything else in the connection string.</span></span>

    [!code-xml[Main](setting-up-the-contact-manager-solution/samples/sample3.xml)]
6. <span data-ttu-id="c5010-147">開いているすべてのファイルを保存します。</span><span class="sxs-lookup"><span data-stu-id="c5010-147">Save all open files.</span></span>

<span data-ttu-id="c5010-148">これで、ローカルコンピューターで Contact Manager ソリューションを実行する準備が整いました。</span><span class="sxs-lookup"><span data-stu-id="c5010-148">You should now be ready to run the Contact Manager solution on your local machine.</span></span>

> [!NOTE]
> <span data-ttu-id="c5010-149">最初にアプリケーションサービスデータベースを作成せずにこれらの手順を実行すると、ASP.NET によって初めてユーザーを作成しようとしたときにデータベースが作成されます。</span><span class="sxs-lookup"><span data-stu-id="c5010-149">If you follow these steps without first creating an application services database, ASP.NET will create the database the first time you attempt to create a user.</span></span> <span data-ttu-id="c5010-150">ただし、データベースを手動で作成すると、サポートするアプリケーションサービスの機能セットをはるかに細かく制御できます。</span><span class="sxs-lookup"><span data-stu-id="c5010-150">However, manually creating the database gives you a lot more control over the application services feature set you want to support.</span></span>

<span data-ttu-id="c5010-151">**Contact Manager ソリューションを実行するには**</span><span class="sxs-lookup"><span data-stu-id="c5010-151">**To run the Contact Manager solution**</span></span>

1. <span data-ttu-id="c5010-152">Visual Studio 2010 で、F5 キーを押します。</span><span class="sxs-lookup"><span data-stu-id="c5010-152">In Visual Studio 2010, press F5.</span></span>
2. <span data-ttu-id="c5010-153">Internet Explorer が起動し、Contact Manager ASP.NET MVC 3 アプリケーションの URL が要求されます。</span><span class="sxs-lookup"><span data-stu-id="c5010-153">Internet Explorer starts up and requests the URL of the Contact Manager ASP.NET MVC 3 application.</span></span> <span data-ttu-id="c5010-154">既定では、アプリケーションは **[すべての連絡先]** ページを表示します。</span><span class="sxs-lookup"><span data-stu-id="c5010-154">By default, the application displays the **All Contacts** page.</span></span>

    ![](setting-up-the-contact-manager-solution/_static/image4.png)
3. <span data-ttu-id="c5010-155">いくつかの連絡先を追加し、アプリケーションが期待どおりに動作することを確認します。</span><span class="sxs-lookup"><span data-stu-id="c5010-155">Add a few contacts, and then verify that the application works as expected.</span></span>

    ![](setting-up-the-contact-manager-solution/_static/image5.png)
4. <span data-ttu-id="c5010-156">`http://localhost:50114/Account/Register` を参照します (別のポートでアプリケーションをホストしている場合は、URL を調整します)。</span><span class="sxs-lookup"><span data-stu-id="c5010-156">Browse to `http://localhost:50114/Account/Register` (adjust the URL if you're hosting the application on a different port).</span></span> <span data-ttu-id="c5010-157">ユーザー名、電子メールアドレス、およびパスワードを追加し、アカウントを正常に登録できることを確認します。</span><span class="sxs-lookup"><span data-stu-id="c5010-157">Add a user name, email address, and password, and verify that you're able to register an account successfully.</span></span>

    ![](setting-up-the-contact-manager-solution/_static/image6.png)
5. <span data-ttu-id="c5010-158">`http://localhost:50114/Account/LogOn` を参照します (別のポートでアプリケーションをホストしている場合は、URL を調整します)。</span><span class="sxs-lookup"><span data-stu-id="c5010-158">Browse to `http://localhost:50114/Account/LogOn` (adjust the URL if you're hosting the application on a different port).</span></span> <span data-ttu-id="c5010-159">先ほど作成したアカウントを使用してログオンできることを確認します。</span><span class="sxs-lookup"><span data-stu-id="c5010-159">Verify that you're able to log on using the account you just created.</span></span>

    ![](setting-up-the-contact-manager-solution/_static/image7.png)
6. <span data-ttu-id="c5010-160">Internet Explorer を閉じて、デバッグを停止します。</span><span class="sxs-lookup"><span data-stu-id="c5010-160">Close Internet Explorer to stop debugging.</span></span>

## <a name="conclusion"></a><span data-ttu-id="c5010-161">まとめ</span><span class="sxs-lookup"><span data-stu-id="c5010-161">Conclusion</span></span>

<span data-ttu-id="c5010-162">この時点で、Contact Manager ソリューションはローカルコンピューターで実行するように完全に構成されている必要があります。</span><span class="sxs-lookup"><span data-stu-id="c5010-162">At this point, the Contact Manager solution should be fully configured to run on your local machine.</span></span> <span data-ttu-id="c5010-163">このチュートリアルの他のトピックを使用して作業する場合は、このソリューションを参照として使用できます。</span><span class="sxs-lookup"><span data-stu-id="c5010-163">You can use the solution as a reference when you work through the other topics in this tutorial.</span></span>

<span data-ttu-id="c5010-164">次のトピック「[プロジェクトファイルについ](understanding-the-project-file.md)て」では、Contact Manager ソリューション内でカスタム Microsoft Build Engine (MSBuild) プロジェクトファイルを使用して、デプロイプロセスを制御する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="c5010-164">The next topic, [Understanding the Project File](understanding-the-project-file.md), explains how you can use the custom Microsoft Build Engine (MSBuild) project files within the Contact Manager solution to control the deployment process.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c5010-165">[前へ](the-contact-manager-solution.md)
> [次へ](understanding-the-project-file.md)</span><span class="sxs-lookup"><span data-stu-id="c5010-165">[Previous](the-contact-manager-solution.md)
[Next](understanding-the-project-file.md)</span></span>
