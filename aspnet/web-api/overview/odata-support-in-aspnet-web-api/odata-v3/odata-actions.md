---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/odata-actions
title: ASP.NET Web API 2 | での OData アクションのサポートMicrosoft Docs
author: MikeWasson
description: OData では、アクションは、エンティティに対する CRUD 操作として簡単に定義できないサーバー側の動作を追加するための手段です。 アクションの用途には、次のようなものがあります。
ms.author: riande
ms.date: 02/25/2014
ms.assetid: 2d7b3aa2-aa47-4e6e-b0ce-3d65a1c6fe02
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/odata-actions
msc.type: authoredcontent
ms.openlocfilehash: ae8b23f0868f992cb2bbbf14ee3f7ac848501515
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600347"
---
# <a name="supporting-odata-actions-in-aspnet-web-api-2"></a><span data-ttu-id="0cda2-104">ASP.NET Web API 2 での OData アクションのサポート</span><span class="sxs-lookup"><span data-stu-id="0cda2-104">Supporting OData Actions in ASP.NET Web API 2</span></span>

<span data-ttu-id="0cda2-105">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="0cda2-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="0cda2-106">完成したプロジェクトのダウンロード</span><span class="sxs-lookup"><span data-stu-id="0cda2-106">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> <span data-ttu-id="0cda2-107">OData では、*アクション*は、エンティティに対する CRUD 操作として簡単に定義できないサーバー側の動作を追加するための手段です。</span><span class="sxs-lookup"><span data-stu-id="0cda2-107">In OData, *actions* are a way to add server-side behaviors that are not easily defined as CRUD operations on entities.</span></span> <span data-ttu-id="0cda2-108">アクションの用途には、次のようなものがあります。</span><span class="sxs-lookup"><span data-stu-id="0cda2-108">Some uses for actions include:</span></span>
> 
> - <span data-ttu-id="0cda2-109">複雑なトランザクションの実装。</span><span class="sxs-lookup"><span data-stu-id="0cda2-109">Implementing complex transactions.</span></span>
> - <span data-ttu-id="0cda2-110">一度に複数のエンティティを操作します。</span><span class="sxs-lookup"><span data-stu-id="0cda2-110">Manipulating several entities at once.</span></span>
> - <span data-ttu-id="0cda2-111">エンティティの特定のプロパティに対してのみ更新を許可します。</span><span class="sxs-lookup"><span data-stu-id="0cda2-111">Allowing updates only to certain properties of an entity.</span></span>
> - <span data-ttu-id="0cda2-112">エンティティで定義されていないサーバーに情報を送信しています。</span><span class="sxs-lookup"><span data-stu-id="0cda2-112">Sending information to the server that is not defined in an entity.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="0cda2-113">このチュートリアルで使用されているソフトウェアのバージョン</span><span class="sxs-lookup"><span data-stu-id="0cda2-113">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="0cda2-114">Web API 2</span><span class="sxs-lookup"><span data-stu-id="0cda2-114">Web API 2</span></span>
> - <span data-ttu-id="0cda2-115">OData バージョン3</span><span class="sxs-lookup"><span data-stu-id="0cda2-115">OData Version 3</span></span>
> - <span data-ttu-id="0cda2-116">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="0cda2-116">Entity Framework 6</span></span>

## <a name="example-rating-a-product"></a><span data-ttu-id="0cda2-117">例: 製品の評価</span><span class="sxs-lookup"><span data-stu-id="0cda2-117">Example: Rating a Product</span></span>

<span data-ttu-id="0cda2-118">この例では、ユーザーが製品を評価し、各製品の平均評価を公開できるようにします。</span><span class="sxs-lookup"><span data-stu-id="0cda2-118">In this example, we want to let users rate products, and then expose the average ratings for each product.</span></span> <span data-ttu-id="0cda2-119">データベースには、製品にキーを付けた評価の一覧が保存されます。</span><span class="sxs-lookup"><span data-stu-id="0cda2-119">On the database, we will store a list of ratings, keyed to products.</span></span>

<span data-ttu-id="0cda2-120">Entity Framework で評価を表すために使用できるモデルを次に示します。</span><span class="sxs-lookup"><span data-stu-id="0cda2-120">Here is the model we might use to represent the ratings in Entity Framework:</span></span>

