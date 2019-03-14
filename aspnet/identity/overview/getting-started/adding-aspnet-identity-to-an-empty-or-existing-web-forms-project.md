---
uid: identity/overview/getting-started/adding-aspnet-identity-to-an-empty-or-existing-web-forms-project
title: ASP.NET Identity を空または既存の web フォーム プロジェクトの追加 |Microsoft Docs
author: raquelsa
description: このチュートリアルでは、ASP.NET アプリケーションを ASP.NET Identity (ASP.NET の新しいメンバーシップ システム) を追加する方法を示します。 ときに、新しい Web フォームまたは MVC を作成しています.
ms.author: riande
ms.date: 01/22/2019
ms.assetid: 1cbc0ed2-5bd6-4b62-8d34-4c193dcd8b25
msc.legacyurl: /identity/overview/getting-started/adding-aspnet-identity-to-an-empty-or-existing-web-forms-project
msc.type: authoredcontent
ms.openlocfilehash: cd28cc68db96b52eb205b8764aa2af014ffad9c3
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57038279"
---
# <a name="adding-aspnet-identity-to-an-empty-or-existing-web-forms-project"></a><span data-ttu-id="6aaf2-104">ASP.NET Identity を空または既存の Web フォーム プロジェクトに追加する</span><span class="sxs-lookup"><span data-stu-id="6aaf2-104">Adding ASP.NET Identity to an Empty or Existing Web Forms Project</span></span>


> <span data-ttu-id="6aaf2-105">このチュートリアルは、追加する方法を示します[ASP.NET Identity](introduction-to-aspnet-identity.md) (ASP.NET の新しいメンバーシップ システム) を ASP.NET アプリケーション。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-105">This tutorial shows you how to add [ASP.NET Identity](introduction-to-aspnet-identity.md) (the new membership system for ASP.NET) to an ASP.NET application.</span></span>
> 
> <span data-ttu-id="6aaf2-106">Visual Studio 2017 の RTM が個々 のアカウントで新しい Web フォームまたは MVC プロジェクトを作成するときに、Visual Studio は、必要なすべてのパッケージをインストールし、必要なすべてのクラスを追加します。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-106">When you create a new Web Forms or MVC project in Visual Studio 2017 RTM with Individual Accounts, Visual Studio will install all the required packages and add all necessary classes for you.</span></span> <span data-ttu-id="6aaf2-107">このチュートリアルでは、ASP.NET Identity のサポートを既存の Web フォーム プロジェクトまたは新しい空のプロジェクトに追加する手順について説明します。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-107">This tutorial will illustrate the steps to add ASP.NET Identity support to your existing Web Forms project or a new empty project.</span></span> <span data-ttu-id="6aaf2-108">すべての NuGet のパッケージをインストールする必要があるとを追加する必要があるクラスについて説明されます。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-108">I will outline all the NuGet packages you need to install, and classes you need to add.</span></span> <span data-ttu-id="6aaf2-109">新しいユーザーを登録すると、ログイン ユーザーの管理と認証のためのすべてのメイン エントリ ポイントの Api を強調表示し、サンプルの Web フォームは経由されます。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-109">I will go over sample Web Forms for registering new users and logging in while highlighting all main entry point APIs for user management and authentication.</span></span> <span data-ttu-id="6aaf2-110">このサンプルは Entity Framework に組み込まれている SQL データ ストレージの既定の ASP.NET Identity の実装を使用します。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-110">This sample will use the ASP.NET Identity default implementation for SQL data storage which is built on Entity Framework.</span></span> <span data-ttu-id="6aaf2-111">このチュートリアルでは、SQL database の LocalDB を使用します。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-111">This tutorial, we will use LocalDB for the SQL database.</span></span>
> 

## <a name="get-started-with-aspnet-identity"></a><span data-ttu-id="6aaf2-112">ASP.NET Identity を概要します。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-112">Get started with ASP.NET Identity</span></span>

