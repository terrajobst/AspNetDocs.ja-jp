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
# <a name="single-sign-on-building-real-world-cloud-apps-with-azure"></a><span data-ttu-id="62381-104">シングルサインオン (Azure を使用した実際のクラウドアプリの構築)</span><span class="sxs-lookup"><span data-stu-id="62381-104">Single Sign-On (Building Real-World Cloud Apps with Azure)</span></span>

<span data-ttu-id="62381-105">[Mike Wasson](https://github.com/MikeWasson)、 [Rick Anderson]((https://twitter.com/RickAndMSFT))、 [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="62381-105">by [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson]((https://twitter.com/RickAndMSFT)), [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="62381-106">[修正 It プロジェクトをダウンロード](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)するか[、電子書籍をダウンロード](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)します</span><span class="sxs-lookup"><span data-stu-id="62381-106">[Download Fix It Project](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) or [Download E-book](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)</span></span>

> <span data-ttu-id="62381-107">Azure 電子ブック**を使用した実際のクラウドアプリの構築**は、Scott Guthrie によって開発されたプレゼンテーションに基づいています。</span><span class="sxs-lookup"><span data-stu-id="62381-107">The **Building Real World Cloud Apps with Azure** e-book is based on a presentation developed by Scott Guthrie.</span></span> <span data-ttu-id="62381-108">ここでは、クラウド用の web アプリの開発を成功させるのに役立つ13のパターンとプラクティスについて説明します。</span><span class="sxs-lookup"><span data-stu-id="62381-108">It explains 13 patterns and practices that can help you be successful developing web apps for the cloud.</span></span> <span data-ttu-id="62381-109">電子書籍の詳細については、[最初の章](introduction.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="62381-109">For information about the e-book, see [the first chapter](introduction.md).</span></span>

<span data-ttu-id="62381-110">クラウドアプリの開発時には、多くのセキュリティの問題について検討する必要がありますが、このシリーズではシングルサインオンのみに注目します。</span><span class="sxs-lookup"><span data-stu-id="62381-110">There are many security issues to think about when you're developing a cloud app, but for this series we'll focus on just one: single sign-on.</span></span> <span data-ttu-id="62381-111">"私は主に私の会社の従業員のためにアプリを構築しています。これらのアプリをクラウドでホストしても、ファイアウォール内でホストされているアプリを実行しているときに、社内環境で使用しているのと同じセキュリティモデルを使用できるようにするにはどうすればよいですか? "</span><span class="sxs-lookup"><span data-stu-id="62381-111">A question people often ask is this: "I'm primarily building apps for the employees of my company; how do I host these apps in the cloud and still enable them to use the same security model that my employees know and use in the on-premises environment when they're running apps that are hosted inside the firewall?"</span></span> <span data-ttu-id="62381-112">このシナリオを有効にする方法の1つとして、Azure Active Directory (Azure AD) が挙げられます。</span><span class="sxs-lookup"><span data-stu-id="62381-112">One of the ways we enable this scenario is called Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="62381-113">Azure AD を使用すると、企業の基幹業務 (LOB) アプリをインターネット経由で利用できるようになり、これらのアプリをビジネスパートナーも使用できるようになります。</span><span class="sxs-lookup"><span data-stu-id="62381-113">Azure AD enables you to make enterprise line-of-business (LOB) apps available over the Internet, and it enables you to make these apps available to business partners as well.</span></span>

## <a name="introduction-to-azure-ad"></a><span data-ttu-id="62381-114">Azure AD の概要</span><span class="sxs-lookup"><span data-stu-id="62381-114">Introduction to Azure AD</span></span>

<span data-ttu-id="62381-115">[Azure AD](https://docs.microsoft.com/azure/active-directory/)はクラウドで[Active Directory](https://msdn.microsoft.com/library/windows/desktop/aa746492.aspx)を提供します。</span><span class="sxs-lookup"><span data-stu-id="62381-115">[Azure AD](https://docs.microsoft.com/azure/active-directory/) provides [Active Directory](https://msdn.microsoft.com/library/windows/desktop/aa746492.aspx) in the cloud.</span></span> <span data-ttu-id="62381-116">主な機能は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="62381-116">Key features include the following:</span></span>

- <span data-ttu-id="62381-117">オンプレミスの Active Directory と統合されます。</span><span class="sxs-lookup"><span data-stu-id="62381-117">It integrates with on-premises Active Directory.</span></span>
- <span data-ttu-id="62381-118">これにより、アプリでのシングルサインオンが可能になります。</span><span class="sxs-lookup"><span data-stu-id="62381-118">It enables single sign-on with your apps.</span></span>
- <span data-ttu-id="62381-119">[SAML](http://en.wikipedia.org/wiki/SAML_2.0)、 [ws-atomictransaction](http://en.wikipedia.org/wiki/WS-Federation)、 [OAuth 2.0](http://oauth.net/2/)などのオープン標準をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="62381-119">It supports open standards such as [SAML](http://en.wikipedia.org/wiki/SAML_2.0), [WS-Fed](http://en.wikipedia.org/wiki/WS-Federation), and [OAuth 2.0](http://oauth.net/2/).</span></span>
- <span data-ttu-id="62381-120">エンタープライズ[グラフ REST API](https://msdn.microsoft.com/library/hh974476.aspx)がサポートされています。</span><span class="sxs-lookup"><span data-stu-id="62381-120">It supports Enterprise [Graph REST API](https://msdn.microsoft.com/library/hh974476.aspx).</span></span>

<span data-ttu-id="62381-121">たとえば、従業員がイントラネットアプリにサインオンできるようにするために使用するオンプレミスの Windows Server Active Directory 環境があるとします。</span><span class="sxs-lookup"><span data-stu-id="62381-121">Suppose you have an on-premises Windows Server Active Directory environment that you use to enable employees to sign on to Intranet apps:</span></span>

![](single-sign-on/_static/image1.png)

<span data-ttu-id="62381-122">クラウド内にディレクトリを作成すると、どのような Azure AD が可能になります。</span><span class="sxs-lookup"><span data-stu-id="62381-122">What Azure AD enables you to do is create a directory in the cloud.</span></span> <span data-ttu-id="62381-123">これは無料の機能であり、簡単に設定できます。</span><span class="sxs-lookup"><span data-stu-id="62381-123">It's a free feature and easy to set up.</span></span>

<span data-ttu-id="62381-124">オンプレミスの Active Directory から完全に独立している可能性があります。任意のユーザーを追加して、インターネットアプリで認証することができます。</span><span class="sxs-lookup"><span data-stu-id="62381-124">It can be entirely independent from your on-premises Active Directory; you can put anyone you want in it and authenticate them in Internet apps.</span></span>

![Windows Azure Active Directory](single-sign-on/_static/image2.png)

<span data-ttu-id="62381-126">または、オンプレミスの AD と統合することもできます。</span><span class="sxs-lookup"><span data-stu-id="62381-126">Or you can integrate it with your on-premises AD.</span></span>

![AD と WAAD の統合](single-sign-on/_static/image3.png)

<span data-ttu-id="62381-128">これで、オンプレミスで認証できるすべての従業員が、インターネット経由でも認証できるようになりました。ファイアウォールを開放したり、新しいサーバーをデータセンターにデプロイしたりする必要はありません。</span><span class="sxs-lookup"><span data-stu-id="62381-128">Now all the employees who can authenticate on-premises can also authenticate over the Internet – without you having to open up a firewall or deploy any new servers in your data center.</span></span> <span data-ttu-id="62381-129">現在お持ちの既存の Active Directory 環境を引き続き活用し、内部アプリのシングルサインオン機能を利用することができます。</span><span class="sxs-lookup"><span data-stu-id="62381-129">You can continue to leverage all the existing Active Directory environment that you know and use today to give your internal apps single-sign on capability.</span></span>

<span data-ttu-id="62381-130">AD と Azure AD の間でこの接続を確立すると、web アプリとモバイルデバイスでクラウド内の従業員を認証できるようになります。また、Office 365、SalesForce.com、Google apps などのサードパーティ製アプリを有効にして、従業員の資格情報。</span><span class="sxs-lookup"><span data-stu-id="62381-130">Once you've made this connection between AD and Azure AD, you can also enable your web apps and your mobile devices to authenticate your employees in the cloud, and you can enable third-party apps, such as Office 365, SalesForce.com, or Google apps, to accept your employees' credentials.</span></span> <span data-ttu-id="62381-131">Office 365 を使用している場合は、Azure AD で既にセットアップされています。これは、Office 365 が認証と承認に Azure AD を使用するためです。</span><span class="sxs-lookup"><span data-stu-id="62381-131">If you're using Office 365, you're already set up with Azure AD because Office 365 uses Azure AD for authentication and authorization.</span></span>

![サードパーティ製アプリ](single-sign-on/_static/image4.png)

<span data-ttu-id="62381-133">この方法の利点は、組織がユーザーを追加または削除した場合や、ユーザーがパスワードを変更した場合は、現在オンプレミス環境で使用しているのと同じプロセスを使用することです。</span><span class="sxs-lookup"><span data-stu-id="62381-133">The beauty of this approach is that any time your organization adds or deletes a user, or a user changes a password, you use the same process that you use today in your on-premises environment.</span></span> <span data-ttu-id="62381-134">オンプレミスの AD の変更はすべて、自動的にクラウド環境に反映されます。</span><span class="sxs-lookup"><span data-stu-id="62381-134">All of your on-premises AD changes are automatically propagated to the cloud environment.</span></span>

<span data-ttu-id="62381-135">会社がを使用している場合、または Office 365 に移行している場合は、Office 365 で認証に Azure AD を使用するため、Azure AD が自動的に設定されます。</span><span class="sxs-lookup"><span data-stu-id="62381-135">If your company is using or moving to Office 365, the good news is that you'll have Azure AD set up automatically because Office 365 uses Azure AD for authentication.</span></span> <span data-ttu-id="62381-136">これにより、Office 365 が使用するのと同じ認証を、独自のアプリで簡単に使用できるようになります。</span><span class="sxs-lookup"><span data-stu-id="62381-136">So you can easily use in your own apps the same authentication that Office 365 uses.</span></span>

## <a name="set-up-an-azure-ad-tenant"></a><span data-ttu-id="62381-137">Azure AD テナントを設定する</span><span class="sxs-lookup"><span data-stu-id="62381-137">Set up an Azure AD tenant</span></span>

<span data-ttu-id="62381-138">Azure AD ディレクトリは Azure AD[テナント](https://technet.microsoft.com/library/jj573650.aspx)と呼ばれ、テナントの設定は非常に簡単です。</span><span class="sxs-lookup"><span data-stu-id="62381-138">an Azure AD directory is called an Azure AD [tenant](https://technet.microsoft.com/library/jj573650.aspx), and setting up a tenant is pretty easy.</span></span> <span data-ttu-id="62381-139">概念を説明するために Azure 管理ポータルでどのように行われるかについて説明しますが、他のポータル関数と同様に、スクリプトまたは管理 API を使用して行うこともできます。</span><span class="sxs-lookup"><span data-stu-id="62381-139">We'll show you how it's done in the Azure Management Portal in order to illustrate the concepts, but of course like the other portal functions you can also do it by using a script or management API.</span></span>

<span data-ttu-id="62381-140">管理ポータルで、[Active Directory] タブをクリックします。</span><span class="sxs-lookup"><span data-stu-id="62381-140">In the management portal click the Active Directory tab.</span></span>

![ポータルでの WAAD](single-sign-on/_static/image5.png)

<span data-ttu-id="62381-142">Azure アカウント用に1つの Azure AD テナントが自動的に作成されます。ページの下部にある **[追加]** ボタンをクリックすると、追加のディレクトリを作成できます。</span><span class="sxs-lookup"><span data-stu-id="62381-142">You automatically have one Azure AD tenant for your Azure account, and you can click the **Add** button at the bottom of the page to create additional directories.</span></span> <span data-ttu-id="62381-143">たとえば、テスト環境用に1つ、運用環境用に1つを使用することができます。</span><span class="sxs-lookup"><span data-stu-id="62381-143">You might want one for a test environment and one for production, for example.</span></span> <span data-ttu-id="62381-144">新しいディレクトリの名前については、慎重に検討してください。</span><span class="sxs-lookup"><span data-stu-id="62381-144">Think carefully about what you name a new directory.</span></span> <span data-ttu-id="62381-145">ディレクトリの名前を使用した後で、いずれかのユーザーに対して名前を再び使用すると、混乱を招く可能性があります。</span><span class="sxs-lookup"><span data-stu-id="62381-145">If you use your name for the directory and then you use your name again for one of the users, that can be confusing.</span></span>

![ディレクトリを追加する](single-sign-on/_static/image6.png)

<span data-ttu-id="62381-147">ポータルでは、この環境内でのユーザーの作成、削除、管理を完全にサポートしています。</span><span class="sxs-lookup"><span data-stu-id="62381-147">The portal has full support for creating, deleting, and managing users within this environment.</span></span> <span data-ttu-id="62381-148">たとえば、ユーザーを追加するには、 **[ユーザー]** タブにアクセスし、 **[ユーザーの追加]** ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="62381-148">For example, to add a user go to the **Users** tab and click the **Add User** button.</span></span>

![[ユーザーの追加] ボタン](single-sign-on/_static/image7.png)

![[ユーザーの追加] ダイアログ](single-sign-on/_static/image8.png)

<span data-ttu-id="62381-151">このディレクトリにのみ存在する新しいユーザーを作成したり、このディレクトリに Microsoft アカウントをユーザーとして登録したり、このディレクトリ内のユーザーとして別の Azure AD ディレクトリのユーザーを登録したりすることができます。</span><span class="sxs-lookup"><span data-stu-id="62381-151">You can create a new user who exists only in this directory, or you can register a Microsoft Account as a user in this directory, or register or a user from another Azure AD directory as a user in this directory.</span></span> <span data-ttu-id="62381-152">(実際のディレクトリでは、既定のドメインは ContosoTest.onmicrosoft.com です。</span><span class="sxs-lookup"><span data-stu-id="62381-152">(In a real directory, the default domain would be ContosoTest.onmicrosoft.com.</span></span> <span data-ttu-id="62381-153">また、contoso.com のように、自分で選択したドメインを使用することもできます)。</span><span class="sxs-lookup"><span data-stu-id="62381-153">You can also use a domain of your own choosing, like contoso.com.)</span></span>

![ユーザーの種類](single-sign-on/_static/image9.png)

![[ユーザーの追加] ダイアログ](single-sign-on/_static/image10.png)

<span data-ttu-id="62381-156">ロールにユーザーを割り当てることができます。</span><span class="sxs-lookup"><span data-stu-id="62381-156">You can assign the user to a role.</span></span>

![ユーザー プロファイル](single-sign-on/_static/image11.png)

<span data-ttu-id="62381-158">アカウントは一時パスワードで作成されます。</span><span class="sxs-lookup"><span data-stu-id="62381-158">And the account is created with a temporary password.</span></span>

![一時パスワード](single-sign-on/_static/image12.png)

<span data-ttu-id="62381-160">この方法で作成したユーザーは、このクラウドディレクトリを使用して、すぐに web アプリにログインできます。</span><span class="sxs-lookup"><span data-stu-id="62381-160">The users you create this way can immediately log in to your web apps using this cloud directory.</span></span>

<span data-ttu-id="62381-161">エンタープライズシングルサインオンに適しているのは、[ディレクトリの**統合**] タブです。</span><span class="sxs-lookup"><span data-stu-id="62381-161">What's great for enterprise single sign-on, though, is the **Directory Integration** tab:</span></span>

![[ディレクトリの統合] タブ](single-sign-on/_static/image13.png)

<span data-ttu-id="62381-163">ディレクトリ統合を有効にして[ツールをダウンロード](https://social.technet.microsoft.com/wiki/contents/articles/19098.howto-install-the-windows-azure-active-directory-sync-tool-now-with-pictures.aspx)する場合は、組織内で既に使用している既存のオンプレミス Active Directory とこのクラウドディレクトリを同期できます。</span><span class="sxs-lookup"><span data-stu-id="62381-163">If you enable directory integration, and [download a tool](https://social.technet.microsoft.com/wiki/contents/articles/19098.howto-install-the-windows-azure-active-directory-sync-tool-now-with-pictures.aspx), you can sync this cloud directory with your existing on-premises Active Directory that you're already using inside your organization.</span></span> <span data-ttu-id="62381-164">ディレクトリに格納されているすべてのユーザーが、このクラウドディレクトリに表示されます。</span><span class="sxs-lookup"><span data-stu-id="62381-164">Then all of the users stored in your directory will show up in this cloud directory.</span></span> <span data-ttu-id="62381-165">クラウドアプリは、既存の Active Directory 資格情報を使用してすべての従業員を認証できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="62381-165">Your cloud apps can now authenticate all of your employees using their existing Active Directory credentials.</span></span> <span data-ttu-id="62381-166">また、同期ツールと Azure AD 自体も無料です。</span><span class="sxs-lookup"><span data-stu-id="62381-166">And all this is free – both the sync tool and Azure AD itself.</span></span>

<span data-ttu-id="62381-167">ツールは、これらのスクリーンショットからわかるように、簡単に使用できるウィザードです。</span><span class="sxs-lookup"><span data-stu-id="62381-167">The tool is a wizard that is easy to use, as you can see from these screen shots.</span></span> <span data-ttu-id="62381-168">これらは完全な手順ではなく、基本的なプロセスを示す例にすぎません。</span><span class="sxs-lookup"><span data-stu-id="62381-168">These are not complete instructions, just an example showing you the basic process.</span></span> <span data-ttu-id="62381-169">詳細な操作方法の詳細については、章の最後にある「 [resources](#resources) 」セクションのリンクを参照してください。</span><span class="sxs-lookup"><span data-stu-id="62381-169">For more detailed how-to-do-it information, see the links in the [Resources](#resources) section at the end of the chapter.</span></span>

![WAAD 同期ツールの構成ウィザード](single-sign-on/_static/image14.png)

<span data-ttu-id="62381-171">**[次へ]** をクリックし、Azure Active Directory の資格情報を入力します。</span><span class="sxs-lookup"><span data-stu-id="62381-171">Click **Next**, and then enter your Azure Active Directory credentials.</span></span>

![WAAD 同期ツールの構成ウィザード](single-sign-on/_static/image15.png)

<span data-ttu-id="62381-173">**[次へ]** をクリックし、オンプレミスの AD 資格情報を入力します。</span><span class="sxs-lookup"><span data-stu-id="62381-173">Click **Next**, and then enter your on-premises AD credentials.</span></span>

![WAAD 同期ツールの構成ウィザード](single-sign-on/_static/image16.png)

<span data-ttu-id="62381-175">**[次へ]** をクリックし、AD パスワードのハッシュをクラウドに格納するかどうかを指定します。</span><span class="sxs-lookup"><span data-stu-id="62381-175">Click **Next**, and then indicate if you want to store a hash of your AD passwords in the cloud.</span></span>

![WAAD 同期ツールの構成ウィザード](single-sign-on/_static/image17.png)

<span data-ttu-id="62381-177">クラウドに格納できるパスワードハッシュは一方向のハッシュです。実際のパスワードは Azure AD に格納されません。</span><span class="sxs-lookup"><span data-stu-id="62381-177">The password hash that you can store in the cloud is a one-way hash; actual passwords are never stored in Azure AD.</span></span> <span data-ttu-id="62381-178">クラウドにハッシュを格納しない場合は、 [Active Directory フェデレーションサービス (AD FS)](https://technet.microsoft.com/library/hh831502.aspx) (ADFS) を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="62381-178">If you decide against storing hashes in the cloud, you'll have to use [Active Directory Federation Services](https://technet.microsoft.com/library/hh831502.aspx) (ADFS).</span></span> <span data-ttu-id="62381-179">[ADFS を使用するかどうかを選択する際に考慮すべきその他の要素](https://technet.microsoft.com/library/jj573653.aspx)もあります。</span><span class="sxs-lookup"><span data-stu-id="62381-179">There are also [other factors to consider when choosing whether or not to use ADFS](https://technet.microsoft.com/library/jj573653.aspx).</span></span> <span data-ttu-id="62381-180">ADFS オプションには、追加の構成手順がいくつか必要です。</span><span class="sxs-lookup"><span data-stu-id="62381-180">The ADFS option requires a few additional configuration steps.</span></span>

<span data-ttu-id="62381-181">クラウドにハッシュを保存することを選択した場合は完了です。 **[次へ]** をクリックすると、ツールによってディレクトリの同期が開始されます。</span><span class="sxs-lookup"><span data-stu-id="62381-181">If you choose to store hashes in the cloud, you're done, and the tool starts synchronizing directories when you click **Next**.</span></span>

![WAAD 同期ツールの構成ウィザード](single-sign-on/_static/image18.png)

<span data-ttu-id="62381-183">数分で完了します。</span><span class="sxs-lookup"><span data-stu-id="62381-183">And in a few minutes you're done.</span></span>

![WAAD 同期ツールの構成ウィザード](single-sign-on/_static/image19.png)

<span data-ttu-id="62381-185">これは、Windows 2003 以降の組織の1つのドメインコントローラーでのみ実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="62381-185">You only have to run this on one domain controller in the organization, on Windows 2003 or higher.</span></span> <span data-ttu-id="62381-186">再起動は必要ありません。</span><span class="sxs-lookup"><span data-stu-id="62381-186">And no need to reboot.</span></span> <span data-ttu-id="62381-187">完了すると、すべてのユーザーがクラウドに存在し、SAML、OAuth、または WS-ATOMICTRANSACTION を使用して任意の web アプリケーションまたはモバイルアプリケーションからシングルサインオンできるようになります。</span><span class="sxs-lookup"><span data-stu-id="62381-187">When you're done, all of your users are in the cloud and you can do single sign-on from any web or mobile application, using SAML, OAuth, or WS-Fed.</span></span>

<span data-ttu-id="62381-188">Microsoft では、これがどのようにセキュリティで保護されているのかをたずねられる場合があります。</span><span class="sxs-lookup"><span data-stu-id="62381-188">Sometimes we get asked about how secure this is – does Microsoft use it for their own sensitive business data?</span></span> <span data-ttu-id="62381-189">答えは "はい" です。</span><span class="sxs-lookup"><span data-stu-id="62381-189">And the answer is yes we do.</span></span> <span data-ttu-id="62381-190">たとえば、 [https://microsoft.sharepoint.com/](https://microsoft.sharepoint.com/)の内部 Microsoft SharePoint サイトに移動すると、ログインを求めるメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="62381-190">For example, if you go to the internal Microsoft SharePoint site at [https://microsoft.sharepoint.com/](https://microsoft.sharepoint.com/), you get prompted to log in.</span></span>

![Office 365 サインイン](single-sign-on/_static/image20.png)

<span data-ttu-id="62381-192">Microsoft では ADFS が有効になっているため、Microsoft ID を入力すると、ADFS ログインページにリダイレクトされます。</span><span class="sxs-lookup"><span data-stu-id="62381-192">Microsoft has enabled ADFS, so when you enter a Microsoft ID, you get redirected to an ADFS log-in page.</span></span>

![ADFS サインイン](single-sign-on/_static/image21.png)

<span data-ttu-id="62381-194">また、内部の Microsoft AD アカウントに格納されている資格情報を入力すると、この内部アプリケーションにアクセスできるようになります。</span><span class="sxs-lookup"><span data-stu-id="62381-194">And once you enter credentials stored in an internal Microsoft AD account, you have access to this internal application.</span></span>

![MS SharePoint サイト](single-sign-on/_static/image22.png)

<span data-ttu-id="62381-196">AD サインインサーバーを使用しているのは、Azure AD が利用可能になる前に ADFS が既に設定されているが、ログインプロセスがクラウド内の Azure AD ディレクトリを経由しているためです。</span><span class="sxs-lookup"><span data-stu-id="62381-196">We're using an AD sign-in server mainly because we already had ADFS set up before Azure AD became available, but the log-in process is going through an Azure AD directory in the cloud.</span></span> <span data-ttu-id="62381-197">重要なドキュメント、ソース管理、パフォーマンス管理ファイル、販売レポートなどをクラウドに置き、同じソリューションを使用してセキュリティを保護しています。</span><span class="sxs-lookup"><span data-stu-id="62381-197">We put our important documents, source control, performance management files, sales reports, and more, in the cloud and are using this exact same solution to secure them.</span></span>

## <a name="create-an-aspnet-app-that-uses-azure-ad-for-single-sign-on"></a><span data-ttu-id="62381-198">シングルサインオンに Azure AD を使用する ASP.NET アプリを作成する</span><span class="sxs-lookup"><span data-stu-id="62381-198">Create an ASP.NET app that uses Azure AD for single sign-on</span></span>

<span data-ttu-id="62381-199">Visual Studio を使用すると、いくつかのスクリーンショットからわかるように、シングルサインオンに Azure AD を使用するアプリを簡単に作成できます。</span><span class="sxs-lookup"><span data-stu-id="62381-199">Visual Studio makes it really easy to create an app that uses Azure AD for single sign-on, as you can see from a few screen shots.</span></span>

<span data-ttu-id="62381-200">新しい ASP.NET アプリケーション (MVC または Web フォーム) を作成する場合は、既定の認証方法が ASP.NET Identity ます。</span><span class="sxs-lookup"><span data-stu-id="62381-200">When you create a new ASP.NET application, either MVC or Web Forms, the default authentication method is ASP.NET Identity.</span></span> <span data-ttu-id="62381-201">これを Azure AD に変更するには、 **[認証の変更]** ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="62381-201">To change that to Azure AD, you click a **Change Authentication** button.</span></span>

![認証の変更](single-sign-on/_static/image23.png)

<span data-ttu-id="62381-203">[組織アカウント] を選択し、ドメイン名を入力して、[シングルサインオン] を選択します。</span><span class="sxs-lookup"><span data-stu-id="62381-203">Select Organizational Accounts, enter your domain name, and then select Single Sign On.</span></span>

![認証の構成ダイアログ](single-sign-on/_static/image24.png)

<span data-ttu-id="62381-205">また、ディレクトリデータに対する読み取りアクセス許可または読み取り/書き込みアクセス許可をアプリに付与することもできます。</span><span class="sxs-lookup"><span data-stu-id="62381-205">You can also give the app read or read/write permission for directory data.</span></span> <span data-ttu-id="62381-206">これを行うと、 [Azure Graph REST API](https://msdn.microsoft.com/library/windowsazure/hh974476.aspx)を使用して、ユーザーの電話番号を検索したり、オフィス内にいるかどうかを確認したり、最後にログオンしたときにその情報を確認したりすることができます。</span><span class="sxs-lookup"><span data-stu-id="62381-206">If you do that, it can use the [Azure Graph REST API](https://msdn.microsoft.com/library/windowsazure/hh974476.aspx) to look up users' phone number, find out if they're in the office, when they last logged on, etc.</span></span>

<span data-ttu-id="62381-207">これで作業は完了です。 Visual Studio によって Azure AD テナントの管理者の資格情報が要求され、新しいアプリケーション用のプロジェクトと Azure AD テナントの両方が構成されます。</span><span class="sxs-lookup"><span data-stu-id="62381-207">That's all you have to do - Visual Studio asks for the credentials for an administrator for your Azure AD tenant, and then it configures both your project and your Azure AD tenant for the new application.</span></span>

<span data-ttu-id="62381-208">プロジェクトを実行すると、サインインページが表示され、Azure AD ディレクトリ内のユーザーの資格情報を使用してサインインできます。</span><span class="sxs-lookup"><span data-stu-id="62381-208">When you run the project, you'll see a sign-in page, and you can sign in with credentials of a user in your Azure AD directory.</span></span>

![組織アカウントのサインイン](single-sign-on/_static/image25.png)

![ログイン済み](single-sign-on/_static/image26.png)

<span data-ttu-id="62381-211">アプリを Azure にデプロイする場合は、[**組織の認証を有効に**する] チェックボックスをオンにするだけで、もう一度 Visual Studio によってすべての構成が処理されます。</span><span class="sxs-lookup"><span data-stu-id="62381-211">When you deploy the app to Azure, all you have to do is select an **Enable Organizational Authentication** check box, and once again Visual Studio takes care of all the configuration for you.</span></span>

![Web 公開](single-sign-on/_static/image27.png)

<span data-ttu-id="62381-213">これらのスクリーンショットは、Azure AD 認証を使用するアプリを構築する方法を示す完全なステップバイステップのチュートリアルであり、 [Azure Active Directory を使用した ASP.NET アプリの開発](../../../../identity/overview/getting-started/developing-aspnet-apps-with-windows-azure-active-directory.md)について説明しています。</span><span class="sxs-lookup"><span data-stu-id="62381-213">These screen shots come from a complete step-by-step tutorial that shows how to build an app that uses Azure AD authentication: [Developing ASP.NET Apps with Azure Active Directory](../../../../identity/overview/getting-started/developing-aspnet-apps-with-windows-azure-active-directory.md).</span></span>

## <a name="summary"></a><span data-ttu-id="62381-214">要約</span><span class="sxs-lookup"><span data-stu-id="62381-214">Summary</span></span>

<span data-ttu-id="62381-215">この章では、Azure Active Directory、Visual Studio、および ASP.NET を使用して、組織のユーザーのインターネットアプリケーションでのシングルサインオンを簡単にセットアップできるようにしました。</span><span class="sxs-lookup"><span data-stu-id="62381-215">In this chapter you saw that Azure Active Directory, Visual Studio, and ASP.NET, make it easy to set up single sign-on in Internet applications for your organization's users.</span></span> <span data-ttu-id="62381-216">ユーザーは、内部ネットワークで Active Directory を使用したサインオンに使用するのと同じ資格情報を使用して、インターネットアプリでサインオンできます。</span><span class="sxs-lookup"><span data-stu-id="62381-216">Your users can sign on in Internet apps using the same credentials they use to sign on using Active Directory in your internal network.</span></span>

<span data-ttu-id="62381-217">[次の章](data-storage-options.md)では、クラウドアプリで使用できるデータストレージオプションについて説明します。</span><span class="sxs-lookup"><span data-stu-id="62381-217">The [next chapter](data-storage-options.md) looks at the data storage options available for a cloud app.</span></span>

<a id="resources"></a>
## <a name="resources"></a><span data-ttu-id="62381-218">リソース</span><span class="sxs-lookup"><span data-stu-id="62381-218">Resources</span></span>

<span data-ttu-id="62381-219">詳細については、次のリソースを参照してください。</span><span class="sxs-lookup"><span data-stu-id="62381-219">For more information, see the following resources:</span></span>

- <span data-ttu-id="62381-220">[Azure Active Directory ドキュメント](https://docs.microsoft.com/azure/active-directory/)。</span><span class="sxs-lookup"><span data-stu-id="62381-220">[Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span></span> <span data-ttu-id="62381-221">Windowsazure.com サイトの Azure AD ドキュメントのポータルページです。</span><span class="sxs-lookup"><span data-stu-id="62381-221">Portal page for Azure AD documentation on the windowsazure.com site.</span></span> <span data-ttu-id="62381-222">詳細な手順のチュートリアルについては、「**開発**」セクションを参照してください。</span><span class="sxs-lookup"><span data-stu-id="62381-222">For step by step tutorials, see the **Develop** section.</span></span>
- <span data-ttu-id="62381-223">[Azure Multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/)。</span><span class="sxs-lookup"><span data-stu-id="62381-223">[Azure Multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/).</span></span> <span data-ttu-id="62381-224">Azure での multi-factor authentication に関するドキュメントのポータルページです。</span><span class="sxs-lookup"><span data-stu-id="62381-224">Portal page for documentation about multi-factor authentication in Azure.</span></span>
- <span data-ttu-id="62381-225">[組織アカウントの認証オプション](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#orgauthoptions)。</span><span class="sxs-lookup"><span data-stu-id="62381-225">[Organizational account authentication options](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#orgauthoptions).</span></span> <span data-ttu-id="62381-226">[新しいプロジェクトの Visual Studio 2013] ダイアログボックスの Azure AD 認証オプションについて説明します。</span><span class="sxs-lookup"><span data-stu-id="62381-226">Explanation of the Azure AD authentication options in the Visual Studio 2013 new-project dialog.</span></span>
- <span data-ttu-id="62381-227">[Microsoft のパターンとプラクティス-フェデレーション Id パターン](https://msdn.microsoft.com/library/dn589790.aspx)。</span><span class="sxs-lookup"><span data-stu-id="62381-227">[Microsoft Patterns and Practices - Federated Identity Pattern](https://msdn.microsoft.com/library/dn589790.aspx).</span></span>
- <span data-ttu-id="62381-228">[HowTo: Azure Active Directory 同期ツールをインストール](https://social.technet.microsoft.com/wiki/contents/articles/19098.howto-install-the-windows-azure-active-directory-sync-tool-now-with-pictures.aspx)します。</span><span class="sxs-lookup"><span data-stu-id="62381-228">[HowTo: Install the Azure Active Directory Sync Tool](https://social.technet.microsoft.com/wiki/contents/articles/19098.howto-install-the-windows-azure-active-directory-sync-tool-now-with-pictures.aspx).</span></span>
- <span data-ttu-id="62381-229">[Active Directory フェデレーションサービス (AD FS) 2.0 コンテンツマップ](https://social.technet.microsoft.com/wiki/contents/articles/2735.ad-fs-2-0-content-map.aspx)。</span><span class="sxs-lookup"><span data-stu-id="62381-229">[Active Directory Federation Services 2.0 Content Map](https://social.technet.microsoft.com/wiki/contents/articles/2735.ad-fs-2-0-content-map.aspx).</span></span> <span data-ttu-id="62381-230">ADFS 2.0 に関するドキュメントへのリンク。</span><span class="sxs-lookup"><span data-stu-id="62381-230">Links to documentation about ADFS 2.0.</span></span>
- <span data-ttu-id="62381-231">[Windows Azure AD アプリケーションでのロールベースおよび ACL ベースの承認](https://code.msdn.microsoft.com/Role-Based-and-ACL-Based-86ad71a1)。</span><span class="sxs-lookup"><span data-stu-id="62381-231">[Role-Based and ACL-Based Authorization in a Windows Azure AD Application](https://code.msdn.microsoft.com/Role-Based-and-ACL-Based-86ad71a1).</span></span> <span data-ttu-id="62381-232">サンプルアプリケーション。</span><span class="sxs-lookup"><span data-stu-id="62381-232">Sample application.</span></span>
- <span data-ttu-id="62381-233">[Azure Active Directory Graph API ブログ](https://blogs.msdn.com/b/aadgraphteam/)をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="62381-233">[Azure Active Directory Graph API blog](https://blogs.msdn.com/b/aadgraphteam/).</span></span>
- <span data-ttu-id="62381-234">[ハイブリッド Id インフラストラクチャでの BYOD とディレクトリの統合における Access Control](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2014/PCIT-B213#fbid=)。</span><span class="sxs-lookup"><span data-stu-id="62381-234">[Access Control in BYOD and Directory Integration in a Hybrid Identity Infrastructure](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2014/PCIT-B213#fbid=).</span></span> <span data-ttu-id="62381-235">Gayana Bagdasaryan による Tech Ed 2014 session video。</span><span class="sxs-lookup"><span data-stu-id="62381-235">Tech Ed 2014 session video by Gayana Bagdasaryan.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="62381-236">[前へ](web-development-best-practices.md)
> [次へ](data-storage-options.md)</span><span class="sxs-lookup"><span data-stu-id="62381-236">[Previous](web-development-best-practices.md)
[Next](data-storage-options.md)</span></span>
