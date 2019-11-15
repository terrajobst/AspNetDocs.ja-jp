---
uid: web-forms/overview/data-access/introduction/creating-a-data-access-layer-cs
title: データアクセス層 (C#) を作成するMicrosoft Docs
author: rick-anderson
description: このチュートリアルでは、最初から開始し、型指定されたデータセットを使用してデータアクセス層 (DAL) を作成し、データベース内の情報にアクセスします。
ms.author: riande
ms.date: 04/05/2010
ms.assetid: cfe2a6a0-1e56-4dc8-9537-c8ec76ba96a4
msc.legacyurl: /web-forms/overview/data-access/introduction/creating-a-data-access-layer-cs
msc.type: authoredcontent
ms.openlocfilehash: 5aaf97dc8448dcb7b94ef2e4e23f34fd37ac4426
ms.sourcegitcommit: 6f0e10e4ca61a1e5534b09c655fd35cdc6886c8a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/15/2019
ms.locfileid: "74115249"
---
# <a name="creating-a-data-access-layer-c"></a>データ アクセス層を作成する (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[PDF のダウンロード](creating-a-data-access-layer-cs/_static/datatutorial01cs1.pdf)

> このチュートリアルでは、最初から開始し、型指定されたデータセットを使用してデータアクセス層 (DAL) を作成し、データベース内の情報にアクセスします。

## <a name="introduction"></a>概要

Web 開発者として、データの操作を中心にしています。 データを格納するデータベース、データを取得および変更するコード、収集して集計するための web ページを作成します。 これは、ASP.NET 2.0 でこれらの共通パターンを実装するための手法を紹介する、長いシリーズの最初のチュートリアルです。 まず、型指定されたデータセットを使用するデータアクセス層 (DAL)、カスタムビジネスルールを適用するビジネスロジック層 (BLL)、および共通ページレイアウトを共有する ASP.NET ページで構成されるプレゼンテーション層で構成される[ソフトウェアアーキテクチャ](http://en.wikipedia.org/wiki/Software_architecture)の作成から始めます。 このバックエンドの基礎を説明した後、レポートを作成し、web アプリケーションのデータを表示、要約、収集、検証する方法を示します。 これらのチュートリアルは簡潔にすることを目的としており、プロセスを視覚的に説明するためのさまざまなスクリーンショットを含む詳細な手順を説明しています。 各チュートリアルは、およびC# Visual Basic バージョンで使用でき、使用されている完全なコードのダウンロードが含まれています。 (この最初のチュートリアルでは非常に時間がかかりますが、残りの部分はより多くの消化チャンクで示されています)。

これらのチュートリアルでは、**アプリ\_データ**ディレクトリに配置されている Microsoft SQL Server 2005 Express Edition バージョンの Northwind データベースを使用します。 データベースファイルに加えて、 **App\_Data**フォルダーには、別のデータベースバージョンを使用する場合に備えて、データベースを作成するための SQL スクリプトも含まれています。 これらのスクリプトは、必要に応じて[Microsoft から直接ダウンロード](https://www.microsoft.com/downloads/details.aspx?FamilyID=06616212-0356-46a0-8da2-eebc53a68034&amp;DisplayLang=en)することもできます。 別の SQL Server バージョンの Northwind データベースを使用する場合は、アプリケーションの**web.config**ファイルの**NORTHWNDConnectionString**設定を更新する必要があります。 Web アプリケーションは、Visual Studio 2005 Professional Edition をファイルシステムベースの Web サイトプロジェクトとして使用して構築されました。 ただし、すべてのチュートリアルは、Visual Studio 2005、 [Visual Web Developer](https://msdn.microsoft.com/vstudio/express/vwd/)の無料版でも同様に機能します。  
  
このチュートリアルでは、最初から開始し、データアクセス層 (DAL) を作成します。次に、2番目のチュートリアルでビジネスロジック層 (BLL) を作成し、3番目のページレイアウトとナビゲーションを操作します。 3番目のチュートリアルの後のチュートリアルは、最初の3つの基盤に基づいて構築されます。 この最初のチュートリアルでは詳しく説明しているので、Visual Studio を起動して始めましょう。

## <a name="step-1-creating-a-web-project-and-connecting-to-the-database"></a>手順 1: Web プロジェクトの作成とデータベースへの接続

データアクセス層 (DAL) を作成するには、まず web サイトを作成し、データベースをセットアップする必要があります。 まず、新しいファイルシステムベースの ASP.NET web サイトを作成します。 これを行うには、[ファイル] メニューの [新しい Web サイト] をクリックし、[新しい Web サイト] ダイアログボックスを表示します。 ASP.NET Web サイトテンプレートを選択し、[場所] ドロップダウンリストを [ファイルシステム] に設定して、Web サイトを配置するフォルダーを選択C#し、言語をに設定します。

[新しいファイルシステムベースの Web サイトを作成 ![には](creating-a-data-access-layer-cs/_static/image2.png)](creating-a-data-access-layer-cs/_static/image1.png)

**図 1**: 新しいファイルシステムベースの Web サイトを作成[する (クリックすると、フルサイズの画像が表示](creating-a-data-access-layer-cs/_static/image3.png)されます)

これにより、 **default.aspx** ASP.NET ページと**App\_Data**フォルダーを使用して新しい web サイトが作成されます。

Web サイトが作成されたので、次の手順では、Visual Studio のサーバーエクスプローラーでデータベースへの参照を追加します。 サーバーエクスプローラーにデータベースを追加することで、Visual Studio 内からテーブル、ストアドプロシージャ、ビューなどを追加できます。 また、クエリビルダーを使用して、テーブルデータを表示したり、独自のクエリを作成したりすることもできます。 さらに、DAL 用に型指定されたデータセットを作成する場合は、型指定されたデータセットを構築するデータベースを Visual Studio にポイントする必要があります。 この接続情報はその時点で提供できますが、Visual Studio では、サーバーエクスプローラーに既に登録されているデータベースのドロップダウンリストが自動的に作成されます。

Northwind データベースをサーバーエクスプローラーに追加する手順は、**アプリ\_Data**フォルダーで SQL Server 2005 Express Edition データベースを使用するかどうか、または代わりに使用する Microsoft SQL Server 2000 または2005データベースサーバーのセットアップがあるかどうかによって異なります。

## <a name="using-a-database-in-the-app_data-folder"></a>App\_Data フォルダー内のデータベースの使用

接続する SQL Server 2000 または2005データベースサーバーがない場合、または単にデータベースサーバーにデータベースを追加する必要がない場合は、ダウンロードした web サイトの**アプリ\_データ**フォルダー (northwnd.mdf) にある SQL Server 2005 Express Edition バージョンの Northwind データベースを使用でき**ます。MDF**)。

**App\_Data**フォルダーに配置されたデータベースがサーバーエクスプローラーに自動的に追加されます。 コンピューターに SQL Server 2005 Express Edition がインストールされていると仮定すると、NORTHWND.MDF という名前のノードが表示されます。サーバーエクスプローラーの MDF。テーブル、ビュー、ストアドプロシージャなどを展開し、探索することができます (図2を参照)。

**アプリの\_データ**フォルダーには、Microsoft access の **.mdb**ファイルも保持できます。このファイルは、対応する SQL Server と同様に、サーバーエクスプローラーに自動的に追加されます。 SQL Server オプションを使用しない場合は、常に[Microsoft access バージョンの Northwind データベースファイルをダウンロード](https://www.microsoft.com/downloads/details.aspx?FamilyID=C6661372-8DBE-422B-8676-C632D66C529C&amp;displaylang=EN)して、**アプリの\_データ**ディレクトリにドロップできます。 ただし、Access データベースは SQL Server ほど機能が豊富ではなく、web サイトのシナリオで使用するように設計されていないことに注意してください。 さらに、35以上のチュートリアルでは、Access でサポートされていないデータベースレベルの機能がいくつか使用されています。

## <a name="connecting-to-the-database-in-a-microsoft-sql-server-2000-or-2005-database-server"></a>Microsoft SQL Server 2000 または2005データベースサーバーでのデータベースへの接続

または、データベースサーバーにインストールされている Northwind データベースに接続することもできます。 データベースサーバーに Northwind データベースがまだインストールされていない場合は、まず、このチュートリアルのダウンロードに含まれているインストールスクリプトを実行するか、 [northwind およびインストールスクリプトの SQL Server 2000 バージョン](https://www.microsoft.com/downloads/details.aspx?FamilyID=06616212-0356-46a0-8da2-eebc53a68034&amp;DisplayLang=en)を Microsoft の web サイトから直接ダウンロードして、データベースサーバーに追加する必要があります。

データベースがインストールされたら、Visual Studio のサーバーエクスプローラーにアクセスし、[データ接続] ノードを右クリックして、[接続の追加] を選択します。 サーバーエクスプローラーが表示されない場合は、ビューまたはサーバーエクスプローラーにアクセスするか、Ctrl + Alt + S キーを押します。 [接続の追加] ダイアログボックスが表示されます。このダイアログボックスでは、接続先のサーバー、認証情報、およびデータベース名を指定できます。 データベース接続情報を正しく構成し、[OK] ボタンをクリックすると、データベースは [データ接続] ノードの下にノードとして追加されます。 データベースノードを展開して、テーブル、ビュー、ストアドプロシージャなどを調べることができます。

![データベースサーバーの Northwind データベースに接続を追加する](creating-a-data-access-layer-cs/_static/image4.png)

**図 2**: データベースサーバーの Northwind データベースに接続を追加する

## <a name="step-2-creating-the-data-access-layer"></a>手順 2: データアクセス層の作成

データを操作する場合は、データ固有のロジックをプレゼンテーション層に直接埋め込む方法があります (web アプリケーションでは、ASP.NET ページがプレゼンテーション層を構成します)。 これは、ASP.NET ページのコード部分で ADO.NET コードを記述したり、マークアップ部分からの SqlDataSource コントロールを使用したりすることがあります。 どちらの場合も、この方法を使用すると、データアクセスロジックがプレゼンテーション層と緊密に結合されます。 ただし、データアクセスロジックをプレゼンテーション層から分離することをお勧めします。 この分離レイヤーは、データアクセス層として使用され、略して DAL は、通常、別個のクラスライブラリプロジェクトとして実装されます。 この多層アーキテクチャのメリットについては、このチュートリアルの最後にある「詳細情報」セクションを参照してください。これらの利点については、このシリーズで説明します。

データベースへの接続の作成、 **SELECT**、 **INSERT**、 **UPDATE**、および**DELETE**コマンドの発行など、基になるデータソースに固有のすべてのコードは、DAL に配置する必要があります。 プレゼンテーション層には、このようなデータアクセスコードへの参照を含めないでください。ただし、すべてのデータ要求に対して DAL を呼び出す必要があります。 通常、データアクセス層には、基になるデータベースデータにアクセスするためのメソッドが含まれています。 たとえば、Northwind データベースには、販売用の製品とそれが属するカテゴリを記録する**products**テーブルと**categories**テーブルがあります。 この DAL では、次のような方法があります。

- **GetCategories ()。** すべてのカテゴリに関する情報が返されます。
- **Getproducts ()。** すべての製品に関する情報が返されます。
- **Getproducts Bycategoryid (*categoryid*)。** 指定されたカテゴリに属するすべての製品を返します。
- **Getproductbyproductid (*productid*)。** 特定の製品に関する情報を返します。

これらのメソッドは、呼び出されると、データベースに接続し、適切なクエリを発行して、結果を返します。 これらの結果を返す方法は重要です。 これらのメソッドは、単にデータベースクエリによって設定されたデータセットまたは DataReader を返すことができますが、これらの結果は、*厳密に型指定*されたオブジェクトを使用して返す必要があります 厳密に型指定されたオブジェクトとは、コンパイル時にスキーマが厳格に定義されているオブジェクトのことです。一方、弱い型指定のオブジェクトとは、スキーマが実行時までわからないことを意味します。

たとえば、DataReader とデータセット (既定では) は、値の設定に使用されるデータベースクエリによって返される列によってスキーマが定義されているため、疎に型指定されたオブジェクトです。 疎型の DataTable から特定の列にアクセスするには、次のような構文を使用する必要があります。  <strong><em>datatable</em>です。Rows [<em>index</em>] ["<em>columnName</em>"]</strong>。 この例では、DataTable の厳密な型指定は、文字列または序数のインデックスを使用して列名にアクセスする必要があることを示しています。 一方、厳密に型指定された DataTable では、それぞれの列がプロパティとして実装され、次のようなコードが作成さ<strong>れます。行 [<em>インデックス</em>]。*columnName</strong>* 。

厳密に型指定されたオブジェクトを返すために、開発者は独自のカスタムビジネスオブジェクトを作成したり、型指定されたデータセットを使用したりできます。 ビジネスオブジェクトは、ビジネスオブジェクトが表す基になるデータベーステーブルの列をプロパティに反映するクラスとして、開発者によって実装されます。 型指定されたデータセットは、データベーススキーマに基づいて Visual Studio によって生成されるクラスであり、そのメンバーはこのスキーマに従って厳密に型指定されます。 型指定されたデータセット自体は、ADO.NET データセット、DataTable、および DataRow クラスを拡張するクラスで構成されています。 厳密に型指定された Datatable に加えて、型指定されたデータセットには Tableadapter も含まれるようになりました。 Tableadapter は、データセットの Datatable にデータを格納し、Datatable 内の変更をデータベースに反映するためのメソッドを持つクラスです。

> [!NOTE]
> 型指定されたデータセットを使用する場合とカスタムビジネスオブジェクトを使用する場合の長所と短所の詳細については、「[データ層コンポーネントの設計」および「階層を介したデータの引き渡し](https://msdn.microsoft.com/library/ms978496.aspx)」を参照してください。

これらのチュートリアルのアーキテクチャには、厳密に型指定されたデータセットを使用します。 図3は、型指定されたデータセットを使用するアプリケーションのさまざまな層間のワークフローを示しています。

[すべてのデータアクセスコードが DAL に作業 ![](creating-a-data-access-layer-cs/_static/image6.png)](creating-a-data-access-layer-cs/_static/image5.png)

**図 3**: すべてのデータアクセスコードが DAL に作業 ([クリックすると、フルサイズの画像が表示](creating-a-data-access-layer-cs/_static/image7.png)されます)

## <a name="creating-a-typed-dataset-and-table-adapter"></a>型指定されたデータセットとテーブルアダプターの作成

DAL の作成を開始するには、まず、型指定されたデータセットをプロジェクトに追加します。 これを行うには、ソリューションエクスプローラーでプロジェクトノードを右クリックし、[新しい項目の追加] を選択します。 テンプレートの一覧から [データセット] オプションを選択し、「 **Northwind. xsd**」という名前を指定します。

[新しいデータセットをプロジェクトに追加することを選択 ![](creating-a-data-access-layer-cs/_static/image9.png)](creating-a-data-access-layer-cs/_static/image8.png)

**図 4**: プロジェクトに新しいデータセットを追加することを選択する ([クリックすると、フルサイズの画像が表示](creating-a-data-access-layer-cs/_static/image10.png)される)

[追加] をクリックした後、データセットを**アプリ\_コード**フォルダーに追加するよう求められたら、[はい] を選択します。 次に、型指定されたデータセットのデザイナーが表示され、TableAdapter 構成ウィザードが開始されます。これにより、最初の TableAdapter を型指定されたデータセットに追加できます。

型指定されたデータセットは、厳密に型指定されたデータのコレクションとして機能します。これは、厳密に型指定された DataTable インスタンスで構成されており、それぞれが厳密に型指定された DataRow インスタンスで構成されています。 ここでは、このチュートリアルシリーズで使用する必要がある基になるデータベーステーブルごとに、厳密に型指定された DataTable を作成します。 **Products**テーブルの DataTable の作成から始めましょう。

厳密に型指定された Datatable には、基になるデータベーステーブルからデータにアクセスする方法に関する情報が含まれていないことに注意してください。 DataTable にデータを設定するためにデータを取得するには、データアクセス層として機能する TableAdapter クラスを使用します。 **製品**の DataTable の場合、TableAdapter には**getproducts ()** 、 **getproductbycategoryid (*categoryid*)** などのメソッドが含まれます。これはプレゼンテーション層から呼び出されます。 DataTable のロールは、レイヤー間でデータを渡すために使用される、厳密に型指定されたオブジェクトとして機能します。

TableAdapter 構成ウィザードでは、最初に、使用するデータベースを選択するように求めるメッセージが表示されます。 ドロップダウンリストには、サーバーエクスプローラー内のそれらのデータベースが表示されます。 Northwind データベースをサーバーエクスプローラーに追加しなかった場合は、この時点で [新しい接続] ボタンをクリックすると、この操作を行うことができます。

[ドロップダウンリストから Northwind データベースを選択 ![には](creating-a-data-access-layer-cs/_static/image12.png)](creating-a-data-access-layer-cs/_static/image11.png)

**図 5**: ドロップダウンリストから Northwind データベースを選択[する (クリックすると、フルサイズの画像が表示](creating-a-data-access-layer-cs/_static/image13.png)されます)

データベースを選択して [次へ] をクリックすると、 **web.config ファイルに**接続文字列を保存するかどうかを確認するメッセージが表示されます。 接続文字列を保存することで、TableAdapter クラスにハードコーディングされないようにすることができます。これにより、接続文字列情報が将来変更された場合の処理が簡単になります。 構成ファイルに接続文字列を保存することを選択した場合は、 **&lt;connectionStrings&gt;** セクションに配置されます。これは、[必要に応じて暗号化](http://aspnet.4guysfromrolla.com/articles/021506-1.aspx)してセキュリティを強化することも、後で IIS GUI 管理ツール内の新しい ASP.NET 2.0 プロパティページを使用して変更することもできます。これは、管理者にとって理想的です。

[接続文字列を web.config に保存 ![には](creating-a-data-access-layer-cs/_static/image15.png)](creating-a-data-access-layer-cs/_static/image14.png)

**図 6**: 接続文字列を Web.config に保存する ([クリックすると、フルサイズの画像が表示](creating-a-data-access-layer-cs/_static/image16.png)され**ます**)

次に、厳密に型指定された最初の DataTable のスキーマを定義し、厳密に型指定されたデータセットを作成するときに TableAdapter で使用する最初のメソッドを指定する必要があります。 この2つの手順は、DataTable に反映するテーブルから列を返すクエリを作成することによって、同時に実行されます。 ウィザードの最後で、このクエリにメソッド名を指定します。 これが完了したら、プレゼンテーション層からこのメソッドを呼び出すことができます。 メソッドは、定義されたクエリを実行し、厳密に型指定された DataTable を設定します。

SQL クエリの定義を開始するには、まず TableAdapter でクエリを発行する方法を指定する必要があります。 アドホック SQL ステートメントを使用するか、新しいストアドプロシージャを作成するか、既存のストアドプロシージャを使用することができます。 これらのチュートリアルでは、アドホック SQL ステートメントを使用します。 ストアドプロシージャの使用例については、 [Brian Noyes](http://briannoyes.net/)の記事「 [Visual Studio 2005 データセットデザイナーを使用してデータアクセス層を構築](http://www.theserverside.net/articles/showarticle.tss?id=DataSetDesigner)する」を参照してください。

[アドホック SQL ステートメントを使用してデータのクエリを実行 ![には](creating-a-data-access-layer-cs/_static/image18.png)](creating-a-data-access-layer-cs/_static/image17.png)

**図 7**: アドホック SQL ステートメントを使用してデータにクエリを実行[する (クリックすると、フルサイズの画像が表示](creating-a-data-access-layer-cs/_static/image19.png)されます)

この時点で、手動で SQL クエリを入力できます。 TableAdapter で最初のメソッドを作成する場合は、通常、対応する DataTable で表現する必要がある列を返すクエリを使用します。 これを実現するには、 **Products**テーブルからすべての列とすべての行を返すクエリを作成します。

[テキストボックスに SQL クエリを入力 ![には](creating-a-data-access-layer-cs/_static/image21.png)](creating-a-data-access-layer-cs/_static/image20.png)

**図 8**: テキストボックスに SQL クエリを入力[する (クリックすると、フルサイズの画像が表示](creating-a-data-access-layer-cs/_static/image22.png)されます)

または、図9に示すように、クエリビルダーを使用し、クエリをグラフィカルに作成します。

[クエリエディターを使用してクエリをグラフィカルに作成 ![には](creating-a-data-access-layer-cs/_static/image24.png)](creating-a-data-access-layer-cs/_static/image23.png)

**図 9**: クエリエディターを使用してクエリをグラフィカルに作成[する (クリックしてフルサイズのイメージを表示する](creating-a-data-access-layer-cs/_static/image25.png))

クエリを作成した後、次の画面に移動する前に、[詳細オプション] ボタンをクリックします。 Web サイトプロジェクトでは、[Insert、Update、および Delete ステートメントの生成] が既定で選択されている唯一の詳細設定オプションです。クラスライブラリまたは Windows プロジェクトからこのウィザードを実行する場合は、[オプティミスティック同時実行制御を使用する] オプションも選択されます。 ここでは、[オプティミスティック同時実行制御を使用する] オプションをオフのままにします。 オプティミスティック同時実行制御については、今後のチュートリアルで確認します。

[![[Insert、Update、および Delete ステートメントを生成する] オプションのみを選択します。](creating-a-data-access-layer-cs/_static/image27.png)](creating-a-data-access-layer-cs/_static/image26.png)

**図 10**: [Insert、Update、および Delete ステートメントを生成する] オプションのみを選択[する (クリックすると、フルサイズの画像が表示](creating-a-data-access-layer-cs/_static/image28.png)されます)

詳細設定オプションを確認したら、[次へ] をクリックして最後の画面に進みます。 ここでは、TableAdapter に追加するメソッドを選択するよう求められます。 データの読み込みには、次の2つのパターンがあります。

- この方法で DataTable にデータを**格納**します。 datatable をパラメーターとして受け取り、クエリの結果に基づいてデータを設定するメソッドが作成されます。 たとえば、ADO.NET DataAdapter クラスは、このパターンを**Fill ()** メソッドと共に実装します。
- この方法で**datatable を返し**ます。メソッドは datatable を作成してデータを格納し、メソッドの戻り値として返します。

TableAdapter では、これらのパターンのいずれかまたは両方を実装できます。 ここで指定したメソッドの名前を変更することもできます。 両方のチェックボックスをオンのままにしておきますが、これらのチュートリアルでは後者のパターンのみを使用します。 また、代わりに汎用の**GetData**メソッドを**getproducts**に変更してみましょう。

オンにすると、最後のチェックボックス "GenerateDBDirectMethods" によって、TableAdapter の**Insert ()** 、 **Update ()** 、および**Delete ()** の各メソッドが作成されます。 このオプションをオフのままにした場合、すべての更新は、型指定されたデータセット、DataTable、単一の DataRow、または Datarow の配列を受け取る TableAdapter の唯一の**Update ()** メソッドを使用して実行する必要があります。 (図9の詳細プロパティから [Insert、Update、および Delete ステートメントを生成する] オプションをオフにした場合、このチェックボックスの設定は効果がありません)。このチェックボックスはオンのままにしておきます。

[メソッド名を GetData から GetProducts に変更 ![には](creating-a-data-access-layer-cs/_static/image30.png)](creating-a-data-access-layer-cs/_static/image29.png)

**図 11**: メソッド名を**GetData**から**getproducts**に変更する ([クリックすると、フルサイズの画像が表示](creating-a-data-access-layer-cs/_static/image31.png)されます)

[完了] をクリックしてウィザードを完了します。 ウィザードを閉じると、先ほど作成した DataTable を示すデータセットデザイナーに戻ります。 **Products** DataTable (**ProductID**、 **ProductName**など) の列の一覧に加えて、 **ProductsTableAdapter** (**Fill ()** および**getproducts ()** ) のメソッドも表示されます。

[![Products DataTable と ProductsTableAdapter が、型指定されたデータセットに追加されました。](creating-a-data-access-layer-cs/_static/image33.png)](creating-a-data-access-layer-cs/_static/image32.png)

**図 12**: **Products** DataTable と**ProductsTableAdapter**が型指定されたデータセットに追加された (クリックすると、[フルサイズの画像が表示](creating-a-data-access-layer-cs/_static/image34.png)されます)

この時点で、1つの DataTable (**Northwind products**) と、 **getproducts ()** メソッドを使用した厳密に型指定された DataAdapter クラス (**NorthwindTableAdapters**) を持つ型指定されたデータセットがあります。 これらのオブジェクトを使用して、次のようなコードからすべての製品の一覧にアクセスできます。

[!code-html[Main](creating-a-data-access-layer-cs/samples/sample1.html)]

このコードでは、データアクセス固有のコードを1ビット記述する必要はありませんでした。 ADO.NET クラスをインスタンス化する必要はありませんでした。接続文字列、SQL クエリ、またはストアドプロシージャを参照する必要はありませんでした。 代わりに、TableAdapter によって、低レベルのデータアクセスコードが提供されます。

この例で使用される各オブジェクトも厳密に型指定されているため、Visual Studio で IntelliSense とコンパイル時の型チェックを行うことができます。 また、TableAdapter によって返されるすべての Datatable を ASP.NET データ Web コントロール (GridView、DetailsView、DropDownList、CheckBoxList など) にバインドすることもできます。 次の例は、 **Getproducts ()** メソッドによって返される DataTable を、scan Load イベントハンドラーの **\_ページ**内の3行のコードだけで GridView にバインドする方法を示しています。

AllProducts .aspx

[!code-aspx[Main](creating-a-data-access-layer-cs/samples/sample2.aspx)]

AllProducts.aspx.cs

[!code-csharp[Main](creating-a-data-access-layer-cs/samples/sample3.cs)]

[製品の一覧が GridView に表示される ![](creating-a-data-access-layer-cs/_static/image36.png)](creating-a-data-access-layer-cs/_static/image35.png)

**図 13**: 製品の一覧が GridView に表示される ([クリックすると、フルサイズの画像が表示](creating-a-data-access-layer-cs/_static/image37.png)されます)

この例では、ASP.NET ページの**ページ\_Load**イベントハンドラーに3行のコードを記述する必要がありましたが、今後のチュートリアルでは、ObjectDataSource を使用して DAL からデータを宣言によって取得する方法を確認します。 ObjectDataSource を使用すると、コードを記述する必要がなくなり、ページングや並べ替えもサポートされます。

## <a name="step-3-adding-parameterized-methods-to-the-data-access-layer"></a>手順 3: データアクセス層へのパラメーター化されたメソッドの追加

この時点で、 **ProductsTableAdapter**クラスには、 **getproducts ()** という1つのメソッドがあります。このメソッドは、データベース内のすべての製品を返します。 すべての製品を使用できるということは確かに便利ですが、特定の製品、または特定のカテゴリに属するすべての製品に関する情報を取得することが必要になる場合もあります。 データアクセス層にこのような機能を追加するには、パラメーター化されたメソッドを TableAdapter に追加します。

ここで、 **Get$ Bycategoryid (*categoryid*)** メソッドを追加します。 DAL に新しいメソッドを追加するには、データセットデザイナーに戻り、 **[ProductsTableAdapter]** セクションを右クリックして、[クエリの追加] を選択します。

![TableAdapter を右クリックし、[クエリの追加] を選択します。](creating-a-data-access-layer-cs/_static/image38.png)

**図 14**: TableAdapter を右クリックし、[クエリの追加] を選択する

まず、アドホック SQL ステートメントまたは新規または既存のストアドプロシージャを使用してデータベースにアクセスするかどうかを確認するメッセージが表示されます。 アドホック SQL ステートメントをもう一度使用してみましょう。 次に、使用する SQL クエリの種類を尋ねられます。 指定されたカテゴリに属するすべての製品を返す必要があるため、行を返す**SELECT**ステートメントを記述します。

[行を返す SELECT ステートメントの作成を選択 ![には](creating-a-data-access-layer-cs/_static/image40.png)](creating-a-data-access-layer-cs/_static/image39.png)

**図 15**: 行を返す**SELECT**ステートメントの作成を選択する ([クリックすると、フルサイズの画像が表示](creating-a-data-access-layer-cs/_static/image41.png)されます)

次の手順では、データへのアクセスに使用する SQL クエリを定義します。 特定のカテゴリに属する製品のみを返すようにするため、 <strong>Getproducts ()</strong>と同じ<strong>SELECT</strong>ステートメントを使用しますが、次の<strong>where</strong>句を追加します。ここで、 <strong>CategoryID = @CategoryID</strong>です。 <strong>@CategoryID</strong>パラメーターは、作成するメソッドが、対応する型 (つまり、null 許容の整数) の入力パラメーターを必要とすることを TableAdapter ウィザードに示します。

[指定したカテゴリの製品のみを返すクエリを入力 ![](creating-a-data-access-layer-cs/_static/image43.png)](creating-a-data-access-layer-cs/_static/image42.png)

**図 16**: 指定したカテゴリの製品のみを返すクエリを入力する ([クリックすると、フルサイズの画像が表示](creating-a-data-access-layer-cs/_static/image44.png)されます)

最後の手順では、使用するデータアクセスパターンを選択したり、生成されるメソッドの名前をカスタマイズしたりすることができます。 Fill パターンの場合は、名前を<strong>Fillbycategoryid</strong>に変更し、DataTable return パターン ( <strong>Get*X</strong>* メソッド) を返すには、 <strong>get$ bycategoryid</strong>を使用します。

[TableAdapter メソッドの名前を選択 ![には](creating-a-data-access-layer-cs/_static/image46.png)](creating-a-data-access-layer-cs/_static/image45.png)

**図 17**: TableAdapter メソッドの名前を選択する ([クリックすると、フルサイズの画像が表示](creating-a-data-access-layer-cs/_static/image47.png)されます)

ウィザードを完了すると、データセットデザイナーに新しい TableAdapter メソッドが追加されます。

![これで、製品のカテゴリ別にクエリを実行できるようになりました](creating-a-data-access-layer-cs/_static/image48.png)

**図 18**: カテゴリ別に製品を照会できるようになりました。

同じ手法を使用して**Getproductbyproductid (*productID*)** メソッドを追加してみましょう。

これらのパラメーター化クエリは、データセットデザイナーから直接テストできます。 TableAdapter のメソッドを右クリックし、[データのプレビュー] を選択します。 次に、パラメーターに使用する値を入力し、[プレビュー] をクリックします。

[飲料カテゴリに属する製品 ![が表示されます。](creating-a-data-access-layer-cs/_static/image50.png)](creating-a-data-access-layer-cs/_static/image49.png)

**図 19**: 飲み物カテゴリに属する製品が表示されます ([クリックすると、フルサイズの画像が表示](creating-a-data-access-layer-cs/_static/image51.png)されます)

DAL の**Getproducts Bycategoryid (*categoryID*)** メソッドを使用して、指定したカテゴリの製品のみを表示する ASP.NET ページを作成できるようになりました。 次の例では、飲料カテゴリに含まれるすべての製品を示しています。このカテゴリには、 **CategoryID**が1です。

飲み物

[!code-aspx[Main](creating-a-data-access-layer-cs/samples/sample4.aspx)]

Beverages.aspx.cs

[!code-csharp[Main](creating-a-data-access-layer-cs/samples/sample5.cs)]

[[飲料] カテゴリの製品 ![表示されます。](creating-a-data-access-layer-cs/_static/image53.png)](creating-a-data-access-layer-cs/_static/image52.png)

**図 20**: 飲料カテゴリのこれらの製品が表示される ([クリックすると、フルサイズの画像が表示](creating-a-data-access-layer-cs/_static/image54.png)されます)

## <a name="step-4-inserting-updating-and-deleting-data"></a>手順 4: データの挿入、更新、および削除

データの挿入、更新、および削除には、一般的に使用される2つのパターンがあります。 最初のパターンでは、データベースダイレクトパターンを呼び出します。このパターンでは、呼び出されたときに、1つのデータベースレコードで動作するデータベースに対して**INSERT**、 **UPDATE**、または**DELETE**コマンドを発行するメソッドを作成します。 通常、このようなメソッドは、挿入、更新、または削除する値に対応する一連のスカラー値 (整数、文字列、ブール値、DateTimes など) で渡されます。 たとえば、 **Products**テーブルに対してこのパターンを使用した場合、delete メソッドは、削除するレコードの**ProductID**を示す整数パラメーターを受け取ります。一方、Insert メソッドは、 **ProductName**の文字列、 **UnitPrice**の10進数、 **UnitsOnStock**の整数などを受け取ります。

[挿入、更新、および削除の各要求がデータベースに直ちに送信さ ![](creating-a-data-access-layer-cs/_static/image56.png)](creating-a-data-access-layer-cs/_static/image55.png)

**図 21**: 挿入、更新、および削除の各要求がすぐにデータベースに送信される ([クリックすると、フルサイズの画像が表示](creating-a-data-access-layer-cs/_static/image57.png)されます)

もう1つのパターン (バッチ更新パターンと呼ばれます) は、1つのメソッド呼び出しでデータセット、DataTable、または Datarow のコレクション全体を更新することです。 このパターンでは、開発者が DataTable 内の Datarow を削除、挿入、変更し、それらの Datarow または DataTable を update メソッドに渡します。 このメソッドは、渡された Datarow を列挙し、変更、追加、または削除された (DataRow の[RowState プロパティ](https://msdn.microsoft.com/library/system.data.datarow.rowstate.aspx)値を使用して) かどうかを判断し、各レコードに対して適切なデータベース要求を発行します。

[更新メソッドが呼び出されたときに、すべての変更がデータベースと同期さ ![](creating-a-data-access-layer-cs/_static/image59.png)](creating-a-data-access-layer-cs/_static/image58.png)

**図 22**: 更新メソッドが呼び出されたときにすべての変更がデータベースと同期される ([クリックしてフルサイズの画像を表示する](creating-a-data-access-layer-cs/_static/image60.png))

TableAdapter では、既定でバッチ更新パターンが使用されますが、DB direct パターンもサポートされています。 TableAdapter の作成時に詳細プロパティから [Insert、Update、Delete ステートメントの生成] オプションを選択したため、 **ProductsTableAdapter**には、バッチ更新パターンを実装する**update ()** メソッドが含まれています。 具体的には、TableAdapter には、型指定されたデータセット、厳密に型指定された DataTable、または1つ以上の Datarow に渡すことができる**Update ()** メソッドが含まれています。 最初に TableAdapter を作成するときに [GenerateDBDirectMethods] チェックボックスをオンにした場合、 **Insert ()** 、 **Update ()** 、および**Delete ()** の各メソッドを使用して DB direct パターンも実装されます。

どちらのデータ変更パターンでも、TableAdapter の**InsertCommand**、 **UpdateCommand**、および**DeleteCommand**プロパティを使用して、 **INSERT**、 **UPDATE**、および**DELETE**コマンドをデータベースに発行します。 データセットデザイナーで TableAdapter をクリックし、プロパティウィンドウに移動することで、 **InsertCommand**、 **UpdateCommand**、および**DeleteCommand**の各プロパティを確認および変更できます。 (TableAdapter が選択されていること、および**ProductsTableAdapter**オブジェクトがプロパティウィンドウのドロップダウンリストで選択されていることを確認してください)。

[TableAdapter に InsertCommand、UpdateCommand、および DeleteCommand プロパティがある ![](creating-a-data-access-layer-cs/_static/image62.png)](creating-a-data-access-layer-cs/_static/image61.png)

**図 23**: TableAdapter には**InsertCommand**、 **UpdateCommand**、および**DeleteCommand**プロパティがあります ([クリックすると、フルサイズの画像が表示](creating-a-data-access-layer-cs/_static/image63.png)されます)

これらのデータベースコマンドのプロパティのいずれかを確認または変更するには、 **CommandText**サブプロパティをクリックします。これにより、クエリビルダーが表示されます。

[クエリビルダーで INSERT、UPDATE、および DELETE ステートメントを構成 ![には](creating-a-data-access-layer-cs/_static/image65.png)](creating-a-data-access-layer-cs/_static/image64.png)

**図 24**: クエリビルダーで**INSERT**、 **UPDATE**、および**DELETE**ステートメントを構成する ([クリックすると、フルサイズの画像が表示](creating-a-data-access-layer-cs/_static/image66.png)されます)

次のコード例では、バッチ更新パターンを使用して、廃止されておらず、25単位の在庫があるすべての製品の価格を2倍にする方法を示します。

[!code-csharp[Main](creating-a-data-access-layer-cs/samples/sample6.cs)]

次のコードは、DB ダイレクトパターンを使用して、プログラムで特定の製品を削除してから更新し、新しい製品を追加する方法を示しています。

[!code-csharp[Main](creating-a-data-access-layer-cs/samples/sample7.cs)]

## <a name="creating-custom-insert-update-and-delete-methods"></a>カスタムの Insert、Update、および Delete メソッドの作成

DB ダイレクトメソッドによって作成される**Insert ()** 、 **Update ()** 、および**Delete ()** の各メソッドは、特に多くの列を持つテーブルでは、少し面倒な場合があります。 前のコード例では、IntelliSense のヘルプを使用せずに、 **Update ()** および**Insert ()** の各メソッドに対して各入力パラメーターにマップされている**Products**テーブル列は特に明確ではありません。 1つまたは2つの列のみを更新する必要がある場合や、新しく挿入されたレコードの**id** (自動インクリメント) フィールドの値を返すようにカスタマイズされた**Insert ()** メソッドが必要な場合があります。

このようなカスタムメソッドを作成するには、データセットデザイナーに戻ります。 TableAdapter を右クリックし、[クエリの追加] を選択して、TableAdapter ウィザードに戻ります。 2番目の画面では、作成するクエリの種類を指定できます。 新しい製品を追加し、新しく追加したレコードの**ProductID**の値を返すメソッドを作成してみましょう。 そのため、**挿入**クエリを作成することを選択します。

[Products テーブルに新しい行を追加するメソッドを作成 ![には](creating-a-data-access-layer-cs/_static/image68.png)](creating-a-data-access-layer-cs/_static/image67.png)

**図 25**: **Products**テーブルに新しい行を追加するメソッドを作成する ([クリックすると、フルサイズの画像が表示](creating-a-data-access-layer-cs/_static/image69.png)されます)

次の画面で、 **InsertCommand**の**CommandText**が表示されます。 クエリの最後に**SELECT SCOPE\_identity ()** を追加することによって、このクエリを拡張します。これにより、同じスコープ内の**id**列に挿入された最後の id 値が返されます。 (**スコープ\_id ()** の詳細と、 [@@IDENTITYの代わりに scope\_identity () を使用](http://weblogs.sqlteam.com/travisl/archive/2003/10/29/405.aspx)する理由の詳細については、[技術ドキュメント](https://msdn.microsoft.com/library/ms190315.aspx)を参照してください。**SELECT**ステートメントを追加する前に、必ずセミコロンで**挿入**ステートメントを終了してください。

[SCOPE_IDENTITY () 値を返すようにクエリを拡張 ![](creating-a-data-access-layer-cs/_static/image71.png)](creating-a-data-access-layer-cs/_static/image70.png)

**図 26**:**スコープ\_IDENTITY ()** 値を返すようにクエリを拡張する ([クリックしてフルサイズのイメージを表示する](creating-a-data-access-layer-cs/_static/image72.png))

最後に、新しいメソッドに**Insertproduct**という名前を指定します。

[新しいメソッド名を InsertProduct に設定 ![](creating-a-data-access-layer-cs/_static/image74.png)](creating-a-data-access-layer-cs/_static/image73.png)

**図 27**: 新しいメソッド名を**insertproduct**に設定する ([クリックすると、フルサイズの画像が表示](creating-a-data-access-layer-cs/_static/image75.png)されます)

データセットデザイナーに戻ると、 **ProductsTableAdapter**に新しいメソッド**insertproduct**が含まれていることがわかります。 この新しいメソッドに**Products**テーブル内の各列のパラメーターがない場合、**挿入**ステートメントをセミコロンで終了することを忘れた可能性があります。 **Insertproduct**メソッドを構成し、 **INSERT**ステートメントと**SELECT**ステートメントをセミコロンで区切るようにします。

既定では、insert メソッドはクエリ以外のメソッドを発行します。つまり、影響を受ける行の数を返すことを意味します。 ただし、 **Insertproduct**メソッドでは、クエリによって返された値を返し、影響を受けた行数は返さないようにする必要があります。 これを実現するには、 **Insertproduct**メソッドの**executemode**プロパティを**スカラー**に調整します。

[ExecuteMode プロパティをスカラーに変更 ![には](creating-a-data-access-layer-cs/_static/image77.png)](creating-a-data-access-layer-cs/_static/image76.png)

**図 28**: **executemode**プロパティを**スカラー**に変更する ([クリックすると、フルサイズの画像が表示](creating-a-data-access-layer-cs/_static/image78.png)されます)

次のコードは、この新しい**Insertproduct**メソッドの動作を示しています。

[!code-csharp[Main](creating-a-data-access-layer-cs/samples/sample8.cs)]

## <a name="step-5-completing-the-data-access-layer"></a>手順 5: データアクセス層を完成させる

**ProductsTableAdapters**クラスは**Products**テーブルから**CategoryID**および**仕入**先の値を返しますが、 **Categories**テーブルまたは**仕入先**テーブルの**CompanyName**列の [**区分**値] 列は含まれていませんが、これらは製品情報を表示するときに表示する列である可能性があることに注意してください。 TableAdapter の初期メソッド**Getproducts ()** を拡張して、 **[区分]** 値 と **[CompanyName]** の両方の列の値を含めることができます。これにより、これらの新しい列が含まれるように、厳密に型指定された DataTable が更新されます。

ただし、この方法では、データの挿入、更新、および削除の TableAdapter のメソッドがこの初期の方法に基づいているため、問題が発生する可能性があります。 幸い、挿入、更新、および削除のための自動生成されたメソッドは、 **SELECT**句のサブクエリの影響を受けません。 **結合**を使用するのではなく、**カテゴリ**や**サプライヤー**にクエリをサブクエリとして追加することで、データを変更するためにこれらのメソッドを再作成する必要がなくなります。 **ProductsTableAdapter**の**getproducts ()** メソッドを右クリックし、[構成] を選択します。 次に、 **SELECT**句を次のように調整します。

[!code-sql[Main](creating-a-data-access-layer-cs/samples/sample9.sql)]

[GetProducts () メソッドの SELECT ステートメントを ![更新します。](creating-a-data-access-layer-cs/_static/image80.png)](creating-a-data-access-layer-cs/_static/image79.png)

**図 29**: **getproducts ()** メソッドの**SELECT**ステートメントを更新する ([クリックすると、フルサイズの画像が表示](creating-a-data-access-layer-cs/_static/image81.png)されます)

**Getproducts ()** メソッドを更新してこの新しいクエリを使用すると、DataTable に2つの新しい列 (**区分**テーブルと**SupplierName**) が追加されます。

![Products DataTable には2つの新しい列があります。](creating-a-data-access-layer-cs/_static/image82.png)

**図 30**: **Products** DataTable に2つの新しい列がある

**Get$ Bycategoryid (*categoryID*)** メソッドの**SELECT**句も更新します。

**Getproducts ()** を更新する場合は、[ **JOIN**構文を使用する **] を選択**すると、データセットデザイナーで DB direct パターンを使用してデータベースデータの挿入、更新、および削除を行うためのメソッドを自動生成できなくなります。 代わりに、このチュートリアルの前の「 **Insertproduct**メソッド」で行ったのと同じように手動で作成する必要があります。 さらに、バッチ更新パターンを使用する場合は、手動で**InsertCommand**、 **UpdateCommand**、および**DeleteCommand**プロパティの値を指定する必要があります。

## <a name="adding-the-remaining-tableadapters"></a>残りの Tableadapter の追加

これまでは、1つのデータベーステーブルに対して1つの TableAdapter を操作するだけでした。 ただし、Northwind データベースには、web アプリケーションで使用する必要がある関連テーブルがいくつか含まれています。 型指定されたデータセットには、関連する複数の Datatable を含めることができます。 そのため、DAL を完了するには、これらのチュートリアルで使用する他のテーブルの Datatable を追加する必要があります。 型指定されたデータセットに新しい TableAdapter を追加するには、データセットデザイナーを開き、デザイナーで右クリックして、[追加/TableAdapter] を選択します。 これにより、新しい DataTable と TableAdapter が作成され、このチュートリアルの前半で説明したウィザードが表示されます。

次のクエリを使用して、次の Tableadapter とメソッドを作成します。 **ProductsTableAdapter**のクエリには、各製品のカテゴリ名と仕入先名を取得するサブクエリが含まれていることに注意してください。 また、 **ProductsTableAdapter**クラスの**getproducts ()** メソッドと**getproducts bycategoryid (*categoryid*)** メソッドを既に追加してある場合もあります。

- **ProductsTableAdapter**

  - **Getproducts**: 

      [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample10.sql)]
  - **Get製品 Bycategoryid**: 

      [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample11.sql)]
  - **Get製品 By仕入**先: 

      [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample12.sql)]
  - **Getproductbyproductid**: 

      [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample13.sql)]
- **CategoriesTableAdapter**

  - **GetCategories**: 

      [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample14.sql)]
  - **Getカテゴリ Bycategoryid**: 

      [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample15.sql)]
- **SuppliersTableAdapter**

  - **Getsuppliers**: 

      [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample16.sql)]
  - **GetSuppliersByCountry**: 

      [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample17.sql)]
  - **GetSupplierBySupplierID**: 

      [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample18.sql)]
- **EmployeesTableAdapter**

  - **GetEmployees**: 

      [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample19.sql)]
  - **GetEmployeesByManager**: 

      [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample20.sql)]
  - **GetEmployeeByEmployeeID**: 

      [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample21.sql)]