1. <span data-ttu-id="6aaf2-113">インストールと実行によって開始[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/)します。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-113">Start by installing and running [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="6aaf2-114">選択**新しいプロジェクト**開始から ページで、またはメニューを使用して選択します**ファイル**、し**新しいプロジェクト**します。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-114">Select **New Project** from the Start page, or you can use the menu and select **File**, and then **New Project**.</span></span>
3. <span data-ttu-id="6aaf2-115">左側のウィンドウで展開**Visual C#** を選択し、 **Web**、し**ASP.NET Web アプリケーション (.Net Framework)** します。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-115">In the left pane, expand **Visual C#**, then select **Web**, then **ASP.NET Web Application (.Net Framework)**.</span></span> <span data-ttu-id="6aaf2-116">プロジェクトに名前を"WebFormsIdentity"選び**OK**します。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-116">Name your project "WebFormsIdentity" and select **OK**.</span></span>
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image17.png)
4. <span data-ttu-id="6aaf2-117">**新しい ASP.NET プロジェクト**ダイアログ ボックスで、**空**テンプレート。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-117">In the **New ASP.NET Project** dialog, select the **Empty** template.</span></span>
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image2.png)  
  
   <span data-ttu-id="6aaf2-118">通知、**認証の変更**ボタンが無効になり、このテンプレートでの認証のサポートは提供されません。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-118">Notice the **Change Authentication** button is disabled and no authentication support is provided in this template.</span></span> <span data-ttu-id="6aaf2-119">Web フォーム、MVC、Web API テンプレートを使用すると、認証方法を選択することができます。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-119">The Web Forms, MVC and Web API templates allow you to select the authentication approach.</span></span>

## <a name="add-identity-packages-to-your-app"></a><span data-ttu-id="6aaf2-120">アプリへの Identity のパッケージを追加します。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-120">Add Identity packages to your app</span></span>

<span data-ttu-id="6aaf2-121">ソリューション エクスプ ローラーでプロジェクトを右クリックし、選択**NuGet パッケージの管理**します。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-121">In Solution Explorer, right-click your project and select **Manage NuGet Packages**.</span></span> <span data-ttu-id="6aaf2-122">検索し、インストール、 **Microsoft.AspNet.Identity.EntityFramework**パッケージ。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-122">Search for and install the **Microsoft.AspNet.Identity.EntityFramework** package.</span></span> 
  
![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image15.png)
  
<span data-ttu-id="6aaf2-123">このパッケージが依存関係パッケージをインストールすることに注意してください。**EntityFramework**と**Microsoft ASP.NET Identity に Core**します。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-123">Note that this package will install the dependency packages: **EntityFramework** and **Microsoft ASP.NET Identity Core**.</span></span>

## <a name="add-a-web-form-to-register-users"></a><span data-ttu-id="6aaf2-124">ユーザーを登録する web フォームを追加します。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-124">Add a web form to register users</span></span>

