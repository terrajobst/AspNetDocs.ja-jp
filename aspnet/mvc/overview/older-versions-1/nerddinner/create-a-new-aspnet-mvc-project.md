---
uid: mvc/overview/older-versions-1/nerddinner/create-a-new-aspnet-mvc-project
title: 新しい ASP.NET MVC プロジェクトを作成する |Microsoft Docs
author: microsoft
description: 手順 1. では、基本的なユーザーのアプリケーション構造を配置する方法を示します。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 7e0e9928-8fdc-4b74-9882-55fac0976628
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/create-a-new-aspnet-mvc-project
msc.type: authoredcontent
ms.openlocfilehash: 189ddc187fc83db14106b2da199ba12a70a32b45
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78469240"
---
# <a name="create-a-new-aspnet-mvc-project"></a><span data-ttu-id="754e4-103">新しい ASP.NET MVC プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="754e4-103">Create a New ASP.NET MVC Project</span></span>

<span data-ttu-id="754e4-104">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="754e4-104">by [Microsoft](https://github.com/microsoft)</span></span>

<span data-ttu-id="754e4-105">[[Download PDF]\(PDF をダウンロード\)](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)</span><span class="sxs-lookup"><span data-stu-id="754e4-105">[Download PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)</span></span>

> <span data-ttu-id="754e4-106">これは、ASP.NET MVC 1 を使用して小規模で完成した web アプリケーションを構築する方法について説明する無料の["" アプリケーションのチュートリアル](introducing-the-nerddinner-tutorial.md)の手順1です。</span><span class="sxs-lookup"><span data-stu-id="754e4-106">This is step 1 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="754e4-107">手順 1. では、基本的なユーザーのアプリケーション構造を配置する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="754e4-107">Step 1 shows you how to put the basic NerdDinner application structure in place.</span></span>
> 
> <span data-ttu-id="754e4-108">ASP.NET MVC 3 を使用している場合は、MVC 3 または[Mvc ミュージックストア](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)[のチュートリアルではじめに](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)に従うことをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="754e4-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-1-file-gtnew-project"></a><span data-ttu-id="754e4-109">手順 1: ファイル&gt;新しいプロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="754e4-109">NerdDinner Step 1: File-&gt;New Project</span></span>

<span data-ttu-id="754e4-110">次に、Visual Studio 2008 または無料の Visual Web Developer 2008 Express のいずれかで、[**ファイル]&gt;[新しいプロジェクト**] メニュー項目を選択して、このアプリケーションを開始します。</span><span class="sxs-lookup"><span data-stu-id="754e4-110">We'll begin our NerdDinner application by selecting the **File-&gt;New Project** menu item within either Visual Studio 2008 or the free Visual Web Developer 2008 Express.</span></span>

<span data-ttu-id="754e4-111">[新しいプロジェクト] ダイアログが表示されます。</span><span class="sxs-lookup"><span data-stu-id="754e4-111">This will bring up the "New Project" dialog.</span></span> <span data-ttu-id="754e4-112">新しい ASP.NET MVC アプリケーションを作成するには、ダイアログの左側にある [Web] ノードを選択し、右側の [ASP.NET MVC Web アプリケーション] プロジェクトテンプレートを選択します。</span><span class="sxs-lookup"><span data-stu-id="754e4-112">To create a new ASP.NET MVC application, we'll select the "Web" node on the left-hand side of the dialog and then choose the "ASP.NET MVC Web Application" project template on the right:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image1.png)

<span data-ttu-id="754e4-113">*重要: ASP.NET MVC をダウンロードしてインストールしたことを確認してください。そうしないと、[新しいプロジェクト] ダイアログに表示されません。まだインストールしていない場合は、 [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)の V2 を使用できます (ASP.NET MVC は、"Web Platform-&gt;framework and runtime" セクション内で利用できます)。*</span><span class="sxs-lookup"><span data-stu-id="754e4-113">*Important: Make sure you've downloaded and installed ASP.NET MVC - otherwise it won't show up in the New Project dialog. You can use V2 of the [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx) if you haven't installed it yet (ASP.NET MVC is available within the "Web Platform-&gt;Frameworks and Runtimes" section).*</span></span>

<span data-ttu-id="754e4-114">作成する新しいプロジェクトに "are Dディナー" という名前を指定し、[ok] ボタンをクリックして作成します。</span><span class="sxs-lookup"><span data-stu-id="754e4-114">We'll name the new project we are going to create "NerdDinner" and then click the "ok" button to create it.</span></span>

<span data-ttu-id="754e4-115">[Ok] をクリックすると、Visual Studio によって追加のダイアログが表示され、必要に応じて新しいアプリケーションの単体テストプロジェクトも作成するように求められます。</span><span class="sxs-lookup"><span data-stu-id="754e4-115">When we click "ok" Visual Studio will bring up an additional dialog that prompts us to optionally create a unit test project for the new application as well.</span></span> <span data-ttu-id="754e4-116">この単体テストプロジェクトを使用すると、アプリケーションの機能と動作を確認する自動テストを作成できます (このチュートリアルで後ほど説明します)。</span><span class="sxs-lookup"><span data-stu-id="754e4-116">This unit test project enables us to create automated tests that verify the functionality and behavior of our application (something we'll cover how to-do later in this tutorial).</span></span>

![](create-a-new-aspnet-mvc-project/_static/image2.png)

<span data-ttu-id="754e4-117">このダイアログの [テストフレームワーク] ドロップダウンには、コンピューターにインストールされている使用可能なすべての ASP.NET MVC 単体テストプロジェクトテンプレートが表示されます。</span><span class="sxs-lookup"><span data-stu-id="754e4-117">The "Test framework" dropdown in the above dialog is populated with all available ASP.NET MVC unit test project templates installed on the machine.</span></span> <span data-ttu-id="754e4-118">NUnit、MBUnit、XUnit のバージョンをダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="754e4-118">Versions can be downloaded for NUnit, MBUnit, and XUnit.</span></span> <span data-ttu-id="754e4-119">組み込みの Visual Studio 単体テストフレームワークもサポートされています。</span><span class="sxs-lookup"><span data-stu-id="754e4-119">The built-in Visual Studio Unit Test framework is also supported.</span></span>

<span data-ttu-id="754e4-120">*注: Visual Studio 単体テストフレームワークは、Visual Studio 2008 Professional 以降のバージョンでのみ使用できます。VS 2008 Standard Edition または Visual Web Developer 2008 Express を使用している場合は、このダイアログを表示するために、ASP.NET MVC の NUnit、MBUnit、または XUnit 拡張機能をダウンロードしてインストールする必要があります。テストフレームワークがインストールされていない場合、ダイアログは表示されません。*</span><span class="sxs-lookup"><span data-stu-id="754e4-120">*Note: The Visual Studio Unit Test Framework is only available with Visual Studio 2008 Professional and higher versions. If you are using VS 2008 Standard Edition or Visual Web Developer 2008 Express you will need to download and install the NUnit, MBUnit or XUnit extensions for ASP.NET MVC in order for this dialog to be shown. The dialog will not display if there aren't any test frameworks installed.*</span></span>

<span data-ttu-id="754e4-121">ここでは、作成したテストプロジェクトに対して既定の "" を使用する "という名前を使用し、" Visual Studio 単体テスト "フレームワークオプションを使用します。</span><span class="sxs-lookup"><span data-stu-id="754e4-121">We'll use the default "NerdDinner.Tests" name for the test project we create, and use the "Visual Studio Unit Test" framework option.</span></span> <span data-ttu-id="754e4-122">[Ok] ボタンをクリックすると、Visual Studio によって、2つのプロジェクト (web アプリケーション用と単体テスト用) を含むソリューションが作成されます。</span><span class="sxs-lookup"><span data-stu-id="754e4-122">When we click the "ok" button Visual Studio will create a solution for us with two projects in it - one for our web application and one for our unit tests:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image3.png)

### <a name="examining-the-nerddinner-directory-structure"></a><span data-ttu-id="754e4-123">各ディレクトリ構造の検証</span><span class="sxs-lookup"><span data-stu-id="754e4-123">Examining the NerdDinner directory structure</span></span>

<span data-ttu-id="754e4-124">Visual Studio で新しい ASP.NET MVC アプリケーションを作成すると、次のような多数のファイルとディレクトリがプロジェクトに自動的に追加されます。</span><span class="sxs-lookup"><span data-stu-id="754e4-124">When you create a new ASP.NET MVC application with Visual Studio, it automatically adds a number of files and directories to the project:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image4.png)

<span data-ttu-id="754e4-125">既定では、ASP.NET MVC プロジェクトには、次の6つの最上位レベルのディレクトリがあります。</span><span class="sxs-lookup"><span data-stu-id="754e4-125">ASP.NET MVC projects by default have six top-level directories:</span></span>

| <span data-ttu-id="754e4-126">**ディレクトリ**</span><span class="sxs-lookup"><span data-stu-id="754e4-126">**Directory**</span></span> | <span data-ttu-id="754e4-127">**目的**</span><span class="sxs-lookup"><span data-stu-id="754e4-127">**Purpose**</span></span> |
| --- | --- |
| <span data-ttu-id="754e4-128">**/コントローラー**</span><span class="sxs-lookup"><span data-stu-id="754e4-128">**/Controllers**</span></span> | <span data-ttu-id="754e4-129">URL 要求を処理するコントローラークラスを配置する場所</span><span class="sxs-lookup"><span data-stu-id="754e4-129">Where you put Controller classes that handle URL requests</span></span> |
| <span data-ttu-id="754e4-130">**/Models**</span><span class="sxs-lookup"><span data-stu-id="754e4-130">**/Models**</span></span> | <span data-ttu-id="754e4-131">データを表現および操作するクラスを配置する場所</span><span class="sxs-lookup"><span data-stu-id="754e4-131">Where you put classes that represent and manipulate data</span></span> |
| <span data-ttu-id="754e4-132">**/Views**</span><span class="sxs-lookup"><span data-stu-id="754e4-132">**/Views**</span></span> | <span data-ttu-id="754e4-133">出力のレンダリングを担当する UI テンプレートファイルを配置する場所</span><span class="sxs-lookup"><span data-stu-id="754e4-133">Where you put UI template files that are responsible for rendering output</span></span> |
| <span data-ttu-id="754e4-134">**/Scripts**</span><span class="sxs-lookup"><span data-stu-id="754e4-134">**/Scripts**</span></span> | <span data-ttu-id="754e4-135">JavaScript ライブラリファイルとスクリプト (.js) を配置する場所</span><span class="sxs-lookup"><span data-stu-id="754e4-135">Where you put JavaScript library files and scripts (.js)</span></span> |
| <span data-ttu-id="754e4-136">**/コンテンツ**</span><span class="sxs-lookup"><span data-stu-id="754e4-136">**/Content**</span></span> | <span data-ttu-id="754e4-137">CSS およびイメージファイル、およびその他の非動的/非 JavaScript コンテンツを配置する場所</span><span class="sxs-lookup"><span data-stu-id="754e4-137">Where you put CSS and image files, and other non-dynamic/non-JavaScript content</span></span> |
| <span data-ttu-id="754e4-138">**/アプリ\_データ**</span><span class="sxs-lookup"><span data-stu-id="754e4-138">**/App\_Data**</span></span> | <span data-ttu-id="754e4-139">読み取り/書き込みの対象となるデータファイルを保存する場所。</span><span class="sxs-lookup"><span data-stu-id="754e4-139">Where you store data files you want to read/write.</span></span> |

<span data-ttu-id="754e4-140">ASP.NET MVC では、この構造は必要ありません。</span><span class="sxs-lookup"><span data-stu-id="754e4-140">ASP.NET MVC does not require this structure.</span></span> <span data-ttu-id="754e4-141">実際、大規模なアプリケーションで作業している開発者は、通常、アプリケーションを複数のプロジェクトに分割して管理しやすくしています (たとえば、データモデルクラスは、多くの場合、web アプリケーションとは別のクラスライブラリプロジェクトにあります)。</span><span class="sxs-lookup"><span data-stu-id="754e4-141">In fact, developers working on large applications will typically partition the application up across multiple projects to make it more manageable (for example: data model classes often go in a separate class library project from the web application).</span></span> <span data-ttu-id="754e4-142">ただし、既定のプロジェクト構造には、アプリケーションの問題をクリーンな状態に保つために使用できる、既定のディレクトリ規則が用意されています。</span><span class="sxs-lookup"><span data-stu-id="754e4-142">The default project structure, however, does provide a nice default directory convention that we can use to keep our application concerns clean.</span></span>

<span data-ttu-id="754e4-143">コントローラーディレクトリを展開すると、Visual Studio によって、HomeController と AccountController という2つのコントローラークラスが既定でプロジェクトに追加されていることがわかります。</span><span class="sxs-lookup"><span data-stu-id="754e4-143">When we expand the /Controllers directory we'll find that Visual Studio added two controller classes – HomeController and AccountController – by default to the project:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image5.png)

<span data-ttu-id="754e4-144">ビューディレクトリを展開すると、3つのサブディレクトリ (/Home、/Account、/Shared) が検出されます。また、その中にはいくつかのテンプレートファイルも既定でプロジェクトに追加されています。</span><span class="sxs-lookup"><span data-stu-id="754e4-144">When we expand the /Views directory, we'll find three sub-directories – /Home, /Account and /Shared – as well as several template files within them were also added to the project by default:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image6.png)

<span data-ttu-id="754e4-145">/コンテンツディレクトリとスクリプトディレクトリを展開すると、サイト上のすべての HTML のスタイルを設定するために使用される .css ファイルと、アプリケーション内で ASP.NET AJAX および jQuery サポートを有効にできる JavaScript ライブラリが見つかります。</span><span class="sxs-lookup"><span data-stu-id="754e4-145">When we expand the /Content and /Scripts directories, we'll find a Site.css file that is used to style all HTML on the site, as well as JavaScript libraries that can enable ASP.NET AJAX and jQuery support within the application:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image7.png)

<span data-ttu-id="754e4-146">このテストプロジェクトを展開すると、コントローラークラスの単体テストを含む2つのクラスが見つかります。</span><span class="sxs-lookup"><span data-stu-id="754e4-146">When we expand the NerdDinner.Tests project we'll find two classes that contain unit tests for our controller classes:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image8.png)

<span data-ttu-id="754e4-147">Visual Studio によって追加されたこれらの既定のファイルには、作業中のアプリケーション (ホームページ、about ページ、アカウントのログイン/ログアウト/登録ページ) の基本構造と、ハンドルされないエラーページ (すべてのワイヤード (有線) と機能があります) が用意されています。</span><span class="sxs-lookup"><span data-stu-id="754e4-147">These default files added by Visual Studio provide us with a basic structure for a working application - complete with home page, about page, account login/logout/registration pages, and an unhandled error page (all wired-up and working out of the box).</span></span>

### <a name="running-the-nerddinner-application"></a><span data-ttu-id="754e4-148">アプリケーションの実行</span><span class="sxs-lookup"><span data-stu-id="754e4-148">Running the NerdDinner Application</span></span>

<span data-ttu-id="754e4-149">プロジェクトを実行するには、[デバッグ]、[デバッグの開始]、また&gt;は [デバッグ] の順に選択 **&gt;** し、[デバッグ**なしで開始**] メニュー項目を選択します</span><span class="sxs-lookup"><span data-stu-id="754e4-149">We can run the project by choosing either the **Debug-&gt;Start Debugging** or **Debug-&gt;Start Without Debugging** menu items:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image9.png)

