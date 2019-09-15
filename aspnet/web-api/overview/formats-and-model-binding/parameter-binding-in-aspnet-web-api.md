---
uid: web-api/overview/formats-and-model-binding/parameter-binding-in-aspnet-web-api
title: ASP.NET Web API-ASP.NET 4.x のパラメーターバインド
author: MikeWasson
description: Web API がパラメーターをバインドする方法と、ASP.NET 4.x でバインドプロセスをカスタマイズする方法について説明します。
ms.author: riande
ms.date: 07/11/2013
ms.custom: seoapril2019
ms.assetid: e42c8388-04ed-4341-9fdb-41b1b4c06320
msc.legacyurl: /web-api/overview/formats-and-model-binding/parameter-binding-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 5386532ab581e023d93d16a5d4107e07f40b986f
ms.sourcegitcommit: 4b324a11131e38f920126066b94ff478aa9927f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/13/2019
ms.locfileid: "70985816"
---
# <a name="parameter-binding-in-aspnet-web-api"></a>ASP.NET Web API でのパラメーターバインド

作成者[Mike Wasson](https://github.com/MikeWasson)

[!INCLUDE[](~/includes/coreWebAPI.md)]

この記事では、Web API によるパラメーターのバインド方法と、バインドプロセスをカスタマイズする方法について説明します。 Web API がコントローラー上でメソッドを呼び出す場合は、*バインド*と呼ばれるプロセスであるパラメーターの値を設定する必要があります。

既定では、Web API は次の規則を使用してパラメーターをバインドします。

- パラメーターが "simple" 型の場合、Web API は URI から値の取得を試みます。 単純型には、.NET[プリミティブ型](https://msdn.microsoft.com/library/system.type.isprimitive.aspx)(**int**、 **bool**、 **double**など) と、 **TimeSpan**、 **DateTime**、 **Guid**、 **decimal**、および**string**、および型を*持つ任意の*型が含まれます。文字列から変換できるコンバーター。 (後で型コンバーターについて詳しく説明します)。
- 複合型の場合、Web API は、[メディアの種類のフォーマッタ](media-formatters.md)を使用して、メッセージ本文から値の読み取りを試みます。

たとえば、一般的な Web API コントローラーメソッドを次に示します。

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample1.cs)]

*Id*パラメーターは&quot;単純&quot;型であるため、Web API は要求 URI から値を取得しようとします。 *Item*パラメーターは複合型であるため、Web API はメディア型フォーマッタを使用して、要求本文から値を読み取ります。

URI から値を取得するために、Web API はルートデータと URI クエリ文字列を検索します。 ルートデータは、ルーティングシステムが URI を解析し、それをルートと照合するときに設定されます。 詳細については、「[ルーティングとアクションの選択](../web-api-routing-and-actions/routing-and-action-selection.md)」を参照してください。

この記事の残りの部分では、モデルバインドプロセスをカスタマイズする方法について説明します。 ただし、複合型の場合は、可能な限りメディアの種類のフォーマッタを使用することを検討してください。 HTTP の重要な原則は、リソースがメッセージ本文で送信されることです。コンテンツネゴシエーションを使用してリソースの表現を指定します。 メディアタイプのフォーマッタは、まさにこの目的のために設計されています。

## <a name="using-fromuri"></a>[FromUri] を使用する

Web API で URI から複合型を強制的に読み取るには、 **[Fromuri]** 属性をパラメーターに追加します。 次の例では`GeoPoint` 、URI `GeoPoint`からを取得するコントローラーメソッドと共に、型を定義しています。

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample2.cs)]

クライアントは、緯度と経度の値をクエリ文字列に含めることができ、Web API はそれらを`GeoPoint`使用してを構築します。 例えば:

`http://localhost/api/values/?Latitude=47.678558&Longitude=-122.130989`

## <a name="using-frombody"></a>[FromBody] を使用する

Web API で要求本文から単純型を強制的に読み取るには、 **[Frombody]** 属性をパラメーターに追加します。

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample3.cs)]

この例では、Web API はメディアタイプフォーマッタを使用して、要求本文から*名前*の値を読み取ります。 クライアント要求の例を次に示します。

[!code-console[Main](parameter-binding-in-aspnet-web-api/samples/sample4.cmd)]

パラメーターに [FromBody] がある場合、Web API は Content-type ヘッダーを使用してフォーマッタを選択します。 この例では、コンテンツの種類&quot;は application/&quot; json で、要求本文は json オブジェクトではなく生の json 文字列です。

メッセージ本文からの読み取りは、最大で1つのパラメーターで許可されます。 これは機能しません。

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample5.cs)]

このルールの理由は、要求本文は、一度しか読み取ることができないバッファーストリームに格納されている可能性があるためです。

## <a name="type-converters"></a>型コンバーター

Web API によって、クラスを単純型として扱うことができます (これにより、Web API は、 **TypeConverter**を作成し、文字列変換を提供することで、URI からのバインドを試行します)。