1. <span data-ttu-id="6aaf2-125">**ソリューション エクスプ ローラー**プロジェクトを右クリックし、選択、**追加**、し**Web フォーム**します。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-125">In **Solution Explorer**, right-click your project and select **Add**, and then **Web Form**.</span></span>
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image4.png)
2. <span data-ttu-id="6aaf2-126">**項目の名前を指定**] ダイアログ ボックスで、名前の新しい web フォーム**登録**、し、[ **[ok]**</span><span class="sxs-lookup"><span data-stu-id="6aaf2-126">In the **Specify Name for Item** dialog box, name the new web form **Register**, and then select **OK**</span></span>
3. <span data-ttu-id="6aaf2-127">生成されたマークアップを置き換えます*Register.aspx*次のコードでのファイル。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-127">Replace the markup in the generated *Register.aspx* file with the code below.</span></span> <span data-ttu-id="6aaf2-128">コードの変更が強調表示されています。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-128">The code changes are highlighted.</span></span> 

    [!code-html[Main](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/samples/sample1.aspx?highlight=9,12-40)]

    > [!NOTE]
    > <span data-ttu-id="6aaf2-129">これは簡略化されたバージョンののみ、 *Register.aspx*新しい ASP.NET Web フォーム プロジェクトを作成するときに作成されるファイル。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-129">This is just a simplified version of the *Register.aspx* file that is created when you create a new ASP.NET Web Forms project.</span></span> <span data-ttu-id="6aaf2-130">上記のマークアップは、フォーム フィールドと新しいユーザーを登録するためのボタンを追加します。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-130">The markup above adds form fields and a button to register a new user.</span></span>
4. <span data-ttu-id="6aaf2-131">開く、 *Register.aspx.cs*ファイルを開き、ファイルの内容を次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-131">Open the *Register.aspx.cs* file and replace the contents of the file with the following code:</span></span>

    [!code-csharp[Main](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/samples/sample2.cs)]

    > [!NOTE] 
    > 
    > 1. <span data-ttu-id="6aaf2-132">上記のコードが簡略化されたバージョンの*Register.aspx.cs*新しい ASP.NET Web フォーム プロジェクトを作成するときに作成されるファイル。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-132">The code above is a simplified version of the *Register.aspx.cs* file that is created when you create a new ASP.NET Web Forms project.</span></span>
    > 2. <span data-ttu-id="6aaf2-133">*IdentityUser*クラスは、の既定の EntityFramework 実装、 *IUser*インターフェイス。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-133">The *IdentityUser* class is the default EntityFramework implementation of the *IUser* interface.</span></span> <span data-ttu-id="6aaf2-134">*IUser*インターフェイスは Asp.net Identity のユーザーの最小限のインターフェイスです。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-134">*IUser* interface is the minimal interface for a user on ASP.NET Identity Core.</span></span>
    > 3. <span data-ttu-id="6aaf2-135">*UserStore*クラスは、ユーザー ストアの既定の EntityFramework 実装します。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-135">The *UserStore* class is the default EntityFramework implementation of a user store.</span></span> <span data-ttu-id="6aaf2-136">このクラスは、Asp.net Identity の最小限のインターフェイスを実装します。*IUserStore*、 *IUserLoginStore*、 *IUserClaimStore*と*IUserRoleStore*します。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-136">This class implements the ASP.NET Identity Core's minimal interfaces: *IUserStore*, *IUserLoginStore*, *IUserClaimStore* and *IUserRoleStore*.</span></span>
    > 4. <span data-ttu-id="6aaf2-137">*UserManager*への変更が自動的に保存するクラスが公開ユーザー関連 Api、 *UserStore*します。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-137">The *UserManager* class exposes user related APIs which will automatically save changes to the *UserStore*.</span></span>
    > 5. <span data-ttu-id="6aaf2-138">*IdentityResult*クラス id 操作の結果を表します。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-138">The *IdentityResult* class represents the result of an identity operation.</span></span>
5. <span data-ttu-id="6aaf2-139">**ソリューション エクスプ ローラー**プロジェクトを右クリックし、選択、**追加**、 **ASP.NET フォルダーの追加**し**アプリ\_データ**します。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-139">In **Solution Explorer**, right-click your project and select **Add**, **Add ASP.NET Folder** and then **App\_Data**.</span></span>
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image5.png)
6. <span data-ttu-id="6aaf2-140">開く、 *Web.config*ファイルし、ユーザー情報を使用して、データベースの接続文字列のエントリを追加します。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-140">Open the *Web.config* file and add a connection string entry for the database we will use to store user information.</span></span> <span data-ttu-id="6aaf2-141">データベースは、その EntityFramework で Identity エンティティのランタイムで作成されます。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-141">The database will be created at runtime by EntityFramework for the Identity entities.</span></span> <span data-ttu-id="6aaf2-142">接続文字列は、1 つの新しい Web フォーム プロジェクトを作成するときに作成に似ています。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-142">The connection string is similar to one created for you when you create a new Web Forms project.</span></span> <span data-ttu-id="6aaf2-143">強調表示されたコードは、追加する必要があります、マークアップを示しています。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-143">The highlighted code shows the markup you should add:</span></span>

    [!code-xml[Main](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/samples/sample3.xml?highlight=11-14)]
    
    > [!NOTE] 
    > <span data-ttu-id="6aaf2-144">Visual Studio 2015 以降では、または置換`(localdb)\v11.0`で`(localdb)\MSSQLLocalDB`の接続文字列。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-144">For Visual Studio 2015 or higher, replace `(localdb)\v11.0` with `(localdb)\MSSQLLocalDB` in your connection string.</span></span>
    
