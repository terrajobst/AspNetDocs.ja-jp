---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12
title: 'Visual Studio または Visual Web Developer を使用して SQL Server Compact で ASP.NET Web アプリケーションをデプロイする: データベースの更新をデプロイする-9/12 |Microsoft Docs'
author: tdykstra
description: この一連のチュートリアルでは、Visual Stu... を使用して SQL Server Compact データベースを含む ASP.NET web アプリケーションプロジェクトをデプロイ (発行) する方法について説明します。
ms.author: riande
ms.date: 11/17/2011
ms.assetid: a8d776af-4735-4612-87f6-9f326587f2d3
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12
msc.type: authoredcontent
ms.openlocfilehash: 3385e1019d9e7a9263fd9513c39b25eb85febbb5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78455104"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-a-database-update---9-of-12"></a><span data-ttu-id="aa4ba-103">Visual Studio または Visual Web Developer を使用した SQL Server Compact を使用した ASP.NET Web アプリケーションのデプロイ: データベース更新プログラムのデプロイ-9/12</span><span class="sxs-lookup"><span data-stu-id="aa4ba-103">Deploying an ASP.NET Web Application with SQL Server Compact using Visual Studio or Visual Web Developer: Deploying a Database Update - 9 of 12</span></span>

<span data-ttu-id="aa4ba-104">[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="aa4ba-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="aa4ba-105">スタートプロジェクトのダウンロード</span><span class="sxs-lookup"><span data-stu-id="aa4ba-105">Download Starter Project</span></span>](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> <span data-ttu-id="aa4ba-106">この一連のチュートリアルでは、Visual Studio 2012 RC または Visual Studio Express 2012 RC for Web を使用して SQL Server Compact データベースを含む ASP.NET web アプリケーションプロジェクトをデプロイ (発行) する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="aa4ba-106">This series of tutorials shows you how to deploy (publish) an ASP.NET web application project that includes a SQL Server Compact database by using Visual Studio 2012 RC or Visual Studio Express 2012 RC for Web.</span></span> <span data-ttu-id="aa4ba-107">Web 発行の更新をインストールする場合は、Visual Studio 2010 を使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="aa4ba-107">You can also use Visual Studio 2010 if you install the Web Publish Update.</span></span> <span data-ttu-id="aa4ba-108">シリーズの概要については、[シリーズの最初のチュートリアル](deployment-to-a-hosting-provider-introduction-1-of-12.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="aa4ba-108">For an introduction to the series, see [the first tutorial in the series](deployment-to-a-hosting-provider-introduction-1-of-12.md).</span></span>
> 
> <span data-ttu-id="aa4ba-109">Visual Studio 2012 の RC リリース後に導入された配置機能を示すチュートリアルについては、SQL Server Compact 以外の SQL Server のエディションをデプロイする方法、Azure App Service Web Apps にデプロイする方法については、「 [ASP.NET Web deployment Using Visual studio (Visual studio を使用した Web デプロイ](../../deployment/visual-studio-web-deployment/introduction.md)のデプロイ)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="aa4ba-109">For a tutorial that shows deployment features introduced after the RC release of Visual Studio 2012, shows how to deploy SQL Server editions other than SQL Server Compact, and shows how to deploy to Azure App Service Web Apps, see [ASP.NET Web Deployment using Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md).</span></span>

## <a name="overview"></a><span data-ttu-id="aa4ba-110">概要</span><span class="sxs-lookup"><span data-stu-id="aa4ba-110">Overview</span></span>

<span data-ttu-id="aa4ba-111">このチュートリアルでは、データベースの変更と関連するコードの変更を行い、Visual Studio で変更をテストして、テスト環境と運用環境の両方に更新プログラムを配置します。</span><span class="sxs-lookup"><span data-stu-id="aa4ba-111">In this tutorial, you make a database change and related code changes, test the changes in Visual Studio, then deploy the update to both the test and production environments.</span></span>

<span data-ttu-id="aa4ba-112">リマインダー: チュートリアルを実行しているときにエラーメッセージが表示されたり機能しない場合は、必ず[トラブルシューティングのページ](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)を確認してください。</span><span class="sxs-lookup"><span data-stu-id="aa4ba-112">Reminder: If you get an error message or something doesn't work as you go through the tutorial, be sure to check the [troubleshooting page](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md).</span></span>

## <a name="adding-a-new-column-to-a-table"></a><span data-ttu-id="aa4ba-113">テーブルへの新しい列の追加</span><span class="sxs-lookup"><span data-stu-id="aa4ba-113">Adding a New Column to a Table</span></span>

<span data-ttu-id="aa4ba-114">このセクションでは、`Student` エンティティと `Instructor` エンティティの `Person` 基本クラスに生年月日列を追加します。</span><span class="sxs-lookup"><span data-stu-id="aa4ba-114">In this section, you add a birth date column to the `Person` base class for the `Student` and `Instructor` entities.</span></span> <span data-ttu-id="aa4ba-115">次に、インストラクターのデータを表示するページを更新して、新しい列が表示されるようにします。</span><span class="sxs-lookup"><span data-stu-id="aa4ba-115">Then you update the page that displays instructor data so that it displays the new column.</span></span>

<span data-ttu-id="aa4ba-116">*ContosoUniversity*プロジェクトで、 *Person.cs*を開き、次のプロパティを `Person` クラスの末尾に追加します (この後に2つの右中かっこが必要です)。</span><span class="sxs-lookup"><span data-stu-id="aa4ba-116">In the *ContosoUniversity.DAL* project, open *Person.cs* and add the following property at the end of the `Person` class (there should be two closing curly braces following it):</span></span>

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample1.cs)]

