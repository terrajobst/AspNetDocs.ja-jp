---
title: Razor のコンポーネントのレイアウト
author: guardrex
description: Blazor と剃刀コンポーネント向けのレイアウトを再利用可能なコンポーネントを作成する方法について説明します。
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 01/29/2019
uid: razor-components/layouts
ms.openlocfilehash: 23d8f441c0b3bbde7a73717f6257013831617ec0
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57039039"
---
# <a name="razor-components-layouts"></a><span data-ttu-id="8df81-103">Razor のコンポーネントのレイアウト</span><span class="sxs-lookup"><span data-stu-id="8df81-103">Razor Components layouts</span></span>

<span data-ttu-id="8df81-104">によって[Rainer Stropek](https://www.timecockpit.com)</span><span class="sxs-lookup"><span data-stu-id="8df81-104">By [Rainer Stropek](https://www.timecockpit.com)</span></span>

<span data-ttu-id="8df81-105">通常、アプリには、複数のページが含まれます。</span><span class="sxs-lookup"><span data-stu-id="8df81-105">Apps typically contain more than one page.</span></span> <span data-ttu-id="8df81-106">メニューの著作権のメッセージ、およびロゴなどのレイアウト要素は、すべてのページに存在する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8df81-106">Layout elements, such as menus, copyright messages, and logos, must be present on all pages.</span></span> <span data-ttu-id="8df81-107">効率的なソリューションではないすべてのアプリのページにこれらのレイアウト要素のコードをコピーします。</span><span class="sxs-lookup"><span data-stu-id="8df81-107">Copying the code of these layout elements into all of the pages of an app isn't an efficient solution.</span></span> <span data-ttu-id="8df81-108">このような重複では、管理するが難しいと、おそらく時間の経過と共に一貫性のないコンテンツにつながります。</span><span class="sxs-lookup"><span data-stu-id="8df81-108">Such duplication is hard to maintain and probably leads to inconsistent content over time.</span></span> <span data-ttu-id="8df81-109">*レイアウト*この問題を解決します。</span><span class="sxs-lookup"><span data-stu-id="8df81-109">*Layouts* solve this problem.</span></span>

<span data-ttu-id="8df81-110">技術的には、レイアウトには、もう 1 つのコンポーネントです。</span><span class="sxs-lookup"><span data-stu-id="8df81-110">Technically, a layout is just another component.</span></span> <span data-ttu-id="8df81-111">Razor テンプレートまたはレイアウトが定義されているC#コードし、データ バインド、依存関係の挿入、およびその他のコンポーネントの通常の機能に含めることができます。</span><span class="sxs-lookup"><span data-stu-id="8df81-111">A layout is defined in a Razor template or in C# code and can contain data binding, dependency injection, and other ordinary features of components.</span></span> <span data-ttu-id="8df81-112">その他の 2 つの側面が有効にする、*コンポーネント*に、*レイアウト*:</span><span class="sxs-lookup"><span data-stu-id="8df81-112">Two additional aspects turn a *component* into a *layout*:</span></span>

* <span data-ttu-id="8df81-113">レイアウト コンポーネントが継承する必要があります`BlazorLayoutComponent`します。</span><span class="sxs-lookup"><span data-stu-id="8df81-113">The layout component must inherit from `BlazorLayoutComponent`.</span></span> <span data-ttu-id="8df81-114">`BlazorLayoutComponent` 定義、`Body`レイアウト内にレンダリングされるコンテンツを含むプロパティ。</span><span class="sxs-lookup"><span data-stu-id="8df81-114">`BlazorLayoutComponent` defines a `Body` property that contains the content to be rendered inside the layout.</span></span>
* <span data-ttu-id="8df81-115">レイアウト コンポーネントを使用して、`Body`プロパティを本文の内容が表示されるはずの場所を指定する、Razor 構文を使用してレンダリング`@Body`します。</span><span class="sxs-lookup"><span data-stu-id="8df81-115">The layout component uses the `Body` property to specify where the body content should be rendered using the Razor syntax `@Body`.</span></span> <span data-ttu-id="8df81-116">レンダリング中に`@Body`レイアウトのコンテンツで置き換えられます。</span><span class="sxs-lookup"><span data-stu-id="8df81-116">During rendering, `@Body` is replaced by the content of the layout.</span></span>

<span data-ttu-id="8df81-117">レイアウト コンポーネントの Razor テンプレートを次のコード サンプルに示します。</span><span class="sxs-lookup"><span data-stu-id="8df81-117">The following code sample shows the Razor template of a layout component.</span></span> <span data-ttu-id="8df81-118">使用に注意してください`BlazorLayoutComponent`と`@Body`:</span><span class="sxs-lookup"><span data-stu-id="8df81-118">Note the use of `BlazorLayoutComponent` and `@Body`:</span></span>

```csharp
@inherits BlazorLayoutComponent

<header>
    <h1>ERP Master 3000</h1>
</header>

<nav>
    <a href="master-data">Master Data Management</a>
    <a href="invoicing">Invoicing</a>
    <a href="accounting">Accounting</a>
</nav>

@Body

<footer>
    &copy; by @CopyrightMessage
</footer>

@functions {
    public string CopyrightMessage { get; set; }
    ...
}
```

## <a name="use-a-layout-in-a-component"></a><span data-ttu-id="8df81-119">コンポーネントでのレイアウトを使用します。</span><span class="sxs-lookup"><span data-stu-id="8df81-119">Use a layout in a component</span></span>

<span data-ttu-id="8df81-120">Razor ディレクティブを使用して、`@layout`コンポーネントにレイアウトを適用します。</span><span class="sxs-lookup"><span data-stu-id="8df81-120">Use the Razor directive `@layout` to apply a layout to a component.</span></span> <span data-ttu-id="8df81-121">コンパイラは変換には、このディレクティブを`LayoutAttribute`、これコンポーネント クラスに適用されます。</span><span class="sxs-lookup"><span data-stu-id="8df81-121">The compiler converts this directive into a `LayoutAttribute`, which is applied to the component class.</span></span>

<span data-ttu-id="8df81-122">次のコード サンプルでは、概念を示します。</span><span class="sxs-lookup"><span data-stu-id="8df81-122">The following code sample demonstrates the concept.</span></span> <span data-ttu-id="8df81-123">このコンポーネントの内容が挿入、 *MasterLayout*の位置にある`@Body`:</span><span class="sxs-lookup"><span data-stu-id="8df81-123">The content of this component is inserted into the *MasterLayout* at the position of `@Body`:</span></span>

```csharp
@layout MasterLayout

@page "/master-data"

<h2>Master Data Management</h2>
...
```

## <a name="centralized-layout-selection"></a><span data-ttu-id="8df81-124">一元的なレイアウトの選択</span><span class="sxs-lookup"><span data-stu-id="8df81-124">Centralized layout selection</span></span>

<span data-ttu-id="8df81-125">すべてのフォルダーのアプリは、という名前のテンプレート ファイルを含めることができます必要に応じて *_ViewImports.cshtml*します。</span><span class="sxs-lookup"><span data-stu-id="8df81-125">Every folder of a an app can optionally contain a template file named *_ViewImports.cshtml*.</span></span> <span data-ttu-id="8df81-126">コンパイラには、すべての同じフォルダーに Razor テンプレートとそのすべてのサブフォルダーで再帰的にビューのインポートのファイルで指定されたディレクティブが含まれています。</span><span class="sxs-lookup"><span data-stu-id="8df81-126">The compiler includes the directives specified in the view imports file in all of the Razor templates in the same folder and recursively in all of its subfolders.</span></span> <span data-ttu-id="8df81-127">そのため、 *_ViewImports.cshtml*ファイルを含む`@layout MainLayout`でフォルダー内のコンポーネントのすべてのこと、 *MainLayout*レイアウト。</span><span class="sxs-lookup"><span data-stu-id="8df81-127">Therefore, a *_ViewImports.cshtml* file containing `@layout MainLayout` ensures that all of the components in a folder use the *MainLayout* layout.</span></span> <span data-ttu-id="8df81-128">繰り返しを追加する必要はありません`@layout`のすべてに、  *\*.cshtml*ファイル。</span><span class="sxs-lookup"><span data-stu-id="8df81-128">There's no need to repeatedly add `@layout` to all of the *\*.cshtml* files.</span></span>

<span data-ttu-id="8df81-129">既定のテンプレートを使用している、 *_ViewImports.cshtml*レイアウトの選択するためのメカニズムです。</span><span class="sxs-lookup"><span data-stu-id="8df81-129">Note that the default template uses the *_ViewImports.cshtml* mechanism for layout selection.</span></span> <span data-ttu-id="8df81-130">新しく作成されたアプリが含まれる、 *_ViewImports.cshtml*ファイル、*ページ*フォルダー。</span><span class="sxs-lookup"><span data-stu-id="8df81-130">A newly created app contains the *_ViewImports.cshtml* file in the *Pages* folder.</span></span>

## <a name="nested-layouts"></a><span data-ttu-id="8df81-131">入れ子になったレイアウト</span><span class="sxs-lookup"><span data-stu-id="8df81-131">Nested layouts</span></span>

<span data-ttu-id="8df81-132">アプリは、入れ子になったレイアウトで構成できます。</span><span class="sxs-lookup"><span data-stu-id="8df81-132">Apps can consist of nested layouts.</span></span> <span data-ttu-id="8df81-133">コンポーネントは、さらに別のレイアウトを参照するレイアウトを参照できます。</span><span class="sxs-lookup"><span data-stu-id="8df81-133">A component can reference a layout which in turn references another layout.</span></span> <span data-ttu-id="8df81-134">たとえば、入れ子のレイアウトは、複数レベルのメニュー構造を反映するために使用できます。</span><span class="sxs-lookup"><span data-stu-id="8df81-134">For example, nesting layouts can be used to reflect a multi-level menu structure.</span></span>

<span data-ttu-id="8df81-135">次のコード サンプルでは、入れ子になったレイアウトを使用する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="8df81-135">The following code samples show how to use nested layouts.</span></span> <span data-ttu-id="8df81-136">*CustomersComponent.cshtml*ファイルは、コンポーネントを表示します。</span><span class="sxs-lookup"><span data-stu-id="8df81-136">The *CustomersComponent.cshtml* file is the component to display.</span></span> <span data-ttu-id="8df81-137">コンポーネントがレイアウトを参照することに注意してください`MasterDataLayout`します。</span><span class="sxs-lookup"><span data-stu-id="8df81-137">Note that the component references the layout `MasterDataLayout`.</span></span>

<span data-ttu-id="8df81-138">*CustomersComponent.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="8df81-138">*CustomersComponent.cshtml*:</span></span>

```csharp
@layout MasterDataLayout

@page "/master-data/customers"

<h1>Customer Maintenance</h1>
...
```

<span data-ttu-id="8df81-139">*MasterDataLayout.cshtml*ファイルは、提供、`MasterDataLayout`します。</span><span class="sxs-lookup"><span data-stu-id="8df81-139">The *MasterDataLayout.cshtml* file provides the `MasterDataLayout`.</span></span> <span data-ttu-id="8df81-140">レイアウトは、別のレイアウトを参照`MainLayout`埋め込まれる進んでいます。</span><span class="sxs-lookup"><span data-stu-id="8df81-140">The layout references another layout, `MainLayout`, where it's going to be embedded.</span></span>

<span data-ttu-id="8df81-141">*MasterDataLayout.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="8df81-141">*MasterDataLayout.cshtml*:</span></span>

```csharp
@layout MainLayout
@inherits BlazorLayoutComponent

<nav>
    <!-- Menu structure of master data module -->
    ...
</nav>

@Body
```

<span data-ttu-id="8df81-142">最後に、`MainLayout`ヘッダー、フッター、およびメイン メニューなど、最上位のレイアウト要素が含まれています。</span><span class="sxs-lookup"><span data-stu-id="8df81-142">Finally, `MainLayout` contains the top-level layout elements, such as the header, footer, and main menu.</span></span>

<span data-ttu-id="8df81-143">*MainLayout.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="8df81-143">*MainLayout.cshtml*:</span></span>

```csharp
@inherits BlazorLayoutComponent

<header>...</header>
<nav>...</nav>

@Body
```