次のコードは、 `GeoPoint`地理的ポイントを表すクラスと、文字列からインスタンスに`GeoPoint`変換する**TypeConverter**を示しています。 クラスは、型コンバーターを指定するために、 **[TypeConverter]** 属性で修飾されています。 `GeoPoint` (この例は、Mike ストールのブログ投稿で、 [MVC/WebAPI のアクションシグネチャのカスタムオブジェクトにバインドする方法](https://blogs.msdn.com/b/jmstall/archive/2012/04/20/how-to-bind-to-custom-objects-in-action-signatures-in-mvc-webapi.aspx)を示していました)。

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample6.cs)]

これで、Web API `GeoPoint`は単純型として処理します。つまり`GeoPoint` 、URI からパラメーターをバインドしようとします。 パラメーターに **[Fromuri]** を含める必要はありません。

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample7.cs)]

クライアントは、次のような URI を使用してメソッドを呼び出すことができます。

`http://localhost/api/values/?location=47.678558,-122.130989`

## <a name="model-binders"></a>モデル バインダー

型コンバーターよりも柔軟なオプションは、カスタムモデルバインダーを作成することです。 モデルバインダーを使用すると、HTTP 要求、アクションの説明、ルートデータからの生の値などにアクセスできます。

モデルバインダーを作成するには、 **Imodelbinder**インターフェイスを実装します。 このインターフェイスは、 **Bindmodel**という1つのメソッドを定義します。

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample8.cs)]

ここでは、オブジェクトの`GeoPoint`モデルバインダーを示します。

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample9.cs)]

モデルバインダーは、*値プロバイダー*から生の入力値を取得します。 この設計では、次の2つの異なる関数を分離します。

- 値プロバイダーは、HTTP 要求を受け取り、キーと値のペアのディクショナリを設定します。
- モデルバインダーは、このディクショナリを使用してモデルにデータを読み込みます。

Web API の既定値プロバイダーは、ルートデータとクエリ文字列から値を取得します。 たとえば、URI が`http://localhost/api/values/1?location=48,-122`の場合、値プロバイダーは次のキーと値のペアを作成します。

- id = &quot;1&quot;
- 場所 = &quot;48122&quot;

(既定のルートテンプレート&quot;は api/{controller}/{id}&quot;であると仮定しています)。

バインドするパラメーターの名前は、 **ModelName**プロパティに格納されます。 モデルバインダーは、ディクショナリ内のこの値を持つキーを検索します。 値が存在し、に`GeoPoint`変換できる場合、モデルバインダーは、バインドされた値を**ModelBindingContext**プロパティに割り当てます。

モデルバインダーは単純型変換に限定されないことに注意してください。 この例では、モデルバインダーは、まず既知の場所のテーブルを検索し、失敗した場合は型変換を使用します。

**モデルバインダーの設定**

モデルバインダーを設定するには、いくつかの方法があります。 最初に、パラメーターに **[Modelbinder]** 属性を追加できます。

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample10.cs)]

また、 **[Modelbinder]** 属性を型に追加することもできます。 Web API は、指定されたモデルバインダーをその型のすべてのパラメーターに使用します。

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample11.cs)]

最後に、 **Httpconfiguration**にモデルバインダープロバイダーを追加できます。 モデルバインダープロバイダーは、単にモデルバインダーを作成するファクトリクラスです。 プロバイダーを作成するには、 [ModelBinderProvider](https://msdn.microsoft.com/library/system.web.http.modelbinding.modelbinderprovider.aspx)クラスから派生させます。 ただし、モデルバインダーが1つの型を処理する場合は、この目的のために設計された組み込みの**SimpleModelBinderProvider**を使用する方が簡単です。 この方法を次のコードに示します。

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample12.cs)]

モデルバインディングプロバイダーを使用する場合は、 **[modelbinder]** 属性をパラメーターに追加して、メディアタイプのフォーマッタではなくモデルバインダーを使用する必要があることを Web API に通知する必要があります。 ただし、ここでは、属性でモデルバインダーの種類を指定する必要はありません。

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample13.cs)]

## <a name="value-providers"></a>値プロバイダー

ここでは、モデルバインダーが値プロバイダーから値を取得することを説明しました。 カスタム値プロバイダーを作成するには、 **Ivalueprovider**インターフェイスを実装します。 要求の cookie から値をプルする例を次に示します。

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample14.cs)]

また、 **Valueproviderfactory**クラスから派生することによって、値プロバイダーファクトリを作成する必要があります。

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample15.cs)]

次のように、 **Httpconfiguration**に値プロバイダーファクトリを追加します。

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample16.cs)]

Web API はすべての値プロバイダーを結合するため、モデルバインダーが**valueprovider. GetValue**を呼び出すと、モデルバインダーは、その値を生成できる最初の値プロバイダーから値を受け取ります。

または、次のように、 **valueprovider**属性を使用して、値プロバイダーファクトリをパラメーターレベルで設定することもできます。

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample17.cs)]

これは、指定された値プロバイダーファクトリでモデルバインディングを使用するように Web API に指示します。他の登録済みの値プロバイダーは使用しません。

