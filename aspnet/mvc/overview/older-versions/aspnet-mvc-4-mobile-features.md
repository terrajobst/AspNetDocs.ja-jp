---
uid: mvc/overview/older-versions/aspnet-mvc-4-mobile-features
title: ASP.NET MVC 4 モバイル機能 |Microsoft Docs
author: Rick-Anderson
description: このチュートリアルの MVC 5 バージョンは、Azure Websites での ASP.NET MVC 5 モバイル Web アプリケーションのデプロイに関するページでコードサンプルと共に使用できます。
ms.author: riande
ms.date: 08/15/2012
ms.assetid: 27dc4fc8-1b51-43b0-933f-fc1b52476523
msc.legacyurl: /mvc/overview/older-versions/aspnet-mvc-4-mobile-features
msc.type: authoredcontent
ms.openlocfilehash: 9716def069ca9f7115af32e16381f41bd4d13342
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457649"
---
# <a name="aspnet-mvc-4-mobile-features"></a>ASP.NET MVC 4 のモバイル機能

[Rick Anderson](https://twitter.com/RickAndMSFT)

> このチュートリアルの MVC 5 バージョンは、 [Azure websites での ASP.NET MVC 5 モバイル Web アプリケーションのデプロイ](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/)に関するページでコードサンプルと共に使用できます。

このチュートリアルでは、ASP.NET MVC 4 Web アプリケーションでモバイル機能を使用する方法の基本について説明します。 このチュートリアルでは、 [Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express)または Visual web Developer 2010 Express Service Pack 1 (&quot;Visual web developer または vwd&quot;) を使用できます。 既にお持ちの場合は、Visual Studio の professional バージョンを使用できます。

開始する前に、以下に示す前提条件がインストールされていることを確認してください。

- [Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express) (推奨) または Visual Studio Web DEVELOPER Express SP1。 Visual Studio 2012 には ASP.NET MVC 4 が含まれています。 Visual Web Developer 2010 を使用している場合は、 [ASP.NET MVC 4](https://go.microsoft.com/fwlink/?LinkId=243392)をインストールする必要があります。

モバイル ブラウザー エミュレーターも必要です。 次のいずれでも動作します。

- [Windows 7 Phone エミュレーター](https://msdn.microsoft.com/library/ff402563(VS.92).aspx)。 (これは、このチュートリアルのほとんどのスクリーンショットで使用されるエミュレーターです)。
- IPhone をエミュレートするようにユーザーエージェント文字列を変更します。 [この](http://www.howtogeek.com/113439/how-to-change-your-browsers-user-agent-without-installing-any-extensions/)ブログエントリを参照してください。
- [Opera Mobile エミュレーター](http://www.opera.com/developer/tools/mobile/)
- ユーザーエージェントが iPhone に設定されている[Apple Safari](http://www.apple.com/safari/download/) 。 Safari のユーザーエージェントを "iPhone" に設定する方法については、David Alison のブログで[safari でその IE を使用する方法](http://www.davidalison.com/2008/05/how-to-let-safari-pretend-its-ie.html)に関する記事をご覧ください。

次のトピック用に、C# のソース コードを使用した Visual Studio プロジェクトが用意されています。

- [スタートプロジェクトのダウンロード](https://go.microsoft.com/fwlink/?linkid=228307&amp;clcid=0x409)
- [完成したプロジェクトのダウンロード](https://go.microsoft.com/fwlink/?linkid=228306&amp;clcid=0x409)

### <a name="what-youll-build"></a>作成するアプリケーション:

このチュートリアルでは、[スタートプロジェクト](https://go.microsoft.com/fwlink/?LinkId=228307)に用意されている単純な会議一覧アプリケーションにモバイル機能を追加します。 次のスクリーンショットは、 [Windows 7 Phone エミュレーター](https://msdn.microsoft.com/library/ff402563(VS.92).aspx)での完成したアプリケーションの [タグ] ページを示しています。 キーボード入力を簡略化するには、「 [Windows Phone Emulator のキーボードマップ](https://msdn.microsoft.com/library/ff754352(v=vs.92).aspx)」を参照してください。

[![p1_Tags_CompletedProj](aspnet-mvc-4-mobile-features/_static/image2.png)](aspnet-mvc-4-mobile-features/_static/image1.png)

Internet Explorer バージョン9または10、FireFox、または Chrome を使用して、[ユーザーエージェント文字列](http://www.howtogeek.com/113439/how-to-change-your-browsers-user-agent-without-installing-any-extensions/)を設定することにより、モバイルアプリケーションを開発できます。 次の図は、iPhone をエミュレートする Internet Explorer を使用した完成したチュートリアルを示しています。 Internet Explorer の開発者用ツールと[Fiddler ツール](http://www.fiddler2.com/fiddler2/)を使用すると、アプリケーションのデバッグに役立てることができます。

![](aspnet-mvc-4-mobile-features/_static/image3.png)

### <a name="skills-youll-learn"></a>学習内容

ここでは次の内容について学習します。

- ASP.NET MVC 4 テンプレートで HTML5 `viewport` 属性とアダプティブレンダリングを使用してモバイルデバイスの表示を向上させる方法について説明します。
- モバイル専用のビューを作成する方法。
- ユーザーがモバイルビューとアプリケーションのデスクトップビューを切り替えることができるビュースイッチャーを作成する方法について説明します。

### <a name="getting-started"></a>作業の開始

次のリンクを使用して、スタートプロジェクトのカンファレンスリストアプリケーションを[ダウンロードします。](https://go.microsoft.com/fwlink/?LinkId=228307) 次に、Windows エクスプローラーで*Mvcmobile .zip*ファイルを右クリックし、 **[プロパティ]** を選択します。 **[Mvcmobile. .zip のプロパティ]** ダイアログボックスで、 **[ブロック解除]** ボタンを選択します。 (ブロックを解除すると、Web からダウンロードした *.zip* ファイルを使おうとしたときに表示されるセキュリティに関する警告を回避できます)。

![p1_unBlock](aspnet-mvc-4-mobile-features/_static/image4.png)

*Mvcmobile .zip*ファイルを右クリックし、 **[すべて展開]** を選択して、ファイルを解凍します。 Visual Studio で、 *Mvcmobile .sln*ファイルを開きます。

CTRL キーを押しながら F5 キーを押してアプリケーションを実行すると、アプリケーションがデスクトップブラウザーに表示されます。 モバイルブラウザーエミュレーターを起動し、会議アプリケーションの URL をエミュレーターにコピーして、 **[タグで参照]** リンクをクリックします。 Windows Phone Emulator を使用している場合は、URL バー内をクリックし、Pause キーを押して、キーボードアクセスを取得します。 次の画像は、( **[タグで参照]** を選択した) *alltags*ビューを示しています。

[![p1_browseTag](aspnet-mvc-4-mobile-features/_static/image6.png)](aspnet-mvc-4-mobile-features/_static/image5.png)

モバイル デバイス上でも読みやすい表示になっています。 [ASP.NET] リンクを選択します。

[![p1_tagged_ASPNET](aspnet-mvc-4-mobile-features/_static/image8.png)](aspnet-mvc-4-mobile-features/_static/image7.png)

ASP.NET タグビューが非常に乱雑になっています。 たとえば、**日付**列の読み取りが非常に困難です。 このチュートリアルの後半では、モバイルブラウザー専用の*Alltags*ビューのバージョンを作成します。これにより、ディスプレイが読みやすくなります。

注: 現在、モバイルキャッシュエンジンにはバグが存在します。 実稼働アプリケーションの場合は、[固定 DisplayModes](http://nuget.org/packages/Microsoft.AspNet.Mvc.FixedDisplayModes) nugget パッケージをインストールする必要があります。 修正の詳細については、「 [ASP.NET MVC 4 Mobile Cache Bug Fixed](https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx) 」を参照してください。

## <a name="css-media-queries"></a>CSS メディアクエリ

[Css メディアクエリ](http://www.w3.org/TR/css3-mediaqueries/)は、メディアの種類に対する css の拡張機能です。 特定のブラウザー (ユーザーエージェント) の既定の CSS 規則を上書きする規則を作成できます。 モバイルブラウザーを対象とする CSS の一般的な規則は、画面の最大サイズを定義することです。 新しい ASP.NET MVC 4 インターネットプロジェクトを作成するときに作成される*Contentsite.css*ファイルには、次のメディアクエリが含まれています。

[!code-css[Main](aspnet-mvc-4-mobile-features/samples/sample1.css)]

ブラウザーウィンドウが850ピクセル幅以下である場合は、このメディアブロック内の CSS ルールが使用されます。 このような CSS メディアクエリを使用すると、デスクトップブラウザーの幅が広くなるように設計された既定の CSS 規則よりも小さいブラウザー (モバイルブラウザーなど) で HTML コンテンツをより適切に表示できます。

## <a name="the-viewport-meta-tag"></a>ビューポートメタタグ

ほとんどのモバイルブラウザーでは、モバイルデバイスの実際の幅よりはるかに大きい仮想ブラウザーウィンドウの幅 (*ビューポート*) が定義されています。 これにより、モバイルブラウザーは web ページ全体を仮想ディスプレイ内に収めることができます。 ユーザーは、興味深いコンテンツにズームインできます。 ただし、ビューポートの幅を実際のデバイスの幅に設定した場合、コンテンツがモバイルブラウザーに収まるため、ズームは必要ありません。

ASP.NET MVC 4 レイアウトファイルのビューポート `<meta>` タグによって、ビューポートがデバイスの幅に設定されます。 次の行は、ASP.NET MVC 4 レイアウトファイルのビューポート `<meta>` タグを示しています。

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample2.html)]

## <a name="examining-the-effect-of-css-media-queries-and-the-viewport-meta-tag"></a>CSS メディアクエリとビューポートメタタグの効果を調べる

エディターで*Views\Shared\\_Layout*ファイルを開き、ビューポート `<meta>` タグをコメントアウトします。 次のマークアップは、コメントアウトされた行を示しています。

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample3.cshtml)]

エディターで*MvcMobile\Content\Site.css*ファイルを開き、メディアクエリの最大の幅を0ピクセルに変更します。 これにより、モバイルブラウザーで CSS ルールが使用されなくなります。 次の行は、変更されたメディアクエリを示しています。

[!code-css[Main](aspnet-mvc-4-mobile-features/samples/sample4.css)]

変更を保存し、モバイルブラウザーエミュレーターで会議アプリケーションを参照します。 次の図の小さなテキストは、ビューポート `<meta>` タグを削除した結果です。 ビューポート `<meta>` タグがない場合、ブラウザーは既定のビューポートの幅 (ほとんどのモバイルブラウザーでは850ピクセル以上) にズームアウトします。

[![p1_noViewPort](aspnet-mvc-4-mobile-features/_static/image10.png)](aspnet-mvc-4-mobile-features/_static/image9.png)

変更を元に戻して、レイアウトファイルのビューポート `<meta>` タグのコメントを解除し、メディアクエリを*サイト .css*ファイルの850ピクセルに復元します。 変更を保存し、モバイルブラウザーを最新の状態に更新して、モバイル対応のディスプレイが復元されたことを確認します。

ビューポート `<meta>` タグと CSS メディアクエリは ASP.NET MVC 4 に固有のものではなく、すべての web アプリケーションでこれらの機能を利用できます。 ただし、新しい ASP.NET MVC 4 プロジェクトを作成するときに生成されるファイルに組み込まれるようになりました。

ビューポート `<meta>` タグの詳細については、「 [tale of two」の2つのビューポート](http://www.quirksmode.org/mobile/viewports2.html)を参照してください。

次のセクションでは、モバイル ブラウザー専用ビューを作成する方法について説明します。

## <a name="overriding-views-layouts-and-partial-views"></a>ビュー、レイアウト、および部分ビューのオーバーライド

ASP.NET MVC 4 の重要な新機能は、モバイルブラウザー全般、個々のモバイルブラウザー、または特定のブラウザーに対して、すべてのビュー (レイアウトと部分ビューを含む) を上書きできる単純なメカニズムです。 モバイル専用ビューを用意するには、ビュー ファイルをコピーして *.Mobile* をファイル名に追加します。 たとえば、モバイル*インデックス*ビューを作成するには、 *Views\Home\Index.cshtml*を*Views\Home\Index.Mobile.cshtml*にコピーします。

このセクションでは、モバイル専用のレイアウト ファイルを作成します。

開始するには、 *Views\Shared\\_Layout*を*Views\Shared\\_Layout*にコピーします。 *\_Layout*を開き、 **MVC4 カンファレンス**から**カンファレンス (Mobile)** にタイトルを変更します。

各 `Html.ActionLink` 呼び出しで、各リンク*html.actionlink*の "Browse by" を削除します。 次のコードは、モバイルレイアウトファイルの完成した body セクションを示しています。

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample5.cshtml)]

*Views\Home\AllTags.cshtml*ファイルを*Views\Home\AllTags.Mobile.cshtml*にコピーします。 新しいファイルを開き、次のように `<h2>` 要素を「Tags」から「Tags (M)」に変更します。

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample6.html)]

デスクトップ ブラウザー、および、モバイル ブラウザー エミュレーターを使用してタグ ページに移動します。 モバイルブラウザーエミュレーターには、2つの変更が表示されます。

[![p2m_layoutTags](aspnet-mvc-4-mobile-features/_static/image12.png)](aspnet-mvc-4-mobile-features/_static/image11.png)

これに対して、デスクトップの表示は変更されていません。

[![p2_layoutTagsDesktop](aspnet-mvc-4-mobile-features/_static/image14.png)](aspnet-mvc-4-mobile-features/_static/image13.png)

## <a name="browser-specific-views"></a>ブラウザー固有のビュー

モバイル専用のビューやデスクトップ専用のビューに加え、個別のブラウザーに対してビューを作成できます。 たとえば、iPhone ブラウザー専用のビューを作成できます。 このセクションでは、iPhone ブラウザーと iPhone バージョンの *AllTags* ビュー用のレイアウトを作成します。

*Global.asax*ファイルを開き、次のコードを `Application_Start` メソッドに追加します。

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample7.cs)]

このコードでは、"iPhone" という表示モードを定義し、受信された各要求をその定義に対して照合します。 受信された要求が定義した条件に一致する場合 (つまり、ユーザー エージェントに "iPhone" という文字列が含まれている場合)、"iPhone" というサフィックスが含まれる名前のビューが ASP.NET MVC によって検索されます。

コードで、`DefaultDisplayMode` を右クリックし、 **[解決]** 、`using System.Web.WebPages;` の順にクリックします。 `System.Web.WebPages` 型と `DisplayModes` 型が定義されている `DefaultDisplayMode` 名前空間に参照が追加されます。

[![p2_resolve](aspnet-mvc-4-mobile-features/_static/image16.png)](aspnet-mvc-4-mobile-features/_static/image15.png)

別の方法として、単純にファイルの `using` セクションに、次の行を手動で追加することもできます。

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample8.cs)]

*Global.asax*ファイルの完全な内容を次に示します。

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample9.cs)]

