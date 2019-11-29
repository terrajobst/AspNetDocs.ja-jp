---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application
title: ASP.NET MVC アプリケーションの Entity Framework データモデルを作成する (1/10) |Microsoft Docs
author: tdykstra
description: このチュートリアルシリーズの新しいバージョンは、Visual Studio 2013、Entity Framework 6、および MVC 5 で使用できます。 Contoso 大学のサンプル web アプリケーション...
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 4ba029b6-ee7c-4e45-a0e7-b703c37e5d9a
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 8ee5aa22b6b2329b01d41437f30508e28a2288b2
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74595970"
---
# <a name="creating-an-entity-framework-data-model-for-an-aspnet-mvc-application-1-of-10"></a>ASP.NET MVC アプリケーションの Entity Framework データモデルの作成 (10 件)

[Tom Dykstra](https://github.com/tdykstra)

[完成したプロジェクトのダウンロード](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> > [!NOTE] 
> > 
> > [このチュートリアルシリーズの新しいバージョン](../../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)は、Visual Studio 2013、Entity Framework 6、および MVC 5 で使用できます。
> 
> 
> Contoso 大学のサンプル web アプリケーションは、Entity Framework 5 と Visual Studio 2012 を使用して ASP.NET MVC 4 アプリケーションを作成する方法を示しています。 サンプル アプリケーションは架空の Contoso University の Web サイトです。 学生の受け付け、講座の作成、講師の割り当てなどの機能が含まれています。 このチュートリアルシリーズでは、Contoso 大学サンプルアプリケーションを構築する方法について説明します。 完成した[アプリケーションをダウンロード](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)できます。
> 
> ## <a name="code-first"></a>Code First
> 
> Entity Framework のデータを操作するには、 *Database First*、 *Model First*、および*Code First*の3つの方法があります。 このチュートリアルは Code First を対象としています。 これらのワークフローの違いと、シナリオに最適なワークフローを選択する方法については、「 [Entity Framework 開発ワークフロー](https://msdn.microsoft.com/library/ms178359.aspx#dbfmfcf)」を参照してください。
> 
> ## <a name="mvc"></a>MVC
> 
> このサンプルアプリケーションは、 [ASP.NET MVC](../../../index.md)上に構築されています。 ASP.NET Web フォームモデルを使用する場合は、[モデルバインドと Web フォーム](../../../../web-forms/overview/presenting-and-managing-data/model-binding/retrieving-data.md)チュートリアルシリーズおよび[ASP.NET データアクセスコンテンツマップ](../../../../whitepapers/aspnet-data-access-content-map.md)を参照してください。
> 
> ## <a name="software-versions"></a>ソフトウェアのバージョン
> 
> | **チュートリアルに表示されます。** | **でも動作します。** |
> | --- | --- |
> | Windows 8 | Windows 7 |
> | Visual Studio 2012 | Visual Studio 2012 Express for Web。 これは、Microsoft Azure SDK によって自動的にインストールされます (VS 2012 または VS 2012 Express for Web をまだお持ちでない場合)。 Visual Studio 2013 は機能しますが、チュートリアルではテストが行われていないため、メニューの選択とダイアログボックスが異なる場合があります。 Windows azure のデプロイには、 [Windows AZURE SDK の VS 2013 バージョン](https://go.microsoft.com/fwlink/p/?linkid=323510)が必要です。 |
> | .NET 4.5 | ここに示されている機能のほとんどは .NET 4 で動作しますが、一部の機能は機能しません。 たとえば、EF での enum サポートには .NET 4.5 が必要です。 |
> | Entity Framework 5 |  |
> | [Windows Azure SDK 2.1](https://go.microsoft.com/fwlink/p/?linkid=323511) | Windows Azure のデプロイ手順を省略した場合、SDK は必要ありません。 新しいバージョンの SDK がリリースされると、新しいバージョンがインストールされます。 その場合は、一部の手順を新しい UI と機能に適合させる必要があります。 |
> 
> ## <a name="questions"></a>質問
> 
> チュートリアルに直接関係のない質問がある場合は、 [ASP.NET Entity Framework フォーラム](https://forums.asp.net/1227.aspx)、 [Entity Framework と LINQ to Entities フォーラム](https://social.msdn.microsoft.com/forums/adodotnetentityframework/threads/)、または[StackOverflow.com](http://stackoverflow.com/)に投稿できます。
> 
> ## <a name="acknowledgments"></a>謝辞
> 
> 確認については、シリーズの最後のチュートリアル[と VB に関するメモ](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#acknowledgments)を参照してください。
> 
> ## <a name="original-version-of-the-tutorial"></a>チュートリアルの元のバージョン
> 
> このチュートリアルの元のバージョンは、 [EF 4.1/MVC 3 の電子書籍](https://social.technet.microsoft.com/wiki/contents/articles/11608.e-book-gallery-for-microsoft-technologies.aspx#GettingStartedwiththeEntityFramework4.1usingASP.NETMVC)で入手できます。

## <a name="the-contoso-university-web-application"></a>Contoso 大学 Web アプリケーション

一連のチュートリアルで作成するアプリケーションは、簡単な大学向け Web サイトです。

ユーザーは学生、講座、講師の情報を見たり、更新したりできます。 次のような画面をこれから作成します。

![Students_Index_page](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image1.png)

![](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image2.png)

このサイトの UI スタイルは、組み込みテンプレートで生成されるスタイルに近いものになっています。それにより、このチュートリアルでは主に、Entity Framework の使い方を取り上げることができます。

## <a name="prerequisites"></a>必要条件

このチュートリアルの指示とスクリーンショットでは、 [Visual studio 2012](https://www.microsoft.com/visualstudio/eng/downloads)または[Visual studio 2012 Express for Web](https://go.microsoft.com/fwlink/?LinkID=275131)を使用しており、最新の更新プログラムと Azure SDK For .Net が2013年7月の時点でインストールされていることを前提としています。 次のリンクを使用して、すべての情報を取得できます。

[Azure SDK for .NET (Visual Studio 2012)](https://go.microsoft.com/fwlink/?LinkId=254364)

Visual Studio がインストールされている場合、上記のリンクを使用すると、不足しているコンポーネントがインストールされます。 Visual Studio をお持ちでない場合は、Visual Studio 2012 Express for Web がインストールされます。 Visual Studio 2013 を使用できますが、いくつかの必要な手順と画面は異なります。

## <a name="create-an-mvc-web-application"></a>MVC Web アプリケーションを作成する

Visual Studio を開き、 C# **ASP.NET MVC 4 Web アプリケーション**テンプレートを使用して、"ContosoUniversity" という名前の新しいプロジェクトを作成します。 **.NET Framework 4.5**を対象としていることを確認します ( [`enum` のプロパティ](https://msdn.microsoft.com/data/hh859576.aspx)を使用し、.net 4.5 が必要です)。

![New_project_dialog_box](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image3.png)

**[New ASP.NET MVC 4 プロジェクト]** ダイアログボックスで、 **[インターネットアプリケーション]** テンプレートを選択します。

**[Razor]** ビューエンジン を選択したままにして、 **[単体テストプロジェクトの作成]** チェックボックスはオフのままにします。

**[OK]** をクリックします。

![Project_template_options](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image4.png)

## <a name="set-up-the-site-style"></a>サイトスタイルを設定する

簡単な変更をいくつか行い、サイトのメニュー、レイアウト、ホーム ページを決めます。

*Views\Shared\\_Layout*を開き、ファイルの内容を次のコードに置き換えます。 変更が強調表示されます。

[!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample1.cshtml?highlight=5,15,25-28,43)]

このコードにより、次の変更が行われます。

- "My ASP.NET MVC Application" と "your logo here" のテンプレートインスタンスを "Contoso 大学" に置き換えます。
- チュートリアルの後半で使用されるアクションリンクをいくつか追加します。

*Views\Home\Index.cshtml*で、ファイルの内容を次のコードに置き換えて、ASP.NET と MVC に関するテンプレートの段落を削除します。

[!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample2.cshtml)]

次の例に示すように、 *controllers\ homecontroller.cs*で、`Index` アクションメソッドの `ViewBag.Message` の値を「Contoso 大学にようこそ!」に変更します。

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample3.cs?highlight=3)]

CTRL キーを押しながら F5 キーを押してサイトを実行します。 メインメニューが表示されたホームページが表示されます。

![Contoso_University_home_page](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image5.png)

## <a name="create-the-data-model"></a>データモデルを作成する

次に、Contoso University アプリケーションのエンティティ クラスを作成します。 次の3つのエンティティから始めます。

![Class_diagram](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image6.png)

`Student` エンティティと `Enrollment` エンティティの間に一対多の関係があり、`Course` エンティティと `Enrollment` エンティティの間に一対多の関係があります。 言い換えると、1 人の学生をさまざまな講座に登録し、1 つの講座にたくさんの学生を登録できます。

次のセクションでは、エンティティごとにクラスを作成します。

> [!NOTE]
> これらのエンティティクラスのすべての作成を完了する前にプロジェクトをコンパイルしようとすると、コンパイラエラーが発生します。

### <a name="the-student-entity"></a>Student エンティティ

![Student_entity](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image7.png)

[*モデル*] フォルダーで*Student.cs*を作成し、既存のコードを次のコードに置き換えます。

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample4.cs)]

`StudentID` プロパティは、このクラスに相当するデータベース テーブルの主キー列になります。 既定では、Entity Framework は `ID` または*classname* `ID` という名前のプロパティを主キーとして解釈します。

`Enrollments` プロパティは*ナビゲーション プロパティ*です。 ナビゲーション プロパティには、このエンティティに関連する他のエンティティが含まれます。 この場合、`Student` エンティティの `Enrollments` プロパティには、その `Student` エンティティに関連付けられているすべての `Enrollment` エンティティが保持されます。 言い換えると、データベース内の特定の `Student` 行に2つの関連する `Enrollment` 行 (その学生の主キー値が `StudentID` 外部キー列に含まれる行) がある場合、その `Student` エンティティの `Enrollments` ナビゲーションプロパティには、その2つの `Enrollment` エンティティが含まれます。

通常、ナビゲーションプロパティは、*遅延読み込み*などの特定の Entity Framework 機能を利用できるように `virtual` として定義されます。 (遅延読み込みについては、このシリーズの後の「[関連データの読み取り](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)」チュートリアルで後ほど説明します。

ナビゲーション プロパティに複数のエンティティが含まれる場合 (多対多または一対多の関係で)、その型はリストにする必要があります。`ICollection` のように、エンティティを追加、削除、更新できるリストです。

### <a name="the-enrollment-entity"></a>登録エンティティ

![Enrollment_entity](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image8.png)

*[Models]* フォルダーで、*Enrollment.cs* を作成し、既存のコードを次のコードに変更します。

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample5.cs)]

学年プロパティは[列挙型](https://msdn.microsoft.com/data/hh859576.aspx)です。 `Grade` の型宣言の後の疑問符は、`Grade` プロパティが [nullable](https://msdn.microsoft.com/library/2cf62fcy.aspx) であることを示します。 Null のグレードは0グレードとは異なります。 null は、グレードが不明であるか、まだ割り当てられていないことを示します。

`StudentID` プロパティは外部キーです。それに対応するナビゲーション プロパティは `Student` です。 `Enrollment` エンティティは 1 つの `Student` エンティティに関連付けられており、1 つの `Student` エンティティだけを保持できます (先に見た、複数の `Enrollment` エンティティを保持できる `Student.Enrollments` ナビゲーション プロパティとは異なります)。

`CourseID` プロパティは外部キーです。それに対応するナビゲーション プロパティは `Course` です。 `Enrollment` エンティティは 1 つの `Course` エンティティに関連付けられます。

### <a name="the-course-entity"></a>Course エンティティ

![Course_entity](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image9.png)

[*モデル*] フォルダーで*Course.cs*を作成し、既存のコードを次のコードに置き換えます。

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample6.cs)]

`Enrollments` プロパティはナビゲーション プロパティです。 1 つの `Course` エンティティにたくさんの `Enrollment` エンティティを関連付けることができます。

ここでは、[[Databasegenerated](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.databasegeneratedattribute(v=vs.110).aspx)([databasegeneratedo)](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.databasegeneratedoption(v=vs.95).aspx)の詳細について説明します。None)] 属性を次のチュートリアルで行います。 基本的に、この属性によって、講座の主キーをデータベースに生成させず、自分で入力できるようになります。

## <a name="create-the-database-context"></a>データベース コンテキストの作成

特定のデータモデルの Entity Framework 機能を調整するメインクラスは、*データベースコンテキスト*クラスです。 このクラスは、system.string[コンテキスト](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=VS.103).aspx)クラスから派生させることによって作成します。 自分のコードでは、データ モデルに含めるエンティティを自分で指定します。 Entity Framework の特定の動作をカスタマイズすることもできます。 このプロジェクトでは、クラスに `SchoolContext` という名前が付けられています。

