---
uid: signalr/overview/getting-started/tutorial-getting-started-with-signalr-and-mvc
title: 'チュートリアル: SignalR 2 と MVC 5 を使用したリアルタイムチャット |Microsoft Docs'
author: bradygaster
description: このチュートリアルでは、ASP.NET SignalR 2 を使用してリアルタイムチャットアプリケーションを作成する方法について説明します。 MVC 5 アプリケーションに SignalR を追加します。
ms.author: bradyg
ms.date: 01/22/2019
ms.assetid: 80bfe5fb-bdfc-41fe-ac43-2132e5d69fac
msc.legacyurl: /signalr/overview/getting-started/tutorial-getting-started-with-signalr-and-mvc
msc.type: authoredcontent
ms.topic: tutorial
ms.openlocfilehash: 5671e4f0123ca2b0cb5314336cf4411467feac70
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78431620"
---
# <a name="tutorial-real-time-chat-with-signalr-2-and-mvc-5"></a><span data-ttu-id="480e2-104">チュートリアル: SignalR 2 と MVC 5 を使用したリアルタイムチャット</span><span class="sxs-lookup"><span data-stu-id="480e2-104">Tutorial: Real-time chat with SignalR 2 and MVC 5</span></span>

<span data-ttu-id="480e2-105">このチュートリアルでは、ASP.NET SignalR 2 を使用してリアルタイムチャットアプリケーションを作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="480e2-105">This tutorial shows how to use ASP.NET SignalR 2 to create a real-time chat application.</span></span> <span data-ttu-id="480e2-106">SignalR を MVC 5 アプリケーションに追加し、メッセージを送信して表示するためのチャットビューを作成します。</span><span class="sxs-lookup"><span data-stu-id="480e2-106">You add SignalR to an MVC 5 application and create a chat view to send and display messages.</span></span>

<span data-ttu-id="480e2-107">このチュートリアルでは、次のことを行いました。</span><span class="sxs-lookup"><span data-stu-id="480e2-107">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="480e2-108">プロジェクトのセットアップ</span><span class="sxs-lookup"><span data-stu-id="480e2-108">Set up the project</span></span>
> * <span data-ttu-id="480e2-109">サンプルを実行する</span><span class="sxs-lookup"><span data-stu-id="480e2-109">Run the sample</span></span>
> * <span data-ttu-id="480e2-110">コードを確認する</span><span class="sxs-lookup"><span data-stu-id="480e2-110">Examine the code</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

## <a name="prerequisites"></a><span data-ttu-id="480e2-111">前提条件</span><span class="sxs-lookup"><span data-stu-id="480e2-111">Prerequisites</span></span>

* <span data-ttu-id="480e2-112">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) と **ASP.NET および開発**ワークロード。</span><span class="sxs-lookup"><span data-stu-id="480e2-112">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) with the **ASP.NET and web development** workload.</span></span>

## <a name="set-up-the-project"></a><span data-ttu-id="480e2-113">プロジェクトを設定する</span><span class="sxs-lookup"><span data-stu-id="480e2-113">Set up the Project</span></span>

<span data-ttu-id="480e2-114">このセクションでは、Visual Studio 2017 と SignalR 2 を使用して、空の ASP.NET MVC 5 アプリケーションを作成する方法、SignalR ライブラリを追加する方法、チャットアプリケーションを作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="480e2-114">This section shows how to use Visual Studio 2017 and SignalR 2 to create an empty ASP.NET MVC 5 application, add the SignalR library, and create the chat application.</span></span>

1. <span data-ttu-id="480e2-115">Visual Studio で、.NET Framework 4.5 C#を対象とする ASP.NET アプリケーションを作成し、SignalRChat という名前を指定して、[OK] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="480e2-115">In Visual Studio, create a C# ASP.NET application that targets .NET Framework 4.5, name it SignalRChat, and click OK.</span></span>

    ![Web の作成](tutorial-getting-started-with-signalr-and-mvc/_static/image1.png)

1. <span data-ttu-id="480e2-117">**New ASP.NET Web アプリケーション-SignalRMvcChat**で、 **[MVC]** を選択し、 **[認証の変更]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="480e2-117">In **New ASP.NET Web Application - SignalRMvcChat**, select **MVC** and then select **Change Authentication**.</span></span>

