---
uid: web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-without-an-updatepanel-cs
title: UpdatePanel を使用せずに Popup コントロールからポストC#バックを処理する () |Microsoft Docs
author: wenz
description: AJAX Control Toolkit の PopupControl extender は、他のコントロールがアクティブになったときにポップアップをトリガーする簡単な方法を提供します。 Su でポストバックが発生したとき...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 25444121-5a72-4dac-8e50-ad2b7ac667af
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-without-an-updatepanel-cs
msc.type: authoredcontent
ms.openlocfilehash: 9c4c59bb9dbd3e2ba2b3b81ecf76271f21673bce
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78496504"
---
# <a name="handling-postbacks-from-a-popup-control-without-an-updatepanel-c"></a>ポップアップ コントロールからポストバックを処理する (UpdatePanel なし) (C#)

[Christian Wenz](https://github.com/wenz)別

[コードのダウンロード](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl3.cs.zip)または[PDF のダウンロード](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol3CS.pdf)

> AJAX Control Toolkit の PopupControl extender は、他のコントロールがアクティブになったときにポップアップをトリガーする簡単な方法を提供します。 このようなパネルでポストバックが発生し、ページに複数のパネルがある場合は、どのパネルがクリックされたかを判断するのは困難です。

## <a name="overview"></a>概要

AJAX Control Toolkit の PopupControl extender は、他のコントロールがアクティブになったときにポップアップをトリガーする簡単な方法を提供します。 このようなパネルでポストバックが発生し、ページに複数のパネルがある場合は、どのパネルがクリックされたかを判断するのは困難です。

## <a name="steps"></a>手順

ポストバックで `PopupControl` を使用するときに、ページに `UpdatePanel` を設定していない場合、コントロールツールキットでは、ポストバックの原因となったポップアップをトリガーしたクライアント要素を特定する方法は提供されません。 ただし、このシナリオの回避策としては小さなトリックがあります。

まず、基本的なセットアップは次のようになります。2つのテキストボックスで同じポップアップ (予定表) がトリガーされます。 2つの `PopupControlExtenders` テキストボックスとポップアップをまとめて表示します。

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/samples/sample1.aspx)]

基本的な考え方は、ポップアップを起動したテキストボックスを保持する &lt;`form`&gt; 要素に非表示のフォームフィールドを追加することです。

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/samples/sample2.aspx)]

ページが読み込まれると、JavaScript コードによって、イベントハンドラーが両方のテキストボックスに追加されます。ユーザーがテキストボックスをクリックするたびに、その名前が隠しフォームフィールドに書き込まれます。

[!code-html[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/samples/sample3.html)]

サーバー側のコードでは、隠しフィールドの値を読み取る必要があります。 非表示のフォームフィールドは簡単に操作できるため、非表示の値を検証するホワイトリストアプローチが必要です。 正しいテキストボックスが識別されると、カレンダーの日付が書き込まれます。

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/samples/sample4.aspx)]

[ユーザーがテキストボックスをクリックしたときにカレンダーが表示される ![](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image2.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image1.png)

ユーザーがテキストボックスをクリックするとカレンダーが表示されます ([クリックすると、フルサイズの画像が表示](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image3.png)されます)

[日付をクリック ![と、テキストボックスに挿入されます。](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image5.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image4.png)

日付をクリックするとテキストボックスに挿入されます ([クリックすると、フルサイズの画像が表示](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image6.png)されます)

> [!div class="step-by-step"]
> [前へ](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs.md)
> [次へ](using-multiple-popup-controls-vb.md)
