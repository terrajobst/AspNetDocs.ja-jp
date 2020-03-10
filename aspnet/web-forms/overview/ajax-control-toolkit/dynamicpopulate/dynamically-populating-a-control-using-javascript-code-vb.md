---
uid: web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-using-javascript-code-vb
title: JavaScript コードを使用してコントロールを動的に設定する (VB) |Microsoft Docs
author: wenz
description: ASP.NET AJAX Control Toolkit の DynamicPopulate コントロールは、web サービス (またはページメソッド) を呼び出し、結果の値を t... のターゲットコントロールに入力します。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 90582e54-3e90-432a-9da5-689fb39ed56b
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-using-javascript-code-vb
msc.type: authoredcontent
ms.openlocfilehash: b2bd5b1571ccebc9baa501b29743aecdb4543fb2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78497380"
---
# <a name="dynamically-populating-a-control-using-javascript-code-vb"></a>JavaScript コードを使用してコントロールに動的に入力する (VB)

[Christian Wenz](https://github.com/wenz)別

[コードのダウンロード](https://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate1.vb.zip)または[PDF のダウンロード](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate1VB.pdf)

> ASP.NET AJAX Control Toolkit の DynamicPopulate コントロールは、web サービス (またはページメソッド) を呼び出し、結果の値をページのターゲットコントロールに入力します。ページの更新は行われません。 また、カスタムクライアント側の JavaScript コードを使用して、作成をトリガーすることもできます。

## <a name="overview"></a>概要

ASP.NET AJAX Control Toolkit の `DynamicPopulate` コントロールは、web サービス (またはページメソッド) を呼び出し、結果の値をページのターゲットコントロールに入力します。ページの更新は行われません。 また、カスタムクライアント側の JavaScript コードを使用して、作成をトリガーすることもできます。

## <a name="steps"></a>手順

まず、`DynamicPopulateExtender` コントロールによって呼び出されるメソッドを実装する ASP.NET Web サービスが必要です。 この web サービスは、`contextKey`と呼ばれる文字列型の引数を1つ必要とするメソッド `getDate()` を実装しています。これは、`DynamicPopulate` コントロールが各 web サービス呼び出しに1つのコンテキスト情報を送信するためです。 次に示すコード (ファイル `DynamicPopulate.vb.asmx`) は、次の3つの形式のいずれかで現在の日付を取得します。

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-vb/samples/sample1.aspx)]

次の手順で、新しい ASP.NET サイトを作成し、ASP.NET AJAX ScriptManager コントロールから開始します。

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-vb/samples/sample2.aspx)]

次に、label コントロールを追加します (たとえば、同じ名前の HTML コントロールまたは `<asp:Label />` web コントロールを使用する場合)。この場合、後で web サービス呼び出しの結果が表示されます。

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-vb/samples/sample3.aspx)]

次に、`DynamicPopulateExtender` コントロールを含め、web サービス情報、ターゲットコントロールを指定します。ただし、作成をトリガーするコントロールの名前は、後でカスタム JavaScript を使用して実行します。

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-vb/samples/sample4.aspx)]

ここで、JavaScript の部分にします。 `$find()` 関数は、ASP.NET AJAX ライブラリによって定義され、`DynamicPopulateExtender`などの ASP.NET AJAX Control Toolkit のサーバー側オブジェクトへの参照を返します。 現在のファイルでは、`$find("dpe")` はページ内の1つの `DynamicPopulateExtender` コントロールへの参照を返します。 動的な作成プロセスをトリガーする `populate()` と呼ばれるメソッドを公開します。 `populate()` メソッドには1つの引数が必要です。これは、`getDate()` web メソッドの引数として機能するコンテキストキーです。 たとえば、`$find("dpe").populate("format1")` では、ラベルに月-日-年形式の現在の日付が設定されます。

このサンプルを少し柔軟にするために、ユーザーは複数の日付形式を選択できるようになりました。 それぞれに対して、ラジオボタンが表示されます。 ユーザーがラジオボタンをクリックすると、JavaScript コードによって、選択した日付形式でラベルが動的に設定されます。 これらのオプションボタンは次のとおりです。

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-vb/samples/sample5.aspx)]

オプションボタンのコンテキスト内では、JavaScript 式 `this.value` が現在のボタンの値を参照することに注意してください。これは、`getDate()` メソッドが使用できる情報とまったく同じです。

[![ボタンをクリックすると、指定した形式でサーバーから日付が取得されます。](dynamically-populating-a-control-using-javascript-code-vb/_static/image2.png)](dynamically-populating-a-control-using-javascript-code-vb/_static/image1.png)

このボタンをクリックすると、指定した形式でサーバーから日付が取得されます ([クリックすると、フルサイズの画像が表示](dynamically-populating-a-control-using-javascript-code-vb/_static/image3.png)されます)。

> [!div class="step-by-step"]
> [前へ](dynamically-populating-a-control-vb.md)
> [次へ](using-dynamicpopulate-with-a-user-control-and-javascript-vb.md)