[!code-csharp[Main](odata-actions/samples/sample1.cs)]

<span data-ttu-id="0cda2-121">しかし、クライアントが "評価" コレクションに `ProductRating` オブジェクトを投稿することは望ましくありません。</span><span class="sxs-lookup"><span data-stu-id="0cda2-121">But we don't want clients to POST a `ProductRating` object to a "Ratings" collection.</span></span> <span data-ttu-id="0cda2-122">直観的に、評価は Products コレクションに関連付けられており、クライアントは評価値を投稿するだけでよいはずです。</span><span class="sxs-lookup"><span data-stu-id="0cda2-122">Intuitively, the rating is associated with the Products collection, and the client should only need to post the rating value.</span></span>

<span data-ttu-id="0cda2-123">そのため、通常の CRUD 操作を使用する代わりに、クライアントが製品で呼び出すことができるアクションを定義します。</span><span class="sxs-lookup"><span data-stu-id="0cda2-123">Therefore, instead of using the normal CRUD operations, we define an action that a client can invoke on a Product.</span></span> <span data-ttu-id="0cda2-124">OData 用語では、アクションは製品エンティティに*バインド*されます。</span><span class="sxs-lookup"><span data-stu-id="0cda2-124">In OData terminology, the action is *bound* to Product entities.</span></span>

><span data-ttu-id="0cda2-125">アクションにはサーバーへの副作用があります。</span><span class="sxs-lookup"><span data-stu-id="0cda2-125">Actions have side-effects on the server.</span></span> <span data-ttu-id="0cda2-126">このため、HTTP POST 要求を使用して呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="0cda2-126">For this reason, they are invoked using HTTP POST requests.</span></span> <span data-ttu-id="0cda2-127">アクションには、サービスメタデータで記述されているパラメーターと戻り値の型を含めることができます。</span><span class="sxs-lookup"><span data-stu-id="0cda2-127">Actions can have parameters and return types, which are described in the service metadata.</span></span> <span data-ttu-id="0cda2-128">クライアントは要求本文にパラメーターを送信し、サーバーは応答本文で戻り値を送信します。</span><span class="sxs-lookup"><span data-stu-id="0cda2-128">The client sends the parameters in the request body, and the server sends the return value in the response body.</span></span> <span data-ttu-id="0cda2-129">"製品の評価" アクションを呼び出すために、クライアントは次のような URI に投稿を送信します。</span><span class="sxs-lookup"><span data-stu-id="0cda2-129">To invoke the "Rate Product" action, the client sends a POST to a URI like the following:</span></span>

[!code-console[Main](odata-actions/samples/sample2.cmd)]

<span data-ttu-id="0cda2-130">POST 要求のデータは、単純に製品の評価です。</span><span class="sxs-lookup"><span data-stu-id="0cda2-130">The data in the POST request is simply the product rating:</span></span>

[!code-console[Main](odata-actions/samples/sample3.cmd)]

## <a name="declare-the-action-in-the-entity-data-model"></a><span data-ttu-id="0cda2-131">Entity Data Model でアクションを宣言します。</span><span class="sxs-lookup"><span data-stu-id="0cda2-131">Declare the Action in the Entity Data Model</span></span>

<span data-ttu-id="0cda2-132">Web API 構成で、アクションを entity data model (EDM) に追加します。</span><span class="sxs-lookup"><span data-stu-id="0cda2-132">In your Web API configuration, add the action to the entity data model (EDM):</span></span>

[!code-csharp[Main](odata-actions/samples/sample4.cs)]

<span data-ttu-id="0cda2-133">このコードでは、Product エンティティに対して実行できるアクションとして "RateProduct" が定義されています。</span><span class="sxs-lookup"><span data-stu-id="0cda2-133">This code defines "RateProduct" as an action that can be performed on Product entities.</span></span> <span data-ttu-id="0cda2-134">また、アクションが "評価" という名前の**int**パラメーターを受け取り、 **int**値を返すことも宣言します。</span><span class="sxs-lookup"><span data-stu-id="0cda2-134">It also declares that the action takes an **int** parameter named "Rating", and returns an **int** value.</span></span>

## <a name="add-the-action-to-the-controller"></a><span data-ttu-id="0cda2-135">コントローラーにアクションを追加する</span><span class="sxs-lookup"><span data-stu-id="0cda2-135">Add the Action to the Controller</span></span>

