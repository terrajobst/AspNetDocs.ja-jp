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
# <a name="examining--how--aspnet-mvc-scaffolds-the-dropdownlist-helper"></a><span data-ttu-id="24145-102">ASP.NET MVC で DropDownList ヘルパーをスキャフォールディングするしくみを確認する</span><span class="sxs-lookup"><span data-stu-id="24145-102">Examining  how  ASP.NET MVC scaffolds the DropDownList Helper</span></span>

<span data-ttu-id="24145-103">[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="24145-103">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="24145-104">**ソリューションエクスプローラー**で、[*コントローラー* ] フォルダーを右クリックし、 **[コントローラーの追加]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="24145-104">In **Solution Explorer**, right-click the *Controllers* folder and then select **Add Controller**.</span></span> <span data-ttu-id="24145-105">コントローラーに**StoreManagerController**という名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="24145-105">Name the controller **StoreManagerController**.</span></span> <span data-ttu-id="24145-106">次の図に示すように、 **[コントローラーの追加]** ダイアログのオプションを設定します。</span><span class="sxs-lookup"><span data-stu-id="24145-106">Set the options for the **Add Controller** dialog as shown in the image below.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image1.png)

<span data-ttu-id="24145-107">*StoreManager\Index.cshtml*ビューを編集し、`AlbumArtUrl`を削除します。</span><span class="sxs-lookup"><span data-stu-id="24145-107">Edit the *StoreManager\Index.cshtml* view and remove `AlbumArtUrl`.</span></span> <span data-ttu-id="24145-108">`AlbumArtUrl` を削除すると、プレゼンテーションが読みやすくなります。</span><span class="sxs-lookup"><span data-stu-id="24145-108">Removing `AlbumArtUrl` will make the presentation more readable.</span></span> <span data-ttu-id="24145-109">完成したコードを以下に示します。</span><span class="sxs-lookup"><span data-stu-id="24145-109">The completed code is shown below.</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample1.cshtml)]

<span data-ttu-id="24145-110">*Controllers\StoreManagerController.cs*ファイルを開き、`Index` メソッドを見つけます。</span><span class="sxs-lookup"><span data-stu-id="24145-110">Open the *Controllers\StoreManagerController.cs* file and find the `Index` method.</span></span> <span data-ttu-id="24145-111">アルバムが価格で並べ替えられるように、`OrderBy` 句を追加します。</span><span class="sxs-lookup"><span data-stu-id="24145-111">Add the `OrderBy` clause so the albums will be sorted by price.</span></span> <span data-ttu-id="24145-112">完全なコードを次に示します。</span><span class="sxs-lookup"><span data-stu-id="24145-112">The complete code is shown below.</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample2.cs)]

<span data-ttu-id="24145-113">価格で並べ替えを行うと、データベースへの変更をテストしやすくなります。</span><span class="sxs-lookup"><span data-stu-id="24145-113">Sorting by price will make it easier to test changes to the database.</span></span> <span data-ttu-id="24145-114">Edit メソッドと create メソッドをテストする際には、保存したデータが最初に表示されるように低価格を使用できます。</span><span class="sxs-lookup"><span data-stu-id="24145-114">When you are testing the edit and create methods, you can use a low price so the saved data will appear first.</span></span>

<span data-ttu-id="24145-115">*StoreManager\Edit.cshtml*ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="24145-115">Open the *StoreManager\Edit.cshtml* file.</span></span> <span data-ttu-id="24145-116">凡例タグの直後に次の行を追加します。</span><span class="sxs-lookup"><span data-stu-id="24145-116">Add the following line just after the legend tag.</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample3.cshtml)]

<span data-ttu-id="24145-117">次のコードは、この変更のコンテキストを示しています。</span><span class="sxs-lookup"><span data-stu-id="24145-117">The following code shows the context of this change:</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample4.cshtml)]

<span data-ttu-id="24145-118">アルバムレコードに変更を加えるには、`AlbumId` が必要です。</span><span class="sxs-lookup"><span data-stu-id="24145-118">The `AlbumId` is required to make changes to an album record.</span></span>

<span data-ttu-id="24145-119">Ctrl キーを押しながら F5 キーを押してアプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="24145-119">Press CTRL+F5 to run the application.</span></span> <span data-ttu-id="24145-120">**[管理者]** リンクを選択し、 **[新規作成]** リンクを選択して新しいアルバムを作成します。</span><span class="sxs-lookup"><span data-stu-id="24145-120">Select to the **Admin** link, then select the **Create New** link to create a new album.</span></span> <span data-ttu-id="24145-121">アルバム情報が保存されたことを確認します。</span><span class="sxs-lookup"><span data-stu-id="24145-121">Verify the album information was saved.</span></span> <span data-ttu-id="24145-122">アルバムを編集し、加えた変更が保存されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="24145-122">Edit an album and verify the changes you made are persisted.</span></span>

