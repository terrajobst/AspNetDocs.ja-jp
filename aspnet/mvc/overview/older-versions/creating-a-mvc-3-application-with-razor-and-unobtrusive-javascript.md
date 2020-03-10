---
uid: mvc/overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript
title: Razor および控えめな JavaScript を使用した MVC 3 アプリケーションの作成 |Microsoft Docs
author: microsoft
description: ユーザー一覧のサンプル web アプリケーションでは、Razor ビューエンジンを使用して ASP.NET MVC 3 アプリケーションを簡単に作成する方法を示しています。 サンプルアプリケーション...
ms.author: riande
ms.date: 11/01/2010
ms.assetid: 658b149b-d770-46bf-8b4b-4e47cca242f3
msc.legacyurl: /mvc/overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript
msc.type: authoredcontent
ms.openlocfilehash: fb63493ff22c9261fc5746a998a32f2511141f87
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78434998"
---
# <a name="creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript"></a><span data-ttu-id="a3e6a-104">Razor および控えめな JavaScript を使用した MVC 3 アプリケーションの作成</span><span class="sxs-lookup"><span data-stu-id="a3e6a-104">Creating a MVC 3 Application with Razor and Unobtrusive JavaScript</span></span>

<span data-ttu-id="a3e6a-105">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="a3e6a-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="a3e6a-106">ユーザー一覧のサンプル web アプリケーションでは、Razor ビューエンジンを使用して ASP.NET MVC 3 アプリケーションを簡単に作成する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-106">The User List sample web application demonstrates how simple it is to create ASP.NET MVC 3 applications using the Razor view engine.</span></span> <span data-ttu-id="a3e6a-107">このサンプルアプリケーションでは、ASP.NET MVC version 3 と Visual Studio 2010 で新しい Razor ビューエンジンを使用して、ユーザーの作成、表示、編集、削除などの機能を含む架空のユーザーリスト web サイトを作成する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-107">The sample application shows how to use the new Razor view engine with ASP.NET MVC version 3 and Visual Studio 2010 to create a fictional User List website that includes functionality such as creating, displaying, editing, and deleting users.</span></span>
> 
> <span data-ttu-id="a3e6a-108">このチュートリアルでは、ユーザーリストのサンプル ASP.NET MVC 3 アプリケーションをビルドするために実行された手順について説明します。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-108">This tutorial describes the steps that were taken in order to build the User List sample ASP.NET MVC 3 application.</span></span> <span data-ttu-id="a3e6a-109">このトピックでC#は、visual Studio プロジェクトと VB ソースコードを[ダウンロード](https://code.msdn.microsoft.com/aspnetmvcsamples/Release/ProjectReleases.aspx?ReleaseId=5114)できます。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-109">A Visual Studio project with C# and VB source code is available to accompany this topic: [Download](https://code.msdn.microsoft.com/aspnetmvcsamples/Release/ProjectReleases.aspx?ReleaseId=5114).</span></span> <span data-ttu-id="a3e6a-110">このチュートリアルについてご不明な点がある場合は、 [MVC フォーラム](https://forums.asp.net/1146.aspx)に投稿してください。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-110">If you have questions about this tutorial, please post them to the [MVC forum](https://forums.asp.net/1146.aspx).</span></span>

## <a name="overview"></a><span data-ttu-id="a3e6a-111">概要</span><span class="sxs-lookup"><span data-stu-id="a3e6a-111">Overview</span></span>

<span data-ttu-id="a3e6a-112">構築するアプリケーションは、単純なユーザーリストの web サイトです。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-112">The application you'll be building is a simple user list website.</span></span> <span data-ttu-id="a3e6a-113">ユーザーは、ユーザー情報の入力、表示、および更新を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-113">Users can enter, view, and update user information.</span></span>

![サンプルサイト](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image1.png)

