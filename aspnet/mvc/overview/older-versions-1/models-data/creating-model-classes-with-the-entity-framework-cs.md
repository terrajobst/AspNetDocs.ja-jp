---
uid: mvc/overview/older-versions-1/models-data/creating-model-classes-with-the-entity-framework-cs
title: Entity Framework (C#) を使用してモデルクラスを作成するMicrosoft Docs
author: microsoft
description: このチュートリアルでは、Microsoft Entity Framework で ASP.NET MVC を使用する方法について説明します。 Entity Wizard を使用して ADO.NET エンティティを作成する方法について説明します。
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 61644169-e8b1-45dd-bf96-9c2301b69879
msc.legacyurl: /mvc/overview/older-versions-1/models-data/creating-model-classes-with-the-entity-framework-cs
msc.type: authoredcontent
ms.openlocfilehash: 2e0e365c287fc455015d237ea466301335805d14
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78469438"
---
# <a name="creating-model-classes-with-the-entity-framework-c"></a>Entity Framework でモデル クラスを作成する (C#)

[Microsoft](https://github.com/microsoft)

> このチュートリアルでは、Microsoft Entity Framework で ASP.NET MVC を使用する方法について説明します。 Entity Wizard を使用して、ADO.NET Entity Data Model を作成する方法について説明します。 このチュートリアルでは、Entity Framework を使用してデータベースデータを選択、挿入、更新、および削除する方法を示す web アプリケーションを作成します。

このチュートリアルの目的は、ASP.NET MVC アプリケーションを構築するときに、Microsoft Entity Framework を使用してデータアクセスクラスを作成する方法について説明することです。 このチュートリアルでは、Microsoft Entity Framework に関する以前の知識がないことを前提としています。 このチュートリアルの最後に、Entity Framework を使用してデータベースレコードを選択、挿入、更新、および削除する方法について説明します。

Microsoft Entity Framework は、オブジェクトリレーショナルマッピング (O/RM) ツールです。このツールを使用すると、データベースからデータアクセス層を自動的に生成できます。 Entity Framework を使用すると、手動でデータアクセスクラスを構築する面倒な作業を回避できます。

ASP.NET MVC で Microsoft Entity Framework を使用する方法を説明するために、簡単なサンプルアプリケーションを作成します。 ムービーデータベースアプリケーションを作成し、ムービーデータベースレコードを表示および編集できるようにします。

このチュートリアルでは、Visual Studio 2008 または Visual Web Developer 2008 (Service Pack 1) を使用していることを前提としています。 Entity Framework を使用するには、Service Pack 1 が必要です。 次のアドレスから、Visual Studio 2008 Service Pack 1 または Visual Web Developer with Service Pack 1 をダウンロードできます。

> [https://www.asp.net/downloads/](https://www.asp.net/downloads)

> [!NOTE] 
> 
> ASP.NET MVC と Microsoft Entity Framework の間には、重要な接続はありません。 ASP.NET MVC で使用できる Entity Framework には、いくつかの選択肢があります。 たとえば、Microsoft LINQ to SQL、NHibernate、SubSonic などの他の O/RM ツールを使用して、MVC モデルクラスを構築できます。

## <a name="creating-the-movie-sample-database"></a>ムービーサンプルデータベースの作成

ムービーデータベースアプリケーションでは、次の列を含む、ムービーという名前のデータベーステーブルを使用します。

| 列名 | データ型 | Null を許容しますか? | 主キーか? |
| --- | --- | --- | --- |
| Id | INT | False | True |
| タイトル | nvarchar(100) | False | False |
| ディレクター | nvarchar(100) | False | False |

このテーブルを ASP.NET MVC プロジェクトに追加するには、次の手順を実行します。

1. ソリューションエクスプローラーウィンドウで [App\_Data] フォルダーを右クリックし、メニューオプション [追加]、[新しい項目] の順に選択し**ます。**
2. **[新しい項目の追加]** ダイアログボックスで、 **[SQL Server データベース]** を選択し、データベースに MoviesDB という名前を付けて、 **[追加]** ボタンをクリックします。
3. MoviesDB ファイルをダブルクリックして、[サーバーエクスプローラー/データベースエクスプローラー] ウィンドウを開きます。
4. MoviesDB データベース接続を展開し、テーブル フォルダーを右クリックして、**新しいテーブルの追加** メニューオプションを選択します。
5. テーブルデザイナーで、Id、タイトル、ディレクター の各列を追加します。
6. **[保存]** ボタン (フロッピーのアイコン) をクリックして、ムービーという名前の新しいテーブルを保存します。

ムービーデータベーステーブルを作成したら、いくつかのサンプルデータをテーブルに追加する必要があります。 映画 テーブルを右クリックし、**テーブルデータの表示** メニューオプションを選択します。 表示されるグリッドにフェイクムービーデータを入力できます。

## <a name="creating-the-adonet-entity-data-model"></a>ADO.NET Entity Data Model の作成

Entity Framework を使用するには、Entity Data Model を作成する必要があります。 Visual Studio の*Entity Data Model ウィザード*を利用すると、データベースから Entity Data Model を自動的に生成できます。

次の手順に従います。

1. ソリューションエクスプローラーウィンドウで [モデル] フォルダーを右クリックし、メニューオプション [**追加]、[新しい項目**] の順に選択します。
2. **新しい項目の追加** ダイアログで、データ カテゴリを選択します (図1を参照)。
3. **ADO.NET Entity Data Model**テンプレートを選択し、Entity Data Model の名前を MoviesDBModel に指定して、 **[追加]** ボタンをクリックします。 **[追加]** ボタンをクリックすると、データモデルウィザードが起動します。
4. **[モデルの内容の選択]** ステップで、 **[データベースから生成]** オプションを選択し、 **[次へ]** ボタンをクリックします (図2を参照)。
5. **[データ接続の選択]** 手順で、MoviesDB データベース接続を選択し、エンティティ接続設定の名前 MoviesDBEntities を入力して、 **[次へ]** ボタンをクリックします (図3を参照)。
6. **[データベースオブジェクトの選択]** ステップで、ムービーデータベース テーブルを選択し、 **[完了]** ボタンをクリックします (図4を参照)。

これらの手順を完了すると、ADO.NET Entity Data Model Designer (Entity Designer) が開きます。

**図1–新しい Entity Data Model の作成**

![clip_image002](creating-model-classes-with-the-entity-framework-cs/_static/image1.jpg)

**図2–モデルの内容を選択する手順**

![clip_image004](creating-model-classes-with-the-entity-framework-cs/_static/image2.jpg)

**図 3-データ接続を選択する**

![clip_image006](creating-model-classes-with-the-entity-framework-cs/_static/image3.jpg)

**図4–データベースオブジェクトを選択する**

![clip_image008](creating-model-classes-with-the-entity-framework-cs/_static/image4.jpg)

#### <a name="modifying-the-adonet-entity-data-model"></a>ADO.NET Entity Data Model の変更

Entity Data Model を作成したら、Entity Designer を利用してモデルを変更できます (図5を参照)。 [ソリューションエクスプローラー] ウィンドウ内の [モデル] フォルダーに格納されている MoviesDBModel ファイルをダブルクリックすると、いつでも Entity Designer を開くことができます。

**図 5: ADO.NET Entity Data Model デザイナー**

![clip_image010](creating-model-classes-with-the-entity-framework-cs/_static/image5.jpg)

たとえば、エンティティモデルデータウィザードによって生成されるクラスの名前を変更するには、Entity Designer を使用します。 このウィザードでは、ムービーという名前の新しいデータアクセスクラスが作成されました。 つまり、ウィザードでは、データベーステーブルとまったく同じ名前が付けられています。 このクラスを使用して特定のムービーインスタンスを表すため、ムービーからムービーにクラスの名前を変更する必要があります。

エンティティクラスの名前を変更する場合は、Entity Designer でクラス名をダブルクリックし、新しい名前を入力します (図6を参照)。 また、Entity Designer でエンティティを選択した後で、プロパティウィンドウ内のエンティティの名前を変更することもできます。

**図6–エンティティ名の変更**

![clip_image012](creating-model-classes-with-the-entity-framework-cs/_static/image6.jpg)

変更を行った後は、[保存] ボタン (フロッピーディスクのアイコン) をクリックして Entity Data Model を保存してください。 バックグラウンドでは、Entity Designer によってクラスのC#セットが生成されます。 これらのクラスを表示するには、[ソリューションエクスプローラー] ウィンドウで MoviesDBModel.Designer.cs ファイルを開きます。

Designer.cs ファイルのコードを変更しないでください。変更内容は、次回 Entity Designer を使用したときに上書きされます。 Designer.cs ファイルで定義されているエンティティクラスの機能を拡張する場合は、*部分クラス*を別々のファイルに作成できます。

#### <a name="selecting-database-records-with-the-entity-framework"></a>Entity Framework を使用したデータベースレコードの選択

ムービーレコードの一覧を表示するページを作成して、ムービーデータベースアプリケーションの作成を開始しましょう。 リスト1のホームコントローラーは、Index () という名前のアクションを公開します。 Index () アクションは、Entity Framework を利用して、ムービーデータベーステーブルのすべてのムービーレコードを返します。

**リスト1– Controllers\ homecontroller.cs**

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample1.cs)]

リスト1のコントローラーには、コンストラクターが含まれていることに注意してください。 コンストラクターは \_db という名前のクラスレベルのフィールドを初期化します。 \_db フィールドは、Microsoft Entity Framework によって生成されるデータベースエンティティを表します。 \_db フィールドは、Entity Designer によって生成された MoviesDBEntities クラスのインスタンスです。

Home コントローラーで Oviesdbentities クラスを使用するには、Mogo Entityapp. Model 名前空間 (*Mvcprojectname*) をインポートする必要があります。モデル)。

