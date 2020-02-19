---
uid: mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2
title: ASP.NET MVC での HTML5 と jQuery UI Datepicker ポップアップカレンダーの使用-パート 2 |Microsoft Docs
author: Rick-Anderson
description: このチュートリアルでは、ASP.NET MV... でエディターテンプレート、表示テンプレート、jQuery UI datepicker popup カレンダーを操作する方法の基本について説明します。
ms.author: riande
ms.date: 08/29/2011
ms.assetid: 21a178de-4c5a-4211-8a9c-74ec576c0f30
msc.legacyurl: /mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2
msc.type: authoredcontent
ms.openlocfilehash: 325cc90eb6e717c47863eda6253e0d48d796386b
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2020
ms.locfileid: "77455894"
---
# <a name="using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc---part-2"></a>ASP.NET MVC での HTML5 と jQuery UI Datepicker ポップアップカレンダーの使用-パート2

[Rick Anderson](https://twitter.com/RickAndMSFT)

> このチュートリアルでは、ASP.NET MVC Web アプリケーションでエディターテンプレート、表示テンプレート、jQuery UI datepicker popup カレンダーを操作する方法の基本について説明します。

## <a name="adding-an-automatic-datetime-template"></a>自動 DateTime テンプレートの追加

このチュートリアルの最初の部分では、モデルに属性を追加して書式を明示的に指定する方法と、モデルの表示に使用するテンプレートを明示的に指定する方法について説明しました。 たとえば、次のコードの[Displayformat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx)属性は、`ReleaseDate` プロパティの書式を明示的に指定します。

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample1.cs)]

次の例では、 [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)属性を使用して、`Date` 列挙型を使用して、日付テンプレートを使用してモデルを表示するように指定しています。 プロジェクトに日付テンプレートがない場合は、組み込みの日付テンプレートが使用されます。

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample2.cs)]

ただし、ASP。MVC では、型の名前と一致するテンプレートを検索することで、構成上の規則を使用して型の照合を実行できます。 これにより、属性やコードをまったく使用せずにデータを自動的に書式設定するテンプレートを作成できます。 このチュートリアルのパートでは、 [DateTime](https://msdn.microsoft.com/library/system.datetime.aspx)型のモデルプロパティに自動的に適用されるテンプレートを作成します。 属性またはその他の構成を使用して、 [DateTime](https://msdn.microsoft.com/library/system.datetime.aspx)型のすべてのモデルプロパティを表示するためにテンプレートを使用する必要はありません。

また、個々のプロパティや個々のフィールドの表示をカスタマイズする方法についても説明します。

まず、既存の書式設定情報を削除して、アプリケーションに完全な日付を表示してみましょう。

*Movie.cs*ファイルを開き、`ReleaseDate` プロパティの `DataType` 属性をコメントアウトします。

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample3.cs)]

Ctrl キーを押しながら F5 キーを押してアプリケーションを実行します。

`ReleaseDate` プロパティには、日付と時刻の両方が表示されることに注意してください。これは、書式設定情報が提供されない場合の既定値であるためです。

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image1.png)

### <a name="adding-css-styles-for-testing-new-templates"></a>新しいテンプレートをテストするための CSS スタイルの追加

日付の書式を設定するためのテンプレートを作成する前に、新しいテンプレートに適用できる CSS スタイルルールをいくつか追加します。 これらは、レンダリングされたページが新しいテンプレートを使用していることを確認するのに役立ちます。

*Content¥ siteof cs*ファイルを開き、次の CSS ルールをファイルの末尾に追加します。

[!code-css[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample4.css)]

### <a name="adding-datetime-display-templates"></a>DateTime 表示テンプレートの追加

新しいテンプレートを作成できるようになりました。 *Views\Movies*フォルダーで*displaytemplates*フォルダーを作成します。

*Views\Shared*フォルダーで、 *Displaytemplates*フォルダーと*editortemplates*フォルダーを作成します。

