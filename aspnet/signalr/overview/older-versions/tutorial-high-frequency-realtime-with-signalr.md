---
uid: signalr/overview/older-versions/tutorial-high-frequency-realtime-with-signalr
title: SignalR 1.x を使用した高頻度のリアルタイム |Microsoft Docs
author: bradygaster
description: このチュートリアルでは、ASP.NET SignalR を使用して高頻度のメッセージング機能を提供する web アプリケーションを作成する方法について説明します。 高頻度のメッセージング...
ms.author: bradyg
ms.date: 04/16/2013
ms.assetid: ad2a5da5-2e79-40ea-bc84-028d327f5982
msc.legacyurl: /signalr/overview/older-versions/tutorial-high-frequency-realtime-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: e37e63a410952ec170cbbaadeeb54eae7e82b3b5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78505714"
---
# <a name="high-frequency-realtime-with-signalr-1x"></a><span data-ttu-id="1c3ee-104">SignalR 1.x による高頻度リアルタイム</span><span class="sxs-lookup"><span data-stu-id="1c3ee-104">High-Frequency Realtime with SignalR 1.x</span></span>

<span data-ttu-id="1c3ee-105">([パトリック Fletcher](https://github.com/pfletcher) )</span><span class="sxs-lookup"><span data-stu-id="1c3ee-105">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="1c3ee-106">このチュートリアルでは、ASP.NET SignalR を使用して高頻度のメッセージング機能を提供する web アプリケーションを作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-106">This tutorial shows how to create a web application that uses ASP.NET SignalR to provide high-frequency messaging functionality.</span></span> <span data-ttu-id="1c3ee-107">この場合、高頻度のメッセージングでは、一定のレートで送信された更新を意味します。このアプリケーションの場合、1秒あたり最大10個のメッセージが送信されます。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-107">High-frequency messaging in this case means updates that are sent at a fixed rate; in the case of this application, up to 10 messages a second.</span></span>
> 
> <span data-ttu-id="1c3ee-108">このチュートリアルで作成するアプリケーションは、ユーザーがドラッグできる図形を表示します。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-108">The application you'll create in this tutorial displays a shape that users can drag.</span></span> <span data-ttu-id="1c3ee-109">その他のすべての接続されたブラウザーでの図形の位置は、時間指定の更新を使用して、ドラッグした図形の位置と一致するように更新されます。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-109">The position of the shape in all other connected browsers will then be updated to match the position of the dragged shape using timed updates.</span></span>
> 
> <span data-ttu-id="1c3ee-110">このチュートリアルで導入された概念には、リアルタイムゲームやその他のシミュレーションアプリケーションのアプリケーションがあります。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-110">Concepts introduced in this tutorial have applications in real-time gaming and other simulation applications.</span></span>
> 
> <span data-ttu-id="1c3ee-111">このチュートリアルのコメントは歓迎しています。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-111">Comments on the tutorial are welcome.</span></span> <span data-ttu-id="1c3ee-112">チュートリアルに直接関係のない質問がある場合は、 [ASP.NET SignalR フォーラム](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)または[StackOverflow.com](http://stackoverflow.com)に投稿できます。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-112">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com).</span></span>

## <a name="overview"></a><span data-ttu-id="1c3ee-113">概要</span><span class="sxs-lookup"><span data-stu-id="1c3ee-113">Overview</span></span>

<span data-ttu-id="1c3ee-114">このチュートリアルでは、リアルタイムで他のブラウザーとオブジェクトの状態を共有するアプリケーションを作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-114">This tutorial demonstrates how to create an application that shares the state of an object with other browsers in real time.</span></span> <span data-ttu-id="1c3ee-115">作成するアプリケーションは MoveShape と呼ばれます。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-115">The application we'll create is called MoveShape.</span></span> <span data-ttu-id="1c3ee-116">MoveShape ページには、ユーザーがドラッグできる HTML Div 要素が表示されます。ユーザーが Div をドラッグすると、その新しい位置がサーバーに送信されます。その後、接続されている他のすべてのクライアントに対して、一致するように図形の位置を更新するように指示します。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-116">The MoveShape page will display an HTML Div element that the user can drag; when the user drags the Div, its new position will be sent to the server, which will then tell all other connected clients to update the shape's position to match.</span></span>

![アプリケーションウィンドウ](tutorial-high-frequency-realtime-with-signalr/_static/image1.png)

<span data-ttu-id="1c3ee-118">このチュートリアルで作成するアプリケーションは、Damian Edwards のデモに基づいています。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-118">The application created in this tutorial is based on a demo by Damian Edwards.</span></span> <span data-ttu-id="1c3ee-119">このデモを含むビデオについては、[こちら](https://channel9.msdn.com/Series/Building-Web-Apps-with-ASP-NET-Jump-Start/Building-Web-Apps-with-ASPNET-Jump-Start-08-Real-time-Communication-with-SignalR)をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-119">A video containing this demo can be seen [here](https://channel9.msdn.com/Series/Building-Web-Apps-with-ASP-NET-Jump-Start/Building-Web-Apps-with-ASPNET-Jump-Start-08-Real-time-Communication-with-SignalR).</span></span>

<span data-ttu-id="1c3ee-120">このチュートリアルでは、最初に、図形のドラッグ時に発生する各イベントから SignalR メッセージを送信する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-120">The tutorial will start by demonstrating how to send SignalR messages from each event that fires as the shape is dragged.</span></span> <span data-ttu-id="1c3ee-121">接続された各クライアントは、メッセージを受信するたびに、図形のローカルバージョンの位置を更新します。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-121">Each connected client will then update the position of the local version of the shape each time a message is received.</span></span>

<span data-ttu-id="1c3ee-122">アプリケーションはこの方法を使用して機能しますが、送信されるメッセージの数に上限がないため、クライアントとサーバーがメッセージを大量に使用し、パフォーマンスが低下する可能性があるため、これは推奨されるプログラミングモデルではありません.</span><span class="sxs-lookup"><span data-stu-id="1c3ee-122">While the application will function using this method, this is not a recommended programming model, since there would be no upper limit to the number of messages getting sent, so the clients and server could get overwhelmed with messages and performance would degrade.</span></span> <span data-ttu-id="1c3ee-123">また、クライアントで表示されるアニメーションも不整合になります。これは、各メソッドによって図形が瞬時に移動されるのではなく、新しい場所に滑らかに移動するためです。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-123">The displayed animation on the client would also be disjointed, as the shape would be moved instantly by each method, rather than moving smoothly to each new location.</span></span> <span data-ttu-id="1c3ee-124">このチュートリアルの後のセクションでは、クライアントまたはサーバーによってメッセージが送信される最大速度を制限するタイマー関数を作成する方法と、図形を位置をスムーズに移動する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-124">Later sections of the tutorial will demonstrate how to create a timer function that restricts the maximum rate at which messages are sent by either the client or server, and how to move the shape smoothly between locations.</span></span> <span data-ttu-id="1c3ee-125">このチュートリアルで作成したアプリケーションの最終バージョンは、[コードギャラリー](https://code.msdn.microsoft.com/SignalR-MoveShape-demo-3366dac6)からダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-125">The final version of the application created in this tutorial can be downloaded from [Code Gallery](https://code.msdn.microsoft.com/SignalR-MoveShape-demo-3366dac6).</span></span>

<span data-ttu-id="1c3ee-126">このチュートリアルは、次のセクションで構成されています。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-126">This tutorial contains the following sections:</span></span>

- [<span data-ttu-id="1c3ee-127">前提条件</span><span class="sxs-lookup"><span data-stu-id="1c3ee-127">Prerequisites</span></span>](#prerequisites)
- [<span data-ttu-id="1c3ee-128">プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="1c3ee-128">Create the project</span></span>](#createtheproject)
- [<span data-ttu-id="1c3ee-129">ASP.NET SignalR と JQuery. UI NuGet パッケージを追加する</span><span class="sxs-lookup"><span data-stu-id="1c3ee-129">Add the ASP.NET SignalR and JQuery.UI NuGet packages</span></span>](#nugetpackages)
- [<span data-ttu-id="1c3ee-130">基本アプリケーションを作成する</span><span class="sxs-lookup"><span data-stu-id="1c3ee-130">Create the base application</span></span>](#baseapp)
- [<span data-ttu-id="1c3ee-131">クライアントループを追加する</span><span class="sxs-lookup"><span data-stu-id="1c3ee-131">Add the client loop</span></span>](#clientloop)
- [<span data-ttu-id="1c3ee-132">サーバーループの追加</span><span class="sxs-lookup"><span data-stu-id="1c3ee-132">Add the server loop</span></span>](#serverloop)
- [<span data-ttu-id="1c3ee-133">クライアントに smooth animation を追加する</span><span class="sxs-lookup"><span data-stu-id="1c3ee-133">Add smooth animation on the client</span></span>](#animation)
- [<span data-ttu-id="1c3ee-134">その他の手順</span><span class="sxs-lookup"><span data-stu-id="1c3ee-134">Further Steps</span></span>](#furthersteps)

<a id="prerequisites"></a>

## <a name="prerequisites"></a><span data-ttu-id="1c3ee-135">前提条件</span><span class="sxs-lookup"><span data-stu-id="1c3ee-135">Prerequisites</span></span>

<span data-ttu-id="1c3ee-136">このチュートリアルには、Visual Studio 2012 または Visual Studio 2010 が必要です。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-136">This tutorial requires Visual Studio 2012 or Visual Studio 2010.</span></span> <span data-ttu-id="1c3ee-137">Visual Studio 2010 が使用されている場合、プロジェクトは .NET Framework 4.5 ではなく .NET Framework 4 を使用します。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-137">If Visual Studio 2010 is used, the project will use .NET Framework 4 rather than .NET Framework 4.5.</span></span>

<span data-ttu-id="1c3ee-138">Visual Studio 2012 を使用している場合は、 [ASP.NET and Web Tools 2012.2 更新プログラム](https://go.microsoft.com/fwlink/?LinkId=282650)をインストールすることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-138">If you are using Visual Studio 2012, it's recommended that you install the [ASP.NET and Web Tools 2012.2 update](https://go.microsoft.com/fwlink/?LinkId=282650).</span></span> <span data-ttu-id="1c3ee-139">この更新プログラムには、公開、新機能、新しいテンプレートなどの新機能が追加されています。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-139">This update contains new features such as enhancements to publishing, new functionality, and new templates.</span></span>

<span data-ttu-id="1c3ee-140">Visual Studio 2010 を使用している場合は、 [NuGet](https://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c)がインストールされていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-140">If you have Visual Studio 2010, make sure that [NuGet](https://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c) is installed.</span></span>

<a id="createtheproject"></a>

## <a name="create-the-project"></a><span data-ttu-id="1c3ee-141">プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="1c3ee-141">Create the project</span></span>

<span data-ttu-id="1c3ee-142">このセクションでは、Visual Studio でプロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-142">In this section, we'll create the project in Visual Studio.</span></span>

1. <span data-ttu-id="1c3ee-143">**[ファイル]** メニューの **[新しいプロジェクト]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-143">From the **File** menu click **New Project**.</span></span>
2. <span data-ttu-id="1c3ee-144">**[新しいプロジェクト]** ダイアログボックスの [ **C#** **テンプレート**] で展開し、 **[Web]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-144">In the **New Project** dialog box, expand **C#** under **Templates** and select **Web**.</span></span>
3. <span data-ttu-id="1c3ee-145">**[ASP.NET 空の Web アプリケーション]** テンプレートを選択し、プロジェクトに*MoveShapeDemo*という名前を指定して、[ **OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-145">Select the **ASP.NET Empty Web Application** template, name the project *MoveShapeDemo*, and click **OK**.</span></span>

    ![新しいプロジェクトの作成](tutorial-high-frequency-realtime-with-signalr/_static/image2.png)

<a id="nugetpackages"></a>

## <a name="add-the-signalr-and-jqueryui-nuget-packages"></a><span data-ttu-id="1c3ee-147">SignalR および JQuery. UI NuGet パッケージを追加する</span><span class="sxs-lookup"><span data-stu-id="1c3ee-147">Add the SignalR and JQuery.UI NuGet Packages</span></span>

<span data-ttu-id="1c3ee-148">NuGet パッケージをインストールすることによって、SignalR 機能をプロジェクトに追加できます。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-148">You can add SignalR functionality to a project by installing a NuGet package.</span></span> <span data-ttu-id="1c3ee-149">また、このチュートリアルでは、図形をドラッグアンドアニメーション化できるようにするために、JQuery. UI パッケージも使用します。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-149">This tutorial will also use the JQuery.UI package for allowing the shape to be dragged and animated.</span></span>

1. <span data-ttu-id="1c3ee-150">[ツール] をクリックします。 **NuGet パッケージマネージャー |パッケージマネージャーコンソール**。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-150">Click **Tools | NuGet Package Manager | Package Manager Console**.</span></span>
2. <span data-ttu-id="1c3ee-151">パッケージマネージャーで、次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-151">Enter the following command in the package manager.</span></span>

    [!code-powershell[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample1.ps1)]

    <span data-ttu-id="1c3ee-152">SignalR パッケージは、他のいくつかの NuGet パッケージを依存関係としてインストールします。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-152">The SignalR package installs a number of other NuGet packages as dependencies.</span></span> <span data-ttu-id="1c3ee-153">インストールが完了すると、ASP.NET アプリケーションで SignalR を使用するために必要なすべてのサーバーおよびクライアントコンポーネントが作成されます。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-153">When the installation is finished you have all of the server and client components required to use SignalR in an ASP.NET application.</span></span>
3. <span data-ttu-id="1c3ee-154">次のコマンドをパッケージマネージャーコンソールに入力して、JQuery および JQuery. UI パッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-154">Enter the following command into the package manager console to install the JQuery and JQuery.UI packages.</span></span>

    [!code-powershell[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample2.ps1)]

<a id="baseapp"></a>

## <a name="create-the-base-application"></a><span data-ttu-id="1c3ee-155">基本アプリケーションを作成する</span><span class="sxs-lookup"><span data-stu-id="1c3ee-155">Create the base application</span></span>

<span data-ttu-id="1c3ee-156">このセクションでは、各マウス移動イベント時に図形の場所をサーバーに送信するブラウザーアプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-156">In this section, we'll create a browser application that sends the location of the shape to the server during each mouse move event.</span></span> <span data-ttu-id="1c3ee-157">その後、サーバーは、受信時に、他のすべての接続されたクライアントにこの情報をブロードキャストします。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-157">The server then broadcasts this information to all other connected clients as it is received.</span></span> <span data-ttu-id="1c3ee-158">このアプリケーションの拡張については、後のセクションで説明します。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-158">We'll expand on this application in later sections.</span></span>

1. <span data-ttu-id="1c3ee-159">**ソリューションエクスプローラー**で、プロジェクトを右クリックし、 **[追加]** 、 **[クラス.]** . の順に選択します。クラスに**MoveShapeHub**という名前を指定し、 **[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-159">In **Solution Explorer**, right-click on the project and select **Add**, **Class...**. Name the class **MoveShapeHub** and click **Add**.</span></span>
2. <span data-ttu-id="1c3ee-160">新しい**MoveShapeHub**クラスのコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-160">Replace the code in the new **MoveShapeHub** class with the following code.</span></span>

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample3.cs)]

    <span data-ttu-id="1c3ee-161">上の `MoveShapeHub` クラスは、SignalR hub の実装です。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-161">The `MoveShapeHub` class above is an implementation of a SignalR hub.</span></span> <span data-ttu-id="1c3ee-162">[SignalR でのはじめに](index.md)チュートリアルと同様、ハブにはクライアントが直接呼び出すメソッドがあります。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-162">As in the [Getting Started with SignalR](index.md) tutorial, the hub has a method that the clients will call directly.</span></span> <span data-ttu-id="1c3ee-163">この場合、クライアントは図形の新しい X 座標と Y 座標を含むオブジェクトをサーバーに送信し、その後、接続されている他のすべてのクライアントにブロードキャストされます。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-163">In this case, the client will send an object containing the new X and Y coordinates of the shape to the server, which then gets broadcasted to all other connected clients.</span></span> <span data-ttu-id="1c3ee-164">SignalR は、このオブジェクトを JSON を使用して自動的にシリアル化します。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-164">SignalR will automatically serialize this object using JSON.</span></span>

    <span data-ttu-id="1c3ee-165">クライアントに送信されるオブジェクト (`ShapeModel`) には、図形の位置を格納するためのメンバーが含まれています。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-165">The object that will be sent to the client (`ShapeModel`) contains members to store the position of the shape.</span></span> <span data-ttu-id="1c3ee-166">サーバー上のオブジェクトのバージョンには、特定のクライアントに独自のデータが送信されないように、格納されているクライアントのデータを追跡するためのメンバーも含まれています。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-166">The version of the object on the server also contains a member to track which client's data is being stored, so that a given client won't be sent their own data.</span></span> <span data-ttu-id="1c3ee-167">このメンバーは、`JsonIgnore` 属性を使用して、シリアル化とクライアントへの送信を維持します。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-167">This member uses the `JsonIgnore` attribute to keep it from being serialized and sent to the client.</span></span>
3. <span data-ttu-id="1c3ee-168">次に、アプリケーションの起動時にハブを設定します。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-168">Next, we'll set up the hub when the application starts.</span></span> <span data-ttu-id="1c3ee-169">**ソリューションエクスプローラー**で、プロジェクトを右クリックし、[追加] をクリックします。 **グローバルアプリケーションクラス**。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-169">In **Solution Explorer**, right-click the project, then click **Add | Global Application Class**.</span></span> <span data-ttu-id="1c3ee-170">*グローバル*の既定の名前をそのまま使用し、[ **OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-170">Accept the default name of *Global* and click **OK**.</span></span>

    ![グローバルアプリケーションクラスの追加](tutorial-high-frequency-realtime-with-signalr/_static/image3.png)
4. <span data-ttu-id="1c3ee-172">Global.asax.cs クラスの**using**ステートメントの後に、次の `using` ステートメントを追加します。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-172">Add the following `using` statement after the provided **using** statements in the Global.asax.cs class.</span></span>

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample4.cs)]
5. <span data-ttu-id="1c3ee-173">SignalR の既定のルートを登録するには、グローバルクラスの `Application_Start` メソッドに次のコード行を追加します。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-173">Add the following line of code in the `Application_Start` method of the Global class to register the default route for SignalR.</span></span>

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample5.cs)]

    <span data-ttu-id="1c3ee-174">Global.asax ファイルは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-174">Your global.asax file should look like the following:</span></span>

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample6.cs)]
6. <span data-ttu-id="1c3ee-175">次に、クライアントを追加します。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-175">Next, we'll add the client.</span></span> <span data-ttu-id="1c3ee-176">**ソリューションエクスプローラー**で、プロジェクトを右クリックし、[追加] をクリックします。 **新しい項目**。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-176">In **Solution Explorer**, right-click the project, then click **Add | New Item**.</span></span> <span data-ttu-id="1c3ee-177">**[新しい項目の追加]** ダイアログで、 **[Html ページ]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-177">In the **Add New Item** dialog, select **Html Page**.</span></span> <span data-ttu-id="1c3ee-178">ページに適切な名前 (既定の **.html**など) を付け、 **[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-178">Give the page an appropriate name (like **Default.html**) and click **Add**.</span></span>
7. <span data-ttu-id="1c3ee-179">**ソリューションエクスプローラー**で、作成したページを右クリックし、 **[スタートページとして設定]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-179">In **Solution Explorer**, right-click the page you just created and click **Set as Start Page**.</span></span>
8. <span data-ttu-id="1c3ee-180">HTML ページの既定のコードを次のコードスニペットに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-180">Replace the default code in the HTML page with the following code snippet.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1c3ee-181">以下のスクリプト参照が、Scripts フォルダー内のプロジェクトに追加されたパッケージと一致していることを確認します。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-181">Verify that the script references below match the packages added to your project in the Scripts folder.</span></span> <span data-ttu-id="1c3ee-182">Visual Studio 2010 では、プロジェクトに追加された JQuery と SignalR のバージョンが以下のバージョン番号と一致しない可能性があります。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-182">In Visual Studio 2010, the version of JQuery and SignalR added to the project may not match the version numbers below.</span></span>

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample7.html)]

    <span data-ttu-id="1c3ee-183">上記の HTML および JavaScript コードでは、Shape という名前の赤い Div を作成し、jQuery ライブラリを使用して図形のドラッグ動作を有効にし、図形の `drag` イベントを使用して、図形の位置をサーバーに送信します。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-183">The above HTML and JavaScript code creates a red Div called Shape, enables the shape's dragging behavior using the jQuery library, and uses the shape's `drag` event to send the shape's position to the server.</span></span>
9. <span data-ttu-id="1c3ee-184">F5 キーを押してアプリケーションを起動します。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-184">Start the application by pressing F5.</span></span> <span data-ttu-id="1c3ee-185">ページの URL をコピーし、2番目のブラウザーウィンドウに貼り付けます。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-185">Copy the page's URL, and paste it into a second browser window.</span></span> <span data-ttu-id="1c3ee-186">ブラウザーウィンドウのいずれかで図形をドラッグします。他のブラウザーウィンドウの図形は移動します。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-186">Drag the shape in one of the browser windows; the shape in the other browser window should move.</span></span>

    ![アプリケーションウィンドウ](tutorial-high-frequency-realtime-with-signalr/_static/image4.png)

<a id="clientloop"></a>

## <a name="add-the-client-loop"></a><span data-ttu-id="1c3ee-188">クライアントループを追加する</span><span class="sxs-lookup"><span data-stu-id="1c3ee-188">Add the client loop</span></span>

<span data-ttu-id="1c3ee-189">すべてのマウス移動イベントに対して図形の場所を送信すると、不要なネットワークトラフィックが発生するため、クライアントからのメッセージを調整する必要があります。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-189">Since sending the location of the shape on every mouse move event will create an unnecessary amount of network traffic, the messages from the client need to be throttled.</span></span> <span data-ttu-id="1c3ee-190">Javascript `setInterval` 関数を使用して、固定レートでサーバーに新しい位置情報を送信するループを設定します。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-190">We'll use the javascript `setInterval` function to set up a loop that sends new position information to the server at a fixed rate.</span></span> <span data-ttu-id="1c3ee-191">このループは、ゲームまたはその他のシミュレーションのすべての機能を駆動する "ゲームループ" の非常に基本的な表現です。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-191">This loop is a very basic representation of a "game loop", a repeatedly called function that drives all of the functionality of a game or other simulation.</span></span>

1. <span data-ttu-id="1c3ee-192">次のコードスニペットと一致するように、HTML ページのクライアントコードを更新します。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-192">Update the client code in the HTML page to match the following code snippet.</span></span>

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample8.html)]

    <span data-ttu-id="1c3ee-193">上記の更新では、固定頻度で呼び出される `updateServerModel` 関数が追加されます。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-193">The above update adds the `updateServerModel` function, which gets called on a fixed frequency.</span></span> <span data-ttu-id="1c3ee-194">この関数は、`moved` フラグによって、送信する新しい位置データがあることが示されたときに、その位置データをサーバーに送信します。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-194">This function sends the position data to the server whenever the `moved` flag indicates that there is new position data to send.</span></span>
2. <span data-ttu-id="1c3ee-195">F5 キーを押してアプリケーションを起動します。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-195">Start the application by pressing F5.</span></span> <span data-ttu-id="1c3ee-196">ページの URL をコピーし、2番目のブラウザーウィンドウに貼り付けます。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-196">Copy the page's URL, and paste it into a second browser window.</span></span> <span data-ttu-id="1c3ee-197">ブラウザーウィンドウのいずれかで図形をドラッグします。他のブラウザーウィンドウの図形は移動します。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-197">Drag the shape in one of the browser windows; the shape in the other browser window should move.</span></span> <span data-ttu-id="1c3ee-198">サーバーに送信されるメッセージの数は制限されるため、アニメーションは前のセクションと同様に smooth として表示されません。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-198">Since the number of messages that get sent to the server will be throttled, the animation will not appear as smooth as in the previous section.</span></span>

    ![アプリケーションウィンドウ](tutorial-high-frequency-realtime-with-signalr/_static/image5.png)

<a id="serverloop"></a>

## <a name="add-the-server-loop"></a><span data-ttu-id="1c3ee-200">サーバーループの追加</span><span class="sxs-lookup"><span data-stu-id="1c3ee-200">Add the server loop</span></span>

<span data-ttu-id="1c3ee-201">現在のアプリケーションでは、サーバーからクライアントに送信されたメッセージは、受信された頻度で送信されます。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-201">In the current application, messages sent from the server to the client go out as often as they are received.</span></span> <span data-ttu-id="1c3ee-202">これは、クライアントで見られたのと同様の問題を示しています。メッセージは必要以上に頻繁に送信され、その結果、接続があふれてしまう可能性があります。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-202">This presents a similar problem as was seen on the client; messages can be sent more often than they are needed, and the connection could become flooded as a result.</span></span> <span data-ttu-id="1c3ee-203">このセクションでは、送信メッセージの速度を調整するタイマーを実装するようにサーバーを更新する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-203">This section describes how to update the server to implement a timer that throttles the rate of the outgoing messages.</span></span>

1. <span data-ttu-id="1c3ee-204">`MoveShapeHub.cs` の内容を次のコードスニペットに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-204">Replace the contents of `MoveShapeHub.cs` with the following code snippet.</span></span>

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample9.cs)]

    <span data-ttu-id="1c3ee-205">上記のコードでは、クライアントを拡張して `Broadcaster` クラスを追加しています。これにより、.NET framework の `Timer` クラスを使用して送信メッセージが調整されます。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-205">The above code expands the client to add the `Broadcaster` class, which throttles the outgoing messages using the `Timer` class from the .NET framework.</span></span>

    <span data-ttu-id="1c3ee-206">ハブ自体は一時的なものであるため (必要になるたびに作成されます)、`Broadcaster` がシングルトンとして作成されます。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-206">Since the hub itself is transitory (it is created every time it is needed), the `Broadcaster` will be created as a singleton.</span></span> <span data-ttu-id="1c3ee-207">遅延初期化 (.NET 4 で導入) は、必要になるまで作成を延期するために使用されます。これにより、タイマーが開始される前に最初のハブインスタンスが完全に作成されます。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-207">Lazy initialization (introduced in .NET 4) is used to defer its creation until it is needed, ensuring that the first hub instance is completely created before the timer is started.</span></span>

    <span data-ttu-id="1c3ee-208">次に、クライアントの `UpdateShape` 関数の呼び出しはハブの `UpdateModel` メソッドから移動され、受信メッセージが受信されるとすぐには呼び出されなくなります。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-208">The call to the clients' `UpdateShape` function is then moved out of the hub's `UpdateModel` method, so that it is no longer called immediately whenever incoming messages are received.</span></span> <span data-ttu-id="1c3ee-209">代わりに、クライアントへのメッセージは、`Broadcaster` クラス内から `_broadcastLoop` タイマーによって管理される、1秒あたり25回の呼び出しで送信されます。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-209">Instead, the messages to the clients will be sent at a rate of 25 calls per second, managed by the `_broadcastLoop` timer from within the `Broadcaster` class.</span></span>

    <span data-ttu-id="1c3ee-210">最後に、ハブからクライアントメソッドを直接呼び出すのではなく、`Broadcaster` クラスは `GlobalHost`を使用して現在の操作ハブ (`_hubContext`) への参照を取得する必要があります。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-210">Lastly, instead of calling the client method from the hub directly, the `Broadcaster` class needs to obtain a reference to the currently operating hub (`_hubContext`) using the `GlobalHost`.</span></span>
2. <span data-ttu-id="1c3ee-211">F5 キーを押してアプリケーションを起動します。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-211">Start the application by pressing F5.</span></span> <span data-ttu-id="1c3ee-212">ページの URL をコピーし、2番目のブラウザーウィンドウに貼り付けます。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-212">Copy the page's URL, and paste it into a second browser window.</span></span> <span data-ttu-id="1c3ee-213">ブラウザーウィンドウのいずれかで図形をドラッグします。他のブラウザーウィンドウの図形は移動します。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-213">Drag the shape in one of the browser windows; the shape in the other browser window should move.</span></span> <span data-ttu-id="1c3ee-214">前のセクションのブラウザーには表示される違いはありませんが、クライアントに送信されるメッセージの数は制限されます。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-214">There will not be a visible difference in the browser from the previous section, but the number of messages that get sent to the client will be throttled.</span></span>

    ![アプリケーションウィンドウ](tutorial-high-frequency-realtime-with-signalr/_static/image6.png)

<a id="animation"></a>

## <a name="add-smooth-animation-on-the-client"></a><span data-ttu-id="1c3ee-216">クライアントに smooth animation を追加する</span><span class="sxs-lookup"><span data-stu-id="1c3ee-216">Add smooth animation on the client</span></span>

<span data-ttu-id="1c3ee-217">アプリケーションはほぼ完成していますが、サーバーメッセージに応答してクライアントが移動されるときに、クライアント上の図形の動きにおいて、改良が加えられています。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-217">The application is almost complete, but we could make one more improvement, in the motion of the shape on the client as it is moved in response to server messages.</span></span> <span data-ttu-id="1c3ee-218">図形の位置をサーバーによって指定された新しい場所に設定するのではなく、JQuery UI ライブラリの `animate` 関数を使用して、現在と新しい位置の間で図形を滑らかに移動します。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-218">Rather than setting the position of the shape to the new location given by the server, we'll use the JQuery UI library's `animate` function to move the shape smoothly between its current and new position.</span></span>

1. <span data-ttu-id="1c3ee-219">次の強調表示されているコードのように、クライアントの `updateShape` メソッドを更新します。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-219">Update the client's `updateShape` method to look like the highlighted code below:</span></span>

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample10.html?highlight=35-42)]

    <span data-ttu-id="1c3ee-220">上のコードでは、アニメーションの間隔 (この場合は100ミリ秒) で、前の場所からサーバーによって指定された新しい位置に図形を移動します。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-220">The above code moves the shape from the old location to the new one given by the server over the course of the animation interval (in this case, 100 milliseconds).</span></span> <span data-ttu-id="1c3ee-221">図形で実行されている前のアニメーションは、新しいアニメーションが開始される前にクリアされます。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-221">Any previous animation running on the shape is cleared before the new animation starts.</span></span>
2. <span data-ttu-id="1c3ee-222">F5 キーを押してアプリケーションを起動します。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-222">Start the application by pressing F5.</span></span> <span data-ttu-id="1c3ee-223">ページの URL をコピーし、2番目のブラウザーウィンドウに貼り付けます。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-223">Copy the page's URL, and paste it into a second browser window.</span></span> <span data-ttu-id="1c3ee-224">ブラウザーウィンドウのいずれかで図形をドラッグします。他のブラウザーウィンドウの図形は移動します。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-224">Drag the shape in one of the browser windows; the shape in the other browser window should move.</span></span> <span data-ttu-id="1c3ee-225">他のウィンドウでの図形の移動は、受信メッセージごとに1回設定されるのではなく、時間の経過と共に補間されるため、不自然に見えないようになります。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-225">The movement of the shape in the other window should appear less jerky as its movement is interpolated over time rather than being set once per incoming message.</span></span>

    ![アプリケーションウィンドウ](tutorial-high-frequency-realtime-with-signalr/_static/image7.png)

<a id="furthersteps"></a>

## <a name="further-steps"></a><span data-ttu-id="1c3ee-227">その他の手順</span><span class="sxs-lookup"><span data-stu-id="1c3ee-227">Further Steps</span></span>

<span data-ttu-id="1c3ee-228">このチュートリアルでは、クライアントとサーバー間で頻度の高いメッセージを送信する SignalR アプリケーションをプログラミングする方法を学習しました。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-228">In this tutorial, you've learned how to program a SignalR application that sends high-frequency messages between clients and servers.</span></span> <span data-ttu-id="1c3ee-229">この通信パラダイムは、オンラインゲームや、 [SignalR で作成された ShootR ゲーム](http://shootr.signalr.net)などの他のシミュレーションを開発する場合に便利です。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-229">This communication paradigm is useful for developing online games and other simulations, such as [the ShootR game created with SignalR](http://shootr.signalr.net).</span></span>

<span data-ttu-id="1c3ee-230">このチュートリアルで作成した完全なアプリケーションは、[コードギャラリー](https://code.msdn.microsoft.com/SignalR-MoveShape-demo-3366dac6)からダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-230">The complete application created in this tutorial can be downloaded from [Code Gallery](https://code.msdn.microsoft.com/SignalR-MoveShape-demo-3366dac6).</span></span>

<span data-ttu-id="1c3ee-231">SignalR development の概念の詳細については、SignalR のソースコードとリソースに関する次のサイトを参照してください。</span><span class="sxs-lookup"><span data-stu-id="1c3ee-231">To learn more about SignalR development concepts, visit the following sites for SignalR source code and resources:</span></span>

- [<span data-ttu-id="1c3ee-232">SignalR プロジェクト</span><span class="sxs-lookup"><span data-stu-id="1c3ee-232">SignalR Project</span></span>](http://signalr.net)
- [<span data-ttu-id="1c3ee-233">SignalR Github とサンプル</span><span class="sxs-lookup"><span data-stu-id="1c3ee-233">SignalR Github and Samples</span></span>](https://github.com/SignalR/SignalR)
- [<span data-ttu-id="1c3ee-234">SignalR Wiki</span><span class="sxs-lookup"><span data-stu-id="1c3ee-234">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)
