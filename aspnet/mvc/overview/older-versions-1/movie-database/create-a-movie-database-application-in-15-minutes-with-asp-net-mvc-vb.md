---
uid: mvc/overview/older-versions-1/movie-database/create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb
title: ASP.NET MVC を使用して15分でムービーデータベースアプリケーションを作成する (VB) |Microsoft Docs
author: StephenWalther
description: Stephen Walther は、データベース主導型の ASP.NET MVC アプリケーション全体を最初から最後までビルドします。 このチュートリアルは、新たに導入されたユーザーのためのすばらしい概要です...
ms.author: riande
ms.date: 01/27/2009
ms.assetid: e4ba9786-734c-4eb3-91bb-089793325d0d
msc.legacyurl: /mvc/overview/older-versions-1/movie-database/create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb
msc.type: authoredcontent
ms.openlocfilehash: 0ce8161d29a8ab4005e2b20462b08c9e10ee815a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78435772"
---
# <a name="create-a-movie-database-application-in-15-minutes-with-aspnet-mvc-vb"></a>ASP.NET MVC を使用し、映画データベース アプリケーションを 15 分で作成する (VB)

[Stephen Walther](https://github.com/StephenWalther)

[コードのダウンロード](https://download.microsoft.com/download/7/2/8/728F8794-E59A-4D18-9A56-7AD2DB05BD9D/MovieApp_VB.zip)

> Stephen Walther は、データベース主導型の ASP.NET MVC アプリケーション全体を最初から最後までビルドします。 このチュートリアルは、ASP.NET MVC フレームワークを初めて使用し、ASP.NET MVC アプリケーションを構築するプロセスを理解したい方を対象とした、すばらしい概要です。

このチュートリアルの目的は、ASP.NET MVC アプリケーションを構築するための "何がいいか" という意味を持つことです。 このチュートリアルでは、ASP.NET MVC アプリケーション全体を最初から最後まで構築します。 ここでは、データベースレコードを一覧表示、作成、および編集する方法を示す単純なデータベースドリブンアプリケーションを構築する方法について説明します。

アプリケーションの構築プロセスを簡略化するために、Visual Studio 2008 のスキャフォールディング機能を活用します。 ここでは、コントローラー、モデル、およびビューの初期コードとコンテンツを Visual Studio で生成します。

Active Server のページや ASP.NET を使用していた場合は、ASP.NET MVC が非常に使い慣れていることがわかります。 ASP.NET MVC ビューは、Active Server Pages アプリケーションのページとよく似ています。 また、従来の ASP.NET Web フォームアプリケーションと同様に、ASP.NET MVC では、.NET framework に用意されている豊富な言語およびクラスのセットへのフルアクセスを提供しています。

このチュートリアルでは、ASP.NET MVC アプリケーションの構築エクスペリエンスが、Active Server ページまたは ASP.NET Web フォームアプリケーションを構築する場合と似ているかどうかについての理解を深めることをお勧めします。

## <a name="overview-of-the-movie-database-application"></a>ムービーデータベースアプリケーションの概要

私たちの目標は単純なものを保持することであるため、非常に単純なムービーデータベースアプリケーションを構築します。 この単純なムービーデータベースアプリケーションでは、次の3つのことを実行できます。

1. 一連のムービーデータベースレコードを一覧表示する
2. 新しいムービーデータベースレコードを作成する
3. 既存のムービーデータベースレコードを編集する

ここでも、単純なものを保持する必要があるため、アプリケーションの構築に必要な ASP.NET MVC フレームワークの最小限の機能を活用します。 たとえば、テスト駆動開発を利用することはできません。

アプリケーションを作成するには、次の各手順を実行する必要があります。

1. ASP.NET MVC Web アプリケーションプロジェクトを作成する
2. データベースの作成
3. データベースモデルを作成する
4. ASP.NET MVC コントローラーを作成する
5. ASP.NET MVC ビューを作成する

## <a name="preliminaries"></a>準備

ASP.NET MVC アプリケーションをビルドするには、Visual Studio 2008 または Visual Web Developer 2008 Express が必要です。 また、ASP.NET MVC フレームワークをダウンロードする必要もあります。

Visual Studio 2008 を所有していない場合は、この web サイトから Visual Studio 2008 の90日の試用版をダウンロードできます。

[https://msdn.microsoft.com/vs2008/products/cc268305.aspx](https://msdn.microsoft.com/vs2008/products/cc268305.aspx)

または、Visual Web Developer Express 2008 を使用して ASP.NET MVC アプリケーションを作成することもできます。 Visual Web Developer Express を使用する場合は、Service Pack 1 がインストールされている必要があります。 Visual Web Developer 2008 Express with Service Pack 1 は、次の web サイトからダウンロードできます。

[https://www.microsoft.com/downloads/details.aspx?FamilyId=BDB6391C-05CA-4036-9154-6DF4F6DEBD14&amp;d isplaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyId=BDB6391C-05CA-4036-9154-6DF4F6DEBD14&amp;displaylang=en)

Visual Studio 2008 または Visual Web Developer 2008 をインストールした後、ASP.NET MVC フレームワークをインストールする必要があります。 ASP.NET MVC フレームワークは、次の web サイトからダウンロードできます。

[https://www.asp.net/mvc/](../../../index.md)

> [!NOTE] 
> 
> ASP.NET framework と ASP.NET MVC フレームワークを個別にダウンロードするのではなく、Web Platform Installer を利用できます。 Web Platform Installer は、インストールされているアプリケーションをコンピューターで簡単に管理できるようにするアプリケーションです。
> 
> [https://www.microsoft.com/web/gallery/Install.aspx](https://www.microsoft.com/web/gallery/Install.aspx)

## <a name="creating-an-aspnet-mvc-web-application-project"></a>ASP.NET MVC Web アプリケーションプロジェクトの作成

まず、Visual Studio 2008 で新しい ASP.NET MVC Web アプリケーションプロジェクトを作成します。 メニューオプションファイル **新しいプロジェクト** を選択すると、図1の 新しいプロジェクト ダイアログボックスが表示されます。 プログラミング言語として [Visual Basic] を選択し、[ASP.NET MVC Web アプリケーション] プロジェクトテンプレートを選択します。 プロジェクトに名前を付け、[OK] ボタンをクリックします。

[[新しいプロジェクト] ダイアログボックスの ![](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image1.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image1.png)

**図 01**: [新しいプロジェクト] ダイアログボックス ([クリックすると、フルサイズの画像が表示](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image2.png)されます)

[新しいプロジェクト] ダイアログボックスの上部にあるドロップダウンリストから .NET Framework 3.5 を選択したことを確認してください。そうしないと、ASP.NET MVC Web アプリケーションプロジェクトテンプレートが表示されません。

新しい MVC Web アプリケーションプロジェクトを作成するたびに、Visual Studio によって個別の単体テストプロジェクトを作成するよう求められます。 図2のダイアログが表示されます。 このチュートリアルでは時間の制約があるためテストを作成しないので、このことには少しの問題があるので、 **[いいえ]** オプションを選択し、 **[OK]** ボタンをクリックします。

> [!NOTE] 
> 
> Visual Web Developer では、テストプロジェクトはサポートされていません。

[[新しいプロジェクト] ダイアログボックスの ![](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image2.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image3.png)

**図 02**: [単体テストプロジェクトの作成] ダイアログ ([クリックすると、フルサイズの画像が表示](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image4.png)されます)

ASP.NET MVC アプリケーションには、モデル、ビュー、およびコントローラーフォルダーという標準のフォルダーセットがあります。 この標準のフォルダーセットは、[ソリューションエクスプローラー] ウィンドウに表示されます。 ムービーデータベースアプリケーションをビルドするには、各モデル、ビュー、およびコントローラーフォルダーにファイルを追加する必要があります。

Visual Studio で新しい MVC アプリケーションを作成すると、サンプルアプリケーションが取得されます。 最初から開始する必要があるため、このサンプルアプリケーションのコンテンツを削除する必要があります。 次のファイルとフォルダーを削除する必要があります。

- Controllers\HomeController.vb
- Views\Home

## <a name="creating-the-database"></a>データベースの作成

ムービーデータベースレコードを保持するデータベースを作成する必要があります。 さいわい、Visual Studio には、SQL Server Express という名前の無料のデータベースが含まれています。 データベースを作成するには、次の手順に従います。

1. ソリューションエクスプローラーウィンドウで App\_Data フォルダーを右クリックし、メニューオプション 追加、**新しい項目** の順に選択します。
2. **[データ]** カテゴリを選択し、 **[SQL Server データベース]** テンプレートを選択します (図3を参照)。
3. 新しいデータベースに*MoviesDB*という名前を指定し、 **[追加]** ボタンをクリックします。

データベースを作成したら、[App\_Data] フォルダーにある MoviesDB ファイルをダブルクリックしてデータベースに接続できます。 MoviesDB ファイルをダブルクリックすると、[サーバーエクスプローラー] ウィンドウが開きます。

> [!NOTE] 
> 
> Visual Web Developer の場合、[サーバーエクスプローラー] ウィンドウには [データベースエクスプローラー] ウィンドウという名前が付けられます。

[[新しいプロジェクト] ダイアログボックスの ![](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image3.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image5.png)

**図 03**: Microsoft SQL Server データベースの作成 ([クリックすると、フルサイズの画像が表示](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image6.png)される)

次に、新しいデータベーステーブルを作成する必要があります。 サーバーエクスプローラー ウィンドウで、テーブル フォルダーを右クリックし、**新しいテーブルの追加** メニューオプションを選択します。 このメニューオプションを選択すると、データベーステーブルデザイナーが開きます。 次のデータベース列を作成します。

<a id="0.2_table01"></a>

| **列名** | **[データ型]** | **[NULL を許容]** |
| --- | --- | --- |
| Id | int | False |
| タイトル | Nvarchar (100) | False |
| ディレクター | Nvarchar (100) | False |
| DateReleased | DateTime | False |

最初の列である Id 列には、2つの特殊なプロパティがあります。 まず、Id 列を主キー列としてマークする必要があります。 Id 列を選択したら、**主キーの設定** ボタンをクリックします (これは、キーのようなアイコンです)。 次に、Id 列を Id 列としてマークする必要があります。 列プロパティウィンドウで、[Identity Specification] セクションまで下にスクロールし、それを展開します。 **[Id]** プロパティを **[はい]** に変更します。 完了すると、テーブルは図4のようになります。

[[新しいプロジェクト] ダイアログボックスの ![](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image4.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image7.png)

**図 04**: ムービーデータベーステーブル ([クリックすると、フルサイズの画像が表示](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image8.png)されます)

最後の手順では、新しいテーブルを保存します。 [保存] ボタン (フロッピーのアイコン) をクリックし、新しいテーブルに「映画」という名前を付けます。

テーブルの作成が完了したら、いくつかのムービーレコードをテーブルに追加します。 サーバーエクスプローラーウィンドウで 映画 テーブルを右クリックし、**テーブルデータの表示** メニューオプションを選択します。 お気に入りのムービーの一覧を入力します (図5を参照)。

[[新しいプロジェクト] ダイアログボックスの ![](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image5.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image9.png)

**図 05**: ムービーレコードを入力[する (クリックすると、フルサイズの画像が表示](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image10.png)される)

## <a name="creating-the-model"></a>モデルの作成

次に、データベースを表す一連のクラスを作成する必要があります。 データベースモデルを作成する必要があります。 Microsoft Entity Framework を利用して、データベースモデルのクラスを自動的に生成します。

> [!NOTE] 
> 
> ASP.NET MVC フレームワークは、Microsoft Entity Framework に関連付けられていません。 LINQ to SQL、Subsonic、NHibernate などのさまざまなオブジェクトリレーショナルマッピング (または/M) ツールを利用して、データベースモデルクラスを作成できます。

Entity Data Model ウィザードを起動するには、次の手順を実行します。

1. ソリューションエクスプローラーウィンドウで モデル フォルダーを右クリックし、メニューオプション 追加、**新しい項目** の順に選択します。
2. **[データ]** カテゴリを選択し、 **[ADO.NET Entity Data Model]** テンプレートを選択します。
3. データモデルに*MoviesDBModel*という名前を付け、 **[追加]** ボタンをクリックします。

[追加] ボタンをクリックすると、Entity Data Model ウィザードが表示されます (図6を参照)。 ウィザードを完了するには、次の手順を実行します。

1. **[モデルの内容の選択]** ステップで、 **[データベースから生成]** オプションを選択します。
2. **[データ接続の選択]** 手順で、 *MoviesDB*データ接続を使用し、接続設定に*MoviesDBEntities*という名前を使用します。 **[次へ]** をクリックします。
3. **データベースオブジェクトの選択** ステップで、テーブル ノードを展開し、映画 テーブルを選択します。 名前空間を入力し、 **[完了]** ボタンをクリックし*ます。*

[[新しいプロジェクト] ダイアログボックスの ![](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image6.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image11.png)

**図 06**: Entity Data Model ウィザードを使用してデータベースモデルを生成[する (クリックすると、フルサイズの画像が表示](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image12.png)されます)

Entity Data Model ウィザードを完了すると、Entity Data Model デザイナーが開きます。 デザイナーに、ムービーデータベーステーブルが表示されます (図7を参照)。

[[新しいプロジェクト] ダイアログボックスの ![](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image7.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image13.png)

**図 07**: Entity Data Model デザイナー ([クリックしてフルサイズのイメージを表示](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image14.png))

続行する前に、1つの変更を加える必要があります。 Entity Data Wizard では、ムービーデータベーステーブルを表す、ムービーという名前のモデルクラスが生成されます。 映画クラスを使用して特定の映画を表現するため、クラスの名前を *、ムービーで*はなく*ムービー* (複数形ではなく単数形) に変更する必要があります。

デザイナー画面でクラスの名前をダブルクリックし、ムービーからムービーにクラスの名前を変更します。 この変更を行った後、 **[保存]** ボタン (フロッピーディスクのアイコン) をクリックして、Movie クラスを生成します。

## <a name="creating-the-aspnet-mvc-controller"></a>ASP.NET MVC コントローラーの作成

次の手順では、ASP.NET MVC コントローラーを作成します。 コントローラーは、ユーザーが ASP.NET MVC アプリケーションと対話する方法を制御する役割を担います。

次の手順に従います。

1. [ソリューションエクスプローラー] ウィンドウで、Controllers フォルダーを右クリックし、[追加] **、[コントローラー**] の順に選択します。
2. [コントローラーの追加] ダイアログボックスで、「 *HomeController* 」という名前を入力し、[**作成、更新、詳細のシナリオのアクションメソッドを追加**する] のチェックボックスをオンにします (図8を参照)。
3. **[追加]** ボタンをクリックして、プロジェクトに新しいコントローラーを追加します。

これらの手順を完了すると、リスト1のコントローラーが作成されます。 これには、Index、Details、Create、および Edit という名前のメソッドが含まれていることに注意してください。 以下のセクションでは、これらのメソッドを機能させるために必要なコードを追加します。

[[新しいプロジェクト] ダイアログボックスの ![](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image8.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image15.png)

**図 08**: 新しい ASP.NET MVC コントローラーを追加[する (クリックすると、フルサイズのイメージが表示](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image16.png)される)

**リスト1– Controllers\HomeController.vb**

[!code-vb[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/samples/sample1.vb)]

## <a name="listing-database-records"></a>データベースレコードの一覧表示

Home コントローラーの Index () メソッドは、ASP.NET MVC アプリケーションの既定のメソッドです。 ASP.NET MVC アプリケーションを実行すると、Index () メソッドが最初に呼び出されたコントローラーメソッドになります。

Index () メソッドを使用して、映画データベーステーブルのレコードの一覧を表示します。 先ほど作成したデータベースモデルクラスを利用して、Index () メソッドを使用してムービーデータベースレコードを取得します。

リスト2の HomeController クラスを変更して、\_db という名前の新しいプライベートフィールドが含まれるようにしました。 MoviesDBEntities クラスはデータベースモデルを表し、このクラスを使用してデータベースと通信します。

また、リスト2の Index () メソッドも変更しました。 Index () メソッドは、MoviesDBEntities クラスを使用して、映画データベーステーブルからすべてのムービーレコードを取得します。 式 *\_db です。Moを設定します。 ToList ()* は、ムービーデータベーステーブルのすべてのムービーレコードの一覧を返します。

ムービーの一覧がビューに渡されます。 View () メソッドに渡されるすべてのものがビューデータとしてビューに渡されます。

**リスト2– Controllers/HomeController (変更されたインデックスメソッド)**

[!code-vb[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/samples/sample2.vb)]

Index () メソッドは、Index という名前のビューを返します。 ムービーデータベースレコードの一覧を表示するには、このビューを作成する必要があります。 次の手順に従います。

**ビューの追加** ダイアログを開く前にプロジェクトをビルドし (メニューオプション ビルド、**ソリューションのビルド**)、**ビューデータクラス** ボックスの一覧に クラス が表示されないようにする必要があります。

1. コードエディターで Index () メソッドを右クリックし、 **[ビューの追加]** メニューオプションを選択します (図9を参照)。
2. [ビューの追加] ダイアログで、[厳密に**型指定されたビューを作成する**] チェックボックスがオンになっていることを確認します。
3. **[ビューコンテンツ]** ボックスの一覧で、[値 *] ボックスの一覧*を選択します。
4. **[データクラスの表示]** ドロップダウンリストから、値を選択します *。*
5. [追加] ボタンをクリックして、新しいビューを作成します (図10を参照)。

これらの手順を完了すると、Views\Home フォルダーに Index .aspx という名前の新しいビューが追加されます。 インデックスビューの内容は、リスト3に含まれています。

[[新しいプロジェクト] ダイアログボックスの ![](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image9.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image17.png)

**図 09**: コントローラーアクションからビューを追加する ([クリックすると、フルサイズの画像が表示](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image18.png)される)

[[新しいプロジェクト] ダイアログボックスの ![](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image10.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image19.png)

**図 10**: [ビューの追加] ダイアログボックスを使用して新しいビューを作成する ([クリックすると、フルサイズの画像が表示](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image20.png)されます)

[!code-aspx[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/samples/sample3.aspx)]

インデックスビューには、ムービーデータベーステーブルのすべてのムービーレコードが HTML テーブル内に表示されます。 ビューには、ViewData プロパティによって表される各ムービーを反復処理する For Each ループが含まれています。 F5 キーを押してアプリケーションを実行すると、図11の web ページが表示されます。

[[新しいプロジェクト] ダイアログボックスの ![](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image11.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image21.png)

**図 11**: インデックスビュー ([クリックすると、フルサイズの画像が表示](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image22.png)されます)

## <a name="creating-new-database-records"></a>新しいデータベースレコードの作成

前のセクションで作成したインデックスビューには、新しいデータベースレコードを作成するためのリンクが含まれています。 ロジックを実装し、新しいムービーデータベースレコードを作成するために必要なビューを作成してみましょう。

Home コントローラーには、Create () という名前の2つのメソッドが含まれています。 最初の Create () メソッドにはパラメーターがありません。 Create () メソッドのこのオーバーロードは、新しいムービーデータベースレコードを作成するための HTML フォームを表示するために使用されます。

2番目の Create () メソッドには、FormCollection パラメーターがあります。 Create () メソッドのこのオーバーロードは、新しいムービーを作成するための HTML フォームがサーバーにポストされるときに呼び出されます。 この2番目の Create () メソッドには、HTTP Post 操作が実行されない限りメソッドが呼び出されないようにする AcceptVerbs 属性があることに注意してください。

この2番目の Create () メソッドは、リスト4の更新された HomeController クラスで変更されています。 新しいバージョンの Create () メソッドは、Movie パラメーターを受け取り、ムービーデータベーステーブルに新しいムービーを挿入するためのロジックを含んでいます。

> [!NOTE] 
> 
> Bind 属性に注意してください。 ムービー Id プロパティを HTML フォームから更新したくないので、このプロパティを明示的に除外する必要があります。

**リスト4– Controllers\HomeController.vb (変更された Create メソッド)**

[!code-vb[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/samples/sample4.vb)]

Visual Studio を使用すると、新しいムービーデータベースレコードを作成するためのフォームを簡単に作成できます (図12を参照)。 次の手順に従います。

1. コードエディターで Create () メソッドを右クリックし、 **[ビューの追加]** メニューオプションを選択します。
2. [**厳密に型指定されたビューを作成**する] チェックボックスがオンになっていることを確認します。
3. **[ビューコンテンツ]** ドロップダウンリストから、[*作成*] の値を選択します。
4. **[データクラスの表示]** ドロップダウンリストから、値を選択します *。*
5. **[追加]** ボタンをクリックして、新しいビューを作成します。

[[新しいプロジェクト] ダイアログボックスの ![](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image12.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image23.png)

**図 12**: 作成ビュー[を追加する (クリックすると、フルサイズの画像が表示](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image24.png)されます)

Visual Studio によって、リスト5に自動的にビューが生成されます。 このビューには、Movie クラスの各プロパティに対応するフィールドを含む HTML フォームが含まれています。

**リスト5– Views\Home\Create.aspx**

[!code-aspx[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/samples/sample5.aspx)]

> [!NOTE] 
> 
> [ビューの追加] ダイアログで生成された HTML フォームは、Id フォームフィールドを生成します。 Id 列は Id 列であるため、このフォームフィールドは不要であり、安全に削除できます。

[作成] ビューを追加した後、新しいムービーレコードをデータベースに追加できます。 F5 キーを押してアプリケーションを実行し、[新規作成] リンクをクリックして、図13のフォームを表示します。 フォームを完了して送信すると、新しいムービーデータベースレコードが作成されます。

フォームの検証は自動的に行われることに注意してください。 ムービーのリリース日を入力しなかった場合、または無効なリリース日を入力した場合は、フォームが再表示され、リリース日フィールドが強調表示されます。

[[新しいプロジェクト] ダイアログボックスの ![](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image13.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image25.png)

**図 13**: 新しいムービーデータベースレコードを作成[する (クリックすると、フルサイズの画像が表示](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image26.png)される)

## <a name="editing-existing-database-records"></a>既存のデータベースレコードの編集

前のセクションでは、新しいデータベースレコードを一覧表示し、作成する方法について説明しました。 この最後のセクションでは、既存のデータベースレコードを編集する方法について説明します。

まず、編集フォームを生成する必要があります。 この手順は、Visual Studio によって自動的に編集フォームが生成されるため、簡単です。 Visual Studio コードエディターで HomeController クラスを開き、次の手順を実行します。

1. コードエディターで Edit () メソッドを右クリックし、 **[ビューの追加]** メニューオプションを選択します (図14を参照)。
2. **[厳密に型指定されたビューを作成する]** チェックボックスをオンにします。
3. **[ビューコンテンツ]** ドロップダウンリストから、[値の*編集*] を選択します。
4. **[データクラスの表示]** ドロップダウンリストから、値を選択します *。*
5. **[追加]** ボタンをクリックして、新しいビューを作成します。

これらの手順を完了すると、Views\Home フォルダーに、エディット .aspx という名前の新しいビューが追加されます。 このビューには、ムービーレコードを編集するための HTML フォームが含まれています。

[[新しいプロジェクト] ダイアログボックスの ![](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image14.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image27.png)

**図 14**: 編集ビュー[を追加する (クリックすると、フルサイズの画像が表示](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image28.png)されます)

> [!NOTE] 
> 
> [編集] ビューには、"ムービー Id" プロパティに対応する HTML フォームフィールドがあります。 Id プロパティの値を編集しないようにするには、このフォームフィールドを削除する必要があります。

最後に、データベースレコードの編集をサポートするように Home コントローラーを変更する必要があります。 更新された HomeController クラスは、リスト6に含まれています。

**リスト6– Controllers\HomeController.vb (メソッドの編集)**

[!code-vb[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/samples/sample6.vb)]

リスト6では、Edit () メソッドの両方のオーバーロードにロジックを追加しました。 最初の Edit () メソッドは、メソッドに渡された Id パラメーターに対応するムービーデータベースレコードを返します。 2番目のオーバーロードは、データベース内のムービーレコードの更新を実行します。

元のムービーを取得し、ApplyPropertyChanges () を呼び出して、データベース内の既存のムービーを更新する必要があることに注意してください。

## <a name="summary"></a>まとめ

このチュートリアルの目的は、ASP.NET MVC アプリケーションを構築する経験を理解することでした。 ASP.NET MVC web アプリケーションを構築することは、Active Server ページまたは ASP.NET アプリケーションを構築する場合とよく似ていると思います。

このチュートリアルでは、ASP.NET MVC フレームワークの最も基本的な機能のみを検討しています。 今後のチュートリアルでは、コントローラー、コントローラーアクション、ビュー、ビューデータ、HTML ヘルパーなどのトピックについて詳しく説明します。

> [!div class="step-by-step"]
> [[戻る]](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs.md)
