---
ms.openlocfilehash: 025a244812a50709bfd48de9f47a234a547c53e2
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57047419"
---
<span data-ttu-id="728bc-101"><!-- THIS INCLUDE USED BY MVC AND RP --> `Movie` クラスに次のプロパティを追加します。</span><span class="sxs-lookup"><span data-stu-id="728bc-101"><!-- THIS INCLUDE USED BY MVC AND RP --> Add the following properties to the `Movie` class:</span></span>

[!code-csharp[](~/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie22/Models/Movie.cs?name=snippet1)]

<span data-ttu-id="728bc-102">`Movie` クラスには次が含まれます。</span><span class="sxs-lookup"><span data-stu-id="728bc-102">The `Movie` class contains:</span></span>

* <span data-ttu-id="728bc-103">`ID` フィールドは、データベースで主キー用に必要です。</span><span class="sxs-lookup"><span data-stu-id="728bc-103">The `ID` field is required by the database for the primary key.</span></span>
* <span data-ttu-id="728bc-104">`[DataType(DataType.Date)]`:[DataType](/dotnet/api/microsoft.aspnetcore.mvc.dataannotations.internal.datatypeattributeadapter) 属性では、データの型 (Date) を指定します。</span><span class="sxs-lookup"><span data-stu-id="728bc-104">`[DataType(DataType.Date)]`:  The [DataType](/dotnet/api/microsoft.aspnetcore.mvc.dataannotations.internal.datatypeattributeadapter) attribute specifies the type of the data (Date).</span></span> <span data-ttu-id="728bc-105">この属性を使用する場合:</span><span class="sxs-lookup"><span data-stu-id="728bc-105">With this attribute:</span></span>

  * <span data-ttu-id="728bc-106">ユーザーは日付フィールドに時刻の情報を入力する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="728bc-106">The user is not required to enter time information in the date field.</span></span>
  * <span data-ttu-id="728bc-107">日付のみが表示され、時刻の情報は表示されません。</span><span class="sxs-lookup"><span data-stu-id="728bc-107">Only the date is displayed, not time information.</span></span>

<span data-ttu-id="728bc-108">[DataAnnotations](/dotnet/api/system.componentmodel.dataannotations) は、後のチュートリアルで説明されます。</span><span class="sxs-lookup"><span data-stu-id="728bc-108">[DataAnnotations](/dotnet/api/system.componentmodel.dataannotations) are covered in a later tutorial.</span></span>