<span data-ttu-id="aa4ba-117">次に、新しい列の値を提供するように、Seed メソッドを更新します。</span><span class="sxs-lookup"><span data-stu-id="aa4ba-117">Next, update the Seed method so that it provides a value for the new column.</span></span> <span data-ttu-id="aa4ba-118">*Migrations\ configuration.cs*を開き、`var instructors = new List<Instructor>` 開始するコードブロックを、生年月日の情報を含む次のコードブロックに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="aa4ba-118">Open *Migrations\Configuration.cs* and replace the code block that begins `var instructors = new List<Instructor>` with the following code block which includes birth date information:</span></span>

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample2.cs)]

<span data-ttu-id="aa4ba-119">ContosoUniversity プロジェクトで、*講師*を開き、生年月日を表示する新しいテンプレートフィールドを追加します。</span><span class="sxs-lookup"><span data-stu-id="aa4ba-119">In the ContosoUniversity project, open *Instructors.aspx* and add a new template field to display the birth date.</span></span> <span data-ttu-id="aa4ba-120">入社年月日と office assignment の間に追加します。</span><span class="sxs-lookup"><span data-stu-id="aa4ba-120">Add it between the ones for hire date and office assignment:</span></span>

[!code-aspx[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample3.aspx)]

<span data-ttu-id="aa4ba-121">(コードのインデントが同期されない場合は、CTRL + K キーを押してから CTRL + D キーを押してファイルを自動的に再フォーマットできます)。</span><span class="sxs-lookup"><span data-stu-id="aa4ba-121">(If code indentation gets out of sync, you can press CTRL-K and then CTRL-D to automatically reformat the file.)</span></span>

<span data-ttu-id="aa4ba-122">ソリューションをビルドし、 **[パッケージマネージャーコンソール]** ウィンドウを開きます。</span><span class="sxs-lookup"><span data-stu-id="aa4ba-122">Build the solution, and then open the **Package Manager Console** window.</span></span> <span data-ttu-id="aa4ba-123">ContosoUniversity が**既定のプロジェクト**として選択されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="aa4ba-123">Make sure that ContosoUniversity.DAL is still selected as the **Default project**.</span></span>

<span data-ttu-id="aa4ba-124">**パッケージマネージャーコンソール**ウィンドウで、**既定のプロジェクト**として **[ContosoUniversity]** を選択し、次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="aa4ba-124">In the **Package Manager Console** window, select **ContosoUniversity.DAL** as the **Default project**, and then enter the following command:</span></span>

[!code-powershell[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample4.ps1)]

<span data-ttu-id="aa4ba-125">このコマンドが終了すると、Visual Studio によって新しい `DbMigration` クラスを定義するクラスファイルが開き、`Up` メソッドに新しい列を作成するコードが表示されます。</span><span class="sxs-lookup"><span data-stu-id="aa4ba-125">When this command finishes, Visual Studio opens the class file that defines the new `DbMigration` class, and in the `Up` method you can see the code that creates the new column.</span></span>

![AddBirthDate_migration_code](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image1.png)