### <a name="the-album-schema"></a><span data-ttu-id="24145-123">アルバムスキーマ</span><span class="sxs-lookup"><span data-stu-id="24145-123">The Album Schema</span></span>

<span data-ttu-id="24145-124">MVC スキャフォールディングメカニズムによって作成された `StoreManager` コントローラーは、music (作成、読み取り、更新、削除) ミュージックストアデータベース内のアルバムへのアクセスを許可します。</span><span class="sxs-lookup"><span data-stu-id="24145-124">The `StoreManager` controller created by the MVC scaffolding mechanism allows CRUD (Create, Read, Update, Delete) access to the albums in the music store database.</span></span> <span data-ttu-id="24145-125">アルバム情報のスキーマは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="24145-125">The schema for album information is shown below:</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image2.png)

<span data-ttu-id="24145-126">`Albums` テーブルには、アルバムのジャンルと説明が格納されていません。 `Genres` テーブルに外部キーが格納されます。</span><span class="sxs-lookup"><span data-stu-id="24145-126">The `Albums` table does not store the album genre and description, it stores a foreign key to the `Genres` table.</span></span> <span data-ttu-id="24145-127">`Genres` テーブルには、ジャンルの名前と説明が含まれています。</span><span class="sxs-lookup"><span data-stu-id="24145-127">The `Genres` table contains the genre name and description.</span></span> <span data-ttu-id="24145-128">同様に、`Albums` テーブルにはアルバムアーティスト名は含まれていませんが、`Artists` テーブルの外部キーは含まれていません。</span><span class="sxs-lookup"><span data-stu-id="24145-128">Likewise, the `Albums` table doesn't contain the album artists name, but a foreign key to the `Artists` table.</span></span> <span data-ttu-id="24145-129">`Artists` テーブルには、アーティストの名前が含まれています。</span><span class="sxs-lookup"><span data-stu-id="24145-129">The `Artists` table contains the artist's name.</span></span> <span data-ttu-id="24145-130">`Albums` テーブルのデータを調べると、`Genres` テーブルへの外部キーと `Artists` テーブルへの外部キーが各行に含まれていることを確認できます。</span><span class="sxs-lookup"><span data-stu-id="24145-130">If you examine the data in the `Albums` table, you can see each row contains a foreign key to the `Genres` table and a foreign key to the `Artists` table.</span></span> <span data-ttu-id="24145-131">次の図は、`Albums` テーブルのテーブルデータを示しています。</span><span class="sxs-lookup"><span data-stu-id="24145-131">The image below show some table data from the `Albums` table.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image3.png)

### <a name="the-html-select-tag"></a><span data-ttu-id="24145-132">HTML の Select タグ</span><span class="sxs-lookup"><span data-stu-id="24145-132">The HTML Select Tag</span></span>

<span data-ttu-id="24145-133">Html `<select>` 要素 (HTML [DropDownList](https://msdn.microsoft.com/library/dd492948.aspx)ヘルパーによって作成されます) は、値の完全な一覧 (ジャンルの一覧など) を表示するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="24145-133">The HTML `<select>` element (created by the HTML [DropDownList](https://msdn.microsoft.com/library/dd492948.aspx) helper) is used to display a complete list of values (such as the list of genres).</span></span> <span data-ttu-id="24145-134">編集フォームの場合、現在の値がわかっている場合は、選択リストに現在の値が表示されます。</span><span class="sxs-lookup"><span data-stu-id="24145-134">For edit forms, when the current value is known, the select list can display the current value.</span></span> <span data-ttu-id="24145-135">これは、選択した値を**コメディ**に設定したときに以前に見たことがあります。</span><span class="sxs-lookup"><span data-stu-id="24145-135">We saw this previously when we set the selected value to **Comedy**.</span></span> <span data-ttu-id="24145-136">選択リストは、カテゴリまたは外部キーのデータを表示するのに最適です。</span><span class="sxs-lookup"><span data-stu-id="24145-136">The select list is ideal for displaying category or foreign key data.</span></span> <span data-ttu-id="24145-137">Genre 外部キーの `<select>` 要素には、使用可能なジャンル名の一覧が表示されますが、フォームを保存すると、ジャンルプロパティは、表示されているジャンル名ではなく、ジャンルの外部キーの値で更新されます。</span><span class="sxs-lookup"><span data-stu-id="24145-137">The `<select>` element for the Genre foreign key displays the list of possible genre names, but when you save the form the Genre property is updated with the Genre foreign key value, not the displayed genre name.</span></span> <span data-ttu-id="24145-138">次の画像では、選択されたジャンルは**ディスコ**、アーティストは**Donna 夏**です。</span><span class="sxs-lookup"><span data-stu-id="24145-138">In the image below, the genre selected is **Disco** and the artist is **Donna Summer**.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image4.png)

### <a name="examining-the-aspnet-mvc-scaffolded-code"></a><span data-ttu-id="24145-139">ASP.NET MVC スキャフォールディングコードの検証</span><span class="sxs-lookup"><span data-stu-id="24145-139">Examining the ASP.NET MVC Scaffolded Code</span></span>

<span data-ttu-id="24145-140">*Controllers\StoreManagerController.cs*ファイルを開き、`HTTP GET Create` メソッドを見つけます。</span><span class="sxs-lookup"><span data-stu-id="24145-140">Open the *Controllers\StoreManagerController.cs* file and find the `HTTP GET Create` method.</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample5.cs)]

