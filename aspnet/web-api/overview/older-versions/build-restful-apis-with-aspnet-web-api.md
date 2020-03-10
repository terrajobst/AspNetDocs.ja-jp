---
uid: web-api/overview/older-versions/build-restful-apis-with-aspnet-web-api
title: ASP.NET Web API-ASP.NET 4.x を使用して RESTful Api をビルドする
author: rick-anderson
description: 'ハンズオンラボ: ASP.NET 4.x の Web API を使用して、contact manager アプリケーションの簡単な REST API を作成します。'
ms.author: riande
ms.date: 02/18/2013
ms.custom: seoapril2019
ms.assetid: 87daa99f-3810-407e-b969-dd28a192959d
msc.legacyurl: /web-api/overview/older-versions/build-restful-apis-with-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 35b115d6b4f84084e78e429bbb4842670e57bba4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78504268"
---
# <a name="build-restful-apis-with-aspnet-web-api"></a><span data-ttu-id="16755-103">ASP.NET Web API で RESTful Api をビルドする</span><span class="sxs-lookup"><span data-stu-id="16755-103">Build RESTful APIs with ASP.NET Web API</span></span>

<span data-ttu-id="16755-104">[Web キャンプチーム](https://twitter.com/webcamps)別</span><span class="sxs-lookup"><span data-stu-id="16755-104">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

> <span data-ttu-id="16755-105">ハンズオンラボ: ASP.NET 4.x の Web API を使用して、contact manager アプリケーションの簡単な REST API を作成します。</span><span class="sxs-lookup"><span data-stu-id="16755-105">Hands on lab: Use Web API in ASP.NET 4.x to build a simple REST API for a contact manager application.</span></span> <span data-ttu-id="16755-106">また、API を使用するクライアントを構築します。</span><span class="sxs-lookup"><span data-stu-id="16755-106">You will also build a client to consume the API.</span></span>

<span data-ttu-id="16755-107">近年、HTTP が HTML ページを提供するだけではないことが明らかになっています。</span><span class="sxs-lookup"><span data-stu-id="16755-107">In recent years, it has become clear that HTTP is not just for serving up HTML pages.</span></span> <span data-ttu-id="16755-108">また、いくつかの動詞 (GET、POST など) に加え、 *uri*や*ヘッダー*などのいくつかの簡単な概念を使用して、Web api を構築するための強力なプラットフォームでもあります。</span><span class="sxs-lookup"><span data-stu-id="16755-108">It is also a powerful platform for building Web APIs, using a handful of verbs (GET, POST, and so forth) plus a few simple concepts such as *URIs* and *headers*.</span></span> <span data-ttu-id="16755-109">ASP.NET Web API は、HTTP プログラミングを簡素化するコンポーネントのセットです。</span><span class="sxs-lookup"><span data-stu-id="16755-109">ASP.NET Web API is a set of components that simplify HTTP programming.</span></span> <span data-ttu-id="16755-110">ASP.NET MVC ランタイムの上に構築されているため、Web API は HTTP の低レベルトランスポートの詳細を自動的に処理します。</span><span class="sxs-lookup"><span data-stu-id="16755-110">Because it is built on top of the ASP.NET MVC runtime, Web API automatically handles the low-level transport details of HTTP.</span></span> <span data-ttu-id="16755-111">同時に、Web API は通常、HTTP プログラミングモデルを公開します。</span><span class="sxs-lookup"><span data-stu-id="16755-111">At the same time, Web API naturally exposes the HTTP programming model.</span></span> <span data-ttu-id="16755-112">実際、Web API の目的の1つは、HTTP の事実を抽象化し*ないこと*です。</span><span class="sxs-lookup"><span data-stu-id="16755-112">In fact, one goal of Web API is to *not* abstract away the reality of HTTP.</span></span> <span data-ttu-id="16755-113">その結果、Web API は柔軟性が高く、簡単に拡張することができます。</span><span class="sxs-lookup"><span data-stu-id="16755-113">As a result, Web API is both flexible and easy to extend.</span></span>  <span data-ttu-id="16755-114">REST アーキテクチャスタイルは、http を利用するための効果的な方法であることが実証されていますが、HTTP に対する唯一の有効なアプローチではありません。</span><span class="sxs-lookup"><span data-stu-id="16755-114">The REST architectural style has proven to be an effective way to leverage HTTP - although it is certainly not the only valid approach to HTTP.</span></span> <span data-ttu-id="16755-115">連絡先マネージャーは、連絡先の一覧表示、追加、および削除のための RESTful を公開します。</span><span class="sxs-lookup"><span data-stu-id="16755-115">The contact manager will expose the RESTful for listing, adding and removing contacts, among others.</span></span> 

<span data-ttu-id="16755-116">このラボでは、HTTP、REST、および HTML、JavaScript、jQuery に関する基本的な知識があることを前提としています。</span><span class="sxs-lookup"><span data-stu-id="16755-116">This lab requires a basic understanding of HTTP, REST, and assumes you have a basic working knowledge of HTML, JavaScript, and jQuery.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="16755-117">ASP.NET Web サイトには、 [https://asp.net/web-api](https://asp.net/web-api)の ASP.NET Web API フレームワーク専用の領域があります。</span><span class="sxs-lookup"><span data-stu-id="16755-117">The ASP.NET Web site has an area dedicated to the ASP.NET Web API framework at [https://asp.net/web-api](https://asp.net/web-api).</span></span> <span data-ttu-id="16755-118">このサイトでは、Web API に関する最新の情報、サンプル、ニュースが引き続き提供されます。そのため、事実上あらゆるデバイスまたは開発フレームワークで使用できるカスタム Web Api の作成について詳しく掘り下げたい場合は、頻繁に確認してください。</span><span class="sxs-lookup"><span data-stu-id="16755-118">This site will continue to provide late-breaking information, samples, and news related to Web API, so check it frequently if you'd like to delve deeper into the art of creating custom Web APIs available to virtually any device or development framework.</span></span>
> > 
> > <span data-ttu-id="16755-119">ASP.NET Web API は、ASP.NET MVC 4 に似ていますが、サービス層をコントローラーから分離することによって非常に柔軟で、利用可能ないくつかの依存関係挿入フレームワークを非常に簡単に使用できます。</span><span class="sxs-lookup"><span data-stu-id="16755-119">ASP.NET Web API, similar to ASP.NET MVC 4, has great flexibility in terms of separating the service layer from the controllers allowing you to use several of the available Dependency Injection frameworks fairly easy.</span></span> <span data-ttu-id="16755-120">MSDN には、[ここ](https://code.msdn.microsoft.com/ASPNET-Web-API-JavaScript-d0d64dd7)からダウンロードできる ASP.NET Web API プロジェクトでの依存関係の挿入に ninject を使用する方法を示す優れたサンプルが用意されています。</span><span class="sxs-lookup"><span data-stu-id="16755-120">There is a good sample in MSDN that shows how to use Ninject for dependency injection in an ASP.NET Web API project that you can download it from [here](https://code.msdn.microsoft.com/ASPNET-Web-API-JavaScript-d0d64dd7).</span></span>
> 
> 
> <span data-ttu-id="16755-121">すべてのサンプルコードとスニペットは、 [https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409)で入手できる Web キャンプトレーニングキットに含まれています。</span><span class="sxs-lookup"><span data-stu-id="16755-121">All sample code and snippets are included in the Web Camps Training Kit, available at [https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409).</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="16755-122">目標</span><span class="sxs-lookup"><span data-stu-id="16755-122">Objectives</span></span>

<span data-ttu-id="16755-123">このハンズオンラボでは、次の方法を学習します。</span><span class="sxs-lookup"><span data-stu-id="16755-123">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="16755-124">RESTful Web API を実装する</span><span class="sxs-lookup"><span data-stu-id="16755-124">Implement a RESTful Web API</span></span>
- <span data-ttu-id="16755-125">HTML クライアントから API を呼び出す</span><span class="sxs-lookup"><span data-stu-id="16755-125">Call the API from an HTML client</span></span>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="16755-126">前提条件</span><span class="sxs-lookup"><span data-stu-id="16755-126">Prerequisites</span></span>

<span data-ttu-id="16755-127">このハンズオンラボを完了するには、次のものが必要です。</span><span class="sxs-lookup"><span data-stu-id="16755-127">The following is required to complete this hands-on lab:</span></span>

- <span data-ttu-id="16755-128">Web またはそれ以降[の2012を Microsoft Visual Studio Express](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web)します (付録 B をインストールする手順については、 [「付録 B](#AppendixB) 」を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="16755-128">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix B](#AppendixB) for instructions on how to install it).</span></span>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="16755-129">セットアップ</span><span class="sxs-lookup"><span data-stu-id="16755-129">Setup</span></span>

<span data-ttu-id="16755-130">**コードスニペットのインストール**</span><span class="sxs-lookup"><span data-stu-id="16755-130">**Installing Code Snippets**</span></span>

<span data-ttu-id="16755-131">便宜上、このラボで管理するコードの多くは、Visual Studio のコードスニペットとして提供されています。</span><span class="sxs-lookup"><span data-stu-id="16755-131">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="16755-132">コードスニペットをインストールするには、 **.\Source\Setup\CodeSnippets.vsi**ファイルを実行します。</span><span class="sxs-lookup"><span data-stu-id="16755-132">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="16755-133">Visual Studio Code のスニペットを使い慣れておらず、その使用方法を学習する場合は、このドキュメントの付録「[付録 a: コードスニペット](#AppendixA)&quot;の使用」 &quot;参照してください。</span><span class="sxs-lookup"><span data-stu-id="16755-133">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix A: Using Code Snippets](#AppendixA)&quot;.</span></span>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="16755-134">手順</span><span class="sxs-lookup"><span data-stu-id="16755-134">Exercises</span></span>

<span data-ttu-id="16755-135">このハンズオンラボには、次の演習が含まれています。</span><span class="sxs-lookup"><span data-stu-id="16755-135">This hands-on lab includes the following exercise:</span></span>

1. [<span data-ttu-id="16755-136">演習 1: 読み取り専用の Web API を作成する</span><span class="sxs-lookup"><span data-stu-id="16755-136">Exercise 1: Create a Read-Only Web API</span></span>](#Exercise1)
2. [<span data-ttu-id="16755-137">演習 2: 読み取り/書き込み Web API を作成する</span><span class="sxs-lookup"><span data-stu-id="16755-137">Exercise 2: Create a Read/Write Web API</span></span>](#Exercise2)
3. [<span data-ttu-id="16755-138">演習 3: HTML クライアントから Web API を使用する</span><span class="sxs-lookup"><span data-stu-id="16755-138">Exercise 3: Consume the Web API from an HTML Client</span></span>](#Exercise3)

> [!NOTE]
> <span data-ttu-id="16755-139">各演習には、演習を完了した後に取得する必要があるソリューションを含む**終了**フォルダーが付属しています。</span><span class="sxs-lookup"><span data-stu-id="16755-139">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="16755-140">演習を通じて追加のヘルプが必要な場合は、このソリューションをガイドとして使用できます。</span><span class="sxs-lookup"><span data-stu-id="16755-140">You can use this solution as a guide if you need additional help working through the exercises.</span></span>

<span data-ttu-id="16755-141">このラボの推定所要時間: **60 分**。</span><span class="sxs-lookup"><span data-stu-id="16755-141">Estimated time to complete this lab: **60 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Create_a_Read-Only_Web_API"></a>
### <a name="exercise-1-create-a-read-only-web-api"></a><span data-ttu-id="16755-142">演習 1: 読み取り専用の Web API を作成する</span><span class="sxs-lookup"><span data-stu-id="16755-142">Exercise 1: Create a Read-Only Web API</span></span>

<span data-ttu-id="16755-143">この演習では、連絡先マネージャーに読み取り専用の GET メソッドを実装します。</span><span class="sxs-lookup"><span data-stu-id="16755-143">In this exercise, you will implement the read-only GET methods for the contact manager.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_the_API_Project"></a>
#### <a name="task-1---creating-the-api-project"></a><span data-ttu-id="16755-144">タスク 1-API プロジェクトの作成</span><span class="sxs-lookup"><span data-stu-id="16755-144">Task 1 - Creating the API Project</span></span>

<span data-ttu-id="16755-145">このタスクでは、新しい ASP.NET web プロジェクトテンプレートを使用して、Web API web アプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="16755-145">In this task, you will use the new ASP.NET web project templates to create a Web API web application.</span></span>

1. <span data-ttu-id="16755-146">**Visual Studio 2012 Express For Web**を実行し**ます。これ**を行うには、 **[スタート]** に移り、 **VS Express for Web**入力して、enter キーを押します。</span><span class="sxs-lookup"><span data-stu-id="16755-146">Run **Visual Studio 2012 Express for Web**, to do this go to **Start** and type **VS Express for Web** then press **Enter**.</span></span>
2. <span data-ttu-id="16755-147">**[ファイル]** メニューの **[新しいプロジェクト]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="16755-147">From the **File** menu, select **New Project**.</span></span> <span data-ttu-id="16755-148">Visual | を選択します。  **C#** [プロジェクトの種類] ツリービューの [web プロジェクトの種類] をクリックし、 **ASP.NET MVC 4 web アプリケーション**プロジェクトの種類を選択します。</span><span class="sxs-lookup"><span data-stu-id="16755-148">Select the **Visual C# | Web** project type from the project type tree view, then select the **ASP.NET MVC 4 Web Application** project type.</span></span> <span data-ttu-id="16755-149">プロジェクトの**名前**を*contactmanager*に設定し、**ソリューション名**を*開始*して、[ **OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="16755-149">Set the project's **Name** to *ContactManager* and the **Solution name** to *Begin*, then click **OK**.</span></span>

    <span data-ttu-id="16755-150">![新しい ASP.NET MVC 4.0 Web アプリケーションプロジェクトの作成](build-restful-apis-with-aspnet-web-api/_static/image1.png "新しい ASP.NET MVC 4.0 Web アプリケーションプロジェクトの作成")</span><span class="sxs-lookup"><span data-stu-id="16755-150">![Creating a new ASP.NET MVC 4.0 Web Application Project](build-restful-apis-with-aspnet-web-api/_static/image1.png "Creating a new ASP.NET MVC 4.0 Web Application Project")</span></span>

    <span data-ttu-id="16755-151">*新しい ASP.NET MVC 4.0 Web アプリケーションプロジェクトの作成*</span><span class="sxs-lookup"><span data-stu-id="16755-151">*Creating a new ASP.NET MVC 4.0 Web Application Project*</span></span>
3. <span data-ttu-id="16755-152">ASP.NET MVC 4 プロジェクトの種類 ダイアログで、 **WEB API** プロジェクトの種類を選択します。</span><span class="sxs-lookup"><span data-stu-id="16755-152">In the ASP.NET MVC 4 project type dialog, select the **Web API** project type.</span></span> <span data-ttu-id="16755-153">**[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="16755-153">Click **OK**.</span></span>

    <span data-ttu-id="16755-154">![Web API プロジェクトの種類の指定](build-restful-apis-with-aspnet-web-api/_static/image2.png "Web API プロジェクトの種類の指定")</span><span class="sxs-lookup"><span data-stu-id="16755-154">![Specifying the Web API project type](build-restful-apis-with-aspnet-web-api/_static/image2.png "Specifying the Web API project type")</span></span>

    <span data-ttu-id="16755-155">*Web API プロジェクトの種類の指定*</span><span class="sxs-lookup"><span data-stu-id="16755-155">*Specifying the Web API project type*</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Creating_the_Contact_Manager_API_Controllers"></a>
#### <a name="task-2---creating-the-contact-manager-api-controllers"></a><span data-ttu-id="16755-156">タスク 2-Contact Manager API コントローラーの作成</span><span class="sxs-lookup"><span data-stu-id="16755-156">Task 2 - Creating the Contact Manager API Controllers</span></span>

<span data-ttu-id="16755-157">このタスクでは、API メソッドが存在するコントローラークラスを作成します。</span><span class="sxs-lookup"><span data-stu-id="16755-157">In this task, you will create the controller classes in which API methods will reside.</span></span>

1. <span data-ttu-id="16755-158">**Controllers**フォルダー内の**ValuesController.cs**という名前のファイルをプロジェクトから削除します。</span><span class="sxs-lookup"><span data-stu-id="16755-158">Delete the file named **ValuesController.cs** within **Controllers** folder from the project.</span></span>
2. <span data-ttu-id="16755-159">プロジェクト内の**Controllers**フォルダーを右クリックし、[追加] を選択します。コンテキストメニューの [コントローラー]。</span><span class="sxs-lookup"><span data-stu-id="16755-159">Right-click the **Controllers** folder in the project and select **Add | Controller** from the context menu.</span></span>

    <span data-ttu-id="16755-160">![プロジェクトへの新しいコントローラーの追加](build-restful-apis-with-aspnet-web-api/_static/image3.png "プロジェクトへの新しいコントローラーの追加")</span><span class="sxs-lookup"><span data-stu-id="16755-160">![Adding a new controller to the project](build-restful-apis-with-aspnet-web-api/_static/image3.png "Adding a new controller to the project")</span></span>

    <span data-ttu-id="16755-161">*プロジェクトへの新しいコントローラーの追加*</span><span class="sxs-lookup"><span data-stu-id="16755-161">*Adding a new controller to the project*</span></span>
3. <span data-ttu-id="16755-162">表示される **[コントローラーの追加]** ダイアログボックスで、テンプレート メニューの **[空の API コントローラー]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="16755-162">In the **Add Controller** dialog that appears, select **Empty API Controller** from the Template menu.</span></span> <span data-ttu-id="16755-163">コントローラークラスに**contactcontroller**という名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="16755-163">Name the controller class **ContactController**.</span></span> <span data-ttu-id="16755-164">次に、[追加] をクリックし**ます。**</span><span class="sxs-lookup"><span data-stu-id="16755-164">Then, click **Add.**</span></span>

    <span data-ttu-id="16755-165">![[コントローラーの追加] ダイアログボックスを使用して新しい Web API コントローラーを作成する](build-restful-apis-with-aspnet-web-api/_static/image4.png "[コントローラーの追加] ダイアログボックスを使用して新しい Web API コントローラーを作成する")</span><span class="sxs-lookup"><span data-stu-id="16755-165">![Using the Add Controller dialog to create a new Web API controller](build-restful-apis-with-aspnet-web-api/_static/image4.png "Using the Add Controller dialog to create a new Web API controller")</span></span>

    <span data-ttu-id="16755-166">*[コントローラーの追加] ダイアログボックスを使用して新しい Web API コントローラーを作成する*</span><span class="sxs-lookup"><span data-stu-id="16755-166">*Using the Add Controller dialog to create a new Web API controller*</span></span>
4. <span data-ttu-id="16755-167">次のコードを**Contactcontroller**に追加します。</span><span class="sxs-lookup"><span data-stu-id="16755-167">Add the following code to the **ContactController**.</span></span>

    <span data-ttu-id="16755-168">(コードスニペット- *WEB Api Ex01-GET Api メソッド*)</span><span class="sxs-lookup"><span data-stu-id="16755-168">(Code Snippet - *Web API Lab - Ex01 - Get API Method*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample1.cs)]
5. <span data-ttu-id="16755-169">**F5** キーを押してアプリケーションをデバッグします。</span><span class="sxs-lookup"><span data-stu-id="16755-169">Press **F5** to debug the application.</span></span> <span data-ttu-id="16755-170">Web API プロジェクトの既定のホームページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="16755-170">The default home page for a Web API project should appear.</span></span>

    <span data-ttu-id="16755-171">![ASP.NET Web API アプリケーションの既定のホームページ](build-restful-apis-with-aspnet-web-api/_static/image5.png "ASP.NET Web API アプリケーションの既定のホームページ")</span><span class="sxs-lookup"><span data-stu-id="16755-171">![The default home page of an ASP.NET Web API application](build-restful-apis-with-aspnet-web-api/_static/image5.png "The default home page of an ASP.NET Web API application")</span></span>

    <span data-ttu-id="16755-172">*ASP.NET Web API アプリケーションの既定のホームページ*</span><span class="sxs-lookup"><span data-stu-id="16755-172">*The default home page of an ASP.NET Web API application*</span></span>
6. <span data-ttu-id="16755-173">Internet Explorer ウィンドウで、 **F12**キーを押して **[開発者ツール]** ウィンドウを開きます。</span><span class="sxs-lookup"><span data-stu-id="16755-173">In the Internet Explorer window, press the **F12** key to open the **Developer Tools** window.</span></span> <span data-ttu-id="16755-174">**[ネットワーク]** タブをクリックし、 **[キャプチャの開始]** ボタンをクリックして、ウィンドウへのネットワークトラフィックのキャプチャを開始します。</span><span class="sxs-lookup"><span data-stu-id="16755-174">Click the **Network** tab, and then click the **Start Capturing** button to begin capturing network traffic into the window.</span></span>

    <span data-ttu-id="16755-175">![[ネットワーク] タブを開いてネットワークキャプチャを開始する](build-restful-apis-with-aspnet-web-api/_static/image6.png "[ネットワーク] タブを開いてネットワークキャプチャを開始する")</span><span class="sxs-lookup"><span data-stu-id="16755-175">![Opening the network tab and initiating network capture](build-restful-apis-with-aspnet-web-api/_static/image6.png "Opening the network tab and initiating network capture")</span></span>

    <span data-ttu-id="16755-176">*[ネットワーク] タブを開いてネットワークキャプチャを開始する*</span><span class="sxs-lookup"><span data-stu-id="16755-176">*Opening the network tab and initiating network capture*</span></span>
7. <span data-ttu-id="16755-177">ブラウザーのアドレスバーに **/api/contact**という URL を追加し、enter キーを押します。</span><span class="sxs-lookup"><span data-stu-id="16755-177">Append the URL in the browser's address bar with **/api/contact** and press enter.</span></span> <span data-ttu-id="16755-178">転送の詳細は、[ネットワークキャプチャ] ウィンドウに表示されます。</span><span class="sxs-lookup"><span data-stu-id="16755-178">The transmission details will appear in the network capture window.</span></span> <span data-ttu-id="16755-179">応答の MIME の種類は**application/json**であることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="16755-179">Note that the response's MIME type is **application/json**.</span></span> <span data-ttu-id="16755-180">これは、既定の出力形式が JSON であることを示しています。</span><span class="sxs-lookup"><span data-stu-id="16755-180">This demonstrates how the default output format is JSON.</span></span>

    <span data-ttu-id="16755-181">![ネットワークビューでの Web API 要求の出力の表示](build-restful-apis-with-aspnet-web-api/_static/image7.png "ネットワークビューでの Web API 要求の出力の表示")</span><span class="sxs-lookup"><span data-stu-id="16755-181">![Viewing the output of the Web API request in the Network view](build-restful-apis-with-aspnet-web-api/_static/image7.png "Viewing the output of the Web API request in the Network view")</span></span>

    <span data-ttu-id="16755-182">*ネットワークビューでの Web API 要求の出力の表示*</span><span class="sxs-lookup"><span data-stu-id="16755-182">*Viewing the output of the Web API request in the Network view*</span></span>

    > [!NOTE]
    > <span data-ttu-id="16755-183">この時点での Internet Explorer 10 の既定の動作では、ユーザーが Web API 呼び出しによって生成されたストリームを保存するか開くかを確認します。</span><span class="sxs-lookup"><span data-stu-id="16755-183">Internet Explorer 10's default behavior at this point will be to ask if the user would like to save or open the stream resulting from the Web API call.</span></span> <span data-ttu-id="16755-184">出力は、Web API URL 呼び出しの JSON 結果を含むテキストファイルになります。</span><span class="sxs-lookup"><span data-stu-id="16755-184">The output will be a text file containing the JSON result of the Web API URL call.</span></span> <span data-ttu-id="16755-185">開発者ツールウィンドウで応答の内容を見ることができるように、ダイアログをキャンセルしないでください。</span><span class="sxs-lookup"><span data-stu-id="16755-185">Do not cancel the dialog in order to be able to watch the response's content through Developers Tool window.</span></span>
8. <span data-ttu-id="16755-186">**[詳細表示に進む]** ボタンをクリックして、この API 呼び出しの応答に関する詳細を表示します。</span><span class="sxs-lookup"><span data-stu-id="16755-186">Click the **Go to detailed view** button to see more details about the response of this API call.</span></span>

    <span data-ttu-id="16755-187">![詳細ビューに切り替え](build-restful-apis-with-aspnet-web-api/_static/image8.png "詳細ビューに切り替え")</span><span class="sxs-lookup"><span data-stu-id="16755-187">![Switch to Detailed View](build-restful-apis-with-aspnet-web-api/_static/image8.png "Switch to Details View")</span></span>

    <span data-ttu-id="16755-188">*詳細ビューに切り替え*</span><span class="sxs-lookup"><span data-stu-id="16755-188">*Switch to Detailed View*</span></span>
9. <span data-ttu-id="16755-189">**[応答本文]** タブをクリックして、実際の JSON 応答テキストを表示します。</span><span class="sxs-lookup"><span data-stu-id="16755-189">Click the **Response body** tab to view the actual JSON response text.</span></span>

    <span data-ttu-id="16755-190">![ネットワークモニターでの JSON 出力テキストの表示](build-restful-apis-with-aspnet-web-api/_static/image9.png "ネットワークモニターでの JSON 出力テキストの表示")</span><span class="sxs-lookup"><span data-stu-id="16755-190">![Viewing the JSON output text in the network monitor](build-restful-apis-with-aspnet-web-api/_static/image9.png "Viewing the JSON output text in the network monitor")</span></span>

    <span data-ttu-id="16755-191">*ネットワークモニターでの JSON 出力テキストの表示*</span><span class="sxs-lookup"><span data-stu-id="16755-191">*Viewing the JSON output text in the network monitor*</span></span>

<a id="Ex1Task3"></a>

<a id="Task_3_-_Creating_the_Contact_Models_and_Augment_the_Contact_Controller"></a>
#### <a name="task-3---creating-the-contact-models-and-augment-the-contact-controller"></a><span data-ttu-id="16755-192">タスク 3-連絡先モデルの作成と連絡先コントローラーの拡張</span><span class="sxs-lookup"><span data-stu-id="16755-192">Task 3 - Creating the Contact Models and Augment the Contact Controller</span></span>

<span data-ttu-id="16755-193">このタスクでは、API メソッドが存在するコントローラークラスを作成します。</span><span class="sxs-lookup"><span data-stu-id="16755-193">In this task, you will create the controller classes in which API methods will reside.</span></span>

1. <span data-ttu-id="16755-194">**モデル** フォルダーを右クリックし、追加 を選択します。 **クラス...** コンテキストメニューから。</span><span class="sxs-lookup"><span data-stu-id="16755-194">Right-click the **Models** folder and select **Add | Class...** from the context menu.</span></span>

    <span data-ttu-id="16755-195">![Web アプリケーションへの新しいモデルの追加](build-restful-apis-with-aspnet-web-api/_static/image10.png "Web アプリケーションへの新しいモデルの追加")</span><span class="sxs-lookup"><span data-stu-id="16755-195">![Adding a new model to the web application](build-restful-apis-with-aspnet-web-api/_static/image10.png "Adding a new model to the web application")</span></span>

    <span data-ttu-id="16755-196">*Web アプリケーションへの新しいモデルの追加*</span><span class="sxs-lookup"><span data-stu-id="16755-196">*Adding a new model to the web application*</span></span>
2. <span data-ttu-id="16755-197">**[新しい項目の追加]** ダイアログで、新しいファイルに**Contact.cs**という名前を指定し、[追加] をクリックし**ます。**</span><span class="sxs-lookup"><span data-stu-id="16755-197">In the **Add New Item** dialog, name the new file **Contact.cs** and click **Add.**</span></span>

    <span data-ttu-id="16755-198">![新しい Contact クラスファイルを作成しています](build-restful-apis-with-aspnet-web-api/_static/image11.png "新しい Contact クラスファイルを作成しています")</span><span class="sxs-lookup"><span data-stu-id="16755-198">![Creating the new Contact class file](build-restful-apis-with-aspnet-web-api/_static/image11.png "Creating the new Contact class file")</span></span>

    <span data-ttu-id="16755-199">*新しい Contact クラスファイルを作成しています*</span><span class="sxs-lookup"><span data-stu-id="16755-199">*Creating the new Contact class file*</span></span>
3. <span data-ttu-id="16755-200">次の強調表示されたコードを**Contact**クラスに追加します。</span><span class="sxs-lookup"><span data-stu-id="16755-200">Add the following highlighted code to the **Contact** class.</span></span>

    <span data-ttu-id="16755-201">(コードスニペット- *WEB API Ex01-Contact クラス*)</span><span class="sxs-lookup"><span data-stu-id="16755-201">(Code Snippet - *Web API Lab - Ex01 - Contact Class*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample2.cs)]
4. <span data-ttu-id="16755-202">**Contactcontroller**クラスで、 **Get**メソッドの [メソッド定義内の**文字列**] を選択し、「 *Contact*」と入力します。</span><span class="sxs-lookup"><span data-stu-id="16755-202">In the **ContactController** class, select the word **string** in method definition of the **Get** method, and type the word *Contact*.</span></span> <span data-ttu-id="16755-203">単語がに入力されると、" **Contact**" という単語の先頭にインジケーターが表示されます。</span><span class="sxs-lookup"><span data-stu-id="16755-203">Once the word is typed in, an indicator will appear at the beginning of the word **Contact**.</span></span> <span data-ttu-id="16755-204">**Ctrl**キーを押したままピリオド (.) キーを押すか、マウスを使用してアイコンをクリックしてコードエディターの [アシスタンス] ダイアログを開き、モデルの名前空間の**using**ディレクティブを自動的に入力します。</span><span class="sxs-lookup"><span data-stu-id="16755-204">Either hold down the **Ctrl** key and press the period (.) key or click the icon using your mouse to open up the assistance dialog in the code editor, to automatically fill in the **using** directive for the Models namespace.</span></span>

    ![名前空間宣言における Intellisense アシスタントの使用](build-restful-apis-with-aspnet-web-api/_static/image12.png)

    <span data-ttu-id="16755-206">*名前空間宣言における Intellisense アシスタントの使用*</span><span class="sxs-lookup"><span data-stu-id="16755-206">*Using Intellisense assistance for namespace declarations*</span></span>
5. <span data-ttu-id="16755-207">Contact モデルのインスタンスの配列を返すように、 **Get**メソッドのコードを変更します。</span><span class="sxs-lookup"><span data-stu-id="16755-207">Modify the code for the **Get** method so that it returns an array of Contact model instances.</span></span>

    <span data-ttu-id="16755-208">(コードスニペット- *WEB API Lab-Ex01-連絡先の一覧を返す*)</span><span class="sxs-lookup"><span data-stu-id="16755-208">(Code Snippet - *Web API Lab - Ex01 - Returning a list of contacts*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample3.cs)]
6. <span data-ttu-id="16755-209">**F5**キーを押して、ブラウザーで web アプリケーションをデバッグします。</span><span class="sxs-lookup"><span data-stu-id="16755-209">Press **F5** to debug the web application in the browser.</span></span> <span data-ttu-id="16755-210">API の応答出力に加えられた変更を表示するには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="16755-210">To view the changes made to the response output of the API, perform the following steps.</span></span>

   1. <span data-ttu-id="16755-211">ブラウザーが開いたら、開発者ツールがまだ開いていない場合は**F12**キーを押します。</span><span class="sxs-lookup"><span data-stu-id="16755-211">Once the browser opens, press **F12** if the developer tools are not open yet.</span></span>
   2. <span data-ttu-id="16755-212">**[ネットワーク]** タブをクリックします。</span><span class="sxs-lookup"><span data-stu-id="16755-212">Click the **Network** tab.</span></span>
   3. <span data-ttu-id="16755-213">**[キャプチャの開始]** ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="16755-213">Press the **Start Capturing** button.</span></span>
   4. <span data-ttu-id="16755-214">URL サフィックス **/api/contact**をアドレスバーの url に追加し、 **enter**キーを押します。</span><span class="sxs-lookup"><span data-stu-id="16755-214">Add the URL suffix **/api/contact** to the URL in the address bar and press the **Enter** key.</span></span>
   5. <span data-ttu-id="16755-215">**[詳細表示に進む]** ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="16755-215">Press the **Go to detailed view** button.</span></span>
   6. <span data-ttu-id="16755-216">**[応答本文]** タブを選択します。シリアル化されたフォームを表す JSON 文字列が、連絡先インスタンスの配列として表示されます。</span><span class="sxs-lookup"><span data-stu-id="16755-216">Select the **Response body** tab. You should see a JSON string representing the serialized form of an array of Contact instances.</span></span>

      <span data-ttu-id="16755-217">![複雑な Web API メソッド呼び出しの JSON でシリアル化された出力](build-restful-apis-with-aspnet-web-api/_static/image13.png "複雑な Web API メソッド呼び出しの JSON でシリアル化された出力")</span><span class="sxs-lookup"><span data-stu-id="16755-217">![JSON serialized output of a complex Web API method call](build-restful-apis-with-aspnet-web-api/_static/image13.png "JSON serialized output of a complex Web API method call")</span></span>

      <span data-ttu-id="16755-218">*複雑な Web API メソッド呼び出しの JSON でシリアル化された出力*</span><span class="sxs-lookup"><span data-stu-id="16755-218">*JSON serialized output of a complex Web API method call*</span></span>

<a id="Ex1Task4"></a>

<a id="Task_4_-_Extracting_Functionality_into_a_Service_Layer"></a>
#### <a name="task-4---extracting-functionality-into-a-service-layer"></a><span data-ttu-id="16755-219">タスク 4-サービスレイヤーへの機能の抽出</span><span class="sxs-lookup"><span data-stu-id="16755-219">Task 4 - Extracting Functionality into a Service Layer</span></span>

<span data-ttu-id="16755-220">このタスクでは、サービス層に機能を抽出して、開発者がサービス機能をコントローラーレイヤーから簡単に分離できるようにする方法について説明します。これにより、実際に作業を行うサービスを再利用できます。</span><span class="sxs-lookup"><span data-stu-id="16755-220">This task will demonstrate how to extract functionality into a Service layer to make it easy for developers to separate their service functionality from the controller layer, thereby allowing reusability of the services that actually do the work.</span></span>

1. <span data-ttu-id="16755-221">ソリューションルートに新しいフォルダーを作成し、「**サービス**」という名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="16755-221">Create a new folder in the solution root and name it **Services**.</span></span> <span data-ttu-id="16755-222">これを行うには、[ **Contactmanager**プロジェクト] を右クリックし、[**追加** | **新しいフォルダー**] を選択して、「*サービス*」という名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="16755-222">To do this, right-click **ContactManager** project, select **Add** | **New Folder**, name it *Services*.</span></span>

    <span data-ttu-id="16755-223">![サービスフォルダーを作成しています](build-restful-apis-with-aspnet-web-api/_static/image14.png "サービスフォルダーを作成しています")</span><span class="sxs-lookup"><span data-stu-id="16755-223">![Creating Services folder](build-restful-apis-with-aspnet-web-api/_static/image14.png "Creating Services folder")</span></span>

    <span data-ttu-id="16755-224">*サービスフォルダーを作成しています*</span><span class="sxs-lookup"><span data-stu-id="16755-224">*Creating Services folder*</span></span>
2. <span data-ttu-id="16755-225">**サービス** フォルダーを右クリックし、追加 を選択します。 **クラス...** コンテキストメニューから。</span><span class="sxs-lookup"><span data-stu-id="16755-225">Right-click the **Services** folder and select **Add | Class...** from the context menu.</span></span>

    <span data-ttu-id="16755-226">![サービスフォルダーへの新しいクラスの追加](build-restful-apis-with-aspnet-web-api/_static/image15.png "サービスフォルダーへの新しいクラスの追加")</span><span class="sxs-lookup"><span data-stu-id="16755-226">![Adding a new class to the Services folder](build-restful-apis-with-aspnet-web-api/_static/image15.png "Adding a new class to the Services folder")</span></span>

    <span data-ttu-id="16755-227">*サービスフォルダーへの新しいクラスの追加*</span><span class="sxs-lookup"><span data-stu-id="16755-227">*Adding a new class to the Services folder*</span></span>
3. <span data-ttu-id="16755-228">**[新しい項目の追加]** ダイアログが表示されたら、新しいクラスに**contactrepository**という名前を指定し、 **[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="16755-228">When the **Add New Item** dialog appears, name the new class **ContactRepository** and click **Add**.</span></span>

    <span data-ttu-id="16755-229">![Contact Repository サービスレイヤーのコードを格納するクラスファイルを作成する](build-restful-apis-with-aspnet-web-api/_static/image16.png "Contact Repository サービスレイヤーのコードを格納するクラスファイルを作成する")</span><span class="sxs-lookup"><span data-stu-id="16755-229">![Creating a class file to contain the code for the Contact Repository service layer](build-restful-apis-with-aspnet-web-api/_static/image16.png "Creating a class file to contain the code for the Contact Repository service layer")</span></span>

    <span data-ttu-id="16755-230">*Contact Repository サービスレイヤーのコードを格納するクラスファイルを作成する*</span><span class="sxs-lookup"><span data-stu-id="16755-230">*Creating a class file to contain the code for the Contact Repository service layer*</span></span>
4. <span data-ttu-id="16755-231">**ContactRepository.cs**ファイルに using ディレクティブを追加して、モデルの名前空間を含めます。</span><span class="sxs-lookup"><span data-stu-id="16755-231">Add a using directive to the **ContactRepository.cs** file to include the models namespace.</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample4.cs)]
5. <span data-ttu-id="16755-232">次の強調表示されたコードを**ContactRepository.cs**ファイルに追加して、GetAllContacts メソッドを実装します。</span><span class="sxs-lookup"><span data-stu-id="16755-232">Add the following highlighted code to the **ContactRepository.cs** file to implement GetAllContacts method.</span></span>

    <span data-ttu-id="16755-233">(コードスニペット- *WEB API Lab-Ex01-Contact Repository*)</span><span class="sxs-lookup"><span data-stu-id="16755-233">(Code Snippet - *Web API Lab - Ex01 - Contact Repository*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample5.cs)]
6. <span data-ttu-id="16755-234">**ContactController.cs**ファイルがまだ開いていない場合は開きます。</span><span class="sxs-lookup"><span data-stu-id="16755-234">Open the **ContactController.cs** file if it is not already open.</span></span>
7. <span data-ttu-id="16755-235">次の using ステートメントをファイルの名前空間宣言セクションに追加します。</span><span class="sxs-lookup"><span data-stu-id="16755-235">Add the following using statement to the namespace declaration section of the file.</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample6.cs)]
8. <span data-ttu-id="16755-236">次の強調表示されたコードを**ContactController.cs**クラスに追加して、リポジトリのインスタンスを表すプライベートフィールドを追加します。これにより、他のクラスメンバーがサービス実装を利用できるようになります。</span><span class="sxs-lookup"><span data-stu-id="16755-236">Add the following highlighted code to the **ContactController.cs** class to add a private field to represent the instance of the repository, so that the rest of the class members can make use of the service implementation.</span></span>

    <span data-ttu-id="16755-237">(コードスニペット- *WEB API Lab-Ex01-Contact Controller*)</span><span class="sxs-lookup"><span data-stu-id="16755-237">(Code Snippet - *Web API Lab - Ex01 - Contact Controller*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample7.cs)]
9. <span data-ttu-id="16755-238">Contact repository サービスを利用できるように**Get**メソッドを変更します。</span><span class="sxs-lookup"><span data-stu-id="16755-238">Change the **Get** method so that it makes use of the contact repository service.</span></span>

    <span data-ttu-id="16755-239">(コードスニペット- *WEB API Lab-Ex01-リポジトリを介して連絡先の一覧を返す*)</span><span class="sxs-lookup"><span data-stu-id="16755-239">(Code Snippet - *Web API Lab - Ex01 - Returning a list of contacts via the repository*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample8.cs)]
10. <span data-ttu-id="16755-240">**Contactcontroller**の**Get**メソッドの定義にブレークポイントを設定します。</span><span class="sxs-lookup"><span data-stu-id="16755-240">Put a breakpoint on the **ContactController**'s **Get** method definition.</span></span>

   <span data-ttu-id="16755-241">![連絡先コントローラーへのブレークポイントの追加](build-restful-apis-with-aspnet-web-api/_static/image17.png "連絡先コントローラーへのブレークポイントの追加")</span><span class="sxs-lookup"><span data-stu-id="16755-241">![Adding breakpoints to the contact controller](build-restful-apis-with-aspnet-web-api/_static/image17.png "Adding breakpoints to the contact controller")</span></span>

   <span data-ttu-id="16755-242">*連絡先コントローラーへのブレークポイントの追加*</span><span class="sxs-lookup"><span data-stu-id="16755-242">*Adding breakpoints to the contact controller*</span></span>
11. <span data-ttu-id="16755-243">**F5** キーを押してアプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="16755-243">Press **F5** to run the application.</span></span>
12. <span data-ttu-id="16755-244">ブラウザーが開いたら、 **F12**キーを押して開発者ツールを開きます。</span><span class="sxs-lookup"><span data-stu-id="16755-244">When the browser opens, press **F12** to open the developer tools.</span></span>
13. <span data-ttu-id="16755-245">**[ネットワーク]** タブをクリックします。</span><span class="sxs-lookup"><span data-stu-id="16755-245">Click the **Network** tab.</span></span>
14. <span data-ttu-id="16755-246">**[キャプチャの開始]** ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="16755-246">Click the **Start Capturing** button.</span></span>
15. <span data-ttu-id="16755-247">アドレスバーにサフィックス **/api/contact**を入力して URL を追加し、 **enter**キーを押して api コントローラーを読み込みます。</span><span class="sxs-lookup"><span data-stu-id="16755-247">Append the URL in the address bar with the suffix **/api/contact** and press **Enter** to load the API controller.</span></span>
16. <span data-ttu-id="16755-248">**Get**メソッドの実行が開始されると、Visual Studio 2012 は中断されます。</span><span class="sxs-lookup"><span data-stu-id="16755-248">Visual Studio 2012 should break once **Get** method begins execution.</span></span>

   <span data-ttu-id="16755-249">![Get メソッド内での中断](build-restful-apis-with-aspnet-web-api/_static/image18.png "Get メソッド内での中断")</span><span class="sxs-lookup"><span data-stu-id="16755-249">![Breaking within the Get method](build-restful-apis-with-aspnet-web-api/_static/image18.png "Breaking within the Get method")</span></span>

   <span data-ttu-id="16755-250">*Get メソッド内での中断*</span><span class="sxs-lookup"><span data-stu-id="16755-250">*Breaking within the Get method*</span></span>
17. <span data-ttu-id="16755-251">**F5** キーを押して続行します。</span><span class="sxs-lookup"><span data-stu-id="16755-251">Press **F5** to continue.</span></span>
18. <span data-ttu-id="16755-252">まだフォーカスされていない場合は、Internet Explorer に戻ります。</span><span class="sxs-lookup"><span data-stu-id="16755-252">Go back to Internet Explorer if it is not already in focus.</span></span> <span data-ttu-id="16755-253">[ネットワークキャプチャ] ウィンドウに注意してください。</span><span class="sxs-lookup"><span data-stu-id="16755-253">Note the network capture window.</span></span>

    <span data-ttu-id="16755-254">![Web API 呼び出しの結果を表示する Internet Explorer のネットワークビュー](build-restful-apis-with-aspnet-web-api/_static/image19.png "Web API 呼び出しの結果を表示する Internet Explorer のネットワークビュー")</span><span class="sxs-lookup"><span data-stu-id="16755-254">![Network view in Internet Explorer showing results of the Web API call](build-restful-apis-with-aspnet-web-api/_static/image19.png "Network view in Internet Explorer showing results of the Web API call")</span></span>

    <span data-ttu-id="16755-255">*Web API 呼び出しの結果を表示する Internet Explorer のネットワークビュー*</span><span class="sxs-lookup"><span data-stu-id="16755-255">*Network view in Internet Explorer showing results of the Web API call*</span></span>
19. <span data-ttu-id="16755-256">**[詳細表示に進む]** ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="16755-256">Click the **Go to detailed view** button.</span></span>
20. <span data-ttu-id="16755-257">**[応答本文]** タブをクリックします。 API 呼び出しの JSON 出力と、サービスレイヤーによって取得された2つの連絡先を表す方法に注意してください。</span><span class="sxs-lookup"><span data-stu-id="16755-257">Click the **Response body** tab. Note the JSON output of the API call, and how it represents the two contacts retrieved by the service layer.</span></span>

    <span data-ttu-id="16755-258">![開発者ツールウィンドウで Web API からの JSON 出力を表示する](build-restful-apis-with-aspnet-web-api/_static/image20.png "開発者ツールウィンドウで Web API からの JSON 出力を表示する")</span><span class="sxs-lookup"><span data-stu-id="16755-258">![Viewing the JSON output from the Web API in the developer tools window](build-restful-apis-with-aspnet-web-api/_static/image20.png "Viewing the JSON output from the Web API in the developer tools window")</span></span>

    <span data-ttu-id="16755-259">*開発者ツールウィンドウで Web API からの JSON 出力を表示する*</span><span class="sxs-lookup"><span data-stu-id="16755-259">*Viewing the JSON output from the Web API in the developer tools window*</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Create_a_ReadWrite_Web_API"></a>
### <a name="exercise-2-create-a-readwrite-web-api"></a><span data-ttu-id="16755-260">演習 2: 読み取り/書き込み Web API を作成する</span><span class="sxs-lookup"><span data-stu-id="16755-260">Exercise 2: Create a Read/Write Web API</span></span>

<span data-ttu-id="16755-261">この演習では、連絡先マネージャーがデータ編集機能を有効にするための POST メソッドと PUT メソッドを実装します。</span><span class="sxs-lookup"><span data-stu-id="16755-261">In this exercise, you will implement POST and PUT methods for the contact manager to enable it with data-editing features.</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_-_Opening_the_Web_API_Project"></a>
#### <a name="task-1---opening-the-web-api-project"></a><span data-ttu-id="16755-262">タスク 1-Web API プロジェクトを開く</span><span class="sxs-lookup"><span data-stu-id="16755-262">Task 1 - Opening the Web API Project</span></span>

<span data-ttu-id="16755-263">このタスクでは、ユーザー入力を受け入れることができるように、演習1で作成した Web API プロジェクトを拡張する準備をします。</span><span class="sxs-lookup"><span data-stu-id="16755-263">In this task, you will prepare to enhance the Web API project created in Exercise 1 so that it can accept user input.</span></span>

1. <span data-ttu-id="16755-264">**Visual Studio 2012 Express For Web**を実行し**ます。これ**を行うには、 **[スタート]** に移り、 **VS Express for Web**入力して、enter キーを押します。</span><span class="sxs-lookup"><span data-stu-id="16755-264">Run **Visual Studio 2012 Express for Web**, to do this go to **Start** and type **VS Express for Web** then press **Enter**.</span></span>
2. <span data-ttu-id="16755-265">**Source/Ex02-ReadWriteWebAPI/begin/** folder にある**begin**ソリューションを開きます。</span><span class="sxs-lookup"><span data-stu-id="16755-265">Open the **Begin** solution located at **Source/Ex02-ReadWriteWebAPI/Begin/** folder.</span></span> <span data-ttu-id="16755-266">それ以外の場合は、前の演習を完了することによって得られた**終了**ソリューションを引き続き使用することができます。</span><span class="sxs-lookup"><span data-stu-id="16755-266">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="16755-267">提供された**Begin**ソリューションを開いた場合は、続行する前に、不足している NuGet パッケージをダウンロードする必要があります。</span><span class="sxs-lookup"><span data-stu-id="16755-267">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="16755-268">これを行うには、 **[プロジェクト]** メニューをクリックし、 **[NuGet パッケージの管理]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="16755-268">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="16755-269">**[NuGet パッケージの管理]** ダイアログで、 **[復元]** をクリックして、不足しているパッケージをダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="16755-269">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="16755-270">最後に、[**ビルド** | **ビルド**] をクリックしてソリューションをビルドします。</span><span class="sxs-lookup"><span data-stu-id="16755-270">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="16755-271">NuGet を使用する利点の1つは、プロジェクトのすべてのライブラリを配布する必要がなく、プロジェクトのサイズを小さくすることです。</span><span class="sxs-lookup"><span data-stu-id="16755-271">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="16755-272">NuGet パワーツールを使用すると、パッケージのバージョンを app.config ファイルで指定することで、プロジェクトを初めて実行するときに必要なすべてのライブラリをダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="16755-272">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="16755-273">このため、このラボから既存のソリューションを開いた後に、これらの手順を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="16755-273">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="16755-274">**Services/ContactRepository .cs**ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="16755-274">Open the **Services/ContactRepository.cs** file.</span></span>

<a id="Ex2Task2"></a>

<a id="Task_2_-_Adding_Data-Persistence_Features_to_the_Contact_Repository_Implementation"></a>
#### <a name="task-2---adding-data-persistence-features-to-the-contact-repository-implementation"></a><span data-ttu-id="16755-275">タスク 2-連絡先リポジトリの実装にデータの永続性機能を追加する</span><span class="sxs-lookup"><span data-stu-id="16755-275">Task 2 - Adding Data-Persistence Features to the Contact Repository Implementation</span></span>

<span data-ttu-id="16755-276">このタスクでは、演習1で作成した Web API プロジェクトの ContactRepository クラスを拡張して、ユーザー入力と新しい連絡先インスタンスを永続化して受け入れることができるようにします。</span><span class="sxs-lookup"><span data-stu-id="16755-276">In this task, you will augment the ContactRepository class of the Web API project created in Exercise 1 so that it can persist and accept user input and new Contact instances.</span></span>

1. <span data-ttu-id="16755-277">次の定数を**Contactrepository**クラスに追加して、この演習の後半で web サーバーキャッシュ項目のキー名を表します。</span><span class="sxs-lookup"><span data-stu-id="16755-277">Add the following constant to the **ContactRepository** class to represent the name of the web server cache item key name later in this exercise.</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample9.cs)]
2. <span data-ttu-id="16755-278">次のコードを含む**Contactrepository**にコンストラクターを追加します。</span><span class="sxs-lookup"><span data-stu-id="16755-278">Add a constructor to the **ContactRepository** containing the following code.</span></span>

    <span data-ttu-id="16755-279">(コードスニペット- *WEB API Lab-Ex02-Contact Repository Constructor*)</span><span class="sxs-lookup"><span data-stu-id="16755-279">(Code Snippet - *Web API Lab - Ex02 - Contact Repository Constructor*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample10.cs)]
3. <span data-ttu-id="16755-280">次に示すように、 **GetAllContacts**メソッドのコードを変更します。</span><span class="sxs-lookup"><span data-stu-id="16755-280">Modify the code for the **GetAllContacts** method as demonstrated below.</span></span>

    <span data-ttu-id="16755-281">(コードスニペット- *WEB API Lab-Ex02-すべての連絡先を取得*します)</span><span class="sxs-lookup"><span data-stu-id="16755-281">(Code Snippet - *Web API Lab - Ex02 - Get All Contacts*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample11.cs)]

    > [!NOTE]
    > <span data-ttu-id="16755-282">この例はデモンストレーションを目的としており、web サーバーのキャッシュをストレージメディアとして使用します。これにより、セッションストレージメカニズムや要求ストレージの有効期間を使用するのではなく、複数のクライアントで同時に値を使用できるようになります。</span><span class="sxs-lookup"><span data-stu-id="16755-282">This example is for demonstration purposes and will use the web server's cache as a storage medium, so that the values will be available to multiple clients simultaneously, rather than use a Session storage mechanism or a Request storage lifetime.</span></span> <span data-ttu-id="16755-283">Web サーバーキャッシュの代わりに、Entity Framework、XML ストレージ、またはその他のさまざまなものを使用できます。</span><span class="sxs-lookup"><span data-stu-id="16755-283">One could use Entity Framework, XML storage, or any other variety in place of the web server cache.</span></span>
4. <span data-ttu-id="16755-284">連絡先を保存する作業を行うために、 **Contactrepository**クラスに**SaveContact**という名前の新しいメソッドを実装します。</span><span class="sxs-lookup"><span data-stu-id="16755-284">Implement a new method named **SaveContact** to the **ContactRepository** class to do the work of saving a contact.</span></span> <span data-ttu-id="16755-285">**SaveContact**メソッドは、単一の**Contact**パラメーターを受け取り、成功または失敗を示すブール値を返す必要があります。</span><span class="sxs-lookup"><span data-stu-id="16755-285">The **SaveContact** method should take a single **Contact** parameter and return a Boolean value indicating success or failure.</span></span>

    <span data-ttu-id="16755-286">(コードスニペット- *WEB API Ex02-SaveContact メソッドの実装*)</span><span class="sxs-lookup"><span data-stu-id="16755-286">(Code Snippet - *Web API Lab - Ex02 - Implementing the SaveContact Method*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample12.cs)]

<a id="Exercise3"></a>

<a id="Exercise_3_Consume_the_Web_API_from_an_HTML_Client"></a>
### <a name="exercise-3-consume-the-web-api-from-an-html-client"></a><span data-ttu-id="16755-287">演習 3: HTML クライアントから Web API を使用する</span><span class="sxs-lookup"><span data-stu-id="16755-287">Exercise 3: Consume the Web API from an HTML Client</span></span>

<span data-ttu-id="16755-288">この演習では、Web API を呼び出す HTML クライアントを作成します。</span><span class="sxs-lookup"><span data-stu-id="16755-288">In this exercise, you will create an HTML client to call the Web API.</span></span> <span data-ttu-id="16755-289">このクライアントは、JavaScript を使用する Web API とのデータ交換を容易にし、HTML マークアップを使用して結果を web ブラウザーに表示します。</span><span class="sxs-lookup"><span data-stu-id="16755-289">This client will facilitate data exchange with the Web API using JavaScript and will display the results in a web browser using HTML markup.</span></span>

<a id="Ex3Task1"></a>

<a id="Task_1_-_Modifying_the_Index_View_to_Provide_a_GUI_for_Displaying_Contacts"></a>
#### <a name="task-1---modifying-the-index-view-to-provide-a-gui-for-displaying-contacts"></a><span data-ttu-id="16755-290">タスク 1-インデックスビューを変更して、連絡先を表示する GUI を提供する</span><span class="sxs-lookup"><span data-stu-id="16755-290">Task 1 - Modifying the Index View to Provide a GUI for Displaying Contacts</span></span>

<span data-ttu-id="16755-291">このタスクでは、web アプリケーションの既定のインデックスビューを変更して、既存の連絡先の一覧を HTML ブラウザーに表示するための要件をサポートします。</span><span class="sxs-lookup"><span data-stu-id="16755-291">In this task, you will modify the default Index view of the web application to support the requirement of displaying the list of existing contacts in an HTML browser.</span></span>

1. <span data-ttu-id="16755-292">**Visual Studio 2012 Express For Web**がまだ開いていない場合は開きます。</span><span class="sxs-lookup"><span data-stu-id="16755-292">Open **Visual Studio 2012 Express for Web** if it is not already open.</span></span>
2. <span data-ttu-id="16755-293">**Source/Ex03-ConsumingWebAPI/begin/** folder にある**begin**ソリューションを開きます。</span><span class="sxs-lookup"><span data-stu-id="16755-293">Open the **Begin** solution located at **Source/Ex03-ConsumingWebAPI/Begin/** folder.</span></span> <span data-ttu-id="16755-294">それ以外の場合は、前の演習を完了することによって得られた**終了**ソリューションを引き続き使用することができます。</span><span class="sxs-lookup"><span data-stu-id="16755-294">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="16755-295">提供された**Begin**ソリューションを開いた場合は、続行する前に、不足している NuGet パッケージをダウンロードする必要があります。</span><span class="sxs-lookup"><span data-stu-id="16755-295">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="16755-296">これを行うには、 **[プロジェクト]** メニューをクリックし、 **[NuGet パッケージの管理]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="16755-296">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="16755-297">**[NuGet パッケージの管理]** ダイアログで、 **[復元]** をクリックして、不足しているパッケージをダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="16755-297">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="16755-298">最後に、[**ビルド** | **ビルド**] をクリックしてソリューションをビルドします。</span><span class="sxs-lookup"><span data-stu-id="16755-298">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="16755-299">NuGet を使用する利点の1つは、プロジェクトのすべてのライブラリを配布する必要がなく、プロジェクトのサイズを小さくすることです。</span><span class="sxs-lookup"><span data-stu-id="16755-299">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="16755-300">NuGet パワーツールを使用すると、パッケージのバージョンを app.config ファイルで指定することで、プロジェクトを初めて実行するときに必要なすべてのライブラリをダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="16755-300">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="16755-301">このため、このラボから既存のソリューションを開いた後に、これらの手順を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="16755-301">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="16755-302">**Views/Home**フォルダーにある**インデックスの cshtml**ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="16755-302">Open the **Index.cshtml** file located at **Views/Home** folder.</span></span>
4. <span data-ttu-id="16755-303">Div 要素内の HTML コードを id**本文**に置き換えて、次のコードのようにします。</span><span class="sxs-lookup"><span data-stu-id="16755-303">Replace the HTML code within the div element with id **body** so that it looks like the following code.</span></span>

    [!code-html[Main](build-restful-apis-with-aspnet-web-api/samples/sample13.html)]
5. <span data-ttu-id="16755-304">ファイルの末尾に次の Javascript コードを追加して、Web API への HTTP 要求を実行します。</span><span class="sxs-lookup"><span data-stu-id="16755-304">Add the following Javascript code at the bottom of the file to perform the HTTP request to the Web API.</span></span>

    [!code-cshtml[Main](build-restful-apis-with-aspnet-web-api/samples/sample14.cshtml)]
6. <span data-ttu-id="16755-305">**ContactController.cs**ファイルがまだ開いていない場合は開きます。</span><span class="sxs-lookup"><span data-stu-id="16755-305">Open the **ContactController.cs** file if it is not already open.</span></span>
7. <span data-ttu-id="16755-306">**Contactcontroller**クラスの**Get**メソッドにブレークポイントを設定します。</span><span class="sxs-lookup"><span data-stu-id="16755-306">Place a breakpoint on the **Get** method of the **ContactController** class.</span></span>

    <span data-ttu-id="16755-307">![API コントローラーの Get メソッドにブレークポイントを配置する](build-restful-apis-with-aspnet-web-api/_static/image21.png "API コントローラーの Get メソッドにブレークポイントを配置する")</span><span class="sxs-lookup"><span data-stu-id="16755-307">![Placing a breakpoint on the Get method of the API controller](build-restful-apis-with-aspnet-web-api/_static/image21.png "Placing a breakpoint on the Get method of the API controller")</span></span>

    <span data-ttu-id="16755-308">*API コントローラーの Get メソッドにブレークポイントを配置する*</span><span class="sxs-lookup"><span data-stu-id="16755-308">*Placing a breakpoint on the Get method of the API controller*</span></span>
8. <span data-ttu-id="16755-309">**F5** キーを押してプロジェクトを実行します。</span><span class="sxs-lookup"><span data-stu-id="16755-309">Press **F5** to run the project.</span></span> <span data-ttu-id="16755-310">ブラウザーは HTML ドキュメントを読み込みます。</span><span class="sxs-lookup"><span data-stu-id="16755-310">The browser will load the HTML document.</span></span>

    > [!NOTE]
    > <span data-ttu-id="16755-311">アプリケーションのルート URL を参照していることを確認します。</span><span class="sxs-lookup"><span data-stu-id="16755-311">Ensure that you are browsing to the root URL of your application.</span></span>
9. <span data-ttu-id="16755-312">ページが読み込まれ、JavaScript が実行されると、ブレークポイントにヒットし、コントローラーでコードの実行が一時停止されます。</span><span class="sxs-lookup"><span data-stu-id="16755-312">Once the page loads and the JavaScript executes, the breakpoint will be hit and the code execution will pause in the controller.</span></span>

    <span data-ttu-id="16755-313">![VS Express for Web を使用した Web API 呼び出しへのデバッグ](build-restful-apis-with-aspnet-web-api/_static/image22.png "VS Express for Web を使用した Web API 呼び出しへのデバッグ")</span><span class="sxs-lookup"><span data-stu-id="16755-313">![Debugging into the Web API calls using VS Express for Web](build-restful-apis-with-aspnet-web-api/_static/image22.png "Debugging into the Web API calls using VS Express for Web")</span></span>

    <span data-ttu-id="16755-314">*Visual Studio 2012 Express for Web を使用した Web API 呼び出しへのデバッグ*</span><span class="sxs-lookup"><span data-stu-id="16755-314">*Debugging into the Web API call using Visual Studio 2012 Express for Web*</span></span>
10. <span data-ttu-id="16755-315">ブレークポイントを削除し、 **F5**キーまたはデバッグツールバーの **[続行]** ボタンを押して、ブラウザーでのビューの読み込みを続行します。</span><span class="sxs-lookup"><span data-stu-id="16755-315">Remove the breakpoint and press **F5** or the debugging toolbar's **Continue** button to continue loading the view in the browser.</span></span> <span data-ttu-id="16755-316">Web API の呼び出しが完了すると、ブラウザーにリスト項目として表示された Web API 呼び出しから返された連絡先が表示されます。</span><span class="sxs-lookup"><span data-stu-id="16755-316">Once the Web API call completes you should see the contacts returned from the Web API call displayed as list items in the browser.</span></span>

    <span data-ttu-id="16755-317">![ブラウザーにリスト項目として表示される API 呼び出しの結果](build-restful-apis-with-aspnet-web-api/_static/image23.png "ブラウザーにリスト項目として表示される API 呼び出しの結果")</span><span class="sxs-lookup"><span data-stu-id="16755-317">![Results of the API call displayed in the browser as list items](build-restful-apis-with-aspnet-web-api/_static/image23.png "Results of the API call displayed in the browser as list items")</span></span>

    <span data-ttu-id="16755-318">*ブラウザーにリスト項目として表示される API 呼び出しの結果*</span><span class="sxs-lookup"><span data-stu-id="16755-318">*Results of the API call displayed in the browser as list items*</span></span>
11. <span data-ttu-id="16755-319">デバッグを停止します。</span><span class="sxs-lookup"><span data-stu-id="16755-319">Stop debugging.</span></span>

<a id="Ex3Task2"></a>

<a id="Task_2_-_Modifying_the_Index_View_to_Provide_a_GUI_for_Creating_Contacts"></a>
#### <a name="task-2---modifying-the-index-view-to-provide-a-gui-for-creating-contacts"></a><span data-ttu-id="16755-320">タスク 2-インデックスビューを変更して、連絡先を作成するための GUI を提供する</span><span class="sxs-lookup"><span data-stu-id="16755-320">Task 2 - Modifying the Index View to Provide a GUI for Creating Contacts</span></span>

<span data-ttu-id="16755-321">このタスクでは、MVC アプリケーションのインデックスビューの変更を続行します。</span><span class="sxs-lookup"><span data-stu-id="16755-321">In this task, you will continue to modify the Index view of the MVC application.</span></span> <span data-ttu-id="16755-322">ユーザー入力をキャプチャし、Web API に送信して新しい連絡先を作成するフォームが HTML ページに追加され、GUI から日付を収集するための新しい Web API コントローラーメソッドが作成されます。</span><span class="sxs-lookup"><span data-stu-id="16755-322">A form will be added to the HTML page that will capture user input and send it to the Web API to create a new Contact, and a new Web API controller method will be created to collect date from the GUI.</span></span>

1. <span data-ttu-id="16755-323">**ContactController.cs**ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="16755-323">Open the **ContactController.cs** file.</span></span>
2. <span data-ttu-id="16755-324">次のコードに示すように、 **Post**という名前のコントローラークラスに新しいメソッドを追加します。</span><span class="sxs-lookup"><span data-stu-id="16755-324">Add a new method to the controller class named **Post** as shown in the following code.</span></span>

    <span data-ttu-id="16755-325">(コードスニペット- *WEB API Ex03-Post メソッド*)</span><span class="sxs-lookup"><span data-stu-id="16755-325">(Code Snippet - *Web API Lab - Ex03 - Post Method*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample15.cs)]
3. <span data-ttu-id="16755-326">まだ開いていない場合は、Visual Studio で**インデックスの cshtml**ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="16755-326">Open the **Index.cshtml** file in Visual Studio if it is not already open.</span></span>
4. <span data-ttu-id="16755-327">前のタスクで追加した順序付けられていないリストの直後に、次の HTML コードをファイルに追加します。</span><span class="sxs-lookup"><span data-stu-id="16755-327">Add the HTML code below to the file just after the unordered list you added in the previous task.</span></span>

    [!code-html[Main](build-restful-apis-with-aspnet-web-api/samples/sample16.html)]
5. <span data-ttu-id="16755-328">ドキュメントの下部にある script 要素内に、ボタンクリックイベントを処理する次の強調表示されたコードを追加します。これにより、HTTP POST 呼び出しを使用して Web API にデータがポストされます。</span><span class="sxs-lookup"><span data-stu-id="16755-328">Within the script element at the bottom of the document, add the following highlighted code to handle button-click events, which will post the data to the Web API using an HTTP POST call.</span></span>

    [!code-html[Main](build-restful-apis-with-aspnet-web-api/samples/sample17.html)]
6. <span data-ttu-id="16755-329">**ContactController.cs**で、 **Post**メソッドにブレークポイントを設定します。</span><span class="sxs-lookup"><span data-stu-id="16755-329">In **ContactController.cs**, place a breakpoint on the **Post** method.</span></span>
7. <span data-ttu-id="16755-330">**F5**キーを押して、ブラウザーでアプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="16755-330">Press **F5** to run the application in the browser.</span></span>
8. <span data-ttu-id="16755-331">ブラウザーにページが読み込まれたら、新しい連絡先の名前と Id を入力し、 **[保存]** ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="16755-331">Once the page is loaded in the browser, type in a new contact name and Id and click the **Save** button.</span></span>

    <span data-ttu-id="16755-332">![ブラウザーに読み込まれたクライアントの HTML ドキュメント](build-restful-apis-with-aspnet-web-api/_static/image24.png "ブラウザーに読み込まれたクライアントの HTML ドキュメント")</span><span class="sxs-lookup"><span data-stu-id="16755-332">![The client HTML document loaded in the browser](build-restful-apis-with-aspnet-web-api/_static/image24.png "The client HTML document loaded in the browser")</span></span>

    <span data-ttu-id="16755-333">*ブラウザーに読み込まれたクライアントの HTML ドキュメント*</span><span class="sxs-lookup"><span data-stu-id="16755-333">*The client HTML document loaded in the browser*</span></span>
9. <span data-ttu-id="16755-334">**Post**メソッドでデバッガーウィンドウが中断した場合は、 **contact**パラメーターのプロパティを参照してください。</span><span class="sxs-lookup"><span data-stu-id="16755-334">When the debugger window breaks in the **Post** method, take a look at the properties of the **contact** parameter.</span></span> <span data-ttu-id="16755-335">値は、フォームに入力したデータと一致している必要があります。</span><span class="sxs-lookup"><span data-stu-id="16755-335">The values should match the data you entered in the form.</span></span>

    <span data-ttu-id="16755-336">![クライアントから Web API に送信される Contact オブジェクト](build-restful-apis-with-aspnet-web-api/_static/image25.png "クライアントから Web API に送信される Contact オブジェクト")</span><span class="sxs-lookup"><span data-stu-id="16755-336">![The Contact object being sent to the Web API from the client](build-restful-apis-with-aspnet-web-api/_static/image25.png "The Contact object being sent to the Web API from the client")</span></span>

    <span data-ttu-id="16755-337">*クライアントから Web API に送信される Contact オブジェクト*</span><span class="sxs-lookup"><span data-stu-id="16755-337">*The Contact object being sent to the Web API from the client*</span></span>
10. <span data-ttu-id="16755-338">**応答**変数が作成されるまで、デバッガーでメソッドをステップ実行します。</span><span class="sxs-lookup"><span data-stu-id="16755-338">Step through the method in the debugger until the **response** variable has been created.</span></span> <span data-ttu-id="16755-339">デバッガーの **[ローカル]** ウィンドウで検査すると、すべてのプロパティが設定されていることがわかります。</span><span class="sxs-lookup"><span data-stu-id="16755-339">Upon inspection in the **Locals** window in the debugger, you'll see that all the properties have been set.</span></span>

   <span data-ttu-id="16755-340">![デバッガーでの作成後の応答](build-restful-apis-with-aspnet-web-api/_static/image26.png "デバッガーでの作成後の応答")</span><span class="sxs-lookup"><span data-stu-id="16755-340">![The response following creation in the debugger](build-restful-apis-with-aspnet-web-api/_static/image26.png "The response following creation in the debugger")</span></span>

   <span data-ttu-id="16755-341">*デバッガーでの作成後の応答*</span><span class="sxs-lookup"><span data-stu-id="16755-341">*The response following creation in the debugger*</span></span>
11. <span data-ttu-id="16755-342">**F5**キーを押すか、デバッガーで **[続行]** をクリックすると、要求が完了します。</span><span class="sxs-lookup"><span data-stu-id="16755-342">If you press **F5** or click **Continue** in the debugger the request will complete.</span></span> <span data-ttu-id="16755-343">ブラウザーに戻ると、 **Contactrepository**実装によって格納されている連絡先の一覧に新しい連絡先が追加されます。</span><span class="sxs-lookup"><span data-stu-id="16755-343">Once you switch back to the browser, the new contact has been added to the list of contacts stored by the **ContactRepository** implementation.</span></span>

   <span data-ttu-id="16755-344">![ブラウザーに新しい連絡先インスタンスが正常に作成されたことが反映されます。](build-restful-apis-with-aspnet-web-api/_static/image27.png "ブラウザーに新しい連絡先インスタンスが正常に作成されたことが反映されます。")</span><span class="sxs-lookup"><span data-stu-id="16755-344">![The browser reflects successful creation of the new contact instance](build-restful-apis-with-aspnet-web-api/_static/image27.png "The browser reflects successful creation of the new contact instance")</span></span>

   <span data-ttu-id="16755-345">*ブラウザーに新しい連絡先インスタンスが正常に作成されたことが反映されます。*</span><span class="sxs-lookup"><span data-stu-id="16755-345">*The browser reflects successful creation of the new contact instance*</span></span>

> [!NOTE]
> <span data-ttu-id="16755-346">また、 [「付録 C: Web 配置を使用した ASP.NET MVC 4 アプリケーションの発行](#AppendixC)」に従って、このアプリケーションを Azure にデプロイすることもできます。</span><span class="sxs-lookup"><span data-stu-id="16755-346">Additionally, you can deploy this application to Azure following [Appendix C: Publishing an ASP.NET MVC 4 Application using Web Deploy](#AppendixC).</span></span>

---

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="16755-347">まとめ</span><span class="sxs-lookup"><span data-stu-id="16755-347">Summary</span></span>

<span data-ttu-id="16755-348">このラボでは、新しい ASP.NET Web API framework と、フレームワークを使用した RESTful Web Api の実装について紹介しました。</span><span class="sxs-lookup"><span data-stu-id="16755-348">This lab has introduced you to the new ASP.NET Web API framework and to the implementation of RESTful Web APIs using the framework.</span></span> <span data-ttu-id="16755-349">ここから、このラボの例として提供されている単純なメカニズムではなく、任意の数のメカニズムを使用してデータの永続化を容易にする新しいリポジトリを作成できます。</span><span class="sxs-lookup"><span data-stu-id="16755-349">From here, you could create a new repository that facilitates data persistence using any number of mechanisms and wire that service up rather than the simple one provided as an example in this lab.</span></span> <span data-ttu-id="16755-350">Web API は、HTTP、JSON、または XML をサポートする任意の言語で記述された HTML 以外のクライアントからの通信を可能にするなど、多くの追加機能をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="16755-350">Web API supports a number of additional features, such as enabling communication from non-HTML clients written in any language that supports HTTP and JSON or XML.</span></span> <span data-ttu-id="16755-351">一般的な web アプリケーションの外部で Web API をホストする機能も可能であり、独自のシリアル化形式を作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="16755-351">The ability to host a Web API outside of a typical web application is also possible, as well as is the ability to create your own serialization formats.</span></span>

<span data-ttu-id="16755-352">ASP.NET Web サイトには、 [[https://asp.net/web-api](https://asp.net/web-api)](https://asp.net/web-api)の ASP.NET Web API フレームワーク専用の領域があります。</span><span class="sxs-lookup"><span data-stu-id="16755-352">The ASP.NET Web site has an area dedicated to the ASP.NET Web API framework at [[https://asp.net/web-api](https://asp.net/web-api)](https://asp.net/web-api).</span></span> <span data-ttu-id="16755-353">このサイトでは、Web API に関する最新の情報、サンプル、ニュースが引き続き提供されます。そのため、事実上あらゆるデバイスまたは開発フレームワークで使用できるカスタム Web Api の作成について詳しく掘り下げたい場合は、頻繁に確認してください。</span><span class="sxs-lookup"><span data-stu-id="16755-353">This site will continue to provide late-breaking information, samples, and news related to Web API, so check it frequently if you'd like to delve deeper into the art of creating custom Web APIs available to virtually any device or development framework.</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Using_Code_Snippets"></a>
## <a name="appendix-a-using-code-snippets"></a><span data-ttu-id="16755-354">付録 A: コードスニペットの使用</span><span class="sxs-lookup"><span data-stu-id="16755-354">Appendix A: Using Code Snippets</span></span>

<span data-ttu-id="16755-355">コードスニペットを使用すると、必要なすべてのコードをすぐに利用できます。</span><span class="sxs-lookup"><span data-stu-id="16755-355">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="16755-356">次の図に示すように、ラボドキュメントには、使用できるタイミングがわかります。</span><span class="sxs-lookup"><span data-stu-id="16755-356">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="16755-357">![Visual Studio のコードスニペットを使用してプロジェクトにコードを挿入する](build-restful-apis-with-aspnet-web-api/_static/image28.png "Visual Studio のコードスニペットを使用してプロジェクトにコードを挿入する")</span><span class="sxs-lookup"><span data-stu-id="16755-357">![Using Visual Studio code snippets to insert code into your project](build-restful-apis-with-aspnet-web-api/_static/image28.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="16755-358">*Visual Studio のコードスニペットを使用してプロジェクトにコードを挿入する*</span><span class="sxs-lookup"><span data-stu-id="16755-358">*Using Visual Studio code snippets to insert code into your project*</span></span>

<a id="CodeSnippetUsingKeyBoard"></a>

<a id="To_add_a_code_snippet_using_the_keyboard_C_only"></a>
### <a name="to-add-a-code-snippet-using-the-keyboard-c-only"></a><span data-ttu-id="16755-359">キーボードを使用してコードスニペットを追加C#するには (のみ)</span><span class="sxs-lookup"><span data-stu-id="16755-359">To add a code snippet using the keyboard (C# only)</span></span>

1. <span data-ttu-id="16755-360">コードを挿入する場所にカーソルを置きます。</span><span class="sxs-lookup"><span data-stu-id="16755-360">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="16755-361">(スペースまたはハイフンを含まない) スニペット名の入力を開始します。</span><span class="sxs-lookup"><span data-stu-id="16755-361">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="16755-362">IntelliSense によって、一致するスニペットの名前が表示されます。</span><span class="sxs-lookup"><span data-stu-id="16755-362">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="16755-363">正しいスニペットを選択します (または、スニペットの名前全体が選択されるまで入力し続けます)。</span><span class="sxs-lookup"><span data-stu-id="16755-363">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="16755-364">Tab キーを2回押すと、スニペットがカーソル位置に挿入されます。</span><span class="sxs-lookup"><span data-stu-id="16755-364">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

    <span data-ttu-id="16755-365">![スニペット名の入力を開始します](build-restful-apis-with-aspnet-web-api/_static/image29.png "スニペット名の入力を開始します")</span><span class="sxs-lookup"><span data-stu-id="16755-365">![Start typing the snippet name](build-restful-apis-with-aspnet-web-api/_static/image29.png "Start typing the snippet name")</span></span>

    <span data-ttu-id="16755-366">*スニペット名の入力を開始します*</span><span class="sxs-lookup"><span data-stu-id="16755-366">*Start typing the snippet name*</span></span>

    <span data-ttu-id="16755-367">![Tab キーを押して、強調表示されているスニペットを選択します](build-restful-apis-with-aspnet-web-api/_static/image30.png "Tab キーを押して、強調表示されているスニペットを選択します")</span><span class="sxs-lookup"><span data-stu-id="16755-367">![Press Tab to select the highlighted snippet](build-restful-apis-with-aspnet-web-api/_static/image30.png "Press Tab to select the highlighted snippet")</span></span>

    <span data-ttu-id="16755-368">*Tab キーを押して、強調表示されているスニペットを選択します*</span><span class="sxs-lookup"><span data-stu-id="16755-368">*Press Tab to select the highlighted snippet*</span></span>

    <span data-ttu-id="16755-369">![もう一度 Tab キーを押すと、スニペットが展開されます。](build-restful-apis-with-aspnet-web-api/_static/image31.png "もう一度 Tab キーを押すと、スニペットが展開されます。")</span><span class="sxs-lookup"><span data-stu-id="16755-369">![Press Tab again and the snippet will expand](build-restful-apis-with-aspnet-web-api/_static/image31.png "Press Tab again and the snippet will expand")</span></span>

    <span data-ttu-id="16755-370">*もう一度 Tab キーを押すと、スニペットが展開されます。*</span><span class="sxs-lookup"><span data-stu-id="16755-370">*Press Tab again and the snippet will expand*</span></span>

<a id="CodeSnippetUsingMouse"></a>

<a id="To_add_a_code_snippet_using_the_mouse_C_Visual_Basic_and_XML"></a>
### <a name="to-add-a-code-snippet-using-the-mouse-c-visual-basic-and-xml"></a><span data-ttu-id="16755-371">マウス (C#、VISUAL BASIC および XML) を使用してコードスニペットを追加するには</span><span class="sxs-lookup"><span data-stu-id="16755-371">To add a code snippet using the mouse (C#, Visual Basic and XML)</span></span>

1. <span data-ttu-id="16755-372">コードスニペットを挿入する場所を右クリックします。</span><span class="sxs-lookup"><span data-stu-id="16755-372">Right-click where you want to insert the code snippet.</span></span>
2. <span data-ttu-id="16755-373">**[スニペットの挿入]** 、 **[マイコードスニペット**] の順に選択します。</span><span class="sxs-lookup"><span data-stu-id="16755-373">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
3. <span data-ttu-id="16755-374">一覧から該当するスニペットをクリックして選択します。</span><span class="sxs-lookup"><span data-stu-id="16755-374">Pick the relevant snippet from the list, by clicking on it.</span></span>

    <span data-ttu-id="16755-375">![コードスニペットを挿入する場所を右クリックし、[スニペットの挿入] を選択します。](build-restful-apis-with-aspnet-web-api/_static/image32.png "コードスニペットを挿入する場所を右クリックし、[スニペットの挿入] を選択します。")</span><span class="sxs-lookup"><span data-stu-id="16755-375">![Right-click where you want to insert the code snippet and select Insert Snippet](build-restful-apis-with-aspnet-web-api/_static/image32.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

    <span data-ttu-id="16755-376">*コードスニペットを挿入する場所を右クリックし、[スニペットの挿入] を選択します。*</span><span class="sxs-lookup"><span data-stu-id="16755-376">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

    <span data-ttu-id="16755-377">![一覧から関連するスニペットをクリックして選択します。](build-restful-apis-with-aspnet-web-api/_static/image33.png "一覧から関連するスニペットをクリックして選択します。")</span><span class="sxs-lookup"><span data-stu-id="16755-377">![Pick the relevant snippet from the list, by clicking on it](build-restful-apis-with-aspnet-web-api/_static/image33.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

    <span data-ttu-id="16755-378">*一覧から関連するスニペットをクリックして選択します。*</span><span class="sxs-lookup"><span data-stu-id="16755-378">*Pick the relevant snippet from the list, by clicking on it*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-b-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="16755-379">付録 B: Visual Studio Express 2012 を Web 用にインストールする</span><span class="sxs-lookup"><span data-stu-id="16755-379">Appendix B: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="16755-380">**[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)** を使用して、Web または別の &quot;Express&quot; バージョン**用に Microsoft Visual Studio Express 2012**をインストールできます。</span><span class="sxs-lookup"><span data-stu-id="16755-380">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="16755-381">次の手順では、 *Microsoft Web Platform Installer*を使用して*Visual studio Express 2012 for Web*をインストールするために必要な手順について説明します。</span><span class="sxs-lookup"><span data-stu-id="16755-381">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="16755-382">[[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)にアクセスします。</span><span class="sxs-lookup"><span data-stu-id="16755-382">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="16755-383">または、Web Platform Installer が既にインストールされている場合は、それを開いて、 <em>AZURE SDK&quot;で web 用に 2012 Visual Studio Express を</em>検索 &quot;ことができます。</span><span class="sxs-lookup"><span data-stu-id="16755-383">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="16755-384">**[今すぐインストール]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="16755-384">Click on **Install Now**.</span></span> <span data-ttu-id="16755-385">**Web Platform Installer**がない場合は、最初にダウンロードしてインストールするようにリダイレクトされます。</span><span class="sxs-lookup"><span data-stu-id="16755-385">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="16755-386">**Web Platform Installer**が開いたら、 **[インストール]** をクリックしてセットアップを開始します。</span><span class="sxs-lookup"><span data-stu-id="16755-386">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="16755-387">![Visual Studio Express のインストール](build-restful-apis-with-aspnet-web-api/_static/image34.png "Visual Studio Express のインストール")</span><span class="sxs-lookup"><span data-stu-id="16755-387">![Install Visual Studio Express](build-restful-apis-with-aspnet-web-api/_static/image34.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="16755-388">*Visual Studio Express のインストール*</span><span class="sxs-lookup"><span data-stu-id="16755-388">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="16755-389">すべての製品のライセンスと条項を読み、[**同意**する] をクリックして続行します。</span><span class="sxs-lookup"><span data-stu-id="16755-389">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![ライセンス条項に同意する](build-restful-apis-with-aspnet-web-api/_static/image35.png)

    <span data-ttu-id="16755-391">*ライセンス条項に同意する*</span><span class="sxs-lookup"><span data-stu-id="16755-391">*Accepting the license terms*</span></span>
5. <span data-ttu-id="16755-392">ダウンロードとインストールのプロセスが完了するまで待ちます。</span><span class="sxs-lookup"><span data-stu-id="16755-392">Wait until the downloading and installation process completes.</span></span>

    ![Installation progress](build-restful-apis-with-aspnet-web-api/_static/image36.png)

    <span data-ttu-id="16755-394">*インストールの進行状況*</span><span class="sxs-lookup"><span data-stu-id="16755-394">*Installation progress*</span></span>
6. <span data-ttu-id="16755-395">インストールが完了したら、 **[完了]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="16755-395">When the installation completes, click **Finish**.</span></span>

    ![インストールの完了](build-restful-apis-with-aspnet-web-api/_static/image37.png)

    <span data-ttu-id="16755-397">*インストールの完了*</span><span class="sxs-lookup"><span data-stu-id="16755-397">*Installation completed*</span></span>
7. <span data-ttu-id="16755-398">**[終了]** をクリックして Web Platform Installer を閉じます。</span><span class="sxs-lookup"><span data-stu-id="16755-398">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="16755-399">Web 用の Visual Studio Express を開くには、**スタート**画面にアクセスして &quot;**VS Express**&quot;の書き込みを開始し、 **[VS Express for Web]** タイルをクリックします。</span><span class="sxs-lookup"><span data-stu-id="16755-399">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![VS Express for Web タイル](build-restful-apis-with-aspnet-web-api/_static/image38.png)

    <span data-ttu-id="16755-401">*VS Express for Web タイル*</span><span class="sxs-lookup"><span data-stu-id="16755-401">*VS Express for Web tile*</span></span>

<a id="AppendixC"></a>

<a id="Appendix_C_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-c-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="16755-402">付録 C: Web 配置を使用した ASP.NET MVC 4 アプリケーションの発行</span><span class="sxs-lookup"><span data-stu-id="16755-402">Appendix C: Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

<span data-ttu-id="16755-403">この付録では、azure によって提供される Web 配置公開機能を活用して、Azure Portal から新しい web サイトを作成し、取得したアプリケーションを発行する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="16755-403">This appendix will show you how to create a new web site from the Azure Portal and publish the application you obtained by following the lab, taking advantage of the Web Deploy publishing feature provided by Azure.</span></span>

<a id="ApxCTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-azure-portal"></a><span data-ttu-id="16755-404">タスク 1-Azure Portal から新しい Web サイトを作成する</span><span class="sxs-lookup"><span data-stu-id="16755-404">Task 1 - Creating a New Web Site from the Azure Portal</span></span>

1. <span data-ttu-id="16755-405">[Azure 管理ポータル](https://manage.windowsazure.com/)にアクセスし、サブスクリプションに関連付けられている Microsoft 資格情報を使用してサインインします。</span><span class="sxs-lookup"><span data-stu-id="16755-405">Go to the [Azure Management Portal](https://manage.windowsazure.com/) and sign in using the Microsoft credentials associated with your subscription.</span></span>

    > [!NOTE]
    > <span data-ttu-id="16755-406">Azure では、10 ASP.NET の Web サイトを無料でホストし、トラフィックの増加に合わせて拡張できます。</span><span class="sxs-lookup"><span data-stu-id="16755-406">With Azure you can host 10 ASP.NET Web Sites for free and then scale as your traffic grows.</span></span> <span data-ttu-id="16755-407">[ここで](https://aka.ms/aspnet-hol-azure)サインアップできます。</span><span class="sxs-lookup"><span data-stu-id="16755-407">You can sign up [here](https://aka.ms/aspnet-hol-azure).</span></span>

    <span data-ttu-id="16755-408">![Windows Azure portal にログオンします。](build-restful-apis-with-aspnet-web-api/_static/image39.png "Windows Azure portal にログオンします。")</span><span class="sxs-lookup"><span data-stu-id="16755-408">![Log on to Windows Azure portal](build-restful-apis-with-aspnet-web-api/_static/image39.png "Log on to Windows Azure portal")</span></span>

    <span data-ttu-id="16755-409">*ポータルにログオンする*</span><span class="sxs-lookup"><span data-stu-id="16755-409">*Log on to Portal*</span></span>
2. <span data-ttu-id="16755-410">コマンドバーの **[新規]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="16755-410">Click **New** on the command bar.</span></span>

    <span data-ttu-id="16755-411">![新しい Web サイトの作成](build-restful-apis-with-aspnet-web-api/_static/image40.png "新しい Web サイトの作成")</span><span class="sxs-lookup"><span data-stu-id="16755-411">![Creating a new Web Site](build-restful-apis-with-aspnet-web-api/_static/image40.png "Creating a new Web Site")</span></span>

    <span data-ttu-id="16755-412">*新しい Web サイトの作成*</span><span class="sxs-lookup"><span data-stu-id="16755-412">*Creating a new Web Site*</span></span>
3. <span data-ttu-id="16755-413">[ **Compute** | **Web サイト**] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="16755-413">Click **Compute** | **Web Site**.</span></span> <span data-ttu-id="16755-414">次に、 **[簡易作成]** オプションを選択します。</span><span class="sxs-lookup"><span data-stu-id="16755-414">Then select **Quick Create** option.</span></span> <span data-ttu-id="16755-415">新しい web サイトの使用可能な URL を指定し、 **[Web サイトの作成]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="16755-415">Provide an available URL for the new web site and click **Create Web Site**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="16755-416">Azure は、管理および管理が可能なクラウドで実行されている web アプリケーションのホストです。</span><span class="sxs-lookup"><span data-stu-id="16755-416">Azure is the host for a web application running in the cloud that you can control and manage.</span></span> <span data-ttu-id="16755-417">[簡易作成] オプションを使用すると、完成した web アプリケーションをポータルの外部から Azure にデプロイできます。</span><span class="sxs-lookup"><span data-stu-id="16755-417">The Quick Create option allows you to deploy a completed web application to the Azure from outside the portal.</span></span> <span data-ttu-id="16755-418">データベースを設定する手順は含まれていません。</span><span class="sxs-lookup"><span data-stu-id="16755-418">It does not include steps for setting up a database.</span></span>

    <span data-ttu-id="16755-419">![簡易作成を使用した新しい Web サイトの作成](build-restful-apis-with-aspnet-web-api/_static/image41.png "簡易作成を使用した新しい Web サイトの作成")</span><span class="sxs-lookup"><span data-stu-id="16755-419">![Creating a new Web Site using Quick Create](build-restful-apis-with-aspnet-web-api/_static/image41.png "Creating a new Web Site using Quick Create")</span></span>

    <span data-ttu-id="16755-420">*簡易作成を使用した新しい Web サイトの作成*</span><span class="sxs-lookup"><span data-stu-id="16755-420">*Creating a new Web Site using Quick Create*</span></span>
4. <span data-ttu-id="16755-421">新しい**Web サイト**が作成されるまで待ちます。</span><span class="sxs-lookup"><span data-stu-id="16755-421">Wait until the new **Web Site** is created.</span></span>
5. <span data-ttu-id="16755-422">Web サイトが作成されたら、 **[URL]** 列の下のリンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="16755-422">Once the Web Site is created click the link under the **URL** column.</span></span> <span data-ttu-id="16755-423">新しい Web サイトが機能していることを確認します。</span><span class="sxs-lookup"><span data-stu-id="16755-423">Check that the new Web Site is working.</span></span>

    <span data-ttu-id="16755-424">![新しい web サイトを参照しています](build-restful-apis-with-aspnet-web-api/_static/image42.png "新しい web サイトを参照しています")</span><span class="sxs-lookup"><span data-stu-id="16755-424">![Browsing to the new web site](build-restful-apis-with-aspnet-web-api/_static/image42.png "Browsing to the new web site")</span></span>

    <span data-ttu-id="16755-425">*新しい web サイトを参照しています*</span><span class="sxs-lookup"><span data-stu-id="16755-425">*Browsing to the new web site*</span></span>

    <span data-ttu-id="16755-426">![実行中の Web サイト](build-restful-apis-with-aspnet-web-api/_static/image43.png "実行中の Web サイト")</span><span class="sxs-lookup"><span data-stu-id="16755-426">![Web site running](build-restful-apis-with-aspnet-web-api/_static/image43.png "Web site running")</span></span>

    <span data-ttu-id="16755-427">*実行中の Web サイト*</span><span class="sxs-lookup"><span data-stu-id="16755-427">*Web site running*</span></span>
6. <span data-ttu-id="16755-428">ポータルに戻り、 **[名前]** 列の下にある web サイトの名前をクリックして、管理ページを表示します。</span><span class="sxs-lookup"><span data-stu-id="16755-428">Go back to the portal and click the name of the web site under the **Name** column to display the management pages.</span></span>

    <span data-ttu-id="16755-429">![Web サイトの管理ページを開く](build-restful-apis-with-aspnet-web-api/_static/image44.png "Web サイトの管理ページを開く")</span><span class="sxs-lookup"><span data-stu-id="16755-429">![Opening the web site management pages](build-restful-apis-with-aspnet-web-api/_static/image44.png "Opening the web site management pages")</span></span>

    <span data-ttu-id="16755-430">*Web サイトの管理ページを開く*</span><span class="sxs-lookup"><span data-stu-id="16755-430">*Opening the Web Site management pages*</span></span>
7. <span data-ttu-id="16755-431">**[ダッシュボード]** ページの **[概要] セクションで**、 **[発行プロファイルのダウンロード]** リンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="16755-431">In the **Dashboard** page, under the **quick glance** section, click the **Download publish profile** link.</span></span>

    > [!NOTE]
    > <span data-ttu-id="16755-432">*発行プロファイル*には、有効になっている各発行方法について、Azure に web アプリケーションを発行するために必要なすべての情報が含まれています。</span><span class="sxs-lookup"><span data-stu-id="16755-432">The *publish profile* contains all of the information required to publish a web application to a Azure for each enabled publication method.</span></span> <span data-ttu-id="16755-433">発行プロファイルには、発行メソッドが有効化される各エンドポイントに接続して認証するために必要な URL、ユーザーの資格情報、およびデータベース文字列が含まれています。</span><span class="sxs-lookup"><span data-stu-id="16755-433">The publish profile contains the URLs, user credentials and database strings required to connect to and authenticate against each of the endpoints for which a publication method is enabled.</span></span> <span data-ttu-id="16755-434">**Microsoft WebMatrix 2**、 **Microsoft Visual Studio Express for Web**および**Microsoft Visual Studio 2012**では、発行プロファイルを読み取り、Web アプリケーションを Azure に発行するためのこれらのプログラムの構成を自動化することがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="16755-434">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** and **Microsoft Visual Studio 2012** support reading publish profiles to automate configuration of these programs for publishing web applications to Azure.</span></span>

    <span data-ttu-id="16755-435">![Web サイト発行プロファイルをダウンロードしています](build-restful-apis-with-aspnet-web-api/_static/image45.png "Web サイト発行プロファイルをダウンロードしています")</span><span class="sxs-lookup"><span data-stu-id="16755-435">![Downloading the web site publish profile](build-restful-apis-with-aspnet-web-api/_static/image45.png "Downloading the web site publish profile")</span></span>

    <span data-ttu-id="16755-436">*Web サイト発行プロファイルをダウンロードしています*</span><span class="sxs-lookup"><span data-stu-id="16755-436">*Downloading the Web Site publish profile*</span></span>
8. <span data-ttu-id="16755-437">発行プロファイルファイルを既知の場所にダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="16755-437">Download the publish profile file to a known location.</span></span> <span data-ttu-id="16755-438">この演習では、このファイルを使用して Visual Studio から Azure に web アプリケーションを発行する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="16755-438">Further in this exercise you will see how to use this file to publish a web application to Azure from Visual Studio.</span></span>

    <span data-ttu-id="16755-439">![発行プロファイルファイルを保存しています](build-restful-apis-with-aspnet-web-api/_static/image46.png "発行プロファイルを保存しています")</span><span class="sxs-lookup"><span data-stu-id="16755-439">![Saving the publish profile file](build-restful-apis-with-aspnet-web-api/_static/image46.png "Saving the publish profile")</span></span>

    <span data-ttu-id="16755-440">*発行プロファイルファイルを保存しています*</span><span class="sxs-lookup"><span data-stu-id="16755-440">*Saving the publish profile file*</span></span>

<a id="ApxCTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a><span data-ttu-id="16755-441">タスク 2-データベースサーバーの構成</span><span class="sxs-lookup"><span data-stu-id="16755-441">Task 2 - Configuring the Database Server</span></span>

<span data-ttu-id="16755-442">アプリケーションで SQL Server データベースを使用する場合は、SQL Database サーバーを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="16755-442">If your application makes use of SQL Server databases you will need to create a SQL Database server.</span></span> <span data-ttu-id="16755-443">SQL Server を使用しない単純なアプリケーションを展開する場合は、このタスクを省略できます。</span><span class="sxs-lookup"><span data-stu-id="16755-443">If you want to deploy a simple application that does not use SQL Server you might skip this task.</span></span>

1. <span data-ttu-id="16755-444">アプリケーションデータベースを格納するには、SQL Database サーバーが必要です。</span><span class="sxs-lookup"><span data-stu-id="16755-444">You will need a SQL Database server for storing the application database.</span></span> <span data-ttu-id="16755-445">Azure 管理ポータルのサブスクリプションから**SQL Database サーバーを**表示するには、 **SQL データベース** | サーバー | **サーバーのダッシュボード**を参照してください。</span><span class="sxs-lookup"><span data-stu-id="16755-445">You can view the SQL Database servers from your subscription in the Azure Management portal at **Sql Databases** | **Servers** | **Server's Dashboard**.</span></span> <span data-ttu-id="16755-446">サーバーを作成していない場合は、コマンドバーの **[追加]** ボタンを使用して作成できます。</span><span class="sxs-lookup"><span data-stu-id="16755-446">If you do not have a server created, you can create one using the **Add** button on the command bar.</span></span> <span data-ttu-id="16755-447">次のタスクで使用するので、**サーバー名と URL、管理者のログイン名、パスワード**をメモしておきます。</span><span class="sxs-lookup"><span data-stu-id="16755-447">Take note of the **server name and URL, administrator login name and password**, as you will use them in the next tasks.</span></span> <span data-ttu-id="16755-448">データベースは、後の段階で作成されるため、まだ作成しないでください。</span><span class="sxs-lookup"><span data-stu-id="16755-448">Do not create the database yet, as it will be created in a later stage.</span></span>

    <span data-ttu-id="16755-449">![SQL Database サーバーダッシュボード](build-restful-apis-with-aspnet-web-api/_static/image47.png "SQL Database サーバーダッシュボード")</span><span class="sxs-lookup"><span data-stu-id="16755-449">![SQL Database Server Dashboard](build-restful-apis-with-aspnet-web-api/_static/image47.png "SQL Database Server Dashboard")</span></span>

    <span data-ttu-id="16755-450">*SQL Database サーバーダッシュボード*</span><span class="sxs-lookup"><span data-stu-id="16755-450">*SQL Database Server Dashboard*</span></span>
2. <span data-ttu-id="16755-451">次のタスクでは、Visual Studio からデータベース接続をテストします。そのため、**使用可能な Ip アドレス**の一覧にローカル ip アドレスを含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="16755-451">In the next task you will test the database connection from Visual Studio, for that reason you need to include your local IP address in the server's list of **Allowed IP Addresses**.</span></span> <span data-ttu-id="16755-452">これを行うには、 **[構成]** をクリックし、 **[現在のクライアント IP アドレス]** の ip アドレスを選択して、 **[開始 Ip アドレス]** と **[終了 ip アドレス]** のテキストボックスに貼り付け、[![の](build-restful-apis-with-aspnet-web-api/_static/image48.png) 追加] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="16755-452">To do that, click **Configure**, select the IP address from **Current Client IP Address** and paste it on the **Start IP Address** and **End IP Address** text boxes and click the ![add-client-ip-address-ok-button](build-restful-apis-with-aspnet-web-api/_static/image48.png) button.</span></span>

    ![クライアント IP アドレスを追加しています](build-restful-apis-with-aspnet-web-api/_static/image49.png)

    <span data-ttu-id="16755-454">*クライアント IP アドレスを追加しています*</span><span class="sxs-lookup"><span data-stu-id="16755-454">*Adding Client IP Address*</span></span>
3. <span data-ttu-id="16755-455">[許可された IP アドレス] の一覧に**クライアントの Ip アドレス**が追加されたら、 **[保存]** をクリックして変更を確認します。</span><span class="sxs-lookup"><span data-stu-id="16755-455">Once the **Client IP Address** is added to the allowed IP addresses list, click on **Save** to confirm the changes.</span></span>

    ![変更の確認](build-restful-apis-with-aspnet-web-api/_static/image50.png)

    <span data-ttu-id="16755-457">*変更の確認*</span><span class="sxs-lookup"><span data-stu-id="16755-457">*Confirm Changes*</span></span>

<a id="ApxCTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="16755-458">タスク 3-Web 配置を使用した ASP.NET MVC 4 アプリケーションの発行</span><span class="sxs-lookup"><span data-stu-id="16755-458">Task 3 - Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

1. <span data-ttu-id="16755-459">ASP.NET MVC 4 ソリューションに戻ります。</span><span class="sxs-lookup"><span data-stu-id="16755-459">Go back to the ASP.NET MVC 4 solution.</span></span> <span data-ttu-id="16755-460">**ソリューションエクスプローラー**で、web サイトプロジェクトを右クリックし、 **[発行]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="16755-460">In the **Solution Explorer**, right-click the web site project and select **Publish**.</span></span>

    <span data-ttu-id="16755-461">![アプリケーションの発行](build-restful-apis-with-aspnet-web-api/_static/image51.png "アプリケーションの発行")</span><span class="sxs-lookup"><span data-stu-id="16755-461">![Publishing the Application](build-restful-apis-with-aspnet-web-api/_static/image51.png "Publishing the Application")</span></span>

    <span data-ttu-id="16755-462">*Web サイトの公開*</span><span class="sxs-lookup"><span data-stu-id="16755-462">*Publishing the web site*</span></span>
2. <span data-ttu-id="16755-463">最初のタスクで保存した発行プロファイルをインポートします。</span><span class="sxs-lookup"><span data-stu-id="16755-463">Import the publish profile you saved in the first task.</span></span>

    <span data-ttu-id="16755-464">![発行プロファイルをインポートしています](build-restful-apis-with-aspnet-web-api/_static/image52.png "発行プロファイルをインポートしています")</span><span class="sxs-lookup"><span data-stu-id="16755-464">![Importing the publish profile](build-restful-apis-with-aspnet-web-api/_static/image52.png "Importing the publish profile")</span></span>

    <span data-ttu-id="16755-465">*発行プロファイルをインポートしています*</span><span class="sxs-lookup"><span data-stu-id="16755-465">*Importing publish profile*</span></span>
3. <span data-ttu-id="16755-466">**[接続の検証]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="16755-466">Click **Validate Connection**.</span></span> <span data-ttu-id="16755-467">検証が完了したら、 **[次へ]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="16755-467">Once Validation is complete click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="16755-468">検証が完了すると、[接続の検証] ボタンの横に緑色のチェックマークが表示されます。</span><span class="sxs-lookup"><span data-stu-id="16755-468">Validation is complete once you see a green checkmark appear next to the Validate Connection button.</span></span>

    <span data-ttu-id="16755-469">![接続の検証](build-restful-apis-with-aspnet-web-api/_static/image53.png "接続の検証")</span><span class="sxs-lookup"><span data-stu-id="16755-469">![Validating connection](build-restful-apis-with-aspnet-web-api/_static/image53.png "Validating connection")</span></span>

    <span data-ttu-id="16755-470">*接続の検証*</span><span class="sxs-lookup"><span data-stu-id="16755-470">*Validating connection*</span></span>
4. <span data-ttu-id="16755-471">**[設定]** ページの **[データベース]** セクションで、データベース接続のテキストボックスの横にあるボタン ( **defaultconnection**など) をクリックします。</span><span class="sxs-lookup"><span data-stu-id="16755-471">In the **Settings** page, under the **Databases** section, click the button next to your database connection's textbox (i.e. **DefaultConnection**).</span></span>

    <span data-ttu-id="16755-472">![Web deploy の構成](build-restful-apis-with-aspnet-web-api/_static/image54.png "Web deploy の構成")</span><span class="sxs-lookup"><span data-stu-id="16755-472">![Web deploy configuration](build-restful-apis-with-aspnet-web-api/_static/image54.png "Web deploy configuration")</span></span>

    <span data-ttu-id="16755-473">*Web deploy の構成*</span><span class="sxs-lookup"><span data-stu-id="16755-473">*Web deploy configuration*</span></span>
5. <span data-ttu-id="16755-474">次のようにデータベース接続を構成します。</span><span class="sxs-lookup"><span data-stu-id="16755-474">Configure the database connection as follows:</span></span>

   - <span data-ttu-id="16755-475">**サーバー名**には、 *tcp:* プレフィックスを使用して SQL Database サーバーの URL を入力します。</span><span class="sxs-lookup"><span data-stu-id="16755-475">In the **Server name** type your SQL Database server URL using the *tcp:* prefix.</span></span>
   - <span data-ttu-id="16755-476">**User name (ユーザー名**) に、サーバー管理者のログイン名を入力します。</span><span class="sxs-lookup"><span data-stu-id="16755-476">In **User name** type your server administrator login name.</span></span>
   - <span data-ttu-id="16755-477">**パスワード**で、サーバー管理者のログインパスワードを入力します。</span><span class="sxs-lookup"><span data-stu-id="16755-477">In **Password** type your server administrator login password.</span></span>
   - <span data-ttu-id="16755-478">新しいデータベース名を入力します (例: *MVC4SampleDB*)。</span><span class="sxs-lookup"><span data-stu-id="16755-478">Type a new database name, for example: *MVC4SampleDB*.</span></span>

     <span data-ttu-id="16755-479">![変換先の接続文字列を構成しています](build-restful-apis-with-aspnet-web-api/_static/image55.png "変換先の接続文字列を構成しています")</span><span class="sxs-lookup"><span data-stu-id="16755-479">![Configuring destination connection string](build-restful-apis-with-aspnet-web-api/_static/image55.png "Configuring destination connection string")</span></span>

     <span data-ttu-id="16755-480">*変換先の接続文字列を構成しています*</span><span class="sxs-lookup"><span data-stu-id="16755-480">*Configuring destination connection string*</span></span>
6. <span data-ttu-id="16755-481">次に、 **[OK]** をクリックします</span><span class="sxs-lookup"><span data-stu-id="16755-481">Then click **OK**.</span></span> <span data-ttu-id="16755-482">データベースの作成を求めるメッセージが表示されたら、[**はい]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="16755-482">When prompted to create the database click **Yes**.</span></span>

    <span data-ttu-id="16755-483">![データベースの作成](build-restful-apis-with-aspnet-web-api/_static/image56.png "データベース文字列の作成")</span><span class="sxs-lookup"><span data-stu-id="16755-483">![Creating the database](build-restful-apis-with-aspnet-web-api/_static/image56.png "Creating the database string")</span></span>

    <span data-ttu-id="16755-484">*データベースの作成*</span><span class="sxs-lookup"><span data-stu-id="16755-484">*Creating the database*</span></span>
7. <span data-ttu-id="16755-485">Windows Azure の SQL Database に接続するために使用する接続文字列は、[既定の接続] ボックスに表示されます。</span><span class="sxs-lookup"><span data-stu-id="16755-485">The connection string you will use to connect to SQL Database in Windows Azure is shown within Default Connection textbox.</span></span> <span data-ttu-id="16755-486">続けて、 **[次へ]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="16755-486">Then click **Next**.</span></span>

    <span data-ttu-id="16755-487">![SQL Database を指す接続文字列](build-restful-apis-with-aspnet-web-api/_static/image57.png "SQL Database を指す接続文字列")</span><span class="sxs-lookup"><span data-stu-id="16755-487">![Connection string pointing to SQL Database](build-restful-apis-with-aspnet-web-api/_static/image57.png "Connection string pointing to SQL Database")</span></span>

    <span data-ttu-id="16755-488">*SQL Database を指す接続文字列*</span><span class="sxs-lookup"><span data-stu-id="16755-488">*Connection string pointing to SQL Database*</span></span>
8. <span data-ttu-id="16755-489">**[プレビュー]** ページで、 **[発行]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="16755-489">In the **Preview** page, click **Publish**.</span></span>

    <span data-ttu-id="16755-490">![Web アプリケーションの発行](build-restful-apis-with-aspnet-web-api/_static/image58.png "Web アプリケーションの発行")</span><span class="sxs-lookup"><span data-stu-id="16755-490">![Publishing the web application](build-restful-apis-with-aspnet-web-api/_static/image58.png "Publishing the web application")</span></span>

    <span data-ttu-id="16755-491">*Web アプリケーションの発行*</span><span class="sxs-lookup"><span data-stu-id="16755-491">*Publishing the web application*</span></span>
9. <span data-ttu-id="16755-492">発行プロセスが完了すると、既定のブラウザーによって公開された web サイトが開きます。</span><span class="sxs-lookup"><span data-stu-id="16755-492">Once the publishing process finishes, your default browser will open the published web site.</span></span>

    <span data-ttu-id="16755-493">![Windows Azure に発行されたアプリケーション](build-restful-apis-with-aspnet-web-api/_static/image59.png "Windows Azure に発行されたアプリケーション")</span><span class="sxs-lookup"><span data-stu-id="16755-493">![Application published to Windows Azure](build-restful-apis-with-aspnet-web-api/_static/image59.png "Application published to Windows Azure")</span></span>

    <span data-ttu-id="16755-494">*Azure に発行されたアプリケーション*</span><span class="sxs-lookup"><span data-stu-id="16755-494">*Application published to Azure*</span></span>
