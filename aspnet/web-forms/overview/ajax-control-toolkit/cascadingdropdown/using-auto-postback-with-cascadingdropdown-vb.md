---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-auto-postback-with-cascadingdropdown-vb
title: CascadingDropDown で自動ポストバックを使用する (VB) |Microsoft Docs
author: wenz
description: AJAX コントロールツールキットの CascadingDropDown コントロールは、dropdownlist コントロールを拡張して、1つの DropDownList の変更によって anoth に関連付けられた値が読み込まれるようにします。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 0b34f7f6-a0cc-4b9f-9761-643fb0bb3ece
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-auto-postback-with-cascadingdropdown-vb
msc.type: authoredcontent
ms.openlocfilehash: 5dea23a20aba00af5109f05f18365b89e409a131
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74574460"
---
# <a name="using-auto-postback-with-cascadingdropdown-vb"></a>CascadingDropDown で自動ポストバックを使用する (VB)

[Christian Wenz](https://github.com/wenz)別

[コードのダウンロード](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown3.vb.zip)または[PDF のダウンロード](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown3VB.pdf)

> AJAX コントロールツールキットの CascadingDropDown コントロールは、dropdownlist コントロールを拡張して、1つの DropDownList の変更によって別の DropDownList に関連付けられた値が読み込まれるようにします。 ただし、CascadingDropDown コントロールを使用する場合は ASP を使用します。リストにデータを非同期で読み込むと (不要な) ポストバック自体が生成されるため、ネットワークの DropDownList コントロールの AutoPostBack 機能は機能しません。 一部の JavaScript コードでは、この影響を回避できます。

## <a name="overview"></a>の概要

AJAX コントロールツールキットの CascadingDropDown コントロールは、dropdownlist コントロールを拡張して、1つの DropDownList の変更によって別の DropDownList に関連付けられた値が読み込まれるようにします。 (たとえば、1つのリストに米国の州の一覧が表示され、その州の主要都市が次の一覧に入力されます)。ただし、CascadingDropDown コントロールを使用する場合は ASP を使用します。リストにデータを非同期で読み込むと (不要な) ポストバック自体が生成されるため、ネットワークの DropDownList コントロールの AutoPostBack 機能は機能しません。 一部の JavaScript コードでは、この影響を回避できます。

## <a name="steps"></a>手順

ASP.NET AJAX と Control Toolkit の機能をアクティブ化するには、ページの任意の場所に `ScriptManager` コントロールを配置する必要があります (&lt;`form`&gt; 要素内)。

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-vb/samples/sample1.aspx)]

次に、DropDownList コントロールが必要です。

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-vb/samples/sample2.aspx)]

この一覧では、web サービスの URL とメソッドの情報を提供する CascadingDropDown extender が追加されます。

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-vb/samples/sample3.aspx)]

次に、CascadingDropDown extender は、次のメソッドシグネチャを使用して web サービスを非同期に呼び出します。

[!code-vb[Main](using-auto-postback-with-cascadingdropdown-vb/samples/sample4.vb)]

このメソッドは、CascadingDropDown value 型の配列を返します。 型のコンストラクターは、最初にリストエントリのキャプションを受け取り、次に値 (HTML `value` 属性) を必要とします。

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-vb/samples/sample5.aspx)]

ブラウザーにページを読み込むと、ドロップダウンリストに3つのベンダが挿入され、2番目のベンダーが事前に選択されます。 また、ASP.NET は `__doPostBack()` JavaScript メソッドを定義します。 ページが読み込まれると、この JavaScript 呼び出しはドロップダウンリストに追加されますが、その中に要素がある場合に限ります。 リストに要素が存在しない場合、コントロールツールキットは現在それらを読み込んでいるため、JavaScript コードはタイムアウトを使用して、0.5 秒後にもう一度試行します。

[!code-html[Main](using-auto-postback-with-cascadingdropdown-vb/samples/sample6.html)]

このようにして、ポストバックは、リスト内に実際に要素が存在し、ユーザーがエントリを選択した場合にのみ実行されます。

[リスト要素を選択するとポストバックが発生する ![](using-auto-postback-with-cascadingdropdown-vb/_static/image2.png)](using-auto-postback-with-cascadingdropdown-vb/_static/image1.png)

リスト要素を選択するとポストバックが発生します ([クリックすると、フルサイズの画像が表示](using-auto-postback-with-cascadingdropdown-vb/_static/image3.png)される)

> [!div class="step-by-step"]
> [前へ](presetting-list-entries-with-cascadingdropdown-vb.md)
