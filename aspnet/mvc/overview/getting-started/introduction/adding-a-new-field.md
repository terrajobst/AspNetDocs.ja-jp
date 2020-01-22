---
uid: mvc/overview/getting-started/introduction/adding-a-new-field
title: 新しいフィールドの追加 |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 10/17/2013
ms.assetid: 4085de68-d243-4378-8a64-86236ea8d2da
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-a-new-field
msc.type: authoredcontent
ms.openlocfilehash: d79655bfadff83095bf4cb84445f5efaf44d6a89
ms.sourcegitcommit: 88fc80e3f65aebdf61ec9414810ddbc31c543f04
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/22/2020
ms.locfileid: "76519077"
---
# <a name="adding-a-new-field"></a>新しいフィールドの追加

[Rick Anderson]((https://twitter.com/RickAndMSFT))

[!INCLUDE [Tutorial Note](index.md)]

このセクションでは、Entity Framework Code First Migrations を使用して、変更がデータベースに適用されるように、モデルクラスにいくつかの変更を移行します。

既定では、このチュートリアルの前に示したように Entity Framework Code First を使用してデータベースを自動的に作成すると、データベースのスキーマが生成元のモデルクラスと同期しているかどうかを追跡できるように Code First、データベースにテーブルが追加されます。 同期されていない場合は、Entity Framework によってエラーがスローされます。 これにより、開発時に問題を簡単に追跡できるようになります。これは、実行時に (あいまいなエラーによって) 検出された場合にのみ発生します。

## <a name="setting-up-code-first-migrations-for-model-changes"></a>モデル変更の Code First Migrations の設定

ソリューションエクスプローラーに移動します。 *ムービーの .mdf*ファイルを右クリックし、 **[削除]** を選択して、ムービーデータベースを削除します。 *ムービーの .mdf*ファイルが表示されない場合は、次の赤いアウトラインにある **[すべてのファイルを表示]** アイコンをクリックします。

![](adding-a-new-field/_static/image1.png)

アプリケーションをビルドしてエラーがないことを確認します。

**[ツール]** メニューで **[NuGet パッケージ マネージャー]** 、 **[パッケージ マネージャー コンソール]** の順にクリックします。

![パックマンの追加](adding-a-new-field/_static/image2.png)

**パッケージマネージャーコンソール**ウィンドウの `PM>` プロンプトで、「」と入力します。

Enable-Migrations -ContextTypeName MvcMovie.Models.MovieDBContext

![](adding-a-new-field/_static/image3.png)

(上の図に示した)**移行を有効に**するコマンドを実行すると、新しい*移行*フォルダーに*Configuration.cs*ファイルが作成されます。

![](adding-a-new-field/_static/image4.png)

Visual Studio によって*Configuration.cs*ファイルが開きます。 *Configuration.cs*ファイルの `Seed` メソッドを次のコードに置き換えます。

[!code-csharp[Main](adding-a-new-field/samples/sample1.cs)]

`Movie` の下の赤い波線の上にマウスポインターを移動し、[`Show Potential Fixes`] をクリックして、[ **mvcmovie** **を使用する**] をクリックします。

![](adding-a-new-field/_static/image5.png)

これにより、次の using ステートメントが追加されます。

[!code-csharp[Main](adding-a-new-field/samples/sample2.cs)]

> [!NOTE]
> 
> Code First Migrations は、すべての移行の後 (つまり、パッケージマネージャーコンソールで**更新プログラムデータベース**を呼び出す) に `Seed` メソッドを呼び出します。このメソッドは、既に挿入されている行を更新するか、まだ存在しない場合は挿入します。
> 
> 次のコードの[Addorupdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx)メソッドは、"upsert" 操作を実行します。
> 
> [!code-csharp[Main](adding-a-new-field/samples/sample3.cs)]
> 
> [シード](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx)メソッドはすべての移行で実行されるため、データを挿入することはできません。これは、データベースを最初に移行した後に、追加しようとしている行が既に存在するためです。 "[Upsert](http://en.wikipedia.org/wiki/Upsert)" 操作は、既に存在する行を挿入しようとすると発生するエラーを防ぎますが、アプリケーションのテスト中に行われたデータの変更を上書きします。 一部のテーブルのテストデータでは、このような処理が不要な場合があります。テスト中にデータを変更し、データベースの更新後も変更を保持する場合があります。 その場合は、条件付き挿入操作を実行します。行がまだ存在しない場合にのみ、行を挿入します。   
> 
> [Addorupdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx)メソッドに渡される最初のパラメーターは、行が既に存在するかどうかを確認するために使用するプロパティを指定します。 提供しているテストムービーデータの場合は、リスト内の各タイトルが一意であるため、この目的には `Title` プロパティを使用できます。
> 
> [!code-csharp[Main](adding-a-new-field/samples/sample4.cs)]
> 
> このコードは、タイトルが一意であることを前提としています。 重複するタイトルを手動で追加すると、次に移行を実行したときに次の例外が発生します。   
> 
> *シーケンスに複数の要素が含まれています*  
> 
> [Addorupdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx)メソッドの詳細については、「 [EF 4.3 Addorupdate メソッドに](http://thedatafarm.com/blog/data-access/take-care-with-ef-4-3-addorupdate-method/)対処する」を参照してください。

**CTRL + SHIFT + B キーを押して、プロジェクトをビルドします。** (この時点でビルドしない場合、次の手順は失敗します)。

次の手順では、初期移行のために `DbMigration` クラスを作成します。 この移行によって新しいデータベースが作成されます。これは、前の手順で*ムービー .mdf*ファイルを削除したためです。

**パッケージマネージャーコンソール**ウィンドウで、コマンド `add-migration Initial` を入力して、初期移行を作成します。 "Initial" という名前は任意であり、作成される移行ファイルに名前を指定するために使用されます。

![](adding-a-new-field/_static/image6.png)

Code First Migrations は、*移行*フォルダー ( *{datestamp}\_Initial.cs* ) に別のクラスファイルを作成します。このクラスには、データベーススキーマを作成するコードが含まれています。 移行ファイル名は、順序付けを支援するタイムスタンプで事前に固定されています。 *{Datestamp}\_Initial.cs*ファイルを調べます。このファイルには、Movie DB の `Movies` テーブルを作成するための手順が含まれています。 以下の手順でデータベースを更新すると、この *{Datestamp}\_Initial.cs*ファイルが実行され、DB スキーマが作成されます。 次に、 **Seed**メソッドを実行して、データベースにテストデータを読み込みます。

**パッケージマネージャーコンソール**で、コマンド `update-database` を入力してデータベースを作成し、`Seed` メソッドを実行します。

![](adding-a-new-field/_static/image7.png)

テーブルが既に存在して作成できないことを示すエラーが表示された場合は、データベースを削除した後、`update-database`を実行する前にアプリケーションを実行したことが原因である可能性があります。 その場合は、もう一度*ムービーの .mdf*ファイルを削除し、`update-database` コマンドを再試行してください。 それでもエラーが発生する場合は、移行フォルダとコンテンツを削除してから、このページの上部にある指示に従って作業を開始してください (*つまり、この*ページの内容を削除してから、移行の有効化に進みます)。 それでもエラーが発生する場合は、SQL Server オブジェクトエクスプローラーを開き、データベースを一覧から削除します。

アプリケーションを実行し、 */ムービー*の URL に移動します。 シードデータが表示されます。

![](adding-a-new-field/_static/image8.png)

## <a name="adding-a-rating-property-to-the-movie-model"></a>ムービー モデルへの評価プロパティの追加

まず、既存の `Movie` クラスに新しい `Rating` プロパティを追加します。 *Modelthe modelfile*を開き、次のように `Rating` プロパティを追加します。

[!code-csharp[Main](adding-a-new-field/samples/sample5.cs)]

完成した `Movie` クラスは次のコードのようになります。

[!code-csharp[Main](adding-a-new-field/samples/sample6.cs?highlight=12)]

アプリケーションをビルドします (Ctrl + Shift + B)。

新しいフィールドを `Movie` クラスに追加したので、この新しいプロパティが含まれるように、バインドの*ホワイトリスト*も更新する必要があります。 `Create` および `Edit` アクションメソッドの `bind` 属性を更新して、`Rating` プロパティを含めます。

[!code-csharp[Main](adding-a-new-field/samples/sample7.cs?highlight=1)]

ブラウザー ビューで新しい `Rating` プロパティを表示、作成、編集する目的でビュー テンプレートを更新する必要もあります。

*\Views\Movies\Index.cshtml*ファイルを開き、 **Price**列の直後に `<th>Rating</th>` 列見出しを追加します。 次に、テンプレートの末尾付近に `<td>` 列を追加して、`@item.Rating` 値を表示します。 更新されたインデックスの例を次に示し*ます。 cshtml* view テンプレートは次のようになります。

[!code-cshtml[Main](adding-a-new-field/samples/sample8.cshtml?highlight=31-33,52-54)]

次に、 *\Views\Movies\Create.cshtml*ファイルを開き、次の強調表示されたマークアップを含む `Rating` フィールドを追加します。 新しいムービーを作成するときに評価を指定できるように、テキストボックスが表示されます。

[!code-cshtml[Main](adding-a-new-field/samples/sample9.cshtml?highlight=9-15)]

これで、新しい `Rating` プロパティをサポートするようにアプリケーションコードが更新されました。

アプリケーションを実行し、 */ムービー*の URL に移動します。 ただし、この操作を行うと、次のいずれかのエラーが表示されます。

![](adding-a-new-field/_static/image9.png)  
  
データベースが作成されてから、' Mo? Dbcontext ' コンテキストをバッキングするモデルが変更されました。 Code First Migrations を使用してデータベースを更新することを検討してください (https://go.microsoft.com/fwlink/?LinkId=238269) 。

![](adding-a-new-field/_static/image10.png)

このエラーが表示されるのは、アプリケーションの更新された `Movie` モデルクラスが、既存のデータベースの `Movie` テーブルのスキーマとは異なるようになったためです。 (データベース テーブルに `Rating` 列はありません)。

このエラーを解決するための手法がいくつかあります。

1. Entity Framework に、新しいモデル クラス スキーマに基づいてデータベースを自動的にドロップさせ、再作成させます。 この手法は、開発周期の早い段階で、テスト データベースで開発しているときに非常に便利です。モデルとデータベース スキーマを一緒に短期間で発展させることができます。 ただし、この欠点は、データベース内の既存のデータが失われているため、運用データベースでこのアプローチを使用したく*ない*ということです。 初期化子を利用し、データベースにテスト データを自動的に初期投入します。多くの場合、アプリケーション開発の手法として有益な方法です。 Entity Framework データベース初期化子の詳細については、「 [ASP.NET MVC/Entity Framework チュートリアル](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)」を参照してください。
2. モデル クラスに一致するように、既存のデータベースのスキーマを明示的に変更します。 この手法の長所は、データが維持されることです。 この変更は手動で行うことも、データベース変更スクリプトを作成して行うこともできます。
3. Code First Migrations を使用して、データベース スキーマを更新します。

このチュートリアルでは、Code First Migrations を利用します。

新しい列の値を提供するように、Seed メソッドを更新します。 Migrations\ configuration.cs ファイルを開き、各ムービーオブジェクトに評価フィールドを追加します。

[!code-csharp[Main](adding-a-new-field/samples/sample10.cs?highlight=6)]

ソリューションをビルドし、 **[パッケージマネージャーコンソール]** ウィンドウを開き、次のコマンドを入力します。

`add-migration Rating`

`add-migration` のコマンドは、現在のムービーの DB スキーマを使用して現在のムービーモデルを確認し、新しいモデルにデータベースを移行するために必要なコードを作成するように移行フレームワークに指示します。 名前の*評価*は任意であり、移行ファイルの名前を指定するために使用されます。 移行手順にわかりやすい名前を使用すると便利です。

このコマンドが終了すると、Visual Studio によって、新しい `DbMigration` 派生クラスを定義するクラスファイルが開き、`Up` メソッドに新しい列を作成するコードが表示されます。

[!code-csharp[Main](adding-a-new-field/samples/sample11.cs)]

ソリューションをビルドし、 **[パッケージマネージャーコンソール]** ウィンドウで `update-database` コマンドを入力します。

次の図は、**パッケージマネージャーコンソール**ウィンドウの出力を示しています (日付スタンプの前の*評価*は異なっています)。

![](adding-a-new-field/_static/image11.png)

アプリケーションを再実行し、/ムービーの URL に移動します。 [新しい評価] フィールドが表示されます。

![](adding-a-new-field/_static/image12.png)

新しいムービーを追加するには、 **[新規作成]** リンクをクリックします。 評価を追加できることに注意してください。

![7_CreateRioII](adding-a-new-field/_static/image13.png)

**[作成]** をクリックします。 新しいムービー (評価を含む) がムービーの一覧に表示されるようになりました。

![7_ourNewMovie_SM](adding-a-new-field/_static/image14.png)

プロジェクトが移行を使用しているので、新しいフィールドを追加するとき、またはスキーマを更新するときに、データベースを削除する必要はありません。 次のセクションでは、より多くのスキーマ変更を行い、移行を使用してデータベースを更新します。

また、[編集]、[詳細]、および [削除] ビューテンプレートに `Rating` フィールドを追加する必要があります。

**パッケージマネージャーコンソール**ウィンドウに [データベースの更新] コマンドをもう一度入力すると、スキーマがモデルに一致するので、移行コードは実行されません。 ただし、"データベースの更新" を実行すると、`Seed` メソッドが再度実行されます。また、いずれかのシードデータを変更した場合は、`Seed` メソッド upsert データによって変更が失われます。 `Seed` メソッドの詳細については、Tom Dykstra の一般的な[ASP.NET MVC/Entity Framework チュートリアル](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)を参照してください。

このセクションでは、モデルオブジェクトを変更し、データベースと変更の同期を維持する方法について説明しました。 また、新しく作成されたデータベースにサンプルデータを設定して、シナリオを試す方法についても学習しました。 これは、Code First について簡単に説明したばかりです。詳細については、「 [ASP.NET MVC アプリケーションの Entity Framework データモデルを作成](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)する」を参照してください。 次に、より高度な検証ロジックをモデルクラスに追加し、一部のビジネスルールを適用できるようにする方法を見てみましょう。

> [!div class="step-by-step"]
> [前へ](adding-search.md)
> [次へ](adding-validation.md)
