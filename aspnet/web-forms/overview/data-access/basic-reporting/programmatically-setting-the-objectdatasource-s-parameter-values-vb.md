---
uid: web-forms/overview/data-access/basic-reporting/programmatically-setting-the-objectdatasource-s-parameter-values-vb
title: ObjectDataSource のパラメーター値をプログラムで設定する (VB) |Microsoft Docs
author: rick-anderson
description: このチュートリアルでは、単一の入力パラメーターを受け取り、データを返す、DAL と BLL にメソッドを追加する方法について説明します。 この例では、次のパラメーターを設定します...
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 0ecb03b6-52a0-4731-8c7a-436391d36838
msc.legacyurl: /web-forms/overview/data-access/basic-reporting/programmatically-setting-the-objectdatasource-s-parameter-values-vb
msc.type: authoredcontent
ms.openlocfilehash: f1dd50f46528e8dd51f85e503604d3f0dbc21ad2
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74601848"
---
# <a name="programmatically-setting-the-objectdatasources-parameter-values-vb"></a>ObjectDataSource のパラメーター値をプログラムで設定する (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[サンプルアプリのダウンロード](https://download.microsoft.com/download/5/d/7/5d7571fc-d0b7-4798-ad4a-c976c02363ce/ASPNET_Data_Tutorial_6_VB.exe)または[PDF のダウンロード](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/datatutorial06vb1.pdf)

> このチュートリアルでは、単一の入力パラメーターを受け取り、データを返す、DAL と BLL にメソッドを追加する方法について説明します。 この例では、このパラメーターをプログラムによって設定します。

## <a name="introduction"></a>はじめに

[前のチュートリアル](declarative-parameters-vb.md)で見たように、パラメーター値を ObjectDataSource のメソッドに宣言的に渡すためのオプションがいくつか用意されています。 パラメーター値がハードコーディングされている場合、ページ上の Web コントロールから取得された場合、またはデータソース `Parameter` オブジェクトによって読み取り可能な他の任意のソースにある場合は、コード行を記述せずにその値を入力パラメーターにバインドできます。

ただし、組み込みのデータソース `Parameter` オブジェクトのいずれかによってまだ使用されていないソースからパラメーター値が取得される場合もあります。 サイトでユーザーアカウントがサポートされている場合は、現在ログインしているビジターのユーザー ID に基づいてパラメーターを設定することができます。 また、場合によっては、ObjectDataSource の基になるオブジェクトのメソッドに送信する前に、パラメーター値をカスタマイズする必要があります。

ObjectDataSource の `Select` メソッドが呼び出されるたびに、ObjectDataSource は最初に選択した[イベント](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.selecting%28VS.80%29.aspx)を発生させます。 次に、ObjectDataSource の基になるオブジェクトのメソッドが呼び出されます。 この処理が完了すると、ObjectDataSource の[選択されたイベント](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.selected%28VS.80%29.aspx)が発生します (図1はこの一連のイベントを示しています)。 ObjectDataSource の基になるオブジェクトのメソッドに渡されたパラメーター値は、`Selecting` イベントのイベントハンドラーで設定またはカスタマイズできます。

