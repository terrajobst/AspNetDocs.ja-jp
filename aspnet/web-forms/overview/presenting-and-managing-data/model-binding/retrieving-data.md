---
uid: web-forms/overview/presenting-and-managing-data/model-binding/retrieving-data
title: モデルバインドと web フォームを使用したデータの取得と表示 |Microsoft Docs
author: Rick-Anderson
description: このチュートリアルシリーズでは、ASP.NET Web フォームプロジェクトでモデルバインドを使用するための基本的な側面を示します。 モデルバインドを使用すると、データの相互作用がより簡単になり-...
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 9f24fb82-c7ac-48da-b8e2-51b3da17e365
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/retrieving-data
msc.type: authoredcontent
ms.openlocfilehash: 81cca22cb4752d071d2a68986ae9ac2bed737594
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74633170"
---
# <a name="retrieving-and-displaying-data-with-model-binding-and-web-forms"></a>モデルバインドと web フォームを使用したデータの取得と表示

> このチュートリアルシリーズでは、ASP.NET Web フォームプロジェクトでモデルバインドを使用するための基本的な側面を示します。 モデルバインドを使用すると、データソースオブジェクト (ObjectDataSource や SqlDataSource など) を処理するよりも、データ操作がより簡単になります。 このシリーズでは、入門資料から開始し、以降のチュートリアルでより高度な概念に移ります。
> 
> モデルバインドパターンは、任意のデータアクセステクノロジと連携します。 このチュートリアルでは Entity Framework を使用しますが、最も使い慣れたデータアクセステクノロジを使用することもできます。 GridView、ListView、DetailsView、FormView コントロールなどのデータバインドサーバーコントロールから、データの選択、更新、削除、および作成に使用するメソッドの名前を指定します。 このチュートリアルでは、SelectMethod の値を指定します。 
> 
> そのメソッド内で、データを取得するためのロジックを提供します。 次のチュートリアルでは、UpdateMethod、DeleteMethod、および InsertMethod の値を設定します。
>
> 完全なプロジェクトは、またはC# Visual Basic で[ダウンロード](https://go.microsoft.com/fwlink/?LinkId=286116)できます。 ダウンロード可能なコードは、Visual Studio 2012 以降で動作します。 Visual Studio 2012 テンプレートが使用されています。このテンプレートは、このチュートリアルで示した Visual Studio 2017 テンプレートとは少し異なります。
> 
> このチュートリアルでは、Visual Studio でアプリケーションを実行します。 また、アプリケーションをホスティングプロバイダーに展開し、インターネット経由で使用できるようにすることもできます。 Microsoft では、最大10個の web サイトの web ホスティングを無料で提供しています。  
> [無料の Azure 試用版アカウント](https://azure.microsoft.com/free/?WT.mc_id=A443DD604)。 Visual Studio web プロジェクトを Azure App Service Web Apps にデプロイする方法の詳細については、「 [Visual studio シリーズを使用した ASP.NET Web デプロイ](../../deployment/visual-studio-web-deployment/introduction.md)」を参照してください。 このチュートリアルでは、Entity Framework Code First Migrations を使用して、SQL Server データベースを Azure SQL Database にデプロイする方法についても説明します。
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>このチュートリアルで使用されているソフトウェアのバージョン
> 
> - Microsoft Visual Studio 2017 または Microsoft Visual Studio Community 2017
>   
> このチュートリアルは、Visual Studio 2012 および Visual Studio 2013 でも動作しますが、ユーザーインターフェイスとプロジェクトテンプレートにはいくつかの違いがあります。

## <a name="what-youll-build"></a>ビルドする内容

このチュートリアルでは、次のことについて説明します。

* 学生がコースに登録されている大学を反映するデータオブジェクトを構築する
* オブジェクトからデータベーステーブルを作成する
* データベースにテストデータを設定する
* Web フォームにデータを表示する

## <a name="create-the-project"></a>プロジェクトの作成

1. Visual Studio 2017 で、 **ASP.NET Web アプリケーション (.NET Framework)** プロジェクトを作成します。このプロジェクトには、"_ **Osouniversitymodelbinding**" という名前を付いています。

   ![プロジェクトの作成](retrieving-data/_static/image19.png)

2. **[OK]** を選択します。 テンプレートを選択するためのダイアログボックスが表示されます。

   ![web フォームの選択](retrieving-data/_static/image3.png)

3. **[Web フォーム]** テンプレートを選択します。 

4. 必要に応じて、認証を**個々のユーザーアカウント**に変更します。 

5. **[OK]** をクリックして、プロジェクトを作成します。

## <a name="modify-site-appearance"></a>サイトの外観を変更する

   サイトの外観をカスタマイズするには、いくつかの変更を行います。 
   
   1. サイトのマスターファイルを開きます。
   
   2. **ASP.NET アプリケーション**ではなく、 **Contoso 大学**を表示するようにタイトルを変更します。

      [!code-aspx-csharp[Main](retrieving-data/samples/sample1.aspx?highlight=1)]

   3. ヘッダーテキストを**アプリケーション名**から**Contoso 大学**に変更します。

      [!code-aspx-csharp[Main](retrieving-data/samples/sample2.aspx?highlight=7)]

   4. ナビゲーションヘッダーリンクをサイト適切なサイトに変更します。 
   
      **About**と**Contact**のリンクを削除し、代わりに **[学生]** ページにリンクします。このページでは、作成します。

      [!code-aspx-csharp[Main](retrieving-data/samples/sample3.aspx)]

   5. Site. Master を保存します。

## <a name="add-a-web-form-to-display-student-data"></a>学生データを表示するための web フォームを追加する

   1. **ソリューションエクスプローラー**で、プロジェクトを右クリックし、 **[追加]** 、 **[新しい項目]** の順に選択します。 
   
   2. **[新しい項目の追加]** ダイアログボックスで、**マスターページ**テンプレートを使用して Web フォームを選択し、「 **student .aspx**」という名前を付けます。

      ![ページの作成](retrieving-data/_static/image5.png)

   3. **[追加]** を選びます。
   
   4. Web フォームのマスターページの場合は、 **[.master]** を選択します。
   
   5. **[OK]** を選択します。

## <a name="add-the-data-model"></a>データ モデルを追加する

**[モデル]** フォルダーで、 **UniversityModels.cs**という名前のクラスを追加します。

   1. **[モデル]** を右クリックし、 **[追加]** 、 **[新しい項目]** の順に選択します。 **[新しい項目の追加]** ダイアログ ボックスが表示されます。

   2. 左側のナビゲーションメニューから、 **[Code]** 、 **[Class]** の順に選択します。

      ![モデルクラスの作成](retrieving-data/_static/image20.png)

   3. クラスに**UniversityModels.cs**という名前を指定し、 **[追加]** を選択します。

      このファイルで、`SchoolContext`、`Student`、`Enrollment`、および `Course` クラスを次のように定義します。

      [!code-csharp[Main](retrieving-data/samples/sample4.cs)]

      `SchoolContext` クラスは、データベース接続とデータの変更を管理する `DbContext`から派生します。

      `Student` クラスで、`FirstName`、`LastName`、および `Year` の各プロパティに適用されている属性を確認します。 このチュートリアルでは、これらの属性を使用してデータを検証します。 コードを簡略化するために、これらのプロパティのみがデータ検証属性でマークされます。 実際のプロジェクトでは、検証が必要なすべてのプロパティに検証属性を適用します。

   4. UniversityModels.cs を保存します。

## <a name="set-up-the-database-based-on-classes"></a>クラスに基づいてデータベースを設定する

このチュートリアルでは、 [Code First Migrations](https://docs.microsoft.com/ef/ef6/modeling/code-first/migrations/)を使用してオブジェクトとデータベーステーブルを作成します。 これらのテーブルには、学生とそのコースに関する情報が格納されます。

   1. [**ツール** > **NuGet パッケージマネージャー** > **パッケージマネージャーコンソール**] を選択します。

   2. **パッケージマネージャーコンソール**で、次のコマンドを実行します。  
      `enable-migrations -ContextTypeName ContosoUniversityModelBinding.Models.SchoolContext`

      コマンドが正常に完了した場合は、移行が有効になっているというメッセージが表示されます。

      ![移行を有効にする](retrieving-data/_static/image8.png)

      *Configuration.cs*という名前のファイルが作成されていることに注意してください。 `Configuration` クラスには、データベーステーブルにテストデータを事前に設定できる `Seed` メソッドがあります。

## <a name="pre-populate-the-database"></a>データベースを事前設定する

   1. Configuration.cs を開きます。
   
   2. `Seed` メソッドに次のコードを追加します。 また、`ContosoUniversityModelBinding. Models` 名前空間の `using` ステートメントも追加します。

      [!code-csharp[Main](retrieving-data/samples/sample5.cs)]

   3. Configuration.cs を保存します。

   4. パッケージマネージャーコンソールで、 **[追加-移行の初期]** コマンドを実行します。

   5. コマンド**update-database**を実行します。

      このコマンドの実行時に例外が発生した場合は、`StudentID` と `CourseID` の値が `Seed` メソッドの値と異なる可能性があります。 これらのデータベーステーブルを開き、`StudentID` と `CourseID`の既存の値を検索します。 これらの値をコードに追加して、`Enrollments` テーブルをシード処理します。

## <a name="add-a-gridview-control"></a>GridView コントロールの追加

データベースデータが入力されたので、そのデータを取得して表示する準備ができました。 

1. Student を開きます。

2. `MainContent` プレースホルダーを見つけます。 このプレースホルダー内に、このコードを含む**GridView**コントロールを追加します。

   [!code-aspx-csharp[Main](retrieving-data/samples/sample6.aspx)]

   注意点:
   * GridView 要素の `SelectMethod` プロパティに設定されている値に注目してください。 この値は、次の手順で作成する GridView データを取得するために使用するメソッドを指定します。 
   
   * `ItemType` プロパティは、前に作成した `Student` クラスに設定されます。 この設定により、マークアップでクラスのプロパティを参照できます。 たとえば、`Student` クラスには、`Enrollments`という名前のコレクションがあります。 `Item.Enrollments` を使用してそのコレクションを取得し、 [LINQ 構文](https://docs.microsoft.com/dotnet/csharp/programming-guide/concepts/linq/query-syntax-and-method-syntax-in-linq)を使用して各学生の登録済みクレジットの合計を取得することができます。
   
3. Student を保存します。

## <a name="add-code-to-retrieve-data"></a>データを取得するコードを追加する

   Student 分離コードファイルで、`SelectMethod` 値に指定されたメソッドを追加します。 
   
   1. Students.aspx.cs を開きます。
   
   2. `ContosoUniversityModelBinding. Models` と `System.Data.Entity` 名前空間に `using` ステートメントを追加します。

      [!code-csharp[Main](retrieving-data/samples/sample7.cs)]

   3. `SelectMethod`に指定したメソッドを追加します。

      [!code-csharp[Main](retrieving-data/samples/sample8.cs)]

      `Include` 句を指定すると、クエリのパフォーマンスが向上しますが、必須ではありません。 `Include` 句を指定しない場合は、[*遅延読み込み*](https://en.wikipedia.org/wiki/Lazy_loading)を使用してデータが取得されます。これには、関連するデータが取得されるたびに、データベースに個別のクエリを送信する必要があります。 `Include` 句を使用すると、*一括読み込み*を使用してデータが取得されます。これは、1つのデータベースクエリですべての関連データを取得することを意味します。 関連するデータが使用されていない場合は、より多くのデータが取得されるため、一括読み込みの方が効率が悪くなります。 ただし、この場合、一括読み込みでは、各レコードの関連データが表示されるため、最適なパフォーマンスが得られます。

      関連データを読み込むときのパフォーマンスに関する考慮事項の詳細については、「 [ASP.NET MVC アプリケーションでの Entity Framework を使用した関連データの読み取り](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)」の記事の「関連データ**の遅延、一括読み込み、明示的な読み込み**」セクションを参照してください。

      既定では、データは、キーとしてマークされているプロパティの値によって並べ替えられます。 `OrderBy` 句を追加して、別の並べ替え値を指定できます。 この例では、並べ替えに既定の `StudentID` プロパティが使用されています。 データの[並べ替え、ページング、およびフィルター処理](sorting-paging-and-filtering-data.md)の記事では、ユーザーは並べ替えの対象となる列を選択できます。
 
   4. Students.aspx.cs を保存します。

## <a name="run-your-application"></a>アプリケーションを実行する 

Web アプリケーション (**F5**) を実行し、 **[Students]** ページに移動します。次の内容が表示されます。

   ![データの表示](retrieving-data/_static/image16.png)

## <a name="automatic-generation-of-model-binding-methods"></a>モデルバインドメソッドの自動生成

このチュートリアルシリーズを通じて作業する場合は、チュートリアルのコードをプロジェクトにコピーするだけで済みます。 ただし、この方法の欠点の1つは、モデルバインドメソッドのコードを自動的に生成するために Visual Studio によって提供される機能を認識できないことです。 独自のプロジェクトで作業する場合、自動コード生成によって時間を節約し、操作を実装する方法を理解するのに役立ちます。 このセクションでは、自動コード生成機能について説明します。 このセクションは情報提供のみを目的としており、プロジェクトに実装する必要があるコードは含まれていません。 

マークアップコードで `SelectMethod`、`UpdateMethod`、`InsertMethod`、または `DeleteMethod` プロパティの値を設定する場合は、[**新しいメソッドを作成**する] オプションを選択できます。

![メソッドを作成する](retrieving-data/_static/image18.png)

Visual Studio では、適切なシグネチャを持つ分離コードでメソッドが作成されるだけでなく、操作を実行する実装コードも生成されます。 自動コード生成機能を使用する前に最初に `ItemType` プロパティを設定した場合、生成されたコードはその型を操作に使用します。 たとえば、`UpdateMethod` プロパティを設定すると、次のコードが自動的に生成されます。

[!code-csharp[Main](retrieving-data/samples/sample9.cs)]

ここでも、このコードをプロジェクトに追加する必要はありません。 次のチュートリアルでは、新しいデータを更新、削除、および追加するためのメソッドを実装します。

## <a name="summary"></a>まとめ

このチュートリアルでは、データモデルクラスを作成し、それらのクラスからデータベースを生成しました。 データベーステーブルにテストデータが格納されています。 モデルバインドを使用してデータベースからデータを取得し、GridView でデータを表示しています。

このシリーズの次の[チュートリアル](updating-deleting-and-creating-data.md)では、データの更新、削除、および作成を有効にします。

> [!div class="step-by-step"]
> [Next](updating-deleting-and-creating-data.md)
