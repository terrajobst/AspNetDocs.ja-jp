---
uid: web-forms/overview/getting-started/code-editing-in-web-forms-pages
title: コード編集 ASP.NET の Web フォームを Visual Studio 2013 |Microsoft Docs
author: Erikre
description: ''
ms.author: riande
ms.date: 03/03/2014
ms.assetid: 5344b74e-b888-479a-92bc-601a33bd61a2
msc.legacyurl: /web-forms/overview/getting-started/code-editing-in-web-forms-pages
msc.type: authoredcontent
ms.openlocfilehash: 3473ad476fbbebc58e12586334b4600f57cf17ed
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78513640"
---
# <a name="code-editing-aspnet-web-forms-in-visual-studio-2013"></a><span data-ttu-id="e5377-102">Visual Studio 2013 で ASP.NET Web フォームのコードを編集する</span><span class="sxs-lookup"><span data-stu-id="e5377-102">Code Editing ASP.NET Web Forms in Visual Studio 2013</span></span>

<span data-ttu-id="e5377-103">[Erik Reitan](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="e5377-103">by [Erik Reitan](https://github.com/Erikre)</span></span>

<span data-ttu-id="e5377-104">多くの ASP.NET Web フォーム ページでは、Visual Basic、C#、または別の言語でコードを記述します。</span><span class="sxs-lookup"><span data-stu-id="e5377-104">In many ASP.NET Web Form pages, you write code in Visual Basic, C#, or another language.</span></span> <span data-ttu-id="e5377-105">Visual Studio のコードエディターを使用すると、エラーを回避しながらコードをすばやく記述できます。</span><span class="sxs-lookup"><span data-stu-id="e5377-105">The code editor in Visual Studio can help you write code quickly while helping you avoid errors.</span></span> <span data-ttu-id="e5377-106">また、エディターは、再利用可能なコードを作成して、必要な作業量を減らすための手段を提供します。</span><span class="sxs-lookup"><span data-stu-id="e5377-106">In addition, the editor provides ways for you to create reusable code to help reduce the amount of work you need to do.</span></span>

<span data-ttu-id="e5377-107">このチュートリアルでは、Visual Studio コードエディターのさまざまな機能について説明します。</span><span class="sxs-lookup"><span data-stu-id="e5377-107">This walkthrough illustrates various features of the Visual Studio code editor.</span></span>

<span data-ttu-id="e5377-108">このチュートリアルでは、次の作業を行う方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="e5377-108">During this walkthrough, you will learn how to:</span></span>

- <span data-ttu-id="e5377-109">インラインのコードエラーを修正します。</span><span class="sxs-lookup"><span data-stu-id="e5377-109">Correct inline coding errors.</span></span>
- <span data-ttu-id="e5377-110">コードをリファクターして名前を変更します。</span><span class="sxs-lookup"><span data-stu-id="e5377-110">Refactor and rename code.</span></span>
- <span data-ttu-id="e5377-111">変数とオブジェクトの名前を変更します。</span><span class="sxs-lookup"><span data-stu-id="e5377-111">Rename variables and objects.</span></span>
- <span data-ttu-id="e5377-112">コードスニペットを挿入します。</span><span class="sxs-lookup"><span data-stu-id="e5377-112">Insert code snippets.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e5377-113">前提条件</span><span class="sxs-lookup"><span data-stu-id="e5377-113">Prerequisites</span></span>

<span data-ttu-id="e5377-114">このチュートリアルを完了するには、以下が必要です。</span><span class="sxs-lookup"><span data-stu-id="e5377-114">In order to complete this walkthrough, you will need:</span></span>

- <span data-ttu-id="e5377-115">[Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/downloads#vs)または[Web 用 Microsoft Visual Studio Express 2013](https://www.microsoft.com/visualstudio/11/downloads#express-web)。</span><span class="sxs-lookup"><span data-stu-id="e5377-115">[Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/downloads#vs) or [Microsoft Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web).</span></span> <span data-ttu-id="e5377-116">.NET Framework は自動的にインストールされます。</span><span class="sxs-lookup"><span data-stu-id="e5377-116">The .NET Framework is installed automatically.</span></span> 

    > [!NOTE] 
    > 
    > <span data-ttu-id="e5377-117">このチュートリアルシリーズでは、多くの場合、Web 用の Microsoft Visual Studio 2013 と Microsoft Visual Studio Express 2013 を Visual Studio と呼びます。</span><span class="sxs-lookup"><span data-stu-id="e5377-117">Microsoft Visual Studio 2013 and Microsoft Visual Studio Express 2013 for Web will often be referred to as Visual Studio throughout this tutorial series.</span></span>  
    >   
    > <span data-ttu-id="e5377-118">Visual Studio を使用している場合、このチュートリアルでは、Visual Studio を初めて起動したときに設定の**Web 開発**コレクションが選択されていることを前提としています。</span><span class="sxs-lookup"><span data-stu-id="e5377-118">If you are using Visual Studio, this walkthrough assumes that you selected the **Web Development** collection of settings the first time that you started Visual Studio.</span></span> <span data-ttu-id="e5377-119">詳細については、「[方法: Web 開発環境の設定を選択する](https://msdn.microsoft.com/library/ff521558.aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="e5377-119">For more information, see [How to: Select Web Development Environment Settings](https://msdn.microsoft.com/library/ff521558.aspx).</span></span>

## <a name="creating-a-web-application-project-and-a-page"></a><span data-ttu-id="e5377-120">Web アプリケーションプロジェクトとページの作成</span><span class="sxs-lookup"><span data-stu-id="e5377-120">Creating a Web application project and a Page</span></span>

<a id="sectionToggle0"></a>

<span data-ttu-id="e5377-121">チュートリアルのこの部分では、Web アプリケーションプロジェクトを作成し、そこに新しいページを追加します。</span><span class="sxs-lookup"><span data-stu-id="e5377-121">In this part of the walkthrough, you will create a Web application project and add a new page to it.</span></span>

### <a name="to-create-a-web-application-project"></a><span data-ttu-id="e5377-122">Web アプリケーションプロジェクトを作成するには</span><span class="sxs-lookup"><span data-stu-id="e5377-122">To create a Web application project</span></span>

1. <span data-ttu-id="e5377-123">Microsoft Visual Studio を開きます。</span><span class="sxs-lookup"><span data-stu-id="e5377-123">Open Microsoft Visual Studio.</span></span>
2. <span data-ttu-id="e5377-124">**[ファイル]** メニューの **[新しいプロジェクト]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="e5377-124">On the **File** menu, select **New Project**.</span></span>  
    <span data-ttu-id="e5377-125">![ファイル メニュー](code-editing-in-web-forms-pages/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="e5377-125">![File Menu](code-editing-in-web-forms-pages/_static/image1.png)</span></span>

    <span data-ttu-id="e5377-126">**[新しいプロジェクト]** ダイアログ ボックスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="e5377-126">The **New Project** dialog box appears.</span></span>
3. <span data-ttu-id="e5377-127">左側にある [**テンプレート** -&gt; **Visual C#**  -&gt; **Web**テンプレート] グループを選択します。</span><span class="sxs-lookup"><span data-stu-id="e5377-127">Select the **Templates** -&gt; **Visual C#** -&gt; **Web** templates group on the left.</span></span>
4. <span data-ttu-id="e5377-128">中央の列で **[ASP.NET Web アプリケーション]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="e5377-128">Choose the **ASP.NET Web Application** template in the center column.</span></span>
5. <span data-ttu-id="e5377-129">プロジェクトに***Basicwebapp***という名前を指定し、 **[OK]** ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="e5377-129">Name your project ***BasicWebApp*** and click the **OK** button.</span></span>   
<span data-ttu-id="e5377-130">![[新しいプロジェクト] ダイアログ ボックス](code-editing-in-web-forms-pages/_static/image2.png)</span><span class="sxs-lookup"><span data-stu-id="e5377-130">![New Project dialog box](code-editing-in-web-forms-pages/_static/image2.png)</span></span>
6. <span data-ttu-id="e5377-131">次に、 **[Web フォーム]** テンプレートを選択し、 **[OK]** ボタンをクリックしてプロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="e5377-131">Next, select the **Web Forms** template and click the **OK** button to create the project.</span></span>  
<span data-ttu-id="e5377-132">![[新しい ASP.NET プロジェクト] ダイアログ ボックス](code-editing-in-web-forms-pages/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="e5377-132">![New ASP.NET Project dialog box](code-editing-in-web-forms-pages/_static/image3.png)</span></span>  

    <span data-ttu-id="e5377-133">Visual Studio によって、Web フォームテンプレートに基づく事前構築済みの機能を含む新しいプロジェクトが作成されます。</span><span class="sxs-lookup"><span data-stu-id="e5377-133">Visual Studio creates a new project that includes prebuilt functionality based on the Web Forms template.</span></span>

## <a name="creating-a-new-aspnet-web-forms-page"></a><span data-ttu-id="e5377-134">新しい ASP.NET Web フォームページの作成</span><span class="sxs-lookup"><span data-stu-id="e5377-134">Creating a new ASP.NET Web Forms Page</span></span>

<span data-ttu-id="e5377-135">**ASP.NET Web アプリケーション**プロジェクトテンプレートを使用して新しい Web フォームアプリケーションを作成すると、Visual Studio によって、 *default.aspx*という名前の ASP.NET ページ (Web フォームページ) とその他のいくつかのファイルとフォルダーが追加されます。</span><span class="sxs-lookup"><span data-stu-id="e5377-135">When you create a new Web Forms application using the **ASP.NET Web Application** project template, Visual Studio adds an ASP.NET page (Web Forms page) named *Default.aspx*, as well as several other files and folders.</span></span> <span data-ttu-id="e5377-136">*Default.aspx*ページは、Web アプリケーションのホームページとして使用できます。</span><span class="sxs-lookup"><span data-stu-id="e5377-136">You can use the *Default.aspx* page as the home page for your Web application.</span></span> <span data-ttu-id="e5377-137">ただし、このチュートリアルでは、新しいページを作成して操作します。</span><span class="sxs-lookup"><span data-stu-id="e5377-137">However, for this walkthrough, you will create and work with a new page.</span></span>

### <a name="to-add-a-page-to-the-web-application"></a><span data-ttu-id="e5377-138">Web アプリケーションにページを追加するには</span><span class="sxs-lookup"><span data-stu-id="e5377-138">To add a page to the Web application</span></span>

1. <span data-ttu-id="e5377-139">**ソリューションエクスプローラー**で、Web アプリケーション名 (このチュートリアルではアプリケーション名は**basicwebsite**) を右クリックし、[ -の**追加**] をクリックして &gt;**新しい項目**を追加します。</span><span class="sxs-lookup"><span data-stu-id="e5377-139">In **Solution Explorer**, right-click the Web application name (in this tutorial the application name is **BasicWebSite**), and then click **Add** -&gt; **New Item**.</span></span>   
<span data-ttu-id="e5377-140">**[新しい項目の追加]** ダイアログ ボックスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="e5377-140">The **Add New Item** dialog box is displayed.</span></span>
2. <span data-ttu-id="e5377-141">左側の **[ C# Visual** -&gt; **Web**テンプレート] グループを選択します。</span><span class="sxs-lookup"><span data-stu-id="e5377-141">Select the **Visual C#** -&gt; **Web** templates group on the left.</span></span> <span data-ttu-id="e5377-142">次に、中央の一覧から **[Web フォーム]** を選択し、 *firstwebpage ページ*にという名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="e5377-142">Then, select **Web Form** from the middle list and name it *FirstWebPage.aspx*.</span></span>   
    <span data-ttu-id="e5377-143">![[新しい項目の追加] ダイアログ ボックス](code-editing-in-web-forms-pages/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="e5377-143">![Add New Item dialog box](code-editing-in-web-forms-pages/_static/image4.png)</span></span>
3. <span data-ttu-id="e5377-144">**[追加]** をクリックして、Web フォームページをプロジェクトに追加します。</span><span class="sxs-lookup"><span data-stu-id="e5377-144">Click **Add** to add the Web Forms page to your project.</span></span>  
 <span data-ttu-id="e5377-145">新しいページが作成されて開きます。</span><span class="sxs-lookup"><span data-stu-id="e5377-145">Visual Studio creates the new page and opens it.</span></span>
4. <span data-ttu-id="e5377-146">次に、この新しいページを既定のスタートアップページとして設定します。</span><span class="sxs-lookup"><span data-stu-id="e5377-146">Next, set this new page as the default startup page.</span></span> <span data-ttu-id="e5377-147">**ソリューションエクスプローラー**で、 *firstwebpage*という名前の新しいページを右クリックし、 **[スタートページとして設定]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="e5377-147">In **Solution Explorer**, right-click the new page named *FirstWebPage.aspx* and select **Set As Start Page**.</span></span> <span data-ttu-id="e5377-148">次回このアプリケーションを実行して進行状況をテストすると、ブラウザーにこの新しいページが自動的に表示されます。</span><span class="sxs-lookup"><span data-stu-id="e5377-148">The next time you run this application to test our progress, you will automatically see this new page in the browser.</span></span>

## <a name="correcting-inline-coding-errors"></a><span data-ttu-id="e5377-149">インラインコードエラーの修正</span><span class="sxs-lookup"><span data-stu-id="e5377-149">Correcting Inline Coding Errors</span></span>

<span data-ttu-id="e5377-150">Visual Studio のコードエディターを使用すると、コードを記述するときにエラーを回避できます。また、エラーが発生した場合は、コードエディターを使用してエラーを修正することができます。</span><span class="sxs-lookup"><span data-stu-id="e5377-150">The code editor in Visual Studio helps you to avoid errors as you write code, and if you have made an error, the code editor helps you to correct the error.</span></span> <span data-ttu-id="e5377-151">チュートリアルのこの部分では、エディターのエラー修正機能を示すコード行を記述します。</span><span class="sxs-lookup"><span data-stu-id="e5377-151">In this part of the walkthrough, you will write a line of code that illustrate the error correction features in the editor.</span></span>

### <a name="to-correct-simple-coding-errors-in-visual-studio"></a><span data-ttu-id="e5377-152">Visual Studio で単純なコードエラーを修正するには</span><span class="sxs-lookup"><span data-stu-id="e5377-152">To correct simple coding errors in Visual Studio</span></span>

1. <span data-ttu-id="e5377-153">**デザイン**ビューで、空白のページをダブルクリックして、ページの**読み込み**イベントのハンドラーを作成します。</span><span class="sxs-lookup"><span data-stu-id="e5377-153">In **Design** view, double-click the blank page to create a handler for the **Load** event for the page.</span></span>   
   <span data-ttu-id="e5377-154">イベントハンドラーを使用するのは、コードを記述する場所としてのみです。</span><span class="sxs-lookup"><span data-stu-id="e5377-154">You are using the event handler only as a place to write some code.</span></span>
2. <span data-ttu-id="e5377-155">ハンドラー内で、エラーを含む次の行を入力し、 **enter キーを押します。**</span><span class="sxs-lookup"><span data-stu-id="e5377-155">Inside the handler, type the following line that contains an error and press **ENTER**:</span></span>

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample1.cs)]

   <span data-ttu-id="e5377-156">**Enter キーを**押すと、コードエディターによって、問題のあるコード領域の下に緑と赤の下線が表示されます (通常は、波線 &quot;&quot; 線になります)。</span><span class="sxs-lookup"><span data-stu-id="e5377-156">When you press **ENTER**, the code editor places green and red underlines (commonly call &quot;squiggly&quot; lines) under areas of the code that have issues.</span></span> <span data-ttu-id="e5377-157">緑の下線は警告を示します。</span><span class="sxs-lookup"><span data-stu-id="e5377-157">A green underline indicates a warning.</span></span> <span data-ttu-id="e5377-158">赤い下線は、修正する必要があるエラーを示しています。</span><span class="sxs-lookup"><span data-stu-id="e5377-158">A red underline indicates an error that you must fix.</span></span> 

    <span data-ttu-id="e5377-159">`myStr` 上にマウスポインターを置くと、警告に関する情報を示すツールヒントが表示されます。</span><span class="sxs-lookup"><span data-stu-id="e5377-159">Hold the mouse pointer over `myStr` to see a tooltip that tells you about the warning.</span></span> <span data-ttu-id="e5377-160">また、赤い枠線の上にマウスポインターを置くと、エラーメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="e5377-160">Also, hold your mouse pointer over the red underline to see the error message.</span></span>

    <span data-ttu-id="e5377-161">次の図は、下線付きのコードを示しています。</span><span class="sxs-lookup"><span data-stu-id="e5377-161">The following image shows the code with the underlines.</span></span>

    <span data-ttu-id="e5377-162">![デザインビューのようこそテキスト](code-editing-in-web-forms-pages/_static/image5.png "デザイン ビューの開始テキスト")</span><span class="sxs-lookup"><span data-stu-id="e5377-162">![Welcome text in Design view](code-editing-in-web-forms-pages/_static/image5.png "Welcome text in Design view")</span></span>  
   <span data-ttu-id="e5377-163">このエラーは、行の末尾にセミコロン `;` を追加することで修正する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e5377-163">The error must be fixed by adding a semicolon `;` to the end of the line.</span></span> <span data-ttu-id="e5377-164">警告は、`myStr` 変数をまだ使用していないことを通知するだけです。</span><span class="sxs-lookup"><span data-stu-id="e5377-164">The warning simply notifies you that you haven't used the `myStr` variable yet.</span></span>  

    > [!NOTE] 
    > 
    > <span data-ttu-id="e5377-165">Visual Studio で現在のコードの書式設定を表示するには、[**ツール** -&gt;**オプション]** を選択し &gt;**フォントと色**を -します。</span><span class="sxs-lookup"><span data-stu-id="e5377-165">You view your current code formatting settings in Visual Studio by selecting **Tools** -&gt; **Options** -&gt; **Fonts and Colors**.</span></span>

## <a name="refactoring-and-renaming"></a><span data-ttu-id="e5377-166">リファクタリングと名前の変更</span><span class="sxs-lookup"><span data-stu-id="e5377-166">Refactoring and Renaming</span></span>

<span data-ttu-id="e5377-167">リファクタリングとは、コードを再構築することによって、機能を維持しながら理解を深め、保守を容易にする、ソフトウェアの手法です。</span><span class="sxs-lookup"><span data-stu-id="e5377-167">Refactoring is a software methodology that involves restructuring your code to make it easier to understand and to maintain, while preserving its functionality.</span></span> <span data-ttu-id="e5377-168">単純な例として、イベントハンドラーにコードを記述してデータベースからデータを取得することがあります。</span><span class="sxs-lookup"><span data-stu-id="e5377-168">A simple example might be that you write code in an event handler to get data from a database.</span></span> <span data-ttu-id="e5377-169">ページを開発する際には、複数の異なるハンドラーからデータにアクセスする必要があることがわかります。</span><span class="sxs-lookup"><span data-stu-id="e5377-169">As you develop your page, you discover that you need to access the data from several different handlers.</span></span> <span data-ttu-id="e5377-170">したがって、ページにデータアクセスメソッドを作成し、ハンドラーにメソッドの呼び出しを挿入することによって、ページのコードをリファクターします。</span><span class="sxs-lookup"><span data-stu-id="e5377-170">Therefore, you refactor the page's code by creating a data-access method in the page and inserting calls to the method in the handlers.</span></span>

<span data-ttu-id="e5377-171">コードエディターには、さまざまなリファクタリングタスクの実行に役立つツールが用意されています。</span><span class="sxs-lookup"><span data-stu-id="e5377-171">The code editor includes tools to help you perform various refactoring tasks.</span></span> <span data-ttu-id="e5377-172">このチュートリアルでは、変数の名前の変更とメソッドの抽出という2つのリファクタリング手法を使用します。</span><span class="sxs-lookup"><span data-stu-id="e5377-172">In this walkthrough, you will work with two refactoring techniques: renaming variables and extracting methods.</span></span> <span data-ttu-id="e5377-173">その他のリファクタリングオプションとしては、フィールドのカプセル化、メソッドパラメーターへのローカル変数の昇格、およびメソッドパラメーターの管理などがあります。</span><span class="sxs-lookup"><span data-stu-id="e5377-173">Other refactoring options include encapsulating fields, promoting local variables to method parameters, and managing method parameters.</span></span> <span data-ttu-id="e5377-174">これらのリファクタリングオプションを使用できるかどうかは、コード内の場所によって異なります。</span><span class="sxs-lookup"><span data-stu-id="e5377-174">The availability of these refactoring options depends on the location in the code.</span></span>

### <a name="refactoring-code"></a><span data-ttu-id="e5377-175">リファクタリング (コードを)</span><span class="sxs-lookup"><span data-stu-id="e5377-175">Refactoring Code</span></span>

<span data-ttu-id="e5377-176">一般的なリファクタリングシナリオでは、メソッドなど、別のメンバー内にあるコードからメソッドを作成 (抽出) します。</span><span class="sxs-lookup"><span data-stu-id="e5377-176">A common refactoring scenario is to create (extract) a method from code that is inside another member, such as a method.</span></span> <span data-ttu-id="e5377-177">これにより、元のメンバーのサイズが縮小され、抽出されたコードが再利用可能になります。</span><span class="sxs-lookup"><span data-stu-id="e5377-177">This reduces the size of the original member and makes the extracted code reusable.</span></span>

<span data-ttu-id="e5377-178">チュートリアルのこの部分では、単純なコードを記述し、そこからメソッドを抽出します。</span><span class="sxs-lookup"><span data-stu-id="e5377-178">In this part of the walkthrough, you will write some simple code, and then extract a method from it.</span></span> <span data-ttu-id="e5377-179">リファクタリングはサポートされている C# の場合は、ため、プログラミング言語として C# を使用するページを作成します。</span><span class="sxs-lookup"><span data-stu-id="e5377-179">Refactoring is supported for C#, so you will create a page that uses C# as its programming language.</span></span>

### <a name="to-extract-a-method-in-a-c-page"></a><span data-ttu-id="e5377-180">C#ページ内のメソッドを抽出するには</span><span class="sxs-lookup"><span data-stu-id="e5377-180">To extract a method in a C# page</span></span>

1. <span data-ttu-id="e5377-181">**デザイン**ビューに切り替えます。</span><span class="sxs-lookup"><span data-stu-id="e5377-181">Switch to **Design** view.</span></span>
2. <span data-ttu-id="e5377-182">**ツールボックス**の **[標準]** タブで、[ボタン](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)コントロールをページにドラッグします。</span><span class="sxs-lookup"><span data-stu-id="e5377-182">In the **Toolbox**, from the **Standard** tab, drag a [Button](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) control onto the page.</span></span>
3. <span data-ttu-id="e5377-183">**ボタン**コントロールをダブルクリックして、[クリック](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx)イベントのハンドラーを作成し、次の強調表示されたコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="e5377-183">Double-click the **Button** control to create a handler for its [Click](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx) event, and then add the following highlighted code:</span></span>

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample2.cs?highlight=3-16)]

   <span data-ttu-id="e5377-184">このコードは、 **arraylist**オブジェクトを作成し、ループを使用して値を読み込み、別のループを使用して**arraylist**オブジェクトの内容を表示します。</span><span class="sxs-lookup"><span data-stu-id="e5377-184">The code creates an **ArrayList** object, uses a loop to load it with values, and then uses another loop to display the contents of the **ArrayList** object.</span></span>
4. <span data-ttu-id="e5377-185">CTRL キーを押し**ながら F5**キーを押してページを実行し、**ボタン**をクリックして、次の出力が表示されることを確認します。</span><span class="sxs-lookup"><span data-stu-id="e5377-185">Press **CTRL+F5** to run the page, and then click the **button** to make sure that you see the following output:</span></span>   

    [!code-html[Main](code-editing-in-web-forms-pages/samples/sample3.html)]
5. <span data-ttu-id="e5377-186">コードエディターに戻り、イベントハンドラーで次の行を選択します。</span><span class="sxs-lookup"><span data-stu-id="e5377-186">Return to the code editor, and then select the following lines in the event handler.</span></span>   

    [!code-html[Main](code-editing-in-web-forms-pages/samples/sample4.html)]
6. <span data-ttu-id="e5377-187">選択範囲を右クリックし、 **[リファクター]** 、 **[メソッドの抽出]** の順にクリックします。</span><span class="sxs-lookup"><span data-stu-id="e5377-187">Right-click the selection, click **Refactor**, and then choose **Extract Method**.</span></span> 

    <span data-ttu-id="e5377-188">**[メソッドの抽出]** ダイアログボックスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="e5377-188">The **Extract Method** dialog box appears.</span></span>
7. <span data-ttu-id="e5377-189">**[新しいメソッド名]** ボックスに「 **displayarray**」と入力し、 **[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="e5377-189">In the **New Method Name** box, type **DisplayArray**, and then click **OK**.</span></span> 

    <span data-ttu-id="e5377-190">コードエディターによって `DisplayArray`という名前の新しいメソッドが作成され、ループがもともと呼び出されていた**クリック**ハンドラーに新しいメソッドの呼び出しが配置されます。</span><span class="sxs-lookup"><span data-stu-id="e5377-190">The code editor creates a new method named `DisplayArray`, and puts a call to the new method in the **Click** handler where the loop was originally.</span></span>

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample5.cs?highlight=12)]
8. <span data-ttu-id="e5377-191">CTRL キーを押し**ながら F5**キーを押してページを再度実行し、**ボタン**をクリックします。</span><span class="sxs-lookup"><span data-stu-id="e5377-191">Press **CTRL+F5** to run the page again, and click the **button**.</span></span>

    <span data-ttu-id="e5377-192">ページは、以前と同じように機能します。</span><span class="sxs-lookup"><span data-stu-id="e5377-192">The page functions the same as it did before.</span></span> <span data-ttu-id="e5377-193">`DisplayArray` メソッドは、ページクラスのどこからでも呼び出すことができるようになりました。</span><span class="sxs-lookup"><span data-stu-id="e5377-193">The `DisplayArray` method can now be call from anywhere in the page class.</span></span>

## <a name="renaming-variables"></a><span data-ttu-id="e5377-194">変数名の変更</span><span class="sxs-lookup"><span data-stu-id="e5377-194">Renaming Variables</span></span>

<span data-ttu-id="e5377-195">変数とオブジェクトを操作する場合は、コード内で既に参照されているときに名前を変更することもできます。</span><span class="sxs-lookup"><span data-stu-id="e5377-195">When you work with variables, as well as objects, you might want to rename them after they are already referenced in your code.</span></span> <span data-ttu-id="e5377-196">ただし、変数とオブジェクトの名前を変更すると、いずれかの参照の名前を変更しないとコードが破損する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="e5377-196">However, renaming variables and objects can cause the code to break if you miss renaming one of the references.</span></span> <span data-ttu-id="e5377-197">そのため、リファクタリングを使用して名前の変更を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="e5377-197">Therefore, you can use refactoring to perform the renaming.</span></span>

### <a name="to-use-refactoring-to-rename-a-variable"></a><span data-ttu-id="e5377-198">リファクタリングを使用して変数の名前を変更するには</span><span class="sxs-lookup"><span data-stu-id="e5377-198">To use refactoring to rename a variable</span></span>

1. <span data-ttu-id="e5377-199">**Click**イベントハンドラーで、次の行を見つけます。</span><span class="sxs-lookup"><span data-stu-id="e5377-199">In the **Click** event handler, locate the following line:</span></span>

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample6.cs)]
2. <span data-ttu-id="e5377-200">変数名 `alist`を右クリックし、 **[リファクター]** 、 **[名前の変更]** の順に選択します。</span><span class="sxs-lookup"><span data-stu-id="e5377-200">Right-click the variable name `alist`, choose **Refactor**, and then choose **Rename**.</span></span>

    <span data-ttu-id="e5377-201">**[名前の変更]** ダイアログボックスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="e5377-201">The **Rename** dialog box appears.</span></span>
3. <span data-ttu-id="e5377-202">**[新しい名前]** ボックスに「 **ArrayList1** 」と入力し、 **[参照の変更のプレビュー]** チェックボックスがオンになっていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="e5377-202">In the **New name** box, type **ArrayList1** and make sure the **Preview reference changes** checkbox has been selected.</span></span> <span data-ttu-id="e5377-203">次に、 **[OK]** をクリックします</span><span class="sxs-lookup"><span data-stu-id="e5377-203">Then click **OK**.</span></span>

    <span data-ttu-id="e5377-204">**[変更のプレビュー]** ダイアログボックスが表示され、名前を変更しようとしている変数へのすべての参照を含むツリーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="e5377-204">The **Preview Changes** dialog box appears, and displays a tree that contains all references to the variable that you are renaming.</span></span>
4. <span data-ttu-id="e5377-205">**[適用]** をクリックして、 **[変更のプレビュー]** ダイアログボックスを閉じます。</span><span class="sxs-lookup"><span data-stu-id="e5377-205">Click **Apply** to close the **Preview Changes** dialog box.</span></span>

    <span data-ttu-id="e5377-206">選択したインスタンスを明示的に参照する変数の名前は変更されます。</span><span class="sxs-lookup"><span data-stu-id="e5377-206">The variables that refer specifically to the instance that you selected are renamed.</span></span> <span data-ttu-id="e5377-207">ただし、次の行に `alist` 変数の名前は変更されないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="e5377-207">Note, however, that the variable `alist` in the following line is not renamed.</span></span>

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample7.cs)]

    <span data-ttu-id="e5377-208">この行の `alist` 変数の名前は変更されません。これは、名前を変更した `alist` 変数と同じ値を表していないためです。</span><span class="sxs-lookup"><span data-stu-id="e5377-208">The variable `alist` in this line is not renamed because it does not represent the same value as the variable `alist` that you renamed.</span></span> <span data-ttu-id="e5377-209">`DisplayArray` 宣言内の変数 `alist` は、そのメソッドのローカル変数です。</span><span class="sxs-lookup"><span data-stu-id="e5377-209">The variable `alist` in the `DisplayArray` declaration is a local variable for that method.</span></span> <span data-ttu-id="e5377-210">これは、リファクタリングを使用して変数名を変更することは、エディターで [検索と置換] アクションを実行することとは異なります。リファクタリングでは、変数の名前が、使用している変数のセマンティクスに関する情報で変更されます。</span><span class="sxs-lookup"><span data-stu-id="e5377-210">This illustrates that using refactoring to rename variables is different than simply performing a find-and-replace action in the editor; refactoring renames variables with knowledge of the semantics of the variable that it is working with.</span></span>

