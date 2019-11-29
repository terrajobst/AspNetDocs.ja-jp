---
uid: web-forms/overview/ajax-control-toolkit/reorderlist/drag-and-drop-via-reorderlist-cs
title: ReorderList (C#) を使用してドラッグアンドドロップします。Microsoft Docs
author: wenz
description: AJAX コントロールツールキットの ReorderList コントロールは、ドラッグアンドドロップを使用してユーザーが並べ替えることのできるリストを提供します。 リストの現在の順序は...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 6350ee8e-11d6-4aff-b51c-942878014835
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/reorderlist/drag-and-drop-via-reorderlist-cs
msc.type: authoredcontent
ms.openlocfilehash: 2fc6d55a290cbb58bea36d8145d814e337bbd931
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74611462"
---
# <a name="drag-and-drop-via-reorderlist-c"></a><span data-ttu-id="82ecf-104">ReorderList 経由でドラッグ アンド ドロップする (C#)</span><span class="sxs-lookup"><span data-stu-id="82ecf-104">Drag and Drop via ReorderList (C#)</span></span>

<span data-ttu-id="82ecf-105">[Christian Wenz](https://github.com/wenz)別</span><span class="sxs-lookup"><span data-stu-id="82ecf-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="82ecf-106">[コードのダウンロード](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList5.cs.zip)または[PDF のダウンロード](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist5CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="82ecf-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList5.cs.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist5CS.pdf)</span></span>

> <span data-ttu-id="82ecf-107">AJAX コントロールツールキットの ReorderList コントロールは、ドラッグアンドドロップを使用してユーザーが並べ替えることのできるリストを提供します。</span><span class="sxs-lookup"><span data-stu-id="82ecf-107">The ReorderList control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="82ecf-108">リストの現在の順序は、サーバーで保持されている必要があります。</span><span class="sxs-lookup"><span data-stu-id="82ecf-108">The current order of the list shall be persisted on the server.</span></span>

## <a name="overview"></a><span data-ttu-id="82ecf-109">の概要</span><span class="sxs-lookup"><span data-stu-id="82ecf-109">Overview</span></span>

<span data-ttu-id="82ecf-110">AJAX コントロールツールキットの `ReorderList` コントロールには、ドラッグアンドドロップを使用してユーザーが並べ替えることのできるリストが用意されています。</span><span class="sxs-lookup"><span data-stu-id="82ecf-110">The `ReorderList` control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="82ecf-111">リストの現在の順序は、サーバーで保持されている必要があります。</span><span class="sxs-lookup"><span data-stu-id="82ecf-111">The current order of the list shall be persisted on the server.</span></span>

## <a name="steps"></a><span data-ttu-id="82ecf-112">手順</span><span class="sxs-lookup"><span data-stu-id="82ecf-112">Steps</span></span>

<span data-ttu-id="82ecf-113">`ReorderList` コントロールでは、データベースからリストへのデータのバインドがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="82ecf-113">The `ReorderList` control supports binding data from a database to the list.</span></span> <span data-ttu-id="82ecf-114">また、リスト要素の順序に対する変更をデータストアに書き戻すこともできます。</span><span class="sxs-lookup"><span data-stu-id="82ecf-114">Best of all, it also supports writing changes to the order of the list element back to the data store.</span></span>

<span data-ttu-id="82ecf-115">このサンプルでは、データストアとして Microsoft SQL Server 2005 Express Edition を使用します。</span><span class="sxs-lookup"><span data-stu-id="82ecf-115">This sample uses Microsoft SQL Server 2005 Express Edition as the data store.</span></span> <span data-ttu-id="82ecf-116">データベースは、Visual Studio のインストールにおいて、express edition を含む省略可能な (無料の) 部分です。</span><span class="sxs-lookup"><span data-stu-id="82ecf-116">The database is an optional (and free) part of a Visual Studio installation, including express edition.</span></span> <span data-ttu-id="82ecf-117">また、 [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064)で個別にダウンロードすることもできます。</span><span class="sxs-lookup"><span data-stu-id="82ecf-117">It is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="82ecf-118">このサンプルでは、SQL Server 2005 Express Edition のインスタンスが `SQLEXPRESS` 呼び出され、web サーバーと同じコンピューター上に存在することを前提としています。これは、既定のセットアップでもあります。</span><span class="sxs-lookup"><span data-stu-id="82ecf-118">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="82ecf-119">セットアップが異なる場合は、データベースの接続情報を調整する必要があります。</span><span class="sxs-lookup"><span data-stu-id="82ecf-119">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="82ecf-120">データベースをセットアップする最も簡単な方法は、Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en) ) を使用することです。</span><span class="sxs-lookup"><span data-stu-id="82ecf-120">The easiest way to set up the database is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en) ).</span></span> <span data-ttu-id="82ecf-121">サーバーに接続し、`Databases` をダブルクリックして、新しいデータベースを作成します (右クリックして [`New Database`] を選択し `Tutorials`)。</span><span class="sxs-lookup"><span data-stu-id="82ecf-121">Connect to the server, double-click on `Databases` and create a new database (right-click and choose `New Database`) called `Tutorials`.</span></span>