[ObjectDataSource の選択した ![、基になるオブジェクトのメソッドが呼び出される前と後にイベントを選択します。](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image2.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image1.png)

**図 1**: 基になるオブジェクトのメソッドが呼び出される前と後に、ObjectDataSource の `Selected` イベントと `Selecting` イベントが起動される ([クリックすると、フルサイズの画像が表示](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image3.png)されます)

このチュートリアルでは、`Integer` 型の1つの入力パラメーター `Month`を受け取り、指定された `Month`で採用記念日がある従業員を含む `EmployeesDataTable` オブジェクトを返す、DAL および BLL にメソッドを追加する方法について説明します。 この例では、現在の月に基づいて、このパラメーターをプログラムによって設定し、「今月の従業員記念日」の一覧を示します。

では、始めましょう。

## <a name="step-1-adding-a-method-toemployeestableadapter"></a>手順 1:`EmployeesTableAdapter` にメソッドを追加する

最初の例では、指定された月に `HireDate` が発生した従業員を取得するための手段を追加する必要があります。 アーキテクチャに従ってこの機能を提供するには、まず、適切な SQL ステートメントに対応する `EmployeesTableAdapter` のメソッドを作成する必要があります。 これを実現するには、まず、Northwind 型のデータセットを開きます。 `EmployeesTableAdapter` ラベルを右クリックし、[クエリの追加] を選択します。

[EmployeesTableAdapter に新しいクエリを追加 ![には](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image5.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image4.png)

**図 2**: `EmployeesTableAdapter` に新しいクエリを追加する ([クリックすると、フルサイズの画像が表示](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image6.png)されます)

行を返す SQL ステートメントを追加することを選択します。 [`SELECT` ステートメントの指定] 画面が表示されたら、`EmployeesTableAdapter` の既定の `SELECT` ステートメントが既に読み込まれています。 単に `WHERE` 句: `WHERE DATEPART(m, HireDate) = @Month`にを追加します。 [DATEPART](https://msdn.microsoft.com/library/ms174420.aspx)は、`datetime` 型の特定の日付部分を返す t-sql 関数です。この例では、`DATEPART` を使用して、`HireDate` 列の月を返しています。

[![は、HireDate 列が @HiredBeforeDate パラメーター以下の行のみを返します。](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image8.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image7.png)

**図 3**: `HireDate` 列が `@HiredBeforeDate` パラメーター以下の行のみを返す ([クリックすると、フルサイズの画像が表示](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image9.png)されます)

最後に、`FillBy` および `GetDataBy` メソッド名を `FillByHiredDateMonth` と `GetEmployeesByHiredDateMonth`にそれぞれ変更します。

[FillBy と Get![y よりも適切なメソッド名を選択します](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image11.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image10.png)

**図 4**: `FillBy` と `GetDataBy` よりも適切なメソッド名を選択[する (クリックしてフルサイズのイメージを表示する](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image12.png))

[完了] をクリックしてウィザードを完了し、データセットのデザイン画面に戻ります。 `EmployeesTableAdapter` には、指定された月に入社した従業員にアクセスするための新しい一連のメソッドが含まれるようになりました。

[新しいメソッド ![データセットのデザインサーフェイスに表示されます。](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image14.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image13.png)

**図 5**: 新しいメソッドがデータセットのデザインサーフェイスに表示される ([クリックしてフルサイズのイメージを表示する](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image15.png))

## <a name="step-2-adding-thegetemployeesbyhireddatemonthmonthmethod-to-the-business-logic-layer"></a>手順 2: ビジネスロジック層への`GetEmployeesByHiredDateMonth(month)`メソッドの追加

アプリケーションアーキテクチャでは、ビジネスロジックとデータアクセスロジックに個別のレイヤーを使用しているため、指定された日付より前に入社した従業員を取得するために、DAL を呼び出すメソッドを BLL に追加する必要があります。 `EmployeesBLL.vb` ファイルを開き、次のメソッドを追加します。

[!code-vb[Main](programmatically-setting-the-objectdatasource-s-parameter-values-vb/samples/sample1.vb)]

このクラスの他のメソッドと同様に、`GetEmployeesByHiredDateMonth(month)` は単に DAL を呼び出し、結果を返します。

## <a name="step-3-displaying-employees-whose-hiring-anniversary-is-this-month"></a>手順 3: 雇用記念日が今月である従業員を表示する

この例の最後の手順では、雇用記念日が今月である従業員を表示します。 まず、GridView を `BasicReporting` フォルダーの `ProgrammaticParams.aspx` ページに追加し、新しい ObjectDataSource をそのデータソースとして追加します。 `SelectMethod` が `GetEmployeesByHiredDateMonth(month)`に設定された `EmployeesBLL` クラスを使用するように ObjectDataSource を構成します。

[EmployeesBLL クラスを使用 ![には](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image17.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image16.png)

**図 6**: `EmployeesBLL` クラスを使用[する (クリックすると、フルサイズの画像が表示](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image18.png)されます)

[GetEmployeesByHiredDateMonth (month) メソッドから Select を ![](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image20.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image19.png)

**図 7**: `GetEmployeesByHiredDateMonth(month)` メソッドから選択する ([クリックすると、フルサイズの画像が表示](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image21.png)されます)

最後の画面では、`month` パラメーター値のソースを指定するように求められます。 この値はプログラムによって設定されるため、[パラメーターソース] を既定の [なし] に設定したままにして、[完了] をクリックします。

[パラメーターソースを None に設定したままにする ![](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image23.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image22.png)

**図 8**: パラメーターソースを None に設定したままにする ([クリックすると、フルサイズのイメージが表示](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image24.png)されます)

これにより、値が指定されていない ObjectDataSource の `SelectParameters` コレクションに `Parameter` オブジェクトが作成されます。

[!code-aspx[Main](programmatically-setting-the-objectdatasource-s-parameter-values-vb/samples/sample2.aspx)]

この値をプログラムで設定するには、ObjectDataSource の `Selecting` イベントのイベントハンドラーを作成する必要があります。 これを行うには、デザインビューにアクセスし、ObjectDataSource をダブルクリックします。 または、ObjectDataSource を選択し、プロパティウィンドウにアクセスして、[稲妻] アイコンをクリックします。 次に、`Selecting` イベントの横にあるテキストボックスをダブルクリックするか、使用するイベントハンドラーの名前を入力します。 3番目のオプションとして、イベントハンドラーを作成するには、ページの分離コードクラスの上部にある2つのドロップダウンリストから ObjectDataSource とその `Selecting` イベントを選択します。

![[プロパティ] ウィンドウの [稲妻] アイコンをクリックして、Web コントロールのイベントの一覧を表示します。](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image25.png)

**図 9**: [プロパティ] ウィンドウの稲妻アイコンをクリックして、Web コントロールのイベントを一覧表示する

3つの方法はすべて、ObjectDataSource の `Selecting` イベントの新しいイベントハンドラーをページの分離コードクラスに追加します。 このイベントハンドラーでは、`e.InputParameters(parameterName)`を使用してパラメーター値の読み取りと書き込みを行うことができます。ここで *`parameterName`* は `<asp:Parameter>` タグの `Name` 属性の値です (`InputParameters` コレクションには、`e.InputParameters(index)`のように、インデックスを作成することもできます)。 `month` パラメーターを現在の月に設定するには、`Selecting` イベントハンドラーに次のを追加します。

[!code-vb[Main](programmatically-setting-the-objectdatasource-s-parameter-values-vb/samples/sample3.vb)]

ブラウザーを使用してこのページにアクセスすると、1人の従業員のみが入社したことがわかります。この月に入社した従業員は、1994年以降、Callahan 年3月になりました。

[今月の記念日が表示されている従業員を ![します](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image27.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image26.png)

**図 10**: 今月の記念日が表示されている従業員 ([フルサイズの画像を表示するにはクリックし](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image28.png)ます)

## <a name="summary"></a>要約

ObjectDataSource のパラメーターの値は通常、コード行を必要とせずに宣言して設定できますが、パラメーター値はプログラムで簡単に設定できます。 必要なのは、ObjectDataSource の `Selecting` イベントのイベントハンドラーを作成することだけです。これは、基になるオブジェクトのメソッドが呼び出される前に発生し、`InputParameters` コレクションを介して1つ以上のパラメーターの値を手動で設定します。

このチュートリアルでは、基本的なレポートのセクションについて説明します。 [次のチュートリアル](../masterdetail/master-detail-filtering-with-a-dropdownlist-vb.md)では、「フィルター処理とマスター/詳細シナリオ」セクションを開始します。このセクションでは、ビジターがデータをフィルター処理し、マスターレポートから詳細レポートにドリルダウンできるようにする方法について説明します。

プログラミングを楽しんでください。

## <a name="about-the-author"></a>作成者について

1998以来、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)は 7 asp/創設者 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)の執筆者であり、Microsoft Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 2.0 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 mitchell@4GuysFromRolla.comでアクセスでき[ます。](mailto:mitchell@4GuysFromRolla.com) または彼のブログを参照してください。これは[http://ScottOnWriting.NET](http://ScottOnWriting.NET)にあります。

## <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビュー担当者は、Hilton Giesenow でした。 今後の MSDN 記事を確認することに興味がありますか? その場合は、mitchell@4GuysFromRolla.comの行を削除[します。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [前へ](declarative-parameters-vb.md)
