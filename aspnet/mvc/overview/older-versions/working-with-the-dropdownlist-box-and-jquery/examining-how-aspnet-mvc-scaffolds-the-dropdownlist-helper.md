---
uid: mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper
title: ASP.NET MVC スキャフォールディング DropDownList ヘルパー | を調べるMicrosoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/12/2012
ms.assetid: 8921d7f2-21f0-427a-8b27-2df7251174b0
msc.legacyurl: /mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper
msc.type: authoredcontent
ms.openlocfilehash: 275b20ad964b3e8ddc272a7448f0740ed0891eff
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457610"
---
# <a name="examining--how--aspnet-mvc-scaffolds-the-dropdownlist-helper"></a>ASP.NET MVC で DropDownList ヘルパーをスキャフォールディングするしくみを確認する

[Rick Anderson](https://twitter.com/RickAndMSFT)

**ソリューションエクスプローラー**で、[*コントローラー* ] フォルダーを右クリックし、 **[コントローラーの追加]** を選択します。 コントローラーに**StoreManagerController**という名前を指定します。 次の図に示すように、 **[コントローラーの追加]** ダイアログのオプションを設定します。

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image1.png)

*StoreManager\Index.cshtml*ビューを編集し、`AlbumArtUrl`を削除します。 `AlbumArtUrl` を削除すると、プレゼンテーションが読みやすくなります。 完成したコードを以下に示します。

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample1.cshtml)]

*Controllers\StoreManagerController.cs*ファイルを開き、`Index` メソッドを見つけます。 アルバムが価格で並べ替えられるように、`OrderBy` 句を追加します。 完全なコードを次に示します。

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample2.cs)]

価格で並べ替えを行うと、データベースへの変更をテストしやすくなります。 Edit メソッドと create メソッドをテストする際には、保存したデータが最初に表示されるように低価格を使用できます。

*StoreManager\Edit.cshtml*ファイルを開きます。 凡例タグの直後に次の行を追加します。

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample3.cshtml)]

次のコードは、この変更のコンテキストを示しています。

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample4.cshtml)]

アルバムレコードに変更を加えるには、`AlbumId` が必要です。

Ctrl キーを押しながら F5 キーを押してアプリケーションを実行します。 **[管理者]** リンクを選択し、 **[新規作成]** リンクを選択して新しいアルバムを作成します。 アルバム情報が保存されたことを確認します。 アルバムを編集し、加えた変更が保存されていることを確認します。

### <a name="the-album-schema"></a>アルバムスキーマ

MVC スキャフォールディングメカニズムによって作成された `StoreManager` コントローラーは、music (作成、読み取り、更新、削除) ミュージックストアデータベース内のアルバムへのアクセスを許可します。 アルバム情報のスキーマは次のようになります。

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image2.png)

`Albums` テーブルには、アルバムのジャンルと説明が格納されていません。 `Genres` テーブルに外部キーが格納されます。 `Genres` テーブルには、ジャンルの名前と説明が含まれています。 同様に、`Albums` テーブルにはアルバムアーティスト名は含まれていませんが、`Artists` テーブルの外部キーは含まれていません。 `Artists` テーブルには、アーティストの名前が含まれています。 `Albums` テーブルのデータを調べると、`Genres` テーブルへの外部キーと `Artists` テーブルへの外部キーが各行に含まれていることを確認できます。 次の図は、`Albums` テーブルのテーブルデータを示しています。

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image3.png)

### <a name="the-html-select-tag"></a>HTML の Select タグ

Html `<select>` 要素 (HTML [DropDownList](https://msdn.microsoft.com/library/dd492948.aspx)ヘルパーによって作成されます) は、値の完全な一覧 (ジャンルの一覧など) を表示するために使用されます。 編集フォームの場合、現在の値がわかっている場合は、選択リストに現在の値が表示されます。 これは、選択した値を**コメディ**に設定したときに以前に見たことがあります。 選択リストは、カテゴリまたは外部キーのデータを表示するのに最適です。 Genre 外部キーの `<select>` 要素には、使用可能なジャンル名の一覧が表示されますが、フォームを保存すると、ジャンルプロパティは、表示されているジャンル名ではなく、ジャンルの外部キーの値で更新されます。 次の画像では、選択されたジャンルは**ディスコ**、アーティストは**Donna 夏**です。

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image4.png)

### <a name="examining-the-aspnet-mvc-scaffolded-code"></a>ASP.NET MVC スキャフォールディングコードの検証

*Controllers\StoreManagerController.cs*ファイルを開き、`HTTP GET Create` メソッドを見つけます。

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample5.cs)]

