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
# <a name="introducing-aspnet-web-pages---deleting-database-data"></a><span data-ttu-id="3e81c-104">ASP.NET Web ページの概要-データベースデータの削除</span><span class="sxs-lookup"><span data-stu-id="3e81c-104">Introducing ASP.NET Web Pages - Deleting Database Data</span></span>

<span data-ttu-id="3e81c-105">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="3e81c-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="3e81c-106">このチュートリアルでは、個々のデータベースエントリを削除する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="3e81c-106">This tutorial shows you how to delete an individual database entry.</span></span> <span data-ttu-id="3e81c-107">[ASP.NET Web ページでデータベースデータを更新](updating-data.md)することによってシリーズを完了していることを前提としています。</span><span class="sxs-lookup"><span data-stu-id="3e81c-107">It assumes you have completed the series through [Updating Database Data in ASP.NET Web Pages](updating-data.md).</span></span>
> 
> <span data-ttu-id="3e81c-108">ここでは、次の内容について学習します。</span><span class="sxs-lookup"><span data-stu-id="3e81c-108">What you'll learn:</span></span>
> 
> - <span data-ttu-id="3e81c-109">レコードの一覧から個々のレコードを選択する方法。</span><span class="sxs-lookup"><span data-stu-id="3e81c-109">How to select an individual record from a listing of records.</span></span>
> - <span data-ttu-id="3e81c-110">データベースから1つのレコードを削除する方法。</span><span class="sxs-lookup"><span data-stu-id="3e81c-110">How to delete a single record from a database.</span></span>
> - <span data-ttu-id="3e81c-111">フォームで特定のボタンがクリックされたことを確認する方法。</span><span class="sxs-lookup"><span data-stu-id="3e81c-111">How to check that a specific button was clicked in a form.</span></span>
>   
> 
> <span data-ttu-id="3e81c-112">説明する機能/テクノロジ:</span><span class="sxs-lookup"><span data-stu-id="3e81c-112">Features/technologies discussed:</span></span>
> 
> - <span data-ttu-id="3e81c-113">`WebGrid` ヘルパー。</span><span class="sxs-lookup"><span data-stu-id="3e81c-113">The `WebGrid` helper.</span></span>
> - <span data-ttu-id="3e81c-114">SQL `Delete` コマンド。</span><span class="sxs-lookup"><span data-stu-id="3e81c-114">The SQL `Delete` command.</span></span>
> - <span data-ttu-id="3e81c-115">SQL `Delete` コマンドを実行する `Database.Execute` メソッド。</span><span class="sxs-lookup"><span data-stu-id="3e81c-115">The `Database.Execute` method to run a SQL `Delete` command.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="3e81c-116">作成するアプリケーション:</span><span class="sxs-lookup"><span data-stu-id="3e81c-116">What You'll Build</span></span>

<span data-ttu-id="3e81c-117">前のチュートリアルでは、既存のデータベースレコードを更新する方法について学習しました。</span><span class="sxs-lookup"><span data-stu-id="3e81c-117">In the previous tutorial, you learned how to update an existing database record.</span></span> <span data-ttu-id="3e81c-118">このチュートリアルは似ていますが、レコードを更新するのではなく、レコードを削除する点が異なります。</span><span class="sxs-lookup"><span data-stu-id="3e81c-118">This tutorial is similar, except that instead of updating the record, you'll delete it.</span></span> <span data-ttu-id="3e81c-119">プロセスはほぼ同じですが、削除の方が簡単であるため、このチュートリアルは短くなります。</span><span class="sxs-lookup"><span data-stu-id="3e81c-119">The processes are much the same, except that deleting is simpler, so this tutorial will be short.</span></span>

<span data-ttu-id="3e81c-120">[*ムービー* ] ページで `WebGrid` ヘルパーを更新して、前に追加した**編集**リンクに付随する各ムービーの横に **[削除]** リンクが表示されるようにします。</span><span class="sxs-lookup"><span data-stu-id="3e81c-120">In the *Movies* page, you'll update the `WebGrid` helper so that it displays a **Delete** link next to each movie to accompany the **Edit** link you added earlier.</span></span>

![各ムービーの [削除] リンクを示すムービーページ](deleting-data/_static/image1.png)

