---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/handling-postbacks-from-a-modalpopup-cs
title: ModalPopup からポストバックを処理C#する () |Microsoft Docs
author: wenz
description: AJAX コントロールツールキットの ModalPopup コントロールを使用すると、クライアント側の方法を使用してモーダルポップアップを簡単に作成できます。 Pos を使用する場合は、特別な注意が必要です。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 7963890b-4ea3-4a1c-b65d-6098a3d56f62
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/handling-postbacks-from-a-modalpopup-cs
msc.type: authoredcontent
ms.openlocfilehash: 20073d156b4bd5ce67a47d2511b28594b70ce260
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78446206"
---
# <a name="handling-postbacks-from-a-modalpopup-c"></a>ModalPopup からポストバックを処理する (C#)

[Christian Wenz](https://github.com/wenz)別

[コードのダウンロード](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup3.cs.zip)または[PDF のダウンロード](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup3CS.pdf)

> AJAX コントロールツールキットの ModalPopup コントロールを使用すると、クライアント側の方法を使用してモーダルポップアップを簡単に作成できます。 ポップアップ内からポストバックを作成する場合は、特別な注意が必要です。

## <a name="overview"></a>概要

AJAX コントロールツールキットの ModalPopup コントロールを使用すると、クライアント側の方法を使用してモーダルポップアップを簡単に作成できます。 ポップアップ内からポストバックを作成する場合は、特別な注意が必要です。

## <a name="steps"></a>手順

ASP.NET AJAX と Control Toolkit の機能をアクティブ化するには、ページの任意の場所に `ScriptManager` コントロールを配置する必要があります (`<form>` 要素内)。

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-cs/samples/sample1.aspx)]

次に、モーダルポップアップとして機能するパネルを追加します。 ここで、ユーザーは名前と電子メールアドレスを入力できます。 ボタンを使用してポップアップを閉じ、情報を保存します。 このボタンがクリックされたときにポストバックが発生するように、`OnClick` 属性が設定されていることに注意してください。

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-cs/samples/sample2.aspx)]

ページ自体は、名前と電子メールアドレスというまったく同じ情報の2つのラベルで構成されます。 モーダルポップアップをトリガーするには、ボタンを使用します。

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-cs/samples/sample3.aspx)]

ポップアップが表示されるようにするには、`ModalPopupExtender` コントロールを追加します。 `PopupControlID` 属性をパネルの ID に設定し、ボタンの ID に `TargetControlID` します。

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-cs/samples/sample4.aspx)]

モーダルポップアップ内の [`Save`] ボタンがクリックされるたびに、サーバー側の `SaveData()` メソッドが実行されます。 ここでは、入力したデータをデータストアに保存できます。 わかりやすくするために、新しいデータは次のようにラベルに出力されます。

[!code-csharp[Main](handling-postbacks-from-a-modalpopup-cs/samples/sample5.cs)]

また、モーダルポップアップ内のテキストボックスコントロールに、現在の名前と電子メールアドレスが入力されている必要があります。 ただし、これはポストバックが発生しない場合にのみ必要です。 ポストバックがある場合は、ASP.NET viewstate 機能によって、テキストボックスに適切な値が自動的に入力されます。

[!code-csharp[Main](handling-postbacks-from-a-modalpopup-cs/samples/sample6.cs)]

[モーダルポップアップによってポストバックが発生 ![](handling-postbacks-from-a-modalpopup-cs/_static/image2.png)](handling-postbacks-from-a-modalpopup-cs/_static/image1.png)

モーダルポップアップによってポストバックが発生します ([クリックすると、フルサイズのイメージが表示](handling-postbacks-from-a-modalpopup-cs/_static/image3.png)されます)

> [!div class="step-by-step"]
> [前へ](using-modalpopup-with-a-repeater-control-cs.md)
> [次へ](positioning-a-modalpopup-cs.md)
