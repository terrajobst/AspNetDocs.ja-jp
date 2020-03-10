---
uid: signalr/overview/getting-started/real-time-web-applications-with-signalr
title: 'ハンズオンラボ: SignalR を使用したリアルタイム Web アプリケーション |Microsoft Docs'
author: bradygaster
description: リアルタイム Web アプリケーションは、接続されているクライアントに対して、リアルタイムでサーバー側のコンテンツをプッシュする機能を備えています。 ASP.NET 開発者向けの ASP...
ms.author: bradyg
ms.date: 07/16/2014
ms.assetid: ba07958c-42e1-4da0-81db-ba6925ed6db0
msc.legacyurl: /signalr/overview/getting-started/real-time-web-applications-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: 9e39fd3f2fc9d4e791002450085215096c222fcd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78431668"
---
# <a name="hands-on-lab-real-time-web-applications-with-signalr"></a><span data-ttu-id="86009-104">ハンズオンラボ: SignalR を使用したリアルタイム Web アプリケーション</span><span class="sxs-lookup"><span data-stu-id="86009-104">Hands On Lab: Real-Time Web Applications with SignalR</span></span>

<span data-ttu-id="86009-105">[Web キャンプチーム](https://twitter.com/webcamps)別</span><span class="sxs-lookup"><span data-stu-id="86009-105">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

[<span data-ttu-id="86009-106">Web キャンプトレーニングキットのダウンロード (2015 年10月リリース)</span><span class="sxs-lookup"><span data-stu-id="86009-106">Download Web Camps Training Kit, October 2015 Release</span></span>](https://github.com/Microsoft-Web/WebCampTrainingKit/releases/tag/v2015.10.13b)

> <span data-ttu-id="86009-107">リアルタイム Web アプリケーションは、接続されているクライアントに対して、リアルタイムでサーバー側のコンテンツをプッシュする機能を備えています。</span><span class="sxs-lookup"><span data-stu-id="86009-107">Real-time Web applications feature the ability to push server-side content to the connected clients as it happens, in real-time.</span></span> <span data-ttu-id="86009-108">ASP.NET 開発者にとって、 **ASP.NET SignalR**は、リアルタイム web 機能をアプリケーションに追加するためのライブラリです。</span><span class="sxs-lookup"><span data-stu-id="86009-108">For ASP.NET developers, **ASP.NET SignalR** is a library to add real-time web functionality to their applications.</span></span> <span data-ttu-id="86009-109">複数のトランスポートを利用し、クライアントおよびサーバーの最適なトランスポートを指定して、最適なトランスポートを自動的に選択します。</span><span class="sxs-lookup"><span data-stu-id="86009-109">It takes advantage of several transports, automatically selecting the best available transport given the client and server's best available transport.</span></span> <span data-ttu-id="86009-110">これは、ブラウザーとサーバー間の双方向通信を可能にする HTML5 API である**WebSocket**を利用します。</span><span class="sxs-lookup"><span data-stu-id="86009-110">It takes advantage of **WebSocket**, an HTML5 API that enables bi-directional communication between the browser and server.</span></span>
> 
> <span data-ttu-id="86009-111">また、 **SignalR**は、ASP.NET アプリケーションでサーバーとクライアントの RPC を実行するための単純な高レベルの API (サーバー側の .net コードからクライアントのブラウザーで JavaScript 関数を呼び出す) を提供するだけでなく、接続/切断イベント、グループ化接続、承認など、接続管理のための便利なフックを追加します。</span><span class="sxs-lookup"><span data-stu-id="86009-111">**SignalR** also provides a simple, high-level API for doing server to client RPC (call JavaScript functions in your clients' browsers from server-side .NET code) in your ASP.NET application, as well as adding useful hooks for connection management, such as connect/disconnect events, grouping connections, and authorization.</span></span>
> 
> <span data-ttu-id="86009-112">**SignalR**は、クライアントとサーバー間でリアルタイムの作業を行うために必要なトランスポートの一部を抽象化したものです。</span><span class="sxs-lookup"><span data-stu-id="86009-112">**SignalR** is an abstraction over some of the transports that are required to do real-time work between client and server.</span></span> <span data-ttu-id="86009-113">**SignalR**接続は HTTP として起動し、使用可能な場合は**WebSocket**接続に昇格されます。</span><span class="sxs-lookup"><span data-stu-id="86009-113">A **SignalR** connection starts as HTTP, and is then promoted to a **WebSocket** connection if available.</span></span> <span data-ttu-id="86009-114">**Websocket**は**SignalR**に最適なトランスポートです。これは、サーバーのメモリを最も効率的に使用し、待機時間が最も短く、最も基本的な機能 (クライアントとサーバー間の完全な双方向通信など) を備えているためです。 **websocket**では、サーバーが**windows server 2012**または**windows 8**を使用している必要がありますが、 **.NET Framework 4.5**。</span><span class="sxs-lookup"><span data-stu-id="86009-114">**WebSocket** is the ideal transport for **SignalR**, since it makes the most efficient use of server memory, has the lowest latency, and has the most underlying features (such as full duplex communication between client and server), but it also has the most stringent requirements: **WebSocket** requires the server to be using **Windows Server 2012** or **Windows 8**, along with **.NET Framework 4.5**.</span></span> <span data-ttu-id="86009-115">これらの要件が満たされていない場合、 **SignalR**は他のトランスポートを使用して接続しようとします ( *Ajax 長時間ポーリング*など)。</span><span class="sxs-lookup"><span data-stu-id="86009-115">If these requirements are not met, **SignalR** will attempt to use other transports to make its connections (like *Ajax long polling*).</span></span>
> 
> <span data-ttu-id="86009-116">**SignalR** API には、クライアントとサーバー間の通信用に、**永続的な接続**と**ハブ**の2つのモデルが含まれています。</span><span class="sxs-lookup"><span data-stu-id="86009-116">The **SignalR** API contains two models for communicating between clients and servers: **Persistent Connections** and **Hubs**.</span></span> <span data-ttu-id="86009-117">**接続**は、単一受信者、グループ化、またはブロードキャストメッセージを送信するための単純なエンドポイントを表します。</span><span class="sxs-lookup"><span data-stu-id="86009-117">A **Connection** represents a simple endpoint for sending single-recipient, grouped, or broadcast messages.</span></span> <span data-ttu-id="86009-118">**ハブ**は、接続 API に基づいて構築されたより高度なパイプラインで、クライアントとサーバーが互いにメソッドを直接呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="86009-118">A **Hub** is a more high-level pipeline built upon the Connection API that allows your client and server to call methods on each other directly.</span></span>
> 
> ![SignalR アーキテクチャ](real-time-web-applications-with-signalr/_static/image1.png)
> 
> <span data-ttu-id="86009-120">すべてのサンプルコードとスニペットは、 [https://github.com/Microsoft-Web/WebCampTrainingKit/releases/tag/v2015.10.13b](https://github.com/Microsoft-Web/WebCampTrainingKit/releases/tag/v2015.10.13b)で提供される2015年10月リリースの Web キャンプトレーニングキットに含まれています。</span><span class="sxs-lookup"><span data-stu-id="86009-120">All sample code and snippets are included in the Web Camps Training Kit, October 2015 Release, available at [https://github.com/Microsoft-Web/WebCampTrainingKit/releases/tag/v2015.10.13b](https://github.com/Microsoft-Web/WebCampTrainingKit/releases/tag/v2015.10.13b).</span></span>  <span data-ttu-id="86009-121">このページのインストーラーのリンクは機能しなくなっていることに注意してください。代わりに、Assets セクションの下にあるいずれかのリンクを使用してください。</span><span class="sxs-lookup"><span data-stu-id="86009-121">Please note that the Installer link on that page no longer works; use one of the links under the Assets section instead.</span></span>

<a id="Overview"></a>
## <a name="overview"></a><span data-ttu-id="86009-122">概要</span><span class="sxs-lookup"><span data-stu-id="86009-122">Overview</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="86009-123">目標</span><span class="sxs-lookup"><span data-stu-id="86009-123">Objectives</span></span>

<span data-ttu-id="86009-124">このハンズオンラボでは、次の方法を学習します。</span><span class="sxs-lookup"><span data-stu-id="86009-124">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="86009-125">SignalR を使用して、サーバーからクライアントに通知を送信します。</span><span class="sxs-lookup"><span data-stu-id="86009-125">Send notifications from server to client using SignalR.</span></span>
- <span data-ttu-id="86009-126">**SQL Server**を使用して SignalR アプリケーションを Scale Out します。</span><span class="sxs-lookup"><span data-stu-id="86009-126">Scale Out your SignalR application using **SQL Server**.</span></span>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="86009-127">前提条件</span><span class="sxs-lookup"><span data-stu-id="86009-127">Prerequisites</span></span>

<span data-ttu-id="86009-128">このハンズオンラボを完了するには、次のものが必要です。</span><span class="sxs-lookup"><span data-stu-id="86009-128">The following is required to complete this hands-on lab:</span></span>

- <span data-ttu-id="86009-129">[Web 用に2013を Visual Studio Express](https://www.microsoft.com/visualstudio/)</span><span class="sxs-lookup"><span data-stu-id="86009-129">[Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/) or greater</span></span>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="86009-130">セットアップ</span><span class="sxs-lookup"><span data-stu-id="86009-130">Setup</span></span>

<span data-ttu-id="86009-131">このハンズオンラボの演習を実行するには、まず環境をセットアップする必要があります。</span><span class="sxs-lookup"><span data-stu-id="86009-131">In order to run the exercises in this hands-on lab, you will need to set up your environment first.</span></span>

1. <span data-ttu-id="86009-132">Windows エクスプローラーウィンドウを開き、ラボの**ソース**フォルダーを参照します。</span><span class="sxs-lookup"><span data-stu-id="86009-132">Open a Windows Explorer window and browse to the lab's **Source** folder.</span></span>
2. <span data-ttu-id="86009-133">**[Setup.exe]** を右クリックし、 **[管理者として実行]** を選択して、環境を構成し、このラボ用の Visual Studio コードスニペットをインストールするセットアッププロセスを開始します。</span><span class="sxs-lookup"><span data-stu-id="86009-133">Right-click **Setup.cmd** and select **Run as administrator** to launch the setup process that will configure your environment and install the Visual Studio code snippets for this lab.</span></span>
3. <span data-ttu-id="86009-134">ユーザー アカウント制御ダイアログ ボックスが表示されている場合は、続行するアクションを確認します。</span><span class="sxs-lookup"><span data-stu-id="86009-134">If the User Account Control dialog box is shown, confirm the action to proceed.</span></span>

> [!NOTE]
> <span data-ttu-id="86009-135">セットアップを実行する前に、このラボのすべての依存関係を確認していることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="86009-135">Make sure you have checked all the dependencies for this lab before running the setup.</span></span>

<a id="CodeSnippets"></a>
### <a name="using-the-code-snippets"></a><span data-ttu-id="86009-136">コードスニペットの使用</span><span class="sxs-lookup"><span data-stu-id="86009-136">Using the Code Snippets</span></span>

<span data-ttu-id="86009-137">ラボドキュメント全体で、コードブロックを挿入するように指示されます。</span><span class="sxs-lookup"><span data-stu-id="86009-137">Throughout the lab document, you will be instructed to insert code blocks.</span></span> <span data-ttu-id="86009-138">便宜上、このコードのほとんどは Visual Studio Code のスニペットとして提供されており、Visual Studio 2013 内からアクセスして、手動で追加する必要がないようにすることができます。</span><span class="sxs-lookup"><span data-stu-id="86009-138">For your convenience, most of this code is provided as Visual Studio Code Snippets, which you can access from within Visual Studio 2013 to avoid having to add it manually.</span></span>

> [!NOTE]
> <span data-ttu-id="86009-139">各演習には、演習の**Begin**フォルダーに配置された開始ソリューションが付属しています。これにより、各演習を別の手順に従って実行することができます。</span><span class="sxs-lookup"><span data-stu-id="86009-139">Each exercise is accompanied by a starting solution located in the **Begin** folder of the exercise that allows you to follow each exercise independently of the others.</span></span> <span data-ttu-id="86009-140">演習中に追加されたコードスニペットは、これらの開始ソリューションにはないため、演習を完了するまで機能しないことがあります。</span><span class="sxs-lookup"><span data-stu-id="86009-140">Please be aware that the code snippets that are added during an exercise are missing from these starting solutions and may not work until you have completed the exercise.</span></span> <span data-ttu-id="86009-141">演習用のソースコード内では、対応する演習の手順を完了した結果として得られるコードを使用して、Visual Studio ソリューションを含む**終了**フォルダーも検索します。</span><span class="sxs-lookup"><span data-stu-id="86009-141">Inside the source code for an exercise, you will also find an **End** folder containing a Visual Studio solution with the code that results from completing the steps in the corresponding exercise.</span></span> <span data-ttu-id="86009-142">このハンズオンラボを使用して作業する際に、追加のヘルプが必要な場合は、これらのソリューションをガイダンスとして使用できます。</span><span class="sxs-lookup"><span data-stu-id="86009-142">You can use these solutions as guidance if you need additional help as you work through this hands-on lab.</span></span>

---

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="86009-143">手順</span><span class="sxs-lookup"><span data-stu-id="86009-143">Exercises</span></span>

<span data-ttu-id="86009-144">このハンズオンラボには、次の演習が含まれています。</span><span class="sxs-lookup"><span data-stu-id="86009-144">This hands-on lab includes the following exercises:</span></span>

1. [<span data-ttu-id="86009-145">SignalR を使用したリアルタイムデータの操作</span><span class="sxs-lookup"><span data-stu-id="86009-145">Working with Real-Time Data Using SignalR</span></span>](#Exercise1)
2. [<span data-ttu-id="86009-146">SQL Server を使用したスケールアウト</span><span class="sxs-lookup"><span data-stu-id="86009-146">Scaling Out Using SQL Server</span></span>](#Exercise2)

<span data-ttu-id="86009-147">このラボの推定所要時間: **60 分**</span><span class="sxs-lookup"><span data-stu-id="86009-147">Estimated time to complete this lab: **60 minutes**</span></span>

> [!NOTE]
> <span data-ttu-id="86009-148">Visual Studio を初めて起動するときに、定義済みの設定コレクションのいずれかを選択する必要があります。</span><span class="sxs-lookup"><span data-stu-id="86009-148">When you first start Visual Studio, you must select one of the predefined settings collections.</span></span> <span data-ttu-id="86009-149">定義済みの各コレクションは、特定の開発スタイルに一致するように設計されており、ウィンドウのレイアウト、エディターの動作、IntelliSense コードスニペット、およびダイアログボックスのオプションを決定します。</span><span class="sxs-lookup"><span data-stu-id="86009-149">Each predefined collection is designed to match a particular development style and determines window layouts, editor behavior, IntelliSense code snippets, and dialog box options.</span></span> <span data-ttu-id="86009-150">このラボの手順では、**全般的な開発設定**のコレクションを使用するときに、Visual Studio で特定のタスクを実行するために必要なアクションについて説明します。</span><span class="sxs-lookup"><span data-stu-id="86009-150">The procedures in this lab describe the actions necessary to accomplish a given task in Visual Studio when using the **General Development Settings** collection.</span></span> <span data-ttu-id="86009-151">開発環境に対して別の設定コレクションを選択した場合は、注意が必要な手順が異なる場合があります。</span><span class="sxs-lookup"><span data-stu-id="86009-151">If you choose a different settings collection for your development environment, there may be differences in the steps that you should take into account.</span></span>

<a id="Exercise1"></a>
### <a name="exercise-1-working-with-real-time-data-using-signalr"></a><span data-ttu-id="86009-152">演習 1: SignalR を使用したリアルタイムデータの操作</span><span class="sxs-lookup"><span data-stu-id="86009-152">Exercise 1: Working with Real-Time Data Using SignalR</span></span>

<span data-ttu-id="86009-153">チャットは例としてよく使用されますが、リアルタイムの Web 機能を使用して、さらに多くのことを行うことができます。</span><span class="sxs-lookup"><span data-stu-id="86009-153">While chat is often used as an example, you can do a whole lot more with real-time Web functionality.</span></span> <span data-ttu-id="86009-154">ユーザーが web ページを更新して新しいデータを表示したり、新しいデータを取得するために Ajax 長いポーリングを実装するたびに、SignalR を使用することができます。</span><span class="sxs-lookup"><span data-stu-id="86009-154">Any time a user refreshes a web page to see new data or the page implements Ajax long polling to retrieve new data, you can use SignalR.</span></span>

<span data-ttu-id="86009-155">SignalR は**サーバープッシュ**または**ブロードキャスト**機能をサポートしています。接続管理は自動的に処理されます。</span><span class="sxs-lookup"><span data-stu-id="86009-155">SignalR supports **server push** or **broadcasting** functionality; it handles connection management automatically.</span></span> <span data-ttu-id="86009-156">クライアントとサーバー間の通信に対する従来の HTTP 接続では、要求ごとに接続が再確立されますが、SignalR はクライアントとサーバー間の永続的な接続を提供します。</span><span class="sxs-lookup"><span data-stu-id="86009-156">In classic HTTP connections for client-server communication, connection is re-established for each request, but SignalR provides persistent connection between the client and server.</span></span> <span data-ttu-id="86009-157">SignalR では、サーバーコードは、現在知られている要求-応答モデルではなく、リモートプロシージャコール (RPC) を使用してブラウザーでクライアントコードを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="86009-157">In SignalR the server code calls out to a client code in the browser using Remote Procedure Calls (RPC), rather than the request-response model we know today.</span></span>

<span data-ttu-id="86009-158">この演習では、SignalR を使用して統計ダッシュボードと更新されたメトリックを表示するように**マニアクイズ**アプリケーションを構成します。ページ全体を更新する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="86009-158">In this exercise, you will configure the **Geek Quiz** application to use SignalR to display the Statistics dashboard with the updated metrics without the need to refresh the entire page.</span></span>

<a id="Ex1Task1"></a>
#### <a name="task-1--exploring-the-geek-quiz-statistics-page"></a><span data-ttu-id="86009-159">タスク1–マニアクイズ統計ページを調べる</span><span class="sxs-lookup"><span data-stu-id="86009-159">Task 1 – Exploring the Geek Quiz Statistics Page</span></span>

<span data-ttu-id="86009-160">このタスクでは、アプリケーションを実行し、統計ページがどのように表示されるか、および情報の更新方法を改善する方法を確認します。</span><span class="sxs-lookup"><span data-stu-id="86009-160">In this task, you will go through the application and verify how the statistics page is shown and how you can improve the way the information is updated.</span></span>

1. <span data-ttu-id="86009-161">**Web 用 Visual Studio Express 2013**を開き、 **Source\Ex1-WorkingWithRealTimeData\Begin**フォルダーにある**GeekQuiz**ソリューションを開きます。</span><span class="sxs-lookup"><span data-stu-id="86009-161">Open **Visual Studio Express 2013 for Web** and open the **GeekQuiz.sln** solution located in the **Source\Ex1-WorkingWithRealTimeData\Begin** folder.</span></span>
2. <span data-ttu-id="86009-162">F5 キーを押して、ソリューションを実行します。</span><span class="sxs-lookup"><span data-stu-id="86009-162">Press **F5** to run the solution.</span></span> <span data-ttu-id="86009-163">ブラウザーに**ログイン**ページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="86009-163">The **Log in** page should appear in the browser.</span></span>

    <span data-ttu-id="86009-164">![ソリューションの実行](real-time-web-applications-with-signalr/_static/image2.png "ソリューションの実行")</span><span class="sxs-lookup"><span data-stu-id="86009-164">![Running the solution](real-time-web-applications-with-signalr/_static/image2.png "Running the solution")</span></span>

    <span data-ttu-id="86009-165">*ソリューションの実行*</span><span class="sxs-lookup"><span data-stu-id="86009-165">*Running the solution*</span></span>
3. <span data-ttu-id="86009-166">ページの右上隅にある **[登録]** をクリックして、アプリケーションに新しいユーザーを作成します。</span><span class="sxs-lookup"><span data-stu-id="86009-166">Click **Register** in the upper-right corner of the page to create a new user in the application.</span></span>

    <span data-ttu-id="86009-167">![リンクの登録](real-time-web-applications-with-signalr/_static/image3.png "リンクの登録")</span><span class="sxs-lookup"><span data-stu-id="86009-167">![Register link](real-time-web-applications-with-signalr/_static/image3.png "Register link")</span></span>

    <span data-ttu-id="86009-168">*リンクの登録*</span><span class="sxs-lookup"><span data-stu-id="86009-168">*Register link*</span></span>
4. <span data-ttu-id="86009-169">**[登録]** ページで、**ユーザー名**と**パスワード**を入力し、 **[登録]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="86009-169">In the **Register** page, enter a **User name** and **Password**, and then click **Register**.</span></span>

    <span data-ttu-id="86009-170">![ユーザーの登録](real-time-web-applications-with-signalr/_static/image4.png "ユーザーの登録")</span><span class="sxs-lookup"><span data-stu-id="86009-170">![Registering a user](real-time-web-applications-with-signalr/_static/image4.png "Registering a user")</span></span>

    <span data-ttu-id="86009-171">*ユーザーの登録*</span><span class="sxs-lookup"><span data-stu-id="86009-171">*Registering a user*</span></span>
5. <span data-ttu-id="86009-172">アプリケーションは新しいアカウントを登録し、ユーザーは認証されて、最初のクイズの質問を示すホームページにリダイレクトされます。</span><span class="sxs-lookup"><span data-stu-id="86009-172">The application registers the new account and the user is authenticated and redirected back to the home page showing the first quiz question.</span></span>
6. <span data-ttu-id="86009-173">新しいウィンドウで **[統計]** ページを開き、[**ホーム**ページと**統計情報**] ページを横に並べて表示します。</span><span class="sxs-lookup"><span data-stu-id="86009-173">Open the **Statistics** page in a new window and put the **Home** page and **Statistics** page side-by-side.</span></span>

    <span data-ttu-id="86009-174">![サイドバイサイドウィンドウ](real-time-web-applications-with-signalr/_static/image5.png "サイドバイサイドウィンドウ")</span><span class="sxs-lookup"><span data-stu-id="86009-174">![Side-by-side windows](real-time-web-applications-with-signalr/_static/image5.png "Side by side windows")</span></span>

    <span data-ttu-id="86009-175">*サイドバイサイドウィンドウ*</span><span class="sxs-lookup"><span data-stu-id="86009-175">*Side-by-side windows*</span></span>
7. <span data-ttu-id="86009-176">**ホーム**ページで、いずれかのオプションをクリックして質問に回答します。</span><span class="sxs-lookup"><span data-stu-id="86009-176">In the **Home** page, answer the question by clicking one of the options.</span></span>

    <span data-ttu-id="86009-177">![質問への回答](real-time-web-applications-with-signalr/_static/image6.png "質問への回答")</span><span class="sxs-lookup"><span data-stu-id="86009-177">![Answering a question](real-time-web-applications-with-signalr/_static/image6.png "Answering a question")</span></span>

    <span data-ttu-id="86009-178">*質問への回答*</span><span class="sxs-lookup"><span data-stu-id="86009-178">*Answering a question*</span></span>
8. <span data-ttu-id="86009-179">いずれかのボタンをクリックすると、回答が表示されます。</span><span class="sxs-lookup"><span data-stu-id="86009-179">After clicking one of the buttons, the answer should appear.</span></span>

    <span data-ttu-id="86009-180">![回答が正しい質問](real-time-web-applications-with-signalr/_static/image7.png "回答が正しい質問")</span><span class="sxs-lookup"><span data-stu-id="86009-180">![Question answered correct](real-time-web-applications-with-signalr/_static/image7.png "Question answered correct")</span></span>

    <span data-ttu-id="86009-181">*質問に正しく回答*</span><span class="sxs-lookup"><span data-stu-id="86009-181">*Question answered correctly*</span></span>
9. <span data-ttu-id="86009-182">[統計] ページに表示される情報が古くなっていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="86009-182">Notice that the information provided in the Statistics page is outdated.</span></span> <span data-ttu-id="86009-183">更新された結果を表示するためにページを更新します。</span><span class="sxs-lookup"><span data-stu-id="86009-183">Refresh the page in order to see the updated results.</span></span>

    <span data-ttu-id="86009-184">![[統計] ページ](real-time-web-applications-with-signalr/_static/image8.png "[統計] ページ")</span><span class="sxs-lookup"><span data-stu-id="86009-184">![Statistics page](real-time-web-applications-with-signalr/_static/image8.png "Statistics page")</span></span>

    <span data-ttu-id="86009-185">*[統計] ページ*</span><span class="sxs-lookup"><span data-stu-id="86009-185">*Statistics page*</span></span>
10. <span data-ttu-id="86009-186">Visual Studio に戻り、デバッグを停止します。</span><span class="sxs-lookup"><span data-stu-id="86009-186">Go back to Visual Studio and stop debugging.</span></span>

<a id="Ex1Task2"></a>
#### <a name="task-2--adding-signalr-to-geek-quiz-to-show-online-charts"></a><span data-ttu-id="86009-187">タスク2–マニアクイズに SignalR を追加してオンライングラフを表示する</span><span class="sxs-lookup"><span data-stu-id="86009-187">Task 2 – Adding SignalR to Geek Quiz to Show Online Charts</span></span>

<span data-ttu-id="86009-188">このタスクでは、SignalR をソリューションに追加し、新しい回答がサーバーに送信されたときにクライアントに自動的に更新を送信します。</span><span class="sxs-lookup"><span data-stu-id="86009-188">In this task, you will add SignalR to the solution and send updates to the clients automatically when a new answer is sent to the server.</span></span>

1. <span data-ttu-id="86009-189">Visual Studio の **[ツール]** メニューで、 **[NuGet パッケージマネージャー]** を選択し、 **[パッケージマネージャーコンソール]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="86009-189">From the **Tools** menu in Visual Studio, select **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>
2. <span data-ttu-id="86009-190">**[パッケージマネージャーコンソール]** ウィンドウで、次のコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="86009-190">In the **Package Manager Console** window, execute the following command:</span></span>

    [!code-powershell[Main](real-time-web-applications-with-signalr/samples/sample1.ps1)]

    <span data-ttu-id="86009-191">![SignalR パッケージのインストール](real-time-web-applications-with-signalr/_static/image9.png "SignalR パッケージのインストール")</span><span class="sxs-lookup"><span data-stu-id="86009-191">![SignalR package installation](real-time-web-applications-with-signalr/_static/image9.png "SignalR package installation")</span></span>

    <span data-ttu-id="86009-192">*SignalR パッケージのインストール*</span><span class="sxs-lookup"><span data-stu-id="86009-192">*SignalR package installation*</span></span>

   > [!NOTE]
   > <span data-ttu-id="86009-193">新しい MVC 5 アプリケーションから**SignalR** NuGet パッケージバージョン2.0.2 をインストールする場合は、SignalR をインストールする前に**OWIN**パッケージをバージョン 2.0.1 (またはそれ以降) に手動で更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="86009-193">When installing **SignalR** NuGet packages version 2.0.2 from a brand new MVC 5 application, you will need to manually update **OWIN** packages to version 2.0.1 (or higher) before installing SignalR.</span></span> <span data-ttu-id="86009-194">これを行うには、**パッケージマネージャーコンソール**で次のスクリプトを実行します。</span><span class="sxs-lookup"><span data-stu-id="86009-194">To do this, you can execute the following script in the **Package Manager Console**:</span></span>
   > 
   > [!code-powershell[Main](real-time-web-applications-with-signalr/samples/sample2.ps1)]
   > 
   > <span data-ttu-id="86009-195">SignalR の今後のリリースでは、OWIN の依存関係が自動的に更新されます。</span><span class="sxs-lookup"><span data-stu-id="86009-195">In a future release of SignalR, OWIN dependencies will be automatically updated.</span></span>
3. <span data-ttu-id="86009-196">**ソリューションエクスプローラー**で、 **Scripts**フォルダーを展開し、SignalR *js*ファイルがソリューションに追加されたことを確認します。</span><span class="sxs-lookup"><span data-stu-id="86009-196">In **Solution Explorer**, expand the **Scripts** folder and notice that the SignalR *js* files were added to the solution.</span></span>

    <span data-ttu-id="86009-197">![SignalR JavaScript の参照](real-time-web-applications-with-signalr/_static/image10.png "SignalR JavaScript の参照")</span><span class="sxs-lookup"><span data-stu-id="86009-197">![SignalR JavaScript references](real-time-web-applications-with-signalr/_static/image10.png "SignalR JavaScript references")</span></span>

    <span data-ttu-id="86009-198">*SignalR JavaScript の参照*</span><span class="sxs-lookup"><span data-stu-id="86009-198">*SignalR JavaScript references*</span></span>
4. <span data-ttu-id="86009-199">**ソリューションエクスプローラー**で、 **GeekQuiz**プロジェクトを右クリックし、 **[追加]** [ | **新しいフォルダー**] の順に選択して、**ハブ**に名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="86009-199">In **Solution Explorer**, right-click the **GeekQuiz** project, select **Add** | **New Folder**, and name it **Hubs**.</span></span>
5. <span data-ttu-id="86009-200">**ハブ** フォルダーを右クリックし、追加 を選択します。 **新しい項目**。</span><span class="sxs-lookup"><span data-stu-id="86009-200">Right-click the **Hubs** folder and select **Add | New Item**.</span></span>

    <span data-ttu-id="86009-201">![新しい項目の追加](real-time-web-applications-with-signalr/_static/image11.png "新しい項目の追加")</span><span class="sxs-lookup"><span data-stu-id="86009-201">![Add new item](real-time-web-applications-with-signalr/_static/image11.png "Add new item")</span></span>

    <span data-ttu-id="86009-202">*新しい項目の追加*</span><span class="sxs-lookup"><span data-stu-id="86009-202">*Add new item*</span></span>
6. <span data-ttu-id="86009-203">**[新しい項目の追加]** ダイアログボックスで、 **[ C# Visual |] を選択します。Web |SignalR**ノード左側のウィンドウで、中央のウィンドウから **[SignalR Hub クラス (v2)]** を選択し、ファイルに**StatisticsHub.cs**という名前を指定して、 **[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="86009-203">In the **Add New Item** dialog box, select the **Visual C# | Web | SignalR** node in the left pane, select **SignalR Hub Class (v2)** from the center pane, name the file **StatisticsHub.cs** and click **Add**.</span></span>

    <span data-ttu-id="86009-204">![[新しい項目の追加] ダイアログボックス](real-time-web-applications-with-signalr/_static/image12.png "[新しい項目の追加] ダイアログボックス")</span><span class="sxs-lookup"><span data-stu-id="86009-204">![Add new item dialog box](real-time-web-applications-with-signalr/_static/image12.png "Add new item dialog box")</span></span>

    <span data-ttu-id="86009-205">*[新しい項目の追加] ダイアログボックス*</span><span class="sxs-lookup"><span data-stu-id="86009-205">*Add new item dialog box*</span></span>
7. <span data-ttu-id="86009-206">**StatisticsHub**クラスのコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="86009-206">Replace the code in the **StatisticsHub** class with the following code.</span></span>

    <span data-ttu-id="86009-207">(コードスニペット- *Realtimesignalr-Ex1-StatisticsHubClass*)</span><span class="sxs-lookup"><span data-stu-id="86009-207">(Code Snippet - *RealTimeSignalR - Ex1 - StatisticsHubClass*)</span></span>

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample3.cs)]
8. <span data-ttu-id="86009-208">**Startup.cs**を開き、**構成**メソッドの末尾に次の行を追加します。</span><span class="sxs-lookup"><span data-stu-id="86009-208">Open **Startup.cs** and add the following line at the end of the **Configuration** method.</span></span>

    <span data-ttu-id="86009-209">(コードスニペット- *Realtimesignalr-Ex1-MapSignalR*)</span><span class="sxs-lookup"><span data-stu-id="86009-209">(Code Snippet - *RealTimeSignalR - Ex1 - MapSignalR*)</span></span>

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample4.cs)]
9. <span data-ttu-id="86009-210">**Services**フォルダー内の**StatisticsService.cs**ページを開き、次の using ディレクティブを追加します。</span><span class="sxs-lookup"><span data-stu-id="86009-210">Open the **StatisticsService.cs** page inside the **Services** folder and add the following using directives.</span></span>

    <span data-ttu-id="86009-211">(コードスニペット- *Realtimesignalr-Ex1 ディレクティブ*)</span><span class="sxs-lookup"><span data-stu-id="86009-211">(Code Snippet - *RealTimeSignalR - Ex1 - UsingDirectives*)</span></span>

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample5.cs)]
10. <span data-ttu-id="86009-212">接続しているクライアントに更新プログラムを通知するには、最初に現在の接続の**コンテキスト**オブジェクトを取得します。</span><span class="sxs-lookup"><span data-stu-id="86009-212">To notify connected clients of updates, you first retrieve a **Context** object for the current connection.</span></span> <span data-ttu-id="86009-213">**ハブ**オブジェクトには、1つのクライアントにメッセージを送信したり、接続されているすべてのクライアントにブロードキャストしたりするメソッドが含まれています。</span><span class="sxs-lookup"><span data-stu-id="86009-213">The **Hub** object contains methods to send messages to a single client or broadcast to all connected clients.</span></span> <span data-ttu-id="86009-214">次のメソッドを**StatisticsService**クラスに追加して、統計データをブロードキャストします。</span><span class="sxs-lookup"><span data-stu-id="86009-214">Add the following method to the **StatisticsService** class to broadcast the statistics data.</span></span>

    <span data-ttu-id="86009-215">(コードスニペット- *Realtimesignalr-Ex1-NotifyUpdatesMethod*)</span><span class="sxs-lookup"><span data-stu-id="86009-215">(Code Snippet - *RealTimeSignalR - Ex1 - NotifyUpdatesMethod*)</span></span>

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample6.cs)]

    > [!NOTE]
    > <span data-ttu-id="86009-216">上記のコードでは、任意のメソッド名を使用してクライアント上の関数を呼び出しています (つまり、 *updateStatistics*)。</span><span class="sxs-lookup"><span data-stu-id="86009-216">In the code above, you are using an arbitrary method name to call a function on the client (i.e.: *updateStatistics*).</span></span> <span data-ttu-id="86009-217">指定したメソッド名は動的オブジェクトとして解釈されます。つまり、IntelliSense やコンパイル時の検証は行われません。</span><span class="sxs-lookup"><span data-stu-id="86009-217">The method name that you specify is interpreted as a dynamic object, which means there is no IntelliSense or compile-time validation for it.</span></span> <span data-ttu-id="86009-218">式は実行時に評価されます。</span><span class="sxs-lookup"><span data-stu-id="86009-218">The expression is evaluated at run time.</span></span> <span data-ttu-id="86009-219">メソッドの呼び出しが実行されると、SignalR はメソッド名とパラメーター値をクライアントに送信します。</span><span class="sxs-lookup"><span data-stu-id="86009-219">When the method call executes, SignalR sends the method name and the parameter values to the client.</span></span> <span data-ttu-id="86009-220">クライアントに名前と一致するメソッドがある場合、そのメソッドが呼び出され、パラメーター値が渡されます。</span><span class="sxs-lookup"><span data-stu-id="86009-220">If the client has a method that matches the name, that method is called and the parameter values are passed to it.</span></span> <span data-ttu-id="86009-221">一致するメソッドがクライアントに見つからない場合、エラーは発生しません。</span><span class="sxs-lookup"><span data-stu-id="86009-221">If no matching method is found on the client, no error is raised.</span></span> <span data-ttu-id="86009-222">詳細については、 [ASP.NET SignalR HUB API ガイド](../guide-to-the-api/hubs-api-guide-server.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="86009-222">For more information, refer to [ASP.NET SignalR Hubs API Guide](../guide-to-the-api/hubs-api-guide-server.md).</span></span>
11. <span data-ttu-id="86009-223">**Controllers**フォルダー内の**TriviaController.cs**ページを開き、次の using ディレクティブを追加します。</span><span class="sxs-lookup"><span data-stu-id="86009-223">Open the **TriviaController.cs** page inside the **Controllers** folder and add the following using directives.</span></span>

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample7.cs)]
12. <span data-ttu-id="86009-224">次の強調表示されたコードを**Post**アクションメソッドに追加します。</span><span class="sxs-lookup"><span data-stu-id="86009-224">Add the following highlighted code to the **Post** action method.</span></span>

    <span data-ttu-id="86009-225">(コードスニペット- *Realtimesignalr-Ex1-Notifyアップデートの呼び出し*)</span><span class="sxs-lookup"><span data-stu-id="86009-225">(Code Snippet - *RealTimeSignalR - Ex1 - NotifyUpdatesCall*)</span></span>

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample8.cs)]
13. <span data-ttu-id="86009-226">ビュー内の Statistics ページを開きます **。** **ホーム**フォルダー。</span><span class="sxs-lookup"><span data-stu-id="86009-226">Open the **Statistics.cshtml** page inside the **Views | Home** folder.</span></span> <span data-ttu-id="86009-227">**Scripts**セクションを見つけて、セクションの先頭に次のスクリプト参照を追加します。</span><span class="sxs-lookup"><span data-stu-id="86009-227">Locate the **Scripts** section and add the following script references at the beginning of the section.</span></span>

    <span data-ttu-id="86009-228">(コードスニペット- *Realtimesignalr-Ex1-SignalRScriptReferences*)</span><span class="sxs-lookup"><span data-stu-id="86009-228">(Code Snippet - *RealTimeSignalR - Ex1 - SignalRScriptReferences*)</span></span>

    [!code-cshtml[Main](real-time-web-applications-with-signalr/samples/sample9.cshtml)]

    > [!NOTE]
    > <span data-ttu-id="86009-229">SignalR およびその他のスクリプトライブラリを Visual Studio プロジェクトに追加すると、パッケージマネージャーによって、このトピックに示されているバージョンよりも新しいバージョンの SignalR スクリプトファイルがインストールされる場合があります。</span><span class="sxs-lookup"><span data-stu-id="86009-229">When you add SignalR and other script libraries to your Visual Studio project, the Package Manager might install a version of the SignalR script file that is more recent than the version shown in this topic.</span></span> <span data-ttu-id="86009-230">コード内のスクリプト参照が、プロジェクトにインストールされているスクリプトライブラリのバージョンと一致していることを確認します。</span><span class="sxs-lookup"><span data-stu-id="86009-230">Make sure that the script reference in your code matches the version of the script library installed in your project.</span></span>
