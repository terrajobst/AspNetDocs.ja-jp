---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-endpoint
title: ASP.NET Web API 2.2 | を使用して OData v4 エンドポイントを作成するMicrosoft Docs
author: MikeWasson
description: Open Data Protocol (OData) は、web 用のデータアクセスプロトコルです。 OData は、CRUD 操作によってデータセットをクエリおよび操作するための統一された方法を提供します...
ms.author: riande
ms.date: 01/23/2019
ms.assetid: 1e1927c0-ded1-4752-80fd-a146628d2f09
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-endpoint
msc.type: authoredcontent
ms.openlocfilehash: 81d134cbd3231b9a0d5537ccbd1bbfe6419254af
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484498"
---
# <a name="create-an-odata-v4-endpoint-using-aspnet-web-api"></a>ASP.NET Web API を使用して OData v4 エンドポイントを作成する 

> Open Data Protocol (OData) は、web 用のデータアクセスプロトコルです。 OData は、CRUD 操作 (作成、読み取り、更新、および削除) によってデータセットをクエリおよび操作するための統一された方法を提供します。
>
> ASP.NET Web API は、プロトコルの v3 と v4 の両方をサポートしています。 V4 エンドポイントを、v3 エンドポイントとサイドバイサイドで実行することもできます。
>
> このチュートリアルでは、CRUD 操作をサポートする OData v4 エンドポイントを作成する方法について説明します。
>
> ## <a name="software-versions-used-in-the-tutorial"></a>このチュートリアルで使用されているソフトウェアのバージョン
>
> - Web API 5.2
> - OData v4
> - Visual Studio 2017 (Visual Studio 2017 を[こちら](https://visualstudio.microsoft.com/downloads/)からダウンロード)
> - Entity Framework 6
> - .NET 4.7.2
>
> ## <a name="tutorial-versions"></a>チュートリアルのバージョン
>
> OData バージョン3については、「 [odata V3 エンドポイントの作成](../odata-v3/creating-an-odata-endpoint.md)」を参照してください。

## <a name="create-the-visual-studio-project"></a>Visual Studio プロジェクトを作成する

Visual Studio で、 **[ファイル]** メニューの [**新しい**&gt;**プロジェクト**] をクリックします。

[**インストールされている**&gt;  **C# Visual** &gt; **web**] を展開し、 **[ASP.NET Web Application (.NET Framework)]** テンプレートを選択します。 プロジェクトに ProductService&quot;&quot;名前を指定します。

[![](create-an-odata-v4-endpoint/_static/image7.png)](create-an-odata-v4-endpoint/_static/image7.png)

**[OK]** を選択します。

[![](create-an-odata-v4-endpoint/_static/image8.png)](create-an-odata-v4-endpoint/_static/image8.png)

**[空]** テンプレートを選択します。 **[フォルダーとコア参照の追加先]** で、 **[Web API]** を選択します。 **[OK]** を選択します。

## <a name="install-the-odata-packages"></a>OData パッケージのインストール

**[ツール]** メニューで、 **[NuGet パッケージ マネージャー]** &gt; **[パッケージ マネージャー コンソール]** の順に選択します。 [パッケージマネージャーコンソール] ウィンドウで、次のように入力します。

[!code-console[Main](create-an-odata-v4-endpoint/samples/sample1.cmd)]

このコマンドは、最新の OData NuGet パッケージをインストールします。

## <a name="add-a-model-class"></a>モデル クラスの追加

*モデル*は、アプリケーション内のデータエンティティを表すオブジェクトです。

ソリューション エクスプローラーで、[モデル] フォルダーを右クリックします。 コンテキストメニューから [&gt;**クラス**の**追加**] を選択します。

[![](create-an-odata-v4-endpoint/_static/image6.png)](create-an-odata-v4-endpoint/_static/image5.png)

> [!NOTE]
> 慣例により、モデルクラスは [モデル] フォルダーに配置されますが、独自のプロジェクトでこの規則に従う必要はありません。

クラスに `Product` という名前を付けます。 Product.cs ファイルで、定型コードを次のコードに置き換えます。

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample2.cs)]

`Id` プロパティは、エンティティキーです。 クライアントは、キーによってエンティティを照会できます。 たとえば、ID が5の製品を取得するために、URI は `/Products(5)`ます。 `Id` プロパティは、バックエンドデータベースの主キーにもなります。

## <a name="enable-entity-framework"></a>Entity Framework を有効にする

このチュートリアルでは、Entity Framework (EF) Code First を使用してバックエンドデータベースを作成します。

> [!NOTE]
> Web API OData には EF は必要ありません。 データベースエンティティをモデルに変換できる任意のデータアクセスレイヤーを使用します。

最初に、EF 用の NuGet パッケージをインストールします。 **[ツール]** メニューで、 **[NuGet パッケージ マネージャー]** &gt; **[パッケージ マネージャー コンソール]** の順に選択します。 [パッケージマネージャーコンソール] ウィンドウで、次のように入力します。

[!code-console[Main](create-an-odata-v4-endpoint/samples/sample3.cmd)]

Web.config ファイルを開き、**構成**要素内の**configsections**要素の後に次のセクションを追加します。

[!code-xml[Main](create-an-odata-v4-endpoint/samples/sample4.xml?highlight=6)]

この設定により、LocalDB データベースの接続文字列が追加されます。 このデータベースは、アプリをローカルで実行するときに使用されます。

次に、`ProductsContext` という名前のクラスを [モデル] フォルダーに追加します。

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample5.cs)]

