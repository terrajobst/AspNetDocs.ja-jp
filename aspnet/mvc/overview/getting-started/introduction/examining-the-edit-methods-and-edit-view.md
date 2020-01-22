---
uid: mvc/overview/getting-started/introduction/examining-the-edit-methods-and-edit-view
title: Edit メソッドと Edit ビューを調べるMicrosoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/06/2019
ms.assetid: 52a4d5fe-aa31-4471-b3cb-a064f82cb791
msc.legacyurl: /mvc/overview/getting-started/introduction/examining-the-edit-methods-and-edit-view
msc.type: authoredcontent
ms.openlocfilehash: 946c88d2b337e3bf634f815c7f1ce045f29d9d84
ms.sourcegitcommit: 88fc80e3f65aebdf61ec9414810ddbc31c543f04
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/22/2020
ms.locfileid: "76518746"
---
# <a name="examining-the-edit-methods-and-edit-view"></a>Edit メソッドと Edit ビューの確認

[Rick Anderson]((https://twitter.com/RickAndMSFT))

[!INCLUDE [Tutorial Note](index.md)]

このセクションでは、ムービーコントローラーに対して生成された `Edit` アクションメソッドとビューを確認します。 しかし、最初に、リリース日の見栄えを良くするために、短い diversion を行います。 *Modelthe modelfile*を開き、次に示す強調表示された行を追加します。

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample1.cs?highlight=2,12-14)]

次のように、日付カルチャを指定することもできます。

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample2.cs?highlight=3)]

[DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) については、次のチュートリアルで説明します。 [Display](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayattribute.aspx) 属性は、フィールドの名前として表示する内容 (ここでは、"ReleaseDate" ではなく、"Release Date") を指定します。 [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx)属性はデータの型 (この場合は日付) を指定するため、フィールドに格納される時刻情報は表示されません。 [Displayformat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx)属性は、日付形式が正しく表示されない、Chrome ブラウザーのバグに必要です。

アプリケーションを実行し、`Movies` コントローラーに移動します。 **編集**リンクの上にマウスポインターを置くと、リンク先の URL が表示されます。

![EditLink_sm](examining-the-edit-methods-and-edit-view/_static/image1.png)

**Edit**リンクは、 *Views\Movies\Index.cshtml*ビューの `Html.ActionLink` メソッドによって生成されました。

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample3.cshtml)]

![Html.ActionLink](examining-the-edit-methods-and-edit-view/_static/image2.png)

`Html` オブジェクトは、 [system.web. Mvc. WebViewPage](https://msdn.microsoft.com/library/gg402107(VS.98).aspx)基本クラスのプロパティを使用して公開されるヘルパーです。 ヘルパーの `ActionLink` メソッドを使用すると、コントローラーのアクションメソッドにリンクする HTML ハイパーリンクを簡単に動的に生成できます。 `ActionLink` メソッドの最初の引数は、表示するリンクテキスト (たとえば、`<a>Edit Me</a>`) です。 2番目の引数は、呼び出すアクションメソッドの名前 (この場合は `Edit` アクション) です。 最後の引数は、ルートデータ (この場合は4の ID) を生成する[匿名オブジェクト](https://weblogs.asp.net/scottgu/archive/2007/05/15/new-orcas-language-feature-anonymous-types.aspx)です。

前の図のように生成されたリンクが `http://localhost:1234/Movies/Edit/4`ます。 既定のルート ( *App\_Start\RouteConfig.cs*) では、URL パターン `{controller}/{action}/{id}`が設定されます。 したがって、ASP.NET は、パラメーター `ID` が4に等しい `Movies` コントローラーの `Edit` アクションメソッドへの `http://localhost:1234/Movies/Edit/4` を要求に変換します。 *アプリ\_Start\RouteConfig.cs*ファイルから、次のコードを確認します。 [Maproute](../../older-versions-1/controllers-and-routing/asp-net-mvc-routing-overview-cs.md)メソッドは、HTTP 要求を適切なコントローラーとアクションメソッドにルーティングし、オプションの ID パラメーターを指定するために使用されます。 [Maproute](../../older-versions-1/controllers-and-routing/asp-net-mvc-routing-overview-cs.md)メソッドは、`ActionLink` などの[htmlhelpers](https://msdn.microsoft.com/library/system.web.mvc.htmlhelper(v=vs.108).aspx)によって、コントローラー、アクションメソッド、およびルートデータに指定された url を生成するためにも使用されます。

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample4.cs?highlight=7)]