14. <span data-ttu-id="86009-231">クライアントを SignalR hub に接続し、ハブから新しいメッセージを受信したときに統計データを更新するために、次の強調表示されたコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="86009-231">Add the following highlighted code to connect the client to the SignalR hub and update the statistics data when a new message is received from the hub.</span></span>

    <span data-ttu-id="86009-232">(コードスニペット- *Realtimesignalr-Ex1-SignalRClientCode*)</span><span class="sxs-lookup"><span data-stu-id="86009-232">(Code Snippet - *RealTimeSignalR - Ex1 - SignalRClientCode*)</span></span>

    [!code-cshtml[Main](real-time-web-applications-with-signalr/samples/sample10.cshtml)]

    <span data-ttu-id="86009-233">このコードでは、ハブプロキシを作成し、サーバーから送信されたメッセージをリッスンするイベントハンドラーを登録します。</span><span class="sxs-lookup"><span data-stu-id="86009-233">In this code, you are creating a Hub Proxy and registering an event handler to listen for messages sent by the server.</span></span> <span data-ttu-id="86009-234">この場合は、 *updateStatistics*メソッドを介して送信されたメッセージをリッスンします。</span><span class="sxs-lookup"><span data-stu-id="86009-234">In this case, you listen for messages sent through the *updateStatistics* method.</span></span>

