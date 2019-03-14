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
# <a name="razor-components-class-libraries"></a>Razor のコンポーネントのクラス ライブラリ

によって[Simon Timms](https://github.com/stimms)

> [!NOTE]
> .NET Core 3.0 プレビュー 2 SDK は、Razor コンポーネントのクラス ライブラリ プロジェクト テンプレートを含まれていませんが、今後のプレビューでテンプレートを追加する予定です。 それまでの間、このトピックで説明されている Blazor コンポーネントのクラス ライブラリ テンプレートを使用できます。

コンポーネントは、プロジェクト間でのコンポーネント ライブラリで共有できます。 コンポーネントから指定できます。

* ソリューション内の別のプロジェクト。
* NuGet パッケージ。
* 参照先の .NET ライブラリです。

コンポーネントが通常の .NET 型であるのと同様、コンポーネントのライブラリは、通常の .NET アセンブリになります。

新しいコンポーネント ライブラリを作成するには、使用、`blazorlib`とテンプレート、[新しい dotnet](/dotnet/core/tools/dotnet-new)コマンド。 テンプレートがインストールされているテンプレートの一部と[Razor コンポーネント セットアップ](xref:razor-components/get-started)します。

```console
dotnet new blazorlib -o MyComponentLib1
```

既存のプロジェクトにライブラリを追加するには、使用、 [dotnet sln](/dotnet/core/tools/dotnet-sln)コマンド。

```console
dotnet sln add .\MyComponentLib1
```

コンポーネント ライブラリには、イメージ、JavaScript、およびスタイル シートなどの静的ファイルを含めることができます。 ビルド時に、静的ファイルがビルドされたアセンブリ ファイルに埋め込まれる (*.dll*)、そのリソースを追加する方法の詳細について心配することがなく、コンポーネントの消費量をことができます。 含まれるすべてのファイル、`content`ディレクトリは、埋め込みリソースとしてマークされます。 

## <a name="consume-a-library-component"></a>ライブラリのコンポーネントを使用します。

別のプロジェクトでのライブラリで定義されているコンポーネントを使用するために、 [ @addTagHelper ](/aspnet/core/mvc/views/tag-helpers/intro#add-helper-label)ディレクティブを使用する必要があります。 名前では、個々 のコンポーネントを追加する可能性があります。 たとえば、次のディレクティブが追加されます`Component1`の`MyComponentLib1`:

```cshtml
@addTagHelper MyComponentLib1.Component1, MyComponentLib1
```

ディレクティブの一般的な形式です。

```cshtml
@addTagHelper <namespaced component name>, <assembly name>
```

ただし、共通するすべてのワイルドカードを使用してアセンブリからコンポーネントを含めるは。

```cshtml
@addTagHelper *, MyComponentLib1
```

`@addTagHelper`にディレクティブを含めることが *_ViewImport.cshtml*コンポーネントを 1 つのページまたはフォルダー内のページのセットにプロジェクト全体の使用または適用します。 `@addTagHelper`インプレース ディレクティブ、コンポーネント ライブラリのコンポーネント使用できるように格納されている場合、アプリと同じアセンブリ。 

## <a name="build-pack-and-ship-to-nuget"></a>ビルド、パック、および NuGet に出荷

コンポーネント ライブラリは、標準の .NET ライブラリであるために、パッケージ化し、それらを NuGet はパッケージ化と配布の任意のライブラリを NuGet 異なりません。 使用してパッケージを実行、 [dotnet pack](/dotnet/core/tools/dotnet-pack)コマンド。

```console
dotnet pack
```

NuGet を使用するパッケージをアップロード、 [dotnet nuget 発行](/dotnet/core/tools/dotnet-nuget-push)コマンド。

```console
dotnet nuget publish
```

NuGet パッケージに含まれている、静的なリソースが含まれます。 コンシューマーは、リソースを手動でインストールする必要のないように、スクリプトやスタイル シート、ライブラリ使用者は自動的に受け取ります。