1. <span data-ttu-id="480e2-118">**[認証の変更]** で、 **[認証なし]** を選択し、 **[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="480e2-118">In **Change Authentication**, select **No Authentication** and click **OK**.</span></span>

    ![[認証なし] を選択する](tutorial-getting-started-with-signalr-and-mvc/_static/image2.png)

1. <span data-ttu-id="480e2-120">**New ASP.NET Web アプリケーション-SignalRMvcChat**で、[ **OK]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="480e2-120">In **New ASP.NET Web Application - SignalRMvcChat**, select **OK**.</span></span>

1. <span data-ttu-id="480e2-121">**ソリューションエクスプローラー**で、プロジェクトを右クリックし、[ > **新しい項目**の**追加**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="480e2-121">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="480e2-122">**[新しい項目の追加-signalrchat]** で、[**インストール済み** > **Visual C#**  > **Web** > **SignalR** ] を選択し、 **[SignalR Hub クラス (v2)]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="480e2-122">In **Add New Item - SignalRChat**, select **Installed** > **Visual C#** > **Web** > **SignalR**  and then select **SignalR Hub Class (v2)**.</span></span>

1. <span data-ttu-id="480e2-123">クラスに*ChatHub*という名前を指定し、プロジェクトに追加します。</span><span class="sxs-lookup"><span data-stu-id="480e2-123">Name the class *ChatHub* and add it to the project.</span></span>

    <span data-ttu-id="480e2-124">この手順では、 *ChatHub.cs*クラスファイルを作成し、SignalR をサポートする一連のスクリプトファイルとアセンブリ参照をプロジェクトに追加します。</span><span class="sxs-lookup"><span data-stu-id="480e2-124">This step creates the *ChatHub.cs* class file and adds a set of script files and assembly references that support SignalR to the project.</span></span>

1. <span data-ttu-id="480e2-125">新しい*ChatHub.cs*クラスファイルのコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="480e2-125">Replace the code in the new *ChatHub.cs* class file with this code:</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample1.cs)]

1. <span data-ttu-id="480e2-126">**ソリューションエクスプローラー**で、プロジェクトを右クリックし、[ > **クラス**の**追加**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="480e2-126">In **Solution Explorer**, right-click the project and select **Add** > **Class**.</span></span>

1. <span data-ttu-id="480e2-127">新しいクラスに「 *Startup* 」という名前を指定し、プロジェクトに追加します。</span><span class="sxs-lookup"><span data-stu-id="480e2-127">Name the new class *Startup* and add it to the project.</span></span>

1. <span data-ttu-id="480e2-128">*Startup.cs*クラスファイル内のコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="480e2-128">Replace the code in the *Startup.cs* class file with this code:</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample2.cs)]

1. <span data-ttu-id="480e2-129">**ソリューションエクスプローラー**で、[**コントローラー** > **HomeController.cs**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="480e2-129">In **Solution Explorer**, select **Controllers** > **HomeController.cs**.</span></span>

1. <span data-ttu-id="480e2-130">このメソッドを*HomeController.cs*に追加します。</span><span class="sxs-lookup"><span data-stu-id="480e2-130">Add this method to the *HomeController.cs*.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample3.cs)]

    <span data-ttu-id="480e2-131">このメソッドは、後の手順で作成した**チャット**ビューを返します。</span><span class="sxs-lookup"><span data-stu-id="480e2-131">This method returns the **Chat** view that you create in a later step.</span></span>

