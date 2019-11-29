---
uid: web-forms/overview/ajax-control-toolkit/filteredtextbox/allowing-only-certain-characters-in-a-text-box-vb
title: テキストボックス内の特定の文字のみを許可する (VB) |Microsoft Docs
author: wenz
description: ASP.NET 検証コントロールを使用すると、ユーザー入力で特定の文字のみが許可されるようにすることができます。 ただし、これによって、ユーザーが無効な型を入力するのを防ぐことはできません...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 33af23f1-4016-4740-8fb2-37d1773452cd
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/filteredtextbox/allowing-only-certain-characters-in-a-text-box-vb
msc.type: authoredcontent
ms.openlocfilehash: 895708ebecc30c5f35e6ecd0349604bb777cbd93
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74573935"
---
# <a name="allowing-only-certain-characters-in-a-text-box-vb"></a>テキスト ボックスで特定の文字だけを許可する (VB)

[Christian Wenz](https://github.com/wenz)別

[コードのダウンロード](https://download.microsoft.com/download/4/c/2/4c2def7a-0d23-4055-91f9-1f18504167d7/FilteredTextBox0.vb.zip)または[PDF のダウンロード](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/filteredtextbox0VB.pdf)

> ASP.NET 検証コントロールを使用すると、ユーザー入力で特定の文字のみが許可されるようにすることができます。 ただし、これによって、ユーザーが無効な文字を入力したり、フォームを送信したりするのを防ぐことはできません。

## <a name="overview"></a>の概要

ASP.NET 検証コントロールを使用すると、ユーザー入力で特定の文字のみが許可されるようにすることができます。 ただし、これによって、ユーザーが無効な文字を入力したり、フォームを送信したりするのを防ぐことはできません。

## <a name="steps"></a>手順

ASP.NET AJAX Control Toolkit には、テキストボックスを拡張する `FilteredTextBox` コントロールが含まれています。 アクティブ化されると、特定の文字セットのみがフィールドに入力される可能性があります。

これを機能させるには、まず、ASP.NET AJAX Control Toolkit でも使用されている JavaScript ライブラリを読み込む ASP.NET AJAX `ScriptManager` が必要です。

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-vb/samples/sample1.aspx)]

次に、テキストボックスが必要です。

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-vb/samples/sample2.aspx)]

最後に、`FilteredTextBoxExtender` コントロールは、ユーザーが入力できる文字を制限します。 最初に、`TargetControlID` 属性を `TextBox` コントロールの `ID` に設定します。 次に、使用可能な `FilterType` の値のいずれかを選択します。

- `Custom` 既定値です。有効な文字の一覧を指定する必要があります
- 小文字のみを `LowercaseLetters`
- `Numbers` 数字のみ
- `UppercaseLetters` 大文字のみ

`Custom FilterType` を使用する場合は、`ValidChars` プロパティを設定し、入力可能な文字の一覧を指定する必要があります。 方法: テキストボックスにテキストを貼り付けようとすると、無効な文字がすべて削除されます。

数字のみを許可する `FilteredTextBoxExtender` コントロールのマークアップを次に示します (`FilterType="Numbers"`でも可能なもの)。

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-vb/samples/sample3.aspx)]

ページを実行し、JavaScript が有効になっている場合は文字を入力しようとすると機能しません。ただし、このページには数字が表示されます。 ただし、で提供される保護 `FilteredTextBox` では、"箇条書き" ではないことに注意してください。 JavaScript が有効になっている場合、テキストボックスにデータが入力される可能性があるため、追加の検証方法 (つまり、ASP) を使用する必要があります。NET の検証コントロール。

[![数字のみを入力できます](allowing-only-certain-characters-in-a-text-box-vb/_static/image2.png)](allowing-only-certain-characters-in-a-text-box-vb/_static/image1.png)

数字のみを入力できます ([クリックすると、フルサイズの画像が表示](allowing-only-certain-characters-in-a-text-box-vb/_static/image3.png)されます)

> [!div class="step-by-step"]
> [前へ](allowing-only-certain-characters-in-a-text-box-cs.md)
