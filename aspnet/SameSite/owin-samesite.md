---
title: SameSite cookie と Open Web Interface for .NET (OWIN) を使用する
author: rick-anderson
description: SameSite cookie と Open Web Interface for .NET (OWIN) を使用する
ms.author: riande
ms.date: 12/6/2019
uid: owin-samesite
ms.openlocfilehash: a3353fd0f0332899aaba26b83aea0ff7c3a6d19b
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2020
ms.locfileid: "77455738"
---
# <a name="samesite-cookies-and-the-open-web-interface-for-net-owin"></a><span data-ttu-id="8986c-103">SameSite cookie と Open Web Interface for .NET (OWIN)</span><span class="sxs-lookup"><span data-stu-id="8986c-103">SameSite cookies and the Open Web Interface for .NET (OWIN)</span></span>

<span data-ttu-id="8986c-104">作成者: [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="8986c-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="8986c-105">`SameSite` は、クロスサイトリクエスト偽造 (CSRF) 攻撃に対して何らかの保護を提供するように設計された[IETF](https://ietf.org/about/)ドラフトです。</span><span class="sxs-lookup"><span data-stu-id="8986c-105">`SameSite` is an [IETF](https://ietf.org/about/) draft designed to provide some protection against cross-site request forgery (CSRF) attacks.</span></span> <span data-ttu-id="8986c-106">[SameSite 2019 のドラフト](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00):</span><span class="sxs-lookup"><span data-stu-id="8986c-106">The [SameSite 2019 draft](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00):</span></span>

* <span data-ttu-id="8986c-107">クッキーを既定で `SameSite=Lax` として扱います。</span><span class="sxs-lookup"><span data-stu-id="8986c-107">Treats cookies as `SameSite=Lax` by default.</span></span>
* <span data-ttu-id="8986c-108">クロスサイト配信を有効にするために `SameSite=None` を明示的にアサートする cookie の状態を `Secure`としてマークする必要があります。</span><span class="sxs-lookup"><span data-stu-id="8986c-108">States cookies that explicitly assert `SameSite=None` in order to enable cross-site delivery should be marked as `Secure`.</span></span>

<span data-ttu-id="8986c-109">`Lax` は、ほとんどのアプリ cookie で機能します。</span><span class="sxs-lookup"><span data-stu-id="8986c-109">`Lax` works for most app cookies.</span></span> <span data-ttu-id="8986c-110">[OpenID connect](https://openid.net/connect/) (oidc) や[ws-federation](https://auth0.com/docs/protocols/ws-fed)のような認証形式では、既定で POST ベースのリダイレクトが設定されます。</span><span class="sxs-lookup"><span data-stu-id="8986c-110">Some forms of authentication like [OpenID Connect](https://openid.net/connect/) (OIDC) and [WS-Federation](https://auth0.com/docs/protocols/ws-fed) default to POST based redirects.</span></span> <span data-ttu-id="8986c-111">POST ベースのリダイレクトによって `SameSite` ブラウザーの保護がトリガーされるため、これらのコンポーネントの `SameSite` は無効になります。</span><span class="sxs-lookup"><span data-stu-id="8986c-111">The POST based redirects trigger the `SameSite` browser protections, so `SameSite` is disabled for these components.</span></span> <span data-ttu-id="8986c-112">ほとんどの[OAuth](https://oauth.net/)ログインは、要求フローの違いによって影響を受けません。</span><span class="sxs-lookup"><span data-stu-id="8986c-112">Most [OAuth](https://oauth.net/) logins aren't affected due to differences in how the request flows.</span></span> <span data-ttu-id="8986c-113">その他のすべてのコンポーネントは、既定で `SameSite` を設定**せず**、クライアントの既定の動作 (old または new) を使用します。</span><span class="sxs-lookup"><span data-stu-id="8986c-113">All other components do **not** set `SameSite` by default and use the clients default behavior (old or new).</span></span>

<span data-ttu-id="8986c-114">`None` パラメーターを指定すると、以前の[2016 ドラフト標準](https://tools.ietf.org/html/draft-west-first-party-cookies-07)(iOS 12 など) を実装したクライアントとの互換性の問題が発生します。</span><span class="sxs-lookup"><span data-stu-id="8986c-114">The `None` parameter causes compatibility problems with clients that implemented the prior [2016 draft standard](https://tools.ietf.org/html/draft-west-first-party-cookies-07) (for example, iOS 12).</span></span> <span data-ttu-id="8986c-115">このドキュメントの「[古いブラウザーのサポート](#sob)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="8986c-115">See [Supporting older browsers](#sob) in this document.</span></span>

<span data-ttu-id="8986c-116">Cookie を生成する各 OWIN コンポーネントは、`SameSite` が適切かどうかを判断する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8986c-116">Each OWIN component that emits cookies needs to decide if `SameSite` is appropriate.</span></span>

<span data-ttu-id="8986c-117">この記事の ASP.NET 4.x バージョンについては、「<xref:samesite/system-web-samesite>」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="8986c-117">For the ASP.NET 4.x version of this article, see <xref:samesite/system-web-samesite>.</span></span>

## <a name="api-usage-with-samesite"></a><span data-ttu-id="8986c-118">SameSite を使用した API の使用</span><span class="sxs-lookup"><span data-stu-id="8986c-118">API usage with SameSite</span></span>

<span data-ttu-id="8986c-119">`Microsoft.Owin` には、独自の `SameSite` 実装があります。</span><span class="sxs-lookup"><span data-stu-id="8986c-119">`Microsoft.Owin` has its own `SameSite` implementation:</span></span>

* <span data-ttu-id="8986c-120">これは `System.Web`のものに直接依存していません。</span><span class="sxs-lookup"><span data-stu-id="8986c-120">That is not directly dependent on the one in `System.Web`.</span></span>
* <span data-ttu-id="8986c-121">`SameSite` は、`Microsoft.Owin` パッケージ、.net 4.5 以降のすべてのバージョンの不要で機能します。</span><span class="sxs-lookup"><span data-stu-id="8986c-121">`SameSite` works on all versions targetable by the `Microsoft.Owin` packages, .NET 4.5 and later.</span></span>
* <span data-ttu-id="8986c-122">[SystemWebCookieManager](https://github.com/aspnet/AspNetKatana/blob/dev/src/Microsoft.Owin.Host.SystemWeb/SystemWebCookieManager.cs)コンポーネントのみが `System.Web` `HttpCookie` クラスと直接やり取りします。</span><span class="sxs-lookup"><span data-stu-id="8986c-122">Only the [SystemWebCookieManager](https://github.com/aspnet/AspNetKatana/blob/dev/src/Microsoft.Owin.Host.SystemWeb/SystemWebCookieManager.cs) component directly interacts with the `System.Web` `HttpCookie` class.</span></span>

<span data-ttu-id="8986c-123">`SystemWebCookieManager` は、`SameSite` サポートを有効にするための .NET 4.7.2 `System.Web` Api と、動作を変更するための修正プログラムに依存しています。</span><span class="sxs-lookup"><span data-stu-id="8986c-123">`SystemWebCookieManager` depends on the .NET 4.7.2 `System.Web` APIs to enable `SameSite` support, and the patches to change the behavior.</span></span>

<span data-ttu-id="8986c-124">`SystemWebCookieManager` を使用する理由については、 [「OWIN And system.web response cookie の統合に関する問題](https://github.com/aspnet/AspNetKatana/wiki/System.Web-response-cookie-integration-issues)」を説明しています。</span><span class="sxs-lookup"><span data-stu-id="8986c-124">The reasons to use `SystemWebCookieManager` are outlined in [OWIN and System.Web response cookie integration issues](https://github.com/aspnet/AspNetKatana/wiki/System.Web-response-cookie-integration-issues).</span></span> <span data-ttu-id="8986c-125">`System.Web`で実行する場合は `SystemWebCookieManager` をお勧めします。</span><span class="sxs-lookup"><span data-stu-id="8986c-125">`SystemWebCookieManager` is recommended when running on `System.Web`.</span></span>

<span data-ttu-id="8986c-126">次のコードでは、`SameSite` を `Lax`に設定しています。</span><span class="sxs-lookup"><span data-stu-id="8986c-126">The following code sets `SameSite` to `Lax`:</span></span>

```csharp
owinContext.Response.Cookies.Append("My Key", "My Value", new CookieOptions()
{
    SameSite = SameSiteMode.Lax
});
```

<span data-ttu-id="8986c-127">次の Api は `SameSite`を使用します。</span><span class="sxs-lookup"><span data-stu-id="8986c-127">The following APIs use `SameSite`:</span></span>

* [<span data-ttu-id="8986c-128">Owin. SameSiteMode</span><span class="sxs-lookup"><span data-stu-id="8986c-128">Microsoft.Owin.SameSiteMode</span></span>](https://github.com/aspnet/AspNetKatana/blob/dev/src/Microsoft.Owin/SameSiteMode.cs)
* [<span data-ttu-id="8986c-129">CookieOptions. SameSite</span><span class="sxs-lookup"><span data-stu-id="8986c-129">CookieOptions.SameSite</span></span>](xref:Microsoft.AspNetCore.Http.CookieOptions.SameSite)
* <span data-ttu-id="8986c-130">[CookieAuthenticationOptions クラス](/previous-versions/aspnet/dn385599(v%3Dvs.113))</span><span class="sxs-lookup"><span data-stu-id="8986c-130">[CookieAuthenticationOptions Class](/previous-versions/aspnet/dn385599(v%3Dvs.113))</span></span> <!-- CookieAuthenticationOptions.CookieSameSite not published -->
* [<span data-ttu-id="8986c-131">CookieAuthenticationOptions. CookieSameSite</span><span class="sxs-lookup"><span data-stu-id="8986c-131">CookieAuthenticationOptions.CookieSameSite</span></span>](https://github.com/aspnet/AspNetKatana/blob/dev/src/Microsoft.Owin.Security.Cookies/CookieAuthenticationOptions.cs#L68-#L72)
* <span data-ttu-id="8986c-132">[ICookieManager](/previous-versions/aspnet/dn800238(v%3Dvs.113))</span><span class="sxs-lookup"><span data-stu-id="8986c-132">[ICookieManager](/previous-versions/aspnet/dn800238(v%3Dvs.113))</span></span>
* [<span data-ttu-id="8986c-133">SystemWebCookieManager</span><span class="sxs-lookup"><span data-stu-id="8986c-133">SystemWebCookieManager</span></span>](https://github.com/aspnet/AspNetKatana/blob/dev/src/Microsoft.Owin.Host.SystemWeb/SystemWebCookieManager.cs)
* [<span data-ttu-id="8986c-134">SystemWebChunkingCookieManager</span><span class="sxs-lookup"><span data-stu-id="8986c-134">SystemWebChunkingCookieManager</span></span>](https://github.com/aspnet/AspNetKatana/blob/dev/src/Microsoft.Owin.Host.SystemWeb/SystemWebChunkingCookieManager.cs)
* [<span data-ttu-id="8986c-135">CookieAuthenticationOptions. CookieManager</span><span class="sxs-lookup"><span data-stu-id="8986c-135">CookieAuthenticationOptions.CookieManager</span></span>](https://github.com/aspnet/AspNetKatana/blob/dev/src/Microsoft.Owin.Security.Cookies/CookieAuthenticationOptions.cs#L143-#AL148)
* [<span data-ttu-id="8986c-136">OpenIdConnectAuthenticationOptions. CookieManager</span><span class="sxs-lookup"><span data-stu-id="8986c-136">OpenIdConnectAuthenticationOptions.CookieManager</span></span>](https://github.com/aspnet/AspNetKatana/blob/dev/src/Microsoft.Owin.Security.OpenIdConnect/OpenIdConnectAuthenticationOptions.cs#L315-#L318)

## <a name="history-and-changes"></a><span data-ttu-id="8986c-137">履歴と変更</span><span class="sxs-lookup"><span data-stu-id="8986c-137">History and changes</span></span>

<span data-ttu-id="8986c-138">[Owin](https://www.nuget.org/packages/Microsoft.Owin/)では、 [2016 ドラフト標準`SameSite`](https://tools.ietf.org/html/draft-west-first-party-cookies-07#section-4.1)がサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="8986c-138">[Microsoft.Owin](https://www.nuget.org/packages/Microsoft.Owin/) never supported the [`SameSite` 2016 draft standard](https://tools.ietf.org/html/draft-west-first-party-cookies-07#section-4.1).</span></span>

<span data-ttu-id="8986c-139">[SameSite 2019 draft](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00)のサポートは、`Microsoft.Owin` 4.1.0 以降でのみ使用できます。</span><span class="sxs-lookup"><span data-stu-id="8986c-139">Support for the [SameSite 2019 draft](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00) is only available in `Microsoft.Owin` 4.1.0 and later.</span></span> <span data-ttu-id="8986c-140">以前のバージョンの修正プログラムはありません。</span><span class="sxs-lookup"><span data-stu-id="8986c-140">There are no patches for prior versions.</span></span>

<span data-ttu-id="8986c-141">`SameSite` 仕様の2019ドラフトは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="8986c-141">The 2019 draft of the `SameSite` specification:</span></span>

* <span data-ttu-id="8986c-142">は、2016ドラフトとの下位互換性が**ありません**。</span><span class="sxs-lookup"><span data-stu-id="8986c-142">Is **not** backwards compatible with the 2016 draft.</span></span> <span data-ttu-id="8986c-143">詳細については、このドキュメントの「[古いブラウザーのサポート](#sob)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="8986c-143">For more information, see [Supporting older browsers](#sob) in this document.</span></span>
* <span data-ttu-id="8986c-144">Cookie を既定で `SameSite=Lax` として扱うことを指定します。</span><span class="sxs-lookup"><span data-stu-id="8986c-144">Specifies cookies are treated as `SameSite=Lax` by default.</span></span>
* <span data-ttu-id="8986c-145">クロスサイト配信を有効にするために `SameSite=None` を明示的にアサートする cookie を `Secure`としてマークする必要があることを指定します。</span><span class="sxs-lookup"><span data-stu-id="8986c-145">Specifies cookies that explicitly assert `SameSite=None` in order to enable cross-site delivery should be marked as `Secure`.</span></span> <span data-ttu-id="8986c-146">`None` は、オプトアウトする新しいエントリです。</span><span class="sxs-lookup"><span data-stu-id="8986c-146">`None` is a new entry to opt out.</span></span>
* <span data-ttu-id="8986c-147">[2 月 2020](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)日に既定で[Chrome](https://chromestatus.com/feature/5088147346030592)によって有効になるようにスケジュールされています。</span><span class="sxs-lookup"><span data-stu-id="8986c-147">Is scheduled to be enabled by [Chrome](https://chromestatus.com/feature/5088147346030592) by default in [Feb 2020](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html).</span></span> <span data-ttu-id="8986c-148">ブラウザーは2019でこの標準への移行を開始しました。</span><span class="sxs-lookup"><span data-stu-id="8986c-148">Browsers started moving to this standard in 2019.</span></span>
* <span data-ttu-id="8986c-149">は、サポート技術情報の記事の説明に従って発行された修正プログラムによってサポートされます</span><span class="sxs-lookup"><span data-stu-id="8986c-149">Is supported by patches issued as described in KB articles.</span></span> <span data-ttu-id="8986c-150">詳細については、<xref:samesite/kbs-samesite> を参照してください。</span><span class="sxs-lookup"><span data-stu-id="8986c-150">For more information, see <xref:samesite/kbs-samesite>.</span></span>

<a name="sob"></a>

## <a name="supporting-older-browsers"></a><span data-ttu-id="8986c-151">古いブラウザーのサポート</span><span class="sxs-lookup"><span data-stu-id="8986c-151">Supporting older browsers</span></span>

<span data-ttu-id="8986c-152">2016 `SameSite` 標準では、不明な値を `SameSite=Strict` 値として扱う必要があることが義務付けられています。</span><span class="sxs-lookup"><span data-stu-id="8986c-152">The 2016 `SameSite` standard mandated that unknown values must be treated as `SameSite=Strict` values.</span></span> <span data-ttu-id="8986c-153">2016 `SameSite` 標準をサポートする古いブラウザーからアクセスされるアプリは、値が `None`の `SameSite` プロパティを取得すると壊れます。</span><span class="sxs-lookup"><span data-stu-id="8986c-153">Apps accessed from older browsers which support the 2016 `SameSite` standard may break when they get a `SameSite` property with a value of `None`.</span></span> <span data-ttu-id="8986c-154">Web apps が古いブラウザーをサポートする予定の場合は、ブラウザーの検出を実装する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8986c-154">Web apps must implement browser detection if they intend to support older browsers.</span></span> <span data-ttu-id="8986c-155">ASP.NET は、ユーザーエージェントの値が変動し頻繁に変更されるため、ブラウザーの検出を実装しません。</span><span class="sxs-lookup"><span data-stu-id="8986c-155">ASP.NET doesn't implement browser detection because User-Agents values are highly volatile and change frequently.</span></span> <span data-ttu-id="8986c-156">[ICookieManager](/previous-versions/aspnet/dn800238(v%3Dvs.113))の拡張ポイントを使用すると、ユーザーエージェント固有のロジックをプラグインできます。</span><span class="sxs-lookup"><span data-stu-id="8986c-156">An extension point in [ICookieManager](/previous-versions/aspnet/dn800238(v%3Dvs.113)) allows plugging in User-Agent specific logic.</span></span>
<!-- https://docs.microsoft.com/previous-versions/aspnet/dn800238(v%3Dvs.113) -->

<span data-ttu-id="8986c-157">`Startup.Configuration`で、次のようなコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="8986c-157">In `Startup.Configuration`, add code similar to the following:</span></span>

[!code-csharp[](sample/Startup1.cs?name=snippet)]

<span data-ttu-id="8986c-158">上記のコードでは、.NET 4.7.2 以降 `SameSite` パッチが必要です。</span><span class="sxs-lookup"><span data-stu-id="8986c-158">The preceding code requires the .NET 4.7.2 or later `SameSite` patch.</span></span>

<span data-ttu-id="8986c-159">次のコードは、`SameSiteCookieManager`の実装例を示しています。</span><span class="sxs-lookup"><span data-stu-id="8986c-159">The following code shows an example implementation of `SameSiteCookieManager`:</span></span>

[!code-csharp[](sample/SameSiteCookieManager.cs?name=snippet)]

<span data-ttu-id="8986c-160">前の例では、`CheckSameSite` メソッドで `DisallowsSameSiteNone` が呼び出されています。</span><span class="sxs-lookup"><span data-stu-id="8986c-160">In the preceding sample, `DisallowsSameSiteNone` is called in the `CheckSameSite` method.</span></span> <span data-ttu-id="8986c-161">`DisallowsSameSiteNone` は、ユーザーエージェントが `SameSite` `None`をサポートしていないかどうかを検出するユーザーメソッドです。</span><span class="sxs-lookup"><span data-stu-id="8986c-161">`DisallowsSameSiteNone` is a user method that detects if the user agent doesn't support `SameSite` `None`:</span></span>

[!code-csharp[](sample/SameSiteCookieManager.cs?name=snippet3&highlight=4)]

<span data-ttu-id="8986c-162">次のコードは、`DisallowsSameSiteNone` メソッドの例を示しています。</span><span class="sxs-lookup"><span data-stu-id="8986c-162">The following code shows a sample `DisallowsSameSiteNone` method:</span></span>

> [!WARNING]
> <span data-ttu-id="8986c-163">次のコードは、デモンストレーションのみを対象としています。</span><span class="sxs-lookup"><span data-stu-id="8986c-163">The following code is for demonstration only:</span></span>
> * <span data-ttu-id="8986c-164">完全であるとは限りません。</span><span class="sxs-lookup"><span data-stu-id="8986c-164">It should not be considered complete.</span></span>
> * <span data-ttu-id="8986c-165">管理されていないか、サポートされていません。</span><span class="sxs-lookup"><span data-stu-id="8986c-165">It is not maintained or supported.</span></span>

[!code-csharp[](sample/SameSiteCookieManager.cs?name=snippet2)]

## <a name="test-apps-for-samesite-problems"></a><span data-ttu-id="8986c-166">SameSite 問題のアプリをテストする</span><span class="sxs-lookup"><span data-stu-id="8986c-166">Test apps for SameSite problems</span></span>

<span data-ttu-id="8986c-167">サードパーティのログインによってなどのリモートサイトと対話するアプリでは、次の操作を行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="8986c-167">Apps that interact with remote sites such as through third-party login need to:</span></span>

* <span data-ttu-id="8986c-168">複数のブラウザーで相互作用をテストします。</span><span class="sxs-lookup"><span data-stu-id="8986c-168">Test the interaction on multiple browsers.</span></span>
* <span data-ttu-id="8986c-169">このドキュメントで説明され[ているブラウザーの検出と軽減策](#sob)を適用します。</span><span class="sxs-lookup"><span data-stu-id="8986c-169">Apply the [browser detection and mitigation](#sob) discussed in this document.</span></span>

<span data-ttu-id="8986c-170">新しい `SameSite` 動作にオプトインできるクライアントバージョンを使用して、web アプリをテストします。</span><span class="sxs-lookup"><span data-stu-id="8986c-170">Test web apps using a client version that can opt-in to the new `SameSite` behavior.</span></span> <span data-ttu-id="8986c-171">Chrome、Firefox、Chromium Edge には、テストに使用できる新しいオプトイン機能フラグがあります。</span><span class="sxs-lookup"><span data-stu-id="8986c-171">Chrome, Firefox, and Chromium Edge all have new opt-in feature flags that can be used for testing.</span></span> <span data-ttu-id="8986c-172">アプリが `SameSite` パッチを適用したら、古いクライアントバージョン (特に Safari) を使用してテストします。</span><span class="sxs-lookup"><span data-stu-id="8986c-172">After your app applies the `SameSite` patches, test it with older client versions, especially Safari.</span></span> <span data-ttu-id="8986c-173">詳細については、このドキュメントの「[古いブラウザーのサポート](#sob)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="8986c-173">For more information, see [Supporting older browsers](#sob) in this document.</span></span>

### <a name="test-with-chrome"></a><span data-ttu-id="8986c-174">Chrome を使用したテスト</span><span class="sxs-lookup"><span data-stu-id="8986c-174">Test with Chrome</span></span>

<span data-ttu-id="8986c-175">Chrome 78 + には一時的な軽減策があるため、誤解を招く結果になります。</span><span class="sxs-lookup"><span data-stu-id="8986c-175">Chrome 78+ gives misleading results because it has a temporary mitigation in place.</span></span> <span data-ttu-id="8986c-176">Chrome 78 + 一時的な軽減策では、2分前よりも少ない cookie を使用できます。</span><span class="sxs-lookup"><span data-stu-id="8986c-176">The Chrome 78+ temporary mitigation allows cookies less than two minutes old.</span></span> <span data-ttu-id="8986c-177">適切なテストフラグが有効になっている Chrome 76 または77では、より正確な結果が得られます。</span><span class="sxs-lookup"><span data-stu-id="8986c-177">Chrome 76 or 77 with the appropriate test flags enabled provides more accurate results.</span></span> <span data-ttu-id="8986c-178">新しい `SameSite` 動作をテストするには、`chrome://flags/#same-site-by-default-cookies` を**有効**に切り替えます。</span><span class="sxs-lookup"><span data-stu-id="8986c-178">To test the new `SameSite` behavior toggle `chrome://flags/#same-site-by-default-cookies` to **Enabled**.</span></span> <span data-ttu-id="8986c-179">新しい `None` 設定で失敗するように、Chrome の旧バージョン (75 以降) が報告されます。</span><span class="sxs-lookup"><span data-stu-id="8986c-179">Older versions of Chrome (75 and below) are reported to fail with the new `None` setting.</span></span> <span data-ttu-id="8986c-180">このドキュメントの「[古いブラウザーのサポート](#sob)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="8986c-180">See [Supporting older browsers](#sob) in this document.</span></span>

<span data-ttu-id="8986c-181">Google では、以前のバージョンの chrome は使用できません。</span><span class="sxs-lookup"><span data-stu-id="8986c-181">Google does not make older chrome versions available.</span></span> <span data-ttu-id="8986c-182">「 [Chromium のダウンロード](https://www.chromium.org/getting-involved/download-chromium)」の手順に従って、Chrome の旧バージョンをテストします。</span><span class="sxs-lookup"><span data-stu-id="8986c-182">Follow the instructions at [Download Chromium](https://www.chromium.org/getting-involved/download-chromium) to test older versions of Chrome.</span></span> <span data-ttu-id="8986c-183">以前のバージョンの chrome を検索することによって提供されるリンクから Chrome**をダウンロードしないでください**。</span><span class="sxs-lookup"><span data-stu-id="8986c-183">Do **not** download Chrome from links provided by searching for older versions of chrome.</span></span>

* [<span data-ttu-id="8986c-184">Chromium 76 Win64</span><span class="sxs-lookup"><span data-stu-id="8986c-184">Chromium 76 Win64</span></span>](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/664998/)
* [<span data-ttu-id="8986c-185">Chromium 74 Win64</span><span class="sxs-lookup"><span data-stu-id="8986c-185">Chromium 74 Win64</span></span>](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/638880/)

### <a name="test-with-safari"></a><span data-ttu-id="8986c-186">Safari を使用したテスト</span><span class="sxs-lookup"><span data-stu-id="8986c-186">Test with Safari</span></span>

<span data-ttu-id="8986c-187">Safari 12 では以前のドラフトが厳密に実装されており、新しい `None` 値が cookie に含まれていると失敗します。</span><span class="sxs-lookup"><span data-stu-id="8986c-187">Safari 12 strictly implemented the prior draft and fails when the new `None` value is in a cookie.</span></span> <span data-ttu-id="8986c-188">このドキュメントでは、[古いブラウザーをサポート](#sob)するブラウザーの検出コードを使用して `None` を回避します。</span><span class="sxs-lookup"><span data-stu-id="8986c-188">`None` is avoided via the browser detection code [Supporting older browsers](#sob) in this document.</span></span> <span data-ttu-id="8986c-189">MSAL、ADAL、使用している任意のライブラリを使用して、Safari 12、Safari 13、WebKit ベースの OS スタイルのログインをテストします。</span><span class="sxs-lookup"><span data-stu-id="8986c-189">Test Safari 12, Safari 13, and WebKit based OS style logins using MSAL, ADAL or whatever library you are using.</span></span> <span data-ttu-id="8986c-190">この問題は、基盤の OS バージョンによって変わります。</span><span class="sxs-lookup"><span data-stu-id="8986c-190">The problem is dependent on the underlying OS version.</span></span> <span data-ttu-id="8986c-191">OSX Mojave (10.14) と iOS 12 には、新しい `SameSite` 動作との互換性の問題があることがわかっています。</span><span class="sxs-lookup"><span data-stu-id="8986c-191">OSX Mojave (10.14) and iOS 12 are known to have compatibility problems with the new `SameSite` behavior.</span></span> <span data-ttu-id="8986c-192">OS を OSX Catalina.properties (10.15) または iOS 13 にアップグレードすると、問題が解決されます。</span><span class="sxs-lookup"><span data-stu-id="8986c-192">Upgrading the OS to OSX Catalina (10.15) or iOS 13 fixes the problem.</span></span> <span data-ttu-id="8986c-193">Safari には、現在、新しい仕様動作をテストするオプトインフラグがありません。</span><span class="sxs-lookup"><span data-stu-id="8986c-193">Safari does not currently have an opt-in flag for testing the new spec behavior.</span></span>

### <a name="test-with-firefox"></a><span data-ttu-id="8986c-194">Firefox でのテスト</span><span class="sxs-lookup"><span data-stu-id="8986c-194">Test with Firefox</span></span>

<span data-ttu-id="8986c-195">新しい標準の Firefox サポートは、バージョン68以降で、[`about:config`] ページで機能フラグ `network.cookie.sameSite.laxByDefault`をオンにしてテストできます。</span><span class="sxs-lookup"><span data-stu-id="8986c-195">Firefox support for the new standard can be tested on version 68+ by opting in on the `about:config` page with the feature flag `network.cookie.sameSite.laxByDefault`.</span></span> <span data-ttu-id="8986c-196">以前のバージョンの Firefox との互換性に関する問題は報告されていません。</span><span class="sxs-lookup"><span data-stu-id="8986c-196">There haven't been reports of compatibility issues with older versions of Firefox.</span></span>

### <a name="test-with-edge-browser"></a><span data-ttu-id="8986c-197">Edge ブラウザーを使用したテスト</span><span class="sxs-lookup"><span data-stu-id="8986c-197">Test with Edge browser</span></span>

<span data-ttu-id="8986c-198">Edge では、古い `SameSite` 標準がサポートされています。</span><span class="sxs-lookup"><span data-stu-id="8986c-198">Edge supports the old `SameSite` standard.</span></span> <span data-ttu-id="8986c-199">Edge バージョン44には、新しい標準との互換性に関する既知の問題はありません。</span><span class="sxs-lookup"><span data-stu-id="8986c-199">Edge version 44 doesn't have any known compatibility problems with the new standard.</span></span>

### <a name="test-with-edge-chromium"></a><span data-ttu-id="8986c-200">Edge でテストする (Chromium)</span><span class="sxs-lookup"><span data-stu-id="8986c-200">Test with Edge (Chromium)</span></span>

<span data-ttu-id="8986c-201">`SameSite` フラグは、`edge://flags/#same-site-by-default-cookies` ページで設定します。</span><span class="sxs-lookup"><span data-stu-id="8986c-201">`SameSite` flags are set on the `edge://flags/#same-site-by-default-cookies` page.</span></span> <span data-ttu-id="8986c-202">Edge Chromium で互換性の問題は検出されませんでした。</span><span class="sxs-lookup"><span data-stu-id="8986c-202">No compatibility issues were discovered with Edge Chromium.</span></span>

### <a name="test-with-electron"></a><span data-ttu-id="8986c-203">電子を使用したテスト</span><span class="sxs-lookup"><span data-stu-id="8986c-203">Test with Electron</span></span>

<span data-ttu-id="8986c-204">Electron の複数のバージョンには、Chromium の古いバージョンが含まれています。</span><span class="sxs-lookup"><span data-stu-id="8986c-204">Versions of Electron include older versions of Chromium.</span></span> <span data-ttu-id="8986c-205">たとえば、チームによって使用されている電子 66 Chromium のバージョンは、以前の動作を示しています。</span><span class="sxs-lookup"><span data-stu-id="8986c-205">For example, the version of Electron used by Teams is Chromium 66, which exhibits the older behavior.</span></span> <span data-ttu-id="8986c-206">製品で使用されている電子版を使用して、独自の互換性テストを実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8986c-206">You must perform your own compatibility testing with the version of Electron your product uses.</span></span> <span data-ttu-id="8986c-207">次のセクションの「[古いブラウザーのサポート](#sob)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="8986c-207">See [Supporting older browsers](#sob) in the following section.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8986c-208">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="8986c-208">Additional resources</span></span>

* [<span data-ttu-id="8986c-209">Chromium ブログ: 開発者: 新しい SameSite の準備 = None;セキュリティで保護された Cookie の設定</span><span class="sxs-lookup"><span data-stu-id="8986c-209">Chromium Blog:Developers: Get Ready for New SameSite=None; Secure Cookie Settings</span></span>](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)
* [<span data-ttu-id="8986c-210">SameSite cookie の説明</span><span class="sxs-lookup"><span data-stu-id="8986c-210">SameSite cookies explained</span></span>](https://web.dev/samesite-cookies-explained/)
* [<span data-ttu-id="8986c-211">OWIN と System.web response cookie の統合に関する問題</span><span class="sxs-lookup"><span data-stu-id="8986c-211">OWIN and System.Web response cookie integration issues</span></span>](https://github.com/aspnet/AspNetKatana/wiki/System.Web-response-cookie-integration-issues)
