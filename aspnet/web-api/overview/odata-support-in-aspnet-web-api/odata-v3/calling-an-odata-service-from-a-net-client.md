---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/calling-an-odata-service-from-a-net-client
title: .NET クライアントからの OData サービスの呼び出し (C#) |Microsoft Docs
author: MikeWasson
description: このチュートリアルでは、 C#クライアントアプリケーションから OData サービスを呼び出す方法について説明します。 チュートリアルで使用されているソフトウェアのバージョン Visual Studio 2013 (Visual S で動作します...
ms.author: riande
ms.date: 02/26/2014
ms.assetid: 6f448917-ad23-4dcc-9789-897fad74051b
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/calling-an-odata-service-from-a-net-client
msc.type: authoredcontent
ms.openlocfilehash: 6a289fcb843634eeeefef1e0767e04e0be8b6973
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600382"
---
# <a name="calling-an-odata-service-from-a-net-client-c"></a><span data-ttu-id="1c69f-104">.NET クライアントから OData サービスを呼び出す (C#)</span><span class="sxs-lookup"><span data-stu-id="1c69f-104">Calling an OData Service From a .NET Client (C#)</span></span>

<span data-ttu-id="1c69f-105">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="1c69f-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="1c69f-106">完成したプロジェクトのダウンロード</span><span class="sxs-lookup"><span data-stu-id="1c69f-106">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> <span data-ttu-id="1c69f-107">このチュートリアルでは、 C#クライアントアプリケーションから OData サービスを呼び出す方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="1c69f-107">This tutorial shows how to call an OData service from a C# client application.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="1c69f-108">このチュートリアルで使用されているソフトウェアのバージョン</span><span class="sxs-lookup"><span data-stu-id="1c69f-108">Software versions used in the tutorial</span></span>
>
>
> - <span data-ttu-id="1c69f-109">[Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013) (Visual Studio 2012 で動作)</span><span class="sxs-lookup"><span data-stu-id="1c69f-109">[Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013) (works with Visual Studio 2012)</span></span>
> - [<span data-ttu-id="1c69f-110">WCF Data Services クライアント ライブラリ</span><span class="sxs-lookup"><span data-stu-id="1c69f-110">WCF Data Services Client Library</span></span>](https://msdn.microsoft.com/library/cc668772.aspx)
> - <span data-ttu-id="1c69f-111">Web API 2。</span><span class="sxs-lookup"><span data-stu-id="1c69f-111">Web API 2.</span></span> <span data-ttu-id="1c69f-112">(例の OData サービスは Web API 2 を使用して構築されていますが、クライアントアプリケーションは Web API に依存していません)。</span><span class="sxs-lookup"><span data-stu-id="1c69f-112">(The example OData service is built using Web API 2, but the client application does not depend on Web API.)</span></span>

<span data-ttu-id="1c69f-113">このチュートリアルでは、OData サービスを呼び出すクライアントアプリケーションを作成する手順について説明します。</span><span class="sxs-lookup"><span data-stu-id="1c69f-113">In this tutorial, I'll walk through creating a client application that calls an OData service.</span></span> <span data-ttu-id="1c69f-114">OData サービスは、次のエンティティを公開します。</span><span class="sxs-lookup"><span data-stu-id="1c69f-114">The OData service exposes the following entities:</span></span>

- `Product`
- `Supplier`
- `ProductRating`

![](calling-an-odata-service-from-a-net-client/_static/image1.png)

<span data-ttu-id="1c69f-115">次の記事では、Web API で OData サービスを実装する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="1c69f-115">The following articles describe how to implement the OData service in Web API.</span></span> <span data-ttu-id="1c69f-116">(ただし、このチュートリアルを理解するために読む必要はありません)。</span><span class="sxs-lookup"><span data-stu-id="1c69f-116">(You don't need to read them to understand this tutorial, however.)</span></span>

- [<span data-ttu-id="1c69f-117">Web API 2 で OData エンドポイントを作成する</span><span class="sxs-lookup"><span data-stu-id="1c69f-117">Creating an OData Endpoint in Web API 2</span></span>](creating-an-odata-endpoint.md)
- [<span data-ttu-id="1c69f-118">Web API 2 での OData エンティティの関係</span><span class="sxs-lookup"><span data-stu-id="1c69f-118">OData Entity Relations in Web API 2</span></span>](working-with-entity-relations.md)
- [<span data-ttu-id="1c69f-119">Web API 2 の OData アクション</span><span class="sxs-lookup"><span data-stu-id="1c69f-119">OData Actions in Web API 2</span></span>](odata-actions.md)

## <a name="generate-the-service-proxy"></a><span data-ttu-id="1c69f-120">サービスプロキシの生成</span><span class="sxs-lookup"><span data-stu-id="1c69f-120">Generate the Service Proxy</span></span>

<span data-ttu-id="1c69f-121">最初の手順では、サービスプロキシを生成します。</span><span class="sxs-lookup"><span data-stu-id="1c69f-121">The first step is to generate a service proxy.</span></span> <span data-ttu-id="1c69f-122">サービスプロキシは、OData サービスにアクセスするためのメソッドを定義する .NET クラスです。</span><span class="sxs-lookup"><span data-stu-id="1c69f-122">The service proxy is a .NET class that defines methods for accessing the OData service.</span></span> <span data-ttu-id="1c69f-123">プロキシは、メソッドの呼び出しを HTTP 要求に変換します。</span><span class="sxs-lookup"><span data-stu-id="1c69f-123">The proxy translates method calls into HTTP requests.</span></span>

![](calling-an-odata-service-from-a-net-client/_static/image2.png)

<span data-ttu-id="1c69f-124">まず、Visual Studio で OData サービスプロジェクトを開きます。</span><span class="sxs-lookup"><span data-stu-id="1c69f-124">Start by opening the OData service project in Visual Studio.</span></span> <span data-ttu-id="1c69f-125">CTRL キーを押しながら F5 キーを押して IIS Express でサービスをローカルに実行します。</span><span class="sxs-lookup"><span data-stu-id="1c69f-125">Press CTRL+F5 to run the service locally in IIS Express.</span></span> <span data-ttu-id="1c69f-126">Visual Studio によって割り当てられるポート番号など、ローカルアドレスをメモしておきます。</span><span class="sxs-lookup"><span data-stu-id="1c69f-126">Note the local address, including the port number that Visual Studio assigns.</span></span> <span data-ttu-id="1c69f-127">プロキシを作成するときに、このアドレスが必要になります。</span><span class="sxs-lookup"><span data-stu-id="1c69f-127">You will need this address when you create the proxy.</span></span>

<span data-ttu-id="1c69f-128">次に、Visual Studio の別のインスタンスを開き、コンソールアプリケーションプロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="1c69f-128">Next, open another instance of Visual Studio and create a console application project.</span></span> <span data-ttu-id="1c69f-129">コンソールアプリケーションが OData クライアントアプリケーションになります。</span><span class="sxs-lookup"><span data-stu-id="1c69f-129">The console application will be our OData client application.</span></span> <span data-ttu-id="1c69f-130">(プロジェクトをサービスと同じソリューションに追加することもできます)。</span><span class="sxs-lookup"><span data-stu-id="1c69f-130">(You can also add the project to the same solution as the service.)</span></span>

> [!NOTE]
> <span data-ttu-id="1c69f-131">残りの手順では、コンソールプロジェクトを参照します。</span><span class="sxs-lookup"><span data-stu-id="1c69f-131">The remaining steps refer the console project.</span></span>

<span data-ttu-id="1c69f-132">ソリューションエクスプローラーで、 **[参照]** を右クリックし、 **[サービス参照の追加]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="1c69f-132">In Solution Explorer, right-click **References** and select **Add Service Reference**.</span></span>

![](calling-an-odata-service-from-a-net-client/_static/image3.png)

<span data-ttu-id="1c69f-133">**[サービス参照の追加]** ダイアログボックスで、OData サービスのアドレスを入力します。</span><span class="sxs-lookup"><span data-stu-id="1c69f-133">In the **Add Service Reference** dialog, type the address of the OData service:</span></span>

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample1.cmd)]

<span data-ttu-id="1c69f-134">ここで、 *port*はポート番号です。</span><span class="sxs-lookup"><span data-stu-id="1c69f-134">where *port* is the port number.</span></span>

[![](calling-an-odata-service-from-a-net-client/_static/image5.png)](calling-an-odata-service-from-a-net-client/_static/image4.png)

<span data-ttu-id="1c69f-135">**[名前空間]** に「productservice」と入力します。</span><span class="sxs-lookup"><span data-stu-id="1c69f-135">For **Namespace**, type "ProductService".</span></span> <span data-ttu-id="1c69f-136">このオプションでは、プロキシクラスの名前空間を定義します。</span><span class="sxs-lookup"><span data-stu-id="1c69f-136">This option defines the namespace of the proxy class.</span></span>

<span data-ttu-id="1c69f-137">**[検索]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="1c69f-137">Click **Go**.</span></span> <span data-ttu-id="1c69f-138">Visual Studio は、サービス内のエンティティを検出するために OData メタデータドキュメントを読み取ります。</span><span class="sxs-lookup"><span data-stu-id="1c69f-138">Visual Studio reads the OData metadata document to discover the entities in the service.</span></span>

[![](calling-an-odata-service-from-a-net-client/_static/image7.png)](calling-an-odata-service-from-a-net-client/_static/image6.png)

<span data-ttu-id="1c69f-139">[ **OK]** をクリックして、プロキシクラスをプロジェクトに追加します。</span><span class="sxs-lookup"><span data-stu-id="1c69f-139">Click **OK** to add the proxy class to your project.</span></span>

![](calling-an-odata-service-from-a-net-client/_static/image8.png)

## <a name="create-an-instance-of-the-service-proxy-class"></a><span data-ttu-id="1c69f-140">サービスプロキシクラスのインスタンスを作成する</span><span class="sxs-lookup"><span data-stu-id="1c69f-140">Create an Instance of the Service Proxy Class</span></span>

<span data-ttu-id="1c69f-141">`Main` メソッド内で、次のようにプロキシクラスの新しいインスタンスを作成します。</span><span class="sxs-lookup"><span data-stu-id="1c69f-141">Inside your `Main` method, create a new instance of the proxy class, as follows:</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample2.cs)]