<span data-ttu-id="a3e6a-115">[ここで](https://code.msdn.microsoft.com/Creating-a-MVC-3-28883c0f)は、VB およびC#完成したプロジェクトをダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-115">You can download the VB and C# completed project [here](https://code.msdn.microsoft.com/Creating-a-MVC-3-28883c0f).</span></span>

## <a name="creating-the-web-application"></a><span data-ttu-id="a3e6a-116">Web アプリケーションの作成</span><span class="sxs-lookup"><span data-stu-id="a3e6a-116">Creating the Web Application</span></span>

<span data-ttu-id="a3e6a-117">チュートリアルを開始するには、Visual Studio 2010 を開き、 *ASP.NET MVC 3 Web アプリケーション*テンプレートを使用して新しいプロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-117">To start the tutorial, open Visual Studio 2010 and create a new project using the *ASP.NET MVC 3 Web Application* template.</span></span> <span data-ttu-id="a3e6a-118">アプリケーション &quot;Mvc3Razor&quot;という名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-118">Name the application &quot;Mvc3Razor&quot;.</span></span>

<span data-ttu-id="a3e6a-119">[新しい MVC 3 プロジェクトの ![](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image3.png)](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image2.png)</span><span class="sxs-lookup"><span data-stu-id="a3e6a-119">[![New MVC 3 project](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image3.png)](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image2.png)</span></span>

<span data-ttu-id="a3e6a-120">**[New ASP.NET MVC 3 プロジェクト]** ダイアログボックスで、 **[インターネットアプリケーション]** を選択し、Razor ビューエンジンを選択して、 **[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-120">In the **New ASP.NET MVC 3 Project** dialog, select **Internet Application**, select the Razor view engine, and then click **OK**.</span></span>

![新しい ASP.NET MVC 3 プロジェクトダイアログ](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image4.png)

<span data-ttu-id="a3e6a-122">このチュートリアルでは、ASP.NET メンバーシッププロバイダーを使用しないので、ログオンとメンバーシップに関連付けられているすべてのファイルを削除できます。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-122">In this tutorial you will not be using the ASP.NET membership provider, so you can delete all the files associated with logon and membership.</span></span> <span data-ttu-id="a3e6a-123">**ソリューションエクスプローラー**で、次のファイルとディレクトリを削除します。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-123">In **Solution Explorer**, remove the following files and directories:</span></span>

- <span data-ttu-id="a3e6a-124">*コントローラー \ アカウント*</span><span class="sxs-lookup"><span data-stu-id="a3e6a-124">*Controllers\AccountController*</span></span>
- <span data-ttu-id="a3e6a-125">*Models\AccountModels*</span><span class="sxs-lookup"><span data-stu-id="a3e6a-125">*Models\AccountModels*</span></span>
- <span data-ttu-id="a3e6a-126">*Views\Shared\\_LogOnPartial*</span><span class="sxs-lookup"><span data-stu-id="a3e6a-126">*Views\Shared\\_LogOnPartial*</span></span>
- <span data-ttu-id="a3e6a-127">*Views\Account* (およびこのディレクトリ内のすべてのファイル)</span><span class="sxs-lookup"><span data-stu-id="a3e6a-127">*Views\Account* (and all the files in this directory)</span></span>

![% N Exp](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image5.png)

<span data-ttu-id="a3e6a-129"><em>\_Layout</em>ファイルを編集し、`logindisplay` という名前の `<div>` 要素内のマークアップを、ログインが無効になっている&quot;<em>&quot;</em>メッセージに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-129">Edit the <em>\_Layout.cshtml</em> file and replace the markup inside the `<div>` element named `logindisplay` with the message <em>&quot;</em>Login Disabled&quot;.</span></span> <span data-ttu-id="a3e6a-130">新しいマークアップの例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-130">The following example shows the new markup:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample1.cshtml)]

## <a name="adding-the-model"></a><span data-ttu-id="a3e6a-131">モデルの追加</span><span class="sxs-lookup"><span data-stu-id="a3e6a-131">Adding the Model</span></span>

