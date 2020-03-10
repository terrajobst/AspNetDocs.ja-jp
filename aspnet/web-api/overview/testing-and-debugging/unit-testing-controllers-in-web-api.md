---
uid: web-api/overview/testing-and-debugging/unit-testing-controllers-in-web-api
title: ASP.NET Web API 2 | の単体テストコントローラーMicrosoft Docs
author: MikeWasson
description: このトピックでは、Web API 2 の単体テストコントローラーの特定の手法について説明します。 このトピックを読む前に、「チュートリアル単位...」を読むことをお勧めします。
ms.author: riande
ms.date: 06/11/2014
ms.assetid: 43a6cce7-a3ef-42aa-ad06-90d36d49f098
msc.legacyurl: /web-api/overview/testing-and-debugging/unit-testing-controllers-in-web-api
msc.type: authoredcontent
ms.openlocfilehash: cdb1700537021e276669de1a9e0330a62659746c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78447004"
---
# <a name="unit-testing-controllers-in-aspnet-web-api-2"></a><span data-ttu-id="6d30a-104">ASP.NET Web API 2 の単体テスト コントローラー</span><span class="sxs-lookup"><span data-stu-id="6d30a-104">Unit Testing Controllers in ASP.NET Web API 2</span></span>

<span data-ttu-id="6d30a-105">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="6d30a-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="6d30a-106">このトピックでは、Web API 2 の単体テストコントローラーの特定の手法について説明します。</span><span class="sxs-lookup"><span data-stu-id="6d30a-106">This topic describes some specific techniques for unit testing controllers in Web API 2.</span></span> <span data-ttu-id="6d30a-107">このトピックを読む前に、単体テストプロジェクトをソリューションに追加する方法を示すチュートリアル[単体テスト ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md)を読むことをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="6d30a-107">Before reading this topic, you might want to read the tutorial [Unit Testing ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md), which shows how to add a unit-test project to your solution.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="6d30a-108">このチュートリアルで使用されているソフトウェアのバージョン</span><span class="sxs-lookup"><span data-stu-id="6d30a-108">Software versions used in the tutorial</span></span>
>
> - [<span data-ttu-id="6d30a-109">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="6d30a-109">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
> - <span data-ttu-id="6d30a-110">Web API 2</span><span class="sxs-lookup"><span data-stu-id="6d30a-110">Web API 2</span></span>
> - <span data-ttu-id="6d30a-111">[Moq](https://github.com/Moq) 4.5.30</span><span class="sxs-lookup"><span data-stu-id="6d30a-111">[Moq](https://github.com/Moq) 4.5.30</span></span>

> [!NOTE]
> <span data-ttu-id="6d30a-112">Moq を使用しましたが、モックフレームワークにも同じアイデアが適用されます。</span><span class="sxs-lookup"><span data-stu-id="6d30a-112">I used Moq, but the same idea applies to any mocking framework.</span></span> <span data-ttu-id="6d30a-113">Moq 4.5.30 (以降) は、Visual Studio 2017、Roslyn、.NET 4.5 以降のバージョンをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="6d30a-113">Moq 4.5.30 (and later) supports Visual Studio 2017, Roslyn and .NET 4.5 and later versions.</span></span>

<span data-ttu-id="6d30a-114">単体テストの一般的なパターンは、&quot;&quot;:</span><span class="sxs-lookup"><span data-stu-id="6d30a-114">A common pattern in unit tests is &quot;arrange-act-assert&quot;:</span></span>

- <span data-ttu-id="6d30a-115">配置: テストを実行するための前提条件を設定します。</span><span class="sxs-lookup"><span data-stu-id="6d30a-115">Arrange: Set up any prerequisites for the test to run.</span></span>
- <span data-ttu-id="6d30a-116">Act: テストを実行します。</span><span class="sxs-lookup"><span data-stu-id="6d30a-116">Act: Perform the test.</span></span>
- <span data-ttu-id="6d30a-117">Assert: テストが成功したことを確認します。</span><span class="sxs-lookup"><span data-stu-id="6d30a-117">Assert: Verify that the test succeeded.</span></span>

<span data-ttu-id="6d30a-118">配置手順では、モックオブジェクトまたはスタブオブジェクトを使用することがよくあります。</span><span class="sxs-lookup"><span data-stu-id="6d30a-118">In the arrange step, you will often use mock or stub objects.</span></span> <span data-ttu-id="6d30a-119">これにより、依存関係の数が最小限に抑えられるため、テストは1つのテストに重点を置いています。</span><span class="sxs-lookup"><span data-stu-id="6d30a-119">That minimizes the number of dependencies, so the test is focused on testing one thing.</span></span>

<span data-ttu-id="6d30a-120">ここでは、Web API コントローラーで単体テストを行う必要がある点をいくつか示します。</span><span class="sxs-lookup"><span data-stu-id="6d30a-120">Here are some things that you should unit test in your Web API controllers:</span></span>

- <span data-ttu-id="6d30a-121">アクションは、正しい種類の応答を返します。</span><span class="sxs-lookup"><span data-stu-id="6d30a-121">The action returns the correct type of response.</span></span>
- <span data-ttu-id="6d30a-122">無効なパラメーターは、正しいエラー応答を返します。</span><span class="sxs-lookup"><span data-stu-id="6d30a-122">Invalid parameters return the correct error response.</span></span>
- <span data-ttu-id="6d30a-123">アクションは、リポジトリまたはサービスレイヤーで適切なメソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="6d30a-123">The action calls the correct method on the repository or service layer.</span></span>
- <span data-ttu-id="6d30a-124">応答にドメインモデルが含まれている場合は、モデルの種類を確認します。</span><span class="sxs-lookup"><span data-stu-id="6d30a-124">If the response includes a domain model, verify the model type.</span></span>

<span data-ttu-id="6d30a-125">これらは一般的なテストですが、詳細はコントローラーの実装によって異なります。</span><span class="sxs-lookup"><span data-stu-id="6d30a-125">These are some of the general things to test, but the specifics depend on your controller implementation.</span></span> <span data-ttu-id="6d30a-126">特に、コントローラーアクションが**HttpResponseMessage**または**Ihttpactionresult**を返すかどうかに大きな違いがあります。</span><span class="sxs-lookup"><span data-stu-id="6d30a-126">In particular, it makes a big difference whether your controller actions return **HttpResponseMessage** or **IHttpActionResult**.</span></span> <span data-ttu-id="6d30a-127">これらの結果の種類の詳細については、「 [Web Api 2 でのアクションの結果](../getting-started-with-aspnet-web-api/action-results.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="6d30a-127">For more information about these result types, see [Action Results in Web Api 2](../getting-started-with-aspnet-web-api/action-results.md).</span></span>

## <a name="testing-actions-that-return-httpresponsemessage"></a><span data-ttu-id="6d30a-128">HttpResponseMessage を返すアクションのテスト</span><span class="sxs-lookup"><span data-stu-id="6d30a-128">Testing Actions that Return HttpResponseMessage</span></span>

<span data-ttu-id="6d30a-129">アクションが**HttpResponseMessage**を返すコントローラーの例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="6d30a-129">Here is an example of a controller whose actions return **HttpResponseMessage**.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample1.cs)]

<span data-ttu-id="6d30a-130">コントローラーは、依存関係の挿入を使用して `IProductRepository`を挿入することに注意してください。</span><span class="sxs-lookup"><span data-stu-id="6d30a-130">Notice the controller uses dependency injection to inject an `IProductRepository`.</span></span> <span data-ttu-id="6d30a-131">これにより、モックリポジトリを挿入できるため、コントローラーのテストが容易になります。</span><span class="sxs-lookup"><span data-stu-id="6d30a-131">That makes the controller more testable, because you can inject a mock repository.</span></span> <span data-ttu-id="6d30a-132">次の単体テストでは、`Get` メソッドが応答本文に `Product` を書き込むかどうかを確認します。</span><span class="sxs-lookup"><span data-stu-id="6d30a-132">The following unit test verifies that the `Get` method writes a `Product` to the response body.</span></span> <span data-ttu-id="6d30a-133">`repository` がモック `IProductRepository`であると仮定します。</span><span class="sxs-lookup"><span data-stu-id="6d30a-133">Assume that `repository` is a mock `IProductRepository`.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample2.cs)]

