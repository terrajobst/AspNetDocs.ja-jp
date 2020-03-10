---
uid: whitepapers/mvc4-beta-release-notes
title: ASP.NET MVC 4 |Microsoft Docs
author: rick-anderson
description: このドキュメントでは、Visual Studio 2010 用の ASP.NET MVC 4 Beta のリリースについて説明します。
ms.author: riande
ms.date: 09/09/2011
ms.assetid: 666407bb-81de-4319-89ba-0302c382a208
msc.legacyurl: /whitepapers/mvc4-beta-release-notes
msc.type: content
ms.openlocfilehash: 17800dfe091bbb7afb25f7f41e3bd885b882edb0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78419842"
---
# <a name="aspnet-mvc-4"></a>ASP.NET MVC 4

> このドキュメントでは、Visual Studio 2010 用の ASP.NET MVC 4 Beta のリリースについて説明します。
> 
> > [!NOTE]
> > これは、最新のリリースではありません。 ASP.NET MVC 4 RC のリリースノートについては、[こちら](mvc4-release-notes.md)を参照してください。

- [インストールに関する注意事項](#_Toc303253802)
- [ドキュメント](#_Toc303253803)
- [サポート](#_Toc303253804)
- [ソフトウェア要件](#_Toc303253805)
- [ASP.NET MVC 3 プロジェクトを ASP.NET MVC 4 にアップグレードする](#_Toc303253806)
- [ASP.NET MVC 4 Beta の新機能](#_Toc303253807)

    - [ASP.NET Web API](#_Toc317096197)
    - [ASP.NET シングルページアプリケーション](#_Toc317096198)
    - [既定のプロジェクトテンプレートの機能強化](#_Toc303253808)
    - [モバイルプロジェクトテンプレート](#_Toc303253809)
    - [表示モード](#_Toc303253810)
    - [jQuery Mobile、ビュースイッチャー、およびブラウザーのオーバーライド](#_Toc303253811)
    - [Visual Studio でのコード生成のためのレシピ](#_Toc303253812)
    - [非同期コントローラーのタスクサポート](#_Toc303253813)
    - [Azure SDK](#_Toc303253814)
    - [既知の問題と重大な変更](#_Toc303253815)

<a id="_Toc303253802"></a>
## <a name="installation-notes"></a>インストールに関する注意事項

ASP.NET MVC 4 Beta for Visual Studio 2010 は、Web Platform Installer を使用して[ASP.NET mvc 4 ホームページ](../mvc/mvc4.md)からインストールできます。

ASP.NET MVC 4 Beta をインストールする前に、以前にインストールされた ASP.NET MVC 4 のプレビューをアンインストールする必要があります。

このリリースは、.NET Framework 4.5 Developer Preview と互換性がありません。 ASP.NET MVC 4 Beta をインストールする前に、.NET 4.5 Developer Preview をアンインストールする必要があります。

ASP.NET MVC 4 はインストールでき、ASP.NET MVC 3 とサイドバイサイドで実行できます。

<a id="_Toc303253803"></a>
## <a name="documentation"></a>ドキュメント

ASP.NET MVC のドキュメントについては、次の URL で MSDN Web サイトを参照してください。

[https://go.microsoft.com/fwlink/?LinkID=243043](https://go.microsoft.com/fwlink/?LinkID=243043)

ASP.NET MVC に関するチュートリアルやその他の情報については、ASP.NET web サイト ([https://www.asp.net/mvc/mvc4](../mvc/mvc4.md)) の mvc 4 ページを参照してください。

<a id="_Toc303253804"></a>
## <a name="support"></a>サポート

これはプレビューリリースであり、公式にはサポートされていません。 このリリースの使用についてご質問がある場合は、ASP.NET MVC フォーラム ([https://forums.asp.net/1146.aspx](https://forums.asp.net/1146.aspx)) に投稿してください。 ASP.NET コミュニティのメンバーは、多くの場合、非公式のサポートを提供できます。

<a id="_Toc303253805"></a>
## <a name="software-requirements"></a>ソフトウェア要件

Visual Studio の ASP.NET MVC 4 コンポーネントには、PowerShell 2.0、Visual Studio 2010 Service Pack 1、または Visual Web Developer Express 2010 Service Pack 1 が必要です。

<a id="_Toc303253806"></a>
## <a name="upgrading-an-aspnet-mvc-3-project-to-aspnet-mvc-4"></a>ASP.NET  4、ASP.NET MVC 3 プロジェクトをアップグレードします。

ASP.NET MVC 4 は、ASP.NET MVC 3 とサイドバイサイドで同じコンピューターにインストールできます。これにより、ASP.NET MVC 3 アプリケーションを ASP.NET MVC 4 にアップグレードするタイミングを柔軟に選択できます。

アップグレードする最も簡単な方法は、新しい ASP.NET MVC 4 プロジェクトを作成し、既存の MVC 3 プロジェクトのすべてのビュー、コントローラー、コード、コンテンツファイルを新しいプロジェクトにコピーしてから、新しいプロジェクトのアセンブリ参照を古いプロジェクトに一致するように更新することです。 MVC 3 プロジェクトの web.config ファイルに変更を加えた場合は、それらの変更を MVC 4 プロジェクトの web.config ファイルにマージする必要もあります。

既存の ASP.NET MVC 3 アプリケーションをバージョン4に手動でアップグレードするには、次の手順を実行します。

1. プロジェクトのすべての web.config ファイル (プロジェクトのルートに1つ、[Views] フォルダーに1つ、プロジェクト内の各領域の [Views] フォルダーに1つ) で、次のテキストのすべてのインスタンスを置き換えます。

    [!code-console[Main](mvc4-beta-release-notes/samples/sample1.cmd)]

    には、次の対応するテキストがあります。

    [!code-console[Main](mvc4-beta-release-notes/samples/sample2.cmd)]
2. ルートの Web.config ファイルで、Web*ページ: Version*要素を "2.0.0.0" に更新し、値 "true" を持つ新しい*PreserveLoginUrl*キーを追加します。

    [!code-xml[Main](mvc4-beta-release-notes/samples/sample3.xml)]
3. ソリューションエクスプローラーで、(バージョン3の DLL を指す) *system.web. Mvc*への参照を削除します。 次に、4.0.0.0 (v) に*参照を追加*します。 特に、アセンブリ参照を更新するには、次の変更を行います。 これらについて詳しく説明します。

    1. ソリューションエクスプローラーで、次のアセンブリへの参照を削除します。 

        - *System.web. Mvc*(v 3.0.0.0)
        - *System.web. Web ページ*(1.0.0.0)
        - *System.web. Razor*(v 1.0.0.0)
        - *System.web. Web ページ*(1.0.0.0)
        - *System.web. Web ページ*(v 1.0.0.0)
    2. 次のアセンブリへの参照を追加します。 

        - *System.web. Mvc*(v 4.0.0.0)
        - *System.web. Web ページ*(v 2.0.0.0)
        - *System.web. Razor*(v 2.0.0.0)
        - *System.web. Web ページ. 配置*(v 2.0.0.0)
        - *System.web. Web ページ*(v 2.0.0.0)
4. ソリューションエクスプローラーで、プロジェクト名を右クリックし、[プロジェクトのアンロード] を選択します。 次に、名前をもう一度右クリックし、[ *ProjectName*の編集] を選択します。
5. *Projecttypeguids*要素を見つけ、{E53F8FEA-EAE0-44A6-8774-FFD645390401} を {E3E379DF-F4C6-4180-9B81-6769533ABE47} に置き換えます。
6. 変更を保存し、編集中のプロジェクト (.csproj) ファイルを閉じて、プロジェクトを右クリックし、[プロジェクトの再読み込み] を選択します。
7. 以前のバージョンの ASP.NET MVC を使用してコンパイルされたサードパーティ製のライブラリをプロジェクトが参照する場合は、ルートの Web.config ファイルを開き、*構成*セクションの下に次の3つの*bindingRedirect*要素を追加します。 

    [!code-xml[Main](mvc4-beta-release-notes/samples/sample4.xml)]

<a id="_Toc303253807"></a>
## <a name="new-features-in-aspnet-mvc-4-beta"></a>ASP.NET MVC 4 Beta の新機能

このセクションでは、ASP.NET MVC 4 ベータリリースで導入された機能について説明します。

<a id="_Toc317096197"></a>
### <a name="aspnet-web-api"></a>ASP.NET Web API

ASP.NET MVC 4 には、ブラウザーやモバイルデバイスを含む広範なクライアントに接続できる HTTP サービスを作成するための新しいフレームワークである ASP.NET Web API が含まれるようになりました。 ASP.NET Web API は、RESTful サービスを構築するための最適なプラットフォームでもあります。

ASP.NET Web API には、次の機能のサポートが含まれています。

- **最新の HTTP プログラミングモデル:** 新しい厳密に型指定された HTTP オブジェクトモデルを使用して、Web Api の HTTP 要求と応答に直接アクセスして操作します。 新しい HttpClient 型を使用して、クライアントで同じプログラミングモデルと HTTP パイプラインを対称的に使用できます。
- **ルートの完全なサポート**: web api では、ルートパラメーターや制約など、常に web スタックの一部であるルート機能の完全なセットがサポートされるようになりました。 また、アクションへのマッピングでは規約が完全にサポートされているため、[HttpPost] などの属性をクラスやメソッドに適用する必要がなくなりました。
- **コンテンツネゴシエーション**: クライアントとサーバーは連携して、API から返されるデータの適切な形式を判断できます。 XML、JSON、およびフォームの URL エンコード形式の既定のサポートが用意されています。独自のフォーマッタを追加することによって、このサポートを拡張することも、既定のコンテンツネゴシエーション戦略を置き換えることもできます。
- **モデルのバインドと検証:** モデルバインダーを使用すると、HTTP 要求のさまざまな部分からデータを抽出し、それらのメッセージ部分を .NET オブジェクトに変換して、Web API アクションで使用できるようにすることができます。
- **フィルター:** Web Api では、[承認] 属性などの既知のフィルターを含むフィルターがサポートされるようになりました。 アクション、承認、および例外処理のために、独自のフィルターを作成してプラグインすることができます。
- **クエリの構成:** IQueryable&lt;T&gt;を返すだけで、Web API は OData URL 規則を使用したクエリをサポートします。
- **HTTP 詳細のテストの容易性の向上:** 静的コンテキストオブジェクトで HTTP の詳細を設定するのではなく、Web API アクションを HttpRequestMessage および HttpResponseMessage のインスタンスと共に使用できるようになりました。 これらのオブジェクトのジェネリックバージョンは、HTTP 型に加えてカスタム型を操作できるようにするためにも存在します。
- **DependencyResolver を使用したコントロールの反転 (IoC) の向上:** Web API では、MVC の依存関係競合回避モジュールによって実装されたサービスロケーターパターンを使用して、さまざまな機能のインスタンスを取得するようになりました。
- **コードベースの構成:** Web API の構成はコードを使用してのみ実行され、構成ファイルはクリーンなままになります。
- **自己ホスト:** Web api は、IIS だけでなく、独自のプロセスでホストすることもできます。また、Web API のルートやその他の機能を最大限に活用できます。

の詳細については ASP.NET Web API [https://www.asp.net/web-api](../web-api/index.md)を参照してください。

<a id="_Toc317096198"></a>
### <a name="aspnet-single-page-application"></a>ASP.NET シングルページアプリケーション

ASP.NET MVC 4 には、JavaScript と Web Api を使用して、クライアント側の重要な対話機能を備えたシングルページアプリケーションを構築するための初期プレビューが含まれるようになりました。 このサポートには次のものが含まれます。

- キャッシュされたデータとのより高度なローカル操作のための JavaScript ライブラリのセット
- 作業単位と DAL のサポートのための追加の Web API コンポーネント
- すぐに作業を開始するためのスキャフォールディングを含む MVC プロジェクトテンプレート

ASP.NET MVC 4 のシングルページアプリケーションサポートの詳細については、 [https://www.asp.net/single-page-application](../single-page-application/index.md)を参照してください。

<a id="_Toc303253808"></a>
### <a name="enhancements-to-default-project-templates"></a>既定のプロジェクトテンプレートの機能強化

新しい ASP.NET MVC 4 プロジェクトを作成するために使用されるテンプレートは、最新の web サイトを作成するように更新されました。

![](mvc4-beta-release-notes/_static/image1.png)

表面的な機能強化に加えて、新しいテンプレートの機能が強化されています。 このテンプレートは、デスクトップブラウザーとモバイルブラウザーの両方で適切に表示されるように、アダプティブレンダリングと呼ばれる手法を採用しています。カスタマイズは必要ありません。

![](mvc4-beta-release-notes/_static/image2.png)

アダプティブレンダリングが動作していることを確認するには、モバイルエミュレーターを使用するか、デスクトップブラウザーウィンドウのサイズを小さくしてみてください。 ブラウザーウィンドウのサイズが十分に小さくなると、ページのレイアウトが変わります。

既定のプロジェクトテンプレートのもう1つの拡張機能は、JavaScript を使用して豊富な UI を提供することです。 テンプレートで使用されるログインリンクとレジスタリンクは、jQuery UI ダイアログを使用してリッチログイン画面を表示する方法の例です。

![](mvc4-beta-release-notes/_static/image3.png)

<a id="_Toc303253809"></a>
### <a name="mobile-project-template"></a>モバイルプロジェクトテンプレート

新しいプロジェクトを開始していて、モバイルおよびタブレットのブラウザー専用のサイトを作成する場合は、[新しいモバイルアプリケーション] プロジェクトテンプレートを使用できます。 これは、タッチに最適化された UI を構築するためのオープンソースライブラリである jQuery Mobile に基づいています。

![](mvc4-beta-release-notes/_static/image4.png)

このテンプレートには、インターネットアプリケーションテンプレートと同じアプリケーション構造が含まれています (コントローラーコードは実質的に同じです) が、jQuery Mobile を使用してスタイルを適用し、タッチベースのモバイルデバイスで適切に動作します。 モバイル UI を構造化およびスタイルする方法の詳細については、 [JQuery mobile プロジェクトの web サイト](http://jquerymobile.com/)を参照してください。

モバイル最適化されたビューを追加するデスクトップ指向サイトが既にある場合、またはデスクトップとモバイルのブラウザーに異なるスタイルのビューを提供する1つのサイトを作成する場合は、新しい表示モード機能を使用できます。 (次のセクションを参照してください)。

<a id="_Toc303253810"></a>
### <a name="display-modes"></a>表示モード

新しい表示モード機能を使用すると、アプリケーションは、要求を行っているブラウザーに応じて、ビューを選択できます。 たとえば、デスクトップブラウザーがホームページを要求した場合、アプリケーションは Views\Home\Index.cshtml テンプレートを使用することがあります。 モバイルブラウザーがホームページを要求した場合、アプリケーションは Views\Home\Index.mobile.cshtml テンプレートを返すことがあります。

また、レイアウトとパーシャルは、特定のブラウザーの種類に対してオーバーライドすることもできます。 次に例を示します。

- Views\Shared フォルダーに \_Layout と \_Layout の両方のテンプレートが含まれている場合、既定では、アプリケーションは、モバイルブラウザーからの要求中に \_を使用し、他の要求時には \_を使用します。
- フォルダーに \_MyPartial. cshtml と \_MyPartial.\_の両方が含まれている場合、命令 @Html.Partial("MyPartial") は、モバイルブラウザーからの要求時に MyPartial を表示し、他の要求では MyPartial. cshtml を \_します。\_

他のデバイスの特定のビュー、レイアウト、または部分ビューを作成する場合は、新しい*Defaultdisplaymode*インスタンスを登録して、要求が特定の条件を満たすときに検索する名前を指定できます。 たとえば、次のコードを*アプリケーション\_* の global.asax ファイルに追加して、Apple iPhone ブラウザーが要求を行うときに適用される表示モードとして文字列 "iPhone" を登録することができます。

[!code-csharp[Main](mvc4-beta-release-notes/samples/sample5.cs)]

このコードを実行すると、Apple iPhone ブラウザーが要求を行うときに、アプリケーションで Views\Shared\\_Layout (存在する場合) が使用されます。

<a id="_Toc303253811"></a>
### <a name="jquery-mobile-the-view-switcher-and-browser-overriding"></a>jQuery Mobile、ビュースイッチャー、およびブラウザーのオーバーライド

jQuery Mobile は、タッチに最適化された web UI を構築するためのオープンソースライブラリです。 ASP.NET MVC 4 アプリケーションで jQuery Mobile を使用する場合は、作業の開始に役立つ NuGet パッケージをダウンロードしてインストールすることができます。 Visual Studio パッケージマネージャーコンソールからインストールするには、次のコマンドを入力します。

[!code-powershell[Main](mvc4-beta-release-notes/samples/sample6.ps1)]

これにより、jQuery Mobile と、次のようなヘルパーファイルがインストールされます。

- Views/Shared/\_Layout。これは jQuery モバイルベースのレイアウトです。
- Views/Shared/\_ViewSwitcher. cshtml partial ビューと ViewSwitcherController.cs controller で構成されるビュースイッチャーコンポーネント。

パッケージをインストールした後、モバイルブラウザーを使用してアプリケーションを実行します (または、Firefox[ユーザーエージェントスイッチャー](http://chrispederick.com/work/user-agent-switcher/)アドオンなどの同等のものを使用します)。 JQuery Mobile はレイアウトとスタイル設定を処理するため、ページの外観が大きく異なることがわかります。 この機能を利用するには、次の操作を行います。

- 前の「[表示モード](#_Toc303253810)」で説明されているように、モバイル固有のビューの上書きを作成します (たとえば、モバイルブラウザーの Views\Home\Index.cshtml を上書きするように Views\Home\Index.mobile.cshtml を作成します)。
- タッチに最適化された UI 要素をモバイルビューに追加する方法の詳細については、 [JQuery Mobile のドキュメント](http://jquerymobile.com/)を参照してください。

モバイルで最適化された web ページの規則としては、ユーザーがデスクトップバージョンのページに切り替えることができるように、デスクトップビューや完全サイトモードなどのテキストを持つリンクを追加します。 JQuery パッケージには、この目的のためのサンプルのビュースイッチャーコンポーネントが含まれています。 これは、既定の Views\Shared\\_Layout で使用されます。これは、ページが表示されたときの次のようになります。

![](mvc4-beta-release-notes/_static/image5.png)

ビジターがリンクをクリックすると、同じページのデスクトップバージョンに切り替わります。

既定では、デスクトップレイアウトにはビュースイッチャーが含まれないため、訪問者はモバイルモードに戻ることができません。 これを有効にするには、 *\_ViewSwitcher*への次の参照を、 *&lt;body&gt;* 要素の内側にあるデスクトップレイアウトに追加します。

[!code-cshtml[Main](mvc4-beta-release-notes/samples/sample7.cshtml)]

ビュースイッチャーは、ブラウザーのオーバーライドと呼ばれる新しい機能を使用します。 この機能を使用すると、アプリケーションは、実際のものとは異なるブラウザー (ユーザーエージェント) からの要求を処理できます。 次の表に、ブラウザーがオーバーライドするメソッドを示します。

| `HttpContext.SetOverriddenBrowser(userAgentString)` | 指定されたユーザー エージェントを使用して、要求の実際のユーザー エージェント値をオーバーライドします。 |
| --- | --- |
| `HttpContext.GetOverriddenUserAgent()` | 要求のユーザーエージェントのオーバーライド値、またはオーバーライドが指定されていない場合は実際のユーザーエージェント文字列を返します。 |
| `HttpContext.GetOverriddenBrowser()` | 要求に対して現在設定されているユーザーエージェントに対応する*HttpBrowserCapabilitiesBase*インスタンスを返します (実際またはオーバーライドされます)。 この値を使用して、 *IsMobileDevice*などのプロパティを取得できます。 |
| `HttpContext.ClearOverriddenBrowser()` | 現在の要求でオーバーライドされたユーザー エージェントがあれば削除します。 |

ブラウザーのオーバーライドは ASP.NET MVC 4 の中核機能であり、jQuery パッケージをインストールしない場合でも使用できます。 ただし、ビュー、レイアウト、および部分ビューの選択にのみ影響します *。 Browser*オブジェクトに依存する他の ASP.NET 機能には影響しません。

既定では、ユーザーエージェントのオーバーライドは cookie を使用して格納されます。 (たとえば、データベースで) 上書きを別の場所に保存する場合は、既定のプロバイダー (*Browseroverridestores. Current*) を置き換えることができます。 このプロバイダーのドキュメントは、ASP.NET MVC の今後のリリースに付属しています。

<a id="_Toc303253812"></a>
### <a name="recipes-for-code-generation-in-visual-studio"></a>Visual Studio でのコード生成のためのレシピ

新しいレシピ機能により、Visual Studio は、NuGet を使用してインストールできるパッケージに基づいて、ソリューション固有のコードを生成できます。 レシピフレームワークを使用すると、開発者はコード生成プラグインを簡単に記述できるようになります。このプラグインを使用すると、追加領域、コントローラーの追加、ビューの追加用の組み込みのコードジェネレーターを置き換えることができます。 レシピは NuGet パッケージとして配置されるため、簡単にソース管理にチェックインし、プロジェクトのすべての開発者と共有することができます。 また、ソリューションごとに使用することもできます。

<a id="_Toc303253813"></a>
### <a name="task-support-for-asynchronous-controllers"></a>非同期コントローラーのタスクサポート

*ActionResult&gt;&lt;* *型の*オブジェクトを返す単一のメソッドとして、非同期アクションメソッドを記述できるようになりました。

たとえば、Visual C# 5 (または[Async CTP](https://msdn.microsoft.com/vstudio/async.aspx)を使用) を使用している場合は、次のような非同期アクションメソッドを作成できます。

[!code-csharp[Main](mvc4-beta-release-notes/samples/sample8.cs)]

前のアクションメソッドでは、 *NewsService async*と*sportsService*の呼び出しは非同期に呼び出され、スレッドプールからのスレッドはブロックされません。

*タスク*インスタンスを返す非同期アクションメソッドは、タイムアウトをサポートすることもできます。 アクションメソッドをキャンセル可能なにするには、アクションメソッドシグネチャに*CancellationToken*型のパラメーターを追加します。 次の例は、タイムアウトが2500ミリ秒で、タイムアウトが発生した場合に*TimedOut*ビューをクライアントに表示する非同期アクションメソッドを示しています。

[!code-csharp[Main](mvc4-beta-release-notes/samples/sample9.cs)]

<a id="_Toc303253814"></a>
### <a name="azure-sdk"></a>Azure SDK

ASP.NET MVC 4 Beta では、Windows Azure SDK の9月 2011 1.5 リリースがサポートされています。

<a id="_Toc303253815"></a>
## <a name="known-issues-and-breaking-changes"></a>既知の問題と重大な変更

- **ASP.NET MVC 4 Beta をインストールすると、Visual Studio 2010 Service Pack 1 の cshtml/vbhtml エディターの cshtml/VBHTML エディターが、cshtml または VBHTML ファイル内にスニペットまたは JavaScript を入力した後、長い時間一時停止する場合があります。** これは、作成されたばかりでまだコンパイルされていない ASP.NET MVC 4 アプリケーションでのみ発生します。

    この回避策は、プロジェクトをコンパイルして bin フォルダー内のアセンブリを取得することです。 Bin フォルダーからアセンブリを削除するプロジェクトをクリーニングすると、エディターの問題が返されます。

    これは、次のリリースで修正される予定です。
- **C#Visual Studio 11 Beta のプロジェクトテンプレートに、Global.asax.cs に正しくない接続文字列が含まれています。** Visual Studio 11 Beta で作成されたプロジェクトの Application\_Start メソッドに指定された既定の接続には、エスケープされていない円記号 (\) 文字を含む LocalDB 接続文字列が含まれています。 この結果、SqlException を生成する DbContext Entity Framework にアクセスしようとすると接続エラーが発生します。

    この問題を解決するには、次のように読み取られるように、App\_Start メソッドで円記号をエスケープします。

    [!code-csharp[Main](mvc4-beta-release-notes/samples/sample10.cs)]
- **.Net 4.5 を対象とする ASP.NET MVC 4 アプリケーションは、.NET 4.0 で実行されるときに FileLoadException アセンブリにアクセスしようとすると、をスローします。** .NET 4.5 で作成された ASP.NET MVC 4 アプリケーションには、バインドリダイレクトが含まれています。これにより、"ファイルまたはアセンブリ ' FileLoadException ' またはその依存関係の1つを読み込めませんでした。" という状態になります。 .NET 4.0 がインストールされているシステムでアプリケーションを実行する場合。 この問題を解決するには、web.config から次のバインドリダイレクトを削除します。

    [!code-xml[Main](mvc4-beta-release-notes/samples/sample11.xml)]

    変更した web.config のアセンブリバインド要素は、次のように表示されます。

    [!code-xml[Main](mvc4-beta-release-notes/samples/sample12.xml)]
- <strong>Visual Basic プロジェクトの "コントローラーの追加" 項目テンプレートは、領域内から呼び出されたときに正しくない名前空間を生成し</strong><strong>ます。</strong> Visual Basic を使用する ASP.NET MVC プロジェクトの領域にコントローラーを追加すると、項目テンプレートによって、コントローラーに間違った名前空間が挿入されます。 コントローラーのアクションに移動すると、"ファイルが見つかりません" というエラーが発生します。  
  
  生成された名前空間は、ルート名前空間の後にあるすべてのものを省略します。 たとえば、生成される名前空間は*RootNamespace*ですが、 *RootNamespace*である必要があります。
- **Razor ビューエンジンでの重大な変更。** Razor パーサーの書き換えの一環として、次の型が*system.web*から削除されました。 

    - *ModelSpan*
    - *MvcVBRazorCodeGenerator*
    - *MvcCSharpRazorCodeGenerator*
    - *MvcVBRazorCodeParser*

  次のメソッドも削除されました。 

    - *MvcCSharpRazorCodeParser (System.web..... パーサー. CodeBlockInfo)*
    - *MvcWebPageRazorHost (RazorCodeGenerator) のようになります。*
    - *MvcVBRazorCodeParser (System.web..... パーサー. CodeBlockInfo)*
- **ASP.NET MVC 4 アプリの/bin ディレクトリに WebData が含まれている場合、フォーム認証の URL が引き継がれます。** WebData アセンブリをアプリケーションに追加する ([配置可能な依存関係の追加] ダイアログボックスを使用して [Razor 構文を使用する] を ASP.NET Web ページ選択するなど) と、既定の ASP.NET MVC アカウントコントローラーによって想定されているように、/account/ログインではなく、認証ログインリダイレクトがオーバーライドされます。 この動作を回避し、web.config の認証セクションに既に指定されている URL を使用するには、PreserveLoginUrl という名前の appSetting を追加し、それを true に設定します。 

    [!code-xml[Main](mvc4-beta-release-notes/samples/sample13.xml)]
- **Visual Studio 2010 と Visual Web Developer 2010 をサイドバイサイドでインストールするために ASP.NET MVC 4 をインストールしようとすると、NuGet パッケージマネージャーのインストールが失敗します。** Visual Studio 2010 と Visual Web Developer 2010 を ASP.NET MVC 4 とサイドバイサイドで実行するには、Visual Studio の両方のバージョンが既にインストールされていると、ASP.NET MVC 4 をインストールする必要があります。
- **前提条件が既にアンインストールされている場合、ASP.NET MVC 4 のアンインストールは失敗します。** ASP.NET MVC 4you 正常にアンインストールするには、Visual Studio をアンインストールする前に ASP.NET MVC 4 をアンインストールする必要があります。
- **既定の Web API プロジェクトを実行すると、存在しない RegisterApis メソッドを使用してルートを追加するようにユーザーに誤って指示する命令が示されます。** ルートは、ASP.NET route テーブルを使用して RegisterRoutes メソッドに追加する必要があります。
- **ASP.NET MVC 4 Beta ASP.NET をインストールすると、MVC 3 RTM アプリケーションが中断します。** RTM リリース (ASP.NET MVC 3 Tools Update リリースではない) で作成された ASP.NET MVC 3 アプリケーションでは、ASP.NET MVC 4 Beta とサイドバイサイドで動作するために次の変更が必要です。 これらの更新を行わずにプロジェクトをビルドすると、コンパイルエラーになります。 

    **必要な更新プログラム**

  1. ルートの Web.config ファイルで、新しい *&lt;appSettings&gt;* エントリを追加します。このキー*ページ*には、バージョンと値*1.0.0.0*があります。

      [!code-xml[Main](mvc4-beta-release-notes/samples/sample14.xml)]
  2. ソリューションエクスプローラーで、プロジェクト名を右クリックし、[プロジェクトのアンロード] を選択します。 次に、名前をもう一度右クリックし、[ *ProjectName*の編集] を選択します。
  3. 次のアセンブリ参照を見つけます。 

      [!code-xml[Main](mvc4-beta-release-notes/samples/sample15.xml)]

      次のように置き換えます。

      [!code-xml[Main](mvc4-beta-release-notes/samples/sample16.xml)]
  4. 変更を保存し、編集中のプロジェクト (.csproj) ファイルを閉じてから、プロジェクトを右クリックして [再読み込み] を選択します。
