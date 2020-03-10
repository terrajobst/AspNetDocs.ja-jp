---
uid: web-api/overview/getting-started-with-aspnet-web-api/using-web-api-with-aspnet-web-forms
title: Web API と ASP.NET Web フォームの使用-ASP.NET 4.x
author: MikeWasson
description: ASP.NET 4.x 用の ASP.NET Forms アプリケーションに Web API を追加するためのコード手順を説明したチュートリアル
ms.author: riande
ms.date: 04/03/2012
ms.custom: seoapril2019
ms.assetid: 25da8c3f-4e90-4946-9765-4f160985e1e4
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/using-web-api-with-aspnet-web-forms
msc.type: authoredcontent
ms.openlocfilehash: ae553b62998fefd128e12711cbde958ea42d8c63
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448534"
---
# <a name="using-web-api-with-aspnet-web-forms"></a><span data-ttu-id="86b35-103">ASP.NET Web フォームでの Web API の使用</span><span class="sxs-lookup"><span data-stu-id="86b35-103">Using Web API with ASP.NET Web Forms</span></span>

<span data-ttu-id="86b35-104">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="86b35-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="86b35-105">このチュートリアルでは、ASP.NET 4.x の従来の ASP.NET Web フォームアプリケーションに Web API を追加する手順について説明します。</span><span class="sxs-lookup"><span data-stu-id="86b35-105">This tutorial walks you through the steps to add Web API to a traditional ASP.NET Web Forms application in ASP.NET 4.x.</span></span> 

## <a name="overview"></a><span data-ttu-id="86b35-106">概要</span><span class="sxs-lookup"><span data-stu-id="86b35-106">Overview</span></span>

<span data-ttu-id="86b35-107">ASP.NET Web API は ASP.NET MVC でパッケージ化されていますが、従来の ASP.NET Web フォームアプリケーションに Web API を簡単に追加できます。</span><span class="sxs-lookup"><span data-stu-id="86b35-107">Although ASP.NET Web API is packaged with ASP.NET MVC, it is easy to add Web API to a traditional ASP.NET Web Forms application.</span></span>

<span data-ttu-id="86b35-108">Web フォームアプリケーションで Web API を使用するには、次の2つの主要な手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="86b35-108">To use Web API in a Web Forms application, there are two main steps:</span></span>

- <span data-ttu-id="86b35-109">**ApiController**クラスから派生した Web API コントローラーを追加します。</span><span class="sxs-lookup"><span data-stu-id="86b35-109">Add a Web API controller that derives from the **ApiController** class.</span></span>
- <span data-ttu-id="86b35-110">ルートテーブルを**アプリケーション\_の開始**メソッドに追加します。</span><span class="sxs-lookup"><span data-stu-id="86b35-110">Add a route table to the **Application\_Start** method.</span></span>

## <a name="create-a-web-forms-project"></a><span data-ttu-id="86b35-111">Web フォームプロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="86b35-111">Create a Web Forms Project</span></span>

<span data-ttu-id="86b35-112">Visual Studio を起動し、**スタート**ページで **[新しいプロジェクト]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="86b35-112">Start Visual Studio and select **New Project** from the **Start** page.</span></span> <span data-ttu-id="86b35-113">または、 **[ファイル]** メニューの **[新規作成]** をポイントし、 **[プロジェクト]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="86b35-113">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<span data-ttu-id="86b35-114">**[テンプレート]** ペインで、 **[インストールされたテンプレート]** を選択し、  **C#ビジュアル**ノードを展開します。</span><span class="sxs-lookup"><span data-stu-id="86b35-114">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="86b35-115">**[ビジュアルC# ]** で **[Web]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="86b35-115">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="86b35-116">プロジェクトテンプレートの一覧で、 **[ASP.NET Web フォームアプリケーション]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="86b35-116">In the list of project templates, select **ASP.NET Web Forms Application**.</span></span> <span data-ttu-id="86b35-117">プロジェクトの名前を入力し、[ **OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="86b35-117">Enter a name for the project and click **OK**.</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image1.png)

## <a name="create-the-model-and-controller"></a><span data-ttu-id="86b35-118">モデルとコントローラーを作成する</span><span class="sxs-lookup"><span data-stu-id="86b35-118">Create the Model and Controller</span></span>