<span data-ttu-id="754e4-150">これにより、Visual Studio に付属する組み込みの ASP.NET Web サーバーが起動し、アプリケーションが実行されます。</span><span class="sxs-lookup"><span data-stu-id="754e4-150">This will launch the built-in ASP.NET Web-server that comes with Visual Studio, and run our application:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image10.png)

<span data-ttu-id="754e4-151">次に示すのは、新しいプロジェクト (URL: "/") の実行時のホームページです。</span><span class="sxs-lookup"><span data-stu-id="754e4-151">Below is the home page for our new project (URL: "/") when it runs:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image11.png)

<span data-ttu-id="754e4-152">[バージョン情報] タブをクリックすると、about ページ (URL: "/Home/About") が表示されます。</span><span class="sxs-lookup"><span data-stu-id="754e4-152">Clicking the "About" tab displays an about page (URL: "/Home/About"):</span></span>

![](create-a-new-aspnet-mvc-project/_static/image12.png)

<span data-ttu-id="754e4-153">右上にある [ログオン] リンクをクリックすると、ログインページ (URL: "/アカウント/ログオン") に移動します。</span><span class="sxs-lookup"><span data-stu-id="754e4-153">Clicking the "Log On" link on the top-right takes us to a Login page (URL: "/Account/LogOn")</span></span>

