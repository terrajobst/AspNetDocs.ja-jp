---
uid: web-forms/overview/ajax-control-toolkit/rating/creating-a-rating-control-vb
title: 評価コントロールを作成する (VB) |Microsoft Docs
author: wenz
description: E コマースからコミュニティサイトまで、多くの web サイトでは、記事や項目を評価することができます。 これには通常、いくつかのコーディング作業が必要ですが、
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 6d0d70f4-725e-4258-8ae8-24a6ba1ddbf7
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/rating/creating-a-rating-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 08e245edfe73db4e3896db51151e5d7a0fa9697c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78496036"
---
# <a name="creating-a-rating-control-vb"></a>評価コントロールを作成する (VB)

[Christian Wenz](https://github.com/wenz)別

[コードのダウンロード](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/rating0.vb.zip)または[PDF のダウンロード](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/rating0VB.pdf)

> E コマースからコミュニティサイトまで、多くの web サイトでは、記事や項目を評価することができます。 これには通常、何らかのコーディング作業が必要ですが、制御ツールキットが用意されています。

## <a name="overview"></a>概要

E コマースからコミュニティサイトまで、多くの web サイトでは、記事や項目を評価することができます。 これには通常、何らかのコーディング作業が必要ですが、制御ツールキットが用意されています。

## <a name="steps"></a>手順

まず、2種類のイメージ (少なくとも) が必要です。1つは、入力された評価項目用で、もう1つは空の評価項目用です。 通常、評価項目は星またはスマイルです。 このシナリオでは、このチュートリアルのソースコードのダウンロードの一部として、3つのファイル、smiley-done、および空の .png とを見つけます。

次に、新しい ASP.NET ファイルを作成し、`ScriptManager` コントロールの追加を開始します。

[!code-aspx[Main](creating-a-rating-control-vb/samples/sample1.aspx)]

次に、ASP.NET AJAX Control Toolkit から `Rating` コントロールを追加します。 この例では、次の属性を設定する必要があります。

- 使用する初期評価を `CurrentRating` します
- 最大評価の `MaxRating`
- 評価項目 (星) が空のときに使用する CSS クラスを `EmptyStarCssClass` します
- 評価項目 (星) が入力されたときに使用する CSS クラスを `FilledStarCssClass` します
- 表示される stat に使用する CSS クラスを `StarCssClass` します
- 星評価がサーバーに送り返されるときに使用する CSS クラスを `WaitingStarCssClass` します

次に示すのは、5つの項目 (smileys) を持つ評価コントロールを作成するマークアップです。この場合、最初は何も入力されません。

[!code-aspx[Main](creating-a-rating-control-vb/samples/sample2.aspx)]

参照される3つの CSS クラスは、CSS を使用して簡単に実行できる適切なイメージファイルを表示する必要があります。

[!code-css[Main](creating-a-rating-control-vb/samples/sample3.css)]

3つのイメージの幅と高さを指定していることを確認してください。そうしないと、表示が少し失敗に見えます。

最後に、評価の結果がユーザーに表示される (少なくともデータベースに保存されている) 必要があります。 そのため、テキストメッセージの出力のラベルと、評価フォームをサーバーにポストバックするための [送信] ボタンを追加します。

[!code-aspx[Main](creating-a-rating-control-vb/samples/sample4.aspx)]

サーバー側コードで、`ID` を使用して評価コントロールにアクセスし、選択した評価項目の番号である `CurrentRating` プロパティにアクセスします。この例では、0 ~ 5 の値を使用します。

[!code-aspx[Main](creating-a-rating-control-vb/samples/sample5.aspx)]

ページを保存し、ブラウザーに読み込みます。 (最初に空になっている) 評価項目をポイントすると、JavaScript の効果が発生します。評価が変更されます。 星のセットをクリックすると、現在の評価が保持されます。 最後に、フォームを送信すると、サーバー側のコードによって、選択した評価が出力されます。

[最小限のコードで評価システムを作成 ![には](creating-a-rating-control-vb/_static/image2.png)](creating-a-rating-control-vb/_static/image1.png)

最小限のコードで評価システムを作成[する (クリックすると、フルサイズの画像が表示](creating-a-rating-control-vb/_static/image3.png)されます)

> [!div class="step-by-step"]
> [[戻る]](creating-a-rating-control-cs.md)
