---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12
title: 'Visual Studio または Visual Web Developer を使用した SQL Server Compact を使用した ASP.NET Web アプリケーションのデプロイ: SQL Server データベース更新プログラムのデプロイ-11/12 |Microsoft Docs'
author: tdykstra
description: この一連のチュートリアルでは、Visual Stu... を使用して SQL Server Compact データベースを含む ASP.NET web アプリケーションプロジェクトをデプロイ (発行) する方法について説明します。
ms.author: riande
ms.date: 11/17/2011
ms.assetid: 5e2bb092-cb22-4511-ad0a-22ae12dd99b3
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12
msc.type: authoredcontent
ms.openlocfilehash: 0894c0ac24737e66b6960ef3d48aa17f78c6aa1d
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74621068"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-a-sql-server-database-update---11-of-12"></a><span data-ttu-id="56b56-103">Visual Studio または Visual Web Developer を使用した SQL Server Compact を使用した ASP.NET Web アプリケーションのデプロイ: SQL Server データベース更新プログラムのデプロイ-11/12</span><span class="sxs-lookup"><span data-stu-id="56b56-103">Deploying an ASP.NET Web Application with SQL Server Compact using Visual Studio or Visual Web Developer: Deploying a SQL Server Database Update - 11 of 12</span></span>

<span data-ttu-id="56b56-104">[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="56b56-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="56b56-105">スタートプロジェクトのダウンロード</span><span class="sxs-lookup"><span data-stu-id="56b56-105">Download Starter Project</span></span>](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> <span data-ttu-id="56b56-106">この一連のチュートリアルでは、Visual Studio 2012 RC または Visual Studio Express 2012 RC for Web を使用して SQL Server Compact データベースを含む ASP.NET web アプリケーションプロジェクトをデプロイ (発行) する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="56b56-106">This series of tutorials shows you how to deploy (publish) an ASP.NET web application project that includes a SQL Server Compact database by using Visual Studio 2012 RC or Visual Studio Express 2012 RC for Web.</span></span> <span data-ttu-id="56b56-107">Web 発行の更新をインストールする場合は、Visual Studio 2010 を使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="56b56-107">You can also use Visual Studio 2010 if you install the Web Publish Update.</span></span> <span data-ttu-id="56b56-108">シリーズの概要については、[シリーズの最初のチュートリアル](deployment-to-a-hosting-provider-introduction-1-of-12.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="56b56-108">For an introduction to the series, see [the first tutorial in the series](deployment-to-a-hosting-provider-introduction-1-of-12.md).</span></span>
> 
> <span data-ttu-id="56b56-109">Visual Studio 2012 の RC リリース後に導入された配置機能を示すチュートリアルについては、SQL Server Compact 以外の SQL Server のエディションをデプロイする方法、および Windows Azure Web サイトへのデプロイ方法については、「 [ASP.NET Web deployment Using Visual studio](../../deployment/visual-studio-web-deployment/introduction.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="56b56-109">For a tutorial that shows deployment features introduced after the RC release of Visual Studio 2012, shows how to deploy SQL Server editions other than SQL Server Compact, and shows how to deploy to Windows Azure Web Sites, see [ASP.NET Web Deployment using Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md).</span></span>

## <a name="overview"></a><span data-ttu-id="56b56-110">の概要</span><span class="sxs-lookup"><span data-stu-id="56b56-110">Overview</span></span>

<span data-ttu-id="56b56-111">このチュートリアルでは、データベースの更新を完全な SQL Server データベースに配置する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="56b56-111">This tutorial shows you how to deploy a database update to a full SQL Server database.</span></span> <span data-ttu-id="56b56-112">Code First Migrations はデータベースを更新するすべての作業を実行するため、このプロセスは「[データベースの更新の配置](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md)」チュートリアルの SQL Server Compact とほぼ同じです。</span><span class="sxs-lookup"><span data-stu-id="56b56-112">Because Code First Migrations does all the work of updating the database, the process is almost identical to what you did for SQL Server Compact in the [Deploying a Database Update](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md) tutorial.</span></span>

<span data-ttu-id="56b56-113">リマインダー: チュートリアルを実行しているときにエラーメッセージが表示されたり機能しない場合は、必ず[トラブルシューティングのページ](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)を確認してください。</span><span class="sxs-lookup"><span data-stu-id="56b56-113">Reminder: If you get an error message or something doesn't work as you go through the tutorial, be sure to check the [troubleshooting page](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md).</span></span>

## <a name="adding-a-new-column-to-a-table"></a><span data-ttu-id="56b56-114">テーブルへの新しい列の追加</span><span class="sxs-lookup"><span data-stu-id="56b56-114">Adding a New Column to a Table</span></span>

<span data-ttu-id="56b56-115">チュートリアルのこのセクションでは、データベースの変更とそれに対応するコードの変更を行い、テスト環境と運用環境に配置するための準備として Visual Studio でテストします。</span><span class="sxs-lookup"><span data-stu-id="56b56-115">In this section of the tutorial you'll make a database change and corresponding code changes, then test them in Visual Studio in preparation for deploying them to the test and production environments.</span></span> <span data-ttu-id="56b56-116">この変更には、`Instructor` エンティティに `OfficeHours` 列を追加し、**インストラクター** web ページに新しい情報を表示する作業が含まれます。</span><span class="sxs-lookup"><span data-stu-id="56b56-116">The change involves adding an `OfficeHours` column to the `Instructor` entity and displaying the new information in the **Instructors** web page.</span></span>

<span data-ttu-id="56b56-117">ContosoUniversity プロジェクトで*Instructor.cs*を開き、`HireDate` と `Courses` のプロパティの間に次のプロパティを追加します。</span><span class="sxs-lookup"><span data-stu-id="56b56-117">In the ContosoUniversity.DAL project, open *Instructor.cs* and add the following property between the `HireDate` and `Courses` properties:</span></span>

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample1.cs)]

