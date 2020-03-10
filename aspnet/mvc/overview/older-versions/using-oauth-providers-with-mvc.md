---
uid: mvc/overview/older-versions/using-oauth-providers-with-mvc
title: MVC 4 での OAuth プロバイダーの使用 |Microsoft Docs
author: Rick-Anderson
description: このチュートリアルでは、ユーザーが外部プロバイダーから資格情報 (Facebo... など) を使用してログインできるようにする ASP.NET MVC 4 web アプリケーションを構築する方法について説明します。
ms.author: riande
ms.date: 06/19/2013
ms.assetid: 7a87f16f-0e19-4f15-a88a-094ae866c4a2
msc.legacyurl: /mvc/overview/older-versions/using-oauth-providers-with-mvc
msc.type: authoredcontent
ms.openlocfilehash: 5dfd1305376a62f4987caea242ca0f6aac1018e9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78433366"
---
# <a name="using-oauth-providers-with-mvc-4"></a>MVC 4 で OAuth プロバイダーを使用する

[Tom FitzMacken](https://github.com/tfitzmac)

> このチュートリアルでは、ユーザーが Facebook、Twitter、Microsoft、Google などの外部プロバイダーから資格情報を使用してログインできるようにする ASP.NET MVC 4 web アプリケーションを作成する方法について説明します。また、これらのプロバイダーの機能の一部をに統合します。web アプリケーション。 わかりやすくするために、このチュートリアルでは Facebook の資格情報を使用する方法について説明します。
> 
> ASP.NET MVC 5 web アプリケーションで外部資格情報を使用するには、 [Facebook と Google OAuth2 を使用した ASP.NET MVC 5 アプリの作成と OpenID サインオン](../security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)に関する web サイトを参照してください。
> 
> Web サイトでこれらの資格情報を有効にすると、これらの外部プロバイダーのアカウントが何百万ものユーザーに既に存在するため、大きな利点があります。 このようなユーザーは、新しい資格情報のセットを作成して記憶する必要がない場合に、サイトにサインアップすることができます。 また、ユーザーがこれらのプロバイダーのいずれかを使用してログインした後、プロバイダーからソーシャル操作を組み込むことができます。

## <a name="what-youll-build"></a>ビルドする内容

このチュートリアルには主に次の2つの目標があります。

1. ユーザーが OAuth プロバイダーからの資格情報でログインできるようにします。
2. プロバイダーからアカウント情報を取得し、その情報をサイトのアカウント登録と統合します。

このチュートリアルの例では、Facebook を認証プロバイダーとして使用する方法に焦点を当てていますが、プロバイダーのいずれかを使用するようにコードを変更することもできます。 プロバイダーを実装する手順は、このチュートリアルで説明されている手順とよく似ています。 プロバイダーの API セットを直接呼び出す場合は、大きな違いに注意してください。

## <a name="prerequisites"></a>前提条件

- [Microsoft Visual Studio 2012](https://www.microsoft.com/visualstudio/eng/downloads#vs)または[Web 用 Microsoft Visual Studio Express 2012](https://www.microsoft.com/visualstudio/eng/downloads#d-2012-express)

または

- Microsoft Visual Studio 2010 SP1 または[Visual Web Developer Express 2010 sp1](https://www.microsoft.com/visualstudio/eng/downloads#d-2010-express)
- [ASP.NET MVC 4](https://go.microsoft.com/fwlink/?LinkId=243392)

さらに、このトピックでは、ASP.NET MVC と Visual Studio に関する基本的な知識があることを前提としています。 ASP.NET MVC 4 の概要については、「 [ASP.NET mvc 4](getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4.md)の概要」を参照してください。

## <a name="create-the-project"></a>プロジェクトを作成する

Visual Studio で、新しい ASP.NET MVC 4 Web アプリケーションを作成し、&quot;OAuthMVC&quot;という名前を指定します。 .NET Framework 4.5 または4のいずれかを対象にすることができます。

![プロジェクトの作成](using-oauth-providers-with-mvc/_static/image1.png)

新しい ASP.NET MVC 4 プロジェクトウィンドウで、 **[インターネットアプリケーション]** を選択し、 **Razor**をビューエンジンとして残します。

![インターネットアプリケーションの選択](using-oauth-providers-with-mvc/_static/image2.png)

## <a name="enable-a-provider"></a>プロバイダーを有効にする

インターネットアプリケーションテンプレートを使用して MVC 4 web アプリケーションを作成すると、アプリ\_の [開始] フォルダーに AuthConfig.cs という名前のファイルがプロジェクトに作成されます。

![AuthConfig ファイル](using-oauth-providers-with-mvc/_static/image3.png)

AuthConfig ファイルには、外部認証プロバイダーのクライアントを登録するためのコードが含まれています。 既定では、このコードはコメントアウトされているため、外部プロバイダーは有効になりません。

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample1.cs)]

外部認証クライアントを使用するには、このコードのコメントを解除する必要があります。 サイトに含めるプロバイダーのみをコメント解除します。 このチュートリアルでは、Facebook の資格情報のみを有効にします。

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample2.cs)]