<span data-ttu-id="a3e6a-132">**ソリューションエクスプローラー**で、[*モデル*] フォルダーを右クリックし、 **[追加]** 、 **[クラス]** の順にクリックします。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-132">In **Solution Explorer**, right-click the *Models* folder, select **Add**, and then click **Class**.</span></span>

![新しいユーザー Mdl クラス](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image6.png)

<span data-ttu-id="a3e6a-134">クラスに `UserModel` という名前を付けます。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-134">Name the class `UserModel`.</span></span> <span data-ttu-id="a3e6a-135">*Usermodel*ファイルの内容を次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-135">Replace the contents of the *UserModel* file with the following code:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample2.cs)]

<span data-ttu-id="a3e6a-136">`UserModel` クラスは、ユーザーを表します。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-136">The `UserModel` class represents users.</span></span> <span data-ttu-id="a3e6a-137">クラスの各メンバーには、 [Dataannotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)名前空間の[Required](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx)属性で注釈が付けられます。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-137">Each member of the class is annotated with the [Required](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) attribute from the [DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) namespace.</span></span> <span data-ttu-id="a3e6a-138">[Dataannotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)名前空間の属性は、web アプリケーションのクライアント側およびサーバー側の自動検証を提供します。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-138">The attributes in the [DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) namespace provide automatic client- and server-side validation for web applications.</span></span>

<span data-ttu-id="a3e6a-139">`HomeController` クラスを開き、`UserModel` および `Users` クラスにアクセスできるように、`using` ディレクティブを追加します。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-139">Open the `HomeController` class and add a `using` directive so that you can access the `UserModel` and `Users` classes:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample3.cs)]

<span data-ttu-id="a3e6a-140">`HomeController` 宣言の直後に、次のコメントと、`Users` クラスへの参照を追加します。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-140">Just after the `HomeController` declaration, add the following comment and the reference to a `Users` class:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample4.cs)]

<span data-ttu-id="a3e6a-141">`Users` クラスは、このチュートリアルで使用する簡素化されたインメモリデータストアです。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-141">The `Users` class is a simplified, in-memory data store that you'll use in this tutorial.</span></span> <span data-ttu-id="a3e6a-142">実際のアプリケーションでは、データベースを使用してユーザー情報を格納します。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-142">In a real application you would use a database to store user information.</span></span> <span data-ttu-id="a3e6a-143">`HomeController` ファイルの最初の数行を次の例に示します。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-143">The first few lines of the `HomeController` file are shown in the following example:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample5.cs)]

<span data-ttu-id="a3e6a-144">アプリケーションをビルドして、次の手順でスキャフォールディングウィザードでユーザーモデルが使用できるようにします。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-144">Build the application so that the user model will be available to the scaffolding wizard in the next step.</span></span>

## <a name="creating-the-default-view"></a><span data-ttu-id="a3e6a-145">既定のビューの作成</span><span class="sxs-lookup"><span data-stu-id="a3e6a-145">Creating the Default View</span></span>

<span data-ttu-id="a3e6a-146">次の手順では、ユーザーを表示するためのアクションメソッドとビューを追加します。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-146">The next step is to add an action method and view to display the users.</span></span>

<span data-ttu-id="a3e6a-147">既存の*Views\Home\Index*ファイルを削除します。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-147">Delete the existing *Views\Home\Index* file.</span></span> <span data-ttu-id="a3e6a-148">ユーザーを表示するには、新しい*インデックス*ファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-148">You will create a new *Index* file to display the users.</span></span>

<span data-ttu-id="a3e6a-149">`HomeController` クラスで、`Index` メソッドの内容を次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-149">In the `HomeController` class, replace the contents of the `Index` method with the following code:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample6.cs)]

