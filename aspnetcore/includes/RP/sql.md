---
ms.openlocfilehash: d963e3b52db7703e9b2fad1466a23fdeb1b8f848
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57035359"
---
# <a name="work-with-sqlite-in-an-aspnet-core-razor-pages-app"></a><span data-ttu-id="15a14-101">ASP.NET Core Razor ページ アプリでの SQLite の操作</span><span class="sxs-lookup"><span data-stu-id="15a14-101">Work with SQLite in an ASP.NET Core Razor Pages app</span></span>

<span data-ttu-id="15a14-102">作成者: [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="15a14-102">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="15a14-103">`MovieContext` オブジェクトは、データベースへの接続と、データベース レコードへの `Movie` オブジェクトのマッピングのタスクを処理します。</span><span class="sxs-lookup"><span data-stu-id="15a14-103">The `MovieContext` object handles the task of connecting to the database and mapping `Movie` objects to database records.</span></span> <span data-ttu-id="15a14-104">データベース コンテキストは、*Startup.cs* ファイルの `ConfigureServices` メソッドで[依存性の注入 (DI) ](xref:fundamentals/dependency-injection)コンテナーに登録されます。</span><span class="sxs-lookup"><span data-stu-id="15a14-104">The database context is registered with the [Dependency Injection (DI)](xref:fundamentals/dependency-injection) container in the `ConfigureServices` method in the *Startup.cs* file:</span></span>

[!code-csharp[](code/Startup.cs?name=snippet2&highlight=6-8)]

<span data-ttu-id="15a14-105">DI で `DbContext` を使用する方法の詳細については、「[Using DbContext with DI](/ef/core/miscellaneous/configuring-dbcontext#using-dbcontext-with-dependency-injection)」(DI で DbContext を使用する) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="15a14-105">For more information on using `DbContext` with DI, see [Using DbContext with DI](/ef/core/miscellaneous/configuring-dbcontext#using-dbcontext-with-dependency-injection).</span></span>

## <a name="sqlite"></a><span data-ttu-id="15a14-106">SQLite</span><span class="sxs-lookup"><span data-stu-id="15a14-106">SQLite</span></span>

<span data-ttu-id="15a14-107">[SQLite](https://www.sqlite.org/) の Web サイトは次のようなものです。</span><span class="sxs-lookup"><span data-stu-id="15a14-107">The [SQLite](https://www.sqlite.org/) website states:</span></span>

> <span data-ttu-id="15a14-108">SQLite は埋め込みの全機能を備えた、自己完結型かつ高信頼性でパブリック ドメインの SQL データベース エンジンです。</span><span class="sxs-lookup"><span data-stu-id="15a14-108">SQLite is a self-contained, high-reliability, embedded, full-featured, public-domain, SQL database engine.</span></span> <span data-ttu-id="15a14-109">SQLite は、世界で最も使用されているデータベース エンジンです。</span><span class="sxs-lookup"><span data-stu-id="15a14-109">SQLite is the most used database engine in the world.</span></span>

<span data-ttu-id="15a14-110">SQLite データベースを管理および表示するためにダウンロードできるサードパーティ製ツールは多数あります。</span><span class="sxs-lookup"><span data-stu-id="15a14-110">There are many third party tools you can download to manage and view a SQLite database.</span></span> <span data-ttu-id="15a14-111">以下の画像は [DB Browser for SQLite](http://sqlitebrowser.org/) のものです。</span><span class="sxs-lookup"><span data-stu-id="15a14-111">The image below is from [DB Browser for SQLite](http://sqlitebrowser.org/).</span></span> <span data-ttu-id="15a14-112">お気に入りの SQLite ツールがございましたら、そのツールの気に入っている点についてコメントしてください。</span><span class="sxs-lookup"><span data-stu-id="15a14-112">If you have a favorite SQLite tool, leave a comment on what you like about it.</span></span>

![movie db を示している DB Browser for SQLite](../../tutorials/first-mvc-app-xplat/working-with-sql/_static/dbb.png)

## <a name="seed-the-database"></a><span data-ttu-id="15a14-114">データベースのシード</span><span class="sxs-lookup"><span data-stu-id="15a14-114">Seed the database</span></span>

<span data-ttu-id="15a14-115">*Models* フォルダーに `SeedData` という名前の新しいクラスを作成します。</span><span class="sxs-lookup"><span data-stu-id="15a14-115">Create a new class named `SeedData` in the *Models* folder.</span></span> <span data-ttu-id="15a14-116">生成されたコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="15a14-116">Replace the generated code with the following:</span></span>

[!code-csharp[](code/Models/SeedData.cs)]

<span data-ttu-id="15a14-117">DB にムービーがある場合、シード初期化子が返されます。</span><span class="sxs-lookup"><span data-stu-id="15a14-117">If there are any movies in the DB, the seed initializer returns.</span></span>

```csharp
if (context.Movie.Any())
{
    return;   // DB has been seeded.
}
```

<a name="si"></a>
### <a name="add-the-seed-initializer"></a><span data-ttu-id="15a14-118">シード初期化子の追加</span><span class="sxs-lookup"><span data-stu-id="15a14-118">Add the seed initializer</span></span>

<span data-ttu-id="15a14-119">次のように、*Program.cs* ファイルで `Main` メソッドにシード初期化子を追加します。</span><span class="sxs-lookup"><span data-stu-id="15a14-119">Add the seed initializer to the `Main` method in the *Program.cs* file:</span></span>

[!code-csharp[](../../tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Program.cs)]

### <a name="test-the-app"></a><span data-ttu-id="15a14-120">アプリのテスト</span><span class="sxs-lookup"><span data-stu-id="15a14-120">Test the app</span></span>

<span data-ttu-id="15a14-121">DB 内のすべてのレコードを削除します (そのため Seed メソッドが実行されます)。</span><span class="sxs-lookup"><span data-stu-id="15a14-121">Delete all the records in the DB (So the seed method will run).</span></span> <span data-ttu-id="15a14-122">アプリを停止および起動して、データベースをシードします。</span><span class="sxs-lookup"><span data-stu-id="15a14-122">Stop and start the app to seed the database.</span></span>

<span data-ttu-id="15a14-123">アプリにシードされたデータが表示されます。</span><span class="sxs-lookup"><span data-stu-id="15a14-123">The app shows the seeded data.</span></span>
