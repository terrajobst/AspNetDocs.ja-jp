---
uid: web-forms/overview/ajax-control-toolkit/rating/creating-a-rating-control-cs
title: 評価コントロールを作成するC#() |Microsoft Docs
author: wenz
description: E コマースからコミュニティサイトまで、多くの web サイトでは、記事や項目を評価することができます。 これには通常、いくつかのコーディング作業が必要ですが、
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 969fb28f-2bff-4fc4-b24a-27f5e2534a37
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/rating/creating-a-rating-control-cs
msc.type: authoredcontent
ms.openlocfilehash: c0bf793406e378321f54f0460031c526a0b41a02
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74611576"
---
# <a name="creating-a-rating-control-c"></a>評価コントロールを作成する (C#)

[Christian Wenz](https://github.com/wenz)別

[コードのダウンロード](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/rating0.cs.zip)または[PDF のダウンロード](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/rating0CS.pdf)

> E コマースからコミュニティサイトまで、多くの web サイトでは、記事や項目を評価することができます。 これには通常、何らかのコーディング作業が必要ですが、制御ツールキットが用意されています。

## <a name="overview"></a>の概要

E コマースからコミュニティサイトまで、多くの web サイトでは、記事や項目を評価することができます。 これには通常、何らかのコーディング作業が必要ですが、制御ツールキットが用意されています。

## <a name="steps"></a>手順

まず、2種類のイメージ (少なくとも) が必要です。1つは、入力された評価項目用で、もう1つは空の評価項目用です。 通常、評価項目は星またはスマイルです。 このシナリオでは、このチュートリアルのソースコードのダウンロードの一部として、3つのファイル、smiley-done、および空の .png とを見つけます。

次に、新しい ASP.NET ファイルを作成し、`ScriptManager` コントロールの追加を開始します。

[!code-aspx[Main](creating-a-rating-control-cs/samples/sample1.aspx)]

次に、ASP.NET AJAX Control Toolkit から `Rating` コントロールを追加します。 この例では、次の属性を設定する必要があります。

- 使用する初期評価を `CurrentRating` します
- 最大評価の `MaxRating`
- 評価項目 (星) が空のときに使用する CSS クラスを `EmptyStarCssClass` します
- 評価項目 (星) が入力されたときに使用する CSS クラスを `FilledStarCssClass` します
- 表示される stat に使用する CSS クラスを `StarCssClass` します
- 星評価がサーバーに送り返されるときに使用する CSS クラスを `WaitingStarCssClass` します

次に示すのは、5つの項目 (smileys) を持つ評価コントロールを作成するマークアップです。この場合、最初は何も入力されません。

[!code-aspx[Main](creating-a-rating-control-cs/samples/sample2.aspx)]

参照される3つの CSS クラスは、CSS を使用して簡単に実行できる適切なイメージファイルを表示する必要があります。

[!code-css[Main](creating-a-rating-control-cs/samples/sample3.css)]

3つのイメージの幅と高さを指定していることを確認してください。そうしないと、表示が少し失敗に見えます。

最後に、評価の結果がユーザーに表示される (少なくともデータベースに保存されている) 必要があります。 そのため、テキストメッセージの出力のラベルと、評価フォームをサーバーにポストバックするための [送信] ボタンを追加します。

[!code-aspx[Main](creating-a-rating-control-cs/samples/sample4.aspx)]

サーバー側コードで、`ID` を使用して評価コントロールにアクセスし、選択した評価項目の番号である `CurrentRating` プロパティにアクセスします。この例では、0 ~ 5 の値を使用します。

[!code-aspx[Main](creating-a-rating-control-cs/samples/sample5.aspx)]

ページを保存し、ブラウザーに読み込みます。 (最初に空になっている) 評価項目をポイントすると、JavaScript の効果が発生します。評価が変更されます。 星のセットをクリックすると、現在の評価が保持されます。 最後に、フォームを送信すると、サーバー側のコードによって、選択した評価が出力されます。

[最小限のコードで評価システムを作成 ![には](creating-a-rating-control-cs/_static/image2.png)](creating-a-rating-control-cs/_static/image1.png)

最小限のコードで評価システムを作成[する (クリックすると、フルサイズの画像が表示](creating-a-rating-control-cs/_static/image3.png)されます)

> [!div class="step-by-step"]
> [次へ](creating-a-rating-control-vb.md)
