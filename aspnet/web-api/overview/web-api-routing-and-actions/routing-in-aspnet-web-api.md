---
uid: web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api
title: ASP.NET Web API | でのルーティングMicrosoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 10/29/2018
ms.assetid: 0675bdc7-282f-4f47-b7f3-7e02133940ca
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 85862c094cc54365267b1f21e68d235a15519cda
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449248"
---
# <a name="routing-in-aspnet-web-api"></a>ASP.NET Web API でのルーティング

[Mike Wasson](https://github.com/MikeWasson)

この記事では、ASP.NET Web API が HTTP 要求をコントローラーにルーティングする方法について説明します。

> [!NOTE]
> ASP.NET MVC を使い慣れている場合、Web API ルーティングは MVC ルーティングとよく似ています。 主な違いは、Web API は URI パスではなく HTTP 動詞を使用してアクションを選択することです。 Web API で MVC スタイルのルーティングを使用することもできます。 この記事では、ASP.NET MVC に関する知識を前提としていません。

## <a name="routing-tables"></a>ルーティングテーブル

ASP.NET Web API では、*コントローラー*は HTTP 要求を処理するクラスです。 コントローラーのパブリックメソッドは、*アクションメソッド*または単なる*アクション*と呼ばれます。 Web API フレームワークは、要求を受信すると、要求をアクションにルーティングします。

呼び出すアクションを決定するために、フレームワークは*ルーティングテーブル*を使用します。 Web API 用の Visual Studio プロジェクトテンプレートでは、既定のルートが作成されます。

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample1.cs)]

このルートは*WebApiConfig.cs*ファイルで定義されています。このファイルは、*アプリ\_の開始*ディレクトリに配置されます。

![](routing-in-aspnet-web-api/_static/image1.png)

`WebApiConfig` クラスの詳細については、「 [ASP.NET Web API の構成](../advanced/configuring-aspnet-web-api.md)」を参照してください。

Web API を自己ホストする場合は、`HttpSelfHostConfiguration` オブジェクトでルーティングテーブルを直接設定する必要があります。 詳細については、「 [WEB API をセルフホストする](../older-versions/self-host-a-web-api.md)」を参照してください。

ルーティングテーブルの各エントリには、*ルートテンプレート*が含まれています。 Web API の既定のルートテンプレートは &quot;api/{controller}/{id}&quot;です。 このテンプレートでは、&quot;api&quot; はリテラルパスセグメントで、{controller} と {id} はプレースホルダー変数です。

Web API フレームワークは HTTP 要求を受信すると、URI とルーティングテーブル内のいずれかのルートテンプレートとの照合を試みます。 一致するルートがない場合、クライアントは404エラーを受け取ります。 たとえば、次の Uri は既定のルートと一致します。

- /api/contacts
- /api/contacts/1
- /api/products/gizmo1

ただし、次の URI は一致しません。これは、&quot;api&quot; セグメントがないためです。

- /contacts/1

> [!NOTE]
> ルートで "api" を使用する理由は、ASP.NET MVC ルーティングとの競合を避けるためです。 このようにして、&quot;/連絡先&quot; MVC コントローラーにアクセスできます。また、Web API コントローラーにアクセス&quot; に &quot;/連絡先を設定することもできます。 もちろん、この規則に満足できない場合は、既定のルートテーブルを変更することができます。

一致するルートが見つかると、Web API はコントローラーとアクションを選択します。

- コントローラーを検索するために、Web API は &quot;コントローラーの&quot; を *{controller}* 変数の値に追加します。
- アクションを検索するために、Web API は HTTP 動詞を参照し、その HTTP 動詞名で始まる名前を持つアクションを検索します。 たとえば、GET 要求では、Web API は &quot;GetContact&quot; や &quot;GetAllContacts&quot;などの &quot;Get&quot;で始まるアクションを検索します。 この規則は、GET、POST、PUT、DELETE、HEAD、OPTIONS、PATCH 動詞にのみ適用されます。 他の HTTP 動詞は、コントローラーの属性を使用して有効にすることができます。 その例については後で説明します。
- *{Id}* など、ルートテンプレート内のその他のプレースホルダー変数は、アクションパラメーターにマップされます。

