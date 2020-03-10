---
uid: web-forms/overview/ajax-control-toolkit/confirmbutton/using-a-confirmbutton-in-a-repeater-vb
title: Repeater で ConfirmButton を使用する (VB) |Microsoft Docs
author: wenz
description: AJAX コントロールツールキットの ConfirmButton エクステンダーは、ユーザーがボタン (LinkButton コントロールを含む) をクリックしたときに、[はい/いいえ] ポップアップを作成します。 [はい] の場合のみ...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 18c31709-3f9d-4d93-8b01-f1356bf610b4
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/confirmbutton/using-a-confirmbutton-in-a-repeater-vb
msc.type: authoredcontent
ms.openlocfilehash: 001233d866d8a731d93d6900f714cd2060f3d08c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78497542"
---
# <a name="using-a-confirmbutton-in-a-repeater-vb"></a><span data-ttu-id="41ffb-104">Repeater で ConfirmButton を使用する (VB)</span><span class="sxs-lookup"><span data-stu-id="41ffb-104">Using a ConfirmButton In a Repeater (VB)</span></span>

<span data-ttu-id="41ffb-105">[Christian Wenz](https://github.com/wenz)別</span><span class="sxs-lookup"><span data-stu-id="41ffb-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="41ffb-106">[コードのダウンロード](https://download.microsoft.com/download/8/6/d/86dea6c6-bb92-4fa6-aa14-f8c0f82100f5/ConfirmButton1.vb.zip)または[PDF のダウンロード](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/confirmbutton1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="41ffb-106">[Download Code](https://download.microsoft.com/download/8/6/d/86dea6c6-bb92-4fa6-aa14-f8c0f82100f5/ConfirmButton1.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/confirmbutton1VB.pdf)</span></span>

> <span data-ttu-id="41ffb-107">AJAX コントロールツールキットの ConfirmButton エクステンダーは、ユーザーがボタン (LinkButton コントロールを含む) をクリックしたときに、[はい/いいえ] ポップアップを作成します。</span><span class="sxs-lookup"><span data-stu-id="41ffb-107">The ConfirmButton extender in the AJAX Control Toolkit creates a Yes/No popup when the user clicks on a button (including LinkButton control).</span></span> <span data-ttu-id="41ffb-108">[はい] をクリックした場合にのみ、ボタンのアクションが実行されます。それ以外の場合は取り消されます。</span><span class="sxs-lookup"><span data-stu-id="41ffb-108">Only if Yes is clicked, the button's action is executed, otherwise cancelled.</span></span> <span data-ttu-id="41ffb-109">これは、リピータでも可能です。</span><span class="sxs-lookup"><span data-stu-id="41ffb-109">This is also possible in a repeater.</span></span>

## <a name="overview"></a><span data-ttu-id="41ffb-110">概要</span><span class="sxs-lookup"><span data-stu-id="41ffb-110">Overview</span></span>

<span data-ttu-id="41ffb-111">AJAX コントロールツールキットの ConfirmButton エクステンダーは、ユーザーがボタン (LinkButton コントロールを含む) をクリックしたときに、[はい/いいえ] ポップアップを作成します。</span><span class="sxs-lookup"><span data-stu-id="41ffb-111">The ConfirmButton extender in the AJAX Control Toolkit creates a Yes/No popup when the user clicks on a button (including LinkButton control).</span></span> <span data-ttu-id="41ffb-112">[はい] をクリックした場合にのみ、ボタンのアクションが実行されます。それ以外の場合は取り消されます。</span><span class="sxs-lookup"><span data-stu-id="41ffb-112">Only if Yes is clicked, the button's action is executed, otherwise cancelled.</span></span> <span data-ttu-id="41ffb-113">これは、リピータでも可能です。</span><span class="sxs-lookup"><span data-stu-id="41ffb-113">This is also possible in a repeater.</span></span>

## <a name="steps"></a><span data-ttu-id="41ffb-114">手順</span><span class="sxs-lookup"><span data-stu-id="41ffb-114">Steps</span></span>

<span data-ttu-id="41ffb-115">まず、データソースが必要です。</span><span class="sxs-lookup"><span data-stu-id="41ffb-115">First of all, a data source is required.</span></span> <span data-ttu-id="41ffb-116">このサンプルでは、AdventureWorks データベースと Microsoft SQL Server 2005 Express Edition を使用します。</span><span class="sxs-lookup"><span data-stu-id="41ffb-116">This sample uses the AdventureWorks database and the Microsoft SQL Server 2005 Express Edition.</span></span> <span data-ttu-id="41ffb-117">このデータベースは、Visual Studio のインストール (express edition を含む) の省略可能な部分であり、 [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064)で個別にダウンロードすることもできます。</span><span class="sxs-lookup"><span data-stu-id="41ffb-117">The database is an optional part of a Visual Studio installation (including express edition) and is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="41ffb-118">AdventureWorks データベースは SQL Server 2005 サンプルおよびサンプルデータベース ( [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;D isplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)) に含まれています。</span><span class="sxs-lookup"><span data-stu-id="41ffb-118">The AdventureWorks database is part of the SQL Server 2005 Samples and Sample Databases (download at [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span></span> <span data-ttu-id="41ffb-119">データベースをセットアップする最も簡単な方法は、Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) を使用して、`AdventureWorks.mdf` データベースファイルをアタッチすることです。</span><span class="sxs-lookup"><span data-stu-id="41ffb-119">The easiest way to set the database up is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) and attach the `AdventureWorks.mdf` database file.</span></span>

<span data-ttu-id="41ffb-120">このサンプルでは、SQL Server 2005 Express Edition のインスタンスが `SQLEXPRESS` 呼び出され、web サーバーと同じコンピューター上に存在することを前提としています。これは、既定のセットアップでもあります。</span><span class="sxs-lookup"><span data-stu-id="41ffb-120">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="41ffb-121">セットアップが異なる場合は、データベースの接続情報を調整する必要があります。</span><span class="sxs-lookup"><span data-stu-id="41ffb-121">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="41ffb-122">ASP.NET AJAX と Control Toolkit の機能をアクティブ化するには、ページの任意の場所に `ScriptManager` コントロールを配置する必要があります (`<form>` 要素内)。</span><span class="sxs-lookup"><span data-stu-id="41ffb-122">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](using-a-confirmbutton-in-a-repeater-vb/samples/sample1.aspx)]

