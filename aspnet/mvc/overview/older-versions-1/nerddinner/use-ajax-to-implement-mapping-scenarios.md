---
uid: mvc/overview/older-versions-1/nerddinner/use-ajax-to-implement-mapping-scenarios
title: AJAX を使用してマッピングシナリオを実装する |Microsoft Docs
author: microsoft
description: 手順 11. では、AJAX マッピングサポートをディナーアプリケーションに統合して、ユーザーがを作成、編集、または表示していることを確認する方法を示します。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: f731990a-0a81-4d62-81df-87d676cdedd6
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-ajax-to-implement-mapping-scenarios
msc.type: authoredcontent
ms.openlocfilehash: 7fc90f978b9f9eca511feca70a3c0d02ec69b940
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78468538"
---
# <a name="use-ajax-to-implement-mapping-scenarios"></a><span data-ttu-id="c1342-103">AJAX を使用し、マッピング シナリオを実装する</span><span class="sxs-lookup"><span data-stu-id="c1342-103">Use AJAX to Implement Mapping Scenarios</span></span>

<span data-ttu-id="c1342-104">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="c1342-104">by [Microsoft](https://github.com/microsoft)</span></span>

<span data-ttu-id="c1342-105">[[Download PDF]\(PDF をダウンロード\)](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)</span><span class="sxs-lookup"><span data-stu-id="c1342-105">[Download PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)</span></span>

> <span data-ttu-id="c1342-106">これは、ASP.NET MVC 1 を使用して小規模で完成した web アプリケーションを構築する方法を説明する無料の["" アプリケーションのチュートリアル](introducing-the-nerddinner-tutorial.md)の手順11です。</span><span class="sxs-lookup"><span data-stu-id="c1342-106">This is step 11 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="c1342-107">手順 11. では、AJAX マッピングサポートをディナーアプリケーションに統合する方法を示します。これにより、ユーザーがを作成、編集、または表示して、ディナーの場所をグラフィカルに表示できるようになります。</span><span class="sxs-lookup"><span data-stu-id="c1342-107">Step 11 shows how to integrate AJAX mapping support into our NerdDinner application, enabling users who are creating, editing or viewing dinners to see the location of the dinner graphically.</span></span>
> 
> <span data-ttu-id="c1342-108">ASP.NET MVC 3 を使用している場合は、MVC 3 または[Mvc ミュージックストア](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)[のチュートリアルではじめに](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)に従うことをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="c1342-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-11-integrating-an-ajax-map"></a><span data-ttu-id="c1342-109">手順 11: AJAX マップを統合する</span><span class="sxs-lookup"><span data-stu-id="c1342-109">NerdDinner Step 11: Integrating an AJAX Map</span></span>

<span data-ttu-id="c1342-110">AJAX マッピングのサポートを統合することで、アプリケーションをより視覚的に魅力的にすることができるようになります。</span><span class="sxs-lookup"><span data-stu-id="c1342-110">We'll now make our application a little more visually exciting by integrating AJAX mapping support.</span></span> <span data-ttu-id="c1342-111">これにより、ディナーを作成、編集、または表示して、ディナーの場所をグラフィカルに表示することができます。</span><span class="sxs-lookup"><span data-stu-id="c1342-111">This will enable users who are creating, editing or viewing dinners to see the location of the dinner graphically.</span></span>

### <a name="creating-a-map-partial-view"></a><span data-ttu-id="c1342-112">マップ部分ビューの作成</span><span class="sxs-lookup"><span data-stu-id="c1342-112">Creating a Map Partial View</span></span>

<span data-ttu-id="c1342-113">ここでは、アプリケーション内の複数の場所でマッピング機能を使用します。</span><span class="sxs-lookup"><span data-stu-id="c1342-113">We are going to use mapping functionality in several places within our application.</span></span> <span data-ttu-id="c1342-114">コードを乾いたままにするために、共通のマップ機能を1つの部分的なテンプレート内にカプセル化します。これは、複数のコントローラーアクションやビューで再利用できます。</span><span class="sxs-lookup"><span data-stu-id="c1342-114">To keep our code DRY we'll encapsulate the common map functionality within a single partial template that we can re-use across multiple controller actions and views.</span></span> <span data-ttu-id="c1342-115">この部分ビューに "map. .ascx" という名前を付け、\Views\Dinners ディレクトリ内に作成します。</span><span class="sxs-lookup"><span data-stu-id="c1342-115">We'll name this partial view "map.ascx" and create it within the \Views\Dinners directory.</span></span>

<span data-ttu-id="c1342-116">マップの .ascx 部分を作成するには、\Views\Dinners ディレクトリを右クリックし、[&gt;ビューの追加] メニューコマンドを選択します。</span><span class="sxs-lookup"><span data-stu-id="c1342-116">We can create the map.ascx partial by right-clicking on the \Views\Dinners directory and choosing the Add-&gt;View menu command.</span></span> <span data-ttu-id="c1342-117">ビューに "Map. .ascx" という名前を付け、部分ビューとしてチェックし、厳密に型指定された "ディナー" モデルクラスを渡すことを示します。</span><span class="sxs-lookup"><span data-stu-id="c1342-117">We'll name the view "Map.ascx", check it as a partial view, and indicate that we are going to pass it a strongly-typed "Dinner" model class:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image1.png)

<span data-ttu-id="c1342-118">[追加] ボタンをクリックすると、部分的なテンプレートが作成されます。</span><span class="sxs-lookup"><span data-stu-id="c1342-118">When we click the "Add" button our partial template will be created.</span></span> <span data-ttu-id="c1342-119">次に、次の内容が含まれるようにマップの .ascx ファイルを更新します。</span><span class="sxs-lookup"><span data-stu-id="c1342-119">We'll then update the Map.ascx file to have the following content:</span></span>

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample1.aspx)]

