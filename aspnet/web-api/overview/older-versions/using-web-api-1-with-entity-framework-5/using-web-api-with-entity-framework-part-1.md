---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-1
title: 'パート 1: 概要とプロジェクトの作成 |Microsoft Docs'
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/03/2012
ms.assetid: 94421d86-68c4-4471-bf5f-82d654a17252
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-1
msc.type: authoredcontent
ms.openlocfilehash: a76a18f2bd95969358452085ef342fdca8a386e2
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600322"
---
# <a name="part-1-overview-and-creating-the-project"></a><span data-ttu-id="259d1-102">パート 1: 概要とプロジェクトの作成</span><span class="sxs-lookup"><span data-stu-id="259d1-102">Part 1: Overview and Creating the Project</span></span>

<span data-ttu-id="259d1-103">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="259d1-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="259d1-104">完成したプロジェクトのダウンロード</span><span class="sxs-lookup"><span data-stu-id="259d1-104">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

<span data-ttu-id="259d1-105">Entity Framework は、オブジェクト/リレーショナルマッピングフレームワークです。</span><span class="sxs-lookup"><span data-stu-id="259d1-105">Entity Framework is an object/relational mapping framework.</span></span> <span data-ttu-id="259d1-106">コード内のドメインオブジェクトをリレーショナルデータベースのエンティティにマップします。</span><span class="sxs-lookup"><span data-stu-id="259d1-106">It maps the domain objects in your code to entities in a relational database.</span></span> <span data-ttu-id="259d1-107">ほとんどの場合、データベース層について心配する必要はありません。これは、Entity Framework によって処理されるためです。</span><span class="sxs-lookup"><span data-stu-id="259d1-107">For the most part, you do not have to worry about the database layer, because Entity Framework takes care of it for you.</span></span> <span data-ttu-id="259d1-108">コードはオブジェクトを操作し、変更はデータベースに保存されます。</span><span class="sxs-lookup"><span data-stu-id="259d1-108">Your code manipulates the objects, and changes are persisted to a database.</span></span>

## <a name="about-the-tutorial"></a><span data-ttu-id="259d1-109">チュートリアルについて</span><span class="sxs-lookup"><span data-stu-id="259d1-109">About the Tutorial</span></span>

<span data-ttu-id="259d1-110">このチュートリアルでは、単純なストアアプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="259d1-110">In this tutorial, you will create a simple store application.</span></span> <span data-ttu-id="259d1-111">アプリケーションには主に2つの部分があります。</span><span class="sxs-lookup"><span data-stu-id="259d1-111">There are two main parts to the application.</span></span> <span data-ttu-id="259d1-112">通常のユーザーは、製品を表示して注文を作成できます。</span><span class="sxs-lookup"><span data-stu-id="259d1-112">Normal users can view products and create orders:</span></span>

![](using-web-api-with-entity-framework-part-1/_static/image1.png)

<span data-ttu-id="259d1-113">管理者は、製品の作成、削除、または編集を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="259d1-113">Administrators can create, delete, or edit products:</span></span>

![](using-web-api-with-entity-framework-part-1/_static/image2.png)

## <a name="skills-youll-learn"></a><span data-ttu-id="259d1-114">学習するスキル</span><span class="sxs-lookup"><span data-stu-id="259d1-114">Skills You'll Learn</span></span>

<span data-ttu-id="259d1-115">学習する内容は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="259d1-115">Here's what you'll learn:</span></span>

- <span data-ttu-id="259d1-116">ASP.NET Web API で Entity Framework を使用する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="259d1-116">How to use Entity Framework with ASP.NET Web API.</span></span>
- <span data-ttu-id="259d1-117">ノックアウトを使用して動的クライアント UI を作成する方法。</span><span class="sxs-lookup"><span data-stu-id="259d1-117">How to use knockout.js to create a dynamic client UI.</span></span>
- <span data-ttu-id="259d1-118">Web API でフォーム認証を使用してユーザーを認証する方法。</span><span class="sxs-lookup"><span data-stu-id="259d1-118">How to use forms authentication with Web API to authenticate users.</span></span>