変更を保存します。 *MvcMobile\Views\Shared\\_Layout* *\\_Layout*にコピーします。このファイルは、MvcMobile\Views\Shared にコピーします。 新しいファイルを開き、`h1` 見出しを `Conference (Mobile)` から `Conference (iPhone)`に変更します。

*MvcMobile\Views\Home\AllTags.Mobile.cshtml*ファイルを*MvcMobile\Views\Home\AllTags.iPhone.cshtml*にコピーします。 新しいファイルで、 `<h2>` 要素を "Tags (M)" から "Tags (iPhone)" に変更します。

アプリケーションを実行します。 モバイル ブラウザー エミュレーターを実行し、ユーザー エージェントが "iPhone" に設定されていることを確認して、 *AllTags* ビューにアクセスします。 次のスクリーンショットは、 [Safari](http://www.apple.com/safari/download/)ブラウザーに表示される*alltags*ビューを示しています。 Windows 用 Safari は[こちら](https://support.apple.com/kb/DL1531)からダウンロードできます。

[![p2_iphoneView](aspnet-mvc-4-mobile-features/_static/image18.png)](aspnet-mvc-4-mobile-features/_static/image17.png)

このセクションでは、モバイル レイアウトとビューの作成方法および iPhone などの特定のデバイス専用のレイアウトとビューの作成方法を説明しました。 次のセクションでは、より説得力のあるモバイルビューに jQuery Mobile を活用する方法について説明します。

## <a name="using-jquery-mobile"></a>JQuery Mobile の使用

[JQuery mobile](http://jquerymobile.com/demos/1.0b3/#/demos/1.0b3/docs/about/intro.html)ライブラリには、すべての主要なモバイルブラウザーで動作するユーザーインターフェイスフレームワークが用意されています。 jQuery Mobile は、CSS と JavaScript をサポートするモバイルブラウザーに*プログレッシブ拡張機能*を適用します。 プログレッシブ拡張機能を使用すると、すべてのブラウザーが web ページの基本コンテンツを表示できるようになります。一方、より強力なブラウザーやデバイスでは、より豊富な表示を行うことができます。 JQuery Mobile のスタイルに含まれる JavaScript ファイルと CSS ファイルは、マークアップを変更することなく、モバイルブラウザーに合わせて多数の要素に対応しています。

このセクションでは、jquery Mobile とビュースイッチャーウィジェットをインストールする*jquery*の NuGet パッケージをインストールします。

最初に、前の手順で作成した*共有\\_Layout* 、_Layout、および*共有\\* を削除します。

*Views\Home\AllTags.Mobile.cshtml*ファイルと*Views\Home\AllTags.iPhone.cshtml*ファイルの名前を*Views\Home\AllTags.iPhone.cshtml.hide*と*Views\Home\AllTags.Mobile.cshtml.hide*に変更します。 ファイルに*は拡張子が*付いていないため、ASP.NET MVC ランタイムで*alltags*ビューを表示するために使用されることはありません。

次の手順に従って、 *jQuery. Mobile. MVC* NuGet パッケージをインストールします。

1. **[ツール]** メニューの **[NuGet パッケージマネージャー]** を選択し、 **[パッケージマネージャーコンソール]** を選択します。

    [![p3_packageMgr](aspnet-mvc-4-mobile-features/_static/image20.png)](aspnet-mvc-4-mobile-features/_static/image19.png)
2. **パッケージマネージャーコンソール**で、「」と入力し `Install-Package jQuery.Mobile.MVC -version 1.0.0`

次の図は、NuGet jQuery. Mobile. MVC パッケージによって追加され、MvcMobile プロジェクトに変更されたファイルを示しています。 追加されるファイルには、ファイル名の後に [add] が追加されています。 この画像では、*コンテンツ \ イメージ*フォルダーに追加された GIF ファイルと PNG ファイルは表示されません。

![](aspnet-mvc-4-mobile-features/_static/image21.png)

JQuery の NuGet パッケージでは、次のものがインストールされます。

- *アプリ\_Start\BundleMobileConfig.cs*ファイル。これは、追加された jQuery JAVASCRIPT と CSS ファイルを参照するために必要です。 次の手順に従って、このファイルで定義されているモバイルバンドルを参照する必要があります。
- jQuery Mobile CSS ファイル。
- `ViewSwitcher` コントローラーウィジェット (コントローラー \*ビュー*)。
- jQuery Mobile JavaScript ファイル。
- JQuery モバイルスタイルのレイアウトファイル (*Views\Shared\\_Layout*)。
- ビュースイッチャー部分ビュー *(MvcMobile\Views\Shared\\_ViewSwitcher*)。デスクトップビューからモバイルビューに切り替えるためのリンクが各ページの上部に表示されます。逆の場合も同様です。
- <em>Content¥ images</em>フォルダー内のいくつかの<em>.png</em>および<em>.gif</em>画像ファイル。

*Global.asax*ファイルを開き、`Application_Start` メソッドの最後の行として次のコードを追加します。

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample10.cs)]