7. <span data-ttu-id="6aaf2-145">ファイルを右クリックして*Register.aspx*プロジェクトを選び、**スタート ページとして設定**します。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-145">Right click file *Register.aspx* in your project and select **Set as Start Page**.</span></span> <span data-ttu-id="6aaf2-146">ビルドして、web アプリケーションを実行するには、ctrl キーを押しながら F5 キーを押します。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-146">Press Ctrl + F5 to build and run the web application.</span></span> <span data-ttu-id="6aaf2-147">新しいユーザー名とパスワードを入力し、選択**登録**します。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-147">Enter a new user name and password and then select **Register**.</span></span>
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image6.png)  

    > [!NOTE]
    > <span data-ttu-id="6aaf2-148">ASP.NET の Id が検証をサポートし、このサンプルでは、ユーザー名とパスワードの既定の動作を確認することができます、Identity コア パッケージに由来する検証コントロール。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-148">ASP.NET Identity has support for validation and in this sample you can verify the default behavior on User and Password validators that come from the Identity Core package.</span></span> <span data-ttu-id="6aaf2-149">ユーザーの既定の検証コントロール (`UserValidator`) プロパティを持つ`AllowOnlyAlphanumericUserNames`に設定する既定値を持つ`true`します。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-149">The default validator for User (`UserValidator`) has a property `AllowOnlyAlphanumericUserNames` that has default value set to `true`.</span></span> <span data-ttu-id="6aaf2-150">既定のパスワードの検証コントロール (`MinimumLengthValidator`) により、そのパスワードが 6 文字以上にします。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-150">The default validator for Password (`MinimumLengthValidator`) ensures that password has at least 6 characters.</span></span> <span data-ttu-id="6aaf2-151">これらの検証コントロールのプロパティを`UserManager`カスタムの検証を用意する場合をオーバーライドすることができます</span><span class="sxs-lookup"><span data-stu-id="6aaf2-151">These validators are properties on `UserManager` that can be overridden if you want to have custom validation,</span></span>

## <a name="verify-the-localdb-identity-database-and-tables-generated-by-entity-framework"></a><span data-ttu-id="6aaf2-152">LocalDb の Id データベースと Entity Framework によって生成されたテーブルを確認します。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-152">Verify the LocalDb Identity database and tables generated by Entity Framework</span></span>

1. <span data-ttu-id="6aaf2-153">**ビュー**メニューの **サーバー エクスプ ローラー**します。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-153">In the **View** menu, select **Server Explorer**.</span></span>
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image7.png)
2. <span data-ttu-id="6aaf2-154">展開**DefaultConnection (WebFormsIdentity)**、展開**テーブル**を右クリックして**AspNetUsers**選び**テーブル データの表示**します。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-154">Expand **DefaultConnection (WebFormsIdentity)**, expand **Tables**, right-click **AspNetUsers** and then select **Show Table Data**.</span></span>
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image8.png)  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image9.png)

## <a name="configure-the-application-for-owin-authentication"></a><span data-ttu-id="6aaf2-155">OWIN 認証のアプリケーションを構成します。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-155">Configure the application for OWIN authentication</span></span>

