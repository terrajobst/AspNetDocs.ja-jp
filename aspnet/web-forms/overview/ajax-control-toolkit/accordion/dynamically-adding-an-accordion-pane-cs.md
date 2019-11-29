---
uid: web-forms/overview/ajax-control-toolkit/accordion/dynamically-adding-an-accordion-pane-cs
title: アコーディオンペインを動的に追加C#する () |Microsoft Docs
author: wenz
description: AJAX コントロールツールキットのアコーディオンコントロールは、複数のウィンドウを提供し、ユーザーが一度に1つずつ表示できるようにします。 通常、パネルは...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 66d88cfa-f26f-46b1-ad52-1c9e03c04a48
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/accordion/dynamically-adding-an-accordion-pane-cs
msc.type: authoredcontent
ms.openlocfilehash: 2834f56bd77c412923f4a8f382e670727f70eae4
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74607242"
---
# <a name="dynamically-adding-an-accordion-pane-c"></a>アコーディオンウィンドウを動的に追加C#する ()

[Christian Wenz](https://github.com/wenz)別

[コードのダウンロード](https://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion2.cs.zip)または[PDF のダウンロード](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion2CS.pdf)

> AJAX コントロールツールキットのアコーディオンコントロールは、複数のウィンドウを提供し、ユーザーが一度に1つずつ表示できるようにします。 通常、パネルはページ内で宣言されますが、サーバー側のコードを使用して同じ結果を得ることができます。

## <a name="overview"></a>の概要

AJAX コントロールツールキットのアコーディオンコントロールは、複数のウィンドウを提供し、ユーザーが一度に1つずつ表示できるようにします。 通常、パネルはページ内で宣言されますが、サーバー側のコードを使用して同じ結果を得ることができます。

## <a name="steps"></a>手順

アコーディオンコントロールは、すべての重要なプロパティをサーバー側のコードに公開します。 特に、`Panes` プロパティは、アコーディオンを構成するペインのコレクションへのアクセスを許可します。 すべてのウィンドウには `AccordionPane`型があります。 そのため、このようなペインを作成するのは簡単です。

[!code-csharp[Main](dynamically-adding-an-accordion-pane-cs/samples/sample1.cs)]

`AccordionPane` の `HeaderContainer` プロパティは、ペインのヘッダーセクション内の ASP.NET コントロールへのアクセスを提供します。`AccordionPane` の `ContentContainer` プロパティは、ペインのコンテンツセクションでも同じです。 これにより、ASP.NET コードで、ウィンドウにコンテンツを追加できます。

[!code-csharp[Main](dynamically-adding-an-accordion-pane-cs/samples/sample2.cs)]

最後に、ウィンドウをアコーディオンの `Panes` コレクションに追加する必要があります。

[!code-csharp[Main](dynamically-adding-an-accordion-pane-cs/samples/sample3.cs)]

次に示すのは、アコーディオンコントロールに2つのペインを追加する完全なサーバー側コードです。

[!code-aspx[Main](dynamically-adding-an-accordion-pane-cs/samples/sample4.aspx)]

見つからない要素は、ASP.NET `ScriptManager` コントロールの存在に応じて、アコーディオン自体だけです。

[!code-aspx[Main](dynamically-adding-an-accordion-pane-cs/samples/sample5.aspx)]

この例を完了するために、アコーディオンコントロールで参照される2つの CSS クラスでブラウザーのスタイル情報が提供されます。

[!code-css[Main](dynamically-adding-an-accordion-pane-cs/samples/sample6.css)]

[サーバー側のコードによって、アコーディオン内のデータが動的に追加された ![](dynamically-adding-an-accordion-pane-cs/_static/image2.png)](dynamically-adding-an-accordion-pane-cs/_static/image1.png)

アコーディオン内のデータはサーバー側のコードによって動的に追加されました ([クリックすると、フルサイズの画像が表示](dynamically-adding-an-accordion-pane-cs/_static/image3.png)されます)

> [!div class="step-by-step"]
> [前へ](databinding-to-an-accordion-cs.md)
> [次へ](databinding-to-an-accordion-vb.md)