<span data-ttu-id="c1342-120">最初の &lt;スクリプト&gt; 参照ポイントは、Microsoft Virtual Earth 6.2 マッピングライブラリを指しています。</span><span class="sxs-lookup"><span data-stu-id="c1342-120">The first &lt;script&gt; reference points to the Microsoft Virtual Earth 6.2 mapping library.</span></span> <span data-ttu-id="c1342-121">2番目の &lt;スクリプト&gt; 参照は、一般的な Javascript マッピングロジックをカプセル化するために作成されるマップ .js ファイルを指します。</span><span class="sxs-lookup"><span data-stu-id="c1342-121">The second &lt;script&gt; reference points to a map.js file that we will shortly create which will encapsulate our common Javascript mapping logic.</span></span> <span data-ttu-id="c1342-122">&lt;div id = ""&gt; 要素 "は、Virtual Earth がマップをホストするために使用する HTML コンテナーです。</span><span class="sxs-lookup"><span data-stu-id="c1342-122">The &lt;div id="theMap"&gt; element is the HTML container that Virtual Earth will use to host the map.</span></span>

<span data-ttu-id="c1342-123">次に、このビューに固有の2つの JavaScript 関数を含む &lt;スクリプト&gt; が埋め込まれています。</span><span class="sxs-lookup"><span data-stu-id="c1342-123">We then have an embedded &lt;script&gt; block that contains two JavaScript functions specific to this view.</span></span> <span data-ttu-id="c1342-124">最初の関数は、jQuery を使用して、ページがクライアント側スクリプトを実行する準備ができたときに実行される関数を接続します。</span><span class="sxs-lookup"><span data-stu-id="c1342-124">The first function uses jQuery to wire-up a function that executes when the page is ready to run client-side script.</span></span> <span data-ttu-id="c1342-125">このメソッドは、virtual earth マップコントロールを読み込むために、マップの .js スクリプトファイル内で定義する LoadMap () ヘルパー関数を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="c1342-125">It calls a LoadMap() helper function that we'll define within our Map.js script file to load the virtual earth map control.</span></span> <span data-ttu-id="c1342-126">2番目の関数は、位置を識別するマップにピンを追加するコールバックイベントハンドラーです。</span><span class="sxs-lookup"><span data-stu-id="c1342-126">The second function is a callback event handler that adds a pin to the map that identifies a location.</span></span>

<span data-ttu-id="c1342-127">ここでは、クライアント側のスクリプトブロック内でサーバー側の &lt;% =%&gt; ブロックを使用して、コードを JavaScript にマップするディナーの緯度と経度を埋め込む方法に注目してください。</span><span class="sxs-lookup"><span data-stu-id="c1342-127">Notice how we are using a server-side &lt;%= %&gt; block within the client-side script block to embed the latitude and longitude of the Dinner we want to map into the JavaScript.</span></span> <span data-ttu-id="c1342-128">これは、クライアント側のスクリプトで使用できる動的な値を出力するための便利な手法です (値を取得するために、サーバーに対して個別の AJAX コールバックを必要とせず、値が高速になります)。</span><span class="sxs-lookup"><span data-stu-id="c1342-128">This is a useful technique to output dynamic values that can be used by client-side script (without requiring a separate AJAX call back to the server to retrieve the values – which makes it faster).</span></span> <span data-ttu-id="c1342-129">&lt;% =%&gt; ブロックは、ビューがサーバーでレンダリングされるときに実行されます。したがって、HTML の出力は、埋め込まれた JavaScript の値 (例: var 緯度 = 47.64312;) で終了します。</span><span class="sxs-lookup"><span data-stu-id="c1342-129">The &lt;%= %&gt; blocks will execute when the view is rendering on the server – and so the output of the HTML will just end up with embedded JavaScript values (for example: var latitude = 47.64312;).</span></span>