<span data-ttu-id="1c69f-142">ここでも、サービスが実行されている実際のポート番号を使用します。</span><span class="sxs-lookup"><span data-stu-id="1c69f-142">Again, use the actual port number where your service is running.</span></span> <span data-ttu-id="1c69f-143">サービスをデプロイするときには、ライブサービスの URI を使用します。</span><span class="sxs-lookup"><span data-stu-id="1c69f-143">When you deploy your service, you will use the URI of the live service.</span></span> <span data-ttu-id="1c69f-144">プロキシを更新する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="1c69f-144">You don't need to update the proxy.</span></span>

<span data-ttu-id="1c69f-145">次のコードは、要求 Uri をコンソールウィンドウに出力するイベントハンドラーを追加します。</span><span class="sxs-lookup"><span data-stu-id="1c69f-145">The following code adds an event handler that prints the request URIs to the console window.</span></span> <span data-ttu-id="1c69f-146">この手順は必須ではありませんが、各クエリの Uri を確認することが重要です。</span><span class="sxs-lookup"><span data-stu-id="1c69f-146">This step isn't required, but it's interesting to see the URIs for each query.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample3.cs)]

## <a name="query-the-service"></a><span data-ttu-id="1c69f-147">サービスのクエリを実行する</span><span class="sxs-lookup"><span data-stu-id="1c69f-147">Query the Service</span></span>

