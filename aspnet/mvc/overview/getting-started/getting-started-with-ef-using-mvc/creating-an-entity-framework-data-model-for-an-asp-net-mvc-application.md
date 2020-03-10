---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application
title: 'チュートリアル: MVC 5 を使用した Entity Framework 6 Code First の概要 |Microsoft Docs'
description: この一連のチュートリアルでは、データアクセスに Entity Framework 6 を使用する ASP.NET MVC 5 アプリケーションを構築する方法について説明します。
author: tdykstra
ms.author: riande
ms.date: 01/22/2019
ms.topic: tutorial
ms.assetid: 00bc8b51-32ed-4fd3-9745-be4c2a9c1eaf
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: a00a5a3aa295c2584b90abbf931c258c9e1b58ca
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78499408"
---
# <a name="tutorial-get-started-with-entity-framework-6-code-first-using-mvc-5"></a>チュートリアル: MVC 5 を使用した Entity Framework 6 Code First の概要

> [!NOTE]
> 新しい開発では、ASP.NET MVC コントローラーとビューを[ASP.NET Core Razor Pages](/aspnet/core/razor-pages)をお勧めします。 Razor Pages を使用したこの例に似たチュートリアルシリーズについては、「[チュートリアル: ASP.NET Core で Razor Pages](/aspnet/core/tutorials/razor-pages/razor-pages-start)の使用を開始する」を参照してください。 新しいチュートリアルは次のとおりです。
> * 理解しやすい。
> * より多くの EF Core のベスト プラクティスが提供されている。
> * より効率的なクエリを使用している。
> * より最新の API を使用している。
> * 多くの機能をカバーしている。
> * 新しいアプリケーションの開発で推奨されるアプローチである。

この一連のチュートリアルでは、データアクセスに Entity Framework 6 を使用する ASP.NET MVC 5 アプリケーションを構築する方法について説明します。 このチュートリアルでは、Code First ワークフローを使用します。 Code First、Database First、Model First の選択方法の詳細については、「[モデルを作成](/ef/ef6/modeling/)する」を参照してください。

このチュートリアルシリーズでは、Contoso 大学サンプルアプリケーションを構築する方法について説明します。 サンプルアプリケーションは、単純な大学の web サイトです。 これを使用すると、学生、コース、およびインストラクターの情報を表示および更新できます。 次の2つの画面を作成します。

![Students_Index_page](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image1.png)

![学生の編集](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image2.png)

このチュートリアルでは、次のことを行いました。

> [!div class="checklist"]
> * MVC web アプリを作成する
> * サイトのスタイルを設定する
> * Entity Framework 6 をインストールする
> * データ モデルを作成する
> * データベース コンテキストの作成
> * テスト データで DB を初期化する
> * LocalDB を使用するように EF 6 を設定する
> * コントローラーとビューを作成する
> * データベースを表示する

## <a name="prerequisites"></a>前提条件

* [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)

## <a name="create-an-mvc-web-app"></a>MVC web アプリを作成する

1. Visual Studio を開き、 C# **ASP.NET web アプリケーション (.NET Framework)** テンプレートを使用して web プロジェクトを作成します。 プロジェクトに*ContosoUniversity*という名前を指定し、[ **OK]** を選択します。

   ![Visual Studio の [新しいプロジェクト] ダイアログボックス](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/new-project-dialog.png)

1. **New ASP.NET Web Application-ContosoUniversity**で、 **[MVC]** を選択します。

   ![Visual Studio の [新しい web アプリ] ダイアログボックス](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/new-web-app-dialog.png)

    > [!NOTE]
    > 既定では、**認証**オプションは **[認証なし]** に設定されています。 このチュートリアルでは、web アプリでユーザーにサインインする必要はありません。 また、サインインしたユーザーに基づいてアクセスを制限することもありません。

1. **[OK]** を選択すると、プロジェクトが作成されます。

## <a name="set-up-the-site-style"></a>サイトのスタイルを設定する