<span data-ttu-id="24145-141">`Create` メソッドは、2つの[Selectlist](https://msdn.microsoft.com/library/system.web.mvc.selectlist.aspx)オブジェクトを `ViewBag`に追加します。1つはジャンル情報を格納するオブジェクト、もう1つはアーティスト情報を格納するオブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="24145-141">The `Create` method adds two [SelectList](https://msdn.microsoft.com/library/system.web.mvc.selectlist.aspx) objects to the `ViewBag`, one to contain the genre information, and one to contain the artist information.</span></span> <span data-ttu-id="24145-142">上で使用される[Selectlist](https://msdn.microsoft.com/library/dd505286.aspx)コンストラクターのオーバーロードには、次の3つの引数が必要です。</span><span class="sxs-lookup"><span data-stu-id="24145-142">The [SelectList](https://msdn.microsoft.com/library/dd505286.aspx) constructor overload used above takes three arguments:</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample6.cs)]

1. <span data-ttu-id="24145-143">*items*: リスト内の項目を含む[IEnumerable](https://msdn.microsoft.com/library/system.collections.ienumerable.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="24145-143">*items*: An [IEnumerable](https://msdn.microsoft.com/library/system.collections.ienumerable.aspx) containing the items in the list.</span></span> <span data-ttu-id="24145-144">上記の例では、`db.Genres`によって返されるジャンルの一覧を示します。</span><span class="sxs-lookup"><span data-stu-id="24145-144">In the example above, the list of genres returned by `db.Genres`.</span></span>
2. <span data-ttu-id="24145-145">*dataValueField*: キー値を含む**IEnumerable**リスト内のプロパティの名前。</span><span class="sxs-lookup"><span data-stu-id="24145-145">*dataValueField*: The name of the property in the **IEnumerable** list that contains the key value.</span></span> <span data-ttu-id="24145-146">上記の例では、を `GenreId` し、`ArtistId`します。</span><span class="sxs-lookup"><span data-stu-id="24145-146">In the example above, `GenreId` and `ArtistId`.</span></span>
3. <span data-ttu-id="24145-147">*Datatextfield*: 表示する情報が格納されている**IEnumerable**リスト内のプロパティの名前。</span><span class="sxs-lookup"><span data-stu-id="24145-147">*dataTextField*: The name of the property in the **IEnumerable** list that contains the information to display.</span></span> <span data-ttu-id="24145-148">アーティストと genre テーブルの両方で、[`name`] フィールドが使用されます。</span><span class="sxs-lookup"><span data-stu-id="24145-148">In both the artists and genre table, the `name` field is used.</span></span>

<span data-ttu-id="24145-149">*Views\StoreManager\Create.cshtml*ファイルを開き、[ジャンル] フィールドの `Html.DropDownList` ヘルパーマークアップを確認します。</span><span class="sxs-lookup"><span data-stu-id="24145-149">Open the *Views\StoreManager\Create.cshtml* file and examine the `Html.DropDownList` helper markup for the genre field.</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample7.cshtml)]

