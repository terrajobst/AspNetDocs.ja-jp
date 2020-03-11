---
uid: web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-vb
title: AJAX Control Toolkit コントロールとコントロールエクステンダーの使用 (VB) |Microsoft Docs
author: microsoft
description: AJAX Control Toolkit のコントロールとエクステンダーを ASP.NET ページに追加する方法について説明します。
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 763650a9-ffde-46a9-b779-7a9145dd5d88
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-vb
msc.type: authoredcontent
ms.openlocfilehash: 90a6003ff50ba6e85196c25cf175e057810f0f84
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78497050"
---
# <a name="using-ajax-control-toolkit-controls-and-control-extenders-vb"></a><span data-ttu-id="59648-103">AJAX Control Toolkit のコントロールとコントロール エクステンダーを使用する (VB)</span><span class="sxs-lookup"><span data-stu-id="59648-103">Using AJAX Control Toolkit Controls and Control Extenders (VB)</span></span>

<span data-ttu-id="59648-104">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="59648-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="59648-105">AJAX Control Toolkit のコントロールとエクステンダーを ASP.NET ページに追加する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="59648-105">Learn how to add AJAX Control Toolkit controls and extenders to your ASP.NET pages.</span></span>

<span data-ttu-id="59648-106">AJAX Control Toolkit には、一連のコントロールとコントロールエクステンダーが含まれています。</span><span class="sxs-lookup"><span data-stu-id="59648-106">The AJAX Control Toolkit contains a set of controls and control extenders.</span></span> <span data-ttu-id="59648-107">この簡単なチュートリアルでは、ASP.NET ページにコントロールとコントロールエクステンダーの両方を追加する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="59648-107">In this brief tutorial, you learn how to add both controls and control extenders to an ASP.NET page.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="59648-108">Ajax コントロールツールキットをインストールし、Visual Studio/Visual Web Developer ツールボックスに AJAX Control Toolkit を追加する方法については、「チュートリアル- [Ajax Control toolkit の概要](get-started-with-the-ajax-control-toolkit-vb.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="59648-108">For instructions on installing the AJAX Control Toolkit and adding the AJAX Control Toolkit to the Visual Studio/Visual Web Developer toolbox, see the tutorial [Get Started with the AJAX Control Toolkit](get-started-with-the-ajax-control-toolkit-vb.md).</span></span>

## <a name="using-ajax-control-toolkit-controls"></a><span data-ttu-id="59648-109">AJAX コントロールツールキットコントロールの使用</span><span class="sxs-lookup"><span data-stu-id="59648-109">Using AJAX Control Toolkit Controls</span></span>

<span data-ttu-id="59648-110">AJAX コントロールツールキットコントロールは、通常の ASP.NET コントロールと同様に動作します。</span><span class="sxs-lookup"><span data-stu-id="59648-110">An AJAX Control Toolkit control works just like a normal ASP.NET control.</span></span> <span data-ttu-id="59648-111">ツールボックスから ASP.NET ページにコントロールをドラッグできます。</span><span class="sxs-lookup"><span data-stu-id="59648-111">You can drag the control from the toolbox onto an ASP.NET page.</span></span> <span data-ttu-id="59648-112">コントロールは、デザインビューまたはソースビューのいずれかのページに追加できます。</span><span class="sxs-lookup"><span data-stu-id="59648-112">You can add the control to the page in either Design view or Source view.</span></span>

<span data-ttu-id="59648-113">AJAX Control Toolkit のコントロールを使用する場合は、特別な要件が1つあります。</span><span class="sxs-lookup"><span data-stu-id="59648-113">There is one special requirement when using the controls from the AJAX Control Toolkit.</span></span> <span data-ttu-id="59648-114">ページに ScriptManager コントロールが含まれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="59648-114">The page must contain a ScriptManager control.</span></span> <span data-ttu-id="59648-115">ScriptManager コントロールは、AJAX コントロールツールキットコントロールに必要なすべての JavaScript を含めることを担当します。</span><span class="sxs-lookup"><span data-stu-id="59648-115">The ScriptManager control is responsible for including all of the necessary JavaScript required by the AJAX Control Toolkit controls.</span></span>

<span data-ttu-id="59648-116">たとえば、AJAX コントロールツールキットタブには、エディターコントロールという名前のコントロールが含まれています。</span><span class="sxs-lookup"><span data-stu-id="59648-116">For example, the AJAX Control Toolkit tab includes a control named the Editor control.</span></span> <span data-ttu-id="59648-117">このコントロールは、リッチ HTML エディターを表示します。</span><span class="sxs-lookup"><span data-stu-id="59648-117">This control displays a rich HTML editor.</span></span> <span data-ttu-id="59648-118">次の手順に従って、エディターコントロールをページに追加します。</span><span class="sxs-lookup"><span data-stu-id="59648-118">Follow these steps to add the Editor control to a page:</span></span>

1. <span data-ttu-id="59648-119">ShowEditor という名前の新しい ASP.NET ページを作成します。</span><span class="sxs-lookup"><span data-stu-id="59648-119">Create a new ASP.NET page named ShowEditor.aspx</span></span>
2. <span data-ttu-id="59648-120">[ツールボックス] の [AJAX 拡張] タブの下にある ScriptManager コントロールを選択し、コントロールをページにドラッグします。</span><span class="sxs-lookup"><span data-stu-id="59648-120">Select the ScriptManager control from beneath the AJAX Extensions tab in the toolbox and drag the control onto the page.</span></span>
3. <span data-ttu-id="59648-121">ツールボックスの [AJAX Control Toolkit] タブの下にあるエディターコントロールを選択し、コントロールをページにドラッグします (図1を参照)。</span><span class="sxs-lookup"><span data-stu-id="59648-121">Select the Editor control from beneath the AJAX Control Toolkit tab in the toolbox and drag the control onto the page (see Figure 1).</span></span> <span data-ttu-id="59648-122">デザイナーは図2のようになります。</span><span class="sxs-lookup"><span data-stu-id="59648-122">The Designer should look like Figure 2.</span></span>
4. <span data-ttu-id="59648-123">メニューオプション [デバッグ]、[デバッグの**開始**] の順に選択するか、F5 キーを押して、web サイトを実行します。</span><span class="sxs-lookup"><span data-stu-id="59648-123">Run the web site by selecting the menu option **Debug, Start Debugging** or hitting the F5 key.</span></span>
5. <span data-ttu-id="59648-124">図3のページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="59648-124">You should see the page in Figure 3.</span></span>

<span data-ttu-id="59648-125">[HTML エディターコントロールを選択 ![には](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image1.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="59648-125">[![Selecting the HTML Editor control](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image1.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image1.png)</span></span>

<span data-ttu-id="59648-126">**図 01**: HTML エディターコントロールを選択[する (クリックすると、フルサイズのイメージが表示](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image2.png)されます)</span><span class="sxs-lookup"><span data-stu-id="59648-126">**Figure 01**: Selecting the HTML Editor control([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image2.png))</span></span>

<span data-ttu-id="59648-127">[ScriptManager コントロールとエディットコントロールを使用した Visual Studio デザイナーの ![](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image2.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="59648-127">[![Visual Studio Designer with ScriptManager and Edit control](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image2.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image3.png)</span></span>

<span data-ttu-id="59648-128">**図 02**: ScriptManager コントロールとエディットコントロールを使用した Visual Studio デザイナー ([クリックすると、フルサイズのイメージが表示](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image4.png)されます)</span><span class="sxs-lookup"><span data-stu-id="59648-128">**Figure 02**: Visual Studio Designer with ScriptManager and Edit control([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image4.png))</span></span>

<span data-ttu-id="59648-129">[DisplayEditor .aspx ページを ![する](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image3.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="59648-129">[![The DisplayEditor.aspx page](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image3.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image5.png)</span></span>

<span data-ttu-id="59648-130">**図 03**: displayeditor .aspx ページ ([クリックしてフルサイズのイメージを表示](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="59648-130">**Figure 03**: The DisplayEditor.aspx page([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image6.png))</span></span>

## <a name="using-ajax-control-toolkit-control-extenders"></a><span data-ttu-id="59648-131">AJAX Control Toolkit コントロールエクステンダーの使用</span><span class="sxs-lookup"><span data-stu-id="59648-131">Using AJAX Control Toolkit Control Extenders</span></span>

<span data-ttu-id="59648-132">AJAX コントロールツールキットには、コントロールエクステンダーも含まれています。</span><span class="sxs-lookup"><span data-stu-id="59648-132">The AJAX Control Toolkit also contains control extenders.</span></span> <span data-ttu-id="59648-133">名前が示すように、コントロールエクステンダーは既存のコントロールの機能を拡張します。</span><span class="sxs-lookup"><span data-stu-id="59648-133">As its name suggests, a control extender extends the functionality of an existing control.</span></span> <span data-ttu-id="59648-134">たとえば、ConfirmButton コントロールエクステンダーは、標準の ASP.NET Button コントロールを拡張します。</span><span class="sxs-lookup"><span data-stu-id="59648-134">For example, the ConfirmButton control extender extends the standard ASP.NET Button control.</span></span> <span data-ttu-id="59648-135">Extender はボタンコントロールの動作を変更し、ボタンをクリックしたときに確認ダイアログが表示されるようにします。</span><span class="sxs-lookup"><span data-stu-id="59648-135">The extender changes the Button control�s behavior so that the Button displays a confirmation dialog when you click it.</span></span>

<span data-ttu-id="59648-136">コントロールエクステンダーは、AJAX コントロールツールキットコントロールと同様に、ScriptManager コントロールを必要とします。</span><span class="sxs-lookup"><span data-stu-id="59648-136">A control extender, just like an AJAX Control Toolkit control, requires a ScriptManager control.</span></span> <span data-ttu-id="59648-137">ページでコントロールエクステンダーの使用を開始する前に、ScriptManager コントロールをページに追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="59648-137">You must add a ScriptManager control to a page before you start using control extenders in the page.</span></span>

<span data-ttu-id="59648-138">ConfirmButton コントロールエクステンダーを使用するには、次の手順に従います。</span><span class="sxs-lookup"><span data-stu-id="59648-138">Follow these steps to use the ConfirmButton control extender:</span></span>

1. <span data-ttu-id="59648-139">ShowConfirmButton .aspx という名前の新しい ASP.NET ページを作成します。</span><span class="sxs-lookup"><span data-stu-id="59648-139">Create a new ASP.NET page named ShowConfirmButton.aspx</span></span>
2. <span data-ttu-id="59648-140">[AJAX 拡張] タブの下にあるページにコントロールをドラッグして、ScriptManager コントロールをページに追加します。</span><span class="sxs-lookup"><span data-stu-id="59648-140">Add a ScriptManager control to the page by dragging the control onto the page from beneath the AJAX Extensions tab.</span></span>
3. <span data-ttu-id="59648-141">ツールボックスの [標準] タブの下にあるボタンをデザイナー画面にドラッグして、標準のボタンコントロールをページに追加します。</span><span class="sxs-lookup"><span data-stu-id="59648-141">Add a standard Button control to the page by dragging the Button from beneath the Standard tab in the toolbox onto the Designer surface.</span></span>
4. <span data-ttu-id="59648-142">[拡張タスクの**追加**] オプションをクリックします (図4を参照)。</span><span class="sxs-lookup"><span data-stu-id="59648-142">Click the **Add Extender** task option (see Figure 4).</span></span>
5. <span data-ttu-id="59648-143">[拡張の選択] ダイアログで、[ConfirmButtonExtender] を選択し (図5を参照)、[OK] ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="59648-143">In the Choose Extender dialog, select ConfirmButtonExtender (see Figure 5) and click the OK button.</span></span>
6. <span data-ttu-id="59648-144">デザイナーで Button コントロールを選択し、プロパティウィンドウの Extender、Button1\_ConfirmButtonExtender ノードの順に展開します (図6を参照)。</span><span class="sxs-lookup"><span data-stu-id="59648-144">Select the Button control in the Designer and expand the Extenders, Button1\_ConfirmButtonExtender node in the Properties window (see Figure 6).</span></span> <span data-ttu-id="59648-145">値を ConfirmText プロパティに*割り当てます。*</span><span class="sxs-lookup"><span data-stu-id="59648-145">Assign the value *�Really?�* to the ConfirmText property.</span></span>
7. <span data-ttu-id="59648-146">メニューオプション [**デバッグ]、[デバッグの開始**] の順に選択するか、F5 キーを押して、ページを実行します。</span><span class="sxs-lookup"><span data-stu-id="59648-146">Run the page by selecting the menu option **Debug, Start Debugging** or hit the F5 key.</span></span>

<span data-ttu-id="59648-147">[[拡張タスクの追加] オプションの ![](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image4.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="59648-147">[![The Add Extender task option](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image4.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image7.png)</span></span>

<span data-ttu-id="59648-148">**図 04**: [拡張タスクの追加] オプション ([クリックすると、フルサイズの画像が表示](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image8.png)されます)</span><span class="sxs-lookup"><span data-stu-id="59648-148">**Figure 04**: The Add Extender task option([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image8.png))</span></span>

<span data-ttu-id="59648-149">[ConfirmButton コントロールエクステンダーを選択 ![には](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image5.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="59648-149">[![Selecting the ConfirmButton control extender](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image5.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image9.png)</span></span>

<span data-ttu-id="59648-150">**図 05**: confirmbutton コントロールエクステンダーを選択[する (クリックすると、フルサイズのイメージが表示](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image10.png)されます)</span><span class="sxs-lookup"><span data-stu-id="59648-150">**Figure 05**: Selecting the ConfirmButton control extender([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image10.png))</span></span>

<span data-ttu-id="59648-151">[ConfirmButton プロパティの設定 ![](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image6.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="59648-151">[![Setting a ConfirmButton property](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image6.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image11.png)</span></span>

<span data-ttu-id="59648-152">**図 06**: confirmbutton プロパティの設定 ([クリックすると、フルサイズの画像が表示](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image12.png)される)</span><span class="sxs-lookup"><span data-stu-id="59648-152">**Figure 06**: Setting a ConfirmButton property([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image12.png))</span></span>

<span data-ttu-id="59648-153">ページが開くと、ボタンが表示されます。</span><span class="sxs-lookup"><span data-stu-id="59648-153">When the page opens, you should see a button.</span></span> <span data-ttu-id="59648-154">このボタンをクリックすると、図7の確認ダイアログが表示されます。</span><span class="sxs-lookup"><span data-stu-id="59648-154">When you click the button, you get the confirmation dialog in Figure 7.</span></span>

<span data-ttu-id="59648-155">[確認ダイアログを表示 ![には](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image7.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="59648-155">[![Displaying the confirmation dialog](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image7.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image13.png)</span></span>

<span data-ttu-id="59648-156">**図 07**: 確認ダイアログ[を表示する (クリックすると、フルサイズの画像が表示](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image14.png)されます)</span><span class="sxs-lookup"><span data-stu-id="59648-156">**Figure 07**: Displaying the confirmation dialog([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image14.png))</span></span>

<span data-ttu-id="59648-157">通常は、コントロールエクステンダーをページにドラッグしないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="59648-157">Notice that you normally do not drag a control extender onto a page.</span></span> <span data-ttu-id="59648-158">代わりに、[拡張タスクの**追加**] オプションを使用して、既にページに追加したコントロールに extender を追加します。</span><span class="sxs-lookup"><span data-stu-id="59648-158">Instead, you use the **Add Extender** task option to add an extender to a control that you have already added to a page.</span></span> <span data-ttu-id="59648-159">さらに、拡張されるコントロールのプロパティシートを開いて、コントロールエクステンダーのプロパティを設定することにも注意してください。</span><span class="sxs-lookup"><span data-stu-id="59648-159">Notice, furthermore, that you set control extender properties by opening the property sheet for the control being extended.</span></span>

<span data-ttu-id="59648-160">1つの ASP.NET コントロールは、複数のコントロールエクステンダーで拡張できます。</span><span class="sxs-lookup"><span data-stu-id="59648-160">A single ASP.NET control can be extended by multiple control extenders.</span></span> <span data-ttu-id="59648-161">拡張されるコントロールのプロパティシートには、コントロールに関連付けられているすべてのコントロールエクステンダーが一覧表示されます。</span><span class="sxs-lookup"><span data-stu-id="59648-161">The property sheet for the control being extended will list all of the control extenders associated with the control.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="59648-162">[前へ](get-started-with-the-ajax-control-toolkit-vb.md)
> [次へ](creating-a-custom-ajax-control-toolkit-control-extender-vb.md)</span><span class="sxs-lookup"><span data-stu-id="59648-162">[Previous](get-started-with-the-ajax-control-toolkit-vb.md)
[Next](creating-a-custom-ajax-control-toolkit-control-extender-vb.md)</span></span>
