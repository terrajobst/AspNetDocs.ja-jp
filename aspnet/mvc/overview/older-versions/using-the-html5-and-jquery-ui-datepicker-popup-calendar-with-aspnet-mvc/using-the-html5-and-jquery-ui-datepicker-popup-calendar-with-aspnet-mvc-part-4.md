---
uid: mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4
title: HTML5 と jQuery UI Datepicker ポップアップ カレンダーを使用して、ASP.NET MVC - パート 4 |Microsoft Docs
author: Rick-Anderson
description: このチュートリアルでは、ASP.NET MV... でエディターテンプレート、表示テンプレート、jQuery UI datepicker popup カレンダーを操作する方法の基本について説明します。
ms.author: riande
ms.date: 08/29/2011
ms.assetid: 57666c69-2b0f-423a-a61d-be49547fa585
msc.legacyurl: /mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4
msc.type: authoredcontent
ms.openlocfilehash: 583e782641efea9a9517edb31f7718b28203d756
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78433252"
---
# <a name="using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc---part-4"></a>ASP.NET MVC での HTML5 と jQuery UI Datepicker ポップアップカレンダーの使用-パート4

[Rick Anderson](https://twitter.com/RickAndMSFT)

> このチュートリアルでは、ASP.NET MVC Web アプリケーションでエディターテンプレート、表示テンプレート、jQuery UI datepicker popup カレンダーを操作する方法の基本について説明します。

### <a name="adding-a-template-for-editing-dates"></a>日付を編集するためのテンプレートの追加

このセクションでは、 [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)属性の**日付**列挙でマークされたモデルプロパティを編集するために ASP.NET MVC が UI を表示するときに適用される編集日のテンプレートを作成します。 テンプレートでは、日付のみが表示されます。時刻は表示されません。 このテンプレートでは、 [JQUERY UI Datepicker](http://jqueryui.com/demos/datepicker/)ポップアップカレンダーを使用して、日付を編集する方法を提供します。

まず、次のコードに示すように、 *Movie.cs*ファイルを開き、 **Date**列挙[型の DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx)属性を `ReleaseDate` プロパティに追加します。

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample1.cs)]

このコードを実行すると、表示テンプレートと編集テンプレートの両方に時間を指定せずに `ReleaseDate` フィールドが表示されます。 アプリケーションに*Views\Shared\EditorTemplates*フォルダーまたは*Views\Movies\EditorTemplates*フォルダーにある*日付の cshtml*テンプレートが含まれている場合は、編集中にそのテンプレートを使用して `DateTime` プロパティが表示されます。 それ以外の場合は、組み込みの ASP.NET テンプレートシステムによって、プロパティが日付として表示されます。

Ctrl キーを押しながら F5 キーを押してアプリケーションを実行します。 [編集] リンクを選択して、リリース日の入力フィールドに日付のみが表示されていることを確認します。

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image1.png)

**ソリューションエクスプローラー**で、 *Views*フォルダーを展開し、*共有*フォルダーを展開して、 *Views\Shared\EditorTemplates*フォルダーを右クリックします。

**[追加]** をクリックし、 **[表示]** をクリックします。 **[ビューの追加]** ダイアログボックスが表示されます。

**[ビュー名]** ボックスに、「&quot;Date&quot;」と入力します。

**[部分ビューとして作成]** チェックボックスをオンにします。 [**レイアウトまたはマスターページを使用**し、**厳密に型指定されたビューを作成**する] チェックボックスがオフになっていることを確認します。

**[追加]** をクリックします。 *Views\Shared\EditorTemplates\Date.cshtml*テンプレートが作成されます。

*Views\Shared\EditorTemplates\Date.cshtml*テンプレートに次のコードを追加します。

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample2.cshtml)]