<span data-ttu-id="6d30a-134">コントローラーで**要求**と**構成**を設定することが重要です。</span><span class="sxs-lookup"><span data-stu-id="6d30a-134">It's important to set **Request** and **Configuration** on the controller.</span></span> <span data-ttu-id="6d30a-135">それ以外の場合、テストは**system.argumentnullexception**または**InvalidOperationException**で失敗します。</span><span class="sxs-lookup"><span data-stu-id="6d30a-135">Otherwise, the test will fail with an **ArgumentNullException** or **InvalidOperationException**.</span></span>

## <a name="testing-link-generation"></a><span data-ttu-id="6d30a-136">リンク生成のテスト</span><span class="sxs-lookup"><span data-stu-id="6d30a-136">Testing Link Generation</span></span>

<span data-ttu-id="6d30a-137">`Post` メソッドは、 **Urlhelper. リンク**を呼び出して、応答内にリンクを作成します。</span><span class="sxs-lookup"><span data-stu-id="6d30a-137">The `Post` method calls **UrlHelper.Link** to create links in the response.</span></span> <span data-ttu-id="6d30a-138">そのためには、単体テストでもう少しセットアップする必要があります。</span><span class="sxs-lookup"><span data-stu-id="6d30a-138">This requires a little more setup in the unit test:</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample3.cs)]

