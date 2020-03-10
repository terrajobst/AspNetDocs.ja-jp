---
uid: visual-studio/overview/2012/aspnet-and-web-tools-20131-for-visual-studio-2012
title: ASP.NET and Web Tools 2013.1 for Visual Studio 2012 のリリースノート |Microsoft Docs
author: microsoft
description: このドキュメントでは、Visual Studio 2012 用の ASP.NET and Web Tools 2013.1 のリリースについて説明します。
ms.author: riande
ms.date: 11/13/2013
ms.assetid: ca26e5bb-630e-41d2-8512-2a9386c431cb
msc.legacyurl: /visual-studio/overview/2012/aspnet-and-web-tools-20131-for-visual-studio-2012
msc.type: authoredcontent
ms.openlocfilehash: 260af1018064d60d80cbb1002001f28c4daffffd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467104"
---
# <a name="release-notes-for-aspnet-and-web-tools-20131-for-visual-studio-2012"></a>Visual Studio 2012 の ASP.NET と Web 2013.1 ツールのリリース ノート

[Microsoft](https://github.com/microsoft)

> このドキュメントでは、Visual Studio 2012 用の ASP.NET and Web Tools 2013.1 のリリースについて説明します。

## <a name="contents"></a>内容

- [インストールに関する注意事項](#install)
- [ソフトウェア要件](#requirements)
- ASP.NET and Web Tools 2013.1 の新機能 (Visual Studio 2012 用)

    - [Bootstrap](#bootstrap)
    - [テンプレート](#templates)

        - [ASP.NET MVC 5 テンプレート](#mvc5template)
        - [ASP.NET Web API 2 テンプレート](#apitemplate)
        - [項目テンプレート](#itemtemplate)
    - [Entity Framework 6](#ef6)
    - [ASP.NET スキャフォールディング](#scaffold)
    - [Razor エディター](#razor)
    - [NuGet 2.7](#nuget)
- 既知の問題と重大な変更

    - [ASP.NET スキャフォールディング](#issuescaffolding)

        - [MVC および Web API のスキャフォールディング-HTTP 404、見つからないエラー](#404issue)
        - [スキャフォールディング項目を追加した後、Web 用の Visual Studio Express 2012 が動作を停止する](#expressissue)
    - [ASP.NET Razor 3](#issuerazor)

        - [Browse を使用して、または F5 キーを使用して cshtml ファイルを表示すると、サーバーエラーが発生する](#browseissue)
        - [Url の書き換えとチルダ (~)](#rewriteissue)
    - [テンプレート](#templateissue)

<a id="install"></a>
## <a name="installation-notes"></a>インストールに関する注意事項

[インストール](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WebNode11Pack.appids)Visual Studio 2012 の場合は ASP.NET and Web Tools 2013.1。

<a id="requirements"></a>
## <a name="software-requirements"></a>ソフトウェア要件

Visual Studio 2012 を使用しているか、Web 用に Visual Studio Express 2012 が必要です。

## <a name="new-features-in-aspnet-and-web-tools-20131-for-visual-studio-2012"></a>ASP.NET and Web Tools 2013.1 の新機能 (Visual Studio 2012 用)

<a id="bootstrap"></a>
### <a name="bootstrap"></a>ブートストラップ

MVC 5 コントローラーとビューをスキャフォールディングした場合、ビューのマークアップでは[ブートストラップ](http://getbootstrap.com/)が使用されます。

<a id="templates"></a>
### <a name="templates"></a>テンプレート

<a id="mvc5template"></a>
#### <a name="aspnet-mvc-5-template"></a>ASP.NET MVC 5 テンプレート

新しい MVC 5 テンプレートを追加しました。 最新の MVC 5 NuGet パッケージを参照し、スキャフォールディングを使用してコントローラーとビューを追加できます。

<a id="apitemplate"></a>
#### <a name="aspnet-web-api-2-template"></a>ASP.NET Web API 2 テンプレート

新しい Web API 2 テンプレートを追加しました。 最新の Web API 2 NuGet パッケージを参照し、スキャフォールディングを使用してコントローラーとビューを追加できます。

<a id="itemtemplate"></a>
#### <a name="item-templates"></a>項目テンプレート

MVC 5 ビュー、Web ページ (Razor 3)、および Web API 2 コントローラー用の新しい項目テンプレートが追加されました。 新しい項目を追加するときに、関連する NuGet パッケージをプロジェクトにインストールします。

<a id="ef6"></a>
### <a name="entity-framework-6"></a>Entity Framework 6

Entity Framework を使用して MVC または Web API コントローラーをスキャフォールディングする場合は、フレームワーク6を使用します。 Entity Framework の詳細については、 [Entity Framework のバージョン履歴](https://msdn.com/data/jj574253)を参照してください。

Entity Framework 6 Tools for Visual Studio 2012 をダウンロードしてインストールすることもできます。 「 [Get Entity Framework](https://msdn.com/data/ee712906#tooling)」を参照してください。

<a id="scaffold"></a>
### <a name="aspnet-scaffolding"></a>ASP.NET スキャフォールディング

ASP.NET スキャフォールディングは、ASP.NET Web アプリケーションのコード生成フレームワークです。 これにより、データモデルと対話する定型コードをプロジェクトに簡単に追加できるようになります。

以前のバージョンの Visual Studio では、スキャフォールディングは ASP.NET MVC プロジェクトに限定されていました。 この更新プログラムでは、Web フォームを含む任意の ASP.NET プロジェクトにスキャフォールディングを使用できるようになりました。 この更新プログラムは、Web フォームプロジェクトのページの生成をサポートしていませんが、MVC の依存関係をプロジェクトに追加することで、Web フォームでスキャフォールディングを使用することができます。 Web フォームのページ生成のサポートは、今後の更新プログラムで追加される予定です。

スキャフォールディングを使用する場合は、必要なすべての依存関係がプロジェクトにインストールされていることを確認します。 たとえば、ASP.NET の Web フォームプロジェクトから開始し、スキャフォールディングを使用して Web API コントローラーを追加すると、必要な NuGet パッケージと参照がプロジェクトに自動的に追加されます。

MVC スキャフォールディングを Web フォームプロジェクトに追加するには、**新しいスキャフォールディング項目**を追加し、ダイアログウィンドウで **[Mvc 5 の依存関係]** を選択します。 MVC のスキャフォールディングには、2つのオプションがあります。最小と完全。 [最小] を選択すると、ASP.NET MVC の NuGet パッケージと参照のみがプロジェクトに追加されます。 [完全] オプションを選択した場合は、最小の依存関係だけでなく、MVC プロジェクトに必要なコンテンツファイルが追加されます。

非同期コントローラーのスキャフォールディングのサポートには、Entity Framework 6 の新しい非同期機能が使用されます。

詳細とチュートリアルについては、「 [ASP.NET スキャフォールディングの概要](../2013/aspnet-scaffolding-overview.md)」を参照してください。 これらのチュートリアルでは Visual Studio 2013 を使用したスキャフォールディングを示していますが、Visual Studio 2012 の ASP.NET and Web Tools 2013.1 にも適用できます。

<a id="razor"></a>
### <a name="razor-editor"></a>Razor エディター

この更新プログラムでは、Visual Studio 2012 で Razor 3 ツール/編集がサポートされるようになりました。

<a id="nuget"></a>
### <a name="nuget-27"></a>NuGet 2.7

NuGet 2.7 には新機能の豊富なセットが含まれています。詳細については、「 [nuget 2.7 のリリースノート](http://docs.nuget.org/docs/release-notes/nuget-2.7)」を参照してください。

このバージョンの NuGet では、不足しているパッケージの復元を NuGet に明示的に許可する必要がなくなります。 NuGet 2.7 をインストールすると、ユーザーは、不足しているパッケージを自動的に復元することに同意したことになります。 ユーザーは、Visual Studio の NuGet 設定を使用して、パッケージの復元を明示的に無効にすることができます。 この変更により、パッケージの復元のしくみが簡略化されます。

## <a name="known-issues-and-breaking-changes"></a>既知の問題と重大な変更

<a id="issuescaffolding"></a>
### <a name="aspnet-scaffolding"></a>ASP.NET スキャフォールディング

<a id="404issue"></a>
#### <a name="mvc-and-web-api-scaffolding---http-404-not-found-error"></a>MVC および Web API のスキャフォールディング-HTTP 404、見つからないエラー

スキャフォールディング項目をプロジェクトに追加するときにエラーが発生した場合は、プロジェクトが不整合な状態のままになる可能性があります。 スキャフォールディングに加えられた変更の一部はロールバックされますが、インストールされている NuGet パッケージなどのその他の変更はロールバックされません。 ルーティング構成の変更がロールバックされた場合、スキャフォールディング items に移動すると、ユーザーには HTTP 404 エラーが表示されます。

MVC のこのエラーを修正するには、新しいスキャフォールディング項目を追加し、[MVC 5 の依存関係] ([最小] または [完全]) を選択します。 このプロセスによって、必要なすべての変更がプロジェクトに追加されます。

このエラーを解決するには、次のように Web API を使用します。

1. 次の Webapiconfig.cs クラスをプロジェクトに追加します。

    [!code-csharp[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample1.cs)]

    [!code-vb[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample2.vb)]
2. 次に示すように、global.asax で Webapiconfig.cs をアプリケーション\_に構成します。

    [!code-csharp[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample3.cs)]

    [!code-vb[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample4.vb)]

<a id="expressissue"></a>
#### <a name="visual-studio-express-2012-for-web-stops-working-after-adding-a-scaffolded-item"></a>スキャフォールディング項目を追加した後、Web 用の Visual Studio Express 2012 が動作を停止する

Entity Framework (Web API 2 コントローラーなど) を使用してスキャフォールディング item を Entity Framework を使用して追加した後、Web 用の Visual Studio Express 2012 が動作しなくなった場合は、Visual Studio Express がアセンブリのネイティブイメージを読み込むことができなかった可能性があります。System.web. 拡張子に依存します。

この問題を解決するには、Visual Studio Express を構成して、次のようにします。

1. 管理者モードでコマンドプロンプトを開きます。
2. %ProgramFiles%\Microsoft Visual Studio 11.0 \ Common7\IDE または% ProgramFiles (x86)% \ Microsoft Visual Studio 11.0 \ Common7\IDE (64 ビット Windows の場合) にアクセスします。
3. テキストエディターで VWDExpress を開きます。
4. &lt;構成&gt;の下に次の行を追加し /&lt;runtime&gt; 要素を追加します。  

    [!code-xml[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample5.xml)]
5. Web 用に 2012 Visual Studio Express を再起動します。

<a id="issuerazor"></a>
### <a name="aspnet-razor-3"></a>ASP.NET Razor 3

<a id="browseissue"></a>
#### <a name="viewing-cshtml-file-with-browse-with-or-f5-causes-a-server-error"></a>Browse を使用して、または F5 キーを使用して cshtml ファイルを表示すると、サーバーエラーが発生する

Visual Studio 2012 で MVC 5 プロジェクトを作成した場合 (Visual Studio 2013 で作成された MVC 5 プロジェクトで Visual Studio 2012 を開いている場合)、Browse With または F5 を使用して cshtml ファイルを表示しようとすると、 **'/' アプリケーションで-Server error**というエラーが表示されます。 サーバーが `http://localhost:XXXX/Views/../XXXX.cshtml` に移動しようとしています

この問題を解決するには、プロジェクトの **[開始アクション]** 設定を [**特定] ページ**に変更します。 ページの値を指定する必要はありません。

![](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image1.png)

この変更を行った後、F5 キーを押すと、アプリケーションのルート (`http://localhost:XXXX`) に移動します。 この動作は Visual Studio 2013 の MVC 5 プロジェクトの動作と同じではありません。**現在のページ**の設定によって、開いているページが起動します。

<a id="rewriteissue"></a>
#### <a name="url-rewrite-and-tilde"></a>Url の書き換えとチルダ (~)

ASP.NET Razor 3 または ASP.NET MVC 5 にアップグレードした後、URL リライトを使用していると、チルダ (~) 表記が正しく機能しなくなる可能性があります。 URL 書き換えは、&lt;A/&gt;、&lt;SCRIPT/&gt;、&lt;LINK/&gt;などの HTML 要素のチルダ (~) 表記に影響します。その結果、チルダはルートディレクトリにマップされなくなります。

たとえば、 **asp.net/content**の要求を**asp.net**に書き換えると、href = "~/content/"/&gt; &lt;の href 属性は、 **/** ではなく、/ **content/content/** に解決されます。 この変更を行わないようにするには、各 Web ページまたは**アプリケーション\_BeginRequest**内の**IIS\_** にある、IIS によって書き換えられたコンテキストを false に設定します。

<a id="templateissue"></a>
### <a name="templates"></a>テンプレート

Windows 8.1 または Windows Server 2012 R2 で Visual Studio 2012 を使用して ASP.NET MVC プロジェクトを作成すると、Visual Studio に "ASP.NET 4.5 の Web [url] の構成に失敗しました" というエラーメッセージが表示されます。

![構成エラー](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image2.png)

このエラーが表示されるのは、Visual Studio 2012 では、ASP.NET 4.5 機能が Windows のこれらのリリースにインストールされている場合には有効にならないためです。 ASP.NET 4.5 を有効にするには、「 [Windows の機能の有効化または無効化](https://windows.microsoft.com/windows-8/turn-windows-features-on-off)」で説明されている手順を実行します。

![Windows の機能を有効または無効にする](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image3.png)

または、コマンドラインを使用して ASP.NET 4.5 を有効にすることもできます。

1. 管理者モードでコマンドプロンプトを開きます。
2. 次のコマンドを実行して、ASP.NET 4.5 を有効にします。  
    `dism /Online /Enable-Feature /FeatureName:NetFx4Extended-ASPNET45 /Quiet /NoRestart`
