---
uid: mvc/overview/older-versions-1/nerddinner/use-ajax-to-deliver-dynamic-updates
title: AJAX を使用して動的更新を配信する |Microsoft Docs
author: microsoft
description: 手順10では、ログインしているユーザーが、ディナーの詳細に統合された Ajax ベースのアプローチを使用して、ディナーに参加することに関心があることを RSVP に対してサポートします。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 18700815-8e6c-4489-91af-7ea9dab6529e
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-ajax-to-deliver-dynamic-updates
msc.type: authoredcontent
ms.openlocfilehash: 3edc02fec546609505b5e085440fa684abe7acd0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486310"
---
# <a name="use-ajax-to-deliver-dynamic-updates"></a><span data-ttu-id="60e4e-103">AJAX を使用し、動的更新を配信する</span><span class="sxs-lookup"><span data-stu-id="60e4e-103">Use AJAX to Deliver Dynamic Updates</span></span>

<span data-ttu-id="60e4e-104">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="60e4e-104">by [Microsoft](https://github.com/microsoft)</span></span>

<span data-ttu-id="60e4e-105">[[Download PDF]\(PDF をダウンロード\)](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)</span><span class="sxs-lookup"><span data-stu-id="60e4e-105">[Download PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)</span></span>

> <span data-ttu-id="60e4e-106">これは、ASP.NET MVC 1 を使用して小規模で完成した web アプリケーションを構築する方法について説明する無料の["" アプリケーションのチュートリアル](introducing-the-nerddinner-tutorial.md)の手順10です。</span><span class="sxs-lookup"><span data-stu-id="60e4e-106">This is step 10 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="60e4e-107">手順10では、ログインしているユーザーが、ディナーの詳細ページに統合された Ajax ベースのアプローチを使用して、ディナーに参加することを目的として RSVP を管理します。</span><span class="sxs-lookup"><span data-stu-id="60e4e-107">Step 10 implements support for logged-in users to RSVP their interest in attending a dinner, using an Ajax-based approach integrated within the dinner details page.</span></span>
> 
> <span data-ttu-id="60e4e-108">ASP.NET MVC 3 を使用している場合は、MVC 3 または[Mvc ミュージックストア](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)[のチュートリアルではじめに](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)に従うことをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="60e4e-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-10-ajax-enabling-rsvps-accepts"></a><span data-ttu-id="60e4e-109">ステップ 10: AJAX で RSVPs を有効にする</span><span class="sxs-lookup"><span data-stu-id="60e4e-109">NerdDinner Step 10: AJAX Enabling RSVPs Accepts</span></span>

<span data-ttu-id="60e4e-110">次に、ログインしているユーザーのサポートを実装して、ディナーに参加することを目的としています。</span><span class="sxs-lookup"><span data-stu-id="60e4e-110">Let's now implement support for logged-in users to RSVP their interest in attending a dinner.</span></span> <span data-ttu-id="60e4e-111">これは、ディナーの詳細ページで統合された AJAX ベースのアプローチを使用して有効にします。</span><span class="sxs-lookup"><span data-stu-id="60e4e-111">We'll enable this using an AJAX-based approach integrated within the dinner details page.</span></span>

### <a name="indicating-whether-the-user-is-rsvpd"></a><span data-ttu-id="60e4e-112">ユーザーが RSVP であるかどうかを示す</span><span class="sxs-lookup"><span data-stu-id="60e4e-112">Indicating whether the user is RSVP'd</span></span>

<span data-ttu-id="60e4e-113">ユーザーは、 *[id*] の URL にアクセスして、特定のディナーに関する詳細を確認できます。</span><span class="sxs-lookup"><span data-stu-id="60e4e-113">Users can visit the */Dinners/Details/[id*] URL to see details about a particular dinner:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image1.png)

<span data-ttu-id="60e4e-114">Details () アクションメソッドは、次のように実装されます。</span><span class="sxs-lookup"><span data-stu-id="60e4e-114">The Details() action method is implemented like so:</span></span>

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample1.cs)]

