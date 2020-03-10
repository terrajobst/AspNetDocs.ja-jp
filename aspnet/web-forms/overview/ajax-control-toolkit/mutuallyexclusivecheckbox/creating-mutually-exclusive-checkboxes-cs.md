---
uid: web-forms/overview/ajax-control-toolkit/mutuallyexclusivecheckbox/creating-mutually-exclusive-checkboxes-cs
title: 相互排他的なチェックC#ボックスを作成する () |Microsoft Docs
author: wenz
description: 選択できるオプションのセットが1つだけの場合は、通常、ラジオボタンが使用されます。 ただし、グループ内の1つのオプションボタンが選択されると、欠点があり,...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 8e11b813-ba0d-4c29-b0f8-f65db6dbef1e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/mutuallyexclusivecheckbox/creating-mutually-exclusive-checkboxes-cs
msc.type: authoredcontent
ms.openlocfilehash: ddc154601752cc856f00dd4f3207952ab7e0e3e0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78496786"
---
# <a name="creating-mutually-exclusive-checkboxes-c"></a>相互に排他的なチェックボックスを作成する (C#)

[Christian Wenz](https://github.com/wenz)別

[コードのダウンロード](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/MutuallyExclusiveCheckBox0.cs.zip)または[PDF のダウンロード](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/mutuallyexclusivecheckbox0CS.pdf)

> 選択できるオプションのセットが1つだけの場合は、通常、ラジオボタンが使用されます。 ただし、欠点があります。グループ内の1つのラジオボタンを選択すると、すべてのラジオボタンをオフにすることはできません。 チェックボックスは、いつでもオフにすることができますが、相互に排他的ではありません。 このチュートリアルでは、2つのアプローチ (相互に排他的なチェックボックス) について説明します。

## <a name="overview"></a>概要

選択できるオプションのセットが1つだけの場合は、通常、ラジオボタンが使用されます。 ただし、欠点があります。グループ内の1つのラジオボタンを選択すると、すべてのラジオボタンをオフにすることはできません。 チェックボックスは、いつでもオフにすることができますが、相互に排他的ではありません。 このチュートリアルでは、2つのアプローチ (相互に排他的なチェックボックス) について説明します。

## <a name="steps"></a>手順

ASP.NET AJAX Control Toolkit には、MutuallyExclusiveCheckBox extender が含まれています。 これにより、プログラマは任意のチェックボックスをグループ名 (`Key` 属性) に割り当てることができます。 同じグループ内のすべてのチェックボックスから、一度に選択できるのは1つだけです。

2つのチェックボックスを新しい ASP.NET ページに配置してみましょう。 多くの場合もありますが、そのうちの2つは、原則を示すのに十分です。

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-cs/samples/sample1.aspx)]

両方のチェックボックスについて、MutuallyExclusiveCheckBoxExtender コントロールをページに配置する必要があります。 両方のキー属性は、同じ値を持つ必要があります。これは、HTML ラジオボタン要素の値属性が所属するグループを示すのと同じである必要があるためです。 エクステンダーの TargetControlID プロパティは、チェックボックスの ID を指します。

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-cs/samples/sample2.aspx)]

最後に、ASP.NET AJAX Control Toolkit のすべての要素に必要な ASP.NET AJAX `ScriptManager` を含めます。

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-cs/samples/sample3.aspx)]

ページを保存して実行する: 両方のチェックボックスをオンまたはオフにできますが、両方のチェックボックスをオンにすることはできません。

[一度にチェックできるチェックボックスは1つだけ ![](creating-mutually-exclusive-checkboxes-cs/_static/image2.png)](creating-mutually-exclusive-checkboxes-cs/_static/image1.png)

チェックボックスは一度に1つしかチェックできません ([クリックすると、フルサイズの画像が表示](creating-mutually-exclusive-checkboxes-cs/_static/image3.png)されます)

> [!div class="step-by-step"]
> [Next](creating-mutually-exclusive-checkboxes-vb.md)
