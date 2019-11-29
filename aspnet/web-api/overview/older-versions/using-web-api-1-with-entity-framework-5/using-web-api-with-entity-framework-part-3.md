---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-3
title: 'パート 3: 管理コントローラーの作成 |Microsoft Docs'
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: 6b9ae3c4-0274-4170-a1bb-9df9c546b2a9
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-3
msc.type: authoredcontent
ms.openlocfilehash: f39be7a84e85db93487d246e9f8cb59c401fe5ce
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600041"
---
# <a name="part-3-creating-an-admin-controller"></a>パート 3: 管理コントローラーの作成

[Mike Wasson](https://github.com/MikeWasson)

[完成したプロジェクトのダウンロード](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-an-admin-controller"></a>管理コントローラーを追加する

このセクションでは、CRUD (作成、読み取り、更新、および削除) 操作をサポートする Web API コントローラーを製品に追加します。 コントローラーは Entity Framework を使用してデータベース層と通信します。 このコントローラーを使用できるのは管理者のみです。 お客様は、別のコントローラーを通じて製品にアクセスします。

ソリューションエクスプローラーで、Controllers フォルダーを右クリックします。 **[追加]** 、 **[コントローラー]** の順に選択します。

![](using-web-api-with-entity-framework-part-3/_static/image1.png)

**[コントローラーの追加]** ダイアログで、コントローラーに `AdminController`という名前を指定します。 **[テンプレート]** で、Entity Framework&quot;を使用して、読み取り/書き込みアクションを含む &quot;API コントローラーを選択します。 **モデルクラス** で、Product (productstore) を選択します。 **[データコンテキスト]** で、[新しいデータコンテキスト&gt;の&lt;] を選択します。

![](using-web-api-with-entity-framework-part-3/_static/image2.png)

> [!NOTE]
> モデル**クラス**のドロップダウンにモデルクラスが表示されない場合は、プロジェクトをコンパイルしたことを確認してください。 Entity Framework はリフレクションを使用するため、コンパイルされたアセンブリが必要です。

[新しいデータコンテキスト&gt;を&lt;] を選択すると、 **[新しいデータコンテキスト]** ダイアログボックスが開きます。 データコンテキストに `ProductStore.Models.OrdersContext`名前を指定します。

![](using-web-api-with-entity-framework-part-3/_static/image3.png)

**[OK]** をクリックして、 **[新しいデータコンテキスト]** ダイアログボックスを閉じます。 **[コントローラーの追加]** ダイアログで、 **[追加]** をクリックします。

プロジェクトに追加された内容は次のとおりです。

- **Dbcontext**から派生する `OrdersContext` という名前のクラス。 このクラスは、POCO モデルとデータベース間の接着を提供します。
- `AdminController`という名前の Web API コントローラー。 このコントローラーは `Product` インスタンスに対する CRUD 操作をサポートします。 `OrdersContext` クラスを使用して Entity Framework と通信します。
- Web.config ファイル内の新しいデータベース接続文字列。

![](using-web-api-with-entity-framework-part-3/_static/image4.png)

OrdersContext.cs ファイルを開きます。 コンストラクターはデータベース接続文字列の名前を指定することに注意してください。 この名前は、web.config に追加された接続文字列を示します。

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample1.cs)]

`OrdersContext` クラスに次のプロパティを追加します。

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample2.cs)]

**Dbset**は、クエリ可能なエンティティのセットを表します。 `OrdersContext` クラスの完全な一覧を次に示します。

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample3.cs)]

`AdminController` クラスは、基本的な CRUD 機能を実装する5つのメソッドを定義します。 各メソッドは、クライアントが呼び出すことができる URI に対応します。

| コントローラーメソッド | 説明 | URI | HTTP メソッド |
| --- | --- | --- | --- |
| GetProducts | すべての製品を取得します。 | api/製品 | GET |
| GetProduct | ID で製品を検索します。 | api/製品/*id* | GET |
| PutProduct | 製品を更新します。 | api/製品/*id* | PUT |
| PostProduct | 新しい製品を作成します。 | api/製品 | 投稿 |
| DeleteProduct | 製品を削除します。 | api/製品/*id* | Del |

各メソッドは、`OrdersContext` を呼び出してデータベースにクエリを実行します。 コレクション (PUT、POST、および DELETE) を変更するメソッドは、データベースへの変更を保持するために `db.SaveChanges` を呼び出します。 コントローラーは HTTP 要求ごとに作成され、破棄されます。そのため、メソッドが返される前に変更を保持する必要があります。

## <a name="add-a-database-initializer"></a>データベース初期化子の追加

Entity Framework には、起動時にデータベースを設定したり、モデルが変更されるたびに自動的にデータベースを再作成したりできる便利な機能があります。 この機能は、モデルを変更した場合でも、常にテストデータがあるため、開発時に便利です。

ソリューションエクスプローラーで、[モデル] フォルダーを右クリックし、`OrdersContextInitializer`という名前の新しいクラスを作成します。 次の実装を貼り付けます。

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample4.cs)]

**Dropcreatedatabaseifmodelchanges**クラスから継承することにより、モデルクラスを変更するたびにデータベースを削除するように Entity Framework に指示します。 Entity Framework によってデータベースが作成 (または再作成) されるときに、 **Seed**メソッドを呼び出してテーブルを設定します。 **Seed**メソッドを使用して、いくつかのサンプル製品と注文例を追加します。

この機能はテストに適していますが、実稼働環境では**Dropcreatedatabaseifmodelchanges**クラスを使用しないでください。これは、他のユーザーがモデルクラスを変更した場合にデータが失われる可能性があるためです。

次に、global.asax を開き、次のコードを**Application\_Start**メソッドに追加します。

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample5.cs)]

## <a name="send-a-request-to-the-controller"></a>コントローラーに要求を送信する

この時点では、クライアントコードは作成されていませんが、web ブラウザーまたは[Fiddler](http://www.fiddler2.com/fiddler2/)などの HTTP デバッグツールを使用して web API を呼び出すことができます。 Visual Studio で、F5 キーを押してデバッグを開始します。 Web ブラウザーで `http://localhost:*portnum*/`が開きます。ここで、 *portnum*はいくつかのポート番号です。

HTTP 要求を "`http://localhost:*portnum*/api/admin`に送信します。 最初の要求が完了するまでに時間がかかることがあります。これは Entity Framework がデータベースの作成とシードを行う必要があるためです。 応答は次のようになります。

[!code-console[Main](using-web-api-with-entity-framework-part-3/samples/sample6.cmd)]

> [!div class="step-by-step"]
> [前へ](using-web-api-with-entity-framework-part-2.md)
> [次へ](using-web-api-with-entity-framework-part-4.md)
