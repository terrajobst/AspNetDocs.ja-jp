---
uid: web-api/overview/testing-and-debugging/mocking-entity-framework-when-unit-testing-aspnet-web-api-2
title: 単体テスト ASP.NET Web API 2 | のモック Entity FrameworkMicrosoft Docs
author: Rick-Anderson
description: このガイドとアプリケーションでは、Entity Framework を使用する Web API 2 アプリケーションの単体テストを作成する方法を示します。 変更する方法を示しています...
ms.author: riande
ms.date: 12/13/2013
ms.assetid: cd844025-ccad-41ce-8694-595f1022a49f
msc.legacyurl: /web-api/overview/testing-and-debugging/mocking-entity-framework-when-unit-testing-aspnet-web-api-2
msc.type: authoredcontent
ms.openlocfilehash: 258450107ee7443c4efd43a3b8e4851249745227
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78447088"
---
# <a name="mocking-entity-framework-when-unit-testing-aspnet-web-api-2"></a><span data-ttu-id="cfbbc-104">単体テスト時のモック Entity Framework ASP.NET Web API 2</span><span class="sxs-lookup"><span data-stu-id="cfbbc-104">Mocking Entity Framework when Unit Testing ASP.NET Web API 2</span></span>

<span data-ttu-id="cfbbc-105">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="cfbbc-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[<span data-ttu-id="cfbbc-106">完成したプロジェクトのダウンロード</span><span class="sxs-lookup"><span data-stu-id="cfbbc-106">Download Completed Project</span></span>](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11)

