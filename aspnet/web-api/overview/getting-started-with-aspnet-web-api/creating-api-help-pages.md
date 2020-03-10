---
uid: web-api/overview/getting-started-with-aspnet-web-api/creating-api-help-pages
title: ASP.NET Web API のヘルプページを作成する-ASP.NET 4.x
author: MikeWasson
description: このチュートリアルでは、ASP.NET 4.x で ASP.NET Web API 用のヘルプページを作成する方法を示します。
ms.author: riande
ms.date: 04/01/2013
ms.custom: seoapril2019
ms.assetid: 0150e67b-c50d-4613-83ea-7b4ef8cacc5a
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/creating-api-help-pages
msc.type: authoredcontent
ms.openlocfilehash: 8308dab8bd66aa8f5a3c5fb4133fc7a3df78f671
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448618"
---
# <a name="creating-help-pages-for-aspnet-web-api"></a>ASP.NET Web API のヘルプページの作成

[Mike Wasson](https://github.com/MikeWasson)

このチュートリアルでは、ASP.NET 4.x で ASP.NET Web API 用のヘルプページを作成する方法を示します。

Web API を作成するときは、多くの場合、他の開発者が API の呼び出し方法を理解できるように、ヘルプページを作成すると便利です。 すべてのドキュメントを手動で作成することもできますが、可能な限り自動生成することをお勧めします。 このタスクを簡単にするために、ASP.NET Web API では、実行時に自動生成ヘルプページ用のライブラリが用意されています。

![](creating-api-help-pages/_static/image1.png)

## <a name="creating-api-help-pages"></a>API ヘルプページの作成

[ASP.NET and Web Tools 2012.2 更新プログラム](https://go.microsoft.com/fwlink/?LinkId=282650)をインストールします。 この更新プログラムは、ヘルプページを Web API プロジェクトテンプレートに統合します。

次に、新しい ASP.NET MVC 4 プロジェクトを作成し、[Web API プロジェクト] テンプレートを選択します。 プロジェクトテンプレートは、`ValuesController`という名前の API コントローラーの例を作成します。 このテンプレートは、API のヘルプページも作成します。 ヘルプページのすべてのコードファイルは、プロジェクトの [区分] フォルダーに配置されます。

![](creating-api-help-pages/_static/image2.png)

アプリケーションを実行すると、ホームページに API ヘルプページへのリンクが表示されます。 ホームページから、相対パスは/helpになります。

![](creating-api-help-pages/_static/image3.png)

このリンクを使用すると、API の概要ページが表示されます。

![](creating-api-help-pages/_static/image4.png)

このページの MVC ビューは、Areas/HelpPage/Views/Help/Index. cshtml で定義されています。 このページを編集して、レイアウト、概要、タイトル、スタイルなどを変更できます。

ページの主要な部分は、コントローラー別にグループ化された Api のテーブルです。 テーブルエントリは、 **Iapiexplorer**インターフェイスを使用して動的に生成されます。 (このインターフェイスについては後で詳しく説明します)。新しい API コントローラーを追加すると、テーブルは実行時に自動的に更新されます。

[API] 列には、HTTP メソッドと相対 URI が一覧表示されます。 [説明] 列には、各 API のドキュメントが含まれています。 最初に、ドキュメントはプレースホルダーテキストにすぎません。 次のセクションでは、XML コメントからドキュメントを追加する方法について説明します。

各 API には、要求や応答の本文など、詳細な情報が記載されたページへのリンクがあります。

![](creating-api-help-pages/_static/image5.png)

## <a name="adding-help-pages-to-an-existing-project"></a>既存のプロジェクトへのヘルプページの追加

NuGet パッケージマネージャーを使用して、既存の Web API プロジェクトにヘルプページを追加できます。 このオプションは、"Web API" テンプレートとは別のプロジェクトテンプレートから開始する場合に便利です。

**[ツール]** メニューの **[NuGet パッケージマネージャー]** を選択し、 **[パッケージマネージャーコンソール]** を選択します。 [[パッケージマネージャーコンソール](http://docs.nuget.org/docs/start-here/using-the-package-manager-console)] ウィンドウで、次のいずれかのコマンドを入力します。

**C#** アプリケーションの場合: `Install-Package Microsoft.AspNet.WebApi.HelpPage`

**Visual Basic**アプリケーションの場合: `Install-Package Microsoft.AspNet.WebApi.HelpPage.VB`

パッケージは2つあります。 C# 1 つは Visual Basic 用、もう1つは1つです。 プロジェクトに一致するものを使用してください。

このコマンドは、必要なアセンブリをインストールし、ヘルプページの MVC ビューを追加します (区分/ヘルプページフォルダーにあります)。 ヘルプページへのリンクを手動で追加する必要があります。 URI は/helpです。 Razor ビューでリンクを作成するには、次のように追加します。

[!code-cshtml[Main](creating-api-help-pages/samples/sample1.cshtml)]

また、領域を登録してください。 Global.asax ファイルで、次のコードを**アプリケーション\_Start**メソッドに追加します (まだ存在していない場合)。

[!code-csharp[Main](creating-api-help-pages/samples/sample2.cs?highlight=4)]

## <a name="adding-api-documentation"></a>API ドキュメントの追加

既定では、ヘルプページにドキュメントのプレースホルダー文字列があります。 [XML ドキュメントコメント](https://msdn.microsoft.com/library/b2s063f7.aspx)を使用して、ドキュメントを作成できます。 この機能を有効にするには、[ファイルエリア]、[ヘルプ] ページ、[アプリ] の順に開き、[Start/\_] を開き、次の行をコメント解除します。

[!code-csharp[Main](creating-api-help-pages/samples/sample3.cs)]

ここで XML ドキュメントを有効にします。 ソリューションエクスプローラーで、プロジェクトを右クリックし、 **[プロパティ]** を選択します。 **[ビルド]** ページを選択します。

![](creating-api-help-pages/_static/image6.png)

**[出力]** で、 **[XML ドキュメントファイル]** を確認します。 [編集] ボックスに「App\_Data/XmlDocument .xml」と入力します。

![](creating-api-help-pages/_static/image7.png)

次に、/Controllers/ValuesController.cs. で定義されている `ValuesController` API コントローラーのコードを開きます。 いくつかのドキュメントコメントをコントローラーメソッドに追加します。 次に例を示します。

[!code-csharp[Main](creating-api-help-pages/samples/sample4.cs)]

> [!NOTE]
> ヒント: メソッドの上の行にカレットを置き、3つのスラッシュを入力すると、Visual Studio によって自動的に XML 要素が挿入されます。 次に、空白を入力します。

次に、アプリケーションを再度ビルドして実行し、ヘルプページに移動します。 ドキュメント文字列が API テーブルに表示されます。

![](creating-api-help-pages/_static/image8.png)

ヘルプページは、実行時に XML ファイルから文字列を読み取ります。 (アプリケーションを配置するときは、必ず XML ファイルを展開してください)。

## <a name="under-the-hood"></a>しくみ

ヘルプページは、Web API フレームワークの一部である**Apiexplorer**クラスの上に構築されています。 **Apiexplorer**クラスは、ヘルプページを作成するための未加工のマテリアルを提供します。 API ごとに、 **Apiexplorer**に api を説明する**apiexplorer**が含まれています。 このため、"API" は HTTP メソッドと相対 URI の組み合わせとして定義されています。 たとえば、次の Api があります。

- Api/製品を入手
- GET /api/Products/{id}
- 投稿/Api/製品

コントローラーアクションで複数の HTTP メソッドがサポートされている場合、 **Apiexplorer**は各メソッドを個別の API として扱います。

**Apiexplorer**から API を非表示にするには、アクションに**ApiExplorerSettings**属性を追加し、 *ignoreapi*を true に設定します。

[!code-csharp[Main](creating-api-help-pages/samples/sample5.cs)]

コントローラー全体を除外するために、コントローラーにこの属性を追加することもできます。

ApiExplorer クラスは、 **Idocumentation プロバイダー**インターフェイスからドキュメント文字列を取得します。 既に説明したように、ヘルプページライブラリには、XML ドキュメント文字列からドキュメントを取得する**Idocumentation プロバイダー**が用意されています。 このコードは/Areas/HelpPage/XmlDocumentationProvider.cs. にあります。 独自の**Idocumentation プロバイダー**を作成することによって、別のソースからドキュメントを取得できます。 これを行うには、 **HelpPageConfigurationExtensions**で定義されている**setdocumentation provider**拡張メソッドを呼び出します。

**Apiexplorer**は、 **idocumentation プロバイダー**インターフェイスを自動的に呼び出し、各 API のドキュメント文字列を取得します。 これらは、 **apidescription**オブジェクトと**apiparameterdescription**オブジェクトの**Documentation**プロパティに格納されます。

## <a name="next-steps"></a>次の手順

ここに表示されているヘルプページには制限がありません。 実際、 **Apiexplorer**はヘルプページの作成に限定されません。 Yao のリンクは、すぐに使えるように、優れたブログ投稿を作成しました。

- [ASP.NET Web API のヘルプページへの単純なテストクライアントの追加](https://blogs.msdn.com/b/yaohuang1/archive/2012/12/02/adding-a-simple-test-client-to-asp-net-web-api-help-page.aspx)
- [自己ホスト型サービスでの ASP.NET Web API ヘルプページの作成](https://blogs.msdn.com/b/yaohuang1/archive/2012/12/20/making-asp-net-web-api-help-page-work-on-self-hosted-services.aspx)
- [ASP.NET Web API 用のヘルプページ (またはクライアント) のデザイン時生成](https://blogs.msdn.com/b/yaohuang1/archive/2013/01/20/design-time-generation-of-help-page-or-proxy-for-asp-net-web-api.aspx)
- [詳細なヘルプページのカスタマイズ](https://blogs.msdn.com/b/yaohuang1/archive/2012/12/10/asp-net-web-api-help-page-part-3-advanced-help-page-customizations.aspx)
