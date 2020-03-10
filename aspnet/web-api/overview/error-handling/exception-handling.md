---
uid: web-api/overview/error-handling/exception-handling
title: ASP.NET Web API での例外処理-ASP.NET 4.x
author: MikeWasson
description: ''
ms.author: riande
ms.date: 03/12/2012
ms.custom: seoapril2019
ms.assetid: cbebeb37-2594-41f2-b71a-f4f26520d512
msc.legacyurl: /web-api/overview/error-handling/exception-handling
msc.type: authoredcontent
ms.openlocfilehash: dbdbab6aefec840e2fec9e9cd33f3d124093750e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78504700"
---
# <a name="exception-handling-in-aspnet-web-api"></a><span data-ttu-id="76867-102">ASP.NET Web API での例外処理</span><span class="sxs-lookup"><span data-stu-id="76867-102">Exception Handling in ASP.NET Web API</span></span>

<span data-ttu-id="76867-103">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="76867-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="76867-104">この記事では、ASP.NET Web API でのエラーと例外の処理について説明します。</span><span class="sxs-lookup"><span data-stu-id="76867-104">This article describes error and exception handling in ASP.NET Web API.</span></span>

- [<span data-ttu-id="76867-105">HttpResponseException</span><span class="sxs-lookup"><span data-stu-id="76867-105">HttpResponseException</span></span>](#httpresponserexception)
- [<span data-ttu-id="76867-106">例外フィルター</span><span class="sxs-lookup"><span data-stu-id="76867-106">Exception Filters</span></span>](#exception_filters)
- [<span data-ttu-id="76867-107">登録 (例外フィルターを)</span><span class="sxs-lookup"><span data-stu-id="76867-107">Registering Exception Filters</span></span>](#registering_exception_filters)
- [<span data-ttu-id="76867-108">Http エラー</span><span class="sxs-lookup"><span data-stu-id="76867-108">HttpError</span></span>](#httperror)

<a id="httpresponserexception"></a>
## <a name="httpresponseexception"></a><span data-ttu-id="76867-109">HttpResponseException</span><span class="sxs-lookup"><span data-stu-id="76867-109">HttpResponseException</span></span>

<span data-ttu-id="76867-110">Web API コントローラーでキャッチされない例外がスローされるとどうなりますか。</span><span class="sxs-lookup"><span data-stu-id="76867-110">What happens if a Web API controller throws an uncaught exception?</span></span> <span data-ttu-id="76867-111">既定では、ほとんどの例外は、状態コード500、内部サーバーエラーを含む HTTP 応答に変換されます。</span><span class="sxs-lookup"><span data-stu-id="76867-111">By default, most exceptions are translated into an HTTP response with status code 500, Internal Server Error.</span></span>

<span data-ttu-id="76867-112">**HttpResponseException**型は特殊なケースです。</span><span class="sxs-lookup"><span data-stu-id="76867-112">The **HttpResponseException** type is a special case.</span></span> <span data-ttu-id="76867-113">この例外は、例外コンストラクターで指定した HTTP 状態コードを返します。</span><span class="sxs-lookup"><span data-stu-id="76867-113">This exception returns any HTTP status code that you specify in the exception constructor.</span></span> <span data-ttu-id="76867-114">たとえば、次のメソッドは、 *id*パラメーターが有効でない場合に、404 (見つからない) を返します。</span><span class="sxs-lookup"><span data-stu-id="76867-114">For example, the following method returns 404, Not Found, if the *id* parameter is not valid.</span></span>

[!code-csharp[Main](exception-handling/samples/sample1.cs)]

<span data-ttu-id="76867-115">応答をより詳細に制御するには、応答メッセージ全体を作成し、HttpResponseException に含めることもでき**ます。**</span><span class="sxs-lookup"><span data-stu-id="76867-115">For more control over the response, you can also construct the entire response message and include it with the **HttpResponseException:**</span></span> 

[!code-csharp[Main](exception-handling/samples/sample2.cs)]

<a id="exception_filters"></a>
## <a name="exception-filters"></a><span data-ttu-id="76867-116">例外フィルター</span><span class="sxs-lookup"><span data-stu-id="76867-116">Exception Filters</span></span>

<span data-ttu-id="76867-117">*例外フィルター*を記述することで、Web API が例外を処理する方法をカスタマイズできます。</span><span class="sxs-lookup"><span data-stu-id="76867-117">You can customize how Web API handles exceptions by writing an *exception filter*.</span></span> <span data-ttu-id="76867-118">例外フィルターは、コントローラーメソッドが、 **HttpResponseException**例外ではないハンドルされ*ない*例外をスローしたときに実行されます。</span><span class="sxs-lookup"><span data-stu-id="76867-118">An exception filter is executed when a controller method throws any unhandled exception that is *not* an **HttpResponseException** exception.</span></span> <span data-ttu-id="76867-119">**HttpResponseException**型は特殊なケースです。これは、HTTP 応答を返す専用に設計されているためです。</span><span class="sxs-lookup"><span data-stu-id="76867-119">The **HttpResponseException** type is a special case, because it is designed specifically for returning an HTTP response.</span></span>

<span data-ttu-id="76867-120">例外フィルターは、 **System.web Exceptionfilter**インターフェイスを実装します。</span><span class="sxs-lookup"><span data-stu-id="76867-120">Exception filters implement the **System.Web.Http.Filters.IExceptionFilter** interface.</span></span> <span data-ttu-id="76867-121">例外フィルターを記述する最も簡単な方法**は、system.exception クラスから**派生させ、 **onexception**メソッドをオーバーライドすることです。</span><span class="sxs-lookup"><span data-stu-id="76867-121">The simplest way to write an exception filter is to derive from the **System.Web.Http.Filters.ExceptionFilterAttribute** class and override the **OnException** method.</span></span>

> [!NOTE]
> <span data-ttu-id="76867-122">ASP.NET Web API での例外フィルターは、ASP.NET MVC と似ています。</span><span class="sxs-lookup"><span data-stu-id="76867-122">Exception filters in ASP.NET Web API are similar to those in ASP.NET MVC.</span></span> <span data-ttu-id="76867-123">ただし、これらは個別の名前空間と関数で宣言されています。</span><span class="sxs-lookup"><span data-stu-id="76867-123">However, they are declared in a separate namespace and function separately.</span></span> <span data-ttu-id="76867-124">特に、MVC で使用される**Handleerrorattribute**クラスは、Web API コントローラーによってスローされる例外を処理しません。</span><span class="sxs-lookup"><span data-stu-id="76867-124">In particular, the **HandleErrorAttribute** class used in MVC does not handle exceptions thrown by Web API controllers.</span></span>

<span data-ttu-id="76867-125">**NotImplementedException**例外を HTTP 状態コード501に変換するフィルターを次に示します (実装されていません)。</span><span class="sxs-lookup"><span data-stu-id="76867-125">Here is a filter that converts **NotImplementedException** exceptions into HTTP status code 501, Not Implemented:</span></span>

[!code-csharp[Main](exception-handling/samples/sample3.cs)]

<span data-ttu-id="76867-126">**Httpactionexecutedcontext**オブジェクトの**response**プロパティには、クライアントに送信される HTTP 応答メッセージが含まれています。</span><span class="sxs-lookup"><span data-stu-id="76867-126">The **Response** property of the **HttpActionExecutedContext** object contains the HTTP response message that will be sent to the client.</span></span>

<a id="registering_exception_filters"></a>
## <a name="registering-exception-filters"></a><span data-ttu-id="76867-127">登録 (例外フィルターを)</span><span class="sxs-lookup"><span data-stu-id="76867-127">Registering Exception Filters</span></span>

<span data-ttu-id="76867-128">Web API 例外フィルターを登録する方法はいくつかあります。</span><span class="sxs-lookup"><span data-stu-id="76867-128">There are several ways to register a Web API exception filter:</span></span>

- <span data-ttu-id="76867-129">アクションごと</span><span class="sxs-lookup"><span data-stu-id="76867-129">By action</span></span>
- <span data-ttu-id="76867-130">コントローラーごと</span><span class="sxs-lookup"><span data-stu-id="76867-130">By controller</span></span>
- <span data-ttu-id="76867-131">グローバル</span><span class="sxs-lookup"><span data-stu-id="76867-131">Globally</span></span>

<span data-ttu-id="76867-132">特定のアクションにフィルターを適用するには、フィルターをアクションに属性として追加します。</span><span class="sxs-lookup"><span data-stu-id="76867-132">To apply the filter to a specific action, add the filter as an attribute to the action:</span></span>

[!code-csharp[Main](exception-handling/samples/sample4.cs)]

<span data-ttu-id="76867-133">コントローラー上のすべてのアクションにフィルターを適用するには、フィルターを属性としてコントローラークラスに追加します。</span><span class="sxs-lookup"><span data-stu-id="76867-133">To apply the filter to all of the actions on a controller, add the filter as an attribute to the controller class:</span></span>

[!code-csharp[Main](exception-handling/samples/sample5.cs)]

<span data-ttu-id="76867-134">すべての Web API コントローラーに対してフィルターをグローバルに適用するには、フィルターのインスタンスを**Globalconfiguration. Configuration. Filters**コレクションに追加します。</span><span class="sxs-lookup"><span data-stu-id="76867-134">To apply the filter globally to all Web API controllers, add an instance of the filter to the **GlobalConfiguration.Configuration.Filters** collection.</span></span> <span data-ttu-id="76867-135">このコレクション内の例外フィルターは、任意の Web API コントローラー アクションに適用されます。</span><span class="sxs-lookup"><span data-stu-id="76867-135">Exception filters in this collection apply to any Web API controller action.</span></span>

[!code-csharp[Main](exception-handling/samples/sample6.cs)]

<span data-ttu-id="76867-136">"ASP.NET MVC 4 Web アプリケーション" プロジェクトテンプレートを使用してプロジェクトを作成する場合は、Web API 構成コードを `WebApiConfig` クラス内に配置します。このクラスは、アプリ\_の [開始] フォルダーにあります。</span><span class="sxs-lookup"><span data-stu-id="76867-136">If you use the "ASP.NET MVC 4 Web Application" project template to create your project, put your Web API configuration code inside the `WebApiConfig` class, which is located in the App\_Start folder:</span></span>

[!code-csharp[Main](exception-handling/samples/sample7.cs?highlight=5)]

<a id="httperror"></a>
## <a name="httperror"></a><span data-ttu-id="76867-137">Http エラー</span><span class="sxs-lookup"><span data-stu-id="76867-137">HttpError</span></span>

<span data-ttu-id="76867-138">**Httperror**オブジェクトは、応答本文にエラー情報を返す一貫した方法を提供します。</span><span class="sxs-lookup"><span data-stu-id="76867-138">The **HttpError** object provides a consistent way to return error information in the response body.</span></span> <span data-ttu-id="76867-139">次の例では、HTTP 状態コード 404 (見つからない) を応答本文で**httperror**状態で返す方法を示します。</span><span class="sxs-lookup"><span data-stu-id="76867-139">The following example shows how to return HTTP status code 404 (Not Found) with an **HttpError** in the response body.</span></span>

[!code-csharp[Main](exception-handling/samples/sample8.cs)]

<span data-ttu-id="76867-140">**Createerrorresponse**は、 **HttpRequestMessageExtensions**クラスで定義されている拡張メソッドです。</span><span class="sxs-lookup"><span data-stu-id="76867-140">**CreateErrorResponse** is an extension method defined in the **System.Net.Http.HttpRequestMessageExtensions** class.</span></span> <span data-ttu-id="76867-141">内部的には、 **Createerrorresponse**は**httperror**インスタンスを作成し、 **httperror**を含むを作成します。</span><span class="sxs-lookup"><span data-stu-id="76867-141">Internally, **CreateErrorResponse** creates an **HttpError** instance and then creates an **HttpResponseMessage** that contains the **HttpError**.</span></span>

<span data-ttu-id="76867-142">この例では、メソッドが成功した場合、HTTP 応答で製品が返されます。</span><span class="sxs-lookup"><span data-stu-id="76867-142">In this example, if the method is successful, it returns the product in the HTTP response.</span></span> <span data-ttu-id="76867-143">ただし、要求された製品が見つからない場合、HTTP 応答には要求本文に**httperror**含まれています。</span><span class="sxs-lookup"><span data-stu-id="76867-143">But if the requested product is not found, the HTTP response contains an **HttpError** in the request body.</span></span> <span data-ttu-id="76867-144">応答は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="76867-144">The response might look like the following:</span></span>

[!code-console[Main](exception-handling/samples/sample9.cmd)]

<span data-ttu-id="76867-145">この例では、 **HTTPERROR** JSON にシリアル化されていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="76867-145">Notice that the **HttpError** was serialized to JSON in this example.</span></span> <span data-ttu-id="76867-146">**Httperror**使用する利点の1つは、その他の厳密に型指定されたモデルと同じ[コンテンツネゴシエーション](../formats-and-model-binding/content-negotiation.md)およびシリアル化プロセスを通過することです。</span><span class="sxs-lookup"><span data-stu-id="76867-146">One advantage of using **HttpError** is that it goes through the same [content-negotiation](../formats-and-model-binding/content-negotiation.md) and serialization process as any other strongly-typed model.</span></span>

### <a name="httperror-and-model-validation"></a><span data-ttu-id="76867-147">HttpError エラーとモデルの検証</span><span class="sxs-lookup"><span data-stu-id="76867-147">HttpError and Model Validation</span></span>

<span data-ttu-id="76867-148">モデルの検証では、モデルの状態を**Createerrorresponse**に渡して、検証エラーを応答に含めることができます。</span><span class="sxs-lookup"><span data-stu-id="76867-148">For model validation, you can pass the model state to **CreateErrorResponse**, to include the validation errors in the response:</span></span>

[!code-csharp[Main](exception-handling/samples/sample10.cs)]

<span data-ttu-id="76867-149">この例では、次の応答が返される場合があります。</span><span class="sxs-lookup"><span data-stu-id="76867-149">This example might return the following response:</span></span>

[!code-console[Main](exception-handling/samples/sample11.cmd)]

<span data-ttu-id="76867-150">モデルの検証の詳細については、「 [ASP.NET Web API でのモデルの検証](../formats-and-model-binding/model-validation-in-aspnet-web-api.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="76867-150">For more information about model validation, see [Model Validation in ASP.NET Web API](../formats-and-model-binding/model-validation-in-aspnet-web-api.md).</span></span>

### <a name="using-httperror-with-httpresponseexception"></a><span data-ttu-id="76867-151">HttpResponseException での HttpError 使用</span><span class="sxs-lookup"><span data-stu-id="76867-151">Using HttpError with HttpResponseException</span></span>

<span data-ttu-id="76867-152">前の例では、コントローラーアクションから**HttpResponseMessage**メッセージが返されますが、 **HttpResponseException**を使用して**httperror**返すこともできます。</span><span class="sxs-lookup"><span data-stu-id="76867-152">The previous examples return an **HttpResponseMessage** message from the controller action, but you can also use **HttpResponseException** to return an **HttpError**.</span></span> <span data-ttu-id="76867-153">これにより、通常の成功事例では厳密に型指定されたモデルを返すことができますが、エラーが発生しても**httperror**返されます。</span><span class="sxs-lookup"><span data-stu-id="76867-153">This lets you return a strongly-typed model in the normal success case, while still returning **HttpError** if there is an error:</span></span>

[!code-csharp[Main](exception-handling/samples/sample12.cs)]