次のコードは、完全な*global.asax*ファイルを示しています。

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample11.cs?highlight=26)]

> [!NOTE]
> Internet Explorer 9 を使用していて、上に黄色の強調表示されている `BundleMobileConfig` が表示されていない場合は、IE の [![互換表示] ボタン (オフ) の](https://res2.windows.microsoft.com/resbox/en/Windows 7/main/f080e77f-9b66-4ac8-9af0-803c4f8a859c_15.jpg "[互換表示] ボタンの画像 (オフ)")[[互換](https://windows.microsoft.com/windows7/How-to-use-Compatibility-View-in-Internet-Explorer-9)表示] ボタンの画像をクリックして、[互換表示![] ボタン (オフ) のアウトライン画像](https://res2.windows.microsoft.com/resbox/en/Windows 7/main/f080e77f-9b66-4ac8-9af0-803c4f8a859c_15.jpg "[互換表示] ボタンの画像 (オフ)")から [互換![表示] ボタン (オン) の](https://res1.windows.microsoft.com/resbox/en/Windows 7/main/156805ff-3130-481b-a12d-4d3a96470f36_14.jpg "[互換表示] ボタンの画像 (オン)")純色の画像に または、このチュートリアルを FireFox または Chrome で表示することもできます。

*MvcMobile\Views\Shared\\_Layout*を開き、`Html.Partial` の呼び出しの直後に次のマークアップを追加します。

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample12.cshtml)]