<span data-ttu-id="60e4e-115">RSVP サポートを実装する最初の手順として、先ほど作成した Dinner.cs 部分クラス内で、"IsUserRegistered (username)" ヘルパーメソッドをディナーオブジェクトに追加します。</span><span class="sxs-lookup"><span data-stu-id="60e4e-115">Our first step to implement RSVP support will be to add an "IsUserRegistered(username)" helper method to our Dinner object (within the Dinner.cs partial class we built earlier).</span></span> <span data-ttu-id="60e4e-116">このヘルパーメソッドは、ユーザーが現在ディナーであるかどうかによって、true または false を返します。</span><span class="sxs-lookup"><span data-stu-id="60e4e-116">This helper method returns true or false depending on whether the user is currently RSVP'd for the Dinner:</span></span>

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample2.cs)]

<span data-ttu-id="60e4e-117">その後、次のコードを Details ビューテンプレートに追加して、ユーザーがイベントに対して登録されているかどうかを示す適切なメッセージを表示することができます。</span><span class="sxs-lookup"><span data-stu-id="60e4e-117">We can then add the following code to our Details.aspx view template to display an appropriate message indicating whether the user is registered or not for the event:</span></span>

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample3.html)]

<span data-ttu-id="60e4e-118">これで、ユーザーがディナーにアクセスすると、次のメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="60e4e-118">And now when a user visits a Dinner they are registered for they'll see this message:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image2.png)

<span data-ttu-id="60e4e-119">また、お客様がディナーにアクセスすると、次のメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="60e4e-119">And when they visit a Dinner they are not registered for they'll see the below message:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image3.png)

### <a name="implementing-the-register-action-method"></a><span data-ttu-id="60e4e-120">Register アクションメソッドの実装</span><span class="sxs-lookup"><span data-stu-id="60e4e-120">Implementing the Register Action Method</span></span>

<span data-ttu-id="60e4e-121">次に、ユーザーが [詳細] ページからディナーを使用できるようにするために必要な機能を追加してみましょう。</span><span class="sxs-lookup"><span data-stu-id="60e4e-121">Let's now add the functionality necessary to enable users to RSVP for a dinner from the details page.</span></span>

<span data-ttu-id="60e4e-122">これを実装するには、新しい "RSVPController" クラスを作成します。そのためには、\ Controllers ディレクトリを右クリックし、[&gt;コントローラー] メニューコマンドを選択します。</span><span class="sxs-lookup"><span data-stu-id="60e4e-122">To implement this, we'll create a new "RSVPController" class by right-clicking on the \Controllers directory and choosing the Add-&gt;Controller menu command.</span></span>

<span data-ttu-id="60e4e-123">新しい RSVPController クラス内に "Register" アクションメソッドを実装します。このクラスは、ディナーの id を引数として受け取り、適切なディナーオブジェクトを取得し、ログインしているユーザーが現在、登録されているユーザーの一覧にあるかどうかを確認します。では、次のように RSVP オブジェクトが追加されません。</span><span class="sxs-lookup"><span data-stu-id="60e4e-123">We'll implement a "Register" action method within the new RSVPController class that takes an id for a Dinner as an argument, retrieves the appropriate Dinner object, checks to see if the logged-in user is currently in the list of users who have registered for it, and if not adds an RSVP object for them:</span></span>

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample4.cs)]

<span data-ttu-id="60e4e-124">ここでは、アクションメソッドの出力として簡単な文字列を返す方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="60e4e-124">Notice above how we are returning a simple string as the output of the action method.</span></span> <span data-ttu-id="60e4e-125">ビューテンプレート内にこのメッセージを埋め込むこともできますが、そのため、コントローラーの基本クラスで Content () ヘルパーメソッドを使用し、上記のような文字列メッセージを返すだけです。</span><span class="sxs-lookup"><span data-stu-id="60e4e-125">We could have embedded this message within a view template – but since it is so small we'll just use the Content() helper method on the controller base class and return a string message like above.</span></span>

### <a name="calling-the-rsvpforevent-action-method-using-ajax"></a><span data-ttu-id="60e4e-126">AJAX を使用した RSVPForEvent アクションメソッドの呼び出し</span><span class="sxs-lookup"><span data-stu-id="60e4e-126">Calling the RSVPForEvent Action Method using AJAX</span></span>

