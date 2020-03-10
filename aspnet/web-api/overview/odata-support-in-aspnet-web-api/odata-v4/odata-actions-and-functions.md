---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/odata-actions-and-functions
title: ASP.NET Web API 2.2 | を使用した OData v4 のアクションと関数Microsoft Docs
author: MikeWasson
description: OData では、アクションと関数を利用して、エンティティに対する CRUD 操作として簡単に定義できないサーバー側の動作を追加することができます。 このチュートリアルでは、次の操作方法について説明します。
ms.author: riande
ms.date: 06/27/2014
ms.assetid: 0e6fb03c-b16d-4bb0-ab0b-552bd2b6ece1
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/odata-actions-and-functions
msc.type: authoredcontent
ms.openlocfilehash: f5af94e93e5b7f2351d40febbf1a468d635c9db1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448060"
---
# <a name="actions-and-functions-in-odata-v4-using-aspnet-web-api-22"></a><span data-ttu-id="b5f87-104">ASP.NET Web API 2.2 を使用した OData v4 のアクションと関数</span><span class="sxs-lookup"><span data-stu-id="b5f87-104">Actions and Functions in OData v4 Using ASP.NET Web API 2.2</span></span>

<span data-ttu-id="b5f87-105">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="b5f87-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="b5f87-106">OData では、アクションと関数を利用して、エンティティに対する CRUD 操作として簡単に定義できないサーバー側の動作を追加することができます。</span><span class="sxs-lookup"><span data-stu-id="b5f87-106">In OData, actions and functions are a way to add server-side behaviors that are not easily defined as CRUD operations on entities.</span></span> <span data-ttu-id="b5f87-107">このチュートリアルでは、Web API 2.2 を使用して、OData v4 エンドポイントにアクションと関数を追加する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="b5f87-107">This tutorial shows how to add actions and functions to an OData v4 endpoint, using Web API 2.2.</span></span> <span data-ttu-id="b5f87-108">このチュートリアルでは、チュートリアル[「ASP.NET Web API 2 を使用して OData V4 エンドポイントを作成](create-an-odata-v4-endpoint.md)する」を基にしています。</span><span class="sxs-lookup"><span data-stu-id="b5f87-108">The tutorial builds on the tutorial [Create an OData v4 Endpoint Using ASP.NET Web API 2](create-an-odata-v4-endpoint.md)</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="b5f87-109">このチュートリアルで使用されているソフトウェアのバージョン</span><span class="sxs-lookup"><span data-stu-id="b5f87-109">Software versions used in the tutorial</span></span>
>
> - <span data-ttu-id="b5f87-110">Web API 2.2</span><span class="sxs-lookup"><span data-stu-id="b5f87-110">Web API 2.2</span></span>
> - <span data-ttu-id="b5f87-111">OData v4</span><span class="sxs-lookup"><span data-stu-id="b5f87-111">OData v4</span></span>
> - <span data-ttu-id="b5f87-112">Visual Studio 2013 (こちらから Visual Studio 2017 をダウンロードして[ください](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017))</span><span class="sxs-lookup"><span data-stu-id="b5f87-112">Visual Studio 2013 (download Visual Studio 2017 [here](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017))</span></span>
> - <span data-ttu-id="b5f87-113">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="b5f87-113">.NET 4.5</span></span>
>
> ## <a name="tutorial-versions"></a><span data-ttu-id="b5f87-114">チュートリアルのバージョン</span><span class="sxs-lookup"><span data-stu-id="b5f87-114">Tutorial versions</span></span>
>
> <span data-ttu-id="b5f87-115">OData バージョン3については、「 [ASP.NET Web API 2 の Odata アクション](../odata-v3/odata-actions.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="b5f87-115">For OData Version 3, see [OData Actions in ASP.NET Web API 2](../odata-v3/odata-actions.md).</span></span>

<span data-ttu-id="b5f87-116">*アクション*と*関数*の違いは、アクションに副作用が生じる可能性があることと、関数によって処理されないことです。</span><span class="sxs-lookup"><span data-stu-id="b5f87-116">The difference between *actions* and *functions* is that actions can have side effects, and functions do not.</span></span> <span data-ttu-id="b5f87-117">アクションと関数はどちらもデータを返すことができます。</span><span class="sxs-lookup"><span data-stu-id="b5f87-117">Both actions and functions can return data.</span></span> <span data-ttu-id="b5f87-118">アクションの用途には、次のようなものがあります。</span><span class="sxs-lookup"><span data-stu-id="b5f87-118">Some uses for actions include:</span></span>

- <span data-ttu-id="b5f87-119">複雑なトランザクション。</span><span class="sxs-lookup"><span data-stu-id="b5f87-119">Complex transactions.</span></span>
- <span data-ttu-id="b5f87-120">一度に複数のエンティティを操作します。</span><span class="sxs-lookup"><span data-stu-id="b5f87-120">Manipulating several entities at once.</span></span>
- <span data-ttu-id="b5f87-121">エンティティの特定のプロパティに対してのみ更新を許可します。</span><span class="sxs-lookup"><span data-stu-id="b5f87-121">Allowing updates only to certain properties of an entity.</span></span>
- <span data-ttu-id="b5f87-122">エンティティではないデータを送信しています。</span><span class="sxs-lookup"><span data-stu-id="b5f87-122">Sending data that is not an entity.</span></span>

<span data-ttu-id="b5f87-123">関数は、エンティティまたはコレクションに直接対応していない情報を返す場合に便利です。</span><span class="sxs-lookup"><span data-stu-id="b5f87-123">Functions are useful for returning information that does not correspond directly to an entity or collection.</span></span>

<span data-ttu-id="b5f87-124">アクション (または関数) は、1つのエンティティまたはコレクションを対象にすることができます。</span><span class="sxs-lookup"><span data-stu-id="b5f87-124">An action (or function) can target a single entity or a collection.</span></span> <span data-ttu-id="b5f87-125">OData 用語では、これは*バインド*です。</span><span class="sxs-lookup"><span data-stu-id="b5f87-125">In OData terminology, this is the *binding*.</span></span> <span data-ttu-id="b5f87-126">また、&quot;バインドされていない&quot; アクション/関数を使用することもできます。これは、サービスで静的操作として呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="b5f87-126">You can also have &quot;unbound&quot; actions/functions, which are called as static operations on the service.</span></span>

## <a name="example-adding-an-action"></a><span data-ttu-id="b5f87-127">例: アクションの追加</span><span class="sxs-lookup"><span data-stu-id="b5f87-127">Example: Adding an Action</span></span>

<span data-ttu-id="b5f87-128">製品を評価するアクションを定義してみましょう。</span><span class="sxs-lookup"><span data-stu-id="b5f87-128">Let's define an action to rate a product.</span></span>

> [!NOTE]
> <span data-ttu-id="b5f87-129">このチュートリアルは、チュートリアル[「ASP.NET Web API 2 を使用して OData V4 エンドポイントを作成](create-an-odata-v4-endpoint.md)する」を基にしています。</span><span class="sxs-lookup"><span data-stu-id="b5f87-129">This tutorial builds on the tutorial [Create an OData v4 Endpoint Using ASP.NET Web API 2](create-an-odata-v4-endpoint.md)</span></span>

<span data-ttu-id="b5f87-130">まず、評価を表す `ProductRating` モデルを追加します。</span><span class="sxs-lookup"><span data-stu-id="b5f87-130">First, add a `ProductRating` model to represent the ratings.</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample1.cs)]