<span data-ttu-id="24145-150">最初の行は、create ビューが `Album` モデルを取得することを示しています。</span><span class="sxs-lookup"><span data-stu-id="24145-150">The first line shows that the create view takes an `Album` model.</span></span> <span data-ttu-id="24145-151">上に示した `Create` メソッドでは、モデルが渡されなかったため、ビューは**null** `Album` モデルを取得します。</span><span class="sxs-lookup"><span data-stu-id="24145-151">In the `Create` method shown above, no model was passed, so the view gets a **null** `Album` model.</span></span> <span data-ttu-id="24145-152">この時点では、新しいアルバムを作成しています。そのため、`Album` データがありません。</span><span class="sxs-lookup"><span data-stu-id="24145-152">At this point we are creating a new album so we don't have any `Album` data for it.</span></span>

<span data-ttu-id="24145-153">上に示した[Html の DropDownList](https://msdn.microsoft.com/library/dd492948.aspx)オーバーロードは、モデルにバインドするフィールドの名前を受け取ります。</span><span class="sxs-lookup"><span data-stu-id="24145-153">The [Html.DropDownList](https://msdn.microsoft.com/library/dd492948.aspx) overload shown above takes the name of the field to bind to the model.</span></span> <span data-ttu-id="24145-154">また、この名前を使用して、 [Selectlist](https://msdn.microsoft.com/library/dd505286.aspx)オブジェクトを含む**ViewBag**オブジェクトを検索します。</span><span class="sxs-lookup"><span data-stu-id="24145-154">It also uses this name to look for a **ViewBag** object containing a [SelectList](https://msdn.microsoft.com/library/dd505286.aspx) object.</span></span> <span data-ttu-id="24145-155">このオーバーロードを使用して、 **ViewBag SelectList**オブジェクトに `GenreId`という名前を指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="24145-155">Using this overload, you are required to name the **ViewBag SelectList** object `GenreId`.</span></span> <span data-ttu-id="24145-156">2番目のパラメーター (`String.Empty`) は、項目が選択されていない場合に表示されるテキストです。</span><span class="sxs-lookup"><span data-stu-id="24145-156">The second parameter (`String.Empty`) is the text to display when no item is selected.</span></span> <span data-ttu-id="24145-157">これは、新しいアルバムを作成するときに必要なことです。</span><span class="sxs-lookup"><span data-stu-id="24145-157">This is exactly what we want when creating a new album.</span></span> <span data-ttu-id="24145-158">2番目のパラメーターを削除し、次のコードを使用するとします。</span><span class="sxs-lookup"><span data-stu-id="24145-158">If you removed the second parameter and used the following code:</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample8.cshtml)]

<span data-ttu-id="24145-159">選択リストは、既定では最初の要素、またはサンプルのロックになります。</span><span class="sxs-lookup"><span data-stu-id="24145-159">The select list would default to the first element, or Rock in our sample.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image5.png)

<span data-ttu-id="24145-160">`HTTP POST Create` メソッドを調べています。</span><span class="sxs-lookup"><span data-stu-id="24145-160">Examining the `HTTP POST Create` method.</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample9.cs)]

<span data-ttu-id="24145-161">`Create` メソッドのこのオーバーロードは、ASP.NET MVC モデルバインドシステムによって作成された `album` のオブジェクトを、ポストされたフォーム値から受け取ります。</span><span class="sxs-lookup"><span data-stu-id="24145-161">This overload of the `Create` method takes an `album` object, created by the ASP.NET MVC model binding system from the form values posted.</span></span> <span data-ttu-id="24145-162">新しいアルバムを送信するときに、モデルの状態が有効で、データベースエラーがない場合は、新しいアルバムにデータベースが追加されます。</span><span class="sxs-lookup"><span data-stu-id="24145-162">When you submit a new album, if model state is valid and there are no database errors, the new album is added the database.</span></span> <span data-ttu-id="24145-163">次の図は、新しいアルバムの作成を示しています。</span><span class="sxs-lookup"><span data-stu-id="24145-163">The following image shows the creation of a new album.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image6.png)

