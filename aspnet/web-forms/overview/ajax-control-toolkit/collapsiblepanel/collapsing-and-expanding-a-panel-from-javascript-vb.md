---
uid: web-forms/overview/ajax-control-toolkit/collapsiblepanel/collapsing-and-expanding-a-panel-from-javascript-vb
title: JavaScript からパネルを折りたたむ/展開する (VB) |Microsoft Docs
author: wenz
description: ASP.NET AJAX Control Toolkit の CollapsiblePanel コントロールは、パネルを拡張し、その内容を折りたたんで展開する機能を提供します...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 298789b4-2964-49f5-a0a8-d4dbeb9ff2c2
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/collapsiblepanel/collapsing-and-expanding-a-panel-from-javascript-vb
msc.type: authoredcontent
ms.openlocfilehash: aa9779c65fb587193dbabde55cc6900283ce239d
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599358"
---
# <a name="collapsing-and-expanding-a-panel-from-javascript-vb"></a>JavaScript からパネルを折りたたむ/展開する (VB)

[Christian Wenz](https://github.com/wenz)別

[コードのダウンロード](https://download.microsoft.com/download/8/a/a/8aab3c3e-de6f-463f-805c-5fda567eef6e/CollapsiblePanel1.vb.zip)または[PDF のダウンロード](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/collapsiblepanel1VB.pdf)

> ASP.NET AJAX Control Toolkit の CollapsiblePanel コントロールは、パネルを拡張し、その内容を折りたたんでもう一度拡張する機能を提供します。 これらの2つのアクションは、カスタム JavaScript コードからトリガーすることもできます。

## <a name="overview"></a>の概要

ASP.NET AJAX Control Toolkit の CollapsiblePanel コントロールは、パネルを拡張し、その内容を折りたたんでもう一度拡張する機能を提供します。 これらの2つのアクションは、カスタム JavaScript コードからトリガーすることもできます。

## <a name="steps"></a>手順

まず、新しい ASP.NET ページを作成し、1つの `<form>` 要素内に `ScriptManager` を含めます。 これにより、Control Toolkit で必要とされる ASP.NET AJAX ライブラリが読み込まれます。

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample1.aspx)]

次に、いくつかのテキストを含むパネルを作成して、折りたたみ/展開の効果を確認できるようにします。

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample2.aspx)]

ご覧のとおり、パネルはここに表示されている CSS クラスを参照しています (基本的に、背景色とパネルの幅を定義しています)。

[!code-css[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample3.css)]

`CollapsiblePanelExtender` コントロールには、要求に応じて縮小または展開するパネルをツールキットが認識できるように、`TargetControlID` 属性が必要です。

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample4.aspx)]

残念ながら、現在のところ、extender は、パネルを折りたたんだり展開したりするための特定の API を公開していませんが、いくつかのドキュメントに記載されていないメソッドは、 まず、3つの HTML ボタンをページに追加します。これにより、クライアント側の JavaScript がトリガーされ、パネルの内容が折りたたまれたり、展開されたりします。

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample5.aspx)]

クライアント側の JavaScript コード (`<script type="text/javascript">`で開始) では、`$find()` メソッドを使用して `CollapsiblePanelExtender`にアクセスする必要があります。 `$find("cpe")` はその参照を返します。 そこから、特定のメソッドによってタスクが手動で解決されます。

パネルを開く (展開する) メソッドは `_doOpen()`と呼ばれます。次のコードは、最初のボタンがクリックされたときに呼び出される `doOpen()` 関数を実装しています。

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample6.js)]

パネルを閉じる、または折りたたむには、`_doClose()` メソッドを実行する必要があります。 そのため、ユーザーが2番目のボタンをクリックすると、次の JavaScript コードが呼び出されます。

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample7.js)]

3番目のボタンは、パネルの状態を切り替えます。つまり、折りたたまれてから展開されます。逆の場合も同様です。 `CollapsiblePanelExtender` は、パネルの状態を元に戻す `toggle()` メソッドを公開します。 ただし、別の方法もあります (`toggle()` メソッドによって内部で使用されます)。 `CollapsiblePanelExtender()` の `get_Collapsed()` メソッドによって、パネルが折りたたまれているかどうかがわかります。 この関数の戻り値に応じて、パネルは展開された (`_doOpen()` メソッド) か、折りたたまれた (`_doClose()`) メソッドになります。

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample8.js)]

[3番目のボタン ![、パネルの状態を変更します。折りたたまれてから展開された状態に戻ります。](collapsing-and-expanding-a-panel-from-javascript-vb/_static/image2.png)](collapsing-and-expanding-a-panel-from-javascript-vb/_static/image1.png)

3番目のボタンは、パネルの状態を変更します。折りたたまれてから展開されてから元に戻ります ([クリックすると、フルサイズの画像が表示](collapsing-and-expanding-a-panel-from-javascript-vb/_static/image3.png)されます)。

> [!div class="step-by-step"]
> [前へ](collapsing-and-expanding-a-panel-from-javascript-cs.md)
