---
uid: web-api/overview/advanced/sending-html-form-data-part-1
title: 'ASP.NET Web API で HTML フォームデータを送信する: url エンコード Data-ASP.NET 4.x'
author: MikeWasson
description: この記事では、ASP.NET 4.x を使用して Web API コントローラーにフォーム url エンコードデータを投稿する方法を示します。
ms.author: riande
ms.date: 06/15/2012
ms.custom: seoapril2019
ms.assetid: 585351c4-809a-4bf5-bcbe-35d624f565fe
msc.legacyurl: /web-api/overview/advanced/sending-html-form-data-part-1
msc.type: authoredcontent
ms.openlocfilehash: 7243069dbd8051b1374ed6e0112c273b8fe26f61
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449242"
---
# <a name="sending-html-form-data-in-aspnet-web-api-form-urlencoded-data"></a><span data-ttu-id="4de1d-103">ASP.NET Web API での HTML フォームデータの送信: フォーム url エンコードデータ</span><span class="sxs-lookup"><span data-stu-id="4de1d-103">Sending HTML Form Data in ASP.NET Web API: Form-urlencoded Data</span></span>

<span data-ttu-id="4de1d-104">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="4de1d-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

## <a name="part-1-form-urlencoded-data"></a><span data-ttu-id="4de1d-105">パート 1: フォーム url エンコードデータ</span><span class="sxs-lookup"><span data-stu-id="4de1d-105">Part 1: Form-urlencoded Data</span></span>

<span data-ttu-id="4de1d-106">この記事では、Web API コントローラーにフォーム url エンコードデータを投稿する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="4de1d-106">This article shows how to post form-urlencoded data to a Web API controller.</span></span>

