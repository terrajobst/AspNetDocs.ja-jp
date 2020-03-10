---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/odata-actions
title: ASP.NET Web API 2 | での OData アクションのサポートMicrosoft Docs
author: MikeWasson
description: OData では、アクションは、エンティティに対する CRUD 操作として簡単に定義できないサーバー側の動作を追加するための手段です。 アクションの用途には、次のようなものがあります。
ms.author: riande
ms.date: 02/25/2014
ms.assetid: 2d7b3aa2-aa47-4e6e-b0ce-3d65a1c6fe02
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/odata-actions
msc.type: authoredcontent
ms.openlocfilehash: ae8b23f0868f992cb2bbbf14ee3f7ac848501515
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448174"
---
# <a name="supporting-odata-actions-in-aspnet-web-api-2"></a>ASP.NET Web API 2 での OData アクションのサポート

[Mike Wasson](https://github.com/MikeWasson)

[完成したプロジェクトのダウンロード](https://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> OData では、*アクション*は、エンティティに対する CRUD 操作として簡単に定義できないサーバー側の動作を追加するための手段です。 アクションの用途には、次のようなものがあります。
> 
> - 複雑なトランザクションの実装。
> - 一度に複数のエンティティを操作します。
> - エンティティの特定のプロパティに対してのみ更新を許可します。
> - エンティティで定義されていないサーバーに情報を送信しています。
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>このチュートリアルで使用されているソフトウェアのバージョン
> 
> 
> - Web API 2
> - OData バージョン3
> - Entity Framework 6

## <a name="example-rating-a-product"></a>例: 製品の評価

この例では、ユーザーが製品を評価し、各製品の平均評価を公開できるようにします。 データベースには、製品にキーを付けた評価の一覧が保存されます。

Entity Framework で評価を表すために使用できるモデルを次に示します。

[!code-csharp[Main](odata-actions/samples/sample1.cs)]

しかし、クライアントが "評価" コレクションに `ProductRating` オブジェクトを投稿することは望ましくありません。 直観的に、評価は Products コレクションに関連付けられており、クライアントは評価値を投稿するだけでよいはずです。

そのため、通常の CRUD 操作を使用する代わりに、クライアントが製品で呼び出すことができるアクションを定義します。 OData 用語では、アクションは製品エンティティに*バインド*されます。

>アクションにはサーバーへの副作用があります。 このため、HTTP POST 要求を使用して呼び出されます。 アクションには、サービスメタデータで記述されているパラメーターと戻り値の型を含めることができます。 クライアントは要求本文にパラメーターを送信し、サーバーは応答本文で戻り値を送信します。 "製品の評価" アクションを呼び出すために、クライアントは次のような URI に投稿を送信します。

[!code-console[Main](odata-actions/samples/sample2.cmd)]

POST 要求のデータは、単純に製品の評価です。

[!code-console[Main](odata-actions/samples/sample3.cmd)]

## <a name="declare-the-action-in-the-entity-data-model"></a>Entity Data Model でアクションを宣言します。

Web API 構成で、アクションを entity data model (EDM) に追加します。

[!code-csharp[Main](odata-actions/samples/sample4.cs)]

このコードでは、Product エンティティに対して実行できるアクションとして "RateProduct" が定義されています。 また、アクションが "評価" という名前の**int**パラメーターを受け取り、 **int**値を返すことも宣言します。

## <a name="add-the-action-to-the-controller"></a>コントローラーにアクションを追加する

"RateProduct" アクションは、製品エンティティにバインドされています。 アクションを実装するには、`RateProduct` という名前のメソッドを Products コントローラーに追加します。

[!code-csharp[Main](odata-actions/samples/sample5.cs)]

メソッド名が EDM のアクションの名前と一致することに注意してください。 メソッドには、次の2つのパラメーターがあります。

- *キー*: 評価する製品のキー。
- *parameters*: アクションパラメーター値のディクショナリ。

既定のルーティング規約を使用している場合、キーパラメーターの名前は "key" にする必要があります。 次に示すように、 **[Fromodatauri]** 属性を含めることも重要です。 この属性は、要求 URI からキーを解析するときに、OData 構文規則を使用するように Web API に指示します。

*パラメーター*ディクショナリを使用して、アクションパラメーターを取得します。

[!code-csharp[Main](odata-actions/samples/sample6.cs)]

クライアントがアクションパラメーターを正しい形式で送信する場合、 **Modelstate. IsValid**の値は true になります。 その場合は、パラメーターの値を取得するために、指定され**たパラメーターを**使用できます。 この例では、`RateProduct` アクションは "評価" という名前の1つのパラメーターを受け取ります。

## <a name="action-metadata"></a>アクションメタデータ

サービスメタデータを表示するには、GET 要求を/odata/$metadata に送信します。 `RateProduct` アクションを宣言するメタデータの部分を次に示します。

[!code-xml[Main](odata-actions/samples/sample7.xml)]

**FunctionImport**要素はアクションを宣言します。 ほとんどのフィールドはわかりやすくなっていますが、2つの注意点があります。

- **Isbindable**可能は、少なくとも一部の時点で、ターゲットエンティティに対してアクションを呼び出すことができることを意味します。
- **Isalways バインド**可能とは、アクションをターゲットエンティティで常に呼び出すことができることを意味します。

違いは、一部のアクションはクライアントで常に使用できるということですが、他のアクションはエンティティの状態によって異なる場合があります。 たとえば、"Purchase" アクションを定義するとします。 購入できるのは在庫内の商品だけです。 項目が在庫切れの場合、クライアントはそのアクションを呼び出すことができません。

EDM を定義すると、**アクション**メソッドによって、常にバインド可能なアクションが作成されます。

[!code-csharp[Main](odata-actions/samples/sample8.cs?highlight=1)]

ここでは、このトピックで後述する、非 always バインド操作 (*一時*アクションとも呼ばれます) について説明します。

## <a name="invoking-the-action"></a>アクションの呼び出し

ここで、クライアントがこのアクションを呼び出す方法を見てみましょう。 たとえば、ID が4の製品に対して2という評価を行うとします。 要求本文の JSON 形式を使用した要求メッセージの例を次に示します。

[!code-console[Main](odata-actions/samples/sample9.cmd)]

応答メッセージは次のとおりです。

[!code-console[Main](odata-actions/samples/sample10.cmd)]

## <a name="binding-an-action-to-an-entity-set"></a>エンティティセットへのアクションのバインド

前の例では、アクションは単一のエンティティにバインドされています。クライアントは1つの製品を評価します。 また、アクションをエンティティのコレクションにバインドすることもできます。 次の変更を行うだけです。

EDM で、アクションをエンティティの**コレクション**プロパティに追加します。

[!code-csharp[Main](odata-actions/samples/sample11.cs?highlight=1)]

コントローラーメソッドで、*キー*パラメーターを省略します。

[!code-csharp[Main](odata-actions/samples/sample12.cs)]

これで、クライアントは Products エンティティセットに対してアクションを呼び出します。

[!code-console[Main](odata-actions/samples/sample13.cmd)]

## <a name="actions-with-collection-parameters"></a>コレクションパラメーターを使用したアクション

アクションは、値のコレクションを受け取るパラメーターを持つことができます。 EDM では、 **collectionparameter&lt;t&gt;** を使用してパラメーターを宣言します。

[!code-csharp[Main](odata-actions/samples/sample14.cs)]

これは、 **int**値のコレクションを受け取る "評価" という名前のパラメーターを宣言します。 コントローラーメソッドでは、現在では、パラメーターの値は、次のようにします。**このオブジェクトは、パラメーター**の値を指定します。値は**ICollection&lt;int&gt;** 値です。

[!code-csharp[Main](odata-actions/samples/sample15.cs)]

## <a name="transient-actions"></a>一時的なアクション

"RateProduct" の例では、ユーザーは常に製品を評価できるため、アクションは常に使用できます。 ただし、一部のアクションはエンティティの状態に依存します。 たとえば、ビデオレンタルサービスでは、"チェックアウト" アクションは常に使用できるとは限りません。 (そのビデオのコピーが利用可能かどうかによって異なります)。この種類のアクションは、*一時的*なアクションと呼ばれます。

サービスメタデータでは、一時的なアクションの値は**常**に false になります。 これは実際には既定値であるため、メタデータは次のようになります。

[!code-xml[Main](odata-actions/samples/sample16.xml)]

これが重要な理由は次のとおりです。アクションが一時的なものである場合、サーバーは、アクションが使用可能であることをクライアントに通知する必要があります。 これを行うには、エンティティ内のアクションへのリンクを含めます。 次に、ムービーエンティティの例を示します。

[!code-console[Main](odata-actions/samples/sample17.cmd)]

"#CheckOut" プロパティには、チェックアウトアクションへのリンクが含まれています。 アクションが使用できない場合、サーバーはリンクを省略します。

EDM で一時的なアクションを宣言するには、次のように、**遷移**メソッドを呼び出します。

[!code-csharp[Main](odata-actions/samples/sample18.cs)]

また、特定のエンティティのアクションリンクを返す関数を指定する必要があります。 この関数は、 **HasActionLink**を呼び出して設定します。 関数をラムダ式として記述できます。

[!code-csharp[Main](odata-actions/samples/sample19.cs)]

アクションが使用可能な場合、ラムダ式はアクションへのリンクを返します。 OData シリアライザーは、エンティティをシリアル化するときにこのリンクを含みます。 アクションが使用できない場合、関数は `null`を返します。

## <a name="additional-resources"></a>その他のリソース

[OData アクションのサンプル](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v3/ODataActionsSample/)
