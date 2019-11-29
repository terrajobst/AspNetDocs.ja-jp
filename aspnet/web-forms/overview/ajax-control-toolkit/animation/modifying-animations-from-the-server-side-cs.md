---
uid: web-forms/overview/ajax-control-toolkit/animation/modifying-animations-from-the-server-side-cs
title: サーバー側からアニメーションを変更するC#() |Microsoft Docs
author: wenz
description: ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。 アニメーションも...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: b0abec39-a1c9-422d-ba9a-ef16f6185af8
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/modifying-animations-from-the-server-side-cs
msc.type: authoredcontent
ms.openlocfilehash: 0594efea9598a6c2461a72f789b5bd5f8ece23da
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74575188"
---
# <a name="modifying-animations-from-the-server-side-c"></a>サーバー側からアニメーションを変更するC#()

[Christian Wenz](https://github.com/wenz)別

[コードのダウンロード](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation9.cs.zip)または[PDF のダウンロード](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation9CS.pdf)

> ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。 アニメーションはサーバー側でも変更される可能性があります。

## <a name="overview"></a>の概要

ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。 アニメーションはサーバー側でも変更される可能性があります。

## <a name="steps"></a>手順

まず、ページに `ScriptManager` を含めます。次に、ASP.NET AJAX ライブラリが読み込まれ、Control Toolkit を使用できるようになります。

[!code-aspx[Main](modifying-animations-from-the-server-side-cs/samples/sample1.aspx)]

アニメーションは、次のようなテキストパネルに適用されます。

[!code-aspx[Main](modifying-animations-from-the-server-side-cs/samples/sample2.aspx)]

パネルに関連付けられている CSS クラスで、優れた背景色を定義し、パネルに固定幅を設定します。

[!code-css[Main](modifying-animations-from-the-server-side-cs/samples/sample3.css)]

残りのコードはサーバー側で実行され、マークアップを使用しません。代わりに、コードを使用して `AnimationExtender` コントロールを作成します。

[!code-aspx[Main](modifying-animations-from-the-server-side-cs/samples/sample4.aspx)]

ただし、Control Toolkit は、現在、個々のアニメーションを作成するための API アクセスを提供していません。 ただし、`AnimationExtender`のアニメーションプロパティを、アニメーションを宣言的に割り当てるときに使用する XML マークアップを含む文字列に設定することはできます。 `<Animations>` 要素を含んでいない XML を作成するには、.NET Framework の XML サポートを使用するか、次のコードのように、文字列を指定するだけです。

[!code-css[Main](modifying-animations-from-the-server-side-cs/samples/sample5.css)]

最後に、`<form runat="server">` 要素内の現在のページに `AnimationExtender` コントロールを追加し、アニメーションが含まれ、実行されていることを確認します。

[!code-html[Main](modifying-animations-from-the-server-side-cs/samples/sample6.html)]

[アニメーションがサーバー側C#/VB コードを使用して作成される ![](modifying-animations-from-the-server-side-cs/_static/image2.png)](modifying-animations-from-the-server-side-cs/_static/image1.png)

アニメーションは、サーバー側C#のコードまたは VB のコードを使用して作成されます ([クリックすると、フルサイズの画像が表示](modifying-animations-from-the-server-side-cs/_static/image3.png)されます)

> [!div class="step-by-step"]
> [前へ](triggering-an-animation-in-another-control-cs.md)
> [次へ](executing-animations-using-client-side-code-cs.md)