上記の例では、メソッドに登録パラメーターに空の文字列が含まれていることに注意してください。 ここでアプリケーションを実行しようとすると、パラメーターに空の文字列が許可されていないため、アプリケーションは引数の例外をスローします。 有効な値を指定するには、次のセクションで示すように、外部プロバイダーに web サイトを登録する必要があります。

## <a name="registering-with-an-external-provider"></a>外部プロバイダーへの登録

外部プロバイダーからの資格情報を使用してユーザーを認証するには、web サイトをプロバイダーに登録する必要があります。 サイトを登録すると、クライアントを登録するときに含めるパラメーター (キー、id、シークレットなど) が表示されます。 使用するプロバイダーを持つアカウントが必要です。

このチュートリアルでは、これらのプロバイダーに登録するために実行する必要があるすべての手順については説明しません。 通常、この手順は困難ではありません。 サイトを正常に登録するには、これらのサイトに記載されている手順に従います。 サイトの登録を開始するには、次の開発者向けサイトを参照してください。

- [Facebook](https://developers.facebook.com/)
- [Google](https://developers.google.com/)
- [Microsoft](http://manage.dev.live.com/)
- [Twitter](https://dev.twitter.com/)

Facebook にサイトを登録するときに、次の図に示すように、サイトドメインに &quot;localhost&quot; を指定し、URL に `&quot; http://localhost/&quot;` します。 Localhost の使用はほとんどのプロバイダーで機能しますが、現在、Microsoft プロバイダーでは機能しません。 Microsoft プロバイダーには、有効な web サイトの URL を含める必要があります。

![サイトの登録](using-oauth-providers-with-mvc/_static/image4.png)

前の画像では、アプリ id、アプリのシークレット、連絡先の電子メールの値が削除されています。 実際にサイトを登録すると、その値が表示されます。 アプリ id とアプリシークレットの値は、アプリケーションに追加するため、メモしておきます。

## <a name="creating-test-users"></a>テストユーザーの作成

既存の Facebook アカウントを使用してサイトをテストすることが気にならない場合は、このセクションを省略してもかまいません。

Facebook アプリの管理ページで、アプリケーションのテストユーザーを簡単に作成できます。 これらのテストアカウントを使用して、サイトにログインすることができます。 テストユーザーを作成するには、左側のナビゲーションウィンドウで **[ロール]** リンクをクリックし、 **[作成]** リンクをクリックします。

![テストユーザーの作成](using-oauth-providers-with-mvc/_static/image5.png)

Facebook サイトでは、要求したテストアカウントの数が自動的に作成されます。

## <a name="adding-application-id-and-secret-from-the-provider"></a>プロバイダーからのアプリケーション id とシークレットの追加

Facebook から id とシークレットを受け取ったので、AuthConfig ファイルに戻り、パラメーター値として追加します。 次に示す値は実際の値ではありません。

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample3.cs)]

## <a name="log-in-with-external-credentials"></a>外部資格情報を使用してログインする

これで、サイトで外部資格情報を有効にする必要があります。 アプリケーションを実行し、右上隅にある [ログイン] リンクをクリックします。 このテンプレートは、Facebook をプロバイダーとして登録し、プロバイダーのボタンを含むことを自動的に認識します。 複数のプロバイダーを登録すると、1つのボタンが自動的に追加されます。

![外部ログイン](using-oauth-providers-with-mvc/_static/image6.png)

このチュートリアルでは、外部プロバイダーの [ログイン] ボタンをカスタマイズする方法については説明しません。 詳細については、「 [OAuth/OpenID を使用する場合のログイン UI のカスタマイズ](https://blogs.msdn.com/b/pranav_rastogi/archive/2012/08/24/customizing-the-login-ui-when-using-oauth-openid.aspx)」を参照してください。

Facebook の資格情報でログインするには、[Facebook] ボタンをクリックします。 外部プロバイダーの1つを選択すると、そのサイトにリダイレクトされ、そのサービスからログインするように求められます。

次の図は、Facebook のログイン画面を示しています。 ここでは、oauthmvcexample という名前のサイトにログインするために Facebook アカウントを使用していることに注意してください。

![facebook 認証](using-oauth-providers-with-mvc/_static/image7.png)

Facebook の資格情報を使用してログインすると、サイトが基本情報にアクセスできることをユーザーに通知するページが表示されます。

![アクセス許可の要求](using-oauth-providers-with-mvc/_static/image8.png)

**[アプリにアクセスする]** を選択した後、ユーザーはサイトに登録する必要があります。 次の図は、ユーザーが Facebook の資格情報でログインした後の登録ページを示しています。 通常、ユーザー名はプロバイダーからの名前で事前に入力されます。

![registrations](using-oauth-providers-with-mvc/_static/image9.png)

**[登録]** をクリックして登録を完了します。 ブラウザーを閉じます。

新しいアカウントがデータベースに追加されていることを確認できます。 サーバーエクスプローラーで、 **Defaultconnection**データベースを開き、 **Tables**フォルダーを開きます。

![データベース テーブル](using-oauth-providers-with-mvc/_static/image10.png)

**UserProfile**テーブルを右クリックし、 **[テーブルデータの表示]** をクリックします。

![データの表示](using-oauth-providers-with-mvc/_static/image11.png)

追加した新しいアカウントが表示されます。 **Web ページ\_OAuthMembership**テーブルのデータを確認します。 追加したアカウントの外部プロバイダーに関連するデータがさらに表示されます。

外部認証のみを有効にする場合は、これで完了です。 ただし、次のセクションに示すように、プロバイダーからの情報を新しいユーザー登録プロセスにさらに統合することができます。

## <a name="create-models-for-additional-user-information"></a>追加のユーザー情報のモデルを作成する

前のセクションでご存知のように、組み込みアカウントの登録に関する追加情報を取得する必要はありません。 ただし、ほとんどの外部プロバイダーは、ユーザーに関する追加情報を返します。 以下のセクションでは、その情報を保持し、データベースに保存する方法について説明します。 具体的には、ユーザーのフルネーム、ユーザーの個人用 web ページの URI、および Facebook によってアカウントが検証されたかどうかを示す値を保持します。

追加のユーザー情報を格納するテーブルを追加するには、 [Code First Migrations](https://msdn.microsoft.com/data/jj591621)を使用します。 既存のデータベースにテーブルを追加しようとしているため、最初に現在のデータベースのスナップショットを作成する必要があります。 現在のデータベースのスナップショットを作成することによって、後で新しいテーブルだけを含む移行を作成できます。 現在のデータベースのスナップショットを作成するには、次のようにします。

1. **パッケージマネージャーコンソール**を開く
2. **Enable-移行**コマンドを実行します。
3. **[追加-移行の初期-ignorechanges 追加]** コマンドを実行します。
4. コマンド「 **update-database** 」を実行します。

ここでは、新しいプロパティを追加します。 [モデル] フォルダーで、AccountModels.cs ファイルを開き、RegisterExternalLoginModel クラスを見つけます。 RegisterExternalLoginModel クラスは、認証プロバイダーから返される値を保持します。 次に強調表示されているように、FullName と Link という名前のプロパティを追加します。

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample4.cs?highlight=9-13)]

また、AccountModels.cs で、ExtraUserInformation という名前の新しいクラスを追加します。 このクラスは、データベースに作成される新しいテーブルを表します。

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample5.cs)]

