---
uid: mvc/overview/getting-started/introduction/examining-the-details-and-delete-methods
title: Details メソッドと Delete メソッドの検証 |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 03/26/2015
ms.assetid: f1d2a916-626c-4a54-8df4-77e6b9fff355
msc.legacyurl: /mvc/overview/getting-started/introduction/examining-the-details-and-delete-methods
msc.type: authoredcontent
ms.openlocfilehash: da06815b5c1d76a939fdfb77ce11774081dfb881
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2020
ms.locfileid: "77456401"
---
# <a name="examining-the-details-and-delete-methods"></a>Details メソッドと Delete メソッドの確認

[Rick Anderson](https://twitter.com/RickAndMSFT)

[!INCLUDE [Tutorial Note](index.md)]

チュートリアルのこの部分では、自動的に生成された `Details` と `Delete` メソッドを確認します。

## <a name="examining-the-details-and-delete-methods"></a>Details メソッドと Delete メソッドの確認

`Movie` コントローラーを開き、`Details` メソッドを確認します。

![](examining-the-details-and-delete-methods/_static/image1.png)

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample1.cs)]

このアクションメソッドを作成した MVC スキャフォールディングエンジンは、メソッドを呼び出す HTTP 要求を示すコメントを追加します。 この例では、3つの URL セグメント、`Movies` コントローラー、`Details` メソッド、および `ID` 値を含む `GET` 要求です。

Code First により、`Find` メソッドを使用してデータを簡単に検索できます。 メソッドに組み込まれている重要なセキュリティ機能として、コードがコードで何かを実行しようとする前に、`Find` メソッドがムービーを検出したことを検証することが挙げられます。 たとえば、ハッカーは、リンクによって作成された URL を `http://localhost:xxxx/Movies/Details/1` から `http://localhost:xxxx/Movies/Details/12345` (または実際のムービーを表さない他の値) に変更することによって、サイトにエラーを持ち込む可能性があります。 Null ムービーを確認しなかった場合、null ムービーはデータベースエラーになります。

`Delete` メソッドと `DeleteConfirmed` メソッドを調べます。

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample2.cs?highlight=17)]

HTTP GET `Delete` メソッドは、指定されたムービーを削除しないので、削除を送信 (`HttpPost`) できるムービーのビューを返します。 GET 要求の応答で削除操作を実行すると (さらに言えば、編集操作、作成操作、データを変更するその他のあらゆる操作を実行すると)、セキュリティに穴が空きます。 詳細については、「Stephen Walther's blog entry ASP.NET MVC Tip #46」を参照してください。[削除リンクは、セキュリティホールを作成するため、使用しないで](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx)ください。

データを削除する `HttpPost` メソッドの名前は「`DeleteConfirmed`」になり、HTTP POST メソッドに一意のシグネチャまたは名前が与えられます。 2 つのメソッド シグネチャは下の画像のようになります。

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample3.cs)]

共通言語ランタイム (CLR) は、オーバーロードのメソッドに一意のパラメーター シグネチャを持つことを要求します (メソッド名は同じであるが、パラメーターの一覧が異なる)。 ただし、ここでは2つの Delete メソッドが必要です。1つは GET、もう1つは同じパラメーターシグネチャを持ちます。 (いずれも、1 つの整数をパラメーターとして受け取る必要があります。)

これを並べ替えるために、いくつかのことを行うことができます。 1つは、メソッドに異なる名前を付けることです。 先の例では、スキャフォールディング メカニズムがこれを行いました。 ただし、これは小さな問題を引き起こします。ASP.NET が URL のセグメントをアクション メソッドに名前でマッピングします。メソッドの名前を変更すると、通常、ルーティングでそのメソッドが見つからなくなります。 この解決策はこの例で確認できます。`ActionName("Delete")` 属性を `DeleteConfirmed` メソッドに追加しています。 これにより、ルーティングシステムのマッピングが効果的に実行されるため、POST 要求の */Delete/* が含まれている URL が `DeleteConfirmed` メソッドを見つけることができます。

同じ名前とシグネチャを持つメソッドの問題を回避するもう1つの一般的な方法は、POST メソッドのシグネチャを意図的に変更して、未使用のパラメーターを含めることです。 たとえば、一部の開発者は、POST メソッドに渡される `FormCollection` パラメーター型を追加し、パラメーターを使用しないようにします。

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample4.cs)]

## <a name="summary"></a>要約

これで、ローカル DB データベースにデータを格納する完全な ASP.NET MVC アプリケーションが完成しました。 ムービーの作成、読み取り、更新、削除、検索を行うことができます。

![](examining-the-details-and-delete-methods/_static/image2.png)

## <a name="next-steps"></a>次の手順

Web アプリケーションをビルドしてテストしたら、次の手順として、インターネット経由で他のユーザーが使用できるようにします。 これを行うには、それを web ホスティングプロバイダーに展開する必要があります。 Microsoft では、[無料の Azure 試用版アカウント](https://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A443DD604)で、最大10個の web サイト向けの無料の web ホスティングを提供しています。 次に、 [「Azure へのメンバーシップ、OAuth、SQL Database を使用した Secure ASP.NET MVC アプリのデプロイ](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)」を参照してください。 優れたチュートリアルとして、Tom Dykstra の中間レベルで、 [ASP.NET MVC アプリケーションの Entity Framework データモデルを作成して](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)います。 [Stackoverflow](http://stackoverflow.com/help)と[ASP.NET MVC フォーラム](https://forums.asp.net/1146.aspx)は、質問をする絶好の場所です。 最新[のチュートリアル](https://twitter.com/RickAndMSFT)で更新プログラムを入手できるように、twitter でフォローします。

フィードバックは歓迎します。

— [Rick Anderson](https://blogs.msdn.com/rickAndy) twitter: [@RickAndMSFT](https://twitter.com/RickAndMSFT)  
— [Scott マン Selman](http://www.hanselman.com/blog/) twitter: [@shanselman](https://twitter.com/shanselman)

> [!div class="step-by-step"]
> [[戻る]](adding-validation.md)
