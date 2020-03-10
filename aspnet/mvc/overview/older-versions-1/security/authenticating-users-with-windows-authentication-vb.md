---
uid: mvc/overview/older-versions-1/security/authenticating-users-with-windows-authentication-vb
title: Windows 認証を使用してユーザーを認証する (VB) |Microsoft Docs
author: microsoft
description: MVC アプリケーションのコンテキストで Windows 認証を使用する方法について説明します。 アプリケーションの web co で Windows 認証を有効にする方法について説明します。
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 532fa051-7d5c-4d6d-87f6-339ce4b84c44
msc.legacyurl: /mvc/overview/older-versions-1/security/authenticating-users-with-windows-authentication-vb
msc.type: authoredcontent
ms.openlocfilehash: aa64b1f9ef6461a81611ca066310dca2d545baa3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78506242"
---
# <a name="authenticating-users-with-windows-authentication-vb"></a><span data-ttu-id="1c6a3-104">Windows 認証でユーザーを認証する (VB)</span><span class="sxs-lookup"><span data-stu-id="1c6a3-104">Authenticating Users with Windows Authentication (VB)</span></span>

<span data-ttu-id="1c6a3-105">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="1c6a3-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="1c6a3-106">MVC アプリケーションのコンテキストで Windows 認証を使用する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="1c6a3-106">Learn how to use Windows authentication in the context of an MVC application.</span></span> <span data-ttu-id="1c6a3-107">アプリケーションの web 構成ファイル内で Windows 認証を有効にする方法と、IIS で認証を構成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="1c6a3-107">You learn how to enable Windows authentication within your application's web configuration file and how to configure authentication with IIS.</span></span> <span data-ttu-id="1c6a3-108">最後に、[承認] 属性を使用して、特定の Windows ユーザーまたはグループに対するコントローラーアクションへのアクセスを制限する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="1c6a3-108">Finally, you learn how to use the [Authorize] attribute to restrict access to controller actions to particular Windows users or groups.</span></span>

<span data-ttu-id="1c6a3-109">このチュートリアルの目的は、MVC アプリケーションのビューをパスワードで保護するためにインターネットインフォメーションサービスに組み込まれているセキュリティ機能を活用する方法を説明することです。</span><span class="sxs-lookup"><span data-stu-id="1c6a3-109">The goal of this tutorial is to explain how you can take advantage of the security features built into Internet Information Services to password protect the views in your MVC applications.</span></span> <span data-ttu-id="1c6a3-110">特定の windows ユーザーまたは特定の Windows グループのメンバーであるユーザーのみがコントローラーアクションを呼び出せるようにする方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="1c6a3-110">You learn how to allow controller actions to be invoked only by particular Windows users or users who are members of particular Windows groups.</span></span>

<span data-ttu-id="1c6a3-111">社内の社内 web サイト (イントラネットサイト) を構築していて、ユーザーが web サイトにアクセスするときに標準の Windows ユーザー名とパスワードを使用できるようにする場合は、Windows 認証を使用するのが理にかなっています。</span><span class="sxs-lookup"><span data-stu-id="1c6a3-111">Using Windows authentication makes sense when you are building an internal company website (an intranet site) and you want your users to be able to use their standard Windows user names and passwords when accessing the website.</span></span> <span data-ttu-id="1c6a3-112">外部に接続する web サイト (インターネット web サイト) を構築する場合は、代わりにフォーム認証を使用することを検討してください。</span><span class="sxs-lookup"><span data-stu-id="1c6a3-112">If you are building an outwards facing website (an Internet website) consider using Forms authentication instead.</span></span>

#### <a name="enabling-windows-authentication"></a><span data-ttu-id="1c6a3-113">Windows 認証を有効にする</span><span class="sxs-lookup"><span data-stu-id="1c6a3-113">Enabling Windows Authentication</span></span>

