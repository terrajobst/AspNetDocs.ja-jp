---
uid: web-api/overview/mobile-clients/calling-web-api-from-a-windows-phone-8-application
title: Windows Phone 8 アプリケーションから Web API を呼び出す (C#)-ASP.NET 4.x
author: rmcmurray
description: 'コードを使用したチュートリアル: Windows Phone 8 アプリケーションに書籍のカタログを提供する、ASP.NET 4.x の ASP.NET Web API アプリケーションを作成します。'
ms.author: riande
ms.date: 10/09/2013
ms.custom: seoapril2019
ms.assetid: b9775f41-352a-4f82-baa6-23e95b342e20
msc.legacyurl: /web-api/overview/mobile-clients/calling-web-api-from-a-windows-phone-8-application
msc.type: authoredcontent
ms.openlocfilehash: c5da14a6856f551343b6fb14f0aedc659e792f6b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78498214"
---
# <a name="calling-web-api-from-a-windows-phone-8-application-c"></a><span data-ttu-id="672a7-103">Windows Phone 8 アプリケーションから Web API を呼び出す (C#)</span><span class="sxs-lookup"><span data-stu-id="672a7-103">Calling Web API from a Windows Phone 8 Application (C#)</span></span>

<span data-ttu-id="672a7-104">[Robert McMurray](https://github.com/rmcmurray)</span><span class="sxs-lookup"><span data-stu-id="672a7-104">by [Robert McMurray](https://github.com/rmcmurray)</span></span>

<span data-ttu-id="672a7-105">このチュートリアルでは、Windows Phone 8 アプリケーションに書籍のカタログを提供する ASP.NET Web API アプリケーションで構成される完全なエンドツーエンドのシナリオを作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="672a7-105">In this tutorial, you will learn how to create a complete end-to-end scenario consisting of an ASP.NET Web API application that provides a catalog of books to a Windows Phone 8 application.</span></span>

### <a name="overview"></a><span data-ttu-id="672a7-106">概要</span><span class="sxs-lookup"><span data-stu-id="672a7-106">Overview</span></span>

<span data-ttu-id="672a7-107">ASP.NET Web API のような RESTful サービスは、サーバー側とクライアント側のアプリケーションのアーキテクチャを抽象化することによって、開発者のための HTTP ベースのアプリケーションの作成を簡略化します。</span><span class="sxs-lookup"><span data-stu-id="672a7-107">RESTful services like ASP.NET Web API simplify the creation of HTTP-based applications for developers by abstracting the architecture for server-side and client-side applications.</span></span> <span data-ttu-id="672a7-108">Web API 開発者は、通信用に専用のソケットベースのプロトコルを作成するのではなく、必要な HTTP メソッド (GET、POST、PUT、DELETE など) をアプリケーションに対して発行するだけで済みます。また、クライアントアプリケーションの開発者は、アプリケーションに必要な HTTP メソッド。</span><span class="sxs-lookup"><span data-stu-id="672a7-108">Instead of creating a proprietary socket-based protocol for communication, Web API developers simply need to publish the requisite HTTP methods for their application, (for example: GET, POST, PUT, DELETE), and client application developers only need to consume the HTTP methods that are necessary for their application.</span></span>

<span data-ttu-id="672a7-109">このエンドツーエンドのチュートリアルでは、Web API を使用して次のプロジェクトを作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="672a7-109">In this end-to-end tutorial, you will learn how to use Web API to create the following projects:</span></span>

- <span data-ttu-id="672a7-110">[このチュートリアルの最初の部分](#STEP1)では、すべての作成、読み取り、更新、および削除 (CRUD) 操作をサポートし、書籍カタログを管理する ASP.NET Web API アプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="672a7-110">In the [first part of this tutorial](#STEP1), you will create an ASP.NET Web API application that supports all of the Create, Read, Update, and Delete (CRUD) operations to manage a book catalog.</span></span> <span data-ttu-id="672a7-111">このアプリケーションでは、MSDN の[サンプル Xml ファイル (books.xml)](https://msdn.microsoft.com/library/windows/desktop/ms762271.aspx)を使用します。</span><span class="sxs-lookup"><span data-stu-id="672a7-111">This application will use the [Sample XML File (books.xml)](https://msdn.microsoft.com/library/windows/desktop/ms762271.aspx) from MSDN.</span></span>
- <span data-ttu-id="672a7-112">[このチュートリアルの2番目のパート](#STEP2)では、Web API アプリケーションからデータを取得する対話型 Windows Phone 8 アプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="672a7-112">In the [second part of this tutorial](#STEP2), you will create an interactive Windows Phone 8 application that retrieves the data from your Web API application.</span></span>

#### <a name="prerequisites"></a><span data-ttu-id="672a7-113">前提条件</span><span class="sxs-lookup"><span data-stu-id="672a7-113">Prerequisites</span></span>

- <span data-ttu-id="672a7-114">Windows Phone 8 SDK がインストールされている Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="672a7-114">Visual Studio 2013 with the Windows Phone 8 SDK installed</span></span>
- <span data-ttu-id="672a7-115">Windows 8 以降 (Hyper-v がインストールされている64ビットシステムの場合)</span><span class="sxs-lookup"><span data-stu-id="672a7-115">Windows 8 or later on a 64-bit system with Hyper-V installed</span></span>
- <span data-ttu-id="672a7-116">その他の要件の一覧については、 [WINDOWS PHONE SDK 8.0](https://www.microsoft.com/download/details.aspx?id=35471)ダウンロードページの「*システム要件*」セクションを参照してください。</span><span class="sxs-lookup"><span data-stu-id="672a7-116">For a list of additional requirements, see the *System Requirements* section on the [Windows Phone SDK 8.0](https://www.microsoft.com/download/details.aspx?id=35471) download page.</span></span>

> [!NOTE]
> <span data-ttu-id="672a7-117">ローカルシステム上の Web API と Windows Phone 8 プロジェクト間の接続をテストする場合は、「 *[Windows Phone 8 エミュレーターをローカルコンピューターの WEB Api アプリケーションに接続](https://go.microsoft.com/fwlink/?LinkId=324014)* する」の手順に従って、テスト環境を設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="672a7-117">If you are going to test the connectivity between Web API and Windows Phone 8 projects on your local system, you will need to follow the instructions in the *[Connecting the Windows Phone 8 Emulator to Web API Applications on a Local Computer](https://go.microsoft.com/fwlink/?LinkId=324014)* article to set up your testing environment.</span></span>

<a id="STEP1"></a>
### <a name="step-1-creating-the-web-api-bookstore-project"></a><span data-ttu-id="672a7-118">手順 1: Web API 書店プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="672a7-118">Step 1: Creating the Web API Bookstore Project</span></span>

<span data-ttu-id="672a7-119">このエンドツーエンドチュートリアルの最初の手順では、すべての CRUD 操作をサポートする Web API プロジェクトを作成します。このチュートリアルの[手順 2](#STEP2)では、このソリューションに Windows Phone アプリケーションプロジェクトを追加することに注意してください。</span><span class="sxs-lookup"><span data-stu-id="672a7-119">The first step of this end-to-end tutorial is to create a Web API project that supports all of the CRUD operations; note that you will add the Windows Phone application project to this solution in [Step 2](#STEP2) of this tutorial.</span></span>

1. <span data-ttu-id="672a7-120">**Visual Studio 2013**を開きます。</span><span class="sxs-lookup"><span data-stu-id="672a7-120">Open **Visual Studio 2013**.</span></span>
2. <span data-ttu-id="672a7-121">**[ファイル]** 、 **[新規作成]** 、 **[プロジェクト]** の順にクリックします。</span><span class="sxs-lookup"><span data-stu-id="672a7-121">Click **File**, then **New**, and then **Project**.</span></span>
3. <span data-ttu-id="672a7-122">**[新しいプロジェクト]** ダイアログボックスが表示されたら、 **[インストール済み]** 、 **[テンプレート]** 、 **[ C#ビジュアル]** 、 **[Web]** の順に展開します。</span><span class="sxs-lookup"><span data-stu-id="672a7-122">When the **New Project** dialog box is displayed, expand **Installed**, then **Templates**, then **Visual C#**, and then **Web**.</span></span>

   | [![](calling-web-api-from-a-windows-phone-8-application/_static/image2.png)](calling-web-api-from-a-windows-phone-8-application/_static/image1.png) |
   |-----------------------------------------------------------------------------------------------------------------------------------------------------|
   |                                                                <span data-ttu-id="672a7-123">[イメージ] をクリックして展開します。</span><span class="sxs-lookup"><span data-stu-id="672a7-123">Click image to expand</span></span>                                                                |

4. <span data-ttu-id="672a7-124">**ASP.NET Web アプリケーション**を強調表示し、プロジェクト名として「**書店**」と入力して、[ **OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="672a7-124">Highlight **ASP.NET Web Application**, enter **BookStore** for the project name, and then click **OK**.</span></span>
5. <span data-ttu-id="672a7-125">**[新しい ASP.NET プロジェクト]** ダイアログボックスが表示されたら、 **Web API**テンプレートを選択し、 **[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="672a7-125">When the **New ASP.NET Project** dialog box is displayed, select the **Web API** template, and then click **OK**.</span></span>

   | [![](calling-web-api-from-a-windows-phone-8-application/_static/image4.png)](calling-web-api-from-a-windows-phone-8-application/_static/image3.png) |
   |-----------------------------------------------------------------------------------------------------------------------------------------------------|
   |                                                                <span data-ttu-id="672a7-126">[イメージ] をクリックして展開します。</span><span class="sxs-lookup"><span data-stu-id="672a7-126">Click image to expand</span></span>                                                                |

6. <span data-ttu-id="672a7-127">Web API プロジェクトが開いたら、プロジェクトからサンプルコントローラーを削除します。</span><span class="sxs-lookup"><span data-stu-id="672a7-127">When the Web API project opens, remove the sample controller from the project:</span></span>

    1. <span data-ttu-id="672a7-128">ソリューションエクスプローラーで**Controllers**フォルダーを展開します。</span><span class="sxs-lookup"><span data-stu-id="672a7-128">Expand the **Controllers** folder in the solution explorer.</span></span>
    2. <span data-ttu-id="672a7-129">**ValuesController.cs**ファイルを右クリックし、 **[削除]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="672a7-129">Right-click the **ValuesController.cs** file, and then click **Delete**.</span></span>
    3. <span data-ttu-id="672a7-130">削除の確認を求めるメッセージが表示されたら、[ **OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="672a7-130">Click **OK** when prompted to confirm the deletion.</span></span>
7. <span data-ttu-id="672a7-131">XML データファイルを Web API プロジェクトに追加します。このファイルには、書店カタログの内容が含まれています。</span><span class="sxs-lookup"><span data-stu-id="672a7-131">Add an XML data file to the Web API project; this file contains the contents of the bookstore catalog:</span></span>

   1. <span data-ttu-id="672a7-132">ソリューションエクスプローラーで [ **App\_Data** ] フォルダーを右クリックし、 **[追加]** をクリックして、 **[新しい項目]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="672a7-132">Right-click the **App\_Data** folder in the solution explorer, then click **Add**, and then click **New Item**.</span></span>
   2. <span data-ttu-id="672a7-133">**[新しい項目の追加]** ダイアログボックスが表示されたら、 **XML ファイル**テンプレートを強調表示します。</span><span class="sxs-lookup"><span data-stu-id="672a7-133">When the **Add New Item** dialog box is displayed, highlight the **XML File** template.</span></span>
   3. <span data-ttu-id="672a7-134">ファイルに「 **books.xml**」という名前を指定し、 **[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="672a7-134">Name the file **Books.xml**, and then click **Add**.</span></span>
   4. <span data-ttu-id="672a7-135">**Books.xml**ファイルを開いたら、ファイル内のコードを、MSDN のサンプルの**BOOKS.XML**ファイルの xml に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="672a7-135">When the **Books.xml** file is opened, replace the code in the file with the XML from the sample **books.xml** file on MSDN:</span></span> 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample1.xml)]
   5. <span data-ttu-id="672a7-136">XML ファイルを保存して閉じます。</span><span class="sxs-lookup"><span data-stu-id="672a7-136">Save and close the XML file.</span></span>

8. <span data-ttu-id="672a7-137">Web API プロジェクトに書店モデルを追加します。このモデルには、書店アプリケーションの作成、読み取り、更新、および削除 (CRUD) のロジックが含まれています。</span><span class="sxs-lookup"><span data-stu-id="672a7-137">Add the bookstore model to the Web API project; this model contains the Create, Read, Update, and Delete (CRUD) logic for the bookstore application:</span></span>

   1. <span data-ttu-id="672a7-138">ソリューションエクスプローラーで **[モデル]** フォルダーを右クリックし、 **[追加]** をクリックして、 **[クラス]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="672a7-138">Right-click the **Models** folder in the solution explorer, then click **Add**, and then click **Class**.</span></span>
   2. <span data-ttu-id="672a7-139">**[新しい項目の追加]** ダイアログボックスが表示されたら、クラスファイルに**BookDetails.cs**という名前を指定し、 **[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="672a7-139">When the **Add New Item** dialog box is displayed, name the class file **BookDetails.cs**, and then click **Add**.</span></span>
   3. <span data-ttu-id="672a7-140">**BookDetails.cs**ファイルを開いたら、ファイル内のコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="672a7-140">When the **BookDetails.cs** file is opened, replace the code in the file with the following:</span></span> 

       [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample2.cs)]
   4. <span data-ttu-id="672a7-141">**BookDetails.cs**ファイルを保存して閉じます。</span><span class="sxs-lookup"><span data-stu-id="672a7-141">Save and close the **BookDetails.cs** file.</span></span>

9. <span data-ttu-id="672a7-142">Web API プロジェクトに書店コントローラーを追加します。</span><span class="sxs-lookup"><span data-stu-id="672a7-142">Add the bookstore controller to the Web API project:</span></span>

   1. <span data-ttu-id="672a7-143">ソリューションエクスプローラーで**Controllers**フォルダーを右クリックし、 **[追加]** をクリックして、 **[コントローラー]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="672a7-143">Right-click the **Controllers** folder in the solution explorer, then click **Add**, and then click **Controller**.</span></span>
   2. <span data-ttu-id="672a7-144">**[スキャフォールディングの追加]** ダイアログボックスが表示されたら、 **[Web API 2 コントローラー-空]** を強調表示し、 **[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="672a7-144">When the **Add Scaffold** dialog box is displayed, highlight **Web API 2 Controller - Empty**, and then click **Add**.</span></span>
   3. <span data-ttu-id="672a7-145">**[コントローラーの追加]** ダイアログボックスが表示されたら、コントローラーに「 **bookscontroller**」という名前を指定し、 **[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="672a7-145">When the **Add Controller** dialog box is displayed, name the controller **BooksController**, and then click **Add**.</span></span>
   4. <span data-ttu-id="672a7-146">**BooksController.cs**ファイルを開いたら、ファイル内のコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="672a7-146">When the **BooksController.cs** file is opened, replace the code in the file with the following:</span></span> 

       [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample3.cs)]
   5. <span data-ttu-id="672a7-147">**BooksController.cs**ファイルを保存して閉じます。</span><span class="sxs-lookup"><span data-stu-id="672a7-147">Save and close the **BooksController.cs** file.</span></span>

10. <span data-ttu-id="672a7-148">Web API アプリケーションをビルドして、エラーがないかどうかを確認します。</span><span class="sxs-lookup"><span data-stu-id="672a7-148">Build the Web API application to check for errors.</span></span>

<a id="STEP2"></a>
### <a name="step-2-adding-the-windows-phone-8-bookstore-catalog-project"></a><span data-ttu-id="672a7-149">手順 2: Windows Phone 8 書店カタログプロジェクトの追加</span><span class="sxs-lookup"><span data-stu-id="672a7-149">Step 2: Adding the Windows Phone 8 Bookstore Catalog Project</span></span>

<span data-ttu-id="672a7-150">このエンドツーエンドのシナリオの次の手順では、Windows Phone 8 のカタログアプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="672a7-150">The next step of this end-to-end scenario is to create the catalog application for Windows Phone 8.</span></span> <span data-ttu-id="672a7-151">このアプリケーションでは、既定のユーザーインターフェイスに*Windows Phone データバインドアプリ*テンプレートを使用します。このテンプレートは、このチュートリアルの[手順 1](#STEP1)で作成した Web API アプリケーションをデータソースとして使用します。</span><span class="sxs-lookup"><span data-stu-id="672a7-151">This application will use the *Windows Phone Databound App* template for the default user interface, and it will use the Web API application that you created in [Step 1](#STEP1) of this tutorial as the data source.</span></span>

1. <span data-ttu-id="672a7-152">ソリューションエクスプローラーで、の**書店**ソリューションを右クリックし、 **[追加]** 、 **[新しいプロジェクト]** の順にクリックします。</span><span class="sxs-lookup"><span data-stu-id="672a7-152">Right-click the **BookStore** solution in the in the solution explorer, then click **Add**, and then **New Project**.</span></span>
2. <span data-ttu-id="672a7-153">**新しいプロジェクト** ダイアログボックスが表示されたら、**インストール済み**、 **C#ビジュアル** の順に展開し、 **Windows Phone** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="672a7-153">When the **New Project** dialog box is displayed, expand **Installed**, then **Visual C#**, and then **Windows Phone**.</span></span>
3. <span data-ttu-id="672a7-154">**データバインドアプリ Windows Phone**強調表示し、名前として「 **bookcatalog** 」と入力して、 **OK**をクリックします。</span><span class="sxs-lookup"><span data-stu-id="672a7-154">Highlight **Windows Phone Databound App**, enter **BookCatalog** for the name, and then click **OK**.</span></span>
4. <span data-ttu-id="672a7-155">Json.NET NuGet パッケージを**Bookcatalog**プロジェクトに追加します。</span><span class="sxs-lookup"><span data-stu-id="672a7-155">Add the Json.NET NuGet package to the **BookCatalog** project:</span></span>

    1. <span data-ttu-id="672a7-156">ソリューションエクスプローラーで**Bookcatalog**プロジェクトの **[参照]** を右クリックし、 **[NuGet パッケージの管理]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="672a7-156">Right-click **References** for the **BookCatalog** project in the solution explorer, and then click **Manage NuGet Packages**.</span></span>
    2. <span data-ttu-id="672a7-157">**[NuGet パッケージの管理]** ダイアログボックスが表示されたら、 **[オンライン]** セクションを展開し、 **[nuget.org]** を強調表示します。</span><span class="sxs-lookup"><span data-stu-id="672a7-157">When the **Manage NuGet Packages** dialog box is displayed, expand the **Online** section, and highlight **nuget.org**.</span></span>
    3. <span data-ttu-id="672a7-158">検索フィールドに「 **Json.NET** 」と入力し、[検索] アイコンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="672a7-158">Enter **Json.NET** in the search field and click the search icon.</span></span>
    4. <span data-ttu-id="672a7-159">検索結果で**Json.NET**を強調表示し、 **[インストール]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="672a7-159">Highlight **Json.NET** in the search results, and then click **Install**.</span></span>
    5. <span data-ttu-id="672a7-160">インストールが完了したら、 **[閉じる]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="672a7-160">When the installation has completed, click **Close**.</span></span>
5. <span data-ttu-id="672a7-161">Bookdetails プロジェクトに**Bookdetails**モデルを追加します。これには、書店クラスの汎用モデルが含まれます。</span><span class="sxs-lookup"><span data-stu-id="672a7-161">Add the **BookDetails** model to the **BookCatalog** project; this contains a generic model of the bookstore class:</span></span>

   1. <span data-ttu-id="672a7-162">ソリューションエクスプローラーで**Bookcatalog**プロジェクトを右クリックし、 **[追加]** をクリックして、 **[新しいフォルダー]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="672a7-162">Right-click the **BookCatalog** project in the solution explorer, then click **Add**, and then click **New Folder**.</span></span>
   2. <span data-ttu-id="672a7-163">新しいフォルダーに**モデル**の名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="672a7-163">Name the new folder **Models**.</span></span>
   3. <span data-ttu-id="672a7-164">ソリューションエクスプローラーで **[モデル]** フォルダーを右クリックし、 **[追加]** をクリックして、 **[クラス]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="672a7-164">Right-click the **Models** folder in the solution explorer, then click **Add**, and then click **Class**.</span></span>
   4. <span data-ttu-id="672a7-165">**[新しい項目の追加]** ダイアログボックスが表示されたら、クラスファイルに**BookDetails.cs**という名前を指定し、 **[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="672a7-165">When the **Add New Item** dialog box is displayed, name the class file **BookDetails.cs**, and then click **Add**.</span></span>
   5. <span data-ttu-id="672a7-166">**BookDetails.cs**ファイルを開いたら、ファイル内のコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="672a7-166">When the **BookDetails.cs** file is opened, replace the code in the file with the following:</span></span> 

       [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample4.cs)]
   6. <span data-ttu-id="672a7-167">**BookDetails.cs**ファイルを保存して閉じます。</span><span class="sxs-lookup"><span data-stu-id="672a7-167">Save and close the **BookDetails.cs** file.</span></span>

6. <span data-ttu-id="672a7-168">**MainViewModel.cs**クラスを更新して、書店の Web API アプリケーションと通信する機能を含めます。</span><span class="sxs-lookup"><span data-stu-id="672a7-168">Update the **MainViewModel.cs** class to include the functionality to communicate with the BookStore Web API application:</span></span>

   1. <span data-ttu-id="672a7-169">ソリューションエクスプローラーで**viewmodel**フォルダーを展開し、 **MainViewModel.cs**ファイルをダブルクリックします。</span><span class="sxs-lookup"><span data-stu-id="672a7-169">Expand the **ViewModels** folder in the solution explorer, and then double-click the **MainViewModel.cs** file.</span></span>
   2. <span data-ttu-id="672a7-170">**MainViewModel.cs**ファイルを開いたら、ファイル内のコードを次のコードに置き換えます。`apiUrl` 定数の値は、実際の Web API の URL で更新する必要があることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="672a7-170">When the **MainViewModel.cs** file is opened, replace the code in the file with the following; note that you will need to update the value of the `apiUrl` constant with the actual URL of your Web API:</span></span> 

       [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample5.cs)]
   3. <span data-ttu-id="672a7-171">**MainViewModel.cs**ファイルを保存して閉じます。</span><span class="sxs-lookup"><span data-stu-id="672a7-171">Save and close the **MainViewModel.cs** file.</span></span>

7. <span data-ttu-id="672a7-172">**Mainpage.xaml**ファイルを更新して、アプリケーション名をカスタマイズします。</span><span class="sxs-lookup"><span data-stu-id="672a7-172">Update the **MainPage.xaml** file to customize the application name:</span></span>

   1. <span data-ttu-id="672a7-173">ソリューションエクスプローラーで**mainpage.xaml**ファイルをダブルクリックします。</span><span class="sxs-lookup"><span data-stu-id="672a7-173">Double-click the **MainPage.xaml** file in the solution explorer.</span></span>
   2. <span data-ttu-id="672a7-174">**Mainpage.xaml**ファイルを開いたら、次のコード行を見つけます。</span><span class="sxs-lookup"><span data-stu-id="672a7-174">When the **MainPage.xaml** file is opened, locate the following lines of code:</span></span> 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample6.xml)]
   3. <span data-ttu-id="672a7-175">これらの行を次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="672a7-175">Replace those lines with the following:</span></span> 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample7.xml)]
   4. <span data-ttu-id="672a7-176">**Mainpage.xaml**ファイルを保存して閉じます。</span><span class="sxs-lookup"><span data-stu-id="672a7-176">Save and close the **MainPage.xaml** file.</span></span>

8. <span data-ttu-id="672a7-177">**DetailsPage**ファイルを更新して、表示される項目をカスタマイズします。</span><span class="sxs-lookup"><span data-stu-id="672a7-177">Update the **DetailsPage.xaml** file to customize the displayed items:</span></span>

   1. <span data-ttu-id="672a7-178">ソリューションエクスプローラーで**DetailsPage**ファイルをダブルクリックします。</span><span class="sxs-lookup"><span data-stu-id="672a7-178">Double-click the **DetailsPage.xaml** file in the solution explorer.</span></span>
   2. <span data-ttu-id="672a7-179">**DetailsPage**ファイルを開いたら、次のコード行を見つけます。</span><span class="sxs-lookup"><span data-stu-id="672a7-179">When the **DetailsPage.xaml** file is opened, locate the following lines of code:</span></span> 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample8.xml)]
   3. <span data-ttu-id="672a7-180">これらの行を次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="672a7-180">Replace those lines with the following:</span></span> 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample9.xml)]
   4. <span data-ttu-id="672a7-181">**DetailsPage**ファイルを保存して閉じます。</span><span class="sxs-lookup"><span data-stu-id="672a7-181">Save and close the **DetailsPage.xaml** file.</span></span>

9. <span data-ttu-id="672a7-182">Windows Phone アプリケーションをビルドして、エラーがないかどうかを確認します。</span><span class="sxs-lookup"><span data-stu-id="672a7-182">Build the Windows Phone application to check for errors.</span></span>

### <a name="step-3-testing-the-end-to-end-solution"></a><span data-ttu-id="672a7-183">手順 3: エンドツーエンドのソリューションをテストする</span><span class="sxs-lookup"><span data-stu-id="672a7-183">Step 3: Testing the End-to-End Solution</span></span>

<span data-ttu-id="672a7-184">このチュートリアルの*前提条件*のセクションで説明したように、ローカルシステム上の web api と Windows Phone 8 プロジェクト間の接続をテストするときは、「 *[Windows Phone 8 エミュレーターをローカルコンピューターの web Api アプリケーションに接続](https://go.microsoft.com/fwlink/?LinkId=324014)* する」の手順に従って、テスト環境を設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="672a7-184">As mentioned in the *Prerequisites* section of this tutorial, when you are testing the connectivity between Web API and Windows Phone 8 projects on your local system, you will need to follow the instructions in the *[Connecting the Windows Phone 8 Emulator to Web API Applications on a Local Computer](https://go.microsoft.com/fwlink/?LinkId=324014)* article to set up your testing environment.</span></span>

<span data-ttu-id="672a7-185">テスト環境を構成したら、Windows Phone アプリケーションをスタートアッププロジェクトとして設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="672a7-185">Once you have the testing environment configured, you will need to set the Windows Phone application as the startup project.</span></span> <span data-ttu-id="672a7-186">これを行うには、ソリューションエクスプローラーで**Bookcatalog**アプリケーションを強調表示し、 **[スタートアッププロジェクトに設定]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="672a7-186">To do so, highlight the **BookCatalog** application in the solution explorer, and then click **Set as StartUp Project**:</span></span>

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image6.png)](calling-web-api-from-a-windows-phone-8-application/_static/image5.png) |
| --- |
| <span data-ttu-id="672a7-187">[イメージ] をクリックして展開します。</span><span class="sxs-lookup"><span data-stu-id="672a7-187">Click image to expand</span></span> |

<span data-ttu-id="672a7-188">F5 キーを押すと、Visual Studio は Windows Phone エミュレーターの両方を起動します。これにより、Web API からアプリケーションデータが取得されている間、&quot; メッセージ &quot;を表示します。</span><span class="sxs-lookup"><span data-stu-id="672a7-188">When you press F5, Visual Studio will start both the Windows Phone Emulator, which will display a &quot;Please Wait&quot; message while the application data is retrieved from your Web API:</span></span>

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image8.png)](calling-web-api-from-a-windows-phone-8-application/_static/image7.png) |
| --- |
| <span data-ttu-id="672a7-189">[イメージ] をクリックして展開します。</span><span class="sxs-lookup"><span data-stu-id="672a7-189">Click image to expand</span></span> |

