---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/deleting-data
title: ASP.NET Web ページの概要-データベースデータの削除 |Microsoft Docs
author: Rick-Anderson
description: このチュートリアルでは、個々のデータベースエントリを削除する方法について説明します。 この記事では、ASP.NET Web Pa でデータベースデータを更新して、シリーズを完了していることを前提としています。
ms.author: riande
ms.date: 01/02/2018
ms.assetid: 75b5c1cf-84bd-434f-8a86-85c568eb5b09
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/deleting-data
msc.type: authoredcontent
ms.openlocfilehash: c8620fc1abc61d514bdc039c66f7a84e67e89abe
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78510460"
---
# <a name="introducing-aspnet-web-pages---deleting-database-data"></a>ASP.NET Web ページの概要-データベースデータの削除

[Tom FitzMacken](https://github.com/tfitzmac)

> このチュートリアルでは、個々のデータベースエントリを削除する方法について説明します。 [ASP.NET Web ページでデータベースデータを更新](updating-data.md)することによってシリーズを完了していることを前提としています。
> 
> ここでは、次の内容について学習します。
> 
> - レコードの一覧から個々のレコードを選択する方法。
> - データベースから1つのレコードを削除する方法。
> - フォームで特定のボタンがクリックされたことを確認する方法。
>   
> 
> 説明する機能/テクノロジ:
> 
> - `WebGrid` ヘルパー。
> - SQL `Delete` コマンド。
> - SQL `Delete` コマンドを実行する `Database.Execute` メソッド。

## <a name="what-youll-build"></a>作成するアプリケーション:

前のチュートリアルでは、既存のデータベースレコードを更新する方法について学習しました。 このチュートリアルは似ていますが、レコードを更新するのではなく、レコードを削除する点が異なります。 プロセスはほぼ同じですが、削除の方が簡単であるため、このチュートリアルは短くなります。

[*ムービー* ] ページで `WebGrid` ヘルパーを更新して、前に追加した**編集**リンクに付随する各ムービーの横に **[削除]** リンクが表示されるようにします。

![各ムービーの [削除] リンクを示すムービーページ](deleting-data/_static/image1.png)

編集と同様に、 **[削除]** リンクをクリックすると、別のページに移動します。このページでは、ムービー情報が既にフォームに含まれています。

![ムービーが表示されているムービーページを削除する](deleting-data/_static/image2.png)

このボタンをクリックすると、レコードが完全に削除されます。

## <a name="adding-a-delete-link-to-the-movie-listing"></a>ムービーの一覧への削除リンクの追加

まず、`WebGrid` ヘルパーに**Delete**リンクを追加します。 このリンクは、前のチュートリアルで追加した**編集**リンクに似ています。

ムービーの*cshtml*ファイルを開きます。

列を追加して、ページの本文の `WebGrid` マークアップを変更します。 変更されたマークアップを次に示します。

[!code-html[Main](deleting-data/samples/sample1.html?highlight=9-10)]

新しい列は次のようになります。

[!code-html[Main](deleting-data/samples/sample2.html)]

グリッドの構成方法では、 **[編集]** 列がグリッドの一番左にあり、 **[削除]** 列が右端になります。 (これに気付いていない場合は、`Year` 列の後にコンマがあります)。これらのリンク列がどこに配置されているかについて特別なことはありません。また、互いに簡単に配置することもできます。 このケースでは、これらは混同されることがないように分離されています。

![[編集] リンクと [詳細] リンクが横に表示されていないことを示すムービーページ](deleting-data/_static/image3.png)

新しい列には、"Delete" というテキストを含むリンク (`<a>` 要素) が表示されます。 リンクのターゲット (`href` 属性) は、次の URL のように最終的に解決されるコードです。ムービーごとに `id` 値は異なります。

[!code-css[Main](deleting-data/samples/sample3.css)]

このリンクを選択すると、 *DeleteMovie*という名前のページが呼び出され、選択したムービーの ID が渡されます。

このチュートリアルでは、このリンクの構築方法について詳しく説明しません。これは、前のチュートリアルの**編集**リンク ([ASP.NET Web ページでのデータベースデータの更新](updating-data.md)) とほぼ同じであるためです。

## <a name="creating-the-delete-page"></a>[削除] ページの作成

これで、グリッド内の **[削除]** リンクのターゲットとなるページを作成できるようになりました。

> [!NOTE] 
> 
> **重要**最初に削除するレコードを選択し、別のページとボタンを使用してプロセスを確認する方法は、セキュリティ上重要です。 前のチュートリアルで読んだように、web サイトに*何らか*の変更を加える場合は、*常*に HTTP POST 操作を使用して &mdash; フォームを使用して行う必要があります。 リンクをクリックして (つまり、GET 操作を使用して) サイトを変更できるようにした場合、ユーザーはサイトに単純な要求を行い、データを削除することができます。 サイトにインデックスを作成している検索エンジンのクローラーでも、次のリンクによってデータが誤って削除される可能性があります。
> 
> アプリでレコードを変更できるようにするには、編集のためにレコードをユーザーに提示する必要があります。 ただし、レコードを削除する場合は、この手順をスキップすることがあります。 ただし、この手順は省略しないでください。 (これは、ユーザーがレコードを確認し、意図したレコードを削除していることを確認する場合にも役立ちます)。
> 
> 以降のチュートリアルでは、ユーザーがレコードを削除する前にログインしなければならないように、ログイン機能を追加する方法を説明します。

*DeleteMovie*という名前のページを作成し、ファイルの内容を次のマークアップに置き換えます。

[!code-cshtml[Main](deleting-data/samples/sample4.cshtml)]

このマークアップは、 *Editmovie*ページに似ていますが、テキストボックス (`<input type="text">`) を使用するのではなく、マークアップに `<span>` の要素が含まれている点が異なります。 編集するものはありません。 必要なのは、ムービーの詳細を表示して、ユーザーが適切なムービーを削除していることを確認できるようにすることだけです。

マークアップには、ユーザーがムービー一覧ページに戻るためのリンクが既に含まれています。

[ *Editmovie* ] ページと同様に、選択したムービーの ID が隠しフィールドに格納されます。 (クエリ文字列値として最初の場所にページが渡されます)。検証エラーを表示する `Html.ValidationSummary` の呼び出しがあります。 この場合、エラーは、ムービー ID がページに渡されなかったか、ムービー ID が無効である可能性があります。 この状況は、*最初にムービーページで*ムービーを選択せずにこのページを実行した場合に発生する可能性があります。

ボタンのキャプションは **[ムービーの削除]** で、name 属性は `buttonDelete`に設定されています。 `name` 属性は、フォームを送信したボタンを識別するためにコード内で使用されます。

コードを1に記述する必要があります)。ページが最初に表示されたときにムービーの詳細を確認し、2) ユーザーがボタンをクリックしたときにムービーを実際に削除します。

