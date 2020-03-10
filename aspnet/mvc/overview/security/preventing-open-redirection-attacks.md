---
uid: mvc/overview/security/preventing-open-redirection-attacks
title: オープンリダイレクト攻撃の防止C#() |Microsoft Docs
author: jongalloway
description: このチュートリアルでは、ASP.NET MVC アプリケーションでのオープンリダイレクト攻撃を防ぐ方法について説明します。 このチュートリアルでは、加えられた変更について説明します。
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 69fb02e0-f5b7-4c35-878c-fa87164fc785
msc.legacyurl: /mvc/overview/security/preventing-open-redirection-attacks
msc.type: authoredcontent
ms.openlocfilehash: cfa635d4fd14d031993c5b452325cbe334f82dc2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78432586"
---
# <a name="preventing-open-redirection-attacks-c"></a>オープン リダイレクト攻撃の防止 (C#)

( [Jon Galloway](https://github.com/jongalloway) )

> このチュートリアルでは、ASP.NET MVC アプリケーションでのオープンリダイレクト攻撃を防ぐ方法について説明します。 このチュートリアルでは、ASP.NET MVC 3 で AccountController に加えられた変更について説明し、既存の ASP.NET MVC 1.0 および2アプリケーションでこれらの変更を適用する方法を示します。

## <a name="what-is-an-open-redirection-attack"></a>オープンリダイレクト攻撃とは何ですか。

クエリ文字列やフォームデータなど、要求によって指定された URL にリダイレクトされる web アプリケーションは、外部の悪意のある URL にユーザーをリダイレクトするために改ざんされる可能性があります。 この改ざんは、オープンリダイレクト攻撃と呼ばれます。

アプリケーションロジックが指定した URL にリダイレクトする度に、リダイレクト URL が改ざんされていないことを確認する必要があります。 ASP.NET MVC 1.0 と ASP.NET MVC 2 の両方の既定の AccountController で使用されるログインは、オープンリダイレクト攻撃に対して脆弱です。 幸い、ASP.NET MVC 3 Preview の修正プログラムを使用するには、既存のアプリケーションを簡単に更新できます。

脆弱性を理解するために、既定の ASP.NET MVC 2 Web アプリケーションプロジェクトでログインリダイレクトがどのように機能するかを見てみましょう。 このアプリケーションでは、[承認] 属性を持つコントローラーアクションにアクセスしようとすると、承認されていないユーザーがアカウント/ログオンビューにリダイレクトされます。 /Accountにリダイレクトすると、returnUrl querystring パラメーターが追加されます。これにより、ユーザーは、最初に要求された URL にログインした後に返されるようになります。

次のスクリーンショットでは、ログインしていないときに/accountview にアクセスしようとすると、/アカウント/ログオンにリダイレクトされることがわかります。ReturnUrl =% 2fAccount% 2fChangePassword% 2f

[![](preventing-open-redirection-attacks/_static/image2.png)](preventing-open-redirection-attacks/_static/image1.png)

**図 01**: 開いているリダイレクトがあるログインページ

ReturnUrl querystring パラメーターは検証されないため、攻撃者はこれを変更して、URL アドレスをパラメーターに挿入して、オープンなリダイレクト攻撃を行うことができます。 このデモを実行するには、ReturnUrl パラメーターを[http://bing.com](http://bing.com)に変更します。その結果、ログイン URL は/アカウント/ログオンになりますか。ReturnUrl =<http://www.bing.com/>。 サイトへのログインに成功すると、 [http://bing.com](http://bing.com)にリダイレクトされます。 このリダイレクトは検証されていないため、ユーザーをトリックしようとする悪意のあるサイトを指している可能性があります。

### <a name="a-more-complex-open-redirection-attack"></a>より複雑なオープンリダイレクト攻撃

オープンリダイレクト攻撃は特に危険です。攻撃者は、特定の web サイトにログインしようとしていることを認識しているため、[フィッシング攻撃](https://www.microsoft.com/protect/fraud/phishing/symptoms.aspx)に対して脆弱になります。 たとえば、攻撃者は、パスワードをキャプチャしようとして、web サイトのユーザーに悪意のある電子メールを送信することができます。 では、これがどのように機能するかを見てみましょう。 (Live のリダイレクト攻撃から保護するために、ライブサイトが更新されていることに注意してください)。

まず、攻撃者は、偽造されたページへのリダイレクトを含む、ユーザーのログインページへのリンクを送信します。

[http://nerddinner.com/Account/LogOn?returnUrl=http://nerddiner.com/Account/LogOn](http://nerddinner.com/Account/LogOn?returnUrl=http://nerddiner.com/Account/LogOn)

戻り先 URL が nerddiner.com を指していることに注意してください。これには、ディナーの "n" がありません。 この例では、これは攻撃者が制御するドメインです。 上記のリンクにアクセスすると、正当な NerdDinner.com ログインページが表示されます。

[![](preventing-open-redirection-attacks/_static/image4.png)](preventing-open-redirection-attacks/_static/image3.png)

**図 02**: 開いているリダイレクトを使用した管理ログインページ

正常にログインすると、ASP.NET MVC AccountController のログオンアクションによって、returnUrl querystring パラメーターで指定された URL にリダイレクトされます。 この場合、攻撃者が入力した URL が[http://nerddiner.com/Account/LogOn](http://nerddiner.com/Account/LogOn)ます。 非常に配るでない限り、特に、攻撃者が偽造されたページが正当なログインページとまったく同じように見えるようにするために、これに気付くことはほとんどありません。 このログインページには、もう一度ログインを要求するエラーメッセージが含まれています。 いくぶん us では、パスワードの入力ミスが必要です。

[![](preventing-open-redirection-attacks/_static/image6.png)](preventing-open-redirection-attacks/_static/image5.png)

**図 03**: 偽造したログイン画面

ユーザー名とパスワードを再入力すると、偽造ログインページに情報が保存され、正当な NerdDinner.com サイトに返送されます。 この時点で、NerdDinner.com サイトは既に認証されているので、偽造ログインページはそのページに直接リダイレクトできます。 最終的には、攻撃者がユーザー名とパスワードを持っていることがわかります。これは、攻撃者に提供されたことを認識していません。

## <a name="looking-at-the-vulnerable-code-in-the-accountcontroller-logon-action"></a>AccountController ログオンアクションの脆弱性のあるコードを見る

ASP.NET MVC 2 アプリケーションのログオンアクションのコードを次に示します。 ログインが成功すると、コントローラーから returnUrl へのリダイレクトが返されることに注意してください。 ReturnUrl パラメーターに対して検証が実行されていないことがわかります。

**リスト1– `AccountController.cs` での ASP.NET MVC 2 ログオンアクション**

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample1.cs)]

次に、ASP.NET MVC 3 ログオンアクションの変更について説明します。 このコードは、`IsLocalUrl()`という名前の returnUrl ヘルパークラスで新しいメソッドを呼び出すことによって、パラメーターが検証されるように変更されています。

**リスト2– `AccountController.cs` での ASP.NET MVC 3 ログオンアクション**

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample2.cs)]

これは、`IsLocalUrl()`の新しいメソッドを呼び出すことによって、戻り先 URL パラメーターを検証するように変更されています。

## <a name="protecting-your-aspnet-mvc-10-and-mvc-2-applications"></a>ASP.NET MVC 1.0 アプリケーションと MVC 2 アプリケーションの保護

IsLocalUrl () ヘルパーメソッドを追加し、ログオンアクションを更新して returnUrl パラメーターを検証することで、既存の ASP.NET MVC 1.0 および2アプリケーションの ASP.NET MVC 3 の変更を利用できます。

UrlHelper IsLocalUrl () メソッドは、実際には、ASP.NET Web ページアプリケーションでも使用されるため、実際には System.web. Web ページのメソッドを呼び出すだけです。

**リスティング3– ASP.NET MVC 3 UrlHelper の IsLocalUrl () メソッド `class`**

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample3.cs)]

