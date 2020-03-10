---
uid: web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-in-a-formview-vb
title: FormView で TextBoxWatermark を使用する (VB) |Microsoft Docs
author: wenz
description: AJAX コントロールツールキットの TextBoxWatermark コントロールは、テキストがボックス内に表示されるようにテキストボックスを拡張します。 ユーザーがボックスをクリックすると、...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 41497361-7fba-4825-b36c-f58d79522a88
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-in-a-formview-vb
msc.type: authoredcontent
ms.openlocfilehash: 1dd17ed57383680122c4ca613ca71f6682dec40e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78508804"
---
# <a name="using-textboxwatermark-in-a-formview-vb"></a><span data-ttu-id="cf697-104">FormView で TextBoxWatermark を使用する (VB)</span><span class="sxs-lookup"><span data-stu-id="cf697-104">Using TextBoxWatermark in a FormView (VB)</span></span>

<span data-ttu-id="cf697-105">[Christian Wenz](https://github.com/wenz)別</span><span class="sxs-lookup"><span data-stu-id="cf697-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="cf697-106">[コードのダウンロード](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/TextBoxWatermark1.vb.zip)または[PDF のダウンロード](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/textboxwatermark1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="cf697-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/TextBoxWatermark1.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/textboxwatermark1VB.pdf)</span></span>

> <span data-ttu-id="cf697-107">AJAX コントロールツールキットの TextBoxWatermark コントロールは、テキストがボックス内に表示されるようにテキストボックスを拡張します。</span><span class="sxs-lookup"><span data-stu-id="cf697-107">The TextBoxWatermark control in the AJAX Control Toolkit extends a text box so that a text is displayed within the box.</span></span> <span data-ttu-id="cf697-108">ユーザーがボックスをクリックすると、そのボックスは空になります。</span><span class="sxs-lookup"><span data-stu-id="cf697-108">When a user clicks into the box, it is emptied.</span></span> <span data-ttu-id="cf697-109">ユーザーがテキストを入力せずにボックスを離れると、事前テキストが再び表示されます。</span><span class="sxs-lookup"><span data-stu-id="cf697-109">If the user leaves the box without entering text, the prefilled text reappears.</span></span> <span data-ttu-id="cf697-110">これは、FormView コントロール内でも可能です。</span><span class="sxs-lookup"><span data-stu-id="cf697-110">This is also possible within a FormView control.</span></span>

## <a name="overview"></a><span data-ttu-id="cf697-111">概要</span><span class="sxs-lookup"><span data-stu-id="cf697-111">Overview</span></span>

<span data-ttu-id="cf697-112">AJAX コントロールツールキットの `TextBoxWatermark` コントロールは、テキストがボックス内に表示されるようにテキストボックスを拡張します。</span><span class="sxs-lookup"><span data-stu-id="cf697-112">The `TextBoxWatermark` control in the AJAX Control Toolkit extends a text box so that a text is displayed within the box.</span></span> <span data-ttu-id="cf697-113">ユーザーがボックスをクリックすると、そのボックスは空になります。</span><span class="sxs-lookup"><span data-stu-id="cf697-113">When a user clicks into the box, it is emptied.</span></span> <span data-ttu-id="cf697-114">ユーザーがテキストを入力せずにボックスを離れると、事前テキストが再び表示されます。</span><span class="sxs-lookup"><span data-stu-id="cf697-114">If the user leaves the box without entering text, the prefilled text reappears.</span></span> <span data-ttu-id="cf697-115">これは、`FormView` コントロール内でも可能です。</span><span class="sxs-lookup"><span data-stu-id="cf697-115">This is also possible within a `FormView` control.</span></span>

## <a name="steps"></a><span data-ttu-id="cf697-116">手順</span><span class="sxs-lookup"><span data-stu-id="cf697-116">Steps</span></span>

<span data-ttu-id="cf697-117">まず、データソースが必要です。</span><span class="sxs-lookup"><span data-stu-id="cf697-117">First of all, a data source is required.</span></span> <span data-ttu-id="cf697-118">このサンプルでは、AdventureWorks データベースと Microsoft SQL Server 2005 Express Edition を使用します。</span><span class="sxs-lookup"><span data-stu-id="cf697-118">This sample uses the AdventureWorks database and the Microsoft SQL Server 2005 Express Edition.</span></span> <span data-ttu-id="cf697-119">このデータベースは、Visual Studio のインストール (express edition を含む) の省略可能な部分であり、 [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064)で個別にダウンロードすることもできます。</span><span class="sxs-lookup"><span data-stu-id="cf697-119">The database is an optional part of a Visual Studio installation (including express edition) and is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="cf697-120">AdventureWorks データベースは SQL Server 2005 サンプルおよびサンプルデータベース ( [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;D isplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)) に含まれています。</span><span class="sxs-lookup"><span data-stu-id="cf697-120">The AdventureWorks database is part of the SQL Server 2005 Samples and Sample Databases (download at [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span></span> <span data-ttu-id="cf697-121">データベースをセットアップする最も簡単な方法は、Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) を使用して、`AdventureWorks.mdf` データベースファイルをアタッチすることです。</span><span class="sxs-lookup"><span data-stu-id="cf697-121">The easiest way to set the database up is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) and attach the `AdventureWorks.mdf` database file.</span></span>

<span data-ttu-id="cf697-122">このサンプルでは、SQL Server 2005 Express Edition のインスタンスが `SQLEXPRESS` 呼び出され、web サーバーと同じコンピューター上に存在することを前提としています。これは、既定のセットアップでもあります。</span><span class="sxs-lookup"><span data-stu-id="cf697-122">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="cf697-123">セットアップが異なる場合は、データベースの接続情報を調整する必要があります。</span><span class="sxs-lookup"><span data-stu-id="cf697-123">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="cf697-124">ASP.NET AJAX と Control Toolkit の機能をアクティブ化するには、ページの任意の場所に `ScriptManager` コントロールを配置する必要があります (`<form>` 要素内)。</span><span class="sxs-lookup"><span data-stu-id="cf697-124">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](using-textboxwatermark-in-a-formview-vb/samples/sample1.aspx)]

