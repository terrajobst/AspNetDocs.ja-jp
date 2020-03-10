---
uid: web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started
title: 'Entity Framework 4.0 と ObjectDataSource コントロールを使用して、パート 1: はじめに |Microsoft Docs'
author: tdykstra
description: このチュートリアルシリーズは、Entity Framework チュートリアルシリーズを使用してはじめにによって作成された Contoso 大学 web アプリケーションに基づいています。 If...
ms.author: riande
ms.date: 01/26/2011
ms.assetid: 244278c1-fec8-4255-8a8a-13bde491c4f5
msc.legacyurl: /web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started
msc.type: authoredcontent
ms.openlocfilehash: 2f14707eb058d438495dd2bc4c17b976c471fc97
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78440404"
---
# <a name="using-the-entity-framework-40-and-the-objectdatasource-control-part-1-getting-started"></a>Entity Framework 4.0 と ObjectDataSource コントロールを使用して、パート 1: はじめに

[Tom Dykstra](https://github.com/tdykstra)

> このチュートリアルシリーズは、 [Entity Framework 4.0 チュートリアルシリーズを使用](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md)してはじめにによって作成された Contoso 大学 web アプリケーションに基づいています。 前のチュートリアルを完了していない場合は、このチュートリアルの開始点として、作成した[アプリケーションをダウンロード](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a)できます。 チュートリアルシリーズ全体で作成した[アプリケーションをダウンロード](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa)することもできます。
> 
> Contoso 大学のサンプル web アプリケーションは、Entity Framework 4.0 と Visual Studio 2010 を使用して ASP.NET Web フォームアプリケーションを作成する方法を示しています。 サンプルアプリケーションは、架空の Contoso 大学の web サイトです。 学生の受け付け、講座の作成、講師の割り当てなどの機能が含まれています。
> 
> このチュートリアルでは、 C#の例を示します。 ダウンロード可能な[サンプル](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa)には、 C#と Visual Basic の両方のコードが含まれています。
> 
> ## <a name="database-first"></a>Database First
> 
> Entity Framework のデータを操作するには、 *Database First*、 *Model First*、および*Code First*の3つの方法があります。 このチュートリアルは Database First を対象としています。 これらのワークフローの違いと、シナリオに最適なワークフローを選択する方法については、「 [Entity Framework 開発ワークフロー](https://msdn.microsoft.com/library/ms178359.aspx#dbfmfcf)」を参照してください。
> 
> ## <a name="web-forms"></a>Web フォーム
> 
> はじめにシリーズと同様に、このチュートリアルシリーズでは ASP.NET Web フォームモデルを使用しており、Visual Studio で ASP.NET Web フォームを操作する方法を理解していることを前提としています。 そうでない場合は、「[はじめにと ASP.NET 4.5 Web フォーム](../../getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview.md)」を参照してください。 ASP.NET MVC フレームワークを使用する場合は、「 [ASP.NET mvc を使用した Entity Framework でのはじめに](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)」を参照してください。
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

`EntityDataSource` コントロールを使用すると、アプリケーションを非常に短時間で作成できますが、通常は、 *.aspx*ページで大量のビジネスロジックとデータアクセスロジックを保持する必要があります。 アプリケーションが複雑さを増し、継続的なメンテナンスを必要とする場合は、より保守しやすい*n 層* *または複数層の*アプリケーション構造を作成するために、より多くの開発時間を事前に投資することができます。 このアーキテクチャを実装するには、プレゼンテーション層をビジネスロジック層 (BLL) とデータアクセス層 (DAL) から分離します。 この構造体を実装する方法の1つは、`EntityDataSource` コントロールではなく、`ObjectDataSource` コントロールを使用することです。 `ObjectDataSource` コントロールを使用する場合は、独自のデータアクセスコードを実装し、他のデータソースコントロールと同じ機能の多くを持つコントロールを使用して *.aspx*ページで呼び出すことができます。 これにより、データアクセスに Web フォームコントロールを使用する利点と比較して、n 層アプローチの利点を組み合わせることができます。

`ObjectDataSource` コントロールを使用すると、他の方法でも柔軟性を高めることができます。 独自のデータアクセスコードを記述するので、特定のエンティティ型を読み取り、挿入、更新、または削除するだけでなく、`EntityDataSource` コントロールが実行するように設計されたタスクでも、より簡単に行うことができます。 たとえば、エンティティが更新されるたびにログ記録を実行したり、エンティティが削除されるたびにデータをアーカイブしたり、外部キー値を持つ行を挿入するときに必要に応じて関連データを自動的にチェックおよび更新したりすることができます。

## <a name="business-logic-and-repository-classes"></a>ビジネスロジックとリポジトリクラス

`ObjectDataSource` コントロールは、作成したクラスを呼び出すことによって機能します。 クラスには、データを取得および更新するメソッドが含まれています。また、これらのメソッドの名前をマークアップの `ObjectDataSource` コントロールに指定します。 レンダリングまたはポストバック処理中に、`ObjectDataSource` は指定したメソッドを呼び出します。

基本的な CRUD 操作に加えて、`ObjectDataSource` コントロールで使用するために作成するクラスは、`ObjectDataSource` がデータを読み取りまたは更新するときにビジネスロジックを実行することが必要になる場合があります。 たとえば、部門を更新するときに、1人のユーザーが複数の部門の管理者になることができないため、他の部署が同じ管理者を持っていないことを検証する必要がある場合があります。

[ObjectDataSource クラスの概要](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.aspx)など、一部の `ObjectDataSource` ドキュメントでは、コントロールはビジネスロジックとデータアクセスロジックの両方を含む*ビジネスオブジェクト*と呼ばれるクラスを呼び出します。 このチュートリアルでは、ビジネスロジックとデータアクセスロジックに個別のクラスを作成します。 データアクセスロジックをカプセル化するクラスは、*リポジトリ*と呼ばれます。 ビジネスロジッククラスには、ビジネスロジックメソッドとデータアクセスメソッドの両方が含まれていますが、データアクセスメソッドはリポジトリを呼び出してデータアクセスタスクを実行します。

また、bll の自動単体テストを容易にする、BLL と DAL の間に抽象レイヤーを作成します。 この抽象化レイヤーは、ビジネスロジッククラスでリポジトリをインスタンス化するときに、インターフェイスを作成し、インターフェイスを使用することによって実装されます。 これにより、リポジトリインターフェイスを実装するオブジェクトへの参照をビジネスロジッククラスに提供できるようになります。 通常の操作では、Entity Framework と連携するリポジトリオブジェクトを指定します。 テストでは、コレクションとして定義されているクラス変数など、簡単に操作できる方法で格納されたデータを処理するリポジトリオブジェクトを提供します。

次の図は、リポジトリを使用しないデータアクセスロジックとリポジトリを使用するビジネスロジッククラスの違いを示しています。

[![Image05](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image2.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image1.png)

まず、基本的なデータアクセスタスクのみを実行するため、`ObjectDataSource` コントロールがリポジトリに直接バインドされている web ページを作成します。 次のチュートリアルでは、検証ロジックを使用してビジネスロジッククラスを作成し、リポジトリクラスではなく、そのクラスに `ObjectDataSource` コントロールをバインドします。 また、検証ロジックの単体テストも作成します。 このシリーズの3番目のチュートリアルでは、アプリケーションに並べ替えとフィルター処理の機能を追加します。

このチュートリアルで作成するページは、[はじめにチュートリアルシリーズ](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md)で作成したデータモデルの `Departments` エンティティセットに対応しています。

[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image4.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image3.png)

[![Image02](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image6.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image5.png)

## <a name="updating-the-database-and-the-data-model"></a>データベースとデータモデルの更新

このチュートリアルを開始するには、データベースに2つの変更を加えます。どちらも、 [Entity Framework および Web フォームのチュートリアルではじめに](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md)で作成したデータモデルに対応する変更を必要とします。 これらのチュートリアルでは、データベースが変更された後に、デザイナーで手動で変更を行って、データモデルをデータベースと同期させました。 このチュートリアルでは、データベースツールのデザイナーの**更新モデル**を使用して、データモデルを自動的に更新します。

### <a name="adding-a-relationship-to-the-database"></a>データベースへのリレーションシップの追加

Visual Studio で、 [Entity Framework および Web フォーム](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md)チュートリアルシリーズを使用してはじめにで作成した Contoso 大学 web アプリケーションを開き、`SchoolDiagram` データベースダイアグラムを開きます。

データベースダイアグラムの `Department` テーブルを見ると、`Administrator` 列があることがわかります。 この列は `Person` テーブルに対する外部キーですが、データベースに外部キーリレーションシップが定義されていません。 リレーションシップを作成し、データモデルを更新して、Entity Framework がこのリレーションシップを自動的に処理できるようにする必要があります。

データベースダイアグラムで、`Department` テーブルを右クリックし、 **[リレーションシップ]** をクリックします。

[![Image80](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image8.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image7.png)

**[外部キーのリレーションシップ]** ボックスで **[追加]** をクリックし、 **[テーブルと列の指定]** の省略記号をクリックします。

[![Image81](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image10.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image9.png)

**[テーブルと列]** ダイアログボックスで、主キーのテーブルとフィールドを `Person` と `PersonID`に設定し、外部キーのテーブルとフィールドを `Department` および `Administrator`に設定します。 (これを行うと、リレーションシップ名が `FK_Department_Department` から `FK_Department_Person`に変わります)。

[![Image82](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image12.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image11.png)

**[テーブルと列]** ボックスの **[OK]** をクリックし、 **[外部キーのリレーションシップ]** ボックスの **[閉じる]** をクリックして、変更を保存します。 `Person` テーブルと `Department` テーブルを保存するかどうかを確認するメッセージが表示されたら、 **[はい]** をクリックします。

> [!NOTE]
> `Administrator` 列に既に存在するデータに対応する `Person` 行を削除した場合、この変更を保存することはできません。 その場合は、**サーバーエクスプローラー**のテーブルエディターを使用して、すべての `Department` 行の `Administrator` 値に、`Person` テーブルに実際に存在するレコードの ID が含まれていることを確認してください。
> 
> 変更を保存した後、そのユーザーが部門の管理者である場合、`Person` テーブルから行を削除することはできません。 実稼働アプリケーションでは、データベースの制約によって削除が禁止されている場合、または連鎖削除を指定した場合に、特定のエラーメッセージが表示されます。 連鎖削除を指定する方法の例については、「 [Entity Framework と ASP.NET –はじめにパート 2](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-2.md)」を参照してください。

### <a name="adding-a-view-to-the-database"></a>データベースへのビューの追加

作成*する新しい department*ページで、ユーザーが部門管理者を選択できるように、講師のドロップダウンリストを "last, first" の形式で入力します。 この操作を簡単に行うには、データベースにビューを作成します。 ビューは、ドロップダウンリストに必要なデータのみで構成されます。完全な名前 (正しい形式) とレコードキーです。

**サーバーエクスプローラー**で、[ *School .mdf*] を展開し、 **[ビュー]** フォルダーを右クリックして、 **[新しいビューの追加]** を選択します。

[![Image06](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image14.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image13.png)

**[テーブルの追加]** ダイアログボックスが表示されたら **[閉じる]** をクリックし、sql ペインに次の sql ステートメントを貼り付けます。

[!code-sql[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample1.sql)]

ビューを `vInstructorName`として保存します。

### <a name="updating-the-data-model"></a>データモデルの更新

*DAL*フォルダーで、 *SchoolModel*ファイルを開き、デザイン画面を右クリックして、 **[データベースからモデルを更新]** を選択します。

[![Image07](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image16.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image15.png)

**[データベースオブジェクトの選択]** ダイアログボックスで、 **[追加]** タブを選択し、先ほど作成したビューを選択します。

[![Image08](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image18.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image17.png)

**[完了]** をクリックします。

デザイナーでは、このツールによって、`vInstructorName` エンティティと、`Department` エンティティと `Person` エンティティの間の新しいアソシエーションが作成されたことがわかります。

[![Image13](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image20.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image19.png)

> [!NOTE]
> **[出力]** ウィンドウと **[エラー一覧]** ウィンドウに、ツールによって新しい `vInstructorName` ビューの主キーが自動的に作成されたことを知らせる警告メッセージが表示される場合があります。 これは正しい動作です。

コードで新しい `vInstructorName` エンティティを参照する場合、小文字の "v" にプレフィックスとして付けるデータベース規則を使用しないことをお勧めします。 そのため、モデル内のエンティティとエンティティセットの名前を変更します。

**モデルブラウザー**を開きます。 エンティティ型とビュー `vInstructorName` 表示されます。

[![Image14](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image22.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image21.png)

[ **SchoolModel** ( **SchoolModel**)] で、 **[vInstructorName]** を右クリックし、 **[プロパティ]** を選択します。 **[プロパティ]** ウィンドウで、 **[名前]** プロパティを "InstructorName" に変更し、 **[エンティティセット名]** プロパティを "InstructorNames" に変更します。

[![Image15](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image24.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image23.png)

データモデルを保存して閉じてから、プロジェクトをリビルドします。

## <a name="using-a-repository-class-and-an-objectdatasource-control"></a>リポジトリクラスと ObjectDataSource コントロールの使用

*DAL*フォルダーに新しいクラスファイルを作成し、 *SchoolRepository.cs*という名前を付けて、既存のコードを次のコードに置き換えます。

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample2.cs)]

このコードは、`Departments` エンティティセット内のすべてのエンティティを返す1つの `GetDepartments` メソッドを提供します。 返されるすべての行の `Person` ナビゲーションプロパティにアクセスすることがわかっているので、`Include` メソッドを使用して、そのプロパティの一括読み込みを指定します。 また、クラスは、オブジェクトが破棄されたときにデータベース接続が解放されるように、`IDisposable` インターフェイスも実装します。

> [!NOTE]
> 一般的な方法は、エンティティ型ごとにリポジトリクラスを作成することです。 このチュートリアルでは、複数のエンティティ型に対して1つのリポジトリクラスを使用します。 リポジトリパターンの詳細については、 [Entity Framework チームのブログ](https://blogs.msdn.com/b/adonet/archive/2009/06/16/using-repository-and-unit-of-work-patterns-with-entity-framework-4-0.aspx)と[ジュリー Lerman のブログ](http://thedatafarm.com/blog/data-access/agile-ef4-repository-part-3-fine-tuning-the-repository/)で投稿を参照してください。

`GetDepartments` メソッドは、リポジトリオブジェクト自体が破棄された後でも返されたコレクションが使用可能であることを確認するために、`IQueryable` オブジェクトではなく `IEnumerable` オブジェクトを返します。 `IQueryable` オブジェクトは、アクセスされるたびにデータベースへのアクセスが発生する可能性がありますが、データの表示を試みたときにリポジトリオブジェクトが破棄される可能性があります。 `IEnumerable` オブジェクトではなく、`IList` オブジェクトなど、別のコレクション型を返すこともできます。 ただし、`IEnumerable` オブジェクトを返すと、`foreach` ループや LINQ クエリなどの一般的な読み取り専用のリスト処理タスクを実行できますが、コレクション内のアイテムを追加したり削除したりすることはできません。このような変更がデータベースに保存される可能性があります。

*.Master*マスターページを使用する department *.aspx*ページを作成し、`Content2`という名前の `Content` コントロールに次のマークアップを追加します。

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample3.aspx)]

このマークアップは、先ほど作成したリポジトリクラスを使用する `ObjectDataSource` コントロールと、データを表示するための `GridView` コントロールを作成します。 `GridView` コントロールでは、 **Edit**コマンドと**Delete**コマンドが指定されていますが、まだサポートするためのコードは追加されていません。

いくつかの列では、データの自動書式設定と検証機能を利用できるように `DynamicField` コントロールを使用しています。 これらの機能を使用するには、`Page_Init` イベントハンドラーで `EnableDynamicData` メソッドを呼び出す必要があります。 (`DynamicControl` コントロールは、ナビゲーションプロパティでは機能しないため、[`Administrator`] フィールドでは使用されません)。

入れ子になった `GridView` コントロールを持つ列をグリッドに追加すると、後で `Vertical-Align="Top"` 属性が重要になります。

*Departments.aspx.cs*ファイルを開き、次の `using` ステートメントを追加します。

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample4.cs)]

次に、ページの `Init` イベントに対して次のハンドラーを追加します。

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample5.cs)]

*DAL*フォルダーで、 *Department.cs*という名前の新しいクラスファイルを作成し、既存のコードを次のコードに置き換えます。

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample6.cs)]

このコードでは、メタデータをデータモデルに追加します。 これは、`Department` エンティティの [`Budget`] プロパティが実際には通貨を表すことを指定しますが、そのデータ型は `Decimal`、0から $1000000.00 の間の値である必要があることを指定します。 また、`StartDate` プロパティを mm/dd/yyyy の形式で日付として書式設定するように指定します。

Department *. .aspx*ページを実行します。

[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image26.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image25.png)

Department ページマークアップでは、**予算**または**開始日**の列の書式設定文字列を指定していませんが、 *Department.cs*ファイルで指定したメタデータを使用して、`DynamicField` コントロールによって既定の通貨と日付の書式設定が適用されていることに注意して*ください。*

## <a name="adding-insert-and-delete-functionality"></a>挿入機能と削除機能の追加

*SchoolRepository.cs*を開き、`Insert` メソッドと `Delete` メソッドを作成するために次のコードを追加します。 このコードには、`Insert` メソッドで使用するために使用できる次のレコードキー値を計算する `GenerateDepartmentID` という名前のメソッドも含まれています。 この設定が必要なのは、データベースが `Department` テーブルに対して自動的に計算するように構成されていないためです。

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample7.cs)]

### <a name="the-attach-method"></a>Attach メソッド

`DeleteDepartment` メソッドは、メモリ内のエンティティとそれが表すデータベース行との間で、オブジェクトコンテキストのオブジェクト状態マネージャーに保持されているリンクを再確立するために、`Attach` メソッドを呼び出します。 これは、メソッドが `SaveChanges` メソッドを呼び出す前に行う必要があります。

*オブジェクトコンテキスト*という用語は、エンティティセットとエンティティにアクセスするために使用する `ObjectContext` クラスから派生した Entity Framework クラスを指します。 このプロジェクトのコードでは、クラスには `SchoolEntities`という名前が付けられ、のインスタンスには常に `context`という名前が付けられます。 オブジェクトコンテキストの*オブジェクト状態マネージャー*は、`ObjectStateManager` クラスから派生するクラスです。 オブジェクトの連絡先は、オブジェクト状態マネージャーを使用してエンティティオブジェクトを格納し、それぞれがデータベース内の対応するテーブル行と同期しているかどうかを追跡します。

エンティティを読み取ると、オブジェクトコンテキストはオブジェクトをオブジェクト状態マネージャーに格納し、オブジェクトの表現がデータベースと同期されているかどうかを追跡します。 たとえば、プロパティ値を変更すると、変更したプロパティがデータベースと同期されなくなったことを示すフラグが設定されます。 その後、`SaveChanges` メソッドを呼び出すと、オブジェクトの状態マネージャーは、エンティティの現在の状態とデータベースの状態との間で何が異なるのかを認識しているので、データベースで何を行うのかがオブジェクトのコンテキストに認識されます。

ただし、このプロセスは通常、web アプリケーションでは機能しません。これは、エンティティを読み取るオブジェクトコンテキストインスタンスとそのオブジェクト状態マネージャーのすべての要素が、ページのレンダリング後に破棄されるためです。 変更を適用する必要があるオブジェクトコンテキストインスタンスは、ポストバック処理用にインスタンス化された新しいインスタンスです。 `DeleteDepartment` 方法の場合、`ObjectDataSource` コントロールは、ビューステートの値から元のエンティティのエンティティを再作成しますが、この再作成された `Department` エンティティはオブジェクト状態マネージャーに存在しません。 この再作成されたエンティティで `DeleteObject` メソッドを呼び出した場合、エンティティがデータベースと同期されているかどうかがオブジェクトコンテキストで認識されないため、呼び出しは失敗します。 ただし、`Attach` メソッドを呼び出すと、再作成されたエンティティと、オブジェクトコンテキストの以前のインスタンスでエンティティが読み取られたときに、最初に自動的に実行されたデータベース内の値との間で同じ追跡が再確立されます。

オブジェクトコンテキストがオブジェクト状態マネージャーのエンティティを追跡しないようにする場合があります。また、この処理が行われないようにフラグを設定することもできます。 この例については、このシリーズの後のチュートリアルで説明します。

### <a name="the-savechanges-method"></a>SaveChanges メソッド

この単純なリポジトリクラスは、CRUD 操作を実行する方法の基本的な原則を示しています。 この例では、`SaveChanges` メソッドが各更新の直後に呼び出されます。 実稼働アプリケーションでは、別のメソッドから `SaveChanges` メソッドを呼び出すことによって、データベースをいつ更新するかをより細かく制御できます。 (次のチュートリアルの最後に、関連する更新プログラムを調整するための1つの方法である、作業単位パターンについて説明したホワイトペーパーへのリンクがあります)。この例では、`DeleteDepartment` メソッドに、同時実行の競合を処理するコードが含まれていないことにも注意してください。そのためのコードは、このシリーズの後のチュートリアルで追加します。

### <a name="retrieving-instructor-names-to-select-when-inserting"></a>挿入時に選択するインストラクター名を取得しています

ユーザーは、新しい部門を作成するときに、ドロップダウンリストでインストラクターの一覧から管理者を選択できる必要があります。 したがって、次のコードを*SchoolRepository.cs*に追加して、前に作成したビューを使用してインストラクターの一覧を取得するメソッドを作成します。

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample8.cs)]

