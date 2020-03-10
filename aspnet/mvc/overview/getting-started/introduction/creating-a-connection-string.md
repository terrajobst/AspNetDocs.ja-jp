---
uid: mvc/overview/getting-started/introduction/creating-a-connection-string
title: 接続文字列を作成し SQL Server LocalDB | を操作するMicrosoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 10/17/2013
ms.assetid: 6127804d-c1a9-414d-8429-7f3dd0f56e97
msc.legacyurl: /mvc/overview/getting-started/introduction/creating-a-connection-string
msc.type: authoredcontent
ms.openlocfilehash: 20781ad760d3a0e4559ec4c7e18528f3686dcc02
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78499012"
---
# <a name="creating-a-connection-string-and-working-with-sql-server-localdb"></a><span data-ttu-id="9da4d-102">接続文字列の作成と SQL Server LocalDB の使用</span><span class="sxs-lookup"><span data-stu-id="9da4d-102">Creating a Connection String and Working with SQL Server LocalDB</span></span>

<span data-ttu-id="9da4d-103">[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="9da4d-103">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[!INCLUDE [Tutorial Note](index.md)]

## <a name="creating-a-connection-string-and-working-with-sql-server-localdb"></a><span data-ttu-id="9da4d-104">接続文字列の作成と SQL Server LocalDB の使用</span><span class="sxs-lookup"><span data-stu-id="9da4d-104">Creating a Connection String and Working with SQL Server LocalDB</span></span>

<span data-ttu-id="9da4d-105">作成した `MovieDBContext` クラスによって、データベースへの接続と `Movie` オブジェクトのデータベースレコードへのマッピングのタスクが処理されます。</span><span class="sxs-lookup"><span data-stu-id="9da4d-105">The `MovieDBContext` class you created handles the task of connecting to the database and mapping `Movie` objects to database records.</span></span> <span data-ttu-id="9da4d-106">ただし、接続先のデータベースを指定する方法について質問することもできます。</span><span class="sxs-lookup"><span data-stu-id="9da4d-106">One question you might ask, though, is how to specify which database it will connect to.</span></span> <span data-ttu-id="9da4d-107">実際には、使用するデータベースを指定する必要はありません。 Entity Framework 既定で[LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb)が使用されます。</span><span class="sxs-lookup"><span data-stu-id="9da4d-107">You don't actually have to specify which database to use, Entity Framework will default to using [LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb).</span></span> <span data-ttu-id="9da4d-108">このセクションで*は、アプリケーションの web.config ファイルに*接続文字列を明示的に追加します。</span><span class="sxs-lookup"><span data-stu-id="9da4d-108">In this section we'll explicitly add a connection string in the *Web.config* file of the application.</span></span>

## <a name="sql-server-express-localdb"></a><span data-ttu-id="9da4d-109">SQL Server Express LocalDB</span><span class="sxs-lookup"><span data-stu-id="9da4d-109">SQL Server Express LocalDB</span></span>

<span data-ttu-id="9da4d-110">[LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb)は、オンデマンドで開始され、ユーザーモードで実行される SQL Server Express データベースエンジンの軽量バージョンです。</span><span class="sxs-lookup"><span data-stu-id="9da4d-110">[LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb) is a lightweight version of the SQL Server Express Database Engine that starts on demand and runs in user mode.</span></span> <span data-ttu-id="9da4d-111">LocalDB は、 *.mdf*ファイルとしてデータベースを操作できるようにする SQL Server Express の特別な実行モードで実行されます。</span><span class="sxs-lookup"><span data-stu-id="9da4d-111">LocalDB runs in a special execution mode of SQL Server Express that enables you to work with databases as *.mdf* files.</span></span> <span data-ttu-id="9da4d-112">通常、LocalDB データベースファイルは、web プロジェクトの*App\_Data*フォルダーに保持されます。</span><span class="sxs-lookup"><span data-stu-id="9da4d-112">Typically, LocalDB database files are kept in the *App\_Data* folder of a web project.</span></span>

<span data-ttu-id="9da4d-113">SQL Server Express は、運用 web アプリケーションでは使用しないことをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="9da4d-113">SQL Server Express is not recommended for use in production web applications.</span></span> <span data-ttu-id="9da4d-114">特に LocalDB は、IIS で動作するように設計されていないため、web アプリケーションを使用した運用環境では使用しないでください。</span><span class="sxs-lookup"><span data-stu-id="9da4d-114">LocalDB in particular should not be used for production with a web application because it is not designed to work with IIS.</span></span> <span data-ttu-id="9da4d-115">ただし、LocalDB データベースは、SQL Server または SQL Azure に簡単に移行できます。</span><span class="sxs-lookup"><span data-stu-id="9da4d-115">However, a LocalDB database can be easily migrated to SQL Server or SQL Azure.</span></span>

<span data-ttu-id="9da4d-116">Visual Studio 2017 では、LocalDB は既定で Visual Studio と共にインストールされます。</span><span class="sxs-lookup"><span data-stu-id="9da4d-116">In Visual Studio 2017, LocalDB is installed by default with Visual Studio.</span></span>

<span data-ttu-id="9da4d-117">既定では、Entity Framework は、オブジェクトコンテキストクラス (このプロジェクトの`MovieDBContext`) と同じ名前の接続文字列を検索します。</span><span class="sxs-lookup"><span data-stu-id="9da4d-117">By default, the Entity Framework looks for a connection string named the same as the object context class (`MovieDBContext` for this project).</span></span> <span data-ttu-id="9da4d-118">詳細については、「 [SQL Server ASP.NET Web Applications の接続文字列」を](https://msdn.microsoft.com/library/jj653752.aspx)参照してください。</span><span class="sxs-lookup"><span data-stu-id="9da4d-118">For more information see [SQL Server Connection Strings for ASP.NET Web Applications](https://msdn.microsoft.com/library/jj653752.aspx).</span></span>

<span data-ttu-id="9da4d-119">次に示すように、*アプリケーションルートの web.config ファイル*を開きます。</span><span class="sxs-lookup"><span data-stu-id="9da4d-119">Open the application root *Web.config* file shown below.</span></span> <span data-ttu-id="9da4d-120">( *Views*フォルダー*内の web.config ファイルで*はありません)。</span><span class="sxs-lookup"><span data-stu-id="9da4d-120">(Not the *Web.config* file in the *Views* folder.)</span></span>

![](creating-a-connection-string/_static/image1.png)

<span data-ttu-id="9da4d-121">`<connectionStrings>` 要素を検索します。</span><span class="sxs-lookup"><span data-stu-id="9da4d-121">Find the `<connectionStrings>` element:</span></span>

![](creating-a-connection-string/_static/image2.png)

<span data-ttu-id="9da4d-122">次の接続文字列を web.config ファイルの `<connectionStrings>` 要素に追加*します。*</span><span class="sxs-lookup"><span data-stu-id="9da4d-122">Add the following connection string to the `<connectionStrings>` element in the *Web.config* file.</span></span>

[!code-xml[Main](creating-a-connection-string/samples/sample1.xml)]

<span data-ttu-id="9da4d-123">次の例は、新しい接続文字列が追加された web.config ファイルの一部を示して*い*ます。</span><span class="sxs-lookup"><span data-stu-id="9da4d-123">The following example shows a portion of the *Web.config* file with the new connection string added:</span></span>

[!code-xml[Main](creating-a-connection-string/samples/sample2.xml)]

<span data-ttu-id="9da4d-124">2つの接続文字列はよく似ています。</span><span class="sxs-lookup"><span data-stu-id="9da4d-124">The two connection strings are very similar.</span></span> <span data-ttu-id="9da4d-125">最初の接続文字列には `DefaultConnection` という名前が付けられ、メンバーシップデータベースでアプリケーションにアクセスできるユーザーを制御するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="9da4d-125">The first connection string is named `DefaultConnection` and is used for the membership database to control who can access the application.</span></span> <span data-ttu-id="9da4d-126">追加した接続文字列によって、 *App\_Data*フォルダーにある、 *Movie*という名前の LocalDB データベースが指定されます。</span><span class="sxs-lookup"><span data-stu-id="9da4d-126">The connection string you've added specifies a LocalDB database named *Movie.mdf* located in the *App\_Data* folder.</span></span> <span data-ttu-id="9da4d-127">このチュートリアルではメンバーシップデータベースを使用しません。メンバーシップ、認証、およびセキュリティの詳細については、「 [ASP.NET MVC アプリを認証および SQL DB で作成する」と「Azure App Service に配置する](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="9da4d-127">We won't use the membership database in this tutorial, for more information on membership, authentication and security, see my tutorial [Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span></span>

<span data-ttu-id="9da4d-128">接続文字列の名前は、 [Dbcontext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx)クラスの名前と一致している必要があります。</span><span class="sxs-lookup"><span data-stu-id="9da4d-128">The name of the connection string must match the name of the [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx) class.</span></span>

[!code-csharp[Main](creating-a-connection-string/samples/sample3.cs?highlight=15)]

<span data-ttu-id="9da4d-129">実際には、`MovieDBContext` 接続文字列を追加する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="9da4d-129">You don't actually need to add the `MovieDBContext` connection string.</span></span> <span data-ttu-id="9da4d-130">接続文字列を指定しない場合、Entity Framework によって、 [Dbcontext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx)クラス (この場合 `MvcMovie.Models.MovieDBContext`) の完全修飾名を持つ LocalDB データベースが users ディレクトリに作成されます。</span><span class="sxs-lookup"><span data-stu-id="9da4d-130">If you don't specify a connection string, Entity Framework will create a LocalDB database in the users directory with the fully qualified name of the [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx) class (in this case `MvcMovie.Models.MovieDBContext`).</span></span> <span data-ttu-id="9da4d-131">データベースには、が含まれている限り、任意の名前を指定でき*ます。MDF*サフィックス。</span><span class="sxs-lookup"><span data-stu-id="9da4d-131">You can name the database anything you like, as long as it has the *.MDF* suffix.</span></span> <span data-ttu-id="9da4d-132">たとえば、データベースに*Myfilms .mdf*という名前を指定できます。</span><span class="sxs-lookup"><span data-stu-id="9da4d-132">For example, we could name the database *MyFilms.mdf*.</span></span>

<span data-ttu-id="9da4d-133">次に、ムービーデータを表示するために使用できる新しい `MoviesController` クラスを作成し、ユーザーが新しいムービーの一覧を作成できるようにします。</span><span class="sxs-lookup"><span data-stu-id="9da4d-133">Next, you'll build a new `MoviesController` class that you can use to display the movie data and allow users to create new movie listings.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="9da4d-134">[前へ](adding-a-model.md)
> [次へ](accessing-your-models-data-from-a-controller.md)</span><span class="sxs-lookup"><span data-stu-id="9da4d-134">[Previous](adding-a-model.md)
[Next](accessing-your-models-data-from-a-controller.md)</span></span>
