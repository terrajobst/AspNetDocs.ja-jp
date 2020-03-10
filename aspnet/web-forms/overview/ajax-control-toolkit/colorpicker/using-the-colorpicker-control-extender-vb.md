---
uid: web-forms/overview/ajax-control-toolkit/colorpicker/using-the-colorpicker-control-extender-vb
title: ColorPicker コントロールエクステンダーを使用する (VB) |Microsoft Docs
author: microsoft
description: ColorPicker は ASP.NET AJAX extender で、クライアント側のカラー選択機能を UI と共にポップアップコントロールに提供します。 任意の ASP.NET にアタッチできます...
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 577ae07b-a872-4818-a804-bca489b40ad0
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/colorpicker/using-the-colorpicker-control-extender-vb
msc.type: authoredcontent
ms.openlocfilehash: 77e2e3bc61a5e1498570959ca40acff83dc3fc82
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78446584"
---
# <a name="using-the-colorpicker-control-extender-vb"></a><span data-ttu-id="b5b95-104">ColorPicker コントロールエクステンダーの使用 (VB)</span><span class="sxs-lookup"><span data-stu-id="b5b95-104">Using the ColorPicker Control Extender (VB)</span></span>

<span data-ttu-id="b5b95-105">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="b5b95-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="b5b95-106">ColorPicker は ASP.NET AJAX extender で、クライアント側のカラー選択機能を UI と共にポップアップコントロールに提供します。</span><span class="sxs-lookup"><span data-stu-id="b5b95-106">ColorPicker is an ASP.NET AJAX extender that provides client-side color-picking functionality with UI in a popup control.</span></span> <span data-ttu-id="b5b95-107">任意の ASP.NET TextBox コントロールにアタッチできます。</span><span class="sxs-lookup"><span data-stu-id="b5b95-107">It can be attached to any ASP.NET TextBox control.</span></span> <span data-ttu-id="b5b95-108">し.</span><span class="sxs-lookup"><span data-stu-id="b5b95-108">It.</span></span>

<span data-ttu-id="b5b95-109">このチュートリアルの目的は、AJAX Control Toolkit ColorPicker コントロールエクステンダーの使用方法について説明することです。</span><span class="sxs-lookup"><span data-stu-id="b5b95-109">The goal of this tutorial is to explain how you can use the AJAX Control Toolkit ColorPicker control extender.</span></span> <span data-ttu-id="b5b95-110">ColorPicker コントロールエクステンダーには、色を選択できるポップアップダイアログが表示されます。</span><span class="sxs-lookup"><span data-stu-id="b5b95-110">The ColorPicker control extender displays a popup dialog that enables you to select a color.</span></span> <span data-ttu-id="b5b95-111">ColorPicker は、ユーザーが色を選択するための直感的なユーザーインターフェイスを提供する場合に便利です。</span><span class="sxs-lookup"><span data-stu-id="b5b95-111">The ColorPicker is useful whenever you want to provide an intuitive user interface for a user to pick a color.</span></span>

## <a name="extending-a-textbox-control-with-the-colorpicker-control-extender"></a><span data-ttu-id="b5b95-112">ColorPicker コントロールエクステンダーを使用した TextBox コントロールの拡張</span><span class="sxs-lookup"><span data-stu-id="b5b95-112">Extending a TextBox Control with the ColorPicker Control Extender</span></span>

<span data-ttu-id="b5b95-113">たとえば、訪問者がカスタマイズした名刺を作成できるようにする web サイトを作成する場合を考えてみましょう。</span><span class="sxs-lookup"><span data-stu-id="b5b95-113">Imagine, for example, that you want to create a website that enables visitors to create customized business cards.</span></span> <span data-ttu-id="b5b95-114">訪問者は、名刺のテキストを入力し、色を選択できます。</span><span class="sxs-lookup"><span data-stu-id="b5b95-114">Visitors can enter the text for a business card and pick the color.</span></span> <span data-ttu-id="b5b95-115">リスト1の ASP.NET ページには、txtCardText および Txtcardtext という名前の2つのテキストボックスコントロールが含まれています。</span><span class="sxs-lookup"><span data-stu-id="b5b95-115">The ASP.NET page in Listing 1 contains two TextBox controls named txtCardText and txtCardColor.</span></span> <span data-ttu-id="b5b95-116">フォームを送信すると、選択した値が表示されます (図1を参照)。</span><span class="sxs-lookup"><span data-stu-id="b5b95-116">When you submit the form, the selected values are displayed (see Figure 1).</span></span>

