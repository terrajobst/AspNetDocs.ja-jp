---
uid: identity/overview/extensibility/change-primary-key-for-users-in-aspnet-identity
title: ASP.NET Identity のユーザーのプライマリキーを変更する-ASP.NET 4.x
author: Rick-Anderson
description: Visual Studio 2013 では、既定の web アプリケーションは、ユーザーアカウントのキーに文字列値を使用します。 ASP.NET Identity を使用すると、...
ms.author: riande
ms.date: 09/30/2014
ms.assetid: 44925849-5762-4504-a8cd-8f0cd06f6dc3
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/extensibility/change-primary-key-for-users-in-aspnet-identity
msc.type: authoredcontent
ms.openlocfilehash: 0afea8eacfc646f1489b87629fdb2d437815d88c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78472264"
---
# <a name="change-primary-key-for-users-in-aspnet-identity"></a><span data-ttu-id="7e34b-104">ASP.NET Identity でユーザーの主キーを変更する</span><span class="sxs-lookup"><span data-stu-id="7e34b-104">Change Primary Key for Users in ASP.NET Identity</span></span>

<span data-ttu-id="7e34b-105">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="7e34b-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="7e34b-106">Visual Studio 2013 では、既定の web アプリケーションは、ユーザーアカウントのキーに文字列値を使用します。</span><span class="sxs-lookup"><span data-stu-id="7e34b-106">In Visual Studio 2013, the default web application uses a string value for the key for user accounts.</span></span> <span data-ttu-id="7e34b-107">ASP.NET Identity を使用すると、データ要件に合わせてキーの種類を変更できます。</span><span class="sxs-lookup"><span data-stu-id="7e34b-107">ASP.NET Identity enables you to change the type of the key to meet your data requirements.</span></span> <span data-ttu-id="7e34b-108">たとえば、キーの型を文字列から整数に変更できます。</span><span class="sxs-lookup"><span data-stu-id="7e34b-108">For example, you can change the type of the key from a string to an integer.</span></span>
> 
> <span data-ttu-id="7e34b-109">このトピックでは、既定の web アプリケーションを使用してを開始し、ユーザーアカウントキーを整数に変更する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="7e34b-109">This topic shows how to start with the default web application and change the user account key to an integer.</span></span> <span data-ttu-id="7e34b-110">同じ変更を使用して、プロジェクト内の任意の種類のキーを実装できます。</span><span class="sxs-lookup"><span data-stu-id="7e34b-110">You can use the same modifications to implement any type of key in your project.</span></span> <span data-ttu-id="7e34b-111">既定の web アプリケーションでこれらの変更を行う方法を示していますが、カスタマイズされたアプリケーションに同様の変更を適用することもできます。</span><span class="sxs-lookup"><span data-stu-id="7e34b-111">It shows how to make these changes in the default web application, but you could apply similar modifications to a customized application.</span></span> <span data-ttu-id="7e34b-112">MVC または Web フォームを操作するときに必要な変更を示します。</span><span class="sxs-lookup"><span data-stu-id="7e34b-112">It shows the changes needed when working with MVC or Web Forms.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="7e34b-113">このチュートリアルで使用されているソフトウェアのバージョン</span><span class="sxs-lookup"><span data-stu-id="7e34b-113">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="7e34b-114">Update 2 (またはそれ以降) の Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="7e34b-114">Visual Studio 2013 with Update 2 (or later)</span></span>
> - <span data-ttu-id="7e34b-115">ASP.NET Identity 2.1 以降</span><span class="sxs-lookup"><span data-stu-id="7e34b-115">ASP.NET Identity 2.1 or later</span></span>

<span data-ttu-id="7e34b-116">このチュートリアルの手順を実行するには、Visual Studio 2013 Update 2 (以降)、および ASP.NET Web アプリケーションテンプレートから作成された web アプリケーションが必要です。</span><span class="sxs-lookup"><span data-stu-id="7e34b-116">To perform the steps in this tutorial, you must have Visual Studio 2013 Update 2 (or later), and a web application created from the ASP.NET Web Application template.</span></span> <span data-ttu-id="7e34b-117">Update 3 でテンプレートが変更されました。</span><span class="sxs-lookup"><span data-stu-id="7e34b-117">The template changed in Update 3.</span></span> <span data-ttu-id="7e34b-118">このトピックでは、Update 2 および Update 3 でテンプレートを変更する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="7e34b-118">This topic shows how to change the template in Update 2 and Update 3.</span></span>