1 つ例を見てみましょう。 次のコントローラーを定義するとします。

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample2.cs)]

次に、使用可能な HTTP 要求と、それぞれに対して呼び出されるアクションを示します。

| HTTP 動詞 | URI パス | アクション | パラメーター |
| --- | --- | --- | --- |
| GET | api/製品 | GetAllProducts | *存在* |
| GET | api/製品/4 | GetProductById | 4 |
| DELETE | api/製品/4 | DeleteProduct | 4 |
| POST | api/製品 | *(一致なし)* |  |

URI の *{id}* セグメント (存在する場合) がアクションの*id*パラメーターにマップされていることに注意してください。 この例では、コントローラーは2つの GET メソッドを定義します。1つは*id*パラメーターを持ち、もう1つはパラメーターを指定しません。

また、コントローラーでは &quot;Post...&quot; メソッドが定義されていないため、POST 要求は失敗します。

## <a name="routing-variations"></a>ルーティングのバリエーション

前のセクションでは、ASP.NET Web API の基本的なルーティングメカニズムについて説明しています。 ここでは、いくつかのバリエーションについて説明します。

### <a name="http-verbs"></a>HTTP 動詞

HTTP 動詞の名前付け規則を使用する代わりに、次のいずれかの属性を使用してアクションメソッドを装飾することで、アクションの HTTP 動詞を明示的に指定できます。

- `[HttpGet]`
- `[HttpPut]`
- `[HttpPost]`
- `[HttpDelete]`
- `[HttpHead]`
- `[HttpOptions]`
- `[HttpPatch]`

次の例では、`FindProduct` メソッドが GET 要求にマップされます。

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample3.cs)]

アクションに対して複数の HTTP 動詞を許可したり、GET、PUT、POST、DELETE、HEAD、OPTIONS、PATCH 以外の HTTP 動詞を許可したりするには、`[AcceptVerbs]` 属性を使用します。この属性は、HTTP 動詞の一覧を受け取ります。

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample4.cs)]

<a id="routing_by_action_name"></a>
### <a name="routing-by-action-name"></a>アクション名によるルーティング

既定のルーティングテンプレートでは、Web API は HTTP 動詞を使用してアクションを選択します。 ただし、URI にアクション名が含まれているルートを作成することもできます。

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample5.cs)]

このルートテンプレートでは、 *{action}* パラメーターはコントローラーのアクションメソッドに名前を指定します。 このスタイルのルーティングでは、属性を使用して、許可される HTTP 動詞を指定します。 たとえば、コントローラーに次のメソッドがあるとします。

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample6.cs)]

この場合、"api/products/details/1" の GET 要求が `Details` メソッドにマップされます。 このスタイルのルーティングは ASP.NET MVC に似ており、RPC スタイルの API に適している場合があります。

アクション名をオーバーライドするには、`[ActionName]` 属性を使用します。 次の例では、&quot;api/製品/サムネイル/*id*にマップされる2つのアクションがあります。GET をサポートし、もう1つは POST をサポートします。

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample7.cs)]

### <a name="non-actions"></a>非アクション

メソッドがアクションとして呼び出されないようにするには、`[NonAction]` 属性を使用します。 これは、メソッドがルーティング規則と一致する場合でも、メソッドがアクションではないことをフレームワークに通知します。

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample8.cs)]

## <a name="further-reading"></a>参考資料

このトピックでは、ルーティングの概要について説明しました。 詳細については、「[ルーティングとアクションの選択](routing-and-action-selection.md)」を参照してください。これは、フレームワークがルートと URI を照合する方法を正確に説明し、コントローラーを選択して、呼び出すアクションを選択します。