<span data-ttu-id="60e4e-127">AJAX を使用して、詳細ビューからレジスタアクションメソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="60e4e-127">We'll use AJAX to invoke the Register action method from our Details view.</span></span> <span data-ttu-id="60e4e-128">この実装は非常に簡単です。</span><span class="sxs-lookup"><span data-stu-id="60e4e-128">Implementing this is pretty easy.</span></span> <span data-ttu-id="60e4e-129">まず、2つのスクリプトライブラリ参照を追加します。</span><span class="sxs-lookup"><span data-stu-id="60e4e-129">First we'll add two script library references:</span></span>

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample5.html)]

<span data-ttu-id="60e4e-130">最初のライブラリは、中核となる ASP.NET AJAX クライアント側スクリプトライブラリを参照します。</span><span class="sxs-lookup"><span data-stu-id="60e4e-130">The first library references the core ASP.NET AJAX client-side script library.</span></span> <span data-ttu-id="60e4e-131">このファイルのサイズは約24k で、クライアント側の AJAX のコア機能が含まれています。</span><span class="sxs-lookup"><span data-stu-id="60e4e-131">This file is approximately 24k in size (compressed) and contains core client-side AJAX functionality.</span></span> <span data-ttu-id="60e4e-132">2番目のライブラリには、ASP.NET MVC の組み込み AJAX ヘルパーメソッドと統合するユーティリティ関数が含まれています (これはすぐに使用します)。</span><span class="sxs-lookup"><span data-stu-id="60e4e-132">The second library contains utility functions that integrate with ASP.NET MVC's built-in AJAX helper methods (which we'll use shortly).</span></span>

<span data-ttu-id="60e4e-133">その後、先ほど追加したビューテンプレートコードを更新して、"このイベントに登録されていません" というメッセージを出力するのではなく、プッシュ時に、その RSVP コントローラーで RSVPForEvent アクションメソッドを呼び出す AJAX 呼び出しを実行するリンクをレンダリングします。ユーザーを RSVPs します。</span><span class="sxs-lookup"><span data-stu-id="60e4e-133">We can then update the view template code we added earlier so that instead of outputting a "You are not registered for this event" message, we instead render a link that when pushed performs an AJAX call that invokes our RSVPForEvent action method on our RSVP controller and RSVPs the user:</span></span>

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample6.aspx)]

<span data-ttu-id="60e4e-134">上記で使用した Html.actionlink () ヘルパーメソッドは ASP.NET MVC に組み込まれており、Html.actionlink () ヘルパーメソッドに似ています。ただし、標準ナビゲーションを実行する代わりに、リンクをクリックすると、AJAX 呼び出しがアクションメソッドに対して行われる点が異なります。</span><span class="sxs-lookup"><span data-stu-id="60e4e-134">The Ajax.ActionLink() helper method used above is built-into ASP.NET MVC and is similar to the Html.ActionLink() helper method except that instead of performing a standard navigation it makes an AJAX call to the action method when the link is clicked.</span></span> <span data-ttu-id="60e4e-135">上記の例では、"RSVP" コントローラーで "Register" アクションメソッドを呼び出し、その Id を "id" パラメーターとして渡しています。</span><span class="sxs-lookup"><span data-stu-id="60e4e-135">Above we are calling the "Register" action method on the "RSVP" controller and passing the DinnerID as the "id" parameter to it.</span></span> <span data-ttu-id="60e4e-136">渡される最後の AjaxOptions パラメーターは、アクションメソッドから返されたコンテンツを取得し、id が "rsvpmsg" であるページの HTML &lt;div&gt; 要素を更新することを示します。</span><span class="sxs-lookup"><span data-stu-id="60e4e-136">The final AjaxOptions parameter we are passing indicates that we want to take the content returned from the action method and update the HTML &lt;div&gt; element on the page whose id is "rsvpmsg".</span></span>

<span data-ttu-id="60e4e-137">これで、ユーザーが夕食に登録されていない場合は、それに対する RSVP へのリンクが表示されます。</span><span class="sxs-lookup"><span data-stu-id="60e4e-137">And now when a user browses to a dinner they aren't registered for yet they'll see a link to RSVP for it:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image4.png)

<span data-ttu-id="60e4e-138">これらのユーザーが "このイベントの RSVP" リンクをクリックすると、次のようなメッセージが表示され、それが完了すると、次のようなメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="60e4e-138">If they click the "RSVP for this event" link they'll make an AJAX call to the Register action method on the RSVP controller, and when it completes they'll see an updated message like below:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image5.png)

