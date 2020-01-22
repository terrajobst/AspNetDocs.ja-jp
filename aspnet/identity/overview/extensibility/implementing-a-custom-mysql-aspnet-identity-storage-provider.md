---
uid: identity/overview/extensibility/implementing-a-custom-mysql-aspnet-identity-storage-provider
title: カスタム MySQL ASP.NET Identity ストレージプロバイダーの実装-ASP.NET 4.x
author: raquelsa
description: ASP.NET Identity は拡張可能なシステムです。これを使用すると、独自の記憶域プロバイダーを作成し、アプリケーションにプラグインできます。
ms.author: riande
ms.date: 05/22/2015
ms.assetid: 248f5fe7-39ba-40ea-ab1e-71a69b0bd649
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/extensibility/implementing-a-custom-mysql-aspnet-identity-storage-provider
msc.type: authoredcontent
ms.openlocfilehash: 2f0b47d45bce82c71d1864536309f9e2ffed2d63
ms.sourcegitcommit: 88fc80e3f65aebdf61ec9414810ddbc31c543f04
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/22/2020
ms.locfileid: "76519129"
---
# <a name="implementing-a-custom-mysql-aspnet-identity-storage-provider"></a><span data-ttu-id="351e8-103">カスタム MySQL ASP.NET Identity ストレージ プロバイダーの実装</span><span class="sxs-lookup"><span data-stu-id="351e8-103">Implementing a Custom MySQL ASP.NET Identity Storage Provider</span></span>