> <span data-ttu-id="cfbbc-107">このガイドとアプリケーションでは、Entity Framework を使用する Web API 2 アプリケーションの単体テストを作成する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="cfbbc-107">This guidance and application demonstrate how to create unit tests for your Web API 2 application that uses the Entity Framework.</span></span> <span data-ttu-id="cfbbc-108">スキャフォールディングコントローラーを変更して、テスト用のコンテキストオブジェクトを渡すことができるようにする方法と、Entity Framework で使用するテストオブジェクトを作成する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="cfbbc-108">It shows how to modify the scaffolded controller to enable passing a context object for testing, and how to create test objects that work with Entity Framework.</span></span>
>
> <span data-ttu-id="cfbbc-109">ASP.NET Web API を使用した単体テストの概要については、「 [ASP.NET Web API 2 を使用した単体](unit-testing-with-aspnet-web-api.md)テスト」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="cfbbc-109">For an introduction to unit testing with ASP.NET Web API, see [Unit Testing with ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md).</span></span>
>
> <span data-ttu-id="cfbbc-110">このチュートリアルでは、ASP.NET Web API の基本的な概念を理解していることを前提としています。</span><span class="sxs-lookup"><span data-stu-id="cfbbc-110">This tutorial assumes you are familiar with the basic concepts of ASP.NET Web API.</span></span> <span data-ttu-id="cfbbc-111">入門用のチュートリアルについては、「 [ASP.NET Web API 2 を使用したはじめに](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="cfbbc-111">For an introductory tutorial, see [Getting Started with ASP.NET Web API 2](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md).</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="cfbbc-112">このチュートリアルで使用されているソフトウェアのバージョン</span><span class="sxs-lookup"><span data-stu-id="cfbbc-112">Software versions used in the tutorial</span></span>
>
> - [<span data-ttu-id="cfbbc-113">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="cfbbc-113">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
> - <span data-ttu-id="cfbbc-114">Web API 2</span><span class="sxs-lookup"><span data-stu-id="cfbbc-114">Web API 2</span></span>

## <a name="in-this-topic"></a><span data-ttu-id="cfbbc-115">このトピックの内容</span><span class="sxs-lookup"><span data-stu-id="cfbbc-115">In this topic</span></span>

<span data-ttu-id="cfbbc-116">このトピックには、次のセクションが含まれます。</span><span class="sxs-lookup"><span data-stu-id="cfbbc-116">This topic contains the following sections:</span></span>

- [<span data-ttu-id="cfbbc-117">前提条件</span><span class="sxs-lookup"><span data-stu-id="cfbbc-117">Prerequisites</span></span>](#prereqs)
- [<span data-ttu-id="cfbbc-118">コードのダウンロード</span><span class="sxs-lookup"><span data-stu-id="cfbbc-118">Download code</span></span>](#download)
- [<span data-ttu-id="cfbbc-119">単体テストプロジェクトを使用したアプリケーションの作成</span><span class="sxs-lookup"><span data-stu-id="cfbbc-119">Create application with unit test project</span></span>](#appwithunittest)
- [<span data-ttu-id="cfbbc-120">モデルクラスを作成する</span><span class="sxs-lookup"><span data-stu-id="cfbbc-120">Create the model class</span></span>](#modelclass)
- [<span data-ttu-id="cfbbc-121">コントローラーの追加</span><span class="sxs-lookup"><span data-stu-id="cfbbc-121">Add the controller</span></span>](#controller)
- [<span data-ttu-id="cfbbc-122">依存関係の挿入の追加</span><span class="sxs-lookup"><span data-stu-id="cfbbc-122">Add dependency injection</span></span>](#dependency)
- [<span data-ttu-id="cfbbc-123">テストプロジェクトに NuGet パッケージをインストールする</span><span class="sxs-lookup"><span data-stu-id="cfbbc-123">Install NuGet packages in test project</span></span>](#testpackages)
- [<span data-ttu-id="cfbbc-124">テストコンテキストの作成</span><span class="sxs-lookup"><span data-stu-id="cfbbc-124">Create test context</span></span>](#testcontext)
- [<span data-ttu-id="cfbbc-125">テストの作成</span><span class="sxs-lookup"><span data-stu-id="cfbbc-125">Create tests</span></span>](#tests)
- [<span data-ttu-id="cfbbc-126">テストの実行</span><span class="sxs-lookup"><span data-stu-id="cfbbc-126">Run tests</span></span>](#runtests)

<span data-ttu-id="cfbbc-127">[ASP.NET Web API 2 での単体テスト](unit-testing-with-aspnet-web-api.md)の手順を既に完了している場合は、「[コントローラーを追加](#controller)する」のセクションに進んでください。</span><span class="sxs-lookup"><span data-stu-id="cfbbc-127">If you have already completed the steps in [Unit Testing with ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md), you can skip to the section [Add the controller](#controller).</span></span>

<a id="prereqs"></a>
## <a name="prerequisites"></a><span data-ttu-id="cfbbc-128">前提条件</span><span class="sxs-lookup"><span data-stu-id="cfbbc-128">Prerequisites</span></span>

<span data-ttu-id="cfbbc-129">Visual Studio 2017 Community、Professional、または Enterprise edition</span><span class="sxs-lookup"><span data-stu-id="cfbbc-129">Visual Studio 2017 Community, Professional or Enterprise edition</span></span>

<a id="download"></a>
## <a name="download-code"></a><span data-ttu-id="cfbbc-130">コードをダウンロードする</span><span class="sxs-lookup"><span data-stu-id="cfbbc-130">Download code</span></span>

<span data-ttu-id="cfbbc-131">完成し[たプロジェクト](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11)をダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="cfbbc-131">Download the [completed project](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11).</span></span> <span data-ttu-id="cfbbc-132">ダウンロード可能なプロジェクトには、このトピックの単体テストコードと[単体テスト ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md)のトピックが含まれています。</span><span class="sxs-lookup"><span data-stu-id="cfbbc-132">The downloadable project includes unit test code for this topic and for the [Unit Testing ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md) topic.</span></span>

<a id="appwithunittest"></a>
## <a name="create-application-with-unit-test-project"></a><span data-ttu-id="cfbbc-133">単体テストプロジェクトを使用したアプリケーションの作成</span><span class="sxs-lookup"><span data-stu-id="cfbbc-133">Create application with unit test project</span></span>

<span data-ttu-id="cfbbc-134">アプリケーションを作成するとき、または既存のアプリケーションに単体テストプロジェクトを追加するときに、単体テストプロジェクトを作成することができます。</span><span class="sxs-lookup"><span data-stu-id="cfbbc-134">You can either create a unit test project when creating your application or add a unit test project to an existing application.</span></span> <span data-ttu-id="cfbbc-135">このチュートリアルでは、アプリケーションの作成時に単体テストプロジェクトを作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="cfbbc-135">This tutorial shows creating a unit test project when creating the application.</span></span>

<span data-ttu-id="cfbbc-136">**Storeapp**という名前の新しい ASP.NET Web アプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="cfbbc-136">Create a new ASP.NET Web Application named **StoreApp**.</span></span>

<span data-ttu-id="cfbbc-137">New ASP.NET プロジェクトウィンドウで、**空**のテンプレートを選択し、Web API のフォルダーとコア参照を追加します。</span><span class="sxs-lookup"><span data-stu-id="cfbbc-137">In the New ASP.NET Project windows, select the **Empty** template and add folders and core references for Web API.</span></span> <span data-ttu-id="cfbbc-138">**[単体テストの追加]** オプションを選択します。</span><span class="sxs-lookup"><span data-stu-id="cfbbc-138">Select the **Add unit tests** option.</span></span> <span data-ttu-id="cfbbc-139">単体テストプロジェクトには、 **Storeapp.** test という名前が自動的に付けられます。</span><span class="sxs-lookup"><span data-stu-id="cfbbc-139">The unit test project is automatically named **StoreApp.Tests**.</span></span> <span data-ttu-id="cfbbc-140">この名前をそのまま使用できます。</span><span class="sxs-lookup"><span data-stu-id="cfbbc-140">You can keep this name.</span></span>

![単体テストプロジェクトの作成](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image1.png)

<span data-ttu-id="cfbbc-142">アプリケーションを作成した後、2つのプロジェクトが含まれていることがわかります ( **storeapp**と**Storeapp. テスト**)。</span><span class="sxs-lookup"><span data-stu-id="cfbbc-142">After creating the application, you will see it contains two projects - **StoreApp** and **StoreApp.Tests**.</span></span>

<a id="modelclass"></a>
## <a name="create-the-model-class"></a><span data-ttu-id="cfbbc-143">モデルクラスを作成する</span><span class="sxs-lookup"><span data-stu-id="cfbbc-143">Create the model class</span></span>

<span data-ttu-id="cfbbc-144">StoreApp プロジェクトで、 **Product.cs**という名前の**モデル**フォルダーにクラスファイルを追加します。</span><span class="sxs-lookup"><span data-stu-id="cfbbc-144">In your StoreApp project, add a class file to the **Models** folder named **Product.cs**.</span></span> <span data-ttu-id="cfbbc-145">このファイルの内容を次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="cfbbc-145">Replace the contents of the file with the following code.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample1.cs)]

<span data-ttu-id="cfbbc-146">ソリューションをビルドします。</span><span class="sxs-lookup"><span data-stu-id="cfbbc-146">Build the solution.</span></span>

<a id="controller"></a>
## <a name="add-the-controller"></a><span data-ttu-id="cfbbc-147">コントローラーの追加</span><span class="sxs-lookup"><span data-stu-id="cfbbc-147">Add the controller</span></span>

<span data-ttu-id="cfbbc-148">Controllers フォルダーを右クリックし、 **[追加]** 、 **[新しいスキャフォールディング項目]** の順に選択します。</span><span class="sxs-lookup"><span data-stu-id="cfbbc-148">Right-click the Controllers folder and select **Add** and **New Scaffolded Item**.</span></span> <span data-ttu-id="cfbbc-149">Entity Framework を使用して、アクションがある Web API 2 コントローラーを選択します。</span><span class="sxs-lookup"><span data-stu-id="cfbbc-149">Select Web API 2 Controller with actions, using Entity Framework.</span></span>

![新しいコントローラーの追加](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image2.png)

<span data-ttu-id="cfbbc-151">次の値を設定します。</span><span class="sxs-lookup"><span data-stu-id="cfbbc-151">Set the following values:</span></span>

- <span data-ttu-id="cfbbc-152">コントローラー名: **Productcontroller**</span><span class="sxs-lookup"><span data-stu-id="cfbbc-152">Controller name: **ProductController**</span></span>
- <span data-ttu-id="cfbbc-153">モデルクラス: **Product**</span><span class="sxs-lookup"><span data-stu-id="cfbbc-153">Model class: **Product**</span></span>
- <span data-ttu-id="cfbbc-154">データコンテキストクラス: [**新しいデータコンテキスト**を選択] をクリックすると、以下の値が表示されます。</span><span class="sxs-lookup"><span data-stu-id="cfbbc-154">Data context class: [Select **New data context** button which fills in the values seen below]</span></span>

![コントローラーの指定](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image3.png)

<span data-ttu-id="cfbbc-156">自動的に生成されたコードを使用してコントローラーを作成するには、 **[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="cfbbc-156">Click **Add** to create the controller with automatically-generated code.</span></span> <span data-ttu-id="cfbbc-157">このコードには、Product クラスのインスタンスを作成、取得、更新、および削除するメソッドが含まれています。</span><span class="sxs-lookup"><span data-stu-id="cfbbc-157">The code includes methods for creating, retrieving, updating and deleting instances of the Product class.</span></span> <span data-ttu-id="cfbbc-158">次のコードは、製品を追加する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="cfbbc-158">The following code shows the method for add a Product.</span></span> <span data-ttu-id="cfbbc-159">メソッドが**Ihttpactionresult**のインスタンスを返すことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="cfbbc-159">Notice that the method returns an instance of **IHttpActionResult**.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample2.cs)]

<span data-ttu-id="cfbbc-160">IHttpActionResult は、Web API 2 の新機能の1つであり、単体テストの開発を簡略化します。</span><span class="sxs-lookup"><span data-stu-id="cfbbc-160">IHttpActionResult is one of the new features in Web API 2, and it simplifies unit test development.</span></span>

<span data-ttu-id="cfbbc-161">次のセクションでは、生成されたコードをカスタマイズして、テストオブジェクトをコントローラーに渡すのを容易にします。</span><span class="sxs-lookup"><span data-stu-id="cfbbc-161">In the next section, you will customize the generated code to facilitate passing test objects to the controller.</span></span>

<a id="dependency"></a>
## <a name="add-dependency-injection"></a><span data-ttu-id="cfbbc-162">依存関係の挿入の追加</span><span class="sxs-lookup"><span data-stu-id="cfbbc-162">Add dependency injection</span></span>

<span data-ttu-id="cfbbc-163">現在、ProductController クラスは、StoreAppContext クラスのインスタンスを使用するようにハードコーディングされています。</span><span class="sxs-lookup"><span data-stu-id="cfbbc-163">Currently, the ProductController class is hard-coded to use an instance of the StoreAppContext class.</span></span> <span data-ttu-id="cfbbc-164">依存関係の注入と呼ばれるパターンを使用して、アプリケーションを変更し、ハードコーディングされた依存関係を削除します。</span><span class="sxs-lookup"><span data-stu-id="cfbbc-164">You will use a pattern called dependency injection to modify your application and remove that hard-coded dependency.</span></span> <span data-ttu-id="cfbbc-165">この依存関係を分割することにより、テスト時にモックオブジェクトを渡すことができます。</span><span class="sxs-lookup"><span data-stu-id="cfbbc-165">By breaking this dependency, you can pass in a mock object when testing.</span></span>

<span data-ttu-id="cfbbc-166">**[モデル]** フォルダーを右クリックし、 **Istoreappcontext**という名前の新しいインターフェイスを追加します。</span><span class="sxs-lookup"><span data-stu-id="cfbbc-166">Right-click the **Models** folder, and add a new interface named **IStoreAppContext**.</span></span>

<span data-ttu-id="cfbbc-167">このコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="cfbbc-167">Replace the code with the following code.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample3.cs)]

<span data-ttu-id="cfbbc-168">StoreAppContext.cs ファイルを開き、次の強調表示された変更を行います。</span><span class="sxs-lookup"><span data-stu-id="cfbbc-168">Open the StoreAppContext.cs file and make the following highlighted changes.</span></span> <span data-ttu-id="cfbbc-169">注意すべき重要な変更点は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="cfbbc-169">The important changes to note are:</span></span>

- <span data-ttu-id="cfbbc-170">StoreAppContext クラスは IStoreAppContext インターフェイスを実装します</span><span class="sxs-lookup"><span data-stu-id="cfbbc-170">StoreAppContext class implements IStoreAppContext interface</span></span>
- <span data-ttu-id="cfbbc-171">MarkAsModified メソッドが実装されています</span><span class="sxs-lookup"><span data-stu-id="cfbbc-171">MarkAsModified method is implemented</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample4.cs?highlight=6,14-17)]

<span data-ttu-id="cfbbc-172">ProductController.cs ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="cfbbc-172">Open the ProductController.cs file.</span></span> <span data-ttu-id="cfbbc-173">強調表示されたコードに一致するように既存のコードを変更します。</span><span class="sxs-lookup"><span data-stu-id="cfbbc-173">Change the existing code to match the highlighted code.</span></span> <span data-ttu-id="cfbbc-174">これらの変更により、StoreAppContext の依存関係が解除され、他のクラスがコンテキストクラスの別のオブジェクトを渡すことができるようになります。</span><span class="sxs-lookup"><span data-stu-id="cfbbc-174">These changes break the dependency on StoreAppContext and enable other classes to pass in a different object for the context class.</span></span> <span data-ttu-id="cfbbc-175">この変更により、単体テスト中にテストコンテキストを渡すことができます。</span><span class="sxs-lookup"><span data-stu-id="cfbbc-175">This change will enable you to pass in a test context during unit tests.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample5.cs?highlight=4,7-12)]

<span data-ttu-id="cfbbc-176">ProductController でもう1つの変更を行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="cfbbc-176">There is one more change you must make in ProductController.</span></span> <span data-ttu-id="cfbbc-177">**Putproduct**メソッドで、エンティティの状態を設定する行を MarkAsModified メソッドの呼び出しに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="cfbbc-177">In the **PutProduct** method, replace the line that sets the entity state to modified with a call to the MarkAsModified method.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample6.cs?highlight=14-15)]

<span data-ttu-id="cfbbc-178">ソリューションをビルドします。</span><span class="sxs-lookup"><span data-stu-id="cfbbc-178">Build the solution.</span></span>

<span data-ttu-id="cfbbc-179">これで、テストプロジェクトを設定する準備ができました。</span><span class="sxs-lookup"><span data-stu-id="cfbbc-179">You are now ready to set up the test project.</span></span>

<a id="testpackages"></a>
## <a name="install-nuget-packages-in-test-project"></a><span data-ttu-id="cfbbc-180">テストプロジェクトに NuGet パッケージをインストールする</span><span class="sxs-lookup"><span data-stu-id="cfbbc-180">Install NuGet packages in test project</span></span>

<span data-ttu-id="cfbbc-181">空のテンプレートを使用してアプリケーションを作成する場合、単体テストプロジェクト (StoreApp. Tests) には、インストールされている NuGet パッケージは含まれません。</span><span class="sxs-lookup"><span data-stu-id="cfbbc-181">When you use the Empty template to create an application, the unit test project (StoreApp.Tests) does not include any installed NuGet packages.</span></span> <span data-ttu-id="cfbbc-182">Web API テンプレートなどの他のテンプレートには、単体テストプロジェクトにいくつかの NuGet パッケージが含まれています。</span><span class="sxs-lookup"><span data-stu-id="cfbbc-182">Other templates, such as the Web API template, include some NuGet packages in the unit test project.</span></span> <span data-ttu-id="cfbbc-183">このチュートリアルでは、Entity Framework パッケージと Microsoft ASP.NET Web API 2 コアパッケージをテストプロジェクトに含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="cfbbc-183">For this tutorial, you must include the Entity Framework package and the Microsoft ASP.NET Web API 2 Core package to the test project.</span></span>

<span data-ttu-id="cfbbc-184">StoreApp. Tests プロジェクトを右クリックし、 **[NuGet パッケージの管理]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="cfbbc-184">Right-click the StoreApp.Tests project and select **Manage NuGet Packages**.</span></span> <span data-ttu-id="cfbbc-185">パッケージをプロジェクトに追加するには、StoreApp. Tests プロジェクトを選択する必要があります。</span><span class="sxs-lookup"><span data-stu-id="cfbbc-185">You must select the StoreApp.Tests project to add the packages to that project.</span></span>

![パッケージの管理](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image4.png)

<span data-ttu-id="cfbbc-187">オンラインパッケージから EntityFramework パッケージ (バージョン6.0 以降) を検索してインストールします。</span><span class="sxs-lookup"><span data-stu-id="cfbbc-187">From the Online packages, find and install the EntityFramework package (version 6.0 or later).</span></span> <span data-ttu-id="cfbbc-188">EntityFramework パッケージが既にインストールされている場合は、StoreApp. Tests プロジェクトではなく StoreApp プロジェクトを選択している可能性があります。</span><span class="sxs-lookup"><span data-stu-id="cfbbc-188">If it appears that the EntityFramework package is already installed, you may have selected the StoreApp project instead of the StoreApp.Tests project.</span></span>

![Entity Framework の追加](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image5.png)

<span data-ttu-id="cfbbc-190">Microsoft ASP.NET Web API 2 コアパッケージを検索してインストールします。</span><span class="sxs-lookup"><span data-stu-id="cfbbc-190">Find and install Microsoft ASP.NET Web API 2 Core package.</span></span>

![web api core パッケージのインストール](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image6.png)

<span data-ttu-id="cfbbc-192">[NuGet パッケージの管理] ウィンドウを閉じます。</span><span class="sxs-lookup"><span data-stu-id="cfbbc-192">Close the Manage NuGet Packages window.</span></span>

<a id="testcontext"></a>
## <a name="create-test-context"></a><span data-ttu-id="cfbbc-193">テストコンテキストの作成</span><span class="sxs-lookup"><span data-stu-id="cfbbc-193">Create test context</span></span>

<span data-ttu-id="cfbbc-194">**Testdbset**という名前のクラスをテストプロジェクトに追加します。</span><span class="sxs-lookup"><span data-stu-id="cfbbc-194">Add a class named **TestDbSet** to the test project.</span></span> <span data-ttu-id="cfbbc-195">このクラスは、テストデータセットの基本クラスとして機能します。</span><span class="sxs-lookup"><span data-stu-id="cfbbc-195">This class serves as the base class for your test data set.</span></span> <span data-ttu-id="cfbbc-196">このコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="cfbbc-196">Replace the code with the following code.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample7.cs)]

