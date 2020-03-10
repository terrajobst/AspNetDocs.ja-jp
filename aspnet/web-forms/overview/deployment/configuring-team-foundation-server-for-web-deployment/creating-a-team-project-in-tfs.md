---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/creating-a-team-project-in-tfs
title: TFS でのチームプロジェクトの作成 |Microsoft Docs
author: jrjlee
description: このトピックでは、Team Foundation Server (TFS) 2010 で新しいチームプロジェクトを作成する方法について説明します。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: b28d3e2d-0bb4-4e29-a780-af810b964722
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/creating-a-team-project-in-tfs
msc.type: authoredcontent
ms.openlocfilehash: d12e0636ce3b6239d125305db4354278f9f24960
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78519562"
---
# <a name="creating-a-team-project-in-tfs"></a><span data-ttu-id="8d1fa-103">TFS でチーム プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="8d1fa-103">Creating a Team Project in TFS</span></span>

<span data-ttu-id="8d1fa-104">[Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="8d1fa-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

<span data-ttu-id="8d1fa-105">[[Download PDF]\(PDF をダウンロード\)](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)</span><span class="sxs-lookup"><span data-stu-id="8d1fa-105">[Download PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)</span></span>

> <span data-ttu-id="8d1fa-106">このトピックでは、Team Foundation Server (TFS) 2010 で新しいチームプロジェクトを作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-106">This topic describes how to create a new team project in Team Foundation Server (TFS) 2010.</span></span>

<span data-ttu-id="8d1fa-107">このトピックでは、Fabrikam, Inc. という架空の企業のエンタープライズ展開要件に基づいて、一連のチュートリアルの一部を説明します。このチュートリアルシリーズでは、&#x2014; [Contact Manager ソリューション](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;のサンプルソリューションを使用して、ASP.NET MVC 3 アプリケーション、Windows Communication Foundation (WCF) サービス、データベースプロジェクトなど、現実的なレベルの複雑さを持つ web アプリケーションを表します。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-107">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

## <a name="task-overview"></a><span data-ttu-id="8d1fa-108">タスクの概要</span><span class="sxs-lookup"><span data-stu-id="8d1fa-108">Task Overview</span></span>

<span data-ttu-id="8d1fa-109">TFS で新しいチームプロジェクトをプロビジョニングして使用するには、次の大まかな手順を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-109">To provision and use a new team project in TFS, you'll need to complete these high-level steps:</span></span>

- <span data-ttu-id="8d1fa-110">新しいチームプロジェクトを作成するユーザーにアクセス許可を付与します。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-110">Grant permissions to the user who will create the new team project.</span></span>
- <span data-ttu-id="8d1fa-111">チームプロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-111">Create the team project.</span></span>
- <span data-ttu-id="8d1fa-112">プロジェクトで作業するチームメンバーにアクセス許可を付与します。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-112">Grant permissions to the team members who will work on the project.</span></span>
- <span data-ttu-id="8d1fa-113">一部のコンテンツをチェックインします。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-113">Check in some content.</span></span>

<span data-ttu-id="8d1fa-114">このトピックでは、これらの手順を実行する方法について説明します。また、各手順の責任を負う可能性のあるユーザーとジョブの役割を示します。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-114">This topic will show you how to perform these procedures, and it will identify the users and job roles that are likely to be responsible for each procedure.</span></span> <span data-ttu-id="8d1fa-115">組織の構造によっては、これらの各タスクが別のユーザーの責任であることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-115">Be aware that, depending on the structure of your organization, each of these tasks may be the responsibility of a different person.</span></span>

<span data-ttu-id="8d1fa-116">このトピックのタスクとチュートリアルでは、TFS をインストールして構成したこと、および構成プロセスの一環としてチームプロジェクトコレクションを作成したことを前提としています。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-116">The tasks and walkthroughs in this topic assume that you've installed and configured TFS, and that you've created a team project collection as part of the configuration process.</span></span> <span data-ttu-id="8d1fa-117">これらの前提の詳細と、シナリオに関する一般的な背景情報については、「 [Configure a TFS Build Server For Web Deployment](configuring-a-tfs-build-server-for-web-deployment.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-117">For more information on these assumptions, and for more general background information on the scenario, see [Configure a TFS Build Server for Web Deployment](configuring-a-tfs-build-server-for-web-deployment.md).</span></span>

## <a name="grant-permissions-to-the-team-project-creator"></a><span data-ttu-id="8d1fa-118">チームプロジェクト作成者にアクセス許可を付与する</span><span class="sxs-lookup"><span data-stu-id="8d1fa-118">Grant Permissions to the Team Project Creator</span></span>

<span data-ttu-id="8d1fa-119">新しいチームプロジェクトを作成するには、次のアクセス許可が必要です。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-119">In order to create a new team project, you need these permissions:</span></span>

- <span data-ttu-id="8d1fa-120">TFS アプリケーション層に対する "**新しいプロジェクトの作成**" アクセス許可が必要です。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-120">You must have the **Create new projects** permission on the TFS application tier.</span></span> <span data-ttu-id="8d1fa-121">通常、このアクセス許可を付与するには、**プロジェクトコレクション管理者**TFS グループにユーザーを追加します。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-121">You typically grant this permission by adding users to the **Project Collection Administrators** TFS group.</span></span> <span data-ttu-id="8d1fa-122">**Team Foundation 管理者**グローバルグループには、このアクセス許可も含まれています。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-122">The **Team Foundation Administrators** global group also includes this permission.</span></span>
- <span data-ttu-id="8d1fa-123">TFS チームプロジェクトコレクションに対応する SharePoint サイトコレクション内に新しいチームサイトを作成するためのアクセス許可が必要です。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-123">You must have permission to create new team sites within the SharePoint site collection that corresponds to the TFS team project collection.</span></span> <span data-ttu-id="8d1fa-124">通常、このアクセス許可を付与するには、SharePoint サイトコレクションに対する**フルコントロール**権限を持つ sharepoint グループにユーザーを追加します。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-124">You typically grant this permission by adding the user to a SharePoint group with **Full Control** rights on the SharePoint site collection.</span></span>
- <span data-ttu-id="8d1fa-125">SQL Server Reporting Services の機能を使用している場合は、Reporting Services の**Team Foundation コンテンツマネージャー**ロールのメンバーである必要があります。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-125">If you're using SQL Server Reporting Services features, you must be a member of the **Team Foundation Content Manager** role in Reporting Services.</span></span>

### <a name="who-performs-these-procedures"></a><span data-ttu-id="8d1fa-126">これらの手順を実行するユーザー</span><span class="sxs-lookup"><span data-stu-id="8d1fa-126">Who Performs These Procedures?</span></span>

<span data-ttu-id="8d1fa-127">通常、TFS の配置を管理するユーザーまたはグループは、これらの手順も実行します。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-127">Typically, the person or group who administers the TFS deployment also performs these procedures.</span></span>

<span data-ttu-id="8d1fa-128">これはアクセス許可の高い特権セットであるため、通常、新しいチームプロジェクトは、TFS 配置の管理を担当する少数のユーザーによって作成されます。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-128">Because this is a highly privileged set of permissions, new team projects are typically created by a small subset of users with responsibility for administering a TFS deployment.</span></span> <span data-ttu-id="8d1fa-129">通常、開発者には、新しいチームプロジェクトを作成するために必要なアクセス許可が付与されません。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-129">Developers will not usually be granted the permissions required to create new team projects.</span></span>

### <a name="grant-permissions-in-tfs"></a><span data-ttu-id="8d1fa-130">TFS でのアクセス許可の付与</span><span class="sxs-lookup"><span data-stu-id="8d1fa-130">Grant Permissions in TFS</span></span>

<span data-ttu-id="8d1fa-131">ユーザーが新しいチームプロジェクトを作成できるようにするには、最初の大まかなタスクとして、チームプロジェクトコレクションの**プロジェクトコレクション管理者**グループにユーザーを追加します。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-131">If you want to enable a user to create new team projects, the first high-level task is to add the user to the **Project Collection Administrators** group for the team project collection.</span></span>

<span data-ttu-id="8d1fa-132">**プロジェクトコレクション管理者グループにユーザーを追加するには**</span><span class="sxs-lookup"><span data-stu-id="8d1fa-132">**To add a user to the Project Collection Administrators group**</span></span>

1. <span data-ttu-id="8d1fa-133">TFS サーバーで、 **[スタート]** メニューの すべての **[プログラム]** をポイントし、 **[Microsoft Team Foundation Server 2010]** をクリックして、 **[Team Foundation 管理コンソール]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-133">On the TFS server, on the **Start** menu, point to **All Programs**, click **Microsoft Team Foundation Server 2010**, and then click **Team Foundation Administration Console**.</span></span>
2. <span data-ttu-id="8d1fa-134">ナビゲーションツリービューで、 **[アプリケーション層]** を展開し、 **[チームプロジェクトコレクション]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-134">In the navigation tree view, expand **Application Tier**, and then click **Team Project Collections**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image1.png)
3. <span data-ttu-id="8d1fa-135">**[チームプロジェクトコレクション]** ウィンドウで、管理するチームプロジェクトコレクションを選択します。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-135">In the **Team Project Collections** pane, select the team project collection you want to manage.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image2.png)
4. <span data-ttu-id="8d1fa-136">**[全般]** タブで、 **[グループメンバーシップ]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-136">On the **General** tab, click **Group Membership**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image3.png)
5. <span data-ttu-id="8d1fa-137">**[グローバルグループ]** ダイアログボックスで、**プロジェクトコレクション管理者**グループを選択し、 **[プロパティ]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-137">In the **Global Groups** dialog box, select the **Project Collection Administrators** group, and then click **Properties**.</span></span>
6. <span data-ttu-id="8d1fa-138">**[Team Foundation Server グループのプロパティ]** ダイアログボックスで、 **[Windows ユーザーまたはグループ]** を選択し、 **[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-138">In the **Team Foundation Server Group Properties** dialog box, select **Windows User or Group**, and then click **Add**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image4.png)
7. <span data-ttu-id="8d1fa-139">**[ユーザー、コンピューター、またはグループの選択]** ダイアログボックスで、新しいチームプロジェクトを作成できるようにするユーザーのユーザー名を入力し、 **[名前の確認]** をクリックして、 **[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-139">In the **Select Users, Computers, or Groups** dialog box, type the user name of the user you want to be able to create new team projects, click **Check Names**, and then click **OK**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image5.png)
8. <span data-ttu-id="8d1fa-140">**[Team Foundation Server グループのプロパティ]** ダイアログボックスで、[ **OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-140">In the **Team Foundation Server Group Properties** dialog box, click **OK**.</span></span>
9. <span data-ttu-id="8d1fa-141">**[グローバルグループ]** ダイアログボックスで、 **[閉じる]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-141">In the **Global Groups** dialog box, click **Close**.</span></span>

### <a name="grant-permissions-in-sharepoint-services"></a><span data-ttu-id="8d1fa-142">SharePoint Services で権限を付与する</span><span class="sxs-lookup"><span data-stu-id="8d1fa-142">Grant Permissions in SharePoint Services</span></span>

<span data-ttu-id="8d1fa-143">次に、TFS チームプロジェクトコレクションに対応する SharePoint サイトコレクションに新しいチームサイトを作成するためのアクセス許可をユーザーに付与する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-143">Next, you need to give the user permission to create new team sites in the SharePoint site collection that corresponds to your TFS team project collection.</span></span>

<span data-ttu-id="8d1fa-144">**SharePoint サイトコレクションに対するフルコントロール権限を付与するには**</span><span class="sxs-lookup"><span data-stu-id="8d1fa-144">**To grant Full Control permissions on the SharePoint site collection**</span></span>

1. <span data-ttu-id="8d1fa-145">Team Foundation Server 管理コンソールの **[チームプロジェクトコレクション]** ページで、管理するチームプロジェクトコレクションを選択します。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-145">In the Team Foundation Server Administration Console, on the **Team Project Collections** page, select the team project collection you want to manage.</span></span>
2. <span data-ttu-id="8d1fa-146">**[SharePoint サイト]** タブで、現在の既定の**サイトの場所**の URL の値を確認します。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-146">On the **SharePoint Site** tab, note the value of the **Current Default Site Location** URL.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image6.png)
3. <span data-ttu-id="8d1fa-147">Internet Explorer を開き、手順2でメモした URL にアクセスします。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-147">Open Internet Explorer, and then go to the URL you noted in step 2.</span></span>

    > [!NOTE]
    > <span data-ttu-id="8d1fa-148">チームプロジェクトコレクションを作成したユーザーとして Windows にログオンしていない場合は、続行するために、このユーザーとして SharePoint にサインインする必要があります。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-148">If you're not logged on to Windows as the user who created the team project collection, you'll need to sign in to SharePoint as this user in order to continue.</span></span>
4. <span data-ttu-id="8d1fa-149">**[サイトの操作]** メニューの **[サイトの設定]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-149">On the **Site Actions** menu, click **Site Settings**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image7.png)
5. <span data-ttu-id="8d1fa-150">**[サイトの設定]** ページの **[ユーザーとアクセス許可]** で、 **[ユーザーとグループ]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-150">On the **Site Settings** page, under **Users and Permissions**, click **People and groups**.</span></span>
6. <span data-ttu-id="8d1fa-151">左側のナビゲーションパネルで、 **[グループ]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-151">In the left navigation panel, click **Groups**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image8.png)
7. <span data-ttu-id="8d1fa-152">**[People And groups: すべてのグループ]** ページで、 **[このサイトのグループをセットアップする]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-152">On the **People and Groups: All Groups** page, click **Set Up Groups for this Site**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image9.png)

   > [!NOTE]
   > <span data-ttu-id="8d1fa-153">2つの HTTP エンコードのバグにより、 <strong>http 404 Not Found</strong>エラーが発生することがあります。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-153">You may receive an <strong>HTTP 404 Not Found</strong> error due to a double HTTP encoding bug.</span></span> <span data-ttu-id="8d1fa-154">このエラーが発生した場合は、URL を次のように置き換えます。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-154">If this occurs, replace the URL with this:</span></span>   
   > <span data-ttu-id="8d1fa-155">`[site_collection_URL]/_layouts/permsetup.aspx`次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-155">`[site_collection_URL]/_layouts/permsetup.aspx` For example:</span></span>  
   > `http://tfs/sites/Fabrikam%20Web%20Projects/_layouts/permsetup.aspx` 
8. <span data-ttu-id="8d1fa-156">**[このサイトのグループの設定]** ページで、 **[所有者]** グループにチームプロジェクトを作成するユーザーを追加し、[ **OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-156">On the **Set Up Groups for this Site** page, add the user who will create team projects to the **Owners** group, and then click **OK**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image10.png)

<span data-ttu-id="8d1fa-157">チームプロジェクトコレクション内でユーザーが新しいチームプロジェクトを作成できるようにする方法の詳細については、「[チームプロジェクトコレクションの管理アクセス許可を設定](https://msdn.microsoft.com/library/dd547204.aspx)する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-157">For more information on enabling users to create new team projects within a team project collection, see [Set Administrator Permissions for Team Project Collections](https://msdn.microsoft.com/library/dd547204.aspx).</span></span>

## <a name="create-a-new-team-project-and-add-users"></a><span data-ttu-id="8d1fa-158">新しいチームプロジェクトを作成してユーザーを追加する</span><span class="sxs-lookup"><span data-stu-id="8d1fa-158">Create a New Team Project and Add Users</span></span>

<span data-ttu-id="8d1fa-159">必要なアクセス許可が得られたら、Visual Studio 2010 の **[チームエクスプローラー]** ウィンドウを使用して、新しいチームプロジェクトを作成できます。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-159">Once you have the necessary permissions, you can use the **Team Explorer** window in Visual Studio 2010 to create a new team project.</span></span> <span data-ttu-id="8d1fa-160">この方法では、必要なすべての情報を収集し、TFS、SharePoint、および SQL Server Reporting Services で必要なタスクを実行するウィザードが提供されます。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-160">This approach provides a wizard that collects all the required information and performs the necessary tasks in TFS, SharePoint, and SQL Server Reporting Services.</span></span> <span data-ttu-id="8d1fa-161">また、新しいチームプロジェクトに対するアクセス許可を開発者チームのメンバーに付与して、コンテンツを追加および変更できるようにする必要もあります。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-161">You'll also need to grant permissions on the new team project to members of the developer team, to enable them to add and modify content.</span></span>

### <a name="who-performs-these-procedures"></a><span data-ttu-id="8d1fa-162">これらの手順を実行するユーザー</span><span class="sxs-lookup"><span data-stu-id="8d1fa-162">Who Performs These Procedures?</span></span>

<span data-ttu-id="8d1fa-163">通常、TFS 管理者または開発者チームリーダーは、これらの手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-163">Usually either a TFS administrator or a developer team leader performs these procedures.</span></span>

### <a name="create-a-new-team-project"></a><span data-ttu-id="8d1fa-164">新しいチームプロジェクトの作成</span><span class="sxs-lookup"><span data-stu-id="8d1fa-164">Create a New Team Project</span></span>

<span data-ttu-id="8d1fa-165">次の手順では、TFS 2010 で新しいチームプロジェクトを作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-165">The next procedure describes how to create a new team project in TFS 2010.</span></span>

<span data-ttu-id="8d1fa-166">**新しいチームプロジェクトを作成するには**</span><span class="sxs-lookup"><span data-stu-id="8d1fa-166">**To create a new team project**</span></span>

1. <span data-ttu-id="8d1fa-167">**[スタート]** ボタンをクリックし、 **[すべてのプログラム]** をポイントします。次に、 **[Microsoft Visual Studio 2010]** をクリックし**Microsoft Visual Studio 2010**を右クリックし、 **[管理者として実行]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-167">On the **Start** menu, point to **All Programs**, click **Microsoft Visual Studio 2010**, right-click **Microsoft Visual Studio 2010**, and then click **Run as administrator**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="8d1fa-168">管理者として Visual Studio 2010 を実行していない場合、新しいチームプロジェクトウィザードは、最後の手順で失敗します。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-168">If you don't run Visual Studio 2010 as an administrator, the New Team Project Wizard will fail on the last step.</span></span>
2. <span data-ttu-id="8d1fa-169">**[ユーザー アカウント制御]** ダイアログ ボックスが表示されたら、 **[はい]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-169">If the **User Account Control** dialog box appears, click **Yes**.</span></span>
3. <span data-ttu-id="8d1fa-170">Visual Studio の **[チーム]** メニューで、[ **Team Foundation Server に接続] を**クリックします。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-170">In Visual Studio, on the **Team** menu, click **Connect to Team Foundation Server**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="8d1fa-171">TFS サーバーへの接続が既に構成されている場合は、手順4-7 を省略できます。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-171">If you have already configured a connection to a TFS server, you can omit steps 4-7.</span></span>
4. <span data-ttu-id="8d1fa-172">**[チームプロジェクトへの接続]** ダイアログボックスで、 **[サーバー]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-172">In the **Connection to Team Project** dialog box, click **Servers**.</span></span>
5. <span data-ttu-id="8d1fa-173">**[Team Foundation Server の追加と削除]** ダイアログボックスで、 **[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-173">In the **Add/Remove Team Foundation Server** dialog box, click **Add**.</span></span>
6. <span data-ttu-id="8d1fa-174">**[Team Foundation Server の追加]** ダイアログボックスで、TFS インスタンスの詳細を指定し、 **[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-174">In the **Add Team Foundation Server** dialog box, provide the details of your TFS instance, and then click **OK**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image11.png)
7. <span data-ttu-id="8d1fa-175">**[Team Foundation Server の追加と削除]** ダイアログボックスで、 **[閉じる]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-175">In the **Add/Remove Team Foundation Server** dialog box, click **Close**.</span></span>
8. <span data-ttu-id="8d1fa-176">**[チームプロジェクトへの接続]** ダイアログボックスで、接続先の TFS インスタンスを選択し、追加するチームプロジェクトコレクションを選択して、 **[接続]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-176">In the **Connect to Team Project** dialog box, select the TFS instance you want to connect to, select the team project collection you want to add to, and then click **Connect**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image12.png)
9. <span data-ttu-id="8d1fa-177">**チームエクスプローラー** ウィンドウで、チームプロジェクトコレクション を右クリックし、**新しいチームプロジェクト** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-177">In the **Team Explorer** window, right-click the team project collection, and then click **New Team Project**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image13.png)
10. <span data-ttu-id="8d1fa-178">**[新しいチームプロジェクト]** ダイアログボックスで、チームプロジェクトの名前と説明を入力し、 **[次へ]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-178">In the **New Team Project** dialog box, provide a name and a description for the team project, and then click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="8d1fa-179">チームプロジェクトにスペースが含まれている場合は、インターネットインフォメーションサービス (IIS) Web 配置ツール (Web 配置) を使用して出力パスからパッケージを配置すると、いくつかの問題が発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-179">If your team project includes spaces, you may face some issues when you come to use the Internet Information Services (IIS) Web Deployment Tool (Web Deploy) to deploy packages from the output path.</span></span> <span data-ttu-id="8d1fa-180">パス内のスペースを使用すると、Web 配置コマンドの実行が難しくなります。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-180">Spaces in the path can make it a lot more difficult to run Web Deploy commands.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image14.png)
11. <span data-ttu-id="8d1fa-181">**[プロセステンプレートの選択]** ページで、開発プロセスの管理に使用するプロセステンプレートを選択し、 **[次へ]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-181">On the **Select a Process Template** page, select the process template that you want to use to manage the development process, and then click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="8d1fa-182">TFS のプロセステンプレートの詳細については、「[プロセステンプレートとツール](https://msdn.microsoft.com/vstudio/aa718795)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-182">For more information on process templates for TFS, see [Process Templates and Tools](https://msdn.microsoft.com/vstudio/aa718795).</span></span>
12. <span data-ttu-id="8d1fa-183">**[チームサイトの設定]** ページで、既定の設定を変更せずにそのまま使用し、 **[次へ]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-183">On the **Team Site Settings** page, leave the default settings unchanged, and then click **Next**.</span></span>
13. <span data-ttu-id="8d1fa-184">この設定は、TFS チームプロジェクトに関連付けられている SharePoint チームサイトを作成または識別します。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-184">This setting creates, or identifies, a SharePoint team site that is associated with the TFS team project.</span></span> <span data-ttu-id="8d1fa-185">開発チームは、このサイトを使用して、ドキュメントを管理したり、ディスカッションスレッドに参加したり、wiki ページを作成したり、コードに関連しない他のさまざまなタスクを実行したりできます。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-185">Your development team can use this site to manage documentation, participate in discussion threads, create wiki pages, and perform various other tasks that are not related to code.</span></span> <span data-ttu-id="8d1fa-186">詳細については、「 [SharePoint 製品と Team Foundation Server の間の相互作用](https://msdn.microsoft.com/library/ms253177.aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-186">For more information, see [Interactions Between SharePoint Products and Team Foundation Server](https://msdn.microsoft.com/library/ms253177.aspx).</span></span>
14. <span data-ttu-id="8d1fa-187">**[ソース管理の設定の指定]** ページで、既定の設定を変更せずにそのまま使用し、 **[次へ]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-187">On the **Specify Source Control Settings** page, leave the default settings unchanged, and then click **Next**.</span></span>
15. <span data-ttu-id="8d1fa-188">この設定により、コンテンツのルートフォルダーとして機能する TFS フォルダー階層内の場所が識別または作成されます。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-188">This setting identifies or creates the location in the TFS folder hierarchy that will act as a root folder for your content.</span></span>
16. <span data-ttu-id="8d1fa-189">**[チームプロジェクト設定の確認]** ページで、 **[完了]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-189">On the **Confirm Team Project Settings** page, click **Finish**.</span></span>
17. <span data-ttu-id="8d1fa-190">新しいチームプロジェクトが正常に作成されたら、 **[作成されたチームプロジェクト]** ページで **[閉じる]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-190">When the new team project is successfully created, on the **Team Project Created** page, click **Close**.</span></span>

### <a name="add-users-to-a-team-project"></a><span data-ttu-id="8d1fa-191">チームプロジェクトへのユーザーの追加</span><span class="sxs-lookup"><span data-stu-id="8d1fa-191">Add Users to a Team Project</span></span>

<span data-ttu-id="8d1fa-192">新しいチームプロジェクトを作成したので、ユーザーにアクセス許可を付与して、コンテンツの追加と共同作業を開始できるようにします。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-192">Now that you've created the new team project, you can grant permissions to users to enable them to start adding and collaborating on content.</span></span>

<span data-ttu-id="8d1fa-193">**チームプロジェクトにユーザーを追加するには**</span><span class="sxs-lookup"><span data-stu-id="8d1fa-193">**To add users to a team project**</span></span>

1. <span data-ttu-id="8d1fa-194">Visual Studio 2010 の **[チームエクスプローラー]** ウィンドウで、チームプロジェクトを右クリックし、 **[チームプロジェクトの設定]** をポイントして、 **[グループメンバーシップ]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-194">In Visual Studio 2010, in the **Team Explorer** window, right-click the team project, point to **Team Project Settings**, and then click **Group Membership**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image15.png)
2. <span data-ttu-id="8d1fa-195">ユーザーがソース管理でコードの追加、変更、および削除を行えるようにするには、**共同**作成者グループに追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-195">To enable a user to add, modify, and remove code under source control, you need to add him or her to the **Contributors** group.</span></span>
3. <span data-ttu-id="8d1fa-196">**[プロジェクトグループ]** ダイアログボックスで、 **[共同]** 作成者 グループを選択し、 **[プロパティ]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-196">In the **Project Groups** dialog box, select the **Contributors** group, and then click **Properties**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image16.png)
4. <span data-ttu-id="8d1fa-197">**[Team Foundation Server グループのプロパティ]** ダイアログボックスで、 **[Windows ユーザーまたはグループ]** を選択し、 **[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-197">In the **Team Foundation Server Group Properties** dialog box, select **Windows User or Group**, and then click **Add**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image17.png)
5. <span data-ttu-id="8d1fa-198">**[ユーザー、コンピューター、またはグループの選択]** ダイアログボックスで、チームプロジェクトに追加するユーザーのユーザー名を入力し、 **[名前の確認]** をクリックして、 **[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-198">In the **Select Users, Computers, or Groups** dialog box, type the user name of the user you want to add to the team project, click **Check Names**, and then click **OK**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image18.png)
6. <span data-ttu-id="8d1fa-199">**[Team Foundation Server グループのプロパティ]** ダイアログボックスで、[ **OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-199">In the **Team Foundation Server Group Properties** dialog box, click **OK**.</span></span>
7. <span data-ttu-id="8d1fa-200">**[プロジェクトグループ]** ダイアログボックスで、 **[閉じる]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-200">In the **Project Groups** dialog box, click **Close**.</span></span>

## <a name="conclusion"></a><span data-ttu-id="8d1fa-201">まとめ</span><span class="sxs-lookup"><span data-stu-id="8d1fa-201">Conclusion</span></span>

<span data-ttu-id="8d1fa-202">この時点で、新しいチームプロジェクトを使用する準備ができました。開発者チームは、コンテンツの追加と開発プロセスのコラボレーションを開始できます。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-202">At this point, your new team project is ready to use, and your developer team can start adding content and collaborating on the development process.</span></span>

<span data-ttu-id="8d1fa-203">次のトピック「[ソース管理へのコンテンツの追加](adding-content-to-source-control.md)」では、ソース管理にコンテンツを追加する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-203">The next topic, [Adding Content to Source Control](adding-content-to-source-control.md), describes how to add content to source control.</span></span>

## <a name="further-reading"></a><span data-ttu-id="8d1fa-204">参考資料</span><span class="sxs-lookup"><span data-stu-id="8d1fa-204">Further Reading</span></span>

<span data-ttu-id="8d1fa-205">TFS でチームプロジェクトを作成するための広範なガイダンスについては、「[チームプロジェクトの作成](https://msdn.microsoft.com/library/ms181477(v=VS.100).aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-205">For broader guidance on creating team projects in TFS, see [Create a Team Project](https://msdn.microsoft.com/library/ms181477(v=VS.100).aspx).</span></span> <span data-ttu-id="8d1fa-206">チームプロジェクトコレクション内でユーザーが新しいチームプロジェクトを作成できるようにする方法の詳細については、「[チームプロジェクトコレクションの管理アクセス許可を設定](https://msdn.microsoft.com/library/dd547204.aspx)する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-206">For more information on enabling users to create new team projects within a team project collection, see [Set Administrator Permissions for Team Project Collections](https://msdn.microsoft.com/library/dd547204.aspx).</span></span> <span data-ttu-id="8d1fa-207">チームプロジェクトへのユーザーの追加の詳細については、「[チームプロジェクトへのユーザーの追加](https://msdn.microsoft.com/library/bb558971.aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="8d1fa-207">For more information on adding users to team projects, see [Add Users to Team Projects](https://msdn.microsoft.com/library/bb558971.aspx).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="8d1fa-208">[前へ](configuring-team-foundation-server-for-web-deployment.md)
> [次へ](adding-content-to-source-control.md)</span><span class="sxs-lookup"><span data-stu-id="8d1fa-208">[Previous](configuring-team-foundation-server-for-web-deployment.md)
[Next](adding-content-to-source-control.md)</span></span>