<span data-ttu-id="351e8-104">[Raquel Soares De Almeida](https://github.com/raquelsa)、 [suhas Joshi](https://github.com/suhasj)、 [Tom fitzmacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="351e8-104">by [Raquel Soares De Almeida](https://github.com/raquelsa), [Suhas Joshi](https://github.com/suhasj), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="351e8-105">ASP.NET Identity は拡張可能なシステムで、アプリケーションを再実行することなく、独自の記憶域プロバイダーを作成してアプリケーションに組み込むことができます。</span><span class="sxs-lookup"><span data-stu-id="351e8-105">ASP.NET Identity is an extensible system which enables you to create your own storage provider and plug it into your application without re-working the application.</span></span> <span data-ttu-id="351e8-106">このトピックでは、ASP.NET Identity 用の MySQL 記憶域プロバイダーを作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="351e8-106">This topic describes how to create a MySQL storage provider for ASP.NET Identity.</span></span> <span data-ttu-id="351e8-107">カスタム記憶域プロバイダーの作成の概要については、「 [ASP.NET Identity 用のカスタム記憶域プロバイダーの概要](overview-of-custom-storage-providers-for-aspnet-identity.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="351e8-107">For an overview of creating custom storage providers, see [Overview of Custom Storage Providers for ASP.NET Identity](overview-of-custom-storage-providers-for-aspnet-identity.md).</span></span>
> 
> <span data-ttu-id="351e8-108">このチュートリアルを完了するには、Update 2 の Visual Studio 2013 が必要です。</span><span class="sxs-lookup"><span data-stu-id="351e8-108">To complete this tutorial, you must have Visual Studio 2013 with Update 2.</span></span>
> 
> <span data-ttu-id="351e8-109">このチュートリアルでは次のことを行います。</span><span class="sxs-lookup"><span data-stu-id="351e8-109">This tutorial will:</span></span>
> 
> - <span data-ttu-id="351e8-110">Azure で MySQL データベースインスタンスを作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="351e8-110">Show how to create a MySQL database instance on Azure.</span></span>
> - <span data-ttu-id="351e8-111">MySQL クライアントツール (MySQL ワークベンチ) を使用してテーブルを作成し、Azure でリモートデータベースを管理する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="351e8-111">Show how to use a MySQL client tool (MySQL Workbench) to create tables and manage your remote database on Azure.</span></span>
> - <span data-ttu-id="351e8-112">MVC アプリケーションプロジェクトで既定の ASP.NET Identity ストレージの実装をカスタム実装に置き換える方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="351e8-112">Show how to replace the default ASP.NET Identity storage implementation with our custom implementation on a MVC application project.</span></span>
> 
> <span data-ttu-id="351e8-113">このチュートリアルは、もともと Raquel Soares De Almeida と Rick Anderson ( [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) ) によって作成されました。</span><span class="sxs-lookup"><span data-stu-id="351e8-113">This tutorial was originally written by Raquel Soares De Almeida and Rick Anderson ( [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) ).</span></span> <span data-ttu-id="351e8-114">サンプルプロジェクトは、Suhas Joshi によって Id 2.0 に更新されました。</span><span class="sxs-lookup"><span data-stu-id="351e8-114">The sample project was updated for Identity 2.0 by Suhas Joshi.</span></span> <span data-ttu-id="351e8-115">このトピックは、Tom FitzMacken によって Id 2.0 に対して更新されました。</span><span class="sxs-lookup"><span data-stu-id="351e8-115">The topic was updated for Identity 2.0 by Tom FitzMacken.</span></span>

## <a name="download-completed-project"></a><span data-ttu-id="351e8-116">完成したプロジェクトのダウンロード</span><span class="sxs-lookup"><span data-stu-id="351e8-116">Download completed project</span></span>

<span data-ttu-id="351e8-117">このチュートリアルの最後には、Azure でホストされている MySQL データベースを使用して ASP.NET Identity 使用する MVC アプリケーションプロジェクトが作成されます。</span><span class="sxs-lookup"><span data-stu-id="351e8-117">At the end of this tutorial, you will have an MVC application project with ASP.NET Identity working with a MySQL database hosted on Azure.</span></span>

<span data-ttu-id="351e8-118">完成した MySQL ストレージプロバイダーは、 [AspNet. Identity. MySQL (GitHub)](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/AspNet.Identity.MySQL)からダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="351e8-118">You can download the completed MySQL storage provider at [AspNet.Identity.MySQL (GitHub)](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/AspNet.Identity.MySQL).</span></span>

## <a name="the-steps-you-will-perform"></a><span data-ttu-id="351e8-119">実行する手順</span><span class="sxs-lookup"><span data-stu-id="351e8-119">The steps you will perform</span></span>

<span data-ttu-id="351e8-120">このチュートリアルでは次のことを行います。</span><span class="sxs-lookup"><span data-stu-id="351e8-120">In this tutorial you will:</span></span>

1. <span data-ttu-id="351e8-121">Azure で MySQL データベースを作成する</span><span class="sxs-lookup"><span data-stu-id="351e8-121">Create a MySQL database on Azure</span></span>
2. <span data-ttu-id="351e8-122">MySQL で ASP.NET Identity テーブルを作成する</span><span class="sxs-lookup"><span data-stu-id="351e8-122">Create the ASP.NET Identity tables in MySQL</span></span>
3. <span data-ttu-id="351e8-123">MVC アプリケーションを作成し、MySQL プロバイダーを使用するように構成する</span><span class="sxs-lookup"><span data-stu-id="351e8-123">Create an MVC application and configure it to use the MySQL provider</span></span>
4. <span data-ttu-id="351e8-124">アプリを実行する</span><span class="sxs-lookup"><span data-stu-id="351e8-124">Run the app</span></span>

<span data-ttu-id="351e8-125">このトピックでは、ASP.NET Identity のアーキテクチャと、お客様のストレージプロバイダーを実装するときに行う必要がある決定事項については説明しません。</span><span class="sxs-lookup"><span data-stu-id="351e8-125">This topic does not cover the architecture of ASP.NET Identity and the decisions you must make when implementing a customer storage provider.</span></span> <span data-ttu-id="351e8-126">詳細については、「 [ASP.NET Identity 用のカスタム記憶域プロバイダーの概要](overview-of-custom-storage-providers-for-aspnet-identity.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="351e8-126">For that information, see [Overview of Custom Storage Providers for ASP.NET Identity](overview-of-custom-storage-providers-for-aspnet-identity.md).</span></span>

## <a name="review-mysql-storage-provider-classes"></a><span data-ttu-id="351e8-127">MySQL ストレージプロバイダークラスの確認</span><span class="sxs-lookup"><span data-stu-id="351e8-127">Review MySQL storage provider classes</span></span>

<span data-ttu-id="351e8-128">MySQL 記憶域プロバイダーを作成する手順に進む前に、記憶域プロバイダーを構成するクラスを見てみましょう。</span><span class="sxs-lookup"><span data-stu-id="351e8-128">Before jumping into the steps to create the MySQL storage provider, let's look at the classes that make up the storage provider.</span></span> <span data-ttu-id="351e8-129">ユーザーとロールを管理するには、アプリケーションから呼び出されるデータベース操作とクラスを管理するクラスが必要です。</span><span class="sxs-lookup"><span data-stu-id="351e8-129">You will need classes that manage the database operations and classes that are called from the application to manage users and roles.</span></span>

### <a name="storage-classes"></a><span data-ttu-id="351e8-130">ストレージ クラス</span><span class="sxs-lookup"><span data-stu-id="351e8-130">Storage classes</span></span>

- <span data-ttu-id="351e8-131">[[ユーザー](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/IdentityUser.cs) ]-ユーザーのプロパティが含まれます。</span><span class="sxs-lookup"><span data-stu-id="351e8-131">[IdentityUser](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/IdentityUser.cs) - contains properties for the user.</span></span>
- <span data-ttu-id="351e8-132">[Userstore](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserStore.cs) -ユーザーを追加、更新、または取得するための操作が含まれています。</span><span class="sxs-lookup"><span data-stu-id="351e8-132">[UserStore](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserStore.cs) - contains operations for adding, updating or retrieving users.</span></span>
- <span data-ttu-id="351e8-133">"Identity [role](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/IdentityRole.cs) "-ロールのプロパティが含まれます。</span><span class="sxs-lookup"><span data-stu-id="351e8-133">[IdentityRole](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/IdentityRole.cs) - contains properties for roles.</span></span>
- <span data-ttu-id="351e8-134">[Rolestore](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/RoleStore.cs) -ロールを追加、削除、更新、および取得するための操作が含まれています。</span><span class="sxs-lookup"><span data-stu-id="351e8-134">[RoleStore](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/RoleStore.cs) - contains operations for adding, deleting, updating and retrieving roles.</span></span>

### <a name="data-access-layer-classes"></a><span data-ttu-id="351e8-135">データアクセス層クラス</span><span class="sxs-lookup"><span data-stu-id="351e8-135">Data access layer classes</span></span>

<span data-ttu-id="351e8-136">この例では、データアクセス層クラスにテーブルを操作するための SQL ステートメントが含まれています。ただし、コードでは、Entity Framework や NHibernate などのオブジェクトリレーショナルマッピング (ORM) を使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="351e8-136">For this example, the data access layer classes contain SQL statements for working with the tables; however, in your code you might want to use object-relational mapping (ORM) such as Entity Framework or NHibernate.</span></span> <span data-ttu-id="351e8-137">特に、遅延読み込みとオブジェクトキャッシュを含む ORM を使用しないと、アプリケーションのパフォーマンスが低下する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="351e8-137">In particular, your application may experience poor performance without an ORM that includes lazy loading and object caching.</span></span> <span data-ttu-id="351e8-138">詳細については、「 [Entity Framework のない ASP.NET Identity 2.0](https://aspnetidentity.codeplex.com/discussions/561828) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="351e8-138">For more information, see [ASP.NET Identity 2.0 without Entity Framework?](https://aspnetidentity.codeplex.com/discussions/561828)</span></span>

- <span data-ttu-id="351e8-139">[MySQLDatabase](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/MySQLDatabase.cs) -MySQL データベース接続と、データベース操作を実行するためのメソッドが含まれています。</span><span class="sxs-lookup"><span data-stu-id="351e8-139">[MySQLDatabase](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/MySQLDatabase.cs) - contains the MySQL database connection and methods for performing database operations.</span></span> <span data-ttu-id="351e8-140">UserStore と RoleStore は、どちらもこのクラスのインスタンスでインスタンス化されます。</span><span class="sxs-lookup"><span data-stu-id="351e8-140">UserStore and RoleStore are both instantiated with an instance of this class.</span></span>
- <span data-ttu-id="351e8-141">[Roletable](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/RoleTable.cs) -ロールを格納するテーブルのデータベース操作が含まれます。</span><span class="sxs-lookup"><span data-stu-id="351e8-141">[RoleTable](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/RoleTable.cs) - contains database operations for the table that stores roles.</span></span>
- <span data-ttu-id="351e8-142">[Userclaimstable](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserClaimsTable.cs) -ユーザー要求を格納するテーブルのデータベース操作が含まれます。</span><span class="sxs-lookup"><span data-stu-id="351e8-142">[UserClaimsTable](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserClaimsTable.cs) - contains database operations for the table that stores user claims.</span></span>
- <span data-ttu-id="351e8-143">[UserLoginsTable](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserLoginsTable.cs) -ユーザーのログイン情報を格納するテーブルのデータベース操作を格納します。</span><span class="sxs-lookup"><span data-stu-id="351e8-143">[UserLoginsTable](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserLoginsTable.cs) - contains database operations for the table that stores user login information.</span></span>
- <span data-ttu-id="351e8-144">[Userroletable](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserRoleTable.cs) -どのユーザーがどのロールに割り当てられているかを格納するテーブルのデータベース操作が含まれます。</span><span class="sxs-lookup"><span data-stu-id="351e8-144">[UserRoleTable](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserRoleTable.cs) - contains database operations for the table that stores which users are assigned to which roles.</span></span>
- <span data-ttu-id="351e8-145">[Usertable](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserTable.cs) -ユーザーを格納するテーブルのデータベース操作が含まれます。</span><span class="sxs-lookup"><span data-stu-id="351e8-145">[UserTable](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserTable.cs) - contains database operations for the table that stores users.</span></span>

## <a name="create-a-mysql-database-instance-on-azure"></a><span data-ttu-id="351e8-146">Azure で MySQL データベースインスタンスを作成する</span><span class="sxs-lookup"><span data-stu-id="351e8-146">Create a MySQL database instance on Azure</span></span>

1. <span data-ttu-id="351e8-147">[Azure Portal](https://manage.windowsazure.com/) にログインします。</span><span class="sxs-lookup"><span data-stu-id="351e8-147">Log in to the [Azure Portal](https://manage.windowsazure.com/).</span></span>
2. <span data-ttu-id="351e8-148">ページの下部にある **[+ 新規]** をクリックし、 **[ストア]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="351e8-148">Click **+NEW** at the bottom of the page, and then select **STORE**.</span></span>  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image1.png)
3. <span data-ttu-id="351e8-149">**選択とアドオン**ウィザードで、 **[ClearDB MySQL Database]** を選択し、ダイアログの右下にある次へ進む矢印をクリックします。</span><span class="sxs-lookup"><span data-stu-id="351e8-149">In the **Choose and Add-on** wizard, select **ClearDB MySQL Database** and click on the next arrow at the bottom right of the dialog.</span></span>  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image2.png)
4. <span data-ttu-id="351e8-150">既定の**Free**プランをそのままにして、**名前**を「**識別子**」に変更します。</span><span class="sxs-lookup"><span data-stu-id="351e8-150">Keep the default **Free** plan and change the **Name** to **IdentityMySQLDatabase**.</span></span> <span data-ttu-id="351e8-151">最も近いリージョンを選択し、次へ進む矢印をクリックします。</span><span class="sxs-lookup"><span data-stu-id="351e8-151">Select the region nearest you and then click the next arrow.</span></span>  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image3.png)
5. <span data-ttu-id="351e8-152">チェックマークをクリックして、データベースの作成を完了します。</span><span class="sxs-lookup"><span data-stu-id="351e8-152">Click the checkmark to complete the database creation.</span></span>  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image4.png)
6. <span data-ttu-id="351e8-153">データベースが作成されたら、管理ポータルの **[アドオン]** タブから管理できます。</span><span class="sxs-lookup"><span data-stu-id="351e8-153">After your database has been created, you can manage it from the **ADD-ONS** tab in the management portal.</span></span>   
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image5.png)
7. <span data-ttu-id="351e8-154">ページの下部にある **[接続情報]** をクリックすると、データベース接続情報を取得できます。</span><span class="sxs-lookup"><span data-stu-id="351e8-154">You can get the database connection information by clicking on **CONNECTION INFO** at the bottom of the page.</span></span>  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image6.png)
8. <span data-ttu-id="351e8-155">[コピー] ボタンをクリックして接続文字列をコピーし、MVC アプリケーションで後で使用できるように保存します。</span><span class="sxs-lookup"><span data-stu-id="351e8-155">Copy the connection string by clicking on the copy button and save it so you can use later in your MVC application.</span></span>   
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image7.png)

