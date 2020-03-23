---
title: ASP.NET 4.7.2 VB WebForms の SameSite cookie サンプル
author: blowdart
description: ASP.NET 4.7.2 VB WebForms の SameSite cookie サンプル
ms.author: riande
ms.date: 2/15/2019
uid: samesite/vbWF
ms.openlocfilehash: 8979edecc5acf7dac81b9f53d31af00389f4727c
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2020
ms.locfileid: "77458385"
---
# <a name="samesite-cookie-sample-for-aspnet-472-vb-webforms"></a><span data-ttu-id="14c71-103">ASP.NET 4.7.2 VB WebForms の SameSite cookie サンプル</span><span class="sxs-lookup"><span data-stu-id="14c71-103">SameSite cookie sample for ASP.NET 4.7.2 VB WebForms</span></span>
<span data-ttu-id="14c71-104">.NET Framework 4.7 には[SameSite](https://www.owasp.org/index.php/SameSite)属性のサポートが組み込まれていますが、元の標準に準拠しています。</span><span class="sxs-lookup"><span data-stu-id="14c71-104">.NET Framework 4.7 has built-in support for the [SameSite](https://www.owasp.org/index.php/SameSite) attribute, but it adheres to the original standard.</span></span>
<span data-ttu-id="14c71-105">パッチを適用した動作により、`SameSite.None` の意味が変更され、値がまったく出力されるのではなく、`None`の値を持つ属性が出力されます。</span><span class="sxs-lookup"><span data-stu-id="14c71-105">The patched behavior changed the meaning of `SameSite.None` to emit the attribute with a value of `None`, rather than not emit the value at all.</span></span> <span data-ttu-id="14c71-106">値を出力しない場合は、cookie の `SameSite` プロパティを-1 に設定します。</span><span class="sxs-lookup"><span data-stu-id="14c71-106">If you want to not emit the value you can set the `SameSite` property on a cookie to -1.</span></span>

## <a name="writing-the-samesite-attribute"></a><a name="sampleCode"></a><span data-ttu-id="14c71-107">SameSite 属性の書き込み</span><span class="sxs-lookup"><span data-stu-id="14c71-107">Writing the SameSite attribute</span></span>

<span data-ttu-id="14c71-108">SameSite 属性をクッキーに書き込む方法の例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="14c71-108">Following is an example of how to write a SameSite attribute on a cookie;</span></span>

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

<span data-ttu-id="14c71-109">フォーム認証クッキーの既定の sameSite 属性は、のフォーム認証設定の `cookieSameSite` パラメーターで設定され `web.config`</span><span class="sxs-lookup"><span data-stu-id="14c71-109">The default sameSite attribute for a forms authentication cookie is set in the `cookieSameSite` parameter of the forms authentication settings in `web.config`</span></span> 

```xml
<system.web>
  <authentication mode="Forms">
    <forms name=".ASPXAUTH" loginUrl="~/" cookieSameSite="None" requireSSL="true">
    </forms>
  </authentication>
</system.web>
```

<span data-ttu-id="14c71-110">セッション状態の既定の sameSite 属性は、のセッション設定の ' cookieSameSite ' パラメーターでも設定され `web.config`</span><span class="sxs-lookup"><span data-stu-id="14c71-110">The default sameSite attribute for session state is also set in the 'cookieSameSite' parameter of the session settings in `web.config`</span></span>

```xml
<system.web>
  <sessionState cookieSameSite="None">     
  </sessionState>
</system.web>
```

<span data-ttu-id="14c71-111">2019年11月の.NETへの更新により、最も互換性のある設定であるフォーム認証とセッションのデフォルト設定が `lax` に変更されましたが、ページをiframeに埋め込む場合、この設定を[なし]に戻し、`none`を追加する必要があります \*ブラウザの機能に応じて[動作を調整するインターセプト](#interception)以下のコード。</span><span class="sxs-lookup"><span data-stu-id="14c71-111">The November 2019 update to .NET changed the default settings for Forms Authentication and Session to `lax` as is the most compatible setting, however if you embed pages into iframes you may need to revert this setting to None, and then add the [interception](#interception) code shown below to adjust the `none` behavior depending on browser capability.</span></span>

### <a name="running-the-sample"></a><span data-ttu-id="14c71-112">サンプルの実行</span><span class="sxs-lookup"><span data-stu-id="14c71-112">Running the sample</span></span>

<span data-ttu-id="14c71-113">サンプルプロジェクトを実行する場合は、最初のページにブラウザーデバッガーを読み込み、それを使用してサイトの cookie のコレクションを表示します。</span><span class="sxs-lookup"><span data-stu-id="14c71-113">If you run the sample project  load your browser debugger on the initial page and use it to view the cookie collection for the site.</span></span>
<span data-ttu-id="14c71-114">これを行うには、Microsoft Edge と Chrome で `F12`、[`Application`] タブを選択し、[`Storage`] セクションの [`Cookies`] オプションでサイトの URL をクリックします。</span><span class="sxs-lookup"><span data-stu-id="14c71-114">To do so in Edge and Chrome press `F12` then select the `Application` tab and click the site URL under the `Cookies` option in the `Storage` section.</span></span>

![ブラウザーデバッガーの Cookie の一覧](sample/img/BrowserDebugger.png)

<span data-ttu-id="14c71-116">上の図から、[Cookie の作成] ボタンをクリックしたときにサンプルによって作成されたクッキーが、[サンプルコード](#sampleCode)で設定した値と一致する `Lax`の SameSite 属性値を持つことがわかります。</span><span class="sxs-lookup"><span data-stu-id="14c71-116">You can see from the image above that the cookie created by the sample when you click the "Create Cookies" button has a SameSite attribute value of `Lax`, matching the value set in the [sample code](#sampleCode).</span></span>

## <a name="intercepting-cookies-you-do-not-control"></a><a name="interception"></a><span data-ttu-id="14c71-117">制御しない cookie を傍受する</span><span class="sxs-lookup"><span data-stu-id="14c71-117">Intercepting cookies you do not control</span></span>

<span data-ttu-id="14c71-118">.NET 4.5.2 では、ヘッダーの書き込みをインターセプトするための新しいイベント `Response.AddOnSendingHeaders`導入されました。</span><span class="sxs-lookup"><span data-stu-id="14c71-118">.NET 4.5.2 introduced a new event for intercepting the writing of headers, `Response.AddOnSendingHeaders`.</span></span> <span data-ttu-id="14c71-119">これは、クライアントコンピューターに返される前に cookie を傍受するために使用できます。</span><span class="sxs-lookup"><span data-stu-id="14c71-119">This can be used to intercept cookies before they are returned to the client machine.</span></span> <span data-ttu-id="14c71-120">このサンプルでは、新しい sameSite の変更がブラウザーでサポートされているかどうかを確認する静的メソッドにイベントを接続します。そうでない場合は、新しい `None` の値が設定されている場合に、属性を出力しないようにクッキーを変更します。</span><span class="sxs-lookup"><span data-stu-id="14c71-120">In the sample we wire up the event to a static method which checks whether the browser supports the new sameSite changes, and if not, changes the cookies to not emit the attribute if the new `None` value has been set.</span></span>

<span data-ttu-id="14c71-121">イベントを処理し、cookie `sameSite` 属性を調整する[例につい](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472VisualBasicWebForms/SameSiteCookieRewriter.vb)ては、「 [global.asax](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472VisualBasicWebForms/Global.asax.vb) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="14c71-121">See [global.asax](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472VisualBasicWebForms/Global.asax.vb) for an example of hooking up the event and [SameSiteCookieRewriter.cs](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472VisualBasicWebForms/SameSiteCookieRewriter.vb) for an example of handling the event and adjusting the cookie `sameSite` attribute.</span></span>


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

<span data-ttu-id="14c71-122">特定の名前付き cookie の動作は、ほぼ同じように変更できます。次のサンプルでは、`Lax` の既定の認証 cookie を、`None` 値をサポートするブラウザーで `None` に調整するか、`None`をサポートしていないブラウザーで sameSite 属性を削除します。</span><span class="sxs-lookup"><span data-stu-id="14c71-122">You can change specific named cookie behavior in much the same way; the sample below adjust the default authentication cookie from `Lax` to `None` on browsers which support the `None` value, or removes the sameSite attribute on browsers which do not support `None`.</span></span>

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

## <a name="more-information"></a><span data-ttu-id="14c71-123">詳細情報</span><span class="sxs-lookup"><span data-stu-id="14c71-123">More Information</span></span>

[<span data-ttu-id="14c71-124">Chrome の更新</span><span class="sxs-lookup"><span data-stu-id="14c71-124">Chrome Updates</span></span>](https://www.chromium.org/updates/same-site)

[<span data-ttu-id="14c71-125">ASP.NET のドキュメント</span><span class="sxs-lookup"><span data-stu-id="14c71-125">ASP.NET Documentation</span></span>](/aspnet/samesite/system-web-samesite)

[<span data-ttu-id="14c71-126">.NET SameSite パッチ</span><span class="sxs-lookup"><span data-stu-id="14c71-126">.NET SameSite Patches</span></span>](/aspnet/samesite/kbs-samesite)