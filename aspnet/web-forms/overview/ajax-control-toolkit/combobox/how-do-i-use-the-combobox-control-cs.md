---
uid: web-forms/overview/ajax-control-toolkit/combobox/how-do-i-use-the-combobox-control-cs
title: ComboBox コントロールを使用操作方法には (C#) |Microsoft Docs
author: microsoft
description: ComboBox は、テキストボックスの柔軟性と、ユーザーが選択できるオプションの一覧を組み合わせた ASP.NET AJAX コントロールです。
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 0bbf4134-04df-4226-8930-d5bb99e27128
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/combobox/how-do-i-use-the-combobox-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 1c5fc61300441303b39e348d3eee83b6ee6847b4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78446542"
---
# <a name="how-do-i-use-the-combobox-control-c"></a>ComboBox コントロールを使用操作方法には (C#)

[Microsoft](https://github.com/microsoft)

> ComboBox は、テキストボックスの柔軟性と、ユーザーが選択できるオプションの一覧を組み合わせた ASP.NET AJAX コントロールです。

このチュートリアルの目的は、AJAX Control Toolkit ComboBox コントロールについて説明することです。 ComboBox は、標準の ASP.NET DropDownList コントロールと TextBox コントロールの組み合わせと同様に機能します。 既存の項目の一覧から選択するか、新しい項目を入力することができます。

ComboBox は AutoComplete コントロールエクステンダーに似ていますが、コントロールはさまざまなシナリオで使用されます。 オートコンプリートエクステンダーは、web サービスに対してクエリを行い、一致するエントリを取得します。 これに対し、ComboBox コントロールは、一連の項目で初期化されます。 オートコンプリートエクステンダーの使用は、大規模なデータセット (何百万もの車の部品) を使用しているときに、ComboBox コントロールを使用しているときに意味があります。これは、少数のデータ (多数の自動車部品) を使用する場合に適しています。

## <a name="selecting-from-a-static-list-of-items"></a>項目の静的なリストからの選択

まず、ComboBox コントロールを使用した簡単なサンプルを見てみましょう。 ドロップダウンリストに項目の静的なリストを表示する場合を考えてみましょう。 ただし、リストが完全ではない可能性を開いたままにしておく必要があります。 ユーザーがリストにカスタム値を入力できるようにする場合。

新しい ASP.NET Web フォームページを作成し、ページの ComboBox コントロールを使用します。 新しい ASP.NET ページをプロジェクトに追加し、デザインビューに切り替えます。

ページで ComboBox コントロールを使用する場合は、ScriptManager コントロールをページに追加する必要があります。 [AJAX 拡張] タブの下からデザイナー画面に ScriptManager コントロールをドラッグします。 ページの上部に ScriptManager コントロールを追加する必要があります。&gt; タグを開いているサーバー側 &lt;フォームのすぐ下に追加できます。

次に、ComboBox コントロールをページにドラッグします。 ツールボックスの ComboBox コントロールは、他の AJAX Control Toolkit コントロールとコントロールエクステンダーを使用して見つけることができます (「図1」を参照してください)。

[名刺を作成するためのシンプルなフォーム ![](how-do-i-use-the-combobox-control-cs/_static/image1.jpg)](how-do-i-use-the-combobox-control-cs/_static/image1.png)

**図 01**: ツールボックスから ComboBox コントロールを選択[する (クリックすると、フルサイズの画像が表示](how-do-i-use-the-combobox-control-cs/_static/image2.png)されます)

ComboBox コントロールを使用して、選択肢の静的リストを表示します。 ユーザーは、[軽度]、[中]、[ホット] の3つの選択肢の一覧から、食品の特定のレベルの spiciness を選択できます (図2を参照)。

[項目の静的なリストから選択 ![](how-do-i-use-the-combobox-control-cs/_static/image2.jpg)](how-do-i-use-the-combobox-control-cs/_static/image3.png)

**図 02**: 項目の静的なリストから選択[する (クリックすると、フルサイズの画像が表示](how-do-i-use-the-combobox-control-cs/_static/image4.png)される)

これらの選択肢を ComboBox コントロールに追加するには、次の2つの方法があります。 最初に、デザインビューのコントロールの上にマウスポインターを置いたときに [オプションの編集] タスクオプションを選択し、項目エディターを開きます (図3を参照)。

[ComboBox 項目の編集 ![](how-do-i-use-the-combobox-control-cs/_static/image3.jpg)](how-do-i-use-the-combobox-control-cs/_static/image5.png)

**図 03**: ComboBox 項目の編集 ([クリックしてフルサイズのイメージを表示する](how-do-i-use-the-combobox-control-cs/_static/image6.png))

2つ目の方法は、ソースビューの開始タグと終了 &lt;asp: ComboBox&gt; タグの間に項目の一覧を追加する方法です。 リスト1のページには、項目の一覧を含む更新されたコンボボックスが含まれています。

**リスト 1-Static .aspx**

[!code-aspx[Main](how-do-i-use-the-combobox-control-cs/samples/sample1.aspx)]

リスト1のページを開いたときに、コンボボックスから既存のオプションのいずれかを選択できます。 つまり、コンボボックスは DropDownList コントロールと同様に動作します。

ただし、既存のリストに含まれていない新しい選択肢 (たとえば、Super Spicy) を入力することもできます。 そのため、ComboBox は TextBox コントロールと同様に動作します。

既存の項目を選択するか、カスタム項目を入力するかにかかわらず、フォームを送信すると、ラベルコントロールに選択内容が表示されます。 フォームを送信すると、btnSubmit\_クリックハンドラーが実行され、ラベルが更新されます (図4を参照)。

[選択した項目を表示 ![](how-do-i-use-the-combobox-control-cs/_static/image4.jpg)](how-do-i-use-the-combobox-control-cs/_static/image7.png)

**図 04**: 選択した項目の表示 ([クリックすると、フルサイズの画像が表示](how-do-i-use-the-combobox-control-cs/_static/image8.png)されます)

コンボボックスでは、フォームの送信後に選択した項目を取得するための DropDownList コントロールと同じプロパティがサポートされています。

- SelectedItem-選択された項目の Text プロパティの値を表示します。
- SelectedItem-選択された項目の Value プロパティの値を表示するか、コンボボックスに入力されたテキストを表示します。
- SelectedValue-SelectedItem と同じですが、このプロパティでは、既定の (初期) 選択された項目を指定できます。

カスタムの選択項目をコンボボックスに入力すると、カスタムの選択項目が SelectedItem プロパティと SelectedItem プロパティの両方に割り当てられます。

## <a name="selecting-the-list-of-items-from-the-database"></a>データベースから項目の一覧を選択する

ComboBox によってデータベースから表示されるアイテムの一覧を取得できます。 たとえば、コンボボックスは、SqlDataSource コントロール、ObjectDataSource コントロール、LinqDataSource、または EntityDataSource にバインドできます。

たとえば、一連の映画をコンボボックスに表示したいとします。 ムービーデータベーステーブルからムービーの一覧を取得します。 次の手順に従います。

1. ムービー .aspx という名前のページを作成する
2. Scriptmanager コントロールをページに追加します。これを行うには、ツールボックスの [AJAX 拡張] タブで ScriptManager をページにドラッグします。
3. Combobox コントロールをページに追加します。このためには、コンボボックスをページにドラッグします。
4. デザインビューで、ComboBox コントロールの上にマウスポインターを置き、 **[データソースの選択]** タスクオプションを選択します (図5を参照)。 データソース構成ウィザードが起動されます。
5. **[データソースの選択]** ステップで、[新しいデータソースを &lt;&gt;] オプションを選択します。
6. **データソースの種類を選択** ステップで、データベース を選択します。
7. **[データ接続の選択]** ステップで、データベースを選択します (たとえば、MoviesDB)。
8. **[アプリケーション構成ファイルへの接続文字列の保存]** ステップで、接続文字列を保存するオプションを選択します。
9. **[Select ステートメントの構成]** ステップで、[ムービーデータベース] テーブルを選択し、すべての列を選択します。
10. **クエリのテスト** ステップで、完了 をクリックします。
11. **データソースの選択** ステップに戻り、表示するフィールドの タイトル 列と、データフィールドの Id 列を選択します (図を参照)。
12. [OK] ボタンをクリックして、ウィザードを閉じます。

[データソースの選択 ![](how-do-i-use-the-combobox-control-cs/_static/image5.jpg)](how-do-i-use-the-combobox-control-cs/_static/image9.png)

**図 05**: データソースを選択[する (クリックすると、フルサイズの画像が表示](how-do-i-use-the-combobox-control-cs/_static/image10.png)される)

[データテキストフィールドと値フィールドを選択 ![には](how-do-i-use-the-combobox-control-cs/_static/image6.jpg)](how-do-i-use-the-combobox-control-cs/_static/image11.png)

**図 06**: データテキストフィールドと値フィールドを選択[する (クリックすると、フルサイズの画像が表示](how-do-i-use-the-combobox-control-cs/_static/image12.png)されます)

上記の手順を完了すると、コンボボックスがムービーデータベーステーブルのムービーを表す SqlDataSource コントロールにバインドされます。 ページのソースは、リスト2のようになります (書式設定を少しずつクリーンアップしました)。

**リスト 2-default.aspx**

[!code-aspx[Main](how-do-i-use-the-combobox-control-cs/samples/sample2.aspx)]

ComboBox コントロールに、SqlDataSource コントロールを指す DataSourceID プロパティがあることに注意してください。 ブラウザーでページを開くと、データベースからのムービーの一覧が表示されます (図7を参照)。 リストからムービーを選択するか、コンボボックスにムービーを入力して新しいムービーを入力することができます。

[ムービーの一覧を表示 ![には](how-do-i-use-the-combobox-control-cs/_static/image7.jpg)](how-do-i-use-the-combobox-control-cs/_static/image13.png)

**図 07**: ムービーの一覧を表示[する (クリックすると、フルサイズの画像が表示](how-do-i-use-the-combobox-control-cs/_static/image14.png)される)

## <a name="setting-the-dropdownstyle"></a>DropDownStyle の設定

Combobox の DropDownStyle プロパティを使用して、コンボボックスの動作を変更できます。 このプロパティは、有効な値を受け入れます。

- ドロップダウン-(既定値) 矢印をクリックするとドロップダウンリストが表示され、カスタム値を入力できます。
- Simple-ComboBox にはドロップダウンリストが自動的に表示され、カスタム値を入力できます。
- DropDownList-コンボボックスは、DropDownList コントロールと同様に動作します。

ドロップダウンと単純の違いは、項目の一覧が表示されるときです。 Simple の場合、コンボボックスにフォーカスを移動するとすぐに一覧が表示されます。 ドロップダウンの場合は、矢印をクリックして項目の一覧を表示する必要があります。

DropDownList 値を指定すると、ComboBox コントロールは標準の DropDownList コントロールと同じように動作します。 ただし、ここでは重要な違いがあります。 以前のバージョンの Internet Explorer では、最前面に配置されているコントロールの前にコントロールが表示されるように、z インデックスが無制限の DropDownList コントロールが表示されます。 ComboBox では、html &lt;select&gt; タグではなく、HTML &lt;div&gt; タグがレンダリングされるため、ComboBox は z 順序を正しく反映します。

## <a name="setting-the-autocompletemode"></a>Autocompletemode.none の設定

Combobox にテキストを入力するとどうなるかを指定するには、ComboBox Autocompletemode.none プロパティを使用します。 このプロパティは、次の有効な値を受け入れます。

- None-(既定値) コンボボックスにオートコンプリートの動作が指定されていません。
- [提案]-コンボボックスに一覧が表示され、一覧内の一致する項目が強調表示されます (図8を参照)。
- Append-ComboBox はリストを表示せず、一致する項目をリストから入力したものに追加します (図9を参照)。
- SuggestAppend-ComboBox は、リストを表示し、一致する項目をリストから入力したものに追加します (図10を参照)。

[ComboBox が提案を ![](how-do-i-use-the-combobox-control-cs/_static/image8.jpg)](how-do-i-use-the-combobox-control-cs/_static/image15.png)

**図 08**: コンボボックスを使用して、提案を作成[する (クリックすると、フルサイズの画像が表示](how-do-i-use-the-combobox-control-cs/_static/image16.png)されます)

[![ComboBox は一致するテキストを追加します](how-do-i-use-the-combobox-control-cs/_static/image9.jpg)](how-do-i-use-the-combobox-control-cs/_static/image17.png)

**図 09**: ComboBox によって一致するテキストが追加される ([クリックすると、フルサイズの画像が表示](how-do-i-use-the-combobox-control-cs/_static/image18.png)される)

[ComboBox によって提案され、追加さ ![](how-do-i-use-the-combobox-control-cs/_static/image10.jpg)](how-do-i-use-the-combobox-control-cs/_static/image19.png)

**図 10**: コンボボックスが提案して追加[する (クリックすると、フルサイズの画像が表示](how-do-i-use-the-combobox-control-cs/_static/image20.png)されます)

## <a name="summary"></a>まとめ

このチュートリアルでは、ComboBox コントロールを使用して、固定された一連の項目を表示する方法について学習しました。 ComboBox コントロールは、項目の静的なセットとデータベーステーブルの両方にバインドされています。 最後に、DropDownStyle プロパティと Autocompletemode.none プロパティを設定して、ComboBox の動作を変更する方法を学習しました。

> [!div class="step-by-step"]
> [Next](how-do-i-use-the-combobox-control-vb.md)
