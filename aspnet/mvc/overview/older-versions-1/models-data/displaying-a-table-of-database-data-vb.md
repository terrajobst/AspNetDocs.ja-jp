---
uid: mvc/overview/older-versions-1/models-data/displaying-a-table-of-database-data-vb
title: データベースデータのテーブルを表示する (VB) |Microsoft Docs
author: microsoft
description: このチュートリアルでは、一連のデータベースレコードを表示する2つの方法について説明します。 HTML ta でデータベースレコードのセットを書式設定する2つの方法を示しています...
ms.author: riande
ms.date: 10/07/2008
ms.assetid: 5bb4587f-5bcd-44f5-b368-3c1709162b35
msc.legacyurl: /mvc/overview/older-versions-1/models-data/displaying-a-table-of-database-data-vb
msc.type: authoredcontent
ms.openlocfilehash: f2e2489ac8455913f55c746dbe05b9fe8272285b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78436738"
---
# <a name="displaying-a-table-of-database-data-vb"></a>データベース データの表を表示する (VB)

[Microsoft](https://github.com/microsoft)

[[Download PDF]\(PDF をダウンロード\)](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_11_VB.pdf)

> このチュートリアルでは、一連のデータベースレコードを表示する2つの方法について説明します。 ここでは、一連のデータベースレコードを HTML テーブルに書式設定する2つの方法について説明します。 まず、ビュー内でデータベースレコードを直接書式設定する方法を説明します。 次に、データベースレコードを書式設定するときにパーシャルを活用する方法を説明します。

このチュートリアルの目的は、ASP.NET MVC アプリケーションでデータベースデータの HTML テーブルを表示する方法について説明することです。 まず、Visual Studio に含まれているスキャフォールディングツールを使用して、レコードのセットを自動的に表示するビューを生成する方法について説明します。 次に、データベースレコードを書式設定するときに、部分をテンプレートとして使用する方法について説明します。

## <a name="create-the-model-classes"></a>モデルクラスを作成する

ここでは、ムービーデータベーステーブルのレコードのセットを表示します。 ムービーデータベーステーブルには、次の列が含まれています。

<a id="0.4_table01"></a>

| **列名** | **[データ型]** | **[NULL を許容]** |
| --- | --- | --- |
| Id | int | False |
| タイトル | Nvarchar(200) | False |
| ディレクター | NVarchar (50) | False |
| DateReleased | DateTime | False |

ASP.NET MVC アプリケーションのムービーテーブルを表すために、モデルクラスを作成する必要があります。 このチュートリアルでは、Microsoft Entity Framework を使用して、モデルクラスを作成します。

> [!NOTE] 
> 
> このチュートリアルでは、Microsoft Entity Framework を使用します。 ただし、LINQ to SQL、NHibernate、ADO.NET などの ASP.NET MVC アプリケーションでは、さまざまなテクノロジを使用してデータベースとやり取りできることを理解しておくことが重要です。

Entity Data Model ウィザードを起動するには、次の手順を実行します。

1. ソリューションエクスプローラーウィンドウで モデル フォルダーを右クリックし、メニューオプション 追加、**新しい項目** の順に選択します。
2. **[データ]** カテゴリを選択し、 **[ADO.NET Entity Data Model]** テンプレートを選択します。
3. データモデルに*MoviesDBModel*という名前を付け、 **[追加]** ボタンをクリックします。

[追加] ボタンをクリックすると、Entity Data Model ウィザードが表示されます (図1を参照)。 ウィザードを完了するには、次の手順を実行します。

1. **[モデルの内容の選択]** ステップで、 **[データベースから生成]** オプションを選択します。
2. **[データ接続の選択]** 手順で、 *MoviesDB*データ接続を使用し、接続設定に*MoviesDBEntities*という名前を使用します。 **[次へ]** をクリックします。
3. **データベースオブジェクトの選択** ステップで、テーブル ノードを展開し、映画 テーブルを選択します。 名前空間*モデル*を入力し、 **[完了]** をクリックします。

[LINQ to SQL クラスの作成 ![](displaying-a-table-of-database-data-vb/_static/image1.jpg)](displaying-a-table-of-database-data-vb/_static/image1.png)

**図 01**: LINQ to SQL クラスの作成 ([クリックしてフルサイズのイメージを表示する](displaying-a-table-of-database-data-vb/_static/image2.png))

Entity Data Model ウィザードを完了すると、Entity Data Model デザイナーが開きます。 デザイナーには、ムービーエンティティが表示されます (図2を参照)。

[Entity Data Model デザイナーの ![](displaying-a-table-of-database-data-vb/_static/image2.jpg)](displaying-a-table-of-database-data-vb/_static/image3.png)

**図 02**: Entity Data Model デザイナー ([クリックしてフルサイズのイメージを表示](displaying-a-table-of-database-data-vb/_static/image4.png))

続行する前に、1つの変更を加える必要があります。 Entity Data Wizard では、ムービーデータベーステーブルを表す、*ムービー*という名前のモデルクラスが生成されます。 映画クラスを使用して特定の映画を表現するため、クラスの名前を *、ムービーで*はなく*ムービー* (複数形ではなく単数形) に変更する必要があります。

デザイナー画面でクラスの名前をダブルクリックし、ムービーからムービーにクラスの名前を変更します。 この変更を行った後、 **[保存]** ボタン (フロッピーディスクのアイコン) をクリックして、Movie クラスを生成します。

## <a name="create-the-movies-controller"></a>ムービーコントローラーを作成する

これで、データベースレコードを表すことができるようになったので、映画のコレクションを返すコントローラーを作成できます。 Visual Studio のソリューションエクスプローラーウィンドウで、Controllers フォルダーを右クリックし、メニューオプション [**追加]、[コントローラー** ] の順に選択します (図3を参照)。

[[コントローラーの追加] メニューの ![](displaying-a-table-of-database-data-vb/_static/image3.jpg)](displaying-a-table-of-database-data-vb/_static/image5.png)

**図 03**: [コントローラーの追加] メニュー ([クリックすると、フルサイズのイメージが表示](displaying-a-table-of-database-data-vb/_static/image6.png)されます)

**[コントローラーの追加]** ダイアログが表示されたら、コントローラー名 MovieController を入力します (図4を参照)。 **[追加]** ボタンをクリックして、新しいコントローラーを追加します。

[[コントローラーの追加] ダイアログ ![](displaying-a-table-of-database-data-vb/_static/image4.jpg)](displaying-a-table-of-database-data-vb/_static/image7.png)

**図 04**: [コントローラーの追加] ダイアログボックス ([クリックすると、フルサイズの画像が表示](displaying-a-table-of-database-data-vb/_static/image8.png)されます)

データベースレコードのセットを返すように、ムービーコントローラーによって公開されている Index () アクションを変更する必要があります。 リスト1のコントローラーのようにコントローラーを変更します。

**リスト1– Controllers\MovieController.vb**

[!code-vb[Main](displaying-a-table-of-database-data-vb/samples/sample1.vb)]

リスト1では、MoviesDBEntities クラスを使用して MoviesDB データベースを表します。 式の*エンティティ。Mo視聴セット。 ToList ()* は、ムービーデータベーステーブルからすべてのムービーのセットを返します。

## <a name="create-the-view"></a>ビューを作成する

一連のデータベースレコードを HTML テーブルに表示する最も簡単な方法は、Visual Studio に用意されているスキャフォールディングを利用することです。

[ビルド] メニューの [ソリューションの**ビルド**] を選択して、アプリケーションをビルドします。 **[ビューの追加]** ダイアログボックスを開く前にアプリケーションをビルドする必要があります。そうしないと、データクラスがダイアログに表示されません。

Index () アクションを右クリックし、 **[ビューの追加]** メニューオプションを選択します (図5を参照)。

[ビューを追加 ![には](displaying-a-table-of-database-data-vb/_static/image5.jpg)](displaying-a-table-of-database-data-vb/_static/image9.png)

**図 05**: ビューを追加[する (クリックすると、フルサイズの画像が表示](displaying-a-table-of-database-data-vb/_static/image10.png)される)

**[ビューの追加]** ダイアログボックスで、 **[厳密に型指定されたビューを作成する]** チェックボックスをオンにします。 [ムービー] クラスを**ビューデータクラス**として選択します。 **ビューコンテンツ**として [*リスト*] を選択します (図6を参照)。 これらのオプションを選択すると、ムービーの一覧を表示する厳密に型指定されたビューが生成されます。

[[ビューの追加] ダイアログ ![](displaying-a-table-of-database-data-vb/_static/image6.jpg)](displaying-a-table-of-database-data-vb/_static/image11.png)

**図 06**: [ビューの追加] ダイアログボックス ([クリックすると、フルサイズの画像が表示](displaying-a-table-of-database-data-vb/_static/image12.png)されます)

**[追加]** ボタンをクリックすると、リスト2のビューが自動的に生成されます。 このビューには、映画のコレクションを反復処理し、ムービーの各プロパティを表示するために必要なコードが含まれています。

**リスト2– Views\Movie\Index.aspx**

[!code-aspx[Main](displaying-a-table-of-database-data-vb/samples/sample2.aspx)]

アプリケーションを実行するには、メニューオプション [**デバッグ]、[デバッグの開始**] の順に選択するか、F5 キーを押します。 アプリケーションを実行すると、Internet Explorer が起動します。 /ムービーの URL に移動すると、図7にページが表示されます。

[映画のテーブルを ![する](displaying-a-table-of-database-data-vb/_static/image7.jpg)](displaying-a-table-of-database-data-vb/_static/image13.png)

**図 07**: ムービーのテーブル ([クリックすると、フルサイズの画像が表示](displaying-a-table-of-database-data-vb/_static/image14.png)される)

図7のデータベースレコードのグリッドの外観について何も気にしない場合は、単純にインデックスビューを変更できます。 たとえば、インデックスビューを変更すると、 *DateReleased*ヘッダーを [*リリース日*] に変更できます。

## <a name="create-a-template-with-a-partial"></a>部分的なテンプレートを作成する

ビューが複雑すぎる場合は、ビューをパーシャルに分割することをお勧めします。 パーシャルを使用すると、ビューの理解と保守が容易になります。 各ムービーデータベースレコードをフォーマットするためのテンプレートとして使用できる部分を作成します。

部分を作成するには、次の手順に従います。

1. Views\Movie フォルダーを右クリックし、 **[ビューの追加]** メニューオプションを選択します。
2. [*部分ビュー (.ascx) を作成する*] チェックボックスをオンにします。
3. 部分的な*テンプレート*に名前を指定します。
4. **[厳密に型指定されたビューを作成する]** チェックボックスをオンにします。
5. *ビューデータクラス*として [ムービー] を選択します。
6. *ビューのコンテンツ*として [空] を選択します。
7. **[追加]** ボタンをクリックして、プロジェクトに部分を追加します。

これらの手順を完了したら、リスト3のように Molook テンプレート部分を変更します。

**リスト3– Views\Movie\MovieTemplate.ascx**

[!code-aspx[Main](displaying-a-table-of-database-data-vb/samples/sample3.aspx)]

リスト3の部分には、1行のレコードのテンプレートが含まれています。

リスト4の変更されたインデックスビューでは、Mo閲覧テンプレート partial が使用されます。

**リスト4– Views\Movie\Index.aspx**

[!code-aspx[Main](displaying-a-table-of-database-data-vb/samples/sample4.aspx)]

リスト4のビューには、すべてのムービーを反復処理する For Each ループが含まれています。 ムービーのフォーマットには、各ムービーに対して Mo視聴テンプレート部分が使用されます。 MovieTemplate は、RenderPartial () ヘルパーメソッドを呼び出すことによってレンダリングされます。

変更されたインデックスビューでは、データベースレコードのまったく同じ HTML テーブルが表示されます。 しかし、ビューは大幅に簡素化されています。

RenderPartial () メソッドは、文字列を返さないため、他のヘルパーメソッドとは異なります。 そのため、&lt;% = Html. RenderPartial ()%&gt;ではなく &lt;% .Html 部分 ()%&gt; を使用して、RenderPartial () メソッドを呼び出す必要があります。

## <a name="summary"></a>まとめ

このチュートリアルの目的は、一連のデータベースレコードを HTML テーブルに表示する方法を説明することでした。 まず、Microsoft Entity Framework を利用して、コントローラーアクションから一連のデータベースレコードを返す方法について学習しました。 次に、Visual Studio のスキャフォールディングを使用して、項目のコレクションを自動的に表示するビューを生成する方法を学習しました。 最後に、部分的なを利用して、ビューを簡略化する方法について学習しました。 各データベースレコードをフォーマットできるように、部分をテンプレートとして使用する方法について学習しました。

> [!div class="step-by-step"]
> [前へ](creating-model-classes-with-linq-to-sql-vb.md)
> [次へ](performing-simple-validation-vb.md)