簡単な変更をいくつか行い、サイトのメニュー、レイアウト、ホーム ページを決めます。

1. *Views\Shared\\_Layout*を開き、次のように変更します。

   - "My ASP.NET Application" と "Application name" の出現箇所をそれぞれ "Contoso 大学" に変更します。
   - 学生、コース、インストラクター、部署のメニューエントリを追加し、連絡先エントリを削除します。

   変更は、次のコードスニペットで強調表示されています。

   [!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample1.cshtml?highlight=6,19,24-27,38)]

2. *Views\Home\Index.cshtml*で、ファイルの内容を次のコードに置き換えて、ASP.NET と MVC に関するテキストをこのアプリケーションに関するテキストに置き換えます。

   [!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample2.cshtml)]

3. Ctrl キーを押しながら F5 キーを押して web サイトを実行します。 メインメニューが表示されたホームページが表示されます。

## <a name="install-entity-framework-6"></a>Entity Framework 6 をインストールする

1. **[ツール]** メニューの **[NuGet パッケージマネージャー]** を選択し、 **[パッケージマネージャーコンソール]** を選択します。

2. **[パッケージ マネージャー コンソール]** ウィンドウで、次のコマンドを入力します。

   ```text
   Install-Package EntityFramework
   ```

この手順は、このチュートリアルで手動で行うことができるいくつかの手順の1つですが、ASP.NET MVC のスキャフォールディング機能によって自動的に実行される可能性があります。 Entity Framework (EF) を使用するために必要な手順を確認できるように、手動で実行します。 スキャフォールディングを後で使用して、MVC コントローラーとビューを作成します。 別の方法として、スキャフォールディングを使用して EF NuGet パッケージを自動的にインストールし、データベースコンテキストクラスを作成して、接続文字列を作成する方法があります。 これを行う準備ができたら、これらの手順を省略し、エンティティクラスを作成した後に MVC コントローラーをスキャフォールディングするだけです。

## <a name="create-the-data-model"></a>データ モデルを作成する

次に、Contoso University アプリケーションのエンティティ クラスを作成します。 次の3つのエンティティから始めます。

**コース** <-> **登録** <-> **Student**

| [エンティティ] | リレーションシップ |
| -------- | ------------ |
| 登録のコース | 一対多 |
| 学生の登録 | 一対多 |

`Student` エンティティと `Enrollment` エンティティの間に一対多の関係があり、`Course` エンティティと `Enrollment` エンティティの間に一対多の関係があります。 言い換えると、1 人の学生をさまざまな講座に登録し、1 つの講座にたくさんの学生を登録できます。

以下のセクションでは、これらのエンティティのいずれかにクラスを作成します。

> [!NOTE]
> これらのエンティティクラスのすべての作成を完了する前にプロジェクトをコンパイルしようとすると、コンパイラエラーが発生します。

### <a name="the-student-entity"></a>Student エンティティ

- [*モデル*] フォルダーで、**ソリューションエクスプローラー**のフォルダーを右クリックし、[ > **クラス**の**追加**] を選択して、 *Student.cs*という名前のクラスファイルを作成します。 テンプレート コードを次のコードに置き換えます。

   [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample3.cs)]

`ID` プロパティは、このクラスに相当するデータベース テーブルの主キー列になります。 既定では、Entity Framework は `ID` または*classname* `ID` という名前のプロパティを主キーとして解釈します。

`Enrollments` プロパティは*ナビゲーション プロパティ*です。 ナビゲーション プロパティには、このエンティティに関連する他のエンティティが含まれます。 この場合、`Student` エンティティの `Enrollments` プロパティには、その `Student` エンティティに関連付けられているすべての `Enrollment` エンティティが保持されます。 言い換えると、データベース内の特定の `Student` 行に2つの関連する `Enrollment` 行 (その学生の主キー値が `StudentID` 外部キー列に含まれる行) がある場合、その `Student` エンティティの `Enrollments` ナビゲーションプロパティには、その2つの `Enrollment` エンティティが含まれます。

