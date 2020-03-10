---
uid: web-api/samples-list
title: Web API サンプルリスト-ASP.NET 4.x
author: rick-anderson
description: ASP.NET 4.x の ASP.NET Web API サンプルリスト
ms.author: riande
ms.date: 09/18/2012
ms.custom: seoapril2019
ms.assetid: 8cbd9d7f-7027-4390-b098-cb81a63ecd6f
msc.legacyurl: /web-api/samples-list
msc.type: content
ms.openlocfilehash: 24368fc80e7fc3c840f1f1f9accf13fa15a06c1b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484264"
---
# <a name="web-api-samples-list"></a>Web API サンプル一覧

## <a name="httpclient-samples"></a>HttpClient のサンプル

**Bing Translate サンプル** | [VS 2012 ソース](https://github.com/aspnet/samples/blob/master/samples/aspnet/HttpClient/BingTranslateSample)

**Httpclient**クラスを使用して[Microsoft Translator サービス](https://msdn.microsoft.com/library/ff512419.aspx)を呼び出す方法について説明します。 Microsoft Translator service API には、OAuth トークンが必要です。このトークンは、トランスレーターサービスへの要求ごとに Azure トークンサーバーに要求を送信することによって取得します。 トークンサーバーからの結果は、変換サービスに送信される要求に送られます。 このサンプルを実行する前に、 [Azure Marketplace からアプリケーションキー](https://msdn.microsoft.com/library/hh454950.aspx)を取得し、AccessTokenMessageHandler sample クラスの情報を入力する必要があります。

 | [VS 2012 ソース](https://github.com/aspnet/samples/blob/master/samples/aspnet/HttpClient/GoogleMapsSample)の[詳細な説明](https://blogs.msdn.com/b/henrikn/archive/2012/02/17/downloading-a-google-map-to-local-file.aspx) | **Google Maps サンプル**

**Httpclient**を使用して、 [Google Maps API](https://developers.google.com/maps/)から Redmond のマップをダウンロードし、ローカルファイルとして保存して、既定のイメージビューアーを開きます。

**Twitter クライアントのサンプル** |  | [VS 2012 ソース](https://github.com/aspnet/samples/blob/master/samples/aspnet/HttpClient/TwitterSample)の[詳細な説明](https://blogs.msdn.com/b/henrikn/archive/2012/02/16/extending-httpclient-with-oauth-to-access-twitter.aspx)

**Httpclient**を使用して簡単な Twitter クライアントを作成する方法について説明します。 このサンプルでは、 **Httpmessagehandler**を使用して、OAuth 認証情報を送信**HttpRequestMessage**に挿入します。 Twitter からの結果は、JSON.NET を使用して読み取られます。 このサンプルを実行する前に、 [Twitter からアプリケーションキー](https://dev.twitter.com/)を取得し、OAuthMessageHandler サンプルクラスの情報を入力する必要があります。

**ワールドバンクのサンプル** |  | vs [2010 ソース](https://github.com/aspnet/samples/blob/master/samples/aspnet/HttpClient/WorldBankSample/Net40) | 対[2012 ソース](https://github.com/aspnet/samples/blob/master/samples/aspnet/HttpClient/WorldBankSample/Net45)の[詳細な説明](https://blogs.msdn.com/b/henrikn/archive/2012/02/16/httpclient-is-here.aspx)

JSON.NET を使用して結果を解析することにより、世界銀行のデータサイトからデータを取得する方法について説明します。

## <a name="web-api-samples"></a>Web API のサンプル

ASP.NET Web API | [VS 2012 ソース](overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)**でのはじめに**

HTTP GET 要求をサポートする基本的な web API を作成する方法について説明します。 [最初の ASP.NET Web API](overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)チュートリアルのソースコードが含まれています。

**ASP.NET Web API JavaScript シナリオ–コメント** | [VS 2012 ソース](https://code.msdn.microsoft.com/ASPNET-Web-API-JavaScript-d0d64dd7)

ASP.NET Web API を使用してブラウザークライアントをサポートする Web Api を構築する方法について説明します。 jQuery を使用して簡単に呼び出すことができます。

**連絡先マネージャー** | [VS 2010 ソース](https://code.msdn.microsoft.com/Contact-Manager-Web-API-0e8e373d)

このサンプルでは、ASP.NET Web API を使用して、簡単な contact manager アプリケーションを作成します。 このアプリケーションは、ASP.NET MVC アプリケーションと Windows Phone アプリケーションが連絡先の一覧を表示および管理するために使用する contact manager web API で構成されます。

**バッチ**処理のサンプル | [詳細な説明](http://trocolate.wordpress.com/2012/07/19/mitigate-issue-260-in-batching-scenario/) | [VS 2012 ソース](https://github.com/aspnet/samples/blob/master/samples/aspnet/WebApi/BatchSample)

ASP.NET 内で HTTP バッチ処理を実装する方法について説明します。 バッチ処理は、1つの MIME マルチパートエンティティ本体内に複数の HTTP 要求を配置することで構成され、その後、HTTP POST としてサーバーに送信されます。 要求は個別に処理され、応答は別の MIME マルチパートエンティティ本体に格納されます。これがクライアントに返されます。

**コンテンツコントローラーのサンプル** | [詳細な説明](https://blogs.msdn.com/b/henrikn/archive/2012/02/24/async-actions-in-asp-net-web-api.aspx) | [vs 2010 ソース](https://github.com/aspnet/samples/blob/master/samples/aspnet/WebApi/ContentControllerSample/Net40) | [対2012ソース](https://github.com/aspnet/samples/blob/master/samples/aspnet/WebApi/ContentControllerSample/Net45)

ストリームを使用して、要求エンティティと応答エンティティを非同期的に読み書きする方法を示します。 サンプルコントローラーには、要求エンティティ本体を非同期に読み取り、ローカルファイルに格納する PUT アクションと、ローカルファイルの内容を返す GET アクションの2つのアクションがあります。

**カスタムアセンブリリゾルバーサンプル** | [VS 2012 ソース](https://github.com/aspnet/samples/blob/master/samples/aspnet/WebApi/CustomAssemblyResolverSample)

動的に読み込まれたライブラリアセンブリからのコントローラーの検出をサポートするように ASP.NET Web API を変更する方法を示します。 このサンプルでは、既定の実装を呼び出すカスタム**IAssembliesResolver**を実装し、ライブラリアセンブリを既定の結果に追加します。

**カスタムメディアの種類のフォーマッタのサンプル** | [詳細な説明](https://blogs.msdn.com/b/henrikn/archive/2012/04/23/using-cookies-with-asp-net-web-api.aspx) | [VS 2010 ソース](https://github.com/aspnet/samples/blob/master/samples/aspnet/WebApi/CustomMediaTypeFormatterSample)

**BufferedMediaTypeFormatter**基本クラスを使用してカスタムメディアタイプフォーマッタを作成する方法について説明します。 この基底クラスは、主に同期読み取りおよび書き込み操作を使用するフォーマッタを対象としています。 このサンプルでは、メディアの種類のフォーマッタを表示するだけでなく、アプリケーションの**Httpconfiguration**の一部として登録することによってフックする方法を示します。 **MediaTypeFormatter**基底クラスを直接使用することもできます。フォーマッタでは、主に非同期の読み取り操作と書き込み操作を使用します。

**カスタムパラメーターバインディングのサンプル** | [詳細な説明](https://blogs.msdn.com/b/jmstall/archive/2012/05/11/webapi-parameter-binding-under-the-hood.aspx) | [VS 2010 ソース](https://github.com/aspnet/samples/blob/master/samples/aspnet/WebApi/CustomParameterBinding)

パラメーターバインドプロセスをカスタマイズする方法を示します。これは、要求の情報をアクションパラメーターにバインドする方法を決定するプロセスです。 このサンプルでは、Home コントローラーには次の4つのアクションがあります。

1. BindPrincipal は、HTTP GET メッセージではなく、カスタム汎用プリンシパルから IPrincipal パラメーターをバインドする方法を示しています。
2. BindCustomComplexTypeFromUriOrBody は、メッセージ本文または HTTP POST メッセージの要求 URI から取得される複合型パラメーターをバインドする方法を示しています。
3. BindCustomComplexTypeFromUriWithRenamedProperty shows how to bind a complex-type parameter with a renamed property which comes from the request URI of an HTTP POST message;
4. PostMultipleParametersFromBody は、POST メッセージの本文から複数のパラメーターをバインドする方法を示しています。

**ファイルアップロードのサンプル** | [詳細な説明](https://blogs.msdn.com/b/henrikn/archive/2012/03/01/file-upload-and-asp-net-web-api.aspx) | [VS 2012 ソース](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/FileUploadSample)

MIME マルチパートファイルのアップロードを使用して**ApiController**にファイルをアップロードする方法と、Progress **notificationhandler**を使用して**httpclient**で進行状況の通知を設定する方法について説明します。 コントローラーは HTML ファイルアップロードの内容を非同期に読み取り、1つまたは複数の本文部分をローカルファイルに書き込みます。 応答には、アップロードされたファイル (またはファイル) に関する情報が含まれます。

**Azure Blob ストアへのファイルのアップロードのサンプル** | [詳細な説明](https://blogs.msdn.com/b/yaohuang1/archive/2012/07/02/asp-net-web-api-and-azure-blob-storage.aspx) | [VS 2012 ソース](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/AzureBlobsFileUploadSample)

このサンプルは、ファイルアップロードのサンプルと似ていますが、アップロードされたファイルをローカルディスクに保存する代わりに、 [Windows AZURE SDK for .net](https://www.windowsazure.com/develop/net/)を使用してファイルを[azure Blob ストア](https://docs.microsoft.com/azure/storage/blobs/storage-dotnet-how-to-use-blobs)に非同期的にアップロードします。 また、 [Azure Blob Storage コンテナー](https://docs.microsoft.com/azure/storage/blobs/storage-dotnet-how-to-use-blobs)に現在存在する blob を一覧表示するメカニズムも提供します。 Azure SDK に付属している**Azure Storage Emulator**に対して実行しているサンプルを試すことができます。 [Azure Storage アカウント](https://docs.microsoft.com/azure/storage/blobs/storage-dotnet-how-to-use-blobs)を持っている場合は、実際のストレージサービスに対しても実行できます。

**Http メッセージハンドラーパイプラインのサンプル** |  | [VS 2010 ソース](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/HttpMessageHandlerPipelineSample)の[詳細な説明](https://blogs.msdn.com/b/henrikn/archive/2012/08/07/httpclient-httpclienthandler-and-httpwebrequesthandler.aspx)

クライアント (**Httpclient**) とサーバー (ASP.NET Web API) の両方で**httpmessagehandler**インスタンスを接続する方法について説明します。 このサンプルでは、クライアントとサーバーの両方で同じハンドラーが使用されています。 まったく同じハンドラーが両方の場所で実行されることはめったにありませんが、オブジェクトモデルはクライアント側とサーバー側で同じです。

**JSON アップロードサンプル** | [VS 2012 ソース](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/JsonUploadSample)

**ApiController**との間で JSON をアップロードしてダウンロードする方法を示します。 このサンプルでは、最小の**ApiController**を使用し、 **httpclient**を使用してそれにアクセスします。

**マッシュアップサンプル** |  | [VS 2012 ソース](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/MashupSample)の[詳細説明](https://blogs.msdn.com/b/henrikn/archive/2012/03/03/async-mashups-using-asp-net-web-api.aspx)

**ApiController**アクション内から複数のリモートサイトに非同期にアクセスする方法を示します。 アクションがヒットするたびに、スレッドがブロックされないように、要求が非同期的に実行されます。

**メモリトレースのサンプル** |  | [VS 2010 ソース](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/MemoryTracingSample)の[詳細な説明](https://blogs.msdn.com/b/roncain/archive/2012/04/12/tracing-in-asp-net-web-api.aspx)

このサンプルプロジェクトでは、ASP.NET Web API アプリケーションにカスタムのインメモリトレースライターをインストールする Nuget パッケージを作成します。

**MongoDB サンプル** |  | [VS 2012 ソース](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/MongoSample)の[詳細説明](https://blogs.msdn.com/b/henrikn/archive/2012/02/19/using-web-api-with-mongodb.aspx)

リポジトリパターンを使用して、 **ApiController**の永続ストアとして MongoDB を使用する方法を示します。

**応答本文プロセッサのサンプル** | [VS 2012 ソース](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/ResponseEntityProcessorSample)

応答エンティティ (つまり HTTP 応答の本文) をクライアントに送信する前にローカルファイルにコピーし、そのファイルに対して追加の処理を非同期的に実行する方法について説明します。 このサンプルでは、応答エンティティをラップする**Httpmessagehandler**を実装します。このハンドラーは、両方とも出力に通常として、ローカルファイルに書き込みます。

**XDocument サンプル** | [詳細な説明](https://blogs.msdn.com/b/henrikn/archive/2012/02/17/push-and-pull-streams-using-httpclient.aspx) | [VS 2012 ソース](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/UploadXDocumentSample)のアップロード

**Pushstreamcontent**および**httpclient**を使用して**ApiController**に XDocument をアップロードする方法について説明します。

**検証サンプル** | [VS 2010 ソース](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/ValidationSample)

ASP.NET WebAPI でモデルの検証属性を使用して、HTTP 要求の内容を検証する方法について説明します。 必要に応じてプロパティをマークする方法、フレームワーク定義の検証属性とカスタム検証属性の両方を使用してモデルに注釈を付ける方法、および無効なモデルの状態に対してエラー応答を返す方法を示します。

**Web フォームのサンプル** |  | [VS 2010 ソース](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/WebFormSample)の[詳細な説明](https://blogs.msdn.com/b/henrikn/archive/2012/02/23/using-asp-net-web-api-with-asp-net-web-forms.aspx)

Web フォームプロジェクトに追加された ApiController を表示します。

**[RestBugs サンプル](https://github.com/howarddierking/RestBugs)**

RestBugs は、ASP.NET Web API と新しい HTTP クライアントライブラリを使用してハイパーメディア駆動型システムを作成する方法を示す単純なバグ追跡アプリケーションです。 このサンプルには、ASP.NET Web API を使用した、クライアントとサーバーの両方の実装が含まれています。 サーバーは、カスタム Razor フォーマッタを使用してリソース表現を生成します。 このサンプルでは、ハイパーメディア設計を使用してクライアントとサーバーを分離することによってもたらされる利点を示す node.js サーバーも提供します。