<span data-ttu-id="60e4e-139">この AJAX 呼び出しを行う際に関係するネットワーク帯域幅とトラフィックは、非常に軽量です。</span><span class="sxs-lookup"><span data-stu-id="60e4e-139">The network bandwidth and traffic involved when making this AJAX call is really lightweight.</span></span> <span data-ttu-id="60e4e-140">ユーザーが [このイベントの RSVP] リンクをクリックすると、次のような */Dinners/Register/1* URL に対して小さな HTTP POST ネットワーク要求が行われます。</span><span class="sxs-lookup"><span data-stu-id="60e4e-140">When the user clicks on the "RSVP for this event" link, a small HTTP POST network request is made to the */Dinners/Register/1* URL that looks like below on the wire:</span></span>

[!code-console[Main](use-ajax-to-deliver-dynamic-updates/samples/sample7.cmd)]

<span data-ttu-id="60e4e-141">また、登録アクションメソッドからの応答は、単純に次のようになります。</span><span class="sxs-lookup"><span data-stu-id="60e4e-141">And the response from our Register action method is simply:</span></span>

[!code-console[Main](use-ajax-to-deliver-dynamic-updates/samples/sample8.cmd)]

<span data-ttu-id="60e4e-142">この軽量な呼び出しは高速で、低速のネットワークでも機能します。</span><span class="sxs-lookup"><span data-stu-id="60e4e-142">This lightweight call is fast and will work even over a slow network.</span></span>

### <a name="adding-a-jquery-animation"></a><span data-ttu-id="60e4e-143">JQuery アニメーションの追加</span><span class="sxs-lookup"><span data-stu-id="60e4e-143">Adding a jQuery Animation</span></span>

<span data-ttu-id="60e4e-144">実装した AJAX の機能は、適切で高速に動作します。</span><span class="sxs-lookup"><span data-stu-id="60e4e-144">The AJAX functionality we implemented works well and fast.</span></span> <span data-ttu-id="60e4e-145">場合によっては、RSVP リンクが新しいテキストに置き換えられたことがユーザーに通知されないことがあります。</span><span class="sxs-lookup"><span data-stu-id="60e4e-145">Sometimes it can happen so fast, though, that a user might not notice that the RSVP link has been replaced with new text.</span></span> <span data-ttu-id="60e4e-146">結果を少し明確にするために、更新メッセージに注目する単純なアニメーションを追加できます。</span><span class="sxs-lookup"><span data-stu-id="60e4e-146">To make the outcome a little more obvious we can add a simple animation to draw attention to the update message.</span></span>

<span data-ttu-id="60e4e-147">既定の ASP.NET MVC プロジェクトテンプレートには、jQuery – Microsoft でもサポートされている、優れた (かつ人気のある) オープンソース JavaScript ライブラリが含まれています。</span><span class="sxs-lookup"><span data-stu-id="60e4e-147">The default ASP.NET MVC project template includes jQuery – an excellent (and very popular) open source JavaScript library that is also supported by Microsoft.</span></span> <span data-ttu-id="60e4e-148">jQuery には、優れた HTML DOM の選択や効果ライブラリなど、さまざまな機能が用意されています。</span><span class="sxs-lookup"><span data-stu-id="60e4e-148">jQuery provides a number of features, including a nice HTML DOM selection and effects library.</span></span>

<span data-ttu-id="60e4e-149">JQuery を使用するには、まずスクリプト参照を追加します。</span><span class="sxs-lookup"><span data-stu-id="60e4e-149">To use jQuery we'll first add a script reference to it.</span></span> <span data-ttu-id="60e4e-150">ここでは、サイト内のさまざまな場所で jQuery を使用します。そのため、すべてのページで使用できるように、サイトのマスターページファイルにスクリプト参照を追加します。</span><span class="sxs-lookup"><span data-stu-id="60e4e-150">Because we are going to be using jQuery within a variety of places within our site, we'll add the script reference within our Site.master master page file so that all pages can use it.</span></span>

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample9.html)]

<span data-ttu-id="60e4e-151">*ヒント: JavaScript ファイル (jQuery を含む) に対するより高度な intellisense のサポートを有効にする、VS 2008 SP1 用の JavaScript intellisense 修正プログラムがインストールされていることを確認します。次のものからダウンロードできます: http://tinyurl.com/vs2008javascripthotfix*</span><span class="sxs-lookup"><span data-stu-id="60e4e-151">*Tip: make sure you have installed the JavaScript intellisense hotfix for VS 2008 SP1 that enables richer intellisense support for JavaScript files (including jQuery). You can download it from: http://tinyurl.com/vs2008javascripthotfix*</span></span>

