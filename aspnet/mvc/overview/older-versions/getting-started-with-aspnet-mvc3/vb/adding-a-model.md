---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-model
title: モデルの追加 (VB) |Microsoft Docs
author: Rick-Anderson
description: このチュートリアルでは、Microsoft Visual Web Developer 2010 Express Service Pack 1 を使用した ASP.NET MVC Web アプリケーションの構築の基本について説明します。
ms.author: riande
ms.date: 01/12/2011
ms.assetid: b3aa7720-5c78-4ca2-baef-9a52234fb7ce
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-model
msc.type: authoredcontent
ms.openlocfilehash: e69d59aed4d74f08f1c653c4965b128c4dbe20ff
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78434602"
---
# <a name="adding-a-model-vb"></a>モデルの追加 (VB)

[Rick Anderson](https://twitter.com/RickAndMSFT)

> このチュートリアルでは、Microsoft Visual Studio の無料バージョンである Microsoft Visual Web Developer 2010 Express Service Pack 1 を使用した ASP.NET MVC Web アプリケーションの構築の基本について説明します。 開始する前に、以下に示す前提条件がインストールされていることを確認してください。 これらのすべてをインストールするには、[ [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)] リンクをクリックします。 または、次のリンクを使用して、前提条件を個別にインストールすることもできます。
> 
> - [Visual Studio Web Developer Express SP1 の前提条件](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 ツールの更新](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(ランタイム + ツールのサポート)
> 
> Visual Web Developer 2010 ではなく Visual Studio 2010 を使用している場合は、次のリンクをクリックして必要なコンポーネントをインストールします: [Visual studio 2010 の前提条件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。
> 
> このトピックには、VB.NET ソースコードを含む Visual Web Developer プロジェクトが用意されています。 [VB.NET バージョンをダウンロード](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)します。 必要に応じC#て[ C# ](../cs/adding-a-model.md) 、このチュートリアルのバージョンに切り替えます。

## <a name="adding-a-model"></a>モデルの追加

このセクションでは、データベースのムービーを管理するためのクラスをいくつか追加します。 これらのクラスは、ASP.NET MVC アプリケーションの "モデル" 部分になります。

Entity Framework と呼ばれる .NET Framework のデータアクセステクノロジを使用して、これらのモデルクラスを定義および操作します。 Entity Framework (EF と呼ばれることもあります) では、 *Code First*と呼ばれる開発パラダイムがサポートされています。 Code First を使用すると、単純なクラスを記述することによってモデルオブジェクトを作成できます。 (これらは、"plain old CLR objects" の POCO クラスとも呼ばれます)。その後、データベースをクラスからすぐに作成することができます。これにより、非常にクリーンで迅速な開発ワークフローが可能になります。

## <a name="adding-model-classes"></a>モデルクラスの追加

**ソリューションエクスプローラー**で、[*モデル*] フォルダーを右クリックし、 **[追加]** 、 **[クラス]** の順に選択します。

![](adding-a-model/_static/image1.png)

クラスに "Movie" という名前を指定します。

次の5つのプロパティを `Movie` クラスに追加します。

[!code-vb[Main](adding-a-model/samples/sample1.vb)]

`Movie` クラスを使用して、データベース内の映画を表します。 `Movie` オブジェクトの各インスタンスは、データベーステーブル内の行に対応し、`Movie` クラスの各プロパティはテーブル内の列にマップされます。

同じファイルで、次の `MovieDBContext` クラスを追加します。

[!code-vb[Main](adding-a-model/samples/sample2.vb)]

`MovieDBContext` クラスは Entity Framework ムービーデータベースコンテキストを表します。このコンテキストでは、データベース内の `Movie` クラスインスタンスのフェッチ、格納、および更新が処理されます。 `MovieDBContext` は、Entity Framework によって提供される `DbContext` 基底クラスから派生します。 `DbContext` と `DbSet`の詳細については、「 [Entity Framework の生産性の向上](https://blogs.msdn.com/b/efdesign/archive/2010/06/21/productivity-improvements-for-the-entity-framework.aspx?wa=wsignin1.0)」を参照してください。

`DbContext` と `DbSet`を参照できるようにするには、ファイルの先頭に次の `imports` ステートメントを追加する必要があります。

[!code-vb[Main](adding-a-model/samples/sample3.vb)]

完成した*ムービー .vb*ファイルを以下に示します。

[!code-vb[Main](adding-a-model/samples/sample4.vb)]

## <a name="creating-a-connection-string-and-working-with-sql-server-compact"></a>接続文字列の作成と SQL Server Compact の操作

作成した `MovieDBContext` クラスによって、データベースへの接続と `Movie` オブジェクトのデータベースレコードへのマッピングのタスクが処理されます。 ただし、接続先のデータベースを指定する方法について質問することもできます。 これを行うに*は、アプリケーションの web.config ファイルに*接続情報を追加します。

アプリケーション*ルートの web.config ファイル*を開きます。 ( *Views*フォルダー*内の web.config ファイルで*はありません)。次の図は、両方の web.config ファイルを示して*い*ます。赤で囲まれた web.config ファイルを*開きます。*

![](adding-a-model/_static/image2.png)

次の接続文字列を web.config ファイルの `<connectionStrings>` 要素に追加*します。*

[!code-xml[Main](adding-a-model/samples/sample5.xml)]

次の例は、新しい接続文字列が追加された web.config ファイルの一部を示して*い*ます。

[!code-xml[Main](adding-a-model/samples/sample6.xml)]

この少量のコードと XML は、ムービーデータを表現してデータベースに格納するために記述する必要があるすべてのものです。

次に、ムービーデータを表示するために使用できる新しい `MoviesController` クラスを作成し、ユーザーが新しいムービーの一覧を作成できるようにします。

> [!div class="step-by-step"]
> [前へ](adding-a-view.md)
> [次へ](accessing-your-models-data-from-a-controller.md)
