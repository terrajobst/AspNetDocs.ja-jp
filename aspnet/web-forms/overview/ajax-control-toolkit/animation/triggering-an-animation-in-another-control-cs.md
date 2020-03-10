---
uid: web-forms/overview/ajax-control-toolkit/animation/triggering-an-animation-in-another-control-cs
title: 別のコントロールでアニメーションをトリガーC#する () |Microsoft Docs
author: wenz
description: ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。 一般に、...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e5d99c2b-d8ee-413c-80d5-c120cffb0a4c
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/triggering-an-animation-in-another-control-cs
msc.type: authoredcontent
ms.openlocfilehash: e0a1f8986047da04db6fde8e54b6fd0ac6ee2603
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78430792"
---
# <a name="triggering-an-animation-in-another-control-c"></a>別のコントロールでアニメーションをトリガーする (C#)

[Christian Wenz](https://github.com/wenz)別

[コードのダウンロード](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation8.cs.zip)または[PDF のダウンロード](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation8CS.pdf)

> ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。 通常、アニメーションの起動は、同じコントロールでのユーザー操作によってトリガーされます。 ただし、1つのコントロールと対話し、別のコントロールをアニメーションすることもできます。

## <a name="overview"></a>概要

ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。 通常、アニメーションの起動は、同じコントロールでのユーザー操作によってトリガーされます。 ただし、1つのコントロールと対話し、別のコントロールをアニメーションすることもできます。

## <a name="steps"></a>手順

まず、ページに `ScriptManager` を含めます。次に、ASP.NET AJAX ライブラリが読み込まれ、Control Toolkit を使用できるようになります。

[!code-aspx[Main](triggering-an-animation-in-another-control-cs/samples/sample1.aspx)]

アニメーションは、次のようなテキストパネルに適用されます。

[!code-aspx[Main](triggering-an-animation-in-another-control-cs/samples/sample2.aspx)]

パネルに関連付けられている CSS クラスで、優れた背景色を定義し、パネルに固定幅を設定します。

[!code-css[Main](triggering-an-animation-in-another-control-cs/samples/sample3.css)]

パネルのアニメーション化を開始するために、HTML ボタンが使用されます。 `<input type="button" />` は、ユーザーがボタンをクリックしたときにポストバックが不要になるため、`<asp:Button />` で favoured されることに注意してください。

[!code-aspx[Main](triggering-an-animation-in-another-control-cs/samples/sample4.aspx)]

次に、`ID`、`TargetControlID` 属性、および加える `runat="server"`を指定して、ページに `AnimationExtender` を追加します。 `TargetControlID` を、パネルの ID (アニメーション化する要素) ではなく、ボタンの ID (アニメーションをトリガーする要素) に設定することが重要です。

[!code-aspx[Main](triggering-an-animation-in-another-control-cs/samples/sample5.aspx)]

[`<Animations>`] ノード内で、アニメーションを通常どおりに配置します。 ボタンではなくパネルを変更するには、`AnimationExtender`内のすべてのアニメーション要素の `AnimationTarget` 属性を設定します。 `AnimationTarget` の値は、もちろん、パネルの ID です。 これにより、アニメーションは、[トリガー] ボタンではなく、パネルで行われます。 このシナリオの `AnimationExtender` マークアップは次のとおりです。

[!code-aspx[Main](triggering-an-animation-in-another-control-cs/samples/sample6.aspx)]

個々のアニメーションが表示される特別な順序に注意してください。 まず、アニメーションを実行すると、ボタンが非アクティブになります。 `<EnableAction>` 要素には `AnimationTarget` 属性がないため、このアニメーションは元のコントロール (ボタン) に適用されます。 次の2つのアニメーションの手順は、並列 (`<Parallel>` 要素) で実行する必要があります。 どちらの `AnimationTarget` 属性も `"Panel1"`に設定されているので、ボタンではなくパネルをアニメーション化します。

[ボタンをクリックする ![、パネルアニメーションが開始されます。](triggering-an-animation-in-another-control-cs/_static/image2.png)](triggering-an-animation-in-another-control-cs/_static/image1.png)

ボタンをクリックするとパネルアニメーションが開始されます ([クリックすると、フルサイズの画像が表示](triggering-an-animation-in-another-control-cs/_static/image3.png)されます)

> [!div class="step-by-step"]
> [前へ](disabling-actions-during-animation-cs.md)
> [次へ](modifying-animations-from-the-server-side-cs.md)