<span data-ttu-id="a3e6a-150">`Index` メソッド内を右クリックし、 **[ビューの追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-150">Right-click inside the `Index` method and then click **Add View**.</span></span>

![ビューの追加](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image7.png)

<span data-ttu-id="a3e6a-152">**[厳密に型指定されたビューを作成する]** オプションを選択します。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-152">Select the **Create a strongly-typed view** option.</span></span> <span data-ttu-id="a3e6a-153">**[ビューデータクラス]** で、 **[Mvc3Razor]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-153">For **View data class**, select **Mvc3Razor.Models.UserModel**.</span></span> <span data-ttu-id="a3e6a-154">( **[データクラスの表示]** ボックスに**Mvc3Razor**が表示されない場合は、プロジェクトをビルドする必要があります)。ビューエンジンが**Razor**に設定されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-154">(If you don't see **Mvc3Razor.Models.UserModel** in the **View data class** box, you need to build the project.) Make sure that the view engine is set to **Razor**.</span></span> <span data-ttu-id="a3e6a-155">**[表示コンテンツ]** を **[一覧]** に設定 に設定し、 **[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-155">Set **View content** to **List** and then click **Add**.</span></span>

![インデックスビューの追加](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image8.png)

<span data-ttu-id="a3e6a-157">新しいビューでは、`Index` ビューに渡されたユーザーデータが自動的にスキャフォールディングされます。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-157">The new view automatically scaffolds the user data that's passed to the `Index` view.</span></span> <span data-ttu-id="a3e6a-158">新しく生成された*Views\Home\Index*ファイルを確認します。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-158">Examine the newly generated *Views\Home\Index* file.</span></span> <span data-ttu-id="a3e6a-159">**[新規作成]** 、 **[編集]** 、 **[詳細]** 、および **[削除]** の各リンクは機能しませんが、ページの残りの部分は機能します。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-159">The **Create New**, **Edit**, **Details**, and **Delete** links don't work, but the rest of the page is functional.</span></span> <span data-ttu-id="a3e6a-160">ページを実行します。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-160">Run the page.</span></span> <span data-ttu-id="a3e6a-161">ユーザーの一覧が表示できます。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-161">You see a list of users.</span></span>

![インデックスページ](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image9.png)

<span data-ttu-id="a3e6a-163">次のコードを使用して、*インデックスの cshtml*ファイルを開き、 **Edit**、 **Details**、 **Delete**のマークアップ `ActionLink` を置き換えます。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-163">Open the *Index.cshtml* file and replace the `ActionLink` markup for **Edit**, **Details**, and **Delete** with the following code:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample7.cshtml)]

<span data-ttu-id="a3e6a-164">ユーザー名は、 **[編集]** 、 **[詳細]** 、および **[削除]** リンクで選択したレコードを検索するための ID として使用されます。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-164">The user name is used as the ID to find the selected record in the **Edit**, **Details**, and **Delete** links.</span></span>

## <a name="creating-the-details-view"></a><span data-ttu-id="a3e6a-165">詳細ビューの作成</span><span class="sxs-lookup"><span data-stu-id="a3e6a-165">Creating the Details View</span></span>

<span data-ttu-id="a3e6a-166">次の手順では、ユーザーの詳細を表示するために `Details` アクションメソッドとビューを追加します。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-166">The next step is to add a `Details` action method and view in order to display user details.</span></span>

![詳細](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image10.png)

<span data-ttu-id="a3e6a-168">次の `Details` メソッドを home コントローラーに追加します。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-168">Add the following `Details` method to the home controller:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample8.cs)]

<span data-ttu-id="a3e6a-169">`Details` メソッド内を右クリックし、[<strong>ビューの追加</strong>] を選択します。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-169">Right-click inside the `Details` method and then select <strong>Add View</strong>.</span></span> <span data-ttu-id="a3e6a-170">[<strong>データクラスの表示</strong>] ボックスに<strong>Mvc3Razor</strong>が含まれていることを確認し<em>ます。</em></span><span class="sxs-lookup"><span data-stu-id="a3e6a-170">Verify that the <strong>View data class</strong> box contains <strong>Mvc3Razor.Models.UserModel</strong><em>.</em></span></span> <span data-ttu-id="a3e6a-171">[<strong>表示コンテンツ</strong>] を [<strong>詳細</strong>] に設定し、[<strong>追加</strong>] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-171">Set <strong>View content</strong> to <strong>Details</strong> and then click <strong>Add</strong>.</span></span>

![詳細ビューの追加](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image11.png)

<span data-ttu-id="a3e6a-173">アプリケーションを実行し、[詳細] リンクを選択します。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-173">Run the application and select a details link.</span></span> <span data-ttu-id="a3e6a-174">自動スキャフォールディングは、モデル内の各プロパティを表示します。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-174">The automatic scaffolding shows each property in the model.</span></span>

![詳細](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image12.png)

## <a name="creating-the-edit-view"></a><span data-ttu-id="a3e6a-176">編集ビューを作成する</span><span class="sxs-lookup"><span data-stu-id="a3e6a-176">Creating the Edit View</span></span>

<span data-ttu-id="a3e6a-177">次の `Edit` メソッドを home コントローラーに追加します。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-177">Add the following `Edit` method to the home controller.</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample9.cs)]

<span data-ttu-id="a3e6a-178">前の手順と同様にビューを追加しますが、**ビューの内容**を**編集**するように設定します。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-178">Add a view as in the previous steps, but set **View content** to **Edit**.</span></span>

![編集ビューの追加](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image13.png)

<span data-ttu-id="a3e6a-180">アプリケーションを実行し、1人のユーザーの姓と名を編集します。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-180">Run the application and edit the first and last name of one of the users.</span></span> <span data-ttu-id="a3e6a-181">`UserModel` クラスに適用されている `DataAnnotation` 制約に違反した場合は、フォームを送信すると、サーバーコードによって生成された検証エラーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-181">If you violate any `DataAnnotation` constraints that have been applied to the `UserModel` class, when you submit the form, you will see validation errors that are produced by server code.</span></span> <span data-ttu-id="a3e6a-182">たとえば、名 &quot;"彩&quot;" を&quot;&quot;に変更すると、フォームの送信時にフォームに次のエラーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-182">For example, if you change the first name &quot;Ann&quot; to &quot;A&quot;, when you submit the form, the following error is displayed on the form:</span></span>

`The field First Name must be a string with a minimum length of 3 and a maximum length of 8.`

<span data-ttu-id="a3e6a-183">このチュートリアルでは、ユーザー名を主キーとして扱います。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-183">In this tutorial, you're treating the user name as the primary key.</span></span> <span data-ttu-id="a3e6a-184">そのため、ユーザー名プロパティは変更できません。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-184">Therefore, the user name property cannot be changed.</span></span> <span data-ttu-id="a3e6a-185">`Html.BeginForm` ステートメントの直後にある*Edit. cshtml*ファイルで、ユーザー名を隠しフィールドに設定します。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-185">In the *Edit.cshtml* file, just after the `Html.BeginForm` statement, set the user name to be a hidden field.</span></span> <span data-ttu-id="a3e6a-186">これにより、プロパティがモデルで渡されます。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-186">This causes the property to be passed in the model.</span></span> <span data-ttu-id="a3e6a-187">次のコードフラグメントは、`Hidden` ステートメントの配置を示しています。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-187">The following code fragment shows the placement of the `Hidden` statement:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample10.cshtml)]

<span data-ttu-id="a3e6a-188">ユーザー名の `TextBoxFor` および `ValidationMessageFor` マークアップを `DisplayFor` 呼び出しに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-188">Replace the `TextBoxFor` and `ValidationMessageFor` markup for the user name with a `DisplayFor` call.</span></span> <span data-ttu-id="a3e6a-189">`DisplayFor` メソッドは、プロパティを読み取り専用の要素として表示します。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-189">The `DisplayFor` method displays the property as a read-only element.</span></span> <span data-ttu-id="a3e6a-190">完全なマークアップの例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-190">The following example shows the completed markup.</span></span> <span data-ttu-id="a3e6a-191">元の `TextBoxFor` と `ValidationMessageFor` の呼び出しは、Razor の開始コメントと終了コメント文字 (`@* *@`) でコメントアウトされます。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-191">The original `TextBoxFor` and `ValidationMessageFor` calls are commented out with the Razor begin-comment and end-comment characters (`@* *@`)</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample11.cshtml)]

