---
uid: web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-with-an-updatepanel-vb
title: UpdatePanel を使用したポップアップコントロールからのポストバックの処理 (VB) |Microsoft Docs
author: wenz
description: AJAX Control Toolkit の PopupControl extender は、他のコントロールがアクティブになったときにポップアップをトリガーする簡単な方法を提供します。 特別な注意が必要です...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: ec9db57c-9f68-402a-bf4c-0d63d5f6908e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-with-an-updatepanel-vb
msc.type: authoredcontent
ms.openlocfilehash: dd045ae56696c7944df98cf805ba812fde1bb4ff
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74598817"
---
# <a name="handling-postbacks-from-a-popup-control-with-an-updatepanel-vb"></a>ポップアップ コントロールからポストバックを処理する (UpdatePanel あり) (VB)

[Christian Wenz](https://github.com/wenz)別

[コードのダウンロード](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl2.vb.zip)または[PDF のダウンロード](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol2VB.pdf)

> AJAX Control Toolkit の PopupControl extender は、他のコントロールがアクティブになったときにポップアップをトリガーする簡単な方法を提供します。 このようなポップアップ内でポストバックが発生した場合は、特別な注意が必要です。

## <a name="overview"></a>の概要

AJAX Control Toolkit の PopupControl extender は、他のコントロールがアクティブになったときにポップアップをトリガーする簡単な方法を提供します。 このようなポップアップ内でポストバックが発生した場合は、特別な注意が必要です。

## <a name="steps"></a>手順

ポストバックで `PopupControl` を使用すると、ポストバックによるページの更新が `UpdatePanel` によって妨げられる可能性があります。 次のマークアップは、いくつかの重要な要素を定義します。

- ASP.NET AJAX Control Toolkit が動作するように `ScriptManager` コントロール
- ポップアップをトリガーする2つの `TextBox` コントロール
- ポップアップとして機能する `Panel` コントロール
- パネル内では、`Calendar` コントロールが `UpdatePanel` コントロール内に埋め込まれます。
- パネルをテキストボックスに割り当てる2つの `PopupControlExtender` コントロール

[!code-aspx[Main](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/samples/sample1.aspx)]

`Calendar` コントロールの `OnSelectionChanged` 属性が設定されていることに注意してください。 そのため、ユーザーがカレンダー内の日付を選択すると、ポストバックが発生し、サーバー側のメソッド `c1_SelectionChanged()` が実行されます。 そのメソッド内で、現在の日付を取得し、テキストボックスに書き戻す必要があります。

の構文は次のとおりです。最初に、ページの `PopupControlExtender` のプロキシオブジェクトを生成する必要があります。 ASP.NET AJAX Control Toolkit には、`GetProxyForCurrentPopup()` メソッドが用意されています。 このメソッドが返すオブジェクトは、`Commit()` メソッドをサポートしています。このメソッドは、ポップアップをトリガーしたコントロール (メソッド呼び出しをトリガーしたコントロールではない) に値を返します。 次のコードでは、`Commit()` メソッドの引数として選択された日付を提供しています。これにより、コードは、選択した日付をテキストボックスに書き戻します。

[!code-aspx[Main](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/samples/sample2.aspx)]

これで、カレンダーの日付をクリックするたびに、選択した日付が関連するテキストボックスに表示され、多くの web サイトで現在検出できる日付の選択コントロールが作成されます。

[ユーザーがテキストボックスをクリックしたときにカレンダーが表示される ![](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image2.png)](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image1.png)

ユーザーがテキストボックスをクリックするとカレンダーが表示されます ([クリックすると、フルサイズの画像が表示](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image3.png)されます)

[日付をクリック ![と、テキストボックスに挿入されます。](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image5.png)](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image4.png)

日付をクリックするとテキストボックスに挿入されます ([クリックすると、フルサイズの画像が表示](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image6.png)されます)

> [!div class="step-by-step"]
> [前へ](using-multiple-popup-controls-vb.md)
> [次へ](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb.md)
