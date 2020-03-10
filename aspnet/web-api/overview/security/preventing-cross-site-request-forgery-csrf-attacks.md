---
uid: web-api/overview/security/preventing-cross-site-request-forgery-csrf-attacks
title: ASP.NET MVC でのクロスサイト要求偽造 (CSRF) 攻撃の防止
author: MikeWasson
description: クロスサイト要求偽造 (CSRF) 攻撃と、ASP.NET Web MVC で CSRF メジャーを実装する方法について説明します。
ms.author: riande
ms.date: 12/12/2012
ms.assetid: 81d46f14-8f48-4d8c-830d-cc8d594dc11b
msc.legacyurl: /web-api/overview/security/preventing-cross-site-request-forgery-csrf-attacks
msc.type: authoredcontent
ms.openlocfilehash: 5fb0f8bcc9e587ba4fbbf2b857d3bf7adcaafb94
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78447112"
---
# <a name="preventing-cross-site-request-forgery-csrf-attacks-in-aspnet-mvc-application"></a>ASP.NET MVC アプリケーションでのクロスサイト要求偽造 (CSRF) 攻撃の防止

[Mike Wasson](https://github.com/MikeWasson)

クロスサイト要求偽造 (CSRF) は、悪意のあるサイトが、ユーザーが現在ログインしている脆弱なサイトに要求を送信する攻撃です。

CSRF 攻撃の例を次に示します。

1. ユーザーは、フォーム認証を使用して `www.example.com` にログインします。
2. サーバーは、ユーザーを認証します。 サーバーからの応答には、認証クッキーが含まれています。
3. ログオフしないと、ユーザーは悪意のある web サイトにアクセスします。 この悪意のあるサイトには、次の HTML フォームが含まれています。 

    [!code-html[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample1.html)]

    フォームアクションは、悪意のあるサイトではなく、脆弱なサイトに投稿されることに注意してください。 これは、CSRF の "cross-site" の一部です。
4. ユーザーが [送信] ボタンをクリックします。 ブラウザーには、要求と共に認証クッキーが含まれます。
5. 要求は、ユーザーの認証コンテキストを使用してサーバー上で実行され、認証されたユーザーが実行できるすべての操作を実行できます。

この例では、ユーザーがフォームボタンをクリックする必要がありますが、悪意のあるページでは、フォームを自動的に送信するスクリプトを簡単に実行できます。 また、悪意のあるサイトが "https://" 要求を送信できるため、SSL を使用しても CSRF 攻撃を防ぐことはできません。

通常、ブラウザーでは、関連するすべての cookie が送信先の web サイトに送信されるため、認証に cookie を使用する web サイトに対しては CSRF 攻撃を行うことができます。 ただし、CSRF 攻撃は cookie を利用することに限定されません。 例えば、ベーシック認証やダイジェスト認証も脆弱です。 ユーザーが基本認証またはダイジェスト認証を使用してログインした後。 ブラウザーは、セッションが終了するまで資格情報を自動的に送信します。

## <a name="anti-forgery-tokens"></a>偽造防止トークン

CSRF 攻撃を防ぐために、ASP.NET MVC では偽造防止トークンを使用します。これは、*要求検証トークン*とも呼ばれます。

1. クライアントは、フォームを含む HTML ページを要求します。
2. サーバーには、応答に2つのトークンが含まれています。 1つのトークンが cookie として送信されます。 もう一方は、非表示のフォームフィールドに配置されます。 トークンはランダムに生成されるため、敵対者は値を推測できません。
3. クライアントは、フォームを送信するときに、両方のトークンをサーバーに送り返す必要があります。 クライアントは cookie トークンをクッキーとして送信し、フォームデータ内にフォームトークンを送信します。 (ブラウザークライアントは、ユーザーがフォームを送信したときに自動的にこれを行います)。
4. 要求に両方のトークンが含まれていない場合、サーバーは要求を拒否します。

次に、非表示のフォームトークンを持つ HTML フォームの例を示します。

[!code-html[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample2.html)]

悪意のあるページでは、同じオリジンのポリシーによってユーザーのトークンを読み取ることができないため、偽造防止トークンが機能します。 ([同じオリジンポリシー](http://www.w3.org/Security/wiki/Same_Origin_Policy)を利用すると、2つの異なるサイトでホストされているドキュメントから互いのコンテンツにアクセスできなくなります。 このため、前の例では、悪意のあるページは example.com に要求を送信できますが、応答を読み取ることはできません)。

CSRF 攻撃を防ぐには、ユーザーがログインした後にブラウザーがサイレントモードで資格情報を送信する認証プロトコルで偽造防止トークンを使用します。 これには、フォーム認証などの cookie ベースの認証プロトコルや、基本認証やダイジェスト認証などのプロトコルが含まれます。

安全でないメソッド (POST、PUT、DELETE) では、偽造防止トークンが必要です。 また、安全なメソッド (GET、HEAD) に副作用がないことを確認してください。 さらに、CORS や JSONP などのドメイン間のサポートを有効にすると、GET などの安全なメソッドも CSRF 攻撃に対して脆弱になる可能性があるため、攻撃者は機密データを読み取ることができます。

## <a name="anti-forgery-tokens-in-aspnet-mvc"></a>ASP.NET MVC の偽造防止トークン

偽造防止トークンを Razor ページに追加するには、 **htmlhelper..........................** :

[!code-cshtml[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample3.cshtml)]

このメソッドは、隠しフォームフィールドを追加し、cookie トークンも設定します。

## <a name="anti-csrf-and-ajax"></a>CSRF と AJAX の防止

AJAX 要求は HTML フォーム データではなく JSON データを送信する場合があるため、フォーム トークンは AJAX 要求に対して問題である可能性があります。 1 つの解決策は、カスタム HTTP ヘッダーでトークンを送信することです。 次のコードでは、Razor 構文を使ってトークンを生成した後、AJAX 要求にトークンを追加しています。 トークンは、**偽造防止. GetTokens**を呼び出すことによって、サーバーで生成されます。

[!code-html[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample4.html)]

要求を処理するときは、要求ヘッダーからトークンを抽出します。 次に、**偽造**防止の validate メソッドを呼び出してトークンを検証します。 トークンが有効でない場合、 **Validate**メソッドは例外をスローします。

[!code-csharp[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample5.cs)]