<span data-ttu-id="3e81c-122">編集と同様に、 **[削除]** リンクをクリックすると、別のページに移動します。このページでは、ムービー情報が既にフォームに含まれています。</span><span class="sxs-lookup"><span data-stu-id="3e81c-122">As with editing, when you click the **Delete** link, it takes you to a different page, where the movie information is already in a form:</span></span>

![ムービーが表示されているムービーページを削除する](deleting-data/_static/image2.png)

<span data-ttu-id="3e81c-124">このボタンをクリックすると、レコードが完全に削除されます。</span><span class="sxs-lookup"><span data-stu-id="3e81c-124">You can then click the button to delete the record permanently.</span></span>

## <a name="adding-a-delete-link-to-the-movie-listing"></a><span data-ttu-id="3e81c-125">ムービーの一覧への削除リンクの追加</span><span class="sxs-lookup"><span data-stu-id="3e81c-125">Adding a Delete Link to the Movie Listing</span></span>

<span data-ttu-id="3e81c-126">まず、`WebGrid` ヘルパーに**Delete**リンクを追加します。</span><span class="sxs-lookup"><span data-stu-id="3e81c-126">You'll start by adding a **Delete** link to the `WebGrid` helper.</span></span> <span data-ttu-id="3e81c-127">このリンクは、前のチュートリアルで追加した**編集**リンクに似ています。</span><span class="sxs-lookup"><span data-stu-id="3e81c-127">This link is similar to the **Edit** link you added in a previous tutorial.</span></span>

<span data-ttu-id="3e81c-128">ムービーの*cshtml*ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="3e81c-128">Open the *Movies.cshtml* file.</span></span>

<span data-ttu-id="3e81c-129">列を追加して、ページの本文の `WebGrid` マークアップを変更します。</span><span class="sxs-lookup"><span data-stu-id="3e81c-129">Change the `WebGrid` markup in the body of the page by adding a column.</span></span> <span data-ttu-id="3e81c-130">変更されたマークアップを次に示します。</span><span class="sxs-lookup"><span data-stu-id="3e81c-130">Here's the modified markup:</span></span>

[!code-html[Main](deleting-data/samples/sample1.html?highlight=9-10)]

<span data-ttu-id="3e81c-131">新しい列は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="3e81c-131">The new column is this one:</span></span>

[!code-html[Main](deleting-data/samples/sample2.html)]

<span data-ttu-id="3e81c-132">グリッドの構成方法では、 **[編集]** 列がグリッドの一番左にあり、 **[削除]** 列が右端になります。</span><span class="sxs-lookup"><span data-stu-id="3e81c-132">The way the grid is configured, the **Edit** column is leftmost in the grid and the **Delete** column is rightmost.</span></span> <span data-ttu-id="3e81c-133">(これに気付いていない場合は、`Year` 列の後にコンマがあります)。これらのリンク列がどこに配置されているかについて特別なことはありません。また、互いに簡単に配置することもできます。</span><span class="sxs-lookup"><span data-stu-id="3e81c-133">(There's a comma after the `Year` column now, in case you didn't notice that.) There's nothing special about where these link columns go, and you could as easily put them next to each other.</span></span> <span data-ttu-id="3e81c-134">このケースでは、これらは混同されることがないように分離されています。</span><span class="sxs-lookup"><span data-stu-id="3e81c-134">In this case, they're separate to make them harder to get mixed up.</span></span>

![[編集] リンクと [詳細] リンクが横に表示されていないことを示すムービーページ](deleting-data/_static/image3.png)

<span data-ttu-id="3e81c-136">新しい列には、"Delete" というテキストを含むリンク (`<a>` 要素) が表示されます。</span><span class="sxs-lookup"><span data-stu-id="3e81c-136">The new column shows a link (`<a>` element) whose text says "Delete".</span></span> <span data-ttu-id="3e81c-137">リンクのターゲット (`href` 属性) は、次の URL のように最終的に解決されるコードです。ムービーごとに `id` 値は異なります。</span><span class="sxs-lookup"><span data-stu-id="3e81c-137">The target of the link (its `href` attribute) is code that ultimately resolves to something like this URL, with the `id` value different for each movie:</span></span>

[!code-css[Main](deleting-data/samples/sample3.css)]

<span data-ttu-id="3e81c-138">このリンクを選択すると、 *DeleteMovie*という名前のページが呼び出され、選択したムービーの ID が渡されます。</span><span class="sxs-lookup"><span data-stu-id="3e81c-138">This link will invoke a page named *DeleteMovie* and pass it the ID of the movie you've selected.</span></span>

