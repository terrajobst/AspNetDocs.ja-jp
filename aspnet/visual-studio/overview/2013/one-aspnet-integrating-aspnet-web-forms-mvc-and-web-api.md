---
uid: visual-studio/overview/2013/one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api
title: 'ハンズオンラボ: One ASP.NET: ASP.NET Web フォーム、MVC、Web API の統合 |Microsoft Docs'
author: rick-anderson
description: ASP.NET は、MVC、Web API などの特殊なテクノロジを使用して、Web サイト、アプリ、サービスを構築するためのフレームワークです。 拡張 ASP.NET...
ms.author: riande
ms.date: 07/16/2014
ms.assetid: 4fe2558d-67cc-4d12-a5c1-6fb9f6f16137
msc.legacyurl: /visual-studio/overview/2013/one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api
msc.type: authoredcontent
ms.openlocfilehash: 165d104b5d3ef3281af449cc8673ad96f531d628
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78505456"
---
# <a name="hands-on-lab-one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api"></a><span data-ttu-id="1a117-104">ハンズオンラボ: One ASP.NET: ASP.NET Web フォーム、MVC、Web API の統合</span><span class="sxs-lookup"><span data-stu-id="1a117-104">Hands On Lab: One ASP.NET: Integrating ASP.NET Web Forms, MVC and Web API</span></span>

