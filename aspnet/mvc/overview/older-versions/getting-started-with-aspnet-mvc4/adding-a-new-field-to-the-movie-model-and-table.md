---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-new-field-to-the-movie-model-and-table
title: ムービーモデルとテーブルに新しいフィールドを追加する |Microsoft Docs
author: Rick-Anderson
description: '注: このチュートリアルの更新バージョンは、ASP.NET MVC 5 と Visual Studio 2013 を使用するこちらで入手できます。 より安全で、より簡単にフォローとデモができます...'
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 9ef2c4f1-a305-4e0a-9fb8-bfbd9ef331d9
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-new-field-to-the-movie-model-and-table
msc.type: authoredcontent
ms.openlocfilehash: d966b95163f64b20a17d2327a12c5d6c44a4a66b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78498514"
---
# <a name="adding-a-new-field-to-the-movie-model-and-table"></a>Movie モデルとテーブルに新しいフィールドを追加する

[Rick Anderson](https://twitter.com/RickAndMSFT)

> > [!NOTE]
> > このチュートリアルの更新バージョンは、ASP.NET MVC 5 と Visual Studio 2013 を使用する[こちらで](../../getting-started/introduction/getting-started.md)入手できます。 より安全で、より簡単にフォローし、より多くの機能を紹介します。

このセクションでは、Entity Framework Code First Migrations を使用して、変更がデータベースに適用されるように、モデルクラスにいくつかの変更を移行します。

既定では、このチュートリアルの前に示したように Entity Framework Code First を使用してデータベースを自動的に作成すると、データベースのスキーマが生成元のモデルクラスと同期しているかどうかを追跡できるように Code First、データベースにテーブルが追加されます。 同期されていない場合は、Entity Framework によってエラーがスローされます。 これにより、開発時に問題を簡単に追跡できるようになります。これは、実行時に (あいまいなエラーによって) 検出された場合にのみ発生します。

## <a name="setting-up-code-first-migrations-for-model-changes"></a>モデル変更の Code First Migrations の設定

Visual Studio 2012 を使用している場合は、ソリューションエクスプローラーからの*ムービーの .mdf*ファイルをダブルクリックして、データベースツールを開きます。 Web 用の Visual Studio Express にデータベースエクスプローラーが表示され、Visual Studio 2012 にサーバーエクスプローラーが表示されます。 Visual Studio 2010 を使用している場合は、SQL Server オブジェクトエクスプローラーを使用します。

データベースツール (データベースエクスプローラー、サーバーエクスプローラーまたは SQL Server オブジェクトエクスプローラー) で、`MovieDBContext` を右クリックし、 **[削除]** を選択して、ムービーデータベースを削除します。

![](adding-a-new-field-to-the-movie-model-and-table/_static/image1.png)

ソリューションエクスプローラーに戻ります。 *ムービーの .mdf*ファイルを右クリックし、 **[削除]** を選択して、ムービーデータベースを削除します。

![](adding-a-new-field-to-the-movie-model-and-table/_static/image2.png)

アプリケーションをビルドしてエラーがないことを確認します。

**[ツール]** メニューで **[NuGet パッケージ マネージャー]** 、 **[パッケージ マネージャー コンソール]** の順にクリックします。

![パックマンの追加](adding-a-new-field-to-the-movie-model-and-table/_static/image3.png)

**パッケージマネージャーコンソール**ウィンドウの `PM>` プロンプトで、「Enable-移行-ContextTypeName MvcMovie」と入力します。

![](adding-a-new-field-to-the-movie-model-and-table/_static/image4.png)

(上の図に示した)**移行を有効に**するコマンドを実行すると、新しい*移行*フォルダーに*Configuration.cs*ファイルが作成されます。

![](adding-a-new-field-to-the-movie-model-and-table/_static/image5.png)

Visual Studio によって*Configuration.cs*ファイルが開きます。 *Configuration.cs*ファイルの `Seed` メソッドを次のコードに置き換えます。

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample1.cs)]

`Movie` の下の赤い波線を右クリックし、 **[解決]** 、[ **mvcmovie の** **使用**] の順に選択します。

![](adding-a-new-field-to-the-movie-model-and-table/_static/image6.png)

これにより、次の using ステートメントが追加されます。

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample2.cs)]

