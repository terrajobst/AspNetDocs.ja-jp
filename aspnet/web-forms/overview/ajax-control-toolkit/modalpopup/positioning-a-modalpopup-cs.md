---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/positioning-a-modalpopup-cs
title: ModalPopup (C#) を配置するMicrosoft Docs
author: wenz
description: AJAX コントロールツールキットの ModalPopup コントロールを使用すると、クライアント側の方法を使用してモーダルポップアップを簡単に作成できます。 ただし、コントロールは...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 1caac9d0-e21e-49d6-a8ff-e563a736d6ca
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/positioning-a-modalpopup-cs
msc.type: authoredcontent
ms.openlocfilehash: 8034f5aeb5a1a80f1ea8cbc9d638f3dfb1a38706
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599008"
---
# <a name="positioning-a-modalpopup-c"></a>ModalPopup の位置を決める (C#)

[Christian Wenz](https://github.com/wenz)別

[コードのダウンロード](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup4.cs.zip)または[PDF のダウンロード](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup4CS.pdf)

> AJAX コントロールツールキットの ModalPopup コントロールを使用すると、クライアント側の方法を使用してモーダルポップアップを簡単に作成できます。 ただし、このコントロールにはポップアップを配置するための組み込みの機能は用意されていません。

## <a name="overview"></a>の概要

AJAX コントロールツールキットの ModalPopup コントロールを使用すると、クライアント側の方法を使用してモーダルポップアップを簡単に作成できます。 ただし、このコントロールにはポップアップを配置するための組み込みの機能は用意されていません。

## <a name="steps"></a>手順

ASP.NET AJAX と Control Toolkit の機能をアクティブ化するために、`ScriptManager`ます。 コントロールは、ページの任意の場所に配置する必要があります (`<form>` 要素内)。

[!code-aspx[Main](positioning-a-modalpopup-cs/samples/sample1.aspx)]

次に、モーダルポップアップとして機能するパネルを追加します。 ポップアップを閉じるには、ボタンを使用します。

[!code-aspx[Main](positioning-a-modalpopup-cs/samples/sample2.aspx)]

ポップアップが表示されるたびに、ページ内の特定の場所に配置されます。 このタスクでは、クライアント側の JavaScript 関数が作成されます。 まず、パネルにアクセスしようとします。 成功した場合、パネルの位置は CSS と JavaScript を使用して設定されます (ポップアップの位置を変更します)。 ただし、`ModalPopupExtender` コントロールでもポップアップの配置が試行されます。 したがって、JavaScript コードでは、ポップアップが1秒ごとに繰り返し配置されます。

[!code-html[Main](positioning-a-modalpopup-cs/samples/sample3.html)]

ご覧のように、`setTimeout()` JavaScript メソッドの戻り値はグローバル変数に保存されます。 これにより、`clearTimeout()` メソッドを使用して、オンデマンドでポップアップの繰り返し位置を停止できます。

[!code-javascript[Main](positioning-a-modalpopup-cs/samples/sample4.js)]

ここでは、必要に応じて、ブラウザーがこれらの関数を呼び出すようにします。 パネルをトリガーするボタンをクリックしたときに `movePanel()` JavaScript 関数を呼び出す必要があります。

[!code-aspx[Main](positioning-a-modalpopup-cs/samples/sample5.aspx)]

また、`stopMoving()` 関数は、ポップアップが閉じられたときに再生されます。これは、`ModalPopupExtender` コントロールでトリガーできます。

[!code-aspx[Main](positioning-a-modalpopup-cs/samples/sample6.aspx)]

[指定した位置にモーダルポップアップが表示さ ![](positioning-a-modalpopup-cs/_static/image2.png)](positioning-a-modalpopup-cs/_static/image1.png)

モーダルポップアップが指定した位置に表示されます ([クリックすると、フルサイズの画像が表示](positioning-a-modalpopup-cs/_static/image3.png)されます)

> [!div class="step-by-step"]
> [前へ](handling-postbacks-from-a-modalpopup-cs.md)
> [次へ](launching-a-modal-popup-window-from-server-code-vb.md)
