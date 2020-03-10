---
uid: web-api/overview/error-handling/exception-handling
title: ASP.NET Web API での例外処理-ASP.NET 4.x
author: MikeWasson
description: ''
ms.author: riande
ms.date: 03/12/2012
ms.custom: seoapril2019
ms.assetid: cbebeb37-2594-41f2-b71a-f4f26520d512
msc.legacyurl: /web-api/overview/error-handling/exception-handling
msc.type: authoredcontent
ms.openlocfilehash: dbdbab6aefec840e2fec9e9cd33f3d124093750e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78504700"
---
# <a name="exception-handling-in-aspnet-web-api"></a>ASP.NET Web API での例外処理

[Mike Wasson](https://github.com/MikeWasson)

この記事では、ASP.NET Web API でのエラーと例外の処理について説明します。

- [HttpResponseException](#httpresponserexception)
- [例外フィルター](#exception_filters)
- [登録 (例外フィルターを)](#registering_exception_filters)
- [Http エラー](#httperror)

<a id="httpresponserexception"></a>
## <a name="httpresponseexception"></a>HttpResponseException

Web API コントローラーでキャッチされない例外がスローされるとどうなりますか。 既定では、ほとんどの例外は、状態コード500、内部サーバーエラーを含む HTTP 応答に変換されます。

**HttpResponseException**型は特殊なケースです。 この例外は、例外コンストラクターで指定した HTTP 状態コードを返します。 たとえば、次のメソッドは、 *id*パラメーターが有効でない場合に、404 (見つからない) を返します。

[!code-csharp[Main](exception-handling/samples/sample1.cs)]

応答をより詳細に制御するには、応答メッセージ全体を作成し、HttpResponseException に含めることもでき**ます。** 

[!code-csharp[Main](exception-handling/samples/sample2.cs)]

<a id="exception_filters"></a>
## <a name="exception-filters"></a>例外フィルター

*例外フィルター*を記述することで、Web API が例外を処理する方法をカスタマイズできます。 例外フィルターは、コントローラーメソッドが、 **HttpResponseException**例外ではないハンドルされ*ない*例外をスローしたときに実行されます。 **HttpResponseException**型は特殊なケースです。これは、HTTP 応答を返す専用に設計されているためです。

例外フィルターは、 **System.web Exceptionfilter**インターフェイスを実装します。 例外フィルターを記述する最も簡単な方法**は、system.exception クラスから**派生させ、 **onexception**メソッドをオーバーライドすることです。

> [!NOTE]
> ASP.NET Web API での例外フィルターは、ASP.NET MVC と似ています。 ただし、これらは個別の名前空間と関数で宣言されています。 特に、MVC で使用される**Handleerrorattribute**クラスは、Web API コントローラーによってスローされる例外を処理しません。

**NotImplementedException**例外を HTTP 状態コード501に変換するフィルターを次に示します (実装されていません)。

[!code-csharp[Main](exception-handling/samples/sample3.cs)]

**Httpactionexecutedcontext**オブジェクトの**response**プロパティには、クライアントに送信される HTTP 応答メッセージが含まれています。

<a id="registering_exception_filters"></a>
## <a name="registering-exception-filters"></a>登録 (例外フィルターを)

Web API 例外フィルターを登録する方法はいくつかあります。

- アクションごと
- コントローラーごと
- グローバル

特定のアクションにフィルターを適用するには、フィルターをアクションに属性として追加します。

[!code-csharp[Main](exception-handling/samples/sample4.cs)]

コントローラー上のすべてのアクションにフィルターを適用するには、フィルターを属性としてコントローラークラスに追加します。

[!code-csharp[Main](exception-handling/samples/sample5.cs)]

すべての Web API コントローラーに対してフィルターをグローバルに適用するには、フィルターのインスタンスを**Globalconfiguration. Configuration. Filters**コレクションに追加します。 このコレクション内の例外フィルターは、任意の Web API コントローラー アクションに適用されます。

[!code-csharp[Main](exception-handling/samples/sample6.cs)]

"ASP.NET MVC 4 Web アプリケーション" プロジェクトテンプレートを使用してプロジェクトを作成する場合は、Web API 構成コードを `WebApiConfig` クラス内に配置します。このクラスは、アプリ\_の [開始] フォルダーにあります。

[!code-csharp[Main](exception-handling/samples/sample7.cs?highlight=5)]

<a id="httperror"></a>
## <a name="httperror"></a>Http エラー

**Httperror**オブジェクトは、応答本文にエラー情報を返す一貫した方法を提供します。 次の例では、HTTP 状態コード 404 (見つからない) を応答本文で**httperror**状態で返す方法を示します。

[!code-csharp[Main](exception-handling/samples/sample8.cs)]

**Createerrorresponse**は、 **HttpRequestMessageExtensions**クラスで定義されている拡張メソッドです。 内部的には、 **Createerrorresponse**は**httperror**インスタンスを作成し、 **httperror**を含むを作成します。

この例では、メソッドが成功した場合、HTTP 応答で製品が返されます。 ただし、要求された製品が見つからない場合、HTTP 応答には要求本文に**httperror**含まれています。 応答は次のようになります。

[!code-console[Main](exception-handling/samples/sample9.cmd)]

この例では、 **HTTPERROR** JSON にシリアル化されていることに注意してください。 **Httperror**使用する利点の1つは、その他の厳密に型指定されたモデルと同じ[コンテンツネゴシエーション](../formats-and-model-binding/content-negotiation.md)およびシリアル化プロセスを通過することです。

### <a name="httperror-and-model-validation"></a>HttpError エラーとモデルの検証

モデルの検証では、モデルの状態を**Createerrorresponse**に渡して、検証エラーを応答に含めることができます。

[!code-csharp[Main](exception-handling/samples/sample10.cs)]

この例では、次の応答が返される場合があります。

[!code-console[Main](exception-handling/samples/sample11.cmd)]

モデルの検証の詳細については、「 [ASP.NET Web API でのモデルの検証](../formats-and-model-binding/model-validation-in-aspnet-web-api.md)」を参照してください。

### <a name="using-httperror-with-httpresponseexception"></a>HttpResponseException での HttpError 使用

前の例では、コントローラーアクションから**HttpResponseMessage**メッセージが返されますが、 **HttpResponseException**を使用して**httperror**返すこともできます。 これにより、通常の成功事例では厳密に型指定されたモデルを返すことができますが、エラーが発生しても**httperror**返されます。

[!code-csharp[Main](exception-handling/samples/sample12.cs)]
