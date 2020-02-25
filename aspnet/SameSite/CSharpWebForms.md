---
title: ASP.NET 4.7.2 C# WebForms の SameSite cookie サンプル
author: blowdart
description: ASP.NET 4.7.2 C# WebForms の SameSite cookie サンプル
ms.author: riande
ms.date: 2/15/2019
uid: samesite/CSharpWebForms
ms.openlocfilehash: 50d4745eca5954275abaa59dab726e7cf7ea193f
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2020
ms.locfileid: "77458421"
---
# <a name="samesite-cookie-sample-for-aspnet-472-c-webforms"></a>ASP.NET 4.7.2 C# WebForms の SameSite cookie サンプル

.NET Framework 4.7 には[SameSite](https://www.owasp.org/index.php/SameSite)属性のサポートが組み込まれていますが、元の標準に準拠しています。
パッチを適用した動作により、`SameSite.None` の意味が変更され、値がまったく出力されるのではなく、`None`の値を持つ属性が出力されます。 値を出力しない場合は、cookie の `SameSite` プロパティを-1 に設定します。

## <a name="sampleCode"></a>SameSite 属性の書き込み

SameSite 属性をクッキーに書き込む方法の例を次に示します。

```c#
// Create the cookie
HttpCookie sameSiteCookie = new HttpCookie("SameSiteSample");

// Set a value for the cookie
sameSiteCookie.Value = "sample";

// Set the secure flag, which Chrome's changes will require for SameSite none.
// Note this will also require you to be running on HTTPS
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

フォーム認証クッキーの既定の sameSite 属性は、のフォーム認証設定の `cookieSameSite` パラメーターで設定され `web.config` 

```xml
<system.web>
  <authentication mode="Forms">
    <forms name=".ASPXAUTH" loginUrl="~/" cookieSameSite="None" requireSSL="true">
    </forms>
  </authentication>
</system.web>
```

セッション状態の既定の sameSite 属性は、のセッション設定の ' cookieSameSite ' パラメーターでも設定され `web.config`

```xml
<system.web>
  <sessionState cookieSameSite="None">     
  </sessionState>
</system.web>
```

2019年11月の.NETへの更新により、最も互換性のある設定であるフォーム認証とセッションのデフォルト設定が `lax` に変更されましたが、ページをiframeに埋め込む場合、この設定を[なし]に戻し、`none`を追加する必要があります *ブラウザの機能に応じて[動作を調整するインターセプト](#interception)以下のコード。

### <a name="running-the-sample"></a>サンプルの実行

サンプルプロジェクトを実行する場合は、最初のページにブラウザーデバッガーを読み込み、それを使用してサイトの cookie のコレクションを表示します。
これを行うには、Edge と Chrome で `F12`、[`Application`] タブを選択し、[`Storage`] セクションの [`Cookies`] オプションでサイトの URL をクリックします。

![ブラウザーデバッガーの Cookie の一覧](sample/img/BrowserDebugger.png)

上の図から、[Cookie の作成] ボタンをクリックしたときにサンプルによって作成されたクッキーが、[サンプルコード](#sampleCode)で設定した値と一致する `Lax`の SameSite 属性値を持つことがわかります。

## <a name="interception"></a>制御しない cookie を傍受する

.NET 4.5.2 では、ヘッダーの書き込みをインターセプトするための新しいイベント `Response.AddOnSendingHeaders`導入されました。 これは、クライアントコンピューターに返される前に cookie を傍受するために使用できます。 このサンプルでは、新しい sameSite の変更がブラウザーでサポートされているかどうかを確認する静的メソッドにイベントを接続します。そうでない場合は、新しい `None` の値が設定されている場合に、属性を出力しないようにクッキーを変更します。

イベントを処理し、cookie `sameSite` 属性を調整する[例につい](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472CSharpWebForms/SameSiteCookieRewriter.cs)ては、「 [global.asax](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472CSharpWebForms/Global.asax.cs) 」を参照してください。

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

## <a name="more-information"></a>詳細情報

[Chrome の更新](https://www.chromium.org/updates/same-site)

[ASP.NET のドキュメント](/aspnet/samesite/system-web-samesite)

[.NET SameSite パッチ](/aspnet/samesite/kbs-samesite)