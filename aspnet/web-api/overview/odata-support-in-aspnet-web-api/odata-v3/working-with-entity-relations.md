---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/working-with-entity-relations
title: Web API 2 を使用した OData v3 でのエンティティリレーションのサポート |Microsoft Docs
author: MikeWasson
description: ほとんどのデータセットは、エンティティ間のリレーションシップを定義します。顧客は注文を持ちます。書籍には作成者がいます。製品には仕入先があります。 クライアントは、OData を使用して移動できます...
ms.author: riande
ms.date: 02/26/2014
ms.assetid: 1e4c2eb4-b6cf-42ff-8a65-4d71ddca0394
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/working-with-entity-relations
msc.type: authoredcontent
ms.openlocfilehash: 726a7d51123805e05f6831ef9cd7eaa84b6c44bd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484504"
---
# <a name="supporting-entity-relations-in-odata-v3-with-web-api-2"></a>OData v3 での Web API 2 を使用したエンティティリレーションのサポート

[Mike Wasson](https://github.com/MikeWasson)

[完成したプロジェクトのダウンロード](https://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> ほとんどのデータセットは、エンティティ間のリレーションシップを定義します。顧客は注文を持ちます。書籍には作成者がいます。製品には仕入先があります。 OData を使用すると、クライアントはエンティティの関係を移動できます。 製品を指定すると、業者を見つけることができます。 リレーションシップを作成または削除することもできます。 たとえば、製品の仕入先を設定できます。
> 
> このチュートリアルでは、ASP.NET Web API でこれらの操作をサポートする方法について説明します。 このチュートリアルは、 [WEB API 2 で OData V3 エンドポイントを作成する](creating-an-odata-endpoint.md)チュートリアルに基づいています。
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>このチュートリアルで使用されているソフトウェアのバージョン
> 
> 
> - Web API 2
> - OData バージョン3
> - Entity Framework 6

## <a name="add-a-supplier-entity"></a>Supplier エンティティを追加する

まず、OData フィードに新しいエンティティ型を追加する必要があります。 `Supplier` クラスを追加します。

[!code-csharp[Main](working-with-entity-relations/samples/sample1.cs)]

このクラスは、エンティティキーに文字列を使用します。 実際には、整数キーを使用するよりも、あまり一般的ではない可能性があります。 ただし、OData が整数以外のキーの種類を処理する方法についても説明します。

次に、`Product` クラスに `Supplier` プロパティを追加して、リレーションシップを作成します。

[!code-csharp[Main](working-with-entity-relations/samples/sample2.cs)]

新しい**Dbset**を `ProductServiceContext` クラスに追加して、Entity Framework に `Supplier` テーブルをデータベースに含めます。

[!code-csharp[Main](working-with-entity-relations/samples/sample3.cs?highlight=9)]

WebApiConfig.cs で、EDM モデルに "仕入先" エンティティを追加します。

[!code-csharp[Main](working-with-entity-relations/samples/sample4.cs?highlight=4)]

## <a name="navigation-properties"></a>ナビゲーション プロパティ

製品の供給業者を取得するために、クライアントは GET 要求を送信します。

[!code-console[Main](working-with-entity-relations/samples/sample5.cmd)]

ここで、"Supplier" は `Product` 型のナビゲーションプロパティです。 この場合、`Supplier` は1つの項目を参照しますが、ナビゲーションプロパティはコレクション (一対多または多対多の関係) を返すこともできます。

この要求をサポートするには、次のメソッドを `ProductsController` クラスに追加します。

[!code-csharp[Main](working-with-entity-relations/samples/sample6.cs)]

*キー*パラメーターは製品のキーです。 このメソッドは、関連エンティティ&#8212;(この場合は `Supplier` インスタンス) を返します。 メソッド名とパラメーター名はどちらも重要です。 一般に、ナビゲーションプロパティの名前が "X" の場合は、"GetX" という名前のメソッドを追加する必要があります。 メソッドは、親のキーのデータ型と一致する "*key*" という名前のパラメーターを受け取る必要があります。

*キー*パラメーターに **[Fromodatauri]** 属性を含めることも重要です。 この属性は、要求 URI からキーを解析するときに、OData 構文規則を使用するように Web API に指示します。

## <a name="creating-and-deleting-links"></a>リンクの作成と削除

OData は、2つのエンティティ間のリレーションシップの作成または削除をサポートしています。 OData 用語では、リレーションシップは "リンク" です。 各リンクには、*エンティティ*/$links/*エンティティ*という形式の URI があります。 たとえば、product から supplier へのリンクは次のようになります。

[!code-console[Main](working-with-entity-relations/samples/sample7.cmd)]

新しいリンクを作成するために、クライアントは、リンク URI に POST 要求を送信します。 要求の本文は、ターゲットエンティティの URI です。 たとえば、"CTSO" というキーを持つ業者があるとします。 "Product (1)" から "Supplier (' CTSO ')" へのリンクを作成するために、クライアントは次のような要求を送信します。

[!code-console[Main](working-with-entity-relations/samples/sample8.cmd)]

リンクを削除するには、クライアントがリンク URI に DELETE 要求を送信します。

**リンクの作成**

クライアントが製品供給業者のリンクを作成できるようにするには、次のコードを `ProductsController` クラスに追加します。

[!code-csharp[Main](working-with-entity-relations/samples/sample9.cs)]

このメソッドには、次の 3 つのパラメーターがあります。

- *キー*: 親エンティティ (製品) へのキー
- *navigationProperty*: ナビゲーションプロパティの名前。 この例では、有効なナビゲーションプロパティは "Supplier" だけです。
- *リンク*: 関連エンティティの OData URI。 この値は、要求本文から取得されます。 たとえば、リンク URI は "`http://localhost/odata/Suppliers('CTSO')`、つまり、ID が ' CTSO ' の業者を意味します。

このメソッドは、リンクを使用して業者を検索します。 一致する業者が見つかった場合、メソッドは `Product.Supplier` プロパティを設定し、結果をデータベースに保存します。

最も難しい部分は、リンク URI の解析です。 基本的には、その URI に GET 要求を送信した結果をシミュレートする必要があります。 次のヘルパーメソッドは、この方法を示しています。 メソッドは、Web API ルーティングプロセスを呼び出し、解析された OData パスを表す**ODataPath**インスタンスを取得します。 リンク URI の場合、セグメントの1つをエンティティキーにする必要があります。 (存在しない場合、クライアントは無効な URI を送信しました)。

[!code-csharp[Main](working-with-entity-relations/samples/sample10.cs)]

**リンクの削除**

リンクを削除するには、`ProductsController` クラスに次のコードを追加します。

[!code-csharp[Main](working-with-entity-relations/samples/sample11.cs)]

この例では、ナビゲーションプロパティは単一の `Supplier` エンティティです。 ナビゲーションプロパティがコレクションの場合、リンクを削除するための URI には、関連エンティティのキーが含まれている必要があります。 次に例を示します。

[!code-console[Main](working-with-entity-relations/samples/sample12.cmd)]

この要求により、顧客1の注文1が削除されます。 この場合、DeleteLink メソッドのシグネチャは次のようになります。

[!code-csharp[Main](working-with-entity-relations/samples/sample13.cs)]

関連付けられた*キー*パラメーターは、関連エンティティのキーを指定します。 したがって、`DeleteLink` メソッドでは、 *key*パラメーターでプライマリエンティティを検索し、関連するエンティティを関連する*キー*パラメーターで検索してから、関連付けを削除します。 データモデルによっては、`DeleteLink`の両方のバージョンを実装することが必要になる場合があります。 Web API は、要求 URI に基づいて正しいバージョンを呼び出します。