<span data-ttu-id="1c69f-148">次のコードは、OData サービスから製品の一覧を取得します。</span><span class="sxs-lookup"><span data-stu-id="1c69f-148">The following code gets the list of products from the OData service.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample4.cs)]

<span data-ttu-id="1c69f-149">HTTP 要求を送信したり、応答を解析したりするコードを記述する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="1c69f-149">Notice that you don't need to write any code to send the HTTP request or parse the response.</span></span> <span data-ttu-id="1c69f-150">このプロキシクラスは、 **foreach**ループ内の `Container.Products` コレクションを列挙すると、この処理を自動的に行います。</span><span class="sxs-lookup"><span data-stu-id="1c69f-150">The proxy class does this automatically when you enumerate the `Container.Products` collection in the **foreach** loop.</span></span>

<span data-ttu-id="1c69f-151">アプリケーションを実行すると、出力は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="1c69f-151">When you run the application, the output should look like the following:</span></span>

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample5.cmd)]

<span data-ttu-id="1c69f-152">ID でエンティティを取得するには、`where` 句を使用します。</span><span class="sxs-lookup"><span data-stu-id="1c69f-152">To get an entity by ID, use a `where` clause.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample6.cs)]

<span data-ttu-id="1c69f-153">このトピックの残りの部分では、サービスの呼び出しに必要なコードだけで `Main` 関数全体を表示しません。</span><span class="sxs-lookup"><span data-stu-id="1c69f-153">For the rest of this topic, I won't show the entire `Main` function, just the code needed to call the service.</span></span>

