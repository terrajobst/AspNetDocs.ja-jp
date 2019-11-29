---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application
title: ASP.NET MVC アプリケーションでの Entity Framework による継承の実装 (8/10) |Microsoft Docs
author: tdykstra
description: Contoso 大学のサンプル web アプリケーションでは、Entity Framework 5 Code First と Visual Studio を使用して ASP.NET MVC 4 アプリケーションを作成する方法を示しています。
ms.author: riande
ms.date: 07/30/2013
ms.assetid: a5c3feff-5335-4cdd-a97d-f7a8785c2494
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 9507cba71b976825257cc9948d54f2651355959d
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74595319"
---
# <a name="implementing-inheritance-with-the-entity-framework-in-an-aspnet-mvc-application-8-of-10"></a>ASP.NET MVC アプリケーションでの Entity Framework による継承の実装 (8/10)

[Tom Dykstra](https://github.com/tdykstra)

[完成したプロジェクトのダウンロード](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Contoso 大学のサンプル web アプリケーションは、Entity Framework 5 Code First と Visual Studio 2012 を使用して ASP.NET MVC 4 アプリケーションを作成する方法を示しています。 チュートリアル シリーズについては、[シリーズの最初のチュートリアル](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)を参照してください。 チュートリアルシリーズは、最初から開始するか、[この章のスタートプロジェクトをダウンロード](building-the-ef5-mvc4-chapter-downloads.md)して開始することができます。
> 
> > [!NOTE] 
> > 
> > 解決できない問題が発生した場合は、完成した[章をダウンロード](building-the-ef5-mvc4-chapter-downloads.md)し、問題の再現を試みてください。 一般に、コードと完成したコードを比較することで、問題の解決策を見つけることができます。 一般的なエラーとその解決方法については、「[エラーと回避策](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)」を参照してください。

前のチュートリアルでは、同時実行例外を処理しています。 このチュートリアルでは、データ モデルで継承を実装する方法を示します。

オブジェクト指向プログラミングでは、継承を使用して冗長なコードを排除できます。 このチュートリアルでは、`Instructor` と `Student` クラスを `Person` 基底クラスから派生するように変更します。この基底クラスはインストラクターと受講者の両方に共通な `LastName` などのプロパティを含んでいます。 どの Web ページも追加または変更しませんが、コードの一部を変更し、それらの変更はデータベースに自動的に反映されます。

## <a name="table-per-hierarchy-versus-table-per-type-inheritance"></a>階層ごとのテーブルと型ごとの継承の比較

オブジェクト指向プログラミングでは、継承を使用して、関連するクラスを簡単に操作できるようになります。 たとえば、`School` データモデルの `Instructor` クラスと `Student` クラスは、次のようないくつかのプロパティを共有します。これにより、冗長なコードが生成されます。

![Student_and_Instructor_classes](https://asp.net/media/2578113/Windows-Live-Writer_58f5a93579b2_CC7B_Student_and_Instructor_classes_e7a32f99-8bc4-48ce-aeaf-216a18071a8b.png)

`Instructor` エンティティと `Student` エンティティで共有されるプロパティの冗長なコードを削除すると仮定します。 次の図に示すように、共有プロパティだけを含む `Person` 基本クラスを作成し、その基本クラスから `Instructor` と `Student` のエンティティを継承させることができます。

![Student_and_Instructor_classes_deriving_from_Person_class](https://asp.net/media/2578119/Windows-Live-Writer_58f5a93579b2_CC7B_Student_and_Instructor_classes_deriving_from_Person_class_671d708c-cbb8-454a-a8f8-c2d99439acd9.png)

データベースでこの継承構造を表すことができるいくつかの方法があります。 1つのテーブルに学生とインストラクターの両方に関する情報を含む `Person` テーブルを作成することもできます。 一部の列は、インストラクター (`HireDate`) にのみ適用されます。学生のみに (`EnrollmentDate`)、一部の列 (`LastName`、`FirstName`) にのみ適用されます。 通常、各行が表す型を示す*識別子*列があります。 たとえば、識別子列にインストラクターを示す "Instructor" と受講者を示す "Student" がある場合があります。

![Hierarchy_example あたりのテーブル数](https://asp.net/media/2578125/Windows-Live-Writer_58f5a93579b2_CC7B_Table-per-hierarchy_example_244067cd-b451-4e9b-9595-793b9afca505.png)

1つのデータベーステーブルからエンティティの継承構造を生成するこのパターンは、*階層単位*(TPH) の継承と呼ばれます。

代わりに、継承構造と同じように見えるデータベースを作成することもできます。 たとえば、`Person` テーブルには name フィールドだけを指定し、`Instructor` テーブルと `Student` テーブルには日付フィールドを含めることができます。

![Type_inheritance あたりのテーブル数](https://asp.net/media/2578131/Windows-Live-Writer_58f5a93579b2_CC7B_Table-per-type_inheritance.png)

各エンティティクラスのデータベーステーブルを作成するこのパターンは、 *table per type* (TPT) 継承と呼ばれます。

TPH 継承パターンを使用すると、一般に、TPT 継承パターンよりも Entity Framework でパフォーマンスが向上します。 TPT パターンでは、複雑な結合クエリが発生する可能性があるためです。 このチュートリアルでは、TPH 継承の実装方法を示します。 これを行うには、次の手順を実行します。

- `Person` クラスを作成し、`Person`から派生するように `Instructor` および `Student` クラスを変更します。
- データベースコンテキストクラスにモデルとデータベースのマッピングコードを追加します。
- プロジェクト全体で `InstructorID` および `StudentID` 参照を変更して `PersonID`します。

## <a name="creating-the-person-class"></a>Person クラスの作成

 注: これらのクラスを使用するコントローラーを更新するまで、以下のクラスを作成した後にプロジェクトをコンパイルすることはできません。 

[*モデル*] フォルダーで*Person.cs*を作成し、テンプレートコードを次のコードに置き換えます。

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

*Instructor.cs*で、`Person` クラスから `Instructor` クラスを派生させ、key フィールドと name フィールドを削除します。 コードは次の例のように表示されます。

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

*Student.cs*に同様の変更を加えます。 `Student` クラスは次の例のようになります。

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

## <a name="adding-the-person-entity-type-to-the-model"></a>Person エンティティ型をモデルに追加する

*SchoolContext.cs*で、`Person` エンティティ型の `DbSet` プロパティを追加します。

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

Table-per-Hierarchy 継承を構成するために Entity Framework に必要なのことはこれですべてです。 ご覧のように、データベースを再作成すると、`Student` テーブルと `Instructor` テーブルの代わりに `Person` テーブルが作成されます。

## <a name="changing-instructorid-and-studentid-to-personid"></a>InstructorID と StudentID を PersonID に変更する

*SchoolContext.cs*のインストラクター-講座マッピングステートメントで、`MapRightKey("InstructorID")` を `MapRightKey("PersonID")`に変更します。

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs?highlight=4)]

この変更は必要ありません。これは、多対多の結合テーブルの InstructorID 列の名前を変更するだけです。 名前を InstructorID として残した場合でも、アプリケーションは正常に動作します。 完成した*SchoolContext.cs*は次のようになります。

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs?highlight=15,24)]

次に、`InstructorID` を `PersonID` に変更し、[*移行*] フォルダー内のタイムスタンプ付きの移行ファイルを***除き***、プロジェクト全体で `PersonID` に `StudentID` する必要があります。 これを行うには、変更する必要があるファイルのみを見つけて開き、開いたファイルに対してグローバルな変更を実行します。 変更する必要がある*移行*フォルダー内のファイルは*Migrations\Configuration.cs.* だけです。

1. > [!IMPORTANT]
   > まず、Visual Studio で開いているすべてのファイルを閉じます。
2. **検索と置換** をクリックし、**編集** メニューの すべてのファイルを検索 をクリックし、`InstructorID`を含むプロジェクト内のすべてのファイルを検索します。  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)
3. **[検索結果]** ウィンドウで各ファイルを開きます。***ただし***、[*マイグレー*ション] フォルダーにある [&lt;タイムスタンプ&gt; *\_* ] をクリックして、各ファイルの1行をダブルクリックします。  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)
4. [**フォルダーを**選択して置換] ダイアログを開き、開いている**すべてのドキュメント**に移動します。
5. [フォルダーを選択して**置換**] ダイアログボックスを使用して、すべての `InstructorID` を `PersonID.` に変更します。  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)
6. `StudentID`が含まれているプロジェクト内のすべてのファイルを検索します。
7. **検索結果** ウィンドウで各ファイルを開きます。***ただし*** *、migration フォルダーに*ある &lt;タイムスタンプ&gt; *\_\** の場合は、各ファイルの1行をダブルクリックします。  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)
8. [**フォルダーを**選択して置換] ダイアログを開き、開いている**すべてのドキュメント**に移動します。
9. [**フォルダーを**選択して置換] ダイアログボックスを使用すると、すべての `StudentID` を `PersonID`に変更できます。   
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)
10. プロジェクトをビルドする。

