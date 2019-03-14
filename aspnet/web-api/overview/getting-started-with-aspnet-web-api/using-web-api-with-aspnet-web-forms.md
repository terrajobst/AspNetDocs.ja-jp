---
uid: web-api/overview/getting-started-with-aspnet-web-api/using-web-api-with-aspnet-web-forms
title: ASP.NET Web フォームによる Web API の使用 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 04/03/2012
ms.assetid: 25da8c3f-4e90-4946-9765-4f160985e1e4
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/using-web-api-with-aspnet-web-forms
msc.type: authoredcontent
ms.openlocfilehash: a14bf0abd8c5d603cf3859891f855415cf3df9f3
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57055689"
---
<a name="using-web-api-with-aspnet-web-forms"></a><span data-ttu-id="9b0da-102">ASP.NET Web フォームで Web API を使用する</span><span class="sxs-lookup"><span data-stu-id="9b0da-102">Using Web API with ASP.NET Web Forms</span></span>
====================
<span data-ttu-id="9b0da-103">作成者[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="9b0da-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="9b0da-104">ASP.NET Web API は、ASP.NET MVC にパッケージ化されてが簡単に Web API を従来の ASP.NET Web フォーム アプリケーションに追加できます。</span><span class="sxs-lookup"><span data-stu-id="9b0da-104">Although ASP.NET Web API is packaged with ASP.NET MVC, it is easy to add Web API to a traditional ASP.NET Web Forms application.</span></span> <span data-ttu-id="9b0da-105">このチュートリアルの手順について説明します。</span><span class="sxs-lookup"><span data-stu-id="9b0da-105">This tutorial walks you through the steps.</span></span>

## <a name="overview"></a><span data-ttu-id="9b0da-106">概要</span><span class="sxs-lookup"><span data-stu-id="9b0da-106">Overview</span></span>

<span data-ttu-id="9b0da-107">Web フォーム アプリケーションで Web API を使用するには、2 つの主な手順があります。</span><span class="sxs-lookup"><span data-stu-id="9b0da-107">To use Web API in a Web Forms application, there are two main steps:</span></span>

- <span data-ttu-id="9b0da-108">派生した Web API コント ローラーを追加、 **ApiController**クラス。</span><span class="sxs-lookup"><span data-stu-id="9b0da-108">Add a Web API controller that derives from the **ApiController** class.</span></span>
- <span data-ttu-id="9b0da-109">ルート テーブルを追加、**アプリケーション\_開始**メソッド。</span><span class="sxs-lookup"><span data-stu-id="9b0da-109">Add a route table to the **Application\_Start** method.</span></span>

## <a name="create-a-web-forms-project"></a><span data-ttu-id="9b0da-110">Web フォーム プロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="9b0da-110">Create a Web Forms Project</span></span>

<span data-ttu-id="9b0da-111">Visual Studio を起動し、選択**新しいプロジェクト**から、**開始**ページ。</span><span class="sxs-lookup"><span data-stu-id="9b0da-111">Start Visual Studio and select **New Project** from the **Start** page.</span></span> <span data-ttu-id="9b0da-112">またはから、**ファイル**メニューの **新規**し**プロジェクト**します。</span><span class="sxs-lookup"><span data-stu-id="9b0da-112">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<span data-ttu-id="9b0da-113">**テンプレート**ペインで、**インストールされたテンプレート**を展開し、 **Visual c#** ノード。</span><span class="sxs-lookup"><span data-stu-id="9b0da-113">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="9b0da-114">**Visual c#**、 **Web**します。</span><span class="sxs-lookup"><span data-stu-id="9b0da-114">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="9b0da-115">プロジェクト テンプレートの一覧で選択**ASP.NET Web フォーム アプリケーション**します。</span><span class="sxs-lookup"><span data-stu-id="9b0da-115">In the list of project templates, select **ASP.NET Web Forms Application**.</span></span> <span data-ttu-id="9b0da-116">プロジェクトの名前を入力し、クリックして**OK**します。</span><span class="sxs-lookup"><span data-stu-id="9b0da-116">Enter a name for the project and click **OK**.</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image1.png)

## <a name="create-the-model-and-controller"></a><span data-ttu-id="9b0da-117">モデルとコント ローラーを作成します。</span><span class="sxs-lookup"><span data-stu-id="9b0da-117">Create the Model and Controller</span></span>

<span data-ttu-id="9b0da-118">このチュートリアルと同じモデルとコント ローラー クラスを使用して、 [Getting Started](tutorial-your-first-web-api.md)チュートリアル。</span><span class="sxs-lookup"><span data-stu-id="9b0da-118">This tutorial uses the same model and controller classes as the [Getting Started](tutorial-your-first-web-api.md) tutorial.</span></span>

<span data-ttu-id="9b0da-119">最初に、モデル クラスを追加します。</span><span class="sxs-lookup"><span data-stu-id="9b0da-119">First, add a model class.</span></span> <span data-ttu-id="9b0da-120">**ソリューション エクスプ ローラー**プロジェクトを右クリックし、選択、**クラスの追加**します。</span><span class="sxs-lookup"><span data-stu-id="9b0da-120">In **Solution Explorer**, right-click the project and select **Add Class**.</span></span> <span data-ttu-id="9b0da-121">製品、クラスの名前を次の実装を追加します。</span><span class="sxs-lookup"><span data-stu-id="9b0da-121">Name the class Product, and add the following implementation:</span></span>

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample1.cs)]

