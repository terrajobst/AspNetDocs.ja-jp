---
uid: web-forms/overview/ajax-control-toolkit/dropshadow/adjusting-the-z-index-of-a-dropshadow-cs
title: DropShadow の Z インデックスを調整する (C#) |Microsoft Docs
author: wenz
description: AJAX コントロールツールキットの DropShadow コントロールは、ドロップシャドウを持つパネルを拡張します。 ただし、この影は、他のコントロールと競合することがあります。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 14133833-e518-4347-87b9-6b6f71f14a77
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dropshadow/adjusting-the-z-index-of-a-dropshadow-cs
msc.type: authoredcontent
ms.openlocfilehash: 12bc7f0430f1f30ff964cd9547ee1e9b0aa7423c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78497482"
---
# <a name="adjusting-the-z-index-of-a-dropshadow-c"></a>DropShadow の Z インデックスを調整する (C#)

[Christian Wenz](https://github.com/wenz)別

[コードのダウンロード](https://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow1.cs.zip)または[PDF のダウンロード](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow1CS.pdf)

> AJAX コントロールツールキットの DropShadow コントロールは、ドロップシャドウを持つパネルを拡張します。 ただし、この影は、ASP.NET Menu コントロールなど、他のコントロールと競合することがあります。 メニューエントリがポップアップ表示されると、ドロップシャドウの背後に表示されます。

## <a name="overview"></a>概要

AJAX コントロールツールキットの DropShadow コントロールは、ドロップシャドウを持つパネルを拡張します。 ただし、この影は、ASP.NET Menu コントロールなど、他のコントロールと競合することがあります。 メニューエントリがポップアップ表示されると、ドロップシャドウの背後に表示されます。

## <a name="steps"></a>手順

コードはパネル自体で開始されます。これにより、パネルには、効果を表示するのに十分なテキストが含まれるようになります。

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample1.aspx)]

`panelShadow` パネルの直前に別のパネルが配置されます。 メニュー項目が [`dropShadow`] パネルの上 (または下) に表示されるように、横方向のメニューが含まれています。

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample2.aspx)]

次に、`DropShadowExtender` を追加して、ドロップシャドウ効果を持つ `panelShadow` パネルを拡張します。

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample3.aspx)]

最後に、ASP.NET AJAX `ScriptManager` コントロールを使用して、コントロールツールキットを機能させることができます。

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample4.aspx)]

このスクリプトを実行すると、メニューエントリがパネルの下に表示されます。 ただし、メニューでは CSS クラス `panel` を使用します。ここでは、要素を他のパネルの前面に表示するために、次の2つの項目を定義する必要があります。

- 相対配置
- 正の z インデックス

[!code-css[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample5.css)]

その後、`DropShadowExtender` コントロールがメニューコントロールと競合しないようになります。

[![の前: メニューエントリは表示されません](adjusting-the-z-index-of-a-dropshadow-cs/_static/image2.png)](adjusting-the-z-index-of-a-dropshadow-cs/_static/image1.png)

[前]: メニューエントリは表示されません ([クリックすると、フルサイズの画像が表示](adjusting-the-z-index-of-a-dropshadow-cs/_static/image3.png)されます)

[![後: メニュー項目が表示されます。](adjusting-the-z-index-of-a-dropshadow-cs/_static/image5.png)](adjusting-the-z-index-of-a-dropshadow-cs/_static/image4.png)

[完了]: メニューエントリが表示されます ([クリックすると、フルサイズの画像が表示](adjusting-the-z-index-of-a-dropshadow-cs/_static/image6.png)されます)

> [!div class="step-by-step"]
> [Next](manipulating-dropshadow-properties-from-client-code-cs.md)
