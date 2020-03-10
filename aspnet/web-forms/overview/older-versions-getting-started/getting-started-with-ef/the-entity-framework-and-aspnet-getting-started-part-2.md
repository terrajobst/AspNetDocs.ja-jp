---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-2
title: Entity Framework 4.0 Database First および ASP.NET 4 Web フォームでのはじめに-パート 2 |Microsoft Docs
author: tdykstra
description: Contoso 大学のサンプル web アプリケーションは、Entity Framework を使用して ASP.NET Web フォームアプリケーションを作成する方法を示しています。 サンプルアプリケーションは...
ms.author: riande
ms.date: 12/03/2010
ms.assetid: fb63a326-a4ae-4b0c-a4f5-412327197216
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-2
msc.type: authoredcontent
ms.openlocfilehash: bd6a2e29e6f0df04e39be29160e2e08cc99c4706
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78456448"
---
# <a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-2"></a>Entity Framework 4.0 Database First および ASP.NET 4 Web フォームでのはじめに-パート2

[Tom Dykstra](https://github.com/tdykstra)

> Contoso 大学のサンプル web アプリケーションは、Entity Framework 4.0 と Visual Studio 2010 を使用して ASP.NET Web フォームアプリケーションを作成する方法を示しています。 チュートリアルシリーズの詳細については、[シリーズの最初のチュートリアル](the-entity-framework-and-aspnet-getting-started-part-1.md)を参照してください。

## <a name="the-entitydatasource-control"></a>EntityDataSource コントロール

前のチュートリアルでは、web サイト、データベース、およびデータモデルを作成しました。 このチュートリアルでは、ASP.NET が提供する `EntityDataSource` コントロールを使用して、Entity Framework データモデルを簡単に操作できるようにします。 学生データを表示および編集するための `GridView` コントロール、新しい学生を追加するための `DetailsView` コントロール、部署を選択するための `DropDownList` コントロール (関連付けられたコースを表示するために後で使用する) を作成します。

[![Image20](the-entity-framework-and-aspnet-getting-started-part-2/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image1.png)

[![Image09](the-entity-framework-and-aspnet-getting-started-part-2/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image3.png)

[![Image18](the-entity-framework-and-aspnet-getting-started-part-2/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image5.png)

このアプリケーションでは、データベースを更新するページに入力検証を追加することはできません。また、一部のエラー処理は、実稼働アプリケーションで必要になるほど堅牢ではありません。 このチュートリアルでは、Entity Framework に重点を置いているので、時間がかかりすぎないようにします。 これらの機能をアプリケーションに追加する方法の詳細については、「 [ASP.NET Web ページでのユーザー入力の検証](https://msdn.microsoft.com/library/7kh55542.aspx)」および「 [ASP.NET ページとアプリケーションでのエラー処理](https://msdn.microsoft.com/library/w16865z6.aspx)」を参照してください。

## <a name="adding-and-configuring-the-entitydatasource-control"></a>EntityDataSource コントロールの追加と構成

まず、`People` エンティティセットから `Person` エンティティを読み取るように `EntityDataSource` コントロールを構成します。

Visual Studio が開いていること、およびパート1で作成したプロジェクトを操作していることを確認します。 データモデルを作成した後、または前回変更を行った後にプロジェクトをビルドしていない場合は、ここでプロジェクトをビルドします。 データモデルへの変更は、プロジェクトがビルドされるまで、デザイナーでは使用できません。

**マスターページテンプレートを使用して Web フォーム**を使用して新しい web ページを作成し、「 *Students*」という名前を指定します。

[![Image23](the-entity-framework-and-aspnet-getting-started-part-2/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image7.png)

マスターページとして「 *.master* 」と指定します。 これらのチュートリアル用に作成したすべてのページで、このマスターページが使用されます。

[![Image24](the-entity-framework-and-aspnet-getting-started-part-2/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image9.png)

**ソース**ビューで、次の例に示すように、`Content2`という名前の `Content` コントロールに `h2` 見出しを追加します。

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample1.aspx)]

**ツールボックス**の **[データ]** タブから `EntityDataSource` コントロールをページにドラッグし、見出しの下にドロップして、ID を `StudentsEntityDataSource`に変更します。

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample2.aspx)]

**デザイン**ビューに切り替え、データソースコントロールのスマートタグをクリックします。次に、 **[データソースの構成]** をクリックして、**データソースの構成**ウィザードを起動します。

[![Image01](the-entity-framework-and-aspnet-getting-started-part-2/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image11.png)

ObjectContext の**構成**ウィザードの手順で、 **[名前付き接続]** の値として **[SchoolEntities]** を選択し、 **DefaultContainerName**値として **[SchoolEntities]** を選択します。 続けて、 **[次へ]** をクリックします。

[![Image02](the-entity-framework-and-aspnet-getting-started-part-2/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image13.png)

注: この時点で次のダイアログボックスが表示される場合は、続行する前にプロジェクトをビルドする必要があります。

[![Image25](the-entity-framework-and-aspnet-getting-started-part-2/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image15.png)

**[データ選択の構成]** ステップで、 **[EntitySetName]** の値として **[People]** を選択します。 **[選択]** で、Ll を **[選択する]** チェックボックスがオンになっていることを確認します。 次に、更新と削除を有効にするオプションを選択します。 完了したら、 **[完了]** をクリックします。

[![Image03](the-entity-framework-and-aspnet-getting-started-part-2/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image17.png)

## <a name="configuring-database-rules-to-allow-deletion"></a>削除を許可するデータベースルールの構成

ユーザーが `Person` テーブルから学生を削除できるページを作成します。このテーブルには、他のテーブル (`Course`、`StudentGrade`、および `OfficeAssignment`) との3つのリレーションシップがあります。 既定では、他のいずれかのテーブルに関連する行がある場合、データベースによって `Person` の行が削除されるのを防ぐことができます。 最初に関連する行を手動で削除することも、`Person` 行を削除したときにデータベースを自動的に削除するように構成することもできます。 このチュートリアルの student レコードでは、関連データを自動的に削除するようにデータベースを構成します。 学生は `StudentGrade` テーブルにのみ関連する行を持つことができるため、3つのリレーションシップのうち1つだけを構成する必要があります。

このチュートリアルで作成したプロジェクトからダウンロードした*School .mdf*ファイルを使用している場合は、これらの構成の変更が既に行われているため、このセクションをスキップできます。 スクリプトを実行してデータベースを作成した場合は、次の手順を実行してデータベースを構成します。

**サーバーエクスプローラー**で、パート1で作成したデータベースダイアグラムを開きます。 `Person` と `StudentGrade` (テーブル間の線) の間のリレーションシップを右クリックし、 **[プロパティ]** を選択します。

[![Image04](the-entity-framework-and-aspnet-getting-started-part-2/_static/image20.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image19.png)

**[プロパティ]** ウィンドウで、 **[挿入と更新の指定]** を展開し、 **DeleteRule**プロパティを**Cascade**に設定します。

[![Image05](the-entity-framework-and-aspnet-getting-started-part-2/_static/image22.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image21.png)

ダイアグラムを保存して閉じます。 データベースを更新するかどうかを確認するメッセージが表示されたら、 **[はい]** をクリックします。

モデルで、メモリ内のエンティティがデータベースで実行されているものと同期されるようにするには、データモデルで対応するルールを設定する必要があります。 *SchoolModel*を開き、`Person` と `StudentGrade`の間の関連行を右クリックし、 **[プロパティ]** を選択します。

[![Image21](the-entity-framework-and-aspnet-getting-started-part-2/_static/image24.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image23.png)

**[プロパティ]** ウィンドウで、 **End1 OnDelete**を**Cascade**に設定します。

[![Image22](the-entity-framework-and-aspnet-getting-started-part-2/_static/image26.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image25.png)

*SchoolModel*ファイルを保存して閉じてから、プロジェクトをリビルドします。

一般に、データベースが変更された場合、モデルを同期する方法にはいくつかの選択肢があります。

- 特定の種類の変更 (テーブル、ビュー、またはストアドプロシージャの追加や更新など) については、デザイナー内で右クリックし、 **[データベースからモデルを更新]** を選択して、デザイナーが変更を自動的に行うようにします。
- データモデルを再生成します。
- このような手動更新を行います。

この場合、モデルを再生成するか、リレーションシップの変更によって影響を受けるテーブルを更新することができますが、その場合は、フィールド名を再度変更する必要があります (`FirstName` から `FirstMidName`)。

## <a name="using-a-gridview-control-to-read-and-update-entities"></a>GridView コントロールを使用したエンティティの読み取りと更新

このセクションでは、`GridView` コントロールを使用して、学生の表示、更新、または削除を行います。

*Student .aspx*に移動し、 **[デザイン]** ビューに切り替えます。 **ツールボックス**の **[データ]** タブから、`GridView` コントロールを `EntityDataSource` コントロールの右側にドラッグし、`StudentsGridView`という名前を付けて、スマートタグをクリックし、データソースとして **[StudentsEntityDataSource]** を選択します。

[![Image06](the-entity-framework-and-aspnet-getting-started-part-2/_static/image28.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image27.png)

**スキーマの更新** をクリックし (確認を求められたら **はい**をクリックします)、**ページング**を有効にする、**並べ替え**を有効にする、**編集**を有効にする、および **削除を**有効

**[列の編集]** をクリックします。

[![Image10](the-entity-framework-and-aspnet-getting-started-part-2/_static/image30.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image29.png)

**[選択されたフィールド]** ボックスで、 **PersonID**、 **LastName**、および**HireDate**を削除します。 通常、ユーザーにはレコードキーを表示せず、採用日は学生には関係しません。また、名前の両方の部分を1つのフィールドに入力するので、名前フィールドのいずれか1つだけが必要です。

[![Image11](the-entity-framework-and-aspnet-getting-started-part-2/_static/image32.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image31.png)

**[Firstmidname]** フィールドを選択し、 **[このフィールドを TemplateField に変換する]** をクリックします。

**EnrollmentDate**に対しても同じ操作を行います。

[![Image13](the-entity-framework-and-aspnet-getting-started-part-2/_static/image34.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image33.png)

[ **OK]** をクリックし、[**ソース**ビュー] に切り替えます。 残りの変更は、マークアップで直接行う方が簡単です。 `GridView` コントロールマークアップは、次の例のようになります。

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample3.aspx)]

コマンドフィールドの後の最初の列は、現在名を表示しているテンプレートフィールドです。 このテンプレートフィールドのマークアップを次の例のように変更します。

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample4.aspx)]

表示モードでは、2つの `Label` コントロールに姓と名が表示されます。 編集モードでは、姓と名を変更できるように、2つのテキストボックスが用意されています。 表示モードの `Label` コントロールと同様に、データベースに直接接続するデータソースコントロールを ASP.NET する場合と同じように `Bind` と `Eval` 式を使用します。 唯一の違いは、データベース列ではなくエンティティプロパティを指定することです。

最後の列は、登録日を表示するテンプレートフィールドです。 このフィールドのマークアップを次の例のように変更します。

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample5.aspx)]

表示モードと編集モードの両方で、書式文字列 "{0, d}" を指定すると、日付が "short date" 形式で表示されます。 (このコンピューターは、このチュートリアルで示されている画面イメージとは異なる形式で表示されるように構成されている場合があります)。

これらの各テンプレートフィールドでは、デザイナーでは既定で `Bind` 式が使用されていましたが、これは `ItemTemplate` 要素の `Eval` 式に変更されています。 `Bind` 式を使用すると、コード内のデータにアクセスする必要がある場合に、`GridView` コントロールのプロパティでデータを使用できるようになります。 このページでは、コード内でこのデータにアクセスする必要はないため、`Eval`を使用できますが、これはより効率的です。 詳細については、「データ[コントロールからのデータの取得](https://weblogs.asp.net/davidfowler/archive/2008/12/12/getting-your-data-out-of-the-data-controls.aspx)」を参照してください。

## <a name="revising-entitydatasource-control-markup-to-improve-performance"></a>パフォーマンスを向上させるために EntityDataSource コントロールのマークアップを改訂する

`EntityDataSource` コントロールのマークアップで、`ConnectionString` 属性と `DefaultContainerName` 属性を削除し、`ContextTypeName="ContosoUniversity.DAL.SchoolEntities"` 属性に置き換えます。 これは、オブジェクトコンテキストクラスにハードコーディングされている接続とは異なる接続を使用する必要がある場合を除き、`EntityDataSource` コントロールを作成するたびに行う必要がある変更です。 `ContextTypeName` 属性を使用すると、次のような利点があります。

- パフォーマンスが向上します。 `EntityDataSource` コントロールが `ConnectionString` 属性と `DefaultContainerName` 属性を使用してデータモデルを初期化すると、すべての要求にメタデータを読み込むための追加作業が実行されます。 これは、`ContextTypeName` 属性を指定する場合は必要ありません。
- 遅延読み込みは、Entity Framework 4.0 の生成されたオブジェクトコンテキストクラス (このチュートリアルでは `SchoolEntities` など) で既定で有効になっています。 これは、必要に応じて、ナビゲーションプロパティが関連データと共に自動的に読み込まれることを意味します。 遅延読み込みの詳細については、このチュートリアルの後半で説明します。
- オブジェクトコンテキストクラス (この場合は `SchoolEntities` クラス) に適用したカスタマイズは、`EntityDataSource` コントロールを使用するコントロールで使用できるようになります。 オブジェクトコンテキストクラスのカスタマイズは、このチュートリアルシリーズでは説明されていない高度なトピックです。 詳細については、「 [Entity Framework 生成された型の拡張](https://msdn.microsoft.com/library/dd456844.aspx)」を参照してください。

マークアップは次の例のようになります (プロパティの順序が異なる場合があります)。

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample6.aspx)]

`EnableFlattening` 属性は、外部キー列がエンティティプロパティとして公開されていないため、以前のバージョンの Entity Framework で必要な機能を参照します。 現在のバージョンでは、*外部キーの関連付け*を使用できるようになっています。つまり、外部キーのプロパティは、すべての多対多のアソシエーションに対して公開されます。 エンティティに外部キープロパティがあり、[複合型](https://msdn.microsoft.com/library/bb738472.aspx)がない場合は、この属性を `False`に設定したままにすることができます。 既定値は `True`ので、マークアップから属性を削除しないでください。 詳細については、「オブジェクトのフラット化」 [(EntityDataSource)](https://msdn.microsoft.com/library/ee404746.aspx)を参照してください。

ページを実行すると、学生と従業員の一覧が表示されます (次のチュートリアルでは、生徒にのみフィルターを適用します)。 姓と名が一緒に表示されます。

[![Image07](the-entity-framework-and-aspnet-getting-started-part-2/_static/image36.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image35.png)

表示を並べ替えるには、列名をクリックします。

任意の行の **[編集]** をクリックします。 テキストボックスが表示され、姓と名を変更できます。

[![Image08](the-entity-framework-and-aspnet-getting-started-part-2/_static/image38.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image37.png)

**[削除]** ボタンも機能します。 登録日がある行の [削除] をクリックすると、行が表示されなくなります。 (登録日のない行は講師を表し、参照整合性エラーが発生する可能性があります。 次のチュートリアルでは、このリストにフィルターを適用して、学生だけを含めます)。

## <a name="displaying-data-from-a-navigation-property"></a>ナビゲーションプロパティからのデータの表示

ここで、各学生が登録されているコースの数を知りたいとします。 Entity Framework は、`Person` エンティティの `StudentGrades` ナビゲーションプロパティにその情報を提供します。 データベースの設計では、学年が割り当てられていなくても学生を講座に登録することはできないため、このチュートリアルでは、コースに関連付けられている `StudentGrade` テーブル行内の行が、コースに登録されているものと同じであることを想定できます。 (`Courses` ナビゲーションプロパティは、インストラクターだけを対象としています)。

`EntityDataSource` コントロールの `ContextTypeName` 属性を使用すると、そのプロパティにアクセスしたときに、ナビゲーションプロパティの情報が Entity Framework によって自動的に取得されます。 これは*遅延読み込み*と呼ばれます。 ただし、追加情報が必要になるたびにデータベースが個別に呼び出されるため、これは非効率的になる可能性があります。 `EntityDataSource` コントロールによって返されるすべてのエンティティのナビゲーションプロパティからのデータが必要な場合は、データベースへの1回の呼び出しで、関連するデータをエンティティ自体と共に取得する方が効率的です。 これは、*一括読み込み*と呼ばれ、`EntityDataSource` コントロールの `Include` プロパティを設定することによって、ナビゲーションプロパティの一括読み込みを指定します。

*Students*では、各学生のコース数を表示したいので、一括読み込みが最適な選択肢です。 すべての学生を表示していても、いくつかのコース (マークアップに加えていくつかのコードを記述する必要があります) のコースのみを表示している場合は、遅延読み込みの方が適している可能性があります。

*Student .aspx*に切り替えて、**デザイン**ビューに切り替え、[`StudentsEntityDataSource`] を選択します。次に、 **[プロパティ]** ウィンドウで、 **Include**プロパティを**StudentGrades**に設定します。 (複数のナビゲーションプロパティを取得する場合は、名前をコンマで区切って指定できます (たとえば、 **StudentGrades、** course)。

[![Image19](the-entity-framework-and-aspnet-getting-started-part-2/_static/image40.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image39.png)

**ソース**ビューに切り替えます。 `StudentsGridView` コントロールで、最後の `asp:TemplateField` 要素の後に、次の新しいテンプレートフィールドを追加します。

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample7.aspx)]

`Eval` 式では、ナビゲーションプロパティ `StudentGrades`を参照できます。 このプロパティにはコレクションが含まれているため、学生が登録されているコースの数を表示するために使用できる `Count` のプロパティがあります。 後のチュートリアルでは、コレクションではなく単一のエンティティを含むナビゲーションプロパティからデータを表示する方法について説明します。 (`BoundField` 要素を使用して、ナビゲーションプロパティのデータを表示することはできません)。

ページを実行すると、各学生が登録したコースの数が表示されます。

[![Image20](the-entity-framework-and-aspnet-getting-started-part-2/_static/image42.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image41.png)

## <a name="using-a-detailsview-control-to-insert-entities"></a>DetailsView コントロールを使用してエンティティを挿入する

次の手順では、新しい学生を追加できる `DetailsView` コントロールを持つページを作成します。 ブラウザーを閉じてから、新しい web ページを作成し*ます。* ページに*StudentsAdd*という名前を指定し、**ソース**ビューに切り替えます。

次のマークアップを追加して、`Content2`という名前の `Content` コントロールの既存のマークアップを置き換えます。

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample8.aspx)]

このマークアップは、挿入を可能にする以外は、 *student*で作成したコントロールに似た `EntityDataSource` コントロールを作成します。 `GridView` コントロールと同様に、`DetailsView` コントロールのバインドされたフィールドは、エンティティのプロパティを参照することを除いて、データベースに直接接続するデータコントロールの場合とまったく同じようにコード化されます。 この場合、`DetailsView` コントロールは行の挿入にのみ使用されるため、既定のモードを `Insert`に設定します。

ページを実行し、新しい学生を追加します。

[![Image09](the-entity-framework-and-aspnet-getting-started-part-2/_static/image44.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image43.png)

新しい学生を挿入した後は何も起こりませんが、ここで student*を実行すると、新しい*学生情報が表示されます。

## <a name="displaying-data-in-a-drop-down-list"></a>ドロップダウンリストでのデータの表示

次の手順では、`EntityDataSource` コントロールを使用して、`DropDownList` コントロールをエンティティセットにバインドします。 チュートリアルのこの部分では、この一覧についてはあまりいきません。 ただし、その後の部分では、一覧を使用して、ユーザーが部署を選択して部門に関連付けられているコースを表示できるようにします。

「Course」という名前の新しい web ページを作成*します。* **ソース**ビューで、`Content2`という名前の `Content` コントロールに見出しを追加します。

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample9.aspx)]

**デザイン**ビューで、前と同じように `EntityDataSource` コントロールをページに追加します。ただし、この時刻の名前は `DepartmentsEntityDataSource`ます。 **EntitySetName**値と**して [department] を選択**し、 **[DepartmentID]** および **[Name]** プロパティのみを選択します。

[![Image15](the-entity-framework-and-aspnet-getting-started-part-2/_static/image46.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image45.png)

**ツールボックス**の **[標準]** タブで `DropDownList` コントロールをページにドラッグし、`DepartmentsDropDownList`という名前を付けて、スマートタグをクリックし、 **[データソースの選択]** を選択してデータソース**構成ウィザード**を開始します。

[![Image16](the-entity-framework-and-aspnet-getting-started-part-2/_static/image48.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image47.png)

**データソースの選択** ステップで、データソースとして **DepartmentsEntityDataSource** を選択し、**スキーマの更新** をクリックします。次に、表示するデータフィールドとして **名前** を選択し、値のデータ フィールドに**DepartmentID**を選択します。 **[OK]** をクリックします。

[![Image17](the-entity-framework-and-aspnet-getting-started-part-2/_static/image50.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image49.png)

Entity Framework を使用してコントロールをデータバインドするために使用するメソッドは、エンティティとエンティティのプロパティを指定する点を除いて、他の ASP.NET データソースコントロールと同じです。

**ソース**ビューに切り替えて、`DropDownList` コントロールの直前に "Select a department:" を追加します。

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample10.aspx)]

この時点で、`ConnectionString` 属性と `DefaultContainerName` 属性を `ContextTypeName="ContosoUniversity.DAL.SchoolEntities"` 属性で置き換えることによって、この時点で `EntityDataSource` コントロールのマークアップを変更します。 `EntityDataSource` コントロールのマークアップを変更する前に、データソースコントロールにリンクされているデータバインドコントロールを作成しておくと、多くの場合は待機することをお勧めします。これは、変更を行った後に、デザイナーがデータバインドコントロールの **[スキーマの更新]** オプションを提供しないためです。

ページを実行すると、ドロップダウンリストから部門を選択できます。

[![Image18](the-entity-framework-and-aspnet-getting-started-part-2/_static/image52.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image51.png)

これで、`EntityDataSource` コントロールの使用方法の概要が完成します。 このコントロールの操作は、通常、他の ASP.NET データソースコントロールとは異なりますが、テーブルや列ではなくエンティティとプロパティを参照する点が異なります。 唯一の例外は、ナビゲーションプロパティにアクセスする場合です。 次のチュートリアルでは、データのフィルター処理、グループ化、および並べ替えを行うときに、`EntityDataSource` コントロールで使用する構文も、他のデータソースコントロールとは異なる場合があることがわかります。

> [!div class="step-by-step"]
> [前へ](the-entity-framework-and-aspnet-getting-started-part-1.md)
> [次へ](the-entity-framework-and-aspnet-getting-started-part-3.md)