<span data-ttu-id="86b35-119">このチュートリアルでは、[はじめに](tutorial-your-first-web-api.md)チュートリアルと同じモデルとコントローラークラスを使用します。</span><span class="sxs-lookup"><span data-stu-id="86b35-119">This tutorial uses the same model and controller classes as the [Getting Started](tutorial-your-first-web-api.md) tutorial.</span></span>

<span data-ttu-id="86b35-120">まず、モデルクラスを追加します。</span><span class="sxs-lookup"><span data-stu-id="86b35-120">First, add a model class.</span></span> <span data-ttu-id="86b35-121">**ソリューションエクスプローラー**で、プロジェクトを右クリックし、 **[クラスの追加]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="86b35-121">In **Solution Explorer**, right-click the project and select **Add Class**.</span></span> <span data-ttu-id="86b35-122">クラスに Product という名前を指定し、次の実装を追加します。</span><span class="sxs-lookup"><span data-stu-id="86b35-122">Name the class Product, and add the following implementation:</span></span>

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample1.cs)]

<span data-ttu-id="86b35-123">次に、Web API コントローラーをプロジェクトに追加します。*コントローラー*は、web API の HTTP 要求を処理するオブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="86b35-123">Next, add a Web API controller to the project., A *controller* is the object that handles HTTP requests for Web API.</span></span>

<span data-ttu-id="86b35-124">**Solution Explorer** で、プロジェクト名を右クリックします。</span><span class="sxs-lookup"><span data-stu-id="86b35-124">In **Solution Explorer**, right-click the project.</span></span> <span data-ttu-id="86b35-125">**[新しい項目の追加]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="86b35-125">Select **Add New Item**.</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image2.png)

<span data-ttu-id="86b35-126">**[インストールされたテンプレート]** で **[ C#ビジュアル]** を展開し、 **[Web]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="86b35-126">Under **Installed Templates**, expand **Visual C#** and select **Web**.</span></span> <span data-ttu-id="86b35-127">次に、テンプレートの一覧から **[WEB API コントローラークラス]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="86b35-127">Then, from the list of templates, select **Web API Controller Class**.</span></span> <span data-ttu-id="86b35-128">コントローラーに "製品コントローラー" という名前を指定し、 **[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="86b35-128">Name the controller "ProductsController" and click **Add**.</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image3.png)

<span data-ttu-id="86b35-129">**新しい項目の追加**ウィザードでは、ProductsController.cs という名前のファイルが作成されます。</span><span class="sxs-lookup"><span data-stu-id="86b35-129">The **Add New Item** wizard will create a file named ProductsController.cs.</span></span> <span data-ttu-id="86b35-130">ウィザードに含まれているメソッドを削除し、次のメソッドを追加します。</span><span class="sxs-lookup"><span data-stu-id="86b35-130">Delete the methods that the wizard included and add the following methods:</span></span>

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample2.cs)]

<span data-ttu-id="86b35-131">このコントローラーのコードの詳細については、[はじめに](tutorial-your-first-web-api.md)チュートリアルを参照してください。</span><span class="sxs-lookup"><span data-stu-id="86b35-131">For more information about the code in this controller, see the [Getting Started](tutorial-your-first-web-api.md) tutorial.</span></span>

## <a name="add-routing-information"></a><span data-ttu-id="86b35-132">ルーティング情報の追加</span><span class="sxs-lookup"><span data-stu-id="86b35-132">Add Routing Information</span></span>

<span data-ttu-id="86b35-133">次に、URI ルートを追加します。これにより、フォーム &quot;/api/&quot; の Uri がコントローラーにルーティングされるようになります。</span><span class="sxs-lookup"><span data-stu-id="86b35-133">Next, we'll add a URI route so that URIs of the form &quot;/api/products/&quot; are routed to the controller.</span></span>

<span data-ttu-id="86b35-134">**ソリューションエクスプローラー**で、[global.asax] をダブルクリックして、分離コードファイル Global.asax.cs を開きます。</span><span class="sxs-lookup"><span data-stu-id="86b35-134">In **Solution Explorer**, double-click Global.asax to open the code-behind file Global.asax.cs.</span></span> <span data-ttu-id="86b35-135">次の**using ステートメントを**追加します。</span><span class="sxs-lookup"><span data-stu-id="86b35-135">Add the following **using** statement.</span></span>

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample3.cs)]