通常、ナビゲーションプロパティは、*遅延読み込み*などの特定の Entity Framework 機能を利用できるように `virtual` として定義されます。 (遅延読み込みについては、このシリーズの後の「[関連データの読み取り](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)」チュートリアルで後ほど説明します)。

ナビゲーション プロパティに複数のエンティティが含まれる場合 (多対多または一対多の関係で)、その型はリストにする必要があります。`ICollection` のように、エンティティを追加、削除、更新できるリストです。

### <a name="the-enrollment-entity"></a>Enrollment エンティティ

- *[Models]* フォルダーで、*Enrollment.cs* を作成し、既存のコードを次のコードに変更します。

   [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample4.cs)]

`EnrollmentID` プロパティは主キーになります。このエンティティは、`Student` エンティティで見たように `ID` ではなく*classname* `ID` パターンを使用します。 通常、パターンを 1 つ選択し、データ モデル全体でそれを使用します。 ここのバリエーションから、いずれのパターンも利用できることがわかります。 後のチュートリアルでは、`classname` を使用せずに `ID` を使用することにより、データモデルでの継承の実装を容易にする方法について説明します。

`Grade` プロパティは[列挙型](/ef/ef6/modeling/code-first/data-types/enums)です。 `Grade` の型宣言の後の疑問符は、`Grade` プロパティが [nullable](/dotnet/csharp/programming-guide/nullable-types/using-nullable-types) であることを示します。 Null のグレードは0グレードとは異なります。 null は、グレードが不明であるか、まだ割り当てられていないことを示します。

`StudentID` プロパティは外部キーです。それに対応するナビゲーション プロパティは `Student` です。 `Enrollment` エンティティは 1 つの `Student` エンティティに関連付けられており、1 つの `Student` エンティティだけを保持できます (先に見た、複数の `Student.Enrollments` エンティティを保持できる `Enrollment` ナビゲーション プロパティとは異なります)。

`CourseID` プロパティは外部キーです。それに対応するナビゲーション プロパティは `Course` です。 `Enrollment` エンティティは 1 つの `Course` エンティティに関連付けられます。

Entity Framework は、プロパティを外部キープロパティとして解釈します ( *&lt;ナビゲーションプロパティ名&gt;&lt;主キープロパティ名&gt;* (`StudentID` エンティティの主キーが `Student` であるために `Student` ナビゲーションプロパティの `ID`など)。 外部キープロパティの名前を同じにすることもできます。これは、*主キーのプロパティ名&gt;* (たとえば、`Course` エンティティの主キーが `CourseID`であるため `CourseID`)&lt;同じです。

### <a name="the-course-entity"></a>Course エンティティ

- [*モデル*] フォルダーで*Course.cs*を作成し、テンプレートコードを次のコードに置き換えます。

   [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample5.cs)]

`Enrollments` プロパティはナビゲーション プロパティです。 1 つの `Course` エンティティにたくさんの `Enrollment` エンティティを関連付けることができます。

<xref:System.ComponentModel.DataAnnotations.Schema.DatabaseGeneratedAttribute> 属性の詳細については、このシリーズの後のチュートリアルで説明します。 基本的に、この属性によって、講座の主キーをデータベースに生成させず、自分で入力できるようになります。

## <a name="create-the-database-context"></a>データベース コンテキストの作成

特定のデータモデルの Entity Framework 機能を調整するメインクラスは、*データベースコンテキスト*クラスです。 このクラスは、system.string[コンテキスト](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.113).aspx)クラスから派生させることによって作成します。 コードでは、データモデルに含めるエンティティを指定します。 Entity Framework の特定の動作をカスタマイズすることもできます。 このプロジェクトでは、クラスに `SchoolContext` という名前が付けられています。