<span data-ttu-id="aa4ba-127">ソリューションをビルドし、 **[パッケージマネージャーコンソール]** ウィンドウで次のコマンドを入力します (ContosoUniversity プロジェクトが選択されていることを確認します)。</span><span class="sxs-lookup"><span data-stu-id="aa4ba-127">Build the solution, and then enter the following command in the **Package Manager Console** window (make sure the ContosoUniversity.DAL project is still selected):</span></span>

[!code-powershell[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample5.ps1)]

<span data-ttu-id="aa4ba-128">コマンドが完了したら、アプリケーションを実行し、[インストラクター] ページを選択します。</span><span class="sxs-lookup"><span data-stu-id="aa4ba-128">When the command finishes, run the application and select the Instructors page.</span></span> <span data-ttu-id="aa4ba-129">ページが読み込まれると、[新しい生年月日] フィールドが表示されます。</span><span class="sxs-lookup"><span data-stu-id="aa4ba-129">When the page loads, you see that it has the new birth date field.</span></span>

<span data-ttu-id="aa4ba-130">[![Instructors_page_with_birth_date](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image3.png)](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image2.png)</span><span class="sxs-lookup"><span data-stu-id="aa4ba-130">[![Instructors_page_with_birth_date](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image3.png)](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image2.png)</span></span>

## <a name="deploying-the-database-update-to-the-test-environment"></a><span data-ttu-id="aa4ba-131">テスト環境へのデータベースの更新の配置</span><span class="sxs-lookup"><span data-stu-id="aa4ba-131">Deploying the Database Update to the Test Environment</span></span>

<span data-ttu-id="aa4ba-132">**ソリューションエクスプローラー** ContosoUniversity プロジェクトを選択します。</span><span class="sxs-lookup"><span data-stu-id="aa4ba-132">In **Solution Explorer** select the ContosoUniversity project.</span></span>

<span data-ttu-id="aa4ba-133">Web 上の **[発行**] ツールバーで、**テスト**発行プロファイルを選択し、 **[web の発行]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="aa4ba-133">In the **Web One Click Publish** toolbar, select the **Test** publish profile, and then click **Publish Web**.</span></span> <span data-ttu-id="aa4ba-134">(ツールバーが無効になっている場合は**ソリューションエクスプローラー**で ContosoUniversity プロジェクトを選択します)。</span><span class="sxs-lookup"><span data-stu-id="aa4ba-134">(If the toolbar is disabled, select the ContosoUniversity project in **Solution Explorer**.)</span></span>

<span data-ttu-id="aa4ba-135">更新されたアプリケーションが Visual Studio によってデプロイされ、ブラウザーがホームページに表示されます。</span><span class="sxs-lookup"><span data-stu-id="aa4ba-135">Visual Studio deploys the updated application, and the browser opens to the home page.</span></span> <span data-ttu-id="aa4ba-136">インストラクターページを実行して、更新プログラムが正常に展開されたことを確認します。</span><span class="sxs-lookup"><span data-stu-id="aa4ba-136">Run the Instructors page to verify that the update was successfully deployed.</span></span> <span data-ttu-id="aa4ba-137">アプリケーションがこのページのデータベースにアクセスしようとすると、Code First データベーススキーマが更新され、`Seed` メソッドが実行されます。</span><span class="sxs-lookup"><span data-stu-id="aa4ba-137">When the application tries to access the database for this page, Code First updates the database schema and runs the `Seed` method.</span></span> <span data-ttu-id="aa4ba-138">ページが表示されると、[予想される**誕生日**] 列に日付が含まれていることがわかります。</span><span class="sxs-lookup"><span data-stu-id="aa4ba-138">When the page displays, you see the expected **Birth Date** column with dates in it.</span></span>