<span data-ttu-id="6d30a-139">**Urlhelper**クラスには要求 URL とルートデータが必要であるため、テストでこれらの値を設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6d30a-139">The **UrlHelper** class needs the request URL and route data, so the test has to set values for these.</span></span> <span data-ttu-id="6d30a-140">もう1つのオプションは、モックまたはスタブ**Urlhelper**です。</span><span class="sxs-lookup"><span data-stu-id="6d30a-140">Another option is mock or stub **UrlHelper**.</span></span> <span data-ttu-id="6d30a-141">この方法では、ApiController の既定値を、固定値を返すモックまたはスタブバージョンに置き換え[ます](https://msdn.microsoft.com/library/system.web.http.apicontroller.url.aspx)。</span><span class="sxs-lookup"><span data-stu-id="6d30a-141">With this approach, you replace the default value of [ApiController.Url](https://msdn.microsoft.com/library/system.web.http.apicontroller.url.aspx) with a mock or stub version that returns a fixed value.</span></span>

<span data-ttu-id="6d30a-142">[Moq](https://github.com/Moq)フレームワークを使用してテストを書き直してみましょう。</span><span class="sxs-lookup"><span data-stu-id="6d30a-142">Let's rewrite the test using the [Moq](https://github.com/Moq) framework.</span></span> <span data-ttu-id="6d30a-143">テストプロジェクトに `Moq` NuGet パッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="6d30a-143">Install the `Moq` NuGet package in the test project.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample4.cs)]

<span data-ttu-id="6d30a-144">このバージョンでは、モック**Urlhelper**が定数文字列を返すため、ルートデータを設定する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="6d30a-144">In this version, you don't need to set up any route data, because the mock **UrlHelper** returns a constant string.</span></span>

## <a name="testing-actions-that-return-ihttpactionresult"></a><span data-ttu-id="6d30a-145">IHttpActionResult を返すテストアクション</span><span class="sxs-lookup"><span data-stu-id="6d30a-145">Testing Actions that Return IHttpActionResult</span></span>

<span data-ttu-id="6d30a-146">Web API 2 では、コントローラーアクションは**Ihttpactionresult**を返すことができます。これは ASP.NET MVC の**actionresult**に似ています。</span><span class="sxs-lookup"><span data-stu-id="6d30a-146">In Web API 2, a controller action can return **IHttpActionResult**, which is analogous to **ActionResult** in ASP.NET MVC.</span></span> <span data-ttu-id="6d30a-147">**Ihttpactionresult**インターフェイスは、HTTP 応答を作成するためのコマンドパターンを定義します。</span><span class="sxs-lookup"><span data-stu-id="6d30a-147">The **IHttpActionResult** interface defines a command pattern for creating HTTP responses.</span></span> <span data-ttu-id="6d30a-148">コントローラーは、応答を直接作成するのではなく、 **Ihttpactionresult**を返します。</span><span class="sxs-lookup"><span data-stu-id="6d30a-148">Instead of creating the response directly, the controller returns an **IHttpActionResult**.</span></span> <span data-ttu-id="6d30a-149">後で、パイプラインは**Ihttpactionresult**を呼び出して応答を作成します。</span><span class="sxs-lookup"><span data-stu-id="6d30a-149">Later, the pipeline invokes the **IHttpActionResult** to create the response.</span></span> <span data-ttu-id="6d30a-150">この方法では、 **HttpResponseMessage**に必要なセットアップの大部分をスキップできるため、単体テストの記述が容易になります。</span><span class="sxs-lookup"><span data-stu-id="6d30a-150">This approach makes it easier to write unit tests, because you can skip a lot of the setup that is needed for **HttpResponseMessage**.</span></span>

<span data-ttu-id="6d30a-151">アクションが**Ihttpactionresult**を返すコントローラーの例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="6d30a-151">Here is an example controller whose actions return **IHttpActionResult**.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample5.cs)]

