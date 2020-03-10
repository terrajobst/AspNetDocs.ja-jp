---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-after-each-other-cs
title: 複数のアニメーションを相互に実行C#する () |Microsoft Docs
author: wenz
description: ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。 これにより、を実行できます...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 7dc02b18-2b5d-4844-b7c5-cbd818477163
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-after-each-other-cs
msc.type: authoredcontent
ms.openlocfilehash: e378ac038796dbd44e89d099532b9e186dcf673f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78497824"
---
# <a name="executing-several-animations-after-each-other-c"></a>複数のアニメーションを順番に実行する (C#)

[Christian Wenz](https://github.com/wenz)別

[コードのダウンロード](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation3.cs.zip)または[PDF のダウンロード](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation3CS.pdf)

> ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。 複数のアニメーションを1つずつ実行できます。

ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。 複数のアニメーションを1つずつ実行できます。

## <a name="steps"></a>手順

まず、ページに `ScriptManager` を含めます。次に、ASP.NET AJAX ライブラリが読み込まれ、Control Toolkit を使用できるようになります。

[!code-aspx[Main](executing-several-animations-after-each-other-cs/samples/sample1.aspx)]

アニメーションは、次のようなテキストパネルに適用されます。

[!code-aspx[Main](executing-several-animations-after-each-other-cs/samples/sample2.aspx)]

パネルに関連付けられている CSS クラスで、優れた背景色を定義し、パネルに固定幅を設定します。

[!code-css[Main](executing-several-animations-after-each-other-cs/samples/sample3.css)]

次に、`ID`、`TargetControlID` 属性、および加えるを指定して、ページに `AnimationExtender` を追加し `runat="server":`

[!code-aspx[Main](executing-several-animations-after-each-other-cs/samples/sample4.aspx)]

ページが完全に読み込まれたら、[`<Animations>`] ノードで `<OnLoad>` を使用してアニメーションを実行します。 通常、`<OnLoad>` は1つのアニメーションのみを受け入れます。 Animation framework では、`<Sequence>` 要素を使用して複数のアニメーションを1つに結合できます。 `<Sequence>` 内のすべてのアニメーションが1つずつ実行されます。 `AnimationExtender` コントロールのマークアップを次に示します。まず、パネルの幅を広げ、その高さを小さくします。

[!code-aspx[Main](executing-several-animations-after-each-other-cs/samples/sample5.aspx)]

このスクリプトを実行すると、最初にパネルの幅が広くなり、小さくなります。

[最初 ![幅が増加しています](executing-several-animations-after-each-other-cs/_static/image2.png)](executing-several-animations-after-each-other-cs/_static/image1.png)

最初に幅が増加します ([クリックすると、フルサイズの画像が表示](executing-several-animations-after-each-other-cs/_static/image3.png)されます)

[![高さを下げる](executing-several-animations-after-each-other-cs/_static/image5.png)](executing-several-animations-after-each-other-cs/_static/image4.png)

次に、高さを下げます ([クリックすると、フルサイズの画像が表示](executing-several-animations-after-each-other-cs/_static/image6.png)されます)

> [!div class="step-by-step"]
> [前へ](executing-several-animations-at-the-same-time-cs.md)
> [次へ](animation-depending-on-a-condition-cs.md)
