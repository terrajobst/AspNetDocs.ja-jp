---
title: Razor のコンポーネントのクラス ライブラリ
author: guardrex
description: コンポーネントを含める、外部コンポーネント ライブラリの Razor コンポーネント アプリにする方法を説明します。
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 02/09/2019
uid: razor-components/class-libraries
ms.openlocfilehash: 0e644627178bae2b8880760335860b3e0ebef156
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57037409"
---
# <a name="razor-components-class-libraries"></a><span data-ttu-id="8cb76-103">Razor のコンポーネントのクラス ライブラリ</span><span class="sxs-lookup"><span data-stu-id="8cb76-103">Razor Components Class Libraries</span></span>

<span data-ttu-id="8cb76-104">によって[Simon Timms](https://github.com/stimms)</span><span class="sxs-lookup"><span data-stu-id="8cb76-104">By [Simon Timms](https://github.com/stimms)</span></span>

> [!NOTE]
> <span data-ttu-id="8cb76-105">.NET Core 3.0 プレビュー 2 SDK は、Razor コンポーネントのクラス ライブラリ プロジェクト テンプレートを含まれていませんが、今後のプレビューでテンプレートを追加する予定です。</span><span class="sxs-lookup"><span data-stu-id="8cb76-105">The .NET Core 3.0 Preview 2 SDK doesn't include a project template for Razor Component Class Libraries, but we expect to add a template in a future preview.</span></span> <span data-ttu-id="8cb76-106">それまでの間、このトピックで説明されている Blazor コンポーネントのクラス ライブラリ テンプレートを使用できます。</span><span class="sxs-lookup"><span data-stu-id="8cb76-106">In meantime, you can use the Blazor Component Class Library template explained in this topic.</span></span>

<span data-ttu-id="8cb76-107">コンポーネントは、プロジェクト間でのコンポーネント ライブラリで共有できます。</span><span class="sxs-lookup"><span data-stu-id="8cb76-107">Components can be shared in component libraries across projects.</span></span> <span data-ttu-id="8cb76-108">コンポーネントから指定できます。</span><span class="sxs-lookup"><span data-stu-id="8cb76-108">Components can be included from:</span></span>

* <span data-ttu-id="8cb76-109">ソリューション内の別のプロジェクト。</span><span class="sxs-lookup"><span data-stu-id="8cb76-109">Another project in the solution.</span></span>
* <span data-ttu-id="8cb76-110">NuGet パッケージ。</span><span class="sxs-lookup"><span data-stu-id="8cb76-110">A NuGet package.</span></span>
* <span data-ttu-id="8cb76-111">参照先の .NET ライブラリです。</span><span class="sxs-lookup"><span data-stu-id="8cb76-111">A referenced .NET library.</span></span>

<span data-ttu-id="8cb76-112">コンポーネントが通常の .NET 型であるのと同様、コンポーネントのライブラリは、通常の .NET アセンブリになります。</span><span class="sxs-lookup"><span data-stu-id="8cb76-112">Just as components are regular .NET types, component libraries are normal .NET assemblies.</span></span>

<span data-ttu-id="8cb76-113">新しいコンポーネント ライブラリを作成するには、使用、`blazorlib`とテンプレート、[新しい dotnet](/dotnet/core/tools/dotnet-new)コマンド。</span><span class="sxs-lookup"><span data-stu-id="8cb76-113">To create a new component library, use the `blazorlib` template with the [dotnet new](/dotnet/core/tools/dotnet-new) command.</span></span> <span data-ttu-id="8cb76-114">テンプレートがインストールされているテンプレートの一部と[Razor コンポーネント セットアップ](xref:razor-components/get-started)します。</span><span class="sxs-lookup"><span data-stu-id="8cb76-114">The template is part of the templates installed when [setting up Razor Components](xref:razor-components/get-started).</span></span>

```console
dotnet new blazorlib -o MyComponentLib1
```

<span data-ttu-id="8cb76-115">既存のプロジェクトにライブラリを追加するには、使用、 [dotnet sln](/dotnet/core/tools/dotnet-sln)コマンド。</span><span class="sxs-lookup"><span data-stu-id="8cb76-115">To add the library to an existing project, use the [dotnet sln](/dotnet/core/tools/dotnet-sln) command:</span></span>

```console
dotnet sln add .\MyComponentLib1
```

<span data-ttu-id="8cb76-116">コンポーネント ライブラリには、イメージ、JavaScript、およびスタイル シートなどの静的ファイルを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="8cb76-116">Component libraries may contain static files, such as images, JavaScript, and stylesheets.</span></span> <span data-ttu-id="8cb76-117">ビルド時に、静的ファイルがビルドされたアセンブリ ファイルに埋め込まれる (*.dll*)、そのリソースを追加する方法の詳細について心配することがなく、コンポーネントの消費量をことができます。</span><span class="sxs-lookup"><span data-stu-id="8cb76-117">At build time, static files are embedded into the built assembly file (*.dll*), which allows consumption of the components without having to worry about how to include their resources.</span></span> <span data-ttu-id="8cb76-118">含まれるすべてのファイル、`content`ディレクトリは、埋め込みリソースとしてマークされます。</span><span class="sxs-lookup"><span data-stu-id="8cb76-118">Any files included in the `content` directory are marked as an embedded resource.</span></span> 

## <a name="consume-a-library-component"></a><span data-ttu-id="8cb76-119">ライブラリのコンポーネントを使用します。</span><span class="sxs-lookup"><span data-stu-id="8cb76-119">Consume a library component</span></span>

<span data-ttu-id="8cb76-120">別のプロジェクトでのライブラリで定義されているコンポーネントを使用するために、 [ @addTagHelper ](/aspnet/core/mvc/views/tag-helpers/intro#add-helper-label)ディレクティブを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8cb76-120">In order to consume components defined in a library in another project, the [@addTagHelper](/aspnet/core/mvc/views/tag-helpers/intro#add-helper-label) directive must be used.</span></span> <span data-ttu-id="8cb76-121">名前では、個々 のコンポーネントを追加する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="8cb76-121">Individual components may be added by name.</span></span> <span data-ttu-id="8cb76-122">たとえば、次のディレクティブが追加されます`Component1`の`MyComponentLib1`:</span><span class="sxs-lookup"><span data-stu-id="8cb76-122">For example, the following directive adds `Component1` of `MyComponentLib1`:</span></span>

```cshtml
@addTagHelper MyComponentLib1.Component1, MyComponentLib1
```

<span data-ttu-id="8cb76-123">ディレクティブの一般的な形式です。</span><span class="sxs-lookup"><span data-stu-id="8cb76-123">The general format of the directive is:</span></span>

```cshtml
@addTagHelper <namespaced component name>, <assembly name>
```

<span data-ttu-id="8cb76-124">ただし、共通するすべてのワイルドカードを使用してアセンブリからコンポーネントを含めるは。</span><span class="sxs-lookup"><span data-stu-id="8cb76-124">However, it's common to include all of the components from an assembly using a wildcard:</span></span>

```cshtml
@addTagHelper *, MyComponentLib1
```

<span data-ttu-id="8cb76-125">`@addTagHelper`にディレクティブを含めることが *_ViewImport.cshtml*コンポーネントを 1 つのページまたはフォルダー内のページのセットにプロジェクト全体の使用または適用します。</span><span class="sxs-lookup"><span data-stu-id="8cb76-125">The `@addTagHelper` directive can be included in *_ViewImport.cshtml* to make the components available for an entire project or applied to a single page or set of pages within a folder.</span></span> <span data-ttu-id="8cb76-126">`@addTagHelper`インプレース ディレクティブ、コンポーネント ライブラリのコンポーネント使用できるように格納されている場合、アプリと同じアセンブリ。</span><span class="sxs-lookup"><span data-stu-id="8cb76-126">With the `@addTagHelper` directive in place, the components of the component library can be consumed as if they were in the same assembly as the app.</span></span> 

## <a name="build-pack-and-ship-to-nuget"></a><span data-ttu-id="8cb76-127">ビルド、パック、および NuGet に出荷</span><span class="sxs-lookup"><span data-stu-id="8cb76-127">Build, pack, and ship to NuGet</span></span>

<span data-ttu-id="8cb76-128">コンポーネント ライブラリは、標準の .NET ライブラリであるために、パッケージ化し、それらを NuGet はパッケージ化と配布の任意のライブラリを NuGet 異なりません。</span><span class="sxs-lookup"><span data-stu-id="8cb76-128">Because component libraries are standard .NET libraries, packaging and shipping them to NuGet is no different from packaging and shipping any library to NuGet.</span></span> <span data-ttu-id="8cb76-129">使用してパッケージを実行、 [dotnet pack](/dotnet/core/tools/dotnet-pack)コマンド。</span><span class="sxs-lookup"><span data-stu-id="8cb76-129">Packaging is performed using the [dotnet pack](/dotnet/core/tools/dotnet-pack) command:</span></span>

```console
dotnet pack
```

<span data-ttu-id="8cb76-130">NuGet を使用するパッケージをアップロード、 [dotnet nuget 発行](/dotnet/core/tools/dotnet-nuget-push)コマンド。</span><span class="sxs-lookup"><span data-stu-id="8cb76-130">Upload the package to NuGet using the [dotnet nuget publish](/dotnet/core/tools/dotnet-nuget-push) command:</span></span>

```console
dotnet nuget publish
```

<span data-ttu-id="8cb76-131">NuGet パッケージに含まれている、静的なリソースが含まれます。</span><span class="sxs-lookup"><span data-stu-id="8cb76-131">Any included static resources are included in the NuGet package.</span></span> <span data-ttu-id="8cb76-132">コンシューマーは、リソースを手動でインストールする必要のないように、スクリプトやスタイル シート、ライブラリ使用者は自動的に受け取ります。</span><span class="sxs-lookup"><span data-stu-id="8cb76-132">Library consumers automatically receive scripts and stylesheets, so consumers aren't required to manually install the resources.</span></span>
