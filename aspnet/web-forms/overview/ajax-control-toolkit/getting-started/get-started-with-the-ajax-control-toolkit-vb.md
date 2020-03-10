---
uid: web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-vb
title: AJAX Control Toolkit (VB) を使ってみる |Microsoft Docs
author: microsoft
description: AJAX Control Toolkit の使用を開始するために知っておく必要があることについて説明します。
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 9f8fa166-49a2-402c-b236-20caef0c658f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-vb
msc.type: authoredcontent
ms.openlocfilehash: ff614308555b31710b11f408e12e9a6fadbf98d0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78497140"
---
# <a name="get-started-with-the-ajax-control-toolkit-vb"></a><span data-ttu-id="14e73-103">AJAX Control Toolkit の概要 (VB)</span><span class="sxs-lookup"><span data-stu-id="14e73-103">Get Started with the AJAX Control Toolkit (VB)</span></span>

<span data-ttu-id="14e73-104">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="14e73-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="14e73-105">AJAX Control Toolkit の使用を開始するために知っておく必要があることについて説明します。</span><span class="sxs-lookup"><span data-stu-id="14e73-105">Learn all you need to know to get started using the AJAX Control Toolkit.</span></span>

<span data-ttu-id="14e73-106">AJAX Control Toolkit には、ASP.NET アプリケーションで使用できる30を超える無料のコントロールが含まれています。</span><span class="sxs-lookup"><span data-stu-id="14e73-106">The AJAX Control Toolkit contains more than 30 free controls that you can use in your ASP.NET applications.</span></span> <span data-ttu-id="14e73-107">このチュートリアルでは、AJAX Control Toolkit をダウンロードし、Visual Studio/Visual Web Developer Express ツールボックスにツールキットコントロールを追加する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="14e73-107">In this tutorial, you learn how to download the AJAX Control Toolkit and add the toolkit controls to your Visual Studio/Visual Web Developer Express toolbox.</span></span>

## <a name="downloading-the-ajax-control-toolkit"></a><span data-ttu-id="14e73-108">AJAX Control Toolkit のダウンロード</span><span class="sxs-lookup"><span data-stu-id="14e73-108">Downloading the AJAX Control Toolkit</span></span>

