---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/calling-an-odata-service-from-a-net-client
title: .NET クライアントからの OData サービスの呼び出し (C#) |Microsoft Docs
author: MikeWasson
description: このチュートリアルでは、 C#クライアントアプリケーションから OData サービスを呼び出す方法について説明します。 チュートリアルで使用されているソフトウェアのバージョン Visual Studio 2013 (Visual S で動作します...
ms.author: riande
ms.date: 02/26/2014
ms.assetid: 6f448917-ad23-4dcc-9789-897fad74051b
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/calling-an-odata-service-from-a-net-client
msc.type: authoredcontent
ms.openlocfilehash: 6a289fcb843634eeeefef1e0767e04e0be8b6973
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600382"
---
# <a name="calling-an-odata-service-from-a-net-client-c"></a>.NET クライアントから OData サービスを呼び出す (C#)

[Mike Wasson](https://github.com/MikeWasson)

[完成したプロジェクトのダウンロード](https://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> このチュートリアルでは、 C#クライアントアプリケーションから OData サービスを呼び出す方法について説明します。
>
> ## <a name="software-versions-used-in-the-tutorial"></a>このチュートリアルで使用されているソフトウェアのバージョン
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013) (Visual Studio 2012 で動作)
> - [WCF Data Services クライアント ライブラリ](https://msdn.microsoft.com/library/cc668772.aspx)
> - Web API 2。 (例の OData サービスは Web API 2 を使用して構築されていますが、クライアントアプリケーションは Web API に依存していません)。

このチュートリアルでは、OData サービスを呼び出すクライアントアプリケーションを作成する手順について説明します。 OData サービスは、次のエンティティを公開します。

- `Product`
- `Supplier`
- `ProductRating`

![](calling-an-odata-service-from-a-net-client/_static/image1.png)

次の記事では、Web API で OData サービスを実装する方法について説明します。 (ただし、このチュートリアルを理解するために読む必要はありません)。

- [Web API 2 で OData エンドポイントを作成する](creating-an-odata-endpoint.md)
- [Web API 2 での OData エンティティの関係](working-with-entity-relations.md)
- [Web API 2 の OData アクション](odata-actions.md)

## <a name="generate-the-service-proxy"></a>サービスプロキシの生成

最初の手順では、サービスプロキシを生成します。 サービスプロキシは、OData サービスにアクセスするためのメソッドを定義する .NET クラスです。 プロキシは、メソッドの呼び出しを HTTP 要求に変換します。

![](calling-an-odata-service-from-a-net-client/_static/image2.png)

まず、Visual Studio で OData サービスプロジェクトを開きます。 CTRL キーを押しながら F5 キーを押して IIS Express でサービスをローカルに実行します。 Visual Studio によって割り当てられるポート番号など、ローカルアドレスをメモしておきます。 プロキシを作成するときに、このアドレスが必要になります。

次に、Visual Studio の別のインスタンスを開き、コンソールアプリケーションプロジェクトを作成します。 コンソールアプリケーションが OData クライアントアプリケーションになります。 (プロジェクトをサービスと同じソリューションに追加することもできます)。

> [!NOTE]
> 残りの手順では、コンソールプロジェクトを参照します。

ソリューションエクスプローラーで、 **[参照]** を右クリックし、 **[サービス参照の追加]** を選択します。

![](calling-an-odata-service-from-a-net-client/_static/image3.png)

**[サービス参照の追加]** ダイアログボックスで、OData サービスのアドレスを入力します。

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample1.cmd)]

ここで、 *port*はポート番号です。

[![](calling-an-odata-service-from-a-net-client/_static/image5.png)](calling-an-odata-service-from-a-net-client/_static/image4.png)

**[名前空間]** に「productservice」と入力します。 このオプションでは、プロキシクラスの名前空間を定義します。

**[検索]** をクリックします。 Visual Studio は、サービス内のエンティティを検出するために OData メタデータドキュメントを読み取ります。

[![](calling-an-odata-service-from-a-net-client/_static/image7.png)](calling-an-odata-service-from-a-net-client/_static/image6.png)

[ **OK]** をクリックして、プロキシクラスをプロジェクトに追加します。

![](calling-an-odata-service-from-a-net-client/_static/image8.png)

## <a name="create-an-instance-of-the-service-proxy-class"></a>サービスプロキシクラスのインスタンスを作成する

`Main` メソッド内で、次のようにプロキシクラスの新しいインスタンスを作成します。

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample2.cs)]

