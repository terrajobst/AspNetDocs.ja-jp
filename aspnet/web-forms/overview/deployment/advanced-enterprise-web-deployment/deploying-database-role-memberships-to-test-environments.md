---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments
title: テスト環境へのデータベースロールメンバーシップの配置 |Microsoft Docs
author: jrjlee
description: このトピックでは、テスト環境へのソリューションの配置の一部として、ユーザーアカウントをデータベースロールに追加する方法について説明します。 ... を含むソリューションを配置する場合
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 9b2af539-7ad9-47aa-b66e-873bd9906e79
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments
msc.type: authoredcontent
ms.openlocfilehash: a15f5bf5f659d151e91ef9e53c5ad55bcd8e2b01
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78474946"
---
# <a name="deploying-database-role-memberships-to-test-environments"></a><span data-ttu-id="a94eb-104">テスト環境にデータベース ロール メンバーシップを配置する</span><span class="sxs-lookup"><span data-stu-id="a94eb-104">Deploying Database Role Memberships to Test Environments</span></span>

<span data-ttu-id="a94eb-105">[Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="a94eb-105">by [Jason Lee](https://github.com/jrjlee)</span></span>

<span data-ttu-id="a94eb-106">[[Download PDF]\(PDF をダウンロード\)](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)</span><span class="sxs-lookup"><span data-stu-id="a94eb-106">[Download PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)</span></span>

> <span data-ttu-id="a94eb-107">このトピックでは、テスト環境へのソリューションの配置の一部として、ユーザーアカウントをデータベースロールに追加する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="a94eb-107">This topic describes how to add user accounts to database roles as part of a solution deployment to a test environment.</span></span>
> 
> <span data-ttu-id="a94eb-108">データベースプロジェクトを含むソリューションをステージング環境または運用環境に配置する場合は、通常、開発者がデータベースロールへのユーザーアカウントの追加を自動化する必要がありません。</span><span class="sxs-lookup"><span data-stu-id="a94eb-108">When you deploy a solution containing a database project to a staging or production environment, you typically don't want the developer to automate the addition of user accounts to database roles.</span></span> <span data-ttu-id="a94eb-109">ほとんどの場合、開発者はどのユーザーアカウントをどのデータベースロールに追加する必要があるかを把握しておらず、これらの要件はいつでも変更される可能性があります。</span><span class="sxs-lookup"><span data-stu-id="a94eb-109">In most cases, the developer won't know which user accounts need to be added to which database roles, and these requirements could change at any time.</span></span> <span data-ttu-id="a94eb-110">ただし、データベースプロジェクトを含むソリューションを開発環境またはテスト環境に配置する場合は、通常、状況は異なります。</span><span class="sxs-lookup"><span data-stu-id="a94eb-110">However, when you deploy a solution containing a database project to a development or test environment, the situation is usually rather different:</span></span>
> 
> - <span data-ttu-id="a94eb-111">通常、開発者は定期的にソリューションを再デプロイします (多くの場合、1日に数回)。</span><span class="sxs-lookup"><span data-stu-id="a94eb-111">The developer typically re-deploys the solution on a regular basis, often several times a day.</span></span>
> - <span data-ttu-id="a94eb-112">通常、データベースは、すべての配置で再作成されます。つまり、データベースユーザーを作成し、すべての配置後にロールに追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a94eb-112">The database is typically re-created on every deployment, which means that database users must be created and added to roles after every deployment.</span></span>
> - <span data-ttu-id="a94eb-113">開発者は、通常、対象となる開発環境またはテスト環境を完全に制御できます。</span><span class="sxs-lookup"><span data-stu-id="a94eb-113">The developer typically has full control over the target development or test environment.</span></span>
> 
> <span data-ttu-id="a94eb-114">このシナリオでは、データベースユーザーを自動的に作成し、データベースロールのメンバーシップをデプロイプロセスの一部として割り当てる方が便利です。</span><span class="sxs-lookup"><span data-stu-id="a94eb-114">In this scenario, it's often beneficial to automatically create database users and assign database role memberships as part of the deployment process.</span></span>
> 
> <span data-ttu-id="a94eb-115">重要なのは、この操作はターゲット環境に基づいて条件を設定する必要があることです。</span><span class="sxs-lookup"><span data-stu-id="a94eb-115">The key factor is that this operation needs to be conditional based on the target environment.</span></span> <span data-ttu-id="a94eb-116">ステージング環境または運用環境にデプロイしている場合は、操作をスキップします。</span><span class="sxs-lookup"><span data-stu-id="a94eb-116">If you're deploying to a staging or a production environment, you want to skip the operation.</span></span> <span data-ttu-id="a94eb-117">開発者またはテスト環境に配置する場合は、追加の操作を行わずにロールメンバーシップを配置する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a94eb-117">If you're deploying to a developer or test environment, you want to deploy role memberships without further intervention.</span></span> <span data-ttu-id="a94eb-118">このトピックでは、この課題に対処するために使用できる1つの方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="a94eb-118">This topic describes one approach you can use to address this challenge.</span></span>

<span data-ttu-id="a94eb-119">このトピックでは、Fabrikam, Inc. という架空の企業のエンタープライズ展開要件に基づいて、一連のチュートリアルの一部を説明します。このチュートリアルシリーズでは、&#x2014; [Contact Manager ソリューション](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;のサンプルソリューションを使用して、ASP.NET MVC 3 アプリケーション、Windows Communication Foundation (WCF) サービス、データベースプロジェクトなど、現実的なレベルの複雑さを持つ web アプリケーションを表します。</span><span class="sxs-lookup"><span data-stu-id="a94eb-119">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

<span data-ttu-id="a94eb-120">これらのチュートリアルの中核となる配置方法は、「[プロジェクトファイルについ](../web-deployment-in-the-enterprise/understanding-the-project-file.md)て」で説明されている分割プロジェクトファイルアプローチに基づいています。この&#x2014;プロジェクトファイルには、ビルドプロセスは、すべての変換先環境に適用されるビルド命令を含む2つのプロジェクトファイルと、環境固有のビルドおよび配置設定を含んでいます。</span><span class="sxs-lookup"><span data-stu-id="a94eb-120">The deployment method at the heart of these tutorials is based on the split project file approach described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md), in which the build process is controlled by two project files&#x2014;one containing build instructions that apply to every destination environment, and one containing environment-specific build and deployment settings.</span></span> <span data-ttu-id="a94eb-121">ビルド時に、環境固有のプロジェクトファイルが環境に依存しないプロジェクトファイルにマージされ、ビルド命令の完全なセットが形成されます。</span><span class="sxs-lookup"><span data-stu-id="a94eb-121">At build time, the environment-specific project file is merged into the environment-agnostic project file to form a complete set of build instructions.</span></span>

## <a name="task-overview"></a><span data-ttu-id="a94eb-122">タスクの概要</span><span class="sxs-lookup"><span data-stu-id="a94eb-122">Task Overview</span></span>

<span data-ttu-id="a94eb-123">このトピックは次のことを前提としています。</span><span class="sxs-lookup"><span data-stu-id="a94eb-123">This topic assumes that:</span></span>

- <span data-ttu-id="a94eb-124">「プロジェクト[ファイルについ](../web-deployment-in-the-enterprise/understanding-the-project-file.md)て」で説明されているように、ソリューションの配置には、プロジェクトファイルの分割アプローチを使用します。</span><span class="sxs-lookup"><span data-stu-id="a94eb-124">You use the split project file approach to solution deployment, as described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md).</span></span>
- <span data-ttu-id="a94eb-125">「[ビルドプロセスについ](../web-deployment-in-the-enterprise/understanding-the-build-process.md)て」で説明されているように、プロジェクトファイルから VSDBCMD を呼び出して、データベースプロジェクトを配置します。</span><span class="sxs-lookup"><span data-stu-id="a94eb-125">You call VSDBCMD from the project file to deploy your database project, as described in [Understanding the Build Process](../web-deployment-in-the-enterprise/understanding-the-build-process.md).</span></span>

<span data-ttu-id="a94eb-126">データベースプロジェクトをテスト環境に配置するときにデータベースユーザーを作成し、ロールメンバーシップを割り当てるには、次のことを行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="a94eb-126">To create database users and assign role memberships when you deploy a database project to a test environment, you'll need to:</span></span>

- <span data-ttu-id="a94eb-127">必要なデータベースの変更を行う Transact 構造化照会言語 (Transact-sql) スクリプトを作成します。</span><span class="sxs-lookup"><span data-stu-id="a94eb-127">Create a Transact Structured Query Language (Transact-SQL) script that makes the necessary database changes.</span></span>
- <span data-ttu-id="a94eb-128">Sqlcmd ユーティリティを使用して SQL スクリプトを実行する Microsoft Build Engine (MSBuild) ターゲットを作成します。</span><span class="sxs-lookup"><span data-stu-id="a94eb-128">Create a Microsoft Build Engine (MSBuild) target that uses the sqlcmd.exe utility to run the SQL script.</span></span>
- <span data-ttu-id="a94eb-129">ソリューションをテスト環境に配置するときに、ターゲットを呼び出すようにプロジェクトファイルを構成します。</span><span class="sxs-lookup"><span data-stu-id="a94eb-129">Configure your project files to invoke the target when you're deploying your solution to a test environment.</span></span>

<span data-ttu-id="a94eb-130">このトピックでは、これらの各手順を実行する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="a94eb-130">This topic will show you how to perform each of these procedures.</span></span>

## <a name="scripting-the-database-role-memberships"></a><span data-ttu-id="a94eb-131">データベースロールのメンバーシップのスクリプトを作成する</span><span class="sxs-lookup"><span data-stu-id="a94eb-131">Scripting the Database Role Memberships</span></span>

<span data-ttu-id="a94eb-132">Transact-sql スクリプトは、さまざまな方法で、または任意の場所で作成できます。</span><span class="sxs-lookup"><span data-stu-id="a94eb-132">You can create a Transact-SQL script in a lot of different ways, and in any location you choose.</span></span> <span data-ttu-id="a94eb-133">最も簡単な方法は、Visual Studio 2010 でソリューション内にスクリプトを作成することです。</span><span class="sxs-lookup"><span data-stu-id="a94eb-133">The easiest approach is to create the script within your solution in Visual Studio 2010.</span></span>

<span data-ttu-id="a94eb-134">**SQL スクリプトを作成するには**</span><span class="sxs-lookup"><span data-stu-id="a94eb-134">**To create a SQL script**</span></span>

1. <span data-ttu-id="a94eb-135">**[ソリューションエクスプローラー]** ウィンドウで、データベースプロジェクトノードを展開します。</span><span class="sxs-lookup"><span data-stu-id="a94eb-135">In the **Solution Explorer** window, expand your database project node.</span></span>
2. <span data-ttu-id="a94eb-136">**Scripts**フォルダーを右クリックして **[追加]** をポイントし、 **[新しいフォルダー]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="a94eb-136">Right-click the **Scripts** folder, point to **Add**, and then click **New Folder**.</span></span>
3. <span data-ttu-id="a94eb-137">フォルダー名として「 **Test** 」と入力し、enter キーを押します。</span><span class="sxs-lookup"><span data-stu-id="a94eb-137">Type **Test** as the folder name, and then press Enter.</span></span>
4. <span data-ttu-id="a94eb-138">**テスト**フォルダーを右クリックし、 **[追加]** をポイントして、 **[スクリプト]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="a94eb-138">Right-click the **Test** folder, point to **Add**, and then click **Script**.</span></span>
5. <span data-ttu-id="a94eb-139">**[新しい項目の追加]** ダイアログボックスで、スクリプトにわかりやすい名前 (たとえば、 **AddRoleMemberships**) を付け、 **[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="a94eb-139">In the **Add New Item** dialog box, give your script a meaningful name (for example, **AddRoleMemberships.sql**), and then click **Add**.</span></span>

    ![](deploying-database-role-memberships-to-test-environments/_static/image1.png)
6. <span data-ttu-id="a94eb-140">*AddRoleMemberships*ファイルで、次のような transact-sql ステートメントを追加します。</span><span class="sxs-lookup"><span data-stu-id="a94eb-140">In the *AddRoleMemberships.sql* file, add Transact-SQL statements that:</span></span>

    1. <span data-ttu-id="a94eb-141">データベースにアクセスする SQL Server ログインのデータベースユーザーを作成します。</span><span class="sxs-lookup"><span data-stu-id="a94eb-141">Create a database user for the SQL Server login that will access your database.</span></span>
    2. <span data-ttu-id="a94eb-142">必要なデータベースロールにデータベースユーザーを追加します。</span><span class="sxs-lookup"><span data-stu-id="a94eb-142">Add the database user to any required database roles.</span></span>
7. <span data-ttu-id="a94eb-143">ファイルは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="a94eb-143">The file should resemble this:</span></span>

    [!code-sql[Main](deploying-database-role-memberships-to-test-environments/samples/sample1.sql)]
8. <span data-ttu-id="a94eb-144">ファイルを保存します。</span><span class="sxs-lookup"><span data-stu-id="a94eb-144">Save the file.</span></span>

## <a name="executing-the-script-on-the-target-database"></a><span data-ttu-id="a94eb-145">ターゲットデータベースでのスクリプトの実行</span><span class="sxs-lookup"><span data-stu-id="a94eb-145">Executing the Script on the Target Database</span></span>

<span data-ttu-id="a94eb-146">データベースプロジェクトを配置するときに、配置後スクリプトの一部として必要な Transact-sql スクリプトを実行するのが理想的です。</span><span class="sxs-lookup"><span data-stu-id="a94eb-146">Ideally, you'd run any required Transact-SQL scripts as part of a post-deployment script when you deploy your database project.</span></span> <span data-ttu-id="a94eb-147">ただし、配置後スクリプトでは、ソリューション構成またはビルドプロパティに基づいて条件付きでロジックを実行することはできません。</span><span class="sxs-lookup"><span data-stu-id="a94eb-147">However, post-deployment scripts don't allow you to execute logic conditionally based on solution configurations or build properties.</span></span> <span data-ttu-id="a94eb-148">別の方法として、sqlcmd コマンドを実行する**Target**要素を作成することによって、MSBuild プロジェクトファイルから直接 SQL スクリプトを実行します。</span><span class="sxs-lookup"><span data-stu-id="a94eb-148">The alternative is to run your SQL scripts directly from the MSBuild project file, by creating a **Target** element that executes a sqlcmd.exe command.</span></span> <span data-ttu-id="a94eb-149">このコマンドを使用して、ターゲットデータベースでスクリプトを実行できます。</span><span class="sxs-lookup"><span data-stu-id="a94eb-149">You can use this command to run your script on the target database:</span></span>

[!code-console[Main](deploying-database-role-memberships-to-test-environments/samples/sample2.cmd)]

> [!NOTE]
> <span data-ttu-id="a94eb-150">Sqlcmd のコマンドラインオプションの詳細については、「 [Sqlcmd ユーティリティ](https://msdn.microsoft.com/library/ms162773.aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a94eb-150">For more information on sqlcmd command-line options, see [sqlcmd Utility](https://msdn.microsoft.com/library/ms162773.aspx).</span></span>

<span data-ttu-id="a94eb-151">MSBuild ターゲットにこのコマンドを埋め込む前に、スクリプトを実行する条件を考慮する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a94eb-151">Before you embed this command in an MSBuild target, you need to consider under what conditions you want the script to run:</span></span>

- <span data-ttu-id="a94eb-152">ターゲットデータベースは、ロールメンバーシップを変更する前に存在している必要があります。</span><span class="sxs-lookup"><span data-stu-id="a94eb-152">The target database must exist before you change its role memberships.</span></span> <span data-ttu-id="a94eb-153">そのため、このスクリプトは、データベースの配置*後*に実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a94eb-153">As such, you need to run this script *after* the database deployment.</span></span>
- <span data-ttu-id="a94eb-154">テスト環境に対してのみスクリプトが実行されるように、条件を含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="a94eb-154">You need to include a condition so that the script is only executed for test environments.</span></span>
- <span data-ttu-id="a94eb-155">"What-if" 配置&#x2014;を実行している場合、配置スクリプトを生成しているものの、実際に&#x2014;は実行していない場合は、SQL スクリプトを実行しないでください。</span><span class="sxs-lookup"><span data-stu-id="a94eb-155">If you're running a "what if" deployment&#x2014;in other words, if you're generating deployment scripts but not actually running them&#x2014;you shouldn't run the SQL script.</span></span>

<span data-ttu-id="a94eb-156">Contact Manager サンプルソリューションに示されているように、「[プロジェクトファイルについ](../web-deployment-in-the-enterprise/understanding-the-project-file.md)て」で説明されているプロジェクトファイルの分割方法を使用している場合は、次のように SQL スクリプトのビルド命令を分割できます。</span><span class="sxs-lookup"><span data-stu-id="a94eb-156">If you're using the split project file approach described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md), as demonstrated by the Contact Manager sample solution, you can split the build instructions for your SQL script like this:</span></span>

- <span data-ttu-id="a94eb-157">必要な環境固有のプロパティは、アクセス許可を配置するかどうかを決定するプロパティと共に、環境固有のプロジェクトファイル (たとえば、 *Env Dev. proj*) に配置する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a94eb-157">Any required environment-specific properties, together with the property that determines whether to deploy permissions, should go in the environment-specific project file (for example, *Env-Dev.proj*).</span></span>
- <span data-ttu-id="a94eb-158">MSBuild ターゲット自体は、変換先の環境間で変更されないプロパティと共に、ユニバーサルプロジェクトファイル (たとえば、 *Publish*) に配置する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a94eb-158">The MSBuild target itself, together with any properties that will not change between destination environments, should go in the universal project file (for example, *Publish.proj*).</span></span>

<span data-ttu-id="a94eb-159">環境固有のプロジェクトファイルでは、データベースサーバー名、ターゲットデータベース名、およびロールメンバーシップを配置するかどうかをユーザーが指定できるようにするブール型プロパティを定義する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a94eb-159">In the environment-specific project file, you need to define the database server name, the target database name, and a Boolean property that lets the user specify whether to deploy role memberships.</span></span>

[!code-xml[Main](deploying-database-role-memberships-to-test-environments/samples/sample3.xml)]

<span data-ttu-id="a94eb-160">ユニバーサルプロジェクトファイルで、sqlcmd 実行可能ファイルの場所と実行する SQL スクリプトの場所を指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a94eb-160">In the universal project file, you need to provide the location of the sqlcmd executable and the location of the SQL script you want to run.</span></span> <span data-ttu-id="a94eb-161">これらのプロパティは、移行先の環境に関係なく同じままです。</span><span class="sxs-lookup"><span data-stu-id="a94eb-161">These properties will remain the same regardless of the destination environment.</span></span> <span data-ttu-id="a94eb-162">また、sqlcmd コマンドを実行するために MSBuild ターゲットを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a94eb-162">You also need to create an MSBuild target to execute the sqlcmd command.</span></span>

[!code-xml[Main](deploying-database-role-memberships-to-test-environments/samples/sample4.xml)]

<span data-ttu-id="a94eb-163">Sqlcmd 実行可能ファイルの場所を静的プロパティとして追加することに注意してください。これは他のターゲットにとって便利な場合があるためです。</span><span class="sxs-lookup"><span data-stu-id="a94eb-163">Notice that you add the location of the sqlcmd executable as a static property, as this could be useful to other targets.</span></span> <span data-ttu-id="a94eb-164">これに対して、SQL スクリプトの場所と sqlcmd コマンドの構文は、ターゲット内の動的プロパティとして定義します。これは、ターゲットを実行する前に必要ではないためです。</span><span class="sxs-lookup"><span data-stu-id="a94eb-164">In contrast, you define the location of your SQL script and the syntax of the sqlcmd command as dynamic properties within the target, as they will not be required before the target is executed.</span></span> <span data-ttu-id="a94eb-165">この場合、 **Deploytestdbpermissions**ターゲットは、これらの条件が満たされた場合にのみ実行されます。</span><span class="sxs-lookup"><span data-stu-id="a94eb-165">In this case, the **DeployTestDBPermissions** target will only be executed if these conditions are met:</span></span>

- <span data-ttu-id="a94eb-166">**DeployTestDBRoleMemberships**プロパティは**true**に設定されています。</span><span class="sxs-lookup"><span data-stu-id="a94eb-166">The **DeployTestDBRoleMemberships** property is set to **true**.</span></span>
- <span data-ttu-id="a94eb-167">ユーザーに**WhatIf = true**フラグが指定されていません。</span><span class="sxs-lookup"><span data-stu-id="a94eb-167">The user hasn't specified a **WhatIf=true** flag.</span></span>

<span data-ttu-id="a94eb-168">最後に、必ずターゲットを呼び出してください。</span><span class="sxs-lookup"><span data-stu-id="a94eb-168">Finally, don't forget to invoke the target.</span></span> <span data-ttu-id="a94eb-169">既定の**Fullpublish**ターゲットの依存関係の一覧にターゲットを追加することで、このファイルを*パブリッシュします*。</span><span class="sxs-lookup"><span data-stu-id="a94eb-169">In the *Publish.proj* file, you can do this by adding the target to the dependency list for the default **FullPublish** target.</span></span> <span data-ttu-id="a94eb-170">**Publishdbpackages**ターゲットが実行されるまでは、 **Deploytestdbpermissions**ターゲットが実行されないようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="a94eb-170">You need to ensure that the **DeployTestDBPermissions** target is not executed until the **PublishDbPackages** target has been executed.</span></span>

[!code-xml[Main](deploying-database-role-memberships-to-test-environments/samples/sample5.xml)]

## <a name="conclusion"></a><span data-ttu-id="a94eb-171">まとめ</span><span class="sxs-lookup"><span data-stu-id="a94eb-171">Conclusion</span></span>

<span data-ttu-id="a94eb-172">このトピックでは、データベースプロジェクトを配置するときに、データベースユーザーとロールメンバーシップを配置後アクションとして追加できる方法の1つについて説明します。</span><span class="sxs-lookup"><span data-stu-id="a94eb-172">This topic described one way in which you can add database users and role memberships as a post-deployment action when you deploy a database project.</span></span> <span data-ttu-id="a94eb-173">通常、この方法は、テスト環境でデータベースを定期的に再作成する場合に便利ですが、データベースをステージング環境または運用環境に配置するときは通常は避ける必要があります。</span><span class="sxs-lookup"><span data-stu-id="a94eb-173">This is typically useful when you regularly re-create a database in a test environment, but it should usually be avoided when you deploy databases to staging or production environments.</span></span> <span data-ttu-id="a94eb-174">そのため、データベースユーザーとロールメンバーシップが適切な場合にのみ作成されるように、必要な条件ロジックを必ず使用してください。</span><span class="sxs-lookup"><span data-stu-id="a94eb-174">As such, you should ensure that you use the necessary conditional logic so that database users and role memberships are only created when it's appropriate to do so.</span></span>

## <a name="further-reading"></a><span data-ttu-id="a94eb-175">参考資料</span><span class="sxs-lookup"><span data-stu-id="a94eb-175">Further Reading</span></span>

<span data-ttu-id="a94eb-176">VSDBCMD を使用してデータベースプロジェクトを配置する方法の詳細については、「[データベースプロジェクトの配置](../web-deployment-in-the-enterprise/deploying-database-projects.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a94eb-176">For more information on using VSDBCMD to deploy database projects, see [Deploying Database Projects](../web-deployment-in-the-enterprise/deploying-database-projects.md).</span></span> <span data-ttu-id="a94eb-177">さまざまなターゲット環境のデータベース配置をカスタマイズする方法については、「[複数の環境でのデータベース配置のカスタマイズ](customizing-database-deployments-for-multiple-environments.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a94eb-177">For guidance on customizing database deployments for different target environments, see [Customizing Database Deployments for Multiple Environments](customizing-database-deployments-for-multiple-environments.md).</span></span> <span data-ttu-id="a94eb-178">カスタム MSBuild プロジェクトファイルを使用した配置プロセスの制御の詳細については、「[プロジェクトファイルについ](../web-deployment-in-the-enterprise/understanding-the-project-file.md)て」および「[ビルドプロセスについ](../web-deployment-in-the-enterprise/understanding-the-build-process.md)て」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a94eb-178">For more information on using custom MSBuild project files to control the deployment process, see [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md) and [Understanding the Build Process](../web-deployment-in-the-enterprise/understanding-the-build-process.md).</span></span> <span data-ttu-id="a94eb-179">Sqlcmd のコマンドラインオプションの詳細については、「 [Sqlcmd ユーティリティ](https://msdn.microsoft.com/library/ms162773.aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a94eb-179">For more information on sqlcmd command-line options, see [sqlcmd Utility](https://msdn.microsoft.com/library/ms162773.aspx).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="a94eb-180">[前へ](customizing-database-deployments-for-multiple-environments.md)
> [次へ](deploying-membership-databases-to-enterprise-environments.md)</span><span class="sxs-lookup"><span data-stu-id="a94eb-180">[Previous](customizing-database-deployments-for-multiple-environments.md)
[Next](deploying-membership-databases-to-enterprise-environments.md)</span></span>