<span data-ttu-id="7e34b-119">このトピックには、次のセクションが含まれます。</span><span class="sxs-lookup"><span data-stu-id="7e34b-119">This topic contains the following sections:</span></span>

- [<span data-ttu-id="7e34b-120">Identity user クラスのキーの種類を変更する</span><span class="sxs-lookup"><span data-stu-id="7e34b-120">Change the type of the key in the Identity user class</span></span>](#userclass)
- [<span data-ttu-id="7e34b-121">キーの種類を使用するカスタマイズされた Id クラスを追加する</span><span class="sxs-lookup"><span data-stu-id="7e34b-121">Add customized Identity classes that use the key type</span></span>](#customclass)
- [<span data-ttu-id="7e34b-122">キーの種類を使用するようにコンテキストクラスとユーザーマネージャーを変更する</span><span class="sxs-lookup"><span data-stu-id="7e34b-122">Change the context class and user manager to use the key type</span></span>](#context)
- [<span data-ttu-id="7e34b-123">キーの種類を使用するようにスタートアップ構成を変更する</span><span class="sxs-lookup"><span data-stu-id="7e34b-123">Change start-up configuration to use the key type</span></span>](#startup)
- [<span data-ttu-id="7e34b-124">Update 2 の MVC では、キーの種類を渡すために AccountController を変更します。</span><span class="sxs-lookup"><span data-stu-id="7e34b-124">For MVC with Update 2, change the AccountController to pass the key type</span></span>](#mvcupdate2)
- [<span data-ttu-id="7e34b-125">Update 3 の MVC では、キーの種類を渡すように AccountController と ManageController を変更します。</span><span class="sxs-lookup"><span data-stu-id="7e34b-125">For MVC with Update 3, change the AccountController and ManageController to pass the key type</span></span>](#mvcupdate3)
- [<span data-ttu-id="7e34b-126">Web フォーム Update 2 では、キーの種類を渡すようにアカウントページを変更します。</span><span class="sxs-lookup"><span data-stu-id="7e34b-126">For Web Forms with Update 2, change Account pages to pass the key type</span></span>](#webformsupdate2)
- [<span data-ttu-id="7e34b-127">Update 3 で Web フォームを使用する場合は、キーの種類を渡すようにアカウントページを変更します。</span><span class="sxs-lookup"><span data-stu-id="7e34b-127">For Web Forms with Update 3, change Account pages to pass the key type</span></span>](#webformsupdate3)
- [<span data-ttu-id="7e34b-128">アプリケーションの実行</span><span class="sxs-lookup"><span data-stu-id="7e34b-128">Run application</span></span>](#run)
- [<span data-ttu-id="7e34b-129">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="7e34b-129">Other resources</span></span>](#other)

<a id="userclass"></a>
## <a name="change-the-type-of-the-key-in-the-identity-user-class"></a><span data-ttu-id="7e34b-130">Identity user クラスのキーの種類を変更する</span><span class="sxs-lookup"><span data-stu-id="7e34b-130">Change the type of the key in the Identity user class</span></span>

<span data-ttu-id="7e34b-131">ASP.NET Web アプリケーションテンプレートから作成したプロジェクトで、ApplicationUser クラスがユーザーアカウントのキーに整数を使用するように指定します。</span><span class="sxs-lookup"><span data-stu-id="7e34b-131">In your project created from the ASP.NET Web Application template, specify that the ApplicationUser class uses an integer for the key for user accounts.</span></span> <span data-ttu-id="7e34b-132">IdentityModels.cs の ApplicationUser クラスを、TKey ジェネリックパラメーターの**int**型を持つユーザーから継承するように変更します。</span><span class="sxs-lookup"><span data-stu-id="7e34b-132">In IdentityModels.cs, change the ApplicationUser class to inherit from IdentityUser that has a type of **int** for the TKey generic parameter.</span></span> <span data-ttu-id="7e34b-133">まだ実装していない3つのカスタマイズされたクラスの名前を渡すこともできます。</span><span class="sxs-lookup"><span data-stu-id="7e34b-133">You also pass the names of three customized class which you have not implemented yet.</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample1.cs?highlight=1-2)]

<span data-ttu-id="7e34b-134">キーの種類を変更しましたが、既定では、アプリケーションの残りの部分では、キーが文字列であると想定しています。</span><span class="sxs-lookup"><span data-stu-id="7e34b-134">You have changed the type of the key, but, by default, the rest of the application still assumes the key is a string.</span></span> <span data-ttu-id="7e34b-135">文字列を想定するコードでは、キーの型を明示的に指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7e34b-135">You must explicitly indicate the type of the key in code that assumes a string.</span></span>

<span data-ttu-id="7e34b-136">次の強調表示されているコードに示すように、 **Applicationuser**クラスで、 **Generateuserの async**メソッドを変更して int を含めます。</span><span class="sxs-lookup"><span data-stu-id="7e34b-136">In the **ApplicationUser** class, change the **GenerateUserIdentityAsync** method to include int, as shown in the highlighted code below.</span></span> <span data-ttu-id="7e34b-137">この変更は、Update 3 テンプレートを使用した Web フォームプロジェクトには必要ありません。</span><span class="sxs-lookup"><span data-stu-id="7e34b-137">This change is not necessary for Web Forms projects with the Update 3 template.</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample2.cs?highlight=2)]

<a id="customclass"></a>
## <a name="add-customized-identity-classes-that-use-the-key-type"></a><span data-ttu-id="7e34b-138">キーの種類を使用するカスタマイズされた Id クラスを追加する</span><span class="sxs-lookup"><span data-stu-id="7e34b-138">Add customized Identity classes that use the key type</span></span>

<span data-ttu-id="7e34b-139">その他の Id クラス (ユーザー Id、ユーザー Id クレーム、ユーザー名ログイン、Id ロール、UserStore、RoleStore など) は、文字列キーを使用するように設定されたままです。</span><span class="sxs-lookup"><span data-stu-id="7e34b-139">The other Identity classes, such as IdentityUserRole, IdentityUserClaim, IdentityUserLogin, IdentityRole, UserStore, RoleStore, are still set up to use a string key.</span></span> <span data-ttu-id="7e34b-140">キーの整数を指定する、これらのクラスの新しいバージョンを作成します。</span><span class="sxs-lookup"><span data-stu-id="7e34b-140">Create new versions of these classes that specify an integer for the key.</span></span> <span data-ttu-id="7e34b-141">これらのクラスでは、多くの実装コードを指定する必要はありません。主に、キーとして int を設定するだけです。</span><span class="sxs-lookup"><span data-stu-id="7e34b-141">You do not need to provide much implementation code in these classes, you are primarily just setting int as the key.</span></span>

<span data-ttu-id="7e34b-142">IdentityModels.cs ファイルに次のクラスを追加します。</span><span class="sxs-lookup"><span data-stu-id="7e34b-142">Add the following classes to your IdentityModels.cs file.</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample3.cs)]

<a id="context"></a>
## <a name="change-the-context-class-and-user-manager-to-use-the-key-type"></a><span data-ttu-id="7e34b-143">キーの種類を使用するようにコンテキストクラスとユーザーマネージャーを変更する</span><span class="sxs-lookup"><span data-stu-id="7e34b-143">Change the context class and user manager to use the key type</span></span>

<span data-ttu-id="7e34b-144">IdentityModels.cs で、新しいカスタマイズされたクラスを使用するように**Applicationdbcontext**クラスの定義を変更し、強調表示されているコードに示されているように、キーの**int**を使用します。</span><span class="sxs-lookup"><span data-stu-id="7e34b-144">In IdentityModels.cs, change the definition of the **ApplicationDbContext** class to use your new customized classes and an **int** for the key, as shown in the highlighted code.</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample4.cs?highlight=1-2)]

<span data-ttu-id="7e34b-145">ThrowIfV1Schema パラメーターがコンストラクターで有効ではなくなりました。</span><span class="sxs-lookup"><span data-stu-id="7e34b-145">The ThrowIfV1Schema parameter is no longer valid in the constructor.</span></span> <span data-ttu-id="7e34b-146">ThrowIfV1Schema 値が渡されないようにコンストラクターを変更します。</span><span class="sxs-lookup"><span data-stu-id="7e34b-146">Change the constructor so it does not pass a ThrowIfV1Schema value.</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample5.cs)]