[4つの Tableadapter が追加された後のデータセットデザイナーの ![](creating-a-data-access-layer-cs/_static/image84.png)](creating-a-data-access-layer-cs/_static/image83.png)

**図 31**: 4 つの Tableadapter を追加した後のデータセットデザイナー ([クリックすると、フルサイズのイメージが表示](creating-a-data-access-layer-cs/_static/image85.png)されます)

## <a name="adding-custom-code-to-the-dal"></a>DAL へのカスタムコードの追加

型指定されたデータセットに追加された Tableadapter と Datatable は、XML スキーマ定義ファイル (**Northwind .xsd**) として表現されます。 このスキーマ情報を表示するには、ソリューションエクスプローラーで**Northwind .xsd**ファイルを右クリックし、[コードの表示] を選択します。

[Northwinds 型指定されたデータセットの XML スキーマ定義 (XSD) ファイルの ![](creating-a-data-access-layer-cs/_static/image87.png)](creating-a-data-access-layer-cs/_static/image86.png)

**図 32**: Northwinds に型指定されたデータセットの XML スキーマ定義 (XSD) ファイル ([クリックすると、フルサイズの画像が表示](creating-a-data-access-layer-cs/_static/image88.png)されます)

このスキーマ情報は、コンパイルC#時または実行時 (必要な場合) に、デザイン時にコードに変換または Visual Basic します。その時点でデバッガーでステップスルーすることができます。 この自動生成されたコードを表示するには、クラスビューに移動し、TableAdapter または型指定されたデータセットクラスにドリルダウンします。 画面にクラスビューが表示されない場合は、[表示] メニューに移動し、そこから選択するか、Ctrl + Shift + C キーを押します。 クラスビューから、型指定されたデータセットと TableAdapter クラスのプロパティ、メソッド、およびイベントを確認できます。 特定のメソッドのコードを表示するには、クラスビューでメソッド名をダブルクリックするか、それを右クリックして [定義へのジャンプ] を選択します。