<span data-ttu-id="6d30a-152">この例では、 **Ihttpactionresult**を使用する一般的なパターンをいくつか示します。</span><span class="sxs-lookup"><span data-stu-id="6d30a-152">This example shows some common patterns using **IHttpActionResult**.</span></span> <span data-ttu-id="6d30a-153">単体テストの方法を見てみましょう。</span><span class="sxs-lookup"><span data-stu-id="6d30a-153">Let's see how to unit test them.</span></span>

### <a name="action-returns-200-ok-with-a-response-body"></a><span data-ttu-id="6d30a-154">アクションは、応答本文で 200 (OK) を返します</span><span class="sxs-lookup"><span data-stu-id="6d30a-154">Action returns 200 (OK) with a response body</span></span>

<span data-ttu-id="6d30a-155">`Get` メソッドは、製品が見つかった場合に `Ok(product)` を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="6d30a-155">The `Get` method calls `Ok(product)` if the product is found.</span></span> <span data-ttu-id="6d30a-156">単体テストで、戻り値の型が**OkNegotiatedContentResult**で、返された製品の ID が正しいことを確認します。</span><span class="sxs-lookup"><span data-stu-id="6d30a-156">In the unit test, make sure the return type is **OkNegotiatedContentResult** and the returned product has the right ID.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample6.cs)]

<span data-ttu-id="6d30a-157">単体テストでは、アクションの結果は実行されないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="6d30a-157">Notice that the unit test doesn't execute the action result.</span></span> <span data-ttu-id="6d30a-158">アクションの結果によって HTTP 応答が正しく作成されると想定できます。</span><span class="sxs-lookup"><span data-stu-id="6d30a-158">You can assume the action result creates the HTTP response correctly.</span></span> <span data-ttu-id="6d30a-159">(そのため、Web API フレームワークには独自の単体テストがあります)。</span><span class="sxs-lookup"><span data-stu-id="6d30a-159">(That's why the Web API framework has its own unit tests!)</span></span>

### <a name="action-returns-404-not-found"></a><span data-ttu-id="6d30a-160">アクションは 404 (見つかりません) を返します</span><span class="sxs-lookup"><span data-stu-id="6d30a-160">Action returns 404 (Not Found)</span></span>

<span data-ttu-id="6d30a-161">`Get` メソッドは、製品が見つからない場合に `NotFound()` を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="6d30a-161">The `Get` method calls `NotFound()` if the product is not found.</span></span> <span data-ttu-id="6d30a-162">この場合、単体テストでは、戻り値の型が**notfound の結果**であるかどうかのみをチェックします。</span><span class="sxs-lookup"><span data-stu-id="6d30a-162">For this case, the unit test just checks if the return type is **NotFoundResult**.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample7.cs)]

