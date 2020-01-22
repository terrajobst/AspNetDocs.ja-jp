---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application
title: 'チュートリアル: ASP.NET MVC 5 アプリで EF を使用して継承を実装する'
description: このチュートリアルでは、データ モデルで継承を実装する方法を示します。
author: tdykstra
ms.author: riande
ms.date: 01/21/2019
ms.topic: tutorial
ms.assetid: 08834147-77ec-454a-bb7a-d931d2a40dab
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 73a01ed47b0935a1a9734c197377470defb1fe36
ms.sourcegitcommit: 88fc80e3f65aebdf61ec9414810ddbc31c543f04
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/22/2020
ms.locfileid: "76519389"
---
# <a name="tutorial-implement-inheritance-with-ef-in-an-aspnet-mvc-5-app"></a>チュートリアル: ASP.NET MVC 5 アプリで EF を使用して継承を実装する

前のチュートリアルでは、同時実行例外を処理しています。 このチュートリアルでは、データ モデルで継承を実装する方法を示します。

オブジェクト指向プログラミングでは、[継承](http://en.wikipedia.org/wiki/Inheritance_(object-oriented_programming))を使用して[コードの再利用](http://en.wikipedia.org/wiki/Code_reuse)を容易にすることができます。 このチュートリアルでは、`Instructor` と `Student` クラスを `Person` 基底クラスから派生するように変更します。この基底クラスはインストラクターと受講者の両方に共通な `LastName` などのプロパティを含んでいます。 どの Web ページも追加または変更しませんが、コードの一部を変更し、それらの変更はデータベースに自動的に反映されます。

このチュートリアルでは、次の作業を行います。

> [!div class="checklist"]
> * 継承をデータベースにマップする方法について説明します。
> * Person クラスの作成
> * Instructor と Student を更新する
> * Person をモデルに追加する
> * 移行の作成と更新
> * 実装をテストする
> * Azure に配置する

## <a name="prerequisites"></a>Prerequisites

* [コンカレンシーの処理](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="map-inheritance-to-database"></a>継承をデータベースにマップする

`School` データモデルの `Instructor` クラスと `Student` クラスには、同一のいくつかのプロパティがあります。

![Student_and_Instructor_classes](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

`Instructor` エンティティと `Student` エンティティで共有されるプロパティの冗長なコードを削除すると仮定します。 または、インストラクターと学生のどちらから名前を取得したかに関係なく、名前をフォーマットできるサービスを記述するとします。 次の図に示すように、共有プロパティだけを含む `Person` 基本クラスを作成し、その基本クラスから `Instructor` と `Student` のエンティティを継承させることができます。

![Student_and_Instructor_classes_deriving_from_Person_class](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

データベースでこの継承構造を表すことができるいくつかの方法があります。 1つのテーブルに学生とインストラクターの両方に関する情報を含む `Person` テーブルを作成することもできます。 一部の列は、インストラクター (`HireDate`) にのみ適用されます。学生のみに (`EnrollmentDate`)、一部の列 (`LastName`、`FirstName`) にのみ適用されます。 通常、各行が表す型を示す*識別子*列があります。 たとえば、識別子列にインストラクターを示す "Instructor" と受講者を示す "Student" がある場合があります。

![Hierarchy_example あたりのテーブル数](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

1つのデータベーステーブルからエンティティの継承構造を生成するこのパターンは、*階層単位*(TPH) の継承と呼ばれます。

代わりに、継承構造と同じように見えるデータベースを作成することもできます。 たとえば、`Person` テーブルには name フィールドだけを指定し、`Instructor` テーブルと `Student` テーブルには日付フィールドを含めることができます。

![Table-per-type_inheritance](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

各エンティティクラスのデータベーステーブルを作成するこのパターンは、 *table per type* (TPT) 継承と呼ばれます。

他のオプションとして、個々のテーブルにすべての非抽象型をマップすることもできます。 継承されたプロパティを含むクラスのすべてのプロパティは、対応するテーブルの列にマップされます。 このパターンは、Table-per-Concrete Class (TPC) 継承と呼ばれます。 前に示したように、`Person`、`Student`、および `Instructor` クラスに対して TPC の継承を実装した場合、以前と比べて、`Student` テーブルと `Instructor` テーブルは、継承を実装した後に違いがないように見えます。

通常、TPC と TPH の継承パターンでは、TPT 継承パターンよりも Entity Framework でのパフォーマンスが向上します。これは、TPT パターンが複雑な結合クエリにつながる可能性があるためです。

このチュートリアルでは、TPH 継承の実装方法を示します。 TPH は Entity Framework の既定の継承パターンなので、`Person` クラスを作成し、`Person`から派生するように `Instructor` および `Student` クラスを変更し、新しいクラスを `DbContext`に追加して、移行を作成するだけです。 (他の継承パターンを実装する方法の詳細については、MSDN Entity Framework ドキュメントの「[テーブルごとのテーブル (TPT) の継承のマッピング](https://msdn.microsoft.com/data/jj591617#2.5)と、[具象クラス (TPC) の継承の](https://msdn.microsoft.com/data/jj591617#2.6)マッピング)」を参照してください。

## <a name="create-the-person-class"></a>Person クラスの作成

[*モデル*] フォルダーで*Person.cs*を作成し、テンプレートコードを次のコードに置き換えます。

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

## <a name="update-instructor-and-student"></a>Instructor と Student を更新する

次に、 *Instructor.cs*と*Student.cs*を更新して、 *Person.sc*から値を継承します。

*Instructor.cs*で、`Person` クラスから `Instructor` クラスを派生させ、key フィールドと name フィールドを削除します。 コードは次の例のように表示されます。

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

*Student.cs*に同様の変更を加えます。 `Student` クラスは次の例のようになります。

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

## <a name="add-person-to-the-model"></a>Person をモデルに追加する

*SchoolContext.cs*で、`Person` エンティティ型の `DbSet` プロパティを追加します。

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

Table-per-Hierarchy 継承を構成するために Entity Framework に必要なのことはこれですべてです。 ご覧のように、データベースが更新されると、`Student` テーブルと `Instructor` テーブルの代わりに `Person` テーブルが作成されます。

## <a name="create-and-update-migrations"></a>移行の作成と更新

パッケージマネージャーコンソール (PMC) で、次のコマンドを入力します。

`Add-Migration Inheritance`

PMC で `Update-Database` コマンドを実行します。 この時点では、移行によって処理方法がわからない既存のデータがあるため、このコマンドは失敗します。 次のようなエラーメッセージが表示されます。

> *オブジェクト ' dbo ' を削除できませんでした。インストラクターは、外部キー制約によって参照されています。*

移行を開いて *\&lt; timestamp&gt;\_Inheritance.cs*を開き、`Up` メソッドを次のコードに置き換えます。

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs)]

このコードは、次のデータベースの更新タスクを処理します。

- 外部キー制約と Student テーブルをポイントするインデックスを削除します。
- Instructor テーブルの名前の Person に変更し、Student データを格納するために必要な変更を加えます。

    - 受講者の null 許容 EnrollmentDate を追加します。
    - 行が、受講者かインストラクターかを示すために識別子列を追加します。
    - 受講者行には雇用日がないので HireDate を nul 許容にします。
    - 受講者をポイントする外部キーの更新に使用する一時的なフィールドを追加します。 学生を Person テーブルにコピーすると、新しい主キー値が取得されます。
- Student テーブルから Person テーブルにデータをコピーします。 これにより、受講者に新しい主キー値が割り当てられます。
- 受講者をポイントする外部キー値を修正します。
- 今は Person テーブルをポイントしている外部キー制約とインデックスを再作成します

(主キーの型として整数の代わりに GUID を使用した場合は、受講者の主キー値を変更する必要はなく、これらの手順のいくつかを省略できます)。

`update-database` コマンドをもう一度実行します。

(実稼働システムでは、以前のバージョンのデータベースに戻るために使用する必要があった場合に備えて、ダウンメソッドに対して、対応する変更を行います。 このチュートリアルでは、Down メソッドは使用しません)。

> [!NOTE]
> データを移行してスキーマを変更するときに、他のエラーが発生する可能性があります。 解決できない移行エラーが発生した場合は、 *web.config ファイルの*接続文字列を変更するか、データベースを削除することで、チュートリアルを続行できます。 最も簡単な方法*は、web.config ファイル内*のデータベースの名前を変更することです。 たとえば、次の例に示すように、データベース名を ContosoUniversity2 に変更します。
>
> [!code-xml[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.xml?highlight=2)]
>
> 新しいデータベースでは、移行するデータは存在せず、`update-database` のコマンドはエラーなしで完了する可能性が高くなります。 データベースを削除する方法については、「 [Visual Studio 2012 からデータベースを削除する方法](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/)」を参照してください。 このチュートリアルを続行するためにこの方法を使用する場合は、このチュートリアルの最後にあるデプロイ手順をスキップするか、新しいサイトとデータベースに配置してください。 既に展開している同じサイトに更新プログラムを展開した場合、自動的に移行を実行すると、EF によって同じエラーが返されます。 移行エラーのトラブルシューティングを行う場合は、Entity Framework フォーラムまたは StackOverflow.com のいずれかのリソースを使用することをお勧めします。

## <a name="test-the-implementation"></a>実装をテストする

サイトを実行し、さまざまなページを試してみてください。 すべてが前と同じように動作します。

**サーバーエクスプローラーで、** **[Data Connections\SchoolContext]** 、 **[Tables]** の順に展開し、 **Student**テーブルと**教師**テーブルが**Person**テーブルに置き換えられていることを確認します。 **Person**テーブルを展開すると、 **Student**テーブルと**教師**テーブルに使用されていたすべての列が含まれていることがわかります。

Person テーブルを右クリックし、 **[テーブル データの表示]** をクリックして識別子列を表示します。

次の図は、新しい School データベースの構造を示しています。

![School_database_diagram](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

## <a name="deploy-to-azure"></a>Azure に配置する

このセクションでは、このチュートリアルシリーズの[パート3、並べ替え、フィルター処理、およびページング](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md)に関するページの「 **Azure へのアプリのデプロイ**」セクションを完了している必要があります。 ローカルプロジェクトでデータベースを削除することによって解決した移行エラーが発生した場合は、この手順をスキップします。または、新しいサイトとデータベースを作成し、新しい環境にデプロイします。

1. Visual Studio の**ソリューション エクスプローラー**で、プロジェクトを右クリックし、コンテキスト メニューの **[発行]** をクリックします。

2. **[発行]** をクリックします。

    Web アプリが既定のブラウザーで開きます。

3. アプリケーションをテストして、動作していることを確認します。

    データベースにアクセスするページを初めて実行する場合、Entity Framework は、現在のデータモデルを使用してデータベースを最新の状態にするために必要なすべての移行 `Up` 方法を実行します。

## <a name="get-the-code"></a>コードを取得する

[完成したプロジェクトのダウンロード](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a>その他の技術情報

その他の Entity Framework リソースへのリンクについては、 [ASP.NET Data Access の推奨リソース](../../../../whitepapers/aspnet-data-access-content-map.md)を参照してください。

このとその他の継承構造の詳細については、MSDN の「 [TPT 継承パターン](https://msdn.microsoft.com/data/jj618293)と[TPH 継承パターン](https://msdn.microsoft.com/data/jj618292)」を参照してください。 次のチュートリアルでは、比較的高度なさまざまな Entity Framework のシナリオを処理する方法を説明します。

## <a name="next-steps"></a>次のステップ:

このチュートリアルでは、次の作業を行います。

> [!div class="checklist"]
> * 継承をデータベースにマップする方法について学習しました
> * Person クラスを作成した
> * Instructor と Student を更新した
> * モデルにユーザーを追加しました
> * 移行の作成と更新
> * 実装をテストした
> * Azure にデプロイ済み

次の記事に進み、Entity Framework Code First を使用する ASP.NET web アプリケーションの開発の基本について理解しておくと役立つトピックについて説明します。
> [!div class="nextstepaction"]
> [高度な Entity Framework シナリオ](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)
