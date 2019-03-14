---
title: Razor のコンポーネントの依存関係の挿入
author: guardrex
description: コンポーネントに挿入することによって、Blazor と剃刀コンポーネントのアプリケーションが組み込みサービスを使用する方法を参照してください。
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 01/29/2019
uid: razor-components/dependency-injection
ms.openlocfilehash: 6ce8fa74f20145f48797d267c20ef2593368b941
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57042429"
---
# <a name="razor-components-dependency-injection"></a>Razor のコンポーネントの依存関係の挿入

によって[Rainer Stropek](https://www.timecockpit.com)

[依存関係の注入 (DI)](/aspnet/core/fundamentals/dependency-injection)が組み込まれています。 アプリでは、コンポーネントに挿入することによって、組み込みのサービスを使用できます。 アプリは、カスタム サービスを定義し、DI 経由で利用できるようにすることができますも。

## <a name="dependency-injection"></a>依存関係の挿入

DI は、中央の場所に構成されているサービスにアクセスするための手法です。 これに役に立ちます。

* 多くのコンポーネント間でのサービス クラスの 1 つのインスタンスの共有 (と呼ばれる、*シングルトン*サービス)。
* 特定のサービスの具象クラスからコンポーネントを分離し、のみの抽象化を参照します。 たとえば、インターフェイス`IDataAccess`具象クラスによって実装されます`DataAccess`します。 コンポーネントが受信する DI を使用する場合、`IDataAccess`コンポーネントの実装が具象型に結合されていません。 おそらく、実装は、単体テストでモック実装にはスワップできます。

DI システムは、サービスをコンポーネントのインスタンスの提供を担当します。 DI では、サービス自体は、さらにサービスに依存できるように依存関係を再帰的にも解決されます。 DI はアプリの起動中に構成されます。 このトピックの「例を示します。

## <a name="add-services-to-di"></a>DI にサービスを追加します。

新しいアプリを作成すると、確認、`Startup.ConfigureServices`メソッド。

```csharp
public void ConfigureServices(IServiceCollection services)
{
    // Add custom services here
}
```

`ConfigureServices`メソッドに渡されますが、 [IServiceCollection](/dotnet/api/microsoft.extensions.dependencyinjection.iservicecollection)、サービスの記述子オブジェクトの一覧 ([ServiceDescriptor](/dotnet/api/microsoft.extensions.dependencyinjection.servicedescriptor))。 サービスは、サービスのコレクションにサービスの記述子を提供することによって追加されます。 次のコード サンプルでは、概念を示しています。

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddSingleton<IDataAccess, DataAccess>();
}
```

サービスは、次の有効期間で構成できます。

| メソッド      | 説明 |
| ----------- | ----------- |
| [シングルトン](/dotnet/api/microsoft.extensions.dependencyinjection.servicedescriptor.singleton#Microsoft_Extensions_DependencyInjection_ServiceDescriptor_Singleton__1_System_Func_System_IServiceProvider___0__) | DI を作成、*単一インスタンス*のサービス。 このサービスを必要とするすべてのコンポーネントは、このインスタンスへの参照を受け取ります。 |
| [一時的](/dotnet/api/microsoft.extensions.dependencyinjection.servicedescriptor.transient) | 受信コンポーネントは、このサービスを必要とするたびに、*新しいインスタンス*サービス。 |
| [スコープ](/dotnet/api/microsoft.extensions.dependencyinjection.servicedescriptor.scoped) | クライアント側 Blazor 現在 DI スコープの概念はありません。 `Scoped` ように動作`Singleton`します。 ただし、ASP.NET Core Razor のコンポーネントのサポート、`Scoped`有効期間。 Razor のコンポーネントでは、スコープ化されたサービスの登録は、接続に制限されます。 このため、スコープを持つサービスを使用して、現在のユーザーにスコープする必要がありますサービスの優先が (現在の目的は、クライアント側で実行する場合でも、ブラウザーで)。 |

DI システムは、ASP.NET Core で DI システムに基づきます。 詳細については、次を参照してください。 [ASP.NET Core の依存関係挿入](/aspnet/core/fundamentals/dependency-injection)します。

## <a name="default-services"></a>既定のサービス

既定のサービスは、アプリのサービスのコレクションに自動的に追加されます。 次の表では、提供される便利な既定のサービスの一部を示します。

| メソッド       | 説明 |
| ------------ | ----------- |
| [HttpClient](/dotnet/api/system.net.http.httpclient) | HTTP 要求の送信と URI (シングルトン) で識別されるリソースから HTTP 応答を受信するメソッドを提供します。 注意のこのインスタンス`HttpClient`バック グラウンドで HTTP トラフィックを処理するため、ブラウザーを使用します。 [HttpClient.BaseAddress](/dotnet/api/system.net.http.httpclient.baseaddress)アプリのベース URI プレフィックスが自動的に設定します。 `HttpClient` クライアント側 Blazor アプリにのみ提供されます。 |
| `IJSRuntime` | JavaScript ランタイムの呼び出しをディスパッチできますのインスタンスを表します。 詳細については、「 <xref:razor-components/javascript-interop> 」を参照してください。 |
| `IUriHelper` | Uri およびナビゲーションの状態 (シングルトン) を操作するためのヘルパー。 `IUriHelper` 両方のクライアント側 Blazor と ASP.NET Core の Razor コンポーネント アプリに提供されます。 |

既定のテンプレートによって追加される既定のサービス プロバイダーではなく、カスタム サービス プロバイダーを使用することに注意してください。 カスタム サービス プロバイダーは、表に示す既定のサービスを自動的に提供しません。 これらのサービスは、新しいサービス プロバイダーに明示的に追加する必要があります。

## <a name="request-a-service-in-a-component"></a>要求では、コンポーネント サービス

使用して、コンポーネントの Razor テンプレートに挿入するサービスがサービス コレクションに追加されると、それらの`@inject`Razor ディレクティブ。 `@inject` 2 つのパラメーターがあります。

* 型名:挿入するサービスの型。
* プロパティ名:挿入された app service の受信プロパティの名前。 プロパティが手動で作成を必要としないことに注意してください。 コンパイラは、プロパティを作成します。

複数`@inject`ステートメントを使用して、さまざまなサービスを挿入することができます。

次の例は、`@inject` を使用する方法を示しています。 実装するサービス`Services.IDataAccess`コンポーネントのプロパティには挿入`DataRepository`します。 コードがのみを使用する方法に注意してください、`IDataAccess`抽象化します。

```csharp
@page "/customer-list"
@using Services
@inject IDataAccess DataRepository

