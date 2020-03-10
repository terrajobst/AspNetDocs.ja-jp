---
title: ASP.NET 4.7.2 C# MVC の SameSite cookie サンプル
author: blowdart
description: ASP.NET 4.7.2 C# MVC の SameSite cookie サンプル
ms.author: riande
ms.date: 2/15/2019
uid: samesite/csMVC
ms.openlocfilehash: dcbd0bee009669fb747d74e6ccef07fbae70a236
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78438202"
---
# <a name="samesite-cookie-sample-for-aspnet-472-c-mvc"></a>ASP.NET 4.7.2 C# MVC の SameSite cookie サンプル

.NET Framework 4.7 には[SameSite](https://www.owasp.org/index.php/SameSite)属性のサポートが組み込まれていますが、元の標準に準拠しています。
パッチを適用した動作により、`SameSite.None` の意味が変更され、値がまったく出力されるのではなく、`None`の値を持つ属性が出力されます。 値を出力しない場合は、cookie の `SameSite` プロパティを-1 に設定します。

## <a name="sampleCode"></a>SameSite 属性の書き込み

SameSite 属性をクッキーに書き込む方法の例を次に示します。

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

セッション状態の既定の sameSite 属性は、のセッション設定の ' cookieSameSite ' パラメーターで設定され `web.config`

```xml
<system.web>
  <sessionState cookieSameSite="None">     
  </sessionState>
</system.web>
```

## <a name="mvc-authentication"></a>MVC 認証

OWIN MVC cookie ベースの認証では、cookie マネージャーを使用して cookie 属性の変更を有効にします。 [SameSiteCookieManager.cs](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472CSharpMVC5/SameSiteCookieManager.cs)は、このようなクラスの実装であり、独自のプロジェクトにコピーできます。 

Owin コンポーネントがすべてバージョン4.1.0 以上にアップグレードされていることを確認する必要があります。 `packages.config` ファイルをチェックして、すべてのバージョン番号が一致していることを確認します。たとえば、のようになります。

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

次に、スタートアップクラスで CookieManager を使用するように認証コンポーネントを構成する必要があります。

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

クッキーマネージャーは、それをサポートする*各*コンポーネントに設定する必要があります。これには、cookieauthentication と OpenIdConnectAuthentication が含まれます。

SystemWebCookieManager は、応答クッキーの統合に[関する既知の問題](https://github.com/aspnet/AspNetKatana/wiki/System.Web-response-cookie-integration-issues)を回避するために使用されます。

### <a name="running-the-sample"></a>サンプルの実行

サンプルプロジェクトを実行する場合は、最初のページにブラウザーデバッガーを読み込み、それを使用してサイトの cookie のコレクションを表示します。
これを行うには、Edge と Chrome で `F12`、[`Application`] タブを選択し、[`Storage`] セクションの [`Cookies`] オプションでサイトの URL をクリックします。

![ブラウザーデバッガーの Cookie の一覧](sample/img/BrowserDebugger.png)

上の図から、[Cookie の作成] ボタンをクリックしたときにサンプルによって作成されたクッキーが、[サンプルコード](#sampleCode)で設定した値と一致する `Lax`の SameSite 属性値を持つことがわかります。

## <a name="interception"></a>制御しない cookie を傍受する

.NET 4.5.2 では、ヘッダーの書き込みをインターセプトするための新しいイベント `Response.AddOnSendingHeaders`導入されました。 これは、クライアントコンピューターに返される前に cookie を傍受するために使用できます。 このサンプルでは、新しい sameSite の変更がブラウザーでサポートされているかどうかを確認する静的メソッドにイベントを接続します。そうでない場合は、新しい `None` の値が設定されている場合に、属性を出力しないようにクッキーを変更します。

イベントを処理する例と、[独自のコード](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472CSharpMVC5/SameSiteCookieRewriter.cs)にコピーできる cookie `sameSite` 属性を調整する例については、「 [global.asax](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472CSharpMVC5/Global.asax.cs) 」を参照してください。

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

特定の名前付き cookie の動作は、ほぼ同じように変更できます。次のサンプルでは、`Lax` の既定の認証 cookie を、`None` 値をサポートするブラウザーで `None` に調整するか、`None`をサポートしていないブラウザーで sameSite 属性を削除します。

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

### <a name="more-information"></a>詳細情報
 
[Chrome の更新](https://www.chromium.org/updates/same-site)

[OWIN SameSite のドキュメント](/aspnet/samesite/owin-samesite)

[ASP.NET のドキュメント](/aspnet/samesite/system-web-samesite)

[.NET SameSite パッチ](/aspnet/samesite/kbs-samesite)