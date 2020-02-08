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
ms.openlocfilehash: cb9053593e2ea788638aec063c845cb91121861b
ms.sourcegitcommit: e365196c75ce93cd8967412b1cfdc27121816110
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/07/2020
ms.locfileid: "77075113"
---
# <a name="adding-a-new-category-to-the-dropdownlist-using-jquery-ui"></a><span data-ttu-id="fb7f1-102">jQuery UI を使用し、DropDownList に新しいカテゴリを追加する</span><span class="sxs-lookup"><span data-stu-id="fb7f1-102">Adding a New Category to the DropDownList using jQuery UI</span></span>

<span data-ttu-id="fb7f1-103">[Rick Anderson]((https://twitter.com/RickAndMSFT))</span><span class="sxs-lookup"><span data-stu-id="fb7f1-103">by [Rick Anderson]((https://twitter.com/RickAndMSFT))</span></span>

<span data-ttu-id="fb7f1-104">HTML `Select` タグは、固定カテゴリデータの一覧を表示するのに最適ですが、多くの場合、新しいカテゴリを追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="fb7f1-104">The HTML `Select` tag is ideal for presenting a list of fixed category data, but often times you need to add a new category.</span></span> <span data-ttu-id="fb7f1-105">ジャンル "Opera" をデータベースのカテゴリに追加するとします。</span><span class="sxs-lookup"><span data-stu-id="fb7f1-105">Suppose we want to add the genre "Opera" to the categories in our database?</span></span> <span data-ttu-id="fb7f1-106">このセクションでは、jQuery UI を使用して、新しいカテゴリを追加するために使用できるダイアログボックスを追加します。</span><span class="sxs-lookup"><span data-stu-id="fb7f1-106">In this section, we will use jQuery UI to add a dialog box we can use to add a new category.</span></span> <span data-ttu-id="fb7f1-107">次の図は、UI がブラウザーにどのように表示されるかを示しています。</span><span class="sxs-lookup"><span data-stu-id="fb7f1-107">The image below shows how the UI will present in the browser.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image1.png)

<span data-ttu-id="fb7f1-108">ユーザーが **[新しいジャンルの追加]** リンクを選択すると、ポップアップダイアログボックスが表示され、ユーザーは新しいジャンル名 (および必要に応じて説明) を入力するように求められます。</span><span class="sxs-lookup"><span data-stu-id="fb7f1-108">When a user selects the **Add New Genre** link, a pop-up dialog box prompts the user for a new genre name (and optionally a description).</span></span> <span data-ttu-id="fb7f1-109">次の画像は、 **[ジャンルの追加]** ポップアップダイアログを示しています。</span><span class="sxs-lookup"><span data-stu-id="fb7f1-109">The image below show the **Add Genre** pop-up dialog.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image2.png)

<span data-ttu-id="fb7f1-110">新しいジャンル名を入力して **[保存]** ボタンを押すと、次のような結果になります。</span><span class="sxs-lookup"><span data-stu-id="fb7f1-110">When a new genre name is entered and the **Save** button is pushed, the following happens:</span></span>

1. <span data-ttu-id="fb7f1-111">AJAX 呼び出しでは、Genre コントローラーの Create メソッドにデータがポストされます。これにより、新しいジャンルがデータベースに保存され、新しいジャンル情報 (ジャンル名と ID) が JSON として返されます。</span><span class="sxs-lookup"><span data-stu-id="fb7f1-111">An AJAX call posts the data to the Create method of the Genre Controller, which saves the new genre to the database and returns the new genre information (genre name and ID) as JSON.</span></span>
2. <span data-ttu-id="fb7f1-112">JavaScript は、新しいジャンルデータを選択リストに追加します。</span><span class="sxs-lookup"><span data-stu-id="fb7f1-112">JavaScript adds the new genre data to the select list.</span></span>
3. <span data-ttu-id="fb7f1-113">JavaScript は、選択された項目を新しいジャンルにします。</span><span class="sxs-lookup"><span data-stu-id="fb7f1-113">JavaScript makes the new genre the selected item.</span></span>

   <span data-ttu-id="fb7f1-114">次の図では、 **Opera**がデータベースに追加され、 **[ジャンル]** ドロップダウンリストで選択されています。</span><span class="sxs-lookup"><span data-stu-id="fb7f1-114">In the image below, **Opera** was added to the database and selected in the **Genre** drop down list.</span></span> 

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image3.png)

