---
uid: aspnet/mvc/overview/older-versions-1/views/creating-custom-html-helpers-cs
title: カスタム HTML ヘルパーの作成C#() |Microsoft Docs
author: microsoft
description: このチュートリアルの目的は、MVC ビュー内で使用できるカスタム HTML ヘルパーを作成する方法を示すことです。 HTML ヘルパーを利用することで...
ms.author: riande
ms.date: 10/07/2008
ms.assetid: e454c67d-a86e-4119-a858-eb04bbec2dff
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-custom-html-helpers-cs
msc.type: authoredcontent
ms.openlocfilehash: 264ff9850bad397826b45649d52fbfefafc53a01
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74594524"
---
# <a name="creating-custom-html-helpers-c"></a>カスタム HTML ヘルパーの作成 (C#)

[Microsoft](https://github.com/microsoft)

[PDF のダウンロード](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_9_CS.pdf)

> このチュートリアルの目的は、MVC ビュー内で使用できるカスタム HTML ヘルパーを作成する方法を示すことです。 HTML ヘルパーを利用することで、標準の HTML ページを作成するために実行する必要がある HTML タグの面倒な入力の量を減らすことができます。

このチュートリアルの目的は、MVC ビュー内で使用できるカスタム HTML ヘルパーを作成する方法を示すことです。 HTML ヘルパーを利用することで、標準の HTML ページを作成するために実行する必要がある HTML タグの面倒な入力の量を減らすことができます。

このチュートリアルの最初の部分では、ASP.NET MVC フレームワークに含まれる既存の HTML ヘルパーのいくつかについて説明します。 次に、カスタム HTML ヘルパーを作成する2つの方法について説明します。ここでは、静的メソッドを作成し、拡張メソッドを作成することによってカスタム HTML ヘルパーを作成する方法について説明します。

## <a name="understanding-html-helpers"></a>HTML ヘルパーについて

HTML ヘルパーは、文字列を返すメソッドにすぎません。 文字列は、必要な任意の種類のコンテンツを表すことができます。 たとえば、html ヘルパーを使用して、HTML `<input>` や `<img>` タグなどの標準の HTML タグを表示できます。 また、HTML ヘルパーを使用して、タブストリップやデータベースデータの HTML テーブルなど、より複雑なコンテンツを表示することもできます。

ASP.NET MVC フレームワークには、次の一連の標準 HTML ヘルパーが含まれています (これは完全な一覧ではありません)。

- Html.actionlink ()
- Html. BeginForm ()
- Html. CheckBox ()
- Html. DropDownList ()
- Html. EndForm ()
- Html. Hidden ()
- Html. ListBox ()
- Html. Password ()
- Html. RadioButton ()
- Html. TextArea ()
- Html. TextBox ()

たとえば、リスト1のフォームについて考えてみます。 このフォームは、標準の HTML ヘルパーの2つのヘルプを使用してレンダリングされます (図1を参照)。 このフォームでは、`Html.BeginForm()` と `Html.TextBox()` のヘルパーメソッドを使用して、単純な HTML フォームをレンダリングします。

[HTML ヘルパーで表示される ![ページ](creating-custom-html-helpers-cs/_static/image2.png)](creating-custom-html-helpers-cs/_static/image1.png)

**図 01**: HTML ヘルパーでレンダリングされるページ ([クリックすると、フルサイズの画像が表示](creating-custom-html-helpers-cs/_static/image3.png)されます)

**リスト1– `Views\Home\Index.aspx`**

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample1.aspx)]

Html. BeginForm () ヘルパーメソッドは、HTML `<form>` の開始タグと終了タグを作成するために使用されます。 `Html.BeginForm()` メソッドは、using ステートメント内で呼び出されることに注意してください。 Using ステートメントを使用すると、`<form>` タグが using ブロックの末尾で閉じられるようになります。

必要に応じて、using ブロックを作成するのではなく、Html の EndForm () ヘルパーメソッドを呼び出して、`<form>` タグを閉じることができます。 どちらの方法を使用しても、直感的にわかりやすい `<form>` タグを作成できます。

リスト1で HTML `<input>` タグを表示するには、`Html.TextBox()` ヘルパーメソッドを使用します。 ブラウザーで [ソースの表示] を選択すると、リスト2に HTML ソースが表示されます。 ソースに標準の HTML タグが含まれていることに注意してください。

> [!IMPORTANT]
> `Html.TextBox()`HTML ヘルパーは `<% %>` タグではなく `<%= %>` タグでレンダリングされることに注意してください。 等号を含めない場合は、ブラウザーに何も表示されません。

