---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part8
title: モデルに列を追加する |Microsoft Docs
author: shanselman
description: これは、ASP.NET MVC の基本を紹介する初心者向けチュートリアルです。 データベースを読み書きする単純な web アプリケーションを作成します。
ms.author: riande
ms.date: 08/14/2010
ms.assetid: 7ae696b9-348f-4993-8ebb-a838acbe0c28
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part8
msc.type: authoredcontent
ms.openlocfilehash: 1cf092c3db3959d6f47006f1be2ba82833c5dc06
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78437224"
---
# <a name="adding-a-column-to-the-model"></a><span data-ttu-id="4905a-104">モデルに列を追加する</span><span class="sxs-lookup"><span data-stu-id="4905a-104">Adding a Column to the Model</span></span>

<span data-ttu-id="4905a-105">[Scott マン Selman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="4905a-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> <span data-ttu-id="4905a-106">これは、ASP.NET MVC の基本を紹介する初心者向けチュートリアルです。</span><span class="sxs-lookup"><span data-stu-id="4905a-106">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="4905a-107">データベースを読み書きする単純な web アプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="4905a-107">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="4905a-108">他の ASP.NET MVC のチュートリアルとサンプルについては、 [ASP.NET mvc learning center](../../../index.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="4905a-108">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>

<span data-ttu-id="4905a-109">このセクションでは、データベースのスキーマに変更を加え、アプリケーション内で変更を処理する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="4905a-109">In this section we are going to walk through how we can make changes to the schema of our database, and handle the changes within our application.</span></span>

<span data-ttu-id="4905a-110">ムービーテーブルに "評価" 列を追加してみましょう。</span><span class="sxs-lookup"><span data-stu-id="4905a-110">Let's add a "Rating" Column to the Movie table.</span></span> <span data-ttu-id="4905a-111">IDE に戻り、[データベースエクスプローラー] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="4905a-111">Go back to the IDE and click the Database Explorer.</span></span> <span data-ttu-id="4905a-112">[ムービー] テーブルを右クリックし、[テーブル定義を開く] を選択します。</span><span class="sxs-lookup"><span data-stu-id="4905a-112">Right click the Movie table and select Open Table Definition.</span></span>

<span data-ttu-id="4905a-113">次に示すように "評価" 列を追加します。</span><span class="sxs-lookup"><span data-stu-id="4905a-113">Add a "Rating" column as seen below.</span></span> <span data-ttu-id="4905a-114">現在評価がないため、列で null 値を許容できます。</span><span class="sxs-lookup"><span data-stu-id="4905a-114">Since we don't have any Ratings now, the column can allow nulls.</span></span> <span data-ttu-id="4905a-115">[保存] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="4905a-115">Click Save.</span></span>

<span data-ttu-id="4905a-116">[ムービーテーブルの編集 ![](getting-started-with-mvc-part8/_static/image2.png)](getting-started-with-mvc-part8/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="4905a-116">[![Editing Movies Table](getting-started-with-mvc-part8/_static/image2.png)](getting-started-with-mvc-part8/_static/image1.png)</span></span>

<span data-ttu-id="4905a-117">次に、ソリューションエクスプローラーに戻り、([モデル] フォルダー内の) .edmx ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="4905a-117">Next, return to the Solution Explorer and open up the Movies.edmx file (which is in the \Models folder).</span></span> <span data-ttu-id="4905a-118">デザイン画面 (白い部分) を右クリックし、[データベースからモデルを更新] を選択します。</span><span class="sxs-lookup"><span data-stu-id="4905a-118">Right click on the design surface (the white area) and select Update Model from Database.</span></span>

<span data-ttu-id="4905a-119">[![映画-Microsoft Visual Web Developer 2010 Express (11)](getting-started-with-mvc-part8/_static/image4.png)](getting-started-with-mvc-part8/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="4905a-119">[![Movies - Microsoft Visual Web Developer 2010 Express (11)](getting-started-with-mvc-part8/_static/image4.png)](getting-started-with-mvc-part8/_static/image3.png)</span></span>

<span data-ttu-id="4905a-120">これにより、"更新ウィザード" が起動します。</span><span class="sxs-lookup"><span data-stu-id="4905a-120">This will launch the "Update Wizard".</span></span> <span data-ttu-id="4905a-121">その中の [更新] タブをクリックし、[完了] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="4905a-121">Click the Refresh tab within it and click Finish.</span></span> <span data-ttu-id="4905a-122">次に、ムービーモデルクラスが新しい列で更新されます。</span><span class="sxs-lookup"><span data-stu-id="4905a-122">Our Movie model class will then be updated with the new column.</span></span>

![更新ウィザード (2)](getting-started-with-mvc-part8/_static/image5.png)

<span data-ttu-id="4905a-124">[完了] をクリックすると、モデルの Movie エンティティに新しい評価列が追加されていることがわかります。</span><span class="sxs-lookup"><span data-stu-id="4905a-124">After clicking Finish, you can see the new Rating Column has been added to the Movie Entity in our model.</span></span>

<span data-ttu-id="4905a-125">[![Movie エンティティ](getting-started-with-mvc-part8/_static/image7.png)](getting-started-with-mvc-part8/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="4905a-125">[![Movie Entity](getting-started-with-mvc-part8/_static/image7.png)](getting-started-with-mvc-part8/_static/image6.png)</span></span>

<span data-ttu-id="4905a-126">データベースモデルに列を追加しましたが、ビューで認識されません。</span><span class="sxs-lookup"><span data-stu-id="4905a-126">We've added a column in the database model, but the Views don't know about it.</span></span>

## <a name="update-views-with-model-changes"></a><span data-ttu-id="4905a-127">モデルの変更によるビューの更新</span><span class="sxs-lookup"><span data-stu-id="4905a-127">Update Views with Model Changes</span></span>

<span data-ttu-id="4905a-128">新しい評価列を反映するようにビューテンプレートを更新するには、いくつかの方法があります。</span><span class="sxs-lookup"><span data-stu-id="4905a-128">There are a few ways we could update our view templates to reflect the new Rating column.</span></span> <span data-ttu-id="4905a-129">[ビューの追加] ダイアログでこれらのビューを生成して作成したため、これらのビューを削除して再作成することができます。</span><span class="sxs-lookup"><span data-stu-id="4905a-129">Since we created these Views by generating them via the Add View dialog, we could delete them and recreate them again.</span></span> <span data-ttu-id="4905a-130">ただし、通常、ユーザーは最初のスキャフォールディング生成からビューテンプレートを変更しています。また、Create の ID フィールドの場合と同様に、フィールドを手動で追加または削除する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4905a-130">However, typically people will have already made modifications to their View templates from the initial scaffolded generation and will want to add or delete fields manually, just as we did with the ID field for Create.</span></span>

<span data-ttu-id="4905a-131">\Views\Movies\Index.aspx テンプレートを開き、&lt;th&gt;評価&lt;/th&gt; をムービーテーブルの先頭に追加します。</span><span class="sxs-lookup"><span data-stu-id="4905a-131">Open up the \Views\Movies\Index.aspx template and add a &lt;th&gt;Rating&lt;/th&gt; to the head of the Movie table.</span></span> <span data-ttu-id="4905a-132">ジャンルの後に自分のものを追加しました。</span><span class="sxs-lookup"><span data-stu-id="4905a-132">I added mine after Genre.</span></span> <span data-ttu-id="4905a-133">次に、同じ列の位置で下に移動し、新しい評価を出力する行を追加します。</span><span class="sxs-lookup"><span data-stu-id="4905a-133">Then, in the same column position but lower down, add a line to output our new Rating.</span></span>

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample1.aspx)]

<span data-ttu-id="4905a-134">最後のインデックス .aspx テンプレートは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="4905a-134">Our final Index.aspx template will look like this:</span></span>

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample2.aspx)]

