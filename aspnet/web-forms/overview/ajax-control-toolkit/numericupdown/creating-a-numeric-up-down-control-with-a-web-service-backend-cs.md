---
uid: web-forms/overview/ajax-control-toolkit/numericupdown/creating-a-numeric-up-down-control-with-a-web-service-backend-cs
title: Web サービスバックエンド (C#) を使用した数値のアップダウンコントロールの作成Microsoft Docs
author: wenz
description: ユーザーがチェックボックスに値を入力するのではなく、(Windows およびその他のオペレーティングシステムに存在する) 数値のアップ/ダウンコントロールで、さらに c...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: c99bbc72-d4de-41ed-92a4-9a4632368363
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/numericupdown/creating-a-numeric-up-down-control-with-a-web-service-backend-cs
msc.type: authoredcontent
ms.openlocfilehash: 816a840b9e93b95a049c3a4cb792e9deeab28983
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74598911"
---
# <a name="creating-a-numeric-updown-control-with-a-web-service-backend-c"></a>Web サービス バックエンドで数値を上げ下げするコントロールを作成する (C#)

[Christian Wenz](https://github.com/wenz)別

[コードのダウンロード](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/numericupdown1.cs.zip)または[PDF のダウンロード](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/numericupdown1CS.pdf)

> ユーザーがチェックボックスに値を入力する代わりに、数値のアップ/ダウンコントロール (Windows およびその他のオペレーティングシステムに存在) を確認することで、より快適に証明できます。 既定では、NumericUpDown コントロールの値は常に1ずつ増加または減少しますが、web サービスの方が柔軟性が高くなります。

## <a name="overview"></a>の概要

ユーザーがチェックボックスに値を入力する代わりに、数値のアップ/ダウンコントロール (Windows およびその他のオペレーティングシステムに存在) を確認することで、より快適に証明できます。 既定では、`NumericUpDown` コントロールの値は常に1ずつ増加または減少しますが、web サービスの方が柔軟性が高くなります。

## <a name="steps"></a>手順

ASP.NET AJAX Control Toolkit には、テキストボックスに2つのボタンが自動的に追加される `NumericUpDown` extender が含まれています。1つは値を大きくするためのボタンで、もう1つは値を小さくするためのものです。 ただし、コントロールでは、web サービス呼び出し (またはページメソッド呼び出し) もサポートされています。 上矢印または下矢印ボタンがクリックされるたびに、JavaScript コードは web サーバーに接続し、そこでメソッドを実行します。 メソッドシグネチャは次のとおりです。

[!code-csharp[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/samples/sample1.cs)]

`current` 引数は、テキストボックス内の現在の値です。`tag` 属性は、`NumericUpDown` extender のプロパティとして設定できる追加のコンテキストデータです (ただし、必須ではありません)。

このサンプルでは、数値のアップダウンコントロールでは、2の累乗値 (1、2、4、8、16、32、64など) のみを許可する必要があります。 そのため、ユーザーが値を大きくするときに実行されるメソッドは、古い値を2倍にする必要があります。もう1つの方法では、値を2で割る必要があります。 完全な web サービスを次に示します。

[!code-aspx[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/samples/sample2.aspx)]

最後に、新しい ASP.NET ページを作成します。 通常どおり、`ScriptManager` コントロール、`TextBox` コントロール、および `NumericUpDownExtender` コントロールが必要です。 後者の場合は、web サービスの情報を提供する必要があります。

- ダウン web メソッドまたはページメソッドの `ServiceDownMethod` 名
- down service メソッドを使用して web サービスへのパスを `ServiceDownPath` します。page メソッドを使用している場合は省略する
- アップ web メソッドまたはページメソッドの `ServiceUpMethod` 名
- up service メソッドを使用して web サービスへのパスを `ServiceUpPath` します。page メソッドを使用している場合は省略する

ページの完全なマークアップを次に示します。

[!code-aspx[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/samples/sample3.aspx)]

ページを実行すると、上部のボタンをクリックしたときにテキストボックス内の値が常に2倍になり、下部のボタンをクリックすると、その値が半分になります。

[2の累乗の数値のみが表示される ![](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/_static/image2.png)](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/_static/image1.png)

2の累乗の数値のみが表示されます ([クリックすると、フルサイズの画像が表示](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/_static/image3.png)されます)

> [!div class="step-by-step"]
> [次へ](creating-a-numeric-up-down-control-with-a-web-service-backend-vb.md)