1. <span data-ttu-id="480e2-132">**ソリューションエクスプローラー**で、[**ビュー** > **ホーム**] を右クリックし、[ >  **ビュー**の**追加**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="480e2-132">In **Solution Explorer**, right-click **Views** > **Home**, and select **Add** >  **View**.</span></span>

1. <span data-ttu-id="480e2-133">**[ビューの追加]** で、新しいビューに「**チャット**」という名前を指定し、 **[追加]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="480e2-133">In **Add View**, name the new view **Chat** and select **Add**.</span></span>

1. <span data-ttu-id="480e2-134">**Chat**の内容を次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="480e2-134">Replace the contents of **Chat.cshtml** with this code:</span></span>

    [!code-cshtml[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample4.cshtml)]

1. <span data-ttu-id="480e2-135">**ソリューションエクスプローラー**で、 **[スクリプト]** を展開します。</span><span class="sxs-lookup"><span data-stu-id="480e2-135">In **Solution Explorer**, expand **Scripts**.</span></span>

    <span data-ttu-id="480e2-136">JQuery と SignalR のスクリプトライブラリは、プロジェクトに表示されます。</span><span class="sxs-lookup"><span data-stu-id="480e2-136">Script libraries for jQuery and SignalR are visible in the project.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="480e2-137">パッケージマネージャーで、SignalR スクリプトの新しいバージョンがインストールされている可能性があります。</span><span class="sxs-lookup"><span data-stu-id="480e2-137">The package manager may have installed a later version of the SignalR scripts.</span></span>

1. <span data-ttu-id="480e2-138">コードブロック内のスクリプト参照が、プロジェクト内のスクリプトファイルのバージョンに対応していることを確認します。</span><span class="sxs-lookup"><span data-stu-id="480e2-138">Check that the script references in the code block correspond to the versions of the script files in the project.</span></span>

    <span data-ttu-id="480e2-139">元のコードブロックからのスクリプト参照:</span><span class="sxs-lookup"><span data-stu-id="480e2-139">Script references from the original code block:</span></span>

    ```cshtml
    <!--Script references. -->
    <!--The jQuery library is required and is referenced by default in _Layout.cshtml. -->
    <!--Reference the SignalR library. -->
    <script src="~/Scripts/jquery.signalR-2.1.0.min.js"></script>
    ```

1. <span data-ttu-id="480e2-140">一致しない場合は、 *cshtml*ファイルを更新します。</span><span class="sxs-lookup"><span data-stu-id="480e2-140">If they don't match, update the *.cshtml* file.</span></span>

1. <span data-ttu-id="480e2-141">メニューバーで **[ファイル]** 、 **[すべて保存]** の > を選択します。</span><span class="sxs-lookup"><span data-stu-id="480e2-141">From the menu bar, select **File** > **Save All**.</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="480e2-142">サンプルを実行する</span><span class="sxs-lookup"><span data-stu-id="480e2-142">Run the Sample</span></span>

1. <span data-ttu-id="480e2-143">ツールバーの **スクリプトデバッグ** をオンにし、再生 ボタンを選択して、サンプルをデバッグモードで実行します。</span><span class="sxs-lookup"><span data-stu-id="480e2-143">In the toolbar, turn on **Script Debugging** and then select the play button to run the sample in Debug mode.</span></span>

    ![ユーザー名の入力](tutorial-getting-started-with-signalr-and-mvc/_static/image3.png)

1. <span data-ttu-id="480e2-145">ブラウザーが開いたら、チャット id の名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="480e2-145">When the browser opens, enter a name for your chat identity.</span></span>

1. <span data-ttu-id="480e2-146">ブラウザーから URL をコピーし、他の2つのブラウザーを開いて、アドレスバーに Url を貼り付けます。</span><span class="sxs-lookup"><span data-stu-id="480e2-146">Copy the URL from the browser, open two other browsers, and paste the URLs into the address bars.</span></span>

1. <span data-ttu-id="480e2-147">各ブラウザーで、一意の名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="480e2-147">In each browser, enter a unique name.</span></span>

1. <span data-ttu-id="480e2-148">ここで、コメントを追加し、 **[送信]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="480e2-148">Now, add a comment and select **Send**.</span></span> <span data-ttu-id="480e2-149">他のブラウザーでも同じ手順を繰り返します。</span><span class="sxs-lookup"><span data-stu-id="480e2-149">Repeat that in the other browsers.</span></span> <span data-ttu-id="480e2-150">コメントはリアルタイムで表示されます。</span><span class="sxs-lookup"><span data-stu-id="480e2-150">The comments appear in real time.</span></span>

    > [!NOTE]
    > <span data-ttu-id="480e2-151">この単純なチャットアプリケーションでは、サーバー上のディスカッションコンテキストは維持されません。</span><span class="sxs-lookup"><span data-stu-id="480e2-151">This simple chat application does not maintain the discussion context on the server.</span></span> <span data-ttu-id="480e2-152">ハブは、現在のすべてのユーザーにコメントをブロードキャストします。</span><span class="sxs-lookup"><span data-stu-id="480e2-152">The hub broadcasts comments to all current users.</span></span> <span data-ttu-id="480e2-153">後でチャットに参加したユーザーには、参加したときから追加されたメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="480e2-153">Users who join the chat later will see messages added from the time they join.</span></span>

    <span data-ttu-id="480e2-154">チャットアプリケーションを3つの異なるブラウザーで実行する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="480e2-154">See how the chat application runs in three different browsers.</span></span> <span data-ttu-id="480e2-155">Tom、Anand、およびスーザンがメッセージを送信すると、すべてのブラウザーがリアルタイムで更新されます。</span><span class="sxs-lookup"><span data-stu-id="480e2-155">When Tom, Anand, and Susan send messages, all browsers update in real time:</span></span>

    ![3つのブラウザーすべてに同じチャット履歴が表示されます](tutorial-getting-started-with-signalr-and-mvc/_static/image4.png)

1. <span data-ttu-id="480e2-157">**ソリューションエクスプローラー**で、実行中のアプリケーションの **[スクリプトドキュメント]** ノードを調べます。</span><span class="sxs-lookup"><span data-stu-id="480e2-157">In **Solution Explorer**, inspect the **Script Documents** node for the running application.</span></span> <span data-ttu-id="480e2-158">SignalR ライブラリによって実行時に生成される*ハブ*という名前のスクリプトファイルがあります。</span><span class="sxs-lookup"><span data-stu-id="480e2-158">There's a script file named *hubs* that the SignalR library generates at runtime.</span></span> <span data-ttu-id="480e2-159">このファイルは、jQuery スクリプトとサーバー側コード間の通信を管理します。</span><span class="sxs-lookup"><span data-stu-id="480e2-159">This file manages the communication between jQuery script and server-side code.</span></span>

    ![スクリプトドキュメントノードで自動生成されたハブスクリプト](tutorial-getting-started-with-signalr-and-mvc/_static/image5.png)

## <a name="examine-the-code"></a><span data-ttu-id="480e2-161">コードを確認する</span><span class="sxs-lookup"><span data-stu-id="480e2-161">Examine the Code</span></span>

<span data-ttu-id="480e2-162">SignalR chat アプリケーションは、2つの基本的な SignalR 開発タスクを示しています。</span><span class="sxs-lookup"><span data-stu-id="480e2-162">The SignalR chat application demonstrates two basic SignalR development tasks.</span></span> <span data-ttu-id="480e2-163">ハブを作成する方法についても説明します。</span><span class="sxs-lookup"><span data-stu-id="480e2-163">It shows you how to create a hub.</span></span> <span data-ttu-id="480e2-164">サーバーは、そのハブをメイン調整オブジェクトとして使用します。</span><span class="sxs-lookup"><span data-stu-id="480e2-164">The server uses that hub as the main coordination object.</span></span> <span data-ttu-id="480e2-165">ハブは、SignalR jQuery ライブラリを使用してメッセージを送受信します。</span><span class="sxs-lookup"><span data-stu-id="480e2-165">The hub uses the SignalR jQuery library to send and receive messages.</span></span>

### <a name="signalr-hubs-in-the-chathubcs"></a><span data-ttu-id="480e2-166">ChatHub.cs の SignalR Hub</span><span class="sxs-lookup"><span data-stu-id="480e2-166">SignalR Hubs in the ChatHub.cs</span></span>

<span data-ttu-id="480e2-167">コードサンプルでは、`ChatHub` クラスは `Microsoft.AspNet.SignalR.Hub` クラスから派生します。</span><span class="sxs-lookup"><span data-stu-id="480e2-167">In the code sample, the `ChatHub` class derives from the `Microsoft.AspNet.SignalR.Hub` class.</span></span> <span data-ttu-id="480e2-168">`Hub` クラスからの派生は、SignalR アプリケーションを構築するための便利な方法です。</span><span class="sxs-lookup"><span data-stu-id="480e2-168">Deriving from the `Hub` class is a useful way to build a SignalR application.</span></span> <span data-ttu-id="480e2-169">ハブクラスにパブリックメソッドを作成し、web ページのスクリプトからそれらのメソッドにアクセスすることによって、これらのメソッドにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="480e2-169">You can create public methods on your hub class and then access those methods by calling them from scripts in a web page.</span></span>

<span data-ttu-id="480e2-170">チャットコードでは、クライアントは `ChatHub.Send` メソッドを呼び出して、新しいメッセージを送信します。</span><span class="sxs-lookup"><span data-stu-id="480e2-170">In the chat code, clients call the `ChatHub.Send` method to send a new message.</span></span> <span data-ttu-id="480e2-171">その後、ハブは `Clients.All.addNewMessageToPage`を呼び出すことによって、すべてのクライアントにメッセージを送信します。</span><span class="sxs-lookup"><span data-stu-id="480e2-171">The hub in turn sends the message to all clients by calling `Clients.All.addNewMessageToPage`.</span></span>

<span data-ttu-id="480e2-172">`Send` メソッドは、いくつかのハブの概念を示しています。</span><span class="sxs-lookup"><span data-stu-id="480e2-172">The `Send` method demonstrates several hub concepts:</span></span>

* <span data-ttu-id="480e2-173">クライアントがそれらを呼び出すことができるように、ハブでパブリックメソッドを宣言します。</span><span class="sxs-lookup"><span data-stu-id="480e2-173">Declare public methods on a hub so that clients can call them.</span></span>

* <span data-ttu-id="480e2-174">このハブに接続されているすべてのクライアントと通信するには、`Microsoft.AspNet.SignalR.Hub.Clients` 動的プロパティを使用します。</span><span class="sxs-lookup"><span data-stu-id="480e2-174">Use the `Microsoft.AspNet.SignalR.Hub.Clients` dynamic property to communicate with all clients connected to this hub.</span></span>

* <span data-ttu-id="480e2-175">クライアントの関数 (`addNewMessageToPage` 関数など) を呼び出して、クライアントを更新します。</span><span class="sxs-lookup"><span data-stu-id="480e2-175">Call a function on the client (like the `addNewMessageToPage` function) to update clients.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample5.cs)]