<span data-ttu-id="4905a-135">次に、\Views\Movies\Create.aspx テンプレートを開き、新しい評価プロパティのラベルとテキストボックスを追加します。</span><span class="sxs-lookup"><span data-stu-id="4905a-135">Let's then open up the \Views\Movies\Create.aspx template and add a Label and Textbox for our new Rating property:</span></span>

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample3.aspx)]

<span data-ttu-id="4905a-136">最終的に作成された .aspx テンプレートは次のようになります。ブラウザーのタイトルとセカンダリ &lt;h2&gt; タイトルは、ここで説明しているように "ムービーの作成" のように変更してみましょう。</span><span class="sxs-lookup"><span data-stu-id="4905a-136">Our final Create.aspx template will look like this, and let's change our browser's title and secondary &lt;h2&gt; title to something like "Create a Movie" while we're in here!</span></span>

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample4.aspx)]

<span data-ttu-id="4905a-137">アプリを実行すると、[作成] ページに追加された新しいフィールドがデータベースに追加されました。</span><span class="sxs-lookup"><span data-stu-id="4905a-137">Run your app and now you've got a new field in the database that's been added to the Create page.</span></span> <span data-ttu-id="4905a-138">新しいムービーを追加します。今回は評価付きで、[作成] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="4905a-138">Add a new Movie - this time with a Rating - and click Create.</span></span>

