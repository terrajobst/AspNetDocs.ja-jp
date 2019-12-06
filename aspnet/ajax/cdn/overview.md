---
uid: ajax/cdn/overview
title: Microsoft Ajax Content Delivery Network |Microsoft Docs
author: rick-anderson
description: ''
ms.author: riande
ms.date: 10/14/2017
ms.assetid: 8935bf14-ca6d-4a4e-9dbe-b96ce74cef49
msc.legacyurl: /ajax/cdn
msc.type: content
ms.openlocfilehash: 51cb8d672139aaebd77bcdbe80bb579d4b3776aa
ms.sourcegitcommit: 969e7db924ebad3cc0f0cb0d65d148e8b9221b9a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/06/2019
ms.locfileid: "74899571"
---
# <a name="microsoft-ajax-content-delivery-network"></a><span data-ttu-id="0b9f6-102">Microsoft Ajax Content Delivery Network</span><span class="sxs-lookup"><span data-stu-id="0b9f6-102">Microsoft Ajax Content Delivery Network</span></span>

> [!WARNING]
> <span data-ttu-id="0b9f6-103">運用アプリケーションでは、CDN 資産に対してハードな依存関係を使用しないでください。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-103">Production applications should not take a hard dependency on CDN assets.</span></span> <span data-ttu-id="0b9f6-104">アプリケーションでは、参照されている CDN 資産をテストし、CDN が利用できない場合にフォールバックアセットを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-104">Applications should test for the CDN asset referenced, and use a fallback asset when the CDN is not available.</span></span>
>
> <span data-ttu-id="0b9f6-105">Microsoft Ajax CDN には、Azure CDN を超える SLA はありません。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-105">The Microsoft Ajax CDN has no SLA above and beyond using an Azure CDN.</span></span>
>
> <span data-ttu-id="0b9f6-106">Microsoft Ajax CDN に関する問題を報告するには、[この GitHub の問題](https://github.com/aspnet/AspNetDocs/issues/116)を使用します。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-106">Use [this GitHub issue](https://github.com/aspnet/AspNetDocs/issues/116) to report problems with the Microsoft Ajax CDN.</span></span>

## <a name="table-of-contents"></a><span data-ttu-id="0b9f6-107">目次</span><span class="sxs-lookup"><span data-stu-id="0b9f6-107">Table of Contents</span></span>

<span data-ttu-id="0b9f6-108">**[ajax.microsoft.com の名前が ajax.aspnetcdn.com に変更されました](#ajaxmicrosoftcom_renamed_to_ajaxaspnetcdncom_18)**</span><span class="sxs-lookup"><span data-stu-id="0b9f6-108">**[ajax.microsoft.com renamed to ajax.aspnetcdn.com](#ajaxmicrosoftcom_renamed_to_ajaxaspnetcdncom_18)**</span></span>  
<span data-ttu-id="0b9f6-109">**[Visual Studio の vsdoc サポート](#Visual_Studio_vsdoc_Support_19)**</span><span class="sxs-lookup"><span data-stu-id="0b9f6-109">**[Visual Studio .vsdoc Support](#Visual_Studio_vsdoc_Support_19)**</span></span>  
<span data-ttu-id="0b9f6-110">**[CDN からの ASP.NET Ajax の使用](#Using_ASPNET_Ajax_from_the_CDN_20)**</span><span class="sxs-lookup"><span data-stu-id="0b9f6-110">**[Using ASP.NET Ajax from the CDN](#Using_ASPNET_Ajax_from_the_CDN_20)**</span></span>  
<span data-ttu-id="0b9f6-111">**[CDN からの jQuery の使用](#Using_jQuery_from_the_CDN_21)**</span><span class="sxs-lookup"><span data-stu-id="0b9f6-111">**[Using jQuery from the CDN](#Using_jQuery_from_the_CDN_21)**</span></span>  
<span data-ttu-id="0b9f6-112">**[CDN から jQuery UI を使用する](#Using_jQuery_UI_from_the_CDN_22)**</span><span class="sxs-lookup"><span data-stu-id="0b9f6-112">**[Using jQuery UI from the CDN](#Using_jQuery_UI_from_the_CDN_22)**</span></span>  
<span data-ttu-id="0b9f6-113">**[CDN 上のサードパーティファイル](#Third-Party_Files_on_the_CDN_23)**</span><span class="sxs-lookup"><span data-stu-id="0b9f6-113">**[Third-Party Files on the CDN](#Third-Party_Files_on_the_CDN_23)**</span></span>  
  
 [<span data-ttu-id="0b9f6-114">CDN の jQuery リリース</span><span class="sxs-lookup"><span data-stu-id="0b9f6-114">jQuery Releases on the CDN</span></span>](#jQuery_Releases_on_the_CDN_0)  
 [<span data-ttu-id="0b9f6-115">CDN でリリースされた jQuery Migrate</span><span class="sxs-lookup"><span data-stu-id="0b9f6-115">jQuery Migrate Releases on the CDN</span></span>](#jQuery_Migrate_Releases_on_the_CDN_1)  
 [<span data-ttu-id="0b9f6-116">CDN の jQuery UI リリース</span><span class="sxs-lookup"><span data-stu-id="0b9f6-116">jQuery UI Releases on the CDN</span></span>](#jQuery_UI_Releases_on_the_CDN_2)  
 [<span data-ttu-id="0b9f6-117">CDN での jQuery 検証リリース</span><span class="sxs-lookup"><span data-stu-id="0b9f6-117">jQuery Validation Releases on the CDN</span></span>](#jQuery_Validation_Releases_on_the_CDN_3)  
 [<span data-ttu-id="0b9f6-118">CDN での jQuery Mobile リリース</span><span class="sxs-lookup"><span data-stu-id="0b9f6-118">jQuery Mobile Releases on the CDN</span></span>](#jQuery_Mobile_Releases_on_the_CDN_4)  
 [<span data-ttu-id="0b9f6-119">CDN での jQuery テンプレートのリリース</span><span class="sxs-lookup"><span data-stu-id="0b9f6-119">jQuery Templates Releases on the CDN</span></span>](#jQuery_Templates_Releases_on_the_CDN_5)  
 [<span data-ttu-id="0b9f6-120">CDN の jQuery サイクルリリース</span><span class="sxs-lookup"><span data-stu-id="0b9f6-120">jQuery Cycle Releases on the CDN</span></span>](#jQuery_Cycle_Releases_on_the_CDN_6)  
 [<span data-ttu-id="0b9f6-121">CDN での jQuery Datatable のリリース</span><span class="sxs-lookup"><span data-stu-id="0b9f6-121">jQuery DataTables Releases on the CDN</span></span>](#jQuery_DataTables_Releases_on_the_CDN_7)  
 [<span data-ttu-id="0b9f6-122">CDN での Modernizr リリース</span><span class="sxs-lookup"><span data-stu-id="0b9f6-122">Modernizr Releases on the CDN</span></span>](#Modernizr_Releases_on_the_CDN_8)  
 [<span data-ttu-id="0b9f6-123">CDN での JSHint リリース</span><span class="sxs-lookup"><span data-stu-id="0b9f6-123">JSHint Releases on the CDN</span></span>](#JSHint_Releases_on_the_CDN_10)  
 [<span data-ttu-id="0b9f6-124">CDN でのノックアウトリリース</span><span class="sxs-lookup"><span data-stu-id="0b9f6-124">Knockout Releases on the CDN</span></span>](#Knockout_Releases_on_the_CDN_11)  
 [<span data-ttu-id="0b9f6-125">CDN でのグローバライズのリリース</span><span class="sxs-lookup"><span data-stu-id="0b9f6-125">Globalize Releases on the CDN</span></span>](#Globalize_Releases_on_the_CDN_12)  
 [<span data-ttu-id="0b9f6-126">CDN でのリリースの応答</span><span class="sxs-lookup"><span data-stu-id="0b9f6-126">Respond Releases on the CDN</span></span>](#Respond_Releases_on_the_CDN_13)  
 [<span data-ttu-id="0b9f6-127">CDN でのブートストラップリリース</span><span class="sxs-lookup"><span data-stu-id="0b9f6-127">Bootstrap Releases on the CDN</span></span>](#Bootstrap_Releases_on_the_CDN_14)  
 [<span data-ttu-id="0b9f6-128">CDN でのブートストラップ TouchCarousel のリリース</span><span class="sxs-lookup"><span data-stu-id="0b9f6-128">Bootstrap TouchCarousel Releases on the CDN</span></span>](#BootstrapTouchCarousel_Releases_on_the_CDN_18)  
 [<span data-ttu-id="0b9f6-129">CDN でのハンマーのリリース</span><span class="sxs-lookup"><span data-stu-id="0b9f6-129">Hammer.js Releases on the CDN</span></span>](#Hammerjs_Releases_on_the_CDN_19)  
 [<span data-ttu-id="0b9f6-130">CDN での ASP.NET Web フォームと Ajax リリース</span><span class="sxs-lookup"><span data-stu-id="0b9f6-130">ASP.NET Web Forms and Ajax Releases on the CDN</span></span>](#ASPNET_Web_Forms_and_Ajax_Releases_on_the_CDN_15)  
 [<span data-ttu-id="0b9f6-131">CDN での ASP.NET MVC リリース</span><span class="sxs-lookup"><span data-stu-id="0b9f6-131">ASP.NET MVC Releases on the CDN</span></span>](#ASPNET_MVC_Releases_on_the_CDN_16)  
 [<span data-ttu-id="0b9f6-132">CDN での ASP.NET SignalR リリース</span><span class="sxs-lookup"><span data-stu-id="0b9f6-132">ASP.NET SignalR Releases on the CDN</span></span>](#ASPNET_SignalR_Releases_on_the_CDN_17)

<span data-ttu-id="0b9f6-133">Microsoft Ajax Content Delivery Network (CDN) は、jQuery などの一般的なサードパーティ製の JavaScript ライブラリをホストし、Web アプリケーションに簡単に追加できるようにします。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-133">The Microsoft Ajax Content Delivery Network (CDN) hosts popular third party JavaScript libraries such as jQuery and enables you to easily add them to your Web applications.</span></span> <span data-ttu-id="0b9f6-134">たとえば、ajax.aspnetcdn.com をポイントする &lt;スクリプト&gt; タグをページに追加するだけで、この CDN でホストされている jQuery の使用を開始できます。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-134">For example, you can start using jQuery which is hosted on this CDN simply by adding a &lt;script&gt; tag to your page that points to ajax.aspnetcdn.com.</span></span>

<span data-ttu-id="0b9f6-135">CDN を利用することで、Ajax アプリケーションのパフォーマンスを大幅に向上させることができます。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-135">By taking advantage of the CDN, you can significantly improve the performance of your Ajax applications.</span></span> <span data-ttu-id="0b9f6-136">CDN の内容は、世界中のサーバーにキャッシュされます。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-136">The contents of the CDN are cached on servers located around the world.</span></span> <span data-ttu-id="0b9f6-137">さらに、CDN を使用すると、ブラウザーは、別のドメインに配置されている web サイトに対してキャッシュされたサードパーティ製の JavaScript ファイルを再利用できます。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-137">In addition, the CDN enables browsers to reuse cached third party JavaScript files for web sites that are located in different domains.</span></span>

<span data-ttu-id="0b9f6-138">Secure Sockets Layer を使用して web ページを提供する必要がある場合に備えて、CDN は SSL (HTTPS) をサポートします。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-138">The CDN supports SSL (HTTPS) in case you need to serve a web page using the Secure Sockets Layer.</span></span>

<span data-ttu-id="0b9f6-139">CDN は、これらのライブラリの所有者によってアップロードされ、ユーザーに対してライセンスされている、次のサードパーティ製スクリプトライブラリをホストします。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-139">The CDN hosts the following third party script libraries which have been uploaded, and are licensed to you, by the owners of those libraries:</span></span>

- <span data-ttu-id="0b9f6-140">jQuery (www.jquery.com)</span><span class="sxs-lookup"><span data-stu-id="0b9f6-140">jQuery (www.jquery.com)</span></span>
- <span data-ttu-id="0b9f6-141">jQuery UI (www.jqueryui.com)</span><span class="sxs-lookup"><span data-stu-id="0b9f6-141">jQuery UI (www.jqueryui.com)</span></span>
- <span data-ttu-id="0b9f6-142">jQuery Mobile (www.jquerymobile.com)</span><span class="sxs-lookup"><span data-stu-id="0b9f6-142">jQuery Mobile (www.jquerymobile.com)</span></span>
- <span data-ttu-id="0b9f6-143">jQuery の検証 (www.jquery.com)</span><span class="sxs-lookup"><span data-stu-id="0b9f6-143">jQuery Validation (www.jquery.com)</span></span>
- <span data-ttu-id="0b9f6-144">jQuery サイクル (www.malsup.com/jquery/cycle/)</span><span class="sxs-lookup"><span data-stu-id="0b9f6-144">jQuery Cycle (www.malsup.com/jquery/cycle/)</span></span>
- <span data-ttu-id="0b9f6-145">jQuery Datatable (http://datatables.net/)</span><span class="sxs-lookup"><span data-stu-id="0b9f6-145">jQuery DataTables (http://datatables.net/)</span></span>

<span data-ttu-id="0b9f6-146">Microsoft Ajax CDN には、Microsoft によってアップロードされた次のライブラリも含まれています。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-146">The Microsoft Ajax CDN also includes the following libraries which have been uploaded by Microsoft:</span></span>

- <span data-ttu-id="0b9f6-147">ASP.NET Ajax</span><span class="sxs-lookup"><span data-stu-id="0b9f6-147">ASP.NET Ajax</span></span>
- <span data-ttu-id="0b9f6-148">ASP.NET MVC JavaScript ファイル</span><span class="sxs-lookup"><span data-stu-id="0b9f6-148">ASP.NET MVC JavaScript Files</span></span>
- <span data-ttu-id="0b9f6-149">ASP.NET SignalR JavaScript ファイル</span><span class="sxs-lookup"><span data-stu-id="0b9f6-149">ASP.NET SignalR JavaScript Files</span></span>

<span data-ttu-id="0b9f6-150">Microsoft は、この CDN でホストされているサードパーティ製ライブラリの所有権を要求しません。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-150">Microsoft does not claim ownership of any third-party libraries hosted on this CDN.</span></span> <span data-ttu-id="0b9f6-151">ライブラリの著作権者は、これらのライブラリのライセンスを取得します。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-151">The copyright owners of the libraries are licensing these libraries to you.</span></span> <span data-ttu-id="0b9f6-152">このようなライブラリをダウンロードして使用する必要がある権利は、それぞれの著作権者によってのみ付与されます。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-152">Any rights that you may have to download and use such libraries are granted solely by the respective copyright owners.</span></span> <span data-ttu-id="0b9f6-153">Microsoft はこれらのライブラリではないため、この CDN でホストされているサードパーティのライブラリに対して、マイクロソフトはいかなる保証も知的財産権の付与 (黙示的な特許権を含む) もいたしません。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-153">Because these are not Microsoft libraries, Microsoft provides no warranties or intellectual property rights licenses (including no implied patent rights) for the third party libraries hosted on this CDN.</span></span>

<span data-ttu-id="0b9f6-154">場合は、JavaScript ライブラリを提出して、ライブラリは、最上位の JavaScript ライブラリのいずれか (に示された http://trends.builtwith.com) または 拡張機能/プラグインには、人気のある (a)。 または (b) ASP.NET で使用するために役立ちますし、にお問い合わせくださいこれらのライブラリに AjaxCDNSubmission@Microsoft.com します。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-154">If you wish to submit your JavaScript library and your library is one of the top JavaScript libraries (as listed on http://trends.builtwith.com) or extensions/plugins to these libraries that are (a) popular; or (b) helpful for use on ASP.NET then please contact AjaxCDNSubmission@Microsoft.com.</span></span>

<a id="ajaxmicrosoftcom_renamed_to_ajaxaspnetcdncom_18"></a>

## <a name="ajaxmicrosoftcom-renamed-to-ajaxaspnetcdncom"></a><span data-ttu-id="0b9f6-155">ajax.microsoft.com の名前が ajax.aspnetcdn.com に変更されました</span><span class="sxs-lookup"><span data-stu-id="0b9f6-155">ajax.microsoft.com renamed to ajax.aspnetcdn.com</span></span>

<span data-ttu-id="0b9f6-156">Microsoft.com ドメイン名を使用するために使用される CDN は、aspnetcdn.com ドメイン名を使用するように変更されています。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-156">The CDN used to use the microsoft.com domain name and has been changed to use the aspnetcdn.com domain name.</span></span> <span data-ttu-id="0b9f6-157">この変更はパフォーマンスを向上させるために行われました。これは、ブラウザーが microsoft.com ドメインを参照したときに、各要求でネットワーク経由でそのドメインからクッキーを送信するからです。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-157">This change was made to increase performance because when a browser referenced the microsoft.com domain it would send any cookies from that domain across the wire with each request.</span></span> <span data-ttu-id="0b9f6-158">Microsoft.com パフォーマンス以外のドメイン名に名前を変更すると、25% まで増やすことができます。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-158">By renaming to a domain name other than microsoft.com performance can be increased by as much to 25%.</span></span> <span data-ttu-id="0b9f6-159">注 ajax.microsoft.com は引き続き機能しますが、ajax.aspnetcdn.com をお勧めします。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-159">Note ajax.microsoft.com will continue to function but ajax.aspnetcdn.com is recommended.</span></span>

- <span data-ttu-id="0b9f6-160">古い形式: https://ajax.microsoft.com/ajax/jQuery/jquery-1.8.0.js</span><span class="sxs-lookup"><span data-stu-id="0b9f6-160">Old Format: https://ajax.microsoft.com/ajax/jQuery/jquery-1.8.0.js</span></span>
- <span data-ttu-id="0b9f6-161">新しい形式: https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js</span><span class="sxs-lookup"><span data-stu-id="0b9f6-161">New Format: https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js</span></span>

<a id="Visual_Studio_vsdoc_Support_19"></a>

## <a name="visual-studio-vsdoc-support"></a><span data-ttu-id="0b9f6-162">Visual Studio の vsdoc サポート</span><span class="sxs-lookup"><span data-stu-id="0b9f6-162">Visual Studio .vsdoc Support</span></span>

<span data-ttu-id="0b9f6-163">Visual Studio 2008 で vsdoc ファイルを適切に使用するには、VS 2008 SP1 がインストールされていること、および vsdoc ファイル用の修正プログラムがインストールされていることを確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-163">To use the .vsdoc files properly with Visual Studio 2008 you need to make sure that you have VS 2008 SP1 installed and the hotfix for vsdoc files installed.</span></span> <span data-ttu-id="0b9f6-164">次の場所から取得できます。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-164">You can get these from here:</span></span>

- [<span data-ttu-id="0b9f6-165">Visual Studio 2008 SP1 のダウンロード</span><span class="sxs-lookup"><span data-stu-id="0b9f6-165">Download Visual Studio 2008 SP1</span></span>](https://www.microsoft.com/downloads/en/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en "Visual Studio 2008 SP1 のダウンロード")
- [<span data-ttu-id="0b9f6-166">Visual Studio 2008 SP1 の vsdoc 修正プログラムをダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-166">Download .vsdoc hotfix for Visual Studio 2008 SP1</span></span>](https://code.msdn.microsoft.com/KB958502/Release/ProjectReleases.aspx?ReleaseId=1736 "Visual Studio 2008 SP1 の vsdoc 修正プログラムをダウンロードします。")

<span data-ttu-id="0b9f6-167">Visual Studio 2010 では、追加の修正プログラムを適用せずに、vsdoc ファイルをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-167">Visual Studio 2010 supports .vsdoc files without any additional patches.</span></span>

<a id="Using_ASPNET_Ajax_from_the_CDN_20"></a>

## <a name="using-aspnet-ajax-from-the-cdn"></a><span data-ttu-id="0b9f6-168">CDN からの ASP.NET Ajax の使用</span><span class="sxs-lookup"><span data-stu-id="0b9f6-168">Using ASP.NET Ajax from the CDN</span></span>

<span data-ttu-id="0b9f6-169">ASP.NET 4 を使用する場合は、ASP.NET framework スクリプトに対するすべての要求を CDN にリダイレクトできます。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-169">When using ASP.NET 4, you can redirect all requests for ASP.NET framework scripts to the CDN.</span></span> <span data-ttu-id="0b9f6-170">ローカル web サーバーではなく CDN からスクリプトを取得すると、パブリック ASP.NET web サイトのパフォーマンスを大幅に向上させることができます。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-170">Retrieving scripts from the CDN instead of your local web server can substantially improve the performance of public ASP.NET websites.</span></span>

<span data-ttu-id="0b9f6-171">ScriptManager EnableCDN プロパティを使用して、すべての ASP.NET framework スクリプト要求を Microsoft Ajax CDN にリダイレクトします。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-171">Use the ScriptManager EnableCDN property to redirect all ASP.NET framework script requests to the Microsoft Ajax CDN:</span></span>

[!code-aspx[Main](overview/samples/sample1.aspx)]

<a id="Using_jQuery_from_the_CDN_21"></a>

## <a name="using-jquery-from-the-cdn"></a><span data-ttu-id="0b9f6-172">CDN からの jQuery の使用</span><span class="sxs-lookup"><span data-stu-id="0b9f6-172">Using jQuery from the CDN</span></span>

<span data-ttu-id="0b9f6-173">Web アプリケーションで CDN でホストされている jQuery スクリプトを使用するには、次のスクリプト要素をページに追加します。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-173">You can use jQuery scripts hosted on CDN in your Web application by adding the following script element to a page:</span></span>

[!code-html[Main](overview/samples/sample2.html)]

<span data-ttu-id="0b9f6-174">CDN には、次の要素を使用して取得できる、指定されたバージョンの jQuery スクリプトも含まれています。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-174">The CDN also includes the minified version of the jQuery script, which you can get using the following element:</span></span>

[!code-html[Main](overview/samples/sample3.html)]

<span data-ttu-id="0b9f6-175">CDN を使用できない場合に、ページが自分の web サイトのローカルパスから jQuery を読み込むことができるようにするには、CDN を参照する要素の直後に次の要素を追加します。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-175">To allow your page to fallback to loading jQuery from a local path on your own website if the CDN happens to be unavailable, add the following element immediately after the element referencing the CDN:</span></span>

[!code-html[Main](overview/samples/sample4.html)]

<span data-ttu-id="0b9f6-176">次のサンプルページでは、ボタンがクリックされたときに、(ローカルコピーにフォールバックする) jQuery ライブラリの CDN バージョンを使用して、div 要素の内容を表示します。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-176">The following sample page uses the CDN version of the jQuery library (with fallback to a local copy) to display the contents of a div element when a button is clicked.</span></span>

[!code-html[Main](overview/samples/sample5.html)]

<span data-ttu-id="0b9f6-177">Jquery の詳細について[は、jquery Web サイト](http://jquery.com/)にアクセスして jquery のローカルコピーをダウンロードしてください。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-177">You can learn more about jQuery and download a local copy of jQuery by visiting the [jQuery](http://jquery.com/) Web site.</span></span>

<a id="Using_jQuery_UI_from_the_CDN_22"></a>

## <a name="using-jquery-ui-from-the-cdn"></a><span data-ttu-id="0b9f6-178">CDN から jQuery UI を使用する</span><span class="sxs-lookup"><span data-stu-id="0b9f6-178">Using jQuery UI from the CDN</span></span>

<span data-ttu-id="0b9f6-179">CDN は、jQuery UI ライブラリもホストします。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-179">The CDN also hosts the jQuery UI library.</span></span> <span data-ttu-id="0b9f6-180">JQuery UI ライブラリには、ASP.NET アプリケーションで使用できる豊富なウィジェットと効果のセットが含まれています。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-180">The jQuery UI library includes a rich set of widgets and effects that you can use in your ASP.NET applications.</span></span> <span data-ttu-id="0b9f6-181">たとえば、次のページは、ASP.NET Web フォームアプリケーションのコンテキストで jQuery UI Datepicker を使用してポップアップカレンダーを表示する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-181">For example, the following page illustrates how you can use the jQuery UI Datepicker in the context of an ASP.NET Web Forms application to display a pop-up calendar:</span></span>

[!code-aspx[Main](overview/samples/sample6.aspx)]

<span data-ttu-id="0b9f6-182">キーボードを使用してテキストボックスにフォーカスを移動すると、カレンダーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-182">When you move focus to the TextBox using your keyboard, a calendar is displayed:</span></span>

![Datepicker で作成されたポップアップカレンダー](overview/_static/image1.png)

<span data-ttu-id="0b9f6-184">上記のコードでは、CDN から次の3つのファイルを含める必要があることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-184">Notice that you must include three files from the CDN in the code above:</span></span>

- <span data-ttu-id="0b9f6-185">Jquery UI ライブラリ &mdash; jquery ライブラリは、jQuery ライブラリに依存します。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-185">The jQuery library &mdash; The jQuery UI library depends on the jQuery library.</span></span> <span data-ttu-id="0b9f6-186">Jquery UI ライブラリを追加する前に、jQuery ライブラリをページに追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-186">You must add the jQuery library to your page before you add the jQuery UI library.</span></span>
- <span data-ttu-id="0b9f6-187">Jquery UI ライブラリ &mdash; jQuery ui ライブラリには、上のページで使用されている Datepicker ウィジェットなどのすべての jQuery UI 効果とウィジェットが含まれています。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-187">The jQuery UI library &mdash; The jQuery UI library contains all of the jQuery UI effects and widgets such as the Datepicker widget used in the page above.</span></span>
- <span data-ttu-id="0b9f6-188">Jquery ui の &mdash; jQuery UI テーマは、さまざまなテーマをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-188">A jQuery UI theme &mdash; The jQuery UI supports different themes.</span></span> <span data-ttu-id="0b9f6-189">上のページには、Redmond テーマをインポートするための CSS ファイルへのリンクが含まれています。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-189">The page above includes a link to a CSS file to import the Redmond theme.</span></span>

<span data-ttu-id="0b9f6-190">すべての標準的な jQuery UI テーマは CDN でホストされます。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-190">All of the standard jQuery UI themes are hosted on the CDN.</span></span> <span data-ttu-id="0b9f6-191">[このページにアクセス](jquery-ui/cdnjqueryui1910.md "jMicrosoft Ajax CDN のクエリ UI 1.8.10)すると、各テーマのサムネイルが表示されます。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-191">[Visit this page](jquery-ui/cdnjqueryui1910.md "jQuery UI 1.8.10 on the Microsoft Ajax CDN") to view thumbnails for each theme.</span></span>

<span data-ttu-id="0b9f6-192">JQuery UI ライブラリの詳細については、公式の[JQUERY ui web サイト](http://jQueryUI.com "jQuery UI web サイト")を参照してください。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-192">To learn more about the jQuery UI library, visit the official [jQuery UI website](http://jQueryUI.com "jQuery UI website").</span></span>

<a id="Third-Party_Files_on_the_CDN_23"></a>

## <a name="third-party-files-on-the-cdn"></a><span data-ttu-id="0b9f6-193">CDN 上のサードパーティファイル</span><span class="sxs-lookup"><span data-stu-id="0b9f6-193">Third-Party Files on the CDN</span></span>

<span data-ttu-id="0b9f6-194">CDN は、最も一般的なサードパーティ製の JavaScript ライブラリの一部をホストします。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-194">The CDN hosts some of the most popular third party JavaScript libraries.</span></span> <span data-ttu-id="0b9f6-195">Microsoft は、この CDN でホストされているサードパーティ製ライブラリの所有権を要求しません。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-195">Microsoft does not claim ownership of any third-party libraries hosted on this CDN.</span></span> <span data-ttu-id="0b9f6-196">ライブラリの著作権者は、これらのライブラリのライセンスを取得します。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-196">The copyright owners of the libraries are licensing these libraries to you.</span></span> <span data-ttu-id="0b9f6-197">このようなライブラリをダウンロードして使用する必要がある権利は、それぞれの著作権者によってのみ付与されます。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-197">Any rights that you may have to download and use such libraries are granted solely by the respective copyright owners.</span></span> <span data-ttu-id="0b9f6-198">Microsoft はこれらのライブラリではないため、この CDN でホストされているサードパーティのライブラリに対して、マイクロソフトはいかなる保証も知的財産権の付与 (黙示的な特許権を含む) もいたしません。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-198">Because these are not Microsoft libraries, Microsoft provides no warranties or intellectual property rights licenses (including no implied patent rights) for the third party libraries hosted on this CDN.</span></span>

<a id="jQuery_Releases_on_the_CDN_0"></a>

### <a name="jquery-releases-on-the-cdn"></a><span data-ttu-id="0b9f6-199">CDN の jQuery リリース</span><span class="sxs-lookup"><span data-stu-id="0b9f6-199">jQuery Releases on the CDN</span></span>

<span data-ttu-id="0b9f6-200">次の jQuery のリリースは CDN でホストされています。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-200">The following releases of jQuery are hosted on the CDN:</span></span>

#### <a name="jquery-version-341"></a><span data-ttu-id="0b9f6-201">jQuery バージョン3.4.1</span><span class="sxs-lookup"><span data-stu-id="0b9f6-201">jQuery version 3.4.1</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.slim.min.map

#### <a name="jquery-version-340"></a><span data-ttu-id="0b9f6-202">jQuery バージョン3.4.0</span><span class="sxs-lookup"><span data-stu-id="0b9f6-202">jQuery version 3.4.0</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.slim.min.map

#### <a name="jquery-version-331"></a><span data-ttu-id="0b9f6-203">jQuery バージョン3.3.1</span><span class="sxs-lookup"><span data-stu-id="0b9f6-203">jQuery version 3.3.1</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.min.map

#### <a name="jquery-version-321"></a><span data-ttu-id="0b9f6-204">jQuery バージョン3.2.1</span><span class="sxs-lookup"><span data-stu-id="0b9f6-204">jQuery version 3.2.1</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.min.map

#### <a name="jquery-version-320"></a><span data-ttu-id="0b9f6-205">jQuery バージョン3.2.0</span><span class="sxs-lookup"><span data-stu-id="0b9f6-205">jQuery version 3.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.min.map

#### <a name="jquery-version-311"></a><span data-ttu-id="0b9f6-206">jQuery バージョン3.1.1</span><span class="sxs-lookup"><span data-stu-id="0b9f6-206">jQuery version 3.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.min.map

#### <a name="jquery-version-310"></a><span data-ttu-id="0b9f6-207">jQuery バージョン3.1.0</span><span class="sxs-lookup"><span data-stu-id="0b9f6-207">jQuery version 3.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.min.map

#### <a name="jquery-version-300"></a><span data-ttu-id="0b9f6-208">jQuery バージョン3.0.0</span><span class="sxs-lookup"><span data-stu-id="0b9f6-208">jQuery version 3.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.min.map

#### <a name="jquery-version-224"></a><span data-ttu-id="0b9f6-209">jQuery バージョン2.2.4</span><span class="sxs-lookup"><span data-stu-id="0b9f6-209">jQuery version 2.2.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.min.map

#### <a name="jquery-version-223"></a><span data-ttu-id="0b9f6-210">jQuery バージョン2.2.3</span><span class="sxs-lookup"><span data-stu-id="0b9f6-210">jQuery version 2.2.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.min.map

#### <a name="jquery-version-222"></a><span data-ttu-id="0b9f6-211">jQuery バージョン2.2.2</span><span class="sxs-lookup"><span data-stu-id="0b9f6-211">jQuery version 2.2.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.min.map

#### <a name="jquery-version-221"></a><span data-ttu-id="0b9f6-212">jQuery バージョン2.2.1</span><span class="sxs-lookup"><span data-stu-id="0b9f6-212">jQuery version 2.2.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.min.map

#### <a name="jquery-version-220"></a><span data-ttu-id="0b9f6-213">jQuery バージョン2.2.0</span><span class="sxs-lookup"><span data-stu-id="0b9f6-213">jQuery version 2.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.min.map

#### <a name="jquery-version-214"></a><span data-ttu-id="0b9f6-214">jQuery バージョン2.1.4</span><span class="sxs-lookup"><span data-stu-id="0b9f6-214">jQuery version 2.1.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.min.map

#### <a name="jquery-version-213"></a><span data-ttu-id="0b9f6-215">jQuery バージョン2.1.3</span><span class="sxs-lookup"><span data-stu-id="0b9f6-215">jQuery version 2.1.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.min.map

#### <a name="jquery-version-212"></a><span data-ttu-id="0b9f6-216">jQuery バージョン2.1.2</span><span class="sxs-lookup"><span data-stu-id="0b9f6-216">jQuery version 2.1.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.2.min.js

#### <a name="jquery-version-211"></a><span data-ttu-id="0b9f6-217">jQuery バージョン2.1.1</span><span class="sxs-lookup"><span data-stu-id="0b9f6-217">jQuery version 2.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.map

#### <a name="jquery-version-210"></a><span data-ttu-id="0b9f6-218">jQuery バージョン2.1.0</span><span class="sxs-lookup"><span data-stu-id="0b9f6-218">jQuery version 2.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.min.map

#### <a name="jquery-version-203"></a><span data-ttu-id="0b9f6-219">jQuery バージョン2.0.3</span><span class="sxs-lookup"><span data-stu-id="0b9f6-219">jQuery version 2.0.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.min.map

#### <a name="jquery-version-202"></a><span data-ttu-id="0b9f6-220">jQuery バージョン2.0.2</span><span class="sxs-lookup"><span data-stu-id="0b9f6-220">jQuery version 2.0.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.min.map

#### <a name="jquery-version-201"></a><span data-ttu-id="0b9f6-221">jQuery バージョン2.0.1</span><span class="sxs-lookup"><span data-stu-id="0b9f6-221">jQuery version 2.0.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.min.map

#### <a name="jquery-version-200"></a><span data-ttu-id="0b9f6-222">jQuery バージョン2.0.0</span><span class="sxs-lookup"><span data-stu-id="0b9f6-222">jQuery version 2.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.min.map

#### <a name="jquery-version-1124"></a><span data-ttu-id="0b9f6-223">jQuery バージョン1.12.4</span><span class="sxs-lookup"><span data-stu-id="0b9f6-223">jQuery version 1.12.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.min.map

#### <a name="jquery-version-1123"></a><span data-ttu-id="0b9f6-224">jQuery バージョン1.12.3</span><span class="sxs-lookup"><span data-stu-id="0b9f6-224">jQuery version 1.12.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.min.map

#### <a name="jquery-version-1122"></a><span data-ttu-id="0b9f6-225">jQuery バージョン1.12.2</span><span class="sxs-lookup"><span data-stu-id="0b9f6-225">jQuery version 1.12.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.min.map

#### <a name="jquery-version-1121"></a><span data-ttu-id="0b9f6-226">jQuery バージョン1.12.1</span><span class="sxs-lookup"><span data-stu-id="0b9f6-226">jQuery version 1.12.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.min.map

#### <a name="jquery-version-1120"></a><span data-ttu-id="0b9f6-227">jQuery バージョン1.12.0 以降</span><span class="sxs-lookup"><span data-stu-id="0b9f6-227">jQuery version 1.12.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.min.map

#### <a name="jquery-version-1113"></a><span data-ttu-id="0b9f6-228">jQuery バージョン1.11.3</span><span class="sxs-lookup"><span data-stu-id="0b9f6-228">jQuery version 1.11.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.min.map

#### <a name="jquery-version-1112"></a><span data-ttu-id="0b9f6-229">jQuery バージョン1.11.2</span><span class="sxs-lookup"><span data-stu-id="0b9f6-229">jQuery version 1.11.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.min.map

#### <a name="jquery-version-1111"></a><span data-ttu-id="0b9f6-230">jQuery バージョン1.11.1</span><span class="sxs-lookup"><span data-stu-id="0b9f6-230">jQuery version 1.11.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.min.map

#### <a name="jquery-version-1110"></a><span data-ttu-id="0b9f6-231">jQuery バージョン1.11.0</span><span class="sxs-lookup"><span data-stu-id="0b9f6-231">jQuery version 1.11.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.min.map

#### <a name="jquery-version-1102"></a><span data-ttu-id="0b9f6-232">jQuery バージョン1.10.2</span><span class="sxs-lookup"><span data-stu-id="0b9f6-232">jQuery version 1.10.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.min.map

#### <a name="jquery-version-1101"></a><span data-ttu-id="0b9f6-233">jQuery バージョン1.10.1 以降</span><span class="sxs-lookup"><span data-stu-id="0b9f6-233">jQuery version 1.10.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.min.map

#### <a name="jquery-version-1100"></a><span data-ttu-id="0b9f6-234">jQuery バージョン1.10.0</span><span class="sxs-lookup"><span data-stu-id="0b9f6-234">jQuery version 1.10.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.min.map

#### <a name="jquery-version-191"></a><span data-ttu-id="0b9f6-235">jQuery バージョン1.9.1</span><span class="sxs-lookup"><span data-stu-id="0b9f6-235">jQuery version 1.9.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.min.map

#### <a name="jquery-version-190"></a><span data-ttu-id="0b9f6-236">jQuery バージョン1.9.0 以降</span><span class="sxs-lookup"><span data-stu-id="0b9f6-236">jQuery version 1.9.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.min.map

#### <a name="jquery-version-183"></a><span data-ttu-id="0b9f6-237">jQuery バージョン1.8.3</span><span class="sxs-lookup"><span data-stu-id="0b9f6-237">jQuery version 1.8.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3-vsdoc.js

#### <a name="jquery-version-182"></a><span data-ttu-id="0b9f6-238">jQuery バージョン1.8.2</span><span class="sxs-lookup"><span data-stu-id="0b9f6-238">jQuery version 1.8.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2-vsdoc.js

#### <a name="jquery-version-181"></a><span data-ttu-id="0b9f6-239">jQuery バージョン1.8.1</span><span class="sxs-lookup"><span data-stu-id="0b9f6-239">jQuery version 1.8.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1-vsdoc.js

#### <a name="jquery-version-180"></a><span data-ttu-id="0b9f6-240">jQuery バージョン1.8.0 以降</span><span class="sxs-lookup"><span data-stu-id="0b9f6-240">jQuery version 1.8.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0-vsdoc.js

#### <a name="jquery-version-172"></a><span data-ttu-id="0b9f6-241">jQuery バージョン1.7.2</span><span class="sxs-lookup"><span data-stu-id="0b9f6-241">jQuery version 1.7.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.2.min.js

#### <a name="jquery-version-171"></a><span data-ttu-id="0b9f6-242">jQuery バージョン1.7.1</span><span class="sxs-lookup"><span data-stu-id="0b9f6-242">jQuery version 1.7.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1-vsdoc.js

#### <a name="jquery-version-17"></a><span data-ttu-id="0b9f6-243">jQuery バージョン1.7</span><span class="sxs-lookup"><span data-stu-id="0b9f6-243">jQuery version 1.7</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7-vsdoc.js

#### <a name="jquery-version-164"></a><span data-ttu-id="0b9f6-244">jQuery バージョン1.6.4</span><span class="sxs-lookup"><span data-stu-id="0b9f6-244">jQuery version 1.6.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4-vsdoc.js

#### <a name="jquery-version-163"></a><span data-ttu-id="0b9f6-245">jQuery バージョン1.6.3</span><span class="sxs-lookup"><span data-stu-id="0b9f6-245">jQuery version 1.6.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3-vsdoc.js

#### <a name="jquery-version-162"></a><span data-ttu-id="0b9f6-246">jQuery バージョン1.6.2</span><span class="sxs-lookup"><span data-stu-id="0b9f6-246">jQuery version 1.6.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2-vsdoc.js

#### <a name="jquery-version-161"></a><span data-ttu-id="0b9f6-247">jQuery バージョン1.6.1</span><span class="sxs-lookup"><span data-stu-id="0b9f6-247">jQuery version 1.6.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1-vsdoc.js

#### <a name="jquery-version-16"></a><span data-ttu-id="0b9f6-248">jQuery バージョン1.6</span><span class="sxs-lookup"><span data-stu-id="0b9f6-248">jQuery version 1.6</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6-vsdoc.js

#### <a name="jquery-version-152"></a><span data-ttu-id="0b9f6-249">jQuery バージョン1.5.2</span><span class="sxs-lookup"><span data-stu-id="0b9f6-249">jQuery version 1.5.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2-vsdoc.js

#### <a name="jquery-version-151"></a><span data-ttu-id="0b9f6-250">jQuery バージョン1.5.1</span><span class="sxs-lookup"><span data-stu-id="0b9f6-250">jQuery version 1.5.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1-vsdoc.js

#### <a name="jquery-version-15"></a><span data-ttu-id="0b9f6-251">jQuery バージョン1.5</span><span class="sxs-lookup"><span data-stu-id="0b9f6-251">jQuery version 1.5</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5-vsdoc.js

#### <a name="jquery-version-144"></a><span data-ttu-id="0b9f6-252">jQuery バージョン1.4.4</span><span class="sxs-lookup"><span data-stu-id="0b9f6-252">jQuery version 1.4.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4-vsdoc.js

#### <a name="jquery-version-143"></a><span data-ttu-id="0b9f6-253">jQuery バージョン1.4.3</span><span class="sxs-lookup"><span data-stu-id="0b9f6-253">jQuery version 1.4.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3-vsdoc.js

#### <a name="jquery-version-142"></a><span data-ttu-id="0b9f6-254">jQuery バージョン1.4.2</span><span class="sxs-lookup"><span data-stu-id="0b9f6-254">jQuery version 1.4.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2-vsdoc.js

#### <a name="jquery-version-141"></a><span data-ttu-id="0b9f6-255">jQuery バージョン1.4.1</span><span class="sxs-lookup"><span data-stu-id="0b9f6-255">jQuery version 1.4.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1-vsdoc.js

#### <a name="jquery-version-14"></a><span data-ttu-id="0b9f6-256">jQuery バージョン1.4</span><span class="sxs-lookup"><span data-stu-id="0b9f6-256">jQuery version 1.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.min.js

#### <a name="jquery-version-132"></a><span data-ttu-id="0b9f6-257">jQuery バージョン1.3.2</span><span class="sxs-lookup"><span data-stu-id="0b9f6-257">jQuery version 1.3.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.min-vsdoc.js

<a id="jQuery_Migrate_Releases_on_the_CDN_1"></a>

### <a name="jquery-migrate-releases-on-the-cdn"></a><span data-ttu-id="0b9f6-258">CDN でリリースされた jQuery Migrate</span><span class="sxs-lookup"><span data-stu-id="0b9f6-258">jQuery Migrate Releases on the CDN</span></span>

<span data-ttu-id="0b9f6-259">JQuery Migrate の次のリリースは、CDN でホストされています。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-259">The following releases of jQuery Migrate are hosted on the CDN:</span></span>

#### <a name="jquery-migrate-version-300"></a><span data-ttu-id="0b9f6-260">jQuery Migrate バージョン3.0.0</span><span class="sxs-lookup"><span data-stu-id="0b9f6-260">jQuery Migrate version 3.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-3.0.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-3.0.0.min.js

#### <a name="jquery-migrate-version-121"></a><span data-ttu-id="0b9f6-261">jQuery Migrate バージョン1.2.1</span><span class="sxs-lookup"><span data-stu-id="0b9f6-261">jQuery Migrate version 1.2.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.1.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.1.min.js

<span data-ttu-id="0b9f6-262">jQuery Migrate バージョン1.2.0</span><span class="sxs-lookup"><span data-stu-id="0b9f6-262">jQuery Migrate version 1.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.0.min.js

#### <a name="jquery-migrate-version-111"></a><span data-ttu-id="0b9f6-263">jQuery Migrate バージョン1.1.1</span><span class="sxs-lookup"><span data-stu-id="0b9f6-263">jQuery Migrate version 1.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.1.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.1.min.js

#### <a name="jquery-migrate-version-110"></a><span data-ttu-id="0b9f6-264">jQuery Migrate バージョン1.1.0</span><span class="sxs-lookup"><span data-stu-id="0b9f6-264">jQuery Migrate version 1.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.0.min.js

#### <a name="jquery-migrate-version-100"></a><span data-ttu-id="0b9f6-265">jQuery Migrate バージョン1.0.0</span><span class="sxs-lookup"><span data-stu-id="0b9f6-265">jQuery Migrate version 1.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.0.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.0.0.min.js

<a id="jQuery_UI_Releases_on_the_CDN_2"></a>

### <a name="jquery-ui-releases-on-the-cdn"></a><span data-ttu-id="0b9f6-266">CDN の jQuery UI リリース</span><span class="sxs-lookup"><span data-stu-id="0b9f6-266">jQuery UI Releases on the CDN</span></span>

<span data-ttu-id="0b9f6-267">JQuery UI ライブラリの次のリリースは、この CDN でホストされています。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-267">The following releases of the jQuery UI library are hosted on this CDN.</span></span> <span data-ttu-id="0b9f6-268">各リンクをクリックすると、ファイルの実際の一覧が表示されます。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-268">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="0b9f6-269">jQuery UI 1.12.1</span><span class="sxs-lookup"><span data-stu-id="0b9f6-269">jQuery UI 1.12.1</span></span>](jquery-ui/cdnjqueryui1121.md "Microsoft Ajax CDN の jQuery UI 1.12.1")
- [<span data-ttu-id="0b9f6-270">jQuery UI 1.12.0 以降</span><span class="sxs-lookup"><span data-stu-id="0b9f6-270">jQuery UI 1.12.0</span></span>](jquery-ui/cdnjqueryui1120.md "Microsoft Ajax CDN の jQuery UI 1.12.0")
- [<span data-ttu-id="0b9f6-271">jQuery UI 1.11.4 以降</span><span class="sxs-lookup"><span data-stu-id="0b9f6-271">jQuery UI 1.11.4</span></span>](jquery-ui/cdnjqueryui1114.md "Microsoft Ajax CDN の jQuery UI 1.11.4")
- [<span data-ttu-id="0b9f6-272">jQuery UI 1.11.3</span><span class="sxs-lookup"><span data-stu-id="0b9f6-272">jQuery UI 1.11.3</span></span>](jquery-ui/cdnjqueryui1113.md "Microsoft Ajax CDN の jQuery UI 1.11.3")
- [<span data-ttu-id="0b9f6-273">jQuery UI 1.11.2</span><span class="sxs-lookup"><span data-stu-id="0b9f6-273">jQuery UI 1.11.2</span></span>](jquery-ui/cdnjqueryui1112.md "Microsoft Ajax CDN の jQuery UI 1.11.2")
- [<span data-ttu-id="0b9f6-274">jQuery UI 1.11.1</span><span class="sxs-lookup"><span data-stu-id="0b9f6-274">jQuery UI 1.11.1</span></span>](jquery-ui/cdnjqueryui1111.md "Microsoft Ajax CDN の jQuery UI 1.11.1")
- [<span data-ttu-id="0b9f6-275">jQuery UI 1.11.0</span><span class="sxs-lookup"><span data-stu-id="0b9f6-275">jQuery UI 1.11.0</span></span>](jquery-ui/cdnjqueryui1110.md "Microsoft Ajax CDN の jQuery UI 1.11.0")
- [<span data-ttu-id="0b9f6-276">jQuery UI 1.10.4</span><span class="sxs-lookup"><span data-stu-id="0b9f6-276">jQuery UI 1.10.4</span></span>](jquery-ui/cdnjqueryui1104.md "Microsoft Ajax CDN の jQuery UI 1.10.4")
- [<span data-ttu-id="0b9f6-277">jQuery UI 1.10.3</span><span class="sxs-lookup"><span data-stu-id="0b9f6-277">jQuery UI 1.10.3</span></span>](jquery-ui/cdnjqueryui1103.md "Microsoft Ajax CDN の jQuery UI 1.10.3")
- [<span data-ttu-id="0b9f6-278">jQuery UI 1.10.2</span><span class="sxs-lookup"><span data-stu-id="0b9f6-278">jQuery UI 1.10.2</span></span>](jquery-ui/cdnjqueryui1102.md "Microsoft Ajax CDN の jQuery UI 1.10.2")
- [<span data-ttu-id="0b9f6-279">jQuery UI 1.10.1 以降</span><span class="sxs-lookup"><span data-stu-id="0b9f6-279">jQuery UI 1.10.1</span></span>](jquery-ui/cdnjqueryui1101.md "Microsoft Ajax CDN の jQuery UI 1.10.1")
- [<span data-ttu-id="0b9f6-280">jQuery UI 1.10.0</span><span class="sxs-lookup"><span data-stu-id="0b9f6-280">jQuery UI 1.10.0</span></span>](jquery-ui/cdnjqueryui1100.md "Microsoft Ajax CDN の jQuery UI 1.10.0")
- [<span data-ttu-id="0b9f6-281">jQuery UI 1.9.2</span><span class="sxs-lookup"><span data-stu-id="0b9f6-281">jQuery UI 1.9.2</span></span>](jquery-ui/cdnjqueryui192.md "Microsoft Ajax CDN の jQuery UI 1.9.2")
- [<span data-ttu-id="0b9f6-282">jQuery UI 1.9.1</span><span class="sxs-lookup"><span data-stu-id="0b9f6-282">jQuery UI 1.9.1</span></span>](jquery-ui/cdnjqueryui191.md "Microsoft Ajax CDN の jQuery UI 1.9.1")
- [<span data-ttu-id="0b9f6-283">jQuery UI 1.9.0 以降</span><span class="sxs-lookup"><span data-stu-id="0b9f6-283">jQuery UI 1.9.0</span></span>](jquery-ui/cdnjqueryui190.md "Microsoft Ajax CDN の jQuery UI 1.9.0")
- [<span data-ttu-id="0b9f6-284">jQuery UI 1.8.24</span><span class="sxs-lookup"><span data-stu-id="0b9f6-284">jQuery UI 1.8.24</span></span>](jquery-ui/cdnjqueryui1824.md "Microsoft Ajax CDN の jQuery UI 1.8.24")
- [<span data-ttu-id="0b9f6-285">jQuery UI 1.8.23</span><span class="sxs-lookup"><span data-stu-id="0b9f6-285">jQuery UI 1.8.23</span></span>](jquery-ui/cdnjqueryui1823.md "Microsoft Ajax CDN の jQuery UI 1.8.23")
- [<span data-ttu-id="0b9f6-286">jQuery UI 1.8.22</span><span class="sxs-lookup"><span data-stu-id="0b9f6-286">jQuery UI 1.8.22</span></span>](jquery-ui/cdnjqueryui1822.md "Microsoft Ajax CDN の jQuery UI 1.8.22")
- [<span data-ttu-id="0b9f6-287">jQuery UI 1.8.21</span><span class="sxs-lookup"><span data-stu-id="0b9f6-287">jQuery UI 1.8.21</span></span>](jquery-ui/cdnjqueryui1821.md "Microsoft Ajax CDN の jQuery UI 1.8.21")
- [<span data-ttu-id="0b9f6-288">jQuery UI 1.8.20</span><span class="sxs-lookup"><span data-stu-id="0b9f6-288">jQuery UI 1.8.20</span></span>](jquery-ui/cdnjqueryui1820.md "Microsoft Ajax CDN の jQuery UI 1.8.20")
- [<span data-ttu-id="0b9f6-289">jQuery UI 1.8.19</span><span class="sxs-lookup"><span data-stu-id="0b9f6-289">jQuery UI 1.8.19</span></span>](jquery-ui/cdnjqueryui1819.md "Microsoft Ajax CDN の jQuery UI 1.8.19")
- [<span data-ttu-id="0b9f6-290">jQuery UI 1.8.18</span><span class="sxs-lookup"><span data-stu-id="0b9f6-290">jQuery UI 1.8.18</span></span>](jquery-ui/cdnjqueryui1818.md "Microsoft Ajax CDN の jQuery UI 1.8.18")
- [<span data-ttu-id="0b9f6-291">jQuery UI 1.8.17</span><span class="sxs-lookup"><span data-stu-id="0b9f6-291">jQuery UI 1.8.17</span></span>](jquery-ui/cdnjqueryui1817.md "Microsoft Ajax CDN の jQuery UI 1.8.17")
- [<span data-ttu-id="0b9f6-292">jQuery UI 1.8.16</span><span class="sxs-lookup"><span data-stu-id="0b9f6-292">jQuery UI 1.8.16</span></span>](jquery-ui/cdnjqueryui1816.md "Microsoft Ajax CDN の jQuery UI 1.8.16")
- [<span data-ttu-id="0b9f6-293">jQuery UI 1.8.15</span><span class="sxs-lookup"><span data-stu-id="0b9f6-293">jQuery UI 1.8.15</span></span>](jquery-ui/cdnjqueryui1815.md "Microsoft Ajax CDN の jQuery UI 1.8.15")
- [<span data-ttu-id="0b9f6-294">jQuery UI 1.8.14</span><span class="sxs-lookup"><span data-stu-id="0b9f6-294">jQuery UI 1.8.14</span></span>](jquery-ui/cdnjqueryui1814.md "Microsoft Ajax CDN の jQuery UI 1.8.14")
- [<span data-ttu-id="0b9f6-295">jQuery UI 1.8.13</span><span class="sxs-lookup"><span data-stu-id="0b9f6-295">jQuery UI 1.8.13</span></span>](jquery-ui/cdnjqueryui1813.md "Microsoft Ajax CDN の jQuery UI 1.8.13")
- [<span data-ttu-id="0b9f6-296">jQuery UI 1.8.12</span><span class="sxs-lookup"><span data-stu-id="0b9f6-296">jQuery UI 1.8.12</span></span>](jquery-ui/cdnjqueryui1812.md "Microsoft Ajax CDN の jQuery UI 1.8.12")
- [<span data-ttu-id="0b9f6-297">jQuery UI 1.8.11</span><span class="sxs-lookup"><span data-stu-id="0b9f6-297">jQuery UI 1.8.11</span></span>](jquery-ui/cdnjqueryui1811.md "Microsoft Ajax CDN の jQuery UI 1.8.11")
- [<span data-ttu-id="0b9f6-298">jQuery UI 1.8.10</span><span class="sxs-lookup"><span data-stu-id="0b9f6-298">jQuery UI 1.8.10</span></span>](jquery-ui/cdnjqueryui1910.md "Microsoft Ajax CDN の jQuery UI 1.8.10")
- [<span data-ttu-id="0b9f6-299">jQuery UI 1.8.9</span><span class="sxs-lookup"><span data-stu-id="0b9f6-299">jQuery UI 1.8.9</span></span>](jquery-ui/cdnjqueryui189.md "Microsoft Ajax CDN の jQuery UI 1.8.9")
- [<span data-ttu-id="0b9f6-300">jQuery UI 1.8.8</span><span class="sxs-lookup"><span data-stu-id="0b9f6-300">jQuery UI 1.8.8</span></span>](jquery-ui/cdnjqueryui188.md "Microsoft Ajax CDN の jQuery UI 1.8.8")
- [<span data-ttu-id="0b9f6-301">jQuery UI 1.8.7</span><span class="sxs-lookup"><span data-stu-id="0b9f6-301">jQuery UI 1.8.7</span></span>](jquery-ui/cdnjqueryui187.md "Microsoft Ajax CDN の jQuery UI 1.8.7")
- [<span data-ttu-id="0b9f6-302">jQuery UI 1.8.6</span><span class="sxs-lookup"><span data-stu-id="0b9f6-302">jQuery UI 1.8.6</span></span>](jquery-ui/cdnjqueryui186.md "Microsoft Ajax CDN の jQuery UI 1.8.6")
- [<span data-ttu-id="0b9f6-303">jQuery UI 1.8.5</span><span class="sxs-lookup"><span data-stu-id="0b9f6-303">jQuery UI 1.8.5</span></span>](jquery-ui/cdnjqueryui185.md "jQuery UI 1.8.5")

<a id="jQuery_Validation_Releases_on_the_CDN_3"></a>

### <a name="jquery-validation-releases-on-the-cdn"></a><span data-ttu-id="0b9f6-304">CDN での jQuery 検証リリース</span><span class="sxs-lookup"><span data-stu-id="0b9f6-304">jQuery Validation Releases on the CDN</span></span>

<span data-ttu-id="0b9f6-305">この CDN でホストされている jQuery 検証ライブラリのリリースは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-305">The following releases of the jQuery Validation library are hosted on this CDN.</span></span> <span data-ttu-id="0b9f6-306">各リンクをクリックすると、ファイルの実際の一覧が表示されます。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-306">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="0b9f6-307">jQuery Validate 1.19.1</span><span class="sxs-lookup"><span data-stu-id="0b9f6-307">jQuery Validate 1.19.1</span></span>](jquery-validate/cdnjqueryvalidate1191.md "jQuery Validation 1.19.1")
- [<span data-ttu-id="0b9f6-308">jQuery Validate 1.19.0</span><span class="sxs-lookup"><span data-stu-id="0b9f6-308">jQuery Validate 1.19.0</span></span>](jquery-validate/cdnjqueryvalidate1190.md "jQuery Validation 1.19.0")
- [<span data-ttu-id="0b9f6-309">jQuery Validate 1.17.0 以降</span><span class="sxs-lookup"><span data-stu-id="0b9f6-309">jQuery Validate 1.17.0</span></span>](jquery-validate/cdnjqueryvalidate1170.md "jQuery Validation 1.17.0 以降")
- [<span data-ttu-id="0b9f6-310">jQuery Validate 1.16.0</span><span class="sxs-lookup"><span data-stu-id="0b9f6-310">jQuery Validate 1.16.0</span></span>](jquery-validate/cdnjqueryvalidate1160.md "jQuery Validation 1.16.0")
- [<span data-ttu-id="0b9f6-311">jQuery Validate 1.15.1</span><span class="sxs-lookup"><span data-stu-id="0b9f6-311">jQuery Validate 1.15.1</span></span>](jquery-validate/cdnjqueryvalidate1151.md "jQuery Validation 1.15.1")
- [<span data-ttu-id="0b9f6-312">jQuery Validate 1.15.0</span><span class="sxs-lookup"><span data-stu-id="0b9f6-312">jQuery Validate 1.15.0</span></span>](jquery-validate/cdnjqueryvalidate1150.md "jQuery Validation 1.15.0")
- [<span data-ttu-id="0b9f6-313">jQuery Validate 1.14.0</span><span class="sxs-lookup"><span data-stu-id="0b9f6-313">jQuery Validate 1.14.0</span></span>](jquery-validate/cdnjqueryvalidate1140.md "jQuery Validation 1.14.0")
- [<span data-ttu-id="0b9f6-314">jQuery Validate 1.13.1</span><span class="sxs-lookup"><span data-stu-id="0b9f6-314">jQuery Validate 1.13.1</span></span>](jquery-validate/cdnjqueryvalidate1131.md "jQuery Validation 1.13.1")
- [<span data-ttu-id="0b9f6-315">jQuery Validate 1.13.0</span><span class="sxs-lookup"><span data-stu-id="0b9f6-315">jQuery Validate 1.13.0</span></span>](jquery-validate/cdnjqueryvalidate1130.md "jQuery Validation 1.13.0")
- [<span data-ttu-id="0b9f6-316">jQuery Validate 1.12.0 以降</span><span class="sxs-lookup"><span data-stu-id="0b9f6-316">jQuery Validate 1.12.0</span></span>](jquery-validate/cdnjqueryvalidate1120.md "jQuery Validation 1.12.0")
- [<span data-ttu-id="0b9f6-317">jQuery Validate 1.11.1</span><span class="sxs-lookup"><span data-stu-id="0b9f6-317">jQuery Validate 1.11.1</span></span>](jquery-validate/cdnjqueryvalidate1111.md "jQuery Validation 1.11.1")
- [<span data-ttu-id="0b9f6-318">jQuery Validate 1.11.0</span><span class="sxs-lookup"><span data-stu-id="0b9f6-318">jQuery Validate 1.11.0</span></span>](jquery-validate/cdnjqueryvalidate111.md "jQuery Validation 1.11.0")
- [<span data-ttu-id="0b9f6-319">jQuery Validate 1.10.0</span><span class="sxs-lookup"><span data-stu-id="0b9f6-319">jQuery Validate 1.10.0</span></span>](jquery-validate/cdnjqueryvalidate110.md "jQuery Validation 1.10.0")
- [<span data-ttu-id="0b9f6-320">jQuery の検証1.9</span><span class="sxs-lookup"><span data-stu-id="0b9f6-320">jQuery Validate 1.9</span></span>](jquery-validate/cdnjqueryvalidate19.md "jquery.validate バージョン 1.9")
- [<span data-ttu-id="0b9f6-321">jQuery Validate 1.8.1</span><span class="sxs-lookup"><span data-stu-id="0b9f6-321">jQuery Validate 1.8.1</span></span>](jquery-validate/cdnjqueryvalidate181.md "jquery.validate バージョン 1.8.1")
- [<span data-ttu-id="0b9f6-322">jQuery の検証1.8</span><span class="sxs-lookup"><span data-stu-id="0b9f6-322">jQuery Validate 1.8</span></span>](jquery-validate/cdnjqueryvalidate18.md "jquery.validate バージョン 1.8")
- [<span data-ttu-id="0b9f6-323">jQuery の検証1.7</span><span class="sxs-lookup"><span data-stu-id="0b9f6-323">jQuery Validate 1.7</span></span>](jquery-validate/cdnjqueryvalidate17.md "jquery.validate バージョン 1.7")
- [<span data-ttu-id="0b9f6-324">jQuery Validate 1.6</span><span class="sxs-lookup"><span data-stu-id="0b9f6-324">jQuery Validate 1.6</span></span>](jquery-validate/cdnjqueryvalidate16.md "jQuery Validate 1.6")
- [<span data-ttu-id="0b9f6-325">jQuery Validate 1.5.5</span><span class="sxs-lookup"><span data-stu-id="0b9f6-325">jQuery Validate 1.5.5</span></span>](jquery-validate/cdnjqueryvalidate155.md "jQuery Validate 1.5.5")

<a id="jQuery_Mobile_Releases_on_the_CDN_4"></a>

### <a name="jquery-mobile-releases-on-the-cdn"></a><span data-ttu-id="0b9f6-326">CDN での jQuery Mobile リリース</span><span class="sxs-lookup"><span data-stu-id="0b9f6-326">jQuery Mobile Releases on the CDN</span></span>

<span data-ttu-id="0b9f6-327">JQuery Mobile ライブラリの次のリリースは、この CDN でホストされています。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-327">The following releases of the jQuery Mobile library are hosted on this CDN.</span></span> <span data-ttu-id="0b9f6-328">各リンクをクリックすると、ファイルの実際の一覧が表示されます。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-328">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="0b9f6-329">jQuery Mobile 1.4.5</span><span class="sxs-lookup"><span data-stu-id="0b9f6-329">jQuery Mobile 1.4.5</span></span>](jquery-mobile/cdnjquerymobile145.md "Microsoft Ajax CDN の jQuery Mobile 1.4.5")
- [<span data-ttu-id="0b9f6-330">jQuery Mobile 1.4.2</span><span class="sxs-lookup"><span data-stu-id="0b9f6-330">jQuery Mobile 1.4.2</span></span>](jquery-mobile/cdnjquerymobile142.md "Microsoft Ajax CDN の jQuery Mobile 1.4.2")
- [<span data-ttu-id="0b9f6-331">jQuery Mobile 1.4.1</span><span class="sxs-lookup"><span data-stu-id="0b9f6-331">jQuery Mobile 1.4.1</span></span>](jquery-mobile/cdnjquerymobile141.md "Microsoft Ajax CDN の jQuery Mobile 1.4.1")
- [<span data-ttu-id="0b9f6-332">jQuery Mobile の場合</span><span class="sxs-lookup"><span data-stu-id="0b9f6-332">jQuery Mobile 1.4.0</span></span>](jquery-mobile/cdnjquerymobile140.md "Microsoft Ajax CDN の jQuery Mobile 1.4.0")
- [<span data-ttu-id="0b9f6-333">jQuery Mobile 1.3.2</span><span class="sxs-lookup"><span data-stu-id="0b9f6-333">jQuery Mobile 1.3.2</span></span>](jquery-mobile/cdnjquerymobile132.md "Microsoft Ajax CDN の jQuery Mobile 1.3.2")
- [<span data-ttu-id="0b9f6-334">jQuery Mobile 1.3.1</span><span class="sxs-lookup"><span data-stu-id="0b9f6-334">jQuery Mobile 1.3.1</span></span>](jquery-mobile/cdnjquerymobile131.md "Microsoft Ajax CDN の jQuery Mobile 1.3.1")
- [<span data-ttu-id="0b9f6-335">jQuery Mobile 1.3.0</span><span class="sxs-lookup"><span data-stu-id="0b9f6-335">jQuery Mobile 1.3.0</span></span>](jquery-mobile/cdnjquerymobile130.md "Microsoft Ajax CDN の jQuery Mobile 1.3.0")
- [<span data-ttu-id="0b9f6-336">jQuery Mobile 1.2.0</span><span class="sxs-lookup"><span data-stu-id="0b9f6-336">jQuery Mobile 1.2.0</span></span>](jquery-mobile/cdnjquerymobile120.md "Microsoft Ajax CDN の jQuery Mobile 1.2.0")
- [<span data-ttu-id="0b9f6-337">jQuery Mobile 1.1.2</span><span class="sxs-lookup"><span data-stu-id="0b9f6-337">jQuery Mobile 1.1.2</span></span>](jquery-mobile/cdnjquerymobile112.md "Microsoft Ajax CDN の jQuery Mobile 1.1.2")
- [<span data-ttu-id="0b9f6-338">jQuery Mobile 1.1.1</span><span class="sxs-lookup"><span data-stu-id="0b9f6-338">jQuery Mobile 1.1.1</span></span>](jquery-mobile/cdnjquerymobile111.md "Microsoft Ajax CDN の jQuery Mobile 1.1.1")
- [<span data-ttu-id="0b9f6-339">jQuery Mobile 1.1.0</span><span class="sxs-lookup"><span data-stu-id="0b9f6-339">jQuery Mobile 1.1.0</span></span>](jquery-mobile/cdnjquerymobile110.md "Microsoft Ajax CDN の jQuery Mobile 1.1.0")
- [<span data-ttu-id="0b9f6-340">jQuery Mobile 1.1.0 RC 2</span><span class="sxs-lookup"><span data-stu-id="0b9f6-340">jQuery Mobile 1.1.0 RC 2</span></span>](jquery-mobile/cdnjquerymobile110rc2.md "Microsoft Ajax CDN の jQuery Mobile 1.1.0 RC2")
- [<span data-ttu-id="0b9f6-341">jQuery Mobile 1.0.1</span><span class="sxs-lookup"><span data-stu-id="0b9f6-341">jQuery Mobile 1.0.1</span></span>](jquery-mobile/cdnjquerymobile101.md "Microsoft Ajax CDN の jQuery Mobile 1.0.1")
- [<span data-ttu-id="0b9f6-342">jQuery Mobile 1.0</span><span class="sxs-lookup"><span data-stu-id="0b9f6-342">jQuery Mobile 1.0</span></span>](jquery-mobile/cdnjquerymobile10.md "Microsoft Ajax CDN の jQuery Mobile 1.0")
- [<span data-ttu-id="0b9f6-343">jQuery Mobile 1.0 RC 2</span><span class="sxs-lookup"><span data-stu-id="0b9f6-343">jQuery Mobile 1.0 RC 2</span></span>](jquery-mobile/cdnjquerymobile10rc2.md "Microsoft Ajax CDN の jQuery Mobile 1.0 RC2")
- [<span data-ttu-id="0b9f6-344">jQuery Mobile 1.0 RC 1</span><span class="sxs-lookup"><span data-stu-id="0b9f6-344">jQuery Mobile 1.0 RC 1</span></span>](jquery-mobile/cdnjquerymobile10rc1.md "Microsoft Ajax CDN の jQuery Mobile 1.0 RC1")
- [<span data-ttu-id="0b9f6-345">jQuery Mobile 1.0 beta 3</span><span class="sxs-lookup"><span data-stu-id="0b9f6-345">jQuery Mobile 1.0 beta 3</span></span>](jquery-mobile/cdnjquerymobile10b3.md "Microsoft Ajax CDN の jQuery Mobile 1.0 Beta 3")

<a id="jQuery_Templates_Releases_on_the_CDN_5"></a>

### <a name="jquery-templates-releases-on-the-cdn"></a><span data-ttu-id="0b9f6-346">CDN での jQuery テンプレートのリリース</span><span class="sxs-lookup"><span data-stu-id="0b9f6-346">jQuery Templates Releases on the CDN</span></span>

<span data-ttu-id="0b9f6-347">JQuery Templates プラグインの次のリリースは、この CDN でホストされています。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-347">The following releases of the jQuery Templates plugin are hosted on this CDN.</span></span> <span data-ttu-id="0b9f6-348">各リンクをクリックすると、ファイルの実際の一覧が表示されます。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-348">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="0b9f6-349">jQuery Templates Beta 1</span><span class="sxs-lookup"><span data-stu-id="0b9f6-349">jQuery Templates Beta 1</span></span>](jquery-templates/cdnjquerytemplatesbeta1.md "jQuery Templates Beta 1")

<a id="jQuery_Cycle_Releases_on_the_CDN_6"></a>

### <a name="jquery-cycle-releases-on-the-cdn"></a><span data-ttu-id="0b9f6-350">CDN の jQuery サイクルリリース</span><span class="sxs-lookup"><span data-stu-id="0b9f6-350">jQuery Cycle Releases on the CDN</span></span>

<span data-ttu-id="0b9f6-351">JQuery サイクルプラグインの次のリリースは、この CDN でホストされています。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-351">The following releases of the jQuery Cycle plugin are hosted on this CDN.</span></span> <span data-ttu-id="0b9f6-352">各リンクをクリックすると、ファイルの実際の一覧が表示されます。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-352">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="0b9f6-353">jQuery Cycle 2.99</span><span class="sxs-lookup"><span data-stu-id="0b9f6-353">jQuery Cycle 2.99</span></span>](jquery-cycle/cdnjquerycycle299.md "jQuery Cycle 2.99")
- [<span data-ttu-id="0b9f6-354">jQuery Cycle 2.94</span><span class="sxs-lookup"><span data-stu-id="0b9f6-354">jQuery Cycle 2.94</span></span>](jquery-cycle/cdnjquerycycle294.md "jQuery Cycle 2.94")
- [<span data-ttu-id="0b9f6-355">jQuery Cycle 2.88</span><span class="sxs-lookup"><span data-stu-id="0b9f6-355">jQuery Cycle 2.88</span></span>](jquery-cycle/cdnjquerycycle288.md "jQuery Cycle 2.88")

<a id="jQuery_DataTables_Releases_on_the_CDN_7"></a>

### <a name="jquery-datatables-releases-on-the-cdn"></a><span data-ttu-id="0b9f6-356">CDN での jQuery Datatable のリリース</span><span class="sxs-lookup"><span data-stu-id="0b9f6-356">jQuery DataTables Releases on the CDN</span></span>

<span data-ttu-id="0b9f6-357">JQuery Datatable プラグインの次のリリースは、この CDN でホストされています。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-357">The following releases of the jQuery DataTables plugin are hosted on this CDN.</span></span> <span data-ttu-id="0b9f6-358">各リンクをクリックすると、ファイルの実際の一覧が表示されます。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-358">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="0b9f6-359">jQuery DataTables 1.10.5</span><span class="sxs-lookup"><span data-stu-id="0b9f6-359">jQuery DataTables 1.10.5</span></span>](jquery-datatables/cdnjquerydatatables105.md "jQuery DataTables 1.10.5")
- [<span data-ttu-id="0b9f6-360">jQuery DataTables 1.10.4</span><span class="sxs-lookup"><span data-stu-id="0b9f6-360">jQuery DataTables 1.10.4</span></span>](jquery-datatables/cdnjquerydatatables104.md "jQuery DataTables 1.10.4")
- [<span data-ttu-id="0b9f6-361">jQuery DataTables 1.9.4</span><span class="sxs-lookup"><span data-stu-id="0b9f6-361">jQuery DataTables 1.9.4</span></span>](jquery-datatables/cdnjquerydatatables194.md "jQuery DataTables 1.9.4")
- [<span data-ttu-id="0b9f6-362">jQuery DataTables 1.9.3</span><span class="sxs-lookup"><span data-stu-id="0b9f6-362">jQuery DataTables 1.9.3</span></span>](jquery-datatables/cdnjquerydatatables193.md "jQuery DataTables 1.9.3")
- [<span data-ttu-id="0b9f6-363">jQuery DataTables 1.9.2</span><span class="sxs-lookup"><span data-stu-id="0b9f6-363">jQuery DataTables 1.9.2</span></span>](jquery-datatables/cdnjquerydatatables192.md "jQuery DataTables 1.9.2")
- [<span data-ttu-id="0b9f6-364">jQuery DataTables 1.9.1</span><span class="sxs-lookup"><span data-stu-id="0b9f6-364">jQuery DataTables 1.9.1</span></span>](jquery-datatables/cdnjquerydatatables191.md "jQuery DataTables 1.9.1")
- [<span data-ttu-id="0b9f6-365">jQuery DataTables 1.9.0</span><span class="sxs-lookup"><span data-stu-id="0b9f6-365">jQuery DataTables 1.9.0</span></span>](jquery-datatables/cdnjquerydatatables190.md "jQuery DataTables 1.9.0")
- [<span data-ttu-id="0b9f6-366">jQuery DataTables 1.8.2</span><span class="sxs-lookup"><span data-stu-id="0b9f6-366">jQuery DataTables 1.8.2</span></span>](jquery-datatables/cdnjquerydatatables182.md "jQuery DataTables 1.8.2")

<a id="Modernizr_Releases_on_the_CDN_8"></a>

### <a name="modernizr-releases-on-the-cdn"></a><span data-ttu-id="0b9f6-367">CDN での Modernizr リリース</span><span class="sxs-lookup"><span data-stu-id="0b9f6-367">Modernizr Releases on the CDN</span></span>

<span data-ttu-id="0b9f6-368">次の[Modernizr](http://www.modernizr.com "Modernizr")のリリースは CDN でホストされています。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-368">The following releases of [Modernizr](http://www.modernizr.com "Modernizr") are hosted on the CDN:</span></span>

- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-3.5.0.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.8.3.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.7.2.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.7.1.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.6.2.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-1.7-development-only.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.0.6-development-only.js

<a id="JSHint_Releases_on_the_CDN_10"></a>

### <a name="jshint-releases-on-the-cdn"></a><span data-ttu-id="0b9f6-369">CDN での JSHint リリース</span><span class="sxs-lookup"><span data-stu-id="0b9f6-369">JSHint Releases on the CDN</span></span>

<span data-ttu-id="0b9f6-370">次の[Jshint](http://www.jshint.com "JSHint")のリリースは CDN でホストされています。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-370">The following releases of [JSHint](http://www.jshint.com "JSHint") are hosted on the CDN:</span></span>

- https://ajax.aspnetcdn.com/ajax/jshint/r07/jshint.js

<a id="Knockout_Releases_on_the_CDN_11"></a>

### <a name="knockout-releases-on-the-cdn"></a><span data-ttu-id="0b9f6-371">CDN でのノックアウトリリース</span><span class="sxs-lookup"><span data-stu-id="0b9f6-371">Knockout Releases on the CDN</span></span>

<span data-ttu-id="0b9f6-372">次の[ノックアウト](http://www.knockoutjs.com "抜き合わせ")のリリースは CDN でホストされています。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-372">The following releases of [Knockout](http://www.knockoutjs.com "Knockout") are hosted on the CDN:</span></span>

- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.1.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.1.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.1.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.1.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.0.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.0.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.1.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.1.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.2.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.2.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.3.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.3.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.1.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.1.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.2.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.2.debug.js

<a id="Globalize_Releases_on_the_CDN_12"></a>

### <a name="globalize-releases-on-the-cdn"></a><span data-ttu-id="0b9f6-373">CDN でのグローバライズのリリース</span><span class="sxs-lookup"><span data-stu-id="0b9f6-373">Globalize Releases on the CDN</span></span>

<span data-ttu-id="0b9f6-374">次の[グローバライズ](https://github.com/jquery/globalize "グローバライズ")のリリースは CDN でホストされています。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-374">The following releases of [Globalize](https://github.com/jquery/globalize "Globalize") are hosted on the CDN:</span></span>

#### <a name="globalize-version-100"></a><span data-ttu-id="0b9f6-375">グローバライズバージョン1.0.0</span><span class="sxs-lookup"><span data-stu-id="0b9f6-375">Globalize version 1.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/node-main.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/currency.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/date.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/message.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/number.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/plural.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/relative-time.js

#### <a name="globalize-version-011"></a><span data-ttu-id="0b9f6-376">グローバライズバージョン0.1.1</span><span class="sxs-lookup"><span data-stu-id="0b9f6-376">Globalize version 0.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/globalize.min.js
- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/globalize.js
- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/cultures/globalize.cultures.js

    - <span data-ttu-id="0b9f6-377">すべてのカルチャ</span><span class="sxs-lookup"><span data-stu-id="0b9f6-377">all cultures</span></span>
- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/cultures/globalize.culture.{culture-code}.js

    - <span data-ttu-id="0b9f6-378">"{Culture-code}" を目的のカルチャコード (たとえば、en-GB = = CDN = = の Microsoft ファイル) に置き換えます。これらのライブラリは、Microsoft によってアップロードされました。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-378">Replace "{culture-code}" with the desired culture code, e.g. globalize.culture.en-GB.js== Microsoft Files on the CDN ==These libraries were uploaded by Microsoft.</span></span>

<a id="Respond_Releases_on_the_CDN_13"></a>

### <a name="respond-releases-on-the-cdn"></a><span data-ttu-id="0b9f6-379">CDN でのリリースの応答</span><span class="sxs-lookup"><span data-stu-id="0b9f6-379">Respond Releases on the CDN</span></span>

<span data-ttu-id="0b9f6-380">[応答](https://github.com/scottjehl/Respond "応答")の次のリリースは CDN でホストされます。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-380">The following releases of [Respond](https://github.com/scottjehl/Respond "Respond") are hosted on the CDN:</span></span>

#### <a name="respond-version-142"></a><span data-ttu-id="0b9f6-381">バージョン1.4.2 に応答する</span><span class="sxs-lookup"><span data-stu-id="0b9f6-381">Respond version 1.4.2</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.min.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.matchmedia.addListener.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.matchmedia.addListener.min.js

#### <a name="respond-version-141"></a><span data-ttu-id="0b9f6-382">バージョン1.4.1 に応答する</span><span class="sxs-lookup"><span data-stu-id="0b9f6-382">Respond version 1.4.1</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.min.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.matchmedia.addListener.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.matchmedia.addListener.min.js

#### <a name="respond-version-140"></a><span data-ttu-id="0b9f6-383">バージョンを応答する</span><span class="sxs-lookup"><span data-stu-id="0b9f6-383">Respond version 1.4.0</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.min.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.matchmedia.addListener.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.matchmedia.addListener.min.js

#### <a name="respond-version-130"></a><span data-ttu-id="0b9f6-384">応答バージョン1.3.0</span><span class="sxs-lookup"><span data-stu-id="0b9f6-384">Respond version 1.3.0</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.3.0/respond.js

#### <a name="respond-version-120"></a><span data-ttu-id="0b9f6-385">応答バージョン1.2.0</span><span class="sxs-lookup"><span data-stu-id="0b9f6-385">Respond version 1.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.2.0/respond.js

<a id="Bootstrap_Releases_on_the_CDN_14"></a>

### <a name="bootstrap-releases-on-the-cdn"></a><span data-ttu-id="0b9f6-386">CDN でのブートストラップリリース</span><span class="sxs-lookup"><span data-stu-id="0b9f6-386">Bootstrap Releases on the CDN</span></span>

<span data-ttu-id="0b9f6-387">[Getbootstrap.com](http://getbootstrap.com "getbootstrap.com")ブートストラップの次のリリースは、CDN でホストされます。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-387">The following releases of [getbootstrap.com](http://getbootstrap.com "getbootstrap.com") bootstrap are hosted on the CDN:</span></span>

#### <a name="bootstrap-version-441"></a><span data-ttu-id="0b9f6-388">ブートストラップバージョン4.4.1</span><span class="sxs-lookup"><span data-stu-id="0b9f6-388">Bootstrap version 4.4.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/bootstrap.bundle.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap-grid.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap-grid.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap-grid.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap-reboot.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap-reboot.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap-reboot.css.map

#### <a name="bootstrap-version-431"></a><span data-ttu-id="0b9f6-389">ブートストラップバージョン4.3.1</span><span class="sxs-lookup"><span data-stu-id="0b9f6-389">Bootstrap version 4.3.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/bootstrap.bundle.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap-grid.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap-grid.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap-grid.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap-reboot.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap-reboot.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap-reboot.css.map

#### <a name="bootstrap-version-421"></a><span data-ttu-id="0b9f6-390">ブートストラップバージョン4.2.1</span><span class="sxs-lookup"><span data-stu-id="0b9f6-390">Bootstrap version 4.2.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/bootstrap.bundle.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-grid.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-grid.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-grid.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-reboot.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-reboot.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-reboot.css.map

#### <a name="bootstrap-version-411"></a><span data-ttu-id="0b9f6-391">ブートストラップバージョン4.1.1</span><span class="sxs-lookup"><span data-stu-id="0b9f6-391">Bootstrap version 4.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/bootstrap.bundle.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-grid.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-grid.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-grid.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-reboot.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-reboot.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-reboot.css.map

#### <a name="bootstrap-version-400"></a><span data-ttu-id="0b9f6-392">ブートストラップバージョン4.0.0</span><span class="sxs-lookup"><span data-stu-id="0b9f6-392">Bootstrap version 4.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/bootstrap.bundle.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-grid.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-grid.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-grid.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-reboot.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-reboot.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-reboot.css.map

#### <a name="bootstrap-version-341"></a><span data-ttu-id="0b9f6-393">ブートストラップバージョン3.4.1</span><span class="sxs-lookup"><span data-stu-id="0b9f6-393">Bootstrap version 3.4.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-340"></a><span data-ttu-id="0b9f6-394">ブートストラップバージョン3.4.0</span><span class="sxs-lookup"><span data-stu-id="0b9f6-394">Bootstrap version 3.4.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-337"></a><span data-ttu-id="0b9f6-395">ブートストラップバージョン3.3.7</span><span class="sxs-lookup"><span data-stu-id="0b9f6-395">Bootstrap version 3.3.7</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-336"></a><span data-ttu-id="0b9f6-396">ブートストラップバージョン3.3.6</span><span class="sxs-lookup"><span data-stu-id="0b9f6-396">Bootstrap version 3.3.6</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-335"></a><span data-ttu-id="0b9f6-397">ブートストラップバージョン3.3.5</span><span class="sxs-lookup"><span data-stu-id="0b9f6-397">Bootstrap version 3.3.5</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-334"></a><span data-ttu-id="0b9f6-398">ブートストラップバージョン3.3.4</span><span class="sxs-lookup"><span data-stu-id="0b9f6-398">Bootstrap version 3.3.4</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-332"></a><span data-ttu-id="0b9f6-399">ブートストラップバージョン3.3.2</span><span class="sxs-lookup"><span data-stu-id="0b9f6-399">Bootstrap version 3.3.2</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-331"></a><span data-ttu-id="0b9f6-400">ブートストラップバージョン3.3.1</span><span class="sxs-lookup"><span data-stu-id="0b9f6-400">Bootstrap version 3.3.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-330"></a><span data-ttu-id="0b9f6-401">ブートストラップバージョン3.3.0</span><span class="sxs-lookup"><span data-stu-id="0b9f6-401">Bootstrap version 3.3.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-320"></a><span data-ttu-id="0b9f6-402">ブートストラップバージョン3.2.0</span><span class="sxs-lookup"><span data-stu-id="0b9f6-402">Bootstrap version 3.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-311"></a><span data-ttu-id="0b9f6-403">ブートストラップバージョン3.1.1</span><span class="sxs-lookup"><span data-stu-id="0b9f6-403">Bootstrap version 3.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-310"></a><span data-ttu-id="0b9f6-404">ブートストラップバージョン3.1.0</span><span class="sxs-lookup"><span data-stu-id="0b9f6-404">Bootstrap version 3.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-303"></a><span data-ttu-id="0b9f6-405">ブートストラップバージョン3.0.3</span><span class="sxs-lookup"><span data-stu-id="0b9f6-405">Bootstrap version 3.0.3</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-302"></a><span data-ttu-id="0b9f6-406">ブートストラップバージョン3.0.2</span><span class="sxs-lookup"><span data-stu-id="0b9f6-406">Bootstrap version 3.0.2</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-301"></a><span data-ttu-id="0b9f6-407">ブートストラップバージョン3.0.1</span><span class="sxs-lookup"><span data-stu-id="0b9f6-407">Bootstrap version 3.0.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-300"></a><span data-ttu-id="0b9f6-408">ブートストラップバージョン3.0.0</span><span class="sxs-lookup"><span data-stu-id="0b9f6-408">Bootstrap version 3.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-232"></a><span data-ttu-id="0b9f6-409">ブートストラップバージョン2.3.2</span><span class="sxs-lookup"><span data-stu-id="0b9f6-409">Bootstrap version 2.3.2</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap-responsive.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap-responsive.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/img/glyphicons-halflings.png
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/img/glyphicons-halflings-white.png

#### <a name="bootstrap-version-231"></a><span data-ttu-id="0b9f6-410">ブートストラップバージョン2.3.1</span><span class="sxs-lookup"><span data-stu-id="0b9f6-410">Bootstrap version 2.3.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap-responsive.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap-responsive.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/img/glyphicons-halflings.png
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/img/glyphicons-halflings-white.png

<a id="BootstrapTouchCarousel_Releases_on_the_CDN_18"></a>

### <a name="bootstrap-touchcarousel-releases-on-the-cdn"></a><span data-ttu-id="0b9f6-411">CDN でのブートストラップ TouchCarousel のリリース</span><span class="sxs-lookup"><span data-stu-id="0b9f6-411">Bootstrap TouchCarousel Releases on the CDN</span></span>

<span data-ttu-id="0b9f6-412">次のリリースの[https://github.com/ixisio/bootstrap-touch-carousel](https://github.com/ixisio/bootstrap-touch-carousel "https://github.com/ixisio/bootstrap-touch-carousel")ブートストラップ TouchCarousel リリースは CDN でホストされています。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-412">The following releases of [https://github.com/ixisio/bootstrap-touch-carousel](https://github.com/ixisio/bootstrap-touch-carousel "https://github.com/ixisio/bootstrap-touch-carousel") Bootstrap TouchCarousel releases are hosted on the CDN:</span></span>

#### <a name="bootstrap-touchcarousel-version-080"></a><span data-ttu-id="0b9f6-413">ブートストラップ TouchCarousel バージョン0.8.0 以降</span><span class="sxs-lookup"><span data-stu-id="0b9f6-413">Bootstrap TouchCarousel version 0.8.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap-touch-carousel/0.8.0/css/bootstrap-touch-carousel.css
- https://ajax.aspnetcdn.com/ajax/bootstrap-touch-carousel/0.8.0/js/bootstrap-touch-carousel.js

<a id="Hammerjs_Releases_on_the_CDN_19"></a>

### <a name="hammerjs-releases-on-the-cdn"></a><span data-ttu-id="0b9f6-414">CDN でのハンマーのリリース</span><span class="sxs-lookup"><span data-stu-id="0b9f6-414">Hammer.js Releases on the CDN</span></span>

<span data-ttu-id="0b9f6-415">次のリリースの[http://hammerjs.github.io/](http://hammerjs.github.io/ "http://hammerjs.github.io/")のバージョンのハンマーが CDN でホストされています。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-415">The following releases of [http://hammerjs.github.io/](http://hammerjs.github.io/ "http://hammerjs.github.io/") Hammer.js releases are hosted on the CDN:</span></span>

#### <a name="hammerjs-version-204"></a><span data-ttu-id="0b9f6-416">2\.0.4 のバージョン</span><span class="sxs-lookup"><span data-stu-id="0b9f6-416">Hammer.js version 2.0.4</span></span>

- https://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.js
- https://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.min.js
- https://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.min.map

<a id="ASPNET_Web_Forms_and_Ajax_Releases_on_the_CDN_15"></a>

### <a name="aspnet-web-forms-and-ajax-releases-on-the-cdn"></a><span data-ttu-id="0b9f6-417">CDN での ASP.NET Web フォームと Ajax リリース</span><span class="sxs-lookup"><span data-stu-id="0b9f6-417">ASP.NET Web Forms and Ajax Releases on the CDN</span></span>

<span data-ttu-id="0b9f6-418">ASP.NET Ajax ライブラリの次のリリースは、CDN でホストされています。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-418">The following releases of the ASP.NET Ajax Library are hosted on the CDN.</span></span> <span data-ttu-id="0b9f6-419">各リンクをクリックすると、ファイルの実際の一覧が表示されます。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-419">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="0b9f6-420">ASP.NET Web フォームと Ajax バージョン4.5.2</span><span class="sxs-lookup"><span data-stu-id="0b9f6-420">ASP.NET Web Forms and Ajax version 4.5.2</span></span>](cdnajax452.md "ASP.NET Web フォームと Ajax 4.5.2")
- [<span data-ttu-id="0b9f6-421">ASP.NET Web Forms および Ajax version 4</span><span class="sxs-lookup"><span data-stu-id="0b9f6-421">ASP.NET Web Forms and Ajax version 4</span></span>](cdnajax4.md "ASP.NET Web フォームと Ajax 4")
- [<span data-ttu-id="0b9f6-422">ASP.NET Ajax バージョン3.5</span><span class="sxs-lookup"><span data-stu-id="0b9f6-422">ASP.NET Ajax version 3.5</span></span>](cdnajax35.md "ASP.NET Ajax 3.5")

<a id="ASPNET_MVC_Releases_on_the_CDN_16"></a>

### <a name="aspnet-mvc-releases-on-the-cdn"></a><span data-ttu-id="0b9f6-423">CDN での ASP.NET MVC リリース</span><span class="sxs-lookup"><span data-stu-id="0b9f6-423">ASP.NET MVC Releases on the CDN</span></span>

<span data-ttu-id="0b9f6-424">次の ASP.NET MVC JavaScript ファイルは、この CDN でホストされています。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-424">The following ASP.NET MVC JavaScript files are hosted on this CDN:</span></span>

#### <a name="aspnet-mvc-523"></a><span data-ttu-id="0b9f6-425">ASP.NET MVC 5.2.3</span><span class="sxs-lookup"><span data-stu-id="0b9f6-425">ASP.NET MVC 5.2.3</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/5.2.3/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/5.2.3/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-51"></a><span data-ttu-id="0b9f6-426">ASP.NET MVC 5.1</span><span class="sxs-lookup"><span data-stu-id="0b9f6-426">ASP.NET MVC 5.1</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/5.1/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/5.1/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-50"></a><span data-ttu-id="0b9f6-427">ASP.NET MVC 5.0</span><span class="sxs-lookup"><span data-stu-id="0b9f6-427">ASP.NET MVC 5.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/5.0/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/5.0/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-40"></a><span data-ttu-id="0b9f6-428">ASP.NET MVC 4.0</span><span class="sxs-lookup"><span data-stu-id="0b9f6-428">ASP.NET MVC 4.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/4.0/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/4.0/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-30"></a><span data-ttu-id="0b9f6-429">ASP.NET MVC 3.0</span><span class="sxs-lookup"><span data-stu-id="0b9f6-429">ASP.NET MVC 3.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.unobtrusive-ajax.js
- https://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.unobtrusive-ajax.min.js
- https://ajax.aspnetcdn.com/ajax/jquery.unobtrusive-ajax/3.2.5/jquery.unobtrusive-ajax.js
- https://ajax.aspnetcdn.com/ajax/jquery.unobtrusive-ajax/3.2.5/jquery.unobtrusive-ajax.min.js 
- https://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.validate.unobtrusive.min.js
- https://ajax.aspnetcdn.com/ajax/jquery.validation.unobtrusive/3.2.10/jquery.validate.unobtrusive.js 
- https://ajax.aspnetcdn.com/ajax/jquery.validation.unobtrusive/3.2.10/jquery.validate.unobtrusive.min.js
- https://ajax.aspnetcdn.com/ajax/mvc/3.0/MicrosoftMvcAjax.js
- https://ajax.aspnetcdn.com/ajax/mvc/3.0/MicrosoftMvcAjax.debug.js

#### <a name="aspnet-mvc-20"></a><span data-ttu-id="0b9f6-430">ASP.NET MVC 2.0</span><span class="sxs-lookup"><span data-stu-id="0b9f6-430">ASP.NET MVC 2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/2.0/MicrosoftMvcAjax.js
- https://ajax.aspnetcdn.com/ajax/mvc/2.0/MicrosoftMvcAjax.debug.js

#### <a name="aspnet-mvc-10"></a><span data-ttu-id="0b9f6-431">ASP.NET MVC 1.0</span><span class="sxs-lookup"><span data-stu-id="0b9f6-431">ASP.NET MVC 1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/1.0/MicrosoftMvcAjax.js
- https://ajax.aspnetcdn.com/ajax/mvc/1.0/MicrosoftMvcAjax.debug.js

<a id="ASPNET_SignalR_Releases_on_the_CDN_17"></a>

### <a name="aspnet-signalr-releases-on-the-cdn"></a><span data-ttu-id="0b9f6-432">CDN での ASP.NET SignalR リリース</span><span class="sxs-lookup"><span data-stu-id="0b9f6-432">ASP.NET SignalR Releases on the CDN</span></span>

<span data-ttu-id="0b9f6-433">次の ASP.NET SignalR JavaScript ファイルは、この CDN でホストされます。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-433">The following ASP.NET SignalR JavaScript files are hosted on this CDN:</span></span>

#### <a name="aspnet-signalr-222"></a><span data-ttu-id="0b9f6-434">ASP.NET SignalR 2.2.2</span><span class="sxs-lookup"><span data-stu-id="0b9f6-434">ASP.NET SignalR 2.2.2</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.2.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.2.js

#### <a name="aspnet-signalr-221"></a><span data-ttu-id="0b9f6-435">ASP.NET SignalR 2.2.1</span><span class="sxs-lookup"><span data-stu-id="0b9f6-435">ASP.NET SignalR 2.2.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.1.js

#### <a name="aspnet-signalr-220"></a><span data-ttu-id="0b9f6-436">ASP.NET SignalR 2.2.0</span><span class="sxs-lookup"><span data-stu-id="0b9f6-436">ASP.NET SignalR 2.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.0.js

#### <a name="aspnet-signalr-210"></a><span data-ttu-id="0b9f6-437">ASP.NET SignalR 2.1.0</span><span class="sxs-lookup"><span data-stu-id="0b9f6-437">ASP.NET SignalR 2.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.1.0.js

#### <a name="aspnet-signalr-203"></a><span data-ttu-id="0b9f6-438">ASP.NET SignalR 2.0.3</span><span class="sxs-lookup"><span data-stu-id="0b9f6-438">ASP.NET SignalR 2.0.3</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.3.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.3.js

#### <a name="aspnet-signalr-202"></a><span data-ttu-id="0b9f6-439">ASP.NET SignalR 2.0.2</span><span class="sxs-lookup"><span data-stu-id="0b9f6-439">ASP.NET SignalR 2.0.2</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.2.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.2.js

#### <a name="aspnet-signalr-201"></a><span data-ttu-id="0b9f6-440">ASP.NET SignalR 2.0.1</span><span class="sxs-lookup"><span data-stu-id="0b9f6-440">ASP.NET SignalR 2.0.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.1.js

#### <a name="aspnet-signalr-200"></a><span data-ttu-id="0b9f6-441">ASP.NET SignalR 2.0.0</span><span class="sxs-lookup"><span data-stu-id="0b9f6-441">ASP.NET SignalR 2.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.0.js

#### <a name="aspnet-signalr-113"></a><span data-ttu-id="0b9f6-442">ASP.NET SignalR 1.1.3</span><span class="sxs-lookup"><span data-stu-id="0b9f6-442">ASP.NET SignalR 1.1.3</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.3.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.3.js

#### <a name="aspnet-signalr-112"></a><span data-ttu-id="0b9f6-443">ASP.NET SignalR 1.1.2</span><span class="sxs-lookup"><span data-stu-id="0b9f6-443">ASP.NET SignalR 1.1.2</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.2.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.2.js

#### <a name="aspnet-signalr-111"></a><span data-ttu-id="0b9f6-444">ASP.NET SignalR 1.1.1</span><span class="sxs-lookup"><span data-stu-id="0b9f6-444">ASP.NET SignalR 1.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.1.js

#### <a name="aspnet-signalr-110"></a><span data-ttu-id="0b9f6-445">ASP.NET SignalR 1.1.0</span><span class="sxs-lookup"><span data-stu-id="0b9f6-445">ASP.NET SignalR 1.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.0.js

#### <a name="aspnet-signalr-101"></a><span data-ttu-id="0b9f6-446">ASP.NET SignalR 1.0.1</span><span class="sxs-lookup"><span data-stu-id="0b9f6-446">ASP.NET SignalR 1.0.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.0.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.0.1.js

<span data-ttu-id="0b9f6-447">CDN の使用条件の詳細については、「 [Microsoft AJAX Cdn 使用条件](https://www.asp.net/terms-of-use "Microsoft Ajax CDN 使用条件")」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="0b9f6-447">For information about the terms of use for the CDN, see [Microsoft Ajax CDN Terms of Use](https://www.asp.net/terms-of-use "Microsoft Ajax CDN Terms of Use").</span></span>