コンストラクターでは、`"name=ProductsContext"` 接続文字列の名前を指定します。

## <a name="configure-the-odata-endpoint"></a>OData エンドポイントを構成する

File App\_Start/Webapiconfig.cs を開きます。 次の**using ステートメントを追加し**ます。

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample6.cs)]

次に、 **Register**メソッドに次のコードを追加します。

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample7.cs)]

このコードでは、次の2つの処理を行います。

- Entity Data Model (EDM) を作成します。
- ルートを追加します。

EDM は、データの抽象モデルです。 EDM は、サービスメタデータドキュメントの作成に使用されます。 **ODataConventionModelBuilder**クラスは、既定の名前付け規則を使用して EDM を作成します。 この方法では、最小限のコードが必要です。 EDM をより細かく制御する場合は、プロパティ、キー、およびナビゲーションプロパティを明示的に追加することで、**使用**クラスを使用して edm を作成できます。

*ルート*は、HTTP 要求をエンドポイントにルーティングする方法を Web API に指示します。 OData v4 ルートを作成するには、 **MapODataServiceRoute**拡張メソッドを呼び出します。

アプリケーションに複数の OData エンドポイントがある場合は、それぞれに対して個別のルートを作成します。 各ルートに一意のルート名とプレフィックスを指定します。

## <a name="add-the-odata-controller"></a>OData コントローラーを追加する

*コントローラー*は、HTTP 要求を処理するクラスです。 OData サービスでは、エンティティセットごとに個別のコントローラーを作成します。 このチュートリアルでは、`Product` エンティティ用に1つのコントローラーを作成します。

ソリューションエクスプローラーで、Controllers フォルダーを右クリックし、[&gt;**クラス**の**追加**] を選択します。 クラスに `ProductsController` という名前を付けます。

> [!NOTE]
> OData v3 用のこのチュートリアルのバージョンでは、**コントローラーの追加**スキャフォールディングを使用します。 現時点では、OData v4 のスキャフォールディングはありません。

ProductsController.cs の定型コードを次のコードに置き換えます。

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample8.cs)]

コントローラーは `ProductsContext` クラスを使用して、EF を使用してデータベースにアクセスします。 コントローラーは、製品**コンテキスト**を破棄するために**dispose**メソッドをオーバーライドすることに注意してください。

これは、コントローラーの開始点です。 次に、すべての CRUD 操作に対してメソッドを追加します。

## <a name="query-the-entity-set"></a>エンティティセットに対してクエリを実行する

次のメソッドを `ProductsController`に追加します。

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample9.cs)]

`Get` メソッドのパラメーターなしのバージョンは、製品コレクション全体を返します。 *キー*パラメーターを指定した `Get` メソッドでは、キー (この例では `Id` プロパティ) によって製品が検索されます。

**[Enablequery]** 属性を使用すると、$filter、$sort、$page などのクエリオプションを使用して、クライアントがクエリを変更できます。 詳細については、「 [OData クエリオプションのサポート](../supporting-odata-query-options.md)」を参照してください。

## <a name="add-an-entity-to-the-entity-set"></a>エンティティをエンティティセットに追加する

クライアントがデータベースに新しい製品を追加できるようにするには、次のメソッドを `ProductsController`に追加します。

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample10.cs)]

## <a name="update-an-entity"></a>エンティティを更新する

OData は、エンティティ、修正プログラム、および PUT を更新するための2つの異なるセマンティクスをサポートしています。

- PATCH は、部分的な更新を実行します。 クライアントは、更新するプロパティだけを指定します。
- PUT は、エンティティ全体を置き換えます。

PUT の欠点は、クライアントがエンティティ内のすべてのプロパティの値を送信する必要があることです。変更されていない値も含まれます。 [OData 仕様](http://docs.oasis-open.org/odata/odata/v4.0/os/part1-protocol/odata-v4.0-os-part1-protocol.html#_Toc372793719)では、修正プログラムが推奨されています。

どのような場合でも、PATCH メソッドと PUT メソッドのコードは次のようになります。

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample11.cs)]

パッチの場合、コントローラーは**デルタ&lt;t&gt;** 型を使用して変更を追跡します。

## <a name="delete-an-entity"></a>エンティティを削除する

クライアントがデータベースから製品を削除できるようにするには、次のメソッドを `ProductsController`に追加します。

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample12.cs)]
