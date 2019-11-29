---
uid: web-forms/overview/ajax-control-toolkit/dynamicpopulate/using-dynamicpopulate-with-a-user-control-and-javascript-vb
title: DynamicPopulate ユーザーコントロールと JavaScript を設定する (VB) |Microsoft Docs
author: wenz
description: ASP.NET AJAX Control Toolkit の DynamicPopulate コントロールは、web サービス (またはページメソッド) を呼び出し、結果の値を t... のターゲットコントロールに入力します。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 778b9009-76f2-4665-940e-afc0e35bc917
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dynamicpopulate/using-dynamicpopulate-with-a-user-control-and-javascript-vb
msc.type: authoredcontent
ms.openlocfilehash: ee5923ad6d8b101f689a0564aef8b1e0e00a7639
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599146"
---
# <a name="using-dynamicpopulate-with-a-user-control-and-javascript-vb"></a>ユーザー コントロールと JavaScript で DynamicPopulate を使用する (VB)

[Christian Wenz](https://github.com/wenz)別

[コードのダウンロード](https://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate2.vb.zip)または[PDF のダウンロード](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate2VB.pdf)

> ASP.NET AJAX Control Toolkit の DynamicPopulate コントロールは、web サービス (またはページメソッド) を呼び出し、結果の値をページのターゲットコントロールに入力します。ページの更新は行われません。 また、カスタムクライアント側の JavaScript コードを使用して、作成をトリガーすることもできます。 ただし、extender がユーザーコントロールに存在する場合は、特別な注意が必要です。

## <a name="overview"></a>の概要

ASP.NET AJAX Control Toolkit の `DynamicPopulate` コントロールは、web サービス (またはページメソッド) を呼び出し、結果の値をページのターゲットコントロールに入力します。ページの更新は行われません。 また、カスタムクライアント側の JavaScript コードを使用して、作成をトリガーすることもできます。 ただし、extender がユーザーコントロールに存在する場合は、特別な注意が必要です。

## <a name="steps"></a>手順

まず、`DynamicPopulateExtender` コントロールによって呼び出されるメソッドを実装する ASP.NET Web サービスが必要です。 この web サービスは、`contextKey`と呼ばれる文字列型の引数を1つ必要とするメソッド `getDate()` を実装しています。これは、`DynamicPopulate` コントロールが各 web サービス呼び出しに1つのコンテキスト情報を送信するためです。 次に示すコード (files `DynamicPopulate.vb.asmx`) は、次の3つの形式のいずれかで現在の日付を取得します。

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample1.aspx)]

次の手順では、新しいユーザーコントロール (`.ascx` ファイル) を作成します。最初の行には次の宣言が示されています。

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample2.aspx)]

&lt;`label`&gt; 要素を使用して、サーバーからのデータが表示されます。

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample3.aspx)]

また、ユーザーコントロールファイルでは、3つのラジオボタンを使用します。各ボタンは、web サービスでサポートされる3つの日付形式のいずれかを表します。 ユーザーがいずれかのオプションボタンをクリックすると、ブラウザーは次のような JavaScript コードを実行します。

[!code-powershell[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample4.ps1)]

このコードは、`DynamicPopulateExtender` にアクセスします (奇妙な ID について心配する必要はありません。これについては後で説明します)。動的な作成をデータでトリガーします。 現在のオプションボタンのコンテキストでは、`this.value` は `format1`、`format2` また `format3` は web メソッドが期待する内容を示します。

ユーザーコントロールにまだ存在しないのは、オプションボタンを web サービスにリンクする `DynamicPopulateExtender` コントロールです。

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample5.aspx)]

ここでも、コントロールで使用されている奇妙な ID (`myDate`ではなく `mcd1$myDate`) に注意することができます。 以前は、JavaScript コードは `dpe1`ではなく `DynamicPopulateExtender` にアクセスするために `mcd1_dpe1` 使用されていました。この名前付け方法は、ユーザーコントロール内で `DynamicPopulateExtender` を使用する場合に特別な要件となります。 さらに、すべての機能を使用するには、ユーザーコントロールを特定の方法で埋め込む必要があります。 新しい ASP.NET ページを作成し、先ほど実装したユーザーコントロールのタグプレフィックスを登録します。

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample6.aspx)]

次に、ASP.NET AJAX `ScriptManager` コントロールを新しいページに追加します。

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample7.aspx)]

最後に、ユーザーコントロールをページに追加します。 `ID` 属性を設定する必要があるだけです (もちろん `runat="server"`ます) が、これは JavaScript を使用してアクセスするためにユーザーコントロール内で使用されるプレフィックスであるため、`mcd1` を特定の名前に設定する必要があります。

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample8.aspx)]

以上です。 ページは想定どおりに動作します。ユーザーがいずれかのオプションボタンをクリックすると、ツールキットのコントロールが web サービスを呼び出し、現在の日付を目的の形式で表示します。

[オプションボタンがユーザーコントロールに存在する ![](using-dynamicpopulate-with-a-user-control-and-javascript-vb/_static/image2.png)](using-dynamicpopulate-with-a-user-control-and-javascript-vb/_static/image1.png)

オプションボタンはユーザーコントロールに存在します ([クリックすると、フルサイズの画像が表示](using-dynamicpopulate-with-a-user-control-and-javascript-vb/_static/image3.png)されます)

> [!div class="step-by-step"]
> [前へ](dynamically-populating-a-control-using-javascript-code-vb.md)