<span data-ttu-id="7e34b-147">IdentityConfig.cs を開き、 **Applicationusermanger**クラスを変更して、データを保持するための新しいユーザーストアクラスとキーの**int**を使用するように変更します。</span><span class="sxs-lookup"><span data-stu-id="7e34b-147">Open IdentityConfig.cs, and change the **ApplicationUserManger** class to use your new user store class for persisting data and an **int** for the key.</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample6.cs?highlight=1,3,12,14,32,37,48)]

<span data-ttu-id="7e34b-148">Update 3 テンプレートでは、ApplicationSignInManager クラスを変更する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7e34b-148">In the Update 3 template, you must change the ApplicationSignInManager class.</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample7.cs?highlight=1)]

<a id="startup"></a>
## <a name="change-start-up-configuration-to-use-the-key-type"></a><span data-ttu-id="7e34b-149">キーの種類を使用するようにスタートアップ構成を変更する</span><span class="sxs-lookup"><span data-stu-id="7e34b-149">Change start-up configuration to use the key type</span></span>

<span data-ttu-id="7e34b-150">Startup.Auth.cs で、下の強調表示されているように OnValidateIdentity コードを置き換えます。</span><span class="sxs-lookup"><span data-stu-id="7e34b-150">In Startup.Auth.cs, replace the OnValidateIdentity code, as highlighted below.</span></span> <span data-ttu-id="7e34b-151">GetUserIdCallback 定義により、文字列値が整数に解析されることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="7e34b-151">Notice that the getUserIdCallback definition, parses the string value into an integer.</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample8.cs?highlight=7-12)]

