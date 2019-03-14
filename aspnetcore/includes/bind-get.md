---
ms.openlocfilehash: 545448e3673b02abc7e685bd987f2cf5f71375b4
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57051959"
---
> [!WARNING]
> セキュリティ上の理由から、ページ モデルのプロパティに対して `GET` 要求データのバインドをオプトインする必要があります。 プロパティにマップする前に、ユーザー入力を確認してください。 `GET` バインドをオプトインするのは、クエリ文字列やルート値に依存するシナリオに対処する場合に便利です。
>
> `GET` 要求のプロパティをバインドするには、[[BindProperty]](/dotnet/api/microsoft.aspnetcore.mvc.bindpropertyattribute) 属性の `SupportsGet` プロパティを `true`: `[BindProperty(SupportsGet = true)]` に設定します
