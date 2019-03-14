---
title: Razor のコンポーネントを概要します。
author: guardrex
description: 作成と Razor コンポーネント プロジェクトを変更して Razor コンポーネントを開始する方法について説明します。
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 02/03/2019
uid: razor-components/get-started
ms.openlocfilehash: a9ada603e5ed4e0e75c4aebc5105c331118666e6
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57036389"
---
# <a name="get-started-with-razor-components"></a>Razor のコンポーネントを概要します。

作成者: [Daniel Roth](https://github.com/danroth27)、[Luke Latham](https://github.com/guardrex)

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

必要条件:

[!INCLUDE[](~/includes/net-core-prereqs-vs-3.0.md)]

Visual Studio で、最初の Razor コンポーネント プロジェクトを作成するには

1. 選択**ファイル** > **新しいプロジェクト** > **Web** > **ASP.NET Core Web アプリケーション**します。
1. 確認します **.NET Core**と**ASP.NET Core 3.0**上部にある選択されます。
1. 選択、 **Razor コンポーネント**テンプレートと選択**OK**します。

   ![新しいアプリのダイアログ](https://msdnshared.blob.core.windows.net/media/2019/01/razor-components-template.png)

1. **F5 キー**を押してアプリを実行します。

おめでとうございます! 最初の Razor コンポーネント アプリを実行しました。

<!--

# [Visual Studio Code](#tab/visual-studio-code)

Prerequisites:

[!INCLUDE[](~/includes/net-core-prereqs-vsc-3.0.md)]

To create your first Razor Components project in Visual Studio Code:

1. Execute the following command from a command shell:

   ```console
   dotnet new razorcomponents -o WebApplication1
   ```

1. Open the *WebApplication1* folder in Visual Studio Code.

1. Add a *.vscode* folder.

1. Add a *tasks.json* file to the *.vscode* folder with the following content:

   [!code-json[](get-started/samples_snapshot/3.x/tasks.json)]

1. Add a *launch.json* file to the *.vscode* folder with the following content:

   [!code-json[](get-started/samples_snapshot/3.x/launch.json)]

1. Execute the app using the Visual Studio Code debugger.

1. In a browser, navigate to `https://localhost:5001`.

Congratulations! You just ran your first Razor Components app!

# [Visual Studio for Mac](#tab/visual-studio-mac)

.NET Core 3.0 will be supported with Visual Studio for Mac version 8.0 or later. Visual Studio for Mac version 8.0 Preview isn't available at this time.

Use the [.NET Core CLI version of this topic](xref:razor-components/get-started?tabs=netcore-cli) on macOS.


[!INCLUDE[](~/includes/net-core-prereqs-mac-3.0.md)]

To create your first project Razor Components project in Visual Studio for Mac:

1. Select **File** > **New Solution** or **New Project**.
1. In the sidebar, select **.NET Core** > **App**.
1. Select **ASP.NET Core Razor Components** and select **Next**.
1. The **Target Framework** defaults to **.NET Core 3.0**. Select **Next**.
1. In the **Project Name** field, enter `WebApplication1`. Select **Create**.
1. Select **Run** > **Run Without Debugging** to run the app *without the debugger*. Running with the debugger isn't supported at this time.

Congratulations! You just ran your first Razor Components app!
-->

# <a name="net-core-clitabnetcore-cli"></a>[.NET Core CLI](#tab/netcore-cli/)

必要条件:

* [.NET core SDK 3.0 プレビュー](https://dotnet.microsoft.com/download/dotnet-core/3.0)

1. コマンド シェルから、最初の Razor コンポーネント プロジェクトを作成するには

   ```console
   dotnet new razorcomponents -o WebApplication1
   cd WebApplication1
   dotnet run
   ```

1. ブラウザーで、`https://localhost:5001` に移動します。

おめでとうございます! 最初の Razor コンポーネント アプリを実行しました。

---

## <a name="razor-components-project"></a>Razor のコンポーネントのプロジェクト

コンポーネントの Razor テンプレートによって作成されたソリューションには、2 つのプロジェクトが含まれています。

* *WebApplication1.Server* &ndash;サーバー プロジェクトは、ASP.NET Core プロジェクトは、Razor コンポーネント アプリケーションをホストするように設定します。
* *WebApplication1.App* &ndash; Razor コンポーネントを使用するクライアント側の web UI プロジェクト。

UI ロジック、 *WebApplication1.App*プロジェクトは ASP.NET Core 3.0 プレビュー 2 の技術的な制限により、アプリの残りの部分から分離します。 Razor ファイルの拡張子 (*.cshtml*) 使用の Razor コンポーネントは、Razor ページと MVC のビューにも使用します。 現時点では、Razor のコンポーネントと Razor ページ/MVC は、さまざまなコンパイル モデルをあるので、Razor のコンポーネントの Razor ファイルが個別に保存されます。 Razor のコンポーネントの新しいファイル拡張子を導入する予定の今後のプレビュー (*.razor*)。 コンポーネント、ページ、およびビューをホストする*同じプロジェクトで*します。

アプリを実行すると、複数のページは、サイドバー内のタブから利用できます。

* Home
* カウンター
* データをフェッチします。

Counter ページ上で **[クリックしてください]** ボタンを選択し、ページを更新することなくカウンターをインクリメントします。 Web ページでカウンターをインクリメントする場合、通常は JavaScript を記述することが必要ですが、Razor Components には C# を使ったより優れた方法が用意されています。

*WebApplication1.App/Pages/Counter.cshtml*:

[!code-cshtml[](get-started/samples_snapshot/3.x/Counter1.cshtml)]

要求を`/counter`で指定したとおり、ブラウザーで、`@page`上部にあるディレクティブがそのコンテンツを表示するために、カウンターのコンポーネント。 コンポーネントは、柔軟で効率的な方法で UI を更新するために使用するレンダリング ツリーのメモリ内表現にレンダリングします。

毎回、 **Click me**ボタンが選択されています。

* `onclick`イベントが発生します。
* `IncrementCount` メソッドが呼び出された場合。
* `currentCount`がインクリメントされます。
* コンポーネントは、もう一度表示されます。

ランタイムは、前のコンテンツを新しいコンテンツを比較し、ドキュメント オブジェクト モデル (DOM) に変更されたコンテンツにのみ適用されます。

HTML のような構文を使用して別のコンポーネントにコンポーネントを追加します。 コンポーネントのパラメーターは、属性または子コンテンツを使用して指定されます。 追加することでカウンター コンポーネントをアプリのホーム ページに追加するなど、`<Counter />`インデックス コンポーネント要素。

*WebApplication1.App/Pages/Index.cshtml*:

[!code-cshtml[](get-started/samples_snapshot/3.x/Index1.cshtml?highlight=7)]

アプリを実行します。 ホームページには、独自のカウンターを指定します。

カウンターのコンポーネントにパラメーターを追加する更新コンポーネントの`@functions`ブロック。

* プロパティを追加`IncrementAmount`で修飾された、`[Parameter]`属性。
* `currentCount` の値を増やすときに `IncrementAmount` を使うように `IncrementCount` メソッドを変更します。

*WebApplication1.App/Pages/Counter.cshtml*:

[!code-cshtml[](get-started/samples_snapshot/3.x/Counter2.cshtml?highlight=4,8)]

属性を使って、Home コンポーネントの `<Counter>` 要素に `IncrementAmount` パラメーターを指定します。

*WebApplication1.App/Pages/Index.cshtml*:

[!code-cshtml[](get-started/samples_snapshot/3.x/Index2.cshtml)]

アプリを実行します。 ホームページには、10 たびにインクリメントする独自のカウンター、 **Click me**ボタンが選択されています。

## <a name="next-steps"></a>次の手順

<xref:tutorials/first-razor-components-app>