<a id="Ex1Task3"></a>
#### <a name="task-3--running-the-solution"></a><span data-ttu-id="86009-235">タスク3–ソリューションを実行する</span><span class="sxs-lookup"><span data-stu-id="86009-235">Task 3 – Running the Solution</span></span>

<span data-ttu-id="86009-236">このタスクでは、ソリューションを実行して、新しい質問に回答した後、SignalR を使用して統計ビューが自動的に更新されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="86009-236">In this task, you will run the solution to verify that the statistics view is updated automatically using SignalR after answering a new question.</span></span>

1. <span data-ttu-id="86009-237">F5 キーを押して、ソリューションを実行します。</span><span class="sxs-lookup"><span data-stu-id="86009-237">Press **F5** to run the solution.</span></span>

    > [!NOTE]
    > <span data-ttu-id="86009-238">まだアプリケーションにログインしていない場合は、タスク1で作成したユーザーでログインします。</span><span class="sxs-lookup"><span data-stu-id="86009-238">If not already logged in to the application, log in with the user you created in Task 1.</span></span>
2. <span data-ttu-id="86009-239">新しいウィンドウで **[統計]** ページを開き、タスク1で行ったように**ホーム**ページと**統計情報**のページを並べて表示します。</span><span class="sxs-lookup"><span data-stu-id="86009-239">Open the **Statistics** page in a new window and put the **Home** page and **Statistics** page side-by-side as you did in Task 1.</span></span>
3. <span data-ttu-id="86009-240">**ホーム**ページで、いずれかのオプションをクリックして質問に回答します。</span><span class="sxs-lookup"><span data-stu-id="86009-240">In the **Home** page, answer the question by clicking one of the options.</span></span>

    <span data-ttu-id="86009-241">![別の質問への回答](real-time-web-applications-with-signalr/_static/image13.png "別の質問への回答")</span><span class="sxs-lookup"><span data-stu-id="86009-241">![Answering another question](real-time-web-applications-with-signalr/_static/image13.png "Answering another question")</span></span>

    <span data-ttu-id="86009-242">*別の質問への回答*</span><span class="sxs-lookup"><span data-stu-id="86009-242">*Answering another question*</span></span>
