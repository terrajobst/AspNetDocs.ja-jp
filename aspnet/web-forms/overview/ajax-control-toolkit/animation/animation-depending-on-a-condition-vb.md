---
uid: web-forms/overview/ajax-control-toolkit/animation/animation-depending-on-a-condition-vb
title: 条件に応じたアニメーション (VB) |Microsoft Docs
author: wenz
description: ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。 アニメーションの有無
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 1b87d8d6-b3f7-4126-b51c-d41442fbf947
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animation-depending-on-a-condition-vb
msc.type: authoredcontent
ms.openlocfilehash: 583ebdbf109beb74b9a425020477183067bbb79a
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74607014"
---
# <a name="animation-depending-on-a-condition-vb"></a>条件に基づくアニメーション (VB)

[Christian Wenz](https://github.com/wenz)別

[コードのダウンロード](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation4.vb.zip)または[PDF のダウンロード](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation4VB.pdf)

> ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。 アニメーションが実行されるかどうかは、JavaScript コードの形式で条件に依存することもできます。

## <a name="overview"></a>の概要

ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。 アニメーションが実行されるかどうかは、JavaScript コードの形式で条件に依存することもできます。

## <a name="steps"></a>手順

まず、ページに `ScriptManager` を含めます。次に、ASP.NET AJAX ライブラリが読み込まれ、Control Toolkit を使用できるようになります。

[!code-aspx[Main](animation-depending-on-a-condition-vb/samples/sample1.aspx)]

アニメーションは、次のようなテキストパネルに適用されます。

[!code-aspx[Main](animation-depending-on-a-condition-vb/samples/sample2.aspx)]

パネルに関連付けられている CSS クラスで、優れた背景色を定義し、パネルに固定幅を設定します。

[!code-css[Main](animation-depending-on-a-condition-vb/samples/sample3.css)]

次に、`ID`、`TargetControlID` 属性、および加えるを指定して、ページに `AnimationExtender` を追加し `runat="server":`

[!code-aspx[Main](animation-depending-on-a-condition-vb/samples/sample4.aspx)]

ページが完全に読み込まれたら、[`<Animations>`] ノードで `<OnLoad>` を使用してアニメーションを実行します。 通常のアニメーションのいずれかではなく、`<Condition>` 要素が再生されます。 `ConditionScript` 属性の値として指定された JavaScript コードは、実行時に実行されます。 True と評価された場合、アニメーションは実行されます。それ以外の場合は実行されません。 次のマークアップは、2つのアニメーションを提供します。それぞれのアニメーションは、ランダムに50% のケースで実行されます。 `<OnLoad>`内には1つのアニメーションしか存在しないため、2つの `<Condition>` アニメーションは `<Sequence>` 要素を使用して結合されます。

[!code-aspx[Main](animation-depending-on-a-condition-vb/samples/sample5.aspx)]

`ConditionScript` 属性の不等号 (`<`) をエスケープする () 必要があることに注意してください。 このスクリプトを実行すると、アニメーションは実行されず、どちらか一方または両方が実行されます。

[パネルのサイズを変更せずにフェードアウトする ![、2番目のアニメーションが実行されます。最初のアニメーションは実行されませんでした。](animation-depending-on-a-condition-vb/_static/image2.png)](animation-depending-on-a-condition-vb/_static/image1.png)

パネルはサイズ変更せずにフェードアウトします。そのため、2番目のアニメーションを実行します ([クリックすると、フルサイズの画像が表示](animation-depending-on-a-condition-vb/_static/image3.png)されます)。

> [!div class="step-by-step"]
> [前へ](executing-several-animations-after-each-other-vb.md)
> [次へ](picking-one-animation-out-of-a-list-vb.md)
