---
uid: web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs
title: 'ハンズオンラボ: ASP.NET Web API と ASP.NET 4.x を使用して単一ページアプリケーション (SPA) を構築する'
author: rick-anderson
description: 'ステップバイステップコード: ASP.NET 4.x 用の ASP.NET Web API とを使用して単一ページアプリケーション (SPA) をビルドします。'
ms.author: riande
ms.date: 09/30/2015
ms.custom: seoapril2019
ms.assetid: 719727b7-bef3-45ad-bfe9-ba5bcdb2305f
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs
msc.type: authoredcontent
ms.openlocfilehash: 86833a890da759e489dd11dc9afb128a9b7a75e3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448762"
---
# <a name="hands-on-lab-build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs"></a><span data-ttu-id="c925d-103">ハンズオンラボ: ASP.NET Web API と角速度を使用してシングルページアプリケーション (SPA) を構築する</span><span class="sxs-lookup"><span data-stu-id="c925d-103">Hands On Lab: Build a Single Page Application (SPA) with ASP.NET Web API and Angular.js</span></span>

<span data-ttu-id="c925d-104">[Web キャンプチーム](https://twitter.com/webcamps)別</span><span class="sxs-lookup"><span data-stu-id="c925d-104">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="c925d-105">Web キャンプトレーニングキットをダウンロードする</span><span class="sxs-lookup"><span data-stu-id="c925d-105">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

<span data-ttu-id="c925d-106">このハンズオンラボでは、ASP.NET 4.x 用の ASP.NET Web API とを使用してシングルページアプリケーション (SPA) を構築する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="c925d-106">This hands on lab shows you how to build a Single Page Application (SPA) with ASP.NET Web API and Angular.js for ASP.NET 4.x.</span></span>

<span data-ttu-id="c925d-107">このラボでは、これらのテクノロジを利用して、SPA の概念に基づくトリビア web サイトであるマニアクイズを実装します。</span><span class="sxs-lookup"><span data-stu-id="c925d-107">In this hand-on lab, you will take advantage of those technologies to implement Geek Quiz, a trivia website based on the SPA concept.</span></span> <span data-ttu-id="c925d-108">まず、ASP.NET Web API を使用してサービス層を実装し、クイズの質問を取得して回答を格納するために必要なエンドポイントを公開します。</span><span class="sxs-lookup"><span data-stu-id="c925d-108">You will first implement the service layer with ASP.NET Web API to expose the required endpoints to retrieve the quiz questions and store the answers.</span></span> <span data-ttu-id="c925d-109">次に、AngularJS および CSS3 変換効果を使用して、優れた応答性の高い UI を構築します。</span><span class="sxs-lookup"><span data-stu-id="c925d-109">Then, you will build a rich and responsive UI using AngularJS and CSS3 transformation effects.</span></span>

<span data-ttu-id="c925d-110">従来の web アプリケーションでは、クライアント (ブラウザー) がページを要求することによってサーバーとの通信を開始します。</span><span class="sxs-lookup"><span data-stu-id="c925d-110">In traditional web applications, the client (browser) initiates the communication with the server by requesting a page.</span></span> <span data-ttu-id="c925d-111">次に、サーバーが要求を処理し、ページの HTML をクライアントに送信します。</span><span class="sxs-lookup"><span data-stu-id="c925d-111">The server then processes the request and sends the HTML of the page to the client.</span></span> <span data-ttu-id="c925d-112">このページとの後続の操作 (ユーザーがリンクに移動したり、データでフォームを送信したりする場合など) では、新しい要求がサーバーに送信され、フローが再び開始されます。サーバーが要求を処理し、新しいページを新しいアクション要求への応答としてブラウザーに送信します。クライアントによる ed。</span><span class="sxs-lookup"><span data-stu-id="c925d-112">In subsequent interactions with the page –e.g. the user navigates to a link or submits a form with data– a new request is sent to the server, and the flow starts again: the server processes the request and sends a new page to the browser in response to the new action requested by the client.</span></span>
> 
> <span data-ttu-id="c925d-113">シングルページアプリケーション (spa) では、最初の要求の後にページ全体がブラウザーに読み込まれますが、それ以降の対話は Ajax 要求によって行われます。</span><span class="sxs-lookup"><span data-stu-id="c925d-113">In Single-Page Applications (SPAs) the entire page is loaded in the browser after the initial request, but subsequent interactions take place through Ajax requests.</span></span> <span data-ttu-id="c925d-114">これは、ブラウザーが変更されたページの部分のみを更新する必要があることを意味します。ページ全体を再読み込みする必要はありません。</span><span class="sxs-lookup"><span data-stu-id="c925d-114">This means that the browser has to update only the portion of the page that has changed; there is no need to reload the entire page.</span></span> <span data-ttu-id="c925d-115">SPA アプローチを使用すると、アプリケーションがユーザーの操作に応答するためにかかる時間が短縮され、より滑らかなエクスペリエンスが得られます。</span><span class="sxs-lookup"><span data-stu-id="c925d-115">The SPA approach reduces the time taken by the application to respond to user actions, resulting in a more fluid experience.</span></span>
> 
> <span data-ttu-id="c925d-116">SPA のアーキテクチャには、従来の web アプリケーションには存在しない特定の課題が伴います。</span><span class="sxs-lookup"><span data-stu-id="c925d-116">The architecture of a SPA involves certain challenges that are not present in traditional web applications.</span></span> <span data-ttu-id="c925d-117">ただし、ASP.NET Web API などの新しいテクノロジや、CSS3 によって提供される新しいスタイル機能などの JavaScript フレームワークにより、SPAs の設計とビルドが非常に簡単になります。</span><span class="sxs-lookup"><span data-stu-id="c925d-117">However, emerging technologies like ASP.NET Web API, JavaScript frameworks like AngularJS and new styling features provided by CSS3 make it really easy to design and build SPAs.</span></span>
> 
> 
> <span data-ttu-id="c925d-118">すべてのサンプルコードとスニペットは、 [https://aka.ms/webcamps-training-kit](https://aka.ms/webcamps-training-kit)で入手できる Web キャンプトレーニングキットに含まれています。</span><span class="sxs-lookup"><span data-stu-id="c925d-118">All sample code and snippets are included in the Web Camps Training Kit, available at [https://aka.ms/webcamps-training-kit](https://aka.ms/webcamps-training-kit).</span></span>

## <a name="overview"></a><span data-ttu-id="c925d-119">概要</span><span class="sxs-lookup"><span data-stu-id="c925d-119">Overview</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="c925d-120">目標</span><span class="sxs-lookup"><span data-stu-id="c925d-120">Objectives</span></span>

<span data-ttu-id="c925d-121">このハンズオンラボでは、次の方法を学習します。</span><span class="sxs-lookup"><span data-stu-id="c925d-121">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="c925d-122">JSON データを送受信するための ASP.NET Web API サービスを作成する</span><span class="sxs-lookup"><span data-stu-id="c925d-122">Create an ASP.NET Web API service to send and receive JSON data</span></span>
- <span data-ttu-id="c925d-123">AngularJS を使用して応答性の高い UI を作成する</span><span class="sxs-lookup"><span data-stu-id="c925d-123">Create a responsive UI using AngularJS</span></span>
- <span data-ttu-id="c925d-124">CSS3 変換による UI エクスペリエンスの向上</span><span class="sxs-lookup"><span data-stu-id="c925d-124">Enhance the UI experience with CSS3 transformations</span></span>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="c925d-125">前提条件</span><span class="sxs-lookup"><span data-stu-id="c925d-125">Prerequisites</span></span>

<span data-ttu-id="c925d-126">このハンズオンラボを完了するには、次のものが必要です。</span><span class="sxs-lookup"><span data-stu-id="c925d-126">The following is required to complete this hands-on lab:</span></span>

- <span data-ttu-id="c925d-127">[Web 用に2013を Visual Studio Express](https://www.microsoft.com/visualstudio/)</span><span class="sxs-lookup"><span data-stu-id="c925d-127">[Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/) or greater</span></span>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="c925d-128">セットアップ</span><span class="sxs-lookup"><span data-stu-id="c925d-128">Setup</span></span>

<span data-ttu-id="c925d-129">このハンズオンラボの演習を実行するには、まず環境をセットアップする必要があります。</span><span class="sxs-lookup"><span data-stu-id="c925d-129">In order to run the exercises in this hands-on lab, you will need to set up your environment first.</span></span>

1. <span data-ttu-id="c925d-130">エクスプローラーを開き、ラボの**ソース**フォルダーを参照します。</span><span class="sxs-lookup"><span data-stu-id="c925d-130">Open Windows Explorer and browse to the lab's **Source** folder.</span></span>
2. <span data-ttu-id="c925d-131">**Setup.exe**を右クリックし、 **[管理者として実行]** を選択して、環境を構成し、このラボ用の Visual Studio コードスニペットをインストールするセットアッププロセスを開始します。</span><span class="sxs-lookup"><span data-stu-id="c925d-131">Right-click on **Setup.cmd** and select **Run as administrator** to launch the setup process that will configure your environment and install the Visual Studio code snippets for this lab.</span></span>
3. <span data-ttu-id="c925d-132">ユーザー アカウント制御ダイアログ ボックスが表示されている場合は、続行するアクションを確認します。</span><span class="sxs-lookup"><span data-stu-id="c925d-132">If the User Account Control dialog box is shown, confirm the action to proceed.</span></span>

> [!NOTE]
> <span data-ttu-id="c925d-133">セットアップを実行する前に、このラボのすべての依存関係を確認していることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="c925d-133">Make sure you have checked all the dependencies for this lab before running the setup.</span></span>

<a id="CodeSnippets"></a>
### <a name="using-the-code-snippets"></a><span data-ttu-id="c925d-134">コードスニペットの使用</span><span class="sxs-lookup"><span data-stu-id="c925d-134">Using the Code Snippets</span></span>

<span data-ttu-id="c925d-135">ラボドキュメント全体で、コードブロックを挿入するように指示されます。</span><span class="sxs-lookup"><span data-stu-id="c925d-135">Throughout the lab document, you will be instructed to insert code blocks.</span></span> <span data-ttu-id="c925d-136">便宜上、このコードのほとんどは Visual Studio Code のスニペットとして提供されており、Visual Studio 2013 内からアクセスして、手動で追加する必要がないようにすることができます。</span><span class="sxs-lookup"><span data-stu-id="c925d-136">For your convenience, most of this code is provided as Visual Studio Code Snippets, which you can access from within Visual Studio 2013 to avoid having to add it manually.</span></span>

> [!NOTE]
> <span data-ttu-id="c925d-137">各演習には、演習の**Begin**フォルダーに配置された開始ソリューションが付属しています。これにより、各演習を別の手順に従って実行することができます。</span><span class="sxs-lookup"><span data-stu-id="c925d-137">Each exercise is accompanied by a starting solution located in the **Begin** folder of the exercise that allows you to follow each exercise independently of the others.</span></span> <span data-ttu-id="c925d-138">演習中に追加されたコードスニペットは、これらの開始ソリューションにはないため、演習を完了するまで機能しないことがあります。</span><span class="sxs-lookup"><span data-stu-id="c925d-138">Please be aware that the code snippets that are added during an exercise are missing from these starting solutions and may not work until you have completed the exercise.</span></span> <span data-ttu-id="c925d-139">演習用のソースコード内では、対応する演習の手順を完了した結果として得られるコードを使用して、Visual Studio ソリューションを含む**終了**フォルダーも検索します。</span><span class="sxs-lookup"><span data-stu-id="c925d-139">Inside the source code for an exercise, you will also find an **End** folder containing a Visual Studio solution with the code that results from completing the steps in the corresponding exercise.</span></span> <span data-ttu-id="c925d-140">このハンズオンラボを使用して作業する際に、追加のヘルプが必要な場合は、これらのソリューションをガイダンスとして使用できます。</span><span class="sxs-lookup"><span data-stu-id="c925d-140">You can use these solutions as guidance if you need additional help as you work through this hands-on lab.</span></span>

---

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="c925d-141">手順</span><span class="sxs-lookup"><span data-stu-id="c925d-141">Exercises</span></span>

<span data-ttu-id="c925d-142">このハンズオンラボには、次の演習が含まれています。</span><span class="sxs-lookup"><span data-stu-id="c925d-142">This hands-on lab includes the following exercises:</span></span>

1. [<span data-ttu-id="c925d-143">Web API の作成</span><span class="sxs-lookup"><span data-stu-id="c925d-143">Creating a Web API</span></span>](#Exercise1)
2. [<span data-ttu-id="c925d-144">SPA インターフェイスの作成</span><span class="sxs-lookup"><span data-stu-id="c925d-144">Creating a SPA Interface</span></span>](#Exercise2)

<span data-ttu-id="c925d-145">このラボの推定所要時間: **60 分**</span><span class="sxs-lookup"><span data-stu-id="c925d-145">Estimated time to complete this lab: **60 minutes**</span></span>

> [!NOTE]
> <span data-ttu-id="c925d-146">Visual Studio を初めて起動するときに、定義済みの設定コレクションのいずれかを選択する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c925d-146">When you first start Visual Studio, you must select one of the predefined settings collections.</span></span> <span data-ttu-id="c925d-147">定義済みの各コレクションは、特定の開発スタイルに一致するように設計されており、ウィンドウのレイアウト、エディターの動作、IntelliSense コードスニペット、およびダイアログボックスのオプションを決定します。</span><span class="sxs-lookup"><span data-stu-id="c925d-147">Each predefined collection is designed to match a particular development style and determines window layouts, editor behavior, IntelliSense code snippets, and dialog box options.</span></span> <span data-ttu-id="c925d-148">このラボの手順では、**全般的な開発設定**のコレクションを使用するときに、Visual Studio で特定のタスクを実行するために必要なアクションについて説明します。</span><span class="sxs-lookup"><span data-stu-id="c925d-148">The procedures in this lab describe the actions necessary to accomplish a given task in Visual Studio when using the **General Development Settings** collection.</span></span> <span data-ttu-id="c925d-149">開発環境に対して別の設定コレクションを選択した場合は、注意が必要な手順が異なる場合があります。</span><span class="sxs-lookup"><span data-stu-id="c925d-149">If you choose a different settings collection for your development environment, there may be differences in the steps that you should take into account.</span></span>

<a id="Exercise1"></a>
### <a name="exercise-1-creating-a-web-api"></a><span data-ttu-id="c925d-150">演習 1: Web API の作成</span><span class="sxs-lookup"><span data-stu-id="c925d-150">Exercise 1: Creating a Web API</span></span>

<span data-ttu-id="c925d-151">SPA の重要な部分の1つは、サービス層です。</span><span class="sxs-lookup"><span data-stu-id="c925d-151">One of the key parts of a SPA is the service layer.</span></span> <span data-ttu-id="c925d-152">これは、UI によって送信された Ajax 呼び出しを処理し、その呼び出しに応答してデータを返す役割を担います。</span><span class="sxs-lookup"><span data-stu-id="c925d-152">It is responsible for processing the Ajax calls sent by the UI and returning data in response to that call.</span></span> <span data-ttu-id="c925d-153">取得したデータは、クライアントによって解析および使用されるために、コンピューターが判読できる形式で表示される必要があります。</span><span class="sxs-lookup"><span data-stu-id="c925d-153">The data retrieved should be presented in a machine-readable format in order to be parsed and consumed by the client.</span></span>

<span data-ttu-id="c925d-154">Web API フレームワークは ASP.NET スタックの一部であり、HTTP サービスを簡単に実装できるように設計されています。これは、一般に、RESTful API を使用して JSON または XML 形式のデータを送受信します。</span><span class="sxs-lookup"><span data-stu-id="c925d-154">The Web API framework is part of the ASP.NET Stack and is designed to make it easy to implement HTTP services, generally sending and receiving JSON- or XML-formatted data through a RESTful API.</span></span> <span data-ttu-id="c925d-155">この演習では、マニアクイズアプリケーションをホストする Web サイトを作成し、ASP.NET Web API を使用して、クイズデータを公開して永続化するバックエンドサービスを実装します。</span><span class="sxs-lookup"><span data-stu-id="c925d-155">In this exercise you will create the Web site to host the Geek Quiz application and then implement the back-end service to expose and persist the quiz data using ASP.NET Web API.</span></span>

<a id="Ex1Task1"></a>
#### <a name="task-1--creating-the-initial-project-for-geek-quiz"></a><span data-ttu-id="c925d-156">タスク 1-マニアクイズの初期プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="c925d-156">Task 1 – Creating the Initial Project for Geek Quiz</span></span>

<span data-ttu-id="c925d-157">このタスクでは、Visual Studio に付属する**ASP.NET**プロジェクトの種類に基づいて ASP.NET Web API をサポートする新しい ASP.NET MVC プロジェクトの作成を開始します。</span><span class="sxs-lookup"><span data-stu-id="c925d-157">In this task you will start creating a new ASP.NET MVC project with support for ASP.NET Web API based on the **One ASP.NET** project type that comes with Visual Studio.</span></span> <span data-ttu-id="c925d-158">**ASP.NET**は、すべての ASP.NET テクノロジを統合し、必要に応じてそれらを組み合わせて照合するオプションを提供します。</span><span class="sxs-lookup"><span data-stu-id="c925d-158">**One ASP.NET** unifies all ASP.NET technologies and gives you the option to mix and match them as desired.</span></span> <span data-ttu-id="c925d-159">次に、Entity Framework のモデルクラスとデータベース初期化子を追加して、クイズの質問を挿入します。</span><span class="sxs-lookup"><span data-stu-id="c925d-159">You will then add the Entity Framework's model classes and the database initializer to insert the quiz questions.</span></span>

1. <span data-ttu-id="c925d-160">**Web 用 Visual Studio Express 2013**を開き、[ファイル] を選択します。 **新しいプロジェクト...** を実行すると、新しいソリューションが開始されます。</span><span class="sxs-lookup"><span data-stu-id="c925d-160">Open **Visual Studio Express 2013 for Web** and select **File | New Project...** to start a new solution.</span></span>

    <span data-ttu-id="c925d-161">![新しいプロジェクトの作成](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image1.png "新規プロジェクトの作成")</span><span class="sxs-lookup"><span data-stu-id="c925d-161">![Creating a New Project](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image1.png "Creating a New Project")</span></span>

    <span data-ttu-id="c925d-162">*新しいプロジェクトの作成*</span><span class="sxs-lookup"><span data-stu-id="c925d-162">*Creating a New Project*</span></span>
2. <span data-ttu-id="c925d-163">**[新しいプロジェクト]** ダイアログボックスで、Visual  **C# | の下にある [ASP.NET Web Application] を選択します。[Web** ] タブ。 **.NET Framework 4.5**が選択されていることを確認し、 *GeekQuiz*という名前を設定して、**場所**を選択し、 **[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c925d-163">In the **New Project** dialog box, select **ASP.NET Web Application** under the **Visual C# | Web** tab. Make sure **.NET Framework 4.5** is selected, name it *GeekQuiz*, choose a **Location** and click **OK**.</span></span>

    <span data-ttu-id="c925d-164">![新しい ASP.NET Web アプリケーションプロジェクトの作成](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image2.png "新しい ASP.NET Web アプリケーションプロジェクトの作成")</span><span class="sxs-lookup"><span data-stu-id="c925d-164">![Creating a new ASP.NET Web Application project](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image2.png "Creating a new ASP.NET Web Application project")</span></span>

    <span data-ttu-id="c925d-165">*新しい ASP.NET Web アプリケーションプロジェクトの作成*</span><span class="sxs-lookup"><span data-stu-id="c925d-165">*Creating a new ASP.NET Web Application project*</span></span>
3. <span data-ttu-id="c925d-166">**[New ASP.NET プロジェクト]** ダイアログボックスで、 **[MVC]** テンプレートを選択し、 **[Web API]** オプションを選択します。</span><span class="sxs-lookup"><span data-stu-id="c925d-166">In the **New ASP.NET Project** dialog box, select the **MVC** template and select the **Web API** option.</span></span> <span data-ttu-id="c925d-167">また、**認証**オプションが**個々のユーザーアカウント**に設定されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="c925d-167">Also, make sure that the **Authentication** option is set to **Individual User Accounts**.</span></span> <span data-ttu-id="c925d-168">続行するには、 **[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c925d-168">Click **OK** to continue.</span></span>

    ![MVC テンプレートを使用した新しいプロジェクトの作成 (Web API コンポーネントを含む)](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image3.png)

    <span data-ttu-id="c925d-170">*MVC テンプレートを使用した新しいプロジェクトの作成 (Web API コンポーネントを含む)*</span><span class="sxs-lookup"><span data-stu-id="c925d-170">*Creating a new project with the MVC template, including Web API components*</span></span>
4. <span data-ttu-id="c925d-171">**ソリューションエクスプローラー**で、 **GeekQuiz**プロジェクトの **モデル** フォルダーを右クリックし、追加 を選択します。 **既存の項目...** .</span><span class="sxs-lookup"><span data-stu-id="c925d-171">In **Solution Explorer**, right-click the **Models** folder of the **GeekQuiz** project and select **Add | Existing Item...**.</span></span>

    <span data-ttu-id="c925d-172">![既存の項目の追加](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image4.png "既存の項目の追加")</span><span class="sxs-lookup"><span data-stu-id="c925d-172">![Adding an existing item](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image4.png "Adding an existing item")</span></span>

    <span data-ttu-id="c925d-173">*既存の項目の追加*</span><span class="sxs-lookup"><span data-stu-id="c925d-173">*Adding an existing item*</span></span>
5. <span data-ttu-id="c925d-174">**[既存項目の追加]** ダイアログボックスで、 **[ソース/アセット/モデル]** フォルダーに移動し、すべてのファイルを選択します。</span><span class="sxs-lookup"><span data-stu-id="c925d-174">In the **Add Existing Item** dialog box, navigate to the **Source/Assets/Models** folder and select all the files.</span></span> <span data-ttu-id="c925d-175">**[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c925d-175">Click **Add**.</span></span>

    <span data-ttu-id="c925d-176">![モデルアセットの追加](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image5.png "モデルアセットの追加")</span><span class="sxs-lookup"><span data-stu-id="c925d-176">![Adding the model assets](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image5.png "Adding the model assets")</span></span>

    <span data-ttu-id="c925d-177">*モデルアセットの追加*</span><span class="sxs-lookup"><span data-stu-id="c925d-177">*Adding the model assets*</span></span>

    > [!NOTE]
    > <span data-ttu-id="c925d-178">これらのファイルを追加することで、データモデル、Entity Framework のデータベースコンテキスト、マニアクイズアプリケーションのデータベース初期化子を追加します。</span><span class="sxs-lookup"><span data-stu-id="c925d-178">By adding these files, you are adding the data model, the Entity Framework's database context and the database initializer for the Geek Quiz application.</span></span>
    > 
    > <span data-ttu-id="c925d-179">**Entity Framework (EF)** は、リレーショナルストレージスキーマを使用して直接プログラミングするのではなく、概念アプリケーションモデルを使用してプログラミングすることで、データアクセスアプリケーションを作成できる、オブジェクトリレーショナルマッパー (ORM) です。</span><span class="sxs-lookup"><span data-stu-id="c925d-179">**Entity Framework (EF)** is an object-relational mapper (ORM) that enables you to create data access applications by programming with a conceptual application model instead of programming directly using a relational storage schema.</span></span> <span data-ttu-id="c925d-180">Entity Framework の詳細については、[こちら](../../../entity-framework.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c925d-180">You can learn more about Entity Framework [here](../../../entity-framework.md).</span></span>
    > 
    > <span data-ttu-id="c925d-181">追加したクラスの説明を次に示します。</span><span class="sxs-lookup"><span data-stu-id="c925d-181">The following is a description of the classes you just added:</span></span>
    > 
    > - <span data-ttu-id="c925d-182">**TriviaOption:** クイズ質問に関連付けられた1つのオプションを表します。</span><span class="sxs-lookup"><span data-stu-id="c925d-182">**TriviaOption:** represents a single option associated with a quiz question</span></span>
    > - <span data-ttu-id="c925d-183">**TriviaQuestion:** クイズの質問を表し、 **options**プロパティを使用して関連するオプションを公開します。</span><span class="sxs-lookup"><span data-stu-id="c925d-183">**TriviaQuestion:** represents a quiz question and exposes the associated options through the **Options** property</span></span>
    > - <span data-ttu-id="c925d-184">**TriviaAnswer:** クイズの質問への応答としてユーザーが選択したオプションを表します。</span><span class="sxs-lookup"><span data-stu-id="c925d-184">**TriviaAnswer:** represents the option selected by the user in response to a quiz question</span></span>
    > - <span data-ttu-id="c925d-185">**TriviaContext:** マニアクイズアプリケーションの Entity Framework のデータベースコンテキストを表します。</span><span class="sxs-lookup"><span data-stu-id="c925d-185">**TriviaContext:** represents the Entity Framework's database context of the Geek Quiz application.</span></span> <span data-ttu-id="c925d-186">このクラスは、 **Dcontext**から派生し、上で説明したエンティティのコレクションを表す**dbset**プロパティを公開します。</span><span class="sxs-lookup"><span data-stu-id="c925d-186">This class derives from **DContext** and exposes **DbSet** properties that represent collections of the entities described above.</span></span>
    > - <span data-ttu-id="c925d-187">**TriviaDatabaseInitializer:** **Createdatabaseifnotexists**から継承する**TriviaContext**クラスの Entity Framework 初期化子の実装。</span><span class="sxs-lookup"><span data-stu-id="c925d-187">**TriviaDatabaseInitializer:** the implementation of the Entity Framework initializer for the **TriviaContext** class which inherits from **CreateDatabaseIfNotExists**.</span></span> <span data-ttu-id="c925d-188">このクラスの既定の動作では、データベースが存在しない場合にのみデータベースを作成し、 **Seed**メソッドで指定したエンティティを挿入します。</span><span class="sxs-lookup"><span data-stu-id="c925d-188">The default behavior of this class is to create the database only if it does not exist, inserting the entities specified in the **Seed** method.</span></span>
6. <span data-ttu-id="c925d-189">**Global.asax.cs**ファイルを開き、次の using ステートメントを追加します。</span><span class="sxs-lookup"><span data-stu-id="c925d-189">Open the **Global.asax.cs** file and add the following using statement.</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample1.cs)]
7. <span data-ttu-id="c925d-190">**Application\_Start**メソッドの先頭に次のコードを追加して、データベース初期化子として**TriviaDatabaseInitializer**を設定します。</span><span class="sxs-lookup"><span data-stu-id="c925d-190">Add the following code at the beginning of the **Application\_Start** method to set the **TriviaDatabaseInitializer** as the database initializer.</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample2.cs)]
8. <span data-ttu-id="c925d-191">認証されたユーザーへのアクセスを制限するように**Home**コントローラーを変更します。</span><span class="sxs-lookup"><span data-stu-id="c925d-191">Modify the **Home** controller to restrict access to authenticated users.</span></span> <span data-ttu-id="c925d-192">これを行うには、 **Controllers**フォルダー内の**HomeController.cs**ファイルを開き、 **HomeController**クラス定義に**承認**属性を追加します。</span><span class="sxs-lookup"><span data-stu-id="c925d-192">To do this, open the **HomeController.cs** file inside the **Controllers** folder and add the **Authorize** attribute to the **HomeController** class definition.</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample3.cs)]

    > [!NOTE]
    > <span data-ttu-id="c925d-193">**承認**フィルターは、ユーザーが認証されているかどうかを確認します。</span><span class="sxs-lookup"><span data-stu-id="c925d-193">The **Authorize** filter checks to see if the user is authenticated.</span></span> <span data-ttu-id="c925d-194">ユーザーが認証されていない場合は、アクションを呼び出さずに HTTP 状態コード 401 (未承認) が返されます。</span><span class="sxs-lookup"><span data-stu-id="c925d-194">If the user is not authenticated, it returns HTTP status code 401 (Unauthorized) without invoking the action.</span></span> <span data-ttu-id="c925d-195">フィルターは、グローバルに、コントローラーレベルで、または個々のアクションのレベルで適用できます。</span><span class="sxs-lookup"><span data-stu-id="c925d-195">You can apply the filter globally, at the controller level, or at the level of individual actions.</span></span>
9. <span data-ttu-id="c925d-196">ここでは、web ページとブランドのレイアウトをカスタマイズします。</span><span class="sxs-lookup"><span data-stu-id="c925d-196">You will now customize the layout of the web pages and the branding.</span></span> <span data-ttu-id="c925d-197">これを行うには、ビュー内で **\_Layout**ファイルを開きます。 *ASP.NET アプリケーション*を*マニアクイズ*に置き換えることによって、 **&lt;title&gt;** 要素の内容を共有フォルダーに更新します。</span><span class="sxs-lookup"><span data-stu-id="c925d-197">To do this, open the **\_Layout.cshtml** file inside the **Views | Shared** folder and update the content of the **&lt;title&gt;** element by replacing *My ASP.NET Application* with *Geek Quiz*.</span></span>

    [!code-cshtml[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample4.cshtml)]
10. <span data-ttu-id="c925d-198">同じファイルで、 *About*リンクと*Contact*リンクを削除し、*ホーム*リンクの名前を*Play*に変更して、ナビゲーションバーを更新します。</span><span class="sxs-lookup"><span data-stu-id="c925d-198">In the same file, update the navigation bar by removing the *About* and *Contact* links and renaming the *Home* link to *Play*.</span></span> <span data-ttu-id="c925d-199">また、[*アプリケーション名*] リンクの名前を「*マニアクイズ*」に変更します。</span><span class="sxs-lookup"><span data-stu-id="c925d-199">Additionally, rename the *Application name* link to *Geek Quiz*.</span></span> <span data-ttu-id="c925d-200">ナビゲーションバーの HTML は、次のコードのようになります。</span><span class="sxs-lookup"><span data-stu-id="c925d-200">The HTML for the navigation bar should look like the following code.</span></span>

    [!code-cshtml[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample5.cshtml)]
11. <span data-ttu-id="c925d-201">*ASP.NET アプリケーション*を*マニアクイズ*に置き換えることにより、レイアウトページのフッターを更新します。</span><span class="sxs-lookup"><span data-stu-id="c925d-201">Update the footer of the layout page by replacing *My ASP.NET Application* with *Geek Quiz*.</span></span> <span data-ttu-id="c925d-202">これを行うには、 **&lt;フッターの&gt;** 要素の内容を、次の強調表示されたコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="c925d-202">To do this, replace the content of the **&lt;footer&gt;** element with the following highlighted code.</span></span>

    [!code-html[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample6.html)]

<a id="Ex1Task2"></a>
#### <a name="task-2--creating-the-triviacontroller-web-api"></a><span data-ttu-id="c925d-203">タスク2– TriviaController Web API の作成</span><span class="sxs-lookup"><span data-stu-id="c925d-203">Task 2 – Creating the TriviaController Web API</span></span>

<span data-ttu-id="c925d-204">前のタスクでは、マニアクイズ web アプリケーションの初期構造を作成しました。</span><span class="sxs-lookup"><span data-stu-id="c925d-204">In the previous task, you created the initial structure of the Geek Quiz web application.</span></span> <span data-ttu-id="c925d-205">クイズデータモデルと対話する単純な Web API サービスを構築し、次のアクションを公開するようになりました。</span><span class="sxs-lookup"><span data-stu-id="c925d-205">You will now build a simple Web API service that interacts with the quiz data model and exposes the following actions:</span></span>

- <span data-ttu-id="c925d-206">**GET/api/trivia**: 認証されたユーザーが回答する次の質問をクイズ一覧から取得します。</span><span class="sxs-lookup"><span data-stu-id="c925d-206">**GET /api/trivia**: Retrieves the next question from the quiz list to be answered by the authenticated user.</span></span>
- <span data-ttu-id="c925d-207">**POST/api/trivia**: 認証されたユーザーによって指定されたクイズ回答を格納します。</span><span class="sxs-lookup"><span data-stu-id="c925d-207">**POST /api/trivia**: Stores the quiz answer specified by the authenticated user.</span></span>

<span data-ttu-id="c925d-208">Visual Studio に用意されている ASP.NET スキャフォールディングツールを使用して、Web API コントローラークラスのベースラインを作成します。</span><span class="sxs-lookup"><span data-stu-id="c925d-208">You will use the ASP.NET Scaffolding tools provided by Visual Studio to create the baseline for the Web API controller class.</span></span>

1. <span data-ttu-id="c925d-209">**アプリ\_** の [開始] フォルダー内の**WebApiConfig.cs**ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="c925d-209">Open the **WebApiConfig.cs** file inside the **App\_Start** folder.</span></span> <span data-ttu-id="c925d-210">このファイルは、web api コントローラーアクションにルートをマップする方法など、Web API サービスの構成を定義します。</span><span class="sxs-lookup"><span data-stu-id="c925d-210">This file defines the configuration of the Web API service, like how routes are mapped to Web API controller actions.</span></span>
2. <span data-ttu-id="c925d-211">ファイルの先頭に次の using ステートメントを追加します。</span><span class="sxs-lookup"><span data-stu-id="c925d-211">Add the following using statement at the beginning of the file.</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample7.cs)]
3. <span data-ttu-id="c925d-212">次の強調表示されたコードを**Register**メソッドに追加して、Web API アクションメソッドによって取得される JSON データのフォーマッタをグローバルに構成します。</span><span class="sxs-lookup"><span data-stu-id="c925d-212">Add the following highlighted code to the **Register** method to globally configure the formatter for the JSON data retrieved by the Web API action methods.</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample8.cs)]

    > [!NOTE]
    > <span data-ttu-id="c925d-213">**CamelCasePropertyNamesContractResolver**は、プロパティ名を*camel*形式に自動的に変換します。これは、JavaScript でのプロパティ名の一般的な規則です。</span><span class="sxs-lookup"><span data-stu-id="c925d-213">The **CamelCasePropertyNamesContractResolver** automatically converts property names to *camel* case, which is the general convention for property names in JavaScript.</span></span>
