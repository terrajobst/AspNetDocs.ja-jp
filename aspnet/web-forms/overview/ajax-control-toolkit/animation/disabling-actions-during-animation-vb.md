---
uid: web-forms/overview/ajax-control-toolkit/animation/disabling-actions-during-animation-vb
title: アニメーション中のアクションを無効にする (VB) |Microsoft Docs
author: wenz
description: ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。 また、操作もサポートしています...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: a86c0276-6481-46ee-8b4f-8c2009399ee9
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/disabling-actions-during-animation-vb
msc.type: authoredcontent
ms.openlocfilehash: 4924d4f70099255b930d53f6a72e810be7a47485
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74606837"
---
# <a name="disabling-actions-during-animation-vb"></a>アニメーション中のアクションを無効にする (VB)

[Christian Wenz](https://github.com/wenz)別

[コードのダウンロード](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation7.vb.zip)または[PDF のダウンロード](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation7VB.pdf)

> ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。 また、マウスクリックなどの操作もサポートしています。 ただし、マウスクリックでアニメーションを開始する場合は、アニメーション中にマウスのクリックを無効にすることをお勧めします。

## <a name="overview"></a>の概要

ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。 また、マウスクリックなどの操作もサポートしています。 ただし、マウスクリックでアニメーションを開始する場合は、アニメーション中にマウスのクリックを無効にすることをお勧めします。

## <a name="steps"></a>手順

まず、ページに `ScriptManager` を含めます。次に、ASP.NET AJAX ライブラリが読み込まれ、Control Toolkit を使用できるようになります。

[!code-aspx[Main](disabling-actions-during-animation-vb/samples/sample1.aspx)]

アニメーションは、次のような HTML ボタンに適用されます。

[!code-aspx[Main](disabling-actions-during-animation-vb/samples/sample2.aspx)]

ボタンがポストバックを作成しないようにするため、Web コントロールの代わりに HTML コントロールが使用されていることに注意してください。ここでは、クライアント側のアニメーションを起動します。

次に、`ID`、`TargetControlID` 属性、および加える `runat="server"`を指定して、ページに `AnimationExtender` を追加します。

[!code-aspx[Main](disabling-actions-during-animation-vb/samples/sample3.aspx)]

`<Animations>` ノード内では、`<OnClick>` はマウスクリックを処理する右側の要素です。 ただし、アニメーション中にボタンをクリックすることもできます。 `<EnableAction>` 要素は、そのような処理を行うことができます。 `Enabled="false"` 設定すると、アニメーションの一部としてボタンが無効になります。 複数の個別のアニメーション (ボタンと実際のアニメーションを無効にする) を使用しているため、1つのアニメーションを1つに連結するには、`<Parallel>` 要素が必要です。 `AnimationExtender`の完全なマークアップを次に示します。

[!code-aspx[Main](disabling-actions-during-animation-vb/samples/sample4.aspx)]

また、リストの末尾にある次の XML 要素を使用して、アニメーションの後にボタンを再び有効にすることもできます。

[!code-xml[Main](disabling-actions-during-animation-vb/samples/sample5.xml)]

ただし、このようなシナリオでは、ボタンがフェードアウトし、アニメーションの最後に表示されないため、これは役に立ちません。

[アニメーションが実行されるとすぐにボタンが無効に ![](disabling-actions-during-animation-vb/_static/image2.png)](disabling-actions-during-animation-vb/_static/image1.png)

このボタンは、アニメーションが実行されるとすぐに無効になります ([クリックすると、フルサイズの画像が表示](disabling-actions-during-animation-vb/_static/image3.png)されます)

> [!div class="step-by-step"]
> [前へ](animating-in-response-to-user-interaction-vb.md)
> [次へ](triggering-an-animation-in-another-control-vb.md)