<span data-ttu-id="259d1-119">このチュートリアルは自己完結していますが、まず次のチュートリアルを読むことをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="259d1-119">Although this tutorial is self-contained, you might want to read the following tutorials first:</span></span>

- [<span data-ttu-id="259d1-120">最初の ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="259d1-120">Your First ASP.NET Web API</span></span>](../../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)
- [<span data-ttu-id="259d1-121">CRUD 操作をサポートする Web API の作成</span><span class="sxs-lookup"><span data-stu-id="259d1-121">Creating a Web API that Supports CRUD Operations</span></span>](../creating-a-web-api-that-supports-crud-operations.md)

<span data-ttu-id="259d1-122">[ASP.NET MVC](../../../../mvc/index.md)に関する知識も役に立ちます。</span><span class="sxs-lookup"><span data-stu-id="259d1-122">Some knowledge of [ASP.NET MVC](../../../../mvc/index.md) is also helpful.</span></span>

## <a name="overview"></a><span data-ttu-id="259d1-123">の概要</span><span class="sxs-lookup"><span data-stu-id="259d1-123">Overview</span></span>

<span data-ttu-id="259d1-124">大まかに言えば、アプリケーションのアーキテクチャは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="259d1-124">At a high level, here is the architecture of the application:</span></span>

- <span data-ttu-id="259d1-125">ASP.NET MVC では、クライアントの HTML ページが生成されます。</span><span class="sxs-lookup"><span data-stu-id="259d1-125">ASP.NET MVC generates the HTML pages for the client.</span></span>
- <span data-ttu-id="259d1-126">ASP.NET Web API は、データ (製品と注文) に対して CRUD 操作を公開します。</span><span class="sxs-lookup"><span data-stu-id="259d1-126">ASP.NET Web API exposes CRUD operations on the data (products and orders).</span></span>
- <span data-ttu-id="259d1-127">Entity Framework は、 C# Web API によって使用されるモデルをデータベースエンティティに変換します。</span><span class="sxs-lookup"><span data-stu-id="259d1-127">Entity Framework translates the C# models used by Web API into database entities.</span></span>

![](using-web-api-with-entity-framework-part-1/_static/image3.png)

<span data-ttu-id="259d1-128">次の図は、アプリケーションのさまざまな層でドメインオブジェクトがどのように表されるかを示しています。データベース層、オブジェクトモデル、最後にワイヤ形式を使用します。これは、HTTP 経由でクライアントにデータを送信するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="259d1-128">The following diagram shows how the domain objects are represented at various layers of the application: The database layer, the object model, and finally the wire format, which is used to transmit data to the client via HTTP.</span></span>

![](using-web-api-with-entity-framework-part-1/_static/image4.png)

## <a name="create-the-visual-studio-project"></a><span data-ttu-id="259d1-129">Visual Studio プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="259d1-129">Create the Visual Studio Project</span></span>

<span data-ttu-id="259d1-130">チュートリアルプロジェクトは、Visual Web Developer Express または Visual Studio の完全バージョンのいずれかを使用して作成できます。</span><span class="sxs-lookup"><span data-stu-id="259d1-130">You can create the tutorial project using either Visual Web Developer Express or the full version of Visual Studio.</span></span>

<span data-ttu-id="259d1-131">**スタート**ページで、 **[新しいプロジェクト]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="259d1-131">From the **Start** page, click **New Project**.</span></span>

