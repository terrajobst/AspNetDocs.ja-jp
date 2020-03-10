---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/creating-a-build-definition-that-supports-deployment
title: 配置をサポートするビルド定義を作成する |Microsoft Docs
author: jrjlee
description: Team Foundation Server (TFS) 2010 で任意の種類のビルドを実行する場合は、チームプロジェクト内にビルド定義を作成する必要があります。 このトピックの内容
ms.author: riande
ms.date: 05/04/2012
ms.assetid: fe47a018-f6d0-4979-80e7-5b1fa75a5865
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/creating-a-build-definition-that-supports-deployment
msc.type: authoredcontent
ms.openlocfilehash: e11c91a824446572aaf0b3bc6954b9b8ffb4eaff
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78489010"
---
# <a name="creating-a-build-definition-that-supports-deployment"></a><span data-ttu-id="4e990-104">配置をサポートするビルド定義を作成する</span><span class="sxs-lookup"><span data-stu-id="4e990-104">Creating a Build Definition That Supports Deployment</span></span>

<span data-ttu-id="4e990-105">[Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="4e990-105">by [Jason Lee](https://github.com/jrjlee)</span></span>

<span data-ttu-id="4e990-106">[[Download PDF]\(PDF をダウンロード\)](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)</span><span class="sxs-lookup"><span data-stu-id="4e990-106">[Download PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)</span></span>

> <span data-ttu-id="4e990-107">Team Foundation Server (TFS) 2010 で任意の種類のビルドを実行する場合は、チームプロジェクト内にビルド定義を作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4e990-107">If you want to perform any kind of build in Team Foundation Server (TFS) 2010, you need to create a build definition within your team project.</span></span> <span data-ttu-id="4e990-108">このトピックでは、TFS で新しいビルド定義を作成する方法と、チームビルドでビルドプロセスの一部として web 配置を制御する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="4e990-108">This topic describes how to create a new build definition in TFS and how to control web deployment as part of the build process in Team Build.</span></span>

<span data-ttu-id="4e990-109">このトピックでは、Fabrikam, Inc. という架空の企業のエンタープライズ展開要件に基づいて、一連のチュートリアルの一部を説明します。このチュートリアルシリーズでは、&#x2014; [Contact Manager ソリューション](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;のサンプルソリューションを使用して、ASP.NET MVC 3 アプリケーション、Windows Communication Foundation (WCF) サービス、データベースプロジェクトなど、現実的なレベルの複雑さを持つ web アプリケーションを表します。</span><span class="sxs-lookup"><span data-stu-id="4e990-109">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

<span data-ttu-id="4e990-110">これらのチュートリアルの中核となる配置方法は、「プロジェクト[ファイルについ](../web-deployment-in-the-enterprise/understanding-the-project-file.md)て」で説明されている分割プロジェクトファイルアプローチに基づいています。この方法で&#x2014;は、ビルドおよび配置プロセスは、すべての変換先環境に適用されるビルド命令を含む2つのプロジェクトファイルと、環境固有のビルドと配置の設定を含んでいます。</span><span class="sxs-lookup"><span data-stu-id="4e990-110">The deployment method at the heart of these tutorials is based on the split project file approach described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md), in which the build and deployment process is controlled by two project files&#x2014;one containing build instructions that apply to every destination environment, and one containing environment-specific build and deployment settings.</span></span> <span data-ttu-id="4e990-111">ビルド時に、環境固有のプロジェクトファイルが環境に依存しないプロジェクトファイルにマージされ、ビルド命令の完全なセットが形成されます。</span><span class="sxs-lookup"><span data-stu-id="4e990-111">At build time, the environment-specific project file is merged into the environment-agnostic project file to form a complete set of build instructions.</span></span>

## <a name="task-overview"></a><span data-ttu-id="4e990-112">タスクの概要</span><span class="sxs-lookup"><span data-stu-id="4e990-112">Task Overview</span></span>

<span data-ttu-id="4e990-113">ビルド定義は、TFS のチームプロジェクトに対してビルドを実行する方法とタイミングを制御するメカニズムです。</span><span class="sxs-lookup"><span data-stu-id="4e990-113">A build definition is the mechanism that controls how and when builds occur for team projects in TFS.</span></span> <span data-ttu-id="4e990-114">各ビルド定義は次を指定します。</span><span class="sxs-lookup"><span data-stu-id="4e990-114">Each build definition specifies:</span></span>

- <span data-ttu-id="4e990-115">ビルドする項目。 Visual Studio ソリューションファイルやカスタム Microsoft Build Engine (MSBuild) プロジェクトファイルなどです。</span><span class="sxs-lookup"><span data-stu-id="4e990-115">The things you want to build, like Visual Studio solution files or custom Microsoft Build Engine (MSBuild) project files.</span></span>
- <span data-ttu-id="4e990-116">手動トリガー、継続的インテグレーション (CI)、ゲートチェックインなど、ビルドを実行するタイミングを決定する条件。</span><span class="sxs-lookup"><span data-stu-id="4e990-116">The criteria that determine when a build should take place, like manual triggers, continuous integration (CI), or gated check-ins.</span></span>
- <span data-ttu-id="4e990-117">チームビルドがビルド出力を送信する場所 (web パッケージやデータベーススクリプトなどの配置成果物を含む)。</span><span class="sxs-lookup"><span data-stu-id="4e990-117">The location to which Team Build should send build outputs, including deployment artifacts like web packages and database scripts.</span></span>
- <span data-ttu-id="4e990-118">各ビルドが保持される時間の長さ。</span><span class="sxs-lookup"><span data-stu-id="4e990-118">The amount of time that each build should be retained.</span></span>
- <span data-ttu-id="4e990-119">ビルドプロセスの他のさまざまなパラメーター。</span><span class="sxs-lookup"><span data-stu-id="4e990-119">Various other parameters of the build process.</span></span>

> [!NOTE]
> <span data-ttu-id="4e990-120">ビルド定義の詳細については、「[ビルドプロセスの定義](https://msdn.microsoft.com/library/ms181715.aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="4e990-120">For more information on build definitions, see [Define Your Build Process](https://msdn.microsoft.com/library/ms181715.aspx).</span></span>

<span data-ttu-id="4e990-121">このトピックでは、開発者が新しいコンテンツをチェックインしたときにビルドがトリガーされるように、CI を使用するビルド定義を作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="4e990-121">This topic will show you how to create a build definition that uses CI, so that a build is triggered when a developer checks in new content.</span></span> <span data-ttu-id="4e990-122">ビルドが成功した場合、ビルドサービスはカスタムプロジェクトファイルを実行して、ソリューションをテスト環境に配置します。</span><span class="sxs-lookup"><span data-stu-id="4e990-122">If the build succeeds, the build service runs a custom project file to deploy the solution to a test environment.</span></span>

<span data-ttu-id="4e990-123">ビルドをトリガーするときは、次の操作を行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="4e990-123">When you trigger a build, these actions need to happen:</span></span>

- <span data-ttu-id="4e990-124">まず、チームビルドによってソリューションがビルドされます。</span><span class="sxs-lookup"><span data-stu-id="4e990-124">First, Team Build should build the solution.</span></span> <span data-ttu-id="4e990-125">このプロセスの一部として、チームビルドは Web 発行パイプライン (WPP) を呼び出して、ソリューション内の各 web アプリケーションプロジェクトの web 配置パッケージを生成します。</span><span class="sxs-lookup"><span data-stu-id="4e990-125">As part of this process, Team Build will invoke the Web Publishing Pipeline (WPP) to generate web deployment packages for each of the web application projects in the solution.</span></span> <span data-ttu-id="4e990-126">チームビルドでは、ソリューションに関連付けられている単体テストも実行されます。</span><span class="sxs-lookup"><span data-stu-id="4e990-126">Team Build will also run any unit tests associated with the solution.</span></span>
- <span data-ttu-id="4e990-127">ソリューションのビルドに失敗した場合、チームビルドはそれ以上の操作を行う必要はありません。</span><span class="sxs-lookup"><span data-stu-id="4e990-127">If the solution build fails, Team Build should take no further action.</span></span> <span data-ttu-id="4e990-128">単体テストの失敗は、ビルドの失敗として扱う必要があります。</span><span class="sxs-lookup"><span data-stu-id="4e990-128">Unit test failures should be treated as a build failure.</span></span>
- <span data-ttu-id="4e990-129">ソリューションのビルドが成功した場合は、ソリューションの配置を制御するカスタムプロジェクトファイルをチームビルドで実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4e990-129">If the solution build succeeds, Team Build should run the custom project file that controls the deployment of the solution.</span></span> <span data-ttu-id="4e990-130">このプロセスの一部として、チームビルドはインターネットインフォメーションサービス (IIS) Web 配置ツール (Web 配置) を呼び出して、パッケージ化された web アプリケーションを対象の web サーバーにインストールします。また、VSDBCMD ユーティリティを呼び出してデータベースの作成を実行します。転送先データベースサーバー上のスクリプト。</span><span class="sxs-lookup"><span data-stu-id="4e990-130">As part of this process, Team Build will invoke the Internet Information Services (IIS) Web Deployment Tool (Web Deploy) to install the packaged web applications on the destination web servers, and it will invoke the VSDBCMD.exe utility to run database creation scripts on the destination database servers.</span></span>

<span data-ttu-id="4e990-131">このプロセスを次に示します。</span><span class="sxs-lookup"><span data-stu-id="4e990-131">This illustrates the process:</span></span>

![](creating-a-build-definition-that-supports-deployment/_static/image1.png)

<span data-ttu-id="4e990-132">[Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)サンプルソリューションには、msbuild またはチームビルドから実行できるカスタム msbuild プロジェクトファイル ( *Publish. proj*) が含まれています。</span><span class="sxs-lookup"><span data-stu-id="4e990-132">The [Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) sample solution includes a custom MSBuild project file, *Publish.proj*, that you can run from MSBuild or Team Build.</span></span> <span data-ttu-id="4e990-133">「[ビルドプロセスについ](../web-deployment-in-the-enterprise/understanding-the-build-process.md)て」で説明されているように、このプロジェクトファイルは、web パッケージとデータベースをターゲット環境に配置するロジックを定義します。</span><span class="sxs-lookup"><span data-stu-id="4e990-133">As described in [Understanding the Build Process](../web-deployment-in-the-enterprise/understanding-the-build-process.md), this project file defines the logic that deploys your web packages and databases to a target environment.</span></span> <span data-ttu-id="4e990-134">このファイルには、チームビルドで実行されている場合にビルドおよびパッケージ化のプロセスを省略するロジックが含まれており、実行する配置タスクだけが残ります。</span><span class="sxs-lookup"><span data-stu-id="4e990-134">The file includes logic that omits the building and packaging process if it's running in Team Build, leaving just the deployment tasks to run.</span></span> <span data-ttu-id="4e990-135">これは、この方法で配置を自動化する場合、通常、ソリューションが正常にビルドされ、配置プロセスが開始される前に単体テストが合格することを確認する必要があるためです。</span><span class="sxs-lookup"><span data-stu-id="4e990-135">This is because when you automate deployment in this way, you'll typically want to ensure that the solution builds successfully and passes any unit tests before the deployment process commences.</span></span>

<span data-ttu-id="4e990-136">次のセクションでは、新しいビルド定義を作成することによって、このプロセスを実装する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="4e990-136">The next section explains how to implement this process by creating a new build definition.</span></span>

> [!NOTE]
> <span data-ttu-id="4e990-137">この手順&#x2014;では、ソリューション&#x2014;をビルド、テスト、および配置するための単一の自動化されたプロセスが、テスト環境への配置に最も適している可能性があります。</span><span class="sxs-lookup"><span data-stu-id="4e990-137">This procedure&#x2014;in which a single automated process builds, tests, and deploys a solution&#x2014;is likely to be most suited to deployment to test environments.</span></span> <span data-ttu-id="4e990-138">ステージング環境と運用環境では、テスト環境で既に検証および検証済みのコンテンツを以前のビルドから配置する方がはるかに多い場合があります。</span><span class="sxs-lookup"><span data-stu-id="4e990-138">For staging and production environments you're a lot more likely to want to deploy content from a previous build that you've already verified and validated in a test environment.</span></span> <span data-ttu-id="4e990-139">この方法については、次のトピック「[特定のビルドの配置](deploying-a-specific-build.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="4e990-139">This approach is described in the next topic, [Deploying a Specific Build](deploying-a-specific-build.md).</span></span>

### <a name="who-performs-this-procedure"></a><span data-ttu-id="4e990-140">だれがこの手順を実行しますか?</span><span class="sxs-lookup"><span data-stu-id="4e990-140">Who Performs This Procedure?</span></span>

<span data-ttu-id="4e990-141">通常、TFS 管理者がこの手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="4e990-141">Typically, a TFS administrator performs this procedure.</span></span> <span data-ttu-id="4e990-142">場合によっては、開発者チームリーダーが TFS のチームプロジェクトコレクションに対して責任を負うことがあります。</span><span class="sxs-lookup"><span data-stu-id="4e990-142">In some cases, a developer team leader may take responsibility for the team project collection in TFS.</span></span> <span data-ttu-id="4e990-143">新しいビルド定義を作成するには、ソリューションを含むチームプロジェクトコレクションの**プロジェクトコレクションビルド管理者**グループのメンバーである必要があります。</span><span class="sxs-lookup"><span data-stu-id="4e990-143">In order to create a new build definition, you need to be a member of the **Project Collection Build Administrators** group for the team project collection that contains your solution.</span></span>

## <a name="create-a-build-definition-for-ci-and-deployment"></a><span data-ttu-id="4e990-144">CI とデプロイのビルド定義を作成する</span><span class="sxs-lookup"><span data-stu-id="4e990-144">Create a Build Definition for CI and Deployment</span></span>

<span data-ttu-id="4e990-145">次の手順では、CI によってトリガーされるビルド定義を作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="4e990-145">The next procedure describes how to create a build definition that CI triggers.</span></span> <span data-ttu-id="4e990-146">ビルドが成功すると、カスタム MSBuild プロジェクトファイルのロジックを使用してソリューションが配置されます。</span><span class="sxs-lookup"><span data-stu-id="4e990-146">If the build succeeds, the solution is deployed using the logic in a custom MSBuild project file.</span></span>

<span data-ttu-id="4e990-147">**CI およびデプロイのビルド定義を作成するには**</span><span class="sxs-lookup"><span data-stu-id="4e990-147">**To create a build definition for CI and deployment**</span></span>

1. <span data-ttu-id="4e990-148">Visual Studio 2010 の **[チームエクスプローラー]** ウィンドウで、チームプロジェクトノードを展開し、 **[ビルド]** を右クリックして、 **[新しいビルド定義]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="4e990-148">In Visual Studio 2010, in the **Team Explorer** window, expand your team project node, right-click **Builds**, and then click **New Build Definition**.</span></span>

    ![](creating-a-build-definition-that-supports-deployment/_static/image2.png)
2. <span data-ttu-id="4e990-149">**[全般]** タブで、ビルド定義に名前 ( **deploytotest**など) とオプションの説明を指定します。</span><span class="sxs-lookup"><span data-stu-id="4e990-149">On the **General** tab, give the build definition a name (for example, **DeployToTest**) and an optional description.</span></span>
3. <span data-ttu-id="4e990-150">**[トリガー]** タブで、新しいビルドをトリガーする条件を選択します。</span><span class="sxs-lookup"><span data-stu-id="4e990-150">On the **Trigger** tab, select the criteria on which you want to trigger a new build.</span></span> <span data-ttu-id="4e990-151">たとえば、開発者が新しいコードをチェックインするたびにソリューションをビルドしてテスト環境に配置する場合は、 **[継続的インテグレーション]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="4e990-151">For example, if you want to build the solution and deploy to the test environment every time a developer checks in new code, select **Continuous Integration**.</span></span>
4. <span data-ttu-id="4e990-152">**[ビルドの既定値]** タブで、 **[ビルド出力を次の格納フォルダーにコピーする]** ボックスに、格納フォルダーの汎用名前付け規則 (UNC) パス (たとえば、 **\\TFSBUILD\Drops**) を入力します。</span><span class="sxs-lookup"><span data-stu-id="4e990-152">On the **Build Defaults** tab, in the **Copy build output to the following drop folder** box, type the Universal Naming Convention (UNC) path of your drop folder (for example, **\\TFSBUILD\Drops**).</span></span>

    ![](creating-a-build-definition-that-supports-deployment/_static/image3.png)

    > [!NOTE]
    > <span data-ttu-id="4e990-153">この格納場所には、構成する保持ポリシーに応じて複数のビルドが格納されます。</span><span class="sxs-lookup"><span data-stu-id="4e990-153">This drop location stores several builds, depending on the retention policy you configure.</span></span> <span data-ttu-id="4e990-154">特定のビルドからステージング環境または運用環境に配置アーティファクトを発行する場合は、ここで確認できます。</span><span class="sxs-lookup"><span data-stu-id="4e990-154">When you want to publish deployment artifacts from a specific build to a staging or production environment, this is where you'll find them.</span></span>
5. <span data-ttu-id="4e990-155">**[プロセス]** タブの **[ビルドプロセスファイル]** ドロップダウンリストで、 **[defaulttemplate .xaml]** を選択したままにします。</span><span class="sxs-lookup"><span data-stu-id="4e990-155">On the **Process** tab, in the **Build process file** dropdown list, leave **DefaultTemplate.xaml** selected.</span></span> <span data-ttu-id="4e990-156">これは、すべての新しいチームプロジェクトに追加される既定のビルドプロセステンプレートの1つです。</span><span class="sxs-lookup"><span data-stu-id="4e990-156">This is one of the default build process templates that get added to all new team projects.</span></span>
6. <span data-ttu-id="4e990-157">**[ビルドプロセスパラメーター]** テーブルで、 **[ビルドする項目]** 行をクリックし、**省略記号**ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="4e990-157">In the **Build process parameters** table, click in the **Items to Build** row, and then click the **ellipsis** button.</span></span>

    ![](creating-a-build-definition-that-supports-deployment/_static/image4.png)
7. <span data-ttu-id="4e990-158">**[ビルドする項目]** ダイアログボックスで、 **[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="4e990-158">In the **Items to Build** dialog box, click **Add**.</span></span>
8. <span data-ttu-id="4e990-159">ソリューションファイルの場所を参照し、[ **OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="4e990-159">Browse to the location of your solution file, and then click **OK**.</span></span>

    ![](creating-a-build-definition-that-supports-deployment/_static/image5.png)
9. <span data-ttu-id="4e990-160">**[ビルドする項目]** ダイアログボックスで、 **[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="4e990-160">In the **Items to Build** dialog box, click **Add**.</span></span>
10. <span data-ttu-id="4e990-161">**[項目の種類]** ボックスの一覧で、 **[MSBuild プロジェクトファイル]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="4e990-161">In the **Items of type** dropdown list, select **MSBuild Project files**.</span></span>
11. <span data-ttu-id="4e990-162">デプロイプロセスを制御するカスタムプロジェクトファイルの場所を参照し、ファイルを選択して、[ **OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="4e990-162">Browse to the location of the custom project file with which you control the deployment process, select the file, and then click **OK**.</span></span>

    ![](creating-a-build-definition-that-supports-deployment/_static/image6.png)
12. <span data-ttu-id="4e990-163">**[ビルドする項目]** ダイアログボックスに2つの項目が表示されるようになりました。</span><span class="sxs-lookup"><span data-stu-id="4e990-163">The **Items to Build** dialog box should now show two items.</span></span> <span data-ttu-id="4e990-164">**[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="4e990-164">Click **OK**.</span></span>

    ![](creating-a-build-definition-that-supports-deployment/_static/image7.png)
13. <span data-ttu-id="4e990-165">**[プロセス]** タブの **[ビルドプロセスパラメーター]** テーブルで、 **[詳細設定**] セクションを展開します。</span><span class="sxs-lookup"><span data-stu-id="4e990-165">On the **Process** tab, in the **Build process parameters** table, expand the **Advanced** section.</span></span>
14. <span data-ttu-id="4e990-166">**[Msbuild 引数]** 行に、ビルドする項目の*いずれか*に必要な msbuild コマンドライン引数を追加します。</span><span class="sxs-lookup"><span data-stu-id="4e990-166">In the **MSBuild Arguments** row, add any MSBuild command-line arguments that *either* of your items to build requires.</span></span> <span data-ttu-id="4e990-167">Contact Manager ソリューションのシナリオでは、次の引数が必要です。</span><span class="sxs-lookup"><span data-stu-id="4e990-167">In the Contact Manager solution scenario, these arguments are required:</span></span>

    [!code-console[Main](creating-a-build-definition-that-supports-deployment/samples/sample1.cmd)]

    ![](creating-a-build-definition-that-supports-deployment/_static/image8.png)
15. <span data-ttu-id="4e990-168">次の点に注意してください。</span><span class="sxs-lookup"><span data-stu-id="4e990-168">In this example:</span></span>

    1. <span data-ttu-id="4e990-169">Contact Manager ソリューションをビルドする場合は、 **Deployonbuild = true**および**deploytarget = package**引数が必要です。</span><span class="sxs-lookup"><span data-stu-id="4e990-169">The **DeployOnBuild=true** and **DeployTarget=package** arguments are required when you build the Contact Manager solution.</span></span> <span data-ttu-id="4e990-170">これにより、「 [Web アプリケーションプロジェクトのビルドおよびパッケージ化](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md)」で説明されているように、各 web アプリケーションプロジェクトをビルドした後に、web 配置パッケージを作成するよう MSBuild に指示します。</span><span class="sxs-lookup"><span data-stu-id="4e990-170">This instructs MSBuild to create web deployment packages after building each web application project, as described in [Building and Packaging Web Application Projects](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md).</span></span>
    2. <span data-ttu-id="4e990-171">**TargetEnvPropsFile**引数は、 *Publish*ファイルをビルドするときに必要です。</span><span class="sxs-lookup"><span data-stu-id="4e990-171">The **TargetEnvPropsFile** argument is required when you build the *Publish.proj* file.</span></span> <span data-ttu-id="4e990-172">このプロパティは、「[ビルドプロセスについ](../web-deployment-in-the-enterprise/understanding-the-build-process.md)て」で説明されているように、環境固有の構成ファイルの場所を示します。</span><span class="sxs-lookup"><span data-stu-id="4e990-172">This property indicates the location of the environment-specific configuration file, as described in [Understanding the Build Process](../web-deployment-in-the-enterprise/understanding-the-build-process.md).</span></span>
16. <span data-ttu-id="4e990-173">**[保持ポリシー]** タブで、必要に応じて保持する各種類のビルド数を構成します。</span><span class="sxs-lookup"><span data-stu-id="4e990-173">On the **Retention Policy** tab, configure how many builds of each type you want to retain as required.</span></span>
17. <span data-ttu-id="4e990-174">**[保存]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="4e990-174">Click **Save**.</span></span>

## <a name="queue-a-build"></a><span data-ttu-id="4e990-175">ビルドをキューに配置する</span><span class="sxs-lookup"><span data-stu-id="4e990-175">Queue a Build</span></span>

<span data-ttu-id="4e990-176">この時点で、少なくとも1つの新しいビルド定義が作成されています。</span><span class="sxs-lookup"><span data-stu-id="4e990-176">At this point, you have created at least one new build definition.</span></span> <span data-ttu-id="4e990-177">これで、定義したビルドプロセスが、ビルド定義で指定したトリガーに従って実行されるようになります。</span><span class="sxs-lookup"><span data-stu-id="4e990-177">The build process you defined will now run according to the triggers you specified in the build definition.</span></span>

<span data-ttu-id="4e990-178">CI を使用するようにビルド定義を構成した場合は、次の2つの方法でビルド定義をテストできます。</span><span class="sxs-lookup"><span data-stu-id="4e990-178">If you've configured your build definition to use CI, you can test your build definition in two ways:</span></span>

- <span data-ttu-id="4e990-179">一部のコンテンツをチームプロジェクトにチェックインして、自動ビルドをトリガーします。</span><span class="sxs-lookup"><span data-stu-id="4e990-179">Check in some content to the team project to trigger an automatic build.</span></span>
- <span data-ttu-id="4e990-180">ビルドを手動でキューに置いてください。</span><span class="sxs-lookup"><span data-stu-id="4e990-180">Queue a build manually.</span></span>

<span data-ttu-id="4e990-181">**ビルドを手動でキューに作成するには**</span><span class="sxs-lookup"><span data-stu-id="4e990-181">**To queue a build manually**</span></span>

1. <span data-ttu-id="4e990-182">**[チームエクスプローラー]** ウィンドウで、ビルド定義を右クリックし、 **[新しいビルドをキューに追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="4e990-182">In the **Team Explorer** window, right-click the build definition, and then click **Queue New Build**.</span></span>

    ![](creating-a-build-definition-that-supports-deployment/_static/image9.png)
2. <span data-ttu-id="4e990-183">**[ビルドのキュー]** ダイアログボックスで、ビルドのプロパティを確認し、 **[キュー]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="4e990-183">In the **Queue Build** dialog box, review the build properties, and then click **Queue**.</span></span>

    ![](creating-a-build-definition-that-supports-deployment/_static/image10.png)

<span data-ttu-id="4e990-184">手動でトリガーされたかどうかに&#x2014;関係なく、ビルドの進行状況と結果&#x2014;を確認するには、 **[チームエクスプローラー]** ウィンドウでビルド定義をダブルクリックします。</span><span class="sxs-lookup"><span data-stu-id="4e990-184">To review the progress and the outcome of a build&#x2014;regardless of whether it was triggered manually or automatically&#x2014;double-click the build definition in the **Team Explorer** window.</span></span> <span data-ttu-id="4e990-185">これにより、 **[ビルドエクスプローラー]** タブが開きます。</span><span class="sxs-lookup"><span data-stu-id="4e990-185">This will open a **Build Explorer** tab.</span></span>

![](creating-a-build-definition-that-supports-deployment/_static/image11.png)

<span data-ttu-id="4e990-186">ここから、失敗したビルドのトラブルシューティングを行うことができます。</span><span class="sxs-lookup"><span data-stu-id="4e990-186">From here, you can troubleshoot failed builds.</span></span> <span data-ttu-id="4e990-187">個々のビルドをダブルクリックすると、概要情報を表示したり、詳細なログファイルまでクリックしたりできます。</span><span class="sxs-lookup"><span data-stu-id="4e990-187">If you double-click an individual build, you can view summary information and click through to detailed log files.</span></span>

![](creating-a-build-definition-that-supports-deployment/_static/image12.png)

<span data-ttu-id="4e990-188">この情報を使用して、失敗したビルドをトラブルシューティングし、問題が解決されてから別のビルドを試みることができます。</span><span class="sxs-lookup"><span data-stu-id="4e990-188">You can use this information to troubleshoot failed builds and address any problems before you attempt another build.</span></span>

> [!NOTE]
> <span data-ttu-id="4e990-189">配置ロジックを実行するビルドは、対象となる環境で必要なアクセス許可をビルドサーバーに付与するまで、失敗する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="4e990-189">Builds that execute deployment logic are likely to fail until you have granted the build server any permissions required in the destination environment.</span></span> <span data-ttu-id="4e990-190">詳細については、「[チームビルドの配置のアクセス許可を構成する](configuring-permissions-for-team-build-deployment.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="4e990-190">For more information, see [Configuring Permissions for Team Build Deployment](configuring-permissions-for-team-build-deployment.md).</span></span>

## <a name="monitor-the-build-process"></a><span data-ttu-id="4e990-191">ビルドプロセスを監視する</span><span class="sxs-lookup"><span data-stu-id="4e990-191">Monitor the Build Process</span></span>

<span data-ttu-id="4e990-192">TFS には、ビルドプロセスを監視するのに役立つさまざまな機能が用意されています。</span><span class="sxs-lookup"><span data-stu-id="4e990-192">TFS provides a broad range of functionality to help you monitor the build process.</span></span> <span data-ttu-id="4e990-193">たとえば、TFS は、ビルドが完了すると、タスクバーの通知領域に電子メールを送信したり、警告を表示したりできます。</span><span class="sxs-lookup"><span data-stu-id="4e990-193">For example, TFS can send you an email or display alerts in your taskbar notification area when a build has completed.</span></span> <span data-ttu-id="4e990-194">詳細については、「[ビルドの実行と監視](https://msdn.microsoft.com/library/ms181721.aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="4e990-194">For more information, see [Run and Monitor Builds](https://msdn.microsoft.com/library/ms181721.aspx).</span></span>

## <a name="conclusion"></a><span data-ttu-id="4e990-195">まとめ</span><span class="sxs-lookup"><span data-stu-id="4e990-195">Conclusion</span></span>

<span data-ttu-id="4e990-196">このトピックでは、TFS でビルド定義を作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="4e990-196">This topic described how to create a build definition in TFS.</span></span> <span data-ttu-id="4e990-197">ビルド定義は CI 用に構成されているため、開発者がチームプロジェクトにコンテンツをチェックインするたびにビルドプロセスが実行されます。</span><span class="sxs-lookup"><span data-stu-id="4e990-197">The build definition is configured for CI, so the build process runs whenever a developer checks in content to the team project.</span></span> <span data-ttu-id="4e990-198">ビルド定義により、カスタム MSBuild プロジェクトファイルが実行され、web パッケージとデータベーススクリプトが対象サーバー環境に配置されます。</span><span class="sxs-lookup"><span data-stu-id="4e990-198">The build definition executes a custom MSBuild project file to deploy web packages and database scripts to a target server environment.</span></span>

<span data-ttu-id="4e990-199">自動配置をビルドプロセスの一部として成功させるには、ターゲット web サーバーとターゲットデータベースサーバーのビルドサービスアカウントに適切なアクセス許可を付与する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4e990-199">In order for an automated deployment to succeed as part of a build process, you'll need to grant appropriate permissions to the build service account on the target web servers and the target database server.</span></span> <span data-ttu-id="4e990-200">このチュートリアルの最後のトピック「[チームビルドの配置に対するアクセス許可の構成](configuring-permissions-for-team-build-deployment.md)」では、チームビルドサーバーからの自動配置に必要なアクセス許可を識別および構成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="4e990-200">The final topic in this tutorial, [Configuring Permissions for Team Build Deployment](configuring-permissions-for-team-build-deployment.md), describes how to identify and configure the permissions required for automated deployment from a Team Build server.</span></span>

## <a name="further-reading"></a><span data-ttu-id="4e990-201">参考資料</span><span class="sxs-lookup"><span data-stu-id="4e990-201">Further Reading</span></span>

<span data-ttu-id="4e990-202">ビルド定義の作成の詳細については、「[基本的なビルド定義の作成](https://msdn.microsoft.com/library/ms181716.aspx)」および「[ビルドプロセスの定義](https://msdn.microsoft.com/library/ms181715.aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="4e990-202">For more information on creating build definitions, see [Create a Basic Build Definition](https://msdn.microsoft.com/library/ms181716.aspx) and [Define Your Build Process](https://msdn.microsoft.com/library/ms181715.aspx).</span></span> <span data-ttu-id="4e990-203">ビルドをキューに追加する方法の詳細については、「[ビルドをキュー](https://msdn.microsoft.com/library/ms181722.aspx)に入れ」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="4e990-203">For more guidance on queuing builds, see [Queue a Build](https://msdn.microsoft.com/library/ms181722.aspx).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="4e990-204">[前へ](configuring-a-tfs-build-server-for-web-deployment.md)
> [次へ](deploying-a-specific-build.md)</span><span class="sxs-lookup"><span data-stu-id="4e990-204">[Previous](configuring-a-tfs-build-server-for-web-deployment.md)
[Next](deploying-a-specific-build.md)</span></span>