4. <span data-ttu-id="c925d-214">**ソリューションエクスプローラー**で、 **GeekQuiz**プロジェクトの**Controllers**フォルダーを右クリックし、[追加] を選択します。 **新しいスキャフォールディング項目...**</span><span class="sxs-lookup"><span data-stu-id="c925d-214">In **Solution Explorer**, right-click the **Controllers** folder of the **GeekQuiz** project and select **Add | New Scaffolded Item...**.</span></span>

    <span data-ttu-id="c925d-215">![新しいスキャフォールディング項目の作成](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image6.png "新しいスキャフォールディング項目の作成")</span><span class="sxs-lookup"><span data-stu-id="c925d-215">![Creating a new scaffolded item](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image6.png "Creating a new scaffolded item")</span></span>

    <span data-ttu-id="c925d-216">*新しいスキャフォールディング項目の作成*</span><span class="sxs-lookup"><span data-stu-id="c925d-216">*Creating a new scaffolded item*</span></span>
5. <span data-ttu-id="c925d-217">**[スキャフォールディングの追加]** ダイアログボックスで、左側のウィンドウで **[共通]** ノードが選択されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="c925d-217">In the **Add Scaffold** dialog box, make sure that the **Common** node is selected in the left pane.</span></span> <span data-ttu-id="c925d-218">次に、中央のウィンドウで **[WEB API 2 コントローラー-空]** のテンプレート テンプレートを選択し、 **[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c925d-218">Then, select the **Web API 2 Controller - Empty** template in the center pane and click **Add**.</span></span>

    <span data-ttu-id="c925d-219">![Web API 2 コントローラーの空のテンプレートを選択する](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image7.png "Web API 2 コントローラーの空のテンプレートを選択する")</span><span class="sxs-lookup"><span data-stu-id="c925d-219">![Selecting the Web API 2 Controller Empty template](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image7.png "Selecting the Web API 2 Controller Empty template")</span></span>

    <span data-ttu-id="c925d-220">*Web API 2 コントローラーの空のテンプレートを選択する*</span><span class="sxs-lookup"><span data-stu-id="c925d-220">*Selecting the Web API 2 Controller Empty template*</span></span>

    > [!NOTE]
    > <span data-ttu-id="c925d-221">**ASP.NET スキャフォールディング**は、ASP.NET Web アプリケーションのコード生成フレームワークです。</span><span class="sxs-lookup"><span data-stu-id="c925d-221">**ASP.NET Scaffolding** is a code generation framework for ASP.NET Web applications.</span></span> <span data-ttu-id="c925d-222">Visual Studio 2013 には、MVC および Web API プロジェクト用のプレインストールされたコードジェネレーターが含まれています。</span><span class="sxs-lookup"><span data-stu-id="c925d-222">Visual Studio 2013 includes pre-installed code generators for MVC and Web API projects.</span></span> <span data-ttu-id="c925d-223">標準データ操作の開発に必要な時間を短縮するために、データモデルと対話するコードをすばやく追加する場合は、プロジェクトでスキャフォールディングを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c925d-223">You should use scaffolding in your project when you want to quickly add code that interacts with data models in order to reduce the amount of time required to develop standard data operations.</span></span>
    > 
    > <span data-ttu-id="c925d-224">また、スキャフォールディングプロセスによって、必要なすべての依存関係がプロジェクトにインストールされます。</span><span class="sxs-lookup"><span data-stu-id="c925d-224">The scaffolding process also ensures that all the required dependencies are installed in the project.</span></span> <span data-ttu-id="c925d-225">たとえば、空の ASP.NET プロジェクトから開始し、スキャフォールディングを使用して Web API コントローラーを追加すると、必要な Web API の NuGet パッケージと参照がプロジェクトに自動的に追加されます。</span><span class="sxs-lookup"><span data-stu-id="c925d-225">For example, if you start with an empty ASP.NET project and then use scaffolding to add a Web API controller, the required Web API NuGet packages and references are added to your project automatically.</span></span>
6. <span data-ttu-id="c925d-226">**[コントローラーの追加]** ダイアログボックスで、 **[コントローラー名]** ボックスに「 *TriviaController* 」と入力し、 **[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c925d-226">In the **Add Controller** dialog box, type *TriviaController* in the **Controller name** text box and click **Add**.</span></span>

    <span data-ttu-id="c925d-227">![トリビアコントローラーの追加](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image8.png "トリビアコントローラーの追加")</span><span class="sxs-lookup"><span data-stu-id="c925d-227">![Adding the Trivia Controller](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image8.png "Adding the Trivia Controller")</span></span>

    <span data-ttu-id="c925d-228">*トリビアコントローラーの追加*</span><span class="sxs-lookup"><span data-stu-id="c925d-228">*Adding the Trivia Controller*</span></span>
7. <span data-ttu-id="c925d-229">次に、 **TriviaController.cs**ファイルが**GeekQuiz**プロジェクトの**Controllers**フォルダーに追加されます。このフォルダーには空の**TriviaController**クラスが含まれています。</span><span class="sxs-lookup"><span data-stu-id="c925d-229">The **TriviaController.cs** file is then added to the **Controllers** folder of the **GeekQuiz** project, containing an empty **TriviaController** class.</span></span> <span data-ttu-id="c925d-230">ファイルの先頭に次の using ステートメントを追加します。</span><span class="sxs-lookup"><span data-stu-id="c925d-230">Add the following using statements at the beginning of the file.</span></span>

    <span data-ttu-id="c925d-231">(コードスニペット- *AspNetWebApiSpa-Ex1-TriviaControllerUsings*)</span><span class="sxs-lookup"><span data-stu-id="c925d-231">(Code Snippet - *AspNetWebApiSpa - Ex1 - TriviaControllerUsings*)</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample9.cs)]