<span data-ttu-id="0cda2-136">"RateProduct" アクションは、製品エンティティにバインドされています。</span><span class="sxs-lookup"><span data-stu-id="0cda2-136">The "RateProduct" action is bound to Product entities.</span></span> <span data-ttu-id="0cda2-137">アクションを実装するには、`RateProduct` という名前のメソッドを Products コントローラーに追加します。</span><span class="sxs-lookup"><span data-stu-id="0cda2-137">To implement the action, add a method named `RateProduct` to the Products controller:</span></span>

[!code-csharp[Main](odata-actions/samples/sample5.cs)]

<span data-ttu-id="0cda2-138">メソッド名が EDM のアクションの名前と一致することに注意してください。</span><span class="sxs-lookup"><span data-stu-id="0cda2-138">Notice that the method name matches the name of the action in the EDM.</span></span> <span data-ttu-id="0cda2-139">メソッドには、次の2つのパラメーターがあります。</span><span class="sxs-lookup"><span data-stu-id="0cda2-139">The method has two parameters:</span></span>

- <span data-ttu-id="0cda2-140">*キー*: 評価する製品のキー。</span><span class="sxs-lookup"><span data-stu-id="0cda2-140">*key*: The key for the product to rate.</span></span>
- <span data-ttu-id="0cda2-141">*parameters*: アクションパラメーター値のディクショナリ。</span><span class="sxs-lookup"><span data-stu-id="0cda2-141">*parameters*: A dictionary of action parameter values.</span></span>

<span data-ttu-id="0cda2-142">既定のルーティング規約を使用している場合、キーパラメーターの名前は "key" にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="0cda2-142">If you are using the default routing conventions, the key parameter must be named "key".</span></span> <span data-ttu-id="0cda2-143">次に示すように、 **[Fromodatauri]** 属性を含めることも重要です。</span><span class="sxs-lookup"><span data-stu-id="0cda2-143">It is also important to include the **[FromOdataUri]** attribute, as shown.</span></span> <span data-ttu-id="0cda2-144">この属性は、要求 URI からキーを解析するときに、OData 構文規則を使用するように Web API に指示します。</span><span class="sxs-lookup"><span data-stu-id="0cda2-144">This attribute tells Web API to use OData syntax rules when it parses the key from the request URI.</span></span>

<span data-ttu-id="0cda2-145">*パラメーター*ディクショナリを使用して、アクションパラメーターを取得します。</span><span class="sxs-lookup"><span data-stu-id="0cda2-145">Use the *parameters* dictionary to get the action parameters:</span></span>

[!code-csharp[Main](odata-actions/samples/sample6.cs)]

<span data-ttu-id="0cda2-146">クライアントがアクションパラメーターを正しい形式で送信する場合、 **Modelstate. IsValid**の値は true になります。</span><span class="sxs-lookup"><span data-stu-id="0cda2-146">If the client sends the action parameters in the correct format, the value of **ModelState.IsValid** is true.</span></span> <span data-ttu-id="0cda2-147">その場合は、パラメーターの値を取得するために、指定され**たパラメーターを**使用できます。</span><span class="sxs-lookup"><span data-stu-id="0cda2-147">In that case, you can use the **ODataActionParameters** dictionary to get the parameter values.</span></span> <span data-ttu-id="0cda2-148">この例では、`RateProduct` アクションは "評価" という名前の1つのパラメーターを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="0cda2-148">In this example, the `RateProduct` action takes a single parameter named "Rating".</span></span>

## <a name="action-metadata"></a><span data-ttu-id="0cda2-149">アクションメタデータ</span><span class="sxs-lookup"><span data-stu-id="0cda2-149">Action Metadata</span></span>

<span data-ttu-id="0cda2-150">サービスメタデータを表示するには、GET 要求を/odata/$metadata に送信します。</span><span class="sxs-lookup"><span data-stu-id="0cda2-150">To view the service metadata, send a GET request to /odata/$metadata.</span></span> <span data-ttu-id="0cda2-151">`RateProduct` アクションを宣言するメタデータの部分を次に示します。</span><span class="sxs-lookup"><span data-stu-id="0cda2-151">Here is the portion of the metadata that declares the `RateProduct` action:</span></span>

