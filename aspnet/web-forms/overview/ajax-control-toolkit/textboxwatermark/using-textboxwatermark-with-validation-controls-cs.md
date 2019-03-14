---
uid: web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-with-validation-controls-cs
title: (C#) の検証コントロールと共に TextBoxWatermark を使用 |Microsoft Docs
author: wenz
description: AJAX Control Toolkit で TextBoxWatermark コントロールでは、テキスト ボックスを拡張するので、ボックス内でテキストが表示されます。 ボックスに、ユーザーがクリックしたときに.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: d49940cb-d38c-456a-b800-5f0eb705d09f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-with-validation-controls-cs
msc.type: authoredcontent
ms.openlocfilehash: 35dd340ffce7b83303a44a0d6532ce73be5350f0
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57064729"
---
<a name="using-textboxwatermark-with-validation-controls-c"></a>検証コントロールと共に TextBoxWatermark を使用する (C#)
====================
によって[Christian Wenz](https://github.com/wenz)

[コードのダウンロード](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/TextBoxWatermark2.cs.zip)または[PDF のダウンロード](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/textboxwatermark2CS.pdf)

> AJAX Control Toolkit で TextBoxWatermark コントロールでは、テキスト ボックスを拡張するので、ボックス内でテキストが表示されます。 ボックスに、ユーザーがクリックするは空になります。 ユーザーがテキストを入力しなくても、ボックスのまま、指定済みのテキストが表示されます。 これは、同じ ページで、ASP.NET 検証コントロールと衝突する可能性がありますが、これらの問題を克服することがあります。


## <a name="overview"></a>概要

`TextBoxWatermark`ボックス内でテキストが表示されるように、AJAX Control Toolkit のコントロールがテキスト ボックスを拡張します。 ボックスに、ユーザーがクリックするは空になります。 ユーザーがテキストを入力しなくても、ボックスのまま、指定済みのテキストが表示されます。 これは、同じ ページで、ASP.NET 検証コントロールと衝突する可能性がありますが、これらの問題を克服することがあります。

## <a name="steps"></a>手順

サンプルの基本的なセットアップは、次:`TextBox`を使用してコントロールを透かし、`TextBoxWatermarkExtender`コントロール。 ボタンは、ポストバックをトリガーし、後で、ページの検証コントロールのトリガーに使用されます。 また、`ScriptManager`コントロールが ASP.NET AJAX を初期化するために必要です。

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-cs/samples/sample1.aspx)]

ここで追加、`RequiredFieldValidator`かどうかにテキストが、フィールド、フォームが送信されたときにチェックするコントロール。 `InitialValue`検証コントロールのプロパティで使用されているのと同じ値に設定する必要があります、`TextBoxWatermarkExtender`コントロール。フォームが送信されたときに、変更されていないテキスト ボックスの値はその中の基準値に。

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-cs/samples/sample2.aspx)]

ただしこのアプローチの 1 つの問題があります。場合は、クライアントは、JavaScript を無効化、テキスト フィールドがないあらかじめ入力されています、透かしテキストをそのため、`RequiredFieldValidator`エラー メッセージは発生しません。 そのため、2 つ目`RequiredFieldValidator`コントロールが必要ですが、空のテキスト ボックスを確認します (省略すると、`InitialValue`属性)。

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-cs/samples/sample3.aspx)]

両方の検証コントロールを使用しているため`Display` = `"Dynamic"`、エンドユーザーが発生した、この 2 つの検証コントロールの外観から区別できません。 代わりに、ように見えますが、1 つだけです。

最後に、検証コントロールには、エラー メッセージ発行いない場合、フィールド内のテキストを出力するいくつかのサーバー側コードを追加します。

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-cs/samples/sample4.aspx)]


[![検証コントロール文句を言う フィールドにテキストがないこと](using-textboxwatermark-with-validation-controls-cs/_static/image2.png)](using-textboxwatermark-with-validation-controls-cs/_static/image1.png)

検証コントロール文句を言う フィールドにテキストがないこと ([フルサイズの画像を表示する をクリックします](using-textboxwatermark-with-validation-controls-cs/_static/image3.png))。

> [!div class="step-by-step"]
> [前へ](using-textboxwatermark-in-a-formview-cs.md)
> [次へ](using-textboxwatermark-in-a-formview-vb.md)