8. <span data-ttu-id="c925d-232">**TriviaController**クラスの先頭に次のコードを追加して、コントローラーの**TriviaContext**インスタンスを定義、初期化、および破棄します。</span><span class="sxs-lookup"><span data-stu-id="c925d-232">Add the following code at the beginning of the **TriviaController** class to define, initialize and dispose the **TriviaContext** instance in the controller.</span></span>

    <span data-ttu-id="c925d-233">(コードスニペット- *AspNetWebApiSpa-Ex1-TriviaControllerContext*)</span><span class="sxs-lookup"><span data-stu-id="c925d-233">(Code Snippet - *AspNetWebApiSpa - Ex1 - TriviaControllerContext*)</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample10.cs)]

    > [!NOTE]
    > <span data-ttu-id="c925d-234">**TriviaController**の**dispose**メソッドは、 **TriviaContext**インスタンスの**dispose**メソッドを呼び出します。これにより、 **TriviaContext**インスタンスが破棄またはガベージコレクトされたときに、context オブジェクトによって使用されるすべてのリソースが解放されます。</span><span class="sxs-lookup"><span data-stu-id="c925d-234">The **Dispose** method of **TriviaController** invokes the **Dispose** method of the **TriviaContext** instance, which ensures that all the resources used by the context object are released when the **TriviaContext** instance is disposed or garbage-collected.</span></span> <span data-ttu-id="c925d-235">これには、Entity Framework によって開かれたすべてのデータベース接続の終了が含まれます。</span><span class="sxs-lookup"><span data-stu-id="c925d-235">This includes closing all database connections opened by Entity Framework.</span></span>
