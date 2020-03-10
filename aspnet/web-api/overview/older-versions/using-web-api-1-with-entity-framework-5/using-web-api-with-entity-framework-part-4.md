---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-4
title: 'パート 4: 管理者ビューの追加 |Microsoft Docs'
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: 792f4513-a508-4d14-a0dd-1a2fe282c7bb
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-4
msc.type: authoredcontent
ms.openlocfilehash: 664aeb33031e933322886a6d6bdd989277e9fda2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78447880"
---
# <a name="part-4-adding-an-admin-view"></a><span data-ttu-id="5e894-102">パート 4: 管理ビューの追加</span><span class="sxs-lookup"><span data-stu-id="5e894-102">Part 4: Adding an Admin View</span></span>

<span data-ttu-id="5e894-103">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="5e894-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="5e894-104">完成したプロジェクトのダウンロード</span><span class="sxs-lookup"><span data-stu-id="5e894-104">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-an-admin-view"></a><span data-ttu-id="5e894-105">管理ビューの追加</span><span class="sxs-lookup"><span data-stu-id="5e894-105">Add an Admin View</span></span>

<span data-ttu-id="5e894-106">次に、クライアント側に切り替え、管理コントローラーのデータを使用できるページを追加します。</span><span class="sxs-lookup"><span data-stu-id="5e894-106">Now we'll turn to the client side, and add a page that can consume data from the Admin controller.</span></span> <span data-ttu-id="5e894-107">このページでは、ユーザーが AJAX 要求をコントローラーに送信することによって、製品の作成、編集、または削除を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="5e894-107">The page will allow users to create, edit, or delete products, by sending AJAX requests to the controller.</span></span>

<span data-ttu-id="5e894-108">ソリューションエクスプローラーで、Controllers フォルダーを展開し、HomeController.cs という名前のファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="5e894-108">In Solution Explorer, expand the Controllers folder and open the file named HomeController.cs.</span></span> <span data-ttu-id="5e894-109">このファイルには、MVC コントローラーが含まれています。</span><span class="sxs-lookup"><span data-stu-id="5e894-109">This file contains an MVC controller.</span></span> <span data-ttu-id="5e894-110">`Admin`という名前のメソッドを追加します。</span><span class="sxs-lookup"><span data-stu-id="5e894-110">Add a method named `Admin`:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample1.cs)]

<span data-ttu-id="5e894-111">**HttpRouteUrl**メソッドは、web API への URI を作成し、後でこのをビューバッグに格納します。</span><span class="sxs-lookup"><span data-stu-id="5e894-111">The **HttpRouteUrl** method creates the URI to the web API, and we store this in the view bag for later.</span></span>

<span data-ttu-id="5e894-112">次に、`Admin` アクションメソッド内にテキストカーソルを置き、右クリックして **[ビューの追加]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="5e894-112">Next, position the text cursor within the `Admin` action method, then right-click and select **Add View**.</span></span> <span data-ttu-id="5e894-113">**[ビューの追加]** ダイアログが表示されます。</span><span class="sxs-lookup"><span data-stu-id="5e894-113">This will bring up the **Add View** dialog.</span></span>

![](using-web-api-with-entity-framework-part-4/_static/image1.png)

<span data-ttu-id="5e894-114">**[ビューの追加]** ダイアログで、ビューに "Admin" という名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="5e894-114">In the **Add View** dialog, name the view "Admin".</span></span> <span data-ttu-id="5e894-115">**[厳密に型指定されたビューを作成する]** チェックボックスをオンにします。</span><span class="sxs-lookup"><span data-stu-id="5e894-115">Select the check box labeled **Create a strongly-typed view**.</span></span> <span data-ttu-id="5e894-116">**モデルクラス** で、Product (productstore) を選択します。</span><span class="sxs-lookup"><span data-stu-id="5e894-116">Under **Model Class**, select "Product (ProductStore.Models)".</span></span> <span data-ttu-id="5e894-117">その他のオプションはすべて既定値のままにしておきます。</span><span class="sxs-lookup"><span data-stu-id="5e894-117">Leave all the other options as their default values.</span></span>

![](using-web-api-with-entity-framework-part-4/_static/image2.png)

