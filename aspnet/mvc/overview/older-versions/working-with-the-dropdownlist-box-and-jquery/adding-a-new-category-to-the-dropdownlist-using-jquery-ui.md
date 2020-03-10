---
uid: mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/adding-a-new-category-to-the-dropdownlist-using-jquery-ui
title: JQuery UI を使用して DropDownList に新しいカテゴリを追加する |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/12/2012
ms.assetid: 44aa1ac4-6ea2-48a2-972d-52710c48eae5
msc.legacyurl: /mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/adding-a-new-category-to-the-dropdownlist-using-jquery-ui
msc.type: authoredcontent
ms.openlocfilehash: 3207079ee468232e5f75b081421241c232936baf
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78433156"
---
# <a name="adding-a-new-category-to-the-dropdownlist-using-jquery-ui"></a>jQuery UI を使用し、DropDownList に新しいカテゴリを追加する

[Rick Anderson](https://twitter.com/RickAndMSFT)

HTML `Select` タグは、固定カテゴリデータの一覧を表示するのに最適ですが、多くの場合、新しいカテゴリを追加する必要があります。 ジャンル "Opera" をデータベースのカテゴリに追加するとします。 このセクションでは、jQuery UI を使用して、新しいカテゴリを追加するために使用できるダイアログボックスを追加します。 次の図は、UI がブラウザーにどのように表示されるかを示しています。

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image1.png)

ユーザーが **[新しいジャンルの追加]** リンクを選択すると、ポップアップダイアログボックスが表示され、ユーザーは新しいジャンル名 (および必要に応じて説明) を入力するように求められます。 次の画像は、 **[ジャンルの追加]** ポップアップダイアログを示しています。

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image2.png)

新しいジャンル名を入力して **[保存]** ボタンを押すと、次のような結果になります。

1. AJAX 呼び出しでは、Genre コントローラーの Create メソッドにデータがポストされます。これにより、新しいジャンルがデータベースに保存され、新しいジャンル情報 (ジャンル名と ID) が JSON として返されます。
2. JavaScript は、新しいジャンルデータを選択リストに追加します。
3. JavaScript は、選択された項目を新しいジャンルにします。

   次の図では、 **Opera**がデータベースに追加され、 **[ジャンル]** ドロップダウンリストで選択されています。 

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image3.png)

*Views\StoreManager\Create.cshtml*ファイルを開き、genre マークアップを次のコードに置き換えます。

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample1.cshtml)]

`_ChooseGenre` 部分ビューには、新しいジャンルの追加機能を実装するために使用される JavaScript と jQuery をフックするためのすべてのロジックが含まれます。 コードを完成させると、アーティスト UI でも同じことが簡単になります。

ソリューションエクスプローラーで、 *Views\StoreManager*フォルダーを右クリックし、 **[追加]** 、 **[表示]** の順に選択します。 **[ビュー名]** の入力 ボックスに「`_ChooseGenre`」と入力し、 **[追加]** を選択します。 *Views\StoreManager\\_ChooseGenre*ファイル内のマークアップを次のように置き換えます。

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample2.cshtml)]

最初の行では、`Album` をモデルとして渡していることを宣言しています。これは、Create view にあるモデルステートメントとまったく同じです。 次の数行は、**ラベル**ヘルパーマークアップです。 次の行は、元の Create view とまったく同じように、 **DropDownList**ヘルパー呼び出しです。 次の行では、`Add New Genre`という名前のリンクを追加し、ボタンのようにスタイルを指定します。 `ValidationMessageFor` を含む行は、Create ビューから直接コピーされます。 次の行を実行します。

[!code-html[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample3.html)]

`genreDialog`の ID を使用して、非表示の div を作成します。 JQuery を使用して、 **[ジャンルの追加]** ダイアログボックスをこの div の `genreDialog` ID と共にフックします。 最後の2つのスクリプトタグには、新しいジャンルの追加機能を実装するために使用する JavaScript ファイルへのリンクが含まれています。 この*ファイルは、プロジェクト*で提供されています。これについては、チュートリアルの後半で説明します。

アプリケーションを実行し、 **[新しいジャンルの追加]** ボタンをクリックします。 **[ジャンルの追加]** ダイアログボックスで、 **[名前]** 入力ボックスに「 **Opera** 」と入力します。

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image4.png)

**[保存]** ボタンをクリックします。 AJAX 呼び出しによって Opera カテゴリが作成され、ドロップダウンリストに Opera が挿入され、選択したジャンルとして Opera が設定されます。

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image5.png)

アーティスト、タイトル、価格を入力し、 **[作成]** ボタンを選択します。 $8.99 未満の価格を入力すると、新しいアルバムがインデックスビューの上部に表示されます。 新しいアルバムエントリがデータベースに保存されたことを確認します。

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image6.png)

1文字だけで新しいジャンルを作成してみてください。 次のコードでは、 *modelall Genre.cs*ファイルのジャンル名の最小値と最大長を設定しています。

[!code-csharp[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample4.cs)]

クライアント側の検証レポート 2 ~ 20 文字の文字列を入力する必要があります。

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image7.png)

