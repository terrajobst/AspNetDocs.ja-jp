---
uid: signalr/overview/testing-and-debugging/unit-testing-signalr-applications
title: SignalR Applications の単体テスト |Microsoft Docs
author: bradygaster
description: この記事では、SignalR 2.0 の単体テスト機能を使用する方法について説明します。
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: d1983524-e0d5-4ee6-9d87-1f552f7cb964
msc.legacyurl: /signalr/overview/testing-and-debugging/unit-testing-signalr-applications
msc.type: authoredcontent
ms.openlocfilehash: 2cf2e88f141d89971439dc1fc4979849f8dded47
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467302"
---
# <a name="unit-testing-signalr-applications"></a><span data-ttu-id="24f41-103">SignalR アプリケーションの単体テスト</span><span class="sxs-lookup"><span data-stu-id="24f41-103">Unit Testing SignalR Applications</span></span>

<span data-ttu-id="24f41-104">([パトリック Fletcher](https://github.com/pfletcher) )</span><span class="sxs-lookup"><span data-stu-id="24f41-104">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="24f41-105">この記事では、SignalR 2 の単体テスト機能の使用方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="24f41-105">This article describes using the Unit Testing features of SignalR 2.</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="24f41-106">このトピックで使用されているソフトウェアのバージョン</span><span class="sxs-lookup"><span data-stu-id="24f41-106">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="24f41-107">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="24f41-107">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="24f41-108">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="24f41-108">.NET 4.5</span></span>
> - <span data-ttu-id="24f41-109">SignalR バージョン2</span><span class="sxs-lookup"><span data-stu-id="24f41-109">SignalR version 2</span></span>
>
>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="24f41-110">質問とコメント</span><span class="sxs-lookup"><span data-stu-id="24f41-110">Questions and comments</span></span>
>
> <span data-ttu-id="24f41-111">このチュートリアルの良い点に関するフィードバックや、ページ下部にあるコメントで改善できる点をお知らせください。</span><span class="sxs-lookup"><span data-stu-id="24f41-111">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="24f41-112">チュートリアルに直接関係のない質問がある場合は、 [ASP.NET SignalR フォーラム](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)または[StackOverflow.com](http://stackoverflow.com/)に投稿できます。</span><span class="sxs-lookup"><span data-stu-id="24f41-112">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

<a id="unit"></a>
## <a name="unit-testing-signalr-applications"></a><span data-ttu-id="24f41-113">SignalR アプリケーションの単体テスト</span><span class="sxs-lookup"><span data-stu-id="24f41-113">Unit testing SignalR applications</span></span>

<span data-ttu-id="24f41-114">SignalR 2 の単体テスト機能を使用して、SignalR アプリケーションの単体テストを作成できます。</span><span class="sxs-lookup"><span data-stu-id="24f41-114">You can use the unit test features in SignalR 2 to create unit tests for your SignalR application.</span></span> <span data-ttu-id="24f41-115">SignalR 2 には[IHubCallerConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.ihubcallerconnectioncontext(v=vs.118).aspx)インターフェイスが含まれています。このインターフェイスを使用して、テスト用のハブメソッドをシミュレートするモックオブジェクトを作成できます。</span><span class="sxs-lookup"><span data-stu-id="24f41-115">SignalR 2 includes the [IHubCallerConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.ihubcallerconnectioncontext(v=vs.118).aspx) interface, which can be used to create a mock object to simulate your hub methods for testing.</span></span>

<span data-ttu-id="24f41-116">このセクションでは、 [XUnit.net](https://github.com/xunit/xunit)と[moq](https://github.com/Moq/moq4)を使用して[はじめにチュートリアル](../getting-started/tutorial-getting-started-with-signalr.md)で作成したアプリケーションの単体テストを追加します。</span><span class="sxs-lookup"><span data-stu-id="24f41-116">In this section, you'll add unit tests for the application created in the [Getting Started tutorial](../getting-started/tutorial-getting-started-with-signalr.md) using [XUnit.net](https://github.com/xunit/xunit) and [Moq](https://github.com/Moq/moq4).</span></span>

<span data-ttu-id="24f41-117">XUnit.net は、テストを制御するために使用されます。Moq は、テスト用の[モック](http://en.wikipedia.org/wiki/Mock_object)オブジェクトを作成するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="24f41-117">XUnit.net will be used to control the test; Moq will be used to create a [mock](http://en.wikipedia.org/wiki/Mock_object) object for testing.</span></span> <span data-ttu-id="24f41-118">必要に応じて、他のモックフレームワークを使用することもできます。また、 [Nsubstitute](http://nsubstitute.github.io/)も選択することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="24f41-118">Other mocking frameworks can be used if desired; [NSubstitute](http://nsubstitute.github.io/) is also a good choice.</span></span> <span data-ttu-id="24f41-119">このチュートリアルでは、2つの方法でモックオブジェクトを設定する方法について説明します。最初に、`dynamic` オブジェクト (.NET Framework 4 で導入) を使用し、2つ目にインターフェイスを使用します。</span><span class="sxs-lookup"><span data-stu-id="24f41-119">This tutorial demonstrates how to set up the mock object in two ways: First, using a `dynamic` object (introduced in .NET Framework 4), and second, using an interface.</span></span>

### <a name="contents"></a><span data-ttu-id="24f41-120">内容</span><span class="sxs-lookup"><span data-stu-id="24f41-120">Contents</span></span>

<span data-ttu-id="24f41-121">このチュートリアルは、次のセクションで構成されています。</span><span class="sxs-lookup"><span data-stu-id="24f41-121">This tutorial contains the following sections.</span></span>

- [<span data-ttu-id="24f41-122">動的な単体テスト</span><span class="sxs-lookup"><span data-stu-id="24f41-122">Unit testing with Dynamic</span></span>](#dynamic)
- [<span data-ttu-id="24f41-123">種類別の単体テスト</span><span class="sxs-lookup"><span data-stu-id="24f41-123">Unit testing by type</span></span>](#type)

<a id="dynamic"></a>
### <a name="unit-testing-with-dynamic"></a><span data-ttu-id="24f41-124">動的な単体テスト</span><span class="sxs-lookup"><span data-stu-id="24f41-124">Unit testing with Dynamic</span></span>

<span data-ttu-id="24f41-125">このセクションでは、[はじめにチュートリアル](../getting-started/tutorial-getting-started-with-signalr.md)で作成したアプリケーションの単体テストを動的オブジェクトを使用して追加します。</span><span class="sxs-lookup"><span data-stu-id="24f41-125">In this section, you'll add a unit test for the application created in the [Getting Started tutorial](../getting-started/tutorial-getting-started-with-signalr.md) using a dynamic object.</span></span>

1. <span data-ttu-id="24f41-126">Visual Studio 2013 用の[Xunit ランナー拡張機能](https://visualstudiogallery.msdn.microsoft.com/463c5987-f82b-46c8-a97e-b1cde42b9099)をインストールします。</span><span class="sxs-lookup"><span data-stu-id="24f41-126">Install the [XUnit Runner extension](https://visualstudiogallery.msdn.microsoft.com/463c5987-f82b-46c8-a97e-b1cde42b9099) for Visual Studio 2013.</span></span>
2. <span data-ttu-id="24f41-127">[はじめにチュートリアル](../getting-started/tutorial-getting-started-with-signalr.md)を完了するか、 [MSDN コードギャラリー](https://code.msdn.microsoft.com/SignalR-Getting-Started-b9d18aa9)から完成したアプリケーションをダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="24f41-127">Either complete the [Getting Started tutorial](../getting-started/tutorial-getting-started-with-signalr.md), or download the completed application from [MSDN Code Gallery](https://code.msdn.microsoft.com/SignalR-Getting-Started-b9d18aa9).</span></span>
3. <span data-ttu-id="24f41-128">ダウンロードバージョンのはじめにアプリケーションを使用している場合は、**パッケージマネージャーコンソール**を開き、 **[復元]** をクリックして SignalR パッケージをプロジェクトに追加します。</span><span class="sxs-lookup"><span data-stu-id="24f41-128">If you are using the download version of the Getting Started application, open **Package Manager Console** and click **Restore** to add the SignalR package to the project.</span></span>

    ![パッケージの復元](unit-testing-signalr-applications/_static/image1.png)
4. <span data-ttu-id="24f41-130">単体テストのソリューションにプロジェクトを追加します。</span><span class="sxs-lookup"><span data-stu-id="24f41-130">Add a project to the solution for the unit test.</span></span> <span data-ttu-id="24f41-131">**ソリューションエクスプローラー**でソリューションを右クリックし、 **[追加]** 、 **[新しいプロジェクト...]** の順に選択します。**C#** ノードの下で、 **[Windows]** ノードを選択します。</span><span class="sxs-lookup"><span data-stu-id="24f41-131">Right-click your solution in **Solution Explorer** and select **Add**, **New Project...**. Under the **C#** node, select the **Windows** node.</span></span> <span data-ttu-id="24f41-132">**[クラスライブラリ]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="24f41-132">Select **Class Library**.</span></span> <span data-ttu-id="24f41-133">新しいプロジェクトに**Testlibrary**という名前を指定し、[ **OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="24f41-133">Name the new project **TestLibrary** and click **OK**.</span></span>

    ![テストライブラリの作成](unit-testing-signalr-applications/_static/image2.png)
5. <span data-ttu-id="24f41-135">テストライブラリプロジェクトで、SignalRChat プロジェクトに参照を追加します。</span><span class="sxs-lookup"><span data-stu-id="24f41-135">Add a reference in the test library project to the SignalRChat project.</span></span> <span data-ttu-id="24f41-136">**Testlibrary**プロジェクトを右クリックし、 **[追加]** 、 **[参照]** の順に選択します。**ソリューション**ノードの下にある **[プロジェクト]** ノードを選択し、 **[signalrchat]** をオンにします。</span><span class="sxs-lookup"><span data-stu-id="24f41-136">Right-click the **TestLibrary** project and select **Add**, **Reference...**. Select the **Projects** node under the **Solution** node, and check **SignalRChat**.</span></span> <span data-ttu-id="24f41-137">**[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="24f41-137">Click **OK**.</span></span>

    ![プロジェクト参照の追加](unit-testing-signalr-applications/_static/image3.png)
6. <span data-ttu-id="24f41-139">SignalR、Moq、および XUnit パッケージを**Testlibrary**プロジェクトに追加します。</span><span class="sxs-lookup"><span data-stu-id="24f41-139">Add the SignalR, Moq, and XUnit packages to the **TestLibrary** project.</span></span> <span data-ttu-id="24f41-140">**パッケージマネージャーコンソール**で、既定の **[プロジェクト]** ドロップダウンを **[testlibrary]** に設定します。</span><span class="sxs-lookup"><span data-stu-id="24f41-140">In the **Package Manager Console**, set the **Default Project** dropdown to **TestLibrary**.</span></span> <span data-ttu-id="24f41-141">コンソールウィンドウで、次のコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="24f41-141">Run the following commands in the console window:</span></span>

   - `Install-Package Microsoft.AspNet.SignalR`
   - `Install-Package Moq`
   - `Install-Package XUnit`

     ![パッケージのインストール](unit-testing-signalr-applications/_static/image4.png)
7. <span data-ttu-id="24f41-143">テストファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="24f41-143">Create the test file.</span></span> <span data-ttu-id="24f41-144">**Testlibrary**プロジェクトを右クリックし、 **[追加]** 、 **[クラス]** の順にクリックします。</span><span class="sxs-lookup"><span data-stu-id="24f41-144">Right-click the **TestLibrary** project and click **Add...**, **Class**.</span></span> <span data-ttu-id="24f41-145">新しいクラスに**Tests.cs**という名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="24f41-145">Name the new class **Tests.cs**.</span></span>
8. <span data-ttu-id="24f41-146">Tests.cs の内容を次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="24f41-146">Replace the contents of Tests.cs with the following code.</span></span>

    [!code-csharp[Main](unit-testing-signalr-applications/samples/sample1.cs)]

    <span data-ttu-id="24f41-147">上記のコードでは、 [IHubCallerConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.ihubcallerconnectioncontext(v=vs.118).aspx)型の[moq](https://github.com/Moq/moq4)ライブラリの `Mock` オブジェクトを使用してテストクライアントが作成されます (SignalR 2.1 では、型パラメーターに `dynamic` を割り当てます)。`IHubCallerConnectionContext` インターフェイスは、クライアントでメソッドを呼び出すためのプロキシオブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="24f41-147">In the code above, a test client is created using the `Mock` object from the [Moq](https://github.com/Moq/moq4) library, of type [IHubCallerConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.ihubcallerconnectioncontext(v=vs.118).aspx) (in SignalR 2.1, assign `dynamic` for the type parameter.) The `IHubCallerConnectionContext` interface is the proxy object with which you invoke methods on the client.</span></span> <span data-ttu-id="24f41-148">その後、`broadcastMessage` 関数がモッククライアントに対して定義され、`ChatHub` クラスから呼び出すことができるようになります。</span><span class="sxs-lookup"><span data-stu-id="24f41-148">The `broadcastMessage` function is then defined for the mock client so that it can be called by the `ChatHub` class.</span></span> <span data-ttu-id="24f41-149">次に、テストエンジンは、`ChatHub` クラスの `Send` メソッドを呼び出します。このメソッドはモック `broadcastMessage` 関数を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="24f41-149">The test engine then calls the `Send` method of the `ChatHub` class, which in turn calls the mocked `broadcastMessage` function.</span></span>
9. <span data-ttu-id="24f41-150">**F6**キーを押してソリューションをビルドします。</span><span class="sxs-lookup"><span data-stu-id="24f41-150">Build the solution by pressing **F6**.</span></span>
10. <span data-ttu-id="24f41-151">単体テストを実行します。</span><span class="sxs-lookup"><span data-stu-id="24f41-151">Run the unit test.</span></span> <span data-ttu-id="24f41-152">Visual Studio で、 **[テスト]** 、 **[Windows]** 、 **[テストエクスプローラー]** の順番に選択します。</span><span class="sxs-lookup"><span data-stu-id="24f41-152">In Visual Studio, select **Test**, **Windows**, **Test Explorer**.</span></span> <span data-ttu-id="24f41-153">テストエクスプローラー ウィンドウで、 **HubsAreMockableViaDynamic** を右クリックし、**選択したテストの実行** を選択します。</span><span class="sxs-lookup"><span data-stu-id="24f41-153">In the Test Explorer window, right-click **HubsAreMockableViaDynamic** and select **Run Selected Tests**.</span></span>

    ![テスト エクスプローラー](unit-testing-signalr-applications/_static/image5.png)
11. <span data-ttu-id="24f41-155">[テストエクスプローラー] ウィンドウの下側のペインで、テストが成功したことを確認します。</span><span class="sxs-lookup"><span data-stu-id="24f41-155">Verify that the test passed by checking the lower pane in the Test Explorer window.</span></span> <span data-ttu-id="24f41-156">テストが成功したことがウィンドウに表示されます。</span><span class="sxs-lookup"><span data-stu-id="24f41-156">The window will show that the test passed.</span></span>

    ![テスト成功](unit-testing-signalr-applications/_static/image6.png)

<a id="type"></a>
### <a name="unit-testing-by-type"></a><span data-ttu-id="24f41-158">種類別の単体テスト</span><span class="sxs-lookup"><span data-stu-id="24f41-158">Unit testing by type</span></span>

<span data-ttu-id="24f41-159">このセクションでは、[はじめにチュートリアル](../getting-started/tutorial-getting-started-with-signalr.md)で作成したアプリケーションのテストを、テスト対象のメソッドを含むインターフェイスを使用して追加します。</span><span class="sxs-lookup"><span data-stu-id="24f41-159">In this section, you'll add a test for the application created in the [Getting Started tutorial](../getting-started/tutorial-getting-started-with-signalr.md) using an interface that contains the method to be tested.</span></span>

1. <span data-ttu-id="24f41-160">前の「動的チュートリアル[を使用した単体テスト](#dynamic)」の手順1-7 を実行します。</span><span class="sxs-lookup"><span data-stu-id="24f41-160">Complete steps 1-7 in the [Unit testing with Dynamic](#dynamic) tutorial above.</span></span>
2. <span data-ttu-id="24f41-161">Tests.cs の内容を次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="24f41-161">Replace the contents of Tests.cs with the following code.</span></span>

    [!code-csharp[Main](unit-testing-signalr-applications/samples/sample2.cs)]

    <span data-ttu-id="24f41-162">上記のコードでは、テストエンジンがモッククライアントを作成するための `broadcastMessage` メソッドのシグネチャを定義するインターフェイスが作成されます。</span><span class="sxs-lookup"><span data-stu-id="24f41-162">In the code above, an interface is created defining the signature of the `broadcastMessage` method for which the test engine will create a mock client.</span></span> <span data-ttu-id="24f41-163">モッククライアントは、 [IHubCallerConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.ihubcallerconnectioncontext(v=vs.118).aspx)型の `Mock` オブジェクトを使用して作成されます (SignalR 2.1 では、型パラメーターに `dynamic` を割り当てます)。`IHubCallerConnectionContext` インターフェイスは、クライアントでメソッドを呼び出すためのプロキシオブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="24f41-163">A mock client is then created using the `Mock` object, of type [IHubCallerConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.ihubcallerconnectioncontext(v=vs.118).aspx) (in SignalR 2.1, assign `dynamic` for the type parameter.) The `IHubCallerConnectionContext` interface is the proxy object with which you invoke methods on the client.</span></span>

    <span data-ttu-id="24f41-164">次に、`ChatHub`のインスタンスを作成し、`broadcastMessage` メソッドのモックバージョンを作成します。これは、ハブで `Send` メソッドを呼び出すことによって呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="24f41-164">The test then creates an instance of `ChatHub`, and then creates a mock version of the `broadcastMessage` method, which in turn is invoked by calling the `Send` method on the hub.</span></span>
3. <span data-ttu-id="24f41-165">**F6**キーを押してソリューションをビルドします。</span><span class="sxs-lookup"><span data-stu-id="24f41-165">Build the solution by pressing **F6**.</span></span>
4. <span data-ttu-id="24f41-166">単体テストを実行します。</span><span class="sxs-lookup"><span data-stu-id="24f41-166">Run the unit test.</span></span> <span data-ttu-id="24f41-167">Visual Studio で、 **[テスト]** 、 **[Windows]** 、 **[テストエクスプローラー]** の順番に選択します。</span><span class="sxs-lookup"><span data-stu-id="24f41-167">In Visual Studio, select **Test**, **Windows**, **Test Explorer**.</span></span> <span data-ttu-id="24f41-168">テストエクスプローラー ウィンドウで、 **HubsAreMockableViaDynamic** を右クリックし、**選択したテストの実行** を選択します。</span><span class="sxs-lookup"><span data-stu-id="24f41-168">In the Test Explorer window, right-click **HubsAreMockableViaDynamic** and select **Run Selected Tests**.</span></span>

    ![テスト エクスプローラー](unit-testing-signalr-applications/_static/image7.png)
5. <span data-ttu-id="24f41-170">[テストエクスプローラー] ウィンドウの下側のペインで、テストが成功したことを確認します。</span><span class="sxs-lookup"><span data-stu-id="24f41-170">Verify that the test passed by checking the lower pane in the Test Explorer window.</span></span> <span data-ttu-id="24f41-171">テストが成功したことがウィンドウに表示されます。</span><span class="sxs-lookup"><span data-stu-id="24f41-171">The window will show that the test passed.</span></span>

    ![テスト成功](unit-testing-signalr-applications/_static/image8.png)
