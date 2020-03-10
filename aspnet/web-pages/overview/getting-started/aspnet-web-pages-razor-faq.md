---
uid: web-pages/overview/getting-started/aspnet-web-pages-razor-faq
title: ASP.NET Web ページ (Razor) に関する FAQ |Microsoft Docs
author: Rick-Anderson
description: この記事では、ASP.NET Web ページ (Razor) と WebMatrix に関してよく寄せられる質問をいくつか紹介します。 チュートリアルで使用されているソフトウェアのバージョン ASP.NET Web ページ (R...
ms.author: riande
ms.date: 02/07/2014
ms.assetid: b137bd04-25e1-47cb-9d96-ef2e179ecf1f
msc.legacyurl: /web-pages/overview/getting-started/aspnet-web-pages-razor-faq
msc.type: authoredcontent
ms.openlocfilehash: 6fa1b668e915af856a693e79eafb7180ed504dc2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78520654"
---
# <a name="aspnet-web-pages-razor-faq"></a>ASP.NET Web Pages (Razor) FAQ (英語)

[Tom FitzMacken](https://github.com/tfitzmac)

> > [!NOTE] 
> > WebMatrix はASP.NET Webページの統合開発環境としては推奨されなくなりました。 [Visual Studio](xref:aspnet/web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio)または[Visual Studio Code](https://code.visualstudio.com/)を使用します。
>
> この記事では、ASP.NET Web ページ (Razor) と WebMatrix に関してよく寄せられる質問をいくつか紹介します。
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>このチュートリアルで使用されているソフトウェアのバージョン
> 
> 
> - ASP.NET Web ページ (Razor) 3
> - Visual Studio 2013
> - WebMatrix 3
>   
> 
> このチュートリアルは、ASP.NET Web ページ2、WebMatrix 2、および Visual Studio 2012 でも動作します。

- [ASP.NET Web ページ、ASP.NET Web Forms、ASP.NET MVC の違いは何ですか。](#Whats_the_difference_between_ASP.NET_Web_Pages,_ASP.NET_Web_Forms,_and_ASP.NET_MVC)
- [Web ページを操作するために WebMatrix が必要ですか。](#Do_I_need_WebMatrix_in_order_to_work_with_Web_Pages)
- [Web ページページで ASP.NET Web フォームコントロールを使用できますか。](#Can_I_use_ASP.NET_Web_Forms_controls_on_a_Web_Pages_page)
- [WebMatrix を使用せずに ASP.NET Web ページサイトをデプロイすることはできますか。](#Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix)
- [ログインをサポートするには、WebSecurity ヘルパーを使用する必要がありますか。](#Do_I_have_to_use_the_WebSecurity_helper_to_support_logins)
- [HTML5 はサポート ASP.NET Web ページ。](#Does_ASP.NET_Web_Pages_support_HTML5)
- [Web ページで JavaScript と jQuery を使用できますか。](#Can_I_use_JavaScript_and_jQuery_with_Web_Pages)
- [その他のリソース](#AdditionalResources)

エラーおよびその他の問題に関する質問については、 [ASP.NET Web ページ (Razor) のトラブルシューティングガイド](https://go.microsoft.com/fwlink/?LinkId=253001)を参照してください。

<a id="Whats_the_difference_between_ASP.NET_Web_Pages,_ASP.NET_Web_Forms,_and_ASP.NET_MVC"></a>
## <a name="whats-the-difference-between-aspnet-web-pages-aspnet-web-forms-and-aspnet-mvc"></a>ASP.NET Web ページ、ASP.NET Web Forms、ASP.NET MVC の違いは何ですか。

動的な web アプリケーションを作成するための ASP.NET テクノロジは3つあります。

- ASP.NET Web ページは、HTML ページへの動的 (サーバー側) コードおよびデータベースアクセスの追加に焦点を当てており、シンプルで軽量な構文を特徴としています。
- ASP.NET Web フォームは、ページオブジェクトモデルと従来のウィンドウ型コントロール (ボタン、リストなど) に基づいています。 Web フォームでは、クライアントベース (Windows フォーム) 開発に携わっているユーザーにとって使い慣れたイベントベースのモデルを使用します。
- ASP.NET MVC では、ASP.NET のモデルビューコントローラーパターンが実装されています。 「懸念事項の分離」 (処理、データ、および UI レイヤー) に重点を置いています。

3つすべてのフレームワークは完全にサポートされており、ASP.NET チームによる開発は継続されます。 一般に、使用するフレームワークの選択は、ASP.NET の背景と経験によって異なります。

特に ASP.NET Web ページは、HTML を知っているユーザーがページにサーバー処理を追加するのを簡単にするように設計されています。 これは、プログラミングを初めて使用する学生、趣味、一般ユーザーに適した選択肢です。 また、non-ASP.NET web テクノロジを経験している開発者にも適しています。

<a id="Do_I_need_WebMatrix_in_order_to_work_with_Web_Pages"></a>
## <a name="do-i-need-webmatrix-in-order-to-work-with-web-pages"></a>Web ページを操作するために WebMatrix が必要ですか。

いいえ。 WebMatrix はASP.NET Webページの統合開発環境としては推奨されなくなりました。 [Visual Studio](program-asp-net-web-pages-in-visual-studio.md)または[Visual Studio Code](https://code.visualstudio.com/)を使用します。

Visual Studio も Visual Studio Code も使用しない場合は、 [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)を使用してコンポーネント製品を個別にインストールできます。 次の製品が必要です。

- Microsoft .NET Framework 4.5
- ASP.NET MVC 5 (ASP.NET Web ページ framework もインストールする)
- IIS Express (web サーバー)
- Microsoft SQL Server Compact 4.0 (データベース)

テキストエディターを使用して、 *cshtml* (または*vbhtml*) ページを編集できます。

ツールを使用せずに SQL Server Compact データベース ( *.sdf*ファイル) を管理することは少し難しくなります。 Visual Studio には、.sdf データベースを管理するためのツールが*あります*。 コードで SQL コマンドを実行して、多くの SQL Server 管理タスクを実行することもできます。

統合開発環境 (IDE) を使用せずに*cshtml*ページをテストするには、それらをライブサーバーに配置します。 (「 [WebMatrix を使用せずに ASP.NET Web ページサイトをデプロイすることはできますか」を](#Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix)参照してください)。

### <a name="running-iis-express-without-using-an-ide"></a>IDE を使用せずに IIS Express を実行する

IIS Express を web サーバーとしてコンピューターにインストールする場合は、それを使用してページをテストすることができます。 コマンドラインから IIS Express を実行して、特定のポート番号に関連付けることができます。 次に、ブラウザーで*cshtml*ファイルを要求するときに、そのポートを指定します。

Windows で、管理者特権でコマンドプロンプトを開き、 *C:\Program Files\IIS Express*に変更します。 (64 ビットシステムの場合は、 *C:\Program files (x86) \ IIS Express*というフォルダーを使用します。次に、サイトへの実際のパスを使用して、次のコマンドを入力します。

`iisexpress.exe /port:35896 /path:C:\BasicWebSite`

他のプロセスによって既に予約されていない任意のポート番号を使用できます。 (通常、1024を超えるポート番号は無料です)。`path` 値には、 *cshtml*ファイルが格納されている web サイトフォルダーのパスを使用します。

このコマンドを実行してページを提供するように IIS Express を設定した後、ブラウザーを開いて、 *cshtml*ファイルを参照できます。 次のような URL を使用します。

`http://localhost:35896/default.cshtml`

IIS Express のコマンドラインオプションについては、コマンドラインで「`iisexpress.exe /?`」と入力してください。

<a id="Can_I_use_ASP.NET_Web_Forms_controls_on_a_Web_Pages_page"></a>
## <a name="can-i-use-aspnet-web-forms-controls-on-a-web-pages-page"></a>Web ページページで ASP.NET Web フォームコントロールを使用できますか。

いいえ。 [CheckBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.checkbox)コントロール、[検証コントロール](https://msdn.microsoft.com/library/bwd43d0x)、 [GridView](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview)コントロールなどの Web フォームコントロールは、web フォームページ ( *.aspx*ファイル) でのみ機能します。 これらのコントロールには、Web フォームページフレームワークが必要です。

<a id="Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix"></a>
## <a name="can-i-deploy-an-aspnet-web-pages-site-without-using-webmatrix"></a>WebMatrix を使用せずに ASP.NET Web ページサイトをデプロイすることはできますか。

はい。 Web サイトファイルをサーバーに手動でコピーできます (通常は FTP を使用します)。 手動コピーを実行する場合は、SQL Server Compact (データベース) をサポートするファイルもコピーする必要があります。 詳細については、「[ツールを使用しない Web ページアプリケーションのデプロイ](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2317)」のブログ記事を参照してください。

<a id="Do_I_have_to_use_the_WebSecurity_helper_to_support_logins"></a>
## <a name="do-i-have-to-use-the-websecurity-helper-to-support-logins"></a>ログインをサポートするには、WebSecurity ヘルパーを使用する必要がありますか。

いいえ。 ASP.NET Web ページの一部である `SimpleMembership` プロバイダーは、1つのオプションです。 ASP.NET の一部である (Web フォームでの操作に使用する可能性がある) セキュリティプロバイダーも使用できます。 たとえば、Web フォームの場合と同じように ASP.NET Web ページでフォーム認証を使用できます。 フォーム認証を使用する方法の例については、「 [.Net を使用C#して ASP.NET アプリケーションでフォームベースの認証を実装する方法](https://support.microsoft.com/kb/301240)Microsoft サポート」を参照してください。 簡単な例をダウンロードするには、「 [ASP.NET バージョンのログイン &amp; パスワード](http://www.codeguru.com/csharp/.net/net_asp/scripting/article.php/c19295/ASPNET-version-of-Login--Password.htm)」を参照してください。

Windows 認証の使用方法の詳細については、 [ASP.NET Web ページで windows 認証を使用](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2298)するブログの投稿を参照してください。

<a id="Does_ASP.NET_Web_Pages_support_HTML5"></a>
## <a name="does-aspnet-web-pages-support-html5"></a>HTML5 はサポート ASP.NET Web ページ。

はい。 ASP.NET Web ページ (*cshtml*または*vbhtml*ページ) を使用して作成したページは、ページが表示される前に、サーバーで実行されるコードも含む HTML ページです。 ユーザーのブラウザーで HTML5 がサポートされている限り、 *cshtml*または*VBHTML*ページで html5 要素を使用できます。

<a id="Can_I_use_JavaScript_and_jQuery_with_Web_Pages"></a>
## <a name="can-i-use-javascript-and-jquery-with-web-pages"></a>Web ページで JavaScript と jQuery を使用できますか。

そして、 ASP.NET Web ページ (*cshtml*または*vbhtml*ページ) で作成するページは、サーバーコードが含まれた HTML ページにすぎません。 そのため、JavaScript または jQuery を使用して通常の HTML ページで実行できることは、すべて、 *cshtml*または*vbhtml*ページで行うことができます。

WebMatrix の**スターターサイト**テンプレートには、さまざまな jQuery ライブラリが含まれています。 そのテンプレートを使用してサイトを作成した場合、 *Scripts*フォルダーには jquery のコアライブラリ (*jquery-1.6.2)* と、jquery validation (*jquery*など) のライブラリが含まれています。

次に、ASP.NET Web ページで jQuery を使用する方法を説明するブログ記事をいくつか紹介します。

- [WebMatrix を使用した ASP.NET Web ページへの jQuery の追加 (](http://rachelappel.com/jquery/adding-jquery-goodness-to-asp-net-web-pages-using-webmatrix/) Rachel appel)
- [5 分: WebMatrix + JQUERY UI + json + jquery templates](http://joeriks.com/2011/01/30/5-min-webmatrix-jquery-ui-json-jquery-templates/) By Jonas Eriksson
- Mike Brind による[WebMatrix と JQuery Forms](http://mikesdotnetting.com/Article/155/WebMatrix-And-jQuery-Forms)

<a id="AdditionalResources"></a>
## <a name="additional-resources"></a>その他のリソース

[ASP.NET Web ページ (Razor) トラブルシューティング ガイド](https://go.microsoft.com/fwlink/?LinkId=253001)

ASP.NET web サイトの[WebMatrix と ASP.NET Web ページフォーラム](https://forums.asp.net/1224.aspx/1?WebMatrix)