### <a name="signalr-and-jquery-chatcshtml"></a><span data-ttu-id="480e2-176">SignalR と jQuery Chat. cshtml</span><span class="sxs-lookup"><span data-stu-id="480e2-176">SignalR and jQuery Chat.cshtml</span></span>

<span data-ttu-id="480e2-177">コードサンプルの*Chat. cshtml*ビューファイルは、SignalR jQuery ライブラリを使用して SignalR hub と通信する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="480e2-177">The *Chat.cshtml* view file in the code sample shows how to use the SignalR jQuery library to communicate with a SignalR hub.</span></span>  <span data-ttu-id="480e2-178">このコードでは、多くの重要なタスクが実行されています。</span><span class="sxs-lookup"><span data-stu-id="480e2-178">The code carries out many important tasks.</span></span> <span data-ttu-id="480e2-179">ハブ用に自動生成されたプロキシへの参照を作成し、サーバーがクライアントにコンテンツをプッシュするために呼び出すことができる関数を宣言して、ハブにメッセージを送信するための接続を開始します。</span><span class="sxs-lookup"><span data-stu-id="480e2-179">It creates a reference to the autogenerated proxy for the hub, declares a function that the server can call to push content to clients, and it starts a connection to send messages to the hub.</span></span>

[!code-javascript[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample6.js)]