### <a name="creating-a-page-for-inserting-departments"></a>部署を挿入するためのページの作成

*DepartmentsAdd*ページを使用するページを作成し、`Content2`という*名前の `Content`* コントロールに次のマークアップを追加します。

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample9.aspx)]

このマークアップでは、2つの `ObjectDataSource` コントロールが作成されます。1つは新しい `Department` エンティティを挿入するためのコントロールで、もう1つは部門管理者の選択に使用される `DropDownList` コントロールのインストラクター名を取得するためのものです。 マークアップは、新しい部署を入力するための `DetailsView` コントロールを作成し、`Administrator` 外部キーの値を設定できるように、コントロールの `ItemInserting` イベントのハンドラーを指定します。 は、エラーメッセージを表示するための `ValidationSummary` コントロールです。

*DepartmentsAdd.aspx.cs*を開き、次の `using` ステートメントを追加します。

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample10.cs)]

次のクラス変数とメソッドを追加します。

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample11.cs)]

`Page_Init` メソッドを使用すると、動的データ機能が有効になります。 `DropDownList` コントロールの `Init` イベントのハンドラーは、コントロールへの参照を保存します。また、`DetailsView` コントロールの `Inserting` イベントのハンドラーは、その参照を使用して、選択されたインストラクターの `PersonID` 値を取得し、`Administrator` エンティティの `Department` 外部キープロパティを更新します。

