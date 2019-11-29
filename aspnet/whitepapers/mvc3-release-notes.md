---
uid: whitepapers/mvc3-release-notes
title: ASP.NET MVC 3 |Microsoft Docs
author: rick-anderson
description: ''
ms.author: riande
ms.date: 10/06/2010
ms.assetid: f44c166e-7e91-48a0-a6f8-d9285f3594e5
msc.legacyurl: /whitepapers/mvc3-release-notes
msc.type: content
ms.openlocfilehash: 504202068f5db4f8614bba02e8066ffecfd15b48
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74619240"
---
# <a name="aspnet-mvc-3"></a>ASP.NET MVC 3

- [概要](#overview)
- [インストールに関する注意事項](#installation-notes)
- [ソフトウェア要件](#software-requirements)
- [ドキュメント](#documentation)
- [サポート](#support)
- [ASP.NET MVC 2 プロジェクトを ASP.NET MVC 3 Tools Update にアップグレードする](#upgrading)
- [ASP.NET MVC 3 Tools 更新プログラム (2011 年4月12日)](#tu-changes)

    - [[コントローラーの追加] ダイアログボックスで、コントローラーをビューおよびデータアクセスコードにスキャフォールディングできるようになりました](#tu-AddControllerDialog)
    - [[ASP.NET MVC 3 New Project (新しいプロジェクトの追加)] ダイアログボックスの機能強化](#tu-ImprovementsNewDialogBox)
    - [プロジェクトテンプレートに Modernizr 1.7 が含まれるようになりました](#tu-Modernizr)
    - [プロジェクトテンプレートには、jQuery、jQuery UI、および jQuery Validation の更新バージョンが含まれています](#tu-UpdatedJQuery)
    - [プロジェクトテンプレートに、事前にインストールされた NuGet パッケージとして ADO.NET Entity Framework 4.1 が含まれるようになりました](#tu-EF)
    - [プロジェクトテンプレートには、プレインストールされた NuGet パッケージとしての JavaScript ライブラリが含まれています](#tu-JavaScriptLibsNuget)
    - [既知の問題](#tu-KI)
- [ASP.NET MVC 3 RTM (2011 年1月13日)](#MVC3RTM)

    - [変更: jQuery UI のバージョンを1.8.7 に更新しました](#RTM-1)
    - [変更: 既定の ModelMetadataProvider を Data注釈の内容に変更しました。](#RTM-2)
    - [修正: 空白を含む Razor 式の一部を貼り付けると、元に戻されます。](#RTM-3)
    - [修正: エディターで開いた Razor ファイルの名前を変更すると、構文の色付けと IntelliSense が無効になります。](#RTM-4)
    - [既知の問題](#RTM-KI)
    - [重大な変更](#RTM-BC)
- [ASP.NET MVC 3 リリース候補 2 (2010 年12月10日)](#_Toc2)

    - [JQuery 1.4.4、jQuery Validation 1.7、jQuery UI 1.8.6 y UI 1.8.6 を含むようにプロジェクトテンプレートが変更されました。](#_Toc2_1)
    - ["AdditionalMetadataAttribute" クラスを追加しました](#_Toc2_2)
    - [ビューのスキャフォールディングの向上](#_Toc2_3)
    - [追加された Html. Raw メソッド](#_Toc2_3)
    - ["Controller. ビュー名" プロパティと "View" プロパティの名前を "ViewBag" に変更しました](#_Toc2_4)
    - ["ControllerSessionStateAttribute" クラスの名前を "SessionStateAttribute" に変更しました](#_Toc2_5)
    - [RemoteAttribute "Fields" プロパティの名前を "AdditionalFields" に変更しました](#_Toc2_6)
    - ["SkipRequestValidationAttribute" を "AllowHtmlAttribute" に変更しました](#_Toc2_7)
    - [最初の役に立つエラーメッセージを表示するように "Html. ValidationMessage" メソッドを変更しました](#_Toc2_8)
    - [ドキュメントに空白を追加しないように @model 宣言を修正した](#_Toc2_9)
    - [エンジン固有のファイル名をサポートするための "FileExtensions" プロパティをビューエンジンに追加しました](#_Toc2_10)
    - ["For" 属性の正しい値を出力するように "LabelFor" ヘルパーを修正しています](#_Toc2_11)
    - [モデルバインド中に明示的な値の優先順位を指定するように "RenderAction" メソッドを修正した](#_Toc2_12)
    - [重大な変更](#_Toc2_BC)
    - [既知の問題](#_Toc2_KI)
- [ASP.NET MVC 3 リリース候補 (2010 年11月9日)](#TOC_ASP_NET_3_RC)

    - [ASP.NET MVC 3 RC の新機能](#_Toc276711785)
    - [NuGet パッケージマネージャー](#_Toc276711786)
    - [[新しいプロジェクト] ダイアログボックスの機能強化](#_Toc276711787)
    - [セッションレスコントローラー](#_Toc276711788)
    - [新しい検証属性](#_Toc276711789)
    - ["LabelFor" メソッドと "LabelForModel" メソッドの新しいオーバーロード](#_Toc276711790)
    - [子アクションの出力キャッシュ](#_Toc276711791)
    - [[ビューの追加] ダイアログボックスの機能強化](#_Toc276711792)
    - [詳細な要求の検証](#_Toc276711793)
    - [重大な変更](#_Toc276711794)
    - [既知の問題](#_Toc276711795)
- [ASP.MVC 3 ベータノート (2010 年10月6、)](#TOC_ASP_NET_3_Beta)

    - [ASP.NET MVC 3 Beta の新機能](#0.1__Toc274034215)
    - [NuPack パッケージマネージャー](#0.1__Toc274034216)
    - [強化された [新しいプロジェクト] ダイアログボックス](#0.1__Toc274034217)
    - [Razor ビューで厳密に型指定されたモデルを指定するための簡略化された方法](#0.1__Toc274034218)
    - [新しい ASP.NET Web ページヘルパーメソッドのサポート](#0.1__Toc274034219)
    - [追加の依存関係の挿入のサポート](#0.1__Toc274034220)
    - [控えめな jQuery ベースの Ajax の新しいサポート](#0.1__Toc274034221)
    - [控えめな jQuery 検証の新しいサポート](#0.1__Toc274034222)
    - [クライアント検証と控えめな JavaScript のための新しいアプリケーション全体のフラグ](#0.1__Toc274034223)
    - [ビューの実行前に実行されるコードの新しいサポート](#0.1__Toc274034224)
    - [VBHTML Razor 構文の新しいサポート](#0.1__Toc274034225)
    - [ValidateInputAttribute をより細かく制御する](#0.1__Toc274034226)
    - [ヘルパーは、匿名オブジェクトを使用して指定された HTML 属性名のアンダースコアをハイフンに変換します](#0.1__Toc274034227)
    - [バグの修正](#0.1__Toc274034228)
    - [重大な変更](#0.1__Toc274034229)
    - [既知の問題](#0.1__Toc274034230)
- [免責事項](#0.1__Toc274034231)

<a id="overview"></a>
## <a name="overview"></a>の概要

このドキュメントでは、Visual Studio 2010 用 ASP.NET MVC 3 RTM のリリースについて説明します。 ASP.NET MVC は、モデルビューコントローラー (MVC) パターンを使用する Web アプリケーションを開発するためのフレームワークです。 ASP.NET MVC 3 インストーラーには、次のコンポーネントが含まれています。

- ASP.NET MVC 3 ランタイムコンポーネント
- ASP.NET MVC 3 Visual Studio 2010 ツール
- 実行時コンポーネントの ASP.NET Web ページ
- ASP.NET Web ページ Visual Studio 2010 ツール
- .NET 用 Microsoft パッケージマネージャー (NuGet)
- Razor 構文のサポートを有効にする Visual Studio 2010 の更新プログラム。 (詳細については、サポート技術情報の記事2483190を参照してください。)

ASP.NET MVC 3 のプレリリース版のすべてのリリース ノートは、次の URL の ASP.NET Web サイトで公開されています。

https://www.asp.net/learn/whitepapers/mvc3-release-notes

<a id="installation-notes"></a>
## <a name="installation-notes"></a>インストールに関する注意事項

Web Platform Installer (Web PI) を使用して ASP.NET MVC 3 RTM をインストールするには、次のページを参照してください。

[https://www.microsoft.com/web/gallery/install.aspx?appid=MVC3](https://www.microsoft.com/web/gallery/install.aspx?appid=MVC3)

または、次のページから ASP.NET MVC 3 RTM for Visual Studio 2010 のインストーラーをダウンロードすることもできます。

https://go.microsoft.com/fwlink/?LinkID=208140

ASP.NET MVC 3 はインストールでき、ASP.NET MVC 2 とサイドバイサイドで実行できます。

<a id="software-requirements"></a>
## <a name="software-requirements"></a>ソフトウェア要件

ASP.NET MVC 3 ランタイムコンポーネントには、次のソフトウェアが必要です。

- .NET Framework バージョン4。 

    ASP.NET MVC 3 Visual Studio 2010 ツールには、次のソフトウェアが必要です。
- Visual Studio 2010 または Visual Web Developer 2010 Express。

<a id="documentation"></a>
## <a name="documentation"></a>Documentation

ASP.NET MVC のドキュメントは、MSDN Web サイトの次の URL から入手できます。

[https://go.microsoft.com/fwlink/?LinkId=205717](https://go.microsoft.com/fwlink/?LinkId=205717)

ASP.NET MVC に関するチュートリアルやその他の情報については、ASP.NET Web サイトの MVC ページの次の URL を参照してください。

[https://www.asp.net/mvc/](../mvc/index.md)

<a id="support"></a>
## <a name="support"></a>でのサポート

このリリースは完全にサポートされています。 テクニカルサポートを受ける方法については、 [Microsoft サポート web サイト](https://support.microsoft.com/)を参照してください。

また、このリリースについての質問はお気軽に ASP.NET MVC フォーラムにお寄せください。このフォーラムでは、ASP.NET コミュニティのメンバーによる非公式のサポートを受けられる場合が多くあります。

[https://forums.asp.net/1146.aspx](https://forums.asp.net/1146.aspx)

<a id="upgrading"></a>
## <a name="upgrading-an-aspnet-mvc-2-project-to-aspnet-mvc-3-tools-update"></a>ASP.NET MVC 2 プロジェクトを ASP.NET MVC 3 Tools Update にアップグレードする

ASP.NET MVC 3 は、ASP.NET MVC 2 とサイドバイサイドで同じコンピューターにインストールできます。これにより、ASP.NET MVC 2 アプリケーションを ASP.NET MVC 3 にアップグレードするタイミングを柔軟に選択できます。

既存の ASP.NET MVC 2 アプリケーションをバージョン3に手動でアップグレードするには、次の手順を実行します。

1. コンピューターに新しい空の ASP.NET MVC 3 プロジェクトを作成します。 このプロジェクトには、アップグレードに必要ないくつかのファイルが含まれています。
2. ASP.NET MVC 3 プロジェクトから次のファイルを ASP.NET MVC 2 プロジェクトの対応する場所にコピーします。 jQuery ライブラリへの参照を更新して、新しいファイル名を参照する必要があります (jQuery-1.5.1.js)。 

    - /Views/Web.config
    - /packages.config
    - /スクリプト/\*.js
    - /\*します。\*
3. 空の ASP.NET MVC 3 プロジェクトソリューションのルートにある*packages*フォルダーをソリューションのルートにコピーします。このフォルダーは、ソリューションの .sln ファイルが配置されているディレクトリにあります。
4. ASP.NET MVC 2 プロジェクトに領域が含まれている場合は、/ビューファイルを各領域の*Views*フォルダーにコピーします。
5. ASP.NET MVC 2 プロジェクトの Web.config ファイルの両方で、ASP.NET MVC バージョンをグローバルに検索して置き換えます。 次の文字列を検索します。 

    [!code-console[Main](mvc3-release-notes/samples/sample1.cmd)]

    上記を次の文字列に置き換えます。

    [!code-console[Main](mvc3-release-notes/samples/sample2.cmd)]
6. ソリューションエクスプローラーで、(バージョン2の DLL を指す) system.web *. mvc*への参照を削除し、3.0.0.0 への*参照 (v) を追加*します。
7. System.web. web ページ .dll と system.servicemodel への参照を追加します。 これらのアセンブリは、次のフォルダーに保存されています。 

    - %ProgramFiles%\ Microsoft ASP.NET\ASP.NET MVC 3\Assemblies
    - %ProgramFiles%\ Microsoft ASP.NET\ASP.NET Web Pages\v1.0\Assemblies
8. ソリューション エクスプローラーで、プロジェクト名を右クリックし、[プロジェクトのアンロード] を選択します。 次に、プロジェクト名をもう一度右クリックし、[ *ProjectName*. .Csproj の編集] を選択します。
9. *Projecttypeguids*要素を見つけ、{F85E285D-A4E0-4152-9332-AB1D724D3325} を {E53F8FEA-EAE0-44A6-8774-FFD645390401} に置き換えます。
10. 変更を保存してプロジェクトを右クリックし、[プロジェクトの再読み込み] をクリックします。
11. アプリケーションのルートの Web.config ファイルで、次の設定を*assemblies*セクションに追加します。 

    [!code-xml[Main](mvc3-release-notes/samples/sample3.xml)]
12. ASP.NET MVC 2 を使用してコンパイルされたサードパーティ製のライブラリをプロジェクトが参照する場合は、次の強調表示されている*bindingRedirect*要素を、アプリケーションルートの web.config ファイルに*構成*セクションの下に追加します。 

    [!code-xml[Main](mvc3-release-notes/samples/sample4.xml)]

<a id="tu-changes"></a>
## <a name="changes-in-aspnet-mvc-3-tools-update"></a>ASP.NET MVC 3 Tools Update の変更点

このセクションでは、ASP.NET MVC 3 RTM リリース以降、ASP.NET MVC 3 Tools Update リリースで加えられた変更について説明します。

<a id="tu-AddControllerDialog"></a>
### <a name="add-controller-dialog-box-can-now-scaffold-controllers-with-views-and-data-access-code"></a>[コントローラーの追加] ダイアログ ボックスで、ビューとデータ アクセス コードを使用したコントローラーのスキャフォールディングが可能に

スキャフォールディングを使用すると、アプリケーションのコントローラーとビューをすばやく生成できます。 生成されたコードは、プロジェクトの要件に合わせて編集できます。

ASP.NET MVC 3 の [*コントローラーの追加*] ダイアログボックスを起動するには、*ソリューションエクスプローラー*で [*コントローラー* ] フォルダーを右クリックし、[*追加*] をクリックして、[*コントローラー*] をクリックします。 このダイアログ ボックスには、新たにスキャフォールディング オプションが追加されています。

![](mvc3-release-notes/_static/image1.png)

既定では、3 種類のスキャフォールディング テンプレートが表示されます。

#### <a name="empty-controller"></a>空のコントローラー

このテンプレートは、空のコントローラー ファイルを生成します。 このテンプレートは、以前のバージョンの ASP.NET MVC の*作成、編集、詳細、削除の各シナリオに対して [アクションの追加*] チェックボックスをオンにすることと同じです。 このテンプレートを選択した場合、その他のオプションは利用できません。

#### <a name="controller-with-empty-readwrite-actions"></a>空の読み取り/書き込み操作のあるコントローラー

このテンプレートは、実装コードが設定されていませんが、必要なアクション メソッドがすべてあるコントローラー ファイルを生成します。 このテンプレートは、以前のバージョンの ASP.NET MVC の*作成、編集、詳細、削除の各シナリオに対する追加アクション*を確認することと同じです。 このテンプレートを選択した場合、その他のオプションは利用できません。

#### <a name="controller-with-readwrite-actions-and-views-using-entity-framework"></a>Entity Framework を使用した、読み取り/書き込み操作とビューのあるコントローラー

このテンプレートでは、運用可能なデータ入力ユーザー インターフェイスをすばやく作成できます。 次のような、さまざまな一般的な要件やシナリオに対応するコードが生成されます。

- *データアクセス*。 生成されたコードは、データベースのエンティティの読み取りおよび書き込みを行います。 既存のデータコンテキストクラスを選択した場合、またはテンプレートに新しい*Dbcontext*クラスを生成させる場合は、Entity Framework Code First の方法で動作します。 また、既存の*ObjectContext*クラスを選択した場合は、Entity Framework Database First または Model First アプローチでも機能します。
- *検証*。 生成されたコードは、ASP.NET MVC モデル バインディング機能とメタデータ機能を使用して、モデル クラスで宣言している規則に従ってフォーム送信が検証されるようにします。 これには、*必須*の属性や*stringlength*属性などの組み込みの検証規則や、カスタム検証規則が含まれます。
- *一対多のリレーションシップ*。 モデル クラス間に一対多外部キーリレーションシップを定義する場合、生成されたコードは関連エンティティを選択するためのドロップダウン リストを生成します。 たとえば、Entity Framework Code First 規約に従って、次のモデル クラスを定義するとします。 

    [!code-csharp[Main](mvc3-release-notes/samples/sample5.cs)]

    その後、 *product*クラスのコントローラーをスキャフォールディングすると、そのビューでは、ユーザーが各*製品*インスタンスの*カテゴリ*オブジェクトを選択できるようになります。

    このテンプレートは、[コントローラーの*追加*] ダイアログボックスで追加のオプションを有効にします。 [*モデルクラス*] では、ソリューション内の任意のモデルクラスを選択できます。これにより、ユーザーが作成または編集できるデータの種類が決まります。
- Entity Framework Code First を使用する場合は、どのモデル クラスを選択してもかまいません。
- Entity Framework Database First または Entity Framework Model First を使用する場合は、必ず、概念モデルに定義されているエンティティ クラスを選択してください。

*データコンテキストクラス*では、次の選択を行うことができます。

- Code First を使用し、既存のデータコンテキストクラスがない場合は、* * [新しいデータコンテキスト] * * を選択します。 これにより、データ コンテキスト クラスが自動的に生成されます。
- Code First を使用する場合に既存のデータ コンテキストがある場合は、そのコンテキストを選択します。 選択したモデル クラスを保持するように、コンテキストが更新されます。
- Database First または Model First を使用する場合は、オブジェクト コンテキスト クラスを選択します。

[ビュー] では、使用するビュー エンジンを選択するか、ビューのスキャフォールディングを行わない場合は [なし] を選択します。

[詳細設定] を選択すると、生成されるビューのオプションをさらに指定できます。 たとえば、使用するレイアウトやマスター ページを選択できます。

<a id="tu-ImprovementsNewDialogBox"></a>
### <a name="improvements-to-the-aspnet-mvc-3-new-project-dialog-box"></a>[新しい ASP.NET MVC 3 プロジェクト] ダイアログ ボックスの機能強化

新しい ASP.NET MVC 3 プロジェクトの作成に使用するダイアログボックスには、次に示すように、複数の機能強化が含まれています。

![](mvc3-release-notes/_static/image2.png)

#### <a name="new-intranet-project-template"></a>"イントラネット プロジェクト" テンプレートの導入

[プロジェクト テンプレート] の一覧に、"イントラネット アプリケーション" テンプレートが加わりました。 このテンプレートには、フォーム認証ではなく Windows 認証を使用する Web アプリケーションを作成するための設定が含まれています。 イントラネットアプリケーションでは、プロジェクトテンプレートにカプセル化できないいくつかの IIS 設定が必要であるため、テンプレートには、プロジェクトテンプレートを IIS で動作させるための手順を示す readme ファイルが含まれています。 新しいイントラネットアプリケーションテンプレートのドキュメントについては、MSDN web サイトの次の URL を参照してください。

[https://msdn.microsoft.com/library/gg703322(VS.98).aspx](https://msdn.microsoft.com/library/gg703322(VS.98).aspx)

#### <a name="project-templates-are-now-html5-enabled"></a>プロジェクト テンプレートが HTML5 に対応

プロジェクトの新規作成ダイアログ ボックスに、HTML5 固有の機能をプロジェクト テンプレートに追加するオプションが追加されました。 このオプションを選択すると、新しい HTML5 `<header>`、`<footer>`、および `<navigation>` 要素を含むビューが生成されます。

ただし、古いバージョンのブラウザーでは、HTML5 固有のタグがサポートされていないことに注意してください。 この制限に対応するため、HTML5 プロジェクト テンプレートには、Modernizr ライブラリへの参照が含まれています (次のセクションを参照してください)。

<a id="tu-Modernizr"></a>
### <a name="project-templates-now-include-modernizr-17"></a>プロジェクトテンプレートに Modernizr 1.7 が含まれるようになりました

Modernizr は、これらの機能をまだサポートしていないブラウザーで CSS 3 と HTML5 のサポートを有効にする JavaScript ライブラリです。 このライブラリは、ASP.NET MVC 3 プロジェクトのテンプレートに、事前にインストールされた NuGet パッケージとして含まれています。 Modernizr の詳細については、「 [http://www.modernizr.com/](http://www.modernizr.com/)」を参照してください。

<a id="tu-UpdatedJQuery"></a>
### <a name="project-templates-include-updated-versions-of-jquery-jquery-ui-and-jquery-validation"></a>プロジェクト テンプレートの jQuery、jQuery UI、および jQuery Validation のバージョンが新しく

プロジェクト テンプレートの jQuery スクリプトが次のバージョンになりました。

- jQuery 1.5.1
- jQuery Validation 1.8
- jQuery UI 1.8.11

これらのライブラリは、NuGet プレインストール パッケージとして含まれています。

<a id="tu-EF"></a>
### <a name="project-templates-now-include-adonet-entity-framework-41-as-a-pre-installed-nuget-package"></a>プロジェクトテンプレートに、事前にインストールされた NuGet パッケージとして ADO.NET Entity Framework 4.1 が含まれるようになりました

ADO.NET Entity Framework 4.1 には、Code First 機能が含まれています。 Code First は既存の Database First パターンや Model First パターンに代えて使用できる ADO.NET Entity Framework の新しい開発パターンです。

Code First は、Visual Basic または C# で記述された POCO クラス ("plain old CLR object") を使用するモデルを定義するための機能です。 これらのクラスは、既存のデータベースにマップするか、データベース スキーマの生成に使用できます。 *Dataannotations*属性を使用するか、fluent api を使用して、追加の構成を指定できます。

Code Firstwith ASP.NET MVC の使用に関するドキュメントは、ASP.NET の web サイトの次の Url にあります。

[https://www.asp.net/mvc/tutorials/getting-started-with-mvc3-part1-cs](../mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) [https://www.asp.net/entity-framework/tutorials/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)

<a id="tu-JavaScriptLibsNuget"></a>
### <a name="project-templates-include-javascript-libraries-as-pre-installed-nuget-packages"></a>プロジェクト テンプレートに、NuGet プレインストール パッケージとして JavaScript ライブラリが追加

新しい ASP.NET MVC 3 プロジェクトを作成する場合、プロジェクトには、プロジェクトテンプレートの Scripts フォルダーにスクリプトを直接追加するのではなく、NuGet を使用してインストールした JavaScript ファイル (Modernizr ライブラリなど) が含まれます。内容. これにより、スクリプトの新しいバージョンがリリースされたときに、NuGet を使用してスクリプトを最新バージョンに更新できます。

たとえば、jQuery の新しいリリースが提供される頻度を考えると、プロジェクトに含まれる jQuery のバージョンは、ある時点で古くなります。 しかし、jQuery はインストール済みの NuGet パッケージとして含まれているため、jQuery の新しいバージョンが公開されると NuGet のダイアログ ボックスによって通知されます。

JQuery にはファイル名にバージョン番号が含まれているので、jQuery を最新バージョンに更新するには、jQuery ファイルを参照する `<script>` タグを更新して、新しいファイル名を使用する必要もあります。 プロジェクトに含まれるその他のスクリプト ライブラリでは、スクリプト名にバージョン番号は含まれていないため、より簡単に最新バージョンに更新できます。

<a id="tu-KI"></a>
## <a name="known-issues"></a>既知の問題

- 場合によっては、インストールが失敗し、"インストールに失敗しました。エラーコード (0x80070643)" というエラーメッセージが表示されることがあります。 この問題を回避する方法については、サポート技術情報の[記事 2531566](https://support.microsoft.com/kb/2531566)を参照してください。
- コントローラーを追加するためのスキャフォールディングでは、Entity Framework 内のエンティティ継承サポートを利用するエンティティはスキャフォールディングされません。 たとえば、 *student*クラスによって継承される基本*Person*クラスを指定した場合、*学生*クラスをスキャフォールディングすると、コンパイルされないコードが生成されます。
- ソリューションフォルダー内に新しい ASP.NET MVC 3 プロジェクトを作成すると、 *NullReferenceException*エラーが発生します。 この問題を回避するには、ソリューションのルートに ASP.NET MVC 3 プロジェクトを作成し、ソリューションフォルダーに移動します。
- Razor 構文の IntelliSense は、ReSharper がインストールされていると機能しません。 再インストールが完了していて、ASP.NET MVC 3 で Razor IntelliSense のサポートを利用する場合は、「 [Razor intellisense](https://blogs.jetbrains.com/dotnet/2010/11/razor-intellisense-and-resharper/)の使用」と「Hadi Hariri のブログ」を参照してください。これについては、現在の方法について説明しています。
- インストール中にライセンス条項への同意を確認するためのダイアログ ボックスで、意図したよりも小さいウィンドウにライセンス条項が表示されます。
- Razor ビュー (cshtml またはを編集する場合。*vbhtml*ファイル)、ビュー。 ASP.NET MVC 3 には Razor ビューのスニペットは含まれていません。「」を参照してください。ASP.NET MVC のコードスニペットを選択すると、のスニペットが表示されます。
- Visual Studio がインストールされていないコンピューターに ASP.NET MVC 3 for Visual Web Developer Express をインストールし、後で Visual Studio をインストールする場合は、ASP.NET MVC 3 を再インストールする必要があります。 Visual Studio と Visual Web Developer Express は、ASP.NET MVC 3 インストーラーによってアップグレードされるコンポーネントを共有します。 Visual Web Developer Express がインストールされていないコンピューターに ASP.NET MVC 3 for Visual Studio をインストールし、後で Visual Web Developer Express をインストールした場合も、同じ問題が発生します。

<a id="MVC3RTM"></a>
## <a name="changes-in-aspnet-mvc-3-rtm"></a>ASP.NET MVC 3 RTM での変更点

このセクションでは、RC2 リリース以降の ASP.NET MVC 3 RTM リリースで行われた変更点とバグ修正について説明します。

<a id="RTM-1"></a>
### <a name="change-updated-the-version-of-jquery-ui-to-187"></a>変更: jQuery UI のバージョンを1.8.7 に更新しました

Visual Studio 用の ASP.NET MVC プロジェクトテンプレートが更新され、jQuery UI ライブラリの最新バージョンが追加されました。 テンプレートには、関連する CSS ファイルやイメージファイルなど、jQuery UI で必要な最小限のリソースファイルも含まれています。

<a id="RTM-2"></a>
### <a name="change-changed-the-default-modelmetadataprovider-back-to-dataannotationsmodelmetadataprovider"></a>変更: 既定の ModelMetadataProvider を Data注釈の内容に変更しました。

ASP.NET MVC 3 の RC2 リリースでは、パフォーマンス向上のために、既存の*Data注釈*の CachedDataAnnotationsMetadataProvider クラスの上にキャッシュを提供するクラスが導入されました。 ただし、一部のバグはこの実装で報告されたため、変更は元に戻され、 [ASP.NET WebStack](https://github.com/aspnet/AspNetWebStack)で利用できる MVC 計画プロジェクトに移動されました。

<a id="RTM-3"></a>
### <a name="fixed-pasting-part-of-a-razor-expression-that-contains-whitespace-results-in-it-being-reversed"></a>修正: 空白を含む Razor 式の一部を貼り付けると、元に戻されます。

ASP.NET MVC 3 のプレリリース版では、Razor ファイルに空白を含む Razor 式の一部を貼り付けると、結果として得られる式が反転されます。 たとえば、次の Razor コードブロックについて考えてみます。

[!code-cshtml[Main](mvc3-release-notes/samples/sample6.cshtml)]

最初のメソッドで "first param" というテキストを選択し、2番目のメソッドに引数として貼り付けると、結果は次のようになります。

[!code-cshtml[Main](mvc3-release-notes/samples/sample7.cshtml)]

正しい動作では、貼り付け操作の結果は次のようになります。

[!code-cshtml[Main](mvc3-release-notes/samples/sample8.cshtml)]

この問題は、貼り付け操作中に式が正しく保持されるように、RTM リリースで修正されました。

<a id="RTM-4"></a>
### <a name="fixed-renaming-a-razor-file-that-is-opened-in-the-editor-disables-syntax-colorization-and-intellisense"></a>修正: エディターで開いた Razor ファイルの名前を変更すると、構文の色付けと IntelliSense が無効になります。

ファイルがエディターウィンドウで開かれているときにソリューションエクスプローラーを使用して Razor ファイルの名前を変更すると、そのファイルに対して構文の強調表示や IntelliSense の動作が停止します。 これは修正され、名前の変更後に強調表示と IntelliSense が維持されるようになりました。

<a id="RTM-KI"></a>
## <a name="known-issues"></a>既知の問題

- NuGet パッケージマネージャーコンソールが開いているときに Visual Studio 2010 SP1 Beta を閉じると、Visual Studio がクラッシュし、再起動が試行されます。 これは、Visual Studio 2010 SP1 の RTM リリースで修正される予定です。
- ASP.NET MVC 3 インストーラーでは、NuGet パッケージマネージャーの初期バージョンのみをインストールできます。 初期バージョンをインストールした後、Visual Studio 拡張機能マネージャーを使用して NuGet をインストールし、更新することができます。 NuGet が既にインストールされている場合は、Visual Studio 拡張機能ギャラリーにアクセスして、最新バージョンの NuGet に更新してください。
- ソリューションフォルダー内に新しい ASP.NET MVC 3 プロジェクトを作成すると、 *NullReferenceException*エラーが発生します。 この問題を回避するには、ソリューションのルートに ASP.NET MVC 3 プロジェクトを作成し、ソリューションフォルダーに移動します。
- インストーラーを完了するには、以前のバージョンの ASP.NET MVC よりもはるかに長い時間がかかることがあります。 これは、Visual Studio 2010 のコンポーネントを更新するためです。
- Razor 構文の IntelliSense は、ReSharper がインストールされていると機能しません。 再インストールが完了していて、ASP.NET MVC 3 で Razor IntelliSense のサポートを利用する場合は、「 [Razor intellisense](https://blogs.jetbrains.com/dotnet/2010/11/razor-intellisense-and-resharper/)の使用」と「Hadi Hariri のブログ」を参照してください。これについては、現在の方法について説明しています。
- ASP.NET MVC 3 のベータ版で作成された CCSHTML および VBHTML ビューには、ビルドアクションが正しく設定されていません。その結果、プロジェクトの発行時にこれらのビューの種類が省略されます。 これらのファイルのビルドアクション値は、"Content" に設定する必要があります。 ASP.NET MVC 3 RTM では、新しいファイルのこの問題を修正しますが、プレリリースバージョンで作成されたプロジェクトの既存のファイルの設定は修正されません。
- ![](mvc3-release-notes/_static/image3.png)
- インストール中にライセンス条項への同意を確認するためのダイアログ ボックスで、意図したよりも小さいウィンドウにライセンス条項が表示されます。
- Razor ビュー (cshtml ファイル) を編集しているときに、Visual Studio の [コントローラーへのジャンプ] メニュー項目は使用できず、コードスニペットもありません。
- Visual Studio がインストールされていないコンピューターに ASP.NET MVC 3 for Visual Web Developer Express をインストールし、後で Visual Studio をインストールする場合は、ASP.NET MVC 3 を再インストールする必要があります。 Visual Studio と Visual Web Developer Express は、ASP.NET MVC 3 インストーラーによってアップグレードされるコンポーネントを共有します。 Visual Web Developer Express がインストールされていないコンピューターに ASP.NET MVC 3 for Visual Studio をインストールし、後で Visual Web Developer Express をインストールした場合も、同じ問題が発生します。

<a id="RTM-BC"></a>
## <a name="breaking-changes"></a>互換性に影響する変更点

- 以前のバージョンの ASP.NET MVC では、アクションフィルターは、いくつかのケースを除き、要求ごとに作成されます。 この動作は保証される動作ではありませんが、実装の詳細だけでなく、フィルターのコントラクトによってステートレスであると見なされていました。 ASP.NET MVC 3 では、フィルターはより積極的にキャッシュされます。 そのため、インスタンスの状態を不適切に格納するカスタムアクションフィルターが壊れている可能性があります。
- 同じ*順序*の値を持つ例外フィルターの実行順序が変更されました。 ASP.NET MVC 2 以前では、アクションメソッドの例外フィルターと同じ*順序*値を持つコントローラー上の例外フィルターが、アクションメソッドの例外フィルターの前に実行されます。 これは通常、特定の*順序*の値を指定せずに例外フィルターが適用された場合に発生します。 ASP.NET MVC 3 では、最も具体的な例外ハンドラーが最初に実行されるように、この順序は逆になっています。 以前のバージョンと同様に、 *order*プロパティが明示的に指定されている場合、フィルターは指定された順序で実行されます。
- *FileExtensions*という名前の新しいプロパティが*Virtualpathproviderviewengine*基本クラスに追加されました。 ASP.NET が (名前ではなく) パスによってビューを検索する場合、この新しいプロパティで指定されたリストに含まれるファイル拡張子を持つビューだけが考慮されます。 これは、Web フォームビューでカスタムファイル拡張子を有効にするためにカスタムビルドプロバイダーが登録されているアプリケーションの互換性に影響する変更点です。また、プロバイダーは名前ではなく完全パスを使用してこれらのビューを参照します。 回避策として、 *FileExtensions*プロパティの値を変更して、カスタムファイル拡張子を含めることができます。
- *IControllerFactory*インターフェイスを直接実装するカスタムコントローラーファクトリの実装では、このリリースのインターフェイスに追加された新しい*Getcontroller sessionbehavior*メソッドの実装を提供する必要があります。 一般に、このインターフェイスを直接実装せずに、代わりに*Defaultコントローラーファクトリ*からクラスを派生させることをお勧めします。

<a id="_Toc2"></a>
## <a name="changes-in-aspnet-mvc-3-rc2"></a>ASP.NET MVC 3 RC2 の変更点

このセクションでは、RC リリース以降の ASP.NET MVC 3 RC2 リリースで行われた変更 (新機能とバグ修正) について説明します。

<a id="_Toc2_1"></a>
### <a name="project-templates-changed-to-include-jquery-144-jquery-validation-17-and-jquery-ui-186"></a>JQuery 1.4.4、jQuery Validation 1.7、jQuery UI 1.8.6 を含むようにプロジェクトテンプレートが変更されました

ASP.NET MVC 3 のプロジェクトテンプレートには、jQuery、jQuery Validation、jQuery UI の最新バージョンが含まれるようになりました。 jQuery UI は、プロジェクトテンプレートに新しく追加されたもので、便利なユーザーインターフェイスウィジェットを提供します。 JQuery UI の詳細については、ホームページの「 [http://jqueryui.com/](http://jqueryui.com/)」を参照してください。

<a id="_Toc2_2"></a>
### <a name="added-additionalmetadataattribute-class"></a>"AdditionalMetadataAttribute" クラスを追加しました

*Additionalmetadataattribute*クラスを使用して、モデルプロパティの*Modelmetadata. additionalvalues*ディクショナリを設定できます。

たとえば、ビューモデルに、管理者にのみ表示する必要があるプロパティがあるとします。 このモデルには、次の例に示すように、キーとして AdminOnly を使用し、値として true を使用して、新しい属性で注釈を付けることができます。

[!code-csharp[Main](mvc3-release-notes/samples/sample9.cs)]

このメタデータは、製品ビューモデルがレンダリングされるときに、任意の表示またはエディターテンプレートで使用できるようになります。 アプリケーション開発者は、メタデータ情報を解釈する必要があります。

<a id="_Toc2_3"></a>
### <a name="improved-view-scaffolding"></a>ビューのスキャフォールディングの向上

スキャフォールディングビューに使用される T4 テンプレートで、 *TextBoxFor*などのヘルパーではなく、 *editorfor*のようなテンプレートヘルパーメソッドの呼び出しが生成されるようになりました。 この変更により、[ビューの追加] ダイアログボックスでビューが生成されたときのデータ注釈属性の形式で、モデルのメタデータのサポートが向上します。

また、[ビューの追加] スキャフォールディングには、規則に基づいて、モデルの主キー情報の検出と使用が改善されています。 たとえば、[ビューの追加] ダイアログボックスでは、この情報を使用して、主キーの値が編集可能なフォームフィールドとしてスキャフォールディングされないようにします。

既定の編集テンプレートと作成テンプレートには、クライアント検証に必要な jQuery スクリプトへの参照が含まれています。

<a id="_Toc2_4"></a>
### <a name="added-htmlraw-method"></a>追加された Html. Raw メソッド

既定では、Razor ビューエンジンはすべての値を HTML エンコードします。 たとえば、次のコードスニペットは、`<strong>Hello World!</strong>`としてページに表示されるように、あいさつ変数内の HTML をエンコードします。

[!code-cshtml[Main](mvc3-release-notes/samples/sample10.cshtml)]

新しい*html の未加工*のメソッドを使用すると、コンテンツが安全であることがわかっている場合に、エンコードされていない Html を簡単に表示できます。 次の例では、同じ文字列を表示しますが、文字列はマークアップとして表示されます。

[!code-cshtml[Main](mvc3-release-notes/samples/sample11.cshtml)]

<a id="_Toc2_5"></a>
### <a name="renamed-controllerviewmodel-property-and-the-view-property-to-viewbag"></a>"Controller. ビュー名" プロパティと "View" プロパティの名前を "ViewBag" に変更しました

以前は、*コントローラー*のビュー*モデル*プロパティは、ビューの*view*プロパティにこれしていました。 これらのプロパティはどちらも、動的なプロパティアクセサー構文を使用して*ViewDataDictionary*オブジェクトの値にアクセスする方法を提供します。 混乱を回避し、一貫性を高めるために、両方のプロパティの名前が同じに変更されました。

<a id="_Toc2_6"></a>
### <a name="renamed-controllersessionstateattribute-class-to-sessionstateattribute"></a>"ControllerSessionStateAttribute" クラスの名前を "SessionStateAttribute" に変更しました

*ControllerSessionStateAttribute*クラスは、ASP.NET MVC 3 の RC リリースで導入されました。 プロパティの名前がより簡潔に変更されました。

<a id="_Toc2_7"></a>
### <a name="renamed-remoteattribute-fields-property-to-additionalfields"></a>RemoteAttribute "Fields" プロパティの名前を "AdditionalFields" に変更しました

*Remoteattribute*クラスの*Fields*プロパティによって、ユーザー間でいくつかの混乱が発生しました。 このプロパティの名前を*Additionalfields*に変更すると、その意図が明確になります。

<a id="_Toc2_8"></a>
### <a name="renamed-skiprequestvalidationattribute-to-allowhtmlattribute"></a>"SkipRequestValidationAttribute" を "AllowHtmlAttribute" に変更しました

*SkipRequestValidationAttribute*属性の名前が*AllowHtmlAttribute*に変更され、目的の用途がより適切に表されました。

<a id="_Toc2_9"></a>
### <a name="changed-htmlvalidationmessage-method-to-display-the-first-useful-error-message"></a>最初の役に立つエラーメッセージを表示するように "Html. ValidationMessage" メソッドを変更しました

最初のエラーを表示するのではなく、最初の便利なエラーメッセージを表示するように*Html の ValidationMessage*メソッドが修正されました。

モデルバインド中に、 *Modelstate*ディクショナリは、プロパティに関するエラーメッセージを含む複数のソースから作成できます。これには、モデル自体 ( *IValidatableObject*を実装している場合)、プロパティに適用された検証属性、およびプロパティにアクセスしている間にスローされた例外が含まれます。

Html の*validationmessage*メソッドは、検証メッセージを表示するときに、例外を含むモデル状態エントリをスキップします。これは通常、エンドユーザー向けのものではないためです。 代わりに、メソッドは、例外に関連付けられていない最初の検証メッセージを検索し、そのメッセージを表示します。 このようなメッセージが見つからない場合、既定では、最初の例外に関連付けられている一般的なエラーメッセージが表示されます。

<a id="_Toc2_10"></a>
### <a name="fixed-model-declaration-to-not-add-whitespace-to-the-document"></a>ドキュメントに空白を追加しないように @model 宣言を修正した

以前のリリースでは、ビューの上部にある `@model` 宣言によって、表示される HTML 出力に空白行が追加されました。 これは修正され、宣言によって空白が導入されないようになっています。

<a id="_Toc2_11"></a>
### <a name="added-fileextensions-property-to-view-engines-to-support-engine-specific-file-names"></a>エンジン固有のファイル名をサポートするための "FileExtensions" プロパティをビューエンジンに追加しました

ビューエンジンは、次の例のように、明示的なビューパスを使用してビューを返すことができます。

[!code-csharp[Main](mvc3-release-notes/samples/sample12.cs)]

最初のビューエンジンは、常にビューを表示しようとします。 既定では、Web フォームビューエンジンは最初のビューエンジンです。Web フォームエンジンは Razor ビューを表示できないため、エラーが発生します。 ビューエンジンには、サポートするファイル拡張子を指定するための*FileExtensions*プロパティが用意されました。 このプロパティは、ASP.NET がビューエンジンがファイルを表示できるかどうかを判断するときにチェックされます。 これは互換性に影響する変更点で、詳細については、このドキュメントの「互換性に影響する[変更点](#_Toc2_BC)」を参照してください。

<a id="_Toc2_12"></a>
### <a name="fixed-labelfor-helper-to-emit-the-correct-value-for-the-for-attribute"></a>"For" 属性の正しい値を出力するように "LabelFor" ヘルパーを修正しています

バグが修正されました。*このメソッドでは、ID*ではなく、*入力*要素の*name*属性に一致する for 属性が*に*よって表示されます。 W3C によれば、 *for*属性は*入力*要素の ID と一致している必要があります。

<a id="_Toc2_13"></a>
### <a name="fixed-renderaction-method-to-give-explicit-values-precedence-during-model-binding"></a>モデルバインド中に明示的な値の優先順位を指定するように "RenderAction" メソッドを修正した

以前のバージョンでは、 *renderaction*メソッドに渡された明示的な値は、子アクション内のモデルバインド時に現在のフォーム値を優先して無視されていました。 修正により、モデルバインド中に明示的な値が優先されるようになります。

<a id="_Toc2_BC"></a>
## <a name="breaking-changes"></a>互換性に影響する変更点

- 以前のバージョンの ASP.NET MVC では、いくつかのケースを除き、要求ごとにアクションフィルターが作成されました。 この動作は保証される動作ではありませんが、実装の詳細だけでなく、フィルターのコントラクトによってステートレスであると見なされていました。 ASP.NET MVC 3 では、フィルターはより積極的にキャッシュされます。 そのため、インスタンスの状態を不適切に格納するカスタムアクションフィルターが壊れている可能性があります。
- 同じ*順序*の値を持つ例外フィルターの実行順序が変更されました。 ASP.NET MVC 2 以前では、アクションメソッドの例外フィルターの前に、アクションメソッドと同じ*順序*値を持つコントローラーの例外フィルターが実行されました。 これは通常、特定の*順序*の値を指定せずに例外フィルターが適用された場合に発生します。 ASP.NET MVC 3 では、最も具体的な例外ハンドラーが最初に実行されるように、この順序は逆になっています。 以前のバージョンと同様に、 *order*プロパティが明示的に指定されている場合、フィルターは指定された順序で実行されます。
- *FileExtensions*という名前の新しいプロパティが*Virtualpathproviderviewengine*基本クラスに追加されました。 ASP.NET が (名前ではなく) パスによってビューを検索する場合、この新しいプロパティで指定されたリストに含まれるファイル拡張子を持つビューだけが考慮されます。 これは、Web フォームビューでカスタムファイル拡張子を有効にするためにカスタムビルドプロバイダーが登録されているアプリケーションの互換性に影響する変更点です。また、プロバイダーは名前ではなく完全パスを使用してこれらのビューを参照します。 回避策として、 *FileExtensions*プロパティの値を変更して、カスタムファイル拡張子を含めることができます。
- *IControllerFactory*インターフェイスを直接実装するカスタムコントローラーファクトリの実装では、このリリースのインターフェイスに追加された新しい*Getcontroller sessionbehavior*メソッドの実装を提供する必要があります。 一般に、このインターフェイスを直接実装せずに、代わりに*Defaultコントローラーファクトリ*からクラスを派生させることをお勧めします。

<a id="_Toc2_KI"></a>
## <a name="known-issues"></a>既知の問題

- ASP.NET MVC 3 インストーラーでは、NuGet パッケージマネージャーの初期バージョンのみをインストールできます。 初期バージョンをインストールした後、Visual Studio 拡張機能マネージャーを使用して NuGet をインストールし、更新することができます。 NuGet が既にインストールされている場合は、Visual Studio 拡張機能ギャラリーにアクセスして、最新バージョンの NuGet に更新してください。
- ソリューションフォルダー内に新しい ASP.NET MVC 3 プロジェクトを作成すると、 *NullReferenceException*エラーが発生します。 この問題を回避するには、ソリューションのルートに ASP.NET MVC 3 プロジェクトを作成し、ソリューションフォルダーに移動します。
- インストーラーを完了するには、以前のバージョンの ASP.NET MVC よりもはるかに長い時間がかかることがあります。 これは、Visual Studio 2010 のコンポーネントを更新するためです。
- Razor 構文の IntelliSense は、ReSharper がインストールされていると機能しません。 再インストールが完了していて、ASP.NET MVC 3 RC2 で Razor IntelliSense のサポートを利用する場合は、「 [Razor intellisense](https://blogs.jetbrains.com/dotnet/2010/11/razor-intellisense-and-resharper/)の使用」と「Hadi Hariri のブログ」を参照してください。これについては、現在の方法に関する記事をご覧ください。
- ASP.NET MVC 3 のベータ版で作成された CSHTML および VBHTML ビューには、ビルドアクションが正しく設定されていません。その結果、プロジェクトの発行時にこれらのビューの種類が省略されます。 これらのファイルの*ビルドアクション*値は、[コンテンツ] に設定する必要があります。 ASP.NET MVC 3 RC2 は、新しいファイルに対してこの問題を修正しますが、ベータバージョンで作成されたプロジェクトの既存のファイルの設定は修正しません。![](mvc3-release-notes/_static/image4.png)
- インストール中にライセンス条項への同意を確認するためのダイアログ ボックスで、意図したよりも小さいウィンドウにライセンス条項が表示されます。
- Razor ビュー (cshtml ファイル) を編集しているときに、Visual Studio の [コントローラーへのジャンプ] メニュー項目は使用できず、コードスニペットもありません。
- Visual Studio がインストールされていないコンピューターに ASP.NET MVC 3 for Visual Web Developer Express をインストールし、後で Visual Studio をインストールする場合は、ASP.NET MVC 3 を再インストールする必要があります。 Visual Studio と Visual Web Developer Express は、ASP.NET MVC 3 インストーラーによってアップグレードされるコンポーネントを共有します。 Visual Web Developer Express がインストールされていないコンピューターに ASP.NET MVC 3 for Visual Studio をインストールし、後で Visual Web Developer Express をインストールした場合も、同じ問題が発生します。
- ASP.NET MVC 3 RC 2 をインストールすると、NuGet は更新されません (既にインストールされている場合)。 NuGet をアップグレードするには、Visual Studio 拡張機能マネージャーにアクセスして、使用可能な更新プログラムとして表示する必要があります。 NuGet は、そこから最新リリースにアップグレードできます。

<a id="TOC_ASP_NET_3_RC"></a>
## <a name="aspnet-mvc-3-release-candidate"></a>ASP.NET MVC 3 リリース候補

ASP.NET MVC リリース候補は、2010年11月9日にリリースされました。

<a id="_Toc276711785"></a>
## <a name="new-features-in-aspnet-mvc-3-rc"></a>ASP.NET MVC 3 RC の新機能

このセクションでは、ベータリリース以降、ASP.NET MVC 3 RC リリースで導入された機能について説明します。

<a id="_Toc276711786"></a>
### <a name="nuget-package-manager"></a>NuGet パッケージ マネージャー

ASP.NET MVC 3 には、NuGet パッケージマネージャー (旧称 NuPack) が含まれています。これは、ライブラリとツールを Visual Studio プロジェクトに追加するための統合パッケージ管理ツールです。 このツールを使用すると、開発者がライブラリをソースツリーに取り込むための手順が自動化されます。

NuGet は、Visual Studio 2010 内の統合されたコンソールウィンドウ、Visual Studio のコンテキストメニュー、および一連の PowerShell コマンドレットとして、コマンドラインツールとして使用できます。

NuGet の詳細については、 [nuget のドキュメント](https://docs.microsoft.com/nuget/)を参照してください。

<a id="_Toc276711787"></a>
### <a name="improved-new-project-dialog-box"></a>[新しいプロジェクト] ダイアログボックスの機能強化

新しいプロジェクトを作成すると、[新しいプロジェクト] ダイアログボックスで、ビューエンジンと ASP.NET MVC プロジェクトの種類を指定できるようになりました。

![](mvc3-release-notes/_static/image5.png)

このリリースでは、ダイアログボックスに一覧表示されているテンプレートおよびビューエンジンの一覧の変更がサポートされています。

既定のテンプレートは次のとおりです。

空。 ASP.NET MVC プロジェクトの最小限のファイルセットを格納します。これには、ASP.NET MVC プロジェクトの既定のディレクトリ構造、既定の ASP.NET MVC スタイルを含むサイト .css ファイル、および既定の JavaScript ファイルを含む Scripts ディレクトリが含まれます。

インターネットアプリケーション。 ASP.NET MVC でメンバーシッププロバイダーを使用する方法を示すサンプル機能が含まれています。

ダイアログボックスに表示されるプロジェクトテンプレートの一覧は、Windows レジストリで指定されます。

<a id="_Toc276711788"></a>
### <a name="sessionless-controllers"></a>セッションレスコントローラー

新しい*ControllerSessionStateAttribute*を使用すると、 [SessionState](https://msdn.microsoft.com/library/system.web.sessionstate.sessionstatebehavior.aspx)列挙値を指定することで、コントローラーのセッション状態の動作をより細かく制御できます。

次の例は、コントローラーに対するすべての要求のセッション状態をオフにする方法を示しています。

[!code-csharp[Main](mvc3-release-notes/samples/sample13.cs)]

次の例は、コントローラーに対するすべての要求に対して読み取り専用のセッション状態を設定する方法を示しています。

[!code-csharp[Main](mvc3-release-notes/samples/sample14.cs)]

<a id="_Toc276711789"></a>
### <a name="new-validation-attributes"></a>新しい検証属性

#### <a name="compareattribute"></a>CompareAttribute

新しい*compareattribute*検証属性を使用すると、モデルの2つの異なるプロパティの値を比較できます。 次の例では、有効にするために、 *comparepassword*プロパティが*パスワード*フィールドと一致している必要があります。

[!code-csharp[Main](mvc3-release-notes/samples/sample15.cs)]

#### <a name="remoteattribute"></a>RemoteAttribute

新しい*Remoteattribute*検証属性は、jQuery validation プラグインのリモート検証を利用します。これにより、クライアント側の検証で、実際の検証ロジックを実行するサーバー上でメソッドを呼び出すことができます。

次の例では、 *UserName*プロパティに*remoteattribute*が適用されています。 このプロパティを編集ビューで編集すると、クライアント検証は、このフィールドを検証するため*に、* *UserNameAvailable*という名前のアクションを、このフィールドに対して呼び出します。

[!code-csharp[Main](mvc3-release-notes/samples/sample16.cs)]

次の例は、対応するコントローラーを示しています。

[!code-csharp[Main](mvc3-release-notes/samples/sample17.cs)]

既定では、属性が適用されるプロパティ名は、クエリ文字列パラメーターとしてアクションメソッドに送信されます。

<a id="_Toc276711790"></a>
### <a name="new-overloads-for-labelfor-and-labelformodel-methods"></a>"LabelFor" メソッドと "LabelForModel" メソッドの新しいオーバーロード

ラベルのテキストを指定できる*labelfor*および*labelformodel*メソッドに新しいオーバーロードが追加されました。 これらのオーバーロードを使用する方法を次の例に示します。

[!code-cshtml[Main](mvc3-release-notes/samples/sample18.cshtml)]

<a id="_Toc276711791"></a>
### <a name="child-action-output-caching"></a>子アクションの出力キャッシュ

*Outputcacheattribute*は、 *Html の renderaction*または*html. action*ヘルパーメソッドを使用して呼び出される子アクションの出力キャッシュをサポートしています。 次の例は、別のアクションを呼び出すビューを示しています。

[!code-cshtml[Main](mvc3-release-notes/samples/sample19.cshtml)]

*GetDate*アクションには、 *outputcacheattribute*で注釈が付けられています。

[!code-csharp[Main](mvc3-release-notes/samples/sample20.cs)]

このコードを実行すると、Html. Action ("GetDate") の呼び出しの結果が100秒間キャッシュされます。

<a id="_Toc276711792"></a>
### <a name="add-view-dialog-box-improvements"></a>[ビューの追加] ダイアログボックスの機能強化

厳密に型指定されたビューを追加すると、[ビューの追加] ダイアログボックスでは、以前のリリース (多くのコア .NET Framework 型など) よりも適用できない型が除外されるようになりました。 また、リストは、完全修飾型名ではなくクラス名で並べ替えられるようになりました。これにより、型を簡単に見つけることができます。 たとえば、型名は次の例のように表示されるようになりました。

ClassName (名前空間)

以前のリリースでは、これは次のように表示されていました。

Namespace.ClassName

<a id="_Toc276711793"></a>
### <a name="granular-request-validation"></a>詳細な要求の検証

*Validateinputattribute*の*Exclude*プロパティは存在しません。 代わりに、モデルバインド中にモデルの特定のプロパティに対して要求の検証をスキップするには、新しい*SkipRequestValidationAttribute*を使用します。

たとえば、ブログの投稿を編集するためにアクションメソッドが使用されているとします。

[!code-csharp[Main](mvc3-release-notes/samples/sample21.cs)]

次の例は、ブログ投稿のビューモデルを示しています。

[!code-csharp[Main](mvc3-release-notes/samples/sample22.cs)]

ユーザーが Description プロパティのマークアップを送信すると、要求の検証によってモデルバインドが失敗します。 ブログ投稿の説明のモデルバインド中に要求の検証を無効にするには、次の例に示すように、 *SkipRequpestValidationAttribute*をプロパティに適用します。

[!code-csharp[Main](mvc3-release-notes/samples/sample23.cs)]

または、モデルのすべてのプロパティの要求の検証を無効にするには、アクションメソッドに値が*false*の*validateinputattribute*を適用します。

[!code-csharp[Main](mvc3-release-notes/samples/sample24.cs)]

<a id="_Toc276711794"></a>
## <a name="breaking-changes"></a>互換性に影響する変更点

- 同じ*順序*の値を持つ例外フィルターの実行順序が変更されました。 ASP.NET MVC 2 以前では、アクションメソッドの例外フィルターは、アクションメソッドの例外フィルターの前に実行さ*れてい*た、コントローラー上の例外フィルターが実行されました。 これは通常、特定の*順序*の値を指定せずに例外フィルターが適用された場合に発生します。 ASP.NET MVC 3 では、最も具体的な例外ハンドラーが最初に実行されるように、この順序は逆になっています。 以前のバージョンと同様に、 *order*プロパティが明示的に指定されている場合、フィルターは指定された順序で実行されます。
- *Virtualpathproviderviewengine*基本クラスに*FileExtensions*という名前の新しいプロパティを追加しました。 (名前ではなく) パスによってビューを検索する場合、この新しいプロパティで指定されたリストに含まれるファイル拡張子を持つビューだけが考慮されます。 これは、カスタムビルドプロバイダーを登録して web フォームビューのカスタムファイル拡張子を有効にし、名前ではなく完全パスを使用してそれらのビューを参照している場合に、互換性に影響する変更点です。 回避策として、 *FileExtensions*プロパティの値を変更して、カスタムファイル拡張子を含めることができます。

<a id="_Toc276711795"></a>
## <a name="known-issues"></a>既知の問題

- インストーラーは、Visual Studio 2010 のコンポーネントを更新するため、以前のバージョンの ASP.NET MVC よりもはるかに長い時間がかかることがあります。
- Astrongly に型指定されたビューを選択するときの Add View スキャフォールディングは、書き込み専用のプロパティをスキャフォールディングします。 これらは、スキャフォールディングによって常に無視されます。 [ビューの追加] ダイアログボックスでは、[編集] ビューまたは [作成] ビューを生成するときに、読み取り専用プロパティもスキャフォールディングされます。 読み取り専用プロパティは、表示ビューとリストビューに対してのみスキャフォールディングにする必要があります。
- 非同期 CTP と共に ASP.NET MVC 3 がインストールされている場合、デバッグは機能しません。 ASP.NET MVC 3 は、非同期 CTP とサイドバイサイドでインストールすることはできません。 デバッグを修復するには、非同期 CTP をアンインストールしてください。 詳細については、ASP.NET MVC 3 RC のすべての部分のアンインストールに関する[ブログ投稿](http://drew-prog.blogspot.com/2010/11/how-to-uninstall-microsoft-aspnet-mvc-3.html)を参照してください。
- Razor Intellisense は、再シャープ化がインストールされている場合は機能しません。 再インストールが完了していて、ASP.NET MVC 3 RC で Razor intellisense サポートを利用する場合は、JetBrains からの[このブログ](https://blogs.jetbrains.com/dotnet/2010/11/razor-intellisense-and-resharper/)記事をお読みください。これを使用する方法については、こちらを参照してください。
- ASP.NET MVC 3 のベータ版で作成された CSHTML ビューおよび VBHTML ビューには、発行から除外されるビルドアクションが正しくありません。 これらのファイルの*ビルドアクション*は、"Content" に設定する必要があります。 ASP.NET MVC 3 RC では、新しいファイルに対してこの問題を修正しますが、Beta で作成されたプロジェクトの既存のファイルの設定は修正されません。
- インストーラーは、Visual Studio 2010 のコンポーネントを更新するため、以前のバージョンの ASP.NET MVC よりもはるかに長い時間がかかることがあります。
- "Edit" 厳密に型指定されたビューを選択すると、ビューの追加スキャフォールディングは読み取り専用のプロパティをスキャフォールディングします。 同様に、書き込み専用プロパティは、"Display" ビューではスキャフォールディングです。
- インストール中にライセンス条項への同意を確認するためのダイアログ ボックスで、意図したよりも小さいウィンドウにライセンス条項が表示されます。
- Visual Studio Async CTP をインストールすると、ASP.NET MVC 3 ツールのインストールの一部として含まれている Razor リリースとの競合が発生します。 Visual Studio Async CTP と Razor リリースの両方を同じコンピューターにインストールしないようにしてください。
- Razor ビュー (cshtml ファイル) を編集しているときに、Visual Studio の [コントローラーへのジャンプ] メニュー項目は使用できず、コードスニペットもありません。

<a id="TOC_ASP_NET_3_Beta"></a>
## <a name="aspnet-mvc-3-beta"></a>ASP.NET MVC 3 ベータ版

ASP.NET MVC 3 Beta は、2010年10月6日にリリースされました。 次の注意事項は、ベータリリースに固有のものであり、上の「ASP.NET MVC 3 リリース候補」セクションで参照されている更新または変更の対象となります。

## <a id="0.1__Toc274034215"></a>ASP.NET MVC 3 Beta の新特長

<a id="0.1__Default_validation_system"></a>このセクションでは、ASP.NET MVC 3 ベータリリースで導入された機能について説明します。

### <a id="0.1__Toc274034216"></a>NuGet パッケージマネージャー

ASP.NET MVC 3 には、ライブラリとツールを Visual Studio プロジェクトに追加するための統合パッケージ管理ツールである NuGet パッケージマネージャーが含まれています。 ほとんどの場合、開発者がライブラリをソースツリーに取り込むために使用する手順が自動化されます。

NuGet は、Visual Studio 2010 内の統合されたコンソールウィンドウ、Visual Studio のコンテキストメニュー、および PowerShell コマンドレットのセットとして、コマンドラインツールとして使用できます。

NuGet の詳細については、 [nuget のドキュメント](https://docs.microsoft.com/nuget/)を参照してください。

### <a id="0.1__Toc274034217"></a>強化された [新しいプロジェクト] ダイアログボックス

新しいプロジェクトを作成すると、[新しいプロジェクト] ダイアログボックスで、ビューエンジンと ASP.NET MVC プロジェクトの種類を指定できるようになりました。

![](mvc3-release-notes/_static/image6.png)

このリリースでは、ダイアログボックスに一覧表示されているテンプレートおよびビューエンジンの一覧の変更はサポートされていません。

既定のテンプレートは次のとおりです。

空。 ASP.NET MVC プロジェクトの最小限のファイルセットを格納します。これには、ASP.NET MVC プロジェクトの既定のディレクトリ構造、既定の ASP.NET MVC スタイルを含む小さなサイト .css ファイル、および既定の JavaScript ファイルを含む Scripts ディレクトリが含まれます。

インターネットアプリケーション。 ASP.NET MVC 内でメンバーシッププロバイダーを使用する方法を示すサンプル機能が含まれています。

### <a id="0.1__Toc274034218"></a>Razor ビューで厳密に型指定されたモデルを指定するための簡略化された方法

厳密に型指定された Razor ビューのモデル型を指定する方法は、CSHTML ビュー用の新しい @model ディレクティブと、VBHTML ビュー用の @ModelType ディレクティブを使用することによって簡略化されています。 以前のバージョンの ASP.NET MVC では、この方法で Razor ビューに厳密に型指定されたモデルを指定します。

[!code-cshtml[Main](mvc3-release-notes/samples/sample25.cshtml)]

このリリースでは、次の構文を使用できます。

[!code-cshtml[Main](mvc3-release-notes/samples/sample26.cshtml)]

### <a id="0.1__Toc274034219"></a>新しい ASP.NET Web ページヘルパーメソッドのサポート

新しい ASP.NET Web ページテクノロジには、一般的に使用される機能をビューおよびコントローラーに追加するのに役立つ一連のヘルパーメソッドが含まれています。 ASP.NET MVC 3 では、コントローラーとビュー内でのこれらのヘルパーメソッドの使用がサポートされています (該当する場合)。 これらのメソッドは、system.servicemodel アセンブリに含まれています。 次の表に、ASP.NET Web ページヘルパーメソッドのいくつかを示します。

| **パー** | **説明** |
| --- | --- |
| グラフ | ビュー内のグラフを表示します。 Chart. ToWebImage、Chart. Save、および Chart. Write などのメソッドが含まれています。 |
| 暗号 | ハッシュアルゴリズムを使用して、適切なソルトおよびハッシュされたパスワードを作成します。 |
| WebGrid | オブジェクト (通常はデータベースのデータ) のコレクションをグリッドとして表示します。 ページングと並べ替えをサポートします。 |
| WebImage | イメージをレンダリングします。 |
| Web メール | 電子メールを送信します。 |

ヘルパーと基本構文の一覧に関するクイックリファレンストピックは、次の URL にある ASP.NET Razor 構文のドキュメントの一部として入手できます。

[https://www.asp.net/webmatrix/tutorials/asp-net-web-pages-api-reference](../web-pages/overview/api-reference/asp-net-web-pages-api-reference.md)

### <a id="0.1__Toc274034220"></a>追加の依存関係の挿入のサポート

現在のリリースでは、ASP.NET MVC 3 Preview 1 リリースを基盤として、2つの新しいサービスと4つの既存サービスのサポートが追加され、依存関係の解決と共通サービスロケーターのサポートが強化されています。

#### <a name="new-icontrolleractivator-interface-for-fine-grained-controller-instantiation"></a>粒度の細かいコントローラーのインスタンス化用の新しい IControllerActivator インターフェイス

新しい IControllerActivator インターフェイスを使用すると、依存関係の挿入によってコントローラーをインスタンス化する方法をより細かく制御できます。 次の例は、インターフェイスを示しています。

[!code-csharp[Main](mvc3-release-notes/samples/sample27.cs)]

これをコントローラーファクトリの役割と比較します。 コントローラーファクトリは IControllerFactory インターフェイスを実装したものであり、コントローラーの種類を特定し、そのコントローラーの種類のインスタンスをインスタンス化するための役割を担います。

コントローラーアクティベーターは、コントローラー型のインスタンスをインスタンス化するためだけに責任を持ちます。 コントローラーの種類の検索は実行されません。 コントローラーファクトリは、適切なコントローラーの種類を特定した後、コントローラーの実際のインスタンス化を処理するために、IControllerActivator のインスタンスに代行させる必要があります。

Defaultコントローラーファクトリクラスには、IControllerFactory インスタンスを受け入れる新しいコンストラクターがあります。 これにより、依存関係の挿入を適用して、コントローラーの作成のこの側面を管理できます。既定のコントローラーの型の参照動作をオーバーライドする必要はありません。

#### <a name="iservicelocator-interface-replaced-with-idependencyresolver"></a>IServiceLocator インターフェイスが Iservicelocator に置き換えられました

コミュニティからのフィードバックに基づき、ASP.NET MVC 3 ベータリリースでは、IServiceLocator インターフェイスの使用が ASP.NET MVC のニーズに固有の規模小さくダウンの Iservicelocator インターフェイスに置き換えられました。 次の例は、新しいインターフェイスを示しています。

[!code-csharp[Main](mvc3-release-notes/samples/sample28.cs)]

この変更の一環として、ServiceLocator クラスも DependencyResolver クラスに置き換えられました。 依存関係競合回避モジュールの登録は、以前のバージョンの ASP.NET MVC に似ています。

[!code-csharp[Main](mvc3-release-notes/samples/sample29.cs)]

このインターフェイスの実装は、要求された型の登録済みサービスを提供するために、基になる依存関係挿入コンテナーに単純にデリゲートする必要があります。

要求された型の登録済みサービスがない場合、ASP.NET MVC は、GetService から null を返し、GetServices から空のコレクションを返すために、このインターフェイスの実装を想定しています。

新しい DependencyResolver クラスを使用すると、新しい IDependencyResolver インターフェイスまたは共通サービスロケーターインターフェイス (Idependencyresolver) のいずれかを実装するクラスを登録できます。 一般的なサービスロケーターの詳細については、 [GitHub の「Commonservicelocator](https://github.com/unitycontainer/commonservicelocator)」を参照してください。

<a id="0.1__Breaking_Changes"></a>

#### <a name="new-iviewactivator-interface-for-fine-grained-view-page-instantiation"></a>詳細ビューページのインスタンス化用の新しい IViewActivator インターフェイス

新しい IViewPageActivator インターフェイスでは、依存関係の挿入によってビューページをインスタンス化する方法をより細かく制御できます。 これは、WebFormView インスタンスと RazorView インスタンスの両方に適用されます。 次の例は、新しいインターフェイスを示しています。

[!code-csharp[Main](mvc3-release-notes/samples/sample30.cs)]

これらのクラスは IViewPageActivator コンストラクター引数を受け取るようになりました。これにより、依存関係の挿入を使用して、ViewPage、ViewUserControl、および WebViewPage 型のインスタンス化方法を制御できます。

#### <a name="new-dependency-resolver-support-for-existing-services"></a>既存のサービスに対する新しい依存関係競合回避モジュールのサポート

新しいリリースには、次のサービスの依存関係解決のサポートが含まれています。

- モデル検証プロバイダー。 ModelValidatorProvider を実装するクラスは、依存関係競合回避モジュールに登録できます。また、これらのクラスを使用して、クライアント側およびサーバー側の検証をサポートします。
- モデルメタデータプロバイダー。 ModelMetadataProvider を実装する1つのクラスを依存関係競合回避モジュールに登録すると、システムはそれを使用してテンプレートおよび検証システムのメタデータを提供します。
- 値プロバイダー。 ValueProviderFactory を実装するクラスは、依存関係競合回避モジュールに登録できます。また、システムはこれらのクラスを使用して、コントローラーおよびモデルバインド中に使用される値プロバイダーを作成します。
- モデルバインダー。 にを実装するクラスは、依存関係競合回避モジュールに登録できます。また、これらのクラスを使用して、モデルバインドシステムによって使用されるモデルバインダーが作成されます。

### <a id="0.1__Toc274034221"></a>控えめな jQuery ベースの Ajax の新しいサポート

ASP.NET MVC には、次のような Ajax ヘルパーメソッドが含まれています。

- Html.actionlink
- Ajax. Teltelink
- Ajax. BeginForm
- Ajax. BeginRouteForm

これらのメソッドは、JavaScript を使用して、完全なポストバックを使用するのではなく、サーバー上でアクションメソッドを呼び出します。 この機能は、jQuery を控えめな方法で利用するように更新されました。 これらのヘルパーメソッドは、インラインクライアントスクリプトを出力するのではなく、*データ ajax*プレフィックスを使用して HTML5 属性を出力することによって、マークアップからの動作を分離します。 次に、適切な JavaScript ファイルを参照することによって、動作がマークアップに適用されます。 次の JavaScript ファイルが参照されていることを確認します。

- jquery-1.4.1
- jquery。 node.js

この機能は、ASP.NET MVC 3 の新しいプロジェクトテンプレートの Web.config ファイルでは既定で有効になっていますが、既存のプロジェクトでは既定で無効になっています。 詳細については、このドキュメントで後述する「[クライアント検証と控えめな JavaScript のためのアプリケーション全体のフラグの追加](#0.1_AddedApplicationWideFlagsForClientValida)」を参照してください。

### <a id="0.1__Toc274034222"></a>控えめな jQuery 検証の新しいサポート

既定では、ASP.NET MVC 3 Beta は、クライアント側の検証を実行するために、控えめな方法で jQuery 検証を使用します。 控えめなクライアント検証を有効にするには、ビュー内から次のような呼び出しを行います。

[!code-csharp[Main](mvc3-release-notes/samples/sample31.cs)]

これを行うには、UnobtrusiveJavaScriptEnabled プロパティが true に設定されている必要があります。これは、次の呼び出しを行うことによって行うことができます。

[!code-csharp[Main](mvc3-release-notes/samples/sample32.cs)]

また、次の JavaScript ファイルが参照されていることを確認します。

- jquery-1.4.1
- jquery. .js の検証
- jquery. 検証 (控えめ)

この機能は、ASP.NET MVC 3 の新しいプロジェクトテンプレートの Web.config ファイルでは既定で有効になっていますが、既存のプロジェクトでは既定で無効になっています。 詳細については、このドキュメントで後述する「[クライアント検証と控えめな JavaScript のための新しいアプリケーション全体のフラグ](#0.1_AddedApplicationWideFlagsForClientValida)」を参照してください。

<a id="0.1__Toc274034223"></a>

### <a id="0.1_AddedApplicationWideFlagsForClientValida"></a>クライアント検証と控えめな JavaScript のための新しいアプリケーション全体のフラグ

次の例のように、HtmlHelper クラスの静的メンバーを使用して、クライアント検証と控えめな JavaScript をグローバルに有効または無効にすることができます。

[!code-csharp[Main](mvc3-release-notes/samples/sample33.cs)]

既定のプロジェクトテンプレートでは、既定で控えめに設定された JavaScript が有効になります。 また、次の設定を使用して、アプリケーションのルート Web.config ファイルでこれらの機能を有効または無効にすることもできます。

[!code-xml[Main](mvc3-release-notes/samples/sample34.xml)]

これらの機能は既定で有効にできるため、次の例に示すように、既定の設定をオーバーライドできる HtmlHelper クラスに新しいオーバーロードが導入されました。

[!code-csharp[Main](mvc3-release-notes/samples/sample35.cs)]

旧バージョンとの互換性のために、これらの機能はどちらも既定で無効になっています。

### <a id="0.1__Toc274034224"></a>ビューの実行前に実行されるコードの新しいサポート

Views ディレクトリに \_viewstart. cshtml (または \_viewstart. vbhtml) という名前のファイルを配置し、そのディレクトリとそのサブディレクトリ内の複数のビュー間で共有されるコードを追加できるようになりました。 たとえば、次のコードを、~/Views フォルダーの \_viewstart. cshtml ページに配置できます。

[!code-cshtml[Main](mvc3-release-notes/samples/sample36.cshtml)]

これにより、Views フォルダー内のすべてのビューとそのすべてのサブフォルダーのレイアウトページが再帰的に設定されます。 ビューを表示すると、ビューコードの実行前に、\_viewstart. cshtml ファイルのコードが実行されます。 \_viewstart. cshtml コードは、そのフォルダー内のすべてのビューに適用されます。

既定では、\_viewstart. cshtml ファイルのコードは、サブフォルダー内のビューにも適用されます。 ただし、個々のサブフォルダーには、独自のバージョンの \_viewstart. cshtml ファイルを含めることができます。この場合は、ローカルバージョンが優先されます。 たとえば、HomeController のすべてのビューに共通するコードを実行するには、~/ビューの/Home フォルダーに viewstart. cshtml ファイル \_します。

### <a id="0.1__Toc274034225"></a>VBHTML Razor 構文の新しいサポート

前の ASP.NET MVC プレビューには、にC#基づく Razor 構文を使用したビューのサポートが含まれていました。 これらのビューでは、ファイル拡張子を使用します。 Razor をサポートするための進行中の作業の一部として、ASP.NET MVC 3 ベータ版では Visual Basic の Razor 構文のサポートが導入されています。これは、拡張子が vbhtml のファイルです。

VBHTML ページで Visual Basic 構文を使用する方法の概要については、次の URL にあるチュートリアルを参照してください。

[https://www.asp.net/webmatrix/tutorials/asp-net-web-pages-visual-basic](../web-pages/overview/getting-started/introducing-razor-syntax-vb.md)

### <a id="0.1__Toc274034226"></a>ValidateInputAttribute をより細かく制御する

ASP.NET MVC には、常に ValidateInputAttribute クラスが含まれています。このクラスは、コア ASP.NET request 検証インフラストラクチャを呼び出して、受信要求に悪意のある可能性のある入力が含まれていないことを確認します。 既定では、入力の検証が有効になっています。 次の例に示すように、ValidateInputAttribute 属性を使用して、要求の検証を無効にすることができます。

[!code-csharp[Main](mvc3-release-notes/samples/sample37.cs)]

ただし、多くの web アプリケーションには、HTML を許可する必要がある個々のフォームフィールドがありますが、残りのフィールドには使用できません。 ValidateInputAttribute クラスで、要求の検証に含まれていないフィールドの一覧を指定できるようになりました。

たとえば、ブログエンジンを開発している場合は、[本文] フィールドと [概要] フィールドでマークアップを許可することができます。 これらのフィールドは2つの input 要素で表され、それぞれにプロパティ名に対応する name 属性があります ("Body" と "Summary")。 これらのフィールドに対してのみ要求の検証を無効にするには、次の例に示すように、ValidateInput クラスの Exclude プロパティで名前 (コンマ区切り) を指定します。

[!code-csharp[Main](mvc3-release-notes/samples/sample38.cs)]

### <a id="0.1__Toc274034227"></a>ヘルパーは、匿名オブジェクトを使用して指定された HTML 属性名のアンダースコアをハイフンに変換します

ヘルパーメソッドでは、次の例に示すように、匿名オブジェクトを使用して属性の名前と値のペアを指定できます。

[!code-csharp[Main](mvc3-release-notes/samples/sample39.cs)]

この方法では、ASP.NET のプロパティ名にハイフンを使用することはできないため、属性名にハイフンを使用することはできません。 ただし、カスタム HTML5 属性ではハイフンが重要です。たとえば、HTML5 では "data-" プレフィックスが使用されます。

同時に、アンダースコアを HTML の属性名に使用することはできませんが、プロパティ名では有効です。 したがって、匿名オブジェクトを使用して属性を指定し、属性名にアンダースコアが含まれている場合、ヘルパーメソッドはアンダースコアをハイフンに変換します。 たとえば、次のヘルパー構文では、アンダースコアを使用します。

[!code-csharp[Main](mvc3-release-notes/samples/sample40.cs)]

前の例では、ヘルパーを実行すると、次のマークアップがレンダリングされます。

[!code-html[Main](mvc3-release-notes/samples/sample41.html)]

## <a id="0.1__Toc274034228"></a>バグの修正

EditorFor および DisplayFor テンプレートヘルパーの既定のオブジェクトテンプレートで、Displayfor. Order プロパティに指定された順序がサポートされるようになりました。 (以前のバージョンでは、注文の設定は使用されませんでした)。

クライアント検証で、検証属性が適用されているオーバーライドされたプロパティの検証がサポートされるようになりました。

JsonValueProviderFactory が既定で登録されるようになりました。

## <a id="0.1__Toc274034229"></a>重大な変更

同じ順序の値を持つ例外フィルターの実行順序が変更されました。 ASP.NET MVC 2 以前では、アクションメソッドの例外フィルターと同じ順序で、アクションメソッドの例外フィルターが実行されました。 これは通常、特定の順序の値を指定せずに例外フィルターが適用された場合に発生します。 ASP.NET MVC 3 では、最も具体的な例外ハンドラーが最初に実行されるように、この順序は逆になっています。 以前のバージョンと同様に、Order プロパティが明示的に指定されている場合、フィルターは指定された順序で実行されます。

## <a id="0.1__Toc274034230"></a>既知の問題

インストール中にライセンス条項への同意を確認するためのダイアログ ボックスで、意図したよりも小さいウィンドウにライセンス条項が表示されます。

Razor ビューには、IntelliSense のサポートや構文の強調表示がありません。 Visual Studio での Razor 構文のサポートは、今後のリリースの一部として含まれることが予想されます。

Razor ビュー (CSHTML ファイル) <a id="0.1__Toc224729061"></a> <a id="0.1__Toc238051347"></a>を編集しているときに、Visual Studio の [コントローラーへのジャンプ] メニュー項目は使用できず、コードスニペットもありません。

厳密に型指定された CSHTML ビューを指定するために @model 構文を使用する場合、型の言語固有のショートカットは認識されません。 たとえば、@model int は機能しませんが、@model Int32 が機能します。 このバグの回避策は、モデルの種類を指定するときに実際の型名を使用することです。

@model 構文を使用して、厳密に型指定された CSHTML ビュー (または厳密に型指定された VBHTML ビューを指定する @ModelType) を指定する場合、null 許容型および配列宣言はサポートされません。 たとえば、@model int?はサポートされていません。 代わりに、`@model Nullable<Int32>`を使用します。 文字列 [] @model 構文もサポートされていません。代わりに、`@model IList<string>`を使用します。

ASP.NET MVC 2 プロジェクトを ASP.NET MVC 3 にアップグレードする場合は、web.config ファイルの appSettings セクションに次の項目を追加してください。

[!code-xml[Main](mvc3-release-notes/samples/sample42.xml)]

フォーム認証によって認証されていないユーザーが常に ~/アカウントにリダイレクトされるという既知の問題があります。これは、web.config で使用されるフォーム認証設定を無視します。この回避策は、次のアプリ設定を追加することです。

[!code-xml[Main](mvc3-release-notes/samples/sample43.xml)]

## <a id="0.1__Toc274034231"></a>免責事項

© 2011 Microsoft Corporation. All rights reserved. このドキュメントは何等保障もない現状有姿のままで提供されるものです。 このドキュメントに記載されている情報と表示 (URL および他のインターネット Web サイトの参照を含む) は、将来予告なく変更されることがあります。 お客様ご自身の責任において使用してください。

このドキュメントは、Microsoft 製品の知的財産権に関する法的な権利をお客様に許諾するものではありません。 内部的な参照目的に限り、このドキュメントを複製して使用することができます。
