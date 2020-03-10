---
title: ASP.NET 4.7.2 VB MVC の SameSite cookie サンプル
author: blowdart
description: ASP.NET 4.7.2 VB MVC の SameSite cookie サンプル
ms.author: riande
ms.date: 2/15/2019
uid: samesite/vbMVC
ms.openlocfilehash: f6effce6075f94fb58ce10ec08bf010fab8b4b56
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78440848"
---
# <a name="samesite-cookie-sample-for-aspnet-472-vb-mvc"></a>ASP.NET 4.7.2 VB MVC の SameSite cookie サンプル

.NET Framework 4.7 には[SameSite](https://www.owasp.org/index.php/SameSite)属性のサポートが組み込まれていますが、元の標準に準拠しています。
パッチを適用した動作により、`SameSite.None` の意味が変更され、値がまったく出力されるのではなく、`None`の値を持つ属性が出力されます。 値を出力しない場合は、cookie の `SameSite` プロパティを-1 に設定します。

## <a name="sampleCode"></a>SameSite 属性の書き込み

SameSite 属性をクッキーに書き込む方法の例を次に示します。

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

セッション状態の既定の sameSite 属性は、のセッション設定の ' cookieSameSite ' パラメーターで設定され `web.config`

```xml
<system.web>
  <sessionState cookieSameSite="None">     
  </sessionState>
</system.web>
```

## <a name="mvc-authentication"></a>MVC 認証

OWIN MVC cookie ベースの認証では、cookie マネージャーを使用して cookie 属性の変更を有効にします。 [SameSiteCookieManager](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472VisualBasicMVC5/SameSiteCookieManager.vb)は、このようなクラスを実装したもので、独自のプロジェクトにコピーできます。 

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

認証コンポーネントは、スタートアップクラスで CookieManager を使用するように構成されている必要があります。

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

クッキーマネージャーは、それをサポートする*各*コンポーネントに設定する必要があります。これには、cookieauthentication と OpenIdConnectAuthentication が含まれます。

SystemWebCookieManager は、応答クッキーの統合に[関する既知の問題](https://github.com/aspnet/AspNetKatana/wiki/System.Web-response-cookie-integration-issues)を回避するために使用されます。

### <a name="running-the-sample"></a>サンプルの実行

サンプルプロジェクトを実行する場合は、最初のページにブラウザーデバッガーを読み込み、それを使用してサイトの cookie のコレクションを表示します。
これを行うには、Edge と Chrome で `F12`、[`Application`] タブを選択し、[`Storage`] セクションの [`Cookies`] オプションでサイトの URL をクリックします。

![ブラウザーデバッガーの Cookie の一覧](sample/img/BrowserDebugger.png)

上の図からわかるように、[Create SameSite Cookie] ボタンをクリックしたときにサンプルによって作成された cookie には、[サンプルコード](#sampleCode)で設定した値と一致する、SameSite 属性値 `Lax`があります。

## <a name="interception"></a>制御しない cookie を傍受する

.NET 4.5.2 では、ヘッダーの書き込みをインターセプトするための新しいイベント `Response.AddOnSendingHeaders`導入されました。 これは、クライアントコンピューターに返される前に cookie を傍受するために使用できます。 このサンプルでは、新しい sameSite の変更がブラウザーでサポートされているかどうかを確認する静的メソッドにイベントを接続します。そうでない場合は、新しい `None` の値が設定されている場合に、属性を出力しないようにクッキーを変更します。

イベントの処理や、独自のコードにコピーできる cookie `sameSite` 属性の調整の[例につい](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472VisualBasicMVC5/SameSiteCookieRewriter.vb)ては、global.asax の「 [global.asax](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472VisualBasicMVC5/Global.asax.vb) 」を参照してください。

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

特定の名前付き cookie の動作は、ほぼ同じように変更できます。次のサンプルでは、`Lax` の既定の認証 cookie を、`None` 値をサポートするブラウザーで `None` に調整するか、`None`をサポートしていないブラウザーで sameSite 属性を削除します。

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

## <a name="more-information"></a>詳細情報
 
[Chrome の更新](https://www.chromium.org/updates/same-site)

[OWIN SameSite のドキュメント](/aspnet/samesite/owin-samesite)

[ASP.NET のドキュメント](/aspnet/samesite/system-web-samesite)

[.NET SameSite パッチ](/aspnet/samesite/kbs-samesite)