---
uid: web-pages/overview/testing-and-debugging/aspnet-web-pages-razor-troubleshooting-guide
title: ASP.NET Web ページ (Razor) トラブルシューティングガイド |Microsoft Docs
author: Rick-Anderson
description: この記事では、ASP.NET Web ページ (Razor) といくつかの提案された解決策を使用する場合に発生する可能性がある問題について説明します。 ソフトウェアバージョン ASP.NET Web Pag...
ms.author: riande
ms.date: 02/10/2014
ms.assetid: 2a2c1833-0bfe-4e2e-9cc0-341b52c7b121
msc.legacyurl: /web-pages/overview/testing-and-debugging/aspnet-web-pages-razor-troubleshooting-guide
msc.type: authoredcontent
ms.openlocfilehash: fc03767c16f46c1e282d24ee3a7df2409a7c38bb
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78473380"
---
# <a name="aspnet-web-pages-razor-troubleshooting-guide"></a><span data-ttu-id="a327c-104">ASP.NET Web Pages (Razor) トラブルシューティング ガイド (英語)</span><span class="sxs-lookup"><span data-stu-id="a327c-104">ASP.NET Web Pages (Razor) Troubleshooting Guide</span></span>

<span data-ttu-id="a327c-105">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="a327c-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="a327c-106">この記事では、ASP.NET Web ページ (Razor) といくつかの提案された解決策を使用する場合に発生する可能性がある問題について説明します。</span><span class="sxs-lookup"><span data-stu-id="a327c-106">This article describes issues that you might have when working with ASP.NET Web Pages (Razor) and some suggested solutions.</span></span>
> 
> ## <a name="software-versions"></a><span data-ttu-id="a327c-107">ソフトウェアのバージョン</span><span class="sxs-lookup"><span data-stu-id="a327c-107">Software versions</span></span>
> 
> 
> - <span data-ttu-id="a327c-108">ASP.NET Web ページ (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="a327c-108">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="a327c-109">このチュートリアルは ASP.NET Web ページ2および ASP.NET Web ページ1.0 でも動作します。</span><span class="sxs-lookup"><span data-stu-id="a327c-109">This tutorial also works with ASP.NET Web Pages 2 and ASP.NET Web Pages 1.0.</span></span>

<span data-ttu-id="a327c-110">このトピックには、次のセクションが含まれます。</span><span class="sxs-lookup"><span data-stu-id="a327c-110">This topic contains the following sections:</span></span>

- [<span data-ttu-id="a327c-111">実行中のページに関する問題</span><span class="sxs-lookup"><span data-stu-id="a327c-111">Issues with Running Pages</span></span>](#Issues_Running_.cshtml_Pages)
- [<span data-ttu-id="a327c-112">Razor コードに関する問題</span><span class="sxs-lookup"><span data-stu-id="a327c-112">Issues with Razor Code</span></span>](#IssuesWithRazorCode)
- [<span data-ttu-id="a327c-113">セキュリティとメンバーシップに関する問題</span><span class="sxs-lookup"><span data-stu-id="a327c-113">Issues with Security and Membership</span></span>](#membership)
- [<span data-ttu-id="a327c-114">電子メールの送信に関する問題</span><span class="sxs-lookup"><span data-stu-id="a327c-114">Issues with Sending Email</span></span>](#email)
- [<span data-ttu-id="a327c-115">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="a327c-115">Additional Resources</span></span>](#AdditionalResources)

<span data-ttu-id="a327c-116">一般的な質問については、「 [ASP.NET Web ページ (Razor)](https://go.microsoft.com/fwlink/?LinkId=253000)に関する FAQ」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a327c-116">For general questions, see [ASP.NET Web Pages (Razor) FAQ](https://go.microsoft.com/fwlink/?LinkId=253000).</span></span>

<a id="Issues_Running_.cshtml_Pages"></a>
## <a name="issues-with-running-pages"></a><span data-ttu-id="a327c-117">実行中のページに関する問題</span><span class="sxs-lookup"><span data-stu-id="a327c-117">Issues with Running Pages</span></span>

<span data-ttu-id="a327c-118">さまざまな問題により、 *cshtml*および*vbhtml*ページが正常に実行されない可能性があります。</span><span class="sxs-lookup"><span data-stu-id="a327c-118">A variety of issues can prevent *.cshtml* and *.vbhtml* pages from running properly.</span></span> <span data-ttu-id="a327c-119">ここでは、一般的なエラーメッセージと考えられる原因を示します。</span><span class="sxs-lookup"><span data-stu-id="a327c-119">This section lists common error messages and likely causes.</span></span>

### <a name="http-error-403---forbidden-access-is-denied"></a><span data-ttu-id="a327c-120">HTTP エラー 403-許可されていません: アクセスが拒否されました</span><span class="sxs-lookup"><span data-stu-id="a327c-120">HTTP Error 403 - Forbidden: Access is denied</span></span>

<span data-ttu-id="a327c-121">*指定した資格情報を使用して、このディレクトリまたはページを表示するアクセス許可がありません。*</span><span class="sxs-lookup"><span data-stu-id="a327c-121">*You do not have permission to view this directory or page using the credentials that you supplied.*</span></span>

<span data-ttu-id="a327c-122">このエラーは、サーバーで正しいバージョンの .NET Framework が実行されていない場合に発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="a327c-122">This error can occur if the server is not running the correct version of the .NET Framework.</span></span> <span data-ttu-id="a327c-123">サーバー (ローカルまたはリモート) を実行しているコンピューターに、少なくとも .NET Framework 4 がインストールされていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="a327c-123">Make sure that the computer that's running the server (locally or remotely) has at least the .NET Framework 4 installed.</span></span> <span data-ttu-id="a327c-124">また、アプリケーション自体が適切なバージョンを実行するように構成されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="a327c-124">Also make sure that the application itself is configured to run the right version.</span></span>

<span data-ttu-id="a327c-125">WebMatrix での作業中にこの問題がローカルに表示される場合は、**サイト**ワークスペースをクリックし、treeview で **[設定]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="a327c-125">If you see this problem locally while working in WebMatrix, click the **Site** workspace, and then in the treeview click **Settings**.</span></span> <span data-ttu-id="a327c-126">**[.NET Framework バージョンの選択**] ボックスの一覧で、 **[.Net 4 (統合)]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="a327c-126">In the **Select .NET Framework Version** list, select **.NET 4 (Integrated)**.</span></span> <span data-ttu-id="a327c-127">このバージョンが既に設定されている場合は、管理者として WebMatrix を実行してみてください。</span><span class="sxs-lookup"><span data-stu-id="a327c-127">If this version is already set, try running WebMatrix as an administrator.</span></span>

<span data-ttu-id="a327c-128">Web サイトのルートに少なくとも1つの*cshtml*ファイルがあることを確認します。</span><span class="sxs-lookup"><span data-stu-id="a327c-128">Make sure that the root of your website has at least one *.cshtml* file in it.</span></span>

<span data-ttu-id="a327c-129">Web サーバーがリモートサーバー上にあるときにこのエラーが表示される場合は、サーバー管理者に問い合わせてください。</span><span class="sxs-lookup"><span data-stu-id="a327c-129">If you see this error when the web server is on a remote server, contact the server administrator.</span></span> <span data-ttu-id="a327c-130">サーバーに .NET Framework 4 以降がインストールされていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="a327c-130">Make sure that the server has the .NET Framework 4 or later installed.</span></span> <span data-ttu-id="a327c-131">また、そのバージョンの the.NET Framework を使用するように構成されたアプリケーションプールでアプリケーションが実行されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="a327c-131">Also make sure that the application is running in an application pool that's configured to use that version of the.NET Framework.</span></span>

<span data-ttu-id="a327c-132">サーバーを制御している場合は、正しいバージョンの .NET Framework が実行されていることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="a327c-132">If you have control over the server, make sure it's running the correct version of the .NET Framework.</span></span> <span data-ttu-id="a327c-133">`aspnet_regiis -iru` のコマンドを実行して、インストールの修復を試みることもできます。</span><span class="sxs-lookup"><span data-stu-id="a327c-133">You might also try repairing the installation by running the `aspnet_regiis -iru` command.</span></span> <span data-ttu-id="a327c-134">(たとえば、.NET Framework をインストールした後に IIS をインストールした場合、IIS は ASP.NET ページを実行するように正しく構成されません)。詳細については、「 [ASP.NET IIS Registration Tool (Aspnet\_iis 登録ツール)](https://msdn.microsoft.com/library/k6h9cz8h(v=vs.100).aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a327c-134">(For example, if you install IIS after you install the .NET Framework, IIS will not be correctly configured to run ASP.NET pages.) For more information, see [ASP.NET IIS Registration Tool (Aspnet\_regiis.exe)](https://msdn.microsoft.com/library/k6h9cz8h(v=vs.100).aspx).</span></span>

### <a name="http-error-40314---forbidden"></a><span data-ttu-id="a327c-135">HTTP エラー 403.14-許可されていません</span><span class="sxs-lookup"><span data-stu-id="a327c-135">HTTP Error 403.14 - Forbidden</span></span>

<span data-ttu-id="a327c-136">*Web サーバーは、このディレクトリの内容を一覧表示しないように構成されています。*</span><span class="sxs-lookup"><span data-stu-id="a327c-136">*The Web server is configured to not list the contents of this directory.*</span></span>

<span data-ttu-id="a327c-137">このエラー*は、保護*されているリソース (web.config ファイルなど) を要求した場合、または保護されているフォルダー ( *app\_データ*や*アプリ\_コード*など) にある場合に発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="a327c-137">This error can occur if you request a resource that's protected (like the *Web.config* file) or that's in a folder that's protected (like *App\_Data* or *App\_Code*).</span></span>

### <a name="http-error-40417---not-found"></a><span data-ttu-id="a327c-138">HTTP エラー 404.17-見つかりません</span><span class="sxs-lookup"><span data-stu-id="a327c-138">HTTP Error 404.17 - Not Found</span></span>

<span data-ttu-id="a327c-139">*要求されたコンテンツはスクリプトであり、静的ファイルハンドラーによって処理されません。*</span><span class="sxs-lookup"><span data-stu-id="a327c-139">*The requested content appears to be script and will not be served by the static file handler.*</span></span>

<span data-ttu-id="a327c-140">このエラーは、サーバーが .NET Framework 4 以降を使用するように正しく構成されていないために、`@{ }` ブロックのコードを認識しない場合に発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="a327c-140">This error can occur if the server is not configured correctly to use the .NET Framework 4 or later, and therefore does not recognize the code in `@{ }` blocks.</span></span> <span data-ttu-id="a327c-141">前の「 *HTTP エラー 403-許可されていません: アクセスが拒否されまし*た」の説明を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a327c-141">See the description earlier for *HTTP Error 403 - Forbidden: Access is denied*.</span></span>

### <a name="http-error-4047---not-found"></a><span data-ttu-id="a327c-142">HTTP エラー 404.7-見つかりません</span><span class="sxs-lookup"><span data-stu-id="a327c-142">HTTP Error 404.7 - Not Found</span></span>

<span data-ttu-id="a327c-143">*要求フィルターモジュールは、ファイル拡張子を拒否するように構成されています*</span><span class="sxs-lookup"><span data-stu-id="a327c-143">*The request filtering module is configured to deny the file extension*</span></span>

<span data-ttu-id="a327c-144">このエラーは、サーバーで*cshtml*または*vbhtml*拡張子が明示的にブロックされている場合に発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="a327c-144">This error can occur if *.cshtml* or *.vbhtml* extensions have been explicitly blocked on the server.</span></span> <span data-ttu-id="a327c-145">この問題が発生するのは、拡張子が含まれていない Url は機能しますが、拡張子が*cshtml*または*vbhtml*の url は機能しないということです。</span><span class="sxs-lookup"><span data-stu-id="a327c-145">A symptom of this problem is that URLs work when they do not include the extension, but URLs that include *.cshtml* or *.vbhtml* do not work.</span></span> <span data-ttu-id="a327c-146">解決策として、サイトの*web.config*ファイルにある拡張機能を再度有効にすることが考えられます。</span><span class="sxs-lookup"><span data-stu-id="a327c-146">A possible solution is to re-enable the extensions in the site's *Web.config* file.</span></span> <span data-ttu-id="a327c-147">次の例は、拡張子を有効にする方法を示し*ています*。</span><span class="sxs-lookup"><span data-stu-id="a327c-147">The following example shows how to enable the *.cshtml* extension.</span></span>

[!code-xml[Main](aspnet-web-pages-razor-troubleshooting-guide/samples/sample1.xml?highlight=5-6)]

### <a name="http-error-4048---not-found"></a><span data-ttu-id="a327c-148">HTTP エラー 404.8-見つかりません</span><span class="sxs-lookup"><span data-stu-id="a327c-148">HTTP Error 404.8 - Not Found</span></span>

<span data-ttu-id="a327c-149">*要求フィルターモジュールは、hiddenSegment セクションを含む URL 内のパスを拒否するように構成されています。*</span><span class="sxs-lookup"><span data-stu-id="a327c-149">*The request filtering module is configured to deny a path in the URL that contains a hiddenSegment section.*</span></span>

<span data-ttu-id="a327c-150">このエラー*は、保護*されているリソース (web.config ファイルなど) を要求した場合、または保護されているフォルダー ( *app\_データ*や*アプリ\_コード*など) にある場合に発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="a327c-150">This error can occur if you request a resource that's protected (like the *Web.config* file) or that's in a folder that's protected (like *App\_Data* or *App\_Code*).</span></span>

### <a name="this-type-of-page-is-not-served-server-error-in--application"></a><span data-ttu-id="a327c-151">この種類のページは提供されていません ('/' アプリケーションのサーバーエラー)</span><span class="sxs-lookup"><span data-stu-id="a327c-151">This type of page is not served (Server Error in '/' Application)</span></span>

<span data-ttu-id="a327c-152">HTTP エラー404.17 については、前述の説明を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a327c-152">See the description earlier for HTTP Error 404.17.</span></span>

<a id="IssuesWithRazorCode"></a>
## <a name="issues-with-razor-code"></a><span data-ttu-id="a327c-153">Razor コードに関する問題</span><span class="sxs-lookup"><span data-stu-id="a327c-153">Issues with Razor code</span></span>

### <a name="the-name-class-does-not-exist-in-the-current-context"></a><span data-ttu-id="a327c-154">名前 '*class*' は現在のコンテキストに存在しません</span><span class="sxs-lookup"><span data-stu-id="a327c-154">The name '*class*' does not exist in the current context</span></span>

<span data-ttu-id="a327c-155">多くの場合、このエラーが表示される理由は、`class` がヘルパーを参照するが、ヘルパーがインストールされていないことです。</span><span class="sxs-lookup"><span data-stu-id="a327c-155">Often, a reason you see this error is that `class` references a helper, but the helper is not installed.</span></span> <span data-ttu-id="a327c-156">たとえば、ヘルパーを使用しようとしても、NuGet からパッケージをインストールしていない場合は、このエラーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="a327c-156">For example, if you try to use a helper, but if you haven't installed the package from NuGet, you'll see this error.</span></span> <span data-ttu-id="a327c-157">WebMatrix のギャラリーを使用して、ヘルパーを検索してインストールします。</span><span class="sxs-lookup"><span data-stu-id="a327c-157">Use the Gallery in WebMatrix to find and install the helper.</span></span>

<span data-ttu-id="a327c-158">ヘルパーがインストールされていても、ページがそれを認識しない場合は、`using` ステートメントをコードに追加してみてください。</span><span class="sxs-lookup"><span data-stu-id="a327c-158">If the helper is installed, but the page still doesn't recognize it, try adding add a `using` statement to the code.</span></span> <span data-ttu-id="a327c-159">`using` ステートメントで、ヘルパーを含む名前空間を参照します。</span><span class="sxs-lookup"><span data-stu-id="a327c-159">In the `using` statement, reference the namespace that includes the helper.</span></span> <span data-ttu-id="a327c-160">たとえば、ASP.NET Web ヘルパーパッケージに含まれる基本的なヘルパーは、`System.Web.Helpers` 名前空間にあります。</span><span class="sxs-lookup"><span data-stu-id="a327c-160">For example, the basic helpers that are in the ASP.NET Web Helpers package are in the `System.Web.Helpers` namespace.</span></span> <span data-ttu-id="a327c-161">ヘルパーを使用するページの先頭に、次の行を追加します。</span><span class="sxs-lookup"><span data-stu-id="a327c-161">At the top of the page where you want to use the helper, add this line:</span></span>

`@using Microsoft.Web.Helpers;`

<a id="membership"></a>
## <a name="issues-with-security-and-membership"></a><span data-ttu-id="a327c-162">セキュリティとメンバーシップに関する問題</span><span class="sxs-lookup"><span data-stu-id="a327c-162">Issues with Security and Membership</span></span>

<span data-ttu-id="a327c-163">ASP.NET Web ページ (Razor) で組み込みのセキュリティ (メンバーシップ) システムを使用している場合は、次の問題が発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="a327c-163">If you are using the built-in security (membership) system in ASP.NET Web Pages (Razor), you might encounter the following issues.</span></span>

### <a name="to-call-this-method-the-membershipprovider-property-must-be-an-instance-of-extendedmembershipprovider"></a><span data-ttu-id="a327c-164">このメソッドを呼び出すには、"ExtendedMembershipProvider" プロパティが "" のインスタンスである必要があります。</span><span class="sxs-lookup"><span data-stu-id="a327c-164">To call this method, the "Membership.Provider" property must be an instance of "ExtendedMembershipProvider"</span></span>

<span data-ttu-id="a327c-165">このエラーは、`AspNetSqlMembershipProvider` クラスが構成されていないことを示している可能性があります。</span><span class="sxs-lookup"><span data-stu-id="a327c-165">This error can indicate that no `AspNetSqlMembershipProvider` class is configured.</span></span> <span data-ttu-id="a327c-166">(症状として、サイトはローカルで正常に動作しますが、ホスティングプロバイダーのサーバーに公開すると、このエラーがスローされます)。この問題の解決策の1つは、サイトの*web.config*ファイルに次の内容を追加して単純なメンバーシップを明示的に有効にすることです。</span><span class="sxs-lookup"><span data-stu-id="a327c-166">(A symptom is that the site works fine locally but throws this error when you publish it to a hosting provider's server.) One fix for this problem is to explicitly enable simple membership by adding the following to the site's *Web.config* file:</span></span>

[!code-xml[Main](aspnet-web-pages-razor-troubleshooting-guide/samples/sample2.xml?highlight=6)]

<a id="email"></a>
## <a name="issues-with-sending-email"></a><span data-ttu-id="a327c-167">電子メールの送信に関する問題</span><span class="sxs-lookup"><span data-stu-id="a327c-167">Issues with Sending Email</span></span>

<span data-ttu-id="a327c-168">電子メールの送信に問題があると、デバッグが困難になることがあります。</span><span class="sxs-lookup"><span data-stu-id="a327c-168">Problems with sending email can be challenging to debug.</span></span> <span data-ttu-id="a327c-169">最初の問題は、SMTP サーバーに接続できないことです。</span><span class="sxs-lookup"><span data-stu-id="a327c-169">An initial problem can be that you can't connect to the SMTP server.</span></span> <span data-ttu-id="a327c-170">接続に成功した場合、ASP.NET はメッセージを SMTP サーバーに渡します。</span><span class="sxs-lookup"><span data-stu-id="a327c-170">If the connection is successful, ASP.NET hands the message off to the SMTP server.</span></span> <span data-ttu-id="a327c-171">ただし、メッセージ自体には、SMTP サーバーから送信されないという問題があります。</span><span class="sxs-lookup"><span data-stu-id="a327c-171">However, there can be problems with the message itself that prevents the SMTP server from sending it.</span></span>

<span data-ttu-id="a327c-172">アプリケーションが電子メールを正常に送信できない場合は、次のことを試してください。</span><span class="sxs-lookup"><span data-stu-id="a327c-172">If your application does not successfully send email, try the following:</span></span>

- <span data-ttu-id="a327c-173">SMTP サーバー名は、多くの場合 `smtp.provider.com` や `smtp.provider.net`のようなものです。</span><span class="sxs-lookup"><span data-stu-id="a327c-173">The SMTP server name is often something like `smtp.provider.com` or `smtp.provider.net`.</span></span> <span data-ttu-id="a327c-174">ただし、サイトをホスティングプロバイダーに発行する場合、その時点での SMTP サーバー名が `localhost`可能性があります。</span><span class="sxs-lookup"><span data-stu-id="a327c-174">However, if you publish your site to a hosting provider, the SMTP server name at that point might be `localhost`.</span></span> <span data-ttu-id="a327c-175">この状況は、発行後にサイトがプロバイダーのサーバーで実行されている場合に発生します。そのため、SMTP サーバーは、アプリケーションの観点からローカルに配置されている可能性があります。</span><span class="sxs-lookup"><span data-stu-id="a327c-175">This situation occurs because after you've published and your site is running on the provider's server, the SMTP server might be local from the perspective of your application.</span></span> <span data-ttu-id="a327c-176">このようにサーバー名を変更すると、発行プロセスの一部として SMTP サーバー名を変更する必要があるということが考えられます。</span><span class="sxs-lookup"><span data-stu-id="a327c-176">This change in server names might mean that you have to change the SMTP server name as part of your publishing process.</span></span>
- <span data-ttu-id="a327c-177">ポート番号は通常25です。</span><span class="sxs-lookup"><span data-stu-id="a327c-177">The port number is usually 25.</span></span> <span data-ttu-id="a327c-178">ただし、一部のプロバイダーでは、ポート587またはその他のポートを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a327c-178">However, some providers require you to use port 587 or some other port.</span></span> <span data-ttu-id="a327c-179">使用するポート番号を SMTP サーバーの所有者に確認してください。</span><span class="sxs-lookup"><span data-stu-id="a327c-179">Check with the owner of the SMTP server what port number they expect you to use.</span></span>
- <span data-ttu-id="a327c-180">適切な資格情報を使用していることを確認します。</span><span class="sxs-lookup"><span data-stu-id="a327c-180">Make sure that you use the right credentials.</span></span> <span data-ttu-id="a327c-181">サイトをホスティングプロバイダーに発行した場合は、プロバイダーが特別に指定した資格情報を電子メール用に使用します。</span><span class="sxs-lookup"><span data-stu-id="a327c-181">If you've published your site to a hosting provider, use the credentials that the provider has specifically indicated are for email.</span></span> <span data-ttu-id="a327c-182">これらの資格情報は、発行に使用する資格情報とは異なる場合があります。</span><span class="sxs-lookup"><span data-stu-id="a327c-182">These credentials might be different from the credentials you use to publish.</span></span>
- <span data-ttu-id="a327c-183">場合によっては、資格情報をまったく必要としません。</span><span class="sxs-lookup"><span data-stu-id="a327c-183">Sometimes you don't need credentials at all.</span></span> <span data-ttu-id="a327c-184">個人用 ISP を使用して電子メールを送信している場合は、電子メールプロバイダーによって既に資格情報が知られている可能性があります。</span><span class="sxs-lookup"><span data-stu-id="a327c-184">If you're sending email by using your personal ISP, your email provider might already know your credentials.</span></span> <span data-ttu-id="a327c-185">発行後、ローカルコンピューターでテストする場合とは異なる資格情報を使用することが必要になる場合があります。</span><span class="sxs-lookup"><span data-stu-id="a327c-185">After you publish, you might need to use different credentials than when you test on your local computer.</span></span>
- <span data-ttu-id="a327c-186">電子メールプロバイダーが暗号化を使用する場合は、`WebMail.EnableSsl` を `true`に設定します。</span><span class="sxs-lookup"><span data-stu-id="a327c-186">If your email provider uses encryption, set `WebMail.EnableSsl` to `true`.</span></span>

<span data-ttu-id="a327c-187">電子メールの送信中にエラーが発生した場合は、標準の ASP.NET エラーメッセージが表示されることがあります。これは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="a327c-187">If there is an error sending email, you might see a standard ASP.NET error message, which looks like this:</span></span>

![電子メールに問題があるときに ASP.NET エラーメッセージを表示する](aspnet-web-pages-razor-troubleshooting-guide/_static/image1.png)

<span data-ttu-id="a327c-189">次の例に示すように、`try-catch` ブロックを使用して、電子メールの送信に関する問題をデバッグすることもできます。</span><span class="sxs-lookup"><span data-stu-id="a327c-189">You can also debug problems with sending email by using a `try-catch` block, as in the following example.</span></span> <span data-ttu-id="a327c-190">`try-catch` ブロックを使用する場合、ASP.NET では標準エラーメッセージは表示されません。</span><span class="sxs-lookup"><span data-stu-id="a327c-190">When you use a `try-catch` block, ASP.NET does not display its standard error messages.</span></span> <span data-ttu-id="a327c-191">代わりに、ブロックの `catch` 部分でエラーをキャプチャできます。</span><span class="sxs-lookup"><span data-stu-id="a327c-191">Instead, you can capture the error in the `catch` portion of the block.</span></span>

[!code-cshtml[Main](aspnet-web-pages-razor-troubleshooting-guide/samples/sample3.cshtml)]

<span data-ttu-id="a327c-192">`your-SMTP-server-name`の適切な値に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="a327c-192">Substitute the appropriate values for `your-SMTP-server-name`, and so on.</span></span> <span data-ttu-id="a327c-193">このように表示されるエラーメッセージには、次のようなものがあります。</span><span class="sxs-lookup"><span data-stu-id="a327c-193">Some of the error messages you might see this way include the following:</span></span>

- <span data-ttu-id="a327c-194">*メールの送信に失敗します。*</span><span class="sxs-lookup"><span data-stu-id="a327c-194">*Failure sending mail.*</span></span>

    <span data-ttu-id="a327c-195">または</span><span class="sxs-lookup"><span data-stu-id="a327c-195">-or-</span></span>

    <span data-ttu-id="a327c-196">*接続されたパーティが一定期間内に適切に応答しなかったか、接続されたホストが応答に失敗したために確立された接続に失敗したため、接続に失敗しました*</span><span class="sxs-lookup"><span data-stu-id="a327c-196">*A connection attempt failed because the connected party did not properly respond after a period of time, or established connection failed because connected host has failed to respond*</span></span>

    <span data-ttu-id="a327c-197">このエラーは通常、アプリケーションが SMTP サーバーに接続できなかったことを示します。</span><span class="sxs-lookup"><span data-stu-id="a327c-197">This error usually means that the application could not connect to the SMTP server.</span></span> <span data-ttu-id="a327c-198">サーバー名とポート番号を確認します。</span><span class="sxs-lookup"><span data-stu-id="a327c-198">Check the server name and port number.</span></span>
- <span data-ttu-id="a327c-199">*メールボックスを使用できません。サーバーの応答: 5.1.0 &lt;someuser@invaliddomain&gt; 送信者が拒否しました: 送信者ドメインが無効です*</span><span class="sxs-lookup"><span data-stu-id="a327c-199">*Mailbox unavailable. The server response was: 5.1.0 &lt;someuser@invaliddomain&gt; sender rejected : invalid sender domain*</span></span>

    <span data-ttu-id="a327c-200">このメッセージは、`From` アドレスが正しくないか、または存在しないことを示している可能性があります。</span><span class="sxs-lookup"><span data-stu-id="a327c-200">This message can indicate that the `From` address is not correct or is missing.</span></span>
- <span data-ttu-id="a327c-201">*指定された文字列は、電子メールアドレスに必要な形式ではありません。*</span><span class="sxs-lookup"><span data-stu-id="a327c-201">*The specified string is not in the form required for an email address.*</span></span>

    <span data-ttu-id="a327c-202">このエラーは、`To` または `From` プロパティの値が電子メールアドレスとして認識されないことを示している可能性があります。</span><span class="sxs-lookup"><span data-stu-id="a327c-202">This error might indicate that the value of the `To` or `From` properties are not recognized as email addresses.</span></span> <span data-ttu-id="a327c-203">(ASP.NET のように、電子メールアドレスが有効であることを確認することはできません。 *name@domain.com* のように、正しい形式である必要があります)。</span><span class="sxs-lookup"><span data-stu-id="a327c-203">(ASP.NET cannot check that the email address is valid, only that it's in the correct format, like *name@domain.com*.)</span></span>

> [!NOTE]
> <span data-ttu-id="a327c-204">ページをライブサイトに発行する前に、エラー (`@errorMessage`) を表示するマークアップを削除します。</span><span class="sxs-lookup"><span data-stu-id="a327c-204">Remove the markup that displays the error (`@errorMessage`) before you publish the page to a live site.</span></span> <span data-ttu-id="a327c-205">サーバーから取得したエラーメッセージをユーザーに表示させることはお勧めしません。</span><span class="sxs-lookup"><span data-stu-id="a327c-205">It's not a good idea to let users see error messages that you get from a server.</span></span>

<a id="AdditionalResources"></a>
## <a name="additional-resources"></a><span data-ttu-id="a327c-206">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="a327c-206">Additional Resources</span></span>

[<span data-ttu-id="a327c-207">ASP.NET Web ページ (Razor) のよくあるご質問</span><span class="sxs-lookup"><span data-stu-id="a327c-207">ASP.NET Web Pages (Razor) FAQ</span></span>](https://go.microsoft.com/fwlink/?LinkId=253000)

<span data-ttu-id="a327c-208">ASP.NET web サイトの[WebMatrix と ASP.NET Web ページ](https://forums.asp.net/1224.aspx/1?WebMatrix)フォーラム</span><span class="sxs-lookup"><span data-stu-id="a327c-208">[WebMatrix and ASP.NET Web Pages](https://forums.asp.net/1224.aspx/1?WebMatrix) forum on the ASP.NET website</span></span>
