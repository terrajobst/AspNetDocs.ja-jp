---
uid: web-pages/readme/beta3
title: Web Matrix and ASP.NET Web ページ (Razor) Beta 3 リリース Readme |Microsoft Docs
author: rick-anderson
description: Web Matrix と ASP.NET Web ページ (Razor) Beta 3 リリース Readme
ms.author: riande
ms.date: 01/10/2011
ms.assetid: ffa3d5c9-91e5-4da3-b409-560b0c7fbbf0
msc.legacyurl: /web-pages/readme/beta3
msc.type: content
ms.openlocfilehash: dc1d9237c04a7fcdbf4db6ccc8c36d255f6de003
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78510340"
---
# <a name="web-matrix-and-aspnet-web-pages-razor-beta-3-release-readme"></a>Web Matrix と ASP.NET Web ページ (Razor) Beta 3 リリース Readme

> Web Matrix と ASP.NET Web ページ (Razor) Beta 3 リリース Readme

2010年11月9日

## <a name="contents"></a>内容

- [概要](#Overview)
- [インストール](#Installation_Notes)
- [ベータ3リリースの新機能、変更点、および既知の問題](#Known_Issues)

    - [WebMatrix のインストールに関する問題](#Known_Issues_Installation)
    - [ASP.NET Web ページ](#Known_Issues_ASPNET)
    - [SQL Server Compact](#Known_Issues_SQL_Server_Compact)
    - [アプリケーションのインストール](#Known_Issues_Installing_Applications)
    - [アプリケーションの発行](#Known_Issues_Publishing_Applications)
    - [その他の問題](#Known_Issues_Other_Issues)
- [参照項目](#More_Info)

<a id="Overview"></a>

## <a name="overview"></a>概要

> Microsoft WebMatrix Beta は無料の web 開発スタックで、数分でインストールできます。 データベースとプログラミングのフレームワークに Web サーバーを組み合わせることによって、1 つの統合的な環境を実現します。 WebMatrix ベータを使用すると、独自の ASP.NET または PHP web サイトのコーディング、テスト、発行の方法を効率化することができます。また、WebMatrix ベータを使用して、DotNetNuke、Umbraco、WordPress、Joomla などの一般的なオープンソースアプリを使用して新しい web サイトを開始することもできます。 WebMatrix ベータは、インターネット上で web サイトを実行するのと同じ強力な web サーバー、データベースエンジン、フレームワーク環境を使用します。これにより、開発から運用環境への移行がスムーズでシームレスになります。

<a id="Installation_Notes"></a>

## <a name="installation"></a>インストール

> WebMatrix Beta 3 をインストールするには、 [Microsoft Web Platform Installer 3.0](https://go.microsoft.com/fwlink/?LinkID=194638)を使用します。 Web Platform Installer をインストールしたら、それを使用して WebMatrix Beta 3 をインストールできます。
> 
> インストール中に問題が発生した場合は、「 [Microsoft Web Platform Installer に関する問題のトラブルシューティング](https://go.microsoft.com/fwlink/?LinkId=196212)」を参照してください。

<a id="Installation_Notes0"></a>

## <a name="instructions-for-publishing-applications"></a>アプリケーションを公開するための手順

> [アプリケーションを公開するための詳細な手順を確認する](https://go.microsoft.com/fwlink/?LinkID=196149)

<a id="Known_Issues"></a>

## <a name="new-features-changes-andknown-issues"></a>新機能、変更点、および既知の問題

<a id="Known_Issues_Installation"></a>

### <a name="webmatrix-beta-3-installation"></a>WebMatrix Beta 3 のインストール

#### <a name="issue-webmatrix-beta-3-is-only-available-on-platforms-that-support-microsoft-net-framework-4"></a>問題点: WebMatrix Beta 3 は Microsoft .NET Framework 4 をサポートするプラットフォームでのみ使用できます。

> WebMatrix ベータ版には .NET Framework version 4 が必要です。 場合によっては、WebMatrix Beta インストーラーを使用して、サポートされている構成セットに含まれていないプラットフォームにをインストールしようとすることがあります。 特に、SP1 更新プログラムがインストールされていない Windows Vista では WebMatrix ベータ版のインストールを開始できますが、.NET Framework 4 コンポーネントは失敗し、インストールがブロックされます。
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

#### <a name="issue-cannot-install-webmatrix-beta-3-if-microsoft-visual-studio-2008-is-installed-without-microsoft-visual-studio-2008-sp1"></a>問題: Microsoft Visual Studio 2008 SP1 を使用せずに Microsoft Visual Studio 2008 がインストールされている場合は、WebMatrix Beta 3 をインストールできない

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

ドキュメントのこのセクションでは、Razor 構文による ASP.NET Web ページのベータ3リリースにおける新機能、変更点、および既知の問題について説明します。

- [新機能](#NewFeatures)
- [[変更点]](#Changes)
- [問題](#Issues)

<a id="NewFeatures"></a>

#### <a name="new-features-in-beta-3-for-aspnet-web-pages-with-razor-syntax"></a>Razor 構文を使用した ASP.NET Web ページ用の Beta 3 の新機能

#### <a name="new-htmlraw-method-renders-unencoded-markup"></a>New: "Html. Raw" メソッドがエンコードマークアップをレンダリングします。

> 新しい `Html.Raw` メソッドを使用すると、エンコードされた出力を表示する代わりに、HTML マークアップをマークアップとして表示できます。 (既定では、ASP.NET Razor は文字列をレンダリングする前にエンコードします)。構文は次のとおりです。
> 
> `Html.Raw(value)`
> 
> `Html.Raw` を使用する方法を次の例に示します。
> 
> [!code-cshtml[Main](beta3/samples/sample1.cshtml)]

<a id="Changes"></a>

#### <a name="changes-in-beta-3-for-aspnet-web-pages-with-razor-syntax"></a>Razor 構文を使用した ASP.NET Web ページに関する Beta 3 の変更点

#### <a name="change-hrefattribute-method-removed"></a>変更: "HrefAttribute" メソッドが削除されました

> `WebPage` クラスの `HrefAttribute` メソッドが削除されました。 このヘルパーは、Url 内の安全でない文字をエンコードするために使用されました。 ASP.NET Razor は文字列を自動的にエンコードするため、これは不要になりました。 (新しい `Html.Raw` メソッドを使用して、エンコードされていない文字列を表示します)。

#### <a name="change-syntax-for-declarative-helper-helpers-changed"></a>変更: 宣言型の "@helper" ヘルパーの構文が変更されました

> Beta 3 リリースでは、ASP.NET は、`@helper` 構文を使用して作成されたヘルパーを解析する方法を変更します。 基本的に、`@helper` 構文は、コードを含めることができるマークアップブロックとしてではなく、コードブロックとして解析されるようになりました。 そのため、ヘルパー内のコードを `@{ }` ブロックで囲む必要はありません。 逆に、ヘルパー内のマークアップは、HTML 要素または ASP.NET Razor `<text></text>` タグに明示的に含める必要があります。
> 
> たとえば、次の `@helper` 構文は、ベータ3リリースで動作します。
> 
> [!code-cshtml[Main](beta3/samples/sample2.cshtml)]
> 
> Beta 3 リリースでは、このヘルパーを次の例のように変更する必要があります。
> 
> [!code-cshtml[Main](beta3/samples/sample3.cshtml)]
> 
> ヘルパーの初期コードの周囲に `@{ }` 文字が使用されなくなったことに注意してください。 これは、ヘルパーの内容が既定でコードブロックとして扱われるためです。 ヘルパーは、開始 `<a>` タグで始まるマークアップをレンダリングします。 ヘルパーが、終了タグ (`<meta>` タグなど) を含まないプレーンテキストまたはタグをレンダリングする必要がある場合は、表示されるコンテンツが `<text></text>` タグに含まれている必要があります。

#### <a name="change-webpagecontexthttpcontext-removed"></a>変更: "WebPageContext. HttpContext" が削除されました

> `WebPageContext.HttpContext` プロパティは削除されました。 代わりに `HttpContext.Current` を使用してください (`WebPageContext.HttpContext` プロパティは、単純にこれをラップしたものです)。

#### <a name="change-facebook-helper-moved-to-new-package"></a>変更: "Facebook" ヘルパーを新しいパッケージに移動しました

> `Facebook` helper は、`Facebook` のヘルパーや追加機能を含む、 *Facebook のヘルパー*ライブラリに移動されました。 このライブラリを個別のパッケージとしてインストールする必要があります。詳細については、「チュートリアル[はじめに ASP.NET Pages](https://go.microsoft.com/fwlink/?LinkId=202889)」を参照してください。

#### <a name="change-membership-role-and-security-types-moves-to-new-assembly"></a>変更: メンバーシップ、ロール、およびセキュリティの種類が新しいアセンブリに移動します

> 次の型が `WebMatrix.WebData` アセンブリに移動されました。
> 
> - `ExtendedMembershipProvider`
> - `SimpleMembershipProvider`
> - `SimpleRoleProvider`
> - `WebSecurity`

#### <a name="change-tagbuilder-class-moved-to-systemwebwebpagesdll-assembly"></a>変更: "TagBuilder" クラスを System.web. Web ページの .dll アセンブリに移動

> `TagBuilde` r クラスは、System.web. Web ページの .dll アセンブリに移動されました。 以前は、これは ASP.NET MVC の一部であったアセンブリに含まれていました。 この変更は、`TagBuilder` クラスを使用するために ASP.NET MVC をインストールする必要がないことを意味します。
> 
> ただし、クラスは依然として `System.Web.Mvc` 名前空間にあります。 `TagBuilder` クラス (たとえば、カスタム ASP.NET Razor ヘルパー) を使用するには、名前空間を参照する必要があります (たとえば、コードに `@using System.Web.Mvc` を追加します)。

#### <a name="change-request-validation-syntax-changed-validation-class-removed"></a>変更: 要求の検証構文が変更されました。"Validation" クラスが削除されました

> Beta 3 リリースでは、個別のフィールドまたはフィールドのセットの検証を無効にするために、`Validation.Exclude` メソッドを呼び出して、検証から除外するフィールドの名前または名前を渡すことができます。 検証をバイパスするために、Beta 3 リリースで新しい構文を使用できます。 Beta 3 で使用されている `Validation` 方法は削除されました。
> 
> > [!NOTE]
> > 要求の検証を無効にしない場合、ユーザーが HTML マークアップをアップロードしようとすると (たとえば、ページのリッチテキストエディターを使用して)、web サイトは危険な要求のようなエラーを報告*します。クライアントからのフォームの値が検出*され、ユーザーの入力は受け入れられません。 要求の検証を無効にした場合は、ユーザー入力を手動で確認して、 [Microsoft のクロスサイトスクリプティングライブラリ](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=f4cd231b-7e06-445b-bec7-343e5884e651)v4.0 などを使用する危険性のあるマークアップやスクリプトが含まれていないことを確認する必要があります。
> 
> 
> 自動要求の検証を無効にするには、`Request.Unvalidated` メソッドを呼び出して、要求の検証をバイパスするフィールドまたはその他の post オブジェクトの名前を渡します。 このメソッドを使用すると、`Form`、`QueryString`、`Cookies`、および `ServerVariables` コレクション内の項目の検証を省略できます。 次の例は、`Unvalidated` メソッドの使用方法を示しています。
> 
> [!code-csharp[Main](beta3/samples/sample4.cs)]

<a id="Issues"></a>

#### <a name="known-issues-for-aspnet-web-pages-with-razor-syntax"></a>Razor 構文での ASP.NET Web ページに関する既知の問題

#### <a name="issue-unexpected-behavior-when-using-a-custom-user-table-for-membership"></a>問題: メンバーシップ用のカスタム ユーザー テーブルを使用しているときに予期しない動作が生じる

> ASP.NET Razor web サイトのメンバーシッププロバイダーを初期化するには、`WebSecurity.InitializeDatabaseConnection` メソッドを呼び出します。 (WebMatrix では、スターターサイトテンプレートには、 *\_該当*ファイルにこのメソッドの呼び出しが含まれています)。このメソッドの `autoCreateTables` パラメーターが true に設定されている場合 (既定では、スタートサイトテンプレートで true に設定されています)、認識できないテーブル名がメソッドに渡された場合 (2 番目のパラメーター)、メソッドはエラーをスローしません。 エラーがスローされずに、自動的にテーブルが作成されます。
> 
> メンバーシップにカスタムユーザーテーブルを使用するが、間違ったテーブル名を `WebSecurity.InitializeDatabaseConnection` メソッドに渡す場合は、この問題が発生する可能性があります。 指定したテーブルが存在しなかったとしても、既定ではメソッドからエラーが生成されません。新しいテーブルが作成されるため、アプリケーションは一見、正常に機能しているように見えます。 しかし、最終的には、カスタム ユーザー テーブル (とそのテーブル内のフィールド) に依存しているアプリケーション コードで予期しないエラーが発生します。
> 
> **回避策**  
> `InitializeDatabaseConnection` メソッドで渡された名前がメンバーシップデータベースのユーザープロファイルテーブルと一致していることを確認するか、`autoCreateTables` パラメーターが false に設定されていることを確認してください。

#### <a name="issue-failed-to-generate-a-user-instance-of-sql-server-error"></a>問題: "SQL Server のユーザー インスタンスを生成できませんでした" というエラーが表示される

> WebMatrix Web アプリケーションに SQL Server Express が使用されており、Windows 7 または Windows Server 2008 R2 で IIS 7.5 が実行されている場合、ユーザーのローカル アプリケーション パスを SQL Server が実行時に取得できないことを示すエラーが表示される場合があります。
> 
> **回避策**アプリケーションが実行されている Windows アカウント (通常は NETWORK SERVICE) に、アプリケーションのルートフォルダーと、*アプリの\_データ*などのサブフォルダーに対する読み取り/書き込みアクセス許可があることを確認します。 詳細については、サポート技術情報の記事「 [SQL Server Express ユーザーインスタンスと ASP.net Web アプリケーションプロジェクトに関する問題](https://support.microsoft.com/kb/2002980)」を参照してください。

#### <a name="issue-in-visual-studio-namespaces-for-custom-assemblies-dlls-are-not-imported-automatically"></a>問題点: Visual Studio でカスタムアセンブリ (Dll) の名前空間が自動的にインポートされない

> Visual Studio のプロジェクトでカスタムアセンブリを使用する場合、これらのアセンブリで宣言されている名前空間は、デザイン時に自動的にインポートされません。 その結果、カスタム型への参照がデザイン時に認識されず、Visual Studio で認識されていないとマークされることがあります ("波線" を使用)。 この問題は、Visual Studio のデザイン時にのみ発生します。アプリケーション自体が正常に実行されます。
> 
> **回避策**  
> デザイン時に認識されないエンティティを参照する `using` ステートメント (`imports` Visual Basic) を含めます。

#### <a name="issue-visual-studio-intellisense-and-project-templates-available-only-in-aspnet-mvc-version-3"></a>問題: Visual Studio IntelliSense およびプロジェクト テンプレートは ASP.NET MVC Version 3 でしか利用できない

> ASP.NET Web Pages をインストールしても Visual Studio 用のツール (ASP.NET Web Pages アプリケーション用のプロジェクト テンプレート、IntelliSense など) はインストールされません。
> 
> **回避策**Visual Studio で ASP.NET Web ページアプリケーションの IntelliSense とプロジェクトテンプレートを使用するには、Web Platform Installer または[スタンドアロンインストーラー](https://go.microsoft.com/fwlink/?LinkID=191797)を使用して ASP.NET MVC 3 RC をインストールします。

#### <a name="issue-lthelpergt-class-cannot-be-found-error"></a>問題: "&lt;ヘルパー&gt; クラスが見つかりません" エラー

> Beta 3 にアップグレードすると、ヘルパークラス (`Facebook` クラスなど) が見つからないというエラーが表示されることがあります。 Beta 2 以降、Beta 3 では、明示的にインストールする必要があるパッケージにヘルパーが移動されました。 既存のサイトは、これらのパッケージを含むようにアップグレードされません。これには、 *\My Documents\IISExpress*または *\My Documents\My* websites フォルダー内のサイトが含まれます。 特に、 *[個人用サイト*(WebSite1)] で既定のサイトを使用すると、このエラーが表示されます。このサイトには、`Twitter` ヘルパーへの参照が含まれています。
> 
> **回避策**  
> サイト内のヘルパーへの呼び出しをコメントアウトし、[ *\_管理者*] ページを実行して、使用するヘルパーを含むパッケージまたはパッケージをインストールします。 パッケージをインストールしたら、ヘルパーを参照する行のコメントを解除できます。

#### <a name="issue-deploying-beta-3-aspnet-razor-assemblies-to-the-bin-folder-might-not-work-on-hosting-sites"></a>問題点: Beta 3 ASP.NET Razor アセンブリを Bin フォルダーに配置すると、ホスティングサイトで機能しない場合がある

> ASP.NET Web ページ web サイトをホストサイトに展開し、ASP.NET Razor Beta 3 アセンブリをサイトの*Bin*フォルダーに配置すると、次のようなエラーが発生する可能性があります。
> 
> `Could not load type 'Microsoft.Web.Infrastructure.DynamicModuleHelper.DynamicModuleUtility' from assembly 'Microsoft.Web.Infrastructure, Version=1.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35'.`
> 
> これは、ホスティングプロバイダーが ASP.NET Web ページ Beta 1 のアセンブリをサーバーのグローバルアプリケーションキャッシュ (GAC) にインストールしている場合に発生する可能性があります。 GAC 内のアセンブリは、 *Bin*フォルダーにローカルにインストールされているアセンブリよりも優先されます。
> 
> **回避策**ホスティングプロバイダーに問い合わせて、発生しているエラーの原因が、プロバイダーのアセンブリのバージョン間の競合によるものであることを確認してください。 その場合は、ホスティングプロバイダーがサーバーの GAC 内のアセンブリを更新するように要求します。

#### <a name="issue-reading-feeds-or-other-external-data-via-a-proxy-server"></a>問題: フィードなどの外部データをプロキシ サーバーから読み取る

> サイトを実行しているサーバーがプロキシサーバーの背後にある場合は、サイトの外部からの情報を読み取ることができるよう*に、web.config ファイルに*プロキシ情報を構成することが必要になる場合があります。 たとえば、`ReCaptcha` ヘルパーを使用する場合、ヘルパーは reCAPTCHA サービスと通信しますが、プロキシサーバーによってブロックされる可能性があります。 同様に、ASP.NET Web Pages で使用されているフィード (パッケージ マネージャーによって使用されているフィードなど) にもプロキシ構成が必要となることがあります。
> 
> 外部サービスの操作中またはパッケージフィードの操作で問題が発生した場合は、アプリケーションのルート*web.config*ファイルに次の要素を追加します。
> 
> [!code-xml[Main](beta3/samples/sample5.xml)]
> 
> プロキシサーバーの構成の詳細については、MSDN Web サイトの「 [&lt;proxy&gt; 要素 (ネットワーク設定)](https://msdn.microsoft.com/library/sa91de1e.aspx) 」を参照してください。

#### <a name="issue-microsoftwebinfrastructuredll-cannot-be-loaded-error"></a>問題: "Microsoft Web インフラストラクチャを読み込めません" エラーが発生する

> ベータ1バージョンの ASP.NET Web ページを Razor 構文と共にインストールした後、Beta 3 バージョンをインストールした場合は、すべての適切なアセンブリが、 *Microsoft Web インフラストラクチャ .dll*を除く GAC にインストールされます。 その結果、ASP.NET Razor ページを実行すると、 *Microsoft Web インフラストラクチャ*を読み込めなかったことを示すエラーが表示されます。
> 
> この問題は、クリーンコンピューターでベータ3リリースを読み込んだ場合は発生しません。
> 
> **回避策**  
> コントロールパネルで ASP.NET Web ページをアンインストールします。 次に、Beta 3 リリースを再インストールします。

#### <a name="issue-uninstalling-the-net-framework-version-4-disables-aspnet-web-pages-with-razor-syntax"></a>問題: .NET Framework  Version 4 をアンインストールすると Razor 構文を使用する ASP.NET Web Pages が無効になる

> .NET Framework  Version 4 をアンインストールして再インストールした場合、Razor 構文を使用する ASP.NET Web Pages は無効になります。 拡張子が*cshtml*のページは正しく動作しません。 ASP.NET Web ページは、アセンブリをコンピューターのルート*web.config*ファイルに登録し、.NET Framework を削除するとそのファイルが削除されます。 .NET Framework を再インストールすると、新しいバージョンの構成ファイルがインストールされますが、ASP.NET Web Pages アセンブリに対する参照は追加されません。
> 
> **回避策**.NET Framework を再インストールした後、Razor 構文で ASP.NET Web ページを再インストールします。 これにより、コンピュータールートの*web.config ファイルに*次の要素が追加されます。通常は次の場所にあります。  
> 
> `C:\Windows\Microsoft.NET\Framework\v4.0.30319\Config (32-bit)`  
> 
> `C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config (64-bit)`
> 
> [!code-xml[Main](beta3/samples/sample6.xml)]

#### <a name="issue-applications-previously-deployed-with-aspnet-assemblies-in-the-bin-folder-experience-errors"></a>問題: 以前に Bin フォルダー内の ASP.NET アセンブリを使用して展開されたアプリケーションでエラーが発生する

> 配置時に、ASP.NET Web ページアセンブリ (たとえば、 *Microsoft Web ページ*) のコピーをサーバー上の web サイトの*Bin*フォルダーにコピーします。 (これは、配置中、または開発者によってアセンブリが明示的にコピーされたために自動的に発生した可能性があります)。ただし、Beta 3 リリースがインストールされている場合、特定の種類が見つからないエラーなど、エラーが発生します。 これは、ベータ3リリース用に複数の ASP.NET Web ページ型が異なる名前空間に移動されたために発生します。
> 
> **回避策**   
> 配置されたアプリケーションの*Bin*フォルダーをクリアし、新しいアセンブリをフォルダーにコピー (またはアプリケーションを再デプロイ) してから、アプリケーションを再起動します。

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
> 
> [!code-xml[Main](beta3/samples/sample7.xml)]

#### <a name="issue-using-web-application-project-or-aspnet-mvc-and-aspnet-web-pages-in-the-same-application"></a>問題点: 同じアプリケーションで Web アプリケーションプロジェクトまたは ASP.NET MVC と ASP.NET Web ページを使用する

> Web アプリケーションプロジェクトまたは ASP.NET MVC アプリケーションで ASP.NET Web ページを使用していた場合、 *WebPageHttpApplication*が見つからないというエラーが表示されることがあります。
> 
> **回避策**  
> このエラーが発生した場合は、アプリケーションを派生させる基底クラスを変更します。 *Global.asax*ファイルで、次の行を変更します。
> 
> [!code-csharp[Main](beta3/samples/sample8.cs)]
> 
> この行を次のように変更します。
> 
> [!code-csharp[Main](beta3/samples/sample9.cs)]
> 
> これにより、ASP.NET Web ページのベータ1リリースで導入された変更が Razor 構文によって元に戻されます。

#### <a name="issue-deploying-an-application-to-a-computer-that-does-not-have-sql-server-compact-installed"></a>問題: SQL Server Compact がインストールされていないコンピューターにアプリケーションを展開する

> SQL Server Compact データベースを含むアプリケーションは、SQL Server Compact がインストールされていないコンピューターで実行できます。 Microsoft WebMatrix Beta 3 では、これらのバイナリが自動的にコピーされ *、適切な web.config ファイル*変換が実行されます。
> 
> **回避策**これらのファイルをコピーし*て、web.config ファイルを*手動で変更する必要がある場合は、次の手順を実行します。
> 
> 1. データベースエンジンアセンブリを、ターゲットコンピューター上のアプリケーションの*Bin*フォルダー (およびサブフォルダー) にコピーします。 
> 
>     - *SQL Server Compact C:\Program Edition\v4.0\Desktop\System.Data.SqlServerCe.dll* **を** *\bin*にコピーします。
>     - *SQL Server Compact C:\Program Edition\v4.0\Private\x86\\* * を \Bin\x86**にコピーし**ます。
>     - *SQL Server Compact C:\Program Edition\v4.0\Private\amd64\\* * を \Bin\amd64**にコピーし**ます。
> 2. *Web*サイトのルートフォルダーで、web.config ファイルを作成するか、開きます。 (WebMatrix Beta 3 では、 **[ファイルの種類の選択]** ダイアログボックスで **[すべて]** をクリックすると、このファイルの種類が使用可能になります)。
> 3. 次の要素を **&lt;configuration&gt;** 要素の子として追加します ( **&lt;system.web&gt;** 要素の内側には追加しません)。
> 
> 
> [!code-xml[Main](beta3/samples/sample10.xml)]

#### <a name="issue-database-and-webgrid-helpers-do-not-work-in-medium-trust-in-visual-basic"></a>問題点: データベースと WebGrid のヘルパーは、Visual Basic の中程度の信頼では機能しません

> Visual Basic ( *vbhtml*ファイルの作成) を使用している場合、アプリケーションが中程度の信頼を使用するように設定されていると、`Database` と `WebGrid` のヘルパーは機能しません。
> 
> **回避策**  
> 完全信頼を使用するようにアプリケーションを一時的に設定します。

<a id="Known_Issues_SQL_Server_Compact"></a>
### <a name="sql-server-compact"></a>SQL Server Compact

#### <a name="issue-encrypt-property-is-not-recognized"></a>問題: "Encrypt" プロパティが認識されない

> SQL Server Compact 4.0 は `SqlCeConnection` クラスの `Encrypt` プロパティを認識しません。 このプロパティを使用してデータベースファイルを暗号化しないでください。 `Encrypt` プロパティは SQL Server Compact 3.5 リリースでは非推奨とされており、旧バージョンとの互換性のためだけに保持されていました。 
> 
> **回避策**  
> `SqlCeConnection` クラスの `Encryption Mode` プロパティを使用して、SQL Server Compact 4.0 データベースファイルを暗号化します。 次の例では、`Encryption Mode` プロパティを使用して、暗号化された SQL Server Compact 4.0 データベースを作成する方法を示します。
> 
> [!code-csharp[Main](beta3/samples/sample11.cs)]
> 
> [!code-vb[Main](beta3/samples/sample12.vb)]
> 
> 既存の SQL Server Compact 4.0 データベースの暗号化モードを変更するには、次の手順を実行します。
> 
> [!code-csharp[Main](beta3/samples/sample13.cs)]
> 
> [!code-vb[Main](beta3/samples/sample14.vb)]
> 
> 暗号化されていない SQL Server Compact 4.0 データベースを暗号化するには、次の手順を実行します。
> 
> [!code-csharp[Main](beta3/samples/sample15.cs)]
> 
> [!code-vb[Main](beta3/samples/sample16.vb)]

#### <a name="issue-microsoft-visual-c-2008-runtime-libraries-are-required"></a>問題: Microsoft Visual C++ 2008 ランタイムライブラリが必要です

> SQL Server Compact 4.0 のネイティブ Dll には、Microsoft Visual C++ 2008 ランタイムライブラリ (X86、IA64、X64) Service Pack 1 が必要です。
> 
> **回避策**  
> .NET Framework 3.5 SP1 をインストールします。 これにより、Visual C++ 2008 ランタイムライブラリ SP1 もインストールされます。 ライブラリは次の場所からダウンロードできます。   
>   
> [Microsoft Visual C++ 2008 Service Pack 1 再頒布可能パッケージ ATL のセキュリティ更新プログラム](https://go.microsoft.com/fwlink/?LinkId=194827)
> 
> [!NOTE]
> .NET Framework 2.0、3.0、または4をインストールしても、Visual C++ 2008 RUNTIME library SP1 はインストール*されない*ことに注意してください。

#### <a name="issue-if-sql-server-compact-is-installed-prior-to-installing-net-framework-on-the-computer-its-provider-invariant-name-is-not-registered-in-the-net-framework-machineconfig-file"></a>問題: コンピューターに .NET Framework をインストールする前に SQL Server Compact がインストールされている場合、そのプロバイダーの不変名は .NET Framework の machine.config ファイルに登録されていません。

> SQL Server Compact には .NET Framework が必要なため、.NET Framework がインストールされていないコンピューターに SQL Server Compact をインストールできます。 SQL Server Compact をインストールする前に .NET Framework バージョン3.5 と4の両方がインストールされていない場合、SQL Server Compact セットアップでは、プロバイダーの不変名が*machine.config ファイルに*登録されません。 *Machine.config*ファイルの SQL Server Compact エントリに依存するアプリケーションはすべて失敗します。 *Machine.config*の不変名の登録エントリは、次の例のようになります。
> 
> [!code-xml[Main](beta3/samples/sample17.xml)]
> 
> **回避策**  
> SQL Server Compact 4.0 CTP1 をアンインストールします。 次の場所から .NET Framework の完全なバージョンをダウンロードしてインストールします。
> 
> [Microsoft .NET Framework 3.5 Service pack 1 (フルパッケージ)](https://go.microsoft.com/fwlink/?LinkId=194828)  
> [Microsoft .NET Framework 4.0 リリース (完全なパッケージ)](https://www.microsoft.com/downloads/details.aspx?FamilyID=9cfb2d51-5ff4-4491-b0e5-b386f32c0992&amp;displaylang=en)
> 
> [SQL Server Compact 4.0 CTP1](https://www.microsoft.com/downloads/details.aspx?FamilyID=0d2357ea-324f-46fd-88fc-7364c80e4fdb&amp;displaylang=en)を再インストールします。

<a id="Known_Issues_Installing_Applications"></a>

### <a name="installing-applications"></a>アプリケーションのインストール

#### <a name="issue-installing-an-application-can-take-a-long-time-if-the-users-my-documents-folder-is-redirected-to-a-network-share"></a>問題: ユーザーの [マイドキュメント] フォルダーがネットワーク共有にリダイレクトされると、アプリケーションのインストールに時間がかかることがある

> **回避策**  
> [なし] : アプリケーションのインストールには時間がかかる場合がありますが、正しくインストールされます。

<a id="Known_Issues_Publishing_Applications"></a>

### <a name="publishing-applications"></a>アプリケーションの発行

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

<a id="Known_Issues_Other_Issues"></a>

### <a name="other-issues"></a>その他の問題

#### <a name="issue-searchfilter-does-not-work-in-reports-for-group-by-issue-type"></a>問題: [グループ化] のレポートで検索/フィルターが機能しない: 問題の種類

> サイトのレポートを実行するときに、[ *URL でフィルター* ] ボックスにテキストを入力して [*検索*] をクリックした場合、何も起こりません。 これは、レポートの [*グループ化*の状態] が [*問題の種類*] (既定) に設定されている場合に、このコントロールが機能しないためです。
> 
> **回避策**リボンの [*グループ化*] タブで、[ *url* ] をクリックして、ソース url でエントリをグループ化します。 この状態では、エントリをフィルター処理するためのテキストボックスとボタンが機能します。

#### <a name="issue-wcf-applications-fail-to-run-with-iis-express"></a>問題: WCF アプリケーションを IIS Express で実行できない

> WCF アプリケーションを参照すると、次のようなエラーが発生します。
> 
> *ファイルまたはアセンブリ ' 7.0.0.0, Version =, Culture = ニュートラル, PublicKeyToken = 31bf3856ad364e35 ' またはその依存関係の1つが読み込めませんでした。指定されたファイルが見つかりません。*
> 
> これは IIS Express ベータリリースでは、既定では WCF がサポートされていないために発生します。
> 
> **回避策**次のいずれかの回避策を使用してください (回避 #2 には、Microsoft Windows Vista 以降が必要です)。
> 
> 
> 1. WebMatrix のインストール場所から、WCF アプリケーションの*bin*ディレクトリに、 *microsoft Web .dll*および*microsoft. web.config*アセンブリをコピーします。 既定では、WebMatrix は、システムの*Program Files*フォルダーの下にある*Microsoft webmatrix*サブフォルダーにインストールされます。
> 2. Microsoft Windows Vista 以降では、次のコマンドを使用して、 *bin*ディレクトリ内のアセンブリへのシンボリックリンクを作成します。 (このアプローチには、アセンブリのコピーを作成しないという利点があります)。
> 
>     [!code-console[Main](beta3/samples/sample18.cmd)]
> 3. 2つのアセンブリを GAC にインストールします。 管理者特権のプロンプトで、次のコマンドを実行します。
> 
>     [!code-console[Main](beta3/samples/sample19.cmd)]

#### <a name="issue-webmatrix-beta-3-is-unable-to-perform-certain-tasks-that-require-elevation"></a>問題: WebMatrix Beta 3 は、昇格が必要な特定のタスクを実行できない

> WebMatrix Beta 3 では、次の状況での追加コンポーネントのインストールなど、昇格が必要な特定のタスクを実行できません。
> 
> - Windows Vista または Windows 7 では、管理者特権を持たないアカウントを使用してログインし、ユーザーアカウント制御 (UAC) が無効になっています。
> - Microsoft Windows XP または Microsoft Windows Server 2003 を使用している。
> 
> **回避策**  
> WebMatrix Beta 3 のほとんどのタスクには、管理者権限は必要ありません。 そのためには、管理者として操作を実行するか、次の手順に従います。
> 
> - Windows Vista または Windows 7 では、UAC を有効にします。
> - Windows XP では、ユーザーを管理者セキュリティグループに追加します。

#### <a name="issue-site-from-web-gallery-is-disabled"></a>問題: "Web ギャラリーからのサイト" が無効になっています

> Web Platform Installer 3.0 がインストールされていない場合、 **[Web ギャラリーからのサイト]** オプションは無効になっています。
> 
> **回避策**  
> [Microsoft Web Platform Installer 3.0](https://go.microsoft.com/fwlink/?LinkID=194638)をインストールします。

#### <a name="issue-on-windows-server-2003-iis-express-does-not-start-for-a-non-administrative-user"></a>問題: Windows Server 2003 で、管理者以外のユーザーに対して IIS Express が開始しない

> Windows Server 2003 では、ページを起動したり IIS Express を開始したりしても、IIS Express は開始されません。 Web ページの場合、管理者以外のユーザーによってアプリケーションが起動されたことを示すエラーが表示されます。
> 
> **回避策**  
> WebMatrix Beta 3 を管理ユーザーとして起動します。 詳細については、次のサポート技術情報を参照してください。  
>   
> [管理者以外のユーザーによって起動されたアプリケーションは、Windows Vista、Windows Server 2003、または Windows XP でアプリケーションが実行されているコンピューターの HTTP トラフィックをリッスンできません。](https://support.microsoft.com/kb/939786)

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

#### <a name="issue-the-relationships-button-is-disabled"></a>問題: [リレーションシップ] ボタンが無効になっている

> SQL Server Compact データベースでは、 **[データベース]** ワークスペースの **[テーブル]** タブの下にある **[リレーションシップ]** ボタンは無効になっています。
> 
> **回避策**  
> [なし] : SQL Server Compact はテーブル間のリレーションシップをサポートしていません。

#### <a name="issue-parameterized-sql-queries-throw-exceptions"></a>問題点: パラメーター化された SQL クエリで例外がスローされる

> SQL Server Compact 4.0 では、パラメーター化クエリのパラメーターに `SqlDbType` や `DbType` などのデータ型を指定しなかった場合、クエリの実行時に例外がスローされます。
> 
> **回避策**  
> `SqlDbType` や `DbType`などのパラメーターのデータ型を明示的に設定します。 これは、BLOB データ型 (`image` および `ntext`) の場合に重要です。 次のようなコードを使用します。
> 
> [!code-sql[Main](beta3/samples/sample20.sql)]
> 
> [!code-vb[Main](beta3/samples/sample21.vb)]

<a id="More_Info"></a>

## <a name="for-more-information"></a>詳細情報

WebMatrix Beta 3 の詳細については、次の web サイトを参照してください。

- [IIS.net](http://iis.net/)
- [ASP.NET](https://asp.net/webmatrix)
- [Microsoft.com/web](https://www.microsoft.com/web)

---

© 2010 Microsoft Corporation. All rights reserved. [使用条件](https://msdn.microsoft.cos/cc300389.aspx)。
