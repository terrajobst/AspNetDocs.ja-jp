---
uid: signalr/overview/getting-started/tutorial-getting-started-with-signalr
title: 'チュートリアル: SignalR 2 を使用したリアルタイムチャットMicrosoft Docs'
author: bradygaster
description: このチュートリアルでは、SignalR を使用してリアルタイムのチャット アプリケーションを作成する方法を示します。 空の ASP.NET web アプリケーションに SignalR を追加します。
ms.author: bradyg
ms.date: 01/22/2019
ms.assetid: a8b3b778-f009-4369-85c7-e90f9878d8b4
msc.legacyurl: /signalr/overview/getting-started/tutorial-getting-started-with-signalr
msc.type: authoredcontent
ms.topic: tutorial
ms.openlocfilehash: bc4ef190b6e36812b6fe7ca4e16eb763431e0e82
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78431566"
---
# <a name="tutorial-real-time-chat-with-signalr-2"></a><span data-ttu-id="12fd6-104">チュートリアル: SignalR 2 を使用したリアルタイムチャット</span><span class="sxs-lookup"><span data-stu-id="12fd6-104">Tutorial: Real-time chat with SignalR 2</span></span>

<span data-ttu-id="12fd6-105">このチュートリアルでは、SignalR を使用してリアルタイムチャットアプリケーションを作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="12fd6-105">This tutorial shows you how to use SignalR to create a real-time chat application.</span></span> <span data-ttu-id="12fd6-106">SignalR を空の ASP.NET web アプリケーションに追加し、メッセージを送信して表示する HTML ページを作成します。</span><span class="sxs-lookup"><span data-stu-id="12fd6-106">You add SignalR to an empty ASP.NET web application and create an HTML page to send and display messages.</span></span>

<span data-ttu-id="12fd6-107">このチュートリアルでは、次のことを行いました。</span><span class="sxs-lookup"><span data-stu-id="12fd6-107">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="12fd6-108">プロジェクトのセットアップ</span><span class="sxs-lookup"><span data-stu-id="12fd6-108">Set up the project</span></span>
> * <span data-ttu-id="12fd6-109">サンプルを実行する</span><span class="sxs-lookup"><span data-stu-id="12fd6-109">Run the sample</span></span>
> * <span data-ttu-id="12fd6-110">コードを確認する</span><span class="sxs-lookup"><span data-stu-id="12fd6-110">Examine the code</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

## <a name="prerequisites"></a><span data-ttu-id="12fd6-111">前提条件</span><span class="sxs-lookup"><span data-stu-id="12fd6-111">Prerequisites</span></span>

* <span data-ttu-id="12fd6-112">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) と **ASP.NET および開発**ワークロード。</span><span class="sxs-lookup"><span data-stu-id="12fd6-112">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) with the **ASP.NET and web development** workload.</span></span>

## <a name="set-up-the-project"></a><span data-ttu-id="12fd6-113">プロジェクトを設定する</span><span class="sxs-lookup"><span data-stu-id="12fd6-113">Set up the Project</span></span>

<span data-ttu-id="12fd6-114">このセクションでは、Visual Studio 2017 と SignalR 2 を使用して空の ASP.NET web アプリケーションを作成し、SignalR を追加して、チャットアプリケーションを作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="12fd6-114">This section shows how to use Visual Studio 2017 and SignalR 2 to create an empty ASP.NET web application, add SignalR, and create the chat application.</span></span>

1. <span data-ttu-id="12fd6-115">Visual Studio で、ASP.NET Web アプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="12fd6-115">In Visual Studio, create an ASP.NET Web Application.</span></span>

    ![Web の作成](tutorial-getting-started-with-signalr/_static/image2.png)

1. <span data-ttu-id="12fd6-117">**新しい ASP.NET プロジェクト-SignalRChat**ウィンドウで、**空**のままにして [ **OK]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="12fd6-117">In the **New ASP.NET Project - SignalRChat** window, leave **Empty** selected and select **OK**.</span></span>

