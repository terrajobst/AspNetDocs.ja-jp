---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/entering-data
title: ASP.NET Web ページの概要-Forms | を使用したデータベースデータの入力 |Microsoft Docs
author: Rick-Anderson
description: このチュートリアルでは、ASP.NET Web ページ (... を使用する場合に、入力フォームを作成し、フォームから取得したデータをデータベーステーブルに入力する方法について説明します。
ms.author: riande
ms.date: 05/28/2015
ms.assetid: d37c93fc-25fd-4e94-8671-0d437beef206
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/entering-data
msc.type: authoredcontent
ms.openlocfilehash: b9354a7b97a7df9020a681f709e16a92650cfcf0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78506602"
---
# <a name="introducing-aspnet-web-pages---entering-database-data-by-using-forms"></a><span data-ttu-id="46bb3-103">ASP.NET Web ページの概要-フォームを使用してデータベースデータを入力する</span><span class="sxs-lookup"><span data-stu-id="46bb3-103">Introducing ASP.NET Web Pages - Entering Database Data by Using Forms</span></span>

<span data-ttu-id="46bb3-104">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="46bb3-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="46bb3-105">このチュートリアルでは、ASP.NET Web ページ (Razor) を使用するときに、入力フォームを作成し、フォームから取得したデータをデータベーステーブルに入力する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="46bb3-105">This tutorial shows you how to create an entry form and then enter the data that you get from the form into a database table when you use ASP.NET Web Pages (Razor).</span></span> <span data-ttu-id="46bb3-106">[ASP.NET Web ページの HTML フォームの基本](https://go.microsoft.com/fwlink/?LinkId=251581)を通じてシリーズを完了していることを前提としています。</span><span class="sxs-lookup"><span data-stu-id="46bb3-106">It assumes you have completed the series through [Basics of HTML Forms in ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=251581).</span></span>
> 
> <span data-ttu-id="46bb3-107">ここでは、次の内容について学習します。</span><span class="sxs-lookup"><span data-stu-id="46bb3-107">What you'll learn:</span></span>
> 
> - <span data-ttu-id="46bb3-108">入力フォームを処理する方法の詳細については、こちらを参照してください。</span><span class="sxs-lookup"><span data-stu-id="46bb3-108">More about how to process entry forms.</span></span>
> - <span data-ttu-id="46bb3-109">データベースにデータを追加 (挿入) する方法。</span><span class="sxs-lookup"><span data-stu-id="46bb3-109">How to add (insert) data in a database.</span></span>
> - <span data-ttu-id="46bb3-110">ユーザーがフォームに必須の値 (ユーザー入力の検証方法) を入力したことを確認する方法。</span><span class="sxs-lookup"><span data-stu-id="46bb3-110">How to make sure that users have entered a required value in a form (how to validate user input).</span></span>
> - <span data-ttu-id="46bb3-111">検証エラーを表示する方法。</span><span class="sxs-lookup"><span data-stu-id="46bb3-111">How to display validation errors.</span></span>
> - <span data-ttu-id="46bb3-112">現在のページから別のページに移動する方法。</span><span class="sxs-lookup"><span data-stu-id="46bb3-112">How to jump to another page from the current page.</span></span>
>   
> 
> <span data-ttu-id="46bb3-113">説明する機能/テクノロジ:</span><span class="sxs-lookup"><span data-stu-id="46bb3-113">Features/technologies discussed:</span></span>
> 
> - <span data-ttu-id="46bb3-114">`Database.Execute` メソッド。</span><span class="sxs-lookup"><span data-stu-id="46bb3-114">The `Database.Execute` method.</span></span>
> - <span data-ttu-id="46bb3-115">SQL `Insert Into` ステートメント</span><span class="sxs-lookup"><span data-stu-id="46bb3-115">The SQL `Insert Into` statement</span></span>
> - <span data-ttu-id="46bb3-116">`Validation` ヘルパー。</span><span class="sxs-lookup"><span data-stu-id="46bb3-116">The `Validation` helper.</span></span>
> - <span data-ttu-id="46bb3-117">`Response.Redirect` メソッド。</span><span class="sxs-lookup"><span data-stu-id="46bb3-117">The `Response.Redirect` method.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="46bb3-118">作成するアプリケーション:</span><span class="sxs-lookup"><span data-stu-id="46bb3-118">What You'll Build</span></span>

<span data-ttu-id="46bb3-119">前のチュートリアルでは、データベースを作成する方法を説明しました。 WebMatrix でデータベースを直接編集してデータベースデータを入力し、**データベース**ワークスペースで作業していました。</span><span class="sxs-lookup"><span data-stu-id="46bb3-119">In the tutorial earlier that showed you how to create a database, you entered database data by editing the database directly in WebMatrix, working in the **Database** workspace.</span></span> <span data-ttu-id="46bb3-120">ただし、ほとんどのアプリでは、データベースにデータを格納するのは実用的な方法ではありません。</span><span class="sxs-lookup"><span data-stu-id="46bb3-120">In most apps, that's not a practical way to put data into the database, though.</span></span> <span data-ttu-id="46bb3-121">このチュートリアルでは、web ベースのインターフェイスを作成して、ユーザーまたはユーザーがデータを入力してデータベースに保存できるようにします。</span><span class="sxs-lookup"><span data-stu-id="46bb3-121">So in this tutorial, you'll create a web-based interface that lets you or anyone enter data and save it to the database.</span></span>

<span data-ttu-id="46bb3-122">新しいムービーを入力できるページを作成します。</span><span class="sxs-lookup"><span data-stu-id="46bb3-122">You'll create a page where you can enter new movies.</span></span> <span data-ttu-id="46bb3-123">このページには、フィールド (テキストボックス) を含む入力フォームが含まれます。このフォームでは、ムービーのタイトル、ジャンル、および年を入力できます。</span><span class="sxs-lookup"><span data-stu-id="46bb3-123">The page will contain an entry form that has fields (text boxes) where you can enter a movie title, genre, and year.</span></span> <span data-ttu-id="46bb3-124">ページは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="46bb3-124">The page will look like this page:</span></span>

![ブラウザーでの [ムービーの追加] ページ](entering-data/_static/image1.png)

<span data-ttu-id="46bb3-126">テキストボックスは、次のマークアップのように表示される HTML `<input>` 要素になります。</span><span class="sxs-lookup"><span data-stu-id="46bb3-126">The text boxes will be HTML `<input>` elements that will look like this markup:</span></span>

`<input type="text" name="genre" value="" />`

## <a name="creating-the-basic-entry-form"></a><span data-ttu-id="46bb3-127">基本的な入力フォームの作成</span><span class="sxs-lookup"><span data-stu-id="46bb3-127">Creating the Basic Entry Form</span></span>

<span data-ttu-id="46bb3-128">*Addmovie. cshtml*という名前のページを作成します。</span><span class="sxs-lookup"><span data-stu-id="46bb3-128">Create a page named *AddMovie.cshtml*.</span></span>

<span data-ttu-id="46bb3-129">ファイルの内容を次のマークアップに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="46bb3-129">Replace what's in the file with the following markup.</span></span> <span data-ttu-id="46bb3-130">すべてを上書きします。コードブロックは、すぐに先頭に追加します。</span><span class="sxs-lookup"><span data-stu-id="46bb3-130">Overwrite everything; you'll add a code block at the top shortly.</span></span>

[!code-cshtml[Main](entering-data/samples/sample1.cshtml)]

<span data-ttu-id="46bb3-131">この例は、フォームを作成するための一般的な HTML を示しています。</span><span class="sxs-lookup"><span data-stu-id="46bb3-131">This example shows typical HTML for creating a form.</span></span> <span data-ttu-id="46bb3-132">この例では、テキストボックスと [送信] ボタンに `<input>` 要素を使用しています。</span><span class="sxs-lookup"><span data-stu-id="46bb3-132">It uses `<input>` elements for the text boxes and for the submit button.</span></span> <span data-ttu-id="46bb3-133">テキストボックスのキャプションは、標準の `<label>` 要素を使用して作成されます。</span><span class="sxs-lookup"><span data-stu-id="46bb3-133">The captions for the text boxes are created by using standard `<label>` elements.</span></span> <span data-ttu-id="46bb3-134">`<fieldset>` 要素と `<legend>` 要素は、フォームの周囲に便利なボックスを配置します。</span><span class="sxs-lookup"><span data-stu-id="46bb3-134">The `<fieldset>` and `<legend>` elements put a nice box around the form.</span></span>

<span data-ttu-id="46bb3-135">このページの `<form>` 要素では、`method` 属性の値として `post` が使用されていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="46bb3-135">Notice that in this page, the `<form>` element uses `post` as the value for the `method` attribute.</span></span> <span data-ttu-id="46bb3-136">前のチュートリアルでは、`get` メソッドを使用するフォームを作成しました。</span><span class="sxs-lookup"><span data-stu-id="46bb3-136">In the previous tutorial, you created a form that used the `get` method.</span></span> <span data-ttu-id="46bb3-137">これは正しいことです。フォームがサーバーに値を送信しましたが、要求では何も変更されていません。</span><span class="sxs-lookup"><span data-stu-id="46bb3-137">That was correct, because although the form submitted values to the server, the request did not make any changes.</span></span> <span data-ttu-id="46bb3-138">これまでは、さまざまな方法でデータをフェッチしました。</span><span class="sxs-lookup"><span data-stu-id="46bb3-138">All it did was fetch data in different ways.</span></span> <span data-ttu-id="46bb3-139">ただし、このページで*は*変更を行います。新しいデータベースレコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="46bb3-139">However, in this page you *will* make changes—you're going to add new database records.</span></span> <span data-ttu-id="46bb3-140">したがって、このフォームでは `post` メソッドを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="46bb3-140">Therefore, this form should use the `post` method.</span></span> <span data-ttu-id="46bb3-141">(`GET` 操作と `POST` 操作の違いの詳細については、前のチュートリアルの「[GET、POST、および HTTP 動詞の安全性](https://go.microsoft.com/fwlink/?LinkId=251581#GET,_POST,_and_HTTP_Verb_Safety)に関する補足記事」を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="46bb3-141">(For more about the difference between `GET` and `POST` operations, see the[GET, POST, and HTTP Verb Safety](https://go.microsoft.com/fwlink/?LinkId=251581#GET,_POST,_and_HTTP_Verb_Safety) sidebar in the previous tutorial.)</span></span>

<span data-ttu-id="46bb3-142">各テキストボックスには `name` 要素 (`title`、`genre`、`year`) があることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="46bb3-142">Note that each text box has a `name` element (`title`, `genre`, `year`).</span></span> <span data-ttu-id="46bb3-143">前のチュートリアルで見たように、これらの名前は、後でユーザーの入力を取得できるようにする必要があるため、重要です。</span><span class="sxs-lookup"><span data-stu-id="46bb3-143">As you saw in the previous tutorial, these names are important because you must have those names so you can get the user's input later.</span></span> <span data-ttu-id="46bb3-144">任意の名前を使用できます。</span><span class="sxs-lookup"><span data-stu-id="46bb3-144">You can use any names.</span></span> <span data-ttu-id="46bb3-145">意味のある名前を使用して、使用しているデータを思い出すのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="46bb3-145">It's helpful to use meaningful names that help you remember what data you're working with.</span></span>

<span data-ttu-id="46bb3-146">各 `<input>` 要素の `value` 属性には、いくつかの Razor コード (たとえば、`Request.Form["title"]`) が含まれています。</span><span class="sxs-lookup"><span data-stu-id="46bb3-146">The `value` attribute of each `<input>` element contains a bit of Razor code (for example, `Request.Form["title"]`).</span></span> <span data-ttu-id="46bb3-147">フォームが送信された後にテキストボックスに入力した値 (存在する場合) を保持するために、前のチュートリアルでこのトリックのバージョンを学習しました。</span><span class="sxs-lookup"><span data-stu-id="46bb3-147">You learned a version of this trick in the previous tutorial to preserve the value entered into the text box (if any) after the form has been submitted.</span></span>

## <a name="getting-the-form-values"></a><span data-ttu-id="46bb3-148">フォーム値の取得</span><span class="sxs-lookup"><span data-stu-id="46bb3-148">Getting the Form Values</span></span>

<span data-ttu-id="46bb3-149">次に、フォームを処理するコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="46bb3-149">Next, you add code that processes the form.</span></span> <span data-ttu-id="46bb3-150">概要では、次の操作を行います。</span><span class="sxs-lookup"><span data-stu-id="46bb3-150">In outline, you'll do the following:</span></span>

1. <span data-ttu-id="46bb3-151">ページが投稿されている (送信された) かどうかを確認します。</span><span class="sxs-lookup"><span data-stu-id="46bb3-151">Check whether the page is being posted (was submitted).</span></span> <span data-ttu-id="46bb3-152">ユーザーがボタンをクリックしたときにのみコードを実行する場合は、ページが最初に実行されるときではなく、コードを実行します。</span><span class="sxs-lookup"><span data-stu-id="46bb3-152">You want to your code to run only when users have clicked the button, not when the page first runs.</span></span>
2. <span data-ttu-id="46bb3-153">ユーザーがテキストボックスに入力した値を取得します。</span><span class="sxs-lookup"><span data-stu-id="46bb3-153">Get the values that the user entered into the text boxes.</span></span> <span data-ttu-id="46bb3-154">この場合、フォームは `POST` 動詞を使用しているため、`Request.Form` コレクションからフォーム値を取得します。</span><span class="sxs-lookup"><span data-stu-id="46bb3-154">In this case, because the form is using the `POST` verb, you get the form values from the `Request.Form` collection.</span></span>
3. <span data-ttu-id="46bb3-155">新しいレコードとして、*ムービー*データベーステーブルに値を挿入します。</span><span class="sxs-lookup"><span data-stu-id="46bb3-155">Insert the values as a new record in the *Movies* database table.</span></span>

<span data-ttu-id="46bb3-156">ファイルの先頭に次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="46bb3-156">At the top of the file, add the following code:</span></span>

[!code-cshtml[Main](entering-data/samples/sample2.cshtml)]

<span data-ttu-id="46bb3-157">最初の数行では、テキストボックスの値を保持するために、変数 (`title`、`genre`、および `year`) を作成します。</span><span class="sxs-lookup"><span data-stu-id="46bb3-157">The first few lines create variables (`title`, `genre`, and `year`) to hold the values from the text boxes.</span></span> <span data-ttu-id="46bb3-158">行 `if(IsPost)` は、ユーザーが **[ムービーの追加]** ボタンをクリックしたとき (つまり、フォームがポストされたとき) に*のみ*変数が設定されるようにします。</span><span class="sxs-lookup"><span data-stu-id="46bb3-158">The line `if(IsPost)` makes sure that the variables are set *only* when users click the **Add Movie** button — that is, when the form has been posted.</span></span>

<span data-ttu-id="46bb3-159">前のチュートリアルで見たように、`Request.Form["name"]`のような式を使用してテキストボックスの値を取得します。ここで、 *name*は `<input>` 要素の名前です。</span><span class="sxs-lookup"><span data-stu-id="46bb3-159">As you saw in an earlier tutorial, you get the value of a text box by using an expression like `Request.Form["name"]`, where *name* is the name of the `<input>` element.</span></span>

<span data-ttu-id="46bb3-160">変数の名前 (`title`、`genre`、および `year`) は任意です。</span><span class="sxs-lookup"><span data-stu-id="46bb3-160">The names of the variables (`title`, `genre`, and `year`) are arbitrary.</span></span> <span data-ttu-id="46bb3-161">`<input>` 要素に割り当てる名前と同様に、任意の要素を呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="46bb3-161">Like the names that you assign to `<input>` elements, you can call them anything you like.</span></span> <span data-ttu-id="46bb3-162">(変数の名前は、フォームの `<input>` 要素の name 属性と一致する必要はありません)。ただし、`<input>` の要素と同様に、変数名に含まれるデータを反映する変数名を使用することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="46bb3-162">(The names of the variables don't have to match the name attributes of `<input>` elements on the form.) But as with the `<input>` elements, it's a good idea to use variable names that reflect the data that they contain.</span></span> <span data-ttu-id="46bb3-163">コードを記述すると、一貫性のある名前を使用すると、使用しているデータを簡単に思い出すことができます。</span><span class="sxs-lookup"><span data-stu-id="46bb3-163">When you write code, consistent names make it easier for you to remember what data you're working with.</span></span>

## <a name="adding-data-to-the-database"></a><span data-ttu-id="46bb3-164">データベースへのデータの追加</span><span class="sxs-lookup"><span data-stu-id="46bb3-164">Adding Data to the Database</span></span>

<span data-ttu-id="46bb3-165">追加したコードブロックで、`if` ブロックの右中かっこ (`}`) の*内側*に (コードブロックの内部だけではなく)、次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="46bb3-165">In the code block you just added, just *inside* the closing brace ( `}` ) of the `if` block (not just inside the code block), add the following code:</span></span>

[!code-csharp[Main](entering-data/samples/sample3.cs)]

<span data-ttu-id="46bb3-166">この例は、前のチュートリアルでデータをフェッチして表示するために使用したコードに似ています。</span><span class="sxs-lookup"><span data-stu-id="46bb3-166">This example is similar to the code you used in a previous tutorial to fetch and display data.</span></span> <span data-ttu-id="46bb3-167">`db =` で始まる行は、前のようにデータベースを開き、次の行では前述のように SQL ステートメントを定義します。</span><span class="sxs-lookup"><span data-stu-id="46bb3-167">The line that starts with `db =` opens the database, like before, and the next line defines a SQL statement, again as you saw before.</span></span> <span data-ttu-id="46bb3-168">ただし今回は、SQL `Insert Into` ステートメントを定義します。</span><span class="sxs-lookup"><span data-stu-id="46bb3-168">However, this time it defines a SQL `Insert Into` statement.</span></span> <span data-ttu-id="46bb3-169">次の例は、`Insert Into` ステートメントの一般的な構文を示しています。</span><span class="sxs-lookup"><span data-stu-id="46bb3-169">The following example shows the general syntax of the `Insert Into` statement:</span></span>

`INSERT INTO table (column1, column2, column3, ...) VALUES (value1, value2, value3, ...)`

<span data-ttu-id="46bb3-170">つまり、挿入するテーブルを指定し、挿入する列を一覧表示して、挿入する値を一覧表示します。</span><span class="sxs-lookup"><span data-stu-id="46bb3-170">In other words, you specify the table to insert into, then list the columns to insert into, and then list the values to insert.</span></span> <span data-ttu-id="46bb3-171">(前述のように、SQL では大文字と小文字は区別されませんが、コマンドを読みやすくするためにキーワードを大文字にすることがあります)。</span><span class="sxs-lookup"><span data-stu-id="46bb3-171">(As noted before, SQL is not case sensitive but some people capitalize the keywords to make it easier to read the command.)</span></span>

<span data-ttu-id="46bb3-172">挿入しようとしている列は、コマンドの `(Title, Genre, Year)`に既に表示されています。</span><span class="sxs-lookup"><span data-stu-id="46bb3-172">The columns that you're inserting into are already listed in the command — `(Title, Genre, Year)`.</span></span> <span data-ttu-id="46bb3-173">興味深いのは、テキストボックスからコマンドの `VALUES` 部分に値を取得する方法です。</span><span class="sxs-lookup"><span data-stu-id="46bb3-173">The interesting part is how you get the values from the text boxes into the `VALUES` part of the command.</span></span> <span data-ttu-id="46bb3-174">実際の値の代わりに、`@0`、`@1`、および `@2`が表示されます。これは当然のプレースホルダーです。</span><span class="sxs-lookup"><span data-stu-id="46bb3-174">Instead of actual values, you see `@0`, `@1`, and `@2`, which are of course placeholders.</span></span> <span data-ttu-id="46bb3-175">コマンド (`db.Execute` 行) を実行すると、テキストボックスから受け取った値が渡されます。</span><span class="sxs-lookup"><span data-stu-id="46bb3-175">When you run the command (on the `db.Execute` line), you pass the values that you got from the text boxes.</span></span>

<span data-ttu-id="46bb3-176">**重要!**</span><span class="sxs-lookup"><span data-stu-id="46bb3-176">**Important!**</span></span> <span data-ttu-id="46bb3-177">SQL ステートメントでユーザーがオンラインで入力したデータを含める唯一の方法は、ここで説明するようにプレースホルダーを使用することです (`VALUES(@0, @1, @2)`)。</span><span class="sxs-lookup"><span data-stu-id="46bb3-177">Remember that the only way you should ever include data entered online by a user in a SQL statement is to use placeholders, as you see here (`VALUES(@0, @1, @2)`).</span></span> <span data-ttu-id="46bb3-178">ユーザー入力を SQL ステートメントに連結する場合は、「 [ASP.NET Web ページの基本フォーム](https://go.microsoft.com/fwlink/?LinkId=251581)」 (前のチュートリアル) で説明されているように、sql インジェクション攻撃を受けます。</span><span class="sxs-lookup"><span data-stu-id="46bb3-178">If you concatenate user input into a SQL statement, you open yourself to a SQL injection attack, as explained in [Form Basics in ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=251581) (the previous tutorial).</span></span>

<span data-ttu-id="46bb3-179">`if` ブロックの内部で、`db.Execute` 行の後に次の行を追加します。</span><span class="sxs-lookup"><span data-stu-id="46bb3-179">Still inside the `if` block, add the following line after the `db.Execute` line:</span></span>

[!code-css[Main](entering-data/samples/sample4.css)]

<span data-ttu-id="46bb3-180">新しいムービーがデータベースに挿入された後、この行に移動して (リダイレクト) *、ムービーページに*移動します。これにより、先ほど入力したムービーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="46bb3-180">After the new movie has been inserted into the database, this line jumps you (redirects) to the *Movies* page so you can see the movie you just entered.</span></span> <span data-ttu-id="46bb3-181">`~` 演算子は、"web サイトのルート" を意味します。</span><span class="sxs-lookup"><span data-stu-id="46bb3-181">The `~` operator means "root of the website."</span></span> <span data-ttu-id="46bb3-182">(`~` 演算子は、HTML ではなく ASP.NET ページでのみ機能します)。</span><span class="sxs-lookup"><span data-stu-id="46bb3-182">(The `~` operator works only in ASP.NET pages, not in HTML generally.)</span></span>

<span data-ttu-id="46bb3-183">完全なコードブロックは、次の例のようになります。</span><span class="sxs-lookup"><span data-stu-id="46bb3-183">The complete code block looks like this example:</span></span>

[!code-cshtml[Main](entering-data/samples/sample5.cshtml)]

## <a name="testing-the-insert-command-so-far"></a><span data-ttu-id="46bb3-184">挿入コマンドのテスト (これまで)</span><span class="sxs-lookup"><span data-stu-id="46bb3-184">Testing the Insert Command (So Far)</span></span>

<span data-ttu-id="46bb3-185">まだ完了していませんが、テストには時間がかかるようになりました。</span><span class="sxs-lookup"><span data-stu-id="46bb3-185">You're not done yet, but now is a good time to test.</span></span>

<span data-ttu-id="46bb3-186">WebMatrix のファイルのツリービューで、[ *Addmovie. cshtml* ] ページを右クリックし、 **[ブラウザーで起動]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="46bb3-186">In the tree view of files in WebMatrix, right-click the *AddMovie.cshtml* page and then click **Launch in browser**.</span></span>

![ブラウザーでの [ムービーの追加] ページ](entering-data/_static/image2.png)

<span data-ttu-id="46bb3-188">(ブラウザーに別のページが表示された場合は、URL が `http://localhost:nnnnn/AddMovie`) であることを確認してください *。ここで、"は、* 使用しているポート番号です。"</span><span class="sxs-lookup"><span data-stu-id="46bb3-188">(If you end up with a different page in the browser, make sure that the URL is `http://localhost:nnnnn/AddMovie`), where *nnnnn* is the port number that you're using.)</span></span>

<span data-ttu-id="46bb3-189">エラーページを表示しましたか?</span><span class="sxs-lookup"><span data-stu-id="46bb3-189">Did you get an error page?</span></span> <span data-ttu-id="46bb3-190">その場合は、それを注意深く読んで、コードが前に示したものと正確に一致していることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="46bb3-190">If so, read it carefully and make sure that the code looks exactly what was listed earlier.</span></span>

<span data-ttu-id="46bb3-191">&mdash; の形式でムービーを入力します。たとえば、"Kane"、"ドラマ"、"1941" を使用します。</span><span class="sxs-lookup"><span data-stu-id="46bb3-191">Enter a movie in the form &mdash; for example, use "Citizen Kane", "Drama", and "1941".</span></span> <span data-ttu-id="46bb3-192">(または任意のもの) **[ムービーの追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="46bb3-192">(Or whatever.) Then click **Add Movie**.</span></span>

<span data-ttu-id="46bb3-193">すべてうまくいくと、*ムービー*ページにリダイレクトされます。</span><span class="sxs-lookup"><span data-stu-id="46bb3-193">If all goes well, you're redirected to the *Movies* page.</span></span> <span data-ttu-id="46bb3-194">新しいムービーが表示されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="46bb3-194">Make sure that your new movie is listed.</span></span>

![新しく追加されたムービーを示すムービーページ](entering-data/_static/image3.png)

## <a name="validating-user-input"></a><span data-ttu-id="46bb3-196">ユーザー入力の検証</span><span class="sxs-lookup"><span data-stu-id="46bb3-196">Validating User Input</span></span>

<span data-ttu-id="46bb3-197">*Addmovie*ページに戻り、もう一度実行します。</span><span class="sxs-lookup"><span data-stu-id="46bb3-197">Go back to the *AddMovie* page, or run it again.</span></span> <span data-ttu-id="46bb3-198">別のムービーを入力しますが、今回はタイトルだけを入力し &mdash; たとえば、雨に「Singin' と入力します。</span><span class="sxs-lookup"><span data-stu-id="46bb3-198">Enter another movie, but this time, enter only the title &mdash; for example, enter "Singin' in the Rain".</span></span> <span data-ttu-id="46bb3-199">**[ムービーの追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="46bb3-199">Then click **Add Movie**.</span></span>

<span data-ttu-id="46bb3-200">もう一度*ムービー*ページにリダイレクトされます。</span><span class="sxs-lookup"><span data-stu-id="46bb3-200">You're redirected to the *Movies* page again.</span></span> <span data-ttu-id="46bb3-201">新しいムービーは検索できますが、完全ではありません。</span><span class="sxs-lookup"><span data-stu-id="46bb3-201">You can find the new movie, but it's incomplete.</span></span>

![値が不足している新しいムービーを示すムービーページ](entering-data/_static/image4.png)

<span data-ttu-id="46bb3-203">*ムービー*テーブルを作成したときに、どのフィールドも null にできないと明示的に言いました。</span><span class="sxs-lookup"><span data-stu-id="46bb3-203">When you created the *Movies* table, you explicitly said that none of the fields could be null.</span></span> <span data-ttu-id="46bb3-204">ここには新しい映画の入力フォームがあり、フィールドを空白のままにしています。</span><span class="sxs-lookup"><span data-stu-id="46bb3-204">Here you have an entry form for new movies, and you're leaving fields blank.</span></span> <span data-ttu-id="46bb3-205">これはエラーです。</span><span class="sxs-lookup"><span data-stu-id="46bb3-205">That's an error.</span></span>

<span data-ttu-id="46bb3-206">この場合、データベースはエラーを実際には発生 (または*スロー*) しませんでした。</span><span class="sxs-lookup"><span data-stu-id="46bb3-206">In this case, the database didn't actually raise (or *throw*) an error.</span></span> <span data-ttu-id="46bb3-207">ジャンルまたは年を指定していないため、 *Addmovie*ページのコードでは、これらの値がいわゆる*空の文字列*として扱われます。</span><span class="sxs-lookup"><span data-stu-id="46bb3-207">You didn't supply a genre or year, so the code in the *AddMovie* page treated those values as so-called *empty strings*.</span></span> <span data-ttu-id="46bb3-208">SQL `Insert Into` コマンドの実行時に、ジャンルと年のフィールドには有用なデータが含まれていませんでしたが、これらは null ではありませんでした。</span><span class="sxs-lookup"><span data-stu-id="46bb3-208">When the SQL `Insert Into` command ran, the genre and year fields didn't have useful data in them, but they weren't null.</span></span>

<span data-ttu-id="46bb3-209">当然ながら、ユーザーが半空のムービー情報をデータベースに入力できないようにしたいと考えています。</span><span class="sxs-lookup"><span data-stu-id="46bb3-209">Obviously, you don't want to let users enter half-empty movie information into the database.</span></span> <span data-ttu-id="46bb3-210">解決策は、ユーザーの入力を検証することです。</span><span class="sxs-lookup"><span data-stu-id="46bb3-210">The solution is to validate the user's input.</span></span> <span data-ttu-id="46bb3-211">最初に、検証では、ユーザーがすべてのフィールドに対して値を入力したことを確認します (つまり、すべてのフィールドに空の文字列が含まれているわけではありません)。</span><span class="sxs-lookup"><span data-stu-id="46bb3-211">Initially, the validation will simply make sure that the user has entered a value for all of the fields (that is, that none of them contains an empty string).</span></span>

> [!TIP]
> 
> <span data-ttu-id="46bb3-212">**Null および空の文字列**</span><span class="sxs-lookup"><span data-stu-id="46bb3-212">**Null and Empty Strings**</span></span>
> 
> <span data-ttu-id="46bb3-213">プログラミングでは、"値なし" の異なる概念を区別しています。</span><span class="sxs-lookup"><span data-stu-id="46bb3-213">In programming, there's a distinction between different notions of "no value."</span></span> <span data-ttu-id="46bb3-214">一般に、値が何も設定または初期化されていない場合は、 *null*になります。</span><span class="sxs-lookup"><span data-stu-id="46bb3-214">In general, a value is *null* if it has never been set or initialized in any way.</span></span> <span data-ttu-id="46bb3-215">これに対し、文字データ (文字列) を必要とする変数は、*空の文字列*に設定できます。</span><span class="sxs-lookup"><span data-stu-id="46bb3-215">In contrast, a variable that expects character data (strings) can be set to an *empty string*.</span></span> <span data-ttu-id="46bb3-216">この場合、値は null ではありません。長さが0の文字列に明示的に設定されているだけです。</span><span class="sxs-lookup"><span data-stu-id="46bb3-216">In that case, the value is not null; it's just been explicitly set to a string of characters whose length is zero.</span></span> <span data-ttu-id="46bb3-217">次の2つのステートメントは、違いを示しています。</span><span class="sxs-lookup"><span data-stu-id="46bb3-217">These two statements show the difference:</span></span>
> 
> [!code-csharp[Main](entering-data/samples/sample6.cs)]
> 
> <span data-ttu-id="46bb3-218">これは少し複雑ですが、重要な点は、`null` が未確定の状態を表すことです。</span><span class="sxs-lookup"><span data-stu-id="46bb3-218">It's a little more complicated than that, but the important point is that `null` represents a sort of undetermined state.</span></span>
> 
> <span data-ttu-id="46bb3-219">次に、値が null で、空の文字列であるかを正確に理解しておくことが重要です。</span><span class="sxs-lookup"><span data-stu-id="46bb3-219">Now and then it's important to understand exactly when a value is null and when it's just an empty string.</span></span> <span data-ttu-id="46bb3-220">[ *Addmovie* ] ページのコードでは、`Request.Form["title"]` を使用してテキストボックスの値を取得します。</span><span class="sxs-lookup"><span data-stu-id="46bb3-220">In the code for the *AddMovie* page, you get the values of the text boxes by using `Request.Form["title"]` and so on.</span></span> <span data-ttu-id="46bb3-221">ページが最初に実行されたとき (ボタンをクリックする前) に、`Request.Form["title"]` の値が null になります。</span><span class="sxs-lookup"><span data-stu-id="46bb3-221">When the page first runs (before you click the button), the value of `Request.Form["title"]` is null.</span></span> <span data-ttu-id="46bb3-222">ただし、フォームを送信すると、`Request.Form["title"]` `title` テキストボックスの値が取得されます。</span><span class="sxs-lookup"><span data-stu-id="46bb3-222">But when you submit the form, `Request.Form["title"]` gets the value of the `title` text box.</span></span> <span data-ttu-id="46bb3-223">明らかではありませんが、空のテキストボックスは null ではありません。空の文字列が含まれているだけです。</span><span class="sxs-lookup"><span data-stu-id="46bb3-223">It's not obvious, but an empty text box is not null; it just has an empty string in it.</span></span> <span data-ttu-id="46bb3-224">そのため、ボタンクリックに応答してコードを実行すると、`Request.Form["title"]` に空の文字列が含まれます。</span><span class="sxs-lookup"><span data-stu-id="46bb3-224">So when the code runs in response to the button click, `Request.Form["title"]` has an empty string in it.</span></span>
> 
> <span data-ttu-id="46bb3-225">この区別が重要なのはなぜですか。</span><span class="sxs-lookup"><span data-stu-id="46bb3-225">Why is this distinction important?</span></span> <span data-ttu-id="46bb3-226">*ムービー*テーブルを作成したときに、どのフィールドも null にできないと明示的に言いました。</span><span class="sxs-lookup"><span data-stu-id="46bb3-226">When you created the *Movies* table, you explicitly said that none of the fields could be null.</span></span> <span data-ttu-id="46bb3-227">しかし、ここでは新しい映画の入力フォームがあり、フィールドを空白のままにしています。</span><span class="sxs-lookup"><span data-stu-id="46bb3-227">But here you have an entry form for new movies, and you're leaving fields blank.</span></span> <span data-ttu-id="46bb3-228">ジャンルまたは年の値がない新しいムービーを保存しようとしたときに、データベースが文句を言います。</span><span class="sxs-lookup"><span data-stu-id="46bb3-228">You would reasonably expect the database to complain when you tried to save new movies that didn't have values for genre or year.</span></span> <span data-ttu-id="46bb3-229">しかし、そのようなテキストボックスを空白のままにしても、値が null ではない場合でも、これは &mdash; です。これらは空の文字列です。</span><span class="sxs-lookup"><span data-stu-id="46bb3-229">But that's the point &mdash; even if you leave those text boxes blank, the values aren't null; they're empty strings.</span></span> <span data-ttu-id="46bb3-230">その結果、これらの列が null ではなく &mdash; 空で、データベースに新しいムービーを保存できるようになります。</span><span class="sxs-lookup"><span data-stu-id="46bb3-230">As a result, you're able to save new movies to the database with these columns empty &mdash; but not null!</span></span> <span data-ttu-id="46bb3-231">&mdash; 値。</span><span class="sxs-lookup"><span data-stu-id="46bb3-231">&mdash; values.</span></span> <span data-ttu-id="46bb3-232">そのため、ユーザーが空の文字列を送信しないようにする必要があります。これは、ユーザーの入力を検証することによって行うことができます。</span><span class="sxs-lookup"><span data-stu-id="46bb3-232">Therefore, you have to make sure that users don't submit an empty string, which you can do by validating the user's input.</span></span>

### <a name="the-validation-helper"></a><span data-ttu-id="46bb3-233">検証ヘルパー</span><span class="sxs-lookup"><span data-stu-id="46bb3-233">The Validation Helper</span></span>

<span data-ttu-id="46bb3-234">ASP.NET Web ページには、ユーザーが要件を満たすデータを確実に入力できるようにするために使用できる、`Validation` helper &mdash; のヘルパー &mdash; が含まれています。</span><span class="sxs-lookup"><span data-stu-id="46bb3-234">ASP.NET Web Pages includes a helper &mdash; the `Validation` helper &mdash; that you can use to make sure that users enter data that meets your requirements.</span></span> <span data-ttu-id="46bb3-235">`Validation` helper は、ASP.NET Web ページに組み込まれているヘルパーの1つであるため、前のチュートリアルで Gravatar helper をインストールしたのと同じ方法で、NuGet を使用してパッケージとしてインストールする必要はありません。</span><span class="sxs-lookup"><span data-stu-id="46bb3-235">The `Validation` helper is one of the helpers that's built in to ASP.NET Web Pages, so you don't have to install it as a package by using NuGet, the way you installed the Gravatar helper in an earlier tutorial.</span></span>

<span data-ttu-id="46bb3-236">ユーザーの入力を検証するには、次の操作を行います。</span><span class="sxs-lookup"><span data-stu-id="46bb3-236">To validate the user's input, you'll do the following:</span></span>

- <span data-ttu-id="46bb3-237">コードを使用して、ページ上のテキストボックスに値を要求するように指定します。</span><span class="sxs-lookup"><span data-stu-id="46bb3-237">Use code to specify that you want to require values in the text boxes on the page.</span></span>
- <span data-ttu-id="46bb3-238">すべてが正しく検証された場合にのみムービー情報がデータベースに追加されるように、テストをコードに配置します。</span><span class="sxs-lookup"><span data-stu-id="46bb3-238">Put a test into the code so that the movie information is added to the database only if everything validates properly.</span></span>
- <span data-ttu-id="46bb3-239">エラーメッセージを表示するコードをマークアップに追加します。</span><span class="sxs-lookup"><span data-stu-id="46bb3-239">Add code into the markup to display error messages.</span></span>

<span data-ttu-id="46bb3-240">*Addmovie*ページのコードブロックで、変数宣言の前の上部にある、次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="46bb3-240">In the code block in the *AddMovie* page, right up at the top before the variable declarations, add the following code:</span></span>

[!code-csharp[Main](entering-data/samples/sample7.cs)]

<span data-ttu-id="46bb3-241">エントリを要求するフィールド (`<input>` 要素) ごとに `Validation.RequireField` を1回呼び出します。</span><span class="sxs-lookup"><span data-stu-id="46bb3-241">You call `Validation.RequireField` once for each field (`<input>` element) where you want to require an entry.</span></span> <span data-ttu-id="46bb3-242">ここに示すように、呼び出しごとにカスタムエラーメッセージを追加することもできます。</span><span class="sxs-lookup"><span data-stu-id="46bb3-242">You can also add a custom error message for each call, like you see here.</span></span> <span data-ttu-id="46bb3-243">(ここでは、メッセージをさまざまな方法で表示するようにしています)。</span><span class="sxs-lookup"><span data-stu-id="46bb3-243">(We varied the messages just to show that you can put anything you like there.)</span></span>

<span data-ttu-id="46bb3-244">問題が発生した場合は、新しいムービー情報がデータベースに挿入されないようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="46bb3-244">If there's a problem, you want to prevent the new movie information from being inserted into the database.</span></span> <span data-ttu-id="46bb3-245">`if(IsPost)` ブロックで `&&` (論理 AND) を使用して、`Validation.IsValid()`をテストする別の条件を追加します。</span><span class="sxs-lookup"><span data-stu-id="46bb3-245">In the `if(IsPost)` block, use `&&` (logical AND) to add another condition that tests `Validation.IsValid()`.</span></span> <span data-ttu-id="46bb3-246">完了すると、`if(IsPost)` ブロック全体は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="46bb3-246">When you're done, the whole `if(IsPost)` block looks like this code:</span></span>

[!code-csharp[Main](entering-data/samples/sample8.cs)]

<span data-ttu-id="46bb3-247">`Validation` helper を使用して登録したフィールドのいずれかに検証エラーがある場合、`Validation.IsValid` メソッドは false を返します。</span><span class="sxs-lookup"><span data-stu-id="46bb3-247">If there's a validation error with any of the fields that you registered by using the `Validation` helper, the `Validation.IsValid` method returns false.</span></span> <span data-ttu-id="46bb3-248">その場合、そのブロック内のコードは実行されないため、無効なムービーエントリはデータベースに挿入されません。</span><span class="sxs-lookup"><span data-stu-id="46bb3-248">And in that case, none of the code in that block will run, so no invalid movie entries will be inserted into the database.</span></span> <span data-ttu-id="46bb3-249">もちろん、*映画*ページにリダイレクトされることはありません。</span><span class="sxs-lookup"><span data-stu-id="46bb3-249">And of course you're not redirected to the *Movies* page.</span></span>

<span data-ttu-id="46bb3-250">検証コードを含む完全なコードブロックは、次の例のようになります。</span><span class="sxs-lookup"><span data-stu-id="46bb3-250">The complete code block, including the validation code, now looks like this example:</span></span>

[!code-cshtml[Main](entering-data/samples/sample9.cshtml?highlight=10)]

## <a name="displaying-validation-errors"></a><span data-ttu-id="46bb3-251">検証エラーの表示</span><span class="sxs-lookup"><span data-stu-id="46bb3-251">Displaying Validation Errors</span></span>

<span data-ttu-id="46bb3-252">最後の手順では、エラーメッセージを表示します。</span><span class="sxs-lookup"><span data-stu-id="46bb3-252">The last step is to display any error messages.</span></span> <span data-ttu-id="46bb3-253">各検証エラーの個々のメッセージを表示することも、概要またはその両方を表示することもできます。</span><span class="sxs-lookup"><span data-stu-id="46bb3-253">You can display individual messages for each validation error, or you can display a summary, or both.</span></span> <span data-ttu-id="46bb3-254">このチュートリアルでは、そのしくみを確認できるように、両方を実行します。</span><span class="sxs-lookup"><span data-stu-id="46bb3-254">For this tutorial, you'll do both so that you can see how it works.</span></span>

<span data-ttu-id="46bb3-255">検証する各 `<input>` 要素の横に、`Html.ValidationMessage` メソッドを呼び出し、検証する `<input>` 要素の名前を渡します。</span><span class="sxs-lookup"><span data-stu-id="46bb3-255">Next to each `<input>` element that you're validating, call the `Html.ValidationMessage` method and pass it the name of the `<input>` element you're validating.</span></span> <span data-ttu-id="46bb3-256">`Html.ValidationMessage` メソッドは、エラーメッセージを表示する場所に配置します。</span><span class="sxs-lookup"><span data-stu-id="46bb3-256">You put the `Html.ValidationMessage` method right where you want the error message to appear.</span></span> <span data-ttu-id="46bb3-257">ページが実行されると、`Html.ValidationMessage` メソッドは、検証エラーが発生する `<span>` 要素をレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="46bb3-257">When the page runs, the `Html.ValidationMessage` method renders a `<span>` element where the validation error will go.</span></span> <span data-ttu-id="46bb3-258">(エラーがない場合は、`<span>` 要素がレンダリングされますが、テキストは表示されません)。</span><span class="sxs-lookup"><span data-stu-id="46bb3-258">(If there's no error, the `<span>` element is rendered, but there's no text in it.)</span></span>

<span data-ttu-id="46bb3-259">ページのマークアップを変更して、次の例のように、ページ上の3つの `<input>` 要素のそれぞれに `Html.ValidationMessage` メソッドを含めます。</span><span class="sxs-lookup"><span data-stu-id="46bb3-259">Change the markup in the page so that it includes an `Html.ValidationMessage` method for each of the three `<input>` elements on the page, like this example:</span></span>

[!code-cshtml[Main](entering-data/samples/sample10.cshtml?highlight=3,8,13)]

<span data-ttu-id="46bb3-260">概要のしくみを確認するには、ページの `<h1>Add a Movie</h1>` 要素の直後に次のマークアップとコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="46bb3-260">To see how the summary works, also add the following markup and code right after the `<h1>Add a Movie</h1>` element on the page:</span></span>

[!code-cshtml[Main](entering-data/samples/sample11.cshtml)]

<span data-ttu-id="46bb3-261">既定では、`Html.ValidationSummary` メソッドは、すべての検証メッセージをリスト (`<div>` 要素内にある `<ul>` 要素) に表示します。</span><span class="sxs-lookup"><span data-stu-id="46bb3-261">By default, the `Html.ValidationSummary` method displays all the validation messages in a list (a `<ul>` element that's inside a `<div>` element).</span></span> <span data-ttu-id="46bb3-262">`Html.ValidationMessage` メソッドと同様に、検証の概要のマークアップは常に表示されます。エラーがない場合は、リスト項目はレンダリングされません。</span><span class="sxs-lookup"><span data-stu-id="46bb3-262">As with the `Html.ValidationMessage` method, the markup for the validation summary is always rendered; if there are no errors, no list items are rendered.</span></span>

<span data-ttu-id="46bb3-263">概要は、フィールド固有の各エラーを表示するために `Html.ValidationMessage` メソッドを使用する代わりに、検証メッセージを表示する別の方法にすることができます。</span><span class="sxs-lookup"><span data-stu-id="46bb3-263">The summary can be an alternative way to display validation messages instead of by using the `Html.ValidationMessage` method to display each field-specific error.</span></span> <span data-ttu-id="46bb3-264">または、概要と詳細の両方を使用できます。</span><span class="sxs-lookup"><span data-stu-id="46bb3-264">Or you can use both a summary and the details.</span></span> <span data-ttu-id="46bb3-265">または、`Html.ValidationSummary` メソッドを使用して一般的なエラーを表示し、個々の `Html.ValidationMessage` 呼び出しを使用して詳細を表示することもできます。</span><span class="sxs-lookup"><span data-stu-id="46bb3-265">Or you can use the `Html.ValidationSummary` method to display a generic error and then use individual `Html.ValidationMessage` calls to display details.</span></span>

<span data-ttu-id="46bb3-266">完成したページは次の例のようになります。</span><span class="sxs-lookup"><span data-stu-id="46bb3-266">The complete page now looks like this example:</span></span>

[!code-cshtml[Main](entering-data/samples/sample12.cshtml)]

<span data-ttu-id="46bb3-267">これで終了です。</span><span class="sxs-lookup"><span data-stu-id="46bb3-267">That's it.</span></span> <span data-ttu-id="46bb3-268">これで、ムービーを追加して1つ以上のフィールドを残して、ページをテストできるようになりました。</span><span class="sxs-lookup"><span data-stu-id="46bb3-268">You can now test the page by adding a movie but leaving out one or more of the fields.</span></span> <span data-ttu-id="46bb3-269">この操作を行うと、次のようなエラーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="46bb3-269">When you do, you see the following error display:</span></span>

![検証エラーメッセージが表示された [ムービーの追加] ページ](entering-data/_static/image5.png)

## <a name="styling-the-validation-error-messages"></a><span data-ttu-id="46bb3-271">検証エラーメッセージのスタイル設定</span><span class="sxs-lookup"><span data-stu-id="46bb3-271">Styling the Validation Error Messages</span></span>

<span data-ttu-id="46bb3-272">エラーメッセージがあることを確認できますが、非常に優れているわけではありません。</span><span class="sxs-lookup"><span data-stu-id="46bb3-272">You can see that there are error messages, but they don't really stand out very well.</span></span> <span data-ttu-id="46bb3-273">ただし、エラーメッセージのスタイルを簡単に行うことができます。</span><span class="sxs-lookup"><span data-stu-id="46bb3-273">There's an easy way to style the error messages, though.</span></span>

<span data-ttu-id="46bb3-274">`Html.ValidationMessage`によって表示される個々のエラーメッセージのスタイルを指定するには、`field-validation-error`という名前の CSS スタイルクラスを作成します。</span><span class="sxs-lookup"><span data-stu-id="46bb3-274">To style the individual error messages that are displayed by `Html.ValidationMessage`, create a CSS style class named `field-validation-error`.</span></span> <span data-ttu-id="46bb3-275">検証の概要の外観を定義するには、`validation-summary-errors`という名前の CSS スタイルクラスを作成します。</span><span class="sxs-lookup"><span data-stu-id="46bb3-275">To define the look for the validation summary, create a CSS style class named `validation-summary-errors`.</span></span>

<span data-ttu-id="46bb3-276">この手法の動作を確認するには、ページの `<head>` セクション内に `<style>` 要素を追加します。</span><span class="sxs-lookup"><span data-stu-id="46bb3-276">To see how this technique works, add a `<style>` element inside the `<head>` section of the page.</span></span> <span data-ttu-id="46bb3-277">次に、`field-validation-error` という名前のスタイルクラスと、次の規則を含む `validation-summary-errors` を定義します。</span><span class="sxs-lookup"><span data-stu-id="46bb3-277">Then define style classes named `field-validation-error` and `validation-summary-errors` that contain the following rules:</span></span>

[!code-cshtml[Main](entering-data/samples/sample13.cshtml?highlight=4-17)]

<span data-ttu-id="46bb3-278">通常、スタイル情報は別の *.css*ファイルに配置することをお勧めしますが、わかりやすくするために、これをページに配置することができます。</span><span class="sxs-lookup"><span data-stu-id="46bb3-278">Normally you'd probably put style information into a separate *.css* file, but for simplicity you can put them in the page for now.</span></span> <span data-ttu-id="46bb3-279">(このチュートリアルの後の方で、CSS ルールを別の *.css*ファイルに移動します)。</span><span class="sxs-lookup"><span data-stu-id="46bb3-279">(Later in this tutorial set, you'll move the CSS rules to a separate *.css* file.)</span></span>

<span data-ttu-id="46bb3-280">検証エラーが発生した場合、`Html.ValidationMessage` メソッドは `class="field-validation-error"`を含む `<span>` 要素をレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="46bb3-280">If there's a validation error, the `Html.ValidationMessage` method renders a `<span>` element that includes `class="field-validation-error"`.</span></span> <span data-ttu-id="46bb3-281">そのクラスのスタイル定義を追加することによって、どのようなメッセージが表示されるかを構成できます。</span><span class="sxs-lookup"><span data-stu-id="46bb3-281">By adding a style definition for that class, you can configure what the message looks like.</span></span> <span data-ttu-id="46bb3-282">エラーが発生した場合、`ValidationSummary` メソッドは同様に、属性 `class="validation-summary-errors"`を動的に表示します。</span><span class="sxs-lookup"><span data-stu-id="46bb3-282">If there are errors, the `ValidationSummary` method likewise dynamically renders the attribute `class="validation-summary-errors"`.</span></span>

<span data-ttu-id="46bb3-283">もう一度ページを実行し、いくつかのフィールドを意図的に省略します。</span><span class="sxs-lookup"><span data-stu-id="46bb3-283">Run the page again and deliberately leave out a couple of the fields.</span></span> <span data-ttu-id="46bb3-284">エラーはさらに顕著になりました。</span><span class="sxs-lookup"><span data-stu-id="46bb3-284">The errors are now more noticeable.</span></span> <span data-ttu-id="46bb3-285">(実際には、何ができるかを説明するだけです)。</span><span class="sxs-lookup"><span data-stu-id="46bb3-285">(In fact, they're overdone, but that's just to show what you can do.)</span></span>

![スタイル設定された検証エラーを示す [ムービーの追加] ページ](entering-data/_static/image6.png)

## <a name="adding-a-link-to-the-movies-page"></a><span data-ttu-id="46bb3-287">[ムービー] ページへのリンクの追加</span><span class="sxs-lookup"><span data-stu-id="46bb3-287">Adding a Link to the Movies Page</span></span>

<span data-ttu-id="46bb3-288">最後の手順の1つは、元のムービーリストから*Addmovie*ページにアクセスするのに便利なことです。</span><span class="sxs-lookup"><span data-stu-id="46bb3-288">One final step is to make it convenient to get to the *AddMovie* page from the original movie listing.</span></span>

<span data-ttu-id="46bb3-289">もう一度 [*ムービー* ] ページを開きます。</span><span class="sxs-lookup"><span data-stu-id="46bb3-289">Open the *Movies* page again.</span></span> <span data-ttu-id="46bb3-290">`WebGrid` ヘルパーの後に続く `</div>` タグの後に、次のマークアップを追加します。</span><span class="sxs-lookup"><span data-stu-id="46bb3-290">After the closing `</div>` tag that follows the `WebGrid` helper, add the following markup:</span></span>

[!code-cshtml[Main](entering-data/samples/sample14.cshtml)]

<span data-ttu-id="46bb3-291">前述のように、ASP.NET は、`~` 演算子を web サイトのルートとして解釈します。</span><span class="sxs-lookup"><span data-stu-id="46bb3-291">As you saw before, ASP.NET interprets the `~` operator as the root of the website.</span></span> <span data-ttu-id="46bb3-292">`~` 演算子を使用する必要はありません。マークアップ `<a href="./AddMovie">Add a movie</a>` またはその他の方法を使用して、HTML によって認識されるパスを定義できます。</span><span class="sxs-lookup"><span data-stu-id="46bb3-292">You don't have to use the `~` operator; you could use the markup `<a href="./AddMovie">Add a movie</a>` or some other way to define the path that HTML understands.</span></span> <span data-ttu-id="46bb3-293">ただし、`~` 演算子は、サイトの柔軟性が向上するため、Razor ページへのリンクを作成するときによく使用される一般的な方法です。現在のページをサブフォルダーに移動しても、リンクは*Addmovie*ページに移動します。</span><span class="sxs-lookup"><span data-stu-id="46bb3-293">But the `~` operator is a good general approach when you create links for Razor pages, because it makes the site more flexible — if you move the current page to a subfolder, the link will still go to the *AddMovie* page.</span></span> <span data-ttu-id="46bb3-294">(`~` 演算子は、 *cshtml*ページでのみ機能することに注意してください。</span><span class="sxs-lookup"><span data-stu-id="46bb3-294">(Remember that the `~` operator only works in *.cshtml* pages.</span></span> <span data-ttu-id="46bb3-295">ASP.NET はこれを理解していますが、標準の HTML ではありません)。</span><span class="sxs-lookup"><span data-stu-id="46bb3-295">ASP.NET understands it, but it's not standard HTML.)</span></span>

<span data-ttu-id="46bb3-296">完了したら、[*ムービー* ] ページを実行します。</span><span class="sxs-lookup"><span data-stu-id="46bb3-296">When you're done, run the *Movies* page.</span></span> <span data-ttu-id="46bb3-297">次のようなページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="46bb3-297">It will look like this page:</span></span>

![[ムービーの追加] ページへのリンクを含むムービーページ](entering-data/_static/image7.png)

<span data-ttu-id="46bb3-299">**[ムービーの追加]** リンクをクリックして、[ *addmovie* ] ページに移動することを確認します。</span><span class="sxs-lookup"><span data-stu-id="46bb3-299">Click the **Add a movie** link to make sure that it goes to the *AddMovie* page.</span></span>

## <a name="coming-up-next"></a><span data-ttu-id="46bb3-300">次へ</span><span class="sxs-lookup"><span data-stu-id="46bb3-300">Coming Up Next</span></span>

<span data-ttu-id="46bb3-301">次のチュートリアルでは、データベースに既に存在するデータをユーザーが編集できるようにする方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="46bb3-301">In the next tutorial, you'll learn how to let users edit data that's already in the database.</span></span>

## <a name="complete-listing-for-addmovie-page"></a><span data-ttu-id="46bb3-302">AddMovie ページの完全な一覧</span><span class="sxs-lookup"><span data-stu-id="46bb3-302">Complete Listing for AddMovie Page</span></span>

[!code-cshtml[Main](entering-data/samples/sample15.cshtml)]

## <a name="additional-resources"></a><span data-ttu-id="46bb3-303">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="46bb3-303">Additional Resources</span></span>

- [<span data-ttu-id="46bb3-304">Razor 構文を使用した ASP.NET Web プログラミングの概要</span><span class="sxs-lookup"><span data-stu-id="46bb3-304">Introduction to ASP.NET Web Programming Using the Razor Syntax</span></span>](https://go.microsoft.com/fwlink/?LinkID=202890)
- <span data-ttu-id="46bb3-305">W3Schools サイトでの[SQL INSERT INTO ステートメント](http://www.w3schools.com/sql/sql_insert.asp)</span><span class="sxs-lookup"><span data-stu-id="46bb3-305">[SQL INSERT INTO Statement](http://www.w3schools.com/sql/sql_insert.asp) on the W3Schools site</span></span>
- <span data-ttu-id="46bb3-306">[ASP.NET Web ページサイトのユーザー入力を検証](https://go.microsoft.com/fwlink/?LinkId=253002)しています。</span><span class="sxs-lookup"><span data-stu-id="46bb3-306">[Validating User Input in ASP.NET Web Pages Sites](https://go.microsoft.com/fwlink/?LinkId=253002).</span></span> <span data-ttu-id="46bb3-307">`Validation` ヘルパーの操作の詳細については、こちらを参照してください。</span><span class="sxs-lookup"><span data-stu-id="46bb3-307">More information about working with the `Validation` helper.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="46bb3-308">[前へ](form-basics.md)
> [次へ](updating-data.md)</span><span class="sxs-lookup"><span data-stu-id="46bb3-308">[Previous](form-basics.md)
[Next](updating-data.md)</span></span>
