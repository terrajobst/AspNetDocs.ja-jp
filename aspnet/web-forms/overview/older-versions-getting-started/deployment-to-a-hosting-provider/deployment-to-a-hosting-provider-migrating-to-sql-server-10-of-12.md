---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12
title: 'Visual Studio または Visual Web Developer を使用した SQL Server Compact を使用した ASP.NET Web アプリケーションのデプロイ: SQL Server 12 | への移行Microsoft Docs'
author: tdykstra
description: この一連のチュートリアルでは、Visual Stu... を使用して SQL Server Compact データベースを含む ASP.NET web アプリケーションプロジェクトをデプロイ (発行) する方法について説明します。
ms.author: riande
ms.date: 11/17/2011
ms.assetid: a89d6f32-b71b-4036-8ff7-5f8ac2a6eca8
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12
msc.type: authoredcontent
ms.openlocfilehash: c5281a42596d95e725b32e652c75785abe0fd64e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78462838"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-migrating-to-sql-server---10-of-12"></a><span data-ttu-id="943ba-103">Visual Studio または Visual Web Developer を使用した SQL Server Compact を使用した ASP.NET Web アプリケーションのデプロイ: SQL Server 12 の10への移行</span><span class="sxs-lookup"><span data-stu-id="943ba-103">Deploying an ASP.NET Web Application with SQL Server Compact using Visual Studio or Visual Web Developer: Migrating to SQL Server - 10 of 12</span></span>

