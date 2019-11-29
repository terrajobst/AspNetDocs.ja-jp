---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/using-modalpopup-with-a-repeater-control-cs
title: Repeater コントロールで ModalPopup を使用するC#() |Microsoft Docs
author: wenz
description: AJAX コントロールツールキットの ModalPopup コントロールを使用すると、クライアント側の方法を使用してモーダルポップアップを簡単に作成できます。 また、次のものを使用することもできます...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: d686d84a-1c58-492e-8a77-3eb5a0cfe918
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/using-modalpopup-with-a-repeater-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 980f023c9e8256ad5323aaa6cbb6918b04e18974
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74598920"
---
# <a name="using-modalpopup-with-a-repeater-control-c"></a><span data-ttu-id="27320-104">Repeater コントロールで ModalPopup を使用する (C#)</span><span class="sxs-lookup"><span data-stu-id="27320-104">Using ModalPopup with a Repeater Control (C#)</span></span>

<span data-ttu-id="27320-105">[Christian Wenz](https://github.com/wenz)別</span><span class="sxs-lookup"><span data-stu-id="27320-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="27320-106">[コードのダウンロード](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup2.cs.zip)または[PDF のダウンロード](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup2CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="27320-106">[Download Code](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup2.cs.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup2CS.pdf)</span></span>

> <span data-ttu-id="27320-107">AJAX コントロールツールキットの ModalPopup コントロールを使用すると、クライアント側の方法を使用してモーダルポップアップを簡単に作成できます。</span><span class="sxs-lookup"><span data-stu-id="27320-107">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="27320-108">リピータ内でこのコントロールを使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="27320-108">It is also possible to use this control within a repeater.</span></span>

## <a name="overview"></a><span data-ttu-id="27320-109">の概要</span><span class="sxs-lookup"><span data-stu-id="27320-109">Overview</span></span>

<span data-ttu-id="27320-110">AJAX コントロールツールキットの ModalPopup コントロールを使用すると、クライアント側の方法を使用してモーダルポップアップを簡単に作成できます。</span><span class="sxs-lookup"><span data-stu-id="27320-110">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="27320-111">リピータ内でこのコントロールを使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="27320-111">It is also possible to use this control within a repeater.</span></span>

## <a name="steps"></a><span data-ttu-id="27320-112">手順</span><span class="sxs-lookup"><span data-stu-id="27320-112">Steps</span></span>

<span data-ttu-id="27320-113">まず、データソースが必要です。</span><span class="sxs-lookup"><span data-stu-id="27320-113">First of all, a data source is required.</span></span> <span data-ttu-id="27320-114">このサンプルでは、AdventureWorks データベースと Microsoft SQL Server 2005 Express Edition を使用します。</span><span class="sxs-lookup"><span data-stu-id="27320-114">This sample uses the AdventureWorks database and the Microsoft SQL Server 2005 Express Edition.</span></span> <span data-ttu-id="27320-115">このデータベースは、Visual Studio のインストール (express edition を含む) の省略可能な部分であり、 [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064)で個別にダウンロードすることもできます。</span><span class="sxs-lookup"><span data-stu-id="27320-115">The database is an optional part of a Visual Studio installation (including express edition) and is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="27320-116">AdventureWorks データベースは SQL Server 2005 サンプルおよびサンプルデータベース ( [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;D isplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)) に含まれています。</span><span class="sxs-lookup"><span data-stu-id="27320-116">The AdventureWorks database is part of the SQL Server 2005 Samples and Sample Databases (download at [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span></span> <span data-ttu-id="27320-117">データベースをセットアップする最も簡単な方法は、Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) を使用して、`AdventureWorks.mdf` データベースファイルをアタッチすることです。</span><span class="sxs-lookup"><span data-stu-id="27320-117">The easiest way to set the database up is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) and attach the `AdventureWorks.mdf` database file.</span></span> <span data-ttu-id="27320-118">このサンプルでは、SQL Server 2005 Express Edition のインスタンスが `SQLEXPRESS` 呼び出され、web サーバーと同じコンピューター上に存在することを前提としています。これは、既定のセットアップでもあります。</span><span class="sxs-lookup"><span data-stu-id="27320-118">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="27320-119">セットアップが異なる場合は、データベースの接続情報を調整する必要があります。</span><span class="sxs-lookup"><span data-stu-id="27320-119">If your setup differs, you have to adapt the connection information for the database.</span></span> <span data-ttu-id="27320-120">ASP.NET AJAX と Control Toolkit の機能をアクティブ化するには、ページの任意の場所に `ScriptManager` コントロールを配置する必要があります (`<form>` 要素内)。</span><span class="sxs-lookup"><span data-stu-id="27320-120">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](using-modalpopup-with-a-repeater-control-cs/samples/sample1.aspx)]