<span data-ttu-id="4905a-139">[ムービーを作成 ![には-Windows Internet Explorer](getting-started-with-mvc-part8/_static/image9.png)](getting-started-with-mvc-part8/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="4905a-139">[![Create a Movie - Windows Internet Explorer](getting-started-with-mvc-part8/_static/image9.png)](getting-started-with-mvc-part8/_static/image8.png)</span></span>

<span data-ttu-id="4905a-140">[作成] をクリックすると、新しいムービーがデータベースの新しい評価列と共に一覧表示されるインデックスページに送信されます。</span><span class="sxs-lookup"><span data-stu-id="4905a-140">After you click Create, you're sent to the Index page where you new Movie is listed with the new Rating Column in the database</span></span>

<span data-ttu-id="4905a-141">[![ムービーの一覧-Windows Internet Explorer (12)](getting-started-with-mvc-part8/_static/image11.png)](getting-started-with-mvc-part8/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="4905a-141">[![Movie List - Windows Internet Explorer (12)](getting-started-with-mvc-part8/_static/image11.png)](getting-started-with-mvc-part8/_static/image10.png)</span></span>

<span data-ttu-id="4905a-142">この基本的なチュートリアルでは、コントローラーの作成と、それらをビューに関連付け、ハードコーディングされたデータを使用する方法について見てきました。</span><span class="sxs-lookup"><span data-stu-id="4905a-142">This basic tutorial got you started making Controllers, associating them with Views and passing around hard-coded data.</span></span> <span data-ttu-id="4905a-143">次に、データベースを作成してデザインし、データを格納します。</span><span class="sxs-lookup"><span data-stu-id="4905a-143">Then we created and designed a Database and put some data it in.</span></span> <span data-ttu-id="4905a-144">データベースからデータを取得し、HTML テーブルに表示しました。</span><span class="sxs-lookup"><span data-stu-id="4905a-144">We retrieved the data from the database and displayed it in an HTML table.</span></span> <span data-ttu-id="4905a-145">その後、ユーザーが Web アプリケーション内からデータベース自体にデータを追加できるようにする Create フォームを追加しました。</span><span class="sxs-lookup"><span data-stu-id="4905a-145">Then we added a Create form that let the user add data to the database themselves from within the Web Application.</span></span> <span data-ttu-id="4905a-146">検証を追加し、クライアント側で検証を使用するようにしました。</span><span class="sxs-lookup"><span data-stu-id="4905a-146">We added validation, then made the validation use JavaScript on the client-side.</span></span> <span data-ttu-id="4905a-147">最後に、データの新しい列が含まれるようにデータベースを変更し、この新しいデータを作成して表示するように2つのページを更新しました。</span><span class="sxs-lookup"><span data-stu-id="4905a-147">Finally, we changed the database to include a new column of data, then updated our two pages to create and display this new data.</span></span>

<span data-ttu-id="4905a-148">ここでは、中級者向けのチュートリアル「[Mvc Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)」、および[https://asp.net/mvc](https://asp.net/mvc)にある多くのビデオとリソースを参照して、ASP.NET MVC についてさらに詳しく学習することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="4905a-148">I now encourage you to move on to our intermediate-level tutorial "[MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)" as well as the many videos and resources at [https://asp.net/mvc](https://asp.net/mvc) to learn even more about ASP.NET MVC!</span></span>

<span data-ttu-id="4905a-149">機能を有効にご活用ください。</span><span class="sxs-lookup"><span data-stu-id="4905a-149">Enjoy!</span></span>

- <span data-ttu-id="4905a-150">Scott マン Selman- [http://hanselman.com](http://hanselman.com) 、Twitter で[@shanselman](http://twitter.com/shanselman)ます。</span><span class="sxs-lookup"><span data-stu-id="4905a-150">Scott Hanselman - [http://hanselman.com](http://hanselman.com) and [@shanselman](http://twitter.com/shanselman) on Twitter.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="4905a-151">[[戻る]](getting-started-with-mvc-part7.md)</span><span class="sxs-lookup"><span data-stu-id="4905a-151">[Previous](getting-started-with-mvc-part7.md)</span></span>