4. <span data-ttu-id="86009-243">いずれかのボタンをクリックすると、回答が表示されます。</span><span class="sxs-lookup"><span data-stu-id="86009-243">After clicking one of the buttons, the answer should appear.</span></span> <span data-ttu-id="86009-244">ページ全体を更新する必要なく、更新された情報で質問に回答した後、ページの統計情報が自動的に更新されることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="86009-244">Notice that the Statistics information on the page is updated automatically after answering the question with the updated information without the need to refresh the entire page.</span></span>

    <span data-ttu-id="86009-245">![回答後に更新された統計ページ](real-time-web-applications-with-signalr/_static/image14.png "回答後に更新された統計ページ")</span><span class="sxs-lookup"><span data-stu-id="86009-245">![Statistics page refreshed after answer](real-time-web-applications-with-signalr/_static/image14.png "Statistics page refreshed after answer")</span></span>

    <span data-ttu-id="86009-246">*回答後に更新された統計ページ*</span><span class="sxs-lookup"><span data-stu-id="86009-246">*Statistics page refreshed after answer*</span></span>

<a id="Exercise2"></a>
### <a name="exercise-2-scaling-out-using-sql-server"></a><span data-ttu-id="86009-247">演習 2: SQL Server を使用したスケールアウト</span><span class="sxs-lookup"><span data-stu-id="86009-247">Exercise 2: Scaling Out Using SQL Server</span></span>

