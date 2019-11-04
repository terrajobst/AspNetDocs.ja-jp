---
uid: web-api/overview/testing-and-debugging/troubleshooting-http-405-errors-after-publishing-web-api-applications
title: Visual Studio で動作し、実稼働 IIS サーバーで失敗する Web API2 アプリのトラブルシューティング
author: rmcmurray
description: Visual Studio で動作し、実稼働 IIS サーバーで失敗する Web API2 アプリのトラブルシューティング
ms.author: riande
ms.date: 01/23/2019
ms.assetid: 07ec7d37-023f-43ea-b471-60b08ce338f7
msc.legacyurl: /web-api/overview/testing-and-debugging/troubleshooting-http-405-errors-after-publishing-web-api-applications
msc.type: authoredcontent
ms.openlocfilehash: 1b47f1ade3619cfd010260352f6a96985ab3598b
ms.sourcegitcommit: 84b1681d4e6253e30468c8df8a09fe03beea9309
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/02/2019
ms.locfileid: "73445706"
---
# <a name="troubleshoot-web-api2-apps-that-work-in-visual-studio-and-fail-on-a-production-iis-server"></a>Visual Studio で動作し、実稼働 IIS サーバーで失敗する Web API2 アプリのトラブルシューティング

> このドキュメントでは、運用環境の IIS サーバーに配置されている Web API2 アプリのトラブルシューティングを行う方法について説明します。 一般的な HTTP 405 および501のエラーに対処します。
> 
> ## <a name="software-used-in-this-tutorial"></a>このチュートリアルで使用するソフトウェア
> 
> 
> - [インターネットインフォメーションサービス (IIS)](https://www.iis.net/) (バージョン7以降)
> - [Web API](../../index.md) 

Web API apps では、通常、GET、POST、PUT、DELETE、および場合によっては修正プログラムがいくつか使用されます。 このように、開発者は、これらの動詞が実稼働 IIS サーバー上の別の IIS モジュールによって実装されている状況になる可能性があります。これにより、Visual Studio または開発サーバーで正しく動作する Web API コントローラーが、実稼働 IIS サーバーに配置されると、HTTP 405 エラーが返されます。

## <a name="what-causes-http-405-errors"></a>HTTP 405 エラーの原因

HTTP 405 エラーをトラブルシューティングするための最初の手順は、HTTP 405 エラーが実際に意味することを理解することです。 HTTP のプライマリ管理ドキュメントは[RFC 2616](http://www.ietf.org/rfc/rfc2616.txt)であり、これによって、http 405 ステータスコードがメソッドとして***許可されていない***ものとして定義されています。また、この状態コードについては、要求行に指定されたメソッドが許可されていない &quot;、要求 URI によって識別されるリソース。つまり、http クライアントが要求した特定の URL に対して HTTP 動詞を使用することはできません。&quot;

ここでは、RFC 2616、RFC 4918、RFC 5789 で定義されている、最も使用されている HTTP メソッドのいくつかについて簡単に説明します。

| HTTP メソッド | 説明 |
| --- | --- |
| **取得** | このメソッドは、URI からデータを取得するために使用され、おそらく最も使用される HTTP メソッドです。 |
| **HEAD** | このメソッドは GET メソッドに似ていますが、実際には、要求 URI からデータを取得しない点が異なります。 HTTP ステータスを取得するだけです。 |
| **投稿** | このメソッドは、通常、URI に新しいデータを送信するために使用されます。POST は、フォームデータを送信するためによく使用されます。 |
| **投入** | このメソッドは通常、URI に生データを送信するために使用されます。PUT は、JSON または XML データを Web API アプリケーションに送信するためによく使用されます。 |
| **DELETE** | このメソッドは、URI からデータを削除するために使用されます。 |
| **OPTIONS** | このメソッドは、通常、URI でサポートされている HTTP メソッドの一覧を取得するために使用されます。 |
| **コピー移動** | これらの2つの方法は、WebDAV と共に使用され、その目的はわかりやすいものです。 |
| **MKCOL** | このメソッドは WebDAV と共に使用され、指定された URI にコレクション (ディレクトリなど) を作成するために使用されます。 |
| **PROPFIND PROPPATCH** | これらの2つのメソッドは、WebDAV と共に使用され、URI のプロパティを照会または設定するために使用されます。 |
| **ロックロック解除** | これらの2つのメソッドは、WebDAV と共に使用され、作成時に要求 URI によって識別されるリソースをロック/ロック解除するために使用されます。 |
| **KB830347** | このメソッドは、既存の HTTP リソースを変更するために使用されます。 |

これらの HTTP メソッドのいずれかがサーバーで使用するように構成されている場合、サーバーは、その要求に適した HTTP ステータスおよびその他のデータを使用して応答します。 (たとえば、GET メソッドは HTTP 200 ***OK***応答を受け取り、PUT メソッドは Http 201 ***Created***応答を受け取ることがあります)。

HTTP メソッドがサーバーで使用するように構成されていない場合、サーバーは HTTP 501 の実装されて***いない***エラーで応答します。

ただし、HTTP メソッドがサーバーで使用するように構成されていても、特定の URI に対して無効になっている場合、サーバーは HTTP 405 メソッドの許可されて***いない***エラーで応答します。

## <a name="example-http-405-error"></a>HTTP 405 エラーの例

次の HTTP 要求と応答の例では、HTTP クライアントが web サーバー上の Web API アプリに値を設定しようとしたときに、PUT メソッドが許可されていないことを示す HTTP エラーが返されます。

HTTP 要求:

[!code-console[Main](troubleshooting-http-405-errors-after-publishing-web-api-applications/samples/sample1.cmd)]

HTTP 応答:

[!code-console[Main](troubleshooting-http-405-errors-after-publishing-web-api-applications/samples/sample2.cmd)]

この例では、HTTP クライアントが web サーバー上の Web API アプリケーションの URL に有効な JSON 要求を送信しましたが、サーバーは、PUT メソッドが URL に許可されていないことを示す HTTP 405 エラーメッセージを返しました。 これに対し、要求 URI が Web API アプリケーションのルートと一致しなかった場合、サーバーは HTTP 404 ***Not Found***エラーを返します。

## <a name="resolve-http-405-errors"></a>HTTP 405 エラーの解決

特定の HTTP 動詞が許可されない理由はいくつかありますが、IIS では、このエラーの主な原因として、複数のハンドラーが同じ動詞/メソッドに対して定義されています。また、1つのハンドラーが、予期されたハンドラーをブロックしています。要求を処理しています。 説明のとおり、IIS では、 *applicationhost.config*および*web.config*ファイル内の順序ハンドラーエントリに基づいて、最初から最後までのハンドラーを処理します。このとき、最初に一致したパス、動詞、リソースなどの組み合わせが使用され、要求。

次の例は、PUT メソッドを使用して Web API アプリケーションにデータを送信するときに、HTTP 405 エラーを返す IIS サーバーの*applicationhost.config*ファイルからの抜粋です。 この抜粋では、複数の HTTP ハンドラーが定義されており、各ハンドラーには構成されている HTTP メソッドのセットが異なります。リストの最後のエントリは静的なコンテンツハンドラーです。これは、他のハンドラーが chanc を持っていた後に使用される既定のハンドラーです。要求を確認するには、次のようにします。

[!code-xml[Main](troubleshooting-http-405-errors-after-publishing-web-api-applications/samples/sample3.xml)]

前の例では、WebDAV ハンドラーと ASP.NET (Web API に使用される) の拡張 URL ハンドラーが、HTTP メソッドの個別のリストに対して明確に定義されています。 ISAPI DLL ハンドラーはすべての HTTP メソッドに対して構成されることに注意してください。ただし、この構成では必ずしもエラーが発生するとは限りません。 ただし、このような構成設定は、HTTP 405 エラーのトラブルシューティングを行うときに考慮する必要があります。

前の例では、ISAPI DLL ハンドラーは問題ではありませんでした。実際、問題は IIS サーバーの*applicationhost.config*ファイルで定義されていませんでした。この問題は、web API アプリケーションが Visual Studio で作成されたときに*web.config ファイルで*作成されたエントリが原因でした。 アプリケーションの web.config ファイルの次の抜粋は、問題の場所を示して*い*ます。

[!code-xml[Main](troubleshooting-http-405-errors-after-publishing-web-api-applications/samples/sample4.xml)]

この抜粋では、ASP.NET の拡張機能のない URL ハンドラーを再定義して、Web API アプリケーションで使用される追加の HTTP メソッドを含めます。 ただし、同様の HTTP メソッドセットが WebDAV ハンドラーに対して定義されているため、競合が発生します。 この特定のケースでは、Web API アプリケーションを含む web サイトで WebDAV が無効になっていても、WebDAV ハンドラーは IIS によって定義および読み込まれます。 HTTP PUT 要求の処理中に、IIS は PUT 動詞に対して定義されているため、WebDAV モジュールを呼び出します。 WebDAV モジュールが呼び出されると、構成を確認し、無効になっていることを確認します。これにより、WebDAV 要求に似た要求に対して、HTTP 405 メソッドの許可されて***いない***エラーが返されます。 この問題を解決するには、Web API アプリケーションが定義されている web サイトの HTTP モジュールの一覧から WebDAV を削除する必要があります。 次の例は、どのようなものかを示しています。

[!code-xml[Main](troubleshooting-http-405-errors-after-publishing-web-api-applications/samples/sample5.xml)]

このシナリオは、多くの場合、アプリケーションが開発環境から IIS 運用環境に発行された後で発生します。これは、開発環境と運用環境の間でハンドラーやモジュールの一覧が異なるために発生します。 たとえば、Visual Studio 2012 以降を使用して Web API アプリケーションを開発している場合、IIS Express はテスト用の既定の web サーバーです。 この開発 web サーバーは、サーバー製品に付属する完全な IIS 機能をスケールダウンしたバージョンです。この開発 web サーバーには、開発シナリオ用に追加されたいくつかの変更が含まれています。 たとえば、多くの場合、WebDAV モジュールは、完全版の IIS を実行している運用 web サーバーにインストールされますが、使用されていない場合もあります。 IIS の開発バージョン (IIS Express) は、WebDAV モジュールをインストールしますが、WebDAV モジュールのエントリは意図的にコメントアウトされているので、IIS Express 構成を明示的に変更しない限り、WebDAV モジュールが IIS Express に読み込まれることはありません。IIS Express のインストールに WebDAV 機能を追加するための設定。 その結果、web アプリケーションは開発用コンピューターで正しく動作しますが、運用環境の IIS web サーバーに Web API アプリケーションを発行すると、HTTP 405 エラーが発生する場合があります。

## <a name="http-501-errors"></a>HTTP 501 エラー

* 特定の機能がサーバーに実装されていないことを示します。
* 通常、HTTP 要求に一致するハンドラーが IIS 設定に定義されていないことを意味します。
  * IIS に何かが正しくインストールされていないことを示している場合があります。
  * 特定の HTTP メソッドをサポートするハンドラーが定義されていないように、何らかの方法で IIS 設定が変更されています。

この問題を解決するには、対応するモジュールまたはハンドラーの定義がない HTTP メソッドを使用しようとしているアプリケーションを再インストールする必要があります。

## <a name="summary"></a>まとめ

Http 405 エラーは、要求された URL に対して web サーバーで HTTP メソッドが許可されていない場合に発生します。 この条件は、特定の動詞に対して特定のハンドラーが定義されていて、そのハンドラーが要求を処理するハンドラーをオーバーライドしている場合によく見られます。
