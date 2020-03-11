---
uid: web-forms/overview/ajax-control-toolkit/getting-started/creating-a-custom-ajax-control-toolkit-control-extender-vb
title: カスタム AJAX Control Toolkit コントロールエクステンダーを作成する (VB) |Microsoft Docs
author: microsoft
description: カスタムエクステンダーを使用すると、新しいクラスを作成しなくても、ASP.NET コントロールの機能をカスタマイズおよび拡張できます。
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 18b29834-c991-4e0c-b533-44d358fbfc9c
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/creating-a-custom-ajax-control-toolkit-control-extender-vb
msc.type: authoredcontent
ms.openlocfilehash: 0849fa6c13679e0cd01bb20a4067a097acbce298
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78466864"
---
# <a name="creating-a-custom-ajax-control-toolkit-control-extender-vb"></a><span data-ttu-id="0a668-103">カスタム AJAX Control Toolkit コントロール エクステンダーを作成する (VB)</span><span class="sxs-lookup"><span data-stu-id="0a668-103">Creating a Custom AJAX Control Toolkit Control Extender (VB)</span></span>

<span data-ttu-id="0a668-104">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="0a668-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="0a668-105">カスタムエクステンダーを使用すると、新しいクラスを作成しなくても、ASP.NET コントロールの機能をカスタマイズおよび拡張できます。</span><span class="sxs-lookup"><span data-stu-id="0a668-105">Custom Extenders enable you to customize and extend the capabilities of ASP.NET controls without having to create new classes.</span></span>

<span data-ttu-id="0a668-106">このチュートリアルでは、カスタム AJAX Control Toolkit コントロールエクステンダーを作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="0a668-106">In this tutorial, you learn how to create a custom AJAX Control Toolkit control extender.</span></span> <span data-ttu-id="0a668-107">テキストをテキストボックスに入力するときに、ボタンの状態を無効から有効に変更する、シンプルで便利な新しいエクステンダーを作成します。</span><span class="sxs-lookup"><span data-stu-id="0a668-107">We create a simple, but useful, new extender that changes the state of a Button from disabled to enabled when you type text into a TextBox.</span></span> <span data-ttu-id="0a668-108">このチュートリアルを読み終えると、独自の制御エクステンダーを使用して ASP.NET AJAX Toolkit を拡張できるようになります。</span><span class="sxs-lookup"><span data-stu-id="0a668-108">After reading this tutorial, you will be able to extend the ASP.NET AJAX Toolkit with your own control extenders.</span></span>

<span data-ttu-id="0a668-109">Visual Studio または Visual Web Developer を使用して、カスタムコントロールエクステンダーを作成できます (最新バージョンの Visual Web Developer があることを確認してください)。</span><span class="sxs-lookup"><span data-stu-id="0a668-109">You can create custom control extenders using either Visual Studio or Visual Web Developer (make sure that you have the latest version of Visual Web Developer).</span></span>

## <a name="overview-of-the-disabledbutton-extender"></a><span data-ttu-id="0a668-110">DisabledButton Extender の概要</span><span class="sxs-lookup"><span data-stu-id="0a668-110">Overview of the DisabledButton Extender</span></span>

<span data-ttu-id="0a668-111">新しいコントロールエクステンダーには、DisabledButton extender という名前が付けられています。</span><span class="sxs-lookup"><span data-stu-id="0a668-111">Our new control extender is named the DisabledButton extender.</span></span> <span data-ttu-id="0a668-112">このエクステンダーには、次の3つのプロパティがあります。</span><span class="sxs-lookup"><span data-stu-id="0a668-112">This extender will have three properties:</span></span>

- <span data-ttu-id="0a668-113">TargetControlID-コントロールが拡張するテキストボックス。</span><span class="sxs-lookup"><span data-stu-id="0a668-113">TargetControlID - The TextBox that the control extends.</span></span>
- <span data-ttu-id="0a668-114">TargetButtonIID-無効または有効になっているボタン。</span><span class="sxs-lookup"><span data-stu-id="0a668-114">TargetButtonIID - The Button that is disabled or enabled.</span></span>
- <span data-ttu-id="0a668-115">DisabledText-ボタンに最初に表示されるテキスト。</span><span class="sxs-lookup"><span data-stu-id="0a668-115">DisabledText - The text that is initially displayed in the Button.</span></span> <span data-ttu-id="0a668-116">入力を開始すると、ボタンの [テキスト] プロパティの値が表示されます。</span><span class="sxs-lookup"><span data-stu-id="0a668-116">When you start typing, the Button displays the value of the Button Text property.</span></span>

<span data-ttu-id="0a668-117">DisabledButton extender を TextBox コントロールと Button コントロールにフックします。</span><span class="sxs-lookup"><span data-stu-id="0a668-117">You hook the DisabledButton extender to a TextBox and Button control.</span></span> <span data-ttu-id="0a668-118">テキストを入力する前に、ボタンは無効になり、テキストボックスとボタンは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="0a668-118">Before you type any text, the Button is disabled and the TextBox and Button look like this:</span></span>