`Create` メソッドは、2つの[Selectlist](https://msdn.microsoft.com/library/system.web.mvc.selectlist.aspx)オブジェクトを `ViewBag`に追加します。1つはジャンル情報を格納するオブジェクト、もう1つはアーティスト情報を格納するオブジェクトです。 上で使用される[Selectlist](https://msdn.microsoft.com/library/dd505286.aspx)コンストラクターのオーバーロードには、次の3つの引数が必要です。

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample6.cs)]

1. *items*: リスト内の項目を含む[IEnumerable](https://msdn.microsoft.com/library/system.collections.ienumerable.aspx) 。 上記の例では、`db.Genres`によって返されるジャンルの一覧を示します。
2. *dataValueField*: キー値を含む**IEnumerable**リスト内のプロパティの名前。 上記の例では、を `GenreId` し、`ArtistId`します。
3. *Datatextfield*: 表示する情報が格納されている**IEnumerable**リスト内のプロパティの名前。 アーティストと genre テーブルの両方で、[`name`] フィールドが使用されます。

*Views\StoreManager\Create.cshtml*ファイルを開き、[ジャンル] フィールドの `Html.DropDownList` ヘルパーマークアップを確認します。

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample7.cshtml)]

最初の行は、create ビューが `Album` モデルを取得することを示しています。 上に示した `Create` メソッドでは、モデルが渡されなかったため、ビューは**null** `Album` モデルを取得します。 この時点では、新しいアルバムを作成しています。そのため、`Album` データがありません。

上に示した[Html の DropDownList](https://msdn.microsoft.com/library/dd492948.aspx)オーバーロードは、モデルにバインドするフィールドの名前を受け取ります。 また、この名前を使用して、 [Selectlist](https://msdn.microsoft.com/library/dd505286.aspx)オブジェクトを含む**ViewBag**オブジェクトを検索します。 このオーバーロードを使用して、 **ViewBag SelectList**オブジェクトに `GenreId`という名前を指定する必要があります。 2番目のパラメーター (`String.Empty`) は、項目が選択されていない場合に表示されるテキストです。 これは、新しいアルバムを作成するときに必要なことです。 2番目のパラメーターを削除し、次のコードを使用するとします。

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample8.cshtml)]

選択リストは、既定では最初の要素、またはサンプルのロックになります。

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image5.png)

`HTTP POST Create` メソッドを調べています。

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample9.cs)]

`Create` メソッドのこのオーバーロードは、ASP.NET MVC モデルバインドシステムによって作成された `album` のオブジェクトを、ポストされたフォーム値から受け取ります。 新しいアルバムを送信するときに、モデルの状態が有効で、データベースエラーがない場合は、新しいアルバムにデータベースが追加されます。 次の図は、新しいアルバムの作成を示しています。

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image6.png)

[Fiddler ツール](http://www.fiddler2.com/fiddler2/)を使用すると、ASP.NET MVC モデルバインドがアルバムオブジェクトの作成に使用する、ポストされたフォームの値を調べることができます。

[https://login.microsoftonline.com/consumers/](![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image7.png))

### <a name="refactoring-the-viewbag-selectlist-creation"></a>ViewBag SelectList 作成のリファクタリング

`Edit` メソッドと `HTTP POST Create` メソッドの両方に同じコードがあるため、 **ViewBag**で**selectlist**を設定できます。 [ドライ](http://en.wikipedia.org/wiki/Don't_repeat_yourself)の精神で、このコードをリファクターします。 このリファクタリングされたコードは後で使用します。

新しいメソッドを作成して、ジャンルとアーティストの**Selectlist**を**ViewBag**に追加します。

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample10.cs)]

`Create` と `Edit` の各メソッドの `ViewBag` を設定する2つの行を、`SetGenreArtistViewBag` メソッドの呼び出しに置き換えます。 完成したコードを以下に示します。

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample11.cs)]

新しいアルバムを作成し、アルバムを編集して、変更が有効であることを確認します。

### <a name="explicitly-passing-the-selectlist-to-the-dropdownlist"></a>SelectList を明示的に DropDownList に渡す

ASP.NET MVC スキャフォールディングによって作成される create ビューと edit ビューでは、次の**DropDownList**オーバーロードを使用します。

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample12.cs)]

Create ビューの `DropDownList` マークアップを次に示します。

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample13.cshtml)]

`SelectList` の `ViewBag` プロパティの名前は `GenreId`であるため、 **DropDownList**ヘルパーは**ViewBag**の `GenreId`**selectlist**を使用します。 次の**DropDownList**オーバーロードでは、`SelectList` が明示的に渡されます。

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample14.cs)]

*Views\StoreManager\Edit.cshtml*ファイルを開き、 **DropDownList**呼び出しを変更して、上記のオーバーロードを使用して**selectlist**を明示的に渡します。 ジャンルカテゴリに対してこれを行います。 完成したコードを次に示します。

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample15.cshtml)]

アプリケーションを実行し、 **[管理者]** リンクをクリックします。次に、ジャズアルバムに移動し、 **[編集]** リンクを選択します。

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image8.png)