[プロパティ] コンテキストクラスで、下に強調表示されているコードを追加して、新しいクラスの DbSet プロパティを作成します。

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample6.cs?highlight=9)]

これで、新しいテーブルを作成する準備が整いました。 次のように、パッケージマネージャーコンソールをもう一度開きます。

1. **AddExtraUserInformation**コマンドを実行します。
2. コマンド「 **update-database** 」を実行します。

新しいテーブルがデータベースに存在するようになりました。

## <a name="retrieve-the-additional-data"></a>追加データを取得する

追加のユーザーデータを取得するには、2つの方法があります。 最初の方法は、認証要求時に既定で返されるユーザーデータを保持することです。 2つ目の方法は、プロバイダー API を呼び出し、詳細情報を要求することです。 FullName と Link の値は、Facebook によって自動的に返されます。 Facebook API の呼び出しによってアカウントが取得されたことを Facebook が検証したかどうかを示す値。 まず、FullName と Link の値を設定してから、後で検証済みの値を取得します。

追加のユーザーデータを取得するには、 **Controllers**フォルダー内の**AccountController.cs**ファイルを開きます。

このファイルには、アカウントのログ記録、登録、管理を行うためのロジックが含まれています。 具体的には、 **Externallogincallback**および**externallogincallback**と呼ばれるメソッドに注意してください。 これらのメソッド内では、アプリケーションの外部ログイン操作をカスタマイズするコードを追加できます。 **Externallogincallback**メソッドの最初の行には、次のものが含まれます。

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample7.cs)]