クエリ文字列を使用して、アクションメソッドのパラメーターを渡すこともできます。 たとえば、URL `http://localhost:1234/Movies/Edit?ID=3` は、パラメーター `ID` 3 を `Movies` コントローラーの `Edit` アクションメソッドに渡すこともできます。

![EditQueryString](examining-the-edit-methods-and-edit-view/_static/image3.png)

`Movies` コントローラーを開きます。 2つの `Edit` アクションメソッドを次に示します。

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample5.cs?highlight=19-21)]

2 番目の `Edit` アクション メソッドの前に `HttpPost` 属性が付いていることに注意してください。 この属性は、`Edit` メソッドのオーバーロードを POST 要求に対してのみ呼び出すことができるように指定します。 `HttpGet` 属性を最初の編集メソッドに適用することもできますが、これは既定値なので必要ありません。 (ここでは、`HttpGet` 属性を `HttpGet` メソッドとして暗黙的に割り当てられたアクションメソッドについて説明します)。[Bind](https://msdn.microsoft.com/library/system.web.mvc.bindattribute(v=vs.108).aspx)属性は、ハッカーがモデルにデータを過剰に送信することを防ぐ、もう1つの重要なセキュリティメカニズムです。 プロパティは、変更するバインド属性にのみ含める必要があります。 過剰投稿とバインドの属性については、「[過剰投稿のセキュリティ](https://go.microsoft.com/fwlink/?LinkId=317598)に関するメモ」を参照してください。 このチュートリアルで使用する単純なモデルでは、モデル内のすべてのデータをバインドします。 [Validateアンチ Forgerytoken](https://msdn.microsoft.com/library/system.web.mvc.validateantiforgerytokenattribute(v=vs.108).aspx)属性は、要求の偽造を防止するために使用され、edit view file (*Views\Movies\Edit.cshtml*) の `@Html.AntiForgeryToken()` とペアになっています。部分を以下に示します。

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample6.cshtml?highlight=9)]

`@Html.AntiForgeryToken()` は、`Movies` コントローラーの `Edit` メソッドで一致する必要がある非表示の偽造防止トークンを生成します。 クロスサイト要求の偽造 (XSRF または CSRF とも呼ばれます) の詳細については、「チュートリアル[XSRF/Csrf 防止 (MVC](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md))」を参照してください。

`HttpGet` `Edit` メソッドはムービー ID パラメーターを受け取り、Entity Framework `Find` メソッドを使用してムービーを検索し、選択したムービーを編集ビューに返します。 ムービーが見つからない場合は、 [HttpNotFound](https://msdn.microsoft.com/library/gg453938(VS.98).aspx)が返されます。 スキャフォールディング システムが編集ビューを作成したときは、そのシステムが `Movie` クラスを調べて、クラスの各プロパティの `<label>` および `<input>` 要素をレンダリングするコードを作成しました。 次の例は、visual studio のスキャフォールディングシステムによって生成された編集ビューを示しています。

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample7.cshtml)]

ビューテンプレートにファイルの先頭に `@model MvcMovie.Models.Movie` ステートメントがあることに注意してください。これは、ビューがビューテンプレートのモデルを `Movie`型であると想定していることを示します。