完全な*MvcMobile\Views\Shared\\_Layout*を次に示します。

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample13.cshtml)]

アプリケーションをビルドし、モバイルブラウザーエミュレーターで*Alltags*ビューを参照します。 次のように表示されます。

[![p3_afterNuGet](aspnet-mvc-4-mobile-features/_static/image23.png)](aspnet-mvc-4-mobile-features/_static/image22.png)

> [!NOTE]
> モバイル固有のコードをデバッグするには、IE または Chrome の[ユーザーエージェント文字列](http://www.howtogeek.com/113439/how-to-change-your-browsers-user-agent-without-installing-any-extensions/)を iPhone に設定してから、F-12 開発者ツールを使用します。 モバイルブラウザーに **[ホーム]** 、 **[スピーカー]** 、 **[タグ]** 、 **[日付]** の各リンクがボタンとして表示されない場合、jQuery モバイルスクリプトと CSS ファイルへの参照が正しくない可能性があります。

スタイルの変更に加えて、 **[モバイルビュー]** と、モバイルビューからデスクトップビューに切り替えるためのリンクが表示されます。 **[デスクトップビュー]** リンクをクリックすると、デスクトップビューが表示されます。

[![p3_desktopView](aspnet-mvc-4-mobile-features/_static/image25.png)](aspnet-mvc-4-mobile-features/_static/image24.png)

デスクトップビューには、モバイルビューに直接移動する方法は用意されていません。 これを修正します。 *Views\Shared\\_Layout*ファイルを開きます。 Page `body` 要素のすぐ下に、ビュースイッチャーウィジェットをレンダリングする次のコードを追加します。

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample14.cshtml)]