[![](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image2.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image1.png)

<span data-ttu-id="0a668-119">([クリックすると、フルサイズの画像が表示](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image3.png)される)</span><span class="sxs-lookup"><span data-stu-id="0a668-119">([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image3.png))</span></span>

<span data-ttu-id="0a668-120">テキストの入力を開始すると、ボタンが有効になり、テキストボックスとボタンは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="0a668-120">After you start typing text, the Button is enabled and the TextBox and Button look like this:</span></span>

[![](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image5.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image4.png)

<span data-ttu-id="0a668-121">([クリックすると、フルサイズの画像が表示](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image6.png)される)</span><span class="sxs-lookup"><span data-stu-id="0a668-121">([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image6.png))</span></span>

<span data-ttu-id="0a668-122">コントロールエクステンダーを作成するには、次の3つのファイルを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0a668-122">To create our control extender, we need to create the following three files:</span></span>

- <span data-ttu-id="0a668-123">DisabledButtonExtender-このファイルは、エクステンダーの作成を管理し、デザイン時にプロパティを設定できるサーバー側のコントロールクラスです。</span><span class="sxs-lookup"><span data-stu-id="0a668-123">DisabledButtonExtender.vb - This file is the server-side control class that will manage creating your extender and allow you to set the properties at design-time.</span></span> <span data-ttu-id="0a668-124">また、extender で設定できるプロパティも定義されています。</span><span class="sxs-lookup"><span data-stu-id="0a668-124">It also defines the properties that can be set on your extender.</span></span> <span data-ttu-id="0a668-125">これらのプロパティは、コードからアクセスでき、デザイン時に、DisableButtonBehavior .js ファイルで定義されているプロパティと一致します。</span><span class="sxs-lookup"><span data-stu-id="0a668-125">These properties are accessible via code and at design time and match properties defined in the DisableButtonBehavior.js file.</span></span>
- <span data-ttu-id="0a668-126">DisabledButtonBehavior--このファイルは、すべてのクライアントスクリプトロジックを追加する場所です。</span><span class="sxs-lookup"><span data-stu-id="0a668-126">DisabledButtonBehavior.js -- This file is where you will add all of your client script logic.</span></span>
- <span data-ttu-id="0a668-127">DisabledButtonDesigner-このクラスを使用すると、デザイン時の機能が有効になります。</span><span class="sxs-lookup"><span data-stu-id="0a668-127">DisabledButtonDesigner.vb - This class enables design-time functionality.</span></span> <span data-ttu-id="0a668-128">このクラスは、コントロールエクステンダーが Visual Studio/Visual Web Developer Designer で正しく動作するようにする場合に必要です。</span><span class="sxs-lookup"><span data-stu-id="0a668-128">You need this class if you want the control extender to work correctly with the Visual Studio/Visual Web Developer Designer.</span></span>

<span data-ttu-id="0a668-129">したがって、制御エクステンダーは、サーバー側のコントロール、クライアント側の動作、およびサーバー側のデザイナークラスで構成されます。</span><span class="sxs-lookup"><span data-stu-id="0a668-129">So a control extender consists of a server-side control, a client-side behavior, and a server-side designer class.</span></span> <span data-ttu-id="0a668-130">これら3つのファイルをすべて作成する方法については、次のセクションで説明します。</span><span class="sxs-lookup"><span data-stu-id="0a668-130">You learn how to create all three of these files in the following sections.</span></span>

## <a name="creating-the-custom-extender-website-and-project"></a><span data-ttu-id="0a668-131">カスタム Extender Web サイトおよびプロジェクトの作成</span><span class="sxs-lookup"><span data-stu-id="0a668-131">Creating the Custom Extender Website and Project</span></span>

<span data-ttu-id="0a668-132">最初の手順は、Visual Studio/Visual Web Developer でクラスライブラリプロジェクトと web サイトを作成することです。</span><span class="sxs-lookup"><span data-stu-id="0a668-132">The first step is to create a class library project and website in Visual Studio/Visual Web Developer.</span></span> <span data-ttu-id="0a668-133">クラスライブラリプロジェクトにカスタムエクステンダーを作成し、web サイトでカスタムエクステンダーをテストします。</span><span class="sxs-lookup"><span data-stu-id="0a668-133">We�ll create the custom extender in the class library project and test the custom extender in the website.</span></span>

<span data-ttu-id="0a668-134">Web サイトから始めましょう。</span><span class="sxs-lookup"><span data-stu-id="0a668-134">Let�s start with the website.</span></span> <span data-ttu-id="0a668-135">Web サイトを作成するには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="0a668-135">Follow these steps to create the website:</span></span>

1. <span data-ttu-id="0a668-136">メニューオプションファイル **[新しい Web サイト]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="0a668-136">Select the menu option **File, New Web Site**.</span></span>
2. <span data-ttu-id="0a668-137">**ASP.NET Web サイト**テンプレートを選択します。</span><span class="sxs-lookup"><span data-stu-id="0a668-137">Select the **ASP.NET Web Site** template.</span></span>
3. <span data-ttu-id="0a668-138">新しい web サイトに*Website1*という名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="0a668-138">Name the new website *Website1*.</span></span>
4. <span data-ttu-id="0a668-139">**[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="0a668-139">Click the **OK** button.</span></span>

<span data-ttu-id="0a668-140">次に、コントロールエクステンダーのコードを含むクラスライブラリプロジェクトを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0a668-140">Next, we need to create the class library project that will contain the code for the control extender:</span></span>

1. <span data-ttu-id="0a668-141">メニューオプション**ファイル、[追加]、[新しいプロジェクト**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="0a668-141">Select the menu option **File, Add, New Project**.</span></span>
2. <span data-ttu-id="0a668-142">**[クラスライブラリ]** テンプレートを選択します。</span><span class="sxs-lookup"><span data-stu-id="0a668-142">Select the **Class Library** template.</span></span>
3. <span data-ttu-id="0a668-143">新しいクラスライブラリに「 **Customextenders**」という名前を付けます。</span><span class="sxs-lookup"><span data-stu-id="0a668-143">Name the new class library with the name **CustomExtenders**.</span></span>
4. <span data-ttu-id="0a668-144">**[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="0a668-144">Click the **OK** button.</span></span>

<span data-ttu-id="0a668-145">これらの手順を完了すると、ソリューションエクスプローラーウィンドウは図1のようになります。</span><span class="sxs-lookup"><span data-stu-id="0a668-145">After you complete these steps, your Solution Explorer window should look like Figure 1.</span></span>

<span data-ttu-id="0a668-146">[web サイトおよびクラスライブラリプロジェクトを使用したソリューションの ![](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image8.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="0a668-146">[![Solution with website and class library project](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image8.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image7.png)</span></span>

<span data-ttu-id="0a668-147">**図 01**: web サイトおよびクラスライブラリプロジェクトを使用したソリューション ([クリックすると、フルサイズの画像が表示](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image9.png)されます)</span><span class="sxs-lookup"><span data-stu-id="0a668-147">**Figure 01**: Solution with website and class library project([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image9.png))</span></span>

<span data-ttu-id="0a668-148">次に、必要なすべてのアセンブリ参照をクラスライブラリプロジェクトに追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0a668-148">Next, you need to add all of the necessary assembly references to the class library project:</span></span>

1. <span data-ttu-id="0a668-149">CustomExtenders プロジェクトを右クリックし、 **[参照の追加]** メニューオプションを選択します。</span><span class="sxs-lookup"><span data-stu-id="0a668-149">Right-click the CustomExtenders project and select the menu option **Add Reference**.</span></span>
2. <span data-ttu-id="0a668-150">[.NET] タブを選択します。</span><span class="sxs-lookup"><span data-stu-id="0a668-150">Select the .NET tab.</span></span>
3. <span data-ttu-id="0a668-151">次のアセンブリへの参照を追加します。</span><span class="sxs-lookup"><span data-stu-id="0a668-151">Add references to the following assemblies:</span></span>

    1. <span data-ttu-id="0a668-152">System.Web.dll</span><span class="sxs-lookup"><span data-stu-id="0a668-152">System.Web.dll</span></span>
    2. <span data-ttu-id="0a668-153">System.Web.Extensions.dll</span><span class="sxs-lookup"><span data-stu-id="0a668-153">System.Web.Extensions.dll</span></span>
    3. <span data-ttu-id="0a668-154">System.Design.dll</span><span class="sxs-lookup"><span data-stu-id="0a668-154">System.Design.dll</span></span>
    4. <span data-ttu-id="0a668-155">System.Web.Extensions.Design.dll</span><span class="sxs-lookup"><span data-stu-id="0a668-155">System.Web.Extensions.Design.dll</span></span>
4. <span data-ttu-id="0a668-156">[参照] タブを選択します。</span><span class="sxs-lookup"><span data-stu-id="0a668-156">Select the Browse tab.</span></span>
5. <span data-ttu-id="0a668-157">AjaxControlToolkit アセンブリへの参照を追加します。</span><span class="sxs-lookup"><span data-stu-id="0a668-157">Add a reference to the AjaxControlToolkit.dll assembly.</span></span> <span data-ttu-id="0a668-158">このアセンブリは、AJAX Control Toolkit をダウンロードしたフォルダーにあります。</span><span class="sxs-lookup"><span data-stu-id="0a668-158">This assembly is located in the folder where you downloaded the AJAX Control Toolkit.</span></span>

<span data-ttu-id="0a668-159">プロジェクトを右クリックし、[プロパティ] をクリックして、[参照] タブをクリックすると、右の参照がすべて追加されていることを確認できます (図2を参照)。</span><span class="sxs-lookup"><span data-stu-id="0a668-159">You can verify that you have added all of the right references by right-clicking your project, selecting Properties, and clicking the References tab (see Figure 2).</span></span>

<span data-ttu-id="0a668-160">[必要な参照を含む ![参照フォルダー](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image11.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="0a668-160">[![References folder with required references](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image11.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image10.png)</span></span>

<span data-ttu-id="0a668-161">**図 02**: 必要な参照を含むフォルダー[を参照する (クリックすると、フルサイズの画像が表示](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image12.png)される)</span><span class="sxs-lookup"><span data-stu-id="0a668-161">**Figure 02**: References folder with required references([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image12.png))</span></span>

## <a name="creating-the-custom-control-extender"></a><span data-ttu-id="0a668-162">カスタムコントロールエクステンダーの作成</span><span class="sxs-lookup"><span data-stu-id="0a668-162">Creating the Custom Control Extender</span></span>

<span data-ttu-id="0a668-163">これでクラスライブラリが用意されたので、extender コントロールの構築を開始できます。</span><span class="sxs-lookup"><span data-stu-id="0a668-163">Now that we have our class library, we can start building our extender control.</span></span> <span data-ttu-id="0a668-164">では、カスタムエクステンダーコントロールクラスのベアボーンから始めましょう (リスト1を参照)。</span><span class="sxs-lookup"><span data-stu-id="0a668-164">Let�s start with the bare bones of a custom extender control class (see Listing 1).</span></span>

<span data-ttu-id="0a668-165">**リスト 1-MyCustomExtender .vb**</span><span class="sxs-lookup"><span data-stu-id="0a668-165">**Listing 1 - MyCustomExtender.vb**</span></span>

[!code-vb[Main](creating-a-custom-ajax-control-toolkit-control-extender-vb/samples/sample1.vb)]

<span data-ttu-id="0a668-166">リスト1のコントロールエクステンダークラスに関しては、いくつかの点に注意してください。</span><span class="sxs-lookup"><span data-stu-id="0a668-166">There are several things that you notice about the control extender class in Listing 1.</span></span> <span data-ttu-id="0a668-167">まず、クラスが base ExtenderControlBase クラスから継承されていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="0a668-167">First, notice that the class inherits from the base ExtenderControlBase class.</span></span> <span data-ttu-id="0a668-168">すべての AJAX コントロールツールキットエクステンダーコントロールは、この基本クラスから派生します。</span><span class="sxs-lookup"><span data-stu-id="0a668-168">All AJAX Control Toolkit extender controls derive from this base class.</span></span> <span data-ttu-id="0a668-169">たとえば、基本クラスには、すべてのコントロールエクステンダーの必須プロパティである TargetID プロパティが含まれています。</span><span class="sxs-lookup"><span data-stu-id="0a668-169">For example, the base class includes the TargetID property that is a required property of every control extender.</span></span>

<span data-ttu-id="0a668-170">次に、クラスには、クライアントスクリプトに関連する次の2つの属性が含まれていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="0a668-170">Next, notice that the class includes the following two attributes related to client script:</span></span>

- <span data-ttu-id="0a668-171">Webresource.axd-アセンブリに埋め込みリソースとしてファイルを含めます。</span><span class="sxs-lookup"><span data-stu-id="0a668-171">WebResource - Causes a file to be included as an embedded resource in an assembly.</span></span>
- <span data-ttu-id="0a668-172">ClientScriptResource-アセンブリからスクリプトリソースを取得します。</span><span class="sxs-lookup"><span data-stu-id="0a668-172">ClientScriptResource - Causes a script resource to be retrieved from an assembly.</span></span>

<span data-ttu-id="0a668-173">Webresource.axd 属性は、カスタムエクステンダーをコンパイルするときに、MyControlBehavior の JavaScript ファイルをアセンブリに埋め込むために使用されます。</span><span class="sxs-lookup"><span data-stu-id="0a668-173">The WebResource attribute is used to embed the MyControlBehavior.js JavaScript file into the assembly when the custom extender is compiled.</span></span> <span data-ttu-id="0a668-174">ClientScriptResource 属性は、カスタム extender が web ページで使用されている場合に、アセンブリから MyControlBehavior .js スクリプトを取得するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="0a668-174">The ClientScriptResource attribute is used to retrieve the MyControlBehavior.js script from the assembly when the custom extender is used in a web page.</span></span>

<span data-ttu-id="0a668-175">Webresource.axd および ClientScriptResource 属性を機能させるには、JavaScript ファイルを埋め込みリソースとしてコンパイルする必要があります。</span><span class="sxs-lookup"><span data-stu-id="0a668-175">In order for the WebResource and ClientScriptResource attributes to work, you must compile the JavaScript file as an embedded resource.</span></span> <span data-ttu-id="0a668-176">ソリューションエクスプローラーウィンドウでファイルを選択し、プロパティシートを開いて、"*埋め込みリソース*" という値を **[ビルドアクション]** プロパティに割り当てます。</span><span class="sxs-lookup"><span data-stu-id="0a668-176">Select the file in the Solution Explorer window, open the property sheet, and assign the value *Embedded Resource* to the **Build Action** property.</span></span>

<span data-ttu-id="0a668-177">コントロールエクステンダーにも TargetControlType 属性が含まれていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="0a668-177">Notice that the control extender also includes a TargetControlType attribute.</span></span> <span data-ttu-id="0a668-178">この属性は、コントロールエクステンダーによって拡張されるコントロールの種類を指定するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="0a668-178">This attribute is used to specify the type of control that is extended by the control extender.</span></span> <span data-ttu-id="0a668-179">リスト1の場合は、コントロールエクステンダーを使用してテキストボックスを拡張します。</span><span class="sxs-lookup"><span data-stu-id="0a668-179">In the case of Listing 1, the control extender is used to extend a TextBox.</span></span>

<span data-ttu-id="0a668-180">最後に、カスタムエクステンダーに T.myproperty という名前のプロパティが含まれていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="0a668-180">Finally, notice that the custom extender includes a property named MyProperty.</span></span> <span data-ttu-id="0a668-181">プロパティは、ExtenderControlProperty 属性でマークされています。</span><span class="sxs-lookup"><span data-stu-id="0a668-181">The property is marked with the ExtenderControlProperty attribute.</span></span> <span data-ttu-id="0a668-182">GetPropertyValue () メソッドと SetPropertyValue () メソッドは、プロパティ値をサーバー側のコントロールエクステンダーからクライアント側の動作に渡すために使用されます。</span><span class="sxs-lookup"><span data-stu-id="0a668-182">The GetPropertyValue() and SetPropertyValue() methods are used to pass the property value from the server-side control extender to the client-side behavior.</span></span>

<span data-ttu-id="0a668-183">では、DisabledButton extender のコードを実装してみましょう。</span><span class="sxs-lookup"><span data-stu-id="0a668-183">Let�s go ahead and implement the code for our DisabledButton extender.</span></span> <span data-ttu-id="0a668-184">このエクステンダーのコードは、リスト2にあります。</span><span class="sxs-lookup"><span data-stu-id="0a668-184">The code for this extender can be found in Listing 2.</span></span>

<span data-ttu-id="0a668-185">**リスティング 2-DisabledButtonExtender**</span><span class="sxs-lookup"><span data-stu-id="0a668-185">**Listing 2 - DisabledButtonExtender.vb**</span></span>

[!code-vb[Main](creating-a-custom-ajax-control-toolkit-control-extender-vb/samples/sample2.vb)]

<span data-ttu-id="0a668-186">リスト2の DisabledButton extender には、TargetButtonID と DisabledText という2つのプロパティがあります。</span><span class="sxs-lookup"><span data-stu-id="0a668-186">The DisabledButton extender in Listing 2 has two properties named TargetButtonID and DisabledText.</span></span> <span data-ttu-id="0a668-187">TargetButtonID プロパティに適用された IDReferenceProperty では、ボタンコントロールの ID 以外のものをこのプロパティに割り当てることはできません。</span><span class="sxs-lookup"><span data-stu-id="0a668-187">The IDReferenceProperty applied to the TargetButtonID property prevents you from assigning anything other than the ID of a Button control to this property.</span></span>

<span data-ttu-id="0a668-188">Webresource.axd および ClientScriptResource 属性は、DisabledButtonBehavior という名前のファイルにあるクライアント側の動作をこのエクステンダーに関連付けます。</span><span class="sxs-lookup"><span data-stu-id="0a668-188">The WebResource and ClientScriptResource attributes associate a client-side behavior located in a file named DisabledButtonBehavior.js with this extender.</span></span> <span data-ttu-id="0a668-189">この JavaScript ファイルについては、次のセクションで説明します。</span><span class="sxs-lookup"><span data-stu-id="0a668-189">We discuss this JavaScript file in the next section.</span></span>

## <a name="creating-the-custom-extender-behavior"></a><span data-ttu-id="0a668-190">カスタム Extender 動作の作成</span><span class="sxs-lookup"><span data-stu-id="0a668-190">Creating the Custom Extender Behavior</span></span>

<span data-ttu-id="0a668-191">コントロールエクステンダーのクライアント側コンポーネントは、動作と呼ばれます。</span><span class="sxs-lookup"><span data-stu-id="0a668-191">The client-side component of a control extender is called a behavior.</span></span> <span data-ttu-id="0a668-192">ボタンを無効および有効にするための実際のロジックは、DisabledButton の動作に含まれています。</span><span class="sxs-lookup"><span data-stu-id="0a668-192">The actual logic for disabling and enabling the Button is contained in the DisabledButton behavior.</span></span> <span data-ttu-id="0a668-193">この動作の JavaScript コードは、リスト3に含まれています。</span><span class="sxs-lookup"><span data-stu-id="0a668-193">The JavaScript code for the behavior is included in Listing 3.</span></span>

<span data-ttu-id="0a668-194">**リスト 3-DisabledButton**</span><span class="sxs-lookup"><span data-stu-id="0a668-194">**Listing 3 - DisabledButton.js**</span></span>

[!code-javascript[Main](creating-a-custom-ajax-control-toolkit-control-extender-vb/samples/sample3.js)]

<span data-ttu-id="0a668-195">リスト3の JavaScript ファイルには、DisabledButtonBehavior という名前のクライアント側クラスが含まれています。</span><span class="sxs-lookup"><span data-stu-id="0a668-195">The JavaScript file in Listing 3 contains a client-side class named DisabledButtonBehavior.</span></span> <span data-ttu-id="0a668-196">このクラスには、サーバー側ツインと同様に、TargetButtonID と DisabledText という名前の2つのプロパティが含まれています。これは get\_TargetButtonID/set\_TargetButtonID を使用してアクセスでき、DisabledText/set\_DisabledText を取得\_ます。</span><span class="sxs-lookup"><span data-stu-id="0a668-196">This class, like its server-side twin, includes two properties named TargetButtonID and DisabledText which you can access using get\_TargetButtonID/set\_TargetButtonID and get\_DisabledText/set\_DisabledText.</span></span>

<span data-ttu-id="0a668-197">Initialize () メソッドは、keyup イベントハンドラーを動作の target 要素に関連付けます。</span><span class="sxs-lookup"><span data-stu-id="0a668-197">The initialize() method associates a keyup event handler with the target element for the behavior.</span></span> <span data-ttu-id="0a668-198">この動作に関連付けられているテキストボックスに文字を入力するたびに、keyup ハンドラーが実行されます。</span><span class="sxs-lookup"><span data-stu-id="0a668-198">Each time you type a letter into the TextBox associated with this behavior, the keyup handler executes.</span></span> <span data-ttu-id="0a668-199">Keyup ハンドラーは、ビヘイビアーに関連付けられたテキストボックスにテキストが含まれているかどうかに応じて、ボタンを有効または無効にします。</span><span class="sxs-lookup"><span data-stu-id="0a668-199">The keyup handler either enables or disables the Button depending on whether the TextBox associated with the behavior contains any text.</span></span>

<span data-ttu-id="0a668-200">リスト3の JavaScript ファイルを埋め込みリソースとしてコンパイルする必要があることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="0a668-200">Remember that you must compile the JavaScript file in Listing 3 as an embedded resource.</span></span> <span data-ttu-id="0a668-201">ソリューションエクスプローラーウィンドウでファイルを選択し、プロパティシートを開き、[値]*埋め込みリソース*を **[ビルドアクション]** プロパティに割り当てます (図3を参照)。</span><span class="sxs-lookup"><span data-stu-id="0a668-201">Select the file in the Solution Explorer window, open the property sheet, and assign the value *Embedded Resource* to the **Build Action** property (see Figure 3).</span></span> <span data-ttu-id="0a668-202">このオプションは、Visual Studio と Visual Web Developer の両方で使用できます。</span><span class="sxs-lookup"><span data-stu-id="0a668-202">This option is available in both Visual Studio and Visual Web Developer.</span></span>

<span data-ttu-id="0a668-203">[埋め込みリソースとして JavaScript ファイルを追加 ![には](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image14.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="0a668-203">[![Adding a JavaScript file as an embedded resource](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image14.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image13.png)</span></span>

<span data-ttu-id="0a668-204">**図 03**: JavaScript ファイルを埋め込みリソースとして追加する ([クリックすると、フルサイズの画像が表示](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image15.png)されます)</span><span class="sxs-lookup"><span data-stu-id="0a668-204">**Figure 03**: Adding a JavaScript file as an embedded resource([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image15.png))</span></span>

## <a name="creating-the-custom-extender-designer"></a><span data-ttu-id="0a668-205">カスタムエクステンダーデザイナーの作成</span><span class="sxs-lookup"><span data-stu-id="0a668-205">Creating the Custom Extender Designer</span></span>

<span data-ttu-id="0a668-206">Extender を完成させるために作成する必要がある最後のクラスが1つあります。</span><span class="sxs-lookup"><span data-stu-id="0a668-206">There is one last class that we need to create to complete our extender.</span></span> <span data-ttu-id="0a668-207">リスト4でデザイナークラスを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0a668-207">We need to create the designer class in Listing 4.</span></span> <span data-ttu-id="0a668-208">このクラスは、extender が Visual Studio/Visual Web Developer デザイナーで正しく動作するようにするために必要です。</span><span class="sxs-lookup"><span data-stu-id="0a668-208">This class is required to make the extender behave correctly with the Visual Studio/Visual Web Developer Designer.</span></span>

<span data-ttu-id="0a668-209">**リスト 4-DisabledButtonDesigner**</span><span class="sxs-lookup"><span data-stu-id="0a668-209">**Listing 4 - DisabledButtonDesigner.vb**</span></span>

[!code-vb[Main](creating-a-custom-ajax-control-toolkit-control-extender-vb/samples/sample4.vb)]

<span data-ttu-id="0a668-210">デザイナー属性を使用して、リスト4のデザイナーと DisabledButton extender を関連付けます。次のように、デザイナー属性を DisabledButtonExtender クラスに適用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0a668-210">You associate the designer in Listing 4 with the DisabledButton extender with the Designer attribute.You need to apply the Designer attribute to the DisabledButtonExtender class like this:</span></span>

[!code-vb[Main](creating-a-custom-ajax-control-toolkit-control-extender-vb/samples/sample5.vb)]

## <a name="using-the-custom-extender"></a><span data-ttu-id="0a668-211">カスタム Extender の使用</span><span class="sxs-lookup"><span data-stu-id="0a668-211">Using the Custom Extender</span></span>

<span data-ttu-id="0a668-212">DisabledButton control extender の作成が終了したので、ASP.NET の web サイトで使用します。</span><span class="sxs-lookup"><span data-stu-id="0a668-212">Now that we have finished creating the DisabledButton control extender, it is time to use it in our ASP.NET website.</span></span> <span data-ttu-id="0a668-213">まず、カスタムエクステンダーをツールボックスに追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0a668-213">First, we need to add the custom extender to the toolbox.</span></span> <span data-ttu-id="0a668-214">次の手順に従います。</span><span class="sxs-lookup"><span data-stu-id="0a668-214">Follow these steps:</span></span>

1. <span data-ttu-id="0a668-215">[ソリューションエクスプローラー] ウィンドウでページをダブルクリックして、ASP.NET ページを開きます。</span><span class="sxs-lookup"><span data-stu-id="0a668-215">Open an ASP.NET page by double-clicking the page in the Solution Explorer window.</span></span>
2. <span data-ttu-id="0a668-216">ツールボックスを右クリックし、[項目の**選択**] メニューオプションを選択します。</span><span class="sxs-lookup"><span data-stu-id="0a668-216">Right-click the toolbox and select the menu option **Choose Items**.</span></span>
3. <span data-ttu-id="0a668-217">[ツールボックスアイテムの選択] ダイアログで、CustomExtenders .dll アセンブリを参照します。</span><span class="sxs-lookup"><span data-stu-id="0a668-217">In the Choose Toolbox Items dialog, browse to the CustomExtenders.dll assembly.</span></span>
4. <span data-ttu-id="0a668-218">**[OK]** ボタンをクリックして、ダイアログを閉じます。</span><span class="sxs-lookup"><span data-stu-id="0a668-218">Click the **OK** button to close the dialog.</span></span>

<span data-ttu-id="0a668-219">これらの手順を完了すると、DisabledButton コントロールエクステンダーがツールボックスに表示されます (図4を参照)。</span><span class="sxs-lookup"><span data-stu-id="0a668-219">After you complete these steps, the DisabledButton control extender should appear in the toolbox (see Figure 4).</span></span>

<span data-ttu-id="0a668-220">[ツールボックスの ![DisabledButton](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image17.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image16.png)</span><span class="sxs-lookup"><span data-stu-id="0a668-220">[![DisabledButton in the toolbox](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image17.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image16.png)</span></span>

<span data-ttu-id="0a668-221">**図 04**: ツールボックスの DisabledButton ([クリックすると、フルサイズの画像が表示](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image18.png)されます)</span><span class="sxs-lookup"><span data-stu-id="0a668-221">**Figure 04**: DisabledButton in the toolbox([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image18.png))</span></span>

<span data-ttu-id="0a668-222">次に、新しい ASP.NET ページを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0a668-222">Next, we need to create a new ASP.NET page.</span></span> <span data-ttu-id="0a668-223">次の手順に従います。</span><span class="sxs-lookup"><span data-stu-id="0a668-223">Follow these steps:</span></span>

1. <span data-ttu-id="0a668-224">ShowDisabledButton という名前の新しい ASP.NET ページを作成します。</span><span class="sxs-lookup"><span data-stu-id="0a668-224">Create a new ASP.NET page named ShowDisabledButton.aspx.</span></span>
2. <span data-ttu-id="0a668-225">ScriptManager をページにドラッグします。</span><span class="sxs-lookup"><span data-stu-id="0a668-225">Drag a ScriptManager onto the page.</span></span>
3. <span data-ttu-id="0a668-226">TextBox コントロールをページにドラッグします。</span><span class="sxs-lookup"><span data-stu-id="0a668-226">Drag a TextBox control onto the page.</span></span>
4. <span data-ttu-id="0a668-227">ボタンコントロールをページにドラッグします。</span><span class="sxs-lookup"><span data-stu-id="0a668-227">Drag a Button control onto the page.</span></span>
5. <span data-ttu-id="0a668-228">プロパティウィンドウで、[ボタン ID] プロパティを「 <em>Btnsave</em> 」の値に、Text プロパティを「 *save\** 」の値に変更します。</span><span class="sxs-lookup"><span data-stu-id="0a668-228">In the Properties window, change the Button ID property to the value <em>btnSave</em> and the Text property to the value *Save\**.</span></span>

<span data-ttu-id="0a668-229">標準の ASP.NET TextBox と Button コントロールを使用してページを作成しました。</span><span class="sxs-lookup"><span data-stu-id="0a668-229">We created a page with a standard ASP.NET TextBox and Button control.</span></span>

<span data-ttu-id="0a668-230">次に、DisabledButton extender を使用して TextBox コントロールを拡張する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0a668-230">Next, we need to extend the TextBox control with the DisabledButton extender:</span></span>

1. <span data-ttu-id="0a668-231">[拡張タスクの**追加**] オプションを選択して、extender ウィザードダイアログを開きます (図5を参照)。</span><span class="sxs-lookup"><span data-stu-id="0a668-231">Select the **Add Extender** task option to open the Extender Wizard dialog (see Figure 5).</span></span> <span data-ttu-id="0a668-232">このダイアログにはカスタム DisabledButton extender が含まれていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="0a668-232">Notice that the dialog includes our custom DisabledButton extender.</span></span>
2. <span data-ttu-id="0a668-233">DisabledButton extender を選択し、 **[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="0a668-233">Select the DisabledButton extender and click the **OK** button.</span></span>

<span data-ttu-id="0a668-234">[Extender ウィザードダイアログ ![](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image20.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image19.png)</span><span class="sxs-lookup"><span data-stu-id="0a668-234">[![The Extender Wizard dialog](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image20.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image19.png)</span></span>

<span data-ttu-id="0a668-235">**図 05**: エクステンダーウィザードダイアログ ([クリックしてフルサイズのイメージを表示](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image21.png))</span><span class="sxs-lookup"><span data-stu-id="0a668-235">**Figure 05**: The Extender Wizard dialog([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image21.png))</span></span>

<span data-ttu-id="0a668-236">最後に、DisabledButton extender のプロパティを設定できます。</span><span class="sxs-lookup"><span data-stu-id="0a668-236">Finally, we can set the properties of the DisabledButton extender.</span></span> <span data-ttu-id="0a668-237">TextBox コントロールのプロパティを変更することで、DisabledButton extender のプロパティを変更できます。</span><span class="sxs-lookup"><span data-stu-id="0a668-237">You can modify the properties of the DisabledButton extender by modifying the properties of the TextBox control:</span></span>

1. <span data-ttu-id="0a668-238">デザイナーでテキストボックスを選択します。</span><span class="sxs-lookup"><span data-stu-id="0a668-238">Select the TextBox in the Designer.</span></span>
2. <span data-ttu-id="0a668-239">プロパティウィンドウで、[Extender] ノードを展開します (図6を参照)。</span><span class="sxs-lookup"><span data-stu-id="0a668-239">In the Properties window, expand the Extenders node (see Figure 6).</span></span>
3. <span data-ttu-id="0a668-240">値*save*を DisabledText プロパティに割り当て、値*Btnsave*を TargetButtonID プロパティに割り当てます。</span><span class="sxs-lookup"><span data-stu-id="0a668-240">Assign the value *Save* to the DisabledText property and the value *btnSave* to the TargetButtonID property.</span></span>

<span data-ttu-id="0a668-241">[extender プロパティの設定 ![](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image23.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image22.png)</span><span class="sxs-lookup"><span data-stu-id="0a668-241">[![Setting extender properties](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image23.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image22.png)</span></span>

<span data-ttu-id="0a668-242">**図 06**: extender のプロパティの設定 ([クリックすると、フルサイズの画像が表示](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image24.png)される)</span><span class="sxs-lookup"><span data-stu-id="0a668-242">**Figure 06**: Setting extender properties([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image24.png))</span></span>

<span data-ttu-id="0a668-243">F5 キーを押してページを実行すると、ボタンコントロールは最初は無効になります。</span><span class="sxs-lookup"><span data-stu-id="0a668-243">When you run the page (by hitting F5), the Button control is initially disabled.</span></span> <span data-ttu-id="0a668-244">テキストボックスへの入力を開始するとすぐに、ボタンコントロールが有効になります (図7を参照)。</span><span class="sxs-lookup"><span data-stu-id="0a668-244">As soon as you start entering text into the TextBox, the Button control is enabled (see Figure 7).</span></span>

<span data-ttu-id="0a668-245">[DisabledButton extender の動作の ![](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image26.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image25.png)</span><span class="sxs-lookup"><span data-stu-id="0a668-245">[![The DisabledButton extender in action](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image26.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image25.png)</span></span>

<span data-ttu-id="0a668-246">**図 07**: DisabledButton extender の動作 ([クリックすると、フルサイズの画像が表示](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image27.png)されます)</span><span class="sxs-lookup"><span data-stu-id="0a668-246">**Figure 07**: The DisabledButton extender in action([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image27.png))</span></span>

## <a name="summary"></a><span data-ttu-id="0a668-247">まとめ</span><span class="sxs-lookup"><span data-stu-id="0a668-247">Summary</span></span>

<span data-ttu-id="0a668-248">このチュートリアルの目的は、カスタム extender コントロールを使用して AJAX Control Toolkit を拡張する方法を説明することでした。</span><span class="sxs-lookup"><span data-stu-id="0a668-248">The goal of this tutorial was to explain how you can extend the AJAX Control Toolkit with custom extender controls.</span></span> <span data-ttu-id="0a668-249">このチュートリアルでは、単純な DisabledButton 制御エクステンダーを作成しました。</span><span class="sxs-lookup"><span data-stu-id="0a668-249">In this tutorial, we created a simple DisabledButton control extender.</span></span> <span data-ttu-id="0a668-250">このエクステンダーは、DisabledButtonExtender クラス、DisabledButtonBehavior JavaScript の動作、および DisabledButtonDesigner クラスを作成することによって実装されています。</span><span class="sxs-lookup"><span data-stu-id="0a668-250">We implemented this extender by creating a DisabledButtonExtender class, a DisabledButtonBehavior JavaScript behavior, and a DisabledButtonDesigner class.</span></span> <span data-ttu-id="0a668-251">カスタムコントロールエクステンダーを作成するたびに、同様の一連の手順に従います。</span><span class="sxs-lookup"><span data-stu-id="0a668-251">You follow a similar set of steps whenever you create a custom control extender.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="0a668-252">[[戻る]](using-ajax-control-toolkit-controls-and-control-extenders-vb.md)</span><span class="sxs-lookup"><span data-stu-id="0a668-252">[Previous](using-ajax-control-toolkit-controls-and-control-extenders-vb.md)</span></span>