## <a name="apply-query-options"></a><span data-ttu-id="1c69f-154">クエリオプションの適用</span><span class="sxs-lookup"><span data-stu-id="1c69f-154">Apply Query Options</span></span>

<span data-ttu-id="1c69f-155">OData は、フィルター処理、並べ替え、データのページなどに使用できる[クエリオプション](../supporting-odata-query-options.md)を定義します。</span><span class="sxs-lookup"><span data-stu-id="1c69f-155">OData defines [query options](../supporting-odata-query-options.md) that can be used to filter, sort, page data, and so forth.</span></span> <span data-ttu-id="1c69f-156">サービスプロキシでは、さまざまな LINQ 式を使用してこれらのオプションを適用できます。</span><span class="sxs-lookup"><span data-stu-id="1c69f-156">In the service proxy, you can apply these options by using various LINQ expressions.</span></span>

<span data-ttu-id="1c69f-157">このセクションでは、簡単な例を紹介します。</span><span class="sxs-lookup"><span data-stu-id="1c69f-157">In this section, I'll show brief examples.</span></span> <span data-ttu-id="1c69f-158">詳細については、MSDN の「 [LINQ に関する考慮事項」 (WCF Data Services)](https://msdn.microsoft.com/library/ee622463.aspx)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="1c69f-158">For more details, see the topic [LINQ Considerations (WCF Data Services)](https://msdn.microsoft.com/library/ee622463.aspx) on MSDN.</span></span>

### <a name="filtering-filter"></a><span data-ttu-id="1c69f-159">フィルター処理 ($filter)</span><span class="sxs-lookup"><span data-stu-id="1c69f-159">Filtering ($filter)</span></span>

<span data-ttu-id="1c69f-160">フィルター処理するには、`where` 句を使用します。</span><span class="sxs-lookup"><span data-stu-id="1c69f-160">To filter, use a `where` clause.</span></span> <span data-ttu-id="1c69f-161">次の例では、製品カテゴリを使用してフィルター処理を行います。</span><span class="sxs-lookup"><span data-stu-id="1c69f-161">The following example filters by product category.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample7.cs)]

<span data-ttu-id="1c69f-162">このコードは、次の OData クエリに対応しています。</span><span class="sxs-lookup"><span data-stu-id="1c69f-162">This code corresponds to the following OData query.</span></span>

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample8.cmd)]

<span data-ttu-id="1c69f-163">プロキシが `where` 句を OData `$filter` 式に変換することに注意してください。</span><span class="sxs-lookup"><span data-stu-id="1c69f-163">Notice that the proxy converts the `where` clause into an OData `$filter` expression.</span></span>