<span data-ttu-id="cfbbc-197">**Testproductdbset**という名前のクラスをテストプロジェクトに追加します。このクラスには、次のコードが含まれています。</span><span class="sxs-lookup"><span data-stu-id="cfbbc-197">Add a class named **TestProductDbSet** to the test project which contains the following code.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample8.cs)]

<span data-ttu-id="cfbbc-198">**Teststoreappcontext**という名前のクラスを追加し、既存のコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="cfbbc-198">Add a class named **TestStoreAppContext** and replace the existing code with the following code.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample9.cs)]

<a id="tests"></a>
## <a name="create-tests"></a><span data-ttu-id="cfbbc-199">テストの作成</span><span class="sxs-lookup"><span data-stu-id="cfbbc-199">Create tests</span></span>

<span data-ttu-id="cfbbc-200">既定では、テストプロジェクトには、 **UnitTest1.cs**という名前の空のテストファイルが含まれています。</span><span class="sxs-lookup"><span data-stu-id="cfbbc-200">By default, your test project includes an empty test file named **UnitTest1.cs**.</span></span> <span data-ttu-id="cfbbc-201">このファイルには、テストメソッドの作成に使用する属性が表示されます。</span><span class="sxs-lookup"><span data-stu-id="cfbbc-201">This file shows the attributes you use to create test methods.</span></span> <span data-ttu-id="cfbbc-202">このチュートリアルでは、新しいテストクラスを追加するため、このファイルを削除できます。</span><span class="sxs-lookup"><span data-stu-id="cfbbc-202">For this tutorial, you can delete this file because you will add a new test class.</span></span>