<span data-ttu-id="b5f87-131">また、 **Dbset**を `ProductsContext` クラスに追加して、EF によってデータベースに評価テーブルが作成されるようにします。</span><span class="sxs-lookup"><span data-stu-id="b5f87-131">Also add a **DbSet** to the `ProductsContext` class, so that EF will create a Ratings table in the database.</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample2.cs)]

### <a name="add-the-action-to-the-edm"></a><span data-ttu-id="b5f87-132">アクションを EDM に追加する</span><span class="sxs-lookup"><span data-stu-id="b5f87-132">Add the Action to the EDM</span></span>

<span data-ttu-id="b5f87-133">WebApiConfig.cs で、次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="b5f87-133">In WebApiConfig.cs, add the following code:</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample3.cs)]

<span data-ttu-id="b5f87-134">**Entitytypeconfiguration action**メソッドは、entity data MODEL (EDM) にアクションを追加します。</span><span class="sxs-lookup"><span data-stu-id="b5f87-134">The **EntityTypeConfiguration.Action** method adds an action to the entity data model (EDM).</span></span> <span data-ttu-id="b5f87-135">**Parameter**メソッドは、アクションに対して型指定されたパラメーターを指定します。</span><span class="sxs-lookup"><span data-stu-id="b5f87-135">The **Parameter** method specifies a typed parameter for the action.</span></span>

