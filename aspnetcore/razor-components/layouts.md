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
# <a name="razor-components-layouts"></a>Razor のコンポーネントのレイアウト

によって[Rainer Stropek](https://www.timecockpit.com)

通常、アプリには、複数のページが含まれます。 メニューの著作権のメッセージ、およびロゴなどのレイアウト要素は、すべてのページに存在する必要があります。 効率的なソリューションではないすべてのアプリのページにこれらのレイアウト要素のコードをコピーします。 このような重複では、管理するが難しいと、おそらく時間の経過と共に一貫性のないコンテンツにつながります。 *レイアウト*この問題を解決します。

技術的には、レイアウトには、もう 1 つのコンポーネントです。 Razor テンプレートまたはレイアウトが定義されているC#コードし、データ バインド、依存関係の挿入、およびその他のコンポーネントの通常の機能に含めることができます。 その他の 2 つの側面が有効にする、*コンポーネント*に、*レイアウト*:

* レイアウト コンポーネントが継承する必要があります`BlazorLayoutComponent`します。 `BlazorLayoutComponent` 定義、`Body`レイアウト内にレンダリングされるコンテンツを含むプロパティ。
* レイアウト コンポーネントを使用して、`Body`プロパティを本文の内容が表示されるはずの場所を指定する、Razor 構文を使用してレンダリング`@Body`します。 レンダリング中に`@Body`レイアウトのコンテンツで置き換えられます。

レイアウト コンポーネントの Razor テンプレートを次のコード サンプルに示します。 使用に注意してください`BlazorLayoutComponent`と`@Body`:

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

## <a name="use-a-layout-in-a-component"></a>コンポーネントでのレイアウトを使用します。

Razor ディレクティブを使用して、`@layout`コンポーネントにレイアウトを適用します。 コンパイラは変換には、このディレクティブを`LayoutAttribute`、これコンポーネント クラスに適用されます。

次のコード サンプルでは、概念を示します。 このコンポーネントの内容が挿入、 *MasterLayout*の位置にある`@Body`:

```csharp
@layout MasterLayout

@page "/master-data"

<h2>Master Data Management</h2>
...
```

## <a name="centralized-layout-selection"></a>一元的なレイアウトの選択

すべてのフォルダーのアプリは、という名前のテンプレート ファイルを含めることができます必要に応じて *_ViewImports.cshtml*します。 コンパイラには、すべての同じフォルダーに Razor テンプレートとそのすべてのサブフォルダーで再帰的にビューのインポートのファイルで指定されたディレクティブが含まれています。 そのため、 *_ViewImports.cshtml*ファイルを含む`@layout MainLayout`でフォルダー内のコンポーネントのすべてのこと、 *MainLayout*レイアウト。 繰り返しを追加する必要はありません`@layout`のすべてに、  *\*.cshtml*ファイル。

既定のテンプレートを使用している、 *_ViewImports.cshtml*レイアウトの選択するためのメカニズムです。 新しく作成されたアプリが含まれる、 *_ViewImports.cshtml*ファイル、*ページ*フォルダー。

## <a name="nested-layouts"></a>入れ子になったレイアウト

アプリは、入れ子になったレイアウトで構成できます。 コンポーネントは、さらに別のレイアウトを参照するレイアウトを参照できます。 たとえば、入れ子のレイアウトは、複数レベルのメニュー構造を反映するために使用できます。

次のコード サンプルでは、入れ子になったレイアウトを使用する方法を示します。 *CustomersComponent.cshtml*ファイルは、コンポーネントを表示します。 コンポーネントがレイアウトを参照することに注意してください`MasterDataLayout`します。

*CustomersComponent.cshtml*:

```csharp
@layout MasterDataLayout

@page "/master-data/customers"

<h1>Customer Maintenance</h1>
...
```

*MasterDataLayout.cshtml*ファイルは、提供、`MasterDataLayout`します。 レイアウトは、別のレイアウトを参照`MainLayout`埋め込まれる進んでいます。

*MasterDataLayout.cshtml*:

```csharp
@layout MainLayout
@inherits BlazorLayoutComponent

<nav>
    <!-- Menu structure of master data module -->
    ...
</nav>

@Body
```

最後に、`MainLayout`ヘッダー、フッター、およびメイン メニューなど、最上位のレイアウト要素が含まれています。

*MainLayout.cshtml*:

```csharp
@inherits BlazorLayoutComponent

<header>...</header>
<nav>...</nav>

@Body
```