<span data-ttu-id="fb7f1-115">*Views\StoreManager\Create.cshtml*ファイルを開き、genre マークアップを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="fb7f1-115">Open the *Views\StoreManager\Create.cshtml* file and replace the genre markup with the following the following code:</span></span>

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample1.cshtml)]

<span data-ttu-id="fb7f1-116">`_ChooseGenre` 部分ビューには、新しいジャンルの追加機能を実装するために使用される JavaScript と jQuery をフックするためのすべてのロジックが含まれます。</span><span class="sxs-lookup"><span data-stu-id="fb7f1-116">The `_ChooseGenre` partial view will contain all the logic to hook up the JavaScript and jQuery used to implement the add new genre feature.</span></span> <span data-ttu-id="fb7f1-117">コードを完成させると、アーティスト UI でも同じことが簡単になります。</span><span class="sxs-lookup"><span data-stu-id="fb7f1-117">Once we have completed the code it will be simple to do the same with the artist UI.</span></span>

<span data-ttu-id="fb7f1-118">ソリューションエクスプローラーで、 *Views\StoreManager*フォルダーを右クリックし、 **[追加]** 、 **[表示]** の順に選択します。</span><span class="sxs-lookup"><span data-stu-id="fb7f1-118">In Solution Explorer, right click the *Views\StoreManager* folder and select **Add**, then **View**.</span></span> <span data-ttu-id="fb7f1-119">**[ビュー名]** の入力 ボックスに「`_ChooseGenre`」と入力し、 **[追加]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="fb7f1-119">In the **View name** input, enter `_ChooseGenre` then select **Add**.</span></span> <span data-ttu-id="fb7f1-120">*Views\StoreManager\\_ChooseGenre*ファイル内のマークアップを次のように置き換えます。</span><span class="sxs-lookup"><span data-stu-id="fb7f1-120">Replace the markup in the *Views\StoreManager\\_ChooseGenre.cshtml* file with the following:</span></span>

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample2.cshtml)]

<span data-ttu-id="fb7f1-121">最初の行では、`Album` をモデルとして渡していることを宣言しています。これは、Create view にあるモデルステートメントとまったく同じです。</span><span class="sxs-lookup"><span data-stu-id="fb7f1-121">The first line declares that we are passing in an `Album` as our model, exactly the same model statement found in the Create view.</span></span> <span data-ttu-id="fb7f1-122">次の数行は、**ラベル**ヘルパーマークアップです。</span><span class="sxs-lookup"><span data-stu-id="fb7f1-122">The next few lines are the **Label** helper markup.</span></span> <span data-ttu-id="fb7f1-123">次の行は、元の Create view とまったく同じように、 **DropDownList**ヘルパー呼び出しです。</span><span class="sxs-lookup"><span data-stu-id="fb7f1-123">The next line is the **DropDownList** helper call, exactly the same as in the original Create view.</span></span> <span data-ttu-id="fb7f1-124">次の行では、`Add New Genre`という名前のリンクを追加し、ボタンのようにスタイルを指定します。</span><span class="sxs-lookup"><span data-stu-id="fb7f1-124">The next line adds a link with the name `Add New Genre`, and styles it like a button.</span></span> <span data-ttu-id="fb7f1-125">`ValidationMessageFor` を含む行は、Create ビューから直接コピーされます。</span><span class="sxs-lookup"><span data-stu-id="fb7f1-125">The line containing `ValidationMessageFor` is copied directly from the Create view.</span></span> <span data-ttu-id="fb7f1-126">次の行を実行します。</span><span class="sxs-lookup"><span data-stu-id="fb7f1-126">The following lines:</span></span>

[!code-html[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample3.html)]

<span data-ttu-id="fb7f1-127">`genreDialog`の ID を使用して、非表示の div を作成します。</span><span class="sxs-lookup"><span data-stu-id="fb7f1-127">creates a hidden div, with the ID of `genreDialog`.</span></span> <span data-ttu-id="fb7f1-128">JQuery を使用して、 **[ジャンルの追加]** ダイアログボックスをこの div の `genreDialog` ID と共にフックします。</span><span class="sxs-lookup"><span data-stu-id="fb7f1-128">We will use jQuery to hook up our **Add Genre** dialog box with the ID `genreDialog` in this div.</span></span> <span data-ttu-id="fb7f1-129">最後の2つのスクリプトタグには、新しいジャンルの追加機能を実装するために使用する JavaScript ファイルへのリンクが含まれています。</span><span class="sxs-lookup"><span data-stu-id="fb7f1-129">The last two script tags contain links to the JavaScript files we will use to implement the add new genre feature.</span></span> <span data-ttu-id="fb7f1-130">この*ファイルは、プロジェクト*で提供されています。これについては、チュートリアルの後半で説明します。</span><span class="sxs-lookup"><span data-stu-id="fb7f1-130">The */Scripts/chooseGenre.js* file is provided for you in the project, we will examine it later in the tutorial.</span></span>

