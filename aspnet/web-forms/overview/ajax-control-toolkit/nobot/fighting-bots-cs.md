---
uid: web-forms/overview/ajax-control-toolkit/nobot/fighting-bots-cs
title: 戦いボット (C#) |Microsoft Docs
author: wenz
description: 自動ボットは、ユーザー操作なしでコメントフォームを送信して、web サイトやスパムを plaster します。 ASP.NET AJAX Con の NoBot コントロール...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 0a1917e0-884a-4576-8e93-9ed660faae51
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/nobot/fighting-bots-cs
msc.type: authoredcontent
ms.openlocfilehash: fef55edf12a024e4dd66e2a18ea371ab4dac861f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78509068"
---
# <a name="fighting-bots-c"></a>ボットと戦う (C#)

[Christian Wenz](https://github.com/wenz)別

[コードのダウンロード](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/NoBot0.cs.zip)または[PDF のダウンロード](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/nobot0CS.pdf)

> 自動ボットは、ユーザー操作なしでコメントフォームを送信して、web サイトやスパムを plaster します。 ASP.NET AJAX Control Toolkit の NoBot コントロールは、これらのボットを戦うのに役立ちます。

## <a name="overview"></a>概要

自動ボットは、ユーザー操作なしでコメントフォームを送信して、web サイトやスパムを plaster します。 ASP.NET AJAX Control Toolkit の NoBot コントロールは、これらのボットを戦うのに役立ちます。

## <a name="steps"></a>手順

ボットを突破する一般的な方法の1つは、CAPTCHAs 完全に自動化されたパブリックチューリングテストを使用して、コンピューターと人間を区別することです。 チューリングテストはもともと、通信パートナーが人間とコンピューターのどちらであるかを判断する必要があるテストでした。 Web では、通常、CAPTCHA は、何らかの変形した文字を含むイメージで構成されます。 これは、人間だけが画像の文字を読み取ることができるのに対し、OCR アルゴリズムは失敗するということです。

この方法にはいくつかの長所と短所がありますが、このチュートリアルでは説明しません。 ただし、ASP.NET AJAX Control Toolkit には、`NoBot`と同様のアプローチを提供するコントロールがあります。 CAPTCHA を克服する方が簡単ですが、ブログなどの web サイトで非常に使いやすく、高速に使用できます。これは、ほとんどのスパム試行が敗北した場合に成功と見なされ、`NoBot` 制御が可能です。

次の条件のうち少なくとも1つが満たされている場合、`NoBot` は現在の ASP.NET web フォームのポストバックをインターセプトします。

- ブラウザーが JavaScript パズルの解決に失敗する (JavaScript が非アクティブになった場合など)
- ユーザーがフォームを高速に送信しました
- クライアントの IP アドレスが、一定期間内にフォームを頻繁に送信しました。

これらの条件を確認するために、`NoBot` コントロールには次の属性が必要です (これらの属性はすべて省略可能です)。

- ポストバックの間隔を `ResponseMinimumDelaySeconds` 最小値 (秒)
- 1つの IP からのポストバックが測定される時間間隔の長さ `CutoffWindowSeconds`
- 時間間隔 (秒単位) `CutoffMaximumInstances` 最大値

次のマークアップでは、ポストバックの間隔が2秒以上であることが要求されています。また、30秒間隔以内にポストバックが5回以下であることが必要です。

[!code-aspx[Main](fighting-bots-cs/samples/sample1.aspx)]

次に、通常どおり、ASP.NET AJAX ライブラリが読み込まれて Control Toolkit を使用できるように、ページに `ScriptManager` を含めます。

[!code-aspx[Main](fighting-bots-cs/samples/sample2.aspx)]

ほとんどのチェック `NoBot` はサーバー側で行われるため、これらの検証の結果を確認する必要があります。 これは `NoBot`の `IsValid()` メソッドを呼び出すことによって行うことができます。 これには、`NoBotState`型の1つの引数 (`out` パラメーター/`ByRef` パラメーター) があります。 この文字列形式には、チェックが失敗した理由が含まれており、それ以外の場合は `Valid` ます。 次のコードは、`NoBot`の結果に従ってメッセージを出力します。

[!code-aspx[Main](fighting-bots-cs/samples/sample3.aspx)]

最後に、フォームを送信し、メッセージを出力するラベル要素を作成する必要があります。完了しました。

[!code-aspx[Main](fighting-bots-cs/samples/sample4.aspx)]

このスクリプトを実行して JavaScript を非アクティブにしたり、最初の2秒以内にフォームを送信したり、30秒以内にフォームを送信したりすると、エラーメッセージが表示されます。 ただし、このコントロールは適切に使用します。これは、ユーザーの約90-95% だけが JavaScript をアクティブにしているため、ユーザーの5-10% は `NoBot`のテストに失敗するためです。

[このエラーメッセージは、bot によって発生した ![ます。](fighting-bots-cs/_static/image2.png)](fighting-bots-cs/_static/image1.png)

このエラーメッセージは bot によって発生した可能性があります ([クリックすると、フルサイズの画像が表示](fighting-bots-cs/_static/image3.png)されます)

> [!div class="step-by-step"]
> [Next](fighting-bots-vb.md)
