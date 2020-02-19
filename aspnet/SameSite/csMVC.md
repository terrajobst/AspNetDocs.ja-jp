---
title: ASP.NET 4.7.2 C# MVC の SameSite cookie サンプル
author: blowdart
description: ASP.NET 4.7.2 C# MVC の SameSite cookie サンプル
ms.author: riande
ms.date: 2/15/2019
uid: samesite/csMVC
ms.openlocfilehash: dcbd0bee009669fb747d74e6ccef07fbae70a236
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2020
ms.locfileid: "77458397"
---
# <a name="samesite-cookie-sample-for-aspnet-472-c-mvc"></a><span data-ttu-id="3fcd5-103">ASP.NET 4.7.2 C# MVC の SameSite cookie サンプル</span><span class="sxs-lookup"><span data-stu-id="3fcd5-103">SameSite cookie sample for ASP.NET 4.7.2 C# MVC</span></span>

<span data-ttu-id="3fcd5-104">.NET Framework 4.7 には[SameSite](https://www.owasp.org/index.php/SameSite)属性のサポートが組み込まれていますが、元の標準に準拠しています。</span><span class="sxs-lookup"><span data-stu-id="3fcd5-104">.NET Framework 4.7 has built-in support for the [SameSite](https://www.owasp.org/index.php/SameSite) attribute, but it adheres to the original standard.</span></span>
<span data-ttu-id="3fcd5-105">パッチを適用した動作により、`SameSite.None` の意味が変更され、値がまったく出力されるのではなく、`None`の値を持つ属性が出力されます。</span><span class="sxs-lookup"><span data-stu-id="3fcd5-105">The patched behavior changed the meaning of `SameSite.None` to emit the attribute with a value of `None`, rather than not emit the value at all.</span></span> <span data-ttu-id="3fcd5-106">値を出力しない場合は、cookie の `SameSite` プロパティを-1 に設定します。</span><span class="sxs-lookup"><span data-stu-id="3fcd5-106">If you want to not emit the value you can set the `SameSite` property on a cookie to -1.</span></span>

## <a name="sampleCode"></a><span data-ttu-id="3fcd5-107">SameSite 属性の書き込み</span><span class="sxs-lookup"><span data-stu-id="3fcd5-107">Writing the SameSite attribute</span></span>

<span data-ttu-id="3fcd5-108">SameSite 属性をクッキーに書き込む方法の例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="3fcd5-108">Following is an example of how to write a SameSite attribute on a cookie;</span></span>

```c#
// Create the cookie
HttpCookie sameSiteCookie = new HttpCookie("SameSiteSample");

// Set a value for the cookieSite none.
// Note this will also require you to be running on HTTPS
sameSiteCookie.Value = "sample";

// Set the secure flag, which Chrome's changes will require for Same
sameSiteCookie.Secure = true;

// Set the cookie to HTTP only which is good practice unless you really do need
// to access it client side in scripts.
sameSiteCookie.HttpOnly = true;

// Add the SameSite attribute, this will emit the attribute with a value of none.
// To not emit the attribute at all set the SameSite property to -1.
sameSiteCookie.SameSite = SameSiteMode.None;

// Add the cookie to the response cookie collection
Response.Cookies.Add(sameSiteCookie);
```

[!INCLUDE[](~/includes/MTcomments.md)]

<span data-ttu-id="3fcd5-109">セッション状態の既定の sameSite 属性は、のセッション設定の ' cookieSameSite ' パラメーターで設定され `web.config`</span><span class="sxs-lookup"><span data-stu-id="3fcd5-109">The default sameSite attribute for session state is set in the 'cookieSameSite' parameter of the session settings in `web.config`</span></span>

```xml
<system.web>
  <sessionState cookieSameSite="None">     
  </sessionState>
</system.web>
```

## <a name="mvc-authentication"></a><span data-ttu-id="3fcd5-110">MVC 認証</span><span class="sxs-lookup"><span data-stu-id="3fcd5-110">MVC Authentication</span></span>

<span data-ttu-id="3fcd5-111">OWIN MVC cookie ベースの認証では、cookie マネージャーを使用して cookie 属性の変更を有効にします。</span><span class="sxs-lookup"><span data-stu-id="3fcd5-111">OWIN MVC cookie based authentication uses a cookie manager to enable the changing of cookie attributes.</span></span> <span data-ttu-id="3fcd5-112">[SameSiteCookieManager.cs](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472CSharpMVC5/SameSiteCookieManager.cs)は、このようなクラスの実装であり、独自のプロジェクトにコピーできます。</span><span class="sxs-lookup"><span data-stu-id="3fcd5-112">The [SameSiteCookieManager.cs](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472CSharpMVC5/SameSiteCookieManager.cs) is an implementation of such a class which you can copy into your own projects.</span></span> 

<span data-ttu-id="3fcd5-113">Owin コンポーネントがすべてバージョン4.1.0 以上にアップグレードされていることを確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="3fcd5-113">You must ensure your Microsoft.Owin components are all upgraded to version 4.1.0 or greater.</span></span> <span data-ttu-id="3fcd5-114">`packages.config` ファイルをチェックして、すべてのバージョン番号が一致していることを確認します。たとえば、のようになります。</span><span class="sxs-lookup"><span data-stu-id="3fcd5-114">Check your `packages.config` file to ensure all the version numbers match, for example.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <!-- other packages -->
  <package id="Microsoft.Owin.Host.SystemWeb" version="4.1.0" targetFramework="net472" />
  <package id="Microsoft.Owin.Security" version="4.1.0" targetFramework="net472" />
  <package id="Microsoft.Owin.Security.Cookies" version="4.1.0" targetFramework="net472" />
  <package id="Microsoft.Web.Infrastructure" version="1.0.0.0" targetFramework="net472" />
  <package id="Owin" version="1.0" targetFramework="net472" />
</packages>
```

<span data-ttu-id="3fcd5-115">次に、スタートアップクラスで CookieManager を使用するように認証コンポーネントを構成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="3fcd5-115">The authentication components must then be configured to use the CookieManager in your startup class;</span></span>

```c#
public void Configuration(IAppBuilder app)
{
    app.UseCookieAuthentication(new CookieAuthenticationOptions
    {
        CookieSameSite = SameSiteMode.None,
        CookieHttpOnly = true,
        CookieSecure = CookieSecureOption.Always,
        CookieManager = new SameSiteCookieManager(new SystemWebCookieManager())
    });
}
```

<span data-ttu-id="3fcd5-116">クッキーマネージャーは、それをサポートする*各*コンポーネントに設定する必要があります。これには、cookieauthentication と OpenIdConnectAuthentication が含まれます。</span><span class="sxs-lookup"><span data-stu-id="3fcd5-116">A cookie manager must be set on *each* component that supports it, this includes CookieAuthentication and OpenIdConnectAuthentication.</span></span>

<span data-ttu-id="3fcd5-117">SystemWebCookieManager は、応答クッキーの統合に[関する既知の問題](https://github.com/aspnet/AspNetKatana/wiki/System.Web-response-cookie-integration-issues)を回避するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="3fcd5-117">The SystemWebCookieManager is used to avoid [known issues](https://github.com/aspnet/AspNetKatana/wiki/System.Web-response-cookie-integration-issues) with response cookie integration.</span></span>

### <a name="running-the-sample"></a><span data-ttu-id="3fcd5-118">サンプルの実行</span><span class="sxs-lookup"><span data-stu-id="3fcd5-118">Running the sample</span></span>

<span data-ttu-id="3fcd5-119">サンプルプロジェクトを実行する場合は、最初のページにブラウザーデバッガーを読み込み、それを使用してサイトの cookie のコレクションを表示します。</span><span class="sxs-lookup"><span data-stu-id="3fcd5-119">If you run the sample project  load your browser debugger on the initial page and use it to view the cookie collection for the site.</span></span>
<span data-ttu-id="3fcd5-120">これを行うには、Edge と Chrome で `F12`、[`Application`] タブを選択し、[`Storage`] セクションの [`Cookies`] オプションでサイトの URL をクリックします。</span><span class="sxs-lookup"><span data-stu-id="3fcd5-120">To do so in Edge and Chrome press `F12` then select the `Application` tab and click the site URL under the `Cookies` option in the `Storage` section.</span></span>

![ブラウザーデバッガーの Cookie の一覧](sample/img/BrowserDebugger.png)

<span data-ttu-id="3fcd5-122">上の図から、[Cookie の作成] ボタンをクリックしたときにサンプルによって作成されたクッキーが、[サンプルコード](#sampleCode)で設定した値と一致する `Lax`の SameSite 属性値を持つことがわかります。</span><span class="sxs-lookup"><span data-stu-id="3fcd5-122">You can see from the image above that the cookie created by the sample when you click the "Create Cookies" button has a SameSite attribute value of `Lax`, matching the value set in the [sample code](#sampleCode).</span></span>

## <a name="interception"></a><span data-ttu-id="3fcd5-123">制御しない cookie を傍受する</span><span class="sxs-lookup"><span data-stu-id="3fcd5-123">Intercepting cookies you do not control</span></span>

<span data-ttu-id="3fcd5-124">.NET 4.5.2 では、ヘッダーの書き込みをインターセプトするための新しいイベント `Response.AddOnSendingHeaders`導入されました。</span><span class="sxs-lookup"><span data-stu-id="3fcd5-124">.NET 4.5.2 introduced a new event for intercepting the writing of headers, `Response.AddOnSendingHeaders`.</span></span> <span data-ttu-id="3fcd5-125">これは、クライアントコンピューターに返される前に cookie を傍受するために使用できます。</span><span class="sxs-lookup"><span data-stu-id="3fcd5-125">This can be used to intercept cookies before they are returned to the client machine.</span></span> <span data-ttu-id="3fcd5-126">このサンプルでは、新しい sameSite の変更がブラウザーでサポートされているかどうかを確認する静的メソッドにイベントを接続します。そうでない場合は、新しい `None` の値が設定されている場合に、属性を出力しないようにクッキーを変更します。</span><span class="sxs-lookup"><span data-stu-id="3fcd5-126">In the sample we wire up the event to a static method which checks whether the browser supports the new sameSite changes, and if not, changes the cookies to not emit the attribute if the new `None` value has been set.</span></span>

<span data-ttu-id="3fcd5-127">イベントを処理する例と、[独自のコード](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472CSharpMVC5/SameSiteCookieRewriter.cs)にコピーできる cookie `sameSite` 属性を調整する例については、「 [global.asax](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472CSharpMVC5/Global.asax.cs) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="3fcd5-127">See [global.asax](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472CSharpMVC5/Global.asax.cs) for an example of hooking up the event and [SameSiteCookieRewriter.cs](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472CSharpMVC5/SameSiteCookieRewriter.cs) for an example of handling the event and adjusting the cookie `sameSite` attribute which you can copy into your own code.</span></span>

```c#
public static void FilterSameSiteNoneForIncompatibleUserAgents(object sender)
{
    HttpApplication application = sender as HttpApplication;
    if (application != null)
    {
        var userAgent = application.Context.Request.UserAgent;
        if (SameSite.BrowserDetection.DisallowsSameSiteNone(userAgent))
        {
            HttpContext.Current.Response.AddOnSendingHeaders(context =>
            {
                var cookies = context.Response.Cookies;
                for (var i = 0; i < cookies.Count; i++)
                {
                    var cookie = cookies[i];
                    if (cookie.SameSite == SameSiteMode.None)
                    {
                        cookie.SameSite = (SameSiteMode)(-1); // Unspecified
                    }
                }
            });
        }
    }
}
```

<span data-ttu-id="3fcd5-128">特定の名前付き cookie の動作は、ほぼ同じように変更できます。次のサンプルでは、`Lax` の既定の認証 cookie を、`None` 値をサポートするブラウザーで `None` に調整するか、`None`をサポートしていないブラウザーで sameSite 属性を削除します。</span><span class="sxs-lookup"><span data-stu-id="3fcd5-128">You can change specific named cookie behavior in much the same way; the sample below adjust the default authentication cookie from `Lax` to `None` on browsers which support the `None` value, or removes the sameSite attribute on browsers which do not support `None`.</span></span>

```c#
public static void AdjustSpecificCookieSettings()
{
    HttpContext.Current.Response.AddOnSendingHeaders(context =>
    {
        var cookies = context.Response.Cookies;
        for (var i = 0; i < cookies.Count; i++)
        {
            var cookie = cookies[i]; 
            // Forms auth: ".ASPXAUTH"
            // Session: "ASP.NET_SessionId"
            if (string.Equals(".ASPXAUTH", cookie.Name, StringComparison.Ordinal))
            { 
                if (SameSite.BrowserDetection.DisallowsSameSiteNone(userAgent))
                {
                    cookie.SameSite = -1;
                }
                else
                {
                    cookie.SameSite = SameSiteMode.None;
                }
                cookie.Secure = true;
            }
        }
    });
}
```

### <a name="more-information"></a><span data-ttu-id="3fcd5-129">詳細</span><span class="sxs-lookup"><span data-stu-id="3fcd5-129">More Information</span></span>
 
[<span data-ttu-id="3fcd5-130">Chrome の更新</span><span class="sxs-lookup"><span data-stu-id="3fcd5-130">Chrome Updates</span></span>](https://www.chromium.org/updates/same-site)

[<span data-ttu-id="3fcd5-131">OWIN SameSite のドキュメント</span><span class="sxs-lookup"><span data-stu-id="3fcd5-131">OWIN SameSite Documentation</span></span>](/aspnet/samesite/owin-samesite)

[<span data-ttu-id="3fcd5-132">ASP.NET のドキュメント</span><span class="sxs-lookup"><span data-stu-id="3fcd5-132">ASP.NET Documentation</span></span>](/aspnet/samesite/system-web-samesite)

[<span data-ttu-id="3fcd5-133">.NET SameSite パッチ</span><span class="sxs-lookup"><span data-stu-id="3fcd5-133">.NET SameSite Patches</span></span>](/aspnet/samesite/kbs-samesite)