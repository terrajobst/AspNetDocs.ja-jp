---
uid: web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api
title: OWIN を使用して自己ホスト ASP.NET Web API-ASP.NET 4.x
author: rick-anderson
description: コンソールアプリケーションで ASP.NET Web API をホストする方法を示すコードを使用したチュートリアルです。
ms.author: riande
ms.date: 07/09/2013
ms.custom: seoapril2019
ms.assetid: a90a04ce-9d07-43ad-8250-8a92fb2bd3d5
msc.legacyurl: /web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api
msc.type: authoredcontent
ms.openlocfilehash: 872b931391a63ef82b96e5b264c070c0b5e9605d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448330"
---
# <a name="use-owin-to-self-host-aspnet-web-api"></a><span data-ttu-id="1c1a7-103">OWIN を使用して自己ホスト ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="1c1a7-103">Use OWIN to Self-Host ASP.NET Web API</span></span> 

> <span data-ttu-id="1c1a7-104">このチュートリアルでは、OWIN を使用して Web API フレームワークをセルフホストするコンソールアプリケーションで ASP.NET Web API をホストする方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="1c1a7-104">This tutorial shows how to host ASP.NET Web API in a console application, using OWIN to self-host the Web API framework.</span></span>
>
> <span data-ttu-id="1c1a7-105">[Open Web Interface for .net](http://owin.org) (OWIN) は、.net web サーバーと web アプリケーションの間の抽象化を定義します。</span><span class="sxs-lookup"><span data-stu-id="1c1a7-105">[Open Web Interface for .NET](http://owin.org) (OWIN) defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="1c1a7-106">OWIN は、サーバーから web アプリケーションを分離します。これにより、IIS の外部にある独自のプロセスで web アプリケーションを自己ホストするために OWIN が理想的になります。</span><span class="sxs-lookup"><span data-stu-id="1c1a7-106">OWIN decouples the web application from the server, which makes OWIN ideal for self-hosting a web application in your own process, outside of IIS.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="1c1a7-107">このチュートリアルで使用されているソフトウェアのバージョン</span><span class="sxs-lookup"><span data-stu-id="1c1a7-107">Software versions used in the tutorial</span></span>
>
>
> - [<span data-ttu-id="1c1a7-108">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="1c1a7-108">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/) 
> - <span data-ttu-id="1c1a7-109">Web API 5.2.7</span><span class="sxs-lookup"><span data-stu-id="1c1a7-109">Web API 5.2.7</span></span>

> [!NOTE]
> <span data-ttu-id="1c1a7-110">このチュートリアルの完全なソースコードについては、 [github.com/aspnet/samples](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/OwinSelfhostSample)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="1c1a7-110">You can find the complete source code for this tutorial at [github.com/aspnet/samples](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/OwinSelfhostSample).</span></span>

## <a name="create-a-console-application"></a><span data-ttu-id="1c1a7-111">コンソール アプリケーションの作成</span><span class="sxs-lookup"><span data-stu-id="1c1a7-111">Create a console application</span></span>

<span data-ttu-id="1c1a7-112">**[ファイル]** メニューの **[新規作成]** をポイントし、 **[プロジェクト]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="1c1a7-112">On the **File** menu,  **New**, then select **Project**.</span></span> <span data-ttu-id="1c1a7-113">**インストールされている**から、 **[ビジュアルC# ]** の下で **[Windows デスクトップ]** を選択し、 **[コンソールアプリ (.net Framework)]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="1c1a7-113">From **Installed**, under **Visual C#**, select **Windows Desktop** and then select **Console App (.Net Framework)**.</span></span> <span data-ttu-id="1c1a7-114">プロジェクトに "OwinSelfhostSample" という名前を指定し、[ **OK]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="1c1a7-114">Name the project "OwinSelfhostSample" and select **OK**.</span></span>

[![](use-owin-to-self-host-web-api/_static/image7.png)](use-owin-to-self-host-web-api/_static/image7.png)

## <a name="add-the-web-api-and-owin-packages"></a><span data-ttu-id="1c1a7-115">Web API と OWIN パッケージを追加する</span><span class="sxs-lookup"><span data-stu-id="1c1a7-115">Add the Web API and OWIN packages</span></span>

<span data-ttu-id="1c1a7-116">**[ツール]** メニューの **[NuGet パッケージマネージャー]** を選択し、 **[パッケージマネージャーコンソール]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="1c1a7-116">From the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="1c1a7-117">[パッケージ マネージャー コンソール] ウィンドウで、次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="1c1a7-117">In the Package Manager Console window, enter the following command:</span></span>

`Install-Package Microsoft.AspNet.WebApi.OwinSelfHost`

<span data-ttu-id="1c1a7-118">これにより、WebAPI OWIN selfhost パッケージと、必要なすべての OWIN パッケージがインストールされます。</span><span class="sxs-lookup"><span data-stu-id="1c1a7-118">This will install the WebAPI OWIN selfhost package and all the required OWIN packages.</span></span>

[![](use-owin-to-self-host-web-api/_static/image4.png)](use-owin-to-self-host-web-api/_static/image3.png)

## <a name="configure-web-api-for-self-host"></a><span data-ttu-id="1c1a7-119">セルフホスト用に Web API を構成する</span><span class="sxs-lookup"><span data-stu-id="1c1a7-119">Configure Web API for self-host</span></span>

<span data-ttu-id="1c1a7-120">ソリューションエクスプローラーで、プロジェクトを右クリックし、[ / **クラス**の**追加**] を選択して新しいクラスを追加します。</span><span class="sxs-lookup"><span data-stu-id="1c1a7-120">In Solution Explorer, right-click the project and select **Add** / **Class** to add a new class.</span></span> <span data-ttu-id="1c1a7-121">クラスに `Startup` という名前を付けます。</span><span class="sxs-lookup"><span data-stu-id="1c1a7-121">Name the class `Startup`.</span></span>

![](use-owin-to-self-host-web-api/_static/image5.png)

<span data-ttu-id="1c1a7-122">このファイルの定型コードをすべて次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="1c1a7-122">Replace all of the boilerplate code in this file with the following:</span></span>

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample1.cs)]

