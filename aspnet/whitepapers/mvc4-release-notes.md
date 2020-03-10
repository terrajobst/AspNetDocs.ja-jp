---
uid: whitepapers/mvc4-release-notes
title: ASP.NET MVC 4 |Microsoft Docs
author: rick-anderson
description: このドキュメントでは、ASP.NET MVC 4 のリリースについて説明します。
ms.author: riande
ms.date: 09/09/2011
ms.assetid: f014524f-25c0-4094-b8e1-886d99536f00
msc.legacyurl: /whitepapers/mvc4-release-notes
msc.type: content
ms.openlocfilehash: b57480bd0274fbb76c600dfb0dd09037bdcbf1e7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78454234"
---
# <a name="aspnet-mvc-4"></a>ASP.NET MVC 4

> このドキュメントでは、ASP.NET MVC 4 のリリースについて説明します。

- [インストールに関する注意事項](#_Toc303253802)
- [ドキュメント](#_Toc303253803)
- [サポート](#_Toc303253804)
- [ソフトウェア要件](#_Toc303253805)
- [ASP.NET MVC 4 の新機能](#_Toc303253807)

    - [ASP.NET Web API](#_Toc317096197)
    - [既定のプロジェクトテンプレートの機能強化](#_Toc303253808)
    - [モバイルプロジェクトテンプレート](#_Toc303253809)
    - [表示モード](#_Toc303253810)
    - [jQuery Mobile、ビュースイッチャー、およびブラウザーのオーバーライド](#_Toc303253811)
    - [非同期コントローラーのタスクサポート](#_Toc303253813)
    - [Azure SDK](#_Toc303253814)
    - [データベースの移行](#_Toc303253818)
    - [空のプロジェクトテンプレート](#_Toc303253819)
    - [コントローラーを任意のプロジェクトフォルダーに追加する](#_Toc303253820)
    - [バンドルと縮小](#_Toc303253821)
    - [OAuth および OpenID を使用した Facebook およびその他のサイトからのログインの有効化](#_Toc303253822)
- [ASP.NET MVC 3 プロジェクトを ASP.NET MVC 4 にアップグレードする](#_Toc303253806)
- [ASP.NET MVC 4 リリース候補からの変更点](#_Toc303253817)
- [既知の問題と重大な変更](#_Toc303253815)

<a id="_Toc303253802"></a>
## <a name="installation-notes"></a>インストールに関する注意事項

ASP.NET MVC 4 for Visual Studio 2010 は、Web Platform Installer を使用して[ASP.NET mvc 4 ホームページ](../mvc/mvc4.md)からインストールできます。

ASP.NET MVC 4 をインストールする前に、以前にインストールした ASP.NET MVC 4 のプレビューをアンインストールすることをお勧めします。 ASP.NET MVC 4 ベータ版とリリース候補版は、アンインストールせずに ASP.NET MVC 4 にアップグレードすることができます。

このリリースは、.NET Framework 4.5 のプレビューリリースと互換性がありません。 ASP.NET MVC 4 をインストールする前に、.NET Framework 4.5 のインストールされているすべてのプレビューリリースを最終バージョンに個別にアップグレードする必要があります。

ASP.NET MVC 4 は、ASP.NET MVC 3 とサイドバイサイドでインストールおよび実行できます。

<a id="_Toc303253803"></a>
## <a name="documentation"></a>ドキュメント

ASP.NET MVC のドキュメントについては、次の URL で MSDN Web サイトを参照してください。

[https://go.microsoft.com/fwlink/?LinkID=243043](https://go.microsoft.com/fwlink/?LinkID=243043)

ASP.NET MVC に関するチュートリアルやその他の情報については、ASP.NET web サイト ([https://www.asp.net/mvc/mvc4](../mvc/mvc4.md)) の mvc 4 ページを参照してください。

<a id="_Toc303253804"></a>
## <a name="support"></a>サポート

ASP.NET MVC 4 は完全にサポートされています。 このリリースの使用に関するご質問がある場合は、ASP.NET MVC フォーラム ([https://forums.asp.net/1146.aspx](https://forums.asp.net/1146.aspx)) に投稿することもできます。 ASP.NET コミュニティのメンバーは、多くの場合、非公式なサポートを提供できます。

<a id="_Toc303253805"></a>
## <a name="software-requirements"></a>ソフトウェア要件

Visual Studio の ASP.NET MVC 4 コンポーネントには、PowerShell 2.0、Visual Studio 2010 Service Pack 1、または Visual Web Developer Express 2010 Service Pack 1 が必要です。

<a id="_Toc303253807"></a>
## <a name="new-features-in-aspnet-mvc-4"></a>ASP.NET MVC 4 の新機能

このセクションでは、ASP.NET MVC 4 リリースで導入された機能について説明します。

<a id="_Toc317096197"></a>
### <a name="aspnet-web-api"></a>ASP.NET Web API

ASP.NET MVC 4 には ASP.NET Web API が含まれています。これは、ブラウザーやモバイルデバイスを含む広範なクライアントに接続できる HTTP サービスを作成するための新しいフレームワークです。 ASP.NET Web API は、RESTful サービスを構築するための最適なプラットフォームでもあります。

ASP.NET Web API には、次の機能のサポートが含まれています。

- **最新の HTTP プログラミングモデル:** 新しい厳密に型指定された HTTP オブジェクトモデルを使用して、Web Api の HTTP 要求と応答に直接アクセスして操作します。 新しい*Httpclient*型を使用して、クライアントで同じプログラミングモデルと HTTP パイプラインを対称的に使用できます。
- **ルートの完全なサポート:** ASP.NET Web API は、ルートパラメーターや制約など、ASP.NET ルーティングのすべてのルート機能をサポートしています。 また、単純な規則を使用して、アクションを HTTP メソッドにマップします。
- **コンテンツネゴシエーション:** クライアントとサーバーは連携して、web API から返されるデータの適切な形式を判断できます。 ASP.NET Web API には、XML、JSON、およびフォームの URL エンコード形式の既定のサポートが用意されています。独自のフォーマッタを追加することによって、このサポートを拡張することも、既定のコンテンツネゴシエーション戦略を置き換えることもできます。
- **モデルのバインドと検証:** モデルバインダーを使用すると、HTTP 要求のさまざまな部分からデータを抽出し、それらのメッセージ部分を .NET オブジェクトに変換して、Web API アクションで使用できるようにすることができます。 検証は、データ注釈に基づいてアクションパラメーターに対しても実行されます。
- **フィルター:** ASP.NET Web API では、 *[承認]* 属性などの既知のフィルターを含むフィルターがサポートされています。 アクション、承認、および例外処理のために、独自のフィルターを作成してプラグインすることができます。
- **クエリの構成:** *IQueryable*を返すアクションでは、 *[クエリ可能]* フィルター属性を使用して、OData クエリ規則を使用した web API のクエリのサポートを有効にします。
- **テストの容易性の向上:** 静的コンテキストオブジェクトで HTTP の詳細を設定するのではなく、web API アクションは*HttpRequestMessage*と*HttpResponseMessage*のインスタンスで動作します。 Web api プロジェクトと共に単体テストプロジェクトを作成して、Web API 機能の単体テストの作成をすぐに開始できるようにします。
- **コードベースの構成:** ASP.NET Web API 構成はコードを使用してのみ実行され、構成ファイルはクリーンになります。 機能拡張ポイントを構成するには、提供されたサービスロケーターパターンを使用します。
- **制御の反転 (IoC) コンテナーのサポートの強化:** ASP.NET Web API は、強化された依存関係競合回避モジュールによる IoC コンテナーの優れたサポートを提供します。
- **自己ホスト:** Web api は、IIS だけでなく、独自のプロセスでホストすることもできます。また、Web API のルートやその他の機能を最大限に活用できます。
- **カスタムヘルプページとテストページを作成する:** 新しい*Iapiexplorer*サービスを使用して web api のカスタムヘルプおよびテストページを簡単に作成できるようになりました。これにより、web api の完全な実行時の説明を取得できます。
- **監視と診断:** ASP.NET Web API は、システム診断、ETW、サードパーティ製のログ記録フレームワークなどの既存のログソリューションと簡単に統合できる軽量なトレースインフラストラクチャを提供するようになりました。 *ITraceWriter*実装を提供し、それを web API 構成に追加することで、トレースを有効にすることができます。
- **リンクの生成:** ASP.NET Web API *Urlhelper*を使用して、同じアプリケーション内の関連リソースへのリンクを生成します。
- **WEB API プロジェクトテンプレート:** 新しい MVC 4 プロジェクトウィザードで新しい Web API プロジェクトを選択すると、ASP.NET Web API をすばやく起動して実行できます。
- **スキャフォールディング:** **[コントローラーの追加]** ダイアログボックスを使用すると、Entity Framework ベースのモデルの種類に基づいて web API コントローラーのスキャフォールディングをすばやく行うことができます。

の詳細については ASP.NET Web API [https://www.asp.net/web-api](../web-api/index.md)を参照してください。

<a id="_Toc303253808"></a>
### <a name="enhancements-to-default-project-templates"></a>既定のプロジェクトテンプレートの機能強化

新しい ASP.NET MVC 4 プロジェクトを作成するために使用されるテンプレートは、最新の web サイトを作成するように更新されました。

![](mvc4-release-notes/_static/image1.png)

表面的な機能強化に加えて、新しいテンプレートの機能が強化されています。 このテンプレートは、デスクトップブラウザーとモバイルブラウザーの両方で適切に表示されるように、アダプティブレンダリングと呼ばれる手法を採用しています。カスタマイズは必要ありません。

![](mvc4-release-notes/_static/image2.png)

アダプティブレンダリングが動作していることを確認するには、モバイルエミュレーターを使用するか、デスクトップブラウザーウィンドウのサイズを小さくしてみてください。 ブラウザーウィンドウのサイズが十分に小さくなると、ページのレイアウトが変わります。

<a id="_Toc303253809"></a>
### <a name="mobile-project-template"></a>モバイルプロジェクトテンプレート

新しいプロジェクトを開始していて、モバイルおよびタブレットのブラウザー専用のサイトを作成する場合は、[新しいモバイルアプリケーション] プロジェクトテンプレートを使用できます。 これは、タッチに最適化された UI を構築するためのオープンソースライブラリである jQuery Mobile に基づいています。

![](mvc4-release-notes/_static/image3.png)

このテンプレートには、インターネットアプリケーションテンプレートと同じアプリケーション構造が含まれています (コントローラーコードは実質的に同じです) が、jQuery Mobile を使用してスタイルを適用し、タッチベースのモバイルデバイスで適切に動作します。 モバイル UI を構造化およびスタイルする方法の詳細については、 [JQuery mobile プロジェクトの web サイト](http://jquerymobile.com/)を参照してください。

モバイル最適化されたビューを追加するデスクトップ指向サイトが既にある場合、またはデスクトップとモバイルのブラウザーに異なるスタイルのビューを提供する1つのサイトを作成する場合は、新しい表示モード機能を使用できます。 (次のセクションを参照してください)。

<a id="_Toc303253810"></a>
### <a name="display-modes"></a>表示モード

新しい表示モード機能を使用すると、アプリケーションは、要求を行っているブラウザーに応じて、ビューを選択できます。 たとえば、デスクトップブラウザーがホームページを要求した場合、アプリケーションは Views\Home\Index.cshtml テンプレートを使用することがあります。 モバイルブラウザーがホームページを要求した場合、アプリケーションは Views\Home\Index.mobile.cshtml テンプレートを返すことがあります。

また、レイアウトとパーシャルは、特定のブラウザーの種類に対してオーバーライドすることもできます。 次に例を示します。

- Views\Shared フォルダーに \_Layout と \_Layout の両方のテンプレートが含まれている場合、既定では、アプリケーションは、モバイルブラウザーからの要求中に \_を使用し、他の要求時には \_を使用します。
- フォルダーに \_MyPartial. cshtml と \_MyPartial.\_の両方が含まれている場合、命令 @Html.Partial("MyPartial") は、モバイルブラウザーからの要求時に MyPartial を表示し、他の要求では MyPartial. cshtml を \_します。\_

他のデバイスの特定のビュー、レイアウト、または部分ビューを作成する場合は、新しい*Defaultdisplaymode*インスタンスを登録して、要求が特定の条件を満たすときに検索する名前を指定できます。 たとえば、次のコードを*アプリケーション\_* の global.asax ファイルに追加して、Apple iPhone ブラウザーが要求を行うときに適用される表示モードとして文字列 "iPhone" を登録することができます。

[!code-csharp[Main](mvc4-release-notes/samples/sample1.cs)]

このコードを実行すると、Apple iPhone ブラウザーが要求を行うときに、アプリケーションで Views\Shared\\_Layout (存在する場合) が使用されます。 表示モードの詳細については、「 [ASP.NET MVC 4 Mobile Features](../mvc/overview/older-versions/aspnet-mvc-4-mobile-features.md)」を参照してください。 DisplayModeProvider を使用するアプリケーションでは、[固定 DisplayModes](http://nuget.org/packages/Microsoft.AspNet.Mvc.FixedDisplayModes) NuGet パッケージをインストールする必要があります。 [ASP.NET フォール2012更新プログラム](https://go.microsoft.com/fwlink/?LinkID=271322)には、新しいプロジェクトテンプレートの[固定 displaymodes](http://nuget.org/packages/Microsoft.AspNet.Mvc.FixedDisplayModes) NuGet パッケージが含まれています。 修正の詳細については、「 [ASP.NET MVC 4 Mobile Cache Bug Fixedd](https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx) 」を参照してください。

<a id="_Toc303253811"></a>
### <a name="jquery-mobile-and-mobile-features"></a>jQuery Mobile とモバイル機能

JQuery Mobile を使用した ASP.NET MVC 4 でのモバイルアプリケーションの構築の詳細については、「チュートリアル[ASP.NET mvc 4 Mobile の機能](../mvc/overview/older-versions/aspnet-mvc-4-mobile-features.md)」を参照してください。

<a id="_Toc303253813"></a>
### <a name="task-support-for-asynchronous-controllers"></a>非同期コントローラーのタスクサポート

*ActionResult&gt;&lt;* *型の*オブジェクトを返す単一のメソッドとして、非同期アクションメソッドを記述できるようになりました。

 詳細については、「 [ASP.NET MVC 4 での非同期メソッドの使用](../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md)」を参照してください。

<a id="_Toc303253814"></a>
### <a name="azure-sdk"></a>Azure SDK

ASP.NET MVC 4 では、Windows Azure SDK の1.6 以降のリリースがサポートされています。

<a id="_Toc303253818"></a>
### <a name="database-migrations"></a>データベースの移行

ASP.NET MVC 4 プロジェクトに Entity Framework 5 が含まれるようになりました。 Entity Framework 5 の優れた機能の1つは、データベースの移行をサポートすることです。 この機能を使用すると、データベース内のデータを保持しながら、コード中心の移行を使用してデータベーススキーマを簡単に拡張できます。 データベースの移行の詳細については、「 [ASP.NET MVC 4 の概要」チュートリアル](../mvc/overview/older-versions/getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4.md)の「[ムービーモデルおよびテーブルに新しいフィールドを追加](../mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-new-field-to-the-movie-model-and-table.md)する」を参照してください。

<a id="_Toc303253819"></a>
### <a name="empty-project-template"></a>空のプロジェクトテンプレート

MVC の空のプロジェクトテンプレートは、完全にクリーンなスレートから始めることができるように、真に空になりました。 空のプロジェクトテンプレートの以前のバージョンは、"Basic" に変更されました。

<a id="_Toc303253820"></a>
### <a name="add-controller-to-any-project-folder"></a>コントローラーを任意のプロジェクトフォルダーに追加する

これで、MVC プロジェクトの任意のフォルダーから右クリックして **[コントローラーの追加]** を選択できるようになりました。 これにより、MVC と Web API コントローラーを別々のフォルダーに保持するなど、必要に応じてコントローラーを柔軟に整理できます。

<a id="_Toc303253821"></a>
### <a name="bundling-and-minification"></a>バンドル化と縮小

バンドルと縮小フレームワークを使用すると、個々のファイルをスクリプトや CSS 用に1つのバンドルされたファイルに結合することによって、Web ページで行う必要がある HTTP 要求の数を減らすことができます。 その後、バンドルの内容を縮小することによって、これらの要求の全体的なサイズを小さくすることができます。 縮小には、変数名を短くするための空白の除去などのアクティビティを含めることができます。これにより、セマンティクスに基づいて CSS セレクターを折りたたむこともできます。 バンドルは、コードで宣言および構成され、バンドルへの単一のリンクを生成するか、または、デバッグ時にバンドルの個々のコンテンツへの複数のリンクを生成するヘルパーメソッドを使用して、ビューで簡単に参照できます。 詳細については[、「バンドルと縮小](../mvc/overview/performance/bundling-and-minification.md)」を参照してください。

<a id="_Toc303253822"></a>
### <a name="enabling-logins-from-facebook-and-other-sites-using-oauth-and-openid"></a>OAuth および OpenID を使用した Facebook およびその他のサイトからのログインの有効化

ASP.NET MVC 4 インターネットプロジェクトテンプレートの既定のテンプレートでは、DotNetOpenAuth ライブラリを使用した OAuth および OpenID ログインがサポートされるようになりました。 OAuth または OpenID プロバイダーの構成の詳細については、ASP.NET Web ページの oauth [/Openid Support For WebForms、MVC、および Web ページ](https://blogs.msdn.com/b/webdev/archive/2012/08/15/oauth-openid-support-for-webforms-mvc-and-webpages.aspx)と[oauth および openid の機能](../web-pages/overview/releases/top-features-in-web-pages-2.md#oauthsetup)に関するドキュメントを参照してください。

<a id="_Toc303253806"></a>
## <a name="upgrading-an-aspnet-mvc-3-project-to-aspnet-mvc-4"></a>ASP.NET  4、ASP.NET MVC 3 プロジェクトをアップグレードします。

ASP.NET MVC 4 は、ASP.NET MVC 3 とサイドバイサイドで同じコンピューターにインストールできます。これにより、ASP.NET MVC 3 アプリケーションを ASP.NET MVC 4 にアップグレードするタイミングを柔軟に選択できます。

アップグレードする最も簡単な方法は、新しい ASP.NET MVC 4 プロジェクトを作成し、既存の MVC 3 プロジェクトのすべてのビュー、コントローラー、コード、コンテンツファイルを新しいプロジェクトにコピーしてから、新しいプロジェクトのアセンブリ参照を更新して、の非 MVC テンプレートに一致させることです。cluded assembiles を使用しています。 MVC 3 プロジェクトの web.config ファイルに変更を加えた場合は、それらの変更を MVC 4 プロジェクトの web.config ファイルにマージする必要もあります。

既存の ASP.NET MVC 3 アプリケーションをバージョン4に手動でアップグレードするには、次の手順を実行します。

1. プロジェクトのすべての web.config ファイル (プロジェクトのルートに1つ、[Views] フォルダーに1つ、プロジェクト内の各領域の [Views] フォルダーにあります) で、次のテキストのすべてのインスタンスを置き換えます (注: System.web、Version = 1.0.0.0 は、にはありません)。Visual Studio 2012 で作成されたプロジェクト: 

    [!code-console[Main](mvc4-release-notes/samples/sample2.cmd)]

    には、次の対応するテキストがあります。

    [!code-console[Main](mvc4-release-notes/samples/sample3.cmd)]
2. ルートの Web.config ファイルで、Web*ページ: Version*要素を "2.0.0.0" に更新し、値 "true" を持つ新しい*PreserveLoginUrl*キーを追加します。 

    [!code-xml[Main](mvc4-release-notes/samples/sample4.xml)]
3. ソリューションエクスプローラーで、[参照] を右クリックし、[NuGet パッケージの管理] を選択します。 左側のウィンドウで、オンライン、**公式パッケージソースの取得** の順に選択し、次の内容を更新します。

    - ASP.NET MVC 4
    - (省略可能) jQuery、jQuery Validation、jQuery UI
    - OptionalEntity Framework
    - (Optonal)Modernizr
4. ソリューションエクスプローラーで、プロジェクト名を右クリックし、[プロジェクトのアンロード] を選択します。 次に、名前をもう一度右クリックし、[ *ProjectName*の編集] を選択します。
5. *Projecttypeguids*要素を見つけ、{E53F8FEA-EAE0-44A6-8774-FFD645390401} を {E3E379DF-F4C6-4180-9B81-6769533ABE47} に置き換えます。
6. 変更を保存し、編集中のプロジェクト (.csproj) ファイルを閉じて、プロジェクトを右クリックし、[プロジェクトの再読み込み] を選択します。
7. 以前のバージョンの ASP.NET MVC を使用してコンパイルされたサードパーティ製のライブラリをプロジェクトが参照する場合は、ルートの Web.config ファイルを開き、*構成*セクションの下に次の3つの*bindingRedirect*要素を追加します。 

    [!code-xml[Main](mvc4-release-notes/samples/sample5.xml)]

<a id="_Toc303253817"></a>
## <a name="changes-from-aspnet-mvc-4-release-candidate"></a>ASP.NET MVC 4 リリース候補からの変更点

ASP.NET MVC 4 リリース候補のリリースノートについては、次を参照してください。

このリリースの ASP.NET MVC 4 リリース候補の主な変更点を次にまとめます。

- **コントローラーごとの構成:** ASP.NET Web API コントローラーは、独自のフォーマッタ、アクションセレクター、およびパラメーターバインダーを設定する*IControllerConfiguration*を実装するカスタム属性を使用して属性を付けることができます。 *Httpコントローラー Configurationattribute*が削除されました。
- **ルートごとのメッセージハンドラー:** 指定されたルートの要求チェーンで、最終的なメッセージハンドラーを指定できるようになりました。 これにより、ルーティングを使用して独自の (非*IHttpController*) エンドポイントにディスパッチすることができます。
- **進行状況の通知:** Progress *Messagehandler*は、アップロードされる要求エンティティとダウンロードされる応答エンティティの両方について、進行状況の通知を生成します。 このハンドラーを使用すると、要求本文をアップロードしたり、応答本文をダウンロードしたりするまでの時間を追跡することができます。
- **プッシュコンテンツ:** *Pushstreamcontent*クラスを使用すると、データプロデューサーがストリームを使用して要求または応答に直接 (同期または非同期で) 書き込むようにするシナリオを実現できます。 *Pushstreamcontent*がデータを受け入れる準備ができたら、出力ストリームを使用してアクションデリゲートを呼び出します。 開発者は、必要に応じてストリームに書き込み、書き込みが完了したらストリームを閉じることができます。 *Pushstreamcontent*は、ストリームの終了を検出し、コンテンツを書き出すための基になる非同期*タスク*を完了します。
- **エラー応答の作成:** *Htterror詳細ポリシー*を引き続き受け入れる一方で、エラー情報を検証エラーや例外などから一貫して表すには、 *httperror*種類を使用します。 新しい*Createerrorresponse*拡張メソッドを使用して、 *httperror*をコンテンツとして含むエラー応答を簡単に作成できます。 *Httperror*内容が完全にネゴシエートされます。
- **削除された MediaRangeMapping:** メディアの種類の範囲が既定のコンテンツ negotiator によって処理されるようになりました。
- **単純型パラメーターの既定のパラメーターバインドは [FromUri] になりました。** 以前のリリースのでは ASP.NET Web API 単純型パラメーターの既定のパラメーターバインドでモデルバインドが使用されていました。 単純型パラメーターの既定のパラメーターバインドは *[Fromuri]* になりました。
- **アクションの選択には、次の必須パラメーターがあります。** URI からのすべての必須パラメーターが指定されている場合にのみ、ASP.NET Web API でのアクションの選択によってアクションが選択されるようになりました。 アクションメソッドシグネチャに引数の既定値を指定することで、パラメーターを省略可能として指定できます。
- **HTTP パラメーターバインドのカスタマイズ:** *Parameterbindingattribute*を使用して、特定のアクションパラメーターのパラメーターバインドをカスタマイズするか、 *Httpconfiguration*で*parameterbindingrを*使用してパラメーターバインドをより広範囲にカスタマイズします。
- **MediaTypeFormatter の機能強化:** フォーマッタは、完全な*Httpcontent*インスタンスにアクセスできるようになりました。
- **ホストのバッファリングポリシーの選択:** ASP.NET Web API で*IHostBufferPolicySelector*サービスを実装して構成し、ホストがバッファリングを使用するときのポリシーを決定できるようにします。
- **ホストに依存しない方法でクライアント証明書にアクセスする:** *GetClientCertificate*拡張メソッドを使用して、要求メッセージから指定されたクライアント証明書を取得します。
- **コンテンツネゴシエーションの拡張性:** *DefaultContentNegotiator*から派生することによってコンテンツネゴシエーションをカスタマイズし、必要なコンテンツネゴシエーションのあらゆる側面をオーバーライドします。
- **406 を返すことのサポートは受け入れられません。** *Excludematchontypeonly*パラメーターを*true*に設定して*DefaultContentNegotiator*を作成することによって適切なフォーマッタが見つからない場合、ASP.NET Web API で許容できない406の応答を返すことができるようになりました。
- **フォームデータを NameValueCollection または JToken として読み取ります。** *Parsequerystring*および*Readasformdataasync*拡張メソッドを使用して、URI クエリ文字列または要求本文のフォームデータを*NameValueCollection*として読み取ることができます。 同様に、URI クエリ文字列または要求本文のフォームデータは、それぞれ*Tryreadqueryasjson*と*readasasync*&lt;t&gt; 拡張メソッドを使用して、 *jtoken*として読み取ることができます。
- **マルチパートの機能強化:** MIME マルチパートデータの種類に合わせて完全に調整され、ユーザーに最適な方法で結果を表示できる*Multipartstreamprovider*を作成できるようになりました。 また、*マルチパート Streamprovider*で処理後の手順をフックすることもできます。これにより、実装は、MIME マルチパートのボディ部で必要なすべてのポスト処理を実行できます。 たとえば、 *Multipartformdatastreamprovider*実装は HTML フォームデータパーツを読み取り、 *NameValueCollection*に追加します。これにより、呼び出し元から簡単に取得できるようになります。
- **リンク生成の機能強化:** *Urlhelper*は*httpコントローラーコンテキスト*に依存しなくなりました。 これで、 *HttpRequestMessage*が使用可能な任意のコンテキストから*urlhelper*にアクセスできるようになりました。
- **メッセージハンドラーの実行順序の変更:** メッセージハンドラーは、逆の順序ではなく、構成されている順序で実行されるようになりました。
- **メッセージハンドラーを接続するためのヘルパー:** *Delegatinghandlerelementcollection*に接続し、目的のパイプラインを使用して*httpclient*を作成できる新しい*HttpClientFactory* 。 また、代替の内部ハンドラー (既定では*Httpclienthandler*) を使用して接続する機能に加えて、 *httpmessage呼び出し*元または*httpclient*ではなく、別の*DelegatingHandler*を上位の呼び出し元として使用する場合の接続を行います。
- **ASP.NET Web 最適化での CDNs のサポート:** ASP.NET Web Optimization では CDN 代替パスがサポートされるようになりました。これにより、各バンドルに対して、コンテンツ配信ネットワーク上の同じリソースを指す追加の URL を指定できるようになります。 CDNs をサポートすることで、スクリプトとスタイルのバンドルを、Web アプリケーションのエンドコンシューマーに地理的に近づけることができます。 CDN が使用できない場合は、運用アプリでフォールバックを実装する必要があります。 フォールバックをテストします。
- **ASP.NET Web API のルートと構成は、テストコードで使用できる*webapiconfig.cs*静的メソッドに移動されました。** 以前に ASP.NET Web API ルートは、標準の MVC ルートと共に*RouteConfig RegisterRoutes*に追加されました。 既定の ASP.NET Web API のルートと構成は、テストを容易にするために別の*webapiconfig.cs*メソッドで処理されるようになりました。

<a id="_Toc303253815"></a>
## <a name="known-issues-and-breaking-changes"></a>既知の問題と重大な変更

- **ASP.NET MVC 4 の RC および RTM バージョンは、モバイルビューを返す必要があるときに、誤ってキャッシュされたデスクトップビューを返しました。**

    - 修正の詳細については、「 [ASP.NET MVC 4 Mobile Cache Bug Fixed](https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx) 」を参照してください。 修正プログラムは、[固定 DisplayModes](http://nuget.org/packages/Microsoft.AspNet.Mvc.FixedDisplayModes) NuGet パッケージからインストールできます。
- **Razor ビューエンジンでの重大な変更**。 次の型は、 *system.web*から削除されました。 

    - *ModelSpan*
    - *MvcVBRazorCodeGenerator*
    - *MvcCSharpRazorCodeGenerator*
    - *MvcVBRazorCodeParser*

  次のメソッドも削除されました。 

    - *MvcCSharpRazorCodeParser (System.web..... パーサー. CodeBlockInfo)*
    - *MvcWebPageRazorHost (RazorCodeGenerator) のようになります。*
    - *MvcVBRazorCodeParser (System.web..... パーサー. CodeBlockInfo)*
- **ASP.NET MVC 4 アプリの/bin ディレクトリに WebData が含まれている場合、フォーム認証の URL が引き継がれます。** WebData アセンブリをアプリケーションに追加する ([配置可能な依存関係の追加] ダイアログボックスを使用して [Razor 構文を使用する] を ASP.NET Web ページ選択するなど) と、既定の ASP.NET MVC アカウントコントローラーによって想定されているように、/account/ログインではなく、認証ログインリダイレクトがオーバーライドされます。 この動作を回避し、web.config の認証セクションに既に指定されている URL を使用するには、PreserveLoginUrl という名前の appSetting を追加し、それを true に設定します。 

    [!code-xml[Main](mvc4-release-notes/samples/sample6.xml)]
- **Visual Studio 2010 と Visual Web Developer 2010 をサイドバイサイドでインストールするために ASP.NET MVC 4 をインストールしようとすると、NuGet パッケージマネージャーのインストールが失敗します。** Visual Studio 2010 と Visual Web Developer 2010 を ASP.NET MVC 4 とサイドバイサイドで実行するには、Visual Studio の両方のバージョンが既にインストールされていると、ASP.NET MVC 4 をインストールする必要があります。
- **前提条件が既にアンインストールされている場合、ASP.NET MVC 4 のアンインストールは失敗します。** ASP.NET MVC 4you 正常にアンインストールするには、Visual Studio をアンインストールする前に ASP.NET MVC 4 をアンインストールする必要があります。
- **ASP.NET MVC 4 をインストールすると、ASP.NET MVC 3 RTM アプリケーションが中断します。** RTM リリース ( [ASP.NET mvc 3 Tools Update](https://www.microsoft.com/download/details.aspx?id=1491)リリースではない) で作成された ASP.NET mvc 3 アプリケーションでは、ASP.NET MVC 4 とサイドバイサイドで動作するために次の変更が必要です。 これらの更新を行わずにプロジェクトをビルドすると、コンパイルエラーになります。 

    **必要な更新プログラム**

  1. ルートの Web.config ファイルで、新しい *&lt;appSettings&gt;* エントリを追加します。このキー*ページ*には、バージョンと値*1.0.0.0*があります。 

      [!code-xml[Main](mvc4-release-notes/samples/sample7.xml)]
  2. ソリューションエクスプローラーで、プロジェクト名を右クリックし、[プロジェクトのアンロード] を選択します。 次に、名前をもう一度右クリックし、[ *ProjectName*の編集] を選択します。
  3. 次のアセンブリ参照を見つけます。 

      [!code-xml[Main](mvc4-release-notes/samples/sample8.xml)]

      次のように置き換えます。

      [!code-xml[Main](mvc4-release-notes/samples/sample9.xml)]
  4. 変更を保存し、編集中のプロジェクト (.csproj) ファイルを閉じてから、プロジェクトを右クリックして [再読み込み] を選択します。

- **4.5 から4.0 をターゲットとするように ASP.NET MVC 4 プロジェクトを変更しても、EntityFramework アセンブリ参照は更新されません。** 4.5 をターゲットにした後、ASP.NET MVC 4 プロジェクトを4.0 ターゲットに変更すると、EntityFramework アセンブリへの参照は引き続き4.5 バージョンを指します。 この問題を解決するには、EntityFramework NuGet パッケージをアンインストールしてから再インストールします。
- **403 をターゲット4.0 から4.5 に変更した後、Azure で ASP.NET MVC 4 アプリケーションを実行しているときには許可されません。** 4.5 をターゲットにしてから Azure にデプロイした後、ASP.NET MVC 4 プロジェクトを4.0 ターゲットに変更すると、実行時に403の禁止エラーが表示されることがあります。 この問題を回避するには、次の内容を web.config: `<modules runAllManagedModulesForAllRequests="true" />` に追加します。
- **Razor ファイルの文字列リテラルに '\' を入力すると、Visual Studio 2012 がクラッシュします。** この問題を回避するには、最初に文字列リテラルの終わりの引用符を入力します。
- <strong>インターネットテンプレートで &quot;Account/Manage&quot; を参照すると、CHS、CHT、および言語のランタイムエラーが発生します。</strong> この問題を修正するには、ページを<em>&lt;strong&gt;</em>タグ内の唯一のコンテンツとして配置して<em>@User.Identity.Name</em>を分離するように変更します。
- **Google および LinkedIn プロバイダーは、Azure Websites 内ではサポートされていません。** Azure Websites にデプロイするときに、別の認証プロバイダーを使用します。
- **IIS 8 Express/IIS で UriPathExtensionMapping を使用すると、拡張機能を使用しようとすると、404が見つからないことを通知するメッセージが表示されます。** 静的ファイルハンドラーは、 *Uripathextensionmappings*を使用する web api への要求に干渉します。 この問題を回避するには、web.config で*Runallmanagedモジュール Forallrequests = true*を設定します。
- **Controller. Execute メソッドは呼び出されなくなりました。** すべての MVC コントローラーは、常に非同期的に実行されるようになりました。
