---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-database-update
title: 'Visual Studio を使用した ASP.NET Web 配置: データベース更新の配置 |Microsoft Docs'
author: tdykstra
description: このチュートリアルシリーズでは、ASP.NET web アプリケーションをデプロイ (発行) して、Web Apps またはサードパーティのホスティングプロバイダーに Azure App Service する方法について説明します。
ms.author: riande
ms.date: 02/15/2013
ms.assetid: 9cad0833-486a-4474-a7f3-7715542ec4ce
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-database-update
msc.type: authoredcontent
ms.openlocfilehash: 805eb84c24764cf921291f89054435601dbac48e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78440788"
---
# <a name="aspnet-web-deployment-using-visual-studio-deploying-a-database-update"></a><span data-ttu-id="7bbc0-103">Visual Studio を使用した ASP.NET Web 配置: データベース更新プログラムの配置</span><span class="sxs-lookup"><span data-stu-id="7bbc0-103">ASP.NET Web Deployment using Visual Studio: Deploying a Database Update</span></span>

<span data-ttu-id="7bbc0-104">[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="7bbc0-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="7bbc0-105">スタートプロジェクトのダウンロード</span><span class="sxs-lookup"><span data-stu-id="7bbc0-105">Download Starter Project</span></span>](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> <span data-ttu-id="7bbc0-106">このチュートリアルシリーズでは、Visual Studio 2012 または Visual Studio 2010 を使用して、Azure App Service Web Apps またはサードパーティのホスティングプロバイダーにするために、ASP.NET web アプリケーションをデプロイ (発行) する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-106">This tutorial series shows you how to deploy (publish) an ASP.NET web application to Azure App Service Web Apps or to a third-party hosting provider, by using Visual Studio 2012 or Visual Studio 2010.</span></span> <span data-ttu-id="7bbc0-107">シリーズの詳細については、[シリーズの最初のチュートリアル](introduction.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-107">For information about the series, see [the first tutorial in the series](introduction.md).</span></span>

## <a name="overview"></a><span data-ttu-id="7bbc0-108">概要</span><span class="sxs-lookup"><span data-stu-id="7bbc0-108">Overview</span></span>

<span data-ttu-id="7bbc0-109">このチュートリアルでは、データベースの変更と関連するコードの変更を行い、Visual Studio で変更をテストしてから、テスト環境、ステージング環境、および運用環境に更新プログラムを配置します。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-109">In this tutorial, you make a database change and related code changes, test the changes in Visual Studio, then deploy the update to the test, staging, and production environments.</span></span>

<span data-ttu-id="7bbc0-110">このチュートリアルでは、まず Code First Migrations によって管理されるデータベースを更新する方法を示します。その後、dbDacFx プロバイダーを使用してデータベースを更新する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-110">The tutorial first shows how to update a database that is managed by Code First Migrations, and then later it shows how to update a database by using the dbDacFx provider.</span></span>

<span data-ttu-id="7bbc0-111">リマインダー: チュートリアルを実行しているときにエラーメッセージが表示されたり機能しない場合は、必ず[トラブルシューティングのページ](troubleshooting.md)を確認してください。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-111">Reminder: If you get an error message or something doesn't work as you go through the tutorial, be sure to check the [troubleshooting page](troubleshooting.md).</span></span>

## <a name="deploy-a-database-update-by-using-code-first-migrations"></a><span data-ttu-id="7bbc0-112">Code First Migrations を使用してデータベースの更新を配置する</span><span class="sxs-lookup"><span data-stu-id="7bbc0-112">Deploy a database update by using Code First Migrations</span></span>

<span data-ttu-id="7bbc0-113">このセクションでは、`Student` エンティティと `Instructor` エンティティの `Person` 基本クラスに生年月日列を追加します。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-113">In this section, you add a birth date column to the `Person` base class for the `Student` and `Instructor` entities.</span></span> <span data-ttu-id="7bbc0-114">次に、インストラクターのデータを表示するページを更新して、新しい列が表示されるようにします。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-114">Then you update the page that displays instructor data so that it displays the new column.</span></span> <span data-ttu-id="7bbc0-115">最後に、変更をテスト、ステージング、および運用にデプロイします。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-115">Finally, you deploy the changes to test, staging, and production.</span></span>

### <a name="add-a-column-to-a-table-in-the-application-database"></a><span data-ttu-id="7bbc0-116">アプリケーションデータベースのテーブルに列を追加する</span><span class="sxs-lookup"><span data-stu-id="7bbc0-116">Add a column to a table in the application database</span></span>

1. <span data-ttu-id="7bbc0-117">*ContosoUniversity*プロジェクトで、 *Person.cs*を開き、次のプロパティを `Person` クラスの末尾に追加します (この後に2つの右中かっこが必要です)。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-117">In the *ContosoUniversity.DAL* project, open *Person.cs* and add the following property at the end of the `Person` class (there should be two closing curly braces following it):</span></span>

    [!code-csharp[Main](deploying-a-database-update/samples/sample1.cs)]

    <span data-ttu-id="7bbc0-118">次に、新しい列の値を提供するように `Seed` メソッドを更新します。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-118">Next, update the `Seed` method so that it provides a value for the new column.</span></span> <span data-ttu-id="7bbc0-119">*Migrations\ configuration.cs*を開き、`var instructors = new List<Instructor>` 開始するコードブロックを、生年月日の情報を含む次のコードブロックに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-119">Open *Migrations\Configuration.cs* and replace the code block that begins `var instructors = new List<Instructor>` with the following code block which includes birth date information:</span></span>

    [!code-csharp[Main](deploying-a-database-update/samples/sample2.cs)]
2. <span data-ttu-id="7bbc0-120">ソリューションをビルドし、 **[パッケージマネージャーコンソール]** ウィンドウを開きます。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-120">Build the solution, and then open the **Package Manager Console** window.</span></span> <span data-ttu-id="7bbc0-121">ContosoUniversity が**既定のプロジェクト**として選択されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-121">Make sure that ContosoUniversity.DAL is still selected as the **Default project**.</span></span>
3. <span data-ttu-id="7bbc0-122">**パッケージマネージャーコンソール**ウィンドウで、**既定のプロジェクト**として **[ContosoUniversity]** を選択し、次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-122">In the **Package Manager Console** window, select **ContosoUniversity.DAL** as the **Default project**, and then enter the following command:</span></span>

    [!code-powershell[Main](deploying-a-database-update/samples/sample3.ps1)]

    <span data-ttu-id="7bbc0-123">このコマンドが終了すると、Visual Studio によって新しい `DbMigration` クラスを定義するクラスファイルが開き、`Up` メソッドに新しい列を作成するコードが表示されます。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-123">When this command finishes, Visual Studio opens the class file that defines the new `DbMigration` class, and in the `Up` method you can see the code that creates the new column.</span></span> <span data-ttu-id="7bbc0-124">`Up` メソッドは、変更を実装するときに列を作成し、変更をロールバックするときに、`Down` メソッドが列を削除します。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-124">The `Up` method creates the column when you are implementing the change, and the `Down` method deletes the column when you are rolling back the change.</span></span>

    ![AddBirthDate_migration_code](deploying-a-database-update/_static/image1.png)
4. <span data-ttu-id="7bbc0-126">ソリューションをビルドし、 **[パッケージマネージャーコンソール]** ウィンドウで次のコマンドを入力します (ContosoUniversity プロジェクトが選択されていることを確認します)。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-126">Build the solution, and then enter the following command in the **Package Manager Console** window (make sure the ContosoUniversity.DAL project is still selected):</span></span>

    [!code-powershell[Main](deploying-a-database-update/samples/sample4.ps1)]

    <span data-ttu-id="7bbc0-127">Entity Framework は、`Up` メソッドを実行し、`Seed` メソッドを実行します。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-127">The Entity Framework runs the `Up` method and then runs the `Seed` method.</span></span>

### <a name="display-the-new-column-in-the-instructors-page"></a><span data-ttu-id="7bbc0-128">[インストラクター] ページに新しい列を表示します。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-128">Display the new column in the Instructors page</span></span>

1. <span data-ttu-id="7bbc0-129">ContosoUniversity プロジェクトで、*講師*を開き、生年月日を表示する新しいテンプレートフィールドを追加します。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-129">In the ContosoUniversity project, open *Instructors.aspx* and add a new template field to display the birth date.</span></span> <span data-ttu-id="7bbc0-130">入社年月日と office assignment の間に追加します。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-130">Add it between the ones for hire date and office assignment:</span></span>

    [!code-aspx[Main](deploying-a-database-update/samples/sample5.aspx?highlight=9-17)]

    <span data-ttu-id="7bbc0-131">(コードのインデントが同期されない場合は、CTRL + K キーを押してから CTRL + D キーを押してファイルを自動的に再フォーマットできます)。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-131">(If code indentation gets out of sync, you can press CTRL-K and then CTRL-D to automatically reformat the file.)</span></span>
2. <span data-ttu-id="7bbc0-132">アプリケーションを実行し、 **[インストラクター]** リンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-132">Run the application and click the **Instructors** link.</span></span>

    <span data-ttu-id="7bbc0-133">ページが読み込まれると、[新しい生年月日] フィールドが表示されます。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-133">When the page loads, you see that it has the new birth date field.</span></span>

    ![誕生日付きのインストラクターページ](deploying-a-database-update/_static/image2.png)
3. <span data-ttu-id="7bbc0-135">ブラウザーを閉じます。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-135">Close the browser.</span></span>

### <a name="deploy-the-database-update"></a><span data-ttu-id="7bbc0-136">データベースの更新を展開する</span><span class="sxs-lookup"><span data-stu-id="7bbc0-136">Deploy the database update</span></span>

1. <span data-ttu-id="7bbc0-137">**ソリューションエクスプローラー** ContosoUniversity プロジェクトを選択します。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-137">In **Solution Explorer** select the ContosoUniversity project.</span></span>
2. <span data-ttu-id="7bbc0-138">Web 上の **[発行**] ツールバーで、**テスト**発行プロファイルをクリックし、 **[web の発行]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-138">In the **Web One Click Publish** toolbar, click the **Test** publish profile, and then click **Publish Web**.</span></span> <span data-ttu-id="7bbc0-139">(ツールバーが無効になっている場合は**ソリューションエクスプローラー**で ContosoUniversity プロジェクトを選択します)。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-139">(If the toolbar is disabled, select the ContosoUniversity project in **Solution Explorer**.)</span></span>

    <span data-ttu-id="7bbc0-140">更新されたアプリケーションが Visual Studio によってデプロイされ、ブラウザーがホームページに表示されます。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-140">Visual Studio deploys the updated application, and the browser opens to the home page.</span></span>
3. <span data-ttu-id="7bbc0-141">**インストラクター**ページを実行して、更新プログラムが正常に展開されたことを確認します。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-141">Run the **Instructors** page to verify that the update was successfully deployed.</span></span>

    <span data-ttu-id="7bbc0-142">アプリケーションがこのページのデータベースにアクセスしようとすると、Code First データベーススキーマが更新され、`Seed` メソッドが実行されます。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-142">When the application tries to access the database for this page, Code First updates the database schema and runs the `Seed` method.</span></span> <span data-ttu-id="7bbc0-143">ページが表示されると、[予想される**誕生日**] 列に日付が含まれていることがわかります。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-143">When the page displays, you see the expected **Birth Date** column with dates in it.</span></span>
4. <span data-ttu-id="7bbc0-144">Web 上の **[発行**] ツールバーで、 **[ステージング]** 発行プロファイル をクリックし、 **[web の発行]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-144">In the **Web One Click Publish** toolbar, click the **Staging** publish profile, and then click **Publish Web**.</span></span>
5. <span data-ttu-id="7bbc0-145">ステージングの**インストラクター**ページを実行して、更新が正常に展開されたことを確認します。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-145">Run the **Instructors** page in staging to verify that the update was successfully deployed.</span></span>
6. <span data-ttu-id="7bbc0-146">Web 上の **[発行**] ツールバーで、 **[実稼働]** 発行プロファイル をクリックし、 **[web の発行]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-146">In the **Web One Click Publish** toolbar, click the **Production** publish profile, and then click **Publish Web**.</span></span>
7. <span data-ttu-id="7bbc0-147">運用環境で**インストラクター**ページを実行し、更新が正常に展開されたことを確認します。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-147">Run the **Instructors** page in production to verify that the update was successfully deployed.</span></span>

    <span data-ttu-id="7bbc0-148">データベースの変更を含む実際の運用アプリケーションの更新については、前のチュートリアルで見たように、*アプリ\_offline .htm*を使用してデプロイ中にアプリケーションをオフラインにすることも通常します。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-148">For a real production application update that includes a database change you would also typically take the application offline during deployment by using *app\_offline.htm*, as you saw in the previous tutorial.</span></span>

## <a name="deploy-a-database-update-by-using-the-dbdacfx-provider"></a><span data-ttu-id="7bbc0-149">DbDacFx プロバイダーを使用してデータベースの更新を配置する</span><span class="sxs-lookup"><span data-stu-id="7bbc0-149">Deploy a database update by using the dbDacFx provider</span></span>

<span data-ttu-id="7bbc0-150">このセクションでは、メンバーシップデータベースの*ユーザー*テーブルに*コメント*列を追加し、各ユーザーのコメントを表示および編集できるページを作成します。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-150">In this section, you add a *Comments* column to the *User* table in the membership database and create a page that lets you display and edit comments for each user.</span></span> <span data-ttu-id="7bbc0-151">次に、変更をテスト、ステージング、および運用にデプロイします。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-151">Then you deploy the changes to test, staging, and production.</span></span>

### <a name="add-a-column-to-a-table-in-the-membership-database"></a><span data-ttu-id="7bbc0-152">メンバーシップデータベースのテーブルに列を追加する</span><span class="sxs-lookup"><span data-stu-id="7bbc0-152">Add a column to a table in the membership database</span></span>

1. <span data-ttu-id="7bbc0-153">Visual Studio で**SQL Server オブジェクトエクスプローラー**を開きます。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-153">In Visual Studio, open **SQL Server Object Explorer**.</span></span>
2. <span data-ttu-id="7bbc0-154">**(Localdb)、v11.0**、 **[データベース]** 、[ **aspnet-ContosoUniversity** ( **aspnet-ContosoUniversity**)] の順に展開し、 **[テーブル]** を展開します。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-154">Expand **(localdb)\v11.0**, expand **Databases**, expand **aspnet-ContosoUniversity** (not **aspnet-ContosoUniversity-Prod**) and then expand **Tables**.</span></span>

    <span data-ttu-id="7bbc0-155">**[SQL Server]** ノードの下に **(localdb) \ v11.0**が表示されない場合は、 **[SQL Server]** ノードを右クリックし、 **[SQL Server の追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-155">If you don't see **(localdb)\v11.0** under the **SQL Server** node, right-click the **SQL Server** node and click **Add SQL Server**.</span></span> <span data-ttu-id="7bbc0-156">**[サーバーへの接続]** ダイアログボックスで、**サーバー名**として *「(localdb) \ v11.0* 」と入力し、 **[接続]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-156">In the **Connect to Server** dialog box enter *(localdb)\v11.0* as the **Server name**, and then click **Connect**.</span></span>

    <span data-ttu-id="7bbc0-157">**ContosoUniversity**が表示されない場合は、プロジェクトを実行し、*管理者*の資格情報 (パスワードは*devpwd*) を使用してログインしてから、 **[SQL Server オブジェクトエクスプローラー]** ウィンドウを更新します。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-157">If you don't see **aspnet-ContosoUniversity**, run the project and log in using the *admin* credentials (password is *devpwd*), and then refresh the **SQL Server Object Explorer** window.</span></span>
3. <span data-ttu-id="7bbc0-158">**Users**テーブルを右クリックし、[デザイナーの**表示**] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-158">Right-click the **Users** table, and then click **View Designer**.</span></span>

    ![SSOX ビューデザイナー](deploying-a-database-update/_static/image3.png)
4. <span data-ttu-id="7bbc0-160">デザイナーで、*コメント*列を追加し、 *nvarchar (128)* および nullable に設定して、 **[更新]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-160">In the designer, add a *Comments* column and make it *nvarchar(128)* and nullable, and then click **Update**.</span></span>

    ![コメント列の追加](deploying-a-database-update/_static/image4.png)
5. <span data-ttu-id="7bbc0-162">**[データベースの更新のプレビュー]** ボックスで、データベースの **[更新]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-162">In the **Preview Database Updates** box, click **Update Database**.</span></span>

    ![データベースの更新のプレビュー](deploying-a-database-update/_static/image5.png)

### <a name="create-a-page-to-display-and-edit-the-new-column"></a><span data-ttu-id="7bbc0-164">新しい列を表示および編集するためのページを作成する</span><span class="sxs-lookup"><span data-stu-id="7bbc0-164">Create a page to display and edit the new column</span></span>

1. <span data-ttu-id="7bbc0-165">**ソリューションエクスプローラー**で、ContosoUniversity プロジェクトの**アカウント**フォルダーを右クリックし、 **[追加]** をクリックして、 **[新しい項目]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-165">In **Solution Explorer**, right-click the **Account** folder in the ContosoUniversity project, click **Add**, and then click **New Item**.</span></span>
2. <span data-ttu-id="7bbc0-166">**マスターページを使用して新しい Web フォーム**を作成し、「 *UserInfo*」という名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-166">Create a new **Web Form Using Master Page** and name it *UserInfo.aspx*.</span></span> <span data-ttu-id="7bbc0-167">既定の*サイトのマスター*ファイルをマスターページとして受け入れます。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-167">Accept the default *Site.Master* file as the master page.</span></span>
3. <span data-ttu-id="7bbc0-168">次のマークアップを `MainContent` `Content` 要素 (最後の3つの `Content` 要素の最後) にコピーします。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-168">Copy the following markup into the `MainContent` `Content` element (the last of the 3 `Content` elements):</span></span>

    [!code-aspx[Main](deploying-a-database-update/samples/sample6.aspx)]
4. <span data-ttu-id="7bbc0-169">[ *UserInfo* ] ページを右クリックし、 **[ブラウザーで表示]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-169">Right-click the *UserInfo.aspx* page and click **View in Browser**.</span></span>
5. <span data-ttu-id="7bbc0-170">*管理者*ユーザーの資格情報 (パスワードは*devpwd*) でログインし、ユーザーにコメントを追加して、ページが正しく機能することを確認します。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-170">Log in with your *admin* user credentials (password is *devpwd*) and add some comments to a user to verify that the page works correctly.</span></span>

    ![UserInfo ページ](deploying-a-database-update/_static/image6.png)
6. <span data-ttu-id="7bbc0-172">ブラウザーを閉じます。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-172">Close the browser.</span></span>

## <a name="deploy-the-database-update"></a><span data-ttu-id="7bbc0-173">データベースの更新を展開する</span><span class="sxs-lookup"><span data-stu-id="7bbc0-173">Deploy the database update</span></span>

<span data-ttu-id="7bbc0-174">DbDacFx プロバイダーを使用して配置するには、発行プロファイルの **[データベースの更新]** オプションを選択するだけです。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-174">To deploy by using the dbDacFx provider, you just need to select the **Update database** option in the publish profile.</span></span> <span data-ttu-id="7bbc0-175">ただし、このオプションを使用した場合の初期デプロイでは、いくつかの追加の SQL スクリプトを実行するように構成しています。これらのスクリプトはまだプロファイルに含まれているため、再度実行されないようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-175">However, for the initial deployment when you used this option you also configured some additional SQL scripts to run: those are still in the profile and you'll have to prevent them from running again.</span></span>

1. <span data-ttu-id="7bbc0-176">ContosoUniversity プロジェクトを右クリックし、 **[発行]** をクリックして、 **Web の発行**ウィザードを開きます。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-176">Open the **Publish Web** wizard by right-clicking the ContosoUniversity project and clicking **Publish**.</span></span>
2. <span data-ttu-id="7bbc0-177">**テスト**プロファイルを選択します。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-177">Select the **Test** profile.</span></span>
3. <span data-ttu-id="7bbc0-178">**[設定]** タブをクリックします。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-178">Click the **Settings** tab.</span></span>
4. <span data-ttu-id="7bbc0-179">**[Defaultconnection]** で **[データベースの更新]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-179">Under **DefaultConnection**, select **Update database**.</span></span>
5. <span data-ttu-id="7bbc0-180">初期デプロイで実行するように構成した追加のスクリプトを無効にします。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-180">Disable the additional scripts that you configured to run for the initial deployment:</span></span>

    1. <span data-ttu-id="7bbc0-181">**[データベースの更新の構成]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-181">Click **Configure database updates**.</span></span>
    2. <span data-ttu-id="7bbc0-182">**[データベースの更新の構成]** ダイアログボックスで、[ *Grant .sql*および*aspnet-data-dev*] の横のチェックボックスをオフにします。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-182">In the **Configure Database Updates** dialog box, clear the check boxes next to *Grant.sql* and *aspnet-data-dev.sql*.</span></span>
    3. <span data-ttu-id="7bbc0-183">**[閉じる]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-183">Click **Close**.</span></span>
6. <span data-ttu-id="7bbc0-184">**[プレビュー]** タブをクリックします。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-184">Click the **Preview** tab.</span></span>
7. <span data-ttu-id="7bbc0-185">**[データベース]** の **[defaultconnection]** の右側で、 **[データベースのプレビュー]** リンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-185">Under **Databases** and to the right of **DefaultConnection**, click the **Preview database** link.</span></span>

    ![データベースのプレビュー](deploying-a-database-update/_static/image7.png)

    <span data-ttu-id="7bbc0-187">プレビューウィンドウには、データベーススキーマがソースデータベースのスキーマと一致するように、コピー先データベースで実行されるスクリプトが表示されます。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-187">The preview window shows the script that will be run in the destination database to make that database schema match the schema of the source database.</span></span> <span data-ttu-id="7bbc0-188">このスクリプトには、新しい列を追加する ALTER TABLE コマンドが含まれています。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-188">The script includes an ALTER TABLE command that adds the new column.</span></span>
8. <span data-ttu-id="7bbc0-189">**[データベースのプレビュー]** ダイアログボックスを閉じ、 **[発行]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-189">Close the **Database Preview** dialog box, and then click **Publish**.</span></span>

    <span data-ttu-id="7bbc0-190">更新されたアプリケーションが Visual Studio によってデプロイされ、ブラウザーがホームページに表示されます。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-190">Visual Studio deploys the updated application, and the browser opens to the home page.</span></span>
9. <span data-ttu-id="7bbc0-191">UserInfo ページ (*アカウント/UserInfo*をホームページの URL に追加) を実行して、更新が正常に展開されたことを確認します。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-191">Run the UserInfo page (add *Account/UserInfo.aspx* to the home page URL) to verify that the update was successfully deployed.</span></span> <span data-ttu-id="7bbc0-192">「 *Admin* 」と「 *devpwd*」と入力してログインする必要があります。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-192">You'll have to log in by entering *admin* and *devpwd*.</span></span>

    <span data-ttu-id="7bbc0-193">テーブル内のデータは既定では配置されません。また、データ配置スクリプトを実行するように構成していないため、開発時に追加したコメントは見つかりません。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-193">Data in tables is not deployed by default, and you didn't configure a data deployment script to run, so you won't find the comment that you added in development.</span></span> <span data-ttu-id="7bbc0-194">ステージングに新しいコメントを追加して、変更がデータベースに配置され、ページが正しく機能することを確認できます。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-194">You can add a new comment now in staging to verify that the change was deployed to the database and the page works correctly.</span></span>
10. <span data-ttu-id="7bbc0-195">同じ手順に従って、ステージング環境と運用環境にデプロイします。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-195">Follow the same procedure to deploy to staging and production.</span></span>

    <span data-ttu-id="7bbc0-196">忘れずに余分なスクリプトを無効にしてください。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-196">Don't forget to disable the extra scripts.</span></span> <span data-ttu-id="7bbc0-197">テストプロファイルとの唯一の違いは、ステージングプロファイルと実稼働プロファイルでは、 *aspnet-prod-data*のみを実行するように構成されているスクリプトを1つだけ無効にすることです。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-197">The only difference compared to the Test profile is that you will disable only one script in the Staging and Production profiles because they were configured to run only *aspnet-prod-data.sql*.</span></span>

    <span data-ttu-id="7bbc0-198">ステージングと運用の資格情報は、admin と prodpwd です。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-198">The credentials for staging and production are admin and prodpwd.</span></span>

    <span data-ttu-id="7bbc0-199">データベースの変更を含む実際の運用アプリケーションの更新については、[前のチュートリアル](deploying-a-code-update.md)で説明したように、後で発行および削除する前に、*アプリ\_offline .htm*をアップロードしてデプロイ中にアプリケーションをオフラインにすることもできます。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-199">For a real production application update that includes a database change you would also typically take the application offline during deployment by uploading *app\_offline.htm* before publishing and deleting it afterward, as you saw in [the previous tutorial](deploying-a-code-update.md).</span></span>

## <a name="summary"></a><span data-ttu-id="7bbc0-200">まとめ</span><span class="sxs-lookup"><span data-stu-id="7bbc0-200">Summary</span></span>

<span data-ttu-id="7bbc0-201">これで、Code First Migrations と dbDacFx プロバイダーの両方を使用してデータベースの変更を含むアプリケーションの更新が配置されました。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-201">You've now deployed an application update that included a database change using both Code First Migrations and the dbDacFx provider.</span></span>

![誕生日付きのインストラクターページ](deploying-a-database-update/_static/image8.png)

![UserInfo ページ](deploying-a-database-update/_static/image9.png)

<span data-ttu-id="7bbc0-204">次のチュートリアルでは、コマンドラインを使用してデプロイを実行する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="7bbc0-204">The next tutorial shows you how to execute deployments by using the command line.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="7bbc0-205">[前へ](deploying-a-code-update.md)
> [次へ](command-line-deployment.md)</span><span class="sxs-lookup"><span data-stu-id="7bbc0-205">[Previous](deploying-a-code-update.md)
[Next](command-line-deployment.md)</span></span>
