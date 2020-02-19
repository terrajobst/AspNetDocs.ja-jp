---
uid: mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3
title: ASP.NET MVC での HTML5 と jQuery UI Datepicker ポップアップカレンダーの使用-パート 3 |Microsoft Docs
author: Rick-Anderson
description: このチュートリアルでは、ASP.NET MV... でエディターテンプレート、表示テンプレート、jQuery UI datepicker popup カレンダーを操作する方法の基本について説明します。
ms.author: riande
ms.date: 08/29/2011
ms.assetid: 8f5f91ae-12d7-4cf3-ac09-4bb53d07ee60
msc.legacyurl: /mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3
msc.type: authoredcontent
ms.openlocfilehash: b3249397e54e64538c4dc78e5fe8b94656e8962b
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457896"
---
# <a name="using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc---part-3"></a>ASP.NET MVC での HTML5 と jQuery UI Datepicker ポップアップカレンダーの使用-パート3

[Rick Anderson](https://twitter.com/RickAndMSFT)

> このチュートリアルでは、ASP.NET MVC Web アプリケーションでエディターテンプレート、表示テンプレート、jQuery UI datepicker popup カレンダーを操作する方法の基本について説明します。

## <a name="working-with-complex-types"></a>複合型の使用

このセクションでは、アドレスクラスを作成し、テンプレートを表示するためのテンプレートを作成する方法を学習します。

[*モデル*] フォルダーで、 *Person.cs*という名前の新しいクラスファイルを作成します。ここで、`Person` クラスと `Address` クラスの2つの型を指定します。 `Person` クラスには、`Address`として型指定されたプロパティが含まれます。 `Address` 型は複合型です。つまり、`int`、`string`、`double`などの組み込み型の1つではありません。 代わりに、いくつかのプロパティがあります。 新しいクラスのコードは次のようになります。

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample1.cs)]

`Movie` コントローラーで、person インスタンスを表示するには、次の `PersonDetail` アクションを追加します。

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample2.cs)]

次に、`Movie` コントローラーに次のコードを追加して、`Person` モデルにいくつかのサンプルデータを設定します。

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample3.cs)]

*Views\Movies\PersonDetail.cshtml*ファイルを開き、`PersonDetail` ビューの次のマークアップを追加します。

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample4.cshtml)]

Ctrl キーを押しながら F5 キーを押してアプリケーションを実行し、[*ムービー/個人情報*] に移動します。

このスクリーンショットに示すように、`PersonDetail` ビューには複合型 `Address` が含まれていません。 (アドレスは表示されません)。

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image1.png)

`Address` モデルデータは、複合型であるため表示されません。 アドレス情報を表示するには、 *Views\Movies\PersonDetail.cshtml*ファイルをもう一度開き、次のマークアップを追加します。

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample5.cshtml)]

`PersonDetail` ビューの完全なマークアップは次のようになります。

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample6.cshtml)]

アプリケーションをもう一度実行し、[`PersonDetail`] ビューを表示します。 アドレス情報が表示されます。

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image2.png)

### <a name="creating-a-template-for-a-complex-type"></a>複合型のテンプレートの作成

このセクションでは、`Address` 複合型をレンダリングするために使用するテンプレートを作成します。 `Address` の種類のテンプレートを作成すると、ASP.NET MVC は自動的にそのテンプレートを使用して、アプリケーション内の任意の場所でアドレスモデルの書式を設定できます。 これにより、アプリケーション内の1つの場所から `Address` 型のレンダリングを制御することができます。

*Views\Shared\DisplayTemplates*フォルダーで、厳密に型指定された**Address**という名前の部分ビューを作成します。

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image3.png)

**[追加]** をクリックし、新しい*Views\Shared\DisplayTemplates\Address.cshtml*ファイルを開きます。 新しいビューには、次の生成されたマークアップが含まれています。

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample7.cshtml)]

アプリケーションを実行し、[`PersonDetail`] ビューを表示します。 今回は、先ほど作成した `Address` テンプレートを使用して `Address` 複合型が表示されるため、表示は次のようになります。

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image4.png)

### <a name="summary-ways-to-specify-the-model-display-format-and-template"></a>まとめ: モデルの表示形式とテンプレートを指定する方法

モデルプロパティの形式またはテンプレートを指定するには、次の方法を使用します。

- モデルのプロパティに `DisplayFormat` 属性を適用します。 たとえば、次のコードでは、日付が時刻なしで表示されます。

    [!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample8.cs)]
- データ型を指定して、モデル内のプロパティに[DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)属性を適用します。 たとえば、次のコードでは、日付が時刻なしで表示されます。

    [!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample9.cs)]

    アプリケーションに*Views\Shared\DisplayTemplates*フォルダーまたは*Views\Movies\DisplayTemplates*フォルダー内に*日付の cshtml*テンプレートが含まれている場合、そのテンプレートを使用して `DateTime` プロパティが表示されます。 それ以外の場合は、組み込みの ASP.NET テンプレートシステムによって、プロパティが日付として表示されます。
- *Views\Shared\DisplayTemplates*フォルダーまたは*Views\Movies\DisplayTemplates*フォルダーで、書式設定するデータ型と一致する名前を持つ表示テンプレートを作成します。 たとえば、モデルに属性を追加したり、ビューにマークアップを追加しなくても、 *Views\Shared\DisplayTemplates\DateTime.cshtml*を使用してモデル内の `DateTime` プロパティを表示したことがわかります。
- モデルの[UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx)属性を使用して、モデルのプロパティを表示するテンプレートを指定します。
- 表示テンプレート名をビューの[Html. DisplayFor](https://msdn.microsoft.com/library/ee407420.aspx)呼び出しに明示的に追加します。

使用する方法は、アプリケーションで何を行う必要があるかによって異なります。 これらの方法を組み合わせて、必要な書式設定の種類を正確に取得することは珍しくありません。

次のセクションでは、1ビットの歯車を切り替え、データの表示方法をカスタマイズして入力方法をカスタマイズします。 JQuery datepicker をアプリケーションの編集ビューにフックして、日付を指定するための洗練された方法を提供します。

> [!div class="step-by-step"]
> [前へ](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2.md)
> [次へ](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4.md)