\_db フィールドは、ムービーデータベーステーブルからレコードを取得するために Index () アクション内で使用されます。 式 \_db です。Mo視聴セットは、ムービーデータベーステーブルのすべてのレコードを表します。 ToList () メソッドは、ムービーのセットを、ムービーオブジェクトのジェネリックコレクション (List&lt;Movie&gt;) に変換するために使用されます。

ムービーレコードは LINQ to Entities のヘルプを使用して取得されます。 リスト1の Index () アクションでは、LINQ*メソッド構文*を使用してデータベースレコードのセットを取得します。 必要に応じて、代わりに LINQ*クエリ構文*を使用できます。 次の2つのステートメントは、まったく同じことを行います。

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample2.cs)]

最も直感的にわかるような LINQ 構文 (メソッド構文またはクエリ構文) を使用します。 2つの方法の間でパフォーマンスに違いはありません。唯一の違いは style です。

リスト2のビューは、ムービーレコードを表示するために使用されます。

**リスト2– Views\Home\Index.aspx**

[!code-aspx[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample3.aspx)]

リスト2のビューには、各ムービーレコードを反復処理し、ムービーレコードのタイトルと監督のプロパティの値を表示する**foreach**ループが含まれています。 各レコードの横に [編集] リンクと [削除] リンクが表示されます。 さらに、[ムービーの追加] リンクがビューの下部に表示されます (図7を参照)。

