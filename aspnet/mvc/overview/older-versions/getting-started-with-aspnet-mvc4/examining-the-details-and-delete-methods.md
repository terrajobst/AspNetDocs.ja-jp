---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/examining-the-details-and-delete-methods
title: Details メソッドと Delete メソッドの検証 |Microsoft Docs
author: Rick-Anderson
description: '注: このチュートリアルの更新バージョンは、ASP.NET MVC 5 と Visual Studio 2013 を使用するこちらで入手できます。 より安全で、より簡単にフォローとデモができます...'
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 11425ff3-09fc-4efa-be9a-b53bce503460
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/examining-the-details-and-delete-methods
msc.type: authoredcontent
ms.openlocfilehash: 37787a26f37473b9d36792a9f7715982cb274074
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457558"
---
# <a name="examining-the-details-and-delete-methods"></a>Details メソッドと Delete メソッドの確認

[Rick Anderson](https://twitter.com/RickAndMSFT)

> > [!NOTE]
> > このチュートリアルの更新バージョンは、ASP.NET MVC 5 と Visual Studio 2013 を使用する[こちらで](../../getting-started/introduction/getting-started.md)入手できます。 より安全で、より簡単にフォローし、より多くの機能を紹介します。

チュートリアルのこの部分では、自動的に生成された `Details` と `Delete` メソッドを確認します。

## <a name="examining-the-details-and-delete-methods"></a>Details メソッドと Delete メソッドの確認

`Movie` コントローラーを開き、`Details` メソッドを確認します。

![](examining-the-details-and-delete-methods/_static/image1.png)

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample1.cs)]

このアクションメソッドを作成した MVC スキャフォールディングエンジンは、メソッドを呼び出す HTTP 要求を示すコメントを追加します。 この例では、3つの URL セグメント、`Movies` コントローラー、`Details` メソッド、および `ID` 値を含む `GET` 要求です。

Code First により、`Find` メソッドを使用してデータを簡単に検索できます。 メソッドに組み込まれている重要なセキュリティ機能として、コードがコードで何かを実行しようとする前に、`Find` メソッドがムービーを検出したことを検証することが挙げられます。 たとえば、ハッカーは、リンクによって作成された URL を `http://localhost:xxxx/Movies/Details/1` から `http://localhost:xxxx/Movies/Details/12345` (または実際のムービーを表さない他の値) に変更することによって、サイトにエラーを持ち込む可能性があります。 Null ムービーを確認しなかった場合、null ムービーはデータベースエラーになります。

`Delete` メソッドと `DeleteConfirmed` メソッドを調べます。

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample2.cs?highlight=17)]

`HTTP Get``Delete` メソッドは、指定されたムービーを削除せず、削除を送信 (`HttpPost`) できるムービーのビューを返します。 GET 要求の応答で削除操作を実行すると (さらに言えば、編集操作、作成操作、データを変更するその他のあらゆる操作を実行すると)、セキュリティに穴が空きます。 詳細については、「Stephen Walther's blog entry ASP.NET MVC Tip #46」を参照してください。[削除リンクは、セキュリティホールを作成するため、使用しないで](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx)ください。

データを削除する `HttpPost` メソッドの名前は「`DeleteConfirmed`」になり、HTTP POST メソッドに一意のシグネチャまたは名前が与えられます。 2 つのメソッド シグネチャは下の画像のようになります。

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample3.cs)]

共通言語ランタイム (CLR) は、オーバーロードのメソッドに一意のパラメーター シグネチャを持つことを要求します (メソッド名は同じであるが、パラメーターの一覧が異なる)。 ただし、ここでは2つの Delete メソッドが必要です。1つは GET、もう1つは同じパラメーターシグネチャを持ちます。 (いずれも、1 つの整数をパラメーターとして受け取る必要があります。)

これを並べ替えるために、いくつかのことを行うことができます。 1つは、メソッドに異なる名前を付けることです。 先の例では、スキャフォールディング メカニズムがこれを行いました。 ただし、これは小さな問題を引き起こします。ASP.NET が URL のセグメントをアクション メソッドに名前でマッピングします。メソッドの名前を変更すると、通常、ルーティングでそのメソッドが見つからなくなります。 この解決策はこの例で確認できます。`ActionName("Delete")` 属性を `DeleteConfirmed` メソッドに追加しています。 これにより、ルーティングシステムのマッピングが効果的に実行されるため、POST 要求の<em>/Delete/</em>が含まれている URL が `DeleteConfirmed` メソッドを見つけることができます。

同じ名前とシグネチャを持つメソッドの問題を回避するもう1つの一般的な方法は、POST メソッドのシグネチャを意図的に変更して、未使用のパラメーターを含めることです。 たとえば、一部の開発者は、POST メソッドに渡される `FormCollection` パラメーター型を追加し、パラメーターを使用しないようにします。

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample4.cs)]

## <a name="summary"></a>要約

これで、ローカル DB データベースにデータを格納する完全な ASP.NET MVC アプリケーションが完成しました。 ムービーの作成、読み取り、更新、削除、検索を行うことができます。

![](examining-the-details-and-delete-methods/_static/image2.png)

## <a name="next-steps"></a>次の手順

Web アプリケーションをビルドしてテストしたら、次の手順として、インターネット経由で他のユーザーが使用できるようにします。 これを行うには、それを web ホスティングプロバイダーに展開する必要があります。 Microsoft では、無料の[Windows Azure 試用版アカウント](https://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A443DD604)で最大10個の web サイトを無料で提供しています。 次に、 [「メンバーシップ、OAuth、および SQL Database を使用する Secure ASP.NET MVC アプリを Windows Azure の Web サイトにデプロイ](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)する」をお勧めします。 優れたチュートリアルとして、Tom Dykstra の中間レベルで、 [ASP.NET MVC アプリケーションの Entity Framework データモデルを作成して](../../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)います。 [Stackoverflow](http://stackoverflow.com/help)と[ASP.NET MVC フォーラム](https://forums.asp.net/1146.aspx)は、質問をする絶好の場所です。 最新[のチュートリアル](https://twitter.com/RickAndMSFT)で更新プログラムを入手できるように、twitter でフォローします。

フィードバックは歓迎します。

— [Rick Anderson](https://blogs.msdn.com/rickAndy) twitter: [@RickAndMSFT](https://twitter.com/RickAndMSFT)  
— [Scott マン Selman](http://www.hanselman.com/blog/) twitter: [@shanselman](https://twitter.com/shanselman)

> [!div class="step-by-step"]
> [[戻る]](adding-validation-to-the-model.md)