9. <span data-ttu-id="c925d-236">**TriviaController**クラスの末尾に、次のヘルパーメソッドを追加します。</span><span class="sxs-lookup"><span data-stu-id="c925d-236">Add the following helper method at the end of the **TriviaController** class.</span></span> <span data-ttu-id="c925d-237">このメソッドは、指定されたユーザーによって応答されるように、データベースから次のクイズ質問を取得します。</span><span class="sxs-lookup"><span data-stu-id="c925d-237">This method retrieves the following quiz question from the database to be answered by the specified user.</span></span>

    <span data-ttu-id="c925d-238">(コードスニペット- *AspNetWebApiSpa-Ex1-TriviaControllerNextQuestion*)</span><span class="sxs-lookup"><span data-stu-id="c925d-238">(Code Snippet - *AspNetWebApiSpa - Ex1 - TriviaControllerNextQuestion*)</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample11.cs)]
10. <span data-ttu-id="c925d-239">次の**Get** action メソッドを**TriviaController**クラスに追加します。</span><span class="sxs-lookup"><span data-stu-id="c925d-239">Add the following **Get** action method to the **TriviaController** class.</span></span> <span data-ttu-id="c925d-240">このアクションメソッドは、前の手順で定義した**NextQuestionAsync** helper メソッドを呼び出して、認証されたユーザーの次の質問を取得します。</span><span class="sxs-lookup"><span data-stu-id="c925d-240">This action method calls the **NextQuestionAsync** helper method defined in the previous step to retrieve the next question for the authenticated user.</span></span>

    <span data-ttu-id="c925d-241">(コードスニペット- *AspNetWebApiSpa-Ex1-TriviaControllerGetAction*)</span><span class="sxs-lookup"><span data-stu-id="c925d-241">(Code Snippet - *AspNetWebApiSpa - Ex1 - TriviaControllerGetAction*)</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample12.cs)]