> [!NOTE] 
> 
> Code First Migrations は、すべての移行の後 (つまり、パッケージマネージャーコンソールで**更新プログラムデータベース**を呼び出す) に `Seed` メソッドを呼び出します。このメソッドは、既に挿入されている行を更新するか、まだ存在しない場合は挿入します。

**CTRL + SHIFT + B キーを押して、プロジェクトをビルドします。** (この時点でをビルドしないと、次の手順は失敗します)。

次の手順では、初期移行のために `DbMigration` クラスを作成します。 この移行によって新しいデータベースが作成されます。これは、前の手順で*ムービーの .mdf*ファイルを削除したためです。

**パッケージマネージャーコンソール**ウィンドウで、"追加-移行の初期" コマンドを入力して、初期移行を作成します。 "Initial" という名前は任意であり、作成される移行ファイルに名前を指定するために使用されます。

![](adding-a-new-field-to-the-movie-model-and-table/_static/image7.png)

Code First Migrations は、*移行*フォルダー ( *{datestamp}\_Initial.cs* ) に別のクラスファイルを作成します。このクラスには、データベーススキーマを作成するコードが含まれています。 移行ファイル名は、順序付けを支援するタイムスタンプで事前に固定されています。 *{Datestamp}\_Initial.cs*ファイルを調べます。このファイルには、Movie DB のムービーテーブルを作成するための手順が含まれています。 以下の手順でデータベースを更新すると、この *{Datestamp}\_Initial.cs*ファイルが実行され、DB スキーマが作成されます。 次に、 **Seed**メソッドを実行して、データベースにテストデータを読み込みます。

**パッケージマネージャーコンソール**で、"データベースの更新" コマンドを入力してデータベースを作成し、 **Seed**メソッドを実行します。

![](adding-a-new-field-to-the-movie-model-and-table/_static/image8.png)

テーブルが既に存在して作成できないことを示すエラーが表示された場合は、データベースを削除した後、`update-database`を実行する前にアプリケーションを実行したことが原因である可能性があります。 その場合は、もう一度*ムービーの .mdf*ファイルを削除し、`update-database` コマンドを再試行してください。 それでもエラーが発生する場合は、移行フォルダとコンテンツを削除してから、このページの上部にある指示に従って作業を開始してください (*つまり、この*ページの内容を削除してから、移行の有効化に進みます)。

アプリケーションを実行し、 */ムービー*の URL に移動します。 シードデータが表示されます。

![](adding-a-new-field-to-the-movie-model-and-table/_static/image9.png)

## <a name="adding-a-rating-property-to-the-movie-model"></a>ムービー モデルへの評価プロパティの追加

まず、既存の `Movie` クラスに新しい `Rating` プロパティを追加します。 *Modelthe modelfile*を開き、次のように `Rating` プロパティを追加します。

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample3.cs)]

完成した `Movie` クラスは次のコードのようになります。

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample4.cs?highlight=8)]

[ビルド &gt;**ビルド**] メニューコマンドを使用するか、CTRL + SHIFT + B キーを押し**て、アプリケーション**をビルドします。

`Model` クラスを更新したので、新しい `Rating` プロパティをブラウザービューで表示するために、 *\Views\Movies\Index.cshtml*および *\Views\Movies\Create.cshtml* view テンプレートも更新する必要があります。

<em>\Views\Movies\Index.cshtml</em>ファイルを開き、 <strong>Price</strong>列の直後に `<th>Rating</th>` 列見出しを追加します。 次に、テンプレートの末尾付近に `<td>` 列を追加して、`@item.Rating` 値を表示します。 更新されたインデックスの例を次に示し<em>ます。 cshtml</em> view テンプレートは次のようになります。

[!code-cshtml[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample5.cshtml?highlight=26-28,46-48)]

次に、 *\Views\Movies\Create.cshtml*ファイルを開き、フォームの末尾付近に次のマークアップを追加します。 新しいムービーを作成するときに評価を指定できるように、テキストボックスが表示されます。

[!code-cshtml[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample6.cshtml)]

これで、新しい `Rating` プロパティをサポートするようにアプリケーションコードが更新されました。

次に、アプリケーションを実行し、 */ムービー*の URL に移動します。 ただし、この操作を行うと、次のいずれかのエラーが表示されます。