<span data-ttu-id="9b0da-122">次に、Web API コント ローラーを追加、プロジェクトに、A*コント ローラー*は Web API の HTTP 要求を処理するオブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="9b0da-122">Next, add a Web API controller to the project., A *controller* is the object that handles HTTP requests for Web API.</span></span>

<span data-ttu-id="9b0da-123">**Solution Explorer** で、プロジェクト名を右クリックします。</span><span class="sxs-lookup"><span data-stu-id="9b0da-123">In **Solution Explorer**, right-click the project.</span></span> <span data-ttu-id="9b0da-124">選択**新しい項目の追加**します。</span><span class="sxs-lookup"><span data-stu-id="9b0da-124">Select **Add New Item**.</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image2.png)

<span data-ttu-id="9b0da-125">**インストールされたテンプレート**、展開**Visual c#** 選択**Web**します。</span><span class="sxs-lookup"><span data-stu-id="9b0da-125">Under **Installed Templates**, expand **Visual C#** and select **Web**.</span></span> <span data-ttu-id="9b0da-126">次に、テンプレートの一覧から次のように選択します。 **Web API コント ローラー クラス**します。</span><span class="sxs-lookup"><span data-stu-id="9b0da-126">Then, from the list of templates, select **Web API Controller Class**.</span></span> <span data-ttu-id="9b0da-127">コント ローラーの名前を"ProductsController"にして**追加**します。</span><span class="sxs-lookup"><span data-stu-id="9b0da-127">Name the controller "ProductsController" and click **Add**.</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image3.png)

<span data-ttu-id="9b0da-128">**新しい項目の追加**ProductsController.cs という名前のファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="9b0da-128">The **Add New Item** wizard will create a file named ProductsController.cs.</span></span> <span data-ttu-id="9b0da-129">ウィザードが含まれているメソッドを削除し、次のメソッドを追加します。</span><span class="sxs-lookup"><span data-stu-id="9b0da-129">Delete the methods that the wizard included and add the following methods:</span></span>

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample2.cs)]

<span data-ttu-id="9b0da-130">このコント ローラー コードの詳細については、次を参照してください。、 [Getting Started](tutorial-your-first-web-api.md)チュートリアル。</span><span class="sxs-lookup"><span data-stu-id="9b0da-130">For more information about the code in this controller, see the [Getting Started](tutorial-your-first-web-api.md) tutorial.</span></span>

## <a name="add-routing-information"></a><span data-ttu-id="9b0da-131">ルーティング情報を追加します。</span><span class="sxs-lookup"><span data-stu-id="9b0da-131">Add Routing Information</span></span>

<span data-ttu-id="9b0da-132">次に、追加します URI ルートのため形式の Uri &quot;/api/製品/&quot;コント ローラーにルーティングされます。</span><span class="sxs-lookup"><span data-stu-id="9b0da-132">Next, we'll add a URI route so that URIs of the form &quot;/api/products/&quot; are routed to the controller.</span></span>

<span data-ttu-id="9b0da-133">**ソリューション エクスプ ローラー**、Global.asax Global.asax.cs の分離コード ファイルを開く をダブルクリックします。</span><span class="sxs-lookup"><span data-stu-id="9b0da-133">In **Solution Explorer**, double-click Global.asax to open the code-behind file Global.asax.cs.</span></span> <span data-ttu-id="9b0da-134">次の追加**を使用して**ステートメント。</span><span class="sxs-lookup"><span data-stu-id="9b0da-134">Add the following **using** statement.</span></span>

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample3.cs)]