## <a name="enabling-client-side-validation"></a><span data-ttu-id="a3e6a-192">クライアント側の検証を有効にする</span><span class="sxs-lookup"><span data-stu-id="a3e6a-192">Enabling Client-Side Validation</span></span>

<span data-ttu-id="a3e6a-193">ASP.NET MVC 3 でクライアント側の検証を有効にするには、2つのフラグを設定し、3つの JavaScript ファイルを含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-193">To enable client-side validation in ASP.NET MVC 3, you must set two flags and you must include three JavaScript files.</span></span>

<span data-ttu-id="a3e6a-194">アプリケーションの*web.config*ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-194">Open the application's *Web.config* file.</span></span> <span data-ttu-id="a3e6a-195">アプリケーション設定で `that ClientValidationEnabled` および `UnobtrusiveJavaScriptEnabled` が true に設定されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-195">Verify `that ClientValidationEnabled` and `UnobtrusiveJavaScriptEnabled` are set to true in the application settings.</span></span> <span data-ttu-id="a3e6a-196">ルートの web.config ファイルの次のフラグメントは、正しい設定を示して*い*ます。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-196">The following fragment from the root *Web.config* file shows the correct settings:</span></span>

[!code-xml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample12.xml)]

<span data-ttu-id="a3e6a-197">`UnobtrusiveJavaScriptEnabled` を true に設定すると、控えめな Ajax と控えめなクライアント検証が有効になります。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-197">Setting `UnobtrusiveJavaScriptEnabled` to true enables unobtrusive Ajax and unobtrusive client validation.</span></span> <span data-ttu-id="a3e6a-198">控えめな検証を使用すると、検証規則が HTML5 属性に変換されます。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-198">When you use unobtrusive validation, the validation rules are turned into HTML5 attributes.</span></span> <span data-ttu-id="a3e6a-199">HTML5 属性名は、小文字、数字、およびダッシュのみで構成されています。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-199">HTML5 attribute names can consist of only lowercase letters, numbers, and dashes.</span></span>

