---
uid: web-forms/overview/ajax-control-toolkit/animation/animating-in-response-to-user-interaction-vb
title: ユーザーの操作に応答してアニメーション化する (VB) |Microsoft Docs
author: wenz
description: ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。 アニメーションは星型にすることができます...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: c8204c05-ec27-40fe-933d-88e4e727a482
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animating-in-response-to-user-interaction-vb
msc.type: authoredcontent
ms.openlocfilehash: 629d79505cebd49c2f05333bfbf78166f80fc6cb
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78497926"
---
# <a name="animating-in-response-to-user-interaction-vb"></a>ユーザー操作に対してアニメーションを返す (VB)

[Christian Wenz](https://github.com/wenz)別

[コードのダウンロード](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation6.vb.zip)または[PDF のダウンロード](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation6VB.pdf)

> ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。 アニメーションは、自動的に開始することも、ユーザーの操作によってトリガーすることもできます。たとえば、マウスを使用してをクリックします。

## <a name="overview"></a>概要

ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。 アニメーションは、自動的に開始することも、ユーザーの操作によってトリガーすることもできます。たとえば、マウスを使用してをクリックします。

## <a name="steps"></a>手順

まず、ページに `ScriptManager` を含めます。次に、ASP.NET AJAX ライブラリが読み込まれ、Control Toolkit を使用できるようになります。

[!code-aspx[Main](animating-in-response-to-user-interaction-vb/samples/sample1.aspx)]

アニメーションは、次のようなテキストパネルに適用されます。

[!code-aspx[Main](animating-in-response-to-user-interaction-vb/samples/sample2.aspx)]

パネルに関連付けられている CSS クラスで、優れた背景色を定義し、パネルに固定幅を設定します。

[!code-css[Main](animating-in-response-to-user-interaction-vb/samples/sample3.css)]

次に、`ID`、`TargetControlID` 属性、および加える `runat="server"`を指定して、ページに `AnimationExtender` を追加します。

[!code-aspx[Main](animating-in-response-to-user-interaction-vb/samples/sample4.aspx)]

[`<Animations>`] ノードには、ユーザーの操作によってアニメーションを開始する5つの方法があります (missing 要素は、ページ全体が完全に読み込まれた後に実行される `<OnLoad>`)。

- `<OnClick>` (コントロール上でマウスをクリック)
- `<OnHoverOut>` (マウスをコントロールから離す)
- `<OnHoverOver>` (マウスポインターをコントロールの上に置くと、`<OnHoverOut>` アニメーションが停止します)
- `<OnMouseOut>` (マウスをコントロールから離す)
- `<OnMouseOver>` (マウスポインターをコントロールの上に置くと、`<OnMouseOut>` アニメーションは停止しません)

このシナリオでは、`<OnClick>` が使用されます。 ユーザーがパネルをクリックすると、サイズが変更され、同時にフェードアウトします。

[!code-aspx[Main](animating-in-response-to-user-interaction-vb/samples/sample5.aspx)]

[マウスクリックによってアニメーションが開始 ![](animating-in-response-to-user-interaction-vb/_static/image2.png)](animating-in-response-to-user-interaction-vb/_static/image1.png)

マウスクリックでアニメーションが開始されます ([クリックすると、フルサイズの画像が表示](animating-in-response-to-user-interaction-vb/_static/image3.png)されます)

> [!div class="step-by-step"]
> [前へ](picking-one-animation-out-of-a-list-vb.md)
> [次へ](disabling-actions-during-animation-vb.md)
