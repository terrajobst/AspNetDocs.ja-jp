---
uid: web-api/overview/testing-and-debugging/unit-testing-with-aspnet-web-api
title: 単体テスト ASP.NET Web API 2 |Microsoft Docs
author: Rick-Anderson
description: このガイダンスとアプリケーションでは、Web API 2 アプリケーションの単純な単体テストを作成する方法を示します。 このチュートリアルでは、単体テストを含める方法について説明します...
ms.author: riande
ms.date: 06/05/2014
ms.assetid: bf20f78d-ff91-48be-abd1-88e23dcc70ba
msc.legacyurl: /web-api/overview/testing-and-debugging/unit-testing-with-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: f2d60b977475e048a3a74aabff4adc768ee22baf
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78446986"
---
# <a name="unit-testing-aspnet-web-api-2"></a><span data-ttu-id="da582-104">単体テスト ASP.NET Web API 2</span><span class="sxs-lookup"><span data-stu-id="da582-104">Unit Testing ASP.NET Web API 2</span></span>

<span data-ttu-id="da582-105">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="da582-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[<span data-ttu-id="da582-106">完成したプロジェクトのダウンロード</span><span class="sxs-lookup"><span data-stu-id="da582-106">Download Completed Project</span></span>](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11)

> <span data-ttu-id="da582-107">このガイダンスとアプリケーションでは、Web API 2 アプリケーションの単純な単体テストを作成する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="da582-107">This guidance and application demonstrate how to create simple unit tests for your Web API 2 application.</span></span> <span data-ttu-id="da582-108">このチュートリアルでは、ソリューションに単体テストプロジェクトを追加し、コントローラーメソッドから返された値を確認するテストメソッドを記述する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="da582-108">This tutorial shows how to include a unit test project in your solution, and write test methods that check the returned values from a controller method.</span></span>
>
> <span data-ttu-id="da582-109">このチュートリアルでは、ASP.NET Web API の基本的な概念を理解していることを前提としています。</span><span class="sxs-lookup"><span data-stu-id="da582-109">This tutorial assumes you are familiar with the basic concepts of ASP.NET Web API.</span></span> <span data-ttu-id="da582-110">入門用のチュートリアルについては、「 [ASP.NET Web API 2 を使用したはじめに](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="da582-110">For an introductory tutorial, see [Getting Started with ASP.NET Web API 2](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md).</span></span>
>
> <span data-ttu-id="da582-111">このトピックの単体テストは、単純なデータのシナリオに意図的に限定されています。</span><span class="sxs-lookup"><span data-stu-id="da582-111">The unit tests in this topic are intentionally limited to simple data scenarios.</span></span> <span data-ttu-id="da582-112">より高度なデータシナリオの単体テストについては、「[単体テスト ASP.NET Web API 2](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md)」の「モック Entity Framework」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="da582-112">For unit testing more advanced data scenarios, see [Mocking Entity Framework when Unit Testing ASP.NET Web API 2](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md).</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="da582-113">このチュートリアルで使用されているソフトウェアのバージョン</span><span class="sxs-lookup"><span data-stu-id="da582-113">Software versions used in the tutorial</span></span>
>
> - [<span data-ttu-id="da582-114">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="da582-114">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
> - <span data-ttu-id="da582-115">Web API 2</span><span class="sxs-lookup"><span data-stu-id="da582-115">Web API 2</span></span>

## <a name="in-this-topic"></a><span data-ttu-id="da582-116">このトピックの内容</span><span class="sxs-lookup"><span data-stu-id="da582-116">In this topic</span></span>

<span data-ttu-id="da582-117">このトピックには、次のセクションが含まれます。</span><span class="sxs-lookup"><span data-stu-id="da582-117">This topic contains the following sections:</span></span>

- [<span data-ttu-id="da582-118">前提条件</span><span class="sxs-lookup"><span data-stu-id="da582-118">Prerequisites</span></span>](#prereqs)
- [<span data-ttu-id="da582-119">コードのダウンロード</span><span class="sxs-lookup"><span data-stu-id="da582-119">Download code</span></span>](#download)
- [<span data-ttu-id="da582-120">単体テストプロジェクトを使用したアプリケーションの作成</span><span class="sxs-lookup"><span data-stu-id="da582-120">Create application with unit test project</span></span>](#appwithunittest)
    - [<span data-ttu-id="da582-121">アプリケーションの作成時に単体テストプロジェクトを追加する</span><span class="sxs-lookup"><span data-stu-id="da582-121">Add unit test project when creating the application</span></span>](#whencreate)
    - [<span data-ttu-id="da582-122">既存のアプリケーションに単体テストプロジェクトを追加する</span><span class="sxs-lookup"><span data-stu-id="da582-122">Add unit test project to an existing application</span></span>](#addtoexisting)
- [<span data-ttu-id="da582-123">Web API 2 アプリケーションをセットアップする</span><span class="sxs-lookup"><span data-stu-id="da582-123">Set up the Web API 2 application</span></span>](#setupproject)
- [<span data-ttu-id="da582-124">テストプロジェクトに NuGet パッケージをインストールする</span><span class="sxs-lookup"><span data-stu-id="da582-124">Install NuGet packages in test project</span></span>](#testpackages)
- [<span data-ttu-id="da582-125">テストの作成</span><span class="sxs-lookup"><span data-stu-id="da582-125">Create tests</span></span>](#tests)
- [<span data-ttu-id="da582-126">テストの実行</span><span class="sxs-lookup"><span data-stu-id="da582-126">Run tests</span></span>](#runtests)

<a id="prereqs"></a>
## <a name="prerequisites"></a><span data-ttu-id="da582-127">前提条件</span><span class="sxs-lookup"><span data-stu-id="da582-127">Prerequisites</span></span>

<span data-ttu-id="da582-128">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)Community、Professional、または Enterprise edition</span><span class="sxs-lookup"><span data-stu-id="da582-128">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community, Professional or Enterprise edition</span></span>

<a id="download"></a>
## <a name="download-code"></a><span data-ttu-id="da582-129">コードをダウンロードする</span><span class="sxs-lookup"><span data-stu-id="da582-129">Download code</span></span>

<span data-ttu-id="da582-130">完成し[たプロジェクト](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11)をダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="da582-130">Download the [completed project](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11).</span></span> <span data-ttu-id="da582-131">ダウンロード可能なプロジェクトには、このトピックの単体テストコードと、[単体テスト ASP.NET Web API トピックのモック Entity Framework](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md)が含まれています。</span><span class="sxs-lookup"><span data-stu-id="da582-131">The downloadable project includes unit test code for this topic and for the [Mocking Entity Framework when Unit Testing ASP.NET Web API](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md) topic.</span></span>

<a id="appwithunittest"></a>
## <a name="create-application-with-unit-test-project"></a><span data-ttu-id="da582-132">単体テストプロジェクトを使用したアプリケーションの作成</span><span class="sxs-lookup"><span data-stu-id="da582-132">Create application with unit test project</span></span>

<span data-ttu-id="da582-133">アプリケーションを作成するとき、または既存のアプリケーションに単体テストプロジェクトを追加するときに、単体テストプロジェクトを作成することができます。</span><span class="sxs-lookup"><span data-stu-id="da582-133">You can either create a unit test project when creating your application or add a unit test project to an existing application.</span></span> <span data-ttu-id="da582-134">このチュートリアルでは、単体テストプロジェクトを作成する2つの方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="da582-134">This tutorial shows both methods for creating a unit test project.</span></span> <span data-ttu-id="da582-135">このチュートリアルを実行するには、どちらの方法でも使用できます。</span><span class="sxs-lookup"><span data-stu-id="da582-135">To follow this tutorial, you can use either approach.</span></span>

<a id="whencreate"></a>
### <a name="add-unit-test-project-when-creating-the-application"></a><span data-ttu-id="da582-136">アプリケーションの作成時に単体テストプロジェクトを追加する</span><span class="sxs-lookup"><span data-stu-id="da582-136">Add unit test project when creating the application</span></span>

<span data-ttu-id="da582-137">**Storeapp**という名前の新しい ASP.NET Web アプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="da582-137">Create a new ASP.NET Web Application named **StoreApp**.</span></span>

![プロジェクトの作成](unit-testing-with-aspnet-web-api/_static/image1.png)

<span data-ttu-id="da582-139">New ASP.NET プロジェクトウィンドウで、**空**のテンプレートを選択し、Web API のフォルダーとコア参照を追加します。</span><span class="sxs-lookup"><span data-stu-id="da582-139">In the New ASP.NET Project windows, select the **Empty** template and add folders and core references for Web API.</span></span> <span data-ttu-id="da582-140">**[単体テストの追加]** オプションを選択します。</span><span class="sxs-lookup"><span data-stu-id="da582-140">Select the **Add unit tests** option.</span></span> <span data-ttu-id="da582-141">単体テストプロジェクトには、 **Storeapp.** test という名前が自動的に付けられます。</span><span class="sxs-lookup"><span data-stu-id="da582-141">The unit test project is automatically named **StoreApp.Tests**.</span></span> <span data-ttu-id="da582-142">この名前をそのまま使用できます。</span><span class="sxs-lookup"><span data-stu-id="da582-142">You can keep this name.</span></span>

![単体テストプロジェクトの作成](unit-testing-with-aspnet-web-api/_static/image2.png)

<span data-ttu-id="da582-144">アプリケーションを作成すると、2つのプロジェクトが含まれていることがわかります。</span><span class="sxs-lookup"><span data-stu-id="da582-144">After creating the application, you will see it contains two projects.</span></span>

![2つのプロジェクト](unit-testing-with-aspnet-web-api/_static/image3.png)

<a id="addtoexisting"></a>
### <a name="add-unit-test-project-to-an-existing-application"></a><span data-ttu-id="da582-146">既存のアプリケーションに単体テストプロジェクトを追加する</span><span class="sxs-lookup"><span data-stu-id="da582-146">Add unit test project to an existing application</span></span>

<span data-ttu-id="da582-147">アプリケーションの作成時に単体テストプロジェクトを作成しなかった場合は、いつでも追加できます。</span><span class="sxs-lookup"><span data-stu-id="da582-147">If you did not create the unit test project when you created your application, you can add one at any time.</span></span> <span data-ttu-id="da582-148">たとえば、StoreApp という名前のアプリケーションが既にあり、単体テストを追加するとします。</span><span class="sxs-lookup"><span data-stu-id="da582-148">For example, suppose you already have an application named StoreApp, and you want to add unit tests.</span></span> <span data-ttu-id="da582-149">単体テストプロジェクトを追加するには、ソリューションを右クリックし、 **[追加]** 、 **[新しいプロジェクト]** の順に選択します。</span><span class="sxs-lookup"><span data-stu-id="da582-149">To add a unit test project, right-click your solution and select **Add** and **New Project**.</span></span>

![ソリューションへの新しいプロジェクトの追加](unit-testing-with-aspnet-web-api/_static/image4.png)

<span data-ttu-id="da582-151">左ペインで **[テスト]** を選択し、プロジェクトの種類として **[単体テストプロジェクト]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="da582-151">Select **Test** in the left pane, and select **Unit Test Project** for the project type.</span></span> <span data-ttu-id="da582-152">プロジェクトに Storeapp という名前を指定し**ます。**</span><span class="sxs-lookup"><span data-stu-id="da582-152">Name the project **StoreApp.Tests**.</span></span>

![単体テストプロジェクトの追加](unit-testing-with-aspnet-web-api/_static/image5.png)

<span data-ttu-id="da582-154">ソリューションに単体テストプロジェクトが表示されます。</span><span class="sxs-lookup"><span data-stu-id="da582-154">You will see the unit test project in your solution.</span></span>

<span data-ttu-id="da582-155">単体テストプロジェクトで、元のプロジェクトへのプロジェクト参照を追加します。</span><span class="sxs-lookup"><span data-stu-id="da582-155">In the unit test project, add a project reference to the original project.</span></span>

<a id="setupproject"></a>
## <a name="set-up-the-web-api-2-application"></a><span data-ttu-id="da582-156">Web API 2 アプリケーションをセットアップする</span><span class="sxs-lookup"><span data-stu-id="da582-156">Set up the Web API 2 application</span></span>

<span data-ttu-id="da582-157">StoreApp プロジェクトで、 **Product.cs**という名前の**モデル**フォルダーにクラスファイルを追加します。</span><span class="sxs-lookup"><span data-stu-id="da582-157">In your StoreApp project, add a class file to the **Models** folder named **Product.cs**.</span></span> <span data-ttu-id="da582-158">このファイルの内容を次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="da582-158">Replace the contents of the file with the following code.</span></span>

[!code-csharp[Main](unit-testing-with-aspnet-web-api/samples/sample1.cs)]

<span data-ttu-id="da582-159">ソリューションをビルドします。</span><span class="sxs-lookup"><span data-stu-id="da582-159">Build the solution.</span></span>

<span data-ttu-id="da582-160">Controllers フォルダーを右クリックし、 **[追加]** 、 **[新しいスキャフォールディング項目]** の順に選択します。</span><span class="sxs-lookup"><span data-stu-id="da582-160">Right-click the Controllers folder and select **Add** and **New Scaffolded Item**.</span></span> <span data-ttu-id="da582-161">**[WEB API 2 コントローラー-空]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="da582-161">Select **Web API 2 Controller - Empty**.</span></span>

![新しいコントローラーの追加](unit-testing-with-aspnet-web-api/_static/image6.png)

<span data-ttu-id="da582-163">コントローラー名を**Simpleproductcontroller**に設定し、 **[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="da582-163">Set the controller name to **SimpleProductController**, and click **Add**.</span></span>

![コントローラーの指定](unit-testing-with-aspnet-web-api/_static/image7.png)

<span data-ttu-id="da582-165">既存のコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="da582-165">Replace the existing code with the following code.</span></span> <span data-ttu-id="da582-166">この例を簡略化するために、データはデータベースではなく一覧に格納されます。</span><span class="sxs-lookup"><span data-stu-id="da582-166">To simplify this example, the data is stored in a list rather than a database.</span></span> <span data-ttu-id="da582-167">このクラスで定義されているリストは、実稼働データを表します。</span><span class="sxs-lookup"><span data-stu-id="da582-167">The list defined in this class represents the production data.</span></span> <span data-ttu-id="da582-168">コントローラーには、製品オブジェクトの一覧をパラメーターとして受け取るコンストラクターが含まれていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="da582-168">Notice that the controller includes a constructor that takes as a parameter a list of Product objects.</span></span> <span data-ttu-id="da582-169">このコンストラクターを使用すると、単体テスト時にテストデータを渡すことができます。</span><span class="sxs-lookup"><span data-stu-id="da582-169">This constructor enables you to pass test data when unit testing.</span></span> <span data-ttu-id="da582-170">また、このコントローラーには、非同期メソッドの単体テストを示す2つの**非同期**メソッドも含まれています。</span><span class="sxs-lookup"><span data-stu-id="da582-170">The controller also includes two **async** methods to illustrate unit testing asynchronous methods.</span></span> <span data-ttu-id="da582-171">これらの非同期メソッドは、余分なコードを最小限に抑えるために、 **FromResult**を呼び出すことによって実装されましたが、通常、メソッドにはリソースを大量に消費する操作が含まれます。</span><span class="sxs-lookup"><span data-stu-id="da582-171">These async methods were implemented by calling **Task.FromResult** to minimize extraneous code, but normally the methods would include resource-intensive operations.</span></span>

[!code-csharp[Main](unit-testing-with-aspnet-web-api/samples/sample2.cs)]

<span data-ttu-id="da582-172">GetProduct メソッドは、 **Ihttpactionresult**インターフェイスのインスタンスを返します。</span><span class="sxs-lookup"><span data-stu-id="da582-172">The GetProduct method returns an instance of the **IHttpActionResult** interface.</span></span> <span data-ttu-id="da582-173">IHttpActionResult は、Web API 2 の新機能の1つであり、単体テストの開発を簡略化します。</span><span class="sxs-lookup"><span data-stu-id="da582-173">IHttpActionResult is one of the new features in Web API 2, and it simplifies unit test development.</span></span> <span data-ttu-id="da582-174">IHttpActionResult インターフェイスを実装するクラスは、System.web. [http.sys](https://msdn.microsoft.com/library/system.web.http.results.aspx)名前空間にあります。</span><span class="sxs-lookup"><span data-stu-id="da582-174">Classes that implement the IHttpActionResult interface are found in the [System.Web.Http.Results](https://msdn.microsoft.com/library/system.web.http.results.aspx) namespace.</span></span> <span data-ttu-id="da582-175">これらのクラスは、アクション要求からの応答を表し、HTTP ステータスコードに対応します。</span><span class="sxs-lookup"><span data-stu-id="da582-175">These classes represent possible responses from an action request, and they correspond to HTTP status codes.</span></span>

<span data-ttu-id="da582-176">ソリューションをビルドします。</span><span class="sxs-lookup"><span data-stu-id="da582-176">Build the solution.</span></span>

<span data-ttu-id="da582-177">これで、テストプロジェクトを設定する準備ができました。</span><span class="sxs-lookup"><span data-stu-id="da582-177">You are now ready to set up the test project.</span></span>

<a id="testpackages"></a>
## <a name="install-nuget-packages-in-test-project"></a><span data-ttu-id="da582-178">テストプロジェクトに NuGet パッケージをインストールする</span><span class="sxs-lookup"><span data-stu-id="da582-178">Install NuGet packages in test project</span></span>

<span data-ttu-id="da582-179">空のテンプレートを使用してアプリケーションを作成する場合、単体テストプロジェクト (StoreApp. Tests) には、インストールされている NuGet パッケージは含まれません。</span><span class="sxs-lookup"><span data-stu-id="da582-179">When you use the Empty template to create an application, the unit test project (StoreApp.Tests) does not include any installed NuGet packages.</span></span> <span data-ttu-id="da582-180">Web API テンプレートなどの他のテンプレートには、単体テストプロジェクトにいくつかの NuGet パッケージが含まれています。</span><span class="sxs-lookup"><span data-stu-id="da582-180">Other templates, such as the Web API template, include some NuGet packages in the unit test project.</span></span> <span data-ttu-id="da582-181">このチュートリアルでは、テストプロジェクトに Microsoft ASP.NET Web API 2 コアパッケージを含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="da582-181">For this tutorial, you must include the Microsoft ASP.NET Web API 2 Core package to the test project.</span></span>

<span data-ttu-id="da582-182">StoreApp. Tests プロジェクトを右クリックし、 **[NuGet パッケージの管理]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="da582-182">Right-click the StoreApp.Tests project and select **Manage NuGet Packages**.</span></span> <span data-ttu-id="da582-183">パッケージをプロジェクトに追加するには、StoreApp. Tests プロジェクトを選択する必要があります。</span><span class="sxs-lookup"><span data-stu-id="da582-183">You must select the StoreApp.Tests project to add the packages to that project.</span></span>

![パッケージの管理](unit-testing-with-aspnet-web-api/_static/image8.png)

<span data-ttu-id="da582-185">Microsoft ASP.NET Web API 2 コアパッケージを検索してインストールします。</span><span class="sxs-lookup"><span data-stu-id="da582-185">Find and install Microsoft ASP.NET Web API 2 Core package.</span></span>

![web api core パッケージのインストール](unit-testing-with-aspnet-web-api/_static/image9.png)

<span data-ttu-id="da582-187">[NuGet パッケージの管理] ウィンドウを閉じます。</span><span class="sxs-lookup"><span data-stu-id="da582-187">Close the Manage NuGet Packages window.</span></span>

<a id="tests"></a>
## <a name="create-tests"></a><span data-ttu-id="da582-188">テストの作成</span><span class="sxs-lookup"><span data-stu-id="da582-188">Create tests</span></span>

<span data-ttu-id="da582-189">既定では、テストプロジェクトには、UnitTest1.cs という名前の空のテストファイルが含まれています。</span><span class="sxs-lookup"><span data-stu-id="da582-189">By default, your test project includes an empty test file named UnitTest1.cs.</span></span> <span data-ttu-id="da582-190">このファイルには、テストメソッドの作成に使用する属性が表示されます。</span><span class="sxs-lookup"><span data-stu-id="da582-190">This file shows the attributes you use to create test methods.</span></span> <span data-ttu-id="da582-191">単体テストでは、このファイルを使用するか、独自のファイルを作成することができます。</span><span class="sxs-lookup"><span data-stu-id="da582-191">For your unit tests, you can either use this file or create your own file.</span></span>

![UnitTest1](unit-testing-with-aspnet-web-api/_static/image10.png)

<span data-ttu-id="da582-193">このチュートリアルでは、独自のテストクラスを作成します。</span><span class="sxs-lookup"><span data-stu-id="da582-193">For this tutorial, you will create your own test class.</span></span> <span data-ttu-id="da582-194">UnitTest1.cs ファイルを削除できます。</span><span class="sxs-lookup"><span data-stu-id="da582-194">You can delete the UnitTest1.cs file.</span></span> <span data-ttu-id="da582-195">**TestSimpleProductController.cs**という名前のクラスを追加し、コードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="da582-195">Add a class named **TestSimpleProductController.cs**, and replace the code with the following code.</span></span>

[!code-csharp[Main](unit-testing-with-aspnet-web-api/samples/sample3.cs)]

<a id="runtests"></a>
## <a name="run-tests"></a><span data-ttu-id="da582-196">テストの実行</span><span class="sxs-lookup"><span data-stu-id="da582-196">Run tests</span></span>

<span data-ttu-id="da582-197">これで、テストを実行する準備が整いました。</span><span class="sxs-lookup"><span data-stu-id="da582-197">You are now ready to run the tests.</span></span> <span data-ttu-id="da582-198">"完了 **" 属性で**マークされているすべてのメソッドがテストされます。</span><span class="sxs-lookup"><span data-stu-id="da582-198">All of the method that are marked with the **TestMethod** attribute will be tested.</span></span> <span data-ttu-id="da582-199">**[テスト]** メニュー項目から、テストを実行します。</span><span class="sxs-lookup"><span data-stu-id="da582-199">From the **Test** menu item, run the tests.</span></span>

![テストの実行](unit-testing-with-aspnet-web-api/_static/image11.png)

<span data-ttu-id="da582-201">**[テストエクスプローラー]** ウィンドウを開き、テストの結果を確認します。</span><span class="sxs-lookup"><span data-stu-id="da582-201">Open the **Test Explorer** window, and notice the results of the tests.</span></span>

![テスト結果](unit-testing-with-aspnet-web-api/_static/image12.png)

## <a name="summary"></a><span data-ttu-id="da582-203">まとめ</span><span class="sxs-lookup"><span data-stu-id="da582-203">Summary</span></span>

<span data-ttu-id="da582-204">これで、このチュートリアルが完了しました。</span><span class="sxs-lookup"><span data-stu-id="da582-204">You have completed this tutorial.</span></span> <span data-ttu-id="da582-205">このチュートリアルのデータは、単体テストの条件に焦点を当てるために意図的に簡略化されています。</span><span class="sxs-lookup"><span data-stu-id="da582-205">The data in this tutorial was intentionally simplified to focus on unit testing conditions.</span></span> <span data-ttu-id="da582-206">より高度なデータシナリオの単体テストについては、「[単体テスト ASP.NET Web API 2](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md)」の「モック Entity Framework」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="da582-206">For unit testing more advanced data scenarios, see [Mocking Entity Framework when Unit Testing ASP.NET Web API 2](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md).</span></span>