<span data-ttu-id="24145-164">[Fiddler ツール](http://www.fiddler2.com/fiddler2/)を使用すると、ASP.NET MVC モデルバインドがアルバムオブジェクトの作成に使用する、ポストされたフォームの値を調べることができます。</span><span class="sxs-lookup"><span data-stu-id="24145-164">You can use the [fiddler tool](http://www.fiddler2.com/fiddler2/) to examine the posted form values that ASP.NET MVC model binding uses to create the album object.</span></span>

<span data-ttu-id="24145-165">[https://login.microsoftonline.com/consumers/](![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image7.png))</span><span class="sxs-lookup"><span data-stu-id="24145-165">![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image7.png).</span></span>

### <a name="refactoring-the-viewbag-selectlist-creation"></a><span data-ttu-id="24145-166">ViewBag SelectList 作成のリファクタリング</span><span class="sxs-lookup"><span data-stu-id="24145-166">Refactoring the ViewBag SelectList Creation</span></span>

<span data-ttu-id="24145-167">`Edit` メソッドと `HTTP POST Create` メソッドの両方に同じコードがあるため、 **ViewBag**で**selectlist**を設定できます。</span><span class="sxs-lookup"><span data-stu-id="24145-167">Both the `Edit` methods and the `HTTP POST Create` method have identical code to set up the **SelectList** in the **ViewBag**.</span></span> <span data-ttu-id="24145-168">[ドライ](http://en.wikipedia.org/wiki/Don't_repeat_yourself)の精神で、このコードをリファクターします。</span><span class="sxs-lookup"><span data-stu-id="24145-168">In the spirit of [DRY](http://en.wikipedia.org/wiki/Don't_repeat_yourself), we will refactor this code.</span></span> <span data-ttu-id="24145-169">このリファクタリングされたコードは後で使用します。</span><span class="sxs-lookup"><span data-stu-id="24145-169">We'll make use of this refactored code later.</span></span>

<span data-ttu-id="24145-170">新しいメソッドを作成して、ジャンルとアーティストの**Selectlist**を**ViewBag**に追加します。</span><span class="sxs-lookup"><span data-stu-id="24145-170">Create a new method to add a genre and artist **SelectList** to the **ViewBag**.</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample10.cs)]

<span data-ttu-id="24145-171">`Create` と `Edit` の各メソッドの `ViewBag` を設定する2つの行を、`SetGenreArtistViewBag` メソッドの呼び出しに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="24145-171">Replace the two lines setting the `ViewBag` in each of the `Create` and `Edit` methods with a call to the `SetGenreArtistViewBag` method.</span></span> <span data-ttu-id="24145-172">完成したコードを以下に示します。</span><span class="sxs-lookup"><span data-stu-id="24145-172">The completed code is shown below.</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample11.cs)]

<span data-ttu-id="24145-173">新しいアルバムを作成し、アルバムを編集して、変更が有効であることを確認します。</span><span class="sxs-lookup"><span data-stu-id="24145-173">Create a new album and edit an album to verify the changes work.</span></span>

### <a name="explicitly-passing-the-selectlist-to-the-dropdownlist"></a><span data-ttu-id="24145-174">SelectList を明示的に DropDownList に渡す</span><span class="sxs-lookup"><span data-stu-id="24145-174">Explicitly Passing the SelectList to the DropDownList</span></span>

<span data-ttu-id="24145-175">ASP.NET MVC スキャフォールディングによって作成される create ビューと edit ビューでは、次の**DropDownList**オーバーロードを使用します。</span><span class="sxs-lookup"><span data-stu-id="24145-175">The create and edit views created by the ASP.NET MVC scaffolding use the following **DropDownList** overload:</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample12.cs)]

<span data-ttu-id="24145-176">Create ビューの `DropDownList` マークアップを次に示します。</span><span class="sxs-lookup"><span data-stu-id="24145-176">The `DropDownList` markup for the create view is shown below.</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample13.cshtml)]

<span data-ttu-id="24145-177">`SelectList` の `ViewBag` プロパティの名前は `GenreId`であるため、 **DropDownList**ヘルパーは**ViewBag**の `GenreId`**selectlist**を使用します。</span><span class="sxs-lookup"><span data-stu-id="24145-177">Because the `ViewBag` property for the `SelectList` is named `GenreId`, the **DropDownList** helper will use the `GenreId`**SelectList** in the **ViewBag**.</span></span> <span data-ttu-id="24145-178">次の**DropDownList**オーバーロードでは、`SelectList` が明示的に渡されます。</span><span class="sxs-lookup"><span data-stu-id="24145-178">In the following **DropDownList** overload, the `SelectList` is explicitly passed in.</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample14.cs)]

<span data-ttu-id="24145-179">*Views\StoreManager\Edit.cshtml*ファイルを開き、 **DropDownList**呼び出しを変更して、上記のオーバーロードを使用して**selectlist**を明示的に渡します。</span><span class="sxs-lookup"><span data-stu-id="24145-179">Open the *Views\StoreManager\Edit.cshtml* file, and change the **DropDownList** call to explicitly pass in the **SelectList**, using the overload above.</span></span> <span data-ttu-id="24145-180">ジャンルカテゴリに対してこれを行います。</span><span class="sxs-lookup"><span data-stu-id="24145-180">Do this for the Genre category.</span></span> <span data-ttu-id="24145-181">完成したコードを次に示します。</span><span class="sxs-lookup"><span data-stu-id="24145-181">The completed code is shown below:</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample15.cshtml)]