![[定義へのジャンプ] を選択して、自動生成されたコードを調べクラスビュー](creating-a-data-access-layer-cs/_static/image89.png)

**図 33**: [クラスビューからの定義へのジャンプ] を選択して、自動生成されたコードを検査する

自動生成されるコードは、かなりの時間の節約になりますが、多くの場合、コードは非常に一般的であり、アプリケーションの固有のニーズを満たすようにカスタマイズする必要があります。 ただし、自動生成されたコードを拡張するリスクは、コードを生成したツールによって "再生成" され、カスタマイズが上書きされる可能性があるということです。 .NET 2.0 の新しい部分クラスの概念を使用すると、複数のファイルにクラスを簡単に分割できます。 これにより、Visual Studio によるカスタマイズの上書きを気にせずに、独自のメソッド、プロパティ、およびイベントを自動生成されたクラスに追加できます。

DAL をカスタマイズする方法を示すために、 **Getproducts ()** メソッドを**SuppliersRow**クラスに追加してみましょう。 **SuppliersRow**クラスは、**仕入先**テーブル内の1つのレコードを表します。各供給業者は、プロバイダーをゼロにすることができます。したがって、 **Getproducts ()** は、指定された仕入先の製品を返します。 これを実現するには、 **SuppliersRow.cs**という名前の新しいクラスファイルを**アプリ\_コード**フォルダーに作成し、次のコードを追加します。