<span data-ttu-id="a3e6a-200">`ClientValidationEnabled` を true に設定すると、クライアント側の検証が有効になります。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-200">Setting `ClientValidationEnabled` to true enables client-side validation.</span></span> <span data-ttu-id="a3e6a-201">アプリケーションの*web.config*ファイルでこれらのキーを設定すると、アプリケーション全体に対してクライアント検証と控えめな JavaScript が有効になります。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-201">By setting these keys in the application *Web.config* file, you enable client validation and unobtrusive JavaScript for the entire application.</span></span> <span data-ttu-id="a3e6a-202">また、次のコードを使用して、個々のビューまたはコントローラーのメソッドでこれらの設定を有効または無効にすることもできます。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-202">You can also enable or disable these settings in individual views or in controller methods using the following code:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample13.cs)]

<span data-ttu-id="a3e6a-203">また、レンダリングされたビューに複数の JavaScript ファイルを含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-203">You also need to include several JavaScript files in the rendered view.</span></span> <span data-ttu-id="a3e6a-204">JavaScript をすべてのビューに含める簡単な方法として、 *Views\Shared\\_Layout*ファイルに追加することができます。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-204">An easy way to include the JavaScript in all views is to add them to the *Views\Shared\\_Layout.cshtml* file.</span></span> <span data-ttu-id="a3e6a-205">*\_Layout*ファイルの `<head>` 要素を次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-205">Replace the `<head>` element of the *\_Layout.cshtml* file with the following code:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample14.cshtml)]