*DAL*という名前のフォルダーを作成します (データアクセス層の場合)。 そのフォルダーで、 *SchoolContext.cs*という名前の新しいクラスファイルを作成し、既存のコードを次のコードに置き換えます。

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample7.cs)]

このコードでは、エンティティセットごとに[dbset](https://msdn.microsoft.com/library/system.data.entity.dbset(v=VS.103).aspx)プロパティを作成します。 Entity Framework 用語では、*エンティティセット*は通常、データベーステーブルに対応し、*エンティティ*はテーブル内の行に対応します。

[Onmodelcreating](https://msdn.microsoft.com/library/system.data.entity.dbcontext.onmodelcreating(v=vs.103).aspx)メソッドの `modelBuilder.Conventions.Remove` ステートメントを実行すると、テーブル名をにできなくなります。 この操作を行わなかった場合、生成されたテーブルには `Students`、`Courses`、および `Enrollments`という名前が付けられます。 代わりに、テーブル名は `Student`、`Course`、および `Enrollment`になります。 テーブル名を複数形にするかどうかについては、開発者の間で意見が分かれるでしょう。 このチュートリアルでは単数形を使用しますが、重要な点は、このコード行を含めたり省略したりすることで、任意の形式を選択できることです。

## <a name="sql-server-express-localdb"></a>SQL Server Express LocalDB

[LocalDB](https://blogs.msdn.com/b/sqlexpress/archive/2011/07/12/introducing-localdb-a-better-sql-express.aspx)は、オンデマンドで開始され、ユーザーモードで実行される SQL Server Express データベースエンジンの軽量バージョンです。 LocalDB は、 *.mdf*ファイルとしてデータベースを操作できるようにする SQL Server Express の特別な実行モードで実行されます。 通常、LocalDB データベースファイルは、web プロジェクトの*App\_Data*フォルダーに保持されます。 SQL Server Express のユーザーインスタンス機能では、.mdf ファイルを使用することもでき*ます*が、ユーザーインスタンス機能は非推奨とされます。そのため、 *.mdf*ファイルを使用する場合は LocalDB をお勧めします。

通常 SQL Server Express は、運用 web アプリケーションでは使用されません。 LocalDB は、IIS で動作するように設計されていないため、web アプリケーションでの運用環境での使用は推奨されません。

Visual Studio 2012 以降のバージョンでは、LocalDB が既定で Visual Studio と共にインストールされます。 Visual Studio 2010 以前のバージョンでは、SQL Server Express (LocalDB なし) が既定で Visual Studio と共にインストールされています。Visual Studio 2010 を使用している場合は、手動でインストールする必要があります。

このチュートリアルでは、LocalDB を使用して、データベースを *.mdf*ファイルとして*App\_Data*フォルダーに格納できるようにします。 ルートの*web.config*ファイルを開き、次の例に示すように、新しい接続文字列を `connectionStrings` コレクションに追加します。 (ルートプロジェクトフォルダー*内の web.config ファイルを*必ず更新してください。 また、 *web.config ファイルは*、更新する必要のない*Views*サブフォルダーにあります)。

[!code-xml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample8.xml)]

既定では、Entity Framework は、`DbContext` クラス (このプロジェクトでは`SchoolContext`) と同じ名前の接続文字列を検索します。 追加した接続文字列によって、 *App\_Data*フォルダーにある*ContosoUniversity*という名前の LocalDB データベースが指定されます。 詳細については、「 [ASP.NET Web Applications の接続文字列の SQL Server](https://msdn.microsoft.com/library/jj653752.aspx)」を参照してください。

実際には、接続文字列を指定する必要はありません。 接続文字列を指定しない場合は、Entity Framework によって作成されます。ただし、アプリケーションの*アプリ\_データ*フォルダーにデータベースが存在しない可能性があります。 データベースを作成する場所の詳細については、「[新しいデータベースへの Code First](https://msdn.microsoft.com/data/jj193542)」を参照してください。

`connectionStrings` コレクションには、メンバーシップデータベースに使用される `DefaultConnection` という名前の接続文字列もあります。 このチュートリアルでは、メンバーシップデータベースを使用しません。 2つの接続文字列の唯一の違いは、データベース名と name 属性値です。

## <a name="set-up-and-execute-a-code-first-migration"></a>Code First の移行を設定して実行する

最初にアプリケーションの開発を開始すると、データモデルが頻繁に変更され、モデルが変更されるたびにデータベースとの同期がなくなります。 データモデルを変更するたびに、データベースを自動的に削除して再作成するように Entity Framework を構成することができます。 テストデータは簡単に作成できます。ただし、実稼働環境に配置した後は、通常、データベースを削除せずにデータベーススキーマを更新することをお勧めします。 移行機能を使用すると、Code First によってデータベースを削除および再作成せずに更新できます。 新しいプロジェクトの開発サイクルの初期段階では、 [Dropcreatedatabaseifmodelchanges](https://msdn.microsoft.com/library/gg679604(v=vs.103).aspx)を使用して、モデルが変更されるたびにデータベースを削除、再作成、および再シードすることができます。 アプリケーションをデプロイする準備ができたら、移行方法に変換することができます。 このチュートリアルでは、移行のみを使用します。 詳細については、「 [Code First Migrations](https://msdn.microsoft.com/data/jj591621)と[移行スクリーンキャスト Series](https://blogs.msdn.com/b/adonet/archive/2014/03/12/migrations-screencast-series.aspx)」を参照してください。

### <a name="enable-code-first-migrations"></a>Code First Migrations を有効にする

1. **[ツール]** メニューの **[NuGet パッケージマネージャー]** をクリックし、 **[パッケージマネージャーコンソール]** をクリックします。

    ![Selecting_Package_Manager_Console](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image10.png)
2. `PM>` プロンプトで、次のコマンドを入力します。

    [!code-powershell[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample9.ps1)]

    ![-移行コマンドを有効にする](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image11.png)

    このコマンドにより、ContosoUniversity プロジェクトに*移行*フォルダーが作成され、そのフォルダーに*Configuration.cs*ファイルが配置されます。このファイルを編集して、移行を構成することができます。

    ![移行フォルダー](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image12.png)

    `Configuration` クラスには、データベースの作成時とデータモデルの変更後に更新されるたびに呼び出される `Seed` メソッドが含まれています。

    [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample10.cs)]

    この `Seed` 方法の目的は、Code First 作成または更新した後に、テストデータをデータベースに挿入できるようにすることです。

### <a name="set-up-the-seed-method"></a>Seed メソッドを設定する

[Seed](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx)メソッドは、Code First Migrations によってデータベースが作成され、データベースが最新の移行に更新されるたびに実行されます。 シードメソッドの目的は、アプリケーションが初めてデータベースにアクセスする前に、テーブルにデータを挿入できるようにすることです。

以前のバージョンの Code First では、移行がリリースされる前に、`Seed` 方法でテストデータを挿入することが一般的でした。これは、開発時にすべてのモデルが変更されたため、データベースを完全に削除してから再作成する必要があるためです。 Code First Migrations を使用すると、データベースの変更後もテストデータが保持されるため、通常、 [Seed](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx)メソッドにテストデータを含める必要はありません。 実際、`Seed` 方法は運用環境で実行されるため、移行を使用してデータベースを運用環境に配置する場合は、`Seed` 方法でテストデータを挿入しないようにする必要があります。 その場合は、`Seed` メソッドを使用して、実稼働環境に挿入するデータのみをデータベースに挿入します。 たとえば、アプリケーションを運用環境で使用できるようになったときに、データベースに実際の部署名を `Department` テーブルに含めるようにすることができます。

このチュートリアルでは、配置のために移行を使用しますが、`Seed` 方法では、大量のデータを手動で挿入することなく、アプリケーションの機能がどのように動作するかを簡単に確認できるように、テストデータを挿入します。

1. *Configuration.cs*ファイルの内容を次のコードに置き換えます。これにより、テストデータが新しいデータベースに読み込まれます。 

    [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample11.cs)]

    [Seed](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx)メソッドは、データベースコンテキストオブジェクトを入力パラメーターとして受け取り、メソッドのコードはそのオブジェクトを使用して新しいエンティティをデータベースに追加します。 このコードは、エンティティ型ごとに新しいエンティティのコレクションを作成し、適切な[Dbset](https://msdn.microsoft.com/library/system.data.entity.dbset(v=vs.103).aspx)プロパティに追加して、変更をデータベースに保存します。 ここで行ったように、エンティティの各グループの後に[SaveChanges](https://msdn.microsoft.com/library/system.data.entity.dbcontext.savechanges(v=VS.103).aspx)メソッドを呼び出す必要はありませんが、コードがデータベースに書き込んでいる間に例外が発生した場合に、問題の原因を特定するのに役立ちます。

    データを挿入するステートメントの中には、 [Addorupdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx)メソッドを使用して "upsert" 操作を実行するものがあります。 `Seed` メソッドはすべての移行で実行されるため、データを挿入することはできません。これは、データベースを最初に移行した後に、追加しようとしている行が既に存在するためです。 "Upsert" 操作は、既に存在する行を挿入しようとすると発生するエラーを防ぎますが、アプリケーションのテスト中に行われたデータの変更を***上書き***します。 一部のテーブルのテストデータでは、このような処理が不要な場合があります。テスト中にデータを変更し、データベースの更新後も変更を保持する場合があります。 その場合は、条件付き挿入操作を実行します。行がまだ存在しない場合にのみ、行を挿入します。 Seed メソッドは、両方の方法を使用します。

    [Addorupdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx)メソッドに渡される最初のパラメーターは、行が既に存在するかどうかを確認するために使用するプロパティを指定します。 指定したテスト学生データに対しては、リスト内の各姓が一意であるため、この目的には `LastName` プロパティを使用できます。

    [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample12.cs)]

    このコードは、姓が一意であることを前提としています。 姓が重複する学生を手動で追加すると、次に移行を実行したときに次の例外が発生します。

    シーケンスに複数の要素が含まれています

    `AddOrUpdate` 方法の詳細については、「ジュリー Lerman のブログの[EF 4.3 AddOrUpdate メソッドに](http://thedatafarm.com/blog/data-access/take-care-with-ef-4-3-addorupdate-method/)対処する」を参照してください。

    `Enrollment` エンティティを追加するコードでは、`AddOrUpdate` メソッドは使用しません。 エンティティが既に存在するかどうかを確認し、エンティティが存在しない場合は挿入します。 この方法では、移行の実行時に登録グレードに加えた変更が保持されます。 このコードでは、`Enrollment`[リスト](https://msdn.microsoft.com/library/6sh2ey19.aspx)の各メンバーをループ処理します。登録がデータベースに見つからない場合は、データベースに登録が追加されます。 データベースを初めて更新すると、データベースは空になるため、各登録が追加されます。

    [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample13.cs)]

    `Seed` メソッドをデバッグする方法、および "アレクサンドロス Carson" という名前の2人の学生などの冗長データを処理する方法の詳細については、Rick Anderson のブログの「 [Entity Framework (EF) db のシード処理とデバッグ](https://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx)」を参照してください。
2. プロジェクトをビルドする。

### <a name="create-and-execute-the-first-migration"></a>最初の移行を作成して実行する

1. [パッケージマネージャーコンソール] ウィンドウで、次のコマンドを入力します。 

    [!code-powershell[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample14.ps1)]

    ![](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image13.png)

    `add-migration` コマンドは、データベースを作成するコードを含む *[Datestamp]\_InitialCreate.cs*ファイルを [移行] フォルダーに追加します。 最初のパラメーター (`InitialCreate)` はファイル名に使用され、任意のものを指定できます。通常は、移行中に実行される内容を要約する単語または語句を選択します。 たとえば、後で移行 &quot;AddDepartmentTable&quot;に名前を指定することができます。

    ![初期移行のある移行フォルダー](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image14.png)

    `InitialCreate` クラスの `Up` メソッドによって、データモデルのエンティティセットに対応するデータベーステーブルが作成され、`Down` メソッドによって削除されます。 移行は、`Up` メソッドを呼び出して、移行のためのデータ モデルの変更を実装します。 更新をロールバックするためのコマンドを入力すると、移行が `Down` メソッドを呼び出します。 次のコードは、`InitialCreate` ファイルの内容を示しています。

    [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample15.cs)]

    `update-database` コマンドは、`Up` メソッドを実行してデータベースを作成し、`Seed` メソッドを実行してデータベースにデータを読み込みます。

これで、データモデルの SQL Server データベースが作成されました。 データベースの名前は*ContosoUniversity*であり、 *.mdf*ファイルはプロジェクトの*App\_Data*フォルダーにあります。これは、接続文字列で指定したものです。

**サーバーエクスプローラー**または**SQL Server オブジェクトエクスプローラー** (ssox) のいずれかを使用して、Visual Studio でデータベースを表示できます。 このチュートリアルでは**サーバーエクスプローラー**を使用します。 Web 用 Visual Studio Express 2012 では、**サーバーエクスプローラー**は**データベースエクスプローラー**と呼ばれます。

1. **[表示]** メニューの **[サーバーエクスプローラー]** をクリックします。
2. **[接続の追加]** アイコンをクリックします。

    ![](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image15.png)
3. **[データソースの選択]** ダイアログボックスが表示されたら、 **[Microsoft SQL Server]** をクリックし、 **[続行]** をクリックします。  
  
    ![](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image16.png)
4. **[接続の追加]** ダイアログボックスで、**サーバー名**として **「(localdb) \ v11.0** 」と入力します。 **データベース名の選択または入力** で、ContosoUniversity を選択し**ます。**  
  
    ![](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image17.png)
5. [OK] をクリックします。
6. **[Schoolcontext.cs]** を展開し、 **[テーブル]** を展開します。  
  
    ![](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image18.png)
7. **Student**テーブルを右クリックし、 **[テーブルデータの表示]** をクリックして、作成された列とテーブルに挿入された行を確認します。

    ![Student テーブル](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image19.png)

## <a name="creating-a-student-controller-and-views"></a>学生のコントローラーとビューを作成する

次の手順では、これらのテーブルのいずれかを使用できる ASP.NET MVC コントローラーとビューをアプリケーションに作成します。

1. `Student` コントローラーを作成するには**ソリューションエクスプローラー**で **[コントローラー]** フォルダーを右クリックし、 **[追加]** をクリックして、 **[コントローラー]** をクリックします。 **[コントローラーの追加]** ダイアログボックスで、次の項目を選択し、 **[追加]** をクリックします。 

   - コントローラー名: **StudentController**。
   - テンプレート: **Entity Framework を使用した、読み取り/書き込みアクションとビューがある MVC コントローラー**。
   - モデルクラス: **Student (ContosoUniversity)** 。 (このオプションがドロップダウンリストに表示されない場合は、プロジェクトをビルドして、もう一度やり直してください。)
   - データコンテキストクラス: **schoolcontext.cs (ContosoUniversity)** 。
   - Views: **Razor (CSHTML)** 。 (既定値)。

     ![Add_Controller_dialog_box_for_Student_controller](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image20.png)
2. Visual Studio によって*Controllers\StudentController.cs*ファイルが開きます。 データベースコンテキストオブジェクトをインスタンス化するクラス変数が作成されていることがわかります。

     [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample16.cs)]

     `Index` アクションメソッドは、データベースコンテキストインスタンスの `Students` プロパティを読み取って、 *students*エンティティセットから学生のリストを取得します。

     [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample17.cs)]

     *Student\Index.cshtml*ビューでは、テーブルに次の一覧が表示されます。

     [!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample18.cshtml)]
3. Ctrl キーを押しながら F5 キーを押してプロジェクトを実行します。

     **[Students]** タブをクリックして、`Seed` メソッドによって挿入されたテストデータを表示します。

     ![学生用インデックスページ](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image21.png)

## <a name="conventions"></a>規約

Entity Framework が完全なデータベースを作成できるようにするために記述する必要があるコードの量は、*規則*を使用するか、Entity Framework が行う前提条件によって最小限に抑えられます。 これらの一部は既に記載されています。

- エンティティクラス名の複数化形式はテーブル名として使用されます。
- 列名には、エンティティ プロパティ名が使用されます。
- `ID` または*classname* `ID` という名前のエンティティプロパティは、主キーのプロパティとして認識されます。

規則を上書きできることがわかりました (たとえば、テーブル名を複数化にしないように指定した場合)。規則の詳細と、このシリーズの後半の「[より複雑なデータモデルの作成](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)」チュートリアルで規則をオーバーライドする方法について説明します。 詳細については、「 [Code First 規則](https://msdn.microsoft.com/data/jj679962)」を参照してください。

## <a name="summary"></a>要約

これで、Entity Framework と SQL Server Express を使用してデータを格納および表示する単純なアプリケーションが作成されました。 次のチュートリアルでは、基本的な CRUD (作成、読み取り、更新、削除) 操作を実行する方法について説明します。 このページの下部には、フィードバックを残しておくことができます。 チュートリアルのこの部分について、どのように改善できるかをお知らせください。

その他の Entity Framework リソースへのリンクについては、「 [ASP.NET Data Access Content Map](../../../../whitepapers/aspnet-data-access-content-map.md)」を参照してください。

> [!div class="step-by-step"]
> [次へ](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)