<span data-ttu-id="3e81c-139">このチュートリアルでは、このリンクの構築方法について詳しく説明しません。これは、前のチュートリアルの**編集**リンク ([ASP.NET Web ページでのデータベースデータの更新](updating-data.md)) とほぼ同じであるためです。</span><span class="sxs-lookup"><span data-stu-id="3e81c-139">This tutorial won't go into detail about how this link is constructed, because it's almost identical to the **Edit** link from the previous tutorial ([Updating Database Data in ASP.NET Web Pages](updating-data.md)).</span></span>

## <a name="creating-the-delete-page"></a><span data-ttu-id="3e81c-140">[削除] ページの作成</span><span class="sxs-lookup"><span data-stu-id="3e81c-140">Creating the Delete Page</span></span>

<span data-ttu-id="3e81c-141">これで、グリッド内の **[削除]** リンクのターゲットとなるページを作成できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="3e81c-141">Now you can create the page that will be the target for the **Delete** link in the grid.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="3e81c-142">**重要**最初に削除するレコードを選択し、別のページとボタンを使用してプロセスを確認する方法は、セキュリティ上重要です。</span><span class="sxs-lookup"><span data-stu-id="3e81c-142">**Important** The technique of first selecting a record to delete and then using a separate page and button to confirm the process is extremely important for security.</span></span> <span data-ttu-id="3e81c-143">前のチュートリアルで読んだように、web サイトに*何らか*の変更を加える場合は、*常*に HTTP POST 操作を使用して &mdash; フォームを使用して行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="3e81c-143">As you've read in previous tutorials, making *any* sort of change to your website should *always* be done using a form &mdash; that is, using an HTTP POST operation.</span></span> <span data-ttu-id="3e81c-144">リンクをクリックして (つまり、GET 操作を使用して) サイトを変更できるようにした場合、ユーザーはサイトに単純な要求を行い、データを削除することができます。</span><span class="sxs-lookup"><span data-stu-id="3e81c-144">If you made it possible to change the site just by clicking a link (that is, using a GET operation), people could make simple requests to your site and delete your data.</span></span> <span data-ttu-id="3e81c-145">サイトにインデックスを作成している検索エンジンのクローラーでも、次のリンクによってデータが誤って削除される可能性があります。</span><span class="sxs-lookup"><span data-stu-id="3e81c-145">Even a search-engine crawler that's indexing your site could inadvertently delete data just by following links.</span></span>
> 
> <span data-ttu-id="3e81c-146">アプリでレコードを変更できるようにするには、編集のためにレコードをユーザーに提示する必要があります。</span><span class="sxs-lookup"><span data-stu-id="3e81c-146">When your app lets people change a record, you have to present the record to the user for editing anyway.</span></span> <span data-ttu-id="3e81c-147">ただし、レコードを削除する場合は、この手順をスキップすることがあります。</span><span class="sxs-lookup"><span data-stu-id="3e81c-147">But you might be tempted to skip this step for deleting a record.</span></span> <span data-ttu-id="3e81c-148">ただし、この手順は省略しないでください。</span><span class="sxs-lookup"><span data-stu-id="3e81c-148">Don't skip that step, though.</span></span> <span data-ttu-id="3e81c-149">(これは、ユーザーがレコードを確認し、意図したレコードを削除していることを確認する場合にも役立ちます)。</span><span class="sxs-lookup"><span data-stu-id="3e81c-149">(It's also helpful for users to see the record and confirm that they're deleting the record that they intended.)</span></span>
> 
> <span data-ttu-id="3e81c-150">以降のチュートリアルでは、ユーザーがレコードを削除する前にログインしなければならないように、ログイン機能を追加する方法を説明します。</span><span class="sxs-lookup"><span data-stu-id="3e81c-150">In a subsequent tutorial set, you'll see how to add login functionality so a user would have to log in before deleting a record.</span></span>

<span data-ttu-id="3e81c-151">*DeleteMovie*という名前のページを作成し、ファイルの内容を次のマークアップに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="3e81c-151">Create a page named *DeleteMovie.cshtml* and replace what's in the file with the following markup:</span></span>

[!code-cshtml[Main](deleting-data/samples/sample4.cshtml)]

