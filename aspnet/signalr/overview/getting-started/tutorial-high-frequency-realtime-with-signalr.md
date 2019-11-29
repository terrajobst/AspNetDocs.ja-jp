---
uid: signalr/overview/getting-started/tutorial-high-frequency-realtime-with-signalr
title: 'チュートリアル: SignalR 2 | を使用した高頻度のリアルタイムアプリの作成Microsoft Docs'
author: bradygaster
description: このチュートリアルでは、ASP.NET SignalR を使用して高頻度のメッセージング機能を提供する web アプリケーションを作成する方法について説明します。
ms.author: bradyg
ms.date: 01/22/2019
ms.assetid: 9f969dda-78ea-4329-b1e3-e51c02210a2b
msc.legacyurl: /signalr/overview/getting-started/tutorial-high-frequency-realtime-with-signalr
msc.type: authoredcontent
ms.topic: tutorial
ms.openlocfilehash: 2503e90735d6cfa445ee08c9e43f8443aa106096
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600454"
---
# <a name="tutorial-create-high-frequency-real-time-app-with-signalr-2"></a><span data-ttu-id="20d76-103">チュートリアル: SignalR 2 を使用した高頻度のリアルタイムアプリの作成</span><span class="sxs-lookup"><span data-stu-id="20d76-103">Tutorial: Create high-frequency real-time app with SignalR 2</span></span>

<span data-ttu-id="20d76-104">このチュートリアルでは、ASP.NET SignalR 2 を使用して高頻度のメッセージング機能を提供する web アプリケーションを作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="20d76-104">This tutorial shows how to create a web application that uses ASP.NET SignalR 2 to provide high-frequency messaging functionality.</span></span> <span data-ttu-id="20d76-105">この場合、"高頻度のメッセージング" とは、サーバーが更新を一定の速度で送信することを意味します。</span><span class="sxs-lookup"><span data-stu-id="20d76-105">In this case, "high-frequency messaging" means the server sends updates at a fixed rate.</span></span> <span data-ttu-id="20d76-106">1秒あたり最大10個のメッセージを送信します。</span><span class="sxs-lookup"><span data-stu-id="20d76-106">You send up to 10 messages a second.</span></span>

<span data-ttu-id="20d76-107">作成したアプリケーションには、ユーザーがドラッグできる図形が表示されます。</span><span class="sxs-lookup"><span data-stu-id="20d76-107">The application you create displays a shape that users can drag.</span></span> <span data-ttu-id="20d76-108">サーバーは、接続されているすべてのブラウザー内の図形の位置を更新し、時間指定の更新を使用して、ドラッグした図形の位置と一致します。</span><span class="sxs-lookup"><span data-stu-id="20d76-108">The server updates the position of the shape in all connected browsers to match the position of the dragged shape using timed updates.</span></span>

<span data-ttu-id="20d76-109">このチュートリアルで導入された概念には、リアルタイムゲームやその他のシミュレーションアプリケーションのアプリケーションがあります。</span><span class="sxs-lookup"><span data-stu-id="20d76-109">Concepts introduced in this tutorial have applications in real-time gaming and other simulation applications.</span></span>

<span data-ttu-id="20d76-110">このチュートリアルでは、次の作業を行いました。</span><span class="sxs-lookup"><span data-stu-id="20d76-110">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="20d76-111">プロジェクトを設定する</span><span class="sxs-lookup"><span data-stu-id="20d76-111">Set up the project</span></span>
> * <span data-ttu-id="20d76-112">基本アプリケーションを作成する</span><span class="sxs-lookup"><span data-stu-id="20d76-112">Create the base application</span></span>
> * <span data-ttu-id="20d76-113">アプリの起動時にハブにマップする</span><span class="sxs-lookup"><span data-stu-id="20d76-113">Map to the hub when app starts</span></span>
> * <span data-ttu-id="20d76-114">クライアントを追加する</span><span class="sxs-lookup"><span data-stu-id="20d76-114">Add the client</span></span>
> * <span data-ttu-id="20d76-115">アプリを実行する</span><span class="sxs-lookup"><span data-stu-id="20d76-115">Run the app</span></span>
> * <span data-ttu-id="20d76-116">クライアントループを追加する</span><span class="sxs-lookup"><span data-stu-id="20d76-116">Add the client loop</span></span>
> * <span data-ttu-id="20d76-117">サーバーループの追加</span><span class="sxs-lookup"><span data-stu-id="20d76-117">Add the server loop</span></span>
> * <span data-ttu-id="20d76-118">スムーズなアニメーションの追加</span><span class="sxs-lookup"><span data-stu-id="20d76-118">Add smooth animation</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

## <a name="prerequisites"></a><span data-ttu-id="20d76-119">必要条件</span><span class="sxs-lookup"><span data-stu-id="20d76-119">Prerequisites</span></span>

* <span data-ttu-id="20d76-120">**ASP.NET と web 開発**ワークロードを含む[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) 。</span><span class="sxs-lookup"><span data-stu-id="20d76-120">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) with the **ASP.NET and web development** workload.</span></span>

## <a name="set-up-the-project"></a><span data-ttu-id="20d76-121">プロジェクトを設定する</span><span class="sxs-lookup"><span data-stu-id="20d76-121">Set up the project</span></span>

