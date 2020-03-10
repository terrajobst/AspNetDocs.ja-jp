---
uid: identity/overview/getting-started/developing-aspnet-apps-with-windows-azure-active-directory
title: Azure Active Directory を使用した ASP.NET アプリの開発-ASP.NET 4.x
author: Rick-Anderson
description: Azure Active Directory 用の Microsoft ASP.NET ツールを使用すると、Azure でホストされている web アプリケーションの認証を簡単に有効にすることができます。 Azure 事前を使用できます...
ms.author: riande
ms.date: 08/14/2014
ms.assetid: 457d7eaf-ee76-4ceb-9082-c7c1721435ad
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/getting-started/developing-aspnet-apps-with-windows-azure-active-directory
msc.type: authoredcontent
ms.openlocfilehash: 28425ea8d1312dfc6e14df9677396f2cbcf6f16d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78471742"
---
# <a name="developing-aspnet-apps-with-azure-active-directory"></a>Azure Active Directory を使った ASP.NET アプリの開発

[Rick Anderson](https://twitter.com/RickAndMSFT)

Azure Active Directory 用の Microsoft ASP.NET ツールを使用すると、 [Azure](https://www.windowsazure.com/home/features/web-sites/)でホストされている web アプリの認証を簡単に行うことができます。 Azure 認証を使用すると、社内の Active Directory、または独自のカスタム Azure Active Directory ドメインで作成されたユーザーから同期された会社のアカウントで、組織からの Office 365 ユーザーを認証できます。 Windows Azure 認証を有効にすると、単一の[Azure Active Directory](https://docs.microsoft.com/azure/active-directory/)テナントを使用してユーザーを認証するようにアプリケーションが構成されます。

このチュートリアルでは、 [Azure Active Directory](https://msdn.microsoft.com/library/azure/mt168838.aspx) (Azure AD) を使用したサインオン用に構成された ASP.NET アプリケーションを作成する方法について説明します。 また、Graph API を呼び出して、現在サインインしているユーザーに関する情報を取得する方法と、Azure にアプリケーションをデプロイする方法についても説明します。

## <a name="prerequisites"></a>前提条件

1. Web または[Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)[の Visual Studio Express 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013#d-2013-express) 。
2. [Visual Studio 2013 Update 4](https://www.microsoft.com/download/details.aspx?id=44921) -Update 3 以降が必要です。
3. Azure アカウント。 まだアカウントをお持ちでない場合は、無料試用版を[クリックし](https://azure.microsoft.com/pricing/free-trial/)てください。

## <a name="add-a-global-administrator-to-your-active-directory"></a>Active Directory にグローバル管理者を追加する

1. [Azure 管理ポータル](https://manage.windowsazure.com/)にサインインします。
2. すべての Azure アカウントには**既定のディレクトリ**が含まれています。これをクリックし、ページの上部にある **[ユーザー]** タブをクリックします (下図を参照)。
3. [ユーザーの追加] をクリックします。
    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image1.png)
4. **グローバル管理者**ロールを持つ新しいユーザーを作成します。 上部のメニューの **[ユーザー]** をクリックし、コマンドバーの **[ユーザーの追加]** ボタンをクリックします。
5. **[ユーザーの追加]** ダイアログボックスで、新しいユーザーの名前を入力し、右矢印をクリックします。

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image2.png)
6. ユーザー名を入力し、ロールを **[グローバル管理者]** に設定します。 グローバル管理者には、パスワードの回復のために連絡用電子メールアドレスが必要です。 終了したら、右矢印をクリックします。

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image3.png)
7. ダイアログの次のページで、 **[作成]** をクリックします。 新しいユーザーの一時パスワードが作成され、ダイアログに表示されます。

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image4.png)

   パスワードを保存します。最初のログイン後にパスワードを変更する必要があります。 次の図は、新しい管理者アカウントを示しています。 このページに示されている Microsoft アカウントではなく、アプリにログインするには Azure Active Directory を使用する必要があります。

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image5.png)

## <a name="create-an-aspnet-application"></a>ASP.NET アプリケーションを作成する

次の手順では、 [Web 用に 2013 Visual Studio Express](https://www.microsoft.com/download/details.aspx?id=40747)を使用し、 [Visual Studio 2013 Update 3](https://www.microsoft.com/download/details.aspx?id=43721)が必要です。

1. Visual Studio で、 **[ファイル]** 、 **[新しいプロジェクト]** の順にクリックします。 **[新しいプロジェクト]** ダイアログで、左側のC#メニューから Visual Web プロジェクト を選択し、 **[OK]** をクリックします。 また、アプリケーションの機能を必要としない場合は、[ **Application Insights をプロジェクトに追加**する] チェックボックスをオフにすることもできます。
2. **[New ASP.NET プロジェクト]** ダイアログボックスで **[MVC]** を選択し、 **[認証の変更]** をクリックします。

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image6.png)
3. **[認証の変更]** ダイアログで、 **[組織アカウント]** を選択します。 これらのオプションを使用すると、アプリケーションを自動的に Azure AD に登録できるだけでなく、アプリケーションを Azure AD と統合するように自動的に構成することもできます。 **[認証の変更]** ダイアログボックスを使用してアプリケーションを登録および構成する必要はありませんが、これははるかに簡単になります。 たとえば、Visual Studio 2012 を使用している場合は、アプリケーションを Azure 管理ポータルに手動で登録し、その構成を Azure AD と統合するように更新することもできます。
   ドロップダウンメニューで、 **[クラウド-単一組織]** と [**シングルサインオン]** を選択し、[ディレクトリデータの読み取り] を選択します。 Azure AD ディレクトリのドメイン (次の図を参照) *aricka0yahoo.onmicrosoft.com*を入力し、[ **OK]** をクリックします。 ドメイン名は、azure portal の既定のディレクトリの [ドメイン] タブから取得できます (次の図を参照)。

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image7.png)

   次の図は、Azure portal のドメイン名を示しています。

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image8.png)

    > [!NOTE]
    > 必要に応じて、[**その他のオプション]** をクリックして Azure AD に登録されるアプリケーション ID URI を構成することもできます。 アプリ ID URI は、アプリケーションの一意の識別子であり、Azure AD に登録され、アプリケーションが Azure AD との通信時に自身を識別するために使用します。 アプリ ID URI および登録済みアプリケーションのその他のプロパティの詳細については、[このトピック](https://msdn.microsoft.com/library/azure/dn499820.aspx#BKMK_Registering)を参照してください。 [アプリ ID URI] フィールドの下にあるチェックボックスをオンにすると、同じアプリ ID URI を使用する Azure AD の既存の登録を上書きすることもできます。
4. **[OK]** をクリックすると、サインインダイアログが表示され、(サブスクリプションに関連付けられている Microsoft アカウントではなく) グローバル管理者アカウントを使用してサインインする必要があります。 以前に新しい管理者アカウントを作成した場合は、パスワードを変更してから、新しいパスワードを使用してもう一度サインインする必要があります。

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image9.png)
5. 認証が正常に完了すると、**新しい [ASP.NET プロジェクト**] ダイアログボックスに、認証の選択 (**組織**) と、新しいアプリケーションを登録するディレクトリ (下の図の*aricka0yahoo.onmicrosoft.com* ) が表示されます。 この情報の下にある **[クラウド内のホスト]** チェックボックスをオンにします。 このチェックボックスをオンにすると、プロジェクトは Azure web アプリとしてプロビジョニングされ、後で簡単に発行できるようになります。 **[OK]** をクリックします。

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image10.png)
6. 自動生成されたサイト名とリージョンを使用して、 **[Azure Web サイトの構成]** ダイアログボックスが表示されます。 また、ダイアログで現在サインインしているアカウントにも注意してください。 このアカウントが、Azure サブスクリプションがアタッチされているアカウント (通常は Microsoft アカウント) であることを確認する必要があります。

    > [!NOTE]
    > このプロジェクトにはデータベースが必要です。 既存のデータベースのいずれかを選択するか、新しいデータベースを作成する必要があります。 データベースは、少数の認証構成データを格納するためにローカルデータベースファイルが既に使用されているため、必要です。 アプリケーションを Azure Web サイトにデプロイする場合、このデータベースはデプロイでパッケージ化されていないため、クラウドでアクセス可能なデータベースを選択する必要があります。 **[OK]** をクリックします。

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image11.png)
7. プロジェクトが作成され、認証オプションと web アプリのオプションがプロジェクトで自動的に構成されます。 このプロセスが完了したら、 **^ F5**キーを押してプロジェクトをローカルで実行します。 組織のアカウントを使用してサインインする必要があります。 前の手順で作成したアカウントのユーザー名とパスワードを入力し、 **[サインイン]** をクリックします。

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image12.png)
8. サインインに成功すると、ASP.NET サイトには、ページの右上隅にユーザー名が表示され、認証済みであることが示されます。

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image13.png)

   エラーが発生した場合: 値を null または空にすることはできません。 パラメーター名: linkText ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image14.png)

   チュートリアルの最後にある「[デバッグ](#dbg)」セクションを参照してください。

## <a name="basics-of-the-graph-api"></a>Graph API の基礎

[Graph API](https://msdn.microsoft.com/library/azure/hh974476.aspx)は、Azure AD ディレクトリ内のオブジェクトに対して CRUD などの操作を実行するために使用されるプログラムインターフェイスです。 Visual Studio 2013 で新しいプロジェクトを作成するときに認証に組織アカウントオプションを選択した場合、アプリケーションは Graph API を呼び出すように既に構成されています。 このセクションでは、Graph API のしくみを簡単に説明します。

1. 実行中のアプリケーションで、ページの右上にあるサインインしているユーザーの名前をクリックします。 これにより、[ユーザープロファイル] ページが表示されます。これは、Home コントローラーのアクションです。 このテーブルには、前に作成した管理者アカウントに関するユーザー情報が含まれていることがわかります。 この情報はディレクトリに格納され、ページが読み込まれるときにこの情報を取得するために Graph API が呼び出されます。

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image15.png)
2. Visual Studio に戻り、 **Controllers**フォルダーを展開して、 **HomeController.cs**ファイルを開きます。 トークンを取得してから Graph API を呼び出すためのコードを含む**UserProfile ()** アクションが表示されます。 このコードは次のように重複しています。

    [!code-csharp[Main](developing-aspnet-apps-with-windows-azure-active-directory/samples/sample1.cs?highlight=22)]

    Graph API を呼び出すには、最初にトークンを取得する必要があります。 トークンを取得するときは、その文字列値を、Graph API への後続のすべての要求の Authorization ヘッダーに追加する必要があります。 上記のコードのほとんどは、トークンを取得するための Azure AD 認証の詳細を処理し、トークンを使用して Graph API を呼び出し、その応答をビューに表示できるように変換します。

    説明の最も関連性の高い部分は、次の強調表示されている行を `UserProfile profile = JsonConvert.DeserializeObject<UserProfile>(responseString);`です。 この行は、JSON 応答から逆シリアル化され、ビューに表示されるユーザーの名前を表します。

    HttpClient を使用して Graph API を呼び出し、生データを自分で処理することができますが、簡単な方法は、 [NuGet から入手できる Graph クライアントライブラリ](http://www.nuget.org/packages/Microsoft.Azure.ActiveDirectory.GraphClient/)を使用する方法です。 クライアントライブラリは、未加工の HTTP 要求と返されたデータの変換を処理し、.NET 環境での Graph API の操作をより簡単にします。 GitHub の関連 Graph API コードサンプルを参照してください[。](https://github.com/AzureADSamples)

## <a name="deploy-the-application-to-azure"></a>Azure にアプリケーションをデプロイする

次の手順は、アプリケーションを Azure にデプロイする方法を示しています。 前の手順では、新しいプロジェクトを Azure の web アプリに接続しました。そのため、いくつかの手順で発行することができます。

1. Visual Studio で、プロジェクトを右クリックし、 **[発行]** を選択します。 各設定が既に構成されている場合は、 **[Web の発行]** ダイアログボックスが表示されます。 **[次へ]** ボタンをクリックして、 **[設定]** ページに戻ります。 認証を求めるメッセージが表示される場合があります。前に作成した組織アカウントではなく、Azure サブスクリプションアカウント (通常は Microsoft アカウント) を使用して認証するようにしてください。

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image16.png)
2. **[組織の認証を有効にする]** オプションをオンにします。 **[ドメイン]** フィールドに、ディレクトリのドメインを入力します。 **[アクセスレベル]** ドロップダウンで、[**シングルサインオン]、[ディレクトリデータの読み取り**] の順に選択します。 以前に使用したデータベースは、 **[データベース]** セクションに既に設定されていることがわかります。 **[発行]** をクリックします。

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image17.png)
3. Web サイトのデプロイが開始され、新しいブラウザーウィンドウが表示されます。 ディレクトリに対してもう一度認証を求めるメッセージが表示される場合があります。 認証が完了すると、Azure で新しく公開された web サイトにリダイレクトされます。

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image18.png)