<span data-ttu-id="a3e6a-206">最初の2つの jQuery スクリプトは、Microsoft Ajax Content Delivery Network (CDN) によってホストされます。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-206">The first two jQuery scripts are hosted by the Microsoft Ajax Content Delivery Network (CDN).</span></span> <span data-ttu-id="a3e6a-207">Microsoft Ajax CDN を利用することにより、アプリケーションの最初のヒットパフォーマンスを大幅に向上させることができます。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-207">By taking advantage of the Microsoft Ajax CDN, you can significantly improve the first-hit performance of your applications.</span></span>

<span data-ttu-id="a3e6a-208">アプリケーションを実行し、[編集] リンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-208">Run the application and click an edit link.</span></span> <span data-ttu-id="a3e6a-209">ブラウザーでページのソースを表示します。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-209">View the page's source in the browser.</span></span> <span data-ttu-id="a3e6a-210">ブラウザーソースには、(データ検証の) `data-val` フォームの多くの属性が表示されます。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-210">The browser source shows many attributes of the form `data-val` (for data validation).</span></span> <span data-ttu-id="a3e6a-211">クライアント検証と控えめな JavaScript が有効になっている場合、クライアント検証規則を持つ入力フィールドには、控えめなクライアント検証をトリガーするための `data-val="true"` 属性が含まれています。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-211">When client validation and unobtrusive JavaScript is enabled, input fields with a client-validation rule contain the `data-val="true"` attribute to trigger unobtrusive client validation.</span></span> <span data-ttu-id="a3e6a-212">たとえば、モデルの `City` フィールドが[Required](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx)属性で修飾された場合、次の例に示すように HTML が生成されます。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-212">For example, the `City` field in the model was decorated with the [Required](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) attribute, which results in the HTML shown in the following example:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample15.cshtml)]

<span data-ttu-id="a3e6a-213">各クライアント検証規則に対して、`data-val-rulename="message"`という形式の属性が追加されます。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-213">For each client-validation rule, an attribute is added that has the form `data-val-rulename="message"`.</span></span> <span data-ttu-id="a3e6a-214">前に示した `City` フィールドの例を使用すると、必要なクライアント検証規則によって `data-val-required` 属性が生成され、City フィールド &quot;メッセージが&quot;必要になります。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-214">Using the `City` field example shown earlier, the required client-validation rule generates the `data-val-required` attribute and the message &quot;The City field is required&quot;.</span></span> <span data-ttu-id="a3e6a-215">アプリケーションを実行し、いずれかのユーザーを編集して、[`City`] フィールドをオフにします。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-215">Run the application, edit one of the users, and clear the `City` field.</span></span> <span data-ttu-id="a3e6a-216">フィールドからタブを除外すると、クライアント側の検証エラーメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-216">When you tab out of the field, you see a client-side validation error message.</span></span>

![市区町村が必要です](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image14.png)

<span data-ttu-id="a3e6a-218">同様に、クライアント検証規則の各パラメーターには、`data-val-rulename-paramname=paramvalue`という形式の属性が追加されます。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-218">Similarly, for each parameter in the client-validation rule, an attribute is added that has the form `data-val-rulename-paramname=paramvalue`.</span></span> <span data-ttu-id="a3e6a-219">たとえば、`FirstName` プロパティは[Stringlength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx)属性で注釈が付けられ、最小長は3、最大長は8です。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-219">For example, the `FirstName` property is annotated with the [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) attribute and specifies a minimum length of 3 and a maximum length of 8.</span></span> <span data-ttu-id="a3e6a-220">`length` という名前のデータ検証規則では、パラメーター名 `max` とパラメーター値8が指定されています。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-220">The data validation rule named `length` has the parameter name `max` and the parameter value 8.</span></span> <span data-ttu-id="a3e6a-221">次に、いずれかのユーザーを編集するときに `FirstName` フィールドに対して生成される HTML を示します。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-221">The following shows the HTML that is generated for the `FirstName` field when you edit one of the users:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample16.cshtml)]