ここでも、サービスが実行されている実際のポート番号を使用します。 サービスをデプロイするときには、ライブサービスの URI を使用します。 プロキシを更新する必要はありません。

次のコードは、要求 Uri をコンソールウィンドウに出力するイベントハンドラーを追加します。 この手順は必須ではありませんが、各クエリの Uri を確認することが重要です。

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample3.cs)]

## <a name="query-the-service"></a>サービスのクエリを実行する

次のコードは、OData サービスから製品の一覧を取得します。

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample4.cs)]

HTTP 要求を送信したり、応答を解析したりするコードを記述する必要はありません。 このプロキシクラスは、 **foreach**ループ内の `Container.Products` コレクションを列挙すると、この処理を自動的に行います。

アプリケーションを実行すると、出力は次のようになります。

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample5.cmd)]

ID でエンティティを取得するには、`where` 句を使用します。

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample6.cs)]

このトピックの残りの部分では、サービスの呼び出しに必要なコードだけで `Main` 関数全体を表示しません。

## <a name="apply-query-options"></a>クエリオプションの適用

OData は、フィルター処理、並べ替え、データのページなどに使用できる[クエリオプション](../supporting-odata-query-options.md)を定義します。 サービスプロキシでは、さまざまな LINQ 式を使用してこれらのオプションを適用できます。

このセクションでは、簡単な例を紹介します。 詳細については、MSDN の「 [LINQ に関する考慮事項」 (WCF Data Services)](https://msdn.microsoft.com/library/ee622463.aspx)を参照してください。

### <a name="filtering-filter"></a>フィルター処理 ($filter)

フィルター処理するには、`where` 句を使用します。 次の例では、製品カテゴリを使用してフィルター処理を行います。

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample7.cs)]

このコードは、次の OData クエリに対応しています。

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample8.cmd)]

プロキシが `where` 句を OData `$filter` 式に変換することに注意してください。

### <a name="sorting-orderby"></a>並べ替え ($orderby)

並べ替えるには、`orderby` 句を使用します。 次の例では、価格を優先順位の高いものから順に並べ替えています。

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample9.cs)]

対応する OData 要求を次に示します。

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample10.cmd)]

### <a name="client-side-paging-skip-and-top"></a>クライアント側のページング ($skip と $top)

大きなエンティティセットの場合、クライアントは結果の数を制限することがあります。 たとえば、クライアントが一度に10個のエントリを表示する場合があります。 これは *、クライアント側のページング*と呼ばれます。 (サーバー側の[ページング](../supporting-odata-query-options.md#server-paging)もあります。この場合、サーバーでは結果の数が制限されます)。クライアント側のページングを実行するには、LINQ の**Skip**メソッドと**Take**メソッドを使用します。 次の例では、最初の40件の結果をスキップし、次の10を取得します。

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample11.cs)]

対応する OData 要求を次に示します。

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample12.cmd)]

### <a name="select-select-and-expand-expand"></a>($Select) を選択し、($expand) を展開します。

関連エンティティを含めるには、`DataServiceQuery<t>.Expand` メソッドを使用します。 たとえば、各 `Product`の `Supplier` を含めるには、次のようにします。

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample13.cs)]

対応する OData 要求を次に示します。

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample14.cmd)]

応答の形状を変更するには、LINQ **select**句を使用します。 次の例では、各製品の名前だけを取得し、その他のプロパティは取得しません。

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample15.cs)]

対応する OData 要求を次に示します。

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample16.cmd)]

