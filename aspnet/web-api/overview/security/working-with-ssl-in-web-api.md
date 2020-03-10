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
# <a name="working-with-ssl-in-web-api"></a><span data-ttu-id="ea15b-103">Web API での SSL の操作</span><span class="sxs-lookup"><span data-stu-id="ea15b-103">Working with SSL in Web API</span></span>

<span data-ttu-id="ea15b-104">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="ea15b-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="ea15b-105">いくつかの一般的な認証方式は、プレーンな HTTP を介してセキュリティで保護されていません。</span><span class="sxs-lookup"><span data-stu-id="ea15b-105">Several common authentication schemes are not secure over plain HTTP.</span></span> <span data-ttu-id="ea15b-106">具体的には、基本認証とフォーム認証で送信する資格情報が暗号化されません。</span><span class="sxs-lookup"><span data-stu-id="ea15b-106">In particular, Basic authentication and forms authentication send unencrypted credentials.</span></span> <span data-ttu-id="ea15b-107">セキュリティを確保するために、これらの認証方式では SSL を使用する*必要があり*ます。</span><span class="sxs-lookup"><span data-stu-id="ea15b-107">To be secure, these authentication schemes *must* use SSL.</span></span> <span data-ttu-id="ea15b-108">さらに、SSL クライアント証明書を使用してクライアントを認証することもできます。</span><span class="sxs-lookup"><span data-stu-id="ea15b-108">In addition, SSL client certificates can be used to authenticate clients.</span></span>

## <a name="enabling-ssl-on-the-server"></a><span data-ttu-id="ea15b-109">サーバーで SSL を有効にする</span><span class="sxs-lookup"><span data-stu-id="ea15b-109">Enabling SSL on the Server</span></span>

<span data-ttu-id="ea15b-110">IIS 7 以降で SSL を設定するには:</span><span class="sxs-lookup"><span data-stu-id="ea15b-110">To set up SSL in IIS 7 or later:</span></span>

- <span data-ttu-id="ea15b-111">証明書を作成または取得します。</span><span class="sxs-lookup"><span data-stu-id="ea15b-111">Create or get a certificate.</span></span> <span data-ttu-id="ea15b-112">テストの場合は、自己署名証明書を作成できます。</span><span class="sxs-lookup"><span data-stu-id="ea15b-112">For testing, you can create a self-signed certificate.</span></span>
- <span data-ttu-id="ea15b-113">HTTPS バインドを追加します。</span><span class="sxs-lookup"><span data-stu-id="ea15b-113">Add an HTTPS binding.</span></span>