*Views\Shared\DisplayTemplates*フォルダー内の表示テンプレートは、すべてのコントローラーで使用されます。 *Views\Movie\DisplayTemplates*フォルダー内の表示テンプレートは、`Movie` コントローラーでのみ使用されます。 (同じ名前のテンプレートが両方のフォルダーに存在する場合、 *Views\Movie\DisplayTemplates*フォルダー内のテンプレート (つまり、より具体的なテンプレート) は、`Movie` コントローラーから返されたビューに対して優先されます)。

**ソリューションエクスプローラー**で、 *Views*フォルダーを展開し、*共有*フォルダーを展開して、 *Views\Shared\DisplayTemplates*フォルダーを右クリックします。

**[追加]** をクリックし、 **[表示]** をクリックします。 **[ビューの追加]** ダイアログボックスが表示されます。

**[ビュー名]** ボックスに「`DateTime`」と入力します。 (この名前は、型の名前と一致させるために使用する必要があります)。

**[部分ビューとして作成]** チェックボックスをオンにします。 [**レイアウトまたはマスターページを使用**し、**厳密に型指定されたビューを作成**する] チェックボックスがオフになっていることを確認します。

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image2.png)

**[追加]** をクリックします。 *Views\Shared\DisplayTemplates*に*DateTime. cshtml*テンプレートが作成されます。

次の図は、`DateTime` 表示とエディターのテンプレートが作成された後の**ソリューションエクスプローラー**の*Views*フォルダーを示しています。

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image3.png)

*Views\Shared\DisplayTemplates\DateTime.cshtml*ファイルを開き、次のマークアップを追加します。このマークアップは、 [String. format](https://msdn.microsoft.com/library/system.string.format.aspx)メソッドを使用して、プロパティを時刻なしの日付として書式設定します。 (`{0:d}` 形式では、短い日付形式を指定します)。

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample5.cs)]

この手順を繰り返して、 *Views\Movie\DisplayTemplates*フォルダーに `DateTime` テンプレートを作成します。 *Views\Movie\DisplayTemplates\DateTime.cshtml*ファイルで次のコードを使用します。

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample6.cs)]

`loud-1` CSS クラスを使用すると、日付が太字の赤いテキストで表示されます。 `loud-1` CSS クラスを一時的なメジャーとして追加したので、この特定のテンプレートがいつ使用されているかを簡単に確認できます。

完了した内容と、ASP.NET が日付を表示するために使用するカスタマイズされたテンプレートが作成されます。 より一般的なテンプレート ( *Views\Shared\DisplayTemplates*フォルダー内) には、単純な短い日付が表示されます。 `Movie` controller ( *Views\Movies\DisplayTemplates*フォルダー内) に特化したテンプレートでは、短い形式の日付が太字で太字で表示されます。

Ctrl キーを押しながら F5 キーを押してアプリケーションを実行します。 ブラウザーは、アプリケーションのインデックスビューをレンダリングします。

`ReleaseDate` プロパティには、時刻を含まない太字の赤いフォントで日付が表示されるようになりました。これにより、共有フォルダー (*Views\Shared\DisplayTemplates*) の `DateTime` テンプレート化されたヘルパー上で、 *Views\Movies\DisplayTemplates*フォルダー内の `DateTime` テンプレートヘルパーが選択されていることを確認できます。

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image4.png)

次に、 *Views\Movies\DisplayTemplates\DateTime.cshtml*ファイルの名前を*Views\Movies\DisplayTemplates\LoudDateTime.cshtml*に変更します。

Ctrl キーを押しながら F5 キーを押してアプリケーションを実行します。

今回は、[`ReleaseDate`] プロパティに、時刻のない日付と太字の赤いフォントが表示されます。 これは、データ型の名前 (この場合 `DateTime`) を持つテンプレートが、その型のすべてのモデルプロパティを表示するために自動的に使用されることを示しています。 *Datetime. cshtml*ファイルの名前を*LoudDateTime*に変更した後、ASP.NET は*Views\Movies\DisplayTemplates*フォルダー内のテンプレートを見つけられなくなりました。そのため、* Views\Movies\Shared\* フォルダーの*テンプレートを使用しまし*た。

