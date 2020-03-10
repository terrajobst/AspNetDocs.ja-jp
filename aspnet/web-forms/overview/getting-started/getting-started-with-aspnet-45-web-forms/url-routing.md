---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/url-routing
title: URL ルーティング |Microsoft Docs
author: Erikre
description: このチュートリアルシリーズでは、ASP.NET 4.5 と Microsoft Visual Studio Express 2013 を使用して ASP.NET Web フォームアプリケーションを構築するための基本について説明します。
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 4f4bf092-c400-471f-a876-78fda0417890
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/url-routing
msc.type: authoredcontent
ms.openlocfilehash: 66b727b69ca4f9a3d35b67f492f9a554146e09ef
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78474814"
---
# <a name="url-routing"></a>URL ルーティング

[Erik Reitan](https://github.com/Erikre)

[Wingtip Toys サンプルプロジェクト (C#) をダウンロード](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)するか[、電子書籍 (PDF) をダウンロード](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)します。

> このチュートリアルシリーズでは、ASP.NET 4.5 を使用して ASP.NET Web フォームアプリケーションを構築するための基礎と、Web 用の Microsoft Visual Studio Express 2013 について説明します。 このチュートリアルシリーズ[でC#は、ソースコードが含ま](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)れる Visual Studio 2013 プロジェクトを利用できます。

このチュートリアルでは、Wingtip Toys サンプルアプリケーションを変更して、URL ルーティングをサポートします。 ルーティングを使用すると、web アプリケーションは、検索エンジンによって、わかりやすく、覚えやすく、より優れた Url を使用できます。 このチュートリアルは、前の「メンバーシップと管理」チュートリアルに基づいており、Wingtip Toys チュートリアルシリーズの一部です。

## <a name="what-youll-learn"></a>ここでは、次の内容について学習します。

- ASP.NET Web フォームアプリケーションのルートを登録する方法。
- Web ページにルートを追加する方法。
- ルートをサポートするためにデータベースからデータを選択する方法。

## <a name="aspnet-routing-overview"></a>ASP.NET ルーティングの概要

URL ルーティングを使用すると、物理ファイルにマップされていない要求 Url を受け入れるようにアプリケーションを構成できます。 要求 URL は、ユーザーがブラウザーに入力して web サイト上のページを見つけるための URL です。 ルーティングを使用して、ユーザーに意味のある Url を定義し、検索エンジンの最適化 (SEO) に役立てることができます。

既定では、Web フォームテンプレートには[ASP.NET フレンドリな url](http://www.nuget.org/packages/Microsoft.AspNet.FriendlyUrls/)が含まれています。 基本的なルーティング作業の多くは、*わかりやすい url*を使用して実装されます。 ただし、このチュートリアルでは、カスタマイズされたルーティング機能を追加します。

URL ルーティングをカスタマイズする前に、Wingtip Toys サンプルアプリケーションは次の URL を使用して製品にリンクできます。

`https://localhost:44300/ProductDetails.aspx?productID=2`

URL ルーティングをカスタマイズすることで、Wingtip Toys サンプルアプリケーションは、読みやすい URL を使用して同じ製品にリンクします。

`https://localhost:44300/Product/Convertible%20Car`

### <a name="routes"></a>ルート

ルートは、ハンドラーにマップされる URL パターンです。 ハンドラーは、Web フォームアプリケーションの .aspx ファイルなどの物理ファイルにすることができます。 ハンドラーは、要求を処理するクラスにすることもできます。 ルートを定義するには、ルートクラスのインスタンスを作成します。そのためには、URL パターン、ハンドラー、および必要に応じてルートの名前を指定します。

ルートをアプリケーションに追加するには、`Route` オブジェクトを `RouteTable` クラスの static `Routes` プロパティに追加します。 Route プロパティは、アプリケーションのすべてのルートを格納する `RouteCollection` オブジェクトです。

### <a name="url-patterns"></a>URL パターン

URL パターンには、リテラル値と変数プレースホルダー (URL パラメーターと呼ばれます) を含めることができます。 リテラルとプレースホルダーは、スラッシュ (`/`) 文字で区切られた URL のセグメントに配置されます。

Web アプリケーションへの要求が行われると、URL がセグメントとプレースホルダーに解析され、変数の値が要求ハンドラーに提供されます。 このプロセスは、クエリ文字列内のデータを解析して要求ハンドラーに渡す方法と似ています。 どちらの場合も、変数情報は URL に含まれ、キーと値のペアの形式でハンドラーに渡されます。 クエリ文字列の場合、キーと値の両方が URL に含まれます。 ルートの場合、キーは URL パターンで定義されているプレースホルダー名で、値のみが URL に含まれます。

URL パターンでは、プレースホルダーを中かっこ (`{` および `}`) で囲んで定義します。 1つのセグメントに複数のプレースホルダーを定義できますが、プレースホルダーはリテラル値で区切る必要があります。 たとえば、`{language}-{country}/{action}` は有効なルートパターンです。 ただし、`{language}{country}/{action}` は有効なパターンではありません。これは、プレースホルダーの間にリテラル値または区切り記号がないためです。 そのため、言語プレースホルダーの値を country プレースホルダーの値と区切る場所をルーティングで決定することはできません。

### <a name="mapping-and-registering-routes"></a>ルートのマッピングと登録

Wingtip Toys サンプルアプリケーションのページにルートを追加するには、アプリケーションの起動時にルートを登録する必要があります。 ルートを登録するには、`Application_Start` イベントハンドラーを変更します。

1. Visual Studio の**ソリューションエクスプローラー**で、 *Global.asax.cs*ファイルを見つけて開きます。
2. 次のように、黄色で強調表示されているコードを*Global.asax.cs*ファイルに追加します。   

    [!code-csharp[Main](url-routing/samples/sample1.cs?highlight=30-31,34-46)]

Wingtip Toys サンプルアプリケーションが起動すると、`Application_Start` イベントハンドラーが呼び出されます。 このイベントハンドラーの最後に、`RegisterCustomRoutes` メソッドが呼び出されます。 `RegisterCustomRoutes` メソッドは、`RouteCollection` オブジェクトの `MapPageRoute` メソッドを呼び出すことによって各ルートを追加します。 ルートは、ルート名、ルート URL、および物理 URL を使用して定義されます。

最初のパラメーター ("`ProductsByCategoryRoute`") は、ルート名です。 必要に応じてルートを呼び出すために使用されます。 2番目のパラメーター ("`Category/{categoryName}`") は、コードに基づいて動的に使用できる代替 URL を定義します。 データに基づいて生成されるリンクをデータコントロールに設定する場合は、このルートを使用します。 ルートは次のようになります。

[!code-csharp[Main](url-routing/samples/sample2.cs)]

ルートの2番目のパラメーターには、中かっこ (`{ }`) で指定された動的な値が含まれます。 この場合、`categoryName` は、適切なルーティングパスを決定するために使用される変数です。

> [!NOTE] 
> 
> **省略可能**
> 
> `RegisterCustomRoutes` メソッドを別のクラスに移動することで、コードの管理が容易になる場合があります。 *Logic*フォルダーで、別個の `RouteActions` クラスを作成します。 上の `RegisterCustomRoutes` メソッドを*Global.asax.cs*ファイルから新しい `RoutesActions` クラスに移動します。 *Global.asax.cs*ファイルから `RegisterCustomRoutes` メソッドを呼び出す方法の例として、`RoleActions` クラスと `createAdmin` メソッドを使用します。

また、`Application_Start` イベントハンドラーの先頭にある `RouteConfig` オブジェクトを使用して、`RegisterRoutes` メソッドの呼び出しを確認することもできます。 この呼び出しは、既定のルーティングを実装するために行われます。 これは、Visual Studio の Web フォームテンプレートを使用してアプリケーションを作成したときに既定のコードとして含まれていました。

## <a name="retrieving-and-using-route-data"></a>ルートデータの取得と使用

前述のように、ルートを定義できます。 *Global.asax.cs*ファイルの `Application_Start` イベントハンドラーに追加したコードによって、定義可能なルートが読み込まれます。

### <a name="setting-routes"></a>ルートの設定

ルートでは、追加のコードを追加する必要があります。 このチュートリアルでは、モデルバインドを使用して、データコントロールのデータを使用してルートを生成するときに使用される `RouteValueDictionary` オブジェクトを取得します。 `RouteValueDictionary` オブジェクトには、製品の特定のカテゴリに属する製品名の一覧が含まれます。 データとルートに基づいて、製品ごとにリンクが作成されます。

#### <a name="enable-routes-for-categories-and-products"></a>カテゴリと製品のルートを有効にする

次に、`ProductsByCategoryRoute` を使用するようにアプリケーションを更新して、各製品カテゴリリンクに含める正しいルートを決定します。 また、 *Productlist .aspx*ページを更新して、各製品のルーティングリンクを含めることもできます。 リンクは変更前として表示されますが、リンクは URL ルーティングを使用するようになります。

1. **ソリューションエクスプローラー**で、まだ開いていない場合は、[ *.master* ] ページを開きます。
2. "`categoryList`" という名前の**ListView**コントロールを、黄色で強調表示されている変更で更新します。これにより、マークアップは次のようになります。   

    [!code-aspx[Main](url-routing/samples/sample3.aspx?highlight=7-9)]
3. **ソリューションエクスプローラー**で、 *productlist .aspx*ページを開きます。
4. 更新プログラムが黄色で強調表示されている状態で、 *Productlist .aspx*ページの `ItemTemplate` 要素を更新します。これにより、マークアップは次のようになります。   

    [!code-aspx[Main](url-routing/samples/sample4.aspx?highlight=6-9,14-16)]
5. *ProductList.aspx.cs*の分離コードを開き、黄色で強調表示されている次の名前空間を追加します。  

    [!code-csharp[Main](url-routing/samples/sample5.cs?highlight=9)]
6. 分離コード (*ProductList.aspx.cs*) の `GetProducts` メソッドを次のコードに置き換えます。   

    [!code-csharp[Main](url-routing/samples/sample6.cs)]

#### <a name="add-code-for-product-details"></a>製品の詳細のコードを追加する

次に、 *Productdetails .aspx*ページの分離コード (*ProductDetails.aspx.cs*) を更新して、ルートデータを使用するようにします。 新しい `GetProduct` メソッドでは、ユーザーが、古い非ルーティング URL を使用するリンクがブックマークに登録されている場合にもクエリ文字列値を受け取ることに注意してください。

1. 分離コード (*ProductDetails.aspx.cs*) の `GetProduct` メソッドを次のコードに置き換えます。   

    [!code-csharp[Main](url-routing/samples/sample7.cs)]

## <a name="running-the-application"></a>アプリケーションの実行

アプリケーションを今すぐ実行して、更新されたルートを確認することができます。

1. **F5**キーを押して Wingtip Toys サンプルアプリケーションを実行します。  
 ブラウザーが開き、 *default.aspx*ページが表示されます。
2. ページの上部にある **[Products]** リンクをクリックします。  
 すべての製品が*Productlist .aspx*ページに表示されます。 ブラウザーでは、次の URL (ポート番号を使用) が表示されます。  
    `https://localhost:44300/ProductList`
3. 次に、ページの上部近くにある **[車両]** カテゴリリンクをクリックします。  
 [ *Productlist] .aspx*ページには、自動車のみが表示されます。 ブラウザーでは、次の URL (ポート番号を使用) が表示されます。  
    `https://localhost:44300/Category/Cars`
4. ページに一覧表示されている最初の車の名前 ("**コンバーチブル車**") を含むリンクをクリックして、製品の詳細を表示します。  
 ブラウザーでは、次の URL (ポート番号を使用) が表示されます。  
    `https://localhost:44300/Product/Convertible%20Car`
5. 次に、ルーティングされていない次の URL (ポート番号を使用) をブラウザーに入力します。  
    `https://localhost:44300/ProductDetails.aspx?productID=2`  
 このコードは、ユーザーがリンクをブックマークした場合に、クエリ文字列を含む URL を引き続き認識します。

## <a name="summary"></a>まとめ

このチュートリアルでは、カテゴリと製品のルートを追加しました。 ここでは、モデルバインドを使用するデータコントロールとルートを統合する方法について学習しました。 次のチュートリアルでは、グローバルエラー処理を実装します。

## <a name="additional-resources"></a>その他のリソース

[ASP.NET のフレンドリな Url](http://www.nuget.org/packages/Microsoft.AspNet.FriendlyUrls/)  
[メンバーシップ、OAuth、SQL Database を持つ Secure ASP.NET Web フォームアプリを Azure App Service にデプロイする](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)  
[Microsoft Azure-無料試用版](https://azure.microsoft.com/pricing/free-trial/)

> [!div class="step-by-step"]
> [前へ](membership-and-administration.md)
> [次へ](aspnet-error-handling.md)
