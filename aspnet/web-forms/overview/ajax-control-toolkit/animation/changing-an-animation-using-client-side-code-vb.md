---
uid: web-forms/overview/ajax-control-toolkit/animation/changing-an-animation-using-client-side-code-vb
title: クライアント側コードを使用してアニメーションを変更する (VB) |Microsoft Docs
author: wenz
description: ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。 アニメーションは、
ms.author: riande
ms.date: 06/02/2008
ms.assetid: a7fe5de5-a964-4780-ae5e-70821dfb50a0
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/changing-an-animation-using-client-side-code-vb
msc.type: authoredcontent
ms.openlocfilehash: cce0a5a901f71edd40eada59ac7eeba93222e2b3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78430990"
---
# <a name="changing-an-animation-using-client-side-code-vb"></a>クライアント側コードを使用してアニメーションを変更する (VB)

[Christian Wenz](https://github.com/wenz)別

[コードのダウンロード](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation11.vb.zip)または[PDF のダウンロード](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation11VB.pdf)

> ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。 アニメーションは、カスタムクライアント側の JavaScript コードを使用して変更することもできます。

## <a name="overview"></a>概要

ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。 アニメーションは、カスタムクライアント側の JavaScript コードを使用して変更することもできます。

## <a name="steps"></a>手順

まず、ページに `ScriptManager` を含めます。次に、ASP.NET AJAX ライブラリが読み込まれ、Control Toolkit を使用できるようになります。

[!code-aspx[Main](changing-an-animation-using-client-side-code-vb/samples/sample1.aspx)]

アニメーションは、次のようなテキストパネルに適用されます。

[!code-aspx[Main](changing-an-animation-using-client-side-code-vb/samples/sample2.aspx)]

パネルに関連付けられている CSS クラスで、優れた背景色を定義し、パネルに固定幅を設定します。

[!code-css[Main](changing-an-animation-using-client-side-code-vb/samples/sample3.css)]

実際のアニメーションは、HTML ボタンによって起動されます。

[!code-aspx[Main](changing-an-animation-using-client-side-code-vb/samples/sample4.aspx)]

次に、`ID`、`TargetControlID` 属性、および加える `runat="server"`を指定して、ページに `AnimationExtender` を追加します。

[!code-aspx[Main](changing-an-animation-using-client-side-code-vb/samples/sample5.aspx)]

`AnimationExtender` コントロール内に `<Animations>` ノードがないことに注意してください。 カスタム JavaScript コードを使用して、コントロールで使用されるアニメーションを提供します。

`AnimationExtender`のサーバー API と同様に、まだ extender にアニメーションを割り当てる簡単な方法はありません。 ただし、extender では、さまざまなイベント (`OnClick`、`OnLoad`など) に登録されたアニメーションの読み取りおよび書き込みを行うためのメソッドがいくつか公開されています。 次に例をいくつか示します。

- `get_OnClick()`
- `set_OnClick()`
- `get_OnLoad()`
- `set_OnLoad()`
- `...`

`get_*()` 関数の戻り値の形式と、`set_*()` 関数の引数の形式は JSON 文字列であり、XML マークアップの内容を表すオブジェクトを提供します。 現在、でオブジェクトを渡す方法はありませんが、指定されたアニメーション (`get_OnXXXBehavior()` メソッド) からオブジェクトを読み取ることはできます。

次に示すのは、ボタンによってトリガーされるアニメーションを表す JSON 文字列 (区切り引用符が不要で、適切に書式設定されたもの) ですが、パネルをアニメーション化し、同時にフェードアウトします。

[!code-json[Main](changing-an-animation-using-client-side-code-vb/samples/sample6.json)]

次の JavaScript コードは、この JSON descripting を現在の extender の `OnClick` アニメーションに割り当てて実行します。

[!code-html[Main](changing-an-animation-using-client-side-code-vb/samples/sample7.html)]

[マウスをクリックしないで (そして、マークアップをほとんど行わずに) アニメーションをすぐに実行 ![](changing-an-animation-using-client-side-code-vb/_static/image2.png)](changing-an-animation-using-client-side-code-vb/_static/image1.png)

アニメーションは、マウスをクリックすることなく (そして、マークアップが非常に少ない)、すぐに実行されます ([クリックすると、フルサイズの画像が表示](changing-an-animation-using-client-side-code-vb/_static/image3.png)されます)

> [!div class="step-by-step"]
> [前へ](executing-animations-using-client-side-code-vb.md)
> [次へ](animating-an-updatepanel-control-vb.md)
