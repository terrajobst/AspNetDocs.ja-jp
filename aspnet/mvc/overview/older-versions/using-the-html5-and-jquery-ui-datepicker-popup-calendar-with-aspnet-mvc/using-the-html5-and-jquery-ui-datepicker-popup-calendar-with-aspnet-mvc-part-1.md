---
uid: mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1
title: ASP.NET MVC での HTML5 と jQuery UI Datepicker ポップアップカレンダーの使用-パート 1 |Microsoft Docs
author: Rick-Anderson
description: このチュートリアルでは、ASP.NET MV... でエディターテンプレート、表示テンプレート、jQuery UI datepicker popup カレンダーを操作する方法の基本について説明します。
ms.author: riande
ms.date: 08/29/2011
ms.assetid: c23d27f7-b0cf-44f2-8445-fb69e045c674
msc.legacyurl: /mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1
msc.type: authoredcontent
ms.openlocfilehash: c1c2380f24c72f6aabaaacaf975e95288a384ff1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78433288"
---
# <a name="using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc---part-1"></a>ASP.NET MVC での HTML5 と jQuery UI Datepicker ポップアップカレンダーの使用-パート1

[Rick Anderson](https://twitter.com/RickAndMSFT)

> このチュートリアルでは、ASP.NET MVC Web アプリケーションでエディターテンプレート、表示テンプレート、jQuery UI datepicker popup カレンダーを操作する方法の基本について説明します。

このチュートリアルでは、ASP.NET MVC Web アプリケーションでエディターテンプレート、表示テンプレート、jQuery [UI datepicker popup カレンダー](http://plugins.jquery.com/project/datepicker)を操作する方法の基本について説明します。 このチュートリアルでは、Microsoft Visual Web Developer 2010 Express Service Pack 1 (&quot;Visual Web Developer&quot;) を使用できます。これは Microsoft Visual Studio の無料バージョンです。または、既に Visual Studio 2010 SP1 を使用することもできます。

開始する前に、以下に示す前提条件がインストールされていることを確認してください。 これらのすべてをインストールするには、[ [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)] リンクをクリックします。 または、次のリンクを使用して、必要なソフトウェアを個別にインストールすることもできます。

- [Visual Studio Web Developer Express SP1 の前提条件](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
- [ASP.NET MVC 3 ツールの更新](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
- [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(ランタイム + ツールのサポート)

Visual Web Developer ではなく Visual Studio 2010 を使用している場合は、次のリンクをクリックして必要なコンポーネントをインストールしてください: [Visual studio 2010 の前提条件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。

このチュートリアルでは、「 [mvc 3 を使用](../getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)したはじめに」チュートリアルを完了していること、または ASP.NET mvc 開発に慣れていることを前提としています。 このチュートリアルでは、「 [MVC 3 を使用](../getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)したはじめに」チュートリアルの完成したプロジェクトから始めます。

このチュートリアルでは、 C#のコードを示します。 ただし、[スタートプロジェクト](https://archive.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=15800)と完成したプロジェクトは、Visual Basic でも使用できます。

と Visual Basic ソースコードをC#含む Visual Studio プロジェクトは、「[ダウンロード](https://archive.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=15800)」を参照してください。

### <a name="what-youll-build"></a>作成するアプリケーション:

「 [MVC 3 を使用](../getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)したはじめに」のチュートリアルで作成した単純なムービーリストアプリケーションに、テンプレート (具体的には編集および表示テンプレート) を追加します。 また、 [JQUERY UI datepicker](http://jqueryui.com/demos/datepicker/)ポップアップカレンダーを追加して、日付入力のプロセスを簡略化します。 次のスクリーンショットは、変更されたアプリケーションを示しています。 jQuery UI datepicker ポップアップカレンダーが表示されています。

![終了した jQuery](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1/_static/image1.png)

### <a name="skills-youll-learn"></a>学習内容

ここでは次の内容について学習します。

- [Dataannotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)名前空間の属性を使用して、データが表示されたときと編集モードになったときの形式を制御する方法。
- テンプレートを作成する方法 (テンプレートの編集と表示) を行って、データの書式設定を制御する方法について説明します。
- 日付フィールドを入力する方法として[JQUERY UI datepicker](http://jqueryui.com/demos/datepicker/)を追加する方法。

### <a name="getting-started"></a>作業の開始

スタートプロジェクトからムービー一覧アプリケーションをまだ持っていない場合は、次のようにダウンロードします。 

* を[ダウンロード](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)します。
* Windows エクスプローラーで、 *Mvcmovie*ファイルを右クリックし、 **[プロパティ]** を選択します。 
* **[Mvcmovie のプロパティ]** ダイアログボックスで、 **[ブロックの解除]** を選択します。 (ブロックを解除すると、Web からダウンロードした *.zip* ファイルを使おうとしたときに表示されるセキュリティに関する警告を回避できます)。

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1/_static/image2.png)

*Mvcmovie .zip*ファイルを右クリックし、 **[すべて展開]** を選択して、ファイルを解凍します。 Visual Web Developer または Visual Studio 2010 で、 *MvcMovieCS\_TU*ファイルを開きます。

**ソリューションエクスプローラー**で、 *Views\Shared\\_Layout*をダブルクリックして開きます。 `H1` ヘッダーを**MVC Movie アプリ**から**movie jQuery**に変更します。 CTRL キーを押しながら F5 キーを押してアプリケーションを実行し、 **[ホーム]** タブをクリックします。これにより、ムービーコントローラーの `Index` 方法が表示されます。 アプリケーションを試すには、いずれかのムービーの **[編集]** リンクと **[詳細]** リンクを選択します。 [インデックス]、[編集]、および [詳細] の各ビューで、リリース日と価格が適切に書式設定されていることに注意してください。

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1/_static/image3.png)

日付と価格の書式設定は、`Movie` クラスのプロパティで[Displayformat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx)属性を使用した結果です。

*Movie.cs*ファイルを開き、`ReleaseDate` プロパティと `Price` プロパティの `DisplayFormat` 属性をコメントアウトします。 生成される `Movie` クラスは次のようになります。

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1/samples/sample1.cs)]

CTRL キーを押しながら F5 キーをもう一度押してアプリケーションを実行し、 **[ホーム]** タブを選択してムービーの一覧を表示します。 今回はリリース日に日付と時刻が表示され、price フィールドには通貨記号が表示されなくなりました。 `Movie` クラスでの変更により、前に見たような書式設定が元に戻されましたが、それをすぐに修正します。

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1/_static/image4.png)

### <a name="using-the-dataannotations-datatype-attribute-to-specify-the-data-type"></a>DataAnnotations DataType 属性を使用してデータ型を指定する

`Date` 列挙体を使用して、`ReleaseDate` プロパティのコメントアウトされた `DisplayFormat` 属性を[DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)属性に置き換えます。 `Price` プロパティの `DisplayFormat` 属性を[DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)属性に置き換えます。今回は `Currency` 列挙体を使用します。 完成したコードは次のようになります。

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1/samples/sample2.cs)]

アプリケーションを実行します。 これで、リリース日と価格プロパティが正しく書式設定されます (つまり、適切な日付と通貨の形式を使用します)。 [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)属性は、フィールドが正しい形式で表示されるように、組み込みの ASP.NET MVC テンプレートの型メタデータを提供します。 `DataType` 属性を使用すること `DisplayFormat` をお勧めします。これは、`DataType` 属性によってモデルが簡素化され、国際化などの目的で柔軟になるためです。

次のセクションでは、カスタムテンプレートを使用して日付フィールドを表示する方法について説明します。

> [!div class="step-by-step"]
> [Next](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2.md)
