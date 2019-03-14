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
# <a name="razor-components-dependency-injection"></a><span data-ttu-id="b6bb0-103">Razor のコンポーネントの依存関係の挿入</span><span class="sxs-lookup"><span data-stu-id="b6bb0-103">Razor Components dependency injection</span></span>

<span data-ttu-id="b6bb0-104">によって[Rainer Stropek](https://www.timecockpit.com)</span><span class="sxs-lookup"><span data-stu-id="b6bb0-104">By [Rainer Stropek](https://www.timecockpit.com)</span></span>

<span data-ttu-id="b6bb0-105">[依存関係の注入 (DI)](/aspnet/core/fundamentals/dependency-injection)が組み込まれています。</span><span class="sxs-lookup"><span data-stu-id="b6bb0-105">[Dependency injection (DI)](/aspnet/core/fundamentals/dependency-injection) is built-in.</span></span> <span data-ttu-id="b6bb0-106">アプリでは、コンポーネントに挿入することによって、組み込みのサービスを使用できます。</span><span class="sxs-lookup"><span data-stu-id="b6bb0-106">Apps can use built-in services by having them injected into components.</span></span> <span data-ttu-id="b6bb0-107">アプリは、カスタム サービスを定義し、DI 経由で利用できるようにすることができますも。</span><span class="sxs-lookup"><span data-stu-id="b6bb0-107">Apps can also define custom services and make them available via DI.</span></span>

## <a name="dependency-injection"></a><span data-ttu-id="b6bb0-108">依存関係の挿入</span><span class="sxs-lookup"><span data-stu-id="b6bb0-108">Dependency injection</span></span>

<span data-ttu-id="b6bb0-109">DI は、中央の場所に構成されているサービスにアクセスするための手法です。</span><span class="sxs-lookup"><span data-stu-id="b6bb0-109">DI is a technique for accessing services configured in a central location.</span></span> <span data-ttu-id="b6bb0-110">これに役に立ちます。</span><span class="sxs-lookup"><span data-stu-id="b6bb0-110">This can be useful to:</span></span>

* <span data-ttu-id="b6bb0-111">多くのコンポーネント間でのサービス クラスの 1 つのインスタンスの共有 (と呼ばれる、*シングルトン*サービス)。</span><span class="sxs-lookup"><span data-stu-id="b6bb0-111">Share a single instance of a service class across many components (known as a *singleton* service).</span></span>
* <span data-ttu-id="b6bb0-112">特定のサービスの具象クラスからコンポーネントを分離し、のみの抽象化を参照します。</span><span class="sxs-lookup"><span data-stu-id="b6bb0-112">Decouple components from particular concrete service classes and only reference abstractions.</span></span> <span data-ttu-id="b6bb0-113">たとえば、インターフェイス`IDataAccess`具象クラスによって実装されます`DataAccess`します。</span><span class="sxs-lookup"><span data-stu-id="b6bb0-113">For example, an interface `IDataAccess` is implemented by a concrete class `DataAccess`.</span></span> <span data-ttu-id="b6bb0-114">コンポーネントが受信する DI を使用する場合、`IDataAccess`コンポーネントの実装が具象型に結合されていません。</span><span class="sxs-lookup"><span data-stu-id="b6bb0-114">When a component uses DI to receive an `IDataAccess` implementation, the component isn't coupled to the concrete type.</span></span> <span data-ttu-id="b6bb0-115">おそらく、実装は、単体テストでモック実装にはスワップできます。</span><span class="sxs-lookup"><span data-stu-id="b6bb0-115">The implementation can be swapped, perhaps to a mock implementation in unit tests.</span></span>

<span data-ttu-id="b6bb0-116">DI システムは、サービスをコンポーネントのインスタンスの提供を担当します。</span><span class="sxs-lookup"><span data-stu-id="b6bb0-116">The DI system is responsible for supplying instances of services to components.</span></span> <span data-ttu-id="b6bb0-117">DI では、サービス自体は、さらにサービスに依存できるように依存関係を再帰的にも解決されます。</span><span class="sxs-lookup"><span data-stu-id="b6bb0-117">DI also resolves dependencies recursively so that services themselves can depend on further services.</span></span> <span data-ttu-id="b6bb0-118">DI はアプリの起動中に構成されます。</span><span class="sxs-lookup"><span data-stu-id="b6bb0-118">DI is configured during startup of the app.</span></span> <span data-ttu-id="b6bb0-119">このトピックの「例を示します。</span><span class="sxs-lookup"><span data-stu-id="b6bb0-119">An example is shown later in this topic.</span></span>

## <a name="add-services-to-di"></a><span data-ttu-id="b6bb0-120">DI にサービスを追加します。</span><span class="sxs-lookup"><span data-stu-id="b6bb0-120">Add services to DI</span></span>

<span data-ttu-id="b6bb0-121">新しいアプリを作成すると、確認、`Startup.ConfigureServices`メソッド。</span><span class="sxs-lookup"><span data-stu-id="b6bb0-121">After creating a new app, examine the `Startup.ConfigureServices` method:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    // Add custom services here
}
```

<span data-ttu-id="b6bb0-122">`ConfigureServices`メソッドに渡されますが、 [IServiceCollection](/dotnet/api/microsoft.extensions.dependencyinjection.iservicecollection)、サービスの記述子オブジェクトの一覧 ([ServiceDescriptor](/dotnet/api/microsoft.extensions.dependencyinjection.servicedescriptor))。</span><span class="sxs-lookup"><span data-stu-id="b6bb0-122">The `ConfigureServices` method is passed an [IServiceCollection](/dotnet/api/microsoft.extensions.dependencyinjection.iservicecollection), which is a list of service descriptor objects ([ServiceDescriptor](/dotnet/api/microsoft.extensions.dependencyinjection.servicedescriptor)).</span></span> <span data-ttu-id="b6bb0-123">サービスは、サービスのコレクションにサービスの記述子を提供することによって追加されます。</span><span class="sxs-lookup"><span data-stu-id="b6bb0-123">Services are added by providing service descriptors to the service collection.</span></span> <span data-ttu-id="b6bb0-124">次のコード サンプルでは、概念を示しています。</span><span class="sxs-lookup"><span data-stu-id="b6bb0-124">The following code sample demonstrates the concept:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddSingleton<IDataAccess, DataAccess>();
}
```