- ContosoUniversity プロジェクトにフォルダーを作成するには、**ソリューションエクスプローラー**でプロジェクトを右クリックし、 **[追加]** をクリックして、 **[新しいフォルダー]** をクリックします。 新しいフォルダーに「 *DAL* 」という名前を指定します (データアクセス層の場合)。 そのフォルダーで、 *SchoolContext.cs*という名前の新しいクラスファイルを作成し、テンプレートコードを次のコードに置き換えます。

   [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample6.cs)]

### <a name="specify-entity-sets"></a>エンティティセットの指定

このコードでは、エンティティセットごとに[dbset](https://msdn.microsoft.com/library/system.data.entity.dbset(v=vs.113).aspx)プロパティを作成します。 Entity Framework 用語では、*エンティティセット*は通常、データベーステーブルに対応し、*エンティティ*はテーブル内の行に対応します。

> [!NOTE]
>
> `DbSet<Enrollment>` と `DbSet<Course>` ステートメントを省略すると、同じように動作します。 `Student` エンティティは `Enrollment` エンティティを参照し、`Enrollment` エンティティは `Course` エンティティを参照するため、Entity Framework に暗黙的に含まれます。

### <a name="specify-the-connection-string"></a>接続文字列を指定します

(後で web.config ファイルに追加する) 接続文字列の名前は、コンストラクターに渡されます。

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample7.cs?highlight=1)]

Web.config ファイルに格納されている名前ではなく、接続文字列自体を渡すこともできます。 使用するデータベースを指定するためのオプションの詳細については、「[接続文字列とモデル](/ef/ef6/fundamentals/configuring/connection-strings)」を参照してください。

接続文字列または1つの名前を明示的に指定しない場合、Entity Framework は、接続文字列名がクラス名と同じであると想定します。 この例の既定の接続文字列名は、明示的に指定したものと同じ `SchoolContext`になります。

### <a name="specify-singular-table-names"></a>単数形のテーブル名を指定する

[Onmodelcreating](https://msdn.microsoft.com/library/system.data.entity.dbcontext.onmodelcreating(v=vs.103).aspx)メソッドの `modelBuilder.Conventions.Remove` ステートメントを実行すると、テーブル名をにできなくなります。 この操作を行わないと、データベース内の生成されたテーブルの名前は `Students`、`Courses`、および `Enrollments`になります。 代わりに、テーブル名は `Student`、`Course`、および `Enrollment`になります。 テーブル名を複数形にするかどうかについては、開発者の間で意見が分かれるでしょう。 このチュートリアルでは単数形を使用しますが、重要な点は、このコード行を含めたり省略したりすることで、任意の形式を選択できることです。

## <a name="initialize-db-with-test-data"></a>テスト データで DB を初期化する

Entity Framework は、アプリケーションの実行時にデータベースを自動的に作成 (または削除して再作成) できます。 アプリケーションが実行されるたびに、またはモデルが既存のデータベースと同期しなくなったときにのみ実行するように指定できます。 また、データベースを作成した後に、テストデータを設定するために自動的にを呼び出す Entity Framework `Seed` メソッドを作成することもできます。

既定の動作では、データベースが存在しない場合にのみデータベースを作成します (モデルが変更され、データベースが既に存在する場合は例外をスローします)。 このセクションでは、モデルが変更されるたびにデータベースを削除して再作成するように指定します。 データベースを削除すると、すべてのデータが失われます。 `Seed` メソッドはデータベースが再作成されるときに実行され、テストデータが再作成されるため、これは通常、開発時には問題ありません。 しかし、実稼働環境では、データベーススキーマを変更する必要があるたびに、すべてのデータを失わないようにする必要があります。 後で、データベースを削除して再作成するのではなく、Code First Migrations を使用してデータベーススキーマを変更することにより、モデルの変更を処理する方法について説明します。

1. DAL フォルダーで、 *SchoolInitializer.cs*という名前の新しいクラスファイルを作成し、テンプレートコードを次のコードに置き換えます。これにより、必要に応じてデータベースが作成され、テストデータが新しいデータベースに読み込まれます。

   [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample8.cs)]

   `Seed` メソッドは、データベースコンテキストオブジェクトを入力パラメーターとして受け取ります。メソッドのコードは、そのオブジェクトを使用して新しいエンティティをデータベースに追加します。 このコードは、エンティティ型ごとに新しいエンティティのコレクションを作成し、適切な `DbSet` プロパティに追加してから、変更をデータベースに保存します。 ここで行ったように、エンティティの各グループの後に `SaveChanges` メソッドを呼び出す必要はありませんが、コードがデータベースに書き込んでいる間に例外が発生した場合に、問題の原因を特定するのに役立ちます。