<span data-ttu-id="1a117-105">[Web キャンプチーム](https://twitter.com/webcamps)別</span><span class="sxs-lookup"><span data-stu-id="1a117-105">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="1a117-106">Web キャンプトレーニングキットをダウンロードする</span><span class="sxs-lookup"><span data-stu-id="1a117-106">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

> <span data-ttu-id="1a117-107">ASP.NET は、MVC、Web API などの特殊なテクノロジを使用して、Web サイト、アプリ、サービスを構築するためのフレームワークです。</span><span class="sxs-lookup"><span data-stu-id="1a117-107">ASP.NET is a framework for building Web sites, apps and services using specialized technologies such as MVC, Web API and others.</span></span> <span data-ttu-id="1a117-108">拡張 ASP.NET が作成されてから、このようなテクノロジを統合する必要があることがわかったので、 **1 つの ASP.NET**に向けた最近の取り組みが行われています。</span><span class="sxs-lookup"><span data-stu-id="1a117-108">With the expansion ASP.NET has seen since its creation and the expressed need to have these technologies integrated, there have been recent efforts in working towards **One ASP.NET**.</span></span>
> 
> <span data-ttu-id="1a117-109">Visual Studio 2013 には、アプリケーションをビルドし、すべての ASP.NET テクノロジを1つのプロジェクトで使用できる新しい統合プロジェクトシステムが導入されています。</span><span class="sxs-lookup"><span data-stu-id="1a117-109">Visual Studio 2013 introduces a new unified project system which lets you build an application and use all the ASP.NET technologies in one project.</span></span> <span data-ttu-id="1a117-110">この機能により、プロジェクトの開始時に1つのテクノロジを選択する必要がなくなり、1つのプロジェクト内で複数の ASP.NET フレームワークを使用することが促進されます。</span><span class="sxs-lookup"><span data-stu-id="1a117-110">This feature eliminates the need to pick one technology at the start of a project and stick with it, and instead encourages the use of multiple ASP.NET frameworks within one project.</span></span>
> 
> <span data-ttu-id="1a117-111">すべてのサンプルコードとスニペットは、 [https://aka.ms/webcamps-training-kit](https://aka.ms/webcamps-training-kit)で入手できる Web キャンプトレーニングキットに含まれています。</span><span class="sxs-lookup"><span data-stu-id="1a117-111">All sample code and snippets are included in the Web Camps Training Kit, available at [https://aka.ms/webcamps-training-kit](https://aka.ms/webcamps-training-kit).</span></span>

<a id="Overview"></a>
## <a name="overview"></a><span data-ttu-id="1a117-112">概要</span><span class="sxs-lookup"><span data-stu-id="1a117-112">Overview</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="1a117-113">目標</span><span class="sxs-lookup"><span data-stu-id="1a117-113">Objectives</span></span>

<span data-ttu-id="1a117-114">このハンズオンラボでは、次の方法を学習します。</span><span class="sxs-lookup"><span data-stu-id="1a117-114">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="1a117-115">**1 つの ASP.NET**プロジェクトの種類に基づいて Web サイトを作成する</span><span class="sxs-lookup"><span data-stu-id="1a117-115">Create a Web site based on the **One ASP.NET** project type</span></span>
- <span data-ttu-id="1a117-116">**MVC**や**Web API**などのさまざまな**ASP.NET**フレームワークを同じプロジェクトで使用する</span><span class="sxs-lookup"><span data-stu-id="1a117-116">Use different **ASP.NET** frameworks like **MVC** and **Web API** in the same project</span></span>
- <span data-ttu-id="1a117-117">**ASP.NET**アプリケーションの主要なコンポーネントを特定する</span><span class="sxs-lookup"><span data-stu-id="1a117-117">Identify the main components of an **ASP.NET** application</span></span>
- <span data-ttu-id="1a117-118">**ASP.NET スキャフォールディング**フレームワークを活用して、モデルクラスに基づいて CRUD 操作を実行するコントローラーとビューを自動的に作成します。</span><span class="sxs-lookup"><span data-stu-id="1a117-118">Take advantage of the **ASP.NET Scaffolding** framework to automatically create Controllers and Views to perform CRUD operations based on your model classes</span></span>
- <span data-ttu-id="1a117-119">ジョブごとに適切なツールを使用して、コンピューターとユーザーが判読できる形式で同じ情報のセットを公開します。</span><span class="sxs-lookup"><span data-stu-id="1a117-119">Expose the same set of information in machine- and human-readable formats using the right tool for each job</span></span>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="1a117-120">前提条件</span><span class="sxs-lookup"><span data-stu-id="1a117-120">Prerequisites</span></span>

<span data-ttu-id="1a117-121">このハンズオンラボを完了するには、次のものが必要です。</span><span class="sxs-lookup"><span data-stu-id="1a117-121">The following is required to complete this hands-on lab:</span></span>

- <span data-ttu-id="1a117-122">[Web 用に2013を Visual Studio Express](https://www.microsoft.com/visualstudio/)</span><span class="sxs-lookup"><span data-stu-id="1a117-122">[Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/) or greater</span></span>
- [<span data-ttu-id="1a117-123">Visual Studio 2013 Update 1</span><span class="sxs-lookup"><span data-stu-id="1a117-123">Visual Studio 2013 Update 1</span></span>](https://go.microsoft.com/fwlink/?LinkId=301714)

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="1a117-124">セットアップ</span><span class="sxs-lookup"><span data-stu-id="1a117-124">Setup</span></span>

<span data-ttu-id="1a117-125">このハンズオンラボの演習を実行するには、まず環境をセットアップする必要があります。</span><span class="sxs-lookup"><span data-stu-id="1a117-125">In order to run the exercises in this hands-on lab, you will need to set up your environment first.</span></span>

1. <span data-ttu-id="1a117-126">エクスプローラーを開き、ラボの**ソース**フォルダーを参照します。</span><span class="sxs-lookup"><span data-stu-id="1a117-126">Open Windows Explorer and browse to the lab's **Source** folder.</span></span>
2. <span data-ttu-id="1a117-127">**Setup.exe**を右クリックし、 **[管理者として実行]** を選択して、環境を構成し、このラボ用の Visual Studio コードスニペットをインストールするセットアッププロセスを開始します。</span><span class="sxs-lookup"><span data-stu-id="1a117-127">Right-click on **Setup.cmd** and select **Run as administrator** to launch the setup process that will configure your environment and install the Visual Studio code snippets for this lab.</span></span>
3. <span data-ttu-id="1a117-128">ユーザー アカウント制御ダイアログ ボックスが表示されている場合は、続行するアクションを確認します。</span><span class="sxs-lookup"><span data-stu-id="1a117-128">If the User Account Control dialog box is shown, confirm the action to proceed.</span></span>

> [!NOTE]
> <span data-ttu-id="1a117-129">セットアップを実行する前に、このラボのすべての依存関係を確認していることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="1a117-129">Make sure you have checked all the dependencies for this lab before running the setup.</span></span>

<a id="CodeSnippets"></a>
### <a name="using-the-code-snippets"></a><span data-ttu-id="1a117-130">コードスニペットの使用</span><span class="sxs-lookup"><span data-stu-id="1a117-130">Using the Code Snippets</span></span>

<span data-ttu-id="1a117-131">ラボドキュメント全体で、コードブロックを挿入するように指示されます。</span><span class="sxs-lookup"><span data-stu-id="1a117-131">Throughout the lab document, you will be instructed to insert code blocks.</span></span> <span data-ttu-id="1a117-132">便宜上、このコードのほとんどは Visual Studio Code のスニペットとして提供されており、Visual Studio 2013 内からアクセスして、手動で追加する必要がないようにすることができます。</span><span class="sxs-lookup"><span data-stu-id="1a117-132">For your convenience, most of this code is provided as Visual Studio Code Snippets, which you can access from within Visual Studio 2013 to avoid having to add it manually.</span></span>

> [!NOTE]
> <span data-ttu-id="1a117-133">各演習には、演習の**Begin**フォルダーに配置された開始ソリューションが付属しています。これにより、各演習を別の手順に従って実行することができます。</span><span class="sxs-lookup"><span data-stu-id="1a117-133">Each exercise is accompanied by a starting solution located in the **Begin** folder of the exercise that allows you to follow each exercise independently of the others.</span></span> <span data-ttu-id="1a117-134">演習中に追加されたコードスニペットは、これらの開始ソリューションにはないため、演習を完了するまで機能しないことがあります。</span><span class="sxs-lookup"><span data-stu-id="1a117-134">Please be aware that the code snippets that are added during an exercise are missing from these starting solutions and may not work until you have completed the exercise.</span></span> <span data-ttu-id="1a117-135">演習用のソースコード内では、対応する演習の手順を完了した結果として得られるコードを使用して、Visual Studio ソリューションを含む**終了**フォルダーも検索します。</span><span class="sxs-lookup"><span data-stu-id="1a117-135">Inside the source code for an exercise, you will also find an **End** folder containing a Visual Studio solution with the code that results from completing the steps in the corresponding exercise.</span></span> <span data-ttu-id="1a117-136">このハンズオンラボを使用して作業する際に、追加のヘルプが必要な場合は、これらのソリューションをガイダンスとして使用できます。</span><span class="sxs-lookup"><span data-stu-id="1a117-136">You can use these solutions as guidance if you need additional help as you work through this hands-on lab.</span></span>

---

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="1a117-137">手順</span><span class="sxs-lookup"><span data-stu-id="1a117-137">Exercises</span></span>

<span data-ttu-id="1a117-138">このハンズオンラボには、次の演習が含まれています。</span><span class="sxs-lookup"><span data-stu-id="1a117-138">This hands-on lab includes the following exercises:</span></span>

1. [<span data-ttu-id="1a117-139">新しい Web フォームプロジェクトの作成</span><span class="sxs-lookup"><span data-stu-id="1a117-139">Creating a New Web Forms Project</span></span>](#Exercise1)
2. [<span data-ttu-id="1a117-140">スキャフォールディングを使用した MVC コントローラーの作成</span><span class="sxs-lookup"><span data-stu-id="1a117-140">Creating an MVC Controller Using Scaffolding</span></span>](#Exercise2)
3. [<span data-ttu-id="1a117-141">スキャフォールディングを使用した Web API コントローラーの作成</span><span class="sxs-lookup"><span data-stu-id="1a117-141">Creating a Web API Controller Using Scaffolding</span></span>](#Exercise3)

<span data-ttu-id="1a117-142">このラボの推定所要時間: **60 分**</span><span class="sxs-lookup"><span data-stu-id="1a117-142">Estimated time to complete this lab: **60 minutes**</span></span>

> [!NOTE]
> <span data-ttu-id="1a117-143">Visual Studio を初めて起動するときに、定義済みの設定コレクションのいずれかを選択する必要があります。</span><span class="sxs-lookup"><span data-stu-id="1a117-143">When you first start Visual Studio, you must select one of the predefined settings collections.</span></span> <span data-ttu-id="1a117-144">定義済みの各コレクションは、特定の開発スタイルに一致するように設計されており、ウィンドウのレイアウト、エディターの動作、IntelliSense コードスニペット、およびダイアログボックスのオプションを決定します。</span><span class="sxs-lookup"><span data-stu-id="1a117-144">Each predefined collection is designed to match a particular development style and determines window layouts, editor behavior, IntelliSense code snippets, and dialog box options.</span></span> <span data-ttu-id="1a117-145">このラボの手順では、**全般的な開発設定**のコレクションを使用するときに、Visual Studio で特定のタスクを実行するために必要なアクションについて説明します。</span><span class="sxs-lookup"><span data-stu-id="1a117-145">The procedures in this lab describe the actions necessary to accomplish a given task in Visual Studio when using the **General Development Settings** collection.</span></span> <span data-ttu-id="1a117-146">開発環境に対して別の設定コレクションを選択した場合は、注意が必要な手順が異なる場合があります。</span><span class="sxs-lookup"><span data-stu-id="1a117-146">If you choose a different settings collection for your development environment, there may be differences in the steps that you should take into account.</span></span>

<a id="Exercise1"></a>
### <a name="exercise-1-creating-a-new-web-forms-project"></a><span data-ttu-id="1a117-147">演習 1: 新しい Web フォームプロジェクトの作成</span><span class="sxs-lookup"><span data-stu-id="1a117-147">Exercise 1: Creating a New Web Forms Project</span></span>

<span data-ttu-id="1a117-148">この演習では、 **ASP.NET**統合プロジェクトのエクスペリエンスを使用して、Visual Studio 2013 に新しい web フォームサイトを作成します。これにより、web フォーム、MVC、および web API コンポーネントを同じアプリケーションに簡単に統合できます。</span><span class="sxs-lookup"><span data-stu-id="1a117-148">In this exercise you will create a new Web Forms site in Visual Studio 2013 using the **One ASP.NET** unified project experience, which will allow you to easily integrate Web Forms, MVC and Web API components in the same application.</span></span> <span data-ttu-id="1a117-149">次に、生成されたソリューションを調査し、その部分を特定します。最後に、Web サイトが動作していることを確認します。</span><span class="sxs-lookup"><span data-stu-id="1a117-149">You will then explore the generated solution and identify its parts, and finally you will see the Web site in action.</span></span>

<a id="Ex1Task1"></a>
#### <a name="task-1--creating-a-new-site-using-the-one-aspnet-experience"></a><span data-ttu-id="1a117-150">タスク 1-ASP.NET エクスペリエンスを1つ使用して新しいサイトを作成する</span><span class="sxs-lookup"><span data-stu-id="1a117-150">Task 1 – Creating a New Site Using the One ASP.NET Experience</span></span>

<span data-ttu-id="1a117-151">このタスクでは、 **1 つの ASP.NET**プロジェクトの種類に基づいて、Visual Studio で新しい Web サイトの作成を開始します。</span><span class="sxs-lookup"><span data-stu-id="1a117-151">In this task you will start creating a new Web site in Visual Studio based on the **One ASP.NET** project type.</span></span> <span data-ttu-id="1a117-152">**ASP.NET**は、すべての ASP.NET テクノロジを統合し、必要に応じてそれらを組み合わせて照合するオプションを提供します。</span><span class="sxs-lookup"><span data-stu-id="1a117-152">**One ASP.NET** unifies all ASP.NET technologies and gives you the option to mix and match them as desired.</span></span> <span data-ttu-id="1a117-153">次に、Web フォーム、MVC、Web API のさまざまなコンポーネントを、アプリケーション内で並行して認識します。</span><span class="sxs-lookup"><span data-stu-id="1a117-153">You will then recognize the different components of Web Forms, MVC and Web API that live side by side within your application.</span></span>

1. <span data-ttu-id="1a117-154">**Web 用 Visual Studio Express 2013**を開き、[ファイル] を選択します。 **新しいプロジェクト...** を実行すると、新しいソリューションが開始されます。</span><span class="sxs-lookup"><span data-stu-id="1a117-154">Open **Visual Studio Express 2013 for Web** and select **File | New Project...** to start a new solution.</span></span>

    ![新規プロジェクトの作成](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image1.png)

    <span data-ttu-id="1a117-156">*新しいプロジェクトの作成*</span><span class="sxs-lookup"><span data-stu-id="1a117-156">*Creating a New Project*</span></span>
2. <span data-ttu-id="1a117-157">**[新しいプロジェクト]** ダイアログボックスで、Visual  **C# | の下にある [ASP.NET Web Application] を選択します。[Web** ] タブで、 **.NET Framework 4.5**が選択されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="1a117-157">In the **New Project** dialog box, select **ASP.NET Web Application** under the **Visual C# | Web** tab, and make sure **.NET Framework 4.5** is selected.</span></span> <span data-ttu-id="1a117-158">プロジェクトに*MyHybridSite*という名前を指定し、**場所**を選択して [ **OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="1a117-158">Name the project *MyHybridSite*, choose a **Location** and click **OK**.</span></span>

    ![新しい ASP.NET Web アプリケーションプロジェクト](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image2.png)

    <span data-ttu-id="1a117-160">*新しい ASP.NET Web アプリケーションプロジェクトの作成*</span><span class="sxs-lookup"><span data-stu-id="1a117-160">*Creating a new ASP.NET Web Application project*</span></span>
3. <span data-ttu-id="1a117-161">**[New ASP.NET プロジェクト]** ダイアログボックスで、 **[Web フォーム]** テンプレートを選択し、 **[MVC]** オプションと **[web API]** オプションを選択します。</span><span class="sxs-lookup"><span data-stu-id="1a117-161">In the **New ASP.NET Project** dialog box, select the **Web Forms** template and select the **MVC** and **Web API** options.</span></span> <span data-ttu-id="1a117-162">また、**認証**オプションが**個々のユーザーアカウント**に設定されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="1a117-162">Also, make sure that the **Authentication** option is set to **Individual User Accounts**.</span></span> <span data-ttu-id="1a117-163">続行するには、 **[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="1a117-163">Click **OK** to continue.</span></span>

    ![Web API と MVC コンポーネントを含む、Web フォームテンプレートを使用した新しいプロジェクトの作成](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image3.png)

    <span data-ttu-id="1a117-165">*Web API と MVC コンポーネントを含む、Web フォームテンプレートを使用した新しいプロジェクトの作成*</span><span class="sxs-lookup"><span data-stu-id="1a117-165">*Creating a new project with the Web Forms template, including Web API and MVC components*</span></span>
4. <span data-ttu-id="1a117-166">生成されたソリューションの構造を調べることができるようになりました。</span><span class="sxs-lookup"><span data-stu-id="1a117-166">You can now explore the structure of the generated solution.</span></span>

    ![生成されたソリューションの調査](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image4.png)

    <span data-ttu-id="1a117-168">*生成されたソリューションの調査*</span><span class="sxs-lookup"><span data-stu-id="1a117-168">*Exploring the generated solution*</span></span>

    1. <span data-ttu-id="1a117-169">**アカウント:** このフォルダーには、アプリケーションのユーザーアカウントを登録、ログイン、および管理するための Web フォームページが含まれています。</span><span class="sxs-lookup"><span data-stu-id="1a117-169">**Account:** This folder contains the Web Form pages to register, log in to and manage the application's user accounts.</span></span> <span data-ttu-id="1a117-170">このフォルダーは、Web フォームプロジェクトテンプレートの構成中に [**個々のユーザーアカウント**認証] オプションを選択すると追加されます。</span><span class="sxs-lookup"><span data-stu-id="1a117-170">This folder is added when the **Individual User Accounts** authentication option is selected during the configuration of the Web Forms project template.</span></span>
    2. <span data-ttu-id="1a117-171">**モデル:** このフォルダーには、アプリケーションデータを表すクラスが含まれます。</span><span class="sxs-lookup"><span data-stu-id="1a117-171">**Models:** This folder will contain the classes that represent your application data.</span></span>
    3. <span data-ttu-id="1a117-172">**コントローラー**と**ビュー**: これらのフォルダーは、 **ASP.NET の MVC**コンポーネントと**ASP.NET Web API**コンポーネントに必要です。</span><span class="sxs-lookup"><span data-stu-id="1a117-172">**Controllers** and **Views**: These folders are required for the **ASP.NET MVC** and **ASP.NET Web API** components.</span></span> <span data-ttu-id="1a117-173">次の演習では、MVC と Web API テクノロジについて説明します。</span><span class="sxs-lookup"><span data-stu-id="1a117-173">You will explore the MVC and Web API technologies in the next exercises.</span></span>
    4. <span data-ttu-id="1a117-174">Default.aspx **、** **Contact .aspx** 、および **.aspx ファイルについて**は、事前に定義された Web フォームページであり、アプリケーションに固有のページを構築するための開始点として使用できます。</span><span class="sxs-lookup"><span data-stu-id="1a117-174">The **Default.aspx**, **Contact.aspx** and **About.aspx** files are pre-defined Web Form pages that you can use as starting points to build the pages specific to your application.</span></span> <span data-ttu-id="1a117-175">これらのファイルのプログラミングロジックは、&quot;分離コード&quot; ファイルと呼ばれる別のファイルに存在します。このファイルには、使用する言語に応じて &quot;.aspx&quot; または &quot;. aspx.cs&quot; extension があります。</span><span class="sxs-lookup"><span data-stu-id="1a117-175">The programming logic of those files resides in a separate file referred to as the &quot;code-behind&quot; file, which has an &quot;.aspx.vb&quot; or &quot;.aspx.cs&quot; extension (depending on the language used).</span></span> <span data-ttu-id="1a117-176">分離コードロジックはサーバー上で実行され、ページの HTML 出力を動的に生成します。</span><span class="sxs-lookup"><span data-stu-id="1a117-176">The code-behind logic runs on the server and dynamically produces the HTML output for your page.</span></span>
    5. <span data-ttu-id="1a117-177">このページ**では、** アプリケーション内のすべてのページのルックアンドフィールと標準動作が定義され**ています**。</span><span class="sxs-lookup"><span data-stu-id="1a117-177">The **Site.Master** and **Site.Mobile.Master** pages define the look and feel and the standard behavior of all the pages in the application.</span></span>
5. <span data-ttu-id="1a117-178">**Default.aspx**ファイルをダブルクリックして、ページの内容を調べます。</span><span class="sxs-lookup"><span data-stu-id="1a117-178">Double-click the **Default.aspx** file to explore the content of the page.</span></span>

    ![Default.aspx ページの調査](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image5.png)

    <span data-ttu-id="1a117-180">*Default.aspx ページの調査*</span><span class="sxs-lookup"><span data-stu-id="1a117-180">*Exploring the Default.aspx page*</span></span>

    > [!NOTE]
    > <span data-ttu-id="1a117-181">ファイルの先頭にある**ページ**ディレクティブによって、Web フォームページの属性が定義されます。</span><span class="sxs-lookup"><span data-stu-id="1a117-181">The **Page** directive at the top of the file defines the attributes of the Web Forms page.</span></span> <span data-ttu-id="1a117-182">たとえば、 **MasterPageFile**属性はマスターページへのパスを指定します。この場合、この例**では、** 継承するページの分離コードクラスを定義し*ます。*</span><span class="sxs-lookup"><span data-stu-id="1a117-182">For example, the **MasterPageFile** attribute specifies the path to the master page -in this case, the *Site.Master* page- and the **Inherits** attribute defines the code-behind class for the page to inherit.</span></span> <span data-ttu-id="1a117-183">このクラスは、**分離コード**属性によって決定されるファイルにあります。</span><span class="sxs-lookup"><span data-stu-id="1a117-183">This class is located in the file determined by the **CodeBehind** attribute.</span></span>
    > 
    > <span data-ttu-id="1a117-184">**Asp: content**コントロールは、ページの実際のコンテンツ (テキスト、マークアップ、およびコントロール) を保持し、マスターページの**asp: ContentPlaceHolder**コントロールにマップされます。</span><span class="sxs-lookup"><span data-stu-id="1a117-184">The **asp:Content** control holds the actual content of the page (text, markup and controls) and is mapped to a **asp:ContentPlaceHolder** control on the master page.</span></span> <span data-ttu-id="1a117-185">この場合、ページコンテンツは、*サイトのマスター*ページで定義されている*maincontent*コントロール内に表示されます。</span><span class="sxs-lookup"><span data-stu-id="1a117-185">In this case, the page content will be rendered inside the *MainContent* control defined in the *Site.Master* page.</span></span>
6. <span data-ttu-id="1a117-186">**アプリ\_[開始**] フォルダーを展開し、 **WebApiConfig.cs**ファイルを確認します。</span><span class="sxs-lookup"><span data-stu-id="1a117-186">Expand the **App\_Start** folder and notice the **WebApiConfig.cs** file.</span></span> <span data-ttu-id="1a117-187">Visual Studio では、ASP.NET テンプレートを使用してプロジェクトを構成するときに Web API が含まれているため、生成されたソリューションにそのファイルが含まれていました。</span><span class="sxs-lookup"><span data-stu-id="1a117-187">Visual Studio included that file in the generated solution because you included Web API when configuring your project with the One ASP.NET template.</span></span>
7. <span data-ttu-id="1a117-188">**WebApiConfig.cs**ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="1a117-188">Open the **WebApiConfig.cs** file.</span></span> <span data-ttu-id="1a117-189">*Webapiconfig.cs*クラスには、web api に関連付けられている構成があります。これにより、HTTP ルートが**web api コントローラー**にマップされます。</span><span class="sxs-lookup"><span data-stu-id="1a117-189">In the *WebApiConfig* class you will find the configuration associated with Web API, which maps HTTP routes to **Web API controllers**.</span></span>

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample1.cs)]
8. <span data-ttu-id="1a117-190">**RouteConfig.cs**ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="1a117-190">Open the **RouteConfig.cs** file.</span></span> <span data-ttu-id="1a117-191">*RegisterRoutes*メソッド内には、mvc に関連付けられている構成があります。これは、 **MVC コントローラー**に HTTP ルートをマップします。</span><span class="sxs-lookup"><span data-stu-id="1a117-191">Inside the *RegisterRoutes* method you will find the configuration associated with MVC, which maps HTTP routes to **MVC controllers**.</span></span>

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample2.cs)]

<a id="Ex1Task2"></a>
#### <a name="task-2--running-the-solution"></a><span data-ttu-id="1a117-192">タスク2–ソリューションを実行する</span><span class="sxs-lookup"><span data-stu-id="1a117-192">Task 2 – Running the Solution</span></span>

<span data-ttu-id="1a117-193">このタスクでは、生成されたソリューションを実行し、アプリとその機能の一部 (URL リライトや組み込み認証など) を探索します。</span><span class="sxs-lookup"><span data-stu-id="1a117-193">In this task you will run the generated solution, explore the app and some of its features, like URL rewriting and built-in authentication.</span></span>

1. <span data-ttu-id="1a117-194">ソリューションを実行するには、 **F5**キーを押すか、ツールバーにある **[開始]** ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="1a117-194">To run the solution, press **F5** or click the **Start** button located on the toolbar.</span></span> <span data-ttu-id="1a117-195">アプリケーションのホームページがブラウザーに表示されます。</span><span class="sxs-lookup"><span data-stu-id="1a117-195">The application home page should open in the browser.</span></span>

    ![ソリューションの実行](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image6.png)
2. <span data-ttu-id="1a117-197">Web フォームページが呼び出されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="1a117-197">Verify that the Web Forms pages are being invoked.</span></span> <span data-ttu-id="1a117-198">これを行うには、アドレスバーの URL に **/contactを** **追加し、enter キーを**押します。</span><span class="sxs-lookup"><span data-stu-id="1a117-198">To do this, append **/contact.aspx** to the URL in the address bar and press **Enter**.</span></span>

    ![わかりやすい URL](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image7.png)

    <span data-ttu-id="1a117-200">*わかりやすい Url*</span><span class="sxs-lookup"><span data-stu-id="1a117-200">*Friendly URLs*</span></span>

    > [!NOTE]
    > <span data-ttu-id="1a117-201">ご覧のとおり、URL は **/contact**に変わります。</span><span class="sxs-lookup"><span data-stu-id="1a117-201">As you can see, the URL changes to **/contact**.</span></span> <span data-ttu-id="1a117-202">**ASP.NET 4**以降では、url ルーティング機能が Web フォームに追加され、 *[http://www.mysite.com/products.aspx?category=software](http://www.mysite.com/products.aspx?category=software)* ではなく *[http://www.mysite.com/products/software](http://www.mysite.com/products/software)* のような url を記述できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="1a117-202">Starting from **ASP.NET 4**, URL routing capabilities were added to Web Forms, so you can write URLs like *[http://www.mysite.com/products/software](http://www.mysite.com/products/software)* instead of *[http://www.mysite.com/products.aspx?category=software](http://www.mysite.com/products.aspx?category=software)*.</span></span> <span data-ttu-id="1a117-203">詳細については、「 [URL ルーティング](../../../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/url-routing.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="1a117-203">For more information refer to [URL Routing](../../../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/url-routing.md).</span></span>
3. <span data-ttu-id="1a117-204">ここでは、アプリケーションに統合されている認証フローについて説明します。</span><span class="sxs-lookup"><span data-stu-id="1a117-204">You will now explore the authentication flow integrated into the application.</span></span> <span data-ttu-id="1a117-205">これを行うには、ページの右上隅にある **[登録]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="1a117-205">To do this, click **Register** in the upper-right corner of the page.</span></span>

    ![新しいユーザーの登録](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image8.png)

    <span data-ttu-id="1a117-207">*新しいユーザーの登録*</span><span class="sxs-lookup"><span data-stu-id="1a117-207">*Registering a new user*</span></span>
4. <span data-ttu-id="1a117-208">**[登録]** ページで、**ユーザー名**と**パスワード**を入力し、 **[登録]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="1a117-208">In the **Register** page, enter a **User name** and **Password**, and then click **Register**.</span></span>

    ![[登録] ページ](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image9.png)

    <span data-ttu-id="1a117-210">*[登録] ページ*</span><span class="sxs-lookup"><span data-stu-id="1a117-210">*Register page*</span></span>
5. <span data-ttu-id="1a117-211">アプリケーションは新しいアカウントを登録し、ユーザーは認証されます。</span><span class="sxs-lookup"><span data-stu-id="1a117-211">The application registers the new account, and the user is authenticated.</span></span>

    ![認証されたユーザー](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image10.png)

    <span data-ttu-id="1a117-213">*認証されたユーザー*</span><span class="sxs-lookup"><span data-stu-id="1a117-213">*User authenticated*</span></span>
6. <span data-ttu-id="1a117-214">Visual Studio に戻り、SHIFT キーを押し**ながら F5**キーを押してデバッグを停止します。</span><span class="sxs-lookup"><span data-stu-id="1a117-214">Go back to Visual Studio and press **SHIFT + F5** to stop debugging.</span></span>

<a id="Exercise2"></a>
### <a name="exercise-2-creating-an-mvc-controller-using-scaffolding"></a><span data-ttu-id="1a117-215">演習 2: スキャフォールディングを使用した MVC コントローラーの作成</span><span class="sxs-lookup"><span data-stu-id="1a117-215">Exercise 2: Creating an MVC Controller Using Scaffolding</span></span>

<span data-ttu-id="1a117-216">この演習では、Visual Studio に用意されている ASP.NET スキャフォールディングフレームワークを利用して、アクションと Razor ビューを含む ASP.NET MVC 5 コントローラーを作成し、コードを1行も記述せずに CRUD 操作を実行します。</span><span class="sxs-lookup"><span data-stu-id="1a117-216">In this exercise you will take advantage of the ASP.NET Scaffolding framework provided by Visual Studio to create an ASP.NET MVC 5 controller with actions and Razor views to perform CRUD operations, without writing a single line of code.</span></span> <span data-ttu-id="1a117-217">スキャフォールディングプロセスでは、Entity Framework Code First を使用して、SQL データベースのデータコンテキストとデータベーススキーマを生成します。</span><span class="sxs-lookup"><span data-stu-id="1a117-217">The scaffolding process will use Entity Framework Code First to generate the data context and the database schema in the SQL database.</span></span>

<span data-ttu-id="1a117-218">**Entity Framework Code First について**</span><span class="sxs-lookup"><span data-stu-id="1a117-218">**About Entity Framework Code First**</span></span>

<span data-ttu-id="1a117-219">Entity Framework (EF) は、リレーショナルストレージスキーマを使用して直接プログラミングするのではなく、概念アプリケーションモデルを使用してプログラミングすることで、データアクセスアプリケーションを作成できる、オブジェクトリレーショナルマッパー (ORM) です。</span><span class="sxs-lookup"><span data-stu-id="1a117-219">Entity Framework (EF) is an object-relational mapper (ORM) that enables you to create data access applications by programming with a conceptual application model instead of programming directly using a relational storage schema.</span></span>

<span data-ttu-id="1a117-220">Entity Framework Code First モデリングワークフローを使用すると、独自のドメインクラスを使用して、クエリ、変更の追跡、および更新の各関数を実行するときに EF が依存するモデルを表すことができます。</span><span class="sxs-lookup"><span data-stu-id="1a117-220">The Entity Framework Code First modeling workflow allows you to use your own domain classes to represent the model that EF relies on when performing querying, change-tracking and updating functions.</span></span> <span data-ttu-id="1a117-221">Code First 開発ワークフローを使用して、データベースを作成したり、スキーマを指定したりして、アプリケーションを開始する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="1a117-221">Using the Code First development workflow, you do not need to begin your application by creating a database or specifying a schema.</span></span> <span data-ttu-id="1a117-222">代わりに、アプリケーションに最も適したドメインモデルオブジェクトを定義する標準の .NET クラスを作成し、Entity Framework によってデータベースが作成されるようにします。</span><span class="sxs-lookup"><span data-stu-id="1a117-222">Instead, you can write standard .NET classes that define the most appropriate domain model objects for your application, and Entity Framework will create the database for you.</span></span>

> [!NOTE]
> <span data-ttu-id="1a117-223">Entity Framework の詳細については、[こちら](../../../entity-framework.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="1a117-223">You can learn more about Entity Framework [here](../../../entity-framework.md).</span></span>

<a id="Ex2Task1"></a>
#### <a name="task-1--creating-a-new-model"></a><span data-ttu-id="1a117-224">タスク1–新しいモデルの作成</span><span class="sxs-lookup"><span data-stu-id="1a117-224">Task 1 – Creating a New Model</span></span>

<span data-ttu-id="1a117-225">ここでは、**ユーザー**クラスを定義します。これは、MVC コントローラーとビューを作成するためにスキャフォールディングプロセスによって使用されるモデルです。</span><span class="sxs-lookup"><span data-stu-id="1a117-225">You will now define a **Person** class, which will be the model used by the scaffolding process to create the MVC controller and the views.</span></span> <span data-ttu-id="1a117-226">まず、 **Person**モデルクラスを作成します。その後、コントローラーの CRUD 操作は、スキャフォールディング機能を使用して自動的に作成されます。</span><span class="sxs-lookup"><span data-stu-id="1a117-226">You will start by creating a **Person** model class, and the CRUD operations in the controller will be automatically created using scaffolding features.</span></span>

1. <span data-ttu-id="1a117-227">**Web 用に Visual Studio Express 2013**を開き、 **Source/Ex2-mvcscaffolding/Begin**フォルダーにある**MyHybridSite**ソリューションを開きます。</span><span class="sxs-lookup"><span data-stu-id="1a117-227">Open **Visual Studio Express 2013 for Web** and the **MyHybridSite.sln** solution located in the **Source/Ex2-MvcScaffolding/Begin** folder.</span></span> <span data-ttu-id="1a117-228">または、前の演習で取得したソリューションを続行することもできます。</span><span class="sxs-lookup"><span data-stu-id="1a117-228">Alternatively, you can continue with the solution that you obtained in the previous exercise.</span></span>
2. <span data-ttu-id="1a117-229">**ソリューションエクスプローラー**で、 **MyHybridSite**プロジェクトの **モデル** フォルダーを右クリックし、追加 を選択します。 **クラス.** ...</span><span class="sxs-lookup"><span data-stu-id="1a117-229">In **Solution Explorer**, right-click the **Models** folder of the **MyHybridSite** project and select **Add | Class...**.</span></span>

    ![Person モデルクラスの追加](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image11.png)

    <span data-ttu-id="1a117-231">*Person モデルクラスの追加*</span><span class="sxs-lookup"><span data-stu-id="1a117-231">*Adding the Person model class*</span></span>
3. <span data-ttu-id="1a117-232">**[新しい項目の追加]** ダイアログボックスで、ファイルに*Person.cs*という名前を指定し、 **[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="1a117-232">In the **Add New Item** dialog box, name the file *Person.cs* and click **Add**.</span></span>

    ![Person モデルクラスの作成](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image12.png)

    <span data-ttu-id="1a117-234">*Person モデルクラスの作成*</span><span class="sxs-lookup"><span data-stu-id="1a117-234">*Creating the Person model class*</span></span>
4. <span data-ttu-id="1a117-235">**Person.cs**ファイルの内容を次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="1a117-235">Replace the content of the **Person.cs** file with the following code.</span></span> <span data-ttu-id="1a117-236">**CTRL + S**キーを押して、変更を保存します。</span><span class="sxs-lookup"><span data-stu-id="1a117-236">Press **CTRL + S** to save the changes.</span></span>

    <span data-ttu-id="1a117-237">(コードスニペット- *BringingTogetherOneAspNet-Ex2-個人クラス*)</span><span class="sxs-lookup"><span data-stu-id="1a117-237">(Code Snippet - *BringingTogetherOneAspNet - Ex2 - PersonClass*)</span></span>

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample3.cs)]
5. <span data-ttu-id="1a117-238">**ソリューションエクスプローラー**で、 **MyHybridSite**プロジェクトを右クリックし、 **[ビルド]** を選択するか、 **CTRL + SHIFT + B**キーを押してプロジェクトをビルドします。</span><span class="sxs-lookup"><span data-stu-id="1a117-238">In **Solution Explorer**, right-click the **MyHybridSite** project and select **Build**, or press **CTRL + SHIFT + B** to build the project.</span></span>

<a id="Ex2Task2"></a>
#### <a name="task-2--creating-an-mvc-controller"></a><span data-ttu-id="1a117-239">タスク 2-MVC コントローラーの作成</span><span class="sxs-lookup"><span data-stu-id="1a117-239">Task 2 – Creating an MVC Controller</span></span>

<span data-ttu-id="1a117-240">これで、 **person**モデルが作成されたので、Entity Framework で ASP.NET MVC スキャフォールディングを使用して、**ユーザー**の CRUD コントローラーアクションとビューを作成します。</span><span class="sxs-lookup"><span data-stu-id="1a117-240">Now that the **Person** model is created, you will use ASP.NET MVC scaffolding with Entity Framework to create the CRUD controller actions and views for **Person**.</span></span>

1. <span data-ttu-id="1a117-241">**ソリューションエクスプローラー**で、 **MyHybridSite**プロジェクトの**Controllers**フォルダーを右クリックし、[追加] を選択します。 **新しいスキャフォールディング項目...**</span><span class="sxs-lookup"><span data-stu-id="1a117-241">In **Solution Explorer**, right-click the **Controllers** folder of the **MyHybridSite** project and select **Add | New Scaffolded Item...**.</span></span>

    ![新しいスキャフォールディングコントローラーを作成する](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image13.png)

    <span data-ttu-id="1a117-243">*新しいスキャフォールディングコントローラーを作成する*</span><span class="sxs-lookup"><span data-stu-id="1a117-243">*Creating a new Scaffolded Controller*</span></span>
2. <span data-ttu-id="1a117-244">**[スキャフォールディングの追加]** ダイアログボックスで、 **[MVC 5 Controller with views]** を選択し Entity Framework を使用して [追加] をクリックし**ます。**</span><span class="sxs-lookup"><span data-stu-id="1a117-244">In the **Add Scaffold** dialog box, select **MVC 5 Controller with views, using Entity Framework** and then click **Add.**</span></span>

    ![ビューと Entity Framework がある MVC 5 コントローラーの選択](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image14.png)

    <span data-ttu-id="1a117-246">*ビューと Entity Framework がある MVC 5 コントローラーの選択*</span><span class="sxs-lookup"><span data-stu-id="1a117-246">*Selecting MVC 5 Controller with views and Entity Framework*</span></span>
3. <span data-ttu-id="1a117-247">[ *Mvc個人コントローラー* ] を**コントローラー名**として設定し、 **[非同期コントローラーアクションを使用する]** オプションを選択して、**モデルクラス**として **[Person (MyHybridSite)]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="1a117-247">Set *MvcPersonController* as the **Controller name**, select the **Use async controller actions** option and select **Person (MyHybridSite.Models)** as the **Model class**.</span></span>

    ![スキャフォールディングを使用した MVC コントローラーの追加](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image15.png)

    <span data-ttu-id="1a117-249">*スキャフォールディングを使用した MVC コントローラーの追加*</span><span class="sxs-lookup"><span data-stu-id="1a117-249">*Adding an MVC controller with scaffolding*</span></span>
4. <span data-ttu-id="1a117-250">**[データコンテキストクラス]** で、 **[新しいデータコンテキスト]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="1a117-250">Under **Data context class**, click **New data context...**.</span></span>

    ![新しいデータコンテキストの作成](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image16.png)

    <span data-ttu-id="1a117-252">*新しいデータコンテキストの作成*</span><span class="sxs-lookup"><span data-stu-id="1a117-252">*Creating a new data context*</span></span>
5. <span data-ttu-id="1a117-253">**[新しいデータコンテキスト]** ダイアログボックスで、新しいデータコンテキストに「*個人のコンテキスト*」という名前を指定し、 **[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="1a117-253">In the **New Data Context** dialog box, name the new data context *PersonContext* and click **Add**.</span></span>

    ![新しい個人のコンテキストを作成する](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image17.png)

    <span data-ttu-id="1a117-255">*新しい個人コンテキストの種類を作成する*</span><span class="sxs-lookup"><span data-stu-id="1a117-255">*Creating the new PersonContext type*</span></span>
6. <span data-ttu-id="1a117-256">**[追加]** をクリックして、スキャフォールディングを持つ**ユーザー**の新しいコントローラーを作成します。</span><span class="sxs-lookup"><span data-stu-id="1a117-256">Click **Add** to create the new controller for **Person** with scaffolding.</span></span> <span data-ttu-id="1a117-257">次に、Visual Studio によってコントローラーアクション、Person データコンテキスト、および Razor ビューが生成されます。</span><span class="sxs-lookup"><span data-stu-id="1a117-257">Visual Studio will then generate the controller actions, the Person data context and the Razor views.</span></span>

    ![スキャフォールディングを使用して MVC コントローラーを作成した後](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image18.png)

    <span data-ttu-id="1a117-259">*スキャフォールディングを使用して MVC コントローラーを作成した後*</span><span class="sxs-lookup"><span data-stu-id="1a117-259">*After creating the MVC controller with scaffolding*</span></span>
7. <span data-ttu-id="1a117-260">**Controllers**フォルダーの**MvcPersonController.cs**ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="1a117-260">Open the **MvcPersonController.cs** file in the **Controllers** folder.</span></span> <span data-ttu-id="1a117-261">CRUD アクションメソッドが自動的に生成されていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="1a117-261">Notice that the CRUD action methods have been generated automatically.</span></span>

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample4.cs)]

    > [!NOTE]
    > <span data-ttu-id="1a117-262">前の手順で スキャフォールディング オプションから  **async controller アクションを使用する** チェックボックスをオンにすると、Visual Studio によって、Person データコンテキストへのアクセスを伴うすべてのアクションの非同期アクションメソッドが生成されます。</span><span class="sxs-lookup"><span data-stu-id="1a117-262">By selecting the **Use async controller actions** check box from the scaffolding options in the previous steps, Visual Studio generates asynchronous action methods for all actions that involve access to the Person data context.</span></span> <span data-ttu-id="1a117-263">要求の処理中に Web サーバーが処理を実行できないようにするために、実行時間の長い CPU にバインドされていない要求には非同期アクションメソッドを使用することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="1a117-263">It is recommended that you use asynchronous action methods for long-running, non-CPU bound requests to avoid blocking the Web server from performing work while the request is being processed.</span></span>

<a id="Ex2Task3"></a>
#### <a name="task-3--running-the-solution"></a><span data-ttu-id="1a117-264">タスク3–ソリューションを実行する</span><span class="sxs-lookup"><span data-stu-id="1a117-264">Task 3 – Running the Solution</span></span>

<span data-ttu-id="1a117-265">このタスクでは、ソリューションをもう一度実行して、**ユーザー**のビューが想定どおりに機能していることを確認します。</span><span class="sxs-lookup"><span data-stu-id="1a117-265">In this task, you will run the solution again to verify that the views for **Person** are working as expected.</span></span> <span data-ttu-id="1a117-266">新しいユーザーを追加して、データベースに正常に保存されたことを確認します。</span><span class="sxs-lookup"><span data-stu-id="1a117-266">You will add a new person to verify that it is successfully saved to the database.</span></span>

1. <span data-ttu-id="1a117-267">F5 キーを押して、ソリューションを実行します。</span><span class="sxs-lookup"><span data-stu-id="1a117-267">Press **F5** to run the solution.</span></span>
2. <span data-ttu-id="1a117-268">**/MvcPerson**に移動します。</span><span class="sxs-lookup"><span data-stu-id="1a117-268">Navigate to **/MvcPerson**.</span></span> <span data-ttu-id="1a117-269">スキャフォールディングビューが表示されます。</span><span class="sxs-lookup"><span data-stu-id="1a117-269">The scaffolded view that shows the list of people should appear.</span></span>
3. <span data-ttu-id="1a117-270">**[新規作成]** をクリックして、新しいユーザーを追加します。</span><span class="sxs-lookup"><span data-stu-id="1a117-270">Click **Create New** to add a new person.</span></span>

    ![スキャフォールディング MVC ビューへの移動](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image19.png)

    <span data-ttu-id="1a117-272">*スキャフォールディング MVC ビューへの移動*</span><span class="sxs-lookup"><span data-stu-id="1a117-272">*Navigating to the scaffolded MVC views*</span></span>
4. <span data-ttu-id="1a117-273">**[作成]** ビューで、ユーザーの**名前**と**年齢**を指定し、 **[作成]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="1a117-273">In the **Create** view, provide a **Name** and an **Age** for the person, and click **Create**.</span></span>

    ![新しいユーザーの追加](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image20.png)

    <span data-ttu-id="1a117-275">*新しいユーザーの追加*</span><span class="sxs-lookup"><span data-stu-id="1a117-275">*Adding a new person*</span></span>
5. <span data-ttu-id="1a117-276">新しいユーザーがリストに追加されます。</span><span class="sxs-lookup"><span data-stu-id="1a117-276">The new person is added to the list.</span></span> <span data-ttu-id="1a117-277">要素 ボックスの一覧の **詳細** をクリックして、個人の詳細ビューを表示します。</span><span class="sxs-lookup"><span data-stu-id="1a117-277">In the element list, click **Details** to display the person's details view.</span></span> <span data-ttu-id="1a117-278">次に、**詳細**ビューで、 **[戻る]** をクリックしてリストビューに戻ります。</span><span class="sxs-lookup"><span data-stu-id="1a117-278">Then, in the **Details** view, click **Back to List** to go back to the list view.</span></span>

    ![個人の詳細ビュー](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image21.png)

    <span data-ttu-id="1a117-280">*個人の詳細ビュー*</span><span class="sxs-lookup"><span data-stu-id="1a117-280">*Person's details view*</span></span>
6. <span data-ttu-id="1a117-281">**[削除]** リンクをクリックして、ユーザーを削除します。</span><span class="sxs-lookup"><span data-stu-id="1a117-281">Click the **Delete** link to delete the person.</span></span> <span data-ttu-id="1a117-282">**[削除]** ビューで、 **[削除]** をクリックして操作を確定します。</span><span class="sxs-lookup"><span data-stu-id="1a117-282">In the **Delete** view, click **Delete** to confirm the operation.</span></span>

    ![個人の削除](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image22.png)

    <span data-ttu-id="1a117-284">*個人の削除*</span><span class="sxs-lookup"><span data-stu-id="1a117-284">*Deleting a person*</span></span>
7. <span data-ttu-id="1a117-285">Visual Studio に戻り、SHIFT キーを押し**ながら F5**キーを押してデバッグを停止します。</span><span class="sxs-lookup"><span data-stu-id="1a117-285">Go back to Visual Studio and press **SHIFT + F5** to stop debugging.</span></span>

<a id="Exercise3"></a>
### <a name="exercise-3-creating-a-web-api-controller-using-scaffolding"></a><span data-ttu-id="1a117-286">演習 3: スキャフォールディングを使用した Web API コントローラーの作成</span><span class="sxs-lookup"><span data-stu-id="1a117-286">Exercise 3: Creating a Web API Controller Using Scaffolding</span></span>

<span data-ttu-id="1a117-287">Web API フレームワークは ASP.NET スタックの一部であり、HTTP サービスの実装を容易にするように設計されており、一般的には、RESTful API を使用して JSON または XML 形式のデータを送受信します。</span><span class="sxs-lookup"><span data-stu-id="1a117-287">The Web API framework is part of the ASP.NET Stack and designed to make implementing HTTP services easier, generally sending and receiving JSON- or XML-formatted data through a RESTful API.</span></span>

<span data-ttu-id="1a117-288">この演習では、ASP.NET スキャフォールディングを再度使用して、Web API コントローラーを生成します。</span><span class="sxs-lookup"><span data-stu-id="1a117-288">In this exercise, you will use ASP.NET Scaffolding again to generate a Web API controller.</span></span> <span data-ttu-id="1a117-289">同じ person データを JSON 形式で提供するために、前の演習で作成したものと同じ**person**クラスと個人の**コンテキスト**クラスを使用します。</span><span class="sxs-lookup"><span data-stu-id="1a117-289">You will use the same **Person** and **PersonContext** classes from the previous exercise to provide the same person data in JSON format.</span></span> <span data-ttu-id="1a117-290">同じ ASP.NET アプリケーション内のさまざまな方法で同じリソースを公開する方法がわかります。</span><span class="sxs-lookup"><span data-stu-id="1a117-290">You will see how you can expose the same resources in different ways within the same ASP.NET application.</span></span>

<a id="Ex3Task1"></a>
#### <a name="task-1--creating-a-web-api-controller"></a><span data-ttu-id="1a117-291">タスク 1-Web API コントローラーを作成する</span><span class="sxs-lookup"><span data-stu-id="1a117-291">Task 1 – Creating a Web API Controller</span></span>

<span data-ttu-id="1a117-292">このタスクでは、ユーザーデータを JSON などのコンピューター使用形式で公開する新しい**WEB API コントローラー**を作成します。</span><span class="sxs-lookup"><span data-stu-id="1a117-292">In this task you will create a new **Web API Controller** that will expose the person data in a machine-consumable format like JSON.</span></span>

1. <span data-ttu-id="1a117-293">まだ開いていない場合は、 **Web 用 Visual Studio Express 2013**を開き、 **Source/Ex3-WebAPI/Begin**フォルダーにある**MyHybridSite**ソリューションを開きます。</span><span class="sxs-lookup"><span data-stu-id="1a117-293">If not already opened, open **Visual Studio Express 2013 for Web** and open the **MyHybridSite.sln** solution located in the **Source/Ex3-WebAPI/Begin** folder.</span></span> <span data-ttu-id="1a117-294">または、前の演習で取得したソリューションを続行することもできます。</span><span class="sxs-lookup"><span data-stu-id="1a117-294">Alternatively, you can continue with the solution that you obtained in the previous exercise.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1a117-295">演習3から始めるソリューションを開始する場合は、 **CTRL + SHIFT + B**キーを押してソリューションをビルドします。</span><span class="sxs-lookup"><span data-stu-id="1a117-295">If you start with the Begin solution from Exercise 3, press **CTRL + SHIFT + B** to build the solution.</span></span>
2. <span data-ttu-id="1a117-296">**ソリューションエクスプローラー**で、 **MyHybridSite**プロジェクトの**Controllers**フォルダーを右クリックし、[追加] を選択します。 **新しいスキャフォールディング項目...**</span><span class="sxs-lookup"><span data-stu-id="1a117-296">In **Solution Explorer**, right-click the **Controllers** folder of the **MyHybridSite** project and select **Add | New Scaffolded Item...**.</span></span>

    ![新しいスキャフォールディングコントローラーを作成する](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image23.png)

    <span data-ttu-id="1a117-298">*新しいスキャフォールディングコントローラーを作成する*</span><span class="sxs-lookup"><span data-stu-id="1a117-298">*Creating a new scaffolded Controller*</span></span>
3. <span data-ttu-id="1a117-299">**[スキャフォールディングの追加]** ダイアログボックスの左側のウィンドウで **[web api]** を選択し、次に、中央のウィンドウで**Entity Framework を使用して [web api 2 コントローラー** ] をクリックし、[追加] をクリックし**ます。**</span><span class="sxs-lookup"><span data-stu-id="1a117-299">In the **Add Scaffold** dialog box, select **Web API** in the left pane, then **Web API 2 Controller with actions, using Entity Framework** in the middle pane and then click **Add.**</span></span>

    <span data-ttu-id="1a117-300">![アクションと Entity Framework がある Web API 2 コントローラーを選択する](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image24.png "アクションと Entity Framework がある Web API 2 コントローラーを選択する")</span><span class="sxs-lookup"><span data-stu-id="1a117-300">![Selecting Web API 2 Controller with actions and Entity Framework](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image24.png "Selecting Web API 2 Controller with actions and Entity Framework")</span></span>

    <span data-ttu-id="1a117-301">*アクションと Entity Framework がある Web API 2 コントローラーを選択する*</span><span class="sxs-lookup"><span data-stu-id="1a117-301">*Selecting Web API 2 Controller with actions and Entity Framework*</span></span>
4. <span data-ttu-id="1a117-302">*Apiperson controller*を**コントローラー名**として設定し、 **[非同期コントローラーアクションを使用する]** オプションを選択し、**モデル**および**データコンテキスト**クラスとして **[Person (MyHybridSite)]** と ユーザー **[コンテキスト (MyHybridSite)]** をそれぞれ選択します。</span><span class="sxs-lookup"><span data-stu-id="1a117-302">Set *ApiPersonController* as the **Controller name**, select the **Use async controller actions** option and select **Person (MyHybridSite.Models)** and **PersonContext (MyHybridSite.Models)** as the **Model** and **Data context** classes respectively.</span></span> <span data-ttu-id="1a117-303">**[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="1a117-303">Then click **Add**.</span></span>

    <span data-ttu-id="1a117-304">![スキャフォールディングを使用した Web API コントローラーの追加](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image25.png "スキャフォールディングを使用した Web API コントローラーの追加")</span><span class="sxs-lookup"><span data-stu-id="1a117-304">![Adding a Web API Controller with scaffolding](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image25.png "Adding a Web API controller with scaffolding")</span></span>

    <span data-ttu-id="1a117-305">*スキャフォールディングを使用した Web API コントローラーの追加*</span><span class="sxs-lookup"><span data-stu-id="1a117-305">*Adding a Web API controller with scaffolding*</span></span>
5. <span data-ttu-id="1a117-306">次に、データを操作する4つの CRUD アクションを使用して、Visual Studio によって**Api個人コントローラー**クラスが生成されます。</span><span class="sxs-lookup"><span data-stu-id="1a117-306">Visual Studio will then generate the **ApiPersonController** class with the four CRUD actions to work with your data.</span></span>

    <span data-ttu-id="1a117-307">![スキャフォールディングを使用して Web API コントローラーを作成した後](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image26.png "スキャフォールディングを使用して Web API コントローラーを作成した後")</span><span class="sxs-lookup"><span data-stu-id="1a117-307">![After creating the Web API controller with scaffolding](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image26.png "After creating the Web API controller with scaffolding")</span></span>

    <span data-ttu-id="1a117-308">*スキャフォールディングを使用して Web API コントローラーを作成した後*</span><span class="sxs-lookup"><span data-stu-id="1a117-308">*After creating the Web API controller with scaffolding*</span></span>
6. <span data-ttu-id="1a117-309">**ApiPersonController.cs**ファイルを開き、 *getpeople*アクションメソッドを調べます。</span><span class="sxs-lookup"><span data-stu-id="1a117-309">Open the **ApiPersonController.cs** file and inspect the *GetPeople* action method.</span></span> <span data-ttu-id="1a117-310">このメソッドは、個人データを取得するために、**個人のコンテキスト**型の db フィールドに対してクエリを行います。</span><span class="sxs-lookup"><span data-stu-id="1a117-310">This method queries the db field of **PersonContext** type in order to get the people data.</span></span>

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample5.cs)]
7. <span data-ttu-id="1a117-311">ここで、メソッド定義の上にコメントがあることを確認します。</span><span class="sxs-lookup"><span data-stu-id="1a117-311">Now notice the comment above the method definition.</span></span> <span data-ttu-id="1a117-312">これは、次のタスクで使用するこのアクションを公開する URI を提供します。</span><span class="sxs-lookup"><span data-stu-id="1a117-312">It provides the URI that exposes this action which you will use in the next task.</span></span>

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample6.cs)]

    > [!NOTE]
    > <span data-ttu-id="1a117-313">既定では、Web API は、MVC コントローラーとの競合を避けるために、 */API*パスに対するクエリをキャッチするように構成されています。</span><span class="sxs-lookup"><span data-stu-id="1a117-313">By default, Web API is configured to catch the queries to the */api* path to avoid collisions with MVC controllers.</span></span> <span data-ttu-id="1a117-314">この設定を変更する必要がある場合は、「 [ASP.NET Web API でのルーティング」](../../../web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="1a117-314">If you need to change this setting, refer to [Routing in ASP.NET Web API](../../../web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api.md).</span></span>

<a id="Ex3Task2"></a>
#### <a name="task-2--running-the-solution"></a><span data-ttu-id="1a117-315">タスク2–ソリューションを実行する</span><span class="sxs-lookup"><span data-stu-id="1a117-315">Task 2 – Running the Solution</span></span>

<span data-ttu-id="1a117-316">このタスクでは、Internet Explorer **F12 開発者ツール**を使用して、Web API コントローラーからの完全な応答を検査します。</span><span class="sxs-lookup"><span data-stu-id="1a117-316">In this task you will use the Internet Explorer **F12 developer tools** to inspect the full response from the Web API controller.</span></span> <span data-ttu-id="1a117-317">ネットワークトラフィックをキャプチャして、アプリケーションデータに関する洞察を得る方法を確認できます。</span><span class="sxs-lookup"><span data-stu-id="1a117-317">You will see how you can capture network traffic to get more insight into your application data.</span></span>

> [!NOTE]
> <span data-ttu-id="1a117-318">Visual Studio ツールバーの **[スタート]** ボタンで**Internet Explorer**が選択されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="1a117-318">Make sure that **Internet Explorer** is selected in the **Start** button located on the Visual Studio toolbar.</span></span>
> 
> ![Internet Explorer オプション](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image27.png)
> 
> <span data-ttu-id="1a117-320">**F12 開発者ツール**には、このハンズオンラボでは説明されていない豊富な機能が用意されています。</span><span class="sxs-lookup"><span data-stu-id="1a117-320">The **F12 developer tools** have a wide set of functionality that is not covered in this hands-on-lab.</span></span> <span data-ttu-id="1a117-321">詳細については、「 [F12 開発者ツールの使用](https://msdn.microsoft.com/library/ie/bg182326(v=vs.85))」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="1a117-321">If you want to learn more about it, refer to [Using the F12 developer tools](https://msdn.microsoft.com/library/ie/bg182326(v=vs.85)).</span></span>

1. <span data-ttu-id="1a117-322">F5 キーを押して、ソリューションを実行します。</span><span class="sxs-lookup"><span data-stu-id="1a117-322">Press **F5** to run the solution.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1a117-323">このタスクを正しく実行するには、アプリケーションにデータが必要です。</span><span class="sxs-lookup"><span data-stu-id="1a117-323">In order to follow this task correctly, your application needs to have data.</span></span> <span data-ttu-id="1a117-324">データベースが空の場合は、演習2のタスク3に戻り、MVC ビューを使用して新しいユーザーを作成する方法の手順に従います。</span><span class="sxs-lookup"><span data-stu-id="1a117-324">If your database is empty, you can go back to Task 3 in Exercise 2 and follow the steps on how to create a new person using the MVC views.</span></span>
2. <span data-ttu-id="1a117-325">ブラウザーで**F12**キーを押して、 **[開発者ツール]** パネルを開きます。</span><span class="sxs-lookup"><span data-stu-id="1a117-325">In the browser, press **F12** to open the **Developer Tools** panel.</span></span> <span data-ttu-id="1a117-326">**CTRL** + **4**キーを押すか、**ネットワーク**アイコンをクリックし、緑色の矢印ボタンをクリックしてネットワークトラフィックのキャプチャを開始します。</span><span class="sxs-lookup"><span data-stu-id="1a117-326">Press **CTRL** + **4** or click the **Network** icon, and then click the green arrow button to begin capturing network traffic.</span></span>

    <span data-ttu-id="1a117-327">![Web API ネットワークキャプチャを開始しています](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image28.png "Web API ネットワークキャプチャを開始しています")</span><span class="sxs-lookup"><span data-stu-id="1a117-327">![Initiating Web API network capture](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image28.png "Initiating Web API network capture")</span></span>

    <span data-ttu-id="1a117-328">*Web API ネットワークキャプチャを開始しています*</span><span class="sxs-lookup"><span data-stu-id="1a117-328">*Initiating Web API network capture*</span></span>
3. <span data-ttu-id="1a117-329">**Api/ApiPerson**をブラウザーのアドレスバーの URL に追加します。</span><span class="sxs-lookup"><span data-stu-id="1a117-329">Append **api/ApiPerson** to the URL in the browser's address bar.</span></span> <span data-ttu-id="1a117-330">次に、 **Api個人コントローラー**からの応答の詳細を調査します。</span><span class="sxs-lookup"><span data-stu-id="1a117-330">You will now inspect the details of the response from the **ApiPersonController**.</span></span>

    <span data-ttu-id="1a117-331">![Web API を使用して個人データを取得する](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image29.png "Web API を使用して個人データを取得する")</span><span class="sxs-lookup"><span data-stu-id="1a117-331">![Retrieving person data through Web API](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image29.png "Retrieving person data through Web API")</span></span>

    <span data-ttu-id="1a117-332">*Web API を使用して個人データを取得する*</span><span class="sxs-lookup"><span data-stu-id="1a117-332">*Retrieving person data through Web API*</span></span>

    > [!NOTE]
    > <span data-ttu-id="1a117-333">ダウンロードが完了すると、ダウンロードしたファイルに対してアクションを実行するように求められます。</span><span class="sxs-lookup"><span data-stu-id="1a117-333">Once the download finishes, you will be prompted to make an action with the downloaded file.</span></span> <span data-ttu-id="1a117-334">[開発者ツール] ウィンドウで応答の内容を確認できるようにするには、ダイアログボックスを開いたままにしておきます。</span><span class="sxs-lookup"><span data-stu-id="1a117-334">Leave the dialog box open in order to be able to watch the response content through the Developers Tool window.</span></span>
4. <span data-ttu-id="1a117-335">次に、応答の本文を調べます。</span><span class="sxs-lookup"><span data-stu-id="1a117-335">Now you will inspect the body of the response.</span></span> <span data-ttu-id="1a117-336">これを行うには、 **[詳細]** タブをクリックし、 **[応答本文]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="1a117-336">To do this, click the **Details** tab and then click **Response body**.</span></span> <span data-ttu-id="1a117-337">ダウンロードしたデータが、 **Person**クラスに対応するプロパティ**Id**、**名前**、および**Age**を持つオブジェクトの一覧であることを確認できます。</span><span class="sxs-lookup"><span data-stu-id="1a117-337">You can check that the downloaded data is a list of objects with the properties **Id**, **Name** and **Age** that correspond to the **Person** class.</span></span>

    <span data-ttu-id="1a117-338">![Web API の応答本文を表示しています](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image30.png "Web API の応答本文を表示しています")</span><span class="sxs-lookup"><span data-stu-id="1a117-338">![Viewing Web API Response Body](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image30.png "Viewing Web API Response Body")</span></span>

    <span data-ttu-id="1a117-339">*Web API の応答本文を表示しています*</span><span class="sxs-lookup"><span data-stu-id="1a117-339">*Viewing Web API Response Body*</span></span>

<a id="Ex3Task3"></a>
#### <a name="task-3--adding-web-api-help-pages"></a><span data-ttu-id="1a117-340">タスク3– Web API のヘルプページを追加する</span><span class="sxs-lookup"><span data-stu-id="1a117-340">Task 3 – Adding Web API Help Pages</span></span>

<span data-ttu-id="1a117-341">Web API を作成するときに、他の開発者が API の呼び出し方法を理解できるように、ヘルプページを作成すると便利です。</span><span class="sxs-lookup"><span data-stu-id="1a117-341">When you create a Web API, it is useful to create a help page so that other developers will know how to call your API.</span></span> <span data-ttu-id="1a117-342">ドキュメントページは手動で作成および更新できますが、メンテナンス作業を行わないように自動生成することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="1a117-342">You could create and update the documentation pages manually, but it is better to auto-generate them to avoid having to do maintenance work.</span></span> <span data-ttu-id="1a117-343">このタスクでは、Nuget パッケージを使用して、Web API のヘルプページをソリューションに自動的に生成します。</span><span class="sxs-lookup"><span data-stu-id="1a117-343">In this task you will use a Nuget package to automatically generate Web API help pages to the solution.</span></span>

1. <span data-ttu-id="1a117-344">Visual Studio の **[ツール]** メニューで、 **[NuGet パッケージマネージャー]** を選択し、 **[パッケージマネージャーコンソール]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="1a117-344">From the **Tools** menu in Visual Studio, select **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>
2. <span data-ttu-id="1a117-345">**[パッケージマネージャーコンソール]** ウィンドウで、次のコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="1a117-345">In the **Package Manager Console** window, execute the following command:</span></span>

    [!code-powershell[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample7.ps1)]

    > [!NOTE]
    > <span data-ttu-id="1a117-346">**WebApi**パッケージは、必要なアセンブリをインストールし、[区分]/[ヘルプ **] ページ**フォルダーの下にあるヘルプページの MVC ビューを追加します。</span><span class="sxs-lookup"><span data-stu-id="1a117-346">The **Microsoft.AspNet.WebApi.HelpPage** package installs the necessary assemblies and adds MVC Views for the help pages under the **Areas/HelpPage** folder.</span></span>

    <span data-ttu-id="1a117-347">![HelpPage 領域](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image31.png "HelpPage 領域")</span><span class="sxs-lookup"><span data-stu-id="1a117-347">![HelpPage Area](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image31.png "HelpPage Area")</span></span>

    <span data-ttu-id="1a117-348">*HelpPage 領域*</span><span class="sxs-lookup"><span data-stu-id="1a117-348">*HelpPage Area*</span></span>
3. <span data-ttu-id="1a117-349">既定では、ヘルプページにドキュメントのプレースホルダー文字列があります。</span><span class="sxs-lookup"><span data-stu-id="1a117-349">By default, the help pages have placeholder strings for documentation.</span></span> <span data-ttu-id="1a117-350">XML ドキュメントコメントを使用して、ドキュメントを作成できます。</span><span class="sxs-lookup"><span data-stu-id="1a117-350">You can use XML documentation comments to create the documentation.</span></span> <span data-ttu-id="1a117-351">この機能を有効にするには、[**区分]、[ヘルプ] ページ、アプリ\_[開始**] フォルダーにある**HelpPageConfig.cs**ファイルを開き、次の行をコメント解除します。</span><span class="sxs-lookup"><span data-stu-id="1a117-351">To enable this feature, open the **HelpPageConfig.cs** file located in the **Areas/HelpPage/App\_Start** folder and uncomment the following line:</span></span>

    [!code-javascript[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample8.js)]
4. <span data-ttu-id="1a117-352">**ソリューションエクスプローラー**で、プロジェクト**MyHybridSite**を右クリックし、 **[プロパティ]** をクリックして、 **[ビルド]** タブをクリックします。</span><span class="sxs-lookup"><span data-stu-id="1a117-352">In **Solution Explorer**, right-click the project **MyHybridSite**, select **Properties** and click the **Build** tab.</span></span>

    <span data-ttu-id="1a117-353">![[ビルド] タブ](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image32.png "ビルドセクション")</span><span class="sxs-lookup"><span data-stu-id="1a117-353">![Build tab](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image32.png "Build section")</span></span>

    <span data-ttu-id="1a117-354">*[ビルド] タブ*</span><span class="sxs-lookup"><span data-stu-id="1a117-354">*Build tab*</span></span>
5. <span data-ttu-id="1a117-355">**[出力]** で、 **[XML ドキュメントファイル]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="1a117-355">Under **Output**, select **XML documentation file**.</span></span> <span data-ttu-id="1a117-356">[編集] ボックスに「 **App\_Data/XmlDocument**」と入力します。</span><span class="sxs-lookup"><span data-stu-id="1a117-356">In the edit box, type **App\_Data/XmlDocument.xml**.</span></span>

    <span data-ttu-id="1a117-357">![[ビルド] タブの [出力] セクション](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image33.png "[ビルド] タブの [出力] セクション")</span><span class="sxs-lookup"><span data-stu-id="1a117-357">![Output section in Build tab](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image33.png "Output section in build tab")</span></span>

    <span data-ttu-id="1a117-358">*[ビルド] タブの [出力] セクション*</span><span class="sxs-lookup"><span data-stu-id="1a117-358">*Output section in Build tab*</span></span>
6. <span data-ttu-id="1a117-359">**CTRL** + **S**キーを押して、変更を保存します。</span><span class="sxs-lookup"><span data-stu-id="1a117-359">Press **CTRL** + **S** to save the changes.</span></span>
7. <span data-ttu-id="1a117-360">**Controllers**フォルダーから**ApiPersonController.cs**ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="1a117-360">Open the **ApiPersonController.cs** file from the **Controllers** folder.</span></span>
8. <span data-ttu-id="1a117-361">*Getpeople*メソッドシグネチャと *//GET Api/apiperson*コメントの間に新しい行を入力し、3つのスラッシュを入力します。</span><span class="sxs-lookup"><span data-stu-id="1a117-361">Enter a new line between the *GetPeople* method signature and the *// GET api/ApiPerson* comment, and then type three forward slashes.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1a117-362">メソッドのドキュメントを定義する XML 要素が Visual Studio によって自動的に挿入されます。</span><span class="sxs-lookup"><span data-stu-id="1a117-362">Visual Studio automatically inserts the XML elements which define the method documentation.</span></span>
9. <span data-ttu-id="1a117-363">*Getpeople*メソッドの概要テキストと戻り値を追加します。</span><span class="sxs-lookup"><span data-stu-id="1a117-363">Add a summary text and the return value for the *GetPeople* method.</span></span> <span data-ttu-id="1a117-364">これは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="1a117-364">It should look like the following.</span></span>

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample9.cs)]
10. <span data-ttu-id="1a117-365">F5 キーを押して、ソリューションを実行します。</span><span class="sxs-lookup"><span data-stu-id="1a117-365">Press **F5** to run the solution.</span></span>
11. <span data-ttu-id="1a117-366">アドレスバーの URL に **/help**を追加して、ヘルプページを参照します。</span><span class="sxs-lookup"><span data-stu-id="1a117-366">Append **/help** to the URL in the address bar to browse to the help page.</span></span>

    <span data-ttu-id="1a117-367">![ASP.NET Web API ヘルプページ](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image34.png "ASP.NET Web API ヘルプページ")</span><span class="sxs-lookup"><span data-stu-id="1a117-367">![ASP.NET Web API Help Page](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image34.png "ASP.NET Web API Help Page")</span></span>

    <span data-ttu-id="1a117-368">*ASP.NET Web API ヘルプページ*</span><span class="sxs-lookup"><span data-stu-id="1a117-368">*ASP.NET Web API Help Page*</span></span>

    > [!NOTE]
    > <span data-ttu-id="1a117-369">ページのメインコンテンツは、コントローラー別にグループ化された Api のテーブルです。</span><span class="sxs-lookup"><span data-stu-id="1a117-369">The main content of the page is a table of APIs, grouped by controller.</span></span> <span data-ttu-id="1a117-370">テーブルエントリは、 **Iapiexplorer**インターフェイスを使用して動的に生成されます。</span><span class="sxs-lookup"><span data-stu-id="1a117-370">The table entries are generated dynamically, using the **IApiExplorer** interface.</span></span> <span data-ttu-id="1a117-371">API コントローラーを追加または更新すると、次にアプリケーションをビルドしたときにテーブルが自動的に更新されます。</span><span class="sxs-lookup"><span data-stu-id="1a117-371">If you add or update an API controller, the table will be automatically updated the next time you build the application.</span></span>
    > 
    > <span data-ttu-id="1a117-372">**[API]** 列には、HTTP メソッドと相対 URI が表示されます。</span><span class="sxs-lookup"><span data-stu-id="1a117-372">The **API** column lists the HTTP method and relative URI.</span></span> <span data-ttu-id="1a117-373">**Description**列には、メソッドのドキュメントから抽出された情報が含まれています。</span><span class="sxs-lookup"><span data-stu-id="1a117-373">The **Description** column contains information that has been extracted from the method's documentation.</span></span>
12. <span data-ttu-id="1a117-374">メソッド定義の上に追加した説明が 説明列に表示されることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="1a117-374">Note that the description you added above the method definition is displayed in the description column.</span></span>

    <span data-ttu-id="1a117-375">![API メソッドの説明](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image35.png "API メソッドの説明")</span><span class="sxs-lookup"><span data-stu-id="1a117-375">![API method description](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image35.png "API method description")</span></span>

    <span data-ttu-id="1a117-376">*API メソッドの説明*</span><span class="sxs-lookup"><span data-stu-id="1a117-376">*API method description*</span></span>
13. <span data-ttu-id="1a117-377">API メソッドのいずれかをクリックして、応答本文のサンプルなどの詳細な情報が記載されたページに移動します。</span><span class="sxs-lookup"><span data-stu-id="1a117-377">Click one of the API methods to navigate to a page with more detailed information, including sample response bodies.</span></span>

    <span data-ttu-id="1a117-378">![[詳細情報] ページ](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image36.png "[詳細情報] ページ")</span><span class="sxs-lookup"><span data-stu-id="1a117-378">![Detail Information page](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image36.png "Detail Information page")</span></span>

    <span data-ttu-id="1a117-379">*詳細情報ページ*</span><span class="sxs-lookup"><span data-stu-id="1a117-379">*Detailed information page*</span></span>

---

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="1a117-380">まとめ</span><span class="sxs-lookup"><span data-stu-id="1a117-380">Summary</span></span>

<span data-ttu-id="1a117-381">このハンズオンラボを完了することで、次の方法を学習できました。</span><span class="sxs-lookup"><span data-stu-id="1a117-381">By completing this hands-on lab you have learned how to:</span></span>

- <span data-ttu-id="1a117-382">Visual Studio 2013 の1つの ASP.NET エクスペリエンスを使用して新しい Web アプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="1a117-382">Create a new Web application using the One ASP.NET Experience in Visual Studio 2013</span></span>
- <span data-ttu-id="1a117-383">複数の ASP.NET テクノロジを1つのプロジェクトに統合する</span><span class="sxs-lookup"><span data-stu-id="1a117-383">Integrate multiple ASP.NET technologies into one single project</span></span>
- <span data-ttu-id="1a117-384">ASP.NET スキャフォールディングを使用してモデルクラスから MVC コントローラーとビューを生成する</span><span class="sxs-lookup"><span data-stu-id="1a117-384">Generate MVC controllers and views from your model classes using ASP.NET Scaffolding</span></span>
- <span data-ttu-id="1a117-385">非同期プログラミングやデータアクセスなどの機能を使用して、Web API コントローラーを生成 Entity Framework</span><span class="sxs-lookup"><span data-stu-id="1a117-385">Generate Web API controllers, which use features such as Async Programming and data access through Entity Framework</span></span>
- <span data-ttu-id="1a117-386">コントローラーの Web API ヘルプページを自動的に生成する</span><span class="sxs-lookup"><span data-stu-id="1a117-386">Automatically generate Web API Help Pages for your controllers</span></span>