### <a name="examining-how-a-new-genre-is-added-to-the-database-and-the-select-list"></a>新しいジャンルがデータベースと選択リストに追加された方法を確認しています。

*スクリプト*ファイルを開き、コードを確認します。

[!code-javascript[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample5.js)]

2行目では、ID `genreDialog` を使用して、 *Views\StoreManager\\_ChooseGenre*ファイルの div タグにダイアログボックスを作成します。 名前付きパラメーターのほとんどは、わかりやすいものです。 `autoOpen` パラメーターが false に設定されている場合は、 **[ジャンルの作成]** ボタンを選択すると、ダイアログが明示的に開きます (これについては後述します)。 ダイアログには、 **[保存]** と **[キャンセル**] の2つのボタンがあります。 **[キャンセル**] ボタンをクリックすると、ダイアログボックスが閉じます。 次のコードは、 **[保存]** ボタンの関数を示しています。

[!code-javascript[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample6.js)]

`var createGenreForm` が `createGenreForm` ID から選択されます。 `createGenreForm` ID は、 *Views\Genre\\_CreateGenre*ファイルにある次のコードで設定されています。

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample7.cshtml)]

*Views\Genre\\_CreateGenre*ファイルで使用される[Html. beginform](https://msdn.microsoft.com/library/dd492714.aspx)ヘルパーオーバーロードでは、フォームを送信するための URL を含む ACTION 属性を持つ html が生成されます。 これを確認するには、ブラウザーで [アルバムの作成] ページを表示し、ブラウザーで [ソースの表示] を選択します。 次のマークアップは、フォームタグを含む生成された HTML を示しています。

[!code-html[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample8.html)]

JQuery `$.post` 行は、アクション属性 (`/StoreManager/Create`) に対して AJAX 呼び出しを行い、 **[ジャンルの作成]** ダイアログボックスからデータを渡します。 データは、新しいジャンルの名前とオプションの説明で構成されます。 AJAX 呼び出しが成功すると、新しいジャンルの名前と値が選択マークアップに追加され、新しいジャンルは選択された値に設定されます。 これは動的に生成されたマークアップであるため、ブラウザーでソースを表示して新しい select オプションを表示することはできません。 新しい HTML は IE 9 の F12 開発者ツールで確認できます。 新しい select オプションを表示するには、Internet Explorer 9 で F12 キーを押して、F12 開発者ツールを起動します。 [作成] ページに移動し、新しいジャンルを追加して、ジャンルの選択リストで新しいジャンルを選択します。 F12 開発者ツールで、次のようにします。

1. [HTML] タブを選択します。
2. 更新アイコンをクリックします。  
    ![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image8.png)
3. 検索ボックスに、「GenreID」と入力します。
4. 次のアイコンを使用します。   
    ![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image9.png)  
   次の select タグに移動します。

    [!code-html[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample9.html)]
5. 最後のオプションの値を展開します。

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image10.png)

次のコードは、*スクリプト*ファイル内の次のコードで、 **[新しいジャンルの追加]** ボタンをクリックイベントに接続する方法と、 **[新しいジャンルの追加]** ダイアログボックスを作成する方法を示しています。

[!code-javascript[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample10.js)]

最初の行では、 **[新しいジャンルの追加]** ボタンに関連付けられている click 関数が作成されます。 Views\StoreManager\\_ChooseGenre の次のマークアップは、 **[新しいジャンルの追加]** ボタンが作成される方法を示しています。

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample11.cshtml)]

Load メソッドは、[ジャンルの追加] ダイアログボックスを作成して開き、ダイアログに入力されたデータに対してクライアント検証が行われるように、jQuery `parse` メソッドを呼び出します。

このセクションでは、選択リストに新しいカテゴリデータを追加するために使用できるダイアログを作成する方法について説明しました。 同じ手順に従って、アーティストの選択リストに新しいアーティストを追加するための UI を作成できます。 このチュートリアルでは、ASP.NET MVC HTML ヘルパーの**DropDownList**の使用方法の概要を説明しました。 **DropDownList**の使用方法の詳細については、以下の「追加の参照」セクションを参照してください。 このチュートリアルが役に立つかどうかをお知らせください。

Rick Anderson [at] Microsoft .com

### <a name="additional-references"></a>その他のリファレンス

- [ASP.NET MVC –カスケードドロップダウンリストのチュートリアル (](https://weblogs.asp.net/raduenuca/archive/2011/03/06/asp-net-mvc-cascading-dropdown-lists-tutorial-part-1-defining-the-problem-and-the-context.aspx)エンコード[u enuca](https://weblogs.asp.net/raduenuca/default.aspx)別)
- [選択](https://harvesthq.github.com/chosen/)複数選択とフィルター処理をサポートする JavaScript プラグイン。

### <a name="contributors"></a>共同作成者

- [レーダー](https://weblogs.asp.net/raduenuca/default.aspx)
- Jean-Sébastien Goupil
- [Brad Wilson](http://bradwilson.typepad.com/)

### <a name="reviewers"></a>レビュー担当者

- Jean-Sébastien Goupil
- [Brad Wilson](http://bradwilson.typepad.com/)
- Mike Pope
- Tom Dykstra

> [!div class="step-by-step"]
> [[戻る]](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper.md)