<span data-ttu-id="7e34b-152">プロジェクトが**Getuserid**メソッドのジェネリック実装を認識しない場合は、ASP.NET Identity NuGet パッケージをバージョン2.1 に更新する必要がある場合があります。</span><span class="sxs-lookup"><span data-stu-id="7e34b-152">If your project does not recognize the generic implementation of the **GetUserId** method, you may need to update the ASP.NET Identity NuGet package to version 2.1</span></span>

<span data-ttu-id="7e34b-153">ASP.NET Identity によって使用されるインフラストラクチャクラスに多数の変更が加えられました。</span><span class="sxs-lookup"><span data-stu-id="7e34b-153">You have made a lot of changes to the infrastructure classes used by ASP.NET Identity.</span></span> <span data-ttu-id="7e34b-154">プロジェクトをコンパイルしようとすると、多数のエラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="7e34b-154">If you try compiling the project, you will notice a lot of errors.</span></span> <span data-ttu-id="7e34b-155">幸い、残りのエラーはすべて類似しています。</span><span class="sxs-lookup"><span data-stu-id="7e34b-155">Fortunately, the remaining errors are all similar.</span></span> <span data-ttu-id="7e34b-156">Id クラスはキーに整数を必要としますが、コントローラー (または Web フォーム) は文字列値を渡しています。</span><span class="sxs-lookup"><span data-stu-id="7e34b-156">The Identity class expects an integer for the key, but the controller (or Web Form) is passing a string value.</span></span> <span data-ttu-id="7e34b-157">どちらの場合も、 **Getuserid&lt;int&gt;** を呼び出すことにより、文字列をと整数に変換する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7e34b-157">In each case, you need to convert from a string to and integer by calling **GetUserId&lt;int&gt;**.</span></span> <span data-ttu-id="7e34b-158">コンパイルからエラー一覧を処理するか、次の変更を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="7e34b-158">You can either work through the error list from compilation or follow the changes below.</span></span>

