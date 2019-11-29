---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/filling-a-list-using-cascadingdropdown-cs
title: CascadingDropDown (C#) を使用してリストに入力するMicrosoft Docs
author: wenz
description: AJAX コントロールツールキットの CascadingDropDown コントロールは、dropdownlist コントロールを拡張して、1つの DropDownList の変更によって anoth に関連付けられた値が読み込まれるようにします。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: f949aafa-fe57-43b0-b722-f0dd33a900be
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/filling-a-list-using-cascadingdropdown-cs
msc.type: authoredcontent
ms.openlocfilehash: b5e9874fb5b6d3e55c8af5b85d12bf1ffacc116b
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74574846"
---
# <a name="filling-a-list-using-cascadingdropdown-c"></a>CascadingDropDown を使用して一覧に入力する (C#)

[Christian Wenz](https://github.com/wenz)別

[コードのダウンロード](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown0.cs.zip)または[PDF のダウンロード](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown0CS.pdf)

> AJAX コントロールツールキットの CascadingDropDown コントロールは、dropdownlist コントロールを拡張して、1つの DropDownList の変更によって別の DropDownList に関連付けられた値が読み込まれるようにします。 (たとえば、1つのリストに米国の州の一覧が表示され、その州の主要都市が次の一覧に入力されます)。最初の問題は、このコントロールを使用して、ドロップダウンリストに実際に入力することです。

## <a name="overview"></a>の概要

AJAX コントロールツールキットの CascadingDropDown コントロールは、dropdownlist コントロールを拡張して、1つの DropDownList の変更によって別の DropDownList に関連付けられた値が読み込まれるようにします。 (たとえば、1つのリストに米国の州の一覧が表示され、その州の主要都市が次の一覧に入力されます)。最初の問題は、このコントロールを使用して、ドロップダウンリストに実際に入力することです。

## <a name="steps"></a>手順

ASP.NET AJAX と Control Toolkit の機能をアクティブ化するには、ページの任意の場所に `ScriptManager` コントロールを配置する必要があります (`<form>` 要素内)。

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample1.aspx)]

次に、DropDownList コントロールが必要です。

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample2.aspx)]

この一覧では、CascadingDropDown extender が追加されます。 非同期要求が web サービスに送信され、リストに表示されるエントリの一覧が返されます。 これを機能させるには、次の CascadingDropDown 属性を設定する必要があります。

- `ServicePath`: リストエントリを提供する web サービスの URL
- `ServiceMethod`: リストエントリを配信する Web メソッド
- `TargetControlID`: ドロップダウンリストの ID
- `Category`: 呼び出されたときに web メソッドに送信されるカテゴリ情報
- `PromptText`: サーバーからリストデータを非同期的に読み込むときに表示されるテキスト

`CascadingDropDown` 要素のマークアップを次に示します。 C#と VB の唯一の違いは、関連付けられた web サービスの名前です。

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample3.aspx)]

`CascadingDropDown` エクステンダーからの JavaScript コードは、次のシグネチャを持つ web サービスメソッドを呼び出します。

[!code-csharp[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample4.cs)]

重要な点は、メソッドが `CascadingDropDownNameValue` 型の配列を返す必要があることです (ASP.NET AJAX Control Toolkit によって定義されています)。 `CascadingDropDownNameValue` コンストラクターでは、最初にリストエントリのテキストを入力し、次に HTML の場合 `<option value="VALUE">NAME</option>` と同様に値を指定する必要があります。 いくつかのサンプルデータを次に示します。

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample5.aspx)]

ブラウザーにページを読み込むと、3つの仕入先がリストに入力されます。

[リストが自動的に入力される ![](filling-a-list-using-cascadingdropdown-cs/_static/image2.png)](filling-a-list-using-cascadingdropdown-cs/_static/image1.png)

リストが自動的に入力されます ([クリックすると、フルサイズの画像が表示](filling-a-list-using-cascadingdropdown-cs/_static/image3.png)されます)

> [!div class="step-by-step"]
> [次へ](using-cascadingdropdown-with-a-database-cs.md)