最初の行では、モデルを `DateTime` 型として宣言します。 編集および表示テンプレートでモデルの型を宣言する必要はありませんが、ビューに渡されるモデルのコンパイル時チェックを行うことをお勧めします。 (もう1つの利点は、Visual Studio のビューでモデルの IntelliSense を取得することです)。モデルの型が宣言されていない場合、ASP.NET MVC はそれを[動的](https://msdn.microsoft.com/library/dd264741.aspx)な型と見なし、コンパイル時の型チェックは行われません。 モデルを `DateTime` 型として宣言すると、厳密に型指定された型になります。

2行目は、日付フィールドの前&quot; 日付テンプレートを使用して &quot;を表示するリテラル HTML マークアップにすぎません。 この行を一時的に使用して、この日付テンプレートが使用されていることを確認します。

次の行は、テキストボックスである `input` フィールドを表示する[Html テキスト](https://msdn.microsoft.com/library/system.web.mvc.html.inputextensions.textbox.aspx)ボックスヘルパーです。 ヘルパーの3番目のパラメーターは、匿名型を使用して、テキストボックスのクラスを `datefield` に、型を `date`に設定します。 (`class` はでC#予約されているので、`@` 文字を使用してC#パーサーの `class` 属性をエスケープする必要があります)。

`date` 型は html5 の入力型で、html5 対応のブラウザーは html5 カレンダーコントロールをレンダリングできます。 後で、`datefield` クラスを使用して、`Html.TextBox` 要素に jQuery datepicker をフックする JavaScript をいくつか追加します。

Ctrl キーを押しながら F5 キーを押してアプリケーションを実行します。 次の図に示すように、[編集] ビューの [`ReleaseDate`] プロパティが [編集] テンプレートを使用していることを確認できます。これは、この図に示すように、テンプレートは `ReleaseDate` テキスト入力ボックスの直前に&quot; 日付テンプレートを使用して &quot;表示されるためです。

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image2.png)

ブラウザーで、ページのソースを表示します。 (たとえば、ページを右クリックし、 **[ソースの表示]** を選択します)。次の例は、表示されている HTML の `class` と `type` 属性を示す、ページのマークアップの一部を示しています。

[!code-html[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample3.html)]

*Views\Shared\EditorTemplates\Date.cshtml*テンプレートに戻り、日付テンプレート&quot; マークアップを使用して &quot;を削除します。 完成したテンプレートは次のようになります。

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample4.cshtml)]

### <a name="adding-a-jquery-ui-datepicker-popup-calendar-using-nuget"></a>NuGet を使用した jQuery UI Datepicker ポップアップカレンダーの追加

このセクションでは、 [JQUERY UI datepicker](http://jqueryui.com/demos/datepicker/) popup カレンダーを日付編集テンプレートに追加します。 [JQUERY UI](http://jqueryui.com/)ライブラリは、アニメーション、高度な効果、およびカスタマイズ可能なウィジェットのサポートを提供します。 これは、jQuery JavaScript ライブラリ上に構築されています。 Datepicker ポップアップカレンダーを使用すると、文字列を入力する代わりに、カレンダーを使用して日付を簡単かつ自然に入力できます。 また、ポップアップカレンダーでは、ユーザーに法的な日付が制限されています。日付の通常のテキスト入力では、`2/33/1999` (1999 年2月3日) などのように入力できますが、 [JQUERY UI datepicker](http://jqueryui.com/demos/datepicker/)ポップアップカレンダーでは許可されません。

まず、jQuery UI ライブラリをインストールする必要があります。 これを行うには、Visual Studio 2010 および Visual Web Developer の SP1 バージョンに含まれているパッケージマネージャーである NuGet を使用します。

Visual Web Developer で、 **[ツール]** メニューの **[nuget パッケージマネージャー]** を選択し、 **[nuget パッケージの管理]** を選択します。

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image3.png)

注: **[ツール]** メニューに **[nuget パッケージマネージャー]** コマンドが表示されない場合は、nuget web サイトの nuget の[インストール](http://docs.nuget.org/docs/start-here/installing-nuget)に関するページの手順に従って nuget をインストールする必要があります。   
  
Visual Web Developer ではなく Visual Studio を使用している場合は、 **[ツール]** メニューの **[NuGet パッケージマネージャー]** を選択し、 **[ライブラリパッケージ参照の追加]** を選択します。

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image4.png)