### <a name="creating-a-mapjs-utility-library"></a><span data-ttu-id="c1342-130">マップ .js ユーティリティライブラリの作成</span><span class="sxs-lookup"><span data-stu-id="c1342-130">Creating a Map.js utility library</span></span>

<span data-ttu-id="c1342-131">ここで、マップの JavaScript 機能をカプセル化するために使用できるマップ .js ファイルを作成します (さらに、上記の LoadMap メソッドと Loadmap メソッドを実装します)。</span><span class="sxs-lookup"><span data-stu-id="c1342-131">Let's now create the Map.js file that we can use to encapsulate the JavaScript functionality for our map (and implement the LoadMap and LoadPin methods above).</span></span> <span data-ttu-id="c1342-132">これを行うには、プロジェクト内の \Scripts ディレクトリを右クリックし、[新しい項目の&gt;追加] メニューコマンドを選択して、[JScript] 項目を選択し、"" という名前を付けます。</span><span class="sxs-lookup"><span data-stu-id="c1342-132">We can do this by right-clicking on the \Scripts directory within our project, and then choose the "Add-&gt;New Item" menu command, select the JScript item, and name it "Map.js".</span></span>

<span data-ttu-id="c1342-133">次に示すのは、Virtual Earth と対話してマップを表示し、ディナーの場所ピンを追加する、マップの .js ファイルに追加する JavaScript コードです。</span><span class="sxs-lookup"><span data-stu-id="c1342-133">Below is the JavaScript code we'll add to the Map.js file that will interact with Virtual Earth to display our map and add locations pins to it for our dinners:</span></span>

[!code-javascript[Main](use-ajax-to-implement-mapping-scenarios/samples/sample2.js)]

### <a name="integrating-the-map-with-create-and-edit-forms"></a><span data-ttu-id="c1342-134">マップを作成フォームと編集フォームに統合する</span><span class="sxs-lookup"><span data-stu-id="c1342-134">Integrating the Map with Create and Edit Forms</span></span>

<span data-ttu-id="c1342-135">ここでは、マップのサポートと既存の作成と編集のシナリオを統合します。</span><span class="sxs-lookup"><span data-stu-id="c1342-135">We'll now integrate the Map support with our existing Create and Edit scenarios.</span></span> <span data-ttu-id="c1342-136">すばらしいのは、これは非常に簡単な方法です。コントローラーコードを変更する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="c1342-136">The good news is that this is pretty easy to-do, and doesn't require us to change any of our Controller code.</span></span> <span data-ttu-id="c1342-137">作成ビューと編集ビューでは、ディナーフォーム UI を実装するための共通の "Dinフォーム" 部分ビューが共有されているため、マップを1か所に追加して、作成と編集の両方のシナリオで使用することができます。</span><span class="sxs-lookup"><span data-stu-id="c1342-137">Because our Create and Edit views share a common "DinnerForm" partial view to implement the dinner form UI, we can add the map in one place and have both our Create and Edit scenarios use it.</span></span>

<span data-ttu-id="c1342-138">\Views\Dinners\DinnerForm.ascx 部分ビューを開き、それを更新して新しいマップ部分を含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="c1342-138">All we need to-do is to open the \Views\Dinners\DinnerForm.ascx partial view and update it to include our new map partial.</span></span> <span data-ttu-id="c1342-139">次に示すのは、マップを追加した後に更新された Dinフォームがどのように表示されるかです (注: 簡潔にするために、HTML フォーム要素は次のコードスニペットから省略されています)。</span><span class="sxs-lookup"><span data-stu-id="c1342-139">Below is what the updated DinnerForm will look like once the map is added (note: the HTML form elements are omitted from the code snippet below for brevity):</span></span>

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample3.aspx)]

<span data-ttu-id="c1342-140">上記の "Din" フォームは、モデルの種類として "Dinという型のオブジェクトを取得します (これには、ディナーオブジェクトと、国の dropdownlist を設定するための SelectList が必要であるため)。</span><span class="sxs-lookup"><span data-stu-id="c1342-140">The DinnerForm partial above takes an object of type "DinnerFormViewModel" as its model type (because it needs both a Dinner object, as well as a SelectList to populate the dropdownlist of countries).</span></span> <span data-ttu-id="c1342-141">マップ部分には、モデルの種類として "ディナー" 型のオブジェクトだけが必要です。そのため、マップの一部をレンダリングするときには、Dinare Formビューモデルのディナーサブプロパティのみを渡しています。</span><span class="sxs-lookup"><span data-stu-id="c1342-141">Our Map partial just needs an object of type "Dinner" as its model type, and so when we render the map partial we are passing just the Dinner sub-property of DinnerFormViewModel to it:</span></span>

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample4.aspx)]

