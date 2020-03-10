---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/odata-actions-and-functions
title: ASP.NET Web API 2.2 | を使用した OData v4 のアクションと関数Microsoft Docs
author: MikeWasson
description: OData では、アクションと関数を利用して、エンティティに対する CRUD 操作として簡単に定義できないサーバー側の動作を追加することができます。 このチュートリアルでは、次の操作方法について説明します。
ms.author: riande
ms.date: 06/27/2014
ms.assetid: 0e6fb03c-b16d-4bb0-ab0b-552bd2b6ece1
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/odata-actions-and-functions
msc.type: authoredcontent
ms.openlocfilehash: f5af94e93e5b7f2351d40febbf1a468d635c9db1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448060"
---
# <a name="actions-and-functions-in-odata-v4-using-aspnet-web-api-22"></a>ASP.NET Web API 2.2 を使用した OData v4 のアクションと関数

[Mike Wasson](https://github.com/MikeWasson)

> OData では、アクションと関数を利用して、エンティティに対する CRUD 操作として簡単に定義できないサーバー側の動作を追加することができます。 このチュートリアルでは、Web API 2.2 を使用して、OData v4 エンドポイントにアクションと関数を追加する方法について説明します。 このチュートリアルでは、チュートリアル[「ASP.NET Web API 2 を使用して OData V4 エンドポイントを作成](create-an-odata-v4-endpoint.md)する」を基にしています。
>
> ## <a name="software-versions-used-in-the-tutorial"></a>このチュートリアルで使用されているソフトウェアのバージョン
>
> - Web API 2.2
> - OData v4
> - Visual Studio 2013 (こちらから Visual Studio 2017 をダウンロードして[ください](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017))
> - .NET 4.5
>
> ## <a name="tutorial-versions"></a>チュートリアルのバージョン
>
> OData バージョン3については、「 [ASP.NET Web API 2 の Odata アクション](../odata-v3/odata-actions.md)」を参照してください。

*アクション*と*関数*の違いは、アクションに副作用が生じる可能性があることと、関数によって処理されないことです。 アクションと関数はどちらもデータを返すことができます。 アクションの用途には、次のようなものがあります。

- 複雑なトランザクション。
- 一度に複数のエンティティを操作します。
- エンティティの特定のプロパティに対してのみ更新を許可します。
- エンティティではないデータを送信しています。

関数は、エンティティまたはコレクションに直接対応していない情報を返す場合に便利です。

アクション (または関数) は、1つのエンティティまたはコレクションを対象にすることができます。 OData 用語では、これは*バインド*です。 また、&quot;バインドされていない&quot; アクション/関数を使用することもできます。これは、サービスで静的操作として呼び出されます。

## <a name="example-adding-an-action"></a>例: アクションの追加

製品を評価するアクションを定義してみましょう。

> [!NOTE]
> このチュートリアルは、チュートリアル[「ASP.NET Web API 2 を使用して OData V4 エンドポイントを作成](create-an-odata-v4-endpoint.md)する」を基にしています。

まず、評価を表す `ProductRating` モデルを追加します。

[!code-csharp[Main](odata-actions-and-functions/samples/sample1.cs)]

また、 **Dbset**を `ProductsContext` クラスに追加して、EF によってデータベースに評価テーブルが作成されるようにします。

[!code-csharp[Main](odata-actions-and-functions/samples/sample2.cs)]

### <a name="add-the-action-to-the-edm"></a>アクションを EDM に追加する

WebApiConfig.cs で、次のコードを追加します。

[!code-csharp[Main](odata-actions-and-functions/samples/sample3.cs)]

**Entitytypeconfiguration action**メソッドは、entity data MODEL (EDM) にアクションを追加します。 **Parameter**メソッドは、アクションに対して型指定されたパラメーターを指定します。

このコードは、EDM の名前空間も設定します。 アクションの URI には完全修飾されたアクション名が含まれているため、名前空間が重要になります。

[!code-console[Main](odata-actions-and-functions/samples/sample4.cmd)]

> [!NOTE]
> 一般的な IIS 構成では、この URL のドットは IIS によってエラー404を返します。 これを解決するには、web.config ファイルに次のセクションを追加します。

[!code-xml[Main](odata-actions-and-functions/samples/sample5.xml)]

### <a name="add-a-controller-method-for-the-action"></a>アクションのコントローラーメソッドを追加します。

&quot;率&quot; アクションを有効にするには、次のメソッドを `ProductsController`に追加します。

[!code-csharp[Main](odata-actions-and-functions/samples/sample6.cs)]

メソッド名がアクション名と一致することに注意してください。 **[Httppost]** 属性では、メソッドが HTTP POST メソッドであることを指定します。

アクションを呼び出すために、クライアントは次のような HTTP POST 要求を送信します。

[!code-console[Main](odata-actions-and-functions/samples/sample7.cmd)]

&quot;率&quot; アクションは製品インスタンスにバインドされているため、アクションの URI は、エンティティ URI に追加された完全修飾アクション名になります。 (EDM 名前空間を &quot;ProductService&quot;に設定しているので、完全修飾されたアクション名は ProductService. レート&quot;に &quot;ます)。

要求の本文には、アクションパラメーターが JSON ペイロードとして含まれています。 Web API は、JSON ペイロードを、パラメーター値のディクショナリである、自動的に、指定さ**れたパラメーターオブジェクトに**変換します。 このディクショナリを使用して、コントローラーメソッドのパラメーターにアクセスします。

クライアントがアクションパラメーターを誤った形式で送信した場合、 **Modelstate. IsValid**の値は false になります。 コントローラーメソッドでこのフラグをチェックし、 **IsValid**が false の場合はエラーを返します。

[!code-csharp[Main](odata-actions-and-functions/samples/sample8.cs)]

## <a name="example-adding-a-function"></a>例: 関数の追加

次に、最も負荷の高い製品を返す OData 関数を追加してみましょう。 前と同様に、最初の手順として、関数を EDM に追加します。 WebApiConfig.cs で、次のコードを追加します。

[!code-csharp[Main](odata-actions-and-functions/samples/sample9.cs)]

この場合、関数は個別の製品インスタンスではなく Products コレクションにバインドされます。 クライアントは GET 要求を送信することによって関数を呼び出します。

[!code-console[Main](odata-actions-and-functions/samples/sample10.cmd)]

この関数のコントローラーメソッドを次に示します。

[!code-csharp[Main](odata-actions-and-functions/samples/sample11.cs)]

メソッド名が関数名と一致することに注意してください。 **[HttpGet]** 属性は、メソッドが HTTP GET メソッドであることを指定します。

HTTP 応答を次に示します。

[!code-console[Main](odata-actions-and-functions/samples/sample12.cmd)]

## <a name="example-adding-an-unbound-function"></a>例: バインド解除関数の追加

前の例は、コレクションにバインドされた関数です。 次の例では、*バインド*されていない関数を作成します。 バインドされていない関数は、サービスに対して静的操作として呼び出されます。 この例の関数は、指定された郵便番号の売上税を返します。

Webapiconfig.cs ファイルで、関数を EDM に追加します。

[!code-csharp[Main](odata-actions-and-functions/samples/sample13.cs)]

エンティティ型またはコレクションではなく、**使用**に対して**関数**を直接呼び出すことに注意してください。 これにより、関数がバインド解除されることがモデルビルダーに伝えられます。

関数を実装するコントローラーメソッドを次に示します。

[!code-csharp[Main](odata-actions-and-functions/samples/sample14.cs)]

このメソッドをどの Web API コントローラーに配置するかは関係ありません。 `ProductsController`に配置することも、別のコントローラーを定義することもできます。 **[ODataRoute]** 属性は、関数の URI テンプレートを定義します。

クライアント要求の例を次に示します。

[!code-console[Main](odata-actions-and-functions/samples/sample15.cmd)]

HTTP 応答:

[!code-console[Main](odata-actions-and-functions/samples/sample16.cmd)]
