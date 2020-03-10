---
uid: mvc/overview/older-versions-1/security/authenticating-users-with-forms-authentication-cs
title: フォーム認証を使用してC#ユーザーを認証する () |Microsoft Docs
author: microsoft
description: '[承認] 属性を使用して、MVC アプリケーションの特定のページをパスワードで保護する方法について説明します。 Web サイトの管理を使用する方法についても説明します。'
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 239fd3ca-5630-4b8d-bc4b-2f906b1d3504
msc.legacyurl: /mvc/overview/older-versions-1/security/authenticating-users-with-forms-authentication-cs
msc.type: authoredcontent
ms.openlocfilehash: bed2eafa47fec25ac04cb07e0037f596494bb7d9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78435448"
---
# <a name="authenticating-users-with-forms-authentication-c"></a><span data-ttu-id="3ba62-104">フォーム認証でユーザーを認証する (C#)</span><span class="sxs-lookup"><span data-stu-id="3ba62-104">Authenticating Users with Forms Authentication (C#)</span></span>

<span data-ttu-id="3ba62-105">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="3ba62-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="3ba62-106">[承認] 属性を使用して、MVC アプリケーションの特定のページをパスワードで保護する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="3ba62-106">Learn how to use the [Authorize] attribute to password protect particular pages in your MVC application.</span></span> <span data-ttu-id="3ba62-107">Web サイト管理ツールを使用して、ユーザーとロールを作成および管理する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="3ba62-107">You learn how to use the Web Site Administration Tool to create and manage users and roles.</span></span> <span data-ttu-id="3ba62-108">また、ユーザーアカウントとロール情報を格納する場所を構成する方法についても説明します。</span><span class="sxs-lookup"><span data-stu-id="3ba62-108">You also learn how to configure where user account and role information is stored.</span></span>

<span data-ttu-id="3ba62-109">このチュートリアルの目的は、フォーム認証を使用して、ASP.NET MVC アプリケーションのビューをパスワードで保護する方法を説明することです。</span><span class="sxs-lookup"><span data-stu-id="3ba62-109">The goal of this tutorial is to explain how you can use Forms authentication to password protect the views in your ASP.NET MVC applications.</span></span> <span data-ttu-id="3ba62-110">Web サイト管理ツールを使用して、ユーザーとロールを作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="3ba62-110">You learn how to use the Web Site Administration Tool to create users and roles.</span></span> <span data-ttu-id="3ba62-111">また、承認されていないユーザーがコントローラーアクションを呼び出さないようにする方法についても説明します。</span><span class="sxs-lookup"><span data-stu-id="3ba62-111">You also learn how to prevent unauthorized users from invoking controller actions.</span></span> <span data-ttu-id="3ba62-112">最後に、ユーザー名とパスワードが格納される場所を構成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="3ba62-112">Finally, you learn how to configure where user names and passwords are stored.</span></span>

#### <a name="using-the-web-site-administration-tool"></a><span data-ttu-id="3ba62-113">Web サイト管理ツールの使用</span><span class="sxs-lookup"><span data-stu-id="3ba62-113">Using the Web Site Administration Tool</span></span>