2. 初期化子クラスを使用する Entity Framework を指定するには、次の例に示すように、アプリケーションの*web.config*ファイル (ルートプロジェクトフォルダー内の要素) の `entityFramework` 要素に要素を追加します。

   [!code-xml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample9.xml?highlight=2-6)]

   `context type` は、完全修飾コンテキストクラス名とそれが含まれるアセンブリを指定し、`databaseinitializer type` は初期化子クラスの完全修飾名とそれが含まれるアセンブリを指定します。 (EF で初期化子を使用しない場合は、`context` 要素で属性を設定できます: `disableDatabaseInitialization="true"`。)詳細については、「[構成ファイルの設定](/ef/ef6/fundamentals/configuring/config-file)」を参照してください。

   *Web.config ファイルで*初期化子を設定する代わりに、 *Global.asax.cs*ファイルの `Application_Start` メソッドに `Database.SetInitializer` ステートメントを追加することによって、コード内で初期化子を設定することもできます。 詳細については、「 [Entity Framework Code First でのデータベース初期化子につい](http://www.codeguru.com/csharp/article.php/c19999/Understanding-Database-Initializers-in-Entity-Framework-Code-First.htm)て」を参照してください。

これで、アプリケーションの特定の実行でデータベースに初めてアクセスしたときに、Entity Framework によってデータベースがモデル (`SchoolContext` とエンティティクラス) と比較されるようになりました。 違いがある場合は、アプリケーションによってデータベースが削除され、再作成されます。

> [!NOTE]
> アプリケーションを実稼働 web サーバーに配置する場合は、データベースを削除して再作成するコードを削除または無効にする必要があります。 これは、このシリーズの後のチュートリアルで行います。

## <a name="set-up-ef-6-to-use-localdb"></a>LocalDB を使用するように EF 6 を設定する

[LocalDB](/sql/database-engine/configure-windows/sql-server-2016-express-localdb?view=sql-server-2017)は、SQL Server Express データベースエンジンの軽量バージョンです。 インストールと構成が簡単で、オンデマンドで開始し、ユーザーモードで実行できます。 LocalDB は、 *.mdf*ファイルとしてデータベースを操作できるようにする SQL Server Express の特別な実行モードで実行されます。 プロジェクトと共にデータベースをコピーできるようにするには、web プロジェクトの*App\_Data*フォルダーに LocalDB データベースファイルを配置します。 SQL Server Express のユーザーインスタンス機能では、.mdf ファイルを使用することもでき*ます*が、ユーザーインスタンス機能は非推奨とされます。そのため、 *.mdf*ファイルを使用する場合は LocalDB をお勧めします。 LocalDB は、既定で Visual Studio と共にインストールされます。

通常、SQL Server Express は、運用 web アプリケーションでは使用されません。 LocalDB は、IIS で動作するように設計されていないため、web アプリケーションでの運用環境での使用は推奨されません。

- このチュートリアルでは、LocalDB を操作します。 次の例に示すように、アプリケーションの*web.config*ファイルを開き、`appSettings` 要素の前に `connectionStrings` 要素を追加します。 (ルートプロジェクトフォルダー*内の web.config ファイルを*必ず更新してください。 また、[ *Views* ] サブフォルダーには、更新する必要のない*web.config ファイルも*あります)。

   [!code-xml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample10.xml?highlight=1-3)]