<span data-ttu-id="7e34b-159">残りの変更は、作成するプロジェクトの種類と、Visual Studio にインストールした更新プログラムによって異なります。</span><span class="sxs-lookup"><span data-stu-id="7e34b-159">The remaining changes depend on the type of project you are creating and which update you have installed in Visual Studio.</span></span> <span data-ttu-id="7e34b-160">関連するセクションに直接アクセスするには、次のリンクを使用します。</span><span class="sxs-lookup"><span data-stu-id="7e34b-160">You can go directly to the relevant section through the following links</span></span>

- [<span data-ttu-id="7e34b-161">Update 2 の MVC では、キーの種類を渡すために AccountController を変更します。</span><span class="sxs-lookup"><span data-stu-id="7e34b-161">For MVC with Update 2, change the AccountController to pass the key type</span></span>](#mvcupdate2)
- [<span data-ttu-id="7e34b-162">Update 3 の MVC では、キーの種類を渡すように AccountController と ManageController を変更します。</span><span class="sxs-lookup"><span data-stu-id="7e34b-162">For MVC with Update 3, change the AccountController and ManageController to pass the key type</span></span>](#mvcupdate3)
- [<span data-ttu-id="7e34b-163">Web フォーム Update 2 では、キーの種類を渡すようにアカウントページを変更します。</span><span class="sxs-lookup"><span data-stu-id="7e34b-163">For Web Forms with Update 2, change Account pages to pass the key type</span></span>](#webformsupdate2)
- [<span data-ttu-id="7e34b-164">Update 3 で Web フォームを使用する場合は、キーの種類を渡すようにアカウントページを変更します。</span><span class="sxs-lookup"><span data-stu-id="7e34b-164">For Web Forms with Update 3, change Account pages to pass the key type</span></span>](#webformsupdate3)

<a id="mvcupdate2"></a>
## <a name="for-mvc-with-update-2-change-the-accountcontroller-to-pass-the-key-type"></a><span data-ttu-id="7e34b-165">Update 2 の MVC では、キーの種類を渡すために AccountController を変更します。</span><span class="sxs-lookup"><span data-stu-id="7e34b-165">For MVC with Update 2, change the AccountController to pass the key type</span></span>

<span data-ttu-id="7e34b-166">AccountController.cs ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="7e34b-166">Open the AccountController.cs file.</span></span> <span data-ttu-id="7e34b-167">次のメソッドを変更する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7e34b-167">You need to change the following methods.</span></span>

<span data-ttu-id="7e34b-168">**ConfirmEmail**メソッド</span><span class="sxs-lookup"><span data-stu-id="7e34b-168">**ConfirmEmail** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample9.cs?highlight=1,3)]

<span data-ttu-id="7e34b-169">**関連付け**解除メソッド</span><span class="sxs-lookup"><span data-stu-id="7e34b-169">**Disassociate** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample10.cs?highlight=5,9)]

<span data-ttu-id="7e34b-170">**Manage (ManageUserViewModel)** メソッド</span><span class="sxs-lookup"><span data-stu-id="7e34b-170">**Manage(ManageUserViewModel)** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample11.cs?highlight=11,17,41)]

<span data-ttu-id="7e34b-171">**Linklogincallback**メソッド</span><span class="sxs-lookup"><span data-stu-id="7e34b-171">**LinkLoginCallback** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample12.cs?highlight=10)]

<span data-ttu-id="7e34b-172">**Removeaccountlist**メソッド</span><span class="sxs-lookup"><span data-stu-id="7e34b-172">**RemoveAccountList** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample13.cs?highlight=3)]

<span data-ttu-id="7e34b-173">**Haspassword**メソッド</span><span class="sxs-lookup"><span data-stu-id="7e34b-173">**HasPassword** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample14.cs?highlight=3)]