<span data-ttu-id="c1342-142">部分に追加した JavaScript 関数は jQuery を使用して "Address" HTML テキストボックスに "ぼかし" イベントをアタッチします。</span><span class="sxs-lookup"><span data-stu-id="c1342-142">The JavaScript function we've added to the partial uses jQuery to attach a "blur" event to the "Address" HTML textbox.</span></span> <span data-ttu-id="c1342-143">ユーザーがテキストボックスをクリックしたり、タブをクリックしたりしたときに発生する "フォーカス" イベントについて耳にすることがあります。</span><span class="sxs-lookup"><span data-stu-id="c1342-143">You've probably heard of "focus" events that fire when a user clicks or tabs into a textbox.</span></span> <span data-ttu-id="c1342-144">反対は、ユーザーがテキストボックスを終了したときに発生する "ぼかし" イベントです。</span><span class="sxs-lookup"><span data-stu-id="c1342-144">The opposite is a "blur" event that fires when a user exits a textbox.</span></span> <span data-ttu-id="c1342-145">上記のイベントハンドラーは、このような場合に緯度と経度のテキストボックスの値をクリアし、マップに新しいアドレスの場所をプロットします。</span><span class="sxs-lookup"><span data-stu-id="c1342-145">The above event handler clears the latitude and longitude textbox values when this happens, and then plots the new address location on our map.</span></span> <span data-ttu-id="c1342-146">その後、マップの .js ファイル内で定義されたコールバックイベントハンドラーによって、指定したアドレスに基づいて virtual earth から返された値を使用して、フォーム上の経度と緯度のテキストボックスが更新されます。</span><span class="sxs-lookup"><span data-stu-id="c1342-146">A callback event handler that we defined within the map.js file will then update the longitude and latitude textboxes on our form using values returned by virtual earth based on the address we gave it.</span></span>

<span data-ttu-id="c1342-147">ここでアプリケーションを再度実行し、[ホストディナー] タブをクリックすると、既定のマップが、標準のディナーフォーム要素と共に表示されます。</span><span class="sxs-lookup"><span data-stu-id="c1342-147">And now when we run our application again and click the "Host Dinner" tab we'll see a default map displayed along with our standard Dinner form elements:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image2.png)

<span data-ttu-id="c1342-148">アドレスを入力して tab キーを押したときに、マップが動的に更新されて場所が表示され、イベントハンドラーによって緯度/経度のテキストボックスに location 値が設定されます。</span><span class="sxs-lookup"><span data-stu-id="c1342-148">When we type in an address, and then tab away, the map will dynamically update to display the location, and our event handler will populate the latitude/longitude textboxes with the location values:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image3.png)

<span data-ttu-id="c1342-149">新しいディナーを保存し、編集のためにもう一度開いた場合は、ページが読み込まれるときにマップの場所が表示されていることがわかります。</span><span class="sxs-lookup"><span data-stu-id="c1342-149">If we save the new dinner and then open it again for editing, we'll find that the map location is displayed when the page loads:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image4.png)

<span data-ttu-id="c1342-150">Address フィールドが変更されるたびに、マップと緯度/経度の座標が更新されます。</span><span class="sxs-lookup"><span data-stu-id="c1342-150">Every time the address field is changed, the map and the latitude/longitude coordinates will update.</span></span>

<span data-ttu-id="c1342-151">これで、マップに夕食の場所が表示されるようになったので、緯度および経度のフォームフィールドを表示可能なテキストボックスから代わりに非表示の要素に変更することもできます (マップは住所が入力されるたびに自動的に更新されるため)。</span><span class="sxs-lookup"><span data-stu-id="c1342-151">Now that the map displays the Dinner location, we can also change the Latitude and Longitude form fields from being visible textboxes to instead be hidden elements (since the map is automatically updating them each time an address is entered).</span></span> <span data-ttu-id="c1342-152">これを行うには、.html () html ヘルパーを使用して、html. Hidden () ヘルパーメソッドを使用するように切り替えます。</span><span class="sxs-lookup"><span data-stu-id="c1342-152">To-do this we'll switch from using the Html.TextBox() HTML helper to using the Html.Hidden() helper method:</span></span>

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample5.aspx)]

<span data-ttu-id="c1342-153">これで、フォームはもう少しわかりやすくなり、生の緯度/経度が表示されないようになりました (ただし、各ディナーをデータベースに格納します)。</span><span class="sxs-lookup"><span data-stu-id="c1342-153">And now our forms are a little more user-friendly and avoid displaying the raw latitude/longitude (while still storing them with each Dinner in the database):</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image5.png)

### <a name="integrating-the-map-with-the-details-view"></a><span data-ttu-id="c1342-154">マップと詳細ビューの統合</span><span class="sxs-lookup"><span data-stu-id="c1342-154">Integrating the Map with the Details View</span></span>

