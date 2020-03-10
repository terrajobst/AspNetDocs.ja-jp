---
uid: web-api/overview/advanced/configuring-aspnet-web-api
title: ASP.NET Web API 2-ASP.NET 4.x の構成
author: MikeWasson
description: 'ASP.NET 4.x 用に ASP.NET Web API 2 を構成する: 設定、ASP.NET 4.x ホスト、OWIN 自己ホスト、グローバルサービス、およびコントローラーの事前構成を構成します。'
ms.author: riande
ms.date: 03/31/2014
ms.custom: seoapril2019
ms.assetid: 9e10a700-8d91-4d2e-a31e-b8b569fe867c
msc.legacyurl: /web-api/overview/advanced/configuring-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 4f76728fa5e4602e35e1b7cb2d41b2245093cad8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449344"
---
# <a name="configuring-aspnet-web-api-2"></a>ASP.NET Web API 2 の構成

[Mike Wasson](https://github.com/MikeWasson)

このトピックでは、ASP.NET Web API を構成する方法について説明します。

- [構成設定](#settings)
- [ASP.NET ホスティングを使用した Web API の構成](#webhost)
- [OWIN 自己ホストによる Web API の構成](#selfhost)
- [グローバル Web API サービス](#services)
- [コントローラーごとの構成](#percontrollerconfig)

<a id="settings"></a>
## <a name="configuration-settings"></a>構成設定

Web API の構成設定は、 [httpconfiguration](https://msdn.microsoft.com/library/system.web.http.httpconfiguration.aspx)クラスで定義されています。

| メンバー | Description |
| --- | --- |
| **DependencyResolver** | コントローラーの依存関係の挿入を有効にします。 「 [WEB API 依存関係競合回避モジュールの使用」を](dependency-injection.md)参照してください。 |
| **フィルター** | アクション フィルター。 |
| **逆** | [メディアの種類のフォーマッタ](../formats-and-model-binding/media-formatters.md)。 |
| **Includeerrorのポリシー** | サーバーが HTTP 応答メッセージに例外メッセージやスタックトレースなどのエラーの詳細を含める必要があるかどうかを指定します。 「 [Includeerror詳細ポリシー](https://msdn.microsoft.com/library/system.web.http.includeerrordetailpolicy(v=vs.108))」を参照してください。 |
| **初期化** | **Httpconfiguration**の最終的な初期化を実行する関数。 |
| **MessageHandlers** | [HTTP メッセージハンドラー](http-message-handlers.md)。 |
| **ParameterBindingRules もの** | コントローラーアクションのパラメーターをバインドするための規則のコレクション。 |
| **Properties** | 汎用プロパティバッグ。 |
| **ルート** | ルートのコレクション。 「 [ASP.NET Web API でのルーティング」を](../web-api-routing-and-actions/routing-in-aspnet-web-api.md)参照してください。 |
| **サービス** | サービスのコレクション。 「[サービス](#services)」を参照してください。 |

## <a name="prerequisites"></a>前提条件

[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community、Professional、または Enterprise エディション。

<a id="webhost"></a>
## <a name="configuring-web-api-with-aspnet-hosting"></a>ASP.NET ホスティングを使用した Web API の構成

ASP.NET アプリケーションで、Globalconfiguration を呼び出して Web API を構成[します。](https://msdn.microsoft.com/library/system.web.http.globalconfiguration.configure.aspx) **application\_Start**メソッドを構成します。 **Configure**メソッドは、 **httpconfiguration**型の1つのパラメーターを持つデリゲートを受け取ります。 デリゲート内ですべての構成を実行します。

匿名デリゲートを使用した例を次に示します。

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample1.cs)]

Visual Studio 2017 では、**新しい ASP.NET プロジェクト** ダイアログボックスで web API を選択した場合、"ASP.NET Web Application" プロジェクトテンプレートによって構成コードが自動的に設定されます。

[![](configuring-aspnet-web-api/_static/image2.png)](configuring-aspnet-web-api/_static/image1.png)

プロジェクトテンプレートによって、WebApiConfig.cs という名前のファイルがアプリ\_の [開始] フォルダー内に作成されます。 このコードファイルは、Web API 構成コードを配置する必要があるデリゲートを定義します。

![](configuring-aspnet-web-api/_static/image3.png)

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample2.cs?highlight=12)]

また、プロジェクトテンプレートによって、アプリケーションからデリゲートを呼び出すコード **\_開始**します。

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample3.cs?highlight=5)]

<a id="selfhost"></a>
## <a name="configuring-web-api-with-owin-self-hosting"></a>OWIN 自己ホストによる Web API の構成

OWIN を使用して自己ホストしている場合は、新しい**Httpconfiguration**インスタンスを作成します。 このインスタンスで構成を実行し、インスタンスを**UseWebApi**拡張メソッドに渡します。

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample4.cs)]

このチュートリアルでは、 [OWIN を自己ホスト ASP.NET Web API 2 に使用](../hosting-aspnet-web-api/use-owin-to-self-host-web-api.md)して、完全な手順を示します。

<a id="services"></a>
## <a name="global-web-api-services"></a>グローバル Web API サービス

**Httpconfiguration. Services**コレクションには、コントローラーの選択やコンテンツネゴシエーションなどのさまざまなタスクを実行するために Web API で使用される一連のグローバルサービスが含まれています。

> [!NOTE]
> サービス**コレクションは**、サービスの検出または依存関係の挿入のための汎用的なメカニズムではありません。 Web API フレームワークに認識されているサービスの種類のみを格納します。

**サービス**コレクションは、既定のサービスのセットを使用して初期化され、独自のカスタム実装を提供できます。 一部のサービスでは複数のインスタンスがサポートされていますが、インスタンスは1つしか持つことができません。 (ただし、コントローラーレベルでサービスを提供することもできます。「[コントローラーごとの構成](#percontrollerconfig)」を参照してください。

単一インスタンスサービス

| サービス | Description |
| --- | --- |
| **IActionValueBinder** | パラメーターのバインディングを取得します。 |
| **IApiExplorer** | アプリケーションによって公開されている Api の説明を取得します。 「 [WEB API のヘルプページを作成](../getting-started-with-aspnet-web-api/creating-api-help-pages.md)する」を参照してください。 |
| **IAssembliesResolver** | アプリケーションのアセンブリの一覧を取得します。 「[ルーティングとアクションの選択」を](../web-api-routing-and-actions/routing-and-action-selection.md)参照してください。 |
| **IBodyModelValidator** | メディアタイプフォーマッタによって要求本文から読み取られるモデルを検証します。 |
| **IContentNegotiator** | コンテンツ ネゴシエーションを実行します。 |
| **Idocumentation プロバイダー** | Api のドキュメントを提供します。 既定値は **null**です。 「 [WEB API のヘルプページを作成](../getting-started-with-aspnet-web-api/creating-api-help-pages.md)する」を参照してください。 |
| **IHostBufferPolicySelector** | ホストが HTTP メッセージエンティティ本体をバッファーする必要があるかどうかを示します。 |
| **IHttpActionInvoker 元** | コントローラーアクションを呼び出します。 「[ルーティングとアクションの選択」を](../web-api-routing-and-actions/routing-and-action-selection.md)参照してください。 |
| **IHttpActionSelector** | コントローラーアクションを選択します。 「[ルーティングとアクションの選択」を](../web-api-routing-and-actions/routing-and-action-selection.md)参照してください。 |
| **IHttpControllerActivator** | コントローラーをアクティブにします。 「[ルーティングとアクションの選択」を](../web-api-routing-and-actions/routing-and-action-selection.md)参照してください。 |
| **IHttpControllerSelector** | コントローラーを選択します。 「[ルーティングとアクションの選択」を](../web-api-routing-and-actions/routing-and-action-selection.md)参照してください。 |
| **IHttpControllerTypeResolver** | アプリケーションの Web API コントローラーの種類の一覧を提供します。 「[ルーティングとアクションの選択」を](../web-api-routing-and-actions/routing-and-action-selection.md)参照してください。 |
| **ITraceManager** | トレースフレームワークを初期化します。 「 [ASP.NET Web API でのトレース」を](../testing-and-debugging/tracing-in-aspnet-web-api.md)参照してください。 |
| **ITraceWriter** | トレースライターを提供します。 既定値は "no op" トレースライターです。 「 [ASP.NET Web API でのトレース」を](../testing-and-debugging/tracing-in-aspnet-web-api.md)参照してください。 |
| **IModelValidatorCache** | モデルの検証コントロールのキャッシュを提供します。 |

複数インスタンスサービス

|                 サービス                 |                                                                                                              Description                                                                                                               |
|-----------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    <strong>IFilterProvider</strong>     |                                                                                           コントローラーアクションのフィルターの一覧を返します。                                                                                           |
|  <strong>ModelBinderProvider</strong>   |                                                                                                指定された型のモデルバインダーを返します。                                                                                                |
| <strong>ModelMetadataProvider</strong>  |                                                                                                     モデルのメタデータを提供します。                                                                                                     |
| <strong>ModelValidatorProvider</strong> |                                                                                                   モデルの検証コントロールを提供します。                                                                                                    |
|  <strong>ValueProviderFactory</strong>  | 値プロバイダーを作成します。 詳細については、「 [WebAPI でカスタム値プロバイダーを作成する方法](https://blogs.msdn.com/b/jmstall/archive/2012/04/23/how-to-create-a-custom-value-provider-in-webapi.aspx)」を参照してください。 |

カスタム実装をマルチインスタンスサービスに追加するには、**サービス**コレクションで**Add**または**Insert**を呼び出します。

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample5.cs)]

単一インスタンスサービスをカスタム実装に置き換えるには、**サービス**コレクションで**replace**を呼び出します。

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample6.cs)]

<a id="percontrollerconfig"></a>
## <a name="per-controller-configuration"></a>コントローラーごとの構成

次の設定は、コントローラーごとにオーバーライドできます。

- メディアの種類のフォーマッタ
- パラメーターのバインド規則
- サービス

これを行うには、 **IControllerConfiguration**インターフェイスを実装するカスタム属性を定義します。 次に、コントローラーに属性を適用します。

既定のメディアタイプフォーマッタをカスタムフォーマッタに置き換える例を次に示します。

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample7.cs)]

**IControllerConfiguration**メソッドは、次の2つのパラメーターを受け取ります。

- **Httpコントローラー設定**オブジェクト
- **Httpコントローラー記述子**オブジェクト

**Httpcontroller 記述子**には、コントローラーの説明が含まれています。これは、2つのコントローラーを区別するために、情報を調べるために使用できます。

**Httpcontroller 設定**オブジェクトを使用してコントローラーを構成します。 このオブジェクトには、コントローラーごとにオーバーライドできる構成パラメーターのサブセットが含まれています。 変更しない設定は、既定でグローバル**Httpconfiguration**オブジェクトに設定されます。
