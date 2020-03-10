---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/performing-a-what-if-deployment
title: What If デプロイを実行する |Microsoft Docs
author: jrjlee
description: このトピックでは、インターネットインフォメーションサービス (IIS) Web 配置ツール (Web 配置) と v2.0 を使用して、"what-if" (またはシミュレートされた) 展開を実行する方法について説明します。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: c711b453-01ac-4e65-a48c-93d99bf22e58
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/performing-a-what-if-deployment
msc.type: authoredcontent
ms.openlocfilehash: 73a0e038cc0d4ebae0ffc8ed3fd2de4c9dad673c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78510334"
---
# <a name="performing-a-what-if-deployment"></a><span data-ttu-id="597c8-103">"What If" 配置を実行する</span><span class="sxs-lookup"><span data-stu-id="597c8-103">Performing a "What If" Deployment</span></span>

<span data-ttu-id="597c8-104">[Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="597c8-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

<span data-ttu-id="597c8-105">[[Download PDF]\(PDF をダウンロード\)](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)</span><span class="sxs-lookup"><span data-stu-id="597c8-105">[Download PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)</span></span>

> <span data-ttu-id="597c8-106">このトピックでは、インターネットインフォメーションサービス (IIS) Web 配置ツール (Web 配置) と VSDBCMD を使用して、"what-if" (またはシミュレートされた) 展開を実行する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="597c8-106">This topic describes how to perform "what if" (or simulated) deployments using the Internet Information Services (IIS) Web Deployment Tool (Web Deploy) and VSDBCMD.</span></span> <span data-ttu-id="597c8-107">これにより、アプリケーションを実際に配置する前に、特定のターゲット環境に対する配置ロジックの効果を判断できます。</span><span class="sxs-lookup"><span data-stu-id="597c8-107">This lets you determine the effects of your deployment logic on a particular target environment before you actually deploy your application.</span></span>

<span data-ttu-id="597c8-108">このトピックでは、Fabrikam, Inc. という架空の企業のエンタープライズ展開要件に基づいて、一連のチュートリアルの一部を説明します。このチュートリアルシリーズでは、&#x2014; [Contact Manager ソリューション](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;のサンプルソリューションを使用して、ASP.NET MVC 3 アプリケーション、Windows Communication Foundation (WCF) サービス、データベースプロジェクトなど、現実的なレベルの複雑さを持つ web アプリケーションを表します。</span><span class="sxs-lookup"><span data-stu-id="597c8-108">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

<span data-ttu-id="597c8-109">これらのチュートリアルの中核となる配置方法は、「プロジェクト[ファイルについ](../web-deployment-in-the-enterprise/understanding-the-project-file.md)て」で説明されている分割プロジェクトファイルアプローチに基づいています。この方法で&#x2014;は、ビルドおよび配置プロセスは、すべての変換先環境に適用されるビルド命令を含む2つのプロジェクトファイルと、環境固有のビルドと配置の設定を含んでいます。</span><span class="sxs-lookup"><span data-stu-id="597c8-109">The deployment method at the heart of these tutorials is based on the split project file approach described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md), in which the build and deployment process is controlled by two project files&#x2014;one containing build instructions that apply to every destination environment, and one containing environment-specific build and deployment settings.</span></span> <span data-ttu-id="597c8-110">ビルド時に、環境固有のプロジェクトファイルが環境に依存しないプロジェクトファイルにマージされ、ビルド命令の完全なセットが形成されます。</span><span class="sxs-lookup"><span data-stu-id="597c8-110">At build time, the environment-specific project file is merged into the environment-agnostic project file to form a complete set of build instructions.</span></span>

## <a name="performing-a-what-if-deployment-for-web-packages"></a><span data-ttu-id="597c8-111">Web パッケージの "What If" 配置の実行</span><span class="sxs-lookup"><span data-stu-id="597c8-111">Performing a "What If" Deployment for Web Packages</span></span>

<span data-ttu-id="597c8-112">Web 配置には、"what-if" (または試用版) モードで展開を実行できる機能が含まれています。</span><span class="sxs-lookup"><span data-stu-id="597c8-112">Web Deploy includes functionality that lets you perform deployments in "what if" (or trial) mode.</span></span> <span data-ttu-id="597c8-113">アイテムを "what-if" モードで展開すると、Web 配置は、展開を実行した場合と同じようにログファイルを生成しますが、実際には移行先サーバーで何も変更しません。</span><span class="sxs-lookup"><span data-stu-id="597c8-113">When you deploy artifacts in "what if" mode, Web Deploy generates a log file as if you had performed the deployment, but it doesn't actually change anything on the destination server.</span></span> <span data-ttu-id="597c8-114">ログファイルを確認すると、配置が移行先サーバーに与える影響を理解するのに役立ちます。具体的には次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="597c8-114">Reviewing the log file can help you to understand what impact your deployment will have on the destination server, in particular:</span></span>

- <span data-ttu-id="597c8-115">追加される内容。</span><span class="sxs-lookup"><span data-stu-id="597c8-115">What will get added.</span></span>
- <span data-ttu-id="597c8-116">更新される内容。</span><span class="sxs-lookup"><span data-stu-id="597c8-116">What will get updated.</span></span>
- <span data-ttu-id="597c8-117">削除される内容。</span><span class="sxs-lookup"><span data-stu-id="597c8-117">What will get deleted.</span></span>

<span data-ttu-id="597c8-118">"What-if" の展開では、移行先サーバーで実際には何も変更されないため、展開が成功するかどうかを予測することはできません。</span><span class="sxs-lookup"><span data-stu-id="597c8-118">Because a "what if" deployment doesn't actually change anything on the destination server, what it can't always do is predict whether a deployment will succeed.</span></span>

<span data-ttu-id="597c8-119">「 [Web パッケージの配置](../web-deployment-in-the-enterprise/deploying-web-packages.md)」で説明したように、msdeploy.exe コマンドラインユーティリティ&#x2014;を直接使用するか、ビルドプロセスによって生成される *.deploy*ファイルを実行することで、Web 配置を使用して web パッケージを配置できます。</span><span class="sxs-lookup"><span data-stu-id="597c8-119">As described in [Deploying Web Packages](../web-deployment-in-the-enterprise/deploying-web-packages.md), you can deploy web packages using Web Deploy in two ways&#x2014;by using the MSDeploy.exe command-line utility directly or by running the *.deploy.cmd* file that the build process generates.</span></span>

<span data-ttu-id="597c8-120">Msdeploy.exe を直接使用している場合は、コマンドに **– whatif**フラグを追加することで、"what-if" 配置を実行できます。</span><span class="sxs-lookup"><span data-stu-id="597c8-120">If you're using MSDeploy.exe directly, you can run a "what if" deployment by adding the **–whatif** flag to your command.</span></span> <span data-ttu-id="597c8-121">たとえば、ContactManager. Mvc パッケージをステージング環境に配置した場合に何が起こるかを評価するために、Msdeploy.exe コマンドは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="597c8-121">For example, to evaluate what would happen if you deployed the ContactManager.Mvc.zip package to a staging environment, the MSDeploy command should resemble this:</span></span>

[!code-console[Main](performing-a-what-if-deployment/samples/sample1.cmd)]

<span data-ttu-id="597c8-122">"What-if" デプロイの結果に問題がなければ、 **– whatif**フラグを削除してライブデプロイを実行できます。</span><span class="sxs-lookup"><span data-stu-id="597c8-122">When you're satisfied with the results of your "what if" deployment, you can remove the **–whatif** flag to run a live deployment.</span></span>

> [!NOTE]
> <span data-ttu-id="597c8-123">Msdeploy.exe のコマンドラインオプションの詳細については、「 [Web 配置操作の設定](https://technet.microsoft.com/library/dd569089(WS.10).aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="597c8-123">For more information on command-line options for MSDeploy.exe, see [Web Deploy Operation Settings](https://technet.microsoft.com/library/dd569089(WS.10).aspx).</span></span>

<span data-ttu-id="597c8-124">*.Deploy*ファイルを使用している場合は、コマンドに **/y**フラグ ("yes" または update mode) ではなく **/t**フラグ (試用モード) フラグを含めることで、"what-if" 展開を実行できます。</span><span class="sxs-lookup"><span data-stu-id="597c8-124">If you're using the *.deploy.cmd* file, you can run a "what if" deployment by including the **/t** flag (trial mode) flag instead of the **/y** flag ("yes," or update mode) in your command.</span></span> <span data-ttu-id="597c8-125">たとえば、 *.deploy*ファイルを実行して Contactmanager の Mvc パッケージを配置した場合の動作を評価するには、コマンドは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="597c8-125">For example, to evaluate what would happen if you deployed the ContactManager.Mvc.zip package by running the *.deploy.cmd* file, your command should resemble this:</span></span>

[!code-console[Main](performing-a-what-if-deployment/samples/sample2.cmd)]

<span data-ttu-id="597c8-126">"試用モード" 展開の結果に問題がなければ、 **/t**フラグを **/y**フラグに置き換えてライブデプロイを実行できます。</span><span class="sxs-lookup"><span data-stu-id="597c8-126">When you're satisfied with the results of your "trial mode" deployment, you can replace the **/t** flag with a **/y** flag to run a live deployment:</span></span>

[!code-console[Main](performing-a-what-if-deployment/samples/sample3.cmd)]

> [!NOTE]
> <span data-ttu-id="597c8-127">*. .Deploy*ファイルのコマンドラインオプションの詳細については、「[方法: .Deploy ファイルを使用して展開パッケージをインストール](https://msdn.microsoft.com/library/ff356104.aspx)する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="597c8-127">For more information on command-line options for *.deploy.cmd* files, see [How to: Install a Deployment Package Using the deploy.cmd File](https://msdn.microsoft.com/library/ff356104.aspx).</span></span> <span data-ttu-id="597c8-128">フラグを指定せずに *.deploy*ファイルを実行すると、使用可能なフラグの一覧がコマンドプロンプトに表示されます。</span><span class="sxs-lookup"><span data-stu-id="597c8-128">If you run the *.deploy.cmd* file without specifying any flags, the command prompt will display a list of available flags.</span></span>

## <a name="performing-a-what-if-deployment-for-databases"></a><span data-ttu-id="597c8-129">データベースの "What If" 配置の実行</span><span class="sxs-lookup"><span data-stu-id="597c8-129">Performing a "What If" Deployment for Databases</span></span>

<span data-ttu-id="597c8-130">このセクションでは、VSDBCMD ユーティリティを使用して、スキーマベースの増分データベース配置を実行していることを前提としています。</span><span class="sxs-lookup"><span data-stu-id="597c8-130">This section assumes that you're using the VSDBCMD utility to perform incremental, schema-based database deployment.</span></span> <span data-ttu-id="597c8-131">この方法の詳細については、「[データベースプロジェクトの配置](../web-deployment-in-the-enterprise/deploying-database-projects.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="597c8-131">This approach is described in more detail in [Deploying Database Projects](../web-deployment-in-the-enterprise/deploying-database-projects.md).</span></span> <span data-ttu-id="597c8-132">ここで説明する概念を適用する前に、このトピックについて理解しておくことをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="597c8-132">We recommend that you familiarize yourself with this topic before you apply the concepts described here.</span></span>

<span data-ttu-id="597c8-133">**配置**モードで VSDBCMD を使用する場合は、 **/dd** (または **/deploytodatabase**) フラグを使用して、VSDBCMD が実際にデータベースを配置するか、配置スクリプトを生成するかを制御できます。</span><span class="sxs-lookup"><span data-stu-id="597c8-133">When you use VSDBCMD in **Deploy** mode, you can use the **/dd** (or **/DeployToDatabase**) flag to control whether VSDBCMD actually deploys the database or just generates a deployment script.</span></span> <span data-ttu-id="597c8-134">.Dbschema ファイルを配置している場合は、次のような動作になります。</span><span class="sxs-lookup"><span data-stu-id="597c8-134">If you're deploying a .dbschema file, this is the behavior:</span></span>

- <span data-ttu-id="597c8-135">**/Dd +** または **/dd**を指定すると、VSDBCMD によって配置スクリプトが生成され、データベースが配置されます。</span><span class="sxs-lookup"><span data-stu-id="597c8-135">If you specify **/dd+** or **/dd**, VSDBCMD will generate a deployment script and deploy the database.</span></span>
- <span data-ttu-id="597c8-136">**/Ddを**指定した場合、またはスイッチを省略した場合、VSDBCMD では配置スクリプトのみが生成されます。</span><span class="sxs-lookup"><span data-stu-id="597c8-136">If you specify **/dd-** or omit the switch, VSDBCMD will generate a deployment script only.</span></span>

> [!NOTE]
> <span data-ttu-id="597c8-137">.Dbschema ファイルではなく、deploymanifest ファイルを配置している場合、 **/dd**スイッチの動作ははるかに複雑になります。</span><span class="sxs-lookup"><span data-stu-id="597c8-137">If you're deploying a .deploymanifest file rather than a .dbschema file, the behavior of the **/dd** switch is a lot more complicated.</span></span> <span data-ttu-id="597c8-138">基本的に、VSDBCMD では、deploymanifest ファイルに値**True**の**deploytodatabase**要素が含まれている場合、 **/dd**スイッチの値は無視されます。</span><span class="sxs-lookup"><span data-stu-id="597c8-138">Essentially, VSDBCMD will ignore the value of the **/dd** switch if the .deploymanifest file includes a **DeployToDatabase** element with a value of **True**.</span></span> <span data-ttu-id="597c8-139">[データベースプロジェクトを配置](../web-deployment-in-the-enterprise/deploying-database-projects.md)すると、この動作が完全に記述されます。</span><span class="sxs-lookup"><span data-stu-id="597c8-139">[Deploying Database Projects](../web-deployment-in-the-enterprise/deploying-database-projects.md) describes this behavior in full.</span></span>

<span data-ttu-id="597c8-140">たとえば、実際にデータベースを配置せずに**Contactmanager**データベースの配置スクリプトを生成する場合、VSDBCMD コマンドは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="597c8-140">For example, to generate a deployment script for the **ContactManager** database without actually deploying the database, your VSDBCMD command should resemble this:</span></span>

[!code-console[Main](performing-a-what-if-deployment/samples/sample4.cmd)]

<span data-ttu-id="597c8-141">VSDBCMD はデータベースの差分配置ツールであるため、配置スクリプトは、現在のデータベース (存在する場合) を指定したスキーマに更新するために必要なすべての SQL コマンドを含むように動的に生成されます。</span><span class="sxs-lookup"><span data-stu-id="597c8-141">VSDBCMD is a differential database deployment tool, and as such the deployment script is dynamically generated to contain all the SQL commands necessary to update the current database, if one exists, to the specified schema.</span></span> <span data-ttu-id="597c8-142">配置スクリプトを確認することは、配置が現在のデータベースとそれに含まれるデータに与える影響を決定するのに便利な方法です。</span><span class="sxs-lookup"><span data-stu-id="597c8-142">Reviewing the deployment script is a useful way to determine what impact your deployment will have on the current database and the data it contains.</span></span> <span data-ttu-id="597c8-143">たとえば、次のような判断が必要になる場合があります。</span><span class="sxs-lookup"><span data-stu-id="597c8-143">For example, you might want to determine:</span></span>

- <span data-ttu-id="597c8-144">既存のテーブルが削除されるかどうか、およびそれによってデータが失われるかどうかを示します。</span><span class="sxs-lookup"><span data-stu-id="597c8-144">Whether any existing tables will be removed, and whether that will result in data loss.</span></span>
- <span data-ttu-id="597c8-145">テーブルを分割またはマージする場合など、操作の順序によってデータ損失のリスクが生じるかどうか。</span><span class="sxs-lookup"><span data-stu-id="597c8-145">Whether the order of operations carries a risk of data loss, for example, if you're splitting or merging tables.</span></span>

<span data-ttu-id="597c8-146">デプロイスクリプトに問題がなければ、VSDBCMD **+** フラグを使用して、変更を加えることができます。</span><span class="sxs-lookup"><span data-stu-id="597c8-146">If you're happy with the deployment script, you can repeat the VSDBCMD with a **/dd+** flag to make the changes.</span></span> <span data-ttu-id="597c8-147">または、必要に応じて配置スクリプトを編集し、データベースサーバーで手動で実行することもできます。</span><span class="sxs-lookup"><span data-stu-id="597c8-147">Alternatively, you can edit the deployment script to meet your requirements and then execute it manually on the database server.</span></span>

## <a name="integrating-what-if-functionality-into-custom-project-files"></a><span data-ttu-id="597c8-148">"What If" 機能のカスタムプロジェクトファイルへの統合</span><span class="sxs-lookup"><span data-stu-id="597c8-148">Integrating "What If" Functionality into Custom Project Files</span></span>

<span data-ttu-id="597c8-149">より複雑な配置シナリオでは、「[プロジェクトファイルについ](../web-deployment-in-the-enterprise/understanding-the-project-file.md)て」で説明されているように、カスタム Microsoft Build Engine (MSBuild) プロジェクトファイルを使用してビルドおよび配置ロジックをカプセル化することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="597c8-149">In more complex deployment scenarios, you'll want to use a custom Microsoft Build Engine (MSBuild) project file to encapsulate your build and deployment logic, as described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md).</span></span> <span data-ttu-id="597c8-150">たとえば、 [Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)サンプルソリューションでは、次のように*発行します。*</span><span class="sxs-lookup"><span data-stu-id="597c8-150">For example, in the [Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) sample solution, the *Publish.proj* file:</span></span>

- <span data-ttu-id="597c8-151">ソリューションをビルドします。</span><span class="sxs-lookup"><span data-stu-id="597c8-151">Builds the solution.</span></span>
- <span data-ttu-id="597c8-152">Web 配置を使用して、ContactManager の Mvc アプリケーションをパッケージ化して配置します。</span><span class="sxs-lookup"><span data-stu-id="597c8-152">Uses Web Deploy to package and deploy the ContactManager.Mvc application.</span></span>
- <span data-ttu-id="597c8-153">Web 配置を使用して、ContactManager. サービスアプリケーションをパッケージ化して配置します。</span><span class="sxs-lookup"><span data-stu-id="597c8-153">Uses Web Deploy to package and deploy the ContactManager.Service application.</span></span>
- <span data-ttu-id="597c8-154">**Contactmanager**データベースをデプロイします。</span><span class="sxs-lookup"><span data-stu-id="597c8-154">Deploys the **ContactManager** database.</span></span>

<span data-ttu-id="597c8-155">この方法で、複数の web パッケージまたはデータベースの配置を1つの手順のプロセスに統合する場合は、"what-if" モードで配置全体を実行するオプションを使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="597c8-155">When you integrate the deployment of multiple web packages and/or databases into a single-step process in this way, you may also want the option of performing the entire deployment in a "what if" mode.</span></span>

<span data-ttu-id="597c8-156">この方法を説明するには、 *Publish*ファイルを使用します。</span><span class="sxs-lookup"><span data-stu-id="597c8-156">The *Publish.proj* file demonstrates how you can do this.</span></span> <span data-ttu-id="597c8-157">まず、"what-if" 値を格納するプロパティを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="597c8-157">First, you need to create a property to store the "what if" value:</span></span>

[!code-xml[Main](performing-a-what-if-deployment/samples/sample5.xml)]

<span data-ttu-id="597c8-158">この例では、 **WhatIf**という名前のプロパティを作成しました。既定値は**false**です。</span><span class="sxs-lookup"><span data-stu-id="597c8-158">In this case, you've created a property named **WhatIf** with a default value of **false**.</span></span> <span data-ttu-id="597c8-159">この値をオーバーライドするには、後で説明するように、コマンドラインパラメーターでプロパティを**true**に設定します。</span><span class="sxs-lookup"><span data-stu-id="597c8-159">Users can override this value by setting the property to **true** in a command-line parameter, as you'll see shortly.</span></span>

<span data-ttu-id="597c8-160">次の段階では、VSDBCMD コマンドを Web 配置パラメーター化し、フラグに**WhatIf**プロパティ値が反映されるようにします。</span><span class="sxs-lookup"><span data-stu-id="597c8-160">The next stage is to parameterize any Web Deploy and VSDBCMD commands so that the flags reflect the **WhatIf** property value.</span></span> <span data-ttu-id="597c8-161">たとえば、次のターゲット ( *Publish. proj*ファイルと簡略化された) は、 *.deploy*ファイルを実行して web パッケージを配置します。</span><span class="sxs-lookup"><span data-stu-id="597c8-161">For example, the next target (taken from the *Publish.proj* file and simplified) runs the *.deploy.cmd* file to deploy a web package.</span></span> <span data-ttu-id="597c8-162">既定では、コマンドには、 **/y**スイッチ ("yes" または update mode) が含まれています。</span><span class="sxs-lookup"><span data-stu-id="597c8-162">By default, the command includes a **/Y** switch ("yes," or update mode).</span></span> <span data-ttu-id="597c8-163">**WhatIf**が**true**に設定されている場合、これは **/t**スイッチ (試用版または "what-if" モード) に置き換えられます。</span><span class="sxs-lookup"><span data-stu-id="597c8-163">If **WhatIf** is set to **true**, this is replaced by a **/T** switch (trial, or "what if" mode).</span></span>

[!code-xml[Main](performing-a-what-if-deployment/samples/sample6.xml)]

<span data-ttu-id="597c8-164">同様に、次のターゲットは、VSDBCMD ユーティリティを使用してデータベースを配置します。</span><span class="sxs-lookup"><span data-stu-id="597c8-164">Similarly, the next target uses the VSDBCMD utility to deploy a database.</span></span> <span data-ttu-id="597c8-165">既定では、 **/dd**スイッチは含まれていません。</span><span class="sxs-lookup"><span data-stu-id="597c8-165">By default, a **/dd** switch is not included.</span></span> <span data-ttu-id="597c8-166">つまり、VSDBCMD は配置スクリプトを生成しますが、"what-if"&#x2014;シナリオではなく、データベースを展開しません。</span><span class="sxs-lookup"><span data-stu-id="597c8-166">This means that VSDBCMD will generate a deployment script but will not deploy the database&#x2014;in other words, a "what if" scenario.</span></span> <span data-ttu-id="597c8-167">**WhatIf**プロパティが**true**に設定されていない場合は、 **/dd**スイッチが追加され、VSDBCMD によってデータベースが配置されます。</span><span class="sxs-lookup"><span data-stu-id="597c8-167">If the **WhatIf** property is not set to **true**, a **/dd** switch is added and VSDBCMD will deploy the database.</span></span>

[!code-xml[Main](performing-a-what-if-deployment/samples/sample7.xml)]

<span data-ttu-id="597c8-168">同じ方法を使用して、プロジェクトファイル内の関連するすべてのコマンドをパラメーター化することができます。</span><span class="sxs-lookup"><span data-stu-id="597c8-168">You can use the same approach to parameterize all the relevant commands in your project file.</span></span> <span data-ttu-id="597c8-169">"What-if" 配置を実行する場合は、コマンドラインから**WhatIf**プロパティ値を指定するだけです。</span><span class="sxs-lookup"><span data-stu-id="597c8-169">When you want to run a "what if" deployment, you can then simply provide a **WhatIf** property value from the command line:</span></span>

[!code-console[Main](performing-a-what-if-deployment/samples/sample8.cmd)]

<span data-ttu-id="597c8-170">このようにして、すべてのプロジェクトコンポーネントの "what-if" 配置を1回の手順で実行できます。</span><span class="sxs-lookup"><span data-stu-id="597c8-170">In this way, you can run a "what if" deployment for all your project components in a single step.</span></span>

## <a name="conclusion"></a><span data-ttu-id="597c8-171">まとめ</span><span class="sxs-lookup"><span data-stu-id="597c8-171">Conclusion</span></span>

<span data-ttu-id="597c8-172">このトピックでは、Web 配置、VSDBCMD、および MSBuild を使用して "what-if" 配置を実行する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="597c8-172">This topic described how to run "what if" deployments using Web Deploy, VSDBCMD, and MSBuild.</span></span> <span data-ttu-id="597c8-173">"What-if" 展開を使用すると、移行先の環境に実際に変更を加える前に、提案された展開の影響を評価できます。</span><span class="sxs-lookup"><span data-stu-id="597c8-173">A "what if" deployment lets you evaluate the impact of a proposed deployment before you actually make any changes to the destination environment.</span></span>

## <a name="further-reading"></a><span data-ttu-id="597c8-174">参考資料</span><span class="sxs-lookup"><span data-stu-id="597c8-174">Further Reading</span></span>

<span data-ttu-id="597c8-175">Web 配置のコマンドライン構文の詳細については、「 [Web 配置操作の設定](https://technet.microsoft.com/library/dd569089(WS.10).aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="597c8-175">For more information on Web Deploy command-line syntax, see [Web Deploy Operation Settings](https://technet.microsoft.com/library/dd569089(WS.10).aspx).</span></span> <span data-ttu-id="597c8-176">*.Deploy*ファイルを使用する場合のコマンドラインオプションのガイダンスについては、「[方法: .Deploy ファイルを使用して展開パッケージをインストール](https://msdn.microsoft.com/library/ff356104.aspx)する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="597c8-176">For guidance on command-line options when you use the *.deploy.cmd* file, see [How to: Install a Deployment Package Using the deploy.cmd File](https://msdn.microsoft.com/library/ff356104.aspx).</span></span> <span data-ttu-id="597c8-177">VSDBCMD コマンドライン構文のガイダンスについては、「 [VSDBCMD のコマンドラインリファレンス」を参照してください。EXE (デプロイとスキーマのインポート)](https://msdn.microsoft.com/library/dd193283.aspx)。</span><span class="sxs-lookup"><span data-stu-id="597c8-177">For guidance on VSDBCMD command-line syntax, see [Command-Line Reference for VSDBCMD.EXE (Deployment and Schema Import)](https://msdn.microsoft.com/library/dd193283.aspx).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="597c8-178">[前へ](advanced-enterprise-web-deployment.md)
> [次へ](customizing-database-deployments-for-multiple-environments.md)</span><span class="sxs-lookup"><span data-stu-id="597c8-178">[Previous](advanced-enterprise-web-deployment.md)
[Next](customizing-database-deployments-for-multiple-environments.md)</span></span>