[!code-csharp[Main](creating-a-data-access-layer-cs/samples/sample22.cs)]

この部分クラスは、定義した**Getproducts ()** メソッドを含めるように**SuppliersRow**クラスをビルドするときに、コンパイラに指示します。 プロジェクトをビルドし、クラスビューに戻ると、 **SuppliersRow**のメソッドとして**getproducts ()** が表示されるようになります。

![GetProducts () メソッドが SuppliersRow クラスの一部になりました。](creating-a-data-access-layer-cs/_static/image90.png)

**図 34**: **getproducts ()** メソッドが、 **SuppliersRow**クラスの一部になっている

次のコードに示すように、 **Getproducts ()** メソッドを使用して、特定の業者の製品セットを列挙できるようになりました。

[!code-html[Main](creating-a-data-access-layer-cs/samples/sample23.html)]

このデータは、任意の ASP で表示することもできます。NET のデータ Web コントロール。 次のページでは、GridView コントロールと2つのフィールドが使用されています。

- 各業者の名前を表示する BoundField
- 各仕入先の**Getproducts ()** メソッドによって返される結果にバインドされる BulletedList コントロールを含む TemplateField。

このようなマスター/詳細レポートを今後のチュートリアルで表示する方法について説明します。 ここでは、この例は、 **SuppliersRow**クラスに追加されたカスタムメソッドの使用方法を示すように設計されています。

