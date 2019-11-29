---
uid: web-api/overview/older-versions/creating-a-web-api-that-supports-crud-operations
title: ASP.NET Web API 1-ASP.NET 4.x で CRUD 操作を有効にする
author: MikeWasson
description: チュートリアルでは、ASP.NET 4.x の ASP.NET Web API を使用して、HTTP サービスで CRUD 操作をサポートする方法を示します。
ms.author: riande
ms.date: 01/28/2012
ms.custom: seoapril2019
ms.assetid: c125ca47-606a-4d6f-a1fc-1fc62928af93
msc.legacyurl: /web-api/overview/older-versions/creating-a-web-api-that-supports-crud-operations
msc.type: authoredcontent
ms.openlocfilehash: a096fd1c54df33b40115907a5c2517b2e3fec5b8
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600338"
---
# <a name="enabling-crud-operations-in-aspnet-web-api-1"></a>ASP.NET Web API 1 で CRUD 操作を有効にする

[Mike Wasson](https://github.com/MikeWasson)

[完成したプロジェクトのダウンロード](https://code.msdn.microsoft.com/ASP-NET-Web-API-Tutorial-c4761894)

> このチュートリアルでは、ASP.NET 4.x の ASP.NET Web API を使用して、HTTP サービスで CRUD 操作をサポートする方法について説明します。
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>このチュートリアルで使用されているソフトウェアのバージョン
> 
> 
> - Visual Studio 2012
> - Web API 1 (Web API 2 でも動作)

CRUD は、4つの基本的なデータベース操作である &quot;作成、読み取り、更新、および削除の&quot; を意味します。 多くの HTTP サービスは、REST や REST に似た Api を使用して CRUD 操作もモデル化します。

このチュートリアルでは、非常に単純な web API を構築して製品の一覧を管理します。 各製品には、名前、価格、カテゴリ (&quot;toys&quot; や &quot;ハードウェア&quot;など)、および製品 ID が含まれます。

Products API は、次のメソッドを公開します。

| 動作 | [HTTP メソッド] | 相対 URI |
| --- | --- | --- |
| すべての製品の一覧を取得する | GET | /api/製品 |
| ID で製品を取得する | GET | /api/*id* |
| カテゴリ別に製品を取得する | GET | /api/products? category =*category* |
| 新しい製品を作成する | 投稿 | /api/製品 |
| 製品を更新する | PUT | /api/*id* |
| 製品を削除する | Del | /api/*id* |

Uri の一部には、パスに製品 ID が含まれていることに注意してください。 たとえば、ID が28の製品を取得するために、クライアントは `http://hostname/api/products/28`の GET 要求を送信します。

### <a name="resources"></a>リソース

Products API は、次の2つのリソースの種類の Uri を定義します。

| Resource | URI |
| --- | --- |
| すべての製品の一覧。 | /api/製品 |
| 個々の製品。 | /api/*id* |

### <a name="methods"></a>メソッド

次のように、4つの主要な HTTP メソッド (GET、PUT、POST、および DELETE) を CRUD 操作にマップできます。

- GET は、指定された URI にあるリソースの表現を取得します。 GET はサーバーに副作用を与えません。
- PUT は、指定された URI のリソースを更新します。 サーバーで新しい Uri を指定できるようにする場合は、PUT を使用して、指定した URI で新しいリソースを作成することもできます。 このチュートリアルでは、API は PUT を使用した作成をサポートしていません。
- POST によって新しいリソースが作成されます。 サーバーは、新しいオブジェクトの URI を割り当て、この URI を応答メッセージの一部として返します。
- DELETE は、指定された URI にあるリソースを削除します。

注: PUT メソッドは、product エンティティ全体を置き換えます。 つまり、クライアントは、更新された製品の完全な表現を送信することを想定しています。 部分更新をサポートする場合は、PATCH メソッドを使用することをお勧めします。 このチュートリアルは PATCH を実装していません。

## <a name="create-a-new-web-api-project"></a>新しい Web API プロジェクトを作成する

まず、Visual Studio を実行し、**スタート**ページで **[新しいプロジェクト]** を選択します。 または、 **[ファイル]** メニューの **[新規作成]** をポイントし、 **[プロジェクト]** をクリックします。

**[テンプレート]** ペインで、 **[インストールされたテンプレート]** を選択し、  **C#ビジュアル**ノードを展開します。 **[ビジュアルC# ]** で **[Web]** を選択します。 プロジェクトテンプレートの一覧で、 **[ASP.NET MVC 4 Web アプリケーション]** を選択します。 プロジェクトに ProductStore という名前を &quot;&quot; [ **OK]** をクリックします。

![](creating-a-web-api-that-supports-crud-operations/_static/image1.png)

**[New ASP.NET MVC 4 プロジェクト]** ダイアログで、 **[Web API]** を選択し、 **[OK]** をクリックします。

![](creating-a-web-api-that-supports-crud-operations/_static/image2.png)

## <a name="adding-a-model"></a>モデルの追加

*モデル*は、アプリケーションのデータを表すオブジェクトです。 ASP.NET Web API では、厳密に型指定された CLR オブジェクトをモデルとして使用できます。これらのオブジェクトは、クライアントの XML または JSON に自動的にシリアル化されます。

ProductStore API では、データは製品で構成されているため、`Product`という名前の新しいクラスを作成します。

ソリューションエクスプローラーがまだ表示されていない場合は、 **[表示]** メニューの **[ソリューションエクスプローラー]** をクリックします。 ソリューションエクスプローラーで、 **[モデル]** フォルダーを右クリックします。 コンテキストメニューから **[追加]** を選択し、 **[クラス]** を選択します。 クラスに Product&quot;&quot;名前を指定します。

![](creating-a-web-api-that-supports-crud-operations/_static/image3.png)

次のプロパティを `Product` クラスに追加します。

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample1.cs)]

## <a name="adding-a-repository"></a>リポジトリの追加

製品のコレクションを格納する必要があります。 サービス実装からコレクションを分離することをお勧めします。 このようにして、サービスクラスを書き直すことなくバッキングストアを変更できます。 この種類の設計は、*リポジトリ*パターンと呼ばれます。 まず、リポジトリのジェネリックインターフェイスを定義します。

ソリューションエクスプローラーで、 **[モデル]** フォルダーを右クリックします。 **[追加]** を選択し、 **[新しい項目]** を選択します。

![](creating-a-web-api-that-supports-crud-operations/_static/image4.png)

**[テンプレート]** ウィンドウで、 **[インストールされ]** たC#テンプレート を選択し、ノードを展開します。 でC#、 **[コード]** を選択します。 コードテンプレートの一覧で、 **[インターフェイス]** を選択します。 インターフェイスに IProductRepository&quot;&quot;名前を指定します。

![](creating-a-web-api-that-supports-crud-operations/_static/image5.png)

次の実装を追加します。

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample2.cs)]

次に、&quot;ProductRepository という名前の別のクラスを [モデル] フォルダーに追加します。&quot; このクラスは、`IProductRepository` インターフェイスを実装します。 次の実装を追加します。

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample3.cs)]

リポジトリでは、リストはローカルメモリ内に保持されます。 これはチュートリアルでは問題ありませんが、実際のアプリケーションでは、データベースまたはクラウドストレージにデータを外部に格納することになります。 リポジトリパターンを使用すると、後で実装を変更しやすくなります。

## <a name="adding-a-web-api-controller"></a>Web API コントローラーの追加

ASP.NET MVC を使用している場合は、既にコントローラーに精通しています。 ASP.NET Web API では、*コントローラー*は、クライアントからの HTTP 要求を処理するクラスです。 新しいプロジェクトウィザードでは、プロジェクトの作成時に2つのコントローラーが作成されました。 これらのファイルを表示するには、ソリューションエクスプローラーで [Controllers] フォルダーを展開します。

- HomeController は従来の ASP.NET MVC コントローラーです。 これは、サイトの HTML ページを提供する役割を担い、web API に直接関連するものではありません。
- WebAPI controller の例です。

ソリューションエクスプローラーのファイルを右クリックし、[削除] を選択して、[を削除] をクリックし**ます。** 次のように、新しいコントローラーを追加します。

**ソリューションエクスプローラー**で、Controllers フォルダーを右クリックします。 **[追加]** を選択し、 **[コントローラー]** を選択します。

![](creating-a-web-api-that-supports-crud-operations/_static/image6.png)

コントローラーの**追加**ウィザードで、コントローラーに &quot;製品コントローラー&quot;という名前を指定します。 **[テンプレート]** ボックスの一覧で、 **[空の API コントローラー]** を選択します。 次に、 **[追加]** をクリックします。

![](creating-a-web-api-that-supports-crud-operations/_static/image7.png)

> [!NOTE]
> コントローラーを Controllers という名前のフォルダーに配置する必要はありません。 フォルダー名は重要ではありません。これは、ソースファイルを整理するための便利な方法にすぎません。

**コントローラーの追加**ウィザードでは、ProductsController.cs という名前のファイルが Controllers フォルダーに作成されます。 このファイルがまだ開いていない場合は、ファイルをダブルクリックして開きます。 次の**using ステートメントを追加し**ます。

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample4.cs)]

**Iproductrepository**インスタンスを保持するフィールドを追加します。

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample5.cs)]

> [!NOTE]
> コントローラーが `IProductRepository`の特定の実装に結び付けられるため、コントローラーで `new ProductRepository()` を呼び出すことは最適な設計ではありません。 より適切な方法については、「 [WEB API 依存関係競合回避モジュールの使用](../advanced/dependency-injection.md)」を参照してください。

## <a name="getting-a-resource"></a>リソースを取得する

ProductStore API は、いくつかの &quot;読み取り&quot; アクションを HTTP GET メソッドとして公開します。 各アクションは、`ProductsController` クラスのメソッドに対応します。

| 動作 | [HTTP メソッド] | 相対 URI |
| --- | --- | --- |
| すべての製品の一覧を取得する | GET | /api/製品 |
| ID で製品を取得する | GET | /api/*id* |
| カテゴリ別に製品を取得する | GET | /api/products? category =*category* |

すべての製品の一覧を取得するには、次のメソッドを `ProductsController` クラスに追加します。

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample6.cs)]

メソッド名は &quot;Get&quot;で始まるため、規約によって GET 要求にマップされます。 また、メソッドにはパラメーターがないため、パスに *&quot;id&quot;* セグメントを含まない URI にマップされます。

ID で製品を取得するには、次のメソッドを `ProductsController` クラスに追加します。

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample7.cs)]

このメソッド名も &quot;Get&quot;で始まりますが、メソッドには*id*という名前のパラメーターがあります。このパラメーターは、URI パスの &quot;id&quot; セグメントにマップされます。 ASP.NET Web API framework では、ID がパラメーターの正しいデータ型 (**int**) に自動的に変換されます。

*Id*が有効でない場合、getproduct メソッドは**HttpResponseException**型の例外をスローします。 この例外は、フレームワークによって 404 (見つかりません) エラーに変換されます。

最後に、カテゴリ別に製品を検索するメソッドを追加します。

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample8.cs)]

要求 URI にクエリ文字列が含まれている場合、Web API はクエリパラメーターをコントローラーメソッドのパラメーターと照合しようとします。 そのため、"api/products? category =*category*" という形式の URI は、このメソッドにマップされます。

## <a name="creating-a-resource"></a>リソースの作成

次に、`ProductsController` クラスにメソッドを追加して、新しい製品を作成します。 メソッドの単純な実装を次に示します。

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample9.cs)]

この方法については、次の2点に注意してください。

- メソッド名は &quot;Post...&quot;で始まります。 新しい製品を作成するために、クライアントは HTTP POST 要求を送信します。
- メソッドは、Product 型のパラメーターを受け取ります。 Web API では、複合型のパラメーターは要求本文から逆シリアル化されます。 したがって、クライアントは、XML 形式または JSON 形式のいずれかで、製品オブジェクトのシリアル化された表現を送信することを想定しています。

この実装は機能しますが、まだ完全ではありません。 HTTP 応答には、次のようなものが含まれているのが理想的です。

- **応答コード:** 既定では、Web API フレームワークは応答状態コードを 200 (OK) に設定します。 ただし、HTTP/1.1 プロトコルによっては、POST 要求によってリソースが作成されるときに、サーバーは状態 201 (Created) を使用して応答する必要があります。
- **場所:** サーバーは、リソースを作成するときに、応答の Location ヘッダーに新しいリソースの URI を含める必要があります。

ASP.NET Web API を使用すると、HTTP 応答メッセージを簡単に操作できます。 次に、強化された実装を示します。

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample10.cs)]

メソッドの戻り値の型が**HttpResponseMessage**になっていることに注意してください。 製品の代わりに**HttpResponseMessage**を返すことによって、ステータスコードや場所ヘッダーなどの HTTP 応答メッセージの詳細を制御できます。

**CreateResponse**メソッドは、 **HttpResponseMessage**を作成し、シリアル化された製品オブジェクトの表現を応答メッセージの本文に自動的に書き込みます。

> [!NOTE]
> この例では、`Product`は検証されません。 モデルの検証の詳細については、「 [ASP.NET Web API でのモデルの検証](../formats-and-model-binding/model-validation-in-aspnet-web-api.md)」を参照してください。

## <a name="updating-a-resource"></a>リソースの更新

PUT を使用して製品を更新するのは簡単です。

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample11.cs)]

メソッド名は &quot;Put...&quot;で始まります。これにより、Web API は PUT 要求と照合します。 このメソッドは、製品 ID と更新された製品の2つのパラメーターを受け取ります。 *Id*パラメーターは URI パスから取得され、 *product*パラメーターは要求本文から逆シリアル化されます。 既定では、ASP.NET Web API framework は、要求本文からルートと複合型からの単純なパラメーター型を受け取ります。

## <a name="deleting-a-resource"></a>リソースの削除

リソースを削除するには、"削除..." を定義します。b.

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample12.cs)]

削除要求が成功すると、状態を説明するエンティティ本体を含むステータス 200 (OK) を返すことができます。削除がまだ保留中の場合、状態 202 (受理)または、エンティティ本体のない状態 204 (コンテンツなし)。 この場合、`DeleteProduct` メソッドには `void` 戻り値の型があるため、ASP.NET Web API はこれを自動的に状態コード 204 (コンテンツなし) に変換します。