<span data-ttu-id="20d76-122">このセクションでは、Visual Studio 2017 でプロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="20d76-122">In this section, you create the project in Visual Studio 2017.</span></span>

<span data-ttu-id="20d76-123">このセクションでは、Visual Studio 2017 を使用して空の ASP.NET Web アプリケーションを作成し、SignalR と jQuery のライブラリを追加する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="20d76-123">This section shows how to use Visual Studio 2017 to create an empty ASP.NET Web Application and add the SignalR and jQuery.UI libraries.</span></span>

1. <span data-ttu-id="20d76-124">Visual Studio で、ASP.NET Web アプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="20d76-124">In Visual Studio, create an ASP.NET Web Application.</span></span>

    ![Web の作成](tutorial-high-frequency-realtime-with-signalr/_static/image1.png)

1. <span data-ttu-id="20d76-126">**[New ASP.NET Web Application-MoveShapeDemo]** ウィンドウで、 **[Empty]** を選択したままにして、[ **OK]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="20d76-126">In the **New ASP.NET Web Application - MoveShapeDemo** window, leave **Empty** selected and select **OK**.</span></span>

1. <span data-ttu-id="20d76-127">**ソリューションエクスプローラー**で、プロジェクトを右クリックし、[ > **新しい項目**の**追加**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="20d76-127">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="20d76-128">**[新しい項目の追加-MoveShapeDemo]** で、[**インストールされている** > **Visual C#**  > **Web** > **SignalR** ] を選択し、 **[SignalR Hub クラス (v2)]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="20d76-128">In **Add New Item - MoveShapeDemo**, select **Installed** > **Visual C#** > **Web** > **SignalR**  and then select **SignalR Hub Class (v2)**.</span></span>

1. <span data-ttu-id="20d76-129">クラスに*MoveShapeHub*という名前を指定し、プロジェクトに追加します。</span><span class="sxs-lookup"><span data-stu-id="20d76-129">Name the class *MoveShapeHub* and add it to the project.</span></span>

    <span data-ttu-id="20d76-130">この手順では、 *MoveShapeHub.cs*クラスファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="20d76-130">This step creates the *MoveShapeHub.cs* class file.</span></span> <span data-ttu-id="20d76-131">同時に、SignalR をサポートする一連のスクリプトファイルとアセンブリ参照をプロジェクトに追加します。</span><span class="sxs-lookup"><span data-stu-id="20d76-131">Simultaneously, it adds  a set of script files and assembly references that support SignalR to the project.</span></span>

1. <span data-ttu-id="20d76-132">[**ツール** > **NuGet パッケージマネージャー** > **パッケージマネージャーコンソール**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="20d76-132">Select **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>

1. <span data-ttu-id="20d76-133">**パッケージマネージャーコンソール**で、次のコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="20d76-133">In **Package Manager Console**, run this command:</span></span>

    ```console
    Install-Package jQuery.UI.Combined
    ```

    <span data-ttu-id="20d76-134">コマンドを実行すると、jQuery UI ライブラリがインストールされます。</span><span class="sxs-lookup"><span data-stu-id="20d76-134">The command installs the jQuery UI library.</span></span> <span data-ttu-id="20d76-135">図形をアニメーション化するために使用します。</span><span class="sxs-lookup"><span data-stu-id="20d76-135">You use it to animate the shape.</span></span>

1. <span data-ttu-id="20d76-136">**ソリューションエクスプローラー**で、[スクリプト] ノードを展開します。</span><span class="sxs-lookup"><span data-stu-id="20d76-136">In **Solution Explorer**, expand the Scripts node.</span></span>

    ![スクリプトライブラリの参照](tutorial-high-frequency-realtime-with-signalr/_static/image2.png)

    <span data-ttu-id="20d76-138">JQuery、jQueryUI、SignalR のスクリプトライブラリは、プロジェクトに表示されます。</span><span class="sxs-lookup"><span data-stu-id="20d76-138">Script libraries for jQuery, jQueryUI, and SignalR are visible in the project.</span></span>

## <a name="create-the-base-application"></a><span data-ttu-id="20d76-139">基本アプリケーションを作成する</span><span class="sxs-lookup"><span data-stu-id="20d76-139">Create the base application</span></span>

<span data-ttu-id="20d76-140">このセクションでは、ブラウザーアプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="20d76-140">In this section, you create a browser application.</span></span> <span data-ttu-id="20d76-141">アプリは、各マウス移動イベントの発生時に、図形の場所をサーバーに送信します。</span><span class="sxs-lookup"><span data-stu-id="20d76-141">The app sends the location of the shape to the server during each mouse move event.</span></span> <span data-ttu-id="20d76-142">サーバーは、この情報を、接続されている他のすべてのクライアントにリアルタイムでブロードキャストします。</span><span class="sxs-lookup"><span data-stu-id="20d76-142">The server broadcasts this information to all other connected clients in real time.</span></span> <span data-ttu-id="20d76-143">このアプリケーションの詳細については、後のセクションで説明します。</span><span class="sxs-lookup"><span data-stu-id="20d76-143">You learn more about this application in later sections.</span></span>

1. <span data-ttu-id="20d76-144">*MoveShapeHub.cs*ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="20d76-144">Open the *MoveShapeHub.cs* file.</span></span>

1. <span data-ttu-id="20d76-145">*MoveShapeHub.cs*ファイル内のコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="20d76-145">Replace the code in the *MoveShapeHub.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample1.cs)]

1. <span data-ttu-id="20d76-146">ファイルを保存します。</span><span class="sxs-lookup"><span data-stu-id="20d76-146">Save the file.</span></span>

<span data-ttu-id="20d76-147">`MoveShapeHub` クラスは、SignalR hub の実装です。</span><span class="sxs-lookup"><span data-stu-id="20d76-147">The `MoveShapeHub` class is an implementation of a SignalR hub.</span></span> <span data-ttu-id="20d76-148">[SignalR でのはじめに](tutorial-getting-started-with-signalr.md)チュートリアルと同様、ハブにはクライアントが直接呼び出すメソッドがあります。</span><span class="sxs-lookup"><span data-stu-id="20d76-148">As in the [Getting Started with SignalR](tutorial-getting-started-with-signalr.md) tutorial, the hub has a method that the clients call directly.</span></span> <span data-ttu-id="20d76-149">この場合、クライアントは図形の新しい X 座標と Y 座標を使用してオブジェクトをサーバーに送信します。</span><span class="sxs-lookup"><span data-stu-id="20d76-149">In this case, the client sends an object with the new X and Y coordinates of the shape to the server.</span></span> <span data-ttu-id="20d76-150">これらの座標は、接続されている他のすべてのクライアントにブロードキャストされます。</span><span class="sxs-lookup"><span data-stu-id="20d76-150">Those coordinates get broadcasted to all other connected clients.</span></span> <span data-ttu-id="20d76-151">SignalR は、このオブジェクトを JSON を使用して自動的にシリアル化します。</span><span class="sxs-lookup"><span data-stu-id="20d76-151">SignalR automatically serializes this object using JSON.</span></span>

<span data-ttu-id="20d76-152">アプリは `ShapeModel` オブジェクトをクライアントに送信します。</span><span class="sxs-lookup"><span data-stu-id="20d76-152">The app sends the `ShapeModel` object to the client.</span></span> <span data-ttu-id="20d76-153">図形の位置を格納するメンバーがあります。</span><span class="sxs-lookup"><span data-stu-id="20d76-153">It has members to store the position of the shape.</span></span> <span data-ttu-id="20d76-154">サーバー上のオブジェクトのバージョンには、どのクライアントのデータが格納されているかを追跡するメンバーもあります。</span><span class="sxs-lookup"><span data-stu-id="20d76-154">The version of the object on the server also has a member to track which client's data is being stored.</span></span> <span data-ttu-id="20d76-155">このオブジェクトは、サーバーがクライアントのデータをそれ自体に送信しないようにします。</span><span class="sxs-lookup"><span data-stu-id="20d76-155">This object prevents the server from sending a client's data back to itself.</span></span> <span data-ttu-id="20d76-156">このメンバーは、`JsonIgnore` 属性を使用して、アプリケーションがデータをシリアル化してクライアントに送り返すことを防止します。</span><span class="sxs-lookup"><span data-stu-id="20d76-156">This member uses the `JsonIgnore` attribute to keep the application from serializing the data and sending it back to the client.</span></span>

## <a name="map-to-the-hub-when-app-starts"></a><span data-ttu-id="20d76-157">アプリの起動時にハブにマップする</span><span class="sxs-lookup"><span data-stu-id="20d76-157">Map to the hub when app starts</span></span>

<span data-ttu-id="20d76-158">次に、アプリケーションの起動時に、ハブへのマッピングを設定します。</span><span class="sxs-lookup"><span data-stu-id="20d76-158">Next, you set up mapping to the hub when the application starts.</span></span> <span data-ttu-id="20d76-159">SignalR 2 では、OWIN startup クラスを追加するとマッピングが作成されます。</span><span class="sxs-lookup"><span data-stu-id="20d76-159">In SignalR 2, adding an OWIN startup class creates the mapping.</span></span>

1. <span data-ttu-id="20d76-160">**ソリューションエクスプローラー**で、プロジェクトを右クリックし、[ > **新しい項目**の**追加**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="20d76-160">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="20d76-161">**[新しい項目の追加-MoveShapeDemo]** で、[**インストールされている** > **Visual C#**  > **Web** ] を選択し、 **[OWIN Startup Class]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="20d76-161">In **Add New Item - MoveShapeDemo** select **Installed** > **Visual C#** > **Web** and then select **OWIN Startup Class**.</span></span>

1. <span data-ttu-id="20d76-162">クラスに「 *Startup* 」という名前を指定し、[ **OK]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="20d76-162">Name the class *Startup* and select **OK**.</span></span>

1. <span data-ttu-id="20d76-163">*Startup.cs*ファイルの既定のコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="20d76-163">Replace the default code in the *Startup.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample2.cs)]

<span data-ttu-id="20d76-164">OWIN startup クラスは、アプリが `Configuration` メソッドを実行するときに `MapSignalR` を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="20d76-164">The OWIN startup class calls `MapSignalR` when the app executes the `Configuration` method.</span></span> <span data-ttu-id="20d76-165">このアプリは、`OwinStartup` assembly 属性を使用して OWIN のスタートアッププロセスにクラスを追加します。</span><span class="sxs-lookup"><span data-stu-id="20d76-165">The app adds the class to OWIN's startup process using the `OwinStartup` assembly attribute.</span></span>

## <a name="add-the-client"></a><span data-ttu-id="20d76-166">クライアントを追加する</span><span class="sxs-lookup"><span data-stu-id="20d76-166">Add the client</span></span>

<span data-ttu-id="20d76-167">クライアントの HTML ページを追加します。</span><span class="sxs-lookup"><span data-stu-id="20d76-167">Add the HTML page for the client.</span></span>

1. <span data-ttu-id="20d76-168">**ソリューションエクスプローラー**で、プロジェクトを右クリックし、[ > **HTML ページ**の**追加**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="20d76-168">In **Solution Explorer**, right-click the project and select **Add** > **HTML Page**.</span></span>

1. <span data-ttu-id="20d76-169">ページの**既定**の名前を指定し、[ **OK]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="20d76-169">Name the page **Default** and select **OK**.</span></span>

1. <span data-ttu-id="20d76-170">**ソリューションエクスプローラー**で、[ *Default .html* ] を右クリックし、 **[スタートページとして設定]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="20d76-170">In **Solution Explorer**, right-click *Default.html* and select **Set as Start Page**.</span></span>

1. <span data-ttu-id="20d76-171">*既定の .html*ファイルの既定のコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="20d76-171">Replace the default code in the *Default.html* file with this code:</span></span>

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample3.html?highlight=14-16)]

