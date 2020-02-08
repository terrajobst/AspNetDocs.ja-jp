---
uid: web-api/overview/security/authentication-filters
title: ASP.NET Web API 2 | の認証フィルターMicrosoft Docs
author: MikeWasson
description: 認証フィルターは、HTTP 要求を認証するコンポーネントです。 Web API 2 と MVC 5 はどちらも認証フィルターをサポートしていますが、若干異なります。
ms.author: riande
ms.date: 09/25/2014
ms.assetid: b9882e53-b3ca-4def-89b0-322846973ccb
msc.legacyurl: /web-api/overview/security/authentication-filters
msc.type: authoredcontent
ms.openlocfilehash: 2ef9e62a6c634237e920b6d7aba2127b835f959d
ms.sourcegitcommit: e365196c75ce93cd8967412b1cfdc27121816110
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/07/2020
ms.locfileid: "77075074"
---
# <a name="authentication-filters-in-aspnet-web-api-2"></a>ASP.NET Web API 2 の認証フィルター

[Mike Wasson](https://github.com/MikeWasson)

> 認証フィルターは、HTTP 要求を認証するコンポーネントです。 Web API 2 と MVC 5 はどちらも認証フィルターをサポートしていますが、ほとんどの場合、フィルターインターフェイスの名前付け規則によって若干異なります。 このトピックでは、Web API 認証フィルターについて説明します。

認証フィルターを使用すると、個々のコントローラーまたはアクションに対して認証スキームを設定できます。 こうすることで、アプリはさまざまな HTTP リソースに対してさまざまな認証メカニズムをサポートできます。

この記事では、 [https://github.com/aspnet/samples](https://github.com/aspnet/samples)の[基本的な認証](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/BasicAuthentication)サンプルからのコードを紹介します。 このサンプルは、HTTP 基本アクセス認証スキーム (RFC 2617) を実装する認証フィルターを示しています。 このフィルターは `IdentityBasicAuthenticationAttribute`という名前のクラスに実装されています。 サンプルのコードをすべて表示するのではなく、認証フィルターを記述する方法を示す部分だけを示します。

## <a name="setting-an-authentication-filter"></a>認証フィルターを設定する

他のフィルターと同様に、認証フィルターはコントローラーごと、アクション単位、またはすべての Web API コントローラーにグローバルに適用できます。

コントローラーに認証フィルターを適用するには、コントローラークラスを filter 属性で装飾します。 次のコードは、コントローラークラスの `[IdentityBasicAuthentication]` フィルターを設定します。これにより、コントローラーのすべてのアクションに対して基本認証が有効になります。

[!code-csharp[Main](authentication-filters/samples/sample1.cs)]

1つのアクションにフィルターを適用するには、フィルターを使用してアクションを装飾します。 次のコードは、コントローラーの `Post` メソッドの `[IdentityBasicAuthentication]` フィルターを設定します。

[!code-csharp[Main](authentication-filters/samples/sample2.cs)]

フィルターをすべての Web API コントローラーに適用するには、 **Globalconfiguration. Filters**に追加します。

[!code-csharp[Main](authentication-filters/samples/sample3.cs)]

## <a name="implementing-a-web-api-authentication-filter"></a>Web API 認証フィルターを実装する

Web API では、認証フィルターによって、 [system.web. Http. フィルター](https://msdn.microsoft.com/library/system.web.http.filters.iauthenticationfilter.aspx)インターフェイスが実装されます。 また、属性として適用するために、これら**の属性を system.string から継承**する必要があります。

**Iauthenticationfilter**インターフェイスには、次の2つのメソッドがあります。

- **AuthenticateAsync**は、要求で資格情報を検証することによって要求を認証します (存在する場合)。
- **ChallengeAsync**は、必要に応じて、HTTP 応答に認証チャレンジを追加します。

これらのメソッドは、 [rfc 2612](http://tools.ietf.org/html/rfc2616)および[rfc 2617](http://tools.ietf.org/html/rfc2617)で定義されている認証フローに対応します。

1. クライアントは、Authorization ヘッダーで資格情報を送信します。 これは通常、クライアントがサーバーから 401 (未承認) の応答を受信した後に発生します。 ただし、クライアントは、401を取得した直後ではなく、任意の要求で資格情報を送信できます。
2. サーバーが資格情報を受け入れない場合は、401 (未承認) の応答を返します。 応答には、1つまたは複数のチャレンジを含む Www 認証ヘッダーが含まれています。 各チャレンジは、サーバーで認識される認証スキームを指定します。

サーバーは、匿名要求から401を返すこともできます。 実際、これは通常、認証プロセスが開始される方法です。

1. クライアントが匿名要求を送信します。
2. サーバーは401を返します。
3. クライアントは、資格情報を使用して要求を再送信します。

このフローには、*認証*と*承認*の両方の手順が含まれています。

- 認証は、クライアントの id を証明します。
- 承認によって、クライアントが特定のリソースにアクセスできるかどうかが決まります。

Web API では、認証フィルターは認証を処理しますが、承認は処理しません。 承認は、承認フィルターまたはコントローラーアクション内で実行する必要があります。

Web API 2 パイプラインのフローを次に示します。

1. アクションを呼び出す前に、Web API によってそのアクションの認証フィルターの一覧が作成されます。 これには、アクションスコープ、コントローラースコープ、およびグローバルスコープを含むフィルターが含まれます。
2. Web API は、リスト内のすべてのフィルターに対して**AuthenticateAsync**を呼び出します。 各フィルターでは、要求で資格情報を検証できます。 フィルターによって資格情報が正常に検証された場合、フィルターは**IPrincipal**を作成し、要求にアタッチします。 フィルターでは、この時点でエラーをトリガーすることもできます。 その場合、パイプラインの残りの部分は実行されません。
3. エラーがないと仮定すると、要求はパイプラインの残りの部分を通過します。
4. 最後に、Web API は、すべての認証フィルターの**ChallengeAsync**メソッドを呼び出します。 フィルターは、必要に応じて、このメソッドを使用して応答にチャレンジを追加します。 通常は (常にではありませんが)、401エラーに応答して発生します。

次の図は、考えられる2つのケースを示しています。 最初の方法では、認証フィルターによって要求が正常に認証され、承認フィルターによって要求が承認され、コントローラーのアクションによって 200 (OK) が返されます。

![](authentication-filters/_static/image1.png)

2番目の例では、認証フィルターは要求を認証しますが、承認フィルターは 401 (許可されていません) を返します。 この場合、コントローラーアクションは呼び出されません。 認証フィルターによって、Www 認証ヘッダーが応答に追加されます。

![](authentication-filters/_static/image2.png)

その他の組み合わせも&mdash;可能です。たとえば、コントローラーアクションによって匿名要求が許可されている場合は、認証フィルターを使用できますが、承認はありません。

## <a name="implementing-the-authenticateasync-method"></a>AuthenticateAsync メソッドの実装

**AuthenticateAsync**メソッドは、要求の認証を試みます。 このメソッド シグネチャを次に示します。

[!code-csharp[Main](authentication-filters/samples/sample4.cs)]

**AuthenticateAsync**メソッドは、次のいずれかを実行する必要があります。

1. Nothing (no op)。
2. **IPrincipal**を作成し、要求に対して設定します。
3. エラーの結果を設定します。

オプション (1) は、要求に、フィルターによって認識される資格情報がないことを示します。 オプション (2) は、フィルターが要求を正常に認証したことを意味します。 オプション (3) は、要求に無効な資格情報 (間違ったパスワードなど) が含まれていることを示します。これにより、エラー応答がトリガーされます。

ここでは、 **AuthenticateAsync**を実装するための一般的な概要について説明します。

1. 要求で資格情報を探します。
2. 資格情報がない場合は、何もしないで (no op) が返されます。
3. 資格情報があるものの、フィルターで認証スキームが認識されない場合は、何も行わずに (no op) を返します。 パイプライン内の別のフィルターによって、スキームが認識される場合があります。
4. フィルターによって認識される資格情報がある場合は、認証を試みます。
5. 資格情報が正しくない場合は、`context.ErrorResult`を設定して401を返します。
6. 資格情報が有効な場合は、 **IPrincipal**を作成し `context.Principal`を設定します。

次のコードは、[基本認証](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/BasicAuthentication)サンプルの**AuthenticateAsync**メソッドを示しています。 コメントは各ステップを示します。 このコードは、資格情報のない Authorization ヘッダー、不適切な資格情報、および無効なユーザー名/パスワードを使用して、いくつかの種類のエラーを示しています。

[!code-csharp[Main](authentication-filters/samples/sample5.cs)]

## <a name="setting-an-error-result"></a>エラー結果の設定

資格情報が無効である場合、フィルターでは、エラー応答を作成する**Ihttpactionresult**に `context.ErrorResult` を設定する必要があります。 **Ihttpactionresult**の詳細については、「 [Web API 2 でのアクションの結果](../getting-started-with-aspnet-web-api/action-results.md)」を参照してください。

基本認証のサンプルには、この目的に適した `AuthenticationFailureResult` クラスが含まれています。

[!code-csharp[Main](authentication-filters/samples/sample6.cs)]

## <a name="implementing-challengeasync"></a>ChallengeAsync の実装

**ChallengeAsync**メソッドの目的は、必要に応じて、応答に認証チャレンジを追加することです。 このメソッド シグネチャを次に示します。

[!code-csharp[Main](authentication-filters/samples/sample7.cs)]

メソッドは、要求パイプラインのすべての認証フィルターで呼び出されます。

**ChallengeAsync**は、HTTP 応答が作成される*前*と、場合によってはコントローラーアクションが実行される前に呼び出されることを理解しておくことが重要です。 **ChallengeAsync**が呼び出されると、`context.Result` には**Ihttpactionresult**が含まれます。これは、後で HTTP 応答を作成するために使用されます。 そのため、 **ChallengeAsync**を呼び出すと、HTTP 応答に関する情報はまだわかりません。 **ChallengeAsync**メソッドは、`context.Result` の元の値を新しい**Ihttpactionresult**に置き換える必要があります。 この**Ihttpactionresult**は元の `context.Result`をラップする必要があります。

![](authentication-filters/_static/image3.png)

元の**Ihttpactionresult**を呼び出すと*内部結果*が生成され、新しい**ihttpactionresult**によって*外部結果*が生成されます。 外部結果は、次の操作を行う必要があります。

1. 内部結果を呼び出して、HTTP 応答を作成します。
2. 応答を確認します。
3. 必要に応じて、認証チャレンジを応答に追加します。

次の例は、「基本認証のサンプル」から抜粋したものです。 外部結果の**Ihttpactionresult**を定義します。

[!code-csharp[Main](authentication-filters/samples/sample8.cs)]

`InnerResult` プロパティは、内部の**Ihttpactionresult**を保持します。 `Challenge` プロパティは、Www 認証ヘッダーを表します。 **Executeasync**は、最初に `InnerResult.ExecuteAsync` を呼び出して HTTP 応答を作成し、必要に応じてチャレンジを追加することに注意してください。

チャレンジを追加する前に、応答コードを確認してください。 次に示すように、ほとんどの認証方式では、応答が401の場合にのみチャレンジが追加されます。 ただし、一部の認証方式では、成功応答にチャレンジが追加されます。 例については、「 [Negotiate](http://tools.ietf.org/html/rfc4559#section-5) (RFC 4559)」を参照してください。

`AddChallengeOnUnauthorizedResult` クラスを指定すると、 **ChallengeAsync**の実際のコードは単純になります。 結果を作成し `context.Result`にアタッチするだけです。

[!code-csharp[Main](authentication-filters/samples/sample9.cs)]

注: 基本認証のサンプルでは、このロジックを拡張メソッドに配置することによって、このロジックを抽象化します。

## <a name="combining-authentication-filters-with-host-level-authentication"></a>認証フィルターとホストレベル認証の組み合わせ

"ホストレベルの認証" は、要求が Web API フレームワークに到達する前に、ホスト (IIS など) によって実行される認証です。

多くの場合、アプリケーションの残りの部分に対してホストレベルの認証を有効にする必要がありますが、Web API コントローラーに対しては無効にすることができます。 たとえば、一般的なシナリオでは、ホストレベルでフォーム認証を有効にしますが、Web API にはトークンベースの認証を使用します。

Web API パイプライン内でホストレベルの認証を無効にするには、構成で `config.SuppressHostPrincipal()` を呼び出します。 これにより、web api は Web API パイプラインに入る要求から**IPrincipal**を削除します。 実質的には、要求&quot; の認証を解除 &quot;ます。

[!code-csharp[Main](authentication-filters/samples/sample10.cs)]

## <a name="additional-resources"></a>その他のリソース

[ASP.NET Web API セキュリティフィルター](https://msdn.microsoft.com/magazine/dn781361.aspx) (MSDN マガジン)
