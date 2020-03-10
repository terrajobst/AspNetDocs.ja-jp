---
uid: web-pages/readme/overview
title: WebMatrix の Readme |Microsoft Docs
author: rick-anderson
description: WebMatrix および ASP.NET Web Pages (Razor) 1.0 リリースの Readme
ms.author: riande
ms.date: 01/06/2011
ms.assetid: 36c5beeb-45a7-48a0-9c30-f82cdf5c5f5f
msc.legacyurl: /web-pages/readme
msc.type: content
ms.openlocfilehash: fac53e935860a90d8f2aa96699d56d66ade3a40f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78454270"
---
# <a name="webmatrix-readme"></a>WebMatrix Readme

2011年1月13日

## <a name="contents"></a>内容

> [!NOTE]
> この readme は、WebMatrix の1.0 リリースに適用されます。

- [概要](#Overview)
- [インストール](#Installation_Notes)
- [アプリケーションを発行する方法](#InstructionsForPublishingApplications)
- [変更と懸案事項](#ChangesAndIssues)

    - [WebMatrix 1.0 のインストール](#Known_Issues_Installation)
    - [ASP.NET Web ページ](#Known_Issues_ASPNET)
    - [WebMatrix](#Known_Issues_WebMatrix)
    - [IIS Express](#Known_Issues_IISExpress)
    - [SQL Server Compact](#Known_Issues_SQLServerCompact)
    - [アプリケーションのインストール](#Known_Issues_Installing_Applications)
    - [アプリケーションの発行](#Known_Issues_Publishing_Applications)
- [参照項目](#More_Info)

<a id="Overview"></a>

## <a name="overview"></a>概要

> WebMatrix は、わずか数分でインストール可能な無償の Web 開発ツールです。 データベースとプログラミングのフレームワークに Web サーバーを組み合わせることによって、1 つの統合的な環境を実現します。 WebMatrix では、独自の ASP.NET または PHP Web サイトを効率よくコーディング、テスト、発行することができるほか、広く普及しているオープン ソース アプリケーション (DotNetNuke、Umbraco、WordPress、Joomla など) をベースにして、新しい Web サイトを作成することもできます。 WebMatrix には、インターネット上で Web サイトを実行するものと同じ強力な Web サーバー、データベース エンジン、フレームワークが使用されているため、開発環境から実稼働環境への円滑かつシームレスな移行が可能です。

<a id="Installation_Notes"></a>

## <a name="installation"></a>インストール

> WebMatrix 1.0 をインストールするには、最初に[Microsoft Web Platform Installer 3.0](https://go.microsoft.com/fwlink/?LinkID=194638)をインストールする必要があります。 まず Web Platform Installer のインストールし、それを使用して WebMatrix をインストールすることになります。
> 
> インストール中に問題が発生した場合は、「 [Microsoft Web Platform Installer に関する問題のトラブルシューティング](https://go.microsoft.com/fwlink/?LinkId=196212)」を参照してください。

<a id="InstructionsForPublishingApplications"></a>
## <a name="how-to-publish-applications"></a>アプリケーションの発行方法

> [アプリケーションを公開するための詳細な手順を確認する](https://go.microsoft.com/fwlink/?LinkID=196149)

<a id="ChangesAndIssues"></a>

## <a name="changes-and-issues"></a>変更点と問題

<a id="Known_Issues_Installation"></a>

### <a name="webmatrix-10-installation-issues"></a>WebMatrix 1.0 のインストールの問題

#### <a name="issue-webmatrix-10-is-available-only-on-platforms-that-support-microsoft-net-framework-4"></a>問題: Microsoft .NET Framework 4 をサポートするプラットフォームでしか WebMatrix 1.0 は使用できない

> WebMatrix には .NET Framework Version 4 が必須です。 特定の条件が揃うと、サポートされたプラットフォーム構成でないにもかかわらず、WebMatrix 1.0 インストーラーが先に進む場合があります。 たとえば、SP1 更新プログラムが適用されていない Windows Vista では、WebMatrix のインストールが正常に開始されますが、.NET Framework 4 コンポーネントでエラーが発生し、インストールはブロックされます。
> 
> **回避策**  
> サポートされているプラットフォームにインストールします。サポート対象のプラットフォームは次のとおりです。
> 
> - Windows 7
> - Windows Server 2008
> - Windows Server 2008 R2
> - Windows Vista SP1 以降
> - Windows XP SP3
> - Windows Server 2003 SP2

#### <a name="issue-cannot-install-webmatrix-10-if-microsoft-visual-studio-2008-is-installed-without-microsoft-visual-studio-2008-sp1"></a>問題: Microsoft Visual Studio 2008 が SP1 未適用の状態でインストールされていると WebMatrix 1.0 をインストールできない

> **回避策**  
> Microsoft ダウンロードセンターから[Microsoft Visual Studio 2008 SP1](https://www.microsoft.com/downloads/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en)をインストールします。

#### <a name="issue-some-assemblies-for-sql-server-compact-40-are-not-installed-in-the-gac"></a>問題: SQL Server Compact 4.0 のアセンブリの一部が GAC にインストールされない

> SQL Server Compact 4.0 を 64 ビット コンピューターにインストールする際、そのコンピューターに .NET Framework 3.5 SP1 Client Profile しかインストールされていないと、SQL Server Compact 4.0 のマネージド アセンブリがグローバル アセンブリ キャッシュ (GAC) に配置されません。 GAC にインストールされないマネージド アセンブリは次のとおりです。
> 
> - *System.data.sqlserverce* (ADO.NET provider) (システムプロバイダー)
> - *System.data.sqlserverce* (ADO.NET) (Entity Framework)
> 
> **回避策**  
> SQL Server Compact 4.0 をアンインストールします。 次の場所から完全バージョンの .NET Framework 3.5 SP1 をダウンロードしてインストールします。  
>   
> [Microsoft .NET Framework 3.5 Service pack 1 (フルパッケージ)](https://go.microsoft.com/fwlink/?LinkId=194828)  
>   
> そのうえで SQL Server Compact 4.0 を再インストールします。

#### <a name="issue-cannot-uninstall-sql-server-compact-using-the-command-line"></a>問題: コマンド ラインを使用して SQL Server Compact をアンインストールすることはできない

> このリリースでは、コマンド ライン オプションを使用して SQL Server Compact をアンインストールすることはできません。
> 
> **回避策**  
> Windows のコントロールパネルの [*プログラムと機能*] を使用して、Microsoft SQL Server Compact 4.0 をアンインストールします。

<a id="Known_Issues_ASPNET"></a>

### <a name="aspnet-web-pages"></a>ASP.NET Web Pages

ここでは、Razor 構文を使用した ASP.NET Web Pages 1.0 リリースの新機能、変更点、および既知の問題について説明します。

- [新機能](#NewFeatures)
- [[変更点]](#Changes)
- [問題](#Issues)

#### <a id="NewFeatures"></a>新機能

#### <a name="new-configuration-setting-added-to-disable-the-package-manager"></a>新機能: パッケージ マネージャーを無効にするための構成設定を追加

> *Web.config ファイルの*`<appSettings>` 要素に新しい `asp:AdminManagerEnabled` キーを使用できます。これにより、パッケージマネージャーを完全に無効にすることができます。 この要素の既定値は true です。これは、 *web.config ファイルに*含まれていない場合、パッケージマネージャーが有効になっていることを意味します。 パッケージマネージャーを無効にするには、 *web*サイトのルートにある web.config ファイルに次の要素を追加します。
> 
> [!code-xml[Main](overview/samples/sample1.xml)]

#### <a id="Changes"></a>変化

#### <a name="change-webpagesadminfoldervirtualpath-key-renamed-to-aspadminfoldervirtualpath"></a>変更点: "webPages:AdminFolderVirtualPath" キーの名前を "asp:AdminFolderVirtualPath" に変更

> パッケージマネージャーの場所を指定するために*web.config ファイルに*追加できる `webPages:AdminFolderVirtualPath` キーは、`webPages` 名前空間ではなく `asp:` 名前空間を使用するように名前が変更されました。 この要素を使用している場合は、構成ファイルで名前を変更する必要があります。

#### <a id="Issues"></a> 既知の問題

#### <a name="issue-passwords-for-membership-users-no-longer-recognized"></a>問題: メンバーシップ ユーザーのパスワードが認識されなくなった

> セキュリティを強化するため、メンバーシップ (ログイン) パスワードの作成と保存のアルゴリズムが変更されました。 その結果、ASP.NET Razor のベータ版で作成されたメンバー (ユーザー) 用に保存されたパスワードは認識されなくなります。 
> 
> **回避策**サイトがまだ運用環境に配置されていない場合は、メンバーシップデータベースからユーザーレコードを削除します。 データベースが有効な場合は、プログラムによってメンバーシップデータベース内の既存のパスワードを再生成します。

#### <a name="issue-unexpected-behavior-when-using-a-custom-user-table-for-membership"></a>問題: メンバーシップ用のカスタム ユーザー テーブルを使用しているときに予期しない動作が生じる

> ASP.NET Razor web サイトのメンバーシッププロバイダーを初期化するには、`WebSecurity.InitializeDatabaseConnection` メソッドを呼び出します。 (WebMatrix では、スターターサイトテンプレートには、 *\_該当*ファイルにこのメソッドの呼び出しが含まれています)。このメソッドの `autoCreateTables` パラメーターが true に設定されている場合 (既定では、スタートサイトテンプレートで true に設定されています)、認識できないテーブル名がメソッドに渡された場合 (2 番目のパラメーター)、メソッドはエラーをスローしません。 エラーがスローされずに、自動的にテーブルが作成されます。
> 
> メンバーシップにカスタムユーザーテーブルを使用するが、間違ったテーブル名を `WebSecurity.InitializeDatabaseConnection` メソッドに渡す場合は、この問題が発生する可能性があります。 指定したテーブルが存在しなかったとしても、既定ではメソッドからエラーが生成されません。新しいテーブルが作成されるため、アプリケーションは一見、正常に機能しているように見えます。 しかし、最終的には、カスタム ユーザー テーブル (とそのテーブル内のフィールド) に依存しているアプリケーション コードで予期しないエラーが発生します。
> 
> **回避策**  
> `InitializeDatabaseConnection` メソッドで渡された名前がメンバーシップデータベースのユーザープロファイルテーブルと一致していることを確認するか、`autoCreateTables` パラメーターが false に設定されていることを確認してください。

#### <a name="issue-error-message-the-admin-module-requires-access-to-app_data"></a>問題: "管理者モジュールは、~/アプリの\_データへのアクセスが必要です" というエラーメッセージが表示される

> 状況によっては、ユーザーを作成しようとしたり、ASP.NET メンバーシップシステムを使用しようとしたりすると、ページには、*管理モジュールからアプリケーション\_データへのアクセスが必要に*なるというエラーが表示されることがあります。 これは、IIS または IIS Express が実行されているアカウントに、web サイトのルートにある*アプリ\_Data*フォルダーに対して作成および書き込みを行うためのアクセス許可がない場合に発生します。 
> 
> **回避策**Web サイトの*アプリ\_データ*フォルダーを手動で作成します。 次に、アプリケーションを実行する Windows アカウント (通常は NETWORK SERVICE) に、アプリケーションのルートフォルダーと、アプリの\_データなどのサブフォルダーに対する読み取り/書き込みアクセス許可が付与されていることを確認します。 詳細については、サポート技術情報の記事「 [SQL Server Express ユーザーインスタンスと ASP.net Web アプリケーションプロジェクトに関する問題](https://support.microsoft.com/kb/2002980)」を参照してください。

#### <a name="issue-failed-to-generate-a-user-instance-of-sql-server-error"></a>問題: "SQL Server のユーザー インスタンスを生成できませんでした" というエラーが表示される

> WebMatrix Web アプリケーションに SQL Server Express が使用されており、Windows 7 または Windows Server 2008 R2 で IIS 7.5 が実行されている場合、ユーザーのローカル アプリケーション パスを SQL Server が実行時に取得できないことを示すエラーが表示される場合があります。
> 
> **回避策**アプリケーションが実行されている Windows アカウント (通常は NETWORK SERVICE) に、アプリケーションのルートフォルダーと、*アプリの\_データ*などのサブフォルダーに対する読み取り/書き込みアクセス許可があることを確認します。 詳細については、サポート技術情報の記事「 [SQL Server Express ユーザーインスタンスと ASP.net Web アプリケーションプロジェクトに関する問題](https://support.microsoft.com/kb/2002980)」を参照してください。

#### <a name="issue-files-that-contains-package-manager-resources-or-package-manager-passwords-are-servable-under-iis-60-and-earlier"></a>問題: IIS 6.0 以前の環境でパッケージ マネージャーのリソースまたはパスワードを含んだファイルが返される

> RC2 リリースを使用してビルドされた ASP.NET Web ページ (Razor) アプリケーションを配置する場合、アプリケーションの packagesources に、 */App\_Data/admin*の下に*パスワード .txt*またはファイルが含まれていると、IIS 6.0 は要求された場合にファイルを提供し、パッケージマネージャーインスタンスのパスワードを公開する可能性があります。 
> 
> **回避策***パスワード .txt*または*packagesources*ファイルの名前を packagesources または*に変更*します。既定では、IIS 6.0 は *.config*拡張子を持つファイルを提供しません。 (IIS 7 では、 *App\_Data*フォルダー内のファイルは提供されないため、ファイルの名前を変更する必要はありません)。

#### <a name="issue-uninstalling-packages-installed-using-the-beta-3-release-does-not-completely-remove-package-components"></a>問題: Beta 3 リリースを使用してインストールしたパッケージをアンインストールしても、パッケージのコンポーネントが完全には削除されない

> Beta 3 リリースのパッケージ マネージャーを使用してインストールされたパッケージを、現在のリリースを使用してアンインストールしようとすると、完全にはパッケージがアンインストールされません。 パッケージマネージャーの **[アンインストール]** ボタンを使用すると、一部のコンポーネントが削除されますが、パッケージのライブラリコードは残され、*パッケージの .config*ファイルは更新されません。
> 
> **回避策**   
> 次の手順を実行します。  
> 1. *アプリ\_Data\packages*フォルダーを削除します。 これにより、すべてのパッケージが削除されます。   
> 2. Web サイトのルートにある*パッケージの .config*ファイルを削除します。

#### <a name="issue-in-visual-studio-invoking-the-web-based-package-manager-takes-the-application-offline"></a>問題: Visual Studio で Web ベースのパッケージ マネージャーを呼び出すとアプリケーションがオフラインになる

> (WebMatrix ではなく) Visual Studio で作業していて、 *\_管理*機能を使用してパッケージマネージャーを起動している場合、visual studio はアプリケーションをオフラインにし、web サイトルートに*アプリ\_* を送信します。これにより、パッケージマネージャーを使用する機能が中断されます。
> 
> [!NOTE]
> ほとんどの場合、web ベースのパッケージマネージャーインターフェイスを使用しているときにこの動作が表示されますが、 *App\_Data*フォルダー内のファイルを追加、削除、または変更すると、同じ動作が発生します。
> 
> **回避策**   
> Visual Studio でパッケージを扱う場合は、Web ベースのパッケージ マネージャーではなく、NuGet 拡張機能を使用します。 詳細については、 [NuGet のドキュメント](https://docs.microsoft.com/nuget/)を参照してください。 *App\_Data*フォルダー内の他のファイルを操作する場合は、この問題を回避するためにファイルを他の場所に保持することを検討してください。 これが現実的でない場合は、*アプリ\_オフライン .htm*ファイルを手動で削除するか、サイトが自動的にオンラインに戻るまで待機します (既定では30秒後)。

#### <a name="issue-visual-studio-intellisense-and-project-templates-available-only-in-aspnet-mvc-version-3"></a>問題: Visual Studio IntelliSense およびプロジェクト テンプレートは ASP.NET MVC Version 3 でしか利用できない

> ASP.NET Web Pages をインストールしても Visual Studio 用のツール (ASP.NET Web Pages アプリケーション用のプロジェクト テンプレート、IntelliSense など) はインストールされません。
> 
> **回避策**Visual Studio で ASP.NET Web ページアプリケーションの IntelliSense とプロジェクトテンプレートを使用するには、Web Platform Installer または[スタンドアロンインストーラー](https://go.microsoft.com/fwlink/?LinkID=191797)を使用して ASP.NET MVC 3 RC をインストールします。

#### <a name="issue-reading-feeds-or-other-external-data-via-a-proxy-server"></a>問題: フィードなどの外部データをプロキシ サーバーから読み取る

> サイトを実行しているサーバーがプロキシサーバーの背後にある場合は、サイトの外部からの情報を読み取ることができるよう*に、web.config ファイルに*プロキシ情報を構成することが必要になる場合があります。 たとえば、`ReCaptcha` ヘルパーを使用する場合、ヘルパーは reCAPTCHA サービスと通信しますが、プロキシサーバーによってブロックされる可能性があります。 同様に、ASP.NET Web Pages で使用されているフィード (パッケージ マネージャーによって使用されているフィードなど) にもプロキシ構成が必要となることがあります。
> 
> 外部サービスの操作中またはパッケージフィードの操作で問題が発生した場合は、アプリケーションのルート*web.config*ファイルに次の要素を追加します。
> 
> [!code-xml[Main](overview/samples/sample2.xml)]
> 
> プロキシサーバーの構成の詳細については、MSDN Web サイトの「 [&lt;proxy&gt; 要素 (ネットワーク設定)](https://msdn.microsoft.com/library/sa91de1e.aspx) 」を参照してください。

#### <a name="issue-uninstalling-the-net-framework-version-4-disables-aspnet-web-pages-with-razor-syntax"></a>問題: .NET Framework  Version 4 をアンインストールすると Razor 構文を使用する ASP.NET Web Pages が無効になる

> .NET Framework  Version 4 をアンインストールして再インストールした場合、Razor 構文を使用する ASP.NET Web Pages は無効になります。 拡張子が*cshtml*のページは正しく動作しません。 ASP.NET Web ページは、アセンブリをコンピューターのルート*web.config*ファイルに登録し、.NET Framework を削除するとそのファイルが削除されます。 .NET Framework を再インストールすると、新しいバージョンの構成ファイルがインストールされますが、ASP.NET Web Pages アセンブリに対する参照は追加されません。
> 
> **回避策**.NET Framework を再インストールした後、Razor 構文で ASP.NET Web ページを再インストールします。 これにより、コンピュータールートの*web.config ファイルに*次の要素が追加されます。通常は次の場所にあります。  
> 
> `C:\Windows\Microsoft.NET\Framework\v4.0.30319\Config (32-bit)`  
> `C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config (64-bit)`
> 
> [!code-xml[Main](overview/samples/sample3.xml)]

#### <a name="issue-extensionless-urls-do-not-find-cshtmlvbhtml-files-on-iis-7-or-iis-75"></a>Issue: Extensionless URLs do not find .cshtml/.vbhtml files on IIS 7 or IIS 7.5

> IIS 7 または IIS 7.5 では、次のような URL の要求は、拡張子が*cshtml*または*vbhtml*のページを見つけることができません。  
> 
> `http://www.example.com/ExampleSite/ExampleFile`  
> 
> IIS 7 または IIS 7.5 では URL の書き換えが既定で有効になっていないため、この問題が発生します。 Likeliest シナリオでは、IIS Express を使用してローカルでテストするときに問題が発生することはありませんが、web サイトをホストする web サイトにデプロイするときにこの問題が発生します。
> 
> **回避策**
> 
> - サーバーコンピューターを制御している場合は、サーバーコンピューターで、更新プログラムに記載されている更新プログラムをインストールします。この更新プログラムは[、特定の iis 7.0 または iis 7.5 ハンドラーが、url の末尾がピリオドではない要求を処理](https://support.microsoft.com/kb/980368)できるようにします。
> - サーバーコンピューターを制御できない場合は (たとえば、ホスティング web サイトに配置する場合)、 *web*サイトの web.config ファイルに次のコードを追加します。 
> 
>     [!code-xml[Main](overview/samples/sample4.xml)]

#### <a name="issue-deploying-an-application-to-a-computer-that-does-not-have-sql-server-compact-installed"></a>問題: SQL Server Compact がインストールされていないコンピューターにアプリケーションを展開する

> SQL Server Compact データベースを含むアプリケーションは、SQL Server Compact がインストールされていないコンピューターで実行できます。 Microsoft WebMatrix 1.0 は、これらのバイナリを自動的にコピーし *、適切な web.config ファイル*変換を実行します。
> 
> **回避策**これらのファイルをコピーし*て、web.config ファイルを*手動で変更する必要がある場合は、次の手順を実行します。
> 
> 1. データベースエンジンアセンブリを、ターゲットコンピューター上のアプリケーションの*Bin*フォルダー (およびサブフォルダー) にコピーします。  
> 
>    - *SQL Server C:\Program Edition\v4.0\Desktop\System.Data.SqlServerCe.dll*をコピー   
>      **to** *\bin*
>    - *SQL Server Compact C:\Program Edition\v4.0\Private\x86\\* **を** *\Bin\x86*にコピーします。
>    - *SQL Server Compact C:\Program Edition\v4.0\Private\amd64\\* * を \Bin\amd64**にコピーし**ます。
> 
> 2. *Web*サイトのルートフォルダーで、web.config ファイルを作成するか、開きます。 (WebMatrix 1.0 では、 **[ファイルの種類の選択]** ダイアログボックスで **[すべて]** をクリックすると、このファイルの種類が使用可能になります)。
> 3. 次の要素を `<configuration>` 要素の子として追加します (`<system.web>` 要素内ではありません)。
> 
>     [!code-xml[Main](overview/samples/sample5.xml)]

#### <a name="issue-database-and-webgrid-helpers-do-not-work-in-medium-trust-in-visual-basic"></a>問題点: "Database" および "WebGrid" のヘルパーは、Visual Basic の中程度の信頼では機能しません

> Visual Basic ( *vbhtml*ファイルの作成) を使用している場合、アプリケーションが中程度の信頼を使用するように設定されていると、`Database` と `WebGrid` のヘルパーは機能しません。
> 
> **回避策**  
> Visual Studio 2010 を使用している場合は、Service Pack 1 のリリースをインストールすることで、この問題を解決できます。 SP1 リリースの最終版が利用可能になるまでは、Microsoft ダウンロードセンターの[Microsoft Visual Studio 2010 Service Pack 1 Beta](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=11ea69cb-cf12-4842-a3d7-b32a1e5642e2&amp;displaylang=en)のページからベータ版の sp1 をダウンロードできます。   
>   
> これが現実的でない場合、または Visual Studio 2010 を使用していない場合は、アプリケーションを一時的に完全信頼を使用するように設定できます。

#### <a name="issue-applicationpart-resources-are-externally-accessible"></a>問題: "ApplicationPart" リソースに外部からアクセスできる

> アセンブリに `ApplicationPart` クラスから派生したオブジェクトが含まれている場合、そのアセンブリのリソースは `ResourceRouteHandler` クラスによって公開されます。 たとえば、次のような URL があるとします。  
>   
> `~/r.ashx/System.Web.WebPages.Administration/Resources/AdminResources.resources`  
>   
> この要求は、すべてのリソース文字列を*system.web. Web ページの管理*アセンブリにダウンロードします。 すべての埋め込みリソース (静的コンテンツとして提供される予定ではないものも含む) がダウンロードされます。 埋め込みリソースに機密情報が含まれている場合は、セキュリティ上のリスクが生じる可能性があります。 
> 
> **回避策**   
> **Applicationpart**オブジェクトを作成する場合は、その**applicationpart**オブジェクトのアセンブリに関連付けられている埋め込みリソースに機密情報が含まれていないことを確認してください。

<a id="Known_Issues_WebMatrix"></a>

### <a name="webmatrix"></a>WebMatrix

> [!NOTE]
> WebMatrix のインストールに関する問題の詳細については、このドキュメントの「 [webmatrix のインストールに関する問題](#Known_Issues_Installation)」を参照してください。

ドキュメントのこのセクションでは、WebMatrix 開発環境に関する既知の問題について説明します。

#### <a name="issue-changes-in-the-username-or-password-of-a-database-connection-string-in-a-webconfig-file-are-not-reflected-in-the-databases-workspace"></a>問題点: web.config ファイルのデータベース接続文字列のユーザー名またはパスワードの変更は、[データベース] ワークスペースに反映されません。

> **回避策**  
> 
> 1. *Web.config ファイルで*、接続文字列のデータベース名を変更します (たとえば、"1" を追加します)。
> 2. *Web.config ファイルを*保存します。
> 3. [**データベース**と更新] をクリックします。
> 4. *Web.config*ファイルの接続文字列でデータベース名を元のデータベース名に変更します。
> 5. *Web.config ファイルを*保存します。
> 6. [**データベース**と更新] をクリックします。

#### <a name="issue-folders-created-by-webmatrix-cannot-be-deleted"></a>問題: WebMatrix によって作成されたフォルダーを削除することはできません

> 高度なアクセス許可を使用して WebMatrix が実行されている場合 (つまり、Windows の **[管理者として実行]** オプションを使用して webmatrix を開始した場合)、webmatrix によって作成されたフォルダーをエクスプローラーを使用して削除することはできません。
> 
> **回避策**  
> 昇格されたアクセス許可を使用してエクスプローラーを実行します。 次の手順に従います。  
> 
> 1. Windows で、 **[開始]** をクリックします。
> 2. 「Windows Explorer」と入力し、**エクスプローラー**のエントリを右クリックします。
> 3. **[管理者として実行]** をクリックします。 その後、フォルダーを削除できます。

#### <a name="issue-webmatrix-10-is-unable-to-perform-certain-tasks-that-require-elevation"></a>問題: WebMatrix 1.0 は、昇格が必要な特定のタスクを実行できない

> WebMatrix 1.0 は、次の状況での追加コンポーネントのインストールなど、昇格が必要な特定のタスクを実行できません。
> 
> - Windows Vista または Windows 7 では、管理者特権を持たないアカウントを使用してログインし、ユーザーアカウント制御 (UAC) が無効になっています。
> - Microsoft Windows XP または Microsoft Windows Server 2003 を使用している。
> 
> **回避策**  
> WebMatrix 1.0 のほとんどのタスクには、管理者権限は必要ありません。 そのためには、管理者として操作を実行するか、次の手順に従います。
> 
> - Windows Vista または Windows 7 では、UAC を有効にします。
> - Windows XP では、ユーザーを管理者セキュリティグループに追加します。

#### <a name="issue-site-from-web-gallery-is-disabled"></a>問題: "Web ギャラリーからのサイト" が無効になっています

> Web Platform Installer 3.0 がインストールされていない場合、 **[Web ギャラリーからのサイト]** オプションは無効になっています。
> 
> **回避策**  
> [Microsoft Web Platform Installer 3.0](https://go.microsoft.com/fwlink/?LinkID=194638)をインストールします。

#### <a name="issue-google-chrome-is-not-available-as-a-run-option"></a>問題: Google Chrome は Run オプションとして使用できません

> Google Chrome は、 **[ホーム]** タブの **[実行]** にあるブラウザーの一覧に表示されません。
> 
> **回避策**  
> Google Chrome の一部のバージョンは、Windows の既定のプログラム機能に正しく登録されません。 回避策として、Google Chrome を起動し、[ *Google chrome* ] メニューをクリックして、[*オプション*] をクリックし、[ *google chrome の既定のブラウザーを作成*する] をクリックします。

#### <a name="issue-the-foreign-key-dialog-box-doesnt-allow-entering-a-primary-key"></a>問題点: [外部キー] ダイアログボックスで主キーを入力できない

> **[外部キー]** ダイアログボックスでは、主キーテーブルの主キーの名前を入力することはできません。
> 
> **回避策**  
> これは意図的なものであり、 主キーテーブルの主キーの名前を入力する必要はありません。

#### <a name="issue-intellisense-is-not-available-in-webmatrix-for-razor-syntax-c-or-visual-basic"></a>問題: Razor 構文、、またはの WebMatrix ではC#、IntelliSense を使用できません Visual Basic

> HTML および CSS では、IntelliSense が WebMatrix でサポートされています。 ただし、他の言語では使用できません。 
> 
> **回避策**   
> [なし] :

#### <a name="issue-intellisense-for-html-and-css-suggests-elements-that-are-not-contextually-appropriate"></a>問題点: HTML および CSS 用の IntelliSense は、文脈に適していない要素を提案します。

> WebMatrix のマークアップ用の IntelliSense では、 [css 2.1 スキーマ](http://www.w3.org/TR/CSS2/)を使用した[XHTML 1.0 移行スキーマ](http://www.w3.org/TR/2002/NOTE-xhtml1-schema-20020902/#xhtml1-transitional)と css を使用した HTML がサポートされます。 IntelliSense はこれらの特定のスキーマに基づいているため、特定のタグ、属性、またはプロパティが、現在のページまたはスタイル定義に適していない可能性があります。 HTML の場合は、不適切な形式の XHTML として解釈される可能性があるコンテンツ (タグが閉じられていない場合など) に予期しない候補が表示されることもあります。 挿入ポイントが不完全なタグ内にある場合、この問題はさらに顕著になる可能性があります。その場合は、IntelliSense によって新しい開始タグが提示されるか、またはその他の不適切な候補が提示されます。 
> 
> **回避策**   
> HTML の場合は、整形式の完全な XHTML ページ内で作業していることを確認してください。 CSS の場合、回避策はありません。

#### <a name="issue-intellisense-is-not-invoked-while-you-type"></a>問題: 入力中に IntelliSense が呼び出されない

> 場合によっては、エディターに HTML または CSS が入力されているときに IntelliSense が呼び出されないことがあります。 特に、挿入ポイントが別の要素の横、またはファイルの末尾にある場合に発生する可能性があります。 
> 
> **回避策**   
> 挿入ポイントの周囲に空白があること、および挿入ポイントがファイルの末尾にないことを確認します。 Ctrl キーを押しながら Space キーを押すと、IntelliSense を手動で呼び出すこともできます。

#### <a name="issue-no-ui-is-available-for-disabling-intellisense"></a>問題: IntelliSense を無効にするための UI が使用できない

> WebMatrix 1.0 では、IntelliSense を無効にするための UI やジェスチャは提供されません。 
> 
> **回避策**   
> 次のコマンドを使用して WebMatrix を開始します。これには、IntelliSense を無効にするスイッチが含まれています。  
>   
> `WebMatrix.exe #ExecuteCommand# EditorIntelliSense off`

<a id="Known_Issues_IISExpress"></a>
### <a name="iis-express"></a>IIS Express

IIS Express には、次の URL から入手できる独自の readme ファイルがあります。

[https://go.microsoft.com/fwlink/?LinkID=207675&amp; clcid = 0x411](https://go.microsoft.com/fwlink/?LinkID=207675&amp;clcid=0x409)

<a id="Known_Issues_SQLServerCompact"></a>

### <a name="sql-server-compact"></a>SQL Server Compact

SQL Server Compact には、次の URL から入手できる独自の readme ファイルがあります。

[https://go.microsoft.com/fwlink/?LinkID=208545](https://go.microsoft.com/fwlink/?LinkID=208545&amp;clcid=0x409)

WebMatrix の一部として SQL Server Compact をインストールする場合の問題の詳細については、このドキュメントの「 [webmatrix のインストールに関する問題](#Known_Issues_Installation)」を参照してください。

### <a id="Known_Issues_Installing_Applications"></a>アプリケーションのインストール

#### <a name="issue-installing-an-application-can-take-a-long-time-if-the-users-my-documents-folder-is-redirected-to-a-network-share"></a>問題: ユーザーの [マイドキュメント] フォルダーがネットワーク共有にリダイレクトされると、アプリケーションのインストールに時間がかかることがある

> **回避策**  
> [なし] : アプリケーションのインストールには時間がかかる場合がありますが、正しくインストールされます。

### <a id="Known_Issues_Publishing_Applications"></a>アプリケーションの発行

#### <a name="issue-required-permissions-cannot-be-acquired-error-when-publishing-a-sql-compact-database"></a>問題: SQL Compact データベースを公開すると、"必要なアクセス許可を取得できません" というエラーが発生する

> WebMatrix では、中程度の信頼の構成で .NET Framework バージョン3.5 を実行しているサーバーに、SQL Server Compact のサポートバイナリを展開することは完全にサポートされていません。
> 
> **回避策**  
> 推奨される回避策は、サーバーに .NET Framework 4 をインストールすることです。 または、次の手順を実行します。
> 
> 1. *Web\_MediumTrust*ファイルの `SecurityClasses` セクションに次の要素を追加します。
> 
>     [!code-html[Main](overview/samples/sample6.html)]
> 2. 次の必要なアクセス許可を使用して、 *Web\_MediumTrust*ファイルに新しいアクセス許可セットを作成します。
> 
>     [!code-html[Main](overview/samples/sample7.html)]
> 3. *Web\_MediumTrust*ファイルに次の要素を配置して、アクセス許可セットを SQL Server Compact に適用します。
> 
>     [!code-html[Main](overview/samples/sample8.html)]

#### <a name="issue-gallery-and-phpbb-web-applications-display-a-service-is-unavailable-error-after-publishing"></a>問題: ギャラリーおよび PhpBB web アプリケーションで、発行後に "サービスを利用できません" というエラーが表示される

> 状況によっては、アプリケーションの発行によって "サービスを利用できません" というエラーが発生することがあります。
> 
> **回避策**  
> WebMatrix で、 **[発行の設定]** ウィンドウでサーバー名の末尾に円記号 (\) を追加し、もう一度アプリケーションを発行します。

#### <a name="issue-moodle-website-layout-and-links-are-broken-after-publishing"></a>問題: 発行後に Moodle web サイトのレイアウトとリンクが壊れている

> Moodle アプリケーションを発行すると、アプリケーションが正常に動作しなくなります。
> 
> **回避策**  
> WebMatrix で、 **[発行の設定]** ウィンドウの **[サイト名]** フィールドの末尾にスラッシュ (/) を追加し、アプリケーションを再度発行します。

#### <a name="issue-publishing-nopcommerce-fails-with-a-database-error"></a>問題: nopCommerce のパブリッシングがデータベースエラーで失敗する

> NopCommerce の発行に失敗し、"nop\_ログテーブルに挿入できませんでした。" などのデータベースエラーが報告されます。
> 
> **回避策**  
> 
> 1. WebMatrix で、 **[実行]** をクリックして nopCommerce をローカルで起動します。
> 2. [管理] ページにログインします。
> 3. **[システム]** メニューをクリックします。
> 4. **[ログ]** オプションをクリックします。
> 5. **[ログの消去]** ボタンをクリックします。
> 6. NopCommerce をもう一度公開します。

#### <a name="issue-silverstripe-cms-displays-a-http-500-php-fcgi-error-when-you-download-a-published-site"></a>問題: 発行されたサイトをダウンロードすると、Silverstripe CMS に "HTTP 500 PHP FCGI エラー" が表示される

> **回避策**  
> [発行**済みサイトのダウンロード**] をクリックした後、**発行プレビュー**で `silverstripe-cache/manifest_main` をスキップします。 このファイルはキャッシュの目的で使用され、各コンピューターに固有です。

#### <a name="issue-subtext-displays-server-error-in--application-when-you-download-a-published-site"></a>問題: 発行されたサイトをダウンロードすると、Subtext に "/' アプリケーションでのサーバーエラーが表示される

> **回避策**  
> サイトの*web.config*ファイルを開き、データベース接続文字列のユーザー ID とパスワードを SQL Server 管理者の資格情報 ("sa" の資格情報) に置き換えます。
> 
> または、次の手順に従って、ログインしているユーザーアカウントに `db_owner` アクセス許可を付与します。
> 
> 1. Web Platform Installer を使用して SQL Server Management Studio をインストールします。
> 2. ローカル SQL Server Express インスタンス (既定では `.\SQLEXPRESS`) に接続します。
> 3. [**データベース**&gt; *[Localsubtextdatabase]* をクリックし &gt;**セキュリティ**&gt; **Users** &gt; *[localsubtextdatabase*] (既定値は `subtextuser`]、右クリックして、 **[プロパティ]** をクリックします。
> 4. [ロールメンバーシップ] セクションで [ **db\_所有者**] を選択します。

#### <a name="issue-site-might-not-work-after-publishing-if-the-destination-url-field-is-not-prefixed-with-http-or-https"></a>問題: [宛先 URL] フィールドに http://または https://のプレフィックスが付いていないと、発行後にサイトが機能しない場合がある

> **[発行の設定]** ダイアログボックスで、インストール先の URL が `http://` または `https://`で始まらない場合は、展開後にサイトが動作しない可能性があります。
> 
> **回避策**  
> サイトを発行する前に、 **[発行の設定]** ダイアログボックスの目的の URL が `http://` または `https://`で始まることを確認します。

#### <a name="issue-publishing-a-mysql-database-fails-with-the-error-failed-to-publish-the-database-this-can-happen-if-the-remote-database-cannot-run-the-script"></a>問題点: MySQL データベースの公開が失敗し、"データベースをパブリッシュできませんでした。 これは、リモートデータベースがスクリプトを実行できない場合に発生する可能性があります。

> このエラーは、さまざまな理由で発生する可能性があります。 このエラーが表示される理由の1つは、データベーススクリプトに単一引用符 (') が含まれていて、MySQL データベースの既定の文字セットが UTF-8 に設定されていない場合です。
> 
> **回避策**  
> リモート MySQL データベースの既定の文字セットを UTF-8 に設定します。

#### <a name="issue-some-links-are-not-visible-in-dotnetnuke-after-publishing-or-downloading-the-site"></a>問題: サイトを公開またはダウンロードした後に、DotNetNuke に一部のリンクが表示されない

> DotNetNuke サイトを発行またはダウンロードする場合は、キャッシュをクリアして、サイトに新しいリンクが表示されるようにすることが必要になる場合があります。
> 
> **回避策**
> 
> 1. "Host" としてログインします。
> 2. ホスト メニューにアクセスし、**ホストの設定** を選択します。
> 3. 下にスクロールし、 **[詳細設定]** の **[パフォーマンスの設定]** を展開します。
> 4. ページの **[キャッシュのクリア]** リンクをクリックします。
> 5. ページの下部にアクセスし、アプリケーションを再起動します。

#### <a name="issue-some-links-in-atomsite-are-broken-after-you-download-a-published-site"></a>問題: 発行されたサイトをダウンロードした後、AtomSite の一部のリンクが壊れている

> **回避策**  
> *App.config*ファイル、*ユーザー .config*ファイル、およびすべての *.xml*ファイルで、URL 文字列 (たとえば、`http://myhost.com/atomsite`) をローカルの文字列 (たとえば、`http://localhost:1239`) に置き換えます。

#### <a name="issue-mysql-based-applications-like-wordpress-fail-to-publish-and-report-a-database-error"></a>問題: WordPress などの MySQL ベースのアプリケーションがデータベースエラーを発行して報告できない

> 既定では、WebMatrix は、UTF-8 文字セットを使用して MySQL をインストールします。 独自のに MySQL をインストールし、文字セットが UTF-8 ではない場合 (たとえば、Latin1)、データベースの発行プロセスが失敗する可能性があります。
> 
> **回避策**
> 
> 1. MySQL の文字セットを UTF-8 に変更します。 (詳細については、MySQL の web サイトの「[サーバー文字セットと照合順序](http://dev.mysql.com/doc/refman/5.0/en/charset-server.html)」を参照してください)。
> 2. アプリケーションを再インストールします。
> 3. アプリケーションを再発行します。

#### <a name="issue-download-published-site-fails-for-applications-that-have-browser-based-setup"></a>問題: ブラウザーベースのセットアップを実行しているアプリケーションで、"発行済みサイトのダウンロード" に失敗する

> 一部のアプリケーション (たとえば、Kentico CMS) では、データベースの作成などのインストール後のセットアップを実行するために、それらのアプリケーションをブラウザーで起動する必要があります。 ブラウザーベースのセットアップを完了せずにこのようなアプリケーションを発行した場合、リモートサーバーから同じサイトをダウンロードしようとすると失敗します。
> 
> **回避策**  
> サイトを公開する前に、ブラウザーベースのセットアップを完了します。

#### <a name="issue-download-published-site-fails-with-a-database-error-for-dotnetnuke-and-kooboo-cms"></a>問題: "公開されたサイトのダウンロード" が DotNetNuke および Kooboo CMS のデータベースエラーで失敗する

> サーバーからアプリケーションをダウンロードしようとしたときに、 **[発行の設定]** ダイアログボックスのデータベース接続文字列に管理者の資格情報がある場合、発行ログに次のエラーが表示されることがあります。
> 
> [!code-console[Main](overview/samples/sample9.cmd)]
> 
> **回避策**  
> 実際には、データベースの管理者以外の資格情報を使用して、サイトを (または公開している) 再発行します。

<a id="More_Info"></a>

## <a name="for-more-information"></a>詳細情報

WebMatrix 1.0 の詳細については、次の web サイトを参照してください。

- [IIS.net](http://iis.net/)
- [ASP.NET](https://asp.net/webmatrix)
- [Microsoft.com/web](https://www.microsoft.com/web)

© 2011 Microsoft Corporation. All rights reserved. [使用条件](https://msdn.microsoft.cos/cc300389.aspx)。