ASP.NET MVC フレームワークには、少数のヘルパーが含まれています。 多くの場合、カスタム HTML ヘルパーを使用して MVC フレームワークを拡張する必要があります。 このチュートリアルの残りの部分では、カスタム HTML ヘルパーを作成する2つの方法について学習します。

**リスト2– `Index.aspx Source`**

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample2.aspx)]

### <a name="creating-html-helpers-with-static-methods"></a>静的メソッドを使用した HTML ヘルパーの作成

新しい HTML ヘルパーを作成する最も簡単な方法は、文字列を返す静的メソッドを作成することです。 たとえば、HTML `<label>` タグをレンダリングする新しい HTML ヘルパーを作成する場合を考えてみます。 リスト2のクラスを使用して、`<label>` を表示できます。

**リスト2– `Helpers\LabelHelper.cs`**

[!code-csharp[Main](creating-custom-html-helpers-cs/samples/sample3.cs)]

リスト2のクラスについては特別なことはありません。 `Label()` メソッドは、単に文字列を返します。

リスト3の変更されたインデックスビューでは、`LabelHelper` を使用して HTML `<label>` タグを表示します。 ビューには、`Application1.Helpers` 名前空間をインポートする `<%@ imports %>` ディレクティブが含まれていることに注意してください。

**リスト2– `Views\Home\Index2.aspx`**

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample4.aspx)]

### <a name="creating-html-helpers-with-extension-methods"></a>拡張メソッドを使用した HTML ヘルパーの作成

ASP.NET MVC フレームワークに含まれている標準の HTML ヘルパーと同様に機能する HTML ヘルパーを作成する場合は、拡張メソッドを作成する必要があります。 拡張メソッドを使用すると、既存のクラスに新しいメソッドを追加できます。 HTML ヘルパーメソッドを作成する場合は、ビューの Html プロパティによって表される HtmlHelper クラスに新しいメソッドを追加します。

リスト3のクラスは、`Label()`という名前の `HtmlHelper` クラスに拡張メソッドを追加します。 このクラスについては、いくつかの点に注意する必要があります。 まず、クラスが静的クラスであることに注意してください。 静的クラスを使用して拡張メソッドを定義する必要があります。

次に、`Label()` メソッドの最初のパラメーターの前に `this`キーワードが付いていることに注意してください。 拡張メソッドの最初のパラメーターは、拡張メソッドが拡張するクラスを示します。

**リスト3– `Helpers\LabelExtensions.cs`**

[!code-csharp[Main](creating-custom-html-helpers-cs/samples/sample5.cs)]

拡張メソッドを作成し、アプリケーションを正常にビルドすると、クラスの他のすべてのメソッドと同様に、Visual Studio の Intellisense に拡張メソッドが表示されます (図2を参照)。 唯一の違いは、拡張メソッドには、その横に特殊記号 (下向きの矢印のアイコン) が表示される点です。

[Html. Label () 拡張メソッドを使用して ![](creating-custom-html-helpers-cs/_static/image5.png)](creating-custom-html-helpers-cs/_static/image4.png)

**図 02**: Html. Label () 拡張メソッドの使用 ([クリックしてフルサイズのイメージを表示する](creating-custom-html-helpers-cs/_static/image6.png))

リスト4の変更されたインデックスビューでは、Html. Label () 拡張メソッドを使用して、すべての `<label>` タグをレンダリングします。

**リスト4– `Views\Home\Index3.aspx`**

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample6.aspx)]

## <a name="summary"></a>要約

このチュートリアルでは、カスタム HTML ヘルパーを作成する2つの方法を学習しました。 まず、文字列を返す静的メソッドを作成して、カスタム `Label()` HTML ヘルパーを作成する方法について学習しました。 次に、`HtmlHelper` クラスに拡張メソッドを作成して、カスタム `Label()` HTML ヘルパーメソッドを作成する方法について学習しました。

このチュートリアルでは、非常に単純な HTML ヘルパーメソッドを構築することに重点を置いています。 HTML ヘルパーは必要に応じて複雑になる可能性があることに注意してください。 ツリービュー、メニュー、データベースデータのテーブルなどのリッチコンテンツを表示する HTML ヘルパーを構築できます。

> [!div class="step-by-step"]
> [前へ](asp-net-mvc-views-overview-cs.md)
> [次へ](using-the-tagbuilder-class-to-build-html-helpers-cs.md)
