---
uid: web-forms/overview/ajax-control-toolkit/slider/using-the-slider-control-with-auto-postback-vb
title: 自動ポストバックと共にスライダーコントロールを使用する (VB) |Microsoft Docs
author: wenz
description: AJAX コントロールツールキットのスライダーコントロールには、マウスを使用して制御できるグラフィカルスライダーが用意されています。 スライダーを自動投稿することができます...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 41d1abba-97a5-4a45-9b44-d05624c19777
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/slider/using-the-slider-control-with-auto-postback-vb
msc.type: authoredcontent
ms.openlocfilehash: e7a3286bcf7ca844f5dcfa4848c15e0bd4767c0f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78445780"
---
# <a name="using-the-slider-control-with-auto-postback-vb"></a>スライダーコントロールを自動ポストバックと共に使用する (VB)

[Christian Wenz](https://github.com/wenz)別

[コードのダウンロード](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider1.vb.zip)または[PDF のダウンロード](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/slider1VB.pdf)

> AJAX コントロールツールキットのスライダーコントロールには、マウスを使用して制御できるグラフィカルスライダーが用意されています。 スライダーの値が変更されたときに、そのスライダーを autopostback にすることができます。

## <a name="overview"></a>概要

AJAX コントロールツールキットのスライダーコントロールには、マウスを使用して制御できるグラフィカルスライダーが用意されています。 スライダーの値が変更されたときに、そのスライダーを autopostback にすることができます。

## <a name="steps"></a>手順

スライダーが変化したときに自動的にポストバックされるようにするには、両方のテキストボックスに属性 `AutoPostBack="true"`が必要です。これは、スライダー自体になるテキストボックスと、スライダーの位置を保持するテキストボックスです。 そのために必要なマークアップは次のとおりです。

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample1.aspx)]

ASP.NET AJAX Control Toolkit の `SliderExtender` コントロールでは、次の2つのテキストボックスにスライダーの機能が割り当てられます。

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample2.aspx)]

後で追加の label 要素を使用して、ユーザーにポストバックを通知します。

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample3.aspx)]

最後に、ASP.NET AJAX の `ScriptManager` 制御によって、コントロールツールキットが動作するために必要な JavaScript が読み込まれます。

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample4.aspx)]

これで、スライダーがポストバックされます。サーバー側では、このイベントがキャッチされ、次のように処理されることがあります。

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample5.aspx)]

[スライダーを移動 ![とポストバックがトリガーされる](using-the-slider-control-with-auto-postback-vb/_static/image2.png)](using-the-slider-control-with-auto-postback-vb/_static/image1.png)

スライダーを移動するとポストバックがトリガーされます ([クリックすると、フルサイズのイメージが表示](using-the-slider-control-with-auto-postback-vb/_static/image3.png)されます)

[![後、この変更の日付はラベルに書き込まれます。](using-the-slider-control-with-auto-postback-vb/_static/image5.png)](using-the-slider-control-with-auto-postback-vb/_static/image4.png)

その後、この変更の日付がラベルに書き込まれます ([クリックすると、フルサイズの画像が表示](using-the-slider-control-with-auto-postback-vb/_static/image6.png)されます)

> [!div class="step-by-step"]
> [前へ](databinding-the-slider-control-cs.md)
> [次へ](databinding-the-slider-control-vb.md)