11. <span data-ttu-id="c925d-242">**TriviaController**クラスの末尾に、次のヘルパーメソッドを追加します。</span><span class="sxs-lookup"><span data-stu-id="c925d-242">Add the following helper method at the end of the **TriviaController** class.</span></span> <span data-ttu-id="c925d-243">このメソッドは、指定された回答をデータベースに格納し、答えが正しいかどうかを示すブール値を返します。</span><span class="sxs-lookup"><span data-stu-id="c925d-243">This method stores the specified answer in the database and returns a Boolean value indicating whether or not the answer is correct.</span></span>

    <span data-ttu-id="c925d-244">(コードスニペット- *AspNetWebApiSpa-Ex1-TriviaControllerStoreAsync*)</span><span class="sxs-lookup"><span data-stu-id="c925d-244">(Code Snippet - *AspNetWebApiSpa - Ex1 - TriviaControllerStoreAsync*)</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample13.cs)]
12. <span data-ttu-id="c925d-245">次の**Post**アクションメソッドを**TriviaController**クラスに追加します。</span><span class="sxs-lookup"><span data-stu-id="c925d-245">Add the following **Post** action method to the **TriviaController** class.</span></span> <span data-ttu-id="c925d-246">このアクションメソッドは、認証されたユーザーに回答を関連付け、 **StoreAsync** helper メソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="c925d-246">This action method associates the answer to the authenticated user and calls the **StoreAsync** helper method.</span></span> <span data-ttu-id="c925d-247">次に、ヘルパーメソッドによって返されるブール値を使用して応答を送信します。</span><span class="sxs-lookup"><span data-stu-id="c925d-247">Then, it sends a response with the Boolean value returned by the helper method.</span></span>

    <span data-ttu-id="c925d-248">(コードスニペット- *AspNetWebApiSpa-Ex1-TriviaControllerPostAction*)</span><span class="sxs-lookup"><span data-stu-id="c925d-248">(Code Snippet - *AspNetWebApiSpa - Ex1 - TriviaControllerPostAction*)</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample14.cs)]
13. <span data-ttu-id="c925d-249">認証されたユーザーへのアクセスを制限するように Web API コントローラーを変更するには、 **TriviaController**クラス定義に**承認**属性を追加します。</span><span class="sxs-lookup"><span data-stu-id="c925d-249">Modify the Web API controller to restrict access to authenticated users by adding the **Authorize** attribute to the **TriviaController** class definition.</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample15.cs)]

<a id="Ex1Task3"></a>
#### <a name="task-3--running-the-solution"></a><span data-ttu-id="c925d-250">タスク3–ソリューションを実行する</span><span class="sxs-lookup"><span data-stu-id="c925d-250">Task 3 – Running the Solution</span></span>

<span data-ttu-id="c925d-251">このタスクでは、前のタスクで作成した Web API サービスが想定どおりに動作していることを確認します。</span><span class="sxs-lookup"><span data-stu-id="c925d-251">In this task you will verify that the Web API service you built in the previous task is working as expected.</span></span> <span data-ttu-id="c925d-252">ネットワークトラフィックをキャプチャし、Web API サービスからの完全な応答を調べるには、Internet Explorer **F12 開発者ツール**を使用します。</span><span class="sxs-lookup"><span data-stu-id="c925d-252">You will use the Internet Explorer **F12 Developer Tools** to capture the network traffic and inspect the full response from the Web API service.</span></span>

> [!NOTE]
> <span data-ttu-id="c925d-253">Visual Studio ツールバーの **[スタート]** ボタンで**Internet Explorer**が選択されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="c925d-253">Make sure that **Internet Explorer** is selected in the **Start** button located on the Visual Studio toolbar.</span></span>
> 
> ![Internet Explorer オプション](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image9.png)

1. <span data-ttu-id="c925d-255">F5 キーを押して、ソリューションを実行します。</span><span class="sxs-lookup"><span data-stu-id="c925d-255">Press **F5** to run the solution.</span></span> <span data-ttu-id="c925d-256">ブラウザーに**ログイン**ページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="c925d-256">The **Log in** page should appear in the browser.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c925d-257">アプリケーションの起動時に、既定の MVC ルートがトリガーされます。既定では、 **HomeController**クラスの**Index**アクションにマップされます。</span><span class="sxs-lookup"><span data-stu-id="c925d-257">When the application starts, the default MVC route is triggered, which by default is mapped to the **Index** action of the **HomeController** class.</span></span> <span data-ttu-id="c925d-258">**HomeController**は認証されたユーザーに限定されるため (演習1では**承認**属性を使用してクラスを修飾しています)、まだユーザーが認証されていないため、アプリケーションは元の要求をログインページにリダイレクトします。</span><span class="sxs-lookup"><span data-stu-id="c925d-258">Since **HomeController** is restricted to authenticated users (remember that you decorated that class with the **Authorize** attribute in Exercise 1) and there is no user authenticated yet, the application redirects the original request to the log in page.</span></span>

    <span data-ttu-id="c925d-259">![ソリューションの実行](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image10.png "ソリューションの実行")</span><span class="sxs-lookup"><span data-stu-id="c925d-259">![Running the solution](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image10.png "Running the solution")</span></span>

    <span data-ttu-id="c925d-260">*ソリューションの実行*</span><span class="sxs-lookup"><span data-stu-id="c925d-260">*Running the solution*</span></span>
2. <span data-ttu-id="c925d-261">**[登録]** をクリックして、新しいユーザーを作成します。</span><span class="sxs-lookup"><span data-stu-id="c925d-261">Click **Register** to create a new user.</span></span>

    <span data-ttu-id="c925d-262">![新しいユーザーの登録](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image11.png "新しいユーザーの登録")</span><span class="sxs-lookup"><span data-stu-id="c925d-262">![Registering a new user](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image11.png "Registering a new user")</span></span>

    <span data-ttu-id="c925d-263">*新しいユーザーの登録*</span><span class="sxs-lookup"><span data-stu-id="c925d-263">*Registering a new user*</span></span>
3. <span data-ttu-id="c925d-264">**[登録]** ページで、**ユーザー名**と**パスワード**を入力し、 **[登録]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c925d-264">In the **Register** page, enter a **User name** and **Password**, and then click **Register**.</span></span>

    <span data-ttu-id="c925d-265">![[登録] ページ](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image12.png "[登録] ページ")</span><span class="sxs-lookup"><span data-stu-id="c925d-265">![Register page](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image12.png "Register page")</span></span>

    <span data-ttu-id="c925d-266">*[登録] ページ*</span><span class="sxs-lookup"><span data-stu-id="c925d-266">*Register page*</span></span>
4. <span data-ttu-id="c925d-267">アプリケーションが新しいアカウントを登録すると、ユーザーが認証され、ホームページにリダイレクトされます。</span><span class="sxs-lookup"><span data-stu-id="c925d-267">The application registers the new account and the user is authenticated and redirected back to the home page.</span></span>

    <span data-ttu-id="c925d-268">![ユーザーは認証されています](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image13.png "認証されたユーザー")</span><span class="sxs-lookup"><span data-stu-id="c925d-268">![User is authenticated](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image13.png "User authenticated")</span></span>

    <span data-ttu-id="c925d-269">*ユーザーは認証されています*</span><span class="sxs-lookup"><span data-stu-id="c925d-269">*User is authenticated*</span></span>
5. <span data-ttu-id="c925d-270">ブラウザーで**F12**キーを押して、 **[開発者ツール]** パネルを開きます。</span><span class="sxs-lookup"><span data-stu-id="c925d-270">In the browser, press **F12** to open the **Developer Tools** panel.</span></span> <span data-ttu-id="c925d-271">**CTRL + 4**キーを押すか、**ネットワーク**アイコンをクリックし、緑色の矢印ボタンをクリックしてネットワークトラフィックのキャプチャを開始します。</span><span class="sxs-lookup"><span data-stu-id="c925d-271">Press **CTRL + 4** or click the **Network** icon, and then click the green arrow button to begin capturing network traffic.</span></span>

    <span data-ttu-id="c925d-272">![Web API ネットワークキャプチャを開始しています](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image14.png "Web API ネットワークキャプチャを開始しています")</span><span class="sxs-lookup"><span data-stu-id="c925d-272">![Initiating Web API network capture](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image14.png "Initiating Web API network capture")</span></span>

    <span data-ttu-id="c925d-273">*Web API ネットワークキャプチャを開始しています*</span><span class="sxs-lookup"><span data-stu-id="c925d-273">*Initiating Web API network capture*</span></span>
6. <span data-ttu-id="c925d-274">ブラウザーのアドレスバーの URL に**api/トリビア**を追加します。</span><span class="sxs-lookup"><span data-stu-id="c925d-274">Append **api/trivia** to the URL in the browser's address bar.</span></span> <span data-ttu-id="c925d-275">次に、 **TriviaController**の**Get** action メソッドから応答の詳細を調べます。</span><span class="sxs-lookup"><span data-stu-id="c925d-275">You will now inspect the details of the response from the **Get** action method in **TriviaController**.</span></span>

    <span data-ttu-id="c925d-276">![Web API を使用して次の質問データを取得する](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image15.png "Web API を使用して次の質問データを取得する")</span><span class="sxs-lookup"><span data-stu-id="c925d-276">![Retrieving the next question data through Web API](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image15.png "Retrieving the next question data through Web API")</span></span>

    <span data-ttu-id="c925d-277">*Web API を使用して次の質問データを取得する*</span><span class="sxs-lookup"><span data-stu-id="c925d-277">*Retrieving the next question data through Web API*</span></span>

    > [!NOTE]
    > <span data-ttu-id="c925d-278">ダウンロードが完了すると、ダウンロードしたファイルに対してアクションを実行するように求められます。</span><span class="sxs-lookup"><span data-stu-id="c925d-278">Once the download finishes, you will be prompted to make an action with the downloaded file.</span></span> <span data-ttu-id="c925d-279">[開発者ツール] ウィンドウで応答の内容を確認できるようにするには、ダイアログボックスを開いたままにしておきます。</span><span class="sxs-lookup"><span data-stu-id="c925d-279">Leave the dialog box open in order to be able to watch the response content through the Developers Tool window.</span></span>
