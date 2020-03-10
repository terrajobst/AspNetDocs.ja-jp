---
uid: web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2
title: ASP.NET Web API 2 | の属性ルーティングMicrosoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 01/20/2014
ms.assetid: 979d6c9f-0129-4e5b-ae56-4507b281b86d
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2
msc.type: authoredcontent
ms.openlocfilehash: 7da1805d8a7066e82743dc9bd7e024cc9813ee89
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78446998"
---
# <a name="attribute-routing-in-aspnet-web-api-2"></a>ASP.NET Web API 2 での属性ルーティング

[Mike Wasson](https://github.com/MikeWasson)

*ルーティング*とは、Web API が URI とアクションを照合する方法を示します。 Web API 2 では、*属性ルーティング*と呼ばれる新しい種類のルーティングがサポートされています。 名前が示すように、属性ルーティングでは、属性を使用してルートを定義します。 属性ルーティングを使用すると、web API の Uri をより詳細に制御できます。 たとえば、リソースの階層を記述する Uri を簡単に作成できます。

規則ベースのルーティングと呼ばれる以前のスタイルのルーティングは、まだ完全にサポートされています。 実際には、両方の手法を同じプロジェクトで組み合わせることができます。

このトピックでは、属性ルーティングを有効にする方法と、属性ルーティングのさまざまなオプションについて説明します。 属性ルーティングを使用するエンドツーエンドのチュートリアルについては、「 [WEB API 2 で属性ルーティングを使用して REST API を作成](create-a-rest-api-with-attribute-routing.md)する」を参照してください。

## <a name="prerequisites"></a>前提条件

[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)Community、Professional、または Enterprise edition

または、NuGet パッケージマネージャーを使用して、必要なパッケージをインストールします。 Visual Studio の **[ツール]** メニューで、 **[NuGet パッケージマネージャー]** 、 **[パッケージマネージャーコンソール]** の順に選択します。 パッケージマネージャーコンソールウィンドウで、次のコマンドを入力します。

`Install-Package Microsoft.AspNet.WebApi.WebHost`

<a id="why"></a>
## <a name="why-attribute-routing"></a>属性ルーティングの理由

Web API の最初のリリースでは、*規約ベース*のルーティングが使用されていました。 この種類のルーティングでは、基本的にパラメーター化された文字列である1つ以上のルートテンプレートを定義します。 フレームワークは、要求を受信すると、ルートテンプレートに対して URI と一致します。 (規則ベースのルーティングの詳細については、「 [ASP.NET Web API でのルーティング](routing-in-aspnet-web-api.md)」を参照してください。

規則ベースのルーティングの利点の1つは、テンプレートが1つの場所で定義され、ルーティング規則がすべてのコントローラーで一貫して適用されることです。 残念ながら、規約ベースのルーティングでは、RESTful Api に共通する特定の URI パターンをサポートすることが難しくなります。 たとえば、多くの場合、リソースには子リソースが含まれています。顧客の注文、映画、出演者などがあります。 これらの関係を反映する Uri を作成するのは自然なことです。

`/customers/1/orders`

この種類の URI は、規約ベースのルーティングを使用して作成することは困難です。 これを行うことはできますが、多くのコントローラーまたはリソースの種類がある場合は、結果が適切にスケールされません。

属性ルーティングでは、この URI のルートを定義するのは簡単ではありません。 コントローラーアクションに属性を追加するだけです。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample1.cs)]

ここでは、属性ルーティングが簡単になる他のパターンをいくつか示します。

**API のバージョン管理**

この例では、"/api/v1/products" は "/api/v2/products" とは別のコントローラーにルーティングされます。

`/api/v1/products`
`/api/v2/products`

**オーバーロードされた URI セグメント**

この例では、"1" は注文番号ですが、"pending" はコレクションにマップされます。

`/orders/1`
`/orders/pending`

**複数のパラメーターの型**

この例では、"1" は注文番号ですが、"2013/06/16" は日付を指定します。

`/orders/1`
`/orders/2013/06/16`

<a id="enable"></a>
## <a name="enabling-attribute-routing"></a>属性ルーティングの有効化

属性ルーティングを有効にするには、構成中に**MapHttpAttributeRoutes**を呼び出します。 この拡張メソッドは、System.web. **Http. HttpConfigurationExtensions**クラスで定義されています。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample2.cs)]

属性ルーティングは[、規則ベース](routing-in-aspnet-web-api.md)のルーティングと組み合わせることができます。 規則ベースのルートを定義するには、 **MapHttpRoute**メソッドを呼び出します。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample3.cs)]

Web API の構成の詳細については、「 [ASP.NET Web API 2 の構成](../advanced/configuring-aspnet-web-api.md)」を参照してください。

<a id="config"></a>
### <a name="note-migrating-from-web-api-1"></a>注: Web API からの移行1

