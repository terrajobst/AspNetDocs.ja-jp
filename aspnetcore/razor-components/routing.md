---
title: ルーティング razor コンポーネント
author: guardrex
description: アプリや NavLink コンポーネントの詳細については、要求をルーティングする方法について説明します。
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 02/01/2019
uid: razor-components/routing
ms.openlocfilehash: 5c648ba1bb3846f5baa515e808a98a3b33f81438
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57031609"
---
# <a name="razor-components-routing"></a><span data-ttu-id="a813d-103">ルーティング razor コンポーネント</span><span class="sxs-lookup"><span data-stu-id="a813d-103">Razor Components routing</span></span>

<span data-ttu-id="a813d-104">作成者: [Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="a813d-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="a813d-105">アプリや NavLink コンポーネントの詳細については、要求をルーティングする方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="a813d-105">Learn how to route requests in apps and about the NavLink component.</span></span>

<span data-ttu-id="a813d-106">[サンプル コードを表示またはダウンロード](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-components/common/samples/)します ([ダウンロード方法](xref:index#how-to-download-a-sample))。</span><span class="sxs-lookup"><span data-stu-id="a813d-106">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-components/common/samples/) ([how to download](xref:index#how-to-download-a-sample)).</span></span> <span data-ttu-id="a813d-107">前提条件については、[作業開始](xref:razor-components/get-started)に関するトピックをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="a813d-107">See the [Get started](xref:razor-components/get-started) topic for prerequisites.</span></span>

## <a name="route-templates"></a><span data-ttu-id="a813d-108">ルート テンプレート</span><span class="sxs-lookup"><span data-stu-id="a813d-108">Route templates</span></span>

<span data-ttu-id="a813d-109">`<Router>`ルーティング、コンポーネントを使用して、ルート テンプレートは、アクセス可能な各コンポーネントに提供されます。</span><span class="sxs-lookup"><span data-stu-id="a813d-109">The `<Router>` component enables routing, and a route template is provided to each accessible component.</span></span> <span data-ttu-id="a813d-110">`<Router>`コンポーネントに表示されます、 *App.cshtml*ファイル。</span><span class="sxs-lookup"><span data-stu-id="a813d-110">The `<Router>` component appears in the *App.cshtml* file:</span></span>

```cshtml
<Router AppAssembly=typeof(Program).Assembly />
```

<span data-ttu-id="a813d-111">ときに、  *\*.cshtml*ファイルと、`@page`ディレクティブをコンパイルすると、生成されたクラスが指定された、 [RouteAttribute](/dotnet/api/microsoft.aspnetcore.mvc.routeattribute)ルート テンプレートを指定します。</span><span class="sxs-lookup"><span data-stu-id="a813d-111">When a *\*.cshtml* file with an `@page` directive is compiled, the generated class is given a [RouteAttribute](/dotnet/api/microsoft.aspnetcore.mvc.routeattribute) specifying the route template.</span></span> <span data-ttu-id="a813d-112">ルーターが持つクラスでコンポーネントが、実行時に、`RouteAttribute`どのコンポーネントが要求された URL に一致するルート テンプレートを表示します。</span><span class="sxs-lookup"><span data-stu-id="a813d-112">At runtime, the router looks for component classes with a `RouteAttribute` and renders whichever component has a route template that matches the requested URL.</span></span>

<span data-ttu-id="a813d-113">コンポーネントには、複数のルート テンプレートを適用できます。</span><span class="sxs-lookup"><span data-stu-id="a813d-113">Multiple route templates can be applied to a component.</span></span> <span data-ttu-id="a813d-114">[サンプル アプリ](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-components/common/samples/)、次のコンポーネントがの要求に応答`/BlazorRoute`と`/DifferentBlazorRoute`します。</span><span class="sxs-lookup"><span data-stu-id="a813d-114">In the [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-components/common/samples/), the following component responds to requests for `/BlazorRoute` and `/DifferentBlazorRoute`.</span></span>

<span data-ttu-id="a813d-115">*Pages/BlazorRoute.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="a813d-115">*Pages/BlazorRoute.cshtml*:</span></span>

[!code-cshtml[](common/samples/3.x/BlazorSample/Pages/BlazorRoute.cshtml?start=1&end=4)]

<span data-ttu-id="a813d-116">`<Router>` では、レンダリング時に要求されたルートのフォールバック コンポーネントの設定は、解決はありません。</span><span class="sxs-lookup"><span data-stu-id="a813d-116">`<Router>` supports setting a fallback component for rendering when a requested route isn't resolved.</span></span> <span data-ttu-id="a813d-117">設定をこのオプトイン シナリオを有効にする、`FallbackComponent`フォールバック コンポーネント クラスの型のパラメーター。</span><span class="sxs-lookup"><span data-stu-id="a813d-117">Enable this opt-in scenario by setting the `FallbackComponent` parameter to the type of the fallback component class.</span></span>

<span data-ttu-id="a813d-118">次の例で定義されているコンポーネントを設定する*Pages/MyFallbackRazorComponent.cshtml*フォールバック コンポーネントとして、 `<Router>`:</span><span class="sxs-lookup"><span data-stu-id="a813d-118">The following example sets a component defined in *Pages/MyFallbackRazorComponent.cshtml* as the fallback component for a `<Router>`:</span></span>

```cshtml
<Router ... FallbackComponent="typeof(Pages.MyFallbackRazorComponent)" />
```

> [!IMPORTANT]
> <span data-ttu-id="a813d-119">ルートを正しく生成するアプリを含める必要があります、`<base>`タグにその*wwwroot/index.html*で指定したアプリ ベース パスとファイル、`href`属性 (`<base href="/" />`)。</span><span class="sxs-lookup"><span data-stu-id="a813d-119">To generate routes properly, the app must include a `<base>` tag in its *wwwroot/index.html* file with the app base path specified in the `href` attribute (`<base href="/" />`).</span></span> <span data-ttu-id="a813d-120">詳細については、次を参照してください。[ホストと展開。アプリ ベース パス](xref:host-and-deploy/razor-components/index#app-base-path)します。</span><span class="sxs-lookup"><span data-stu-id="a813d-120">For more information, see [Host and deploy: App base path](xref:host-and-deploy/razor-components/index#app-base-path).</span></span>

## <a name="route-parameters"></a><span data-ttu-id="a813d-121">ルート パラメーター</span><span class="sxs-lookup"><span data-stu-id="a813d-121">Route parameters</span></span>

<span data-ttu-id="a813d-122">ルーターでは、ルート パラメーターを使用して、対応するコンポーネントのパラメーターと同じ名前 (大文字と小文字を区別しない) を事前設定します。</span><span class="sxs-lookup"><span data-stu-id="a813d-122">The router uses route parameters to populate the corresponding component parameters with the same name (case insensitive).</span></span>

<span data-ttu-id="a813d-123">*Pages/RouteParameter.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="a813d-123">*Pages/RouteParameter.cshtml*:</span></span>

[!code-cshtml[](common/samples/3.x/BlazorSample/Pages/RouteParameter.cshtml?start=1&end=8)]

<span data-ttu-id="a813d-124">省略可能なパラメーターは、まだサポートされていませんので、2 つ`@page`ディレクティブは、上記の例に適用されます。</span><span class="sxs-lookup"><span data-stu-id="a813d-124">Optional parameters aren't supported yet, so two `@page` directives are applied in the example above.</span></span> <span data-ttu-id="a813d-125">最初のパラメーターを指定せず、コンポーネントへの移動を許可します。</span><span class="sxs-lookup"><span data-stu-id="a813d-125">The first permits navigation to the component without a parameter.</span></span> <span data-ttu-id="a813d-126">2 番目の`@page`ディレクティブは、`{text}`ルート パラメーターと値を割り当てます、`Text`プロパティ。</span><span class="sxs-lookup"><span data-stu-id="a813d-126">The second `@page` directive takes the `{text}` route parameter and assigns the value to the `Text` property.</span></span>

## <a name="route-constraints"></a><span data-ttu-id="a813d-127">ルート制約</span><span class="sxs-lookup"><span data-stu-id="a813d-127">Route constraints</span></span>

<span data-ttu-id="a813d-128">ルート制約では、コンポーネントへのルート セグメントで一致する型を強制します。</span><span class="sxs-lookup"><span data-stu-id="a813d-128">A route constraint enforces type matching on a route segment to a component.</span></span>

<span data-ttu-id="a813d-129">次の例では、ルート ユーザー コンポーネントにのみ一致する場合。</span><span class="sxs-lookup"><span data-stu-id="a813d-129">In the following example, the route to the Users component only matches if:</span></span>

* <span data-ttu-id="a813d-130">`Id`ルート セグメントでは、要求 URL に存在します。</span><span class="sxs-lookup"><span data-stu-id="a813d-130">An `Id` route segment is present on the request URL.</span></span>
* <span data-ttu-id="a813d-131">`Id`セグメントは、整数 (`int`)。</span><span class="sxs-lookup"><span data-stu-id="a813d-131">The `Id` segment is an integer (`int`).</span></span>

```cshtml
@page "/Users/{Id:int}"

<h1>The user Id is @Id!</h1>

@functions {
    [Parameter]
    private int Id { get; set; }
}
```

<span data-ttu-id="a813d-132">次の表に示すようにルート制約は、使用可能な。</span><span class="sxs-lookup"><span data-stu-id="a813d-132">The route constraints shown in the following table are available for use.</span></span> <span data-ttu-id="a813d-133">インバリアント カルチャに一致するルート制約では、詳細については、表の下には、警告を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a813d-133">For the route constraints that match with the invariant culture, see the warning below the table for more information.</span></span>

| <span data-ttu-id="a813d-134">制約</span><span class="sxs-lookup"><span data-stu-id="a813d-134">Constraint</span></span> | <span data-ttu-id="a813d-135">例</span><span class="sxs-lookup"><span data-stu-id="a813d-135">Example</span></span>           | <span data-ttu-id="a813d-136">一致の例</span><span class="sxs-lookup"><span data-stu-id="a813d-136">Example Matches</span></span>                                                                  | <span data-ttu-id="a813d-137">インバリアント</span><span class="sxs-lookup"><span data-stu-id="a813d-137">Invariant</span></span><br><span data-ttu-id="a813d-138">カルチャ</span><span class="sxs-lookup"><span data-stu-id="a813d-138">culture</span></span><br><span data-ttu-id="a813d-139">一致</span><span class="sxs-lookup"><span data-stu-id="a813d-139">matching</span></span> |
| ---------- | ----------------- | -------------------------------------------------------------------------------- | :------------------------------: |
| `bool`     | `{active:bool}`   | <span data-ttu-id="a813d-140">`true`, `FALSE`</span><span class="sxs-lookup"><span data-stu-id="a813d-140">`true`, `FALSE`</span></span>                                                                  | <span data-ttu-id="a813d-141">いいえ</span><span class="sxs-lookup"><span data-stu-id="a813d-141">No</span></span>                               |
| `datetime` | `{dob:datetime}`  | <span data-ttu-id="a813d-142">`2016-12-31`, `2016-12-31 7:32pm`</span><span class="sxs-lookup"><span data-stu-id="a813d-142">`2016-12-31`, `2016-12-31 7:32pm`</span></span>                                                | <span data-ttu-id="a813d-143">[はい]</span><span class="sxs-lookup"><span data-stu-id="a813d-143">Yes</span></span>                              |
| `decimal`  | `{price:decimal}` | <span data-ttu-id="a813d-144">`49.99`, `-1,000.01`</span><span class="sxs-lookup"><span data-stu-id="a813d-144">`49.99`, `-1,000.01`</span></span>                                                             | <span data-ttu-id="a813d-145">[はい]</span><span class="sxs-lookup"><span data-stu-id="a813d-145">Yes</span></span>                              |
| `double`   | `{weight:double}` | <span data-ttu-id="a813d-146">`1.234`, `-1,001.01e8`</span><span class="sxs-lookup"><span data-stu-id="a813d-146">`1.234`, `-1,001.01e8`</span></span>                                                           | <span data-ttu-id="a813d-147">[はい]</span><span class="sxs-lookup"><span data-stu-id="a813d-147">Yes</span></span>                              |
| `float`    | `{weight:float}`  | <span data-ttu-id="a813d-148">`1.234`, `-1,001.01e8`</span><span class="sxs-lookup"><span data-stu-id="a813d-148">`1.234`, `-1,001.01e8`</span></span>                                                           | <span data-ttu-id="a813d-149">[はい]</span><span class="sxs-lookup"><span data-stu-id="a813d-149">Yes</span></span>                              |
| `guid`     | `{id:guid}`       | <span data-ttu-id="a813d-150">`CD2C1638-1638-72D5-1638-DEADBEEF1638`, `{CD2C1638-1638-72D5-1638-DEADBEEF1638}`</span><span class="sxs-lookup"><span data-stu-id="a813d-150">`CD2C1638-1638-72D5-1638-DEADBEEF1638`, `{CD2C1638-1638-72D5-1638-DEADBEEF1638}`</span></span> | <span data-ttu-id="a813d-151">いいえ</span><span class="sxs-lookup"><span data-stu-id="a813d-151">No</span></span>                               |
| `int`      | `{id:int}`        | <span data-ttu-id="a813d-152">`123456789`, `-123456789`</span><span class="sxs-lookup"><span data-stu-id="a813d-152">`123456789`, `-123456789`</span></span>                                                        | <span data-ttu-id="a813d-153">[はい]</span><span class="sxs-lookup"><span data-stu-id="a813d-153">Yes</span></span>                              |
| `long`     | `{ticks:long}`    | <span data-ttu-id="a813d-154">`123456789`, `-123456789`</span><span class="sxs-lookup"><span data-stu-id="a813d-154">`123456789`, `-123456789`</span></span>                                                        | <span data-ttu-id="a813d-155">[はい]</span><span class="sxs-lookup"><span data-stu-id="a813d-155">Yes</span></span>                              |

> [!WARNING]
> <span data-ttu-id="a813d-156">URL の妥当性を検証し、CLR 型 (`int` や `DateTime` など) に変換されるルート制約では、常にインバリアント カルチャが使用されます。</span><span class="sxs-lookup"><span data-stu-id="a813d-156">Route constraints that verify the URL and are converted to a CLR type (such as `int` or `DateTime`) always use the invariant culture.</span></span> <span data-ttu-id="a813d-157">これらの制約では、URL がローカライズ不可であることが前提となります。</span><span class="sxs-lookup"><span data-stu-id="a813d-157">These constraints assume that the URL is non-localizable.</span></span>

## <a name="navlink-component"></a><span data-ttu-id="a813d-158">NavLink コンポーネント</span><span class="sxs-lookup"><span data-stu-id="a813d-158">NavLink component</span></span>

<span data-ttu-id="a813d-159">HTML の代わりに NavLink コンポーネントを使用して**\<を >** ナビゲーション リンクを作成するときの要素。</span><span class="sxs-lookup"><span data-stu-id="a813d-159">Use a NavLink component in place of HTML **\<a>** elements when creating navigation links.</span></span> <span data-ttu-id="a813d-160">NavLink コンポーネントと同様に動作、 **\<を >** 切り替えます点を除いて、要素、 `active` CSS クラスかどうかに基づいて、`href`現在の URL と一致します。</span><span class="sxs-lookup"><span data-stu-id="a813d-160">A NavLink component behaves like an **\<a>** element, except it toggles an `active` CSS class based on whether its `href` matches the current URL.</span></span> <span data-ttu-id="a813d-161">`active`クラスは、どのページが表示されるナビゲーション リンクの間でのアクティブなページを理解します。</span><span class="sxs-lookup"><span data-stu-id="a813d-161">The `active` class helps a user understand which page is the active page among the navigation links displayed.</span></span>

<span data-ttu-id="a813d-162">NavMenu コンポーネント、[サンプル アプリ](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-components/common/samples/)作成、[ブートス トラップ](https://getbootstrap.com/docs/)NavLink コンポーネントを使用する方法については、ナビゲーション バー。</span><span class="sxs-lookup"><span data-stu-id="a813d-162">The NavMenu component in the [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-components/common/samples/) creates a [Bootstrap](https://getbootstrap.com/docs/) nav bar that demonstrates how to use NavLink components.</span></span> <span data-ttu-id="a813d-163">次のマークアップ内の最初の 2 つの NavLinks を示しています、 *Shared/NavMenu.cshtml*ファイル。</span><span class="sxs-lookup"><span data-stu-id="a813d-163">The following markup shows the first two NavLinks in the *Shared/NavMenu.cshtml* file.</span></span>

[!code-cshtml[](common/samples/3.x/BlazorSample/Shared/NavMenu.cshtml?start=13&end=24&highlight=4-6,9-11)]

<span data-ttu-id="a813d-164">2 つ`NavLinkMatch`オプション。</span><span class="sxs-lookup"><span data-stu-id="a813d-164">There are two `NavLinkMatch` options:</span></span>

* <span data-ttu-id="a813d-165">`NavLinkMatch.All` &ndash; 全体の現在の URL と一致するときに、NavLink をアクティブながあることを指定します。</span><span class="sxs-lookup"><span data-stu-id="a813d-165">`NavLinkMatch.All` &ndash; Specifies that the NavLink should be active when it matches the entire current URL.</span></span>
* <span data-ttu-id="a813d-166">`NavLinkMatch.Prefix` &ndash; 現在の URL のプレフィックスと一致するときに、NavLink をアクティブながあることを指定します。</span><span class="sxs-lookup"><span data-stu-id="a813d-166">`NavLinkMatch.Prefix` &ndash; Specifies that the NavLink should be active when it matches any prefix of the current URL.</span></span>

<span data-ttu-id="a813d-167">前の例では、ホーム NavLink (`href=""`) すべての Url と一致して、常に受信、 `active` CSS クラス。</span><span class="sxs-lookup"><span data-stu-id="a813d-167">In the preceding example, the Home NavLink (`href=""`) matches all URLs and always receives the `active` CSS class.</span></span> <span data-ttu-id="a813d-168">2 番目の NavLink のみを受信、 `active` BlazorRoute コンポーネントにアクセスするユーザー クラス (`href="BlazorRoute"`)。</span><span class="sxs-lookup"><span data-stu-id="a813d-168">The second NavLink only receives the `active` class when the user visits the BlazorRoute component (`href="BlazorRoute"`).</span></span>
