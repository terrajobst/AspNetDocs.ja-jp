---
uid: web-forms/overview/ajax-control-toolkit/accordion/databinding-to-an-accordion-cs
title: アコーディオン (C#) にデータバインドするMicrosoft Docs
author: wenz
description: AJAX コントロールツールキットのアコーディオンコントロールは、複数のウィンドウを提供し、ユーザーが一度に1つずつ表示できるようにします。 通常、パネルは...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 9c8f0054-e319-46f8-80c0-35b606d2fbd4
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/accordion/databinding-to-an-accordion-cs
msc.type: authoredcontent
ms.openlocfilehash: 6c28cc958a1de9844627ae16175a5aed153993a8
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74607272"
---
# <a name="databinding-to-an-accordion-c"></a><span data-ttu-id="745fe-104">アコーディオンにデータバインドする (C#)</span><span class="sxs-lookup"><span data-stu-id="745fe-104">Databinding to an Accordion (C#)</span></span>

<span data-ttu-id="745fe-105">[Christian Wenz](https://github.com/wenz)別</span><span class="sxs-lookup"><span data-stu-id="745fe-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="745fe-106">[コードのダウンロード](https://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion1.cs.zip)または[PDF のダウンロード](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="745fe-106">[Download Code](https://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion1.cs.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion1CS.pdf)</span></span>

> <span data-ttu-id="745fe-107">AJAX コントロールツールキットのアコーディオンコントロールは、複数のウィンドウを提供し、ユーザーが一度に1つずつ表示できるようにします。</span><span class="sxs-lookup"><span data-stu-id="745fe-107">The Accordion control in the AJAX Control Toolkit provides multiple panes and allows the user to display one of them at a time.</span></span> <span data-ttu-id="745fe-108">通常、パネルはページ内で宣言されますが、データソースへのバインドにより柔軟性が向上します。</span><span class="sxs-lookup"><span data-stu-id="745fe-108">Panels are usually declared within the page itself, but binding to a data source offers more flexibility.</span></span>

## <a name="overview"></a><span data-ttu-id="745fe-109">の概要</span><span class="sxs-lookup"><span data-stu-id="745fe-109">Overview</span></span>

<span data-ttu-id="745fe-110">AJAX コントロールツールキットのアコーディオンコントロールは、複数のウィンドウを提供し、ユーザーが一度に1つずつ表示できるようにします。</span><span class="sxs-lookup"><span data-stu-id="745fe-110">The Accordion control in the AJAX Control Toolkit provides multiple panes and allows the user to display one of them at a time.</span></span> <span data-ttu-id="745fe-111">通常、パネルはページ内で宣言されますが、データソースへのバインドにより柔軟性が向上します。</span><span class="sxs-lookup"><span data-stu-id="745fe-111">Panels are usually declared within the page itself, but binding to a data source offers more flexibility.</span></span>

## <a name="steps"></a><span data-ttu-id="745fe-112">手順</span><span class="sxs-lookup"><span data-stu-id="745fe-112">Steps</span></span>

<span data-ttu-id="745fe-113">まず、データソースが必要です。</span><span class="sxs-lookup"><span data-stu-id="745fe-113">First of all, a data source is required.</span></span> <span data-ttu-id="745fe-114">このサンプルでは、AdventureWorks データベースと Microsoft SQL Server 2005 Express Edition を使用します。</span><span class="sxs-lookup"><span data-stu-id="745fe-114">This sample uses the AdventureWorks database and the Microsoft SQL Server 2005 Express Edition.</span></span> <span data-ttu-id="745fe-115">このデータベースは、Visual Studio のインストール (express edition を含む) の省略可能な部分であり、 [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064)で個別にダウンロードすることもできます。</span><span class="sxs-lookup"><span data-stu-id="745fe-115">The database is an optional part of a Visual Studio installation (including express edition) and is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="745fe-116">AdventureWorks データベースは SQL Server 2005 サンプルおよびサンプルデータベース ( [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;D isplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)) に含まれています。</span><span class="sxs-lookup"><span data-stu-id="745fe-116">The AdventureWorks database is part of the SQL Server 2005 Samples and Sample Databases (download at [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span></span> <span data-ttu-id="745fe-117">データベースをセットアップする最も簡単な方法は、Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) を使用して、`AdventureWorks.mdf` データベースファイルをアタッチすることです。</span><span class="sxs-lookup"><span data-stu-id="745fe-117">The easiest way to set the database up is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) and attach the `AdventureWorks.mdf` database file.</span></span>

<span data-ttu-id="745fe-118">このサンプルでは、SQL Server 2005 Express Edition のインスタンスが `SQLEXPRESS` 呼び出され、web サーバーと同じコンピューター上に存在することを前提としています。これは、既定のセットアップでもあります。</span><span class="sxs-lookup"><span data-stu-id="745fe-118">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="745fe-119">セットアップが異なる場合は、データベースの接続情報を調整する必要があります。</span><span class="sxs-lookup"><span data-stu-id="745fe-119">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="745fe-120">ASP.NET AJAX と Control Toolkit の機能をアクティブ化するには、ページの任意の場所に `ScriptManager` コントロールを配置する必要があります (`<form>` 要素内)。</span><span class="sxs-lookup"><span data-stu-id="745fe-120">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](databinding-to-an-accordion-cs/samples/sample1.aspx)]