<ul>
    @if (Customers != null)
    {
        @foreach (var customer in Customers)
        {
            <li>@customer.FirstName @customer.LastName</li>
        }
    }
</ul>

@functions {
    private IReadOnlyList<Customer> Customers;

    protected override async Task OnInitAsync()
    {
        // The property DataRepository received an implementation
        // of IDataAccess through dependency injection. Use 
        // DataRepository to obtain data from the server.
        Customers = await DataRepository.GetAllCustomersAsync();
    }
}
```

内部的には、生成されたプロパティ (`DataRepository`) で修飾されたが、`InjectAttribute`属性。 通常、この属性は、直接使用されません。 基底クラスはコンポーネントに必要な場合に挿入されたプロパティは、基底クラスに必要なも`InjectAttribute`手動で追加することができます。

```csharp
public class ComponentBase : BlazorComponent
{
    // Dependency injection works even if using the
    // InjectAttribute in a component's base class.
    [Inject]
    protected IDataAccess DataRepository { get; set; }
    ...
}
```

基本クラスから派生したコンポーネントで、`@inject`ディレクティブは必要ありません。 `InjectAttribute`の基本クラスで十分です。

```csharp
@page "/demo"
@inherits ComponentBase

<h1>...</h1>
...
```

## <a name="dependency-injection-in-services"></a>サービスの依存関係の挿入

複雑なサービスには、その他のサービスが必要です。 前の例では、`DataAccess`必要があります、`HttpClient`既定のサービスです。 `@inject` または、`InjectAttribute`サービスでは使用できません。 *コンス トラクターの挿入*代わりに使用する必要があります。 必要なサービスを追加するには、サービスのコンス トラクターにパラメーターを追加します。 依存関係の挿入は、サービスを作成するときに、コンス トラクターで必要し、するにはそれに応じて、サービスを認識します。

次のコード サンプルでは、概念を示しています。

```csharp
public class DataAccess : IDataAccess
{
    // The constructor receives an HttpClient via dependency
    // injection. HttpClient is a default service.
    public DataAccess(HttpClient client)
    {
        ...
    }
    ...
}
```

コンス トラクターの挿入の次の前提条件に注意してください。

* 1 つのコンス トラクター引数はすべてによって満たすことが依存関係の挿入が必要があります。 それらの既定値は指定されている場合、DI でカバーされない追加のパラメーターが許可されることに注意してください。
* 該当するコンス トラクターがある必要があります*パブリック*します。
* 該当するコンス トラクターの 1 つだけあります。 DI は、あいまいさが発生した場合、例外をスローします。

## <a name="additional-resources"></a>その他の技術情報

* [ASP.NET Core での依存関係の挿入](/aspnet/core/fundamentals/dependency-injection)
