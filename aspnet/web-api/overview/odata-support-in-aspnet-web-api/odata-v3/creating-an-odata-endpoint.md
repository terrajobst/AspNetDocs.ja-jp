---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/creating-an-odata-endpoint
title: Web API 2 を使用して OData v3 エンドポイントを作成する |Microsoft Docs
author: MikeWasson
description: Open Data Protocol (OData) は、web 用のデータアクセスプロトコルです。 OData は、データの構造化、データのクエリ、データの操作を行うための統一された方法を提供します...
ms.author: riande
ms.date: 02/25/2014
ms.assetid: 262843d6-43a2-4f1c-82d9-0b90ae6df0cf
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/creating-an-odata-endpoint
msc.type: authoredcontent
ms.openlocfilehash: e68a454398f109dfd089be9c9a44d3fe662acc2f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448222"
---
# <a name="creating-an-odata-v3-endpoint-with-web-api-2"></a>Web API 2 で OData v3 エンドポイントを作成する

[Mike Wasson](https://github.com/MikeWasson)

[完成したプロジェクトのダウンロード](https://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> [Open Data Protocol](http://www.odata.org/) (OData) は、web 用のデータアクセスプロトコルです。 OData は、CRUD 操作 (作成、読み取り、更新、および削除) を使用してデータを構造化し、データを照会し、データセットを操作するための統一された方法を提供します。 OData は、AtomPub (XML) 形式と JSON 形式の両方をサポートしています。 OData では、データに関するメタデータを公開する方法も定義されています。 クライアントはメタデータを使用して、データセットの型情報と関係を検出できます。
>
> ASP.NET Web API を使用すると、データセットの OData エンドポイントを簡単に作成できます。 エンドポイントがサポートする OData 操作を正確に制御できます。 OData 以外のエンドポイントと共に、複数の OData エンドポイントをホストできます。 データモデル、バックエンドビジネスロジック、およびデータ層を完全に制御できます。
>
> ## <a name="software-versions-used-in-the-tutorial"></a>このチュートリアルで使用されているソフトウェアのバージョン
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - Web API 2
> - OData バージョン3
> - Entity Framework 6
> - [Fiddler Web デバッグプロキシ (省略可能)](http://www.fiddler2.com)
>
> Web API の OData サポートが[ASP.NET and Web Tools 2012.2 更新プログラム](https://go.microsoft.com/fwlink/?LinkId=282650)で追加されました。 ただし、このチュートリアルでは Visual Studio 2013 に追加されたスキャフォールディングを使用します。

このチュートリアルでは、クライアントがクエリを実行できる単純な OData エンドポイントを作成します。 また、エンドポイントのC#クライアントも作成します。 このチュートリアルを完了すると、次の一連のチュートリアルでは、エンティティの関係、アクション、$expand/$select を含む機能を追加する方法について説明します。

- [Visual Studio プロジェクトを作成する](#create-project)
- [エンティティモデルを追加する](#add-model)
- [OData コントローラーを追加する](#add-controller)
- [EDM とルートを追加する](#edm)
- [データベースをシード処理する (省略可能)](#seed-db)
- [OData エンドポイントの探索](#explore)
- [OData シリアル化形式](#formats)

<a id="create-project"></a>
## <a name="create-the-visual-studio-project"></a>Visual Studio プロジェクトを作成する

このチュートリアルでは、基本的な CRUD 操作をサポートする OData エンドポイントを作成します。 エンドポイントは、1つのリソース (製品の一覧) を公開します。 後のチュートリアルでは、さらに多くの機能を追加します。

Visual Studio を起動し、スタートページで **[新しいプロジェクト]** を選択します。 または、 **[ファイル]** メニューの **[新規作成]** をポイントし、 **[プロジェクト]** をクリックします。

**[テンプレート]** ペインで、 **[インストールされ]** たテンプレートC# を選択し、ビジュアルノードを展開します。 **[ビジュアルC# ]** で **[Web]** を選択します。 **ASP.NET Web アプリケーション**テンプレートを選択します。

![](creating-an-odata-endpoint/_static/image1.png)

**[New ASP.NET Project]** ダイアログボックスで、**空**のテンプレートを選択します。 [&quot;のフォルダーとコア参照の追加]&quot;で、 **[WEB API]** をオンにします。 **[OK]** をクリックします。

![](creating-an-odata-endpoint/_static/image2.png)

<a id="add-model"></a>
## <a name="add-an-entity-model"></a>エンティティモデルを追加する

*"モデル"* は、アプリケーションでデータを表すオブジェクトです。 このチュートリアルでは、製品を表すモデルが必要です。 このモデルは、OData エンティティ型に対応しています。

ソリューション エクスプローラーで、[モデル] フォルダーを右クリックします。 コンテキスト メニューの **[追加]** を選択し、 **[クラス]** を選択します。

![](creating-an-odata-endpoint/_static/image3.png)

[新しい項目の**追加**] ダイアログボックスで、クラスに Product&quot;&quot;名前を指定します。

![](creating-an-odata-endpoint/_static/image4.png)

> [!NOTE]
> 慣例により、モデルクラスは [モデル] フォルダーに配置されます。 独自のプロジェクトでこの規則に従う必要はありませんが、このチュートリアルで使用します。

Product.cs ファイルで、次のクラス定義を追加します。

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample1.cs)]

ID プロパティはエンティティキーになります。 クライアントは、ID で製品を照会できます。 このフィールドは、バックエンドデータベースの主キーでもあります。

ここでプロジェクトをビルドします。 次の手順では、リフレクションを使用して製品の種類を検索する Visual Studio のスキャフォールディングをいくつか使用します。

<a id="add-controller"></a>
## <a name="add-an-odata-controller"></a>OData コントローラーを追加する

*コントローラー*は、HTTP 要求を処理するクラスです。 OData サービスでは、エンティティセットごとに個別のコントローラーを定義します。 このチュートリアルでは、1つのコントローラーを作成します。

ソリューションエクスプローラーで、Controllers フォルダーを右クリックします。 **[追加]** 、 **[コントローラー]** の順に選択します。

![](creating-an-odata-endpoint/_static/image5.png)

**[スキャフォールディングの追加]** ダイアログボックスで、Entity Framework&quot;を使用して &quot;Web API 2 OData コントローラーとアクションを選択します。

![](creating-an-odata-endpoint/_static/image6.png)

**[コントローラーの追加]** ダイアログで、コントローラーに "製品コントローラー" という名前を指定します。 非同期コントローラーアクションを使用する &quot;&quot; チェックボックスをオンにします。 **[モデル]** ドロップダウンリストで、Product クラスを選択します。

![](creating-an-odata-endpoint/_static/image7.png)

**[新しいデータコンテキスト...]** ボタンをクリックします。 データコンテキストの種類には既定の名前をそのまま使用し、 **[追加]** をクリックします。

![](creating-an-odata-endpoint/_static/image8.png)

[コントローラーの追加] ダイアログボックスの [追加] をクリックして、コントローラーを追加します。

![](creating-an-odata-endpoint/_static/image9.png)

注: 種類...&quot;の取得中にエラーが発生しました &quot;というエラーメッセージが表示された場合は、Product クラスを追加した後に Visual Studio プロジェクトをビルドしたことを確認してください。 スキャフォールディングは、リフレクションを使用してクラスを検索します。

![](creating-an-odata-endpoint/_static/image10.png)

スキャフォールディングは、次の2つのコードファイルをプロジェクトに追加します。

- Products.cs は、OData エンドポイントを実装する Web API コントローラーを定義します。
- ProductServiceContext.cs を使用 Entity Framework して、基になるデータベースに対してクエリを実行するメソッドをに提供します。

![](creating-an-odata-endpoint/_static/image11.png)

<a id="edm"></a>
## <a name="add-the-edm-and-route"></a>EDM とルートを追加する

ソリューションエクスプローラーで、アプリ\_スタートフォルダーを展開し、WebApiConfig.cs という名前のファイルを開きます。 このクラスは、Web API の構成コードを保持します。 このコードを次のコードに置き換えます。

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample2.cs)]

このコードでは、次の2つの処理を行います。

- OData エンドポイントの Entity Data Model (EDM) を作成します。
- エンドポイントのルートを追加します。

EDM は、データの抽象モデルです。 EDM は、メタデータドキュメントを作成し、サービスの Uri を定義するために使用されます。 **ODataConventionModelBuilder**は、既定の名前付け規則 edm のセットを使用して edm を作成します。 この方法では、最小限のコードが必要です。 EDM をより細かく制御する場合は、プロパティ、キー、およびナビゲーションプロパティを明示的に追加することで、**使用**クラスを使用して edm を作成できます。

**EntitySet**メソッドは、エンティティセットを EDM に追加します。

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample3.cs)]

"Products" という文字列は、エンティティセットの名前を定義します。 コントローラーの名前は、エンティティセットの名前と一致している必要があります。 このチュートリアルでは、エンティティセットの名前は "Products" で、コントローラーの名前は `ProductsController`です。 エンティティセットに "ProductSet" という名前を付けた場合は、コントローラーに `ProductSetController`という名前を付けます。 エンドポイントは複数のエンティティセットを持つことができることに注意してください。 各エンティティセットに対して**EntitySet&lt;t&gt;** を呼び出して、対応するコントローラーを定義します。

**MapODataRoute**メソッドは、OData エンドポイントのルートを追加します。

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample4.cs)]

最初のパラメーターは、ルートのフレンドリ名です。 サービスのクライアントには、この名前が表示されません。 2番目のパラメーターは、エンドポイントの URI プレフィックスです。 このコードの場合、Products エンティティセットの URI は http://<em>hostname</em>/odata/Products. になります。 アプリケーションには複数の OData エンドポイントを含めることができます。 各エンドポイントに対して<strong>MapODataRoute</strong>を呼び出し、一意のルート名と一意の URI プレフィックスを指定します。

<a id="seed-db"></a>
## <a name="seed-the-database-optional"></a>データベースをシード処理する (省略可能)

この手順では、Entity Framework を使用して、いくつかのテストデータをデータベースにシード処理します。 この手順は省略可能ですが、OData エンドポイントをすぐにテストできます。

**[ツール]** メニューの **[NuGet パッケージマネージャー]** を選択し、 **[パッケージマネージャーコンソール]** を選択します。 [パッケージ マネージャー コンソール] ウィンドウで、次のコマンドを入力します。

[!code-console[Main](creating-an-odata-endpoint/samples/sample5.cmd)]

これにより、移行という名前のフォルダーと Configuration.cs という名前のコードファイルが追加されます。

![](creating-an-odata-endpoint/_static/image12.png)

このファイルを開き、`Configuration.Seed` メソッドに次のコードを追加します。

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample6.cs)]

[パッケージマネージャーコンソール] ウィンドウで、次のコマンドを入力します。

[!code-console[Main](creating-an-odata-endpoint/samples/sample7.cmd)]

これらのコマンドは、データベースを作成し、そのコードを実行するコードを生成します。

<a id="explore"></a>
## <a name="exploring-the-odata-endpoint"></a>OData エンドポイントの探索

このセクションでは、 [Fiddler Web デバッグプロキシ](http://www.fiddler2.com)を使用して、エンドポイントに要求を送信し、応答メッセージを確認します。 これは、OData エンドポイントの機能を理解するのに役立ちます。

Visual Studio で、F5 キーを押してデバッグを開始します。 既定では、Visual Studio はブラウザーを開いて `http://localhost:*port*`します。ここで、 *port*はプロジェクト設定で構成されているポート番号です。

プロジェクト設定でポート番号を変更できます。 ソリューションエクスプローラーで、プロジェクトを右クリックし、 **[プロパティ]** を選択します。 プロパティ ウィンドウで、 **Web** を選択します。 **[プロジェクト Url]** にポート番号を入力します。

### <a name="service-document"></a>サービスドキュメント

*サービスドキュメント*には、OData エンドポイントのエンティティセットの一覧が含まれています。 サービスドキュメントを取得するには、サービスのルート URI に GET 要求を送信します。

Fiddler を使用して、 **[Composer]** タブに次の URI を入力します `http://localhost:port/odata/`。ここで、 *port*はポート番号です。

![](creating-an-odata-endpoint/_static/image13.png)

**[実行]** ボタンをクリックします。 Fiddler は、アプリケーションに HTTP GET 要求を送信します。 [Web セッション] の一覧に応答が表示されます。 すべてが動作している場合、状態コードは200になります。

![](creating-an-odata-endpoint/_static/image14.png)

[Web セッション] の一覧で応答をダブルクリックすると、[インスペクター] タブに応答メッセージの詳細が表示されます。

![](creating-an-odata-endpoint/_static/image15.png)

未加工の HTTP 応答メッセージは、次のようになります。

[!code-console[Main](creating-an-odata-endpoint/samples/sample8.cmd)]

既定では、Web API はサービスドキュメントを AtomPub 形式で返します。 JSON を要求するには、HTTP 要求に次のヘッダーを追加します。

`Accept: application/json`

![](creating-an-odata-endpoint/_static/image16.png)

HTTP 応答に JSON ペイロードが含まれるようになりました。

[!code-console[Main](creating-an-odata-endpoint/samples/sample9.cmd)]

### <a name="service-metadata-document"></a>サービスメタデータドキュメント

*サービスメタデータドキュメント*では、概念スキーマ定義言語 (CSDL) と呼ばれる XML 言語を使用した、サービスのデータモデルについて説明します。 メタデータドキュメントには、サービス内のデータの構造が表示され、クライアントコードを生成するために使用できます。

メタデータドキュメントを取得するには、GET 要求を `http://localhost:port/odata/$metadata`に送信します。 このチュートリアルでは、エンドポイントのメタデータを次に示します。

[!code-console[Main](creating-an-odata-endpoint/samples/sample10.cmd)]

### <a name="entity-set"></a>エンティティ セット

Products エンティティセットを取得するには、GET 要求を `http://localhost:port/odata/Products`に送信します。

[!code-console[Main](creating-an-odata-endpoint/samples/sample11.cmd)]

### <a name="entity"></a>Entity

個々の製品を取得するには、GET 要求を `http://localhost:port/odata/Products(1)`に送信します。 "1" は製品 ID です。

[!code-console[Main](creating-an-odata-endpoint/samples/sample12.cmd)]

<a id="formats"></a>
## <a name="odata-serialization-formats"></a>OData シリアル化形式

OData は、いくつかのシリアル化形式をサポートします。

- Atom Pub (XML)
- JSON "light" (OData v3 で導入)
- JSON "verbose" (OData v2)

既定では、Web API は AtomPubJSON "light" 形式を使用します。

AtomPub 形式を取得するには、Accept ヘッダーを "application/atom + xml" に設定します。 次は応答本文の例です。

[!code-console[Main](creating-an-odata-endpoint/samples/sample13.cmd)]

Atom 形式の1つの明確な欠点を確認できます。これは、JSON ライトよりもはるかに詳細です。 ただし、AtomPub を認識するクライアントがある場合、クライアントは JSON よりも形式を優先する可能性があります。

同じエンティティの JSON light バージョンを次に示します。

[!code-console[Main](creating-an-odata-endpoint/samples/sample14.cmd)]

JSON light 形式は、OData プロトコルのバージョン3で導入されました。 旧バージョンとの互換性を維持するために、クライアントは古い "verbose" JSON 形式を要求できます。 詳細な JSON を要求するには、Accept ヘッダーを `application/json;odata=verbose`に設定します。 詳細バージョンは次のとおりです。

[!code-console[Main](creating-an-odata-endpoint/samples/sample15.cmd)]

この形式では、応答本文により多くのメタデータが伝達されます。これにより、セッション全体でかなりのオーバーヘッドが発生する可能性があります。 また、"d" という名前のプロパティにオブジェクトをラップすることによって、レベルの間接参照を追加します。

## <a name="next-steps"></a>次の手順

- [エンティティリレーションの追加](working-with-entity-relations.md)
- [OData アクションの追加](odata-actions.md)
- [.NET クライアントから OData サービスを呼び出す](calling-an-odata-service-from-a-net-client.md)
