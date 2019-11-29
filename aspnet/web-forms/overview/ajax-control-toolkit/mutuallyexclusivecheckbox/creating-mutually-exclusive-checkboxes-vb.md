---
uid: web-forms/overview/ajax-control-toolkit/mutuallyexclusivecheckbox/creating-mutually-exclusive-checkboxes-vb
title: 相互排他的なチェックボックスを作成する (VB) |Microsoft Docs
author: wenz
description: 選択できるオプションのセットが1つだけの場合は、通常、ラジオボタンが使用されます。 ただし、グループ内の1つのオプションボタンが選択されると、欠点があり,...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e9dd1d5a-a1db-4114-981d-6a91acb1d709
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/mutuallyexclusivecheckbox/creating-mutually-exclusive-checkboxes-vb
msc.type: authoredcontent
ms.openlocfilehash: f33936dd4d71f6bbf08f02966eefe44c8c152eba
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74606462"
---
# <a name="creating-mutually-exclusive-checkboxes-vb"></a>相互に排他的なチェックボックスを作成する (VB)

[Christian Wenz](https://github.com/wenz)別

[コードのダウンロード](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/MutuallyExclusiveCheckBox0.vb.zip)または[PDF のダウンロード](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/mutuallyexclusivecheckbox0VB.pdf)

> 選択できるオプションのセットが1つだけの場合は、通常、ラジオボタンが使用されます。 ただし、欠点があります。グループ内の1つのラジオボタンを選択すると、すべてのラジオボタンをオフにすることはできません。 チェックボックスは、いつでもオフにすることができますが、相互に排他的ではありません。 このチュートリアルでは、2つのアプローチ (相互に排他的なチェックボックス) について説明します。

## <a name="overview"></a>の概要

選択できるオプションのセットが1つだけの場合は、通常、ラジオボタンが使用されます。 ただし、欠点があります。グループ内の1つのラジオボタンを選択すると、すべてのラジオボタンをオフにすることはできません。 チェックボックスは、いつでもオフにすることができますが、相互に排他的ではありません。 このチュートリアルでは、2つのアプローチ (相互に排他的なチェックボックス) について説明します。

## <a name="steps"></a>手順

ASP.NET AJAX Control Toolkit には、MutuallyExclusiveCheckBox extender が含まれています。 これにより、プログラマは任意のチェックボックスをグループ名 (`Key` 属性) に割り当てることができます。 同じグループ内のすべてのチェックボックスから、一度に選択できるのは1つだけです。

2つのチェックボックスを新しい ASP.NET ページに配置してみましょう。 多くの場合もありますが、そのうちの2つは、原則を示すのに十分です。

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-vb/samples/sample1.aspx)]

両方のチェックボックスについて、MutuallyExclusiveCheckBoxExtender コントロールをページに配置する必要があります。 両方のキー属性は、同じ値を持つ必要があります。これは、HTML ラジオボタン要素の値属性が所属するグループを示すのと同じである必要があるためです。 エクステンダーの TargetControlID プロパティは、チェックボックスの ID を指します。

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-vb/samples/sample2.aspx)]

最後に、ASP.NET AJAX Control Toolkit のすべての要素に必要な ASP.NET AJAX `ScriptManager` を含めます。

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-vb/samples/sample3.aspx)]

ページを保存して実行する: 両方のチェックボックスをオンまたはオフにできますが、両方のチェックボックスをオンにすることはできません。

[一度にチェックできるチェックボックスは1つだけ ![](creating-mutually-exclusive-checkboxes-vb/_static/image2.png)](creating-mutually-exclusive-checkboxes-vb/_static/image1.png)

チェックボックスは一度に1つしかチェックできません ([クリックすると、フルサイズの画像が表示](creating-mutually-exclusive-checkboxes-vb/_static/image3.png)されます)

> [!div class="step-by-step"]
> [前へ](creating-mutually-exclusive-checkboxes-cs.md)
