---
title: ASP.NET 4.7.2 VB MVC の SameSite cookie サンプル
author: blowdart
description: ASP.NET 4.7.2 VB MVC の SameSite cookie サンプル
ms.author: riande
ms.date: 2/15/2019
uid: samesite/vbMVC
ms.openlocfilehash: f6effce6075f94fb58ce10ec08bf010fab8b4b56
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2020
ms.locfileid: "77458409"
---
# <a name="samesite-cookie-sample-for-aspnet-472-vb-mvc"></a><span data-ttu-id="f2776-103">ASP.NET 4.7.2 VB MVC の SameSite cookie サンプル</span><span class="sxs-lookup"><span data-stu-id="f2776-103">SameSite cookie sample for ASP.NET 4.7.2 VB MVC</span></span>

<span data-ttu-id="f2776-104">.NET Framework 4.7 には[SameSite](https://www.owasp.org/index.php/SameSite)属性のサポートが組み込まれていますが、元の標準に準拠しています。</span><span class="sxs-lookup"><span data-stu-id="f2776-104">.NET Framework 4.7 has built-in support for the [SameSite](https://www.owasp.org/index.php/SameSite) attribute, but it adheres to the original standard.</span></span>
<span data-ttu-id="f2776-105">パッチを適用した動作により、`SameSite.None` の意味が変更され、値がまったく出力されるのではなく、`None`の値を持つ属性が出力されます。</span><span class="sxs-lookup"><span data-stu-id="f2776-105">The patched behavior changed the meaning of `SameSite.None` to emit the attribute with a value of `None`, rather than not emit the value at all.</span></span> <span data-ttu-id="f2776-106">値を出力しない場合は、cookie の `SameSite` プロパティを-1 に設定します。</span><span class="sxs-lookup"><span data-stu-id="f2776-106">If you want to not emit the value you can set the `SameSite` property on a cookie to -1.</span></span>

## <a name="sampleCode"></a><span data-ttu-id="f2776-107">SameSite 属性の書き込み</span><span class="sxs-lookup"><span data-stu-id="f2776-107">Writing the SameSite attribute</span></span>

<span data-ttu-id="f2776-108">SameSite 属性をクッキーに書き込む方法の例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="f2776-108">Following is an example of how to write a SameSite attribute on a cookie;</span></span>

```vb
' Create the cookie
Dim sameSiteCookie As New HttpCookie("sameSiteSample")

' Set a value for the cookie
sameSiteCookie.Value = "sample"

' Set the secure flag, which Chrome's changes will require for SameSite none.
' Note this will also require you to be running on HTTPS
sameSiteCookie.Secure = True

' Set the cookie to HTTP only which is good practice unless you really do need
' to access it client side in scripts.
sameSiteCookie.HttpOnly = True

' Expire the cookie in 1 minute
sameSiteCookie.Expires = Date.Now.AddMinutes(1)

' Add the SameSite attribute, this will emit the attribute with a value of none.
' To Not emit the attribute at all set the SameSite property to -1.
sameSiteCookie.SameSite = SameSiteMode.None

' Add the cookie to the response cookie collection
Response.Cookies.Add(sameSiteCookie)
```

[!INCLUDE[](~/includes/MTcomments.md)]

<span data-ttu-id="f2776-109">セッション状態の既定の sameSite 属性は、のセッション設定の ' cookieSameSite ' パラメーターで設定され `web.config`</span><span class="sxs-lookup"><span data-stu-id="f2776-109">The default sameSite attribute for session state is set in the 'cookieSameSite' parameter of the session settings in `web.config`</span></span>

```xml
<system.web>
  <sessionState cookieSameSite="None">     
  </sessionState>
</system.web>
```

## <a name="mvc-authentication"></a><span data-ttu-id="f2776-110">MVC 認証</span><span class="sxs-lookup"><span data-stu-id="f2776-110">MVC Authentication</span></span>

<span data-ttu-id="f2776-111">OWIN MVC cookie ベースの認証では、cookie マネージャーを使用して cookie 属性の変更を有効にします。</span><span class="sxs-lookup"><span data-stu-id="f2776-111">OWIN MVC cookie based authentication uses a cookie manager to enable the changing of cookie attributes.</span></span> <span data-ttu-id="f2776-112">[SameSiteCookieManager](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472VisualBasicMVC5/SameSiteCookieManager.vb)は、このようなクラスを実装したもので、独自のプロジェクトにコピーできます。</span><span class="sxs-lookup"><span data-stu-id="f2776-112">The [SameSiteCookieManager.vb](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472VisualBasicMVC5/SameSiteCookieManager.vb) is an implementation of such a class which you can copy into your own projects.</span></span> 

<span data-ttu-id="f2776-113">Owin コンポーネントがすべてバージョン4.1.0 以上にアップグレードされていることを確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f2776-113">You must ensure your Microsoft.Owin components are all upgraded to version 4.1.0 or greater.</span></span> <span data-ttu-id="f2776-114">`packages.config` ファイルをチェックして、すべてのバージョン番号が一致していることを確認します。たとえば、のようになります。</span><span class="sxs-lookup"><span data-stu-id="f2776-114">Check your `packages.config` file to ensure all the version numbers match, for example.</span></span>

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

<span data-ttu-id="f2776-115">認証コンポーネントは、スタートアップクラスで CookieManager を使用するように構成されている必要があります。</span><span class="sxs-lookup"><span data-stu-id="f2776-115">The authentication components must be configured to use the CookieManager in your startup class;</span></span>

```vb
Public Sub Configuration(app As IAppBuilder)
    app.UseCookieAuthentication(New CookieAuthenticationOptions() With {
        .CookieSameSite = SameSiteMode.None,
        .CookieHttpOnly = True,
        .CookieSecure = CookieSecureOption.Always,
        .CookieManager = New SameSiteCookieManager(New SystemWebCookieManager())
    })
End Sub
```

<span data-ttu-id="f2776-116">クッキーマネージャーは、それをサポートする*各*コンポーネントに設定する必要があります。これには、cookieauthentication と OpenIdConnectAuthentication が含まれます。</span><span class="sxs-lookup"><span data-stu-id="f2776-116">A cookie manager must be set on *each* component that supports it, this includes CookieAuthentication and OpenIdConnectAuthentication.</span></span>

<span data-ttu-id="f2776-117">SystemWebCookieManager は、応答クッキーの統合に[関する既知の問題](https://github.com/aspnet/AspNetKatana/wiki/System.Web-response-cookie-integration-issues)を回避するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="f2776-117">The SystemWebCookieManager is used to avoid [known issues](https://github.com/aspnet/AspNetKatana/wiki/System.Web-response-cookie-integration-issues) with response cookie integration.</span></span>

### <a name="running-the-sample"></a><span data-ttu-id="f2776-118">サンプルの実行</span><span class="sxs-lookup"><span data-stu-id="f2776-118">Running the sample</span></span>

<span data-ttu-id="f2776-119">サンプルプロジェクトを実行する場合は、最初のページにブラウザーデバッガーを読み込み、それを使用してサイトの cookie のコレクションを表示します。</span><span class="sxs-lookup"><span data-stu-id="f2776-119">If you run the sample project please load your browser debugger on the initial page and use it to view the cookie collection for the site.</span></span>
<span data-ttu-id="f2776-120">これを行うには、Edge と Chrome で `F12`、[`Application`] タブを選択し、[`Storage`] セクションの [`Cookies`] オプションでサイトの URL をクリックします。</span><span class="sxs-lookup"><span data-stu-id="f2776-120">To do so in Edge and Chrome press `F12` then select the `Application` tab and click the site URL under the `Cookies` option in the `Storage` section.</span></span>

![ブラウザーデバッガーの Cookie の一覧](sample/img/BrowserDebugger.png)

<span data-ttu-id="f2776-122">上の図からわかるように、[Create SameSite Cookie] ボタンをクリックしたときにサンプルによって作成された cookie には、[サンプルコード](#sampleCode)で設定した値と一致する、SameSite 属性値 `Lax`があります。</span><span class="sxs-lookup"><span data-stu-id="f2776-122">You can see from the image above that the cookie created by the sample when you click the "Create SameSite Cookie" button has a SameSite attribute value of `Lax`, matching the value set in the [sample code](#sampleCode).</span></span>

## <a name="interception"></a><span data-ttu-id="f2776-123">制御しない cookie を傍受する</span><span class="sxs-lookup"><span data-stu-id="f2776-123">Intercepting cookies you do not control</span></span>

<span data-ttu-id="f2776-124">.NET 4.5.2 では、ヘッダーの書き込みをインターセプトするための新しいイベント `Response.AddOnSendingHeaders`導入されました。</span><span class="sxs-lookup"><span data-stu-id="f2776-124">.NET 4.5.2 introduced a new event for intercepting the writing of headers, `Response.AddOnSendingHeaders`.</span></span> <span data-ttu-id="f2776-125">これは、クライアントコンピューターに返される前に cookie を傍受するために使用できます。</span><span class="sxs-lookup"><span data-stu-id="f2776-125">This can be used to intercept cookies before they are returned to the client machine.</span></span> <span data-ttu-id="f2776-126">このサンプルでは、新しい sameSite の変更がブラウザーでサポートされているかどうかを確認する静的メソッドにイベントを接続します。そうでない場合は、新しい `None` の値が設定されている場合に、属性を出力しないようにクッキーを変更します。</span><span class="sxs-lookup"><span data-stu-id="f2776-126">In the sample we wire up the event to a static method which checks whether the browser supports the new sameSite changes, and if not, changes the cookies to not emit the attribute if the new `None` value has been set.</span></span>

<span data-ttu-id="f2776-127">イベントの処理や、独自のコードにコピーできる cookie `sameSite` 属性の調整の[例につい](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472VisualBasicMVC5/SameSiteCookieRewriter.vb)ては、global.asax の「 [global.asax](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472VisualBasicMVC5/Global.asax.vb) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f2776-127">See [global.asax](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472VisualBasicMVC5/Global.asax.vb) for an example of hooking up the event and [SameSiteCookieRewriter.vb](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472VisualBasicMVC5/SameSiteCookieRewriter.vb) for an example of handling the event and adjusting the cookie `sameSite` attribute which you can copy into your own code.</span></span>

```vb
Sub FilterSameSiteNoneForIncompatibleUserAgents(ByVal sender As Object)
    Dim application As HttpApplication = TryCast(sender, HttpApplication)

    If application IsNot Nothing Then
        Dim userAgent = application.Context.Request.UserAgent

        If SameSite.DisallowsSameSiteNone(userAgent) Then
            application.Response.AddOnSendingHeaders(
                Function(context)
                    Dim cookies = context.Response.Cookies

                    For i = 0 To cookies.Count - 1
                        Dim cookie = cookies(i)

                        If cookie.SameSite = SameSiteMode.None Then
                            cookie.SameSite = CType((-1), SameSiteMode)
                        End If
                    Next
                End Function)
        End If
    End If
End Sub
```

<span data-ttu-id="f2776-128">特定の名前付き cookie の動作は、ほぼ同じように変更できます。次のサンプルでは、`Lax` の既定の認証 cookie を、`None` 値をサポートするブラウザーで `None` に調整するか、`None`をサポートしていないブラウザーで sameSite 属性を削除します。</span><span class="sxs-lookup"><span data-stu-id="f2776-128">You can change specific named cookie behavior in much the same way; the sample below adjust the default authentication cookie from `Lax` to `None` on browsers which support the `None` value, or removes the sameSite attribute on browsers which do not support `None`.</span></span>

```vb
Public Shared Sub AdjustSpecificCookieSettings()
    HttpContext.Current.Response.AddOnSendingHeaders(Function(context)
            Dim cookies = context.Response.Cookies

            For i = 0 To cookies.Count - 1
            Dim cookie = cookies(i)

            If String.Equals(".ASPXAUTH", cookie.Name, StringComparison.Ordinal) Then

                If SameSite.BrowserDetection.DisallowsSameSiteNone(userAgent) Then
                    cookie.SameSite = -1
                Else
                    cookie.SameSite = SameSiteMode.None
                End If

                cookie.Secure = True
            End If
            Next
        End Function)
End Sub
```

## <a name="more-information"></a><span data-ttu-id="f2776-129">詳細</span><span class="sxs-lookup"><span data-stu-id="f2776-129">More Information</span></span>
 
[<span data-ttu-id="f2776-130">Chrome の更新</span><span class="sxs-lookup"><span data-stu-id="f2776-130">Chrome Updates</span></span>](https://www.chromium.org/updates/same-site)

[<span data-ttu-id="f2776-131">OWIN SameSite のドキュメント</span><span class="sxs-lookup"><span data-stu-id="f2776-131">OWIN SameSite Documentation</span></span>](/aspnet/samesite/owin-samesite)

[<span data-ttu-id="f2776-132">ASP.NET のドキュメント</span><span class="sxs-lookup"><span data-stu-id="f2776-132">ASP.NET Documentation</span></span>](/aspnet/samesite/system-web-samesite)

[<span data-ttu-id="f2776-133">.NET SameSite パッチ</span><span class="sxs-lookup"><span data-stu-id="f2776-133">.NET SameSite Patches</span></span>](/aspnet/samesite/kbs-samesite)