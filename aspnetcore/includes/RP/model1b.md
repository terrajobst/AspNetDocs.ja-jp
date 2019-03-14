---
ms.openlocfilehash: 025a244812a50709bfd48de9f47a234a547c53e2
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57047419"
---
<!-- THIS INCLUDE USED BY MVC AND RP --> `Movie` クラスに次のプロパティを追加します。

[!code-csharp[](~/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie22/Models/Movie.cs?name=snippet1)]

`Movie` クラスには次が含まれます。

* `ID` フィールドは、データベースで主キー用に必要です。
* `[DataType(DataType.Date)]`:[DataType](/dotnet/api/microsoft.aspnetcore.mvc.dataannotations.internal.datatypeattributeadapter) 属性では、データの型 (Date) を指定します。 この属性を使用する場合:

  * ユーザーは日付フィールドに時刻の情報を入力する必要はありません。
  * 日付のみが表示され、時刻の情報は表示されません。

[DataAnnotations](/dotnet/api/system.componentmodel.dataannotations) は、後のチュートリアルで説明されます。