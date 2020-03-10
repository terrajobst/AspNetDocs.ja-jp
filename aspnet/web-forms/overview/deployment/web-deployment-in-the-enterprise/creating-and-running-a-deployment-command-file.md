---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/creating-and-running-a-deployment-command-file
title: 配置コマンドファイルを作成して実行する |Microsoft Docs
author: jrjlee
description: このトピックでは、Microsoft Build Engine (MSBuild) プロジェクトファイルを使用してデプロイを実行できるようにするコマンドファイルを作成する方法について説明します。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: c61560e9-9f6c-4985-834a-08a3eabf9c3c
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/creating-and-running-a-deployment-command-file
msc.type: authoredcontent
ms.openlocfilehash: f1477ff423e4898385066a35b42503f3c70dcc68
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78514978"
---
# <a name="creating-and-running-a-deployment-command-file"></a><span data-ttu-id="32cbf-103">配置コマンド ファイルを作成し、実行する</span><span class="sxs-lookup"><span data-stu-id="32cbf-103">Creating and Running a Deployment Command File</span></span>

<span data-ttu-id="32cbf-104">[Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="32cbf-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

<span data-ttu-id="32cbf-105">[[Download PDF]\(PDF をダウンロード\)](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)</span><span class="sxs-lookup"><span data-stu-id="32cbf-105">[Download PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)</span></span>

> <span data-ttu-id="32cbf-106">このトピックでは、Microsoft Build Engine (MSBuild) プロジェクトファイルを使用して、単一ステップの反復可能なプロセスとして配置を実行できるようにするコマンドファイルを作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="32cbf-106">This topic describes how to build a command file that will let you run a deployment using Microsoft Build Engine (MSBuild) project files as a single-step, repeatable process.</span></span>

<span data-ttu-id="32cbf-107">このトピックでは、Fabrikam, Inc. という架空の企業のエンタープライズ展開要件に基づいて、一連のチュートリアルの一部を説明します。このチュートリアルシリーズでは、&#x2014; [Contact Manager](the-contact-manager-solution.md)ソリューション&#x2014;のサンプルソリューションを使用して、ASP.NET MVC 3 アプリケーション、Windows Communication Foundation (WCF) サービス、データベースプロジェクトなど、現実的なレベルの複雑さを持つ web アプリケーションを表します。</span><span class="sxs-lookup"><span data-stu-id="32cbf-107">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager](the-contact-manager-solution.md) solution&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

<span data-ttu-id="32cbf-108">これらのチュートリアルの中核となる配置方法は、「ビルド[プロセスについ](understanding-the-build-process.md)て」で説明されている「プロジェクトファイルの分割」の方法に基づいて&#x2014;います。この方法では、ビルドプロセスは、各配置先環境に適用されるビルド命令を含む2つのプロジェクトファイルと、環境固有のビルドおよび配置設定を含んでいます。</span><span class="sxs-lookup"><span data-stu-id="32cbf-108">The deployment method at the heart of these tutorials is based on the split project file approach described in [Understanding the Build Process](understanding-the-build-process.md), in which the build process is controlled by two project files&#x2014;one containing build instructions that apply to every destination environment, and one containing environment-specific build and deployment settings.</span></span> <span data-ttu-id="32cbf-109">ビルド時に、環境固有のプロジェクトファイルが環境に依存しないプロジェクトファイルにマージされ、ビルド命令の完全なセットが形成されます。</span><span class="sxs-lookup"><span data-stu-id="32cbf-109">At build time, the environment-specific project file is merged into the environment-agnostic project file to form a complete set of build instructions.</span></span>

## <a name="process-overview"></a><span data-ttu-id="32cbf-110">プロセスの概要</span><span class="sxs-lookup"><span data-stu-id="32cbf-110">Process Overview</span></span>

<span data-ttu-id="32cbf-111">このトピックでは、これらのプロジェクトファイルを使用するコマンドファイルを作成して実行し、ターゲット環境への反復可能なデプロイを実行する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="32cbf-111">In this topic, you'll learn how to create and run a command file that uses these project files to perform a repeatable deployment to your target environment.</span></span> <span data-ttu-id="32cbf-112">基本的に、コマンドファイルには、次のような MSBuild コマンドが含まれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="32cbf-112">Essentially, the command file simply needs to contain an MSBuild command that:</span></span>

- <span data-ttu-id="32cbf-113">環境に依存しない*パブリッシュの proj*ファイルを実行するよう MSBuild に指示します。</span><span class="sxs-lookup"><span data-stu-id="32cbf-113">Tells MSBuild to execute the environment-agnostic *Publish.proj* file.</span></span>
- <span data-ttu-id="32cbf-114">環境固有のプロジェクト設定を含むファイルと、それを検索する場所を指定します *。*</span><span class="sxs-lookup"><span data-stu-id="32cbf-114">Tells the *Publish.proj* file which file contains the environment-specific project settings and where to find it.</span></span>

## <a name="create-an-msbuild-command"></a><span data-ttu-id="32cbf-115">MSBuild コマンドを作成する</span><span class="sxs-lookup"><span data-stu-id="32cbf-115">Create an MSBuild Command</span></span>

<span data-ttu-id="32cbf-116">「[ビルドプロセスについ](understanding-the-build-process.md)て」で説明されているよう&#x2014;に、環境固有のプロジェクトファイル (例: *Env-Dev. proj*&#x2014;) は、ビルド時に環境に依存しない*発行 proj*ファイルにインポートするように設計されています。</span><span class="sxs-lookup"><span data-stu-id="32cbf-116">As described in [Understanding the Build Process](understanding-the-build-process.md), the environment-specific project file&#x2014;for example, *Env-Dev.proj*&#x2014;is designed to be imported into the environment-agnostic *Publish.proj* file at build time.</span></span> <span data-ttu-id="32cbf-117">これらの2つのファイルは、MSBuild にソリューションのビルド方法と配置方法を指示する完全な命令セットを提供します。</span><span class="sxs-lookup"><span data-stu-id="32cbf-117">Together, these two files provide a complete set of instructions that tell MSBuild how to build and deploy your solution.</span></span>

<span data-ttu-id="32cbf-118">*Publish*ファイルは、 **import**要素を使用して、環境固有のプロジェクトファイルをインポートします。</span><span class="sxs-lookup"><span data-stu-id="32cbf-118">The *Publish.proj* file uses an **Import** element to import the environment-specific project file.</span></span>

[!code-xml[Main](creating-and-running-a-deployment-command-file/samples/sample1.xml)]

<span data-ttu-id="32cbf-119">そのため、Msbuild.exe を使用して Contact Manager ソリューションをビルドおよび配置する場合は、次のことを行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="32cbf-119">As such, when you use MSBuild.exe to build and deploy the Contact Manager solution, you need to:</span></span>

- <span data-ttu-id="32cbf-120">Mstest.exe ファイルで Msbuild.exe を実行し*ます。*</span><span class="sxs-lookup"><span data-stu-id="32cbf-120">Run MSBuild.exe on the *Publish.proj* file.</span></span>
- <span data-ttu-id="32cbf-121">**TargetEnvPropsFile**という名前のコマンドラインパラメーターを指定して、環境固有のプロジェクトファイルの場所を指定します。</span><span class="sxs-lookup"><span data-stu-id="32cbf-121">Specify the location of the environment-specific project file by supplying a command-line parameter named **TargetEnvPropsFile**.</span></span>

<span data-ttu-id="32cbf-122">これを行うには、MSBuild コマンドは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="32cbf-122">To do this, your MSBuild command should resemble this:</span></span>

[!code-console[Main](creating-and-running-a-deployment-command-file/samples/sample2.cmd)]

<span data-ttu-id="32cbf-123">ここからは、反復可能な単一ステップのデプロイに移行するための簡単な手順です。</span><span class="sxs-lookup"><span data-stu-id="32cbf-123">From here, it's a simple step to move to a repeatable, single-step deployment.</span></span> <span data-ttu-id="32cbf-124">必要な作業は、MSBuild コマンドを .cmd ファイルに追加することだけです。</span><span class="sxs-lookup"><span data-stu-id="32cbf-124">All you need to do is to add your MSBuild command to a .cmd file.</span></span> <span data-ttu-id="32cbf-125">Contact Manager ソリューションで、Publish フォルダーには、 *Publish-Dev*という名前のファイルが含まれています。</span><span class="sxs-lookup"><span data-stu-id="32cbf-125">In the Contact Manager solution, the Publish folder includes a file named *Publish-Dev.cmd* that does exactly this.</span></span>

[!code-console[Main](creating-and-running-a-deployment-command-file/samples/sample3.cmd)]

> [!NOTE]
> <span data-ttu-id="32cbf-126">**/Fl**スイッチは、msbuild.exe が呼び出された作業ディレクトリ*に msbuild.exe という名前*のログファイルを作成するよう msbuild に指示します。</span><span class="sxs-lookup"><span data-stu-id="32cbf-126">The **/fl** switch instructs MSBuild to create a log file named *msbuild.log* in the working directory in which MSBuild.exe was invoked.</span></span>

<span data-ttu-id="32cbf-127">Contact Manager ソリューションを配置または再配置するには、 *Publish-Dev*ファイルを実行するだけです。</span><span class="sxs-lookup"><span data-stu-id="32cbf-127">To deploy or redeploy the Contact Manager solution, all you need to do is run the *Publish-Dev.cmd* file.</span></span> <span data-ttu-id="32cbf-128">ファイルを実行すると、MSBuild は次のことを行います。</span><span class="sxs-lookup"><span data-stu-id="32cbf-128">When you run the file, MSBuild will:</span></span>

- <span data-ttu-id="32cbf-129">ソリューション内のすべてのプロジェクトをビルドします。</span><span class="sxs-lookup"><span data-stu-id="32cbf-129">Build all the projects in the solution.</span></span>
- <span data-ttu-id="32cbf-130">Web アプリケーションプロジェクトの配置可能な web パッケージを生成します。</span><span class="sxs-lookup"><span data-stu-id="32cbf-130">Generate deployable web packages for the web application projects.</span></span>
- <span data-ttu-id="32cbf-131">データベースプロジェクトの .dbschema ファイルと deploymanifest ファイルを生成します。</span><span class="sxs-lookup"><span data-stu-id="32cbf-131">Generate .dbschema and .deploymanifest files for the database projects.</span></span>
- <span data-ttu-id="32cbf-132">Web パッケージを web サーバーに配置します。</span><span class="sxs-lookup"><span data-stu-id="32cbf-132">Deploy the web packages to the web server.</span></span>
- <span data-ttu-id="32cbf-133">データベースをデータベースサーバーに配置します。</span><span class="sxs-lookup"><span data-stu-id="32cbf-133">Deploy the database to the database server.</span></span>

## <a name="run-the-deployment"></a><span data-ttu-id="32cbf-134">デプロイを実行する</span><span class="sxs-lookup"><span data-stu-id="32cbf-134">Run the Deployment</span></span>

<span data-ttu-id="32cbf-135">ターゲット環境のコマンドファイルを作成したら、ファイルを実行するだけで配置全体を完了できるようになります。</span><span class="sxs-lookup"><span data-stu-id="32cbf-135">When you've created a command file for your target environment, you should be able to complete the entire deployment by simply running the file.</span></span>

<span data-ttu-id="32cbf-136">**連絡先マネージャーソリューションをテスト環境に配置するには**</span><span class="sxs-lookup"><span data-stu-id="32cbf-136">**To deploy the Contact Manager solution to your test environment**</span></span>

1. <span data-ttu-id="32cbf-137">開発者ワークステーションでエクスプローラーを開き、 *Publish-Dev*ファイルの場所を参照します。</span><span class="sxs-lookup"><span data-stu-id="32cbf-137">On your developer workstation, open Windows Explorer, and then browse to the location of the *Publish-Dev.cmd* file.</span></span>
2. <span data-ttu-id="32cbf-138">ファイルをダブルクリックして実行します。</span><span class="sxs-lookup"><span data-stu-id="32cbf-138">Double-click the file to run it.</span></span>
3. <span data-ttu-id="32cbf-139">**[ファイルを開く-セキュリティの警告]** ダイアログボックスが表示されたら、 **[実行]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="32cbf-139">If an **Open File – Security Warning** dialog box appears, click **Run**.</span></span>
4. <span data-ttu-id="32cbf-140">構成設定とテストサーバーが正しく設定されている場合、MSBuild がプロジェクトファイルの処理を完了すると、コマンドプロンプトウィンドウに "**ビルドが成功しまし**た" というメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="32cbf-140">If your configuration settings and test servers are set up correctly, the Command Prompt window will show a **Build succeeded** message when MSBuild has finished processing the project files.</span></span>

    ![](creating-and-running-a-deployment-command-file/_static/image1.png)
5. <span data-ttu-id="32cbf-141">この環境にソリューションを初めてデプロイした場合は、テスト用の web サーバーマシンアカウントをデータベース **\_datawriter**と**Db\_datareader** **マネージャー**データベースに追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="32cbf-141">If this is the first time you've deployed the solution to this environment, you'll need to add the test web server machine account to the **db\_datawriter** and **db\_datareader** roles on the **ContactManager** database.</span></span> <span data-ttu-id="32cbf-142">この手順につい[ては、「Configure a Database Server for Web 配置 Publishing](../configuring-server-environments-for-web-deployment/configuring-a-database-server-for-web-deploy-publishing.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="32cbf-142">This procedure is described in [Configure a Database Server for Web Deploy Publishing](../configuring-server-environments-for-web-deployment/configuring-a-database-server-for-web-deploy-publishing.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="32cbf-143">これらのアクセス許可は、データベースの作成時にのみ割り当てる必要があります。</span><span class="sxs-lookup"><span data-stu-id="32cbf-143">You only need to assign these permissions when you create the database.</span></span> <span data-ttu-id="32cbf-144">既定では、ビルドプロセスは、すべての配置&#x2014;でデータベースを再作成するのではなく、既存のデータベースを最新のスキーマと比較し、必要な変更のみを行います。</span><span class="sxs-lookup"><span data-stu-id="32cbf-144">By default, the build process will not recreate the database on every deployment&#x2014;instead, it will compare the existing database to the latest schema and make only the changes required.</span></span> <span data-ttu-id="32cbf-145">そのため、初めてソリューションを配置するときは、これらのデータベースロールをマップする必要があります。</span><span class="sxs-lookup"><span data-stu-id="32cbf-145">As a result, you should only need to map these database roles the first time you deploy the solution.</span></span>
6. <span data-ttu-id="32cbf-146">Internet Explorer を開き、Contact Manager アプリケーションの URL (`http://testweb1:85/ContactManager/`など) を参照します。</span><span class="sxs-lookup"><span data-stu-id="32cbf-146">Open Internet Explorer and browse to the URL of the Contact Manager application (for example, `http://testweb1:85/ContactManager/`).</span></span>
7. <span data-ttu-id="32cbf-147">アプリケーションが想定どおりに動作し、連絡先を追加できることを確認します。</span><span class="sxs-lookup"><span data-stu-id="32cbf-147">Verify that the application works as expected and you're able to add contacts.</span></span>

    ![](creating-and-running-a-deployment-command-file/_static/image2.png)

## <a name="conclusion"></a><span data-ttu-id="32cbf-148">まとめ</span><span class="sxs-lookup"><span data-stu-id="32cbf-148">Conclusion</span></span>

<span data-ttu-id="32cbf-149">MSBuild の手順を含むコマンドファイルを作成すると、複数のプロジェクトから成るソリューションを特定の配置先の環境に簡単かつ簡単に構築してデプロイすることができます。</span><span class="sxs-lookup"><span data-stu-id="32cbf-149">Creating a command file containing your MSBuild instructions provides you with a quick and easy way of building and deploying a multi-project solution to a specific destination environment.</span></span> <span data-ttu-id="32cbf-150">複数の移行先環境にソリューションを繰り返しデプロイする必要がある場合は、複数のコマンドファイルを作成できます。</span><span class="sxs-lookup"><span data-stu-id="32cbf-150">If you need to repeatedly deploy your solution to multiple destination environments, you can create multiple command files.</span></span> <span data-ttu-id="32cbf-151">各コマンドファイルでは、MSBuild コマンドによって同じユニバーサルプロジェクトファイルがビルドされますが、環境固有の別のプロジェクトファイルが指定されます。</span><span class="sxs-lookup"><span data-stu-id="32cbf-151">In each command file, the MSBuild command will build the same universal project file, but it will specify a different environment-specific project file.</span></span> <span data-ttu-id="32cbf-152">たとえば、開発者またはテスト環境に発行するコマンドファイルには、次の MSBuild コマンドを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="32cbf-152">For example, a command file to publish to a developer or test environment might contain this MSBuild command:</span></span>

[!code-console[Main](creating-and-running-a-deployment-command-file/samples/sample4.cmd)]

<span data-ttu-id="32cbf-153">ステージング環境に発行するためのコマンドファイルには、次の MSBuild コマンドが含まれる場合があります。</span><span class="sxs-lookup"><span data-stu-id="32cbf-153">A command file to publish to a staging environment might contain this MSBuild command:</span></span>

[!code-console[Main](creating-and-running-a-deployment-command-file/samples/sample5.cmd)]

> [!NOTE]
> <span data-ttu-id="32cbf-154">独自のサーバー環境用に環境固有のプロジェクトファイルをカスタマイズする方法については、「[ターゲット環境の配置プロパティを構成](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md)する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="32cbf-154">For guidance on how to customize the environment-specific project files for your own server environments, see [Configure Deployment Properties for a Target Environment](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md).</span></span>

<span data-ttu-id="32cbf-155">また、プロパティをオーバーライドしたり、MSBuild コマンドで他のさまざまなスイッチを設定したりして、各環境のビルドプロセスをカスタマイズすることもできます。</span><span class="sxs-lookup"><span data-stu-id="32cbf-155">You can also customize the build process for each environment by overriding properties or setting various other switches in your MSBuild command.</span></span> <span data-ttu-id="32cbf-156">詳細については、「 [MSBuild コマンドラインリファレンス](https://msdn.microsoft.com/library/ms164311.aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="32cbf-156">For more information, see [MSBuild Command Line Reference](https://msdn.microsoft.com/library/ms164311.aspx).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="32cbf-157">[前へ](deploying-database-projects.md)
> [次へ](manually-installing-web-packages.md)</span><span class="sxs-lookup"><span data-stu-id="32cbf-157">[Previous](deploying-database-projects.md)
[Next](manually-installing-web-packages.md)</span></span>
