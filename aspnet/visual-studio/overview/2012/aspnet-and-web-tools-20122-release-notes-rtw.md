---
uid: visual-studio/overview/2012/aspnet-and-web-tools-20122-release-notes-rtw
title: ASP.NET and Web Tools 2012.2 リリースノート |Microsoft Docs
author: rick-anderson
description: ASP.NET and Web Tools 2012.2 のリリースノート。
ms.author: riande
ms.date: 02/14/2013
ms.assetid: 9534e58b-1d15-4f1d-b04c-10c79b9d8227
msc.legacyurl: /visual-studio/overview/2012/aspnet-and-web-tools-20122-release-notes-rtw
msc.type: content
ms.openlocfilehash: abd6d8ce0646852a194369589cb730fc98ecb3ad
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78468028"
---
# <a name="aspnet-and-web-tools-20122-release-notes"></a>ASP.NET と Web Tools 2012.2 のリリース ノート

> このドキュメントでは、ASP.NET and Web Tools 2012.2 のリリースについて説明します。 これは、Visual Studio Web ツールと ASP.NET の更新プログラムです。

- [インストールに関する注意事項](#_Installation)
- [ドキュメント](#_Documentation)
- [サポート](#_Support)
- [ソフトウェア要件](#_Software_Requirements)
- [ASP.NET and Web Tools 2012.2 の新機能](#_New_Features_in)

    - [ツール](#_Tooling)
    - [Web 発行](#_Web_Publishing)
    - [ASP.NET MVC テンプレート](#_Templates)
    - [ASP.NET Web API](#_ASP.NET_Web_API)

    - [ASP.NET SignalR](#_ASP.NET_SignalR)
    - [ASP.NET のフレンドリな Url](#_ASP.NET_Friendly_URLs)
- [既知の問題と重大な変更](#_Known_Issues_and)

<a id="_Installation"></a>
## <a name="installation-notes"></a>インストールに関する注意事項

Visual Studio 2012 の ASP.NET and Web Tools 2012.2 は、 [Web Platform installer](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=ASPDOTNETandWebTools2012_2)を使用してインストールできます。 これは、Visual Studio 2012 の更新プログラムまたは Web 用 Visual Studio Express 2012 です。これは必須です。 Visual Studio がインストールされていない場合は、Web 用の Visual Studio Express 2012 がインストールされます。

ASP.NET and Web Tools 2012.2 は手動でインストールすることもできます。 Web 用に Visual Studio 2012 または Visual Studio Express 2012 がインストールされている必要があります。 その後、次の手順を実行します。 

1. ダウンロードセンターから[ASP.NET And Web framework 2012.2](https://download.microsoft.com/download/6/5/6/6562AFBE-9503-4E64-970C-1427133FCD73/AspNetWebTools2012Setup.exe) installer をダウンロードします。
2. メッセージが表示されたら、[実行] をクリックします。 また、後で実行するためにファイルを保存することもできます。
3. 更新する Visual Studio のバージョンを確認します。 これを行うには、更新する Visual Studio を起動します。 次に、[ヘルプ] メニュー項目をクリックします。   
    ![](aspnet-and-web-tools-20122-release-notes-rtw/_static/image1.jpg)
4. Web&quot; の Microsoft Visual Studio 2012 に関する &quot;メニュー項目が表示された場合は、web[開発者ツール 2012.2-Visual Studio Express 2012 For web を](https://go.microsoft.com/fwlink/?LinkID=282228)ダウンロードします。 それ以外[の場合は、Web 開発者ツール 2012.2-Visual Studio 2012](https://go.microsoft.com/fwlink/?LinkID=282228)をダウンロードします。
5. メッセージが表示されたら、[実行] をクリックします。 また、後で実行するためにファイルを保存することもできます。

> [!NOTE]
> ASP.NET and Web Tools 2012.2 リリースには SQL Server Data Tools が含まれていません。 SQL Server と Windows Azure SQL データベースは、オフラインプロジェクトに対応した開発、スキーマ比較、強化されたデータベース配置機能など、豊富なデータベースツールのセットを提供します。 詳細については、SQL Server Data Tools を参照してください[https://go.microsoft.com/fwlink/?LinkID=237127](https://go.microsoft.com/fwlink/?LinkID=237127)を参照してください。

<a id="_Documentation"></a>
## <a name="documentation"></a>ドキュメント

ASP.NET and Web Tools 2012.2 に関するチュートリアルやその他の情報については、ASP.NET Web サイト (https://www.asp.net)を参照してください。

<a id="_Support"></a>
## <a name="support"></a>サポート

ASP.NET and Web Tools 2012.2 は正式にリリースおよびサポートされています。 通常のサポートチャネルを使用できます。 また、ASP.NET フォーラム ([https://forums.asp.net/](https://forums.asp.net/)) に質問を投稿することもできます。 ASP.NET コミュニティのメンバーは、多くの場合、非公式なサポートを提供できます。

<a id="_Software_Requirements"></a>
## <a name="software-requirements"></a>ソフトウェア要件

ASP.NET and Web Tools 2012.2 では、Visual Studio 2012 または Visual Studio Express 2012 for Web が必要です。

<a id="_New_Features_in"></a>
## <a name="new-features-in-aspnet-and-web-tools-20122"></a>ASP.NET and Web Tools 2012.2 の新機能

このセクションでは、ASP.NET and Web Tools 2012.2 リリースで導入された機能について説明します。

<a id="_Tooling"></a>
### <a name="tooling"></a>ツール

- Page Inspector 

    - Page Inspector が、ページに動的に追加された項目を対応する JavaScript コードにマップできるようにする JavaScript 選択のマッピングをサポートします。
    - CSS 更新プログラムをリアルタイムで表示する機能。
    - 詳細については、 [Page Inspector での CSS 自動同期と JavaScript 選択のマッピング](https://blogs.msdn.com/b/webdev/archive/2012/12/14/css-auto-sync-and-javascript-selection-mapping-in-page-inspector.aspx)に関するセクションを参照してください。
- エディター 

    - CoffeeScript、Mustache、ハンドル、および JsRender の構文の強調表示をサポートします。
    - HTML エディターでは、バインドのノックアウトに Intellisense が用意されています。
    - より少ない編集とコンパイラのサポートにより、より少ない方法で動的 CSS を構築できます。
    - JSON を .NET クラスとして貼り付けます。 この特別な貼り付けコマンドを使用してC# json をまたは VB.NET コードファイルに貼り付けると、json から推論される .net クラスが Visual Studio によって自動的に生成されます。
- モバイルエミュレーターのサポートは、サードパーティ製のエミュレーターを VSIX としてインストールできるように、機能拡張フックを追加します。 インストールされているエミュレーターが F5 ドロップダウンに表示されるので、開発者はさまざまなモバイルデバイスで web サイトをプレビューできます。 この機能の詳細について[は、Visual Studio との新しい BrowserStack 統合](http://www.hanselman.com/blog/CrossBrowserDebuggingIntegratedIntoVisualStudioWithBrowserStack.aspx)に関する Scott マン selman のブログ記事をご覧ください。

<a id="_Web_Publishing"></a>
### <a name="web-publishing"></a>Web 公開

- Web サイトプロジェクトでは、Web アプリケーションプロジェクトと同じ発行エクスペリエンスが提供されるようになりました。これには、Windows Azure Web サイトへの発行も含まれます。
- 1つ&#8211;以上のファイルに対して選択的な発行: Web 配置エンドポイントに発行した後で、次の操作を実行できます。 

    - 選択したファイルを発行します。
    - ローカルファイルとリモートファイルの相違点を確認します。
    - リモートファイルでローカルファイルを更新するか、ローカルファイルでリモートファイルを更新してください。

<a id="_Templates"></a>
### <a name="aspnet-mvc-templates"></a>ASP.NET MVC テンプレート

- 新しい Facebook Application テンプレートを使用すると、Facebook Canvas アプリケーションを簡単に作成できます。 いくつかの簡単な手順で、ログイン ユーザーのデータを取得してその友達と統合する Facebook アプリケーションを作成できます。 このテンプレートには、認証、アクセス許可、Facebook データへのアクセスなど、Facebook アプリケーションの作成に必要なすべてのパーツを処理する新しいライブラリが含まれています。 Facebook アプリケーションテンプレートの使用方法の詳細については、「 [https://go.microsoft.com/fwlink/?LinkID=269921](https://go.microsoft.com/fwlink/?LinkID=269921)」を参照してください。
- 新しい Single Page Application MVC テンプレートを使用すると、ASP.NET Web API を基礎にして、HTML 5、CSS 3、および人気のある Knockout ライブラリや jQuery JavaScript ライブラリを使用して対話型のクライアント側 Web アプリケーションを作成できます。 このテンプレートには、RESTful サーバー API を使用する JavaScript HTML5 アプリケーションを構築するための一般的な方法を示す "todo" リストアプリケーションが含まれています。 詳細については、 [https://www.asp.net/single-page-application](../../../single-page-application/index.md)を参照してください。
- 新しいテンプレートを ASP.NET MVC [新しいプロジェクト] ダイアログに追加する VSIX を作成できるようになりました。 詳細については、次を参照してください: [https://go.microsoft.com/fwlink/?LinkId=275019](https://go.microsoft.com/fwlink/?LinkId=275019)
- FixedDisplayModes パッケージ&#8211; mvc プロジェクトテンプレートが更新され、新しい ' Fixeddisplaymodes ' NuGet パッケージが追加されました。これには、mvc 4 のバグの回避策が含まれています。 パッケージに含まれている修正プログラムの詳細については、MVC チームのこちらのブログ記事 ([https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx](https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx)) を参照してください。

<a id="_ASP.NET_Web_API"></a>
### <a name="aspnet-web-api"></a>ASP.NET Web API

ASP.NET Web API は、いくつかの新機能によって強化されています。

- ASP.NET Web API OData
- トレースの ASP.NET Web API
- ASP.NET Web API ヘルプページ

#### <a name="aspnet-web-api-odata"></a>ASP.NET Web API OData

OData ASP.NET Web API は、任意のデータソースに対する豊富なビジネスロジックを使用して OData エンドポイントを構築するために必要な柔軟性を提供します。 OData を ASP.NET Web API すると、公開する OData セマンティクスの量を制御できます。 ASP.NET Web API OData は ASP.NET MVC 4 プロジェクトテンプレートに含まれており、NuGet ([http://www.nuget.org/packages/microsoft.aspnet.webapi.odata](http://www.nuget.org/packages/microsoft.aspnet.webapi.odata)) からも使用できます。

現在、OData ASP.NET Web API は次の機能をサポートしています。

- [クエリ可能] 属性を適用して、OData クエリセマンティクスを有効にします。
- OData クエリを簡単に検証し、サポートされているクエリオプション、演算子、および関数のセットを制限します。
- パラメーターを指定すると、クエリの抽象構文ツリー表現を直接取得して、IQueryable または IEnumerable に検証して適用することができます。
- [クエリ可能] 属性に結果の制限を指定して、サービス主導のページングと次のページリンクの生成を有効にします。
- $Inlinecount を使用して、一致するリソースの合計数をインラインでカウントします。
- Null の伝達を制御します。
- $Filter 内の任意またはすべての演算子。
- Entity data model を規則によって推論するか、Entity Framework コード優先と同様の方法でモデルを明示的にカスタマイズします。
- EntitySetController から派生することによってエンティティセットを公開します。
- ナビゲーションプロパティを公開し、リンクを操作し、OData アクションを実装するための、単純でカスタマイズ可能な規則。
- MapODataRoute 拡張メソッドを使用したルーティングの簡略化。
- 複数の EDM モデルを公開することによるバージョン管理のサポート。
- Web API のクライアント (.NET、Windows Phone、Windows ストアなど) を生成できるように、サービスドキュメントと $metadata を公開します。
- OData Atom、JSON、および JSON の詳細形式のサポート。
- エンティティの作成、更新、部分的な更新 (パッチ) と削除を行います。
- エンティティ間のリレーションシップを照会および操作します。
- ルートに接続するリレーションシップリンクを作成します。
- 複合型。
- エンティティ型の継承。
- コレクションのプロパティ。
- 型.
- OData アクション。
- WCF Data Services と同じ基盤 ([http://www.nuget.org/packages/microsoft.data.odata](http://www.nuget.org/packages/microsoft.data.odata)) に基づいて構築されています。

OData ASP.NET Web API の詳細については、 [https://go.microsoft.com/fwlink/?LinkId=271141](https://go.microsoft.com/fwlink/?LinkId=271141)を参照してください。

#### <a name="aspnet-web-api-tracing"></a>トレースの ASP.NET Web API

ASP.NET Web API のトレースは、Web Api からのトレースデータを .NET トレースと統合します。 これは、Web API プロジェクトテンプレートで既定で有効になっています。 Web Api のトレースデータは [出力] ウィンドウに送信され、IntelliTrace で使用できるようになります。 ASP.NET Web API トレースを使用すると、windows [Azure 診断](https://msdn.microsoft.com/library/windowsazure/hh411529.aspx)との統合によって、windows Azure でホストされている場合に Web API に関する情報をトレースできます。 また、ASP.NET Web API トレース NuGet パッケージ ([http://www.nuget.org/packages/microsoft.aspnet.webapi.tracing](http://www.nuget.org/packages/microsoft.aspnet.webapi.tracing)) を使用して、任意のアプリケーションで ASP.NET Web API トレースをインストールおよび有効にすることもできます。

ASP.NET Web API トレースの構成と使用の詳細については、「 [https://go.microsoft.com/fwlink/?LinkID=269874](https://go.microsoft.com/fwlink/?LinkID=269874)」を参照してください。

#### <a name="aspnet-web-api-help-page"></a>ASP.NET Web API ヘルプページ

ASP.NET Web API ヘルプページは、Web API プロジェクトテンプレートに既定で含まれるようになりました。 ASP.NET Web API のヘルプページでは、HTTP エンドポイント、サポートされている HTTP メソッド、パラメーター、要求および応答メッセージのサンプルペイロードなど、Web Api のドキュメントが自動的に生成されます。 ドキュメントは、コード内のコメントから自動的に取得されます。 また、ASP.NET Web API ヘルプページの NuGet パッケージ ([http://www.nuget.org/packages/microsoft.aspnet.webapi.helppage](http://www.nuget.org/packages/microsoft.aspnet.webapi.helppage)) を使用して、任意のアプリケーションに ASP.NET Web API ヘルプページを追加することもできます。

ASP.NET Web API のヘルプページの設定とカスタマイズの詳細については、「 [https://go.microsoft.com/fwlink/?LinkId=271140](https://go.microsoft.com/fwlink/?LinkId=271140)」を参照してください。

<a id="_ASP.NET_SignalR"></a>
### <a name="aspnet-signalr"></a>ASP.NET SignalR

ASP.NET SignalR を使用すると、使用可能な場合は Websocket を使用して ASP.NET アプリケーションにリアルタイムの web 機能を簡単に追加でき、そうでない場合は自動的に他の手法にフォールバックされます。

ASP.NET SignalR の使用方法の詳細については、「 [https://go.microsoft.com/fwlink/?LinkId=271271](https://go.microsoft.com/fwlink/?LinkId=271271)」を参照してください。

<a id="_ASP.NET_Friendly_URLs"></a>
### <a name="aspnet-friendly-urls"></a>ASP.NET Friendly URL

ASP.NET FriendlyURLs を使用すると、web フォームの開発者は、(.aspx 拡張子を付けずに) わかりやすい Url を生成できます。 構成をほとんど必要とせず、既存の ASP.NET v 4.0 アプリケーションで使用することもできます。 また、FriendlyURLs 機能を使用すると、開発者はデスクトップビューとモバイルビューの切り替えをサポートすることで、モバイルサポートをアプリケーションに簡単に追加できます。

ASP.NET のフレンドリな Url のインストールと使用の詳細については、「 [http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx](http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx)」を参照してください。

<a id="_Known_Issues_and"></a>
## <a name="known-issues-and-breaking-changes"></a>既知の問題と重大な変更

このセクションでは、ASP.NET and Web Tools 2012.2 リリースの既知の問題と重大な変更について説明します。

### <a name="installation-issues"></a>インストールに関する問題

#### <a name="out-of-order-installs-of-visual-studio-2012"></a>Visual Studio 2012 の順不同インストール

ASP.NET and Web Tools 2012.2 をインストールした後に Visual Studio 2012 の追加の SKU をインストールするには、修復操作が必要です。 次の例について考えてみます。

1. Visual Studio 2012 Express for Web のインストール
2. ASP.NET and Web Tools 2012.2 をインストールする
3. Visual Studio 2012 Professional、Premium、または Ultimate のインストール

手順2では、Express for Web の更新プログラムのみがインストールされます。 手順 3. でインストールした追加の SKU に更新プログラムが含まれていることを確認するには、ASP.NET and Web Tools 2012.2 を修復して、最後にインストールされた SKU の更新プログラムをインストールする必要があります。 これは、手順 1. と 3. で Sku を逆にした場合にも適用されます。

#### <a name="installing-microsoft-aspnet-and-web-tools-20122-when-visual-studio-is-open"></a>Visual Studio が開いている場合に Microsoft ASP.NET and Web Tools 2012.2 をインストールする

Microsoft ASP.NET and Web Tools 2012.2 のインストール中に VS が開いている場合、Visual Studio が正常な状態にならないことがあります。 インストールを続行する前に、Visual Studio のすべてのインスタンスを閉じることをお勧めします。

#### <a name="canceling-aspnet-and-web-tools-20122-setup-in-the-middle-of-installation"></a>インストール中に ASP.NET and Web Tools 2012.2 セットアップをキャンセルする

インストールの途中で ASP.NET and Web Tools 2012.2 セットアップをキャンセルすると、Visual Studio が正しくない状態のままになります。 この問題に対処するには、次の手順を実行します。 

- [プログラムの追加と削除] に移動します
- Microsoft ASP.NET and Web Tools 2012.2 をアンインストールします (存在する場合)。
- Microsoft ASP.NET and Web Tools 2012.2 を再インストールする

#### <a name="after-uninstalling-aspnet-and-web-tools-20122-the-aspnet-mvc-4-templates-and-razor-v2-web-site-templates-are-missing"></a>ASP.NET and Web Tools 2012.2 をアンインストールした後、ASP.NET MVC 4 テンプレートと Razor v2 Web サイトテンプレートが見つからない

ASP.NET and Web Tools 2012.2 をアンインストールすると、Visual Studio 2012 から ASP.NET MVC 4 と Razor v2 Web サイトのすべてのテンプレートもアンインストールされます。

回避策として、Visual Studio 2012 のインストールを修復して、ASP.NET MVC 4 および Razor v2 Web サイトテンプレートを再インストールします。

### <a name="tooling-issues"></a>ツールの問題

#### <a name="nuget-error-reported-during-project-creation"></a>プロジェクトの作成中に報告された NuGet エラー

ASP.NET and Web Tools 2012.2 をインストールすると、MVC 4 プロジェクトの作成時に次のエラーが表示される場合があります。

![](aspnet-and-web-tools-20122-release-notes-rtw/_static/image1.png)

ASP.NET and Web Tools 2012.2 は NuGet 2.1 を提供し、Visual Studio 2012 の拡張機能をアップグレードします。 場合によっては、VSIX インストーラーが VSIX を正しく更新できないことがあります。 この問題に対処するには、次の手順を実行します。

1. 管理者として Visual Studio 2012 を起動する
2. ツール-&gt;の拡張機能と更新プログラム にアクセスし、NuGet をアンインストールします。
3. Visual Studio を閉じます。
4. ASP.NET and Web Tools 2012.2 インストールフォルダーに移動します。

    1. Visual Studio 2012 の場合: **NET\ASP.NET Web stack、Visual studio 2012**
    2. Visual Studio 2012 Express for Web の場合:**プログラム NET\ASP.NET web Stack\ Visual Studio Express 2012 For web**
5. Nuget をダブルクリックして、NuGet を再インストールします。

### <a name="web-api-issues"></a>Web API の問題

#### <a name="parsing-issues-in-filter-and-datetime-literals"></a>$filter と DateTime リテラルの解析に関する問題

OData URI パーサーは、部分的な datetime リテラルを正しく解析できません。 たとえば、$filter = start eq datetime ' 2012-12-31T12:00 ' は適切に解析できません。 回避策としては、完全なリテラルを使用します。 $filter = start eq datetime ' 2012-12-31T12:00:00 ' です。

#### <a name="odata-doesnt-support-case-insensitive-property-names"></a>OData は、大文字と小文字を区別しないプロパティ名をサポートしていません。

Odata は、odata クエリと odata パスで大文字と小文字を区別しないプロパティ名をサポートしていません。 Workitem を参照:

- [http://aspnetwebstack.codeplex.com/workitem/366](http://aspnetwebstack.codeplex.com/workitem/366)
- [http://aspnetwebstack.codeplex.com/workitem/704](http://aspnetwebstack.codeplex.com/workitem/704)

Javascript クライアント側とサーバー側で大文字と小文字が異なる場合、この問題が発生する可能性があります。 この問題は、odata プロトコルでの設計によるものです。 ただし、多くのユーザーがこの問題を報告しています。 この問題を回避するには、ユーザーが URL 内のケースを修正する必要があります。

#### <a name="default-odata-routing-conventions-doesnt-support-postput-on-navigation-property"></a>既定の OData ルーティング規則では、ナビゲーションプロパティへのポスト/PUT はサポートされていません。

既定の OData ルーティング規則では、ナビゲーションプロパティへのポスト/PUT はサポートされていません。 「作業項目[http://aspnetwebstack.codeplex.com/workitem/366](http://aspnetwebstack.codeplex.com/workitem/366)」を参照してください。 既定の規則では、この一般的に使用される規則がありません。

この問題を回避するには、ユーザーが新しいルーティング規則を拡張してサポートする必要があります。

### <a name="facebook-template-issues"></a>Facebook テンプレートの問題

#### <a name="facebook-application-template-only-works-using-net-45"></a>Facebook アプリケーションテンプレートは .NET 4.5 を使用してのみ機能します

ASP.NET MVC 4 で Facebook アプリケーションテンプレートを表示するには、[新しいプロジェクト] ダイアログボックスの [framework] ドロップダウンリストで [.NET 4.5] を選択する必要があります。

#### <a name="real-time-update-controller"></a>リアルタイム更新コントローラー

Facebook アプリケーションテンプレートを使用すると、ユーザーは Facebook からのリアルタイム更新を処理する Web API コントローラーを簡単に作成できます。 開発用コンピューターが NAT の背後にある場合は、追加のネットワーク構成を行わないとコントローラーが動作しない可能性があります。 詳細については、こちらを参照してください: [http://facebook.stackoverflow.com/questions/5259467/can-a-computer-behind-a-nat-router-receive-realtime-updates-from-facebook](http://facebook.stackoverflow.com/questions/5259467/can-a-computer-behind-a-nat-router-receive-realtime-updates-from-facebook)

#### <a name="query-string-values-conflict-with-facebook-oauth-parameters"></a>クエリ文字列値が Facebook OAuth パラメーターと競合しています

次のフィールドは、Facebook OAuth dialog のコールバック URL と競合しています。 次の名前を持つ独自のクエリ文字列値を追加しないでください: コード、エラー、エラー\_説明、エラー\_理由。

#### <a name="using-page-inspector-with-facebook-template"></a>Facebook テンプレートでの Page Inspector の使用

Facebook アプリケーションのデバッグ中に、Visual Studio 2012 の Page Inspector 機能を使用することはできません。 Page Inspector は現在 iframe をサポートしていません。

### <a name="single-page-application-template-issues"></a>シングルページアプリケーションテンプレートの問題

#### <a name="with-jquery-19knockout-221-update-when-running-default-mvc-spa-project-new-todo-item-edit-enter-focus-event-is-not-handled-properly"></a>JQuery 1.9/ノックアウト 2.2.1 update では、既定の MVC SPA プロジェクトを実行するときに、新しい todo 項目 edit enter フォーカスイベントは適切に処理されません。

JQuery 1.9/ノックアウト 2.2.1 update を使用すると、既定の MVC SPA プロジェクトを実行するときに、新しい todo 項目を todo リストに入力した後、新しい todo 項目エディットボックスにフォーカスが移動しなくなります。

[http://knockoutjs.com/documentation/hasfocus-binding.html](http://knockoutjs.com/documentation/hasfocus-binding.html)を回避するには、次のサンプルコードと同様の修正を行います。

File todo. モデル .js  
 関数 todolist (データ)、次を追加します。  
 **isSelected = ko (false);**

関数 todoList に、次のブラックテキストを追加します。  
 **isSelected (true);**  
 newTodoTitle (&quot;&quot;);

ファイルブラックに次のテキストを追加します。  
 &lt;フォームデータバインド =&quot;submit: addTodo&quot;&gt;  
 &lt;input class =&quot;addTodo&quot; type =&quot;text&quot; データバインド =&quot;値: newTodoTitle, placeholder: ' Type to add ', blurOnEnter: true, **hasfocus: isSelected**, event: {ぼかし: addtodo}&quot; /&gt;  
 &lt;/&gt;
