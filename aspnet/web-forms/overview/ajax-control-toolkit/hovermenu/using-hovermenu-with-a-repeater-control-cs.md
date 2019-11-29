---
uid: web-forms/overview/ajax-control-toolkit/hovermenu/using-hovermenu-with-a-repeater-control-cs
title: Repeater コントロールで HoverMenu を使用するC#() |Microsoft Docs
author: wenz
description: AJAX コントロールツールキットの HoverMenu コントロールは、単純なポップアップ効果を提供します。マウスポインターが要素の上に置かれると、ポップアップが specifi に表示されます。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e7700e7b-edc3-4183-a713-70e507cc7490
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/hovermenu/using-hovermenu-with-a-repeater-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 3e38b91d837c65191d4b3797fa31ef6112a1f070
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74606717"
---
# <a name="using-hovermenu-with-a-repeater-control-c"></a><span data-ttu-id="a42f1-103">Repeater コントロールで HoverMenu を使用する (C#)</span><span class="sxs-lookup"><span data-stu-id="a42f1-103">Using HoverMenu with a Repeater Control (C#)</span></span>

<span data-ttu-id="a42f1-104">[Christian Wenz](https://github.com/wenz)別</span><span class="sxs-lookup"><span data-stu-id="a42f1-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="a42f1-105">[コードのダウンロード](https://download.microsoft.com/download/b/0/6/b06fe835-5b8f-4c00-aef8-062c19d75b95/HoverMenu1.cs.zip)または[PDF のダウンロード](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/hovermenu1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="a42f1-105">[Download Code](https://download.microsoft.com/download/b/0/6/b06fe835-5b8f-4c00-aef8-062c19d75b95/HoverMenu1.cs.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/hovermenu1CS.pdf)</span></span>

> <span data-ttu-id="a42f1-106">AJAX コントロールツールキットの HoverMenu コントロールは、単純なポップアップ効果を提供します。マウスポインターが要素の上に置かれると、ポップアップが指定した位置に表示されます。</span><span class="sxs-lookup"><span data-stu-id="a42f1-106">The HoverMenu control in the AJAX Control Toolkit provides a simple popup effect: When the mouse pointer hovers over an element, a popup appears at a specified position.</span></span> <span data-ttu-id="a42f1-107">リピータ内でこのコントロールを使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="a42f1-107">It is also possible to use this control within a repeater.</span></span>

## <a name="overview"></a><span data-ttu-id="a42f1-108">の概要</span><span class="sxs-lookup"><span data-stu-id="a42f1-108">Overview</span></span>

<span data-ttu-id="a42f1-109">AJAX コントロールツールキットの `HoverMenu` コントロールは、単純なポップアップ効果を提供します。マウスポインターが要素の上に移動すると、指定した位置にポップアップが表示されます。</span><span class="sxs-lookup"><span data-stu-id="a42f1-109">The `HoverMenu` control in the AJAX Control Toolkit provides a simple popup effect: When the mouse pointer hovers over an element, a popup appears at a specified position.</span></span> <span data-ttu-id="a42f1-110">リピータ内でこのコントロールを使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="a42f1-110">It is also possible to use this control within a repeater.</span></span>

## <a name="steps"></a><span data-ttu-id="a42f1-111">手順</span><span class="sxs-lookup"><span data-stu-id="a42f1-111">Steps</span></span>

<span data-ttu-id="a42f1-112">まず、データソースが必要です。</span><span class="sxs-lookup"><span data-stu-id="a42f1-112">First of all, a data source is required.</span></span> <span data-ttu-id="a42f1-113">このサンプルでは、AdventureWorks データベースと Microsoft SQL Server 2005 Express Edition を使用します。</span><span class="sxs-lookup"><span data-stu-id="a42f1-113">This sample uses the AdventureWorks database and the Microsoft SQL Server 2005 Express Edition.</span></span> <span data-ttu-id="a42f1-114">このデータベースは、Visual Studio のインストール (express edition を含む) の省略可能な部分であり、 [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064)で個別にダウンロードすることもできます。</span><span class="sxs-lookup"><span data-stu-id="a42f1-114">The database is an optional part of a Visual Studio installation (including express edition) and is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="a42f1-115">AdventureWorks データベースは SQL Server 2005 サンプルおよびサンプルデータベース ( [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;D isplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)) に含まれています。</span><span class="sxs-lookup"><span data-stu-id="a42f1-115">The AdventureWorks database is part of the SQL Server 2005 Samples and Sample Databases (download at [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span></span> <span data-ttu-id="a42f1-116">データベースをセットアップする最も簡単な方法は、Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) を使用して、`AdventureWorks.mdf` データベースファイルをアタッチすることです。</span><span class="sxs-lookup"><span data-stu-id="a42f1-116">The easiest way to set the database up is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) and attach the `AdventureWorks.mdf` database file.</span></span>

<span data-ttu-id="a42f1-117">このサンプルでは、SQL Server 2005 Express Edition のインスタンスが `SQLEXPRESS` 呼び出され、web サーバーと同じコンピューター上に存在することを前提としています。これは、既定のセットアップでもあります。</span><span class="sxs-lookup"><span data-stu-id="a42f1-117">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="a42f1-118">セットアップが異なる場合は、データベースの接続情報を調整する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a42f1-118">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="a42f1-119">ASP.NET AJAX と Control Toolkit の機能をアクティブ化するには、ページの任意の場所に `ScriptManager` コントロールを配置する必要があります (`<form>` 要素内)。</span><span class="sxs-lookup"><span data-stu-id="a42f1-119">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample1.aspx)]

<span data-ttu-id="a42f1-120">次に、データソースをページに追加します。</span><span class="sxs-lookup"><span data-stu-id="a42f1-120">Then, add a data source to the page.</span></span> <span data-ttu-id="a42f1-121">限られた量のデータを使用するために、AdventureWorks データベースの Vendor テーブルの最初の5つのエントリのみを選択します。</span><span class="sxs-lookup"><span data-stu-id="a42f1-121">In order to use a limited amount of data, we only select the first five entries in the Vendor table of the AdventureWorks database.</span></span> <span data-ttu-id="a42f1-122">Visual Studio アシスタントを使用してデータソースを作成する場合は、現在のバージョンのバグによって、テーブル名 (`Vendor`) のプレフィックスが `Purchasing`になっていないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="a42f1-122">If you are using the Visual Studio assistant to create the data source, mind that a bug in the current version does not prefix the table name (`Vendor`) with `Purchasing`.</span></span> <span data-ttu-id="a42f1-123">次のマークアップは、正しい構文を示しています。</span><span class="sxs-lookup"><span data-stu-id="a42f1-123">The following markup shows the correct syntax:</span></span>

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample2.aspx)]