現在選択されているジャンルとしてジャズを表示するのではなく、ロックが表示されます。 文字列引数 (バインドするプロパティ) と**Selectlist**オブジェクトの名前が同じ場合、選択した値は使用されません。 選択された値が指定されていない場合、ブラウザーは既定で**Selectlist**の最初の要素 (上記の例では**ロック**) を使用します。 これは、 **DropDownList**ヘルパーの既知の制限です。

*Controllers\StoreManagerController.cs*ファイルを開き、 **selectlist**オブジェクト名を `Genres` と `Artists`に変更します。 完成したコードを次に示します。

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample16.cs)]

ジャンルとアーティストの名前は、各カテゴリの ID だけではなく、カテゴリに適した名前になります。 以前に行ったリファクタリングはオフになっていました。 **ViewBag**を4つの方法で変更するのではなく、変更が `SetGenreArtistViewBag` メソッドに分離されました。

Create ビューと edit ビューで**DropDownList**呼び出しを変更して、新しい**selectlist**名を使用します。 次に、編集ビューの新しいマークアップを示します。

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample17.cshtml)]

Create view では、SelectList 内の最初の項目が表示されないように、空の文字列が必要です。

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample18.cshtml)]

新しいアルバムを作成し、アルバムを編集して、変更が有効であることを確認します。 [ロック] 以外のジャンルのアルバムを選択して、編集コードをテストします。

### <a name="using-a-view-model-with-the-dropdownlist-helper"></a>DropDownList ヘルパーでのビューモデルの使用

`AlbumSelectListViewModel`という名前の Viewmodel フォルダーに新しいクラスを作成します。 `AlbumSelectListViewModel` クラスのコードを次のコードに置き換えます。

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample19.cs)]

`AlbumSelectListViewModel` コンストラクターは、アルバム、アーティスト、ジャンルのリストを受け取り、アルバムを含むオブジェクトと、ジャンルとアーティストの `SelectList` を作成します。

次の手順でビューを作成するときに `AlbumSelectListViewModel` を使用できるように、プロジェクトをビルドします。

`StoreManagerController`に `EditVM` メソッドを追加します。 完成したコードを以下に示します。

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample20.cs)]

`AlbumSelectListViewModel`右クリックして **[解決]** を選択し、次に**MvcMusicStore viewmodel; を使用**します。

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image9.png)

または、次の using ステートメントを追加することもできます。

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample21.cs)]

`EditVM` 右クリックし、 **[ビューの追加]** を選択します。 次に示すオプションを使用します。

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image10.png)

**[追加]** を選択し、 *Views\StoreManager\EditVM.cshtml*ファイルの内容を次の内容に置き換えます。

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample22.cshtml)]

`EditVM` マークアップは、次の例外を除き、元の `Edit` マークアップとよく似ています。

- `Edit` ビューのモデルのプロパティは `model.property`フォーム (`model.Title` など) です。 `EditVm` ビューのモデルのプロパティは `model.Album.property`フォーム (`model.Album.Title`など) です。 これは、`EditVM` ビューには、`Edit` ビューのような `Album` ではなく、`Album`のコンテナーが渡されるためです。
- **DropDownList**の2番目のパラメーターは、 **ViewBag**ではなく、ビューモデルから取得されます。
- `EditVM` ビューの**Beginform**ヘルパーは、`Edit` アクションメソッドに明示的にポストバックします。 `Edit` アクションにポストバックすることで、`HTTP POST EditVM` アクションを記述する必要がなくなり、`HTTP POST` の `Edit` アクションを再利用できます。

アプリケーションを実行し、アルバムを編集します。 `EditVM`を使用するように URL を変更します。 フィールドを変更し、 **[保存]** ボタンをクリックして、コードが動作していることを確認します。

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image11.png)

### <a name="which-approach-should-you-use"></a>どの方法を使用する必要がありますか。

表示される3つの方法はすべて許容されます。 多くの開発者は、`ViewBag`を使用して、`SelectList` を `DropDownList` に明示的に渡すことを好みます。 このアプローチには、より適切な名前をコレクションに使用する柔軟性を提供するという利点があります。 注意点として、`ViewBag SelectList` オブジェクトにモデルプロパティと同じ名前を指定することはできません。

一部の開発者は、ビューモデルのアプローチを好む場合があります。 他のユーザーは、より詳細なマークアップと生成されたモデルビューの手法を考慮して、欠点を検討します。

このセクションでは、 **DropDownList**とカテゴリデータを使用する3つの方法を学習しました。 次のセクションでは、新しいカテゴリを追加する方法について説明します。

> [!div class="step-by-step"]
> [前へ](using-the-dropdownlist-helper-with-aspnet-mvc.md)
> [次へ](adding-a-new-category-to-the-dropdownlist-using-jquery-ui.md)