1. <span data-ttu-id="12fd6-118">**ソリューションエクスプローラー**で、プロジェクトを右クリックし、[ > **新しい項目**の**追加**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="12fd6-118">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="12fd6-119">**[新しい項目の追加-signalrchat]** で、[**インストール済み** > **Visual C#**  > **Web** > **SignalR** ] を選択し、 **[SignalR Hub クラス (v2)]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="12fd6-119">In **Add New Item - SignalRChat**, select **Installed** > **Visual C#** > **Web** > **SignalR**  and then select **SignalR Hub Class (v2)**.</span></span>

1. <span data-ttu-id="12fd6-120">クラスに*ChatHub*という名前を指定し、プロジェクトに追加します。</span><span class="sxs-lookup"><span data-stu-id="12fd6-120">Name the class *ChatHub* and add it to the project.</span></span>

    <span data-ttu-id="12fd6-121">この手順では、 *ChatHub.cs*クラスファイルを作成し、SignalR をサポートする一連のスクリプトファイルとアセンブリ参照をプロジェクトに追加します。</span><span class="sxs-lookup"><span data-stu-id="12fd6-121">This step creates the *ChatHub.cs* class file and adds a set of script files and assembly references that support SignalR to the project.</span></span>

1. <span data-ttu-id="12fd6-122">新しい*ChatHub.cs*クラスファイルのコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="12fd6-122">Replace the code in the new *ChatHub.cs* class file with this code:</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample1.cs)]

1. <span data-ttu-id="12fd6-123">**ソリューションエクスプローラー**で、プロジェクトを右クリックし、[ > **新しい項目**の**追加**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="12fd6-123">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="12fd6-124">**[新しい項目の追加-signalrchat]** で、[**インストールされている** > **Visual C#**  > **Web** ] を選択し、 **[OWIN Startup Class]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="12fd6-124">In **Add New Item - SignalRChat** select **Installed** > **Visual C#** > **Web**  and then select **OWIN Startup Class**.</span></span>

1. <span data-ttu-id="12fd6-125">クラスに*スタートアップ*の名前を指定し、プロジェクトに追加します。</span><span class="sxs-lookup"><span data-stu-id="12fd6-125">Name the class *Startup* and add it to the project.</span></span>

1. <span data-ttu-id="12fd6-126">*Startup*クラスの既定のコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="12fd6-126">Replace the default code in *Startup* class with this code:</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample2.cs)]