<span data-ttu-id="41ffb-123">次に、データソースが必要です。</span><span class="sxs-lookup"><span data-stu-id="41ffb-123">Then, a data source is required.</span></span> <span data-ttu-id="41ffb-124">わかりやすくするために、AdventureWorks の [ベンダ] テーブルの最初の5つのエントリのみが取得されます。</span><span class="sxs-lookup"><span data-stu-id="41ffb-124">For the sake of simplicity, only the first five entries in AdventureWorks' Vendors table are retrieved.</span></span> <span data-ttu-id="41ffb-125">Visual Studio ウィザードを使用してデータソースを作成する場合、テーブル名 (`Vendors`) の先頭には `Purchasing`が正しく付けられていないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="41ffb-125">Note that when using the Visual Studio wizard to create the data source, the table name (`Vendors`) is currently not correctly prefixed with `Purchasing`.</span></span> <span data-ttu-id="41ffb-126">適切なマークアップは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="41ffb-126">The following markup is the correct one:</span></span>

[!code-aspx[Main](using-a-confirmbutton-in-a-repeater-vb/samples/sample2.aspx)]

<span data-ttu-id="41ffb-127">このデータソースは、リピータ内で使用できます。</span><span class="sxs-lookup"><span data-stu-id="41ffb-127">This data source can then be used within a repeater.</span></span> <span data-ttu-id="41ffb-128">通常どおり、`DataBinder.Eval()` メソッドはデータソースからデータを取得します。</span><span class="sxs-lookup"><span data-stu-id="41ffb-128">As usual, the `DataBinder.Eval()` method retrieves data from the data source.</span></span> <span data-ttu-id="41ffb-129">`ConfirmButtonExtender` コントロールは、データソース内のすべてのエントリに対して表示されるように、repeater の `<ItemTemplate>` セクション内に配置する必要があります。</span><span class="sxs-lookup"><span data-stu-id="41ffb-129">The `ConfirmButtonExtender` control must then be placed within the `<ItemTemplate>` section of the repeater so that it appears for every entry in the data source.</span></span>

[!code-aspx[Main](using-a-confirmbutton-in-a-repeater-vb/samples/sample3.aspx)]

<span data-ttu-id="41ffb-130">[![データソースの各エントリの横に [確認] ボタンが表示されます。](using-a-confirmbutton-in-a-repeater-vb/_static/image2.png)](using-a-confirmbutton-in-a-repeater-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="41ffb-130">[![The confirm button appears next to each entry from the data source](using-a-confirmbutton-in-a-repeater-vb/_static/image2.png)](using-a-confirmbutton-in-a-repeater-vb/_static/image1.png)</span></span>

<span data-ttu-id="41ffb-131">データソースからの各エントリの横に [確認] ボタンが表示されます ([クリックすると、フルサイズの画像が表示](using-a-confirmbutton-in-a-repeater-vb/_static/image3.png)されます)</span><span class="sxs-lookup"><span data-stu-id="41ffb-131">The confirm button appears next to each entry from the data source ([Click to view full-size image](using-a-confirmbutton-in-a-repeater-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="41ffb-132">[[戻る]](using-a-confirmbutton-in-a-repeater-cs.md)</span><span class="sxs-lookup"><span data-stu-id="41ffb-132">[Previous](using-a-confirmbutton-in-a-repeater-cs.md)</span></span>