<span data-ttu-id="86b35-136">次に、 **Application\_Start**メソッドに次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="86b35-136">Then add the following code to the **Application\_Start** method:</span></span>

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample4.cs)]

<span data-ttu-id="86b35-137">ルーティングテーブルの詳細については、「 [ASP.NET Web API でのルーティング](../web-api-routing-and-actions/routing-in-aspnet-web-api.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="86b35-137">For more information about routing tables, see [Routing in ASP.NET Web API](../web-api-routing-and-actions/routing-in-aspnet-web-api.md).</span></span>

## <a name="add-client-side-ajax"></a><span data-ttu-id="86b35-138">クライアント側 AJAX の追加</span><span class="sxs-lookup"><span data-stu-id="86b35-138">Add Client-Side AJAX</span></span>

<span data-ttu-id="86b35-139">これで、クライアントがアクセスできる web API を作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="86b35-139">That's all you need to create a web API that clients can access.</span></span> <span data-ttu-id="86b35-140">次に、jQuery を使用して API を呼び出す HTML ページを追加します。</span><span class="sxs-lookup"><span data-stu-id="86b35-140">Now let's add an HTML page that uses jQuery to call the API.</span></span>

<span data-ttu-id="86b35-141">マスターページ (たとえば、「 *master*」) に `ID="HeadContent"`の `ContentPlaceHolder` が含まれていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="86b35-141">Make sure your master page (for example, *Site.Master*) includes a `ContentPlaceHolder` with `ID="HeadContent"`:</span></span>

[!code-html[Main](using-web-api-with-aspnet-web-forms/samples/sample8.html)]

<span data-ttu-id="86b35-142">Default.aspx ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="86b35-142">Open the file Default.aspx.</span></span> <span data-ttu-id="86b35-143">次に示すように、メインコンテンツセクションにある定型テキストを置き換えます。</span><span class="sxs-lookup"><span data-stu-id="86b35-143">Replace the boilerplate text that is in the main content section, as shown:</span></span>

[!code-aspx[Main](using-web-api-with-aspnet-web-forms/samples/sample5.aspx)]

<span data-ttu-id="86b35-144">次に、`HeaderContent` セクションで jQuery ソースファイルへの参照を追加します。</span><span class="sxs-lookup"><span data-stu-id="86b35-144">Next, add a reference to the jQuery source file in the `HeaderContent` section:</span></span>

[!code-aspx[Main](using-web-api-with-aspnet-web-forms/samples/sample6.aspx?highlight=2)]

<span data-ttu-id="86b35-145">注:**ソリューションエクスプローラー**からコードエディターウィンドウにファイルをドラッグアンドドロップすることで、スクリプト参照を簡単に追加できます。</span><span class="sxs-lookup"><span data-stu-id="86b35-145">Note: You can easily add the script reference by dragging and dropping the file from **Solution Explorer** into the code editor window.</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image4.png)

<span data-ttu-id="86b35-146">JQuery script タグの下に、次のスクリプトブロックを追加します。</span><span class="sxs-lookup"><span data-stu-id="86b35-146">Below the jQuery script tag, add the following script block:</span></span>

[!code-html[Main](using-web-api-with-aspnet-web-forms/samples/sample7.html)]

<span data-ttu-id="86b35-147">ドキュメントが読み込まれると、このスクリプトは、&quot;api/products&quot;に AJAX 要求を行います。</span><span class="sxs-lookup"><span data-stu-id="86b35-147">When the document loads, this script makes an AJAX request to &quot;api/products&quot;.</span></span> <span data-ttu-id="86b35-148">要求は、JSON 形式で製品の一覧を返します。</span><span class="sxs-lookup"><span data-stu-id="86b35-148">The request returns a list of products in JSON format.</span></span> <span data-ttu-id="86b35-149">このスクリプトにより、製品情報が HTML テーブルに追加されます。</span><span class="sxs-lookup"><span data-stu-id="86b35-149">The script adds the product information to the HTML table.</span></span>

<span data-ttu-id="86b35-150">アプリケーションを実行すると、次のようになります。</span><span class="sxs-lookup"><span data-stu-id="86b35-150">When you run the application, it should look like this:</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image5.png)