ページを実行し、新しい部署の情報を追加して、 **[挿入]** リンクをクリックします。

[![Image04](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image28.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image27.png)

別の新しい部門の値を入力します。 **[予算]** フィールドに1000000.00 より大きい数値を入力し、tab キーを押して次のフィールドに入力します。 フィールドにアスタリスクが表示され、その上にマウスポインターを置くと、そのフィールドのメタデータに入力したエラーメッセージが表示されます。

[![Image03](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image30.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image29.png)

**[挿入]** をクリックすると、ページの下部にある `ValidationSummary` コントロールによって表示されるエラーメッセージが表示されます。

[![Image12](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image32.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image31.png)

次に、ブラウザーを閉じて、department *.aspx*ページを開きます。 `ObjectDataSource` コントロールに `DeleteMethod` 属性を追加し、`GridView` コントロールに `DataKeyNames` 属性を追加して、department ページに削除機能を追加*します。* これらのコントロールの開始タグは、次の例のようになります。

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample12.aspx)]

ページを実行します。

[![Image09](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image34.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image33.png)

*DepartmentsAdd*ページを実行したときに追加した部署を削除します。

## <a name="adding-update-functionality"></a>更新機能の追加

*SchoolRepository.cs*を開き、次の `Update` メソッドを追加します。

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample13.cs)]