<span data-ttu-id="60e4e-152">JQuery を使用して記述されたコードは、多くの場合、CSS セレクターを使用して1つ以上の HTML 要素を取得する、グローバルな "$ ()" JavaScript メソッドを使用します。</span><span class="sxs-lookup"><span data-stu-id="60e4e-152">Code written using JQuery often uses a global "$()" JavaScript method that retrieves one or more HTML elements using a CSS selector.</span></span> <span data-ttu-id="60e4e-153">たとえば、 *$ ("#rsvpmsg")* は、rsvpmsg の id を持つ HTML 要素を選択します。 *$ ("...")* は、CSS クラス名が "何か" のすべての要素を選択します。</span><span class="sxs-lookup"><span data-stu-id="60e4e-153">For example, *$("#rsvpmsg")* selects any HTML element with the id of rsvpmsg, while *$(".something")* would select all elements with the "something" CSS class name.</span></span> <span data-ttu-id="60e4e-154">また、次のようなセレクタークエリ *("input [@type= radio] [@checked]")* を使用して、"チェックされたすべてのラジオボタンを返す" など、より高度なクエリを作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="60e4e-154">You can also write more advanced queries like "return all of the checked radio buttons" using a selector query like: *$("input[@type=radio][@checked]")*.</span></span>

<span data-ttu-id="60e4e-155">要素を選択したら、それらのメソッドを呼び出して、 *$ ("#rsvpmsg"). hide ();* を非表示にするなどの操作を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="60e4e-155">Once you've selected elements, you can call methods on them to take action, like hiding them: *$("#rsvpmsg").hide();*</span></span>

<span data-ttu-id="60e4e-156">ここでは、"AnimateRSVPMessage" という名前の単純な JavaScript 関数を定義します。この関数は、"rsvpmsg" &lt;div&gt; を選択し、テキストコンテンツのサイズをアニメーション化します。</span><span class="sxs-lookup"><span data-stu-id="60e4e-156">For our RSVP scenario, we'll define a simple JavaScript function named "AnimateRSVPMessage" that selects the "rsvpmsg" &lt;div&gt; and animates the size of its text content.</span></span> <span data-ttu-id="60e4e-157">次のコードでは、テキストを小さくしてから、400ミリ秒の期間を増やしています。</span><span class="sxs-lookup"><span data-stu-id="60e4e-157">The below code starts the text small and then causes it to increase over a 400 milliseconds timeframe:</span></span>

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample10.html)]

<span data-ttu-id="60e4e-158">次に、AJAX 呼び出しが正常に完了した後に呼び出されるように、この JavaScript 関数を接続できます。これを行うには、Html.actionlink () ヘルパーメソッド (AjaxOptions "OnSuccess" イベントプロパティを使用) に名前を渡します。</span><span class="sxs-lookup"><span data-stu-id="60e4e-158">We can then wire-up this JavaScript function to be called after our AJAX call successfully completes by passing its name to our Ajax.ActionLink() helper method (via the AjaxOptions "OnSuccess" event property):</span></span>

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample11.aspx)]

<span data-ttu-id="60e4e-159">これで、"このイベントの RSVP" リンクがクリックされ、AJAX 呼び出しが正常に完了すると、返送されたコンテンツメッセージはアニメーション化され、大きくなります。</span><span class="sxs-lookup"><span data-stu-id="60e4e-159">And now when the "RSVP for this event" link is clicked and our AJAX call completes successfully, the content message sent back will animate and grow large:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image6.png)

<span data-ttu-id="60e4e-160">AjaxOptions オブジェクトは、"OnSuccess" イベントを提供するだけでなく、(他のさまざまなプロパティや便利なオプションと共に) 処理できる OnBegin、OnFailure、および Onbegin イベントを公開します。</span><span class="sxs-lookup"><span data-stu-id="60e4e-160">In addition to providing an "OnSuccess" event, the AjaxOptions object exposes OnBegin, OnFailure, and OnComplete events that you can handle (along with a variety of other properties and useful options).</span></span>