<span data-ttu-id="56b56-118">テストデータを使用して新しい列をシードするように、初期化子クラスを更新します。</span><span class="sxs-lookup"><span data-stu-id="56b56-118">Update the initializer class so that it seeds the new column with test data.</span></span> <span data-ttu-id="56b56-119">*Migrations\ configuration.cs*を開き、`var instructors = new List<Instructor>` 開始するコードブロックを、新しい列を含む次のコードブロックに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="56b56-119">Open *Migrations\Configuration.cs* and replace the code block that begins `var instructors = new List<Instructor>` with the following code block which includes the new column:</span></span>

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample2.cs)]

<span data-ttu-id="56b56-120">ContosoUniversity プロジェクトで、*講師*を開き、最初の `GridView` コントロールの終了 `</Columns>` タグの直前に、office 時間の新しいテンプレートフィールドを追加します。</span><span class="sxs-lookup"><span data-stu-id="56b56-120">In the ContosoUniversity project, open *Instructors.aspx* and add a new template field for office hours just before the closing `</Columns>` tag in the first `GridView` control:</span></span>

[!code-aspx[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample3.aspx)]

<span data-ttu-id="56b56-121">ソリューションをビルドします。</span><span class="sxs-lookup"><span data-stu-id="56b56-121">Build the solution.</span></span>

<span data-ttu-id="56b56-122">**パッケージマネージャーコンソール**ウィンドウを開き、**既定のプロジェクト**として [ContosoUniversity] を選択します。</span><span class="sxs-lookup"><span data-stu-id="56b56-122">Open the **Package Manager Console** window, and select ContosoUniversity.DAL as the **Default project**.</span></span>

<span data-ttu-id="56b56-123">次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="56b56-123">Enter the following commands:</span></span>

[!code-powershell[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample4.ps1)]

<span data-ttu-id="56b56-124">アプリケーションを実行し、 **[インストラクター]** ページを選択します。</span><span class="sxs-lookup"><span data-stu-id="56b56-124">Run the application and select the **Instructors** page.</span></span> <span data-ttu-id="56b56-125">このページの読み込みには、通常よりも少し時間がかかります。これは、Entity Framework によってデータベースが再作成され、テストデータでシード処理されるためです。</span><span class="sxs-lookup"><span data-stu-id="56b56-125">The page takes a little longer than usual to load, because the Entity Framework re-creates the database and seeds it with test data.</span></span>

