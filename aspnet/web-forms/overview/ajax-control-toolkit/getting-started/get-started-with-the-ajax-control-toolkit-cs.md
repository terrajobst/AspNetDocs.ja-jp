---
uid: web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-cs
title: AJAX Control Toolkit (C#) を使ってみる |Microsoft Docs
author: microsoft
description: AJAX Control Toolkit の使用を開始するために知っておく必要があることについて説明します。
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 16dc5c11-65be-4eae-a818-9fad7f8259c6
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-cs
msc.type: authoredcontent
ms.openlocfilehash: 7478b090ec52778572d70065983de6be8bdb4e6b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78504088"
---
# <a name="get-started-with-the-ajax-control-toolkit-c"></a><span data-ttu-id="c6631-103">AJAX Control Toolkit の概要 (C#)</span><span class="sxs-lookup"><span data-stu-id="c6631-103">Get Started with the AJAX Control Toolkit (C#)</span></span>

<span data-ttu-id="c6631-104">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="c6631-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="c6631-105">AJAX Control Toolkit の使用を開始するために知っておく必要があることについて説明します。</span><span class="sxs-lookup"><span data-stu-id="c6631-105">Learn all you need to know to get started using the AJAX Control Toolkit.</span></span>

<span data-ttu-id="c6631-106">AJAX Control Toolkit には、ASP.NET アプリケーションで使用できる30を超える無料のコントロールが含まれています。</span><span class="sxs-lookup"><span data-stu-id="c6631-106">The AJAX Control Toolkit contains more than 30 free controls that you can use in your ASP.NET applications.</span></span> <span data-ttu-id="c6631-107">このチュートリアルでは、AJAX Control Toolkit をダウンロードし、Visual Studio/Visual Web Developer Express ツールボックスにツールキットコントロールを追加する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="c6631-107">In this tutorial, you learn how to download the AJAX Control Toolkit and add the toolkit controls to your Visual Studio/Visual Web Developer Express toolbox.</span></span>

## <a name="downloading-the-ajax-control-toolkit"></a><span data-ttu-id="c6631-108">AJAX Control Toolkit のダウンロード</span><span class="sxs-lookup"><span data-stu-id="c6631-108">Downloading the AJAX Control Toolkit</span></span>

<span data-ttu-id="c6631-109">[AJAX Control Toolkit](http://devexpress.com/act)は、ASP.NET コミュニティと ASP.NET チームのメンバーによって開発されたオープンソースプロジェクトです。</span><span class="sxs-lookup"><span data-stu-id="c6631-109">The [AJAX Control Toolkit](http://devexpress.com/act) is an open source project developed by the members of the ASP.NET community and the ASP.NET team.</span></span> 

<span data-ttu-id="c6631-110">[AJAX Control Toolkit のダウンロード ![](get-started-with-the-ajax-control-toolkit-cs/_static/image1.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="c6631-110">[![Downloading the AJAX Control Toolkit](get-started-with-the-ajax-control-toolkit-cs/_static/image1.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image1.png)</span></span>

<span data-ttu-id="c6631-111">**図 01**: AJAX コントロールツールキットをダウンロード[する (クリックすると、フルサイズのイメージが表示](get-started-with-the-ajax-control-toolkit-cs/_static/image2.png)されます)</span><span class="sxs-lookup"><span data-stu-id="c6631-111">**Figure 01**: Downloading the AJAX Control Toolkit([Click to view full-size image](get-started-with-the-ajax-control-toolkit-cs/_static/image2.png))</span></span>

<span data-ttu-id="c6631-112">ファイルをダウンロードしたら、ファイルのブロックを解除する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c6631-112">After you download the file, you need to unblock the file.</span></span> <span data-ttu-id="c6631-113">ファイルを右クリックして プロパティ を選択し、**ブロック解除** ボタンをクリックします (図2を参照)。</span><span class="sxs-lookup"><span data-stu-id="c6631-113">Right-click the file, select Properties, and click the **Unblock** button (see Figure 2).</span></span>

<span data-ttu-id="c6631-114">[AJAX Control Toolkit ZIP ファイルのブロックを解除 ![](get-started-with-the-ajax-control-toolkit-cs/_static/image2.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="c6631-114">[![Unblocking the AJAX Control Toolkit ZIP file](get-started-with-the-ajax-control-toolkit-cs/_static/image2.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image3.png)</span></span>

<span data-ttu-id="c6631-115">**図 02**: AJAX コントロールツールキットの ZIP ファイルのブロック解除 ([クリックすると、フルサイズのイメージが表示](get-started-with-the-ajax-control-toolkit-cs/_static/image4.png)されます)</span><span class="sxs-lookup"><span data-stu-id="c6631-115">**Figure 02**: Unblocking the AJAX Control Toolkit ZIP file([Click to view full-size image](get-started-with-the-ajax-control-toolkit-cs/_static/image4.png))</span></span>

<span data-ttu-id="c6631-116">ファイルのブロックを解除した後、ファイルを右クリックして **[すべて展開]** メニューオプションを選択すると、ファイルを解凍できます。</span><span class="sxs-lookup"><span data-stu-id="c6631-116">After you unblock the file, you can unzip the file: Right-click the file and select the **Extract All** menu option.</span></span> <span data-ttu-id="c6631-117">これで、ツールキットを Visual Studio/Visual Web Developer ツールボックスに追加する準備ができました。</span><span class="sxs-lookup"><span data-stu-id="c6631-117">Now, we are ready to add the toolkit to the Visual Studio/Visual Web Developer toolbox.</span></span>

## <a name="adding-the-ajax-control-toolkit-to-the-toolbox"></a><span data-ttu-id="c6631-118">ツールボックスへの AJAX コントロールツールキットの追加</span><span class="sxs-lookup"><span data-stu-id="c6631-118">Adding the AJAX Control Toolkit to the Toolbox</span></span>

<span data-ttu-id="c6631-119">AJAX コントロールツールキットを使用する最も簡単な方法は、ツールキットを Visual Studio/Visual Web Developer ツールボックスに追加することです (図3を参照)。</span><span class="sxs-lookup"><span data-stu-id="c6631-119">The easiest way to use the AJAX Control Toolkit is to add the toolkit to your Visual Studio/Visual Web Developer toolbox (see Figure 3).</span></span> <span data-ttu-id="c6631-120">これにより、ツールキットコントロールを使用するときに、単にそのページにドラッグできるようになります。</span><span class="sxs-lookup"><span data-stu-id="c6631-120">That way, you can simply drag a toolkit control onto a page when you want to use it.</span></span>

<span data-ttu-id="c6631-121">[![AJAX コントロールツールキットがツールボックスに表示される](get-started-with-the-ajax-control-toolkit-cs/_static/image3.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="c6631-121">[![AJAX Control Toolkit appears in toolbox](get-started-with-the-ajax-control-toolkit-cs/_static/image3.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image5.png)</span></span>

<span data-ttu-id="c6631-122">**図 03**: AJAX コントロールツールキットがツールボックスに表示される ([クリックしてフルサイズのイメージを表示する](get-started-with-the-ajax-control-toolkit-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="c6631-122">**Figure 03**: AJAX Control Toolkit appears in toolbox([Click to view full-size image](get-started-with-the-ajax-control-toolkit-cs/_static/image6.png))</span></span>

<span data-ttu-id="c6631-123">まず、AJAX Control Toolkit タブをツールボックスに追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c6631-123">First, you need to add an AJAX Control Toolkit tab to the toolbox.</span></span> <span data-ttu-id="c6631-124">次の手順に従います。</span><span class="sxs-lookup"><span data-stu-id="c6631-124">Follow these steps.</span></span>

1. <span data-ttu-id="c6631-125">新しい ASP.NET Web サイトを作成するには、メニューオプションファイル [新しい Web サイト] を選択します。</span><span class="sxs-lookup"><span data-stu-id="c6631-125">Create a new ASP.NET Website by selecting the menu option File, New Website.</span></span> <span data-ttu-id="c6631-126">[ソリューションエクスプローラー] ウィンドウで default.aspx をダブルクリックして、エディターでファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="c6631-126">Double-click the Default.aspx in the Solution Explorer window to open the file in the editor.</span></span>
2. <span data-ttu-id="c6631-127">全般 タブの下にあるツールボックスを右クリックし、メニューオプション **タブの追加** を選択します (図4を参照)。</span><span class="sxs-lookup"><span data-stu-id="c6631-127">Right-click the Toolbox beneath the General Tab and select the menu option **Add Tab** (see Figure 4).</span></span>
3. <span data-ttu-id="c6631-128">「AJAX Control Toolkit」という名前の新しいタブを入力します。</span><span class="sxs-lookup"><span data-stu-id="c6631-128">Enter a new tab named AJAX Control Toolkit.</span></span>

<span data-ttu-id="c6631-129">[新しいタブを追加 ![には](get-started-with-the-ajax-control-toolkit-cs/_static/image4.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="c6631-129">[![Adding a new tab](get-started-with-the-ajax-control-toolkit-cs/_static/image4.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image7.png)</span></span>

<span data-ttu-id="c6631-130">**図 04**: 新しいタブを追加[する (クリックすると、フルサイズの画像が表示](get-started-with-the-ajax-control-toolkit-cs/_static/image8.png)される)</span><span class="sxs-lookup"><span data-stu-id="c6631-130">**Figure 04**: Adding a new tab([Click to view full-size image](get-started-with-the-ajax-control-toolkit-cs/_static/image8.png))</span></span>

<span data-ttu-id="c6631-131">次に、AJAX Control Toolkit コントロールを新しいタブに追加する必要があります。次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="c6631-131">Next, you need to add the AJAX Control Toolkit controls to the new tab. Follow these steps:</span></span>

- <span data-ttu-id="c6631-132">[AJAX Control Toolkit] タブの下を右クリックし、[項目の選択] メニューオプションを選択します **(図5を参照)** 。</span><span class="sxs-lookup"><span data-stu-id="c6631-132">Right-click beneath the AJAX Control Toolkit tab and select the menu option **Choose Items (see Figure 5)**.</span></span>
- <span data-ttu-id="c6631-133">AJAX コントロールツールキットを解凍した場所を参照し、AjaxControlToolkit アセンブリを選択します。</span><span class="sxs-lookup"><span data-stu-id="c6631-133">Browse to the location where you unzipped the AJAX Control Toolkit and select the AjaxControlToolkit.dll assembly.</span></span>

<span data-ttu-id="c6631-134">[ツールボックスに追加する項目を選択 ![には](get-started-with-the-ajax-control-toolkit-cs/_static/image5.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="c6631-134">[![Choose items to add to the toolbox](get-started-with-the-ajax-control-toolkit-cs/_static/image5.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image9.png)</span></span>

<span data-ttu-id="c6631-135">**図 05**: ツールボックスに追加する項目を選択する ([クリックすると、フルサイズの画像が表示](get-started-with-the-ajax-control-toolkit-cs/_static/image10.png)されます)</span><span class="sxs-lookup"><span data-stu-id="c6631-135">**Figure 05**: Choose items to add to the toolbox([Click to view full-size image](get-started-with-the-ajax-control-toolkit-cs/_static/image10.png))</span></span>

<span data-ttu-id="c6631-136">これらの手順を完了すると、すべてのツールキットコントロールがツールボックスに表示されます。</span><span class="sxs-lookup"><span data-stu-id="c6631-136">After you complete these steps, all of the toolkit controls will appear in your toolbox.</span></span>

## <a name="upgrading-to-a-new-version-of-the-toolkit"></a><span data-ttu-id="c6631-137">新しいバージョンの Toolkit へのアップグレード</span><span class="sxs-lookup"><span data-stu-id="c6631-137">Upgrading to a New Version of the Toolkit</span></span>

<span data-ttu-id="c6631-138">以前のリリースの Toolkit を使用していて、今後のバージョンに移行する必要がある場合は、次の手順を実行することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="c6631-138">If you were using an older release of the Toolkit and now need to move to a later version here are the recommended steps:</span></span>

- <span data-ttu-id="c6631-139">バイナリ-web サイトの Bin フォルダーから古いバージョンの AjaxControlToolkit アセンブリを削除します。</span><span class="sxs-lookup"><span data-stu-id="c6631-139">Binaries - Delete the old version of the AjaxControlToolkit.dll assembly from your website Bin folder.</span></span>
- <span data-ttu-id="c6631-140">ツールボックスアイテム-AJAX Control Toolkit タブを削除し、上記の手順に従って、新しいバージョンの AjaxControlToolkit アセンブリを使用してタブを再作成します。</span><span class="sxs-lookup"><span data-stu-id="c6631-140">Toolbox Items - Delete the AJAX Control Toolkit tab and follow the steps above to re-create the tab with the new version of the AjaxControlToolkit.dll assembly.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="c6631-141">Next</span><span class="sxs-lookup"><span data-stu-id="c6631-141">Next</span></span>](using-ajax-control-toolkit-controls-and-control-extenders-cs.md)
