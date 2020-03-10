---
uid: web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-vb
title: コントロールに動的に入力する (VB) |Microsoft Docs
author: wenz
description: ASP.NET AJAX Control Toolkit の DynamicPopulate コントロールは、web サービス (またはページメソッド) を呼び出し、結果の値を t... のターゲットコントロールに入力します。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 27305347-7b5d-4519-97b7-197a357e7f6e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-vb
msc.type: authoredcontent
ms.openlocfilehash: d11320f1f89bb69afe5f62751574079716124da0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78430456"
---
# <a name="dynamically-populating-a-control-vb"></a>コントロールに動的に入力する (VB)

[Christian Wenz](https://github.com/wenz)別

[コードのダウンロード](https://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate0.vb.zip)または[PDF のダウンロード](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate0VB.pdf)

> ASP.NET AJAX Control Toolkit の DynamicPopulate コントロールは、web サービス (またはページメソッド) を呼び出し、結果の値をページのターゲットコントロールに入力します。ページの更新は行われません。

## <a name="overview"></a>概要

ASP.NET AJAX Control Toolkit の `DynamicPopulate` コントロールは、web サービス (またはページメソッド) を呼び出し、結果の値をページのターゲットコントロールに入力します。ページの更新は行われません。 このチュートリアルでは、これを設定する方法について説明します。

## <a name="steps"></a>手順

まず、`DynamicPopulate`によって呼び出されるメソッドを実装する ASP.NET Web サービスが必要です。 Web サービスクラスには、`Microsoft.Web.Script.Services`内で定義されている `ScriptService` 属性が必要です。それ以外の場合、ASP.NET AJAX では、web サービスのクライアント側の JavaScript プロキシを作成することはできません。これは `DynamicPopulate`によって要求されます。

Web メソッドは、`contextKey`と呼ばれる文字列型の1つの引数を想定する必要があります。これは、`DynamicPopulate` コントロールが各 web サービス呼び出しに1つのコンテキスト情報を送信するためです。 次の web サービスは、`contextKey` 引数によって表される形式で現在の日付を返します。

[!code-aspx[Main](dynamically-populating-a-control-vb/samples/sample1.aspx)]

その後、web サービスが `DynamicPopulate.vb.asmx`として保存されます。 また、`DynamicPopulate` コントロールを使用して、実際の ASP.NET ページ内のページメソッドとして `getDate()` メソッドを実装することもできます。

次の手順で、新しい ASP.NET ファイルを作成します。 常に、最初の手順として、現在のページに `ScriptManager` を含めて、ASP.NET AJAX ライブラリを読み込み、コントロールツールキットを機能させることができます。

[!code-aspx[Main](dynamically-populating-a-control-vb/samples/sample2.aspx)]

次に、label コントロール (同じ名前の HTML コントロールを使用する場合は、web サービス呼び出しの結果を後で表示する場合は &lt;`asp:Label` /&gt; web コントロール) を追加します。

[!code-aspx[Main](dynamically-populating-a-control-vb/samples/sample3.aspx)]

Html ボタン (サーバーへのポストバックを必要としないため、HTML コントロール) は、動的な作成をトリガーするために使用されます。

[!code-aspx[Main](dynamically-populating-a-control-vb/samples/sample4.aspx)]

最後に、`DynamicPopulateExtender` 制御が必要です。 次の属性が設定されます (明らかな属性とは別に、`ID` と `runat`=`"server"`)。

- web サービス呼び出しの結果を格納する場所を `TargetControlID` します。
- web サービスへの `ServicePath` パス (page メソッドを使用する場合は省略)
- web メソッドまたはページメソッドの `ServiceMethod` 名
- web サービスに送信される `ContextKey` コンテキスト情報
- web サービス呼び出しをトリガーする `PopulateTriggerControlID` 要素
- web サービス呼び出し中に対象の要素を空にするかどうかを `ClearContentsDuringUpdate` します。

ご覧のように、コントロールにはいくつかの情報が必要ですが、すべてを配置するのは非常に簡単です。 現在のシナリオでの `DynamicPopulateExtender` コントロールのマークアップを次に示します。

[!code-aspx[Main](dynamically-populating-a-control-vb/samples/sample5.aspx)]

ブラウザーで ASP.NET ページを実行し、ボタンをクリックします。現在の日付が月-日-年形式で表示されます。

[![ボタンをクリックすると、サーバーから日付が取得されます。](dynamically-populating-a-control-vb/_static/image2.png)](dynamically-populating-a-control-vb/_static/image1.png)

このボタンをクリックすると、サーバーから日付が取得されます ([クリックすると、フルサイズの画像が表示](dynamically-populating-a-control-vb/_static/image3.png)されます)

> [!div class="step-by-step"]
> [前へ](using-dynamicpopulate-with-a-user-control-and-javascript-cs.md)
> [次へ](dynamically-populating-a-control-using-javascript-code-vb.md)
