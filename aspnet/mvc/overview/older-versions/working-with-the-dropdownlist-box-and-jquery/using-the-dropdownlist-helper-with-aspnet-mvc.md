---
uid: mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/using-the-dropdownlist-helper-with-aspnet-mvc
title: ASP.NET MVC で DropDownList ヘルパーを使用する |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/12/2012
ms.assetid: 53767e05-c8ab-42e1-a94b-22d906195200
msc.legacyurl: /mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/using-the-dropdownlist-helper-with-aspnet-mvc
msc.type: authoredcontent
ms.openlocfilehash: 6375bb2be158cea18309ffa71c71ac3e67bc91ed
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78433078"
---
# <a name="using-the-dropdownlist-helper-with-aspnet-mvc"></a>ASP.NET MVC で DropDownList ヘルパーを使用する

[Rick Anderson](https://twitter.com/RickAndMSFT)

このチュートリアルでは、ASP.NET MVC Web アプリケーションで[DropDownList](https://msdn.microsoft.com/library/dd492948.aspx)ヘルパーと[ListBox](https://msdn.microsoft.com/library/system.web.mvc.html.selectextensions.listbox.aspx)ヘルパーを操作するための基本について説明します。 このチュートリアルに従うには、Microsoft Visual Web Developer 2010 Express Service Pack 1 を使用できます。これは Microsoft Visual Studio の無料版です。 開始する前に、以下に示す前提条件がインストールされていることを確認してください。 これらのすべてをインストールするには、次のリンクをクリックします。[Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。 または、次のリンクを使用して、前提条件を個別にインストールすることもできます。

- [Visual Studio Web Developer EXPRESS SP1 の前提条件](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)<a id="post"></a>
- [ASP.NET MVC 3 ツールの更新](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
- [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(ランタイム + ツールのサポート)

Visual Web Developer 2010 ではなく Visual Studio 2010 を使用している場合は、次のリンクをクリックして必要なコンポーネントをインストールします。[Visual Studio 2010 の前提条件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。 このチュートリアルでは、 [ASP.NET mvc](../getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)チュートリアルまたは[ASP.NET mvc ミュージックストア](../mvc-music-store/mvc-music-store-part-1.md)チュートリアルが完了していることを前提としています。または、ASP.NET mvc の開発に精通していることを前提としています。 このチュートリアルでは、 [ASP.NET MVC Music Store](../mvc-music-store/mvc-music-store-part-1.md)チュートリアルの変更されたプロジェクトから始めます。 次のリンクを使用してスタートプロジェクトをダウンロードし、[バージョンをC#ダウンロード](https://archive.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=15829)することができます。

チュートリアルC#のソースコードが完成した Visual Web Developer プロジェクトは、このトピックに付属しています。 を[ダウンロード](https://code.msdn.microsoft.com/Using-the-DropDownList-67f9367d)します。

### <a name="what-youll-build"></a>作成するアプリケーション:

[DropDownList](https://msdn.microsoft.com/library/system.web.mvc.html.selectextensions.dropdownlist.aspx)ヘルパーを使用してカテゴリを選択するアクションメソッドとビューを作成します。 また、 **jQuery**を使用して、新しいカテゴリ (ジャンルやアーティストなど) が必要な場合に使用できる [カテゴリの挿入] ダイアログを追加します。 新しいジャンルを追加して新しいアーティストを追加するためのリンクを示す [作成] ビューのスクリーンショットを次に示します。

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image1.png)

### <a name="skills-youll-learn"></a>学習内容

ここでは次の内容について学習します。

- [DropDownList](https://msdn.microsoft.com/library/system.web.mvc.html.selectextensions.dropdownlist.aspx)ヘルパーを使用してカテゴリデータを選択する方法。
- 新しいカテゴリを追加するための**jQuery**ダイアログを追加する方法。

### <a name="getting-started"></a>はじめに

まず、次のリンクを使用してスタートプロジェクト[をダウンロードします。](https://archive.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=15829) Windows エクスプローラーで、 *DDL\_Starter*ファイルを右クリックし、[プロパティ] を選択します。 [ **DDL\_のプロパティ**] ダイアログボックスで、[ブロックの解除] を選択します。

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image2.png)

DDL\_Starter ファイルを右クリックし、 **[すべて展開]** を選択して、ファイルを解凍します。 Visual Web Developer 2010 Express ("Visual Web Developer" または "VWD")、または Visual Studio 2010 を使用して、 *StartMusicStore*ファイルを開きます。

CTRL キーを押しながら F5 キーを押してアプリケーションを実行し、 **[テスト]** リンクをクリックします。

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image3.png)

**[ムービーカテゴリの選択 (簡易)]** リンクを選択します。 選択した値をコメディて、ムービーの種類の選択リストが表示されます。

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image4.png)

ブラウザーを右クリックし、[ソースの表示] を選択します。 ページの HTML が表示されます。 次のコードは、select 要素の HTML を示しています。

[!code-html[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample1.html)]

選択リストの各項目には値 (Action には0、ドラマには1、コメディの場合は1、サイエンスの場合は 3) と表示名 (Action、ドラマ、コメディ、およびサイエンス) が表示されます。 上記のコードは、選択リストの標準 HTML です。

選択リストをドラマに変更し、 **[送信]** ボタンをクリックします。 ブラウザーの URL が `http://localhost:2468/Home/CategoryChosen?MovieType=1`、選択した **ページが表示されます。1**。

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image5.png)

*Controllers\ homecontroller.cs*ファイルを開き、`SelectCategory` メソッドを確認します。

[!code-csharp[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample2.cs)]

HTML 選択リストを作成するために使用される[DropDownList](https://msdn.microsoft.com/library/dd492738.aspx)ヘルパーには、明示的または暗黙的に**IEnumerable&lt;selectlistitem &gt;** が必要です。 つまり、 **ienumerable&lt;selectlistitem &gt;** を明示的に[DropDownList](https://msdn.microsoft.com/library/dd492738.aspx)ヘルパーに渡すことができます。または、モデルプロパティとして**selectlistitem**に同じ名前を使用して、 **ienumerable&lt;selectlistitem &gt;** を[ViewBag](https://blogs.msdn.com/b/rickandy/archive/2011/01/28/dynamic-v-strongly-typed-views.aspx)に追加することができます。 **Selectlistitem**を暗黙的かつ明示的に渡す方法については、チュートリアルの次の部分で説明します。 上のコードは、 **IEnumerable&lt;SelectListItem &gt;** を作成し、テキストと値を設定するための最も簡単な方法を示しています。 `Comedy`[Selectlistitem](https://msdn.microsoft.com/library/system.web.mvc.selectlistitem.aspx)には、[選択した](https://msdn.microsoft.com/library/system.web.mvc.selectlistitem.selected.aspx)プロパティが**true**に設定されていることに注意してください。これにより、表示される選択リストでは、リスト内の選択した項目として**コメディ**が表示されます。

上で作成した**IEnumerable&lt;SelectListItem &gt;** が、Mo[ViewBag](https://blogs.msdn.com/b/rickandy/archive/2011/01/28/dynamic-v-strongly-typed-views.aspx) type という名前のに追加されます。 次に示すように、 **IEnumerable&lt;SelectListItem &gt;** 暗黙的に[DropDownList](https://msdn.microsoft.com/library/dd492738.aspx)ヘルパーに渡す方法について説明します。

*Views\Home\SelectCategory.cshtml*ファイルを開き、マークアップを確認します。

[!code-cshtml[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample3.cshtml)]

3行目では、レイアウトを Views/Shared/\_Simple\_Layout に設定します。これは、標準レイアウトファイルの簡略化されたバージョンです。 これを実行して、表示と HTML の表示を単純にします。

このサンプルでは、アプリケーションの状態を変更しないので、http **POST**ではなく**http GET**を使用してデータを送信します。 [HTTP GET または POST を選択する場合](http://www.w3.org/2001/tag/doc/whenToUseGet.html#checklist)は、W3C の「クイックチェックリスト」を参照してください。 アプリケーションを変更したりフォームを投稿したりすることはないため、アクションメソッド、コントローラー、およびフォームメソッド (**HTTP POST**または**http GET**) を指定できるようにするために、 [Html. beginform](https://msdn.microsoft.com/library/dd460344.aspx)のオーバーロードを使用します。 通常、ビューには、パラメーターを取らない[Html の BeginForm](https://msdn.microsoft.com/library/dd505244.aspx)オーバーロードが含まれています。 パラメーターのバージョンを指定しない場合、既定では、同じアクションメソッドとコントローラーのポストバージョンにフォームデータがポストされます。

次の行

[!code-cshtml[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample4.cshtml)]

**DropDownList**ヘルパーに文字列引数を渡します。 この例の "Moの種類" という文字列は、次の2つの処理を行います。

- このメソッドは、 **ViewBag**内の**IEnumerable&lt;selectlistitem &gt;** を検索するための**DropDownList**ヘルパーのキーを提供します。
- これは、Moの Type フォーム要素にデータバインドされています。 Submit メソッドが**HTTP GET**の場合、`MovieType` はクエリ文字列になります。 送信メソッドが**HTTP POST**の場合、メッセージ本文には `MovieType` が追加されます。 次の図は、値が1のクエリ文字列を示しています。

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image6.png)

次のコードは、フォームが送信された `CategoryChosen` メソッドを示しています。

[!code-csharp[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample5.cs)]

テストページに戻り、 **[HTML SelectList]** リンクを選択します。 HTML ページでは、simple ASP.NET MVC テストページと同様の選択要素がレンダリングされます。 ブラウザーウィンドウを右クリックし、 **[ソースの表示]** を選択します。 選択リストの HTML マークアップは、基本的には同じです。 HTML ページのテストは、前にテストした ASP.NET MVC アクションメソッドとビューのように機能します。

### <a name="improving-the-movie-select-list-with-enums"></a>列挙型を使用してムービー選択リストを改善する

アプリケーションのカテゴリが固定されており、変更されない場合は、列挙型を利用して、コードをより堅牢で、より簡単に拡張できるようにすることができます。 新しいカテゴリを追加すると、正しいカテゴリの値が生成されます。 では、新しいカテゴリを追加しても、カテゴリの値を更新し忘れた場合、コピーと貼り付けのエラーを回避します。

*Controllers\ homecontroller.cs*ファイルを開き、次のコードを確認します。

[!code-csharp[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample6.cs)]

[列挙](https://msdn.microsoft.com/library/sbbt4032(VS.80).aspx)`eMovieCategories` は、4種類のムービーをキャプチャします。 `SetViewBagMovieType` メソッドは、`eMovieCategories`**列挙型**から**IEnumerable&lt;selectlistitem &gt;** を作成し、`Selected` パラメーターから `selectedMovie` プロパティを設定します。 `SelectCategoryEnum` アクションメソッドは、`SelectCategory` のアクションメソッドと同じビューを使用します。

テストページに移動し、[`Select Movie Category (Enum)`] リンクをクリックします。 今回は、値 (数値) を表示するのではなく、列挙体を表す文字列が表示されます。

### <a name="posting-enum-values"></a>列挙値のポスト

通常、HTML フォームは、データをサーバーにポストするために使用されます。 次のコードは、`SelectCategoryEnumPost` メソッドの `HTTP GET` と `HTTP POST` バージョンを示しています。

[!code-csharp[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample7.cs)]

`eMovieCategories` 列挙型を `POST` メソッドに渡すことによって、列挙値と列挙型文字列の両方を抽出できます。 サンプルを実行し、[テスト] ページに移動します。 [`Select Movie Category(Enum Post)`] リンクをクリックします。 ムービーの種類を選択し、[送信] ボタンをクリックします。 表示には、ムービーの種類の値と名前の両方が表示されます。

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image7.png)

### <a name="creating-a-multiple-section-select-element"></a>複数のセクションの Select 要素の作成

[ListBox](https://msdn.microsoft.com/library/system.web.mvc.html.selectextensions.listbox.aspx) html ヘルパーは、html `<select>` 要素を `multiple` 属性でレンダリングします。これにより、ユーザーは複数の選択を行うことができます。 テストリンクに移動し、 **[複数選択の国]** リンクを選択します。 レンダリングされた UI を使用すると、複数の国を選択できます。 次の図では、カナダと中国が選択されています。

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image8.png)

### <a name="examining-the-multiselectcountry-code"></a>MultiSelectCountry コードを調べる

*Controllers\ homecontroller.cs*ファイルから次のコードを確認します。

[!code-csharp[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample8.cs)]

`GetCountries` メソッドは、国の一覧を作成し、それを `MultiSelectList` コンストラクターに渡します。 上記の `GetCountries` メソッドで使用される `MultiSelectList` コンストラクターオーバーロードは、次の4つのパラメーターを受け取ります。

[!code-csharp[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample9.cs)]

1. *項目*:リスト内の項目を格納している[IEnumerable](https://msdn.microsoft.com/library/system.collections.ienumerable.aspx) 。 上記の例では、国の一覧です。
2. *dataValueField*:値を格納している**IEnumerable**リスト内のプロパティの名前。 上記の例では、`ID` プロパティです。
3. *Datatextfield*:表示する情報が格納されている**IEnumerable**リスト内のプロパティの名前。 上記の例では、`name` プロパティです。
4. *Selectedvalues*:選択された値の一覧。

上記の例では、`MultiSelectCountry` メソッドによって選択された国の `null` 値が渡されるため、UI を表示するときに国は選択されません。 次のコードは、`MultiSelectCountry` ビューを表示するために使用される Razor マークアップを示しています。

[!code-cshtml[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample10.cshtml)]

上記で使用した HTML ヘルパー [ListBox](https://msdn.microsoft.com/library/dd470200.aspx)メソッドでは、2つのパラメーターを受け取ります。これは、モデルバインドに対するプロパティの名前と、select オプションと値を含む[MultiSelectList](https://msdn.microsoft.com/library/system.web.mvc.multiselectlist.aspx)です。 上記の `ViewBag.YouSelected` コードは、フォームの送信時に選択した国の値を表示するために使用されます。 `MultiSelectCountry` メソッドの HTTP POST のオーバーロードを確認します。

[!code-csharp[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample11.cs)]

`ViewBag.YouSelected` 動的プロパティには、フォームコレクションの `Countries` エントリに対して取得された、選択した国が含まれます。 このバージョンでは、GetCountries メソッドに選択した国の一覧が渡されるため、`MultiSelectCountry` ビューが表示されると、選択した国が UI で選択されます。

### <a name="making-a-select-element-friendly-with-the-harvest-chosen-jquery-plugin"></a>選択した jQuery プラグインを使用して選択要素をフレンドリ化する

[選択した jQuery プラグイン](https://harvesthq.github.com/chosen/)を HTML &lt;select&gt; 要素に追加して、ユーザーフレンドリな UI を作成できます。 次の画像は、`MultiSelectCountry` ビューで[選択](https://harvesthq.github.com/chosen/)された jQuery プラグインを示しています。

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image9.png)

次の2つの図では、**カナダ**が選択されています。

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image10.png)

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image11.png)

上の図では、カナダ が選択されています。  **x** をクリックすると、選択範囲を削除できます。 次の図は、カナダ、中国、および日本を選択した状態を示しています。

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image12.png)

### <a name="hooking-up-the-harvest-chosen-jquery-plugin"></a>選択した jQuery プラグインをフックしています

次のセクションは、jQuery の経験がある場合に簡単に実行できます。 まだ jQuery を使用したことがない場合は、次のいずれかの jQuery チュートリアルを試してみることをお勧めします。

- [John Resig](http://ejohn.org/)による[jQuery の機能](http://docs.jquery.com/Tutorials:How_jQuery_Works)
- JQuery by [Jörn Zaefferer](http://bassistance.de/) [でのはじめに](http://docs.jquery.com/Tutorials:Getting_Started_with_jQuery)
- [JQuery のライブの例 (](http://codylindley.com/blogstuff/js/jquery/#) [cody Lindley](http://codylindley.com/) )

選択したプラグインは、このチュートリアルに付属しているスターターおよび完成したサンプルプロジェクトに含まれています。 このチュートリアルでは、jQuery を使用して UI にフックするだけです。 ASP.NET MVC プロジェクトで選択した jQuery プラグインを使用するには、次のことを行う必要があります。

1. 選択したプラグインを[github](https://github.com/harvesthq/chosen/)からダウンロードします。 この手順は既に実行されています。
2. 選択したフォルダーを ASP.NET MVC プロジェクトに追加します。 前の手順でダウンロードした、選択したプラグインのアセットを、選択したフォルダーに追加します。 この手順は既に実行されています。
3. 選択したプラグインを**DropDownList**または**ListBox** HTML ヘルパーにフックします。

### <a name="hooking-up-the-chosen-plugin-to-the-multiselectcountry-view"></a>選択したプラグインを MultiSelectCountry ビューにフックします。

*Views\Home\MultiSelectCountry.cshtml*ファイルを開き、`Html.ListBox`に `htmlAttributes` パラメーターを追加します。 追加するパラメーターには、選択リスト (`@class = "chzn-select"`) のクラス名が含まれています。 完成したコードを次に示します。

[!code-cshtml[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample12.cshtml)]

上記のコードでは、`class = "chzn-select"`HTML 属性と属性値を追加しています。 クラスの前の \@ 文字は、Razor ビューエンジンとは関係ありません。 `class` は[ C#キーワード](https://msdn.microsoft.com/library/x53a06bb.aspx)です。 C#キーワードは、プレフィックスとして \@ が含まれている場合を除き、識別子として使用できません。 上の例では、`@class` は有効な識別子ですが、class はキーワードで**あるため、** **クラス**は使用できません。

選択*または選択*された jquery に参照を追加し、選択した*または選択した .css*ファイルに参照を追加します。 選択されたまたは選択された*jquery です*。選択したプラグインの機能を実装します。 *選択または選択*された .css ファイルは、スタイルを提供します。 これらの参照を*Views\Home\MultiSelectCountry.cshtml*ファイルの末尾に追加します。 次のコードは、選択したプラグインを参照する方法を示しています。

[!code-cshtml[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample13.cshtml)]

**Html. ListBox**コードで使用されているクラス名を使用して、選択したプラグインをアクティブにします。 上記の例では、クラス名は `chzn-select`です。 *Views\Home\MultiSelectCountry.cshtml* view ファイルの下部に次の行を追加します。 この行は、選択されたプラグインをアクティブにします。

[!code-html[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample14.html)]

次の行は、`chzn-select`クラス名を持つ DOM 要素を選択する jQuery ready 関数を呼び出す構文です。

[!code-powershell[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample15.ps1)]

上記の呼び出しから返されたラップされたセットは、選択したメソッド (`.chosen();`) を適用し、選択したプラグインをフックします。

次のコードは、完成した*Views\Home\MultiSelectCountry.cshtml* view ファイルを示しています。

[!code-cshtml[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample16.cshtml)]

アプリケーションを実行し、[`MultiSelectCountry`] ビューに移動します。 国を追加および削除してみてください。 提供されるサンプルダウンロードには、 **ViewBag**の代わりにビューモデルを使用して MultiSelectCountry 機能を実装する `MultiCountryVM` メソッドとビューも含まれています。

次のセクションでは、ASP.NET MVC のスキャフォールディング機構と**DropDownList**ヘルパーの連携について説明します。

> [!div class="step-by-step"]
> [Next](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper.md)