1. <span data-ttu-id="12fd6-127">**ソリューションエクスプローラー**で、プロジェクトを右クリックし、[ > **HTML ページ**の**追加**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="12fd6-127">In **Solution Explorer**, right-click the project and select **Add** > **HTML Page**.</span></span>

1. <span data-ttu-id="12fd6-128">新しいページの*インデックス*に名前を付け、[ **OK]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="12fd6-128">Name the new page *index* and select **OK**.</span></span>

1. <span data-ttu-id="12fd6-129">**ソリューションエクスプローラー**で、作成した HTML ページを右クリックし、 **[スタートページとして設定]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="12fd6-129">In **Solution Explorer**, right-click the HTML page you created and select **Set as Start Page**.</span></span>

1. <span data-ttu-id="12fd6-130">HTML ページの既定のコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="12fd6-130">Replace the default code in the HTML page with this code:</span></span>

    [!code-html[Main](tutorial-getting-started-with-signalr/samples/sample3.html)]

1. <span data-ttu-id="12fd6-131">**ソリューションエクスプローラー**で、 **[スクリプト]** を展開します。</span><span class="sxs-lookup"><span data-stu-id="12fd6-131">In **Solution Explorer**, expand **Scripts**.</span></span>

    <span data-ttu-id="12fd6-132">JQuery と SignalR のスクリプトライブラリは、プロジェクトに表示されます。</span><span class="sxs-lookup"><span data-stu-id="12fd6-132">Script libraries for jQuery and SignalR are visible in the project.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="12fd6-133">パッケージマネージャーで、SignalR スクリプトの新しいバージョンがインストールされている可能性があります。</span><span class="sxs-lookup"><span data-stu-id="12fd6-133">The package manager may have installed a later version of the SignalR scripts.</span></span>

1. <span data-ttu-id="12fd6-134">コードブロック内のスクリプト参照が、プロジェクト内のスクリプトファイルのバージョンに対応していることを確認します。</span><span class="sxs-lookup"><span data-stu-id="12fd6-134">Check that the script references in the code block correspond to the versions of the script files in the project.</span></span>

    <span data-ttu-id="12fd6-135">元のコードブロックからのスクリプト参照:</span><span class="sxs-lookup"><span data-stu-id="12fd6-135">Script references from the original code block:</span></span>

    ```html
    <!--Script references. -->
    <!--Reference the jQuery library. -->
    <script src="Scripts/jquery-3.1.1.min.js" ></script>
    <!--Reference the SignalR library. -->
    <script src="Scripts/jquery.signalR-2.2.1.min.js"></script>
    ```

1. <span data-ttu-id="12fd6-136">一致しない場合は、 *.html*ファイルを更新します。</span><span class="sxs-lookup"><span data-stu-id="12fd6-136">If they don't match, update the *.html* file.</span></span>

1. <span data-ttu-id="12fd6-137">メニューバーで **[ファイル]** 、 **[すべて保存]** の > を選択します。</span><span class="sxs-lookup"><span data-stu-id="12fd6-137">From the menu bar, select **File** > **Save All**.</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="12fd6-138">サンプルを実行する</span><span class="sxs-lookup"><span data-stu-id="12fd6-138">Run the Sample</span></span>

1. <span data-ttu-id="12fd6-139">ツールバーの **スクリプトデバッグ** をオンにし、再生 ボタンを選択して、サンプルをデバッグモードで実行します。</span><span class="sxs-lookup"><span data-stu-id="12fd6-139">In the toolbar, turn on **Script Debugging** and then select the play button to run the sample in Debug mode.</span></span>

    ![ユーザー名の入力](tutorial-getting-started-with-signalr/_static/image3.png)

1. <span data-ttu-id="12fd6-141">ブラウザーが開いたら、チャット id の名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="12fd6-141">When the browser opens, enter a name for your chat identity.</span></span>

1. <span data-ttu-id="12fd6-142">ブラウザーから URL をコピーし、他の2つのブラウザーを開いて、アドレスバーに Url を貼り付けます。</span><span class="sxs-lookup"><span data-stu-id="12fd6-142">Copy the URL from the browser, open two other browsers, and paste the URLs into the address bars.</span></span>

1. <span data-ttu-id="12fd6-143">各ブラウザーで、一意の名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="12fd6-143">In each browser, enter a unique name.</span></span>

1. <span data-ttu-id="12fd6-144">ここで、コメントを追加し、 **[送信]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="12fd6-144">Now, add a comment and select **Send**.</span></span> <span data-ttu-id="12fd6-145">他のブラウザーでも同じ手順を繰り返します。</span><span class="sxs-lookup"><span data-stu-id="12fd6-145">Repeat that in the other browsers.</span></span> <span data-ttu-id="12fd6-146">コメントはリアルタイムで表示されます。</span><span class="sxs-lookup"><span data-stu-id="12fd6-146">The comments appear in real-time.</span></span>

    > [!NOTE]
    > <span data-ttu-id="12fd6-147">この単純なチャットアプリケーションでは、サーバー上のディスカッションコンテキストは維持されません。</span><span class="sxs-lookup"><span data-stu-id="12fd6-147">This simple chat application does not maintain the discussion context on the server.</span></span> <span data-ttu-id="12fd6-148">ハブは、現在のすべてのユーザーにコメントをブロードキャストします。</span><span class="sxs-lookup"><span data-stu-id="12fd6-148">The hub broadcasts comments to all current users.</span></span> <span data-ttu-id="12fd6-149">後でチャットに参加したユーザーには、参加したときから追加されたメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="12fd6-149">Users who join the chat later will see messages added from the time they join.</span></span>

    <span data-ttu-id="12fd6-150">チャットアプリケーションを3つの異なるブラウザーで実行する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="12fd6-150">See how the chat application runs in three different browsers.</span></span> <span data-ttu-id="12fd6-151">Tom、Anand、およびスーザンがメッセージを送信すると、すべてのブラウザーがリアルタイムで更新されます。</span><span class="sxs-lookup"><span data-stu-id="12fd6-151">When Tom, Anand, and Susan send messages, all browsers update in real time:</span></span>

    ![3つのブラウザーすべてに同じチャット履歴が表示されます](tutorial-getting-started-with-signalr/_static/image4.png)

1. <span data-ttu-id="12fd6-153">**ソリューションエクスプローラー**で、実行中のアプリケーションの **[スクリプトドキュメント]** ノードを調べます。</span><span class="sxs-lookup"><span data-stu-id="12fd6-153">In **Solution Explorer**, inspect the **Script Documents** node for the running application.</span></span> <span data-ttu-id="12fd6-154">SignalR ライブラリによって実行時に生成される*ハブ*という名前のスクリプトファイルがあります。</span><span class="sxs-lookup"><span data-stu-id="12fd6-154">There's a script file named *hubs* that the SignalR library generates at runtime.</span></span> <span data-ttu-id="12fd6-155">このファイルは、jQuery スクリプトとサーバー側コード間の通信を管理します。</span><span class="sxs-lookup"><span data-stu-id="12fd6-155">This file manages the communication between jQuery script and server-side code.</span></span>

    ![スクリプトドキュメントノードで自動生成されたハブスクリプト](tutorial-getting-started-with-signalr/_static/image5.png)

## <a name="examine-the-code"></a><span data-ttu-id="12fd6-157">コードを確認する</span><span class="sxs-lookup"><span data-stu-id="12fd6-157">Examine the Code</span></span>

<span data-ttu-id="12fd6-158">SignalRChat アプリケーションは、2つの基本的な SignalR 開発タスクを示しています。</span><span class="sxs-lookup"><span data-stu-id="12fd6-158">The SignalRChat application demonstrates two basic SignalR development tasks.</span></span> <span data-ttu-id="12fd6-159">ハブを作成する方法についても説明します。</span><span class="sxs-lookup"><span data-stu-id="12fd6-159">It shows you how to create a hub.</span></span> <span data-ttu-id="12fd6-160">サーバーは、そのハブをメイン調整オブジェクトとして使用します。</span><span class="sxs-lookup"><span data-stu-id="12fd6-160">The server uses that hub as the main coordination object.</span></span> <span data-ttu-id="12fd6-161">ハブは、SignalR jQuery ライブラリを使用してメッセージを送受信します。</span><span class="sxs-lookup"><span data-stu-id="12fd6-161">The hub uses the SignalR jQuery library to send and receive messages.</span></span>

### <a name="signalr-hubs-in-the-chathubcs"></a><span data-ttu-id="12fd6-162">ChatHub.cs の SignalR Hub</span><span class="sxs-lookup"><span data-stu-id="12fd6-162">SignalR Hubs in the ChatHub.cs</span></span>

<span data-ttu-id="12fd6-163">上記のコードサンプルでは、`ChatHub` クラスは `Microsoft.AspNet.SignalR.Hub` クラスから派生しています。</span><span class="sxs-lookup"><span data-stu-id="12fd6-163">In the code sample above, the `ChatHub` class derives from the `Microsoft.AspNet.SignalR.Hub` class.</span></span> <span data-ttu-id="12fd6-164">`Hub` クラスからの派生は、SignalR アプリケーションを構築するための便利な方法です。</span><span class="sxs-lookup"><span data-stu-id="12fd6-164">Deriving from the `Hub` class is a useful way to build a SignalR application.</span></span> <span data-ttu-id="12fd6-165">ハブクラスにパブリックメソッドを作成し、web ページのスクリプトからそれらのメソッドを呼び出すことによって、これらのメソッドを使用できます。</span><span class="sxs-lookup"><span data-stu-id="12fd6-165">You can create public methods on your hub class and then use those methods by calling them from scripts in a web page.</span></span>

<span data-ttu-id="12fd6-166">チャットコードでは、クライアントは `ChatHub.Send` メソッドを呼び出して、新しいメッセージを送信します。</span><span class="sxs-lookup"><span data-stu-id="12fd6-166">In the chat code, clients call the `ChatHub.Send` method to send a new message.</span></span> <span data-ttu-id="12fd6-167">その後、ハブは `Clients.All.broadcastMessage`を呼び出すことによって、すべてのクライアントにメッセージを送信します。</span><span class="sxs-lookup"><span data-stu-id="12fd6-167">The hub then sends the message to all clients by calling `Clients.All.broadcastMessage`.</span></span>

<span data-ttu-id="12fd6-168">`Send` メソッドは、いくつかのハブの概念を示しています。</span><span class="sxs-lookup"><span data-stu-id="12fd6-168">The `Send` method demonstrates several hub concepts:</span></span>

* <span data-ttu-id="12fd6-169">クライアントがそれらを呼び出すことができるように、ハブでパブリックメソッドを宣言します。</span><span class="sxs-lookup"><span data-stu-id="12fd6-169">Declare public methods on a hub so that clients can call them.</span></span>

* <span data-ttu-id="12fd6-170">このハブに接続されているすべてのクライアントと通信するには、`Microsoft.AspNet.SignalR.Hub.Clients` 動的プロパティを使用します。</span><span class="sxs-lookup"><span data-stu-id="12fd6-170">Use the `Microsoft.AspNet.SignalR.Hub.Clients` dynamic property to communicate with all clients connected to this hub.</span></span>

* <span data-ttu-id="12fd6-171">クライアントの関数 (`broadcastMessage` 関数など) を呼び出して、クライアントを更新します。</span><span class="sxs-lookup"><span data-stu-id="12fd6-171">Call a function on the client (like the `broadcastMessage` function) to update clients.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample4.cs)]