<span data-ttu-id="b5f87-136">このコードは、EDM の名前空間も設定します。</span><span class="sxs-lookup"><span data-stu-id="b5f87-136">This code also sets the namespace for the EDM.</span></span> <span data-ttu-id="b5f87-137">アクションの URI には完全修飾されたアクション名が含まれているため、名前空間が重要になります。</span><span class="sxs-lookup"><span data-stu-id="b5f87-137">The namespace matters because the URI for the action includes the fully-qualified action name:</span></span>

[!code-console[Main](odata-actions-and-functions/samples/sample4.cmd)]

> [!NOTE]
> <span data-ttu-id="b5f87-138">一般的な IIS 構成では、この URL のドットは IIS によってエラー404を返します。</span><span class="sxs-lookup"><span data-stu-id="b5f87-138">In a typical IIS configuration, the dot in this URL will cause IIS to return error 404.</span></span> <span data-ttu-id="b5f87-139">これを解決するには、web.config ファイルに次のセクションを追加します。</span><span class="sxs-lookup"><span data-stu-id="b5f87-139">You can resolve this by adding the following section to your Web.Config file:</span></span>

[!code-xml[Main](odata-actions-and-functions/samples/sample5.xml)]

### <a name="add-a-controller-method-for-the-action"></a><span data-ttu-id="b5f87-140">アクションのコントローラーメソッドを追加します。</span><span class="sxs-lookup"><span data-stu-id="b5f87-140">Add a Controller Method for the Action</span></span>

<span data-ttu-id="b5f87-141">&quot;率&quot; アクションを有効にするには、次のメソッドを `ProductsController`に追加します。</span><span class="sxs-lookup"><span data-stu-id="b5f87-141">To enable the &quot;Rate&quot; action, add the following method to `ProductsController`:</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample6.cs)]

<span data-ttu-id="b5f87-142">メソッド名がアクション名と一致することに注意してください。</span><span class="sxs-lookup"><span data-stu-id="b5f87-142">Notice that the method name matches the action name.</span></span> <span data-ttu-id="b5f87-143">**[Httppost]** 属性では、メソッドが HTTP POST メソッドであることを指定します。</span><span class="sxs-lookup"><span data-stu-id="b5f87-143">The **[HttpPost]** attribute specifies the method is an HTTP POST method.</span></span>

<span data-ttu-id="b5f87-144">アクションを呼び出すために、クライアントは次のような HTTP POST 要求を送信します。</span><span class="sxs-lookup"><span data-stu-id="b5f87-144">To invoke the action, the client sends an HTTP POST request like the following:</span></span>

[!code-console[Main](odata-actions-and-functions/samples/sample7.cmd)]

