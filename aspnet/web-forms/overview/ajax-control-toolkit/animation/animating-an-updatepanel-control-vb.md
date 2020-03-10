---
uid: web-forms/overview/ajax-control-toolkit/animation/animating-an-updatepanel-control-vb
title: UpdatePanel コントロールのアニメーション化 (VB) |Microsoft Docs
author: wenz
description: ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。 ... の内容
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 4c306a2c-92b6-4904-b70b-365b847334fe
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animating-an-updatepanel-control-vb
msc.type: authoredcontent
ms.openlocfilehash: d66dda923940a328c0757049c9d8bfa3b2d2b9fc
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78431014"
---
# <a name="animating-an-updatepanel-control-vb"></a>UpdatePanel コントロールをアニメーションにする (VB)

[Christian Wenz](https://github.com/wenz)別

[コードのダウンロード](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation1.vb.zip)または[PDF のダウンロード](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation1VB.pdf)

> ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。 UpdatePanel の内容については、animation framework: Updateパネルアニメーションに大きく依存する特別な extender が存在します。 このチュートリアルでは、このようなアニメーションを UpdatePanel に設定する方法について説明します。

## <a name="overview"></a>概要

ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。 `UpdatePanel`の内容については、`UpdatePanelAnimation`のアニメーションフレームワークに大きく依存する特別な extender が存在します。 このチュートリアルでは、このようなアニメーションを `UpdatePanel`に設定する方法について説明します。

## <a name="steps"></a>手順

最初の手順は通常どおり、ASP.NET AJAX ライブラリが読み込まれ、Control Toolkit を使用できるように、ページに `ScriptManager` を含めることです。

[!code-aspx[Main](animating-an-updatepanel-control-vb/samples/sample1.aspx)]

このシナリオのアニメーションは、`UpdatePanel`に存在する ASP.NET `Wizard` web コントロールに適用されます。 ポストバックをトリガーするためのオプションは、3つ (任意) の手順で指定します。

[!code-aspx[Main](animating-an-updatepanel-control-vb/samples/sample2.aspx)]

`UpdatePanelAnimationExtender` コントロールに必要なマークアップは、`AnimationExtender`に使用されるマークアップと非常によく似ています。 `TargetControlID` 属性では、アニメーション化する `UpdatePanel` の `ID` を指定します。`UpdatePanelAnimationExtender` コントロール内では、`<Animations>` 要素は、アニメーションの XML マークアップを保持します。 ただし、1つの違いがあります。 `AnimationExtender`と比較すると、イベントとイベントハンドラーの量が制限されます。 `UpdatePanels`には、次の2つのみが存在します。

- UpdatePanel が更新されたときの `<OnUpdated>`
- UpdatePanel が更新を開始するときに `<OnUpdating>` します。

このシナリオでは、(ポストバック後に) `UpdatePanel` の新しい内容がフェードインされます。 これは、そのために必要なマークアップです。

[!code-aspx[Main](animating-an-updatepanel-control-vb/samples/sample3.aspx)]

これで、UpdatePanel 内でポストバックが発生するたびに、パネルの新しいコンテンツがスムーズにフェードインされます。

[次のウィザードのステップがフェードイン ![](animating-an-updatepanel-control-vb/_static/image2.png)](animating-an-updatepanel-control-vb/_static/image1.png)

次のウィザードステップはフェードインします ([クリックすると、フルサイズの画像が表示](animating-an-updatepanel-control-vb/_static/image3.png)されます)

> [!div class="step-by-step"]
> [前へ](changing-an-animation-using-client-side-code-vb.md)
> [次へ](dynamically-controlling-updatepanel-animations-vb.md)
