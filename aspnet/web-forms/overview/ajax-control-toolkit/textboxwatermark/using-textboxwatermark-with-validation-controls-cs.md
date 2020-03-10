---
uid: web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-with-validation-controls-cs
title: 検証コントロールでの TextBoxWatermark のC#使用 () |Microsoft Docs
author: wenz
description: AJAX コントロールツールキットの TextBoxWatermark コントロールは、テキストがボックス内に表示されるようにテキストボックスを拡張します。 ユーザーがボックスをクリックすると、...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: d49940cb-d38c-456a-b800-5f0eb705d09f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-with-validation-controls-cs
msc.type: authoredcontent
ms.openlocfilehash: bc9498b1c5ba2f38b90706c9200ffa813a945fa9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78466588"
---
# <a name="using-textboxwatermark-with-validation-controls-c"></a>検証コントロールと共に TextBoxWatermark を使用する (C#)

[Christian Wenz](https://github.com/wenz)別

[コードのダウンロード](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/TextBoxWatermark2.cs.zip)または[PDF のダウンロード](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/textboxwatermark2CS.pdf)

> AJAX コントロールツールキットの TextBoxWatermark コントロールは、テキストがボックス内に表示されるようにテキストボックスを拡張します。 ユーザーがボックスをクリックすると、そのボックスは空になります。 ユーザーがテキストを入力せずにボックスを離れると、事前テキストが再び表示されます。 これは、同じページの ASP.NET 検証コントロールと競合する可能性がありますが、これらの問題は解決される可能性があります。

## <a name="overview"></a>概要

AJAX コントロールツールキットの `TextBoxWatermark` コントロールは、テキストがボックス内に表示されるようにテキストボックスを拡張します。 ユーザーがボックスをクリックすると、そのボックスは空になります。 ユーザーがテキストを入力せずにボックスを離れると、事前テキストが再び表示されます。 これは、同じページの ASP.NET 検証コントロールと競合する可能性がありますが、これらの問題は解決される可能性があります。

## <a name="steps"></a>手順

このサンプルの基本的な設定は次のとおりです。 `TextBox` コントロールは、`TextBoxWatermarkExtender` コントロールを使用して目標ます。 ボタンはポストバックをトリガーし、後でページの検証コントロールをトリガーするために使用されます。 また、ASP.NET AJAX を初期化するには、`ScriptManager` コントロールが必要です。

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-cs/samples/sample1.aspx)]

次に、フォームが送信されたときにフィールドにテキストがあるかどうかを確認する `RequiredFieldValidator` コントロールを追加します。 バリデーターの `InitialValue` プロパティは、`TextBoxWatermarkExtender` コントロールで使用されているのと同じ値に設定する必要があります。フォームが送信されると、変更されていないテキストボックスの値は、その中の基準値になります。

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-cs/samples/sample2.aspx)]

ただし、この方法には1つの問題があります。クライアントが JavaScript を無効にした場合は、テキストフィールドがウォーターマークテキストに事前されないため、`RequiredFieldValidator` はエラーメッセージをトリガーしません。 そのため、2番目の `RequiredFieldValidator` コントロールが必要です。このコントロールでは、空のテキストボックスを確認します (`InitialValue` 属性を省略します)。

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-cs/samples/sample3.aspx)]

両方の検証コントロールで `Display`=`"Dynamic"`が使用されるため、エンドユーザーは2つの検証コントロールのどちらを起動したかを視覚的に区別することはできません。そのうちの1つだけがあるようです。

最後に、検証コントロールによってエラーメッセージが発行されなかった場合に、フィールドにテキストを出力するサーバー側コードを追加します。

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-cs/samples/sample4.aspx)]

[検証コントロールの ![、フィールドにテキストがないことを示しています。](using-textboxwatermark-with-validation-controls-cs/_static/image2.png)](using-textboxwatermark-with-validation-controls-cs/_static/image1.png)

検証コントロールは、フィールドにテキストがないことを示しています ([クリックすると、フルサイズの画像が表示](using-textboxwatermark-with-validation-controls-cs/_static/image3.png)されます)

> [!div class="step-by-step"]
> [前へ](using-textboxwatermark-in-a-formview-cs.md)
> [次へ](using-textboxwatermark-in-a-formview-vb.md)