### <a name="sorting-orderby"></a><span data-ttu-id="1c69f-164">並べ替え ($orderby)</span><span class="sxs-lookup"><span data-stu-id="1c69f-164">Sorting ($orderby)</span></span>

<span data-ttu-id="1c69f-165">並べ替えるには、`orderby` 句を使用します。</span><span class="sxs-lookup"><span data-stu-id="1c69f-165">To sort, use an `orderby` clause.</span></span> <span data-ttu-id="1c69f-166">次の例では、価格を優先順位の高いものから順に並べ替えています。</span><span class="sxs-lookup"><span data-stu-id="1c69f-166">The following example sorts by price, from highest to lowest.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample9.cs)]

<span data-ttu-id="1c69f-167">対応する OData 要求を次に示します。</span><span class="sxs-lookup"><span data-stu-id="1c69f-167">Here is the corresponding OData request.</span></span>

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample10.cmd)]

### <a name="client-side-paging-skip-and-top"></a><span data-ttu-id="1c69f-168">クライアント側のページング ($skip と $top)</span><span class="sxs-lookup"><span data-stu-id="1c69f-168">Client-Side Paging ($skip and $top)</span></span>

<span data-ttu-id="1c69f-169">大きなエンティティセットの場合、クライアントは結果の数を制限することがあります。</span><span class="sxs-lookup"><span data-stu-id="1c69f-169">For large entity sets, the client might want to limit the number of results.</span></span> <span data-ttu-id="1c69f-170">たとえば、クライアントが一度に10個のエントリを表示する場合があります。</span><span class="sxs-lookup"><span data-stu-id="1c69f-170">For example, a client might show 10 entries at a time.</span></span> <span data-ttu-id="1c69f-171">これは *、クライアント側のページング*と呼ばれます。</span><span class="sxs-lookup"><span data-stu-id="1c69f-171">This is called *client-side paging*.</span></span> <span data-ttu-id="1c69f-172">(サーバー側の[ページング](../supporting-odata-query-options.md#server-paging)もあります。この場合、サーバーでは結果の数が制限されます)。クライアント側のページングを実行するには、LINQ の**Skip**メソッドと**Take**メソッドを使用します。</span><span class="sxs-lookup"><span data-stu-id="1c69f-172">(There is also [server-side paging](../supporting-odata-query-options.md#server-paging), where the server limits the number of results.) To perform client-side paging, use the LINQ **Skip** and **Take** methods.</span></span> <span data-ttu-id="1c69f-173">次の例では、最初の40件の結果をスキップし、次の10を取得します。</span><span class="sxs-lookup"><span data-stu-id="1c69f-173">The following example skips the first 40 results and takes the next 10.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample11.cs)]

<span data-ttu-id="1c69f-174">対応する OData 要求を次に示します。</span><span class="sxs-lookup"><span data-stu-id="1c69f-174">Here is the corresponding OData request:</span></span>

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample12.cmd)]

### <a name="select-select-and-expand-expand"></a><span data-ttu-id="1c69f-175">($Select) を選択し、($expand) を展開します。</span><span class="sxs-lookup"><span data-stu-id="1c69f-175">Select ($select) and Expand ($expand)</span></span>

<span data-ttu-id="1c69f-176">関連エンティティを含めるには、`DataServiceQuery<t>.Expand` メソッドを使用します。</span><span class="sxs-lookup"><span data-stu-id="1c69f-176">To include related entities, use the `DataServiceQuery<t>.Expand` method.</span></span> <span data-ttu-id="1c69f-177">たとえば、各 `Product`の `Supplier` を含めるには、次のようにします。</span><span class="sxs-lookup"><span data-stu-id="1c69f-177">For example, to include the `Supplier` for each `Product`:</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample13.cs)]

<span data-ttu-id="1c69f-178">対応する OData 要求を次に示します。</span><span class="sxs-lookup"><span data-stu-id="1c69f-178">Here is the corresponding OData request:</span></span>

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample14.cmd)]