<span data-ttu-id="cfbbc-203">**Testproductcontroller**という名前のクラスをテストプロジェクトに追加します。</span><span class="sxs-lookup"><span data-stu-id="cfbbc-203">Add a class named **TestProductController** to the test project.</span></span> <span data-ttu-id="cfbbc-204">このコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="cfbbc-204">Replace the code with the following code.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample10.cs)]

<a id="runtests"></a>
## <a name="run-tests"></a><span data-ttu-id="cfbbc-205">テストの実行</span><span class="sxs-lookup"><span data-stu-id="cfbbc-205">Run tests</span></span>

<span data-ttu-id="cfbbc-206">これで、テストを実行する準備が整いました。</span><span class="sxs-lookup"><span data-stu-id="cfbbc-206">You are now ready to run the tests.</span></span> <span data-ttu-id="cfbbc-207">"完了 **" 属性で**マークされているすべてのメソッドがテストされます。</span><span class="sxs-lookup"><span data-stu-id="cfbbc-207">All of the method that are marked with the **TestMethod** attribute will be tested.</span></span> <span data-ttu-id="cfbbc-208">**[テスト]** メニュー項目から、テストを実行します。</span><span class="sxs-lookup"><span data-stu-id="cfbbc-208">From the **Test** menu item, run the tests.</span></span>

![テストの実行](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image7.png)

<span data-ttu-id="cfbbc-210">**[テストエクスプローラー]** ウィンドウを開き、テストの結果を確認します。</span><span class="sxs-lookup"><span data-stu-id="cfbbc-210">Open the **Test Explorer** window, and notice the results of the tests.</span></span>

![テスト結果](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image8.png)