**[Mvcmovie-NuGet パッケージの管理]** ダイアログボックスで、左側の **[オンライン]** タブをクリックし、検索ボックスに「&quot;jQuery&quot;」と入力します。 J **[QUERY UI ウィジェット: Datepicker]** を選択し、 **[インストール]** ボタンを選択します。

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image5.png)

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image6.png)

NuGet では、次のデバッグバージョンが追加され、jQuery UI Core と jQuery UI 日付選択のバージョンがプロジェクトに追加されます。

- *jquery. ui. node.js*
- *jquery. ui. node.js*
- *jquery. ui. datepicker*
- *datepicker... .js*

注: デバッグバージョン ( *...* . 拡張子のないファイル) はデバッグに役立ちますが、実稼働サイトでは、縮小版のみを含めることができます。

JQuery 日付の選択を実際に使用するには、カレンダーウィジェットを編集テンプレートにフックする jQuery スクリプトを作成する必要があります。 **ソリューションエクスプローラー**で、 *Scripts*フォルダーを右クリックし、 **[追加]** 、 **[新しい項目]** 、 **[JScript ファイル]** の順に選択します。 ファイルに*DatePickerReady*という名前を指定します。

*DatePickerReady*ファイルに次のコードを追加します。

[!code-javascript[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample5.js)]

JQuery に慣れていない場合は、この機能について簡単に説明します。最初の行は &quot;jQuery ready&quot; 関数です。これは、ページ内のすべての DOM 要素が読み込まれたときに呼び出されます。 2行目では、`datefield`クラス名を持つすべての DOM 要素を選択し、それぞれに対して `datepicker` 関数を呼び出します。 (前のチュートリアルでは、 *Views\Shared\EditorTemplates\Date.cshtml*テンプレートに `datefield` クラスを追加したことに注意してください)。

次に、 *Views\Shared\\_Layout*ファイルを開きます。 次のファイルへの参照を追加する必要があります。これらのファイルはすべて、日付の選択を使用できるようにするために必要です。

- *Content/theme/base/jquery. ui. css*
- *Content/theme/base/jquery. datepicker*
- *Content/theme/base/jquery. .css*
- *jquery. ui. node.js*
- *datepicker... .js*
- *DatePickerReady*

次の例は、 *Views\Shared\\_Layout*ファイルの `head` 要素の末尾に追加する実際のコードを示しています。

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample6.cshtml)]

完全な `head` のセクションを次に示します。

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample7.cshtml)]

[URL コンテンツヘルパー](https://msdn.microsoft.com/library/system.web.mvc.urlhelper.content.aspx)メソッドは、リソースパスを絶対パスに変換します。 アプリケーションが IIS で実行されているときにこれらのリソースを正しく参照するには、`@URL.Content` を使用する必要があります。

Ctrl キーを押しながら F5 キーを押してアプリケーションを実行します。 編集 リンクを選択し、 **Releasedate** フィールドに挿入ポイントを配置します。 JQuery UI ポップアップカレンダーが表示されます。

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image7.png)

