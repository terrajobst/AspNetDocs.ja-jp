---
uid: visual-studio/overview/2013/release-notes
title: Visual Studio 2013 リリースノートの ASP.NET and Web Tools |Microsoft Docs
author: microsoft
description: このドキュメントでは、Visual Studio 2013 の ASP.NET and Web Tools のリリースについて説明します。
ms.author: riande
ms.date: 10/17/2013
ms.assetid: 08815768-2702-42ae-ae85-0a59934a11d1
msc.legacyurl: /visual-studio/overview/2013/release-notes
msc.type: authoredcontent
ms.openlocfilehash: d8af9c8e7ee1316a5eac90c5959d07c628154e09
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449524"
---
# <a name="aspnet-and-web-tools-for-visual-studio-2013-release-notes"></a>Visual Studio 2013 の ASP.NET と Web ツールのリリース ノート

[Microsoft](https://github.com/microsoft)

> このドキュメントでは、Visual Studio 2013 の ASP.NET and Web Tools のリリースについて説明します。

## <a name="contents"></a>内容

- [インストールに関する注意事項](#TOC1)
- [ドキュメント](#TOC2)
- [ソフトウェア要件](#TOC4)

### <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-2013"></a>Visual Studio 2013 の ASP.NET and Web Tools の新機能

- [1つの ASP.NET](#TOC6)
- [新しい Web プロジェクトのエクスペリエンス](#newproj)
- [ASP.NET スキャフォールディング](#scaffold)
- [ブラウザー リンク](#browser-link)
- [Visual Studio Web エディターの機能強化](#web-editor)
- [Visual Studio での Azure App Service Web Apps のサポート](#waws)
- [Web 発行の機能強化](#publish)
- [NuGet 2.7](#nuget)
- [ASP.NET Web フォーム](#TOC9)
- [ASP.NET MVC 5](#TOC10)
- [ASP.NET Web API 2](#TOC11)
- [ASP.NET SignalR](#TOC13)
- [ASP.NET Identity](#TOC8)
- [Microsoft OWIN コンポーネント](#TOC7)
- [Entity Framework 6](#ef6)
- [ASP.NET Razor 3](#TOC14)
- [ASP.NET アプリの中断](#TOC15)
- [既知の問題と重大な変更](#knownissues)

<a id="TOC1"></a>
## <a name="installation-notes"></a>インストールに関する注意事項

Visual Studio 2013 の ASP.NET and Web Tools はメインインストーラーにバンドルされており、[ここで](https://www.asp.net/downloads)ダウンロードできます。

<a id="TOC2"></a>
## <a name="documentation"></a>ドキュメント

[ASP.NET の Web サイト](https://www.asp.net/)から、Visual Studio 2013 の ASP.NET and Web Tools に関するチュートリアルやその他の情報を入手できます。

<a id="TOC4"></a>
## <a name="software-requirements"></a>ソフトウェア要件

ASP.NET and Web Tools には Visual Studio 2013 が必要です。

<a id="TOC5"></a>
## <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-2013"></a>Visual Studio 2013 の ASP.NET and Web Tools の新機能

以下のセクションでは、リリースで導入された機能について説明します。

<a id="TOC6"></a>
## <a name="one-aspnet"></a>One ASP.NET

Visual Studio 2013 のリリースでは、ASP.NET テクノロジの使用経験を統合するための手順を実行しました。これによって、必要なものを簡単に組み合わせることができます。 たとえば、MVC を使用してプロジェクトを開始し、後で web フォームページをプロジェクトに簡単に追加したり、web フォームプロジェクトのスキャフォールディング Web Api を追加したりすることができます。 ASP.NET の1つは、ASP.NET で気に入っていることを開発者が簡単に実行できるようにすることです。 どのテクノロジを選択した場合でも、1つの ASP.NET の信頼された基盤となるフレームワークを使用して、自信を持って構築できます。

<a id="newproj"></a>
## <a name="new-web-project-experience"></a>新しい Web プロジェクトのエクスペリエンス

Visual Studio 2013 で新しい web プロジェクトを作成するためのエクスペリエンスが向上しました。 **[New ASP.NET Web プロジェクト]** ダイアログでは、必要なプロジェクトの種類を選択したり、テクノロジ (web フォーム、MVC、web API) の任意の組み合わせを構成したり、認証オプションを構成したり、単体テストプロジェクトを追加したりすることができます。

![新しい ASP.NET プロジェクト](release-notes/_static/image1.png)

新しいダイアログボックスでは、多くのテンプレートの既定の認証オプションを変更できます。 たとえば、ASP.NET Web フォームプロジェクトを作成するときに、次のいずれかのオプションを選択できます。

- [認証なし]
- 個々のユーザーアカウント (ASP.NET メンバーシップまたはソーシャルプロバイダーのログイン)
- 組織アカウント (インターネットアプリケーションの Active Directory)
- Windows 認証 (イントラネットアプリケーションでの Active Directory)

![認証オプション](release-notes/_static/image2.png)

Web プロジェクトを作成するための新しいプロセスの詳細については、「 [Visual Studio 2013 での ASP.NET Web プロジェクトの作成](creating-web-projects-in-visual-studio.md)」を参照してください。 新しい認証オプションの詳細については、このドキュメントの後半の「 [ASP.NET Identity](#TOC8) 」を参照してください。

<a id="scaffold"></a>
## <a name="aspnet-scaffolding"></a>ASP.NET スキャフォールディング

ASP.NET スキャフォールディングは、ASP.NET Web アプリケーションのコード生成フレームワークです。 これにより、データモデルと対話する定型コードをプロジェクトに簡単に追加できるようになります。

以前のバージョンの Visual Studio では、スキャフォールディングは ASP.NET MVC プロジェクトに限定されていました。 Visual Studio 2013 では、Web フォームを含む任意の ASP.NET プロジェクトにスキャフォールディングを使用できるようになりました。 Visual Studio 2013 は、現在、Web フォームプロジェクトのページの生成をサポートしていませんが、MVC の依存関係をプロジェクトに追加することで、Web フォームでスキャフォールディングを使用できます。 Web フォームのページ生成のサポートは、今後の更新プログラムで追加される予定です。

スキャフォールディングを使用する場合は、必要なすべての依存関係がプロジェクトにインストールされていることを確認します。 たとえば、ASP.NET の Web フォームプロジェクトから開始し、スキャフォールディングを使用して Web API コントローラーを追加すると、必要な NuGet パッケージと参照がプロジェクトに自動的に追加されます。

MVC スキャフォールディングを Web フォームプロジェクトに追加するには、**新しいスキャフォールディング項目**を追加し、ダイアログウィンドウで **[Mvc 5 の依存関係]** を選択します。 MVC のスキャフォールディングには、2つのオプションがあります。最小と完全。 [最小] を選択すると、ASP.NET MVC の NuGet パッケージと参照のみがプロジェクトに追加されます。 [完全] オプションを選択した場合は、最小の依存関係だけでなく、MVC プロジェクトに必要なコンテンツファイルが追加されます。

非同期コントローラーのスキャフォールディングのサポートには、Entity Framework 6 の新しい非同期機能が使用されます。

詳細とチュートリアルについては、「 [ASP.NET スキャフォールディングの概要](aspnet-scaffolding-overview.md)」を参照してください。

<a id="browser-link"></a>
## <a name="browser-link--signalr-channel-between-browser-and-visual-studio"></a>Browser Link – browser と Visual Studio の間の SignalR チャネル

新しい[ブラウザーリンク](using-browser-link.md)機能を使用すると、複数のブラウザーを Visual Studio に接続し、ツールバーのボタンをクリックしてすべてを更新できます。 モバイルエミュレーターを含む複数のブラウザーを開発サイトに接続し、[更新] をクリックすると、すべてのブラウザーを同時に更新できます。 ブラウザーリンクでは、開発者がブラウザーリンク拡張機能を作成できるようにする API も公開されています。

![](release-notes/_static/image3.png)

開発者が Browser Link API を利用できるようにすることで、Visual Studio と接続されている任意のブラウザーの間の境界を越える非常に高度なシナリオを作成できるようになります。 Web Essentials は API を利用して、Visual Studio とブラウザーの開発者ツールの間に統合されたエクスペリエンスを作成し、モバイルエミュレーターをリモートで制御します。

<a id="web-editor"></a>
## <a name="visual-studio-web-editor-enhancements"></a>Visual Studio Web エディターの機能強化

Visual Studio 2013 には、Razor ファイル用の新しい HTML エディターと、web アプリケーションの HTML ファイルが含まれています。 新しい HTML エディターには、HTML5 に基づく単一の統合スキーマが用意されています。 これには、かっこの自動補完、jQuery UI と AngularJS 属性の IntelliSense、属性の IntelliSense のグループ化、ID とクラス名の Intellisense、およびパフォーマンスの向上、書式設定、およびスマートタグの追加などの機能強化が含まれています。

次のスクリーンショットは、HTML エディターでブートストラップ属性の IntelliSense を使用する方法を示しています。

![HTML エディターでの Intellisense](release-notes/_static/image4.png)

また Visual Studio 2013 には、CoffeeScript と LESS エディターの両方が組み込まれています。 LESS エディターには、CSS エディターのすべての優れた機能が用意されており、@import チェーン内のすべてのドキュメントにわたって、変数と mixin のための特定の Intellisense が用意されています。

<a id="waws"></a>
## <a name="azure-app-service-web-apps-support-in-visual-studio"></a>Visual Studio での Azure App Service Web Apps のサポート

Azure SDK for .NET 2.2 の Visual Studio 2013 では、**サーバーエクスプローラー**を使用してリモート web アプリと直接やり取りできます。 Azure アカウントにサインインしたり、新しい web アプリを作成したり、アプリを構成したり、リアルタイムログを表示したりできます。 SDK 2.2 がリリースされるとすぐに、Azure でリモートでデバッグモードで実行できるようになります。 Azure App Service Web Apps の新機能のほとんどは、Azure SDK for .NET の現在のリリースをインストールするときに Visual Studio 2012 でも動作します。

詳細については、次のリソースを参照してください。

- [Azure App Service で ASP.NET web アプリを作成する](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/)
- [Visual Studio を使用した Azure App Service での Web アプリのトラブルシューティング](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/)

<a id="publish"></a>
## <a name="web-publish-enhancements"></a>Web 発行の機能強化

Visual Studio 2013 には、Web 公開の新機能と強化された機能が含まれています。 いくつかを次に示します。

- Web.config[ファイルの暗号化](https://go.microsoft.com/fwlink/?LinkId=325529)を簡単に自動化できます。 (このリンクと、次の2つのポイントは、10/17 の当日に予定されていない可能性がある MSDN のドキュメントを示しています)。
- [デプロイ中にアプリケーションをオフラインにする操作を](https://go.microsoft.com/fwlink/?LinkId=325530)簡単に自動化できます。
- サーバーにコピーするファイルを決定するために、[最終更新日ではなくファイルチェックサムを使用](https://go.microsoft.com/fwlink/?LinkId=325531)するように Web 配置を構成します。
- FTP またはファイルシステムの発行方法を使用している場合は、(Web.config を含む) 個々の選択したファイルをすばやく発行します。また、Web 配置を使用することもできます。

ASP.NET web デプロイの詳細については、 [ASP.NET サイト](https://go.microsoft.com/fwlink/?LinkId=322027)を参照してください。

<a id="nuget"></a>
## <a name="nuget-27"></a>NuGet 2.7

NuGet 2.7 には新機能の豊富なセットが含まれています。詳細については、「 [nuget 2.7 のリリースノート](http://docs.nuget.org/docs/release-notes/nuget-2.7)」を参照してください。

このバージョンの NuGet では、パッケージをダウンロードするために NuGet のパッケージ復元機能に明示的に同意する必要もなくなります。 NuGet をインストールすることにより、同意 (および NuGet の [基本設定] ダイアログの関連するチェックボックス) が許可されるようになりました。 既定では、パッケージの復元が正常に機能するようになりました。

<a id="TOC9"></a>
## <a name="aspnet-web-forms"></a>ASP.NET Web Forms

### <a name="one-aspnet"></a>One ASP.NET

Web フォームプロジェクトテンプレートは、新しい1つの ASP.NET エクスペリエンスとシームレスに統合されます。 Web フォームプロジェクトに MVC と Web API のサポートを追加できます。また、ASP.NET プロジェクト作成ウィザードを使用して認証を構成することもできます。 詳細については、「 [Visual Studio 2013 での ASP.NET Web プロジェクトの作成](creating-web-projects-in-visual-studio.md)」を参照してください。

### <a name="aspnet-identity"></a>ASP.NET Identity

Web フォームプロジェクトテンプレートでは、新しい ASP.NET Identity framework がサポートされています。 さらに、テンプレートでは、Web フォームイントラネットプロジェクトの作成がサポートされるようになりました。 詳細については、「 **Visual Studio 2013 での ASP.NET Web プロジェクトの作成**」の[認証方法](creating-web-projects-in-visual-studio.md#auth)に関する説明を参照してください。

### <a name="bootstrap"></a>ブートストラップ

Web フォームテンプレートでは、[ブートストラップ](http://twitter.github.io/bootstrap/)を使用して、外観と応答性が向上し、簡単にカスタマイズできます。 詳細については、 [Visual Studio 2013 web プロジェクトテンプレート](creating-web-projects-in-visual-studio.md#bootstrap)の「ブートストラップ」を参照してください。

<a id="TOC10"></a>
## <a name="aspnet-mvc-5"></a>ASP.NET MVC 5

### <a name="one-aspnet"></a>One ASP.NET

Web MVC プロジェクトテンプレートは、新しい1つの ASP.NET エクスペリエンスとシームレスに統合されます。 1つの ASP.NET プロジェクト作成ウィザードを使用して、MVC プロジェクトをカスタマイズし、認証を構成することができます。 MVC 5 を ASP.NET する入門用のチュートリアルについては、「 [ASP.NET mvc 5 を使用](../../../mvc/overview/getting-started/introduction/getting-started.md)したはじめに」を参照してください。

Mvc 4 プロジェクトを MVC 5 にアップグレードする方法については、「 [ASP.NET mvc 4 と WEB Api プロジェクトを ASP.NET mvc 5 および WEB api 2 にアップグレードする方法](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md)」を参照してください。

### <a name="aspnet-identity"></a>ASP.NET Identity

MVC プロジェクトテンプレートは、認証と id 管理に ASP.NET Identity を使用するように更新されました。 Facebook と Google の認証および新しいメンバーシップ API を使用するチュートリアルについては、「 [facebook と Google OAuth2 を使用した ASP.NET mvc 5 アプリの作成](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)」と「[認証と SQL DB を使用した ASP.NET mvc アプリ](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/)の作成」と「Azure App Service へのデプロイ」を参照してください。

### <a name="bootstrap"></a>ブートストラップ

MVC プロジェクトテンプレートは、[ブートストラップ](http://getbootstrap.com/)を使用するように更新され、簡単にカスタマイズできる外観と応答性を備えています。 詳細については、 [Visual Studio 2013 web プロジェクトテンプレート](creating-web-projects-in-visual-studio.md#bootstrap)の「ブートストラップ」を参照してください。

### <a name="authentication-filters"></a>認証フィルター

認証フィルターは、ASP.NET MVC の新しい種類のフィルターで、ASP.NET MVC パイプラインの承認フィルターの前に実行されます。また、アクションごと、コントローラー単位、またはすべてのコントローラーに対してグローバルに認証ロジックを指定できます。 認証フィルターは、要求内の資格情報を処理し、対応するプリンシパルを指定します。 認証フィルターでは、承認されていない要求に応答して認証チャレンジを追加することもできます。

### <a name="filter-overrides"></a>フィルターのオーバーライド

オーバーライドフィルターを指定することにより、特定のアクションメソッドまたはコントローラーに適用するフィルターを上書きできるようになりました。 上書きフィルターでは、特定のスコープ (action または controller) に対して実行しないフィルターの種類のセットを指定します。 これにより、グローバルに適用されるフィルターを構成してから、特定のグローバルフィルターを特定のアクションまたはコントローラーに適用しないようにすることができます。

### <a name="attribute-routing"></a>属性ルーティング

ASP.NET MVC は、 [http://attributerouting.net](http://attributerouting.net)の作成者である Tim mccall による貢献のおかげで、属性ルーティングをサポートするようになりました。 属性ルーティングを使用すると、アクションとコントローラーに注釈を付けることによって、ルートを指定できます。

<a id="TOC11"></a>
## <a name="aspnet-web-api-2"></a>ASP.NET Web API 2

### <a name="attribute-routing"></a>属性ルーティング

ASP.NET Web API は、 [http://attributerouting.net](http://attributerouting.net)の作成者である Tim mccall による貢献のおかげで、属性ルーティングをサポートするようになりました。 属性ルーティングでは、次のようにアクションとコントローラーに注釈を付けることで、Web API のルートを指定できます。

[!code-csharp[Main](release-notes/samples/sample1.cs)]

属性ルーティングを使用すると、web API の Uri をより詳細に制御できます。 たとえば、1つの API コントローラーを使用してリソース階層を簡単に定義できます。

[!code-csharp[Main](release-notes/samples/sample2.cs)]

属性ルーティングでは、省略可能なパラメーター、既定値、およびルート制約を指定するための便利な構文も提供されます。

[!code-csharp[Main](release-notes/samples/sample3.cs)]

属性ルーティングの詳細については、「 [WEB API 2 での属性ルーティング](../../../web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2.md)」を参照してください。

### <a name="oauth-20"></a>OAuth 2.0

Web API とシングルページアプリケーションプロジェクトテンプレートで、OAuth 2.0 を使用した承認がサポートされるようになりました。 OAuth 2.0 は、保護されたリソースへのクライアントアクセスを承認するためのフレームワークです。 これは、ブラウザーやモバイルデバイスなど、さまざまなクライアントで機能します。

OAuth 2.0 のサポートは、ベアラー認証用の Microsoft OWIN コンポーネントによって提供される新しいセキュリティミドルウェアと、承認サーバーロールの実装に基づいています。 または、Windows Server 2012 R2 の Azure Active Directory や ADFS など、組織の承認サーバーを使用してクライアントを承認することもできます。

### <a name="odata-improvements"></a>OData の機能強化

**$Select、$expand、$batch、および $value のサポート**

ASP.NET Web API OData で $select、$expand、および $value が完全にサポートされるようになりました。 また、要求のバッチ処理と変更セットの処理に $batch を使用することもできます。

$Select オプションと $expand オプションを使用すると、OData エンドポイントから返されるデータの構造を変更できます。 詳細については、「 [WEB API OData での $select と $expand サポートの概要](../../../web-api/overview/odata-support-in-aspnet-web-api/using-select-expand-and-value.md)」を参照してください。

**拡張機能の向上**

OData フォーマッタを拡張できるようになりました。 Atom エントリメタデータを追加したり、名前付きストリームとメディアリンクエントリをサポートしたり、インスタンス注釈を追加したり、リンクの生成方法をカスタマイズしたりすることができます。

**種類-less サポート**

エンティティ型に CLR 型を定義しなくても、OData サービスを構築できるようになりました。 代わりに、odata コントローラーは、OData フォーマッタのシリアル化/逆シリアル化である**Iedmobject**インスタンスを取得または返すことができます。

**既存のモデルを再利用する**

既に既存の entity data model (EDM) を使用している場合は、新しい entity data model を作成するのではなく、直接再利用できるようになりました。 たとえば、Entity Framework を使用している場合、EF がビルドする EDM を使用できます。

### <a name="request-batching"></a>バッチ処理の要求

要求のバッチ処理では、複数の操作を1つの HTTP POST 要求に結合して、ネットワークトラフィックを減らし、よりスムーズで高いなユーザーインターフェイスを提供します。 ASP.NET Web API は、要求バッチ処理のためのいくつかの方法をサポートするようになりました。

- OData サービスの $batch エンドポイントを使用します。
- 複数の要求を1つの MIME マルチパート要求にパッケージ化します。
- カスタムバッチ形式を使用します。

要求のバッチ処理を有効にするには、バッチハンドラーを含むルートを Web API 構成に追加するだけです。

[!code-csharp[Main](release-notes/samples/sample4.cs)]

また、要求または順番に実行するかどうかを制御することもできます。

### <a name="portable-aspnet-web-api-client"></a>ポータブル ASP.NET Web API クライアント

ASP.NET Web API クライアントを使用して、Windows ストアで動作するポータブルクラスライブラリを作成し、8つのアプリケーションを Windows Phone できるようになりました。 また、クライアントとサーバー間で共有できるポータブルフォーマッタを作成することもできます。

### <a name="improved-testability"></a>テストの容易性の向上

Web API 2 を使用すると、API コントローラーの単体テストがはるかに簡単になります。 要求メッセージと構成を使用して API コントローラーをインスタンス化し、テストするアクションメソッドを呼び出すだけです。 また、リンク生成を実行するアクションメソッドの**Urlhelper**クラスを簡単にモックできます。

### <a name="ihttpactionresult"></a>IHttpActionResult

IHttpActionResult を実装して、Web API アクションメソッドの結果をカプセル化できるようになりました。 Web API アクションメソッドから返された IHttpActionResult は、結果の応答メッセージを生成するために ASP.NET Web API ランタイムによって実行されます。 Web api の実装の単体テストを簡単にするために、任意の Web API アクションから IHttpActionResult を返すことができます。 便宜上、特定のステータスコード、書式設定されたコンテンツ、またはコンテンツをネゴシエートした応答を返す結果を含む、いくつかの IHttpActionResult 実装がすぐに用意されています。

### <a name="httprequestcontext"></a>HttpRequestContext

新しい**Httprequestcontext**は、要求に関連付けられているが、要求からすぐには利用できない状態を追跡します。 たとえば、 **Httprequestcontext**を使用して、ルートデータ、要求に関連付けられているプリンシパル、クライアント証明書、 **urlhelper** 、および仮想パスのルートを取得できます。 単体テストのために、 **Httprequestcontext**を簡単に作成できます。

要求のプリンシパルは、 **thread.currentprincipal**に依存するのではなく、要求でフローされるので、Web API パイプライン内にある間、要求の有効期間中にプリンシパルを使用できるようになりました。

### <a name="cors"></a>CORS

Brock Allen によるもう1つの優れた投稿により、ASP.NET はクロスオリジン要求共有 (CORS) を完全にサポートするようになりました。

ブラウザーのセキュリティ機能により、Web ページでは AJAX 要求を別のドメインに送信することはできません。 [CORS](http://www.w3.org/TR/cors/)は、サーバーが同じオリジンポリシーを緩めることを可能にする W3C 標準です。 CORS を使用することで、サーバーが一部のクロス オリジン要求を、その他の要求を拒否しながら、明示的に許可することができます。

Web API 2 では、プレフライト要求の自動処理を含む CORS がサポートされるようになりました。 詳細については、 [ASP.NET Web API でのクロスオリジン要求の有効化](../../../web-api/overview/security/enabling-cross-origin-requests-in-web-api.md)に関する文書を参照してください。

### <a name="authentication-filters"></a>認証フィルター

認証フィルターは、ASP.NET Web API パイプラインの承認フィルターの前に実行される ASP.NET Web API の新しい種類のフィルターであり、アクションごと、コントローラー単位、またはすべてのコントローラーに対してグローバルに認証ロジックを指定できます。 認証フィルターは、要求内の資格情報を処理し、対応するプリンシパルを指定します。 認証フィルターでは、承認されていない要求に応答して認証チャレンジを追加することもできます。

### <a name="filter-overrides"></a>フィルターのオーバーライド

オーバーライドフィルターを指定することにより、特定のアクションメソッドまたはコントローラーに適用するフィルターを上書きできるようになりました。 オーバーライドフィルターは、特定のスコープ (アクションまたはコントローラー) に対して実行してはならないフィルターの種類のセットを指定します。 これにより、グローバルフィルターを追加できますが、特定のアクションまたはコントローラーから除外することができます。

### <a name="owin-integration"></a>OWIN の統合

ASP.NET Web API は OWIN を完全にサポートするようになり、任意の OWIN 対応ホストで実行できるようになりました。 また、OWIN 認証システムとの統合を提供する**Hostauthenticationfilter**も含まれています。

OWIN 統合では、SignalR などの他の OWIN ミドルウェアと共に、独自のプロセスで Web API を自己ホストできます。 詳細については、「 [USE OWIN To Self Host ASP.NET Web API](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)」を参照してください。

<a id="TOC13"></a>
## <a name="aspnet-signalr-20"></a>ASP.NET SignalR 2.0

以下のセクションでは、SignalR 2.0 の機能について説明します。

- [OWIN 上に構築](#builtonowin)
- [MapHubs と Maphubs が MapSignalR になりました](#MapSignalR)
- [ドメイン間サポート](#crossdomain)
- [Monotouch.dialog とモノ Id を使用した iOS および Android のサポート](#mobile)
- [ポータブル .NET クライアント](#portable)
- [新しい自己ホストパッケージ](#selfhost)
- [下位互換性のあるサーバーのサポート](#backwardcompat)
- [.NET 4.0 のサーバーサポートを削除しました](#remove40)
- [クライアントとグループの一覧へのメッセージの送信](#messagelist)
- [特定のユーザーへのメッセージの送信](#sendtouser)
- [より優れたエラー処理のサポート](#errorhandling)
- [ハブの単体テストの簡素化](#unittesting)
- [JavaScript のエラー処理](#javascripterror)

既存の1.x プロジェクトを SignalR 2.0 にアップグレードする方法の例については、「 [SignalR 1.X プロジェクトをアップグレード](../../../signalr/overview/releases/upgrading-signalr-1x-projects-to-20.md)する」を参照してください。

<a id="builtonowin"></a>
### <a name="built-on-owin"></a>OWIN 上に構築

SignalR 2.0 は[、OWIN (Open Web Interface for .net)](http://owin.org/)で完全に構築されています。 この変更により、web ホストアプリケーションと自己ホスト型 SignalR アプリケーションの間で SignalR のセットアッププロセスの一貫性が大幅に向上しますが、多くの API 変更も必要でした。

<a id="MapSignalR"></a>

### <a name="maphubs-and-mapconnection-are-now-mapsignalr"></a>MapHubs と Maphubs が MapSignalR になりました

OWIN 標準との互換性のために、これらのメソッドの名前が `MapSignalR`に変更されました。 パラメーターを指定せずに `MapSignalR` 呼び出されると、すべてのハブがマップされます (バージョン1.x の `MapHubs` と同様)。個々の**PersistentConnection**オブジェクトをマップするには、型パラメーターとして接続の種類を指定し、最初の引数として接続の URL 拡張子を指定します。

`MapSignalR` メソッドは、Owin startup クラスで呼び出されます。 Visual Studio 2013 には、Owin startup クラス用の新しいテンプレートが含まれています。このテンプレートを使用するには、次の手順を実行します。

1. プロジェクトを右クリックします。
2. **[追加]** 、 **[新しい項目]** の選択...
3. **[Owin Startup クラス]** を選択します。 新しいクラスに**Startup.cs**という名前を指定します。

**Web アプリケーション**では、次に示すように、web.config ファイルの [アプリケーションの設定] ノードのエントリを使用して、`MapSignalR` メソッドを含む Owin startup クラスが Owin のスタートアッププロセスに追加されます。

**自己ホスト型アプリケーション**では、Startup クラスは `WebApp.Start` メソッドの型パラメーターとして渡されます。

**SignalR 1.x でのハブと接続のマッピング (web アプリケーションのグローバルアプリケーションファイルから):** 

[!code-csharp[Main](release-notes/samples/sample5.cs)]

**SignalR 2.0 でのハブと接続のマッピング (Owin スタートアップクラスファイルから):** 

[!code-csharp[Main](release-notes/samples/sample6.cs)]

**自己ホスト型アプリケーション**では、次に示すように、Startup クラスが `WebApp.Start` メソッドの型パラメーターとして渡されます。

[!code-csharp[Main](release-notes/samples/sample7.cs)]

<a id="crossdomain"></a>

### <a name="cross-domain-support"></a>ドメイン間サポート

SignalR 1.x では、クロスドメイン要求は単一の EnableCrossDomain フラグによって制御されていました。 このフラグは、JSONP 要求と CORS 要求の両方を制御します。 柔軟性を高めるため、すべての CORS サポートは SignalR のサーバーコンポーネントから削除されています (ブラウザーがサポートしていることが検出された場合、JavaScript クライアントは引き続き CORS を使用します)。また、これらのシナリオをサポートするために新しい OWIN ミドルウェアを利用できるようになりました。

SignalR 2.0 では、クライアントで JSONP が必要な場合 (古いブラウザーでクロスドメイン要求をサポートするため)、次に示すように、`HubConfiguration` オブジェクトの `EnableJSONP` を `true`に設定することによって、明示的に有効にする必要があります。 JSONP は、CORS よりも安全性が低いため、既定では無効になっています。

新しい CORS ミドルウェアを SignalR 2.0 に追加するには、次のセクションに示すように、`Microsoft.Owin.Cors` ライブラリをプロジェクトに追加し、SignalR ミドルウェアの前に `UseCors` を呼び出します。

**プロジェクトへの Owin の追加**: このライブラリをインストールするには、パッケージマネージャーコンソールで次のコマンドを実行します。

[!code-powershell[Main](release-notes/samples/sample8.ps1)]

このコマンドにより、2.0.0 バージョンのパッケージがプロジェクトに追加されます。

**UseCors の呼び出し**

次のコードスニペットは、SignalR 1.x と2.0 でドメイン間接続を実装する方法を示しています。

**SignalR 1.x でのクロスドメイン要求の実装 (グローバルアプリケーションファイルから)**

[!code-csharp[Main](release-notes/samples/sample9.cs)]

**SignalR 2.0 でのクロスドメイン要求の実装 ( C#コードファイルから)**

次のコードは、SignalR 2.0 プロジェクトで CORS または JSONP を有効にする方法を示しています。 このコードサンプルでは、`MapSignalR`ではなく `Map` と `RunSignalR` を使用して、CORS ミドルウェアが、アプリケーション全体ではなく、特定の URL プレフィックスに対して実行する必要のある SignalR 要求に対してのみ実行されるようにします (`MapSignalR`で指定されたパスのすべてのトラフィックではありません `Map`)。

[!code-csharp[Main](release-notes/samples/sample10.cs)]

<a id="mobile"></a>

### <a name="ios-and-android-support-via-monotouch-and-monodroid"></a>Monotouch.dialog とモノ Id を使用した iOS および Android のサポート

[Xamarin ライブラリ](https://xamarin.com/)の monotouch.dialog コンポーネントとモノ id コンポーネントを使用する IOS および Android クライアントのサポートが追加されました。 使用方法の詳細については、「 [Xamarin コンポーネントの使用](https://github.com/SignalR/SignalR/wiki/Building-Mono.Mobile.sln)」を参照してください。 これらのコンポーネントは、SignalR RTW リリースが利用可能になったときに、 [Xamarin ストア](https://store.xamarin.com/)で使用できるようになります。

<a id="portable"></a># # # ポータブル .NET クライアント

クロスプラットフォームの開発を容易にするために、Silverlight、WinRT、および Windows Phone クライアントは、次のプラットフォームをサポートする1つのポータブル .NET クライアントに置き換えられています。

- NET 4.5
- Silverlight 5
- WinRT (Windows ストアアプリ用 .NET)
- Windows Phone 8

<a id="selfhost"></a>

### <a name="new-self-host-package"></a>新しい自己ホストパッケージ

SignalR 自己ホスト (web サーバーでホストされるのではなく、プロセスまたは他のアプリケーションでホストされている SignalR アプリケーション) の使用を簡単に始めることができる NuGet パッケージが用意されています。 SignalR 1.x でビルドされた自己ホストプロジェクトをアップグレードするには、SignalR パッケージを削除してから、SignalR パッケージを追加した後に追加します。 自己ホストパッケージの概要については、「[チュートリアル: SignalR 自己ホスト](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)」を参照してください。

<a id="backwardcompat"></a>

### <a name="backward-compatible-server-support"></a>下位互換性のあるサーバーのサポート

以前のバージョンの SignalR では、クライアントとサーバーで使用されている SignalR パッケージのバージョンが同一である必要があります。 更新が困難なシッククライアントアプリケーションをサポートするために、SignalR 2.0 では、古いクライアントでの新しいサーバーバージョンの使用がサポートされるようになりました。 **注: SignalR 2.0 では、以前のバージョンでビルドされたサーバーを新しいクライアントでサポートしていません。**

<a id="remove40"></a>

### <a name="removed-server-support-for-net-40"></a>.NET 4.0 のサーバーサポートを削除しました

SignalR 2.0 では、.NET 4.0 とのサーバー相互運用性のサポートが削除されました。 .NET 4.5 は、SignalR 2.0 サーバーで使用する必要があります。 引き続き、SignalR 2.0 用の .NET 4.0 クライアントがあります。

<a id="messagelist"></a>

### <a name="sending-a-message-to-a-list-of-clients-and-groups"></a>クライアントとグループの一覧へのメッセージの送信

SignalR 2.0 では、クライアント Id とグループ Id の一覧を使用してメッセージを送信することができます。 次のコードスニペットは、この方法を示しています。

**PersistentConnection を使用して、クライアントとグループの一覧にメッセージを送信する**

[!code-csharp[Main](release-notes/samples/sample11.cs)]

**ハブを使用して、クライアントとグループの一覧にメッセージを送信する**

[!code-csharp[Main](release-notes/samples/sample12.cs)]

<a id="sendtouser"></a>

### <a name="sending-a-message-to-a-specific-user"></a>特定のユーザーへのメッセージの送信

この機能を使用すると、ユーザーは新しいインターフェイス IUserIdProvider を使用して、IRequest に基づいてユーザー Id を指定できます。

**IUserIdProvider インターフェイス**

[!code-csharp[Main](release-notes/samples/sample13.cs)]

既定では、ユーザーの IPrincipal.Identity.Name をユーザー名として使用する実装が存在します。

ハブでは、新しい API を使用して、これらのユーザーにメッセージを送信できます。

**クライアント. User API の使用**

[!code-csharp[Main](release-notes/samples/sample14.cs)]

<a id="errorhandling"></a>

### <a name="better-error-handling-support"></a>より優れたエラー処理のサポート

ユーザーは、任意のハブ呼び出しから**HubException**をスローできるようになりました。 **HubException**のコンストラクターは、文字列メッセージとオブジェクトの追加のエラーデータを受け取ることができます。 SignalR は、例外を自動的にシリアル化し、それをクライアントに送信します。これは、ハブメソッドの呼び出しを拒否/失敗するために使用されます。

[**詳細なハブ例外を表示する]** 設定は、クライアントに送信される**HubException**には影響しません。常に送信されます。

**HubException をクライアントに送信する方法を示すサーバー側コード**

[!code-csharp[Main](release-notes/samples/sample15.cs)]

**サーバーから送信された HubException への応答を示す JavaScript クライアントコード**

[!code-html[Main](release-notes/samples/sample16.html)]

**サーバーから送信された HubException への応答を示す .NET クライアントコード**

[!code-csharp[Main](release-notes/samples/sample17.cs)]

<a id="unittesting"></a>

### <a name="easier-unit-testing-of-hubs"></a>ハブの単体テストの簡素化

SignalR 2.0 には、モッククライアント側の呼び出しの作成を容易にするハブで `IHubCallerConnectionContext` というインターフェイスが含まれています。 次のコードスニペットは、一般的なテストハーネス[xUnit.net](https://github.com/xunit/xunit)と[moq](https://code.google.com/p/moq/)でこのインターフェイスを使用する方法を示しています。

**XUnit.net を使用した SignalR の単体テスト**

[!code-csharp[Main](release-notes/samples/sample18.cs)]

**Moq を使用した SignalR の単体テスト**

[!code-csharp[Main](release-notes/samples/sample19.cs)]

<a id="javascripterror"></a>

### <a name="javascript-error-handling"></a>JavaScript のエラー処理

SignalR 2.0 では、すべての JavaScript エラー処理コールバックで、生の文字列ではなく JavaScript エラーオブジェクトが返されます。 これにより、SignalR は、より豊富な情報をエラーハンドラーに渡すことができます。 内部例外は、エラーの `source` プロパティから取得できます。

**Start. Fail 例外を処理する JavaScript クライアントコード**

[!code-javascript[Main](release-notes/samples/sample20.js)]

<a id="TOC8"></a>
## <a name="aspnet-identity"></a>ASP.NET Identity

### <a name="new-aspnet-membership-system"></a>新しい ASP.NET メンバーシップシステム

ASP.NET Identity は、ASP.NET アプリケーションの新しいメンバーシップシステムです。 ASP.NET Identity を使用すると、ユーザー固有のプロファイルデータをアプリケーションデータに簡単に統合できます。 ASP.NET Identity では、アプリケーションでユーザープロファイルの永続性モデルを選択することもできます。 データは SQL Server データベースまたは別のデータストア (Azure Storage テーブルなどの NoSQL データストア) に格納できます。 詳細については、「 **Visual Studio 2013 での ASP.NET Web プロジェクトの作成**における[個々のユーザーアカウント](creating-web-projects-in-visual-studio.md#indauth)」を参照してください。

### <a name="claims-based-authentication"></a>クレーム ベースの認証

ASP.NET は、信頼性情報ベースの認証をサポートするようになりました。この認証では、ユーザーの id は信頼された発行者からのクレームのセットとして表されます。 ユーザーは、アプリケーションデータベースで保持されているユーザー名とパスワードを使用して、またはソーシャル id プロバイダー (Microsoft アカウント、Facebook、Google、Twitter など) を使用するか、または Azure Active Directory を使用して組織アカウントを使用して認証できます。Active Directory フェデレーションサービス (AD FS) (ADFS)。

### <a name="integration-with-azure-active-directory-and-windows-server-active-directory"></a>Azure Active Directory と Windows Server Active Directory との統合

認証に Azure Active Directory または Windows Server Active Directory (AD) を使用する ASP.NET プロジェクトを作成できるようになりました。 詳細については、「 **Visual Studio 2013 での ASP.NET Web プロジェクトの作成**」の「[組織アカウント](creating-web-projects-in-visual-studio.md#orgauth)」を参照してください。

### <a name="owin-integration"></a>OWIN の統合

ASP.NET 認証は、任意の OWIN ベースのホストで使用できる OWIN ミドルウェアに基づいています。 OWIN の詳細については、次の[MICROSOFT OWIN Components](#TOC7)のセクションを参照してください。

<a id="TOC7"></a>
## <a name="microsoft-owin-components"></a>Microsoft OWIN コンポーネント

[Open Web Interface for .net](http://owin.org/) (OWIN) は、.net web サーバーと web アプリケーションの間の抽象化を定義します。 OWIN は、web アプリケーションをサーバーから分離することで、web アプリケーションをホストに依存しないようにします。 たとえば、IIS で OWIN ベースの web アプリケーションをホストしたり、カスタムプロセスで自己ホストしたりすることができます。

Microsoft OWIN コンポーネント (Katana プロジェクトとも呼ばれます) で導入された変更には、新しいサーバーおよびホストコンポーネント、新しいヘルパーライブラリとミドルウェア、新しい認証ミドルウェアが含まれます。

OWIN と Katana の詳細については、「 [OWIN および Katana の新機能](../../../aspnet/overview/owin-and-katana/index.md)」を参照してください。

**注: [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)アプリケーションを IIS クラシックモードで実行することはできません。統合モードで実行する必要があります。**

**注: [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)アプリケーションは完全信頼で実行する必要があります。**

### <a name="new-servers-and-hosts"></a>新しいサーバーとホスト

このリリースでは、自己ホストのシナリオを可能にするために新しいコンポーネントが追加されました。 これらのコンポーネントには、次の NuGet パッケージが含まれます。

- **Owin. HttpListener**. **HttpListener**を使用して HTTP 要求をリッスンし、それらを OWIN パイプラインに送信する OWIN サーバーを提供します。
- **Owin**には、コンソールアプリケーションや Windows サービスなどのカスタムプロセスで Owin パイプラインを自己ホストする開発者向けのライブラリが用意されています。
- **Owinhost**。 には `Microsoft.Owin.Hosting` をラップするスタンドアロンの実行可能ファイルが用意されています。これにより、カスタムホストアプリケーションを作成しなくても、OWIN パイプラインを自己ホストできます。

さらに、`Microsoft.Owin.Host.SystemWeb` パッケージでは、ミドルウェアが**Systemweb**サーバーにヒントを提供できるようになりました。これは、特定の ASP.NET パイプラインステージの間にミドルウェアを呼び出す必要があることを示しています。 この機能は、ASP.NET パイプラインの早い段階で実行される認証ミドルウェアに特に役立ちます。

### <a name="helper-libraries-and-middleware"></a>ヘルパーライブラリとミドルウェア

OWIN 仕様の関数と型の定義のみを使用して OWIN コンポーネントを記述することもできますが、新しい `Microsoft.Owin` パッケージでは、よりわかりやすい抽象化のセットが提供されます。 このパッケージは、以前のいくつかのパッケージ (`Owin.Extensions`、`Owin.Types`など) を単一の適切に構造化されたオブジェクトモデルに結合して、他の OWIN コンポーネントで簡単に使用できるようにします。 実際、Microsoft OWIN コンポーネントの大部分は、このパッケージを使用するようになりました。

> [!NOTE]
> [OWIN](http://www.owin.org)アプリケーションを IIS クラシックモードで実行することはできません。統合モードで実行する必要があります。

> [!NOTE]
> [OWIN](http://www.owin.org)アプリケーションは完全信頼で実行する必要があります。

このリリースには、Owin パッケージも含まれています。これには、実行中の OWIN アプリケーションを検証するミドルウェア、およびエラーを調査するためのエラーページミドルウェアが含まれています。

### <a name="authentication-components"></a>認証コンポーネント

次の認証コンポーネントを使用できます。

- **Owin**します。 オンプレミスまたはクラウドベースのディレクトリサービスを使用した認証を有効にします。
- **Owin** cookie を使用した認証を有効にします。 このパッケージは、以前は `Microsoft.Owin.Security.Forms`という名前でした。
- **Owin**は、Facebook の OAuth ベースのサービスを使用した認証を可能にします。
- **Owin** Google の OpenID ベースのサービスを使用して認証を有効にします。
- **Owin**は jwt トークンを使用した認証を有効にします。
- **Owin** microsoft アカウントを使用して認証を有効にします。
- **Owin**します。 には、ベアラートークンを認証するための、OAuth 承認サーバーとミドルウェアが用意されています。
- **Owin**は、Twitter の OAuth ベースのサービスを使用した認証を可能にします。

このリリースには、クロスオリジン HTTP 要求を処理するためのミドルウェアを含む `Microsoft.Owin.Cors` パッケージも含まれています。

> [!NOTE]
> JWT 署名のサポートは、Visual Studio 2013 の最終バージョンでは削除されています。

<a id="ef6"></a>
## <a name="entity-framework-6"></a>Entity Framework 6

Entity Framework 6 の新機能とその他の変更点の一覧については、「 [Entity Framework バージョンの履歴](https://msdn.com/data/jj574253)」を参照してください。

<a id="TOC14"></a>
## <a name="aspnet-razor-3"></a>ASP.NET Razor 3

ASP.NET Razor 3 には、次の新機能が含まれています。

- タブ編集のサポート。 以前は、**タブを保持**する オプションを使用すると、Visual Studio の **ドキュメントのフォーマット** コマンド、自動インデント、および 自動書式設定 は正常に動作しませんでした。 この変更により、タブ書式設定用の Razor コードの Visual Studio の書式設定が修正します。
- リンクを生成するときの URL 書き換え規則のサポート。
- 透過的セキュリティ属性の削除。
  > [!NOTE]
  > これは互換性に影響する変更であり、Razor 3 は MVC4 以前と互換性がありませんが、Razor 2 は MVC5 または MVC5 に対してコンパイルされたアセンブリと互換性がありません。

プレリリース版からの Visual Studio 2013 で修正された Razor 3 の問題については、[こちら](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Resolved%7cClosed&type=All&priority=All&release=All%7cv5.0%2bPreview%7cv5.0%2bRC%7cv5.0%2bRTM&assignedTo=All&component=Web%2bPages%252fRazor&reasonClosed=Fixed&sortField=LastUpdatedDate&sortDirection=Descending&page=0)を参照してください。

<a id="TOC15"></a>
## <a name="aspnet-app-suspend"></a>ASP.NET アプリの中断

ASP.NET App Suspend は、1台のコンピューターで多数の ASP.NET サイトをホストするためのユーザーエクスペリエンスと経済モデルを根本的に変更する、.NET Framework 4.5.1 のゲーム変更機能です。 詳細については、「 [ASP.NET App Suspend –応答性の高い共有 .net web ホスティング](https://blogs.msdn.com/b/dotnet/archive/2013/10/09/asp-net-app-suspend-responsive-shared-net-web-hosting.aspx)」を参照してください。

<a id="knownissues"></a>
## <a name="known-issues-and-breaking-changes"></a>既知の問題と重大な変更

このセクションでは、Visual Studio 2013 の ASP.NET and Web Tools における既知の問題と重大な変更について説明します。

### <a name="nuget"></a>NuGet

- [新しいパッケージの復元は、SLN ファイルを使用すると Mono で機能しません](https://nuget.codeplex.com/workitem/3596)。今後の nuget のダウンロードと[nuget.exe パッケージ](http://www.nuget.org/packages/NuGet.CommandLine/)の更新プログラムで修正されます。
- [新しいパッケージの復元は、Wix プロジェクトでは機能しません](https://nuget.codeplex.com/workitem/3598)。今後の nuget のダウンロードと[nuget.exe パッケージ](http://www.nuget.org/packages/NuGet.CommandLine/)の更新プログラムで修正されます。
- [自動パッケージ復元は、ソリューションフォルダーの下にあるプロジェクトに対しては機能しません](https://nuget.codeplex.com/workitem/3625)。 NuGet 2.8 で修正されます。

### <a name="aspnet-web-api"></a>ASP.NET Web API

1. `$select` と `$expand`のサポートが追加されたため、`ODataQueryOptions<T>.ApplyTo(IQueryable)` `IQueryable<T>` は常に返されません。

    `ODataQueryOptions<T>` の前のサンプルでは、`ApplyTo` から `IQueryable<T>`に戻り値が常にキャストされています。 これは、以前にサポートしていたクエリオプション (`$filter`、`$orderby`、`$skip`、`$top`) によってクエリの構造が変更されないため、これまでに動作しました。 これで `$expand` `$select` がサポートされるようになり、`ApplyTo` からの戻り値が常に `IQueryable<T>` されることはなくなりました。

    [!code-csharp[Main](release-notes/samples/sample21.cs)]

    前に示したサンプルコードを使用している場合は、クライアントが `$select` と `$expand`を送信しない場合は動作を続行します。 ただし、`$select` と `$expand` をサポートする場合は、そのコードをこのコードに変更する必要があります。

    [!code-csharp[Main](release-notes/samples/sample22.cs)]
2. **要求の Url または RequestContext。 Url は、バッチ要求の実行中に null になります。**

    バッチ処理のシナリオでは、 **Urlhelper**は、**要求の Url**または**RequestContext**からアクセスした場合に null になります。

    現在、この問題はここで追跡されています: [Batchrequestcontext。バッチ処理要求の Url が null](http://aspnetwebstack.codeplex.com/workitem/1301)です。

    この問題を回避するには、次の例のように**Urlhelper**の新しいインスタンスを作成します。

    **UrlHelper の新しいインスタンスを作成しています**

    [!code-csharp[Main](release-notes/samples/sample23.cs)]

### <a name="aspnet-mvc"></a>ASP.NET MVC

1. MVC5 と OrgAuth を使用しているときに、検証を行うビューがある場合、データをビューにポストすると、次のエラーが表示されることがあります。

    **Error**:

    *'/' アプリケーションでサーバーエラーが発生しています。*

    <em>型 '<http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier>' または '<https://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider>' のクレームが、指定された ClaimsIdentity に存在しませんでした。要求ベースの認証による偽造防止トークンのサポートを有効にするには、構成された要求プロバイダーが、生成した ClaimsIdentity インスタンスに対して両方の要求を提供していることを確認してください。構成された要求プロバイダーが、一意の識別子として別の要求の種類を使用する場合は、静的なプロパティの UniqueClaimTypeIdentifier を設定することによって構成できます。</em>

    **回避策**:

    Global.asax に次の行を追加して修正します。

    `AntiForgeryConfig.UniqueClaimTypeIdentifier = ClaimTypes.Name;`

    これは、次のリリースで修正されます。
2. MVC4 アプリを MVC5 にアップグレードしたら、ソリューションをビルドして起動します。 次のエラーが表示されます。

    あるこのセクションは、[B] System.web. Web.config...................................... は、場所 ' C:\windows\Microsoft.Net\assembly\GAC\_MSIL\System.Web.WebPages.Razor\v4.0\_2.0.0.0\_\_31bf3856ad364e35 \ ' のコンテキスト ' Default ' にある ' System.web. Web. Razor, Version = 2.0.0.0, Culture = ニュートラル, PublicKeyToken = 31bf3856ad364e35 ' から生成されます。 型 B の生成元は、' 3.0.0.0, Version =, Culture = ニュートラル, PublicKeyToken = 31bf3856ad364e35 ' というコンテキストで、場所 ' C:\Windows\Microsoft.NET\Framework\v4.0.30319\Temporary ASP.NET Files\root\6d05bbd0\e8b5908e\assembly\dl3\c9cbca63\f8910382\_62の既定値 ' になります. ' を指定します。

    上記のエラーを修正するには、プロジェクトの*すべて*の web.config ファイル (Views フォルダー内のファイルを含む) を開き、次の手順を実行します。

   1. "4.0.0.0" のバージョン "" のすべての出現箇所を "5.0.0.0" に更新します。
   2. "3.0.0.0" のバージョン "2.0.0.0" のすべての出現箇所を更新し、&quot; を&quot; &quot;して &quot;、"" に変更します。また、

      たとえば、上記の変更を行った後、アセンブリのバインドは次のようになります。

      [!code-xml[Main](release-notes/samples/sample24.xml)]

      Mvc 4 プロジェクトを MVC 5 にアップグレードする方法については、「 [ASP.NET mvc 4 と WEB Api プロジェクトを ASP.NET mvc 5 および WEB api 2 にアップグレードする方法](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md)」を参照してください。
3. JQuery の控えめな検証でクライアント側の検証を使用する場合、型 = ' number ' の HTML 入力要素の検証メッセージが正しくないことがあります。 正しいメッセージではなく有効な数値が入力されている場合は、必要な値 ("Age フィールドが必要") の検証エラーが表示されます。

    この問題は、Create ビューと Edit ビューで整数プロパティを持つモデルのスキャフォールディングコードでよく見られます。

    この問題を回避するには、エディターヘルパーを次のように変更します。

    `@Html.EditorFor(person => person.Age)`

    変更後:

    `@Html.TextBoxFor(person => person.Age)`
4. ASP.NET MVC 5 では、部分信頼はサポートされなくなりました。 MVC または WebAPI バイナリにリンクするプロジェクトでは、 [Securitytransparent](https://msdn.microsoft.com/library/system.security.securitytransparentattribute.aspx)属性と[AllowPartiallyTrustedCallers](https://msdn.microsoft.com/library/system.security.allowpartiallytrustedcallersattribute.aspx)属性を削除する必要があります。 これらの属性を削除すると、次のようなコンパイラエラーが発生しなくなります。

    `Attempt by security transparent method ‘MyComponent' to access security critical type 'System.Web.Mvc.MvcHtmlString' failed. Assembly 'PagedList.Mvc, Version=4.3.0.0, Culture=neutral, PublicKeyToken=abbb863e9397c5e1' is marked with the AllowPartiallyTrustedCallersAttribute, and uses the level 2 security transparency model. Level 2 transparency causes all methods in AllowPartiallyTrustedCallers assemblies to become security transparent by default, which may be the cause of this exception.`

    > この結果、同じアプリケーションで4.0 および5.0 アセンブリを使用することはできません。 すべてを5.0 に更新する必要があります。

### <a name="spa-template-with-facebook-authorization-may-cause-instability-in-ie-while-the-web-site-is-hosted-in-intranet-zone"></a>Web サイトがイントラネットゾーンでホストされている場合、Facebook の承認を持つ SPA テンプレートで IE が不安定になることがある

SPA テンプレートは、Facebook との外部ログインを提供します。 テンプレートを使用して作成したプロジェクトがローカルで実行されている場合、サインインすると、IE がクラッシュする可能性があります。

解決方法:

1. Web サイトをインターネットゾーンでホストします。もしくは

2. IE 以外のブラウザーでシナリオをテストします。

### <a name="web-forms-scaffolding"></a>Web フォームのスキャフォールディング

Web フォームのスキャフォールディングは VS2013 から削除され、Visual Studio の今後の更新プログラムで使用できるようになります。 ただし、MVC の依存関係を追加し、MVC のスキャフォールディングを生成することで、Web フォームプロジェクト内でスキャフォールディングを使用することができます。 プロジェクトには、Web フォームと MVC の組み合わせが含まれます。

MVC を Web フォームプロジェクトに追加するには、新しいスキャフォールディングアイテムを追加し、 **[mvc 5 の依存関係]** を選択します。 すべてのコンテンツファイル (スクリプトなど) が必要かどうかに応じて、[最小] または [完全] を選択します。 次に、MVC のスキャフォールディング item を追加します。これにより、プロジェクトにビューとコントローラーが作成されます。

### <a name="mvc-and-web-api-scaffolding---http-404-not-found-error"></a>MVC および Web API のスキャフォールディング-HTTP 404、見つからないエラー

スキャフォールディング項目をプロジェクトに追加したときにエラーが発生した場合は、プロジェクトが不整合な状態のままになる可能性があります。 スキャフォールディングに加えられた変更の一部はロールバックされますが、インストールされている NuGet パッケージなどのその他の変更はロールバックされません。 ルーティング構成の変更がロールバックされた場合、スキャフォールディング items に移動すると、ユーザーには HTTP 404 エラーが表示されます。

対処法:

- MVC のこのエラーを修正するには、新しいスキャフォールディング項目を追加し、[MVC 5 の依存関係] ([最小] または [完全]) を選択します。 このプロセスによって、必要なすべての変更がプロジェクトに追加されます。
- このエラーを解決するには、次のように Web API を使用します。

  1. Webapiconfig.cs クラスをプロジェクトに追加します。

      [!code-csharp[Main](release-notes/samples/sample25.cs)]

      [!code-vb[Main](release-notes/samples/sample26.vb)]
  2. 次に示すように、global.asax で Webapiconfig.cs をアプリケーション\_に構成します。

      [!code-csharp[Main](release-notes/samples/sample27.cs)]

      [!code-vb[Main](release-notes/samples/sample28.vb)]