IsUrlLocalToHost メソッドには、リスト4に示すように、実際の検証ロジックが含まれています。

**System.web. Web ページの RequestExtensions クラスからのリスト4– IsUrlLocalToHost () メソッド**

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample4.cs)]

ASP.NET MVC 1.0 または2アプリケーションでは、AccountController に IsLocalUrl () メソッドを追加しますが、可能であれば、別のヘルパークラスに追加することをお勧めします。 ASP.NET MVC 3 バージョンの IsLocalUrl () に2つの小さな変更を加えて、AccountController 内で動作するようにします。 まず、コントローラーのパブリックメソッドにコントローラーアクションとしてアクセスできるため、パブリックメソッドからプライベートメソッドに変更します。 次に、アプリケーションホストに対して URL ホストを確認する呼び出しを変更します。 この呼び出しによって、UrlHelper クラスのローカルの RequestContext フィールドが使用されます。 これを使用する代わりに。次のように、このを使用します。要求. Url. Host. 次のコードは、ASP.NET MVC 1.0 と2つのアプリケーションのコントローラークラスで使用する、変更された IsLocalUrl () メソッドを示しています。

**リスト5– IsLocalUrl () メソッド。 MVC コントローラークラスで使用するように変更されています。**

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample5.cs)]

IsLocalUrl () メソッドが配置されたので、次のコードに示すように、ログオンアクションから呼び出して returnUrl パラメーターを検証することができます。

**リスト6– returnUrl パラメーターを検証する更新されたログオン方法**

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample6.cs)]

これで、外部のリターン URL を使用してログインしようとすることで、オープンリダイレクト攻撃をテストできます。 アカウント/ログオンを使用してみましょう。ReturnUrl =<http://www.bing.com/> 再実行します。

[![](preventing-open-redirection-attacks/_static/image8.png)](preventing-open-redirection-attacks/_static/image7.png)

**図 04**: 更新されたログオンアクションのテスト

ログインに成功すると、外部 URL ではなく、Home/Index Controller アクションにリダイレクトされます。

[![](preventing-open-redirection-attacks/_static/image10.png)](preventing-open-redirection-attacks/_static/image9.png)

**図 05**: オープンリダイレクト攻撃の敗北

## <a name="summary"></a>まとめ

オープンリダイレクト攻撃は、リダイレクト Url がアプリケーションの URL でパラメーターとして渡されたときに発生する可能性があります。 ASP.NET MVC 3 テンプレートには、オープンリダイレクト攻撃から保護するためのコードが含まれています。 このコードは、ASP.NET MVC 1.0 と2つのアプリケーションにいくつかの変更を加えることによって追加できます。 ASP.NET 1.0 と2つのアプリケーションにログインするときに、オープンリダイレクト攻撃から保護するには、IsLocalUrl () メソッドを追加し、ログオンアクションで returnUrl パラメーターを検証します。