1. <span data-ttu-id="20d76-172">**ソリューションエクスプローラー**で、 **[スクリプト]** を展開します。</span><span class="sxs-lookup"><span data-stu-id="20d76-172">In **Solution Explorer**, expand **Scripts**.</span></span>

    <span data-ttu-id="20d76-173">JQuery と SignalR のスクリプトライブラリは、プロジェクトに表示されます。</span><span class="sxs-lookup"><span data-stu-id="20d76-173">Script libraries for jQuery and SignalR are visible in the project.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="20d76-174">パッケージマネージャーでは、SignalR スクリプトの新しいバージョンがインストールされます。</span><span class="sxs-lookup"><span data-stu-id="20d76-174">The package manager installs a later version of the SignalR scripts.</span></span>

1. <span data-ttu-id="20d76-175">コードブロック内のスクリプト参照を、プロジェクト内のスクリプトファイルのバージョンに対応するように更新します。</span><span class="sxs-lookup"><span data-stu-id="20d76-175">Update the script references in the code block to correspond to the versions of the script files in the project.</span></span>

<span data-ttu-id="20d76-176">この HTML および JavaScript コードでは、`shape`と呼ばれる赤色の `div` が作成されます。</span><span class="sxs-lookup"><span data-stu-id="20d76-176">This HTML and JavaScript code creates a red `div` called `shape`.</span></span> <span data-ttu-id="20d76-177">JQuery ライブラリを使用して図形のドラッグ動作を有効にし、`drag` イベントを使用して、図形の位置をサーバーに送信します。</span><span class="sxs-lookup"><span data-stu-id="20d76-177">It enables the shape's dragging behavior using the jQuery library and uses the `drag` event to send the shape's position to the server.</span></span>

