---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-a-controller-vb
title: コントローラーを作成する (VB) |Microsoft Docs
author: StephenWalther
description: このチュートリアルでは、Stephen Walther は、ASP.NET MVC アプリケーションにコントローラーを追加する方法を示しています。
ms.author: riande
ms.date: 03/02/2009
ms.assetid: 204b7e86-f560-4611-8adb-785b33e777b9
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-a-controller-vb
msc.type: authoredcontent
ms.openlocfilehash: 60636b79ab5fc06ca904dee90ce74f256e046d12
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486832"
---
# <a name="creating-a-controller-vb"></a><span data-ttu-id="fb092-103">コントローラーを作成する (VB)</span><span class="sxs-lookup"><span data-stu-id="fb092-103">Creating a Controller (VB)</span></span>

<span data-ttu-id="fb092-104">[Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="fb092-104">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="fb092-105">このチュートリアルでは、Stephen Walther は、ASP.NET MVC アプリケーションにコントローラーを追加する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="fb092-105">In this tutorial, Stephen Walther demonstrates how you can add a controller to an ASP.NET MVC application.</span></span>

<span data-ttu-id="fb092-106">このチュートリアルの目的は、新しい ASP.NET MVC コントローラーを作成する方法を説明することです。</span><span class="sxs-lookup"><span data-stu-id="fb092-106">The goal of this tutorial is to explain how you can create new ASP.NET MVC controllers.</span></span> <span data-ttu-id="fb092-107">コントローラーを作成する方法については、Visual Studio の [コントローラーの追加] メニューオプションを使用する方法と、手動でクラスファイルを作成する方法に関するページを参照してください。</span><span class="sxs-lookup"><span data-stu-id="fb092-107">You learn how to create controllers both by using the Visual Studio Add Controller menu option and by creating a class file by hand.</span></span>

### <a name="using-the-add-controller-menu-option"></a><span data-ttu-id="fb092-108">[コントローラーの追加] メニューオプションの使用</span><span class="sxs-lookup"><span data-stu-id="fb092-108">Using the Add Controller Menu Option</span></span>

<span data-ttu-id="fb092-109">新しいコントローラーを作成する最も簡単な方法は、Visual Studio のソリューションエクスプローラーウィンドウで Controllers フォルダーを右クリックし、[**追加]、[コントローラー** ] メニューオプション (図1を参照) を選択することです。</span><span class="sxs-lookup"><span data-stu-id="fb092-109">The easiest way to create a new controller is to right-click the Controllers folder in the Visual Studio Solution Explorer window and select the **Add, Controller** menu option (see Figure 1).</span></span> <span data-ttu-id="fb092-110">このメニューオプションを選択すると、 **[コントローラーの追加]** ダイアログボックスが開きます (図2を参照)。</span><span class="sxs-lookup"><span data-stu-id="fb092-110">Selecting this menu option opens the **Add Controller** dialog (see Figure 2).</span></span>

<span data-ttu-id="fb092-111">[[新しいプロジェクト] ダイアログボックスの ![](creating-a-controller-vb/_static/image1.jpg)](creating-a-controller-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="fb092-111">[![The New Project dialog box](creating-a-controller-vb/_static/image1.jpg)](creating-a-controller-vb/_static/image1.png)</span></span>

<span data-ttu-id="fb092-112">**図 01**: 新しいコントローラーを追加[する (クリックすると、フルサイズの画像が表示](creating-a-controller-vb/_static/image2.png)される)</span><span class="sxs-lookup"><span data-stu-id="fb092-112">**Figure 01**: Adding a new controller([Click to view full-size image](creating-a-controller-vb/_static/image2.png))</span></span>

<span data-ttu-id="fb092-113">[[新しいプロジェクト] ダイアログボックスの ![](creating-a-controller-vb/_static/image2.jpg)](creating-a-controller-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="fb092-113">[![The New Project dialog box](creating-a-controller-vb/_static/image2.jpg)](creating-a-controller-vb/_static/image3.png)</span></span>

<span data-ttu-id="fb092-114">**図 02**: [コントローラーの追加] ダイアログボックス ([クリックすると、フルサイズの画像が表示](creating-a-controller-vb/_static/image4.png)されます)</span><span class="sxs-lookup"><span data-stu-id="fb092-114">**Figure 02**: The Add Controller dialog ([Click to view full-size image](creating-a-controller-vb/_static/image4.png))</span></span>

<span data-ttu-id="fb092-115">コントローラー名の最初の部分が **[コントローラーの追加]** ダイアログボックスで強調表示されていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="fb092-115">Notice that the first part of the controller name is highlighted in the **Add Controller** dialog.</span></span> <span data-ttu-id="fb092-116">すべてのコントローラー名は、サフィックス*コントローラー*で終わる必要があります。</span><span class="sxs-lookup"><span data-stu-id="fb092-116">Every controller name must end with the suffix *Controller*.</span></span> <span data-ttu-id="fb092-117">たとえば、 *Productcontroller*という名前のコントローラーを作成できますが、 *product*という名前のコントローラーは作成できません。</span><span class="sxs-lookup"><span data-stu-id="fb092-117">For example, you can create a controller named *ProductController* but not a controller named *Product*.</span></span>

<span data-ttu-id="fb092-118">*コントローラーのサフィックスが*ないコントローラーを作成すると、コントローラーを呼び出すことができなくなります。</span><span class="sxs-lookup"><span data-stu-id="fb092-118">If you create a controller that is missing the *Controller* suffix then you won't be able to invoke the controller.</span></span> <span data-ttu-id="fb092-119">そうしないでください。この間違いを犯した後、非常に時間を無駄にすることはありません。</span><span class="sxs-lookup"><span data-stu-id="fb092-119">Don't do this -- I've wasted countless hours of my life after making this mistake.</span></span>

<span data-ttu-id="fb092-120">**リスト 1-コントローラーと vb**</span><span class="sxs-lookup"><span data-stu-id="fb092-120">**Listing 1 - Controllers\ProductController.vb**</span></span>

[!code-vb[Main](creating-a-controller-vb/samples/sample1.vb)]

<span data-ttu-id="fb092-121">コントローラーは、常に Controllers フォルダーに作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="fb092-121">You should always create controllers in the Controllers folder.</span></span> <span data-ttu-id="fb092-122">そうしないと、ASP.NET MVC の規則に違反することになり、他の開発者はアプリケーションを理解するのが困難になります。</span><span class="sxs-lookup"><span data-stu-id="fb092-122">Otherwise, you'll be violating the conventions of ASP.NET MVC and other developers will have a more difficult time understanding your application.</span></span>

### <a name="scaffolding-action-methods"></a><span data-ttu-id="fb092-123">スキャフォールディングアクションメソッド</span><span class="sxs-lookup"><span data-stu-id="fb092-123">Scaffolding Action Methods</span></span>

<span data-ttu-id="fb092-124">コントローラーを作成するときに、Create、Update、および Details アクションメソッドを自動的に生成するオプションがあります (図3を参照)。</span><span class="sxs-lookup"><span data-stu-id="fb092-124">When you create a controller, you have the option to generate Create, Update, and Details action methods automatically (see Figure 3).</span></span> <span data-ttu-id="fb092-125">このオプションを選択すると、リスト2のコントローラークラスが生成されます。</span><span class="sxs-lookup"><span data-stu-id="fb092-125">If you select this option then the controller class in Listing 2 is generated.</span></span>

<span data-ttu-id="fb092-126">[アクションメソッドを自動的に作成 ![](creating-a-controller-vb/_static/image3.jpg)](creating-a-controller-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="fb092-126">[![Creating action methods automatically](creating-a-controller-vb/_static/image3.jpg)](creating-a-controller-vb/_static/image5.png)</span></span>

<span data-ttu-id="fb092-127">**図 03**: アクションメソッドを自動的に作成[する (クリックすると、フルサイズの画像が表示](creating-a-controller-vb/_static/image6.png)される)</span><span class="sxs-lookup"><span data-stu-id="fb092-127">**Figure 03**: Creating action methods automatically ([Click to view full-size image](creating-a-controller-vb/_static/image6.png))</span></span>

<span data-ttu-id="fb092-128">**リスト 2-顧客コントローラー (vb)**</span><span class="sxs-lookup"><span data-stu-id="fb092-128">**Listing 2 - Controllers\CustomerController.vb**</span></span>

[!code-vb[Main](creating-a-controller-vb/samples/sample2.vb)]

<span data-ttu-id="fb092-129">これらのメソッドは、スタブメソッドです。</span><span class="sxs-lookup"><span data-stu-id="fb092-129">These generated methods are stub methods.</span></span> <span data-ttu-id="fb092-130">顧客の詳細を作成、更新、表示するための実際のロジックを自分で追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="fb092-130">You must add the actual logic for creating, updating, and showing details for a customer yourself.</span></span> <span data-ttu-id="fb092-131">ただし、スタブメソッドは、適切な開始点を提供します。</span><span class="sxs-lookup"><span data-stu-id="fb092-131">But, the stub methods provide you with a nice starting point.</span></span>

### <a name="creating-a-controller-class"></a><span data-ttu-id="fb092-132">コントローラークラスの作成</span><span class="sxs-lookup"><span data-stu-id="fb092-132">Creating a Controller Class</span></span>

<span data-ttu-id="fb092-133">ASP.NET MVC コントローラーはクラスにすぎません。</span><span class="sxs-lookup"><span data-stu-id="fb092-133">The ASP.NET MVC controller is just a class.</span></span> <span data-ttu-id="fb092-134">必要に応じて、Visual Studio コントローラーの便利なスキャフォールディングを無視し、手動でコントローラークラスを作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="fb092-134">If you prefer, you can ignore the convenient Visual Studio controller scaffolding and create a controller class by hand.</span></span> <span data-ttu-id="fb092-135">次の手順に従います。</span><span class="sxs-lookup"><span data-stu-id="fb092-135">Follow these steps:</span></span>

1. <span data-ttu-id="fb092-136">Controllers フォルダーを右クリックし、[**追加]、[新しい項目**] の順に選択し、 **[クラス]** テンプレートを選択します (図4を参照)。</span><span class="sxs-lookup"><span data-stu-id="fb092-136">Right-click the Controllers folder and select the menu option **Add, New Item** and select the **Class** template (see Figure 4).</span></span>
2. <span data-ttu-id="fb092-137">新しいクラスに「visual Controller .vb」という名前を指定し、 **[追加]** ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="fb092-137">Name the new class PersonController.vb and click the **Add** button.</span></span>
3. <span data-ttu-id="fb092-138">生成されたクラスファイルを変更して、クラスが基本の System.web. Mvc. Controller クラスから継承するようにします (リスト3を参照)。</span><span class="sxs-lookup"><span data-stu-id="fb092-138">Modify the resulting class file so that the class inherits from the base System.Web.Mvc.Controller class (see Listing 3).</span></span>

<span data-ttu-id="fb092-139">[新しいクラスの作成 ![](creating-a-controller-vb/_static/image4.jpg)](creating-a-controller-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="fb092-139">[![Creating a new class](creating-a-controller-vb/_static/image4.jpg)](creating-a-controller-vb/_static/image7.png)</span></span>

<span data-ttu-id="fb092-140">**図 04**: 新しいクラスを作成[する (クリックすると、フルサイズの画像が表示](creating-a-controller-vb/_static/image8.png)される)</span><span class="sxs-lookup"><span data-stu-id="fb092-140">**Figure 04**: Creating a new class([Click to view full-size image](creating-a-controller-vb/_static/image8.png))</span></span>

<span data-ttu-id="fb092-141">**リスト 3-フルマイコントローラー、vb**</span><span class="sxs-lookup"><span data-stu-id="fb092-141">**Listing 3 - Controllers\PersonController.vb**</span></span>

[!code-vb[Main](creating-a-controller-vb/samples/sample3.vb)]

<span data-ttu-id="fb092-142">リスト3のコントローラーは、"Hello World!" という文字列を返す Index () という名前の1つのアクションを公開します。</span><span class="sxs-lookup"><span data-stu-id="fb092-142">The controller in Listing 3 exposes one action named Index() that returns the string "Hello World!".</span></span> <span data-ttu-id="fb092-143">このコントローラーアクションを呼び出すには、アプリケーションを実行し、次のような URL を要求します。</span><span class="sxs-lookup"><span data-stu-id="fb092-143">You can invoke this controller action by running your application and requesting a URL like the following:</span></span>

`http://localhost:40071/Person`

> [!NOTE]
> 
> <span data-ttu-id="fb092-144">ASP.NET 開発サーバーはランダムなポート番号 (40071 など) を使用します。</span><span class="sxs-lookup"><span data-stu-id="fb092-144">The ASP.NET Development Server uses a random port number (for example, 40071).</span></span> <span data-ttu-id="fb092-145">コントローラーを起動するための URL を入力するときは、適切なポート番号を指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="fb092-145">When entering a URL to invoke a controller, you'll need to supply the right port number.</span></span> <span data-ttu-id="fb092-146">ポート番号を確認するには、Windows 通知領域 (画面の右下) にある ASP.NET 開発サーバーのアイコンの上にマウスポインターを置きます。</span><span class="sxs-lookup"><span data-stu-id="fb092-146">You can determine the port number by hovering your mouse over the icon for the ASP.NET Development Server in the Windows Notification Area (bottom-right of your screen).</span></span>
> 
> [!div class="step-by-step"]
> <span data-ttu-id="fb092-147">[前へ](adding-dynamic-content-to-a-cached-page-vb.md)
> [次へ](creating-an-action-vb.md)</span><span class="sxs-lookup"><span data-stu-id="fb092-147">[Previous](adding-dynamic-content-to-a-cached-page-vb.md)
[Next](creating-an-action-vb.md)</span></span>