<span data-ttu-id="86009-248">Web アプリケーションをスケーリングする場合は、通常、*スケールアップ*と*スケールアウト*のオプションのいずれかを選択できます。</span><span class="sxs-lookup"><span data-stu-id="86009-248">When scaling a web application, you can generally choose between *scaling up* and *scaling out* options.</span></span> <span data-ttu-id="86009-249">スケール*アップ*とは、より大きなサーバーを使用して、より多くのリソース (CPU、RAM など) を使用することです。*スケールアウト*とは、負荷を処理するためにサーバーを追加することを意味します。</span><span class="sxs-lookup"><span data-stu-id="86009-249">*Scale up* means using a larger server, with more resources (CPU, RAM, etc.) while *scale out* means adding more servers to handle the load.</span></span> <span data-ttu-id="86009-250">後者の問題は、クライアントが異なるサーバーにルーティングされる可能性があることです。</span><span class="sxs-lookup"><span data-stu-id="86009-250">The problem with the latter is that the clients can get routed to different servers.</span></span> <span data-ttu-id="86009-251">1つのサーバーに接続されているクライアントは、別のサーバーから送信されたメッセージを受信しません。</span><span class="sxs-lookup"><span data-stu-id="86009-251">A client that is connected to one server will not receive messages sent from another server.</span></span>

<span data-ttu-id="86009-252">*バックプレーン*と呼ばれるコンポーネントを使用して、サーバー間でメッセージを転送することで、これらの問題を解決できます。</span><span class="sxs-lookup"><span data-stu-id="86009-252">You can solve these issues by using a component called *backplane*, to forward messages between servers.</span></span> <span data-ttu-id="86009-253">バックプレーンが有効になっている場合、各アプリケーションインスタンスはバックプレーンにメッセージを送信し、バックプレーンはそれらを他のアプリケーションインスタンスに転送します。</span><span class="sxs-lookup"><span data-stu-id="86009-253">With a backplane enabled, each application instance sends messages to the backplane, and the backplane forwards them to the other application instances.</span></span>

<span data-ttu-id="86009-254">現在、SignalR には3種類の背面があります。</span><span class="sxs-lookup"><span data-stu-id="86009-254">There are currently three types of backplanes for SignalR:</span></span>

- <span data-ttu-id="86009-255">**Windows Azure Service Bus**。</span><span class="sxs-lookup"><span data-stu-id="86009-255">**Windows Azure Service Bus**.</span></span> <span data-ttu-id="86009-256">Service Bus は、コンポーネントが疎結合されたメッセージを送信できるようにするメッセージングインフラストラクチャです。</span><span class="sxs-lookup"><span data-stu-id="86009-256">Service Bus is a messaging infrastructure that allows components to send loosely coupled messages.</span></span>
- <span data-ttu-id="86009-257">**SQL Server**。</span><span class="sxs-lookup"><span data-stu-id="86009-257">**SQL Server**.</span></span> <span data-ttu-id="86009-258">SQL Server バックプレーンは、SQL テーブルにメッセージを書き込みます。</span><span class="sxs-lookup"><span data-stu-id="86009-258">The SQL Server backplane writes messages to SQL tables.</span></span> <span data-ttu-id="86009-259">バックプレーンは、効率的なメッセージングのために Service Broker を使用します。</span><span class="sxs-lookup"><span data-stu-id="86009-259">The backplane uses Service Broker for efficient messaging.</span></span> <span data-ttu-id="86009-260">ただし、Service Broker が有効になっていない場合にも機能します。</span><span class="sxs-lookup"><span data-stu-id="86009-260">However, it also works if Service Broker is not enabled.</span></span>
- <span data-ttu-id="86009-261">**Redis**。</span><span class="sxs-lookup"><span data-stu-id="86009-261">**Redis**.</span></span> <span data-ttu-id="86009-262">Redis は、メモリ内のキーと値のストアです。</span><span class="sxs-lookup"><span data-stu-id="86009-262">Redis is an in-memory key-value store.</span></span> <span data-ttu-id="86009-263">Redis は、メッセージを送信するためのパブリッシュ/サブスクライブ ("pub/sub") パターンをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="86009-263">Redis supports a publish/subscribe ("pub/sub") pattern for sending messages.</span></span>

<span data-ttu-id="86009-264">すべてのメッセージは、メッセージバスを介して送信されます。</span><span class="sxs-lookup"><span data-stu-id="86009-264">Every message is sent through a message bus.</span></span> <span data-ttu-id="86009-265">メッセージバスは、パブリッシュ/サブスクライブの抽象化を提供する[IMessageBus](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.imessagebus(v=vs.100).aspx)インターフェイスを実装します。</span><span class="sxs-lookup"><span data-stu-id="86009-265">A message bus implements the [IMessageBus](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.imessagebus(v=vs.100).aspx) interface, which provides a publish/subscribe abstraction.</span></span> <span data-ttu-id="86009-266">背面は、既定の**IMessageBus**をそのバックプレーン用に設計されたバスに置き換えることによって機能します。</span><span class="sxs-lookup"><span data-stu-id="86009-266">The backplanes work by replacing the default **IMessageBus** with a bus designed for that backplane.</span></span>

<span data-ttu-id="86009-267">各サーバーインスタンスは、バスを介してバックプレーンに接続します。</span><span class="sxs-lookup"><span data-stu-id="86009-267">Each server instance connects to the backplane through the bus.</span></span> <span data-ttu-id="86009-268">メッセージが送信されると、バックプレーンに送られ、バックプレーンがすべてのサーバーに送信します。</span><span class="sxs-lookup"><span data-stu-id="86009-268">When a message is sent, it goes to the backplane, and the backplane sends it to every server.</span></span> <span data-ttu-id="86009-269">サーバーは、バックプレーンからメッセージを受信すると、メッセージをローカルキャッシュに格納します。</span><span class="sxs-lookup"><span data-stu-id="86009-269">When a server receives a message from the backplane, it stores the message in its local cache.</span></span> <span data-ttu-id="86009-270">サーバーは、ローカルキャッシュからクライアントにメッセージを配信します。</span><span class="sxs-lookup"><span data-stu-id="86009-270">The server then delivers messages to clients from its local cache.</span></span>