<span data-ttu-id="259d1-132">**[テンプレート]** ペインで、 **[インストールされたテンプレート]** を選択し、  **C#ビジュアル**ノードを展開します。</span><span class="sxs-lookup"><span data-stu-id="259d1-132">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="259d1-133">**[ビジュアルC# ]** で **[Web]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="259d1-133">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="259d1-134">プロジェクトテンプレートの一覧で、 **[ASP.NET MVC 4 Web アプリケーション]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="259d1-134">In the list of project templates, select **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="259d1-135">プロジェクトに "ProductStore" という名前を指定し、[ **OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="259d1-135">Name the project "ProductStore" and click **OK**.</span></span>

![](using-web-api-with-entity-framework-part-1/_static/image5.png)

<span data-ttu-id="259d1-136">**[New ASP.NET MVC 4 プロジェクト]** ダイアログボックスで、 **[インターネットアプリケーション]** を選択し、 **[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="259d1-136">In the **New ASP.NET MVC 4 Project** dialog, select **Internet Application** and click **OK**.</span></span>

![](using-web-api-with-entity-framework-part-1/_static/image6.png)

<span data-ttu-id="259d1-137">"インターネットアプリケーション" テンプレートは、フォーム認証をサポートする ASP.NET MVC アプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="259d1-137">The "Internet Application" template creates an ASP.NET MVC application that supports forms authentication.</span></span> <span data-ttu-id="259d1-138">ここでアプリケーションを実行すると、既にいくつかの機能があります。</span><span class="sxs-lookup"><span data-stu-id="259d1-138">If you run the application now, it already has some features:</span></span>

- <span data-ttu-id="259d1-139">新しいユーザーは、右上隅にある [登録] リンクをクリックすることで登録できます。</span><span class="sxs-lookup"><span data-stu-id="259d1-139">New users can register by clicking the "Register" link in the upper right corner.</span></span>
- <span data-ttu-id="259d1-140">登録されたユーザーは、[ログイン] リンクをクリックしてログインできます。</span><span class="sxs-lookup"><span data-stu-id="259d1-140">Registered users can log in by clicking the "Log in" link.</span></span>

<span data-ttu-id="259d1-141">メンバーシップ情報は、自動的に作成されるデータベースに保持されます。</span><span class="sxs-lookup"><span data-stu-id="259d1-141">Membership information is persisted in a database that gets created automatically.</span></span> <span data-ttu-id="259d1-142">ASP.NET MVC でのフォーム認証の詳細については、「[チュートリアル: ASP.NET mvc でのフォーム認証の使用](https://msdn.microsoft.com/library/ff398049(VS.98).aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="259d1-142">For more information about forms authentication in ASP.NET MVC, see [Walkthrough: Using Forms Authentication in ASP.NET MVC](https://msdn.microsoft.com/library/ff398049(VS.98).aspx).</span></span>

## <a name="update-the-css-file"></a><span data-ttu-id="259d1-143">CSS ファイルを更新する</span><span class="sxs-lookup"><span data-stu-id="259d1-143">Update the CSS File</span></span>

<span data-ttu-id="259d1-144">この手順は表面的なものですが、前のスクリーンショットのようにページがレンダリングされるようになります。</span><span class="sxs-lookup"><span data-stu-id="259d1-144">This step is cosmetic, but it will make the pages render like the earlier screen shots.</span></span>

<span data-ttu-id="259d1-145">ソリューションエクスプローラーで、[コンテンツ] フォルダーを展開し、[サイト .css] という名前のファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="259d1-145">In Solution Explorer, expand the Content folder and open the file named Site.css.</span></span> <span data-ttu-id="259d1-146">次の CSS スタイルを追加します。</span><span class="sxs-lookup"><span data-stu-id="259d1-146">Add the following CSS styles:</span></span>

[!code-css[Main](using-web-api-with-entity-framework-part-1/samples/sample1.css)]

> [!div class="step-by-step"]
> [<span data-ttu-id="259d1-147">次へ</span><span class="sxs-lookup"><span data-stu-id="259d1-147">Next</span></span>](using-web-api-with-entity-framework-part-2.md)