## <a name="add-a-web-api-controller"></a><span data-ttu-id="1c1a7-123">Web API コントローラーを追加する</span><span class="sxs-lookup"><span data-stu-id="1c1a7-123">Add a Web API controller</span></span>

<span data-ttu-id="1c1a7-124">次に、Web API コントローラークラスを追加します。</span><span class="sxs-lookup"><span data-stu-id="1c1a7-124">Next, add a Web API controller class.</span></span> <span data-ttu-id="1c1a7-125">ソリューションエクスプローラーで、プロジェクトを右クリックし、[ / **クラス**の**追加**] を選択して新しいクラスを追加します。</span><span class="sxs-lookup"><span data-stu-id="1c1a7-125">In Solution Explorer, right-click the project and select **Add** / **Class** to add a new class.</span></span> <span data-ttu-id="1c1a7-126">クラスに `ValuesController` という名前を付けます。</span><span class="sxs-lookup"><span data-stu-id="1c1a7-126">Name the class `ValuesController`.</span></span>

<span data-ttu-id="1c1a7-127">このファイルの定型コードをすべて次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="1c1a7-127">Replace all of the boilerplate code in this file with the following:</span></span>

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample2.cs)]

## <a name="start-the-owin-host-and-make-a-request-with-httpclient"></a><span data-ttu-id="1c1a7-128">OWIN ホストを起動し、HttpClient で要求を行う</span><span class="sxs-lookup"><span data-stu-id="1c1a7-128">Start the OWIN Host and make a request with HttpClient</span></span>

<span data-ttu-id="1c1a7-129">Program.cs ファイル内のすべての定型コードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="1c1a7-129">Replace all of the boilerplate code in the Program.cs file with the following:</span></span>

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample3.cs)]

## <a name="run-the-application"></a><span data-ttu-id="1c1a7-130">アプリケーションの実行</span><span class="sxs-lookup"><span data-stu-id="1c1a7-130">Run the application</span></span>

<span data-ttu-id="1c1a7-131">アプリケーションを実行するには、Visual Studio で F5 キーを押します。</span><span class="sxs-lookup"><span data-stu-id="1c1a7-131">To run the application, press F5 in Visual Studio.</span></span> <span data-ttu-id="1c1a7-132">出力は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="1c1a7-132">The output should look like the following:</span></span>

[!code-console[Main](use-owin-to-self-host-web-api/samples/sample4.cmd)]

![](use-owin-to-self-host-web-api/_static/image6.png)

## <a name="additional-resources"></a><span data-ttu-id="1c1a7-133">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="1c1a7-133">Additional resources</span></span>

[<span data-ttu-id="1c1a7-134">プロジェクト Katana の概要</span><span class="sxs-lookup"><span data-stu-id="1c1a7-134">An Overview of Project Katana</span></span>](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)

[<span data-ttu-id="1c1a7-135">Azure Worker ロールでのホスト ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="1c1a7-135">Host ASP.NET Web API in an Azure Worker Role</span></span>](host-aspnet-web-api-in-an-azure-worker-role.md)
