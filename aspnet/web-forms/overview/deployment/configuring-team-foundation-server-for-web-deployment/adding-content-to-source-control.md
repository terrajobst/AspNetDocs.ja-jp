---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/adding-content-to-source-control
title: ソース管理へのコンテンツの追加 |Microsoft Docs
author: jrjlee
description: このトピックでは、Team Foundation Server (TFS) 2010 でソース管理にコンテンツを追加する方法について説明します。 ここでは、ソリューションとプロジェクトをチームに追加する方法について説明します。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 86c14aab-c2dd-4f73-b40c-c6d52fa44950
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/adding-content-to-source-control
msc.type: authoredcontent
ms.openlocfilehash: 16073dd2fb0ea1cc4ddbc94c843181933dc174c1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78515110"
---
# <a name="adding-content-to-source-control"></a><span data-ttu-id="b6e78-104">ソース管理にコンテンツを追加する</span><span class="sxs-lookup"><span data-stu-id="b6e78-104">Adding Content to Source Control</span></span>

<span data-ttu-id="b6e78-105">[Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="b6e78-105">by [Jason Lee](https://github.com/jrjlee)</span></span>

<span data-ttu-id="b6e78-106">[[Download PDF]\(PDF をダウンロード\)](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)</span><span class="sxs-lookup"><span data-stu-id="b6e78-106">[Download PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)</span></span>

> <span data-ttu-id="b6e78-107">このトピックでは、Team Foundation Server (TFS) 2010 でソース管理にコンテンツを追加する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="b6e78-107">This topic explains how to add content to source control in Team Foundation Server (TFS) 2010.</span></span> <span data-ttu-id="b6e78-108">TFS のチームプロジェクトにソリューションとプロジェクトを追加する方法について説明し、フレームワークやアセンブリなどの外部の依存関係をソース管理に追加する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="b6e78-108">It describes how to add solutions and projects to a team project in TFS, and it explains how to add external dependencies like frameworks or assemblies to source control.</span></span>

<span data-ttu-id="b6e78-109">このトピックでは、Fabrikam, Inc. という架空の企業のエンタープライズ展開要件に基づいて、一連のチュートリアルの一部を説明します。このチュートリアルシリーズでは、&#x2014; [Contact Manager ソリューション](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;のサンプルソリューションを使用して、ASP.NET MVC 3 アプリケーション、Windows Communication Foundation (WCF) サービス、データベースプロジェクトなど、現実的なレベルの複雑さを持つ web アプリケーションを表します。</span><span class="sxs-lookup"><span data-stu-id="b6e78-109">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

## <a name="task-overview"></a><span data-ttu-id="b6e78-110">タスクの概要</span><span class="sxs-lookup"><span data-stu-id="b6e78-110">Task Overview</span></span>

<span data-ttu-id="b6e78-111">ほとんどの場合、開発者チームのすべてのメンバーは、ソース管理にコンテンツを追加できる必要があります。</span><span class="sxs-lookup"><span data-stu-id="b6e78-111">In most cases, every member of the developer team should be able to add content to source control.</span></span> <span data-ttu-id="b6e78-112">TFS のソース管理にソリューションを追加するには、次の大まかな手順を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b6e78-112">To add a solution to source control in TFS, you'll need to complete these high-level steps:</span></span>

- <span data-ttu-id="b6e78-113">チームプロジェクトに接続します。</span><span class="sxs-lookup"><span data-stu-id="b6e78-113">Connect to a team project.</span></span>
- <span data-ttu-id="b6e78-114">サーバー上のチームプロジェクトフォルダー構造をローカルコンピューター上のフォルダー構造にマップします。</span><span class="sxs-lookup"><span data-stu-id="b6e78-114">Map the team project folder structure on the server to a folder structure on your local computer.</span></span>
- <span data-ttu-id="b6e78-115">ソリューションとその内容をソース管理に追加します。</span><span class="sxs-lookup"><span data-stu-id="b6e78-115">Add the solution and its contents to source control.</span></span>
- <span data-ttu-id="b6e78-116">ソース管理に外部依存関係を追加します。</span><span class="sxs-lookup"><span data-stu-id="b6e78-116">Add any external dependencies to source control.</span></span>

<span data-ttu-id="b6e78-117">このトピックでは、これらの手順を実行する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="b6e78-117">This topic will show you how to perform these procedures.</span></span>

<span data-ttu-id="b6e78-118">このトピックのタスクとチュートリアルでは、コンテンツを管理するための新しい TFS チームプロジェクトが既に作成されていることを前提としています。</span><span class="sxs-lookup"><span data-stu-id="b6e78-118">The tasks and walkthroughs in this topic assume that you've already created a new TFS team project to manage your content.</span></span> <span data-ttu-id="b6e78-119">新しいチームプロジェクトの作成の詳細については、「 [TFS でのチームプロジェクトの作成](creating-a-team-project-in-tfs.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="b6e78-119">For more information on creating a new team project, see [Creating a Team Project in TFS](creating-a-team-project-in-tfs.md).</span></span>

### <a name="who-performs-these-procedures"></a><span data-ttu-id="b6e78-120">これらの手順を実行するユーザー</span><span class="sxs-lookup"><span data-stu-id="b6e78-120">Who Performs These Procedures?</span></span>

<span data-ttu-id="b6e78-121">ほとんどの場合、開発者チームのすべてのメンバーが、特定のチームプロジェクト内のコンテンツを追加および変更できる必要があります。</span><span class="sxs-lookup"><span data-stu-id="b6e78-121">In most cases, every member of the developer team should be able to add and modify content within specific team projects.</span></span>

## <a name="connect-to-a-team-project-and-create-a-folder-mapping"></a><span data-ttu-id="b6e78-122">チームプロジェクトに接続してフォルダーマッピングを作成する</span><span class="sxs-lookup"><span data-stu-id="b6e78-122">Connect to a Team Project and Create a Folder Mapping</span></span>

<span data-ttu-id="b6e78-123">ソース管理にコンテンツを追加する前に、チームプロジェクトに接続し、サーバー上のフォルダー構造とローカルコンピューター上のファイルシステムとの間にマッピングを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b6e78-123">Before you add any content to source control, you need to connect to a team project and create a mapping between the folder structure on the server and the file system on your local machine.</span></span>

<span data-ttu-id="b6e78-124">**チームプロジェクトに接続してローカルパスをマップするには**</span><span class="sxs-lookup"><span data-stu-id="b6e78-124">**To connect to a team project and map a local path**</span></span>

1. <span data-ttu-id="b6e78-125">開発者ワークステーションで、Visual Studio 2010 を開きます。</span><span class="sxs-lookup"><span data-stu-id="b6e78-125">On your developer workstation, open Visual Studio 2010.</span></span>
2. <span data-ttu-id="b6e78-126">Visual Studio の **[チーム]** メニューで、[ **Team Foundation Server に接続] を**クリックします。</span><span class="sxs-lookup"><span data-stu-id="b6e78-126">In Visual Studio, on the **Team** menu, click **Connect to Team Foundation Server**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b6e78-127">TFS サーバーへの接続が既に構成されている場合は、手順3-6 を省略できます。</span><span class="sxs-lookup"><span data-stu-id="b6e78-127">If you have already configured a connection to a TFS server, you can omit steps 3-6.</span></span>
3. <span data-ttu-id="b6e78-128">**[チームプロジェクトへの接続]** ダイアログボックスで、 **[サーバー]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="b6e78-128">In the **Connection to Team Project** dialog box, click **Servers**.</span></span>
4. <span data-ttu-id="b6e78-129">**[Team Foundation Server の追加と削除]** ダイアログボックスで、 **[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="b6e78-129">In the **Add/Remove Team Foundation Server** dialog box, click **Add**.</span></span>
5. <span data-ttu-id="b6e78-130">**[Team Foundation Server の追加]** ダイアログボックスで、TFS インスタンスの詳細を指定し、 **[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="b6e78-130">In the **Add Team Foundation Server** dialog box, provide the details of your TFS instance, and then click **OK**.</span></span>

    ![](adding-content-to-source-control/_static/image1.png)
6. <span data-ttu-id="b6e78-131">**[Team Foundation Server の追加と削除]** ダイアログボックスで、 **[閉じる]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="b6e78-131">In the **Add/Remove Team Foundation Server** dialog box, click **Close**.</span></span>
7. <span data-ttu-id="b6e78-132">**[チームプロジェクトへの接続]** ダイアログボックスで、接続する TFS インスタンスを選択し、チームプロジェクトコレクション を選択して、追加するチームプロジェクトを選択し、 **[接続]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="b6e78-132">In the **Connect to Team Project** dialog box, select the TFS instance you want to connect to, select the team project collection, select the team project you want to add to, and then click **Connect**.</span></span>

    ![](adding-content-to-source-control/_static/image2.png)
8. <span data-ttu-id="b6e78-133">**[チームエクスプローラー]** ウィンドウで、チームプロジェクトを展開し、 **[ソース管理]** をダブルクリックします。</span><span class="sxs-lookup"><span data-stu-id="b6e78-133">In the **Team Explorer** window, expand your team project, and then double-click **Source Control**.</span></span>

    ![](adding-content-to-source-control/_static/image3.png)
9. <span data-ttu-id="b6e78-134">**[ソース管理エクスプローラー]** タブで、 **[マップされていません]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="b6e78-134">On the **Source Control Explorer** tab, click **Not mapped**.</span></span>

    ![](adding-content-to-source-control/_static/image4.png)
10. <span data-ttu-id="b6e78-135">**[マップ]** ダイアログボックスの **[ローカルフォルダー]** ボックスで、チームプロジェクトのルートフォルダーとして機能するローカルフォルダーを参照 (または作成) してから、 **[マップ]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="b6e78-135">In the **Map** dialog box, in the **Local folder** box, browse to (or create) a local folder to act as the root folder for the team project, and then click **Map**.</span></span>

    ![](adding-content-to-source-control/_static/image5.png)
11. <span data-ttu-id="b6e78-136">ソースファイルのダウンロードを求めるメッセージが表示されたら、[**はい]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="b6e78-136">When you're prompted to download source files, click **Yes**.</span></span>

    ![](adding-content-to-source-control/_static/image6.png)

<span data-ttu-id="b6e78-137">この時点で、チームプロジェクトのサーバー側フォルダーが、開発者ワークステーションのローカルフォルダーにマップされています。</span><span class="sxs-lookup"><span data-stu-id="b6e78-137">At this point, you have mapped the server-side folder for the team project to a local folder on your developer workstation.</span></span> <span data-ttu-id="b6e78-138">また、チームプロジェクトの既存のコンテンツをローカルフォルダー構造にダウンロードしました。</span><span class="sxs-lookup"><span data-stu-id="b6e78-138">You've also downloaded any existing content from the team project to your local folder structure.</span></span> <span data-ttu-id="b6e78-139">これで、ソース管理に独自のコンテンツを追加できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="b6e78-139">You can now start to add your own content to source control.</span></span>

## <a name="add-projects-and-solutions-to-source-control"></a><span data-ttu-id="b6e78-140">ソース管理へのプロジェクトとソリューションの追加</span><span class="sxs-lookup"><span data-stu-id="b6e78-140">Add Projects and Solutions to Source Control</span></span>

<span data-ttu-id="b6e78-141">ソース管理にプロジェクトとソリューションを追加するには、まず、ローカルコンピューター上のチームプロジェクトのマップされたフォルダーに移動する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b6e78-141">To add projects and solutions to source control, you first need to move them to the mapped folder for the team project on your local machine.</span></span> <span data-ttu-id="b6e78-142">その後、コンテンツをチェックインして、追加したサーバーとサーバーとの同期をとることができます。</span><span class="sxs-lookup"><span data-stu-id="b6e78-142">You can then check in the content to synchronize your additions with the server.</span></span>

<span data-ttu-id="b6e78-143">**ソース管理にプロジェクトを追加するには**</span><span class="sxs-lookup"><span data-stu-id="b6e78-143">**To add projects to source control**</span></span>

1. <span data-ttu-id="b6e78-144">開発者ワークステーションで、チームプロジェクトのマップされたフォルダー構造内の適切な場所にプロジェクトとソリューションを移動します。</span><span class="sxs-lookup"><span data-stu-id="b6e78-144">On your developer workstation, move your projects and solutions to an appropriate location within the mapped folder structure for the team project.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b6e78-145">多くの組織では、プロジェクトとソリューションをソース管理でどのように編成するかをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="b6e78-145">Many organizations will have a preferred approach to how projects and solutions should be organized in source control.</span></span> <span data-ttu-id="b6e78-146">フォルダーを構造化する方法のガイダンスについては、「[方法: Team Foundation Server でソース管理フォルダーを構成](https://msdn.microsoft.com/library/bb668992.aspx)する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="b6e78-146">For guidance on how to structure folders, see [How To: Structure Your Source Control Folders in Team Foundation Server](https://msdn.microsoft.com/library/bb668992.aspx).</span></span>
2. <span data-ttu-id="b6e78-147">Visual Studio 2010 でソリューションを開きます。</span><span class="sxs-lookup"><span data-stu-id="b6e78-147">Open the solution in Visual Studio 2010.</span></span>
3. <span data-ttu-id="b6e78-148">**[ソリューションエクスプローラー]** ウィンドウで、ソリューションを右クリックし、[**ソリューションをソース管理に追加] を**クリックします。</span><span class="sxs-lookup"><span data-stu-id="b6e78-148">In the **Solution Explorer** window, right-click the solution, and then click **Add Solution to Source Control**.</span></span>

    ![](adding-content-to-source-control/_static/image7.png)

    > [!NOTE]
    > <span data-ttu-id="b6e78-149">場合によっては、TFS でコンテンツを構造化する方法によっては、ソース管理にプロジェクトを個別に追加して、ソースコードの編成方法をより細かく制御できるようにすることが必要になる場合があります。</span><span class="sxs-lookup"><span data-stu-id="b6e78-149">In some cases, depending on how your organization likes to structure content in TFS, you may need to add projects to source control individually to provide more fine-grained control over how your source code is organized.</span></span>
4. <span data-ttu-id="b6e78-150">**[ソース管理エクスプローラー]** タブに、チームプロジェクトのサーバーフォルダー構造内に追加したコンテンツが表示されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="b6e78-150">Verify that the **Source Control Explorer** tab displays the content you've added within the server folder structure for the team project.</span></span>

    ![](adding-content-to-source-control/_static/image8.png)

    > [!NOTE]
    > <span data-ttu-id="b6e78-151">**[ソース管理エクスプローラー]** タブには、ローカルファイルシステム上のマップされたフォルダーにソリューションを追加したため、メッセージが表示されません。</span><span class="sxs-lookup"><span data-stu-id="b6e78-151">The **Source Control Explorer** tab displays your content with no further prompting because you added your solution to a mapped folder on the local file system.</span></span> <span data-ttu-id="b6e78-152">ソリューションがマップされていない場所にある場合は、TFS とローカルファイルシステムの両方でフォルダーの場所を指定するように求められます。</span><span class="sxs-lookup"><span data-stu-id="b6e78-152">If your solution was in an unmapped location, you'd be prompted to specify folder locations in both TFS and your local file system.</span></span>
5. <span data-ttu-id="b6e78-153">**[ソース管理エクスプローラー]** タブの **[フォルダー]** ウィンドウで、チームプロジェクト ( **contactmanager**など) を右クリックし、 **[保留中の変更をチェックイン]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="b6e78-153">On the **Source Control Explorer** tab, in the **Folders** pane, right-click the team project (for example, **ContactManager**), and then click **Check In Pending Changes**.</span></span>
6. <span data-ttu-id="b6e78-154">**[チェックイン-ソースファイル]** ダイアログボックスで、コメントを入力し、 **[チェックイン]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="b6e78-154">In the **Check In – Source Files** dialog box, type a comment, and then click **Check In**.</span></span>

    ![](adding-content-to-source-control/_static/image9.png)

<span data-ttu-id="b6e78-155">この時点で、ソリューションを TFS のソース管理に追加しました。</span><span class="sxs-lookup"><span data-stu-id="b6e78-155">At this point you have added your solution to source control in TFS.</span></span>

## <a name="add-external-dependencies-to-source-control"></a><span data-ttu-id="b6e78-156">ソース管理への外部依存関係の追加</span><span class="sxs-lookup"><span data-stu-id="b6e78-156">Add External Dependencies to Source Control</span></span>

<span data-ttu-id="b6e78-157">ソース管理にプロジェクトまたはソリューションを追加すると、プロジェクトまたはソリューション内のファイルとフォルダーも追加されます。</span><span class="sxs-lookup"><span data-stu-id="b6e78-157">When you add a project or solution to source control, any files and folders within your project or solution will also be added.</span></span> <span data-ttu-id="b6e78-158">ただし、多くの場合、プロジェクトとソリューションは、ローカルアセンブリなどの外部の依存関係を使用して正常に機能することにも依存します。</span><span class="sxs-lookup"><span data-stu-id="b6e78-158">However, in a lot of cases, projects and solutions also rely on external dependencies, like local assemblies, to function properly.</span></span> <span data-ttu-id="b6e78-159">このようなリソースをソース管理に追加して、チームビルドと開発者チームの他のメンバーがコードを正常にビルドできるようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="b6e78-159">You need to add any such resources to source control to let both Team Build and other members of the developer team build your code successfully.</span></span>

<span data-ttu-id="b6e78-160">たとえば、Contact Manager サンプルソリューションのフォルダー構造には、packages という名前のフォルダーがあります。</span><span class="sxs-lookup"><span data-stu-id="b6e78-160">For example, the folder structure for the Contact Manager sample solution includes a folder named packages.</span></span> <span data-ttu-id="b6e78-161">これには、アセンブリと、ADO.NET Entity Framework 4.1 のさまざまなサポートリソースが含まれます。</span><span class="sxs-lookup"><span data-stu-id="b6e78-161">This contains the assembly and various supporting resources for the ADO.NET Entity Framework 4.1.</span></span> <span data-ttu-id="b6e78-162">Packages フォルダーは Contact Manager ソリューションの一部ではありませんが、ソリューションは正常にビルドされません。</span><span class="sxs-lookup"><span data-stu-id="b6e78-162">The packages folder is not part of the Contact Manager solution, but the solution will not build successfully without it.</span></span> <span data-ttu-id="b6e78-163">チームビルドでソリューションをビルドできるようにするには、[パッケージ] フォルダーをソース管理に追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b6e78-163">To enable Team Build to build the solution, you need to add the packages folder to source control.</span></span>

> [!NOTE]
> <span data-ttu-id="b6e78-164">Packages フォルダーを含めることは、Visual Studio 2010 用の NuGet 拡張機能を使用して、Entity Framework、または同様のリソースをソリューションに追加したときの動作です。</span><span class="sxs-lookup"><span data-stu-id="b6e78-164">The inclusion of a packages folder is typical of what happens when you add the Entity Framework, or similar resources, to your solution using the NuGet extension for Visual Studio 2010.</span></span>

<span data-ttu-id="b6e78-165">**ソース管理にプロジェクト以外のコンテンツを追加するには**</span><span class="sxs-lookup"><span data-stu-id="b6e78-165">**To add non-project content to source control**</span></span>

1. <span data-ttu-id="b6e78-166">追加する項目 (packages フォルダーなど) が、ローカルファイルシステム上のマップされたフォルダー内の適切な場所にあることを確認します。</span><span class="sxs-lookup"><span data-stu-id="b6e78-166">Ensure that the items you want to add (for example, the packages folder) are in an appropriate location within a mapped folder on your local file system.</span></span>
2. <span data-ttu-id="b6e78-167">Visual Studio 2010 の **[チームエクスプローラー]** ウィンドウで、チームプロジェクトを展開し、 **[ソース管理]** をダブルクリックします。</span><span class="sxs-lookup"><span data-stu-id="b6e78-167">In Visual Studio 2010, In the **Team Explorer** window, expand your team project, and then double-click **Source Control**.</span></span>

    ![](adding-content-to-source-control/_static/image10.png)
3. <span data-ttu-id="b6e78-168">**[ソース管理エクスプローラー]** タブの **[フォルダー]** ウィンドウで、追加する項目が含まれているフォルダーを選択します。</span><span class="sxs-lookup"><span data-stu-id="b6e78-168">On the **Source Control Explorer** tab, in the **Folders** pane, select the folder that contains the item or items you want to add.</span></span>
4. <span data-ttu-id="b6e78-169">**[フォルダーへの項目の追加]** ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="b6e78-169">Click the **Add Items to Folder** button.</span></span>

    ![](adding-content-to-source-control/_static/image11.png)
5. <span data-ttu-id="b6e78-170">**[ソース管理に追加]** ダイアログボックスで、追加するフォルダーを選択し、 **[次へ]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="b6e78-170">In the **Add to Source Control** dialog box, select the folder or items you want to add, and then click **Next**.</span></span>

    ![](adding-content-to-source-control/_static/image12.png)
6. <span data-ttu-id="b6e78-171">**[除外する項目]** タブで、自動的に除外された必要な項目 (アセンブリなど) を選択し、 **[項目を含める]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="b6e78-171">On the **Excluded items** tab, select any required items that have been automatically excluded (for example, assemblies), and then click **Include item(s)**.</span></span>

    ![](adding-content-to-source-control/_static/image13.png)
7. <span data-ttu-id="b6e78-172">**[追加する項目]** タブで、含めるすべてのファイルが表示されていることを確認し、 **[完了]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="b6e78-172">On the **Items to add** tab, verify that all the files you want to include are listed, and then click **Finish**.</span></span>

    ![](adding-content-to-source-control/_static/image14.png)
8. <span data-ttu-id="b6e78-173">**[ソース管理エクスプローラー]** ウィンドウで、 **[チェックイン]** ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="b6e78-173">In the **Source Control Explorer** window, click the **Check In** button.</span></span>

    ![](adding-content-to-source-control/_static/image15.png)
9. <span data-ttu-id="b6e78-174">**[チェックイン-ソースファイル]** ダイアログボックスで、コメントを入力し、 **[チェックイン]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="b6e78-174">In the **Check In – Source Files** dialog box, type a comment, and then click **Check In**.</span></span>

<span data-ttu-id="b6e78-175">この時点で、ソリューションの外部の依存関係がソース管理に追加されました。</span><span class="sxs-lookup"><span data-stu-id="b6e78-175">At this point, you have added the external dependencies for your solution to source control.</span></span>

## <a name="conclusion"></a><span data-ttu-id="b6e78-176">まとめ</span><span class="sxs-lookup"><span data-stu-id="b6e78-176">Conclusion</span></span>

<span data-ttu-id="b6e78-177">このトピックでは、チームプロジェクトに接続する方法、フォルダー構造をマップする方法、およびソース管理にコンテンツを追加する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="b6e78-177">This topic described how to connect to a team project, map a folder structure, and add content to source control.</span></span> <span data-ttu-id="b6e78-178">ソース管理下の項目を操作する方法の詳細については、「[バージョン管理の使用](https://msdn.microsoft.com/library/ms181368.aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="b6e78-178">For more information on how to work with items under source control, see [Using Version Control](https://msdn.microsoft.com/library/ms181368.aspx).</span></span>

<span data-ttu-id="b6e78-179">次のトピック「 [Web 配置用の Tfs ビルドサーバーの構成](configuring-a-tfs-build-server-for-web-deployment.md)」では、Tfs チームビルドサーバーを準備してソリューションをビルドおよび配置する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="b6e78-179">The next topic, [Configuring a TFS Build Server for Web Deployment](configuring-a-tfs-build-server-for-web-deployment.md), describes how to prepare a TFS Team Build server to build and deploy your solution.</span></span>

## <a name="further-reading"></a><span data-ttu-id="b6e78-180">参考資料</span><span class="sxs-lookup"><span data-stu-id="b6e78-180">Further Reading</span></span>

<span data-ttu-id="b6e78-181">TFS でソース管理を操作する方法の詳細については、「[バージョン管理の使用](https://msdn.microsoft.com/library/ms181368.aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="b6e78-181">For more comprehensive information on working with source control in TFS, see [Using Version Control](https://msdn.microsoft.com/library/ms181368.aspx).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="b6e78-182">[前へ](creating-a-team-project-in-tfs.md)
> [次へ](configuring-a-tfs-build-server-for-web-deployment.md)</span><span class="sxs-lookup"><span data-stu-id="b6e78-182">[Previous](creating-a-team-project-in-tfs.md)
[Next](configuring-a-tfs-build-server-for-web-deployment.md)</span></span>