<span data-ttu-id="3e81c-152">このマークアップは、 *Editmovie*ページに似ていますが、テキストボックス (`<input type="text">`) を使用するのではなく、マークアップに `<span>` の要素が含まれている点が異なります。</span><span class="sxs-lookup"><span data-stu-id="3e81c-152">This markup is like the *EditMovie* pages, except that instead of using text boxes (`<input type="text">`), the markup includes `<span>` elements.</span></span> <span data-ttu-id="3e81c-153">編集するものはありません。</span><span class="sxs-lookup"><span data-stu-id="3e81c-153">There's nothing here to edit.</span></span> <span data-ttu-id="3e81c-154">必要なのは、ムービーの詳細を表示して、ユーザーが適切なムービーを削除していることを確認できるようにすることだけです。</span><span class="sxs-lookup"><span data-stu-id="3e81c-154">All you have to do is display the movie details so that users can make sure that they're deleting the right movie.</span></span>

<span data-ttu-id="3e81c-155">マークアップには、ユーザーがムービー一覧ページに戻るためのリンクが既に含まれています。</span><span class="sxs-lookup"><span data-stu-id="3e81c-155">The markup already contains a link that lets the user return to the movie listing page.</span></span>

<span data-ttu-id="3e81c-156">[ *Editmovie* ] ページと同様に、選択したムービーの ID が隠しフィールドに格納されます。</span><span class="sxs-lookup"><span data-stu-id="3e81c-156">As in the *EditMovie* page, the ID of the selected movie is stored in a hidden field.</span></span> <span data-ttu-id="3e81c-157">(クエリ文字列値として最初の場所にページが渡されます)。検証エラーを表示する `Html.ValidationSummary` の呼び出しがあります。</span><span class="sxs-lookup"><span data-stu-id="3e81c-157">(It's passed into the page in the first place as a query string value.) There's an `Html.ValidationSummary` call that will display validation errors.</span></span> <span data-ttu-id="3e81c-158">この場合、エラーは、ムービー ID がページに渡されなかったか、ムービー ID が無効である可能性があります。</span><span class="sxs-lookup"><span data-stu-id="3e81c-158">In this case, the error might be that no movie ID was passed to the page or that the movie ID is invalid.</span></span> <span data-ttu-id="3e81c-159">この状況は、*最初にムービーページで*ムービーを選択せずにこのページを実行した場合に発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="3e81c-159">This situation could occur if someone ran this page without first selecting a movie in the *Movies* page.</span></span>

<span data-ttu-id="3e81c-160">ボタンのキャプションは **[ムービーの削除]** で、name 属性は `buttonDelete`に設定されています。</span><span class="sxs-lookup"><span data-stu-id="3e81c-160">The button caption is **Delete Movie**, and its name attribute is set to `buttonDelete`.</span></span> <span data-ttu-id="3e81c-161">`name` 属性は、フォームを送信したボタンを識別するためにコード内で使用されます。</span><span class="sxs-lookup"><span data-stu-id="3e81c-161">The `name` attribute will be used in the code to identify the button that submitted the form.</span></span>

<span data-ttu-id="3e81c-162">コードを1に記述する必要があります)。ページが最初に表示されたときにムービーの詳細を確認し、2) ユーザーがボタンをクリックしたときにムービーを実際に削除します。</span><span class="sxs-lookup"><span data-stu-id="3e81c-162">You'll have to write code to 1) read the movie details when the page is first displayed and 2) actually delete the movie when the user clicks the button.</span></span>

## <a name="adding-code-to-read-a-single-movie"></a><span data-ttu-id="3e81c-163">1つのムービーを読み取るコードを追加する</span><span class="sxs-lookup"><span data-stu-id="3e81c-163">Adding Code to Read a Single Movie</span></span>

<span data-ttu-id="3e81c-164">*DeleteMovie*ページの上部に、次のコードブロックを追加します。</span><span class="sxs-lookup"><span data-stu-id="3e81c-164">At the top of the *DeleteMovie.cshtml* page, add the following code block:</span></span>

[!code-cshtml[Main](deleting-data/samples/sample5.cshtml)]