<span data-ttu-id="c1342-155">これで、作成と編集のシナリオにマップが統合されたので、詳細なシナリオと統合することもできます。</span><span class="sxs-lookup"><span data-stu-id="c1342-155">Now that we have the map integrated with our Create and Edit scenarios, let's also integrate it with our Details scenario.</span></span> <span data-ttu-id="c1342-156">&lt;% .Html 部分 ("map") を呼び出す必要があります。詳細ビュー内の%&gt;。</span><span class="sxs-lookup"><span data-stu-id="c1342-156">All we need to-do is to call &lt;% Html.RenderPartial("map"); %&gt; within the Details view.</span></span>

<span data-ttu-id="c1342-157">完全な詳細ビュー (マップの統合を使用) のソースコードは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="c1342-157">Below is what the source code to the complete Details view (with map integration) looks like:</span></span>

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample6.aspx)]

<span data-ttu-id="c1342-158">これで、ユーザーが//詳細/[id] の URL に移動すると、ディナーに関する詳細が表示されます。マップ上のディナーの場所 (ホバー時にマウスポインターを置いたときにプッシュピンを使用して完了すると、その連絡先のタイトルが表示されます) と、それに対する AJAX リンクがあります。</span><span class="sxs-lookup"><span data-stu-id="c1342-158">And now when a user navigates to a /Dinners/Details/[id] URL they'll see details about the dinner, the location of the dinner on the map (complete with a push-pin that when hovered over displays the title of the dinner and the address of it), and have an AJAX link to RSVP for it:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image6.png)

### <a name="implementing-location-search-in-our-database-and-repository"></a><span data-ttu-id="c1342-159">データベースとリポジトリでの場所検索の実装</span><span class="sxs-lookup"><span data-stu-id="c1342-159">Implementing Location Search in our Database and Repository</span></span>

<span data-ttu-id="c1342-160">AJAX の実装を終了するには、アプリケーションのホームページにマップを追加して、ユーザーが近くにあるディナーをグラフィカルに検索できるようにしましょう。</span><span class="sxs-lookup"><span data-stu-id="c1342-160">To finish off our AJAX implementation, let's add a Map to the home page of the application that allows users to graphically search for dinners near them.</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image7.png)

<span data-ttu-id="c1342-161">まず、データベースとデータリポジトリレイヤー内にサポートを実装して、ディナーの場所ベースの radius 検索を効率的に実行します。</span><span class="sxs-lookup"><span data-stu-id="c1342-161">We'll begin by implementing support within our database and data repository layer to efficiently perform a location-based radius search for Dinners.</span></span> <span data-ttu-id="c1342-162">[Sql 2008 の新しい地理空間機能](https://www.microsoft.com/sqlserver/2008/en/us/spatial-data.aspx)を使用してこれを実装できます。または、次の記事で説明されているような sql 関数の手法を使用することもできます[http://www.codeproject.com/KB/cs/distancebetweenlocations.aspx](http://www.codeproject.com/KB/cs/distancebetweenlocations.aspx) 。詳細については、LINQ to SQL での使用については、「」を参照してください: [http://blog.wekeroad.com/2007/08/30/linq-and-geocoding/](http://blog.wekeroad.com/2007/08/30/linq-and-geocoding/)</span><span class="sxs-lookup"><span data-stu-id="c1342-162">We could use the new [geospatial features of SQL 2008](https://www.microsoft.com/sqlserver/2008/en/us/spatial-data.aspx) to implement this, or alternatively we can use a SQL function approach that Gary Dryden discussed in article here: [http://www.codeproject.com/KB/cs/distancebetweenlocations.aspx](http://www.codeproject.com/KB/cs/distancebetweenlocations.aspx) and Rob Conery blogged about using with LINQ to SQL here: [http://blog.wekeroad.com/2007/08/30/linq-and-geocoding/](http://blog.wekeroad.com/2007/08/30/linq-and-geocoding/)</span></span>

<span data-ttu-id="c1342-163">この手法を実装するには、Visual Studio 内で "サーバーエクスプローラー" を開き、そのデータベースを選択してから、その下の "functions" サブノードを右クリックして、新しい "スカラー値関数" を作成します。</span><span class="sxs-lookup"><span data-stu-id="c1342-163">To implement this technique, we will open the "Server Explorer" within Visual Studio, select the NerdDinner database, and then right-click on the "functions" sub-node under it and choose to create a new "Scalar-valued function":</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image8.png)

<span data-ttu-id="c1342-164">次の DistanceBetween 関数を貼り付けます。</span><span class="sxs-lookup"><span data-stu-id="c1342-164">We'll then paste in the following DistanceBetween function:</span></span>

[!code-sql[Main](use-ajax-to-implement-mapping-scenarios/samples/sample7.sql)]

<span data-ttu-id="c1342-165">次に、"NearestDinners" を呼び出す新しいテーブル値関数 SQL Server を作成します。</span><span class="sxs-lookup"><span data-stu-id="c1342-165">We'll then create a new table-valued function in SQL Server that we'll call "NearestDinners":</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image9.png)