**図 7: インデックスビュー**

![clip_image014](creating-model-classes-with-the-entity-framework-cs/_static/image7.jpg)

インデックスビューは、*型指定*されたビューです。 インデックスビューには、&lt;% @ Page%&gt; ディレクティブが含まれています。これは、Model プロパティを、ムービーオブジェクト (List&lt;Movie) の厳密に型指定されたジェネリックリストコレクションにキャストする*継承*属性です。

## <a name="inserting-database-records-with-the-entity-framework"></a>Entity Framework を使用したデータベースレコードの挿入

Entity Framework を使用すると、データベーステーブルに新しいレコードを簡単に挿入できます。 リスト3には、新しいレコードをムービーデータベーステーブルに挿入するために使用できる Home controller クラスに追加された2つの新しいアクションが含まれています。

**リスト3– Controllers\ homecontroller.cs (メソッドの追加)**

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample4.cs)]

最初の Add () アクションでは、単にビューを返します。 このビューには、新しいムービーデータベースレコードを追加するためのフォームが含まれています (図8を参照)。 フォームを送信すると、2番目の Add () アクションが呼び出されます。

2番目の Add () アクションが、AcceptVerbs 属性で修飾されていることに注意してください。 このアクションは、HTTP POST 操作を実行する場合にのみ呼び出すことができます。 つまり、このアクションは、HTML フォームを投稿するときにのみ呼び出すことができます。

2番目の Add () アクションは、ASP.NET MVC TryUpdateModel () メソッドを使用して、Entity Framework Movie クラスの新しいインスタンスを作成します。 TryUpdateModel () メソッドは、Add () メソッドに渡された FormCollection 内のフィールドを受け取り、これらの HTML フォームフィールドの値を Movie クラスに割り当てます。