> [!NOTE]
> <span data-ttu-id="480e2-180">JavaScript では、サーバークラスとそのメンバーへの参照はキャメルケースにあります。</span><span class="sxs-lookup"><span data-stu-id="480e2-180">In JavaScript, the reference to the server class and its members is in camelCase.</span></span> <span data-ttu-id="480e2-181">このコードサンプルではC# 、`chatHub`として JavaScript の `ChatHub` クラスを参照しています。</span><span class="sxs-lookup"><span data-stu-id="480e2-181">The code sample references the C# `ChatHub` class in JavaScript as `chatHub`.</span></span>

<span data-ttu-id="480e2-182">このコードブロックでは、スクリプトでコールバック関数を作成します。</span><span class="sxs-lookup"><span data-stu-id="480e2-182">In this code block, you create a callback function in the script.</span></span>

[!code-html[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample7.html)]

<span data-ttu-id="480e2-183">サーバー上のハブクラスは、この関数を呼び出して、コンテンツの更新を各クライアントにプッシュします。</span><span class="sxs-lookup"><span data-stu-id="480e2-183">The hub class on the server calls this function to push content updates to each client.</span></span> <span data-ttu-id="480e2-184">`htmlEncode` 関数の省略可能な呼び出しは、メッセージをページに表示する前に HTML エンコードする方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="480e2-184">The optional call to the `htmlEncode` function shows a way to HTML encode the message content before displaying it in the page.</span></span> <span data-ttu-id="480e2-185">スクリプトインジェクションを防ぐ方法です。</span><span class="sxs-lookup"><span data-stu-id="480e2-185">It's a way to prevent script injection.</span></span>

