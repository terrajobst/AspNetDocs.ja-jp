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
# <a name="razor-components-routing"></a>ルーティング razor コンポーネント

作成者: [Luke Latham](https://github.com/guardrex)

アプリや NavLink コンポーネントの詳細については、要求をルーティングする方法について説明します。

[サンプル コードを表示またはダウンロード](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-components/common/samples/)します ([ダウンロード方法](xref:index#how-to-download-a-sample))。 前提条件については、[作業開始](xref:razor-components/get-started)に関するトピックをご覧ください。

## <a name="route-templates"></a>ルート テンプレート

`<Router>`ルーティング、コンポーネントを使用して、ルート テンプレートは、アクセス可能な各コンポーネントに提供されます。 `<Router>`コンポーネントに表示されます、 *App.cshtml*ファイル。

```cshtml
<Router AppAssembly=typeof(Program).Assembly />
```

ときに、  *\*.cshtml*ファイルと、`@page`ディレクティブをコンパイルすると、生成されたクラスが指定された、 [RouteAttribute](/dotnet/api/microsoft.aspnetcore.mvc.routeattribute)ルート テンプレートを指定します。 ルーターが持つクラスでコンポーネントが、実行時に、`RouteAttribute`どのコンポーネントが要求された URL に一致するルート テンプレートを表示します。

コンポーネントには、複数のルート テンプレートを適用できます。 [サンプル アプリ](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-components/common/samples/)、次のコンポーネントがの要求に応答`/BlazorRoute`と`/DifferentBlazorRoute`します。

*Pages/BlazorRoute.cshtml*:

[!code-cshtml[](common/samples/3.x/BlazorSample/Pages/BlazorRoute.cshtml?start=1&end=4)]

`<Router>` では、レンダリング時に要求されたルートのフォールバック コンポーネントの設定は、解決はありません。 設定をこのオプトイン シナリオを有効にする、`FallbackComponent`フォールバック コンポーネント クラスの型のパラメーター。

次の例で定義されているコンポーネントを設定する*Pages/MyFallbackRazorComponent.cshtml*フォールバック コンポーネントとして、 `<Router>`:

```cshtml
<Router ... FallbackComponent="typeof(Pages.MyFallbackRazorComponent)" />
```

> [!IMPORTANT]
> ルートを正しく生成するアプリを含める必要があります、`<base>`タグにその*wwwroot/index.html*で指定したアプリ ベース パスとファイル、`href`属性 (`<base href="/" />`)。 詳細については、次を参照してください。[ホストと展開。アプリ ベース パス](xref:host-and-deploy/razor-components/index#app-base-path)します。

## <a name="route-parameters"></a>ルート パラメーター

ルーターでは、ルート パラメーターを使用して、対応するコンポーネントのパラメーターと同じ名前 (大文字と小文字を区別しない) を事前設定します。

*Pages/RouteParameter.cshtml*:

[!code-cshtml[](common/samples/3.x/BlazorSample/Pages/RouteParameter.cshtml?start=1&end=8)]

省略可能なパラメーターは、まだサポートされていませんので、2 つ`@page`ディレクティブは、上記の例に適用されます。 最初のパラメーターを指定せず、コンポーネントへの移動を許可します。 2 番目の`@page`ディレクティブは、`{text}`ルート パラメーターと値を割り当てます、`Text`プロパティ。

## <a name="route-constraints"></a>ルート制約

ルート制約では、コンポーネントへのルート セグメントで一致する型を強制します。

次の例では、ルート ユーザー コンポーネントにのみ一致する場合。

* `Id`ルート セグメントでは、要求 URL に存在します。
* `Id`セグメントは、整数 (`int`)。

```cshtml
@page "/Users/{Id:int}"

<h1>The user Id is @Id!</h1>

@functions {
    [Parameter]
    private int Id { get; set; }
}
```

次の表に示すようにルート制約は、使用可能な。 インバリアント カルチャに一致するルート制約では、詳細については、表の下には、警告を参照してください。

| 制約 | 例           | 一致の例                                                                  | インバリアント<br>カルチャ<br>一致 |
| ---------- | ----------------- | -------------------------------------------------------------------------------- | :------------------------------: |
| `bool`     | `{active:bool}`   | `true`, `FALSE`                                                                  | いいえ                               |
| `datetime` | `{dob:datetime}`  | `2016-12-31`, `2016-12-31 7:32pm`                                                | [はい]                              |
| `decimal`  | `{price:decimal}` | `49.99`, `-1,000.01`                                                             | [はい]                              |
| `double`   | `{weight:double}` | `1.234`, `-1,001.01e8`                                                           | [はい]                              |
| `float`    | `{weight:float}`  | `1.234`, `-1,001.01e8`                                                           | [はい]                              |
| `guid`     | `{id:guid}`       | `CD2C1638-1638-72D5-1638-DEADBEEF1638`, `{CD2C1638-1638-72D5-1638-DEADBEEF1638}` | いいえ                               |
| `int`      | `{id:int}`        | `123456789`, `-123456789`                                                        | [はい]                              |
| `long`     | `{ticks:long}`    | `123456789`, `-123456789`                                                        | [はい]                              |

> [!WARNING]
> URL の妥当性を検証し、CLR 型 (`int` や `DateTime` など) に変換されるルート制約では、常にインバリアント カルチャが使用されます。 これらの制約では、URL がローカライズ不可であることが前提となります。

## <a name="navlink-component"></a>NavLink コンポーネント

HTML の代わりに NavLink コンポーネントを使用して**\<を >** ナビゲーション リンクを作成するときの要素。 NavLink コンポーネントと同様に動作、 **\<を >** 切り替えます点を除いて、要素、 `active` CSS クラスかどうかに基づいて、`href`現在の URL と一致します。 `active`クラスは、どのページが表示されるナビゲーション リンクの間でのアクティブなページを理解します。

NavMenu コンポーネント、[サンプル アプリ](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-components/common/samples/)作成、[ブートス トラップ](https://getbootstrap.com/docs/)NavLink コンポーネントを使用する方法については、ナビゲーション バー。 次のマークアップ内の最初の 2 つの NavLinks を示しています、 *Shared/NavMenu.cshtml*ファイル。

[!code-cshtml[](common/samples/3.x/BlazorSample/Shared/NavMenu.cshtml?start=13&end=24&highlight=4-6,9-11)]

2 つ`NavLinkMatch`オプション。

* `NavLinkMatch.All` &ndash; 全体の現在の URL と一致するときに、NavLink をアクティブながあることを指定します。
* `NavLinkMatch.Prefix` &ndash; 現在の URL のプレフィックスと一致するときに、NavLink をアクティブながあることを指定します。

前の例では、ホーム NavLink (`href=""`) すべての Url と一致して、常に受信、 `active` CSS クラス。 2 番目の NavLink のみを受信、 `active` BlazorRoute コンポーネントにアクセスするユーザー クラス (`href="BlazorRoute"`)。