<span data-ttu-id="5e894-118">**[追加]** をクリックすると、Views/Home の下に Admin. cshtml という名前のファイルが追加されます。</span><span class="sxs-lookup"><span data-stu-id="5e894-118">Clicking **Add** adds a file named Admin.cshtml under Views/Home.</span></span> <span data-ttu-id="5e894-119">このファイルを開き、次の HTML を追加します。</span><span class="sxs-lookup"><span data-stu-id="5e894-119">Open this file and add the following HTML.</span></span> <span data-ttu-id="5e894-120">この HTML はページの構造を定義しますが、機能はまだ接続されていません。</span><span class="sxs-lookup"><span data-stu-id="5e894-120">This HTML defines the structure of the page, but no functionality is wired up yet.</span></span>

[!code-cshtml[Main](using-web-api-with-entity-framework-part-4/samples/sample2.cshtml)]

## <a name="create-a-link-to-the-admin-page"></a><span data-ttu-id="5e894-121">管理ページへのリンクを作成する</span><span class="sxs-lookup"><span data-stu-id="5e894-121">Create a Link to the Admin Page</span></span>

<span data-ttu-id="5e894-122">ソリューションエクスプローラーで、Views フォルダーを展開し、共有フォルダーを展開します。</span><span class="sxs-lookup"><span data-stu-id="5e894-122">In Solution Explorer, expand the Views folder and then expand the Shared folder.</span></span> <span data-ttu-id="5e894-123">\_Layout. cshtml という名前のファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="5e894-123">Open the file named \_Layout.cshtml.</span></span> <span data-ttu-id="5e894-124">Id が "menu" である**ul**要素と、管理ビューのアクションリンクを探します。</span><span class="sxs-lookup"><span data-stu-id="5e894-124">Locate the **ul** element with id = "menu", and an action link for the Admin view:</span></span>

[!code-cshtml[Main](using-web-api-with-entity-framework-part-4/samples/sample3.cshtml)]

> [!NOTE]
> <span data-ttu-id="5e894-125">サンプルプロジェクトでは、"ここにロゴを入力してください" という文字列を置き換えるなど、いくつかの外観の変更が加えられました。</span><span class="sxs-lookup"><span data-stu-id="5e894-125">In the sample project, I made a few other cosmetic changes, such as replacing the string "Your logo here".</span></span> <span data-ttu-id="5e894-126">これらは、アプリケーションの機能には影響しません。</span><span class="sxs-lookup"><span data-stu-id="5e894-126">These don't affect the functionality of the application.</span></span> <span data-ttu-id="5e894-127">プロジェクトをダウンロードし、ファイルを比較することができます。</span><span class="sxs-lookup"><span data-stu-id="5e894-127">You can download the project and compare the files.</span></span>

<span data-ttu-id="5e894-128">アプリケーションを実行し、ホームページの上部に表示される [Admin] \ (管理者 \) リンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="5e894-128">Run the application and click the "Admin" link that appears at the top of the home page.</span></span> <span data-ttu-id="5e894-129">管理者ページは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="5e894-129">The Admin page should look like the following:</span></span>

![](using-web-api-with-entity-framework-part-4/_static/image3.png)

<span data-ttu-id="5e894-130">現在、このページでは何も実行されません。</span><span class="sxs-lookup"><span data-stu-id="5e894-130">Right now, the page doesn't do anything.</span></span> <span data-ttu-id="5e894-131">次のセクションでは、ノックアウトを使用して動的 UI を作成します。</span><span class="sxs-lookup"><span data-stu-id="5e894-131">In the next section, we'll use Knockout.js to create a dynamic UI.</span></span>

## <a name="add-authorization"></a><span data-ttu-id="5e894-132">承認の追加</span><span class="sxs-lookup"><span data-stu-id="5e894-132">Add Authorization</span></span>

<span data-ttu-id="5e894-133">現在、管理者ページには、サイトにアクセスするすべてのユーザーがアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="5e894-133">The Admin page is currently accessible to anyone visiting the site.</span></span> <span data-ttu-id="5e894-134">これを変更して、管理者にアクセス許可を制限してみましょう。</span><span class="sxs-lookup"><span data-stu-id="5e894-134">Let's change this to restrict permission to administrators.</span></span>

