---
uid: web-forms/overview/ajax-control-toolkit/animation/picking-one-animation-out-of-a-list-vb
title: リストから1つのアニメーションを選択する (VB) |Microsoft Docs
author: wenz
description: ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。 フレームワークも許可する (...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 81ba9116-d485-40c0-8ff6-7e9ae23e0a0c
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/picking-one-animation-out-of-a-list-vb
msc.type: authoredcontent
ms.openlocfilehash: 694416532b558291ff6ab57a442058b53d6167e0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78430822"
---
# <a name="picking-one-animation-out-of-a-list-vb"></a>一覧からアニメーションを 1 つ選択する (VB)

[Christian Wenz](https://github.com/wenz)別

[コードのダウンロード](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation5.vb.zip)または[PDF のダウンロード](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation5VB.pdf)

> ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。 また、一部の JavaScript コードの評価に応じて、アニメーションの一覧から1つのアニメーションを取得することもできます。

## <a name="overview"></a>概要

ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。 また、一部の JavaScript コードの評価に応じて、アニメーションの一覧から1つのアニメーションを取得することもできます。

## <a name="steps"></a>手順

まず、ページに `ScriptManager` を含めます。次に、ASP.NET AJAX ライブラリが読み込まれ、Control Toolkit を使用できるようになります。

[!code-aspx[Main](picking-one-animation-out-of-a-list-vb/samples/sample1.aspx)]

アニメーションは、次のようなテキストパネルに適用されます。

[!code-aspx[Main](picking-one-animation-out-of-a-list-vb/samples/sample2.aspx)]

パネルに関連付けられている CSS クラスで、優れた背景色を定義し、パネルに固定幅を設定します。

[!code-css[Main](picking-one-animation-out-of-a-list-vb/samples/sample3.css)]

次に、`ID`、`TargetControlID` 属性、および加えるを指定して、ページに `AnimationExtender` を追加し `runat="server":`

[!code-aspx[Main](picking-one-animation-out-of-a-list-vb/samples/sample4.aspx)]

ページが完全に読み込まれたら、[`<Animations>`] ノードで `<OnLoad>` を使用してアニメーションを実行します。 通常のアニメーションのいずれかではなく、`<Case>` 要素が再生されます。 SelectScript 属性の値が評価されます。戻り値は数値である必要があります。 この数値に応じて、&lt;Case&gt; 内のいずれかのサブアニメーションが実行されます。 たとえば、SelectScript が2に評価される場合、Control Toolkit は &lt;ケース&gt; 内で3番目のアニメーションを実行します (カウントは0から始まります)。

次のマークアップは、3つのサブアニメーションを定義します。幅の変更、高さのサイズ変更、およびフェードアウトです。次に、JavaScript コード (`Math.floor(3 * Math.random())`) が 0 ~ 2 の範囲の数値を選択して、3つのアニメーションのいずれかが実行されるようにします。

[!code-aspx[Main](picking-one-animation-out-of-a-list-vb/samples/sample5.aspx)]

[使用可能な3つのアニメーションのいずれかを ![します。パネルの幅が広くなります。](picking-one-animation-out-of-a-list-vb/_static/image2.png)](picking-one-animation-out-of-a-list-vb/_static/image1.png)

使用可能な3つのアニメーションのいずれか: パネルの幅が広くなります ([クリックすると、フルサイズの画像が表示](picking-one-animation-out-of-a-list-vb/_static/image3.png)されます)。

> [!div class="step-by-step"]
> [前へ](animation-depending-on-a-condition-vb.md)
> [次へ](animating-in-response-to-user-interaction-vb.md)