<span data-ttu-id="fb7f1-131">アプリケーションを実行し、 **[新しいジャンルの追加]** ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="fb7f1-131">Run the application and click on the **Add New Genre** button.</span></span> <span data-ttu-id="fb7f1-132">**[ジャンルの追加]** ダイアログボックスで、 **[名前]** 入力ボックスに「 **Opera** 」と入力します。</span><span class="sxs-lookup"><span data-stu-id="fb7f1-132">In the **Add Genre** dialog box, enter **Opera** in the **Name** input box.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image4.png)

<span data-ttu-id="fb7f1-133">**[保存]** ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="fb7f1-133">Click the **Save** button.</span></span> <span data-ttu-id="fb7f1-134">AJAX 呼び出しによって Opera カテゴリが作成され、ドロップダウンリストに Opera が挿入され、選択したジャンルとして Opera が設定されます。</span><span class="sxs-lookup"><span data-stu-id="fb7f1-134">An AJAX call creates the Opera category and then populates the dropdown list with Opera, and sets Opera as the selected genre.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image5.png)

<span data-ttu-id="fb7f1-135">アーティスト、タイトル、価格を入力し、 **[作成]** ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="fb7f1-135">Enter an artist, title and price, then select the **Create** button.</span></span> <span data-ttu-id="fb7f1-136">$8.99 未満の価格を入力すると、新しいアルバムがインデックスビューの上部に表示されます。</span><span class="sxs-lookup"><span data-stu-id="fb7f1-136">If you enter a price less than $8.99, the new album will appear at the top of the Index view.</span></span> <span data-ttu-id="fb7f1-137">新しいアルバムエントリがデータベースに保存されたことを確認します。</span><span class="sxs-lookup"><span data-stu-id="fb7f1-137">Verify the new album entry was saved in the database.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image6.png)

<span data-ttu-id="fb7f1-138">1文字だけで新しいジャンルを作成してみてください。</span><span class="sxs-lookup"><span data-stu-id="fb7f1-138">Try creating a new genre with only one letter.</span></span> <span data-ttu-id="fb7f1-139">次のコードでは、 *modelall Genre.cs*ファイルのジャンル名の最小値と最大長を設定しています。</span><span class="sxs-lookup"><span data-stu-id="fb7f1-139">The following code in the *Models\Genre.cs* file sets the minimum and maximum length of the genre name.</span></span>

[!code-csharp[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample4.cs)]

<span data-ttu-id="fb7f1-140">クライアント側の検証レポート 2 ~ 20 文字の文字列を入力する必要があります。</span><span class="sxs-lookup"><span data-stu-id="fb7f1-140">Client side validation reports you must enter a string between 2 and 20 characters.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image7.png)

### <a name="examining-how-a-new-genre-is-added-to-the-database-and-the-select-list"></a><span data-ttu-id="fb7f1-141">新しいジャンルがデータベースと選択リストに追加された方法を確認しています。</span><span class="sxs-lookup"><span data-stu-id="fb7f1-141">Examining How a New Genre is Added to the Database and the Select List.</span></span>

<span data-ttu-id="fb7f1-142">*スクリプト*ファイルを開き、コードを確認します。</span><span class="sxs-lookup"><span data-stu-id="fb7f1-142">Open the *Scripts\chooseGenre.js* file and examine the code.</span></span>

[!code-javascript[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample5.js)]