(これは、主キーの名前付けに `classnameID` パターンの*欠点*を示すことに注意してください。 クラス名の前にプレフィックスを付けずに主キー ID を指定した場合は、名前を変更する必要は*ありません*)。

## <a name="create-and-update-a-migrations-file"></a>移行ファイルを作成および更新する

パッケージマネージャーコンソール (PMC) で、次のコマンドを入力します。

`Add-Migration Inheritance`

PMC で `Update-Database` コマンドを実行します。 この時点では、移行によって処理方法がわからない既存のデータがあるため、このコマンドは失敗します。 次のエラーが表示されます。

*ALTER TABLE ステートメントが FOREIGN KEY 制約 "FK\_dbo と競合しています。Department\_dbo です。Person\_PersonID "。データベース "ContosoUniversity"、テーブル "dbo で競合が発生しました。Person ", column ' PersonID '。*

移行を開いて *\&lt; timestamp&gt;\_Inheritance.cs*を開き、`Up` メソッドを次のコードに置き換えます。

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs?highlight=25,29-40)]

`update-database` コマンドをもう一度実行します。

> [!NOTE]
> データを移行してスキーマを変更するときに、他のエラーが発生する可能性があります。 解決できない移行エラーが発生した場合*は、web.config ファイルの*接続文字列を変更するか、データベースを削除することで、チュートリアルを続行できます。 最も簡単な方法*は、web.config ファイル内*のデータベースの名前を変更することです。 たとえば、次の例に示すように、データベース名を CU\_test に変更します。
> 
> [!code-xml[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.xml?highlight=1-2)]
> 
> 新しいデータベースでは、移行するデータは存在せず、`update-database` のコマンドはエラーなしで完了する可能性が高くなります。 データベースを削除する方法については、「 [Visual Studio 2012 からデータベースを削除する方法](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/)」を参照してください。 このチュートリアルを続行するには、このチュートリアルの最後にあるデプロイ手順をスキップします。これは、展開されたサイトが移行を自動的に実行するときに、同じエラーが発生するためです。 移行エラーのトラブルシューティングを行う場合は、Entity Framework フォーラムまたは StackOverflow.com のいずれかのリソースを使用することをお勧めします。