## <a name="run-the-app"></a><span data-ttu-id="20d76-178">アプリを実行する</span><span class="sxs-lookup"><span data-stu-id="20d76-178">Run the app</span></span>

<span data-ttu-id="20d76-179">アプリを実行して、作業することができます。</span><span class="sxs-lookup"><span data-stu-id="20d76-179">You can run the app to se\`e it work.</span></span> <span data-ttu-id="20d76-180">図形をブラウザーウィンドウの周りにドラッグすると、他のブラウザーでも図形は移動します。</span><span class="sxs-lookup"><span data-stu-id="20d76-180">When you drag the shape around a browser window, the shape moves in the other browsers too.</span></span>

1. <span data-ttu-id="20d76-181">ツールバーの **スクリプトデバッグ** をオンにし、再生 ボタンを選択して、アプリケーションをデバッグモードで実行します。</span><span class="sxs-lookup"><span data-stu-id="20d76-181">In the toolbar, turn on **Script Debugging** and then select the play button to run the application in Debug mode.</span></span>

    ![デバッグモードをオンにして [再生] を選択したユーザーのスクリーンショット。](tutorial-high-frequency-realtime-with-signalr/_static/image3.png)

    <span data-ttu-id="20d76-183">ブラウザーウィンドウが開き、右上隅に赤色の図形が表示されます。</span><span class="sxs-lookup"><span data-stu-id="20d76-183">A browser window opens with the red shape in the upper-right corner.</span></span>

1. <span data-ttu-id="20d76-184">ページの URL をコピーします。</span><span class="sxs-lookup"><span data-stu-id="20d76-184">Copy the page's URL.</span></span>

1. <span data-ttu-id="20d76-185">別のブラウザーを開き、アドレスバーに URL を貼り付けます。</span><span class="sxs-lookup"><span data-stu-id="20d76-185">Open another browser and paste the URL into the address bar.</span></span>

1. <span data-ttu-id="20d76-186">いずれかのブラウザーウィンドウで図形をドラッグします。</span><span class="sxs-lookup"><span data-stu-id="20d76-186">Drag the shape in one of the browser windows.</span></span> <span data-ttu-id="20d76-187">他のブラウザーウィンドウの図形は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="20d76-187">The shape in the other browser window follows.</span></span>

<span data-ttu-id="20d76-188">アプリケーションはこのメソッドを使用して機能しますが、推奨されるプログラミングモデルではありません。</span><span class="sxs-lookup"><span data-stu-id="20d76-188">While the application functions using this method, it's not a recommended programming model.</span></span> <span data-ttu-id="20d76-189">送信されるメッセージの数に上限はありません。</span><span class="sxs-lookup"><span data-stu-id="20d76-189">There's no upper limit to the number of messages getting sent.</span></span> <span data-ttu-id="20d76-190">その結果、クライアントとサーバーはメッセージを処理できないため、パフォーマンスが低下します。</span><span class="sxs-lookup"><span data-stu-id="20d76-190">As a result, the clients and server get overwhelmed with messages and performance degrades.</span></span> <span data-ttu-id="20d76-191">また、アプリによって、クライアントに不整合なアニメーションが表示されます。</span><span class="sxs-lookup"><span data-stu-id="20d76-191">Also, the app displays a disjointed animation on the client.</span></span> <span data-ttu-id="20d76-192">この不自然なアニメーションは、図形が各メソッドによって瞬時に移動するために発生します。</span><span class="sxs-lookup"><span data-stu-id="20d76-192">This jerky animation happens because the shape moves instantly by each method.</span></span> <span data-ttu-id="20d76-193">図形を新しい場所に滑らかに移動させる方が適切です。</span><span class="sxs-lookup"><span data-stu-id="20d76-193">It's better if the shape moves smoothly to each new location.</span></span> <span data-ttu-id="20d76-194">次に、これらの問題を解決する方法を学習します。</span><span class="sxs-lookup"><span data-stu-id="20d76-194">Next, you learn how to fix those issues.</span></span>

## <a name="add-the-client-loop"></a><span data-ttu-id="20d76-195">クライアントループを追加する</span><span class="sxs-lookup"><span data-stu-id="20d76-195">Add the client loop</span></span>

<span data-ttu-id="20d76-196">マウスの移動イベントごとに図形の場所を送信すると、不必要な量のネットワークトラフィックが発生します。</span><span class="sxs-lookup"><span data-stu-id="20d76-196">Sending the location of the shape on every mouse move event creates an unnecessary amount of network traffic.</span></span> <span data-ttu-id="20d76-197">アプリでは、クライアントからのメッセージを調整する必要があります。</span><span class="sxs-lookup"><span data-stu-id="20d76-197">The app needs to throttle the messages from the client.</span></span>

<span data-ttu-id="20d76-198">Javascript `setInterval` 関数を使用して、固定レートでサーバーに新しい位置情報を送信するループを設定します。</span><span class="sxs-lookup"><span data-stu-id="20d76-198">Use the javascript `setInterval` function to set up a loop that sends new position information to the server at a fixed rate.</span></span> <span data-ttu-id="20d76-199">このループは、"ゲームループ" の基本的な表現です。</span><span class="sxs-lookup"><span data-stu-id="20d76-199">This loop is a basic representation of a "game loop."</span></span> <span data-ttu-id="20d76-200">これは、ゲームのすべての機能を駆動する、繰り返し呼び出される関数です。</span><span class="sxs-lookup"><span data-stu-id="20d76-200">It's a repeatedly called function that drives all the functionality of a game.</span></span>

1. <span data-ttu-id="20d76-201">*既定の .html*ファイルのクライアントコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="20d76-201">Replace the client code in the *Default.html* file with this code:</span></span>

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample4.html?highlight=14-16)]

    > [!IMPORTANT]
    > <span data-ttu-id="20d76-202">スクリプト参照を再置換する必要があります。</span><span class="sxs-lookup"><span data-stu-id="20d76-202">You have to replace the script references again.</span></span> <span data-ttu-id="20d76-203">プロジェクト内のスクリプトのバージョンと一致している必要があります。</span><span class="sxs-lookup"><span data-stu-id="20d76-203">They must match the versions of the scripts in the project.</span></span>

    <span data-ttu-id="20d76-204">この新しいコードでは、`updateServerModel` 関数を追加します。</span><span class="sxs-lookup"><span data-stu-id="20d76-204">This new code adds the `updateServerModel` function.</span></span> <span data-ttu-id="20d76-205">固定頻度で呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="20d76-205">It gets called on a fixed frequency.</span></span> <span data-ttu-id="20d76-206">関数は、`moved` フラグによって、送信する新しい位置データがあることが示されたときに、その位置データをサーバーに送信します。</span><span class="sxs-lookup"><span data-stu-id="20d76-206">The function sends the position data to the server whenever the `moved` flag indicates that there's new position data to send.</span></span>

1. <span data-ttu-id="20d76-207">[再生] ボタンを選択してアプリケーションを起動します</span><span class="sxs-lookup"><span data-stu-id="20d76-207">Select the play button to start the application</span></span>

1. <span data-ttu-id="20d76-208">ページの URL をコピーします。</span><span class="sxs-lookup"><span data-stu-id="20d76-208">Copy the page's URL.</span></span>

1. <span data-ttu-id="20d76-209">別のブラウザーを開き、アドレスバーに URL を貼り付けます。</span><span class="sxs-lookup"><span data-stu-id="20d76-209">Open another browser and paste the URL into the address bar.</span></span>

1. <span data-ttu-id="20d76-210">いずれかのブラウザーウィンドウで図形をドラッグします。</span><span class="sxs-lookup"><span data-stu-id="20d76-210">Drag the shape in one of the browser windows.</span></span> <span data-ttu-id="20d76-211">他のブラウザーウィンドウの図形は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="20d76-211">The shape in the other browser window follows.</span></span>

<span data-ttu-id="20d76-212">アプリはサーバーに送信されるメッセージの数を調整するため、アニメーションは最初に smooth did として表示されません。</span><span class="sxs-lookup"><span data-stu-id="20d76-212">Since the app throttles the number of messages that get sent to the server, the animation won't appear as smooth did at first.</span></span>

## <a name="add-the-server-loop"></a><span data-ttu-id="20d76-213">サーバーループの追加</span><span class="sxs-lookup"><span data-stu-id="20d76-213">Add the server loop</span></span>

<span data-ttu-id="20d76-214">現在のアプリケーションでは、サーバーからクライアントに送信されたメッセージは、受信した頻度で送信されます。</span><span class="sxs-lookup"><span data-stu-id="20d76-214">In the current application, messages sent from the server to the client go out as often as they're received.</span></span> <span data-ttu-id="20d76-215">クライアントに表示されるように、このネットワークトラフィックにも同様の問題があります。</span><span class="sxs-lookup"><span data-stu-id="20d76-215">This network traffic presents a similar problem as we see on the client.</span></span>

<span data-ttu-id="20d76-216">アプリは、必要以上に頻繁にメッセージを送信できます。</span><span class="sxs-lookup"><span data-stu-id="20d76-216">The app can send messages more often than they're needed.</span></span> <span data-ttu-id="20d76-217">その結果、接続があふれてしまう可能性があります。</span><span class="sxs-lookup"><span data-stu-id="20d76-217">The connection can become flooded as a result.</span></span> <span data-ttu-id="20d76-218">このセクションでは、送信メッセージの速度を調整するタイマーを追加するようにサーバーを更新する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="20d76-218">This section describes how to update the server to add a timer that throttles the rate of the outgoing messages.</span></span>

1. <span data-ttu-id="20d76-219">`MoveShapeHub.cs` の内容を次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="20d76-219">Replace the contents of `MoveShapeHub.cs` with this code:</span></span>

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample5.cs)]

1. <span data-ttu-id="20d76-220">[Play] \ (再生 \) ボタンを選択して、アプリケーションを開始します。</span><span class="sxs-lookup"><span data-stu-id="20d76-220">Select the play button to start the application.</span></span>

1. <span data-ttu-id="20d76-221">ページの URL をコピーします。</span><span class="sxs-lookup"><span data-stu-id="20d76-221">Copy the page's URL.</span></span>

1. <span data-ttu-id="20d76-222">別のブラウザーを開き、アドレスバーに URL を貼り付けます。</span><span class="sxs-lookup"><span data-stu-id="20d76-222">Open another browser and paste the URL into the address bar.</span></span>

1. <span data-ttu-id="20d76-223">いずれかのブラウザーウィンドウで図形をドラッグします。</span><span class="sxs-lookup"><span data-stu-id="20d76-223">Drag the shape in one of the browser windows.</span></span>

<span data-ttu-id="20d76-224">このコードは、クライアントを拡張して `Broadcaster` クラスを追加します。</span><span class="sxs-lookup"><span data-stu-id="20d76-224">This code expands the client to add the `Broadcaster` class.</span></span> <span data-ttu-id="20d76-225">新しいクラスは、.NET framework の `Timer` クラスを使用して、送信メッセージを調整します。</span><span class="sxs-lookup"><span data-stu-id="20d76-225">The new class throttles the outgoing messages using the `Timer` class from the .NET framework.</span></span>

<span data-ttu-id="20d76-226">ハブ自体が一時的なものであることを理解することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="20d76-226">It's good to learn that the hub itself is transitory.</span></span> <span data-ttu-id="20d76-227">これは、必要になるたびに作成されます。</span><span class="sxs-lookup"><span data-stu-id="20d76-227">It's created every time it's needed.</span></span> <span data-ttu-id="20d76-228">そのため、アプリはシングルトンとして `Broadcaster` を作成します。</span><span class="sxs-lookup"><span data-stu-id="20d76-228">So the app creates the `Broadcaster` as a singleton.</span></span> <span data-ttu-id="20d76-229">遅延初期化を使用して、必要になるまで `Broadcaster`の作成を延期します。</span><span class="sxs-lookup"><span data-stu-id="20d76-229">It uses lazy initialization to defer the `Broadcaster`'s creation until it's needed.</span></span> <span data-ttu-id="20d76-230">これにより、タイマーを開始する前に、アプリが最初のハブインスタンスを完全に作成することが保証されます。</span><span class="sxs-lookup"><span data-stu-id="20d76-230">That guarantees that the app creates the first hub instance completely before starting the timer.</span></span>

<span data-ttu-id="20d76-231">次に、クライアントの `UpdateShape` 関数の呼び出しが、ハブの `UpdateModel` メソッドから移動されます。</span><span class="sxs-lookup"><span data-stu-id="20d76-231">The call to the clients' `UpdateShape` function is then moved out of the hub's `UpdateModel` method.</span></span> <span data-ttu-id="20d76-232">アプリが受信メッセージを受信するたびに、すぐには呼び出されなくなりました。</span><span class="sxs-lookup"><span data-stu-id="20d76-232">It's no longer called immediately whenever the app receives incoming messages.</span></span> <span data-ttu-id="20d76-233">代わりに、アプリは1秒あたり25回の呼び出しでクライアントにメッセージを送信します。</span><span class="sxs-lookup"><span data-stu-id="20d76-233">Instead, the app sends the messages to the clients at a rate of 25 calls per second.</span></span> <span data-ttu-id="20d76-234">プロセスは、`Broadcaster` クラス内の `_broadcastLoop` タイマーによって管理されます。</span><span class="sxs-lookup"><span data-stu-id="20d76-234">The process is  managed by the `_broadcastLoop` timer from within the `Broadcaster` class.</span></span>

<span data-ttu-id="20d76-235">最後に、ハブからクライアントメソッドを直接呼び出すのではなく、`Broadcaster` クラスが現在のオペレーティング `_hubContext` ハブへの参照を取得する必要があります。</span><span class="sxs-lookup"><span data-stu-id="20d76-235">Lastly, instead of calling the client method from the hub directly, the `Broadcaster` class needs to get a reference to the currently operating `_hubContext` hub.</span></span> <span data-ttu-id="20d76-236">`GlobalHost`で参照を取得します。</span><span class="sxs-lookup"><span data-stu-id="20d76-236">It gets the reference with the `GlobalHost`.</span></span>

## <a name="add-smooth-animation"></a><span data-ttu-id="20d76-237">スムーズなアニメーションの追加</span><span class="sxs-lookup"><span data-stu-id="20d76-237">Add smooth animation</span></span>

<span data-ttu-id="20d76-238">アプリケーションはほぼ完成していますが、さらに改善することもできます。</span><span class="sxs-lookup"><span data-stu-id="20d76-238">The application is almost finished, but we could make one more improvement.</span></span> <span data-ttu-id="20d76-239">アプリは、サーバーメッセージに応答してクライアント上の図形を移動します。</span><span class="sxs-lookup"><span data-stu-id="20d76-239">The app moves the shape on the client in response to server messages.</span></span> <span data-ttu-id="20d76-240">図形の位置をサーバーによって指定された新しい場所に設定するのではなく、JQuery UI ライブラリの `animate` 関数を使用します。</span><span class="sxs-lookup"><span data-stu-id="20d76-240">Instead of setting the position of the shape to the new location given by the server, use the JQuery UI library's `animate` function.</span></span> <span data-ttu-id="20d76-241">現在と新しい位置の間で図形を滑らかに移動できます。</span><span class="sxs-lookup"><span data-stu-id="20d76-241">It can move the shape smoothly between its current and new position.</span></span>

1. <span data-ttu-id="20d76-242">*既定の .html*ファイルのクライアントの `updateShape` メソッドを、強調表示されているコードのように更新します。</span><span class="sxs-lookup"><span data-stu-id="20d76-242">Update the client's `updateShape` method in the *Default.html* file to look like the highlighted code:</span></span>

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample6.html?highlight=33-40)]

1. <span data-ttu-id="20d76-243">[Play] \ (再生 \) ボタンを選択して、アプリケーションを開始します。</span><span class="sxs-lookup"><span data-stu-id="20d76-243">Select the play button to start the application.</span></span>

1. <span data-ttu-id="20d76-244">ページの URL をコピーします。</span><span class="sxs-lookup"><span data-stu-id="20d76-244">Copy the page's URL.</span></span>

1. <span data-ttu-id="20d76-245">別のブラウザーを開き、アドレスバーに URL を貼り付けます。</span><span class="sxs-lookup"><span data-stu-id="20d76-245">Open another browser and paste the URL into the address bar.</span></span>

1. <span data-ttu-id="20d76-246">いずれかのブラウザーウィンドウで図形をドラッグします。</span><span class="sxs-lookup"><span data-stu-id="20d76-246">Drag the shape in one of the browser windows.</span></span>

<span data-ttu-id="20d76-247">他のウィンドウでの図形の動きは、不自然に見えます。</span><span class="sxs-lookup"><span data-stu-id="20d76-247">The movement of the shape in the other window appears less jerky.</span></span> <span data-ttu-id="20d76-248">アプリは、着信メッセージごとに1回設定するのではなく、時間の経過と共にその動きを補間します。</span><span class="sxs-lookup"><span data-stu-id="20d76-248">The app interpolates its movement over time rather than being set once per incoming message.</span></span>

<span data-ttu-id="20d76-249">このコードは、図形を古い位置から新しい位置に移動します。</span><span class="sxs-lookup"><span data-stu-id="20d76-249">This code moves the shape from the old location to the new one.</span></span> <span data-ttu-id="20d76-250">サーバーは、アニメーションの間隔の間に図形の位置を示します。</span><span class="sxs-lookup"><span data-stu-id="20d76-250">The server gives the position of the shape over the course of the animation interval.</span></span> <span data-ttu-id="20d76-251">この場合、これは100ミリ秒です。</span><span class="sxs-lookup"><span data-stu-id="20d76-251">In this case, that's 100 milliseconds.</span></span> <span data-ttu-id="20d76-252">新しいアニメーションが開始される前に、その図形で実行されていた前のアニメーションがアプリによってクリアされます。</span><span class="sxs-lookup"><span data-stu-id="20d76-252">The app clears any previous animation running on the shape before the new animation starts.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="20d76-253">コードを取得する</span><span class="sxs-lookup"><span data-stu-id="20d76-253">Get the code</span></span>

[<span data-ttu-id="20d76-254">完成したプロジェクトのダウンロード</span><span class="sxs-lookup"><span data-stu-id="20d76-254">Download Completed Project</span></span>](https://code.msdn.microsoft.com/SignalR-20-MoveShape-Demo-6285b83a)

## <a name="additional-resources"></a><span data-ttu-id="20d76-255">その他の技術情報</span><span class="sxs-lookup"><span data-stu-id="20d76-255">Additional resources</span></span>

<span data-ttu-id="20d76-256">ここで学習した通信パラダイムは、 [SignalR で作成された ShootR ゲーム](https://shootr.azurewebsites.net/)と同様に、オンラインゲームやその他のシミュレーションの開発に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="20d76-256">The communication paradigm you just learned about is useful for developing online games and other simulations, like [the ShootR game created with SignalR](https://shootr.azurewebsites.net/).</span></span>

<span data-ttu-id="20d76-257">SignalR の詳細については、次のリソースを参照してください。</span><span class="sxs-lookup"><span data-stu-id="20d76-257">For more about SignalR, see the following resources:</span></span>

* [<span data-ttu-id="20d76-258">SignalR プロジェクト</span><span class="sxs-lookup"><span data-stu-id="20d76-258">SignalR Project</span></span>](http://signalr.net)

* [<span data-ttu-id="20d76-259">SignalR GitHub とサンプル</span><span class="sxs-lookup"><span data-stu-id="20d76-259">SignalR GitHub and Samples</span></span>](https://github.com/SignalR/SignalR)

* [<span data-ttu-id="20d76-260">SignalR Wiki</span><span class="sxs-lookup"><span data-stu-id="20d76-260">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a><span data-ttu-id="20d76-261">次のステップ:</span><span class="sxs-lookup"><span data-stu-id="20d76-261">Next steps</span></span>

<span data-ttu-id="20d76-262">このチュートリアルでは、次の作業を行いました。</span><span class="sxs-lookup"><span data-stu-id="20d76-262">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="20d76-263">プロジェクトを設定する</span><span class="sxs-lookup"><span data-stu-id="20d76-263">Set up the project</span></span>
> * <span data-ttu-id="20d76-264">基本アプリケーションを作成しました</span><span class="sxs-lookup"><span data-stu-id="20d76-264">Created the base application</span></span>
> * <span data-ttu-id="20d76-265">アプリの起動時にハブにマップされます</span><span class="sxs-lookup"><span data-stu-id="20d76-265">Mapped to the hub when app starts</span></span>
> * <span data-ttu-id="20d76-266">クライアントを追加しました</span><span class="sxs-lookup"><span data-stu-id="20d76-266">Added the client</span></span>
> * <span data-ttu-id="20d76-267">アプリを実行しました</span><span class="sxs-lookup"><span data-stu-id="20d76-267">Ran the app</span></span>
> * <span data-ttu-id="20d76-268">クライアントループを追加しました</span><span class="sxs-lookup"><span data-stu-id="20d76-268">Added the client loop</span></span>
> * <span data-ttu-id="20d76-269">サーバーループを追加しました</span><span class="sxs-lookup"><span data-stu-id="20d76-269">Added the server loop</span></span>
> * <span data-ttu-id="20d76-270">スムーズなアニメーションの追加</span><span class="sxs-lookup"><span data-stu-id="20d76-270">Added smooth animation</span></span>

<span data-ttu-id="20d76-271">次の記事に進み、ASP.NET SignalR 2 を使用してサーバーブロードキャスト機能を提供する web アプリケーションを作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="20d76-271">Advance to the next article to learn how to create a web application that uses ASP.NET SignalR 2 to provide server broadcast functionality.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="20d76-272">SignalR 2 とサーバーブロードキャスト</span><span class="sxs-lookup"><span data-stu-id="20d76-272">SignalR 2 and server broadcasting</span></span>](tutorial-server-broadcast-with-signalr.md)