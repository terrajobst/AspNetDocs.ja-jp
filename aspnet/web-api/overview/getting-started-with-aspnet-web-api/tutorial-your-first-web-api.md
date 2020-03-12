---
uid: web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
title: ASP.NET Web API 2 (C#)-ASP.NET 4.X の概要
author: MikeWasson
description: コードを使用したチュートリアル。 製品の一覧を返す Web API を作成するには、ASP.NET Web API を使用します。
ms.author: riande
ms.date: 11/28/2017
ms.custom: seoapril2019
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
msc.type: authoredcontent
ms.openlocfilehash: 2717d93f47be9d4a6548731d8deeca312b25f39f
ms.sourcegitcommit: 9e3ca74997a67c18589729d4b7303799905473eb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/11/2020
ms.locfileid: "79084052"
---
# <a name="get-started-with-aspnet-web-api-2-c"></a>ASP.NET Web API 2 (C#) を使ってみる

[Mike Wasson](https://github.com/MikeWasson)

[完成したプロジェクトのダウンロード](https://code.msdn.microsoft.com/Sample-code-of-Getting-c56ccb28)

このチュートリアルでは、ASP.NET Web API を使用して、製品の一覧を返す Web API を作成します。

HTTP は web ページを提供するためのものではありません。 HTTP は、サービスとデータを公開する Api を構築するための強力なプラットフォームでもあります。 HTTP はシンプルで柔軟性があり、ユビキタスです。 考えられるほとんどすべてのプラットフォームは HTTP ライブラリを持っているので、HTTP サービスは、ブラウザー、モバイルデバイス、従来のデスクトップアプリケーションを含む広範なクライアントに接続できます。

ASP.NET Web API は、.NET Framework 上に Web Api を構築するためのフレームワークです。 

## <a name="software-versions-used-in-the-tutorial"></a>このチュートリアルで使用されているソフトウェアのバージョン

- [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
- Web API 2

このチュートリアルの新しいバージョンについては、「 [ASP.NET Core と Visual Studio For Windows で WEB API を作成する](https://docs.microsoft.com/aspnet/core/tutorials/first-web-api)」を参照してください。

## <a name="create-a-web-api-project"></a>Web API プロジェクトを作成する

このチュートリアルでは、ASP.NET Web API を使用して、製品の一覧を返す Web API を作成します。 フロントエンド web ページでは、jQuery を使用して結果を表示します。

![](tutorial-your-first-web-api/_static/image1.png)

Visual Studio を起動し、**スタート**ページで **[新しいプロジェクト]** を選択します。 または、 **[ファイル]** メニューの **[新規作成]** をポイントし、 **[プロジェクト]** をクリックします。

**[テンプレート]** ペインで、 **[インストールされたテンプレート]** を選択し、  **C#ビジュアル**ノードを展開します。 **[ビジュアルC# ]** で **[Web]** を選択します。 プロジェクトテンプレートの一覧で、 **[ASP.NET Web Application]** を選択します。 プロジェクトに "製品アプリ" という名前を指定し、[ **OK]** をクリックします。

![](tutorial-your-first-web-api/_static/image2.png)

**[New ASP.NET Project]** ダイアログボックスで、**空**のテンプレートを選択します。 &quot;のフォルダーとコア参照を追加 &quot;には、**WEB API** チェックボックスをオンにします。 **[OK]** をクリックします。

![](tutorial-your-first-web-api/_static/image3.png)

> [!NOTE]
> &quot;Web API&quot; テンプレートを使用して Web API プロジェクトを作成することもできます。 Web API テンプレートでは、ASP.NET MVC を使用して API のヘルプページを提供します。 このチュートリアルでは、MVC を使用せずに Web API を表示するため、空のテンプレートを使用しています。 一般に、Web API を使用するために ASP.NET MVC を理解する必要はありません。

## <a name="adding-a-model"></a>モデルの追加

*"モデル"* は、アプリケーションでデータを表すオブジェクトです。 ASP.NET Web API は、モデルを JSON、XML、またはその他の形式に自動的にシリアル化し、シリアル化されたデータを HTTP 応答メッセージの本文に書き込むことができます。 クライアントがシリアル化形式を読み取ることができる限り、オブジェクトを逆シリアル化できます。 ほとんどのクライアントは、XML または JSON を解析できます。 さらに、クライアントは、HTTP 要求メッセージで Accept ヘッダーを設定することによって、必要な形式を示すことができます。

まず、製品を表す単純なモデルを作成してみましょう。

ソリューション エクスプローラーが表示されていない場合は、 **[表示]** メニューをクリックし、 **[ソリューション エクスプローラー]** を選択します。 ソリューション エクスプローラーで、[モデル] フォルダーを右クリックします。 コンテキスト メニューの **[追加]** を選択し、 **[クラス]** を選択します。

![](tutorial-your-first-web-api/_static/image4.png)

クラスに Product&quot;&quot;名前を指定します。 次のプロパティを `Product` クラスに追加します。

[!code-csharp[Main](tutorial-your-first-web-api/samples/sample1.cs)]

## <a name="adding-a-controller"></a>コントローラーの追加

Web API では、"*コントローラー*" は、HTTP 要求を処理するオブジェクトです。 製品の一覧または ID で指定された1つの製品のいずれかを返すことができるコントローラーを追加します。

> [!NOTE]
> ASP.NET MVC を使用している場合は、既にコントローラーに精通しています。 Web API コントローラーは MVC コントローラーに似ていますが、**コントローラー**クラスではなく**ApiController**クラスを継承します。

**ソリューション エクスプローラー**で、[コントローラー] フォルダーを右クリックします。 **[追加]** 、 **[コントローラー]** の順に選択します。

![](tutorial-your-first-web-api/_static/image5.png)

**[スキャフォールディングの追加]** ダイアログで **[Web API コントローラー - 空]** を選択します。 **[追加]** をクリックします。

![](tutorial-your-first-web-api/_static/image6.png)

**[コントローラーの追加]** ダイアログボックスで、コントローラーに &quot;製品コントローラー&quot;という名前を指定します。 **[追加]** をクリックします。

![](tutorial-your-first-web-api/_static/image7.png)

スキャフォールディングによって、Controllers フォルダーに ProductsController.cs という名前のファイルが作成されます。

![](tutorial-your-first-web-api/_static/image8.png)

> [!NOTE]
> コントローラーを Controllers という名前のフォルダーに配置する必要はありません。 フォルダー名は、ソースファイルを整理するための便利な方法にすぎません。

このファイルがまだ開かれていない場合は、ファイルをダブルクリックして開きます。 このファイルのコードを次のコードに置き換えます。

[!code-csharp[Main](tutorial-your-first-web-api/samples/sample2.cs)]

例を単純にするために、製品はコントローラークラス内の固定配列に格納されています。 もちろん、実際のアプリケーションでは、データベースに対してクエリを実行したり、他の外部データソースを使用したりすることがあります。

コントローラーは、製品を返す2つのメソッドを定義します。

- `GetAllProducts` メソッドは、製品のリスト全体を**IEnumerable&lt;Product&gt;** 型として返します。
- `GetProduct` メソッドは、1つの製品をその ID で検索します。

これで完了です。 Web API が動作しています。 コントローラーの各メソッドは、1つまたは複数の Uri に対応します。

| コントローラーメソッド | URI |
| --- | --- |
| GetAllProducts | /api/products |
| GetProduct | /api/*id* |

`GetProduct` メソッドの場合、URI の*id*はプレースホルダーです。 たとえば、ID が5の製品を取得するために、URI は `api/products/5`ます。

Web API が HTTP 要求をコントローラーメソッドにルーティングする方法の詳細については、「 [ASP.NET Web API でのルーティング](../web-api-routing-and-actions/routing-in-aspnet-web-api.md)」を参照してください。

## <a name="calling-the-web-api-with-javascript-and-jquery"></a>Javascript と jQuery を使用した Web API の呼び出し

このセクションでは、AJAX を使用して web API を呼び出す HTML ページを追加します。 ここでは、jQuery を使用して AJAX 呼び出しを行い、結果を使用してページを更新します。

ソリューションエクスプローラーで、プロジェクトを右クリックし、 **[追加]** 、 **[新しい項目]** の順に選択します。

![](tutorial-your-first-web-api/_static/image9.png)

**[新しい項目の追加]** ダイアログで、 **[ビジュアルC# ]** の下にある **[Web]** ノードを選択し、 **[HTML ページ]** 項目を選択します。 ページに「index .html&quot;&quot;名前を付けます。

![](tutorial-your-first-web-api/_static/image10.png)

このファイル内のすべてを次のものに置き換えます。

[!code-html[Main](tutorial-your-first-web-api/samples/sample3.html)]

jQuery を取得するには、いくつかの方法があります。 この例では、 [Microsoft AJAX CDN](../../../ajax/cdn/overview.md)を使用しました。 また、 [http://jquery.com/](http://jquery.com/)からダウンロードすることもできます。また、ASP.NET "Web API" プロジェクトテンプレートには jQuery も含まれています。

### <a name="getting-a-list-of-products"></a>製品の一覧を取得する

製品の一覧を取得するには、HTTP GET 要求を &quot;/api&quot;に送信します。

JQuery [Getjson](http://api.jquery.com/jQuery.getJSON/)関数は、AJAX 要求を送信します。 応答には、JSON オブジェクトの配列が含まれています。 `done` 関数は、要求が成功した場合に呼び出されるコールバックを指定します。 コールバックで、DOM を製品情報で更新します。

[!code-html[Main](tutorial-your-first-web-api/samples/sample4.html)]

### <a name="getting-a-product-by-id"></a>ID で製品を取得する

ID で製品を取得するには、HTTP GET 要求を &quot;/api/*id*&quot;に送信します。ここで、 *ID*は製品 id です。

[!code-javascript[Main](tutorial-your-first-web-api/samples/sample5.js)]

引き続き AJAX 要求を送信するために `getJSON` を呼び出しますが、今回は要求 URI に ID を含めます。 この要求からの応答は、1つの製品の JSON 表現です。

## <a name="running-the-application"></a>アプリケーションの実行

F5 キーを押してアプリケーションのデバッグを開始します。 Web ページは次のようになります。

![](tutorial-your-first-web-api/_static/image11.png)

ID で製品を取得するには、ID を入力し、[検索] をクリックします。

![](tutorial-your-first-web-api/_static/image12.png)

無効な ID を入力すると、サーバーから HTTP エラーが返されます。

![](tutorial-your-first-web-api/_static/image13.png)

## <a name="using-f12-to-view-the-http-request-and-response"></a>F12 を使用した HTTP 要求と応答の表示

HTTP サービスを使用している場合は、HTTP 要求メッセージと応答メッセージを確認すると非常に便利です。 これを行うには、Internet Explorer 9 の F12 開発者ツールを使用します。 Internet Explorer 9 で、 **F12**キーを押してツールを開きます。 **[ネットワーク]** タブをクリックし、 **[キャプチャの開始]** をクリックします。 次に、web ページに戻り、 **F5**キーを押して web ページを再読み込みします。 Internet Explorer は、ブラウザーと web サーバー間の HTTP トラフィックをキャプチャします。 [概要] ビューには、ページのすべてのネットワークトラフィックが表示されます。

![](tutorial-your-first-web-api/_static/image14.png)

相対 URI "api/products/" のエントリを見つけます。 このエントリを選択し、[**詳細ビューにジャンプ] を**クリックします。 詳細ビューには、要求と応答のヘッダーと本文を表示するタブがあります。 たとえば、 **[要求ヘッダー]** タブをクリックすると、クライアントが Accept ヘッダーで &quot;application/json&quot; を要求したことがわかります。

![](tutorial-your-first-web-api/_static/image15.png)

[応答本文] タブをクリックすると、製品リストが JSON にシリアル化された方法を確認できます。 他のブラウザーも同様の機能を備えています。 もう1つの便利なツールとして、web デバッグプロキシ[Fiddler](http://www.fiddler2.com/fiddler2/)があります。 Fiddler を使用して HTTP トラフィックを表示することができます。また、http 要求を構成することもできます。これにより、要求の HTTP ヘッダーを完全に制御できます。

## <a name="see-this-app-running-on-azure"></a>このアプリが Azure で実行されていることを確認する

完成したサイトがライブ web アプリとして実行されていることを確認しますか? 次のボタンをクリックするだけで、アプリの完全なバージョンを Azure アカウントにデプロイできます。

[![](https://azuredeploy.net/deploybutton.png)](https://deploy.azure.com/?WT.mc_id=deploy_azure_aspnet&repository=https://github.com/tfitzmac/WebAPI-ProductsApp#/form/setup)

このソリューションを Azure にデプロイするには、Azure アカウントが必要です。 まだアカウントを持っていない場合は、次のオプションがあります。

- [無料で azure アカウントを開く](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604)-有料の azure サービスを試用するために使用できるクレジットが得られます。また、使用した後でも、アカウントを保持し、無料の azure サービスを使用できます。
- [Msdn サブスクライバーの特典を有効](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604)にする-msdn サブスクリプションでは、有料の Azure サービスに使用できるクレジットが毎月提供されます。

## <a name="next-steps"></a>次の手順

- POST、PUT、DELETE の各アクションとデータベースへの書き込みをサポートする HTTP サービスの完全な例については、「 [Using WEB API 2 with Entity Framework 6](../data/using-web-api-with-entity-framework/part-1.md)」を参照してください。
- HTTP サービス上に流動的で応答性の高い web アプリケーションを作成する方法の詳細については、「 [ASP.NET Single Page Application](../../../single-page-application/index.md)」を参照してください。
- Azure App Service に Visual Studio web プロジェクトを配置する方法の詳細については、「 [Azure App Service での ASP.NET web アプリの作成](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/)」を参照してください。