<span data-ttu-id="24145-182">アプリケーションを実行し、 **[管理者]** リンクをクリックします。次に、ジャズアルバムに移動し、 **[編集]** リンクを選択します。</span><span class="sxs-lookup"><span data-stu-id="24145-182">Run the application and click the **Admin** link, then navigate to a Jazz album and select the **Edit** link.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image8.png)

<span data-ttu-id="24145-183">現在選択されているジャンルとしてジャズを表示するのではなく、ロックが表示されます。</span><span class="sxs-lookup"><span data-stu-id="24145-183">Instead of showing Jazz as the currently selected genre, Rock is displayed.</span></span> <span data-ttu-id="24145-184">文字列引数 (バインドするプロパティ) と**Selectlist**オブジェクトの名前が同じ場合、選択した値は使用されません。</span><span class="sxs-lookup"><span data-stu-id="24145-184">When the string argument (the property to bind) and the **SelectList** object have the same name, the selected value is not used.</span></span> <span data-ttu-id="24145-185">選択された値が指定されていない場合、ブラウザーは既定で**Selectlist**の最初の要素 (上記の例では**ロック**) を使用します。</span><span class="sxs-lookup"><span data-stu-id="24145-185">When there is no selected value provided, browsers default to the first element in the **SelectList**(which is **Rock** in the example above).</span></span> <span data-ttu-id="24145-186">これは、 **DropDownList**ヘルパーの既知の制限です。</span><span class="sxs-lookup"><span data-stu-id="24145-186">This is a known limitation of the **DropDownList** helper.</span></span>

<span data-ttu-id="24145-187">*Controllers\StoreManagerController.cs*ファイルを開き、 **selectlist**オブジェクト名を `Genres` と `Artists`に変更します。</span><span class="sxs-lookup"><span data-stu-id="24145-187">Open the *Controllers\StoreManagerController.cs* file and change the **SelectList** object names to `Genres` and `Artists`.</span></span> <span data-ttu-id="24145-188">完成したコードを次に示します。</span><span class="sxs-lookup"><span data-stu-id="24145-188">The completed code is shown below:</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample16.cs)]

<span data-ttu-id="24145-189">ジャンルとアーティストの名前は、各カテゴリの ID だけではなく、カテゴリに適した名前になります。</span><span class="sxs-lookup"><span data-stu-id="24145-189">The names Genres and Artists are better names for the categories, as they contain more than just the ID of each category.</span></span> <span data-ttu-id="24145-190">以前に行ったリファクタリングはオフになっていました。</span><span class="sxs-lookup"><span data-stu-id="24145-190">The refactoring we did earlier paid off.</span></span> <span data-ttu-id="24145-191">**ViewBag**を4つの方法で変更するのではなく、変更が `SetGenreArtistViewBag` メソッドに分離されました。</span><span class="sxs-lookup"><span data-stu-id="24145-191">Instead of changing the **ViewBag** in four methods, our changes were isolated to the `SetGenreArtistViewBag` method.</span></span>

<span data-ttu-id="24145-192">Create ビューと edit ビューで**DropDownList**呼び出しを変更して、新しい**selectlist**名を使用します。</span><span class="sxs-lookup"><span data-stu-id="24145-192">Change the **DropDownList** call in the create and edit views to use the new **SelectList** names.</span></span> <span data-ttu-id="24145-193">次に、編集ビューの新しいマークアップを示します。</span><span class="sxs-lookup"><span data-stu-id="24145-193">The new markup for the edit view is shown below:</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample17.cshtml)]

<span data-ttu-id="24145-194">Create view では、SelectList 内の最初の項目が表示されないように、空の文字列が必要です。</span><span class="sxs-lookup"><span data-stu-id="24145-194">The Create view requires an empty string to prevent the first item in the SelectList from being displayed.</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample18.cshtml)]

<span data-ttu-id="24145-195">新しいアルバムを作成し、アルバムを編集して、変更が有効であることを確認します。</span><span class="sxs-lookup"><span data-stu-id="24145-195">Create a new album and edit an album to verify the changes work.</span></span> <span data-ttu-id="24145-196">[ロック] 以外のジャンルのアルバムを選択して、編集コードをテストします。</span><span class="sxs-lookup"><span data-stu-id="24145-196">Test the edit code by selecting an album with a genre other than Rock.</span></span>