<span data-ttu-id="1c69f-179">応答の形状を変更するには、LINQ **select**句を使用します。</span><span class="sxs-lookup"><span data-stu-id="1c69f-179">To change the shape of the response, use the LINQ **select** clause.</span></span> <span data-ttu-id="1c69f-180">次の例では、各製品の名前だけを取得し、その他のプロパティは取得しません。</span><span class="sxs-lookup"><span data-stu-id="1c69f-180">The following example gets just the name of each product, with no other properties.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample15.cs)]

<span data-ttu-id="1c69f-181">対応する OData 要求を次に示します。</span><span class="sxs-lookup"><span data-stu-id="1c69f-181">Here is the corresponding OData request:</span></span>

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample16.cmd)]

<span data-ttu-id="1c69f-182">Select 句には、関連エンティティを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="1c69f-182">A select clause can include related entities.</span></span> <span data-ttu-id="1c69f-183">その場合は、 **Expand**; を呼び出さないでください。この場合、プロキシには自動的に拡張が含まれます。</span><span class="sxs-lookup"><span data-stu-id="1c69f-183">In that case, do not call **Expand**; the proxy automatically includes the expansion in this case.</span></span> <span data-ttu-id="1c69f-184">次の例では、各製品の名前と仕入先を取得します。</span><span class="sxs-lookup"><span data-stu-id="1c69f-184">The following example gets the name and supplier of each product.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample17.cs)]

<span data-ttu-id="1c69f-185">対応する OData 要求を次に示します。</span><span class="sxs-lookup"><span data-stu-id="1c69f-185">Here is the corresponding OData request.</span></span> <span data-ttu-id="1c69f-186">**$Expand**オプションが含まれていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="1c69f-186">Notice that it includes the **$expand** option.</span></span>

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample18.cmd)]

<span data-ttu-id="1c69f-187">$Select と $expand の詳細については、「 [WEB API 2 での $select、$expand、および $value の使用](../using-select-expand-and-value.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="1c69f-187">For more information about $select and $expand, see [Using $select, $expand, and $value in Web API 2](../using-select-expand-and-value.md).</span></span>

## <a name="add-a-new-entity"></a><span data-ttu-id="1c69f-188">新しいエンティティを追加する</span><span class="sxs-lookup"><span data-stu-id="1c69f-188">Add a New Entity</span></span>

<span data-ttu-id="1c69f-189">エンティティセットに新しいエンティティを追加するには、`AddToEntitySet`を呼び出します。ここで、 *EntitySet*はエンティティセットの名前です。</span><span class="sxs-lookup"><span data-stu-id="1c69f-189">To add a new entity to an entity set, call `AddToEntitySet`, where *EntitySet* is the name of the entity set.</span></span> <span data-ttu-id="1c69f-190">たとえば、`AddToProducts` は `Products` エンティティセットに新しい `Product` を追加します。</span><span class="sxs-lookup"><span data-stu-id="1c69f-190">For example, `AddToProducts` adds a new `Product` to the `Products` entity set.</span></span> <span data-ttu-id="1c69f-191">プロキシを生成すると、WCF Data Services によって、これらの厳密に型指定された**Addto**メソッドが自動的に作成されます。</span><span class="sxs-lookup"><span data-stu-id="1c69f-191">When you generate the proxy, WCF Data Services automatically creates these strongly-typed **AddTo** methods.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample19.cs)]

<span data-ttu-id="1c69f-192">2つのエンティティ間にリンクを追加するには、 **addlink**メソッドと**setlink**メソッドを使用します。</span><span class="sxs-lookup"><span data-stu-id="1c69f-192">To add a link between two entities, use the **AddLink** and **SetLink** methods.</span></span> <span data-ttu-id="1c69f-193">次のコードでは、新しい業者と新しい製品を追加し、それらの間にリンクを作成します。</span><span class="sxs-lookup"><span data-stu-id="1c69f-193">The following code adds a new supplier and a new product, and then creates links between them.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample20.cs)]

