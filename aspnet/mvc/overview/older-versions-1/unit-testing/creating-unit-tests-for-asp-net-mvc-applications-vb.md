---
uid: mvc/overview/older-versions-1/unit-testing/creating-unit-tests-for-asp-net-mvc-applications-vb
title: ASP.NET MVC アプリケーション用の単体テストの作成 (VB) |Microsoft Docs
author: StephenWalther
description: コントローラーアクションの単体テストを作成する方法について説明します。 このチュートリアルでは、Stephen Walther はコントローラーアクションが parti を返すかどうかをテストする方法を示しています。
ms.author: riande
ms.date: 08/19/2008
ms.assetid: eb35710d-1d99-44ac-b61f-e50af8cb328a
msc.legacyurl: /mvc/overview/older-versions-1/unit-testing/creating-unit-tests-for-asp-net-mvc-applications-vb
msc.type: authoredcontent
ms.openlocfilehash: 643faddaf6f9cd075131e8e5a9cccb303e355ceb
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74594688"
---
# <a name="creating-unit-tests-for-aspnet-mvc-applications-vb"></a>ASP.NET MVC アプリケーションの単体テストを作成する (VB)

[Stephen Walther](https://github.com/StephenWalther)

[PDF のダウンロード](https://download.microsoft.com/download/8/4/8/84843d8d-1575-426c-bcb5-9d0c42e51416/ASPNET_MVC_Tutorial_07_VB.pdf)

> コントローラーアクションの単体テストを作成する方法について説明します。 このチュートリアルでは、Stephen Walther は、コントローラーアクションが特定のビューを返すか、特定のデータセットを返すか、または別の種類のアクション結果を返すかをテストする方法を示しています。

このチュートリアルの目的は、ASP.NET MVC アプリケーションでコントローラーの単体テストを作成する方法を説明することです。 ここでは、3種類の単体テストを作成する方法について説明します。 コントローラーアクションによって返されるビューをテストする方法、コントローラーアクションによって返されるビューデータをテストする方法、1つのコントローラーアクションが2番目のコントローラーアクションにリダイレクトするかどうかをテストする方法について説明します。

## <a name="creating-the-controller-under-test"></a>テスト対象のコントローラーを作成しています

まず、テストするコントローラーを作成してみましょう。 `ProductController`という名前のコントローラーは、リスト1に含まれています。

**リスト1– `ProductController.vb`**

[!code-vb[Main](creating-unit-tests-for-asp-net-mvc-applications-vb/samples/sample1.vb)]

`ProductController` には、`Index()` と `Details()`という2つのアクションメソッドが含まれています。 どちらのアクションメソッドもビューを返します。 `Details()` アクションでは、Id という名前のパラメーターを受け取ることに注意してください。

## <a name="testing-the-view-returned-by-a-controller"></a>コントローラーによって返されるビューをテストする

`ProductController` が正しいビューを返すかどうかをテストするとします。 `ProductController.Details()` アクションが呼び出されたときに、詳細ビューが返されるようにします。 リスト2のテストクラスには、`ProductController.Details()` アクションによって返されたビューをテストするための単体テストが含まれています。

**リスト2– `ProductControllerTest.vb`**

[!code-vb[Main](creating-unit-tests-for-asp-net-mvc-applications-vb/samples/sample2.vb)]

リスト2のクラスには、`TestDetailsView()`という名前のテストメソッドが含まれています。 このメソッドには3行のコードが含まれています。 コードの1行目では、`ProductController` クラスの新しいインスタンスを作成します。 コードの2行目では、コントローラーの `Details()` アクションメソッドを呼び出します。 最後に、コードの最後の行で、`Details()` アクションによって返されるビューが詳細ビューであるかどうかをチェックします。

`ViewResult.ViewName` プロパティは、コントローラーによって返されるビューの名前を表します。 このプロパティのテストに関する大きな警告が1つあります。 コントローラーがビューを返すには、2つの方法があります。 コントローラーは、次のようなビューを明示的に返すことができます。

[!code-vb[Main](creating-unit-tests-for-asp-net-mvc-applications-vb/samples/sample3.vb)]

また、ビューの名前は、次のようにコントローラーアクションの名前から推論することもできます。

[!code-vb[Main](creating-unit-tests-for-asp-net-mvc-applications-vb/samples/sample4.vb)]

このコントローラーアクションは、`Details`という名前のビューも返します。 ただし、ビューの名前はアクション名から推測されます。 ビュー名をテストする場合は、コントローラーアクションからビュー名を明示的に返す必要があります。

リスト2で単体テストを実行するには、 **Ctrl + R キー**の組み合わせを入力するか、 **[ソリューション内のすべてのテストを実行]** ボタン (図1を参照) をクリックします。 テストに合格すると、図2の [テスト結果] ウィンドウが表示されます。

[ソリューション内のすべてのテストを実行 ![](creating-unit-tests-for-asp-net-mvc-applications-vb/_static/image2.png)](creating-unit-tests-for-asp-net-mvc-applications-vb/_static/image1.png)

**図 01**: ソリューション内のすべてのテストを実行[する (クリックすると、フルサイズのイメージが表示](creating-unit-tests-for-asp-net-mvc-applications-vb/_static/image3.png)される)

[![成功しました。](creating-unit-tests-for-asp-net-mvc-applications-vb/_static/image5.png)](creating-unit-tests-for-asp-net-mvc-applications-vb/_static/image4.png)

**図 02**: 成功! ([クリックすると、フルサイズの画像が表示](creating-unit-tests-for-asp-net-mvc-applications-vb/_static/image6.png)される)

## <a name="testing-the-view-data-returned-by-a-controller"></a>コントローラーによって返されるビューデータのテスト

MVC コントローラーは、 *`View Data`* と呼ばれるものを使用してビューにデータを渡します。 たとえば、`ProductController Details()` アクションを呼び出すときに、特定の製品の詳細を表示したいとします。 その場合は、モデルで定義されている `Product` クラスのインスタンスを作成し、`View Data`を利用して、そのインスタンスを `Details` ビューに渡すことができます。

一覧3の変更された `ProductController` には、製品を返す更新された `Details()` アクションが含まれています。

**リスト3– `ProductController.vb`**

[!code-vb[Main](creating-unit-tests-for-asp-net-mvc-applications-vb/samples/sample5.vb)]

まず、`Details()` アクションは、ラップトップコンピューターを表す `Product` クラスの新しいインスタンスを作成します。 次に、`Product` クラスのインスタンスが、2番目のパラメーターとして `View()` メソッドに渡されます。

単体テストを記述して、予想されるデータがビューデータに含まれているかどうかをテストできます。 リスト4の単体テストでは、`ProductController Details()` アクションメソッドを呼び出すと、ラップトップコンピューターを表す製品が返されるかどうかをテストします。

**リスト4– `ProductControllerTest.vb`**

[!code-vb[Main](creating-unit-tests-for-asp-net-mvc-applications-vb/samples/sample6.vb)]

リスト4では、`TestDetailsView()` メソッドは、`Details()` メソッドを呼び出すことによって返されたビューデータをテストします。 `ViewData` は、`Details()` メソッドを呼び出すことによって返される `ViewResult` のプロパティとして公開されます。 `ViewData.Model` プロパティには、ビューに渡される製品が含まれています。 このテストでは、単に、ビューデータに含まれている製品に "ラップトップ" という名前が付いていることを確認します。

## <a name="testing-the-action-result-returned-by-a-controller"></a>コントローラーによって返されるアクションの結果のテスト

より複雑なコントローラーアクションは、コントローラーアクションに渡されるパラメーターの値に応じて、さまざまな種類のアクション結果を返す可能性があります。 コントローラーアクションは、`ViewResult`、`RedirectToRouteResult`、`JsonResult`など、さまざまな種類のアクション結果を返すことができます。

たとえば、リスト5の変更された `Details()` アクションでは、有効な製品 Id をアクションに渡すと、`Details` ビューが返されます。 無効な製品 Id (値が1未満の Id) を渡した場合、`Index()` アクションにリダイレクトされます。

**リスト5– `ProductController.vb`**

[!code-vb[Main](creating-unit-tests-for-asp-net-mvc-applications-vb/samples/sample7.vb)]

リスト6の単体テストを使用して、`Details()` アクションの動作をテストできます。 リスト6の単体テストでは、値-1 の Id が `Details()` メソッドに渡されたときに `Index` ビューにリダイレクトされることを確認します。

**リスト6– `ProductControllerTest.vb`**

[!code-vb[Main](creating-unit-tests-for-asp-net-mvc-applications-vb/samples/sample8.vb)]

コントローラーアクションで `RedirectToAction()` メソッドを呼び出すと、コントローラーアクションは `RedirectToRouteResult`を返します。 テストでは、`RedirectToRouteResult` が `Index`という名前のコントローラーアクションにユーザーをリダイレクトするかどうかを確認します。

## <a name="summary"></a>要約

このチュートリアルでは、MVC コントローラーアクションの単体テストを作成する方法について学習しました。 まず、コントローラーアクションによって、右側のビューが返されるかどうかを確認する方法を学習しました。 `ViewResult.ViewName` プロパティを使用して、ビューの名前を確認する方法について学習しました。

次に、`View Data`の内容をテストする方法について説明します。 コントローラーアクションを呼び出した後に `View Data` で正しい製品が返されたかどうかを確認する方法について学習しました。

最後に、さまざまな種類のアクションの結果がコントローラーアクションから返されたかどうかをテストする方法について説明しました。 コントローラーが `ViewResult` と `RedirectToRouteResult`のどちらを返すかをテストする方法について学習しました。

> [!div class="step-by-step"]
> [前へ](creating-unit-tests-for-asp-net-mvc-applications-cs.md)
