---
title: ASP.NET で SameSite cookie を使用する
author: rick-anderson
description: を使用して ASP.NET でクッキーを SameSite する方法について説明します。
ms.author: riande
ms.date: 2/15/2019
uid: samesite/system-web-samesite
ms.openlocfilehash: 7987a5d6c9b3a82679d42a2d381d471d56f495c2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78439936"
---
# <a name="work-with-samesite-cookies-in-aspnet"></a><span data-ttu-id="1df9e-103">ASP.NET で SameSite cookie を使用する</span><span class="sxs-lookup"><span data-stu-id="1df9e-103">Work with SameSite cookies in ASP.NET</span></span>

<span data-ttu-id="1df9e-104">作成者: [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="1df9e-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="1df9e-105">SameSite は、クロスサイトリクエスト偽造 (CSRF) 攻撃に対して何らかの保護を提供するように設計された[IETF](https://ietf.org/about/)ドラフト標準です。</span><span class="sxs-lookup"><span data-stu-id="1df9e-105">SameSite is an [IETF](https://ietf.org/about/) draft standard designed to provide some protection against cross-site request forgery (CSRF) attacks.</span></span> <span data-ttu-id="1df9e-106">最初は[2016](https://tools.ietf.org/html/draft-west-first-party-cookies-07)でドラフトされていましたが、draft standard は[2019](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00)で更新されました。</span><span class="sxs-lookup"><span data-stu-id="1df9e-106">Originally drafted in [2016](https://tools.ietf.org/html/draft-west-first-party-cookies-07), the draft standard was updated in [2019](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00).</span></span> <span data-ttu-id="1df9e-107">更新された標準は以前の標準との下位互換性はありませんが、次のように最も顕著な違いがあります。</span><span class="sxs-lookup"><span data-stu-id="1df9e-107">The updated standard is not backward compatible with the previous standard, with the following being the most noticeable differences:</span></span>

* <span data-ttu-id="1df9e-108">SameSite ヘッダーのない cookie は、既定では `SameSite=Lax` として扱われます。</span><span class="sxs-lookup"><span data-stu-id="1df9e-108">Cookies without SameSite header are treated as `SameSite=Lax` by default.</span></span>
* <span data-ttu-id="1df9e-109">クロスサイトクッキーの使用を許可するには、`SameSite=None` を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="1df9e-109">`SameSite=None` must be used to allow cross-site cookie use.</span></span>
* <span data-ttu-id="1df9e-110">`SameSite=None` をアサートする cookie も `Secure`としてマークする必要があります。</span><span class="sxs-lookup"><span data-stu-id="1df9e-110">Cookies that assert `SameSite=None` must also be marked as `Secure`.</span></span>
* <span data-ttu-id="1df9e-111">[`<iframe>`](https://developer.mozilla.org/docs/Web/HTML/Element/iframe)を使用するアプリケーションでは、`<iframe>` はクロスサイトのシナリオとして扱われるため、`sameSite=Lax` または `sameSite=Strict` cookie に関する問題が発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="1df9e-111">Applications that use [`<iframe>`](https://developer.mozilla.org/docs/Web/HTML/Element/iframe) may experience issues with `sameSite=Lax` or `sameSite=Strict` cookies because `<iframe>` is treated as cross-site scenarios.</span></span>
* <span data-ttu-id="1df9e-112">値 `SameSite=None` は[2016 標準](https://tools.ietf.org/html/draft-west-first-party-cookies-07)では許可されていないため、一部の実装では、このような cookie を `SameSite=Strict`として扱います。</span><span class="sxs-lookup"><span data-stu-id="1df9e-112">The value `SameSite=None` is not allowed by the [2016 standard](https://tools.ietf.org/html/draft-west-first-party-cookies-07) and causes some implementations to treat such cookies as `SameSite=Strict`.</span></span> <span data-ttu-id="1df9e-113">このドキュメントの「[古いブラウザーのサポート](#sob)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="1df9e-113">See [Supporting older browsers](#sob) in this document.</span></span>

<span data-ttu-id="1df9e-114">`SameSite=Lax` 設定は、ほとんどのアプリケーション cookie に対して機能します。</span><span class="sxs-lookup"><span data-stu-id="1df9e-114">The `SameSite=Lax` setting works for most application cookies.</span></span> <span data-ttu-id="1df9e-115">[OpenID connect](https://openid.net/connect/) (oidc) や[ws-federation](https://auth0.com/docs/protocols/ws-fed)のような認証形式では、既定で POST ベースのリダイレクトが設定されます。</span><span class="sxs-lookup"><span data-stu-id="1df9e-115">Some forms of authentication like [OpenID Connect](https://openid.net/connect/) (OIDC) and [WS-Federation](https://auth0.com/docs/protocols/ws-fed) default to POST based redirects.</span></span> <span data-ttu-id="1df9e-116">POST ベースのリダイレクトによって SameSite ブラウザーの保護がトリガーされるため、これらのコンポーネントの SameSite は無効になります。</span><span class="sxs-lookup"><span data-stu-id="1df9e-116">The POST based redirects trigger the SameSite browser protections, so SameSite is disabled for these components.</span></span> <span data-ttu-id="1df9e-117">ほとんどの[OAuth](https://oauth.net/)ログインは、要求フローの違いによって影響を受けません。</span><span class="sxs-lookup"><span data-stu-id="1df9e-117">Most [OAuth](https://oauth.net/) logins are not affected due to differences in how the request flows.</span></span>

<span data-ttu-id="1df9e-118">Cookie を生成する各 ASP.NET コンポーネントは、SameSite が適切かどうかを判断する必要があります。</span><span class="sxs-lookup"><span data-stu-id="1df9e-118">Each ASP.NET component that emits cookies needs to decide if SameSite is appropriate.</span></span>

<span data-ttu-id="1df9e-119">2019 .Net SameSite の更新プログラムをインストールした後のアプリケーションの問題に関する[既知の問題](#known)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="1df9e-119">See [Known Issues](#known) for problems with applications after installing the 2019 .Net SameSite updates.</span></span>

## <a name="using-samesite-in-aspnet-472-and-48"></a><span data-ttu-id="1df9e-120">ASP.NET 4.7.2 と4.8 での SameSite の使用</span><span class="sxs-lookup"><span data-stu-id="1df9e-120">Using SameSite in ASP.NET 4.7.2 and 4.8</span></span>

<span data-ttu-id="1df9e-121">.Net 4.7.2 と4.8 では、年 12 2019 月に更新プログラムがリリースされてから、SameSite の[2019 ドラフト標準](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00)がサポートされています。</span><span class="sxs-lookup"><span data-stu-id="1df9e-121">.Net 4.7.2 and 4.8 supports the [2019 draft standard](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00) for SameSite since the release of updates in December 2019.</span></span> <span data-ttu-id="1df9e-122">開発者は、 [HttpCookie プロパティ](/dotnet/api/system.web.httpcookie.samesite#System_Web_HttpCookie_SameSite)を使用して、SameSite ヘッダーの値をプログラムで制御できます。</span><span class="sxs-lookup"><span data-stu-id="1df9e-122">Developers are able to programmatically control the value of the SameSite header using the [HttpCookie.SameSite property](/dotnet/api/system.web.httpcookie.samesite#System_Web_HttpCookie_SameSite).</span></span> <span data-ttu-id="1df9e-123">`SameSite` プロパティを `Strict`、`Lax`、または `None` に設定すると、これらの値が cookie を使用してネットワーク上に書き込まれます。</span><span class="sxs-lookup"><span data-stu-id="1df9e-123">Setting the `SameSite` property to `Strict`, `Lax`, or `None` results in those values being written on the network with the cookie.</span></span> <span data-ttu-id="1df9e-124">これを `(SameSiteMode)(-1)` に設定すると、cookie を使用してネットワークに SameSite ヘッダーを含める必要がなくなります。</span><span class="sxs-lookup"><span data-stu-id="1df9e-124">Setting it equal to `(SameSiteMode)(-1)` indicates that no SameSite header should be included on the network with the cookie.</span></span> <span data-ttu-id="1df9e-125">構成ファイルの[HttpCookie プロパティ](/dotnet/api/system.web.httpcookie.secure)または ' requireSSL ' を使用して、cookie を `Secure` としてマークできます。</span><span class="sxs-lookup"><span data-stu-id="1df9e-125">The [HttpCookie.Secure Property](/dotnet/api/system.web.httpcookie.secure), or 'requireSSL' in config files, can be used to mark the cookie as `Secure` or not.</span></span>

<span data-ttu-id="1df9e-126">新しい `HttpCookie` インスタンスは、既定で `SameSite=(SameSiteMode)(-1)` と `Secure=false`になります。</span><span class="sxs-lookup"><span data-stu-id="1df9e-126">New `HttpCookie` instances will default to `SameSite=(SameSiteMode)(-1)` and `Secure=false`.</span></span> <span data-ttu-id="1df9e-127">これらの既定値は、`system.web/httpCookies` 構成セクションでオーバーライドできます。この場合、文字列 `"Unspecified"` は `(SameSiteMode)(-1)`のわかりやすい構成のみの構文です。</span><span class="sxs-lookup"><span data-stu-id="1df9e-127">These defaults can be overridden in the `system.web/httpCookies` configuration section, where the string `"Unspecified"` is a friendly configuration-only syntax for `(SameSiteMode)(-1)`:</span></span>

```xml
<configuration>
 <system.web>
  <httpCookies sameSite="[Strict|Lax|None|Unspecified]" requireSSL="[true|false]" />
 <system.web>
<configuration>
```

<span data-ttu-id="1df9e-128">また、ASP.Net は、匿名認証、フォーム認証、セッション状態、ロール管理といった機能について、独自の4つの cookie を発行します。</span><span class="sxs-lookup"><span data-stu-id="1df9e-128">ASP.Net also issues four specific cookies of its own for these features: Anonymous Authentication, Forms Authentication, Session State, and Role Management.</span></span> <span data-ttu-id="1df9e-129">ランタイムで取得したこれらのクッキーのインスタンスは、他の HttpCookie インスタンスと同様に、`SameSite` と `Secure` のプロパティを使用して操作できます。</span><span class="sxs-lookup"><span data-stu-id="1df9e-129">Instances of these cookies obtained in runtime can be manipulated using the `SameSite` and `Secure` properties just like any other HttpCookie instance.</span></span> <span data-ttu-id="1df9e-130">ただし、SameSite 標準の寄せ集めが発生しているため、これらの4つの機能の構成オプションには一貫性がありません。</span><span class="sxs-lookup"><span data-stu-id="1df9e-130">However, due to the patchwork emergence of the SameSite standard, configuration options for these four features cookies is inconsistent.</span></span> <span data-ttu-id="1df9e-131">関連する構成セクションと属性 (既定値) を以下に示します。</span><span class="sxs-lookup"><span data-stu-id="1df9e-131">The relevant configuration sections and attributes, with defaults, are shown below.</span></span> <span data-ttu-id="1df9e-132">フィーチャーに `SameSite` または `Secure` 関連属性がない場合、この機能は、前述の `system.web/httpCookies` セクションで構成されている既定値にフォールバックします。</span><span class="sxs-lookup"><span data-stu-id="1df9e-132">If there is no `SameSite` or `Secure` related attribute for a feature, then the feature will fall back on the defaults configured in the `system.web/httpCookies` section discussed above.</span></span>

```xml
<configuration>
 <system.web>
  <anonymousIdentification cookieRequireSSL="false" /> <!-- No config attribute for SameSite -->
  <authentication>
   <forms cookieSameSite="Lax" requireSSL="false" />
  </authentication>
  <sessionState cookieSameSite="Lax" /> <!-- No config attribute for Secure -->
  <roleManager cookieRequireSSL="false" /> <!-- No config attribute for SameSite -->
 <system.web>
<configuration>
```  

<span data-ttu-id="1df9e-133">**注**: ' 未指定 ' は、現時点では `system.web/httpCookies@sameSite` にのみ使用できます。</span><span class="sxs-lookup"><span data-stu-id="1df9e-133">**Note**: 'Unspecified' is only available to `system.web/httpCookies@sameSite` at the moment.</span></span> <span data-ttu-id="1df9e-134">今後の更新で、以前に表示されていた cookieSameSite 属性に同様の構文を追加することを願っています。</span><span class="sxs-lookup"><span data-stu-id="1df9e-134">We hope to add similar syntax to the previously shown cookieSameSite attributes in future updates.</span></span> <span data-ttu-id="1df9e-135">コード内の `(SameSiteMode)(-1)` の設定は、これらの cookie のインスタンスでも機能します。 \*</span><span class="sxs-lookup"><span data-stu-id="1df9e-135">Setting `(SameSiteMode)(-1)` in code still works on instances of these cookies.\*</span></span>

[!INCLUDE[](~/includes/MTcomments.md)]

<a name="retargeting"></a>

### <a name="retarget-net-apps"></a><span data-ttu-id="1df9e-136">.NET アプリの再ターゲット</span><span class="sxs-lookup"><span data-stu-id="1df9e-136">Retarget .NET apps</span></span>

<span data-ttu-id="1df9e-137">.NET 4.7.2 以降をターゲットにするには:</span><span class="sxs-lookup"><span data-stu-id="1df9e-137">To target .NET 4.7.2 or later:</span></span>

* <span data-ttu-id="1df9e-138">Web.config に次のもの*が含まれていること*を確認します。</span><span class="sxs-lookup"><span data-stu-id="1df9e-138">Ensure *web.config* contains the following:</span></span>  <!-- review, I removed `debug="true"` -->

  ```xml
  <system.web>
    <compilation targetFramework="4.7.2"/>
    <httpRuntime targetFramework="4.7.2"/>
  </system.web>

* Verify the project file contains the correct [TargetFrameworkVersion](/visualstudio/msbuild/msbuild-target-framework-and-target-platform?view=vs-2019):

  ```xml
  <TargetFrameworkVersion>v4.7.2</TargetFrameworkVersion>
  ```

  <span data-ttu-id="1df9e-139">詳細については、「 [.Net 移行ガイド」](/dotnet/framework/migration-guide/)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="1df9e-139">The [.NET Migration Guide](/dotnet/framework/migration-guide/) has more details.</span></span>

* <span data-ttu-id="1df9e-140">プロジェクトの NuGet パッケージが、正しいバージョンのフレームワークを対象としていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="1df9e-140">Verify NuGet packages in the project are targeted at the correct framework version.</span></span> <span data-ttu-id="1df9e-141">次の例のように、*パッケージの .config*ファイルを調べることで、正しいフレームワークのバージョンを確認できます。</span><span class="sxs-lookup"><span data-stu-id="1df9e-141">You can verify the correct framework version by examining the *packages.config* file, for example:</span></span>

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <packages>
    <package id="Microsoft.AspNet.Mvc" version="5.2.7" targetFramework="net472" />
    <package id="Microsoft.ApplicationInsights" version="2.4.0" targetFramework="net451" />
  </packages>
  ```

  <span data-ttu-id="1df9e-142">上記の*パッケージ .config*ファイルの `Microsoft.ApplicationInsights` パッケージは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="1df9e-142">In the preceding *packages.config* file, the `Microsoft.ApplicationInsights` package:</span></span>
    * <span data-ttu-id="1df9e-143">は .NET 4.5.1 を対象としています。</span><span class="sxs-lookup"><span data-stu-id="1df9e-143">Is  targeted against .NET 4.5.1.</span></span>
    * <span data-ttu-id="1df9e-144">フレームワークターゲットをターゲットとする更新されたパッケージが存在する場合は、`targetFramework` 属性を `net472` に更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="1df9e-144">Should have its `targetFramework` attribute updated to `net472` if an updated package targeting your framework target exists.</span></span>

<a name="nope"></a>

### <a name="net-versions-earlier-than-472"></a><span data-ttu-id="1df9e-145">4\.7.2 より前の .NET バージョン</span><span class="sxs-lookup"><span data-stu-id="1df9e-145">.NET versions earlier than 4.7.2</span></span>

<span data-ttu-id="1df9e-146">Microsoft では、同じサイトの cookie 属性の書き込みを4.7.2 する .NET バージョンよりもサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="1df9e-146">Microsoft does not support .NET versions lower that 4.7.2 for writing the same-site cookie attribute.</span></span> <span data-ttu-id="1df9e-147">次のような信頼性の高い方法が見つかりませんでした。</span><span class="sxs-lookup"><span data-stu-id="1df9e-147">We have not found a reliable way to:</span></span>

* <span data-ttu-id="1df9e-148">ブラウザーのバージョンに基づいて、属性が正しく記述されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="1df9e-148">Ensure the attribute is written correctly based on browser version.</span></span>
* <span data-ttu-id="1df9e-149">以前のバージョンの framework で認証とセッション cookie をインターセプトして調整します。</span><span class="sxs-lookup"><span data-stu-id="1df9e-149">Intercept and adjust authentication and session cookies on older framework versions.</span></span>

### <a name="december-patch-behavior-changes"></a><span data-ttu-id="1df9e-150">12月のパッチ動作の変更</span><span class="sxs-lookup"><span data-stu-id="1df9e-150">December patch behavior changes</span></span>

<span data-ttu-id="1df9e-151">.NET Framework の特定の動作変更は、`SameSite` プロパティが `None` の値を解釈する方法です。</span><span class="sxs-lookup"><span data-stu-id="1df9e-151">The specific behavior change for .NET Framework is how the `SameSite` property interprets the `None` value:</span></span>

* <span data-ttu-id="1df9e-152">パッチの適用前は、次のような `None` の値になります。</span><span class="sxs-lookup"><span data-stu-id="1df9e-152">Before the patch a value of `None` meant:</span></span>
  * <span data-ttu-id="1df9e-153">属性をまったく生成しません。</span><span class="sxs-lookup"><span data-stu-id="1df9e-153">Do not emit the attribute at all.</span></span>
* <span data-ttu-id="1df9e-154">修正プログラムの適用後:</span><span class="sxs-lookup"><span data-stu-id="1df9e-154">After the patch:</span></span>
  * <span data-ttu-id="1df9e-155">`None`値は、"`None`の値を持つ属性を生成する" ことを意味します。</span><span class="sxs-lookup"><span data-stu-id="1df9e-155">A value of `None`it means "Emit the attribute with a value of `None`".</span></span>
  * <span data-ttu-id="1df9e-156">`(SameSiteMode)(-1)` の `SameSite` 値を指定すると、属性は出力されません。</span><span class="sxs-lookup"><span data-stu-id="1df9e-156">A `SameSite` value of `(SameSiteMode)(-1)` causes the attribute not to be emitted.</span></span>

<span data-ttu-id="1df9e-157">フォーム認証およびセッション状態 cookie の既定の SameSite 値は、`None` から `Lax`に変更されました。</span><span class="sxs-lookup"><span data-stu-id="1df9e-157">The default SameSite value for forms authentication and session state cookies was changed from `None` to `Lax`.</span></span>

### <a name="summary-of-change-impact-on-browsers"></a><span data-ttu-id="1df9e-158">ブラウザーへの変更の影響の概要</span><span class="sxs-lookup"><span data-stu-id="1df9e-158">Summary of change impact on browsers</span></span>

<span data-ttu-id="1df9e-159">修正プログラムをインストールし、`SameSite.None`でクッキーを発行すると、次の2つのいずれかが発生します。</span><span class="sxs-lookup"><span data-stu-id="1df9e-159">If you install the patch and issue a cookie with `SameSite.None`, one of two things will happen:</span></span>
* <span data-ttu-id="1df9e-160">Chrome v80 は、この cookie を新しい実装に従って扱い、cookie に同じサイト制限を適用しません。</span><span class="sxs-lookup"><span data-stu-id="1df9e-160">Chrome v80 will treat this cookie according to the new implementation, and not enforce same site restrictions on the cookie.</span></span>
* <span data-ttu-id="1df9e-161">新しい実装をサポートするように更新されていないブラウザーは、前の実装に従います。</span><span class="sxs-lookup"><span data-stu-id="1df9e-161">Any browser that has not been updated to support the new implementation will follow the old implementation.</span></span> <span data-ttu-id="1df9e-162">以前の実装では、次のようになります。</span><span class="sxs-lookup"><span data-stu-id="1df9e-162">The old implementation says:</span></span>
  * <span data-ttu-id="1df9e-163">理解していない値が表示された場合は無視し、厳密に同じサイト制限に切り替えます。</span><span class="sxs-lookup"><span data-stu-id="1df9e-163">If you see a value you don't understand, ignore it and switch to strict same site restrictions.</span></span>

<span data-ttu-id="1df9e-164">そのため、アプリが Chrome で破損しているか、他のさまざまな場所で中断しています。</span><span class="sxs-lookup"><span data-stu-id="1df9e-164">So either the app breaks in Chrome, or you break in numerous other places.</span></span>

## <a name="history-and-changes"></a><span data-ttu-id="1df9e-165">履歴と変更</span><span class="sxs-lookup"><span data-stu-id="1df9e-165">History and changes</span></span>

<span data-ttu-id="1df9e-166">SameSite のサポートは、 [2016 ドラフト標準](https://tools.ietf.org/html/draft-west-first-party-cookies-07#section-4.1)を使用して最初に .net 4.7.2 に実装されました。</span><span class="sxs-lookup"><span data-stu-id="1df9e-166">SameSite support was first implemented in .NET 4.7.2 using the [2016 draft standard](https://tools.ietf.org/html/draft-west-first-party-cookies-07#section-4.1).</span></span>

<span data-ttu-id="1df9e-167">Windows の2019年11月19日の更新プログラムで、.NET 4.7.2 + が2016標準から2019標準に更新されました。</span><span class="sxs-lookup"><span data-stu-id="1df9e-167">The November 19, 2019 updates for Windows updated .NET 4.7.2+ from the 2016 standard to the 2019 standard.</span></span> <span data-ttu-id="1df9e-168">その他のバージョンの Windows では、追加の更新が予定されています。</span><span class="sxs-lookup"><span data-stu-id="1df9e-168">Additional updates are forthcoming for other versions of Windows.</span></span> <span data-ttu-id="1df9e-169">詳細については、<xref:samesite/kbs-samesite> を参照してください。</span><span class="sxs-lookup"><span data-stu-id="1df9e-169">For more information, see <xref:samesite/kbs-samesite>.</span></span>

 <span data-ttu-id="1df9e-170">SameSite 仕様の2019ドラフト:</span><span class="sxs-lookup"><span data-stu-id="1df9e-170">The 2019 draft of the SameSite specification:</span></span>

* <span data-ttu-id="1df9e-171">は、2016ドラフトとの下位互換性が**ありません**。</span><span class="sxs-lookup"><span data-stu-id="1df9e-171">Is **not** backwards compatible with the 2016 draft.</span></span> <span data-ttu-id="1df9e-172">詳細については、このドキュメントの「[古いブラウザーのサポート](#sob)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="1df9e-172">For more information, see [Supporting older browsers](#sob) in this document.</span></span>
* <span data-ttu-id="1df9e-173">Cookie を既定で `SameSite=Lax` として扱うことを指定します。</span><span class="sxs-lookup"><span data-stu-id="1df9e-173">Specifies cookies are treated as `SameSite=Lax` by default.</span></span>
* <span data-ttu-id="1df9e-174">クロスサイト配信を有効にするために `SameSite=None` を明示的にアサートする cookie も `Secure`としてマークするように指定します。</span><span class="sxs-lookup"><span data-stu-id="1df9e-174">Specifies cookies that explicitly assert `SameSite=None` in order to enable cross-site delivery should also be marked as `Secure`.</span></span>
* <span data-ttu-id="1df9e-175">は、上記の KB に記載されているように発行された修正プログラムによってサポートされています。</span><span class="sxs-lookup"><span data-stu-id="1df9e-175">Is supported by patches issued as described in the KB's listed above.</span></span>
* <span data-ttu-id="1df9e-176">[2 月 2020](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)日に既定で[Chrome](https://chromestatus.com/feature/5088147346030592)によって有効になるようにスケジュールされています。</span><span class="sxs-lookup"><span data-stu-id="1df9e-176">Is scheduled to be enabled by [Chrome](https://chromestatus.com/feature/5088147346030592) by default in [Feb 2020](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html).</span></span> <span data-ttu-id="1df9e-177">ブラウザーは2019でこの標準への移行を開始しました。</span><span class="sxs-lookup"><span data-stu-id="1df9e-177">Browsers started moving to this standard in 2019.</span></span>

<a name="known"><a/>

## <a name="known-issues"></a><span data-ttu-id="1df9e-178">既知の問題</span><span class="sxs-lookup"><span data-stu-id="1df9e-178">Known Issues</span></span>

<span data-ttu-id="1df9e-179">2016と2019のドラフト仕様には互換性がないため、11 2019 月の .Net Framework の更新プログラムでは、いくつかの変更が行われている可能性があります。</span><span class="sxs-lookup"><span data-stu-id="1df9e-179">Because the 2016 and 2019 draft specifications are not compatible, the November 2019 .Net Framework update introduces some changes that may be breaking.</span></span>

* <span data-ttu-id="1df9e-180">セッション状態とフォーム認証 cookie が、未指定ではなく `Lax` としてネットワークに書き込まれるようになりました。</span><span class="sxs-lookup"><span data-stu-id="1df9e-180">Session State and Forms Authentication cookies are now written to the network as `Lax` instead of unspecified.</span></span>
  * <span data-ttu-id="1df9e-181">ほとんどのアプリは `SameSite=Lax` cookie で動作しますが、`iframe` を使用するサイトまたはアプリケーションに投稿するアプリでは、セッション状態またはフォーム認証 cookie が想定どおりに使用されていないことがわかります。</span><span class="sxs-lookup"><span data-stu-id="1df9e-181">While most apps work with `SameSite=Lax` cookies, apps that POST across sites or applications that make use of `iframe` may find that their session state or forms authorization cookies aren't being used as expected.</span></span> <span data-ttu-id="1df9e-182">これを解決するには、前述のように、適切な構成セクションの `cookieSameSite` 値を変更します。</span><span class="sxs-lookup"><span data-stu-id="1df9e-182">To remedy this, change the `cookieSameSite` value in the appropriate configuration section as discussed previously.</span></span>
* <span data-ttu-id="1df9e-183">コードまたは構成で明示的に `SameSite=None` を設定する HttpCookies では、以前は省略されていましたが、この値は cookie で記述されています。</span><span class="sxs-lookup"><span data-stu-id="1df9e-183">HttpCookies that explicitly set `SameSite=None` in code or configuration now have that value written with the cookie, whereas it was previously omitted.</span></span> <span data-ttu-id="1df9e-184">これにより、2016ドラフト標準のみをサポートする古いブラウザーで問題が発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="1df9e-184">This may cause issues with older browsers that only support the 2016 draft standard.</span></span>
  * <span data-ttu-id="1df9e-185">`SameSite=None` cookie を使用して2019ドラフト標準をサポートするブラウザーを対象としている場合は、`Secure` にマークしたり、認識されなかったりすることを忘れないでください。</span><span class="sxs-lookup"><span data-stu-id="1df9e-185">When targeting browsers supporting the 2019 draft standard with `SameSite=None` cookies, remember to also mark them `Secure` or they may not be recognized.</span></span>
  * <span data-ttu-id="1df9e-186">`SameSite=None`を書き込まない場合の2016の動作に戻すには、アプリ設定 `aspnet:SupressSameSiteNone=true`を使用します。</span><span class="sxs-lookup"><span data-stu-id="1df9e-186">To revert to the 2016 behavior of not writing `SameSite=None`, use the app setting `aspnet:SupressSameSiteNone=true`.</span></span> <span data-ttu-id="1df9e-187">これは、アプリ内のすべての HttpCookies に適用されることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="1df9e-187">Note that this will apply to all HttpCookies in the app.</span></span>

### <a name="azure-app-servicesamesite-cookie-handling"></a><span data-ttu-id="1df9e-188">Azure App Service — SameSite cookie 処理</span><span class="sxs-lookup"><span data-stu-id="1df9e-188">Azure App Service—SameSite cookie handling</span></span>

<span data-ttu-id="1df9e-189">.Net 4.7.2 アプリで SameSite の動作を構成 Azure App Service する方法の詳細については[、「Azure App Service — SameSite cookie 処理」と「.NET Framework 4.7.2 patch](https://azure.microsoft.com/updates/app-service-samesite-cookie-update/) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="1df9e-189">See [Azure App Service—SameSite cookie handling and .NET Framework 4.7.2 patch](https://azure.microsoft.com/updates/app-service-samesite-cookie-update/) for information about how Azure App Service is configuring SameSite behaviors in .Net 4.7.2 apps.</span></span>

<a name="sob"></a>

## <a name="supporting-older-browsers"></a><span data-ttu-id="1df9e-190">古いブラウザーのサポート</span><span class="sxs-lookup"><span data-stu-id="1df9e-190">Supporting older browsers</span></span>

<span data-ttu-id="1df9e-191">2016 SameSite 標準では、不明な値を `SameSite=Strict` 値として処理する必要があることが義務付けられています。</span><span class="sxs-lookup"><span data-stu-id="1df9e-191">The 2016 SameSite standard mandated that unknown values must be treated as `SameSite=Strict` values.</span></span> <span data-ttu-id="1df9e-192">2016 SameSite 標準をサポートする古いブラウザーからアクセスされるアプリは、値が `None`の SameSite プロパティを取得すると壊れます。</span><span class="sxs-lookup"><span data-stu-id="1df9e-192">Apps accessed from older browsers which support the 2016 SameSite standard may break when they get a SameSite property with a value of `None`.</span></span> <span data-ttu-id="1df9e-193">Web apps が古いブラウザーをサポートする予定の場合は、ブラウザーの検出を実装する必要があります。</span><span class="sxs-lookup"><span data-stu-id="1df9e-193">Web apps must implement browser detection if they intend to support older browsers.</span></span> <span data-ttu-id="1df9e-194">ASP.NET は、ユーザーエージェントの値が変動し頻繁に変更されるため、ブラウザーの検出を実装しません。</span><span class="sxs-lookup"><span data-stu-id="1df9e-194">ASP.NET doesn't implement browser detection because User-Agents values are highly volatile and change frequently.</span></span>

<span data-ttu-id="1df9e-195">Microsoft がこの問題を解決するには、ブラウザーがサポートしていないことがわかっている場合に、ブラウザー検出コンポーネントを実装して cookie から `sameSite=None` 属性を取り除くことができます。</span><span class="sxs-lookup"><span data-stu-id="1df9e-195">Microsoft's approach to fixing the problem is to help you implement browser detection components to strip the `sameSite=None` attribute from cookies if a browser is known to not support it.</span></span> <span data-ttu-id="1df9e-196">Google のアドバイスは、2つのクッキーを発行することでした。1つは新しい属性で、もう1つは属性なしです。</span><span class="sxs-lookup"><span data-stu-id="1df9e-196">Google's advice was to issue double cookies, one with the new attribute, and one without the attribute at all.</span></span> <span data-ttu-id="1df9e-197">ただし、Google のアドバイスは限定されています。</span><span class="sxs-lookup"><span data-stu-id="1df9e-197">However we consider Google's advice limited.</span></span> <span data-ttu-id="1df9e-198">一部のブラウザー (特にモバイルブラウザー) では、サイトの cookie の数に関する制限が非常に小さいか、またはドメイン名が送信できます。</span><span class="sxs-lookup"><span data-stu-id="1df9e-198">Some browsers, especially mobile browsers have very small limits on the number of cookies a site, or a domain name can send.</span></span> <span data-ttu-id="1df9e-199">複数の cookie を送信すると、特に認証 cookie などの大規模な cookie はモバイルブラウザーの制限に達する可能性があり、その結果、診断や修正が困難なアプリの障害が発生します。</span><span class="sxs-lookup"><span data-stu-id="1df9e-199">Sending multiple cookies, especially large cookies like authentication cookies can reach the mobile browser limit very quickly, causing app failures that are hard to diagnose and fix.</span></span> <span data-ttu-id="1df9e-200">さらに、フレームワークとして、サードパーティのコードとコンポーネントの大規模なエコシステムがあり、二重 cookie のアプローチを使用するように更新することはできません。</span><span class="sxs-lookup"><span data-stu-id="1df9e-200">Furthermore as a framework there is a large ecosystem of third party code and components that may not be updated to use a double cookie approach.</span></span>

<span data-ttu-id="1df9e-201">[この GitHub リポジトリ]()のサンプルプロジェクトで使用されているブラウザー検出コードは、2つのファイルに含まれています。</span><span class="sxs-lookup"><span data-stu-id="1df9e-201">The browser detection code used in the sample projects in [this GitHub repository]() is contained in two files</span></span>

* [<span data-ttu-id="1df9e-202">C#SameSiteSupport.cs</span><span class="sxs-lookup"><span data-stu-id="1df9e-202">C# SameSiteSupport.cs</span></span>](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/SameSiteSupport.cs)
* [<span data-ttu-id="1df9e-203">VB SameSiteSupport</span><span class="sxs-lookup"><span data-stu-id="1df9e-203">VB SameSiteSupport.vb</span></span>](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/SameSiteSupport.vb)

<span data-ttu-id="1df9e-204">これらの検出は、2016標準をサポートし、属性を完全に削除する必要がある、最も一般的なブラウザーエージェントです。</span><span class="sxs-lookup"><span data-stu-id="1df9e-204">These detections are the most common browser agents we have seen that support the 2016 standard and for which the attribute needs to be completely removed.</span></span> <span data-ttu-id="1df9e-205">完全な実装とは言えません。</span><span class="sxs-lookup"><span data-stu-id="1df9e-205">It isn't meant as a complete implementation:</span></span>

* <span data-ttu-id="1df9e-206">テストサイトではないブラウザーがアプリに表示されることがあります。</span><span class="sxs-lookup"><span data-stu-id="1df9e-206">Your app may see browsers that our test sites do not.</span></span>
* <span data-ttu-id="1df9e-207">必要に応じて環境に検出を追加できるように準備する必要があります。</span><span class="sxs-lookup"><span data-stu-id="1df9e-207">You should be prepared to add detections as necessary for your environment.</span></span>

<span data-ttu-id="1df9e-208">検出を接続する方法は、使用している .NET のバージョンと web フレームワークによって異なります。</span><span class="sxs-lookup"><span data-stu-id="1df9e-208">How you wire up the detection varies according the version of .NET and the web framework that you are using.</span></span> <span data-ttu-id="1df9e-209">[HttpCookie](/dotnet/api/system.web.httpcookie) call サイトでは、次のコードを呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="1df9e-209">The following code can be called at the [HttpCookie](/dotnet/api/system.web.httpcookie) call site:</span></span>

[!code-csharp[](sample/SameSiteCheck.cs?name=snippet)]

<span data-ttu-id="1df9e-210">次の ASP.NET 4.7.2 SameSite cookie のトピックを参照してください。</span><span class="sxs-lookup"><span data-stu-id="1df9e-210">See the following ASP.NET 4.7.2 SameSite cookie topics:</span></span>

* [<span data-ttu-id="1df9e-211">C#MVC</span><span class="sxs-lookup"><span data-stu-id="1df9e-211">C# MVC</span></span>](xref:samesite/csMVC)
* [<span data-ttu-id="1df9e-212">C#WebForms</span><span class="sxs-lookup"><span data-stu-id="1df9e-212">C# WebForms</span></span>](xref:samesite/CSharpWebForms)
* [<span data-ttu-id="1df9e-213">VB WebForms</span><span class="sxs-lookup"><span data-stu-id="1df9e-213">VB WebForms</span></span>](xref:samesite/vbWF)
* [<span data-ttu-id="1df9e-214">VB MVC</span><span class="sxs-lookup"><span data-stu-id="1df9e-214">VB MVC</span></span>](xref:samesite/vbMVC)
<!--
* <xref:samesite/csMVC>
* <xref:samesite/CSharpWebForms>
* <xref:samesite/vbWF>
* <xref:samesite/vbMVC>
-->

### <a name="ensuring-your-site-redirects-to-https"></a><span data-ttu-id="1df9e-215">サイトが HTTPS にリダイレクトされるようにする</span><span class="sxs-lookup"><span data-stu-id="1df9e-215">Ensuring your site redirects to HTTPS</span></span>

<span data-ttu-id="1df9e-216">ASP.NET 4.x、WebForms、および MVC では、 [IIS の URL 書き換え](/iis/extensions/url-rewrite-module/creating-rewrite-rules-for-the-url-rewrite-module)機能を使用して、すべての要求を HTTPS にリダイレクトすることができます。</span><span class="sxs-lookup"><span data-stu-id="1df9e-216">For ASP.NET 4.x, WebForms and MVC, [IIS's URL Rewrite](/iis/extensions/url-rewrite-module/creating-rewrite-rules-for-the-url-rewrite-module) feature can be used to redirect all requests to HTTPS.</span></span> <span data-ttu-id="1df9e-217">次の XML は、ルールの例を示しています。</span><span class="sxs-lookup"><span data-stu-id="1df9e-217">The following XML shows a sample rule:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
  <system.webServer>
    <rewrite>
      <rules>
        <rule name="Redirect to https" stopProcessing="true">
          <match url="(.*)"/>
          <conditions>
            <add input="{HTTPS}" pattern="Off"/>
            <add input="{REQUEST_METHOD}" pattern="^get$|^head$" />
          </conditions>
          <action type="Redirect" url="https://{HTTP_HOST}/{R:1}" redirectType="Permanent"/>
        </rule>
      </rules>
    </rewrite>
  </system.webServer>
</configuration>
```

<span data-ttu-id="1df9e-218">[IIS URL 書き換え](https://www.iis.net/downloads/microsoft/url-rewrite)のオンプレミスインストールでは、のインストールが必要になる可能性があるオプションの機能です。</span><span class="sxs-lookup"><span data-stu-id="1df9e-218">In on-premises installations of [IIS URL Rewrite](https://www.iis.net/downloads/microsoft/url-rewrite) is an optional feature that may need installing.</span></span>

## <a name="test-apps-for-samesite-problems"></a><span data-ttu-id="1df9e-219">SameSite 問題のアプリをテストする</span><span class="sxs-lookup"><span data-stu-id="1df9e-219">Test apps for SameSite problems</span></span>

<span data-ttu-id="1df9e-220">サポートされているブラウザーを使用してアプリをテストし、cookie を含むシナリオを確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="1df9e-220">You must test your app with the browsers you support and go through your scenarios that involve cookies.</span></span> <span data-ttu-id="1df9e-221">Cookie のシナリオには通常、</span><span class="sxs-lookup"><span data-stu-id="1df9e-221">Cookie scenarios typically involve</span></span>

* <span data-ttu-id="1df9e-222">ログインフォーム</span><span class="sxs-lookup"><span data-stu-id="1df9e-222">Login forms</span></span>
* <span data-ttu-id="1df9e-223">Facebook、Azure AD、OAuth、OIDC などの外部ログインメカニズム</span><span class="sxs-lookup"><span data-stu-id="1df9e-223">External login mechanisms such as Facebook, Azure AD, OAuth and OIDC</span></span>
* <span data-ttu-id="1df9e-224">他のサイトからの要求を受け入れるページ</span><span class="sxs-lookup"><span data-stu-id="1df9e-224">Pages that accept requests from other sites</span></span>
* <span data-ttu-id="1df9e-225">Iframe に埋め込まれるように設計されたアプリのページ</span><span class="sxs-lookup"><span data-stu-id="1df9e-225">Pages in your app designed to be embedded in iframes</span></span>

<span data-ttu-id="1df9e-226">アプリで cookie が作成、保存、および削除されたことを確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="1df9e-226">You should check that cookies are created, persisted and deleted correctly in your app.</span></span>

<span data-ttu-id="1df9e-227">サードパーティのログインによってなどのリモートサイトと対話するアプリでは、次の操作を行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="1df9e-227">Apps that interact with remote sites such as through third-party login need to:</span></span>

* <span data-ttu-id="1df9e-228">複数のブラウザーで相互作用をテストします。</span><span class="sxs-lookup"><span data-stu-id="1df9e-228">Test the interaction on multiple browsers.</span></span>
* <span data-ttu-id="1df9e-229">このドキュメントで説明され[ているブラウザーの検出と軽減策](#sob)を適用します。</span><span class="sxs-lookup"><span data-stu-id="1df9e-229">Apply the [browser detection and mitigation](#sob) discussed in this document.</span></span>

<span data-ttu-id="1df9e-230">新しい SameSite 動作にオプトインできるクライアントバージョンを使用して、web アプリをテストします。</span><span class="sxs-lookup"><span data-stu-id="1df9e-230">Test web apps using a client version that can opt-in to the new SameSite behavior.</span></span> <span data-ttu-id="1df9e-231">Chrome、Firefox、Chromium Edge には、テストに使用できる新しいオプトイン機能フラグがあります。</span><span class="sxs-lookup"><span data-stu-id="1df9e-231">Chrome, Firefox, and Chromium Edge all have new opt-in feature flags that can be used for testing.</span></span> <span data-ttu-id="1df9e-232">アプリが SameSite パッチを適用したら、古いクライアントバージョン (特に Safari) を使用してテストします。</span><span class="sxs-lookup"><span data-stu-id="1df9e-232">After your app applies the SameSite patches, test it with older client versions, especially Safari.</span></span> <span data-ttu-id="1df9e-233">詳細については、このドキュメントの「[古いブラウザーのサポート](#sob)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="1df9e-233">For more information, see [Supporting older browsers](#sob) in this document.</span></span>

### <a name="test-with-chrome"></a><span data-ttu-id="1df9e-234">Chrome を使用したテスト</span><span class="sxs-lookup"><span data-stu-id="1df9e-234">Test with Chrome</span></span>

<span data-ttu-id="1df9e-235">Chrome 78 + には一時的な軽減策があるため、誤解を招く結果になります。</span><span class="sxs-lookup"><span data-stu-id="1df9e-235">Chrome 78+ gives misleading results because it has a temporary mitigation in place.</span></span> <span data-ttu-id="1df9e-236">Chrome 78 + 一時的な軽減策では、2分前よりも少ない cookie を使用できます。</span><span class="sxs-lookup"><span data-stu-id="1df9e-236">The Chrome 78+ temporary mitigation allows cookies less than two minutes old.</span></span> <span data-ttu-id="1df9e-237">適切なテストフラグが有効になっている Chrome 76 または77では、より正確な結果が得られます。</span><span class="sxs-lookup"><span data-stu-id="1df9e-237">Chrome 76 or 77 with the appropriate test flags enabled provides more accurate results.</span></span> <span data-ttu-id="1df9e-238">新しい SameSite の動作をテストするには、`chrome://flags/#same-site-by-default-cookies` を**有効**に切り替えます。</span><span class="sxs-lookup"><span data-stu-id="1df9e-238">To test the new SameSite behavior toggle `chrome://flags/#same-site-by-default-cookies` to **Enabled**.</span></span> <span data-ttu-id="1df9e-239">新しい `None` 設定で失敗するように、Chrome の旧バージョン (75 以降) が報告されます。</span><span class="sxs-lookup"><span data-stu-id="1df9e-239">Older versions of Chrome (75 and below) are reported to fail with the new `None` setting.</span></span> <span data-ttu-id="1df9e-240">このドキュメントの「[古いブラウザーのサポート](#sob)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="1df9e-240">See [Supporting older browsers](#sob) in this document.</span></span>

<span data-ttu-id="1df9e-241">Google では、以前のバージョンの chrome は使用できません。</span><span class="sxs-lookup"><span data-stu-id="1df9e-241">Google does not make older chrome versions available.</span></span> <span data-ttu-id="1df9e-242">「 [Chromium のダウンロード](https://www.chromium.org/getting-involved/download-chromium)」の手順に従って、Chrome の旧バージョンをテストします。</span><span class="sxs-lookup"><span data-stu-id="1df9e-242">Follow the instructions at [Download Chromium](https://www.chromium.org/getting-involved/download-chromium) to test older versions of Chrome.</span></span> <span data-ttu-id="1df9e-243">以前のバージョンの chrome を検索することによって提供されるリンクから Chrome**をダウンロードしないでください**。</span><span class="sxs-lookup"><span data-stu-id="1df9e-243">Do **not** download Chrome from links provided by searching for older versions of chrome.</span></span>

* [<span data-ttu-id="1df9e-244">Chromium 76 Win64</span><span class="sxs-lookup"><span data-stu-id="1df9e-244">Chromium 76 Win64</span></span>](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/664998/)
* [<span data-ttu-id="1df9e-245">Chromium 74 Win64</span><span class="sxs-lookup"><span data-stu-id="1df9e-245">Chromium 74 Win64</span></span>](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/638880/)
* <span data-ttu-id="1df9e-246">Windows の64ビット版を使用していない場合は、 [Omahaproxy ビューアー](https://omahaproxy.appspot.com/)を使用して、 [Chromium の指示](https://www.chromium.org/getting-involved/download-chromium)に従って、Chrome 74 (v 74.0.3729.108) に対応する Chromium 分岐を調べることができます。</span><span class="sxs-lookup"><span data-stu-id="1df9e-246">If you're not using a 64bit version of Windows you can use the [OmahaProxy viewer](https://omahaproxy.appspot.com/) to look up which Chromium branch corresponds to Chrome 74 (v74.0.3729.108) using the [instructions provided by Chromium](https://www.chromium.org/getting-involved/download-chromium).</span></span>

<span data-ttu-id="1df9e-247">カナリアバージョン `80.0.3975.0`以降では、新しいフラグ `--enable-features=SameSiteDefaultChecksMethodRigorously` を使用することにより、テスト用に厳密ではない + POST 一時軽減を無効にすることができます。これは、軽減策が削除された機能の最終的な終了状態でサイトとサービスをテストできるようにするためのものです。</span><span class="sxs-lookup"><span data-stu-id="1df9e-247">Starting in Canary version `80.0.3975.0`, the Lax+POST temporary mitigation can be disabled for testing purposes using the new flag `--enable-features=SameSiteDefaultChecksMethodRigorously` to allow testing of sites and services in the eventual end state of the feature where the mitigation has been removed.</span></span> <span data-ttu-id="1df9e-248">詳細については、「Chromium Projects [SameSite Updates](https://www.chromium.org/updates/same-site) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="1df9e-248">For more information, see The Chromium Projects [SameSite Updates](https://www.chromium.org/updates/same-site)</span></span>

#### <a name="test-with-chrome-80"></a><span data-ttu-id="1df9e-249">Chrome 80 + を使用したテスト</span><span class="sxs-lookup"><span data-stu-id="1df9e-249">Test with Chrome 80+</span></span>

<span data-ttu-id="1df9e-250">新しい属性をサポートするバージョンの Chrome を[ダウンロード](https://www.google.com/chrome/)します。</span><span class="sxs-lookup"><span data-stu-id="1df9e-250">[Download](https://www.google.com/chrome/) a version of Chrome that supports their new attribute.</span></span> <span data-ttu-id="1df9e-251">このドキュメントの執筆時点では、現在のバージョンは Chrome 80 です。</span><span class="sxs-lookup"><span data-stu-id="1df9e-251">At the time of writing, the current version is Chrome 80.</span></span> <span data-ttu-id="1df9e-252">Chrome 80 では、新しい動作を使用するためにフラグ `chrome://flags/#same-site-by-default-cookies` 有効にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="1df9e-252">Chrome 80 needs the flag `chrome://flags/#same-site-by-default-cookies` enabled to use the new behavior.</span></span> <span data-ttu-id="1df9e-253">また、sameSite 属性が有効になっていない cookie の今後の動作をテストするには、(`chrome://flags/#cookies-without-same-site-must-be-secure`) を有効にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="1df9e-253">You should also enable (`chrome://flags/#cookies-without-same-site-must-be-secure`) to test the upcoming behavior for cookies which have no sameSite attribute enabled.</span></span> <span data-ttu-id="1df9e-254">Chrome 80 はターゲット上にあります。これは、特定の要求に対して一定の猶予期間がある場合でも、`SameSite=Lax`のように属性を持たない cookie をスイッチが処理するようにするためのものです。</span><span class="sxs-lookup"><span data-stu-id="1df9e-254">Chrome 80 is on target to make the switch to treat cookies without the attribute as `SameSite=Lax`, albeit with a timed grace period for certain requests.</span></span> <span data-ttu-id="1df9e-255">時間指定の猶予期間を無効にするには、次のコマンドライン引数を使用して Chrome 80 を起動します。</span><span class="sxs-lookup"><span data-stu-id="1df9e-255">To disable the timed grace period Chrome 80 can be launched with the following command line argument:</span></span>

`--enable-features=SameSiteDefaultChecksMethodRigorously`

<span data-ttu-id="1df9e-256">Chrome 80 では、不足している sameSite 属性について、ブラウザーコンソールに警告メッセージがあります。</span><span class="sxs-lookup"><span data-stu-id="1df9e-256">Chrome 80 has warning messages in the browser console about missing sameSite attributes.</span></span> <span data-ttu-id="1df9e-257">F12 キーを使用してブラウザーコンソールを開きます。</span><span class="sxs-lookup"><span data-stu-id="1df9e-257">Use F12 to open the browser console.</span></span>

### <a name="test-with-safari"></a><span data-ttu-id="1df9e-258">Safari を使用したテスト</span><span class="sxs-lookup"><span data-stu-id="1df9e-258">Test with Safari</span></span>

<span data-ttu-id="1df9e-259">Safari 12 では以前のドラフトが厳密に実装されており、新しい `None` 値が cookie に含まれていると失敗します。</span><span class="sxs-lookup"><span data-stu-id="1df9e-259">Safari 12 strictly implemented the prior draft and fails when the new `None` value is in a cookie.</span></span> <span data-ttu-id="1df9e-260">このドキュメントでは、[古いブラウザーをサポート](#sob)するブラウザーの検出コードを使用して `None` を回避します。</span><span class="sxs-lookup"><span data-stu-id="1df9e-260">`None` is avoided via the browser detection code [Supporting older browsers](#sob) in this document.</span></span> <span data-ttu-id="1df9e-261">MSAL、ADAL、使用している任意のライブラリを使用して、Safari 12、Safari 13、WebKit ベースの OS スタイルのログインをテストします。</span><span class="sxs-lookup"><span data-stu-id="1df9e-261">Test Safari 12, Safari 13, and WebKit based OS style logins using MSAL, ADAL or whatever library you are using.</span></span> <span data-ttu-id="1df9e-262">この問題は、基盤の OS バージョンによって変わります。</span><span class="sxs-lookup"><span data-stu-id="1df9e-262">The problem is dependent on the underlying OS version.</span></span> <span data-ttu-id="1df9e-263">OSX Mojave (10.14) と iOS 12 には、新しい SameSite の動作に互換性の問題があることがわかっています。</span><span class="sxs-lookup"><span data-stu-id="1df9e-263">OSX Mojave (10.14) and iOS 12 are known to have compatibility problems with the new SameSite behavior.</span></span> <span data-ttu-id="1df9e-264">OS を OSX Catalina.properties (10.15) または iOS 13 にアップグレードすると、問題が解決されます。</span><span class="sxs-lookup"><span data-stu-id="1df9e-264">Upgrading the OS to OSX Catalina (10.15) or iOS 13 fixes the problem.</span></span> <span data-ttu-id="1df9e-265">Safari には、現在、新しい仕様動作をテストするオプトインフラグがありません。</span><span class="sxs-lookup"><span data-stu-id="1df9e-265">Safari does not currently have an opt-in flag for testing the new spec behavior.</span></span>

### <a name="test-with-firefox"></a><span data-ttu-id="1df9e-266">Firefox でのテスト</span><span class="sxs-lookup"><span data-stu-id="1df9e-266">Test with Firefox</span></span>

<span data-ttu-id="1df9e-267">新しい標準の Firefox サポートは、バージョン68以降で、[`about:config`] ページで機能フラグ `network.cookie.sameSite.laxByDefault`をオンにしてテストできます。</span><span class="sxs-lookup"><span data-stu-id="1df9e-267">Firefox support for the new standard can be tested on version 68+ by opting in on the `about:config` page with the feature flag `network.cookie.sameSite.laxByDefault`.</span></span> <span data-ttu-id="1df9e-268">以前のバージョンの Firefox との互換性に関する問題は報告されていません。</span><span class="sxs-lookup"><span data-stu-id="1df9e-268">There haven't been reports of compatibility issues with older versions of Firefox.</span></span>

### <a name="test-with-edge-legacy-browser"></a><span data-ttu-id="1df9e-269">Edge (レガシ) ブラウザーを使用したテスト</span><span class="sxs-lookup"><span data-stu-id="1df9e-269">Test with Edge (Legacy) browser</span></span>

<span data-ttu-id="1df9e-270">Edge では、古い SameSite 標準がサポートされています。</span><span class="sxs-lookup"><span data-stu-id="1df9e-270">Edge supports the old SameSite standard.</span></span> <span data-ttu-id="1df9e-271">Edge バージョン44以降では、新しい標準との互換性に関する既知の問題はありません。</span><span class="sxs-lookup"><span data-stu-id="1df9e-271">Edge version 44+ doesn't have any known compatibility problems with the new standard.</span></span>

### <a name="test-with-edge-chromium"></a><span data-ttu-id="1df9e-272">Edge でテストする (Chromium)</span><span class="sxs-lookup"><span data-stu-id="1df9e-272">Test with Edge (Chromium)</span></span>

<span data-ttu-id="1df9e-273">SameSite フラグは `edge://flags/#same-site-by-default-cookies` ページで設定されます。</span><span class="sxs-lookup"><span data-stu-id="1df9e-273">SameSite flags are set on the `edge://flags/#same-site-by-default-cookies` page.</span></span> <span data-ttu-id="1df9e-274">Edge Chromium で互換性の問題は検出されませんでした。</span><span class="sxs-lookup"><span data-stu-id="1df9e-274">No compatibility issues were discovered with Edge Chromium.</span></span>

### <a name="test-with-electron"></a><span data-ttu-id="1df9e-275">電子を使用したテスト</span><span class="sxs-lookup"><span data-stu-id="1df9e-275">Test with Electron</span></span>

<span data-ttu-id="1df9e-276">Electron の複数のバージョンには、Chromium の古いバージョンが含まれています。</span><span class="sxs-lookup"><span data-stu-id="1df9e-276">Versions of Electron include older versions of Chromium.</span></span> <span data-ttu-id="1df9e-277">たとえば、チームによって使用されている電子 66 Chromium のバージョンは、以前の動作を示しています。</span><span class="sxs-lookup"><span data-stu-id="1df9e-277">For example, the version of Electron used by Teams is Chromium 66, which exhibits the older behavior.</span></span> <span data-ttu-id="1df9e-278">製品で使用されている電子版を使用して、独自の互換性テストを実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="1df9e-278">You must perform your own compatibility testing with the version of Electron your product uses.</span></span> <span data-ttu-id="1df9e-279">「[古いブラウザーのサポート](#sob)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="1df9e-279">See [Supporting older browsers](#sob).</span></span>

## <a name="reverting-samesite-patches"></a><span data-ttu-id="1df9e-280">SameSite パッチの復元</span><span class="sxs-lookup"><span data-stu-id="1df9e-280">Reverting SameSite patches</span></span>

<span data-ttu-id="1df9e-281">.NET Framework アプリで更新された sameSite の動作を、`None`の値に対して sameSite 属性が出力されない以前の動作に戻すことができます。また、認証とセッション cookie を元に戻して値を出力しないようにします。</span><span class="sxs-lookup"><span data-stu-id="1df9e-281">You can revert the updated sameSite behavior in .NET Framework apps to its previous behavior where the sameSite attribute is not emitted for a value of `None`, and revert the authentication and session cookies to not emit the value.</span></span> <span data-ttu-id="1df9e-282">Chrome の変更によって、標準への変更をサポートするブラウザーを使用しているユーザーの外部 POST 要求または認証が中断されるため、これは*非常に一時的な修正*として表示されます。</span><span class="sxs-lookup"><span data-stu-id="1df9e-282">This should be viewed as an *extremely temporary fix*, as the Chrome changes will break any external POST requests or authentication for users using browsers which support the changes to the standard.</span></span>

### <a name="reverting-net-472-behavior"></a><span data-ttu-id="1df9e-283">.NET 4.7.2 の動作を元に戻す</span><span class="sxs-lookup"><span data-stu-id="1df9e-283">Reverting .NET 4.7.2 behavior</span></span>

<span data-ttu-id="1df9e-284">Web.config*を更新*して、次の構成設定を含めます。</span><span class="sxs-lookup"><span data-stu-id="1df9e-284">Update *web.config* to include the following configuration settings:</span></span>

```xml
<configuration> 
  <appSettings>
    <add key="aspnet:SuppressSameSiteNone" value="true" />
  </appSettings>
 
  <system.web> 
    <authentication> 
      <forms cookieSameSite="None" /> 
    </authentication> 
    <sessionState cookieSameSite="None" /> 
  </system.web> 
</configuration>
```

## <a name="additional-resources"></a><span data-ttu-id="1df9e-285">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="1df9e-285">Additional resources</span></span>

* [<span data-ttu-id="1df9e-286">ASP.NET と ASP.NET Core での今後の SameSite Cookie の変更</span><span class="sxs-lookup"><span data-stu-id="1df9e-286">Upcoming SameSite Cookie Changes in ASP.NET and ASP.NET Core</span></span>](https://devblogs.microsoft.com/aspnet/upcoming-samesite-cookie-changes-in-asp-net-and-asp-net-core/)
* [<span data-ttu-id="1df9e-287">SameSite および "SameSite = None; のテストとデバッグに関するヒントセキュリティで保護された cookie</span><span class="sxs-lookup"><span data-stu-id="1df9e-287">Tips for testing and debugging SameSite-by-default and “SameSite=None; Secure” cookies</span></span>](https://www.chromium.org/updates/same-site/test-debug)
* [<span data-ttu-id="1df9e-288">Chromium ブログ: 開発者: 新しい SameSite の準備 = None;セキュリティで保護された Cookie の設定</span><span class="sxs-lookup"><span data-stu-id="1df9e-288">Chromium Blog:Developers: Get Ready for New SameSite=None; Secure Cookie Settings</span></span>](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)
* [<span data-ttu-id="1df9e-289">SameSite cookie の説明</span><span class="sxs-lookup"><span data-stu-id="1df9e-289">SameSite cookies explained</span></span>](https://web.dev/samesite-cookies-explained/)
* [<span data-ttu-id="1df9e-290">Chrome の更新</span><span class="sxs-lookup"><span data-stu-id="1df9e-290">Chrome Updates</span></span>](https://www.chromium.org/updates/same-site)
* [<span data-ttu-id="1df9e-291">.NET SameSite パッチ</span><span class="sxs-lookup"><span data-stu-id="1df9e-291">.NET SameSite Patches</span></span>](/aspnet/samesite/kbs-samesite)
* [<span data-ttu-id="1df9e-292">Azure Web アプリケーションと同じサイト情報</span><span class="sxs-lookup"><span data-stu-id="1df9e-292">Azure Web Applications Same Site Information</span></span>](https://azure.microsoft.com/updates/app-service-samesite-cookie-update/)
* [<span data-ttu-id="1df9e-293">Azure Active Directory のサイト情報</span><span class="sxs-lookup"><span data-stu-id="1df9e-293">Azure ActiveDirectory Same Site Information</span></span>](/azure/active-directory/develop/howto-handle-samesite-cookie-changes-chrome-browser)