モバイルブラウザーで*Alltags*ビューを更新します。 デスクトップビューとモバイルビュー間を移動できるようになりました。

[![p3_desktopViewWithMobileLink](aspnet-mvc-4-mobile-features/_static/image27.png)](aspnet-mvc-4-mobile-features/_static/image26.png)

> [!NOTE]
> デバッグメモ: Views\Shared\\_ViewSwitcher の末尾に次のコードを追加すると、ユーザーエージェント文字列がモバイルデバイスに設定されているブラウザーを使用しているときに、ビューのデバッグに役立ちます。
>
> [!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample15.cs)]
>
> 次の見出しを*Views\Shared\\_Layout*ファイルに追加します。
>
> [!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample16.html)]

デスクトップブラウザーで*Alltags*ページに移動します。 ビュースイッチャーウィジェットは、モバイルレイアウトページにのみ追加されるため、デスクトップブラウザーには表示されません。 このチュートリアルの後半では、ビュースイッチャーウィジェットをデスクトップビューに追加する方法について説明します。

[![p3_desktopBrowser](aspnet-mvc-4-mobile-features/_static/image29.png)](aspnet-mvc-4-mobile-features/_static/image28.png)

## <a name="improving-the-speakers-list"></a>スピーカーリストを改善する

モバイル ブラウザーで **[Speakers]** リンクをタップします。 モバイルビュー (*Allspeakers. cshtml*) がないため、既定のスピーカー表示 (*allspeakers. cshtml*) は、モバイルレイアウトビュー ( *\_layout*) を使用してレンダリングされます。

