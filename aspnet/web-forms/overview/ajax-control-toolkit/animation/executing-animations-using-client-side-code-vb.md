---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-animations-using-client-side-code-vb
title: クライアント側コードを使用してアニメーションを実行する (VB) |Microsoft Docs
author: wenz
description: ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。 アニメーションの実行...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: f7073f50-d765-456d-9957-926ce60f35f6
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-animations-using-client-side-code-vb
msc.type: authoredcontent
ms.openlocfilehash: 7ef36900d20d8d07c3c6f3b63ce96568a377a0ed
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484006"
---
# <a name="executing-animations-using-client-side-code-vb"></a>クライアント側コードを使用してアニメーションを実行する (VB)

[Christian Wenz](https://github.com/wenz)別

[コードのダウンロード](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation10.vb.zip)または[PDF のダウンロード](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation10VB.pdf)

> ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。 アニメーションの実行は、カスタムクライアント側の JavaScript コードを使用してトリガーすることもできます。

## <a name="overview"></a>概要

ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。 アニメーションの実行は、カスタムクライアント側の JavaScript コードを使用してトリガーすることもできます。

## <a name="steps"></a>手順

まず、ページに `ScriptManager` を含めます。次に、ASP.NET AJAX ライブラリが読み込まれ、Control Toolkit を使用できるようになります。

[!code-aspx[Main](executing-animations-using-client-side-code-vb/samples/sample1.aspx)]

アニメーションは、次のようなテキストパネルに適用されます。

[!code-aspx[Main](executing-animations-using-client-side-code-vb/samples/sample2.aspx)]

パネルに関連付けられている CSS クラスで、優れた背景色を定義し、パネルに固定幅を設定します。

[!code-css[Main](executing-animations-using-client-side-code-vb/samples/sample3.css)]

次に、`ID`、`TargetControlID` 属性、および加える `runat="server"`を指定して、ページに `AnimationExtender` を追加します。

[!code-aspx[Main](executing-animations-using-client-side-code-vb/samples/sample4.aspx)]

`<Animations>` ノード内で `<OnClick>` を使用して、ユーザーがパネルをクリックした後にアニメーションを実行します。 並列で実行される2つのアニメーションを追加します。

[!code-xml[Main](executing-animations-using-client-side-code-vb/samples/sample5.xml)]

このデモでは、ページが実行されると、JavaScript コードを使用して、このアニメーション (およびコントロールツールキットを使用して作成されたその他のアニメーション) を実行します。 まず、`AnimationExtender` コントロールにアクセスする必要があります。 ASP.NET AJAX ライブラリには、このタスクの `$find()` 関数が用意されています。

[!code-csharp[Main](executing-animations-using-client-side-code-vb/samples/sample6.cs)]

`AnimationExtender` コントロールは、XML マークアップで使用されるイベントハンドラーと同じ名前のメソッド (`OnClick()`、`OnLoad()`など) を含む豊富な API を公開します。 たとえば、`OnClick()` メソッドを呼び出すと、`AnimationExtender` コントロールの `<OnClick>` 要素内でアニメーションが実行されます。

[!code-javascript[Main](executing-animations-using-client-side-code-vb/samples/sample7.js)]

ページが完全に読み込まれた後にパネルをエミュレートする完全なクライアント側 JavaScript コードを次に示します。 `pageLoad()` 関数名が使用されていることに注意してください。これは、ページと含まれているすべての JavaScript ライブラリが読み込まれた後に ASP.NET AJAX によって呼び出されます。

[!code-html[Main](executing-animations-using-client-side-code-vb/samples/sample8.html)]

[マウスをクリックせずに、アニメーションをすぐに実行 ![](executing-animations-using-client-side-code-vb/_static/image2.png)](executing-animations-using-client-side-code-vb/_static/image1.png)

アニメーションは、マウスクリックなしですぐに実行されます ([クリックすると、フルサイズの画像が表示](executing-animations-using-client-side-code-vb/_static/image3.png)されます)

> [!div class="step-by-step"]
> [前へ](modifying-animations-from-the-server-side-vb.md)
> [次へ](changing-an-animation-using-client-side-code-vb.md)