Entity Framework を使用する場合は、TryUpdateModel メソッドまたは UpdateModel メソッドを使用してエンティティクラスのプロパティを更新するときに、プロパティの "ホワイトリスト" を指定する必要があります。

次に、Add () アクションは、単純なフォーム検証を実行します。 アクションは、Title プロパティと Director プロパティの両方に値があることを確認します。 検証エラーが発生した場合は、検証エラーメッセージが ModelState に追加されます。

検証エラーがない場合は、Entity Framework のヘルプを含む新しいムービーレコードがムービーデータベーステーブルに追加されます。 新しいレコードは、次の2行のコードを使用してデータベースに追加されます。

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample5.cs)]

コードの1行目では、Entity Framework によって追跡されている一連のムービーに新しい Movie エンティティを追加します。 コードの2行目では、追跡しているムービーに加えられたすべての変更を、基になるデータベースに保存します。

**図 8: [追加] ビュー**

![clip_image016](creating-model-classes-with-the-entity-framework-cs/_static/image8.jpg)

#### <a name="updating-database-records-with-the-entity-framework"></a>Entity Framework を使用したデータベースレコードの更新

ほぼ同じアプローチに従って、新しいデータベースレコードを挿入する方法として Entity Framework を使用してデータベースレコードを編集できます。 リスト4には、Edit () という名前の新しいコントローラーアクションが2つ含まれています。 最初の Edit () アクションでは、ムービーレコードを編集するための HTML フォームが返されます。 2番目の Edit () アクションは、データベースを更新しようとします。

**リスト4– Controllers\ homecontroller.cs (メソッドの編集)**

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample6.cs)]

2番目の Edit () アクションは、編集中のムービーの Id と一致するムービーレコードをデータベースから取得することによって開始されます。 次の LINQ to Entities ステートメントは、特定の Id に一致する最初のデータベースレコードを取得します。

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample7.cs)]

次に、TryUpdateModel () メソッドを使用して、HTML フォームフィールドの値を movie エンティティのプロパティに割り当てます。 更新するプロパティを正確に指定するためのホワイトリストが提供されていることに注意してください。

次に、ムービータイトルとディレクタープロパティの両方に値が設定されていることを確認するために、いくつかの単純な検証を実行します。 いずれかのプロパティに値が指定されていない場合、ModelState と ModelState に検証エラーメッセージが追加されます。 IsValid は値 false を返します。

最後に、検証エラーがない場合は、SaveChanges () メソッドを呼び出すことにより、基になるムービーデータベーステーブルが変更されて更新されます。

データベースレコードを編集する場合は、編集するレコードの Id を、データベースの更新を実行するコントローラーアクションに渡す必要があります。 それ以外の場合、コントローラーアクションは、基になるデータベースで更新するレコードを認識しません。 リスト5に含まれる編集ビューには、編集中のデータベースレコードの Id を表す非表示のフォームフィールドが含まれています。

**リスト5– Views\Home\Edit.aspx**

[!code-aspx[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample8.aspx)]

## <a name="deleting-database-records-with-the-entity-framework"></a>Entity Framework を使用したデータベースレコードの削除

このチュートリアルで対処する必要がある最後のデータベース操作は、データベースレコードを削除することです。 リスト6のコントローラーアクションを使用して、特定のデータベースレコードを削除できます。

**リスト 6--\Controllers\HomeController.cs (Delete アクション)**

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample9.cs)]

Delete () アクションは、アクションに渡された Id と一致するムービーエンティティを最初に取得します。 次に、DeleteObject () メソッドを呼び出し、その後に SaveChanges () メソッドを呼び出して、ムービーをデータベースから削除します。 最後に、ユーザーはインデックスビューにリダイレクトされます。

## <a name="summary"></a>まとめ

このチュートリアルの目的は、ASP.NET MVC と Microsoft Entity Framework を利用して、データベース駆動型 web アプリケーションを構築する方法を示すことでした。 データベースレコードの選択、挿入、更新、および削除を可能にするアプリケーションを構築する方法について学習しました。

まず、Entity Data Model ウィザードを使用して、Visual Studio 内から Entity Data Model を生成する方法について説明しました。 次に、LINQ to Entities を使用してデータベーステーブルから一連のデータベースレコードを取得する方法について説明します。 最後に、Entity Framework を使用して、データベースレコードを挿入、更新、および削除しています。

> [!div class="step-by-step"]
> [Next](creating-model-classes-with-linq-to-sql-cs.md)
