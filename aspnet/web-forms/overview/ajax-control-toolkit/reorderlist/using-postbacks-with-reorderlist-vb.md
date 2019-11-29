---
uid: web-forms/overview/ajax-control-toolkit/reorderlist/using-postbacks-with-reorderlist-vb
title: ReorderList でポストバックを使用する (VB) |Microsoft Docs
author: wenz
description: AJAX コントロールツールキットの ReorderList コントロールは、ドラッグアンドドロップを使用してユーザーが並べ替えることのできるリストを提供します。 リストが並べ替えられるたびに、po...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e5b6ed70-19ed-4024-ba4f-6d78e8acdc0f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/reorderlist/using-postbacks-with-reorderlist-vb
msc.type: authoredcontent
ms.openlocfilehash: 5d6075e40df2c32df6c0d801243eff98fa7790b2
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74611366"
---
# <a name="using-postbacks-with-reorderlist-vb"></a>ReorderList でポストバックを使用する (VB)

[Christian Wenz](https://github.com/wenz)別

[コードのダウンロード](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList4.vb.zip)または[PDF のダウンロード](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist4VB.pdf)

> AJAX コントロールツールキットの ReorderList コントロールは、ドラッグアンドドロップを使用してユーザーが並べ替えることのできるリストを提供します。 リストが並べ替えられるたびに、ポストバックはサーバーに変更を通知します。

## <a name="overview"></a>の概要

AJAX コントロールツールキットの `ReorderList` コントロールには、ドラッグアンドドロップを使用してユーザーが並べ替えることのできるリストが用意されています。 リストが並べ替えられるたびに、ポストバックはサーバーに変更を通知します。

## <a name="steps"></a>手順

`ReorderList` コントロールには、いくつかのデータソースが考えられます。 1つは、`XmlDataSource` コントロールを使用する方法です。

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample1.aspx)]

この XML を `ReorderList` コントロールにバインドし、ポストバックを有効にするには、次の属性を設定する必要があります。

- `DataSourceID`: データソースの ID
- `SortOrderField`: 並べ替えの基準となるプロパティ
- `AllowReorder`: ユーザーがリスト要素の順序を変更できるようにするかどうか
- `PostBackOnReorder`: リストを再配置するたびにポストバックを作成するかどうか

次に、コントロールの適切なマークアップを示します。

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample2.aspx)]

`ReorderList` コントロール内では、`Eval()` メソッドを使用してデータソースの特定のデータをバインドできます。

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample3.aspx)]

ページ上の任意の位置で、最後の並べ替えが行われたときにラベルに情報が保持されます。

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample4.aspx)]

このラベルには、ポストバックを処理するサーバー側コードのテキストが格納されます。

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample5.aspx)]

最後に、ASP.NET AJAX と Control `ScriptManager` Toolkit の機能をアクティブ化するために、ページにコントロールを配置する必要があります。

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample6.aspx)]

[各並べ替えの ![ポストバックをトリガーする](using-postbacks-with-reorderlist-vb/_static/image2.png)](using-postbacks-with-reorderlist-vb/_static/image1.png)

各並べ替え順序によってポストバックがトリガーされる ([クリックすると、フルサイズの画像が表示](using-postbacks-with-reorderlist-vb/_static/image3.png)される)

> [!div class="step-by-step"]
> [前へ](drag-and-drop-via-reorderlist-cs.md)
> [次へ](drag-and-drop-via-reorderlist-vb.md)