Department ページで **[更新]** をクリックすると、`ObjectDataSource` コントロールによって、`UpdateDepartment` メソッドに渡す2つの `Department` エンティティが作成され*ます。* 一方には、ビューステートに格納されている元の値が含まれ、もう1つは、`GridView` コントロールに入力された新しい値を格納します。 `UpdateDepartment` メソッドのコードは、元の値を持つ `Department` エンティティを `Attach` メソッドに渡して、エンティティとデータベース内のデータの間の追跡を確立します。 次に、新しい値を持つ `Department` エンティティを `ApplyCurrentValues` メソッドに渡します。 オブジェクトコンテキストは、古い値と新しい値を比較します。 新しい値が古い値と異なる場合は、オブジェクトコンテキストによってプロパティ値が変更されます。 `SaveChanges` メソッドは、データベース内の変更された列のみを更新します。 (ただし、このエンティティの update 関数がストアドプロシージャにマップされていた場合、どの列が変更されたかにかかわらず、行全体が更新されます)。

学科の *.aspx*ファイルを開き、次の属性を `DepartmentsObjectDataSource` コントロールに追加します。

- `UpdateMethod="UpdateDepartment"`
- `ConflictDetection="CompareAllValues"`   
 これにより、古い値が `Update` メソッドの新しい値と比較できるように、古い値がビューステートに格納されます。