<span data-ttu-id="fb7f1-143">2行目では、ID `genreDialog` を使用して、 *Views\StoreManager\\_ChooseGenre*ファイルの div タグにダイアログボックスを作成します。</span><span class="sxs-lookup"><span data-stu-id="fb7f1-143">The second line uses the ID `genreDialog` to create a dialog box on the div tag in the *Views\StoreManager\\_ChooseGenre.cshtml* file.</span></span> <span data-ttu-id="fb7f1-144">名前付きパラメーターのほとんどは、わかりやすいものです。</span><span class="sxs-lookup"><span data-stu-id="fb7f1-144">Most of the named parameters are self explanatory.</span></span> <span data-ttu-id="fb7f1-145">`autoOpen` パラメーターが false に設定されている場合は、 **[ジャンルの作成]** ボタンを選択すると、ダイアログが明示的に開きます (これについては後述します)。</span><span class="sxs-lookup"><span data-stu-id="fb7f1-145">The `autoOpen` parameter is set to false, selecting the **Create Genre** button will open the dialogue explicitly (this is described latter on).</span></span> <span data-ttu-id="fb7f1-146">ダイアログには、 **[保存]** と **[キャンセル**] の2つのボタンがあります。</span><span class="sxs-lookup"><span data-stu-id="fb7f1-146">The dialog has two buttons, **Save** and **Cancel**.</span></span> <span data-ttu-id="fb7f1-147">**[キャンセル**] ボタンをクリックすると、ダイアログボックスが閉じます。</span><span class="sxs-lookup"><span data-stu-id="fb7f1-147">The **Cancel** button closes the dialog.</span></span> <span data-ttu-id="fb7f1-148">次のコードは、 **[保存]** ボタンの関数を示しています。</span><span class="sxs-lookup"><span data-stu-id="fb7f1-148">The following code shows the **Save** button function.</span></span>

[!code-javascript[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample6.js)]

<span data-ttu-id="fb7f1-149">`var createGenreForm` が `createGenreForm` ID から選択されます。</span><span class="sxs-lookup"><span data-stu-id="fb7f1-149">The `var createGenreForm` is selected from the `createGenreForm` ID.</span></span> <span data-ttu-id="fb7f1-150">`createGenreForm` ID は、 *Views\Genre\\_CreateGenre*ファイルにある次のコードで設定されています。</span><span class="sxs-lookup"><span data-stu-id="fb7f1-150">The `createGenreForm` ID was set in the following code found in the *Views\Genre\\_CreateGenre.cshtml* file.</span></span>

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample7.cshtml)]

<span data-ttu-id="fb7f1-151">*Views\Genre\\_CreateGenre*ファイルで使用される[Html. beginform](https://msdn.microsoft.com/library/dd492714.aspx)ヘルパーオーバーロードでは、フォームを送信するための URL を含む ACTION 属性を持つ html が生成されます。</span><span class="sxs-lookup"><span data-stu-id="fb7f1-151">The [Html.BeginForm](https://msdn.microsoft.com/library/dd492714.aspx) helper overload used in the *Views\Genre\\_CreateGenre.cshtml* file generates HTML with an action attribute containing the URL to submit the form.</span></span> <span data-ttu-id="fb7f1-152">これを確認するには、ブラウザーで [アルバムの作成] ページを表示し、ブラウザーで [ソースの表示] を選択します。</span><span class="sxs-lookup"><span data-stu-id="fb7f1-152">You can see this by displaying the create album page in a browser and selecting show source in the browser.</span></span> <span data-ttu-id="fb7f1-153">次のマークアップは、フォームタグを含む生成された HTML を示しています。</span><span class="sxs-lookup"><span data-stu-id="fb7f1-153">The following markup shows the generated HTML containing the form tag.</span></span>

[!code-html[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample8.html)]

<span data-ttu-id="fb7f1-154">JQuery `$.post` 行は、アクション属性 (`/StoreManager/Create`) に対して AJAX 呼び出しを行い、 **[ジャンルの作成]** ダイアログボックスからデータを渡します。</span><span class="sxs-lookup"><span data-stu-id="fb7f1-154">The jQuery `$.post` line makes an AJAX call to the action attribute (`/StoreManager/Create`) and passes in the data from the **Create Genre** dialog box.</span></span> <span data-ttu-id="fb7f1-155">データは、新しいジャンルの名前とオプションの説明で構成されます。</span><span class="sxs-lookup"><span data-stu-id="fb7f1-155">The data consists of the name for the new genre and an optional description.</span></span> <span data-ttu-id="fb7f1-156">AJAX 呼び出しが成功すると、新しいジャンルの名前と値が選択マークアップに追加され、新しいジャンルは選択された値に設定されます。</span><span class="sxs-lookup"><span data-stu-id="fb7f1-156">If the AJAX call is successful, the new genre name and value are added to the Select markup, and the new genre is set to the selected value.</span></span> <span data-ttu-id="fb7f1-157">これは動的に生成されたマークアップであるため、ブラウザーでソースを表示して新しい select オプションを表示することはできません。</span><span class="sxs-lookup"><span data-stu-id="fb7f1-157">Because this is dynamically generated markup, you can't see the new select option by viewing the source in the browser.</span></span> <span data-ttu-id="fb7f1-158">新しい HTML は IE 9 の F12 開発者ツールで確認できます。</span><span class="sxs-lookup"><span data-stu-id="fb7f1-158">You can see the new HTML with the IE 9 F12 developer tools.</span></span> <span data-ttu-id="fb7f1-159">新しい select オプションを表示するには、Internet Explorer 9 で F12 キーを押して、F12 開発者ツールを起動します。</span><span class="sxs-lookup"><span data-stu-id="fb7f1-159">To view the new select option, in Internet Explorer 9, hit the F12 key to start the F12 developer tools.</span></span> <span data-ttu-id="fb7f1-160">[作成] ページに移動し、新しいジャンルを追加して、ジャンルの選択リストで新しいジャンルを選択します。</span><span class="sxs-lookup"><span data-stu-id="fb7f1-160">Navigate to the Create page and add a new genre so the new genre is selected in the genre select list.</span></span> <span data-ttu-id="fb7f1-161">F12 開発者ツールで、次のようにします。</span><span class="sxs-lookup"><span data-stu-id="fb7f1-161">In the F12 developer tools:</span></span>

1. <span data-ttu-id="fb7f1-162">[HTML] タブを選択します。</span><span class="sxs-lookup"><span data-stu-id="fb7f1-162">Select the HTML tab.</span></span>
2. <span data-ttu-id="fb7f1-163">更新アイコンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="fb7f1-163">Hit the refresh icon.</span></span>  
    ![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image8.png)
3. <span data-ttu-id="fb7f1-164">検索ボックスに、「GenreID」と入力します。</span><span class="sxs-lookup"><span data-stu-id="fb7f1-164">In the search box, enter GenreID.</span></span>
4. <span data-ttu-id="fb7f1-165">次のアイコンを使用します。</span><span class="sxs-lookup"><span data-stu-id="fb7f1-165">Using the next icon,</span></span>   
    ![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image9.png)  
   <span data-ttu-id="fb7f1-166">次の select タグに移動します。</span><span class="sxs-lookup"><span data-stu-id="fb7f1-166">navigate to the following select tag:</span></span>

    [!code-html[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample9.html)]
5. <span data-ttu-id="fb7f1-167">最後のオプションの値を展開します。</span><span class="sxs-lookup"><span data-stu-id="fb7f1-167">Expand the last option value.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image10.png)

