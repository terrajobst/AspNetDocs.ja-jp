---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/single-sign-on
title: シングルサインオン (Azure を使用した実際のクラウドアプリの構築) |Microsoft Docs
author: MikeWasson
description: Azure 電子ブックを使用した実際のクラウドアプリの構築は、Scott Guthrie によって開発されたプレゼンテーションに基づいています。 13のパターンとベストプラクティスについて説明します。
ms.author: riande
ms.date: 06/12/2014
ms.assetid: 7d82d5e9-0619-4f22-9e03-32a6d52940a5
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/single-sign-on
msc.type: authoredcontent
ms.openlocfilehash: 7e32f444dc38132296cffd45ac658f5abf51f314
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74585278"
---
# <a name="single-sign-on-building-real-world-cloud-apps-with-azure"></a>シングルサインオン (Azure を使用した実際のクラウドアプリの構築)

[Mike Wasson](https://github.com/MikeWasson)、 [Rick Anderson]((https://twitter.com/RickAndMSFT))、 [Tom Dykstra](https://github.com/tdykstra)

[修正 It プロジェクトをダウンロード](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)するか[、電子書籍をダウンロード](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)します

> Azure 電子ブック**を使用した実際のクラウドアプリの構築**は、Scott Guthrie によって開発されたプレゼンテーションに基づいています。 ここでは、クラウド用の web アプリの開発を成功させるのに役立つ13のパターンとプラクティスについて説明します。 電子書籍の詳細については、[最初の章](introduction.md)を参照してください。

クラウドアプリの開発時には、多くのセキュリティの問題について検討する必要がありますが、このシリーズではシングルサインオンのみに注目します。 "私は主に私の会社の従業員のためにアプリを構築しています。これらのアプリをクラウドでホストしても、ファイアウォール内でホストされているアプリを実行しているときに、社内環境で使用しているのと同じセキュリティモデルを使用できるようにするにはどうすればよいですか? " このシナリオを有効にする方法の1つとして、Azure Active Directory (Azure AD) が挙げられます。 Azure AD を使用すると、企業の基幹業務 (LOB) アプリをインターネット経由で利用できるようになり、これらのアプリをビジネスパートナーも使用できるようになります。

## <a name="introduction-to-azure-ad"></a>Azure AD の概要

[Azure AD](https://docs.microsoft.com/azure/active-directory/)はクラウドで[Active Directory](https://msdn.microsoft.com/library/windows/desktop/aa746492.aspx)を提供します。 主な機能は次のとおりです。

- オンプレミスの Active Directory と統合されます。
- これにより、アプリでのシングルサインオンが可能になります。
- [SAML](http://en.wikipedia.org/wiki/SAML_2.0)、 [ws-atomictransaction](http://en.wikipedia.org/wiki/WS-Federation)、 [OAuth 2.0](http://oauth.net/2/)などのオープン標準をサポートしています。
- エンタープライズ[グラフ REST API](https://msdn.microsoft.com/library/hh974476.aspx)がサポートされています。

たとえば、従業員がイントラネットアプリにサインオンできるようにするために使用するオンプレミスの Windows Server Active Directory 環境があるとします。

![](single-sign-on/_static/image1.png)

クラウド内にディレクトリを作成すると、どのような Azure AD が可能になります。 これは無料の機能であり、簡単に設定できます。

オンプレミスの Active Directory から完全に独立している可能性があります。任意のユーザーを追加して、インターネットアプリで認証することができます。

![Windows Azure Active Directory](single-sign-on/_static/image2.png)

または、オンプレミスの AD と統合することもできます。

![AD と WAAD の統合](single-sign-on/_static/image3.png)

これで、オンプレミスで認証できるすべての従業員が、インターネット経由でも認証できるようになりました。ファイアウォールを開放したり、新しいサーバーをデータセンターにデプロイしたりする必要はありません。 現在お持ちの既存の Active Directory 環境を引き続き活用し、内部アプリのシングルサインオン機能を利用することができます。

AD と Azure AD の間でこの接続を確立すると、web アプリとモバイルデバイスでクラウド内の従業員を認証できるようになります。また、Office 365、SalesForce.com、Google apps などのサードパーティ製アプリを有効にして、従業員の資格情報。 Office 365 を使用している場合は、Azure AD で既にセットアップされています。これは、Office 365 が認証と承認に Azure AD を使用するためです。

![サードパーティ製アプリ](single-sign-on/_static/image4.png)

この方法の利点は、組織がユーザーを追加または削除した場合や、ユーザーがパスワードを変更した場合は、現在オンプレミス環境で使用しているのと同じプロセスを使用することです。 オンプレミスの AD の変更はすべて、自動的にクラウド環境に反映されます。

会社がを使用している場合、または Office 365 に移行している場合は、Office 365 で認証に Azure AD を使用するため、Azure AD が自動的に設定されます。 これにより、Office 365 が使用するのと同じ認証を、独自のアプリで簡単に使用できるようになります。

## <a name="set-up-an-azure-ad-tenant"></a>Azure AD テナントを設定する

Azure AD ディレクトリは Azure AD[テナント](https://technet.microsoft.com/library/jj573650.aspx)と呼ばれ、テナントの設定は非常に簡単です。 概念を説明するために Azure 管理ポータルでどのように行われるかについて説明しますが、他のポータル関数と同様に、スクリプトまたは管理 API を使用して行うこともできます。

管理ポータルで、[Active Directory] タブをクリックします。

![ポータルでの WAAD](single-sign-on/_static/image5.png)

Azure アカウント用に1つの Azure AD テナントが自動的に作成されます。ページの下部にある **[追加]** ボタンをクリックすると、追加のディレクトリを作成できます。 たとえば、テスト環境用に1つ、運用環境用に1つを使用することができます。 新しいディレクトリの名前については、慎重に検討してください。 ディレクトリの名前を使用した後で、いずれかのユーザーに対して名前を再び使用すると、混乱を招く可能性があります。

![ディレクトリを追加する](single-sign-on/_static/image6.png)

ポータルでは、この環境内でのユーザーの作成、削除、管理を完全にサポートしています。 たとえば、ユーザーを追加するには、 **[ユーザー]** タブにアクセスし、 **[ユーザーの追加]** ボタンをクリックします。

![[ユーザーの追加] ボタン](single-sign-on/_static/image7.png)

![[ユーザーの追加] ダイアログ](single-sign-on/_static/image8.png)

このディレクトリにのみ存在する新しいユーザーを作成したり、このディレクトリに Microsoft アカウントをユーザーとして登録したり、このディレクトリ内のユーザーとして別の Azure AD ディレクトリのユーザーを登録したりすることができます。 (実際のディレクトリでは、既定のドメインは ContosoTest.onmicrosoft.com です。 また、contoso.com のように、自分で選択したドメインを使用することもできます)。

![ユーザーの種類](single-sign-on/_static/image9.png)

![[ユーザーの追加] ダイアログ](single-sign-on/_static/image10.png)

ロールにユーザーを割り当てることができます。

![ユーザー プロファイル](single-sign-on/_static/image11.png)

アカウントは一時パスワードで作成されます。

![一時パスワード](single-sign-on/_static/image12.png)

この方法で作成したユーザーは、このクラウドディレクトリを使用して、すぐに web アプリにログインできます。

エンタープライズシングルサインオンに適しているのは、[ディレクトリの**統合**] タブです。

![[ディレクトリの統合] タブ](single-sign-on/_static/image13.png)

ディレクトリ統合を有効にして[ツールをダウンロード](https://social.technet.microsoft.com/wiki/contents/articles/19098.howto-install-the-windows-azure-active-directory-sync-tool-now-with-pictures.aspx)する場合は、組織内で既に使用している既存のオンプレミス Active Directory とこのクラウドディレクトリを同期できます。 ディレクトリに格納されているすべてのユーザーが、このクラウドディレクトリに表示されます。 クラウドアプリは、既存の Active Directory 資格情報を使用してすべての従業員を認証できるようになりました。 また、同期ツールと Azure AD 自体も無料です。

ツールは、これらのスクリーンショットからわかるように、簡単に使用できるウィザードです。 これらは完全な手順ではなく、基本的なプロセスを示す例にすぎません。 詳細な操作方法の詳細については、章の最後にある「 [resources](#resources) 」セクションのリンクを参照してください。

![WAAD 同期ツールの構成ウィザード](single-sign-on/_static/image14.png)

**[次へ]** をクリックし、Azure Active Directory の資格情報を入力します。

![WAAD 同期ツールの構成ウィザード](single-sign-on/_static/image15.png)

**[次へ]** をクリックし、オンプレミスの AD 資格情報を入力します。

![WAAD 同期ツールの構成ウィザード](single-sign-on/_static/image16.png)

**[次へ]** をクリックし、AD パスワードのハッシュをクラウドに格納するかどうかを指定します。

![WAAD 同期ツールの構成ウィザード](single-sign-on/_static/image17.png)

クラウドに格納できるパスワードハッシュは一方向のハッシュです。実際のパスワードは Azure AD に格納されません。 クラウドにハッシュを格納しない場合は、 [Active Directory フェデレーションサービス (AD FS)](https://technet.microsoft.com/library/hh831502.aspx) (ADFS) を使用する必要があります。 [ADFS を使用するかどうかを選択する際に考慮すべきその他の要素](https://technet.microsoft.com/library/jj573653.aspx)もあります。 ADFS オプションには、追加の構成手順がいくつか必要です。

クラウドにハッシュを保存することを選択した場合は完了です。 **[次へ]** をクリックすると、ツールによってディレクトリの同期が開始されます。

![WAAD 同期ツールの構成ウィザード](single-sign-on/_static/image18.png)

数分で完了します。

![WAAD 同期ツールの構成ウィザード](single-sign-on/_static/image19.png)

これは、Windows 2003 以降の組織の1つのドメインコントローラーでのみ実行する必要があります。 再起動は必要ありません。 完了すると、すべてのユーザーがクラウドに存在し、SAML、OAuth、または WS-ATOMICTRANSACTION を使用して任意の web アプリケーションまたはモバイルアプリケーションからシングルサインオンできるようになります。

Microsoft では、これがどのようにセキュリティで保護されているのかをたずねられる場合があります。 答えは "はい" です。 たとえば、 [https://microsoft.sharepoint.com/](https://microsoft.sharepoint.com/)の内部 Microsoft SharePoint サイトに移動すると、ログインを求めるメッセージが表示されます。

![Office 365 サインイン](single-sign-on/_static/image20.png)

Microsoft では ADFS が有効になっているため、Microsoft ID を入力すると、ADFS ログインページにリダイレクトされます。

![ADFS サインイン](single-sign-on/_static/image21.png)

また、内部の Microsoft AD アカウントに格納されている資格情報を入力すると、この内部アプリケーションにアクセスできるようになります。

![MS SharePoint サイト](single-sign-on/_static/image22.png)

AD サインインサーバーを使用しているのは、Azure AD が利用可能になる前に ADFS が既に設定されているが、ログインプロセスがクラウド内の Azure AD ディレクトリを経由しているためです。 重要なドキュメント、ソース管理、パフォーマンス管理ファイル、販売レポートなどをクラウドに置き、同じソリューションを使用してセキュリティを保護しています。

## <a name="create-an-aspnet-app-that-uses-azure-ad-for-single-sign-on"></a>シングルサインオンに Azure AD を使用する ASP.NET アプリを作成する

Visual Studio を使用すると、いくつかのスクリーンショットからわかるように、シングルサインオンに Azure AD を使用するアプリを簡単に作成できます。

新しい ASP.NET アプリケーション (MVC または Web フォーム) を作成する場合は、既定の認証方法が ASP.NET Identity ます。 これを Azure AD に変更するには、 **[認証の変更]** ボタンをクリックします。

![認証の変更](single-sign-on/_static/image23.png)

[組織アカウント] を選択し、ドメイン名を入力して、[シングルサインオン] を選択します。

![認証の構成ダイアログ](single-sign-on/_static/image24.png)

また、ディレクトリデータに対する読み取りアクセス許可または読み取り/書き込みアクセス許可をアプリに付与することもできます。 これを行うと、 [Azure Graph REST API](https://msdn.microsoft.com/library/windowsazure/hh974476.aspx)を使用して、ユーザーの電話番号を検索したり、オフィス内にいるかどうかを確認したり、最後にログオンしたときにその情報を確認したりすることができます。

これで作業は完了です。 Visual Studio によって Azure AD テナントの管理者の資格情報が要求され、新しいアプリケーション用のプロジェクトと Azure AD テナントの両方が構成されます。

プロジェクトを実行すると、サインインページが表示され、Azure AD ディレクトリ内のユーザーの資格情報を使用してサインインできます。

![組織アカウントのサインイン](single-sign-on/_static/image25.png)

![ログイン済み](single-sign-on/_static/image26.png)

アプリを Azure にデプロイする場合は、[**組織の認証を有効に**する] チェックボックスをオンにするだけで、もう一度 Visual Studio によってすべての構成が処理されます。

![Web 公開](single-sign-on/_static/image27.png)

これらのスクリーンショットは、Azure AD 認証を使用するアプリを構築する方法を示す完全なステップバイステップのチュートリアルであり、 [Azure Active Directory を使用した ASP.NET アプリの開発](../../../../identity/overview/getting-started/developing-aspnet-apps-with-windows-azure-active-directory.md)について説明しています。

## <a name="summary"></a>要約

この章では、Azure Active Directory、Visual Studio、および ASP.NET を使用して、組織のユーザーのインターネットアプリケーションでのシングルサインオンを簡単にセットアップできるようにしました。 ユーザーは、内部ネットワークで Active Directory を使用したサインオンに使用するのと同じ資格情報を使用して、インターネットアプリでサインオンできます。

[次の章](data-storage-options.md)では、クラウドアプリで使用できるデータストレージオプションについて説明します。

<a id="resources"></a>
## <a name="resources"></a>リソース

詳細については、次のリソースを参照してください。

- [Azure Active Directory ドキュメント](https://docs.microsoft.com/azure/active-directory/)。 Windowsazure.com サイトの Azure AD ドキュメントのポータルページです。 詳細な手順のチュートリアルについては、「**開発**」セクションを参照してください。
- [Azure Multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/)。 Azure での multi-factor authentication に関するドキュメントのポータルページです。
- [組織アカウントの認証オプション](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#orgauthoptions)。 [新しいプロジェクトの Visual Studio 2013] ダイアログボックスの Azure AD 認証オプションについて説明します。
- [Microsoft のパターンとプラクティス-フェデレーション Id パターン](https://msdn.microsoft.com/library/dn589790.aspx)。
- [HowTo: Azure Active Directory 同期ツールをインストール](https://social.technet.microsoft.com/wiki/contents/articles/19098.howto-install-the-windows-azure-active-directory-sync-tool-now-with-pictures.aspx)します。
- [Active Directory フェデレーションサービス (AD FS) 2.0 コンテンツマップ](https://social.technet.microsoft.com/wiki/contents/articles/2735.ad-fs-2-0-content-map.aspx)。 ADFS 2.0 に関するドキュメントへのリンク。
- [Windows Azure AD アプリケーションでのロールベースおよび ACL ベースの承認](https://code.msdn.microsoft.com/Role-Based-and-ACL-Based-86ad71a1)。 サンプルアプリケーション。
- [Azure Active Directory Graph API ブログ](https://blogs.msdn.com/b/aadgraphteam/)をご覧ください。
- [ハイブリッド Id インフラストラクチャでの BYOD とディレクトリの統合における Access Control](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2014/PCIT-B213#fbid=)。 Gayana Bagdasaryan による Tech Ed 2014 session video。

> [!div class="step-by-step"]
> [前へ](web-development-best-practices.md)
> [次へ](data-storage-options.md)