<span data-ttu-id="3e81c-165">このマークアップは、 *Editmovie*ページの対応するコードと同じです。</span><span class="sxs-lookup"><span data-stu-id="3e81c-165">This markup is the same as the corresponding code in the *EditMovie* page.</span></span> <span data-ttu-id="3e81c-166">クエリ文字列からムービー ID を取得し、ID を使用してデータベースからレコードを読み取ります。</span><span class="sxs-lookup"><span data-stu-id="3e81c-166">It gets the movie ID out of the query string and uses the ID to read a record from the database.</span></span> <span data-ttu-id="3e81c-167">このコードには、ページに渡されるムービー ID が有効であることを確認するための検証テスト (`IsInt()` と `row != null`) が含まれています。</span><span class="sxs-lookup"><span data-stu-id="3e81c-167">The code includes the validation test (`IsInt()` and `row != null`) to make sure that the movie ID being passed to the page is valid.</span></span>

<span data-ttu-id="3e81c-168">このコードは、ページを初めて実行するときにのみ実行する必要があることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="3e81c-168">Remember that this code should only run the first time the page runs.</span></span> <span data-ttu-id="3e81c-169">ユーザーが **[ムービーの削除]** ボタンをクリックしたときに、データベースからムービーレコードを再度読み取る必要はありません。</span><span class="sxs-lookup"><span data-stu-id="3e81c-169">You don't want to re-read the movie record from the database when the user clicks the **Delete Movie** button.</span></span> <span data-ttu-id="3e81c-170">そのため、ムービーを読み取るコードは、*要求が post 操作 (フォーム送信) でない場合*は、`if(!IsPost)` &mdash; というテスト内にあります。</span><span class="sxs-lookup"><span data-stu-id="3e81c-170">Therefore, code to read the movie is inside a test that says `if(!IsPost)` &mdash; that is, *if the request is not a post operation (form submission)*.</span></span>

## <a name="adding-code-to-delete-the-selected-movie"></a><span data-ttu-id="3e81c-171">選択したムービーを削除するコードの追加</span><span class="sxs-lookup"><span data-stu-id="3e81c-171">Adding Code to Delete the Selected Movie</span></span>

<span data-ttu-id="3e81c-172">ユーザーがボタンをクリックしたときにムービーを削除するには、`@` ブロックの右中かっこの内側に次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="3e81c-172">To delete the movie when the user clicks the button, add the following code just inside the closing brace of the `@` block:</span></span>

[!code-csharp[Main](deleting-data/samples/sample6.cs)]

<span data-ttu-id="3e81c-173">このコードは、既存のレコードを更新するためのコードに似ていますが、単純です。</span><span class="sxs-lookup"><span data-stu-id="3e81c-173">This code is similar to the code for updating an existing record, but simpler.</span></span> <span data-ttu-id="3e81c-174">このコードは、基本的に SQL `Delete` ステートメントを実行します。</span><span class="sxs-lookup"><span data-stu-id="3e81c-174">The code basically runs a SQL `Delete` statement.</span></span>

 <span data-ttu-id="3e81c-175">*Editmovie*ページと同様に、コードは `if(IsPost)` ブロックにあります。</span><span class="sxs-lookup"><span data-stu-id="3e81c-175">As in the *EditMovie* page, the code is in an `if(IsPost)` block.</span></span> <span data-ttu-id="3e81c-176">今回は、`if()` 条件は少し複雑になります。</span><span class="sxs-lookup"><span data-stu-id="3e81c-176">This time, the `if()` condition is a little more complicated:</span></span> 

[!code-csharp[Main](deleting-data/samples/sample7.cs)]

<span data-ttu-id="3e81c-177">ここでは2つの条件があります。</span><span class="sxs-lookup"><span data-stu-id="3e81c-177">There are two conditions here.</span></span> <span data-ttu-id="3e81c-178">1つ目は、`if(IsPost)`&mdash; 前に示したように、ページが送信されていることです。</span><span class="sxs-lookup"><span data-stu-id="3e81c-178">The first is that the page is being submitted, as you've seen before &mdash; `if(IsPost)`.</span></span>