### <a name="signalr-and-jquery-in-the-indexhtml"></a><span data-ttu-id="12fd6-172">SignalR と jQuery の .html</span><span class="sxs-lookup"><span data-stu-id="12fd6-172">SignalR and jQuery in the index.html</span></span>

<span data-ttu-id="12fd6-173">コードサンプルの*SignalR ページは*、SignalR hub と通信するために、jQuery ライブラリを使用する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="12fd6-173">The *index.html* page in the code sample shows how to use the SignalR jQuery library to communicate with a SignalR hub.</span></span> <span data-ttu-id="12fd6-174">このコードでは、多くの重要なタスクが実行されています。</span><span class="sxs-lookup"><span data-stu-id="12fd6-174">The code carries out many important tasks.</span></span> <span data-ttu-id="12fd6-175">このメソッドは、ハブを参照するプロキシを宣言し、サーバーがクライアントにコンテンツをプッシュするために呼び出すことができる関数を宣言し、接続を開始してハブにメッセージを送信します。</span><span class="sxs-lookup"><span data-stu-id="12fd6-175">It declares a proxy to reference the hub, declares a function that the server can call to push content to clients, and it starts a connection to send messages to the hub.</span></span>

[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample5.js)]

> [!NOTE]
> <span data-ttu-id="12fd6-176">JavaScript では、サーバークラスとそのメンバーへの参照はキャメルケースである必要があります。</span><span class="sxs-lookup"><span data-stu-id="12fd6-176">In JavaScript the reference to the server class and its members has to be camelCase.</span></span> <span data-ttu-id="12fd6-177">このコードサンプルではC# 、`chatHub`として JavaScript の*ChatHub*クラスを参照しています。</span><span class="sxs-lookup"><span data-stu-id="12fd6-177">The code sample references the C# *ChatHub* class in JavaScript as `chatHub`.</span></span>