<span data-ttu-id="745fe-121">次に、データソースをページに追加します。</span><span class="sxs-lookup"><span data-stu-id="745fe-121">Then, add a data source to the page.</span></span> <span data-ttu-id="745fe-122">限られた量のデータを使用するために、AdventureWorks データベースの Vendor テーブルの最初の5つのエントリのみを選択します。</span><span class="sxs-lookup"><span data-stu-id="745fe-122">In order to use a limited amount of data, we only select the first five entries in the Vendor table of the AdventureWorks database.</span></span> <span data-ttu-id="745fe-123">Visual Studio アシスタントを使用してデータソースを作成する場合は、現在のバージョンのバグによって、テーブル名 (`Vendor`) のプレフィックスが `Purchasing`になっていないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="745fe-123">If you are using the Visual Studio assistant to create the data source, mind that a bug in the current version does not prefix the table name (`Vendor`) with `Purchasing`.</span></span> <span data-ttu-id="745fe-124">次のマークアップは、正しい構文を示しています。</span><span class="sxs-lookup"><span data-stu-id="745fe-124">The following markup shows the correct syntax:</span></span>

[!code-aspx[Main](databinding-to-an-accordion-cs/samples/sample2.aspx)]

<span data-ttu-id="745fe-125">データソースの名前 (ID) を記憶します。</span><span class="sxs-lookup"><span data-stu-id="745fe-125">Remember the name (ID) of the data source.</span></span> <span data-ttu-id="745fe-126">このような識別情報は、アコーディオンコントロールの `DataSourceID` プロパティで使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="745fe-126">This very identification must then be used in the `DataSourceID` property of the Accordion control:</span></span>

[!code-aspx[Main](databinding-to-an-accordion-cs/samples/sample3.aspx)]

<span data-ttu-id="745fe-127">アコーディオンコントロール内では、ヘッダー (`<HeaderTemplate>`) やコンテンツ (`<ContentTemplate>`) など、コントロールのさまざまな部分のテンプレートを提供できます。</span><span class="sxs-lookup"><span data-stu-id="745fe-127">Within the Accordion control, you can provide templates for various parts of the control, including the header (`<HeaderTemplate>`) and the content (`<ContentTemplate>`).</span></span> <span data-ttu-id="745fe-128">これらの要素内では、`DataBinder.Eval()` メソッドを使用して、データソースからデータを出力するだけです。</span><span class="sxs-lookup"><span data-stu-id="745fe-128">Within these elements, just output the data from the data source, using the `DataBinder.Eval()` method:</span></span>

[!code-aspx[Main](databinding-to-an-accordion-cs/samples/sample4.aspx)]

<span data-ttu-id="745fe-129">ページが読み込まれたら、次のサーバー側コードを使用してデータソースをアコーディオンにバインドする必要があります。</span><span class="sxs-lookup"><span data-stu-id="745fe-129">When the page is loaded, the data source must be bound to the accordion with this server-side code:</span></span>

[!code-aspx[Main](databinding-to-an-accordion-cs/samples/sample5.aspx)]

<span data-ttu-id="745fe-130">このサンプルを終了するには、アコーディオンコントロールで参照される2つの CSS クラス (プロパティ `HeaderCssClass` と `ContentCssClass`) を定義する必要があります。</span><span class="sxs-lookup"><span data-stu-id="745fe-130">To conclude this sample, you need to define the two CSS classes that are referenced in the Accordion control (in its properties `HeaderCssClass` and `ContentCssClass`).</span></span> <span data-ttu-id="745fe-131">次のマークアップを、ページの `<head>` セクションに配置します。</span><span class="sxs-lookup"><span data-stu-id="745fe-131">Put the following markup in the `<head>` section of the page:</span></span>

[!code-css[Main](databinding-to-an-accordion-cs/samples/sample6.css)]

<span data-ttu-id="745fe-132">[データソースから直接、アコーディオン内のデータを取得 ![](databinding-to-an-accordion-cs/_static/image2.png)](databinding-to-an-accordion-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="745fe-132">[![The data in the accordion comes directly from the data source](databinding-to-an-accordion-cs/_static/image2.png)](databinding-to-an-accordion-cs/_static/image1.png)</span></span>

<span data-ttu-id="745fe-133">アコーディオン内のデータはデータソースから直接取得されます ([クリックすると、フルサイズの画像が表示](databinding-to-an-accordion-cs/_static/image3.png)されます)</span><span class="sxs-lookup"><span data-stu-id="745fe-133">The data in the accordion comes directly from the data source ([Click to view full-size image](databinding-to-an-accordion-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="745fe-134">次へ</span><span class="sxs-lookup"><span data-stu-id="745fe-134">Next</span></span>](dynamically-adding-an-accordion-pane-cs.md)
