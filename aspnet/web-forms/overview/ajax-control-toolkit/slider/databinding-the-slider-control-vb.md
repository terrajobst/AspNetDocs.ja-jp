---
uid: web-forms/overview/ajax-control-toolkit/slider/databinding-the-slider-control-vb
title: スライダーコントロールをデータバインドする (VB) |Microsoft Docs
author: wenz
description: AJAX コントロールツールキットのスライダーコントロールには、マウスを使用して制御できるグラフィカルスライダーが用意されています。 現在の positio をバインドすることができます...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 4f3ba53f-d166-422d-b29c-403348057836
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/slider/databinding-the-slider-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 9c14373bdfdead9916950b8a1cf61f427f7ba50b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78508900"
---
# <a name="databinding-the-slider-control-vb"></a>スライダー コントロールをデータバインドする (VB)

[Christian Wenz](https://github.com/wenz)別

[コードのダウンロード](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider0.vb.zip)または[PDF のダウンロード](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/slider0VB.pdf)

> AJAX コントロールツールキットのスライダーコントロールには、マウスを使用して制御できるグラフィカルスライダーが用意されています。 スライダーの現在位置を別の ASP.NET コントロールにバインドすることができます。

## <a name="overview"></a>概要

AJAX コントロールツールキットのスライダーコントロールには、マウスを使用して制御できるグラフィカルスライダーが用意されています。 スライダーの現在位置を別の ASP.NET コントロールにバインドすることができます。

## <a name="steps"></a>手順

ASP.NET AJAX と Control Toolkit の機能をアクティブ化するには、ページの任意の場所に `ScriptManager` コントロールを配置する必要があります (`<form>` 要素内)。

[!code-aspx[Main](databinding-the-slider-control-vb/samples/sample1.aspx)]

次に、2つの `TextBox` コントロールをページに追加します。 一方はグラフィカルなスライダーに変換され、もう一方はスライダーの位置を保持します。

[!code-aspx[Main](databinding-the-slider-control-vb/samples/sample2.aspx)]

次の手順は、既に最後の手順です。 ASP.NET AJAX Control Toolkit の `SliderExtender` コントロールによって、最初のテキストボックスの下にスライダーが表示され、スライダーの位置が変更されると、2つ目のテキストボックスが自動的に更新されます。 これが機能するためには、`SliderExtender`の `TargetControlID` 属性が最初のテキストボックスの ID に設定されている必要があります。`BoundControlID` 属性は、2番目のテキストボックスの ID に設定する必要があります。

[!code-aspx[Main](databinding-the-slider-control-vb/samples/sample3.aspx)]

ブラウザーで見るとわかるように、データバインディングは双方向で動作します。テキストボックスに新しい値を入力すると、スライダーの位置が更新されます。 2番目のテキストボックスを読み取り専用にする場合は、ユーザーが手動で値を更新するのが難しいように、テキストフィールドに弱い保護を追加することができます。

[![スライダーとテキストボックスが同期されています](databinding-the-slider-control-vb/_static/image2.png)](databinding-the-slider-control-vb/_static/image1.png)

スライダーとテキストボックスが同期されています ([クリックすると、フルサイズの画像が表示](databinding-the-slider-control-vb/_static/image3.png)されます)

> [!div class="step-by-step"]
> [[戻る]](using-the-slider-control-with-auto-postback-vb.md)