<span data-ttu-id="12fd6-178">このコードブロックでは、スクリプトでコールバック関数を作成します。</span><span class="sxs-lookup"><span data-stu-id="12fd6-178">In this code block, you create a callback function in the script.</span></span>

[!code-html[Main](tutorial-getting-started-with-signalr/samples/sample6.html)]

<span data-ttu-id="12fd6-179">サーバー上のハブクラスは、この関数を呼び出して、コンテンツの更新を各クライアントにプッシュします。</span><span class="sxs-lookup"><span data-stu-id="12fd6-179">The hub class on the server calls this function to push content updates to each client.</span></span> <span data-ttu-id="12fd6-180">コンテンツを表示する前に HTML エンコードする2行は省略可能であり、スクリプトインジェクションを防止するための適切な方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="12fd6-180">The two lines that HTML-encode the content before displaying it are optional and show a good way to prevent script injection.</span></span>

<span data-ttu-id="12fd6-181">このコードは、ハブとの接続を開きます。</span><span class="sxs-lookup"><span data-stu-id="12fd6-181">This code opens a connection with the hub.</span></span>

[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample7.js)]

> [!NOTE]
> <span data-ttu-id="12fd6-182">この方法では、イベントハンドラーが実行される前に、コードによって接続が確立されます。</span><span class="sxs-lookup"><span data-stu-id="12fd6-182">This approach ensures that the code establishes a connection before the event handler executes.</span></span>