[!code-xml[Main](odata-actions/samples/sample7.xml)]

<span data-ttu-id="0cda2-152">**FunctionImport**要素はアクションを宣言します。</span><span class="sxs-lookup"><span data-stu-id="0cda2-152">The **FunctionImport** element declares the action.</span></span> <span data-ttu-id="0cda2-153">ほとんどのフィールドはわかりやすくなっていますが、2つの注意点があります。</span><span class="sxs-lookup"><span data-stu-id="0cda2-153">Most of the fields are self-explanatory, but two are worth noting:</span></span>

- <span data-ttu-id="0cda2-154">**Isbindable**可能は、少なくとも一部の時点で、ターゲットエンティティに対してアクションを呼び出すことができることを意味します。</span><span class="sxs-lookup"><span data-stu-id="0cda2-154">**IsBindable** means the action can be invoked on the target entity, at least some of the time.</span></span>
- <span data-ttu-id="0cda2-155">**Isalways バインド**可能とは、アクションをターゲットエンティティで常に呼び出すことができることを意味します。</span><span class="sxs-lookup"><span data-stu-id="0cda2-155">**IsAlwaysBindable** means the action can always be invoked on the target entity.</span></span>

<span data-ttu-id="0cda2-156">違いは、一部のアクションはクライアントで常に使用できるということですが、他のアクションはエンティティの状態によって異なる場合があります。</span><span class="sxs-lookup"><span data-stu-id="0cda2-156">The difference is that some actions are always available to clients, but other actions might depend on the state of the entity.</span></span> <span data-ttu-id="0cda2-157">たとえば、"Purchase" アクションを定義するとします。</span><span class="sxs-lookup"><span data-stu-id="0cda2-157">For example, suppose you define a "Purchase" action.</span></span> <span data-ttu-id="0cda2-158">購入できるのは在庫内の商品だけです。</span><span class="sxs-lookup"><span data-stu-id="0cda2-158">You can only purchase an item that is in stock.</span></span> <span data-ttu-id="0cda2-159">項目が在庫切れの場合、クライアントはそのアクションを呼び出すことができません。</span><span class="sxs-lookup"><span data-stu-id="0cda2-159">If the item is out of stock, a client cannot invoke that action.</span></span>

<span data-ttu-id="0cda2-160">EDM を定義すると、**アクション**メソッドによって、常にバインド可能なアクションが作成されます。</span><span class="sxs-lookup"><span data-stu-id="0cda2-160">When you define the EDM, the **Action** method creates an always-bindable action:</span></span>

[!code-csharp[Main](odata-actions/samples/sample8.cs?highlight=1)]

<span data-ttu-id="0cda2-161">ここでは、このトピックで後述する、非 always バインド操作 (*一時*アクションとも呼ばれます) について説明します。</span><span class="sxs-lookup"><span data-stu-id="0cda2-161">I'll talk about not-always-bindable actions (also called *transient* actions) later in this topic.</span></span>

## <a name="invoking-the-action"></a><span data-ttu-id="0cda2-162">アクションの呼び出し</span><span class="sxs-lookup"><span data-stu-id="0cda2-162">Invoking the Action</span></span>

<span data-ttu-id="0cda2-163">ここで、クライアントがこのアクションを呼び出す方法を見てみましょう。</span><span class="sxs-lookup"><span data-stu-id="0cda2-163">Now let's see how a client would invoke this action.</span></span> <span data-ttu-id="0cda2-164">たとえば、ID が4の製品に対して2という評価を行うとします。</span><span class="sxs-lookup"><span data-stu-id="0cda2-164">Suppose the client wants to give a rating of 2 to the product with ID = 4.</span></span> <span data-ttu-id="0cda2-165">要求本文の JSON 形式を使用した要求メッセージの例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="0cda2-165">Here is an example request message, using JSON format for the request body:</span></span>

[!code-console[Main](odata-actions/samples/sample9.cmd)]

<span data-ttu-id="0cda2-166">応答メッセージは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="0cda2-166">Here is the response message:</span></span>

[!code-console[Main](odata-actions/samples/sample10.cmd)]

## <a name="binding-an-action-to-an-entity-set"></a><span data-ttu-id="0cda2-167">エンティティセットへのアクションのバインド</span><span class="sxs-lookup"><span data-stu-id="0cda2-167">Binding an Action to an Entity Set</span></span>

