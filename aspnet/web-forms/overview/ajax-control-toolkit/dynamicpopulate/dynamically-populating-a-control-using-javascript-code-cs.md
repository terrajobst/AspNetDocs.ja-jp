---
uid: web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-using-javascript-code-cs
title: JavaScript コードを使用してコントロールをC#動的に設定する () |Microsoft Docs
author: wenz
description: ASP.NET AJAX Control Toolkit の DynamicPopulate コントロールは、web サービス (またはページメソッド) を呼び出し、結果の値を t... のターゲットコントロールに入力します。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: cc4c2def-e88c-4456-ae8b-a6ae0ff8cc2d
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-using-javascript-code-cs
msc.type: authoredcontent
ms.openlocfilehash: 24dc358427dec3ffcba16d00041c9a2db657e7e2
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599264"
---
# <a name="dynamically-populating-a-control-using-javascript-code-c"></a>JavaScript コードを使用してコントロールに動的に入力する (C#)

[Christian Wenz](https://github.com/wenz)別

[コードのダウンロード](https://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate1.cs.zip)または[PDF のダウンロード](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate1CS.pdf)

> ASP.NET AJAX Control Toolkit の DynamicPopulate コントロールは、web サービス (またはページメソッド) を呼び出し、結果の値をページのターゲットコントロールに入力します。ページの更新は行われません。 また、カスタムクライアント側の JavaScript コードを使用して、作成をトリガーすることもできます。

## <a name="overview"></a>の概要

ASP.NET AJAX Control Toolkit の `DynamicPopulate` コントロールは、web サービス (またはページメソッド) を呼び出し、結果の値をページのターゲットコントロールに入力します。ページの更新は行われません。 また、カスタムクライアント側の JavaScript コードを使用して、作成をトリガーすることもできます。

## <a name="steps"></a>手順

まず、`DynamicPopulateExtender` コントロールによって呼び出されるメソッドを実装する ASP.NET Web サービスが必要です。 この web サービスは、`contextKey`と呼ばれる文字列型の引数を1つ必要とするメソッド `getDate()` を実装しています。これは、`DynamicPopulate` コントロールが各 web サービス呼び出しに1つのコンテキスト情報を送信するためです。 次に示すコード (ファイル `DynamicPopulate.cs.asmx`) は、次の3つの形式のいずれかで現在の日付を取得します。

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-cs/samples/sample1.aspx)]

次の手順で、新しい ASP.NET サイトを作成し、ASP.NET AJAX ScriptManager コントロールから開始します。

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-cs/samples/sample2.aspx)]

次に、label コントロールを追加します (たとえば、同じ名前の HTML コントロールまたは `<asp:Label />` web コントロールを使用する場合)。この場合、後で web サービス呼び出しの結果が表示されます。

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-cs/samples/sample3.aspx)]

次に、`DynamicPopulateExtender` コントロールを含め、web サービス情報、ターゲットコントロールを指定します。ただし、作成をトリガーするコントロールの名前は、後でカスタム JavaScript を使用して実行します。

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-cs/samples/sample4.aspx)]

ここで、JavaScript の部分にします。 `$find()` 関数は、ASP.NET AJAX ライブラリによって定義され、`DynamicPopulateExtender`などの ASP.NET AJAX Control Toolkit のサーバー側オブジェクトへの参照を返します。 現在のファイルでは、`$find("dpe")` はページ内の1つの `DynamicPopulateExtender` コントロールへの参照を返します。 動的な作成プロセスをトリガーする `populate()` と呼ばれるメソッドを公開します。 `populate()` メソッドには1つの引数が必要です。これは、`getDate()` web メソッドの引数として機能するコンテキストキーです。 たとえば、`$find("dpe").populate("format1")` では、ラベルに月-日-年形式の現在の日付が設定されます。

このサンプルを少し柔軟にするために、ユーザーは複数の日付形式を選択できるようになりました。 それぞれに対して、ラジオボタンが表示されます。 ユーザーがラジオボタンをクリックすると、JavaScript コードによって、選択した日付形式でラベルが動的に設定されます。 これらのオプションボタンは次のとおりです。

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-cs/samples/sample5.aspx)]

オプションボタンのコンテキスト内では、JavaScript 式 `this.value` が現在のボタンの値を参照することに注意してください。これは、`getDate()` メソッドが使用できる情報とまったく同じです。

[![ボタンをクリックすると、指定した形式でサーバーから日付が取得されます。](dynamically-populating-a-control-using-javascript-code-cs/_static/image2.png)](dynamically-populating-a-control-using-javascript-code-cs/_static/image1.png)

このボタンをクリックすると、指定した形式でサーバーから日付が取得されます ([クリックすると、フルサイズの画像が表示](dynamically-populating-a-control-using-javascript-code-cs/_static/image3.png)されます)。

> [!div class="step-by-step"]
> [前へ](dynamically-populating-a-control-cs.md)
> [次へ](using-dynamicpopulate-with-a-user-control-and-javascript-cs.md)
