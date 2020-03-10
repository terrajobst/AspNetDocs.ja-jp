---
uid: web-forms/overview/ajax-control-toolkit/animation/changing-an-animation-using-client-side-code-cs
title: クライアント側コードを使用してアニメーションをC#変更する () |Microsoft Docs
author: wenz
description: ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。 アニメーションは、
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 2bfbc5cc-f942-44b7-a62d-a29520f1da9a
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/changing-an-animation-using-client-side-code-cs
msc.type: authoredcontent
ms.openlocfilehash: 84fc2d6646b89cfabb2193cdfca59462d6d7ef16
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484054"
---
# <a name="changing-an-animation-using-client-side-code-c"></a>クライアント側コードを使用してアニメーションを変更する (C#)

[Christian Wenz](https://github.com/wenz)別

[コードのダウンロード](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation11.cs.zip)または[PDF のダウンロード](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation11CS.pdf)

> ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。 アニメーションは、カスタムクライアント側の JavaScript コードを使用して変更することもできます。

## <a name="overview"></a>概要

ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。 アニメーションは、カスタムクライアント側の JavaScript コードを使用して変更することもできます。

## <a name="steps"></a>手順

まず、ページに `ScriptManager` を含めます。次に、ASP.NET AJAX ライブラリが読み込まれ、Control Toolkit を使用できるようになります。

[!code-aspx[Main](changing-an-animation-using-client-side-code-cs/samples/sample1.aspx)]

アニメーションは、次のようなテキストパネルに適用されます。

[!code-aspx[Main](changing-an-animation-using-client-side-code-cs/samples/sample2.aspx)]

パネルに関連付けられている CSS クラスで、優れた背景色を定義し、パネルに固定幅を設定します。

[!code-css[Main](changing-an-animation-using-client-side-code-cs/samples/sample3.css)]

実際のアニメーションは、HTML ボタンによって起動されます。

[!code-aspx[Main](changing-an-animation-using-client-side-code-cs/samples/sample4.aspx)]

次に、`ID`、`TargetControlID` 属性、および加える `runat="server"`を指定して、ページに `AnimationExtender` を追加します。

[!code-aspx[Main](changing-an-animation-using-client-side-code-cs/samples/sample5.aspx)]

`AnimationExtender` コントロール内に `<Animations>` ノードがないことに注意してください。 カスタム JavaScript コードを使用して、コントロールで使用されるアニメーションを提供します。

`AnimationExtender`のサーバー API と同様に、まだ extender にアニメーションを割り当てる簡単な方法はありません。 ただし、extender では、さまざまなイベント (`OnClick`、`OnLoad`など) に登録されたアニメーションの読み取りおよび書き込みを行うためのメソッドがいくつか公開されています。 次に例をいくつか示します。

- `get_OnClick()`
- `set_OnClick()`
- `get_OnLoad()`
- `set_OnLoad()`
- `...`

`get_*()` 関数の戻り値の形式と、`set_*()` 関数の引数の形式は JSON 文字列であり、XML マークアップの内容を表すオブジェクトを提供します。 現在、でオブジェクトを渡す方法はありませんが、指定されたアニメーション (`get_OnXXXBehavior()` メソッド) からオブジェクトを読み取ることはできます。

次に示すのは、ボタンによってトリガーされるアニメーションを表す JSON 文字列 (区切り引用符が不要で、適切に書式設定されたもの) ですが、パネルをアニメーション化し、同時にフェードアウトします。

[!code-json[Main](changing-an-animation-using-client-side-code-cs/samples/sample6.json)]

次の JavaScript コードは、この JSON descripting を現在の extender の `OnClick` アニメーションに割り当てて実行します。

[!code-html[Main](changing-an-animation-using-client-side-code-cs/samples/sample7.html)]

[マウスをクリックしないで (そして、マークアップをほとんど行わずに) アニメーションをすぐに実行 ![](changing-an-animation-using-client-side-code-cs/_static/image2.png)](changing-an-animation-using-client-side-code-cs/_static/image1.png)

アニメーションは、マウスをクリックすることなく (そして、マークアップが非常に少ない)、すぐに実行されます ([クリックすると、フルサイズの画像が表示](changing-an-animation-using-client-side-code-cs/_static/image3.png)されます)

> [!div class="step-by-step"]
> [前へ](executing-animations-using-client-side-code-cs.md)
> [次へ](animating-an-updatepanel-control-cs.md)