## <a name="create-the-aspnet-identity-tables-in-a-mysql-database"></a><span data-ttu-id="351e8-156">MySQL データベースに ASP.NET Identity テーブルを作成する</span><span class="sxs-lookup"><span data-stu-id="351e8-156">Create the ASP.NET Identity tables in a MySQL database</span></span>

### <a name="install-mysql-workbench-tool-to-connect-and-manage-mysql-database"></a><span data-ttu-id="351e8-157">Mysql データベースに接続して管理するための MySQL ワークベンチツールのインストール</span><span class="sxs-lookup"><span data-stu-id="351e8-157">Install MySQL Workbench tool to connect and manage MySQL database</span></span>

1. <span data-ttu-id="351e8-158">Mysql の[ダウンロードページ](http://dev.mysql.com/downloads/windows/installer/)から**mysql ワークベンチ**ツールをインストールする</span><span class="sxs-lookup"><span data-stu-id="351e8-158">Install the **MySQL Workbench** tool from the [MySQL downloads page](http://dev.mysql.com/downloads/windows/installer/)</span></span>
2. <span data-ttu-id="351e8-159">アプリを起動し、 **[MySQLConnections +]** ボタンをクリックして新しい接続を追加します。</span><span class="sxs-lookup"><span data-stu-id="351e8-159">Launch the app and add click on the **MySQLConnections +** button to add a new connection.</span></span> <span data-ttu-id="351e8-160">このチュートリアルの前の手順で作成した Azure MySQL データベースからコピーした接続文字列データを使用します。</span><span class="sxs-lookup"><span data-stu-id="351e8-160">Use the connection string data you copied from the Azure MySQL database you created earlier in this tutorial.</span></span>
3. <span data-ttu-id="351e8-161">接続を確立したら、新しい **[クエリ]** タブを開きます。[MySQLIdentity](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/MySQLIdentity.sql)のコマンドをクエリに貼り付けて、データベーステーブルを作成するために実行します。</span><span class="sxs-lookup"><span data-stu-id="351e8-161">After establishing the connection, open a new **Query** tab; paste the commands from [MySQLIdentity.sql](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/MySQLIdentity.sql) into the query and execute it in order to create the database tables.</span></span>
4. <span data-ttu-id="351e8-162">次に示すように、Azure でホストされている MySQL データベースで、すべての ASP.NET Identity 必要なテーブルが作成されました。</span><span class="sxs-lookup"><span data-stu-id="351e8-162">You now have all the ASP.NET Identity necessary tables created on a MySQL database hosted on Azure as shown below.</span></span>  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image1.jpg)

