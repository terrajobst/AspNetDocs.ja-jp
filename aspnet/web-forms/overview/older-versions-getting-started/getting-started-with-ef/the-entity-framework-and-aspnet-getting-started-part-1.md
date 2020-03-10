---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1
title: はじめに Entity Framework 4.0 Database First および ASP.NET 4 Web Forms |Microsoft Docs
author: tdykstra
description: Contoso 大学のサンプル web アプリケーションでは、Entity Framework 4.0 と Visual Studio 2010 を使用して ASP.NET Web フォームアプリケーションを作成する方法を示しています。
ms.author: riande
ms.date: 12/03/2010
ms.assetid: 5cb00916-8f46-491f-be25-4739a615d619
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1
msc.type: authoredcontent
ms.openlocfilehash: fd88b32ad2a65e5b4c7ead15f0d6dc5dc6e97e75
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78511678"
---
# <a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms"></a>Entity Framework 4.0 Database First および ASP.NET 4 Web フォームでのはじめに

[Tom Dykstra](https://github.com/tdykstra)

> Contoso 大学のサンプル web アプリケーションは、Entity Framework 4.0 と Visual Studio 2010 を使用して ASP.NET Web フォームアプリケーションを作成する方法を示しています。 サンプルアプリケーションは、架空の Contoso 大学の web サイトです。 学生の受け付け、講座の作成、講師の割り当てなどの機能が含まれています。
> 
> このチュートリアルでは、 C#の例を示します。 ダウンロード可能な[サンプル](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a)には、 C#と Visual Basic の両方のコードが含まれています。
> 
> ## <a name="database-first"></a>Database First
> 
> Entity Framework のデータを操作するには、 *Database First*、 *Model First*、および*Code First*の3つの方法があります。 このチュートリアルは Database First を対象としています。 これらのワークフローの違いと、シナリオに最適なワークフローを選択する方法については、「 [Entity Framework 開発ワークフロー](https://msdn.microsoft.com/library/ms178359.aspx#dbfmfcf)」を参照してください。
> 
> ## <a name="web-forms"></a>Web フォーム
> 
> このチュートリアルシリーズでは、ASP.NET Web フォームモデルを使用しており、Visual Studio で ASP.NET Web フォームを使用する方法を理解していることを前提としています。 そうでない場合は、「[はじめにと ASP.NET 4.5 Web フォーム](../../getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview.md)」を参照してください。 ASP.NET MVC フレームワークを使用する場合は、「 [ASP.NET mvc を使用した Entity Framework でのはじめに](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)」を参照してください。
> 
> ## <a name="software-versions"></a>ソフトウェアのバージョン
> 
> | **チュートリアルに表示されます。** | **でも動作します。** |
> | --- | --- |
> | Windows 7 | Windows 8 |
> | Visual Studio 2010 | Visual Studio 2010 Express for Web。 このチュートリアルは、以降のバージョンの Visual Studio ではテストされていません。 メニューの選択、ダイアログボックス、テンプレートにはさまざまな違いがあります。 |
> | .NET 4 | .Net 4.5 は .NET 4 と下位互換性がありますが、このチュートリアルは .NET 4.5 ではテストされていません。 |
> | Entity Framework 4 | このチュートリアルは、以降のバージョンの Entity Framework ではテストされていません。 Entity Framework 5 以降では、ef 4.1 で導入された `DbContext API` が既定で使用されます。 EntityDataSource コントロールは、`ObjectContext` API を使用するように設計されています。 `DbContext` API で EntityDataSource コントロールを使用する方法の詳細については、[このブログ投稿](https://blogs.msdn.com/b/webdev/archive/2012/09/13/how-to-use-the-entitydatasource-control-with-entity-framework-code-first.aspx)を参照してください。 |
> 
> ## <a name="questions"></a>疑問がある場合
> 
> チュートリアルに直接関係のない質問がある場合は、 [ASP.NET Entity Framework フォーラム](https://forums.asp.net/1227.aspx)、 [Entity Framework と LINQ to Entities フォーラム](https://social.msdn.microsoft.com/forums/adodotnetentityframework/threads/)、または[StackOverflow.com](http://stackoverflow.com/)に投稿できます。

## <a name="overview"></a>概要

これらのチュートリアルで作成するアプリケーションは、単純な大学の web サイトです。

[![Image03](the-entity-framework-and-aspnet-getting-started-part-1/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image1.png)

ユーザーは学生、講座、講師の情報を見たり、更新したりできます。 作成する画面のいくつかを次に示します。

[![Image30](the-entity-framework-and-aspnet-getting-started-part-1/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image3.png)

[![Image37](the-entity-framework-and-aspnet-getting-started-part-1/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image5.png)

[![Image31](the-entity-framework-and-aspnet-getting-started-part-1/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image7.png)

[![Image32](the-entity-framework-and-aspnet-getting-started-part-1/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image9.png)

## <a name="creating-the-web-application"></a>Web アプリケーションの作成

チュートリアルを開始するには、Visual Studio を開き、 **ASP.NET Web アプリケーション**テンプレートを使用して新しい ASP.NET Web アプリケーションプロジェクトを作成します。

[![Image01](the-entity-framework-and-aspnet-getting-started-part-1/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image11.png)

このテンプレートは、スタイルシートとマスターページが既に含まれている web アプリケーションプロジェクトを作成します。

[![Image02](the-entity-framework-and-aspnet-getting-started-part-1/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image13.png)

*.Master*ファイルを開き、"My ASP.NET Application" を "Contoso 大学" に変更します。

[!code-html[Main](the-entity-framework-and-aspnet-getting-started-part-1/samples/sample1.html)]

`NavigationMenu` という名前の*メニュー*コントロールを見つけて、次のマークアップに置き換えます。これにより、作成するページのメニュー項目が追加されます。

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-1/samples/sample2.aspx)]

*Default.aspx*ページを開き、`BodyContent` という名前の `Content` コントロールを次のように変更します。

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-1/samples/sample3.aspx)]

これで、作成するさまざまなページへのリンクを含む単純なホームページが作成されました。

[![Image03](the-entity-framework-and-aspnet-getting-started-part-1/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image15.png)

## <a name="creating-the-database"></a>データベースの作成

これらのチュートリアルでは、Entity Framework データモデルデザイナーを使用して、既存のデータベースに基づいてデータモデルを自動的に作成します (多くの場合、*データベース優先*のアプローチと呼ばれます)。 このチュートリアルシリーズでは説明しませんが、データモデルを手動で作成した後、データベースを作成するスクリプト (*モデルファースト*アプローチ) を生成することもできます。

このチュートリアルで使用するデータベース優先の方法では、次の手順として、データベースをサイトに追加します。 最も簡単な方法は、このチュートリアルで使用するプロジェクトを最初にダウンロードすることです。 次に、[ *App\_Data* ] フォルダーを右クリックし、 **[既存項目の追加]** を選択して、ダウンロードしたプロジェクトから*School*データベースファイルを選択します。

別の方法として、 [School サンプルデータベースの作成](https://msdn.microsoft.com/library/bb399731.aspx)に関する説明に従ってください。 データベースをダウンロードするか、作成するかにかかわらず、次のフォルダーから*School*ファイルをアプリケーションの*アプリ\_データ*フォルダーにコピーします。

`%PROGRAMFILES%\Microsoft SQL Server\MSSQL10.SQLEXPRESS\MSSQL\DATA`

( *.Mdf*ファイルのこの場所では、SQL Server 2008 Express を使用していることを前提としています)。

スクリプトからデータベースを作成する場合は、次の手順を実行してデータベースダイアグラムを作成します。

1. **サーバーエクスプローラー**で、 **[データ接続]** 、[ *School .mdf*] の順に展開し、 **[データベースダイアグラム]** を右クリックして、 **[新しいダイアグラムの追加]** を選択します。

    [![Image35](the-entity-framework-and-aspnet-getting-started-part-1/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image17.png)
2. すべてのテーブルを選択し、 **[追加]** をクリックします。

    [![Image36](the-entity-framework-and-aspnet-getting-started-part-1/_static/image20.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image19.png)

    SQL Server により、テーブル、テーブル内の列、およびテーブル間のリレーションシップを示すデータベースダイアグラムが作成されます。 テーブルを移動して、自由に整理することができます。
3. ダイアグラムを "SchoolDiagram" として保存し、閉じます。

このチュートリアルに記載されている*School .mdf*ファイルをダウンロードすると、**サーバーエクスプローラー**の **[データベースダイアグラム]** の下にある **[SchoolDiagram]** をダブルクリックすると、データベースダイアグラムが表示されます。

[![Image38](the-entity-framework-and-aspnet-getting-started-part-1/_static/image22.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image21.png)

ダイアグラムは次のようになります (テーブルは、ここに表示されている場所とは異なる場所にある可能性があります)。

[![Image04](the-entity-framework-and-aspnet-getting-started-part-1/_static/image24.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image23.png)

## <a name="creating-the-entity-framework-data-model"></a>Entity Framework データモデルの作成

これで、このデータベースから Entity Framework データモデルを作成できるようになりました。 データモデルはアプリケーションのルートフォルダーに作成できますが、このチュートリアルでは、 *DAL*という名前のフォルダーに配置します (データアクセス層の場合)。

**ソリューションエクスプローラー**で、 *DAL*という名前のプロジェクトフォルダーを追加します (ソリューションではなく、プロジェクトの下にあることを確認してください)。

[ *DAL* ] フォルダーを右クリックし、 **[追加]** 、 **[新しい項目]** の順に選択します。 **[インストールされたテンプレート]** で **[データ]** を選択し、 **[ADO.NET Entity Data Model]** テンプレートを選択して*SchoolModel*という名前を入力し、 **[追加]** をクリックします。

[![Image05](the-entity-framework-and-aspnet-getting-started-part-1/_static/image26.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image25.png)

これにより、Entity Data Model ウィザードが起動します。 ウィザードの最初の手順では、 **[データベースから生成]** オプションが既定で選択されています。 **[次へ]** をクリックします。

[![Image06](the-entity-framework-and-aspnet-getting-started-part-1/_static/image28.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image27.png)

**[データ接続の選択]** 手順で、既定値をそのまま使用し、 **[次へ]** をクリックします。 School データベースが既定で選択され、接続設定が*web.config*ファイルに**SchoolEntities**として保存されます。

[![Image07](the-entity-framework-and-aspnet-getting-started-part-1/_static/image30.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image29.png)

**[データベースオブジェクトの選択]** ウィザードの手順で、(前に生成したダイアグラム用に作成された) `sysdiagrams` を除くすべてのテーブルを選択し、 **[完了]** をクリックします。

[![Image08](the-entity-framework-and-aspnet-getting-started-part-1/_static/image32.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image31.png)

モデルの作成が完了すると、Visual Studio には、データベーステーブルに対応する Entity Framework オブジェクト (エンティティ) がグラフィカルに表示されます。 (データベースダイアグラムと同様に、個々の要素の場所は、この図に表示されるものとは異なる場合があります。 必要に応じて、要素をドラッグして、イラストレーションに一致させることができます)。

[![Image09](the-entity-framework-and-aspnet-getting-started-part-1/_static/image34.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image33.png)

## <a name="exploring-the-entity-framework-data-model"></a>Entity Framework データモデルの調査

エンティティダイアグラムがデータベースダイアグラムと非常によく似ていることがわかりますが、いくつか違いがあります。 違いの1つは、関連付けの種類を示す各アソシエーションの最後にシンボルを追加することです (テーブルのリレーションシップはデータモデル内のエンティティの関連付けと呼ばれます)。

- 一対ゼロまたは一対一のアソシエーションは、"1" と "0 ..1" で表されます。

    [![Image39](the-entity-framework-and-aspnet-getting-started-part-1/_static/image36.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image35.png)

    この場合、`Person` エンティティは、`OfficeAssignment` エンティティに関連付けられている場合も、そうでない場合もあります。 `OfficeAssignment` エンティティは、`Person` エンティティに関連付けられている必要があります。 つまり、インストラクターはオフィスに割り当てられない場合もあれば、1人のインストラクターにのみ割り当てることもできます。
- 一対多のアソシエーションは、"1" と "\*" で表されます。

    [![Image40](the-entity-framework-and-aspnet-getting-started-part-1/_static/image38.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image37.png)

    この場合、`Person` エンティティは、`StudentGrade` エンティティに関連付けられている場合と、存在しない場合があります。 `StudentGrade` エンティティは、1つの `Person` エンティティに関連付けられている必要があります。 `StudentGrade` エンティティは、実際には、このデータベースに登録されているコースを表します。学生がコースに登録されていて、まだグレードがない場合、`Grade` プロパティは null になります。 言い換えると、学生がコースに登録されていない場合、1つのコースに登録されている場合、または複数のコースに登録されている場合があります。 登録したコースの各グレードは、1人の学生にのみ適用されます。
- 多対多のアソシエーションは、"\*" と "\*" で表されます。

    [![Image41](the-entity-framework-and-aspnet-getting-started-part-1/_static/image40.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image39.png)

    この場合、`Person` エンティティは、`Course` エンティティに関連付けられている場合と、存在しない場合があります。また、逆の場合もあります。 `Course` エンティティには `Person` エンティティが関連付けられている場合と、存在しない場合があります。 つまり、インストラクターは複数のコースを教えることができ、コースは複数の教師によって教育されることがあります。 (このデータベースでは、この関係は講師にのみ適用されます。学生はコースにリンクされません。 学生は、StudentGrades テーブルによってコースにリンクされています)。

データベースダイアグラムとデータモデルのもう1つの違いは、各エンティティの追加の**ナビゲーションプロパティ**セクションです。 エンティティのナビゲーションプロパティは、関連エンティティを参照します。 たとえば、`Person` エンティティの `Courses` プロパティには、その `Person` エンティティに関連するすべての `Course` エンティティのコレクションが含まれています。

[![Image12](the-entity-framework-and-aspnet-getting-started-part-1/_static/image42.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image41.png)

ただし、データベースとデータモデルのもう1つの違いは、多対多リレーションシップで `Person` テーブルと `Course` テーブルをリンクするためにデータベースで使用される `CourseInstructor` 関連付けテーブルがないことです。 ナビゲーションプロパティを使用すると、`Person` エンティティから関連する `Course` エンティティと、`Course` エンティティから関連する `Person` エンティティを取得できます。そのため、データモデルでアソシエーションテーブルを表す必要はありません。

[![Image11](the-entity-framework-and-aspnet-getting-started-part-1/_static/image44.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image43.png)

このチュートリアルでは、`Person` テーブルの `FirstName` 列に、実際にはユーザーの名とミドルネームの両方が含まれているとします。 これを反映するようにフィールドの名前を変更する必要がありますが、データベース管理者 (DBA) がデータベースを変更したくない可能性があります。 データモデルの `FirstName` プロパティの名前は変更できますが、データベースはそのままにしておきます。

デザイナーで、`Person` エンティティの **[FirstName]** を右クリックし、 **[名前の変更]** を選択します。

[![Image13](the-entity-framework-and-aspnet-getting-started-part-1/_static/image46.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image45.png)

新しい "FirstMidName" という名前を入力します。 これにより、データベースを変更することなく、コード内の列を参照する方法が変更されます。

[![Image29](the-entity-framework-and-aspnet-getting-started-part-1/_static/image48.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image47.png)

モデルブラウザーには、データベース構造、データモデル構造、およびそれらの間のマッピングを表示する別の方法が用意されています。 表示するには、エンティティデザイナーで空白の領域を右クリックし、 **[モデルブラウザー]** をクリックします。

[![Image18](the-entity-framework-and-aspnet-getting-started-part-1/_static/image50.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image49.png)

**[モデルブラウザー]** ペインにツリービューが表示されます。 ( **[モデルブラウザー]** ウィンドウは、 **[ソリューションエクスプローラー]** ウィンドウと共にドッキングされている場合があります)。**SchoolModel**ノードはデータモデル構造を表し、 **SchoolModel**ノードはデータベース構造を表します。

[![Image26](the-entity-framework-and-aspnet-getting-started-part-1/_static/image52.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image51.png)

**[SchoolModel]** を展開してテーブルを表示し、 **[テーブル/ビュー]** を展開してテーブルを表示します。次に、 **[Course]** を展開してテーブル内の列を表示します。

[![Image19](the-entity-framework-and-aspnet-getting-started-part-1/_static/image54.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image53.png)

**[SchoolModel]** 、 **[エンティティ型]** の順に展開し、 **Course**ノードを展開してエンティティとエンティティ内のプロパティを表示します。

[![Image20](the-entity-framework-and-aspnet-getting-started-part-1/_static/image56.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image55.png)

デザイナーまたは **[モデルブラウザー]** ペインには、Entity Framework が2つのモデルのオブジェクトにどのように関連しているかが表示されます。 `Person` エンティティを右クリックし、 **[テーブルマッピング]** を選択します。

[![Image21](the-entity-framework-and-aspnet-getting-started-part-1/_static/image58.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image57.png)

[マッピングの**詳細**] ウィンドウが開きます。 このウィンドウでは、データベース列 `FirstName` が `FirstMidName`にマップされていることを確認できます。これは、データモデルで名前を変更したものです。

[![Image22](the-entity-framework-and-aspnet-getting-started-part-1/_static/image60.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image59.png)

Entity Framework は、XML を使用して、データベース、データモデル、およびそれらの間のマッピングに関する情報を格納します。 *SchoolModel*ファイルは、実際にはこの情報を含む XML ファイルです。 デザイナーでは情報がグラフィカルな形式で表示されますが、ファイルを XML として表示するには、**ソリューションエクスプローラー**で *.edmx*ファイルを右クリックし、ファイルを **[開くアプリケーション]** の選択 をクリックし、 **[xml (テキスト) エディター]** を選択します。 (データモデルデザイナーと XML エディターは、同じファイルを開いて作業するための2つの異なる方法であるため、デザイナーを開いて、同時に XML エディターでファイルを開くことはできません)。

これで、web サイト、データベース、およびデータモデルが作成されました。 次のチュートリアルでは、データモデルと ASP.NET `EntityDataSource` コントロールを使用してデータの操作を開始します。

> [!div class="step-by-step"]
> [Next](the-entity-framework-and-aspnet-getting-started-part-2.md)