[![p3_speakersDeskTop](aspnet-mvc-4-mobile-features/_static/image31.png)](aspnet-mvc-4-mobile-features/_static/image30.png)

既定の (非モバイル) ビューをグローバルに無効にするには、次のように、`RequireConsistentDisplayMode` を設定して、 *_ViewStart ファイル\\ビュー*で `true` に設定します。

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample17.cshtml)]

`RequireConsistentDisplayMode` が `true`に設定されている場合、モバイルレイアウト (<em>\_layout</em>) はモバイルビューにのみ使用されます。 (つまり、ビューファイルの形式は<em>* * ViewName</em><em>です。Mobile.</em>) モバイルレイアウトが非モバイルビューでうまく機能しない場合は、`RequireConsistentDisplayMode` を `true` に設定します。 次のスクリーンショットは `RequireConsistentDisplayMode` が `true`に設定されている場合に、<em>スピーカー</em>ページがどのようにレンダリングされるかを示しています。

[![p3_speakersConsistent](aspnet-mvc-4-mobile-features/_static/image33.png)](aspnet-mvc-4-mobile-features/_static/image32.png)

ビューファイルで `false` に `RequireConsistentDisplayMode` を設定すると、ビューの一貫した表示モードを無効にすることができます。 *Views\Home\AllSpeakers.cshtml*ファイル内の次のマークアップは、`RequireConsistentDisplayMode` を `false`に設定します。

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample18.cshtml)]