<span data-ttu-id="14e73-109">[AJAX Control Toolkit](http://devexpress.com/act)は、ASP.NET コミュニティと ASP.NET チームのメンバーによって開発されたオープンソースプロジェクトです。</span><span class="sxs-lookup"><span data-stu-id="14e73-109">The [AJAX Control Toolkit](http://devexpress.com/act) is an open source project developed by the members of the ASP.NET community and the ASP.NET team.</span></span>

<span data-ttu-id="14e73-110">[AJAX Control Toolkit のダウンロード ![](get-started-with-the-ajax-control-toolkit-vb/_static/image1.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="14e73-110">[![Downloading the AJAX Control Toolkit](get-started-with-the-ajax-control-toolkit-vb/_static/image1.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image1.png)</span></span>

<span data-ttu-id="14e73-111">**図 01**: AJAX コントロールツールキットをダウンロード[する (クリックすると、フルサイズのイメージが表示](get-started-with-the-ajax-control-toolkit-vb/_static/image2.png)されます)</span><span class="sxs-lookup"><span data-stu-id="14e73-111">**Figure 01**: Downloading the AJAX Control Toolkit([Click to view full-size image](get-started-with-the-ajax-control-toolkit-vb/_static/image2.png))</span></span>

<span data-ttu-id="14e73-112">ファイルをダウンロードしたら、ファイルのブロックを解除する必要があります。</span><span class="sxs-lookup"><span data-stu-id="14e73-112">After you download the file, you need to unblock the file.</span></span> <span data-ttu-id="14e73-113">ファイルを右クリックして プロパティ を選択し、**ブロック解除** ボタンをクリックします (図2を参照)。</span><span class="sxs-lookup"><span data-stu-id="14e73-113">Right-click the file, select Properties, and click the **Unblock** button (see Figure 2).</span></span>

<span data-ttu-id="14e73-114">[AJAX Control Toolkit ZIP ファイルのブロックを解除 ![](get-started-with-the-ajax-control-toolkit-vb/_static/image2.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="14e73-114">[![Unblocking the AJAX Control Toolkit ZIP file](get-started-with-the-ajax-control-toolkit-vb/_static/image2.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image3.png)</span></span>

<span data-ttu-id="14e73-115">**図 02**: AJAX コントロールツールキットの ZIP ファイルのブロック解除 ([クリックすると、フルサイズのイメージが表示](get-started-with-the-ajax-control-toolkit-vb/_static/image4.png)されます)</span><span class="sxs-lookup"><span data-stu-id="14e73-115">**Figure 02**: Unblocking the AJAX Control Toolkit ZIP file([Click to view full-size image](get-started-with-the-ajax-control-toolkit-vb/_static/image4.png))</span></span>

<span data-ttu-id="14e73-116">ファイルのブロックを解除した後、ファイルを右クリックして **[すべて展開]** メニューオプションを選択すると、ファイルを解凍できます。</span><span class="sxs-lookup"><span data-stu-id="14e73-116">After you unblock the file, you can unzip the file: Right-click the file and select the **Extract All** menu option.</span></span> <span data-ttu-id="14e73-117">これで、ツールキットを Visual Studio/Visual Web Developer ツールボックスに追加する準備ができました。</span><span class="sxs-lookup"><span data-stu-id="14e73-117">Now, we are ready to add the toolkit to the Visual Studio/Visual Web Developer toolbox.</span></span>

## <a name="adding-the-ajax-control-toolkit-to-the-toolbox"></a><span data-ttu-id="14e73-118">ツールボックスへの AJAX コントロールツールキットの追加</span><span class="sxs-lookup"><span data-stu-id="14e73-118">Adding the AJAX Control Toolkit to the Toolbox</span></span>

<span data-ttu-id="14e73-119">AJAX コントロールツールキットを使用する最も簡単な方法は、ツールキットを Visual Studio/Visual Web Developer ツールボックスに追加することです (図3を参照)。</span><span class="sxs-lookup"><span data-stu-id="14e73-119">The easiest way to use the AJAX Control Toolkit is to add the toolkit to your Visual Studio/Visual Web Developer toolbox (see Figure 3).</span></span> <span data-ttu-id="14e73-120">これにより、ツールキットコントロールを使用するときに、単にそのページにドラッグできるようになります。</span><span class="sxs-lookup"><span data-stu-id="14e73-120">That way, you can simply drag a toolkit control onto a page when you want to use it.</span></span>

<span data-ttu-id="14e73-121">[![AJAX コントロールツールキットがツールボックスに表示される](get-started-with-the-ajax-control-toolkit-vb/_static/image3.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="14e73-121">[![AJAX Control Toolkit appears in toolbox](get-started-with-the-ajax-control-toolkit-vb/_static/image3.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image5.png)</span></span>

<span data-ttu-id="14e73-122">**図 03**: AJAX コントロールツールキットがツールボックスに表示される ([クリックしてフルサイズのイメージを表示する](get-started-with-the-ajax-control-toolkit-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="14e73-122">**Figure 03**: AJAX Control Toolkit appears in toolbox([Click to view full-size image](get-started-with-the-ajax-control-toolkit-vb/_static/image6.png))</span></span>

<span data-ttu-id="14e73-123">まず、AJAX Control Toolkit タブをツールボックスに追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="14e73-123">First, you need to add an AJAX Control Toolkit tab to the toolbox.</span></span> <span data-ttu-id="14e73-124">次の手順に従います。</span><span class="sxs-lookup"><span data-stu-id="14e73-124">Follow these steps.</span></span>

1. <span data-ttu-id="14e73-125">新しい ASP.NET Web サイトを作成するには、メニューオプションファイル [新しい Web サイト] を選択します。</span><span class="sxs-lookup"><span data-stu-id="14e73-125">Create a new ASP.NET Website by selecting the menu option File, New Website.</span></span> <span data-ttu-id="14e73-126">[ソリューションエクスプローラー] ウィンドウで default.aspx をダブルクリックして、エディターでファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="14e73-126">Double-click the Default.aspx in the Solution Explorer window to open the file in the editor.</span></span>
2. <span data-ttu-id="14e73-127">全般 タブの下にあるツールボックスを右クリックし、メニューオプション **タブの追加** を選択します (図4を参照)。</span><span class="sxs-lookup"><span data-stu-id="14e73-127">Right-click the Toolbox beneath the General Tab and select the menu option **Add Tab** (see Figure 4).</span></span>
3. <span data-ttu-id="14e73-128">「AJAX Control Toolkit」という名前の新しいタブを入力します。</span><span class="sxs-lookup"><span data-stu-id="14e73-128">Enter a new tab named AJAX Control Toolkit.</span></span>

<span data-ttu-id="14e73-129">[新しいタブを追加 ![には](get-started-with-the-ajax-control-toolkit-vb/_static/image4.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="14e73-129">[![Adding a new tab](get-started-with-the-ajax-control-toolkit-vb/_static/image4.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image7.png)</span></span>

<span data-ttu-id="14e73-130">**図 04**: 新しいタブを追加[する (クリックすると、フルサイズの画像が表示](get-started-with-the-ajax-control-toolkit-vb/_static/image8.png)される)</span><span class="sxs-lookup"><span data-stu-id="14e73-130">**Figure 04**: Adding a new tab([Click to view full-size image](get-started-with-the-ajax-control-toolkit-vb/_static/image8.png))</span></span>

<span data-ttu-id="14e73-131">次に、AJAX Control Toolkit コントロールを新しいタブに追加する必要があります。次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="14e73-131">Next, you need to add the AJAX Control Toolkit controls to the new tab. Follow these steps:</span></span>

- <span data-ttu-id="14e73-132">[AJAX Control Toolkit] タブの下を右クリックし、[項目の選択] メニューオプションを選択します **(図5を参照)** 。</span><span class="sxs-lookup"><span data-stu-id="14e73-132">Right-click beneath the AJAX Control Toolkit tab and select the menu option **Choose Items (see Figure 5)**.</span></span>
- <span data-ttu-id="14e73-133">AJAX コントロールツールキットを解凍した場所を参照し、AjaxControlToolkit アセンブリを選択します。</span><span class="sxs-lookup"><span data-stu-id="14e73-133">Browse to the location where you unzipped the AJAX Control Toolkit and select the AjaxControlToolkit.dll assembly.</span></span>

<span data-ttu-id="14e73-134">[ツールボックスに追加する項目を選択 ![には](get-started-with-the-ajax-control-toolkit-vb/_static/image5.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="14e73-134">[![Choose items to add to the toolbox](get-started-with-the-ajax-control-toolkit-vb/_static/image5.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image9.png)</span></span>

<span data-ttu-id="14e73-135">**図 05**: ツールボックスに追加する項目を選択する ([クリックすると、フルサイズの画像が表示](get-started-with-the-ajax-control-toolkit-vb/_static/image10.png)されます)</span><span class="sxs-lookup"><span data-stu-id="14e73-135">**Figure 05**: Choose items to add to the toolbox([Click to view full-size image](get-started-with-the-ajax-control-toolkit-vb/_static/image10.png))</span></span>

<span data-ttu-id="14e73-136">これらの手順を完了すると、すべてのツールキットコントロールがツールボックスに表示されます。</span><span class="sxs-lookup"><span data-stu-id="14e73-136">After you complete these steps, all of the toolkit controls will appear in your toolbox.</span></span>

## <a name="upgrading-to-a-new-version-of-the-toolkit"></a><span data-ttu-id="14e73-137">新しいバージョンの Toolkit へのアップグレード</span><span class="sxs-lookup"><span data-stu-id="14e73-137">Upgrading to a New Version of the Toolkit</span></span>

<span data-ttu-id="14e73-138">以前のリリースの Toolkit を使用していて、今後のバージョンに移行する必要がある場合は、次の手順を実行することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="14e73-138">If you were using an older release of the Toolkit and now need to move to a later version here are the recommended steps:</span></span>

- <span data-ttu-id="14e73-139">バイナリ-web サイトの Bin フォルダーから古いバージョンの AjaxControlToolkit アセンブリを削除します。</span><span class="sxs-lookup"><span data-stu-id="14e73-139">Binaries - Delete the old version of the AjaxControlToolkit.dll assembly from your website Bin folder.</span></span>
- <span data-ttu-id="14e73-140">ツールボックスアイテム-AJAX Control Toolkit タブを削除し、上記の手順に従って、新しいバージョンの AjaxControlToolkit アセンブリを使用してタブを再作成します。</span><span class="sxs-lookup"><span data-stu-id="14e73-140">Toolbox Items - Delete the AJAX Control Toolkit tab and follow the steps above to re-create the tab with the new version of the AjaxControlToolkit.dll assembly.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="14e73-141">[前へ](creating-a-custom-ajax-control-toolkit-control-extender-cs.md)
> [次へ](using-ajax-control-toolkit-controls-and-control-extenders-vb.md)</span><span class="sxs-lookup"><span data-stu-id="14e73-141">[Previous](creating-a-custom-ajax-control-toolkit-control-extender-cs.md)
[Next](using-ajax-control-toolkit-controls-and-control-extenders-vb.md)</span></span>