スキャフォールディングコードでは、HTML マークアップを効率化するためにいくつかの*ヘルパーメソッド*を使用しています。 [`Html.LabelFor`](https://msdn.microsoft.com/library/gg401864(VS.98).aspx)ヘルパーには、フィールドの名前 (&quot;タイトル&quot;、&quot;releasedate&quot;、&quot;Genre&quot;、または &quot;Price&quot;) が表示されます。 [`Html.EditorFor`](https://msdn.microsoft.com/library/system.web.mvc.html.editorextensions.editorfor(VS.98).aspx)ヘルパーは、HTML `<input>` 要素をレンダリングします。 [`Html.ValidationMessageFor`](https://msdn.microsoft.com/library/system.web.mvc.html.validationextensions.validationmessagefor(VS.98).aspx)ヘルパーには、そのプロパティに関連付けられている検証メッセージが表示されます。

アプリケーションを実行し、 */ムービー*の URL に移動します。 **[編集]** リンクをクリックします。 ブラウザーで、ページのソースを表示します。 Form 要素の HTML を次に示します。

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample8.cshtml?highlight=1-2)]

`<input>` 要素は、`action` 属性が */Movies/Edit* URL に post するように設定されている HTML `<form>` 要素に含まれています。 フォームデータは、 **[保存]** ボタンをクリックするとサーバーにポストされます。 2行目は、`@Html.AntiForgeryToken()` の呼び出しによって生成された非表示の[XSRF](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md)トークンを示しています。

## <a name="processing-the-post-request"></a>POST 要求の処理

次のリストでは、`Edit` アクション メソッドの `HttpPost` バージョンを示します。

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample9.cs)]

