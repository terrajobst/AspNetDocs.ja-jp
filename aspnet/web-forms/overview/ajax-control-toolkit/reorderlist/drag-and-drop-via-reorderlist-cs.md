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
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78446008"
---
# <a name="drag-and-drop-via-reorderlist-c"></a>ReorderList 経由でドラッグ アンド ドロップする (C#)

[Christian Wenz](https://github.com/wenz)別

[コードのダウンロード](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList5.cs.zip)または[PDF のダウンロード](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist5CS.pdf)

> AJAX コントロールツールキットの ReorderList コントロールは、ドラッグアンドドロップを使用してユーザーが並べ替えることのできるリストを提供します。 リストの現在の順序は、サーバーで保持されている必要があります。

## <a name="overview"></a>概要

AJAX コントロールツールキットの `ReorderList` コントロールには、ドラッグアンドドロップを使用してユーザーが並べ替えることのできるリストが用意されています。 リストの現在の順序は、サーバーで保持されている必要があります。

## <a name="steps"></a>手順

`ReorderList` コントロールでは、データベースからリストへのデータのバインドがサポートされています。 また、リスト要素の順序に対する変更をデータストアに書き戻すこともできます。

このサンプルでは、データストアとして Microsoft SQL Server 2005 Express Edition を使用します。 データベースは、Visual Studio のインストールにおいて、express edition を含む省略可能な (無料の) 部分です。 また、 [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064)で個別にダウンロードすることもできます。 このサンプルでは、SQL Server 2005 Express Edition のインスタンスが `SQLEXPRESS` 呼び出され、web サーバーと同じコンピューター上に存在することを前提としています。これは、既定のセットアップでもあります。 セットアップが異なる場合は、データベースの接続情報を調整する必要があります。

データベースをセットアップする最も簡単な方法は、Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en) ) を使用することです。 サーバーに接続し、`Databases` をダブルクリックして、新しいデータベースを作成します (右クリックして [`New Database`] を選択し `Tutorials`)。

このデータベースで、次の4つの列を含む `AJAX` という名前の新しいテーブルを作成します。

- `id` (主キー、整数、id、NULL 以外)
- `char` (char (1)、NULL)
- `description` (varchar (50)、NULL)
- `position` (int, NULL)

[AJAX テーブルのレイアウトの ![](drag-and-drop-via-reorderlist-cs/_static/image2.png)](drag-and-drop-via-reorderlist-cs/_static/image1.png)

AJAX テーブルのレイアウト ([クリックすると、フルサイズの画像が表示](drag-and-drop-via-reorderlist-cs/_static/image3.png)されます)

次に、テーブルにいくつかの値を入力します。 `position` 列には、要素の並べ替え順序が保持されていることに注意してください。

[AJAX テーブルの初期データの ![](drag-and-drop-via-reorderlist-cs/_static/image5.png)](drag-and-drop-via-reorderlist-cs/_static/image4.png)

AJAX テーブルの初期データ ([クリックすると、フルサイズの画像が表示](drag-and-drop-via-reorderlist-cs/_static/image6.png)されます)

次の手順では、新しいデータベースとそのテーブルと通信するために `SqlDataSource` コントロールを生成する必要があります。 データソースでは、`SELECT` および `UPDATE` SQL コマンドがサポートされている必要があります。 リスト要素の順序が変更されると、`ReorderList` コントロールは、新しい位置と要素の ID の2つの値を、データソースの `Update` コマンドに自動的に送信します。 そのため、データソースには、次の2つの値の `<UpdateParameters>` セクションが必要です。

[!code-aspx[Main](drag-and-drop-via-reorderlist-cs/samples/sample1.aspx)]

`ReorderList` コントロールでは、次の属性を設定する必要があります。

- `AllowReorder`: リスト項目を並べ替えることができるかどうか
- `DataSourceID`: データソースの ID
- `DataKeyField`: データソースの主キー列の名前
- `SortOrderField`: リスト項目の並べ替え順序を提供するデータソース列

`<DragHandleTemplate>` セクションと `<ItemTemplate>` セクションでは、一覧のレイアウトを微調整できます。 また、次に示すように、`Eval()` メソッドを使用してデータバインディングを行うこともできます。

[!code-aspx[Main](drag-and-drop-via-reorderlist-cs/samples/sample2.aspx)]

次の CSS スタイル情報 (`ReorderList` コントロールの `<DragHandleTemplate>` セクションで参照) を使用すると、ドラッグハンドルの上にマウスポインターを置いたときに、マウスポインターが適切に変化します。

[!code-css[Main](drag-and-drop-via-reorderlist-cs/samples/sample3.css)]

最後に、`ScriptManager` コントロールによって、ページの ASP.NET AJAX が初期化されます。

[!code-aspx[Main](drag-and-drop-via-reorderlist-cs/samples/sample4.aspx)]

ブラウザーでこの例を実行し、リスト項目を1つのビットに再配置します。 次に、ページを再読み込みするか、データベースを確認します。 変更された位置が保持され、データベースの [`position`] 列の値と、マークアップを使用するだけで、すべてのコードが含まれていなくても反映されます。

[データベース内のデータが新しいリストアイテムの順序に従って変更 ![](drag-and-drop-via-reorderlist-cs/_static/image8.png)](drag-and-drop-via-reorderlist-cs/_static/image7.png)

データベース内のデータは、新しいリスト項目の順序に従って変更されます ([クリックすると、フルサイズの画像が表示](drag-and-drop-via-reorderlist-cs/_static/image9.png)されます)

> [!div class="step-by-step"]
> [前へ](using-postbacks-with-reorderlist-cs.md)
> [次へ](using-postbacks-with-reorderlist-vb.md)