追加した接続文字列は、Entity Framework が*ContosoUniversity1*という名前の LocalDB データベースを使用することを指定します。 (データベースはまだ存在しませんが、EF によって作成されます)。*アプリ\_データ*フォルダーにデータベースを作成する場合は、接続文字列に `AttachDBFilename=|DataDirectory|\ContosoUniversity1.mdf` を追加できます。 接続文字列の詳細については、「 [ASP.NET Web Applications の接続文字列の SQL Server](/previous-versions/aspnet/jj653752(v=vs.110))」を参照してください。

実際に*は、web.config ファイルに*接続文字列は必要ありません。 接続文字列を指定しない場合、Entity Framework は、コンテキストクラスに基づく既定の接続文字列を使用します。 詳細については、「[新しいデータベースへの Code First](/ef/ef6/modeling/code-first/workflows/new-database)」を参照してください。

## <a name="create-controller-and-views"></a>コントローラーとビューを作成する

次に、データを表示する web ページを作成します。 データを要求するプロセスによって、データベースの作成が自動的にトリガーされます。 まず、新しいコントローラーを作成します。 ただし、その前に、プロジェクトをビルドして、MVC コントローラーのスキャフォールディングでモデルとコンテキストクラスを使用できるようにします。

1. **ソリューションエクスプローラー**で **[Controllers]** フォルダーを右クリックし、 **[追加]** をポイントして、 **[新しいスキャフォールディング Item]** をクリックします。
2. **[スキャフォールディングの追加]** ダイアログボックスで、 **[MVC 5 コントローラー]** を選択し Entity Framework を使用して **[追加]** を選択します。

     ![Visual Studio での [スキャフォールディングの追加] ダイアログボックス](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/add-scaffold.png)

3. **[コントローラーの追加]** ダイアログボックスで、次の選択を行い、 **[追加]** を選択します。

   - モデルクラス: **Student (ContosoUniversity)** 。 (このオプションがドロップダウンリストに表示されない場合は、プロジェクトをビルドして、もう一度やり直してください。)
   - データコンテキストクラス: **schoolcontext.cs (ContosoUniversity)** 。
   - コントローラー名: **StudentController** (StudentsController ではありません)。
   - 他のフィールドの既定値はそのままにします。

     **[追加]** をクリックすると、scaffolder によって、コントローラーで動作する*StudentController.cs*ファイルと一連のビュー (*cshtml*ファイル) が作成されます。 今後 Entity Framework を使用するプロジェクトを作成するときに、scaffolder の追加機能を利用することもできます。最初のモデルクラスを作成し、接続文字列を作成せずに、 **[コントローラーの追加**] ボックスで **[データコンテキストクラス]** の横にある [ **+** ] ボタンを選択して**新しいデータコンテキスト**を指定します。 Scaffolder は、コントローラーとビューだけでなく、`DbContext` クラスと接続文字列を作成します。
4. Visual Studio によって*Controllers\StudentController.cs*ファイルが開きます。 データベースコンテキストオブジェクトをインスタンス化するクラス変数が作成されていることがわかります。

     [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample11.cs)]

     `Index` アクションメソッドは、データベースコンテキストインスタンスの `Students` プロパティを読み取って、 *students*エンティティセットから学生のリストを取得します。

     [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample12.cs)]

     *Student\Index.cshtml*ビューでは、テーブルに次の一覧が表示されます。

     [!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample13.cshtml)]
5. Ctrl キーを押しながら F5 キーを押してプロジェクトを実行します。 ("シャドウコピーを作成できません" というエラーが表示された場合は、ブラウザーを閉じて、もう一度やり直してください。)

     **[Students]** タブをクリックして、`Seed` メソッドによって挿入されたテストデータを表示します。 ブラウザーウィンドウの幅が狭いかどうかに応じて、上部のアドレスバーに [Student] タブのリンクが表示されます。または、右上隅をクリックしてリンクを表示する必要があります。

     ![メニューボタン](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image14.png)

