---
uid: web-pages/overview/security/enabling-login-from-external-sites-in-an-aspnet-web-pages-site
title: ASP.NET Web ページ (Razor) サイトで外部サイトを使用してログインする |Microsoft Docs
author: Rick-Anderson
description: この記事では、Facebook、Google、Twitter、Yahoo、およびその他のサイト (サポートする方法) を使用して、ASP.NET Web ページ (Razor) サイトにログインする方法について説明します。
ms.author: riande
ms.date: 02/21/2014
ms.assetid: ef852096-a5bf-47b3-9945-125cde065093
msc.legacyurl: /web-pages/overview/security/enabling-login-from-external-sites-in-an-aspnet-web-pages-site
msc.type: authoredcontent
ms.openlocfilehash: 860b75422c3df1d191ed861344963bfc19270e8f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78518788"
---
# <a name="logging-in-using-external-sites-in-an-aspnet-web-pages-razor-site"></a>ASP.NET Web ページ (Razor) サイトで外部サイトを使用してログインする

[Tom FitzMacken](https://github.com/tfitzmac)

> この記事では、Facebook、Google、Twitter、Yahoo などのサイトを使用して ASP.NET Web ページ (Razor) サイトにログインする方法について説明します。つまり、サイトで OAuth と OpenID をサポートする方法について説明します。
> 
> ここでは、次の内容について学習します。
> 
> - WebMatrix スターターサイトテンプレートを使用するときに、他のサイトからのログインを有効にする方法について説明します。
> 
> この記事で導入された ASP.NET 機能は次のとおりです。
> 
> - `OAuthWebSecurity` ヘルパー。
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>このチュートリアルで使用されているソフトウェアのバージョン
> 
> 
> - ASP.NET Web ページ (Razor) 2
> - WebMatrix 3

ASP.NET Web ページには、 [OAuth](http://oauth.net/)および[OpenID](http://openid.net/)プロバイダーのサポートが含まれています。 これらのプロバイダーを使用すると、Facebook、Twitter、Microsoft、Google の既存の資格情報を使用して、ユーザーがサイトにログインできるようになります。 たとえば、Facebook アカウントを使用してログインする場合、ユーザーは Facebook アイコンを選択するだけで、facebook のログインページにリダイレクトされ、ユーザー情報が入力されます。 その後、Facebook ログインをサイトのアカウントに関連付けることができます。 Web ページのメンバーシップ機能に関連する機能強化として、ユーザーは複数のログイン (ソーシャルネットワークサイトからのログインを含む) を web サイトの1つのアカウントに関連付けることができます。

このイメージは、**スターターサイト**テンプレートのログインページを示しています。ユーザーは、Facebook、Twitter、Google、Microsoft アイコンを選択して、外部アカウントでログインできるようになります。

![外部プロバイダー](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image1.png)

コメント解除を使用して、いくつかのコード行を**スターターサイト**テンプレートに記述することにより、OAuth および OpenID メンバーシップを有効にすることができます。 OAuth プロバイダーおよび OpenID プロバイダーの操作に使用するメソッドとプロパティは、`WebMatrix.Security.OAuthWebSecurity` クラスに含まれています。 **スターターサイト**テンプレートには、完全なメンバーシップインフラストラクチャが含まれており、ログインページ、メンバーシップデータベース、およびユーザーがローカルの資格情報または別のサイトのサイトにログインするために必要なすべてのコードが含まれています。

このセクションでは、ユーザーが外部サイトから**スターターサイト**テンプレートに基づくサイトにログインできるようにする方法の例を示します。 スターターサイトを作成した後、次の手順を実行します (詳細については、こちらを参照してください)。

- OAuth プロバイダー (Facebook、Twitter、Microsoft) を使用するサイトでは、外部サイトでアプリケーションを作成します。 これにより、これらのサイトのログイン機能を呼び出すために必要なアプリケーションキーが得られます。
- OpenID プロバイダー (Google) を使用するサイトでは、アプリケーションを作成する必要はありません。 これらのサイトのすべてについて、ログインし、開発者アプリケーションを作成するためのアカウントが必要です。

    > [!NOTE]
    > Microsoft アプリケーションは、実際の web サイトのライブ URL のみを受け入れるため、ログインのテストにローカル web サイトの URL を使用することはできません。
- 適切な認証プロバイダーを指定し、使用するサイトにログインを送信するために、web サイト内のいくつかのファイルを編集します。

この記事では、次のタスクについて個別に説明します。

- [Google ログインを有効にする](#To_enable_Google_logins)
- [Facebook ログインの有効化](#To_enable_Facebook_logins)
- [Twitter ログインの有効化](#To_enable_Twitter_logins)

<a id="To_enable_Google_logins"></a>
## <a name="enabling-google-logins"></a>Google ログインを有効にする

1. WebMatrix スターターサイトテンプレートに基づく ASP.NET Web ページサイトを作成または開きます。
2. *\_該当*ページを開き、次のコード行をコメント解除します。 

    [!code-css[Main](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/samples/sample1.css)]

### <a name="testing-google-login"></a>Google ログインをテストしています

1. サイトの*既定の cshtml*ページを実行し、 **[ログイン]** ボタンを選択します。
2. [*ログイン*] ページの **[別のサービスを使用してログインする]** セクションで、 **[Google]** または **[Yahoo]** submit ボタンのいずれかを選択します。 この例では、Google ログインを使用します。 

    Web ページは、要求を Google ログインページにリダイレクトします。

    ![Google サインイン](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image2.png)
3. 既存の Google アカウントの資格情報を入力します。
4. アカウントの情報を*Localhost*で使用できるようにするかどうかを確認するメッセージが表示されたら、 **[許可]** をクリックします。

    このコードでは、Google トークンを使用してユーザーを認証した後、web サイトのこのページに戻ります。 このページでは、ユーザーは Google ログインを web サイトの既存のアカウントに関連付けることができます。また、サイトに新しいアカウントを登録して、外部ログインをに関連付けることもできます。

    ![oauth-5](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image3.png)
5. **[関連付け]** ボタンをクリックします。 ブラウザーがアプリケーションのホームページに戻ります。

<a id="To_enable_Facebook_logins"></a>
## <a name="enabling-facebook-logins"></a>Facebook ログインの有効化

1. [Facebook 開発者サイト](https://developers.facebook.com/apps)にアクセスします (まだログインしていない場合はログインしてください)。
2. **[新しいアプリの作成]** ボタンを選択し、画面の指示に従って新しいアプリケーションを作成します。
3. **[アプリを Facebook と統合する方法を選択**します] セクションで、 **[web サイト]** セクションを選択します。
4. [サイトの**url** ] フィールドに、サイトの url (`http://www.example.com`など) を入力します。 **ドメイン**フィールドは省略可能です。これを使用して、ドメイン全体 ( *example.com*など) の認証を行うことができます。 

    > [!NOTE]
    > `http://localhost:12345` のような URL (番号はローカルポート番号) を使用してローカルコンピューター上でサイトを実行している場合は、サイトをテストするための **[サイトの URL]** フィールドにこの値を追加できます。 ただし、ローカルサイトのポート番号が変更された場合は常に、アプリケーションの **[サイトの URL]** フィールドを更新する必要があります。
5. **[変更の保存]** をクリックします。
6. もう一度 **[アプリ]** タブをクリックし、アプリケーションのスタートページを表示します。
7. アプリケーションの**アプリ ID**と**アプリシークレット**の値をコピーし、一時テキストファイルに貼り付けます。 これらの値は、web サイトコードの Facebook プロバイダーに渡されます。
8. Facebook 開発者サイトを終了します。

ここで、ユーザーが Facebook アカウントを使用してサイトにログインできるように、web サイトの2つのページに変更を加えます。

1. WebMatrix スターターサイトテンプレートに基づく ASP.NET Web ページサイトを作成または開きます。
2. *\_該当*ページを開き、Facebook OAuth プロバイダーのコードをコメント解除します。 コメント解除されたコードブロックは次のようになります。 

    [!code-csharp[Main](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/samples/sample2.cs)]
3. Facebook アプリケーションの **[アプリ ID]** の値を `appId` パラメーター (引用符内) の値としてコピーします。
4. `appSecret` パラメーター値として Facebook アプリケーションから**アプリシークレット**値をコピーします。
5. ファイルを保存して閉じます。

### <a name="testing-facebook-login"></a>Facebook ログインのテスト

1. サイトの既定の*cshtml*ページを実行し、 **[ログイン]** ボタンをクリックします。
2. [*ログイン*] ページの **[別のサービスを使用してログインする]** セクションで、 **[Facebook]** アイコンを選択します。 

    Web ページは、Facebook ログインページに要求をリダイレクトします。

    ![oauth-2](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image4.png)
3. Facebook アカウントにログインします。 

    このコードでは、Facebook トークンを使用して認証を行い、Facebook ログインをサイトのログインに関連付けることができるページに戻ります。 ユーザー名または電子メールアドレスは、フォームの **[電子メール]** フィールドに入力されます。

    ![oauth-5](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image5.png)
4. **[関連付け]** ボタンをクリックします。 

    ブラウザーがホームページに戻り、ログインします。

<a id="To_enable_Twitter_logins"></a>
## <a name="enabling-twitter-logins"></a>Twitter ログインの有効化

1. [Twitter 開発者サイト](https://dev.twitter.com/)に移動します。
2. **[アプリの作成]** リンクを選択し、サイトにログインします。
3. **[アプリケーションの作成]** フォームで、 **[名前]** フィールドと **[説明]** フィールドに入力します。
4. **[Web サイト]** フィールドに、サイトの URL (`http://www.example.com`など) を入力します。 

    > [!NOTE]
    > (`http://localhost:12345`のような URL を使用して) サイトをローカルでテストしている場合、Twitter は URL を受け入れない可能性があります。 ただし、ローカルループバック IP アドレス (`http://127.0.0.1:12345`など) を使用できる場合があります。 これにより、アプリケーションをローカルでテストするプロセスが簡単になります。 ただし、ローカルサイトのポート番号が変更されるたびに、アプリケーションの**Web サイト**フィールドを更新する必要があります。
5. **[コールバック URL]** フィールドに、Twitter にログインした後にユーザーが返す web サイトのページの URL を入力します。 たとえば、スタートサイトのホームページ (ログイン状態を認識する) にユーザーを送信するには、 **[Web サイト]** フィールドに入力したものと同じ URL を入力します。
6. 使用条件に同意し、 **[Twitter アプリケーションの作成]** ボタンを選択します。
7. **[マイアプリケーション**] ランディングページで、作成したアプリケーションを選択します。
8. **[詳細]** タブで一番下までスクロールし、 **[アクセストークンの作成]** ボタンをクリックします。
9. **[詳細]** タブで、アプリケーションの**コンシューマーキー**と**コンシューマーシークレット**の値をコピーし、一時テキストファイルに貼り付けます。 これらの値は、web サイトコードの Twitter プロバイダーに渡されます。
10. Twitter サイトを終了します。

これで、ユーザーが Twitter アカウントを使用してサイトにログインできるように、web サイトの2つのページに変更が加えられました。

1. WebMatrix スターターサイトテンプレートに基づく ASP.NET Web ページサイトを作成または開きます。
2. *\_該当*ページを開き、Twitter OAuth プロバイダーのコードをコメント解除します。 コメント解除されたコードブロックは次のようになります。 

    [!code-csharp[Main](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/samples/sample3.cs)]
3. Twitter アプリケーションの**コンシューマーキー**の値を `consumerKey` パラメーター (引用符内) の値としてコピーします。
4. `consumerSecret` パラメーターの値として、Twitter アプリケーションから**コンシューマーシークレット**の値をコピーします。
5. ファイルを保存して閉じます。

### <a name="testing-twitter-login"></a>Twitter ログインのテスト

1. サイトの*既定の cshtml*ページを実行し、 **[ログイン]** ボタンをクリックします。
2. [*ログイン*] ページの **[別のサービスを使用してログインする]** セクションで、 **Twitter**アイコンを選択します。 

    Web ページによって、作成したアプリケーションの Twitter ログインページに要求がリダイレクトされます。

    ![oauth-4](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image6.png)
3. Twitter アカウントにログインします。
4. このコードでは、Twitter トークンを使用してユーザーを認証した後、ログインを web サイトアカウントに関連付けることができるページに戻ります。 名前または電子メールアドレスは、フォームの **[電子メール]** フィールドに入力されます。

    ![oauth-5](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image7.png)
5. **[関連付け]** ボタンをクリックします。 

    ブラウザーがホームページに戻り、ログインします。

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>その他のリソース

- [サイト全体の動作をカスタマイズする](https://go.microsoft.com/fwlink/?LinkId=202906)
- [ASP.NET Web ページサイトにセキュリティとメンバーシップを追加する](https://go.microsoft.com/fwlink/?LinkID=202904)
