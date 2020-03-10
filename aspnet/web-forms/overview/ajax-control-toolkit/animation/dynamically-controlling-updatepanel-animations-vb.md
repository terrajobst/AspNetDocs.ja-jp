---
uid: web-forms/overview/ajax-control-toolkit/animation/dynamically-controlling-updatepanel-animations-vb
title: UpdatePanel アニメーションを動的に制御する (VB) |Microsoft Docs
author: wenz
description: ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。 ... の内容
ms.author: riande
ms.date: 06/02/2008
ms.assetid: bea66072-59b6-42b4-98fa-211812f5925f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/dynamically-controlling-updatepanel-animations-vb
msc.type: authoredcontent
ms.openlocfilehash: 97a52bd75fdf63ad62282afd9df772f0a9e4f931
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78430858"
---
# <a name="dynamically-controlling-updatepanel-animations-vb"></a>UpdatePanel アニメーションを動的に制御する (VB)

[Christian Wenz](https://github.com/wenz)別

[コードのダウンロード](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation2.vb.zip)または[PDF のダウンロード](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation2VB.pdf)

> ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。 UpdatePanel の内容については、animation framework: Updateパネルアニメーションに大きく依存する特別な extender が存在します。 また、UpdatePanel トリガーと共に使用することもできます。

## <a name="overview"></a>概要

ASP.NET AJAX Control Toolkit のアニメーションコントロールは、コントロールだけではなく、コントロールにアニメーションを追加するためのフレームワーク全体です。 `UpdatePanel`の内容については、`UpdatePanelAnimation`のアニメーションフレームワークに大きく依存する特別な extender が存在します。 また、`UpdatePanel` トリガーと共に使用することもできます。

## <a name="steps"></a>手順

最初の手順は通常どおり、ASP.NET AJAX ライブラリが読み込まれ、Control Toolkit を使用できるように、ページに `ScriptManager` を含めることです。

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-vb/samples/sample1.aspx)]

このシナリオのアニメーションは、現在の時刻の表示に適用されます。 この情報は、`Page_Load()` メソッドを使用してラベルに書き込むことができます (わかりやすくするために、次のインラインコードが使用されます)。

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-vb/samples/sample2.aspx)]

また、時間の更新をトリガーするボタンが作成されます。

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-vb/samples/sample3.aspx)]

このコードは、`UpdatePanel` 要素の `<ContentTemplate>` セクションに配置されます。 パネルの `UpdateMode` 属性は、トリガーのみがパネルの内容を更新する可能性があるため、`"Conditional"`に設定する必要があります。 `UpdatePanel`の `<Triggers>` セクションでは、非同期ポストバックトリガーが作成され、ボタンの `Click` イベントに関連付けられます。 このため、ユーザーがボタンをクリックすると、`UpdatePanel` が更新されます。 `UpdatePanel` コントロールのマークアップを次に示します。

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-vb/samples/sample4.aspx)]

最後に、`UpdatePanelAnimationExtender` を構成する必要があります。 `TargetControlID` 属性をパネルの ID に設定し、extender 内でアニメーションを定義します。 でのフェードは意味があり、更新された時間を視覚的に強調表示します。 Extender マークアップは次のようになります。

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-vb/samples/sample5.aspx)]

ブラウザーでファイルを実行します。 ボタンをクリックするたびに、現在の時刻がパネルに表示されます。1秒間は常にフェードします。

[現在の時刻がフェードイン ![](dynamically-controlling-updatepanel-animations-vb/_static/image2.png)](dynamically-controlling-updatepanel-animations-vb/_static/image1.png)

現在の時刻はフェードインします ([クリックすると、フルサイズの画像が表示](dynamically-controlling-updatepanel-animations-vb/_static/image3.png)されます)

> [!div class="step-by-step"]
> [[戻る]](animating-an-updatepanel-control-vb.md)