<span data-ttu-id="1c6a3-114">新しい ASP.NET MVC アプリケーションを作成する場合、Windows 認証は既定では有効になっていません。</span><span class="sxs-lookup"><span data-stu-id="1c6a3-114">When you create a new ASP.NET MVC application, Windows authentication is not enabled by default.</span></span> <span data-ttu-id="1c6a3-115">フォーム認証は、MVC アプリケーションに対して有効になっている既定の認証の種類です。</span><span class="sxs-lookup"><span data-stu-id="1c6a3-115">Forms authentication is the default authentication type enabled for MVC applications.</span></span> <span data-ttu-id="1c6a3-116">MVC アプリケーションの web 構成 (web.config) ファイルを変更して、Windows 認証を有効にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="1c6a3-116">You must enable Windows authentication by modifying your MVC application's web configuration (web.config) file.</span></span> <span data-ttu-id="1c6a3-117">&lt;authentication&gt; セクションを見つけて、次のようなフォーム認証ではなく Windows を使用するように変更します。</span><span class="sxs-lookup"><span data-stu-id="1c6a3-117">Find the &lt;authentication&gt; section and modify it to use Windows instead of Forms authentication like this:</span></span>

[!code-xml[Main](authenticating-users-with-windows-authentication-vb/samples/sample1.xml)]

<span data-ttu-id="1c6a3-118">Windows 認証を有効にすると、web サーバーはユーザーの認証を担当します。</span><span class="sxs-lookup"><span data-stu-id="1c6a3-118">When you enable Windows authentication, your web server becomes responsible for authenticating users.</span></span> <span data-ttu-id="1c6a3-119">通常、ASP.NET MVC アプリケーションを作成してデプロイするときに使用する web サーバーには2種類あります。</span><span class="sxs-lookup"><span data-stu-id="1c6a3-119">Typically, there are two different types of web servers that you use when creating and deploying an ASP.NET MVC application.</span></span>

<span data-ttu-id="1c6a3-120">まず、MVC アプリケーションを開発するときに、Visual Studio に付属の ASP.NET Development Web サーバーを使用します。</span><span class="sxs-lookup"><span data-stu-id="1c6a3-120">First, while developing an MVC application, you use the ASP.NET Development Web Server included with Visual Studio.</span></span> <span data-ttu-id="1c6a3-121">既定では、ASP.NET Development Web サーバーは、Windows へのログインに使用したすべてのアカウントについて、現在の Windows アカウントのコンテキストですべてのページを実行します。</span><span class="sxs-lookup"><span data-stu-id="1c6a3-121">By default, the ASP.NET Development Web Server executes all pages in the context of the current Windows account (whatever account you used to log into Windows).</span></span>