## <a name="creating-a-mobile-speakers-view"></a>モバイルスピーカービューの作成

いま見たように、 *Speakers* ビューは読み取れますが、リンクが小さく、モバイル デバイスではタップが困難です。 このセクションでは、最新のモバイルアプリケーションのようなモバイル固有の*スピーカー*ビューを作成します。これには、大規模でタップしやすいリンクが表示され、スピーカーをすばやく見つけるための検索ボックスが含まれています。

*Allspeakers. cshtml*を*Allspeakers. Mobile. cshtml*にコピーします。 *Allspeakers の cshtml*ファイルを開き、`<h2>` の見出し要素を削除します。

`<ul>` タグに `data-role` 属性を追加し、その値を `listview`に設定します。 他の[`data-*` 属性](http://html5doctor.com/html5-custom-data-attributes/)と同様に、`data-role="listview"` は大きなリストアイテムをタップしやすくなります。 完成したマークアップは、次のようになります。

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample19.cshtml)]

モバイル ブラウザーの表示を更新します。 更新されたビューは次のようになります。

[![p3_updatedSpeakerView1](aspnet-mvc-4-mobile-features/_static/image35.png)](aspnet-mvc-4-mobile-features/_static/image34.png)

モバイルビューは改善されていますが、スピーカーの長い一覧を移動するのは困難です。 この問題を解決するには、`<ul>` タグで `data-filter` 属性を追加し、`true`に設定します。 次のコードは、`ul` マークアップを示しています。

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample20.html)]

次の図は、`data-filter` 属性によって生成されるページの上部にある検索フィルターボックスを示しています。

[![ps_Data_Filter](aspnet-mvc-4-mobile-features/_static/image37.png)](aspnet-mvc-4-mobile-features/_static/image36.png)

検索ボックスに各文字を入力すると、次の図に示すように、jQuery Mobile によって表示される一覧がフィルター処理されます。

[![ps_data_filter_SC](aspnet-mvc-4-mobile-features/_static/image39.png)](aspnet-mvc-4-mobile-features/_static/image38.png)

## <a name="improving-the-tags-list"></a>タグリストの改良

既定の*スピーカー*ビューと同様に、[*タグ*] ビューは読み取り可能ですが、リンクは小さく、モバイルデバイスではタップが困難です。 このセクションでは、[*スピーカー* ] ビューを固定するのと同じ方法で*タグ*ビューを修正します。

名前が*Views\Home\AllTags.Mobile.cshtml*になるように、 *Views\Home\AllTags.Mobile.cshtml.hide*ファイルの&quot; サフィックス &quot;を削除します。 名前を変更したファイルを開き、`<h2>` 要素を削除します。

次に示すように、`data-role` 属性と `data-filter` 属性を `<ul>` タグに追加します。

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample21.html)]

次の画像は、`J`文字にフィルターを適用するタグページを示しています。

[![p3_tags_J](aspnet-mvc-4-mobile-features/_static/image41.png)](aspnet-mvc-4-mobile-features/_static/image40.png)

## <a name="improving-the-dates-list"></a>日付の一覧の改善

[*日付*] ビューは、モバイルデバイスで使用しやすくするために、*スピーカー*や*タグ*の表示を改善した場合と同様に改善できます。

*Views\Home\AllDates.cshtml*ファイルを*Views\Home\AllDates.Mobile.cshtml*にコピーします。 新しいファイルを開き、`<h2>` 要素を削除します。

次のように、`data-role="listview"` を `<ul>` タグに追加します。

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample22.html)]

次の図は、`data-role` の属性が設定された**日付**ページの外観を示しています。

[![p3_dates1](aspnet-mvc-4-mobile-features/_static/image43.png)](aspnet-mvc-4-mobile-features/_static/image42.png)*Views\Home\AllDates.Mobile.cshtml*ファイルの内容を次のコードに置き換えます。

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample23.cshtml)]

このコードは、すべてのセッションを日単位でグループ化します。 これにより、新しい日ごとにリストの区分線が作成され、各日のすべてのセッションが区分線の下に一覧表示されます。 このコードを実行すると、次のようになります。