追加のユーザーデータは、 **Verifyauthentication**メソッドから返される**Authenticationresult**オブジェクトの**ExtraData**プロパティに戻されます。 Facebook クライアントには、 **ExtraData**プロパティに次の値が含まれています。

- id
- name
- link
- gender
- accesstoken

他のプロバイダーは、ExtraData プロパティに類似しているがわずかに異なるデータを持ちます。

ユーザーがサイトを初めて使用する場合は、追加データを取得し、そのデータを確認ビューに渡します。 メソッドの最後のコードブロックは、ユーザーがサイトを初めて使用する場合にのみ実行されます。 次の行を置き換えます。

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample8.cs)]

次の行に置き換えることができます。

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample9.cs)]

この変更には、FullName プロパティと Link プロパティの値のみが含まれます。

**Externalloginconfirmation**メソッドで、以下の強調表示されているコードを変更して、追加のユーザー情報を保存します。

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample10.cs?highlight=4,7-13)]

## <a name="adjusting-the-view"></a>ビューの調整

プロバイダーから取得した追加のユーザーデータが登録ページに表示されます。

**Views**/**Account**フォルダーで、 **externalloginconfirmation. cshtml**を開きます。 [ユーザー名] の既存のフィールドの下に、[FullName]、[Link]、および [ピクチャ] リンクのフィールドを追加します。

[!code-cshtml[Main](using-oauth-providers-with-mvc/samples/sample11.cshtml)]

これで、アプリケーションを実行し、追加情報が保存された新しいユーザーを登録する準備ができました。 まだサイトに登録されていないアカウントが必要です。 別のテストアカウントを使用するか、再利用するアカウントの**UserProfile**および**Web ページ\_oauthmembership**テーブル内の行を削除することができます。 これらの行を削除すると、アカウントが再度登録されることになります。

アプリケーションを実行し、新しいユーザーを登録します。 今回は、確認ページに多くの値が含まれていることに注意してください。

![registrations](using-oauth-providers-with-mvc/_static/image12.png)

登録が完了したら、ブラウザーを閉じます。 データベースを調べて、 **ExtraUserInformation**テーブルの新しい値を確認します。

## <a name="install-nuget-package-for-facebook-api"></a>Facebook API の NuGet パッケージをインストールする

Facebook には、操作を実行するために呼び出すことができる[API](https://developers.facebook.com/docs/reference/apis/)が用意されています。 Facebook API は、HTTP 要求を送信するか、これらの要求の送信を容易にする NuGet パッケージのインストールを使用して呼び出すことができます。 このチュートリアルでは、NuGet パッケージの使用方法について説明しますが、NuGet パッケージのインストールは必須ではありません。 このチュートリアルでは、Facebook C# SDK パッケージを使用する方法について説明します。 Facebook API の呼び出しに役立つ NuGet パッケージが他にもあります。

**[NuGet パッケージの管理]** ウィンドウで、Facebook C# SDK パッケージを選択します。

![パッケージのインストール](using-oauth-providers-with-mvc/_static/image13.png)

Facebook C# SDK を使用して、ユーザーのアクセストークンを必要とする操作を呼び出します。 次のセクションでは、アクセストークンを取得する方法について説明します。

## <a name="retrieve-access-token"></a>アクセストークンの取得

ほとんどの外部プロバイダーは、ユーザーの資格情報が検証された後にアクセストークンを返します。 このアクセストークンは、認証されたユーザーのみが使用できる操作を呼び出すことができるため、非常に重要です。 そのため、より多くの機能を提供する必要がある場合は、アクセストークンの取得と格納が不可欠です。

外部プロバイダーによっては、アクセストークンの有効期間が限られている場合があります。 有効なアクセストークンがあることを確認するには、ユーザーがログインするたびにそれを取得し、それをデータベースに保存するのではなく、セッション値として格納します。

**Externallogincallback**メソッドでは、アクセストークンも**Authenticationresult**オブジェクトの**ExtraData**プロパティに戻されます。 強調表示されているコードを**Externallogincallback**に追加して、**セッション**オブジェクトにアクセストークンを保存します。 このコードは、ユーザーが Facebook アカウントでログインするたびに実行されます。

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample12.cs?highlight=11-14)]

この例では Facebook からアクセストークンを取得しますが、&quot;accesstoken&quot;という名前の同じキーを使用して外部プロバイダーからアクセストークンを取得できます。

## <a name="logging-off"></a>ログオフ中

既定の**ログオフ**メソッドでは、アプリケーションからユーザーがログアウトされますが、外部プロバイダーからユーザーがログアウトされることはありません。 ユーザーを Facebook からログアウトし、ユーザーがログオフした後にトークンが保持されないようにするには、次の強調表示されたコードを AccountController の**LogOff**メソッドに追加します。

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample13.cs?highlight=6-14)]

`next` パラメーターで指定する値は、ユーザーが Facebook からログアウトした後に使用する URL です。 ローカルコンピューターでテストする場合は、ローカルサイトの正しいポート番号を指定します。 実稼働環境では、contoso.com などの既定のページを指定します。

## <a name="retrieve-user-information-that-requires-the-access-token"></a>アクセストークンを必要とするユーザー情報を取得する

アクセストークンを格納し、Facebook C# SDK パッケージをインストールしたので、これらを一緒に使用して、facebook から追加のユーザー情報を要求することができます。 **Externalloginconfirmation**メソッドで、アクセストークンの値を渡して、 **FacebookClient**クラスのインスタンスを作成します。 現在の認証済みユーザーの**検証済み**プロパティの値を要求します。 "**確認済み**" プロパティは、携帯電話にメッセージを送信するなど、他の方法で Facebook がアカウントを検証したかどうかを示します。 この値をデータベースに保存します。

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample14.cs?highlight=7-18,25)]

この場合も、ユーザーのデータベース内のレコードを削除するか、別の Facebook アカウントを使用する必要があります。

アプリケーションを実行し、新しいユーザーを登録します。 検証済みプロパティの値を確認するには、 **ExtraUserInformation**テーブルを参照してください。

## <a name="conclusion"></a>まとめ

このチュートリアルでは、ユーザー認証と登録データ用に Facebook と統合されたサイトを作成しました。 MVC 4 web アプリケーション用に設定されている既定の動作と、その既定の動作をカスタマイズする方法について学習しました。

## <a name="related-topics"></a>関連トピック

- [認証および SQL DB を使用する ASP.NET MVC アプリの作成と、Azure App Service へのデプロイ](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)