## <a name="create-an-mvc-application-project-from-template-and-configure-it-to-use-mysql-provider"></a><span data-ttu-id="351e8-163">テンプレートから MVC アプリケーションプロジェクトを作成し、MySQL プロバイダーを使用するように構成する</span><span class="sxs-lookup"><span data-stu-id="351e8-163">Create an MVC application project from template and configure it to use MySQL provider</span></span>

<span data-ttu-id="351e8-164">必要に応じて、 [Visual Studio Express 2013 For Web](https://go.microsoft.com/fwlink/?LinkId=299058)または[Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566) Update 2 をインストールします。</span><span class="sxs-lookup"><span data-stu-id="351e8-164">If needed, install either [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) or [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566) with Update 2.</span></span>

### <a name="download-the-aspnetidentitymysql-project-from-github"></a><span data-ttu-id="351e8-165">GitHub から ASP.DLL プロジェクトをダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="351e8-165">Download the ASP.NET.Identity.MySQL project from GitHub</span></span>

1. <span data-ttu-id="351e8-166">[AspNet. Identity. MySQL (GitHub)](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/AspNet.Identity.MySQL/)でリポジトリの URL を参照します。</span><span class="sxs-lookup"><span data-stu-id="351e8-166">Browse to the repository URL at [AspNet.Identity.MySQL (GitHub)](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/AspNet.Identity.MySQL/).</span></span>
2. <span data-ttu-id="351e8-167">ソースコードをダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="351e8-167">Download the source code.</span></span>
3. <span data-ttu-id="351e8-168">ローカルフォルダーに .zip ファイルを抽出します。</span><span class="sxs-lookup"><span data-stu-id="351e8-168">Extract the .zip file into a local folder.</span></span>
4. <span data-ttu-id="351e8-169">AspNet. の MySQL ソリューションを開き、ビルドします。</span><span class="sxs-lookup"><span data-stu-id="351e8-169">Open the AspNet.Identity.MySQL solution and build it.</span></span>

### <a name="create-a-new-mvc-application-project-from-template"></a><span data-ttu-id="351e8-170">テンプレートからの新しい MVC アプリケーションプロジェクトの作成</span><span class="sxs-lookup"><span data-stu-id="351e8-170">Create a new MVC application project from template</span></span>

1. <span data-ttu-id="351e8-171">**AspNet. id. MySQL**ソリューションを右クリックし、[**新しいプロジェクト**の**追加**] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="351e8-171">Right click the **AspNet.Identity.MySQL** solution and **Add**, **New Project**</span></span>
2. <span data-ttu-id="351e8-172">**[新しいプロジェクトの追加]** ダイアログで、左側の **[ビジュアルC# ]** 、 **[web]** の順に選択し、 **[ASP.NET web Application]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="351e8-172">In the **Add New Project** Dialog select **Visual C#** on the left, then **Web** and then select **ASP.NET Web Application**.</span></span> <span data-ttu-id="351e8-173">プロジェクトに名前を **IdentityMySQLDemo** ;[ok] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="351e8-173">Name your project **IdentityMySQLDemo**; and then click OK.</span></span>  
  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image2.jpg)
3. <span data-ttu-id="351e8-174">**[New ASP.NET プロジェクト]** ダイアログボックスで、既定のオプション (認証方法として**個々のユーザーアカウント**を含む) を使用して MVC テンプレートを選択し、[ **OK]** をクリックします。![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image3.jpg)</span><span class="sxs-lookup"><span data-stu-id="351e8-174">In the **New ASP.NET Project** dialog, select the MVC template with the default options (that includes **Individual User Accounts** as authentication method) and click **OK**.![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image3.jpg)</span></span>
4. <span data-ttu-id="351e8-175">ソリューションエクスプローラーで、識別子 Tymysqldemo プロジェクトを右クリックし、 **[NuGet パッケージの管理]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="351e8-175">In Solution Explorer, right-click your IdentityMySQLDemo project and select **Manage NuGet Packages**.</span></span> <span data-ttu-id="351e8-176">[検索テキストボックス] ダイアログボックスで、「 **Identity. EntityFramework**」と入力します。</span><span class="sxs-lookup"><span data-stu-id="351e8-176">In the search text box dialog, type **Identity.EntityFramework**.</span></span> <span data-ttu-id="351e8-177">結果の一覧でこのパッケージを選択し、 **[アンインストール]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="351e8-177">Select this package in the list of results and click **Uninstall**.</span></span> <span data-ttu-id="351e8-178">依存関係パッケージ EntityFramework をアンインストールするよう求めるメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="351e8-178">You will be prompted to uninstall the dependency package EntityFramework.</span></span> <span data-ttu-id="351e8-179">[はい] をクリックします。このパッケージは、このアプリケーションではなくなります。</span><span class="sxs-lookup"><span data-stu-id="351e8-179">Click on Yes as we will no longer this package on this application.</span></span>
5. <span data-ttu-id="351e8-180">識別子 プロジェクトを右クリックし、**追加**、**参照、ソリューション、プロジェクト** の順に選択し、AspNet プロジェクトを選択して  **OK**をクリックします。</span><span class="sxs-lookup"><span data-stu-id="351e8-180">Right click the IdentityMySQLDemo project, select **Add**, **Reference, Solution, Projects;** select the AspNet.Identity.MySQL project and click **OK**.</span></span>
6. <span data-ttu-id="351e8-181">識別子のすべての参照を置き換えます。</span><span class="sxs-lookup"><span data-stu-id="351e8-181">In the IdentityMySQLDemo project, replace all references to</span></span>  
    `using Microsoft.AspNet.Identity.EntityFramework;`  
   <span data-ttu-id="351e8-182">を使用する場合</span><span class="sxs-lookup"><span data-stu-id="351e8-182">with</span></span>  
     `using AspNet.Identity.MySQL;`
7. <span data-ttu-id="351e8-183">IdentityModels.cs で、 **Applicationdbcontext**を**MySqlDatabase**から派生するように設定し、接続名と共に1つのパラメーターを受け取るコンストラクターを含めます。</span><span class="sxs-lookup"><span data-stu-id="351e8-183">In IdentityModels.cs, set **ApplicationDbContext** to derive from **MySqlDatabase** and include a constructor that take a single parameter with the connection name.</span></span>  

    [!code-csharp[Main](implementing-a-custom-mysql-aspnet-identity-storage-provider/samples/sample1.cs)]
8. <span data-ttu-id="351e8-184">IdentityConfig.cs ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="351e8-184">Open the IdentityConfig.cs file.</span></span> <span data-ttu-id="351e8-185">**Applicationusermanager. Create**メソッドで、インスタンス化 usermanager を次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="351e8-185">In the **ApplicationUserManager.Create** method, replace instantiating UserManager with the following code:</span></span>  

    [!code-csharp[Main](implementing-a-custom-mysql-aspnet-identity-storage-provider/samples/sample2.cs)]
9. <span data-ttu-id="351e8-186">Web.config ファイルを開き、DefaultConnection 文字列を次のエントリに置き換えて、強調表示された値を、前の手順で作成した MySQL データベースの接続文字列に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="351e8-186">Open the web.config file and replace the DefaultConnection string with this entry replacing the highlighted values with the connection string of the MySQL database you created on previous steps:</span></span>  

    [!code-xml[Main](implementing-a-custom-mysql-aspnet-identity-storage-provider/samples/sample3.xml?highlight=2)]

## <a name="run-the-app-and-connect-to-the-mysql-db"></a><span data-ttu-id="351e8-187">アプリを実行して MySQL DB に接続する</span><span class="sxs-lookup"><span data-stu-id="351e8-187">Run the app and connect to the MySQL DB</span></span>

1. <span data-ttu-id="351e8-188">**[識別子]** を右クリックし、 **[スタートアッププロジェクトに設定]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="351e8-188">Right click the **IdentityMySQLDemo** project and select **Set as Startup Project**</span></span>
2. <span data-ttu-id="351e8-189">Ctrl キーを押し**ながら F5**キーを押して、アプリをビルドして実行します。</span><span class="sxs-lookup"><span data-stu-id="351e8-189">Press **Ctrl + F5** to build and run the app.</span></span>
3. <span data-ttu-id="351e8-190">ページの上部にある [Register] \ (**登録**\) タブをクリックします。</span><span class="sxs-lookup"><span data-stu-id="351e8-190">Click on **Register** tab on the top of the page.</span></span>
4. <span data-ttu-id="351e8-191">新しいユーザー名とパスワードを入力し、[Register] \ (**登録**\) をクリックします。</span><span class="sxs-lookup"><span data-stu-id="351e8-191">Enter a new user name and password and then click on **Register**.</span></span>  
  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image8.png)
