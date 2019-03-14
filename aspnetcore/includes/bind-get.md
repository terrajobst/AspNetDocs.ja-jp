---
ms.openlocfilehash: 545448e3673b02abc7e685bd987f2cf5f71375b4
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57051959"
---
> [!WARNING]
> <span data-ttu-id="669bc-101">セキュリティ上の理由から、ページ モデルのプロパティに対して `GET` 要求データのバインドをオプトインする必要があります。</span><span class="sxs-lookup"><span data-stu-id="669bc-101">For security reasons, you must opt in to binding `GET` request data to page model properties.</span></span> <span data-ttu-id="669bc-102">プロパティにマップする前に、ユーザー入力を確認してください。</span><span class="sxs-lookup"><span data-stu-id="669bc-102">Verify user input before mapping it to properties.</span></span> <span data-ttu-id="669bc-103">`GET` バインドをオプトインするのは、クエリ文字列やルート値に依存するシナリオに対処する場合に便利です。</span><span class="sxs-lookup"><span data-stu-id="669bc-103">Opting in to `GET` binding is useful when addressing scenarios which rely on query string or route values.</span></span>
>
> <span data-ttu-id="669bc-104">`GET` 要求のプロパティをバインドするには、[[BindProperty]](/dotnet/api/microsoft.aspnetcore.mvc.bindpropertyattribute) 属性の `SupportsGet` プロパティを `true`: `[BindProperty(SupportsGet = true)]` に設定します</span><span class="sxs-lookup"><span data-stu-id="669bc-104">To bind a property on `GET` requests, set the [[BindProperty]](/dotnet/api/microsoft.aspnetcore.mvc.bindpropertyattribute) attribute's `SupportsGet` property to `true`: `[BindProperty(SupportsGet = true)]`</span></span>
