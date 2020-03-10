---
uid: mvc/overview/older-versions-1/controllers-and-routing/asp-net-mvc-routing-overview-vb
title: ASP.NET MVC ルーティングの概要 (VB) |Microsoft Docs
author: StephenWalther
description: このチュートリアルでは、Stephen Walther は、ASP.NET MVC フレームワークがブラウザー要求をコントローラーアクションにマップする方法を示しています。
ms.author: riande
ms.date: 08/19/2008
ms.assetid: 4bc8d19a-80f1-44b4-adbf-95ed22d691ca
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/asp-net-mvc-routing-overview-vb
msc.type: authoredcontent
ms.openlocfilehash: ed043d76b89ce31945cf3423b0c5afca9383cc21
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486898"
---
# <a name="aspnet-mvc-routing-overview-vb"></a>ASP.NET MVC ルーティング概要 (VB)

[Stephen Walther](https://github.com/StephenWalther)

> このチュートリアルでは、Stephen Walther は、ASP.NET MVC フレームワークがブラウザー要求をコントローラーアクションにマップする方法を示しています。

このチュートリアルでは、 *ASP.NET Routing*という名前のすべての ASP.NET MVC アプリケーションの重要な機能を紹介します。 ASP.NET ルーティングモジュールは、受信ブラウザー要求を特定の MVC コントローラーアクションにマップする役割を担います。 このチュートリアルを終了すると、標準のルートテーブルが要求をコントローラーアクションにどのようにマップするかを理解できるようになります。

## <a name="using-the-default-route-table"></a>既定のルートテーブルを使用する

新しい ASP.NET MVC アプリケーションを作成する場合、アプリケーションは既に ASP.NET Routing を使用するように構成されています。 ASP.NET ルーティングは2か所で設定されます。

まず、アプリケーションの Web 構成ファイル (web.config ファイル) で ASP.NET ルーティングが有効になっています。 ルーティングに関連する構成ファイルには、次の4つのセクションがあります。-system.servicemodel セクション、system.web. httpHandlers セクション、system.webserver. modules セクション、および system.webserver. ハンドラーセクションを参照してください。 これらのセクションを削除しないように注意してください。これらのセクションでは、ルーティングが機能しなくなります。

2つ目は、さらに重要なのは、アプリケーションの global.asax ファイルにルートテーブルを作成することです。 Global.asax ファイルは、ASP.NET アプリケーションライフサイクルイベントのイベントハンドラーを含む特殊なファイルです。 ルートテーブルは、アプリケーションの開始イベント時に作成されます。

リスト1のファイルには、ASP.NET MVC アプリケーションの既定の global.asax ファイルが含まれています。

**リスト 1-global.asax**

[!code-vb[Main](asp-net-mvc-routing-overview-vb/samples/sample1.vb)]

MVC アプリケーションを初めて起動すると、アプリケーション\_Start () メソッドが呼び出されます。 次に、このメソッドは RegisterRoutes () メソッドを呼び出します。 RegisterRoutes () メソッドは、ルートテーブルを作成します。

既定のルートテーブルには、1つのルートが含まれています (既定)。 既定のルートは、URL の最初のセグメントをコントローラー名に、URL の2番目のセグメントをコントローラーアクションに、3番目のセグメントを**id**という名前のパラメーターにマップします。

Web ブラウザーのアドレスバーに次の URL を入力したとします。

/Home/Index/3

既定のルートは、この URL を次のパラメーターにマップします。

- controller = Home

- action = Index

- id = 3

URL/Home/Index/3 を要求すると、次のコードが実行されます。

HomeController.Index(3)

既定のルートには、3つのパラメーターすべての既定値が含まれています。 コントローラーを指定しない場合、コントローラーパラメーターの既定値は**Home**です。 アクションを指定しない場合、アクションパラメーターの既定値は**Index**です。 最後に、id を指定しない場合、id パラメーターの既定値は空の文字列になります。

既定のルートでは、Url をコントローラーアクションにマップする方法の例をいくつか見てみましょう。 ブラウザーのアドレスバーに次の URL を入力したとします。

/Home

既定のルートパラメーターの既定値が指定されているため、この URL を入力すると、リスト2の HomeController クラスの Index () メソッドが呼び出されます。

**リスティング 2-HomeController**

[!code-vb[Main](asp-net-mvc-routing-overview-vb/samples/sample2.vb)]

リスト2では、HomeController クラスに、Id という名前の単一のパラメーターを受け取る Index () という名前のメソッドが含まれています。URL/Home を使用すると、Id パラメーターの値として Nothing を指定して Index () メソッドが呼び出されます。

MVC フレームワークがコントローラーアクションを呼び出す方法により、URL/Home も、リスト3の HomeController クラスの Index () メソッドに一致します。

**リスト 3-HomeController (パラメーターなしのインデックスアクション)**

[!code-vb[Main](asp-net-mvc-routing-overview-vb/samples/sample3.vb)]

リスト3の Index () メソッドは、パラメーターを受け取りません。 URL/Home によって、この Index () メソッドが呼び出されます。 また、URL /Home/Index/3 は、(Id は無視されます) このメソッドを呼び出します。

また、URL/Home は、リスト4の HomeController クラスの Index () メソッドにも一致します。

**リスト 4-HomeController (null 値を許容するパラメーターを持つインデックスアクション)**

[!code-vb[Main](asp-net-mvc-routing-overview-vb/samples/sample4.vb)]

リスティング4では、Index () メソッドに1つの整数パラメーターがあります。 パラメーターは null 許容型パラメーターであるため (値は Nothing でもかまいません)、エラーを発生させることなくインデックス () を呼び出すことができます。

最後に、URL/Home を使用してリスト5の Index () メソッドを呼び出すと、Id パラメーターが null 許容パラメーターで*はない*ため、例外が発生します。 Index () メソッドを呼び出そうとすると、図1にエラーが表示されます。

**リスト 5-HomeController (Id パラメーターを持つインデックスアクション)**

[!code-vb[Main](asp-net-mvc-routing-overview-vb/samples/sample5.vb)]

[パラメーター値を要求するコントローラーアクションを呼び出す ![](asp-net-mvc-routing-overview-vb/_static/image1.jpg)](asp-net-mvc-routing-overview-vb/_static/image1.png)

**図 01**: パラメーター値を必要とするコントローラーアクションを呼び出す ([クリックすると、フルサイズのイメージが表示](asp-net-mvc-routing-overview-vb/_static/image2.png)されます)

URL /Home/Index/3 は一方で、リスト 5 でインデックスのコント ローラー アクションでうまくいきます。 要求/Home/Index/3 は、値が3の Id パラメーターを使用して Index () メソッドを呼び出します。

## <a name="summary"></a>まとめ

このチュートリアルの目的は、ASP.NET ルーティングの概要を説明することでした。 新しい ASP.NET MVC アプリケーションを使用して取得した既定のルートテーブルを調べます。 既定のルートでは、Url をコントローラーアクションにマップする方法を学習しました。

> [!div class="step-by-step"]
> [前へ](creating-an-action-cs.md)
> [次へ](understanding-action-filters-vb.md)