### <a name="action-returns-200-ok-with-no-response-body"></a><span data-ttu-id="6d30a-163">アクションは、応答本文なしで 200 (OK) を返します</span><span class="sxs-lookup"><span data-stu-id="6d30a-163">Action returns 200 (OK) with no response body</span></span>

<span data-ttu-id="6d30a-164">`Delete` メソッドは、`Ok()` を呼び出して、空の HTTP 200 応答を返します。</span><span class="sxs-lookup"><span data-stu-id="6d30a-164">The `Delete` method calls `Ok()` to return an empty HTTP 200 response.</span></span> <span data-ttu-id="6d30a-165">前の例と同様に、単体テストは戻り値の型をチェックします。この場合は**Okresult**です。</span><span class="sxs-lookup"><span data-stu-id="6d30a-165">Like the previous example, the unit test checks the return type, in this case **OkResult**.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample8.cs)]

### <a name="action-returns-201-created-with-a-location-header"></a><span data-ttu-id="6d30a-166">アクションは、Location ヘッダーを含む 201 (Created) を返します</span><span class="sxs-lookup"><span data-stu-id="6d30a-166">Action returns 201 (Created) with a Location header</span></span>

<span data-ttu-id="6d30a-167">`Post` メソッドは、`CreatedAtRoute` を呼び出して、Location ヘッダーに URI と共に HTTP 201 応答を返します。</span><span class="sxs-lookup"><span data-stu-id="6d30a-167">The `Post` method calls `CreatedAtRoute` to return an HTTP 201 response with a URI in the Location header.</span></span> <span data-ttu-id="6d30a-168">単体テストで、アクションによって正しいルーティング値が設定されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="6d30a-168">In the unit test, verify that the action sets the correct routing values.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample9.cs)]

### <a name="action-returns-another-2xx-with-a-response-body"></a><span data-ttu-id="6d30a-169">アクションは、応答本文を含む別の2xx を返します</span><span class="sxs-lookup"><span data-stu-id="6d30a-169">Action returns another 2xx with a response body</span></span>

<span data-ttu-id="6d30a-170">`Put` メソッドは、`Content` を呼び出して、応答本文と共に HTTP 202 (受理) 応答を返します。</span><span class="sxs-lookup"><span data-stu-id="6d30a-170">The `Put` method calls `Content` to return an HTTP 202 (Accepted) response with a response body.</span></span> <span data-ttu-id="6d30a-171">この例は、200 (OK) を返すのと似ていますが、単体テストでも状態コードを確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6d30a-171">This case is similar to returning 200 (OK), but the unit test should also check the status code.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample10.cs)]

## <a name="additional-resources"></a><span data-ttu-id="6d30a-172">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="6d30a-172">Additional Resources</span></span>

- [<span data-ttu-id="6d30a-173">単体テスト時のモック Entity Framework ASP.NET Web API 2</span><span class="sxs-lookup"><span data-stu-id="6d30a-173">Mocking Entity Framework when Unit Testing ASP.NET Web API 2</span></span>](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md)
- <span data-ttu-id="6d30a-174">[ASP.NET Web API サービスのテストの作成](https://blogs.msdn.com/b/youssefm/archive/2013/01/28/writing-tests-for-an-asp-net-webapi-service.aspx)(Youssef Moussaoui によるブログ投稿)</span><span class="sxs-lookup"><span data-stu-id="6d30a-174">[Writing tests for an ASP.NET Web API service](https://blogs.msdn.com/b/youssefm/archive/2013/01/28/writing-tests-for-an-asp-net-webapi-service.aspx) (blog post by Youssef Moussaoui).</span></span>
- [<span data-ttu-id="6d30a-175">ルートデバッガーを使用した ASP.NET Web API のデバッグ</span><span class="sxs-lookup"><span data-stu-id="6d30a-175">Debugging ASP.NET Web API with Route Debugger</span></span>](https://blogs.msdn.com/b/webdev/archive/2013/04/04/debugging-asp-net-web-api-with-route-debugger.aspx)
