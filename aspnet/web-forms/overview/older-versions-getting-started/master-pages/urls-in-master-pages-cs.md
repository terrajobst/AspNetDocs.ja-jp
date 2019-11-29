---
uid: web-forms/overview/older-versions-getting-started/master-pages/urls-in-master-pages-cs
title: マスターページ内の UrlC#() |Microsoft Docs
author: rick-anderson
description: マスターページファイルがコンテンツページとは異なる相対ディレクトリにあることが原因で、マスターページ内の Url がどのように壊れるかを説明します。 リベースを確認します...
ms.author: riande
ms.date: 06/10/2008
ms.assetid: 48b58a18-5ea4-468c-b326-f35331b3e1e9
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/urls-in-master-pages-cs
msc.type: authoredcontent
ms.openlocfilehash: 2551a5361256234883bb37e46e794037284445a4
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74640967"
---
# <a name="urls-in-master-pages-c"></a>マスター ページの URL (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[コードのダウンロード](https://download.microsoft.com/download/e/e/f/eef369f5-743a-4a52-908f-b6532c4ce0a4/ASPNET_MasterPages_Tutorial_04_CS.zip)または[PDF のダウンロード](https://download.microsoft.com/download/8/f/6/8f6349e4-6554-405a-bcd7-9b094ba5089a/ASPNET_MasterPages_Tutorial_04_CS.pdf)