<span data-ttu-id="3e81c-179">2番目の条件は `!Request["buttonDelete"].IsEmpty()`であり、要求に `buttonDelete`という名前のオブジェクトが含まれていることを意味します。</span><span class="sxs-lookup"><span data-stu-id="3e81c-179">The second condition is `!Request["buttonDelete"].IsEmpty()`, meaning that the request has an object named `buttonDelete`.</span></span> <span data-ttu-id="3e81c-180">確かに、フォームを送信したボタンをテストするための間接的な方法です。</span><span class="sxs-lookup"><span data-stu-id="3e81c-180">Admittedly, it's an indirect way of testing which button submitted the form.</span></span> <span data-ttu-id="3e81c-181">フォームに複数の [送信] ボタンが含まれている場合は、クリックされたボタンの名前だけが要求に表示されます。</span><span class="sxs-lookup"><span data-stu-id="3e81c-181">If a form contains multiple submit buttons, only the name of the button that was clicked appears in the request.</span></span> <span data-ttu-id="3e81c-182">したがって、論理的には、特定のボタンの名前が要求 &mdash; に表示される場合、またはコードに示されているように表示される場合、そのボタンが空でない場合は、フォームを送信したボタン &mdash; ます。</span><span class="sxs-lookup"><span data-stu-id="3e81c-182">Therefore, logically, if the name of a particular button appears in the request &mdash; or as stated in the code, if that button isn't empty &mdash; that's the button that submitted the form.</span></span>

<span data-ttu-id="3e81c-183">`&&` 演算子は、"and" (論理 AND) を意味します。</span><span class="sxs-lookup"><span data-stu-id="3e81c-183">The `&&` operator means "and" (logical AND).</span></span> <span data-ttu-id="3e81c-184">したがって、`if` 条件全体は...</span><span class="sxs-lookup"><span data-stu-id="3e81c-184">Therefore the entire `if` condition is ...</span></span>

<span data-ttu-id="3e81c-185">*この要求は post (初回要求ではありません) です*</span><span class="sxs-lookup"><span data-stu-id="3e81c-185">*This request is a post (not a first-time request)*</span></span>  
  
 <span data-ttu-id="3e81c-186">AND</span><span class="sxs-lookup"><span data-stu-id="3e81c-186">AND</span></span>  
  
<span data-ttu-id="3e81c-187">*`buttonDelete`ボタンは、* *フォームを送信したボタンでした。*</span><span class="sxs-lookup"><span data-stu-id="3e81c-187">*The* `buttonDelete`*button was the button that submitted the form.*</span></span>

<span data-ttu-id="3e81c-188">このフォーム (実際にはこのページ) には1つのボタンしか含まれていないため、`buttonDelete` に対する追加のテストは技術的には必要ありません。</span><span class="sxs-lookup"><span data-stu-id="3e81c-188">This form (in fact, this page) contains only one button, so the additional test for `buttonDelete` is technically not required.</span></span> <span data-ttu-id="3e81c-189">それでも、データを完全に削除する操作を実行しようとしています。</span><span class="sxs-lookup"><span data-stu-id="3e81c-189">Still, you're about to perform an operation that will permanently remove data.</span></span> <span data-ttu-id="3e81c-190">そのため、ユーザーが明示的に要求した場合にのみ操作を実行するようにします。</span><span class="sxs-lookup"><span data-stu-id="3e81c-190">So you want to be as sure as possible that you're performing the operation only when the user has explicitly requested it.</span></span> <span data-ttu-id="3e81c-191">たとえば、このページを後で展開し、その他のボタンを追加したとします。</span><span class="sxs-lookup"><span data-stu-id="3e81c-191">For example, suppose that you expanded this page later and added other buttons to it.</span></span> <span data-ttu-id="3e81c-192">それでも、ムービーを削除するコードは、[`buttonDelete`] ボタンがクリックされた場合にのみ実行されます。</span><span class="sxs-lookup"><span data-stu-id="3e81c-192">Even then, the code that deletes the movie will run only if the `buttonDelete` button was clicked.</span></span>

<span data-ttu-id="3e81c-193">[ *Editmovie* ] ページと同様に、非表示フィールドから ID を取得し、SQL コマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="3e81c-193">As in the *EditMovie* page, you get the ID from the hidden field and then run the SQL command.</span></span> <span data-ttu-id="3e81c-194">`Delete` ステートメントの構文は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="3e81c-194">The syntax for the `Delete` statement is:</span></span>

`DELETE FROM table WHERE ID = value`

