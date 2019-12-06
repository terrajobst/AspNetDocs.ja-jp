---
title: ASP.NET で SameSite cookie を使用する
author: rick-anderson
description: を使用して ASP.NET でクッキーを SameSite する方法について説明します。
ms.author: riande
ms.date: 12/03/2019
uid: samesite/system-web-samesite
ms.openlocfilehash: 40e5c13b6834912c13b41cbfad7da8cd84ca6c8b
ms.sourcegitcommit: 969e7db924ebad3cc0f0cb0d65d148e8b9221b9a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/06/2019
ms.locfileid: "74902010"
---
# <a name="work-with-samesite-cookies-in-aspnet"></a><span data-ttu-id="10359-103">ASP.NET で SameSite cookie を使用する</span><span class="sxs-lookup"><span data-stu-id="10359-103">Work with SameSite cookies in ASP.NET</span></span>

<span data-ttu-id="10359-104">作成者: [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="10359-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="10359-105">SameSite は、クロスサイトリクエスト偽造 (CSRF) 攻撃に対して何らかの保護を提供するように設計された[IETF](https://ietf.org/about/)ドラフトです。</span><span class="sxs-lookup"><span data-stu-id="10359-105">SameSite is an [IETF](https://ietf.org/about/) draft designed to provide some protection against cross-site request forgery (CSRF) attacks.</span></span> <span data-ttu-id="10359-106">[SameSite 2019 のドラフト](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00):</span><span class="sxs-lookup"><span data-stu-id="10359-106">The [SameSite 2019 draft](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00):</span></span>

* <span data-ttu-id="10359-107">クッキーを既定で `SameSite=Lax` として扱います。</span><span class="sxs-lookup"><span data-stu-id="10359-107">Treats cookies as `SameSite=Lax` by default.</span></span>
* <span data-ttu-id="10359-108">クロスサイト配信を有効にするために `SameSite=None` を明示的にアサートする cookie の状態を `Secure`としてマークする必要があります。</span><span class="sxs-lookup"><span data-stu-id="10359-108">States cookies that explicitly assert `SameSite=None` in order to enable cross-site delivery should be marked as `Secure`.</span></span>

<span data-ttu-id="10359-109">`Lax` は、ほとんどのアプリ cookie で機能します。</span><span class="sxs-lookup"><span data-stu-id="10359-109">`Lax` works for most app cookies.</span></span> <span data-ttu-id="10359-110">[OpenID connect](https://openid.net/connect/) (oidc) や[ws-federation](https://auth0.com/docs/protocols/ws-fed)のような認証形式では、既定で POST ベースのリダイレクトが設定されます。</span><span class="sxs-lookup"><span data-stu-id="10359-110">Some forms of authentication like [OpenID Connect](https://openid.net/connect/) (OIDC) and [WS-Federation](https://auth0.com/docs/protocols/ws-fed) default to POST based redirects.</span></span> <span data-ttu-id="10359-111">POST ベースのリダイレクトによって SameSite ブラウザーの保護がトリガーされるため、これらのコンポーネントの SameSite は無効になります。</span><span class="sxs-lookup"><span data-stu-id="10359-111">The POST based redirects trigger the SameSite browser protections, so SameSite is disabled for these components.</span></span> <span data-ttu-id="10359-112">ほとんどの[OAuth](https://oauth.net/)ログインは、要求フローの違いによって影響を受けません。</span><span class="sxs-lookup"><span data-stu-id="10359-112">Most [OAuth](https://oauth.net/) logins are not affected due to differences in how the request flows.</span></span>

<span data-ttu-id="10359-113">`None` パラメーターを指定すると、以前の[2016 ドラフト標準](https://tools.ietf.org/html/draft-west-first-party-cookies-07)(iOS 12 など) を実装したクライアントとの互換性の問題が発生します。</span><span class="sxs-lookup"><span data-stu-id="10359-113">The `None` parameter causes compatibility problems with clients that implemented the prior [2016 draft standard](https://tools.ietf.org/html/draft-west-first-party-cookies-07) (for example, iOS 12).</span></span> <span data-ttu-id="10359-114">このドキュメントの「[古いブラウザーのサポート](#sob)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="10359-114">See [Supporting older browsers](#sob) in this document.</span></span>

<span data-ttu-id="10359-115">Cookie を生成する各 ASP.NET Core コンポーネントは、SameSite が適切かどうかを判断する必要があります。</span><span class="sxs-lookup"><span data-stu-id="10359-115">Each ASP.NET Core component that emits cookies needs to decide if SameSite is appropriate.</span></span>

## <a name="api-usage-with-samesite"></a><span data-ttu-id="10359-116">SameSite を使用した API の使用</span><span class="sxs-lookup"><span data-stu-id="10359-116">API usage with SameSite</span></span>

<span data-ttu-id="10359-117">[SameSite プロパティを](/dotnet/api/system.web.httpcookie.samesite#System_Web_HttpCookie_SameSite)参照してください HttpCookie</span><span class="sxs-lookup"><span data-stu-id="10359-117">See [HttpCookie.SameSite Property](/dotnet/api/system.web.httpcookie.samesite#System_Web_HttpCookie_SameSite)</span></span>

## <a name="history-and-changes"></a><span data-ttu-id="10359-118">履歴と変更</span><span class="sxs-lookup"><span data-stu-id="10359-118">History and changes</span></span>

<span data-ttu-id="10359-119">SameSite のサポートは、 [2016 ドラフト標準](https://tools.ietf.org/html/draft-west-first-party-cookies-07#section-4.1)を使用して最初に .net 4.7.2 に実装されました。</span><span class="sxs-lookup"><span data-stu-id="10359-119">SameSite support was first implemented in .NET 4.7.2 using the [2016 draft standard](https://tools.ietf.org/html/draft-west-first-party-cookies-07#section-4.1).</span></span>

<span data-ttu-id="10359-120">Windows の2019年11月19日の更新プログラムで、.NET 4.7.2 + が2016標準から2019標準に更新されました。</span><span class="sxs-lookup"><span data-stu-id="10359-120">The November 19, 2019 updates for Windows updated .NET 4.7.2+ from the 2016 standard to the 2019 standard.</span></span> <span data-ttu-id="10359-121">その他のバージョンの Windows では、追加の更新が予定されています。</span><span class="sxs-lookup"><span data-stu-id="10359-121">Additional updates are forthcoming for other versions of Windows.</span></span> <span data-ttu-id="10359-122">詳細については、次の KB を参照してください。</span><span class="sxs-lookup"><span data-stu-id="10359-122">See the following KB's for more information:</span></span>

* [<span data-ttu-id="10359-123">サポート技術情報の記事4531182</span><span class="sxs-lookup"><span data-stu-id="10359-123">KB article 4531182</span></span>](https://support.microsoft.com/help/4531182/kb4531182)
* [<span data-ttu-id="10359-124">サポート技術情報の記事4524421</span><span class="sxs-lookup"><span data-stu-id="10359-124">KB article 4524421</span></span>](https://support.microsoft.com/help/4524421/kb4524421)

 <span data-ttu-id="10359-125">SameSite 仕様の2019ドラフト:</span><span class="sxs-lookup"><span data-stu-id="10359-125">The 2019 draft of the SameSite specification:</span></span>

* <span data-ttu-id="10359-126">は、2016ドラフトとの下位互換性が**ありません**。</span><span class="sxs-lookup"><span data-stu-id="10359-126">Is **not** backwards compatible with the 2016 draft.</span></span> <span data-ttu-id="10359-127">詳細については、このドキュメントの「[古いブラウザーのサポート](#sob)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="10359-127">For more information, see [Supporting older browsers](#sob) in this document.</span></span>
* <span data-ttu-id="10359-128">Cookie を既定で `SameSite=Lax` として扱うことを指定します。</span><span class="sxs-lookup"><span data-stu-id="10359-128">Specifies cookies are treated as `SameSite=Lax` by default.</span></span>
* <span data-ttu-id="10359-129">クロスサイト配信を有効にするために `SameSite=None` を明示的にアサートする cookie を `Secure`としてマークする必要があることを指定します。</span><span class="sxs-lookup"><span data-stu-id="10359-129">Specifies cookies that explicitly assert `SameSite=None` in order to enable cross-site delivery should be marked as `Secure`.</span></span> <span data-ttu-id="10359-130">`None` は、オプトアウトする新しいエントリです。</span><span class="sxs-lookup"><span data-stu-id="10359-130">`None` is a new entry to opt out.</span></span>
* <span data-ttu-id="10359-131">は、上記の KB に記載されているように発行された修正プログラムによってサポートされています。</span><span class="sxs-lookup"><span data-stu-id="10359-131">Is supported by patches issued as described in the KB's listed above.</span></span>
* <span data-ttu-id="10359-132">[2 月 2020](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)日に既定で[Chrome](https://chromestatus.com/feature/5088147346030592)によって有効になるようにスケジュールされています。</span><span class="sxs-lookup"><span data-stu-id="10359-132">Is scheduled to be enabled by [Chrome](https://chromestatus.com/feature/5088147346030592) by default in [Feb 2020](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html).</span></span> <span data-ttu-id="10359-133">ブラウザーは2019でこの標準への移行を開始しました。</span><span class="sxs-lookup"><span data-stu-id="10359-133">Browsers started moving to this standard in 2019.</span></span>

<a name="sob"></a>

## <a name="supporting-older-browsers"></a><span data-ttu-id="10359-134">古いブラウザーのサポート</span><span class="sxs-lookup"><span data-stu-id="10359-134">Supporting older browsers</span></span>

<span data-ttu-id="10359-135">2016 SameSite 標準では、不明な値を `SameSite=Strict` 値として処理する必要があることが義務付けられています。</span><span class="sxs-lookup"><span data-stu-id="10359-135">The 2016 SameSite standard mandated that unknown values must be treated as `SameSite=Strict` values.</span></span> <span data-ttu-id="10359-136">2016 SameSite 標準をサポートする古いブラウザーからアクセスされるアプリは、値が `None`の SameSite プロパティを取得すると壊れます。</span><span class="sxs-lookup"><span data-stu-id="10359-136">Apps accessed from older browsers which support the 2016 SameSite standard may break when they get a SameSite property with a value of `None`.</span></span> <span data-ttu-id="10359-137">Web apps が古いブラウザーをサポートする予定の場合は、ブラウザーの検出を実装する必要があります。</span><span class="sxs-lookup"><span data-stu-id="10359-137">Web apps must implement browser detection if they intend to support older browsers.</span></span> <span data-ttu-id="10359-138">ASP.NET は、ユーザーエージェントの値が変動し頻繁に変更されるため、ブラウザーの検出を実装しません。</span><span class="sxs-lookup"><span data-stu-id="10359-138">ASP.NET doesn't implement browser detection because User-Agents values are highly volatile and change frequently.</span></span> <span data-ttu-id="10359-139"><xref:HTTP.HttpCookie> 呼び出しサイトで、次のコードを呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="10359-139">The following code can be called at the <xref:HTTP.HttpCookie> call site:</span></span>

[!code-csharp[](sample/SameSiteCheck.cs?name=snippet)]

<span data-ttu-id="10359-140">前のサンプルの `MyUserAgentDetectionLib.DisallowsSameSiteNone` は、ユーザーエージェントが SameSite `None`をサポートしていないかどうかを検出するユーザー指定のライブラリです。</span><span class="sxs-lookup"><span data-stu-id="10359-140">In the preceding sample, `MyUserAgentDetectionLib.DisallowsSameSiteNone` is a user supplied library that detects if the user agent doesn't support SameSite `None`.</span></span> <span data-ttu-id="10359-141">次のコードは、`DisallowsSameSiteNone` メソッドの例を示しています。</span><span class="sxs-lookup"><span data-stu-id="10359-141">The following code shows a sample `DisallowsSameSiteNone` method:</span></span>

> [!WARNING]
> <span data-ttu-id="10359-142">次のコードは、デモンストレーションのみを対象としています。</span><span class="sxs-lookup"><span data-stu-id="10359-142">The following code is for demonstration only:</span></span>
> * <span data-ttu-id="10359-143">完全であるとは限りません。</span><span class="sxs-lookup"><span data-stu-id="10359-143">It should not be considered complete.</span></span>
> * <span data-ttu-id="10359-144">管理されていないか、サポートされていません。</span><span class="sxs-lookup"><span data-stu-id="10359-144">It is not maintained or supported.</span></span>

[!code-csharp[](sample/SameSiteCheck.cs?name=snippet2)]

## <a name="test-apps-for-samesite-problems"></a><span data-ttu-id="10359-145">SameSite 問題のアプリをテストする</span><span class="sxs-lookup"><span data-stu-id="10359-145">Test apps for SameSite problems</span></span>

<span data-ttu-id="10359-146">サードパーティのログインによってなどのリモートサイトと対話するアプリでは、次の操作を行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="10359-146">Apps that interact with remote sites such as through third-party login need to:</span></span>

* <span data-ttu-id="10359-147">複数のブラウザーで相互作用をテストします。</span><span class="sxs-lookup"><span data-stu-id="10359-147">Test the interaction on multiple browsers.</span></span>
* <span data-ttu-id="10359-148">このドキュメントで説明され[ているブラウザーの検出と軽減策](#sob)を適用します。</span><span class="sxs-lookup"><span data-stu-id="10359-148">Apply the [browser detection and mitigation](#sob) discussed in this document.</span></span>

<span data-ttu-id="10359-149">新しい SameSite 動作にオプトインできるクライアントバージョンを使用して、web アプリをテストします。</span><span class="sxs-lookup"><span data-stu-id="10359-149">Test web apps using a client version that can opt-in to the new SameSite behavior.</span></span> <span data-ttu-id="10359-150">Chrome、Firefox、Chromium Edge には、テストに使用できる新しいオプトイン機能フラグがあります。</span><span class="sxs-lookup"><span data-stu-id="10359-150">Chrome, Firefox, and Chromium Edge all have new opt-in feature flags that can be used for testing.</span></span> <span data-ttu-id="10359-151">アプリが SameSite パッチを適用したら、古いクライアントバージョン (特に Safari) を使用してテストします。</span><span class="sxs-lookup"><span data-stu-id="10359-151">After your app applies the SameSite patches, test it with older client versions, especially Safari.</span></span> <span data-ttu-id="10359-152">詳細については、このドキュメントの「[古いブラウザーのサポート](#sob)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="10359-152">For more information, see [Supporting older browsers](#sob) in this document.</span></span>

### <a name="test-with-chrome"></a><span data-ttu-id="10359-153">Chrome を使用したテスト</span><span class="sxs-lookup"><span data-stu-id="10359-153">Test with Chrome</span></span>

<span data-ttu-id="10359-154">Chrome 78 + には一時的な軽減策があるため、誤解を招く結果になります。</span><span class="sxs-lookup"><span data-stu-id="10359-154">Chrome 78+ gives misleading results because it has a temporary mitigation in place.</span></span> <span data-ttu-id="10359-155">Chrome 78 + 一時的な軽減策では、2分前よりも少ない cookie を使用できます。</span><span class="sxs-lookup"><span data-stu-id="10359-155">The Chrome 78+ temporary mitigation allows cookies less than two minutes old.</span></span> <span data-ttu-id="10359-156">適切なテストフラグが有効になっている Chrome 76 または77では、より正確な結果が得られます。</span><span class="sxs-lookup"><span data-stu-id="10359-156">Chrome 76 or 77 with the appropriate test flags enabled provides more accurate results.</span></span> <span data-ttu-id="10359-157">新しい SameSite の動作をテストするには、`chrome://flags/#same-site-by-default-cookies` を**有効**に切り替えます。</span><span class="sxs-lookup"><span data-stu-id="10359-157">To test the new SameSite behavior toggle `chrome://flags/#same-site-by-default-cookies` to **Enabled**.</span></span> <span data-ttu-id="10359-158">新しい `None` 設定で失敗するように、Chrome の旧バージョン (75 以降) が報告されます。</span><span class="sxs-lookup"><span data-stu-id="10359-158">Older versions of Chrome (75 and below) are reported to fail with the new `None` setting.</span></span> <span data-ttu-id="10359-159">このドキュメントの「[古いブラウザーのサポート](#sob)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="10359-159">See [Supporting older browsers](#sob) in this document.</span></span>

<span data-ttu-id="10359-160">Google では、以前のバージョンの chrome は使用できません。</span><span class="sxs-lookup"><span data-stu-id="10359-160">Google does not make older chrome versions available.</span></span> <span data-ttu-id="10359-161">「 [Chromium のダウンロード](https://www.chromium.org/getting-involved/download-chromium)」の手順に従って、Chrome の旧バージョンをテストします。</span><span class="sxs-lookup"><span data-stu-id="10359-161">Follow the instructions at [Download Chromium](https://www.chromium.org/getting-involved/download-chromium) to test older versions of Chrome.</span></span> <span data-ttu-id="10359-162">以前のバージョンの chrome を検索することによって提供されるリンクから Chrome**をダウンロードしないでください**。</span><span class="sxs-lookup"><span data-stu-id="10359-162">Do **not** download Chrome from links provided by searching for older versions of chrome.</span></span>

* [<span data-ttu-id="10359-163">Chromium 76 Win64</span><span class="sxs-lookup"><span data-stu-id="10359-163">Chromium 76 Win64</span></span>](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/664998/)
* [<span data-ttu-id="10359-164">Chromium 74 Win64</span><span class="sxs-lookup"><span data-stu-id="10359-164">Chromium 74 Win64</span></span>](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/638880/)

### <a name="test-with-safari"></a><span data-ttu-id="10359-165">Safari を使用したテスト</span><span class="sxs-lookup"><span data-stu-id="10359-165">Test with Safari</span></span>

<span data-ttu-id="10359-166">Safari 12 では以前のドラフトが厳密に実装されており、新しい `None` 値が cookie に含まれていると失敗します。</span><span class="sxs-lookup"><span data-stu-id="10359-166">Safari 12 strictly implemented the prior draft and fails when the new `None` value is in a cookie.</span></span> <span data-ttu-id="10359-167">このドキュメントでは、[古いブラウザーをサポート](#sob)するブラウザーの検出コードを使用して `None` を回避します。</span><span class="sxs-lookup"><span data-stu-id="10359-167">`None` is avoided via the browser detection code [Supporting older browsers](#sob) in this document.</span></span> <span data-ttu-id="10359-168">MSAL、ADAL、使用している任意のライブラリを使用して、Safari 12、Safari 13、WebKit ベースの OS スタイルのログインをテストします。</span><span class="sxs-lookup"><span data-stu-id="10359-168">Test Safari 12, Safari 13, and WebKit based OS style logins using MSAL, ADAL or whatever library you are using.</span></span> <span data-ttu-id="10359-169">この問題は、基になる OS バージョンによって異なります。</span><span class="sxs-lookup"><span data-stu-id="10359-169">The problem is dependent on the underlying OS version.</span></span> <span data-ttu-id="10359-170">OSX Mojave (10.14) と iOS 12 には、新しい SameSite の動作に互換性の問題があることがわかっています。</span><span class="sxs-lookup"><span data-stu-id="10359-170">OSX Mojave (10.14) and iOS 12 are known to have compatibility problems with the new SameSite behavior.</span></span> <span data-ttu-id="10359-171">OS を OSX Catalina.properties (10.15) または iOS 13 にアップグレードすると、問題が解決されます。</span><span class="sxs-lookup"><span data-stu-id="10359-171">Upgrading the OS to OSX Catalina (10.15) or iOS 13 fixes the problem.</span></span> <span data-ttu-id="10359-172">Safari には、現在、新しい仕様動作をテストするオプトインフラグがありません。</span><span class="sxs-lookup"><span data-stu-id="10359-172">Safari does not currently have an opt-in flag for testing the new spec behavior.</span></span>

### <a name="test-with-firefox"></a><span data-ttu-id="10359-173">Firefox でのテスト</span><span class="sxs-lookup"><span data-stu-id="10359-173">Test with Firefox</span></span>

<span data-ttu-id="10359-174">新しい標準の Firefox サポートは、バージョン68以降で、[`about:config`] ページで機能フラグ `network.cookie.sameSite.laxByDefault`をオンにしてテストできます。</span><span class="sxs-lookup"><span data-stu-id="10359-174">Firefox support for the new standard can be tested on version 68+ by opting in on the `about:config` page with the feature flag `network.cookie.sameSite.laxByDefault`.</span></span> <span data-ttu-id="10359-175">以前のバージョンの Firefox との互換性に関する問題は報告されていません。</span><span class="sxs-lookup"><span data-stu-id="10359-175">There haven't been reports of compatibility issues with older versions of Firefox.</span></span>

### <a name="test-with-edge-browser"></a><span data-ttu-id="10359-176">Edge ブラウザーを使用したテスト</span><span class="sxs-lookup"><span data-stu-id="10359-176">Test with Edge browser</span></span>

<span data-ttu-id="10359-177">Edge では、古い SameSite 標準がサポートされています。</span><span class="sxs-lookup"><span data-stu-id="10359-177">Edge supports the old SameSite standard.</span></span> <span data-ttu-id="10359-178">Edge バージョン44には、新しい標準との互換性に関する既知の問題はありません。</span><span class="sxs-lookup"><span data-stu-id="10359-178">Edge version 44 doesn't have any known compatibility problems with the new standard.</span></span>

### <a name="test-with-edge-chromium"></a><span data-ttu-id="10359-179">Edge でテストする (Chromium)</span><span class="sxs-lookup"><span data-stu-id="10359-179">Test with Edge (Chromium)</span></span>

<span data-ttu-id="10359-180">SameSite フラグは `edge://flags/#same-site-by-default-cookies` ページで設定されます。</span><span class="sxs-lookup"><span data-stu-id="10359-180">SameSite flags are set on the `edge://flags/#same-site-by-default-cookies` page.</span></span> <span data-ttu-id="10359-181">Edge Chromium で互換性の問題は検出されませんでした。</span><span class="sxs-lookup"><span data-stu-id="10359-181">No compatibility issues were discovered with Edge Chromium.</span></span>

### <a name="test-with-electron"></a><span data-ttu-id="10359-182">電子を使用したテスト</span><span class="sxs-lookup"><span data-stu-id="10359-182">Test with Electron</span></span>

<span data-ttu-id="10359-183">電子バージョンには、古いバージョンの Chromium が含まれています。</span><span class="sxs-lookup"><span data-stu-id="10359-183">Versions of Electron include older versions of Chromium.</span></span> <span data-ttu-id="10359-184">たとえば、チームによって使用されている電子 66 Chromium のバージョンは、以前の動作を示しています。</span><span class="sxs-lookup"><span data-stu-id="10359-184">For example, the version of Electron used by Teams is Chromium 66, which exhibits the older behavior.</span></span> <span data-ttu-id="10359-185">製品で使用されている電子版を使用して、独自の互換性テストを実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="10359-185">You must perform your own compatibility testing with the version of Electron your product uses.</span></span> <span data-ttu-id="10359-186">次のセクションの「[古いブラウザーのサポート](#sob)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="10359-186">See [Supporting older browsers](#sob) in the following section.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="10359-187">その他の技術情報</span><span class="sxs-lookup"><span data-stu-id="10359-187">Additional resources</span></span>

* [<span data-ttu-id="10359-188">Chromium ブログ: 開発者: 新しい SameSite の準備 = None;セキュリティで保護された Cookie の設定</span><span class="sxs-lookup"><span data-stu-id="10359-188">Chromium Blog:Developers: Get Ready for New SameSite=None; Secure Cookie Settings</span></span>](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)
* [<span data-ttu-id="10359-189">SameSite cookie の説明</span><span class="sxs-lookup"><span data-stu-id="10359-189">SameSite cookies explained</span></span>](https://web.dev/samesite-cookies-explained/)