> マスターページファイルがコンテンツページとは異なる相対ディレクトリにあることが原因で、マスターページ内の Url がどのように壊れるかを説明します。 宣言構文で ~ で Url をリベースし、プログラムで ResolveUrl と ResolveClientUrl を使用する方法について見ていきます。 (も参照してください。

## <a name="introduction"></a>はじめに

これまでに説明したすべての例で、マスターページとコンテンツページは同じフォルダー (web サイトのルートフォルダー) に配置されています。 ただし、マスターページとコンテンツページを同じフォルダーに配置する必要がある理由はありません。 もちろん、サブフォルダーにコンテンツページを作成することもできます。 同様に、サイトのマスターページを配置する `~/MasterPages/` フォルダーを作成することもできます。

マスターページとコンテンツページを異なるフォルダーに配置した場合の潜在的な問題の1つは、Url の破損です。 マスターページにハイパーリンク、画像、またはその他の要素の相対 Url が含まれている場合、リンクは別のフォルダーに存在するコンテンツページに対して無効になります。 このチュートリアルでは、この問題の原因と回避策についても説明します。

## <a name="the-problem-with-relative-urls"></a>相対 Url に関する問題

Web ページの URL は、web ページが指すリソースの場所が web サイトのフォルダー構造内の web ページの場所に対して相対的である場合、*相対 url*と呼ばれます。 先頭のスラッシュ (`/`) またはプロトコル (`http://`など) で始まらない URL は、URL が含まれている web ページの場所に基づいてブラウザーによって解決されるため、相対的になります。

たとえば、web サイトには、`PoweredByASPNET.gif`の1つのイメージファイルを持つ `~/Images/` フォルダーがあります。 マスターページファイル `Site.master` には、`footerContent` 領域に次のマークアップで `<img>` 要素があります。

[!code-html[Main](urls-in-master-pages-cs/samples/sample1.html)]

`<img>` 要素の `src` 属性値は `/` または `http://`で始まらないため、相対 URL です。 つまり、`src` 属性値は、`PoweredByASPNET.gif`という名前のファイルの `Images` サブフォルダーを検索するようにブラウザーに指示します。

コンテンツページにアクセスすると、上記のマークアップがブラウザーに直接送信されます。 `About.aspx` にアクセスし、ブラウザーに送信される HTML ソースを表示します。 マスターページでまったく同じマークアップがブラウザーに送信されたことがわかります。

[!code-html[Main](urls-in-master-pages-cs/samples/sample2.html)]

コンテンツページがルートフォルダー (`About.aspx`のように) にある場合は、ルートフォルダーを基準とした `Images` サブフォルダーが存在するため、すべてが予期したとおりに動作します。 ただし、コンテンツページがマスターページとは別のフォルダーにある場合は、問題が解消されます。 これを説明するために、`Admin`という名前のサブフォルダーを作成します。 次に、`Default.aspx` という名前のコンテンツページを `Admin` フォルダーに追加し、新しいページを `Site.master` マスターページにバインドします。

> [!NOTE]
> [ *「マスターページでタイトル、メタタグ、およびその他の HTML ヘッダーを指定*](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs.md)する」チュートリアルでは、コンテンツページのタイトルを自動的に設定する `BasePage` という名前のカスタム基本ページクラスを作成しました (明示的に割り当てられていない場合)。 新しく作成されたページの分離コードクラスは、この機能を利用できるように `BasePage` から派生したものであることを忘れないでください。

このコンテンツページを作成した後、ソリューションエクスプローラーは図1のようになります。

![新しいフォルダーと ASP.NET ページがプロジェクトに追加されました](urls-in-master-pages-cs/_static/image1.png)

**図 01**: 新しいフォルダーと ASP.NET ページがプロジェクトに追加された

次に、このレッスンの新しい `<siteMapNode>` エントリを含めるように `Web.sitemap` ファイルを更新します。 次の XML は、完全な `Web.sitemap` マークアップを示しています。これには、3番目の `<siteMapNode>` 要素が追加されています。

[!code-xml[Main](urls-in-master-pages-cs/samples/sample3.xml)]

新しく作成された `Default.aspx` ページには、`Site.master`の4つの ContentPlaceHolders に対応する4つのコンテンツコントロールが必要です。 `MainContent` ContentPlaceHolder を参照するテキストをコンテンツコントロールに追加し、ブラウザーを使用してページにアクセスします。 図2に示すように、ブラウザーは `PoweredByASPNET.gif` イメージファイルを見つけることができません。 ここで何が起こっているんですか。

`~/Admin/Default.aspx` コンテンツ ページには、`About.aspx` ページと同じ HTML が `footerContent` 領域に送信されます。

[!code-html[Main](urls-in-master-pages-cs/samples/sample4.html)]

`<img>` 要素の `src` 属性は相対 URL であるため、ブラウザーは web ページのフォルダーの場所を基準とした `Images` フォルダーの検索を試みます。 つまり、ブラウザーは `Admin/Images/PoweredByASPNET.gif`イメージファイルを探しています。

[PoweredByASPNET .gif イメージファイルが見つからない ![](urls-in-master-pages-cs/_static/image3.png)](urls-in-master-pages-cs/_static/image2.png)

**図 02**: `PoweredByASPNET.gif` イメージファイルが見つからない ([クリックしてフルサイズのイメージを表示する](urls-in-master-pages-cs/_static/image4.png))

### <a name="replacing-relative-urls-with-absolute-urls"></a>相対 Url を絶対 Url に置き換える

相対 URL とは逆に、*絶対 url*です。これは、スラッシュ (`/`) または `http://`などのプロトコルで始まります。 絶対 URL は既知の固定ポイントからリソースの場所を指定するため、web ページのフォルダー構造内の web ページの場所に関係なく、すべての web ページで同じ絶対 URL が有効になります。

図2に示されている壊れた画像を修正するには、相対 URL ではなく絶対 URL を使用するように `<img>` 要素の `src` 属性を更新する必要があります。 正しい絶対 URL を確認するには、web サイトの web ページのいずれかにアクセスして、アドレスバーを確認します。 図2のアドレスバーに示されているように、web アプリケーションへの完全修飾パスは `http://localhost:3908/ASPNET_MasterPages_Tutorial_04_CS/`ます。 そのため、`<img>` 要素の `src` 属性を次の2つの絶対 Url のいずれかに更新することができます。

- `/ASPNET_MasterPages_Tutorial_04_CS/Images/PoweredByASPNET.gif`
- `http://localhost:3908/ASPNET_MasterPages_Tutorial_04_CS/Images/PoweredByASPNET.gif`

前に示した形式のいずれかを使用して、`<img>` 要素の `src` 属性を絶対 URL に更新してから、ブラウザーを使用して `~/Admin/Default.aspx` のページにアクセスします。 今度は、ブラウザーは `PoweredByASPNET.gif` イメージファイルを正しく見つけて表示します (図3を参照)。

[PoweredByASPNET .gif イメージが表示され ![](urls-in-master-pages-cs/_static/image6.png)](urls-in-master-pages-cs/_static/image5.png)

**図 03**: `PoweredByASPNET.gif` イメージが表示されるようになりました ([クリックすると、フルサイズの画像が表示](urls-in-master-pages-cs/_static/image7.png)されます)

絶対 URL のハードコーディングは機能しますが、HTML を web サイトのサーバーとフォルダーの場所と緊密に結合します。これは変更される可能性があります。 `http://localhost:3908/...` フォームの絶対 URL を使用するのは、Visual Studio の組み込みの ASP.NET Development Web サーバーを起動するたびに `localhost` 前のポート番号が自動的に選択されるため、不安定になります。 同様に、`http://localhost` 部分は、ローカルでテストする場合にのみ有効です。 コードが実稼働サーバーに配置されると、URL ベースは `http://www.yourserver.com`のように他のものに変更されます。 また、このアプリケーションのパスが開発サーバーと実稼働サーバーで異なることがよくあるため、フォームの絶対 URL `/ASPNET_MasterPages_Tutorial_04_CS/...` も同じ高まるを持ちます。

ASP.NET は、実行時に有効な相対 URL を生成する方法を提供します。

## <a name="usingandresolveclienturl"></a>`~`と`ResolveClientUrl` の使用

ASP.NET は、絶対 URL をハードコーディングするのではなく、チルダ (`~`) を使用して web アプリケーションのルートを示すことができます。 たとえば、このチュートリアルの前半では、`Admin` フォルダーの `Default.aspx` ページを参照するために、テキストの `~/Admin/Default.aspx` 表記を使用しました。 `~` は、`Admin` フォルダーが web アプリケーションのルートのサブフォルダーであることを示します。

`Control` クラスの[`ResolveClientUrl` メソッド](https://msdn.microsoft.com/library/system.web.ui.control.resolveclienturl.aspx)は、URL を受け取り、そのコントロールが存在する web ページに適した相対 url に変更します。 たとえば、`About.aspx` から `ResolveClientUrl("~/Images/PoweredByASPNET.gif")` を呼び出すと `Images/PoweredByASPNET.gif`が返されます。 ただし、`~/Admin/Default.aspx`から呼び出すと、`../Images/PoweredByASPNET.gif`が返されます。

> [!NOTE]
> すべての ASP.NET サーバーコントロールは `Control` クラスから派生するため、すべてのサーバーコントロールは `ResolveClientUrl` メソッドにアクセスできます。 `Page` クラスは `Control` クラスから派生しています。つまり、ASP.NET ページの分離コードクラスから直接このメソッドを使用できます。

### <a name="usingin-the-declarative-markup"></a>宣言型マークアップでの`~`の使用

いくつかの ASP.NET Web コントロールには、URL 関連のプロパティが含まれています。 HyperLink コントロールには `NavigateUrl` のプロパティがあります。イメージコントロールには `ImageUrl` のプロパティがあります。などなど。 これらのコントロールがレンダリングされると、URL 関連のプロパティ値が `ResolveClientUrl`に渡されます。 そのため、これらのプロパティに web アプリケーションのルートを示す `~` が含まれている場合、URL は有効な相対 URL に変更されます。

ASP.NET サーバーコントロールのみが URL 関連のプロパティで `~` を変換することに注意してください。 `~` が `<img src="~/Images/PoweredByASPNET.gif" />`などの静的な HTML マークアップに表示された場合、ASP.NET エンジンは、HTML コンテンツの残りの部分と共に `~` をブラウザーに送信します。 ブラウザーは、`~` が URL の一部であることを前提としています。 たとえば、ブラウザーがマークアップを受け取ると `<img src="~/Images/PoweredByASPNET.gif" />`、`~` という名前のサブフォルダーと、イメージファイル `PoweredByASPNET.gif`を含むサブフォルダー `Images` があると想定されます。

`Site.master`でイメージマークアップを修正するには、既存の `<img>` 要素を ASP.NET Image Web コントロールに置き換えます。 画像 Web コントロールの `ID` を `PoweredByImage`に、その `ImageUrl` プロパティを `~/Images/PoweredByASPNET.gif`に、その `AlternateText` プロパティを "Powered by ASP.NET!" に設定します。

[!code-aspx[Main](urls-in-master-pages-cs/samples/sample5.aspx)]

マスターページにこの変更を加えた後、[`~/Admin/Default.aspx`] ページにもう一度移動します。 今回は、`PoweredByASPNET.gif` イメージファイルがページに表示されます (図3を参照)。 イメージ Web コントロールがレンダリングされるときには、`ResolveClientUrl` メソッドを使用して、`ImageUrl` プロパティ値を解決します。 `~/Admin/Default.aspx` では、次の HTML ソースのスニペットに示すように、`ImageUrl` が適切な相対 URL に変換されます。

[!code-html[Main](urls-in-master-pages-cs/samples/sample6.html)]

> [!NOTE]
> URL ベースの Web コントロールプロパティで使用されるだけでなく、`Response.Redirect` および `Server.MapPath` メソッドを呼び出すときに、`~` を使用することもできます。 また、必要に応じて、`ResolveClientUrl` メソッドを ASP.NET またはマスターページの宣言型マークアップから直接呼び出すこともできます。[マークアップで `ResolveClientUrl` を使用し](https://www.pluralsight.com/blogs/fritz/archive/2006/02/06/18596.aspx)た[Fritz オニオン](https://www.pluralsight.com/blogs/fritz/)のブログエントリを参照してください。

## <a name="fixing-the-master-pages-remaining-relative-urls"></a>マスターページの残りの相対 Url を修正しています

先ほど修正した `footerContent` の `<img>` 要素に加えて、マスターページには、注意が必要な相対 URL が1つ追加されています。 `topContent` 領域には、`Default.aspx`を示すリンク "マスターページチュートリアル" が含まれています。

[!code-html[Main](urls-in-master-pages-cs/samples/sample7.html)]

この URL は相対 URI であるため、ユーザーがアクセスしているコンテンツページのフォルダー内の `Default.aspx` ページにユーザーを送信します。 このリンクを常にルートフォルダー内の `Default.aspx` をポイントさせるには、`<a>` 要素をハイパーリンク Web コントロールに置き換えて、`~` 表記を使用できるようにする必要があります。

`<a>` 要素マークアップを削除し、その代わりにハイパーリンクコントロールを追加します。 ハイパーリンクの `ID` を `lnkHome`に、その `NavigateUrl` プロパティを `~/Default.aspx`に、その `Text` プロパティを "マスターページチュートリアル" に設定します。

[!code-aspx[Main](urls-in-master-pages-cs/samples/sample8.aspx)]

以上で終わりです。 この時点で、マスターページ内のすべての Url は、マスターページとコンテンツページが配置されているフォルダーに関係なく、コンテンツページによってレンダリングされるときに、適切に基づいています。

### <a name="automatic-url-resolution-in-theheadsection"></a>`<head>`セクションの URL の自動解決

「[*マスターページを使用してサイト全体のレイアウトを作成*](creating-a-site-wide-layout-using-master-pages-cs.md)する」チュートリアルでは、`<head>` 領域の `Styles.css` ファイルに `<link>` を追加しました。

[!code-aspx[Main](urls-in-master-pages-cs/samples/sample9.aspx)]

`<link>` 要素の `href` 属性は相対属性ですが、実行時に自動的に適切なパスに変換されます。 「[*マスターページでタイトル、メタタグ、およびその他の HTML ヘッダーを指定*](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs.md)する」のチュートリアルで説明したように、`<head>` 領域は実際にはサーバー側コントロールであり、レンダリング時に内部コントロールの内容を変更できます。

これを確認するには、[`~/Admin/Default.aspx`] ページに戻って、ブラウザーに送信された HTML ソースを表示します。 次のスニペットに示すように、`<link>` 要素の `href` 属性は、適切な相対 URL `../Styles.css`に自動的に変更されています。

[!code-html[Main](urls-in-master-pages-cs/samples/sample10.html)]

## <a name="summary"></a>要約

マスターページには、多くの場合、リンク、画像、および URL を使用して指定する必要があるその他の外部リソースが含まれます。 マスターページとコンテンツページは同じフォルダー内に存在しない可能性があるため、相対 Url を使用しないように abstain することが重要です。 ハードコーディングされた絶対 Url を使用することもできますが、絶対 URL を web アプリケーションに密に結合します。 Web アプリケーションを移動またはデプロイするときのように絶対 URL が変更された場合は、絶対 url を更新してください。

最適な方法は、ティルダ (`~`) を使用してアプリケーションのルートを示すことです。 URL 関連のプロパティを含む ASP.NET Web コントロールは、実行時にアプリケーションルートに `~` をマップします。 内部的には、Web コントロールは `Control` クラスの `ResolveClientUrl` メソッドを使用して、有効な相対 URL を生成します。 このメソッドはパブリックであり、すべてのサーバーコントロール (`Page` クラスを含む) から使用できます。そのため、必要に応じて、分離コードクラスからプログラムによって使用できます。

プログラミングを楽しんでください。

### <a name="further-reading"></a>関連項目

このチュートリアルで説明しているトピックの詳細については、次のリソースを参照してください。

- [ASP.NET のマスターページ](http://www.odetocode.com/Articles/419.aspx)
- [マスターページでの URL リベース](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/masterpages/default.aspx#urls)
- [マークアップでの `ResolveClientUrl` の使用](https://www.pluralsight.com/blogs/fritz/archive/2006/02/06/18596.aspx)

### <a name="about-the-author"></a>作成者について

1998以降、Microsoft の Web テクノロジを使用して、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(複数の asp/創設者4GuysFromRolla.com の執筆者) が Microsoft の Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 3.5 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 Scott は、 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)またはブログで[http://ScottOnWriting.NET](http://scottonwriting.net/)にアクセスできます。

### <a name="special-thanks-to"></a>ありがとうございました。

今後の MSDN 記事を確認することに興味がありますか? その場合は、 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)の行を削除します。

> [!div class="step-by-step"]
> [前へ](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs.md)
> [次へ](control-id-naming-in-content-pages-cs.md)