![](create-a-new-aspnet-mvc-project/_static/image13.png)

<span data-ttu-id="754e4-154">ログインアカウントがない場合は、[登録] リンク (URL: "/Account/register") をクリックして作成できます。</span><span class="sxs-lookup"><span data-stu-id="754e4-154">If we don't have a login account we can click the register link (URL: "/Account/Register") to create one:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image14.png)

<span data-ttu-id="754e4-155">上記の home、about、および logout/register 機能を実装するコードは、新しいプロジェクトを作成したときに既定で追加されました。</span><span class="sxs-lookup"><span data-stu-id="754e4-155">The code to implement the above home, about, and logout/ register functionality was added by default when we created our new project.</span></span> <span data-ttu-id="754e4-156">アプリケーションの出発点として使用します。</span><span class="sxs-lookup"><span data-stu-id="754e4-156">We'll use it as the starting point of our application.</span></span>

### <a name="testing-the-nerddinner-application"></a><span data-ttu-id="754e4-157">アプリケーションのテスト</span><span class="sxs-lookup"><span data-stu-id="754e4-157">Testing the NerdDinner Application</span></span>

<span data-ttu-id="754e4-158">Professional Edition 以降のバージョンの Visual Studio 2008 を使用している場合は、Visual Studio 内で組み込みの単体テスト IDE サポートを使用してプロジェクトをテストすることができます。</span><span class="sxs-lookup"><span data-stu-id="754e4-158">If we are using the Professional Edition or higher version of Visual Studio 2008, we can use the built-in unit testing IDE support within Visual Studio to test the project:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image15.png)

