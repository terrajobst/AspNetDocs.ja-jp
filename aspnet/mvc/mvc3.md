---
uid: mvc/mvc3
title: ASP.NET MVC 3
author: rick-anderson
description: (2011 年4月の更新プログラムを含む)ASP.NET MVC 3 は、適切に確立された設計パターンを使用して、スケーラブルで標準ベースの web アプリケーションを構築するためのフレームワークです...
ms.author: riande
ms.date: 10/05/2010
ms.assetid: dddc8812-a0bc-49f9-aafb-caf2064c2b8c
msc.legacyurl: /mvc/mvc3
msc.type: content
ms.openlocfilehash: 421a06c89d4dbcb05d4080033813cc6558b7c698
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74586752"
---
# <a name="aspnet-mvc-3"></a>ASP.NET MVC 3

> *(2011 年4月の更新プログラムを含む)*
> 
> ASP.NET MVC 3 は、適切に確立された設計パターンと、ASP.NET と .NET Framework の機能を使用して、スケーラブルで標準ベースの web アプリケーションを構築するためのフレームワークです。
> 
> ASP.NET MVC 2 とサイドバイサイドでインストールされるため、すぐに使用を開始できます。
> 
> インストーラーは[こちら](https://go.microsoft.com/fwlink/?LinkID=208140)からダウンロードしてください

## <a name="top-features"></a>上位の機能

- NuGet を使用して拡張可能な統合スキャフォールディングシステム
- HTML 5 が有効なプロジェクトテンプレート
- 新しい Razor ビューエンジンを含む表現力のあるビュー
- 依存関係の挿入とグローバルアクションフィルターを使用した強力なフック
- 控えめな JavaScript、jQuery 検証、および JSON バインドを使用した豊富な JavaScript のサポート
- *以下の全機能リストをお読み[ください](#overview)。*

## <a name="top-links"></a>上位のリンク

ASP.NET MVC 3 の新機能

- Phil Haack: [ASP.NET MVC 3 がリリース](http://haacked.com/archive/2011/01/13/aspnetmvc3-released.aspx)されました
- Scott マン Selman: [ASP.NET MVC3、WebMatrix、NuGet、IIS Express および Orchard がリリースされました-Microsoft 1 月の Web リリース (コンテキスト)](http://www.hanselman.com/blog/ASPNETMVC3WebMatrixNuGetIISExpressAndOrchardReleasedTheMicrosoftJanuaryWebReleaseInContext.aspx)
- Scott Guthrie: [ASP.NET MVC 3、IIS Express、SQL CE 4、Web Farm Framework、Orchard、WebMatrix のリリース発表](https://weblogs.asp.net/scottgu/archive/2011/01/13/announcing-release-of-asp-net-mvc-3-iis-express-sql-ce-4-web-farm-framework-orchard-webmatrix.aspx)
- [ASP.NET MVC 3 のリリースノート](../whitepapers/mvc3-release-notes.md)

インストールとヘルプ

- Web Platform Installer を使用して ASP.NET MVC 3 をインストールする[(推奨)](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MVC3)
- [インストーラー実行可能ファイル](https://go.microsoft.com/fwlink/?LinkID=208140)を使用して ASP.NET MVC 3 をインストールする
- [ASP.NET MVC 3 For Visual Studio 11 Developer Preview の](https://go.microsoft.com/fwlink/?LinkID=208140)インストール
- [ASP.NET MVC 3 のチュートリアルを](overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)読む
- [フォーラム](https://forums.asp.net/1146.aspx)のヘルプを参照し、ASP.NET MVC 3 について話し合う

<a id="overview"></a>
## <a name="aspnet-mvc-3-overview"></a>ASP.NET MVC 3 Overview (ASP.NET MVC 3 の概要)

ASP.NET MVC 3 は、ASP.NET MVC 1 および2上に構築されており、コードを簡略化し、より高度な拡張性を実現する優れた機能を追加しています。 このトピックでは、このリリースに含まれる新機能の多くの概要について、次のセクションで説明します。

- [MvcScaffold 統合を使用した拡張可能なスキャフォールディング](#BM_MvcScaffolding)
- [HTML 5 が有効なプロジェクトテンプレート](#BM_HTML5)
- [Razor ビューエンジン](#BM_TheRazorViewEngine)
- [複数のビューエンジンのサポート](#BM_Support_for_Multiple_View_Engines)
- [コントローラーの機能強化](#BM_Controller_Improvements)
- [JavaScript と Ajax](#BM_JavaScript_and_Ajax_Improvements)
- [モデル検証の機能強化](#BM_Model_Validation_Improvements)
- [依存関係の挿入の機能強化](#BM_Dependency_Injection_Improvements)
- [その他の新機能](#BM_Other_New_Features)

<a id="BM_MvcScaffolding"></a>

## <a name="extensible-scaffolding-with-mvcscaffold-integration"></a>MvcScaffold 統合を使用した拡張可能なスキャフォールディング

新しいスキャフォールディングシステムを使用すると、フレームワークを初めて使用する場合に、より簡単に選択して使い始めることができます。また、経験があり、実行していることがわかっている場合には、一般的な開発タスクを自動化することができます。

これは、 **Mvcscaffolding**と呼ばれる新しい NuGet*スキャフォールディング*パッケージによってサポートされています。 "スキャフォールディング" という用語は、多くのソフトウェアテクノロジで、"編集とカスタマイズが可能なソフトウェアの基本的な概要をすばやく生成する" という意味で使用されています。 ASP.NET MVC 用に作成しているスキャフォールディングパッケージは、次のいくつかのシナリオで非常に役立ちます。

- **ASP.NET MVC を初めて学習する場合**は、便利で実用的なコードを簡単に取得できるので、必要に応じて編集し、調整することができます。 空のページを見て、どこから始めればよいかわからないトラウマからお客様を節約できます。
- **ASP.NET MVC がよくわかっていて**、オブジェクトリレーショナルマッパー、ビューエンジン、テストライブラリなどの新しいアドオンテクノロジを調査している場合は、そのテクノロジの作成者がスキャフォールディングパッケージも作成している可能性があるためです。
- テストフィクスチャや配置スクリプトなど、必要なものを出力するカスタムスキャフォールダーを作成できるため、**同様のクラスまたは何らかのファイルを繰り返し作成する作業がある場合**。 チーム内のすべてのユーザーがカスタムスキャフォールダーを使用することもできます。

MvcScaffolding のその他の機能は次のとおりです。

- と VB C#プロジェクトのサポート
- Razor ビューエンジンと ASPX ビューエンジンのサポート
- ASP.NET MVC 領域へのスキャフォールディング、およびカスタムビューレイアウト/マスターの使用をサポートします
- T4 テンプレートを編集することで、出力を簡単にカスタマイズできます。
- カスタム PowerShell ロジックとカスタム T4 テンプレートを使用して、まったく新しいスキャフォールダーを追加できます。 これら (および指定したカスタムパラメーター) は、コンソールのタブ補完の一覧に自動的に表示されます。
- さまざまなテクノロジの追加のスキャフォールダーを含む NuGet パッケージを取得できます (たとえば、LINQ to SQL について概念実証があります)。また、それらを組み合わせて一致させることができます。

ASP.NET MVC 3 Tools 更新プログラムには、次のような、このスキャフォールディングシステムに対する Visual Studio の優れたサポートが含まれています。

- [コントローラーの追加] ダイアログで、コントローラーアクションと対応するビューの作成、読み取り、更新、および削除の完全な自動スキャフォールディングがサポートされるようになりました。 既定では、このスキャフォールディングは EF Code First を使用してデータアクセスコードをします。
- [コントローラーの追加] ダイアログは、 *Mvcscaffolding*などの NuGet パッケージを使用した*拡張可能なスキャフォールディング*をサポートします。 これにより、カスタムスキャフォールディングをダイアログにプラグインすることができます。これにより、NHibernate などの他のデータアクセステクノロジや、を使用している JET でも、スキャフォールディングを作成できます。

ASP.NET MVC 3 のスキャフォールディングの詳細については、次のリソースを参照してください。

- 上田 Sanderson の投稿シリーズ (次を含む) 

    1. [概要: MvcScaffolding パッケージを使用して ASP.NET MVC 3 プロジェクトをスキャフォールディングする](http://blog.stevensanderson.com/2011/01/13/scaffold-your-aspnet-mvc-3-project-with-the-mvcscaffolding-package/)
    2. [標準の使用法: 一般的なユースケースとオプション](http://blog.stevensanderson.com/2011/01/13/mvcscaffolding-standard-usage/)
    3. [一対多のリレーションシップ](http://blog.stevensanderson.com/2011/01/28/mvcscaffolding-one-to-many-relationships/)
    4. [スキャフォールディングアクションと単体テスト](http://blog.stevensanderson.com/2011/03/28/scaffolding-actions-and-unit-tests-with-mvcscaffolding/)
    5. [T4 テンプレートのオーバーライド](http://blog.stevensanderson.com/2011/04/06/mvcscaffolding-overriding-the-t4-templates/)
    6. [この投稿: カスタムスキャフォールダーの作成](http://blog.stevensanderson.com/2011/04/07/mvcscaffolding-creating-custom-scaffolders/)
- 私の PDC 2010 セッションからの Scott マン Selman の投稿[Microsoft "名前のない Web のパッケージ" でブログを作成する](http://www.hanselman.com/blog/PDC10BuildingABlogWithMicrosoftUnnamedPackageOfWebLove.aspx)
- [MVC 3 リリースノート](../whitepapers/mvc3-release-notes.md)

<a id="BM_HTML5"></a>

## <a name="html-5-project-templates"></a>HTML 5 プロジェクトテンプレート

[新しいプロジェクト] ダイアログには、[HTML 5 バージョンのプロジェクトテンプレートを有効にする] チェックボックスがあります。 これらのテンプレートは、Modernizr 1.7 を利用して、下位レベルのブラウザーで HTML 5 と CSS 3 の互換性をサポートします。

<a id="BM_TheRazorViewEngine"></a>

## <a name="the-razor-view-engine"></a>Razor ビューエンジン

ASP.NET MVC 3 には Razor という名前の新しいビューエンジンが付属しており、次のような利点があります。

- Razor 構文はクリーンで簡潔で、キーストロークの最小数が必要です。
- Razor は、や Visual Basic のようなC#既存の言語に基づいているため、簡単に学ぶことができます。
- Visual Studio には、Razor 構文用の IntelliSense とコードの色付けが含まれています。
- Razor ビューは、アプリケーションを実行したり、web サーバーを起動したりせずに、単体テストを行うことができます。

新しい Razor 機能には、次のようなものがあります。

- ビューに渡される型を指定するための `@model` 構文。
- `@* *@` コメントの構文。
- サイト全体に対して1回だけ既定値 (`layoutpage`など) を指定する機能。
- HTML エンコードせずにテキストを表示するための `Html.Raw` メソッド。
- 複数のビュー間でのコードの共有のサポート ( *\_viewstart. cshtml*または *\_viewstart. vbhtml*ファイル)。

Razor には、次のような新しい HTML ヘルパーも含まれています。

- `Chart`. ASP.NET 4 のグラフコントロールと同じ機能を提供するグラフを表示します。
- `WebGrid`. ページングと並べ替えの機能を備えたデータグリッドをレンダリングします。
- `Crypto`. ハッシュアルゴリズムを使用して、適切なソルトおよびハッシュされたパスワードを作成します。
- `WebImage`. イメージをレンダリングします。
- `WebMail`. 電子メールを送信します。

Razor の詳細については、次のリソースを参照してください。

- [Razor の概要に関する Scott Guthrie のブログ投稿](https://weblogs.asp.net/scottgu/archive/2010/07/02/introducing-razor.aspx)
- [@model キーワードの概要に関する Scott Guthrie のブログ投稿](https://weblogs.asp.net/scottgu/archive/2010/10/19/asp-net-mvc-3-new-model-directive-support-in-razor.aspx)
- [Razor レイアウトの概要に関する Scott Guthrie のブログ投稿](https://weblogs.asp.net/scottgu/archive/2010/10/22/asp-net-mvc-3-layouts.aspx)
- [Razor API クイックリファレンス](../web-pages/overview/api-reference/asp-net-web-pages-api-reference.md)
- [MVC 3 リリースノート](../whitepapers/mvc3-release-notes.md)

<a id="BM_Support_for_Multiple_View_Engines"></a>

## <a name="support-for-multiple-view-engines"></a>複数のビューエンジンのサポート

ASP.NET MVC 3 の **[ビューの追加]** ダイアログボックスを使用すると、操作するビューエンジンを選択できます。また、 **[新しいプロジェクト]** ダイアログボックスでは、プロジェクトの既定のビューエンジンを指定できます。 Web フォームビューエンジン (ASPX)、Razor、または[Spark](http://sparkviewengine.com/)、 [NHaml](https://code.google.com/p/nhaml/)、 [NDjango](http://ndjango.org/)などのオープンソースビューエンジンを選択できます。

<a id="BM_Controller_Improvements"></a>

## <a name="controller-improvements"></a>コントローラーの機能強化

### <a name="global-action-filters"></a>グローバルアクションフィルター

アクションメソッドが実行される前、またはアクションメソッドの実行後にロジックを実行することが必要になる場合があります。 これをサポートするために、ASP.NET MVC 2 ではアクションフィルターが提供されています。 アクションフィルターは、特定のコントローラーアクションメソッドにアクション前の動作とアクション後の動作を追加するための宣言的な手段を提供するカスタム属性です。 ただし、場合によっては、すべてのアクションメソッドに適用されるアクション前またはアクション後の動作を指定する必要があります。 MVC 3 では、グローバルフィルターを `GlobalFilters` コレクションに追加することによって指定できます。 グローバルアクションフィルターの詳細については、次のリソースを参照してください。

- [MVC 3 Preview の Scott Guthrie のブログ](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx)
- [ASP.NET MVC でのフィルター処理](https://msdn.microsoft.com/library/gg416513(VS.98).aspx)

### <a name="new-viewbag-property"></a>新しい "ViewBag" プロパティ

MVC 2 コントローラーは、遅延バインディングされたディクショナリ API を使用してビューテンプレートにデータを渡すことができる `ViewData` プロパティをサポートしています。 MVC 3 では、同じ目的を達成するために、`ViewBag` プロパティでやや単純な構文を使用することもできます。 たとえば、`ViewData["Message"]="text"`を記述するのではなく、`ViewBag.Message="text"`を記述できます。 `ViewBag` プロパティを使用するために、厳密に型指定されたクラスを定義する必要はありません。 動的なプロパティであるため、プロパティを取得または設定するだけで、実行時に動的に解決されます。 内部的には、`ViewBag` のプロパティは、名前と値のペアとして `ViewData` ディクショナリに格納されます。 (注: MVC 3 のほとんどのプレリリースバージョンでは、`ViewBag` プロパティの名前は `ViewModel` プロパティでした。)

### <a name="new-actionresult-types"></a>新しい "ActionResult" 型

MVC 3 では、次の `ActionResult` 型および対応するヘルパーメソッドが新しく追加または強化されています。

- [Httpnotfound 結果](https://msdn.microsoft.com/library/system.web.mvc.httpnotfoundresult(v=vs.98).aspx)。 クライアントに 404 HTTP 状態コードを返します。
- [Redirectresult](https://msdn.microsoft.com/library/system.web.mvc.redirectresult(v=VS.98).aspx)。 ブール型パラメーターに応じて、一時的なリダイレクト (HTTP 302 状態コード) または永続的なリダイレクト (HTTP 301 状態コード) を返します。 この変更と共に、[コントローラー](https://msdn.microsoft.com/library/system.web.mvc.controller(v=VS.98).aspx)クラスには、`RedirectPermanent`、`RedirectToRoutePermanent`、および `RedirectToActionPermanent`の永続的なリダイレクトを実行する3つのメソッドが用意されています。 これらのメソッドは、`Permanent` プロパティが `true`に設定された `RedirectResult` のインスタンスを返します。
- [HttpStatusCodeResult](https://msdn.microsoft.com/library/system.web.mvc.httpstatuscoderesult(v=VS.98).aspx)。 ユーザー指定の HTTP 状態コードを返します。

<a id="BM_JavaScript_and_Ajax_Improvements"></a>

## <a name="javascript-and-ajax-improvements"></a>JavaScript と Ajax の機能強化

既定では、MVC 3 の Ajax および検証ヘルパーは、控えめな JavaScript アプローチを使用します。 控えめになった JavaScript は、インライン JavaScript を HTML に挿入することを回避します。 これにより、HTML のサイズが小さくなり、わかりにくくなり、JavaScript ライブラリを簡単に交換したりカスタマイズしたりできるようになります。 MVC 3 の検証ヘルパーは、既定では `jQueryValidate` プラグインも使用します。 MVC 2 の動作が必要な場合は、 *web.config ファイルの*設定を使用して、控えめな JavaScript を無効にすることができます。 JavaScript と Ajax の機能強化の詳細については、次のリソースを参照してください。

- [Wikipedia のサイトでの控えめな JavaScript の概要](http://en.wikipedia.org/wiki/Unobtrusive_JavaScript)
- [Brad Wilson の控えめな JavaScript 投稿](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-ajax.html)
- [Brad Wilson の控えめな JavaScript 検証の投稿](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html)
- [Razor および控えめな JavaScript を使用した MVC 3 アプリケーションの作成](overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript.md)(ASP.NET サイトのチュートリアル)
- [MVC 3 リリースノート](../whitepapers/mvc3-release-notes.md)

### <a name="client-side-validation-enabled-by-default"></a>クライアント側の検証が既定で有効になっている

以前のバージョンの MVC では、クライアント側の検証を有効にするために、ビューから `Html.EnableClientValidation` メソッドを明示的に呼び出す必要があります。 MVC 3 では、クライアント側の検証が既定で有効になっているため、これは不要になりました。 (これ*は、web.config ファイルの*設定を使用して無効にすることができます)。

クライアント側の検証を機能させるには、サイトで適切な jQuery および jQuery 検証ライブラリを参照する必要があります。 これらのライブラリは、独自のサーバーでホストすることも、Microsoft または Google の CDN (content delivery network) から参照することもできます。

### <a name="remote-validator"></a>リモート検証

ASP.NET MVC 3 では、jQuery Validation プラグインのリモート検証機能のサポートを利用できる新しい[Remoteattribute](https://msdn.microsoft.com/library/system.web.mvc.remoteattribute(v=VS.98).aspx)クラスがサポートされています。 これにより、クライアント側の検証ライブラリは、サーバー側でのみ実行できる検証ロジックを実行するために、サーバー上で定義したカスタムメソッドを自動的に呼び出すことができます。

次の例では、`Remote` 属性は、`UserName` フィールドを検証するために、クライアント検証が `UsersController` クラスで `UserNameAvailable` という名前のアクションを呼び出すように指定しています。

[!code-csharp[Main](mvc3/samples/sample1.cs)]

次の例は、対応するコントローラーを示しています。

[!code-csharp[Main](mvc3/samples/sample2.cs)]

`Remote` 属性の使用方法の詳細については、MSDN ライブラリの「 [how to: ASP.NET MVC でリモート検証を実装する方法](https://msdn.microsoft.com/library/gg508808(VS.98).aspx)」を参照してください。

### <a name="json-binding-support"></a>JSON バインディングのサポート

ASP.NET MVC 3 には、アクションメソッドが JSON エンコードデータを受信し、それをアクションメソッドパラメーターにモデルバインドできる、組み込みの JSON バインドサポートが含まれています。 この機能は、クライアントテンプレートとデータバインディングに関連するシナリオで役立ちます。 (クライアントテンプレートを使用すると、クライアントで実行されるテンプレートを使用して、1つのデータ項目またはデータ項目のセットを書式設定して表示できます)。MVC 3 を使用すると、JSON データを送受信するサーバーのアクションメソッドにクライアントテンプレートを簡単に接続できます。 JSON バインディングのサポートの詳細については、 [Scott Guthrie の MVC 3 Preview ブログの投稿](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx)の**JavaScript と AJAX の機能強化**に関するセクションを参照してください。

<a id="BM_Model_Validation_Improvements"></a>

## <a name="model-validation-improvements"></a>モデル検証の機能強化

### <a name="dataannotations-metadata-attributes"></a>"DataAnnotations" メタデータ属性

ASP.NET MVC 3 は、`DisplayAttribute`などの `DataAnnotations` メタデータ属性をサポートしています。

### <a name="validationattribute-class"></a>"ValidationAttribute" クラス

`ValidationAttribute` クラスは、検証対象のオブジェクトなど、現在の検証コンテキストに関する詳細情報を提供する新しい `IsValid` オーバーロードをサポートするために、.NET Framework 4 で改善されました。 これにより、モデルの別のプロパティに基づいて現在の値を検証できる、より高度なシナリオが可能になります。 たとえば、新しい `CompareAttribute` 属性を使用すると、モデルの2つのプロパティの値を比較できます。 次の例では、有効にするために、`ComparePassword` プロパティが `Password` フィールドと一致している必要があります。

[!code-csharp[Main](mvc3/samples/sample3.cs)]

### <a name="validation-interfaces"></a>検証インターフェイス

[IValidatableObject](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.ivalidatableobject.aspx)インターフェイスを使用すると、モデルレベルの検証を実行できます。また、モデル全体の状態またはモデル内の2つのプロパティ間の検証エラーメッセージを提供できます。 MVC 3 では、モデルバインド時に `IValidatableObject` インターフェイスからエラーを取得し、組み込みの HTML フォームヘルパーを使用して、ビュー内の影響を受けるフィールドに自動的にフラグを設定したり強調表示したりします。

[Iclientvalidatable](https://msdn.microsoft.com/library/system.web.mvc.iclientvalidatable(v=VS.98).aspx)インターフェイスを使用すると、ASP.NET MVC は、検証コントロールがクライアント検証をサポートしているかどうかを実行時に検出できます。 このインターフェイスは、さまざまな検証フレームワークと統合できるように設計されています。

検証インターフェイスの詳細については、 [Scott Guthrie の MVC 3 Preview ブログの投稿](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx)の**モデル検証の機能強化**に関するセクションを参照してください。 (ただし、ブログの "IValidateObject" への参照は "IValidatableObject" である必要があることに注意してください)。

<a id="BM_Dependency_Injection_Improvements"></a>

## <a name="dependency-injection-improvements"></a>依存関係の挿入の機能強化

ASP.NET MVC 3 では、依存関係挿入 (DI) の適用と、依存関係の注入またはコントロールの反転 (IOC) コンテナーとの統合に対するサポートが強化されています。 DI のサポートは、次の領域に追加されました。

- コントローラー (コントローラーファクトリの登録と挿入、コントローラーの挿入)。
- ビュー (ビューエンジンの登録と挿入、ビューページへの依存関係の挿入)。
- アクションフィルター (フィルターの検索と挿入)。
- モデルバインダー (登録と挿入)。
- モデル検証プロバイダー (登録と挿入)。
- モデルメタデータプロバイダー (登録と挿入)。
- 値プロバイダー (登録と挿入)。

MVC 3 では、[共通のサービスロケーター](https://github.com/unitycontainer/commonservicelocator)ライブラリと、そのライブラリの `IServiceLocator` インターフェイスをサポートする DI コンテナーがサポートされています。 また、DI フレームワークの統合を容易にする新しい `IDependencyResolver` インターフェイスもサポートしています。

MVC 3 の DI の詳細については、次のリソースを参照してください。

- [サービスの場所に関する、Brad Wilson の一連のブログ投稿](http://bradwilson.typepad.com/blog/2010/07/service-location-pt1-introduction.html)
- [MVC 3 リリースノート](../whitepapers/mvc3-release-notes.md)

<a id="BM_Other_New_Features"></a>

## <a name="other-new-features"></a>その他の新機能

### <a name="nuget-integration"></a>NuGet の統合

ASP.NET MVC 3 は、セットアップの一部として自動的にインストールされ、NuGet を有効にします。 NuGet は、無料のオープンソースパッケージマネージャーであり、プロジェクト内で .NET ライブラリとツールを簡単に検索、インストール、および使用できます。 これは、すべての Visual Studio プロジェクトの種類 (ASP.NET Web フォームと ASP.NET MVC を含む) で動作します。

NuGet を使用すると、オープンソースプロジェクトを管理する開発者 (たとえば、Moq、NHibernate、Nhibernate、構造体の Map、NUnit、Windsor、RhinoMocks、Elmah などのプロジェクト) を使用して、ライブラリをパッケージ化し、オンラインギャラリーに登録できます。 .NET 開発者は、これらのライブラリのいずれかを使用して、パッケージを検索し、作業しているプロジェクトにインストールするのが簡単です。

ASP.NET 3 ツールの更新プログラムでは、プロジェクトテンプレートには JavaScript ライブラリが事前にインストールされている NuGet パッケージが含まれているため、NuGet を使用して更新できます。 Entity Framework Code First は、NuGet パッケージとしても事前にインストールされています。

NuGet の詳細については、[NuGet のドキュメント](https://docs.microsoft.com/nuget/)を参照してください。

### <a name="partial-page-output-caching"></a>部分ページ出力キャッシュ

ASP.NET MVC は、バージョン1以降のページ全体の応答の出力キャッシュをサポートしています。 MVC 3 では、部分ページ出力キャッシュもサポートされています。これにより、リージョンまたは応答のフラグメントを簡単にキャッシュできます。 キャッシュの詳細については、「mvc 3 リリース候補」の[Scott Guthrie のブログ記事](https://weblogs.asp.net/scottgu/archive/2010/11/09/announcing-the-asp-net-mvc-3-release-candidate.aspx)「 [Mvc 3 リリースノート](../whitepapers/mvc3-release-notes.md) **」の**「**部分ページ出力キャッシュ**」セクションを参照してください。

### <a name="granular-control-over-request-validation"></a>要求の検証をきめ細かく制御する

ASP.NET MVC には、XSS および HTML インジェクション攻撃から保護するための要求検証が組み込まれています。 ただし、ユーザーが HTML コンテンツ (ブログエントリや CMS コンテンツなど) を投稿できるようにする場合など、要求の検証を明示的に無効にすることが必要になる場合があります。 モデルバインド中に、 [AllowHtml](https://msdn.microsoft.com/library/system.web.mvc.allowhtmlattribute(v=VS.98).aspx)属性をモデルに追加したり、モデルを表示して、プロパティごとの検証を無効にしたりできるようになりました。 要求の検証の詳細については、次のリソースを参照してください。

- [MVC 3 リリース候補の Scott Guthrie のブログ投稿](https://weblogs.asp.net/scottgu/archive/2010/11/09/announcing-the-asp-net-mvc-3-release-candidate.aspx)の**控えめな JavaScript と検証**のセクション。
- [MVC 3 リリースノート](../whitepapers/mvc3-release-notes.md)

### <a name="extensible-new-project-dialog-box"></a>拡張可能な [新しいプロジェクト] ダイアログボックス

ASP.NET MVC 3 では、プロジェクトテンプレート、ビューエンジン、および単体テストプロジェクトフレームワークを **[新しいプロジェクト]** ダイアログボックスに追加できます。

### <a name="template-scaffolding-improvements"></a>テンプレートスキャフォールディングの機能強化

ASP.NET MVC 3 スキャフォールディングテンプレートでは、モデルの主キープロパティをより適切に識別し、以前のバージョンの MVC よりも適切に処理することができます。 (たとえば、スキャフォールディングテンプレートでは、主キーが編集可能なフォームフィールドとしてスキャフォールディングされないようになっています)。

既定では、Create と Edit スキャフォールディングは、`Html.TextBoxFor` ヘルパーではなく、`Html.EditorFor` ヘルパーを使用するようになりました。 これにより、 **[ビューの追加]** ダイアログボックスでビューが生成されたときのデータ注釈属性の形式で、モデルのメタデータのサポートが向上します。

### <a name="new-overloads-for-htmllabelfor-and-htmllabelformodel"></a>".Html" と "Html. LabelForModel" の新しいオーバーロード

`LabelFor` および `LabelForModel` ヘルパーメソッドに新しいメソッドオーバーロードが追加されました。 新しいオーバーロードを使用すると、ラベルテキストを指定またはオーバーライドできます。

### <a name="sessionless-controller-support"></a>セッションレスコントローラーのサポート

ASP.NET MVC 3 では、コントローラークラスでセッション状態を使用するかどうかを指定できます。その場合は、セッション状態を読み取り/書き込みまたは読み取り専用にするかどうかを指定できます。 セッションレスコントローラーのサポートの詳細については、「 [MVC 3 リリースノート](../whitepapers/mvc3-release-notes.md)」を参照してください。

### <a name="new-additionalmetadataattribute-class"></a>新しい "AdditionalMetadataAttribute" クラス

[Additionalmetadata](https://msdn.microsoft.com/library/system.web.mvc.additionalmetadataattribute(v=VS.98).aspx)属性を使用して、モデルプロパティの `ModelMetadata.AdditionalValues` ディクショナリを設定できます。 たとえば、ビューモデルに、管理者のみに表示されるプロパティがある場合は、次の例に示すように、そのプロパティに注釈を付けることができます。

[!code-csharp[Main](mvc3/samples/sample4.cs)]

このメタデータは、製品ビューモデルがレンダリングされるときに、任意の表示またはエディターテンプレートで使用できるようになります。 メタデータ情報を解釈するのは、ユーザーの判断です。

### <a name="accountcontroller-improvements"></a>AccountController の機能強化

インターネットプロジェクトテンプレートの AccountController が大幅に改善されました。

### <a name="new-intranet-project-template"></a>新しいイントラネットプロジェクトテンプレート

新しいイントラネットプロジェクトテンプレートが含まれています。これにより、Windows 認証が有効になり、AccountController が削除されます。
