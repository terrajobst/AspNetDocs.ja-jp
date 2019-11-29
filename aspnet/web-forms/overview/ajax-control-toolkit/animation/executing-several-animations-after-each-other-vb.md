---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-after-each-other-vb
title: 複数のアニメーションの実行 (VB) |Microsoft Docs
author: wenz
description: ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。 これにより、を実行できます...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 21ece509-79cc-4d9d-892d-7b6e9c4d3502
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-after-each-other-vb
msc.type: authoredcontent
ms.openlocfilehash: 5034fe905299d4559b713dd841cb166886179c39
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74606850"
---
# <a name="executing-several-animations-after-each-other-vb"></a>複数のアニメーションを順番に実行する (VB)

[Christian Wenz](https://github.com/wenz)別

[コードのダウンロード](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation3.vb.zip)または[PDF のダウンロード](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation3VB.pdf)

> ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。 複数のアニメーションを1つずつ実行できます。

## <a name="overview"></a>の概要

ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。 複数のアニメーションを1つずつ実行できます。

## <a name="steps"></a>手順

まず、ページに `ScriptManager` を含めます。次に、ASP.NET AJAX ライブラリが読み込まれ、Control Toolkit を使用できるようになります。

[!code-aspx[Main](executing-several-animations-after-each-other-vb/samples/sample1.aspx)]

アニメーションは、次のようなテキストパネルに適用されます。

[!code-aspx[Main](executing-several-animations-after-each-other-vb/samples/sample2.aspx)]

パネルに関連付けられている CSS クラスで、優れた背景色を定義し、パネルに固定幅を設定します。

[!code-css[Main](executing-several-animations-after-each-other-vb/samples/sample3.css)]

次に、`ID`、`TargetControlID` 属性、および加えるを指定して、ページに `AnimationExtender` を追加し `runat="server":`

[!code-aspx[Main](executing-several-animations-after-each-other-vb/samples/sample4.aspx)]

ページが完全に読み込まれたら、[`<Animations>`] ノードで `<OnLoad>` を使用してアニメーションを実行します。 通常、`<OnLoad>` は1つのアニメーションのみを受け入れます。 Animation framework では、`<Sequence>` 要素を使用して複数のアニメーションを1つに結合できます。 `<Sequence>` 内のすべてのアニメーションが1つずつ実行されます。 `AnimationExtender` コントロールのマークアップを次に示します。まず、パネルの幅を広げ、その高さを小さくします。

[!code-aspx[Main](executing-several-animations-after-each-other-vb/samples/sample5.aspx)]

このスクリプトを実行すると、最初にパネルの幅が広くなり、小さくなります。

[最初 ![幅が増加しています](executing-several-animations-after-each-other-vb/_static/image2.png)](executing-several-animations-after-each-other-vb/_static/image1.png)

最初に幅が増加します ([クリックすると、フルサイズの画像が表示](executing-several-animations-after-each-other-vb/_static/image3.png)されます)

[![高さを下げる](executing-several-animations-after-each-other-vb/_static/image5.png)](executing-several-animations-after-each-other-vb/_static/image4.png)

次に、高さを下げます ([クリックすると、フルサイズの画像が表示](executing-several-animations-after-each-other-vb/_static/image6.png)されます)

> [!div class="step-by-step"]
> [前へ](executing-several-animations-at-the-same-time-vb.md)
> [次へ](animation-depending-on-a-condition-vb.md)
