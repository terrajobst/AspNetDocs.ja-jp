---
uid: web-forms/overview/ajax-control-toolkit/animation/adding-animation-to-a-control-vb
title: コントロールへのアニメーションの追加 (VB) |Microsoft Docs
author: wenz
description: ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。 このチュートリアルでは、
ms.author: riande
ms.date: 06/02/2008
ms.assetid: c120187e-963e-4439-bb85-32771bc7f1f4
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/adding-animation-to-a-control-vb
msc.type: authoredcontent
ms.openlocfilehash: efaee9c1665d795dc1a889b9ac9f25dd1c08f4e2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484126"
---
# <a name="adding-animation-to-a-control-vb"></a>コントロールにアニメーションを追加する (VB)

[Christian Wenz](https://github.com/wenz)別

[コードのダウンロード](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation1.vb.zip)または[PDF のダウンロード](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation1VB.pdf)

> ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。 このチュートリアルでは、このようなアニメーションを設定する方法について説明します。

## <a name="overview"></a>概要

ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。 このチュートリアルでは、このようなアニメーションを設定する方法について説明します。

## <a name="steps"></a>手順

最初の手順は通常どおり、ASP.NET AJAX ライブラリが読み込まれ、Control Toolkit を使用できるように、ページに `ScriptManager` を含めることです。

[!code-aspx[Main](adding-animation-to-a-control-vb/samples/sample1.aspx)]

このシナリオのアニメーションは、次のようなテキストパネルに適用されます。

[!code-aspx[Main](adding-animation-to-a-control-vb/samples/sample2.aspx)]

パネルに関連付けられている CSS クラスは、背景色と幅を定義します。

[!code-css[Main](adding-animation-to-a-control-vb/samples/sample3.css)]

次に、`AnimationExtender`が必要です。 `ID` と通常の `runat="server"`を指定した後、`TargetControlID` 属性をコントロールに設定して、アニメーション化するには、パネルで次のようにします。

[!code-aspx[Main](adding-animation-to-a-control-vb/samples/sample4.aspx)]

アニメーション全体は XML 構文を使用して宣言によって適用されますが、現時点では Visual Studio の IntelliSense で完全にはサポートされていません。 ルートノードがこのノード内に `<Animations>;`、次のようないくつかのイベントが許可されます。これにより、アニメーションの実行時間が決まります。

- `OnClick` (マウスクリック)
- `OnHoverOut` (マウスをコントロールから離したとき)
- `OnHoverOver` (マウスポインターをコントロールの上に置くと、`OnHoverOut` アニメーションが停止します)
- `OnLoad` (ページが読み込まれたとき)
- `OnMouseOut` (マウスをコントロールから離したとき)
- `OnMouseOver` (マウスポインターをコントロールの上に置くと、`OnMouseOut` アニメーションは停止しません)

フレームワークには一連のアニメーションが用意されており、それぞれが独自の XML 要素で表されます。 次に例を示します。

- `<Color>` (色の変更)
- `<FadeIn>` (フェードイン)
- `<FadeOut>` (フェードアウト)
- `<Property>` (コントロールのプロパティを変更する)
- `<Pulse>` (アウト)
- `<Resize>` (サイズの変更)
- `<Scale>` (サイズの変更に比例)

この例では、パネルはフェードアウトします。アニメーションには1.5 秒 (`Duration` 属性) が必要で、1秒あたり24フレーム (アニメーションステップ) が表示されます (`Fps` 属性)。 `AnimationExtender` コントロールの完全なマークアップを次に示します。

[!code-aspx[Main](adding-animation-to-a-control-vb/samples/sample5.aspx)]

このスクリプトを実行すると、パネルが表示され、1秒と30秒でフェードアウトします。

[パネルがフェードアウト ![](adding-animation-to-a-control-vb/_static/image2.png)](adding-animation-to-a-control-vb/_static/image1.png)

パネルがフェードアウトします ([クリックすると、フルサイズの画像が表示](adding-animation-to-a-control-vb/_static/image3.png)されます)

> [!div class="step-by-step"]
> [前へ](dynamically-controlling-updatepanel-animations-cs.md)
> [次へ](executing-several-animations-at-the-same-time-vb.md)