<span data-ttu-id="6aaf2-156">この時点でユーザーを作成するためのサポートのみが追加されました。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-156">At this point we have only added support for creating users.</span></span> <span data-ttu-id="6aaf2-157">ここで、ユーザーのログインの認証を追加する方法を示すためにここ。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-157">Now, we are going to demonstrate how we can add authentication to login a user.</span></span> <span data-ttu-id="6aaf2-158">ASP.NET Identity では、Microsoft の OWIN 認証ミドルウェアを使用してフォーム認証。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-158">ASP.NET Identity uses Microsoft OWIN Authentication middleware for forms authentication.</span></span> <span data-ttu-id="6aaf2-159">OWIN クッキー認証 cookie、クレーム ベースの認証メカニズムでホストされている任意のフレームワークで使用できる[OWIN](https://msdn.microsoft.com/magazine/dn451439.aspx)または IIS です。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-159">The OWIN Cookie Authentication is a cookie and claims based authentication mechanism that can be used by any framework hosted on [OWIN](https://msdn.microsoft.com/magazine/dn451439.aspx) or IIS.</span></span> <span data-ttu-id="6aaf2-160">このモデルでは、同じ認証パッケージは、ASP.NET MVC と Web フォームを含む複数のフレームワーク全体で使用できます。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-160">With this model, the same authentication packages can be used across multiple frameworks including ASP.NET MVC and Web Forms.</span></span> <span data-ttu-id="6aaf2-161">プロジェクト Katana とホストに依存しない参照でミドルウェアを実行する方法の詳細については[Katana プロジェクトの概要](https://msdn.microsoft.com/magazine/dn451439.aspx)します。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-161">For more information on project Katana and how to run middleware in a host agnostic see [Getting Started with the Katana Project](https://msdn.microsoft.com/magazine/dn451439.aspx).</span></span>

## <a name="install-authentication-packages-to-your-application"></a><span data-ttu-id="6aaf2-162">アプリケーションに認証パッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-162">Install authentication packages to your application</span></span>

1. <span data-ttu-id="6aaf2-163">ソリューション エクスプ ローラーでプロジェクトを右クリックし、選択**NuGet パッケージの管理**します。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-163">In Solution Explorer, right-click your project and select **Manage NuGet Packages**.</span></span> <span data-ttu-id="6aaf2-164">検索し、インストール、 ***Microsoft.AspNet.Identity.Owin***パッケージ。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-164">Search for and install the ***Microsoft.AspNet.Identity.Owin*** package.</span></span> 
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image16.png)

2. <span data-ttu-id="6aaf2-165">検索し、インストール、 ***Microsoft.Owin.Host.SystemWeb***パッケージ。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-165">Search for and install the ***Microsoft.Owin.Host.SystemWeb*** package.</span></span>

    > [!NOTE]
    > <span data-ttu-id="6aaf2-166">**Microsoft.Aspnet.Identity.Owin**パッケージには、一連管理および ASP.NET Identity のコア パッケージで使用する OWIN 認証ミドルウェアを構成する OWIN 拡張機能のクラスにはが含まれています。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-166">The **Microsoft.Aspnet.Identity.Owin** package contains a set of OWIN extension classes to manage and configure OWIN authentication middleware to be consumed by ASP.NET Identity Core packages.</span></span>
    > <span data-ttu-id="6aaf2-167">**Microsoft.Owin.Host.SystemWeb**パッケージには、OWIN ベース アプリケーションを ASP.NET の要求パイプラインを使用して、IIS で実行できるようにする OWIN サーバーが含まれています。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-167">The **Microsoft.Owin.Host.SystemWeb** package contains an OWIN server that enables OWIN-based applications to run on IIS using the ASP.NET request pipeline.</span></span> <span data-ttu-id="6aaf2-168">詳細については、次を参照してください。 [、IIS での OWIN ミドルウェア パイプラインを統合する](../../../aspnet/overview/owin-and-katana/owin-middleware-in-the-iis-integrated-pipeline.md)します。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-168">For more information see [OWIN Middleware in the IIS integrated pipeline](../../../aspnet/overview/owin-and-katana/owin-middleware-in-the-iis-integrated-pipeline.md).</span></span>

## <a name="add-owin-startup-and-authentication-configuration-classes"></a><span data-ttu-id="6aaf2-169">OWIN の起動と認証の構成クラスを追加します。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-169">Add OWIN startup and authentication configuration classes</span></span>

