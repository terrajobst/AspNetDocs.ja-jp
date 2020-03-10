---
uid: web-api/overview/security/working-with-ssl-in-web-api
title: Web API での SSL の使用 |Microsoft Docs
author: MikeWasson
description: Ssl クライアント証明書を使用するなど、ASP.NET Web API で SSL を使用する方法について説明します。
ms.author: riande
ms.date: 02/22/2019
ms.assetid: 97f6164f-59cf-45c0-b820-e4aa29b45396
msc.legacyurl: /web-api/overview/security/working-with-ssl-in-web-api
msc.type: authoredcontent
ms.openlocfilehash: 31589b3713b1f1a9b98d12906bfef81f8bf5e3f9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484414"
---
# <a name="working-with-ssl-in-web-api"></a>Web API での SSL の操作

[Mike Wasson](https://github.com/MikeWasson)

いくつかの一般的な認証方式は、プレーンな HTTP を介してセキュリティで保護されていません。 具体的には、基本認証とフォーム認証で送信する資格情報が暗号化されません。 セキュリティを確保するために、これらの認証方式では SSL を使用する*必要があり*ます。 さらに、SSL クライアント証明書を使用してクライアントを認証することもできます。

## <a name="enabling-ssl-on-the-server"></a>サーバーで SSL を有効にする

IIS 7 以降で SSL を設定するには:

- 証明書を作成または取得します。 テストの場合は、自己署名証明書を作成できます。
- HTTPS バインドを追加します。

詳細については、「 [IIS 7 で SSL を設定する方法](https://www.iis.net/learn/manage/configuring-security/how-to-set-up-ssl-on-iis)」を参照してください。

ローカルテストでは、Visual Studio から IIS Express で SSL を有効にすることができます。 プロパティウィンドウで、 **[SSL Enabled]** を**True**に設定します。 **SSL URL**の値を確認します。この URL を使用して、HTTPS 接続をテストします。

![](working-with-ssl-in-web-api/_static/image1.png)

### <a name="enforcing-ssl-in-a-web-api-controller"></a>Web API コントローラーでの SSL の適用

HTTPS と HTTP の両方のバインドがある場合でも、クライアントは引き続き HTTP を使用してサイトにアクセスできます。 HTTP を介して一部のリソースを使用できるようにする一方で、他のリソースには SSL が必要な場合があります。 その場合は、アクションフィルターを使用して、保護されたリソースに対して SSL を要求します。 次のコードは、SSL をチェックする Web API 認証フィルターを示しています。

[!code-csharp[Main](working-with-ssl-in-web-api/samples/sample1.cs)]

このフィルターを、SSL を必要とする Web API アクションすべてに追加します。

[!code-csharp[Main](working-with-ssl-in-web-api/samples/sample2.cs)]

## <a name="ssl-client-certificates"></a>SSL クライアント証明書

SSL は、公開キーインフラストラクチャ証明書を使用して認証を提供します。 サーバーは、クライアントに対してサーバーを認証する証明書を提供する必要があります。 クライアントがサーバーに証明書を提供するのはあまり一般的ではありませんが、これはクライアントを認証するための1つのオプションです。 SSL でクライアント証明書を使用するには、署名入り証明書をユーザーに配布する方法が必要です。 多くのアプリケーションの種類では、これは適切なユーザーエクスペリエンスではありませんが、環境によっては (たとえば、enterprise) 使用可能な場合があります。

| 長所 | 短所 |
| --- | --- |
| -証明書の資格情報は、ユーザー名/パスワードよりも強力です。 -SSL は、認証、メッセージの整合性、およびメッセージの暗号化を使用して、完全なセキュリティで保護されたチャネルを提供します。 | -PKI 証明書を取得して管理する必要があります。 -クライアントプラットフォームは、SSL クライアント証明書をサポートしている必要があります。 |

クライアント証明書を受け入れるように IIS を構成するには、IIS マネージャーを開き、次の手順を実行します。

1. ツリービューで [サイト] ノードをクリックします。
2. 中央のウィンドウで **[SSL 設定]** 機能をダブルクリックします。
3. **[クライアント証明書]** で、次のいずれかのオプションを選択します。 

    - **Accept**: IIS はクライアントからの証明書を受け入れますが、証明書は必要ありません。
    - **要求**: クライアント証明書が必要です。 (このオプションを有効にするには、[SSL が必要] も選択する必要があります)。

Applicationhost.config ファイルで次のオプションを設定することもできます。

[!code-xml[Main](working-with-ssl-in-web-api/samples/sample3.xml)]

**SslNegotiateCert**フラグは、iis がクライアントからの証明書を受け入れるが、iis マネージャーの "accept" オプションに相当するものを必要としないことを意味します。 証明書を要求するには、 **SslRequireCert**フラグを設定します。 テストの場合は、ローカルの applicationhost で IIS Express でこれらのオプションを設定することもできます。構成ファイル。 "Documents\IISExpress\config" にあります。

### <a name="creating-a-client-certificate-for-testing"></a>テスト用のクライアント証明書の作成

テストの目的で、 [MakeCert](/windows/desktop/SecCrypto/makecert)を使用してクライアント証明書を作成できます。 まず、テストルート証明機関を作成します。

[!code-console[Main](working-with-ssl-in-web-api/samples/sample4.cmd)]

Makecert は、秘密キーのパスワードの入力を求められます。

次に、次のように、テストサーバーの "信頼されたルート証明機関" ストアに証明書を追加します。

1. MMC を開きます。
2. **[ファイル]** で、 **[スナップインの追加と削除]** を選択します。
3. **[コンピューターアカウント]** を選択します。
4. **[ローカルコンピューター]** を選択し、ウィザードを完了します。
5. ナビゲーションウィンドウで、[信頼されたルート証明機関] ノードを展開します。
6. **[操作]** メニューの **[すべてのタスク]** をポイントし、 **[インポート]** をクリックして証明書のインポートウィザードを起動します。
7. 証明書ファイル TempCA .cer を参照します。
8. **[開く]** をクリックし、 **[次へ]** をクリックして、ウィザードを完了します。 (パスワードを再入力するように求められます)。

次に、最初の証明書で署名されたクライアント証明書を作成します。

[!code-console[Main](working-with-ssl-in-web-api/samples/sample5.cmd)]

### <a name="using-client-certificates-in-web-api"></a>Web API でのクライアント証明書の使用

サーバー側では、要求メッセージで[GetClientCertificate](https://msdn.microsoft.com/library/system.net.http.httprequestmessageextensions.getclientcertificate.aspx)を呼び出すことによって、クライアント証明書を取得できます。 クライアント証明書がない場合、メソッドは null を返します。 それ以外の場合は、 **X509Certificate2**インスタンスを返します。 発行者やサブジェクトなどの証明書から情報を取得するには、このオブジェクトを使用します。 その後、この情報を認証や承認に使用できます。

[!code-csharp[Main](working-with-ssl-in-web-api/samples/sample6.cs)]
