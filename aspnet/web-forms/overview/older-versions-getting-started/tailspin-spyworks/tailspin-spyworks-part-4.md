---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-4
title: 'パート 4: 製品の一覧表示 |Microsoft Docs'
author: JoeStagner
description: このチュートリアルシリーズでは、Tailspin Spyworks サンプルアプリケーションを構築するために実行するすべての手順について詳しく説明します。 パート4では、GridView で製品を一覧表示する方法について説明します。
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 4fab47d5-a6ec-4fdc-91f0-651a093a24b9
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-4
msc.type: authoredcontent
ms.openlocfilehash: 7af1b8afa2ecc8df9846f2edd2091b26b93a811c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78457282"
---
# <a name="part-4-listing-products"></a>パート 4: 製品の一覧表示

[Joe Stagner](https://github.com/JoeStagner)

> Tailspin Spyworks は、.NET プラットフォーム用の強力でスケーラブルなアプリケーションを簡単に作成する方法を示しています。 ASP.NET 4 の優れた新機能を使用して、ショッピング、チェックアウト、管理などのオンラインストアを構築する方法を示しています。
> 
> このチュートリアルシリーズでは、Tailspin Spyworks サンプルアプリケーションを構築するために実行するすべての手順について詳しく説明します。 パート4では、GridView コントロールで製品を一覧表示する方法について説明します。

## <a id="_Toc260221670"></a>GridView コントロールを使用した製品の一覧表示

ソリューションを右クリックし、[追加]、[新しい項目] の順に選択して、製品リストの .aspx ページの実装を開始しましょう。

![](tailspin-spyworks-part-4/_static/image1.jpg)

[マスターページを使用した Web フォーム] を選択し、製品のリスト .aspx のページ名を入力します。

[追加] をクリックします。

![](tailspin-spyworks-part-4/_static/image2.jpg)

次に、[スタイル] フォルダーを選択します。このフォルダーは、[フォルダーの内容] ウィンドウから選択します。

![](tailspin-spyworks-part-4/_static/image3.jpg)

[Ok] をクリックしてページを作成します。

次に示すように、データベースに製品データが入力されます。

![](tailspin-spyworks-part-4/_static/image4.jpg)

ページが作成された後、もう一度エンティティデータソースを使用してその製品データにアクセスしますが、この場合は、Product エンティティを選択する必要があります。また、返される項目を、選択したカテゴリの項目のみに制限する必要があります。

これを実現するには、WHERE 句を自動生成するように EntityDataSource に指示し、where-object パラメーターを指定します。

「製品カテゴリメニュー」でメニュー項目を作成したときに、各リンクの QueryString に CategoryID を追加して、リンクを動的に構築したことを思い出してください。 このクエリ文字列パラメーターから WHERE パラメーターを派生させるように、エンティティデータソースに指示します。

[!code-aspx[Main](tailspin-spyworks-part-4/samples/sample1.aspx)]

次に、製品の一覧を表示するように ListView コントロールを構成します。 最適なショッピング体験を作成するには、ListVew に表示される個々の製品ごとに簡潔な機能をいくつか圧縮します。

- 製品名は、製品の詳細ビューへのリンクになります。
- 製品の価格が表示されます。
- 製品のイメージが表示され、アプリケーションのカタログイメージディレクトリからイメージが動的に選択されます。
- 特定の製品をすぐにショッピングカートに追加するためのリンクを含めます。

ListView コントロールインスタンスのマークアップを次に示します。

[!code-aspx[Main](tailspin-spyworks-part-4/samples/sample2.aspx)]

表示されている製品ごとに複数のリンクを動的に構築しています。

また、独自の新しいページをテストする前に、次のように製品カタログイメージのディレクトリ構造を作成する必要があります。

![](tailspin-spyworks-part-4/_static/image1.png)

製品イメージにアクセスできるようになったら、製品リストページをテストできます。

![](tailspin-spyworks-part-4/_static/image5.jpg)

サイトのホームページから、カテゴリ一覧のリンクの1つをクリックします。

![](tailspin-spyworks-part-4/_static/image6.jpg)

次に、ProductDetails .aspx ページと AddToCart 機能を実装する必要があります。

先ほどと同じように、[ファイル&gt;新規] を使用して、サイトマスターページを使用してページ名 ProductDetails .aspx を作成します。

次に、EntityDataSource コントロールを使用してデータベース内の特定の製品レコードにアクセスします。 ASP.NET FormView コントロールを使用して、次のように製品データを表示します。

[!code-aspx[Main](tailspin-spyworks-part-4/samples/sample3.aspx)]

書式設定が少し楽しいものであるかどうかは気にしないでください。 上のマークアップは、後で実装するいくつかの機能について、表示レイアウトの中にスペースを残します。

ショッピングカートは、アプリケーション内でより複雑なロジックを表します。 作業を開始するには、MyShoppingCart という名前のページを作成するために、ファイル&gt;New を使用します。

ShoppingCart という名前は選択していないことに注意してください。

このデータベースには、"ShoppingCart" という名前のテーブルが含まれています。 Entity Data Model 生成されると、データベース内の各テーブルに対してクラスが作成されます。 したがって、Entity Data Model によって、"ShoppingCart" という名前のエンティティクラスが生成されます。 このモデルを編集して、ショッピングカートの実装にその名前を使用できるようにすることも、ニーズに合わせて拡張することもできますが、競合を回避する名前を選択するだけで済みます。

また、簡単なショッピングカートを作成し、ショッピングカートの表示でショッピングカートのロジックを埋め込むことにも注意してください。 また、まったく別のビジネス層にショッピングカートを実装することもできます。

> [!div class="step-by-step"]
> [前へ](tailspin-spyworks-part-3.md)
> [次へ](tailspin-spyworks-part-5.md)