<span data-ttu-id="c1342-166">この "NearestDinners" テーブル関数は、DistanceBetween helper 関数を使用して、緯度の100マイル以内にすべてのディナーを返し、経度を指定します。</span><span class="sxs-lookup"><span data-stu-id="c1342-166">This "NearestDinners" table function uses the DistanceBetween helper function to return all Dinners within 100 miles of the latitude and longitude we supply it:</span></span>

[!code-sql[Main](use-ajax-to-implement-mapping-scenarios/samples/sample8.sql)]

<span data-ttu-id="c1342-167">この関数を呼び出すには、最初に、次のように、-model ディレクトリ内のファイルをダブルクリックして LINQ to SQL デザイナーを開きます。</span><span class="sxs-lookup"><span data-stu-id="c1342-167">To call this function, we'll first open up the LINQ to SQL designer by double-clicking on the NerdDinner.dbml file within our \Models directory:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image10.png)

<span data-ttu-id="c1342-168">次に、NearestDinners 関数と DistanceBetween 関数を LINQ to SQL デザイナーにドラッグします。これにより、LINQ to SQL でメソッドとして追加されます。</span><span class="sxs-lookup"><span data-stu-id="c1342-168">We'll then drag the NearestDinners and DistanceBetween functions onto the LINQ to SQL designer, which will cause them to be added as methods on our LINQ to SQL NerdDinnerDataContext class:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image11.png)

<span data-ttu-id="c1342-169">次に、NearestDinner 関数を使用して、指定された場所の100マイル以内にある今後のディナーを返す、Dinのリポジトリクラスで "FindByLocation" クエリメソッドを公開できます。</span><span class="sxs-lookup"><span data-stu-id="c1342-169">We can then expose a "FindByLocation" query method on our DinnerRepository class that uses the NearestDinner function to return upcoming Dinners that are within 100 miles of the specified location:</span></span>

[!code-csharp[Main](use-ajax-to-implement-mapping-scenarios/samples/sample9.cs)]

### <a name="implementing-a-json-based-ajax-search-action-method"></a><span data-ttu-id="c1342-170">JSON ベースの AJAX 検索アクションメソッドの実装</span><span class="sxs-lookup"><span data-stu-id="c1342-170">Implementing a JSON-based AJAX Search Action Method</span></span>

<span data-ttu-id="c1342-171">ここでは、新しい FindByLocation () リポジトリメソッドを利用して、マップの設定に使用できるディナーデータのリストを返すコントローラーアクションメソッドを実装します。</span><span class="sxs-lookup"><span data-stu-id="c1342-171">We'll now implement a controller action method that takes advantage of the new FindByLocation() repository method to return back a list of Dinner data that can be used to populate a map.</span></span> <span data-ttu-id="c1342-172">このアクションメソッドによって、クライアント上で JavaScript を使用して簡単に操作できるように、ディナーデータを JSON (JavaScript Object Notation) 形式で返すことができます。</span><span class="sxs-lookup"><span data-stu-id="c1342-172">We'll have this action method return back the Dinner data in a JSON (JavaScript Object Notation) format so that it can be easily manipulated using JavaScript on the client.</span></span>

<span data-ttu-id="c1342-173">これを実装するには、新しい "SearchController" クラスを作成します。そのためには、\ Controllers ディレクトリを右クリックし、[&gt;コントローラー] メニューコマンドを選択します。</span><span class="sxs-lookup"><span data-stu-id="c1342-173">To implement this, we'll create a new "SearchController" class by right-clicking on the \Controllers directory and choosing the Add-&gt;Controller menu command.</span></span> <span data-ttu-id="c1342-174">その後、次のように、新しい SearchController クラス内に "SearchByLocation" アクションメソッドを実装します。</span><span class="sxs-lookup"><span data-stu-id="c1342-174">We'll then implement a "SearchByLocation" action method within the new SearchController class like below:</span></span>

[!code-csharp[Main](use-ajax-to-implement-mapping-scenarios/samples/sample10.cs)]