<span data-ttu-id="86009-271">SignalR バックプレーンの動作の詳細については、こちらの[記事](../performance/scaleout-in-signalr.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="86009-271">For more information about how the SignalR backplane works, read this [article](../performance/scaleout-in-signalr.md).</span></span>

> [!NOTE]
> <span data-ttu-id="86009-272">バックプレーンがボトルネックになる可能性があるシナリオがいくつかあります。</span><span class="sxs-lookup"><span data-stu-id="86009-272">There are some scenarios where a backplane can become a bottleneck.</span></span> <span data-ttu-id="86009-273">一般的な SignalR シナリオをいくつか次に示します。</span><span class="sxs-lookup"><span data-stu-id="86009-273">Here are some typical SignalR scenarios:</span></span>
> 
> - <span data-ttu-id="86009-274">[サーバーブロードキャスト](tutorial-server-broadcast-with-signalr.md)(stock ティッカーなど): 背面は、このシナリオに適しています。これは、サーバーがメッセージの送信速度を制御するためです。</span><span class="sxs-lookup"><span data-stu-id="86009-274">[Server broadcast](tutorial-server-broadcast-with-signalr.md) (e.g., stock ticker): Backplanes work well for this scenario, because the server controls the rate at which messages are sent.</span></span>
> - <span data-ttu-id="86009-275">[クライアント対クライアント](tutorial-getting-started-with-signalr.md)(チャットなど): このシナリオでは、メッセージの数がクライアントの数に合わせてスケーリングされる場合、バックプレーンはボトルネックになる可能性があります。これは、より多くのクライアントが参加したときにメッセージの割合が増加した場合に発生します。</span><span class="sxs-lookup"><span data-stu-id="86009-275">[Client-to-client](tutorial-getting-started-with-signalr.md) (e.g., chat): In this scenario, the backplane might be a bottleneck if the number of messages scales with the number of clients; that is, if the rate of messages grows proportionally as more clients join.</span></span>
> - <span data-ttu-id="86009-276">[高頻度リアル](tutorial-high-frequency-realtime-with-signalr.md)タイム (リアルタイムゲームなど): このシナリオでは、バックプレーンはお勧めできません。</span><span class="sxs-lookup"><span data-stu-id="86009-276">[High-frequency realtime](tutorial-high-frequency-realtime-with-signalr.md) (e.g., real-time games): A backplane is not recommended for this scenario.</span></span>

<span data-ttu-id="86009-277">この演習では、 **SQL Server**を使用して、**マニアクイズ**アプリケーション間でメッセージを配布します。</span><span class="sxs-lookup"><span data-stu-id="86009-277">In this exercise, you will use **SQL Server** to distribute messages across the **Geek Quiz** application.</span></span> <span data-ttu-id="86009-278">これらのタスクを1つのテストコンピューターで実行して、構成を設定する方法を学習しますが、完全な効果を得るためには、SignalR アプリケーションを複数のサーバーに配置する必要があります。</span><span class="sxs-lookup"><span data-stu-id="86009-278">You will run these tasks on a single test machine to learn how to set up the configuration, but in order to get the full effect, you will need to deploy the SignalR application to two or more servers.</span></span> <span data-ttu-id="86009-279">また、いずれかのサーバーまたは別の専用サーバーに SQL Server をインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="86009-279">You must also install SQL Server on one of the servers, or on a separate dedicated server.</span></span>

![SQL Server ダイアグラムを使用した Scale Out](real-time-web-applications-with-signalr/_static/image15.png)

<a id="Ex2Task1"></a>
#### <a name="task-1---understanding-the-scenario"></a><span data-ttu-id="86009-281">タスク 1-シナリオについて</span><span class="sxs-lookup"><span data-stu-id="86009-281">Task 1 - Understanding the Scenario</span></span>

<span data-ttu-id="86009-282">このタスクでは、ローカルコンピューターで複数の IIS インスタンスをシミュレートする**マニアクイズ**の2つのインスタンスを実行します。</span><span class="sxs-lookup"><span data-stu-id="86009-282">In this task, you will run 2 instances of **Geek Quiz** simulating multiple IIS instances on your local machine.</span></span> <span data-ttu-id="86009-283">このシナリオでは、1つのアプリケーションでトリビアの質問に回答するときに、2番目のインスタンスの統計ページで更新プログラムに通知されません。</span><span class="sxs-lookup"><span data-stu-id="86009-283">In this scenario, when answering trivia questions on one application, update won't be notified on the statistics page of the second instance.</span></span> <span data-ttu-id="86009-284">このシミュレーションは、アプリケーションが複数のインスタンスに配置され、ロードバランサーを使用してアプリケーションと通信する環境に似ています。</span><span class="sxs-lookup"><span data-stu-id="86009-284">This simulation resembles an environment where your application is deployed on multiple instances and using a load balancer to communicate with them.</span></span>

1. <span data-ttu-id="86009-285">**Source/Ex2-スケール Ingoutwithsqlserver/begin**フォルダーにある**begin. .sln**ソリューションを開きます。</span><span class="sxs-lookup"><span data-stu-id="86009-285">Open the **Begin.sln** solution located in the **Source/Ex2-ScalingOutWithSQLServer/Begin** folder.</span></span> <span data-ttu-id="86009-286">読み込みが完了すると、**サーバーエクスプローラー**が表示されます。このソリューションには、構造が同じで名前が異なる2つのプロジェクトがあることがわかります。</span><span class="sxs-lookup"><span data-stu-id="86009-286">Once loaded, you will notice on the **Server Explorer** that the solution has two projects with identical structures but different names.</span></span> <span data-ttu-id="86009-287">これにより、ローカルコンピューター上で同じアプリケーションの2つのインスタンスの実行がシミュレートされます。</span><span class="sxs-lookup"><span data-stu-id="86009-287">This will simulate running two instances of the same application on your local machine.</span></span>

    <span data-ttu-id="86009-288">![マニアクイズの2つのインスタンスをシミュレートするソリューションを開始する](real-time-web-applications-with-signalr/_static/image16.png "マニアクイズの2つのインスタンスをシミュレートするソリューションを開始する")</span><span class="sxs-lookup"><span data-stu-id="86009-288">![Begin Solution Simulating 2 Instances of Geek Quiz](real-time-web-applications-with-signalr/_static/image16.png "Begin Solution Simulating 2 Instances of Geek Quiz")</span></span>

    <span data-ttu-id="86009-289">*マニアクイズの2つのインスタンスをシミュレートするソリューションを開始する*</span><span class="sxs-lookup"><span data-stu-id="86009-289">*Begin Solution Simulating 2 Instances of Geek Quiz*</span></span>
2. <span data-ttu-id="86009-290">ソリューションの プロパティ ページを開くには、ソリューションノードを右クリックし、**プロパティ** を選択します。</span><span class="sxs-lookup"><span data-stu-id="86009-290">Open the properties page of the solution by right-clicking the solution node and selecting **Properties**.</span></span> <span data-ttu-id="86009-291">**[スタートアッププロジェクト]** で、 **[マルチスタートアッププロジェクト]** を選択し、両方のプロジェクトの**アクション**値を [*開始*] に変更します。</span><span class="sxs-lookup"><span data-stu-id="86009-291">Under **Startup Project**, select **Multiple startup projects** and change the **Action** value for both projects to *Start*.</span></span>

    <span data-ttu-id="86009-292">![複数のプロジェクトの開始](real-time-web-applications-with-signalr/_static/image17.png "複数のプロジェクトの開始")</span><span class="sxs-lookup"><span data-stu-id="86009-292">![Starting Multiple Projects](real-time-web-applications-with-signalr/_static/image17.png "Starting Multiple Projects")</span></span>

    <span data-ttu-id="86009-293">*複数のプロジェクトの開始*</span><span class="sxs-lookup"><span data-stu-id="86009-293">*Starting Multiple Projects*</span></span>
3. <span data-ttu-id="86009-294">F5 キーを押して、ソリューションを実行します。</span><span class="sxs-lookup"><span data-stu-id="86009-294">Press **F5** to run the solution.</span></span> <span data-ttu-id="86009-295">このアプリケーションでは、異なるポートで**マニアクイズ**の2つのインスタンスを起動し、同じアプリケーションの複数のインスタンスをシミュレートします。</span><span class="sxs-lookup"><span data-stu-id="86009-295">The application will launch two instances of **Geek Quiz** in different ports, simulating multiple instances of the same application.</span></span> <span data-ttu-id="86009-296">左側のブラウザーのいずれかを画面の右側にピン留めします。</span><span class="sxs-lookup"><span data-stu-id="86009-296">Pin one of the browsers on left and the other on the right of your screen.</span></span> <span data-ttu-id="86009-297">資格情報を使用してログインするか、新しいユーザーを登録します。</span><span class="sxs-lookup"><span data-stu-id="86009-297">Log in with your credentials or register a new user.</span></span> <span data-ttu-id="86009-298">ログインしたら、左側にある トリビア ページを保持し、右側のブラウザーの **統計情報** ページに移動します。</span><span class="sxs-lookup"><span data-stu-id="86009-298">Once logged in, keep the Trivia page on the left and go to the **Statistics** page in the browser on the right.</span></span>

    ![マニアクイズをサイドバイサイドで](real-time-web-applications-with-signalr/_static/image18.png)

    <span data-ttu-id="86009-300">*マニアクイズをサイドバイサイドで*</span><span class="sxs-lookup"><span data-stu-id="86009-300">*Geek Quiz Side by Side*</span></span>

    ![さまざまなポートでのマニアクイズ](real-time-web-applications-with-signalr/_static/image19.png)

    <span data-ttu-id="86009-302">*さまざまなポートでのマニアクイズ*</span><span class="sxs-lookup"><span data-stu-id="86009-302">*Geek Quiz in Different Ports*</span></span>
4. <span data-ttu-id="86009-303">左側のブラウザーで質問への回答を開始すると、右側のブラウザーの **[統計]** ページが更新されていないことがわかります。</span><span class="sxs-lookup"><span data-stu-id="86009-303">Start answering questions in the left browser and you will notice that the **Statistics** page in the right browser is not being updated.</span></span> <span data-ttu-id="86009-304">これは、 **SignalR**がローカルキャッシュを使用してクライアント間でメッセージを分散するためです。このシナリオでは複数のインスタンスがシミュレートされるため、キャッシュはそれらの間で共有されません。</span><span class="sxs-lookup"><span data-stu-id="86009-304">This is because **SignalR** uses a local cache to distribute messages across their clients and this scenario is simulating multiple instances, therefore the cache is not shared between them.</span></span> <span data-ttu-id="86009-305">**SignalR**が機能していることを確認するには、同じ手順を1つのアプリを使用してテストします。</span><span class="sxs-lookup"><span data-stu-id="86009-305">You can verify that **SignalR** is working by testing the same steps but using a single app.</span></span> <span data-ttu-id="86009-306">次のタスクでは、インスタンス間でメッセージをレプリケートするようにバックプレーンを構成します。</span><span class="sxs-lookup"><span data-stu-id="86009-306">In the following tasks you will configure a backplane to replicate the messages across instances.</span></span>
5. <span data-ttu-id="86009-307">Visual Studio に戻り、デバッグを停止します。</span><span class="sxs-lookup"><span data-stu-id="86009-307">Go back to Visual Studio and stop debugging.</span></span>

<a id="Ex2Task2"></a>
#### <a name="task-2--creating-the-sql-server-backplane"></a><span data-ttu-id="86009-308">タスク2– SQL Server バックプレーンの作成</span><span class="sxs-lookup"><span data-stu-id="86009-308">Task 2 – Creating the SQL Server Backplane</span></span>

<span data-ttu-id="86009-309">このタスクでは、**マニアクイズ**アプリケーションのバックプレーンとして機能するデータベースを作成します。</span><span class="sxs-lookup"><span data-stu-id="86009-309">In this task, you will create a database that will serve as a backplane for the **Geek Quiz** application.</span></span> <span data-ttu-id="86009-310">**SQL Server オブジェクトエクスプローラー**を使用してサーバーを参照し、データベースを初期化します。</span><span class="sxs-lookup"><span data-stu-id="86009-310">You will use **SQL Server Object Explorer** to browse your server and initialize the database.</span></span> <span data-ttu-id="86009-311">さらに、 **Service Broker**を有効にします。</span><span class="sxs-lookup"><span data-stu-id="86009-311">Additionally, you will enable the **Service Broker**.</span></span>

1. <span data-ttu-id="86009-312">**Visual Studio**で、メニュー**ビュー**を開き、 **[SQL Server オブジェクトエクスプローラー]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="86009-312">In **Visual Studio**, open menu **View** and select **SQL Server Object Explorer**.</span></span>
2. <span data-ttu-id="86009-313">LocalDB インスタンスに接続するには、 **[SQL Server]** ノードを右クリックし、 **[SQL Server の追加]** オプションを選択します。</span><span class="sxs-lookup"><span data-stu-id="86009-313">Connect to your LocalDB instance by right-clicking the **SQL Server** node and selecting **Add SQL Server...** option.</span></span>

    <span data-ttu-id="86009-314">![SQL Server インスタンスの追加](real-time-web-applications-with-signalr/_static/image20.png "SQL Server インスタンスの追加")</span><span class="sxs-lookup"><span data-stu-id="86009-314">![Adding a SQL Server Instance](real-time-web-applications-with-signalr/_static/image20.png "Adding a SQL Server Instance")</span></span>

    <span data-ttu-id="86009-315">*SQL Server オブジェクトエクスプローラーへの SQL Server インスタンスの追加*</span><span class="sxs-lookup"><span data-stu-id="86009-315">*Adding a SQL Server instance to SQL Server Object Explorer*</span></span>
3. <span data-ttu-id="86009-316">**サーバー名**を *(localdb) \ v11.0*に設定し、認証モードとして**Windows 認証**をそのまま使用します。</span><span class="sxs-lookup"><span data-stu-id="86009-316">Set the **server name** to *(localdb)\v11.0* and leave **Windows Authentication** as your authentication mode.</span></span> <span data-ttu-id="86009-317">**[接続]** をクリックして続行します。</span><span class="sxs-lookup"><span data-stu-id="86009-317">Click **Connect** to continue.</span></span>

    <span data-ttu-id="86009-318">![LocalDB に接続しています](real-time-web-applications-with-signalr/_static/image21.png "LocalDB に接続しています")</span><span class="sxs-lookup"><span data-stu-id="86009-318">![Connecting to LocalDB](real-time-web-applications-with-signalr/_static/image21.png "Connecting to LocalDB")</span></span>

    <span data-ttu-id="86009-319">*LocalDB に接続しています*</span><span class="sxs-lookup"><span data-stu-id="86009-319">*Connecting to LocalDB*</span></span>
4. <span data-ttu-id="86009-320">LocalDB インスタンスに接続したので、SignalR のバックプレーン SQL Server を表すデータベースを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="86009-320">Now that you are connected to your LocalDB instance, you will need to create a database that will represent the SQL Server backplane for SignalR.</span></span> <span data-ttu-id="86009-321">これを行うには、 **[データベース]** ノードを右クリックし、 **[新しいデータベースの追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="86009-321">To do this, right-click the **Databases** node and select **Add New Database**.</span></span>

    <span data-ttu-id="86009-322">![新しいデータベースの追加](real-time-web-applications-with-signalr/_static/image22.png "新しいデータベースの追加")</span><span class="sxs-lookup"><span data-stu-id="86009-322">![Adding a new database](real-time-web-applications-with-signalr/_static/image22.png "Adding a new database")</span></span>

    <span data-ttu-id="86009-323">*新しいデータベースの追加*</span><span class="sxs-lookup"><span data-stu-id="86009-323">*Adding a new database*</span></span>
5. <span data-ttu-id="86009-324">データベース名を*SignalR*に設定し、 **[OK]** をクリックして作成します。</span><span class="sxs-lookup"><span data-stu-id="86009-324">Set the database name to *SignalR* and click **OK** to create it.</span></span>

    <span data-ttu-id="86009-325">![SignalR データベースの作成](real-time-web-applications-with-signalr/_static/image23.png "SignalR データベースの作成")</span><span class="sxs-lookup"><span data-stu-id="86009-325">![Creating the SignalR database](real-time-web-applications-with-signalr/_static/image23.png "Creating the SignalR database")</span></span>

    <span data-ttu-id="86009-326">*SignalR データベースの作成*</span><span class="sxs-lookup"><span data-stu-id="86009-326">*Creating the SignalR database*</span></span>

    > [!NOTE]
    > <span data-ttu-id="86009-327">データベースの任意の名前を選択できます。</span><span class="sxs-lookup"><span data-stu-id="86009-327">You can choose any name for the database.</span></span>
6. <span data-ttu-id="86009-328">バックプレーンから更新をより効率的に受け取るには、データベースに対して Service Broker を有効にすることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="86009-328">To receive updates more efficiently from the backplane, it is recommended to enable Service Broker for the database.</span></span> <span data-ttu-id="86009-329">Service Broker は、SQL Server でのメッセージングとキューのネイティブサポートを提供します。</span><span class="sxs-lookup"><span data-stu-id="86009-329">Service Broker provides native support for messaging and queuing in SQL Server.</span></span> <span data-ttu-id="86009-330">バックプレーンは、Service Broker なしでも動作します。</span><span class="sxs-lookup"><span data-stu-id="86009-330">The backplane also works without Service Broker.</span></span> <span data-ttu-id="86009-331">データベースを右クリックし、 **[新しいクエリ]** をクリックして、新しいクエリを開きます。</span><span class="sxs-lookup"><span data-stu-id="86009-331">Open a new query by right-clicking the database and select **New Query**.</span></span>

    <span data-ttu-id="86009-332">![新しいクエリを開く](real-time-web-applications-with-signalr/_static/image24.png "新しいクエリを開く")</span><span class="sxs-lookup"><span data-stu-id="86009-332">![Opening a New Query](real-time-web-applications-with-signalr/_static/image24.png "Opening a New Query")</span></span>

    <span data-ttu-id="86009-333">*新しいクエリを開く*</span><span class="sxs-lookup"><span data-stu-id="86009-333">*Opening a New Query*</span></span>
7. <span data-ttu-id="86009-334">Service Broker が有効になっているかどうかを確認するには、**データベース**カタログビューの **\_Broker\_enabled**列に対してクエリを実行します。</span><span class="sxs-lookup"><span data-stu-id="86009-334">To check whether Service Broker is enabled, query the **is\_broker\_enabled** column in the **sys.databases** catalog view.</span></span> <span data-ttu-id="86009-335">最近開いたクエリウィンドウで、次のスクリプトを実行します。</span><span class="sxs-lookup"><span data-stu-id="86009-335">Execute the following script in the recently opened query window.</span></span>

    [!code-sql[Main](real-time-web-applications-with-signalr/samples/sample11.sql)]

    <span data-ttu-id="86009-336">![Service Broker の状態のクエリ](real-time-web-applications-with-signalr/_static/image25.png "Service Broker の状態のクエリ")</span><span class="sxs-lookup"><span data-stu-id="86009-336">![Querying the Service Broker Status](real-time-web-applications-with-signalr/_static/image25.png "Querying the Service Broker Status")</span></span>

    <span data-ttu-id="86009-337">*Service Broker の状態のクエリ*</span><span class="sxs-lookup"><span data-stu-id="86009-337">*Querying the Service Broker Status*</span></span>
8. <span data-ttu-id="86009-338">の値**が\_broker\_有効になっ**ているデータベースの列が 0&quot;&quot;場合は、次のコマンドを使用して有効にします。</span><span class="sxs-lookup"><span data-stu-id="86009-338">If the value of the **is\_broker\_enabled** column in your database is &quot;0&quot;, use the following command to enable it.</span></span> <span data-ttu-id="86009-339">**&lt;データベース&gt;** を、データベースの作成時に設定した名前に置き換えます (例: SignalR)。</span><span class="sxs-lookup"><span data-stu-id="86009-339">Replace **&lt;YOUR-DATABASE&gt;** with the name you set when creating the database (e.g.: SignalR).</span></span>

    [!code-sql[Main](real-time-web-applications-with-signalr/samples/sample12.sql)]

    <span data-ttu-id="86009-340">![Service Broker の有効化](real-time-web-applications-with-signalr/_static/image26.png "Service Broker の有効化")</span><span class="sxs-lookup"><span data-stu-id="86009-340">![Enabling Service Broker](real-time-web-applications-with-signalr/_static/image26.png "Enabling Service Broker")</span></span>

    <span data-ttu-id="86009-341">*Service Broker の有効化*</span><span class="sxs-lookup"><span data-stu-id="86009-341">*Enabling Service Broker*</span></span>

    > [!NOTE]
    > <span data-ttu-id="86009-342">このクエリでデッドロックが発生した場合は、データベースに接続されているアプリケーションがないことを確認してください。</span><span class="sxs-lookup"><span data-stu-id="86009-342">If this query appears to deadlock, make sure there are no applications connected to the DB.</span></span>

<a id="Ex2Task3"></a>
#### <a name="task-3--configuring-the-signalr-application"></a><span data-ttu-id="86009-343">タスク3– SignalR アプリケーションを構成する</span><span class="sxs-lookup"><span data-stu-id="86009-343">Task 3 – Configuring the SignalR Application</span></span>

<span data-ttu-id="86009-344">このタスクでは、SQL Server バックプレーンに接続するように**マニアクイズ**を構成します。</span><span class="sxs-lookup"><span data-stu-id="86009-344">In this task, you will configure **Geek Quiz** to connect to the SQL Server backplane.</span></span> <span data-ttu-id="86009-345">最初に**SignalR** NuGet パッケージを追加し、接続文字列をバックプレーンデータベースに設定します。</span><span class="sxs-lookup"><span data-stu-id="86009-345">You will first add the **SignalR.SqlServer** NuGet package and set the connection string to your backplane database.</span></span>

1. <span data-ttu-id="86009-346">[**ツール** > **NuGet パッケージマネージャー**] から**パッケージマネージャーコンソール**を開きます。</span><span class="sxs-lookup"><span data-stu-id="86009-346">Open the **Package Manager Console** from **Tools** > **NuGet Package Manager**.</span></span> <span data-ttu-id="86009-347">**[既定のプロジェクト]** ドロップダウンリストで **[GeekQuiz]** プロジェクト が選択されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="86009-347">Make sure that **GeekQuiz** project is selected in the **Default project** drop-down list.</span></span> <span data-ttu-id="86009-348">次のコマンドを入力して、 **SignalR** NuGet パッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="86009-348">Type the following command to install the **Microsoft.AspNet.SignalR.SqlServer** NuGet package.</span></span>

    [!code-powershell[Main](real-time-web-applications-with-signalr/samples/sample13.ps1)]
2. <span data-ttu-id="86009-349">前の手順を繰り返しますが、今度は project **GeekQuiz2**を実行します。</span><span class="sxs-lookup"><span data-stu-id="86009-349">Repeat the previous step but this time for project **GeekQuiz2**.</span></span>
3. <span data-ttu-id="86009-350">SQL Server バックプレーンを構成するには、 **GeekQuiz**プロジェクトの**Startup.cs**ファイルを開き、次のコードを**configure**メソッドに追加します。</span><span class="sxs-lookup"><span data-stu-id="86009-350">To configure the SQL Server backplane, open the **Startup.cs** file of the **GeekQuiz** project and add the following code to the **Configure** method.</span></span> <span data-ttu-id="86009-351">**&lt;データベース&gt;** を、SQL Server バックプレーンの作成時に使用したデータベース名に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="86009-351">Replace **&lt;YOUR-DATABASE&gt;** with your database name you used when creating the SQL Server backplane.</span></span> <span data-ttu-id="86009-352">**GeekQuiz2**プロジェクトに対してこの手順を繰り返します。</span><span class="sxs-lookup"><span data-stu-id="86009-352">Repeat this step for the **GeekQuiz2** project.</span></span>

    <span data-ttu-id="86009-353">(コードスニペット- *Realtimesignalr-Ex2-StartupConfiguration*)</span><span class="sxs-lookup"><span data-stu-id="86009-353">(Code Snippet - *RealTimeSignalR - Ex2 - StartupConfiguration*)</span></span>

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample14.cs)]
4. <span data-ttu-id="86009-354">両方のプロジェクトが SQL Server バックプレーンを使用するように構成されたので、 **F5**キーを押してそれらを同時に実行します。</span><span class="sxs-lookup"><span data-stu-id="86009-354">Now that both projects are configured to use the SQL Server backplane, press **F5** to run them simultaneously.</span></span>
5. <span data-ttu-id="86009-355">ここでも、 **Visual Studio**は異なるポートで**マニアクイズ**の2つのインスタンスを起動します。</span><span class="sxs-lookup"><span data-stu-id="86009-355">Again, **Visual Studio** will launch two instances of **Geek Quiz** in different ports.</span></span> <span data-ttu-id="86009-356">画面の右側にあるいずれかのブラウザーをピン留めし、資格情報でログインします。</span><span class="sxs-lookup"><span data-stu-id="86009-356">Pin one of the browsers on the left and the other on the right of your screen and log in with your credentials.</span></span> <span data-ttu-id="86009-357">左側の [トリビア] ページをそのままにして、適切なブラウザーの**Statistics**ページインに移動します。</span><span class="sxs-lookup"><span data-stu-id="86009-357">Keep the Trivia page on the left and go to **Statistics** pagein the right browser.</span></span>
6. <span data-ttu-id="86009-358">左側のブラウザーで質問への回答を開始します。</span><span class="sxs-lookup"><span data-stu-id="86009-358">Start answering questions in the left browser.</span></span> <span data-ttu-id="86009-359">今回は、バックプレーンによって**統計**ページが更新されます。</span><span class="sxs-lookup"><span data-stu-id="86009-359">This time, the **Statistics** page is updated thanks to the backplane.</span></span> <span data-ttu-id="86009-360">アプリケーションを切り替えます (**統計**は左側にあり、**トリビア**が右側にあります)。テストを繰り返して、両方のインスタンスで動作していることを検証します。</span><span class="sxs-lookup"><span data-stu-id="86009-360">Switch between applications (**Statistics** is now on the left, and **Trivia** is on the right) and repeat the test to validate that it is working for both instances.</span></span> <span data-ttu-id="86009-361">バックプレーンは、接続されている各サーバーのメッセージの*共有キャッシュ*として機能し、各サーバーは、接続されたクライアントに配布するために独自のローカルキャッシュにメッセージを格納します。</span><span class="sxs-lookup"><span data-stu-id="86009-361">The backplane serves as a *shared cache* of messages for each connected server, and each server will store the messages in their own local cache to distribute to connected clients.</span></span>
7. <span data-ttu-id="86009-362">Visual Studio に戻り、デバッグを停止します。</span><span class="sxs-lookup"><span data-stu-id="86009-362">Go back to Visual Studio and stop debugging.</span></span>
8. <span data-ttu-id="86009-363">SQL Server バックプレーンコンポーネントは、指定されたデータベースに必要なテーブルを自動的に生成します。</span><span class="sxs-lookup"><span data-stu-id="86009-363">The SQL Server backplane component automatically generates the necessary tables on the specified database.</span></span> <span data-ttu-id="86009-364">**SQL Server オブジェクトエクスプローラー**パネルで、バックプレーン用に作成したデータベース (例: SignalR) を開き、そのテーブルを展開します。</span><span class="sxs-lookup"><span data-stu-id="86009-364">In the **SQL Server Object Explorer** panel, open the database you created for the backplane (e.g.: SignalR) and expand its tables.</span></span> <span data-ttu-id="86009-365">次のテーブルが表示されます。</span><span class="sxs-lookup"><span data-stu-id="86009-365">You should see the following tables:</span></span>

    ![バックプレーンが生成したテーブル](real-time-web-applications-with-signalr/_static/image27.png)

    <span data-ttu-id="86009-367">*バックプレーンが生成したテーブル*</span><span class="sxs-lookup"><span data-stu-id="86009-367">*Backplane Generated Tables*</span></span>
