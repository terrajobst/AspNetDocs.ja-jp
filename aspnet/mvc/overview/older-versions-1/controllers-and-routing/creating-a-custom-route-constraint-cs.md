---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-a-custom-route-constraint-cs
title: カスタムルート制約を作成するC#() |Microsoft Docs
author: StephenWalther
description: Stephen Walther は、カスタムルート制約を作成する方法を示しています。 ルートが一致しないようにする単純なカスタム制約を実装しています...
ms.author: riande
ms.date: 02/16/2009
ms.assetid: a4f4bf4e-abcc-4650-8f43-527e48b52fe6
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-a-custom-route-constraint-cs
msc.type: authoredcontent
ms.openlocfilehash: 98d5839e3d2623665770ccc5689c28f9eb29c8f6
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486826"
---
# <a name="creating-a-custom-route-constraint-c"></a>カスタム ルート制約を作成する (C#)

[Stephen Walther](https://github.com/StephenWalther)

> Stephen Walther は、カスタムルート制約を作成する方法を示しています。 リモートコンピューターからブラウザーの要求が行われたときに、ルートが一致しないようにする単純なカスタム制約を実装します。

このチュートリアルの目的は、カスタムルート制約を作成する方法を説明することです。 カスタムルート制約を使用すると、一部のカスタム条件に一致しない限り、ルートが一致しないようにすることができます。

このチュートリアルでは、Localhost ルート制約を作成します。 Localhost route 制約は、ローカルコンピューターからの要求のみと一致します。 インターネット経由のリモート要求が一致しません。

カスタムルート制約を実装するには、IRouteConstraint インターフェイスを実装します。 これは、1つのメソッドを記述する非常に単純なインターフェイスです。

[!code-csharp[Main](creating-a-custom-route-constraint-cs/samples/sample1.cs)]

メソッドはブール値を返します。 False を返した場合、制約に関連付けられているルートはブラウザーの要求と一致しません。

Localhost 制約は、リスト1に含まれています。

**リスト 1-LocalhostConstraint.cs**

[!code-csharp[Main](creating-a-custom-route-constraint-cs/samples/sample2.cs)]

リスト1の制約では、HttpRequest クラスによって公開されている IsLocal プロパティを利用します。 このプロパティは、要求の IP アドレスが127.0.0.1 であるか、要求の IP アドレスがサーバーの IP アドレスと同じである場合に true を返します。

Global.asax ファイルで定義されているルート内でカスタム制約を使用します。 リスト2の global.asax ファイルは Localhost 制約を使用して、ローカルサーバーから要求を行う場合を除き、だれでも管理ページを要求しないようにします。 たとえば、リモートサーバーからの/Admin/DeleteAll 要求は失敗します。

**リスト 2-global.asax**

[!code-csharp[Main](creating-a-custom-route-constraint-cs/samples/sample3.cs)]

Localhost 制約は、管理ルートの定義で使用されます。 このルートは、リモートブラウザーの要求と一致しません。 ただし、global.asax で定義されている他のルートは、同じ要求と一致している可能性があります。 制約は、グローバルな global.asax ファイルで定義されているすべてのルートではなく、特定のルートが要求と一致しないようにすることを理解しておくことが重要です。

リスト2の global.asax ファイルから、既定のルートがコメントアウトされていることに注意してください。 既定のルートを含めると、既定のルートは管理コントローラーの要求と一致します。 その場合でも、リモートユーザーは、要求が管理者ルートと一致しない場合でも、管理コントローラーのアクションを呼び出すことができます。

> [!div class="step-by-step"]
> [前へ](creating-a-route-constraint-cs.md)
> [次へ](asp-net-mvc-controller-overview-vb.md)