## <a name="view-the-database"></a>データベースを表示する

[Students] ページを実行し、アプリケーションがデータベースにアクセスしようとすると、EF によってデータベースが作成されず、データベースが作成されていないことが検出されました。 EF は、seed メソッドを実行して、データベースにデータを設定します。

**サーバーエクスプローラー**または**SQL Server オブジェクトエクスプローラー** (ssox) のいずれかを使用して、Visual Studio でデータベースを表示できます。 このチュートリアルでは、**サーバーエクスプローラー**を使用します。

1. ブラウザーを閉じます。
2. **サーバーエクスプローラー**で、**データ接続** を展開し (最初に 更新 ボタンを選択する必要があります)、 **School Context (ContosoUniversity)** を展開し、**テーブル** を展開して、新しいデータベース内のテーブルを表示します。

3. **Student**テーブルを右クリックし、 **[テーブルデータの表示]** をクリックして、作成された列とテーブルに挿入された行を確認します。

4. **サーバーエクスプローラー**接続を閉じます。

*ContosoUniversity1*および *.ldf*データベースファイルは *% USERPROFILE%* フォルダーにあります。

`DropCreateDatabaseIfModelChanges` 初期化子を使用しているため、`Student` クラスを変更し、アプリケーションを再度実行すると、変更内容に合わせてデータベースが自動的に再作成されます。 たとえば、`Student` クラスに `EmailAddress` プロパティを追加した場合は、[Students] ページをもう一度実行し、もう一度テーブルを確認すると、新しい `EmailAddress` 列が表示されます。

## <a name="conventions"></a>規則

Entity Framework が完全なデータベースを作成できるようにするために記述する必要があるコードの量は、規則や Entity Framework によって*決まり*ます。 これらの一部は既にメモされているか、使用されていないことを認識していません。

- エンティティクラス名の複数化形式はテーブル名として使用されます。
- 列名には、エンティティ プロパティ名が使用されます。
- `ID` または*classname* `ID` という名前のエンティティプロパティは、主キーのプロパティとして認識されます。
- プロパティは外部キープロパティとして解釈されます。 *&lt;ナビゲーションプロパティ名&gt;&lt;主キープロパティ名&gt;* (たとえば、`StudentID` エンティティの主キーが `Student` であるために、`Student` ナビゲーションプロパティの `ID`) という名前が付けられている場合です。 外部キープロパティの名前を同じにすることもできます。これは、主キーのプロパティ名&gt; (たとえば、`Enrollment` エンティティの主キーが `EnrollmentID`であるため `EnrollmentID`) &lt;同じです。

この規則はオーバーライドできることがわかりました。 たとえば、テーブル名を複数化にしないように指定した場合、後でプロパティを外部キープロパティとして明示的にマークする方法がわかります。

## <a name="get-the-code"></a>コードの入手

[完成したプロジェクトのダウンロード](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a>その他のリソース

EF 6 の詳細については、次の記事を参照してください。

* [ASP.NET データ アクセス - 推奨リソース](../../../../whitepapers/aspnet-data-access-content-map.md)

* [Code First 規則](/ef/ef6/modeling/code-first/conventions/built-in)

* [より複雑なデータ モデルを作成する](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)

## <a name="next-steps"></a>次のステップ

このチュートリアルでは、次のことを行いました。

> [!div class="checklist"]
> * MVC web アプリを作成しました
> * サイトのスタイルを設定する
> * インストール済み Entity Framework 6
> * データ モデルを作成した
> * データベース コンテキストを作成した
> * テスト データで DB を初期化した
> * LocalDB を使用するように EF 6 を設定する
> * コントローラーとビューを作成した
> * データベースを表示した

次の記事に進み、コントローラーとビューの作成、読み取り、更新、削除 (CRUD) コードを確認し、カスタマイズする方法を学習してください。
> [!div class="nextstepaction"]
> [基本 CRUD 機能を実装する](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)