7. <span data-ttu-id="c925d-280">次に、応答の本文を調べます。</span><span class="sxs-lookup"><span data-stu-id="c925d-280">Now you will inspect the body of the response.</span></span> <span data-ttu-id="c925d-281">これを行うには、 **[詳細]** タブをクリックし、 **[応答本文]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c925d-281">To do this, click the **Details** tab and then click **Response body**.</span></span> <span data-ttu-id="c925d-282">ダウンロードしたデータが、 **TriviaQuestion**クラスに対応するプロパティ**オプション**( **TriviaOption**オブジェクトのリスト)、 **id** 、および**タイトル**を持つオブジェクトであることを確認できます。</span><span class="sxs-lookup"><span data-stu-id="c925d-282">You can check that the downloaded data is an object with the properties **options** (which is a list of **TriviaOption** objects), **id** and **title** that correspond to the **TriviaQuestion** class.</span></span>

    <span data-ttu-id="c925d-283">![Web API 応答本文の表示](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image16.png "Web API 応答本文の表示")</span><span class="sxs-lookup"><span data-stu-id="c925d-283">![Viewing the Web API Response Body](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image16.png "Viewing the Web API Response Body")</span></span>

    <span data-ttu-id="c925d-284">*Web API の応答本文を表示しています*</span><span class="sxs-lookup"><span data-stu-id="c925d-284">*Viewing Web API Response Body*</span></span>
8. <span data-ttu-id="c925d-285">Visual Studio に戻り、SHIFT キーを押し**ながら F5**キーを押してデバッグを停止します。</span><span class="sxs-lookup"><span data-stu-id="c925d-285">Go back to Visual Studio and press **SHIFT + F5** to stop debugging.</span></span>

<a id="Exercise2"></a>
### <a name="exercise-2-creating-the-spa-interface"></a><span data-ttu-id="c925d-286">演習 2: SPA インターフェイスの作成</span><span class="sxs-lookup"><span data-stu-id="c925d-286">Exercise 2: Creating the SPA Interface</span></span>

<span data-ttu-id="c925d-287">この演習では、まず、マニアクイズの web フロントエンドの部分を構築します。 **AngularJS**を使用したシングルページアプリケーションの操作に重点を置いています。</span><span class="sxs-lookup"><span data-stu-id="c925d-287">In this exercise you will first build the web front-end portion of Geek Quiz, focusing on the Single-Page Application interaction using **AngularJS**.</span></span> <span data-ttu-id="c925d-288">次に、CSS3 でのユーザーエクスペリエンスを向上させ、豊富なアニメーションを実行し、1つの質問から次の質問に移行するときにコンテキストの切り替え効果を視覚的に示すことができるようにします。</span><span class="sxs-lookup"><span data-stu-id="c925d-288">You will then enhance the user experience with CSS3 to perform rich animations and provide a visual effect of context switching when transitioning from one question to the next.</span></span>

<a id="Ex2Task1"></a>
#### <a name="task-1--creating-the-spa-interface-using-angularjs"></a><span data-ttu-id="c925d-289">タスク1– AngularJS を使用して SPA インターフェイスを作成する</span><span class="sxs-lookup"><span data-stu-id="c925d-289">Task 1 – Creating the SPA Interface Using AngularJS</span></span>

<span data-ttu-id="c925d-290">このタスクでは、 **AngularJS**を使用して、マニアクイズアプリケーションのクライアント側を実装します。</span><span class="sxs-lookup"><span data-stu-id="c925d-290">In this task you will use **AngularJS** to implement the client side of the Geek Quiz application.</span></span> <span data-ttu-id="c925d-291">**AngularJS**は、ブラウザーベースのアプリケーションを*モデルビューコントローラー* (MVC) 機能で強化するオープンソースの JavaScript フレームワークであり、開発とテストの両方を容易にします。</span><span class="sxs-lookup"><span data-stu-id="c925d-291">**AngularJS** is an open-source JavaScript framework that augments browser-based applications with *Model-View-Controller* (MVC) capability, facilitating both development and testing.</span></span>

<span data-ttu-id="c925d-292">最初に、Visual Studio のパッケージマネージャーコンソールから AngularJS をインストールします。</span><span class="sxs-lookup"><span data-stu-id="c925d-292">You will start by installing AngularJS from Visual Studio's Package Manager Console.</span></span> <span data-ttu-id="c925d-293">次に、マニアクイズアプリの動作を提供するコントローラーを作成し、AngularJS テンプレートエンジンを使用してクイズの質問と回答を表示するビューを作成します。</span><span class="sxs-lookup"><span data-stu-id="c925d-293">Then, you will create the controller to provide the behavior of the Geek Quiz app and the view to render the quiz questions and answers using the AngularJS template engine.</span></span>