<span data-ttu-id="1c69f-194">ナビゲーションプロパティがコレクションの場合は、 **Addlink**を使用します。</span><span class="sxs-lookup"><span data-stu-id="1c69f-194">Use **AddLink** when the navigation property is a collection.</span></span> <span data-ttu-id="1c69f-195">この例では、仕入先の `Products` コレクションに製品を追加します。</span><span class="sxs-lookup"><span data-stu-id="1c69f-195">In this example, we are adding a product to the `Products` collection on the supplier.</span></span>

<span data-ttu-id="1c69f-196">ナビゲーションプロパティが単一のエンティティの場合は、 **Setlink**を使用します。</span><span class="sxs-lookup"><span data-stu-id="1c69f-196">Use **SetLink** when the navigation property is a single entity.</span></span> <span data-ttu-id="1c69f-197">この例では、製品の `Supplier` プロパティを設定しています。</span><span class="sxs-lookup"><span data-stu-id="1c69f-197">In this example, we are setting the `Supplier` property on the product.</span></span>

## <a name="update--patch"></a><span data-ttu-id="1c69f-198">更新/パッチ</span><span class="sxs-lookup"><span data-stu-id="1c69f-198">Update / Patch</span></span>

<span data-ttu-id="1c69f-199">エンティティを更新するには、 **Updateobject**メソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="1c69f-199">To update an entity, call the **UpdateObject** method.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample21.cs)]

<span data-ttu-id="1c69f-200">この更新は、 **SaveChanges**を呼び出すと実行されます。</span><span class="sxs-lookup"><span data-stu-id="1c69f-200">The update is performed when you call **SaveChanges**.</span></span> <span data-ttu-id="1c69f-201">既定では、WCF は HTTP MERGE 要求を送信します。</span><span class="sxs-lookup"><span data-stu-id="1c69f-201">By default, WCF sends an HTTP MERGE request.</span></span> <span data-ttu-id="1c69f-202">PATCH **onupdate**オプションは、代わりに HTTP パッチを送信するよう WCF に指示します。</span><span class="sxs-lookup"><span data-stu-id="1c69f-202">The **PatchOnUpdate** option tells WCF to send an HTTP PATCH instead.</span></span>

> [!NOTE]
> <span data-ttu-id="1c69f-203">修正プログラムとマージの理由</span><span class="sxs-lookup"><span data-stu-id="1c69f-203">Why PATCH versus MERGE?</span></span> <span data-ttu-id="1c69f-204">元の HTTP 1.1 仕様 ([Rcf 2616](http://tools.ietf.org/html/rfc2616)) では、"部分的な更新" セマンティクスの http メソッドが定義されていませんでした。</span><span class="sxs-lookup"><span data-stu-id="1c69f-204">The original HTTP 1.1 specification ([RCF 2616](http://tools.ietf.org/html/rfc2616)) did not define any HTTP method with "partial update" semantics.</span></span> <span data-ttu-id="1c69f-205">部分更新をサポートするには、OData 仕様で MERGE メソッドが定義されています。</span><span class="sxs-lookup"><span data-stu-id="1c69f-205">To support partial updates, the OData specification defined the MERGE method.</span></span> <span data-ttu-id="1c69f-206">2010では、 [RFC 5789](http://tools.ietf.org/html/rfc5789)は部分更新の PATCH メソッドを定義していました。</span><span class="sxs-lookup"><span data-stu-id="1c69f-206">In 2010, [RFC 5789](http://tools.ietf.org/html/rfc5789) defined the PATCH method for partial updates.</span></span> <span data-ttu-id="1c69f-207">この[ブログの投稿](https://blogs.msdn.com/b/astoriateam/archive/2008/05/20/merge-vs-replace-semantics-for-update-operations.aspx)では、WCF Data Services のブログで履歴の一部を読むことができます。</span><span class="sxs-lookup"><span data-stu-id="1c69f-207">You can read some of the history in this [blog post](https://blogs.msdn.com/b/astoriateam/archive/2008/05/20/merge-vs-replace-semantics-for-update-operations.aspx) on the WCF Data Services Blog.</span></span> <span data-ttu-id="1c69f-208">現在、MERGE よりもパッチが推奨されています。</span><span class="sxs-lookup"><span data-stu-id="1c69f-208">Today, PATCH is preferred over MERGE.</span></span> <span data-ttu-id="1c69f-209">Web API スキャフォールディングによって作成された OData コントローラーは、両方のメソッドをサポートします。</span><span class="sxs-lookup"><span data-stu-id="1c69f-209">The OData controller created by the Web API scaffolding supports both methods.</span></span>

<span data-ttu-id="1c69f-210">エンティティ全体 (PUT セマンティクス) を置換する場合は、 **Replaceonupdate**オプションを指定します。</span><span class="sxs-lookup"><span data-stu-id="1c69f-210">If you want to replace the entire entity (PUT semantics), specify the **ReplaceOnUpdate** option.</span></span> <span data-ttu-id="1c69f-211">これにより、WCF は HTTP PUT 要求を送信します。</span><span class="sxs-lookup"><span data-stu-id="1c69f-211">This causes WCF to send an HTTP PUT request.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample22.cs)]