Web API 2 より前の Web API プロジェクトでは、次のようなコードが生成されました。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample4.cs)]

属性ルーティングが有効になっている場合、このコードは例外をスローします。 属性ルーティングを使用するように既存の Web API プロジェクトをアップグレードする場合は、この構成コードを次のように更新してください。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample5.cs?highlight=4)]

> [!NOTE]
> 詳細については、「 [ASP.NET ホスティングを使用した WEB API の構成](../advanced/configuring-aspnet-web-api.md#webhost)」を参照してください。

<a id="add-routes"></a>
## <a name="adding-route-attributes"></a>ルート属性の追加

属性を使用して定義されたルートの例を次に示します。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample6.cs)]

文字列 &quot;customers/{customerId}/orders&quot; は、ルートの URI テンプレートです。 Web API は、要求 URI とテンプレートを一致させようとします。 この例では、"customers" と "orders" はリテラルセグメントで、"{customerId}" は変数パラメーターです。 次の Uri は、このテンプレートに一致します。

- `http://localhost/customers/1/orders`
- `http://localhost/customers/bob/orders`
- `http://localhost/customers/1234-5678/orders`

このトピックの後半で説明する[制約](#constraints)を使用して、照合を制限できます。

ルートテンプレートの &quot;{customerId}&quot; パラメーターが、メソッドの*customerId*パラメーターの名前と一致することに注意してください。 Web API がコントローラーアクションを呼び出すと、ルートパラメーターのバインドが試行されます。 たとえば、URI が `http://example.com/customers/1/orders`場合、Web API は、アクションの*customerId*パラメーターに値 "1" をバインドしようとします。

URI テンプレートには、いくつかのパラメーターを含めることができます。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample7.cs)]

ルート属性を持たないコントローラーメソッドでは、規約ベースのルーティングが使用されます。 これにより、両方の種類のルーティングを同じプロジェクトで組み合わせることができます。

## <a name="http-methods"></a>HTTP メソッド

また、Web API は、要求の HTTP メソッド (GET、POST など) に基づいてアクションを選択します。 既定では、Web API は、コントローラーメソッド名の先頭と大文字と小文字を区別しない一致を検索します。 たとえば、`PutCustomers` という名前のコントローラーメソッドは、HTTP PUT 要求と一致します。

次の属性を使用してメソッドを修飾することで、この規則をオーバーライドできます。

- **HttpDelete**
- **[HttpGet]**
- **[HttpHead]**
- **[HttpOptions]**
- **[HttpPatch]**
- **HttpPost**
- **HttpPut**

次の例では、CreateBook メソッドを HTTP POST 要求にマップします。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample8.cs)]

標準以外のメソッドを含め、他のすべての HTTP メソッドについては、 **Acceptverbs**属性を使用します。この属性は、http メソッドの一覧を受け取ります。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample9.cs)]

<a id="prefixes"></a>
## <a name="route-prefixes"></a>ルートプレフィックス

多くの場合、コントローラー内のルートはすべて同じプレフィックスで開始されます。 次に例を示します。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample10.cs)]

**[Routeprefix]** 属性を使用して、コントローラー全体に共通のプレフィックスを設定できます。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample11.cs)]

Route プレフィックスをオーバーライドするには、メソッド属性にティルダ (~) を使用します。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample12.cs)]

ルートプレフィックスには、次のパラメーターを含めることができます。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample13.cs)]

<a id="constraints"></a>
## <a name="route-constraints"></a>ルート制約

ルート制約を使用すると、ルートテンプレートのパラメーターの照合方法を制限できます。 一般的な構文は &quot;{parameter: constraint}&quot;です。 次に例を示します。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample14.cs)]

ここでは、URI の &quot;id&quot; セグメントが整数である場合にのみ、最初のルートが選択されます。 それ以外の場合は、2番目のルートが選択されます。

次の表に、サポートされている制約の一覧を示します。

| 制約 | Description | 例 |
| --- | --- | --- |
| アルファ | 大文字と小文字の英字 (a-z、a-z) を検索します。 | {x:alpha} |
| [bool] | ブール値と一致します。 | {x:bool} |
| DATETIME | **DateTime**値と一致します。 | {x:datetime} |
| decimal | 10進値と一致します。 | {x:decimal} |
| double | 64ビットの浮動小数点値と一致します。 | {x:double} |
| float | 32ビットの浮動小数点値と一致します。 | {x:float} |
| guid | GUID 値と一致します。 | {x:guid} |
| INT | 32ビットの整数値と一致します。 | {x:int} |
| length | 指定された長さの文字列、または指定された長さの範囲内にある文字列と一致します。 | {x:length (6)}{x:length (1, 20)} |
| long | 64ビットの整数値と一致します。 | {x:long} |
| max | 最大値を持つ整数と一致します。 | {x:max(10)} |
| maxlength | 最大長の文字列と一致します。 | {x:maxlength(10)} |
| min | 最小値を持つ整数と一致します。 | {x:min (10)} |
| minlength | 最小長の文字列と一致します。 | {x:minlength (10)} |
| range | 値の範囲内の整数と一致します。 | {x:range(10,50)} |
| regex | 正規表現と一致します。 | {x:regex (^ \d{3}-\d{3}-\d{4}$)} |

