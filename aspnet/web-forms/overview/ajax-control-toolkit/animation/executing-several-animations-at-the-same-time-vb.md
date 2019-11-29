---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-at-the-same-time-vb
title: 複数のアニメーションを同時に実行する (VB) |Microsoft Docs
author: wenz
description: ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。 これにより、を実行できます...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 2469f7ea-1489-42fb-a8e1-414c90141ce9
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-at-the-same-time-vb
msc.type: authoredcontent
ms.openlocfilehash: fc11debd06c897c29db56d42167d483f5608cdf8
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74575305"
---
# <a name="executing-several-animations-at-the-same-time-vb"></a>複数のアニメーションを同時に実行する (VB)

[Christian Wenz](https://github.com/wenz)別

[コードのダウンロード](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation2.vb.zip)または[PDF のダウンロード](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation2VB.pdf)

> ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。 を使用すると、複数のアニメーションを並行して実行できます。

## <a name="overview"></a>の概要

ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。 を使用すると、複数のアニメーションを並行して実行できます。

## <a name="steps"></a>手順

まず、ページに `ScriptManager` を含めます。次に、ASP.NET AJAX ライブラリが読み込まれ、Control Toolkit を使用できるようになります。

[!code-aspx[Main](executing-several-animations-at-the-same-time-vb/samples/sample1.aspx)]

アニメーションは、次のようなテキストパネルに適用されます。

[!code-aspx[Main](executing-several-animations-at-the-same-time-vb/samples/sample2.aspx)]

パネルに関連付けられている CSS クラスで、優れた背景色を定義し、パネルに固定幅を設定します。

[!code-css[Main](executing-several-animations-at-the-same-time-vb/samples/sample3.css)]

次に、`ID`、`TargetControlID` 属性、および加える `runat="server"`を指定して、ページに `AnimationExtender` を追加します。

[!code-aspx[Main](executing-several-animations-at-the-same-time-vb/samples/sample4.aspx)]

ページが完全に読み込まれたら、[`<Animations>`] ノードで `<OnLoad>` を使用してアニメーションを実行します。 通常、`<OnLoad>` は1つのアニメーションのみを受け入れます。 Animation framework では、`<Parallel>` 要素を使用して複数のアニメーションを1つに結合できます。 `<Parallel>` 内のすべてのアニメーションが同時に実行されます。

`AnimationExtender` コントロールのマークアップを次に示します。同時にパネルをフェードアウトし、サイズを変更します。

[!code-aspx[Main](executing-several-animations-at-the-same-time-vb/samples/sample5.aspx)]

実際には、このスクリプトを実行すると、パネルが表示され、サイズが変更され (幅が tripling、高さが半分に)、同時にフェードアウトします。

[ブラウザーのレンダリングエンジンにより、パネルのフェードアウトとサイズ変更 (コンテンツを含む) ![](executing-several-animations-at-the-same-time-vb/_static/image2.png)](executing-several-animations-at-the-same-time-vb/_static/image1.png)

パネルのフェードアウトとサイズ変更 (ブラウザーのレンダリングエンジンにより、コンテンツを含む) が表示されます ([クリックすると、フルサイズの画像が表示](executing-several-animations-at-the-same-time-vb/_static/image3.png)されます)

> [!div class="step-by-step"]
> [前へ](adding-animation-to-a-control-vb.md)
> [次へ](executing-several-animations-after-each-other-vb.md)
