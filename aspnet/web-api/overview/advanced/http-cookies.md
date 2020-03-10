---
uid: web-api/overview/advanced/http-cookies
title: ASP.NET Web API の HTTP Cookie-ASP.NET 4.x
author: MikeWasson
description: Web API for ASP.NET 4.x で HTTP クッキーを送受信する方法について説明します。
ms.author: riande
ms.date: 09/17/2012
ms.custom: seoapril2019
ms.assetid: 243db2ec-8f67-4a5e-a382-4ddcec4b4164
msc.legacyurl: /web-api/overview/advanced/http-cookies
msc.type: authoredcontent
ms.openlocfilehash: 8ca26ff6776daa13bc4f8b06c2eba61afcfefba2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449314"
---
# <a name="http-cookies-in-aspnet-web-api"></a>ASP.NET Web API の HTTP Cookie

[Mike Wasson](https://github.com/MikeWasson)

このトピックでは、Web API で HTTP cookie を送受信する方法について説明します。

## <a name="background-on-http-cookies"></a>HTTP クッキーの背景

ここでは、HTTP レベルでの cookie の実装方法について簡単に説明します。 詳細については、 [RFC 6265](http://tools.ietf.org/html/rfc6265)を参照してください。

Cookie は、サーバーが HTTP 応答で送信するデータの一部です。 クライアントは (必要に応じて) cookie を保存し、後続の要求でそれを返します。 これにより、クライアントとサーバーが状態を共有できるようになります。 Cookie を設定するために、サーバーには、応答に設定 Cookie ヘッダーが含まれています。 Cookie の形式は、名前と値のペアであり、省略可能な属性があります。 次に例を示します。

[!code-powershell[Main](http-cookies/samples/sample1.ps1)]

属性を使用した例を次に示します。

[!code-powershell[Main](http-cookies/samples/sample2.ps1)]

クッキーをサーバーに返すために、クライアントには、後で要求する Cookie ヘッダーが含まれています。

[!code-console[Main](http-cookies/samples/sample3.cmd)]

![](http-cookies/_static/image1.png)

HTTP 応答には、複数の設定 Cookie ヘッダーを含めることができます。

[!code-powershell[Main](http-cookies/samples/sample4.ps1)]

クライアントは、単一の Cookie ヘッダーを使用して複数の cookie を返します。

[!code-console[Main](http-cookies/samples/sample5.cmd)]

Cookie のスコープと存続期間は、次の属性によって、Set Cookie ヘッダーに含まれる属性によって制御されます。

- **Domain**: クッキーを受信する必要があるドメインをクライアントに指示します。 たとえば、ドメインが "example.com" の場合、クライアントは example.com のすべてのサブドメインに cookie を返します。 指定しない場合、ドメインは配信元サーバーになります。
- **パス**: ドメイン内の指定されたパスに cookie を制限します。 指定しない場合は、要求 URI のパスが使用されます。
- **有効期限**: クッキーの有効期限を設定します。 クライアントは、有効期限が切れたときに cookie を削除します。
- **最長有効期間**: cookie の最大有効期間を設定します。 クライアントは、最大有効期間に達したときにクッキーを削除します。

`Expires` と `Max-Age` の両方が設定されている場合は、`Max-Age` が優先されます。 どちらも設定されていない場合、クライアントは、現在のセッションが終了したときにクッキーを削除します。 ("セッション" の正確な意味は、ユーザーエージェントによって決まります)。

ただし、クライアントでは cookie が無視される可能性があることに注意してください。 たとえば、プライバシー上の理由から、ユーザーが cookie を無効にする場合があります。 クライアントは、有効期限が切れる前に cookie を削除することも、保存される cookie の数を制限することもできます。 プライバシー上の理由から、クライアントは、ドメインが配信元サーバーと一致しない "サードパーティ" の cookie を拒否することがよくあります。 つまり、サーバーは、設定された cookie の取得に依存しないようにする必要があります。

## <a name="cookies-in-web-api"></a>Web API の cookie

クッキーを HTTP 応答に追加するには、クッキーを表す**Cookieheadervalue**インスタンスを作成します。 次に、システムの .Net. Http で定義されている**Addcookies**拡張メソッドを呼び出し**ます。** クッキーを追加する HttpResponseHeadersExtensions クラス。

たとえば、次のコードでは、コントローラーアクション内に cookie を追加します。

[!code-csharp[Main](http-cookies/samples/sample6.cs)]

**Addcookies**は、 **cookieheadervalue**インスタンスの配列を受け取ることに注意してください。

クライアント要求からクッキーを抽出するには、 **Getcookies**メソッドを呼び出します。

[!code-csharp[Main](http-cookies/samples/sample7.cs)]

**Cookieheadervalue**には、 **cookiestate**インスタンスのコレクションが含まれています。 各**Cookiestate**は、1つの cookie を表します。 以下に示すように、インデクサーメソッドを使用して、名前で**Cookiestate**を取得します。

## <a name="structured-cookie-data"></a>構造化された Cookie データ

多くのブラウザーでは、合計数と&#8212;ドメインあたりの数の両方を格納する cookie の数が制限されています。 そのため、複数の cookie を設定するのではなく、構造化されたデータを1つの cookie に格納すると便利な場合があります。

> [!NOTE]
> RFC 6265 では、cookie データの構造は定義されていません。

**Cookieheadervalue**クラスを使用して、cookie データの名前と値のペアのリストを渡すことができます。 これらの名前と値のペアは、URL エンコードされたフォームデータとして、Set Cookie ヘッダーにエンコードされます。

[!code-csharp[Main](http-cookies/samples/sample8.cs)]

前のコードでは、次の Set Cookie ヘッダーが生成されます。

[!code-powershell[Main](http-cookies/samples/sample9.ps1)]

**Cookiestate**クラスには、要求メッセージの cookie からサブ値を読み取るためのインデクサーメソッドが用意されています。

[!code-csharp[Main](http-cookies/samples/sample10.cs)]

## <a name="example-set-and-retrieve-cookies-in-a-message-handler"></a>例: メッセージハンドラーで Cookie を設定および取得する

前の例では、Web API コントローラー内から cookie を使用する方法を示しました。 別の方法として、[メッセージハンドラー](http-message-handlers.md)を使用することもできます。 メッセージハンドラーは、パイプラインの前にコントローラーよりも先に呼び出されます。 メッセージハンドラーは、要求がコントローラーに到達する前に要求から cookie を読み取るか、コントローラーが応答を生成した後に cookie を応答に追加します。

![](http-cookies/_static/image2.png)

次のコードは、セッション Id を作成するためのメッセージハンドラーを示しています。 セッション ID はクッキーに格納されます。 ハンドラーは、セッション cookie の要求を確認します。 要求にクッキーが含まれていない場合、ハンドラーは新しいセッション ID を生成します。 どちらの場合も、ハンドラーは**HttpRequestMessage**プロパティバッグにセッション ID を格納します。 また、セッション cookie を HTTP 応答に追加します。

この実装では、クライアントからのセッション ID がサーバーによって実際に発行されたかどうかは検証されません。 認証形式として使用しないでください。 この例では、HTTP クッキー管理を示します。

[!code-csharp[Main](http-cookies/samples/sample11.cs)]

コントローラーは、 **HttpRequestMessage**プロパティバッグからセッション ID を取得できます。

[!code-csharp[Main](http-cookies/samples/sample12.cs)]