## <a name="adding-code-to-read-a-single-movie"></a>1つのムービーを読み取るコードを追加する

*DeleteMovie*ページの上部に、次のコードブロックを追加します。

[!code-cshtml[Main](deleting-data/samples/sample5.cshtml)]

このマークアップは、 *Editmovie*ページの対応するコードと同じです。 クエリ文字列からムービー ID を取得し、ID を使用してデータベースからレコードを読み取ります。 このコードには、ページに渡されるムービー ID が有効であることを確認するための検証テスト (`IsInt()` と `row != null`) が含まれています。

このコードは、ページを初めて実行するときにのみ実行する必要があることに注意してください。 ユーザーが **[ムービーの削除]** ボタンをクリックしたときに、データベースからムービーレコードを再度読み取る必要はありません。 そのため、ムービーを読み取るコードは、*要求が post 操作 (フォーム送信) でない場合*は、`if(!IsPost)` &mdash; というテスト内にあります。

## <a name="adding-code-to-delete-the-selected-movie"></a>選択したムービーを削除するコードの追加

ユーザーがボタンをクリックしたときにムービーを削除するには、`@` ブロックの右中かっこの内側に次のコードを追加します。

[!code-csharp[Main](deleting-data/samples/sample6.cs)]

このコードは、既存のレコードを更新するためのコードに似ていますが、単純です。 このコードは、基本的に SQL `Delete` ステートメントを実行します。

 *Editmovie*ページと同様に、コードは `if(IsPost)` ブロックにあります。 今回は、`if()` 条件は少し複雑になります。 