## <a name="testing"></a>Testing (テスト)

サイトを実行し、さまざまなページを試してみてください。 すべてが前と同じように動作します。

**サーバーエクスプローラーで、** **[schoolcontext.cs]** 、 **[Tables]** の順に展開し、 **Student**テーブルと**教師**テーブルが**Person**テーブルに置き換えられていることを確認します。 **Person**テーブルを展開すると、 **Student**テーブルと**教師**テーブルに使用されていたすべての列が含まれていることがわかります。

![Server_Explorer_showing_Person_table](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

Person テーブルを右クリックし、 **[テーブル データの表示]** をクリックして識別子列を表示します。

![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

次の図は、新しい School データベースの構造を示しています。

![School_database_diagram](https://asp.net/media/2578143/Windows-Live-Writer_58f5a93579b2_CC7B_School_database_diagram_6350a801-7199-413f-bbac-4a2009ed19d7.png)

## <a name="summary"></a>要約

`Person`、`Student`、および `Instructor` の各クラスに対して、階層構造の継承が実装されました。 このとその他の継承構造の詳細については、「Morteza Manavi のブログの[継承マッピング方法](https://weblogs.asp.net/manavi/archive/2010/12/24/inheritance-mapping-strategies-with-entity-framework-code-first-ctp5-part-1-table-per-hierarchy-tph.aspx)」を参照してください。 次のチュートリアルでは、リポジトリと作業単位パターンを実装するいくつかの方法について説明します。

その他の Entity Framework リソースへのリンクについては、「 [ASP.NET Data Access Content Map](../../../../whitepapers/aspnet-data-access-content-map.md)」を参照してください。

> [!div class="step-by-step"]
> [前へ](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)
> [次へ](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md)