<span data-ttu-id="aa4ba-139">[![Instructors_page_with_birth_date_Test](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image5.png)](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="aa4ba-139">[![Instructors_page_with_birth_date_Test](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image5.png)](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image4.png)</span></span>

## <a name="deploying-the-database-update-to-the-production-environment"></a><span data-ttu-id="aa4ba-140">運用環境へのデータベースの更新の配置</span><span class="sxs-lookup"><span data-stu-id="aa4ba-140">Deploying the Database Update to the Production Environment</span></span>

<span data-ttu-id="aa4ba-141">これで、運用環境にデプロイできるようになりました。</span><span class="sxs-lookup"><span data-stu-id="aa4ba-141">You can now deploy to production.</span></span> <span data-ttu-id="aa4ba-142">唯一の違いは、 *app\_offline .htm*を使用して、ユーザーがサイトにアクセスできないようにし、変更を展開するときにデータベースを更新することです。</span><span class="sxs-lookup"><span data-stu-id="aa4ba-142">The only difference is that you'll use *app\_offline.htm* to prevent users from accessing the site and thus updating the database while you're deploying changes.</span></span> <span data-ttu-id="aa4ba-143">運用環境のデプロイでは、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="aa4ba-143">For production deployment perform the following steps:</span></span>

- <span data-ttu-id="aa4ba-144">*アプリ\_オフライン .htm*ファイルを実稼働サイトにアップロードします。</span><span class="sxs-lookup"><span data-stu-id="aa4ba-144">Upload the *app\_offline.htm* file to the production site.</span></span>
- <span data-ttu-id="aa4ba-145">Visual Studio で、 **Web サイトの 発行** ツールバーの 発行 をクリックし、 **web の発行** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="aa4ba-145">In Visual Studio, choose the Production profile in the **Web One Click Publish** toolbar and click **Publish Web**.</span></span>
- <span data-ttu-id="aa4ba-146">運用サイトから、*アプリ\_のオフライン .htm*ファイルを削除します。</span><span class="sxs-lookup"><span data-stu-id="aa4ba-146">Delete the *app\_offline.htm* file from the production site.</span></span>

> [!NOTE]
> <span data-ttu-id="aa4ba-147">アプリケーションが運用環境で使用されている間は、バックアップ計画を実装する必要があります。</span><span class="sxs-lookup"><span data-stu-id="aa4ba-147">While your application is in use in the production environment you should be implementing a backup plan.</span></span> <span data-ttu-id="aa4ba-148">つまり、 *School-Prod*ファイルと*aspnet-Prod*ファイルを運用サイトから安全なストレージの場所に定期的にコピーする必要があり、そのようなバックアップをいくつか作成しておく必要があります。</span><span class="sxs-lookup"><span data-stu-id="aa4ba-148">That is, you should be periodically copying the *School-Prod.sdf* and *aspnet-Prod.sdf* files from the production site to a secure storage location, and you should be keeping several generations of such backups.</span></span> <span data-ttu-id="aa4ba-149">データベースを更新するときは、変更の直前にからバックアップコピーを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="aa4ba-149">When you update the database, you should make a backup copy from immediately before the change.</span></span> <span data-ttu-id="aa4ba-150">これにより、間違いを犯しても、運用環境にデプロイするまで検出されない場合でも、データベースを破損する前の状態に復旧できます。</span><span class="sxs-lookup"><span data-stu-id="aa4ba-150">Then, if you make a mistake and don't discover it until after you have deployed it to production, you will still be able to recover the database to the state it was in before it became corrupted.</span></span>

<span data-ttu-id="aa4ba-151">ブラウザーでホームページの URL を開くと、*アプリ\_offline*ページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="aa4ba-151">When Visual Studio opens the home page URL in the browser, the *app\_offline.htm* page is displayed.</span></span> <span data-ttu-id="aa4ba-152">*アプリ\_のオフライン .htm*ファイルを削除した後、もう一度ホームページを参照して、更新が正常に展開されたことを確認できます。</span><span class="sxs-lookup"><span data-stu-id="aa4ba-152">After you delete the *app\_offline.htm* file, you can browse to your home page again to verify that the update was successfully deployed.</span></span>

<span data-ttu-id="aa4ba-153">[![Instructors_page_with_birth_date_Prod](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image7.png)](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="aa4ba-153">[![Instructors_page_with_birth_date_Prod](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image7.png)](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image6.png)</span></span>

<span data-ttu-id="aa4ba-154">これで、テストと運用の両方にデータベースの変更を含むアプリケーションの更新が展開されました。</span><span class="sxs-lookup"><span data-stu-id="aa4ba-154">You've now deployed an application update that included a database change to both test and production.</span></span> <span data-ttu-id="aa4ba-155">次のチュートリアルでは、SQL Server Compact から SQL Server Express と SQL Server にデータベースを移行する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="aa4ba-155">The next tutorial shows you how to migrate your database from SQL Server Compact to SQL Server Express and SQL Server.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="aa4ba-156">[前へ](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12.md)
> [次へ](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12.md)</span><span class="sxs-lookup"><span data-stu-id="aa4ba-156">[Previous](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12.md)
[Next](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12.md)</span></span>