<span data-ttu-id="fb7f1-168">次のコードは、*スクリプト*ファイル内の次のコードで、 **[新しいジャンルの追加]** ボタンをクリックイベントに接続する方法と、 **[新しいジャンルの追加]** ダイアログボックスを作成する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="fb7f1-168">The following code in the *Scripts\chooseGenre.js* file shows the how the **Add New Genre** button gets connected to the click event, and how the **Add New Genre** dialog box is created.</span></span>

[!code-javascript[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample10.js)]

<span data-ttu-id="fb7f1-169">最初の行では、 **[新しいジャンルの追加]** ボタンに関連付けられている click 関数が作成されます。</span><span class="sxs-lookup"><span data-stu-id="fb7f1-169">The first line creates a click function attached to the **Add New Genre** button.</span></span> <span data-ttu-id="fb7f1-170">Views\StoreManager\\_ChooseGenre の次のマークアップは、 **[新しいジャンルの追加]** ボタンが作成される方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="fb7f1-170">The following markup from the Views\StoreManager\\_ChooseGenre.cshtml file shows how the **Add New Genre** button is created:</span></span>

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample11.cshtml)]

<span data-ttu-id="fb7f1-171">Load メソッドは、[ジャンルの追加] ダイアログボックスを作成して開き、ダイアログに入力されたデータに対してクライアント検証が行われるように、jQuery `parse` メソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="fb7f1-171">The load method creates and opens the Add Genre dialog and calls the jQuery `parse` method so client validation occurs on data entered in the dialog.</span></span>