&quot;min&quot;などの一部の制約は、かっこで囲まれた引数を受け取ることに注意してください。 パラメーターには、コロンで区切られた複数の制約を適用できます。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample15.cs)]

### <a name="custom-route-constraints"></a>カスタム ルート制約

**IHttpRouteConstraint**インターフェイスを実装することによって、カスタムルート制約を作成できます。 たとえば、次の制約では、パラメーターを0以外の整数値に制限しています。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample16.cs)]

次のコードは、制約を登録する方法を示しています。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample17.cs)]

これで、ルートに制約を適用できるようになりました。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample18.cs)]

また、 **Iinlineconstr/** resolver インターフェイスを実装することによって、 **defaulの**完全な使用方法を置き換えることもできます。 これを行うと、 **Iinlineconstrの**実装で明示的に追加されていない限り、組み込みの制約がすべて置き換えられます。

<a id="optional"></a>
## <a name="optional-uri-parameters-and-default-values"></a>省略可能な URI パラメーターと既定値

ルートパラメーターに疑問符を追加することで、URI パラメーターをオプションにすることができます。 ルートパラメーターが省略可能な場合は、メソッドパラメーターの既定値を定義する必要があります。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample19.cs)]

この例では、`/api/books/locale/1033` と `/api/books/locale` は同じリソースを返します。

または、ルートテンプレート内の既定値を次のように指定することもできます。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample20.cs)]

これは前の例とほぼ同じですが、既定値が適用された場合の動作に若干の違いがあります。

- 最初の例 ("{lcid: int?}") では、既定値の1033がメソッドのパラメーターに直接割り当てられているため、パラメーターにはこの正確な値が含まれます。
- 2番目の例 ("{lcid: int = 1033}") では、既定値の "1033" がモデルバインドプロセスを通過します。 既定のモデルバインダーは、"1033" を数値1033に変換します。 ただし、カスタムモデルバインダーをプラグインすることもできますが、これは別の方法で実行される可能性があります。

(ほとんどの場合、パイプラインにカスタムモデルバインダーがある場合を除き、2つの形式は同じです)。

<a id="route-names"></a>
## <a name="route-names"></a>ルート名

Web API では、すべてのルートに名前が付いています。 ルート名はリンクを生成するのに役立ちます。これにより、HTTP 応答にリンクを含めることができます。

ルート名を指定するには、属性の**name**プロパティを設定します。 次の例は、ルート名を設定する方法と、リンクの生成時にルート名を使用する方法を示しています。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample21.cs)]

<a id="order"></a>
## <a name="route-order"></a>ルートの順序

フレームワークが URI とルートを一致させようとすると、ルートは特定の順序で評価されます。 順序を指定するには、route 属性の**order**プロパティを設定します。 下限値が最初に評価されます。 既定の順序の値は0です。

合計の順序を決定する方法を次に示します。

1. Route 属性の**Order**プロパティを比較します。
2. ルートテンプレート内の各 URI セグメントを確認します。 各セグメントについて、次の順序で並べ替えます。

    1. リテラルセグメント。
    2. 制約付きのパラメーターをルーティングします。
    3. 制約のないルートパラメーター。
    4. 制約のあるワイルドカードパラメーターセグメント。
    5. 制約のないワイルドカードパラメーターセグメント。
3. 同一の場合、ルートは、ルートテンプレートの大文字と小文字を区別しない序数の文字列比較 ([stringcomparison.ordinalignorecase](https://msdn.microsoft.com/library/system.stringcomparer.ordinalignorecase.aspx)) によって並べ替えられます。

次に例を示します。 次のコントローラーを定義するとします。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample22.cs)]

これらのルートは次の順序で並べ替えられます。

1. 注文/詳細
2. 注文/{id}
3. orders/{customerName}
4. orders/{\*date}
5. 注文/保留中

"Details" はリテラルセグメントであり、"{id}" の前に表示されますが、 **Order**プロパティが1であるため、"pending" が最後に表示されることに注意してください。 (この例では、"詳細" または "保留中" という名前の顧客がいないことを前提としています。 一般に、あいまいなルートは避けてください。 この例では、`GetByCustomer` のより優れたルートテンプレートは "customers/{様}" です)