5. <span data-ttu-id="351e8-192">これで、新しいユーザーが登録され、ログインされました。</span><span class="sxs-lookup"><span data-stu-id="351e8-192">The new user is now registered and logged in.</span></span>  
  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image9.png)
6. <span data-ttu-id="351e8-193">MySQL ワークベンチツールに戻り、**識別子 Tymysqldatabase**の内容を調べます。</span><span class="sxs-lookup"><span data-stu-id="351e8-193">Go back to the MySQL Workbench tool and inspect the **IdentityMySQLDatabase** table's contents.</span></span> <span data-ttu-id="351e8-194">新しいユーザーを登録するときに、ユーザーテーブルでエントリを調べます。</span><span class="sxs-lookup"><span data-stu-id="351e8-194">Inspect the users table for the entries as you register new users.</span></span>  
  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image10.png)

## <a name="next-steps"></a><span data-ttu-id="351e8-195">次のステップ</span><span class="sxs-lookup"><span data-stu-id="351e8-195">Next Steps</span></span>

<span data-ttu-id="351e8-196">このアプリで他の認証方法を有効にする方法の詳細については、「 [Facebook と Google OAuth2 を使用した ASP.NET MVC 5 アプリの作成」と「OpenID サインオン](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="351e8-196">For more information on how to enable other authentication methods on this app, refer to [Create an ASP.NET MVC 5 App with Facebook and Google OAuth2 and OpenID Sign-on](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md).</span></span>

<span data-ttu-id="351e8-197">DB と OAuth を統合し、ユーザーがアプリへのアクセスを制限するロールを設定する方法については、「 [Azure へのメンバーシップ、OAuth、および SQL Database を使用した Secure ASP.NET MVC 5 アプリのデプロイ](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="351e8-197">To learn how to integrate your DB with OAuth and to set up roles to limit users access to your app, see [Deploy a Secure ASP.NET MVC 5 app with Membership, OAuth, and SQL Database to Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span></span>