<span data-ttu-id="c1342-175">SearchController の SearchByLocation アクションメソッドは、内部的にディナーの一覧を取得するために、FindByLocation メソッドを Dinに呼び出します。</span><span class="sxs-lookup"><span data-stu-id="c1342-175">The SearchController's SearchByLocation action method internally calls the FindByLocation method on DinnerRepository to get a list of nearby dinners.</span></span> <span data-ttu-id="c1342-176">ただし、ディナーオブジェクトをクライアントに直接返すのではなく、代わりに JsonDinner オブジェクトを返します。</span><span class="sxs-lookup"><span data-stu-id="c1342-176">Rather than return the Dinner objects directly to the client, though, it instead returns JsonDinner objects.</span></span> <span data-ttu-id="c1342-177">JsonDinner クラスは、ディナープロパティのサブセットを公開します (たとえば、セキュリティ上の理由から、ディナーを持つユーザーの名前は開示しません)。</span><span class="sxs-lookup"><span data-stu-id="c1342-177">The JsonDinner class exposes a subset of Dinner properties (for example: for security reasons it doesn't disclose the names of the people who have RSVP'd for a dinner).</span></span> <span data-ttu-id="c1342-178">また、ディナーには存在しない RSVPCount プロパティも含まれており、特定のディナーに関連付けられている RSVP オブジェクトの数をカウントすることによって動的に計算されます。</span><span class="sxs-lookup"><span data-stu-id="c1342-178">It also includes an RSVPCount property that doesn't exist on Dinner– and which is dynamically calculated by counting the number of RSVP objects associated with a particular dinner.</span></span>

<span data-ttu-id="c1342-179">次に、コントローラーの基本クラスで Json () ヘルパーメソッドを使用して、JSON ベースのワイヤ形式を使用してディナーのシーケンスを返します。</span><span class="sxs-lookup"><span data-stu-id="c1342-179">We are then using the Json() helper method on the Controller base class to return the sequence of dinners using a JSON-based wire format.</span></span> <span data-ttu-id="c1342-180">JSON は、単純なデータ構造を表すための標準的なテキスト形式です。</span><span class="sxs-lookup"><span data-stu-id="c1342-180">JSON is a standard text format for representing simple data-structures.</span></span> <span data-ttu-id="c1342-181">次に、アクションメソッドから返されたときに、2つの JsonDinner オブジェクトの JSON 形式のリストがどのように見えるかを示します。</span><span class="sxs-lookup"><span data-stu-id="c1342-181">Below is an example of what a JSON-formatted list of two JsonDinner objects looks like when returned from our action method:</span></span>

[!code-json[Main](use-ajax-to-implement-mapping-scenarios/samples/sample11.json)]

### <a name="calling-the-json-based-ajax-method-using-jquery"></a><span data-ttu-id="c1342-182">JQuery を使用した JSON ベースの AJAX メソッドの呼び出し</span><span class="sxs-lookup"><span data-stu-id="c1342-182">Calling the JSON-based AJAX method using jQuery</span></span>

<span data-ttu-id="c1342-183">次に、SearchController の SearchByLocation アクションメソッドを使用するように、このアプリケーションのホームページを更新する準備ができました。</span><span class="sxs-lookup"><span data-stu-id="c1342-183">We are now ready to update the home page of the NerdDinner application to use the SearchController's SearchByLocation action method.</span></span> <span data-ttu-id="c1342-184">これを行うには、/Views/Home/Index.aspx view テンプレートを開き、テキストボックス、検索ボタン、マップ、および &lt;div&gt; 要素を含むように更新します。</span><span class="sxs-lookup"><span data-stu-id="c1342-184">To-do this, we'll open the /Views/Home/Index.aspx view template and update it to have a textbox, search button, our map, and a &lt;div&gt; element named dinnerList:</span></span>

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample12.aspx)]

<span data-ttu-id="c1342-185">その後、次の2つの JavaScript 関数をページに追加できます。</span><span class="sxs-lookup"><span data-stu-id="c1342-185">We can then add two JavaScript functions to the page:</span></span>

[!code-html[Main](use-ajax-to-implement-mapping-scenarios/samples/sample13.html)]

<span data-ttu-id="c1342-186">最初の JavaScript 関数は、ページが最初に読み込まれたときにマップを読み込みます。</span><span class="sxs-lookup"><span data-stu-id="c1342-186">The first JavaScript function loads the map when the page first loads.</span></span> <span data-ttu-id="c1342-187">2番目の JavaScript 関数は、[検索] ボタンに JavaScript のクリックイベントハンドラーを配線します。</span><span class="sxs-lookup"><span data-stu-id="c1342-187">The second JavaScript function wires up a JavaScript click event handler on the search button.</span></span> <span data-ttu-id="c1342-188">このボタンが押されると、次のように、マップの .js ファイルに追加する Finddinの Location () JavaScript 関数が呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="c1342-188">When the button is pressed it calls the FindDinnersGivenLocation() JavaScript function which we'll add to our Map.js file:</span></span>

[!code-javascript[Main](use-ajax-to-implement-mapping-scenarios/samples/sample14.js)]

<span data-ttu-id="c1342-189">この Finddinの Sいい Location () 関数は map を呼び出します。Virtual Earth コントロールで () を検索し、入力した場所に中央揃えで配置します。</span><span class="sxs-lookup"><span data-stu-id="c1342-189">This FindDinnersGivenLocation() function calls map.Find() on the Virtual Earth Control to center it on the entered location.</span></span> <span data-ttu-id="c1342-190">Virtual earth マップサービスが戻ると、マップが返されます。Find () メソッドは、最後の引数として渡された callbackUpdateMapDinners callback メソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="c1342-190">When the virtual earth map service returns, the map.Find() method invokes the callbackUpdateMapDinners callback method we passed it as the final argument.</span></span>

