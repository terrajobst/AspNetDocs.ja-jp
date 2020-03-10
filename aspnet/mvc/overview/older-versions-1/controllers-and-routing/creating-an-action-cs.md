---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-cs
title: アクションを作成するC#() |Microsoft Docs
author: microsoft
description: ASP.NET MVC コントローラーに新しいアクションを追加する方法について説明します。 メソッドをアクションとして使用するための要件について説明します。
ms.author: riande
ms.date: 03/02/2009
ms.assetid: cb33b28c-3025-4bd1-a1fa-eaa3af7bb56f
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-cs
msc.type: authoredcontent
ms.openlocfilehash: ebba935383819935ad85c95245666f4eaf6a0dca
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78470200"
---
# <a name="creating-an-action-c"></a>アクションを作成する (C#)

[Microsoft](https://github.com/microsoft)

> ASP.NET MVC コントローラーに新しいアクションを追加する方法について説明します。 メソッドをアクションとして使用するための要件について説明します。

このチュートリアルの目的は、新しいコントローラーアクションを作成する方法を説明することです。 アクションメソッドの要件について説明します。 また、メソッドがアクションとして公開されないようにする方法についても説明します。

## <a name="adding-an-action-to-a-controller"></a>コントローラーへのアクションの追加

コントローラーに新しいアクションを追加するには、コントローラーに新しいメソッドを追加します。 たとえば、リスト1のコントローラーには、Index () という名前のアクションと、SayHello () という名前のアクションが含まれています。 どちらのメソッドもアクションとして公開されます。

**リスト 1-Controllers\ homecontroller.cs**

[!code-csharp[Main](creating-an-action-cs/samples/sample1.cs)]

アクションとして universe に公開するには、メソッドが特定の要件を満たす必要があります。

- メソッドはパブリックである必要があります。
- メソッドを静的メソッドにすることはできません。
- メソッドを拡張メソッドにすることはできません。
- メソッドをコンストラクター、getter、または setter にすることはできません。
- メソッドにオープンジェネリック型を含めることはできません。
- このメソッドは、コントローラーの基本クラスのメソッドではありません。
- メソッドに**ref**パラメーターまたは**out**パラメーターを含めることはできません。

コントローラーアクションの戻り値の型に制限がないことに注意してください。 コントローラーアクションは、文字列、日時、ランダムクラスのインスタンス、または void を返すことができます。 ASP.NET MVC フレームワークは、アクションの結果ではない戻り値の型を文字列に変換し、その文字列をブラウザーに表示します。

これらの要件に違反しないメソッドをコントローラーに追加すると、そのメソッドはコントローラーアクションとして公開されます。 ここで注意してください。 コントローラーアクションは、インターネットに接続されているすべてのユーザーが呼び出すことができます。 たとえば、DeleteMyWebsite () コントローラーアクションを作成することはできません。

## <a name="preventing-a-public-method-from-being-invoked"></a>パブリックメソッドが呼び出されないようにする

コントローラークラスでパブリックメソッドを作成する必要があり、そのメソッドをコントローラーアクションとして公開しない場合は、[非アクション] 属性を使用してメソッドが呼び出されないようにすることができます。 たとえば、リスト2のコントローラーには、[非アクション] 属性で修飾された、企業秘密 () という名前のパブリックメソッドが含まれています。

**リスト 2-コントローラー (& c)**

[!code-csharp[Main](creating-an-action-cs/samples/sample2.cs)]

ブラウザーのアドレスバーに「/職場/会社のシークレット」と入力して、会社のシークレット () コントローラーの操作を呼び出そうとすると、図1のエラーメッセージが表示されます。

[非アクションメソッドを呼び出す ![](creating-an-action-cs/_static/image1.jpg)](creating-an-action-cs/_static/image1.png)

**図 01**: 非アクションメソッドの呼び出し ([クリックすると、フルサイズの画像が表示](creating-an-action-cs/_static/image2.png)される)

> [!div class="step-by-step"]
> [前へ](creating-a-controller-cs.md)
> [次へ](asp-net-mvc-routing-overview-vb.md)
