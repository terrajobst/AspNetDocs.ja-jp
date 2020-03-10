---
uid: visual-studio/overview/2013/aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes
title: Visual Studio 2013 リリースノートについては、ASP.NET and Web Tools 2013.2Microsoft Docs
author: microsoft
description: ''
ms.author: riande
ms.date: 03/06/2014
ms.assetid: 7ef5f73c-ca60-43c1-bdb2-702800347e7e
msc.legacyurl: /visual-studio/overview/2013/aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes
msc.type: authoredcontent
ms.openlocfilehash: 22d4d4afd6963f23d6cfef1745a859c20b69d599
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78505450"
---
# <a name="aspnet-and-web-tools-20132--for-visual-studio-2013-release-notes"></a>Visual Studio 2013 の ASP.NET と Web 2013.2 ツールのリリース ノート

[Microsoft](https://github.com/microsoft)

## <a name="installation-notes"></a>インストールに関する注意事項

Visual Studio 2013.2 の ASP.NET and Web Tools はメインインストーラーにバンドルされており、 [Visual Studio 2013 Update 2](https://go.microsoft.com/fwlink/?LinkId=390521)の一部としてダウンロードできます。

## <a name="documentation"></a>ドキュメント

[ASP.NET Web サイト](https://www.asp.net/)から、Visual Studio 2013.2 の ASP.NET and Web Tools に関するチュートリアルやその他の情報を入手できます。

## <a name="software-requirements"></a>ソフトウェア要件

Visual Studio 2013.2 の ASP.NET and Web Tools には Visual Studio 2013 が必要です。

## <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-20132"></a>Visual Studio 2013.2 の ASP.NET and Web Tools の新機能

以下のセクションでは、リリースで導入された機能について説明します。

- [1つの ASP.NET プロジェクトテンプレート](#oneaspnet)
- [IIS Express で Web アプリケーションを起動するときに SSL をサポートする](#ssl)
- [Visual Studio Web エディターの機能強化](#vswebeditor)
- [ブラウザー リンク](#browserlink)
- [Visual Studio での Azure App Service Web Apps のサポート](#waws)
- [新しい Web プロジェクトを作成するときにリモートの Azure リソースを作成する](#AzureResources)
- [Web 発行の機能強化](#webpublish)
- [ASP.NET スキャフォールディング](#scaffolding)
- [NuGet 2.8.1](#nuget)
- [ASP.NET Web フォーム](#webforms)
- [ASP.NET MVC 5.1.2](#mvc)
- [ASP.NET Web API 2.1.2](#webapi)
- [ASP.NET Web ページ3.1.2](#webpages)
- [Entity Framework 6.1](#ef)
- [ASP.NET Identity 2.0.0](#identity)
- [Microsoft OWIN コンポーネント](#owin)
- [ASP.NET SignalR 2.0.2](#signalr)

<a id="oneaspnet"></a>
### <a name="one-aspnet-project-templates"></a>1つの ASP.NET プロジェクトテンプレート

- ASP.NET プロジェクトテンプレートを更新して、アカウントの確認とパスワードのリセットをサポートします。
- オンプレミスの組織アカウントを使用した認証をサポートするように ASP.NET Web API テンプレートを更新します。
- ASP.NET SPA テンプレートには、MVC とサーバー側のビューに基づく認証が含まれるようになりました。 テンプレートには、認証されたユーザーのみがアクセスできる WebAPI コントローラーがあります。

<a id="ssl"></a>
### <a name="support-ssl-when-launching-web-applications-on-iis-express"></a>IIS Express で Web アプリケーションを起動するときに SSL をサポートする

Localhost で HTTPS を参照およびデバッグするときのセキュリティの警告を回避するために、Internet Explorer と Chrome が自己署名 IIS express SSL 証明書を信頼できるようにするダイアログを追加しました。

たとえば、web プロジェクトのプロパティは、SSL を使用するように設定できます。 F4 キーをクリックして、[プロパティ] ダイアログボックスを表示します。 **SSL Enabled**を true に変更します。 SSL URL をコピーします。

![SSL Enabled プロパティ](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image1.png)

HTTPS ベースの URL を使用するように web プロジェクトのプロパティページの [web] タブを設定します (ssl Web サイトを以前に作成した場合を除き、SSL URL は `https://localhost:44300/` ます)。

![プロジェクト URL (HTTPS) の設定](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image2.png)

Ctrl キーを押しながら F5 キーを押してアプリケーションを実行します。 指示に従って、IIS Express が生成した自己署名証明書を信頼します。

![SSL の警告](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image3.png)

**[セキュリティの警告]** ダイアログを読み、localhost を表す証明書をインストールする場合は [**はい]** をクリックします。

![Security Warning](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image4.png)

サイトは、ブラウザーに証明書の警告が表示されることなく、IE または Chrome で表示されます。

![警告のない HTTPS ページ](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image5.png)

Firefox は独自の証明書ストアを使用するため、警告が表示されます。

<a id="vswebeditor"></a>
### <a name="visual-studio-web-editor-enhancements"></a>Visual Studio Web エディターの機能強化

- **新しい json プロジェクト項目とエディター**: json プロジェクト項目とエディターを Visual Studio に追加しました。 現在の JSON エディターの機能には、色付け、構文検証、中かっこの補完、アウトライン、ツールオプションの設定などがあります。

    ![JSON エディター](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image6.png)

    IntelliSense で[JSON スキーマ](http://json-schema.org/)v3 と v4 がサポートされるようになりました。 スキーマコンボボックスでは、既存のスキーマを選択したり、ローカルスキーマパスを編集したりすることができます。また、プロジェクトの JSON ファイルをドロップして、相対パスを取得することもできます。

    ![JSON Intellisense](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image7.png)    ![JSON スキーマエディター](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image8.png)
- **新しい Sass (SCSS) エディター**: VS2013 RTM に追加したので、sass プロジェクトの項目とエディターが作成されました。 Sass エディターの機能は、LESS エディターに相当します。これには、色付け、変数との IntelliSense、コメント/コメント解除、クイックヒント、書式設定、構文検証、アウトライン、goto 定義、カラーピッカー、ツールオプションの設定などが含まれます。

    ![新しい項目の追加: SCSS スタイルシート](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image9.png)    ![スタイルシートエディター](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image10.png)
- **HTML、Razor、CSS、LESS、および sass 各ドキュメントでの新しい URL の選択:** Web フォームページ外では、URL 選択のない VS 2013 が付属しています。 HTML、Razor、CSS、LESS、および Sass エディター用の新しい URL ピッカーは、'.. ' を認識するダイアログを使用しない、fluent 入力ピッカーです。 img タグとリンクについては、ファイルの一覧が適切にフィルター処理されます。

    ![イメージタグの URL の選択](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image11.png)    ![ビューの URL の選択](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image12.png)    ![CSS 用の URL の選択](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image13.png)
- **機能を追加することで、より少ないエディターに更新**
- **Intellisense のアップグレードのノックアウト**: vs Intellisense "Ko のビューモデル:" 構文に非標準のノックアウト構文を追加しました。 フォームのコメントを使用して、ページ上の複数のビューモデルにバインドするために使用できます。

    ![ノックアウト (Intellisense を)](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image14.png)

    また、入れ子になったビューモデルの IntelliSense もサポートされるようになったため、ビューモデルの深い入れ子になったオブジェクトにドリルダウンすることができます。

    `<div data-bind="text: foo.bar.baz.etc" />`

    表示される IntelliSense は、JavaScript オブジェクトの完全な IntelliSense です。

    ![完全な JavaScript オブジェクトを示す Intellisense](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image15.png)
- **HTML、Razor、CSS、LESS、および sass のドキュメントでの新しい url の選択**: Web フォームページ以外では、url 選択がない状態での VS 2013 が提供されています。 HTML、Razor、CSS、LESS、および Sass エディター用の新しい URL ピッカーは、'.. ' を認識するダイアログを使用しない、fluent 入力ピッカーです。 img タグとリンクについては、ファイルの一覧が適切にフィルター処理されます。

    ![イメージタグの URL の選択](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image16.png)    ![ビューの URL の選択](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image17.png)    ![CSS 用の URL の選択](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image18.png)

<a id="browserlink"></a>
### <a name="browser-link"></a>ブラウザー リンク

- ブラウザーリンクは、HTTPS 接続をサポートするようになり、証明書がブラウザーによって信頼されている限り、他の接続とダッシュボードに表示されるようになります。
- 静的な HTML ソースマッピング
- データのマッピングの SPA サポート
- マッピングデータを自動更新する

<a id="waws"></a>
### <a name="support-for-azure-app-service-web-apps-in-visual-studio"></a>Visual Studio での Azure App Service Web Apps のサポート

- **Azure サインインをサポートします。**
- **Web アプリのリモートデバッグとリモートビュー**: サーバーエクスプローラーで web アプリの Azure App Service とリモートビューを使用して、web アプリ[のリモートデバッグ](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio)をサポートするようになりました。

<a id="AzureResources"></a>
### <a name="create-remote-azure-resources-when-creating-a-new-web-project"></a>新しい Web プロジェクトを作成するときにリモートの Azure リソースを作成する

[新しい web アプリケーション] ダイアログで、Azure の[[リモートリソースの作成](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet)] チェックボックスを追加しました。 このオプションを選択すると、新しい web アプリケーションを作成するエクスペリエンスを統合し、テスト用に Azure 発行サイトを設定し、いくつかの簡単な手順で発行プロファイルを作成することができます。

![Azure リソースを使用した新しいプロジェクト](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image19.png)![Azure への発行](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image20.png)

<a id="webpublish"></a>
### <a name="web-publish-enhancements"></a>Web 発行の機能強化

- 発行のユーザーエクスペリエンスを向上させます。

<a id="scaffolding"></a>
### <a name="aspnet-scaffolding"></a>ASP.NET スキャフォールディング

- **列挙型のサポート:** モデルが列挙型を使用している場合、MVC Scaffolder によって列挙型のドロップダウンが生成されます。 これは、MVC の列挙型ヘルパーを使用します。
- **ブートストラップのサポート**: MVC スキャフォールディングでテンプレートの editorfor 更新して、ブートストラップクラスを使用できるようにしました。
- **パッケージのサポート**: Mvc および Web api スキャフォールダーは、Mvc と web api の5.1 パッケージを追加します

次のスクリーンショットは、スキャフォールディングモデルを示しています。

- モデルコード:

     ![モデルコード](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image21.png)
- モデルコードをコンパイルして右クリックし、 **[追加]** 、 **[新しいスキャフォールディング Item]** の順に選択します。

     ![新しいスキャフォールディング項目の追加](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image22.png)
- **Entity Framework を使用して、ビューを含む MVC5 Controller**を選択します。

     ![ビューを含む新しい MVC5 controller を追加する](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image23.png)
- モデルを使用して**コントローラーを追加**します。

    ![](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image24.png)
- 生成されたコードを確認します。たとえば、Views/WeekdayModels/Edit には、EnumDropDownListFor を含む `@Html.EnumDropDownListFor`: ![ビューが含まれてい](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image25.png)
- ページを実行すると、生成された列挙型の combobox が表示されます。値を null にできる場合は、コンボボックスに対して空の文字列を選択できます。 たとえば、 **[作成]** ページには次のように表示されます。

    ![空の文字列を許可するコンボボックス](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image26.png)

<a id="nuget"></a>
### <a name="nuget-281"></a>NuGet 2.8.1

NuGet 2.8.1 RTM は2014年4月にリリースされます。 リリースノートの重要なポイントを次に示しますが、これらの変更の詳細については、[完全なリリースノート](http://docs.nuget.org/docs/release-notes/nuget-2.8)を確認してください。

- **ターゲット Windows Phone 8.1 アプリケーション**: NuGet 2.8.1 は、ターゲットフレームワークモニカー ' WindowsPhoneApp '、' WPA '、' WindowsPhoneApp81 '、および ' WPA81 ' を使用して、Windows Phone 8.1 アプリケーションのターゲット設定をサポートするようになりました。

- **依存関係の修正プログラムの解決**: パッケージの依存関係を解決するときに、NuGet は、パッケージの依存関係を満たす最低メジャーおよびマイナーパッケージバージョンを選択するための戦略を実装しました。 ただし、メジャーバージョンとマイナーバージョンとは異なり、修正プログラムのバージョンは常に最も高いバージョンに解決されていました。 動作は攻撃者でしたが、依存関係を含むパッケージをインストールするための決定性が欠如しています。
- **Dependencyversion スイッチ**: NuGet 2.8 では、依存関係を解決するための*既定*の動作が変更されますが、パッケージマネージャーコンソールの-dependencyversion スイッチを使用して依存関係の解決プロセスをより正確に制御することもできます。 スイッチを使用すると、依存関係を、可能な限り低いバージョン (既定の動作)、可能な限り高いバージョン、または最新のマイナーバージョンまたは修正プログラムバージョンに解決できます。 このスイッチは、powershell コマンドのインストールパッケージに対してのみ機能します。
- **Dependencyversion 属性**: 前に説明した-dependencyversion スイッチに加え、nuget では、-dependencyversion スイッチがインストールパッケージの呼び出しで指定されていない場合に、既定値を定義する新しい属性を nuget.exe ファイルに設定することもできます。 この値は、すべてのインストールパッケージ操作の [NuGet パッケージマネージャー] ダイアログでも尊重されます。 この値を設定するには、次の属性を nuget.exe ファイルに追加します。

    `<config> <add key="dependencyversion" value="Highest" /> </config>`
- **-WhatIf を使用した Nuget 操作のプレビュー**: いくつかの nuget パッケージは、深い依存関係グラフを持つことができます。そのため、インストール、アンインストール、または更新の操作中に、何が発生するかを最初に確認するのに役立ちます。 NuGet 2.8 は、標準の PowerShell を追加します。これは、コマンドが適用されるパッケージのクロージャ全体を視覚化できるように、パッケージ、アンインストール、および更新パッケージの各コマンドに切り替えます。
- **パッケージのダウングレード**: 新しい機能を調査し、最新の安定したバージョンにロールバックすることを決定するために、パッケージのプレリリース版をインストールすることは珍しくありません。 NuGet 2.8 より前では、これはプレリリースパッケージとその依存関係をアンインストールしてから、以前のバージョンをインストールする、複数の手順から成るプロセスでした。 ただし、NuGet 2.8 では、更新プログラムパッケージはパッケージのクロージャ全体 (パッケージの依存関係ツリーなど) を以前のバージョンにロールバックします。
- **開発の依存関係**: さまざまな種類の機能を NuGet パッケージとして提供できます。これには、開発プロセスの最適化に使用するツールが含まれます。 これらのコンポーネントは、新しいパッケージの開発に役立ちますが、後で公開するときに新しいパッケージの依存関係とは見なさないでください。 NuGet 2.8 では、パッケージを nuspec ファイル内で developmentDependency として識別できます。 このメタデータは、インストールすると、パッケージがインストールされたプロジェクトの app.config ファイルにも追加されます。 このパッケージの app.config ファイルが後で nuget の依存関係として分析されると、開発依存関係としてマークされた依存関係は除外されます。
- **さまざまなプラットフォームの個別のパッケージ .Config ファイル**: 複数のターゲットプラットフォーム用のアプリケーションを開発する場合、それぞれのビルド環境に対して異なるプロジェクトファイルを使用するのが一般的です。 さまざまなプロジェクトファイルで異なる NuGet パッケージを使用することもよくあります。パッケージには、プラットフォームごとに異なるレベルのサポートが用意されているためです。 NuGet 2.8 では、プラットフォーム固有のさまざまなプロジェクトファイルに対して異なるパッケージの .config ファイルを作成することによって、このシナリオのサポートが強化されています。
- **ローカルキャッシュへのフォールバック**: nuget パッケージは通常、ネットワーク接続を使用する[nuget ギャラリー](http://www.nuget.org)などのリモートギャラリーから使用されますが、クライアントが接続されていないシナリオは多数あります。 ネットワーク接続がないと、NuGet クライアントは、パッケージがローカルの NuGet キャッシュ内のクライアントコンピューターに既に存在する場合でも、パッケージを正常にインストールできませんでした。 NuGet 2.8 では、自動キャッシュフォールバックがパッケージマネージャーコンソールに追加されます。

    キャッシュフォールバック機能では、特定のコマンド引数は必要ありません。 さらに、現在、キャッシュフォールバックはパッケージマネージャーコンソールでのみ機能します。現在、[パッケージマネージャー] ダイアログボックスで動作は機能しません。
- **バグの修正**: 修正された主なバグの1つは、更新プログラムパッケージの再インストールコマンドでパフォーマンスが向上したことでした。

    これらの機能と上記のパフォーマンスの修正に加えて、この NuGet のリリースには他にも多くのバグ修正が含まれています。 リリースで解決された問題の合計は181でした。 NuGet 2.8 で修正された作業項目の完全な一覧については、このリリースの[Nuget Issue Tracker](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all)を参照してください。

<a id="webforms"></a>
### <a name="aspnet-web-forms"></a>ASP.NET Web Forms

- Web フォームテンプレートで、ASP.NET Identity のアカウントの確認とパスワードのリセットを実行する方法が示されるようになりました。
- Entity Framework 6 のエンティティデータソースコントロールと動的データプロバイダー。 詳細については、次の MSDN ブログを参照してください:[動的データ provider And EntityDataSource control for Entity Framework 6](https://blogs.msdn.com/b/webdev/archive/2014/01/30/announcing-preview-of-dynamic-data-provider-and-entitydatasource-control-for-entity-framework-6.aspx).

<a id="mvc"></a>
### <a name="aspnet-mvc-512"></a>ASP.NET MVC 5.1.2

- [属性ルーティングの機能強化](../../../mvc/overview/releases/mvc51-release-notes.md#AttributeRouting)
- [エディターテンプレートのブートストラップサポート](../../../mvc/overview/releases/mvc51-release-notes.md#Bootstrap)
- [ビューでの列挙のサポート](../../../mvc/overview/releases/mvc51-release-notes.md#Enum)
- [MinLength/MaxLength 属性の控えめなサポート](../../../mvc/overview/releases/mvc51-release-notes.md#Unobtrusive)
- [控えめ Ajax での ' this ' コンテキストのサポート](../../../mvc/overview/releases/mvc51-release-notes.md#thisContext)
- さまざまな[バグの修正](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=v5.1%20Preview%7cv5.1%20RTM&assignedTo=All&component=MVC&sortField=AssignedTo&sortDirection=Ascending&page=0&reasonClosed=Fixed)

<a id="webapi"></a>
### <a name="aspnet-web-api-212"></a>ASP.NET Web API 2.1.2

- [グローバルエラー処理](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#global-error)
- [属性ルーティングの機能強化](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#attribute-routing)
- [ヘルプページの機能強化](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#help-page)
- [IgnoreRoute のサポート](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#ignoreroute)
- [BSON メディア型フォーマッタ](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#bson)
- [非同期フィルターのサポートの強化](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#async-filters)
- [クライアントフォーマットライブラリのクエリ解析](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#query-parsing)
- さまざまな[バグの修正](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=v5.1%20Preview%7cv5.1%20RTM&assignedTo=All&component=Web%20API%7cWeb%20API%20OData&sortField=AssignedTo&sortDirection=Ascending&page=0&reasonClosed=Fixed)

<a id="webpages"></a>
### <a name="aspnet-web-pages-312"></a>ASP.NET Web ページ3.1.2

- さまざまな[バグの修正](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=v5.1%20Preview%7cv5.1%20RTM&assignedTo=All&component=Web%20Pages/Razor&sortField=AssignedTo&sortDirection=Ascending&page=0&reasonClosed=Fixed)

<a id="ef"></a>
### <a name="entity-framework-61"></a>Entity Framework 6.1

Entity Framework は、ランタイムとツールの両方のバージョン6.1 に更新されました。 Entity Framework (EF) 6.1 は Entity Framework 6 のマイナーアップデートであり、いくつかのバグ修正と新機能が含まれています。 新しい機能に関するドキュメントへのリンクなど、EF 6.1 の詳細については、「 [Entity Framework のバージョン履歴](https://msdn.microsoft.com/data/jj574253)」を参照してください。 このリリースの新機能は次のとおりです。

- **ツールの統合**により、新しい EF モデルを一貫した方法で作成できます。 この機能は、ADO.NET Entity Data Model ウィザードを拡張して、既存のデータベースからのリバースエンジニアリングを含む Code First モデルの作成をサポートします。 これらの機能は、以前は EF パワーツールのベータ品質で使用できました。
- **トランザクションのコミットエラーを処理**することで、新たに導入されたトランザクション操作をインターセプトする機能を利用する新しい system.string[ハンドラー](https://msdn.microsoft.com/library/system.data.entity.infrastructure.commitfailurehandler(v=vs.113).aspx)が提供されます。 **Commitfailurehandler**を使用すると、トランザクションのコミット中に、接続エラーからの自動復旧を行うことができます。
- **Indexattribute**を使用すると、Code First モデルのプロパティ (またはプロパティ) に属性を配置することで、インデックスを指定できます。 Code First によって、データベースに対応するインデックスが作成されます。
- **パブリックマッピング API は**、プロパティおよび型をデータベース内の列およびテーブルにマップする方法について、EF が使用する情報にアクセスできるようにします。 過去のリリースでは、この API は内部的でした。
- **アプリ/web.config ファイルを使用してインターセプターを構成する機能**(アプリケーションを再コンパイルせずにインターセプターを追加できるようにする)。
- **Databaselogger**は、すべてのデータベース操作をファイルに簡単に記録できる新しいインターセプターです。 以前の機能と組み合わせて使用すると、配置されたアプリケーションのデータベース操作のログ記録を簡単に切り替えることができ、再コンパイルする必要はありません。
- **移行モデル変更の検出**が改善され、スキャフォールディングの移行がより正確になりました。また、変更検出プロセスのパフォーマンスも大幅に向上しています。
- 初期化中のデータベース操作の削減、LINQ クエリでの null 等値比較の最適化、より多くのシナリオでのより高速なビュー生成 (モデルの作成)、複数のアソシエーションを持つ追跡対象エンティティのより効率的な具体化など、**パフォーマンスの向上**。

<a id="identity"></a>
### <a name="aspnet-identity-200"></a>ASP.NET Identity 2.0.0

- **2 要素認証**: ASP.NET Identity で2要素認証がサポートされるようになりました。 2要素認証を使用すると、パスワードが侵害された場合に、ユーザーアカウントにセキュリティレイヤーが追加されます。 2つの要素コードに対するブルートフォース攻撃も保護されています。
- **アカウントのロックアウト:** ユーザーがパスワードまたは2要素のコードを誤って入力した場合に、ユーザーをロックアウトする方法を提供します。 無効な試行の回数と、ユーザーがロックアウトされている期間を構成できます。 開発者は必要に応じて、特定のユーザーアカウントのアカウントロックアウトを無効にすることもできます。
- **アカウントの確認:** ASP.NET Identity システムでアカウントの確認がサポートされるようになりました。 これは、今日のほとんどの web サイトで非常に一般的なシナリオです。 web サイトに新しいアカウントを登録するときに、web サイトで何らかの処理を行う前に、電子メールを確認する必要があります。 電子メールの確認は、偽のアカウントが作成されないようにするために役立ちます。 これは、フォーラムサイト、銀行取引、電子商取引、ソーシャル web サイトなどの web サイトのユーザーとの通信方法として電子メールを使用する場合に非常に便利です。
- **パスワードのリセット:** パスワードリセットは、ユーザーがパスワードを忘れた場合にパスワードをリセットできる機能です。
- **セキュリティスタンプ (すべての場所でサインアウト):** ユーザーがパスワードを変更した場合、または関連付けられているログイン (Facebook、Google、Microsoft アカウントなど) を削除するなどのセキュリティ関連の情報を変更した場合に、ユーザーのセキュリティトークンを再生成する方法をサポートします。 これは、古いパスワードを使用して生成されたすべてのトークンが無効になるようにするために必要です。 サンプルプロジェクトでは、ユーザーのパスワードを変更すると、ユーザーに対して新しいトークンが生成され、以前のトークンは無効になります。 この機能により、アプリケーションのセキュリティが強化されます。パスワードを変更すると、このアプリケーションにログインしたすべての場所 (他のすべてのブラウザー) からログアウトされるようになります。
- **ユーザーおよびロールに対して主キーの種類を拡張できるよう**にします。 ASP.NET Identity 1.0 では、テーブルユーザーとロールの主キーの種類は文字列でした。 これは、ASP.NET Identity システムが Entity Framework を使用して SQL Server に永続化された場合に、nvarchar を使用していたことを意味します。 Stack Overflow でのこの既定の実装については多くの議論があり、受信したフィードバックに基づいています。 ユーザーとロールテーブルの主キーを指定できる機能拡張フックが用意されています。 この機能拡張フックは、アプリケーションを移行するときに、アプリケーションが Userid とを Guid または int として格納していた場合に特に便利です。
- **ユーザーとロールでの iqueryable のサポート**: ユーザーストアとロールストアの iqueryable のサポートが追加され、ユーザーとロールの一覧を簡単に取得できるようになりました。
- **UserManager を使用した削除操作のサポート**
- **ユーザー名でのインデックス作成**: ASP.NET Identity Entity Framework の実装では、EF 6.1.0 の新しい indexattribute を使用して、ユーザー名に一意のインデックスを追加しました。 これにより、ユーザー名が常に一意になり、競合状態が発生しなくなり、ユーザー名が重複してしまう可能性があります。
- **拡張パスワード検証コントロール:** ASP.NET Identity 1.0 に出荷されたパスワード検証コントロールは、最小長を検証するだけだった非常に基本的なパスワード検証コントロールでした。 パスワードの複雑さをより細かく制御できる新しいパスワード検証コントロールが用意されています。 このパスワードのすべての設定を有効にしたとしても、ユーザーアカウントに対して2要素認証を有効にすることをお勧めします。
- [Identity **Factory ミドルウェア]/[CreatePerOwinContext**]:

    - **ユーザーマネージャー**: ファクトリ実装を使用して、OWIN コンテキストから usermanager のインスタンスを取得できます。 このパターンは、サインインとサインアウトの OWIN コンテキストから AuthenticationManager を取得するために使用されるものと似ています。 これは、アプリケーションの要求ごとに UserManager のインスタンスを取得するために推奨される方法です。
    - **Dbcontextfactory**: ASP.NET Identity は SQL Server で id システムを永続化するために Entity Framework を使用します。 これを行うには、Id システムが ApplicationDbContext への参照を持っている必要があります。 DbContextFactory ミドルウェアは、アプリケーションで使用できる ApplicationDbContext のインスタンスを要求ごとに返します。
- サンプル**nuget パッケージ**: サンプル nuget パッケージを使用すると、ASP.NET Identity のサンプルのインストールと実行が容易になり、ベストプラクティスに従うことができます。 ASP.NET Identity これは、サンプルの ASP.NET MVC アプリケーションです。 運用環境にデプロイする前に、アプリケーションに合わせてコードを変更してください。 このサンプルは、空の ASP.NET アプリケーションにインストールする必要があります。 パッケージの詳細については、次のブログ記事「 [ASP.NET Identity 2.0.0 の RTM の発表](https://blogs.msdn.com/b/webdev/archive/2014/03/20/test-announcing-rtm-of-asp-net-identity-2-0-0.aspx)」を参照してください。

<a id="owin"></a>
### <a name="microsoft-owin-components"></a>Microsoft OWIN コンポーネント

このリリースで修正された多くのバグがありました。 詳細については、 [2.1.0 リリースのリリースノート](https://katanaproject.codeplex.com/releases/view/113281)を参照してください。

<a id="signalr"></a>
### <a name="aspnet-signalr-202"></a>ASP.NET SignalR 2.0.2

このリリースで修正された多くのバグがありました。 詳細については、 [2.0.2 リリースのリリースノート](https://github.com/SignalR/SignalR/releases/tag/2.0.2)を参照してください。
