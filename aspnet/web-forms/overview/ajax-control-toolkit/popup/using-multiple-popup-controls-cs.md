---
uid: web-forms/overview/ajax-control-toolkit/popup/using-multiple-popup-controls-cs
title: 複数のポップアップコントロールをC#使用する () |Microsoft Docs
author: wenz
description: AJAX Control Toolkit の PopupControl extender は、他のコントロールがアクティブになったときにポップアップをトリガーする簡単な方法を提供します。 また、m...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 91511b0b-311d-481f-9e7c-73f07b813b79
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/using-multiple-popup-controls-cs
msc.type: authoredcontent
ms.openlocfilehash: 8700fe89af591e8b481e853580b0efa0cddbf1bc
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74611640"
---
# <a name="using-multiple-popup-controls-c"></a>複数のポップアップ コントロールを使用する (C#)

[Christian Wenz](https://github.com/wenz)別

[コードのダウンロード](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl1.cs.zip)または[PDF のダウンロード](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol1CS.pdf)

> AJAX Control Toolkit の PopupControl extender は、他のコントロールがアクティブになったときにポップアップをトリガーする簡単な方法を提供します。 1つのページで複数のポップアップコントロールを使用することもできます。

## <a name="overview"></a>の概要

AJAX Control Toolkit の PopupControl extender は、他のコントロールがアクティブになったときにポップアップをトリガーする簡単な方法を提供します。 1つのページで複数のポップアップコントロールを使用することもできます。

## <a name="steps"></a>手順

ASP.NET AJAX と Control Toolkit の機能をアクティブ化するには、ページの任意の場所に `ScriptManager` コントロールを配置する必要があります (`<form>` 要素内)。

[!code-aspx[Main](using-multiple-popup-controls-cs/samples/sample1.aspx)]

次に、ポップアップとして機能するパネルを追加します。 現在のシナリオでは、パネルには `Calendar` コントロールが含まれています。 カレンダーのポストバックによるページの更新を回避するために、パネルは `UpdatePanel` コントロール内に配置されます。

[!code-aspx[Main](using-multiple-popup-controls-cs/samples/sample2.aspx)]

このページには、2つのテキストボックスも含まれています。 各テキストボックスでは、テキストボックスがアクティブになるとカレンダーのポップアップが表示されます。

[!code-aspx[Main](using-multiple-popup-controls-cs/samples/sample3.aspx)]

ここで、2つのテキストボックスをそれぞれ `PopupControlExtender`に拡張します。 `TargetControlID` 属性は、エクステンダーに関連付けられているコントロールの ID を提供します。 `PopupControlID` 属性には、ポップアップパネルの ID が含まれます。 この場合、どちらのエクステンダーも同じパネルを表示しますが、異なるパネルを使用することもできます。

[!code-aspx[Main](using-multiple-popup-controls-cs/samples/sample4.aspx)]

テキストフィールド内をクリックするたびに、フィールドの下にカレンダーが表示され、日付を選択できるようになります。 (選択した日付をテキストボックスに戻すと、別のチュートリアルで説明されています)。

[ユーザーがテキストボックスをクリックしたときにカレンダーが表示される ![](using-multiple-popup-controls-cs/_static/image2.png)](using-multiple-popup-controls-cs/_static/image1.png)

ユーザーがテキストボックスをクリックするとカレンダーが表示されます ([クリックすると、フルサイズの画像が表示](using-multiple-popup-controls-cs/_static/image3.png)されます)

> [!div class="step-by-step"]
> [次へ](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs.md)
