---
uid: web-forms/overview/ajax-control-toolkit/dropshadow/manipulating-dropshadow-properties-from-client-code-cs
title: クライアントコードから DropShadow プロパティを操作C#する () |Microsoft Docs
author: wenz
description: DataList の編集インターフェイスのカスタマイズ
ms.author: riande
ms.date: 06/02/2008
ms.assetid: c83ca3e6-c0bf-4158-a166-40c1ab0f33da
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dropshadow/manipulating-dropshadow-properties-from-client-code-cs
msc.type: authoredcontent
ms.openlocfilehash: 790f0d881e43518600968d6c175d4eaa53d0e5f9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78497428"
---
# <a name="manipulating-dropshadow-properties-from-client-code-c"></a>クライアント コードから DropShadow プロパティを操作する (C#)

[Christian Wenz](https://github.com/wenz)別

[コードのダウンロード](https://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow2.cs.zip)または[PDF のダウンロード](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow2CS.pdf)

> AJAX コントロールツールキットの DropShadow コントロールは、ドロップシャドウを持つパネルを拡張します。 このエクステンダーのプロパティは、クライアントの JavaScript コードを使用して変更することもできます。

## <a name="overview"></a>概要

AJAX コントロールツールキットの DropShadow コントロールは、ドロップシャドウを持つパネルを拡張します。 このエクステンダーのプロパティは、クライアントの JavaScript コードを使用して変更することもできます。

## <a name="steps"></a>手順

コードは、次のようなテキスト行を含むパネルから始まります。

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample1.aspx)]

関連付けられている CSS クラスは、パネルに優れた背景色を与えます。

[!code-css[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample2.css)]

ドロップシャドウ効果を設定し、不透明度を50% に設定して、パネルを拡張する `DropShadowExtender` が追加されます。

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample3.aspx)]

次に、ASP.NET AJAX `ScriptManager` コントロールを使用して、コントロールツールキットを機能させることができます。

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample4.aspx)]

別のパネルには、ドロップシャドウの不透明度を設定するための JavaScript リンクが2つあります。マイナスリンクを使用すると影の不透明度が下がり、プラスリンクを使用すると、影の不透明度が上がります。

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample5.aspx)]

JavaScript 関数 `changeOpacity()` は、まずページの `DropShadowExtender` コントロールを検索する必要があります。 ASP.NET AJAX は、そのタスクの `$find()` メソッドを定義します。 次に、`get_Opacity()` メソッドは現在の不透明度を取得し、`set_Opacity()` メソッドはそれを設定します。 次に、JavaScript コードによって、現在の不透明度の値が `<label>` 要素に配置されます。

[!code-html[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample6.html)]

[不透明度がクライアント側で変更さ ![](manipulating-dropshadow-properties-from-client-code-cs/_static/image2.png)](manipulating-dropshadow-properties-from-client-code-cs/_static/image1.png)

不透明度がクライアント側で変更されます ([クリックすると、フルサイズの画像が表示](manipulating-dropshadow-properties-from-client-code-cs/_static/image3.png)されます)

> [!div class="step-by-step"]
> [前へ](adjusting-the-z-index-of-a-dropshadow-cs.md)
> [次へ](adjusting-the-z-index-of-a-dropshadow-vb.md)