<span data-ttu-id="754e4-159">上記のオプションのいずれかを選択すると、IDE 内の [テスト結果] ウィンドウが開き、組み込みの機能について説明する新しいプロジェクトに含まれている27の単体テストに合格/不合格の状態が表示されます。</span><span class="sxs-lookup"><span data-stu-id="754e4-159">Choosing one of the above options will open the "Test Results" pane within the IDE and provide us with pass/fail status on the 27 unit tests included in our new project that cover the built-in functionality:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image16.png)

<span data-ttu-id="754e4-160">このチュートリアルの後半では、自動化されたテストについて詳しく説明し、実装するアプリケーション機能をカバーする追加の単体テストを追加します。</span><span class="sxs-lookup"><span data-stu-id="754e4-160">Later in this tutorial we'll talk more about automated testing and add additional unit tests that cover the application functionality we implement.</span></span>

### <a name="next-step"></a><span data-ttu-id="754e4-161">次の手順</span><span class="sxs-lookup"><span data-stu-id="754e4-161">Next Step</span></span>

<span data-ttu-id="754e4-162">これで、基本的なアプリケーション構造が完成しました。</span><span class="sxs-lookup"><span data-stu-id="754e4-162">We've now got a basic application structure in place.</span></span> <span data-ttu-id="754e4-163">次[に、アプリケーションデータを格納するデータベースを作成](create-a-database.md)しましょう。</span><span class="sxs-lookup"><span data-stu-id="754e4-163">Let's now [create a database to store our application data](create-a-database.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="754e4-164">[前へ](introducing-the-nerddinner-tutorial.md)
> [次へ](create-a-database.md)</span><span class="sxs-lookup"><span data-stu-id="754e4-164">[Previous](introducing-the-nerddinner-tutorial.md)
[Next](create-a-database.md)</span></span>