[Validateアンチ Forgerytoken](https://msdn.microsoft.com/library/system.web.mvc.validateantiforgerytokenattribute(v=vs.108).aspx)属性は、ビューの `@Html.AntiForgeryToken()` 呼び出しによって生成された[XSRF](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md)トークンを検証します。

[ASP.NET MVC モデルバインダー](https://msdn.microsoft.com/library/dd410405.aspx)は、ポストされたフォーム値を受け取り、`movie` パラメーターとして渡される `Movie` オブジェクトを作成します。 `ModelState.IsValid` は、フォームで送信されたデータを使用して、`Movie` オブジェクトの変更 (編集または更新) を行うことができるかどうかを確認します。 データが有効な場合、ムービーデータは `db`(`MovieDBContext` インスタンス) の `Movies` コレクションに保存されます。 新しいムービーデータは、`MovieDBContext`の `SaveChanges` メソッドを呼び出すことによってデータベースに保存されます。 データを保存した後、コードはユーザーを `MoviesController` クラスの `Index` アクション メソッドにリダイレクトします。そこでは、行われたばかりの変更を含むムービー コレクションが表示されます。

クライアント側の検証によってフィールドの値が無効であると判断されるとすぐに、エラーメッセージが表示されます。 JavaScript が無効になっている場合、クライアント側の検証は無効になります。 ただし、ポストされた値が無効であることがサーバーによって検出され、フォームの値がエラーメッセージと共に再登録されます。

検証の詳細については、チュートリアルの後半で詳しく説明します。

*Edit. cshtml* view テンプレートの `Html.ValidationMessageFor` ヘルパーは、適切なエラーメッセージを表示します。

![abcNotValid](examining-the-edit-methods-and-edit-view/_static/image4.png)

すべての `HttpGet` メソッドは同様のパターンに従います。 これらは、ムービーオブジェクト (または、`Index`の場合はオブジェクトの一覧) を取得し、モデルをビューに渡します。 `Create` メソッドは、空のムービーオブジェクトを Create ビューに渡します。 データの作成、編集、削除、またはそれ以外の変更を行うすべてのメソッドは、メソッドの `HttpPost` のオーバーロードでそれを行います。 HTTP GET メソッドでのデータの変更は、セキュリティ上のリスクがあります。ブログ投稿「 [ASP.NET MVC Tip #46 –セキュリティホールを作成](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx)するので、Delete リンクは使用しない」を参照してください。 GET メソッドでデータを変更することは、HTTP のベストプラクティスおよびアーキテクチャの[REST](http://en.wikipedia.org/wiki/Representational_State_Transfer)パターンにも違反します。これは、get 要求でアプリケーションの状態を変更しないことを指定します。 つまり、GET 操作の実行は、副作用がなく、永続化されたデータを変更しない、安全な操作である必要があります。

## <a name="jquery-validation-for-non-english-locales"></a>英語以外のロケールの jQuery 検証

米国英語版のコンピューターを使用している場合は、このセクションを省略して次のチュートリアルに進むことができます。 このチュートリアルのグローバライズバージョンは、[こちら](https://archive.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=16475)からダウンロードできます。 国際化に関する優れた2部構成のチュートリアルについては、「 [Nadeem's ASP.NET MVC 5 国際化](http://afana.me/post/aspnet-mvc-internationalization.aspx)」を参照してください。

> [!NOTE]
> 小数点に対してコンマ (&quot;、&quot;) を使用する英語以外のロケール、および米国英語以外の日付形式に対して jQuery 検証をサポートするには、`Globalize.parseFloat`を使用するように、*グローバライズ*および特定の*カルチャ/グローバライズ*ファイル ( [https://github.com/jquery/globalize](https://github.com/jquery/globalize)から)、および JavaScript を含める必要があります。 JQuery の英語以外の検証は NuGet から取得できます。 (英語ロケールを使用している場合は、グローバライズをインストールしないでください)。

1. **[ツール]** メニューの **[nuget パッケージマネージャー]** をクリックし、 **[ソリューションの nuget パッケージの管理]** をクリックします。

    ![](examining-the-edit-methods-and-edit-view/_static/image5.png)
2. 左側のウィンドウで、[参照] を選択し<strong>*ます。</strong>* (下の画像を参照してください)。
3. 入力ボックスに「* グローバライズ * *」と入力します。

    `jQuery.Validation.Globalize`を選択 ![](examining-the-edit-methods-and-edit-view/_static/image6.png) には `MvcMovie` を選択し、 **[インストール]** をクリックします。 *スクリプト*を実行すると、プロジェクトにそのファイルが追加されます。 \* スクリプト \ jquery\* フォルダーには、多くのカルチャ JavaScript ファイルが含まれます。 このパッケージのインストールには5分かかる場合があります。

   次のコードは、Views\Movies\Edit.cshtml ファイルに対する変更を示しています。

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample10.cshtml)]

すべての編集ビューでこのコードが繰り返されないようにするには、レイアウトファイルに移動します。 スクリプトのダウンロードを最適化するには、「my チュートリアルの[バンドルと縮小](../../performance/bundling-and-minification.md)」を参照してください。

詳細については、「 [ASP.NET mvc 3 国際化](http://afana.me/post/aspnet-mvc-internationalization.aspx)AND [ASP.NET mvc 3 国際化-パート 2 ()](http://afana.me/post/aspnet-mvc-internationalization-part-2.aspx)」を参照してください。

一時的な解決策として、ロケールでの検証作業ができない場合は、コンピューターで英語 (米国) を使用するように強制するか、ブラウザーで JavaScript を無効にすることができます。 コンピューターで英語 (米国) を使用するには、グローバリゼーション要素をプロジェクトのルート*web.config*ファイルに追加します。 次のコードは、カルチャが米国英語に設定されたグローバリゼーション要素を示しています。

[!code-xml[Main](examining-the-edit-methods-and-edit-view/samples/sample11.xml)]

<a id="gettingstarted"></a><a id="jQueryAjaxJSON"></a>次のチュートリアルでは、検索機能を実装します。

> [!div class="step-by-step"]
> [前へ](accessing-your-models-data-from-a-controller.md)
> [次へ](adding-search.md)
