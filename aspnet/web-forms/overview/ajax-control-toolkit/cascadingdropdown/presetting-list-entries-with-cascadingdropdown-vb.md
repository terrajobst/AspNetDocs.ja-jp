---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/presetting-list-entries-with-cascadingdropdown-vb
title: CascadingDropDown を使用してリストエントリを事前に事前に入力する (VB) |Microsoft Docs
author: wenz
description: AJAX コントロールツールキットの CascadingDropDown コントロールは、dropdownlist コントロールを拡張して、1つの DropDownList の変更によって anoth に関連付けられた値が読み込まれるようにします。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: ec61ced7-bbca-4bdd-aa3b-80878f295181
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/presetting-list-entries-with-cascadingdropdown-vb
msc.type: authoredcontent
ms.openlocfilehash: 58d675993777f9dcbe0ce1890a60046c91ee8907
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78483808"
---
# <a name="presetting-list-entries-with-cascadingdropdown-vb"></a>CascadingDropDown で一覧のエントリを事前設定する (VB)

[Christian Wenz](https://github.com/wenz)別

[コードのダウンロード](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown2.vb.zip)または[PDF のダウンロード](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/CascadingDropDown2VB.pdf)

> AJAX コントロールツールキットの CascadingDropDown コントロールは、dropdownlist コントロールを拡張して、1つの DropDownList の変更によって別の DropDownList に関連付けられた値が読み込まれるようにします。 少量のコードを使用すると、データが動的に読み込まれた後でリスト要素が事前選択される可能性があります。

## <a name="overview"></a>概要

AJAX コントロールツールキットの CascadingDropDown コントロールは、dropdownlist コントロールを拡張して、1つの DropDownList の変更によって別の DropDownList に関連付けられた値が読み込まれるようにします。 (たとえば、1つのリストに米国の州の一覧が表示され、その州の主要都市が次の一覧に入力されます)。少量のコードを使用すると、データが動的に読み込まれた後でリスト要素が事前選択される可能性があります。

## <a name="steps"></a>手順

ASP.NET AJAX と Control Toolkit の機能をアクティブ化するには、ページの任意の場所に `ScriptManager` コントロールを配置する必要があります (`<form>` 要素内)。

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-vb/samples/sample1.aspx)]

次に、DropDownList コントロールが必要です。

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-vb/samples/sample2.aspx)]

この一覧では、web サービスの URL とメソッドの情報を提供する CascadingDropDown extender が追加されます。

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-vb/samples/sample3.aspx)]

次に、CascadingDropDown extender は、次のメソッドシグネチャを使用して web サービスを非同期に呼び出します。

[!code-vb[Main](presetting-list-entries-with-cascadingdropdown-vb/samples/sample4.vb)]

このメソッドは、CascadingDropDown value 型の配列を返します。 型のコンストラクターは、最初にリストエントリのキャプションを受け取り、次に値 (HTML `value` 属性) を必要とします。 3番目の引数が true に設定されている場合、リスト要素はブラウザーで自動的に選択されます。

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-vb/samples/sample5.aspx)]

ブラウザーにページを読み込むと、ドロップダウンリストに3つのベンダが挿入され、2番目のベンダーが事前に選択されます。

[リストが自動的に入力されて事前選択される ![](presetting-list-entries-with-cascadingdropdown-vb/_static/image2.png)](presetting-list-entries-with-cascadingdropdown-vb/_static/image1.png)

リストが自動的に入力され、事前選択されます ([クリックすると、フルサイズの画像が表示](presetting-list-entries-with-cascadingdropdown-vb/_static/image3.png)されます)

> [!div class="step-by-step"]
> [前へ](using-cascadingdropdown-with-a-database-vb.md)
> [次へ](using-auto-postback-with-cascadingdropdown-vb.md)