<span data-ttu-id="ea15b-114">詳細については、「 [IIS 7 で SSL を設定する方法](https://www.iis.net/learn/manage/configuring-security/how-to-set-up-ssl-on-iis)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ea15b-114">For details, see [How to Set Up SSL on IIS 7](https://www.iis.net/learn/manage/configuring-security/how-to-set-up-ssl-on-iis).</span></span>

<span data-ttu-id="ea15b-115">ローカルテストでは、Visual Studio から IIS Express で SSL を有効にすることができます。</span><span class="sxs-lookup"><span data-stu-id="ea15b-115">For local testing, you can enable SSL in IIS Express from Visual Studio.</span></span> <span data-ttu-id="ea15b-116">プロパティウィンドウで、 **[SSL Enabled]** を**True**に設定します。</span><span class="sxs-lookup"><span data-stu-id="ea15b-116">In the Properties window, set **SSL Enabled** to **True**.</span></span> <span data-ttu-id="ea15b-117">**SSL URL**の値を確認します。この URL を使用して、HTTPS 接続をテストします。</span><span class="sxs-lookup"><span data-stu-id="ea15b-117">Note the value of **SSL URL**; use this URL for testing HTTPS connections.</span></span>

![](working-with-ssl-in-web-api/_static/image1.png)

### <a name="enforcing-ssl-in-a-web-api-controller"></a><span data-ttu-id="ea15b-118">Web API コントローラーでの SSL の適用</span><span class="sxs-lookup"><span data-stu-id="ea15b-118">Enforcing SSL in a Web API Controller</span></span>

<span data-ttu-id="ea15b-119">HTTPS と HTTP の両方のバインドがある場合でも、クライアントは引き続き HTTP を使用してサイトにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="ea15b-119">If you have both an HTTPS and an HTTP binding, clients can still use HTTP to access the site.</span></span> <span data-ttu-id="ea15b-120">HTTP を介して一部のリソースを使用できるようにする一方で、他のリソースには SSL が必要な場合があります。</span><span class="sxs-lookup"><span data-stu-id="ea15b-120">You might allow some resources to be available through HTTP, while other resources require SSL.</span></span> <span data-ttu-id="ea15b-121">その場合は、アクションフィルターを使用して、保護されたリソースに対して SSL を要求します。</span><span class="sxs-lookup"><span data-stu-id="ea15b-121">In that case, use an action filter to require SSL for the protected resources.</span></span> <span data-ttu-id="ea15b-122">次のコードは、SSL をチェックする Web API 認証フィルターを示しています。</span><span class="sxs-lookup"><span data-stu-id="ea15b-122">The following code shows a Web API authentication filter that checks for SSL:</span></span>

[!code-csharp[Main](working-with-ssl-in-web-api/samples/sample1.cs)]

<span data-ttu-id="ea15b-123">このフィルターを、SSL を必要とする Web API アクションすべてに追加します。</span><span class="sxs-lookup"><span data-stu-id="ea15b-123">Add this filter to any Web API actions that require SSL:</span></span>

[!code-csharp[Main](working-with-ssl-in-web-api/samples/sample2.cs)]

## <a name="ssl-client-certificates"></a><span data-ttu-id="ea15b-124">SSL クライアント証明書</span><span class="sxs-lookup"><span data-stu-id="ea15b-124">SSL Client Certificates</span></span>

<span data-ttu-id="ea15b-125">SSL は、公開キーインフラストラクチャ証明書を使用して認証を提供します。</span><span class="sxs-lookup"><span data-stu-id="ea15b-125">SSL provides authentication by using Public Key Infrastructure certificates.</span></span> <span data-ttu-id="ea15b-126">サーバーは、クライアントに対してサーバーを認証する証明書を提供する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ea15b-126">The server must provide a certificate that authenticates the server to the client.</span></span> <span data-ttu-id="ea15b-127">クライアントがサーバーに証明書を提供するのはあまり一般的ではありませんが、これはクライアントを認証するための1つのオプションです。</span><span class="sxs-lookup"><span data-stu-id="ea15b-127">It is less common for the client to provide a certificate to the server, but this is one option for authenticating clients.</span></span> <span data-ttu-id="ea15b-128">SSL でクライアント証明書を使用するには、署名入り証明書をユーザーに配布する方法が必要です。</span><span class="sxs-lookup"><span data-stu-id="ea15b-128">To use client certificates with SSL, you need a way to distribute signed certificates to your users.</span></span> <span data-ttu-id="ea15b-129">多くのアプリケーションの種類では、これは適切なユーザーエクスペリエンスではありませんが、環境によっては (たとえば、enterprise) 使用可能な場合があります。</span><span class="sxs-lookup"><span data-stu-id="ea15b-129">For many application types, this will not be a good user experience, but in some environments (for example, enterprise) it may be feasible.</span></span>

| <span data-ttu-id="ea15b-130">長所</span><span class="sxs-lookup"><span data-stu-id="ea15b-130">Advantages</span></span> | <span data-ttu-id="ea15b-131">短所</span><span class="sxs-lookup"><span data-stu-id="ea15b-131">Disadvantages</span></span> |
| --- | --- |
| <span data-ttu-id="ea15b-132">-証明書の資格情報は、ユーザー名/パスワードよりも強力です。</span><span class="sxs-lookup"><span data-stu-id="ea15b-132">- Certificate credentials are stronger than username/password.</span></span> <span data-ttu-id="ea15b-133">-SSL は、認証、メッセージの整合性、およびメッセージの暗号化を使用して、完全なセキュリティで保護されたチャネルを提供します。</span><span class="sxs-lookup"><span data-stu-id="ea15b-133">- SSL provides a complete secure channel, with authentication, message integrity, and message encryption.</span></span> | <span data-ttu-id="ea15b-134">-PKI 証明書を取得して管理する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ea15b-134">- You must obtain and manage PKI certificates.</span></span> <span data-ttu-id="ea15b-135">-クライアントプラットフォームは、SSL クライアント証明書をサポートしている必要があります。</span><span class="sxs-lookup"><span data-stu-id="ea15b-135">- The client platform must support SSL client certificates.</span></span> |

<span data-ttu-id="ea15b-136">クライアント証明書を受け入れるように IIS を構成するには、IIS マネージャーを開き、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="ea15b-136">To configure IIS to accept client certificates, open IIS Manager and perform the following steps:</span></span>

1. <span data-ttu-id="ea15b-137">ツリービューで [サイト] ノードをクリックします。</span><span class="sxs-lookup"><span data-stu-id="ea15b-137">Click the site node in the tree view.</span></span>
2. <span data-ttu-id="ea15b-138">中央のウィンドウで **[SSL 設定]** 機能をダブルクリックします。</span><span class="sxs-lookup"><span data-stu-id="ea15b-138">Double-click the **SSL Settings** feature in the middle pane.</span></span>
3. <span data-ttu-id="ea15b-139">**[クライアント証明書]** で、次のいずれかのオプションを選択します。</span><span class="sxs-lookup"><span data-stu-id="ea15b-139">Under **Client Certificates**, select one of these options:</span></span> 

    - <span data-ttu-id="ea15b-140">**Accept**: IIS はクライアントからの証明書を受け入れますが、証明書は必要ありません。</span><span class="sxs-lookup"><span data-stu-id="ea15b-140">**Accept**: IIS will accept a certificate from the client, but does not require one.</span></span>
    - <span data-ttu-id="ea15b-141">**要求**: クライアント証明書が必要です。</span><span class="sxs-lookup"><span data-stu-id="ea15b-141">**Require**: Require a client certificate.</span></span> <span data-ttu-id="ea15b-142">(このオプションを有効にするには、[SSL が必要] も選択する必要があります)。</span><span class="sxs-lookup"><span data-stu-id="ea15b-142">(To enable this option, you must also select "Require SSL")</span></span>

<span data-ttu-id="ea15b-143">Applicationhost.config ファイルで次のオプションを設定することもできます。</span><span class="sxs-lookup"><span data-stu-id="ea15b-143">You can also set these options in the ApplicationHost.config file:</span></span>

[!code-xml[Main](working-with-ssl-in-web-api/samples/sample3.xml)]

<span data-ttu-id="ea15b-144">**SslNegotiateCert**フラグは、iis がクライアントからの証明書を受け入れるが、iis マネージャーの "accept" オプションに相当するものを必要としないことを意味します。</span><span class="sxs-lookup"><span data-stu-id="ea15b-144">The **SslNegotiateCert** flag means IIS will accept a certificate from the client, but does not require one (equivalent to the "Accept" option in IIS Manager).</span></span> <span data-ttu-id="ea15b-145">証明書を要求するには、 **SslRequireCert**フラグを設定します。</span><span class="sxs-lookup"><span data-stu-id="ea15b-145">To require a certificate, set the **SslRequireCert** flag.</span></span> <span data-ttu-id="ea15b-146">テストの場合は、ローカルの applicationhost で IIS Express でこれらのオプションを設定することもできます。構成ファイル。 "Documents\IISExpress\config" にあります。</span><span class="sxs-lookup"><span data-stu-id="ea15b-146">For testing, you can also set these options in IIS Express, in the local applicationhost.Config file, located in "Documents\IISExpress\config".</span></span>

### <a name="creating-a-client-certificate-for-testing"></a><span data-ttu-id="ea15b-147">テスト用のクライアント証明書の作成</span><span class="sxs-lookup"><span data-stu-id="ea15b-147">Creating a Client Certificate for Testing</span></span>

<span data-ttu-id="ea15b-148">テストの目的で、 [MakeCert](/windows/desktop/SecCrypto/makecert)を使用してクライアント証明書を作成できます。</span><span class="sxs-lookup"><span data-stu-id="ea15b-148">For testing purposes, you can use [MakeCert.exe](/windows/desktop/SecCrypto/makecert) to create a client certificate.</span></span> <span data-ttu-id="ea15b-149">まず、テストルート証明機関を作成します。</span><span class="sxs-lookup"><span data-stu-id="ea15b-149">First, create a test root authority:</span></span>

[!code-console[Main](working-with-ssl-in-web-api/samples/sample4.cmd)]

<span data-ttu-id="ea15b-150">Makecert は、秘密キーのパスワードの入力を求められます。</span><span class="sxs-lookup"><span data-stu-id="ea15b-150">Makecert will prompt you to enter a password for the private key.</span></span>

<span data-ttu-id="ea15b-151">次に、次のように、テストサーバーの "信頼されたルート証明機関" ストアに証明書を追加します。</span><span class="sxs-lookup"><span data-stu-id="ea15b-151">Next, add the certificate to the test server's "Trusted Root Certification Authorities" store, as follows:</span></span>

1. <span data-ttu-id="ea15b-152">MMC を開きます。</span><span class="sxs-lookup"><span data-stu-id="ea15b-152">Open MMC.</span></span>
2. <span data-ttu-id="ea15b-153">**[ファイル]** で、 **[スナップインの追加と削除]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="ea15b-153">Under **File**, select **Add/Remove Snap-In**.</span></span>
3. <span data-ttu-id="ea15b-154">**[コンピューターアカウント]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="ea15b-154">Select **Computer Account**.</span></span>
4. <span data-ttu-id="ea15b-155">**[ローカルコンピューター]** を選択し、ウィザードを完了します。</span><span class="sxs-lookup"><span data-stu-id="ea15b-155">Select **Local computer** and complete the wizard.</span></span>
5. <span data-ttu-id="ea15b-156">ナビゲーションウィンドウで、[信頼されたルート証明機関] ノードを展開します。</span><span class="sxs-lookup"><span data-stu-id="ea15b-156">Under the navigation pane, expand the "Trusted Root Certification Authorities" node.</span></span>
6. <span data-ttu-id="ea15b-157">**[操作]** メニューの **[すべてのタスク]** をポイントし、 **[インポート]** をクリックして証明書のインポートウィザードを起動します。</span><span class="sxs-lookup"><span data-stu-id="ea15b-157">On the **Action** menu, point to **All Tasks**, and then click **Import** to start the Certificate Import Wizard.</span></span>
7. <span data-ttu-id="ea15b-158">証明書ファイル TempCA .cer を参照します。</span><span class="sxs-lookup"><span data-stu-id="ea15b-158">Browse to the certificate file, TempCA.cer.</span></span>
8. <span data-ttu-id="ea15b-159">**[開く]** をクリックし、 **[次へ]** をクリックして、ウィザードを完了します。</span><span class="sxs-lookup"><span data-stu-id="ea15b-159">Click **Open**, then click **Next** and complete the wizard.</span></span> <span data-ttu-id="ea15b-160">(パスワードを再入力するように求められます)。</span><span class="sxs-lookup"><span data-stu-id="ea15b-160">(You will be prompted to re-enter the password.)</span></span>

<span data-ttu-id="ea15b-161">次に、最初の証明書で署名されたクライアント証明書を作成します。</span><span class="sxs-lookup"><span data-stu-id="ea15b-161">Now create a client certificate that is signed by the first certificate:</span></span>

[!code-console[Main](working-with-ssl-in-web-api/samples/sample5.cmd)]

### <a name="using-client-certificates-in-web-api"></a><span data-ttu-id="ea15b-162">Web API でのクライアント証明書の使用</span><span class="sxs-lookup"><span data-stu-id="ea15b-162">Using Client Certificates in Web API</span></span>

<span data-ttu-id="ea15b-163">サーバー側では、要求メッセージで[GetClientCertificate](https://msdn.microsoft.com/library/system.net.http.httprequestmessageextensions.getclientcertificate.aspx)を呼び出すことによって、クライアント証明書を取得できます。</span><span class="sxs-lookup"><span data-stu-id="ea15b-163">On the server side, you can get the client certificate by calling [GetClientCertificate](https://msdn.microsoft.com/library/system.net.http.httprequestmessageextensions.getclientcertificate.aspx) on the request message.</span></span> <span data-ttu-id="ea15b-164">クライアント証明書がない場合、メソッドは null を返します。</span><span class="sxs-lookup"><span data-stu-id="ea15b-164">The method returns null if there is no client certificate.</span></span> <span data-ttu-id="ea15b-165">それ以外の場合は、 **X509Certificate2**インスタンスを返します。</span><span class="sxs-lookup"><span data-stu-id="ea15b-165">Otherwise, it returns an **X509Certificate2** instance.</span></span> <span data-ttu-id="ea15b-166">発行者やサブジェクトなどの証明書から情報を取得するには、このオブジェクトを使用します。</span><span class="sxs-lookup"><span data-stu-id="ea15b-166">Use this object to get information from the certificate, such as the issuer and subject.</span></span> <span data-ttu-id="ea15b-167">その後、この情報を認証や承認に使用できます。</span><span class="sxs-lookup"><span data-stu-id="ea15b-167">Then you can use this information for authentication and/or authorization.</span></span>

[!code-csharp[Main](working-with-ssl-in-web-api/samples/sample6.cs)]