1. <span data-ttu-id="6aaf2-170">**ソリューション エクスプ ローラー**、プロジェクトを右クリックし、選択**追加**、し**新しい項目の追加**します。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-170">In **Solution Explorer**, right-click your project, select **Add**, and then **Add New Item**.</span></span> <span data-ttu-id="6aaf2-171">検索テキスト ボックス ダイアログ ボックスで次のように入力します。"*owin*"。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-171">In the search text box dialog, type "*owin*".</span></span> <span data-ttu-id="6aaf2-172">クラスの名前"*スタートアップ*"を選択および**追加**します。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-172">Name the class "*Startup*" and select **Add**.</span></span> 
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image11.png)
2. <span data-ttu-id="6aaf2-173">Startup.cs ファイルでは、OWIN クッキー認証の構成を次に示す強調表示されたコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-173">In the Startup.cs file, add the highlighted code shown below to configure OWIN cookie authentication.</span></span>

    [!code-csharp[Main](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/samples/sample4.cs?highlight=1,3,15-19)]

    > [!NOTE]
    > <span data-ttu-id="6aaf2-174">このクラスが含まれています、 `OwinStartup` OWIN スタートアップ クラスを指定するための属性。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-174">This class contains the `OwinStartup` attribute for specifying the OWIN startup class.</span></span> <span data-ttu-id="6aaf2-175">すべての OWIN アプリケーションには、アプリケーション パイプラインのコンポーネントを指定するスタートアップ クラスがあります。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-175">Every OWIN application has a startup class where you specify components for the application pipeline.</span></span> <span data-ttu-id="6aaf2-176">参照してください[OWIN スタートアップ クラス検出](../../../aspnet/overview/owin-and-katana/owin-startup-class-detection.md)このモデルの詳細について。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-176">See [OWIN Startup Class Detection](../../../aspnet/overview/owin-and-katana/owin-startup-class-detection.md) for more info on this model.</span></span>

## <a name="add-web-forms-for-registering-and-signing-in-users"></a><span data-ttu-id="6aaf2-177">Web フォームを登録して、ユーザーのサインインを追加します。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-177">Add web forms for registering and signing in users</span></span>