<span data-ttu-id="480e2-186">このコードは、ハブとの接続を開きます。</span><span class="sxs-lookup"><span data-stu-id="480e2-186">This code opens a connection with the hub.</span></span>

[!code-javascript[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample8.js)]

> [!NOTE]
> <span data-ttu-id="480e2-187">この方法により、イベントハンドラーが実行される前に接続が確立されます。</span><span class="sxs-lookup"><span data-stu-id="480e2-187">This approach ensures that you establish a connection before the event handler executes.</span></span>

<span data-ttu-id="480e2-188">このコードは接続を開始し、チャットページの **[送信]** ボタンでクリックイベントを処理する関数を渡します。</span><span class="sxs-lookup"><span data-stu-id="480e2-188">The code starts the connection and then passes it a function to handle the click event on the **Send** button in the Chat page.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="480e2-189">コードの入手</span><span class="sxs-lookup"><span data-stu-id="480e2-189">Get the code</span></span>

[<span data-ttu-id="480e2-190">完成したプロジェクトのダウンロード</span><span class="sxs-lookup"><span data-stu-id="480e2-190">Download Completed Project</span></span>](https://code.msdn.microsoft.com/Getting-Started-with-c366b2f3)

## <a name="additional-resources"></a><span data-ttu-id="480e2-191">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="480e2-191">Additional resources</span></span>

<span data-ttu-id="480e2-192">SignalR の詳細については、次のリソースを参照してください。</span><span class="sxs-lookup"><span data-stu-id="480e2-192">For more about SignalR, see the following resources:</span></span>

* [<span data-ttu-id="480e2-193">SignalR プロジェクト</span><span class="sxs-lookup"><span data-stu-id="480e2-193">SignalR Project</span></span>](http://signalr.net)

* [<span data-ttu-id="480e2-194">SignalR GitHub とサンプル</span><span class="sxs-lookup"><span data-stu-id="480e2-194">SignalR GitHub and Samples</span></span>](https://github.com/SignalR/SignalR)

* [<span data-ttu-id="480e2-195">SignalR Wiki</span><span class="sxs-lookup"><span data-stu-id="480e2-195">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a><span data-ttu-id="480e2-196">次のステップ</span><span class="sxs-lookup"><span data-stu-id="480e2-196">Next steps</span></span>

<span data-ttu-id="480e2-197">このチュートリアルでは、次のことを行いました。</span><span class="sxs-lookup"><span data-stu-id="480e2-197">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="480e2-198">プロジェクトのセットアップ</span><span class="sxs-lookup"><span data-stu-id="480e2-198">Set up the project</span></span>
> * <span data-ttu-id="480e2-199">サンプルを実行しました</span><span class="sxs-lookup"><span data-stu-id="480e2-199">Ran the sample</span></span>
> * <span data-ttu-id="480e2-200">コードを調べる</span><span class="sxs-lookup"><span data-stu-id="480e2-200">Examined the code</span></span>

<span data-ttu-id="480e2-201">次の記事に進み、ASP.NET SignalR 2 を使用して高頻度のメッセージング機能を提供する web アプリケーションを作成する方法を学習してください。</span><span class="sxs-lookup"><span data-stu-id="480e2-201">Advance to the next article to learn how to create a web application that uses ASP.NET SignalR 2 to provide high-frequency messaging functionality.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="480e2-202">高頻度のメッセージングを使用した Web アプリ</span><span class="sxs-lookup"><span data-stu-id="480e2-202">Web app with high-frequency messaging</span></span>](tutorial-high-frequency-realtime-with-signalr.md)