<span data-ttu-id="27320-121">次に、データソースをページに追加します。</span><span class="sxs-lookup"><span data-stu-id="27320-121">Then, add a data source to the page.</span></span> <span data-ttu-id="27320-122">限られた量のデータを使用するために、AdventureWorks データベースの Vendor テーブルの最初の5つのエントリのみを選択します。</span><span class="sxs-lookup"><span data-stu-id="27320-122">In order to use a limited amount of data, we only select the first five entries in the Vendor table of the AdventureWorks database.</span></span> <span data-ttu-id="27320-123">Visual Studio アシスタントを使用してデータソースを作成する場合は、現在のバージョンのバグによって、テーブル名 (`Vendor`) のプレフィックスが `Purchasing`になっていないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="27320-123">If you are using the Visual Studio assistant to create the data source, mind that a bug in the current version does not prefix the table name (`Vendor`) with `Purchasing`.</span></span> <span data-ttu-id="27320-124">次のマークアップは、正しい構文を示しています。</span><span class="sxs-lookup"><span data-stu-id="27320-124">The following markup shows the correct syntax:</span></span>

[!code-aspx[Main](using-modalpopup-with-a-repeater-control-cs/samples/sample2.aspx)]

<span data-ttu-id="27320-125">次に、モーダルポップアップとして機能するパネルを追加します。</span><span class="sxs-lookup"><span data-stu-id="27320-125">Next, add a panel which serves as the modal popup.</span></span> <span data-ttu-id="27320-126">ポップアップを再び閉じるための `Button` コントロールが含まれています。</span><span class="sxs-lookup"><span data-stu-id="27320-126">It contains a `Button` control to close the popup again:</span></span>

[!code-aspx[Main](using-modalpopup-with-a-repeater-control-cs/samples/sample3.aspx)]

<span data-ttu-id="27320-127">リピータ内でポップアップを機能させるには、`ModalPopupExtender` コントロールをリピータの `<ItemTemplate>` セクション内に配置する必要があります。</span><span class="sxs-lookup"><span data-stu-id="27320-127">In order to make the popup work within the repeater, the `ModalPopupExtender` control must be put within the `<ItemTemplate>` section of the repeater.</span></span> <span data-ttu-id="27320-128">そのため、パネルはリピータの外側にありますが、extender は内側にあります。</span><span class="sxs-lookup"><span data-stu-id="27320-128">So the panel is outside the repeater, but the extender is inside.</span></span> <span data-ttu-id="27320-129">リピータのマークアップを次に示します。</span><span class="sxs-lookup"><span data-stu-id="27320-129">Here is the markup for the repeater:</span></span>

[!code-aspx[Main](using-modalpopup-with-a-repeater-control-cs/samples/sample4.aspx)]

<span data-ttu-id="27320-130">次に、データソース内のすべての項目が、モーダルポップアップをトリガーするボタンと共に表示されます。</span><span class="sxs-lookup"><span data-stu-id="27320-130">Then, every item in the data source is displayed with a button next to it that triggers the modal popup.</span></span>

<span data-ttu-id="27320-131">[データソースエントリごとにモーダルポップアップをトリガーできる ![](using-modalpopup-with-a-repeater-control-cs/_static/image2.png)](using-modalpopup-with-a-repeater-control-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="27320-131">[![The modal popup can be triggered for every data source entry](using-modalpopup-with-a-repeater-control-cs/_static/image2.png)](using-modalpopup-with-a-repeater-control-cs/_static/image1.png)</span></span>

<span data-ttu-id="27320-132">すべてのデータソースエントリに対してモーダルポップアップをトリガーできます ([クリックすると、フルサイズの画像が表示](using-modalpopup-with-a-repeater-control-cs/_static/image3.png)されます)</span><span class="sxs-lookup"><span data-stu-id="27320-132">The modal popup can be triggered for every data source entry ([Click to view full-size image](using-modalpopup-with-a-repeater-control-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="27320-133">[前へ](launching-a-modal-popup-window-from-server-code-cs.md)
> [次へ](handling-postbacks-from-a-modalpopup-cs.md)</span><span class="sxs-lookup"><span data-stu-id="27320-133">[Previous](launching-a-modal-popup-window-from-server-code-cs.md)
[Next](handling-postbacks-from-a-modalpopup-cs.md)</span></span>
