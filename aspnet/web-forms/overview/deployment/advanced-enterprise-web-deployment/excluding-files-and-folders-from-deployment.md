---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/excluding-files-and-folders-from-deployment
title: ファイルとフォルダーを配置から除外する |Microsoft Docs
author: jrjlee
description: このトピックでは、web アプリケーションプロジェクトをビルドしてパッケージ化するときに、web 配置パッケージからファイルとフォルダーを除外する方法について説明します。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: f4cc2d40-6a78-429b-b06f-07d000d4caad
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/excluding-files-and-folders-from-deployment
msc.type: authoredcontent
ms.openlocfilehash: a262ce43d7199fb1015d54d0b7c213857c360946
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78438418"
---
# <a name="excluding-files-and-folders-from-deployment"></a><span data-ttu-id="ed7b1-103">配置からファイルとフォルダーを除外する</span><span class="sxs-lookup"><span data-stu-id="ed7b1-103">Excluding Files and Folders from Deployment</span></span>

<span data-ttu-id="ed7b1-104">[Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="ed7b1-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

<span data-ttu-id="ed7b1-105">[[Download PDF]\(PDF をダウンロード\)](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)</span><span class="sxs-lookup"><span data-stu-id="ed7b1-105">[Download PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)</span></span>

> <span data-ttu-id="ed7b1-106">このトピックでは、web アプリケーションプロジェクトをビルドしてパッケージ化するときに、web 配置パッケージからファイルとフォルダーを除外する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="ed7b1-106">This topic describes how you can exclude files and folders from a web deployment package when you build and package a web application project.</span></span>

<span data-ttu-id="ed7b1-107">このトピックでは、Fabrikam, Inc. という架空の企業のエンタープライズ展開要件に基づいて、一連のチュートリアルの一部を説明します。このチュートリアルシリーズでは、&#x2014; [Contact Manager ソリューション](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;のサンプルソリューションを使用して、ASP.NET MVC 3 アプリケーション、Windows Communication Foundation (WCF) サービス、データベースプロジェクトなど、現実的なレベルの複雑さを持つ web アプリケーションを表します。</span><span class="sxs-lookup"><span data-stu-id="ed7b1-107">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

<span data-ttu-id="ed7b1-108">これらのチュートリアルの中核となる配置方法は、「[プロジェクトファイルについ](../web-deployment-in-the-enterprise/understanding-the-project-file.md)て」で説明されている分割プロジェクトファイルアプローチに基づいています。この&#x2014;プロジェクトファイルには、ビルドプロセスは、すべての変換先環境に適用されるビルド命令を含む2つのプロジェクトファイルと、環境固有のビルドおよび配置設定を含んでいます。</span><span class="sxs-lookup"><span data-stu-id="ed7b1-108">The deployment method at the heart of these tutorials is based on the split project file approach described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md), in which the build process is controlled by two project files&#x2014;one containing build instructions that apply to every destination environment, and one containing environment-specific build and deployment settings.</span></span> <span data-ttu-id="ed7b1-109">ビルド時に、環境固有のプロジェクトファイルが環境に依存しないプロジェクトファイルにマージされ、ビルド命令の完全なセットが形成されます。</span><span class="sxs-lookup"><span data-stu-id="ed7b1-109">At build time, the environment-specific project file is merged into the environment-agnostic project file to form a complete set of build instructions.</span></span>

## <a name="overview"></a><span data-ttu-id="ed7b1-110">概要</span><span class="sxs-lookup"><span data-stu-id="ed7b1-110">Overview</span></span>

<span data-ttu-id="ed7b1-111">Visual Studio 2010 で web アプリケーションプロジェクトをビルドする場合、Web 発行パイプライン (WPP) を使用すると、コンパイルされた web アプリケーションを展開可能な web パッケージにパッケージ化することによって、このビルドプロセスを拡張できます。</span><span class="sxs-lookup"><span data-stu-id="ed7b1-111">When you build a web application project in Visual Studio 2010, the Web Publishing Pipeline (WPP) lets you extend this build process by packaging your compiled web application into a deployable web package.</span></span> <span data-ttu-id="ed7b1-112">その後、インターネットインフォメーションサービス (IIS) Web 配置ツール (Web 配置) を使用して、この web パッケージをリモート IIS web サーバーに展開したり、IIS マネージャーを使用して手動でインポートしたりできます。</span><span class="sxs-lookup"><span data-stu-id="ed7b1-112">You can then use the Internet Information Services (IIS) Web Deployment Tool (Web Deploy) to deploy this web package to a remote IIS web server, or import the web package manually through IIS Manager.</span></span> <span data-ttu-id="ed7b1-113">このパッケージ化プロセスについ[ては、「Web アプリケーションプロジェクトのビルドおよびパッケージ化](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md)」で説明されています。</span><span class="sxs-lookup"><span data-stu-id="ed7b1-113">This packaging process is explained in [Building and Packaging Web Application Projects](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md).</span></span>

<span data-ttu-id="ed7b1-114">では、どのようにして web パッケージに含まれるのかを制御するにはどうすればよいでしょうか。</span><span class="sxs-lookup"><span data-stu-id="ed7b1-114">So how do you control what gets included in your web package?</span></span> <span data-ttu-id="ed7b1-115">Visual Studio のプロジェクト設定は、基になるプロジェクトファイルを通じて、多数のシナリオに十分な制御を提供します。</span><span class="sxs-lookup"><span data-stu-id="ed7b1-115">The project settings in Visual Studio, through the underlying project file, provide sufficient control for a lot of scenarios.</span></span> <span data-ttu-id="ed7b1-116">ただし、場合によっては、web パッケージのコンテンツを特定の配置先環境に合わせて調整する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ed7b1-116">However, in some cases you may want to tailor the contents of your web package to specific destination environments.</span></span> <span data-ttu-id="ed7b1-117">たとえば、アプリケーションをテスト環境に配置するときにログファイルのフォルダーを含め、ステージング環境または運用環境にアプリケーションを配置するときにそのフォルダーを除外することができます。</span><span class="sxs-lookup"><span data-stu-id="ed7b1-117">For example, you might want to include a folder for log files when you deploy your application to a test environment but exclude the folder when you deploy the application to a staging or production environment.</span></span> <span data-ttu-id="ed7b1-118">このトピックでは、その方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="ed7b1-118">This topic will show you how to do this.</span></span>

## <a name="what-gets-included-by-default"></a><span data-ttu-id="ed7b1-119">既定では何が含まれますか。</span><span class="sxs-lookup"><span data-stu-id="ed7b1-119">What Gets Included by Default?</span></span>

<span data-ttu-id="ed7b1-120">Visual Studio で web アプリケーションプロジェクトのプロパティを構成すると、 **[パッケージ/発行]** ページの **[配置する項目]** の一覧で、web 配置パッケージに含める内容を指定できます。</span><span class="sxs-lookup"><span data-stu-id="ed7b1-120">When you configure your web application project properties in Visual Studio, the **Items to deploy** list on the **Package/Publish Web** page lets you specify what you want to include in your web deployment package.</span></span> <span data-ttu-id="ed7b1-121">既定では、このアプリケーションを**実行するために必要なファイルのみ**に設定されます。</span><span class="sxs-lookup"><span data-stu-id="ed7b1-121">By default, this is set to **Only files needed to run this application**.</span></span>

![](excluding-files-and-folders-from-deployment/_static/image1.png)

<span data-ttu-id="ed7b1-122">**このアプリケーションの実行に必要なファイルのみ**を選択した場合、WPP は web パッケージに追加するファイルを決定しようとします。</span><span class="sxs-lookup"><span data-stu-id="ed7b1-122">When you choose **Only files needed to run this application**, the WPP will try to determine which files should be added to the web package.</span></span> <span data-ttu-id="ed7b1-123">これには次のものが含まれます</span><span class="sxs-lookup"><span data-stu-id="ed7b1-123">This includes:</span></span>

- <span data-ttu-id="ed7b1-124">プロジェクトのすべてのビルド出力。</span><span class="sxs-lookup"><span data-stu-id="ed7b1-124">All the build outputs for the project.</span></span>
- <span data-ttu-id="ed7b1-125">**コンテンツ**のビルドアクションでマークされたファイル。</span><span class="sxs-lookup"><span data-stu-id="ed7b1-125">Any files marked with a build action of **Content**.</span></span>

> [!NOTE]
> <span data-ttu-id="ed7b1-126">このファイルには、含めるファイルを決定するロジックが含まれています。</span><span class="sxs-lookup"><span data-stu-id="ed7b1-126">The logic that determines which files to include is contained in this file:</span></span>   
> <span data-ttu-id="ed7b1-127">*%PROGRAMFILES%\MSBuild\Microsoft\VisualStudio\v10.0\Web\.........*</span><span class="sxs-lookup"><span data-stu-id="ed7b1-127">*%PROGRAMFILES%\MSBuild\Microsoft\VisualStudio\v10.0\Web\ Microsoft.Web.Publishing.OnlyFilesToRunTheApp.targets*</span></span>

## <a name="excluding-specific-files-and-folders"></a><span data-ttu-id="ed7b1-128">特定のファイルとフォルダーを除外する</span><span class="sxs-lookup"><span data-stu-id="ed7b1-128">Excluding Specific Files and Folders</span></span>

<span data-ttu-id="ed7b1-129">場合によっては、どのファイルとフォルダーを展開するかをきめ細かく制御する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ed7b1-129">In some cases, you'll want more fine-grained control over which files and folders are deployed.</span></span> <span data-ttu-id="ed7b1-130">事前に除外するファイルがわかっていて、その除外がすべての変換先環境に適用される場合は、各ファイルの**ビルドアクション**を**None**に設定するだけで済みます。</span><span class="sxs-lookup"><span data-stu-id="ed7b1-130">If you know which files you want to exclude ahead of time, and the exclusion applies to all destination environments, you can simply set the **Build Action** of each file to **None**.</span></span>

<span data-ttu-id="ed7b1-131">**特定のファイルを配置から除外するには**</span><span class="sxs-lookup"><span data-stu-id="ed7b1-131">**To exclude specific files from deployment**</span></span>

1. <span data-ttu-id="ed7b1-132">**[ソリューションエクスプローラー]** ウィンドウで、ファイルを右クリックし、 **[プロパティ]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="ed7b1-132">In the **Solution Explorer** window, right-click the file, and then click **Properties**.</span></span>
2. <span data-ttu-id="ed7b1-133">**[プロパティ]** ウィンドウの **[ビルドアクション]** 行で、 **[なし]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="ed7b1-133">In the **Properties** window, in the **Build Action** row, select **None**.</span></span>

<span data-ttu-id="ed7b1-134">ただし、この方法は常に便利であるとは限りません。</span><span class="sxs-lookup"><span data-stu-id="ed7b1-134">However, this approach is not always convenient.</span></span> <span data-ttu-id="ed7b1-135">たとえば、配置先の環境に応じて、または Visual Studio の外部から、どのファイルとフォルダーを含めるかを変更することができます。</span><span class="sxs-lookup"><span data-stu-id="ed7b1-135">For example, you may want to vary which files and folders are included according to your destination environment, and from outside Visual Studio.</span></span> <span data-ttu-id="ed7b1-136">たとえば、Contact Manager サンプルソリューションで、ContactManager. Mvc プロジェクトの内容を確認します。</span><span class="sxs-lookup"><span data-stu-id="ed7b1-136">For example, in the Contact Manager sample solution, take a look at the contents of the ContactManager.Mvc project:</span></span>

![](excluding-files-and-folders-from-deployment/_static/image2.png)

- <span data-ttu-id="ed7b1-137">内部フォルダーには、開発者が開発目的でローカルデータベースを作成、削除、および設定するために使用する SQL スクリプトが含まれています。</span><span class="sxs-lookup"><span data-stu-id="ed7b1-137">The Internal folder contains some SQL scripts that the developer uses to create, drop, and populate local databases for development purposes.</span></span> <span data-ttu-id="ed7b1-138">このフォルダー内の何も、ステージング環境または運用環境に配置することはできません。</span><span class="sxs-lookup"><span data-stu-id="ed7b1-138">Nothing in this folder should be deployed to a staging or production environment.</span></span>
- <span data-ttu-id="ed7b1-139">Scripts フォルダーには、いくつかの JavaScript ファイルが含まれています。</span><span class="sxs-lookup"><span data-stu-id="ed7b1-139">The Scripts folder contains several JavaScript files.</span></span> <span data-ttu-id="ed7b1-140">これらのファイルの大部分は、Visual Studio でのデバッグまたは IntelliSense の提供をサポートするためにのみ含まれています。</span><span class="sxs-lookup"><span data-stu-id="ed7b1-140">A lot of these files are included purely to support debugging or provide IntelliSense in Visual Studio.</span></span> <span data-ttu-id="ed7b1-141">これらのファイルの一部は、ステージング環境または運用環境に配置しないでください。</span><span class="sxs-lookup"><span data-stu-id="ed7b1-141">Some of these files should not be deployed to staging or production environments.</span></span> <span data-ttu-id="ed7b1-142">ただし、トラブルシューティングを容易にするために、開発者向けテスト環境に配置することもできます。</span><span class="sxs-lookup"><span data-stu-id="ed7b1-142">However, you may want to deploy them to a developer test environment to facilitate troubleshooting.</span></span>

<span data-ttu-id="ed7b1-143">プロジェクトファイルを操作して特定のファイルやフォルダーを除外することもできますが、簡単な方法があります。</span><span class="sxs-lookup"><span data-stu-id="ed7b1-143">Although you could manipulate your project files to exclude specific files and folders, there is an easier way.</span></span> <span data-ttu-id="ed7b1-144">WPP には、 **ExcludeFromPackageFolders**および**ExcludeFromPackageFiles**という名前の項目リストを作成してファイルとフォルダーを除外する機構が含まれています。</span><span class="sxs-lookup"><span data-stu-id="ed7b1-144">The WPP includes a mechanism to exclude files and folders by building item lists named **ExcludeFromPackageFolders** and **ExcludeFromPackageFiles**.</span></span> <span data-ttu-id="ed7b1-145">これらのリストに独自の項目を追加することで、この機構を拡張できます。</span><span class="sxs-lookup"><span data-stu-id="ed7b1-145">You can extend this mechanism by adding your own items to these lists.</span></span> <span data-ttu-id="ed7b1-146">これを行うには、次の大まかな手順を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ed7b1-146">To do this, you need to complete these high-level steps:</span></span>

1. <span data-ttu-id="ed7b1-147">プロジェクトファイルと同じフォルダーに、 *[project name] wpp*という名前のカスタムプロジェクトファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="ed7b1-147">Create a custom project file named *[project name].wpp.targets* in the same folder as your project file.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ed7b1-148">*.Targets*ファイルは、web アプリケーションプロジェクトファイル&#x2014;と同じフォルダーに配置する必要があります。たとえば、ビルドと配置のプロセスを制御するために使用するカスタムプロジェクトファイルと同じフォルダーではなく、 *contactmanager. .csproj*&#x2014;というフォルダーにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="ed7b1-148">The *.wpp.targets* file needs to go in the same folder as your web application project file&#x2014;for example, *ContactManager.Mvc.csproj*&#x2014;rather than in the same folder as any custom project files you use to control the build and deployment process.</span></span>
2. <span data-ttu-id="ed7b1-149">**ItemGroup**ファイル*で*、要素を追加します。</span><span class="sxs-lookup"><span data-stu-id="ed7b1-149">In the *.wpp.targets* file, add an **ItemGroup** element.</span></span>
3. <span data-ttu-id="ed7b1-150">**ItemGroup**要素で、必要に応じて特定のファイルとフォルダーを除外するために、 **ExcludeFromPackageFolders**と**ExcludeFromPackageFiles**の項目を追加します。</span><span class="sxs-lookup"><span data-stu-id="ed7b1-150">In the **ItemGroup** element, add **ExcludeFromPackageFolders** and **ExcludeFromPackageFiles** items to exclude specific files and folders as required.</span></span>

<span data-ttu-id="ed7b1-151">*このファイルの*基本的な構造は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="ed7b1-151">This is the basic structure of this *.wpp.targets* file:</span></span>

[!code-xml[Main](excluding-files-and-folders-from-deployment/samples/sample1.xml)]

<span data-ttu-id="ed7b1-152">各項目には、 **Fromtarget**という名前の項目メタデータ要素が含まれていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="ed7b1-152">Note that each item includes an item metadata element named **FromTarget**.</span></span> <span data-ttu-id="ed7b1-153">これは、ビルドプロセスに影響しない省略可能な値です。これは、他のユーザーがビルドログをレビューしたときに特定のファイルやフォルダーが省略された理由を示すためにのみ機能します。</span><span class="sxs-lookup"><span data-stu-id="ed7b1-153">This is an optional value that doesn't affect the build process; it simply serves to indicate why particular files or folders were omitted if someone reviews the build logs.</span></span>

## <a name="excluding-files-and-folders-from-a-web-package"></a><span data-ttu-id="ed7b1-154">Web パッケージからのファイルとフォルダーの除外</span><span class="sxs-lookup"><span data-stu-id="ed7b1-154">Excluding Files and Folders from a Web Package</span></span>

<span data-ttu-id="ed7b1-155">次の手順では、web アプリケーションプロジェクトに*wpp*ファイルを追加する方法と、プロジェクトをビルドするときにファイルを使用して web パッケージから特定のファイルとフォルダーを除外する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="ed7b1-155">The next procedure shows you how to add a *.wpp.targets* file to a web application project and how to use the file to exclude specific files and folders from the web package when you build your project.</span></span>

<span data-ttu-id="ed7b1-156">**ファイルとフォルダーを web 配置パッケージから除外するには**</span><span class="sxs-lookup"><span data-stu-id="ed7b1-156">**To exclude files and folders from a web deployment package**</span></span>

1. <span data-ttu-id="ed7b1-157">Visual Studio 2010 でソリューションを開きます。</span><span class="sxs-lookup"><span data-stu-id="ed7b1-157">Open your solution in Visual Studio 2010.</span></span>
2. <span data-ttu-id="ed7b1-158">**[ソリューションエクスプローラー]** ウィンドウで、web アプリケーションプロジェクトノード ( **contactmanager**など) を右クリックし、 **[追加]** をポイントして、 **[新しい項目]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="ed7b1-158">In the **Solution Explorer** window, right-click your web application project node (for example, **ContactManager.Mvc**), point to **Add**, and then click **New Item**.</span></span>
3. <span data-ttu-id="ed7b1-159">**[新しい項目の追加]** ダイアログボックスで、 **[XML ファイル]** テンプレートを選択します。</span><span class="sxs-lookup"><span data-stu-id="ed7b1-159">In the **Add New Item** dialog box, select the **XML File** template.</span></span>
4. <span data-ttu-id="ed7b1-160">**[名前]** ボックスに「 \*[project Name] \* \* \*\* を使用します。」と入力し (たとえば、 **contactmanager. Mvc. wpp**)、 **[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="ed7b1-160">In the **Name** box, type *[project name]\*\*\*.wpp.targets*\* (for example, **ContactManager.Mvc.wpp.targets**), and then click **Add**.</span></span>

    ![](excluding-files-and-folders-from-deployment/_static/image3.png)

    > [!NOTE]
    > <span data-ttu-id="ed7b1-161">プロジェクトのルートノードに新しい項目を追加すると、そのファイルはプロジェクトファイルと同じフォルダーに作成されます。</span><span class="sxs-lookup"><span data-stu-id="ed7b1-161">If you add a new item to the root node of a project, the file is created in the same folder as the project file.</span></span> <span data-ttu-id="ed7b1-162">これを確認するには、エクスプローラーでフォルダーを開きます。</span><span class="sxs-lookup"><span data-stu-id="ed7b1-162">You can verify this by opening the folder in Windows Explorer.</span></span>
5. <span data-ttu-id="ed7b1-163">ファイルで、**プロジェクト**要素と**ItemGroup**要素を追加します。</span><span class="sxs-lookup"><span data-stu-id="ed7b1-163">In the file, add a **Project** element and an **ItemGroup** element:</span></span>

    [!code-xml[Main](excluding-files-and-folders-from-deployment/samples/sample2.xml)]
6. <span data-ttu-id="ed7b1-164">Web パッケージからフォルダーを除外する場合は、 **ItemGroup**要素に**ExcludeFromPackageFolders**要素を追加します。</span><span class="sxs-lookup"><span data-stu-id="ed7b1-164">If you want to exclude folders from the web package, add an **ExcludeFromPackageFolders** element to the **ItemGroup** element:</span></span>

   1. <span data-ttu-id="ed7b1-165">**Include**属性に、除外するフォルダーのセミコロン区切りのリストを指定します。</span><span class="sxs-lookup"><span data-stu-id="ed7b1-165">In the **Include** attribute, provide a semicolon-separated list of the folders you want to exclude.</span></span>
   2. <span data-ttu-id="ed7b1-166">**Fromtarget**メタデータ要素で、フォルダーが除外される理由を示す意味のある値を指定します。これは *、ファイルの*名前のようになります。</span><span class="sxs-lookup"><span data-stu-id="ed7b1-166">In the **FromTarget** metadata element, provide a meaningful value to indicate why the folders are being excluded, like the name of the *.wpp.targets* file.</span></span>

      [!code-xml[Main](excluding-files-and-folders-from-deployment/samples/sample3.xml)]
7. <span data-ttu-id="ed7b1-167">Web パッケージからファイルを除外する場合は、 **ItemGroup**要素に**ExcludeFromPackageFiles**要素を追加します。</span><span class="sxs-lookup"><span data-stu-id="ed7b1-167">If you want to exclude files from the web package, add an **ExcludeFromPackageFiles** element to the **ItemGroup** element:</span></span>

   1. <span data-ttu-id="ed7b1-168">**Include**属性に、除外するファイルのセミコロン区切りのリストを指定します。</span><span class="sxs-lookup"><span data-stu-id="ed7b1-168">In the **Include** attribute, provide a semicolon-separated list of the files you want to exclude.</span></span>
   2. <span data-ttu-id="ed7b1-169">**Fromtarget**メタデータ要素で、ファイルが除外される理由を示す意味のある値を*指定します*。これは、ファイルの名前のようになります。</span><span class="sxs-lookup"><span data-stu-id="ed7b1-169">In the **FromTarget** metadata element, provide a meaningful value to indicate why the files are being excluded, like the name of the *.wpp.targets* file.</span></span>

      [!code-xml[Main](excluding-files-and-folders-from-deployment/samples/sample4.xml)]
8. <span data-ttu-id="ed7b1-170">*[プロジェクト名] の .targets*ファイルは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="ed7b1-170">The *[project name].wpp.targets* file should now resemble this:</span></span>

    [!code-xml[Main](excluding-files-and-folders-from-deployment/samples/sample5.xml)]
9. <span data-ttu-id="ed7b1-171">*[Project name]. wpp. .targets*ファイルを保存して閉じます。</span><span class="sxs-lookup"><span data-stu-id="ed7b1-171">Save and close the *[project name].wpp.targets* file.</span></span>

<span data-ttu-id="ed7b1-172">次に web アプリケーションプロジェクトをビルドしてパッケージ化すると、WPP によって自動的に*wpp*ファイルが検出されます。</span><span class="sxs-lookup"><span data-stu-id="ed7b1-172">The next time you build and package your web application project, the WPP will automatically detect the *.wpp.targets* file.</span></span> <span data-ttu-id="ed7b1-173">指定したファイルとフォルダーは、web パッケージに含まれません。</span><span class="sxs-lookup"><span data-stu-id="ed7b1-173">Any files and folders you specified will not be included in the web package.</span></span>

## <a name="conclusion"></a><span data-ttu-id="ed7b1-174">まとめ</span><span class="sxs-lookup"><span data-stu-id="ed7b1-174">Conclusion</span></span>

<span data-ttu-id="ed7b1-175">このトピックでは、web アプリケーションプロジェクトファイルと同じフォルダーにカスタムの*wpp*ファイルを作成することによって、web パッケージのビルド時に特定のファイルとフォルダーを除外する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="ed7b1-175">This topic described how to exclude specific files and folders when you build a web package, by creating a custom *.wpp.targets* file in the same folder as your web application project file.</span></span>

## <a name="further-reading"></a><span data-ttu-id="ed7b1-176">参考資料</span><span class="sxs-lookup"><span data-stu-id="ed7b1-176">Further Reading</span></span>

<span data-ttu-id="ed7b1-177">カスタム Microsoft Build Engine (MSBuild) プロジェクトファイルを使用した配置プロセスの制御の詳細については、「[プロジェクトファイルについ](../web-deployment-in-the-enterprise/understanding-the-project-file.md)て」および「[ビルドプロセスについ](../web-deployment-in-the-enterprise/understanding-the-build-process.md)て」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ed7b1-177">For more information on using custom Microsoft Build Engine (MSBuild) project files to control the deployment process, see [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md) and [Understanding the Build Process](../web-deployment-in-the-enterprise/understanding-the-build-process.md).</span></span> <span data-ttu-id="ed7b1-178">パッケージ化と配置のプロセスの詳細については、「 [Web アプリケーションプロジェクトのビルドとパッケージ化](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md)」、「Web[パッケージ配置のパラメーターの構成](../web-deployment-in-the-enterprise/configuring-parameters-for-web-package-deployment.md)」、および「 [web パッケージの配置](../web-deployment-in-the-enterprise/deploying-web-packages.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ed7b1-178">For more information on the packaging and deployment process, see [Building and Packaging Web Application Projects](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md), [Configuring Parameters for Web Package Deployment](../web-deployment-in-the-enterprise/configuring-parameters-for-web-package-deployment.md), and [Deploying Web Packages](../web-deployment-in-the-enterprise/deploying-web-packages.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="ed7b1-179">[前へ](deploying-membership-databases-to-enterprise-environments.md)
> [次へ](taking-web-applications-offline-with-web-deploy.md)</span><span class="sxs-lookup"><span data-stu-id="ed7b1-179">[Previous](deploying-membership-databases-to-enterprise-environments.md)
[Next](taking-web-applications-offline-with-web-deploy.md)</span></span>