<span data-ttu-id="1c6a3-122">ASP.NET Development Web サーバーは、NTLM 認証もサポートしています。</span><span class="sxs-lookup"><span data-stu-id="1c6a3-122">The ASP.NET Development Web Server also supports NTLM authentication.</span></span> <span data-ttu-id="1c6a3-123">NTLM 認証を有効にするには、[ソリューションエクスプローラー] ウィンドウでプロジェクトの名前を右クリックし、[プロパティ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="1c6a3-123">You can enable NTLM authentication by right-clicking the name of your project in the Solution Explorer window and selecting Properties.</span></span> <span data-ttu-id="1c6a3-124">次に、[Web] タブを選択し、[NTLM] チェックボックスをオンにします (図1を参照)。</span><span class="sxs-lookup"><span data-stu-id="1c6a3-124">Next, select the Web tab and check the NTLM checkbox (see Figure 1).</span></span>

<span data-ttu-id="1c6a3-125">**図 1: ASP.NET Development Web サーバーの NTLM 認証を有効にする**</span><span class="sxs-lookup"><span data-stu-id="1c6a3-125">**Figure 1 – Enabling NTLM authentication for the ASP.NET Development Web Server**</span></span>

![clip_image002](authenticating-users-with-windows-authentication-vb/_static/image1.jpg)

<span data-ttu-id="1c6a3-127">実稼働 web アプリケーションの場合は、IIS を web サーバーとして使用します。</span><span class="sxs-lookup"><span data-stu-id="1c6a3-127">For a production web application, on the hand, you use IIS as your web server.</span></span> <span data-ttu-id="1c6a3-128">IIS は次のようないくつかの種類の認証をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="1c6a3-128">IIS supports several types of authentication including:</span></span>

- <span data-ttu-id="1c6a3-129">基本認証-HTTP 1.0 プロトコルの一部として定義されます。</span><span class="sxs-lookup"><span data-stu-id="1c6a3-129">Basic Authentication – Defined as part of the HTTP 1.0 protocol.</span></span> <span data-ttu-id="1c6a3-130">インターネット経由でユーザー名とパスワードをクリアテキスト (Base64 エンコード) で送信します。</span><span class="sxs-lookup"><span data-stu-id="1c6a3-130">Sends user names and passwords in clear text (Base64 encoded) across the Internet.</span></span> <span data-ttu-id="1c6a3-131">-Digest 認証–パスワード自体ではなく、パスワードのハッシュをインターネット経由で送信します。</span><span class="sxs-lookup"><span data-stu-id="1c6a3-131">- Digest Authentication – Sends a hash of a password, instead of the password itself, across the internet.</span></span> <span data-ttu-id="1c6a3-132">-統合 Windows (NTLM) 認証– windows を使用してイントラネット環境で使用する最適な認証の種類。</span><span class="sxs-lookup"><span data-stu-id="1c6a3-132">- Integrated Windows (NTLM) Authentication – The best type of authentication to use in intranet environments using windows.</span></span> <span data-ttu-id="1c6a3-133">-証明書認証–クライアント側の証明書を使用した認証を有効にします。</span><span class="sxs-lookup"><span data-stu-id="1c6a3-133">- Certificate Authentication – Enables authentication using a client-side certificate.</span></span> <span data-ttu-id="1c6a3-134">証明書は Windows ユーザーアカウントにマップされます。</span><span class="sxs-lookup"><span data-stu-id="1c6a3-134">The certificate maps to a Windows user account.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="1c6a3-135">これらのさまざまな種類の認証の詳細については、「 [https://msdn.microsoft.com/library/aa292114(VS.71).aspx](https://msdn.microsoft.com/library/aa292114(VS.71).aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="1c6a3-135">For a more detailed overview of these different types of authentication, see [https://msdn.microsoft.com/library/aa292114(VS.71).aspx](https://msdn.microsoft.com/library/aa292114(VS.71).aspx).</span></span>

<span data-ttu-id="1c6a3-136">インターネットインフォメーションサービス Manager を使用して、特定の種類の認証を有効にすることができます。</span><span class="sxs-lookup"><span data-stu-id="1c6a3-136">You can use Internet Information Services Manager to enable a particular type of authentication.</span></span> <span data-ttu-id="1c6a3-137">すべての種類の認証は、すべてのオペレーティングシステムで使用できるわけではないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="1c6a3-137">Be aware that all types of authentication are not available in the case of every operating system.</span></span> <span data-ttu-id="1c6a3-138">さらに、Windows Vista で IIS 7.0 を使用している場合は、インターネットインフォメーションサービス Manager に表示する前に、さまざまな種類の Windows 認証を有効にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="1c6a3-138">Furthermore, if you are using IIS 7.0 with Windows Vista, you will need to enable the different types of Windows authentication before they appear in the Internet Information Services Manager.</span></span> <span data-ttu-id="1c6a3-139">[**コントロールパネル]、[プログラム]、[プログラムと機能] の順に開き、[Windows の機能の有効化または無効化**] を開き、[インターネットインフォメーションサービス] ノードを展開します (図2を参照)。</span><span class="sxs-lookup"><span data-stu-id="1c6a3-139">Open **Control Panel, Programs, Programs and Features, Turn Windows features on or off**, and expand the Internet Information Services node (see Figure 2).</span></span>

<span data-ttu-id="1c6a3-140">**図 2-Windows IIS 機能の有効化**</span><span class="sxs-lookup"><span data-stu-id="1c6a3-140">**Figure 2 – Enabling Windows IIS features**</span></span>

![clip_image004](authenticating-users-with-windows-authentication-vb/_static/image2.jpg)

<span data-ttu-id="1c6a3-142">インターネットインフォメーションサービスを使用すると、さまざまな種類の認証を有効または無効にすることができます。</span><span class="sxs-lookup"><span data-stu-id="1c6a3-142">Using Internet Information Services, you can enable or disable different types of authentication.</span></span> <span data-ttu-id="1c6a3-143">たとえば、図3は、IIS 7.0 を使用する場合に、匿名認証を無効にし、統合 Windows (NTLM) 認証を有効にする方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="1c6a3-143">For example, Figure 3 illustrates disabling anonymous authentication and enabling Integrated Windows (NTLM) authentication when using IIS 7.0.</span></span>

<span data-ttu-id="1c6a3-144">**図 3-統合 Windows 認証の有効化**</span><span class="sxs-lookup"><span data-stu-id="1c6a3-144">**Figure 3 – Enabling Integrated Windows Authentication**</span></span>

![clip_image006](authenticating-users-with-windows-authentication-vb/_static/image3.jpg)

#### <a name="authorizing-windows-users-and-groups"></a><span data-ttu-id="1c6a3-146">Windows ユーザーとグループの承認</span><span class="sxs-lookup"><span data-stu-id="1c6a3-146">Authorizing Windows Users and Groups</span></span>

<span data-ttu-id="1c6a3-147">Windows 認証を有効にした後、&lt;承認&gt; 属性を使用して、コントローラーまたはコントローラーアクションへのアクセスを制御できます。</span><span class="sxs-lookup"><span data-stu-id="1c6a3-147">After you enable Windows authentication, you can use the &lt;Authorize&gt; attribute to control access to controllers or controller actions.</span></span> <span data-ttu-id="1c6a3-148">この属性は、MVC コントローラー全体または特定のコントローラーアクションに適用できます。</span><span class="sxs-lookup"><span data-stu-id="1c6a3-148">This attribute can be applied to an entire MVC controller or a particular controller action.</span></span>

<span data-ttu-id="1c6a3-149">たとえば、リスト1のホームコントローラーでは、Index ()、企業秘密 ()、StephenSecrets () という3つのアクションが公開されています。</span><span class="sxs-lookup"><span data-stu-id="1c6a3-149">For example, the Home controller in Listing 1 exposes three actions named Index(), CompanySecrets(), and StephenSecrets().</span></span> <span data-ttu-id="1c6a3-150">すべてのユーザーが Index () アクションを呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="1c6a3-150">Anyone can invoke the Index() action.</span></span> <span data-ttu-id="1c6a3-151">ただし、会社のシークレット () アクションを呼び出すことができるのは、Windows ローカルマネージャーグループのメンバーだけです。</span><span class="sxs-lookup"><span data-stu-id="1c6a3-151">However, only members of the Windows local Managers group can invoke the CompanySecrets() action.</span></span> <span data-ttu-id="1c6a3-152">最後に、Stephen (Redmond ドメイン内) という名前の Windows ドメインユーザーのみが StephenSecrets () アクションを呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="1c6a3-152">Finally, only the Windows domain user named Stephen (in the Redmond domain) can invoke the StephenSecrets() action.</span></span>

<span data-ttu-id="1c6a3-153">**リスト1– Controllers\HomeController.vb**</span><span class="sxs-lookup"><span data-stu-id="1c6a3-153">**Listing 1 – Controllers\HomeController.vb**</span></span>

[!code-vb[Main](authenticating-users-with-windows-authentication-vb/samples/sample2.vb)]

> [!NOTE]
> <span data-ttu-id="1c6a3-154">Windows ユーザーアカウント制御 (UAC) のため、Windows Vista または Windows Server 2008 を使用する場合、ローカルの Administrators グループの動作は他のグループとは異なります。</span><span class="sxs-lookup"><span data-stu-id="1c6a3-154">Because of Windows User Account Control (UAC), when working with Windows Vista or Windows Server 2008, the local Administrators group will behave differently than other groups.</span></span> <span data-ttu-id="1c6a3-155">&lt;承認&gt; 属性は、コンピューターの UAC 設定を変更しない限り、ローカルの Administrators グループのメンバーを正しく認識しません。</span><span class="sxs-lookup"><span data-stu-id="1c6a3-155">The &lt;Authorize&gt; attribute won't correctly recognize a member of the local Administrators group unless you modify your computer's UAC settings.</span></span>

<span data-ttu-id="1c6a3-156">適切なアクセス許可がない状態でコントローラーアクションを呼び出そうとすると、有効になっている認証の種類によって、正確に発生します。</span><span class="sxs-lookup"><span data-stu-id="1c6a3-156">Exactly what happens when you attempt to invoke a controller action without being the right permissions depends on the type of authentication enabled.</span></span> <span data-ttu-id="1c6a3-157">既定では、ASP.NET 開発サーバーを使用すると、空白のページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="1c6a3-157">By default, when using the ASP.NET Development Server, you simply get a blank page.</span></span> <span data-ttu-id="1c6a3-158">ページには、401の**承認されていない**HTTP 応答ステータスが提供されます。</span><span class="sxs-lookup"><span data-stu-id="1c6a3-158">The page is served with a **401 Not Authorized** HTTP Response Status.</span></span>

<span data-ttu-id="1c6a3-159">一方、匿名認証を無効にし、基本認証を有効にした状態で IIS を使用している場合は、保護されたページを要求するたびにログインダイアログプロンプトが表示されます (図4を参照)。</span><span class="sxs-lookup"><span data-stu-id="1c6a3-159">If, on the other hand, you are using IIS with Anonymous authentication disabled and Basic authentication enabled, then you keep getting a login dialog prompt each time you request the protected page (see Figure 4).</span></span>

<span data-ttu-id="1c6a3-160">**図4–基本認証のログインダイアログ**</span><span class="sxs-lookup"><span data-stu-id="1c6a3-160">**Figure 4 – Basic authentication login dialog**</span></span>

![clip_image008](authenticating-users-with-windows-authentication-vb/_static/image4.jpg)

#### <a name="summary"></a><span data-ttu-id="1c6a3-162">まとめ</span><span class="sxs-lookup"><span data-stu-id="1c6a3-162">Summary</span></span>

<span data-ttu-id="1c6a3-163">このチュートリアルでは、ASP.NET MVC アプリケーションのコンテキストで Windows 認証を使用する方法について説明しました。</span><span class="sxs-lookup"><span data-stu-id="1c6a3-163">This tutorial explained how you can use Windows authentication in the context of an ASP.NET MVC application.</span></span> <span data-ttu-id="1c6a3-164">アプリケーションの web 構成ファイル内で Windows 認証を有効にする方法と、IIS で認証を構成する方法について学習しました。</span><span class="sxs-lookup"><span data-stu-id="1c6a3-164">You learned how to enable Windows authentication within your application's web configuration file and how to configure authentication with IIS.</span></span> <span data-ttu-id="1c6a3-165">最後に、&lt;承認&gt; 属性を使用して、特定の Windows ユーザーまたはグループに対するコントローラーアクションへのアクセスを制限する方法を学習しました。</span><span class="sxs-lookup"><span data-stu-id="1c6a3-165">Finally, you learned how to use the &lt;Authorize&gt; attribute to restrict access to controller actions to particular Windows users or groups.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="1c6a3-166">[前へ](authenticating-users-with-forms-authentication-vb.md)
> [次へ](preventing-javascript-injection-attacks-vb.md)</span><span class="sxs-lookup"><span data-stu-id="1c6a3-166">[Previous](authenticating-users-with-forms-authentication-vb.md)
[Next](preventing-javascript-injection-attacks-vb.md)</span></span>
