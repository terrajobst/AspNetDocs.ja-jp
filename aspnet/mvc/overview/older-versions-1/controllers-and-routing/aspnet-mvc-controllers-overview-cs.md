---
uid: mvc/overview/older-versions-1/controllers-and-routing/aspnet-mvc-controllers-overview-cs
title: ASP.NET MVC コントローラーの概要C#() |Microsoft Docs
author: StephenWalther
description: このチュートリアルでは、Stephen Walther が、MVC コントローラーの ASP.NET について説明します。 新しいコントローラーを作成し、さまざまな種類のアクションを返す方法について説明します。
ms.author: riande
ms.date: 02/16/2008
ms.assetid: b985c49a-3668-455c-a366-f85f6bc64b12
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/aspnet-mvc-controllers-overview-cs
msc.type: authoredcontent
ms.openlocfilehash: 1a287b37742400a17c2ed53cfd00bfb053b4f3d2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78437680"
---
# <a name="aspnet-mvc-controller-overview-c"></a>ASP.NET MVC コントローラーの概要 (C#)

[Stephen Walther](https://github.com/StephenWalther)

> このチュートリアルでは、Stephen Walther が、MVC コントローラーの ASP.NET について説明します。 新しいコントローラーを作成し、さまざまな種類のアクション結果を返す方法について説明します。

このチュートリアルでは、ASP.NET MVC コントローラー、コントローラーアクション、およびアクションの結果について説明します。 このチュートリアルを完了すると、ユーザーが ASP.NET MVC web サイトと対話する方法を制御するためにコントローラーがどのように使用されるかを理解できます。

## <a name="understanding-controllers"></a>コントローラーについて

MVC コントローラーは、ASP.NET MVC web サイトに対して行われた要求に応答する役割を担います。 各ブラウザー要求は、特定のコントローラーにマップされます。 たとえば、ブラウザーのアドレスバーに次の URL を入力したとします。

`http://localhost/Product/Index/3`

この場合、ProductController という名前のコントローラーが呼び出されます。 ProductController は、ブラウザー要求に対する応答を生成します。 たとえば、コントローラーが特定のビューをブラウザーに返す場合や、コントローラーがユーザーを別のコントローラーにリダイレクトする場合があります。

リスト1には、ProductController という名前のシンプルなコントローラーが含まれています。

**Listing1 (productコントローラー)**

[!code-csharp[Main](aspnet-mvc-controllers-overview-cs/samples/sample1.cs)]

リスト1からわかるように、コントローラーはクラス (Visual Basic .NET またはC#クラス) にすぎません。 コントローラーは、基本の System.web. Mvc クラスから派生するクラスです。 コントローラーはこの基本クラスを継承するため、コントローラーはいくつかの便利なメソッドを無料で継承します (これらのメソッドについては後で説明します)。

## <a name="understanding-controller-actions"></a>コントローラーアクションについて

コントローラーは、コントローラーアクションを公開します。 アクションは、ブラウザーのアドレスバーに特定の URL を入力したときに呼び出されるコントローラー上のメソッドです。 たとえば、次の URL に対して要求を行うとします。

`http://localhost/Product/Index/3`

この場合、ProductController クラスで Index () メソッドが呼び出されます。 Index () メソッドは、コントローラーアクションの一例です。

コントローラーアクションは、コントローラークラスのパブリックメソッドである必要があります。 C#既定では、メソッドはプライベートメソッドです。 コントローラークラスに追加したパブリックメソッドは、コントローラーアクションとして自動的に公開されることに注意してください (コントローラーアクションは、ブラウザーのアドレスバーに適切な URL を入力するだけで、宇宙の任意のユーザーによって呼び出すことができるため、注意する必要があります)。

コントローラーアクションによって満たされる必要がある追加の要件がいくつかあります。 コントローラーアクションとして使用されているメソッドをオーバーロードすることはできません。 さらに、コントローラーアクションを静的メソッドにすることはできません。 それ以外の場合は、任意のメソッドをコントローラーアクションとしてのみ使用できます。

## <a name="understanding-action-results"></a>アクションの結果について

コントローラーアクションは、*アクション結果*と呼ばれるものを返します。 アクションの結果は、ブラウザー要求に応じてコントローラーアクションが返すものです。

ASP.NET MVC フレームワークでは、次のようないくつかの種類のアクションの結果をサポートしています。

1. ViewResult-HTML およびマークアップを表します。
2. EmptyResult-結果を表しません。
3. RedirectResult-新しい URL へのリダイレクトを表します。
4. JsonResult-AJAX アプリケーションで使用できる JavaScript Object Notation の結果を表します。
5. JavaScriptResult-JavaScript スクリプトを表します。
6. ContentResult-テキストの結果を表します。
7. FileContentResult-ダウンロード可能なファイルを表します (バイナリコンテンツを含む)。
8. FilePathResult-ダウンロード可能なファイル (パスを含む) を表します。
9. FileStreamResult-ダウンロード可能なファイル (ファイルストリームを含む) を表します。

これらのアクションの結果はすべて、基本 ActionResult クラスから継承されます。

ほとんどの場合、コントローラーアクションは ViewResult を返します。 たとえば、リスト2のインデックスコントローラーアクションは ViewResult を返します。

**リスト 2-コントローラー (& c)**

[!code-csharp[Main](aspnet-mvc-controllers-overview-cs/samples/sample2.cs)]

アクションから ViewResult が返されると、ブラウザーに HTML が返されます。 リスト2の Index () メソッドは、ブラウザーに Index という名前のビューを返します。

リスト2の Index () アクションから ViewResult () が返されないことに注意してください。 代わりに、コントローラーの基底クラスの View () メソッドが呼び出されます。 通常、アクションの結果は直接返されません。 代わりに、コントローラーの基本クラスの次のいずれかのメソッドを呼び出します。

1. View-ViewResult アクションの結果を返します。
2. リダイレクト-RedirectResult アクションの結果を返します。
3. RedirectToAction-RedirectToRouteResult アクションの結果を返します。
4. RedirectToRoute-RedirectToRouteResult アクションの結果を返します。
5. Json-JsonResult アクションの結果を返します。
6. JavaScriptResult-JavaScriptResult を返します。
7. Content-ContentResult アクションの結果を返します。
8. File-メソッドに渡されたパラメーターに応じて、FileContentResult、FilePathResult、または FileStreamResult を返します。

そのため、ビューをブラウザーに返す場合は、View () メソッドを呼び出します。 コントローラーアクション間でユーザーをリダイレクトする場合は、RedirectToAction () メソッドを呼び出します。 たとえば、リスト3の Details () アクションは、Id パラメーターに値があるかどうかに応じて、ビューを表示するか、ユーザーを Index () アクションにリダイレクトします。

**リスト 3-CustomerController.cs**

[!code-csharp[Main](aspnet-mvc-controllers-overview-cs/samples/sample3.cs)]

ContentResult アクションの結果は特殊です。 ContentResult アクションの結果を使用して、アクションの結果をプレーンテキストとして返すことができます。 たとえば、リスト4の Index () メソッドは、HTML としてではなく、プレーンテキストとしてメッセージを返します。

**リスト 4-コントローラーの一覧 (& c)**

[!code-csharp[Main](aspnet-mvc-controllers-overview-cs/samples/sample4.cs)]

StatusController. Index () アクションを呼び出すと、ビューは返されません。 代わりに、生のテキスト "Hello World!" がブラウザーに返されます。

コントローラーアクションが、アクション結果ではない結果 (日付や整数など) を返す場合、結果は ContentResult に自動的にラップされます。 たとえば、リスト5のワークコントローラーの Index () アクションが呼び出されると、その日付は ContentResult として自動的に返されます。

**リスト 5-WorkController.cs**

[!code-csharp[Main](aspnet-mvc-controllers-overview-cs/samples/sample5.cs)]

リスト5の Index () アクションは、DateTime オブジェクトを返します。 ASP.NET MVC フレームワークは、DateTime オブジェクトを文字列に変換し、ContentResult の DateTime 値を自動的にラップします。 ブラウザーは、日付と時刻をプレーンテキストとして受け取ります。

## <a name="summary"></a>まとめ

このチュートリアルの目的は、ASP.NET MVC コントローラー、コントローラーアクション、およびコントローラーアクションの結果の概念を紹介することでした。 最初のセクションでは、ASP.NET MVC プロジェクトに新しいコントローラーを追加する方法について学習しました。 次に、コントローラーのパブリックメソッドをコントローラーアクションとして universe に公開する方法について学習しました。 最後に、コントローラーアクションから返される可能性があるさまざまな種類のアクションの結果について説明しました。 特に、ViewResult、RedirectToActionResult、および ContentResult をコントローラーアクションから返す方法について説明しました。

> [!div class="step-by-step"]
> [前へ](creating-an-action-vb.md)
> [次へ](creating-custom-routes-cs.md)
