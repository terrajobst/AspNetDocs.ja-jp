---
uid: signalr/overview/older-versions/tutorial-getting-started-with-signalr
title: 'チュートリアル: SignalR 1.x を使用したはじめに |Microsoft Docs'
author: bradygaster
description: ASP.NET SignalR を使用して、HTML ページでリアルタイムチャットアプリケーションを作成します。
ms.author: bradyg
ms.date: 02/18/2013
ms.assetid: fdc3599a-5217-44c1-951f-0eec9812dce7
msc.legacyurl: /signalr/overview/older-versions/tutorial-getting-started-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: 87a90b47ae30bee43e0b0c1e078597db54b8e67d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78505750"
---
# <a name="tutorial-getting-started-with-signalr-1x"></a><span data-ttu-id="72b91-103">チュートリアル: SignalR 1.x でのはじめに</span><span class="sxs-lookup"><span data-stu-id="72b91-103">Tutorial: Getting Started with SignalR 1.x</span></span>

<span data-ttu-id="72b91-104">([パトリック Fletcher](https://github.com/pfletcher)、 [Tim teebken](https://github.com/timlt) )</span><span class="sxs-lookup"><span data-stu-id="72b91-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tim Teebken](https://github.com/timlt)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="72b91-105">このチュートリアルでは、SignalR を使用してリアルタイムのチャット アプリケーションを作成する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="72b91-105">This tutorial shows how to use SignalR to create a real-time chat application.</span></span> <span data-ttu-id="72b91-106">SignalR を空の ASP.NET web アプリケーションに追加し、メッセージを送信および表示する HTML ページを作成します。</span><span class="sxs-lookup"><span data-stu-id="72b91-106">You will add SignalR to an empty ASP.NET web application and create an HTML page to send and display messages.</span></span>

## <a name="overview"></a><span data-ttu-id="72b91-107">概要</span><span class="sxs-lookup"><span data-stu-id="72b91-107">Overview</span></span>

<span data-ttu-id="72b91-108">このチュートリアルでは、簡単なブラウザーベースのチャットアプリケーションを構築する方法を紹介することによって、SignalR の開発について説明します。</span><span class="sxs-lookup"><span data-stu-id="72b91-108">This tutorial introduces SignalR development by showing how to build a simple browser-based chat application.</span></span> <span data-ttu-id="72b91-109">SignalR ライブラリを空の ASP.NET web アプリケーションに追加し、クライアントにメッセージを送信するためのハブクラスを作成して、ユーザーがチャットメッセージを送受信できるようにする HTML ページを作成します。</span><span class="sxs-lookup"><span data-stu-id="72b91-109">You will add the SignalR library to an empty ASP.NET web application, create a hub class for sending messages to clients, and create an HTML page that lets users send and receive chat messages.</span></span> <span data-ttu-id="72b91-110">Mvc ビューを使用して MVC 4 でチャットアプリケーションを作成する方法について説明した同様のチュートリアルについては、「[はじめに With SignalR AND MVC 4](index.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="72b91-110">For a similar tutorial that shows how to create a chat application in MVC 4 using an MVC view, see [Getting Started with SignalR and MVC 4](index.md).</span></span>

> [!NOTE]
> <span data-ttu-id="72b91-111">このチュートリアルでは、SignalR のリリース (1.x) バージョンを使用します。</span><span class="sxs-lookup"><span data-stu-id="72b91-111">This tutorial uses the release (1.x) version of SignalR.</span></span> <span data-ttu-id="72b91-112">SignalR 1.x と2.0 の間の変更の詳細については、「 [SignalR 1.X プロジェクトのアップグレード](../releases/upgrading-signalr-1x-projects-to-20.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="72b91-112">For details on changes between SignalR 1.x and 2.0, see [Upgrading SignalR 1.x Projects](../releases/upgrading-signalr-1x-projects-to-20.md).</span></span>

<span data-ttu-id="72b91-113">SignalR は、web アプリケーションを構築するためのオープンソースの .NET ライブラリであり、ライブユーザー操作やリアルタイムのデータ更新を必要とします。</span><span class="sxs-lookup"><span data-stu-id="72b91-113">SignalR is an open-source .NET library for building web applications that require live user interaction or real-time data updates.</span></span> <span data-ttu-id="72b91-114">例としては、ソーシャルアプリケーション、マルチユーザーゲーム、ビジネスコラボレーション、ニュース、気象、金融更新アプリケーションなどがあります。</span><span class="sxs-lookup"><span data-stu-id="72b91-114">Examples include social applications, multiuser games, business collaboration, and news, weather, or financial update applications.</span></span> <span data-ttu-id="72b91-115">これらは、多くの場合、リアルタイムアプリケーションと呼ばれます。</span><span class="sxs-lookup"><span data-stu-id="72b91-115">These are often called real-time applications.</span></span>

<span data-ttu-id="72b91-116">SignalR は、リアルタイムアプリケーションの構築プロセスを簡略化します。</span><span class="sxs-lookup"><span data-stu-id="72b91-116">SignalR simplifies the process of building real-time applications.</span></span> <span data-ttu-id="72b91-117">これには、クライアントとサーバー間の接続の管理とクライアントへのコンテンツの更新のプッシュを容易にするための、ASP.NET サーバーライブラリと JavaScript クライアントライブラリが含まれています。</span><span class="sxs-lookup"><span data-stu-id="72b91-117">It includes an ASP.NET server library and a JavaScript client library to make it easier to manage client-server connections and push content updates to clients.</span></span> <span data-ttu-id="72b91-118">SignalR ライブラリを既存の ASP.NET アプリケーションに追加して、リアルタイムの機能を取得できます。</span><span class="sxs-lookup"><span data-stu-id="72b91-118">You can add the SignalR library to an existing ASP.NET application to gain real-time functionality.</span></span>

<span data-ttu-id="72b91-119">このチュートリアルでは、次の SignalR の開発タスクについて説明します。</span><span class="sxs-lookup"><span data-stu-id="72b91-119">The tutorial demonstrates the following SignalR development tasks:</span></span>

- <span data-ttu-id="72b91-120">SignalR ライブラリを ASP.NET web アプリケーションに追加する。</span><span class="sxs-lookup"><span data-stu-id="72b91-120">Adding the SignalR library to an ASP.NET web application.</span></span>
- <span data-ttu-id="72b91-121">クライアントにコンテンツをプッシュするハブクラスを作成する。</span><span class="sxs-lookup"><span data-stu-id="72b91-121">Creating a hub class to push content to clients.</span></span>
- <span data-ttu-id="72b91-122">Web ページで SignalR jQuery ライブラリを使用して、メッセージを送信し、ハブから更新を表示します。</span><span class="sxs-lookup"><span data-stu-id="72b91-122">Using the SignalR jQuery library in a web page to send messages and display updates from the hub.</span></span>

<span data-ttu-id="72b91-123">次のスクリーンショットは、ブラウザーで実行されているチャットアプリケーションを示しています。</span><span class="sxs-lookup"><span data-stu-id="72b91-123">The following screen shot shows the chat application running in a browser.</span></span> <span data-ttu-id="72b91-124">新しいユーザーごとに、コメントを投稿し、ユーザーがチャットに参加した後に追加されたコメントを表示することができます。</span><span class="sxs-lookup"><span data-stu-id="72b91-124">Each new user can post comments and see comments added after the user joins the chat.</span></span>

![チャットインスタンス](tutorial-getting-started-with-signalr/_static/image1.png)

<span data-ttu-id="72b91-126">各項</span><span class="sxs-lookup"><span data-stu-id="72b91-126">Sections:</span></span>

- [<span data-ttu-id="72b91-127">プロジェクトを設定する</span><span class="sxs-lookup"><span data-stu-id="72b91-127">Set up the Project</span></span>](#setup)
- [<span data-ttu-id="72b91-128">サンプルを実行する</span><span class="sxs-lookup"><span data-stu-id="72b91-128">Run the Sample</span></span>](#run)
- [<span data-ttu-id="72b91-129">コードを確認する</span><span class="sxs-lookup"><span data-stu-id="72b91-129">Examine the Code</span></span>](#code)
- [<span data-ttu-id="72b91-130">次の手順</span><span class="sxs-lookup"><span data-stu-id="72b91-130">Next Steps</span></span>](#next)

<a id="setup"></a>

## <a name="set-up-the-project"></a><span data-ttu-id="72b91-131">プロジェクトを設定する</span><span class="sxs-lookup"><span data-stu-id="72b91-131">Set up the Project</span></span>

<span data-ttu-id="72b91-132">このセクションでは、空の ASP.NET web アプリケーションを作成し、SignalR を追加して、チャットアプリケーションを作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="72b91-132">This section shows how to create an empty ASP.NET web application, add SignalR, and create the chat application.</span></span>

<span data-ttu-id="72b91-133">前提条件:</span><span class="sxs-lookup"><span data-stu-id="72b91-133">Prerequisites:</span></span>

- <span data-ttu-id="72b91-134">Visual Studio 2010 SP1 または2012。</span><span class="sxs-lookup"><span data-stu-id="72b91-134">Visual Studio 2010 SP1 or 2012.</span></span> <span data-ttu-id="72b91-135">Visual Studio がインストールされていない場合は、無料の Visual Studio 2012 Express 開発ツールを入手するには、「 [ASP.NET のダウンロード](https://www.asp.net/downloads)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="72b91-135">If you do not have Visual Studio, see [ASP.NET Downloads](https://www.asp.net/downloads) to get the free Visual Studio 2012 Express Development Tool.</span></span>
- <span data-ttu-id="72b91-136">[Microsoft ASP.NET and Web Tools 2012.2](https://go.microsoft.com/fwlink/?LinkId=279941)。</span><span class="sxs-lookup"><span data-stu-id="72b91-136">[Microsoft ASP.NET and Web Tools 2012.2](https://go.microsoft.com/fwlink/?LinkId=279941).</span></span> <span data-ttu-id="72b91-137">Visual Studio 2012 では、このインストーラーによって、SignalR テンプレートを含む新しい ASP.NET 機能が Visual Studio に追加されます。</span><span class="sxs-lookup"><span data-stu-id="72b91-137">For Visual Studio 2012, this installer adds new ASP.NET features including SignalR templates to Visual Studio.</span></span> <span data-ttu-id="72b91-138">Visual Studio 2010 SP1 では、インストーラーは使用できませんが、セットアップ手順の説明に従って SignalR NuGet パッケージをインストールすることによって、このチュートリアルを完了できます。</span><span class="sxs-lookup"><span data-stu-id="72b91-138">For Visual Studio 2010 SP1, an installer is not available but you can complete the tutorial by installing the SignalR NuGet package as described in the setup steps.</span></span>

<span data-ttu-id="72b91-139">次の手順では、Visual Studio 2012 を使用して、空の ASP.NET Web アプリケーションを作成し、SignalR ライブラリを追加します。</span><span class="sxs-lookup"><span data-stu-id="72b91-139">The following steps use Visual Studio 2012 to create an ASP.NET Empty Web Application and add the SignalR library:</span></span>

1. <span data-ttu-id="72b91-140">Visual Studio で、ASP.NET 空の Web アプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="72b91-140">In Visual Studio create an ASP.NET Empty Web Application.</span></span>

    ![空の web の作成](tutorial-getting-started-with-signalr/_static/image2.png)
2. <span data-ttu-id="72b91-142">[ツール] を選択して**パッケージマネージャーコンソール**を開きます。 **NuGet パッケージマネージャー |パッケージマネージャーコンソール**。</span><span class="sxs-lookup"><span data-stu-id="72b91-142">Open the **Package Manager Console** by selecting **Tools | NuGet Package Manager | Package Manager Console**.</span></span> <span data-ttu-id="72b91-143">コンソールウィンドウに次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="72b91-143">Enter the following command into the console window:</span></span>

    `Install-Package Microsoft.AspNet.SignalR -Version 1.1.3`

    <span data-ttu-id="72b91-144">このコマンドは、SignalR 1.x の最新バージョンをインストールします。</span><span class="sxs-lookup"><span data-stu-id="72b91-144">This command installs the latest version of SignalR 1.x.</span></span>
3. <span data-ttu-id="72b91-145">**ソリューションエクスプローラー**で、プロジェクトを右クリックし、[追加] を選択します。 **クラス**。</span><span class="sxs-lookup"><span data-stu-id="72b91-145">In **Solution Explorer**, right-click the project, select **Add | Class**.</span></span> <span data-ttu-id="72b91-146">新しいクラスに**ChatHub**という名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="72b91-146">Name the new class **ChatHub**.</span></span>
4. <span data-ttu-id="72b91-147">**ソリューションエクスプローラー** [スクリプト] ノードを展開します。</span><span class="sxs-lookup"><span data-stu-id="72b91-147">In **Solution Explorer** expand the Scripts node.</span></span> <span data-ttu-id="72b91-148">JQuery と SignalR のスクリプトライブラリは、プロジェクトに表示されます。</span><span class="sxs-lookup"><span data-stu-id="72b91-148">Script libraries for jQuery and SignalR are visible in the project.</span></span>

    ![ライブラリ参照](tutorial-getting-started-with-signalr/_static/image3.png)
5. <span data-ttu-id="72b91-150">**ChatHub**クラスのコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="72b91-150">Replace the code in the **ChatHub** class with the following code.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample1.cs)]
6. <span data-ttu-id="72b91-151">**ソリューションエクスプローラー**で、プロジェクトを右クリックし、[追加] をクリックします。 **新しい項目**。</span><span class="sxs-lookup"><span data-stu-id="72b91-151">In **Solution Explorer**, right-click the project, then click **Add | New Item**.</span></span> <span data-ttu-id="72b91-152">**[新しい項目の追加]** ダイアログで、 **[グローバルアプリケーションクラス]** を選択し、 **[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="72b91-152">In the **Add New Item** dialog, select **Global Application Class** and click **Add**.</span></span>

    ![グローバルの追加](tutorial-getting-started-with-signalr/_static/image4.png)
7. <span data-ttu-id="72b91-154">Global.asax.cs クラスの指定された `using` ステートメントの後に、次の `using` ステートメントを追加します。</span><span class="sxs-lookup"><span data-stu-id="72b91-154">Add the following `using` statements after the provided `using` statements in the Global.asax.cs class.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample2.cs)]
8. <span data-ttu-id="72b91-155">SignalR hub の既定のルートを登録するには、グローバルクラスの `Application_Start` メソッドに次のコード行を追加します。</span><span class="sxs-lookup"><span data-stu-id="72b91-155">Add the following line of code in the `Application_Start` method of the Global class to register the default route for SignalR hubs.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample3.cs)]
9. <span data-ttu-id="72b91-156">**ソリューションエクスプローラー**で、プロジェクトを右クリックし、[追加] をクリックします。 **新しい項目**。</span><span class="sxs-lookup"><span data-stu-id="72b91-156">In **Solution Explorer**, right-click the project, then click **Add | New Item**.</span></span> <span data-ttu-id="72b91-157">**[新しい項目の追加]** ダイアログで、Html ページ を選択し、 **[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="72b91-157">In the **Add New Item** dialog, select Html Page and click **Add**.</span></span>
10. <span data-ttu-id="72b91-158">**ソリューションエクスプローラー**で、先ほど作成した HTML ページを右クリックし、 **[スタートページとして設定]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="72b91-158">In **Solution Explorer**, right-click the HTML page you just created and click **Set as Start Page**.</span></span>
11. <span data-ttu-id="72b91-159">HTML ページの既定のコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="72b91-159">Replace the default code in the HTML page with the following code.</span></span>

    [!code-html[Main](tutorial-getting-started-with-signalr/samples/sample4.html)]
12. <span data-ttu-id="72b91-160">プロジェクトの**すべてを保存**します。</span><span class="sxs-lookup"><span data-stu-id="72b91-160">**Save All** for the project.</span></span>

<a id="run"></a>

## <a name="run-the-sample"></a><span data-ttu-id="72b91-161">サンプルを実行する</span><span class="sxs-lookup"><span data-stu-id="72b91-161">Run the Sample</span></span>

1. <span data-ttu-id="72b91-162">F5 キーを押して、プロジェクトをデバッグモードで実行します。</span><span class="sxs-lookup"><span data-stu-id="72b91-162">Press F5 to run the project in debug mode.</span></span> <span data-ttu-id="72b91-163">HTML ページがブラウザーインスタンスに読み込まれ、ユーザー名の入力が求められます。</span><span class="sxs-lookup"><span data-stu-id="72b91-163">The HTML page loads in a browser instance and prompts for a user name.</span></span>

    ![ユーザー名の入力](tutorial-getting-started-with-signalr/_static/image5.png)
2. <span data-ttu-id="72b91-165">ユーザー名を入力します。</span><span class="sxs-lookup"><span data-stu-id="72b91-165">Enter a user name.</span></span>
3. <span data-ttu-id="72b91-166">ブラウザーのアドレス行から URL をコピーし、それを使用して2つ以上のブラウザーインスタンスを開きます。</span><span class="sxs-lookup"><span data-stu-id="72b91-166">Copy the URL from the address line of the browser and use it to open two more browser instances.</span></span> <span data-ttu-id="72b91-167">各ブラウザーインスタンスで、一意のユーザー名を入力します。</span><span class="sxs-lookup"><span data-stu-id="72b91-167">In each browser instance, enter a unique user name.</span></span>
4. <span data-ttu-id="72b91-168">各ブラウザーインスタンスで、コメントを追加し、 **[送信]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="72b91-168">In each browser instance, add a comment and click **Send**.</span></span> <span data-ttu-id="72b91-169">コメントは、すべてのブラウザーインスタンスに表示されます。</span><span class="sxs-lookup"><span data-stu-id="72b91-169">The comments should display in all browser instances.</span></span>

    > [!NOTE]
    > <span data-ttu-id="72b91-170">この単純なチャットアプリケーションでは、サーバー上のディスカッションコンテキストは維持されません。</span><span class="sxs-lookup"><span data-stu-id="72b91-170">This simple chat application does not maintain the discussion context on the server.</span></span> <span data-ttu-id="72b91-171">ハブは、現在のすべてのユーザーにコメントをブロードキャストします。</span><span class="sxs-lookup"><span data-stu-id="72b91-171">The hub broadcasts comments to all current users.</span></span> <span data-ttu-id="72b91-172">後でチャットに参加したユーザーには、参加したときから追加されたメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="72b91-172">Users who join the chat later will see messages added from the time they join.</span></span>

    <span data-ttu-id="72b91-173">次のスクリーンショットは、3つのブラウザーインスタンスで実行されているチャットアプリケーションを示しています。これらはすべて、1つのインスタンスがメッセージを送信したときに更新されます。</span><span class="sxs-lookup"><span data-stu-id="72b91-173">The following screen shot shows the chat application running in three browser instances, all of which are updated when one instance sends a message:</span></span>

    ![チャットブラウザー](tutorial-getting-started-with-signalr/_static/image6.png)
5. <span data-ttu-id="72b91-175">**ソリューションエクスプローラー**で、実行中のアプリケーションの **[スクリプトドキュメント]** ノードを調べます。</span><span class="sxs-lookup"><span data-stu-id="72b91-175">In **Solution Explorer**, inspect the **Script Documents** node for the running application.</span></span> <span data-ttu-id="72b91-176">SignalR ライブラリによって実行時に動的に生成される**ハブ**という名前のスクリプトファイルがあります。</span><span class="sxs-lookup"><span data-stu-id="72b91-176">There is a script file named **hubs** that the SignalR library dynamically generates at runtime.</span></span> <span data-ttu-id="72b91-177">このファイルは、jQuery スクリプトとサーバー側コード間の通信を管理します。</span><span class="sxs-lookup"><span data-stu-id="72b91-177">This file manages the communication between jQuery script and server-side code.</span></span>

    ![生成されたハブスクリプト](tutorial-getting-started-with-signalr/_static/image7.png)

<a id="code"></a>

## <a name="examine-the-code"></a><span data-ttu-id="72b91-179">コードを確認する</span><span class="sxs-lookup"><span data-stu-id="72b91-179">Examine the Code</span></span>

<span data-ttu-id="72b91-180">SignalR chat アプリケーションでは、2つの基本的な SignalR 開発タスクを示しています。サーバー上の主要な調整オブジェクトとしてハブを作成し、SignalR jQuery ライブラリを使用してメッセージを送受信します。</span><span class="sxs-lookup"><span data-stu-id="72b91-180">The SignalR chat application demonstrates two basic SignalR development tasks: creating a hub as the main coordination object on the server, and using the SignalR jQuery library to send and receive messages.</span></span>

### <a name="signalr-hubs"></a><span data-ttu-id="72b91-181">SignalR Hubs</span><span class="sxs-lookup"><span data-stu-id="72b91-181">SignalR Hubs</span></span>

<span data-ttu-id="72b91-182">コードサンプルでは、 **ChatHub**クラスは**SignalR**クラスから派生しています。</span><span class="sxs-lookup"><span data-stu-id="72b91-182">In the code sample the **ChatHub** class derives from the **Microsoft.AspNet.SignalR.Hub** class.</span></span> <span data-ttu-id="72b91-183">**ハブ**クラスからの派生は、SignalR アプリケーションを構築するための便利な方法です。</span><span class="sxs-lookup"><span data-stu-id="72b91-183">Deriving from the **Hub** class is a useful way to build a SignalR application.</span></span> <span data-ttu-id="72b91-184">ハブクラスにパブリックメソッドを作成し、web ページの jQuery スクリプトからメソッドを呼び出すことによって、これらのメソッドにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="72b91-184">You can create public methods on your hub class and then access those methods by calling them from jQuery scripts in a web page.</span></span>

<span data-ttu-id="72b91-185">チャットコードでは、クライアントは**ChatHub**メソッドを呼び出して、新しいメッセージを送信します。</span><span class="sxs-lookup"><span data-stu-id="72b91-185">In the chat code, clients call the **ChatHub.Send** method to send a new message.</span></span> <span data-ttu-id="72b91-186">ハブは、 **broadcastMessage**を呼び出すことによって、すべてのクライアントにメッセージを送信します。</span><span class="sxs-lookup"><span data-stu-id="72b91-186">The hub in turn sends the message to all clients by calling **Clients.All.broadcastMessage**.</span></span>

<span data-ttu-id="72b91-187">**Send**メソッドは、いくつかのハブの概念を示しています。</span><span class="sxs-lookup"><span data-stu-id="72b91-187">The **Send** method demonstrates several hub concepts :</span></span>

- <span data-ttu-id="72b91-188">クライアントがそれらを呼び出すことができるように、ハブでパブリックメソッドを宣言します。</span><span class="sxs-lookup"><span data-stu-id="72b91-188">Declare public methods on a hub so that clients can call them.</span></span>
- <span data-ttu-id="72b91-189">このハブに接続されているすべてのクライアントにアクセスするには、 **SignalR**動的プロパティを使用します。</span><span class="sxs-lookup"><span data-stu-id="72b91-189">Use the **Microsoft.AspNet.SignalR.Hub.Clients** dynamic property to access all clients connected to this hub.</span></span>
- <span data-ttu-id="72b91-190">クライアントの jQuery 関数 (`broadcastMessage` 関数など) を呼び出して、クライアントを更新します。</span><span class="sxs-lookup"><span data-stu-id="72b91-190">Call a jQuery function on the client (such as the `broadcastMessage` function) to update clients.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample5.cs)]

### <a name="signalr-and-jquery"></a><span data-ttu-id="72b91-191">SignalR と jQuery</span><span class="sxs-lookup"><span data-stu-id="72b91-191">SignalR and jQuery</span></span>

<span data-ttu-id="72b91-192">コードサンプルの HTML ページは、SignalR jQuery ライブラリを使用して SignalR hub と通信する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="72b91-192">The HTML page in the code sample shows how to use the SignalR jQuery library to communicate with a SignalR hub.</span></span> <span data-ttu-id="72b91-193">コードの重要なタスクは、ハブを参照するようにプロキシを宣言し、サーバーがクライアントにコンテンツをプッシュするために呼び出すことができる関数を宣言し、ハブにメッセージを送信するための接続を開始することです。</span><span class="sxs-lookup"><span data-stu-id="72b91-193">The essential tasks in the code are declaring a proxy to reference the hub, declaring a function that the server can call to push content to clients, and starting a connection to send messages to the hub.</span></span>

<span data-ttu-id="72b91-194">次のコードでは、ハブのプロキシを宣言しています。</span><span class="sxs-lookup"><span data-stu-id="72b91-194">The following code declares a proxy for a hub.</span></span>

[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample6.js)]

> [!NOTE]
> <span data-ttu-id="72b91-195">JQuery では、サーバークラスとそのメンバーへの参照は camel 形式です。</span><span class="sxs-lookup"><span data-stu-id="72b91-195">In jQuery the reference to the server class and its members is in camel case.</span></span> <span data-ttu-id="72b91-196">このコードサンプルではC# 、jQuery の**ChatHub**クラスを**ChatHub**として参照しています。</span><span class="sxs-lookup"><span data-stu-id="72b91-196">The code sample references the C# **ChatHub** class in jQuery as **chatHub**.</span></span>

<span data-ttu-id="72b91-197">次のコードは、スクリプトでコールバック関数を作成する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="72b91-197">The following code is how you create a callback function in the script.</span></span> <span data-ttu-id="72b91-198">サーバー上のハブクラスは、この関数を呼び出して、コンテンツの更新を各クライアントにプッシュします。</span><span class="sxs-lookup"><span data-stu-id="72b91-198">The hub class on the server calls this function to push content updates to each client.</span></span> <span data-ttu-id="72b91-199">HTML でコンテンツを表示する前にエンコードする2行は省略可能であり、スクリプトインジェクションを防ぐ簡単な方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="72b91-199">The two lines that HTML encode the content before displaying it are optional and show a simple way to prevent script injection.</span></span>

[!code-html[Main](tutorial-getting-started-with-signalr/samples/sample7.html)]

<span data-ttu-id="72b91-200">次のコードは、ハブとの接続を開く方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="72b91-200">The following code shows how to open a connection with the hub.</span></span> <span data-ttu-id="72b91-201">このコードは接続を開始し、HTML ページの **[送信]** ボタンでクリックイベントを処理する関数に渡します。</span><span class="sxs-lookup"><span data-stu-id="72b91-201">The code starts the connection and then passes it a function to handle the click event on the **Send** button in the HTML page.</span></span>

> [!NOTE]
> <span data-ttu-id="72b91-202">この方法では、イベントハンドラーが実行される前に接続が確立されることを保証します。</span><span class="sxs-lookup"><span data-stu-id="72b91-202">This approach insures that the connection is established before the event handler executes.</span></span>

[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample8.js)]

<a id="next"></a>

## <a name="next-steps"></a><span data-ttu-id="72b91-203">次の手順</span><span class="sxs-lookup"><span data-stu-id="72b91-203">Next Steps</span></span>

<span data-ttu-id="72b91-204">SignalR は、リアルタイム web アプリケーションを構築するためのフレームワークであることを学習しました。</span><span class="sxs-lookup"><span data-stu-id="72b91-204">You learned that SignalR is a framework for building real-time web applications.</span></span> <span data-ttu-id="72b91-205">また、いくつかの SignalR 開発タスク (SignalR を ASP.NET アプリケーションに追加する方法、ハブクラスを作成する方法、ハブからメッセージを送受信する方法) についても学習しました。</span><span class="sxs-lookup"><span data-stu-id="72b91-205">You also learned several SignalR development tasks: how to add SignalR to an ASP.NET application, how to create a hub class, and how to send and receive messages from the hub.</span></span>

<span data-ttu-id="72b91-206">このチュートリアルまたは他の SignalR アプリケーションのサンプルアプリケーションは、ホストプロバイダーに展開することで、インターネット経由で利用できます。</span><span class="sxs-lookup"><span data-stu-id="72b91-206">You can make the sample application in this tutorial or other SignalR applications available over the Internet by deploying them to a hosting provider.</span></span> <span data-ttu-id="72b91-207">Microsoft では、無料の[Windows Azure 試用版アカウント](https://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A443DD604)で最大10個の web サイトを無料で提供しています。</span><span class="sxs-lookup"><span data-stu-id="72b91-207">Microsoft offers free web hosting for up to 10 web sites in a free [Windows Azure trial account](https://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A443DD604).</span></span> <span data-ttu-id="72b91-208">サンプル SignalR アプリケーションをデプロイする方法のチュートリアルについては、「 [Windows Azure Web サイトとしての SignalR はじめにサンプルの発行](https://blogs.msdn.com/b/timlee/archive/2013/02/27/deploy-the-signalr-getting-started-sample-as-a-windows-azure-web-site.aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="72b91-208">For a walkthrough on how to deploy the sample SignalR application, see [Publish the SignalR Getting Started Sample as a Windows Azure Web Site](https://blogs.msdn.com/b/timlee/archive/2013/02/27/deploy-the-signalr-getting-started-sample-as-a-windows-azure-web-site.aspx).</span></span> <span data-ttu-id="72b91-209">Visual Studio web プロジェクトを Windows Azure の Web サイトに配置する方法の詳細については、「 [Windows azure Web サイトへの ASP.NET アプリケーションの配置](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="72b91-209">For detailed information about how to deploy a Visual Studio web project to a Windows Azure Web Site, see [Deploying an ASP.NET Application to a Windows Azure Web Site](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet).</span></span> <span data-ttu-id="72b91-210">(注: WebSocket トランスポートは、現在、Windows Azure Websites ではサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="72b91-210">(Note: The WebSocket transport is not currently supported for Windows Azure Web Sites.</span></span> <span data-ttu-id="72b91-211">WebSocket トランスポートが使用できない場合、SignalR は、 [SignalR の概要](index.md)に関するトピックの「トランスポート」セクションで説明されている他の利用可能なトランスポートを使用します。)</span><span class="sxs-lookup"><span data-stu-id="72b91-211">When WebSocket transport is not available, SignalR uses the other available transports as described in the Transports section of the [Introduction to SignalR topic](index.md).)</span></span>

<span data-ttu-id="72b91-212">より高度な SignalR 開発の概念を学習するには、次のサイトで SignalR ソースコードとリソースを参照してください。</span><span class="sxs-lookup"><span data-stu-id="72b91-212">To learn more advanced SignalR developments concepts, visit the following sites for SignalR source code and resources:</span></span>

- [<span data-ttu-id="72b91-213">SignalR プロジェクト</span><span class="sxs-lookup"><span data-stu-id="72b91-213">SignalR Project</span></span>](http://signalr.net)
- [<span data-ttu-id="72b91-214">SignalR Github とサンプル</span><span class="sxs-lookup"><span data-stu-id="72b91-214">SignalR Github and Samples</span></span>](https://github.com/SignalR/SignalR)
- [<span data-ttu-id="72b91-215">SignalR Wiki</span><span class="sxs-lookup"><span data-stu-id="72b91-215">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)