### <a name="using-a-view-model-with-the-dropdownlist-helper"></a><span data-ttu-id="24145-197">DropDownList ヘルパーでのビューモデルの使用</span><span class="sxs-lookup"><span data-stu-id="24145-197">Using a View Model with the DropDownList Helper</span></span>

<span data-ttu-id="24145-198">`AlbumSelectListViewModel`という名前の Viewmodel フォルダーに新しいクラスを作成します。</span><span class="sxs-lookup"><span data-stu-id="24145-198">Create a new class in the ViewModels folder named `AlbumSelectListViewModel`.</span></span> <span data-ttu-id="24145-199">`AlbumSelectListViewModel` クラスのコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="24145-199">Replace the code in the `AlbumSelectListViewModel` class with the following:</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample19.cs)]

<span data-ttu-id="24145-200">`AlbumSelectListViewModel` コンストラクターは、アルバム、アーティスト、ジャンルのリストを受け取り、アルバムを含むオブジェクトと、ジャンルとアーティストの `SelectList` を作成します。</span><span class="sxs-lookup"><span data-stu-id="24145-200">The `AlbumSelectListViewModel` constructor takes an album, a list of artists and genres and creates an object containing the album and a `SelectList` for genres and artists.</span></span>

<span data-ttu-id="24145-201">次の手順でビューを作成するときに `AlbumSelectListViewModel` を使用できるように、プロジェクトをビルドします。</span><span class="sxs-lookup"><span data-stu-id="24145-201">Build the project so the `AlbumSelectListViewModel` is available when we create a view in the next step.</span></span>

<span data-ttu-id="24145-202">`StoreManagerController`に `EditVM` メソッドを追加します。</span><span class="sxs-lookup"><span data-stu-id="24145-202">Add an `EditVM` method to the `StoreManagerController`.</span></span> <span data-ttu-id="24145-203">完成したコードを以下に示します。</span><span class="sxs-lookup"><span data-stu-id="24145-203">The completed code is shown below.</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample20.cs)]

<span data-ttu-id="24145-204">`AlbumSelectListViewModel`右クリックして **[解決]** を選択し、次に**MvcMusicStore viewmodel; を使用**します。</span><span class="sxs-lookup"><span data-stu-id="24145-204">Right click `AlbumSelectListViewModel`, select **Resolve**, then **using MvcMusicStore.ViewModels;**.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image9.png)

<span data-ttu-id="24145-205">または、次の using ステートメントを追加することもできます。</span><span class="sxs-lookup"><span data-stu-id="24145-205">Alternatively, you can add the following using statement:</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample21.cs)]

<span data-ttu-id="24145-206">`EditVM` 右クリックし、 **[ビューの追加]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="24145-206">Right click `EditVM` and select **Add View**.</span></span> <span data-ttu-id="24145-207">次に示すオプションを使用します。</span><span class="sxs-lookup"><span data-stu-id="24145-207">Use the options shown below.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image10.png)

<span data-ttu-id="24145-208">**[追加]** を選択し、 *Views\StoreManager\EditVM.cshtml*ファイルの内容を次の内容に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="24145-208">Select **Add**, then replace the contents of the *Views\StoreManager\EditVM.cshtml* file with the following:</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample22.cshtml)]

<span data-ttu-id="24145-209">`EditVM` マークアップは、次の例外を除き、元の `Edit` マークアップとよく似ています。</span><span class="sxs-lookup"><span data-stu-id="24145-209">The `EditVM` markup is very similar to the original `Edit` markup with the following exceptions.</span></span>

