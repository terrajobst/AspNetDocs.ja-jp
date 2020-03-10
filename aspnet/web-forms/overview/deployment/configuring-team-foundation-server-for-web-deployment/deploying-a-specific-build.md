---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/deploying-a-specific-build
title: 特定のビルドを配置する |Microsoft Docs
author: jrjlee
description: このトピックでは、ステージングまたは実稼働 enviro など、特定の以前のビルドから新しい変換先に web パッケージとデータベーススクリプトを配置する方法について説明します。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: c979535f-48a3-4ec4-a633-a77889b86ddb
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/deploying-a-specific-build
msc.type: authoredcontent
ms.openlocfilehash: 6bede6b36c24ade928ab052e14daec1e017bd0b2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78519574"
---
# <a name="deploying-a-specific-build"></a><span data-ttu-id="6cbf9-103">特定のビルドを配置する</span><span class="sxs-lookup"><span data-stu-id="6cbf9-103">Deploying a Specific Build</span></span>

<span data-ttu-id="6cbf9-104">[Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="6cbf9-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

<span data-ttu-id="6cbf9-105">[[Download PDF]\(PDF をダウンロード\)](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)</span><span class="sxs-lookup"><span data-stu-id="6cbf9-105">[Download PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)</span></span>

> <span data-ttu-id="6cbf9-106">このトピックでは、ステージング環境や運用環境など、特定の以前のビルドから新しい変換先に web パッケージとデータベーススクリプトを配置する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="6cbf9-106">This topic describes how to deploy web packages and database scripts from a specific previous build to a new destination, like a staging or production environment.</span></span>

<span data-ttu-id="6cbf9-107">このトピックでは、Fabrikam, Inc. という架空の企業のエンタープライズ展開要件に基づいて、一連のチュートリアルの一部を説明します。このチュートリアルシリーズでは、&#x2014; [Contact Manager ソリューション](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;のサンプルソリューションを使用して、ASP.NET MVC 3 アプリケーション、Windows Communication Foundation (WCF) サービス、データベースプロジェクトなど、現実的なレベルの複雑さを持つ web アプリケーションを表します。</span><span class="sxs-lookup"><span data-stu-id="6cbf9-107">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

<span data-ttu-id="6cbf9-108">これらのチュートリアルの中核となる配置方法は、「プロジェクト[ファイルについ](../web-deployment-in-the-enterprise/understanding-the-project-file.md)て」で説明されている分割プロジェクトファイルアプローチに基づいています。この方法で&#x2014;は、ビルドおよび配置プロセスは、すべての変換先環境に適用されるビルド命令を含む2つのプロジェクトファイルと、環境固有のビルドと配置の設定を含んでいます。</span><span class="sxs-lookup"><span data-stu-id="6cbf9-108">The deployment method at the heart of these tutorials is based on the split project file approach described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md), in which the build and deployment process is controlled by two project files&#x2014;one containing build instructions that apply to every destination environment, and one containing environment-specific build and deployment settings.</span></span> <span data-ttu-id="6cbf9-109">ビルド時に、環境固有のプロジェクトファイルが環境に依存しないプロジェクトファイルにマージされ、ビルド命令の完全なセットが形成されます。</span><span class="sxs-lookup"><span data-stu-id="6cbf9-109">At build time, the environment-specific project file is merged into the environment-agnostic project file to form a complete set of build instructions.</span></span>

## <a name="task-overview"></a><span data-ttu-id="6cbf9-110">タスクの概要</span><span class="sxs-lookup"><span data-stu-id="6cbf9-110">Task Overview</span></span>

<span data-ttu-id="6cbf9-111">これまでは、このチュートリアルでは、シングルステップまたは自動化されたプロセスの一部として、web アプリケーションとデータベースを構築、パッケージ化、および配置する方法に重点を置いています。</span><span class="sxs-lookup"><span data-stu-id="6cbf9-111">Until now, the topics in this tutorial set have focused on how to build, package, and deploy web applications and databases as part of a single-step or automated process.</span></span> <span data-ttu-id="6cbf9-112">ただし、いくつかの一般的なシナリオでは、ドロップフォルダー内のビルドの一覧から配置するリソースを選択する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6cbf9-112">However, in some common scenarios, you'll want to select the resources that you deploy from a list of builds in a drop folder.</span></span> <span data-ttu-id="6cbf9-113">つまり、最新のビルドが配置するビルドではない可能性があります。</span><span class="sxs-lookup"><span data-stu-id="6cbf9-113">In other words, the latest build may not be the build you want to deploy.</span></span>

<span data-ttu-id="6cbf9-114">前のトピック「[配置をサポートするビルド定義の作成](creating-a-build-definition-that-supports-deployment.md)」で説明した継続的インテグレーション (CI) シナリオを検討してください。</span><span class="sxs-lookup"><span data-stu-id="6cbf9-114">Consider the continuous integration (CI) scenario described in the previous topic, [Creating a Build Definition That Supports Deployment](creating-a-build-definition-that-supports-deployment.md).</span></span> <span data-ttu-id="6cbf9-115">Team Foundation Server (TFS) 2010 でビルド定義を作成しました。</span><span class="sxs-lookup"><span data-stu-id="6cbf9-115">You've created a build definition in Team Foundation Server (TFS) 2010.</span></span> <span data-ttu-id="6cbf9-116">開発者がコードを TFS にチェックインするたびに、チームビルドはコードをビルドし、ビルドプロセスの一部として web パッケージとデータベーススクリプトを作成し、単体テストを実行して、リソースをテスト環境に配置します。</span><span class="sxs-lookup"><span data-stu-id="6cbf9-116">Every time a developer checks code into TFS, Team Build will build your code, create web packages and database scripts as part of the build process, run any unit tests, and deploy your resources to a test environment.</span></span> <span data-ttu-id="6cbf9-117">ビルド定義の作成時に構成した保持ポリシーに応じて、TFS は以前のビルドの数を保持します。</span><span class="sxs-lookup"><span data-stu-id="6cbf9-117">Depending on the retention policy you configured when you created the build definition, TFS will retain a certain number of previous builds.</span></span>

![](deploying-a-specific-build/_static/image1.png)

<span data-ttu-id="6cbf9-118">ここで、テスト環境でこれらのビルドのいずれかに対して検証と検証のテストを実行し、アプリケーションをステージング環境に配置する準備ができたとします。</span><span class="sxs-lookup"><span data-stu-id="6cbf9-118">Now, suppose you've performed verification and validation testing against one of these builds in your test environment, and you're ready to deploy your application to a staging environment.</span></span> <span data-ttu-id="6cbf9-119">それまでの間、開発者は新しいコードをチェックインした可能性があります。</span><span class="sxs-lookup"><span data-stu-id="6cbf9-119">In the meantime, developers may have checked in new code.</span></span> <span data-ttu-id="6cbf9-120">ソリューションをリビルドしてステージング環境に配置する必要はなく、ステージング環境に最新のビルドを配置する必要もありません。</span><span class="sxs-lookup"><span data-stu-id="6cbf9-120">You don't want to rebuild the solution and deploy to the staging environment, and you don't want to deploy the latest build to the staging environment.</span></span> <span data-ttu-id="6cbf9-121">代わりに、テストサーバーで検証および検証した特定のビルドを配置します。</span><span class="sxs-lookup"><span data-stu-id="6cbf9-121">Instead, you want to deploy the specific build that you've verified and validated on the test servers.</span></span>

<span data-ttu-id="6cbf9-122">これを実現するには、Microsoft Build Engine (MSBuild) に対して、特定のビルドが生成した web パッケージとデータベーススクリプトの検索先を指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6cbf9-122">To accomplish this, you need to tell the Microsoft Build Engine (MSBuild) where to find the web packages and database scripts that a specific build generated.</span></span>

## <a name="overriding-the-outputroot-property"></a><span data-ttu-id="6cbf9-123">OutputRoot プロパティのオーバーライド</span><span class="sxs-lookup"><span data-stu-id="6cbf9-123">Overriding the OutputRoot Property</span></span>

<span data-ttu-id="6cbf9-124">[サンプルソリューション](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)では、 *Publish*ファイルは**outputroot**という名前のプロパティを宣言します。</span><span class="sxs-lookup"><span data-stu-id="6cbf9-124">In the [sample solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md), the *Publish.proj* file declares a property named **OutputRoot**.</span></span> <span data-ttu-id="6cbf9-125">名前が示すように、これは、ビルドプロセスが生成するすべてのものを含むルートフォルダーです。</span><span class="sxs-lookup"><span data-stu-id="6cbf9-125">As the name suggests, this is the root folder that contains everything that the build process generates.</span></span> <span data-ttu-id="6cbf9-126">*Publish*ファイルで、 **outputroot**プロパティがすべてのデプロイリソースのルートの場所を参照していることを確認できます。</span><span class="sxs-lookup"><span data-stu-id="6cbf9-126">In the *Publish.proj* file, you can see that the **OutputRoot** property refers to the root location for all deployment resources.</span></span>

> [!NOTE]
> <span data-ttu-id="6cbf9-127">**Outputroot**は、一般的に使用されるプロパティ名です。</span><span class="sxs-lookup"><span data-stu-id="6cbf9-127">**OutputRoot** is a commonly used property name.</span></span> <span data-ttu-id="6cbf9-128">またC# 、ビジュアルおよび Visual Basic プロジェクトファイルは、すべてのビルド出力のルートの場所を格納するために、このプロパティを宣言します。</span><span class="sxs-lookup"><span data-stu-id="6cbf9-128">Visual C# and Visual Basic project files also declare this property to store the root location for all build outputs.</span></span>

[!code-xml[Main](deploying-a-specific-build/samples/sample1.xml)]

<span data-ttu-id="6cbf9-129">プロジェクトファイルで、以前の TFS ビルド&#x2014;&#x2014;の出力のように、別の場所から web パッケージとデータベーススクリプトを配置する場合は、単に**outputroot**プロパティをオーバーライドする必要があります。</span><span class="sxs-lookup"><span data-stu-id="6cbf9-129">If you want your project file to deploy web packages and database scripts from a different location&#x2014;like the outputs of a previous TFS build&#x2014;you simply need to override the **OutputRoot** property.</span></span> <span data-ttu-id="6cbf9-130">プロパティ値は、チームビルドサーバーの関連するビルドフォルダーに設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6cbf9-130">You should set the property value to the relevant build folder on the Team Build server.</span></span> <span data-ttu-id="6cbf9-131">コマンドラインから MSBuild を実行していた場合は、コマンドライン引数として**Outputroot**の値を指定できます。</span><span class="sxs-lookup"><span data-stu-id="6cbf9-131">If you were running MSBuild from the command line, you could specify a value for **OutputRoot** as a command-line argument:</span></span>

[!code-console[Main](deploying-a-specific-build/samples/sample2.cmd)]

<span data-ttu-id="6cbf9-132">ただし、実際には、ビルド出力を使用する予定がない&#x2014;場合は、ビルドターゲットをスキップするだけで、ソリューションをビルドすることはできません。</span><span class="sxs-lookup"><span data-stu-id="6cbf9-132">In practice, however, you'd also want to skip the **Build** target&#x2014;there's no point in building your solution if you don't plan to use the build outputs.</span></span> <span data-ttu-id="6cbf9-133">これを行うには、コマンドラインから実行するターゲットを指定します。</span><span class="sxs-lookup"><span data-stu-id="6cbf9-133">You could do this by specifying the targets you want to execute from the command line:</span></span>

[!code-console[Main](deploying-a-specific-build/samples/sample3.cmd)]

<span data-ttu-id="6cbf9-134">ただし、ほとんどの場合は、TFS ビルド定義に配置ロジックをビルドします。</span><span class="sxs-lookup"><span data-stu-id="6cbf9-134">However, in most cases, you'll want to build your deployment logic into a TFS build definition.</span></span> <span data-ttu-id="6cbf9-135">これにより、**キュービルド**アクセス許可を持つユーザーは、TFS サーバーへの接続を使用して Visual Studio のインストールから配置をトリガーできます。</span><span class="sxs-lookup"><span data-stu-id="6cbf9-135">This enables users with the **Queue builds** permission to trigger the deployment from any Visual Studio installation with a connection to the TFS server.</span></span>

## <a name="creating-a-build-definition-to-deploy-specific-builds"></a><span data-ttu-id="6cbf9-136">特定のビルドを配置するためのビルド定義の作成</span><span class="sxs-lookup"><span data-stu-id="6cbf9-136">Creating a Build Definition to Deploy Specific Builds</span></span>

<span data-ttu-id="6cbf9-137">次の手順では、ユーザーが1つのコマンドでステージング環境への配置をトリガーできるようにするビルド定義を作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="6cbf9-137">The next procedure describes how to create a build definition that enables users to trigger deployments to a staging environment with a single command.</span></span>

<span data-ttu-id="6cbf9-138">この場合、カスタムプロジェクトファイルで配置ロジックを実行するために&#x2014;必要なものをビルド定義に実際に作成する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="6cbf9-138">In this case, you don't want the build definition to actually build anything&#x2014;you just want it to execute the deployment logic in your custom project file.</span></span> <span data-ttu-id="6cbf9-139">*Publish*ファイルには、ファイルがチームビルドで実行されている場合に**ビルド**ターゲットをスキップする条件付きロジックが含まれています。</span><span class="sxs-lookup"><span data-stu-id="6cbf9-139">The *Publish.proj* file includes conditional logic that skips the **Build** target if the file is running in Team Build.</span></span> <span data-ttu-id="6cbf9-140">これを行うには、組み込みの**BuildingInTeamBuild**プロパティを評価します。これは、チームビルドでプロジェクトファイルを実行すると、自動的に**true**に設定されます。</span><span class="sxs-lookup"><span data-stu-id="6cbf9-140">It does this by evaluating the built-in **BuildingInTeamBuild** property, which is automatically set to **true** if you run your project file in Team Build.</span></span> <span data-ttu-id="6cbf9-141">その結果、ビルドプロセスをスキップし、単にプロジェクトファイルを実行して既存のビルドを配置することができます。</span><span class="sxs-lookup"><span data-stu-id="6cbf9-141">As a result, you can skip the build process and simply run the project file to deploy an existing build.</span></span>

<span data-ttu-id="6cbf9-142">**手動で配置をトリガーするビルド定義を作成するには**</span><span class="sxs-lookup"><span data-stu-id="6cbf9-142">**To create a build definition to trigger deployment manually**</span></span>

1. <span data-ttu-id="6cbf9-143">Visual Studio 2010 の **[チームエクスプローラー]** ウィンドウで、チームプロジェクトノードを展開し、 **[ビルド]** を右クリックして、 **[新しいビルド定義]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="6cbf9-143">In Visual Studio 2010, in the **Team Explorer** window, expand your team project node, right-click **Builds**, and then click **New Build Definition**.</span></span>

    ![](deploying-a-specific-build/_static/image2.png)
2. <span data-ttu-id="6cbf9-144">**[全般]** タブで、ビルド定義に名前 ( **deploytostaging**など) とオプションの説明を指定します。</span><span class="sxs-lookup"><span data-stu-id="6cbf9-144">On the **General** tab, give the build definition a name (for example, **DeployToStaging**) and an optional description.</span></span>
3. <span data-ttu-id="6cbf9-145">**[トリガー]** タブで、 **[手動-チェックインで新しいビルドをトリガーしない]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="6cbf9-145">On the **Trigger** tab, select **Manual – Check-ins do not trigger a new build**.</span></span>
4. <span data-ttu-id="6cbf9-146">**[ビルドの既定値]** タブで、 **[ビルド出力を次の格納フォルダーにコピーする]** ボックスに、格納フォルダーの汎用名前付け規則 (UNC) パス (たとえば、 **\\TFSBUILD\Drops**) を入力します。</span><span class="sxs-lookup"><span data-stu-id="6cbf9-146">On the **Build Defaults** tab, in the **Copy build output to the following drop folder** box, type the Universal Naming Convention (UNC) path of your drop folder (for example, **\\TFSBUILD\Drops**).</span></span>

    ![](deploying-a-specific-build/_static/image3.png)
5. <span data-ttu-id="6cbf9-147">**[プロセス]** タブの **[ビルドプロセスファイル]** ドロップダウンリストで、 **[defaulttemplate .xaml]** を選択したままにします。</span><span class="sxs-lookup"><span data-stu-id="6cbf9-147">On the **Process** tab, in the **Build process file** dropdown list, leave **DefaultTemplate.xaml** selected.</span></span> <span data-ttu-id="6cbf9-148">これは、すべての新しいチームプロジェクトに追加される既定のビルドプロセステンプレートの1つです。</span><span class="sxs-lookup"><span data-stu-id="6cbf9-148">This is one of the default build process templates that get added to all new team projects.</span></span>
6. <span data-ttu-id="6cbf9-149">**[ビルドプロセスパラメーター]** テーブルで、 **[ビルドする項目]** 行をクリックし、**省略記号**ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="6cbf9-149">In the **Build process parameters** table, click in the **Items to Build** row, and then click the **ellipsis** button.</span></span>

    ![](deploying-a-specific-build/_static/image4.png)
7. <span data-ttu-id="6cbf9-150">**[ビルドする項目]** ダイアログボックスで、 **[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="6cbf9-150">In the **Items to Build** dialog box, click **Add**.</span></span>
8. <span data-ttu-id="6cbf9-151">**[項目の種類]** ボックスの一覧で、 **[MSBuild プロジェクトファイル]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="6cbf9-151">In the **Items of type** dropdown list, select **MSBuild Project files**.</span></span>
9. <span data-ttu-id="6cbf9-152">デプロイプロセスを制御するカスタムプロジェクトファイルの場所を参照し、ファイルを選択して、[ **OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="6cbf9-152">Browse to the location of the custom project file with which you control the deployment process, select the file, and then click **OK**.</span></span>

    ![](deploying-a-specific-build/_static/image5.png)
10. <span data-ttu-id="6cbf9-153">**[ビルドする項目]** ダイアログボックスで、[ **OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="6cbf9-153">In the **Items to Build** dialog box, click **OK**.</span></span>
11. <span data-ttu-id="6cbf9-154">**[ビルドプロセスパラメーター]** テーブルで、 **[詳細設定**] セクションを展開します。</span><span class="sxs-lookup"><span data-stu-id="6cbf9-154">In the **Build process parameters** table, expand the **Advanced** section.</span></span>
12. <span data-ttu-id="6cbf9-155">**[MSBuild 引数]** 行で、環境固有のプロジェクトファイルの場所を指定し、ビルドフォルダーの場所のプレースホルダーを追加します。</span><span class="sxs-lookup"><span data-stu-id="6cbf9-155">In the **MSBuild Arguments** row, specify the location of your environment-specific project file and add a placeholder for the location of your build folder:</span></span>

    [!code-console[Main](deploying-a-specific-build/samples/sample4.cmd)]

    ![](deploying-a-specific-build/_static/image6.png)

    > [!NOTE]
    > <span data-ttu-id="6cbf9-156">ビルドをキューに置きたびに、 **Outputroot**値をオーバーライドする必要があります。</span><span class="sxs-lookup"><span data-stu-id="6cbf9-156">You'll need to override the **OutputRoot** value every time you queue a build.</span></span> <span data-ttu-id="6cbf9-157">これについては、次の手順で説明します。</span><span class="sxs-lookup"><span data-stu-id="6cbf9-157">This is covered in the next procedure.</span></span>
13. <span data-ttu-id="6cbf9-158">**[保存]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="6cbf9-158">Click **Save**.</span></span>

<span data-ttu-id="6cbf9-159">ビルドをトリガーするときに、配置するビルドを指すように**Outputroot**プロパティを更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6cbf9-159">When you trigger a build, you need to update the **OutputRoot** property to point to the build you want to deploy.</span></span>

<span data-ttu-id="6cbf9-160">**ビルド定義から特定のビルドを配置するには**</span><span class="sxs-lookup"><span data-stu-id="6cbf9-160">**To deploy a specific build from a build definition**</span></span>

1. <span data-ttu-id="6cbf9-161">**[チームエクスプローラー]** ウィンドウで、ビルド定義を右クリックし、 **[新しいビルドをキューに追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="6cbf9-161">In the **Team Explorer** window, right-click the build definition, and then click **Queue New Build**.</span></span>

    ![](deploying-a-specific-build/_static/image7.png)
2. <span data-ttu-id="6cbf9-162">**[キュービルド]** ダイアログボックスの **[パラメーター]** タブで、 **[詳細設定]** セクションを展開します。</span><span class="sxs-lookup"><span data-stu-id="6cbf9-162">In the **Queue Build** dialog box, on the **Parameters** tab, expand the **Advanced** section.</span></span>
3. <span data-ttu-id="6cbf9-163">**[MSBuild 引数]** 行で、 **outputroot**プロパティの値をビルドフォルダーの場所に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="6cbf9-163">In the **MSBuild Arguments** row, replace the value of the **OutputRoot** property with the location of your build folder.</span></span> <span data-ttu-id="6cbf9-164">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="6cbf9-164">For example:</span></span>

    [!code-console[Main](deploying-a-specific-build/samples/sample5.cmd)]

    ![](deploying-a-specific-build/_static/image8.png)

    > [!NOTE]
    > <span data-ttu-id="6cbf9-165">ビルドフォルダーへのパスの末尾には、末尾にスラッシュを含めてください。</span><span class="sxs-lookup"><span data-stu-id="6cbf9-165">Be sure to include a trailing slash at the end of the path to your build folder.</span></span>
4. <span data-ttu-id="6cbf9-166">**[キュー]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="6cbf9-166">Click **Queue**.</span></span>

<span data-ttu-id="6cbf9-167">ビルドをキューに配置すると、プロジェクトファイルによって、 **Outputroot**プロパティに指定したビルド格納フォルダーからデータベーススクリプトと web パッケージが配置されます。</span><span class="sxs-lookup"><span data-stu-id="6cbf9-167">When you queue the build, the project file will deploy the database scripts and web packages from the build drop folder you specified in the **OutputRoot** property.</span></span>

## <a name="conclusion"></a><span data-ttu-id="6cbf9-168">まとめ</span><span class="sxs-lookup"><span data-stu-id="6cbf9-168">Conclusion</span></span>

<span data-ttu-id="6cbf9-169">このトピックでは、split project file デプロイモデルを使用して、特定の以前のビルドから web パッケージやデータベーススクリプトなどのデプロイリソースを発行する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="6cbf9-169">This topic described how to publish deployment resources, like web packages and database scripts, from a specific previous build using the split project file deployment model.</span></span> <span data-ttu-id="6cbf9-170">ここでは、 **Outputroot**プロパティをオーバーライドする方法と、配置ロジックを TFS ビルド定義に組み込む方法について説明しました。</span><span class="sxs-lookup"><span data-stu-id="6cbf9-170">It explained how to override the **OutputRoot** property and how to incorporate the deployment logic into a TFS build definition.</span></span>

## <a name="further-reading"></a><span data-ttu-id="6cbf9-171">参考資料</span><span class="sxs-lookup"><span data-stu-id="6cbf9-171">Further Reading</span></span>

<span data-ttu-id="6cbf9-172">ビルド定義の作成の詳細については、「[基本的なビルド定義の作成](https://msdn.microsoft.com/library/ms181716.aspx)」および「[ビルドプロセスの定義](https://msdn.microsoft.com/library/ms181715.aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="6cbf9-172">For more information on creating build definitions, see [Create a Basic Build Definition](https://msdn.microsoft.com/library/ms181716.aspx) and [Define Your Build Process](https://msdn.microsoft.com/library/ms181715.aspx).</span></span> <span data-ttu-id="6cbf9-173">ビルドをキューに追加する方法の詳細については、「[ビルドをキュー](https://msdn.microsoft.com/library/ms181722.aspx)に入れ」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="6cbf9-173">For more guidance on queuing builds, see [Queue a Build](https://msdn.microsoft.com/library/ms181722.aspx).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="6cbf9-174">[前へ](creating-a-build-definition-that-supports-deployment.md)
> [次へ](configuring-permissions-for-team-build-deployment.md)</span><span class="sxs-lookup"><span data-stu-id="6cbf9-174">[Previous](creating-a-build-definition-that-supports-deployment.md)
[Next](configuring-permissions-for-team-build-deployment.md)</span></span>