<span data-ttu-id="82ecf-122">このデータベースで、次の4つの列を含む `AJAX` という名前の新しいテーブルを作成します。</span><span class="sxs-lookup"><span data-stu-id="82ecf-122">In this database, create a new table called `AJAX` with the following four columns:</span></span>

- <span data-ttu-id="82ecf-123">`id` (主キー、整数、id、NULL 以外)</span><span class="sxs-lookup"><span data-stu-id="82ecf-123">`id` (primary key, integer, identity, not NULL)</span></span>
- <span data-ttu-id="82ecf-124">`char` (char (1)、NULL)</span><span class="sxs-lookup"><span data-stu-id="82ecf-124">`char` (char(1), NULL)</span></span>
- <span data-ttu-id="82ecf-125">`description` (varchar (50)、NULL)</span><span class="sxs-lookup"><span data-stu-id="82ecf-125">`description` (varchar(50), NULL)</span></span>
- <span data-ttu-id="82ecf-126">`position` (int, NULL)</span><span class="sxs-lookup"><span data-stu-id="82ecf-126">`position` (int, NULL)</span></span>

<span data-ttu-id="82ecf-127">[AJAX テーブルのレイアウトの ![](drag-and-drop-via-reorderlist-cs/_static/image2.png)](drag-and-drop-via-reorderlist-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="82ecf-127">[![The layout of the AJAX table](drag-and-drop-via-reorderlist-cs/_static/image2.png)](drag-and-drop-via-reorderlist-cs/_static/image1.png)</span></span>

<span data-ttu-id="82ecf-128">AJAX テーブルのレイアウト ([クリックすると、フルサイズの画像が表示](drag-and-drop-via-reorderlist-cs/_static/image3.png)されます)</span><span class="sxs-lookup"><span data-stu-id="82ecf-128">The layout of the AJAX table ([Click to view full-size image](drag-and-drop-via-reorderlist-cs/_static/image3.png))</span></span>

<span data-ttu-id="82ecf-129">次に、テーブルにいくつかの値を入力します。</span><span class="sxs-lookup"><span data-stu-id="82ecf-129">Next, fill the table with a couple of values.</span></span> <span data-ttu-id="82ecf-130">`position` 列には、要素の並べ替え順序が保持されていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="82ecf-130">Note that the `position` column holds the sort order of the elements.</span></span>

<span data-ttu-id="82ecf-131">[AJAX テーブルの初期データの ![](drag-and-drop-via-reorderlist-cs/_static/image5.png)](drag-and-drop-via-reorderlist-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="82ecf-131">[![The initial data in the AJAX table](drag-and-drop-via-reorderlist-cs/_static/image5.png)](drag-and-drop-via-reorderlist-cs/_static/image4.png)</span></span>

<span data-ttu-id="82ecf-132">AJAX テーブルの初期データ ([クリックすると、フルサイズの画像が表示](drag-and-drop-via-reorderlist-cs/_static/image6.png)されます)</span><span class="sxs-lookup"><span data-stu-id="82ecf-132">The initial data in the AJAX table ([Click to view full-size image](drag-and-drop-via-reorderlist-cs/_static/image6.png))</span></span>

<span data-ttu-id="82ecf-133">次の手順では、新しいデータベースとそのテーブルと通信するために `SqlDataSource` コントロールを生成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="82ecf-133">The next step requires to generate an `SqlDataSource` control to communicate with the new database and its table.</span></span> <span data-ttu-id="82ecf-134">データソースでは、`SELECT` および `UPDATE` SQL コマンドがサポートされている必要があります。</span><span class="sxs-lookup"><span data-stu-id="82ecf-134">The data source must support the `SELECT` and `UPDATE` SQL commands.</span></span> <span data-ttu-id="82ecf-135">リスト要素の順序が変更されると、`ReorderList` コントロールは、新しい位置と要素の ID の2つの値を、データソースの `Update` コマンドに自動的に送信します。</span><span class="sxs-lookup"><span data-stu-id="82ecf-135">When the order of the list elements is later changed, the `ReorderList` control automatically submits two values to the data source's `Update` command: the new position and the ID of the element.</span></span> <span data-ttu-id="82ecf-136">そのため、データソースには、次の2つの値の `<UpdateParameters>` セクションが必要です。</span><span class="sxs-lookup"><span data-stu-id="82ecf-136">Therefore, the data source needs an `<UpdateParameters>` section for these two values:</span></span>

[!code-aspx[Main](drag-and-drop-via-reorderlist-cs/samples/sample1.aspx)]

<span data-ttu-id="82ecf-137">`ReorderList` コントロールでは、次の属性を設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="82ecf-137">The `ReorderList` control needs to set the following attributes:</span></span>

- <span data-ttu-id="82ecf-138">`AllowReorder`: リスト項目を並べ替えることができるかどうか</span><span class="sxs-lookup"><span data-stu-id="82ecf-138">`AllowReorder`: Whether the list items may be rearranged</span></span>
- <span data-ttu-id="82ecf-139">`DataSourceID`: データソースの ID</span><span class="sxs-lookup"><span data-stu-id="82ecf-139">`DataSourceID`: The ID of the data source</span></span>
- <span data-ttu-id="82ecf-140">`DataKeyField`: データソースの主キー列の名前</span><span class="sxs-lookup"><span data-stu-id="82ecf-140">`DataKeyField`: The name of the primary key column in the data source</span></span>
- <span data-ttu-id="82ecf-141">`SortOrderField`: リスト項目の並べ替え順序を提供するデータソース列</span><span class="sxs-lookup"><span data-stu-id="82ecf-141">`SortOrderField`: The data source column that provides the sort order for the list items</span></span>

<span data-ttu-id="82ecf-142">`<DragHandleTemplate>` セクションと `<ItemTemplate>` セクションでは、一覧のレイアウトを微調整できます。</span><span class="sxs-lookup"><span data-stu-id="82ecf-142">In the `<DragHandleTemplate>` and `<ItemTemplate>` sections, the layout of the list can be fine-tuned.</span></span> <span data-ttu-id="82ecf-143">また、次に示すように、`Eval()` メソッドを使用してデータバインディングを行うこともできます。</span><span class="sxs-lookup"><span data-stu-id="82ecf-143">Also, databinding is possible using the `Eval()` method, as seen here:</span></span>

[!code-aspx[Main](drag-and-drop-via-reorderlist-cs/samples/sample2.aspx)]

<span data-ttu-id="82ecf-144">次の CSS スタイル情報 (`ReorderList` コントロールの `<DragHandleTemplate>` セクションで参照) を使用すると、ドラッグハンドルの上にマウスポインターを置いたときに、マウスポインターが適切に変化します。</span><span class="sxs-lookup"><span data-stu-id="82ecf-144">The following CSS style information (referenced in the `<DragHandleTemplate>` section of the `ReorderList` control) makes sure that the mouse pointer changes appropriately when it hovers over the drag handle:</span></span>

[!code-css[Main](drag-and-drop-via-reorderlist-cs/samples/sample3.css)]

<span data-ttu-id="82ecf-145">最後に、`ScriptManager` コントロールによって、ページの ASP.NET AJAX が初期化されます。</span><span class="sxs-lookup"><span data-stu-id="82ecf-145">Finally, a `ScriptManager` control initializes ASP.NET AJAX for the page:</span></span>

[!code-aspx[Main](drag-and-drop-via-reorderlist-cs/samples/sample4.aspx)]

<span data-ttu-id="82ecf-146">ブラウザーでこの例を実行し、リスト項目を1つのビットに再配置します。</span><span class="sxs-lookup"><span data-stu-id="82ecf-146">Run this example in the browser and rearrange the list items a bit.</span></span> <span data-ttu-id="82ecf-147">次に、ページを再読み込みするか、データベースを確認します。</span><span class="sxs-lookup"><span data-stu-id="82ecf-147">Then, reload the page and/or have a look at the database.</span></span> <span data-ttu-id="82ecf-148">変更された位置が保持され、データベースの [`position`] 列の値と、マークアップを使用するだけで、すべてのコードが含まれていなくても反映されます。</span><span class="sxs-lookup"><span data-stu-id="82ecf-148">The altered positions have been maintained and are also reflected by the values in the `position` column in the database and that all without any code, just by using markup.</span></span>

<span data-ttu-id="82ecf-149">[データベース内のデータが新しいリストアイテムの順序に従って変更 ![](drag-and-drop-via-reorderlist-cs/_static/image8.png)](drag-and-drop-via-reorderlist-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="82ecf-149">[![The data in the database changes according to the new list item order](drag-and-drop-via-reorderlist-cs/_static/image8.png)](drag-and-drop-via-reorderlist-cs/_static/image7.png)</span></span>

<span data-ttu-id="82ecf-150">データベース内のデータは、新しいリスト項目の順序に従って変更されます ([クリックすると、フルサイズの画像が表示](drag-and-drop-via-reorderlist-cs/_static/image9.png)されます)</span><span class="sxs-lookup"><span data-stu-id="82ecf-150">The data in the database changes according to the new list item order ([Click to view full-size image](drag-and-drop-via-reorderlist-cs/_static/image9.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="82ecf-151">[前へ](using-postbacks-with-reorderlist-cs.md)
> [次へ](using-postbacks-with-reorderlist-vb.md)</span><span class="sxs-lookup"><span data-stu-id="82ecf-151">[Previous](using-postbacks-with-reorderlist-cs.md)
[Next](using-postbacks-with-reorderlist-vb.md)</span></span>
