---
uid: signalr/overview/older-versions/tutorial-getting-started-with-signalr-and-mvc-4
title: 'チュートリアル: SignalR 1.x および MVC 4 でのはじめに |Microsoft Docs'
author: bradygaster
description: ASP.NET SignalR と ASP.NET MVC 4 を使用して、リアルタイムチャットアプリケーションを作成します。
ms.author: bradyg
ms.date: 03/29/2013
ms.assetid: eeef9f73-6de3-49f9-b50b-9af22108f2ce
msc.legacyurl: /signalr/overview/older-versions/tutorial-getting-started-with-signalr-and-mvc-4
msc.type: authoredcontent
ms.openlocfilehash: 9186915df6d5de6bc20dfc0adabc54056d2f3a8c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78468070"
---
# <a name="tutorial-getting-started-with-signalr-1x-and-mvc-4"></a><span data-ttu-id="64c8f-103">チュートリアル: SignalR 1.x および MVC 4 でのはじめに</span><span class="sxs-lookup"><span data-stu-id="64c8f-103">Tutorial: Getting Started with SignalR 1.x and MVC 4</span></span>

<span data-ttu-id="64c8f-104">([パトリック Fletcher](https://github.com/pfletcher)、 [Tim teebken](https://github.com/timlt) )</span><span class="sxs-lookup"><span data-stu-id="64c8f-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tim Teebken](https://github.com/timlt)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="64c8f-105">このチュートリアルでは、ASP.NET SignalR を使用してリアルタイムチャットアプリケーションを作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="64c8f-105">This tutorial shows how to use ASP.NET SignalR to create a real-time chat application.</span></span> <span data-ttu-id="64c8f-106">SignalR を MVC 4 アプリケーションに追加し、メッセージを送信して表示するためのチャットビューを作成します。</span><span class="sxs-lookup"><span data-stu-id="64c8f-106">You will add SignalR to an MVC 4 application and create a chat view to send and display messages.</span></span>

## <a name="overview"></a><span data-ttu-id="64c8f-107">概要</span><span class="sxs-lookup"><span data-stu-id="64c8f-107">Overview</span></span>

<span data-ttu-id="64c8f-108">このチュートリアルでは、ASP.NET SignalR と ASP.NET MVC 4 を使用したリアルタイムの web アプリケーション開発について説明します。</span><span class="sxs-lookup"><span data-stu-id="64c8f-108">This tutorial introduces you to real-time web application development with ASP.NET SignalR and ASP.NET MVC 4.</span></span> <span data-ttu-id="64c8f-109">このチュートリアルでは、 [SignalR はじめにチュートリアル](tutorial-getting-started-with-signalr.md)と同じチャットアプリケーションコードを使用しますが、インターネットテンプレートに基づいて MVC 4 アプリケーションに追加する方法についても説明します。</span><span class="sxs-lookup"><span data-stu-id="64c8f-109">The tutorial uses the same chat application code as the [SignalR Getting Started tutorial](tutorial-getting-started-with-signalr.md), but shows how to add it to an MVC 4 application based on the Internet template.</span></span>

<span data-ttu-id="64c8f-110">このトピックでは、次の SignalR 開発タスクについて説明します。</span><span class="sxs-lookup"><span data-stu-id="64c8f-110">In this topic you will learn the following SignalR development tasks:</span></span>

- <span data-ttu-id="64c8f-111">MVC 4 アプリケーションへの SignalR ライブラリの追加。</span><span class="sxs-lookup"><span data-stu-id="64c8f-111">Adding the SignalR library to an MVC 4 application.</span></span>
- <span data-ttu-id="64c8f-112">クライアントにコンテンツをプッシュするハブクラスを作成する。</span><span class="sxs-lookup"><span data-stu-id="64c8f-112">Creating a hub class to push content to clients.</span></span>
- <span data-ttu-id="64c8f-113">Web ページで SignalR jQuery ライブラリを使用して、メッセージを送信し、ハブから更新を表示します。</span><span class="sxs-lookup"><span data-stu-id="64c8f-113">Using the SignalR jQuery library in a web page to send messages and display updates from the hub.</span></span>

<span data-ttu-id="64c8f-114">次のスクリーンショットは、ブラウザーで実行されている、完了したチャットアプリケーションを示しています。</span><span class="sxs-lookup"><span data-stu-id="64c8f-114">The following screen shot shows the completed chat application running in a browser.</span></span>

![チャットインスタンス](tutorial-getting-started-with-signalr-and-mvc-4/_static/image2.png)

<span data-ttu-id="64c8f-116">各項</span><span class="sxs-lookup"><span data-stu-id="64c8f-116">Sections:</span></span>

- [<span data-ttu-id="64c8f-117">プロジェクトを設定する</span><span class="sxs-lookup"><span data-stu-id="64c8f-117">Set up the Project</span></span>](#setup)
- [<span data-ttu-id="64c8f-118">サンプルを実行する</span><span class="sxs-lookup"><span data-stu-id="64c8f-118">Run the Sample</span></span>](#run)
- [<span data-ttu-id="64c8f-119">コードを確認する</span><span class="sxs-lookup"><span data-stu-id="64c8f-119">Examine the Code</span></span>](#code)
- [<span data-ttu-id="64c8f-120">次の手順</span><span class="sxs-lookup"><span data-stu-id="64c8f-120">Next Steps</span></span>](#next)

<a id="setup"></a>

## <a name="set-up-the-project"></a><span data-ttu-id="64c8f-121">プロジェクトを設定する</span><span class="sxs-lookup"><span data-stu-id="64c8f-121">Set up the Project</span></span>

<span data-ttu-id="64c8f-122">前提条件:</span><span class="sxs-lookup"><span data-stu-id="64c8f-122">Prerequisites:</span></span>

- <span data-ttu-id="64c8f-123">Visual Studio 2010 SP1、Visual Studio 2012、または Visual Studio 2012 Express。</span><span class="sxs-lookup"><span data-stu-id="64c8f-123">Visual Studio 2010 SP1, Visual Studio 2012, or Visual Studio 2012 Express.</span></span> <span data-ttu-id="64c8f-124">Visual Studio がインストールされていない場合は、無料の Visual Studio 2012 Express 開発ツールを入手するには、「 [ASP.NET のダウンロード](https://www.asp.net/downloads)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="64c8f-124">If you do not have Visual Studio, see [ASP.NET Downloads](https://www.asp.net/downloads) to get the free Visual Studio 2012 Express Development Tool.</span></span>
- <span data-ttu-id="64c8f-125">Visual Studio 2010 の場合は、 [ASP.NET MVC 4](https://www.microsoft.com/download/details.aspx?id=30683)をインストールします。</span><span class="sxs-lookup"><span data-stu-id="64c8f-125">For Visual Studio 2010, install [ASP.NET MVC 4](https://www.microsoft.com/download/details.aspx?id=30683).</span></span>

<span data-ttu-id="64c8f-126">このセクションでは、ASP.NET MVC 4 アプリケーションを作成し、SignalR ライブラリを追加して、チャットアプリケーションを作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="64c8f-126">This section shows how to create an ASP.NET MVC 4 application, add the SignalR library, and create the chat application.</span></span>

1. 1. <span data-ttu-id="64c8f-127">Visual Studio で、ASP.NET MVC 4 アプリケーションを作成し、SignalRChat という名前を指定して、[OK] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="64c8f-127">In Visual Studio create an ASP.NET MVC 4 application, name it SignalRChat, and click OK.</span></span>

        > [!NOTE]
        > <span data-ttu-id="64c8f-128">VS 2010 では、Framework バージョン ドロップダウンコントロールで  **.NET Framework 4** を選択します。</span><span class="sxs-lookup"><span data-stu-id="64c8f-128">In VS 2010, select **.NET Framework 4** in the Framework version dropdown control.</span></span> <span data-ttu-id="64c8f-129">SignalR コードは .NET Framework バージョン4および4.5 で実行されます。</span><span class="sxs-lookup"><span data-stu-id="64c8f-129">SignalR code runs on .NET Framework versions 4 and 4.5.</span></span>

        ![Mvc web の作成](tutorial-getting-started-with-signalr-and-mvc-4/_static/image3.png)
      2. <span data-ttu-id="64c8f-131">[インターネットアプリケーション] テンプレートを選択し、[**単体テストプロジェクトを作成**する] オプションをオフにして、[OK] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="64c8f-131">Select the Internet Application template, clear the option to **Create a unit test project**, and click OK.</span></span>

         ![Mvc インターネットサイトの作成](tutorial-getting-started-with-signalr-and-mvc-4/_static/image4.png)
      3. <span data-ttu-id="64c8f-133">**[ツール > NuGet パッケージマネージャー > パッケージマネージャーコンソール]** を開き、次のコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="64c8f-133">Open the **Tools > NuGet Package Manager > Package Manager Console** and run the following command.</span></span> <span data-ttu-id="64c8f-134">この手順では、SignalR 機能を有効にするスクリプトファイルとアセンブリ参照のセットをプロジェクトに追加します。</span><span class="sxs-lookup"><span data-stu-id="64c8f-134">This step adds to the project a set of script files and assembly references that enable SignalR functionality.</span></span>

         `install-package Microsoft.AspNet.SignalR -Version 1.1.3`
      4. <span data-ttu-id="64c8f-135">**ソリューションエクスプローラー** Scripts フォルダーを展開します。</span><span class="sxs-lookup"><span data-stu-id="64c8f-135">In **Solution Explorer** expand the Scripts folder.</span></span> <span data-ttu-id="64c8f-136">SignalR のスクリプトライブラリがプロジェクトに追加されていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="64c8f-136">Note that script libraries for SignalR have been added to the project.</span></span>

         ![ライブラリ参照](tutorial-getting-started-with-signalr-and-mvc-4/_static/image6.png)
      5. <span data-ttu-id="64c8f-138">**ソリューションエクスプローラー**で、プロジェクトを右クリックし、[追加] を選択します。 **新しいフォルダーを作成**し、**ハブ**という名前の新しいフォルダーを追加します。</span><span class="sxs-lookup"><span data-stu-id="64c8f-138">In **Solution Explorer**, right-click the project, select **Add | New Folder**, and add a new folder named **Hubs**.</span></span>
      6. <span data-ttu-id="64c8f-139">**ハブ** フォルダーを右クリックし、追加 をクリックします。 **クラス**を作成し、 C# **ChatHub.cs**という名前の新しいクラスを作成します。</span><span class="sxs-lookup"><span data-stu-id="64c8f-139">Right-click the **Hubs** folder, click **Add | Class**, and create a new C# class named **ChatHub.cs**.</span></span> <span data-ttu-id="64c8f-140">このクラスは、すべてのクライアントにメッセージを送信する SignalR サーバーハブとして使用します。</span><span class="sxs-lookup"><span data-stu-id="64c8f-140">You will use this class as a SignalR server hub that sends messages to all clients.</span></span>

> [!NOTE]
> <span data-ttu-id="64c8f-141">Visual Studio 2012 を使用していて[ASP.NET and Web Tools 2012.2 更新プログラム](../../../visual-studio/overview/2012/aspnet-and-web-tools-20122-release-notes-rtw.md#_Installation)がインストールされている場合は、new SignalR item テンプレートを使用してハブクラスを作成できます。</span><span class="sxs-lookup"><span data-stu-id="64c8f-141">If you use Visual Studio 2012 and have installed the [ASP.NET and Web Tools 2012.2 update](../../../visual-studio/overview/2012/aspnet-and-web-tools-20122-release-notes-rtw.md#_Installation), you can use the new SignalR item template to create the hub class.</span></span> <span data-ttu-id="64c8f-142">これを行うには、**ハブ** フォルダーを右クリックし、追加 をクリックします。 **新しい項目** を選択し、**SignalR Hub クラス (v1)** を選択して、クラスに**ChatHub.cs**という名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="64c8f-142">To do that, right-click the **Hubs** folder, click **Add | New Item**, select **SignalR Hub Class (v1)**, and name the class **ChatHub.cs**.</span></span>

1. <span data-ttu-id="64c8f-143">**ChatHub**クラスのコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="64c8f-143">Replace the code in the **ChatHub** class with the following code.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample1.cs)]
2. <span data-ttu-id="64c8f-144">プロジェクトの**global.asax**ファイルを開き、`Application_Start` メソッドのコードの最初の行として `RouteTable.Routes.MapHubs();` メソッドの呼び出しを追加します。</span><span class="sxs-lookup"><span data-stu-id="64c8f-144">Open the **Global.asax** file for the project, and add a call to the method `RouteTable.Routes.MapHubs();` as the first line of code in the `Application_Start` method.</span></span> <span data-ttu-id="64c8f-145">このコードは、SignalR ハブの既定のルートを登録し、他のルートを登録する前に呼び出す必要があります。</span><span class="sxs-lookup"><span data-stu-id="64c8f-145">This code registers the default route for SignalR hubs and must be called before you register any other routes.</span></span> <span data-ttu-id="64c8f-146">完成した `Application_Start` メソッドは、次の例のようになります。</span><span class="sxs-lookup"><span data-stu-id="64c8f-146">The completed `Application_Start` method looks like the following example.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample2.cs)]
3. <span data-ttu-id="64c8f-147">**Controllers/HomeController**で見つかった `HomeController` クラスを編集し、次のメソッドをクラスに追加します。</span><span class="sxs-lookup"><span data-stu-id="64c8f-147">Edit the `HomeController` class found in **Controllers/HomeController.cs** and add the following method to the class.</span></span> <span data-ttu-id="64c8f-148">このメソッドは、後の手順で作成する**チャット**ビューを返します。</span><span class="sxs-lookup"><span data-stu-id="64c8f-148">This method returns the **Chat** view that you will create in a later step.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample3.cs)]
4. <span data-ttu-id="64c8f-149">先ほど作成した `Chat` メソッド内を右クリックし、 **[ビューの追加]** をクリックして新しいビューファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="64c8f-149">Right-click within the `Chat` method you just created, and click **Add View** to create a new view file.</span></span>
5. <span data-ttu-id="64c8f-150">**[ビューの追加]** ダイアログボックスで、**レイアウトまたはマスターページを使用**するためのチェックボックスがオンになっていることを確認し (他のチェックボックスをオフにします)、 **[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="64c8f-150">In the **Add View** dialog, make sure the check box is selected to **Use a layout or master page** (clear the other check boxes), and then click **Add**.</span></span>

    ![ビューを追加する](tutorial-getting-started-with-signalr-and-mvc-4/_static/image8.png)
6. <span data-ttu-id="64c8f-152">「 **Chat. cshtml**」という名前の新しいビューファイルを編集します。</span><span class="sxs-lookup"><span data-stu-id="64c8f-152">Edit the new view file named **Chat.cshtml**.</span></span> <span data-ttu-id="64c8f-153">&lt;h2&gt; タグの後に、次の &lt;div&gt; セクションと `@section scripts` コードブロックをページに貼り付けます。</span><span class="sxs-lookup"><span data-stu-id="64c8f-153">After the &lt;h2&gt; tag, paste the following &lt;div&gt; section and `@section scripts` code block into the page.</span></span> <span data-ttu-id="64c8f-154">このスクリプトは、ページがチャットメッセージを送信し、サーバーからメッセージを表示できるようにします。</span><span class="sxs-lookup"><span data-stu-id="64c8f-154">This script enables the page to send chat messages and display messages from the server.</span></span> <span data-ttu-id="64c8f-155">チャットビューの完全なコードは、次のコードブロックに表示されます。</span><span class="sxs-lookup"><span data-stu-id="64c8f-155">The complete code for the chat view appears in the following code block.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="64c8f-156">SignalR およびその他のスクリプトライブラリを Visual Studio プロジェクトに追加すると、パッケージマネージャーによって、このトピックに示されているバージョンよりも新しいバージョンのスクリプトがインストールされる場合があります。</span><span class="sxs-lookup"><span data-stu-id="64c8f-156">When you add SignalR and other script libraries to your Visual Studio project, the Package Manager might install versions of the scripts that are more recent than the versions shown in this topic.</span></span> <span data-ttu-id="64c8f-157">コード内のスクリプト参照が、プロジェクトにインストールされているスクリプトライブラリのバージョンと一致していることを確認します。</span><span class="sxs-lookup"><span data-stu-id="64c8f-157">Make sure that the script references in your code match the versions of the script libraries installed in your project.</span></span>

    [!code-cshtml[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample4.cshtml)]
7. <span data-ttu-id="64c8f-158">プロジェクトの**すべてを保存**します。</span><span class="sxs-lookup"><span data-stu-id="64c8f-158">**Save All** for the project.</span></span>

<a id="run"></a>

## <a name="run-the-sample"></a><span data-ttu-id="64c8f-159">サンプルを実行する</span><span class="sxs-lookup"><span data-stu-id="64c8f-159">Run the Sample</span></span>

1. <span data-ttu-id="64c8f-160">F5 キーを押して、プロジェクトをデバッグモードで実行します。</span><span class="sxs-lookup"><span data-stu-id="64c8f-160">Press F5 to run the project in debug mode.</span></span>
2. <span data-ttu-id="64c8f-161">ブラウザーのアドレスラインで、プロジェクトの既定のページの URL に **/home/chat**を追加します。</span><span class="sxs-lookup"><span data-stu-id="64c8f-161">In the browser address line, append **/home/chat** to the URL of the default page for the project.</span></span> <span data-ttu-id="64c8f-162">チャットページがブラウザーインスタンスに読み込まれ、ユーザー名の入力が求められます。</span><span class="sxs-lookup"><span data-stu-id="64c8f-162">The Chat page loads in a browser instance and prompts for a user name.</span></span>

    ![ユーザー名の入力](tutorial-getting-started-with-signalr-and-mvc-4/_static/image9.png)
3. <span data-ttu-id="64c8f-164">ユーザー名を入力します。</span><span class="sxs-lookup"><span data-stu-id="64c8f-164">Enter a user name.</span></span>
4. <span data-ttu-id="64c8f-165">ブラウザーのアドレス行から URL をコピーし、それを使用して2つ以上のブラウザーインスタンスを開きます。</span><span class="sxs-lookup"><span data-stu-id="64c8f-165">Copy the URL from the address line of the browser and use it to open two more browser instances.</span></span> <span data-ttu-id="64c8f-166">各ブラウザーインスタンスで、一意のユーザー名を入力します。</span><span class="sxs-lookup"><span data-stu-id="64c8f-166">In each browser instance, enter a unique user name.</span></span>
5. <span data-ttu-id="64c8f-167">各ブラウザーインスタンスで、コメントを追加し、 **[送信]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="64c8f-167">In each browser instance, add a comment and click **Send**.</span></span> <span data-ttu-id="64c8f-168">コメントは、すべてのブラウザーインスタンスに表示されます。</span><span class="sxs-lookup"><span data-stu-id="64c8f-168">The comments should display in all browser instances.</span></span>

    > [!NOTE]
    > <span data-ttu-id="64c8f-169">この単純なチャットアプリケーションでは、サーバー上のディスカッションコンテキストは維持されません。</span><span class="sxs-lookup"><span data-stu-id="64c8f-169">This simple chat application does not maintain the discussion context on the server.</span></span> <span data-ttu-id="64c8f-170">ハブは、現在のすべてのユーザーにコメントをブロードキャストします。</span><span class="sxs-lookup"><span data-stu-id="64c8f-170">The hub broadcasts comments to all current users.</span></span> <span data-ttu-id="64c8f-171">後でチャットに参加したユーザーには、参加したときから追加されたメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="64c8f-171">Users who join the chat later will see messages added from the time they join.</span></span>
6. <span data-ttu-id="64c8f-172">次のスクリーンショットは、ブラウザーで実行されているチャットアプリケーションを示しています。</span><span class="sxs-lookup"><span data-stu-id="64c8f-172">The following screen shot shows the chat application running in a browser.</span></span>

    ![チャットブラウザー](tutorial-getting-started-with-signalr-and-mvc-4/_static/image11.png)
7. <span data-ttu-id="64c8f-174">**ソリューションエクスプローラー**で、実行中のアプリケーションの **[スクリプトドキュメント]** ノードを調べます。</span><span class="sxs-lookup"><span data-stu-id="64c8f-174">In **Solution Explorer**, inspect the **Script Documents** node for the running application.</span></span> <span data-ttu-id="64c8f-175">ブラウザーとして Internet Explorer を使用している場合、このノードはデバッグモードで表示されます。</span><span class="sxs-lookup"><span data-stu-id="64c8f-175">This node is visible in debug mode if you are using Internet Explorer as your browser.</span></span> <span data-ttu-id="64c8f-176">SignalR ライブラリによって実行時に動的に生成される**ハブ**という名前のスクリプトファイルがあります。</span><span class="sxs-lookup"><span data-stu-id="64c8f-176">There is a script file named **hubs** that the SignalR library dynamically generates at runtime.</span></span> <span data-ttu-id="64c8f-177">このファイルは、jQuery スクリプトとサーバー側コード間の通信を管理します。</span><span class="sxs-lookup"><span data-stu-id="64c8f-177">This file manages the communication between jQuery script and server-side code.</span></span> <span data-ttu-id="64c8f-178">Internet Explorer 以外のブラウザーを使用する場合は、動的**ハブ**ファイルを直接参照してアクセスすることもできます (http://mywebsite/signalr/hubsなど)。</span><span class="sxs-lookup"><span data-stu-id="64c8f-178">If you use a browser other than Internet Explorer, you can also access the dynamic **hubs** file by browsing to it directly, for example http://mywebsite/signalr/hubs.</span></span>

    ![生成されたハブスクリプト](tutorial-getting-started-with-signalr-and-mvc-4/_static/image13.png)

<a id="code"></a>

## <a name="examine-the-code"></a><span data-ttu-id="64c8f-180">コードを確認する</span><span class="sxs-lookup"><span data-stu-id="64c8f-180">Examine the Code</span></span>

<span data-ttu-id="64c8f-181">SignalR chat アプリケーションでは、2つの基本的な SignalR 開発タスクを示しています。サーバー上の主要な調整オブジェクトとしてハブを作成し、SignalR jQuery ライブラリを使用してメッセージを送受信します。</span><span class="sxs-lookup"><span data-stu-id="64c8f-181">The SignalR chat application demonstrates two basic SignalR development tasks: creating a hub as the main coordination object on the server, and using the SignalR jQuery library to send and receive messages.</span></span>

### <a name="signalr-hubs"></a><span data-ttu-id="64c8f-182">SignalR Hubs</span><span class="sxs-lookup"><span data-stu-id="64c8f-182">SignalR Hubs</span></span>

<span data-ttu-id="64c8f-183">コードサンプルでは、 **ChatHub**クラスは**SignalR**クラスから派生しています。</span><span class="sxs-lookup"><span data-stu-id="64c8f-183">In the code sample the **ChatHub** class derives from the **Microsoft.AspNet.SignalR.Hub** class.</span></span> <span data-ttu-id="64c8f-184">**ハブ**クラスからの派生は、SignalR アプリケーションを構築するための便利な方法です。</span><span class="sxs-lookup"><span data-stu-id="64c8f-184">Deriving from the **Hub** class is a useful way to build a SignalR application.</span></span> <span data-ttu-id="64c8f-185">ハブクラスにパブリックメソッドを作成し、web ページの jQuery スクリプトからメソッドを呼び出すことによって、これらのメソッドにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="64c8f-185">You can create public methods on your hub class and then access those methods by calling them from jQuery scripts in a web page.</span></span>

<span data-ttu-id="64c8f-186">チャットコードでは、クライアントは**ChatHub**メソッドを呼び出して、新しいメッセージを送信します。</span><span class="sxs-lookup"><span data-stu-id="64c8f-186">In the chat code, clients call the **ChatHub.Send** method to send a new message.</span></span> <span data-ttu-id="64c8f-187">その後、ハブはすべてのクライアントにメッセージを送信します。これには、**すべての addNewMessageToPage**を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="64c8f-187">The hub in turn sends the message to all clients by calling **Clients.All.addNewMessageToPage**.</span></span>

<span data-ttu-id="64c8f-188">**Send**メソッドは、いくつかのハブの概念を示しています。</span><span class="sxs-lookup"><span data-stu-id="64c8f-188">The **Send** method demonstrates several hub concepts :</span></span>

- <span data-ttu-id="64c8f-189">クライアントがそれらを呼び出すことができるように、ハブでパブリックメソッドを宣言します。</span><span class="sxs-lookup"><span data-stu-id="64c8f-189">Declare public methods on a hub so that clients can call them.</span></span>
- <span data-ttu-id="64c8f-190">このハブに接続されているすべてのクライアントにアクセスするには、 **SignalR**プロパティを使用します。</span><span class="sxs-lookup"><span data-stu-id="64c8f-190">Use the **Microsoft.AspNet.SignalR.Hub.Clients** property to access all clients connected to this hub.</span></span>
- <span data-ttu-id="64c8f-191">クライアントの jQuery 関数 (`addNewMessageToPage` 関数など) を呼び出して、クライアントを更新します。</span><span class="sxs-lookup"><span data-stu-id="64c8f-191">Call a jQuery function on the client (such as the `addNewMessageToPage` function) to update clients.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample5.cs)]

### <a name="signalr-and-jquery"></a><span data-ttu-id="64c8f-192">SignalR と jQuery</span><span class="sxs-lookup"><span data-stu-id="64c8f-192">SignalR and jQuery</span></span>

<span data-ttu-id="64c8f-193">コードサンプルの**Chat. cshtml**ビューファイルは、SignalR jQuery ライブラリを使用して SignalR hub と通信する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="64c8f-193">The **Chat.cshtml** view file in the code sample shows how to use the SignalR jQuery library to communicate with a SignalR hub.</span></span> <span data-ttu-id="64c8f-194">コードの重要なタスクは、ハブに対して自動生成されたプロキシへの参照を作成し、サーバーがクライアントにコンテンツをプッシュするために呼び出すことができる関数を宣言し、メッセージをハブに送信するための接続を開始することです。</span><span class="sxs-lookup"><span data-stu-id="64c8f-194">The essential tasks in the code are creating a reference to the auto-generated proxy for the hub, declaring a function that the server can call to push content to clients, and starting a connection to send messages to the hub.</span></span>

<span data-ttu-id="64c8f-195">次のコードでは、ハブのプロキシを宣言しています。</span><span class="sxs-lookup"><span data-stu-id="64c8f-195">The following code declares a proxy for a hub.</span></span>

[!code-javascript[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample6.js)]

> [!NOTE]
> <span data-ttu-id="64c8f-196">JQuery では、サーバークラスとそのメンバーへの参照は camel 形式です。</span><span class="sxs-lookup"><span data-stu-id="64c8f-196">In jQuery the reference to the server class and its members is in camel case.</span></span> <span data-ttu-id="64c8f-197">このコードサンプルではC# 、jQuery の**ChatHub**クラスを**ChatHub**として参照しています。</span><span class="sxs-lookup"><span data-stu-id="64c8f-197">The code sample references the C# **ChatHub** class in jQuery as **chatHub**.</span></span> <span data-ttu-id="64c8f-198">でのC#ように、jQuery の `ChatHub` クラスを通常の Pascal 形式で参照する場合は、ChatHub.cs クラスファイルを編集します。</span><span class="sxs-lookup"><span data-stu-id="64c8f-198">If you want to reference the `ChatHub` class in jQuery with conventional Pascal casing as you would in C#, edit the ChatHub.cs class file.</span></span> <span data-ttu-id="64c8f-199">`Microsoft.AspNet.SignalR.Hubs` 名前空間を参照する `using` ステートメントを追加します。</span><span class="sxs-lookup"><span data-stu-id="64c8f-199">Add a `using` statement to reference the `Microsoft.AspNet.SignalR.Hubs` namespace.</span></span> <span data-ttu-id="64c8f-200">次に、`HubName` 属性を `ChatHub` クラス (`[HubName("ChatHub")]`など) に追加します。</span><span class="sxs-lookup"><span data-stu-id="64c8f-200">Then add the `HubName` attribute to the `ChatHub` class, for example `[HubName("ChatHub")]`.</span></span> <span data-ttu-id="64c8f-201">最後に、jQuery 参照を `ChatHub` クラスに更新します。</span><span class="sxs-lookup"><span data-stu-id="64c8f-201">Finally, update your jQuery reference to the `ChatHub` class.</span></span>

<span data-ttu-id="64c8f-202">次のコードは、スクリプトでコールバック関数を作成する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="64c8f-202">The following code shows how to create a callback function in the script.</span></span> <span data-ttu-id="64c8f-203">サーバー上のハブクラスは、この関数を呼び出して、コンテンツの更新を各クライアントにプッシュします。</span><span class="sxs-lookup"><span data-stu-id="64c8f-203">The hub class on the server calls this function to push content updates to each client.</span></span> <span data-ttu-id="64c8f-204">`htmlEncode` 関数の呼び出しは、スクリプトの挿入を防ぐ方法として、メッセージの内容をページに表示する前に HTML エンコードする方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="64c8f-204">The optional call to the `htmlEncode` function shows a way to HTML encode the message content before displaying it in the page, as a way to prevent script injection.</span></span>

[!code-html[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample7.html)]

<span data-ttu-id="64c8f-205">次のコードは、ハブとの接続を開く方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="64c8f-205">The following code shows how to open a connection with the hub.</span></span> <span data-ttu-id="64c8f-206">このコードは接続を開始し、チャットページの **[送信]** ボタンでクリックイベントを処理する関数を渡します。</span><span class="sxs-lookup"><span data-stu-id="64c8f-206">The code starts the connection and then passes it a function to handle the click event on the **Send** button in the Chat page.</span></span>

> [!NOTE]
> <span data-ttu-id="64c8f-207">この方法により、イベントハンドラーが実行される前に接続が確立されます。</span><span class="sxs-lookup"><span data-stu-id="64c8f-207">This approach ensures that the connection is established before the event handler executes.</span></span>

[!code-javascript[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample8.js)]

<a id="next"></a>

## <a name="next-steps"></a><span data-ttu-id="64c8f-208">次の手順</span><span class="sxs-lookup"><span data-stu-id="64c8f-208">Next Steps</span></span>

<span data-ttu-id="64c8f-209">SignalR は、リアルタイム web アプリケーションを構築するためのフレームワークであることを学習しました。</span><span class="sxs-lookup"><span data-stu-id="64c8f-209">You learned that SignalR is a framework for building real-time web applications.</span></span> <span data-ttu-id="64c8f-210">また、いくつかの SignalR 開発タスク (SignalR を ASP.NET アプリケーションに追加する方法、ハブクラスを作成する方法、ハブからメッセージを送受信する方法) についても学習しました。</span><span class="sxs-lookup"><span data-stu-id="64c8f-210">You also learned several SignalR development tasks: how to add SignalR to an ASP.NET application, how to create a hub class, and how to send and receive messages from the hub.</span></span>

<span data-ttu-id="64c8f-211">より高度な SignalR 開発の概念を学習するには、次のサイトで SignalR ソースコードとリソースを参照してください。</span><span class="sxs-lookup"><span data-stu-id="64c8f-211">To learn more advanced SignalR developments concepts, visit the following sites for SignalR source code and resources :</span></span>

- [<span data-ttu-id="64c8f-212">SignalR プロジェクト</span><span class="sxs-lookup"><span data-stu-id="64c8f-212">SignalR Project</span></span>](http://signalr.net)
- [<span data-ttu-id="64c8f-213">SignalR Github とサンプル</span><span class="sxs-lookup"><span data-stu-id="64c8f-213">SignalR Github and Samples</span></span>](https://github.com/SignalR/SignalR)
- [<span data-ttu-id="64c8f-214">SignalR Wiki</span><span class="sxs-lookup"><span data-stu-id="64c8f-214">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)
