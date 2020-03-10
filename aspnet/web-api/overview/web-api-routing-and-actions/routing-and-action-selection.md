---
uid: web-api/overview/web-api-routing-and-actions/routing-and-action-selection
title: ASP.NET Web API でのルーティングとアクションの選択 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 12/14/2018
ms.assetid: bcf2d223-cb7f-411e-be05-f43e96a14015
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/routing-and-action-selection
msc.type: authoredcontent
ms.openlocfilehash: 62114e56fb29e80c93b82dcb78ce2bc2a123a83b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78446914"
---
# <a name="routing-and-action-selection-in-aspnet-web-api"></a>ASP.NET Web API でのルーティングとアクションの選択

[Mike Wasson](https://github.com/MikeWasson)

この記事では、ASP.NET Web API して、コントローラー上の特定のアクションに HTTP 要求をルーティングする方法について説明します。

> [!NOTE]
> ルーティングの概要については、「 [ASP.NET Web API でのルーティング](routing-in-aspnet-web-api.md)」を参照してください。

この記事では、ルーティングプロセスの詳細について説明します。 Web API プロジェクトを作成し、一部の要求が意図したとおりにルーティングされないことを確認した場合、この記事は役に立ちます。

ルーティングには、次の3つの主要なフェーズがあります。

1. URI をルートテンプレートと照合します。
2. コントローラーを選択します。
3. アクションを選択します。

プロセスの一部の部分は、独自のカスタム動作に置き換えることができます。 この記事では、既定の動作について説明します。 最後に、動作をカスタマイズできる場所に注意してください。

## <a name="route-templates"></a>ルートテンプレート

ルートテンプレートは、URI パスに似ていますが、プレースホルダー値を含むことができます (中かっこで囲まれています)。

[!code-csharp[Main](routing-and-action-selection/samples/sample1.ps1)]

ルートを作成するときに、一部またはすべてのプレースホルダーに既定値を指定できます。

[!code-csharp[Main](routing-and-action-selection/samples/sample2.cs)]

また、URI セグメントがプレースホルダーと一致する方法を制限する制約を指定することもできます。

[!code-csharp[Main](routing-and-action-selection/samples/sample3.js)]

フレームワークは、URI パスのセグメントとテンプレートを一致させようとします。 テンプレート内のリテラルは正確に一致する必要があります。 制約を指定しない限り、プレースホルダーは任意の値と一致します。 フレームワークは、ホスト名やクエリパラメーターなど、URI のその他の部分と一致しません。 フレームワークは、ルートテーブル内で URI に一致する最初のルートを選択します。

"{Controller}" と "{action}" という2つの特殊なプレースホルダーがあります。

- "{controller}" には、コントローラーの名前を指定します。
- "{action}" は、アクションの名前を指定します。 Web API では、通常、"{action}" を省略しています。

### <a name="defaults"></a>デフォルト

既定値を指定した場合、ルートはそれらのセグメントが欠落している URI と一致します。 次に例を示します。

[!code-csharp[Main](routing-and-action-selection/samples/sample4.cs)]

Uri `http://localhost/api/products/all` と `http://localhost/api/products` は、前のルートと一致します。 後者の URI では、不足している `{category}` セグメントに既定値 `all`が割り当てられます。

### <a name="route-dictionary"></a>ルートディクショナリ

URI に一致するものが見つかった場合は、各プレースホルダーの値を含むディクショナリが作成されます。 キーはプレースホルダー名であり、中かっこは含まれません。 値は、URI パスまたは既定値から取得されます。 ディクショナリは、 **IHttpRouteData**オブジェクトに格納されます。

このルート照合フェーズでは、特別な "{controller}" プレースホルダーと "{action}" プレースホルダーが、他のプレースホルダーと同じように扱われます。 これらは、他の値と共にディクショナリに格納されるだけです。

既定値は、特別な値 Routeparameter を持つことができ**ます。省略可能**。 プレースホルダーにこの値が割り当てられている場合、その値はルートディクショナリに追加されません。 次に例を示します。

[!code-csharp[Main](routing-and-action-selection/samples/sample5.cs)]

URI パス "api/製品" の場合、ルートディクショナリには次のものが含まれます。

- コントローラー: "製品"
- カテゴリ: "all"

ただし、"api/products/toys/123" の場合、ルートディクショナリには次のものが含まれます。

- コントローラー: "製品"
- category: "toys"
- id: "123"

既定値には、ルートテンプレートのどこにも表示されない値を含めることもできます。 ルートがと一致する場合、その値はディクショナリに格納されます。 次に例を示します。

[!code-csharp[Main](routing-and-action-selection/samples/sample6.cs)]

URI パスが "api/root/8" の場合、ディクショナリには次の2つの値が含まれます。

- コントローラー: "customers"
- id: "8"

## <a name="selecting-a-controller"></a>コントローラーの選択

コントローラーの選択は、 **IHttpControllerSelector**メソッドによって処理されます。 このメソッドは、 **HttpRequestMessage**インスタンスを受け取り、 **httpコントローラー記述子**を返します。 既定の実装は、 **DefaultHttpControllerSelector**クラスによって提供されます。 このクラスは、単純なアルゴリズムを使用します。

1. ルートディクショナリでキー "controller" を探します。
2. このキーの値を取得し、"Controller" という文字列を追加して、コントローラーの種類の名前を取得します。
3. この型名の Web API コントローラーを探します。

たとえば、ルートディクショナリにキーと値のペア "controller" = "products" が含まれている場合、コントローラーの種類は "製品コントローラー" です。 一致する型がない場合、または複数の一致がある場合、フレームワークはクライアントにエラーを返します。

手順3では、 **DefaultHttpControllerSelector**は**IHttpControllerTypeResolver**インターフェイスを使用して、Web API コントローラーの種類の一覧を取得します。 **IHttpControllerTypeResolver**の既定の実装は、(a) が**IHttpController**を実装するすべてのパブリッククラスを返します。 (b) は abstract ではなく、(c) は "Controller" で終わる名前を持ちます。

## <a name="action-selection"></a>アクションの選択

コントローラーを選択した後、フレームワークは**Ihttpactionselector. selectaction**メソッドを呼び出してアクションを選択します。 このメソッドは**Httpコントローラーコンテキスト**を取得し、 **Httpactiondescriptor**を返します。

既定の実装は、 **ApiControllerActionSelector**クラスによって提供されます。 アクションを選択するには、次のように表示されます。

- 要求の HTTP メソッド。
- ルートテンプレート内の "{action}" プレースホルダー (存在する場合)。
- コントローラー上のアクションのパラメーター。

選択アルゴリズムを確認する前に、コントローラーアクションに関するいくつかの点を理解する必要があります。

**コントローラーのどのメソッドが "アクション" と見なされますか。** アクションを選択すると、フレームワークはコントローラーのパブリックインスタンスメソッドのみを参照します。 また、 ["特別な名前"](https://msdn.microsoft.com/library/system.reflection.methodbase.isspecialname)メソッド (コンストラクター、イベント、演算子のオーバーロードなど)、および**ApiController**クラスから継承されたメソッドは除外されます。

**HTTP メソッド。** フレームワークは、次のように決定された要求の HTTP メソッドに一致するアクションのみを選択します。

1. HTTP メソッドには、 **Acceptverbs**、 **httpdelete**、 **HttpGet**、 **httpdelete**、 **HttpOptions**、 **httpdelete**、 **httpdelete**、または**httpdelete**の属性を指定できます。
2. それ以外の場合、コントローラーメソッドの名前が "Get"、"Post"、"Put"、"Delete"、"Head"、"Options"、または "Patch" で始まる場合、規則によって、アクションはその HTTP メソッドをサポートします。
3. 上記のいずれも当てはまらない場合、メソッドは POST をサポートします。

**パラメーターのバインド。** パラメーターのバインドとは、Web API がパラメーターの値を作成する方法です。 パラメーターバインドの既定の規則を次に示します。

- 単純型は URI から取得されます。
- 複合型は、要求本文から取得されます。

単純型には、すべての[.NET Framework プリミティブ型](https://msdn.microsoft.com/library/system.type.isprimitive)に加え、 **DateTime**、 **Decimal**、 **Guid**、 **String**、および**TimeSpan**が含まれます。 アクションごとに、最大で1つのパラメーターで要求本文を読み取ることができます。

> [!NOTE]
> 既定のバインディング規則をオーバーライドできます。 詳細[については、「WebAPI Parameter binding」を](https://blogs.msdn.com/b/jmstall/archive/2012/05/11/webapi-parameter-binding-under-the-hood.aspx)参照してください。

この背景を使用すると、アクションの選択アルゴリズムが次のようになります。

1. HTTP 要求メソッドに一致するコントローラー上のすべてのアクションの一覧を作成します。
2. ルートディクショナリに "action" エントリがある場合は、名前がこの値と一致しないアクションを削除します。
3. 次のように、アクションパラメーターを URI と照合します。 

    1. アクションごとに、単純型のパラメーターのリストを取得します。ここで、バインドは URI からパラメーターを取得します。 省略可能なパラメーターを除外します。
    2. この一覧から、ルートディクショナリまたは URI クエリ文字列のいずれかで、各パラメーター名に一致するものを検索します。 一致では大文字と小文字が区別されず、パラメーターの順序に依存しません。
    3. リスト内のすべてのパラメーターが URI で一致するアクションを選択します。
    4. 1つのアクションがこれらの条件を満たしている場合は、最も多くのパラメーターが一致するものを選択します。
4. **[非アクション]** 属性を持つアクションは無視します。

手順 #3 は、おそらく最もわかりにくいものです。 基本的な考え方は、パラメーターが URI、要求本文、またはカスタムバインディングから値を取得できることです。 URI からのパラメーターの場合、URI に実際にそのパラメーターの値が含まれていることを確認する必要があります (ルートディクショナリ経由のパスまたはクエリ文字列内)。

たとえば、次のようなアクションを考えてみます。

[!code-csharp[Main](routing-and-action-selection/samples/sample7.cs)]

*Id*パラメーターは URI にバインドされます。 このため、このアクションは、ルートディクショナリまたはクエリ文字列に "id" の値を含む URI にのみ一致できます。

省略可能なパラメーターは省略可能であるため、例外です。 省略可能なパラメーターの場合、バインドが URI から値を取得できない場合は問題ありません。

複合型は、さまざまな理由で例外となります。 複合型は、カスタムバインドを介して URI にのみバインドできます。 ただし、この場合、パラメーターが特定の URI にバインドされるかどうかを事前に確認することはできません。 これを確認するには、バインディングを呼び出す必要があります。 選択アルゴリズムの目的は、バインドを呼び出す前に、静的な説明からアクションを選択することです。 したがって、複合型は照合アルゴリズムから除外されます。

アクションを選択すると、すべてのパラメーターバインドが呼び出されます。

概要:

- アクションは、要求の HTTP メソッドと一致している必要があります。
- アクション名がルートディクショナリの "action" エントリと一致している必要があります (存在する場合)。
- アクションのすべてのパラメーターについて、パラメーターが URI から取得されている場合は、ルートディクショナリまたは URI クエリ文字列でパラメーター名を指定する必要があります。 (省略可能なパラメーターと複合型のパラメーターは除外されます)。
- 最も多くのパラメーターを一致させてください。 最適な一致は、パラメーターのないメソッドである可能性があります。

## <a name="extended-example"></a>拡張の例

送る

[!code-csharp[Main](routing-and-action-selection/samples/sample8.cs)]

コントローラー:

[!code-csharp[Main](routing-and-action-selection/samples/sample9.cs)]

HTTP 要求:

[!code-console[Main](routing-and-action-selection/samples/sample10.cmd)]

### <a name="route-matching"></a>ルート一致

URI は "DefaultApi" という名前のルートと一致します。 ルートディクショナリには、次のエントリが含まれています。

- コントローラー: "製品"
- id: "1"

ルートディクショナリには、クエリ文字列パラメーター "version" と "details" は含まれませんが、アクションの選択時には引き続き考慮されます。

### <a name="controller-selection"></a>コントローラーの選択

ルートディクショナリの "controller" エントリから、コントローラーの種類は `ProductsController`になります。

### <a name="action-selection"></a>アクションの選択

HTTP 要求は GET 要求です。 GET をサポートするコントローラーアクションは、`GetAll`、`GetById`、および `FindProductsByName`です。 ルートディクショナリに "action" のエントリが含まれていないため、アクション名と一致する必要はありません。

次に、アクションのパラメーター名を照合して、GET アクションだけを検索します。

| アクション | 一致するパラメーター |
| --- | --- |
| `GetAll` | なし |
| `GetById` | "ID" |
| `FindProductsByName` | 指定 |

`GetById` の*バージョン*パラメーターは、省略可能なパラメーターであるため、考慮されません。

`GetAll` メソッドは普通に一致します。 ルートディクショナリに "id" が含まれているため、`GetById` メソッドも一致します。 `FindProductsByName` メソッドが一致しません。

`GetById` メソッドは、1つのパラメーターに一致するので、`GetAll`のパラメーターとは一致しないため、優先されます。 次のパラメーター値を使用してメソッドが呼び出されます。

- *id* = 1
- *バージョン*= 1.5

選択アルゴリズムで*バージョン*が使用されていなくても、パラメーターの値は URI クエリ文字列から取得されることに注意してください。

## <a name="extension-points"></a>拡張ポイント

Web API には、ルーティングプロセスの一部の拡張ポイントが用意されています。

| インターフェイス | Description |
| --- | --- |
| **IHttpControllerSelector** | コントローラーを選択します。 |
| **IHttpControllerTypeResolver** | コントローラーの種類の一覧を取得します。 **DefaultHttpControllerSelector**は、この一覧からコントローラーの種類を選択します。 |
| **IAssembliesResolver** | プロジェクトアセンブリの一覧を取得します。 **IHttpControllerTypeResolver**インターフェイスは、このリストを使用してコントローラーの種類を検索します。 |
| **IHttpControllerActivator** | 新しいコントローラーインスタンスを作成します。 |
| **IHttpActionSelector** | アクションを選択します。 |
| **IHttpActionInvoker 元** | アクションを呼び出します。 |

これらのインターフェイスのいずれかに独自の実装を提供するには、 **Httpconfiguration**オブジェクトの**Services**コレクションを使用します。

[!code-csharp[Main](routing-and-action-selection/samples/sample11.cs)]
