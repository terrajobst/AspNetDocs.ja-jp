---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-a-route-constraint-cs
title: ルート制約を作成するC#() |Microsoft Docs
author: StephenWalther
description: このチュートリアルでは、Stephen Walther は、正規表現を使用してルート制約を作成することによって、ルートがどのように一致するかを制御する方法を示しています。
ms.author: riande
ms.date: 02/16/2009
ms.assetid: 0bfd06b1-12d3-4fbb-9779-a82e5eb7fe7d
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-a-route-constraint-cs
msc.type: authoredcontent
ms.openlocfilehash: 51ef859287b3424faf85f4a3606a220ab48a9466
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78470164"
---
# <a name="creating-a-route-constraint-c"></a>ルート制約を作成する (C#)

[Stephen Walther](https://github.com/StephenWalther)

> このチュートリアルでは、Stephen Walther は、正規表現を使用してルート制約を作成することによって、ルートがどのように一致するかを制御する方法を示しています。

ルート制約は、特定のルートに一致するブラウザー要求を制限するために使用します。 正規表現を使用して、ルート制約を指定することができます。

たとえば、リスト1のルートが global.asax ファイルに定義されているとします。

**リスト 1-Global.asax.cs**

[!code-csharp[Main](creating-a-route-constraint-cs/samples/sample1.cs)]

リスト1には、Product という名前のルートが含まれています。 製品ルートを使用して、リスト2に含まれる ProductController にブラウザーの要求をマップできます。

**リスト 2-コントローラー (productコントローラー)**

[!code-csharp[Main](creating-a-route-constraint-cs/samples/sample2.cs)]

Product コントローラーによって公開されている Details () アクションでは、productId という名前の1つのパラメーターを受け取ることに注意してください。 このパラメーターは整数のパラメーターです。

リスト1で定義されているルートは、次の Url のいずれかと一致します。

- /Product/23
- /Product/7

残念ながら、ルートは次の Url とも一致します。

- /Product/blah
- /Product/apple

Details () アクションには整数のパラメーターが必要であるため、整数値以外を含む要求を行うと、エラーが発生します。 たとえば、ブラウザーに「/Product/apple」と入力すると、図1のエラーページが表示されます。

[[新しいプロジェクト] ダイアログボックスの ![](creating-a-route-constraint-cs/_static/image1.jpg)](creating-a-route-constraint-cs/_static/image1.png)

**図 01**: ページの爆発を[確認する (クリックすると、フルサイズの画像が表示](creating-a-route-constraint-cs/_static/image2.png)される)

実際に必要なのは、productId が適切な整数を含む Url だけです。 ルートを定義するときに、ルートに一致する Url を制限するための制約を使用できます。 リスト3の変更された製品ルートには、整数のみに一致する正規表現制約が含まれています。

**リスト 3-Global.asax.cs**

[!code-csharp[Main](creating-a-route-constraint-cs/samples/sample3.cs)]

正規表現 \d + は、1つ以上の整数に一致します。 この制約により、製品ルートは次の Url と一致します。

- /Product/3
- /Product/8999

ただし、次の Url はありません。

- /Product/apple
- /Product

- これらのブラウザー要求は別のルートによって処理されます。一致するルートがない場合は、*リソースが見つからない*というエラーが返されます。

> [!div class="step-by-step"]
> [前へ](creating-custom-routes-cs.md)
> [次へ](creating-a-custom-route-constraint-cs.md)
