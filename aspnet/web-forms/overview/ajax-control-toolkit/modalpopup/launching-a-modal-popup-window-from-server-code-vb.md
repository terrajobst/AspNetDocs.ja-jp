---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/launching-a-modal-popup-window-from-server-code-vb
title: サーバーコードからモーダルポップアップウィンドウを起動する (VB) |Microsoft Docs
author: wenz
description: AJAX コントロールツールキットの ModalPopup コントロールを使用すると、クライアント側の方法を使用してモーダルポップアップを簡単に作成できます。 ただし、一部のシナリオでは、
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 36ca81d7-906d-4db2-952b-add18a4ff421
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/launching-a-modal-popup-window-from-server-code-vb
msc.type: authoredcontent
ms.openlocfilehash: 1368a78d35ac6461bbc2e852e468f42eef2c0d2c
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74606598"
---
# <a name="launching-a-modal-popup-window-from-server-code-vb"></a>サーバー コードからモーダル ポップアップ ウィンドウを起動する (VB)

[Christian Wenz](https://github.com/wenz)別

[コードのダウンロード](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup1.vb.zip)または[PDF のダウンロード](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup1VB.pdf)

> AJAX コントロールツールキットの ModalPopup コントロールを使用すると、クライアント側の方法を使用してモーダルポップアップを簡単に作成できます。 ただし、一部のシナリオでは、モーダルポップアップを開くことがサーバー側でトリガーされる必要があります。

## <a name="overview"></a>の概要

AJAX コントロールツールキットの ModalPopup コントロールを使用すると、クライアント側の方法を使用してモーダルポップアップを簡単に作成できます。 ただし、一部のシナリオでは、モーダルポップアップを開くことがサーバー側でトリガーされる必要があります。

## <a name="steps"></a>手順

まず、ModalPopup コントロールがどのように動作するかを示すために、ASP.NET Button web コントロールが必要です。 新しいページの &lt;フォーム&gt; 要素内にこのようなボタンを追加します。

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample1.aspx)]

次に、作成するポップアップのマークアップが必要です。 `<asp:Panel>` コントロールとして定義し、ボタンコントロールが含まれていることを確認します。 ModalPopup コントロールは、このようなボタンをポップアップを閉じる機能を提供します。そうしないと、簡単に消えることができません。

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample2.aspx)]

次に、ASP.NET AJAX Toolkit から ModalPopup コントロールをページに追加します。 コントロールを読み込むボタンのプロパティ、非表示にするボタン、および実際のポップアップの ID を設定します。

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample3.aspx)]

ASP.NET AJAX に基づくすべての web ページと同様です。スクリプトマネージャーでは、さまざまなターゲットブラウザーに必要な JavaScript ライブラリを読み込む必要があります。

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample4.aspx)]

ブラウザーで例を実行します。 このボタンをクリックすると、モーダルポップアップが表示されます。 サーバー側コードを使用して同じ効果を得るために、新しいボタンが必要です。

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample5.aspx)]

ご覧のように、ボタンをクリックするとポストバックが生成され、サーバーで `ServerButton_Click()` メソッドが実行されます。 このメソッドでは、`launchModal()` という名前の JavaScript 関数が完全に実行され、ページが読み込まれると JavaScript 関数が実行されます。

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample6.aspx)]

`launchModal()` のジョブは、ModalPopup を表示することです。 `launchModal()` 関数は、HTML ページ全体が読み込まれた後に実行されます。 しかし、現時点では、ASP.NET AJAX フレームワークはまだ完全に読み込まれていません。 したがって、`launchModal()` 関数は、ModalPopup コントロールを後で表示する必要がある変数を設定するだけです。

[!code-html[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample7.html)]

`pageLoad()` JavaScript 関数は、ASP.NET AJAX が完全に読み込まれた後に実行される特別な関数です。 したがって、ModalPopup コントロールを表示するコードをこの関数に追加しますが、の前に `launchModal()` が呼び出されている場合に限ります。

[!code-javascript[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample8.js)]

`$find()` 関数は、ページ上の名前付き要素を探し、サーバー側 ID をパラメーターとして想定しています。 したがって、`$find("mpe")` は ModalPopup コントロールのクライアント表現を返します。`show()` メソッドを使用すると、ポップアップが表示されます。

[いずれかのボタンをクリックしたときにモーダルポップアップが表示さ ![](launching-a-modal-popup-window-from-server-code-vb/_static/image2.png)](launching-a-modal-popup-window-from-server-code-vb/_static/image1.png)

いずれかのボタンがクリックされると、モーダルポップアップが表示されます ([クリックすると、フルサイズの画像が表示](launching-a-modal-popup-window-from-server-code-vb/_static/image3.png)されます)

> [!div class="step-by-step"]
> [前へ](positioning-a-modalpopup-cs.md)
> [次へ](using-modalpopup-with-a-repeater-control-vb.md)