## <a name="inserting-snippets"></a><span data-ttu-id="e5377-211">スニペットの挿入</span><span class="sxs-lookup"><span data-stu-id="e5377-211">Inserting Snippets</span></span>

<span data-ttu-id="e5377-212">多くの場合、Web フォームの開発者が頻繁に実行する必要があるコーディングタスクが多数あるため、コードエディターでは、スニペットのライブラリ、または記述済みのコードのブロックが提供されます。</span><span class="sxs-lookup"><span data-stu-id="e5377-212">Because there are many coding tasks that Web Forms developers frequently need to perform, the code editor provides a library of snippets, or blocks of prewritten code.</span></span> <span data-ttu-id="e5377-213">これらのスニペットは、ページに挿入できます。</span><span class="sxs-lookup"><span data-stu-id="e5377-213">You can insert these snippets into your page.</span></span>

<span data-ttu-id="e5377-214">Visual Studio で使用する各言語には、コード スニペットを挿入する方法にはわずかな違いがあります。</span><span class="sxs-lookup"><span data-stu-id="e5377-214">Each language that you use in Visual Studio has slight differences in the way you insert code snippets.</span></span> <span data-ttu-id="e5377-215">スニペットの挿入の詳細については、「 [Visual Basic IntelliSense コードスニペット](https://msdn.microsoft.com/library/18yz4be4.aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="e5377-215">For information about inserting snippets, see [Visual Basic IntelliSense Code Snippets](https://msdn.microsoft.com/library/18yz4be4.aspx).</span></span> <span data-ttu-id="e5377-216">ビジュアルC#にスニペットを挿入する方法の詳細については、「 [ C# visual コードスニペット](https://msdn.microsoft.com/library/z41h7fat.aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="e5377-216">For information about inserting snippets in Visual C#, see [Visual C# Code Snippets](https://msdn.microsoft.com/library/z41h7fat.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e5377-217">次の手順</span><span class="sxs-lookup"><span data-stu-id="e5377-217">Next Steps</span></span>

<span data-ttu-id="e5377-218">このチュートリアルでは、Visual Studio 2010 コードエディターの基本的な機能について説明しました。コード内のエラーを修正し、コードをリファクタリングし、変数の名前を変更し、コードスニペットをコードに挿入します。</span><span class="sxs-lookup"><span data-stu-id="e5377-218">This walkthrough has illustrated the basic features of the Visual Studio 2010 code editor for correcting errors in your code, refactoring code, renaming variables, and inserting code snippets into your code.</span></span> <span data-ttu-id="e5377-219">エディターのその他の機能を使用すると、アプリケーション開発を迅速かつ簡単に行うことができます。</span><span class="sxs-lookup"><span data-stu-id="e5377-219">Additional features in the editor can make application development fast and easy.</span></span> <span data-ttu-id="e5377-220">たとえば、次の場合です。</span><span class="sxs-lookup"><span data-stu-id="e5377-220">For example, you might want to:</span></span>

- <span data-ttu-id="e5377-221">Intellisense のオプションの変更、コードスニペットの管理、オンラインでのコードスニペットの検索など、IntelliSense の機能の詳細について説明します。</span><span class="sxs-lookup"><span data-stu-id="e5377-221">Learn more about the features of IntelliSense, such as modifying IntelliSense options, managing code snippets, and searching for code snippets online.</span></span> <span data-ttu-id="e5377-222">詳細については、「 [Using IntelliSense](https://msdn.microsoft.com/library/hcw1s69b.aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="e5377-222">For more information, see [Using IntelliSense](https://msdn.microsoft.com/library/hcw1s69b.aspx).</span></span>
- <span data-ttu-id="e5377-223">独自のコードスニペットを作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="e5377-223">Learn how to create your own code snippets.</span></span> <span data-ttu-id="e5377-224">詳細については、「 [IntelliSense コードスニペットの作成と使用](https://msdn.microsoft.com/library/ms165392.aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="e5377-224">For more information, see [Creating and Using IntelliSense Code Snippets](https://msdn.microsoft.com/library/ms165392.aspx)</span></span>
- <span data-ttu-id="e5377-225">スニペットのカスタマイズやトラブルシューティングなど、IntelliSense コードスニペットの Visual Basic 固有の機能について説明します。</span><span class="sxs-lookup"><span data-stu-id="e5377-225">Learn more about the Visual Basic-specific features of IntelliSense code snippets, such as customizing the snippets and troubleshooting.</span></span> <span data-ttu-id="e5377-226">詳細については、「 [Visual Basic IntelliSense コードスニペット](https://msdn.microsoft.com/library/18yz4be4.aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="e5377-226">For more information, see [Visual Basic IntelliSense Code Snippets](https://msdn.microsoft.com/library/18yz4be4.aspx)</span></span>
- <span data-ttu-id="e5377-227">詳細については、C# は、リファクタリングとコード スニペットなど、IntelliSense の特定の機能。</span><span class="sxs-lookup"><span data-stu-id="e5377-227">Learn more about the C#-specific features of IntelliSense, such as refactoring and code snippets.</span></span> <span data-ttu-id="e5377-228">詳細については、「 [Visual C# IntelliSense](https://msdn.microsoft.com/library/43f44291.aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="e5377-228">For more information, see [Visual C# IntelliSense](https://msdn.microsoft.com/library/43f44291.aspx).</span></span>
