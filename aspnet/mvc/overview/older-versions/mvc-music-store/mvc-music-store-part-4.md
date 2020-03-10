---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-4
title: 'パート 4: モデルとデータアクセス |Microsoft Docs'
author: jongalloway
description: このチュートリアルシリーズでは、ASP.NET MVC ミュージックストアサンプルアプリケーションをビルドするために実行するすべての手順について詳しく説明します。 パート4では、モデルとデータアクセスについて説明します。
ms.author: riande
ms.date: 04/21/2011
ms.assetid: ab55ca81-ab9b-44a0-8700-dc6da2599335
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-4
msc.type: authoredcontent
ms.openlocfilehash: 402be340f1ea3344675e7b859cea8c5130cfc8ee
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78451018"
---
# <a name="part-4-models-and-data-access"></a>パート 4: モデルとデータアクセス

( [Jon Galloway](https://github.com/jongalloway) )

> MVC Music Store は、ASP.NET MVC と Visual Studio を使用して web 開発を行う方法を紹介したチュートリアルアプリケーションです。  
>   
> MVC ミュージックストアは、音楽アルバムをオンラインで販売し、基本的なサイト管理、ユーザーサインイン、およびショッピングカート機能を実装する軽量のサンプルストア実装です。
> 
> このチュートリアルシリーズでは、ASP.NET MVC ミュージックストアサンプルアプリケーションをビルドするために実行するすべての手順について詳しく説明します。 パート4では、モデルとデータアクセスについて説明します。

ここまでは、コントローラーからビューテンプレートに "ダミーデータ" を渡しています。 これで、実際のデータベースをフックする準備ができました。 このチュートリアルでは、データベースエンジンとして SQL Server Compact エディション (多くの場合、SQL CE) を使用する方法について説明します。 SQL CE は、インストールや構成を必要としない、組み込まれた、ファイルベースの無料のデータベースです。これにより、ローカルでの開発に非常に便利です。

## <a name="database-access-with-entity-framework-code-first"></a>Entity Framework コードを使用したデータベースアクセス

ASP.NET MVC 3 プロジェクトに含まれている Entity Framework (EF) のサポートを使用して、データベースのクエリと更新を行います。 EF は、オブジェクト指向の方法でデータベースに格納されているデータのクエリと更新を開発者が行うことができる柔軟なオブジェクトリレーショナルマッピング (ORM) データ API です。

Entity Framework version 4 では、code first と呼ばれる開発パラダイムがサポートされています。 Code first では、単純なクラス ("plain old" CLR オブジェクトからの POCO とも呼ばれます) を記述することによってモデルオブジェクトを作成できます。また、クラスからすぐにデータベースを作成することもできます。

### <a name="changes-to-our-model-classes"></a>モデルクラスの変更点

このチュートリアルでは Entity Framework のデータベース作成機能を利用します。 これを行う前に、モデルクラスにいくつかの軽微な変更を加えて、後で使用するいくつかの点を追加してみましょう。

#### <a name="adding-the-artist-model-classes"></a>アーティストモデルクラスの追加

アルバムはアーティストに関連付けられるので、アーティストを説明する単純なモデルクラスを追加します。 次に示すコードを使用して、Artist.cs という名前のモデルフォルダーに新しいクラスを追加します。

[!code-csharp[Main](mvc-music-store-part-4/samples/sample1.cs)]

#### <a name="updating-our-model-classes"></a>モデルクラスを更新しています

次に示すようにアルバムクラスを更新します。

[!code-csharp[Main](mvc-music-store-part-4/samples/sample2.cs)]

次に、Genre クラスに対して次の更新を行います。

[!code-csharp[Main](mvc-music-store-part-4/samples/sample3.cs)]

### <a name="adding-the-app_data-folder"></a>アプリ\_データフォルダーの追加

ここでは、SQL Server Express データベースファイルを保持するために、アプリ\_データディレクトリをプロジェクトに追加します。 アプリ\_データは、データベースアクセスに対する適切なセキュリティアクセス許可を既に持っている ASP.NET の特別なディレクトリです。 [プロジェクト] メニューの [ASP.NET フォルダーの追加]、[アプリ\_データ] の順に選択します。

![](mvc-music-store-part-4/_static/image1.png)

### <a name="creating-a-connection-string-in-the-webconfig-file"></a>Web.config ファイルでの接続文字列の作成

Web サイトの構成ファイルに数行を追加して、Entity Framework がデータベースへの接続方法を認識できるようにします。 プロジェクトのルートにある web.config ファイルをダブルクリックします。

![](mvc-music-store-part-4/_static/image2.png)

このファイルの一番下までスクロールし、次に示すように、最後の行のすぐ上に &lt;connectionStrings&gt; セクションを追加します。

[!code-xml[Main](mvc-music-store-part-4/samples/sample4.xml)]

### <a name="adding-a-context-class"></a>コンテキストクラスの追加

[モデル] フォルダーを右クリックし、MusicStoreEntities.cs という名前の新しいクラスを追加します。

![](mvc-music-store-part-4/_static/image3.png)

このクラスは Entity Framework データベースコンテキストを表し、作成、読み取り、更新、削除の各操作を処理します。 このクラスのコードを次に示します。

[!code-csharp[Main](mvc-music-store-part-4/samples/sample5.cs)]

これで、他の構成や特別なインターフェイスなどはありません。DbContext 基本クラスを拡張することで、MusicStoreEntities クラスはデータベース操作を処理できるようになります。 これで、データベース内の追加情報の一部を利用するために、いくつかのプロパティをモデルクラスに追加してみましょう。

### <a name="adding-our-store-catalog-data"></a>ストアカタログデータを追加しています

新しく作成されたデータベースに "シード" データを追加する Entity Framework の機能を活用します。 これにより、ストアカタログにジャンル、アーティスト、アルバムの一覧が事前設定されます。 このチュートリアルの前半で使用したサイト設計ファイルが含まれている MvcMusicStore-Assets download には、このシードデータを含むクラスファイルがあります。このファイルは、コードという名前のフォルダーにあります。

次に示すように、[コード/モデル] フォルダー内の SampleData.cs ファイルを見つけて、プロジェクトの [モデル] フォルダーにドロップします。

![](mvc-music-store-part-4/_static/image4.png)

次に、SampleData クラスについて Entity Framework を示す1行のコードを追加する必要があります。 プロジェクトのルートにある global.asax ファイルをダブルクリックして開き、次の行をアプリケーション\_の開始メソッドの先頭に追加します。

[!code-csharp[Main](mvc-music-store-part-4/samples/sample6.cs)]

この時点で、プロジェクトの Entity Framework を構成するために必要な作業が完了しました。

## <a name="querying-the-database"></a>データベースに対するクエリの実行

次に、"ダミーデータ" を使用する代わりに、データベースを呼び出してすべての情報を照会するように、StoreController を更新してみましょう。 まず、 **StoreController**のフィールドを宣言して、storedb という名前の MusicStoreEntities クラスのインスタンスを保持します。

[!code-csharp[Main](mvc-music-store-part-4/samples/sample7.cs)]

### <a name="updating-the-store-index-to-query-the-database"></a>データベースに対してクエリを実行するためのストアインデックスの更新

MusicStoreEntities クラスは Entity Framework によって管理され、データベース内の各テーブルのコレクションプロパティを公開します。 StoreController のインデックスアクションを更新して、データベース内のすべてのジャンルを取得してみましょう。 以前は、文字列データをハードコーディングしていました。 次に、Entity Framework コンテキストのコレクションを使用するだけで済みます。

[!code-csharp[Main](mvc-music-store-part-4/samples/sample8.cs)]

ビューテンプレートを変更する必要はありません。以前に返された同じ StoreIndexViewModel を返しています。ここでは、データベースからライブデータを返すだけです。

プロジェクトを再度実行して "/Store" URL にアクセスすると、データベース内のすべてのジャンルの一覧が表示されます。

![](mvc-music-store-part-4/_static/image1.jpg)

### <a name="updating-store-browse-and-details-to-use-live-data"></a>ライブデータを使用するためのストアの参照と詳細の更新

/Store/Browse? genre = *[some genre]* アクションメソッドを使用して、名前でジャンルを検索しています。 同じジャンル名に対して2つのエントリを持つことはできないため、1つの結果のみが期待されます。これにより、を使用できるようになります。次のように適切な Genre オブジェクトを照会するための LINQ の単一 () 拡張機能 (これはまだ入力しないでください):

[!code-csharp[Main](mvc-music-store-part-4/samples/sample9.cs)]

1つのメソッドは、ラムダ式をパラメーターとして受け取ります。これは、定義した値と名前が一致するように、1つの Genre オブジェクトを必要とすることを指定します。 上記の例では、Disco という名前の値を持つ1つの Genre オブジェクトを読み込んでいます。

ここでは、Genre オブジェクトを取得するときに、読み込まれる他の関連エンティティを示すことができる Entity Framework 機能を活用します。 この機能はクエリ結果の整形と呼ばれており、必要なすべての情報を取得するために、データベースにアクセスする必要がある回数を減らすことができます。 取得したジャンルのアルバムを事前にフェッチして、ジャンルに含まれるようにクエリを更新します。関連するアルバムが必要であることを示すには、"アルバム" を含めます。 これは、1つのデータベース要求でジャンルとアルバムの両方のデータを取得するため、より効率的です。

説明については、更新された Browse controller アクションは次のようになります。

[!code-csharp[Main](mvc-music-store-part-4/samples/sample10.cs)]

ストアの参照ビューを更新して、各ジャンルで利用できるアルバムを表示できるようになりました。 ビューテンプレート (/Views/Store/Browse.cshtml にあります) を開き、次のように、アルバムの箇条書きリストを追加します。

[!code-cshtml[Main](mvc-music-store-part-4/samples/sample11.cshtml)]

アプリケーションを実行し、/ストア/参照を参照します。 genre = ジャズは、結果がデータベースからプルされ、選択したジャンルのすべてのアルバムが表示されるようになったことを示しています。

![](mvc-music-store-part-4/_static/image2.jpg)

ここでは、/Store/[id] URL に対して同じ変更を行い、ダミーデータを、パラメーター値に一致する ID を持つアルバムを読み込むデータベースクエリに置き換えます。

[!code-csharp[Main](mvc-music-store-part-4/samples/sample12.cs)]

アプリケーションを実行して/Store/Details/1 を参照すると、結果がデータベースからプルされていることがわかります。

![](mvc-music-store-part-4/_static/image5.png)

これで、ストアの詳細 ページがアルバム ID でアルバムを表示するように設定されたので、**参照** ビューを更新して詳細ビューにリンクします。 ここでは、Html.actionlink を使用します。これは、ストアインデックスから、前のセクションの最後のストア参照にリンクするのと同じです。 参照ビューの完全なソースが下に表示されます。

[!code-cshtml[Main](mvc-music-store-part-4/samples/sample13.cshtml)]

これで、ストアのページから、利用可能なアルバムを一覧表示するジャンルページを参照できるようになりました。アルバムをクリックすると、そのアルバムの詳細を表示できます。

![](mvc-music-store-part-4/_static/image6.png)

> [!div class="step-by-step"]
> [前へ](mvc-music-store-part-3.md)
> [次へ](mvc-music-store-part-5.md)
