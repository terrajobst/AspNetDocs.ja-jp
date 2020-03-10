---
uid: web-forms/overview/ajax-control-toolkit/animation/animation-depending-on-a-condition-cs
title: 条件に応じたアニメーション (C#) |Microsoft Docs
author: wenz
description: ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。 アニメーションの有無
ms.author: riande
ms.date: 06/02/2008
ms.assetid: b7a28c0d-efb9-443a-80a4-1a5ee54671cd
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animation-depending-on-a-condition-cs
msc.type: authoredcontent
ms.openlocfilehash: 476b0cf80fa7c04cd8b8f9a92060ddabb9d14c13
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484168"
---
# <a name="animation-depending-on-a-condition-c"></a>条件に基づくアニメーション (C#)

[Christian Wenz](https://github.com/wenz)別

[コードのダウンロード](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation4.cs.zip)または[PDF のダウンロード](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation4CS.pdf)

> ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。 アニメーションが実行されるかどうかは、JavaScript コードの形式で条件に依存することもできます。

## <a name="overview"></a>概要

ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。 アニメーションが実行されるかどうかは、JavaScript コードの形式で条件に依存することもできます。

## <a name="steps"></a>手順

まず、ページに `ScriptManager` を含めます。次に、ASP.NET AJAX ライブラリが読み込まれ、Control Toolkit を使用できるようになります。

[!code-aspx[Main](animation-depending-on-a-condition-cs/samples/sample1.aspx)]

アニメーションは、次のようなテキストパネルに適用されます。

[!code-aspx[Main](animation-depending-on-a-condition-cs/samples/sample2.aspx)]

パネルに関連付けられている CSS クラスで、優れた背景色を定義し、パネルに固定幅を設定します。

[!code-css[Main](animation-depending-on-a-condition-cs/samples/sample3.css)]

次に、`ID`、`TargetControlID` 属性、および加えるを指定して、ページに `AnimationExtender` を追加し `runat="server":`

[!code-aspx[Main](animation-depending-on-a-condition-cs/samples/sample4.aspx)]

ページが完全に読み込まれたら、[`<Animations>`] ノードで `<OnLoad>` を使用してアニメーションを実行します。 通常のアニメーションのいずれかではなく、`<Condition>` 要素が再生されます。 `ConditionScript` 属性の値として指定された JavaScript コードは、実行時に実行されます。 True と評価された場合、アニメーションは実行されます。それ以外の場合は実行されません。 次のマークアップは、2つのアニメーションを提供します。それぞれのアニメーションは、ランダムに50% のケースで実行されます。 `<OnLoad>`内には1つのアニメーションしか存在しないため、2つの `<Condition>` アニメーションは `<Sequence>` 要素を使用して結合されます。

[!code-aspx[Main](animation-depending-on-a-condition-cs/samples/sample5.aspx)]

`ConditionScript` 属性の不等号 (`<`) をエスケープする () 必要があることに注意してください。 このスクリプトを実行すると、アニメーションは実行されず、どちらか一方または両方が実行されます。

[パネルのサイズを変更せずにフェードアウトする ![、2番目のアニメーションが実行されます。最初のアニメーションは実行されませんでした。](animation-depending-on-a-condition-cs/_static/image2.png)](animation-depending-on-a-condition-cs/_static/image1.png)

パネルはサイズ変更せずにフェードアウトします。そのため、2番目のアニメーションを実行します ([クリックすると、フルサイズの画像が表示](animation-depending-on-a-condition-cs/_static/image3.png)されます)。

> [!div class="step-by-step"]
> [前へ](executing-several-animations-after-each-other-cs.md)
> [次へ](picking-one-animation-out-of-a-list-cs.md)