<span data-ttu-id="3ba62-114">他の作業を行う前に、まずユーザーとロールをいくつか作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="3ba62-114">Before we do anything else, we should start by creating some users and roles.</span></span> <span data-ttu-id="3ba62-115">新しいユーザーとロールを作成する最も簡単な方法は、Visual Studio 2008 Web サイト管理ツールを利用することです。</span><span class="sxs-lookup"><span data-stu-id="3ba62-115">The easiest way to create new users and roles is to take advantage of the Visual Studio 2008 Web Site Administration Tool.</span></span> <span data-ttu-id="3ba62-116">このツールを起動するには、メニューオプション**プロジェクトの [ASP.NET Configuration**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="3ba62-116">You can launch this tool by selecting the menu option **Project, ASP.NET Configuration**.</span></span> <span data-ttu-id="3ba62-117">または、[ソリューションエクスプローラー] ウィンドウの上部に表示される、ハンマーの (少し恐ろしい) アイコンをクリックして、Web サイト管理ツールを起動することもできます (図1を参照)。</span><span class="sxs-lookup"><span data-stu-id="3ba62-117">Alternatively, you can launch the Web Site Administration Tool by clicking the (somewhat scary) icon of the hammer hitting the world that appears at the top of the Solution Explorer window (see Figure 1).</span></span>

<span data-ttu-id="3ba62-118">**図 1: Web サイト管理ツールの起動**</span><span class="sxs-lookup"><span data-stu-id="3ba62-118">**Figure 1 – Launching the Web Site Administration Tool**</span></span>

![clip_image002](authenticating-users-with-forms-authentication-cs/_static/image1.jpg)

<span data-ttu-id="3ba62-120">Web サイト管理ツールで、セキュリティ タブを選択して新しいユーザーとロールを作成します。 **ユーザーの作成** リンクをクリックして、Stephen という名前の新しいユーザーを作成します (図2を参照)。</span><span class="sxs-lookup"><span data-stu-id="3ba62-120">Within the Web Site Administration Tool, you create new users and roles by selecting the Security tab. Click the **Create user** link to create a new user named Stephen (see Figure 2).</span></span> <span data-ttu-id="3ba62-121">Stephen ユーザーに必要なパスワード (たとえば、 *secret*) を入力します。</span><span class="sxs-lookup"><span data-stu-id="3ba62-121">Provide the Stephen user with any password that you want (for example, *secret*).</span></span>

<span data-ttu-id="3ba62-122">**図2–新しいユーザーの作成**</span><span class="sxs-lookup"><span data-stu-id="3ba62-122">**Figure 2 – Creating a new user**</span></span>

![clip_image004](authenticating-users-with-forms-authentication-cs/_static/image2.jpg)

<span data-ttu-id="3ba62-124">新しいロールを作成するには、最初にロールを有効にし、1つ以上のロールを定義します。</span><span class="sxs-lookup"><span data-stu-id="3ba62-124">You create new roles by first enabling roles and defining one or more roles.</span></span> <span data-ttu-id="3ba62-125">**[ロールの有効化]** リンクをクリックして、ロールを有効にします。</span><span class="sxs-lookup"><span data-stu-id="3ba62-125">Enable roles by clicking the **Enable roles** link.</span></span> <span data-ttu-id="3ba62-126">次に、 **[ロールの作成または管理]** リンクをクリックして、*管理者*という名前のロールを作成します (図3を参照)。</span><span class="sxs-lookup"><span data-stu-id="3ba62-126">Next, create a role named *Administrators* by clicking the **Create or Manage roles** link (see Figure 3).</span></span>

<span data-ttu-id="3ba62-127">**図3–新しいロールを作成する**</span><span class="sxs-lookup"><span data-stu-id="3ba62-127">**Figure 3 – Creating a new role**</span></span>

![clip_image006](authenticating-users-with-forms-authentication-cs/_static/image3.jpg)

<span data-ttu-id="3ba62-129">最後に、[ユーザーの作成] リンクをクリックし、[ユーザーの作成時に管理者を選択する] をクリックして、"ユーザー名" という名前の新しいユーザーを作成し、管理者ロールに関連付けます (図4を参照)。</span><span class="sxs-lookup"><span data-stu-id="3ba62-129">Finally, create a new user named Sally and associate Sally with the Administrators role by clicking the Create User link and selecting Administrators when creating Sally (see Figure 4).</span></span>

<span data-ttu-id="3ba62-130">**図4–ロールへのユーザーの追加**</span><span class="sxs-lookup"><span data-stu-id="3ba62-130">**Figure 4 – Adding a user to a role**</span></span>

![clip_image008](authenticating-users-with-forms-authentication-cs/_static/image4.jpg)

<span data-ttu-id="3ba62-132">すべてが完了したら、2つの新しいユーザーを Stephen として作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="3ba62-132">When all is said and done, you should have two new users named Stephen and Sally.</span></span> <span data-ttu-id="3ba62-133">また、Administrators という名前の新しいロールも必要です。</span><span class="sxs-lookup"><span data-stu-id="3ba62-133">You should also have a new role named Administrators.</span></span> <span data-ttu-id="3ba62-134">Stephen が管理者ロールのメンバーであり、かつ、そのメンバーがではありません。</span><span class="sxs-lookup"><span data-stu-id="3ba62-134">Sally is a member of the Administrators role and Stephen is not.</span></span>

#### <a name="requiring-authorization"></a><span data-ttu-id="3ba62-135">承認が必要</span><span class="sxs-lookup"><span data-stu-id="3ba62-135">Requiring Authorization</span></span>

<span data-ttu-id="3ba62-136">ユーザーが [承認] 属性をアクションに追加することによってコントローラーアクションを呼び出す前に、ユーザーの認証を要求することができます。</span><span class="sxs-lookup"><span data-stu-id="3ba62-136">You can require a user to be authenticated before the user invokes a controller action by adding the [Authorize] attribute to the action.</span></span> <span data-ttu-id="3ba62-137">[承認] 属性を個々のコントローラーアクションに適用することも、この属性をコントローラークラス全体に適用することもできます。</span><span class="sxs-lookup"><span data-stu-id="3ba62-137">You can apply the [Authorize] attribute to an individual controller action or you can apply this attribute to an entire controller class.</span></span>

<span data-ttu-id="3ba62-138">たとえば、リスト1のコントローラーは、企業秘密 () という名前のアクションを公開します。</span><span class="sxs-lookup"><span data-stu-id="3ba62-138">For example, the controller in Listing 1 exposes an action named CompanySecrets().</span></span> <span data-ttu-id="3ba62-139">このアクションは [承認] 属性で修飾されているため、ユーザーが認証されていない限り、このアクションを呼び出すことはできません。</span><span class="sxs-lookup"><span data-stu-id="3ba62-139">Because this action is decorated with the [Authorize] attribute, this action cannot be invoked unless a user is authenticated.</span></span>

<span data-ttu-id="3ba62-140">**リスト1– Controllers\ homecontroller.cs**</span><span class="sxs-lookup"><span data-stu-id="3ba62-140">**Listing 1 – Controllers\HomeController.cs**</span></span>

[!code-csharp[Main](authenticating-users-with-forms-authentication-cs/samples/sample1.cs)]

<span data-ttu-id="3ba62-141">ブラウザーのアドレスバーに/Home/CompanySecrets URL を入力して会社のシークレット () アクションを呼び出すと、認証されたユーザーではない場合、ログインビューに自動的にリダイレクトされます (図5を参照)。</span><span class="sxs-lookup"><span data-stu-id="3ba62-141">If you invoke the CompanySecrets() action by entering the URL /Home/CompanySecrets in the address bar of your browser, and you are not an authenticated user, then you will be redirected to the Login view automatically (see Figure 5).</span></span>

<span data-ttu-id="3ba62-142">**図 5-ログインビュー**</span><span class="sxs-lookup"><span data-stu-id="3ba62-142">**Figure 5 – The Login view**</span></span>

![clip_image010](authenticating-users-with-forms-authentication-cs/_static/image5.jpg)

<span data-ttu-id="3ba62-144">ログインビューを使用して、ユーザー名とパスワードを入力できます。</span><span class="sxs-lookup"><span data-stu-id="3ba62-144">You can use the Login view to enter your user name and password.</span></span> <span data-ttu-id="3ba62-145">登録済みのユーザーでない場合は、 **[登録]** リンクをクリックしてレジスタビューに移動できます (図6を参照)。</span><span class="sxs-lookup"><span data-stu-id="3ba62-145">If you are not a registered user then you can click the **register** link to navigate to the Register view (see Figure 6).</span></span> <span data-ttu-id="3ba62-146">新しいユーザーアカウントを作成するには、[登録] ビューを使用します。</span><span class="sxs-lookup"><span data-stu-id="3ba62-146">You can use the Register view to create a new user account.</span></span>

<span data-ttu-id="3ba62-147">**図6–レジスタビュー**</span><span class="sxs-lookup"><span data-stu-id="3ba62-147">**Figure 6 – The Register view**</span></span>

![clip_image012](authenticating-users-with-forms-authentication-cs/_static/image6.jpg)

<span data-ttu-id="3ba62-149">ログインに成功すると、会社のシークレットビューが表示されます (図7を参照)。</span><span class="sxs-lookup"><span data-stu-id="3ba62-149">After you successfully log in, you can see the CompanySecrets view (see Figure 7).</span></span> <span data-ttu-id="3ba62-150">既定では、ブラウザーウィンドウを閉じるまでログインしたままになります。</span><span class="sxs-lookup"><span data-stu-id="3ba62-150">By default, you will continue to be logged in until you close your browser window.</span></span>

<span data-ttu-id="3ba62-151">**図 7-会社の機密情報の表示**</span><span class="sxs-lookup"><span data-stu-id="3ba62-151">**Figure 7 – The CompanySecrets view**</span></span>

![clip_image014](authenticating-users-with-forms-authentication-cs/_static/image7.jpg)

#### <a name="authorizing-by-user-name-or-user-role"></a><span data-ttu-id="3ba62-153">ユーザー名またはユーザーロールによる承認</span><span class="sxs-lookup"><span data-stu-id="3ba62-153">Authorizing by User Name or User Role</span></span>

<span data-ttu-id="3ba62-154">[承認] 属性を使用して、コントローラーアクションへのアクセスを特定のユーザーセットまたは特定のユーザーロールのセットに制限することができます。</span><span class="sxs-lookup"><span data-stu-id="3ba62-154">You can use the [Authorize] attribute to restrict access to a controller action to a particular set of users or a particular set of user roles.</span></span> <span data-ttu-id="3ba62-155">たとえば、リスト2の変更されたホームコントローラーには、StephenSecrets () と [アドミニストレーターシークレット ()] という2つの新しいアクションが含まれています。</span><span class="sxs-lookup"><span data-stu-id="3ba62-155">For example, the modified Home controller in Listing 2 contains two new actions named StephenSecrets() and AdministratorSecrets().</span></span>

<span data-ttu-id="3ba62-156">**リスト2– Controllers\ homecontroller.cs**</span><span class="sxs-lookup"><span data-stu-id="3ba62-156">**Listing 2 – Controllers\HomeController.cs**</span></span>

[!code-csharp[Main](authenticating-users-with-forms-authentication-cs/samples/sample2.cs)]

<span data-ttu-id="3ba62-157">ユーザー名 Stephen を持つユーザーのみが StephenSecrets () アクションを呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="3ba62-157">Only a user with the user name Stephen can invoke the StephenSecrets() action.</span></span> <span data-ttu-id="3ba62-158">他のすべてのユーザーは、ログインビューにリダイレクトされます。</span><span class="sxs-lookup"><span data-stu-id="3ba62-158">All other users get redirected to the Login view.</span></span> <span data-ttu-id="3ba62-159">Users プロパティは、ユーザーアカウント名のコンマ区切りの一覧を受け取ります。</span><span class="sxs-lookup"><span data-stu-id="3ba62-159">The Users property accepts a comma separated list of user account names.</span></span>

<span data-ttu-id="3ba62-160">管理者のシークレット () アクションを呼び出すことができるのは、Administrators ロールのユーザーだけです。</span><span class="sxs-lookup"><span data-stu-id="3ba62-160">Only users in the Administrators role can invoke the AdministratorSecrets() action.</span></span> <span data-ttu-id="3ba62-161">たとえば、ユーザーが管理者グループのメンバーである場合、管理者のシークレット () アクションを呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="3ba62-161">For example, because Sally is a member of the Administrators group, she can invoke the AdministratorSecrets() action.</span></span> <span data-ttu-id="3ba62-162">他のすべてのユーザーは、ログインビューにリダイレクトされます。</span><span class="sxs-lookup"><span data-stu-id="3ba62-162">All other users get redirected to the Login view.</span></span> <span data-ttu-id="3ba62-163">Roles プロパティは、ロール名のコンマ区切りリストを受け入れます。</span><span class="sxs-lookup"><span data-stu-id="3ba62-163">The Roles property accepts a comma separated list of role names.</span></span>

#### <a name="configuring-authentication"></a><span data-ttu-id="3ba62-164">認証の構成</span><span class="sxs-lookup"><span data-stu-id="3ba62-164">Configuring Authentication</span></span>

<span data-ttu-id="3ba62-165">この時点で、ユーザーアカウントとロール情報が保存されている場所について疑問に思うかもしれません。</span><span class="sxs-lookup"><span data-stu-id="3ba62-165">At this point, you might be wondering where the user account and role information is being stored.</span></span> <span data-ttu-id="3ba62-166">既定では、情報は、MVC アプリケーションの App\_Data フォルダーにある ASPNETDB.MDF という名前の (RANU) SQL Express データベースに格納されます。</span><span class="sxs-lookup"><span data-stu-id="3ba62-166">By default, the information is stored in a (RANU) SQL Express database named ASPNETDB.mdf located in your MVC application's App\_Data folder.</span></span> <span data-ttu-id="3ba62-167">このデータベースは、メンバーシップの使用を開始すると、ASP.NET フレームワークによって自動的に生成されます。</span><span class="sxs-lookup"><span data-stu-id="3ba62-167">This database is generated by the ASP.NET framework automatically when you start using membership.</span></span>

<span data-ttu-id="3ba62-168">ソリューションエクスプローラーウィンドウで ASPNETDB.MDF データベースを表示するには、まずメニューオプションプロジェクト [すべてのファイルを表示] を選択する必要があります。</span><span class="sxs-lookup"><span data-stu-id="3ba62-168">In order to see the ASPNETDB.mdf database in the Solution Explorer window, you first need to select the menu option Project, Show All Files.</span></span>

<span data-ttu-id="3ba62-169">アプリケーションを開発する場合は、既定の SQL Express データベースを使用するのが適切です。</span><span class="sxs-lookup"><span data-stu-id="3ba62-169">Using the default SQL Express database is fine when developing an application.</span></span> <span data-ttu-id="3ba62-170">ただし、ほとんどの場合、実稼働アプリケーションで既定の ASPNETDB.MDF データベースを使用する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="3ba62-170">Most likely, however, you won't want to use the default ASPNETDB.mdf database for a production application.</span></span> <span data-ttu-id="3ba62-171">その場合は、次の2つの手順を実行して、ユーザーアカウント情報の保存場所を変更できます。</span><span class="sxs-lookup"><span data-stu-id="3ba62-171">In that case, you can change where user account information is stored by completing the following two steps:</span></span>

1. <span data-ttu-id="3ba62-172">実稼働データベースにアプリケーションサービスデータベースオブジェクトを追加する-実稼働データベースを指すようにアプリケーションの接続文字列を変更する</span><span class="sxs-lookup"><span data-stu-id="3ba62-172">Add the Application Services database objects to your production database - Change your application connection string to point to your production database</span></span>

<span data-ttu-id="3ba62-173">最初の手順では、必要なすべてのデータベースオブジェクト (テーブルとストアドプロシージャ) を実稼働データベースに追加します。</span><span class="sxs-lookup"><span data-stu-id="3ba62-173">The first step is to add all of the necessary database objects (tables and stored procedures) to your production database.</span></span> <span data-ttu-id="3ba62-174">これらのオブジェクトを新しいデータベースに追加する最も簡単な方法は、ASP.NET SQL Server セットアップウィザードを利用することです (図8を参照)。</span><span class="sxs-lookup"><span data-stu-id="3ba62-174">The easiest way to add these objects to a new database is to take advantage of the ASP.NET SQL Server Setup Wizard (see Figure 8).</span></span> <span data-ttu-id="3ba62-175">このツールを起動するには、Microsoft Visual Studio 2008 プログラムグループから Visual Studio 2008 コマンドプロンプトを開き、コマンドプロンプトから次のコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="3ba62-175">You can launch this tool by opening the Visual Studio 2008 Command Prompt from the Microsoft Visual Studio 2008 program group and executing the following command from the command prompt:</span></span>

<span data-ttu-id="3ba62-176">aspnet\_regsql</span><span class="sxs-lookup"><span data-stu-id="3ba62-176">aspnet\_regsql</span></span>

<span data-ttu-id="3ba62-177">**図 8-ASP.NET SQL Server セットアップウィザード**</span><span class="sxs-lookup"><span data-stu-id="3ba62-177">**Figure 8 – The ASP.NET SQL Server Setup Wizard**</span></span>

![clip_image016](authenticating-users-with-forms-authentication-cs/_static/image8.jpg)

<span data-ttu-id="3ba62-179">ASP.NET SQL Server セットアップウィザードでは、ネットワーク上の SQL Server データベースを選択し、ASP.NET アプリケーションサービスに必要なすべてのデータベースオブジェクトをインストールすることができます。</span><span class="sxs-lookup"><span data-stu-id="3ba62-179">The ASP.NET SQL Server Setup Wizard enables you to select a SQL Server database on your network and install all of the database objects required by the ASP.NET application services.</span></span> <span data-ttu-id="3ba62-180">データベースサーバーがローカルコンピューターに配置されている必要はありません。</span><span class="sxs-lookup"><span data-stu-id="3ba62-180">The database server is not required to be located on your local machine.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="3ba62-181">ASP.NET SQL Server セットアップウィザードを使用しない場合は、次のフォルダーにアプリケーションサービスデータベースオブジェクトを追加するための SQL スクリプトを見つけることができます。</span><span class="sxs-lookup"><span data-stu-id="3ba62-181">If you don't want to use the ASP.NET SQL Server Setup Wizard, then you can find SQL scripts for adding the application services database objects in the following folder:</span></span>
> 
> > <span data-ttu-id="3ba62-182">C:\Windows\Microsoft.NET\Framework\v2.0.50727</span><span class="sxs-lookup"><span data-stu-id="3ba62-182">C:\Windows\Microsoft.NET\Framework\v2.0.50727</span></span>

<span data-ttu-id="3ba62-183">必要なデータベースオブジェクトを作成した後、MVC アプリケーションで使用されるデータベース接続を変更する必要があります。</span><span class="sxs-lookup"><span data-stu-id="3ba62-183">After you create the necessary database objects, you need to modify the database connection used by your MVC application.</span></span> <span data-ttu-id="3ba62-184">Web 構成 (web.config) ファイル内の ApplicationServices 接続文字列を変更して、実稼働データベースをポイントするようにします。</span><span class="sxs-lookup"><span data-stu-id="3ba62-184">Modify the ApplicationServices connection string in your web configuration (web.config) file so that it points to the production database.</span></span> <span data-ttu-id="3ba62-185">たとえば、リスト3の変更された接続は、MyProductionDB という名前のデータベースを指しています (元の ApplicationServices 接続文字列はコメントアウトされています)。</span><span class="sxs-lookup"><span data-stu-id="3ba62-185">For example, the modified connection in Listing 3 points to a database named MyProductionDB (the original ApplicationServices connection string has been commented out).</span></span>

<span data-ttu-id="3ba62-186">**リスト3– web.config**</span><span class="sxs-lookup"><span data-stu-id="3ba62-186">**Listing 3 – Web.config**</span></span>

[!code-xml[Main](authenticating-users-with-forms-authentication-cs/samples/sample3.xml)]

#### <a name="configuring-database-permissions"></a><span data-ttu-id="3ba62-187">データベースのアクセス許可の構成</span><span class="sxs-lookup"><span data-stu-id="3ba62-187">Configuring Database Permissions</span></span>

<span data-ttu-id="3ba62-188">統合セキュリティを使用してデータベースに接続する場合は、正しい Windows ユーザーアカウントをログインとしてデータベースに追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="3ba62-188">If you use Integrated Security to connect to your database then you will need to add the correct Windows user account as a login to your database.</span></span> <span data-ttu-id="3ba62-189">正しいアカウントは、web サーバーとして ASP.NET 開発サーバーまたはインターネットインフォメーションサービスのどちらを使用しているかによって異なります。</span><span class="sxs-lookup"><span data-stu-id="3ba62-189">The correct account depends on whether you are using the ASP.NET Development Server or Internet Information Services as your web server.</span></span> <span data-ttu-id="3ba62-190">正しいユーザーアカウントは、使用しているオペレーティングシステムにも依存します。</span><span class="sxs-lookup"><span data-stu-id="3ba62-190">The correct user account also depends on your operating system.</span></span>

<span data-ttu-id="3ba62-191">ASP.NET 開発サーバー (Visual Studio で使用される既定の web サーバー) を使用している場合、アプリケーションは Windows ユーザーアカウントのコンテキスト内で実行されます。</span><span class="sxs-lookup"><span data-stu-id="3ba62-191">If you are using the ASP.NET Development Server (the default web server used by Visual Studio) then your application executes within the context of your Windows user account.</span></span> <span data-ttu-id="3ba62-192">その場合は、Windows ユーザーアカウントをデータベースサーバーログインとして追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="3ba62-192">In that case, you need to add your Windows user account as a database server login.</span></span>

<span data-ttu-id="3ba62-193">または、インターネットインフォメーションサービスを使用する場合は、ASPNET アカウントまたは NT AUTHORITY/NETWORK サービスアカウントをデータベースサーバーログインとして追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="3ba62-193">Alternatively, if you are using Internet Information Services then you need to add either the ASPNET account or the NT AUTHORITY/NETWORK SERVICE account as a database server login.</span></span> <span data-ttu-id="3ba62-194">Windows XP を使用している場合は、ASPNET アカウントをログインとしてデータベースに追加します。</span><span class="sxs-lookup"><span data-stu-id="3ba62-194">If you are using Windows XP then add the ASPNET account as a login to your database.</span></span> <span data-ttu-id="3ba62-195">Windows Vista や Windows Server 2008 など、より新しいオペレーティングシステムを使用している場合は、データベースログインとして NT AUTHORITY/NETWORK SERVICE アカウントを追加します。</span><span class="sxs-lookup"><span data-stu-id="3ba62-195">If you are using a more recent operating system, such as Windows Vista or Windows Server 2008, then add the NT AUTHORITY/NETWORK SERVICE account as the database login.</span></span>

<span data-ttu-id="3ba62-196">Microsoft SQL Server Management Studio を使用して、新しいユーザーアカウントをデータベースに追加できます (図9を参照)。</span><span class="sxs-lookup"><span data-stu-id="3ba62-196">You can add a new user account to your database by using Microsoft SQL Server Management Studio (see Figure 9).</span></span>

<span data-ttu-id="3ba62-197">**図9–新しい Microsoft SQL Server ログインを作成する**</span><span class="sxs-lookup"><span data-stu-id="3ba62-197">**Figure 9 – Creating a new Microsoft SQL Server login**</span></span>

![clip_image018](authenticating-users-with-forms-authentication-cs/_static/image9.jpg)

<span data-ttu-id="3ba62-199">必要なログインを作成した後、適切なデータベースロールを持つデータベースユーザーにログインをマップする必要があります。</span><span class="sxs-lookup"><span data-stu-id="3ba62-199">After you create the required login, you need to map the login to a database user with the right database roles.</span></span> <span data-ttu-id="3ba62-200">ログインをダブルクリックし、[ユーザーマッピング] タブを選択します。1つまたは複数のアプリケーションサービスデータベースロールを選択します。</span><span class="sxs-lookup"><span data-stu-id="3ba62-200">Double-click the login and select the User Mapping tab. Select one or more application services database roles.</span></span> <span data-ttu-id="3ba62-201">たとえば、ユーザーを認証するには、aspnet\_メンバーシップ\_BasicAccess データベースロールを有効にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="3ba62-201">For example, in order to authenticate users, you need to enable the aspnet\_Membership\_BasicAccess database role.</span></span> <span data-ttu-id="3ba62-202">新しいユーザーを作成するには、aspnet\_メンバーシップ\_FullAccess データベースロールを有効にする必要があります (図10を参照)。</span><span class="sxs-lookup"><span data-stu-id="3ba62-202">In order to create new users, you need to enable the aspnet\_Membership\_FullAccess database role (see Figure 10).</span></span>

<span data-ttu-id="3ba62-203">**図 10-アプリケーションサービスデータベースロールの追加**</span><span class="sxs-lookup"><span data-stu-id="3ba62-203">**Figure 10 – Adding Application Services database roles**</span></span>

![clip_image020](authenticating-users-with-forms-authentication-cs/_static/image10.jpg)

#### <a name="summary"></a><span data-ttu-id="3ba62-205">まとめ</span><span class="sxs-lookup"><span data-stu-id="3ba62-205">Summary</span></span>

<span data-ttu-id="3ba62-206">このチュートリアルでは、ASP.NET MVC アプリケーションを構築するときにフォーム認証を使用する方法について学習しました。</span><span class="sxs-lookup"><span data-stu-id="3ba62-206">In this tutorial, you learned how to use Forms authentication when building an ASP.NET MVC application.</span></span> <span data-ttu-id="3ba62-207">まず、Web サイト管理ツールを利用して、新しいユーザーとロールを作成する方法を学習しました。</span><span class="sxs-lookup"><span data-stu-id="3ba62-207">First, you learned how to create new users and roles by taking advantage of the Web Site Administration Tool.</span></span> <span data-ttu-id="3ba62-208">次に、[承認] 属性を使用して、承認されていないユーザーがコントローラーアクションを呼び出さないようにする方法を学習しました。</span><span class="sxs-lookup"><span data-stu-id="3ba62-208">Next, you learned how to use the [Authorize] attribute to prevent unauthorized users from invoking controller actions.</span></span> <span data-ttu-id="3ba62-209">最後に、ユーザーとロールの情報を運用データベースに格納するように MVC アプリケーションを構成する方法について学習しました。</span><span class="sxs-lookup"><span data-stu-id="3ba62-209">Finally, you learned how to configure your MVC application to store user and role information in a production database.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="3ba62-210">Next</span><span class="sxs-lookup"><span data-stu-id="3ba62-210">Next</span></span>](authenticating-users-with-windows-authentication-cs.md)
