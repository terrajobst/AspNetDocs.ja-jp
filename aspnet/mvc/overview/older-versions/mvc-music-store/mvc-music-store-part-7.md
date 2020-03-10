---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-7
title: 'パート 7: メンバーシップと承認 |Microsoft Docs'
author: jongalloway
description: このチュートリアルシリーズでは、ASP.NET MVC ミュージックストアサンプルアプリケーションをビルドするために実行するすべての手順について詳しく説明します。 パート7では、メンバーシップと承認について説明します。
ms.author: riande
ms.date: 10/13/2010
ms.assetid: c8511ebe-68bc-4240-87c3-d5ced84a3f37
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-7
msc.type: authoredcontent
ms.openlocfilehash: a6a1a936e0ea29ea36721ba78f35845401f74c01
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78433468"
---
# <a name="part-7-membership-and-authorization"></a><span data-ttu-id="c7e7c-104">パート 7: メンバーシップと承認</span><span class="sxs-lookup"><span data-stu-id="c7e7c-104">Part 7: Membership and Authorization</span></span>

<span data-ttu-id="c7e7c-105">( [Jon Galloway](https://github.com/jongalloway) )</span><span class="sxs-lookup"><span data-stu-id="c7e7c-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="c7e7c-106">MVC Music Store は、ASP.NET MVC と Visual Studio を使用して web 開発を行う方法を紹介したチュートリアルアプリケーションです。</span><span class="sxs-lookup"><span data-stu-id="c7e7c-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="c7e7c-107">MVC ミュージックストアは、音楽アルバムをオンラインで販売し、基本的なサイト管理、ユーザーサインイン、およびショッピングカート機能を実装する軽量のサンプルストア実装です。</span><span class="sxs-lookup"><span data-stu-id="c7e7c-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="c7e7c-108">このチュートリアルシリーズでは、ASP.NET MVC ミュージックストアサンプルアプリケーションをビルドするために実行するすべての手順について詳しく説明します。</span><span class="sxs-lookup"><span data-stu-id="c7e7c-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="c7e7c-109">パート7では、メンバーシップと承認について説明します。</span><span class="sxs-lookup"><span data-stu-id="c7e7c-109">Part 7 covers Membership and Authorization.</span></span>

<span data-ttu-id="c7e7c-110">現在、microsoft のストアマネージャーコントローラーは、サイトにアクセスするすべてのユーザーにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="c7e7c-110">Our Store Manager controller is currently accessible to anyone visiting our site.</span></span> <span data-ttu-id="c7e7c-111">これを変更して、サイト管理者にアクセス許可を制限してみましょう。</span><span class="sxs-lookup"><span data-stu-id="c7e7c-111">Let's change this to restrict permission to site administrators.</span></span>

## <a name="adding-the-accountcontroller-and-views"></a><span data-ttu-id="c7e7c-112">AccountController とビューの追加</span><span class="sxs-lookup"><span data-stu-id="c7e7c-112">Adding the AccountController and Views</span></span>

<span data-ttu-id="c7e7c-113">Full ASP.NET MVC 3 Web アプリケーションテンプレートと ASP.NET MVC 3 空の Web アプリケーションテンプレートの違いの1つは、空のテンプレートにはアカウントコントローラーが含まれていないことです。</span><span class="sxs-lookup"><span data-stu-id="c7e7c-113">One difference between the full ASP.NET MVC 3 Web Application template and the ASP.NET MVC 3 Empty Web Application template is that the empty template doesn't include an Account Controller.</span></span> <span data-ttu-id="c7e7c-114">アカウントコントローラーを追加するには、full ASP.NET MVC 3 Web アプリケーションテンプレートから作成された新しい ASP.NET MVC アプリケーションからいくつかのファイルをコピーします。</span><span class="sxs-lookup"><span data-stu-id="c7e7c-114">We'll add an Account Controller by copying a few files from a new ASP.NET MVC application created from the full ASP.NET MVC 3 Web Application template.</span></span>

<span data-ttu-id="c7e7c-115">Full ASP.NET MVC 3 Web アプリケーションテンプレートを使用して新しい ASP.NET MVC アプリケーションを作成し、次のファイルをプロジェクト内の同じディレクトリにコピーします。</span><span class="sxs-lookup"><span data-stu-id="c7e7c-115">Create a new ASP.NET MVC application using the full ASP.NET MVC 3 Web Application template and copy the following files into the same directories in our project:</span></span>

1. <span data-ttu-id="c7e7c-116">Controllers ディレクトリで AccountController.cs をコピーする</span><span class="sxs-lookup"><span data-stu-id="c7e7c-116">Copy AccountController.cs in the Controllers directory</span></span>
2. <span data-ttu-id="c7e7c-117">モデルディレクトリに AccountModels をコピーする</span><span class="sxs-lookup"><span data-stu-id="c7e7c-117">Copy AccountModels in the Models directory</span></span>
3. <span data-ttu-id="c7e7c-118">Views ディレクトリ内にアカウントディレクトリを作成し、の4つのビューをすべてコピーします。</span><span class="sxs-lookup"><span data-stu-id="c7e7c-118">Create an Account directory inside the Views directory and copy all four views in</span></span>

<span data-ttu-id="c7e7c-119">コントローラークラスとモデルクラスの名前空間を変更して、MvcMusicStore で始まるようにします。</span><span class="sxs-lookup"><span data-stu-id="c7e7c-119">Change the namespace for the Controller and Model classes so they begin with MvcMusicStore.</span></span> <span data-ttu-id="c7e7c-120">AccountController クラスは MvcMusicStore 名前空間を使用する必要があり、Accountcontroller クラスは MvcMusicStore 名前空間を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c7e7c-120">The AccountController class should use the MvcMusicStore.Controllers namespace, and the AccountModels class should use the MvcMusicStore.Models namespace.</span></span>

<span data-ttu-id="c7e7c-121">*注: これらのファイルは、チュートリアルの最初にサイトデザインファイルをコピーした MvcMusicStore-Assets ダウンロードでも入手できます。メンバーシップファイルは、コードディレクトリにあります。*</span><span class="sxs-lookup"><span data-stu-id="c7e7c-121">*Note: These files are also available in the MvcMusicStore-Assets.zip download from which we copied our site design files at the beginning of the tutorial. The Membership files are located in the Code directory.*</span></span>

<span data-ttu-id="c7e7c-122">更新されたソリューションは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="c7e7c-122">The updated solution should look like the following:</span></span>

![](mvc-music-store-part-7/_static/image1.png)

## <a name="adding-an-administrative-user-with-the-aspnet-configuration-site"></a><span data-ttu-id="c7e7c-123">ASP.NET 構成サイトでの管理ユーザーの追加</span><span class="sxs-lookup"><span data-stu-id="c7e7c-123">Adding an Administrative User with the ASP.NET Configuration site</span></span>

<span data-ttu-id="c7e7c-124">Web サイトで承認が必要になる前に、アクセス権を持つユーザーを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c7e7c-124">Before we require Authorization in our website, we'll need to create a user with access.</span></span> <span data-ttu-id="c7e7c-125">ユーザーを作成する最も簡単な方法は、組み込みの ASP.NET 構成 web サイトを使用することです。</span><span class="sxs-lookup"><span data-stu-id="c7e7c-125">The easiest way to create a user is to use the built-in ASP.NET Configuration website.</span></span>

<span data-ttu-id="c7e7c-126">ソリューションエクスプローラーのアイコンをクリックして、ASP.NET 構成 web サイトを起動します。</span><span class="sxs-lookup"><span data-stu-id="c7e7c-126">Launch the ASP.NET Configuration website by clicking following the icon in the Solution Explorer.</span></span>

![](mvc-music-store-part-7/_static/image2.png)

<span data-ttu-id="c7e7c-127">これにより、構成 web サイトが起動します。</span><span class="sxs-lookup"><span data-stu-id="c7e7c-127">This launches a configuration website.</span></span> <span data-ttu-id="c7e7c-128">ホーム画面の [セキュリティ] タブをクリックし、画面の中央にある [ロールの有効化] リンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="c7e7c-128">Click on the Security tab on the home screen, then click the "Enable roles" link in the center of the screen.</span></span>

![](mvc-music-store-part-7/_static/image3.png)

<span data-ttu-id="c7e7c-129">[ロールの作成または管理] リンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="c7e7c-129">Click the "Create or Manage roles" link.</span></span>

![](mvc-music-store-part-7/_static/image4.png)

<span data-ttu-id="c7e7c-130">ロール名として「Administrator」と入力し、[ロールの追加] ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="c7e7c-130">Enter "Administrator" as the role name and press the Add Role button.</span></span>

![](mvc-music-store-part-7/_static/image5.png)

<span data-ttu-id="c7e7c-131">[戻る] ボタンをクリックし、左側の [Create user] \ (ユーザーの作成 \) リンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="c7e7c-131">Click the Back button, then click on the Create user link on the left side.</span></span>

![](mvc-music-store-part-7/_static/image6.png)

<span data-ttu-id="c7e7c-132">次の情報を使用して、左側のユーザー情報フィールドに入力します。</span><span class="sxs-lookup"><span data-stu-id="c7e7c-132">Fill in the user information fields on the left using the following information:</span></span>

| <span data-ttu-id="c7e7c-133">**フィールド**</span><span class="sxs-lookup"><span data-stu-id="c7e7c-133">**Field**</span></span> | <span data-ttu-id="c7e7c-134">**Value**</span><span class="sxs-lookup"><span data-stu-id="c7e7c-134">**Value**</span></span> |
| --- | --- |
| <span data-ttu-id="c7e7c-135">**ユーザー名**</span><span class="sxs-lookup"><span data-stu-id="c7e7c-135">**User Name**</span></span> | <span data-ttu-id="c7e7c-136">管理者</span><span class="sxs-lookup"><span data-stu-id="c7e7c-136">Administrator</span></span> |
| <span data-ttu-id="c7e7c-137">**パスワード**</span><span class="sxs-lookup"><span data-stu-id="c7e7c-137">**Password**</span></span> | <span data-ttu-id="c7e7c-138">password123!</span><span class="sxs-lookup"><span data-stu-id="c7e7c-138">password123!</span></span> |
| <span data-ttu-id="c7e7c-139">**[パスワードの確認入力]**</span><span class="sxs-lookup"><span data-stu-id="c7e7c-139">**Confirm Password**</span></span> | <span data-ttu-id="c7e7c-140">password123!</span><span class="sxs-lookup"><span data-stu-id="c7e7c-140">password123!</span></span> |
| <span data-ttu-id="c7e7c-141">**電子メール**</span><span class="sxs-lookup"><span data-stu-id="c7e7c-141">**E-mail**</span></span> | <span data-ttu-id="c7e7c-142">(すべての電子メールアドレスが機能します)</span><span class="sxs-lookup"><span data-stu-id="c7e7c-142">(any email address will work)</span></span> |
| <span data-ttu-id="c7e7c-143">**セキュリティの質問**</span><span class="sxs-lookup"><span data-stu-id="c7e7c-143">**Security Question**</span></span> | <span data-ttu-id="c7e7c-144">(任意のもの)</span><span class="sxs-lookup"><span data-stu-id="c7e7c-144">(whatever you like)</span></span> |
| <span data-ttu-id="c7e7c-145">**セキュリティ返答**</span><span class="sxs-lookup"><span data-stu-id="c7e7c-145">**Security Answer**</span></span> | <span data-ttu-id="c7e7c-146">(任意のもの)</span><span class="sxs-lookup"><span data-stu-id="c7e7c-146">(whatever you like)</span></span> |

<span data-ttu-id="c7e7c-147">*注: もちろん、好きなパスワードを使用することもできます。既定のパスワードセキュリティ設定では、パスワードの長さが7文字で、英数字以外の文字が1つ含まれている必要があります。*</span><span class="sxs-lookup"><span data-stu-id="c7e7c-147">*Note: You can of course use any password you'd like. The default password security settings require a password that is 7 characters long and contains one non-alphanumeric character.*</span></span>

<span data-ttu-id="c7e7c-148">このユーザーの管理者ロールを選択し、[ユーザーの作成] ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="c7e7c-148">Select the Administrator role for this user, and click the Create User button.</span></span>

![](mvc-music-store-part-7/_static/image7.png)

<span data-ttu-id="c7e7c-149">この時点で、ユーザーが正常に作成されたことを示すメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="c7e7c-149">At this point, you should see a message indicating that the user was created successfully.</span></span>

![](mvc-music-store-part-7/_static/image8.png)

<span data-ttu-id="c7e7c-150">ブラウザーウィンドウを閉じることができるようになりました。</span><span class="sxs-lookup"><span data-stu-id="c7e7c-150">You can now close the browser window.</span></span>

## <a name="role-based-authorization"></a><span data-ttu-id="c7e7c-151">ロールベースの承認</span><span class="sxs-lookup"><span data-stu-id="c7e7c-151">Role-based Authorization</span></span>

<span data-ttu-id="c7e7c-152">ここで、[承認] 属性を使用して StoreManagerController へのアクセスを制限できます。これにより、クラス内の任意のコントローラーアクションにアクセスするために、ユーザーが管理者ロールに存在する必要があることを指定します。</span><span class="sxs-lookup"><span data-stu-id="c7e7c-152">Now we can restrict access to the StoreManagerController using the [Authorize] attribute, specifying that the user must be in the Administrator role to access any controller action in the class.</span></span>

[!code-csharp[Main](mvc-music-store-part-7/samples/sample1.cs)]

<span data-ttu-id="c7e7c-153">*注: [承認] 属性は、コントローラークラスレベルだけでなく、特定のアクションメソッドにも配置できます。*</span><span class="sxs-lookup"><span data-stu-id="c7e7c-153">*Note: The [Authorize] attribute can be placed on specific action methods as well as at the Controller class level.*</span></span>

<span data-ttu-id="c7e7c-154">これで、/storemanager を参照すると、[ログオン] ダイアログが表示されるようになります。</span><span class="sxs-lookup"><span data-stu-id="c7e7c-154">Now browsing to /StoreManager brings up a Log On dialog:</span></span>

![](mvc-music-store-part-7/_static/image9.png)

<span data-ttu-id="c7e7c-155">新しい管理者アカウントでログオンすると、前と同じようにアルバムの編集画面にアクセスできるようになります。</span><span class="sxs-lookup"><span data-stu-id="c7e7c-155">After logging on with our new Administrator account, we're able to go to the Album Edit screen as before.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c7e7c-156">[前へ](mvc-music-store-part-6.md)
> [次へ](mvc-music-store-part-8.md)</span><span class="sxs-lookup"><span data-stu-id="c7e7c-156">[Previous](mvc-music-store-part-6.md)
[Next](mvc-music-store-part-8.md)</span></span>