> [!NOTE]
> <span data-ttu-id="c925d-294">AngularJS の詳細については、 [[http://angularjs.org/](http://angularjs.org/)](http://angularjs.org/)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c925d-294">For more information about AngularJS, refer to [[http://angularjs.org/](http://angularjs.org/)](http://angularjs.org/).</span></span>

1. <span data-ttu-id="c925d-295">**Web 用に Visual Studio Express 2013**を開き、 **Source/Ex2 GeekQuiz/Begin**フォルダーにあるソリューションを開きます。</span><span class="sxs-lookup"><span data-stu-id="c925d-295">Open **Visual Studio Express 2013 for Web** and open the **GeekQuiz.sln** solution located in the **Source/Ex2-CreatingASPAInterface/Begin** folder.</span></span> <span data-ttu-id="c925d-296">または、前の演習で取得したソリューションを続行することもできます。</span><span class="sxs-lookup"><span data-stu-id="c925d-296">Alternatively, you can continue with the solution that you obtained in the previous exercise.</span></span>
2. <span data-ttu-id="c925d-297">[**ツール** > **NuGet パッケージマネージャー**] から**パッケージマネージャーコンソール**を開きます。</span><span class="sxs-lookup"><span data-stu-id="c925d-297">Open the **Package Manager Console** from **Tools** > **NuGet Package Manager**.</span></span> <span data-ttu-id="c925d-298">次のコマンドを入力して、 **AngularJS** NuGet パッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="c925d-298">Type the following command to install the **AngularJS.Core** NuGet package.</span></span>

    [!code-powershell[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample16.ps1)]
3. <span data-ttu-id="c925d-299">**ソリューションエクスプローラー**で、 **GeekQuiz**プロジェクトの**Scripts**フォルダーを右クリックし、[追加] を選択します。 **新しいフォルダー**。</span><span class="sxs-lookup"><span data-stu-id="c925d-299">In **Solution Explorer**, right-click the **Scripts** folder of the **GeekQuiz** project and select **Add | New Folder**.</span></span> <span data-ttu-id="c925d-300">フォルダーに**アプリ**の名前を**指定**し、enter キーを押します。</span><span class="sxs-lookup"><span data-stu-id="c925d-300">Name the folder **app** and press **Enter**.</span></span>
4. <span data-ttu-id="c925d-301">先ほど作成した**アプリ**フォルダーを右クリックし、[追加] を選択します。 **JavaScript ファイル**。</span><span class="sxs-lookup"><span data-stu-id="c925d-301">Right-click the **app** folder you just created and select **Add | JavaScript File**.</span></span>

    ![新しい JavaScript ファイルの作成](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image17.png)

    <span data-ttu-id="c925d-303">*新しい JavaScript ファイルの作成*</span><span class="sxs-lookup"><span data-stu-id="c925d-303">*Creating a new JavaScript file*</span></span>
5. <span data-ttu-id="c925d-304">**[項目の名前の指定]** ダイアログボックスの **[項目名]** ボックスに「*クイズ-controller* 」と入力し、 **[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c925d-304">In the **Specify Name for Item** dialog box, type *quiz-controller* in the **Item name** text box and click **OK**.</span></span>

    ![新しい JavaScript ファイルに名前を付ける](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image18.png)

    <span data-ttu-id="c925d-306">*新しい JavaScript ファイルに名前を付ける*</span><span class="sxs-lookup"><span data-stu-id="c925d-306">*Naming the new JavaScript file*</span></span>
6. <span data-ttu-id="c925d-307">**Quiz-controller**ファイルで、AngularJS **QuizCtrl** controller を宣言して初期化する次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="c925d-307">In the **quiz-controller.js** file, add the following code to declare and initialize the AngularJS **QuizCtrl** controller.</span></span>

    <span data-ttu-id="c925d-308">(コードスニペット- *AspNetWebApiSpa-Ex2-AngularQuizController*)</span><span class="sxs-lookup"><span data-stu-id="c925d-308">(Code Snippet - *AspNetWebApiSpa - Ex2 - AngularQuizController*)</span></span>

    [!code-javascript[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample17.js)]

    > [!NOTE]
    > <span data-ttu-id="c925d-309">**QuizCtrl**コントローラーのコンストラクター関数には、 **$scope**という名前の injectable パラメーターが必要です。</span><span class="sxs-lookup"><span data-stu-id="c925d-309">The constructor function of the **QuizCtrl** controller expects an injectable parameter named **$scope**.</span></span> <span data-ttu-id="c925d-310">スコープの初期状態は、プロパティを **$scope**オブジェクトにアタッチすることによって、コンストラクター関数で設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c925d-310">The initial state of the scope should be set up in the constructor function by attaching properties to the **$scope** object.</span></span> <span data-ttu-id="c925d-311">プロパティには**ビューモデル**が含まれており、コントローラーが登録されると、テンプレートにアクセスできるようになります。</span><span class="sxs-lookup"><span data-stu-id="c925d-311">The properties contain the **view model**, and will be accessible to the template when the controller is registered.</span></span>
    > 
    > <span data-ttu-id="c925d-312">**QuizCtrl**コントローラーは、 **QuizApp**という名前のモジュール内で定義されています。</span><span class="sxs-lookup"><span data-stu-id="c925d-312">The **QuizCtrl** controller is defined inside a module named **QuizApp**.</span></span> <span data-ttu-id="c925d-313">モジュールは、アプリケーションを別のコンポーネントに分割できるようにする作業単位です。</span><span class="sxs-lookup"><span data-stu-id="c925d-313">Modules are units of work that let you break your application into separate components.</span></span> <span data-ttu-id="c925d-314">モジュールを使用する主な利点は、コードが理解しやすく、単体テスト、再利用性、および保守容易性が向上することです。</span><span class="sxs-lookup"><span data-stu-id="c925d-314">The main advantages of using modules is that the code is easier to understand and facilitates unit testing, reusability and maintainability.</span></span>
7. <span data-ttu-id="c925d-315">ここで、ビューからトリガーされたイベントに応答するために、スコープに動作を追加します。</span><span class="sxs-lookup"><span data-stu-id="c925d-315">You will now add behavior to the scope in order to react to events triggered from the view.</span></span> <span data-ttu-id="c925d-316">**QuizCtrl**コントローラーの末尾に次のコードを追加して、 **$Scope**オブジェクトで**nextquestion**関数を定義します。</span><span class="sxs-lookup"><span data-stu-id="c925d-316">Add the following code at the end of the **QuizCtrl** controller to define the **nextQuestion** function in the **$scope** object.</span></span>

    <span data-ttu-id="c925d-317">(コードスニペット- *AspNetWebApiSpa-Ex2-AngularQuizControllerNextQuestion*)</span><span class="sxs-lookup"><span data-stu-id="c925d-317">(Code Snippet - *AspNetWebApiSpa - Ex2 - AngularQuizControllerNextQuestion*)</span></span>

    [!code-javascript[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample18.js)]

    > [!NOTE]
    > <span data-ttu-id="c925d-318">この関数は、前の演習で作成した**トリビア**Web API から次の質問を取得し、その質問データを **$scope**オブジェクトにアタッチします。</span><span class="sxs-lookup"><span data-stu-id="c925d-318">This function retrieves the next question from the **Trivia** Web API created in the previous exercise and attaches the question data to the **$scope** object.</span></span>
8. <span data-ttu-id="c925d-319">**QuizCtrl**コントローラーの末尾に次のコードを挿入して、 **$Scope**オブジェクトで**sendanswer**関数を定義します。</span><span class="sxs-lookup"><span data-stu-id="c925d-319">Insert the following code at the end of the **QuizCtrl** controller to define the **sendAnswer** function in the **$scope** object.</span></span>

    <span data-ttu-id="c925d-320">(コードスニペット- *AspNetWebApiSpa-Ex2-AngularQuizControllerSendAnswer*)</span><span class="sxs-lookup"><span data-stu-id="c925d-320">(Code Snippet - *AspNetWebApiSpa - Ex2 - AngularQuizControllerSendAnswer*)</span></span>

    [!code-javascript[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample19.js)]

    > [!NOTE]
    > <span data-ttu-id="c925d-321">この関数は、ユーザーによって選択された回答を**トリビア**Web API に送信し、結果を格納します。つまり、 **$scope**オブジェクト内の結果が正しいかどうかを示します。</span><span class="sxs-lookup"><span data-stu-id="c925d-321">This function sends the answer selected by the user to the **Trivia** Web API and stores the result –i.e. if the answer is correct or not– in the **$scope** object.</span></span>
    > 
    > <span data-ttu-id="c925d-322">上記の**Nextquestion**と**sendanswer**関数は、AngularJS **$http**オブジェクトを使用して、ブラウザーから XMLHttpRequest JAVASCRIPT オブジェクトを介して Web API との通信を抽象化します。</span><span class="sxs-lookup"><span data-stu-id="c925d-322">The **nextQuestion** and **sendAnswer** functions from above use the AngularJS **$http** object to abstract the communication with the Web API via the XMLHttpRequest JavaScript object from the browser.</span></span> <span data-ttu-id="c925d-323">AngularJS は、RESTful Api を介してリソースに対して CRUD 操作を実行するために、より高いレベルの抽象化を提供する別のサービスをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="c925d-323">AngularJS supports another service that brings a higher level of abstraction to perform CRUD operations against a resource through RESTful APIs.</span></span> <span data-ttu-id="c925d-324">AngularJS **$resource**オブジェクトには、 **$http**オブジェクトと対話する必要がない高レベルの動作を提供するアクションメソッドがあります。</span><span class="sxs-lookup"><span data-stu-id="c925d-324">The AngularJS **$resource** object has action methods which provide high-level behaviors without the need to interact with the **$http** object.</span></span> <span data-ttu-id="c925d-325">CRUD モデルを必要とするシナリオでは、 **$resource**オブジェクトの使用を検討してください (前景の情報、 [$resource のドキュメント](https://docs.angularjs.org/api/ngResource/service/$resource)を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="c925d-325">Consider using the **$resource** object in scenarios that requires the CRUD model (fore information, see the [$resource documentation](https://docs.angularjs.org/api/ngResource/service/$resource)).</span></span>
9. <span data-ttu-id="c925d-326">次の手順では、クイズのビューを定義する AngularJS テンプレートを作成します。</span><span class="sxs-lookup"><span data-stu-id="c925d-326">The next step is to create the AngularJS template that defines the view for the quiz.</span></span> <span data-ttu-id="c925d-327">これを行うには、Views | の内側にある**Index. cshtml**ファイルを開きます。 **[ホーム**] フォルダーを使用して、内容を次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="c925d-327">To do this, open the **Index.cshtml** file inside the **Views | Home** folder and replace the content with the following code.</span></span>

    <span data-ttu-id="c925d-328">(コードスニペット- *AspNetWebApiSpa-Ex2-GeekQuizView*)</span><span class="sxs-lookup"><span data-stu-id="c925d-328">(Code Snippet - *AspNetWebApiSpa - Ex2 - GeekQuizView*)</span></span>

    [!code-cshtml[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample20.cshtml)]

    > [!NOTE]
    > <span data-ttu-id="c925d-329">AngularJS テンプレートは、モデルとコントローラーの情報を使用して、ブラウザーでユーザーに表示される動的ビューに静的マークアップを変換する宣言型の仕様です。</span><span class="sxs-lookup"><span data-stu-id="c925d-329">The AngularJS template is a declarative specification that uses information from the model and the controller to transform static markup into the dynamic view that the user sees in the browser.</span></span> <span data-ttu-id="c925d-330">テンプレートで使用できる AngularJS 要素と要素属性の例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="c925d-330">The following are examples of AngularJS elements and element attributes that can be used in a template:</span></span>
    > 
    > - <span data-ttu-id="c925d-331">AngularJS**ディレクティブは、アプリケーション**のルート要素を表す DOM 要素をに指示します。</span><span class="sxs-lookup"><span data-stu-id="c925d-331">The **ng-app** directive tells AngularJS the DOM element that represents the root element of the application.</span></span>
    > - <span data-ttu-id="c925d-332">**Ng コントローラー**ディレクティブは、ディレクティブが宣言されているポイントで、コントローラーを DOM にアタッチします。</span><span class="sxs-lookup"><span data-stu-id="c925d-332">The **ng-controller** directive attaches a controller to the DOM at the point where the directive is declared.</span></span>
    > - <span data-ttu-id="c925d-333">中かっこの表記 **{{}}** は、コントローラーで定義されているスコーププロパティへのバインドを示します。</span><span class="sxs-lookup"><span data-stu-id="c925d-333">The curly brace notation **{{ }}** denotes bindings to the scope properties defined in the controller.</span></span>
    > - <span data-ttu-id="c925d-334">**Ng**ディレクティブは、ユーザーのクリックに応じてスコープ内で定義されている関数を呼び出すために使用されます。</span><span class="sxs-lookup"><span data-stu-id="c925d-334">The **ng-click** directive is used to invoke the functions defined in the scope in response to user clicks.</span></span>
10. <span data-ttu-id="c925d-335">**Content**フォルダー内で**サイトの .css**ファイルを開き、次の強調表示されたスタイルをファイルの末尾に追加して、クイズビューのルックアンドフィールを提供します。</span><span class="sxs-lookup"><span data-stu-id="c925d-335">Open the **Site.css** file inside the **Content** folder and add the following highlighted styles at the end of the file to provide a look and feel for the quiz view.</span></span>

    <span data-ttu-id="c925d-336">(コードスニペット- *AspNetWebApiSpa-Ex2-GeekQuizStyles*)</span><span class="sxs-lookup"><span data-stu-id="c925d-336">(Code Snippet - *AspNetWebApiSpa - Ex2 - GeekQuizStyles*)</span></span>

    [!code-css[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample21.css)]

<a id="Ex2Task2"></a>
#### <a name="task-2--running-the-solution"></a><span data-ttu-id="c925d-337">タスク2–ソリューションを実行する</span><span class="sxs-lookup"><span data-stu-id="c925d-337">Task 2 – Running the Solution</span></span>

<span data-ttu-id="c925d-338">このタスクでは、AngularJS で作成した新しいユーザーインターフェイスを使用してソリューションを実行し、いくつかのクイズの質問に回答します。</span><span class="sxs-lookup"><span data-stu-id="c925d-338">In this task you will execute the solution using the new user interface you built with AngularJS to answer some of the quiz questions.</span></span>

1. <span data-ttu-id="c925d-339">F5 キーを押して、ソリューションを実行します。</span><span class="sxs-lookup"><span data-stu-id="c925d-339">Press **F5** to run the solution.</span></span>
2. <span data-ttu-id="c925d-340">新しいユーザーアカウントを登録します。</span><span class="sxs-lookup"><span data-stu-id="c925d-340">Register a new user account.</span></span> <span data-ttu-id="c925d-341">これを行うには、「演習1、タスク3」で説明されている登録手順に従います。</span><span class="sxs-lookup"><span data-stu-id="c925d-341">To do this, follow the registration steps described in Exercise 1, Task 3.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c925d-342">前の演習のソリューションを使用している場合は、前に作成したユーザーアカウントを使用してログインできます。</span><span class="sxs-lookup"><span data-stu-id="c925d-342">If you are using the solution from the previous exercise, you can log in with the user account you created before.</span></span>
3. <span data-ttu-id="c925d-343">**ホーム**ページが表示され、クイズの最初の質問が表示されます。</span><span class="sxs-lookup"><span data-stu-id="c925d-343">The **Home** page should appear, showing the first question of the quiz.</span></span> <span data-ttu-id="c925d-344">いずれかのオプションをクリックして質問に回答します。</span><span class="sxs-lookup"><span data-stu-id="c925d-344">Answer the question by clicking one of the options.</span></span> <span data-ttu-id="c925d-345">これにより、前に定義した**Sendanswer**関数がトリガーされ、選択したオプションが**トリビア**Web API に送信されます。</span><span class="sxs-lookup"><span data-stu-id="c925d-345">This will trigger the **sendAnswer** function defined earlier, which sends the selected option to the **Trivia** Web API.</span></span>

    <span data-ttu-id="c925d-346">![質問への回答](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image19.png "質問への回答")</span><span class="sxs-lookup"><span data-stu-id="c925d-346">![Answering a question](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image19.png "Answering a question")</span></span>

    <span data-ttu-id="c925d-347">*質問への回答*</span><span class="sxs-lookup"><span data-stu-id="c925d-347">*Answering a question*</span></span>
4. <span data-ttu-id="c925d-348">いずれかのボタンをクリックすると、回答が表示されます。</span><span class="sxs-lookup"><span data-stu-id="c925d-348">After clicking one of the buttons, the answer should appear.</span></span> <span data-ttu-id="c925d-349">**[次の質問]** をクリックして、次の質問を表示します。</span><span class="sxs-lookup"><span data-stu-id="c925d-349">Click **Next Question** to show the following question.</span></span> <span data-ttu-id="c925d-350">これにより、コントローラーで定義されている**Nextquestion**関数がトリガーされます。</span><span class="sxs-lookup"><span data-stu-id="c925d-350">This will trigger the **nextQuestion** function defined in the controller.</span></span>

    <span data-ttu-id="c925d-351">![次の質問を要求する](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image20.png "次の質問を要求する")</span><span class="sxs-lookup"><span data-stu-id="c925d-351">![Requesting the next question](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image20.png "Requesting the next question")</span></span>

    <span data-ttu-id="c925d-352">*次の質問を要求する*</span><span class="sxs-lookup"><span data-stu-id="c925d-352">*Requesting the next question*</span></span>
5. <span data-ttu-id="c925d-353">次の質問が表示されます。</span><span class="sxs-lookup"><span data-stu-id="c925d-353">The next question should appear.</span></span> <span data-ttu-id="c925d-354">必要に応じて何度でも質問に答えることができます。</span><span class="sxs-lookup"><span data-stu-id="c925d-354">Continue answering questions as many times as you want.</span></span> <span data-ttu-id="c925d-355">すべての質問を完了したら、最初の質問に戻ります。</span><span class="sxs-lookup"><span data-stu-id="c925d-355">After completing all the questions you should return to the first question.</span></span>

    <span data-ttu-id="c925d-356">![もう1つの質問](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image21.png "もう1つの質問")</span><span class="sxs-lookup"><span data-stu-id="c925d-356">![Another question](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image21.png "Another question")</span></span>

    <span data-ttu-id="c925d-357">*次の質問*</span><span class="sxs-lookup"><span data-stu-id="c925d-357">*Next question*</span></span>
6. <span data-ttu-id="c925d-358">Visual Studio に戻り、SHIFT キーを押し**ながら F5**キーを押してデバッグを停止します。</span><span class="sxs-lookup"><span data-stu-id="c925d-358">Go back to Visual Studio and press **SHIFT + F5** to stop debugging.</span></span>

<a id="Ex2Task3"></a>
#### <a name="task-3--creating-a-flip-animation-using-css3"></a><span data-ttu-id="c925d-359">タスク3– CSS3 を使用したフリップアニメーションの作成</span><span class="sxs-lookup"><span data-stu-id="c925d-359">Task 3 – Creating a Flip Animation Using CSS3</span></span>

<span data-ttu-id="c925d-360">このタスクでは、CSS3 プロパティを使用して、質問に回答し、次の質問を取得したときにフリップ効果を追加することにより、豊富なアニメーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="c925d-360">In this task you will use CSS3 properties to perform rich animations by adding a flip effect when a question is answered and when the next question is retrieved.</span></span>

1. <span data-ttu-id="c925d-361">**ソリューションエクスプローラー**で、 **GeekQuiz**プロジェクトの**Content**フォルダーを右クリックし、[追加] を選択します。 **既存の項目...** .</span><span class="sxs-lookup"><span data-stu-id="c925d-361">In **Solution Explorer**, right-click the **Content** folder of the **GeekQuiz** project and select **Add | Existing Item...**.</span></span>

    <span data-ttu-id="c925d-362">![既存の項目をコンテンツフォルダーに追加する](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image22.png "既存の項目をコンテンツフォルダーに追加する")</span><span class="sxs-lookup"><span data-stu-id="c925d-362">![Adding an existing item to the Content folder](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image22.png "Adding an existing item to the Content folder")</span></span>

    <span data-ttu-id="c925d-363">*既存の項目をコンテンツフォルダーに追加する*</span><span class="sxs-lookup"><span data-stu-id="c925d-363">*Adding an existing item to the Content folder*</span></span>
2. <span data-ttu-id="c925d-364">**[既存項目の追加]** ダイアログボックスで、 **[ソース/アセット]** フォルダーに移動し、 **[css の反転]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="c925d-364">In the **Add Existing Item** dialog box, navigate to the **Source/Assets** folder and select **Flip.css**.</span></span> <span data-ttu-id="c925d-365">**[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c925d-365">Click **Add**.</span></span>

    <span data-ttu-id="c925d-366">![アセットからのフリップ .css ファイルの追加](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image23.png "アセットからのフリップ .css ファイルの追加")</span><span class="sxs-lookup"><span data-stu-id="c925d-366">![Adding the Flip.css file from Assets](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image23.png "Adding the Flip.css file from Assets")</span></span>

    <span data-ttu-id="c925d-367">*アセットからのフリップ .css ファイルの追加*</span><span class="sxs-lookup"><span data-stu-id="c925d-367">*Adding the Flip.css file from Assets*</span></span>
3. <span data-ttu-id="c925d-368">追加した**フリップ .css**ファイルを開き、その内容を検査します。</span><span class="sxs-lookup"><span data-stu-id="c925d-368">Open the **Flip.css** file you just added and inspect its content.</span></span>
4. <span data-ttu-id="c925d-369">**フリップ変換**のコメントを探します。</span><span class="sxs-lookup"><span data-stu-id="c925d-369">Locate the **flip transformation** comment.</span></span> <span data-ttu-id="c925d-370">このコメントの下にあるスタイルでは、CSS**パースペクティブ**と**rotateY**変換を使用して &quot;カードフリップ&quot; 効果を生成します。</span><span class="sxs-lookup"><span data-stu-id="c925d-370">The styles below that comment use the CSS **perspective** and **rotateY** transformations to generate a &quot;card flip&quot; effect.</span></span>

    [!code-css[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample22.css)]
5. <span data-ttu-id="c925d-371">[**フリップコメント中にウィンドウの背景を非表示にする]** を探します。</span><span class="sxs-lookup"><span data-stu-id="c925d-371">Locate the **hide back of pane during flip** comment.</span></span> <span data-ttu-id="c925d-372">このコメントの下のスタイルでは、 **[背景の表示]** CSS プロパティを [*非表示*] に設定することにより、顔がビューアーから離れているときに、顔の背面が非表示になります。</span><span class="sxs-lookup"><span data-stu-id="c925d-372">The style below that comment hides the back-side of the faces when they are facing away from the viewer by setting the **backface-visibility** CSS property to *hidden*.</span></span>

    [!code-css[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample23.css)]
6. <span data-ttu-id="c925d-373">**App\_Start**フォルダー内の**BundleConfig.cs**ファイルを開き、 **&quot;~/content/Css&quot;** スタイルバンドルに**フリップ .css**ファイルへの参照を追加します。</span><span class="sxs-lookup"><span data-stu-id="c925d-373">Open the **BundleConfig.cs** file inside the **App\_Start** folder and add the reference to the **Flip.css** file in the **&quot;~/Content/css&quot;** style bundle</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample24.cs)]
7. <span data-ttu-id="c925d-374">**F5**キーを押してソリューションを実行し、資格情報でログインします。</span><span class="sxs-lookup"><span data-stu-id="c925d-374">Press **F5** to run the solution and log in with your credentials.</span></span>
8. <span data-ttu-id="c925d-375">いずれかのオプションをクリックして質問に回答します。</span><span class="sxs-lookup"><span data-stu-id="c925d-375">Answer a question by clicking one of the options.</span></span> <span data-ttu-id="c925d-376">ビュー間を切り替えるときのフリップ効果に注意してください。</span><span class="sxs-lookup"><span data-stu-id="c925d-376">Notice the flip effect when transitioning between views.</span></span>

    <span data-ttu-id="c925d-377">![フリップ効果のある質問への回答](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image24.png "フリップ効果のある質問への回答")</span><span class="sxs-lookup"><span data-stu-id="c925d-377">![Answering a question with the flip effect](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image24.png "Answering a question with the flip effect")</span></span>

    <span data-ttu-id="c925d-378">*フリップ効果のある質問への回答*</span><span class="sxs-lookup"><span data-stu-id="c925d-378">*Answering a question with the flip effect*</span></span>
9. <span data-ttu-id="c925d-379">**[次の質問]** をクリックして、次の質問を取得します。</span><span class="sxs-lookup"><span data-stu-id="c925d-379">Click **Next Question** to retrieve the following question.</span></span> <span data-ttu-id="c925d-380">フリップ効果が再び表示されます。</span><span class="sxs-lookup"><span data-stu-id="c925d-380">The flip effect should appear again.</span></span>

    <span data-ttu-id="c925d-381">![フリップ効果で次の質問を取得する](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image25.png "フリップ効果で次の質問を取得する")</span><span class="sxs-lookup"><span data-stu-id="c925d-381">![Retrieving the following question with the flip effect](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image25.png "Retrieving the following question with the flip effect")</span></span>

    <span data-ttu-id="c925d-382">*フリップ効果で次の質問を取得する*</span><span class="sxs-lookup"><span data-stu-id="c925d-382">*Retrieving the following question with the flip effect*</span></span>

---

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="c925d-383">まとめ</span><span class="sxs-lookup"><span data-stu-id="c925d-383">Summary</span></span>

<span data-ttu-id="c925d-384">このハンズオンラボを完了することで、次の方法を学習できました。</span><span class="sxs-lookup"><span data-stu-id="c925d-384">By completing this hands-on lab you have learned how to:</span></span>

- <span data-ttu-id="c925d-385">ASP.NET スキャフォールディングを使用して ASP.NET Web API コントローラーを作成する</span><span class="sxs-lookup"><span data-stu-id="c925d-385">Create an ASP.NET Web API controller using ASP.NET Scaffolding</span></span>
- <span data-ttu-id="c925d-386">Web API の Get アクションを実装して、次のクイズの質問を取得する</span><span class="sxs-lookup"><span data-stu-id="c925d-386">Implement a Web API Get action to retrieve the next quiz question</span></span>
- <span data-ttu-id="c925d-387">クイズの回答を格納するための Web API Post アクションを実装する</span><span class="sxs-lookup"><span data-stu-id="c925d-387">Implement a Web API Post action to store the quiz answers</span></span>
- <span data-ttu-id="c925d-388">Visual Studio パッケージマネージャーコンソールから AngularJS をインストールする</span><span class="sxs-lookup"><span data-stu-id="c925d-388">Install AngularJS from the Visual Studio Package Manager Console</span></span>
- <span data-ttu-id="c925d-389">AngularJS のテンプレートとコントローラーを実装する</span><span class="sxs-lookup"><span data-stu-id="c925d-389">Implement AngularJS templates and controllers</span></span>
- <span data-ttu-id="c925d-390">CSS3 の切り替えを使用してアニメーション効果を行う</span><span class="sxs-lookup"><span data-stu-id="c925d-390">Use CSS3 transitions to perform animation effects</span></span>