<span data-ttu-id="7e34b-174">これで、[アプリケーションを実行](#run)し、新しいユーザーを登録できます。</span><span class="sxs-lookup"><span data-stu-id="7e34b-174">You can now [run the application](#run) and register a new user.</span></span>

<a id="mvcupdate3"></a>
## <a name="for-mvc-with-update-3-change-the-accountcontroller-and-managecontroller-to-pass-the-key-type"></a><span data-ttu-id="7e34b-175">Update 3 の MVC では、キーの種類を渡すように AccountController と ManageController を変更します。</span><span class="sxs-lookup"><span data-stu-id="7e34b-175">For MVC with Update 3, change the AccountController and ManageController to pass the key type</span></span>

<span data-ttu-id="7e34b-176">AccountController.cs ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="7e34b-176">Open the AccountController.cs file.</span></span> <span data-ttu-id="7e34b-177">次のメソッドを変更する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7e34b-177">You need to change the following method.</span></span>

<span data-ttu-id="7e34b-178">**ConfirmEmail**メソッド</span><span class="sxs-lookup"><span data-stu-id="7e34b-178">**ConfirmEmail** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample15.cs?highlight=1,3)]

<span data-ttu-id="7e34b-179">**Sendcode**メソッド</span><span class="sxs-lookup"><span data-stu-id="7e34b-179">**SendCode** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample16.cs?highlight=4)]

<span data-ttu-id="7e34b-180">ManageController.cs ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="7e34b-180">Open the ManageController.cs file.</span></span> <span data-ttu-id="7e34b-181">次のメソッドを変更する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7e34b-181">You need to change the following methods.</span></span>

<span data-ttu-id="7e34b-182">**Index**メソッド</span><span class="sxs-lookup"><span data-stu-id="7e34b-182">**Index** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample17.cs?highlight=15-17)]

<span data-ttu-id="7e34b-183">**Removelogin**メソッド</span><span class="sxs-lookup"><span data-stu-id="7e34b-183">**RemoveLogin** methods</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample18.cs?highlight=3,13,17)]

<span data-ttu-id="7e34b-184">**AddPhoneNumber**メソッド</span><span class="sxs-lookup"><span data-stu-id="7e34b-184">**AddPhoneNumber** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample19.cs?highlight=9)]

<span data-ttu-id="7e34b-185">**EnableTwoFactorAuthentication**メソッド</span><span class="sxs-lookup"><span data-stu-id="7e34b-185">**EnableTwoFactorAuthentication** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample20.cs?highlight=3-4)]

<span data-ttu-id="7e34b-186">**DisableTwoFactorAuthentication**メソッド</span><span class="sxs-lookup"><span data-stu-id="7e34b-186">**DisableTwoFactorAuthentication** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample21.cs?highlight=3-4)]

<span data-ttu-id="7e34b-187">**VerifyPhoneNumber**メソッド</span><span class="sxs-lookup"><span data-stu-id="7e34b-187">**VerifyPhoneNumber** methods</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample22.cs?highlight=4,18,21)]

<span data-ttu-id="7e34b-188">**RemovePhoneNumber**メソッド</span><span class="sxs-lookup"><span data-stu-id="7e34b-188">**RemovePhoneNumber** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample23.cs?highlight=3,8)]

<span data-ttu-id="7e34b-189">**ChangePassword**メソッド</span><span class="sxs-lookup"><span data-stu-id="7e34b-189">**ChangePassword** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample24.cs?highlight=10,13)]

<span data-ttu-id="7e34b-190">**SetPassword**メソッド</span><span class="sxs-lookup"><span data-stu-id="7e34b-190">**SetPassword** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample25.cs?highlight=5,8)]

<span data-ttu-id="7e34b-191">**Managelogins**メソッド</span><span class="sxs-lookup"><span data-stu-id="7e34b-191">**ManageLogins** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample26.cs?highlight=7,12)]

<span data-ttu-id="7e34b-192">**Linklogincallback**メソッド</span><span class="sxs-lookup"><span data-stu-id="7e34b-192">**LinkLoginCallback** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample27.cs?highlight=8)]

