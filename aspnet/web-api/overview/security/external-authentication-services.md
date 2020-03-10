---
uid: web-api/overview/security/external-authentication-services
title: ASP.NET Web API (C#) を使用した外部認証サービスMicrosoft Docs
author: rmcmurray
description: ASP.NET Web API での外部認証サービスの使用について説明します。
ms.author: riande
ms.date: 01/28/2019
ms.assetid: 3bb8eb15-b518-44f5-a67d-a27e051aedc6
msc.legacyurl: /web-api/overview/security/external-authentication-services
msc.type: authoredcontent
ms.openlocfilehash: b2571552a3f8040ff42bfa0a9fa48981f71a1e4b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78447418"
---
# <a name="external-authentication-services-with-aspnet-web-api-c"></a>ASP.NET Web API (C#) を使用した外部認証サービス

Visual Studio 2017 と ASP.NET 4.7.2 は、[シングルページアプリケーション](../../../single-page-application/index.md)(SPA) と[Web API](../../index.md)サービスのセキュリティオプションを拡張して、複数の OAuth/OpenID およびソーシャルメディア認証サービス (Microsoft アカウント、Twitter、Facebook、Google) を含む外部認証サービスと統合します。  

### <a name="in-this-walkthrough"></a>このチュートリアルの手順

- [外部認証サービスの使用](#USING)
- [サンプル Web アプリケーションの作成](#SAMPLE)
- [Facebook 認証を有効にする](#FACEBOOK)
- [Google 認証を有効にする](#GOOGLE)
- [Microsoft 認証を有効にする](#MICROSOFT)
- [Twitter 認証を有効にする](#TWITTER)
- [追加情報](#MOREINFO)

    - [外部認証サービスの組み合わせ](#COMBINE)
    - [完全修飾ドメイン名を使用するように IIS Express を構成する](#FQDN)
    - [Microsoft 認証のアプリケーション設定を取得する方法](#OBTAIN)
    - [省略可能: ローカル登録を無効にする](#DISABLE)

### <a name="prerequisites"></a>前提条件

このチュートリアルの例を実行するには、次のものが必要です。

- Visual Studio 2017
- 次のいずれかのソーシャルメディア認証サービスのアプリケーション id とシークレットキーを持つ開発者アカウント:

  - Microsoft アカウント ([https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070))
  - Twitter ([https://dev.twitter.com/](https://dev.twitter.com/))
  - Facebook ([https://developers.facebook.com/](https://developers.facebook.com/))
  - Google ([https://developers.google.com/](https://developers.google.com))

<a id="USING"></a>
## <a name="using-external-authentication-services"></a>外部認証サービスの使用

Web 開発者が現在使用できる多数の外部認証サービスは、新しい web アプリケーションを作成するときの開発時間を短縮するのに役立ちます。 Web ユーザーは一般的に、一般的な web サービスとソーシャルメディア web サイト用にいくつかの既存のアカウントを持っています。そのため、web アプリケーションが外部 web サービスまたはソーシャルメディア web サイトから認証サービスを実装すると、開発時間が短縮されます。では、認証実装の作成に費やしました。 外部認証サービスを使用すると、エンドユーザーは web アプリケーション用に別のアカウントを作成する必要がなくなります。また、別のユーザー名とパスワードを覚えておく必要もありません。

これまで、開発者には、独自の認証実装を作成する方法と、外部認証サービスをアプリケーションに統合する方法についての2つの選択肢がありました。 最も基本的なレベルでは、次の図は、外部認証サービスを使用するように構成された web アプリケーションの情報を要求しているユーザーエージェント (web ブラウザー) の単純な要求フローを示しています。

[![](external-authentication-services/_static/image2.png "Click to Expand the Image")](external-authentication-services/_static/image1.png)

上の図では、ユーザーエージェント (この例では web ブラウザー) が web アプリケーションに要求を行い、web ブラウザーが外部認証サービスにリダイレクトされます。 ユーザーエージェントが外部認証サービスに資格情報を送信すると、ユーザーエージェントが正常に認証されると、外部認証サービスによってユーザーエージェントが元の web アプリケーションにリダイレクトされ、ユーザーエージェントが web アプリケーションに送信します。 Web アプリケーションは、トークンを使用して、ユーザーエージェントが外部認証サービスによって正常に認証されたことを確認します。また、web アプリケーションは、トークンを使用して、ユーザーエージェントに関する詳細情報を収集できます。 アプリケーションがユーザーエージェントの情報の処理を完了すると、web アプリケーションは、承認設定に基づいて、ユーザーエージェントに適切な応答を返します。

この2番目の例では、ユーザーエージェントが web アプリケーションと外部承認サーバーとネゴシエートし、web アプリケーションが外部承認サーバーとの追加の通信を実行して、ユーザーに関する追加情報を取得します。・

[![](external-authentication-services/_static/image4.png "Click to Expand the Image")](external-authentication-services/_static/image3.png)

Visual Studio 2017 と ASP.NET 4.7.2 は、次の認証サービスの組み込み統合機能を提供することで、開発者にとって外部認証サービスとの統合を容易にします。

- Facebook
- Google
- Microsoft アカウント (Windows Live ID アカウント)
- Twitter

このチュートリアルの例では、Visual Studio 2017 に付属している new ASP.NET Web アプリケーションテンプレートを使用して、サポートされている各外部認証サービスを構成する方法を示します。

> [!NOTE]
> 必要に応じて、外部認証サービスの設定に FQDN を追加することが必要になる場合があります。 この要件は、アプリケーション設定の FQDN がクライアントによって使用される FQDN と一致する必要がある一部の外部認証サービスのセキュリティ制約に基づいています。 (この手順は、外部認証サービスごとに大きく異なります。各外部認証サービスのドキュメントを参照して、必要かどうか、およびこれらの設定を構成する方法を確認する必要があります)。この環境をテストするために FQDN を使用するように IIS Express を構成する必要がある場合は、このチュートリアルで後述[する「完全修飾ドメイン名を使用するための IIS Express の構成](#FQDN)」セクションを参照してください。

<a id="SAMPLE"></a>
## <a name="create-a-sample-web-application"></a>サンプル Web アプリケーションを作成する

次の手順では、ASP.NET Web アプリケーションテンプレートを使用してサンプルアプリケーションを作成します。このサンプルアプリケーションは、このチュートリアルで後述する外部認証サービスのそれぞれに使用します。

Visual Studio 2017 を起動し、スタートページで **[新しいプロジェクト]** を選択します。 または、 **[ファイル]** メニューの **[新規作成]** をポイントし、 **[プロジェクト]** をクリックします。

<!-- [![](external-authentication-services/_static/image6.png "Click to Expand the Image")](external-authentication-services/_static/image5.png) -->

**[新しいプロジェクト]** ダイアログボックスが表示されたら、 **[インストール済み]** を選択し、 **[ C#ビジュアル]** を展開します。 **[ビジュアルC# ]** で **[Web]** を選択します。 プロジェクトテンプレートの一覧で、 **[ASP.NET Web Application (.Net Framework)]** を選択します。 プロジェクトの名前を入力し、[ **OK]** をクリックします。

[![](external-authentication-services/_static/image71.png "Click to Expand the Image")](external-authentication-services/_static/image71.png)

**新しい ASP.NET プロジェクト**が表示されたら、 **[シングルページアプリケーション]** テンプレートを選択し、 **[プロジェクトの作成]** をクリックします。

[![](external-authentication-services/_static/image72.png "Click to Expand the Image")](external-authentication-services/_static/image72.png)

Visual Studio 2017 によってプロジェクトが作成されるまで待ちます。

<!-- [![](external-authentication-services/_static/image12.png "Click to Expand the Image")](external-authentication-services/_static/image11.png) -->

Visual Studio 2017 がプロジェクトの作成を完了したら、**アプリ\_** の [開始] フォルダーにある*Startup.Auth.cs*ファイルを開きます。

最初にプロジェクトを作成するときに、 *Startup.Auth.cs*ファイルで外部認証サービスが有効になっていません。次に、コードがどのようなものかを示します。ここでは、ASP.NET アプリケーションで Microsoft アカウント、Twitter、Facebook、または Google 認証を使用するために、外部認証サービスと関連する設定を有効にする場所のセクションを強調表示しています。

[!code-csharp[Main](external-authentication-services/samples/sample1.cs)]

F5 キーを押して web アプリケーションをビルドおよびデバッグすると、ログイン画面が表示され、外部認証サービスが定義されていないことがわかります。

[![](external-authentication-services/_static/image73.png "Click to Expand the Image")](external-authentication-services/_static/image73.png)

以下のセクションでは、Visual Studio 2017 の ASP.NET で提供されている各外部認証サービスを有効にする方法について説明します。

<a id="FACEBOOK"></a>
## <a name="enabling-facebook-authentication"></a>Facebook 認証を有効にする

Facebook 認証を使用するには、Facebook 開発者アカウントを作成する必要があります。また、プロジェクトで機能するためには、Facebook のアプリケーション ID とシークレットキーが必要です。 Facebook 開発者アカウントを作成し、アプリケーション ID とシークレットキーを取得する方法の詳細については、「 [https://go.microsoft.com/fwlink/?LinkID=252166](https://go.microsoft.com/fwlink/?LinkID=252166)」を参照してください。

アプリケーション ID とシークレットキーを取得したら、次の手順に従って、web アプリケーションの Facebook 認証を有効にします。

1. プロジェクトが Visual Studio 2017 で開かれている場合は、 *Startup.Auth.cs*ファイルを開きます。

2. コードの [Facebook 認証] セクションを探します。

    [!code-csharp[Main](external-authentication-services/samples/sample2.cs)]
3. 強調表示されているコード行のコメントを解除し、アプリケーション ID とシークレットキーを追加するには、&quot;//&quot; 文字を削除します。 これらのパラメーターを追加したら、プロジェクトを再コンパイルできます。

    [!code-csharp[Main](external-authentication-services/samples/sample3.cs)]
4. F5 キーを押して web ブラウザーで web アプリケーションを開くと、Facebook が外部認証サービスとして定義されていることがわかります。

    [![](external-authentication-services/_static/image74.png "Click to Expand the Image")](external-authentication-services/_static/image74.png)
5. **Facebook**のボタンをクリックすると、ブラウザーが facebook のログインページにリダイレクトされます。

    [![](external-authentication-services/_static/image22.png "Click to Expand the Image")](external-authentication-services/_static/image21.png)
6. Facebook の資格情報を入力して **[ログイン]** をクリックすると、web ブラウザーが web アプリケーションにリダイレクトされます。これにより、facebook アカウントに関連付ける**ユーザー名**の入力が求められます。

    [![](external-authentication-services/_static/image24.png "Click to Expand the Image")](external-authentication-services/_static/image23.png)
7. ユーザー名を入力して **[サインアップ]** ボタンをクリックすると、web アプリケーションに Facebook アカウントの既定の**ホームページ**が表示されます。

    [![](external-authentication-services/_static/image26.png "Click to Expand the Image")](external-authentication-services/_static/image25.png)

<a id="GOOGLE"></a>
## <a name="enabling-google-authentication"></a>Google 認証を有効にする

Google 認証を使用するには、Google developer アカウントを作成する必要があります。また、プロジェクトで機能するためには、Google のアプリケーション ID とシークレットキーが必要です。 Google developer アカウントを作成し、アプリケーション ID とシークレットキーを取得する方法の詳細については、「 [https://developers.google.com](https://developers.google.com)」を参照してください。

Web アプリケーションの Google 認証を有効にするには、次の手順に従います。

1. プロジェクトが Visual Studio 2017 で開かれている場合は、 *Startup.Auth.cs*ファイルを開きます。

2. コードの [Google authentication] セクションを探します。

    [!code-csharp[Main](external-authentication-services/samples/sample4.cs)]
3. 強調表示されているコード行のコメントを解除し、アプリケーション ID とシークレットキーを追加するには、&quot;//&quot; 文字を削除します。 これらのパラメーターを追加したら、プロジェクトを再コンパイルできます。

    [!code-csharp[Main](external-authentication-services/samples/sample5.cs)]
4. F5 キーを押して web ブラウザーで web アプリケーションを開くと、Google が外部認証サービスとして定義されていることがわかります。

    [![](external-authentication-services/_static/image75.png "Click to Expand the Image")](external-authentication-services/_static/image75.png)
5. **Google**ボタンをクリックすると、ブラウザーは google ログインページにリダイレクトされます。

    [![](external-authentication-services/_static/image32.png "Click to Expand the Image")](external-authentication-services/_static/image31.png)
6. Google の資格情報を入力して **[サインイン]** をクリックすると、google アカウントにアクセスするためのアクセス許可が web アプリケーションにあるかどうかを確認するメッセージが表示されます。

    [![](external-authentication-services/_static/image34.png "Click to Expand the Image")](external-authentication-services/_static/image33.png)
7. [**同意**する] をクリックすると、web ブラウザーが web アプリケーションにリダイレクトされます。これにより、Google アカウントに関連付ける**ユーザー名**の入力が求められます。

    [![](external-authentication-services/_static/image36.png "Click to Expand the Image")](external-authentication-services/_static/image35.png)
8. ユーザー名を入力して **[サインアップ]** ボタンをクリックすると、web アプリケーションに Google アカウントの既定の**ホームページ**が表示されます。

    [![](external-authentication-services/_static/image38.png "Click to Expand the Image")](external-authentication-services/_static/image37.png)

<a id="MICROSOFT"></a>
## <a name="enabling-microsoft-authentication"></a>Microsoft 認証を有効にする

Microsoft 認証では、開発者アカウントを作成する必要があり、機能するためにはクライアント ID とクライアントシークレットが必要です。 Microsoft 開発者アカウントを作成し、クライアント ID とクライアントシークレットを取得する方法の詳細については、「 [https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070)」を参照してください。

コンシューマーキーとコンシューマーシークレットを取得したら、次の手順に従って、web アプリケーションの Microsoft 認証を有効にします。

1. プロジェクトが Visual Studio 2017 で開かれている場合は、 *Startup.Auth.cs*ファイルを開きます。

2. コードの [Microsoft 認証] セクションを探します。

    [!code-csharp[Main](external-authentication-services/samples/sample6.cs)]
3. 強調表示されているコード行のコメントを解除し、クライアント ID とクライアントシークレットを追加するには、&quot;//&quot; 文字を削除します。 これらのパラメーターを追加したら、プロジェクトを再コンパイルできます。

    [!code-csharp[Main](external-authentication-services/samples/sample7.cs)]
4. F5 キーを押して web ブラウザーで web アプリケーションを開くと、Microsoft が外部認証サービスとして定義されていることがわかります。

    [![](external-authentication-services/_static/image42.png "Click to Expand the Image")](external-authentication-services/_static/image41.png)
5. **[Microsoft]** ボタンをクリックすると、ブラウザーが microsoft ログインページにリダイレクトされます。

    [![](external-authentication-services/_static/image44.png "Click to Expand the Image")](external-authentication-services/_static/image43.png)
6. Microsoft の資格情報を入力して **[サインイン]** をクリックすると、web アプリケーションに Microsoft アカウントにアクセスするためのアクセス許可があるかどうかを確認するメッセージが表示されます。

    [![](external-authentication-services/_static/image46.png "Click to Expand the Image")](external-authentication-services/_static/image45.png)
7. **[はい]** をクリックすると、web ブラウザーが web アプリケーションにリダイレクトされ、Microsoft アカウントに関連付ける**ユーザー名**の入力が求められます。

    [![](external-authentication-services/_static/image48.png "Click to Expand the Image")](external-authentication-services/_static/image47.png)
8. ユーザー名を入力して **[サインアップ]** ボタンをクリックすると、web アプリケーションに Microsoft アカウントの既定の**ホームページ**が表示されます。

    [![](external-authentication-services/_static/image50.png "Click to Expand the Image")](external-authentication-services/_static/image49.png)

<a id="TWITTER"></a>
## <a name="enabling-twitter-authentication"></a>Twitter 認証を有効にする

Twitter 認証では、開発者アカウントを作成する必要があり、機能するためにコンシューマーキーとコンシューマーシークレットが必要です。 Twitter 開発者アカウントを作成し、コンシューマーキーとコンシューマーシークレットを取得する方法の詳細については、「 [https://go.microsoft.com/fwlink/?LinkID=252166](https://go.microsoft.com/fwlink/?LinkID=252166)」を参照してください。

コンシューマーキーとコンシューマーシークレットを取得したら、次の手順に従って、web アプリケーションの Twitter 認証を有効にします。

1. プロジェクトが Visual Studio 2017 で開かれている場合は、 *Startup.Auth.cs*ファイルを開きます。

2. コードの [Twitter 認証] セクションを探します。

    [!code-csharp[Main](external-authentication-services/samples/sample8.cs)]
3. 強調表示されているコード行のコメントを解除し、コンシューマーキーとコンシューマーシークレットを追加するには、&quot;//&quot; 文字を削除します。 これらのパラメーターを追加したら、プロジェクトを再コンパイルできます。

    [!code-csharp[Main](external-authentication-services/samples/sample9.cs)]
4. F5 キーを押して web ブラウザーで web アプリケーションを開くと、Twitter が外部認証サービスとして定義されていることがわかります。

    [![](external-authentication-services/_static/image54.png "Click to Expand the Image")](external-authentication-services/_static/image53.png)
5. **Twitter**ボタンをクリックすると、ブラウザーが twitter ログインページにリダイレクトされます。

    [![](external-authentication-services/_static/image56.png "Click to Expand the Image")](external-authentication-services/_static/image55.png)
6. Twitter の資格情報を入力して **[アプリの承認]** をクリックすると、web ブラウザーが web アプリケーションにリダイレクトされます。これにより、twitter アカウントに関連付ける**ユーザー名**の入力が求められます。

    [![](external-authentication-services/_static/image58.png "Click to Expand the Image")](external-authentication-services/_static/image57.png)
7. ユーザー名を入力して **[サインアップ]** ボタンをクリックすると、web アプリケーションに Twitter アカウントの既定の**ホームページ**が表示されます。

    [![](external-authentication-services/_static/image60.png "Click to Expand the Image")](external-authentication-services/_static/image59.png)

<a id="MOREINFO"></a>
## <a name="additional-information"></a>追加情報

OAuth および OpenID を使用するアプリケーションの作成の詳細については、次の Url を参照してください。

- [https://go.microsoft.com/fwlink/?LinkID=252166](https://go.microsoft.com/fwlink/?LinkID=252166)
- [https://go.microsoft.com/fwlink/?LinkID=243995](https://go.microsoft.com/fwlink/?LinkID=243995)

<a id="COMBINE"></a>
### <a name="combining-external-authentication-services"></a>外部認証サービスの組み合わせ

柔軟性を高めるために、複数の外部認証サービスを同時に定義することができます。これにより、web アプリケーションのユーザーは、有効な外部認証サービスのいずれかのアカウントを使用できるようになります。

[![](external-authentication-services/_static/image62.png "Click to Expand the Image")](external-authentication-services/_static/image61.png)

<a id="FQDN"></a>
### <a name="configure-iis-express-to-use-a-fully-qualified-domain-name"></a>完全修飾ドメイン名を使用するように IIS Express を構成する

一部の外部認証プロバイダーでは、`http://localhost:port/`などの HTTP アドレスを使用したアプリケーションのテストはサポートされていません。 この問題を回避するには、ホストファイルに静的完全修飾ドメイン名 (FQDN) マッピングを追加し、テスト/デバッグで FQDN を使用するように Visual Studio 2017 でプロジェクトオプションを構成します。 そのためには、次の手順を実行してください。

- ホストファイルをマッピングする静的 FQDN を追加します。

  1. Windows で管理者特権でのコマンドプロンプトを開きます。
  2. 次のコマンドを入力します。

      <kbd>メモ帳%WinDir%\system32\drivers\etc\hosts</kbd>
  3. HOSTS ファイルに次のようなエントリを追加します。

      <kbd>127.0.0.1 www.wingtiptoys.com</kbd>
  4. ホストファイルを保存して閉じます。

- FQDN を使用するように Visual Studio プロジェクトを構成します。

  1. プロジェクトが Visual Studio 2017 で開かれている場合は、 **[プロジェクト]** メニューをクリックし、プロジェクトのプロパティを選択します。 たとえば、 **[WebApplication1 Properties]** を選択します。
  2. **[Web]** タブを選択します。
  3. <strong>プロジェクト Url</strong>の FQDN を入力します。 たとえば、ホストファイルに追加した FQDN マッピングである場合は、 <kbd><http://www.wingtiptoys.com></kbd>を入力します。

- アプリケーションの FQDN を使用するように IIS Express を構成します。

    1. Windows で管理者特権でのコマンドプロンプトを開きます。
    2. 次のコマンドを入力して、IIS Express フォルダーに移動します。

        <kbd>cd/d &quot;%ProgramFiles%\IIS Express&quot;</kbd>
    3. 次のコマンドを入力して、アプリケーションに FQDN を追加します。

        <kbd>appcmd.exe set config-section: system.string/sites/+&quot;[name = ' WebApplication1 ']. bindings.[protocol = ' http ', bindingInformation = ' *:80:/commit '] の&quot;: apphost</kbd>

  ここで、 **WebApplication1**はプロジェクトの名前です。 **bindingInformation**には、テストに使用するポート番号と FQDN が含まれています。

<a id="OBTAIN"></a>
### <a name="how-to-obtain-your-application-settings-for-microsoft-authentication"></a>Microsoft 認証のアプリケーション設定を取得する方法

アプリケーションを Windows Live for Microsoft 認証にリンクすることは、簡単なプロセスです。 アプリケーションを Windows Live にまだリンクしていない場合は、次の手順を実行します。

1. [https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070)を参照し、メッセージが表示されたら、Microsoft アカウント名とパスワードを入力し、 **[サインイン]** をクリックします。

   <!--  [![](external-authentication-services/_static/image64.png "Click to Expand the Image")](external-authentication-services/_static/image63.png) -->
2. **[アプリの追加]** を選択し、メッセージが表示されたらアプリケーションの名前を入力して、 **[作成]** をクリックします。

    [![](external-authentication-services/_static/image79.png "Click to Expand the Image")](external-authentication-services/_static/image79.png)
3. **[名前]** でアプリを選択すると、アプリケーションのプロパティページが表示されます。

4. アプリケーションのリダイレクトドメインを入力します。 **アプリケーション ID**をコピーし、 **[アプリケーションシークレット]** で **[パスワードの生成]** を選択します。 表示されたパスワードをコピーします。 アプリケーション ID とパスワードは、クライアント ID とクライアントシークレットです。 [ **Ok]** を選択し、 **[保存]** をクリックします。

    [![](external-authentication-services/_static/image77.png "Click to Expand the Image")](external-authentication-services/_static/image77.png)

<a id="DISABLE"></a>
### <a name="optional-disable-local-registration"></a>省略可能: ローカル登録を無効にする

現在の ASP.NET ローカル登録機能では、自動プログラム (ボット) によるメンバーアカウントの作成が妨げられることはありません。たとえば、 [CAPTCHA](../../../web-pages/overview/security/16-adding-security-and-membership.md)のようなボット防止と検証テクノロジを使用します。 このため、ログインページでローカルログインフォームと登録リンクを削除する必要があります。 これを行うには、プロジェクトの [ *\_のログイン*] ページを開き、[ローカルログイン] パネルと [登録] リンクの行をコメントアウトします。 結果のページは、次のコードサンプルのようになります。

[!code-html[Main](external-authentication-services/samples/sample10.html)]

[ローカルログイン] パネルと登録リンクが無効になると、ログインページには、有効にした外部認証プロバイダーのみが表示されます。

[![](external-authentication-services/_static/image70.png "Click to Expand the Image")](external-authentication-services/_static/image69.png)
