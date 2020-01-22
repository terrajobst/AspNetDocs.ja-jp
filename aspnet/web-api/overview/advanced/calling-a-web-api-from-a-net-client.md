---
uid: web-api/overview/advanced/calling-a-web-api-from-a-net-client
title: .NET クライアントから Web API を呼び出す (C#)-ASP.NET 4.x
author: MikeWasson
description: このチュートリアルでは、.NET 4.x アプリケーションから web API を呼び出す方法について説明します。
ms.author: riande
ms.date: 11/24/2017
ms.custom: seoapril2019
msc.legacyurl: /web-api/overview/advanced/calling-a-web-api-from-a-net-client
msc.type: authoredcontent
ms.openlocfilehash: 960960d26863cc3f725eee8a6c98844c5d3ce721
ms.sourcegitcommit: 88fc80e3f65aebdf61ec9414810ddbc31c543f04
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/22/2020
ms.locfileid: "76519181"
---
# <a name="call-a-web-api-from-a-net-client-c"></a><span data-ttu-id="d8fc5-103">.NET クライアントから Web API を呼び出す (C#)</span><span class="sxs-lookup"><span data-stu-id="d8fc5-103">Call a Web API From a .NET Client (C#)</span></span>

<span data-ttu-id="d8fc5-104">作成者[Mike Wasson](https://github.com/MikeWasson)および[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="d8fc5-104">by [Mike Wasson](https://github.com/MikeWasson) and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="d8fc5-105">[完成したプロジェクトをダウンロード](https://github.com/aspnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample)します。</span><span class="sxs-lookup"><span data-stu-id="d8fc5-105">[Download Completed Project](https://github.com/aspnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample).</span></span> <span data-ttu-id="d8fc5-106">[ダウンロードの方法はこちらをご覧ください。](/aspnet/core/tutorials/#how-to-download-a-sample)</span><span class="sxs-lookup"><span data-stu-id="d8fc5-106">[Download instructions](/aspnet/core/tutorials/#how-to-download-a-sample).</span></span> 

<span data-ttu-id="d8fc5-107">このチュートリアルでは [System.Net.Http.HttpClient](https://msdn.microsoft.com/library/system.net.http.httpclient(v=vs.110).aspx) を使用して .NET アプリケーションから web API を呼び出す方法を説明します。</span><span class="sxs-lookup"><span data-stu-id="d8fc5-107">This tutorial shows how to call a web API from a .NET application, using [System.Net.Http.HttpClient.](https://msdn.microsoft.com/library/system.net.http.httpclient(v=vs.110).aspx)</span></span>

<span data-ttu-id="d8fc5-108">このチュートリアルでは、次の web API を使用するクライアント アプリケーションについて書かれています。</span><span class="sxs-lookup"><span data-stu-id="d8fc5-108">In this tutorial, a client app is written that consumes the following web API:</span></span>

| <span data-ttu-id="d8fc5-109">動作</span><span class="sxs-lookup"><span data-stu-id="d8fc5-109">Action</span></span> | <span data-ttu-id="d8fc5-110">[HTTP メソッド]</span><span class="sxs-lookup"><span data-stu-id="d8fc5-110">HTTP method</span></span> | <span data-ttu-id="d8fc5-111">相対 URI</span><span class="sxs-lookup"><span data-stu-id="d8fc5-111">Relative URI</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d8fc5-112">ID によって製品を取得します。</span><span class="sxs-lookup"><span data-stu-id="d8fc5-112">Get a product by ID</span></span> | <span data-ttu-id="d8fc5-113">GET</span><span class="sxs-lookup"><span data-stu-id="d8fc5-113">GET</span></span> | <span data-ttu-id="d8fc5-114">/api/products/*id*</span><span class="sxs-lookup"><span data-stu-id="d8fc5-114">/api/products/*id*</span></span> |
| <span data-ttu-id="d8fc5-115">新しい製品を作成する</span><span class="sxs-lookup"><span data-stu-id="d8fc5-115">Create a new product</span></span> | <span data-ttu-id="d8fc5-116">POST</span><span class="sxs-lookup"><span data-stu-id="d8fc5-116">POST</span></span> | <span data-ttu-id="d8fc5-117">/api/products</span><span class="sxs-lookup"><span data-stu-id="d8fc5-117">/api/products</span></span> |
| <span data-ttu-id="d8fc5-118">製品を更新する</span><span class="sxs-lookup"><span data-stu-id="d8fc5-118">Update a product</span></span> | <span data-ttu-id="d8fc5-119">PUT</span><span class="sxs-lookup"><span data-stu-id="d8fc5-119">PUT</span></span> | <span data-ttu-id="d8fc5-120">/api/products/*id*</span><span class="sxs-lookup"><span data-stu-id="d8fc5-120">/api/products/*id*</span></span> |
| <span data-ttu-id="d8fc5-121">製品を削除する</span><span class="sxs-lookup"><span data-stu-id="d8fc5-121">Delete a product</span></span> | <span data-ttu-id="d8fc5-122">Del</span><span class="sxs-lookup"><span data-stu-id="d8fc5-122">DELETE</span></span> | <span data-ttu-id="d8fc5-123">/api/products/*id*</span><span class="sxs-lookup"><span data-stu-id="d8fc5-123">/api/products/*id*</span></span> |

<span data-ttu-id="d8fc5-124">ASP.NET Web API を使用して、この API を実装する方法については [CRUD 操作をサポートする Web API の作成](xref:web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="d8fc5-124">To learn how to implement this API with ASP.NET Web API, see [Creating a Web API that Supports CRUD Operations](xref:web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
).</span></span>

<span data-ttu-id="d8fc5-125">簡潔に示す目的のため、このチュートリアルではクライアント アプリケーションとして Windows コンソール アプリケーションを使用します。</span><span class="sxs-lookup"><span data-stu-id="d8fc5-125">For simplicity, the client application in this tutorial is a Windows console application.</span></span> <span data-ttu-id="d8fc5-126">**HttpClient** は Windows Phone や Windows ストア アプリでも同様にサポートされています。</span><span class="sxs-lookup"><span data-stu-id="d8fc5-126">**HttpClient** is also supported for Windows Phone and Windows Store apps.</span></span> <span data-ttu-id="d8fc5-127">より詳しい情報については [複数のプラットフォームを使用してポータブル ライブラリの Web API クライアント コードの記述。](https://blogs.msdn.com/b/webdev/archive/2013/07/19/writing-web-api-client-code-for-multiple-platforms-using-portable-libraries.aspx) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="d8fc5-127">For more information, see [Writing Web API Client Code for Multiple Platforms Using Portable Libraries](https://blogs.msdn.com/b/webdev/archive/2013/07/19/writing-web-api-client-code-for-multiple-platforms-using-portable-libraries.aspx)</span></span>

<a id="CreateConsoleApp"></a>
## <a name="create-the-console-application"></a><span data-ttu-id="d8fc5-128">コンソール アプリケーションを作成する</span><span class="sxs-lookup"><span data-stu-id="d8fc5-128">Create the Console Application</span></span>

<span data-ttu-id="d8fc5-129">Visual Studio で、**HttpClientSample** という名前の新しい Windows コンソール アプリを作成し、次のコードに貼り付けます。</span><span class="sxs-lookup"><span data-stu-id="d8fc5-129">In Visual Studio, create a new Windows console app named **HttpClientSample** and paste in the following code:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_all)]

<span data-ttu-id="d8fc5-130">上記のコードは、完全なクライアントアプリです。</span><span class="sxs-lookup"><span data-stu-id="d8fc5-130">The preceding code is the complete client app.</span></span>

<span data-ttu-id="d8fc5-131">`RunAsync` が実行され、完了するまでブロックされます。</span><span class="sxs-lookup"><span data-stu-id="d8fc5-131">`RunAsync` runs and blocks until it completes.</span></span> <span data-ttu-id="d8fc5-132">**HttpClient**メソッドはネットワーク I/O として振る舞うため、多くの場合、非同期です。</span><span class="sxs-lookup"><span data-stu-id="d8fc5-132">Most **HttpClient** methods are async, because they perform network I/O.</span></span> <span data-ttu-id="d8fc5-133">すべての非同期タスクは `RunAsync` 内で完了します。</span><span class="sxs-lookup"><span data-stu-id="d8fc5-133">All of the async tasks are done inside `RunAsync`.</span></span> <span data-ttu-id="d8fc5-134">通常、アプリは、メイン スレッドをブロックしませんが、このアプリはユーザーとの対話を許可しません。</span><span class="sxs-lookup"><span data-stu-id="d8fc5-134">Normally an app doesn't block the main thread, but this app doesn't allow any interaction.</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_run)]

<a id="InstallClientLib"></a>
## <a name="install-the-web-api-client-libraries"></a><span data-ttu-id="d8fc5-135">Web API クライアントライブラリをインストールする</span><span class="sxs-lookup"><span data-stu-id="d8fc5-135">Install the Web API Client Libraries</span></span>

<span data-ttu-id="d8fc5-136">NuGet パッケージマネージャーを使用して、Web API クライアントライブラリパッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="d8fc5-136">Use NuGet Package Manager to install the Web API Client Libraries package.</span></span>

<span data-ttu-id="d8fc5-137">**[ツール]** メニューで、 **[NuGet パッケージ マネージャー]** 、 **[パッケージ マネージャー コンソール]** の順に選択します。</span><span class="sxs-lookup"><span data-stu-id="d8fc5-137">From the **Tools** menu, select **NuGet Package Manager** > **Package Manager Console**.</span></span> <span data-ttu-id="d8fc5-138">パッケージマネージャーコンソール (PMC) で、次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="d8fc5-138">In the Package Manager Console (PMC), type the following command:</span></span>

`Install-Package Microsoft.AspNet.WebApi.Client`

<span data-ttu-id="d8fc5-139">上記のコマンドは、プロジェクトに次の NuGet パッケージを追加します。</span><span class="sxs-lookup"><span data-stu-id="d8fc5-139">The preceding command adds the following NuGet packages to the project:</span></span>

* <span data-ttu-id="d8fc5-140">Microsoft.AspNet.WebApi.Client</span><span class="sxs-lookup"><span data-stu-id="d8fc5-140">Microsoft.AspNet.WebApi.Client</span></span>
* <span data-ttu-id="d8fc5-141">Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="d8fc5-141">Newtonsoft.Json</span></span>

<span data-ttu-id="d8fc5-142">Netwonsoft (Json.NET とも呼ばれます) は、.NET 用の一般的な高パフォーマンスの JSON フレームワークです。</span><span class="sxs-lookup"><span data-stu-id="d8fc5-142">Netwonsoft.Json (also known as Json.NET) is a popular high-performance JSON framework for .NET.</span></span>

<a id="AddModelClass"></a>
## <a name="add-a-model-class"></a><span data-ttu-id="d8fc5-143">モデルクラスの追加</span><span class="sxs-lookup"><span data-stu-id="d8fc5-143">Add a Model Class</span></span>

<span data-ttu-id="d8fc5-144">次の `Product` クラスを調べます。</span><span class="sxs-lookup"><span data-stu-id="d8fc5-144">Examine the `Product` class:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_prod)]

<span data-ttu-id="d8fc5-145">このクラスでは、web API によって使用されるデータ モデルと一致します。</span><span class="sxs-lookup"><span data-stu-id="d8fc5-145">This class matches the data model used by the web API.</span></span> <span data-ttu-id="d8fc5-146">アプリは **HttpClient** を使用して HTTP レスポンスから `Product` インスタンスを読み取ることができます。</span><span class="sxs-lookup"><span data-stu-id="d8fc5-146">An app can use **HttpClient** to read a `Product` instance from an HTTP response.</span></span> <span data-ttu-id="d8fc5-147">アプリで逆シリアル化コードを記述する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="d8fc5-147">The app doesn't have to write any deserialization code.</span></span>

<a id="InitClient"></a>
## <a name="create-and-initialize-httpclient"></a><span data-ttu-id="d8fc5-148">HttpClient を作成して初期化する</span><span class="sxs-lookup"><span data-stu-id="d8fc5-148">Create and Initialize HttpClient</span></span>

<span data-ttu-id="d8fc5-149">静的**Httpclient**プロパティを確認します。</span><span class="sxs-lookup"><span data-stu-id="d8fc5-149">Examine the static **HttpClient** property:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_HttpClient)]

<span data-ttu-id="d8fc5-150">**Httpclient**は、1回だけインスタンス化し、アプリケーションの有効期間全体に再利用することを目的としています。</span><span class="sxs-lookup"><span data-stu-id="d8fc5-150">**HttpClient** is intended to be instantiated once and reused throughout the life of an application.</span></span> <span data-ttu-id="d8fc5-151">次の状況では、 **Socketexception**エラーが発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="d8fc5-151">The following conditions can result in **SocketException** errors:</span></span>

* <span data-ttu-id="d8fc5-152">要求ごとに新しい**Httpclient**インスタンスを作成しています。</span><span class="sxs-lookup"><span data-stu-id="d8fc5-152">Creating a new **HttpClient** instance per request.</span></span>
* <span data-ttu-id="d8fc5-153">サーバーの負荷が高くなっています。</span><span class="sxs-lookup"><span data-stu-id="d8fc5-153">Server under heavy load.</span></span>

<span data-ttu-id="d8fc5-154">要求ごとに新しい**Httpclient**インスタンスを作成すると、使用可能なソケットが枯渇する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="d8fc5-154">Creating a new **HttpClient** instance per request can exhaust the available sockets.</span></span>

<span data-ttu-id="d8fc5-155">次のコードでは、 **Httpclient**インスタンスを初期化します。</span><span class="sxs-lookup"><span data-stu-id="d8fc5-155">The following code initializes the **HttpClient** instance:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet5)]

<span data-ttu-id="d8fc5-156">上のコードでは以下の操作が行われます。</span><span class="sxs-lookup"><span data-stu-id="d8fc5-156">The preceding code:</span></span>

* <span data-ttu-id="d8fc5-157">HTTP 要求のベース URI を設定します。</span><span class="sxs-lookup"><span data-stu-id="d8fc5-157">Sets the base URI for HTTP requests.</span></span> <span data-ttu-id="d8fc5-158">ポート番号を、サーバーアプリで使用するポートに変更します。</span><span class="sxs-lookup"><span data-stu-id="d8fc5-158">Change the port number to the port used in the server app.</span></span> <span data-ttu-id="d8fc5-159">サーバーアプリのポートが使用されていない場合、アプリは機能しません。</span><span class="sxs-lookup"><span data-stu-id="d8fc5-159">The app won't work unless port for the server app is used.</span></span>
* <span data-ttu-id="d8fc5-160">Accept ヘッダーを "application/json" に設定します。</span><span class="sxs-lookup"><span data-stu-id="d8fc5-160">Sets the Accept header to "application/json".</span></span> <span data-ttu-id="d8fc5-161">このヘッダーを設定すると、JSON 形式でデータを送信するようにサーバーに指示されます。</span><span class="sxs-lookup"><span data-stu-id="d8fc5-161">Setting this header tells the server to send data in JSON format.</span></span>

<a id="GettingResource"></a>
## <a name="send-a-get-request-to-retrieve-a-resource"></a><span data-ttu-id="d8fc5-162">GET 要求を送信してリソースを取得する</span><span class="sxs-lookup"><span data-stu-id="d8fc5-162">Send a GET request to retrieve a resource</span></span>

<span data-ttu-id="d8fc5-163">次のコードは、製品の GET 要求を送信します。</span><span class="sxs-lookup"><span data-stu-id="d8fc5-163">The following code sends a GET request for a product:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_GetProductAsync)]

<span data-ttu-id="d8fc5-164">**GetAsync**メソッドは、HTTP GET 要求を送信します。</span><span class="sxs-lookup"><span data-stu-id="d8fc5-164">The **GetAsync** method sends the HTTP GET request.</span></span> <span data-ttu-id="d8fc5-165">メソッドが完了すると、HTTP 応答を含む**HttpResponseMessage**が返されます。</span><span class="sxs-lookup"><span data-stu-id="d8fc5-165">When the method completes, it returns an **HttpResponseMessage** that contains the HTTP response.</span></span> <span data-ttu-id="d8fc5-166">応答の状態コードが成功コードである場合、応答本文には製品の JSON 表現が含まれます。</span><span class="sxs-lookup"><span data-stu-id="d8fc5-166">If the status code in the response is a success code, the response body contains the JSON representation of a product.</span></span> <span data-ttu-id="d8fc5-167">**Readasasync**を呼び出して、JSON ペイロードを `Product` インスタンスに逆シリアル化します。</span><span class="sxs-lookup"><span data-stu-id="d8fc5-167">Call **ReadAsAsync** to deserialize the JSON payload to a `Product` instance.</span></span> <span data-ttu-id="d8fc5-168">応答本文は任意に大きくなる可能性があるため、 **Readasasync**メソッドは非同期です。</span><span class="sxs-lookup"><span data-stu-id="d8fc5-168">The **ReadAsAsync** method is asynchronous because the response body can be arbitrarily large.</span></span>

<span data-ttu-id="d8fc5-169">**Httpclient**は、HTTP 応答にエラーコードが含まれている場合に例外をスローしません。</span><span class="sxs-lookup"><span data-stu-id="d8fc5-169">**HttpClient** does not throw an exception when the HTTP response contains an error code.</span></span> <span data-ttu-id="d8fc5-170">状態がエラーコードの場合 **、"プロパティ**の報告" プロパティは**false**になります。</span><span class="sxs-lookup"><span data-stu-id="d8fc5-170">Instead, the **IsSuccessStatusCode** property is **false** if the status is an error code.</span></span> <span data-ttu-id="d8fc5-171">HTTP エラーコードを例外として扱う場合は、応答オブジェクトで[EnsureSuccessStatusCode](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.ensuresuccessstatuscode(v=vs.110).aspx)を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="d8fc5-171">If you prefer to treat HTTP error codes as exceptions, call [HttpResponseMessage.EnsureSuccessStatusCode](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.ensuresuccessstatuscode(v=vs.110).aspx) on the response object.</span></span> <span data-ttu-id="d8fc5-172">ステータスコードが 200&ndash;299 の範囲外になると `EnsureSuccessStatusCode` が例外をスローします。</span><span class="sxs-lookup"><span data-stu-id="d8fc5-172">`EnsureSuccessStatusCode` throws an exception if the status code falls outside the range 200&ndash;299.</span></span> <span data-ttu-id="d8fc5-173">**Httpclient**は、要求がタイムアウトした場合など、他の理由で例外をスローする可能性があることに注意してください。 &mdash;。</span><span class="sxs-lookup"><span data-stu-id="d8fc5-173">Note that **HttpClient** can throw exceptions for other reasons &mdash; for example, if the request times out.</span></span>

<a id="MediaTypeFormatters"></a>
### <a name="media-type-formatters-to-deserialize"></a><span data-ttu-id="d8fc5-174">逆シリアル化するメディアの種類のフォーマッタ</span><span class="sxs-lookup"><span data-stu-id="d8fc5-174">Media-Type Formatters to Deserialize</span></span>

<span data-ttu-id="d8fc5-175">パラメーターを使用せずに**Readasasync**を呼び出すと、既定の*メディアフォーマッタ*セットを使用して応答本文が読み取られます。</span><span class="sxs-lookup"><span data-stu-id="d8fc5-175">When **ReadAsAsync** is called with no parameters, it uses a default set of *media formatters* to read the response body.</span></span> <span data-ttu-id="d8fc5-176">既定のフォーマッタは、JSON、XML、およびフォーム url でエンコードされたデータをサポートします。</span><span class="sxs-lookup"><span data-stu-id="d8fc5-176">The default formatters support JSON, XML, and Form-url-encoded data.</span></span>

<span data-ttu-id="d8fc5-177">既定のフォーマッタを使用する代わりに、フォーマッタのリストを**Readasasync**メソッドに渡すことができます。</span><span class="sxs-lookup"><span data-stu-id="d8fc5-177">Instead of using the default formatters, you can provide a list of formatters to the **ReadAsAsync** method.</span></span>  <span data-ttu-id="d8fc5-178">カスタムのメディアタイプフォーマッタがある場合は、フォーマッタの一覧を使用すると便利です。</span><span class="sxs-lookup"><span data-stu-id="d8fc5-178">Using a list of formatters is useful if you have a custom media-type formatter:</span></span>

```csharp
var formatters = new List<MediaTypeFormatter>() {
    new MyCustomFormatter(),
    new JsonMediaTypeFormatter(),
    new XmlMediaTypeFormatter()
};
resp.Content.ReadAsAsync<IEnumerable<Product>>(formatters);
```

<span data-ttu-id="d8fc5-179">詳細については、「 [ASP.NET Web API 2 のメディアフォーマッタ](../formats-and-model-binding/media-formatters.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="d8fc5-179">For more information, see [Media Formatters in ASP.NET Web API 2](../formats-and-model-binding/media-formatters.md)</span></span>

## <a name="sending-a-post-request-to-create-a-resource"></a><span data-ttu-id="d8fc5-180">POST 要求を送信してリソースを作成する</span><span class="sxs-lookup"><span data-stu-id="d8fc5-180">Sending a POST Request to Create a Resource</span></span>

<span data-ttu-id="d8fc5-181">次のコードは、`Product` インスタンスを含む POST 要求を JSON 形式で送信します。</span><span class="sxs-lookup"><span data-stu-id="d8fc5-181">The following code sends a POST request that contains a `Product` instance in JSON format:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_CreateProductAsync)]

<span data-ttu-id="d8fc5-182">**Postasjsonasync**メソッド:</span><span class="sxs-lookup"><span data-stu-id="d8fc5-182">The **PostAsJsonAsync** method:</span></span>

* <span data-ttu-id="d8fc5-183">オブジェクトを JSON にシリアル化します。</span><span class="sxs-lookup"><span data-stu-id="d8fc5-183">Serializes an object to JSON.</span></span>
* <span data-ttu-id="d8fc5-184">POST 要求で JSON ペイロードを送信します。</span><span class="sxs-lookup"><span data-stu-id="d8fc5-184">Sends the JSON payload in a POST request.</span></span>

<span data-ttu-id="d8fc5-185">要求が成功した場合は、次のようになります。</span><span class="sxs-lookup"><span data-stu-id="d8fc5-185">If the request succeeds:</span></span>

* <span data-ttu-id="d8fc5-186">このメソッドは、201 (Created) 応答を返します。</span><span class="sxs-lookup"><span data-stu-id="d8fc5-186">It should return a 201 (Created) response.</span></span>
* <span data-ttu-id="d8fc5-187">応答には、作成されたリソースの URL を Location ヘッダーに含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="d8fc5-187">The response should include the URL of the created resources in the Location header.</span></span>

<a id="PuttingResource"></a>
## <a name="sending-a-put-request-to-update-a-resource"></a><span data-ttu-id="d8fc5-188">PUT 要求を送信してリソースを更新する</span><span class="sxs-lookup"><span data-stu-id="d8fc5-188">Sending a PUT Request to Update a Resource</span></span>

<span data-ttu-id="d8fc5-189">次のコードは、製品を更新する PUT 要求を送信します。</span><span class="sxs-lookup"><span data-stu-id="d8fc5-189">The following code sends a PUT request to update a product:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_UpdateProductAsync)]

<span data-ttu-id="d8fc5-190">**PutAsJsonAsync**メソッドは**Postasjsonasync**と同様に機能しますが、POST ではなく PUT 要求を送信する点が異なります。</span><span class="sxs-lookup"><span data-stu-id="d8fc5-190">The **PutAsJsonAsync** method works like **PostAsJsonAsync**, except that it sends a PUT request instead of POST.</span></span>

<a id="DeletingResource"></a>
## <a name="sending-a-delete-request-to-delete-a-resource"></a><span data-ttu-id="d8fc5-191">削除要求を送信してリソースを削除する</span><span class="sxs-lookup"><span data-stu-id="d8fc5-191">Sending a DELETE Request to Delete a Resource</span></span>

<span data-ttu-id="d8fc5-192">次のコードは、削除要求を送信して製品を削除します。</span><span class="sxs-lookup"><span data-stu-id="d8fc5-192">The following code sends a DELETE request to delete a product:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_DeleteProductAsync)]

<span data-ttu-id="d8fc5-193">GET と同様、DELETE 要求には要求本文がありません。</span><span class="sxs-lookup"><span data-stu-id="d8fc5-193">Like GET, a DELETE request does not have a request body.</span></span> <span data-ttu-id="d8fc5-194">DELETE を使用して JSON または XML 形式を指定する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="d8fc5-194">You don't need to specify JSON or XML format with DELETE.</span></span>

## <a name="test-the-sample"></a><span data-ttu-id="d8fc5-195">サンプルをテストする</span><span class="sxs-lookup"><span data-stu-id="d8fc5-195">Test the sample</span></span>

<span data-ttu-id="d8fc5-196">クライアントアプリをテストするには:</span><span class="sxs-lookup"><span data-stu-id="d8fc5-196">To test the client app:</span></span>

1. <span data-ttu-id="d8fc5-197">サーバーアプリを[ダウンロード](https://github.com/aspnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample/server)して実行します。</span><span class="sxs-lookup"><span data-stu-id="d8fc5-197">[Download](https://github.com/aspnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample/server) and run the server app.</span></span> <span data-ttu-id="d8fc5-198">[ダウンロードの方法はこちらをご覧ください。](/aspnet/core/#how-to-download-a-sample)</span><span class="sxs-lookup"><span data-stu-id="d8fc5-198">[Download instructions](/aspnet/core/#how-to-download-a-sample).</span></span> <span data-ttu-id="d8fc5-199">サーバーアプリが動作していることを確認します。</span><span class="sxs-lookup"><span data-stu-id="d8fc5-199">Verify the server app is working.</span></span> <span data-ttu-id="d8fc5-200">たとえば、`http://localhost:64195/api/products` は製品の一覧を返す必要があります。</span><span class="sxs-lookup"><span data-stu-id="d8fc5-200">For example, `http://localhost:64195/api/products` should return a list of products.</span></span>
2. <span data-ttu-id="d8fc5-201">HTTP 要求のベース URI を設定します。</span><span class="sxs-lookup"><span data-stu-id="d8fc5-201">Set the base URI for HTTP requests.</span></span> <span data-ttu-id="d8fc5-202">ポート番号を、サーバーアプリで使用するポートに変更します。</span><span class="sxs-lookup"><span data-stu-id="d8fc5-202">Change the port number to the port used in the server app.</span></span>
    [!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet5&highlight=2)]

3. <span data-ttu-id="d8fc5-203">クライアント アプリを実行します。</span><span class="sxs-lookup"><span data-stu-id="d8fc5-203">Run the client app.</span></span> <span data-ttu-id="d8fc5-204">次の出力が生成されます。</span><span class="sxs-lookup"><span data-stu-id="d8fc5-204">The following output is produced:</span></span>

   ```console
   Created at http://localhost:64195/api/products/4
   Name: Gizmo     Price: 100.0    Category: Widgets
   Updating price...
   Name: Gizmo     Price: 80.0     Category: Widgets
   Deleted (HTTP Status = 204)
   ```