<span data-ttu-id="7e34b-193">**Haspassword**メソッド</span><span class="sxs-lookup"><span data-stu-id="7e34b-193">**HasPassword** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample28.cs?highlight=3)]

<span data-ttu-id="7e34b-194">**HasPhoneNumber**メソッド</span><span class="sxs-lookup"><span data-stu-id="7e34b-194">**HasPhoneNumber** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample29.cs?highlight=3)]

<span data-ttu-id="7e34b-195">これで、[アプリケーションを実行](#run)し、新しいユーザーを登録できます。</span><span class="sxs-lookup"><span data-stu-id="7e34b-195">You can now [run the application](#run) and register a new user.</span></span>

<a id="webformsupdate2"></a>
## <a name="for-web-forms-with-update-2-change-account-pages-to-pass-the-key-type"></a><span data-ttu-id="7e34b-196">Web フォーム Update 2 では、キーの種類を渡すようにアカウントページを変更します。</span><span class="sxs-lookup"><span data-stu-id="7e34b-196">For Web Forms with Update 2, change Account pages to pass the key type</span></span>

<span data-ttu-id="7e34b-197">Web フォーム Update 2 では、次のページを変更する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7e34b-197">For Web Forms with Update 2, you need to change the following pages.</span></span>

<span data-ttu-id="7e34b-198">**Confirm.aspx.cx**</span><span class="sxs-lookup"><span data-stu-id="7e34b-198">**Confirm.aspx.cx**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample30.cs?highlight=8)]

<span data-ttu-id="7e34b-199">**RegisterExternalLogin.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="7e34b-199">**RegisterExternalLogin.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample31.cs?highlight=36)]

<span data-ttu-id="7e34b-200">**Manage.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="7e34b-200">**Manage.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample32.cs?highlight=3,22,47,52,69,85,93,98)]

<span data-ttu-id="7e34b-201">これで、[アプリケーションを実行](#run)し、新しいユーザーを登録できます。</span><span class="sxs-lookup"><span data-stu-id="7e34b-201">You can now [run the application](#run) and register a new user.</span></span>

<a id="webformsupdate3"></a>
## <a name="for-web-forms-with-update-3-change-account-pages-to-pass-the-key-type"></a><span data-ttu-id="7e34b-202">Update 3 で Web フォームを使用する場合は、キーの種類を渡すようにアカウントページを変更します。</span><span class="sxs-lookup"><span data-stu-id="7e34b-202">For Web Forms with Update 3, change Account pages to pass the key type</span></span>

<span data-ttu-id="7e34b-203">Update 3 で Web フォームを使用する場合は、次のページを変更する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7e34b-203">For Web Forms with Update 3, you need to change the following pages.</span></span>

<span data-ttu-id="7e34b-204">**Confirm.aspx.cx**</span><span class="sxs-lookup"><span data-stu-id="7e34b-204">**Confirm.aspx.cx**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample33.cs?highlight=8)]

<span data-ttu-id="7e34b-205">**RegisterExternalLogin.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="7e34b-205">**RegisterExternalLogin.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample34.cs?highlight=36)]

<span data-ttu-id="7e34b-206">**Manage.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="7e34b-206">**Manage.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample35.cs?highlight=11,27,32,34,82,87,99,108)]

<span data-ttu-id="7e34b-207">**VerifyPhoneNumber.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="7e34b-207">**VerifyPhoneNumber.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample36.cs?highlight=8,23,27)]

<span data-ttu-id="7e34b-208">**AddPhoneNumber.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="7e34b-208">**AddPhoneNumber.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample37.cs?highlight=7)]

<span data-ttu-id="7e34b-209">**ManagePassword.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="7e34b-209">**ManagePassword.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample38.cs?highlight=11,47,50,68)]

<span data-ttu-id="7e34b-210">**ManageLogins.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="7e34b-210">**ManageLogins.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample39.cs?highlight=16,23,32,41,45)]

<span data-ttu-id="7e34b-211">**TwoFactorAuthenticationSignIn.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="7e34b-211">**TwoFactorAuthenticationSignIn.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample40.cs?highlight=14-15,29,53)]