### <a name="cleanup---refactor-out-a-rsvp-partial-view"></a><span data-ttu-id="60e4e-161">クリーンアップ-RSVP 部分ビューをリファクターします。</span><span class="sxs-lookup"><span data-stu-id="60e4e-161">Cleanup - Refactor out a RSVP Partial View</span></span>

<span data-ttu-id="60e4e-162">詳細ビューのテンプレートは少し時間がかかります。そのため、超過しても理解が困難になります。</span><span class="sxs-lookup"><span data-stu-id="60e4e-162">Our details view template is starting to get a little long, which overtime will make it a little harder to understand.</span></span> <span data-ttu-id="60e4e-163">コードの読みやすさを向上させるために、詳細ページのすべての RSVP ビューコードをカプセル化する部分ビュー (RSVPStatus. .ascx) を作成してみましょう。</span><span class="sxs-lookup"><span data-stu-id="60e4e-163">To help improve the code readability, let's finish up by creating a partial view – RSVPStatus.ascx – that encapsulate all of the RSVP view code for our Details page.</span></span>

<span data-ttu-id="60e4e-164">これを行うには、\Views\Dinners フォルダーを右クリックし、[&gt;ビューの追加] メニューコマンドを選択します。</span><span class="sxs-lookup"><span data-stu-id="60e4e-164">We can do this by right-clicking on the \Views\Dinners folder and then choosing the Add-&gt;View menu command.</span></span> <span data-ttu-id="60e4e-165">ここでは、厳密に型指定されたビューモデルとしてディナーオブジェクトを取得します。</span><span class="sxs-lookup"><span data-stu-id="60e4e-165">We'll have it take a Dinner object as its strongly-typed ViewModel.</span></span> <span data-ttu-id="60e4e-166">その後、詳細 .aspx ビューの RSVP コンテンツをコピーして、それに貼り付けることができます。</span><span class="sxs-lookup"><span data-stu-id="60e4e-166">We can then copy/paste the RSVP content from our Details.aspx view into it.</span></span>

<span data-ttu-id="60e4e-167">これが完了したら、編集と削除のリンクビューコードをカプセル化するもう1つの部分ビュー (EditAndDeleteLinks) も作成します。</span><span class="sxs-lookup"><span data-stu-id="60e4e-167">Once we've done that, let's also create another partial view – EditAndDeleteLinks.ascx - that encapsulates our Edit and Delete link view code.</span></span> <span data-ttu-id="60e4e-168">また、このメソッドは、厳密に型指定されたビューモデルとしてディナーオブジェクトを取得し、詳細な .aspx ビューから編集および削除ロジックをコピー/貼り付けます。</span><span class="sxs-lookup"><span data-stu-id="60e4e-168">We'll also have it take a Dinner object as its strongly-typed ViewModel, and copy/paste the Edit and Delete logic from our Details.aspx view into it.</span></span>

<span data-ttu-id="60e4e-169">詳細ビューテンプレートでは、次の2つの Html. RenderPartial () メソッドの呼び出しを一番下に含めることができます。</span><span class="sxs-lookup"><span data-stu-id="60e4e-169">Our details view template can then just include two Html.RenderPartial() method calls at the bottom:</span></span>

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample12.aspx)]

<span data-ttu-id="60e4e-170">これにより、コードが読みやすくなり、維持されます。</span><span class="sxs-lookup"><span data-stu-id="60e4e-170">This makes the code cleaner to read and maintain.</span></span>

### <a name="next-step"></a><span data-ttu-id="60e4e-171">次の手順</span><span class="sxs-lookup"><span data-stu-id="60e4e-171">Next Step</span></span>

<span data-ttu-id="60e4e-172">AJAX をさらに使用して、対話的なマッピングのサポートをアプリケーションに追加する方法を見てみましょう。</span><span class="sxs-lookup"><span data-stu-id="60e4e-172">Let's now look at how we can use AJAX even further and add interactive mapping support to our application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="60e4e-173">[前へ](secure-applications-using-authentication-and-authorization.md)
> [次へ](use-ajax-to-implement-mapping-scenarios.md)</span><span class="sxs-lookup"><span data-stu-id="60e4e-173">[Previous](secure-applications-using-authentication-and-authorization.md)
[Next](use-ajax-to-implement-mapping-scenarios.md)</span></span>