<span data-ttu-id="b5f87-145">&quot;率&quot; アクションは製品インスタンスにバインドされているため、アクションの URI は、エンティティ URI に追加された完全修飾アクション名になります。</span><span class="sxs-lookup"><span data-stu-id="b5f87-145">The &quot;Rate&quot; action is bound to Product instances, so the URI for the action is the fully-qualified action name appended to the entity URI.</span></span> <span data-ttu-id="b5f87-146">(EDM 名前空間を &quot;ProductService&quot;に設定しているので、完全修飾されたアクション名は ProductService. レート&quot;に &quot;ます)。</span><span class="sxs-lookup"><span data-stu-id="b5f87-146">(Recall that we set the EDM namespace to &quot;ProductService&quot;, so the fully-qualified action name is &quot;ProductService.Rate&quot;.)</span></span>

<span data-ttu-id="b5f87-147">要求の本文には、アクションパラメーターが JSON ペイロードとして含まれています。</span><span class="sxs-lookup"><span data-stu-id="b5f87-147">The body of the request contains the action parameters as a JSON payload.</span></span> <span data-ttu-id="b5f87-148">Web API は、JSON ペイロードを、パラメーター値のディクショナリである、自動的に、指定さ**れたパラメーターオブジェクトに**変換します。</span><span class="sxs-lookup"><span data-stu-id="b5f87-148">Web API automatically converts the JSON payload to an **ODataActionParameters** object, which is just a dictionary of parameter values.</span></span> <span data-ttu-id="b5f87-149">このディクショナリを使用して、コントローラーメソッドのパラメーターにアクセスします。</span><span class="sxs-lookup"><span data-stu-id="b5f87-149">Use this dictionary to access the parameters in your controller method.</span></span>

<span data-ttu-id="b5f87-150">クライアントがアクションパラメーターを誤った形式で送信した場合、 **Modelstate. IsValid**の値は false になります。</span><span class="sxs-lookup"><span data-stu-id="b5f87-150">If the client sends the action parameters in the wrong format, the value of **ModelState.IsValid** is false.</span></span> <span data-ttu-id="b5f87-151">コントローラーメソッドでこのフラグをチェックし、 **IsValid**が false の場合はエラーを返します。</span><span class="sxs-lookup"><span data-stu-id="b5f87-151">Check this flag in your controller method and return an error if **IsValid** is false.</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample8.cs)]

## <a name="example-adding-a-function"></a><span data-ttu-id="b5f87-152">例: 関数の追加</span><span class="sxs-lookup"><span data-stu-id="b5f87-152">Example: Adding a Function</span></span>

<span data-ttu-id="b5f87-153">次に、最も負荷の高い製品を返す OData 関数を追加してみましょう。</span><span class="sxs-lookup"><span data-stu-id="b5f87-153">Now let's add an OData function that returns the most expensive product.</span></span> <span data-ttu-id="b5f87-154">前と同様に、最初の手順として、関数を EDM に追加します。</span><span class="sxs-lookup"><span data-stu-id="b5f87-154">As before, the first step is adding the function to the EDM.</span></span> <span data-ttu-id="b5f87-155">WebApiConfig.cs で、次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="b5f87-155">In WebApiConfig.cs, add the following code.</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample9.cs)]

<span data-ttu-id="b5f87-156">この場合、関数は個別の製品インスタンスではなく Products コレクションにバインドされます。</span><span class="sxs-lookup"><span data-stu-id="b5f87-156">In this case, the function is bound to the Products collection, rather than individual Product instances.</span></span> <span data-ttu-id="b5f87-157">クライアントは GET 要求を送信することによって関数を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="b5f87-157">Clients invoke the function by sending a GET request:</span></span>

[!code-console[Main](odata-actions-and-functions/samples/sample10.cmd)]

<span data-ttu-id="b5f87-158">この関数のコントローラーメソッドを次に示します。</span><span class="sxs-lookup"><span data-stu-id="b5f87-158">Here is the controller method for this function:</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample11.cs)]