## <a name="httpparameterbinding"></a>HttpParameterBinding

モデルバインダーは、より一般的なメカニズムの特定のインスタンスです。 **[Modelbinder]** 属性を確認すると、抽象**parameterbindingattribute**クラスから派生したことがわかります。 このクラスは、 **Httpparameterbinding**オブジェクトを返す、 **getbinding**という1つのメソッドを定義します。

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample18.cs)]

**Httpparameterbinding**は、パラメーターを値にバインドする役割を担います。 **[Modelbinder]** の場合、属性は、 **imodelbinder**を使用して実際のバインドを実行する**httpparameterbinding**実装を返します。 独自の**Httpparameterbinding**を実装することもできます。

たとえば、要求内のヘッダーと`if-match` `if-none-match`ヘッダーから etag を取得するとします。 まず、Etag を表すクラスを定義します。

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample19.cs)]

また、 `if-match`ヘッダー `if-none-match`またはヘッダーから ETag を取得するかどうかを示す列挙も定義します。

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample20.cs)]

次に示すのは、目的のヘッダーから ETag を取得し、それを ETag 型のパラメーターにバインドする**Httpparameterbinding**です。

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample21.cs)]

**Executebindingasync**メソッドは、バインディングを行います。 このメソッド内で、 **Httpactioncontext**の**actionargument**ディクショナリにバインドされたパラメーター値を追加します。

> [!NOTE]
> **Executebindingasync**メソッドが要求メッセージの本文を読み取る場合は、によって**true が返されるよう**にします。 要求本文は、1回だけ読み取ることができるバッファーなしのストリームである可能性があるため、Web API は、最大1つのバインディングでメッセージ本文を読み取ることができる規則を適用します。

カスタム**Httpparameterbinding**を適用するには、 **parameterbindingattribute**から派生した属性を定義します。 では、ヘッダー用`if-match`と`if-none-match`ヘッダー用の2つの属性を定義します。 `ETagParameterBinding` どちらも抽象基本クラスから派生します。

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample22.cs)]

`[IfNoneMatch]`属性を使用するコントローラーメソッドを次に示します。

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample23.cs)]

**Parameterbindingattribute**に加えて、カスタム**httpparameterbinding**を追加するための別のフックもあります。 **Httpconfiguration**オブジェクトでは、 **parameterbindingrules**型の匿名関数のコレクションになります (**httpparameterdescriptor**  - &gt; **httpparameterbinding**)。 たとえば、GET メソッドの ETag パラメーターでで`ETagParameterBinding` `if-none-match`使用する規則を追加できます。

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample24.cs)]

関数は、バインド`null`が適用されないパラメーターに対してを返す必要があります。

## <a name="iactionvaluebinder"></a>IActionValueBinder

パラメーターバインドプロセス全体は、プラグ可能なサービスである**Iactionvaluebinder**によって制御されます。 **Iactionvaluebinder**の既定の実装では、次のことが実行されます。

1. パラメーターで**Parameterbindingattribute**を探します。 これには、 **[Frombody]** 、 **[frombody]** 、 **[modelbinder]** 、またはカスタム属性が含まれます。
2. それ以外の場合は、 **Httpconfiguration. ParameterBindingRules** 、null 以外の**httpparameterbinding**を返す関数を探します。
3. それ以外の場合は、前に説明した既定の規則を使用します。 

    - パラメーターの型が "simple" であるか、型コンバーターを持っている場合は、URI からバインドします。 これは、パラメーターに **[Fromuri]** 属性を配置することと同じです。
    - それ以外の場合は、メッセージ本文からパラメーターを読み取ります。 これは、パラメーターに **[Frombody]** を配置することと同じです。

必要に応じて、 **Iactionvaluebinder**サービス全体をカスタム実装に置き換えることができます。

## <a name="additional-resources"></a>その他のリソース

[カスタムパラメーターバインディングのサンプル](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/CustomParameterBinding/ReadMe.txt)

Mike ストールは、Web API パラメーターのバインドに関する一連のブログ投稿を作成しました。

- [Web API がパラメーターのバインドを行う方法](https://blogs.msdn.com/b/jmstall/archive/2012/04/16/how-webapi-does-parameter-binding.aspx)
- [Web API の MVC スタイルパラメーターのバインド](https://blogs.msdn.com/b/jmstall/archive/2012/04/18/mvc-style-parameter-binding-for-webapi.aspx)
- [MVC/Web API でアクションシグネチャのカスタムオブジェクトにバインドする方法](https://blogs.msdn.com/b/jmstall/archive/2012/04/20/how-to-bind-to-custom-objects-in-action-signatures-in-mvc-webapi.aspx)
- [Web API でカスタム値プロバイダーを作成する方法](https://blogs.msdn.com/b/jmstall/archive/2012/04/23/how-to-create-a-custom-value-provider-in-webapi.aspx)
- [内部の Web API パラメーターのバインド](https://blogs.msdn.com/b/jmstall/archive/2012/05/11/webapi-parameter-binding-under-the-hood.aspx)
