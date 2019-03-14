---
ms.openlocfilehash: 22c540058e0b3b9ae612f1b2612cecc08627ea2b
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57063989"
---
<a name="test"></a>
### <a name="test-the-app"></a><span data-ttu-id="3dd92-101">アプリのテスト</span><span class="sxs-lookup"><span data-stu-id="3dd92-101">Test the app</span></span>

* <span data-ttu-id="3dd92-102">アプリを実行し、ブラウザーで URL に `/Movies` を追加します (`http://localhost:port/movies`)。</span><span class="sxs-lookup"><span data-stu-id="3dd92-102">Run the app and append `/Movies` to the URL in the browser (`http://localhost:port/movies`).</span></span>
* <span data-ttu-id="3dd92-103">**[作成]** リンクをテストします。</span><span class="sxs-lookup"><span data-stu-id="3dd92-103">Test the **Create** link.</span></span>

  ![[作成] ページ](../../tutorials/razor-pages/model/_static/conan.png)

<a name="scaffold"></a>

* <span data-ttu-id="3dd92-105">**[編集]**、**[詳細]**、および **[削除]** の各リンクをテストします。</span><span class="sxs-lookup"><span data-stu-id="3dd92-105">Test the **Edit**, **Details**, and **Delete** links.</span></span>

<span data-ttu-id="3dd92-106">次のエラーが発生した場合は、移行を実行しており、データベースを更新したことを確認します。</span><span class="sxs-lookup"><span data-stu-id="3dd92-106">If you get the following error, verify you have run migrations and updated the database:</span></span>

```
An unhandled exception occurred while processing the request.
SqliteException: SQLite Error 1: 'no such table: Movie'.
Microsoft.Data.Sqlite.SqliteException.ThrowExceptionForRC(int rc, sqlite3 db)
```