(テンプレートの照合では大文字と小文字が区別されないため、テンプレートファイル名は大文字と小文字を区別して作成できます。 たとえば、 *datetime. cshtml, datetime.* cshtml, and *datetime*は、すべて `DateTime` 型に一致します)。

確認する: この時点では、 *Views\Movies\DisplayTemplates\DateTime.cshtml*テンプレートを使用して `ReleaseDate` フィールドが表示されます。このテンプレートでは、短い日付形式を使用してデータが表示されますが、それ以外の場合は特別な形式は追加されません。

### <a name="using-uihint-to-specify-a-display-template"></a>UIHint を使用して表示テンプレートを指定する

Web アプリケーションに多くの `DateTime` フィールドがあり、既定ではそれらのすべてまたはほとんどを日付のみの形式で表示する場合は、 *DateTime. cshtml*テンプレートを使用することをお勧めします。 しかし、完全な日付と時刻を表示する日付がいくつかある場合はどうすればよいでしょうか。 ご心配なく。 追加のテンプレートを作成し、 [UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx)属性を使用して、完全な日付と時刻の書式を指定できます。 その後、そのテンプレートを選択的に適用できます。 モデルレベルで[UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx)属性を使用することも、ビュー内でテンプレートを指定することもできます。 このセクションでは、`UIHint` 属性を使用して、日付/時刻フィールドの一部のインスタンスの書式設定を選択的に変更する方法について説明します。

*Views\Movies\DisplayTemplates\LoudDateTime.cshtml*ファイルを開き、既存のコードを次のコードに置き換えます。

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample7.cshtml)]

これにより、完全な日付と時刻が表示され、テキストを緑色と large にする CSS クラスが追加されます。

*Movie.cs*ファイルを開き、次の例に示すように、 [UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx)属性を `ReleaseDate` プロパティに追加します。

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample8.cs)]

これは、ASP.NET プロパティ (具体的には `DateTime` オブジェクトではなく) を `ReleaseDate` 表示するときに、 *LoudDateTime*テンプレートを使用する必要があることを MVC に指示します。

Ctrl キーを押しながら F5 キーを押してアプリケーションを実行します。

`ReleaseDate` プロパティに、日付と時刻が大きな緑色のフォントで表示されるようになりました。

*Movie.cs*ファイルの `UIHint` 属性に戻り、 *LoudDateTime*テンプレートが使用されないようにコメントアウトします。 アプリケーションをもう一度実行する リリース日は、大と緑で表示されません。 これにより、 *Views\Shared\DisplayTemplates\DateTime.cshtml*テンプレートがインデックスビューと詳細ビューで使用されていることが確認されます。

既に説明したように、ビューにテンプレートを適用することもできます。これにより、データの個々のインスタンスにテンプレートを適用できます。 *Views\Movies\Details.cshtml*ビューを開きます。 `ReleaseDate` フィールドの[Html. displayfor](https://msdn.microsoft.com/library/ee407420.aspx)呼び出しの2番目のパラメーターとして `"LoudDateTime"` を追加します。 完成したコードは次のようになります。

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample9.cshtml)]

これにより、モデルに適用される属性に関係なく、`LoudDateTime` テンプレートを使用してモデルのプロパティを表示する必要があることを指定します。

Ctrl キーを押しながら F5 キーを押してアプリケーションを実行します。

ムービーのインデックスページが*Views\Shared\DisplayTemplates\DateTime.cshtml*テンプレート (赤の太字) を使用しており、 *mo の詳細*ページで*Views\Movies\DisplayTemplates\LoudDateTime.cshtml*テンプレート (large と green) が使用されていることを確認します。

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image5.png)

次のセクションでは、複合型のテンプレートを作成します。

> [!div class="step-by-step"]
> [前へ](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1.md)
> [次へ](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3.md)