<span data-ttu-id="b5b95-117">[名刺を作成するためのシンプルなフォーム ![](using-the-colorpicker-control-extender-vb/_static/image1.jpg)](using-the-colorpicker-control-extender-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="b5b95-117">[![Simple form for creating a business card](using-the-colorpicker-control-extender-vb/_static/image1.jpg)](using-the-colorpicker-control-extender-vb/_static/image1.png)</span></span>

<span data-ttu-id="b5b95-118">**図 01**: 名刺を作成するための単純なフォーム ([クリックすると、フルサイズの画像が表示](using-the-colorpicker-control-extender-vb/_static/image2.png)される)</span><span class="sxs-lookup"><span data-stu-id="b5b95-118">**Figure 01**: Simple form for creating a business card ([Click to view full-size image](using-the-colorpicker-control-extender-vb/_static/image2.png))</span></span>

<span data-ttu-id="b5b95-119">**リスト 1-CreateCard**</span><span class="sxs-lookup"><span data-stu-id="b5b95-119">**Listing 1 - CreateCard.aspx**</span></span>

[!code-aspx[Main](using-the-colorpicker-control-extender-vb/samples/sample1.aspx)]

<span data-ttu-id="b5b95-120">リスト1のフォームは機能しますが、優れたユーザーエクスペリエンスは提供されません。</span><span class="sxs-lookup"><span data-stu-id="b5b95-120">The form in Listing 1 works, but it does not provide a great user experience.</span></span> <span data-ttu-id="b5b95-121">ユーザーは、テキストボックスに色を入力する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b5b95-121">The user has to type a color into the textbox.</span></span> <span data-ttu-id="b5b95-122">ユーザーが特殊な色を必要とする場合 (たとえば、.pea が緑である場合など)、ユーザーはヘルプを表示せずに HTML カラーコードを確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b5b95-122">If the user wants a specialized color - for example, just the right shade of pea green - then the user must figure out the HTML color code without any help.</span></span>

<span data-ttu-id="b5b95-123">ColorPicker コントロールエクステンダーを使用すると、より優れたユーザーエクスペリエンスを作成できます。</span><span class="sxs-lookup"><span data-stu-id="b5b95-123">You can use the ColorPicker control extender to create a better user experience.</span></span> <span data-ttu-id="b5b95-124">ColorPicker は、テキストボックスコントロールにフォーカスを移動すると、色のダイアログボックスを表示します (図2を参照)。</span><span class="sxs-lookup"><span data-stu-id="b5b95-124">The ColorPicker displays a color dialog when you move focus to a TextBox control (see Figure 2).</span></span>

<span data-ttu-id="b5b95-125">[ColorPicker コントロールエクステンダーの ![](using-the-colorpicker-control-extender-vb/_static/image2.jpg)](using-the-colorpicker-control-extender-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="b5b95-125">[![The ColorPicker Control Extender](using-the-colorpicker-control-extender-vb/_static/image2.jpg)](using-the-colorpicker-control-extender-vb/_static/image3.png)</span></span>

<span data-ttu-id="b5b95-126">**図 02**: Colorpicker コントロールエクステンダー ([クリックすると、フルサイズの画像が表示](using-the-colorpicker-control-extender-vb/_static/image4.png)されます)</span><span class="sxs-lookup"><span data-stu-id="b5b95-126">**Figure 02**: The ColorPicker Control Extender ([Click to view full-size image](using-the-colorpicker-control-extender-vb/_static/image4.png))</span></span>

<span data-ttu-id="b5b95-127">次の2つの手順を実行して、リスト1のフォームと共に ColorPicker コントロールエクステンダーを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b5b95-127">You need to complete two steps to use the ColorPicker control extender with the form in Listing 1:</span></span>

1. <span data-ttu-id="b5b95-128">ScriptManager コントロールをページに追加する</span><span class="sxs-lookup"><span data-stu-id="b5b95-128">Add a ScriptManager control to the page</span></span>
2. <span data-ttu-id="b5b95-129">ColorPicker コントロールエクステンダーをページに追加します。</span><span class="sxs-lookup"><span data-stu-id="b5b95-129">Add the ColorPicker control extender to the page</span></span>

<span data-ttu-id="b5b95-130">ColorPicker を使用する前に、ScriptManager をページに追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b5b95-130">Before you can use the ColorPicker, you must add a ScriptManager to your page.</span></span> <span data-ttu-id="b5b95-131">ScriptManager を追加するには、サーバー側の &lt;フォーム&gt; タグのすぐ下に配置することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="b5b95-131">A good place to add the ScriptManager is right below the opening server-side &lt;form&gt; tag.</span></span> <span data-ttu-id="b5b95-132">ScriptManager コントロールは、ツールボックスからページにドラッグできます (ScriptManager は [AJAX 拡張] タブの下にあります)。</span><span class="sxs-lookup"><span data-stu-id="b5b95-132">You can drag the ScriptManager onto the page from the toolbox (the ScriptManager is located under the AJAX Extensions tab).</span></span> <span data-ttu-id="b5b95-133">または、[サーバー側フォームの開始] タグの下に、ソースビューに次のタグを入力します。</span><span class="sxs-lookup"><span data-stu-id="b5b95-133">Alternatively, you can type the following tag into Source View beneath the opening server-side form tag:</span></span>

<span data-ttu-id="b5b95-134">&lt;asp: ScriptManager ID = "ScriptManager1" runat = "server"/&gt;</span><span class="sxs-lookup"><span data-stu-id="b5b95-134">&lt;asp:ScriptManager ID="ScriptManager1" runat="server" /&gt;</span></span>

<span data-ttu-id="b5b95-135">ページに ColorPicker コントロールエクステンダーを追加する最も簡単な方法は、デザインビューです。</span><span class="sxs-lookup"><span data-stu-id="b5b95-135">The easiest way to add the ColorPicker control extender to the page is in Design View.</span></span> <span data-ttu-id="b5b95-136">[TxtCardColor] ボックスの上にマウスポインターを置くと、スマートタスクオプションが表示され、extender を追加できます (図3を参照)。</span><span class="sxs-lookup"><span data-stu-id="b5b95-136">If you hover your mouse over the txtCardColor TextBox, a smart task option appears the enables you to add an extender (see Figure 3).</span></span> <span data-ttu-id="b5b95-137">このオプションを選択すると、拡張ウィザードが表示されます (図4を参照)。</span><span class="sxs-lookup"><span data-stu-id="b5b95-137">If you pick this option, the Extender Wizard appears (see Figure 4).</span></span>

<span data-ttu-id="b5b95-138">[extender の追加 ![](using-the-colorpicker-control-extender-vb/_static/image3.jpg)](using-the-colorpicker-control-extender-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="b5b95-138">[![Adding an extender](using-the-colorpicker-control-extender-vb/_static/image3.jpg)](using-the-colorpicker-control-extender-vb/_static/image5.png)</span></span>

<span data-ttu-id="b5b95-139">**図 03**: エクステンダーを追加[する (クリックすると、フルサイズの画像が表示](using-the-colorpicker-control-extender-vb/_static/image6.png)されます)</span><span class="sxs-lookup"><span data-stu-id="b5b95-139">**Figure 03**: Adding an extender ([Click to view full-size image](using-the-colorpicker-control-extender-vb/_static/image6.png))</span></span>

<span data-ttu-id="b5b95-140">[エクステンダーウィザードを使用してコントロールエクステンダーを選択 ![には](using-the-colorpicker-control-extender-vb/_static/image4.jpg)](using-the-colorpicker-control-extender-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="b5b95-140">[![Selecting a control extender with the Extender Wizard](using-the-colorpicker-control-extender-vb/_static/image4.jpg)](using-the-colorpicker-control-extender-vb/_static/image7.png)</span></span>

<span data-ttu-id="b5b95-141">**図 04**: エクステンダーウィザードを使用してコントロールエクステンダーを選択[する (クリックすると、フルサイズの画像が表示](using-the-colorpicker-control-extender-vb/_static/image8.png)されます)</span><span class="sxs-lookup"><span data-stu-id="b5b95-141">**Figure 04**: Selecting a control extender with the Extender Wizard ([Click to view full-size image](using-the-colorpicker-control-extender-vb/_static/image8.png))</span></span>

<span data-ttu-id="b5b95-142">ColorPicker エクステンダーを選択すると、ColorPicker extender を使用して txtCardColor テキストボックスを拡張できます。</span><span class="sxs-lookup"><span data-stu-id="b5b95-142">You can pick the ColorPicker extender to extend the txtCardColor TextBox with the ColorPicker extender.</span></span> <span data-ttu-id="b5b95-143">[OK] をクリックしてダイアログ ボックスを閉じます。</span><span class="sxs-lookup"><span data-stu-id="b5b95-143">Click OK to close the dialog.</span></span>

<span data-ttu-id="b5b95-144">これらの変更を行った後、ページのソースはリスト2のようになります。</span><span class="sxs-lookup"><span data-stu-id="b5b95-144">After you make these changes, the source for the page looks like Listing 2.</span></span>

<span data-ttu-id="b5b95-145">**リスト 2-CreateCard (ColorPicker 付き)**</span><span class="sxs-lookup"><span data-stu-id="b5b95-145">**Listing 2 - CreateCard.aspx (with ColorPicker)**</span></span>

[!code-aspx[Main](using-the-colorpicker-control-extender-vb/samples/sample2.aspx)]

<span data-ttu-id="b5b95-146">ページに、txtCardColor TextBox コントロールのすぐ下に表示される ColorPickerExtender コントロールが含まれていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="b5b95-146">Notice that the page now contains a ColorPickerExtender control that appears directly below the txtCardColor TextBox control.</span></span> <span data-ttu-id="b5b95-147">ColorPickerExtender コントロールは、txtCardColor コントロールを拡張して、カラーピッカーダイアログを表示します。</span><span class="sxs-lookup"><span data-stu-id="b5b95-147">The ColorPickerExtender control extends the txtCardColor control so that it displays a color picker dialog.</span></span>

## <a name="using-a-button-to-launch-the-color-picker-dialog"></a><span data-ttu-id="b5b95-148">ボタンを使用してカラーピッカーダイアログを起動する</span><span class="sxs-lookup"><span data-stu-id="b5b95-148">Using a Button to Launch the Color Picker Dialog</span></span>

<span data-ttu-id="b5b95-149">ColorPicker エクステンダーでは、次のプロパティがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="b5b95-149">The ColorPicker extender supports the following properties:</span></span>

- <span data-ttu-id="b5b95-150">PopupButtonId-[カラーピッカー] ダイアログボックスが表示されるページ上のボタンの ID。</span><span class="sxs-lookup"><span data-stu-id="b5b95-150">PopupButtonId - The ID of a button on the page that causes the color picker dialog to appear.</span></span>
- <span data-ttu-id="b5b95-151">PopupPosition-カラーピッカーダイアログのターゲットコントロールを基準とした相対的な位置。</span><span class="sxs-lookup"><span data-stu-id="b5b95-151">PopupPosition - The position, relative to the target control, of the color picker dialog.</span></span> <span data-ttu-id="b5b95-152">指定できる値は、Absolute、Center、左下、右下、TopLeft、右、Right、Left (既定値は左下) です。</span><span class="sxs-lookup"><span data-stu-id="b5b95-152">Possible values are Absolute, Center, BottomLeft, BottomRight, TopLeft, TopRight, Right, and Left (the default is BottomLeft).</span></span>
- <span data-ttu-id="b5b95-153">SampleControlId-選択された色を表示するコントロールの ID。</span><span class="sxs-lookup"><span data-stu-id="b5b95-153">SampleControlId - The ID of a control that displays the selected color.</span></span>
- <span data-ttu-id="b5b95-154">SelectedColor-ColorPicker によって選択された初期色。</span><span class="sxs-lookup"><span data-stu-id="b5b95-154">SelectedColor - The initial color selected by the ColorPicker.</span></span>

<span data-ttu-id="b5b95-155">これらのプロパティを使用して、[色の選択] ダイアログの表示方法と、選択した色の表示方法をカスタマイズできます。</span><span class="sxs-lookup"><span data-stu-id="b5b95-155">You can use these properties to customize how the color picker dialog is displayed and how the selected color is displayed.</span></span> <span data-ttu-id="b5b95-156">リスト3のページは、これらのプロパティのいくつかを使用する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="b5b95-156">The page in Listing 3 illustrates how you can use several of these properties.</span></span>

<span data-ttu-id="b5b95-157">**リスト 3-Createcシャード .aspx**</span><span class="sxs-lookup"><span data-stu-id="b5b95-157">**Listing 3 - CreateCardButton.aspx**</span></span>

[!code-aspx[Main](using-the-colorpicker-control-extender-vb/samples/sample3.aspx)]

<span data-ttu-id="b5b95-158">リスト3のページには、[色の選択] ボタンがあります (図5を参照)。</span><span class="sxs-lookup"><span data-stu-id="b5b95-158">The page in Listing 3 includes a Pick Color button (see Figure 5).</span></span> <span data-ttu-id="b5b95-159">このボタンをクリックすると、[カラーピッカー] ダイアログがテキストボックスの上に表示されます。</span><span class="sxs-lookup"><span data-stu-id="b5b95-159">When you click this button, the color picker dialog appears above the TextBox.</span></span> <span data-ttu-id="b5b95-160">ダイアログから色を選択すると、選択した色が lblSample Label コントロールの背景色として表示されます。</span><span class="sxs-lookup"><span data-stu-id="b5b95-160">If you select a color from the dialog then the selected color appears as the background color of the lblSample Label control.</span></span>

<span data-ttu-id="b5b95-161">ColorPicker PopupButtonID プロパティは、[色の選択] ボタンを ColorPicker エクステンダーに関連付けるために使用されます。</span><span class="sxs-lookup"><span data-stu-id="b5b95-161">The ColorPicker PopupButtonID property is used to associate the Pick Color button with the ColorPicker extender.</span></span> <span data-ttu-id="b5b95-162">PopupButtonID プロパティの値を指定すると、対象のコントロールにフォーカスがあるときに [カラーピッカー] ダイアログボックスが表示されなくなります。</span><span class="sxs-lookup"><span data-stu-id="b5b95-162">When you supply a value for the PopupButtonID property, the color picker dialog no longer appears when the target control has focus.</span></span> <span data-ttu-id="b5b95-163">ダイアログを表示するには、このボタンをクリックする必要があります。</span><span class="sxs-lookup"><span data-stu-id="b5b95-163">You must click the button to display the dialog.</span></span>

<span data-ttu-id="b5b95-164">SampleControlID プロパティは、選択した色を表示するコントロールを ColorPicker に関連付けるために使用されます。</span><span class="sxs-lookup"><span data-stu-id="b5b95-164">The SampleControlID property is used to associate a control that displays the selected color with the ColorPicker.</span></span> <span data-ttu-id="b5b95-165">ColorPicker は、このコントロールの背景色を現在選択されている色に変更します。</span><span class="sxs-lookup"><span data-stu-id="b5b95-165">The ColorPicker changes the background color of this control to the currently selected color.</span></span>

<span data-ttu-id="b5b95-166">[ボタンを使用してカラーピッカーダイアログを表示 ![には](using-the-colorpicker-control-extender-vb/_static/image5.jpg)](using-the-colorpicker-control-extender-vb/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="b5b95-166">[![Displaying the color picker dialog with a button](using-the-colorpicker-control-extender-vb/_static/image5.jpg)](using-the-colorpicker-control-extender-vb/_static/image9.png)</span></span>

<span data-ttu-id="b5b95-167">**図 05**: ボタンを使用してカラーピッカーダイアログを表示[する (クリックすると、フルサイズの画像が表示](using-the-colorpicker-control-extender-vb/_static/image10.png)されます)</span><span class="sxs-lookup"><span data-stu-id="b5b95-167">**Figure 05**: Displaying the color picker dialog with a button ([Click to view full-size image](using-the-colorpicker-control-extender-vb/_static/image10.png))</span></span>

## <a name="summary"></a><span data-ttu-id="b5b95-168">まとめ</span><span class="sxs-lookup"><span data-stu-id="b5b95-168">Summary</span></span>

<span data-ttu-id="b5b95-169">このチュートリアルでは、ColorPicker コントロールエクステンダーを使用してポップアップカラーピッカーダイアログを表示する方法について学習しました。</span><span class="sxs-lookup"><span data-stu-id="b5b95-169">In this tutorial, you learned how to use the ColorPicker control extender to display a popup color picker dialog.</span></span> <span data-ttu-id="b5b95-170">まず、フォーカスが TextBox コントロールに移動したときにダイアログを表示する方法について説明しました。</span><span class="sxs-lookup"><span data-stu-id="b5b95-170">First, we examined how you can display the dialog when focus is moved to a TextBox control.</span></span> <span data-ttu-id="b5b95-171">次に、ボタンがクリックされたときに [カラーピッカー] ダイアログボックスを表示するボタンを作成する方法を学習しました。</span><span class="sxs-lookup"><span data-stu-id="b5b95-171">Next, you learned how to create a button that displays the color picker dialog when the button is clicked.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="b5b95-172">[[戻る]](using-the-colorpicker-control-extender-cs.md)</span><span class="sxs-lookup"><span data-stu-id="b5b95-172">[Previous](using-the-colorpicker-control-extender-cs.md)</span></span>