<span data-ttu-id="5e894-135">まず、"管理者" ロールと管理者ユーザーを追加します。</span><span class="sxs-lookup"><span data-stu-id="5e894-135">Start by adding an "Administrator" role and an administrator user.</span></span> <span data-ttu-id="5e894-136">ソリューションエクスプローラーで、[フィルター] フォルダーを展開し、InitializeSimpleMembershipAttribute.cs という名前のファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="5e894-136">In Solution Explorer, expand the Filters folder and open the file named InitializeSimpleMembershipAttribute.cs.</span></span> <span data-ttu-id="5e894-137">`SimpleMembershipInitializer` コンストラクターを見つけます。</span><span class="sxs-lookup"><span data-stu-id="5e894-137">Locate the `SimpleMembershipInitializer` constructor.</span></span> <span data-ttu-id="5e894-138">**InitializeDatabaseConnection**の呼び出しの後に、次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="5e894-138">After the call to **WebSecurity.InitializeDatabaseConnection**, add the following code:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample4.cs)]

<span data-ttu-id="5e894-139">これは、"管理者" ロールを追加し、ロールのユーザーを作成するための簡単な方法です。</span><span class="sxs-lookup"><span data-stu-id="5e894-139">This is a quick-and-dirty way to add the "Administrator" role and create a user for the role.</span></span>

<span data-ttu-id="5e894-140">ソリューションエクスプローラーで、Controllers フォルダーを展開し、HomeController.cs ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="5e894-140">In Solution Explorer, expand the Controllers folder and open the HomeController.cs file.</span></span> <span data-ttu-id="5e894-141">`Admin` メソッドに**承認**属性を追加します。</span><span class="sxs-lookup"><span data-stu-id="5e894-141">Add the **Authorize** attribute to the `Admin` method.</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample5.cs)]

<span data-ttu-id="5e894-142">AdminController.cs ファイルを開き、`AdminController` クラス全体に**承認**属性を追加します。</span><span class="sxs-lookup"><span data-stu-id="5e894-142">Open the AdminController.cs file and add the **Authorize** attribute to the entire `AdminController` class.</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample6.cs)]

> [!NOTE]
> <span data-ttu-id="5e894-143">MVC と Web API は両方とも、異なる名前空間の**承認**属性を定義します。</span><span class="sxs-lookup"><span data-stu-id="5e894-143">MVC and Web API both define **Authorize** attributes, in different namespaces.</span></span> <span data-ttu-id="5e894-144">MVC は、system.web. **authorizeattribute**を使用しますが、web API**では、system.web. web.config を**使用します。</span><span class="sxs-lookup"><span data-stu-id="5e894-144">MVC uses **System.Web.Mvc.AuthorizeAttribute**, while Web API uses **System.Web.Http.AuthorizeAttribute**.</span></span>

<span data-ttu-id="5e894-145">管理者のみが管理ページを表示できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="5e894-145">Now only administrators can view the Admin page.</span></span> <span data-ttu-id="5e894-146">また、管理コントローラーに HTTP 要求を送信する場合は、要求に認証クッキーが含まれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="5e894-146">Also, if you send an HTTP request to the Admin controller, the request must contain an authentication cookie.</span></span> <span data-ttu-id="5e894-147">それ以外の場合、サーバーは HTTP 401 (未承認) の応答を送信します。</span><span class="sxs-lookup"><span data-stu-id="5e894-147">If not, the server sends an HTTP 401 (Unauthorized) response.</span></span> <span data-ttu-id="5e894-148">GET 要求を `http://localhost:*port*/api/admin`に送信することで、これを Fiddler で確認できます。</span><span class="sxs-lookup"><span data-stu-id="5e894-148">You can see this in Fiddler by sending a GET request to `http://localhost:*port*/api/admin`.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="5e894-149">[前へ](using-web-api-with-entity-framework-part-3.md)
> [次へ](using-web-api-with-entity-framework-part-5.md)</span><span class="sxs-lookup"><span data-stu-id="5e894-149">[Previous](using-web-api-with-entity-framework-part-3.md)
[Next](using-web-api-with-entity-framework-part-5.md)</span></span>