<span data-ttu-id="a42f1-124">次に、モーダルポップアップとして機能するパネルを追加します。</span><span class="sxs-lookup"><span data-stu-id="a42f1-124">Next, add a panel which serves as the modal popup:</span></span>

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample3.aspx)]

<span data-ttu-id="a42f1-125">これで、`HoverMenuExtender` が登場します。</span><span class="sxs-lookup"><span data-stu-id="a42f1-125">Now, the `HoverMenuExtender` comes into play.</span></span> <span data-ttu-id="a42f1-126">データソース内のすべての要素が独自のポップアップを取得できるように、extender はリピータの `<ItemTemplate>` セクション内に配置する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a42f1-126">So that every element in the data source gets its own popup, the extender must be put within the repeater's `<ItemTemplate>` section.</span></span> <span data-ttu-id="a42f1-127">マークアップは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="a42f1-127">Here is the markup:</span></span>

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample4.aspx)]

<span data-ttu-id="a42f1-128">データソース内のすべてのアイテムは、50ミリ秒 (`PopDelay` 属性) の遅延の後に右側 (`PopupPosition` 属性) のポップアップを表示するようになりました。</span><span class="sxs-lookup"><span data-stu-id="a42f1-128">Now every item in the data source displays a popup to the right (`PopupPosition` attribute) after a delay of 50 milliseconds (`PopDelay` attribute).</span></span>

<span data-ttu-id="a42f1-129">[リピータの各項目の横にホバーメニューが表示される ![](using-hovermenu-with-a-repeater-control-cs/_static/image2.png)](using-hovermenu-with-a-repeater-control-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="a42f1-129">[![The hover menu appears next to each item in the repeater](using-hovermenu-with-a-repeater-control-cs/_static/image2.png)](using-hovermenu-with-a-repeater-control-cs/_static/image1.png)</span></span>

<span data-ttu-id="a42f1-130">リピータの各項目の横に、ホバーメニューが表示されます ([クリックすると、フルサイズの画像が表示](using-hovermenu-with-a-repeater-control-cs/_static/image3.png)されます)</span><span class="sxs-lookup"><span data-stu-id="a42f1-130">The hover menu appears next to each item in the repeater ([Click to view full-size image](using-hovermenu-with-a-repeater-control-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="a42f1-131">次へ</span><span class="sxs-lookup"><span data-stu-id="a42f1-131">Next</span></span>](using-hovermenu-with-a-repeater-control-vb.md)