<span data-ttu-id="672a7-190">すべての処理が成功すると、カタログが表示されます。</span><span class="sxs-lookup"><span data-stu-id="672a7-190">If everything is successful, you should see the catalog displayed:</span></span>

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image10.png)](calling-web-api-from-a-windows-phone-8-application/_static/image9.png) |
| --- |
| <span data-ttu-id="672a7-191">[イメージ] をクリックして展開します。</span><span class="sxs-lookup"><span data-stu-id="672a7-191">Click image to expand</span></span> |

<span data-ttu-id="672a7-192">任意の書籍のタイトルをタップすると、アプリケーションにブックの説明が表示されます。</span><span class="sxs-lookup"><span data-stu-id="672a7-192">If you tap on any book title, the application will display the book description:</span></span>

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image12.png)](calling-web-api-from-a-windows-phone-8-application/_static/image11.png) |
| --- |
| <span data-ttu-id="672a7-193">[イメージ] をクリックして展開します。</span><span class="sxs-lookup"><span data-stu-id="672a7-193">Click image to expand</span></span> |

<span data-ttu-id="672a7-194">アプリケーションが Web API と通信できない場合は、次のエラーメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="672a7-194">If the application cannot communicate with your Web API, an error message will be displayed:</span></span>

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image14.png)](calling-web-api-from-a-windows-phone-8-application/_static/image13.png) |
| --- |
| <span data-ttu-id="672a7-195">[イメージ] をクリックして展開します。</span><span class="sxs-lookup"><span data-stu-id="672a7-195">Click image to expand</span></span> |

<span data-ttu-id="672a7-196">エラーメッセージをタップすると、エラーに関する追加情報が表示されます。</span><span class="sxs-lookup"><span data-stu-id="672a7-196">If you tap on the error message, any additional details about the error will be displayed:</span></span>

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image16.png)](calling-web-api-from-a-windows-phone-8-application/_static/image15.png) |
|-------------------------------------------------------------------------------------------------------------------------------------------------------|
|                                                                 <span data-ttu-id="672a7-197">[イメージ] をクリックして展開します。</span><span class="sxs-lookup"><span data-stu-id="672a7-197">Click image to expand</span></span>                                                                 |