<span data-ttu-id="a3e6a-222">控えめなクライアント検証の詳細については、Brad Wilson のブログの「 [ASP.NET MVC 3 の控えめなクライアント検証](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-222">For more information about unobtrusive client validation, see the entry [Unobtrusive Client Validation in ASP.NET MVC 3](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html) in Brad Wilson's blog.</span></span>

> [!NOTE]
> <span data-ttu-id="a3e6a-223">ASP.NET MVC 3 Beta では、クライアント側の検証を開始するためにフォームを送信することが必要になる場合があります。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-223">In ASP.NET MVC 3 Beta, you sometimes need to submit the form in order to start client-side validation.</span></span> <span data-ttu-id="a3e6a-224">これは、最終リリースで変更される可能性があります。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-224">This might be changed for the final release.</span></span>

## <a name="creating-the-create-view"></a><span data-ttu-id="a3e6a-225">作成ビューの作成</span><span class="sxs-lookup"><span data-stu-id="a3e6a-225">Creating the Create View</span></span>

<span data-ttu-id="a3e6a-226">次の手順では、ユーザーが新しいユーザーを作成できるようにするために `Create` アクションメソッドとビューを追加します。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-226">The next step is to add a `Create` action method and view in order to enable the user to create a new user.</span></span> <span data-ttu-id="a3e6a-227">次の `Create` メソッドを home コントローラーに追加します。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-227">Add the following `Create` method to the home controller:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample17.cs)]

<span data-ttu-id="a3e6a-228">前の手順と同様にビューを追加しますが、[**作成**する**ビューコンテンツ**] を設定します。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-228">Add a view as in the previous steps, but set **View content** to **Create**.</span></span>

![CREATE VIEW](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image15.png)

<span data-ttu-id="a3e6a-230">アプリケーションを実行し、 **[作成]** リンクを選択して、新しいユーザーを追加します。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-230">Run the application, select the **Create** link, and add a new user.</span></span> <span data-ttu-id="a3e6a-231">`Create` メソッドでは、クライアント側とサーバー側の検証を自動的に利用します。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-231">The `Create` method automatically takes advantage of client-side and server-side validation.</span></span> <span data-ttu-id="a3e6a-232">&quot;Ben X&quot;などの空白を含むユーザー名を入力してください。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-232">Try to enter a user name that contains white space, such as &quot;Ben X&quot;.</span></span> <span data-ttu-id="a3e6a-233">[ユーザー名] フィールドから tab キーを使用すると、クライアント側の検証エラー (`White space is not allowed`) が表示されます。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-233">When you tab out of the user name field, a client-side validation error (`White space is not allowed`) is displayed.</span></span>

## <a name="add-the-delete-method"></a><span data-ttu-id="a3e6a-234">Delete メソッドを追加する</span><span class="sxs-lookup"><span data-stu-id="a3e6a-234">Add the Delete method</span></span>

<span data-ttu-id="a3e6a-235">このチュートリアルを完了するには、次の `Delete` メソッドを home コントローラーに追加します。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-235">To complete the tutorial, add the following `Delete` method to the home controller:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample18.cs)]

<span data-ttu-id="a3e6a-236">前の手順のように `Delete` ビューを追加して、[**ビューコンテンツ**を**削除**する] に設定します。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-236">Add a `Delete` view as in the previous steps, setting **View content** to **Delete**.</span></span>

![ビューの削除](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image16.png)

<span data-ttu-id="a3e6a-238">これで、完全に機能する単純な ASP.NET MVC 3 アプリケーションが検証されました。</span><span class="sxs-lookup"><span data-stu-id="a3e6a-238">You now have a simple but fully functional ASP.NET MVC 3 application with validation.</span></span>