<span data-ttu-id="943ba-104">[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="943ba-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="943ba-105">スタートプロジェクトのダウンロード</span><span class="sxs-lookup"><span data-stu-id="943ba-105">Download Starter Project</span></span>](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> <span data-ttu-id="943ba-106">この一連のチュートリアルでは、Visual Studio 2012 RC または Visual Studio Express 2012 RC for Web を使用して SQL Server Compact データベースを含む ASP.NET web アプリケーションプロジェクトをデプロイ (発行) する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="943ba-106">This series of tutorials shows you how to deploy (publish) an ASP.NET web application project that includes a SQL Server Compact database by using Visual Studio 2012 RC or Visual Studio Express 2012 RC for Web.</span></span> <span data-ttu-id="943ba-107">Web 発行の更新をインストールする場合は、Visual Studio 2010 を使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="943ba-107">You can also use Visual Studio 2010 if you install the Web Publish Update.</span></span> <span data-ttu-id="943ba-108">シリーズの概要については、[シリーズの最初のチュートリアル](deployment-to-a-hosting-provider-introduction-1-of-12.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="943ba-108">For an introduction to the series, see [the first tutorial in the series](deployment-to-a-hosting-provider-introduction-1-of-12.md).</span></span>
> 
> <span data-ttu-id="943ba-109">Visual Studio 2012 の RC リリース後に導入された配置機能を示すチュートリアルについては、SQL Server Compact 以外の SQL Server のエディションをデプロイする方法、Azure App Service Web Apps にデプロイする方法については、「 [ASP.NET Web deployment Using Visual studio (Visual studio を使用した Web デプロイ](../../deployment/visual-studio-web-deployment/introduction.md)のデプロイ)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="943ba-109">For a tutorial that shows deployment features introduced after the RC release of Visual Studio 2012, shows how to deploy SQL Server editions other than SQL Server Compact, and shows how to deploy to Azure App Service Web Apps, see [ASP.NET Web Deployment using Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md).</span></span>

## <a name="overview"></a><span data-ttu-id="943ba-110">概要</span><span class="sxs-lookup"><span data-stu-id="943ba-110">Overview</span></span>

<span data-ttu-id="943ba-111">このチュートリアルでは、SQL Server Compact から SQL Server に移行する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="943ba-111">This tutorial shows you how to migrate from SQL Server Compact to SQL Server.</span></span> <span data-ttu-id="943ba-112">そのためには、ストアドプロシージャ、トリガー、ビュー、レプリケーションなど、SQL Server Compact でサポートされていない SQL Server 機能を利用することが必要になることがあります。</span><span class="sxs-lookup"><span data-stu-id="943ba-112">One reason you might want to do that is to take advantage of SQL Server features that SQL Server Compact does not support, such as stored procedures, triggers, views, or replication.</span></span> <span data-ttu-id="943ba-113">SQL Server Compact と SQL Server の違いの詳細については、 [SQL Server Compact のデプロイ](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12.md)に関するチュートリアルを参照してください。</span><span class="sxs-lookup"><span data-stu-id="943ba-113">For more information about the differences between SQL Server Compact and SQL Server, see the [Deploying SQL Server Compact](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12.md) tutorial.</span></span>

### <a name="sql-server-express-versus-full-sql-server-for-development"></a><span data-ttu-id="943ba-114">SQL Server Express と完全な SQL Server 開発</span><span class="sxs-lookup"><span data-stu-id="943ba-114">SQL Server Express versus full SQL Server for Development</span></span>

<span data-ttu-id="943ba-115">SQL Server にアップグレードする場合は、開発環境とテスト環境で SQL Server または SQL Server Express を使用することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="943ba-115">Once you've decided to upgrade to SQL Server, you might want to use SQL Server or SQL Server Express in your development and test environments.</span></span> <span data-ttu-id="943ba-116">ツールのサポートとデータベースエンジンの機能の違いに加えて、SQL Server Compact とその他のバージョンの SQL Server 間のプロバイダー実装には違いがあります。</span><span class="sxs-lookup"><span data-stu-id="943ba-116">In addition to the differences in tool support and in database engine features, there are differences in provider implementations between SQL Server Compact and other versions of SQL Server.</span></span> <span data-ttu-id="943ba-117">これらの違いにより、同じコードによって異なる結果が生成される可能性があります。</span><span class="sxs-lookup"><span data-stu-id="943ba-117">These differences can cause the same code to generate different results.</span></span> <span data-ttu-id="943ba-118">そのため、SQL Server Compact を開発データベースとして保持する場合は、運用環境に配置する前に、SQL Server また SQL Server Express はテスト環境でサイトを十分にテストする必要があります。</span><span class="sxs-lookup"><span data-stu-id="943ba-118">Therefore, if you decide to keep SQL Server Compact as your development database, you should thoroughly test your site in SQL Server or SQL Server Express in a test environment before each deployment to production.</span></span>

<span data-ttu-id="943ba-119">SQL Server Compact とは異なり、SQL Server Express は基本的には同じデータベースエンジンであり、完全 SQL Server と同じ .NET プロバイダーを使用します。</span><span class="sxs-lookup"><span data-stu-id="943ba-119">Unlike SQL Server Compact, SQL Server Express is essentially the same database engine and uses the same .NET provider as full SQL Server.</span></span> <span data-ttu-id="943ba-120">SQL Server Express でテストする場合は、SQL Server と同じ結果を得ることができます。</span><span class="sxs-lookup"><span data-stu-id="943ba-120">When you test with SQL Server Express, you can be confident of getting the same results as you will with SQL Server.</span></span> <span data-ttu-id="943ba-121">SQL Server で使用できるのと同じデータベースツールの大部分 ( [SQL Server プロファイラー](https://msdn.microsoft.com/library/ms181091.aspx)されている重要な例外) を使用して、ストアドプロシージャ、ビュー、トリガー、レプリケーションなどの SQL Server の他の機能をサポート SQL Server Express ことができます。</span><span class="sxs-lookup"><span data-stu-id="943ba-121">You can use most of the same database tools with SQL Server Express that you can use with SQL Server (a notable exception being [SQL Server Profiler](https://msdn.microsoft.com/library/ms181091.aspx)), and it supports other features of SQL Server like stored procedures, views, triggers, and replication.</span></span> <span data-ttu-id="943ba-122">(通常は、運用 web サイトで完全 SQL Server を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="943ba-122">(You typically have to use full SQL Server in a production website, however.</span></span> <span data-ttu-id="943ba-123">SQL Server Express は共有ホスティング環境で実行できますが、そのように設計されていないため、多くのホスティングプロバイダーではサポートされていません)。</span><span class="sxs-lookup"><span data-stu-id="943ba-123">SQL Server Express can run in a shared hosting environment, but it was not designed for that, and many hosting providers do not support it.)</span></span>

<span data-ttu-id="943ba-124">Visual Studio 2012 を使用している場合、通常は Visual Studio と共にインストールされるため、開発環境には SQL Server Express LocalDB を選択します。</span><span class="sxs-lookup"><span data-stu-id="943ba-124">If you are using Visual Studio 2012, you typically choose SQL Server Express LocalDB for your development environment because that is what is installed by default with Visual Studio.</span></span> <span data-ttu-id="943ba-125">ただし、LocalDB は IIS では機能しないため、テスト環境では SQL Server または SQL Server Express のいずれかを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="943ba-125">However, LocalDB does not work in IIS, so for your test environment you have to use either SQL Server or SQL Server Express.</span></span>

### <a name="combining-databases-versus-keeping-them-separate"></a><span data-ttu-id="943ba-126">データベースの結合と分離</span><span class="sxs-lookup"><span data-stu-id="943ba-126">Combining Databases versus Keeping Them Separate</span></span>

<span data-ttu-id="943ba-127">Contoso 大学アプリケーションには、メンバーシップデータベース (*aspnet*) とアプリケーションデータベース (*School*) という2つの SQL Server Compact データベースがあります。</span><span class="sxs-lookup"><span data-stu-id="943ba-127">The Contoso University application has two SQL Server Compact databases: the membership database (*aspnet.sdf*) and the application database (*School.sdf*).</span></span> <span data-ttu-id="943ba-128">移行時に、これらのデータベースを2つの異なるデータベースまたは1つのデータベースに移行できます。</span><span class="sxs-lookup"><span data-stu-id="943ba-128">When you migrate, you can migrate these databases to two separate databases or to a single database.</span></span> <span data-ttu-id="943ba-129">アプリケーションデータベースとメンバーシップデータベースの間のデータベースの結合を容易にするために、これらを組み合わせて使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="943ba-129">You might want to combine them in order to facilitate database joins between your application database and your membership database.</span></span> <span data-ttu-id="943ba-130">ホスティングプランでは、それらを組み合わせる理由が提供される場合もあります。</span><span class="sxs-lookup"><span data-stu-id="943ba-130">Your hosting plan might also provide a reason to combine them.</span></span> <span data-ttu-id="943ba-131">たとえば、ホスティングプロバイダーは複数のデータベースに対してより多くの料金を請求する場合や、複数のデータベースを許可しない場合があります。</span><span class="sxs-lookup"><span data-stu-id="943ba-131">For example, the hosting provider might charge more for multiple databases or might not even allow more than one database.</span></span> <span data-ttu-id="943ba-132">このチュートリアルで使用されている Cytanium Lite ホスティングアカウントの場合は、1つの SQL Server データベースのみが許可されます。</span><span class="sxs-lookup"><span data-stu-id="943ba-132">That's the case with the Cytanium Lite hosting account that's used for this tutorial, which allows only a single SQL Server database.</span></span>

<span data-ttu-id="943ba-133">このチュートリアルでは、次のように2つのデータベースを移行します。</span><span class="sxs-lookup"><span data-stu-id="943ba-133">In this tutorial, you'll migrate your two databases this way:</span></span>

- <span data-ttu-id="943ba-134">開発環境で2つの LocalDB データベースに移行します。</span><span class="sxs-lookup"><span data-stu-id="943ba-134">Migrate to two LocalDB databases in the development environment.</span></span>
- <span data-ttu-id="943ba-135">テスト環境で2つの SQL Server Express データベースに移行します。</span><span class="sxs-lookup"><span data-stu-id="943ba-135">Migrate to two SQL Server Express databases in the test environment.</span></span>
- <span data-ttu-id="943ba-136">運用環境で完全に結合された1つの SQL Server データベースに移行します。</span><span class="sxs-lookup"><span data-stu-id="943ba-136">Migrate to one combined full SQL Server database in the production environment.</span></span>

<span data-ttu-id="943ba-137">リマインダー: チュートリアルを実行しているときにエラーメッセージが表示されたり機能しない場合は、必ず[トラブルシューティングのページ](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)を確認してください。</span><span class="sxs-lookup"><span data-stu-id="943ba-137">Reminder: If you get an error message or something doesn't work as you go through the tutorial, be sure to check the [troubleshooting page](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md).</span></span>

## <a name="installing-sql-server-express"></a><span data-ttu-id="943ba-138">SQL Server Express のインストール</span><span class="sxs-lookup"><span data-stu-id="943ba-138">Installing SQL Server Express</span></span>

<span data-ttu-id="943ba-139">既定では、Visual Studio 2010 には SQL Server Express が自動的にインストールされますが、既定では Visual Studio 2012 と共にインストールされません。</span><span class="sxs-lookup"><span data-stu-id="943ba-139">SQL Server Express is automatically installed by default with Visual Studio 2010, but by default it is not installed with Visual Studio 2012.</span></span> <span data-ttu-id="943ba-140">SQL Server 2012 Express をインストールするには、次のリンクをクリックしてください。</span><span class="sxs-lookup"><span data-stu-id="943ba-140">To install SQL Server 2012 Express, click the following link</span></span>

- [<span data-ttu-id="943ba-141">SQL Server Express 2012</span><span class="sxs-lookup"><span data-stu-id="943ba-141">SQL Server Express 2012</span></span>](https://www.microsoft.com/download/details.aspx?id=29062)

<span data-ttu-id="943ba-142">*Enu/x64/sqlexpr\_x64\_enu*または*enu/X86/sqlexpr\_x86\_enu*を選択し、インストールウィザードで既定の設定をそのまま使用します。</span><span class="sxs-lookup"><span data-stu-id="943ba-142">Choose *ENU/x64/SQLEXPR\_x64\_ENU.exe* or *ENU/x86/SQLEXPR\_x86\_ENU.exe*, and in the installation wizard accept the default settings.</span></span> <span data-ttu-id="943ba-143">インストールオプションの詳細については、「インストール[ウィザードから SQL Server 2012 をインストールする (セットアップ)](https://msdn.microsoft.com/library/ms143219.aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="943ba-143">For more information about installation options, see [Install SQL Server 2012 from the Installation Wizard (Setup)](https://msdn.microsoft.com/library/ms143219.aspx).</span></span>

## <a name="creating-sql-server-express-databases-for-the-test-environment"></a><span data-ttu-id="943ba-144">テスト環境用の SQL Server Express データベースの作成</span><span class="sxs-lookup"><span data-stu-id="943ba-144">Creating SQL Server Express Databases for the Test Environment</span></span>

<span data-ttu-id="943ba-145">次の手順では、ASP.NET membership データベースと School データベースを作成します。</span><span class="sxs-lookup"><span data-stu-id="943ba-145">The next step is to create the ASP.NET membership and School databases.</span></span>

<span data-ttu-id="943ba-146">**表示** メニューの **サーバーエクスプローラー** (Visual Web Developer では**データベースエクスプローラー** ) を選択し、**データ接続** を右クリックして、**新しい SQL Server データベースの作成** を選択します。</span><span class="sxs-lookup"><span data-stu-id="943ba-146">From the **View** menu select **Server Explorer** (**Database Explorer** in Visual Web Developer), and then right-click **Data Connections** and select **Create New SQL Server Database**.</span></span>

![Selecting_Create_New_SQL_Server_Database](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image1.png)

<span data-ttu-id="943ba-148">**[新しい SQL Server データベースの作成]** ダイアログボックスの **[サーバー名]** ボックスに「.\SQLExpress」と入力し、 **[新しいデータベース名]** ボックスに「aspnet-Test」と入力して、[ **OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="943ba-148">In the **Create New SQL Server Database** dialog box, enter ".\SQLExpress" in the **Server name** box and "aspnet-Test" in the **New database name** box, then click **OK**.</span></span>

![Create_New_SQL_Server_Database_aspnet](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image2.png)

<span data-ttu-id="943ba-150">同じ手順に従って、"School-Test" という名前の新しい SQL Server Express School データベースを作成します。</span><span class="sxs-lookup"><span data-stu-id="943ba-150">Follow the same procedure to create a new SQL Server Express School database named "School-Test".</span></span>

<span data-ttu-id="943ba-151">(後で開発環境用に各データベースの追加インスタンスを作成し、2つのデータベースセットを区別できるようにする必要があるため、これらのデータベース名に "Test" を追加しています)。</span><span class="sxs-lookup"><span data-stu-id="943ba-151">(You're appending "Test" to these database names because later you'll create an additional instance of each database for the development environment, and you need to be able to differentiate the two sets of databases.)</span></span>

<span data-ttu-id="943ba-152">**サーバーエクスプローラー**に、2つの新しいデータベースが表示されるようになりました。</span><span class="sxs-lookup"><span data-stu-id="943ba-152">**Server Explorer** now shows the two new databases.</span></span>

![New_databases_in_Server_Explorer](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image3.png)

## <a name="creating-a-grant-script-for-the-new-databases"></a><span data-ttu-id="943ba-154">新しいデータベースに対して Grant スクリプトを作成する</span><span class="sxs-lookup"><span data-stu-id="943ba-154">Creating a Grant Script for the New Databases</span></span>

<span data-ttu-id="943ba-155">開発用コンピューターの IIS でアプリケーションを実行すると、アプリケーションは既定のアプリケーションプールの資格情報を使用してデータベースにアクセスします。</span><span class="sxs-lookup"><span data-stu-id="943ba-155">When the application runs in IIS on your development computer, the application accesses the database by using the default application pool's credentials.</span></span> <span data-ttu-id="943ba-156">ただし、既定では、アプリケーションプール id には、データベースを開くためのアクセス許可がありません。</span><span class="sxs-lookup"><span data-stu-id="943ba-156">However, by default, the application pool identity does not have permission to open the databases.</span></span> <span data-ttu-id="943ba-157">そのため、そのアクセス許可を付与するスクリプトを実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="943ba-157">So you have to run a script to grant that permission.</span></span> <span data-ttu-id="943ba-158">このセクションでは、後で実行するスクリプトを作成して、アプリケーションが IIS で実行されたときにデータベースを開けるようにします。</span><span class="sxs-lookup"><span data-stu-id="943ba-158">In this section you create the script that you'll run later to make sure that the application can open the databases when it runs in IIS.</span></span>

<span data-ttu-id="943ba-159">「[運用環境へのデプロイ](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)」チュートリアルで作成したソリューションの*solutionfiles*フォルダーで、 *Grant .sql*という名前の新しい SQL ファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="943ba-159">In the solution's *SolutionFiles* folder that you created in the [Deploying to the Production Environment](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) tutorial, create a new SQL file named *Grant.sql*.</span></span> <span data-ttu-id="943ba-160">次の SQL コマンドをファイルにコピーし、ファイルを保存して閉じます。</span><span class="sxs-lookup"><span data-stu-id="943ba-160">Copy the following SQL commands into the file, and then save and close the file:</span></span>

[!code-sql[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample1.sql)]

> [!NOTE]
> <span data-ttu-id="943ba-161">このスクリプトは、このチュートリアルで指定されているように、SQL Server 2008 と Windows 7 の IIS 設定で動作するように設計されています。</span><span class="sxs-lookup"><span data-stu-id="943ba-161">This script is designed to work with SQL Server 2008 and with the IIS settings in Windows 7 as they are specified in this tutorial.</span></span> <span data-ttu-id="943ba-162">異なるバージョンの SQL Server または Windows を使用している場合、またはコンピューターに IIS を別の方法でセットアップする場合は、このスクリプトへの変更が必要になることがあります。</span><span class="sxs-lookup"><span data-stu-id="943ba-162">If you're using a different version of SQL Server or of Windows, or if you set up IIS on your computer differently, changes to this script might be required.</span></span> <span data-ttu-id="943ba-163">SQL Server スクリプトの詳細については、「 [SQL Server オンラインブック](https://go.microsoft.com/fwlink/?LinkId=132511)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="943ba-163">For more information about SQL Server scripts, see [SQL Server Books Online](https://go.microsoft.com/fwlink/?LinkId=132511).</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="943ba-164">**セキュリティ**に関する注意このスクリプトは、実行時にデータベースにアクセスするユーザーに対して、db\_所有者のアクセス許可を付与します。これは、運用環境で使用するものです。</span><span class="sxs-lookup"><span data-stu-id="943ba-164">**Security Note** This script gives db\_owner permissions to the user that accesses the database at run time, which is what you'll have in the production environment.</span></span> <span data-ttu-id="943ba-165">場合によっては、完全なデータベーススキーマ更新権限を持つユーザーを配置に対してのみ指定し、実行時にデータの読み取りと書き込みのみの権限を持つユーザーを指定することが必要になる場合があります。</span><span class="sxs-lookup"><span data-stu-id="943ba-165">In some scenarios you might want to specify a user that has full database schema update permissions only for deployment, and specify for run time a different user that has permissions only to read and write data.</span></span> <span data-ttu-id="943ba-166">詳細については、「[テスト環境としての IIS への配置](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md)」の「 **Code First Migrations の Web.config の自動変更を確認**する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="943ba-166">For more information, see **Reviewing the Automatic Web.config Changes for Code First Migrations** in [Deploying to IIS as a Test Environment](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md).</span></span>

## <a name="configuring-database-deployment-for-the-test-environment"></a><span data-ttu-id="943ba-167">テスト環境のデータベース配置の構成</span><span class="sxs-lookup"><span data-stu-id="943ba-167">Configuring Database Deployment for the Test Environment</span></span>

<span data-ttu-id="943ba-168">次に、各データベースに対して次のタスクが実行されるように Visual Studio を構成します。</span><span class="sxs-lookup"><span data-stu-id="943ba-168">Next, you'll configure Visual Studio so that it will do the following tasks for each database:</span></span>

- <span data-ttu-id="943ba-169">コピー先データベースにソースデータベースの構造 (テーブル、列、制約など) を作成する SQL スクリプトを生成します。</span><span class="sxs-lookup"><span data-stu-id="943ba-169">Generate a SQL script that creates the source database's structure (tables, columns, constraints, etc.) in the destination database.</span></span>
- <span data-ttu-id="943ba-170">転送元データベースのデータをコピー先のデータベースのテーブルに挿入する SQL スクリプトを生成します。</span><span class="sxs-lookup"><span data-stu-id="943ba-170">Generate a SQL script that inserts the source database's data into the tables in the destination database.</span></span>
- <span data-ttu-id="943ba-171">生成されたスクリプトと、作成した Grant スクリプトを対象のデータベースに実行します。</span><span class="sxs-lookup"><span data-stu-id="943ba-171">Run the generated scripts, and the Grant script that you created, in the destination database.</span></span>

<span data-ttu-id="943ba-172">プロジェクトの**プロパティ**ウィンドウを開き、 **[SQL のパッケージ化/発行]** タブを選択します。</span><span class="sxs-lookup"><span data-stu-id="943ba-172">Open the **Project Properties** window and select the **Package/Publish SQL** tab.</span></span>

<span data-ttu-id="943ba-173">**[構成]** ドロップダウンリストで **[アクティブ (リリース)]** または **[リリース]** が選択されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="943ba-173">Make sure that **Active (Release)** or **Release** is selected in the **Configuration** drop-down list.</span></span>

<span data-ttu-id="943ba-174">[**このページを有効にする] を**クリックします。</span><span class="sxs-lookup"><span data-stu-id="943ba-174">Click **Enable this Page**.</span></span>

![Package_Publish_SQL_tab_Enable_This_page](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image4.png)

<span data-ttu-id="943ba-176">**[SQL のパッケージ化/発行]** タブは、従来の配置方法を指定するため、通常は無効になっています。</span><span class="sxs-lookup"><span data-stu-id="943ba-176">The **Package/Publish SQL** tab is normally disabled because it specifies a legacy deployment method.</span></span> <span data-ttu-id="943ba-177">ほとんどのシナリオでは、 **Web の発行**ウィザードでデータベースの配置を構成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="943ba-177">For most scenarios, you should configure database deployment in the **Publish Web** wizard.</span></span> <span data-ttu-id="943ba-178">SQL Server Compact から SQL Server または SQL Server Express への移行は、この方法が適切な選択である特殊なケースです。</span><span class="sxs-lookup"><span data-stu-id="943ba-178">Migrating from SQL Server Compact to SQL Server or SQL Server Express is a special case for which this method is a good choice.</span></span>

<span data-ttu-id="943ba-179">[Web.config**からのインポート] を**クリックします。</span><span class="sxs-lookup"><span data-stu-id="943ba-179">Click **Import from Web.config**.</span></span>

![Selecting_Import_from_Web .config](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image5.png)

<span data-ttu-id="943ba-181">Visual *Studio は、web.config ファイルで*接続文字列を検索し、メンバーシップデータベース用と School データベース用の接続文字列を検索し、**データベースエントリ**テーブル内の各接続文字列に対応する行を追加します。</span><span class="sxs-lookup"><span data-stu-id="943ba-181">Visual Studio looks for connection strings in the *Web.config* file, finds one for the membership database and one for the School database, and adds a row corresponding to each connection string in the **Database Entries** table.</span></span> <span data-ttu-id="943ba-182">検出された接続文字列は既存の SQL Server Compact データベース用です。次の手順では、これらのデータベースを配置する方法と場所を構成します。</span><span class="sxs-lookup"><span data-stu-id="943ba-182">The connection strings it finds are for the existing SQL Server Compact databases, and your next step will be to configure how and where to deploy these databases.</span></span>

<span data-ttu-id="943ba-183">データベースの配置設定は、データベース**エントリ**のテーブルの下にある **[データベースエントリの詳細]** セクションに入力します。</span><span class="sxs-lookup"><span data-stu-id="943ba-183">You enter database deployment settings in the **Database Entry Details** section below the **Database Entries** table.</span></span> <span data-ttu-id="943ba-184">次の図に示すように、データベースエントリの **[詳細]** セクションに表示される設定は、 **[データベースエントリ]** テーブルのいずれかの行に関連します。</span><span class="sxs-lookup"><span data-stu-id="943ba-184">The settings shown in the **Database Entry Details** section pertain to whichever row in the **Database Entries** table is selected, as shown in the following illustration.</span></span>

![Database_Entry_Details_section_of_Package_Publish_SQL_tab](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image6.png)

### <a name="configuring-deployment-settings-for-the-membership-database"></a><span data-ttu-id="943ba-186">メンバーシップデータベースの配置設定の構成</span><span class="sxs-lookup"><span data-stu-id="943ba-186">Configuring Deployment Settings for the Membership Database</span></span>

<span data-ttu-id="943ba-187">メンバーシップデータベースに適用される設定を構成するには、 **[データベースエントリ]** テーブルで**Defaultconnection-Deployment**行を選択します。</span><span class="sxs-lookup"><span data-stu-id="943ba-187">Select the **DefaultConnection-Deployment** row in the **Database Entries** table in order to configure settings that apply to the membership database.</span></span>

<span data-ttu-id="943ba-188">**[転送先データベースの接続文字列]** に、新しい SQL Server Express メンバーシップデータベースを指す接続文字列を入力します。</span><span class="sxs-lookup"><span data-stu-id="943ba-188">In **Connection string for destination database**, enter a connection string that points to the new SQL Server Express membership database.</span></span> <span data-ttu-id="943ba-189">**サーバーエクスプローラー**から必要な接続文字列を取得できます。</span><span class="sxs-lookup"><span data-stu-id="943ba-189">You can get the connection string you need from **Server Explorer**.</span></span> <span data-ttu-id="943ba-190">**サーバーエクスプローラー**で、 **[データ接続]** を展開し、 **aspnetTest**データベースを選択します。次に、 **[プロパティ]** ウィンドウで、**接続文字列**の値をコピーします。</span><span class="sxs-lookup"><span data-stu-id="943ba-190">In **Server Explorer**, expand **Data Connections** and select the **aspnetTest** database, then from the **Properties** window copy the **Connection String** value.</span></span>

![aspnet_connection_string_in_Server_Explorer](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image7.png)

<span data-ttu-id="943ba-192">ここでは、同じ接続文字列が再現されます。</span><span class="sxs-lookup"><span data-stu-id="943ba-192">The same connection string is reproduced here:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample2.cmd)]

<span data-ttu-id="943ba-193">この接続文字列をコピーし、 **[SQL のパッケージ化/発行]** タブの **[転送先データベースの接続文字列]** に貼り付けます。</span><span class="sxs-lookup"><span data-stu-id="943ba-193">Copy and paste this connection string into **Connection string for destination database** in the **Package/Publish SQL** tab.</span></span>

<span data-ttu-id="943ba-194">**[既存のデータベースからデータまたはスキーマをプル**する] が選択されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="943ba-194">Make sure that **Pull data and/or schema from an existing database** is selected.</span></span> <span data-ttu-id="943ba-195">これにより、SQL スクリプトが自動的に生成され、転送先データベースで実行されます。</span><span class="sxs-lookup"><span data-stu-id="943ba-195">This is what causes SQL scripts to be automatically generated and run in the destination database.</span></span>

<span data-ttu-id="943ba-196">\**ソースデータベースの値の接続文字列\*\*\*は、web.config ファイルから*抽出され、開発 SQL Server Compact データベースを指します。</span><span class="sxs-lookup"><span data-stu-id="943ba-196">The **Connection string for the source database** value is extracted from the *Web.config* file and points to the development SQL Server Compact database.</span></span> <span data-ttu-id="943ba-197">これは、変換先データベースで後で実行されるスクリプトを生成するために使用されるソースデータベースです。</span><span class="sxs-lookup"><span data-stu-id="943ba-197">This is the source database that will be used to generate the scripts that will run later in the destination database.</span></span> <span data-ttu-id="943ba-198">データベースの実稼働バージョンを配置するため、"aspnet-Dev" を "aspnet-Prod" に変更します。</span><span class="sxs-lookup"><span data-stu-id="943ba-198">Since you want to deploy the production version of the database, change "aspnet-Dev.sdf" to "aspnet-Prod.sdf".</span></span>

<span data-ttu-id="943ba-199">データ (ユーザーアカウントとロール) とデータベース構造をコピーする必要があるので、**データベーススクリプト作成オプション**をスキーマから**スキーマおよびデータ**に**のみ**変更します。</span><span class="sxs-lookup"><span data-stu-id="943ba-199">Change **Database scripting options** from **Schema Only** to **Schema and data**, since you want to copy your data (user accounts and roles) as well as the database structure.</span></span>

<span data-ttu-id="943ba-200">以前に作成した許可スクリプトを実行するように配置を構成するには、 **[データベーススクリプト]** セクションに追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="943ba-200">To configure deployment to run the grant scripts that you created earlier, you have to add them to the **Database Scripts** section.</span></span> <span data-ttu-id="943ba-201">**[スクリプトの追加]** をクリックし、 **[SQL スクリプトの追加]** ダイアログボックスで、grant スクリプトを保存したフォルダーに移動します (これは、ソリューションファイルが格納されているフォルダーです)。</span><span class="sxs-lookup"><span data-stu-id="943ba-201">Click **Add Script**, and in the **Add SQL Scripts** dialog box, navigate to the folder where you stored the grant script (this is the folder that contains your solution file).</span></span> <span data-ttu-id="943ba-202">*Grant .sql*という名前のファイルを選択し、 **[開く]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="943ba-202">Select the file named *Grant.sql*, and click **Open**.</span></span>

<span data-ttu-id="943ba-203">[![Select_File_dialog_box_grant_script](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image9.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="943ba-203">[![Select_File_dialog_box_grant_script](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image9.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image8.png)</span></span>

<span data-ttu-id="943ba-204">**データベースエントリ**の**Defaultconnection-デプロイ**行の設定は、次の図のようになります。</span><span class="sxs-lookup"><span data-stu-id="943ba-204">The settings for the **DefaultConnection-Deployment** row in **Database Entries** now look like the following illustration:</span></span>

![Database_Entry_Details_for_DefaultConnection_Test](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image10.png)

### <a name="configuring-deployment-settings-for-the-school-database"></a><span data-ttu-id="943ba-206">School データベースの展開設定を構成する</span><span class="sxs-lookup"><span data-stu-id="943ba-206">Configuring Deployment Settings for the School Database</span></span>

<span data-ttu-id="943ba-207">次に、 **[データベースエントリ]** テーブルの**schoolcontext.cs**行を選択して、School データベースの配置設定を構成します。</span><span class="sxs-lookup"><span data-stu-id="943ba-207">Next, select the **SchoolContext-Deployment** row in the **Database Entries** table in order to configure deployment settings for the School database.</span></span>

<span data-ttu-id="943ba-208">前に使用したのと同じ方法を使用して、新しい SQL Server Express データベースの接続文字列を取得できます。</span><span class="sxs-lookup"><span data-stu-id="943ba-208">You can use the same method you used earlier to get the connection string for the new SQL Server Express database.</span></span> <span data-ttu-id="943ba-209">**[SQL のパッケージ化/発行]** タブで、この接続文字列を**転送先データベースの接続文字列**にコピーします。</span><span class="sxs-lookup"><span data-stu-id="943ba-209">Copy this connection string into **Connection string for destination database** in the **Package/Publish SQL** tab.</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample3.cmd)]

<span data-ttu-id="943ba-210">**[既存のデータベースからデータまたはスキーマをプル**する] が選択されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="943ba-210">Make sure that **Pull data and/or schema from an existing database** is selected.</span></span>

<span data-ttu-id="943ba-211">\**ソースデータベースの値の接続文字列\*\*\*は、web.config ファイルから*抽出され、開発 SQL Server Compact データベースを指します。</span><span class="sxs-lookup"><span data-stu-id="943ba-211">The **Connection string for the source database** value is extracted from the *Web.config* file and points to the development SQL Server Compact database.</span></span> <span data-ttu-id="943ba-212">"School-Dev" を "School-Prod" に変更して、データベースの実稼働バージョンを展開します。</span><span class="sxs-lookup"><span data-stu-id="943ba-212">Change "School-Dev.sdf" to "School-Prod.sdf" to deploy the production version of the database.</span></span> <span data-ttu-id="943ba-213">(App\_Data フォルダーに School-Prod ファイルを作成したことはありません。そのため、後で ContosoUniversity プロジェクトフォルダー内の App\_Data フォルダーにそのファイルをテスト環境からコピーします)。</span><span class="sxs-lookup"><span data-stu-id="943ba-213">(You never created a School-Prod.sdf file in the App\_Data folder, so you'll copy that file from the test environment to the App\_Data folder in the ContosoUniversity project folder later.)</span></span>

<span data-ttu-id="943ba-214">**データベーススクリプト作成オプション**を**スキーマおよびデータ**に変更します。</span><span class="sxs-lookup"><span data-stu-id="943ba-214">Change **Database scripting options** to **Schema and data**.</span></span>

<span data-ttu-id="943ba-215">また、スクリプトを実行して、このデータベースに対する読み取りと書き込みのアクセス許可をアプリケーションプール id に付与する必要があります。そのため、メンバーシップデータベースの場合と同様に、 *grant .sql*スクリプトファイルを追加します。</span><span class="sxs-lookup"><span data-stu-id="943ba-215">You also want to run the script to grant read and write permission for this database to the application pool identity, so add the *Grant.sql* script file as you did for the membership database.</span></span>

<span data-ttu-id="943ba-216">完了すると、**データベースエントリ**の**schoolcontext.cs**行の設定は次の図のようになります。</span><span class="sxs-lookup"><span data-stu-id="943ba-216">When you're done, the settings for the **SchoolContext-Deployment** row in **Database Entries** look like the following illustration:</span></span>

![Database_Entry_Details_for_SchoolContext_Test](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image11.png)

<span data-ttu-id="943ba-218">**[SQL のパッケージ化/発行]** タブへの変更を保存します。</span><span class="sxs-lookup"><span data-stu-id="943ba-218">Save the changes to the **Package/Publish SQL** tab.</span></span>

<span data-ttu-id="943ba-219">*C:\inetpub\wwwroot\ContosoUniversity\App\_data*フォルダーの*School-Prod*ファイルを、ContosoUniversity プロジェクトの*App\_data*フォルダーにコピーします。</span><span class="sxs-lookup"><span data-stu-id="943ba-219">Copy the *School-Prod.sdf* file from the *c:\inetpub\wwwroot\ContosoUniversity\App\_Data* folder to the *App\_Data* folder in the ContosoUniversity project.</span></span>

### <a name="specifying-transacted-mode-for-the-grant-script"></a><span data-ttu-id="943ba-220">Grant スクリプトのトランザクションモードの指定</span><span class="sxs-lookup"><span data-stu-id="943ba-220">Specifying Transacted Mode for the Grant Script</span></span>

<span data-ttu-id="943ba-221">配置プロセスでは、データベーススキーマとデータを配置するスクリプトが生成されます。</span><span class="sxs-lookup"><span data-stu-id="943ba-221">The deployment process generates scripts that deploy the database schema and data.</span></span> <span data-ttu-id="943ba-222">既定では、これらのスクリプトはトランザクション内で実行されます。</span><span class="sxs-lookup"><span data-stu-id="943ba-222">By default, these scripts run in a transaction.</span></span> <span data-ttu-id="943ba-223">ただし、既定では、カスタムスクリプト (grant スクリプトなど) はトランザクションでは実行されません。</span><span class="sxs-lookup"><span data-stu-id="943ba-223">However, custom scripts (like the grant scripts) by default do not run in a transaction.</span></span> <span data-ttu-id="943ba-224">配置プロセスでトランザクションモードが混在している場合、配置中にスクリプトを実行すると、タイムアウトエラーが発生することがあります。</span><span class="sxs-lookup"><span data-stu-id="943ba-224">If the deployment process mixes transaction modes, you might get a timeout error when the scripts run during deployment.</span></span> <span data-ttu-id="943ba-225">このセクションでは、トランザクションで実行するカスタムスクリプトを構成するために、プロジェクトファイルを編集します。</span><span class="sxs-lookup"><span data-stu-id="943ba-225">In this section, you edit the project file in order to configure the custom scripts to run in a transaction.</span></span>

<span data-ttu-id="943ba-226">**ソリューションエクスプローラー**で、 **ContosoUniversity**プロジェクトを右クリックし、 **[プロジェクトのアンロード]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="943ba-226">In **Solution Explorer**, right-click the **ContosoUniversity** project and select **Unload Project**.</span></span>

![Unload_Project_in_Solution_Explorer](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image12.png)

<span data-ttu-id="943ba-228">次に、プロジェクトを再び右クリックし、 **[Edit ContosoUniversity]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="943ba-228">Then right-click the project again and select **Edit ContosoUniversity.csproj**.</span></span>

![Edit_Project_in_Solution_Explorer](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image13.png)

<span data-ttu-id="943ba-230">Visual Studio エディターには、プロジェクトファイルの XML コンテンツが表示されます。</span><span class="sxs-lookup"><span data-stu-id="943ba-230">The Visual Studio editor shows you the XML content of the project file.</span></span> <span data-ttu-id="943ba-231">`PropertyGroup` 要素がいくつかあることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="943ba-231">Notice that there are several `PropertyGroup` elements.</span></span> <span data-ttu-id="943ba-232">(イメージでは、`PropertyGroup` 要素の内容は省略されています)。</span><span class="sxs-lookup"><span data-stu-id="943ba-232">(In the image, the contents of the `PropertyGroup` elements have been omitted.)</span></span>

![プロジェクトファイルエディターウィンドウ](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image15.png)

<span data-ttu-id="943ba-234">最初の1つは、`Condition` 属性を持たないもので、ビルド構成に関係なく適用される設定です。</span><span class="sxs-lookup"><span data-stu-id="943ba-234">The first one, which has no `Condition` attribute, is for settings that apply regardless of build configuration.</span></span> <span data-ttu-id="943ba-235">1つの `PropertyGroup` 要素は、デバッグビルド構成にのみ適用されます (`Condition` 属性に注意してください)。1つはリリースビルド構成にのみ適用され、もう1つはテストビルド構成にのみ適用されます。</span><span class="sxs-lookup"><span data-stu-id="943ba-235">One `PropertyGroup` element applies only to the Debug build configuration (note the `Condition` attribute), one applies only to the Release build configuration, and one applies only to the Test build configuration.</span></span> <span data-ttu-id="943ba-236">リリースビルド構成の `PropertyGroup` 要素内に、 **[SQL のパッケージ化/発行]** タブで入力した設定を含む `PublishDatabaseSettings` 要素が表示されます。指定した各 grant スクリプトに対応する `Object` 要素があります ("Grant .sql" の2つのインスタンスに注意してください)。</span><span class="sxs-lookup"><span data-stu-id="943ba-236">Within the `PropertyGroup` element for the Release build configuration, you'll see a `PublishDatabaseSettings` element that contains the settings you entered on the **Package/Publish SQL** tab. There is an `Object` element that corresponds to each of the grant scripts you specified (notice the two instances of "Grant.sql").</span></span> <span data-ttu-id="943ba-237">既定では、各 grant スクリプトの `Source` 要素の `Transacted` 属性は `False`です。</span><span class="sxs-lookup"><span data-stu-id="943ba-237">By default, the `Transacted` attribute of the `Source` element for each grant script is `False`.</span></span>

![Transacted_false](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image16.png)

<span data-ttu-id="943ba-239">`Source` 要素の `Transacted` 属性の値を `True`に変更します。</span><span class="sxs-lookup"><span data-stu-id="943ba-239">Change the value of the `Transacted` attribute of the `Source` element to `True`.</span></span>

![Transacted_true](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image17.png)

<span data-ttu-id="943ba-241">プロジェクトファイルを保存して閉じ、**ソリューションエクスプローラー**でプロジェクトを右クリックして、 **[プロジェクトの再読み込み]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="943ba-241">Save and close the project file, and then right-click the project in **Solution Explorer** and select **Reload Project**.</span></span>

![Reload_project](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image18.png)

## <a name="setting-up-webconfig-transformations-for-the-connection-strings"></a><span data-ttu-id="943ba-243">接続文字列の web.config 変換の設定</span><span class="sxs-lookup"><span data-stu-id="943ba-243">Setting up Web.Config Transformations for the Connection Strings</span></span>

<span data-ttu-id="943ba-244">**[Sql のパッケージ化/発行]** タブで入力した新しい sql Express データベースの接続文字列は、配置時に移行先データベースを更新する場合にのみ Web 配置によって使用されます。</span><span class="sxs-lookup"><span data-stu-id="943ba-244">The connection strings for the new SQL Express databases that you entered on the **Package/Publish SQL** tab are used by Web Deploy only for updating the destination database during deployment.</span></span> <span data-ttu-id="943ba-245">*配置された web.config ファイル*内の接続文字列が新しい SQL Server Express データベースを指すように *、web.config の変換を*設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="943ba-245">You still have to set up *Web.config* transformations so that the connection strings in the deployed *Web.config* file point to the new SQL Server Express databases.</span></span> <span data-ttu-id="943ba-246">( **[SQL のパッケージ化/発行]** タブを使用する場合、発行プロファイルで接続文字列を構成することはできません)。</span><span class="sxs-lookup"><span data-stu-id="943ba-246">(When you use the **Package/Publish SQL** tab, you can't configure connection strings in the publish profile.)</span></span>

<span data-ttu-id="943ba-247">Web.config*を開き、* `connectionStrings` 要素を次の例の `connectionStrings` 要素に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="943ba-247">Open *Web.Test.config* and replace the `connectionStrings` element with the `connectionStrings` element in the following example.</span></span> <span data-ttu-id="943ba-248">(コンテキストを提供するためにここに示されている周囲のコードではなく、connectionStrings 要素のみをコピーするようにしてください)。</span><span class="sxs-lookup"><span data-stu-id="943ba-248">(Make sure you only copy the connectionStrings element, not the surrounding code that is shown here to provide context.)</span></span>

[!code-xml[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample4.xml?highlight=2-11)]

<span data-ttu-id="943ba-249">このコードにより、配置された*web.config*ファイルで、各 `add` 要素の `connectionString` と `providerName` 属性が置き換えられます。</span><span class="sxs-lookup"><span data-stu-id="943ba-249">This code causes the `connectionString` and `providerName` attributes of each `add` element to be replaced in the deployed *Web.config* file.</span></span> <span data-ttu-id="943ba-250">これらの接続文字列は、 **[SQL のパッケージ化/発行]** タブで入力したものと同じではありません。Entity Framework とユニバーサルプロバイダーに必要なため、設定 "MultipleActiveResultSets = True" が追加されました。</span><span class="sxs-lookup"><span data-stu-id="943ba-250">These connection strings are not identical to the ones you entered in the **Package/Publish SQL** tab. The setting "MultipleActiveResultSets=True" has been added to them because it's required for the Entity Framework and the Universal Providers.</span></span>

## <a name="installing-sql-server-compact"></a><span data-ttu-id="943ba-251">SQL Server Compact のインストール</span><span class="sxs-lookup"><span data-stu-id="943ba-251">Installing SQL Server Compact</span></span>

<span data-ttu-id="943ba-252">SqlServerCompact NuGet パッケージには、Contoso 大学アプリケーション用の SQL Server Compact データベースエンジンアセンブリが用意されています。</span><span class="sxs-lookup"><span data-stu-id="943ba-252">The SqlServerCompact NuGet package provides the SQL Server Compact database engine assemblies for the Contoso University application.</span></span> <span data-ttu-id="943ba-253">ただし現在は、SQL Server データベースで実行するスクリプトを作成するために、SQL Server Compact データベースを読み取ることができる Web 配置アプリケーションではありません。</span><span class="sxs-lookup"><span data-stu-id="943ba-253">But now it is not the application but Web Deploy that must be able to read the SQL Server Compact databases, in order to create scripts to run in the SQL Server databases.</span></span> <span data-ttu-id="943ba-254">Web 配置が SQL Server Compact データベースを読み取ることができるようにするには、 [Microsoft SQL Server Compact 4.0](https://www.microsoft.com/downloads/details.aspx?FamilyID=15F7C9B3-A150-4AD2-823E-E4E0DCF85DF6)のリンクを使用して開発用コンピューターに SQL Server Compact をインストールします。</span><span class="sxs-lookup"><span data-stu-id="943ba-254">To enable Web Deploy to read SQL Server Compact databases, install SQL Server Compact on the development computer by using the following link: [Microsoft SQL Server Compact 4.0](https://www.microsoft.com/downloads/details.aspx?FamilyID=15F7C9B3-A150-4AD2-823E-E4E0DCF85DF6).</span></span>

## <a name="deploying-to-the-test-environment"></a><span data-ttu-id="943ba-255">テスト環境への配置</span><span class="sxs-lookup"><span data-stu-id="943ba-255">Deploying to the Test Environment</span></span>

<span data-ttu-id="943ba-256">テスト環境に発行するには、発行プロファイルデータベースの設定ではなく、データベースの発行の **[SQL のパッケージ化/発行]** タブを使用するように構成された発行プロファイルを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="943ba-256">In order to publish to the Test environment, you have to create a publish profile that is configured to use the **Package/Publish SQL** tab for database publishing instead of the publish profile database settings.</span></span>

<span data-ttu-id="943ba-257">まず、既存のテストプロファイルを削除します。</span><span class="sxs-lookup"><span data-stu-id="943ba-257">First, delete the existing Test profile.</span></span>

<span data-ttu-id="943ba-258">**ソリューションエクスプローラー**で、ContosoUniversity プロジェクトを右クリックし、 **[発行]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="943ba-258">In **Solution Explorer**, right-click the ContosoUniversity project, and click **Publish**.</span></span>

<span data-ttu-id="943ba-259">**[プロファイル]** タブを選択します。</span><span class="sxs-lookup"><span data-stu-id="943ba-259">Select the **Profile** tab.</span></span>

<span data-ttu-id="943ba-260">**[プロファイルの管理]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="943ba-260">Click **Manage Profiles**.</span></span>

<span data-ttu-id="943ba-261">**[テスト]** を選択し、 **[削除]** をクリックして、 **[閉じる]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="943ba-261">Select **Test**, click **Remove**, and then click **Close**.</span></span>

<span data-ttu-id="943ba-262">この変更を保存するには、 **Web の発行**ウィザードを閉じます。</span><span class="sxs-lookup"><span data-stu-id="943ba-262">Close the **Publish Web** wizard to save this change.</span></span>

<span data-ttu-id="943ba-263">次に、新しいテストプロファイルを作成し、それを使用してプロジェクトを発行します。</span><span class="sxs-lookup"><span data-stu-id="943ba-263">Next, create a new Test profile and use it to publish the project.</span></span>

<span data-ttu-id="943ba-264">**ソリューションエクスプローラー**で、ContosoUniversity プロジェクトを右クリックし、 **[発行]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="943ba-264">In **Solution Explorer**, right-click the ContosoUniversity project, and click **Publish**.</span></span>

<span data-ttu-id="943ba-265">**[プロファイル]** タブを選択します。</span><span class="sxs-lookup"><span data-stu-id="943ba-265">Select the **Profile** tab.</span></span>

<span data-ttu-id="943ba-266">ドロップダウンリストから  **&lt;新規作成...&gt;** を選択し、プロファイル名として「Test」と入力します。</span><span class="sxs-lookup"><span data-stu-id="943ba-266">Select **&lt;New...&gt;** from the drop-down list, and enter "Test" as the profile name.</span></span>

<span data-ttu-id="943ba-267">**[サービス URL]** ボックスに、「 *localhost*」と入力します。</span><span class="sxs-lookup"><span data-stu-id="943ba-267">In the **Service URL** box, enter *localhost*.</span></span>

<span data-ttu-id="943ba-268">**[サイト/アプリケーション]** ボックスに、「 *Default Web Site/ContosoUniversity」と*入力します。</span><span class="sxs-lookup"><span data-stu-id="943ba-268">In the **Site/application** box, enter *Default Web Site/ContosoUniversity*.</span></span>

<span data-ttu-id="943ba-269">**[宛先 URL]** ボックスに、「`http://localhost/ContosoUniversity/`」と入力します。</span><span class="sxs-lookup"><span data-stu-id="943ba-269">In the **Destination URL** box, enter `http://localhost/ContosoUniversity/`.</span></span>

<span data-ttu-id="943ba-270">**[次へ]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="943ba-270">Click **Next**.</span></span>

<span data-ttu-id="943ba-271">**設定** タブには、**SQL のパッケージ化/発行** タブが構成されていることが警告され、新しいデータベースの公開の強化を有効にする をクリックして上書きすることができます。</span><span class="sxs-lookup"><span data-stu-id="943ba-271">The **Settings** tab warns you that the **Package/Publish SQL** tab has been configured, and it gives you an opportunity to override them by clicking enable the new database publishing improvements.</span></span> <span data-ttu-id="943ba-272">このデプロイでは、 **[SQL のパッケージ化/発行]** タブの設定を上書きしないため、 **[次へ]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="943ba-272">For this deployment you don't want to override the **Package/Publish SQL** tab settings, so just click **Next**.</span></span>

![Publish_Web_wizard_Settings_tab_Migrate](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image19.png)

<span data-ttu-id="943ba-274">**[プレビュー]** タブには、**パブリッシュするデータベースが選択**されていないことを示すメッセージが表示されますが、これは、データベースの発行が発行プロファイルで構成されていないことを意味します。</span><span class="sxs-lookup"><span data-stu-id="943ba-274">A message on the **Preview** tab indicates that **No databases are selected to publish**, but this only means that database publishing is not configured in the publish profile.</span></span>

<span data-ttu-id="943ba-275">**[発行]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="943ba-275">Click **Publish**.</span></span>

![Publish_Web_wizard_Preview_tab_Migrate](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image20.png)

<span data-ttu-id="943ba-277">Visual Studio によってアプリケーションが配置され、テスト環境のサイトのホームページにブラウザーが開かれます。</span><span class="sxs-lookup"><span data-stu-id="943ba-277">Visual Studio deploys the application and opens the browser to the home page of the site in the test environment.</span></span> <span data-ttu-id="943ba-278">インストラクターページを実行して、前に見たものと同じデータが表示されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="943ba-278">Run the Instructors page to see that it displays the same data that you saw earlier.</span></span> <span data-ttu-id="943ba-279">**[学生の追加]** ページを実行し、新しい学生を追加して、 **[students]** ページで新しい学生を表示します。</span><span class="sxs-lookup"><span data-stu-id="943ba-279">Run the **Add Students** page, add a new student, and then view the new student in the **Students** page.</span></span> <span data-ttu-id="943ba-280">これにより、データベースを更新できるかどうかが確認されます。</span><span class="sxs-lookup"><span data-stu-id="943ba-280">This verifies that the you can update the database.</span></span> <span data-ttu-id="943ba-281">**[更新プログラムのクレジット]** ページ (ログインする必要があります) を選択して、メンバーシップデータベースが展開されていて、それにアクセスできることを確認します。</span><span class="sxs-lookup"><span data-stu-id="943ba-281">Select the **Update Credits** page (you'll need to log in) to verify that the membership database was deployed and you have access to it.</span></span>

## <a name="creating-a-sql-server-database-for-the-production-environment"></a><span data-ttu-id="943ba-282">運用環境用の SQL Server データベースの作成</span><span class="sxs-lookup"><span data-stu-id="943ba-282">Creating a SQL Server Database for the Production Environment</span></span>

<span data-ttu-id="943ba-283">テスト環境にデプロイしたので、運用環境へのデプロイをセットアップする準備ができました。</span><span class="sxs-lookup"><span data-stu-id="943ba-283">Now that you've deployed to the test environment, you're ready to set up deployment to production.</span></span> <span data-ttu-id="943ba-284">テスト環境の場合は、配置先のデータベースを作成することによって開始します。</span><span class="sxs-lookup"><span data-stu-id="943ba-284">You begin as you did for the test environment, by creating a database to deploy to.</span></span> <span data-ttu-id="943ba-285">概要を思い出してください。 Cytanium Lite ホスティングプランでは、単一の SQL Server データベースのみが許可されているため、2つではなく、データベースを1つだけ設定します。</span><span class="sxs-lookup"><span data-stu-id="943ba-285">As you recall from the Overview, the Cytanium Lite hosting plan only allows a single SQL Server database, so you will set up only one database, not two.</span></span> <span data-ttu-id="943ba-286">メンバーシップと学校 SQL Server Compact データベースのすべてのテーブルとデータは、運用環境の1つの SQL Server データベースにデプロイされます。</span><span class="sxs-lookup"><span data-stu-id="943ba-286">All of the tables and data from the membership and School SQL Server Compact databases will be deployed into one SQL Server database in production.</span></span>

<span data-ttu-id="943ba-287">[http://panel.cytanium.com](http://panel.cytanium.com)の Cytanium コントロールパネルにアクセスします。</span><span class="sxs-lookup"><span data-stu-id="943ba-287">Go to the Cytanium control panel at [http://panel.cytanium.com](http://panel.cytanium.com).</span></span> <span data-ttu-id="943ba-288">**データベース**上にマウスポインターを置き、 **[SQL Server 2008]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="943ba-288">Hold the mouse over **Databases** and then click **SQL Server 2008**.</span></span>

<span data-ttu-id="943ba-289">[![Selecting_Databases_in_Control_Panel](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image22.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image21.png)</span><span class="sxs-lookup"><span data-stu-id="943ba-289">[![Selecting_Databases_in_Control_Panel](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image22.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image21.png)</span></span>

<span data-ttu-id="943ba-290">**[SQL Server 2008]** ページで、 **[データベースの作成]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="943ba-290">In the **SQL Server 2008** page, click **Create Database**.</span></span>

<span data-ttu-id="943ba-291">[![Selecting_Create_Database](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image24.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image23.png)</span><span class="sxs-lookup"><span data-stu-id="943ba-291">[![Selecting_Create_Database](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image24.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image23.png)</span></span>

<span data-ttu-id="943ba-292">データベースに "School" という名前を付け、 **[保存]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="943ba-292">Name the database "School" and click **Save**.</span></span> <span data-ttu-id="943ba-293">(このページではプレフィックス "contosouSchool" が自動的に追加されるため、有効な名前は "" になります)。</span><span class="sxs-lookup"><span data-stu-id="943ba-293">(The page automatically adds the prefix "contosou", so the effective name will be "contosouSchool".)</span></span>

<span data-ttu-id="943ba-294">[![Naming_the_database](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image26.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image25.png)</span><span class="sxs-lookup"><span data-stu-id="943ba-294">[![Naming_the_database](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image26.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image25.png)</span></span>

<span data-ttu-id="943ba-295">同じページで、 **[ユーザーの作成]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="943ba-295">On the same page, click **Create User**.</span></span> <span data-ttu-id="943ba-296">Cytanium のサーバーでは、統合 Windows セキュリティを使用するのではなく、アプリケーションプールの id でデータベースを開いて、データベースを開く権限を持つユーザーを作成します。</span><span class="sxs-lookup"><span data-stu-id="943ba-296">On Cytanium's servers, rather than using integrated Windows security and letting the application pool identity open your database, you'll create a user that has authority to open your database.</span></span> <span data-ttu-id="943ba-297">ユーザーの資格情報を、実稼働の*web.config*ファイルにある接続文字列に追加します。</span><span class="sxs-lookup"><span data-stu-id="943ba-297">You'll add the user's credentials to the connection strings that go in the production *Web.config* file.</span></span> <span data-ttu-id="943ba-298">この手順では、これらの資格情報を作成します。</span><span class="sxs-lookup"><span data-stu-id="943ba-298">In this step you create those credentials.</span></span>

<span data-ttu-id="943ba-299">[![Creating_a_database_user](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image28.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image27.png)</span><span class="sxs-lookup"><span data-stu-id="943ba-299">[![Creating_a_database_user](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image28.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image27.png)</span></span>

<span data-ttu-id="943ba-300">**[SQL ユーザーのプロパティ]** ページで、必要なフィールドを入力します。</span><span class="sxs-lookup"><span data-stu-id="943ba-300">Fill in the required fields in the **SQL User Properties** page:</span></span>

- <span data-ttu-id="943ba-301">名前として「ユーザー」と入力します。</span><span class="sxs-lookup"><span data-stu-id="943ba-301">Enter "ContosoUniversityUser" as the name.</span></span>
- <span data-ttu-id="943ba-302">パスワードを入力します。</span><span class="sxs-lookup"><span data-stu-id="943ba-302">Enter a password.</span></span>
- <span data-ttu-id="943ba-303">既定のデータベースとして **[contosouSchool]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="943ba-303">Select **contosouSchool** as the default database.</span></span>
- <span data-ttu-id="943ba-304">**[ContosouSchool]** チェックボックスをオンにします。</span><span class="sxs-lookup"><span data-stu-id="943ba-304">Select the **contosouSchool** check box.</span></span>

<span data-ttu-id="943ba-305">[![SQL_User_Properties_page](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image30.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image29.png)</span><span class="sxs-lookup"><span data-stu-id="943ba-305">[![SQL_User_Properties_page](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image30.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image29.png)</span></span>

## <a name="configuring-database-deployment-for-the-production-environment"></a><span data-ttu-id="943ba-306">運用環境のデータベース配置の構成</span><span class="sxs-lookup"><span data-stu-id="943ba-306">Configuring Database Deployment for the Production Environment</span></span>

<span data-ttu-id="943ba-307">これで、前にテスト環境で行ったように、 **[SQL のパッケージ化/発行]** タブでデータベース配置設定を設定できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="943ba-307">Now you're ready to set up database deployment settings in the **Package/Publish SQL** tab, as you did earlier for the test environment.</span></span>

<span data-ttu-id="943ba-308">プロジェクトの**プロパティ**ウィンドウを開き、 **[SQL のパッケージ化/発行]** タブを選択し、 **[構成]** ドロップダウンリストで **[アクティブ (リリース)]** または **[リリース]** が選択されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="943ba-308">Open the **Project Properties** window, select the **Package/Publish SQL** tab, and make sure that **Active (Release)** or **Release** is selected in the **Configuration** drop-down list.</span></span>

<span data-ttu-id="943ba-309">各データベースの配置設定を構成する場合、運用環境とテスト環境の間の主な違いは、接続文字列の構成方法です。</span><span class="sxs-lookup"><span data-stu-id="943ba-309">When you configure deployment settings for each database, the key difference between what you do for production and test environments is in how you configure connection strings.</span></span> <span data-ttu-id="943ba-310">テスト環境では、複数の変換先データベースの接続文字列を入力しましたが、運用環境では、両方のデータベースで同期先接続文字列が同じになります。</span><span class="sxs-lookup"><span data-stu-id="943ba-310">For the test environment you entered different destination database connection strings, but for the production environment the destination connection string will be the same for both databases.</span></span> <span data-ttu-id="943ba-311">これは、両方のデータベースを運用環境の1つのデータベースに配置するためです。</span><span class="sxs-lookup"><span data-stu-id="943ba-311">This is because you are deploying both databases to one database in production.</span></span>

### <a name="configuring-deployment-settings-for-the-membership-database"></a><span data-ttu-id="943ba-312">メンバーシップデータベースの配置設定の構成</span><span class="sxs-lookup"><span data-stu-id="943ba-312">Configuring Deployment Settings for the Membership Database</span></span>

<span data-ttu-id="943ba-313">メンバーシップデータベースに適用される設定を構成するには、**データベースエントリ**テーブルで**Defaultconnection-Deployment**行を選択します。</span><span class="sxs-lookup"><span data-stu-id="943ba-313">To configure settings that apply to the membership database, select the **DefaultConnection-Deployment** row in the **Database Entries** table.</span></span>

<span data-ttu-id="943ba-314">**[転送先データベースの接続文字列]** に、先ほど作成した新しい実稼働 SQL Server データベースを指す接続文字列を入力します。</span><span class="sxs-lookup"><span data-stu-id="943ba-314">In **Connection string for destination database**, enter a connection string that points to the new production SQL Server database that you just created.</span></span> <span data-ttu-id="943ba-315">ウェルカムメールから接続文字列を取得できます。</span><span class="sxs-lookup"><span data-stu-id="943ba-315">You can get the connection string from your welcome email.</span></span> <span data-ttu-id="943ba-316">電子メールの関連部分には、次のサンプルの接続文字列が含まれています。</span><span class="sxs-lookup"><span data-stu-id="943ba-316">The relevant part of the email contains the following sample connection string:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample5.cmd)]

<span data-ttu-id="943ba-317">3つの変数を置き換えた後、必要な接続文字列は次の例のようになります。</span><span class="sxs-lookup"><span data-stu-id="943ba-317">After you replace the three variables, the connection string you need looks like this example:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample6.cmd)]

<span data-ttu-id="943ba-318">この接続文字列をコピーし、 **[SQL のパッケージ化/発行]** タブの **[転送先データベースの接続文字列]** に貼り付けます。</span><span class="sxs-lookup"><span data-stu-id="943ba-318">Copy and paste this connection string into **Connection string for destination database** in the **Package/Publish SQL** tab.</span></span>

<span data-ttu-id="943ba-319">**既存のデータベースからのデータまたはスキーマのプル**がまだ選択されていること、および**データベーススクリプト作成オプション**がまだ**スキーマとデータ**であることを確認します。</span><span class="sxs-lookup"><span data-stu-id="943ba-319">Make sure that **Pull data and/or schema from an existing database** is still selected, and that **Database scripting options** is still **Schema and Data**.</span></span>

<span data-ttu-id="943ba-320">**[データベーススクリプト]** ボックスで、Grant .sql スクリプトの横にあるチェックボックスをオフにします。</span><span class="sxs-lookup"><span data-stu-id="943ba-320">In the **Database Scripts** box, clear the check box next to the Grant.sql script.</span></span>

![Disable_Grant_script](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image31.png)

### <a name="configuring-deployment-settings-for-the-school-database"></a><span data-ttu-id="943ba-322">School データベースの展開設定を構成する</span><span class="sxs-lookup"><span data-stu-id="943ba-322">Configuring Deployment Settings for the School Database</span></span>

<span data-ttu-id="943ba-323">次に、School データベースの設定を構成するために、 **[データベースエントリ]** テーブルの**schoolcontext.cs**行を選択します。</span><span class="sxs-lookup"><span data-stu-id="943ba-323">Next, select the **SchoolContext-Deployment** row in the **Database Entries** table in order to configure the School database settings.</span></span>

<span data-ttu-id="943ba-324">メンバーシップデータベースのフィールドにコピーしたコピー**先データベースの接続文字列**に、同じ接続文字列をコピーします。</span><span class="sxs-lookup"><span data-stu-id="943ba-324">Copy the same connection string into **Connection string for destination database** that you copied into that field for the membership database.</span></span>

<span data-ttu-id="943ba-325">**既存のデータベースからのデータまたはスキーマのプル**がまだ選択されていること、および**データベーススクリプト作成オプション**がまだ**スキーマとデータ**であることを確認します。</span><span class="sxs-lookup"><span data-stu-id="943ba-325">Make sure that **Pull data and/or schema from an existing database** is still selected, and that **Database scripting options** is still **Schema and Data**.</span></span>

<span data-ttu-id="943ba-326">**[データベーススクリプト]** ボックスで、Grant .sql スクリプトの横にあるチェックボックスをオフにします。</span><span class="sxs-lookup"><span data-stu-id="943ba-326">In the **Database Scripts** box, clear the check box next to the Grant.sql script.</span></span>

<span data-ttu-id="943ba-327">**[SQL のパッケージ化/発行]** タブへの変更を保存します。</span><span class="sxs-lookup"><span data-stu-id="943ba-327">Save the changes to the **Package/Publish SQL** tab.</span></span>

## <a name="setting-up-webconfig-transforms-for-the-connection-strings-to-production-databases"></a><span data-ttu-id="943ba-328">運用データベースへの接続文字列の Web.config 変換の設定</span><span class="sxs-lookup"><span data-stu-id="943ba-328">Setting Up Web.Config Transforms for the Connection Strings to Production Databases</span></span>

<span data-ttu-id="943ba-329">次に *、配置された web.config ファイル*内の接続文字列が新しい実稼働データベースを指すように*web.config 変換を設定します。*</span><span class="sxs-lookup"><span data-stu-id="943ba-329">Next, you'll set up *Web.config* transformations so that the connection strings in the deployed *Web.config* file to point to the new production database.</span></span> <span data-ttu-id="943ba-330">使用する Web 配置の **[SQL のパッケージ化/発行]** タブで入力した接続文字列は、`MultipleResultSets` オプションを追加する場合を除いて、アプリケーションで使用する必要がある接続文字列と同じです。</span><span class="sxs-lookup"><span data-stu-id="943ba-330">The connection string that you entered on the **Package/Publish SQL** tab for Web Deploy to use is the same as the one the application needs to use, except for the addition of the `MultipleResultSets` option.</span></span>

<span data-ttu-id="943ba-331">Web.config*を開き、* `connectionStrings` 要素を次の例のような `connectionStrings` 要素に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="943ba-331">Open *Web.Production.config* and replace the `connectionStrings` element with a `connectionStrings` element that looks like the following example.</span></span> <span data-ttu-id="943ba-332">(コンテキストを表示するために提供されているタグではなく、`connectionStrings` の要素のみをコピーします)。</span><span class="sxs-lookup"><span data-stu-id="943ba-332">(Only copy the `connectionStrings` element, not the surrounding tags that are provided to show the context.)</span></span>

[!code-xml[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample7.xml?highlight=2-11)]

<span data-ttu-id="943ba-333">*Web.config ファイルで*接続文字列を常に暗号化するように指示するアドバイスが表示されることがあります。</span><span class="sxs-lookup"><span data-stu-id="943ba-333">You sometimes see advice that tells you to always encrypt connection strings in the *Web.config* file.</span></span> <span data-ttu-id="943ba-334">これは、自社のネットワーク上のサーバーにを展開する場合に適しています。</span><span class="sxs-lookup"><span data-stu-id="943ba-334">This might be appropriate if you were deploying to servers on your own company's network.</span></span> <span data-ttu-id="943ba-335">ただし、共有ホスティング環境に配置する場合は、ホスティングプロバイダーのセキュリティプラクティスを信頼しているため、接続文字列を暗号化する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="943ba-335">When you are deploying to a shared hosting environment, though, you're trusting the security practices of the hosting provider, and it's not necessary or practical to encrypt the connection strings.</span></span>

## <a name="deploying-to-the-production-environment"></a><span data-ttu-id="943ba-336">運用環境への配置</span><span class="sxs-lookup"><span data-stu-id="943ba-336">Deploying to the Production Environment</span></span>

<span data-ttu-id="943ba-337">これで、運用環境にデプロイする準備ができました。</span><span class="sxs-lookup"><span data-stu-id="943ba-337">Now you're ready to deploy to production.</span></span> <span data-ttu-id="943ba-338">Web 配置は、プロジェクトの*アプリ\_data*フォルダー内の SQL Server Compact データベースを読み取り、すべてのテーブルとデータを運用環境の SQL Server データベースに再作成します。</span><span class="sxs-lookup"><span data-stu-id="943ba-338">Web Deploy will read the SQL Server Compact databases in your project's *App\_Data* folder and re-create all of their tables and data in the production SQL Server database.</span></span> <span data-ttu-id="943ba-339">**[Web のパッケージ化/発行]** タブ設定を使用して発行するには、運用環境用の新しい発行プロファイルを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="943ba-339">In order to publish by using the **Package/Publish Web** tab settings, you have to create a new publish profile for production.</span></span>

<span data-ttu-id="943ba-340">最初に、以前のテストプロファイルと同じように、既存の運用プロファイルを削除します。</span><span class="sxs-lookup"><span data-stu-id="943ba-340">First, delete the existing Production profile as you did the Test profile earlier.</span></span>

<span data-ttu-id="943ba-341">**ソリューションエクスプローラー**で、ContosoUniversity プロジェクトを右クリックし、 **[発行]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="943ba-341">In **Solution Explorer**, right-click the ContosoUniversity project, and click **Publish**.</span></span>

<span data-ttu-id="943ba-342">**[プロファイル]** タブを選択します。</span><span class="sxs-lookup"><span data-stu-id="943ba-342">Select the **Profile** tab.</span></span>

<span data-ttu-id="943ba-343">**[プロファイルの管理]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="943ba-343">Click **Manage Profiles**.</span></span>

<span data-ttu-id="943ba-344">**[運用]** を選択し、 **[削除]** をクリックして、 **[閉じる]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="943ba-344">Select **Production**, click **Remove**, and then click **Close**.</span></span>

<span data-ttu-id="943ba-345">この変更を保存するには、 **Web の発行**ウィザードを閉じます。</span><span class="sxs-lookup"><span data-stu-id="943ba-345">Close the **Publish Web** wizard to save this change.</span></span>

<span data-ttu-id="943ba-346">次に、新しい実稼働プロファイルを作成し、それを使用してプロジェクトを発行します。</span><span class="sxs-lookup"><span data-stu-id="943ba-346">Next, create a new Production profile and use it to publish the project.</span></span>

<span data-ttu-id="943ba-347">**ソリューションエクスプローラー**で、ContosoUniversity プロジェクトを右クリックし、 **[発行]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="943ba-347">In **Solution Explorer**, right-click the ContosoUniversity project, and click **Publish**.</span></span>

<span data-ttu-id="943ba-348">**[プロファイル]** タブを選択します。</span><span class="sxs-lookup"><span data-stu-id="943ba-348">Select the **Profile** tab.</span></span>

<span data-ttu-id="943ba-349">**[インポート]** をクリックし、前の手順でダウンロードした .publishsettings ファイルを選択します。</span><span class="sxs-lookup"><span data-stu-id="943ba-349">Click **Import**, and select the .publishsettings file that you downloaded earlier.</span></span>

<span data-ttu-id="943ba-350">**[接続]** タブで、**宛先 URL**を正しい一時 URL (この例では http://contosouniversity.com.vserver01.cytanium.com) に変更します。</span><span class="sxs-lookup"><span data-stu-id="943ba-350">On the **Connection** tab, change the **Destination URL** to the correct temporary URL, which in this example is http://contosouniversity.com.vserver01.cytanium.com.</span></span>

<span data-ttu-id="943ba-351">プロファイルの名前を運用環境に変更します。</span><span class="sxs-lookup"><span data-stu-id="943ba-351">Rename the profile to Production.</span></span> <span data-ttu-id="943ba-352">( **[プロファイル]** タブを選択し、 **[プロファイルの管理]** をクリックして実行します)。</span><span class="sxs-lookup"><span data-stu-id="943ba-352">(Select the **Profile** tab and click **Manage Profiles** to do that).</span></span>

<span data-ttu-id="943ba-353">Web の**発行**ウィザードを閉じて、変更を保存します。</span><span class="sxs-lookup"><span data-stu-id="943ba-353">Close the **Publish Web** wizard to save your changes.</span></span>

<span data-ttu-id="943ba-354">実稼働環境でデータベースが更新されている実際のアプリケーションでは、発行する前に、次の2つの手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="943ba-354">In a real application in which the database was being updated in production, you would do two additional steps now before you publish:</span></span>

1. <span data-ttu-id="943ba-355">「[運用環境へのデプロイ](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)」チュートリアルに示されているように、*アプリ\_offline .htm*をアップロードします。</span><span class="sxs-lookup"><span data-stu-id="943ba-355">Upload *app\_offline.htm*, as shown in the [Deploying to the Production Environment](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) tutorial.</span></span>
2. <span data-ttu-id="943ba-356">Cytanium コントロールパネルの**ファイルマネージャー**機能を使用して、 *Aspnet-Prod*ファイルと*School-Prod*ファイルを運用サイトから ContosoUniversity プロジェクトの*App\_Data*フォルダーにコピーします。</span><span class="sxs-lookup"><span data-stu-id="943ba-356">Use the **File Manager** feature of the Cytanium control panel to copy the *aspnet-Prod.sdf* and *School-Prod.sdf* files from the production site to the *App\_Data* folder of the ContosoUniversity project.</span></span> <span data-ttu-id="943ba-357">これにより、新しい SQL Server データベースに配置しているデータに、運用 web サイトによって行われた最新の更新が確実に含まれるようになります。</span><span class="sxs-lookup"><span data-stu-id="943ba-357">This ensures that the data you're deploying to the new SQL Server database includes the latest updates made by your production website.</span></span>

<span data-ttu-id="943ba-358">Web 上の **[発行**] ツールバーで、**運用**プロファイルが選択されていることを確認し、 **[発行]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="943ba-358">In the **Web One Click Publish** toolbar, make sure that the **Production** profile is selected, and then click **Publish**.</span></span>

<span data-ttu-id="943ba-359">発行する前に<em>\_offline .htm</em>をアップロードした場合は、Cytanium コントロールパネルの [<strong>ファイルマネージャー</strong> ] ユーティリティを使用して、<em>アプリ\_をオフライン</em>で削除する必要があります。をテストする前に、.htm を使用します。</span><span class="sxs-lookup"><span data-stu-id="943ba-359">If you uploaded <em>app\_offline.htm</em> before publishing, you have to use the <strong>File Manager</strong> utility in the Cytanium control panel to delete <em>app\_offline.</em>htm before you test.</span></span> <span data-ttu-id="943ba-360">また、<em>アプリ\_データ</em>フォルダーから<em>.sdf</em>ファイルを削除することもできます。</span><span class="sxs-lookup"><span data-stu-id="943ba-360">You can also at the same time delete the <em>.sdf</em> files from the <em>App\_Data</em> folder.</span></span>

<span data-ttu-id="943ba-361">これで、ブラウザーを開き、パブリックサイトの URL にアクセスして、テスト環境に配置した後と同じようにアプリケーションをテストできるようになりました。</span><span class="sxs-lookup"><span data-stu-id="943ba-361">You can now open a browser and go to the URL of your public site to test the application the same way you did after deploying to the test environment.</span></span>

## <a name="switching-to-sql-server-express-localdb-in-development"></a><span data-ttu-id="943ba-362">開発中の SQL Server Express LocalDB への切り替え</span><span class="sxs-lookup"><span data-stu-id="943ba-362">Switching to SQL Server Express LocalDB in Development</span></span>

<span data-ttu-id="943ba-363">概要で説明したように、通常は、テストおよび運用環境で使用する開発で同じデータベースエンジンを使用することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="943ba-363">As was explained in the Overview, it's generally best to use the same database engine in development that you use in test and production.</span></span> <span data-ttu-id="943ba-364">(開発環境で SQL Server Express を使用する利点は、開発環境、テスト環境、および運用環境でデータベースが同じように機能することです)。このセクションでは、Visual Studio からアプリケーションを実行するときに、LocalDB SQL Server Express を使用するように ContosoUniversity プロジェクトを設定します。</span><span class="sxs-lookup"><span data-stu-id="943ba-364">(Remember that the advantage to using SQL Server Express in development is that the database will work the same in your development, test, and production environments.) In this section you'll set up the ContosoUniversity project to use SQL Server Express LocalDB when you run the application from Visual Studio.</span></span>

<span data-ttu-id="943ba-365">この移行を実行する最も簡単な方法は、Code First して、メンバーシップシステムによって新しい開発データベースの両方を作成できるようにすることです。</span><span class="sxs-lookup"><span data-stu-id="943ba-365">The simplest way to perform this migration is to let Code First and the membership system create both new development databases for you.</span></span> <span data-ttu-id="943ba-366">この方法を移行に使用するには、次の3つの手順が必要です。</span><span class="sxs-lookup"><span data-stu-id="943ba-366">Using this method to migrate requires three steps:</span></span>

1. <span data-ttu-id="943ba-367">新しい SQL Express LocalDB データベースを指定するように接続文字列を変更します。</span><span class="sxs-lookup"><span data-stu-id="943ba-367">Change the connection strings to specify new SQL Express LocalDB databases.</span></span>
2. <span data-ttu-id="943ba-368">Web サイト管理ツールを実行して、管理者ユーザーを作成します。</span><span class="sxs-lookup"><span data-stu-id="943ba-368">Run the Web Site Administration Tool to create an administrator user.</span></span> <span data-ttu-id="943ba-369">これにより、メンバーシップデータベースが作成されます。</span><span class="sxs-lookup"><span data-stu-id="943ba-369">This creates the membership database.</span></span>
3. <span data-ttu-id="943ba-370">アプリケーションデータベースの作成とシードを行うには、Code First Migrations を使用します。</span><span class="sxs-lookup"><span data-stu-id="943ba-370">Use the Code First Migrations update-database command to create and seed the application database.</span></span>

### <a name="updating-connection-strings-in-the-webconfig-file"></a><span data-ttu-id="943ba-371">Web.config ファイル内の接続文字列の更新</span><span class="sxs-lookup"><span data-stu-id="943ba-371">Updating Connection Strings in the Web.config file</span></span>

<span data-ttu-id="943ba-372">*Web.config ファイルを*開き、`connectionStrings` 要素を次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="943ba-372">Open the *Web.config* file and replace the `connectionStrings` element with the following code:</span></span>

[!code-xml[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample8.xml)]

### <a name="creating-the-membership-database"></a><span data-ttu-id="943ba-373">メンバーシップデータベースの作成</span><span class="sxs-lookup"><span data-stu-id="943ba-373">Creating the Membership Database</span></span>

<span data-ttu-id="943ba-374">**ソリューションエクスプローラー**で、ContosoUniversity プロジェクトを選択し、 **[プロジェクト]** メニューの **[ASP.NET の構成]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="943ba-374">In **Solution Explorer**, select the ContosoUniversity project, and then click **ASP.NET Configuration** in the **Project** menu.</span></span>

<span data-ttu-id="943ba-375">[セキュリティ] タブをクリックします。</span><span class="sxs-lookup"><span data-stu-id="943ba-375">Select the Security tab.</span></span>

<span data-ttu-id="943ba-376">**[ロールの作成または管理]** をクリックし、**管理者**ロールを作成します。</span><span class="sxs-lookup"><span data-stu-id="943ba-376">Click **Create or Manage Roles**, and then create an **Administrator** role.</span></span>

<span data-ttu-id="943ba-377">[セキュリティ] タブに戻ります。</span><span class="sxs-lookup"><span data-stu-id="943ba-377">Return to the Security tab.</span></span>

<span data-ttu-id="943ba-378">**[ユーザーの作成]** をクリックし、 **[管理者]** チェックボックスをオンにして、admin という名前のユーザーを作成します。</span><span class="sxs-lookup"><span data-stu-id="943ba-378">Click **Create user**, and then select the **Administrator** check box and create a user named admin.</span></span>

<span data-ttu-id="943ba-379">**Web サイト管理ツール**を閉じます。</span><span class="sxs-lookup"><span data-stu-id="943ba-379">Close the **Web Site Administration Tool**.</span></span>

### <a name="creating-the-school-database"></a><span data-ttu-id="943ba-380">School データベースを作成する</span><span class="sxs-lookup"><span data-stu-id="943ba-380">Creating the School Database</span></span>

<span data-ttu-id="943ba-381">パッケージマネージャーコンソールウィンドウを開きます。</span><span class="sxs-lookup"><span data-stu-id="943ba-381">Open the Package Manager Console window.</span></span>

<span data-ttu-id="943ba-382">**[既定のプロジェクト]** ドロップダウンリストで、ContosoUniversity プロジェクトを選択します。</span><span class="sxs-lookup"><span data-stu-id="943ba-382">In the **Default project** drop-down list, select the ContosoUniversity.DAL project.</span></span>

<span data-ttu-id="943ba-383">次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="943ba-383">Enter the following command:</span></span>

[!code-powershell[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample9.ps1)]

<span data-ttu-id="943ba-384">Code First Migrations は、データベースを作成する最初の移行を適用してから、AddBirthDate 移行を適用してから、Seed メソッドを実行します。</span><span class="sxs-lookup"><span data-stu-id="943ba-384">Code First Migrations applies the Initial migration that creates the database and then applies the AddBirthDate migration, then it runs the Seed method.</span></span>

<span data-ttu-id="943ba-385">Ctrl キーを押しながら F5 キーを押して、サイトを実行します。</span><span class="sxs-lookup"><span data-stu-id="943ba-385">Run the site by pressing Control-F5.</span></span> <span data-ttu-id="943ba-386">テスト環境と運用環境で行ったように、 **[学生の追加]** ページを実行し、新しい学生を追加して、 **[students]** ページで新しい学生を表示します。</span><span class="sxs-lookup"><span data-stu-id="943ba-386">As you did for the test and production environments, run the **Add Students** page, add a new student, and then view the new student in the **Students** page.</span></span> <span data-ttu-id="943ba-387">これにより、School データベースが作成および初期化されたこと、およびそのデータベースへの読み取りと書き込みのアクセス権があることが確認されます。</span><span class="sxs-lookup"><span data-stu-id="943ba-387">This verifies that the School database was created and initialized and that you have read and write access to it.</span></span>

<span data-ttu-id="943ba-388">**[更新プログラムのクレジット]** ページを選択してログインし、メンバーシップデータベースが展開されていることと、それにアクセスできることを確認します。</span><span class="sxs-lookup"><span data-stu-id="943ba-388">Select the **Update Credits** page and log in to verify that the membership database was deployed and that you have access to it.</span></span> <span data-ttu-id="943ba-389">ユーザーアカウントを移行していない場合は、管理者アカウントを作成し、 **[更新プログラムのクレジット]** ページを選択して、有効であることを確認します。</span><span class="sxs-lookup"><span data-stu-id="943ba-389">If you did not migrate your user accounts, create an administrator account and then select the **Update Credits** page to verify that it works.</span></span>

## <a name="cleaning-up-sql-server-compact-files"></a><span data-ttu-id="943ba-390">SQL Server Compact ファイルのクリーンアップ</span><span class="sxs-lookup"><span data-stu-id="943ba-390">Cleaning Up SQL Server Compact Files</span></span>

<span data-ttu-id="943ba-391">SQL Server Compact をサポートするために含まれていたファイルと NuGet パッケージは不要になりました。</span><span class="sxs-lookup"><span data-stu-id="943ba-391">You no longer need files and NuGet packages that were included to support SQL Server Compact.</span></span> <span data-ttu-id="943ba-392">必要に応じて (この手順は必要ありません)、不要なファイルと参照をクリーンアップできます。</span><span class="sxs-lookup"><span data-stu-id="943ba-392">If you want (this step is not required), you can clean up unneeded files and references.</span></span>

<span data-ttu-id="943ba-393">**ソリューションエクスプローラー**で、 *App\_Data*フォルダーから *.sdf*ファイルを削除し、 *bin*フォルダーから*amd64*および*x86*フォルダーを削除します。</span><span class="sxs-lookup"><span data-stu-id="943ba-393">In **Solution Explorer**, delete the *.sdf* files from the *App\_Data* folder and the *amd64* and *x86* folders from the *bin* folder.</span></span>

<span data-ttu-id="943ba-394">**ソリューションエクスプローラー**で、(プロジェクトの1つではなく) ソリューションを右クリックし、 **[ソリューションの NuGet パッケージの管理]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="943ba-394">In **Solution Explorer**, right-click the solution (not one of the projects), and then click **Manage NuGet Packages for Solution**.</span></span>

<span data-ttu-id="943ba-395">**[NuGet パッケージの管理]** ダイアログボックスの左ペインで、 **[インストールされたパッケージ]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="943ba-395">In the left pane of the **Manage NuGet Packages** dialog box, select **Installed packages**.</span></span>

<span data-ttu-id="943ba-396">**SqlServerCompact**パッケージを選択し、 **[管理]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="943ba-396">Select the **EntityFramework.SqlServerCompact** package and click **Manage**.</span></span>

<span data-ttu-id="943ba-397">**[プロジェクトの選択**] ダイアログボックスで、両方のプロジェクトが選択されます。</span><span class="sxs-lookup"><span data-stu-id="943ba-397">In the **Select Projects** dialog box, both projects are selected.</span></span> <span data-ttu-id="943ba-398">両方のプロジェクトでパッケージをアンインストールするには、両方のチェックボックスをオフにし、[ **OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="943ba-398">To uninstall the package in both projects, clear both check boxes, then click **OK**.</span></span>

<span data-ttu-id="943ba-399">依存パッケージもアンインストールするかどうかを確認するダイアログボックスが表示されたら、[いいえ] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="943ba-399">In the dialog box that asks if you want to uninstall the dependent packages also, click No.</span></span> <span data-ttu-id="943ba-400">これらのうちの1つは、保持する必要がある Entity Framework パッケージです。</span><span class="sxs-lookup"><span data-stu-id="943ba-400">One of these is the Entity Framework package that you have to keep.</span></span>

<span data-ttu-id="943ba-401">同じ手順に従って、 **SqlServerCompact**パッケージをアンインストールします。</span><span class="sxs-lookup"><span data-stu-id="943ba-401">Follow the same procedure to uninstall the **SqlServerCompact** package.</span></span> <span data-ttu-id="943ba-402">(パッケージは、 **SqlServerCompact**パッケージが**SqlServerCompact**パッケージに依存しているため、この順序でアンインストールする必要があります)。</span><span class="sxs-lookup"><span data-stu-id="943ba-402">(The packages must be uninstalled in this order because the **EntityFramework.SqlServerCompact** package depends on the **SqlServerCompact** package.)</span></span>

<span data-ttu-id="943ba-403">これで、SQL Server Express と完全 SQL Server に正常に移行できました。</span><span class="sxs-lookup"><span data-stu-id="943ba-403">You have now successfully migrated to SQL Server Express and full SQL Server.</span></span> <span data-ttu-id="943ba-404">次のチュートリアルでは、別のデータベースを変更します。テストデータベースと実稼働データベースで SQL Server Express と完全 SQL Server が使用されている場合は、データベースの変更を配置する方法を確認します。</span><span class="sxs-lookup"><span data-stu-id="943ba-404">In the next tutorial you'll make another database change, and you'll see how to deploy database changes when your test and production databases use SQL Server Express and full SQL Server.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="943ba-405">[前へ](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md)
> [次へ](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12.md)</span><span class="sxs-lookup"><span data-stu-id="943ba-405">[Previous](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md)
[Next](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12.md)</span></span>