SuppliersAndProducts

[!code-aspx[Main](creating-a-data-access-layer-cs/samples/sample24.aspx)]

SuppliersAndProducts.aspx.cs

[!code-csharp[Main](creating-a-data-access-layer-cs/samples/sample25.cs)]

[仕入先の会社名が左側の列に一覧表示されている ![、右側に製品が表示されます。](creating-a-data-access-layer-cs/_static/image92.png)](creating-a-data-access-layer-cs/_static/image91.png)

**図 35**: 仕入先の会社名が左側の列に一覧表示され、右側に製品が表示される ([クリックすると、フルサイズの画像が表示](creating-a-data-access-layer-cs/_static/image93.png)されます)

## <a name="summary"></a>まとめ

Web アプリケーションを構築する場合、DAL は、プレゼンテーション層の作成を開始する前に最初に実行する手順の1つである必要があります。 Visual Studio では、型指定されたデータセットに基づいて DAL を作成するタスクは、コード行を記述しなくても10-15 分で実現できます。 前のチュートリアルでは、この DAL を基にしています。 次の[チュートリアル](creating-a-business-logic-layer-cs.md)では、さまざまなビジネスルールを定義し、それらを個別のビジネスロジックレイヤーに実装する方法について説明します。

プログラミングを楽しんでください。