<span data-ttu-id="fb7f1-172">このセクションでは、選択リストに新しいカテゴリデータを追加するために使用できるダイアログを作成する方法について説明しました。</span><span class="sxs-lookup"><span data-stu-id="fb7f1-172">In this section you have learned how to create a dialog that can be used to add new category data to a select list.</span></span> <span data-ttu-id="fb7f1-173">同じ手順に従って、アーティストの選択リストに新しいアーティストを追加するための UI を作成できます。</span><span class="sxs-lookup"><span data-stu-id="fb7f1-173">You can follow the same procedure to create UI to add a new artist to the artist select list.</span></span> <span data-ttu-id="fb7f1-174">このチュートリアルでは、ASP.NET MVC HTML ヘルパーの**DropDownList**の使用方法の概要を説明しました。</span><span class="sxs-lookup"><span data-stu-id="fb7f1-174">This tutorial has given an overview of working with the ASP.NET MVC HTML helper **DropDownList**.</span></span> <span data-ttu-id="fb7f1-175">**DropDownList**の使用方法の詳細については、以下の「追加の参照」セクションを参照してください。</span><span class="sxs-lookup"><span data-stu-id="fb7f1-175">For additional information on working with the **DropDownList**, see the addition references section below.</span></span> <span data-ttu-id="fb7f1-176">このチュートリアルが役に立つかどうかをお知らせください。</span><span class="sxs-lookup"><span data-stu-id="fb7f1-176">Please let us know if this tutorial has been helpful.</span></span>

<span data-ttu-id="fb7f1-177">Rick Anderson [at] Microsoft .com</span><span class="sxs-lookup"><span data-stu-id="fb7f1-177">Rick.Anderson[at]Microsoft.com</span></span>

### <a name="additional-references"></a><span data-ttu-id="fb7f1-178">その他のリファレンス</span><span class="sxs-lookup"><span data-stu-id="fb7f1-178">Additional References</span></span>

- <span data-ttu-id="fb7f1-179">[ASP.NET MVC –カスケードドロップダウンリストのチュートリアル (](https://weblogs.asp.net/raduenuca/archive/2011/03/06/asp-net-mvc-cascading-dropdown-lists-tutorial-part-1-defining-the-problem-and-the-context.aspx)エンコード[u enuca](https://weblogs.asp.net/raduenuca/default.aspx)別)</span><span class="sxs-lookup"><span data-stu-id="fb7f1-179">[ASP.NET MVC–Cascading Dropdown Lists Tutorial](https://weblogs.asp.net/raduenuca/archive/2011/03/06/asp-net-mvc-cascading-dropdown-lists-tutorial-part-1-defining-the-problem-and-the-context.aspx) by [Radu Enuca](https://weblogs.asp.net/raduenuca/default.aspx)</span></span>
- <span data-ttu-id="fb7f1-180">[選択](https://harvesthq.github.com/chosen/)複数選択とフィルター処理をサポートする JavaScript プラグイン。</span><span class="sxs-lookup"><span data-stu-id="fb7f1-180">[Chosen](https://harvesthq.github.com/chosen/) A JavaScript plugin that support multi-select and filtering.</span></span>

### <a name="contributors"></a><span data-ttu-id="fb7f1-181">寄稿者</span><span class="sxs-lookup"><span data-stu-id="fb7f1-181">Contributors</span></span>

- [<span data-ttu-id="fb7f1-182">レーダー</span><span class="sxs-lookup"><span data-stu-id="fb7f1-182">Radu Enuca</span></span>](https://weblogs.asp.net/raduenuca/default.aspx)
- <span data-ttu-id="fb7f1-183">Jean-Sébastien Goupil</span><span class="sxs-lookup"><span data-stu-id="fb7f1-183">Jean-Sébastien Goupil</span></span>
- [<span data-ttu-id="fb7f1-184">Brad Wilson</span><span class="sxs-lookup"><span data-stu-id="fb7f1-184">Brad Wilson</span></span>](http://bradwilson.typepad.com/)

### <a name="reviewers"></a><span data-ttu-id="fb7f1-185">校閲者</span><span class="sxs-lookup"><span data-stu-id="fb7f1-185">Reviewers</span></span>

- <span data-ttu-id="fb7f1-186">Jean-Sébastien Goupil</span><span class="sxs-lookup"><span data-stu-id="fb7f1-186">Jean-Sébastien Goupil</span></span>
- [<span data-ttu-id="fb7f1-187">Brad Wilson</span><span class="sxs-lookup"><span data-stu-id="fb7f1-187">Brad Wilson</span></span>](http://bradwilson.typepad.com/)
- <span data-ttu-id="fb7f1-188">Mike Pope</span><span class="sxs-lookup"><span data-stu-id="fb7f1-188">Mike Pope</span></span>
- <span data-ttu-id="fb7f1-189">Tom Dykstra</span><span class="sxs-lookup"><span data-stu-id="fb7f1-189">Tom Dykstra</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="fb7f1-190">前へ</span><span class="sxs-lookup"><span data-stu-id="fb7f1-190">Previous</span></span>](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper.md)
