---
uid: web-forms/overview/deployment/visual-studio-web-deployment/command-line-deployment
title: 'Visual Studio を使用した ASP.NET Web デプロイ: コマンドラインデプロイ |Microsoft Docs'
author: tdykstra
description: このチュートリアルシリーズでは、ASP.NET web アプリケーションをデプロイ (発行) して、Web Apps またはサードパーティのホスティングプロバイダーに Azure App Service する方法について説明します。
ms.author: riande
ms.date: 02/15/2013
ms.assetid: 82b8dea0-f062-4ee4-8784-3ffa30fbb1ca
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/command-line-deployment
msc.type: authoredcontent
ms.openlocfilehash: 13cfe4492398b59f2c80394689cc113ccb218c60
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74634199"
---
# <a name="aspnet-web-deployment-using-visual-studio-command-line-deployment"></a><span data-ttu-id="7e4bc-103">Visual Studio を使用した ASP.NET Web デプロイ: コマンドライン展開</span><span class="sxs-lookup"><span data-stu-id="7e4bc-103">ASP.NET Web Deployment using Visual Studio: Command Line Deployment</span></span>

<span data-ttu-id="7e4bc-104">[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="7e4bc-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="7e4bc-105">スタートプロジェクトのダウンロード</span><span class="sxs-lookup"><span data-stu-id="7e4bc-105">Download Starter Project</span></span>](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> <span data-ttu-id="7e4bc-106">このチュートリアルシリーズでは、Visual Studio 2012 または Visual Studio 2010 を使用して、Azure App Service Web Apps またはサードパーティのホスティングプロバイダーにするために、ASP.NET web アプリケーションをデプロイ (発行) する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="7e4bc-106">This tutorial series shows you how to deploy (publish) an ASP.NET web application to Azure App Service Web Apps or to a third-party hosting provider, by using Visual Studio 2012 or Visual Studio 2010.</span></span> <span data-ttu-id="7e4bc-107">シリーズの詳細については、[シリーズの最初のチュートリアル](introduction.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="7e4bc-107">For information about the series, see [the first tutorial in the series](introduction.md).</span></span>

## <a name="overview"></a><span data-ttu-id="7e4bc-108">の概要</span><span class="sxs-lookup"><span data-stu-id="7e4bc-108">Overview</span></span>

<span data-ttu-id="7e4bc-109">このチュートリアルでは、コマンドラインから Visual Studio web 発行パイプラインを呼び出す方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="7e4bc-109">This tutorial shows you how to invoke the Visual Studio web publish pipeline from the command line.</span></span> <span data-ttu-id="7e4bc-110">これは、Visual Studio で手動ではなく、[ソースコードのバージョン管理システム](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control.md)を使用して、[配置プロセスを自動化](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery.md)する場合に便利です。</span><span class="sxs-lookup"><span data-stu-id="7e4bc-110">This is useful for scenarios where you want to [automate the deployment process](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery.md) instead of doing it manually in Visual Studio, typically by using a [source code version control system](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control.md).</span></span>

## <a name="make-a-change-to-deploy"></a><span data-ttu-id="7e4bc-111">デプロイを変更する</span><span class="sxs-lookup"><span data-stu-id="7e4bc-111">Make a change to deploy</span></span>

<span data-ttu-id="7e4bc-112">現在、[バージョン情報] ページには、テンプレートコードが表示されます。</span><span class="sxs-lookup"><span data-stu-id="7e4bc-112">Currently the About page displays the template code.</span></span>

![テンプレートコードを使用したページの概要](command-line-deployment/_static/image1.png)

<span data-ttu-id="7e4bc-114">これを、学生登録の概要を表示するコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="7e4bc-114">You'll replace that with code that displays a summary of student enrollment.</span></span>

<span data-ttu-id="7e4bc-115">*About .aspx*ページを開き、`MainContent` `Content` 要素内のすべてのマークアップを削除し、その場所に次のマークアップを挿入します。</span><span class="sxs-lookup"><span data-stu-id="7e4bc-115">Open the *About.aspx* page, delete all of the markup inside the `MainContent` `Content` element, and insert the following markup in its place:</span></span>

[!code-aspx[Main](command-line-deployment/samples/sample1.aspx)]

<span data-ttu-id="7e4bc-116">プロジェクトを実行し、 **[バージョン情報]** ページを選択します。</span><span class="sxs-lookup"><span data-stu-id="7e4bc-116">Run the project and select the **About** page.</span></span>

![About ページ](command-line-deployment/_static/image2.png)

## <a name="deploy-to-test-by-using-the-command-line"></a><span data-ttu-id="7e4bc-118">コマンドラインを使用してテストに配置する</span><span class="sxs-lookup"><span data-stu-id="7e4bc-118">Deploy to Test by using the command line</span></span>

<span data-ttu-id="7e4bc-119">別のデータベースの変更を配置しないので、ContosoUniversity データベースの dbDacFx データベースの配置を無効にしてください。</span><span class="sxs-lookup"><span data-stu-id="7e4bc-119">You won't be deploying another database change, so disable dbDacFx database deployment for the aspnet-ContosoUniversity database.</span></span> <span data-ttu-id="7e4bc-120">Web の**発行**ウィザードを開き、3つの発行プロファイルのそれぞれで、 **[設定]** タブの **[データベースの更新]** チェックボックスをオフにします。</span><span class="sxs-lookup"><span data-stu-id="7e4bc-120">Open the **Publish Web** wizard, and in each of the three publish profiles, clear the **Update Database** check box on the **Settings** tab.</span></span>

<span data-ttu-id="7e4bc-121">Windows 8 のスタートページで、 **VS2012 の開発者コマンドプロンプト**を検索します。</span><span class="sxs-lookup"><span data-stu-id="7e4bc-121">In the Windows 8 Start page, search for **Developer Command Prompt for VS2012**.</span></span>

<span data-ttu-id="7e4bc-122">**VS2012 の [開発者コマンドプロンプト**] のアイコンを右クリックし、 **[管理者として実行]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="7e4bc-122">Right-click the icon for **Developer Command Prompt for VS2012** and click **Run as administrator**.</span></span>

<span data-ttu-id="7e4bc-123">コマンドプロンプトで次のコマンドを入力し、ソリューションファイルへのパスをソリューションファイルへのパスに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="7e4bc-123">Enter the following command at the command prompt, replacing the path to the solution file with the path to your solution file:</span></span>

[!code-console[Main](command-line-deployment/samples/sample2.cmd)]

<span data-ttu-id="7e4bc-124">MSBuild によってソリューションがビルドされ、テスト環境に配置されます。</span><span class="sxs-lookup"><span data-stu-id="7e4bc-124">MSBuild builds the solution and deploys it to the test environment.</span></span>

![コマンド ライン出力](command-line-deployment/_static/image3.png)

<span data-ttu-id="7e4bc-126">ブラウザーを開き、`http://localhost/ContosoUniversity`にアクセスし、 **[バージョン情報]** ページをクリックして、展開が成功したことを確認します。</span><span class="sxs-lookup"><span data-stu-id="7e4bc-126">Open a browser and go to `http://localhost/ContosoUniversity`, then click the **About** page to verify that the deployment was successful.</span></span>

<span data-ttu-id="7e4bc-127">テストで学生を作成していない場合は、 **[Student Body Statistics]** \ (学生の本文 \) の見出しの下に空のページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="7e4bc-127">If you haven't created any students in test, you'll see an empty page under the **Student Body Statistics** heading.</span></span> <span data-ttu-id="7e4bc-128">**学生**のページにアクセスして、 **[学生の追加]** をクリックし、いくつかの学生を追加してから、 **[バージョン情報]** ページに戻って学生の統計情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="7e4bc-128">Go to the **Students** page, click **Add Student**, and add some students, and then return to the **About** page to see student statistics.</span></span>

![テスト環境のページについて](command-line-deployment/_static/image4.png)

## <a name="key-command-line-options"></a><span data-ttu-id="7e4bc-130">キーのコマンドラインオプション</span><span class="sxs-lookup"><span data-stu-id="7e4bc-130">Key command line options</span></span>

<span data-ttu-id="7e4bc-131">入力したコマンドによって、ソリューションファイルのパスと2つのプロパティが MSBuild に渡されました。</span><span class="sxs-lookup"><span data-stu-id="7e4bc-131">The command that you entered passed the solution file path and two properties to MSBuild:</span></span>

[!code-console[Main](command-line-deployment/samples/sample3.cmd)]

### <a name="deploying-the-solution-versus-deploying-individual-projects"></a><span data-ttu-id="7e4bc-132">ソリューションの配置と個々のプロジェクトの配置</span><span class="sxs-lookup"><span data-stu-id="7e4bc-132">Deploying the solution versus deploying individual projects</span></span>

<span data-ttu-id="7e4bc-133">ソリューションファイルを指定すると、ソリューション内のすべてのプロジェクトがビルドされます。</span><span class="sxs-lookup"><span data-stu-id="7e4bc-133">Specifying the solution file causes all projects in the solution to be built.</span></span> <span data-ttu-id="7e4bc-134">ソリューションに複数の web プロジェクトがある場合は、次の MSBuild 動作が適用されます。</span><span class="sxs-lookup"><span data-stu-id="7e4bc-134">If you have multiple web projects in the solution, the following MSBuild behavior applies:</span></span>

- <span data-ttu-id="7e4bc-135">コマンドラインで指定したプロパティは、すべてのプロジェクトに渡されます。</span><span class="sxs-lookup"><span data-stu-id="7e4bc-135">The properties that you specify on the command line are passed to every project.</span></span> <span data-ttu-id="7e4bc-136">したがって、各 web プロジェクトには、指定した名前の発行プロファイルが必要です。</span><span class="sxs-lookup"><span data-stu-id="7e4bc-136">Therefore, each web project must have a publish profile with the name that you specify.</span></span> <span data-ttu-id="7e4bc-137">`/p:PublishProfile=Test`を指定する場合、各 web プロジェクトには*Test*という名前の発行プロファイルが必要です。</span><span class="sxs-lookup"><span data-stu-id="7e4bc-137">If you specify `/p:PublishProfile=Test`, each web project must have a publish profile named *Test*.</span></span>
- <span data-ttu-id="7e4bc-138">1つのプロジェクトがビルドされない場合は、そのプロジェクトが正常に発行される可能性があります。</span><span class="sxs-lookup"><span data-stu-id="7e4bc-138">You might successfully publish one project when another one doesn't even build.</span></span> <span data-ttu-id="7e4bc-139">詳細については、「stackoverflow スレッド[MSBuild が2つのパッケージで失敗](http://stackoverflow.com/questions/14226451/msbuild-fails-with-two-packages)する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="7e4bc-139">For more information, see the stackoverflow thread [MSBuild fails with two packages](http://stackoverflow.com/questions/14226451/msbuild-fails-with-two-packages).</span></span>

<span data-ttu-id="7e4bc-140">ソリューションではなく個々のプロジェクトを指定する場合は、Visual Studio のバージョンを指定するパラメーターを追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7e4bc-140">If you specify an individual project instead of a solution, you have to add a parameter that specifies the Visual Studio version.</span></span> <span data-ttu-id="7e4bc-141">Visual Studio 2012 を使用している場合、コマンドラインは次の例のようになります。</span><span class="sxs-lookup"><span data-stu-id="7e4bc-141">If you are using Visual Studio 2012 the command line would be similar to the following example:</span></span>

[!code-console[Main](command-line-deployment/samples/sample4.cmd?highlight=1)]

<span data-ttu-id="7e4bc-142">Visual Studio 2010 のバージョン番号は10.0 です。</span><span class="sxs-lookup"><span data-stu-id="7e4bc-142">The version number for Visual Studio 2010 is 10.0.</span></span> <span data-ttu-id="7e4bc-143">詳細については、作成者 Hashimi のブログの「 [Visual Studio プロジェクトの互換性と VisualStudioVersion](http://sedodream.com/2012/08/19/VisualStudioProjectCompatabilityAndVisualStudioVersion.aspx) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="7e4bc-143">For more information, see [Visual Studio project compatibility and VisualStudioVersion](http://sedodream.com/2012/08/19/VisualStudioProjectCompatabilityAndVisualStudioVersion.aspx) on Sayed Hashimi's blog.</span></span>

### <a name="specifying-the-publish-profile"></a><span data-ttu-id="7e4bc-144">発行プロファイルの指定</span><span class="sxs-lookup"><span data-stu-id="7e4bc-144">Specifying the publish profile</span></span>

<span data-ttu-id="7e4bc-145">発行プロファイルは、次の例に示すように、名前または*pubxml*ファイルへの完全パスを使用して指定できます。</span><span class="sxs-lookup"><span data-stu-id="7e4bc-145">You can specify the publish profile by name or by the full path to the *.pubxml* file, as shown in the following example:</span></span>

[!code-console[Main](command-line-deployment/samples/sample5.cmd?highlight=1)]

### <a name="web-publish-methods-supported-for-command-line-publishing"></a><span data-ttu-id="7e4bc-146">コマンドライン発行でサポートされている Web 発行方法</span><span class="sxs-lookup"><span data-stu-id="7e4bc-146">Web publish methods supported for command-line publishing</span></span>

<span data-ttu-id="7e4bc-147">コマンドライン発行では、次の3つの発行方法がサポートされています。</span><span class="sxs-lookup"><span data-stu-id="7e4bc-147">Three publish methods are supported for command line publishing:</span></span>

- <span data-ttu-id="7e4bc-148">`MSDeploy`-Web 配置を使用して発行します。</span><span class="sxs-lookup"><span data-stu-id="7e4bc-148">`MSDeploy` - Publish by using Web Deploy.</span></span>
- <span data-ttu-id="7e4bc-149">`Package`-Web 配置パッケージを作成して発行します。</span><span class="sxs-lookup"><span data-stu-id="7e4bc-149">`Package` - Publish by creating a Web Deploy Package.</span></span> <span data-ttu-id="7e4bc-150">パッケージを作成する MSBuild コマンドとは別にパッケージをインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="7e4bc-150">You have to install the package separately from the MSBuild command that creates it.</span></span>
- <span data-ttu-id="7e4bc-151">`FileSystem`-指定したフォルダーにファイルをコピーして発行します。</span><span class="sxs-lookup"><span data-stu-id="7e4bc-151">`FileSystem` - Publish by copying files to a specified folder.</span></span>

### <a name="specifying-the-build-configuration-and-platform"></a><span data-ttu-id="7e4bc-152">ビルド構成とプラットフォームの指定</span><span class="sxs-lookup"><span data-stu-id="7e4bc-152">Specifying the build configuration and platform</span></span>

<span data-ttu-id="7e4bc-153">ビルド構成とプラットフォームは、Visual Studio またはコマンドラインで設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7e4bc-153">The build configuration and platform must be set in Visual Studio or on the command line.</span></span> <span data-ttu-id="7e4bc-154">発行プロファイルには `LastUsedBuildConfiguration` と `LastUsedPlatform`という名前のプロパティが含まれますが、プロジェクトのビルド方法を決定するためにこれらのプロパティを設定することはできません。</span><span class="sxs-lookup"><span data-stu-id="7e4bc-154">The publish profiles include properties that are named `LastUsedBuildConfiguration` and `LastUsedPlatform`, but you can't set these properties in order to determine how the project is built.</span></span> <span data-ttu-id="7e4bc-155">詳細については、「MSBuild: 作成者 Hashimi のブログで[構成プロパティを設定する方法](http://sedodream.com/2012/10/27/MSBuildHowToSetTheConfigurationProperty.aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="7e4bc-155">For more information, see [MSBuild: how to set the configuration property](http://sedodream.com/2012/10/27/MSBuildHowToSetTheConfigurationProperty.aspx) on Sayed Hashimi's blog.</span></span>

## <a name="deploy-to-staging"></a><span data-ttu-id="7e4bc-156">ステージング環境へのデプロイ</span><span class="sxs-lookup"><span data-stu-id="7e4bc-156">Deploy to staging</span></span>

<span data-ttu-id="7e4bc-157">Azure にデプロイするには、コマンドラインにパスワードを追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7e4bc-157">To deploy to Azure, you must add the password to the command line.</span></span> <span data-ttu-id="7e4bc-158">Visual Studio の発行プロファイルにパスワードを保存した場合、パスワードは暗号化された形式で*pubxml. user*ファイルに格納されていました。</span><span class="sxs-lookup"><span data-stu-id="7e4bc-158">If you saved the password in the publish profile in Visual Studio, it was stored in encrypted form in the your *.pubxml.user* file.</span></span> <span data-ttu-id="7e4bc-159">このファイルは、コマンドラインの展開を行うときに MSBuild によってアクセスされることはないため、コマンドラインパラメーターでパスワードを渡す必要があります。</span><span class="sxs-lookup"><span data-stu-id="7e4bc-159">That file is not accessed by MSBuild when you do a command line deployment, so you have to pass in the password in a command line parameter.</span></span>

1. <span data-ttu-id="7e4bc-160">以前にステージング web サイト用にダウンロードした *.publishsettings*ファイルから必要なパスワードをコピーします。</span><span class="sxs-lookup"><span data-stu-id="7e4bc-160">Copy the password that you need from the *.publishsettings* file that you downloaded earlier for the staging web site.</span></span> <span data-ttu-id="7e4bc-161">パスワードは、Web 配置 `publishProfile` 要素の `userPWD` 属性の値です。</span><span class="sxs-lookup"><span data-stu-id="7e4bc-161">The password is the value of the `userPWD` attribute for the Web Deploy `publishProfile` element.</span></span>

    ![Web 配置パスワード](command-line-deployment/_static/image5.png)
2. <span data-ttu-id="7e4bc-163">Windows 8 のスタートページで、 **VS2012 の開発者コマンドプロンプト**を検索し、アイコンをクリックしてコマンドプロンプトを開きます。</span><span class="sxs-lookup"><span data-stu-id="7e4bc-163">In the Windows 8 Start page, search for **Developer Command Prompt for VS2012**, and click the icon to open the command prompt.</span></span> <span data-ttu-id="7e4bc-164">(ローカルコンピューター上の IIS には展開されないため、この時点で管理者として開く必要はありません)。</span><span class="sxs-lookup"><span data-stu-id="7e4bc-164">(You don't have to open it as administrator this time because you aren't deploying to IIS on the local computer.)</span></span>
3. <span data-ttu-id="7e4bc-165">コマンドプロンプトで次のコマンドを入力します。ソリューションファイルへのパスは、ソリューションファイルへのパスとパスワードで置き換えます。</span><span class="sxs-lookup"><span data-stu-id="7e4bc-165">Enter the following command at the command prompt, replacing the path to the solution file with the path to your solution file and the password with your password:</span></span>

    [!code-console[Main](command-line-deployment/samples/sample6.cmd)]

    <span data-ttu-id="7e4bc-166">このコマンドラインには、追加のパラメーターとして `/p:AllowUntrustedCertificate=true`が含まれていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="7e4bc-166">Notice that this command line includes an extra parameter: `/p:AllowUntrustedCertificate=true`.</span></span> <span data-ttu-id="7e4bc-167">このチュートリアルの執筆中は、コマンドラインから Azure に発行するときに、`AllowUntrustedCertificate` のプロパティを設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7e4bc-167">As this tutorial is being written, the `AllowUntrustedCertificate` property must be set when you publish to Azure from the command line.</span></span> <span data-ttu-id="7e4bc-168">このバグの修正がリリースされた場合、そのパラメーターは必要ありません。</span><span class="sxs-lookup"><span data-stu-id="7e4bc-168">When the fix for this bug is released, you won't need that parameter.</span></span>
4. <span data-ttu-id="7e4bc-169">ブラウザーを開き、ステージングサイトの URL にアクセスし、 **[バージョン情報]** ページをクリックして、デプロイが成功したことを確認します。</span><span class="sxs-lookup"><span data-stu-id="7e4bc-169">Open a browser and go to the URL of your staging site, and then click the **About** page to verify that the deployment was successful.</span></span>

    <span data-ttu-id="7e4bc-170">テスト環境で既に説明したように、 **[バージョン情報]** ページで統計を表示するには、いくつかの学生を作成する必要がある場合があります。</span><span class="sxs-lookup"><span data-stu-id="7e4bc-170">As you saw earlier for the test environment, you might have to create some students to see statistics on the **About** page.</span></span>

## <a name="deploy-to-production"></a><span data-ttu-id="7e4bc-171">運用環境へのデプロイ</span><span class="sxs-lookup"><span data-stu-id="7e4bc-171">Deploy to production</span></span>

<span data-ttu-id="7e4bc-172">運用環境にデプロイするプロセスは、ステージングのプロセスに似ています。</span><span class="sxs-lookup"><span data-stu-id="7e4bc-172">The process for deploying to production is similar to the process for staging.</span></span>

1. <span data-ttu-id="7e4bc-173">前の手順でダウンロードした *.publishsettings*ファイルから必要なパスワードをコピーします。</span><span class="sxs-lookup"><span data-stu-id="7e4bc-173">Copy the password that you need from the *.publishsettings* file that you downloaded earlier for the production web site.</span></span>
2. <span data-ttu-id="7e4bc-174">**VS2012 の開発者コマンドプロンプトを**開きます。</span><span class="sxs-lookup"><span data-stu-id="7e4bc-174">Open **Developer Command Prompt for VS2012**.</span></span>
3. <span data-ttu-id="7e4bc-175">コマンドプロンプトで次のコマンドを入力します。ソリューションファイルへのパスは、ソリューションファイルへのパスとパスワードで置き換えます。</span><span class="sxs-lookup"><span data-stu-id="7e4bc-175">Enter the following command at the command prompt, replacing the path to the solution file with the path to your solution file and the password with your password:</span></span>

    [!code-console[Main](command-line-deployment/samples/sample7.cmd)]

    <span data-ttu-id="7e4bc-176">実際の運用サイトでも、データベースの変更があった場合は、通常、展開の前に*アプリ\_offline .htm*ファイルをサイトにコピーし、展開が正常に完了した後に削除します。</span><span class="sxs-lookup"><span data-stu-id="7e4bc-176">For a real production site, if there was also a database change, you would typically copy the *app\_offline.htm* file to the site before deployment and delete it after successful deployment.</span></span>
4. <span data-ttu-id="7e4bc-177">ブラウザーを開き、ステージングサイトの URL にアクセスし、 **[バージョン情報]** ページをクリックして、デプロイが成功したことを確認します。</span><span class="sxs-lookup"><span data-stu-id="7e4bc-177">Open a browser and go to the URL of your staging site, and then click the **About** page to verify that the deployment was successful.</span></span>

## <a name="summary"></a><span data-ttu-id="7e4bc-178">要約</span><span class="sxs-lookup"><span data-stu-id="7e4bc-178">Summary</span></span>

<span data-ttu-id="7e4bc-179">これで、コマンドラインを使用してアプリケーションの更新プログラムが展開されました。</span><span class="sxs-lookup"><span data-stu-id="7e4bc-179">You have now deployed an application update by using the command line.</span></span>

![テスト環境のページについて](command-line-deployment/_static/image6.png)

<span data-ttu-id="7e4bc-181">次のチュートリアルでは、web 発行パイプラインを拡張する方法の例を紹介します。</span><span class="sxs-lookup"><span data-stu-id="7e4bc-181">In the next tutorial, you will see an example of how to extend the web publish pipeline.</span></span> <span data-ttu-id="7e4bc-182">この例では、プロジェクトに含まれていないファイルを配置する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="7e4bc-182">The example will show you how to deploy files that are not included in the project.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="7e4bc-183">[前へ](deploying-a-database-update.md)
> [次へ](deploying-extra-files.md)</span><span class="sxs-lookup"><span data-stu-id="7e4bc-183">[Previous](deploying-a-database-update.md)
[Next](deploying-extra-files.md)</span></span>