[![p3_dates2](aspnet-mvc-4-mobile-features/_static/image45.png)](aspnet-mvc-4-mobile-features/_static/image44.png)

## <a name="improving-the-sessionstable-view"></a>SessionsTable ビューの向上

このセクションでは、セッションのモバイル固有のビューを作成します。 ここで行った変更は、作成した他のビューよりも広くなります。

モバイルブラウザーで、 **[スピーカー]** ボタンをタップし、[検索] ボックスに「`Sc`」と入力します。

[![ps_data_filter_SC](aspnet-mvc-4-mobile-features/_static/image47.png)](aspnet-mvc-4-mobile-features/_static/image46.png)

**Scott マン Selman**リンクをタップします。

[![p3_scottHa](aspnet-mvc-4-mobile-features/_static/image49.png)](aspnet-mvc-4-mobile-features/_static/image48.png)

ご覧のように、モバイルブラウザーで表示するのは簡単ではありません。 日付列が読みにくく、タグ列がビューから外れています。 この問題を解決するには、 *Views\Home\SessionsTable.cshtml*を*Views\Home\SessionsTable.Mobile.cshtml*にコピーし、ファイルの内容を次のコードに置き換えます。

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample24.cshtml)]

このコードでは、ルームとタグ列を削除し、タイトル、スピーカー、および日付を縦に書式設定して、すべての情報がモバイルブラウザーで読み取れるようにします。 次の図にはコードの変更が反映されています。

[![ps_SessionsByScottHa](aspnet-mvc-4-mobile-features/_static/image51.png)](aspnet-mvc-4-mobile-features/_static/image50.png)

## <a name="improving-the-sessionbycode-view"></a>SessionByCode ビューの向上

最後に、 *Sessionbycode*ビューのモバイル専用ビューを作成します。 モバイルブラウザーで、 **[スピーカー]** ボタンをタップし、[検索] ボックスに「`Sc`」と入力します。

[![ps_data_filter_SC](aspnet-mvc-4-mobile-features/_static/image53.png)](aspnet-mvc-4-mobile-features/_static/image52.png)

**Scott マン Selman**リンクをタップします。 Scott マン Selman のセッションが表示されます。

[![ps_SessionsByScottHa](aspnet-mvc-4-mobile-features/_static/image55.png)](aspnet-mvc-4-mobile-features/_static/image54.png)

**MS Web スタック**の [お気に入り] リンクの概要を選択します。

[![ps_love](aspnet-mvc-4-mobile-features/_static/image57.png)](aspnet-mvc-4-mobile-features/_static/image56.png)

既定のデスクトップビューは問題ありませんが、改善することができます。

*Views\Home\SessionByCode.cshtml*を*Views\Home\SessionByCode.Mobile.cshtml*にコピーし、 *Views\Home\SessionByCode.Mobile.cshtml*ファイルの内容を次のマークアップに置き換えます。

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample25.cshtml)]

新しいマークアップでは、`data-role` 属性を使用して、ビューのレイアウトを改善します。

モバイル ブラウザーの表示を更新します。 次の図には行ったコードの変更が反映されています。

[![p3_love2](aspnet-mvc-4-mobile-features/_static/image59.png)](aspnet-mvc-4-mobile-features/_static/image58.png)

## <a name="wrapup-and-review"></a>Wrapup とレビュー

このチュートリアルでは、ASP.NET MVC 4 Developer Preview の新しいモバイル機能を紹介しました。 モバイル機能には次のものがあります。

- レイアウト、ビュー、部分ビューをグローバルと個々のビューの両方でオーバーライドする機能。
- `RequireConsistentDisplayMode` プロパティを使用してレイアウトと部分オーバーライドの適用を制御します。
- モバイルビューのビュー切り替えウィジェットは、デスクトップビューに表示することもできます。
- IPhone ブラウザーなど、特定のブラウザーをサポートするためのサポート。

## <a name="see-also"></a>参照

- [JQuery モバイル](http://jquerymobile.com)サイト。
- [jQuery Mobile の概要](http://jquerymobile.com/demos/1.0b3/docs/about/intro.html)
- [W3C 勧告: モバイル Web アプリケーションのベスト プラクティス](http://www.w3.org/TR/mwabp/)
- [W3C のメディア クエリに関する勧告候補](http://www.w3.org/TR/css3-mediaqueries/)