<span data-ttu-id="56b56-126">[![Instructors_page_with_office_hours](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="56b56-126">[![Instructors_page_with_office_hours](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image1.png)</span></span>

## <a name="deploying-the-database-update-to-the-test-environment"></a><span data-ttu-id="56b56-127">テスト環境へのデータベースの更新の配置</span><span class="sxs-lookup"><span data-stu-id="56b56-127">Deploying the Database Update to the Test Environment</span></span>

<span data-ttu-id="56b56-128">Code First Migrations を使用する場合、データベースの変更を SQL Server に配置する方法は SQL Server Compact の場合と同じです。</span><span class="sxs-lookup"><span data-stu-id="56b56-128">When you use Code First Migrations, the method for deploying a database change to SQL Server is the same as for SQL Server Compact.</span></span> <span data-ttu-id="56b56-129">ただし、SQL Server Compact から SQL Server に移行するように設定されているため、テスト発行プロファイルを変更する必要があります。</span><span class="sxs-lookup"><span data-stu-id="56b56-129">However, you have to change the Test publish profile because it is still set up to migrate from SQL Server Compact to SQL Server.</span></span>

<span data-ttu-id="56b56-130">最初の手順では、前のチュートリアルで作成した接続文字列の変換を削除します。</span><span class="sxs-lookup"><span data-stu-id="56b56-130">The first step is to remove the connection string transformations that you created in the previous tutorial.</span></span> <span data-ttu-id="56b56-131">SQL Server に移行するために **[SQL のパッケージ化/発行]** タブを構成する前と同様に、発行プロファイルで接続文字列の変換を指定するので、これらは不要になりました。</span><span class="sxs-lookup"><span data-stu-id="56b56-131">These are no longer needed because you'll specify connection string transformations in the publish profile, as you did before you configured the **Package/Publish SQL** tab for migration to SQL Server.</span></span>

<span data-ttu-id="56b56-132">*Web.config ファイルを*開き、`connectionStrings` 要素を削除します。</span><span class="sxs-lookup"><span data-stu-id="56b56-132">Open the *Web.Test.config* file and remove the `connectionStrings` element.</span></span> <span data-ttu-id="56b56-133">*Web.config ファイルの*唯一の変換は、`appSettings` 要素の `Environment` 値を示します。</span><span class="sxs-lookup"><span data-stu-id="56b56-133">The only remaining transformation in the *Web.Test.config* file is for the `Environment` value in the `appSettings` element.</span></span>

<span data-ttu-id="56b56-134">発行プロファイルを更新して、テスト環境に発行できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="56b56-134">Now you can update the publish profile and publish to the test environment.</span></span>

<span data-ttu-id="56b56-135">Web の**発行**ウィザードを開き、 **[プロファイル]** タブに切り替えます。</span><span class="sxs-lookup"><span data-stu-id="56b56-135">Open the **Publish Web** wizard, and then switch to the **Profile** tab.</span></span>

<span data-ttu-id="56b56-136">**テスト**発行プロファイルを選択します。</span><span class="sxs-lookup"><span data-stu-id="56b56-136">Select the **Test** publish profile.</span></span>

<span data-ttu-id="56b56-137">**[設定]** タブを選択します。</span><span class="sxs-lookup"><span data-stu-id="56b56-137">Select the **Settings** tab.</span></span>

<span data-ttu-id="56b56-138">[**新しいデータベース公開の機能強化を有効にする] を**クリックします。</span><span class="sxs-lookup"><span data-stu-id="56b56-138">Click **enable the new database publishing improvements**.</span></span>

<span data-ttu-id="56b56-139">**Schoolcontext.cs**の [接続文字列] ボックスに、前のチュートリアルの*web.config 変換ファイル*で使用したものと同じ値を入力します。</span><span class="sxs-lookup"><span data-stu-id="56b56-139">In the connection string box for **SchoolContext**, enter the same value that you used in the *Web.Test.config* transformation file in the previous tutorial:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample5.cmd)]

<span data-ttu-id="56b56-140">**[Code First Migrations の実行 (アプリケーションの起動時に実行)]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="56b56-140">Select **Execute Code First Migrations (runs on application start)**.</span></span> <span data-ttu-id="56b56-141">(使用している Visual Studio のバージョンでは、 **[Code First Migrations の適用]** チェックボックスがオンになっている可能性があります)。</span><span class="sxs-lookup"><span data-stu-id="56b56-141">(In your version of Visual Studio, the check box might be labeled **Apply Code First Migrations**.)</span></span>

<span data-ttu-id="56b56-142">**Defaultconnection**の [接続文字列] ボックスに、前のチュートリアルの*web.config 変換ファイル*で使用したものと同じ値を入力します。</span><span class="sxs-lookup"><span data-stu-id="56b56-142">In the connection string box for **DefaultConnection**, enter the same value that you used in the *Web.Test.config* transformation file in the previous tutorial:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample6.cmd)]