![](adding-a-new-field-to-the-movie-model-and-table/_static/image10.png)

![](adding-a-new-field-to-the-movie-model-and-table/_static/image11.png)

このエラーが表示されるのは、アプリケーションの更新された `Movie` モデルクラスが、既存のデータベースの `Movie` テーブルのスキーマとは異なるようになったためです。 (データベース テーブルに `Rating` 列はありません)。

このエラーを解決するための手法がいくつかあります。

1. Entity Framework に、新しいモデル クラス スキーマに基づいてデータベースを自動的にドロップさせ、再作成させます。 この方法は、テストデータベースに対してアクティブな開発を行う場合に非常に便利です。これにより、モデルとデータベーススキーマを一緒に迅速に進化させることができます。 ただし、この欠点は、データベース内の既存のデータが失われているため、運用データベースでこのアプローチを使用したく*ない*ということです。 初期化子を使用して、データベースをテストデータで自動的にシード処理することは、多くの場合、アプリケーションを開発するための生産性の高い方法です。 Entity Framework データベース初期化子の詳細については、「Tom Dykstra の[ASP.NET MVC/Entity Framework チュートリアル](../../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)」を参照してください。
2. モデル クラスに一致するように、既存のデータベースのスキーマを明示的に変更します。 この手法の長所は、データが維持されることです。 この変更は手動で行うことも、データベース変更スクリプトを作成して行うこともできます。
3. Code First Migrations を使用して、データベース スキーマを更新します。

このチュートリアルでは、Code First Migrations を利用します。

新しい列の値を提供するように、Seed メソッドを更新します。 Migrations\ configuration.cs ファイルを開き、各ムービーオブジェクトに評価フィールドを追加します。

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample7.cs?highlight=6)]

ソリューションをビルドし、 **[パッケージマネージャーコンソール]** ウィンドウを開き、次のコマンドを入力します。

`add-migration AddRatingMig`

`add-migration` のコマンドは、現在のムービーの DB スキーマを使用して現在のムービーモデルを確認し、新しいモデルにデータベースを移行するために必要なコードを作成するように移行フレームワークに指示します。 AddRatingMig は任意であり、移行ファイルの名前を指定するために使用されます。 移行手順にわかりやすい名前を使用すると便利です。

このコマンドが終了すると、Visual Studio によって、新しい `DbMigration` 派生クラスを定義するクラスファイルが開き、`Up` メソッドに新しい列を作成するコードが表示されます。

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample8.cs)]

ソリューションをビルドし、 **[パッケージマネージャーコンソール]** ウィンドウで "データベースの更新" コマンドを入力します。

次の図は、**パッケージマネージャーコンソール**ウィンドウの出力を示しています (日付スタンプの前に AddRatingMig があります)。

![](adding-a-new-field-to-the-movie-model-and-table/_static/image12.png)

アプリケーションを再実行し、/ムービーの URL に移動します。 [新しい評価] フィールドが表示されます。

![](adding-a-new-field-to-the-movie-model-and-table/_static/image13.png)

新しいムービーを追加するには、 **[新規作成]** リンクをクリックします。 評価を追加できることに注意してください。

![7_CreateRioII](adding-a-new-field-to-the-movie-model-and-table/_static/image14.png)

**Create** をクリックしてください。 新しいムービー (評価を含む) がムービーの一覧に表示されるようになりました。

![7_ourNewMovie_SM](adding-a-new-field-to-the-movie-model-and-table/_static/image15.png)

また、[編集]、[詳細]、および [SearchIndex view] テンプレートに `Rating` フィールドを追加する必要があります。

**パッケージマネージャーコンソール**ウィンドウに [データベースの更新] コマンドをもう一度入力すると、スキーマがモデルに一致するため、変更は行われません。

このセクションでは、モデルオブジェクトを変更し、データベースと変更の同期を維持する方法について説明しました。 また、新しく作成されたデータベースにサンプルデータを設定して、シナリオを試す方法についても学習しました。 次に、より高度な検証ロジックをモデルクラスに追加し、一部のビジネスルールを適用できるようにする方法を見てみましょう。

> [!div class="step-by-step"]
> [前へ](examining-the-edit-methods-and-edit-view.md)
> [次へ](adding-validation-to-the-model.md)