## <a name="delete-an-entity"></a><span data-ttu-id="1c69f-212">エンティティの削除</span><span class="sxs-lookup"><span data-stu-id="1c69f-212">Delete an Entity</span></span>

<span data-ttu-id="1c69f-213">エンティティを削除するには、 **DeleteObject**を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="1c69f-213">To delete an entity, call **DeleteObject**.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample23.cs)]

## <a name="invoke-an-odata-action"></a><span data-ttu-id="1c69f-214">OData アクションの呼び出し</span><span class="sxs-lookup"><span data-stu-id="1c69f-214">Invoke an OData Action</span></span>

<span data-ttu-id="1c69f-215">OData では、[アクション](odata-actions.md)は、エンティティに対する CRUD 操作として簡単に定義できないサーバー側の動作を追加するための手段です。</span><span class="sxs-lookup"><span data-stu-id="1c69f-215">In OData, [actions](odata-actions.md) are a way to add server-side behaviors that are not easily defined as CRUD operations on entities.</span></span>

<span data-ttu-id="1c69f-216">OData メタデータドキュメントではアクションについて説明していますが、プロキシクラスは、厳密に型指定されたメソッドを作成しません。</span><span class="sxs-lookup"><span data-stu-id="1c69f-216">Although the OData metadata document describes the actions, the proxy class does not create any strongly-typed methods for them.</span></span> <span data-ttu-id="1c69f-217">その場合でも、汎用**Execute**メソッドを使用して OData アクションを呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="1c69f-217">You can still invoke an OData action by using the generic **Execute** method.</span></span> <span data-ttu-id="1c69f-218">ただし、パラメーターのデータ型と戻り値を把握しておく必要があります。</span><span class="sxs-lookup"><span data-stu-id="1c69f-218">However, you will need to know the data types of the parameters and the return value.</span></span>

<span data-ttu-id="1c69f-219">たとえば、`RateProduct` アクションは、型 `Int32` の "評価" という名前のパラメーターを受け取り、`double`を返します。</span><span class="sxs-lookup"><span data-stu-id="1c69f-219">For example, the `RateProduct` action takes parameter named "Rating" of type `Int32` and returns a `double`.</span></span> <span data-ttu-id="1c69f-220">次のコードは、このアクションを呼び出す方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="1c69f-220">The following code shows how to invoke this action.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample24.cs)]

<span data-ttu-id="1c69f-221">詳細については、「[サービス操作とアクションの呼び出し](https://msdn.microsoft.com/library/hh230677.aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="1c69f-221">For more information, see[Calling Service Operations and Actions](https://msdn.microsoft.com/library/hh230677.aspx).</span></span>

<span data-ttu-id="1c69f-222">1つの方法として、**コンテナー**クラスを拡張して、アクションを呼び出す厳密に型指定されたメソッドを提供します。</span><span class="sxs-lookup"><span data-stu-id="1c69f-222">One option is to extend the **Container** class to provide a strongly typed method that invokes the action:</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample25.cs)]