## <a name="further-reading"></a>関連項目

このチュートリアルで説明しているトピックの詳細については、次のリソースを参照してください。

- [VS 2005 および ASP.NET 2.0 での厳密に型指定された Tableadapter と Datatable を使用した DAL の構築](https://weblogs.asp.net/scottgu/435498)
- [データ層コンポーネントの設計と層によるデータの受け渡し](https://msdn.microsoft.com/library/ms978496.aspx)
- [Visual Studio 2005 データセットデザイナーを使用してデータアクセス層を構築する](http://www.theserverside.net/articles/showarticle.tss?id=DataSetDesigner)
- [ASP.NET 2.0 アプリケーションの構成情報の暗号化](http://aspnet.4guysfromrolla.com/articles/021506-1.aspx)
- [TableAdapter の概要](https://msdn.microsoft.com/library/bz9tthwx.aspx)
- [型指定されたデータセットの操作](https://msdn.microsoft.com/library/esbykkzb.aspx)
- [Visual Studio 2005 および ASP.NET 2.0 での厳密に型指定されたデータアクセスの使用](http://aspnet.4guysfromrolla.com/articles/020806-1.aspx)
- [TableAdapter メソッドを拡張する方法](https://blogs.msdn.com/vbteam/archive/2005/05/04/ExtendingTableAdapters.aspx)
- [ストアドプロシージャからスカラーデータを取得する](http://aspnet.4guysfromrolla.com/articles/062905-1.aspx)

### <a name="video-training-on-topics-contained-in-this-tutorial"></a>このチュートリアルに含まれるトピックのビデオトレーニング

- [ASP.NET アプリケーションのデータ アクセス層](../../../videos/data-access/adonet-data-services/data-access-layers-in-aspnet-applications.md)
- [データセットを Datagrid に手動でバインドする方法](../../../videos/data-access/adonet-data-services/how-to-manually-bind-a-dataset-to-a-datagrid.md)
- [ASP アプリケーションからデータセットとフィルターを操作する方法](../../../videos/data-access/adonet-data-services/how-to-work-with-datasets-and-filters-from-an-asp-application.md)

## <a name="about-the-author"></a>作成者について

1998以来、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)は 7 asp/創設者 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)の執筆者であり、Microsoft Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 2.0 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 mitchell@4GuysFromRolla.comでアクセスでき[ます。](mailto:mitchell@4GuysFromRolla.com) または彼のブログを参照してください。これは[http://ScottOnWriting.NET](http://ScottOnWriting.NET)にあります。

## <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビュー担当者は、Ron Green、Hilton Giesenow、Patterson が、Liz Shulok、Abel Gomez、および Carlos Santos でした。 今後の MSDN 記事を確認することに興味がありますか? その場合は、mitchell@4GuysFromRolla.comの行を削除[します。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [次へ](creating-a-business-logic-layer-cs.md)