<span data-ttu-id="b6bb0-125">サービスは、次の有効期間で構成できます。</span><span class="sxs-lookup"><span data-stu-id="b6bb0-125">Services can be configured with the following lifetimes:</span></span>

| <span data-ttu-id="b6bb0-126">メソッド</span><span class="sxs-lookup"><span data-stu-id="b6bb0-126">Method</span></span>      | <span data-ttu-id="b6bb0-127">説明</span><span class="sxs-lookup"><span data-stu-id="b6bb0-127">Description</span></span> |
| ----------- | ----------- |
| [<span data-ttu-id="b6bb0-128">シングルトン</span><span class="sxs-lookup"><span data-stu-id="b6bb0-128">Singleton</span></span>](/dotnet/api/microsoft.extensions.dependencyinjection.servicedescriptor.singleton#Microsoft_Extensions_DependencyInjection_ServiceDescriptor_Singleton__1_System_Func_System_IServiceProvider___0__) | <span data-ttu-id="b6bb0-129">DI を作成、*単一インスタンス*のサービス。</span><span class="sxs-lookup"><span data-stu-id="b6bb0-129">DI creates a *single instance* of the service.</span></span> <span data-ttu-id="b6bb0-130">このサービスを必要とするすべてのコンポーネントは、このインスタンスへの参照を受け取ります。</span><span class="sxs-lookup"><span data-stu-id="b6bb0-130">All components requiring this service receive a reference to this instance.</span></span> |
| [<span data-ttu-id="b6bb0-131">一時的</span><span class="sxs-lookup"><span data-stu-id="b6bb0-131">Transient</span></span>](/dotnet/api/microsoft.extensions.dependencyinjection.servicedescriptor.transient) | <span data-ttu-id="b6bb0-132">受信コンポーネントは、このサービスを必要とするたびに、*新しいインスタンス*サービス。</span><span class="sxs-lookup"><span data-stu-id="b6bb0-132">Whenever a component requires this service, it receives a *new instance* of the service.</span></span> |
| [<span data-ttu-id="b6bb0-133">スコープ</span><span class="sxs-lookup"><span data-stu-id="b6bb0-133">Scoped</span></span>](/dotnet/api/microsoft.extensions.dependencyinjection.servicedescriptor.scoped) | <span data-ttu-id="b6bb0-134">クライアント側 Blazor 現在 DI スコープの概念はありません。</span><span class="sxs-lookup"><span data-stu-id="b6bb0-134">Client-side Blazor doesn't currently have the concept of DI scopes.</span></span> <span data-ttu-id="b6bb0-135">`Scoped` ように動作`Singleton`します。</span><span class="sxs-lookup"><span data-stu-id="b6bb0-135">`Scoped` behaves like `Singleton`.</span></span> <span data-ttu-id="b6bb0-136">ただし、ASP.NET Core Razor のコンポーネントのサポート、`Scoped`有効期間。</span><span class="sxs-lookup"><span data-stu-id="b6bb0-136">However, ASP.NET Core Razor Components support the `Scoped` lifetime.</span></span> <span data-ttu-id="b6bb0-137">Razor のコンポーネントでは、スコープ化されたサービスの登録は、接続に制限されます。</span><span class="sxs-lookup"><span data-stu-id="b6bb0-137">In a Razor Component, a scoped service registration is scoped to the connection.</span></span> <span data-ttu-id="b6bb0-138">このため、スコープを持つサービスを使用して、現在のユーザーにスコープする必要がありますサービスの優先が (現在の目的は、クライアント側で実行する場合でも、ブラウザーで)。</span><span class="sxs-lookup"><span data-stu-id="b6bb0-138">For this reason, using scoped services is preferred for services that should be scoped to the current user (even if the current intent is to run client-side in the browser).</span></span> |

<span data-ttu-id="b6bb0-139">DI システムは、ASP.NET Core で DI システムに基づきます。</span><span class="sxs-lookup"><span data-stu-id="b6bb0-139">The DI system is based on the DI system in ASP.NET Core.</span></span> <span data-ttu-id="b6bb0-140">詳細については、次を参照してください。 [ASP.NET Core の依存関係挿入](/aspnet/core/fundamentals/dependency-injection)します。</span><span class="sxs-lookup"><span data-stu-id="b6bb0-140">For more information, see [Dependency injection in ASP.NET Core](/aspnet/core/fundamentals/dependency-injection).</span></span>

## <a name="default-services"></a><span data-ttu-id="b6bb0-141">既定のサービス</span><span class="sxs-lookup"><span data-stu-id="b6bb0-141">Default services</span></span>

<span data-ttu-id="b6bb0-142">既定のサービスは、アプリのサービスのコレクションに自動的に追加されます。</span><span class="sxs-lookup"><span data-stu-id="b6bb0-142">Default services are automatically added to the service collection of an app.</span></span> <span data-ttu-id="b6bb0-143">次の表では、提供される便利な既定のサービスの一部を示します。</span><span class="sxs-lookup"><span data-stu-id="b6bb0-143">The following table shows some of the useful default services provided.</span></span>

| <span data-ttu-id="b6bb0-144">メソッド</span><span class="sxs-lookup"><span data-stu-id="b6bb0-144">Method</span></span>       | <span data-ttu-id="b6bb0-145">説明</span><span class="sxs-lookup"><span data-stu-id="b6bb0-145">Description</span></span> |
| ------------ | ----------- |
| [<span data-ttu-id="b6bb0-146">HttpClient</span><span class="sxs-lookup"><span data-stu-id="b6bb0-146">HttpClient</span></span>](/dotnet/api/system.net.http.httpclient) | <span data-ttu-id="b6bb0-147">HTTP 要求の送信と URI (シングルトン) で識別されるリソースから HTTP 応答を受信するメソッドを提供します。</span><span class="sxs-lookup"><span data-stu-id="b6bb0-147">Provides methods for sending HTTP requests and receiving HTTP responses from a resource identified by a URI (singleton).</span></span> <span data-ttu-id="b6bb0-148">注意のこのインスタンス`HttpClient`バック グラウンドで HTTP トラフィックを処理するため、ブラウザーを使用します。</span><span class="sxs-lookup"><span data-stu-id="b6bb0-148">Note that this instance of `HttpClient` uses the browser for handling the HTTP traffic in the background.</span></span> <span data-ttu-id="b6bb0-149">[HttpClient.BaseAddress](/dotnet/api/system.net.http.httpclient.baseaddress)アプリのベース URI プレフィックスが自動的に設定します。</span><span class="sxs-lookup"><span data-stu-id="b6bb0-149">[HttpClient.BaseAddress](/dotnet/api/system.net.http.httpclient.baseaddress) is automatically set to the base URI prefix of the app.</span></span> <span data-ttu-id="b6bb0-150">`HttpClient` クライアント側 Blazor アプリにのみ提供されます。</span><span class="sxs-lookup"><span data-stu-id="b6bb0-150">`HttpClient` is only provided to client-side Blazor apps.</span></span> |
| `IJSRuntime` | <span data-ttu-id="b6bb0-151">JavaScript ランタイムの呼び出しをディスパッチできますのインスタンスを表します。</span><span class="sxs-lookup"><span data-stu-id="b6bb0-151">Represents an instance of a JavaScript runtime to which calls may be dispatched.</span></span> <span data-ttu-id="b6bb0-152">詳細については、「 <xref:razor-components/javascript-interop> 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="b6bb0-152">For more information, see <xref:razor-components/javascript-interop>.</span></span> |
| `IUriHelper` | <span data-ttu-id="b6bb0-153">Uri およびナビゲーションの状態 (シングルトン) を操作するためのヘルパー。</span><span class="sxs-lookup"><span data-stu-id="b6bb0-153">Helpers for working with URIs and navigation state (singleton).</span></span> <span data-ttu-id="b6bb0-154">`IUriHelper` 両方のクライアント側 Blazor と ASP.NET Core の Razor コンポーネント アプリに提供されます。</span><span class="sxs-lookup"><span data-stu-id="b6bb0-154">`IUriHelper` is provided to both client-side Blazor and ASP.NET Core Razor Components apps.</span></span> |

<span data-ttu-id="b6bb0-155">既定のテンプレートによって追加される既定のサービス プロバイダーではなく、カスタム サービス プロバイダーを使用することに注意してください。</span><span class="sxs-lookup"><span data-stu-id="b6bb0-155">Note that it is possible to use a custom services provider instead of the default service provider that's added by the default template.</span></span> <span data-ttu-id="b6bb0-156">カスタム サービス プロバイダーは、表に示す既定のサービスを自動的に提供しません。</span><span class="sxs-lookup"><span data-stu-id="b6bb0-156">A custom service provider doesn't automatically provide the default services listed in the table.</span></span> <span data-ttu-id="b6bb0-157">これらのサービスは、新しいサービス プロバイダーに明示的に追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b6bb0-157">Those services must be added to the new service provider explicitly.</span></span>

## <a name="request-a-service-in-a-component"></a><span data-ttu-id="b6bb0-158">要求では、コンポーネント サービス</span><span class="sxs-lookup"><span data-stu-id="b6bb0-158">Request a service in a component</span></span>

<span data-ttu-id="b6bb0-159">使用して、コンポーネントの Razor テンプレートに挿入するサービスがサービス コレクションに追加されると、それらの`@inject`Razor ディレクティブ。</span><span class="sxs-lookup"><span data-stu-id="b6bb0-159">Once services are added to the service collection, they can be injected into the components' Razor templates using the `@inject` Razor directive.</span></span> <span data-ttu-id="b6bb0-160">`@inject` 2 つのパラメーターがあります。</span><span class="sxs-lookup"><span data-stu-id="b6bb0-160">`@inject` has two parameters:</span></span>

* <span data-ttu-id="b6bb0-161">型名:挿入するサービスの型。</span><span class="sxs-lookup"><span data-stu-id="b6bb0-161">Type name: The type of the service to inject.</span></span>
* <span data-ttu-id="b6bb0-162">プロパティ名:挿入された app service の受信プロパティの名前。</span><span class="sxs-lookup"><span data-stu-id="b6bb0-162">Property name: The name of the property receiving the injected app service.</span></span> <span data-ttu-id="b6bb0-163">プロパティが手動で作成を必要としないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="b6bb0-163">Note that the property doesn't require manual creation.</span></span> <span data-ttu-id="b6bb0-164">コンパイラは、プロパティを作成します。</span><span class="sxs-lookup"><span data-stu-id="b6bb0-164">The compiler creates the property.</span></span>

<span data-ttu-id="b6bb0-165">複数`@inject`ステートメントを使用して、さまざまなサービスを挿入することができます。</span><span class="sxs-lookup"><span data-stu-id="b6bb0-165">Multiple `@inject` statements can be used to inject different services.</span></span>

<span data-ttu-id="b6bb0-166">次の例は、`@inject` を使用する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="b6bb0-166">The following example shows how to use `@inject`.</span></span> <span data-ttu-id="b6bb0-167">実装するサービス`Services.IDataAccess`コンポーネントのプロパティには挿入`DataRepository`します。</span><span class="sxs-lookup"><span data-stu-id="b6bb0-167">The service implementing `Services.IDataAccess` is injected into the component's property `DataRepository`.</span></span> <span data-ttu-id="b6bb0-168">コードがのみを使用する方法に注意してください、`IDataAccess`抽象化します。</span><span class="sxs-lookup"><span data-stu-id="b6bb0-168">Note how the code is only using the `IDataAccess` abstraction:</span></span>

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

<span data-ttu-id="b6bb0-169">内部的には、生成されたプロパティ (`DataRepository`) で修飾されたが、`InjectAttribute`属性。</span><span class="sxs-lookup"><span data-stu-id="b6bb0-169">Internally, the generated property (`DataRepository`) is decorated with the `InjectAttribute` attribute.</span></span> <span data-ttu-id="b6bb0-170">通常、この属性は、直接使用されません。</span><span class="sxs-lookup"><span data-stu-id="b6bb0-170">Typically, this attribute isn't used directly.</span></span> <span data-ttu-id="b6bb0-171">基底クラスはコンポーネントに必要な場合に挿入されたプロパティは、基底クラスに必要なも`InjectAttribute`手動で追加することができます。</span><span class="sxs-lookup"><span data-stu-id="b6bb0-171">If a base class is required for components and injected properties are also required for the base class, `InjectAttribute` can be manually added:</span></span>

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

<span data-ttu-id="b6bb0-172">基本クラスから派生したコンポーネントで、`@inject`ディレクティブは必要ありません。</span><span class="sxs-lookup"><span data-stu-id="b6bb0-172">In components derived from the base class, the `@inject` directive isn't required.</span></span> <span data-ttu-id="b6bb0-173">`InjectAttribute`の基本クラスで十分です。</span><span class="sxs-lookup"><span data-stu-id="b6bb0-173">The `InjectAttribute` of the base class is sufficient:</span></span>

```csharp
@page "/demo"
@inherits ComponentBase

<h1>...</h1>
...
```

## <a name="dependency-injection-in-services"></a><span data-ttu-id="b6bb0-174">サービスの依存関係の挿入</span><span class="sxs-lookup"><span data-stu-id="b6bb0-174">Dependency injection in services</span></span>

<span data-ttu-id="b6bb0-175">複雑なサービスには、その他のサービスが必要です。</span><span class="sxs-lookup"><span data-stu-id="b6bb0-175">Complex services might require additional services.</span></span> <span data-ttu-id="b6bb0-176">前の例では、`DataAccess`必要があります、`HttpClient`既定のサービスです。</span><span class="sxs-lookup"><span data-stu-id="b6bb0-176">In the prior example, `DataAccess` might require the `HttpClient` default service.</span></span> <span data-ttu-id="b6bb0-177">`@inject` または、`InjectAttribute`サービスでは使用できません。</span><span class="sxs-lookup"><span data-stu-id="b6bb0-177">`@inject` or the `InjectAttribute` can't be used in services.</span></span> <span data-ttu-id="b6bb0-178">*コンス トラクターの挿入*代わりに使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b6bb0-178">*Constructor injection* must be used instead.</span></span> <span data-ttu-id="b6bb0-179">必要なサービスを追加するには、サービスのコンス トラクターにパラメーターを追加します。</span><span class="sxs-lookup"><span data-stu-id="b6bb0-179">Required services are added by adding parameters to the service's constructor.</span></span> <span data-ttu-id="b6bb0-180">依存関係の挿入は、サービスを作成するときに、コンス トラクターで必要し、するにはそれに応じて、サービスを認識します。</span><span class="sxs-lookup"><span data-stu-id="b6bb0-180">When dependency injection creates the service, it recognizes the services it requires in the constructor and provides them accordingly.</span></span>

<span data-ttu-id="b6bb0-181">次のコード サンプルでは、概念を示しています。</span><span class="sxs-lookup"><span data-stu-id="b6bb0-181">The following code sample demonstrates the concept:</span></span>

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

<span data-ttu-id="b6bb0-182">コンス トラクターの挿入の次の前提条件に注意してください。</span><span class="sxs-lookup"><span data-stu-id="b6bb0-182">Note the following prerequisites for constructor injection:</span></span>

* <span data-ttu-id="b6bb0-183">1 つのコンス トラクター引数はすべてによって満たすことが依存関係の挿入が必要があります。</span><span class="sxs-lookup"><span data-stu-id="b6bb0-183">There must be one constructor whose arguments can all be fulfilled by dependency injection.</span></span> <span data-ttu-id="b6bb0-184">それらの既定値は指定されている場合、DI でカバーされない追加のパラメーターが許可されることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="b6bb0-184">Note that additional parameters not covered by DI are allowed if default values are specified for them.</span></span>
* <span data-ttu-id="b6bb0-185">該当するコンス トラクターがある必要があります*パブリック*します。</span><span class="sxs-lookup"><span data-stu-id="b6bb0-185">The applicable constructor must be *public*.</span></span>
* <span data-ttu-id="b6bb0-186">該当するコンス トラクターの 1 つだけあります。</span><span class="sxs-lookup"><span data-stu-id="b6bb0-186">There must only be one applicable constructor.</span></span> <span data-ttu-id="b6bb0-187">DI は、あいまいさが発生した場合、例外をスローします。</span><span class="sxs-lookup"><span data-stu-id="b6bb0-187">In case of an ambiguity, DI throws an exception.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b6bb0-188">その他の技術情報</span><span class="sxs-lookup"><span data-stu-id="b6bb0-188">Additional resources</span></span>

* [<span data-ttu-id="b6bb0-189">ASP.NET Core での依存関係の挿入</span><span class="sxs-lookup"><span data-stu-id="b6bb0-189">Dependency injection in ASP.NET Core</span></span>](/aspnet/core/fundamentals/dependency-injection)