9. <span data-ttu-id="86009-368">**SignalR\_0**テーブルを右クリックし、[データの**表示**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="86009-368">Right-click the **SignalR.Messages\_0** table and select **View Data**.</span></span>

    ![SignalR バックプレーンメッセージテーブルの表示](real-time-web-applications-with-signalr/_static/image28.png)

    <span data-ttu-id="86009-370">*SignalR バックプレーンメッセージテーブルの表示*</span><span class="sxs-lookup"><span data-stu-id="86009-370">*View SignalR Backplane Messages Table*</span></span>
10. <span data-ttu-id="86009-371">トリビアの質問に答えると、**ハブ**に送信されたさまざまなメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="86009-371">You can see the different messages sent to the **Hub** when answering the trivia questions.</span></span> <span data-ttu-id="86009-372">バックプレーンは、これらのメッセージを接続されている任意のインスタンスに配布します。</span><span class="sxs-lookup"><span data-stu-id="86009-372">The backplane distributes these messages to any connected instance.</span></span>

    ![バックプレーンメッセージテーブル](real-time-web-applications-with-signalr/_static/image29.png)

    <span data-ttu-id="86009-374">*バックプレーンメッセージテーブル*</span><span class="sxs-lookup"><span data-stu-id="86009-374">*Backplane Messages Table*</span></span>

---

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="86009-375">まとめ</span><span class="sxs-lookup"><span data-stu-id="86009-375">Summary</span></span>

<span data-ttu-id="86009-376">このハンズオンラボでは、 **SignalR**をアプリケーションに追加し、**ハブ**を使用して接続されているクライアントにサーバーから通知を送信する方法を学習しました。</span><span class="sxs-lookup"><span data-stu-id="86009-376">In this hands-on lab, you have learned how to add **SignalR** to your application and send notifications from the server to your connected clients using **Hubs**.</span></span> <span data-ttu-id="86009-377">また、アプリケーションが複数の IIS インスタンスに配置されている場合に、*バックプレーン*コンポーネントを使用してアプリケーションをスケールアウトする方法についても学習しました。</span><span class="sxs-lookup"><span data-stu-id="86009-377">Additionally, you learned how to scale out your application by using a *backplane* component when your application is deployed in multiple IIS instances.</span></span>
