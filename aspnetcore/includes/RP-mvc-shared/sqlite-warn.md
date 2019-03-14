---
ms.openlocfilehash: 2481b10abae9aefce2d5173d8071e4c2236db928
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57048219"
---

> [!NOTE]
> <span data-ttu-id="a66d2-101">スキーマ変更操作の多くは、EF Core の SQLite プロバイダーによってサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="a66d2-101">Many schema change operations are not supported by the EF Core SQLite provider.</span></span> <span data-ttu-id="a66d2-102">たとえば、列の追加はサポートされていますが、列の削除はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="a66d2-102">For example, adding a column is supported, but removing a column is not supported.</span></span> <span data-ttu-id="a66d2-103">移行を作成して、列を削除する場合、`ef migrations add`コマンドが成功したが、`ef database update`コマンドは失敗します。</span><span class="sxs-lookup"><span data-stu-id="a66d2-103">If a migration is created to remove a column, the `ef migrations add` command succeeds but the `ef database update` command fails.</span></span> <span data-ttu-id="a66d2-104">これらの制限の一部は、手動でテーブルの再構築を実行する移行コードを記述することで解決できます。</span><span class="sxs-lookup"><span data-stu-id="a66d2-104">Some of these limitations can be overcome by manually writing migrations code to perform a table rebuild.</span></span> <span data-ttu-id="a66d2-105">テーブルの再構築が含まれます。</span><span class="sxs-lookup"><span data-stu-id="a66d2-105">A table rebuild involves:</span></span>

>* <span data-ttu-id="a66d2-106">既存のテーブルの名前を変更します。</span><span class="sxs-lookup"><span data-stu-id="a66d2-106">Renaming the existing table.</span></span>
>* <span data-ttu-id="a66d2-107">新しいテーブルを作成します。</span><span class="sxs-lookup"><span data-stu-id="a66d2-107">Creating a new table.</span></span>
>* <span data-ttu-id="a66d2-108">新しいテーブルには、古いテーブルからデータをコピーします。</span><span class="sxs-lookup"><span data-stu-id="a66d2-108">Copying data from the old table to the new table.</span></span>
>* <span data-ttu-id="a66d2-109">古いテーブルを削除しています。</span><span class="sxs-lookup"><span data-stu-id="a66d2-109">Dropping the old table.</span></span>

<span data-ttu-id="a66d2-110">詳細については、次のリソースを参照してください。</span><span class="sxs-lookup"><span data-stu-id="a66d2-110">For more information, see the following resources:</span></span>
> * [<span data-ttu-id="a66d2-111">SQLite EF Core データベース プロバイダーの制限事項</span><span class="sxs-lookup"><span data-stu-id="a66d2-111">SQLite EF Core Database Provider Limitations</span></span>](/ef/core/providers/sqlite/limitations)
> * [<span data-ttu-id="a66d2-112">移行コードをカスタマイズする</span><span class="sxs-lookup"><span data-stu-id="a66d2-112">Customize migration code</span></span>](/ef/core/managing-schemas/migrations/#customize-migration-code)
> * [<span data-ttu-id="a66d2-113">データのシード処理</span><span class="sxs-lookup"><span data-stu-id="a66d2-113">Data seeding</span></span>](/ef/core/modeling/data-seeding)