<span data-ttu-id="cf697-125">次に、`DELETE`、`INSERT`、および `UPDATE` SQL ステートメントをサポートするページにデータソースを追加します。</span><span class="sxs-lookup"><span data-stu-id="cf697-125">Then, add a data source to the page which supports the `DELETE`, `INSERT` and `UPDATE` SQL statements.</span></span> <span data-ttu-id="cf697-126">Visual Studio アシスタントを使用してデータソースを作成する場合は、現在のバージョンのバグによって、テーブル名 (`Vendor`) のプレフィックスが `Purchasing`になっていないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="cf697-126">If you are using the Visual Studio assistant to create the data source, mind that a bug in the current version does not prefix the table name (`Vendor`) with `Purchasing`.</span></span> <span data-ttu-id="cf697-127">次のマークアップは、正しい構文を示しています。</span><span class="sxs-lookup"><span data-stu-id="cf697-127">The following markup shows the correct syntax:</span></span>

[!code-aspx[Main](using-textboxwatermark-in-a-formview-vb/samples/sample2.aspx)]

<span data-ttu-id="cf697-128">データソースの名前 (`ID`) は、`FormView` コントロールの `DataSourceID` プロパティで使用されるため、覚えておいてください。</span><span class="sxs-lookup"><span data-stu-id="cf697-128">Remember the name (`ID`) of the data source, since it will be used in the `DataSourceID` property of the `FormView` control.</span></span> <span data-ttu-id="cf697-129">`FormView` の `<InsertItemTemplate>` セクションには、`TextBoxWatermarkExtender` コントロールによって拡張されたテキストボックスが含まれています。</span><span class="sxs-lookup"><span data-stu-id="cf697-129">The `<InsertItemTemplate>` section of the `FormView` contains a textbox which is extended by the `TextBoxWatermarkExtender` control.</span></span> <span data-ttu-id="cf697-130">Extender がテンプレート内に存在し、その外部にないことを確認します。</span><span class="sxs-lookup"><span data-stu-id="cf697-130">Make sure that the extender resides within the template and not outside of it.</span></span>

[!code-aspx[Main](using-textboxwatermark-in-a-formview-vb/samples/sample3.aspx)]

<span data-ttu-id="cf697-131">これで、ユーザーが `FormView` コントロールの挿入モードに変更されたときに、新しいベンダーのテキストフィールドは、`TextBoxWatermarkExtender` コントロールに感謝します。</span><span class="sxs-lookup"><span data-stu-id="cf697-131">Now when the user changes into the insert mode of the `FormView` control, the text field for the new vendor is prefilled thanks to the `TextBoxWatermarkExtender` control.</span></span> <span data-ttu-id="cf697-132">テキストボックス内をクリックすると、充てんテキストが非表示になります。</span><span class="sxs-lookup"><span data-stu-id="cf697-132">A click inside the textbox lets the filler text disappear.</span></span>

<span data-ttu-id="cf697-133">[フィールドのウォーターマークが extender から取得された ![](using-textboxwatermark-in-a-formview-vb/_static/image2.png)](using-textboxwatermark-in-a-formview-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="cf697-133">[![The watermark in the field comes from the extender](using-textboxwatermark-in-a-formview-vb/_static/image2.png)](using-textboxwatermark-in-a-formview-vb/_static/image1.png)</span></span>

<span data-ttu-id="cf697-134">フィールドのウォーターマークは extender から取得されます ([クリックすると、フルサイズの画像が表示](using-textboxwatermark-in-a-formview-vb/_static/image3.png)されます)</span><span class="sxs-lookup"><span data-stu-id="cf697-134">The watermark in the field comes from the extender ([Click to view full-size image](using-textboxwatermark-in-a-formview-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="cf697-135">[前へ](using-textboxwatermark-with-validation-controls-cs.md)
> [次へ](using-textboxwatermark-with-validation-controls-vb.md)</span><span class="sxs-lookup"><span data-stu-id="cf697-135">[Previous](using-textboxwatermark-with-validation-controls-cs.md)
[Next](using-textboxwatermark-with-validation-controls-vb.md)</span></span>