<span data-ttu-id="56b56-143">**更新データベース**をクリアしたままにします。</span><span class="sxs-lookup"><span data-stu-id="56b56-143">Leave **Update database** cleared.</span></span>

<span data-ttu-id="56b56-144">**[発行]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="56b56-144">Click **Publish**.</span></span>

<span data-ttu-id="56b56-145">Visual Studio によってコードの変更がテスト環境に配置され、ブラウザーが開き、Contoso 大学のホームページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="56b56-145">Visual Studio deploys the code changes to the test environment and opens the browser to the Contoso University home page.</span></span>

<span data-ttu-id="56b56-146">[インストラクター] ページを選択します。</span><span class="sxs-lookup"><span data-stu-id="56b56-146">Select the Instructors page.</span></span>

<span data-ttu-id="56b56-147">アプリケーションでこのページを実行すると、データベースへのアクセスが試行されます。</span><span class="sxs-lookup"><span data-stu-id="56b56-147">When the application runs this page, it tries to access the database.</span></span> <span data-ttu-id="56b56-148">Code First Migrations データベースが最新であるかどうかを確認し、最新の移行がまだ適用されていないことを検出します。</span><span class="sxs-lookup"><span data-stu-id="56b56-148">Code First Migrations checks if the database is current, and finds that the latest migration has not been applied yet.</span></span> <span data-ttu-id="56b56-149">Code First Migrations は、最新の移行を適用し、`Seed` メソッドを実行してから、ページが正常に実行されます。</span><span class="sxs-lookup"><span data-stu-id="56b56-149">Code First Migrations applies the latest migration, runs the `Seed` method, and then the page runs normally.</span></span> <span data-ttu-id="56b56-150">シードされたデータを含む新しい勤務時間列が表示されます。</span><span class="sxs-lookup"><span data-stu-id="56b56-150">You see the new Office Hours column with the seeded data.</span></span>