- `OldValuesParameterFormatString="orig{0}"`   
 これにより、元の values パラメーターの名前が `origDepartment` であることがコントロールに通知されます。

`ObjectDataSource` コントロールの開始タグのマークアップは、次の例のようになります。

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample14.aspx)]

`GridView` コントロールに `OnRowUpdating="DepartmentsGridView_RowUpdating"` 属性を追加します。 このプロパティを使用して、ユーザーがドロップダウンリストで選択した行に基づいて、`Administrator` プロパティの値を設定します。 `GridView` の開始タグは、次の例のようになります。

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample15.aspx)]

`Administrator` 列の `EditItemTemplate` コントロールを `GridView` コントロールに追加します。その際、その列の `ItemTemplate` コントロールの直後に追加します。

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample16.aspx)]

この `EditItemTemplate` コントロールは、 *DepartmentsAdd*ページの `InsertItemTemplate` コントロールに似ています。 違いは、コントロールの初期値が `SelectedValue` 属性を使用して設定されていることです。

`GridView` コントロールの前に、 *DepartmentsAdd*ページで行ったように `ValidationSummary` コントロールを追加します。

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample17.aspx)]

*Departments.aspx.cs*を開き、部分クラス宣言の直後に、次のコードを追加して、`DropDownList` コントロールを参照するプライベートフィールドを作成します。

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample18.cs)]