- [<span data-ttu-id="4de1d-107">HTML フォームの概要</span><span class="sxs-lookup"><span data-stu-id="4de1d-107">Overview of HTML Forms</span></span>](#overview_of_html_forms)
- [<span data-ttu-id="4de1d-108">複合型の送信</span><span class="sxs-lookup"><span data-stu-id="4de1d-108">Sending Complex Types</span></span>](#sending_complex_types)
- [<span data-ttu-id="4de1d-109">AJAX を使用したフォームデータの送信</span><span class="sxs-lookup"><span data-stu-id="4de1d-109">Sending Form Data via AJAX</span></span>](#sending_form_data_via_ajax)
- [<span data-ttu-id="4de1d-110">単純型の送信</span><span class="sxs-lookup"><span data-stu-id="4de1d-110">Sending Simple Types</span></span>](#sending_simple_types)

> [!NOTE]
> <span data-ttu-id="4de1d-111">[完成したプロジェクトをダウンロード](https://code.msdn.microsoft.com/ASPNET-Web-API-Sending-a6f9d007)します。</span><span class="sxs-lookup"><span data-stu-id="4de1d-111">[Download the completed project](https://code.msdn.microsoft.com/ASPNET-Web-API-Sending-a6f9d007).</span></span>

<a id="overview_of_html_forms"></a>
## <a name="overview-of-html-forms"></a><span data-ttu-id="4de1d-112">HTML フォームの概要</span><span class="sxs-lookup"><span data-stu-id="4de1d-112">Overview of HTML Forms</span></span>

<span data-ttu-id="4de1d-113">HTML 形式では、GET または POST を使用してサーバーにデータを送信します。</span><span class="sxs-lookup"><span data-stu-id="4de1d-113">HTML forms use either GET or POST to send data to the server.</span></span> <span data-ttu-id="4de1d-114">**Form**要素の**method**属性は、次のように HTTP メソッドを提供します。</span><span class="sxs-lookup"><span data-stu-id="4de1d-114">The **method** attribute of the **form** element gives the HTTP method:</span></span>

[!code-html[Main](sending-html-form-data-part-1/samples/sample1.html)]

<span data-ttu-id="4de1d-115">既定のメソッドは GET です。</span><span class="sxs-lookup"><span data-stu-id="4de1d-115">The default method is GET.</span></span> <span data-ttu-id="4de1d-116">フォームで GET が使用されている場合、フォームデータは URI でクエリ文字列としてエンコードされます。</span><span class="sxs-lookup"><span data-stu-id="4de1d-116">If the form uses GET, the form data is encoded in the URI as a query string.</span></span> <span data-ttu-id="4de1d-117">フォームが POST を使用する場合、フォームデータは要求本文に配置されます。</span><span class="sxs-lookup"><span data-stu-id="4de1d-117">If the form uses POST, the form data is placed in the request body.</span></span> <span data-ttu-id="4de1d-118">ポストされたデータの場合、 **enctype**属性は要求本文の形式を指定します。</span><span class="sxs-lookup"><span data-stu-id="4de1d-118">For POSTed data, the **enctype** attribute specifies the format of the request body:</span></span>

| <span data-ttu-id="4de1d-119">enctype</span><span class="sxs-lookup"><span data-stu-id="4de1d-119">enctype</span></span> | <span data-ttu-id="4de1d-120">Description</span><span class="sxs-lookup"><span data-stu-id="4de1d-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4de1d-121">application/x-www-form-urlencoded</span><span class="sxs-lookup"><span data-stu-id="4de1d-121">application/x-www-form-urlencoded</span></span> | <span data-ttu-id="4de1d-122">フォームデータは、URI クエリ文字列と同様に、名前と値のペアとしてエンコードされます。</span><span class="sxs-lookup"><span data-stu-id="4de1d-122">Form data is encoded as name/value pairs, similar to a URI query string.</span></span> <span data-ttu-id="4de1d-123">これは、POST の既定の形式です。</span><span class="sxs-lookup"><span data-stu-id="4de1d-123">This is the default format for POST.</span></span> |
| <span data-ttu-id="4de1d-124">マルチパート/フォーム-データ</span><span class="sxs-lookup"><span data-stu-id="4de1d-124">multipart/form-data</span></span> | <span data-ttu-id="4de1d-125">フォームデータは、マルチパート MIME メッセージとしてエンコードされます。</span><span class="sxs-lookup"><span data-stu-id="4de1d-125">Form data is encoded as a multipart MIME message.</span></span> <span data-ttu-id="4de1d-126">ファイルをサーバーにアップロードする場合は、この形式を使用します。</span><span class="sxs-lookup"><span data-stu-id="4de1d-126">Use this format if you are uploading a file to the server.</span></span> |

<span data-ttu-id="4de1d-127">この記事のパート1では、url エンコード形式について説明します。</span><span class="sxs-lookup"><span data-stu-id="4de1d-127">Part 1 of this article looks at x-www-form-urlencoded format.</span></span> <span data-ttu-id="4de1d-128">パート[2](sending-html-form-data-part-2.md)では、マルチパート MIME について説明します。</span><span class="sxs-lookup"><span data-stu-id="4de1d-128">[Part 2](sending-html-form-data-part-2.md) describes multipart MIME.</span></span>

<a id="sending_complex_types"></a>
## <a name="sending-complex-types"></a><span data-ttu-id="4de1d-129">複合型の送信</span><span class="sxs-lookup"><span data-stu-id="4de1d-129">Sending Complex Types</span></span>

<span data-ttu-id="4de1d-130">通常は、複数のフォームコントロールから取得した値で構成される複合型を送信します。</span><span class="sxs-lookup"><span data-stu-id="4de1d-130">Typically, you will send a complex type, composed of values taken from several form controls.</span></span> <span data-ttu-id="4de1d-131">状態の更新を表す次のモデルを考えてみましょう。</span><span class="sxs-lookup"><span data-stu-id="4de1d-131">Consider the following model that represents a status update:</span></span>

[!code-csharp[Main](sending-html-form-data-part-1/samples/sample2.cs)]

<span data-ttu-id="4de1d-132">POST を使用して `Update` オブジェクトを受け入れる Web API コントローラーを次に示します。</span><span class="sxs-lookup"><span data-stu-id="4de1d-132">Here is a Web API controller that accepts an `Update` object via POST.</span></span>

[!code-csharp[Main](sending-html-form-data-part-1/samples/sample3.cs)]

> [!NOTE]
> <span data-ttu-id="4de1d-133">このコントローラーは[アクションベースのルーティング](../web-api-routing-and-actions/routing-in-aspnet-web-api.md#routing_by_action_name)を使用しているため、ルートテンプレートは &quot;api/{controller}/{action}/{id}&quot;になります。</span><span class="sxs-lookup"><span data-stu-id="4de1d-133">This controller uses [action-based routing](../web-api-routing-and-actions/routing-in-aspnet-web-api.md#routing_by_action_name), so the route template is &quot;api/{controller}/{action}/{id}&quot;.</span></span> <span data-ttu-id="4de1d-134">クライアントは、&quot;/api&quot;にデータを送信します。</span><span class="sxs-lookup"><span data-stu-id="4de1d-134">The client will post the data to &quot;/api/updates/complex&quot;.</span></span>

<span data-ttu-id="4de1d-135">次に、ユーザーがステータスの更新を送信するための HTML フォームを作成してみましょう。</span><span class="sxs-lookup"><span data-stu-id="4de1d-135">Now let's write an HTML form for users to submit a status update.</span></span>

[!code-html[Main](sending-html-form-data-part-1/samples/sample4.html)]

<span data-ttu-id="4de1d-136">フォームの**action**属性がコントローラーアクションの URI であることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="4de1d-136">Notice that the **action** attribute on the form is the URI of our controller action.</span></span> <span data-ttu-id="4de1d-137">次に、に入力されたいくつかの値を含むフォームを示します。</span><span class="sxs-lookup"><span data-stu-id="4de1d-137">Here is the form with some values entered in:</span></span>

![](sending-html-form-data-part-1/_static/image1.png)

<span data-ttu-id="4de1d-138">ユーザーが [送信] をクリックすると、ブラウザーは次のような HTTP 要求を送信します。</span><span class="sxs-lookup"><span data-stu-id="4de1d-138">When the user clicks Submit, the browser sends an HTTP request similar to the following:</span></span>

[!code-console[Main](sending-html-form-data-part-1/samples/sample5.cmd)]

<span data-ttu-id="4de1d-139">要求本文に、名前と値のペアとして書式設定されたフォームデータが含まれていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="4de1d-139">Notice that the request body contains the form data, formatted as name/value pairs.</span></span> <span data-ttu-id="4de1d-140">Web API は、名前と値のペアを `Update` クラスのインスタンスに自動的に変換します。</span><span class="sxs-lookup"><span data-stu-id="4de1d-140">Web API automatically converts the name/value pairs into an instance of the `Update` class.</span></span>

<a id="sending_form_data_via_ajax"></a>
## <a name="sending-form-data-via-ajax"></a><span data-ttu-id="4de1d-141">AJAX を使用したフォームデータの送信</span><span class="sxs-lookup"><span data-stu-id="4de1d-141">Sending Form Data via AJAX</span></span>

<span data-ttu-id="4de1d-142">ユーザーがフォームを送信すると、ブラウザーは現在のページから移動し、応答メッセージの本文を表示します。</span><span class="sxs-lookup"><span data-stu-id="4de1d-142">When a user submits a form, the browser navigates away from the current page and renders the body of the response message.</span></span> <span data-ttu-id="4de1d-143">応答が HTML ページの場合は問題ありません。</span><span class="sxs-lookup"><span data-stu-id="4de1d-143">That's OK when the response is an HTML page.</span></span> <span data-ttu-id="4de1d-144">ただし、web API では、通常、応答本文は空であるか、JSON などの構造化データを含んでいます。</span><span class="sxs-lookup"><span data-stu-id="4de1d-144">With a web API, however, the response body is usually either empty or contains structured data, such as JSON.</span></span> <span data-ttu-id="4de1d-145">そのような場合は、AJAX 要求を使用してフォームデータを送信して、ページが応答を処理できるようにする方がよりわかりやすくなります。</span><span class="sxs-lookup"><span data-stu-id="4de1d-145">In that case, it makes more sense to send the form data using an AJAX request, so that the page can process the response.</span></span>

<span data-ttu-id="4de1d-146">次のコードは、jQuery を使用してフォームデータをポストする方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="4de1d-146">The following code shows how to post form data using jQuery.</span></span>

[!code-html[Main](sending-html-form-data-part-1/samples/sample6.html)]

<span data-ttu-id="4de1d-147">JQuery **submit**関数は、フォームアクションを新しい関数に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="4de1d-147">The jQuery **submit** function replaces the form action with a new function.</span></span> <span data-ttu-id="4de1d-148">これにより、[送信] ボタンの既定の動作がオーバーライドされます。</span><span class="sxs-lookup"><span data-stu-id="4de1d-148">This overrides the default behavior of the Submit button.</span></span> <span data-ttu-id="4de1d-149">Serialize 関数は、フォームデータを名前と値のペアにシリアル**化**します。</span><span class="sxs-lookup"><span data-stu-id="4de1d-149">The **serialize** function serializes the form data into name/value pairs.</span></span> <span data-ttu-id="4de1d-150">フォームデータをサーバーに送信するには、`$.post()`を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="4de1d-150">To send the form data to the server, call `$.post()`.</span></span>

<span data-ttu-id="4de1d-151">要求が完了すると、`.success()` または `.error()` ハンドラーによって、ユーザーに適切なメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="4de1d-151">When the request completes, the `.success()` or `.error()` handler displays an appropriate message to the user.</span></span>

![](sending-html-form-data-part-1/_static/image2.png)

<a id="sending_simple_types"></a>
## <a name="sending-simple-types"></a><span data-ttu-id="4de1d-152">単純型の送信</span><span class="sxs-lookup"><span data-stu-id="4de1d-152">Sending Simple Types</span></span>

<span data-ttu-id="4de1d-153">前のセクションでは、モデルクラスのインスタンスに Web API が逆シリアル化された複合型を送信しました。</span><span class="sxs-lookup"><span data-stu-id="4de1d-153">In the previous sections, we sent a complex type, which Web API deserialized to an instance of a model class.</span></span> <span data-ttu-id="4de1d-154">文字列などの単純型を送信することもできます。</span><span class="sxs-lookup"><span data-stu-id="4de1d-154">You can also send simple types, such as a string.</span></span>

> [!NOTE]
> <span data-ttu-id="4de1d-155">単純型を送信する前に、複合型に値をラップすることを検討してください。</span><span class="sxs-lookup"><span data-stu-id="4de1d-155">Before sending a simple type, consider wrapping the value in a complex type instead.</span></span> <span data-ttu-id="4de1d-156">これにより、サーバー側でのモデル検証の利点が得られ、必要に応じてモデルを拡張しやすくなります。</span><span class="sxs-lookup"><span data-stu-id="4de1d-156">This gives you the benefits of model validation on the server side, and makes it easier to extend your model if needed.</span></span>

<span data-ttu-id="4de1d-157">単純型を送信する基本的な手順は同じですが、微妙な違いが2つあります。</span><span class="sxs-lookup"><span data-stu-id="4de1d-157">The basic steps to send a simple type are the same, but there are two subtle differences.</span></span> <span data-ttu-id="4de1d-158">まず、コントローラーで、 **Frombody**属性を使用してパラメーター名を修飾する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4de1d-158">First, in the controller, you must decorate the parameter name with the **FromBody** attribute.</span></span>

[!code-csharp[Main](sending-html-form-data-part-1/samples/sample7.cs?highlight=3)]

<span data-ttu-id="4de1d-159">既定では、Web API は要求 URI から単純型を取得しようとします。</span><span class="sxs-lookup"><span data-stu-id="4de1d-159">By default, Web API tries to get simple types from the request URI.</span></span> <span data-ttu-id="4de1d-160">**Frombody**属性は、要求本文から値を読み取るように Web API に指示します。</span><span class="sxs-lookup"><span data-stu-id="4de1d-160">The **FromBody** attribute tells Web API to read the value from the request body.</span></span>

> [!NOTE]
> <span data-ttu-id="4de1d-161">Web API は応答本文を最大で1回読み取ります。そのため、要求本文から取得できるアクションのパラメーターは1つだけです。</span><span class="sxs-lookup"><span data-stu-id="4de1d-161">Web API reads the response body at most once, so only one parameter of an action can come from the request body.</span></span> <span data-ttu-id="4de1d-162">要求本文から複数の値を取得する必要がある場合は、複合型を定義します。</span><span class="sxs-lookup"><span data-stu-id="4de1d-162">If you need to get multiple values from the request body, define a complex type.</span></span>

<span data-ttu-id="4de1d-163">次に、クライアントは、次の形式で値を送信する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4de1d-163">Second, the client needs to send the value with the following format:</span></span>

[!code-xml[Main](sending-html-form-data-part-1/samples/sample8.xml)]

<span data-ttu-id="4de1d-164">具体的には、単純型の場合、名前と値のペアの名前部分は空である必要があります。</span><span class="sxs-lookup"><span data-stu-id="4de1d-164">Specifically, the name portion of the name/value pair must be empty for a simple type.</span></span> <span data-ttu-id="4de1d-165">すべてのブラウザーが HTML フォームに対してこれをサポートしているわけではありませんが、次のようにスクリプトでこの形式を作成します。</span><span class="sxs-lookup"><span data-stu-id="4de1d-165">Not all browsers support this for HTML forms, but you create this format in script as follows:</span></span>

[!code-javascript[Main](sending-html-form-data-part-1/samples/sample9.js)]

<span data-ttu-id="4de1d-166">フォームの例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="4de1d-166">Here is an example form:</span></span>

[!code-html[Main](sending-html-form-data-part-1/samples/sample10.html)]

<span data-ttu-id="4de1d-167">フォーム値を送信するスクリプトを次に示します。</span><span class="sxs-lookup"><span data-stu-id="4de1d-167">And here is the script to submit the form value.</span></span> <span data-ttu-id="4de1d-168">前のスクリプトとの唯一の違いは、 **post**関数に渡される引数です。</span><span class="sxs-lookup"><span data-stu-id="4de1d-168">The only difference from the previous script is the argument passed into the **post** function.</span></span>

[!code-javascript[Main](sending-html-form-data-part-1/samples/sample11.js?highlight=2)]

<span data-ttu-id="4de1d-169">同じ方法を使用して、単純型の配列を送信できます。</span><span class="sxs-lookup"><span data-stu-id="4de1d-169">You can use the same approach to send an array of simple types:</span></span>

[!code-javascript[Main](sending-html-form-data-part-1/samples/sample12.js)]

## <a name="additional-resources"></a><span data-ttu-id="4de1d-170">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="4de1d-170">Additional Resources</span></span>

[<span data-ttu-id="4de1d-171">パート 2: ファイルのアップロードとマルチパート MIME</span><span class="sxs-lookup"><span data-stu-id="4de1d-171">Part 2: File Upload and Multipart MIME</span></span>](sending-html-form-data-part-2.md)