<a id="dbg"></a>
## <a name="debugging-the-app"></a>アプリのデバッグ

次のエラーが表示される場合: 値を null または空にすることはできません。 パラメーター名: linkText

![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image19.png)

*Views\Shared\\_LoginPartial*ファイル内のコードを次のコードに置き換えます。

[!code-cshtml[Main](developing-aspnet-apps-with-windows-azure-active-directory/samples/sample2.cshtml?highlight=1-8,15-16)]

アプリを実行した後、ログインしているユーザーに "Null ユーザー" と表示されている場合は、サインアウトし、前に作成した Active Directory アカウントを使用してもう一度サインインします。

このチュートリアルでは、Rick Rainey の詳細について説明します。 [Azure AD を使用した Azure Websites と組織認証](http://rickrainey.com/2014/08/19/deep-dive-azure-websites-and-organizational-authentication-using-azure-ad/)です。

## <a name="more-information"></a>詳細情報

- [詳細: Azure AD を使用した Azure Websites と組織認証](http://rickrainey.com/2014/08/19/deep-dive-azure-websites-and-organizational-authentication-using-azure-ad/)
- [Azure AD Graph API の概要](https://msdn.microsoft.com/library/azure/hh974476.aspx)
- [Azure AD での認証シナリオ](https://msdn.microsoft.com/library/azure/dn499820.aspx)
- [GitHub の Azure AD コードサンプル](https://github.com/AzureADSamples)