<span data-ttu-id="56b56-151">[![Instructors_page_with_OfficeHours_Test](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="56b56-151">[![Instructors_page_with_OfficeHours_Test](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image3.png)</span></span>

## <a name="deploying-the-database-update-to-the-production-environment"></a><span data-ttu-id="56b56-152">運用環境へのデータベースの更新の配置</span><span class="sxs-lookup"><span data-stu-id="56b56-152">Deploying the Database Update to the Production Environment</span></span>

<span data-ttu-id="56b56-153">運用環境の発行プロファイルも変更する必要があります。</span><span class="sxs-lookup"><span data-stu-id="56b56-153">You have to change the publish profile for the production environment also.</span></span> <span data-ttu-id="56b56-154">この場合は、既存のプロファイルを削除し、更新した .publishsettings ファイルをインポートして新しいプロファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="56b56-154">In this case you'll remove the existing profile and create a new one by importing an updated .publishsettings file.</span></span> <span data-ttu-id="56b56-155">更新されたファイルには、Cytanium の SQL Server データベースの接続文字列が含まれます。</span><span class="sxs-lookup"><span data-stu-id="56b56-155">The updated file will include the connection string for the SQL Server database at Cytanium.</span></span>

<span data-ttu-id="56b56-156">テスト環境に配置したときと同じように、web.config 変換ファイルで接続文字列*を変換する*必要はなくなりました。</span><span class="sxs-lookup"><span data-stu-id="56b56-156">As you saw when you deployed to the test environment, you no longer need connection string transforms in the *Web.Production.config* transformation file.</span></span> <span data-ttu-id="56b56-157">そのファイルを開き、`connectionStrings` 要素を削除します。</span><span class="sxs-lookup"><span data-stu-id="56b56-157">Open that file and remove the `connectionStrings` element.</span></span> <span data-ttu-id="56b56-158">残りの変換は、`appSettings` 要素の `Environment` 値と、Elmah エラーレポートへのアクセスを制限する `location` 要素のためのものです。</span><span class="sxs-lookup"><span data-stu-id="56b56-158">The remaining transformations are for the `Environment` value in the `appSettings` element and the `location` element that restricts access to Elmah error reports.</span></span>

<span data-ttu-id="56b56-159">運用環境用の新しい発行プロファイルを作成する前に、前に「[運用環境へのデプロイ](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)」チュートリアルで行ったのと同じ方法で、更新された .publishsettings ファイルをダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="56b56-159">Before you create a new publish profile for production, download an updated .publishsettings file the same way you did earlier in the [Deploying to the Production Environment](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) tutorial.</span></span> <span data-ttu-id="56b56-160">(Cytanium コントロールパネルで、 **[Web サイト]** をクリックし、 **[contosouniversity.com]** web サイトをクリックします。</span><span class="sxs-lookup"><span data-stu-id="56b56-160">(In the Cytanium control panel, click **Web Sites**, and then click the **contosouniversity.com** website.</span></span> <span data-ttu-id="56b56-161">**[Web 発行]** タブを選択し、 **[この Web サイトの発行プロファイルのダウンロード]** をクリックします。)これを行う理由は、.publishsettings ファイル内のデータベース接続文字列を取得するためです。</span><span class="sxs-lookup"><span data-stu-id="56b56-161">Select the **Web Publishing** tab, and then click **Download Publishing Profile for this web site**.) The reason you are doing this is to pick up the database connection string in the .publishsettings file.</span></span> <span data-ttu-id="56b56-162">この接続文字列は、まだ SQL Server Compact を使用していて、まだ Cytanium に SQL Server データベースを作成していなかったため、初めてファイルをダウンロードしたときには利用できませんでした。</span><span class="sxs-lookup"><span data-stu-id="56b56-162">The connection string wasn't available the first time you downloaded the file, because you were still using SQL Server Compact and hadn't created the SQL Server database at Cytanium yet.</span></span>

<span data-ttu-id="56b56-163">発行プロファイルを更新して、運用環境に発行できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="56b56-163">Now you can update the publish profile and publish to the production environment.</span></span>

<span data-ttu-id="56b56-164">Web の**発行**ウィザードを開き、 **[プロファイル]** タブに切り替えます。</span><span class="sxs-lookup"><span data-stu-id="56b56-164">Open the **Publish Web** wizard, and then switch to the **Profile** tab.</span></span>

<span data-ttu-id="56b56-165">**[プロファイルの管理]** をクリックし、運用プロファイルを削除します。</span><span class="sxs-lookup"><span data-stu-id="56b56-165">Click **Manage Profiles**, and then delete the Production profile.</span></span>

<span data-ttu-id="56b56-166">この変更を保存するには、 **Web の発行**ウィザードを閉じます。</span><span class="sxs-lookup"><span data-stu-id="56b56-166">Close the **Publish Web** wizard to save this change.</span></span>

<span data-ttu-id="56b56-167">Web の**発行**ウィザードをもう一度開き、 **[インポート]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="56b56-167">Open the **Publish Web** wizard again, and then click **Import**.</span></span>

<span data-ttu-id="56b56-168">一時的な URL を使用している場合は、 **[接続]** タブで、 **[送信先 URL]** を適切な値に変更します。</span><span class="sxs-lookup"><span data-stu-id="56b56-168">On the **Connection** tab, change **Destination URL** to the appropriate value if you are using a temporary URL.</span></span>

<span data-ttu-id="56b56-169">[次へ] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="56b56-169">Click **Next**.</span></span>

<span data-ttu-id="56b56-170">**[設定]** タブで、 **[新しいデータベース発行の機能強化を有効にする]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="56b56-170">On the **Settings** tab, click **enable the new database publishing improvements**.</span></span>

<span data-ttu-id="56b56-171">**Schoolcontext.cs**の [接続文字列] ボックスの一覧で、Cytanium 接続文字列を選択します。</span><span class="sxs-lookup"><span data-stu-id="56b56-171">In the connection string drop-down list for **SchoolContext**, select the Cytanium connection string.</span></span>

![Selecting_Cytanium_connection_string](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image5.png)

<span data-ttu-id="56b56-173">**[実行 Code First の移行 (アプリケーションの起動時に実行)]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="56b56-173">Select **Execute Code First migrations (runs on application start)**.</span></span>

<span data-ttu-id="56b56-174">**Defaultconnection**の [接続文字列] ボックスの一覧で、Cytanium 接続文字列を選択します。</span><span class="sxs-lookup"><span data-stu-id="56b56-174">In the connection string drop-down list for **DefaultConnection**, select the Cytanium connection string.</span></span>

<span data-ttu-id="56b56-175">**[プロファイル]** タブを選択し、プロファイルの **[管理]** をクリックして、プロファイルの名前を "contosouniversity.com-Web 配置" から "Production" に変更します。</span><span class="sxs-lookup"><span data-stu-id="56b56-175">Select the **Profile** tab, click **Manage Profiles**, and rename the profile from "contosouniversity.com - Web Deploy" to "Production".</span></span>

<span data-ttu-id="56b56-176">発行プロファイルを閉じて変更を保存し、再度開いてください。</span><span class="sxs-lookup"><span data-stu-id="56b56-176">Close the publish profile to save the change, then open it again.</span></span>

<span data-ttu-id="56b56-177">**[発行]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="56b56-177">Click **Publish**.</span></span> <span data-ttu-id="56b56-178">(実際の運用 web サイトの場合は、 *app\_をオフライン*にしてから運用環境にコピーし、発行前にプロジェクトフォルダーに置き、デプロイが完了したら削除します)。</span><span class="sxs-lookup"><span data-stu-id="56b56-178">(For a real production website, you would copy *app\_offline.htm* to production and put it in your project folder before publishing, then remove it when deployment is complete.)</span></span>

<span data-ttu-id="56b56-179">Visual Studio によってコードの変更がテスト環境に配置され、ブラウザーが開き、Contoso 大学のホームページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="56b56-179">Visual Studio deploys the code changes to the test environment and opens the browser to the Contoso University home page.</span></span>

<span data-ttu-id="56b56-180">[インストラクター] ページを選択します。</span><span class="sxs-lookup"><span data-stu-id="56b56-180">Select the Instructors page.</span></span>

<span data-ttu-id="56b56-181">Code First Migrations は、テスト環境での場合と同じ方法でデータベースを更新します。</span><span class="sxs-lookup"><span data-stu-id="56b56-181">Code First Migrations updates the database the same way it did in the Test environment.</span></span> <span data-ttu-id="56b56-182">シードされたデータを含む新しい勤務時間列が表示されます。</span><span class="sxs-lookup"><span data-stu-id="56b56-182">You see the new Office Hours column with the seeded data.</span></span>

![Instructors_page_with_OfficeHours_Prod](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image6.png)

<span data-ttu-id="56b56-184">これで、SQL Server データベースを使用して、データベースの変更を含むアプリケーションの更新が正常に展開されました。</span><span class="sxs-lookup"><span data-stu-id="56b56-184">You have now successfully deployed an application update that included a database change, using a SQL Server database.</span></span>

## <a name="more-information"></a><span data-ttu-id="56b56-185">その他の情報</span><span class="sxs-lookup"><span data-stu-id="56b56-185">More Information</span></span>

<span data-ttu-id="56b56-186">これで、ASP.NET web アプリケーションをサードパーティのホスティングプロバイダーにデプロイするための一連のチュートリアルが完了します。</span><span class="sxs-lookup"><span data-stu-id="56b56-186">This completes this series of tutorials on deploying an ASP.NET web application to a third-party hosting provider.</span></span> <span data-ttu-id="56b56-187">これらのチュートリアルで説明されているトピックの詳細については、MSDN web サイトの「 [ASP.NET Deployment コンテンツマップ](https://msdn.microsoft.com/library/bb386521(v=vs.110).aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="56b56-187">For more information about any of the topics covered in these tutorials, see the [ASP.NET Deployment Content Map](https://msdn.microsoft.com/library/bb386521(v=vs.110).aspx) on the MSDN web site.</span></span>

## <a name="acknowledgements"></a><span data-ttu-id="56b56-188">謝辞</span><span class="sxs-lookup"><span data-stu-id="56b56-188">Acknowledgements</span></span>

<span data-ttu-id="56b56-189">このチュートリアルシリーズの内容に多大な貢献をした次の人々に感謝したいと思います。</span><span class="sxs-lookup"><span data-stu-id="56b56-189">I would like to thank the following people who made significant contributions to the content of this tutorial series:</span></span>

- [<span data-ttu-id="56b56-190">Alberto Poblacion, MVP &amp; MCT, スペイン</span><span class="sxs-lookup"><span data-stu-id="56b56-190">Alberto Poblacion, MVP &amp; MCT, Spain</span></span>](https://mvp.support.microsoft.com/profile/Alberto)
- <span data-ttu-id="56b56-191">Jarod Ferguson、Data Platform Development MVP、米国</span><span class="sxs-lookup"><span data-stu-id="56b56-191">Jarod Ferguson, Data Platform Development MVP, United States</span></span>
- <span data-ttu-id="56b56-192">過酷 Mittal、Microsoft</span><span class="sxs-lookup"><span data-stu-id="56b56-192">Harsh Mittal, Microsoft</span></span>
- [<span data-ttu-id="56b56-193">Kristina Olson、Microsoft</span><span class="sxs-lookup"><span data-stu-id="56b56-193">Kristina Olson, Microsoft</span></span>](https://blogs.iis.net/krolson/default.aspx)
- [<span data-ttu-id="56b56-194">Mike Pope、Microsoft</span><span class="sxs-lookup"><span data-stu-id="56b56-194">Mike Pope, Microsoft</span></span>](http://www.mikepope.com/blog/DisplayBlog.aspx)
- <span data-ttu-id="56b56-195">Mohit Srivastava、Microsoft</span><span class="sxs-lookup"><span data-stu-id="56b56-195">Mohit Srivastava, Microsoft</span></span>
- [<span data-ttu-id="56b56-196">Raffaele Rialdi、イタリア</span><span class="sxs-lookup"><span data-stu-id="56b56-196">Raffaele Rialdi, Italy</span></span>](http://www.iamraf.net/)
- [<span data-ttu-id="56b56-197">Rick Anderson、Microsoft</span><span class="sxs-lookup"><span data-stu-id="56b56-197">Rick Anderson, Microsoft</span></span>](https://blogs.msdn.com/b/rickandy/)
- <span data-ttu-id="56b56-198">[作成者 Hashimi、Microsoft](http://sedodream.com/default.aspx)(twitter: [@sayedihashimi](http://twitter.com/sayedihashimi))</span><span class="sxs-lookup"><span data-stu-id="56b56-198">[Sayed Hashimi, Microsoft](http://sedodream.com/default.aspx)(twitter: [@sayedihashimi](http://twitter.com/sayedihashimi))</span></span>
- <span data-ttu-id="56b56-199">[Scott マン Selman](http://www.hanselman.com/blog/) (twitter: [@shanselman](http://twitter.com/shanselman))</span><span class="sxs-lookup"><span data-stu-id="56b56-199">[Scott Hanselman](http://www.hanselman.com/blog/) (twitter: [@shanselman](http://twitter.com/shanselman))</span></span>
- <span data-ttu-id="56b56-200">[Scott Hunter、Microsoft](https://blogs.msdn.com/b/scothu/) (twitter: [@coolcsh](http://twitter.com/coolcsh))</span><span class="sxs-lookup"><span data-stu-id="56b56-200">[Scott Hunter, Microsoft](https://blogs.msdn.com/b/scothu/) (twitter: [@coolcsh](http://twitter.com/coolcsh))</span></span>
- [<span data-ttu-id="56b56-201">Srđan Božović、セルビア</span><span class="sxs-lookup"><span data-stu-id="56b56-201">Srđan Božović, Serbia</span></span>](http://msforge.net/blogs/zmajcek/)
- <span data-ttu-id="56b56-202">[Vishal Joshi、Microsoft](http://vishaljoshi.blogspot.com/) (twitter: [@vishalrjoshi](http://twitter.com/vishalrjoshi))</span><span class="sxs-lookup"><span data-stu-id="56b56-202">[Vishal Joshi, Microsoft](http://vishaljoshi.blogspot.com/) (twitter: [@vishalrjoshi](http://twitter.com/vishalrjoshi))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="56b56-203">[前へ](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12.md)
> [次へ](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)</span><span class="sxs-lookup"><span data-stu-id="56b56-203">[Previous](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12.md)
[Next](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)</span></span>