- <span data-ttu-id="24145-210">`Edit` ビューのモデルのプロパティは `model.property`フォーム (`model.Title` など) です。</span><span class="sxs-lookup"><span data-stu-id="24145-210">Model properties in the `Edit` view are of the form `model.property`(for example, `model.Title` ).</span></span> <span data-ttu-id="24145-211">`EditVm` ビューのモデルのプロパティは `model.Album.property`フォーム (`model.Album.Title`など) です。</span><span class="sxs-lookup"><span data-stu-id="24145-211">Model properties in the `EditVm` view are of the form `model.Album.property`(for example, `model.Album.Title`).</span></span> <span data-ttu-id="24145-212">これは、`EditVM` ビューには、`Edit` ビューのような `Album` ではなく、`Album`のコンテナーが渡されるためです。</span><span class="sxs-lookup"><span data-stu-id="24145-212">That's because the `EditVM` view is passed a container for an `Album`, not an `Album` as in the `Edit` view.</span></span>
- <span data-ttu-id="24145-213">**DropDownList**の2番目のパラメーターは、 **ViewBag**ではなく、ビューモデルから取得されます。</span><span class="sxs-lookup"><span data-stu-id="24145-213">The **DropDownList** second parameter comes from the view model, not the **ViewBag**.</span></span>
- <span data-ttu-id="24145-214">`EditVM` ビューの**Beginform**ヘルパーは、`Edit` アクションメソッドに明示的にポストバックします。</span><span class="sxs-lookup"><span data-stu-id="24145-214">The **BeginForm** helper in the `EditVM` view explicitly posts back to the `Edit` action method.</span></span> <span data-ttu-id="24145-215">`Edit` アクションにポストバックすることで、`HTTP POST EditVM` アクションを記述する必要がなくなり、`HTTP POST` の `Edit` アクションを再利用できます。</span><span class="sxs-lookup"><span data-stu-id="24145-215">By posting back to the `Edit` action, we don't have to write an `HTTP POST EditVM` action and can reuse the `HTTP POST` `Edit` action.</span></span>

<span data-ttu-id="24145-216">アプリケーションを実行し、アルバムを編集します。</span><span class="sxs-lookup"><span data-stu-id="24145-216">Run the application and edit an album.</span></span> <span data-ttu-id="24145-217">`EditVM`を使用するように URL を変更します。</span><span class="sxs-lookup"><span data-stu-id="24145-217">Change the URL to use `EditVM`.</span></span> <span data-ttu-id="24145-218">フィールドを変更し、 **[保存]** ボタンをクリックして、コードが動作していることを確認します。</span><span class="sxs-lookup"><span data-stu-id="24145-218">Change a field and hit the **Save** button to verify the code is working.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image11.png)

### <a name="which-approach-should-you-use"></a><span data-ttu-id="24145-219">どの方法を使用する必要がありますか。</span><span class="sxs-lookup"><span data-stu-id="24145-219">Which Approach Should You Use?</span></span>

<span data-ttu-id="24145-220">表示される3つの方法はすべて許容されます。</span><span class="sxs-lookup"><span data-stu-id="24145-220">All three approaches shown are acceptable.</span></span> <span data-ttu-id="24145-221">多くの開発者は、`ViewBag`を使用して、`SelectList` を `DropDownList` に明示的に渡すことを好みます。</span><span class="sxs-lookup"><span data-stu-id="24145-221">Many developers prefer to explicitly pass the `SelectList` to the `DropDownList` using the `ViewBag`.</span></span> <span data-ttu-id="24145-222">このアプローチには、より適切な名前をコレクションに使用する柔軟性を提供するという利点があります。</span><span class="sxs-lookup"><span data-stu-id="24145-222">This approach has the added advantage of giving you the flexibility of using a more appropriate name for the collection.</span></span> <span data-ttu-id="24145-223">注意点として、`ViewBag SelectList` オブジェクトにモデルプロパティと同じ名前を指定することはできません。</span><span class="sxs-lookup"><span data-stu-id="24145-223">The one caveat is you cannot name the `ViewBag SelectList` object the same name as the model property.</span></span>

<span data-ttu-id="24145-224">一部の開発者は、ビューモデルのアプローチを好む場合があります。</span><span class="sxs-lookup"><span data-stu-id="24145-224">Some developers prefer the ViewModel approach.</span></span> <span data-ttu-id="24145-225">他のユーザーは、より詳細なマークアップと生成されたモデルビューの手法を考慮して、欠点を検討します。</span><span class="sxs-lookup"><span data-stu-id="24145-225">Others consider the more verbose markup and generated HTML of the ViewModel approach a disadvantage.</span></span>

<span data-ttu-id="24145-226">このセクションでは、 **DropDownList**とカテゴリデータを使用する3つの方法を学習しました。</span><span class="sxs-lookup"><span data-stu-id="24145-226">In this section we have learned three approaches to using the **DropDownList** with category data.</span></span> <span data-ttu-id="24145-227">次のセクションでは、新しいカテゴリを追加する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="24145-227">In the next section, we'll show how to add a new category.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="24145-228">[前へ](using-the-dropdownlist-helper-with-aspnet-mvc.md)
> [次へ](adding-a-new-category-to-the-dropdownlist-using-jquery-ui.md)</span><span class="sxs-lookup"><span data-stu-id="24145-228">[Previous](using-the-dropdownlist-helper-with-aspnet-mvc.md)
[Next](adding-a-new-category-to-the-dropdownlist-using-jquery-ui.md)</span></span>