<span data-ttu-id="c1342-191">CallbackUpdateMapDinners () メソッドは、実際の作業が行われる場所です。</span><span class="sxs-lookup"><span data-stu-id="c1342-191">The callbackUpdateMapDinners() method is where the real work is done.</span></span> <span data-ttu-id="c1342-192">JQuery の $. post () ヘルパーメソッドを使用して、SearchController の SearchByLocation () アクションメソッドに対する AJAX 呼び出しを実行します。これは、新しく中央に配置されたマップの緯度と経度を渡します。</span><span class="sxs-lookup"><span data-stu-id="c1342-192">It uses jQuery's $.post() helper method to perform an AJAX call to our SearchController's SearchByLocation() action method – passing it the latitude and longitude of the newly centered map.</span></span> <span data-ttu-id="c1342-193">これは、$ post () ヘルパーメソッドが完了したときに呼び出されるインライン関数を定義します。また、SearchByLocation () アクションメソッドから返される JSON 形式のディナー結果は、"ディナー" という変数を使用して渡されます。</span><span class="sxs-lookup"><span data-stu-id="c1342-193">It defines an inline function that will be called when the $.post() helper method completes, and the JSON-formatted dinner results returned from the SearchByLocation() action method will be passed it using a variable called "dinners".</span></span> <span data-ttu-id="c1342-194">次に、返された各ディナーで foreach を行い、ディナーの緯度と経度、およびその他のプロパティを使用してマップに新しい pin を追加します。</span><span class="sxs-lookup"><span data-stu-id="c1342-194">It then does a foreach over each returned dinner, and uses the dinner's latitude and longitude and other properties to add a new pin on the map.</span></span> <span data-ttu-id="c1342-195">また、マップの右側にあるディナーの HTML リストに夕食エントリが追加されます。</span><span class="sxs-lookup"><span data-stu-id="c1342-195">It also adds a dinner entry to the HTML list of dinners to the right of the map.</span></span> <span data-ttu-id="c1342-196">次に、プッシュピンと HTML リストの両方のホバーイベントをワイヤアップします。これにより、ユーザーがマウスを置いたときにディナーの詳細が表示されます。</span><span class="sxs-lookup"><span data-stu-id="c1342-196">It then wires-up a hover event for both the pushpins and the HTML list so that details about the dinner are displayed when a user hovers over them:</span></span>

[!code-html[Main](use-ajax-to-implement-mapping-scenarios/samples/sample15.html)]

<span data-ttu-id="c1342-197">アプリケーションを実行してホームページにアクセスすると、マップが表示されます。</span><span class="sxs-lookup"><span data-stu-id="c1342-197">And now when we run the application and visit the home-page we'll be presented with a map.</span></span> <span data-ttu-id="c1342-198">市区町村の名前を入力すると、マップに近い将来のディナーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="c1342-198">When we enter the name of a city the map will display the upcoming dinners near it:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image12.png)

<span data-ttu-id="c1342-199">ディナーをポイントすると、その詳細が表示されます。</span><span class="sxs-lookup"><span data-stu-id="c1342-199">Hovering over a dinner will display details about it.</span></span>

<span data-ttu-id="c1342-200">バブルまたは HTML リストの右側にあるディナーのタイトルをクリックすると、ディナーに移動します。これにより、必要に応じて次のことを行うことができます。</span><span class="sxs-lookup"><span data-stu-id="c1342-200">Clicking the Dinner title either in the bubble or on the right-hand side in the HTML list will navigate us to the dinner – which we can then optionally RSVP for:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image13.png)

### <a name="next-step"></a><span data-ttu-id="c1342-201">次の手順</span><span class="sxs-lookup"><span data-stu-id="c1342-201">Next Step</span></span>

<span data-ttu-id="c1342-202">これで、世界中のアプリケーションのすべての機能を実装しました。</span><span class="sxs-lookup"><span data-stu-id="c1342-202">We've now implemented all the application functionality of our NerdDinner application.</span></span> <span data-ttu-id="c1342-203">ここでは、自動化された単体テストを有効にする方法を見てみましょう。</span><span class="sxs-lookup"><span data-stu-id="c1342-203">Let's now look at how we can enable automated unit testing of it.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c1342-204">[前へ](use-ajax-to-deliver-dynamic-updates.md)
> [次へ](enable-automated-unit-testing.md)</span><span class="sxs-lookup"><span data-stu-id="c1342-204">[Previous](use-ajax-to-deliver-dynamic-updates.md)
[Next](enable-automated-unit-testing.md)</span></span>