次に、`DropDownList` コントロールの `Init` イベントと `GridView` コントロールの `RowUpdating` イベントのハンドラーを追加します。

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample19.cs)]

`Init` イベントのハンドラーは、クラスフィールドに `DropDownList` コントロールへの参照を保存します。 `RowUpdating` イベントのハンドラーは、参照を使用してユーザーが入力した値を取得し、それを `Department` エンティティの `Administrator` プロパティに適用します。

*DepartmentsAdd*ページを使用して新しい部署を追加し、次に department *.aspx*ページを実行して、追加した行の **[編集]** をクリックします。

> [!NOTE]
> データベース内のデータが無効なため、追加していない行 (つまり、データベースに既に存在していた行) を編集することはできません。データベースで作成された行の管理者は、students です。 これらのいずれかを編集しようとすると、次のようなエラーを報告するエラーページが表示され `'InstructorsDropDownList' has a SelectedValue which is invalid because it does not exist in the list of items.`

[![Image10](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image36.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image35.png)

無効な**予算**金額を入力して **[更新]** をクリックすると、[department *] ページで*確認したのと同じアスタリスクとエラーメッセージが表示されます。

フィールド値を変更するか、別の管理者を選択して **[更新]** をクリックします。 変更が表示されます。

[![Image09](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image38.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image37.png)

このチュートリアルでは、Entity Framework で基本的な CRUD (作成、読み取り、更新、削除) 操作に `ObjectDataSource` コントロールを使用する方法の概要を説明します。 単純な n 層アプリケーションを構築しましたが、ビジネスロジック層はデータアクセス層と緊密に結合されているため、自動単体テストが複雑になります。 次のチュートリアルでは、単体テストを容易にするリポジトリパターンを実装する方法について説明します。

> [!div class="step-by-step"]
> [Next](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests.md)