<span data-ttu-id="0cda2-168">前の例では、アクションは単一のエンティティにバインドされています。クライアントは1つの製品を評価します。</span><span class="sxs-lookup"><span data-stu-id="0cda2-168">In the previous example, the action is bound to a single entity: The client rates a single product.</span></span> <span data-ttu-id="0cda2-169">また、アクションをエンティティのコレクションにバインドすることもできます。</span><span class="sxs-lookup"><span data-stu-id="0cda2-169">You can also bind an action to a collection of entities.</span></span> <span data-ttu-id="0cda2-170">次の変更を行うだけです。</span><span class="sxs-lookup"><span data-stu-id="0cda2-170">Just make the following changes:</span></span>

<span data-ttu-id="0cda2-171">EDM で、アクションをエンティティの**コレクション**プロパティに追加します。</span><span class="sxs-lookup"><span data-stu-id="0cda2-171">In the EDM, add the action to the entity's **Collection** property.</span></span>

[!code-csharp[Main](odata-actions/samples/sample11.cs?highlight=1)]

<span data-ttu-id="0cda2-172">コントローラーメソッドで、*キー*パラメーターを省略します。</span><span class="sxs-lookup"><span data-stu-id="0cda2-172">In the controller method, omit the *key* parameter.</span></span>

[!code-csharp[Main](odata-actions/samples/sample12.cs)]

<span data-ttu-id="0cda2-173">これで、クライアントは Products エンティティセットに対してアクションを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="0cda2-173">Now the client invokes the action on the Products entity set:</span></span>

[!code-console[Main](odata-actions/samples/sample13.cmd)]

## <a name="actions-with-collection-parameters"></a><span data-ttu-id="0cda2-174">コレクションパラメーターを使用したアクション</span><span class="sxs-lookup"><span data-stu-id="0cda2-174">Actions with Collection Parameters</span></span>

<span data-ttu-id="0cda2-175">アクションは、値のコレクションを受け取るパラメーターを持つことができます。</span><span class="sxs-lookup"><span data-stu-id="0cda2-175">Actions can have parameters that take a collection of values.</span></span> <span data-ttu-id="0cda2-176">EDM では、 **collectionparameter&lt;t&gt;** を使用してパラメーターを宣言します。</span><span class="sxs-lookup"><span data-stu-id="0cda2-176">In the EDM, use **CollectionParameter&lt;T&gt;** to declare the parameter.</span></span>

[!code-csharp[Main](odata-actions/samples/sample14.cs)]

<span data-ttu-id="0cda2-177">これは、 **int**値のコレクションを受け取る "評価" という名前のパラメーターを宣言します。</span><span class="sxs-lookup"><span data-stu-id="0cda2-177">This declares a parameter named "Ratings" that takes a collection of **int** values.</span></span> <span data-ttu-id="0cda2-178">コントローラーメソッドでは、現在では、パラメーターの値は、次のようにします。**このオブジェクトは、パラメーター**の値を指定します。値は**ICollection&lt;int&gt;** 値です。</span><span class="sxs-lookup"><span data-stu-id="0cda2-178">In the controller method, you still get the parameter value from the **ODataActionParameters** object, but now the value is an **ICollection&lt;int&gt;** value:</span></span>

[!code-csharp[Main](odata-actions/samples/sample15.cs)]

## <a name="transient-actions"></a><span data-ttu-id="0cda2-179">一時的なアクション</span><span class="sxs-lookup"><span data-stu-id="0cda2-179">Transient Actions</span></span>

<span data-ttu-id="0cda2-180">"RateProduct" の例では、ユーザーは常に製品を評価できるため、アクションは常に使用できます。</span><span class="sxs-lookup"><span data-stu-id="0cda2-180">In the "RateProduct" example, users can always rate a product, so the action is always available.</span></span> <span data-ttu-id="0cda2-181">ただし、一部のアクションはエンティティの状態に依存します。</span><span class="sxs-lookup"><span data-stu-id="0cda2-181">But some actions depend on the state of the entity.</span></span> <span data-ttu-id="0cda2-182">たとえば、ビデオレンタルサービスでは、"チェックアウト" アクションは常に使用できるとは限りません。</span><span class="sxs-lookup"><span data-stu-id="0cda2-182">For example, in a video rental service, the "CheckOut" action is not always available.</span></span> <span data-ttu-id="0cda2-183">(そのビデオのコピーが利用可能かどうかによって異なります)。この種類のアクションは、*一時的*なアクションと呼ばれます。</span><span class="sxs-lookup"><span data-stu-id="0cda2-183">(It depends whether a copy of that video is available.) This type of action is called a *transient* action.</span></span>