<span data-ttu-id="b5f87-159">メソッド名が関数名と一致することに注意してください。</span><span class="sxs-lookup"><span data-stu-id="b5f87-159">Notice that the method name matches the function name.</span></span> <span data-ttu-id="b5f87-160">**[HttpGet]** 属性は、メソッドが HTTP GET メソッドであることを指定します。</span><span class="sxs-lookup"><span data-stu-id="b5f87-160">The **[HttpGet]** attribute specifies the method is an HTTP GET method.</span></span>

<span data-ttu-id="b5f87-161">HTTP 応答を次に示します。</span><span class="sxs-lookup"><span data-stu-id="b5f87-161">Here is the HTTP response:</span></span>

[!code-console[Main](odata-actions-and-functions/samples/sample12.cmd)]

## <a name="example-adding-an-unbound-function"></a><span data-ttu-id="b5f87-162">例: バインド解除関数の追加</span><span class="sxs-lookup"><span data-stu-id="b5f87-162">Example: Adding an Unbound Function</span></span>

<span data-ttu-id="b5f87-163">前の例は、コレクションにバインドされた関数です。</span><span class="sxs-lookup"><span data-stu-id="b5f87-163">The previous example was a function bound to a collection.</span></span> <span data-ttu-id="b5f87-164">次の例では、*バインド*されていない関数を作成します。</span><span class="sxs-lookup"><span data-stu-id="b5f87-164">In this next example, we'll create an *unbound* function.</span></span> <span data-ttu-id="b5f87-165">バインドされていない関数は、サービスに対して静的操作として呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="b5f87-165">Unbound functions are called as static operations on the service.</span></span> <span data-ttu-id="b5f87-166">この例の関数は、指定された郵便番号の売上税を返します。</span><span class="sxs-lookup"><span data-stu-id="b5f87-166">The function in this example will return the sales tax for a given postal code.</span></span>

<span data-ttu-id="b5f87-167">Webapiconfig.cs ファイルで、関数を EDM に追加します。</span><span class="sxs-lookup"><span data-stu-id="b5f87-167">In the WebApiConfig file, add the function to the EDM:</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample13.cs)]

<span data-ttu-id="b5f87-168">エンティティ型またはコレクションではなく、**使用**に対して**関数**を直接呼び出すことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="b5f87-168">Notice that we are calling **Function** directly on the **ODataModelBuilder**, instead of the entity type or collection.</span></span> <span data-ttu-id="b5f87-169">これにより、関数がバインド解除されることがモデルビルダーに伝えられます。</span><span class="sxs-lookup"><span data-stu-id="b5f87-169">This tells the model builder that the function is unbound.</span></span>

<span data-ttu-id="b5f87-170">関数を実装するコントローラーメソッドを次に示します。</span><span class="sxs-lookup"><span data-stu-id="b5f87-170">Here is the controller method that implements the function:</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample14.cs)]

<span data-ttu-id="b5f87-171">このメソッドをどの Web API コントローラーに配置するかは関係ありません。</span><span class="sxs-lookup"><span data-stu-id="b5f87-171">It does not matter which Web API controller you place this method in.</span></span> <span data-ttu-id="b5f87-172">`ProductsController`に配置することも、別のコントローラーを定義することもできます。</span><span class="sxs-lookup"><span data-stu-id="b5f87-172">You could put it in `ProductsController`, or define a separate controller.</span></span> <span data-ttu-id="b5f87-173">**[ODataRoute]** 属性は、関数の URI テンプレートを定義します。</span><span class="sxs-lookup"><span data-stu-id="b5f87-173">The **[ODataRoute]** attribute defines the URI template for the function.</span></span>

<span data-ttu-id="b5f87-174">クライアント要求の例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="b5f87-174">Here is an example client request:</span></span>

[!code-console[Main](odata-actions-and-functions/samples/sample15.cmd)]

<span data-ttu-id="b5f87-175">HTTP 応答:</span><span class="sxs-lookup"><span data-stu-id="b5f87-175">The HTTP response:</span></span>

[!code-console[Main](odata-actions-and-functions/samples/sample16.cmd)]
