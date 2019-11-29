---
uid: web-forms/overview/ajax-control-toolkit/animation/animating-in-response-to-user-interaction-cs
title: ユーザーの操作に応答してC#アニメーション化する () |Microsoft Docs
author: wenz
description: ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。 アニメーションは星型にすることができます...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: ea26549d-fbbf-4973-a108-b14cd1d6de26
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animating-in-response-to-user-interaction-cs
msc.type: authoredcontent
ms.openlocfilehash: d04fa680d0cd4f7fb54521ac6fbb47a2cf9a83cf
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599880"
---
# <a name="animating-in-response-to-user-interaction-c"></a>ユーザー操作に対してアニメーションを返す (C#)

[Christian Wenz](https://github.com/wenz)別

[コードのダウンロード](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation6.cs.zip)または[PDF のダウンロード](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation6CS.pdf)

> ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。 アニメーションは、自動的に開始することも、ユーザーの操作によってトリガーすることもできます。たとえば、マウスを使用してをクリックします。

## <a name="overview"></a>の概要

ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。 アニメーションは、自動的に開始することも、ユーザーの操作によってトリガーすることもできます。たとえば、マウスを使用してをクリックします。

## <a name="steps"></a>手順

まず、ページに `ScriptManager` を含めます。次に、ASP.NET AJAX ライブラリが読み込まれ、Control Toolkit を使用できるようになります。

[!code-aspx[Main](animating-in-response-to-user-interaction-cs/samples/sample1.aspx)]

アニメーションは、次のようなテキストパネルに適用されます。

[!code-aspx[Main](animating-in-response-to-user-interaction-cs/samples/sample2.aspx)]

パネルに関連付けられている CSS クラスで、優れた背景色を定義し、パネルに固定幅を設定します。

[!code-css[Main](animating-in-response-to-user-interaction-cs/samples/sample3.css)]

次に、`ID`、`TargetControlID` 属性、および加える `runat="server"`を指定して、ページに `AnimationExtender` を追加します。

[!code-aspx[Main](animating-in-response-to-user-interaction-cs/samples/sample4.aspx)]

[`<Animations>`] ノードには、ユーザーの操作によってアニメーションを開始する5つの方法があります (missing 要素は、ページ全体が完全に読み込まれた後に実行される `<OnLoad>`)。

- `<OnClick>` (コントロール上でマウスをクリック)
- `<OnHoverOut>` (マウスをコントロールから離す)
- `<OnHoverOver>` (マウスポインターをコントロールの上に置くと、`<OnHoverOut>` アニメーションが停止します)
- `<OnMouseOut>` (マウスをコントロールから離す)
- `<OnMouseOver>` (マウスポインターをコントロールの上に置くと、`<OnMouseOut>` アニメーションは停止しません)

このシナリオでは、`<OnClick>` が使用されます。 ユーザーがパネルをクリックすると、サイズが変更され、同時にフェードアウトします。

[!code-aspx[Main](animating-in-response-to-user-interaction-cs/samples/sample5.aspx)]

[マウスクリックによってアニメーションが開始 ![](animating-in-response-to-user-interaction-cs/_static/image2.png)](animating-in-response-to-user-interaction-cs/_static/image1.png)

マウスクリックでアニメーションが開始されます ([クリックすると、フルサイズの画像が表示](animating-in-response-to-user-interaction-cs/_static/image3.png)されます)

> [!div class="step-by-step"]
> [前へ](picking-one-animation-out-of-a-list-cs.md)
> [次へ](disabling-actions-during-animation-cs.md)