[!code-csharp[Main](deleting-data/samples/sample7.cs)]

ここでは2つの条件があります。 1つ目は、`if(IsPost)`&mdash; 前に示したように、ページが送信されていることです。

2番目の条件は `!Request["buttonDelete"].IsEmpty()`であり、要求に `buttonDelete`という名前のオブジェクトが含まれていることを意味します。 確かに、フォームを送信したボタンをテストするための間接的な方法です。 フォームに複数の [送信] ボタンが含まれている場合は、クリックされたボタンの名前だけが要求に表示されます。 したがって、論理的には、特定のボタンの名前が要求 &mdash; に表示される場合、またはコードに示されているように表示される場合、そのボタンが空でない場合は、フォームを送信したボタン &mdash; ます。

`&&` 演算子は、"and" (論理 AND) を意味します。 したがって、`if` 条件全体は...

*この要求は post (初回要求ではありません) です*  
  
 AND  
  
*`buttonDelete`ボタンは、* *フォームを送信したボタンでした。*

このフォーム (実際にはこのページ) には1つのボタンしか含まれていないため、`buttonDelete` に対する追加のテストは技術的には必要ありません。 それでも、データを完全に削除する操作を実行しようとしています。 そのため、ユーザーが明示的に要求した場合にのみ操作を実行するようにします。 たとえば、このページを後で展開し、その他のボタンを追加したとします。 それでも、ムービーを削除するコードは、[`buttonDelete`] ボタンがクリックされた場合にのみ実行されます。

[ *Editmovie* ] ページと同様に、非表示フィールドから ID を取得し、SQL コマンドを実行します。 `Delete` ステートメントの構文は次のとおりです。

`DELETE FROM table WHERE ID = value`

`WHERE` 句と ID を含めることが重要です。 WHERE 句を省略すると、*テーブル内のすべてのレコードが削除され*ます。 ご覧のとおり、プレースホルダーを使用して、SQL コマンドに ID 値を渡します。

## <a name="testing-the-movie-delete-process"></a>ムービーの削除プロセスのテスト

これで、をテストできるようになりました。 ムービーページを実行し、ムービーの横*にある [* **削除**] をクリックします。 [ *DeleteMovie* ] ページが表示されたら、 **[ムービーの削除]** をクリックします。

![[ムービーの削除] ボタンが強調表示されているムービーページを削除する](deleting-data/_static/image4.png)

このボタンをクリックすると、ムービーが削除され、ムービーの一覧に戻ります。 削除したムービーを検索し、削除されたことを確認できます。

## <a name="coming-up-next"></a>次へ

次のチュートリアルでは、サイトのすべてのページに共通の外観とレイアウトを提供する方法について説明します。

## <a name="complete-listing-for-movie-page-updated-with-delete-links"></a>[ムービーの完全な一覧表示] ページ ([リンクの削除] で更新)

[!code-cshtml[Main](deleting-data/samples/sample8.cshtml)]

## <a name="complete-listing-for-deletemovie-page"></a>DeleteMovie ページの完全な一覧表示

[!code-cshtml[Main](deleting-data/samples/sample9.cshtml)]

## <a name="additional-resources"></a>その他のリソース

- [Razor 構文を使用した ASP.NET Web プログラミングの概要](../introducing-razor-syntax-c.md)
- W3Schools サイトでの[SQL DELETE ステートメント](http://www.w3schools.com/sql/sql_delete.asp)

> [!div class="step-by-step"]
> [前へ](updating-data.md)
> [次へ](layouts.md)