<span data-ttu-id="3e81c-195">`WHERE` 句と ID を含めることが重要です。</span><span class="sxs-lookup"><span data-stu-id="3e81c-195">It's vital to include the `WHERE` clause and the ID.</span></span> <span data-ttu-id="3e81c-196">WHERE 句を省略すると、*テーブル内のすべてのレコードが削除され*ます。</span><span class="sxs-lookup"><span data-stu-id="3e81c-196">If you leave out the WHERE clause, *all the records in the table will be deleted*.</span></span> <span data-ttu-id="3e81c-197">ご覧のとおり、プレースホルダーを使用して、SQL コマンドに ID 値を渡します。</span><span class="sxs-lookup"><span data-stu-id="3e81c-197">As you have seen, you pass the ID value to the SQL command by using a placeholder.</span></span>

## <a name="testing-the-movie-delete-process"></a><span data-ttu-id="3e81c-198">ムービーの削除プロセスのテスト</span><span class="sxs-lookup"><span data-stu-id="3e81c-198">Testing the Movie Delete Process</span></span>

<span data-ttu-id="3e81c-199">これで、をテストできるようになりました。</span><span class="sxs-lookup"><span data-stu-id="3e81c-199">Now you can test.</span></span> <span data-ttu-id="3e81c-200">ムービーページを実行し、ムービーの横*にある [* **削除**] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="3e81c-200">Run the *Movies* page, and click **Delete** next to a movie.</span></span> <span data-ttu-id="3e81c-201">[ *DeleteMovie* ] ページが表示されたら、 **[ムービーの削除]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="3e81c-201">When the *DeleteMovie* page appears, click **Delete Movie**.</span></span>

![[ムービーの削除] ボタンが強調表示されているムービーページを削除する](deleting-data/_static/image4.png)

<span data-ttu-id="3e81c-203">このボタンをクリックすると、ムービーが削除され、ムービーの一覧に戻ります。</span><span class="sxs-lookup"><span data-stu-id="3e81c-203">When you click the button, the code deletes the movies and returns to the movie listing.</span></span> <span data-ttu-id="3e81c-204">削除したムービーを検索し、削除されたことを確認できます。</span><span class="sxs-lookup"><span data-stu-id="3e81c-204">There you can search for the deleted movie and confirm that it's been deleted.</span></span>

## <a name="coming-up-next"></a><span data-ttu-id="3e81c-205">次へ</span><span class="sxs-lookup"><span data-stu-id="3e81c-205">Coming Up Next</span></span>

<span data-ttu-id="3e81c-206">次のチュートリアルでは、サイトのすべてのページに共通の外観とレイアウトを提供する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="3e81c-206">The next tutorial shows you how to give all the pages on your site a common look and layout.</span></span>

## <a name="complete-listing-for-movie-page-updated-with-delete-links"></a><span data-ttu-id="3e81c-207">[ムービーの完全な一覧表示] ページ ([リンクの削除] で更新)</span><span class="sxs-lookup"><span data-stu-id="3e81c-207">Complete Listing for Movie Page (Updated with Delete Links)</span></span>

[!code-cshtml[Main](deleting-data/samples/sample8.cshtml)]

## <a name="complete-listing-for-deletemovie-page"></a><span data-ttu-id="3e81c-208">DeleteMovie ページの完全な一覧表示</span><span class="sxs-lookup"><span data-stu-id="3e81c-208">Complete Listing for DeleteMovie Page</span></span>

[!code-cshtml[Main](deleting-data/samples/sample9.cshtml)]

## <a name="additional-resources"></a><span data-ttu-id="3e81c-209">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="3e81c-209">Additional Resources</span></span>

- [<span data-ttu-id="3e81c-210">Razor 構文を使用した ASP.NET Web プログラミングの概要</span><span class="sxs-lookup"><span data-stu-id="3e81c-210">Introduction to ASP.NET Web Programming by Using the Razor Syntax</span></span>](../introducing-razor-syntax-c.md)
- <span data-ttu-id="3e81c-211">W3Schools サイトでの[SQL DELETE ステートメント](http://www.w3schools.com/sql/sql_delete.asp)</span><span class="sxs-lookup"><span data-stu-id="3e81c-211">[SQL DELETE Statement](http://www.w3schools.com/sql/sql_delete.asp) on the W3Schools site</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="3e81c-212">[前へ](updating-data.md)
> [次へ](layouts.md)</span><span class="sxs-lookup"><span data-stu-id="3e81c-212">[Previous](updating-data.md)
[Next](layouts.md)</span></span>