1. <span data-ttu-id="6aaf2-178">開く、 *Register.aspx.cs*ファイルし、登録が成功したときに、次のコードをサインインするユーザーを追加します。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-178">Open the *Register.aspx.cs* file and add the following code which signs in the user when registration succeeds.</span></span>

    [!code-csharp[Main](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/samples/sample5.cs)]

    > [!NOTE] 
    > 
    > - <span data-ttu-id="6aaf2-179">フレームワークに生成するアプリの開発者が必要です ASP.NET Identity と OWIN クッキー認証は要求ベースのシステムであるため、 [ClaimsIdentity](https://msdn.microsoft.com/library/microsoft.identitymodel.claims.claimsidentity.aspx)ユーザー。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-179">Since ASP.NET Identity and OWIN Cookie Authentication are claims based system, the framework requires the app developer to generate a [ClaimsIdentity](https://msdn.microsoft.com/library/microsoft.identitymodel.claims.claimsidentity.aspx) for the user.</span></span> <span data-ttu-id="6aaf2-180">ClaimsIdentity には、ユーザーが属するロールなど、ユーザーのすべての要求についての情報があります。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-180">ClaimsIdentity has information about all the claims for the user such as what Roles the user belongs to.</span></span> <span data-ttu-id="6aaf2-181">この段階でユーザーの複数のクレームを追加することもできます。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-181">You can also add more claims for the user at this stage.</span></span>
    > - <span data-ttu-id="6aaf2-182">ユーザーをサインインするには、OWIN と呼び出し元から AuthenticationManager を使用して`SignIn`ClaimsIdentity 上記のように渡すとします。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-182">You can sign in the user by using the AuthenticationManager from OWIN and calling `SignIn` and passing in the ClaimsIdentity as shown above.</span></span> <span data-ttu-id="6aaf2-183">このコードは、ユーザーがサインインし、cookie も生成します。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-183">This code will sign in the user and generate a cookie as well.</span></span> <span data-ttu-id="6aaf2-184">この呼び出しに似ています[FormAuthentication.SetAuthCookie](https://msdn.microsoft.com/library/system.web.security.formsauthentication.setauthcookie.aspx)で使用される、 [FormsAuthentication](https://msdn.microsoft.com/library/system.web.security.formsauthenticationmodule.aspx)モジュール。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-184">This call is analogous to [FormAuthentication.SetAuthCookie](https://msdn.microsoft.com/library/system.web.security.formsauthentication.setauthcookie.aspx) used by the [FormsAuthentication](https://msdn.microsoft.com/library/system.web.security.formsauthenticationmodule.aspx) module.</span></span>
2. <span data-ttu-id="6aaf2-185">**ソリューション エクスプ ローラー**、プロジェクトを右クリックし、選択**追加**、し**Web フォーム**します。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-185">In **Solution Explorer**, right-click your project, select **Add**, and then **Web Form**.</span></span> <span data-ttu-id="6aaf2-186">Web フォーム名前**ログイン**します。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-186">Name the web form **Login**.</span></span>
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image12.png)
3. <span data-ttu-id="6aaf2-187">内容を置き換える、 *Login.aspx*を次のコード ファイル。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-187">Replace the contents of the *Login.aspx* file with the following code:</span></span>

    [!code-aspx[Main](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/samples/sample6.aspx)]
4. <span data-ttu-id="6aaf2-188">内容を置き換える、 *Login.aspx.cs*を次のファイル。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-188">Replace the contents of the *Login.aspx.cs* file with the following:</span></span>

    [!code-csharp[Main](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/samples/sample7.cs)]

    > [!NOTE] 
    > 
    > - <span data-ttu-id="6aaf2-189">`Page_Load`現在のユーザーの状態をチェックし、に基づいてアクションを実行するようになりましたその`Context.User.Identity.IsAuthenticated`状態。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-189">The `Page_Load` now checks for the status of current user and takes action based on its `Context.User.Identity.IsAuthenticated` status.</span></span>
    >     <span data-ttu-id="6aaf2-190">**ユーザー名でログインして表示**:Microsoft ASP.NET Identity フレームワークでの拡張メソッドが追加[どのオブジェクト タイプも](https://msdn.microsoft.com/library/system.security.principal.iidentity.aspx)を取得することができます、`UserName`と`UserId`ユーザーでログオンします。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-190">**Display Logged in User Name** : The Microsoft ASP.NET Identity Framework has added extension methods on [System.Security.Principal.IIdentity](https://msdn.microsoft.com/library/system.security.principal.iidentity.aspx) that allows you to get the `UserName` and `UserId`  for the logged in User.</span></span> <span data-ttu-id="6aaf2-191">これらの拡張メソッドが定義されている、`Microsoft.AspNet.Identity.Core`アセンブリ。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-191">These extension methods are defined in the `Microsoft.AspNet.Identity.Core` assembly.</span></span> <span data-ttu-id="6aaf2-192">これらの拡張メソッドは、置換の[HttpContext.User.Identity.Name](https://msdn.microsoft.com/library/system.web.httpcontext.user.aspx)します。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-192">These extension methods are the replacement for [HttpContext.User.Identity.Name](https://msdn.microsoft.com/library/system.web.httpcontext.user.aspx) .</span></span>
    > - <span data-ttu-id="6aaf2-193">SignIn メソッド:`This`メソッドは、置換前`CreateUser_Click`メソッドでは、このサンプルと、ユーザーが正常に作成した後、ユーザー サインインようになりました。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-193">SignIn method: `This` method replaces the previous `CreateUser_Click` method in this sample and now signs in the user after successfully creating the user.</span></span>   
    >   <span data-ttu-id="6aaf2-194">拡張メソッドを追加で Microsoft の OWIN Framework`System.Web.HttpContext`への参照を取得することができます、`IOwinContext`します。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-194">The Microsoft OWIN Framework has added extension methods on `System.Web.HttpContext` that allows you to get a reference to an `IOwinContext`.</span></span> <span data-ttu-id="6aaf2-195">これらの拡張メソッドが定義されている`Microsoft.Owin.Host.SystemWeb`アセンブリ。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-195">These extension methods are defined in `Microsoft.Owin.Host.SystemWeb` assembly.</span></span> <span data-ttu-id="6aaf2-196">`OwinContext`クラスでは、`IAuthenticationManager`現在の要求で使用可能な認証ミドルウェアの機能を表すプロパティ。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-196">The `OwinContext` class exposes an `IAuthenticationManager` property that represents the Authentication middleware functionality available on the current request.</span></span> <span data-ttu-id="6aaf2-197">使用して、ユーザーがサインインすることができます、 `AuthenticationManager` OWIN と呼び出し元から`SignIn`を渡して、`ClaimsIdentity`上記のようです。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-197">You can sign in the user by using the `AuthenticationManager` from OWIN and calling `SignIn` and passing in the `ClaimsIdentity` as shown above.</span></span> <span data-ttu-id="6aaf2-198">フレームワークが、アプリを生成する必要があります ASP.NET Identity と OWIN クッキー認証は要求ベースのシステムであるため、`ClaimsIdentity`ユーザー。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-198">Because ASP.NET Identity and OWIN Cookie Authentication are claims-based system, the framework requires the app to generate a `ClaimsIdentity` for the user.</span></span> <span data-ttu-id="6aaf2-199">`ClaimsIdentity`ユーザーが属するロールなど、ユーザーのすべての要求に関する情報があります。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-199">The `ClaimsIdentity` has information about all the claims for the user, such as what roles the user belongs to.</span></span> <span data-ttu-id="6aaf2-200">このコードは、ユーザーがサインインし、cookie も生成は、この段階でユーザーの複数のクレームを追加することもできます。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-200">You can also add more claims for the user at this stage This code will sign in the user and generate a cookie as well.</span></span> <span data-ttu-id="6aaf2-201">この呼び出しに似ています[FormAuthentication.SetAuthCookie](https://msdn.microsoft.com/library/system.web.security.formsauthentication.setauthcookie.aspx)で使用される、 [FormsAuthentication](https://msdn.microsoft.com/library/system.web.security.formsauthenticationmodule.aspx)モジュール。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-201">This call is analogous to [FormAuthentication.SetAuthCookie](https://msdn.microsoft.com/library/system.web.security.formsauthentication.setauthcookie.aspx) used by the [FormsAuthentication](https://msdn.microsoft.com/library/system.web.security.formsauthenticationmodule.aspx) module.</span></span>
    > - <span data-ttu-id="6aaf2-202">`SignOut` 方法:参照を取得、 `AuthenticationManager` OWIN と呼び出しから`SignOut`します。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-202">`SignOut` method: Gets a reference to the `AuthenticationManager` from OWIN and calls `SignOut`.</span></span> <span data-ttu-id="6aaf2-203">これは、メソッドは[FormsAuthentication.SignOut](https://msdn.microsoft.com/library/system.web.security.formsauthentication.signout.aspx)メソッドで使用される、 [FormsAuthentication](https://msdn.microsoft.com/library/system.web.security.formsauthenticationmodule.aspx)モジュール。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-203">This is analogous to [FormsAuthentication.SignOut](https://msdn.microsoft.com/library/system.web.security.formsauthentication.signout.aspx) method used by the [FormsAuthentication](https://msdn.microsoft.com/library/system.web.security.formsauthenticationmodule.aspx) module.</span></span>
5. <span data-ttu-id="6aaf2-204">キーを押して**ctrl キーを押しながら f5 キーを押して**をビルドして、web アプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-204">Press **Ctrl + F5** to build and run the web application.</span></span> <span data-ttu-id="6aaf2-205">新しいユーザー名とパスワードを入力し、選択**登録**します。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-205">Enter a new user name and password and then select **Register**.</span></span>
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image13.png)  
   <span data-ttu-id="6aaf2-206">メモ:この時点では、新しいユーザーが作成されログに記録します。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-206">Note: At this point, the new user is created and logged in.</span></span>
6. <span data-ttu-id="6aaf2-207">選択、**ログアウト**ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-207">Select the **Log out** button.</span></span> <span data-ttu-id="6aaf2-208">フォームのログにリダイレクトされます。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-208">You are redirected to the Log in form.</span></span>
7. <span data-ttu-id="6aaf2-209">無効なユーザー名またはパスワードを入力し、選択、**ログイン**ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-209">Enter an invalid user name or password and select the **Log in** button.</span></span> 
   <span data-ttu-id="6aaf2-210">`UserManager.Find`メソッドは null と、エラー メッセージを返します。"*無効なユーザー名またはパスワード*"が表示されます。</span><span class="sxs-lookup"><span data-stu-id="6aaf2-210">The `UserManager.Find`  method will return null and the error message: " *Invalid user name or password* " will be displayed.</span></span>
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image14.png)