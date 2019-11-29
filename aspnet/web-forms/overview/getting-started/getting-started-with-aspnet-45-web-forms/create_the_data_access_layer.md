---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/create_the_data_access_layer
title: データアクセス層を作成する |Microsoft Docs
author: Erikre
description: このチュートリアルシリーズでは、ASP.NET 4.5 と Microsoft Visual Studio Express 2013 を使用して ASP.NET Web フォームアプリケーションを構築するための基本について説明します。
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 0bbf7a6e-d7eb-4091-91e4-fff892777f32
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/create_the_data_access_layer
msc.type: authoredcontent
ms.openlocfilehash: 0fcf050474a57be9ed53ec0783a6d6b7dde2bf4c
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74575751"
---
# <a name="create-the-data-access-layer"></a>データ アクセス層の作成

[Erik Reitan](https://github.com/Erikre)

[Wingtip Toys サンプルプロジェクト (C#) をダウンロード](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)するか[、電子書籍 (PDF) をダウンロード](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)します。

> このチュートリアルシリーズでは、ASP.NET 4.5 を使用して ASP.NET Web フォームアプリケーションを構築するための基礎と、Web 用の Microsoft Visual Studio Express 2013 について説明します。 このチュートリアルシリーズ[でC#は、ソースコードが含ま](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)れる Visual Studio 2013 プロジェクトを利用できます。

このチュートリアルでは、ASP.NET Web フォームと Entity Framework Code First を使用して、データベースのデータを作成、アクセス、および確認する方法について説明します。 このチュートリアルは、前の「プロジェクトを作成する」チュートリアルに基づいており、Wingtip 玩具 Store チュートリアルシリーズの一部です。 このチュートリアルを完了すると、プロジェクトの [*モデル*] フォルダーにあるデータアクセスクラスのグループが作成されます。

## <a name="what-youll-learn"></a>学習内容:

- データモデルを作成する方法。
- データベースを初期化してシードする方法。
- データベースをサポートするようにアプリケーションを更新および構成する方法。

### <a name="these-are-the-features-introduced-in-the-tutorial"></a>このチュートリアルで導入された機能を次に示します。

- Entity Framework Code First
- LocalDB
- データの注釈

## <a name="creating-the-data-models"></a>データモデルの作成

[Entity Framework](https://msdn.microsoft.com/data/aa937723)は、オブジェクトリレーショナルマッピング (ORM) フレームワークです。 これにより、リレーショナルデータをオブジェクトとして扱うことができるため、通常は書き込む必要があるほとんどのデータアクセスコードが排除されます。 Entity Framework を使用すると、 [LINQ](https://msdn.microsoft.com/library/bb397926.aspx)を使用してクエリを発行し、厳密に型指定されたオブジェクトとしてデータを取得および操作できます。 LINQ には、データのクエリと更新のためのパターンが用意されています。 Entity Framework を使用すると、データアクセスの基礎を重視するのではなく、アプリケーションの残りの部分を作成することに集中できます。 このチュートリアルシリーズの後半では、データを使用してナビゲーションと製品のクエリを設定する方法について説明します。

Entity Framework は、 *Code First*と呼ばれる開発パラダイムをサポートしています。 Code First を使用すると、クラスを使用してデータモデルを定義できます。 クラスは、他の型、メソッド、およびイベントの変数をまとめてグループ化することによって、独自のカスタム型を作成できるようにするコンストラクトです。 クラスは、既存のデータベースにマップすることも、データベースを生成するために使用することもできます。 このチュートリアルでは、データモデルクラスを記述してデータモデルを作成します。 次に、これらの新しいクラスを使用して、すぐにデータベースを作成 Entity Framework ます。

最初に、Web フォームアプリケーションのデータモデルを定義するエンティティクラスを作成します。 次に、エンティティクラスを管理し、データベースへのデータアクセスを提供するコンテキストクラスを作成します。 また、データベースを設定するために使用する初期化子クラスも作成します。

### <a name="entity-framework-and-references"></a>Entity Framework と参照

既定では、 **Web フォーム**テンプレートを使用して新しい**ASP.NET web アプリケーション**を作成するときに Entity Framework が含まれます。 Entity Framework は、NuGet パッケージとしてインストール、アンインストール、および更新できます。

この NuGet パッケージには、次の**ランタイム**アセンブリがプロジェクト内に含まれています。

- EntityFramework .dll – Entity Framework によって使用されるすべての共通ランタイムコード
- EntityFramework. SqlServer .dll – Entity Framework の Microsoft SQL Server プロバイダー

### <a name="entity-classes"></a>エンティティクラス

データのスキーマを定義するために作成したクラスは、エンティティクラスと呼ばれます。 データベースの設計に慣れていない場合は、エンティティクラスをデータベースのテーブル定義と見なしてください。 クラスの各プロパティは、データベースのテーブルの列を指定します。 これらのクラスは、オブジェクト指向コードとデータベースのリレーショナルテーブル構造との間に、軽量のオブジェクトリレーショナルインターフェイスを提供します。

このチュートリアルでは、製品とカテゴリのスキーマを表す単純なエンティティクラスを追加することから始めます。 Products クラスには、各製品の定義が含まれます。 Product クラスの各メンバーの名前は、`ProductID`、`ProductName`、`Description`、`ImagePath`、`UnitPrice`、`CategoryID`、および `Category`になります。 Category クラスには、車両、ボート、平面など、製品が属することができる各カテゴリの定義が含まれます。 Category クラスの各メンバーの名前は、`CategoryID`、`CategoryName`、`Description`、および `Products`になります。 各製品は、いずれかのカテゴリに属します。 これらのエンティティクラスは、プロジェクトの [既存の*モデル*] フォルダーに追加されます。

1. **ソリューションエクスプローラー**で、[*モデル*] フォルダーを右クリックし、[ -&gt;**新しい項目**の**追加**] を選択します。 

    ![データアクセス層を作成する-[新しい項目] メニュー](create_the_data_access_layer/_static/image1.png)

   **[新しい項目の追加]** ダイアログ ボックスが表示されます。
2. 左側の **[インストール済み]** ウィンドウの **[ビジュアルC# ]** で、 **[コード]** を選択します。 

    ![データアクセス層を作成する-[新しい項目] メニュー](create_the_data_access_layer/_static/image2.png)
3. 中央のペインから **[クラス]** を選択し、この新しいクラスに*Product.cs*という名前を指定します。
4. **[追加]** をクリックします。  
   新しいクラスファイルがエディターに表示されます。
5. 既定のコードを次のコードに置き換えます。   

    [!code-csharp[Main](create_the_data_access_layer/samples/sample1.cs)]
6. 手順 1. ~ 4. を繰り返して別のクラスを作成し、新しいクラスに*Category.cs*という名前を付けて、既定のコードを次のコードに置き換えます。  

    [!code-csharp[Main](create_the_data_access_layer/samples/sample2.cs)]

前述のように、`Category` クラスは、アプリケーションが販売するように設計されている製品の<a id="a"></a>種類 (&quot;自動車&quot;、&quot;ボート&quot;、&quot;Rockets&quot;など) を表します。また、`Product` クラスは、データベース内の個々の製品 (toys) を表します。 `Product` オブジェクトの各インスタンスは、リレーショナルデータベーステーブル内の行に対応します。 Product クラスの各プロパティは、リレーショナルデータベーステーブルの列にマップされます。 このチュートリアルの後の方で、データベースに含まれている製品データを確認します。

### <a name="data-annotations"></a>データの注釈

クラスの一部のメンバーには、`[ScaffoldColumn(false)]`など、メンバーに関する詳細を指定する属性があることに気付きました。 これらは*データ注釈*です。 データ注釈属性では、そのメンバーのユーザー入力を検証する方法、そのメンバーの書式を指定する方法、およびデータベースの作成時にモデル化する方法を指定できます。

### <a name="context-class"></a>Context クラス

クラスを使用してデータアクセスを開始するには、コンテキストクラスを定義する必要があります。 前述のように、コンテキストクラスは、エンティティクラス (`Product` クラスや `Category` クラスなど) を管理し、データベースへのデータアクセスを提供します。

この手順では、 C#新しいコンテキストクラスを [*モデル*] フォルダーに追加します。

1. [*モデル*] フォルダーを右クリックし、[**新しい項目**の -&gt;**追加**] を選択します。   
   **[新しい項目の追加]** ダイアログ ボックスが表示されます。
2. 中央のペインで **[クラス]** を選択し、「 *ProductContext.cs* 」という名前を指定して、 **[追加]** をクリックします。
3. クラスに含まれる既定のコードを次のコードに置き換えます。   

    [!code-csharp[Main](create_the_data_access_layer/samples/sample3.cs)]

このコードは、厳密に型指定されたオブジェクトを使用してデータのクエリ、挿入、更新、および削除を行う機能を含む、Entity Framework のすべてのコア機能にアクセスできるように、`System.Data.Entity` 名前空間を追加します。

`ProductContext` クラスは Entity Framework 製品データベースコンテキストを表します。これは、データベース内の `Product` クラスインスタンスのフェッチ、格納、および更新を処理します。 `ProductContext` クラスは Entity Framework によって提供される `DbContext` 基底クラスから派生します。

### <a name="initializer-class"></a>初期化子クラス

コンテキストが初めて使用されたときにデータベースを初期化するには、いくつかのカスタムロジックを実行する必要があります。 これにより、シードデータをデータベースに追加して、製品とカテゴリをすぐに表示できるようになります。

この手順では、 C#新しい初期化子クラスを [*モデル*] フォルダーに追加します。

1. [*モデル*] フォルダーに別の `Class` を作成し、「 *ProductDatabaseInitializer.cs*」という名前を指定します。
2. クラスに含まれる既定のコードを次のコードに置き換えます。   

    [!code-csharp[Main](create_the_data_access_layer/samples/sample4.cs)]

上記のコードからわかるように、データベースを作成および初期化すると、`Seed` プロパティがオーバーライドされ、設定されます。 `Seed` プロパティが設定されている場合は、カテゴリと製品の値を使用してデータベースを設定します。 データベースの作成後に上記のコードを変更してシードデータを更新しようとすると、Web アプリケーションを実行しても更新は表示されません。 その理由は、上記のコードでは、`DropCreateDatabaseIfModelChanges` クラスの実装を使用して、シードデータをリセットする前にモデル (スキーマ) が変更されたかどうかを認識するためです。 `Category` エンティティクラスと `Product` エンティティクラスが変更されていない場合、データベースはシードデータを使用して再初期化されません。

> [!NOTE] 
> 
> アプリケーションを実行するたびにデータベースを再作成する場合は、`DropCreateDatabaseIfModelChanges` クラスではなく、`DropCreateDatabaseAlways` クラスを使用できます。 ただし、このチュートリアルシリーズでは、`DropCreateDatabaseIfModelChanges` クラスを使用します。

このチュートリアルのこの時点では、4つの新しいクラスと1つの既定のクラスを持つ*モデル*フォルダーが作成されます。

![データアクセスレイヤー-モデルフォルダーを作成する](create_the_data_access_layer/_static/image3.png)

### <a name="configuring-the-application-to-use-the-data-model"></a>データモデルを使用するようにアプリケーションを構成する

データを表すクラスを作成したので、クラスを使用するようにアプリケーションを構成する必要があります。 *Global.asax*ファイルで、モデルを初期化するコードを追加します。 *Web.config ファイルで*、新しいデータクラスによって表されるデータを格納するために使用するデータベースをアプリケーションに通知する情報を追加します。 *Global.asax*ファイルは、アプリケーションイベントまたはメソッドを処理するために使用できます。 Web.config*ファイルを*使用すると、ASP.NET web アプリケーションの構成を制御できます。

#### <a name="updating-the-globalasax-file"></a>Global.asax ファイルを更新しています

アプリケーションの起動時にデータモデルを初期化するには、 *Global.asax.cs*ファイルの `Application_Start` ハンドラーを更新します。

> [!NOTE] 
> 
> ソリューションエクスプローラーでは、 *global.asax*ファイルまたは*Global.asax.cs*ファイルのいずれかを選択して、 *Global.asax.cs*ファイルを編集できます。

1. *Global.asax.cs*ファイルの `Application_Start` メソッドに、黄色で強調表示されている次のコードを追加します。   

    [!code-csharp[Main](create_the_data_access_layer/samples/sample5.cs?highlight=9-10,22-23)]

> [!NOTE] 
> 
> ブラウザーでこのチュートリアルシリーズを表示するときに、ブラウザーで HTML5 をサポートして、黄色で強調表示されているコードを表示する必要があります。

上のコードに示すように、アプリケーションの起動時に、アプリケーションは、データに初めてアクセスしたときに実行される初期化子を指定します。 `Database` オブジェクトおよび `ProductDatabaseInitializer` オブジェクトにアクセスするには、2つの追加の名前空間が必要です。

 Web.config ファイルの変更 

データベースにシードデータが設定されると、Entity Framework Code First によって既定の場所にデータベースが生成されますが、独自の接続情報をアプリケーションに追加することで、データベースの場所を制御できます。 このデータベース接続は、プロジェクトのルートにあるアプリケーションの*web.config*ファイル内の接続文字列を使用して指定します。 新しい接続文字列を追加することによって、データベース (*ウィング*) の場所を、既定の場所ではなく、アプリケーションのデータディレクトリ (*アプリ\_データ*) に組み込むことができます。 この変更を行うと、このチュートリアルの後半でデータベースファイルを検索して調べることができます。

1. **ソリューションエクスプローラー***で、web.config ファイルを*見つけて開きます。
2. 次のように、黄色で強調表示されている接続文字列を*web.config ファイルの*`<connectionStrings>` セクションに追加します。  

    [!code-xml[Main](create_the_data_access_layer/samples/sample6.xml?highlight=4-7)]

アプリケーションを初めて実行すると、接続文字列によって指定された場所にデータベースが構築されます。 しかし、アプリケーションを実行する前に、最初にビルドしてみましょう。

## <a name="building-the-application"></a>アプリケーションのビルド

Web アプリケーションに対するすべてのクラスと変更が確実に動作するようにするには、アプリケーションをビルドする必要があります。

1. **[デバッグ]** メニューの **[ウィングヒント toys のビルド]** を選択します。  
 **[出力]** ウィンドウが表示され、すべて*正常に完了*すると、成功メッセージが表示されます。  

    ![データアクセス層の出力ウィンドウを作成する](create_the_data_access_layer/_static/image4.png)

エラーが発生した場合は、上記の手順を再確認してください。 **[出力]** ウィンドウの情報には、問題が発生しているファイルと、ファイル内の変更が必要な場所が示されます。 この情報を使用すると、プロジェクトで上記の手順のどの部分を確認し、修正する必要があるかを判断できます。

## <a name="summary"></a>要約

このシリーズのこのチュートリアルでは、と同様に、データモデルを作成し、データベースの初期化とシードに使用するコードを追加しました。 また、アプリケーションの実行時にデータモデルを使用するようにアプリケーションを構成しました。

次のチュートリアルでは、UI を更新し、ナビゲーションを追加して、データベースからデータを取得します。 これにより、このチュートリアルで作成したエンティティクラスに基づいて、データベースが自動的に作成されます。

## <a name="additional-resources"></a>その他の資料

[Entity Framework の概要](https://msdn.microsoft.com/library/bb399567.aspx)   
[ADO.NET Entity Framework  の初心](https://msdn.microsoft.com/data/ee712907)者向けガイド  
[Entity Framework を使用した Code First 開発](http://www.msteched.com/2010/Europe/DEV212)(ビデオ)   
[Code First リレーションシップの FLUENT API](https://msdn.microsoft.com/data/hh134698)   
[データ注釈の Code First](https://msdn.microsoft.com/data/gg193958)  
[Entity Framework の生産性の向上](https://blogs.msdn.com/b/efdesign/archive/2010/06/21/productivity-improvements-for-the-entity-framework.aspx?wa=wsignin1.0)

> [!div class="step-by-step"]
> [前へ](create-the-project.md)
> [次へ](ui_and_navigation.md)
