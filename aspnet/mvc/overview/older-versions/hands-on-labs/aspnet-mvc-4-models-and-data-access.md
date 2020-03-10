---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-models-and-data-access
title: ASP.NET MVC 4 のモデルとデータアクセス |Microsoft Docs
author: rick-anderson
description: '注: このハンズオンラボでは、ASP.NET MVC に関する基本的な知識があることを前提としています。 ASP.NET MVC を以前に使用したことがない場合は、ASP.NET MVC 4...'
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 634ea84b-f904-4afe-b71b-49cccef4d9cc
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-models-and-data-access
msc.type: authoredcontent
ms.openlocfilehash: 90635b617930d0a9c126795f4c8790d542e33dc9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78451468"
---
# <a name="aspnet-mvc-4-models-and-data-access"></a><span data-ttu-id="c03a7-104">ASP.NET MVC 4 モデルとデータ アクセス</span><span class="sxs-lookup"><span data-stu-id="c03a7-104">ASP.NET MVC 4 Models and Data Access</span></span>

<span data-ttu-id="c03a7-105">[Web キャンプチーム](https://twitter.com/webcamps)別</span><span class="sxs-lookup"><span data-stu-id="c03a7-105">By [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="c03a7-106">Web キャンプトレーニングキットをダウンロードする</span><span class="sxs-lookup"><span data-stu-id="c03a7-106">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

<span data-ttu-id="c03a7-107">このハンズオンラボでは、 **ASP.NET MVC**に関する基本的な知識があることを前提としています。</span><span class="sxs-lookup"><span data-stu-id="c03a7-107">This Hands-on Lab assumes you have basic knowledge of **ASP.NET MVC**.</span></span> <span data-ttu-id="c03a7-108">以前に**ASP.NET mvc**を使用していない場合は、 **ASP.NET Mvc 4 の基礎**となるハンズオンラボに進むことをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="c03a7-108">If you have not used **ASP.NET MVC** before, we recommend you to go over **ASP.NET MVC 4 Fundamentals** Hands-on Lab.</span></span>

<span data-ttu-id="c03a7-109">このラボでは、ソースフォルダーに用意されているサンプル Web アプリケーションに軽微な変更を適用することによって前述した機能強化と新機能について説明します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-109">This lab walks you through the enhancements and new features previously described by applying minor changes to a sample Web application provided in the Source folder.</span></span>

> [!NOTE]
> <span data-ttu-id="c03a7-110">すべてのサンプルコードとスニペットは、 [Microsoft web/WebCampTrainingKit リリース](https://aka.ms/webcamps-training-kit)で入手できる Web キャンプトレーニングキットに含まれています。</span><span class="sxs-lookup"><span data-stu-id="c03a7-110">All sample code and snippets are included in the Web Camps Training Kit, available at [Microsoft-Web/WebCampTrainingKit Releases](https://aka.ms/webcamps-training-kit).</span></span> <span data-ttu-id="c03a7-111">このラボに固有のプロジェクトについては、「 [ASP.NET MVC 4 のモデルとデータアクセス](https://github.com/Microsoft-Web/HOL-MVC4ModelsAndDataAccess)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c03a7-111">The project specific to this lab is available at [ASP.NET MVC 4 Models and Data Access](https://github.com/Microsoft-Web/HOL-MVC4ModelsAndDataAccess).</span></span>

<span data-ttu-id="c03a7-112">**ASP.NET MVC の基礎**ハンズオンラボでは、コントローラーからビューテンプレートにハードコーディングされたデータを渡しています。</span><span class="sxs-lookup"><span data-stu-id="c03a7-112">In **ASP.NET MVC Fundamentals** Hands-on Lab, you have been passing hard-coded data from the Controllers to the View templates.</span></span> <span data-ttu-id="c03a7-113">しかし、実際の Web アプリケーションを構築するためには、実際のデータベースを使用することが必要になる場合があります。</span><span class="sxs-lookup"><span data-stu-id="c03a7-113">But, in order to build a real Web application, you might want to use a real database.</span></span>

<span data-ttu-id="c03a7-114">このハンズオンラボでは、データベースエンジンを使用して、Music ストアアプリケーションに必要なデータを格納および取得する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-114">This Hands-on Lab will show you how to use a database engine in order to store and retrieve the data needed for the Music Store application.</span></span> <span data-ttu-id="c03a7-115">これを実現するには、既存のデータベースから開始し、そこから Entity Data Model を作成します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-115">To accomplish that, you will start with an existing database and create the Entity Data Model from it.</span></span> <span data-ttu-id="c03a7-116">このラボ全体では、 **Database First**アプローチと、 **Code First**アプローチを満たすことができます。</span><span class="sxs-lookup"><span data-stu-id="c03a7-116">Throughout this lab, you will meet the **Database First** approach as well as the **Code First** approach.</span></span>

<span data-ttu-id="c03a7-117">ただし、 **Model First**方法を使用して、ツールを使用して同じモデルを作成し、そのモデルからデータベースを生成することもできます。</span><span class="sxs-lookup"><span data-stu-id="c03a7-117">However, you can also use the **Model First** approach, create the same model using the tools, and then generate the database from it.</span></span>

<span data-ttu-id="c03a7-118">![Database First と Model First](aspnet-mvc-4-models-and-data-access/_static/image1.png "Database First と Model First")</span><span class="sxs-lookup"><span data-stu-id="c03a7-118">![Database First vs. Model First](aspnet-mvc-4-models-and-data-access/_static/image1.png "Database First vs. Model First")</span></span>

<span data-ttu-id="c03a7-119">*Database First と Model First*</span><span class="sxs-lookup"><span data-stu-id="c03a7-119">*Database First vs. Model First*</span></span>

<span data-ttu-id="c03a7-120">モデルを生成した後は、ハードコーディングされたデータを使用するのではなく、データベースから取得したデータをストアビューに提供するために、StoreController に適切な調整を行います。</span><span class="sxs-lookup"><span data-stu-id="c03a7-120">After generating the Model, you will make the proper adjustments in the StoreController to provide the Store Views with the data taken from the database, instead of using hard-coded data.</span></span> <span data-ttu-id="c03a7-121">ビューテンプレートを変更する必要はありません。これは、StoreController がビューテンプレートに対して同じ Viewmodel を返すためです。ただし、この時点では、データはデータベースから取得されます。</span><span class="sxs-lookup"><span data-stu-id="c03a7-121">You will not need to make any change to the View templates because the StoreController will be returning the same ViewModels to the View templates, although this time the data will come from the database.</span></span>

<span data-ttu-id="c03a7-122">**Code First アプローチ**</span><span class="sxs-lookup"><span data-stu-id="c03a7-122">**The Code First Approach**</span></span>

<span data-ttu-id="c03a7-123">Code First アプローチを使用すると、一般的にフレームワークと結合されたクラスを生成することなく、コードからモデルを定義できます。</span><span class="sxs-lookup"><span data-stu-id="c03a7-123">The Code First approach allows us to define the model from the code without generating classes that are generally coupled with the framework.</span></span>

<span data-ttu-id="c03a7-124">Code first では、モデルオブジェクトは POCOs を使用して定義されています。 &quot;Plain Old CLR Objects&quot;です。</span><span class="sxs-lookup"><span data-stu-id="c03a7-124">In code first, model objects are defined with POCOs, &quot;Plain Old CLR Objects&quot;.</span></span> <span data-ttu-id="c03a7-125">POCOs は、継承されず、インターフェイスを実装しない単純なプレーンクラスです。</span><span class="sxs-lookup"><span data-stu-id="c03a7-125">POCOs are simple plain classes that have no inheritance and do not implement interfaces.</span></span> <span data-ttu-id="c03a7-126">データベースを自動的に生成することも、既存のデータベースを使用してコードからクラスのマッピングを生成することもできます。</span><span class="sxs-lookup"><span data-stu-id="c03a7-126">We can automatically generate the database from them, or we can use an existing database and generate the class mapping from the code.</span></span>

<span data-ttu-id="c03a7-127">この方法を使用する利点は、POCOs クラスがマッピングフレームワークと結合されていないため、モデルが永続化フレームワーク (この場合は Entity Framework) とは独立していることです。</span><span class="sxs-lookup"><span data-stu-id="c03a7-127">The benefits of using this approach is that the Model remains independent from the persistence framework (in this case, Entity Framework), as the POCOs classes are not coupled with the mapping framework.</span></span>

> [!NOTE]
> <span data-ttu-id="c03a7-128">このラボは、ASP.NET MVC 4 と、このハンズオンラボに示されている機能だけに合わせてカスタマイズおよび最小化されたバージョンのミュージックストアサンプルアプリケーションに基づいています。</span><span class="sxs-lookup"><span data-stu-id="c03a7-128">This Lab is based on ASP.NET MVC 4 and a version of the Music Store sample application customized and minimized to fit only the features shown in this Hands-On Lab.</span></span>
> 
> <span data-ttu-id="c03a7-129">**音楽ストア**のチュートリアルアプリケーション全体を調べる場合は、「 [MVC-music-ストア](https://github.com/evilDave/MVC-Music-Store)」で見つけることができます。</span><span class="sxs-lookup"><span data-stu-id="c03a7-129">If you wish to explore the whole **Music Store** tutorial application you can find it in [MVC-Music-Store](https://github.com/evilDave/MVC-Music-Store).</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="c03a7-130">前提条件</span><span class="sxs-lookup"><span data-stu-id="c03a7-130">Prerequisites</span></span>

<span data-ttu-id="c03a7-131">このラボを完了するには、次の項目が必要です。</span><span class="sxs-lookup"><span data-stu-id="c03a7-131">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="c03a7-132">Web またはそれ以降[の2012を Microsoft Visual Studio Express](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web)ます (付録 a をインストールする手順については[、「付録 a](#AppendixA) 」を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="c03a7-132">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="c03a7-133">セットアップ</span><span class="sxs-lookup"><span data-stu-id="c03a7-133">Setup</span></span>

<span data-ttu-id="c03a7-134">**コードスニペットのインストール**</span><span class="sxs-lookup"><span data-stu-id="c03a7-134">**Installing Code Snippets**</span></span>

<span data-ttu-id="c03a7-135">便宜上、このラボで管理するコードの多くは、Visual Studio のコードスニペットとして提供されています。</span><span class="sxs-lookup"><span data-stu-id="c03a7-135">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="c03a7-136">コードスニペットをインストールするには、 **.\Source\Setup\CodeSnippets.vsi**ファイルを実行します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-136">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="c03a7-137">Visual Studio Code のスニペットを使い慣れておらず、その使用方法を学習したい場合は、この &quot;ドキュメントの付録「[付録 C: コードスニペットの使用](#AppendixC)&quot;」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c03a7-137">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix C: Using Code Snippets](#AppendixC)&quot;.</span></span>

---

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="c03a7-138">手順</span><span class="sxs-lookup"><span data-stu-id="c03a7-138">Exercises</span></span>

<span data-ttu-id="c03a7-139">このハンズオンラボは、次の演習によって構成されています。</span><span class="sxs-lookup"><span data-stu-id="c03a7-139">This Hands-on Lab is comprised by the following exercises:</span></span>

1. [<span data-ttu-id="c03a7-140">演習 1: データベースの追加</span><span class="sxs-lookup"><span data-stu-id="c03a7-140">Exercise 1: Adding a Database</span></span>](#Exercise1)
2. [<span data-ttu-id="c03a7-141">演習 2: Code First を使用したデータベースの作成</span><span class="sxs-lookup"><span data-stu-id="c03a7-141">Exercise 2: Creating a Database using Code First</span></span>](#Exercise2)
3. [<span data-ttu-id="c03a7-142">演習 3: パラメーターを使用してデータベースにクエリを実行する</span><span class="sxs-lookup"><span data-stu-id="c03a7-142">Exercise 3: Querying the Database with Parameters</span></span>](#Exercise3)

> [!NOTE]
> <span data-ttu-id="c03a7-143">各演習には、演習を完了した後に取得する必要があるソリューションを含む**終了**フォルダーが付属しています。</span><span class="sxs-lookup"><span data-stu-id="c03a7-143">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="c03a7-144">演習を通じて追加のヘルプが必要な場合は、このソリューションをガイドとして使用できます。</span><span class="sxs-lookup"><span data-stu-id="c03a7-144">You can use this solution as a guide if you need additional help working through the exercises.</span></span>

<span data-ttu-id="c03a7-145">このラボの推定所要時間: **35 分**。</span><span class="sxs-lookup"><span data-stu-id="c03a7-145">Estimated time to complete this lab: **35 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Adding_a_Database"></a>
### <a name="exercise-1-adding-a-database"></a><span data-ttu-id="c03a7-146">演習 1: データベースの追加</span><span class="sxs-lookup"><span data-stu-id="c03a7-146">Exercise 1: Adding a Database</span></span>

<span data-ttu-id="c03a7-147">この演習では、データを使用するために、MusicStore アプリケーションのテーブルを含むデータベースをソリューションに追加する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-147">In this exercise, you will learn how to add a database with the tables of the MusicStore application to the solution in order to consume its data.</span></span> <span data-ttu-id="c03a7-148">モデルを使用してデータベースを生成し、ソリューションに追加したら、StoreController クラスを変更して、ハードコーディングされた値を使用するのではなく、データベースから取得したデータをビューテンプレートに提供します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-148">Once the database is generated with the model, and added to the solution, you will modify the StoreController class to provide the View template with the data taken from the database, instead of using hard-coded values.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Adding_a_Database"></a>
#### <a name="task-1---adding-a-database"></a><span data-ttu-id="c03a7-149">タスク 1-データベースの追加</span><span class="sxs-lookup"><span data-stu-id="c03a7-149">Task 1 - Adding a Database</span></span>

<span data-ttu-id="c03a7-150">このタスクでは、MusicStore アプリケーションのメインテーブルを持つ作成済みのデータベースをソリューションに追加します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-150">In this task, you will add an already created database with the main tables of the MusicStore application to the solution.</span></span>

1. <span data-ttu-id="c03a7-151">**Source/Ex1-AddingADatabaseDBFirst/begin/** folder にある**begin**ソリューションを開きます。</span><span class="sxs-lookup"><span data-stu-id="c03a7-151">Open the **Begin** solution located at **Source/Ex1-AddingADatabaseDBFirst/Begin/** folder.</span></span>

   1. <span data-ttu-id="c03a7-152">続行する前に、不足している NuGet パッケージをダウンロードする必要があります。</span><span class="sxs-lookup"><span data-stu-id="c03a7-152">You will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="c03a7-153">これを行うには、 **[プロジェクト]** メニューをクリックし、 **[NuGet パッケージの管理]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-153">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="c03a7-154">**[NuGet パッケージの管理]** ダイアログで、 **[復元]** をクリックして、不足しているパッケージをダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="c03a7-154">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="c03a7-155">最後に、[**ビルド** | **ビルド**] をクリックしてソリューションをビルドします。</span><span class="sxs-lookup"><span data-stu-id="c03a7-155">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="c03a7-156">NuGet を使用する利点の1つは、プロジェクトのすべてのライブラリを配布する必要がなく、プロジェクトのサイズを小さくすることです。</span><span class="sxs-lookup"><span data-stu-id="c03a7-156">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="c03a7-157">NuGet パワーツールを使用すると、パッケージのバージョンを app.config ファイルで指定することで、プロジェクトを初めて実行するときに必要なすべてのライブラリをダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="c03a7-157">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="c03a7-158">このため、このラボから既存のソリューションを開いた後に、これらの手順を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c03a7-158">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="c03a7-159">**MvcMusicStore**データベースファイルを追加します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-159">Add **MvcMusicStore** database file.</span></span> <span data-ttu-id="c03a7-160">このハンズオンラボでは、 **MvcMusicStore**という名前の作成済みのデータベースを使用します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-160">In this Hands-on Lab, you will use an already created database called **MvcMusicStore.mdf**.</span></span> <span data-ttu-id="c03a7-161">これを行うには、[**アプリ\_データ**フォルダー] を右クリックし、 **[追加]** をポイントして、 **[既存の項目]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c03a7-161">To do that, right-click **App\_Data** folder, point to **Add** and then click **Existing Item**.</span></span> <span data-ttu-id="c03a7-162">**MvcMusicStore**ファイルを参照**して選択します**。</span><span class="sxs-lookup"><span data-stu-id="c03a7-162">Browse to **\Source\Assets** and select the **MvcMusicStore.mdf** file.</span></span>

    <span data-ttu-id="c03a7-163">![既存の項目の追加](aspnet-mvc-4-models-and-data-access/_static/image2.png "既存の項目の追加")</span><span class="sxs-lookup"><span data-stu-id="c03a7-163">![Adding an Existing Item](aspnet-mvc-4-models-and-data-access/_static/image2.png "Adding an Existing Item")</span></span>

    <span data-ttu-id="c03a7-164">*既存の項目の追加*</span><span class="sxs-lookup"><span data-stu-id="c03a7-164">*Adding an Existing Item*</span></span>

    <span data-ttu-id="c03a7-165">![MvcMusicStore データベースファイル](aspnet-mvc-4-models-and-data-access/_static/image3.png "MvcMusicStore データベースファイル")</span><span class="sxs-lookup"><span data-stu-id="c03a7-165">![MvcMusicStore.mdf database file](aspnet-mvc-4-models-and-data-access/_static/image3.png "MvcMusicStore.mdf database file")</span></span>

    <span data-ttu-id="c03a7-166">*MvcMusicStore データベースファイル*</span><span class="sxs-lookup"><span data-stu-id="c03a7-166">*MvcMusicStore.mdf database file*</span></span>

    <span data-ttu-id="c03a7-167">データベースがプロジェクトに追加されました。</span><span class="sxs-lookup"><span data-stu-id="c03a7-167">The database has been added to the project.</span></span> <span data-ttu-id="c03a7-168">データベースがソリューション内に配置されている場合でも、別のデータベースサーバーでホストされているときにクエリを実行し、データベースを更新することができます。</span><span class="sxs-lookup"><span data-stu-id="c03a7-168">Even when the database is located inside the solution, you can query and update it as it was hosted in a different database server.</span></span>

    <span data-ttu-id="c03a7-169">![ソリューションエクスプローラーの MvcMusicStore データベース](aspnet-mvc-4-models-and-data-access/_static/image4.png "ソリューションエクスプローラーの MvcMusicStore データベース")</span><span class="sxs-lookup"><span data-stu-id="c03a7-169">![MvcMusicStore database in Solution Explorer](aspnet-mvc-4-models-and-data-access/_static/image4.png "MvcMusicStore database in Solution Explorer")</span></span>

    <span data-ttu-id="c03a7-170">*ソリューションエクスプローラーの MvcMusicStore データベース*</span><span class="sxs-lookup"><span data-stu-id="c03a7-170">*MvcMusicStore database in Solution Explorer*</span></span>
3. <span data-ttu-id="c03a7-171">データベースへの接続を確認します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-171">Verify the connection to the database.</span></span> <span data-ttu-id="c03a7-172">これを行うには、 **MvcMusicStore**をダブルクリックして接続を確立します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-172">To do this, double-click **MvcMusicStore.mdf** to establish a connection.</span></span>

    <span data-ttu-id="c03a7-173">![MvcMusicStore への接続](aspnet-mvc-4-models-and-data-access/_static/image5.png "MvcMusicStore への接続")</span><span class="sxs-lookup"><span data-stu-id="c03a7-173">![Connecting to MvcMusicStore.mdf](aspnet-mvc-4-models-and-data-access/_static/image5.png "Connecting to MvcMusicStore.mdf")</span></span>

    <span data-ttu-id="c03a7-174">*MvcMusicStore への接続*</span><span class="sxs-lookup"><span data-stu-id="c03a7-174">*Connecting to MvcMusicStore.mdf*</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Creating_a_Data_Model"></a>
#### <a name="task-2---creating-a-data-model"></a><span data-ttu-id="c03a7-175">タスク 2-データモデルの作成</span><span class="sxs-lookup"><span data-stu-id="c03a7-175">Task 2 - Creating a Data Model</span></span>

<span data-ttu-id="c03a7-176">このタスクでは、前のタスクで追加したデータベースと対話するデータモデルを作成します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-176">In this task, you will create a data model to interact with the database added in the previous task.</span></span>

1. <span data-ttu-id="c03a7-177">データベースを表すデータモデルを作成します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-177">Create a data model that will represent the database.</span></span> <span data-ttu-id="c03a7-178">これを行うにはソリューションエクスプローラー **[モデル]** フォルダーを右クリックし、 **[追加]** をポイントして、 **[新しい項目]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c03a7-178">To do this, in Solution Explorer right-click the **Models** folder, point to **Add** and then click **New Item**.</span></span> <span data-ttu-id="c03a7-179">**[新しい項目の追加]** ダイアログで、 **[データ]** テンプレートを選択し、 **[ADO.NET Entity Data Model]** 項目を選択します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-179">In the **Add New Item** dialog, select the **Data** template and then the **ADO.NET Entity Data Model** item.</span></span> <span data-ttu-id="c03a7-180">データモデル名を「 **Storedb. .edmx** 」に変更し、 **[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c03a7-180">Change the data model name to **StoreDB.edmx** and click **Add**.</span></span>

    <span data-ttu-id="c03a7-181">![StoreDB ADO.NET Entity Data Model の追加](aspnet-mvc-4-models-and-data-access/_static/image6.png "StoreDB ADO.NET Entity Data Model の追加")</span><span class="sxs-lookup"><span data-stu-id="c03a7-181">![Adding the StoreDB ADO.NET Entity Data Model](aspnet-mvc-4-models-and-data-access/_static/image6.png "Adding the StoreDB ADO.NET Entity Data Model")</span></span>

    <span data-ttu-id="c03a7-182">*StoreDB ADO.NET Entity Data Model の追加*</span><span class="sxs-lookup"><span data-stu-id="c03a7-182">*Adding the StoreDB ADO.NET Entity Data Model*</span></span>
2. <span data-ttu-id="c03a7-183">**Entity Data Model ウィザード**が表示されます。</span><span class="sxs-lookup"><span data-stu-id="c03a7-183">The **Entity Data Model Wizard** will appear.</span></span> <span data-ttu-id="c03a7-184">このウィザードの手順に従って、モデルレイヤーを作成できます。</span><span class="sxs-lookup"><span data-stu-id="c03a7-184">This wizard will guide you through the creation of the model layer.</span></span> <span data-ttu-id="c03a7-185">最近追加された既存のデータベースに基づいてモデルを作成する必要があるため、 **[データベースから生成]** を選択し、 **[次へ]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c03a7-185">Since the model should be created based on the existing database recently added, select **Generate from database** and click **Next**.</span></span>

    <span data-ttu-id="c03a7-186">![モデルコンテンツの選択](aspnet-mvc-4-models-and-data-access/_static/image7.png "モデルコンテンツの選択")</span><span class="sxs-lookup"><span data-stu-id="c03a7-186">![Choosing the model content](aspnet-mvc-4-models-and-data-access/_static/image7.png "Choosing the model content")</span></span>

    <span data-ttu-id="c03a7-187">*モデルコンテンツの選択*</span><span class="sxs-lookup"><span data-stu-id="c03a7-187">*Choosing the model content*</span></span>
3. <span data-ttu-id="c03a7-188">データベースからモデルを生成するため、使用する接続を指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c03a7-188">Since you are generating a model from a database, you will need to specify the connection to use.</span></span> <span data-ttu-id="c03a7-189">**[新しい接続]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c03a7-189">Click **New Connection**.</span></span>
4. <span data-ttu-id="c03a7-190">**Microsoft SQL Server データベースファイル**を選択し、 **[続行]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c03a7-190">Select **Microsoft SQL Server Database File** and click **Continue**.</span></span>

    <span data-ttu-id="c03a7-191">![データソースの選択](aspnet-mvc-4-models-and-data-access/_static/image8.png "データソースの選択")</span><span class="sxs-lookup"><span data-stu-id="c03a7-191">![Choose data source](aspnet-mvc-4-models-and-data-access/_static/image8.png "Choose data source")</span></span>

    <span data-ttu-id="c03a7-192">*[データソースの選択] ダイアログ*</span><span class="sxs-lookup"><span data-stu-id="c03a7-192">*Choose data source dialog*</span></span>
5. <span data-ttu-id="c03a7-193">**[参照]** をクリックし、 **App\_Data**フォルダーにあるデータベース**MvcMusicStore**を選択し、[ **OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c03a7-193">Click **Browse** and select the database **MvcMusicStore.mdf** you located in the **App\_Data** folder and click **OK**.</span></span>

    <span data-ttu-id="c03a7-194">![接続プロパティ](aspnet-mvc-4-models-and-data-access/_static/image9.png "接続のプロパティ")</span><span class="sxs-lookup"><span data-stu-id="c03a7-194">![Connection properties](aspnet-mvc-4-models-and-data-access/_static/image9.png "Connection properties")</span></span>

    <span data-ttu-id="c03a7-195">*接続プロパティ*</span><span class="sxs-lookup"><span data-stu-id="c03a7-195">*Connection properties*</span></span>
6. <span data-ttu-id="c03a7-196">生成されるクラスは、エンティティ接続文字列と同じ名前にする必要があります。そのため、名前を**MusicStoreEntities**に変更し、 **[次へ]** をクリックしてください。</span><span class="sxs-lookup"><span data-stu-id="c03a7-196">The generated class should have the same name as the entity connection string, so change its name to **MusicStoreEntities** and click **Next**.</span></span>

    <span data-ttu-id="c03a7-197">![データ接続の選択](aspnet-mvc-4-models-and-data-access/_static/image10.png "データ接続の選択")</span><span class="sxs-lookup"><span data-stu-id="c03a7-197">![Choosing the data connection](aspnet-mvc-4-models-and-data-access/_static/image10.png "Choosing the data connection")</span></span>

    <span data-ttu-id="c03a7-198">*データ接続の選択*</span><span class="sxs-lookup"><span data-stu-id="c03a7-198">*Choosing the data connection*</span></span>
7. <span data-ttu-id="c03a7-199">使用するデータベースオブジェクトを選択します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-199">Choose the database objects to use.</span></span> <span data-ttu-id="c03a7-200">エンティティモデルではデータベースのテーブルのみを使用するので、 **[テーブル]** オプションを選択し、[モデルおよび**複数化または単数のオブジェクト名**を**含む外部キー列を含める**] オプションも選択されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-200">As the Entity Model will use just the database's tables, select the **Tables** option, and make sure that the **Include foreign key columns in the model** and **Pluralize or singularize generated object names** options are also selected.</span></span> <span data-ttu-id="c03a7-201">モデルの名前空間を**MvcMusicStore**に変更し、 **[完了]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c03a7-201">Change the Model Namespace to **MvcMusicStore.Model** and click **Finish**.</span></span>

    <span data-ttu-id="c03a7-202">![データベースオブジェクトの選択](aspnet-mvc-4-models-and-data-access/_static/image11.png "データベースオブジェクトの選択")</span><span class="sxs-lookup"><span data-stu-id="c03a7-202">![Choosing the database objects](aspnet-mvc-4-models-and-data-access/_static/image11.png "Choosing the database objects")</span></span>

    <span data-ttu-id="c03a7-203">*データベースオブジェクトの選択*</span><span class="sxs-lookup"><span data-stu-id="c03a7-203">*Choosing the database objects*</span></span>

    > [!NOTE]
    > <span data-ttu-id="c03a7-204">セキュリティ警告ダイアログが表示された場合は、 **[OK]** をクリックしてテンプレートを実行し、モデルエンティティのクラスを生成します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-204">If a Security Warning dialog is shown, click **OK** to run the template and generate the classes for the model entities.</span></span>
8. <span data-ttu-id="c03a7-205">データベースのエンティティダイアグラムが表示され、各テーブルをデータベースにマップする個別のクラスが作成されます。</span><span class="sxs-lookup"><span data-stu-id="c03a7-205">An entity diagram for the database will appear, while a separate class that maps each table to the database will be created.</span></span> <span data-ttu-id="c03a7-206">たとえば **、アルバムのテーブルは** **アルバム**クラスによって表され、テーブル内の各列はクラスのプロパティにマップされます。</span><span class="sxs-lookup"><span data-stu-id="c03a7-206">For example, the **Albums** table will be represented by an **Album** class, where each column in the table will map to a class property.</span></span> <span data-ttu-id="c03a7-207">これにより、データベース内の行を表すオブジェクトを照会して操作できるようになります。</span><span class="sxs-lookup"><span data-stu-id="c03a7-207">This will allow you to query and work with objects that represent rows in the database.</span></span>

    <span data-ttu-id="c03a7-208">![エンティティダイアグラム](aspnet-mvc-4-models-and-data-access/_static/image12.png "エンティティ図")</span><span class="sxs-lookup"><span data-stu-id="c03a7-208">![Entity diagram](aspnet-mvc-4-models-and-data-access/_static/image12.png "Entity diagram")</span></span>

    <span data-ttu-id="c03a7-209">*エンティティダイアグラム*</span><span class="sxs-lookup"><span data-stu-id="c03a7-209">*Entity diagram*</span></span>

    > [!NOTE]
    > <span data-ttu-id="c03a7-210">T4 テンプレート (.tt) は、エンティティクラスを生成するコードを実行し、同じ名前の既存のクラスを上書きします。</span><span class="sxs-lookup"><span data-stu-id="c03a7-210">The T4 templates (.tt) run code to generate the entities classes and will overwrite the existing classes with the same name.</span></span> <span data-ttu-id="c03a7-211">この例では、クラス &quot;アルバム&quot;、&quot;Genre&quot;、および &quot;アーティスト&quot; が生成されたコードで上書きされています。</span><span class="sxs-lookup"><span data-stu-id="c03a7-211">In this example, the classes &quot;Album&quot;, &quot;Genre&quot; and &quot;Artist&quot; were overwritten with the generated code.</span></span>

<a id="Ex1Task3"></a>

<a id="Task_3_-_Building_the_Application"></a>
#### <a name="task-3---building-the-application"></a><span data-ttu-id="c03a7-212">タスク 3-アプリケーションのビルド</span><span class="sxs-lookup"><span data-stu-id="c03a7-212">Task 3 - Building the Application</span></span>

<span data-ttu-id="c03a7-213">このタスクでは、モデルの生成によって**アルバム**、**ジャンル**、および**アーティスト**モデルクラスが削除されましたが、新しいデータモデルクラスを使用してプロジェクトが正常にビルドされることを確認します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-213">In this task, you will check that, although the model generation have removed the **Album**, **Genre** and **Artist** model classes, the project builds successfully by using the new data model classes.</span></span>

1. <span data-ttu-id="c03a7-214">**[ビルド]** メニュー項目を選択し、 **[MvcMusicStore のビルド]** をクリックして、プロジェクトをビルドします。</span><span class="sxs-lookup"><span data-stu-id="c03a7-214">Build the project by selecting the **Build** menu item and then **Build MvcMusicStore**.</span></span>

    <span data-ttu-id="c03a7-215">![プロジェクトのビルド](aspnet-mvc-4-models-and-data-access/_static/image13.png "プロジェクトのビルド")</span><span class="sxs-lookup"><span data-stu-id="c03a7-215">![Building the project](aspnet-mvc-4-models-and-data-access/_static/image13.png "Building the project")</span></span>

    <span data-ttu-id="c03a7-216">*プロジェクトのビルド*</span><span class="sxs-lookup"><span data-stu-id="c03a7-216">*Building the project*</span></span>
2. <span data-ttu-id="c03a7-217">プロジェクトが正常にビルドされました。</span><span class="sxs-lookup"><span data-stu-id="c03a7-217">The project builds successfully.</span></span> <span data-ttu-id="c03a7-218">まだ機能しているのはなぜですか。</span><span class="sxs-lookup"><span data-stu-id="c03a7-218">Why does it still work?</span></span> <span data-ttu-id="c03a7-219">データベーステーブルには、削除されたクラスの**アルバム**および**ジャンル**で使用していたプロパティを含むフィールドがあるため、機能します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-219">It works because the database tables have fields that include the properties that you were using in the removed classes **Album** and **Genre**.</span></span>

    <span data-ttu-id="c03a7-220">![成功したビルド](aspnet-mvc-4-models-and-data-access/_static/image14.png "成功したビルド")</span><span class="sxs-lookup"><span data-stu-id="c03a7-220">![Builds succeeded](aspnet-mvc-4-models-and-data-access/_static/image14.png "Builds succeeded")</span></span>

    <span data-ttu-id="c03a7-221">*成功したビルド*</span><span class="sxs-lookup"><span data-stu-id="c03a7-221">*Builds succeeded*</span></span>
3. <span data-ttu-id="c03a7-222">エンティティは、デザイナーによってダイアグラム形式で表示されますC#が、実際にはクラスです。</span><span class="sxs-lookup"><span data-stu-id="c03a7-222">While the designer displays the entities in a diagram format, they are really C# classes.</span></span> <span data-ttu-id="c03a7-223">ソリューションエクスプローラーで **[Storedb. .edmx]** ノードを展開し、 **StoreDB.tt**をクリックすると、新しく生成されたエンティティが表示されます。</span><span class="sxs-lookup"><span data-stu-id="c03a7-223">Expand the **StoreDB.edmx** node in the Solution Explorer and then **StoreDB.tt**, you will see the new generated entities.</span></span>

    <span data-ttu-id="c03a7-224">![生成されたファイル](aspnet-mvc-4-models-and-data-access/_static/image15.png "生成されたファイル")</span><span class="sxs-lookup"><span data-stu-id="c03a7-224">![Generated files](aspnet-mvc-4-models-and-data-access/_static/image15.png "Generated files")</span></span>

    <span data-ttu-id="c03a7-225">*生成されたファイル*</span><span class="sxs-lookup"><span data-stu-id="c03a7-225">*Generated files*</span></span>

<a id="Ex1Task4"></a>

<a id="Task_4_-_Querying_the_Database"></a>
#### <a name="task-4---querying-the-database"></a><span data-ttu-id="c03a7-226">タスク 4-データベースに対してクエリを実行する</span><span class="sxs-lookup"><span data-stu-id="c03a7-226">Task 4 - Querying the Database</span></span>

<span data-ttu-id="c03a7-227">このタスクでは、StoreController クラスを更新します。これにより、ハードコードされたデータを使用するのではなく、データベースにクエリを実行して情報を取得します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-227">In this task, you will update the StoreController class so that, instead of using hardcoded data, it will query the database to retrieve the information.</span></span>

1. <span data-ttu-id="c03a7-228">**Controllers\StoreController.cs**を開き、次のフィールドをクラスに追加して、 **storedb**という名前の**MusicStoreEntities**クラスのインスタンスを保持します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-228">Open **Controllers\StoreController.cs** and add the following field to the class to hold an instance of the **MusicStoreEntities** class, named **storeDB**:</span></span>

    <span data-ttu-id="c03a7-229">(コードスニペット-*モデルとデータアクセス-Ex1 storeDB*)</span><span class="sxs-lookup"><span data-stu-id="c03a7-229">(Code Snippet - *Models And Data Access - Ex1 storeDB*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample1.cs)]
2. <span data-ttu-id="c03a7-230">**MusicStoreEntities**クラスは、データベース内の各テーブルのコレクションプロパティを公開します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-230">The **MusicStoreEntities** class exposes a collection property for each table in the database.</span></span> <span data-ttu-id="c03a7-231">すべての**アルバム**を含むジャンルを取得するように、**参照**アクションメソッドを更新します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-231">Update **Browse** action method to retrieve a Genre with all of the **Albums**.</span></span>

    <span data-ttu-id="c03a7-232">(コードスニペット-*モデルとデータアクセス-Ex1 Store 参照*)</span><span class="sxs-lookup"><span data-stu-id="c03a7-232">(Code Snippet - *Models And Data Access - Ex1 Store Browse*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample2.cs)]

    > [!NOTE]
    > <span data-ttu-id="c03a7-233">**LINQ** (統合言語クエリ) と呼ばれる .net の機能を使用して、これらのコレクションに対して厳密に型指定されたクエリ式を作成します。このようなコレクションは、データベースに対してコードを実行し、プログラミングできるオブジェクトを返します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-233">You are using a capability of .NET called **LINQ** (language-integrated query) to write strongly-typed query expressions against these collections - which will execute code against the database and return objects that you can program against.</span></span>
    > 
    > <span data-ttu-id="c03a7-234">LINQ の詳細については、 [msdn サイト](https://msdn.microsoft.com/library/bb397926&amp;#040;v=vs.110&amp;#041;.aspx)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c03a7-234">For more information about LINQ, please visit the [msdn site](https://msdn.microsoft.com/library/bb397926&amp;#040;v=vs.110&amp;#041;.aspx).</span></span>
3. <span data-ttu-id="c03a7-235">すべてのジャンルを取得するように**インデックス**アクションメソッドを更新します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-235">Update **Index** action method to retrieve all the genres.</span></span>

    <span data-ttu-id="c03a7-236">(コードスニペット-*モデルとデータアクセス-Ex1 Store Index*)</span><span class="sxs-lookup"><span data-stu-id="c03a7-236">(Code Snippet - *Models And Data Access - Ex1 Store Index*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample3.cs)]
4. <span data-ttu-id="c03a7-237">**インデックス**アクションメソッドを更新してすべてのジャンルを取得し、コレクションをリストに変換します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-237">Update **Index** action method to retrieve all the genres and transform the collection to a list.</span></span>

    <span data-ttu-id="c03a7-238">(コードスニペット-*モデルとデータアクセス-Ex1 Store GenreMenu*)</span><span class="sxs-lookup"><span data-stu-id="c03a7-238">(Code Snippet - *Models And Data Access - Ex1 Store GenreMenu*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample4.cs)]

<a id="Ex1Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a><span data-ttu-id="c03a7-239">タスク 5-アプリケーションを実行する</span><span class="sxs-lookup"><span data-stu-id="c03a7-239">Task 5 - Running the Application</span></span>

<span data-ttu-id="c03a7-240">このタスクでは、ハードコードされたものではなく、データベースに格納されているジャンルが [ストアインデックス] ページに表示されることを確認します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-240">In this task, you will check that the Store Index page will now display the Genres stored in the database instead of the hardcoded ones.</span></span> <span data-ttu-id="c03a7-241">**StoreController**が以前と同じエンティティを返すため、ビューテンプレートを変更する必要はありません。ただし、この時点では、データはデータベースから取得されます。</span><span class="sxs-lookup"><span data-stu-id="c03a7-241">There is no need to change the View template because the **StoreController** is returning the same entities as before, although this time the data will come from the database.</span></span>

1. <span data-ttu-id="c03a7-242">ソリューションをリビルドし、 **F5**キーを押してアプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-242">Rebuild the solution and press **F5** to run the Application.</span></span>
2. <span data-ttu-id="c03a7-243">プロジェクトはホームページから開始します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-243">The project starts in the Home page.</span></span> <span data-ttu-id="c03a7-244">**ジャンル**のメニューがハードコードされた一覧ではなくなり、データがデータベースから直接取得されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-244">Verify that the menu of **Genres** is no longer a hardcoded list, and the data is directly retrieved from the database.</span></span>

    ![BrowsingGenresFromDataBase](aspnet-mvc-4-models-and-data-access/_static/image16.png)

    <span data-ttu-id="c03a7-246">*データベースからのジャンルの参照*</span><span class="sxs-lookup"><span data-stu-id="c03a7-246">*Browsing Genres from the database*</span></span>
3. <span data-ttu-id="c03a7-247">次に、任意のジャンルを参照し、アルバムにデータベースが設定されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-247">Now browse to any genre and verify the albums are populated from database.</span></span>

    <span data-ttu-id="c03a7-248">![データベースからのアルバムの参照](aspnet-mvc-4-models-and-data-access/_static/image17.png "データベースからのアルバムの参照")</span><span class="sxs-lookup"><span data-stu-id="c03a7-248">![Browsing Albums from the database](aspnet-mvc-4-models-and-data-access/_static/image17.png "Browsing Albums from the database")</span></span>

    <span data-ttu-id="c03a7-249">*データベースからのアルバムの参照*</span><span class="sxs-lookup"><span data-stu-id="c03a7-249">*Browsing Albums from the database*</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Creating_a_Database_Using_Code_First"></a>
### <a name="exercise-2-creating-a-database-using-code-first"></a><span data-ttu-id="c03a7-250">演習 2: Code First を使用したデータベースの作成</span><span class="sxs-lookup"><span data-stu-id="c03a7-250">Exercise 2: Creating a Database Using Code First</span></span>

<span data-ttu-id="c03a7-251">この演習では、Code First 方法を使用して、MusicStore アプリケーションのテーブルを含むデータベースを作成し、そのデータにアクセスする方法を学習します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-251">In this exercise, you will learn how to use the Code First approach to create a database with the tables of the MusicStore application, and how to access its data.</span></span>

<span data-ttu-id="c03a7-252">モデルが生成されたら、StoreController を変更して、ハードコーディングされた値を使用するのではなく、データベースから取得したデータをビューテンプレートに提供します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-252">Once the model is generated, you will modify the StoreController to provide the View template with the data taken from the database, instead of using hardcoded values.</span></span>

> [!NOTE]
> <span data-ttu-id="c03a7-253">演習1を完了し、既に Database First 方法を使用していた場合は、別のプロセスで同じ結果を得る方法について学習します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-253">If you have completed Exercise 1 and have already worked with the Database First approach, you will now learn how to get the same results with a different process.</span></span> <span data-ttu-id="c03a7-254">演習1でよく使用されているタスクは、読みやすくするようにマークされています。</span><span class="sxs-lookup"><span data-stu-id="c03a7-254">The tasks that are in common with Exercise 1 have been marked to make your reading easier.</span></span> <span data-ttu-id="c03a7-255">演習1を完了していないが Code First アプローチについて学習したい場合は、この演習を開始して、トピック全体を網羅することができます。</span><span class="sxs-lookup"><span data-stu-id="c03a7-255">If you have not completed Exercise 1 but would like to learn the Code First approach, you can start from this exercise and get a full coverage of the topic.</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_-_Populating_Sample_Data"></a>
#### <a name="task-1---populating-sample-data"></a><span data-ttu-id="c03a7-256">タスク 1-サンプルデータの設定</span><span class="sxs-lookup"><span data-stu-id="c03a7-256">Task 1 - Populating Sample Data</span></span>

<span data-ttu-id="c03a7-257">このタスクでは、最初にコードを使用して作成されたときに、サンプルデータをデータベースに設定します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-257">In this task, you will populate the database with sample data when it is initially created using Code-First.</span></span>

1. <span data-ttu-id="c03a7-258">**Source/Ex2-CreatingADatabaseCodeFirst/begin/** folder にある**begin**ソリューションを開きます。</span><span class="sxs-lookup"><span data-stu-id="c03a7-258">Open the **Begin** solution located at **Source/Ex2-CreatingADatabaseCodeFirst/Begin/** folder.</span></span> <span data-ttu-id="c03a7-259">それ以外の場合は、前の演習を完了することによって得られた**終了**ソリューションを引き続き使用することができます。</span><span class="sxs-lookup"><span data-stu-id="c03a7-259">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="c03a7-260">提供された**Begin**ソリューションを開いた場合は、続行する前に、不足している NuGet パッケージをダウンロードする必要があります。</span><span class="sxs-lookup"><span data-stu-id="c03a7-260">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="c03a7-261">これを行うには、 **[プロジェクト]** メニューをクリックし、 **[NuGet パッケージの管理]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-261">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="c03a7-262">**[NuGet パッケージの管理]** ダイアログで、 **[復元]** をクリックして、不足しているパッケージをダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="c03a7-262">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="c03a7-263">最後に、[**ビルド** | **ビルド**] をクリックしてソリューションをビルドします。</span><span class="sxs-lookup"><span data-stu-id="c03a7-263">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="c03a7-264">NuGet を使用する利点の1つは、プロジェクトのすべてのライブラリを配布する必要がなく、プロジェクトのサイズを小さくすることです。</span><span class="sxs-lookup"><span data-stu-id="c03a7-264">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="c03a7-265">NuGet パワーツールを使用すると、パッケージのバージョンを app.config ファイルで指定することで、プロジェクトを初めて実行するときに必要なすべてのライブラリをダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="c03a7-265">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="c03a7-266">このため、このラボから既存のソリューションを開いた後に、これらの手順を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c03a7-266">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="c03a7-267">**SampleData.cs**ファイルを **[モデル]** フォルダーに追加します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-267">Add the **SampleData.cs** file to the **Models** folder.</span></span> <span data-ttu-id="c03a7-268">これを行うには、 **[モデル]** フォルダーを右クリックし、 **[追加]** をポイントして、 **[既存の項目]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c03a7-268">To do that, right-click **Models** folder, point to **Add** and then click **Existing Item**.</span></span> <span data-ttu-id="c03a7-269">**SampleData.cs**ファイルを参照**して選択します**。</span><span class="sxs-lookup"><span data-stu-id="c03a7-269">Browse to **\Source\Assets** and select the **SampleData.cs** file.</span></span>

    <span data-ttu-id="c03a7-270">![サンプルデータのコードの入力](aspnet-mvc-4-models-and-data-access/_static/image18.png "サンプルデータのコードの入力")</span><span class="sxs-lookup"><span data-stu-id="c03a7-270">![Sample data populate code](aspnet-mvc-4-models-and-data-access/_static/image18.png "Sample data populate code")</span></span>

    <span data-ttu-id="c03a7-271">*サンプルデータのコードの入力*</span><span class="sxs-lookup"><span data-stu-id="c03a7-271">*Sample data populate code*</span></span>
3. <span data-ttu-id="c03a7-272">**Global.asax.cs**ファイルを開き、次の*using*ステートメントを追加します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-272">Open the **Global.asax.cs** file and add the following *using* statements.</span></span>

    <span data-ttu-id="c03a7-273">(コードスニペット-*モデルとデータアクセス-Ex2 Global Global.asax using*)</span><span class="sxs-lookup"><span data-stu-id="c03a7-273">(Code Snippet - *Models And Data Access - Ex2 Global Asax Usings*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample5.cs)]
4. <span data-ttu-id="c03a7-274">**Application\_Start ()** メソッドで、次の行を追加してデータベース初期化子を設定します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-274">In the **Application\_Start()** method add the following line to set the database initializer.</span></span>

    <span data-ttu-id="c03a7-275">(コードスニペット-*モデルとデータアクセス-Ex2 Global Global.asax SetInitializer*)</span><span class="sxs-lookup"><span data-stu-id="c03a7-275">(Code Snippet - *Models And Data Access - Ex2 Global Asax SetInitializer*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample6.cs)]

<a id="Ex2Task2"></a>

<a id="Task_2_-_Configuring_the_connection_to_the_Database"></a>
#### <a name="task-2---configuring-the-connection-to-the-database"></a><span data-ttu-id="c03a7-276">タスク 2-データベースへの接続の構成</span><span class="sxs-lookup"><span data-stu-id="c03a7-276">Task 2 - Configuring the connection to the Database</span></span>

<span data-ttu-id="c03a7-277">プロジェクトにデータベースを既に追加したので、接続文字列を**web.config ファイルに記述します。**</span><span class="sxs-lookup"><span data-stu-id="c03a7-277">Now that you have already added a database to our project, you will write in the **Web.config** file the connection string.</span></span>

1. <span data-ttu-id="c03a7-278">**Web.config に接続**文字列を追加します。これを行うには、プロジェクトのルート**で web.config を開き、** defaultconnection という名前の接続文字列を **&lt;connectionStrings&gt;** セクションの次の行に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="c03a7-278">Add a connection string at **Web.config**. To do that, open **Web.config** at project root and replace the connection string named DefaultConnection with this line in the **&lt;connectionStrings&gt;** section:</span></span>

    <span data-ttu-id="c03a7-279">![Web.config ファイルの場所](aspnet-mvc-4-models-and-data-access/_static/image19.png "Web.config ファイルの場所")</span><span class="sxs-lookup"><span data-stu-id="c03a7-279">![Web.config file location](aspnet-mvc-4-models-and-data-access/_static/image19.png "Web.config file location")</span></span>

    <span data-ttu-id="c03a7-280">*Web.config ファイルの場所*</span><span class="sxs-lookup"><span data-stu-id="c03a7-280">*Web.config file location*</span></span>

    [!code-xml[Main](aspnet-mvc-4-models-and-data-access/samples/sample7.xml)]

<a id="Ex2Task3"></a>

<a id="Task_3_-_Working_with_the_Model"></a>
#### <a name="task-3---working-with-the-model"></a><span data-ttu-id="c03a7-281">タスク 3-モデルの操作</span><span class="sxs-lookup"><span data-stu-id="c03a7-281">Task 3 - Working with the Model</span></span>

<span data-ttu-id="c03a7-282">これで、データベースへの接続が既に構成されているので、モデルをデータベーステーブルにリンクします。</span><span class="sxs-lookup"><span data-stu-id="c03a7-282">Now that you have already configured the connection to the database, you will link the model with the database tables.</span></span> <span data-ttu-id="c03a7-283">このタスクでは、Code First を使用してデータベースにリンクされるクラスを作成します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-283">In this task, you will create a class that will be linked to the database with Code First.</span></span> <span data-ttu-id="c03a7-284">変更する必要がある POCO モデルクラスが存在することに注意してください。</span><span class="sxs-lookup"><span data-stu-id="c03a7-284">Remember that there is an existent POCO model class that should be modified.</span></span>

> [!NOTE]
> <span data-ttu-id="c03a7-285">演習1を完了した場合は、ウィザードによってこの手順が実行されたことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="c03a7-285">If you completed Exercise 1, you will note that this step was performed by a wizard.</span></span> <span data-ttu-id="c03a7-286">Code First には、データエンティティにリンクされるクラスを手動で作成します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-286">By doing Code First, you will manually create classes that will be linked to data entities.</span></span>

1. <span data-ttu-id="c03a7-287">**モデル**プロジェクトフォルダーから POCO モデルクラスの**ジャンル**を開き、ID を含めます。</span><span class="sxs-lookup"><span data-stu-id="c03a7-287">Open the POCO model class **Genre** from **Models** project folder and include an ID.</span></span> <span data-ttu-id="c03a7-288">**Genreid**という名前の int プロパティを使用します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-288">Use an int property with the name **GenreId**.</span></span>

    <span data-ttu-id="c03a7-289">(コードスニペット-*モデルとデータアクセス-Ex2 Code First Genre*)</span><span class="sxs-lookup"><span data-stu-id="c03a7-289">(Code Snippet - *Models And Data Access - Ex2 Code First Genre*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample8.cs)]

    > [!NOTE]
    > <span data-ttu-id="c03a7-290">Code First 規則を使用するには、クラス Genre に自動的に検出される主キープロパティが必要です。</span><span class="sxs-lookup"><span data-stu-id="c03a7-290">To work with Code First conventions, the class Genre must have a primary key property that will be automatically detected.</span></span>
    > 
    > <span data-ttu-id="c03a7-291">Code First の規則の詳細については、この[msdn の記事](https://msdn.microsoft.com/library/hh161541&amp;#040;v=vs.103&amp;#041;.aspx)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c03a7-291">You can read more about Code First Conventions in this [msdn article](https://msdn.microsoft.com/library/hh161541&amp;#040;v=vs.103&amp;#041;.aspx).</span></span>
2. <span data-ttu-id="c03a7-292">次に、**モデル**プロジェクトフォルダーから POCO モデルクラス**アルバム**を開き、外部キーを含め、 **Genreid**と**artistid**という名前のプロパティを作成します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-292">Now, open the POCO model class **Album** from **Models** project folder and include the foreign keys, create properties with the names **GenreId** and **ArtistId**.</span></span> <span data-ttu-id="c03a7-293">このクラスには、主キーの**Genreid**が既に含まれています。</span><span class="sxs-lookup"><span data-stu-id="c03a7-293">This class already have the **GenreId** for the primary key.</span></span>

    <span data-ttu-id="c03a7-294">(コードスニペット-*モデルとデータアクセス-Ex2 Code First アルバム*)</span><span class="sxs-lookup"><span data-stu-id="c03a7-294">(Code Snippet - *Models And Data Access - Ex2 Code First Album*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample9.cs)]
3. <span data-ttu-id="c03a7-295">POCO モデルクラスの**アーティスト**を開き、 **artistid**プロパティを含めます。</span><span class="sxs-lookup"><span data-stu-id="c03a7-295">Open the POCO model class **Artist** and include the **ArtistId** property.</span></span>

    <span data-ttu-id="c03a7-296">(コードスニペット-*モデルとデータアクセス-Ex2 Code First アーティスト*)</span><span class="sxs-lookup"><span data-stu-id="c03a7-296">(Code Snippet - *Models And Data Access - Ex2 Code First Artist*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample10.cs)]
4. <span data-ttu-id="c03a7-297">**モデル** プロジェクトフォルダーを右クリックし、追加 を選択します。 **クラス**。</span><span class="sxs-lookup"><span data-stu-id="c03a7-297">Right-click the **Models** project folder and select **Add | Class**.</span></span> <span data-ttu-id="c03a7-298">ファイルに**MusicStoreEntities.cs**という名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-298">Name the file **MusicStoreEntities.cs**.</span></span> <span data-ttu-id="c03a7-299">次に、[追加] をクリックし**ます。**</span><span class="sxs-lookup"><span data-stu-id="c03a7-299">Then, click **Add.**</span></span>

    <span data-ttu-id="c03a7-300">![クラスの追加](aspnet-mvc-4-models-and-data-access/_static/image20.png "クラスの追加")</span><span class="sxs-lookup"><span data-stu-id="c03a7-300">![Adding a class](aspnet-mvc-4-models-and-data-access/_static/image20.png "Adding a class")</span></span>

    <span data-ttu-id="c03a7-301">*新しい項目の追加*</span><span class="sxs-lookup"><span data-stu-id="c03a7-301">*Adding a new item*</span></span>

    <span data-ttu-id="c03a7-302">![Class2 の追加](aspnet-mvc-4-models-and-data-access/_static/image21.png "Class2 の追加")</span><span class="sxs-lookup"><span data-stu-id="c03a7-302">![Adding a class2](aspnet-mvc-4-models-and-data-access/_static/image21.png "Adding a class2")</span></span>

    <span data-ttu-id="c03a7-303">*クラスの追加*</span><span class="sxs-lookup"><span data-stu-id="c03a7-303">*Adding a class*</span></span>
5. <span data-ttu-id="c03a7-304">先ほど作成したクラスを開き、 **MusicStoreEntities.cs**と**いう名前空間**と、その名前空間を追加**します。**</span><span class="sxs-lookup"><span data-stu-id="c03a7-304">Open the class you have just created, **MusicStoreEntities.cs**, and include the namespaces **System.Data.Entity** and **System.Data.Entity.Infrastructure**.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample11.cs)]
6. <span data-ttu-id="c03a7-305">クラス宣言を置き換えて**Dbcontext**クラスを拡張します。パブリック**dbcontext**を宣言し、 **onmodelcreating**メソッドをオーバーライドします。</span><span class="sxs-lookup"><span data-stu-id="c03a7-305">Replace the class declaration to extend the **DbContext** class: declare a public **DBSet** and override **OnModelCreating** method.</span></span> <span data-ttu-id="c03a7-306">この手順の後には、モデルを Entity Framework にリンクするドメインクラスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="c03a7-306">After this step you will get a domain class that will link your model with the Entity Framework.</span></span> <span data-ttu-id="c03a7-307">そのためには、クラスコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="c03a7-307">In order to do that, replace the class code with the following:</span></span>

    <span data-ttu-id="c03a7-308">(コードスニペット-*モデルとデータアクセス-Ex2 Code First MusicStoreEntities*)</span><span class="sxs-lookup"><span data-stu-id="c03a7-308">(Code Snippet - *Models And Data Access - Ex2 Code First MusicStoreEntities*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample12.cs)]

> [!NOTE]
> <span data-ttu-id="c03a7-309">Entity Framework **Dbcontext**と**dbcontext**を使用すると、POCO クラスのジャンルに対してクエリを実行できます。</span><span class="sxs-lookup"><span data-stu-id="c03a7-309">With Entity Framework **DbContext** and **DBSet** you will be able to query the POCO class Genre.</span></span> <span data-ttu-id="c03a7-310">**Onmodelcreating**メソッドを拡張することで、ジャンルがデータベーステーブルにどのようにマップされるかを**コード**で指定します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-310">By extending **OnModelCreating** method, you are specifying in the **code** how Genre will be mapped to a database table.</span></span> <span data-ttu-id="c03a7-311">DBContext と Dbcontext の詳細については、msdn の記事「 [link](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c03a7-311">You can find more information about DBContext and DBSet in this msdn article: [link](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx)</span></span>

<a id="Ex2Task4"></a>

<a id="Task_4_-_Querying_the_Database"></a>
#### <a name="task-4---querying-the-database"></a><span data-ttu-id="c03a7-312">タスク 4-データベースに対してクエリを実行する</span><span class="sxs-lookup"><span data-stu-id="c03a7-312">Task 4 - Querying the Database</span></span>

<span data-ttu-id="c03a7-313">このタスクでは、StoreController クラスを更新して、ハードコーディングされたデータを使用するのではなく、データベースからデータを取得します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-313">In this task, you will update the StoreController class so that, instead of using hardcoded data, it will retrieve it from the database.</span></span>

> [!NOTE]
> <span data-ttu-id="c03a7-314">この作業は、演習1では一般的です。</span><span class="sxs-lookup"><span data-stu-id="c03a7-314">This task is in common with Exercise 1.</span></span>
> 
> <span data-ttu-id="c03a7-315">演習1を完了した場合、これらの手順は両方の方法で同じになります (データベースの最初またはコードが最初)。</span><span class="sxs-lookup"><span data-stu-id="c03a7-315">If you completed Exercise 1 you will note these steps are the same in both approaches (Database first or Code first).</span></span> <span data-ttu-id="c03a7-316">データがモデルにリンクされている方法は異なりますが、データエンティティへのアクセスはコントローラーから透過的に行われています。</span><span class="sxs-lookup"><span data-stu-id="c03a7-316">They are different in how the data is linked with the model, but the access to data entities is yet transparent from the controller.</span></span>

1. <span data-ttu-id="c03a7-317">**Controllers\StoreController.cs**を開き、次のフィールドをクラスに追加して、 **storedb**という名前の**MusicStoreEntities**クラスのインスタンスを保持します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-317">Open **Controllers\StoreController.cs** and add the following field to the class to hold an instance of the **MusicStoreEntities** class, named **storeDB**:</span></span>

    <span data-ttu-id="c03a7-318">(コードスニペット-*モデルとデータアクセス-Ex1 storeDB*)</span><span class="sxs-lookup"><span data-stu-id="c03a7-318">(Code Snippet - *Models And Data Access - Ex1 storeDB*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample13.cs)]
2. <span data-ttu-id="c03a7-319">**MusicStoreEntities**クラスは、データベース内の各テーブルのコレクションプロパティを公開します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-319">The **MusicStoreEntities** class exposes a collection property for each table in the database.</span></span> <span data-ttu-id="c03a7-320">すべての**アルバム**を含むジャンルを取得するように、**参照**アクションメソッドを更新します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-320">Update **Browse** action method to retrieve a Genre with all of the **Albums**.</span></span>

    <span data-ttu-id="c03a7-321">(コードスニペット-*モデルとデータアクセス-Ex2 Store 参照*)</span><span class="sxs-lookup"><span data-stu-id="c03a7-321">(Code Snippet - *Models And Data Access - Ex2 Store Browse*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample14.cs)]

    > [!NOTE]
    > <span data-ttu-id="c03a7-322">**LINQ** (統合言語クエリ) と呼ばれる .net の機能を使用して、これらのコレクションに対して厳密に型指定されたクエリ式を作成します。このようなコレクションは、データベースに対してコードを実行し、プログラミングできるオブジェクトを返します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-322">You are using a capability of .NET called **LINQ** (language-integrated query) to write strongly-typed query expressions against these collections - which will execute code against the database and return objects that you can program against.</span></span>
    > 
    > <span data-ttu-id="c03a7-323">LINQ の詳細については、 [msdn サイト](https://msdn.microsoft.com/library/bb397926(v=vs.110).aspx)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c03a7-323">For more information about LINQ, please visit the [msdn site](https://msdn.microsoft.com/library/bb397926(v=vs.110).aspx).</span></span>
3. <span data-ttu-id="c03a7-324">すべてのジャンルを取得するように**インデックス**アクションメソッドを更新します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-324">Update **Index** action method to retrieve all the genres.</span></span>

    <span data-ttu-id="c03a7-325">(コードスニペット-*モデルとデータアクセス-Ex2 Store Index*)</span><span class="sxs-lookup"><span data-stu-id="c03a7-325">(Code Snippet - *Models And Data Access - Ex2 Store Index*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample15.cs)]
4. <span data-ttu-id="c03a7-326">**インデックス**アクションメソッドを更新してすべてのジャンルを取得し、コレクションをリストに変換します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-326">Update **Index** action method to retrieve all the genres and transform the collection to a list.</span></span>

    <span data-ttu-id="c03a7-327">(コードスニペット-*モデルとデータアクセス-Ex2 Store GenreMenu*)</span><span class="sxs-lookup"><span data-stu-id="c03a7-327">(Code Snippet - *Models And Data Access - Ex2 Store GenreMenu*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample16.cs)]

<a id="Ex2Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a><span data-ttu-id="c03a7-328">タスク 5-アプリケーションを実行する</span><span class="sxs-lookup"><span data-stu-id="c03a7-328">Task 5 - Running the Application</span></span>

<span data-ttu-id="c03a7-329">このタスクでは、ハードコードされたものではなく、データベースに格納されているジャンルが [ストアインデックス] ページに表示されることを確認します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-329">In this task, you will check that the Store Index page will now display the Genres stored in the database instead of the hardcoded ones.</span></span> <span data-ttu-id="c03a7-330">ビューテンプレートを変更する必要はありません。これは、 **StoreController**が以前と同じ**Storeindexindexview**を返すためですが、今回はデータがデータベースから取得されるためです。</span><span class="sxs-lookup"><span data-stu-id="c03a7-330">There is no need to change the View template because the **StoreController** is returning the same **StoreIndexViewModel** as before, but this time the data will come from the database.</span></span>

1. <span data-ttu-id="c03a7-331">ソリューションをリビルドし、 **F5**キーを押してアプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-331">Rebuild the solution and press **F5** to run the Application.</span></span>
2. <span data-ttu-id="c03a7-332">プロジェクトはホームページから開始します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-332">The project starts in the Home page.</span></span> <span data-ttu-id="c03a7-333">**ジャンル**のメニューがハードコードされた一覧ではなくなり、データがデータベースから直接取得されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-333">Verify that the menu of **Genres** is no longer a hardcoded list, and the data is directly retrieved from the database.</span></span>

    ![BrowsingGenresFromDataBase](aspnet-mvc-4-models-and-data-access/_static/image22.png)

    <span data-ttu-id="c03a7-335">*データベースからのジャンルの参照*</span><span class="sxs-lookup"><span data-stu-id="c03a7-335">*Browsing Genres from the database*</span></span>
3. <span data-ttu-id="c03a7-336">次に、任意のジャンルを参照し、アルバムにデータベースが設定されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-336">Now browse to any genre and verify the albums are populated from database.</span></span>

    <span data-ttu-id="c03a7-337">![データベースからのアルバムの参照](aspnet-mvc-4-models-and-data-access/_static/image23.png "データベースからのアルバムの参照")</span><span class="sxs-lookup"><span data-stu-id="c03a7-337">![Browsing Albums from the database](aspnet-mvc-4-models-and-data-access/_static/image23.png "Browsing Albums from the database")</span></span>

    <span data-ttu-id="c03a7-338">*データベースからのアルバムの参照*</span><span class="sxs-lookup"><span data-stu-id="c03a7-338">*Browsing Albums from the database*</span></span>

<a id="Exercise3"></a>

<a id="Exercise_3_Querying_the_Database_with_Parameters"></a>
### <a name="exercise-3-querying-the-database-with-parameters"></a><span data-ttu-id="c03a7-339">演習 3: パラメーターを使用してデータベースにクエリを実行する</span><span class="sxs-lookup"><span data-stu-id="c03a7-339">Exercise 3: Querying the Database with Parameters</span></span>

<span data-ttu-id="c03a7-340">この演習では、パラメーターを使用してデータベースに対してクエリを実行する方法と、クエリ結果の整形を使用する方法について学習します。この機能を使用すると、データベースへのアクセス回数を減らすことで、より効率的な方法でデータを取得できます。</span><span class="sxs-lookup"><span data-stu-id="c03a7-340">In this exercise, you will learn how to query the database using parameters, and how to use Query Result Shaping, a feature that reduces the number database accesses retrieving data in a more efficient way.</span></span>

> [!NOTE]
> <span data-ttu-id="c03a7-341">クエリ結果の整形の詳細については、次の[msdn の記事](https://msdn.microsoft.com/library/bb896272&amp;#040;v=vs.100&amp;#041;.aspx)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c03a7-341">For further information on Query Result Shaping, visit the following [msdn article](https://msdn.microsoft.com/library/bb896272&amp;#040;v=vs.100&amp;#041;.aspx).</span></span>

<a id="Ex3Task1"></a>

<a id="Task_1_-_Modifying_StoreController_to_Retrieve_Albums_from_Database"></a>
#### <a name="task-1---modifying-storecontroller-to-retrieve-albums-from-database"></a><span data-ttu-id="c03a7-342">タスク 1-StoreController を変更してデータベースからアルバムを取得する</span><span class="sxs-lookup"><span data-stu-id="c03a7-342">Task 1 - Modifying StoreController to Retrieve Albums from Database</span></span>

<span data-ttu-id="c03a7-343">このタスクでは、 **StoreController**クラスを変更して、特定のジャンルからアルバムを取得するためにデータベースにアクセスできるようにします。</span><span class="sxs-lookup"><span data-stu-id="c03a7-343">In this task, you will change the **StoreController** class to access the database to retrieve albums from a specific genre.</span></span>

1. <span data-ttu-id="c03a7-344">データベース優先の方法を使用する場合は、 **Source\Ex3-QueryingTheDatabaseWithParametersCodeFirst\Begin**フォルダーにある**Begin**ソリューションを開き、Code first の方法または**Source\Ex3-QueryingTheDatabaseWithParametersDBFirst\Begin**フォルダーを使用します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-344">Open the **Begin** solution located at the **Source\Ex3-QueryingTheDatabaseWithParametersCodeFirst\Begin** folder if you want to use Code-First approach or **Source\Ex3-QueryingTheDatabaseWithParametersDBFirst\Begin** folder if you want to use Database-First approach.</span></span> <span data-ttu-id="c03a7-345">それ以外の場合は、前の演習を完了することによって得られた**終了**ソリューションを引き続き使用することができます。</span><span class="sxs-lookup"><span data-stu-id="c03a7-345">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="c03a7-346">提供された**Begin**ソリューションを開いた場合は、続行する前に、不足している NuGet パッケージをダウンロードする必要があります。</span><span class="sxs-lookup"><span data-stu-id="c03a7-346">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="c03a7-347">これを行うには、 **[プロジェクト]** メニューをクリックし、 **[NuGet パッケージの管理]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-347">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="c03a7-348">**[NuGet パッケージの管理]** ダイアログで、 **[復元]** をクリックして、不足しているパッケージをダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="c03a7-348">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="c03a7-349">最後に、[**ビルド** | **ビルド**] をクリックしてソリューションをビルドします。</span><span class="sxs-lookup"><span data-stu-id="c03a7-349">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="c03a7-350">NuGet を使用する利点の1つは、プロジェクトのすべてのライブラリを配布する必要がなく、プロジェクトのサイズを小さくすることです。</span><span class="sxs-lookup"><span data-stu-id="c03a7-350">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="c03a7-351">NuGet パワーツールを使用すると、パッケージのバージョンを app.config ファイルで指定することで、プロジェクトを初めて実行するときに必要なすべてのライブラリをダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="c03a7-351">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="c03a7-352">このため、このラボから既存のソリューションを開いた後に、これらの手順を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c03a7-352">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="c03a7-353">**StoreController**クラスを開いて、**参照**アクションメソッドを変更します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-353">Open the **StoreController** class to change the **Browse** action method.</span></span> <span data-ttu-id="c03a7-354">これを行うには、**ソリューションエクスプローラー**で**Controllers**フォルダーを展開し、 **StoreController.cs**をダブルクリックします。</span><span class="sxs-lookup"><span data-stu-id="c03a7-354">To do this, in the **Solution Explorer**, expand the **Controllers** folder and double-click **StoreController.cs**.</span></span>
3. <span data-ttu-id="c03a7-355">特定のジャンルのアルバムを取得するように、**参照**アクションメソッドを変更します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-355">Change the **Browse** action method to retrieve albums for a specific genre.</span></span> <span data-ttu-id="c03a7-356">これを行うには、次のコードを置き換えます。</span><span class="sxs-lookup"><span data-stu-id="c03a7-356">To do this, replace the following code:</span></span>

    <span data-ttu-id="c03a7-357">(コードスニペット-*モデルとデータアクセス-Ex3 StoreController BrowseMethod*)</span><span class="sxs-lookup"><span data-stu-id="c03a7-357">(Code Snippet - *Models And Data Access - Ex3 StoreController BrowseMethod*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample17.cs)]

> [!NOTE]
> <span data-ttu-id="c03a7-358">エンティティのコレクションを設定するには、 **Include**メソッドを使用して、アルバムを取得するように指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c03a7-358">To populate a collection of the entity, you need to use the **Include** method to specify you want to retrieve the albums too.</span></span> <span data-ttu-id="c03a7-359">を使用できます。LINQ では**単一 ()** の拡張機能。この場合、アルバムには1つのジャンルのみが必要です。</span><span class="sxs-lookup"><span data-stu-id="c03a7-359">You can use the .**Single()** extension in LINQ because in this case only one genre is expected for an album.</span></span> <span data-ttu-id="c03a7-360">**Single ()** メソッドは、ラムダ式をパラメーターとして受け取ります。この場合は、名前が定義されている値と一致するように、1つの Genre オブジェクトを指定します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-360">The **Single()** method takes a Lambda expression as a parameter, which in this case specifies a single Genre object such that its name matches the value defined.</span></span>
> 
> <span data-ttu-id="c03a7-361">Genre オブジェクトを取得するときに、読み込みたい他の関連エンティティも指定できる機能を利用できます。</span><span class="sxs-lookup"><span data-stu-id="c03a7-361">You will take advantage of a feature that allows you to indicate other related entities you want loaded as well when the Genre object is retrieved.</span></span> <span data-ttu-id="c03a7-362">この機能は**クエリ結果の整形**と呼ばれ、データベースにアクセスして情報を取得するために必要な回数を減らすことができます。</span><span class="sxs-lookup"><span data-stu-id="c03a7-362">This feature is called **Query Result Shaping**, and enables you to reduce the number of times needed to access the database to retrieve information.</span></span> <span data-ttu-id="c03a7-363">このシナリオでは、取得したジャンルのアルバムを事前にフェッチします。</span><span class="sxs-lookup"><span data-stu-id="c03a7-363">In this scenario, you will want to pre-fetch the Albums for the Genre you retrieve.</span></span>
> 
> <span data-ttu-id="c03a7-364">このクエリには、**ジャンル (&quot;アルバム&quot;)** が含まれており、関連するアルバムも必要であることを示しています。</span><span class="sxs-lookup"><span data-stu-id="c03a7-364">The query includes **Genres.Include(&quot;Albums&quot;)** to indicate that you want related albums as well.</span></span> <span data-ttu-id="c03a7-365">これにより、1つのデータベース要求でジャンルとアルバムの両方のデータを取得するため、より効率的なアプリケーションが得られます。</span><span class="sxs-lookup"><span data-stu-id="c03a7-365">This will result in a more efficient application, since it will retrieve both Genre and Album data in a single database request.</span></span>

<a id="Ex3Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a><span data-ttu-id="c03a7-366">タスク 2-アプリケーションの実行</span><span class="sxs-lookup"><span data-stu-id="c03a7-366">Task 2 - Running the Application</span></span>

<span data-ttu-id="c03a7-367">このタスクでは、アプリケーションを実行し、データベースから特定のジャンルのアルバムを取得します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-367">In this task, you will run the application and retrieve albums of a specific genre from the database.</span></span>

1. <span data-ttu-id="c03a7-368">**F5**キーを押してアプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-368">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="c03a7-369">プロジェクトはホームページから開始します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-369">The project starts in the Home page.</span></span> <span data-ttu-id="c03a7-370">URL を変更して、データベースから結果が取得されていることを確認**します。**</span><span class="sxs-lookup"><span data-stu-id="c03a7-370">Change the URL to **/Store/Browse?genre=Pop** to verify that the results are being retrieved from the database.</span></span>

    <span data-ttu-id="c03a7-371">![ジャンル別の閲覧](aspnet-mvc-4-models-and-data-access/_static/image24.png "ジャンル別の閲覧")</span><span class="sxs-lookup"><span data-stu-id="c03a7-371">![Browsing by genre](aspnet-mvc-4-models-and-data-access/_static/image24.png "Browsing by genre")</span></span>

    <span data-ttu-id="c03a7-372">*参照/ストア/参照? ジャンル = Pop*</span><span class="sxs-lookup"><span data-stu-id="c03a7-372">*Browsing /Store/Browse?genre=Pop*</span></span>

<a id="Ex3Task3"></a>

<a id="Task_3_-_Accessing_Albums_by_Id"></a>
#### <a name="task-3---accessing-albums-by-id"></a><span data-ttu-id="c03a7-373">タスク 3-Id でアルバムにアクセスする</span><span class="sxs-lookup"><span data-stu-id="c03a7-373">Task 3 - Accessing Albums by Id</span></span>

<span data-ttu-id="c03a7-374">このタスクでは、前の手順を繰り返して、Id でアルバムを取得します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-374">In this task, you will repeat the previous procedure to get albums by their Id.</span></span>

1. <span data-ttu-id="c03a7-375">必要に応じてブラウザーを閉じて、Visual Studio に戻ります。</span><span class="sxs-lookup"><span data-stu-id="c03a7-375">Close the browser if needed, to return to Visual Studio.</span></span> <span data-ttu-id="c03a7-376">**StoreController**クラスを開き、 **Details**アクションメソッドを変更します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-376">Open the **StoreController** class to change the **Details** action method.</span></span> <span data-ttu-id="c03a7-377">これを行うには、**ソリューションエクスプローラー**で**Controllers**フォルダーを展開し、 **StoreController.cs**をダブルクリックします。</span><span class="sxs-lookup"><span data-stu-id="c03a7-377">To do this, in the **Solution Explorer**, expand the **Controllers** folder and double-click **StoreController.cs**.</span></span>
2. <span data-ttu-id="c03a7-378">**Id**に基づいてアルバムの詳細を取得するように、**詳細**アクションメソッドを変更します。これを行うには、次のコードを置き換えます。</span><span class="sxs-lookup"><span data-stu-id="c03a7-378">Change the **Details** action method to retrieve albums details based on their **Id**. To do this, replace the following code:</span></span>

    <span data-ttu-id="c03a7-379">(コードスニペット-*モデルとデータアクセス-Ex3 StoreController のメソッド*)</span><span class="sxs-lookup"><span data-stu-id="c03a7-379">(Code Snippet - *Models And Data Access - Ex3 StoreController DetailsMethod*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample18.cs)]

<a id="Ex3Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a><span data-ttu-id="c03a7-380">タスク 4-アプリケーションを実行する</span><span class="sxs-lookup"><span data-stu-id="c03a7-380">Task 4 - Running the Application</span></span>

<span data-ttu-id="c03a7-381">このタスクでは、web ブラウザーでアプリケーションを実行し、Id でアルバムの詳細を取得します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-381">In this task, you will run the Application in a web browser and obtain album details by their Id.</span></span>

1. <span data-ttu-id="c03a7-382">**F5**キーを押してアプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-382">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="c03a7-383">プロジェクトはホームページから開始します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-383">The project starts in the Home page.</span></span> <span data-ttu-id="c03a7-384">[URL] を「 **/Store/** 設定」に変更するか、ジャンルを参照してアルバムを選択し、結果がデータベースから取得されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-384">Change the URL to **/Store/Details/51** or browse the genres and select an album to verify that the results are being retrieved from the database.</span></span>

    <span data-ttu-id="c03a7-385">![詳細の参照](aspnet-mvc-4-models-and-data-access/_static/image25.png "詳細の参照")</span><span class="sxs-lookup"><span data-stu-id="c03a7-385">![Browsing Details](aspnet-mvc-4-models-and-data-access/_static/image25.png "Browsing Details")</span></span>

    <span data-ttu-id="c03a7-386">*参照/表示/表示/51*</span><span class="sxs-lookup"><span data-stu-id="c03a7-386">*Browsing /Store/Details/51*</span></span>

> [!NOTE]
> <span data-ttu-id="c03a7-387">また、 [「付録 B: Web 配置を使用した ASP.NET MVC 4 アプリケーションの発行](#AppendixB)」に従って、このアプリケーションを Windows Azure の Web サイトにデプロイすることもできます。</span><span class="sxs-lookup"><span data-stu-id="c03a7-387">Additionally, you can deploy this application to Windows Azure Web Sites following [Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy](#AppendixB).</span></span>

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="c03a7-388">まとめ</span><span class="sxs-lookup"><span data-stu-id="c03a7-388">Summary</span></span>

<span data-ttu-id="c03a7-389">このハンズオンラボを完了することで、 **Database First**アプローチと**Code First**方法を使用して、ASP.NET MVC モデルとデータアクセスの基礎を学習しました。</span><span class="sxs-lookup"><span data-stu-id="c03a7-389">By completing this Hands-on Lab you have learned the fundamentals of ASP.NET MVC Models and Data Access, using the **Database First** approach as well as the **Code First** Approach:</span></span>

- <span data-ttu-id="c03a7-390">データを使用するためにデータベースをソリューションに追加する方法</span><span class="sxs-lookup"><span data-stu-id="c03a7-390">How to add a database to the solution in order to consume its data</span></span>
- <span data-ttu-id="c03a7-391">ハードコーディングされたものではなく、データベースから取得したデータを使用してビューテンプレートを提供するようにコントローラーを更新する方法</span><span class="sxs-lookup"><span data-stu-id="c03a7-391">How to update Controllers to provide View templates with the data taken from the database instead of hard-coded one</span></span>
- <span data-ttu-id="c03a7-392">パラメーターを使用してデータベースに対してクエリを実行する方法</span><span class="sxs-lookup"><span data-stu-id="c03a7-392">How to query the database using parameters</span></span>
- <span data-ttu-id="c03a7-393">クエリ結果の整形を使用する方法。データベースへのアクセス数を減らし、データをより効率的な方法で取得する機能です。</span><span class="sxs-lookup"><span data-stu-id="c03a7-393">How to use the Query Result Shaping, a feature that reduces the number of database accesses, retrieving data in a more efficient way</span></span>
- <span data-ttu-id="c03a7-394">Microsoft Entity Framework で Database First と Code First の両方のアプローチを使用してデータベースをモデルにリンクする方法</span><span class="sxs-lookup"><span data-stu-id="c03a7-394">How to use both Database First and Code First approaches in Microsoft Entity Framework to link the database with the model</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="c03a7-395">付録 A: Visual Studio Express 2012 を Web 用にインストールする</span><span class="sxs-lookup"><span data-stu-id="c03a7-395">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="c03a7-396">**[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)** を使用して、Web または別の &quot;Express&quot; バージョン**用に Microsoft Visual Studio Express 2012**をインストールできます。</span><span class="sxs-lookup"><span data-stu-id="c03a7-396">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="c03a7-397">次の手順では、 *Microsoft Web Platform Installer*を使用して*Visual studio Express 2012 for Web*をインストールするために必要な手順について説明します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-397">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="c03a7-398">[[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)にアクセスします。</span><span class="sxs-lookup"><span data-stu-id="c03a7-398">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="c03a7-399">または、Web Platform Installer が既にインストールされている場合は、それを開いて、製品 &quot;<em>Visual Studio Express 2012 For web With Windows AZURE SDK</em>&quot;を検索することもできます。</span><span class="sxs-lookup"><span data-stu-id="c03a7-399">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="c03a7-400">**[今すぐインストール]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c03a7-400">Click on **Install Now**.</span></span> <span data-ttu-id="c03a7-401">**Web Platform Installer**がない場合は、最初にダウンロードしてインストールするようにリダイレクトされます。</span><span class="sxs-lookup"><span data-stu-id="c03a7-401">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="c03a7-402">**Web Platform Installer**が開いたら、 **[インストール]** をクリックしてセットアップを開始します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-402">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="c03a7-403">![Visual Studio Express のインストール](aspnet-mvc-4-models-and-data-access/_static/image26.png "Visual Studio Express のインストール")</span><span class="sxs-lookup"><span data-stu-id="c03a7-403">![Install Visual Studio Express](aspnet-mvc-4-models-and-data-access/_static/image26.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="c03a7-404">*Visual Studio Express のインストール*</span><span class="sxs-lookup"><span data-stu-id="c03a7-404">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="c03a7-405">すべての製品のライセンスと条項を読み、[**同意**する] をクリックして続行します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-405">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![ライセンス条項に同意する](aspnet-mvc-4-models-and-data-access/_static/image27.png)

    <span data-ttu-id="c03a7-407">*ライセンス条項に同意する*</span><span class="sxs-lookup"><span data-stu-id="c03a7-407">*Accepting the license terms*</span></span>
5. <span data-ttu-id="c03a7-408">ダウンロードとインストールのプロセスが完了するまで待ちます。</span><span class="sxs-lookup"><span data-stu-id="c03a7-408">Wait until the downloading and installation process completes.</span></span>

    ![Installation progress](aspnet-mvc-4-models-and-data-access/_static/image28.png)

    <span data-ttu-id="c03a7-410">*インストールの進行状況*</span><span class="sxs-lookup"><span data-stu-id="c03a7-410">*Installation progress*</span></span>
6. <span data-ttu-id="c03a7-411">インストールが完了したら、 **[完了]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c03a7-411">When the installation completes, click **Finish**.</span></span>

    ![インストールの完了](aspnet-mvc-4-models-and-data-access/_static/image29.png)

    <span data-ttu-id="c03a7-413">*インストールの完了*</span><span class="sxs-lookup"><span data-stu-id="c03a7-413">*Installation completed*</span></span>
7. <span data-ttu-id="c03a7-414">**[終了]** をクリックして Web Platform Installer を閉じます。</span><span class="sxs-lookup"><span data-stu-id="c03a7-414">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="c03a7-415">Web 用の Visual Studio Express を開くには、**スタート**画面にアクセスして &quot;**VS Express**&quot;の書き込みを開始し、 **[VS Express for Web]** タイルをクリックします。</span><span class="sxs-lookup"><span data-stu-id="c03a7-415">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![VS Express for Web タイル](aspnet-mvc-4-models-and-data-access/_static/image30.png)

    <span data-ttu-id="c03a7-417">*VS Express for Web タイル*</span><span class="sxs-lookup"><span data-stu-id="c03a7-417">*VS Express for Web tile*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="c03a7-418">付録 B: Web 配置を使用した ASP.NET MVC 4 アプリケーションの発行</span><span class="sxs-lookup"><span data-stu-id="c03a7-418">Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

<span data-ttu-id="c03a7-419">この付録では、windows azure 管理ポータルから新しい web サイトを作成し、Windows Azure によって提供される Web 配置公開機能を活用して、ラボに従って取得したアプリケーションを発行する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-419">This appendix will show you how to create a new web site from the Windows Azure Management Portal and publish the application you obtained by following the lab, taking advantage of the Web Deploy publishing feature provided by Windows Azure.</span></span>

<a id="ApxBTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a><span data-ttu-id="c03a7-420">タスク 1-Windows Azure ポータルから新しい Web サイトを作成する</span><span class="sxs-lookup"><span data-stu-id="c03a7-420">Task 1 - Creating a New Web Site from the Windows Azure Portal</span></span>

1. <span data-ttu-id="c03a7-421">[Windows Azure 管理ポータル](https://manage.windowsazure.com/)にアクセスし、サブスクリプションに関連付けられている Microsoft 資格情報を使用してサインインします。</span><span class="sxs-lookup"><span data-stu-id="c03a7-421">Go to the [Windows Azure Management Portal](https://manage.windowsazure.com/) and sign in using the Microsoft credentials associated with your subscription.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c03a7-422">Windows Azure では、10 ASP.NET の Web サイトを無料でホストし、トラフィックの増加に合わせて拡張できます。</span><span class="sxs-lookup"><span data-stu-id="c03a7-422">With Windows Azure you can host 10 ASP.NET Web Sites for free and then scale as your traffic grows.</span></span> <span data-ttu-id="c03a7-423">[ここで](https://aka.ms/aspnet-hol-azure)サインアップできます。</span><span class="sxs-lookup"><span data-stu-id="c03a7-423">You can sign up [here](https://aka.ms/aspnet-hol-azure).</span></span>

    <span data-ttu-id="c03a7-424">![Windows Azure portal にログオンします。](aspnet-mvc-4-models-and-data-access/_static/image31.png "Windows Azure portal にログオンします。")</span><span class="sxs-lookup"><span data-stu-id="c03a7-424">![Log on to Windows Azure portal](aspnet-mvc-4-models-and-data-access/_static/image31.png "Log on to Windows Azure portal")</span></span>

    <span data-ttu-id="c03a7-425">*Windows Azure 管理ポータルにログオンします。*</span><span class="sxs-lookup"><span data-stu-id="c03a7-425">*Log on to Windows Azure Management Portal*</span></span>
2. <span data-ttu-id="c03a7-426">コマンドバーの **[新規]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c03a7-426">Click **New** on the command bar.</span></span>

    <span data-ttu-id="c03a7-427">![新しい Web サイトの作成](aspnet-mvc-4-models-and-data-access/_static/image32.png "新しい Web サイトの作成")</span><span class="sxs-lookup"><span data-stu-id="c03a7-427">![Creating a new Web Site](aspnet-mvc-4-models-and-data-access/_static/image32.png "Creating a new Web Site")</span></span>

    <span data-ttu-id="c03a7-428">*新しい Web サイトの作成*</span><span class="sxs-lookup"><span data-stu-id="c03a7-428">*Creating a new Web Site*</span></span>
3. <span data-ttu-id="c03a7-429">[ **Compute** | **Web サイト**] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c03a7-429">Click **Compute** | **Web Site**.</span></span> <span data-ttu-id="c03a7-430">次に、 **[簡易作成]** オプションを選択します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-430">Then select **Quick Create** option.</span></span> <span data-ttu-id="c03a7-431">新しい web サイトの使用可能な URL を指定し、 **[Web サイトの作成]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c03a7-431">Provide an available URL for the new web site and click **Create Web Site**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c03a7-432">Windows Azure の Web サイトは、制御および管理が可能なクラウドで実行されている web アプリケーションのホストです。</span><span class="sxs-lookup"><span data-stu-id="c03a7-432">A Windows Azure Web Site is the host for a web application running in the cloud that you can control and manage.</span></span> <span data-ttu-id="c03a7-433">[簡易作成] オプションを使用すると、完成した web アプリケーションをポータルの外部から Windows Azure の Web サイトにデプロイできます。</span><span class="sxs-lookup"><span data-stu-id="c03a7-433">The Quick Create option allows you to deploy a completed web application to the Windows Azure Web Site from outside the portal.</span></span> <span data-ttu-id="c03a7-434">データベースを設定する手順は含まれていません。</span><span class="sxs-lookup"><span data-stu-id="c03a7-434">It does not include steps for setting up a database.</span></span>

    <span data-ttu-id="c03a7-435">![簡易作成を使用した新しい Web サイトの作成](aspnet-mvc-4-models-and-data-access/_static/image33.png "簡易作成を使用した新しい Web サイトの作成")</span><span class="sxs-lookup"><span data-stu-id="c03a7-435">![Creating a new Web Site using Quick Create](aspnet-mvc-4-models-and-data-access/_static/image33.png "Creating a new Web Site using Quick Create")</span></span>

    <span data-ttu-id="c03a7-436">*簡易作成を使用した新しい Web サイトの作成*</span><span class="sxs-lookup"><span data-stu-id="c03a7-436">*Creating a new Web Site using Quick Create*</span></span>
4. <span data-ttu-id="c03a7-437">新しい**Web サイト**が作成されるまで待ちます。</span><span class="sxs-lookup"><span data-stu-id="c03a7-437">Wait until the new **Web Site** is created.</span></span>
5. <span data-ttu-id="c03a7-438">Web サイトが作成されたら、 **[URL]** 列の下のリンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="c03a7-438">Once the Web Site is created click the link under the **URL** column.</span></span> <span data-ttu-id="c03a7-439">新しい Web サイトが機能していることを確認します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-439">Check that the new Web Site is working.</span></span>

    <span data-ttu-id="c03a7-440">![新しい web サイトを参照しています](aspnet-mvc-4-models-and-data-access/_static/image34.png "新しい web サイトを参照しています")</span><span class="sxs-lookup"><span data-stu-id="c03a7-440">![Browsing to the new web site](aspnet-mvc-4-models-and-data-access/_static/image34.png "Browsing to the new web site")</span></span>

    <span data-ttu-id="c03a7-441">*新しい web サイトを参照しています*</span><span class="sxs-lookup"><span data-stu-id="c03a7-441">*Browsing to the new web site*</span></span>

    <span data-ttu-id="c03a7-442">![実行中の Web サイト](aspnet-mvc-4-models-and-data-access/_static/image35.png "実行中の Web サイト")</span><span class="sxs-lookup"><span data-stu-id="c03a7-442">![Web site running](aspnet-mvc-4-models-and-data-access/_static/image35.png "Web site running")</span></span>

    <span data-ttu-id="c03a7-443">*実行中の Web サイト*</span><span class="sxs-lookup"><span data-stu-id="c03a7-443">*Web site running*</span></span>
6. <span data-ttu-id="c03a7-444">ポータルに戻り、 **[名前]** 列の下にある web サイトの名前をクリックして、管理ページを表示します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-444">Go back to the portal and click the name of the web site under the **Name** column to display the management pages.</span></span>

    <span data-ttu-id="c03a7-445">![Web サイトの管理ページを開く](aspnet-mvc-4-models-and-data-access/_static/image36.png "Web サイトの管理ページを開く")</span><span class="sxs-lookup"><span data-stu-id="c03a7-445">![Opening the web site management pages](aspnet-mvc-4-models-and-data-access/_static/image36.png "Opening the web site management pages")</span></span>

    <span data-ttu-id="c03a7-446">*Web サイトの管理ページを開く*</span><span class="sxs-lookup"><span data-stu-id="c03a7-446">*Opening the Web Site management pages*</span></span>
7. <span data-ttu-id="c03a7-447">**[ダッシュボード]** ページの **[概要] セクションで**、 **[発行プロファイルのダウンロード]** リンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="c03a7-447">In the **Dashboard** page, under the **quick glance** section, click the **Download publish profile** link.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c03a7-448">*発行プロファイル*には、有効になっている各発行方法について、Windows Azure web サイトに web アプリケーションを発行するために必要なすべての情報が含まれています。</span><span class="sxs-lookup"><span data-stu-id="c03a7-448">The *publish profile* contains all of the information required to publish a web application to a Windows Azure website for each enabled publication method.</span></span> <span data-ttu-id="c03a7-449">発行プロファイルには、発行メソッドが有効化される各エンドポイントに接続して認証するために必要な URL、ユーザーの資格情報、およびデータベース文字列が含まれています。</span><span class="sxs-lookup"><span data-stu-id="c03a7-449">The publish profile contains the URLs, user credentials and database strings required to connect to and authenticate against each of the endpoints for which a publication method is enabled.</span></span> <span data-ttu-id="c03a7-450">**Microsoft WebMatrix 2**、 **Microsoft Visual Studio Express for Web**および**Microsoft Visual Studio 2012**では、発行プロファイルを読み取り、Web アプリケーションを Windows Azure websites に発行するためのこれらのプログラムの構成を自動化することがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="c03a7-450">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** and **Microsoft Visual Studio 2012** support reading publish profiles to automate configuration of these programs for publishing web applications to Windows Azure websites.</span></span>

    <span data-ttu-id="c03a7-451">![Web サイト発行プロファイルをダウンロードしています](aspnet-mvc-4-models-and-data-access/_static/image37.png "Web サイト発行プロファイルをダウンロードしています")</span><span class="sxs-lookup"><span data-stu-id="c03a7-451">![Downloading the web site publish profile](aspnet-mvc-4-models-and-data-access/_static/image37.png "Downloading the web site publish profile")</span></span>

    <span data-ttu-id="c03a7-452">*Web サイト発行プロファイルをダウンロードしています*</span><span class="sxs-lookup"><span data-stu-id="c03a7-452">*Downloading the Web Site publish profile*</span></span>
8. <span data-ttu-id="c03a7-453">発行プロファイルファイルを既知の場所にダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="c03a7-453">Download the publish profile file to a known location.</span></span> <span data-ttu-id="c03a7-454">この演習では、このファイルを使用して、Visual Studio から Windows Azure Web サイトに web アプリケーションを発行する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-454">Further in this exercise you will see how to use this file to publish a web application to a Windows Azure Web Sites from Visual Studio.</span></span>

    <span data-ttu-id="c03a7-455">![発行プロファイルファイルを保存しています](aspnet-mvc-4-models-and-data-access/_static/image38.png "発行プロファイルを保存しています")</span><span class="sxs-lookup"><span data-stu-id="c03a7-455">![Saving the publish profile file](aspnet-mvc-4-models-and-data-access/_static/image38.png "Saving the publish profile")</span></span>

    <span data-ttu-id="c03a7-456">*発行プロファイルファイルを保存しています*</span><span class="sxs-lookup"><span data-stu-id="c03a7-456">*Saving the publish profile file*</span></span>

<a id="ApxBTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a><span data-ttu-id="c03a7-457">タスク 2-データベースサーバーの構成</span><span class="sxs-lookup"><span data-stu-id="c03a7-457">Task 2 - Configuring the Database Server</span></span>

<span data-ttu-id="c03a7-458">アプリケーションで SQL Server データベースを使用する場合は、SQL Database サーバーを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c03a7-458">If your application makes use of SQL Server databases you will need to create a SQL Database server.</span></span> <span data-ttu-id="c03a7-459">SQL Server を使用しない単純なアプリケーションを展開する場合は、このタスクを省略できます。</span><span class="sxs-lookup"><span data-stu-id="c03a7-459">If you want to deploy a simple application that does not use SQL Server you might skip this task.</span></span>

1. <span data-ttu-id="c03a7-460">アプリケーションデータベースを格納するには、SQL Database サーバーが必要です。</span><span class="sxs-lookup"><span data-stu-id="c03a7-460">You will need a SQL Database server for storing the application database.</span></span> <span data-ttu-id="c03a7-461">サブスクリプションの**SQL Database サーバーは**、Windows Azure 管理ポータルの**SQL データベース** | サーバー | **サーバーのダッシュボード**で確認できます。</span><span class="sxs-lookup"><span data-stu-id="c03a7-461">You can view the SQL Database servers from your subscription in the Windows Azure Management portal at **Sql Databases** | **Servers** | **Server's Dashboard**.</span></span> <span data-ttu-id="c03a7-462">サーバーを作成していない場合は、コマンドバーの **[追加]** ボタンを使用して作成できます。</span><span class="sxs-lookup"><span data-stu-id="c03a7-462">If you do not have a server created, you can create one using the **Add** button on the command bar.</span></span> <span data-ttu-id="c03a7-463">次のタスクで使用するので、**サーバー名と URL、管理者のログイン名、パスワード**をメモしておきます。</span><span class="sxs-lookup"><span data-stu-id="c03a7-463">Take note of the **server name and URL, administrator login name and password**, as you will use them in the next tasks.</span></span> <span data-ttu-id="c03a7-464">データベースは、後の段階で作成されるため、まだ作成しないでください。</span><span class="sxs-lookup"><span data-stu-id="c03a7-464">Do not create the database yet, as it will be created in a later stage.</span></span>

    <span data-ttu-id="c03a7-465">![SQL Database サーバーダッシュボード](aspnet-mvc-4-models-and-data-access/_static/image39.png "SQL Database サーバーダッシュボード")</span><span class="sxs-lookup"><span data-stu-id="c03a7-465">![SQL Database Server Dashboard](aspnet-mvc-4-models-and-data-access/_static/image39.png "SQL Database Server Dashboard")</span></span>

    <span data-ttu-id="c03a7-466">*SQL Database サーバーダッシュボード*</span><span class="sxs-lookup"><span data-stu-id="c03a7-466">*SQL Database Server Dashboard*</span></span>
2. <span data-ttu-id="c03a7-467">次のタスクでは、Visual Studio からデータベース接続をテストします。そのため、**使用可能な Ip アドレス**の一覧にローカル ip アドレスを含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="c03a7-467">In the next task you will test the database connection from Visual Studio, for that reason you need to include your local IP address in the server's list of **Allowed IP Addresses**.</span></span> <span data-ttu-id="c03a7-468">これを行うには、 **[構成]** をクリックし、 **[現在のクライアント IP アドレス]** の ip アドレスを選択して、 **[開始 Ip アドレス]** と **[終了 ip アドレス]** のテキストボックスに貼り付け、[![の](aspnet-mvc-4-models-and-data-access/_static/image40.png) 追加] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c03a7-468">To do that, click **Configure**, select the IP address from **Current Client IP Address** and paste it on the **Start IP Address** and **End IP Address** text boxes and click the ![add-client-ip-address-ok-button](aspnet-mvc-4-models-and-data-access/_static/image40.png) button.</span></span>

    ![クライアント IP アドレスを追加しています](aspnet-mvc-4-models-and-data-access/_static/image41.png)

    <span data-ttu-id="c03a7-470">*クライアント IP アドレスを追加しています*</span><span class="sxs-lookup"><span data-stu-id="c03a7-470">*Adding Client IP Address*</span></span>
3. <span data-ttu-id="c03a7-471">[許可された IP アドレス] の一覧に**クライアントの Ip アドレス**が追加されたら、 **[保存]** をクリックして変更を確認します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-471">Once the **Client IP Address** is added to the allowed IP addresses list, click on **Save** to confirm the changes.</span></span>

    ![変更の確認](aspnet-mvc-4-models-and-data-access/_static/image42.png)

    <span data-ttu-id="c03a7-473">*変更の確認*</span><span class="sxs-lookup"><span data-stu-id="c03a7-473">*Confirm Changes*</span></span>

<a id="ApxBTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="c03a7-474">タスク 3-Web 配置を使用した ASP.NET MVC 4 アプリケーションの発行</span><span class="sxs-lookup"><span data-stu-id="c03a7-474">Task 3 - Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

1. <span data-ttu-id="c03a7-475">ASP.NET MVC 4 ソリューションに戻ります。</span><span class="sxs-lookup"><span data-stu-id="c03a7-475">Go back to the ASP.NET MVC 4 solution.</span></span> <span data-ttu-id="c03a7-476">**ソリューションエクスプローラー**で、web サイトプロジェクトを右クリックし、 **[発行]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-476">In the **Solution Explorer**, right-click the web site project and select **Publish**.</span></span>

    <span data-ttu-id="c03a7-477">![アプリケーションの発行](aspnet-mvc-4-models-and-data-access/_static/image43.png "アプリケーションの発行")</span><span class="sxs-lookup"><span data-stu-id="c03a7-477">![Publishing the Application](aspnet-mvc-4-models-and-data-access/_static/image43.png "Publishing the Application")</span></span>

    <span data-ttu-id="c03a7-478">*Web サイトの公開*</span><span class="sxs-lookup"><span data-stu-id="c03a7-478">*Publishing the web site*</span></span>
2. <span data-ttu-id="c03a7-479">最初のタスクで保存した発行プロファイルをインポートします。</span><span class="sxs-lookup"><span data-stu-id="c03a7-479">Import the publish profile you saved in the first task.</span></span>

    <span data-ttu-id="c03a7-480">![発行プロファイルをインポートしています](aspnet-mvc-4-models-and-data-access/_static/image44.png "発行プロファイルをインポートしています")</span><span class="sxs-lookup"><span data-stu-id="c03a7-480">![Importing the publish profile](aspnet-mvc-4-models-and-data-access/_static/image44.png "Importing the publish profile")</span></span>

    <span data-ttu-id="c03a7-481">*発行プロファイルをインポートしています*</span><span class="sxs-lookup"><span data-stu-id="c03a7-481">*Importing publish profile*</span></span>
3. <span data-ttu-id="c03a7-482">**[接続の検証]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c03a7-482">Click **Validate Connection**.</span></span> <span data-ttu-id="c03a7-483">検証が完了したら、 **[次へ]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c03a7-483">Once Validation is complete click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c03a7-484">検証が完了すると、[接続の検証] ボタンの横に緑色のチェックマークが表示されます。</span><span class="sxs-lookup"><span data-stu-id="c03a7-484">Validation is complete once you see a green checkmark appear next to the Validate Connection button.</span></span>

    <span data-ttu-id="c03a7-485">![接続の検証](aspnet-mvc-4-models-and-data-access/_static/image45.png "接続の検証")</span><span class="sxs-lookup"><span data-stu-id="c03a7-485">![Validating connection](aspnet-mvc-4-models-and-data-access/_static/image45.png "Validating connection")</span></span>

    <span data-ttu-id="c03a7-486">*接続の検証*</span><span class="sxs-lookup"><span data-stu-id="c03a7-486">*Validating connection*</span></span>
4. <span data-ttu-id="c03a7-487">**[設定]** ページの **[データベース]** セクションで、データベース接続のテキストボックスの横にあるボタン ( **defaultconnection**など) をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c03a7-487">In the **Settings** page, under the **Databases** section, click the button next to your database connection's textbox (i.e. **DefaultConnection**).</span></span>

    <span data-ttu-id="c03a7-488">![Web deploy の構成](aspnet-mvc-4-models-and-data-access/_static/image46.png "Web deploy の構成")</span><span class="sxs-lookup"><span data-stu-id="c03a7-488">![Web deploy configuration](aspnet-mvc-4-models-and-data-access/_static/image46.png "Web deploy configuration")</span></span>

    <span data-ttu-id="c03a7-489">*Web deploy の構成*</span><span class="sxs-lookup"><span data-stu-id="c03a7-489">*Web deploy configuration*</span></span>
5. <span data-ttu-id="c03a7-490">次のようにデータベース接続を構成します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-490">Configure the database connection as follows:</span></span>

   - <span data-ttu-id="c03a7-491">**サーバー名**には、 *tcp:* プレフィックスを使用して SQL Database サーバーの URL を入力します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-491">In the **Server name** type your SQL Database server URL using the *tcp:* prefix.</span></span>
   - <span data-ttu-id="c03a7-492">**User name (ユーザー名**) に、サーバー管理者のログイン名を入力します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-492">In **User name** type your server administrator login name.</span></span>
   - <span data-ttu-id="c03a7-493">**パスワード**で、サーバー管理者のログインパスワードを入力します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-493">In **Password** type your server administrator login password.</span></span>
   - <span data-ttu-id="c03a7-494">新しいデータベース名を入力します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-494">Type a new database name.</span></span>

     <span data-ttu-id="c03a7-495">![変換先の接続文字列を構成しています](aspnet-mvc-4-models-and-data-access/_static/image47.png "変換先の接続文字列を構成しています")</span><span class="sxs-lookup"><span data-stu-id="c03a7-495">![Configuring destination connection string](aspnet-mvc-4-models-and-data-access/_static/image47.png "Configuring destination connection string")</span></span>

     <span data-ttu-id="c03a7-496">*変換先の接続文字列を構成しています*</span><span class="sxs-lookup"><span data-stu-id="c03a7-496">*Configuring destination connection string*</span></span>
6. <span data-ttu-id="c03a7-497">次に、 **[OK]** をクリックします</span><span class="sxs-lookup"><span data-stu-id="c03a7-497">Then click **OK**.</span></span> <span data-ttu-id="c03a7-498">データベースの作成を求めるメッセージが表示されたら、[**はい]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c03a7-498">When prompted to create the database click **Yes**.</span></span>

    <span data-ttu-id="c03a7-499">![データベースの作成](aspnet-mvc-4-models-and-data-access/_static/image48.png "データベース文字列の作成")</span><span class="sxs-lookup"><span data-stu-id="c03a7-499">![Creating the database](aspnet-mvc-4-models-and-data-access/_static/image48.png "Creating the database string")</span></span>

    <span data-ttu-id="c03a7-500">*データベースの作成*</span><span class="sxs-lookup"><span data-stu-id="c03a7-500">*Creating the database*</span></span>
7. <span data-ttu-id="c03a7-501">Windows Azure の SQL Database に接続するために使用する接続文字列は、[既定の接続] ボックスに表示されます。</span><span class="sxs-lookup"><span data-stu-id="c03a7-501">The connection string you will use to connect to SQL Database in Windows Azure is shown within Default Connection textbox.</span></span> <span data-ttu-id="c03a7-502">続けて、 **[次へ]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c03a7-502">Then click **Next**.</span></span>

    <span data-ttu-id="c03a7-503">![SQL Database を指す接続文字列](aspnet-mvc-4-models-and-data-access/_static/image49.png "SQL Database を指す接続文字列")</span><span class="sxs-lookup"><span data-stu-id="c03a7-503">![Connection string pointing to SQL Database](aspnet-mvc-4-models-and-data-access/_static/image49.png "Connection string pointing to SQL Database")</span></span>

    <span data-ttu-id="c03a7-504">*SQL Database を指す接続文字列*</span><span class="sxs-lookup"><span data-stu-id="c03a7-504">*Connection string pointing to SQL Database*</span></span>
8. <span data-ttu-id="c03a7-505">**[プレビュー]** ページで、 **[発行]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c03a7-505">In the **Preview** page, click **Publish**.</span></span>

    <span data-ttu-id="c03a7-506">![Web アプリケーションの発行](aspnet-mvc-4-models-and-data-access/_static/image50.png "Web アプリケーションの発行")</span><span class="sxs-lookup"><span data-stu-id="c03a7-506">![Publishing the web application](aspnet-mvc-4-models-and-data-access/_static/image50.png "Publishing the web application")</span></span>

    <span data-ttu-id="c03a7-507">*Web アプリケーションの発行*</span><span class="sxs-lookup"><span data-stu-id="c03a7-507">*Publishing the web application*</span></span>
9. <span data-ttu-id="c03a7-508">発行プロセスが完了すると、既定のブラウザーによって公開された web サイトが開きます。</span><span class="sxs-lookup"><span data-stu-id="c03a7-508">Once the publishing process finishes, your default browser will open the published web site.</span></span>

<a id="AppendixC"></a>

<a id="Appendix_C_Using_Code_Snippets"></a>
## <a name="appendix-c-using-code-snippets"></a><span data-ttu-id="c03a7-509">付録 C: コードスニペットの使用</span><span class="sxs-lookup"><span data-stu-id="c03a7-509">Appendix C: Using Code Snippets</span></span>

<span data-ttu-id="c03a7-510">コードスニペットを使用すると、必要なすべてのコードをすぐに利用できます。</span><span class="sxs-lookup"><span data-stu-id="c03a7-510">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="c03a7-511">次の図に示すように、ラボドキュメントには、使用できるタイミングがわかります。</span><span class="sxs-lookup"><span data-stu-id="c03a7-511">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="c03a7-512">![Visual Studio のコードスニペットを使用してプロジェクトにコードを挿入する](aspnet-mvc-4-models-and-data-access/_static/image51.png "Visual Studio のコードスニペットを使用してプロジェクトにコードを挿入する")</span><span class="sxs-lookup"><span data-stu-id="c03a7-512">![Using Visual Studio code snippets to insert code into your project](aspnet-mvc-4-models-and-data-access/_static/image51.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="c03a7-513">*Visual Studio のコードスニペットを使用してプロジェクトにコードを挿入する*</span><span class="sxs-lookup"><span data-stu-id="c03a7-513">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="c03a7-514">***キーボードを使用してコードスニペットを追加C#するには (のみ)***</span><span class="sxs-lookup"><span data-stu-id="c03a7-514">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="c03a7-515">コードを挿入する場所にカーソルを置きます。</span><span class="sxs-lookup"><span data-stu-id="c03a7-515">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="c03a7-516">(スペースまたはハイフンを含まない) スニペット名の入力を開始します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-516">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="c03a7-517">IntelliSense によって、一致するスニペットの名前が表示されます。</span><span class="sxs-lookup"><span data-stu-id="c03a7-517">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="c03a7-518">正しいスニペットを選択します (または、スニペットの名前全体が選択されるまで入力し続けます)。</span><span class="sxs-lookup"><span data-stu-id="c03a7-518">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="c03a7-519">Tab キーを2回押すと、スニペットがカーソル位置に挿入されます。</span><span class="sxs-lookup"><span data-stu-id="c03a7-519">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="c03a7-520">![スニペット名の入力を開始します](aspnet-mvc-4-models-and-data-access/_static/image52.png "スニペット名の入力を開始します")</span><span class="sxs-lookup"><span data-stu-id="c03a7-520">![Start typing the snippet name](aspnet-mvc-4-models-and-data-access/_static/image52.png "Start typing the snippet name")</span></span>

<span data-ttu-id="c03a7-521">*スニペット名の入力を開始します*</span><span class="sxs-lookup"><span data-stu-id="c03a7-521">*Start typing the snippet name*</span></span>

<span data-ttu-id="c03a7-522">![Tab キーを押して、強調表示されているスニペットを選択します](aspnet-mvc-4-models-and-data-access/_static/image53.png "Tab キーを押して、強調表示されているスニペットを選択します")</span><span class="sxs-lookup"><span data-stu-id="c03a7-522">![Press Tab to select the highlighted snippet](aspnet-mvc-4-models-and-data-access/_static/image53.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="c03a7-523">*Tab キーを押して、強調表示されているスニペットを選択します*</span><span class="sxs-lookup"><span data-stu-id="c03a7-523">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="c03a7-524">![もう一度 Tab キーを押すと、スニペットが展開されます。](aspnet-mvc-4-models-and-data-access/_static/image54.png "もう一度 Tab キーを押すと、スニペットが展開されます。")</span><span class="sxs-lookup"><span data-stu-id="c03a7-524">![Press Tab again and the snippet will expand](aspnet-mvc-4-models-and-data-access/_static/image54.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="c03a7-525">*もう一度 Tab キーを押すと、スニペットが展開されます。*</span><span class="sxs-lookup"><span data-stu-id="c03a7-525">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="c03a7-526">***マウスC#(、Visual Basic および XML) を使用してコードスニペットを追加するに***は1.</span><span class="sxs-lookup"><span data-stu-id="c03a7-526">***To add a code snippet using the mouse (C#, Visual Basic and XML)*** 1.</span></span> <span data-ttu-id="c03a7-527">コードスニペットを挿入する場所を右クリックします。</span><span class="sxs-lookup"><span data-stu-id="c03a7-527">Right-click where you want to insert the code snippet.</span></span>

1. <span data-ttu-id="c03a7-528">**[スニペットの挿入]** 、 **[マイコードスニペット**] の順に選択します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-528">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
2. <span data-ttu-id="c03a7-529">一覧から該当するスニペットをクリックして選択します。</span><span class="sxs-lookup"><span data-stu-id="c03a7-529">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="c03a7-530">![コードスニペットを挿入する場所を右クリックし、[スニペットの挿入] を選択します。](aspnet-mvc-4-models-and-data-access/_static/image55.png "コードスニペットを挿入する場所を右クリックし、[スニペットの挿入] を選択します。")</span><span class="sxs-lookup"><span data-stu-id="c03a7-530">![Right-click where you want to insert the code snippet and select Insert Snippet](aspnet-mvc-4-models-and-data-access/_static/image55.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="c03a7-531">*コードスニペットを挿入する場所を右クリックし、[スニペットの挿入] を選択します。*</span><span class="sxs-lookup"><span data-stu-id="c03a7-531">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="c03a7-532">![一覧から関連するスニペットをクリックして選択します。](aspnet-mvc-4-models-and-data-access/_static/image56.png "一覧から関連するスニペットをクリックして選択します。")</span><span class="sxs-lookup"><span data-stu-id="c03a7-532">![Pick the relevant snippet from the list, by clicking on it](aspnet-mvc-4-models-and-data-access/_static/image56.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="c03a7-533">*一覧から関連するスニペットをクリックして選択します。*</span><span class="sxs-lookup"><span data-stu-id="c03a7-533">*Pick the relevant snippet from the list, by clicking on it*</span></span>