Select 句には、関連エンティティを含めることができます。 その場合は、 **Expand**; を呼び出さないでください。この場合、プロキシには自動的に拡張が含まれます。 次の例では、各製品の名前と仕入先を取得します。

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample17.cs)]

対応する OData 要求を次に示します。 **$Expand**オプションが含まれていることに注意してください。

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample18.cmd)]

$Select と $expand の詳細については、「 [WEB API 2 での $select、$expand、および $value の使用](../using-select-expand-and-value.md)」を参照してください。

## <a name="add-a-new-entity"></a>新しいエンティティを追加する

エンティティセットに新しいエンティティを追加するには、`AddToEntitySet`を呼び出します。ここで、 *EntitySet*はエンティティセットの名前です。 たとえば、`AddToProducts` は `Products` エンティティセットに新しい `Product` を追加します。 プロキシを生成すると、WCF Data Services によって、これらの厳密に型指定された**Addto**メソッドが自動的に作成されます。

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample19.cs)]

2つのエンティティ間にリンクを追加するには、 **addlink**メソッドと**setlink**メソッドを使用します。 次のコードでは、新しい業者と新しい製品を追加し、それらの間にリンクを作成します。

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample20.cs)]

ナビゲーションプロパティがコレクションの場合は、 **Addlink**を使用します。 この例では、仕入先の `Products` コレクションに製品を追加します。

ナビゲーションプロパティが単一のエンティティの場合は、 **Setlink**を使用します。 この例では、製品の `Supplier` プロパティを設定しています。

## <a name="update--patch"></a>更新/パッチ

エンティティを更新するには、 **Updateobject**メソッドを呼び出します。

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample21.cs)]

この更新は、 **SaveChanges**を呼び出すと実行されます。 既定では、WCF は HTTP MERGE 要求を送信します。 PATCH **onupdate**オプションは、代わりに HTTP パッチを送信するよう WCF に指示します。

> [!NOTE]
> 修正プログラムとマージの理由 元の HTTP 1.1 仕様 ([Rcf 2616](http://tools.ietf.org/html/rfc2616)) では、"部分的な更新" セマンティクスの http メソッドが定義されていませんでした。 部分更新をサポートするには、OData 仕様で MERGE メソッドが定義されています。 2010では、 [RFC 5789](http://tools.ietf.org/html/rfc5789)は部分更新の PATCH メソッドを定義していました。 この[ブログの投稿](https://blogs.msdn.com/b/astoriateam/archive/2008/05/20/merge-vs-replace-semantics-for-update-operations.aspx)では、WCF Data Services のブログで履歴の一部を読むことができます。 現在、MERGE よりもパッチが推奨されています。 Web API スキャフォールディングによって作成された OData コントローラーは、両方のメソッドをサポートします。

エンティティ全体 (PUT セマンティクス) を置換する場合は、 **Replaceonupdate**オプションを指定します。 これにより、WCF は HTTP PUT 要求を送信します。

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample22.cs)]

## <a name="delete-an-entity"></a>エンティティの削除

エンティティを削除するには、 **DeleteObject**を呼び出します。

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample23.cs)]

## <a name="invoke-an-odata-action"></a>OData アクションの呼び出し

OData では、[アクション](odata-actions.md)は、エンティティに対する CRUD 操作として簡単に定義できないサーバー側の動作を追加するための手段です。

OData メタデータドキュメントではアクションについて説明していますが、プロキシクラスは、厳密に型指定されたメソッドを作成しません。 その場合でも、汎用**Execute**メソッドを使用して OData アクションを呼び出すことができます。 ただし、パラメーターのデータ型と戻り値を把握しておく必要があります。

たとえば、`RateProduct` アクションは、型 `Int32` の "評価" という名前のパラメーターを受け取り、`double`を返します。 次のコードは、このアクションを呼び出す方法を示しています。

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample24.cs)]

詳細については、「[サービス操作とアクションの呼び出し](https://msdn.microsoft.com/library/hh230677.aspx)」を参照してください。

1つの方法として、**コンテナー**クラスを拡張して、アクションを呼び出す厳密に型指定されたメソッドを提供します。

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample25.cs)]