ほとんどの jQuery コントロールと同様に、datepicker を使用すると、広範囲にカスタマイズすることができます。 詳細については、「ビジュアルのカスタマイズ: [jquery ui サイトで](http://learn.jquery.com/jquery-ui/getting-started/)の[jquery Ui テーマの設計](http://learn.jquery.com/jquery-ui/getting-started/#visual-customization-designing-a-jquery-ui-theme)」を参照してください。

### <a name="supporting-the-html5-date-input-control"></a>HTML5 日付入力コントロールのサポート

HTML5 をサポートするブラウザーが増えるにつれて、`date` input 要素などのネイティブ HTML5 入力を使用して、jQuery UI カレンダーを使用しないようにすることができます。 アプリケーションにロジックを追加して、ブラウザーが HTML5 コントロールをサポートしている場合は、自動的に HTML5 コントロールを使用できます。 これを行うには、 *DatePickerReady*ファイルの内容を次のように置き換えます。

[!code-javascript[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample8.js)]

このスクリプトの最初の行では、Modernizr を使用して、HTML5 の日付入力がサポートされていることを確認します。 サポートされていない場合は、代わりに jQuery UI の日付の選択がフックされます。 ([Modernizr](http://www.modernizr.com/docs/)は、HTML5 と CSS3 のネイティブ実装の可用性を検出するオープンソースの JavaScript ライブラリです。 Modernizr は、作成するすべての新しい ASP.NET MVC プロジェクトに含まれています)。

この変更を行った後、Opera 11 などの HTML5 をサポートするブラウザーを使用してテストできます。 HTML5 と互換性のあるブラウザーを使用してアプリケーションを実行し、ムービーエントリを編集します。 次のように、jQuery UI ポップアップカレンダーの代わりに HTML5 日付コントロールが使用されます。

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image8.png)

新しいバージョンのブラウザーは HTML5 を段階的に実装しているため、現時点では、さまざまな HTML5 サポートを利用できるコードを web サイトに追加することをお勧めします。 たとえば、より堅牢な*DatePickerReady*スクリプトを以下に示します。これにより、HTML5 日付コントロールのみを部分的にサポートするブラウザーがサポートされます。

[!code-javascript[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample9.js)]

このスクリプトは、HTML5 日付コントロールを完全にサポートしていない `date` 型の HTML5 `input` の要素を選択します。 これらの要素については、jQuery UI ポップアップカレンダーをフックし、`type` 属性を `date` から `text`に変更します。 `type` 属性を `date` から `text`に変更することにより、部分的な HTML5 日付のサポートは削除されます。 さらに堅牢な*DatePickerReady*スクリプトは[JSFIDDLE](http://jsfiddle.net/XSTK8/15/)にあります。

### <a name="adding-nullable-dates-to-the-templates"></a>テンプレートに Null 許容の日付を追加する

既存の日付テンプレートのいずれかを使用して null 日付を渡すと、実行時エラーが発生します。 日付テンプレートの堅牢性を高めるために、null 値を処理するように変更します。 Null 許容の日付をサポートするには、 *Views\Shared\DisplayTemplates\DateTime.cshtml*のコードを次のように変更します。

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample10.cshtml)]

モデルが**null**の場合、コードは空の文字列を返します。

*Views\Shared\EditorTemplates\Date.cshtml*ファイルのコードを次のように変更します。

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample11.cshtml)]

このコードを実行するときに、モデルが null でない場合は、モデルの `DateTime` 値が使用されます。 モデルが null の場合は、現在の日付が代わりに使用されます。

### <a name="wrapup"></a>Wrapup

このチュートリアルでは、ASP.NET テンプレートヘルパーの基本について説明し、ASP.NET MVC アプリケーションで jQuery UI datepicker popup カレンダーを使用する方法を示します。 詳細については、次のリソースを参照してください。

- ローカライズの詳細については、「Rajeesh's blog [Jqueryui Datepicker in ASP.NET MVC](http://www.rajeeshcv.com/2010/02/jqueryui-datepicker-in-asp-net-mvc/)」を参照してください。
- JQuery UI の詳細については、「 [JQUERY ui](http://docs.jquery.com/UI)」を参照してください。
- Datepicker コントロールをローカライズする方法の詳細については、「 [UI/datepicker/ローカリゼーション](http://docs.jquery.com/UI/Datepicker/Localization)」を参照してください。
- ASP.NET MVC テンプレートの詳細については、 [ASP.NET mvc 2 テンプレート](http://bradwilson.typepad.com/blog/2009/10/aspnet-mvc-2-templates-part-1-introduction.html)の Brad Wilson のブログシリーズを参照してください。 シリーズは ASP.NET MVC 2 用に書かれていますが、この資料は現在のバージョンの ASP.NET MVC にも適用されます。

> [!div class="step-by-step"]
> [[戻る]](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3.md)