<span data-ttu-id="9b0da-135">次のコードを追加し、**アプリケーション\_開始**メソッド。</span><span class="sxs-lookup"><span data-stu-id="9b0da-135">Then add the following code to the **Application\_Start** method:</span></span>

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample4.cs)]

<span data-ttu-id="9b0da-136">ルーティング テーブルの詳細については、次を参照してください。 [ASP.NET Web API におけるルーティング](../web-api-routing-and-actions/routing-in-aspnet-web-api.md)します。</span><span class="sxs-lookup"><span data-stu-id="9b0da-136">For more information about routing tables, see [Routing in ASP.NET Web API](../web-api-routing-and-actions/routing-in-aspnet-web-api.md).</span></span>

## <a name="add-client-side-ajax"></a><span data-ttu-id="9b0da-137">クライアント側 AJAX を追加します。</span><span class="sxs-lookup"><span data-stu-id="9b0da-137">Add Client-Side AJAX</span></span>

<span data-ttu-id="9b0da-138">Web クライアントにアクセスできる API を作成する必要があるだけです。</span><span class="sxs-lookup"><span data-stu-id="9b0da-138">That's all you need to create a web API that clients can access.</span></span> <span data-ttu-id="9b0da-139">これで、API の呼び出しに jQuery を使用する HTML ページを追加してみましょう。</span><span class="sxs-lookup"><span data-stu-id="9b0da-139">Now let's add an HTML page that uses jQuery to call the API.</span></span>

<span data-ttu-id="9b0da-140">マスター ページを確認します (たとえば、 *Site.Master*) が含まれています、`ContentPlaceHolder`で`ID="HeadContent"`:</span><span class="sxs-lookup"><span data-stu-id="9b0da-140">Make sure your master page (for example, *Site.Master*) includes a `ContentPlaceHolder` with `ID="HeadContent"`:</span></span>

[!code-html[Main](using-web-api-with-aspnet-web-forms/samples/sample8.html)]

<span data-ttu-id="9b0da-141">Default.aspx ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="9b0da-141">Open the file Default.aspx.</span></span> <span data-ttu-id="9b0da-142">示すように、メイン コンテンツのセクションでは、定型テキストを置き換えます。</span><span class="sxs-lookup"><span data-stu-id="9b0da-142">Replace the boilerplate text that is in the main content section, as shown:</span></span>

[!code-aspx[Main](using-web-api-with-aspnet-web-forms/samples/sample5.aspx)]

<span data-ttu-id="9b0da-143">次に、jQuery のソース ファイルへの参照を追加、`HeaderContent`セクション。</span><span class="sxs-lookup"><span data-stu-id="9b0da-143">Next, add a reference to the jQuery source file in the `HeaderContent` section:</span></span>

[!code-aspx[Main](using-web-api-with-aspnet-web-forms/samples/sample6.aspx?highlight=2)]

<span data-ttu-id="9b0da-144">メモ:ドラッグ アンド ドロップ ファイルからスクリプト参照を簡単に追加することができます**ソリューション エクスプ ローラー**がコード エディター ウィンドウにします。</span><span class="sxs-lookup"><span data-stu-id="9b0da-144">Note: You can easily add the script reference by dragging and dropping the file from **Solution Explorer** into the code editor window.</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image4.png)

<span data-ttu-id="9b0da-145">JQuery スクリプト タグでは、下には、次のスクリプト ブロックを追加します。</span><span class="sxs-lookup"><span data-stu-id="9b0da-145">Below the jQuery script tag, add the following script block:</span></span>

[!code-html[Main](using-web-api-with-aspnet-web-forms/samples/sample7.html)]

<span data-ttu-id="9b0da-146">このスクリプトで、AJAX 要求には、ドキュメントが読み込まれると、 &quot;api/製品&quot;します。</span><span class="sxs-lookup"><span data-stu-id="9b0da-146">When the document loads, this script makes an AJAX request to &quot;api/products&quot;.</span></span> <span data-ttu-id="9b0da-147">要求は、JSON 形式で製品の一覧を返します。</span><span class="sxs-lookup"><span data-stu-id="9b0da-147">The request returns a list of products in JSON format.</span></span> <span data-ttu-id="9b0da-148">スクリプトでは、HTML テーブルに製品情報を追加します。</span><span class="sxs-lookup"><span data-stu-id="9b0da-148">The script adds the product information to the HTML table.</span></span>

<span data-ttu-id="9b0da-149">アプリケーションを実行するようになります。</span><span class="sxs-lookup"><span data-stu-id="9b0da-149">When you run the application, it should look like this:</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image5.png)
