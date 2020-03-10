---
uid: web-forms/overview/ajax-control-toolkit/colorpicker/using-the-colorpicker-control-extender-cs
title: ColorPicker コントロールエクステンダー (C#) を使用するMicrosoft Docs
author: microsoft
description: ColorPicker は ASP.NET AJAX extender で、クライアント側のカラー選択機能を UI と共にポップアップコントロールに提供します。 任意の ASP.NET にアタッチできます...
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 0d86a1e7-a910-4ab2-b85c-7a9ea6906c39
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/colorpicker/using-the-colorpicker-control-extender-cs
msc.type: authoredcontent
ms.openlocfilehash: ac510ab353878038c1c7a103bfbf6d32fb1b2686
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78497620"
---
# <a name="using-the-colorpicker-control-extender-c"></a>ColorPicker コントロールエクステンダー (C#) の使用

[Microsoft](https://github.com/microsoft)

> ColorPicker は ASP.NET AJAX extender で、クライアント側のカラー選択機能を UI と共にポップアップコントロールに提供します。 任意の ASP.NET TextBox コントロールにアタッチできます。 し.

このチュートリアルの目的は、AJAX Control Toolkit ColorPicker コントロールエクステンダーの使用方法について説明することです。 ColorPicker コントロールエクステンダーには、色を選択できるポップアップダイアログが表示されます。 ColorPicker は、ユーザーが色を選択するための直感的なユーザーインターフェイスを提供する場合に便利です。

## <a name="extending-a-textbox-control-with-the-colorpicker-control-extender"></a>ColorPicker コントロールエクステンダーを使用した TextBox コントロールの拡張

たとえば、訪問者がカスタマイズした名刺を作成できるようにする web サイトを作成する場合を考えてみましょう。 訪問者は、名刺のテキストを入力し、色を選択できます。 リスト1の ASP.NET ページには、txtCardText および Txtcardtext という名前の2つのテキストボックスコントロールが含まれています。 フォームを送信すると、選択した値が表示されます (図1を参照)。

[名刺を作成するためのシンプルなフォーム ![](using-the-colorpicker-control-extender-cs/_static/image1.jpg)](using-the-colorpicker-control-extender-cs/_static/image1.png)

**図 01**: 名刺を作成するための単純なフォーム ([クリックすると、フルサイズの画像が表示](using-the-colorpicker-control-extender-cs/_static/image2.png)される)

**リスト 1-CreateCard**

[!code-aspx[Main](using-the-colorpicker-control-extender-cs/samples/sample1.aspx)]

リスト1のフォームは機能しますが、優れたユーザーエクスペリエンスは提供されません。 ユーザーは、テキストボックスに色を入力する必要があります。 ユーザーが特殊な色を必要とする場合 (たとえば、.pea が緑である場合など)、ユーザーはヘルプを表示せずに HTML カラーコードを確認する必要があります。

ColorPicker コントロールエクステンダーを使用すると、より優れたユーザーエクスペリエンスを作成できます。 ColorPicker は、テキストボックスコントロールにフォーカスを移動すると、色のダイアログボックスを表示します (図2を参照)。

[ColorPicker コントロールエクステンダーの ![](using-the-colorpicker-control-extender-cs/_static/image2.jpg)](using-the-colorpicker-control-extender-cs/_static/image3.png)

**図 02**: Colorpicker コントロールエクステンダー ([クリックすると、フルサイズの画像が表示](using-the-colorpicker-control-extender-cs/_static/image4.png)されます)

次の2つの手順を実行して、リスト1のフォームと共に ColorPicker コントロールエクステンダーを使用する必要があります。

1. ScriptManager コントロールをページに追加する
2. ColorPicker コントロールエクステンダーをページに追加します。

ColorPicker を使用する前に、ScriptManager をページに追加する必要があります。 ScriptManager を追加するには、サーバー側の &lt;フォーム&gt; タグのすぐ下に配置することをお勧めします。 ScriptManager コントロールは、ツールボックスからページにドラッグできます (ScriptManager は [AJAX 拡張] タブの下にあります)。 または、[サーバー側フォームの開始] タグの下に、ソースビューに次のタグを入力します。

&lt;asp: ScriptManager ID = "ScriptManager1" runat = "server"/&gt;

ページに ColorPicker コントロールエクステンダーを追加する最も簡単な方法は、デザインビューです。 [TxtCardColor] ボックスの上にマウスポインターを置くと、スマートタスクオプションが表示され、extender を追加できます (図3を参照)。 このオプションを選択すると、拡張ウィザードが表示されます (図4を参照)。

[extender の追加 ![](using-the-colorpicker-control-extender-cs/_static/image3.jpg)](using-the-colorpicker-control-extender-cs/_static/image5.png)

**図 03**: エクステンダーを追加[する (クリックすると、フルサイズの画像が表示](using-the-colorpicker-control-extender-cs/_static/image6.png)されます)

[エクステンダーウィザードを使用してコントロールエクステンダーを選択 ![には](using-the-colorpicker-control-extender-cs/_static/image4.jpg)](using-the-colorpicker-control-extender-cs/_static/image7.png)

**図 04**: エクステンダーウィザードを使用してコントロールエクステンダーを選択[する (クリックすると、フルサイズの画像が表示](using-the-colorpicker-control-extender-cs/_static/image8.png)されます)

ColorPicker エクステンダーを選択すると、ColorPicker extender を使用して txtCardColor テキストボックスを拡張できます。 [OK] をクリックしてダイアログ ボックスを閉じます。

これらの変更を行った後、ページのソースはリスト2のようになります。

リスト 2-CreateCard (ColorPicker 付き)

[!code-aspx[Main](using-the-colorpicker-control-extender-cs/samples/sample2.aspx)]

ページに、txtCardColor TextBox コントロールのすぐ下に表示される ColorPickerExtender コントロールが含まれていることに注意してください。 ColorPickerExtender コントロールは、txtCardColor コントロールを拡張して、カラーピッカーダイアログを表示します。

## <a name="using-a-button-to-launch-the-color-picker-dialog"></a>ボタンを使用してカラーピッカーダイアログを起動する

ColorPicker エクステンダーでは、次のプロパティがサポートされています。

- PopupButtonId-[カラーピッカー] ダイアログボックスが表示されるページ上のボタンの ID。
- PopupPosition-カラーピッカーダイアログのターゲットコントロールを基準とした相対的な位置。 指定できる値は、Absolute、Center、左下、右下、TopLeft、右、Right、Left (既定値は左下) です。
- SampleControlId-選択された色を表示するコントロールの ID。
- SelectedColor-ColorPicker によって選択された初期色。

これらのプロパティを使用して、[色の選択] ダイアログの表示方法と、選択した色の表示方法をカスタマイズできます。 リスト3のページは、これらのプロパティのいくつかを使用する方法を示しています。

**リスト 3-Createcシャード .aspx**

[!code-aspx[Main](using-the-colorpicker-control-extender-cs/samples/sample3.aspx)]

リスト3のページには、[色の選択] ボタンがあります (図5を参照)。 このボタンをクリックすると、[カラーピッカー] ダイアログがテキストボックスの上に表示されます。 ダイアログから色を選択すると、選択した色が lblSample Label コントロールの背景色として表示されます。

ColorPicker PopupButtonID プロパティは、[色の選択] ボタンを ColorPicker エクステンダーに関連付けるために使用されます。 PopupButtonID プロパティの値を指定すると、対象のコントロールにフォーカスがあるときに [カラーピッカー] ダイアログボックスが表示されなくなります。 ダイアログを表示するには、このボタンをクリックする必要があります。

SampleControlID プロパティは、選択した色を表示するコントロールを ColorPicker に関連付けるために使用されます。 ColorPicker は、このコントロールの背景色を現在選択されている色に変更します。

[ボタンを使用してカラーピッカーダイアログを表示 ![には](using-the-colorpicker-control-extender-cs/_static/image5.jpg)](using-the-colorpicker-control-extender-cs/_static/image9.png)

**図 05**: ボタンを使用してカラーピッカーダイアログを表示[する (クリックすると、フルサイズの画像が表示](using-the-colorpicker-control-extender-cs/_static/image10.png)されます)

## <a name="summary"></a>まとめ

このチュートリアルでは、ColorPicker コントロールエクステンダーを使用してポップアップカラーピッカーダイアログを表示する方法について学習しました。 まず、フォーカスが TextBox コントロールに移動したときにダイアログを表示する方法について説明しました。 次に、ボタンがクリックされたときに [カラーピッカー] ダイアログボックスを表示するボタンを作成する方法を学習しました。

> [!div class="step-by-step"]
> [Next](using-the-colorpicker-control-extender-vb.md)