<span data-ttu-id="0cda2-184">サービスメタデータでは、一時的なアクションの値は**常**に false になります。</span><span class="sxs-lookup"><span data-stu-id="0cda2-184">In the service metadata, a transient action has **IsAlwaysBindable** equal to false.</span></span> <span data-ttu-id="0cda2-185">これは実際には既定値であるため、メタデータは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="0cda2-185">That's actually the default value, so the metadata will look like this:</span></span>

[!code-xml[Main](odata-actions/samples/sample16.xml)]

<span data-ttu-id="0cda2-186">これが重要な理由は次のとおりです。アクションが一時的なものである場合、サーバーは、アクションが使用可能であることをクライアントに通知する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0cda2-186">Here's why this matters: If an action is transient, the server needs to tell the client when the action is available.</span></span> <span data-ttu-id="0cda2-187">これを行うには、エンティティ内のアクションへのリンクを含めます。</span><span class="sxs-lookup"><span data-stu-id="0cda2-187">It does this by including a link to the action in the entity.</span></span> <span data-ttu-id="0cda2-188">次に、ムービーエンティティの例を示します。</span><span class="sxs-lookup"><span data-stu-id="0cda2-188">Here is an example for a Movie entity:</span></span>

[!code-console[Main](odata-actions/samples/sample17.cmd)]

<span data-ttu-id="0cda2-189">"#CheckOut" プロパティには、チェックアウトアクションへのリンクが含まれています。</span><span class="sxs-lookup"><span data-stu-id="0cda2-189">The "#CheckOut" property contains a link to the CheckOut action.</span></span> <span data-ttu-id="0cda2-190">アクションが使用できない場合、サーバーはリンクを省略します。</span><span class="sxs-lookup"><span data-stu-id="0cda2-190">If the action is not available, the server omits the link.</span></span>

<span data-ttu-id="0cda2-191">EDM で一時的なアクションを宣言するには、次のように、**遷移**メソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="0cda2-191">To declare a transient action in the EDM, call the **TransientAction** method:</span></span>

[!code-csharp[Main](odata-actions/samples/sample18.cs)]

<span data-ttu-id="0cda2-192">また、特定のエンティティのアクションリンクを返す関数を指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0cda2-192">Also, you must provide a function that returns an action link for a given entity.</span></span> <span data-ttu-id="0cda2-193">この関数は、 **HasActionLink**を呼び出して設定します。</span><span class="sxs-lookup"><span data-stu-id="0cda2-193">Set this function by calling **HasActionLink**.</span></span> <span data-ttu-id="0cda2-194">関数をラムダ式として記述できます。</span><span class="sxs-lookup"><span data-stu-id="0cda2-194">You can write the function as a lambda expression:</span></span>

[!code-csharp[Main](odata-actions/samples/sample19.cs)]

<span data-ttu-id="0cda2-195">アクションが使用可能な場合、ラムダ式はアクションへのリンクを返します。</span><span class="sxs-lookup"><span data-stu-id="0cda2-195">If the action is available, the lambda expression returns a link to the action.</span></span> <span data-ttu-id="0cda2-196">OData シリアライザーは、エンティティをシリアル化するときにこのリンクを含みます。</span><span class="sxs-lookup"><span data-stu-id="0cda2-196">The OData serializer includes this link when it serializes the entity.</span></span> <span data-ttu-id="0cda2-197">アクションが使用できない場合、関数は `null`を返します。</span><span class="sxs-lookup"><span data-stu-id="0cda2-197">When the action is not available, the function returns `null`.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0cda2-198">その他の資料</span><span class="sxs-lookup"><span data-stu-id="0cda2-198">Additional Resources</span></span>

[<span data-ttu-id="0cda2-199">OData アクションのサンプル</span><span class="sxs-lookup"><span data-stu-id="0cda2-199">OData Actions Sample</span></span>](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v3/ODataActionsSample/)
