---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage
title: 非構造化 Blob Storage (Azure を使用した実際のクラウドアプリの構築) |Microsoft Docs
author: MikeWasson
description: Azure 電子ブックを使用した実際のクラウドアプリの構築は、Scott Guthrie によって開発されたプレゼンテーションに基づいています。 13のパターンとベストプラクティスについて説明します。
ms.author: riande
ms.date: 03/30/2015
ms.assetid: 9f05ccb1-2004-4661-ad8b-c370e6c09c8e
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage
msc.type: authoredcontent
ms.openlocfilehash: f48b2be755b84dff9b2672bd348c73107602c6dd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78500410"
---
# <a name="unstructured-blob-storage-building-real-world-cloud-apps-with-azure"></a><span data-ttu-id="0704a-104">非構造化 Blob Storage (Azure を使用した実際のクラウドアプリの構築)</span><span class="sxs-lookup"><span data-stu-id="0704a-104">Unstructured Blob Storage (Building Real-World Cloud Apps with Azure)</span></span>

<span data-ttu-id="0704a-105">[Mike Wasson](https://github.com/MikeWasson)、 [Rick Anderson](https://twitter.com/RickAndMSFT)、 [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="0704a-105">by [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson](https://twitter.com/RickAndMSFT), [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="0704a-106">[修正 It プロジェクトをダウンロード](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)するか[、電子書籍をダウンロード](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)します</span><span class="sxs-lookup"><span data-stu-id="0704a-106">[Download Fix It Project](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) or [Download E-book](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)</span></span>

> <span data-ttu-id="0704a-107">Azure 電子ブック**を使用した実際のクラウドアプリの構築**は、Scott Guthrie によって開発されたプレゼンテーションに基づいています。</span><span class="sxs-lookup"><span data-stu-id="0704a-107">The **Building Real World Cloud Apps with Azure** e-book is based on a presentation developed by Scott Guthrie.</span></span> <span data-ttu-id="0704a-108">ここでは、クラウド用の web アプリの開発を成功させるのに役立つ13のパターンとプラクティスについて説明します。</span><span class="sxs-lookup"><span data-stu-id="0704a-108">It explains 13 patterns and practices that can help you be successful developing web apps for the cloud.</span></span> <span data-ttu-id="0704a-109">電子書籍の詳細については、[最初の章](introduction.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="0704a-109">For information about the e-book, see [the first chapter](introduction.md).</span></span>

<span data-ttu-id="0704a-110">前の章では、パーティション構成について説明し、It アプリの修正によって Azure Storage Blob サービスに画像が格納される方法、および Azure SQL Database のその他のタスクデータについて説明しました。</span><span class="sxs-lookup"><span data-stu-id="0704a-110">In the previous chapter we looked at partitioning schemes and explained how the Fix It app stores images in the Azure Storage Blob service, and other task data in Azure SQL Database.</span></span> <span data-ttu-id="0704a-111">この章では、Blob service について詳しく説明し、修正した It プロジェクトコードでの実装方法を示します。</span><span class="sxs-lookup"><span data-stu-id="0704a-111">In this chapter we go deeper into the Blob service and show how it's implemented in Fix It project code.</span></span>

## <a name="what-is-blob-storage"></a><span data-ttu-id="0704a-112">BLOB ストレージとは</span><span class="sxs-lookup"><span data-stu-id="0704a-112">What is Blob storage?</span></span>

<span data-ttu-id="0704a-113">Azure Storage Blob サービスは、クラウドにファイルを格納する方法を提供します。</span><span class="sxs-lookup"><span data-stu-id="0704a-113">The Azure Storage Blob service provides a way to store files in the cloud.</span></span> <span data-ttu-id="0704a-114">Blob service には、ローカルネットワークファイルシステムにファイルを保存するよりも多くの利点があります。</span><span class="sxs-lookup"><span data-stu-id="0704a-114">The Blob service has a number of advantages over storing files in a local network file system:</span></span>

- <span data-ttu-id="0704a-115">拡張性に優れています。</span><span class="sxs-lookup"><span data-stu-id="0704a-115">It's highly scalable.</span></span> <span data-ttu-id="0704a-116">1つのストレージアカウントは、[数百テラバイトの](https://msdn.microsoft.com/library/windowsazure/dn249410.aspx)データを格納でき、複数のストレージアカウントを持つことができます。</span><span class="sxs-lookup"><span data-stu-id="0704a-116">A single Storage account can store [hundreds of terabytes](https://msdn.microsoft.com/library/windowsazure/dn249410.aspx), and you can have multiple Storage accounts.</span></span> <span data-ttu-id="0704a-117">最大の Azure のお客様は、数百のペタバイトを格納しています。</span><span class="sxs-lookup"><span data-stu-id="0704a-117">Some of the biggest Azure customers store hundreds of petabytes.</span></span> <span data-ttu-id="0704a-118">Microsoft SkyDrive は、blob ストレージを使用します。</span><span class="sxs-lookup"><span data-stu-id="0704a-118">Microsoft SkyDrive uses blob storage.</span></span>
- <span data-ttu-id="0704a-119">持続性があります。</span><span class="sxs-lookup"><span data-stu-id="0704a-119">It's durable.</span></span> <span data-ttu-id="0704a-120">Blob service に格納するすべてのファイルが自動的にバックアップされます。</span><span class="sxs-lookup"><span data-stu-id="0704a-120">Every file you store in the Blob service is automatically backed up.</span></span>
- <span data-ttu-id="0704a-121">高可用性が提供されます。</span><span class="sxs-lookup"><span data-stu-id="0704a-121">It provides high availability.</span></span> <span data-ttu-id="0704a-122">[ストレージの SLA](https://go.microsoft.com/fwlink/p/?linkid=159705&amp;clcid=0x409)は、選択した geo 冗長オプションに応じて、99.9% または99.99% の稼働時間を保証します。</span><span class="sxs-lookup"><span data-stu-id="0704a-122">The [SLA for Storage](https://go.microsoft.com/fwlink/p/?linkid=159705&amp;clcid=0x409) promises 99.9% or 99.99% uptime, depending on which geo-redundancy option you choose.</span></span>
- <span data-ttu-id="0704a-123">Azure のサービスとしてのプラットフォーム (PaaS) 機能です。これにより、ファイルを格納して取得するだけで、実際に使用したストレージの量に対してのみ料金が発生します。また、Azure では、処理.</span><span class="sxs-lookup"><span data-stu-id="0704a-123">It's a platform-as-a-service (PaaS) feature of Azure, which means you just store and retrieve files, paying only for the actual amount of storage you use, and Azure automatically takes care of setting up and managing all of the VMs and disk drives required for the service.</span></span>
- <span data-ttu-id="0704a-124">Blob service には、REST API を使用するか、プログラミング言語 API を使用してアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="0704a-124">You can access the Blob service by using a REST API or by using a programming language API.</span></span> <span data-ttu-id="0704a-125">Sdk は、.NET、Java、Ruby などで使用できます。</span><span class="sxs-lookup"><span data-stu-id="0704a-125">SDKs are available for .NET, Java, Ruby, and others.</span></span>
- <span data-ttu-id="0704a-126">Blob service にファイルを保存すると、インターネット経由で簡単に公開できるようになります。</span><span class="sxs-lookup"><span data-stu-id="0704a-126">When you store a file in the Blob service, you can easily make it publicly available over the Internet.</span></span>
- <span data-ttu-id="0704a-127">Blob service のファイルは、承認されたユーザーのみがアクセスできるようにセキュリティで保護することができます。また、限られた期間だけユーザーが使用できるようにする一時的なアクセストークンを提供することもできます。</span><span class="sxs-lookup"><span data-stu-id="0704a-127">You can secure files in the Blob service so they can accessed only by authorized users, or you can provide temporary access tokens that makes them available to someone only for a limited period of time.</span></span>

<span data-ttu-id="0704a-128">Azure 向けアプリを構築しているときに、オンプレミスの環境にある大量のデータを保存する場合は、画像、ビデオ、Pdf、スプレッドシートなどのファイルを使用することをお勧めします。 Blob service を検討してください。</span><span class="sxs-lookup"><span data-stu-id="0704a-128">Anytime you're building an app for Azure and you want to store a lot of data that in an on-premises environment would go in files -- such as images, videos, PDFs, spreadsheets, etc. -- consider the Blob service.</span></span>

## <a name="creating-a-storage-account"></a><span data-ttu-id="0704a-129">ストレージアカウントの作成</span><span class="sxs-lookup"><span data-stu-id="0704a-129">Creating a Storage account</span></span>

<span data-ttu-id="0704a-130">Blob service の使用を開始するには、Azure でストレージアカウントを作成します。</span><span class="sxs-lookup"><span data-stu-id="0704a-130">To get started with the Blob service you create a Storage account in Azure.</span></span> <span data-ttu-id="0704a-131">ポータルで、[**新規** -- ] をクリックして、[**ストレージ** -- **簡易作成**] -- **Data Services** 、URL とデータセンターの場所を入力します。</span><span class="sxs-lookup"><span data-stu-id="0704a-131">In the portal, click **New** -- **Data Services** -- **Storage** -- **Quick Create**, and then enter a URL and a data center location.</span></span> <span data-ttu-id="0704a-132">データセンターの場所は、web アプリと同じである必要があります。</span><span class="sxs-lookup"><span data-stu-id="0704a-132">The data center location should be the same as your web app.</span></span>

![ストレージアカウントの作成](unstructured-blob-storage/_static/image1.png)

<span data-ttu-id="0704a-134">コンテンツを格納するプライマリリージョンを選択します。 [geo レプリケーション](https://blogs.msdn.com/b/windowsazurestorage/archive/2013/12/11/introducing-read-access-geo-replicated-storage-ra-grs-for-windows-azure-storage.aspx#_Geo_Redundant_Storage)オプションを選択した場合、Azure は、国の別のリージョンの別のデータセンターにすべてのデータのレプリカを作成します。</span><span class="sxs-lookup"><span data-stu-id="0704a-134">You pick the primary region where you want to store the content, and if you choose the [geo-replication](https://blogs.msdn.com/b/windowsazurestorage/archive/2013/12/11/introducing-read-access-geo-replicated-storage-ra-grs-for-windows-azure-storage.aspx#_Geo_Redundant_Storage) option, Azure creates replicas of all your data in a different data center in another region of the country.</span></span> <span data-ttu-id="0704a-135">たとえば、米国西部のデータセンターを選択した場合、ファイルを保存すると、米国西部のデータセンターに移動しますが、バックグラウンドでは、他の米国のデータセンターのいずれかにもコピーされます。</span><span class="sxs-lookup"><span data-stu-id="0704a-135">For example, if you choose the Western US data center, when you store a file it goes to the Western US data center, but in the background Azure also copies it to one of the other US data centers.</span></span> <span data-ttu-id="0704a-136">ある国の1つのリージョンで障害が発生した場合でも、データは安全です。</span><span class="sxs-lookup"><span data-stu-id="0704a-136">If a disaster happens in one region of the country, your data is still safe.</span></span>

<span data-ttu-id="0704a-137">Azure は地理的な境界を越えてデータをレプリケートしません。プライマリロケーションが米国内にある場合、ファイルは米国内の別のリージョンにのみレプリケートされます。プライマリの場所がオーストラリアの場合、ファイルはオーストラリアの別のデータセンターにのみレプリケートされます。</span><span class="sxs-lookup"><span data-stu-id="0704a-137">Azure won't replicate data across geo-political boundaries: if your primary location is in the U.S., your files are only replicated to another region within the U.S.; if your primary location is Australia, your files are only replicated to another data center in Australia.</span></span>

<span data-ttu-id="0704a-138">もちろん、先ほど見たように、スクリプトからコマンドを実行してストレージアカウントを作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="0704a-138">Of course, you can also create a Storage account by executing commands from a script, as we saw earlier.</span></span> <span data-ttu-id="0704a-139">ストレージアカウントを作成するための Windows PowerShell コマンドを次に示します。</span><span class="sxs-lookup"><span data-stu-id="0704a-139">Here's a Windows PowerShell command to create a Storage account:</span></span>

[!code-powershell[Main](unstructured-blob-storage/samples/sample1.ps1)]

<span data-ttu-id="0704a-140">ストレージアカウントを作成したら、すぐに Blob service にファイルの格納を開始できます。</span><span class="sxs-lookup"><span data-stu-id="0704a-140">Once you have a Storage account, you can immediately start storing files in the Blob service.</span></span>

## <a name="using-blob-storage-in-the-fix-it-app"></a><span data-ttu-id="0704a-141">It アプリを修正するための Blob storage の使用</span><span class="sxs-lookup"><span data-stu-id="0704a-141">Using Blob storage in the Fix It app</span></span>

<span data-ttu-id="0704a-142">Fix It アプリでは、写真をアップロードできます。</span><span class="sxs-lookup"><span data-stu-id="0704a-142">The Fix It app enables you to upload photos.</span></span>

![修正するタスクを作成する](unstructured-blob-storage/_static/image2.png)

<span data-ttu-id="0704a-144">**[FixIt の作成]** をクリックすると、アプリケーションは指定されたイメージファイルをアップロードし、Blob service に保存します。</span><span class="sxs-lookup"><span data-stu-id="0704a-144">When you click **Create the FixIt**, the application uploads the specified image file and stores it in the Blob service.</span></span>

### <a name="set-up-the-blob-container"></a><span data-ttu-id="0704a-145">Blob コンテナーを設定する</span><span class="sxs-lookup"><span data-stu-id="0704a-145">Set up the Blob container</span></span>

<span data-ttu-id="0704a-146">Blob service にファイルを格納するには、そのファイルを格納する*コンテナー*が必要です。</span><span class="sxs-lookup"><span data-stu-id="0704a-146">In order to store a file in the Blob service you need a *container* to store it in.</span></span> <span data-ttu-id="0704a-147">Blob service コンテナーは、ファイルシステムフォルダーに対応します。</span><span class="sxs-lookup"><span data-stu-id="0704a-147">A Blob service container corresponds to a file system folder.</span></span> <span data-ttu-id="0704a-148">「[すべて自動化](automate-everything.md)」の章で確認した環境作成スクリプトでは、ストレージアカウントが作成されますが、コンテナーは作成されません。</span><span class="sxs-lookup"><span data-stu-id="0704a-148">The environment creation scripts that we reviewed in the [Automate Everything chapter](automate-everything.md) create the Storage account, but they don't create a container.</span></span> <span data-ttu-id="0704a-149">したがって、`PhotoService` クラスの `CreateAndConfigure` メソッドの目的は、コンテナーがまだ存在しない場合に作成することです。</span><span class="sxs-lookup"><span data-stu-id="0704a-149">So the purpose of the `CreateAndConfigure` method of the `PhotoService` class is to create a container if it doesn't already exist.</span></span> <span data-ttu-id="0704a-150">このメソッドは、 *global.asax*の `Application_Start` メソッドから呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="0704a-150">This method is called from the `Application_Start` method in *Global.asax*.</span></span>

[!code-csharp[Main](unstructured-blob-storage/samples/sample2.cs)]

<span data-ttu-id="0704a-151">ストレージアカウント名とアクセスキー*は、web.config ファイルの*`appSettings` コレクションに格納され、`StorageUtils.StorageAccount` メソッド内のコードはこれらの値を使用して接続文字列を作成し、接続を確立します。</span><span class="sxs-lookup"><span data-stu-id="0704a-151">The storage account name and access key are stored in the `appSettings` collection of the *Web.config* file, and code in the `StorageUtils.StorageAccount` method uses those values to build a connection string and establish a connection:</span></span>

[!code-csharp[Main](unstructured-blob-storage/samples/sample3.cs)]

<span data-ttu-id="0704a-152">次に、`CreateAndConfigureAsync` メソッドは、Blob service を表すオブジェクトと、Blob service 内の "images" という名前のコンテナー (フォルダー) を表すオブジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="0704a-152">The `CreateAndConfigureAsync` method then creates an object that represents the Blob service, and an object that represents a container (folder) named "images" in the Blob service:</span></span>

[!code-csharp[Main](unstructured-blob-storage/samples/sample4.cs)]

<span data-ttu-id="0704a-153">"Images" という名前のコンテナーがまだ存在しない場合は、新しいストレージアカウントに対して初めてアプリを実行したときに true になります。このコードでは、コンテナーを作成し、アクセス許可を設定してパブリックにすることができます。</span><span class="sxs-lookup"><span data-stu-id="0704a-153">If a container named "images" doesn't exist yet -- which will be true the first time you run the app against a new storage account -- the code creates the container and sets permissions to make it public.</span></span> <span data-ttu-id="0704a-154">(既定では、新しい blob コンテナーはプライベートであり、ストレージアカウントへのアクセス許可を持つユーザーのみがアクセスできます)。</span><span class="sxs-lookup"><span data-stu-id="0704a-154">(By default, new blob containers are private and are accessible only to users who have permission to access your storage account.)</span></span>

[!code-csharp[Main](unstructured-blob-storage/samples/sample5.cs)]

### <a name="store-the-uploaded-photo-in-blob-storage"></a><span data-ttu-id="0704a-155">アップロードした写真を Blob storage に保存する</span><span class="sxs-lookup"><span data-stu-id="0704a-155">Store the uploaded photo in Blob storage</span></span>

<span data-ttu-id="0704a-156">イメージファイルをアップロードして保存するために、アプリは、`IPhotoService` インターフェイスと、`PhotoService` クラスのインターフェイスの実装を使用します。</span><span class="sxs-lookup"><span data-stu-id="0704a-156">To upload and save the image file, the app uses an `IPhotoService` interface and an implementation of the interface in the `PhotoService` class.</span></span> <span data-ttu-id="0704a-157">*PhotoService.cs*ファイルには、Blob service と通信する Fix It アプリのすべてのコードが含まれています。</span><span class="sxs-lookup"><span data-stu-id="0704a-157">The *PhotoService.cs* file contains all of the code in the Fix It app that communicates with the Blob service.</span></span>

<span data-ttu-id="0704a-158">次の MVC コントローラーメソッドは、ユーザーが  **FixIt の作成**をクリックしたときに呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="0704a-158">The following MVC controller method is called when the user clicks **Create the FixIt**.</span></span> <span data-ttu-id="0704a-159">このコードでは、`photoService` は `PhotoService` クラスのインスタンスを参照し、`fixittask` は新しいタスクのデータを格納する `FixItTask` エンティティクラスのインスタンスを参照します。</span><span class="sxs-lookup"><span data-stu-id="0704a-159">In this code, `photoService` refers to an instance of the `PhotoService` class, and `fixittask` refers to an instance of the `FixItTask` entity class that stores data for a new task.</span></span>

[!code-csharp[Main](unstructured-blob-storage/samples/sample6.cs?highlight=8)]

<span data-ttu-id="0704a-160">`PhotoService` クラスの `UploadPhotoAsync` メソッドは、アップロードされたファイルを Blob service に格納し、新しい Blob を指す URL を返します。</span><span class="sxs-lookup"><span data-stu-id="0704a-160">The `UploadPhotoAsync` method in the `PhotoService` class stores the uploaded file in the Blob service and returns a URL that points to the new blob.</span></span>

[!code-csharp[Main](unstructured-blob-storage/samples/sample7.cs)]

<span data-ttu-id="0704a-161">`CreateAndConfigure` メソッドと同様に、コードはストレージアカウントに接続し、"images" blob コンテナーを表すオブジェクトを作成します。ただし、コンテナーが既に存在していることを前提としています。</span><span class="sxs-lookup"><span data-stu-id="0704a-161">As in the `CreateAndConfigure` method, the code connects to the storage account and creates an object that represents the "images" blob container, except here it assumes the container already exists.</span></span>

<span data-ttu-id="0704a-162">次に、新しい GUID 値をファイル拡張子と連結して、アップロードするイメージの一意の識別子を作成します。</span><span class="sxs-lookup"><span data-stu-id="0704a-162">Then it creates a unique identifier for the image about to be uploaded, by concatenating a new GUID value with the file extension:</span></span>

[!code-csharp[Main](unstructured-blob-storage/samples/sample8.cs)]

<span data-ttu-id="0704a-163">次に、blob コンテナーオブジェクトと新しい一意識別子を使用して blob オブジェクトを作成し、ファイルの種類を示す属性をそのオブジェクトに設定して、blob オブジェクトを使用して blob ストレージにファイルを格納します。</span><span class="sxs-lookup"><span data-stu-id="0704a-163">The code then uses the blob container object and the new unique identifier to create a blob object, sets an attribute on that object indicating what kind of file it is, and then uses the blob object to store the file in blob storage.</span></span>

[!code-csharp[Main](unstructured-blob-storage/samples/sample9.cs)]

<span data-ttu-id="0704a-164">最後に、blob を参照する URL を取得します。</span><span class="sxs-lookup"><span data-stu-id="0704a-164">Finally, it gets a URL that references the blob.</span></span> <span data-ttu-id="0704a-165">この URL はデータベースに格納され、アップロードされたイメージを表示するために、It web ページの修正に使用できます。</span><span class="sxs-lookup"><span data-stu-id="0704a-165">This URL will be stored in the database and can be used in Fix It web pages to display the uploaded image.</span></span>

[!code-csharp[Main](unstructured-blob-storage/samples/sample10.cs)]

<span data-ttu-id="0704a-166">この URL は、FixItTask テーブルの列の1つとしてデータベースに格納されます。</span><span class="sxs-lookup"><span data-stu-id="0704a-166">This URL is stored in the database as one of the columns of the FixItTask table.</span></span>

[!code-csharp[Main](unstructured-blob-storage/samples/sample11.cs?highlight=10)]

<span data-ttu-id="0704a-167">データベース内の URL と Blob storage のイメージのみを使用すると、It アプリケーションの修正によってデータベースのサイズが小さくなり、スケーラブルで、低コストになります。一方、ストレージは安価で、テラバイトまたはペタバイト単位で処理することができます。</span><span class="sxs-lookup"><span data-stu-id="0704a-167">With only the URL in the database, and images in Blob storage, the Fix It app keeps the database small, scalable, and inexpensive, while the images are stored where storage is cheap and capable of handling terabytes or petabytes.</span></span> <span data-ttu-id="0704a-168">1つのストレージアカウントは、数百テラバイトの写真を修正でき、使用した分だけ支払います。</span><span class="sxs-lookup"><span data-stu-id="0704a-168">One storage account can store hundreds of terabytes of Fix It photos, and you only pay for what you use.</span></span> <span data-ttu-id="0704a-169">最初のギガバイトに対しては9セントの低料金で開始でき、さらにギガバイトごとに少額のイメージを追加することもできます。</span><span class="sxs-lookup"><span data-stu-id="0704a-169">So you can start off small paying 9 cents for the first gigabyte, and add more images for pennies per additional gigabyte.</span></span>

### <a name="display-the-uploaded-file"></a><span data-ttu-id="0704a-170">アップロードされたファイルを表示する</span><span class="sxs-lookup"><span data-stu-id="0704a-170">Display the uploaded file</span></span>

<span data-ttu-id="0704a-171">It アプリケーションを修正すると、タスクの詳細が表示されるときに、アップロードされたイメージファイルが表示されます。</span><span class="sxs-lookup"><span data-stu-id="0704a-171">The Fix It application displays the uploaded image file when it displays details for a task.</span></span>

![写真を使用して It タスクの詳細を修正する](unstructured-blob-storage/_static/image3.png)

<span data-ttu-id="0704a-173">画像を表示するには、すべての MVC ビューで、ブラウザーに送信される HTML に `PhotoUrl` 値が含まれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="0704a-173">To display the image, all the MVC view has to do is include the `PhotoUrl` value in the HTML sent to the browser.</span></span> <span data-ttu-id="0704a-174">Web サーバーとデータベースでは、イメージを表示するためにサイクルが使用されていません。イメージの URL に対して数バイトしか処理されません。</span><span class="sxs-lookup"><span data-stu-id="0704a-174">The web server and the database are not using cycles to display the image, they are only serving up a few bytes to the image URL.</span></span> <span data-ttu-id="0704a-175">次の Razor コードでは、`Model` は `FixItTask` エンティティクラスのインスタンスを参照します。</span><span class="sxs-lookup"><span data-stu-id="0704a-175">In the following Razor code, `Model` refers to an instance of the `FixItTask` entity class.</span></span>

[!code-cshtml[Main](unstructured-blob-storage/samples/sample12.cshtml?highlight=11)]

<span data-ttu-id="0704a-176">表示されるページの HTML を見ると、次のような blob ストレージ内のイメージを直接指す URL が表示されます。</span><span class="sxs-lookup"><span data-stu-id="0704a-176">If you look at the HTML of the page that displays, you see the URL pointing directly to the image in blob storage, something like this:</span></span>

[!code-cshtml[Main](unstructured-blob-storage/samples/sample13.cshtml?highlight=11)]

## <a name="summary"></a><span data-ttu-id="0704a-177">まとめ</span><span class="sxs-lookup"><span data-stu-id="0704a-177">Summary</span></span>

<span data-ttu-id="0704a-178">修正プログラムによる It アプリの Blob service でのイメージの保存方法と、SQL データベースのイメージ Url の使用方法について説明しました。</span><span class="sxs-lookup"><span data-stu-id="0704a-178">You've seen how the Fix It app stores images in the Blob service and only image URLs in the SQL database.</span></span> <span data-ttu-id="0704a-179">Blob service を使用すると、SQL データベースは、それ以外の場合と比べて大幅に小さくなります。これにより、ほぼ無制限の数のタスクをスケールアップすることができ、多くのコードを記述することなく実行できます。</span><span class="sxs-lookup"><span data-stu-id="0704a-179">Using the Blob service keeps the SQL database much smaller than it otherwise would be, makes it possible to scale up to an almost unlimited number of tasks, and can be done without writing a lot of code.</span></span>

<span data-ttu-id="0704a-180">ストレージアカウントには数百テラバイトを含めることができますが、ストレージコストは SQL Database ストレージよりもはるかにコストがかかります。これは、1 gb あたり約3セントで、トランザクション料金は小さいものです。</span><span class="sxs-lookup"><span data-stu-id="0704a-180">You can have hundreds of terabytes in a storage account, and the storage cost is much less expensive than SQL Database storage, starting at about 3 cents per gigabyte per month plus a small transaction charge.</span></span> <span data-ttu-id="0704a-181">また、最大容量に対しては料金がかかりませんが、実際に格納されている量に対してのみ料金がかかります。そのため、アプリは拡張することができますが、その他の容量については一切料金がかかりません。</span><span class="sxs-lookup"><span data-stu-id="0704a-181">And keep in mind that you're not paying for the maximum capacity but only for the amount you actually store, so your app is ready to scale but you're not paying for all that extra capacity.</span></span>

<span data-ttu-id="0704a-182">次の[章](design-to-survive-failures.md)では、クラウドアプリがエラーを適切に処理できるようにすることの重要性について説明します。</span><span class="sxs-lookup"><span data-stu-id="0704a-182">In the [next chapter](design-to-survive-failures.md) we'll talk about the importance of making a cloud app capable of gracefully handling failures.</span></span>

## <a name="resources"></a><span data-ttu-id="0704a-183">リソース</span><span class="sxs-lookup"><span data-stu-id="0704a-183">Resources</span></span>

<span data-ttu-id="0704a-184">詳細については、次のリソースを参照してください。</span><span class="sxs-lookup"><span data-stu-id="0704a-184">For more information see the following resources:</span></span>

- <span data-ttu-id="0704a-185">[AZURE BLOB Storage の概要](https://www.simple-talk.com/cloud/cloud-data/an-introduction-to-windows-azure-blob-storage-/)。</span><span class="sxs-lookup"><span data-stu-id="0704a-185">[An Introduction to Azure BLOB Storage](https://www.simple-talk.com/cloud/cloud-data/an-introduction-to-windows-azure-blob-storage-/).</span></span> <span data-ttu-id="0704a-186">ブログ (Mike 木材)</span><span class="sxs-lookup"><span data-stu-id="0704a-186">Blog by Mike Wood.</span></span>
- <span data-ttu-id="0704a-187">[.Net で Azure Blob Storage サービスを使用する方法](https://docs.microsoft.com/azure/storage/blobs/storage-dotnet-how-to-use-blobs)。</span><span class="sxs-lookup"><span data-stu-id="0704a-187">[How to use the Azure Blob Storage Service in .NET](https://docs.microsoft.com/azure/storage/blobs/storage-dotnet-how-to-use-blobs).</span></span> <span data-ttu-id="0704a-188">MicrosoftAzure.com サイトの公式ドキュメント。</span><span class="sxs-lookup"><span data-stu-id="0704a-188">Official documentation on the MicrosoftAzure.com site.</span></span> <span data-ttu-id="0704a-189">Blob storage の概要と、blob storage への接続、コンテナーの作成、blob のアップロードとダウンロードなどを示すコード例を紹介します。</span><span class="sxs-lookup"><span data-stu-id="0704a-189">A brief introduction to blob storage followed by code examples showing how to connect to blob storage, create containers, upload and download blobs, etc.</span></span>
- <span data-ttu-id="0704a-190">[フェイルセーフ: スケーラブルで回復力のある Cloud Services を構築](https://channel9.msdn.com/Series/FailSafe)します。</span><span class="sxs-lookup"><span data-stu-id="0704a-190">[FailSafe: Building Scalable, Resilient Cloud Services](https://channel9.msdn.com/Series/FailSafe).</span></span> <span data-ttu-id="0704a-191">Ulrich Homann、Marc Mercuri、Mark Simm による9部構成のビデオシリーズ。</span><span class="sxs-lookup"><span data-stu-id="0704a-191">Nine-part video series by Ulrich Homann, Marc Mercuri, and Mark Simms.</span></span> <span data-ttu-id="0704a-192">高度な概念とアーキテクチャの原則を、非常にアクセスしやすく興味深い方法で紹介します。実際の顧客との Microsoft カスタマーアドバイザリチーム (CAT) エクスペリエンスによってストーリーが描画されます。</span><span class="sxs-lookup"><span data-stu-id="0704a-192">Presents high-level concepts and architectural principles in a very accessible and interesting way, with stories drawn from Microsoft Customer Advisory Team (CAT) experience with actual customers.</span></span> <span data-ttu-id="0704a-193">Azure Storage サービスと blob の詳細については、35:13 以降のエピソード5を参照してください。</span><span class="sxs-lookup"><span data-stu-id="0704a-193">For a discussion of Azure Storage service and blobs, see episode 5 starting at 35:13.</span></span>
- <span data-ttu-id="0704a-194">[Microsoft のパターンとプラクティス-Azure のガイダンス](https://msdn.microsoft.com/library/dn568099.aspx)。</span><span class="sxs-lookup"><span data-stu-id="0704a-194">[Microsoft Patterns and Practices - Azure Guidance](https://msdn.microsoft.com/library/dn568099.aspx).</span></span> <span data-ttu-id="0704a-195">「Valet キーパターン」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="0704a-195">See Valet Key pattern.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="0704a-196">[前へ](data-partitioning-strategies.md)
> [次へ](design-to-survive-failures.md)</span><span class="sxs-lookup"><span data-stu-id="0704a-196">[Previous](data-partitioning-strategies.md)
[Next](design-to-survive-failures.md)</span></span>
