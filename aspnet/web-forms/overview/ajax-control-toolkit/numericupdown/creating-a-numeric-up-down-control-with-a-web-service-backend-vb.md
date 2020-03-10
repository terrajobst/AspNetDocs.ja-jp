---
uid: web-forms/overview/ajax-control-toolkit/numericupdown/creating-a-numeric-up-down-control-with-a-web-service-backend-vb
title: Web サービスバックエンドを使用した数値のアップダウンコントロールの作成 (VB) |Microsoft Docs
author: wenz
description: ユーザーがチェックボックスに値を入力するのではなく、(Windows およびその他のオペレーティングシステムに存在する) 数値のアップ/ダウンコントロールで、さらに c...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: afa59dfa-fef1-43d3-8fdd-aea3be36ed3c
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/numericupdown/creating-a-numeric-up-down-control-with-a-web-service-backend-vb
msc.type: authoredcontent
ms.openlocfilehash: 2bf6e1b27180589d39e308de62b5be1f47fa8fe2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78496720"
---
# <a name="creating-a-numeric-updown-control-with-a-web-service-backend-vb"></a>Web サービス バックエンドで数値を上げ下げするコントロールを作成する (VB)

[Christian Wenz](https://github.com/wenz)別

[コードのダウンロード](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/numericupdown1.vb.zip)または[PDF のダウンロード](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/numericupdown1VB.pdf)

> ユーザーがチェックボックスに値を入力する代わりに、数値のアップ/ダウンコントロール (Windows およびその他のオペレーティングシステムに存在) を確認することで、より快適に証明できます。 既定では、NumericUpDown コントロールの値は常に1ずつ増加または減少しますが、web サービスの方が柔軟性が高くなります。

## <a name="overview"></a>概要

ユーザーがチェックボックスに値を入力する代わりに、数値のアップ/ダウンコントロール (Windows およびその他のオペレーティングシステムに存在) を確認することで、より快適に証明できます。 既定では、`NumericUpDown` コントロールの値は常に1ずつ増加または減少しますが、web サービスの方が柔軟性が高くなります。

## <a name="steps"></a>手順

ASP.NET AJAX Control Toolkit には、テキストボックスに2つのボタンが自動的に追加される `NumericUpDown` extender が含まれています。1つは値を大きくするためのボタンで、もう1つは値を小さくするためのものです。 ただし、コントロールでは、web サービス呼び出し (またはページメソッド呼び出し) もサポートされています。 上矢印または下矢印ボタンがクリックされるたびに、JavaScript コードは web サーバーに接続し、そこでメソッドを実行します。 メソッドシグネチャは次のとおりです。

[!code-vb[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/samples/sample1.vb)]

`current` 引数は、テキストボックス内の現在の値です。`tag` 属性は、`NumericUpDown` extender のプロパティとして設定できる追加のコンテキストデータです (ただし、必須ではありません)。

このサンプルでは、数値のアップダウンコントロールでは、2の累乗値 (1、2、4、8、16、32、64など) のみを許可する必要があります。 そのため、ユーザーが値を大きくするときに実行されるメソッドは、古い値を2倍にする必要があります。もう1つの方法では、値を2で割る必要があります。 完全な web サービスを次に示します。

[!code-aspx[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/samples/sample2.aspx)]

最後に、新しい ASP.NET ページを作成します。 通常どおり、`ScriptManager` コントロール、`TextBox` コントロール、および `NumericUpDownExtender` コントロールが必要です。 後者の場合は、web サービスの情報を提供する必要があります。

- ダウン web メソッドまたはページメソッドの `ServiceDownMethod` 名
- down service メソッドを使用して web サービスへのパスを `ServiceDownPath` します。page メソッドを使用している場合は省略する
- アップ web メソッドまたはページメソッドの `ServiceUpMethod` 名
- up service メソッドを使用して web サービスへのパスを `ServiceUpPath` します。page メソッドを使用している場合は省略する

ページの完全なマークアップを次に示します。

[!code-aspx[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/samples/sample3.aspx)]

ページを実行すると、上部のボタンをクリックしたときにテキストボックス内の値が常に2倍になり、下部のボタンをクリックすると、その値が半分になります。

[2の累乗の数値のみが表示される ![](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/_static/image2.png)](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/_static/image1.png)

2の累乗の数値のみが表示されます ([クリックすると、フルサイズの画像が表示](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/_static/image3.png)されます)

> [!div class="step-by-step"]
> [[戻る]](creating-a-numeric-up-down-control-with-a-web-service-backend-cs.md)
