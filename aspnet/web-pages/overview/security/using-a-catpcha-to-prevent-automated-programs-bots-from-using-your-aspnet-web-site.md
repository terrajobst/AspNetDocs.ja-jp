---
uid: web-pages/overview/security/using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site
title: CAPTCHA を使用して、ボットが ASP.NET Web Razor を使用しないようにします。Microsoft Docs
author: microsoft
description: この記事では、ReCaptcha (セキュリティ対策) を使用して、自動プログラム (ボット) が ASP.NET Web ページ (Razor) のタスクを実行できないようにする方法について説明します。
ms.author: riande
ms.date: 05/21/2012
ms.assetid: 2b381a41-2cb3-40c0-8545-1d393e22877f
msc.legacyurl: /web-pages/overview/security/using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site
msc.type: authoredcontent
ms.openlocfilehash: 2647a3155893a3dfb3214795a5f9cf1e8931fa91
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78440194"
---
# <a name="using-a-captcha-to-prevent-bots-from-using-your-aspnet-web-razor-site"></a>CAPTCHA を使用して、ボットが ASP.NET Web Razor) サイトを使用しないようにする

[Microsoft](https://github.com/microsoft)

> この記事では、ReCaptcha (セキュリティ対策) を使用して、自動プログラム (ボット) が ASP.NET Web ページ (Razor) web サイトでタスクを実行できないようにする方法について説明します。
> 
> **学習内容:** 
> 
> - CAPTCHA テストをサイトに追加する方法。
> 
> この記事で導入された ASP.NET 機能を次に示します。
> 
> - `ReCaptcha` ヘルパー。
> 
> > [!NOTE]
> > この記事の情報は、ASP.NET Web ページ1.0 と Web ページ2に適用されます。

## <a name="about-captchas"></a>CAPTCHAs について

ユーザーがサイトに登録するとき、または名前と URL を入力するだけで (ブログコメントなど)、フェイク名があふれてしまうことがあります。 これらは、多くの場合、検索可能なすべての web サイトに Url を残しようとする自動プログラム (ボット) によって残されています。 (一般的な動機は、販売する製品の Url を投稿することです)。

ユーザーが*CAPTCHA*を使用してユーザーを登録したとき、またはその他の方法で名前とサイトを入力したときにユーザーを検証することで、ユーザーがコンピュータープログラムではないことを確認できます。 CAPTCHA は、コンピューターや人間を区別するために、完全に自動化されたパブリックチューリングテストを意味します。 CAPTCHA は*チャレンジ/レスポンス*テストであり、ユーザーは簡単に実行できますが、自動化されたプログラムを実行するのは難しいものです。 最も一般的な種類の CAPTCHA は、歪んだ文字が表示され、入力を求められるものです。 (ゆがみは、ボットが文字を解読するのを困難にすることが想定されています)。

## <a name="adding-a-recaptcha-test"></a>ReCaptcha テストの追加

ASP.NET ページでは、`ReCaptcha` ヘルパーを使用して、ReCaptcha サービス ([http://recaptcha.net](http://recaptcha.net)) に基づく CAPTCHA テストを表示できます。 `ReCaptcha` ヘルパーは、ページが検証される前にユーザーが正しく入力する必要がある、2つの歪んだ単語の画像を表示します。 ユーザーの応答は、ReCaptcha.Net サービスによって検証されます。

![](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/_static/image1.jpg)

1. Web サイトを ReCaptcha.Net ([http://recaptcha.net](http://recaptcha.net)) に登録します。 登録が完了すると、公開キーと秘密キーが取得されます。
2. 「 [ASP.NET Web ページサイトにヘルパーをインストール](https://go.microsoft.com/fwlink/?LinkId=252372)する」の説明に従って、ASP.NET Web ヘルパーライブラリを web サイトに追加します (まだインストールしていない場合)。
3. *\_該当*ファイルをまだ持っていない場合は、web サイトのルートフォルダーに *\_該当*という名前のファイルを作成します。
4. *\_該当*ファイルに次の `Recaptcha` helper 設定を追加します。 

    [!code-cshtml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample1.cshtml?highlight=6-7)]
5. 独自の公開キーと秘密キーを使用して、`PublicKey` と `PrivateKey` のプロパティを設定します。
6. *\_該当*ファイルを保存して閉じます。
7. Web サイトのルートフォルダーに、 *Recaptcha*という名前の新しいページを作成します。
8. 既存のコンテンツを次の内容に置き換えます。 

    [!code-cshtml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample2.cshtml)]
9. ブラウザーで*Recaptcha*ページを実行します。 `PrivateKey` の値が有効な場合、ページには ReCaptcha コントロールとボタンが表示されます。 *\_該当*でグローバルにキーを設定しなかった場合は、ページにエラーが表示されます。 

    ![](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/_static/image1.png)
10. テスト用の単語を入力します。 ReCaptcha テストに合格すると、その効果に関するメッセージが表示されます。 それ以外の場合は、エラーメッセージが表示され、ReCaptcha コントロールが再表示されます。

> [!NOTE]
> コンピューターがプロキシサーバーを使用するドメインにある場合*は、web.config ファイルの*`defaultproxy` 要素の構成が必要になることがあります。 次の例は、ReCaptcha サービスが機能するように構成された `defaultproxy` 要素を含む*web.config ファイルを*示しています。
> 
> [!code-xml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample3.xml)]

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>その他のリソース

- [ASP.NET Web ページサイトのサイト全体の動作のカスタマイズ](https://go.microsoft.com/fwlink/?LinkId=202906)
- [ReCaptcha サイト](https://www.google.com/recaptcha)
