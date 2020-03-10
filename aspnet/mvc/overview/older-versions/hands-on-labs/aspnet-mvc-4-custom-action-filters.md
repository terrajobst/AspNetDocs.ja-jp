---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-custom-action-filters
title: ASP.NET MVC 4 カスタムアクションフィルター |Microsoft Docs
author: rick-anderson
description: ASP.NET MVC には、アクションメソッドが呼び出される前または後にフィルター処理ロジックを実行するためのアクションフィルターが用意されています。 アクションフィルターはカスタム属性 tha...
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 969ab824-1b98-4552-81fe-b60ef5fc6887
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-custom-action-filters
msc.type: authoredcontent
ms.openlocfilehash: eaeb32180f79fabf557cbc38ff067eb26b47fea7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78468178"
---
# <a name="aspnet-mvc-4-custom-action-filters"></a><span data-ttu-id="f5f7c-104">ASP.NET MVC 4 カスタム アクション フィルター</span><span class="sxs-lookup"><span data-stu-id="f5f7c-104">ASP.NET MVC 4 Custom Action Filters</span></span>

<span data-ttu-id="f5f7c-105">[Web キャンプチーム](https://twitter.com/webcamps)別</span><span class="sxs-lookup"><span data-stu-id="f5f7c-105">By [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="f5f7c-106">Web キャンプトレーニングキットをダウンロードする</span><span class="sxs-lookup"><span data-stu-id="f5f7c-106">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

<span data-ttu-id="f5f7c-107">ASP.NET MVC には、アクションメソッドが呼び出される前または後にフィルター処理ロジックを実行するためのアクションフィルターが用意されています。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-107">ASP.NET MVC provides Action Filters for executing filtering logic either before or after an action method is called.</span></span> <span data-ttu-id="f5f7c-108">アクションフィルターは、コントローラーのアクションメソッドに事前アクション動作とアクション後動作を追加するための宣言型の手段を提供するカスタム属性です。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-108">Action Filters are custom attributes that provide declarative means to add pre-action and post-action behavior to the controller's action methods.</span></span>

<span data-ttu-id="f5f7c-109">このハンズオンラボでは、MvcMusicStore solution にカスタムアクションフィルター属性を作成して、コントローラーの要求をキャッチし、サイトのアクティビティをデータベーステーブルに記録します。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-109">In this Hands-on Lab you will create a custom action filter attribute into MvcMusicStore solution to catch controller's requests and log the activity of a site into a database table.</span></span> <span data-ttu-id="f5f7c-110">任意のコントローラーまたはアクションに挿入することによって、ログ記録フィルターを追加することができます。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-110">You will be able to add your logging filter by injection to any controller or action.</span></span> <span data-ttu-id="f5f7c-111">最後に、訪問者の一覧を示すログビューが表示されます。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-111">Finally, you will see the log view that shows the list of visitors.</span></span>

<span data-ttu-id="f5f7c-112">このハンズオンラボでは、 **ASP.NET MVC**に関する基本的な知識があることを前提としています。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-112">This Hands-on Lab assumes you have basic knowledge of **ASP.NET MVC**.</span></span> <span data-ttu-id="f5f7c-113">以前に**ASP.NET mvc**を使用していない場合は、 **ASP.NET Mvc 4 の基礎**となるハンズオンラボに進むことをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-113">If you have not used **ASP.NET MVC** before, we recommend you to go over **ASP.NET MVC 4 Fundamentals** Hands-on Lab.</span></span>

> [!NOTE]
> <span data-ttu-id="f5f7c-114">すべてのサンプルコードとスニペットは、 [Microsoft web/WebCampTrainingKit リリース](https://aka.ms/webcamps-training-kit)から入手できる Web キャンプトレーニングキットに含まれています。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-114">All sample code and snippets are included in the Web Camps Training Kit, available from at [Microsoft-Web/WebCampTrainingKit Releases](https://aka.ms/webcamps-training-kit).</span></span> <span data-ttu-id="f5f7c-115">このラボに固有のプロジェクトは、 [ASP.NET MVC 4 カスタムアクションフィルター](https://github.com/Microsoft-Web/HOL-MVC4CustomActionFilters)で入手できます。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-115">The project specific to this lab is available at [ASP.NET MVC 4 Custom Action Filters](https://github.com/Microsoft-Web/HOL-MVC4CustomActionFilters).</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="f5f7c-116">目標</span><span class="sxs-lookup"><span data-stu-id="f5f7c-116">Objectives</span></span>

<span data-ttu-id="f5f7c-117">このハンズオンラボでは、次の方法を学習します。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-117">In this Hands-On Lab, you will learn how to:</span></span>

- <span data-ttu-id="f5f7c-118">フィルター機能を拡張するカスタムアクションフィルター属性を作成する</span><span class="sxs-lookup"><span data-stu-id="f5f7c-118">Create a custom action filter attribute to extend filtering capabilities</span></span>
- <span data-ttu-id="f5f7c-119">特定のレベルへの挿入によるカスタムフィルター属性の適用</span><span class="sxs-lookup"><span data-stu-id="f5f7c-119">Apply a custom filter attribute by injection to a specific level</span></span>
- <span data-ttu-id="f5f7c-120">カスタムアクションフィルターをグローバルに登録する</span><span class="sxs-lookup"><span data-stu-id="f5f7c-120">Register a custom action filters globally</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="f5f7c-121">前提条件</span><span class="sxs-lookup"><span data-stu-id="f5f7c-121">Prerequisites</span></span>

<span data-ttu-id="f5f7c-122">このラボを完了するには、次の項目が必要です。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-122">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="f5f7c-123">Web またはそれ以降[の2012を Microsoft Visual Studio Express](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web)ます (付録 a をインストールする手順については[、「付録 a](#AppendixA) 」を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-123">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="f5f7c-124">セットアップ</span><span class="sxs-lookup"><span data-stu-id="f5f7c-124">Setup</span></span>

<span data-ttu-id="f5f7c-125">**コードスニペットのインストール**</span><span class="sxs-lookup"><span data-stu-id="f5f7c-125">**Installing Code Snippets**</span></span>

<span data-ttu-id="f5f7c-126">便宜上、このラボで管理するコードの多くは、Visual Studio のコードスニペットとして提供されています。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-126">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="f5f7c-127">コードスニペットをインストールするには、 **.\Source\Setup\CodeSnippets.vsi**ファイルを実行します。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-127">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="f5f7c-128">Visual Studio Code のスニペットを使い慣れておらず、その使用方法を学習したい場合は、この &quot;ドキュメントの付録「[付録 C: コードスニペットの使用](#AppendixC)&quot;」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-128">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix C: Using Code Snippets](#AppendixC)&quot;.</span></span>

---

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="f5f7c-129">手順</span><span class="sxs-lookup"><span data-stu-id="f5f7c-129">Exercises</span></span>

<span data-ttu-id="f5f7c-130">このハンズオンラボは、次の演習によって構成されています。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-130">This Hands-On Lab is comprised by the following exercises:</span></span>

1. [<span data-ttu-id="f5f7c-131">演習 1: 操作のログ記録</span><span class="sxs-lookup"><span data-stu-id="f5f7c-131">Exercise 1: Logging actions</span></span>](#Exercise1)
2. [<span data-ttu-id="f5f7c-132">演習 2: 複数のアクションフィルターの管理</span><span class="sxs-lookup"><span data-stu-id="f5f7c-132">Exercise 2: Managing Multiple Action Filters</span></span>](#Exercise2)

<span data-ttu-id="f5f7c-133">このラボの推定所要時間: **30 分**。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-133">Estimated time to complete this lab: **30 minutes**.</span></span>

> [!NOTE]
> <span data-ttu-id="f5f7c-134">各演習には、演習を完了した後に取得する必要があるソリューションを含む**終了**フォルダーが付属しています。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-134">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="f5f7c-135">演習を通じて追加のヘルプが必要な場合は、このソリューションをガイドとして使用できます。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-135">You can use this solution as a guide if you need additional help working through the exercises.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Logging_Actions"></a>
### <a name="exercise-1-logging-actions"></a><span data-ttu-id="f5f7c-136">演習 1: 操作のログ記録</span><span class="sxs-lookup"><span data-stu-id="f5f7c-136">Exercise 1: Logging Actions</span></span>

<span data-ttu-id="f5f7c-137">この演習では、ASP.NET MVC 4 フィルタープロバイダーを使用してカスタムアクションログフィルターを作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-137">In this exercise, you will learn how to create a custom action log filter by using ASP.NET MVC 4 Filter Providers.</span></span> <span data-ttu-id="f5f7c-138">そのため、選択したコントローラー内のすべてのアクティビティを記録するログフィルターを MusicStore サイトに適用します。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-138">For that purpose you will apply a logging filter to the MusicStore site that will record all the activities in the selected controllers.</span></span>

<span data-ttu-id="f5f7c-139">フィルターは**Actionfilter属性 eclass**を拡張し、 **onactionexecuting**メソッドをオーバーライドして各要求をキャッチし、ログアクションを実行します。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-139">The filter will extend **ActionFilterAttributeClass** and override **OnActionExecuting** method to catch each request and then perform the logging actions.</span></span> <span data-ttu-id="f5f7c-140">HTTP 要求、実行メソッド、結果、およびパラメーターに関するコンテキスト情報は、ASP.NET MVC **Actionexecutingcontext**クラスによって提供され**ます。**</span><span class="sxs-lookup"><span data-stu-id="f5f7c-140">The context information about HTTP requests, executing methods, results and parameters will be provided by ASP.NET MVC **ActionExecutingContext** class **.**</span></span>

> [!NOTE]
> <span data-ttu-id="f5f7c-141">ASP.NET MVC 4 には、カスタムフィルターを作成せずに使用できる既定のフィルタープロバイダーもあります。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-141">ASP.NET MVC 4 also has default filters providers you can use without creating a custom filter.</span></span> <span data-ttu-id="f5f7c-142">ASP.NET MVC 4 には、次の種類のフィルターが用意されています。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-142">ASP.NET MVC 4 provides the following types of filters:</span></span>
> 
> - <span data-ttu-id="f5f7c-143">**承認**フィルター。認証の実行、要求のプロパティの検証など、アクションメソッドを実行するかどうかに関するセキュリティ上の決定を行います。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-143">**Authorization** filter, which makes security decisions about whether to execute an action method, such as performing authentication or validating properties of the request.</span></span>
> - <span data-ttu-id="f5f7c-144">**アクションフィルター。** アクションメソッドの実行をラップします。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-144">**Action** filter, which wraps the action method execution.</span></span> <span data-ttu-id="f5f7c-145">このフィルターでは、アクションメソッドへの追加データの提供、戻り値の検査、アクションメソッドの実行の取り消しなど、追加の処理を実行できます。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-145">This filter can perform additional processing, such as providing extra data to the action method, inspecting the return value, or canceling execution of the action method</span></span>
> - <span data-ttu-id="f5f7c-146">**結果**フィルター。 actionresult オブジェクトの実行をラップします。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-146">**Result** filter, which wraps execution of the ActionResult object.</span></span> <span data-ttu-id="f5f7c-147">このフィルターは、HTTP 応答の変更など、結果の追加処理を実行できます。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-147">This filter can perform additional processing of the result, such as modifying the HTTP response.</span></span>
> - <span data-ttu-id="f5f7c-148">**例外**フィルター。アクションメソッドのどこかでスローされた未処理の例外がある場合に実行されます。承認フィルターから開始し、結果の実行で終了します。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-148">**Exception** filter, which executes if there is an unhandled exception thrown somewhere in action method, starting with the authorization filters and ending with the execution of the result.</span></span> <span data-ttu-id="f5f7c-149">例外フィルターは、ログの記録やエラー ページの表示などのタスクに使用できます。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-149">Exception filters can be used for tasks such as logging or displaying an error page.</span></span>
> 
> <span data-ttu-id="f5f7c-150">フィルタープロバイダーの詳細については、こちらの MSDN リンク ([https://msdn.microsoft.com/library/dd410209.aspx](https://msdn.microsoft.com/library/dd410209.aspx)) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-150">For more information about Filters Providers please visit this MSDN link: ([https://msdn.microsoft.com/library/dd410209.aspx](https://msdn.microsoft.com/library/dd410209.aspx)) .</span></span>

<a id="AboutLoggingFeature"></a>

<a id="About_MVC_Music_Store_Application_logging_feature"></a>
#### <a name="about-mvc-music-store-application-logging-feature"></a><span data-ttu-id="f5f7c-151">MVC ミュージックストアアプリケーションログ機能について</span><span class="sxs-lookup"><span data-stu-id="f5f7c-151">About MVC Music Store Application logging feature</span></span>

<span data-ttu-id="f5f7c-152">このミュージックストアソリューションには、サイトログ、 **Actionlog**の新しいデータモデルテーブルがあります。このフィールドには、要求を受信したコントローラーの名前 (Action、Client IP、および Time stamp) が含まれています。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-152">This Music Store solution has a new data model table for site logging, **ActionLog**, with the following fields: Name of the controller that received a request, Called action, Client IP and Time stamp.</span></span>

<span data-ttu-id="f5f7c-153">![データモデル。ActionLog テーブル。](aspnet-mvc-4-custom-action-filters/_static/image1.png "データモデル。ActionLog テーブル。")</span><span class="sxs-lookup"><span data-stu-id="f5f7c-153">![Data model. ActionLog table.](aspnet-mvc-4-custom-action-filters/_static/image1.png "Data model. ActionLog table.")</span></span>

<span data-ttu-id="f5f7c-154">*データモデル-ActionLog テーブル*</span><span class="sxs-lookup"><span data-stu-id="f5f7c-154">*Data model - ActionLog table*</span></span>

<span data-ttu-id="f5f7c-155">このソリューションには、アクションログの ASP.NET MVC ビューが用意されています。これは、 **MvcMusicStores/Views/ActionLog**にあります。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-155">The solution provides an ASP.NET MVC View for the Action log that can be found at **MvcMusicStores/Views/ActionLog**:</span></span>

<span data-ttu-id="f5f7c-156">![操作ログの表示](aspnet-mvc-4-custom-action-filters/_static/image2.png "操作ログの表示")</span><span class="sxs-lookup"><span data-stu-id="f5f7c-156">![Action Log view](aspnet-mvc-4-custom-action-filters/_static/image2.png "Action Log view")</span></span>

<span data-ttu-id="f5f7c-157">*操作ログの表示*</span><span class="sxs-lookup"><span data-stu-id="f5f7c-157">*Action Log view*</span></span>

<span data-ttu-id="f5f7c-158">この構造では、すべての作業はコントローラーの要求を中断し、カスタムフィルターを使用してログ記録を実行します。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-158">With this given structure, all the work will be focused on interrupting controller's request and performing the logging by using custom filtering.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_a_Custom_Filter_to_Catch_a_Controllers_Request"></a>
#### <a name="task-1---creating-a-custom-filter-to-catch-a-controllers-request"></a><span data-ttu-id="f5f7c-159">タスク 1-コントローラーの要求をキャッチするカスタムフィルターを作成する</span><span class="sxs-lookup"><span data-stu-id="f5f7c-159">Task 1 - Creating a Custom Filter to Catch a Controller's Request</span></span>

<span data-ttu-id="f5f7c-160">この作業では、ログ記録ロジックを含むカスタムフィルター属性クラスを作成します。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-160">In this task you will create a custom filter attribute class that will contain the logging logic.</span></span> <span data-ttu-id="f5f7c-161">そのためには、ASP.NET MVC **Actionfilterattribute**クラスを拡張し、インターフェイス**iactionfilter**を実装します。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-161">For that purpose you will extend ASP.NET MVC **ActionFilterAttribute** Class and implement the interface **IActionFilter**.</span></span>

> [!NOTE]
> <span data-ttu-id="f5f7c-162">**Actionfilterattribute**は、すべての属性フィルターの基本クラスです。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-162">The **ActionFilterAttribute** is the base class for all the attribute filters.</span></span> <span data-ttu-id="f5f7c-163">このメソッドには、コントローラーアクションの実行後および実行前に特定のロジックを実行するための次のメソッドが用意されています。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-163">It provides the following methods to execute a specific logic after and before controller action's execution:</span></span>
> 
> - <span data-ttu-id="f5f7c-164">**Onactionexecuting**(actionexecutingcontext filtercontext): アクションメソッドが呼び出される直前。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-164">**OnActionExecuting**(ActionExecutingContext filterContext): Just before the action method is called.</span></span>
> - <span data-ttu-id="f5f7c-165">**Onactionexecuted**(actionexecutedcontext filtercontext): アクションメソッドが呼び出された後、結果が実行される前 (ビューレンダリングの前)。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-165">**OnActionExecuted**(ActionExecutedContext filterContext): After the action method is called and before the result is executed (before view render).</span></span>
> - <span data-ttu-id="f5f7c-166">**Onresultexecuting**(resultexecutingcontext filtercontext): 結果が実行される直前 (ビューレンダリングの前)。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-166">**OnResultExecuting**(ResultExecutingContext filterContext): Just before the result is executed (before view render).</span></span>
> - <span data-ttu-id="f5f7c-167">**Onresultexecuted**(resultexecutedcontext filtercontext): 結果が実行された後 (ビューが表示された後)。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-167">**OnResultExecuted**(ResultExecutedContext filterContext): After the result is executed (after the view is rendered).</span></span>
> 
> <span data-ttu-id="f5f7c-168">これらのメソッドのいずれかを派生クラスにオーバーライドすることにより、独自のフィルター処理コードを実行できます。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-168">By overriding any of these methods into a derived class, you can execute your own filtering code.</span></span>

1. <span data-ttu-id="f5f7c-169">**\ Source\ Ex01-のジョブ \ 開始**フォルダーにある**begin**ソリューションを開きます。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-169">Open the **Begin** solution located at **\Source\Ex01-LoggingActions\Begin** folder.</span></span>

   1. <span data-ttu-id="f5f7c-170">続行する前に、不足している NuGet パッケージをダウンロードする必要があります。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-170">You will need to download some missing NuGet packages before you continue.</span></span> <span data-ttu-id="f5f7c-171">これを行うには、 **[プロジェクト]** メニューをクリックし、 **[NuGet パッケージの管理]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-171">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="f5f7c-172">**[NuGet パッケージの管理]** ダイアログで、 **[復元]** をクリックして、不足しているパッケージをダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-172">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="f5f7c-173">最後に、[**ビルド** | **ビルド**] をクリックしてソリューションをビルドします。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-173">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="f5f7c-174">NuGet を使用する利点の1つは、プロジェクトのすべてのライブラリを配布する必要がなく、プロジェクトのサイズを小さくすることです。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-174">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="f5f7c-175">NuGet パワーツールを使用すると、パッケージのバージョンを app.config ファイルで指定することで、プロジェクトを初めて実行するときに必要なすべてのライブラリをダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-175">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="f5f7c-176">このため、このラボから既存のソリューションを開いた後に、これらの手順を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-176">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
      > 
      > <span data-ttu-id="f5f7c-177">詳細については、「 [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-177">For more information, see this article: [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages).</span></span>
2. <span data-ttu-id="f5f7c-178">Filters フォルダーにC#新しいクラスを追加し、 *CustomActionFilter.cs*という名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-178">Add a new C# class into the **Filters** folder and name it *CustomActionFilter.cs*.</span></span> <span data-ttu-id="f5f7c-179">このフォルダーには、すべてのカスタムフィルターが格納されます。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-179">This folder will store all the custom filters.</span></span>
3. <span data-ttu-id="f5f7c-180">**CustomActionFilter.cs**を開き、 **MvcMusicStore**名前空間と名前**空間への**参照を追加します。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-180">Open **CustomActionFilter.cs** and add a reference to **System.Web.Mvc** and **MvcMusicStore.Models** namespaces:</span></span>

    <span data-ttu-id="f5f7c-181">(コードスニペット- *ASP.NET MVC 4 カスタムアクションフィルター-Ex1-CustomActionFilterNamespaces*)</span><span class="sxs-lookup"><span data-stu-id="f5f7c-181">(Code Snippet - *ASP.NET MVC 4 Custom Action Filters - Ex1-CustomActionFilterNamespaces*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample1.cs)]
4. <span data-ttu-id="f5f7c-182">**Actionfilterattribute**から**CustomActionFilter**クラスを継承し、 **CustomActionFilter**クラスが**iactionfilter**インターフェイスを実装するようにします。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-182">Inherit the **CustomActionFilter** class from **ActionFilterAttribute** and then make **CustomActionFilter** class implement **IActionFilter** interface.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample2.cs)]
5. <span data-ttu-id="f5f7c-183">**CustomActionFilter**クラスは、 **onactionexecuting**メソッドをオーバーライドし、フィルターの実行をログに記録するために必要なロジックを追加します。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-183">Make **CustomActionFilter** class override the method **OnActionExecuting** and add the necessary logic to log the filter's execution.</span></span> <span data-ttu-id="f5f7c-184">これを行うには、 **CustomActionFilter**クラス内に次の強調表示されたコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-184">To do this, add the following highlighted code within **CustomActionFilter** class.</span></span>

    <span data-ttu-id="f5f7c-185">(コードスニペット- *ASP.NET MVC 4 カスタムアクションフィルター-Ex1-ログインアクション*)</span><span class="sxs-lookup"><span data-stu-id="f5f7c-185">(Code Snippet - *ASP.NET MVC 4 Custom Action Filters - Ex1-LoggingActions*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample3.cs#Highlight)]

    > [!NOTE]
    > <span data-ttu-id="f5f7c-186">**Onactionexecuting**メソッドでは**Entity Framework**を使用して新しい actionlog レジスタを追加しています。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-186">**OnActionExecuting** method is using **Entity Framework** to add a new ActionLog register.</span></span> <span data-ttu-id="f5f7c-187">**Filtercontext**からのコンテキスト情報を使用して、新しいエンティティインスタンスを作成して入力します。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-187">It creates and fills a new entity instance with the context information from **filterContext**.</span></span>
    > 
    > <span data-ttu-id="f5f7c-188">**コントローラーのコントローラー**の詳細については、 [msdn](https://msdn.microsoft.com/library/system.web.mvc.controllercontext.aspx)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-188">You can read more about **ControllerContext** class at [msdn](https://msdn.microsoft.com/library/system.web.mvc.controllercontext.aspx).</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Injecting_a_Code_Interceptor_into_the_Store_Controller_Class"></a>
#### <a name="task-2---injecting-a-code-interceptor-into-the-store-controller-class"></a><span data-ttu-id="f5f7c-189">タスク 2-ストアコントローラークラスにコードインターセプターを挿入する</span><span class="sxs-lookup"><span data-stu-id="f5f7c-189">Task 2 - Injecting a Code Interceptor into the Store Controller Class</span></span>

<span data-ttu-id="f5f7c-190">このタスクでは、ログに記録されるすべてのコントローラークラスとコントローラーアクションにカスタムフィルターを挿入することによって、カスタムフィルターを追加します。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-190">In this task you will add the custom filter by injecting it to all controller classes and controller actions that will be logged.</span></span> <span data-ttu-id="f5f7c-191">この演習では、Store Controller クラスにログがあります。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-191">For the purpose of this exercise, the Store Controller class will have a log.</span></span>

<span data-ttu-id="f5f7c-192">**Actionlogfilterattribute**カスタムフィルターから実行されるメソッド**onactionexecuting** 、挿入された要素が呼び出されると実行されます。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-192">The method **OnActionExecuting** from **ActionLogFilterAttribute** custom filter runs when an injected element is called.</span></span>

<span data-ttu-id="f5f7c-193">特定のコントローラーメソッドをインターセプトすることもできます。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-193">It is also possible to intercept a specific controller method.</span></span>

1. <span data-ttu-id="f5f7c-194">**MvcMusicStore\Controllers**で**StoreController**を開き、 **Filters**名前空間への参照を追加します。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-194">Open the **StoreController** at **MvcMusicStore\Controllers** and add a reference to the **Filters** namespace:</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample4.cs)]
2. <span data-ttu-id="f5f7c-195">クラス宣言の前に **[CustomActionFilter]** 属性を追加して、カスタムフィルター **CustomActionFilter**を**StoreController**クラスに挿入します。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-195">Inject the custom filter **CustomActionFilter** into **StoreController** class by adding **[CustomActionFilter]** attribute before the class declaration.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample5.cs)]

   > [!NOTE]
   > <span data-ttu-id="f5f7c-196">フィルターがコントローラークラスに挿入されると、そのすべてのアクションも挿入されます。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-196">When a filter is injected into a controller class, all its actions are also injected.</span></span> <span data-ttu-id="f5f7c-197">一連のアクションに対してのみフィルターを適用する場合は、 **[CustomActionFilter]** をそれぞれに挿入する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-197">If you would like to apply the filter only for a set of actions, you would have to inject **[CustomActionFilter]** to each one of them:</span></span>
   > 
   > [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample6.cs)]

<a id="Ex1Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a><span data-ttu-id="f5f7c-198">タスク 3-アプリケーションを実行する</span><span class="sxs-lookup"><span data-stu-id="f5f7c-198">Task 3 - Running the Application</span></span>

<span data-ttu-id="f5f7c-199">このタスクでは、ログ記録フィルターが機能していることをテストします。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-199">In this task, you will test that the logging filter is working.</span></span> <span data-ttu-id="f5f7c-200">アプリケーションを起動してストアにアクセスし、ログに記録されたアクティビティを確認します。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-200">You will start the application and visit the store, and then you will check logged activities.</span></span>

1. <span data-ttu-id="f5f7c-201">**F5** キーを押してアプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-201">Press **F5** to run the application.</span></span>
2. <span data-ttu-id="f5f7c-202">**/Actionlog**を参照して、ログビューの初期状態を確認します。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-202">Browse to **/ActionLog** to see log view initial state:</span></span>

    <span data-ttu-id="f5f7c-203">![ページアクティビティ前のログトラッカーの状態](aspnet-mvc-4-custom-action-filters/_static/image3.png "ページアクティビティ前のログトラッカーの状態")</span><span class="sxs-lookup"><span data-stu-id="f5f7c-203">![Log tracker status before page activity](aspnet-mvc-4-custom-action-filters/_static/image3.png "Log tracker status before page activity")</span></span>

    <span data-ttu-id="f5f7c-204">*ページアクティビティ前のログトラッカーの状態*</span><span class="sxs-lookup"><span data-stu-id="f5f7c-204">*Log tracker status before page activity*</span></span>

   > [!NOTE]
   > <span data-ttu-id="f5f7c-205">既定では、メニューの既存のジャンルを取得するときに生成される1つの項目が常に表示されます。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-205">By default, it will always show one item that is generated when retrieving the existing genres for the menu.</span></span>
   > 
   > <span data-ttu-id="f5f7c-206">わかりやすくするために、アプリケーションを実行するたびに**Actionlog**テーブルをクリーンアップしています。これにより、各タスクの検証のログのみが表示されるようになります。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-206">For simplicity purposes we're cleaning up the **ActionLog** table each time the application runs so it will only show the logs of each particular task's verification.</span></span>
   > 
   > <span data-ttu-id="f5f7c-207">ストアコントローラー内で実行されるすべてのアクションの履歴ログを保存するために、**セッション\_Start**メソッド ( **global.asax**クラス) から次のコードを削除する必要がある場合があります。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-207">You might need to remove the following code from the **Session\_Start** method (in the **Global.asax** class), in order to save an historical log for all the actions executed within the Store Controller.</span></span>
   > 
   > [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample7.cs)]
3. <span data-ttu-id="f5f7c-208">メニューからいずれかの**ジャンル**をクリックし、利用可能なアルバムの閲覧など、いくつかの操作を実行します。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-208">Click one of the **Genres** from the menu and perform some actions there, like browsing an available album.</span></span>
4. <span data-ttu-id="f5f7c-209">**/Actionlog**を参照し、ログが空の場合は**F5**キーを押してページを更新します。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-209">Browse to **/ActionLog** and if the log is empty press **F5** to refresh the page.</span></span> <span data-ttu-id="f5f7c-210">訪問が追跡されたことを確認します。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-210">Check that your visits were tracked:</span></span>

    <span data-ttu-id="f5f7c-211">![アクティビティが記録されたアクションログ](aspnet-mvc-4-custom-action-filters/_static/image4.png "アクティビティが記録されたアクションログ")</span><span class="sxs-lookup"><span data-stu-id="f5f7c-211">![Action log with activity logged](aspnet-mvc-4-custom-action-filters/_static/image4.png "Action log with activity logged")</span></span>

    <span data-ttu-id="f5f7c-212">*アクティビティが記録されたアクションログ*</span><span class="sxs-lookup"><span data-stu-id="f5f7c-212">*Action log with activity logged*</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Managing_Multiple_Action_Filters"></a>
### <a name="exercise-2-managing-multiple-action-filters"></a><span data-ttu-id="f5f7c-213">演習 2: 複数のアクションフィルターの管理</span><span class="sxs-lookup"><span data-stu-id="f5f7c-213">Exercise 2: Managing Multiple Action Filters</span></span>

<span data-ttu-id="f5f7c-214">この演習では、StoreController クラスに2つ目のカスタムアクションフィルターを追加し、両方のフィルターが実行される特定の順序を定義します。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-214">In this exercise you will add a second Custom Action Filter to the StoreController class and define the specific order in which both filters will be executed.</span></span> <span data-ttu-id="f5f7c-215">次に、フィルターをグローバルに登録するようにコードを更新します。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-215">Then you will update the code to register the filter Globally.</span></span>

<span data-ttu-id="f5f7c-216">フィルターの実行順序を定義する際には、さまざまなオプションを考慮する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-216">There are different options to take into account when defining the Filters' execution order.</span></span> <span data-ttu-id="f5f7c-217">たとえば、Order プロパティとフィルターのスコープは、次のようになります。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-217">For example, the Order property and the Filters' scope:</span></span>

<span data-ttu-id="f5f7c-218">フィルターごとに**スコープ**を定義できます。たとえば、**コントローラースコープ**内で実行するすべてのアクションフィルターと、**グローバルスコープ**で実行するすべての承認フィルターのスコープを設定できます。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-218">You can define a **Scope** for each of the Filters, for example, you could scope all the Action Filters to run within the **Controller Scope**, and all Authorization Filters to run in **Global scope**.</span></span> <span data-ttu-id="f5f7c-219">スコープには、定義済みの実行順序があります。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-219">The scopes have a defined execution order.</span></span>

<span data-ttu-id="f5f7c-220">また、各アクションフィルターには、フィルターのスコープ内で実行順序を決定するために使用される Order プロパティがあります。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-220">Additionally, each action filter has an Order property which is used to determine the execution order in the scope of the filter.</span></span>

<span data-ttu-id="f5f7c-221">カスタムアクションフィルターの実行順序の詳細については、MSDN の記事「([https://msdn.microsoft.com/library/dd381609(v=vs.98).aspx](https://msdn.microsoft.com/library/dd381609(v=vs.98).aspx))」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-221">For more information about Custom Action Filters execution order, please visit this MSDN article: ([https://msdn.microsoft.com/library/dd381609(v=vs.98).aspx](https://msdn.microsoft.com/library/dd381609(v=vs.98).aspx)).</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_Creating_a_new_Custom_Action_Filter"></a>
#### <a name="task-1-creating-a-new-custom-action-filter"></a><span data-ttu-id="f5f7c-222">タスク 1: 新しいカスタムアクションフィルターを作成する</span><span class="sxs-lookup"><span data-stu-id="f5f7c-222">Task 1: Creating a new Custom Action Filter</span></span>

<span data-ttu-id="f5f7c-223">このタスクでは、新しいカスタムアクションフィルターを作成して、StoreController クラスに挿入し、フィルターの実行順序を管理する方法を学習します。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-223">In this task, you will create a new Custom Action Filter to inject into the StoreController class, learning how to manage the execution order of the filters.</span></span>

1. <span data-ttu-id="f5f7c-224">**\Source\Ex02-ManagingMultipleActionFilters\Begin**フォルダーにある**Begin**ソリューションを開きます。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-224">Open the **Begin** solution located at **\Source\Ex02-ManagingMultipleActionFilters\Begin** folder.</span></span> <span data-ttu-id="f5f7c-225">それ以外の場合は、前の演習を完了することによって得られた**終了**ソリューションを引き続き使用することができます。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-225">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

    1. <span data-ttu-id="f5f7c-226">提供された**Begin**ソリューションを開いた場合は、続行する前に、不足している NuGet パッケージをダウンロードする必要があります。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-226">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="f5f7c-227">これを行うには、 **[プロジェクト]** メニューをクリックし、 **[NuGet パッケージの管理]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-227">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
    2. <span data-ttu-id="f5f7c-228">**[NuGet パッケージの管理]** ダイアログで、 **[復元]** をクリックして、不足しているパッケージをダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-228">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
    3. <span data-ttu-id="f5f7c-229">最後に、[**ビルド** | **ビルド**] をクリックしてソリューションをビルドします。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-229">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

        > [!NOTE]
        > <span data-ttu-id="f5f7c-230">NuGet を使用する利点の1つは、プロジェクトのすべてのライブラリを配布する必要がなく、プロジェクトのサイズを小さくすることです。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-230">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="f5f7c-231">NuGet パワーツールを使用すると、パッケージのバージョンを app.config ファイルで指定することで、プロジェクトを初めて実行するときに必要なすべてのライブラリをダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-231">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="f5f7c-232">このため、このラボから既存のソリューションを開いた後に、これらの手順を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-232">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
        > 
        > <span data-ttu-id="f5f7c-233">詳細については、「 [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-233">For more information, see this article: [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages).</span></span>
2. <span data-ttu-id="f5f7c-234">Filters フォルダーにC#新しいクラスを追加し、 *MyNewCustomActionFilter.cs*という名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-234">Add a new C# class into the **Filters** folder and name it *MyNewCustomActionFilter.cs*</span></span>
3. <span data-ttu-id="f5f7c-235">**MyNewCustomActionFilter.cs**を開き、 **system.web**および**MvcMusicStore**名前空間への参照を追加します。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-235">Open **MyNewCustomActionFilter.cs** and add a reference to **System.Web.Mvc** and the **MvcMusicStore.Models** namespace:</span></span>

    <span data-ttu-id="f5f7c-236">(コードスニペット- *ASP.NET MVC 4 カスタムアクションフィルター-Ex2-MyNewCustomActionFilterNamespaces*)</span><span class="sxs-lookup"><span data-stu-id="f5f7c-236">(Code Snippet - *ASP.NET MVC 4 Custom Action Filters - Ex2-MyNewCustomActionFilterNamespaces*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample8.cs)]
4. <span data-ttu-id="f5f7c-237">既定のクラス宣言を次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-237">Replace the default class declaration with the following code.</span></span>

    <span data-ttu-id="f5f7c-238">(コードスニペット- *ASP.NET MVC 4 カスタムアクションフィルター-Ex2-MyNewCustomActionFilterClass*)</span><span class="sxs-lookup"><span data-stu-id="f5f7c-238">(Code Snippet - *ASP.NET MVC 4 Custom Action Filters - Ex2-MyNewCustomActionFilterClass*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample9.cs)]

    > [!NOTE]
    > <span data-ttu-id="f5f7c-239">このカスタムアクションフィルターは、前の演習で作成したものとほぼ同じです。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-239">This Custom Action Filter is almost the same than the one you created in the previous exercise.</span></span> <span data-ttu-id="f5f7c-240">主な違いは、 *&quot;属性によって記録*された&quot;がこの新しいクラスの名前で更新され、どのフィルターがログに登録されたかを識別することです。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-240">The main difference is that it has the *&quot;Logged By&quot;* attribute updated with this new class' name to identify which filter registered the log.</span></span>

<a id="Ex2Task2"></a>

<a id="Task_2_Injecting_a_new_Code_Interceptor_into_the_StoreController_Class"></a>
#### <a name="task-2-injecting-a-new-code-interceptor-into-the-storecontroller-class"></a><span data-ttu-id="f5f7c-241">タスク 2: 新しいコードインターセプターを StoreController クラスに挿入する</span><span class="sxs-lookup"><span data-stu-id="f5f7c-241">Task 2: Injecting a new Code Interceptor into the StoreController Class</span></span>

<span data-ttu-id="f5f7c-242">このタスクでは、新しいカスタムフィルターを StoreController クラスに追加し、ソリューションを実行して、両方のフィルターが連携する方法を確認します。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-242">In this task, you will add a new custom filter into the StoreController Class and run the solution to verify how both filters work together.</span></span>

1. <span data-ttu-id="f5f7c-243">**MvcMusicStore\Controllers**にある**StoreController**クラスを開き、次のコードに示すように、新しいカスタムフィルター **MyNewCustomActionFilter**を**StoreController**クラスに挿入します。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-243">Open the **StoreController** class located at **MvcMusicStore\Controllers** and inject the new custom filter **MyNewCustomActionFilter** into **StoreController** class like is shown in the following code.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample10.cs)]
2. <span data-ttu-id="f5f7c-244">ここで、アプリケーションを実行して、これら2つのカスタムアクションフィルターがどのように機能するかを確認します。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-244">Now, run the application in order to see how these two Custom Action Filters work.</span></span> <span data-ttu-id="f5f7c-245">これを行うには、 **F5**キーを押して、アプリケーションが起動するまで待ちます。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-245">To do this, press **F5** and wait until the application starts.</span></span>
3. <span data-ttu-id="f5f7c-246">**/Actionlog**を参照して、ログビューの初期状態を確認します。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-246">Browse to **/ActionLog** to see log view initial state.</span></span>

    <span data-ttu-id="f5f7c-247">![ページアクティビティ前のログトラッカーの状態](aspnet-mvc-4-custom-action-filters/_static/image5.png "ページアクティビティ前のログトラッカーの状態")</span><span class="sxs-lookup"><span data-stu-id="f5f7c-247">![Log tracker status before page activity](aspnet-mvc-4-custom-action-filters/_static/image5.png "Log tracker status before page activity")</span></span>

    <span data-ttu-id="f5f7c-248">*ページアクティビティ前のログトラッカーの状態*</span><span class="sxs-lookup"><span data-stu-id="f5f7c-248">*Log tracker status before page activity*</span></span>
4. <span data-ttu-id="f5f7c-249">メニューからいずれかの**ジャンル**をクリックし、利用可能なアルバムの閲覧など、いくつかの操作を実行します。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-249">Click one of the **Genres** from the menu and perform some actions there, like browsing an available album.</span></span>
5. <span data-ttu-id="f5f7c-250">この時刻を確認してください。訪問が2回追跡されました。 **StorageController**クラスに追加したカスタムアクションフィルターごとに1回です。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-250">Check that this time; your visits were tracked twice: once for each of the Custom Action Filters you added in the **StorageController** class.</span></span>

    <span data-ttu-id="f5f7c-251">![アクティビティが記録されたアクションログ](aspnet-mvc-4-custom-action-filters/_static/image6.png "アクティビティが記録されたアクションログ")</span><span class="sxs-lookup"><span data-stu-id="f5f7c-251">![Action log with activity logged](aspnet-mvc-4-custom-action-filters/_static/image6.png "Action log with activity logged")</span></span>

    <span data-ttu-id="f5f7c-252">*アクティビティが記録されたアクションログ*</span><span class="sxs-lookup"><span data-stu-id="f5f7c-252">*Action log with activity logged*</span></span>
6. <span data-ttu-id="f5f7c-253">ブラウザーを閉じます。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-253">Close the browser.</span></span>

<a id="Ex2Task3"></a>

<a id="Task_3_Managing_Filter_Ordering"></a>
#### <a name="task-3-managing-filter-ordering"></a><span data-ttu-id="f5f7c-254">タスク 3: フィルターの順序を管理する</span><span class="sxs-lookup"><span data-stu-id="f5f7c-254">Task 3: Managing Filter Ordering</span></span>

<span data-ttu-id="f5f7c-255">このタスクでは、Order プロパティを使用してフィルターの実行順序を管理する方法を学習します。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-255">In this task, you will learn how to manage the filters' execution order by using the Order property.</span></span>

1. <span data-ttu-id="f5f7c-256">**MvcMusicStore\Controllers**にある**StoreController**クラスを開き、次に示すように、両方のフィルターで**Order**プロパティを指定します。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-256">Open the **StoreController** class located at **MvcMusicStore\Controllers** and specify the **Order** property in both filters like shown below.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample11.cs)]
2. <span data-ttu-id="f5f7c-257">次に、Order プロパティの値に応じて、フィルターがどのように実行されるかを確認します。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-257">Now, verify how the filters are executed depending on its Order property's value.</span></span> <span data-ttu-id="f5f7c-258">最小の順序の値 (**CustomActionFilter**) を持つフィルターが、最初に実行されるフィルターであることがわかります。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-258">You will find that the filter with the smallest Order value (**CustomActionFilter**) is the first one that is executed.</span></span> <span data-ttu-id="f5f7c-259">**F5**キーを押して、アプリケーションが起動するまで待ちます。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-259">Press **F5** and wait until the application starts.</span></span>
3. <span data-ttu-id="f5f7c-260">**/Actionlog**を参照して、ログビューの初期状態を確認します。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-260">Browse to **/ActionLog** to see log view initial state.</span></span>

    <span data-ttu-id="f5f7c-261">![ページアクティビティ前のログトラッカーの状態](aspnet-mvc-4-custom-action-filters/_static/image7.png "ページアクティビティ前のログトラッカーの状態")</span><span class="sxs-lookup"><span data-stu-id="f5f7c-261">![Log tracker status before page activity](aspnet-mvc-4-custom-action-filters/_static/image7.png "Log tracker status before page activity")</span></span>

    <span data-ttu-id="f5f7c-262">*ページアクティビティ前のログトラッカーの状態*</span><span class="sxs-lookup"><span data-stu-id="f5f7c-262">*Log tracker status before page activity*</span></span>
4. <span data-ttu-id="f5f7c-263">メニューからいずれかの**ジャンル**をクリックし、利用可能なアルバムの閲覧など、いくつかの操作を実行します。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-263">Click one of the **Genres** from the menu and perform some actions there, like browsing an available album.</span></span>
5. <span data-ttu-id="f5f7c-264">この時間が経過すると、最初にフィルターの順序値: **CustomActionFilter** logs によってアクセスが追跡されることを確認します。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-264">Check that this time, your visits were tracked ordered by the filters' Order value: **CustomActionFilter** logs' first.</span></span>

    <span data-ttu-id="f5f7c-265">![アクティビティが記録されたアクションログ](aspnet-mvc-4-custom-action-filters/_static/image8.png "アクティビティが記録されたアクションログ")</span><span class="sxs-lookup"><span data-stu-id="f5f7c-265">![Action log with activity logged](aspnet-mvc-4-custom-action-filters/_static/image8.png "Action log with activity logged")</span></span>

    <span data-ttu-id="f5f7c-266">*アクティビティが記録されたアクションログ*</span><span class="sxs-lookup"><span data-stu-id="f5f7c-266">*Action log with activity logged*</span></span>
6. <span data-ttu-id="f5f7c-267">ここで、フィルターの順序の値を更新し、ログの順序がどのように変わるかを確認します。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-267">Now, you will update the Filters' order value and verify how the logging order changes.</span></span> <span data-ttu-id="f5f7c-268">**StoreController**クラスで、フィルターの順序の値を次のように更新します。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-268">In the **StoreController** class, update the Filters' Order value like shown below.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample12.cs)]
7. <span data-ttu-id="f5f7c-269">**F5**キーを押してアプリケーションを再実行します。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-269">Run the application again by pressing **F5**.</span></span>
8. <span data-ttu-id="f5f7c-270">メニューからいずれかの**ジャンル**をクリックし、利用可能なアルバムの閲覧など、いくつかの操作を実行します。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-270">Click one of the **Genres** from the menu and perform some actions there, like browsing an available album.</span></span>
9. <span data-ttu-id="f5f7c-271">この時間が経過すると、 **MyNewCustomActionFilter** filter によって作成されたログが先に表示されます。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-271">Check that this time, the logs created by **MyNewCustomActionFilter** filter appears first.</span></span>

    <span data-ttu-id="f5f7c-272">![アクティビティが記録されたアクションログ](aspnet-mvc-4-custom-action-filters/_static/image9.png "アクティビティが記録されたアクションログ")</span><span class="sxs-lookup"><span data-stu-id="f5f7c-272">![Action log with activity logged](aspnet-mvc-4-custom-action-filters/_static/image9.png "Action log with activity logged")</span></span>

    <span data-ttu-id="f5f7c-273">*アクティビティが記録されたアクションログ*</span><span class="sxs-lookup"><span data-stu-id="f5f7c-273">*Action log with activity logged*</span></span>

<a id="Ex2Task4"></a>

<a id="Task_4_Registering_Filters_Globally"></a>
#### <a name="task-4-registering-filters-globally"></a><span data-ttu-id="f5f7c-274">タスク 4: フィルターをグローバルに登録する</span><span class="sxs-lookup"><span data-stu-id="f5f7c-274">Task 4: Registering Filters Globally</span></span>

<span data-ttu-id="f5f7c-275">このタスクでは、新しいフィルター (**MyNewCustomActionFilter**) をグローバルフィルターとして登録するようにソリューションを更新します。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-275">In this task, you will update the solution to register the new filter (**MyNewCustomActionFilter**) as a global filter.</span></span> <span data-ttu-id="f5f7c-276">これにより、アプリケーションで実行されるすべてのアクションによってトリガーされます。前のタスクと同様に、StoreController のすべてのアクションがトリガーされます。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-276">By doing this, it will be triggered by all the actions performed in the application and not only in the StoreController ones as in the previous task.</span></span>

1. <span data-ttu-id="f5f7c-277">**StoreController**クラスで、[ **MyNewCustomActionFilter]** 属性と Order プロパティを **[CustomActionFilter]** から削除します。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-277">In **StoreController** class, remove **[MyNewCustomActionFilter]** attribute and the order property from **[CustomActionFilter]**.</span></span> <span data-ttu-id="f5f7c-278">この要素は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-278">It should look like the following:</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample13.cs)]
2. <span data-ttu-id="f5f7c-279">**Global.asax**ファイルを開き、 **Application\_Start**メソッドを見つけます。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-279">Open **Global.asax** file and locate the **Application\_Start** method.</span></span> <span data-ttu-id="f5f7c-280">アプリケーションが起動するたびに、 **Filterconfig**クラス内で**registerglobalfilters**メソッドを呼び出すことによってグローバルフィルターが登録されることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-280">Notice that each time the application starts it is registering the global filters by calling **RegisterGlobalFilters** method within **FilterConfig** class.</span></span>

    <span data-ttu-id="f5f7c-281">![グローバルフィルターを global.asax に登録しています](aspnet-mvc-4-custom-action-filters/_static/image10.png "グローバルフィルターを global.asax に登録しています")</span><span class="sxs-lookup"><span data-stu-id="f5f7c-281">![Registering Global Filters in Global.asax](aspnet-mvc-4-custom-action-filters/_static/image10.png "Registering Global Filters in Global.asax")</span></span>

    <span data-ttu-id="f5f7c-282">*グローバルフィルターを global.asax に登録しています*</span><span class="sxs-lookup"><span data-stu-id="f5f7c-282">*Registering Global Filters in Global.asax*</span></span>
3. <span data-ttu-id="f5f7c-283">**アプリ\_** の [開始フォルダー] で**FilterConfig.cs**ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-283">Open **FilterConfig.cs** file within **App\_Start** folder.</span></span>
4. <span data-ttu-id="f5f7c-284">System.web. Mvc を使用してへの参照を追加します。MvcMusicStore を使用します。空間.</span><span class="sxs-lookup"><span data-stu-id="f5f7c-284">Add a reference to using System.Web.Mvc; using MvcMusicStore.Filters; namespace.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample14.cs)]
5. <span data-ttu-id="f5f7c-285">**Registerglobalfilters**メソッドを更新して、カスタムフィルターを追加します。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-285">Update **RegisterGlobalFilters** method adding your custom filter.</span></span> <span data-ttu-id="f5f7c-286">これを行うには、強調表示されたコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-286">To do this, add the highlighted code:</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample15.cs)]
6. <span data-ttu-id="f5f7c-287">**F5** キーを押してアプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-287">Run the application by pressing **F5**.</span></span>
7. <span data-ttu-id="f5f7c-288">メニューからいずれかの**ジャンル**をクリックし、利用可能なアルバムの閲覧など、いくつかの操作を実行します。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-288">Click one of the **Genres** from the menu and perform some actions there, like browsing an available album.</span></span>
8. <span data-ttu-id="f5f7c-289">今すぐ **[MyNewCustomActionFilter]** が HomeController と ActionLogController に挿入されていることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-289">Check that now **[MyNewCustomActionFilter]** is being injected in HomeController and ActionLogController too.</span></span>

    <span data-ttu-id="f5f7c-290">![アクティビティが記録されたアクションログ](aspnet-mvc-4-custom-action-filters/_static/image11.png "アクティビティが記録されたアクションログ")</span><span class="sxs-lookup"><span data-stu-id="f5f7c-290">![Action log with activity logged](aspnet-mvc-4-custom-action-filters/_static/image11.png "Action log with activity logged")</span></span>

    <span data-ttu-id="f5f7c-291">*グローバルアクティビティが記録されたアクションログ*</span><span class="sxs-lookup"><span data-stu-id="f5f7c-291">*Action log with global activity logged*</span></span>

> [!NOTE]
> <span data-ttu-id="f5f7c-292">また、 [「付録 B: Web 配置を使用した ASP.NET MVC 4 アプリケーションの発行](#AppendixB)」に従って、このアプリケーションを Windows Azure の Web サイトにデプロイすることもできます。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-292">Additionally, you can deploy this application to Windows Azure Web Sites following [Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy](#AppendixB).</span></span>

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="f5f7c-293">まとめ</span><span class="sxs-lookup"><span data-stu-id="f5f7c-293">Summary</span></span>

<span data-ttu-id="f5f7c-294">このハンズオンラボでは、アクションフィルターを拡張してカスタムアクションを実行する方法について学習しました。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-294">By completing this Hands-On Lab you have learned how to extend an action filter to execute custom actions.</span></span> <span data-ttu-id="f5f7c-295">また、任意のフィルターをページコントローラーに挿入する方法についても学習しました。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-295">You have also learned how to inject any filter to your page controllers.</span></span> <span data-ttu-id="f5f7c-296">次の概念が使用されました。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-296">The following concepts were used:</span></span>

- <span data-ttu-id="f5f7c-297">ASP.NET MVC ActionFilterAttribute クラスを使用してカスタムアクションフィルターを作成する方法</span><span class="sxs-lookup"><span data-stu-id="f5f7c-297">How to create Custom Action filters with the ASP.NET MVC ActionFilterAttribute class</span></span>
- <span data-ttu-id="f5f7c-298">ASP.NET MVC コントローラーにフィルターを挿入する方法</span><span class="sxs-lookup"><span data-stu-id="f5f7c-298">How to inject filters into ASP.NET MVC controllers</span></span>
- <span data-ttu-id="f5f7c-299">Order プロパティを使用してフィルターの順序を管理する方法</span><span class="sxs-lookup"><span data-stu-id="f5f7c-299">How to manage filter ordering using the Order property</span></span>
- <span data-ttu-id="f5f7c-300">フィルターをグローバルに登録する方法</span><span class="sxs-lookup"><span data-stu-id="f5f7c-300">How to register filters globally</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="f5f7c-301">付録 A: Visual Studio Express 2012 を Web 用にインストールする</span><span class="sxs-lookup"><span data-stu-id="f5f7c-301">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="f5f7c-302">**[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)** を使用して、Web または別の &quot;Express&quot; バージョン**用に Microsoft Visual Studio Express 2012**をインストールできます。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-302">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="f5f7c-303">次の手順では、 *Microsoft Web Platform Installer*を使用して*Visual studio Express 2012 for Web*をインストールするために必要な手順について説明します。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-303">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="f5f7c-304">[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169) に移動します。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-304">Go to [https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="f5f7c-305">または、Web Platform Installer が既にインストールされている場合は、それを開いて、製品 &quot;<em>Visual Studio Express 2012 For web With Windows AZURE SDK</em>&quot;を検索することもできます。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-305">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="f5f7c-306">**[今すぐインストール]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-306">Click on **Install Now**.</span></span> <span data-ttu-id="f5f7c-307">**Web Platform Installer**がない場合は、最初にダウンロードしてインストールするようにリダイレクトされます。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-307">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="f5f7c-308">**Web Platform Installer**が開いたら、 **[インストール]** をクリックしてセットアップを開始します。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-308">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="f5f7c-309">![Visual Studio Express のインストール](aspnet-mvc-4-custom-action-filters/_static/image12.png "Visual Studio Express のインストール")</span><span class="sxs-lookup"><span data-stu-id="f5f7c-309">![Install Visual Studio Express](aspnet-mvc-4-custom-action-filters/_static/image12.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="f5f7c-310">*Visual Studio Express のインストール*</span><span class="sxs-lookup"><span data-stu-id="f5f7c-310">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="f5f7c-311">すべての製品のライセンスと条項を読み、[**同意**する] をクリックして続行します。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-311">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![ライセンス条項に同意する](aspnet-mvc-4-custom-action-filters/_static/image13.png)

    <span data-ttu-id="f5f7c-313">*ライセンス条項に同意する*</span><span class="sxs-lookup"><span data-stu-id="f5f7c-313">*Accepting the license terms*</span></span>
5. <span data-ttu-id="f5f7c-314">ダウンロードとインストールのプロセスが完了するまで待ちます。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-314">Wait until the downloading and installation process completes.</span></span>

    ![Installation progress](aspnet-mvc-4-custom-action-filters/_static/image14.png)

    <span data-ttu-id="f5f7c-316">*インストールの進行状況*</span><span class="sxs-lookup"><span data-stu-id="f5f7c-316">*Installation progress*</span></span>
6. <span data-ttu-id="f5f7c-317">インストールが完了したら、 **[完了]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-317">When the installation completes, click **Finish**.</span></span>

    ![インストールの完了](aspnet-mvc-4-custom-action-filters/_static/image15.png)

    <span data-ttu-id="f5f7c-319">*インストールの完了*</span><span class="sxs-lookup"><span data-stu-id="f5f7c-319">*Installation completed*</span></span>
7. <span data-ttu-id="f5f7c-320">**[終了]** をクリックして Web Platform Installer を閉じます。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-320">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="f5f7c-321">Web 用の Visual Studio Express を開くには、**スタート**画面にアクセスして &quot;**VS Express**&quot;の書き込みを開始し、 **[VS Express for Web]** タイルをクリックします。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-321">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![VS Express for Web タイル](aspnet-mvc-4-custom-action-filters/_static/image16.png)

    <span data-ttu-id="f5f7c-323">*VS Express for Web タイル*</span><span class="sxs-lookup"><span data-stu-id="f5f7c-323">*VS Express for Web tile*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="f5f7c-324">付録 B: Web 配置を使用した ASP.NET MVC 4 アプリケーションの発行</span><span class="sxs-lookup"><span data-stu-id="f5f7c-324">Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

<span data-ttu-id="f5f7c-325">この付録では、windows azure 管理ポータルから新しい web サイトを作成し、Windows Azure によって提供される Web 配置公開機能を活用して、ラボに従って取得したアプリケーションを発行する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-325">This appendix will show you how to create a new web site from the Windows Azure Management Portal and publish the application you obtained by following the lab, taking advantage of the Web Deploy publishing feature provided by Windows Azure.</span></span>

<a id="ApxBTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a><span data-ttu-id="f5f7c-326">タスク 1-Windows Azure ポータルから新しい Web サイトを作成する</span><span class="sxs-lookup"><span data-stu-id="f5f7c-326">Task 1 - Creating a New Web Site from the Windows Azure Portal</span></span>

1. <span data-ttu-id="f5f7c-327">[Windows Azure 管理ポータル](https://manage.windowsazure.com/)にアクセスし、サブスクリプションに関連付けられている Microsoft 資格情報を使用してサインインします。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-327">Go to the [Windows Azure Management Portal](https://manage.windowsazure.com/) and sign in using the Microsoft credentials associated with your subscription.</span></span>

    > [!NOTE]
    > <span data-ttu-id="f5f7c-328">Windows Azure では、10 ASP.NET の Web サイトを無料でホストし、トラフィックの増加に合わせて拡張できます。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-328">With Windows Azure you can host 10 ASP.NET Web Sites for free and then scale as your traffic grows.</span></span> <span data-ttu-id="f5f7c-329">[ここで](https://aka.ms/aspnet-hol-azure)サインアップできます。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-329">You can sign up [here](https://aka.ms/aspnet-hol-azure).</span></span>

    <span data-ttu-id="f5f7c-330">![Windows Azure portal にログオンします。](aspnet-mvc-4-custom-action-filters/_static/image17.png "Windows Azure portal にログオンします。")</span><span class="sxs-lookup"><span data-stu-id="f5f7c-330">![Log on to Windows Azure portal](aspnet-mvc-4-custom-action-filters/_static/image17.png "Log on to Windows Azure portal")</span></span>

    <span data-ttu-id="f5f7c-331">*Windows Azure 管理ポータルにログオンします。*</span><span class="sxs-lookup"><span data-stu-id="f5f7c-331">*Log on to Windows Azure Management Portal*</span></span>
2. <span data-ttu-id="f5f7c-332">コマンドバーの **[新規]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-332">Click **New** on the command bar.</span></span>

    <span data-ttu-id="f5f7c-333">![新しい Web サイトの作成](aspnet-mvc-4-custom-action-filters/_static/image18.png "新しい Web サイトの作成")</span><span class="sxs-lookup"><span data-stu-id="f5f7c-333">![Creating a new Web Site](aspnet-mvc-4-custom-action-filters/_static/image18.png "Creating a new Web Site")</span></span>

    <span data-ttu-id="f5f7c-334">*新しい Web サイトの作成*</span><span class="sxs-lookup"><span data-stu-id="f5f7c-334">*Creating a new Web Site*</span></span>
3. <span data-ttu-id="f5f7c-335">[ **Compute** | **Web サイト**] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-335">Click **Compute** | **Web Site**.</span></span> <span data-ttu-id="f5f7c-336">次に、 **[簡易作成]** オプションを選択します。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-336">Then select **Quick Create** option.</span></span> <span data-ttu-id="f5f7c-337">新しい web サイトの使用可能な URL を指定し、 **[Web サイトの作成]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-337">Provide an available URL for the new web site and click **Create Web Site**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="f5f7c-338">Windows Azure の Web サイトは、制御および管理が可能なクラウドで実行されている web アプリケーションのホストです。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-338">A Windows Azure Web Site is the host for a web application running in the cloud that you can control and manage.</span></span> <span data-ttu-id="f5f7c-339">[簡易作成] オプションを使用すると、完成した web アプリケーションをポータルの外部から Windows Azure の Web サイトにデプロイできます。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-339">The Quick Create option allows you to deploy a completed web application to the Windows Azure Web Site from outside the portal.</span></span> <span data-ttu-id="f5f7c-340">データベースを設定する手順は含まれていません。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-340">It does not include steps for setting up a database.</span></span>

    <span data-ttu-id="f5f7c-341">![簡易作成を使用した新しい Web サイトの作成](aspnet-mvc-4-custom-action-filters/_static/image19.png "簡易作成を使用した新しい Web サイトの作成")</span><span class="sxs-lookup"><span data-stu-id="f5f7c-341">![Creating a new Web Site using Quick Create](aspnet-mvc-4-custom-action-filters/_static/image19.png "Creating a new Web Site using Quick Create")</span></span>

    <span data-ttu-id="f5f7c-342">*簡易作成を使用した新しい Web サイトの作成*</span><span class="sxs-lookup"><span data-stu-id="f5f7c-342">*Creating a new Web Site using Quick Create*</span></span>
4. <span data-ttu-id="f5f7c-343">新しい**Web サイト**が作成されるまで待ちます。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-343">Wait until the new **Web Site** is created.</span></span>
5. <span data-ttu-id="f5f7c-344">Web サイトが作成されたら、 **[URL]** 列の下のリンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-344">Once the Web Site is created click the link under the **URL** column.</span></span> <span data-ttu-id="f5f7c-345">新しい Web サイトが機能していることを確認します。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-345">Check that the new Web Site is working.</span></span>

    <span data-ttu-id="f5f7c-346">![新しい web サイトを参照しています](aspnet-mvc-4-custom-action-filters/_static/image20.png "新しい web サイトを参照しています")</span><span class="sxs-lookup"><span data-stu-id="f5f7c-346">![Browsing to the new web site](aspnet-mvc-4-custom-action-filters/_static/image20.png "Browsing to the new web site")</span></span>

    <span data-ttu-id="f5f7c-347">*新しい web サイトを参照しています*</span><span class="sxs-lookup"><span data-stu-id="f5f7c-347">*Browsing to the new web site*</span></span>

    <span data-ttu-id="f5f7c-348">![実行中の Web サイト](aspnet-mvc-4-custom-action-filters/_static/image21.png "実行中の Web サイト")</span><span class="sxs-lookup"><span data-stu-id="f5f7c-348">![Web site running](aspnet-mvc-4-custom-action-filters/_static/image21.png "Web site running")</span></span>

    <span data-ttu-id="f5f7c-349">*実行中の Web サイト*</span><span class="sxs-lookup"><span data-stu-id="f5f7c-349">*Web site running*</span></span>
6. <span data-ttu-id="f5f7c-350">ポータルに戻り、 **[名前]** 列の下にある web サイトの名前をクリックして、管理ページを表示します。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-350">Go back to the portal and click the name of the web site under the **Name** column to display the management pages.</span></span>

    <span data-ttu-id="f5f7c-351">![Web サイトの管理ページを開く](aspnet-mvc-4-custom-action-filters/_static/image22.png "Web サイトの管理ページを開く")</span><span class="sxs-lookup"><span data-stu-id="f5f7c-351">![Opening the web site management pages](aspnet-mvc-4-custom-action-filters/_static/image22.png "Opening the web site management pages")</span></span>

    <span data-ttu-id="f5f7c-352">*Web サイトの管理ページを開く*</span><span class="sxs-lookup"><span data-stu-id="f5f7c-352">*Opening the Web Site management pages*</span></span>
7. <span data-ttu-id="f5f7c-353">**[ダッシュボード]** ページの **[概要] セクションで**、 **[発行プロファイルのダウンロード]** リンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-353">In the **Dashboard** page, under the **quick glance** section, click the **Download publish profile** link.</span></span>

    > [!NOTE]
    > <span data-ttu-id="f5f7c-354">*発行プロファイル*には、有効になっている各発行方法について、Windows Azure web サイトに web アプリケーションを発行するために必要なすべての情報が含まれています。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-354">The *publish profile* contains all of the information required to publish a web application to a Windows Azure website for each enabled publication method.</span></span> <span data-ttu-id="f5f7c-355">発行プロファイルには、発行メソッドが有効化される各エンドポイントに接続して認証するために必要な URL、ユーザーの資格情報、およびデータベース文字列が含まれています。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-355">The publish profile contains the URLs, user credentials and database strings required to connect to and authenticate against each of the endpoints for which a publication method is enabled.</span></span> <span data-ttu-id="f5f7c-356">**Microsoft WebMatrix 2**、 **Microsoft Visual Studio Express for Web**および**Microsoft Visual Studio 2012**では、発行プロファイルを読み取り、Web アプリケーションを Windows Azure websites に発行するためのこれらのプログラムの構成を自動化することがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-356">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** and **Microsoft Visual Studio 2012** support reading publish profiles to automate configuration of these programs for publishing web applications to Windows Azure websites.</span></span>

    <span data-ttu-id="f5f7c-357">![Web サイト発行プロファイルをダウンロードしています](aspnet-mvc-4-custom-action-filters/_static/image23.png "Web サイト発行プロファイルをダウンロードしています")</span><span class="sxs-lookup"><span data-stu-id="f5f7c-357">![Downloading the web site publish profile](aspnet-mvc-4-custom-action-filters/_static/image23.png "Downloading the web site publish profile")</span></span>

    <span data-ttu-id="f5f7c-358">*Web サイト発行プロファイルをダウンロードしています*</span><span class="sxs-lookup"><span data-stu-id="f5f7c-358">*Downloading the Web Site publish profile*</span></span>
8. <span data-ttu-id="f5f7c-359">発行プロファイルファイルを既知の場所にダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-359">Download the publish profile file to a known location.</span></span> <span data-ttu-id="f5f7c-360">この演習では、このファイルを使用して、Visual Studio から Windows Azure Web サイトに web アプリケーションを発行する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-360">Further in this exercise you will see how to use this file to publish a web application to a Windows Azure Web Sites from Visual Studio.</span></span>

    <span data-ttu-id="f5f7c-361">![発行プロファイルファイルを保存しています](aspnet-mvc-4-custom-action-filters/_static/image24.png "発行プロファイルを保存しています")</span><span class="sxs-lookup"><span data-stu-id="f5f7c-361">![Saving the publish profile file](aspnet-mvc-4-custom-action-filters/_static/image24.png "Saving the publish profile")</span></span>

    <span data-ttu-id="f5f7c-362">*発行プロファイルファイルを保存しています*</span><span class="sxs-lookup"><span data-stu-id="f5f7c-362">*Saving the publish profile file*</span></span>

<a id="ApxBTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a><span data-ttu-id="f5f7c-363">タスク 2-データベースサーバーの構成</span><span class="sxs-lookup"><span data-stu-id="f5f7c-363">Task 2 - Configuring the Database Server</span></span>

<span data-ttu-id="f5f7c-364">アプリケーションで SQL Server データベースを使用する場合は、SQL Database サーバーを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-364">If your application makes use of SQL Server databases you will need to create a SQL Database server.</span></span> <span data-ttu-id="f5f7c-365">SQL Server を使用しない単純なアプリケーションを展開する場合は、このタスクを省略できます。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-365">If you want to deploy a simple application that does not use SQL Server you might skip this task.</span></span>

1. <span data-ttu-id="f5f7c-366">アプリケーションデータベースを格納するには、SQL Database サーバーが必要です。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-366">You will need a SQL Database server for storing the application database.</span></span> <span data-ttu-id="f5f7c-367">サブスクリプションの**SQL Database サーバーは**、Windows Azure 管理ポータルの**SQL データベース** | サーバー | **サーバーのダッシュボード**で確認できます。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-367">You can view the SQL Database servers from your subscription in the Windows Azure Management portal at **Sql Databases** | **Servers** | **Server's Dashboard**.</span></span> <span data-ttu-id="f5f7c-368">サーバーを作成していない場合は、コマンドバーの **[追加]** ボタンを使用して作成できます。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-368">If you do not have a server created, you can create one using the **Add** button on the command bar.</span></span> <span data-ttu-id="f5f7c-369">次のタスクで使用するので、**サーバー名と URL、管理者のログイン名、パスワード**をメモしておきます。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-369">Take note of the **server name and URL, administrator login name and password**, as you will use them in the next tasks.</span></span> <span data-ttu-id="f5f7c-370">データベースは、後の段階で作成されるため、まだ作成しないでください。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-370">Do not create the database yet, as it will be created in a later stage.</span></span>

    <span data-ttu-id="f5f7c-371">![SQL Database サーバーダッシュボード](aspnet-mvc-4-custom-action-filters/_static/image25.png "SQL Database サーバーダッシュボード")</span><span class="sxs-lookup"><span data-stu-id="f5f7c-371">![SQL Database Server Dashboard](aspnet-mvc-4-custom-action-filters/_static/image25.png "SQL Database Server Dashboard")</span></span>

    <span data-ttu-id="f5f7c-372">*SQL Database サーバーダッシュボード*</span><span class="sxs-lookup"><span data-stu-id="f5f7c-372">*SQL Database Server Dashboard*</span></span>
2. <span data-ttu-id="f5f7c-373">次のタスクでは、Visual Studio からデータベース接続をテストします。そのため、**使用可能な Ip アドレス**の一覧にローカル ip アドレスを含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-373">In the next task you will test the database connection from Visual Studio, for that reason you need to include your local IP address in the server's list of **Allowed IP Addresses**.</span></span> <span data-ttu-id="f5f7c-374">これを行うには、 **[構成]** をクリックし、 **[現在のクライアント IP アドレス]** の ip アドレスを選択して、 **[開始 Ip アドレス]** と **[終了 ip アドレス]** のテキストボックスに貼り付け、[![の](aspnet-mvc-4-custom-action-filters/_static/image26.png) 追加] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-374">To do that, click **Configure**, select the IP address from **Current Client IP Address** and paste it on the **Start IP Address** and **End IP Address** text boxes and click the ![add-client-ip-address-ok-button](aspnet-mvc-4-custom-action-filters/_static/image26.png) button.</span></span>

    ![クライアント IP アドレスを追加しています](aspnet-mvc-4-custom-action-filters/_static/image27.png)

    <span data-ttu-id="f5f7c-376">*クライアント IP アドレスを追加しています*</span><span class="sxs-lookup"><span data-stu-id="f5f7c-376">*Adding Client IP Address*</span></span>
3. <span data-ttu-id="f5f7c-377">[許可された IP アドレス] の一覧に**クライアントの Ip アドレス**が追加されたら、 **[保存]** をクリックして変更を確認します。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-377">Once the **Client IP Address** is added to the allowed IP addresses list, click on **Save** to confirm the changes.</span></span>

    ![変更の確認](aspnet-mvc-4-custom-action-filters/_static/image28.png)

    <span data-ttu-id="f5f7c-379">*変更の確認*</span><span class="sxs-lookup"><span data-stu-id="f5f7c-379">*Confirm Changes*</span></span>

<a id="ApxBTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="f5f7c-380">タスク 3-Web 配置を使用した ASP.NET MVC 4 アプリケーションの発行</span><span class="sxs-lookup"><span data-stu-id="f5f7c-380">Task 3 - Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

1. <span data-ttu-id="f5f7c-381">ASP.NET MVC 4 ソリューションに戻ります。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-381">Go back to the ASP.NET MVC 4 solution.</span></span> <span data-ttu-id="f5f7c-382">**ソリューションエクスプローラー**で、web サイトプロジェクトを右クリックし、 **[発行]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-382">In the **Solution Explorer**, right-click the web site project and select **Publish**.</span></span>

    <span data-ttu-id="f5f7c-383">![アプリケーションの発行](aspnet-mvc-4-custom-action-filters/_static/image29.png "アプリケーションの発行")</span><span class="sxs-lookup"><span data-stu-id="f5f7c-383">![Publishing the Application](aspnet-mvc-4-custom-action-filters/_static/image29.png "Publishing the Application")</span></span>

    <span data-ttu-id="f5f7c-384">*Web サイトの公開*</span><span class="sxs-lookup"><span data-stu-id="f5f7c-384">*Publishing the web site*</span></span>
2. <span data-ttu-id="f5f7c-385">最初のタスクで保存した発行プロファイルをインポートします。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-385">Import the publish profile you saved in the first task.</span></span>

    <span data-ttu-id="f5f7c-386">![発行プロファイルをインポートしています](aspnet-mvc-4-custom-action-filters/_static/image30.png "発行プロファイルをインポートしています")</span><span class="sxs-lookup"><span data-stu-id="f5f7c-386">![Importing the publish profile](aspnet-mvc-4-custom-action-filters/_static/image30.png "Importing the publish profile")</span></span>

    <span data-ttu-id="f5f7c-387">*発行プロファイルをインポートしています*</span><span class="sxs-lookup"><span data-stu-id="f5f7c-387">*Importing publish profile*</span></span>
3. <span data-ttu-id="f5f7c-388">**[接続の検証]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-388">Click **Validate Connection**.</span></span> <span data-ttu-id="f5f7c-389">検証が完了したら、 **[次へ]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-389">Once Validation is complete click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="f5f7c-390">検証が完了すると、[接続の検証] ボタンの横に緑色のチェックマークが表示されます。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-390">Validation is complete once you see a green checkmark appear next to the Validate Connection button.</span></span>

    <span data-ttu-id="f5f7c-391">![接続の検証](aspnet-mvc-4-custom-action-filters/_static/image31.png "接続の検証")</span><span class="sxs-lookup"><span data-stu-id="f5f7c-391">![Validating connection](aspnet-mvc-4-custom-action-filters/_static/image31.png "Validating connection")</span></span>

    <span data-ttu-id="f5f7c-392">*接続の検証*</span><span class="sxs-lookup"><span data-stu-id="f5f7c-392">*Validating connection*</span></span>
4. <span data-ttu-id="f5f7c-393">**[設定]** ページの **[データベース]** セクションで、データベース接続のテキストボックスの横にあるボタン ( **defaultconnection**など) をクリックします。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-393">In the **Settings** page, under the **Databases** section, click the button next to your database connection's textbox (i.e. **DefaultConnection**).</span></span>

    <span data-ttu-id="f5f7c-394">![Web deploy の構成](aspnet-mvc-4-custom-action-filters/_static/image32.png "Web deploy の構成")</span><span class="sxs-lookup"><span data-stu-id="f5f7c-394">![Web deploy configuration](aspnet-mvc-4-custom-action-filters/_static/image32.png "Web deploy configuration")</span></span>

    <span data-ttu-id="f5f7c-395">*Web deploy の構成*</span><span class="sxs-lookup"><span data-stu-id="f5f7c-395">*Web deploy configuration*</span></span>
5. <span data-ttu-id="f5f7c-396">次のようにデータベース接続を構成します。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-396">Configure the database connection as follows:</span></span>

   - <span data-ttu-id="f5f7c-397">**サーバー名**には、 *tcp:* プレフィックスを使用して SQL Database サーバーの URL を入力します。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-397">In the **Server name** type your SQL Database server URL using the *tcp:* prefix.</span></span>
   - <span data-ttu-id="f5f7c-398">**User name (ユーザー名**) に、サーバー管理者のログイン名を入力します。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-398">In **User name** type your server administrator login name.</span></span>
   - <span data-ttu-id="f5f7c-399">**パスワード**で、サーバー管理者のログインパスワードを入力します。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-399">In **Password** type your server administrator login password.</span></span>
   - <span data-ttu-id="f5f7c-400">新しいデータベース名を入力します。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-400">Type a new database name.</span></span>

     <span data-ttu-id="f5f7c-401">![変換先の接続文字列を構成しています](aspnet-mvc-4-custom-action-filters/_static/image33.png "変換先の接続文字列を構成しています")</span><span class="sxs-lookup"><span data-stu-id="f5f7c-401">![Configuring destination connection string](aspnet-mvc-4-custom-action-filters/_static/image33.png "Configuring destination connection string")</span></span>

     <span data-ttu-id="f5f7c-402">*変換先の接続文字列を構成しています*</span><span class="sxs-lookup"><span data-stu-id="f5f7c-402">*Configuring destination connection string*</span></span>
6. <span data-ttu-id="f5f7c-403">次に、 **[OK]** をクリックします</span><span class="sxs-lookup"><span data-stu-id="f5f7c-403">Then click **OK**.</span></span> <span data-ttu-id="f5f7c-404">データベースの作成を求めるメッセージが表示されたら、[**はい]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-404">When prompted to create the database click **Yes**.</span></span>

    <span data-ttu-id="f5f7c-405">![データベースの作成](aspnet-mvc-4-custom-action-filters/_static/image34.png "データベース文字列の作成")</span><span class="sxs-lookup"><span data-stu-id="f5f7c-405">![Creating the database](aspnet-mvc-4-custom-action-filters/_static/image34.png "Creating the database string")</span></span>

    <span data-ttu-id="f5f7c-406">*データベースの作成*</span><span class="sxs-lookup"><span data-stu-id="f5f7c-406">*Creating the database*</span></span>
7. <span data-ttu-id="f5f7c-407">Windows Azure の SQL Database に接続するために使用する接続文字列は、[既定の接続] ボックスに表示されます。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-407">The connection string you will use to connect to SQL Database in Windows Azure is shown within Default Connection textbox.</span></span> <span data-ttu-id="f5f7c-408">続けて、 **[次へ]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-408">Then click **Next**.</span></span>

    <span data-ttu-id="f5f7c-409">![SQL Database を指す接続文字列](aspnet-mvc-4-custom-action-filters/_static/image35.png "SQL Database を指す接続文字列")</span><span class="sxs-lookup"><span data-stu-id="f5f7c-409">![Connection string pointing to SQL Database](aspnet-mvc-4-custom-action-filters/_static/image35.png "Connection string pointing to SQL Database")</span></span>

    <span data-ttu-id="f5f7c-410">*SQL Database を指す接続文字列*</span><span class="sxs-lookup"><span data-stu-id="f5f7c-410">*Connection string pointing to SQL Database*</span></span>
8. <span data-ttu-id="f5f7c-411">**[プレビュー]** ページで、 **[発行]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-411">In the **Preview** page, click **Publish**.</span></span>

    <span data-ttu-id="f5f7c-412">![Web アプリケーションの発行](aspnet-mvc-4-custom-action-filters/_static/image36.png "Web アプリケーションの発行")</span><span class="sxs-lookup"><span data-stu-id="f5f7c-412">![Publishing the web application](aspnet-mvc-4-custom-action-filters/_static/image36.png "Publishing the web application")</span></span>

    <span data-ttu-id="f5f7c-413">*Web アプリケーションの発行*</span><span class="sxs-lookup"><span data-stu-id="f5f7c-413">*Publishing the web application*</span></span>
9. <span data-ttu-id="f5f7c-414">発行プロセスが完了すると、既定のブラウザーによって公開された web サイトが開きます。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-414">Once the publishing process finishes, your default browser will open the published web site.</span></span>

<a id="AppendixC"></a>

<a id="Appendix_C_Using_Code_Snippets"></a>
## <a name="appendix-c-using-code-snippets"></a><span data-ttu-id="f5f7c-415">付録 C: コードスニペットの使用</span><span class="sxs-lookup"><span data-stu-id="f5f7c-415">Appendix C: Using Code Snippets</span></span>

<span data-ttu-id="f5f7c-416">コードスニペットを使用すると、必要なすべてのコードをすぐに利用できます。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-416">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="f5f7c-417">次の図に示すように、ラボドキュメントには、使用できるタイミングがわかります。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-417">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="f5f7c-418">![Visual Studio のコードスニペットを使用してプロジェクトにコードを挿入する](aspnet-mvc-4-custom-action-filters/_static/image37.png "Visual Studio のコードスニペットを使用してプロジェクトにコードを挿入する")</span><span class="sxs-lookup"><span data-stu-id="f5f7c-418">![Using Visual Studio code snippets to insert code into your project](aspnet-mvc-4-custom-action-filters/_static/image37.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="f5f7c-419">*Visual Studio のコードスニペットを使用してプロジェクトにコードを挿入する*</span><span class="sxs-lookup"><span data-stu-id="f5f7c-419">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="f5f7c-420">***キーボードを使用してコードスニペットを追加C#するには (のみ)***</span><span class="sxs-lookup"><span data-stu-id="f5f7c-420">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="f5f7c-421">コードを挿入する場所にカーソルを置きます。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-421">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="f5f7c-422">(スペースまたはハイフンを含まない) スニペット名の入力を開始します。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-422">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="f5f7c-423">IntelliSense によって、一致するスニペットの名前が表示されます。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-423">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="f5f7c-424">正しいスニペットを選択します (または、スニペットの名前全体が選択されるまで入力し続けます)。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-424">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="f5f7c-425">Tab キーを2回押すと、スニペットがカーソル位置に挿入されます。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-425">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="f5f7c-426">![スニペット名の入力を開始します](aspnet-mvc-4-custom-action-filters/_static/image38.png "スニペット名の入力を開始します")</span><span class="sxs-lookup"><span data-stu-id="f5f7c-426">![Start typing the snippet name](aspnet-mvc-4-custom-action-filters/_static/image38.png "Start typing the snippet name")</span></span>

<span data-ttu-id="f5f7c-427">*スニペット名の入力を開始します*</span><span class="sxs-lookup"><span data-stu-id="f5f7c-427">*Start typing the snippet name*</span></span>

<span data-ttu-id="f5f7c-428">![Tab キーを押して、強調表示されているスニペットを選択します](aspnet-mvc-4-custom-action-filters/_static/image39.png "Tab キーを押して、強調表示されているスニペットを選択します")</span><span class="sxs-lookup"><span data-stu-id="f5f7c-428">![Press Tab to select the highlighted snippet](aspnet-mvc-4-custom-action-filters/_static/image39.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="f5f7c-429">*Tab キーを押して、強調表示されているスニペットを選択します*</span><span class="sxs-lookup"><span data-stu-id="f5f7c-429">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="f5f7c-430">![もう一度 Tab キーを押すと、スニペットが展開されます。](aspnet-mvc-4-custom-action-filters/_static/image40.png "もう一度 Tab キーを押すと、スニペットが展開されます。")</span><span class="sxs-lookup"><span data-stu-id="f5f7c-430">![Press Tab again and the snippet will expand](aspnet-mvc-4-custom-action-filters/_static/image40.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="f5f7c-431">*もう一度 Tab キーを押すと、スニペットが展開されます。*</span><span class="sxs-lookup"><span data-stu-id="f5f7c-431">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="f5f7c-432">***マウスC#(、Visual Basic および XML) を使用してコードスニペットを追加するに***は1.</span><span class="sxs-lookup"><span data-stu-id="f5f7c-432">***To add a code snippet using the mouse (C#, Visual Basic and XML)*** 1.</span></span> <span data-ttu-id="f5f7c-433">コードスニペットを挿入する場所を右クリックします。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-433">Right-click where you want to insert the code snippet.</span></span>

1. <span data-ttu-id="f5f7c-434">**[スニペットの挿入]** 、 **[マイコードスニペット**] の順に選択します。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-434">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
2. <span data-ttu-id="f5f7c-435">一覧から該当するスニペットをクリックして選択します。</span><span class="sxs-lookup"><span data-stu-id="f5f7c-435">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="f5f7c-436">![コードスニペットを挿入する場所を右クリックし、[スニペットの挿入] を選択します。](aspnet-mvc-4-custom-action-filters/_static/image41.png "コードスニペットを挿入する場所を右クリックし、[スニペットの挿入] を選択します。")</span><span class="sxs-lookup"><span data-stu-id="f5f7c-436">![Right-click where you want to insert the code snippet and select Insert Snippet](aspnet-mvc-4-custom-action-filters/_static/image41.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="f5f7c-437">*コードスニペットを挿入する場所を右クリックし、[スニペットの挿入] を選択します。*</span><span class="sxs-lookup"><span data-stu-id="f5f7c-437">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="f5f7c-438">![一覧から関連するスニペットをクリックして選択します。](aspnet-mvc-4-custom-action-filters/_static/image42.png "一覧から関連するスニペットをクリックして選択します。")</span><span class="sxs-lookup"><span data-stu-id="f5f7c-438">![Pick the relevant snippet from the list, by clicking on it](aspnet-mvc-4-custom-action-filters/_static/image42.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="f5f7c-439">*一覧から関連するスニペットをクリックして選択します。*</span><span class="sxs-lookup"><span data-stu-id="f5f7c-439">*Pick the relevant snippet from the list, by clicking on it*</span></span>
