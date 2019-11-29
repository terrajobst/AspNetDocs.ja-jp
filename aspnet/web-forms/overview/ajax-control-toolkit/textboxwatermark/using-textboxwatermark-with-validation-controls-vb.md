---
uid: web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-with-validation-controls-vb
title: 検証コントロールでの TextBoxWatermark の使用 (VB) |Microsoft Docs
author: wenz
description: AJAX コントロールツールキットの TextBoxWatermark コントロールは、テキストがボックス内に表示されるようにテキストボックスを拡張します。 ユーザーがボックスをクリックすると、...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e6c2cb98-f745-4bc8-973a-813879c8a891
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-with-validation-controls-vb
msc.type: authoredcontent
ms.openlocfilehash: 141cae26c9e52be510e2a5a8f816cbac977dcf3d
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74597236"
---
# <a name="using-textboxwatermark-with-validation-controls-vb"></a>検証コントロールと共に TextBoxWatermark を使用する (VB)

[Christian Wenz](https://github.com/wenz)別

[コードのダウンロード](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/TextBoxWatermark2.vb.zip)または[PDF のダウンロード](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/textboxwatermark2VB.pdf)

> AJAX コントロールツールキットの TextBoxWatermark コントロールは、テキストがボックス内に表示されるようにテキストボックスを拡張します。 ユーザーがボックスをクリックすると、そのボックスは空になります。 ユーザーがテキストを入力せずにボックスを離れると、事前テキストが再び表示されます。 これは、同じページの ASP.NET 検証コントロールと競合する可能性がありますが、これらの問題は解決される可能性があります。

## <a name="overview"></a>の概要

AJAX コントロールツールキットの `TextBoxWatermark` コントロールは、テキストがボックス内に表示されるようにテキストボックスを拡張します。 ユーザーがボックスをクリックすると、そのボックスは空になります。 ユーザーがテキストを入力せずにボックスを離れると、事前テキストが再び表示されます。 これは、同じページの ASP.NET 検証コントロールと競合する可能性がありますが、これらの問題は解決される可能性があります。

## <a name="steps"></a>手順

このサンプルの基本的な設定は次のとおりです。 `TextBox` コントロールは、`TextBoxWatermarkExtender` コントロールを使用して目標ます。 ボタンはポストバックをトリガーし、後でページの検証コントロールをトリガーするために使用されます。 また、ASP.NET AJAX を初期化するには、`ScriptManager` コントロールが必要です。

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-vb/samples/sample1.aspx)]

次に、フォームが送信されたときにフィールドにテキストがあるかどうかを確認する `RequiredFieldValidator` コントロールを追加します。 バリデーターの `InitialValue` プロパティは、`TextBoxWatermarkExtender` コントロールで使用されているのと同じ値に設定する必要があります。フォームが送信されると、変更されていないテキストボックスの値は、その中の基準値になります。

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-vb/samples/sample2.aspx)]

ただし、この方法には1つの問題があります。クライアントが JavaScript を無効にした場合は、テキストフィールドがウォーターマークテキストに事前されないため、`RequiredFieldValidator` はエラーメッセージをトリガーしません。 そのため、2番目の `RequiredFieldValidator` コントロールが必要です。このコントロールでは、空のテキストボックスを確認します (`InitialValue` 属性を省略します)。

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-vb/samples/sample3.aspx)]

両方の検証コントロールで `Display`=`"Dynamic"`が使用されるため、エンドユーザーは2つの検証コントロールのどちらを起動したかを視覚的に区別することはできません。そのうちの1つだけがあるようです。

最後に、検証コントロールによってエラーメッセージが発行されなかった場合に、フィールドにテキストを出力するサーバー側コードを追加します。

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-vb/samples/sample4.aspx)]

[検証コントロールの ![、フィールドにテキストがないことを示しています。](using-textboxwatermark-with-validation-controls-vb/_static/image2.png)](using-textboxwatermark-with-validation-controls-vb/_static/image1.png)

検証コントロールは、フィールドにテキストがないことを示しています ([クリックすると、フルサイズの画像が表示](using-textboxwatermark-with-validation-controls-vb/_static/image3.png)されます)

> [!div class="step-by-step"]
> [前へ](using-textboxwatermark-in-a-formview-vb.md)