<span data-ttu-id="12fd6-183">このコードは接続を開始し、HTML ページの **[送信]** ボタンでクリックイベントを処理する関数に渡します。</span><span class="sxs-lookup"><span data-stu-id="12fd6-183">The code starts the connection and then passes it a function to handle the click event on the **Send** button in the HTML page.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="12fd6-184">コードの入手</span><span class="sxs-lookup"><span data-stu-id="12fd6-184">Get the code</span></span>

[<span data-ttu-id="12fd6-185">完成したプロジェクトのダウンロード</span><span class="sxs-lookup"><span data-stu-id="12fd6-185">Download Completed Project</span></span>](https://code.msdn.microsoft.com/SignalR-Getting-Started-b9d18aa9)

## <a name="additional-resources"></a><span data-ttu-id="12fd6-186">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="12fd6-186">Additional resources</span></span>

<span data-ttu-id="12fd6-187">SignalR の詳細については、次のリソースを参照してください。</span><span class="sxs-lookup"><span data-stu-id="12fd6-187">For more about SignalR, see the following resources:</span></span>

* [<span data-ttu-id="12fd6-188">SignalR プロジェクト</span><span class="sxs-lookup"><span data-stu-id="12fd6-188">SignalR Project</span></span>](http://signalr.net)

* [<span data-ttu-id="12fd6-189">SignalR Github とサンプル</span><span class="sxs-lookup"><span data-stu-id="12fd6-189">SignalR Github and Samples</span></span>](https://github.com/SignalR/SignalR)

* [<span data-ttu-id="12fd6-190">SignalR Wiki</span><span class="sxs-lookup"><span data-stu-id="12fd6-190">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a><span data-ttu-id="12fd6-191">次のステップ</span><span class="sxs-lookup"><span data-stu-id="12fd6-191">Next steps</span></span>

<span data-ttu-id="12fd6-192">このチュートリアルでは、次のことを行います。</span><span class="sxs-lookup"><span data-stu-id="12fd6-192">In this tutorial you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="12fd6-193">プロジェクトのセットアップ</span><span class="sxs-lookup"><span data-stu-id="12fd6-193">Set up the project</span></span>
> * <span data-ttu-id="12fd6-194">サンプルを実行しました</span><span class="sxs-lookup"><span data-stu-id="12fd6-194">Ran the sample</span></span>
> * <span data-ttu-id="12fd6-195">コードを調べる</span><span class="sxs-lookup"><span data-stu-id="12fd6-195">Examined the code</span></span>

<span data-ttu-id="12fd6-196">SignalR と MVC 5 の使用方法については、次の記事に進んでください。</span><span class="sxs-lookup"><span data-stu-id="12fd6-196">Advance to the next article to learn how to use SignalR and MVC 5.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="12fd6-197">SignalR 2 と MVC 5</span><span class="sxs-lookup"><span data-stu-id="12fd6-197">SignalR 2 and MVC 5</span></span>](tutorial-getting-started-with-signalr-and-mvc.md)