<a id="run"></a>
## <a name="run-application"></a><span data-ttu-id="7e34b-212">アプリケーションを実行する</span><span class="sxs-lookup"><span data-stu-id="7e34b-212">Run application</span></span>

<span data-ttu-id="7e34b-213">既定の Web アプリケーションテンプレートに必要なすべての変更が完了しました。</span><span class="sxs-lookup"><span data-stu-id="7e34b-213">You have finished all of the required changes to the default Web Application template.</span></span> <span data-ttu-id="7e34b-214">アプリケーションを実行し、新しいユーザーを登録します。</span><span class="sxs-lookup"><span data-stu-id="7e34b-214">Run the application and register a new user.</span></span> <span data-ttu-id="7e34b-215">ユーザーを登録すると、AspNetUsers テーブルには整数の Id 列があることがわかります。</span><span class="sxs-lookup"><span data-stu-id="7e34b-215">After registering the user, you will notice that the AspNetUsers table has an Id column that is an integer.</span></span>

![新しい主キー](change-primary-key-for-users-in-aspnet-identity/_static/image1.png)

<span data-ttu-id="7e34b-217">主キーが異なる ASP.NET Identity テーブルを既に作成している場合は、いくつかの追加の変更を行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="7e34b-217">If you have previously created the ASP.NET Identity tables with a different primary key, you need to make some additional changes.</span></span> <span data-ttu-id="7e34b-218">可能であれば、既存のデータベースを削除するだけです。</span><span class="sxs-lookup"><span data-stu-id="7e34b-218">If possible, just delete the existing database.</span></span> <span data-ttu-id="7e34b-219">Web アプリケーションを実行して新しいユーザーを追加すると、適切なデザインでデータベースが再作成されます。</span><span class="sxs-lookup"><span data-stu-id="7e34b-219">The database will be re-created with the correct design when you run the web application and add a new user.</span></span> <span data-ttu-id="7e34b-220">削除できない場合は、code first の移行を実行してテーブルを変更します。</span><span class="sxs-lookup"><span data-stu-id="7e34b-220">If deletion is not possible, run code first migrations to change the tables.</span></span> <span data-ttu-id="7e34b-221">ただし、新しい整数の主キーは、データベースの SQL ID プロパティとしては設定されません。</span><span class="sxs-lookup"><span data-stu-id="7e34b-221">However, the new integer primary key will not be set up as a SQL IDENTITY property in the database.</span></span> <span data-ttu-id="7e34b-222">Id 列は、手動で id として設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7e34b-222">You must manually set the Id column as an IDENTITY.</span></span>

<a id="other"></a>
## <a name="other-resources"></a><span data-ttu-id="7e34b-223">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="7e34b-223">Other resources</span></span>

- [<span data-ttu-id="7e34b-224">ASP.NET Identity のカスタム ストレージ プロバイダーの概要</span><span class="sxs-lookup"><span data-stu-id="7e34b-224">Overview of Custom Storage Providers for ASP.NET Identity</span></span>](overview-of-custom-storage-providers-for-aspnet-identity.md)
- [<span data-ttu-id="7e34b-225">既存 Web サイトを SQL メンバーシップから ASP.NET Identity に移行する</span><span class="sxs-lookup"><span data-stu-id="7e34b-225">Migrating an Existing Website from SQL Membership to ASP.NET Identity</span></span>](../migrations/migrating-an-existing-website-from-sql-membership-to-aspnet-identity.md)
- [<span data-ttu-id="7e34b-226">メンバーシップとユーザープロファイルのユニバーサルプロバイダーデータを ASP.NET Identity に移行する</span><span class="sxs-lookup"><span data-stu-id="7e34b-226">Migrating Universal Provider Data for Membership and User Profiles to ASP.NET Identity</span></span>](../migrations/migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity.md)
- <span data-ttu-id="7e34b-227">主キーが変更された[サンプルアプリケーション](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/ChangePK)</span><span class="sxs-lookup"><span data-stu-id="7e34b-227">[Sample application](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/ChangePK) with changed primary key</span></span>
