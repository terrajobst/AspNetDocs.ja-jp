---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/the-fix-it-sample-application
title: '付録: Fix It サンプルアプリケーション (Azure を使用した実際のクラウドアプリの構築) |Microsoft Docs'
author: MikeWasson
description: Azure 電子ブックを使用した実際のクラウドアプリの構築は、Scott Guthrie によって開発されたプレゼンテーションに基づいています。 13のパターンとベストプラクティスについて説明します。
ms.author: riande
ms.date: 06/12/2014
ms.assetid: 1bc333c5-f096-4ea7-b170-779accc21c1a
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/the-fix-it-sample-application
msc.type: authoredcontent
ms.openlocfilehash: e6fda47babd3c2505315f42667c45f09482218c2
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74583745"
---
# <a name="appendix-the-fix-it-sample-application-building-real-world-cloud-apps-with-azure"></a><span data-ttu-id="bd5f7-104">付録: Fix It サンプルアプリケーション (Azure を使用した実際のクラウドアプリの構築)</span><span class="sxs-lookup"><span data-stu-id="bd5f7-104">Appendix: The Fix It Sample Application (Building Real-World Cloud Apps with Azure)</span></span>

<span data-ttu-id="bd5f7-105">[Mike Wasson](https://github.com/MikeWasson)、 [Rick Anderson]((https://twitter.com/RickAndMSFT))、 [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="bd5f7-105">by [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson]((https://twitter.com/RickAndMSFT)), [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="bd5f7-106">修正プログラムのプロジェクトをダウンロードする</span><span class="sxs-lookup"><span data-stu-id="bd5f7-106">Download The Fix It Project</span></span>](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)

> <span data-ttu-id="bd5f7-107">Azure 電子ブック**を使用した実際のクラウドアプリの構築**は、Scott Guthrie によって開発されたプレゼンテーションに基づいています。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-107">The **Building Real World Cloud Apps with Azure** e-book is based on a presentation developed by Scott Guthrie.</span></span> <span data-ttu-id="bd5f7-108">ここでは、クラウド用の web アプリの開発を成功させるのに役立つ13のパターンとプラクティスについて説明します。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-108">It explains 13 patterns and practices that can help you be successful developing web apps for the cloud.</span></span> <span data-ttu-id="bd5f7-109">電子書籍の詳細については、[最初の章](introduction.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-109">For information about the e-book, see [the first chapter](introduction.md).</span></span>

<span data-ttu-id="bd5f7-110">この付録では、Azure 電子ブックを使用した実際のクラウドアプリの構築について説明します。次のセクションでは、ダウンロード可能な修正プログラムサンプルアプリケーションに関する追加情報を提供しています。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-110">This appendix to the Building Real World Cloud Apps with Azure e-book contains the following sections that provide additional information about the Fix It sample application that you can download:</span></span>

- [<span data-ttu-id="bd5f7-111">既知の問題</span><span class="sxs-lookup"><span data-stu-id="bd5f7-111">Known issues</span></span>](#knownissues)
- [<span data-ttu-id="bd5f7-112">ベスト プラクティス</span><span class="sxs-lookup"><span data-stu-id="bd5f7-112">Best practices</span></span>](#bestpractices)
- [<span data-ttu-id="bd5f7-113">ローカルコンピューター上の Visual Studio からアプリを実行する方法</span><span class="sxs-lookup"><span data-stu-id="bd5f7-113">How to run the app from Visual Studio on your local computer</span></span>](#run-in-vs)
- [<span data-ttu-id="bd5f7-114">Windows PowerShell スクリプトを使用して Azure App Service Web Apps に基本アプリを展開する方法</span><span class="sxs-lookup"><span data-stu-id="bd5f7-114">How to deploy the base app to Azure App Service Web Apps by using the Windows PowerShell scripts</span></span>](#deploybase)
- [<span data-ttu-id="bd5f7-115">Windows PowerShell スクリプトのトラブルシューティング</span><span class="sxs-lookup"><span data-stu-id="bd5f7-115">Troubleshooting the Windows PowerShell scripts</span></span>](#troubleshooting)
- [<span data-ttu-id="bd5f7-116">キュー処理を使用してアプリを Azure App Service Web Apps と Azure クラウドサービスにデプロイする方法</span><span class="sxs-lookup"><span data-stu-id="bd5f7-116">How to deploy the app with queue processing to Azure App Service Web Apps and an Azure Cloud Service</span></span>](#deployqueues)

<a id="knownissues"></a>
## <a name="known-issues"></a><span data-ttu-id="bd5f7-117">既知の問題</span><span class="sxs-lookup"><span data-stu-id="bd5f7-117">Known issues</span></span>

<span data-ttu-id="bd5f7-118">この電子書籍に記載されているパターンのいくつかをできるだけ簡単に説明するために、It アプリを修正しました。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-118">The Fix It app was originally developed in order to illustrate as simply as possible some of the patterns presented in this e-book.</span></span> <span data-ttu-id="bd5f7-119">ただし、電子書籍は実際のアプリの作成に関するものであるため、リリースされたソフトウェアの場合と同様に、レビューおよびテストのプロセスに対してコードの修正を実施しました。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-119">However, since the e-book is about building real-world apps, we subjected the Fix It code to a review and testing process similar to what we'd do for released software.</span></span> <span data-ttu-id="bd5f7-120">いくつかの問題が見つかりました。実際のアプリケーションと同様に、いくつかの問題が修正され、その一部は今後のリリースに延期されました。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-120">We found a number of issues, and as with any real-world application, some of them we fixed and some of them we deferred to a later release.</span></span>

<span data-ttu-id="bd5f7-121">次の一覧には、実稼働アプリケーションで対処する必要がある問題が含まれていますが、1つの理由として、Fix It サンプルアプリケーションの最初のリリースでは対応していないと判断しました。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-121">The following list includes issues that should be addressed in a production application, but for one reason or another we decided not to address in the initial release of the Fix It sample application.</span></span>

### <a name="security"></a><span data-ttu-id="bd5f7-122">セキュリティ</span><span class="sxs-lookup"><span data-stu-id="bd5f7-122">Security</span></span>

- <span data-ttu-id="bd5f7-123">存在しない所有者にタスクを割り当てることができないようにしてください。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-123">Ensure that you can't assign a task to a non-existent owner.</span></span>
- <span data-ttu-id="bd5f7-124">作成したタスク、または自分に割り当てられたタスクだけを表示および変更できることを確認します。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-124">Ensure that you can only view and modify tasks that you created or are assigned to you.</span></span>
- <span data-ttu-id="bd5f7-125">サインインページと認証 cookie には HTTPS を使用します。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-125">Use HTTPS for sign-in pages and authentication cookies.</span></span>
- <span data-ttu-id="bd5f7-126">認証 cookie の制限時間を指定します。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-126">Specify a time limit for authentication cookies.</span></span>

### <a name="input-validation"></a><span data-ttu-id="bd5f7-127">入力の検証</span><span class="sxs-lookup"><span data-stu-id="bd5f7-127">Input validation</span></span>

<span data-ttu-id="bd5f7-128">一般に、運用アプリでは、It アプリの修正よりも多くの入力検証が行われます。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-128">In general, a production app would do more input validation than the Fix It app.</span></span> <span data-ttu-id="bd5f7-129">たとえば、アップロードに許可されているイメージサイズ/イメージファイルのサイズは制限する必要があります。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-129">For example, the image size / image file size allowed for upload should be limited.</span></span>

### <a name="administrator-functionality"></a><span data-ttu-id="bd5f7-130">管理者の機能</span><span class="sxs-lookup"><span data-stu-id="bd5f7-130">Administrator functionality</span></span>

<span data-ttu-id="bd5f7-131">管理者は、既存のタスクの所有権を変更できなければなりません。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-131">An administrator should be able to change ownership on existing tasks.</span></span> <span data-ttu-id="bd5f7-132">たとえば、タスクの作成者が会社を退職した場合、管理アクセスが有効になっていない限り、タスクを維持する権限はありません。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-132">For example, the creator of a task might leave the company, leaving no one with authority to maintain the task unless administrative access is enabled.</span></span>

### <a name="queue-message-processing"></a><span data-ttu-id="bd5f7-133">キューメッセージの処理</span><span class="sxs-lookup"><span data-stu-id="bd5f7-133">Queue message processing</span></span>

<span data-ttu-id="bd5f7-134">Fix It アプリでのキューメッセージ処理は、最小限のコードでキュー中心の作業パターンを示すために単純なものとして設計されました。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-134">Queue message processing in the Fix It app was designed to be simple in order to illustrate the queue-centric work pattern with a minimum amount of code.</span></span> <span data-ttu-id="bd5f7-135">この単純なコードは、実際の運用アプリケーションには適していません。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-135">This simple code would not be adequate for an actual production application.</span></span>

- <span data-ttu-id="bd5f7-136">このコードでは、各キューメッセージが1回だけ処理されることは保証されません。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-136">The code does not guarantee that each queue message will be processed at most once.</span></span> <span data-ttu-id="bd5f7-137">キューからメッセージを取得すると、タイムアウト期間が発生します。その間、メッセージは他のキューリスナーに対して非表示になります。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-137">When you get a message from the queue, there is a timeout period, during which the message is invisible to other queue listeners.</span></span> <span data-ttu-id="bd5f7-138">メッセージが削除される前にタイムアウトが経過すると、メッセージが再び表示されるようになります。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-138">If the timeout expires before the message is deleted, the message becomes visible again.</span></span> <span data-ttu-id="bd5f7-139">このため、worker ロールインスタンスがメッセージの処理に長い時間がかかる場合は、同じメッセージが2回処理される可能性があり、その結果、データベースに重複するタスクが発生します。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-139">Therefore, if a worker role instance spends a long time processing a message, it is theoretically possible for the same message to get processed twice, resulting in a duplicate task in the database.</span></span> <span data-ttu-id="bd5f7-140">この問題の詳細については、「 [Azure Storage キューの使用](https://msdn.microsoft.com/library/ff803365.aspx#sec7)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-140">For more information about this issue, see [Using Azure Storage Queues](https://msdn.microsoft.com/library/ff803365.aspx#sec7).</span></span>
- <span data-ttu-id="bd5f7-141">キューのポーリングロジックは、メッセージの取得をバッチ処理することにより、コスト効率に優れています。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-141">The queue polling logic could be more cost-effective, by batching message retrieval.</span></span> <span data-ttu-id="bd5f7-142">[GetMessageAsync](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.getmessageasync.aspx)を呼び出すたびに、トランザクションコストが発生します。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-142">Every time you call [CloudQueue.GetMessageAsync](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.getmessageasync.aspx), there is a transaction cost.</span></span> <span data-ttu-id="bd5f7-143">代わりに、 [Cloudqueue. Getmessages async](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.getmessagesasync.aspx) (複数形の ') を呼び出すことができます。この場合、1つのトランザクションで複数のメッセージが取得されます。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-143">Instead, you can call [CloudQueue.GetMessagesAsync](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.getmessagesasync.aspx) (note the plural 's'), which gets multiple messages in a single transaction.</span></span> <span data-ttu-id="bd5f7-144">Azure Storage キューのトランザクションコストが非常に低いため、ほとんどのシナリオではコストへの影響は大きくありません。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-144">The transaction costs for Azure Storage Queues are very low, so the impact on costs is not substantial in most scenarios.</span></span>
- <span data-ttu-id="bd5f7-145">キューメッセージ処理コードの短いループにより、CPU アフィニティが発生します。この場合、マルチコア Vm は効率的に使用されません。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-145">The tight loop in the queue message-processing code causes CPU affinity, which does not utilize multi-core VMs efficiently.</span></span> <span data-ttu-id="bd5f7-146">より優れた設計では、タスクの並列化を使用して複数の非同期タスクを並列に実行します。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-146">A better design would use task parallelism to run several async tasks in parallel.</span></span>
- <span data-ttu-id="bd5f7-147">キューメッセージの処理には、基本的な例外処理しかありません。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-147">Queue message-processing has only rudimentary exception handling.</span></span> <span data-ttu-id="bd5f7-148">たとえば、コードは[有害なメッセージ](https://msdn.microsoft.com/library/ms789028.aspx)を処理しません。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-148">For example, the code doesn't handle [poison messages](https://msdn.microsoft.com/library/ms789028.aspx).</span></span> <span data-ttu-id="bd5f7-149">(メッセージ処理によって例外が発生した場合は、エラーを記録してメッセージを削除する必要があります。そうしないと、ワーカーロールはその処理を再試行し、ループは無期限に続行されます)。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-149">(When message processing causes an exception, you have to log the error and delete the message, or the worker role will try to process it again, and the loop will continue indefinitely.)</span></span>

### <a name="sql-queries-are-unbounded"></a><span data-ttu-id="bd5f7-150">SQL クエリはバインドされていません</span><span class="sxs-lookup"><span data-stu-id="bd5f7-150">SQL queries are unbounded</span></span>

<span data-ttu-id="bd5f7-151">現在の修正このコードでは、インデックスページのクエリが返す行の数に制限はありません。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-151">Current Fix It code places no limit on how many rows the queries for Index pages might return.</span></span> <span data-ttu-id="bd5f7-152">大量のタスクがデータベースに入力されると、受信したリストのサイズによってパフォーマンスの問題が発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-152">If a large volume of tasks is entered into the database, the size of the resulting lists received could cause performance issues.</span></span> <span data-ttu-id="bd5f7-153">この解決策は、ページングを実装することです。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-153">The solution is to implement paging.</span></span> <span data-ttu-id="bd5f7-154">例については、「 [ASP.NET MVC アプリケーションでの Entity Framework の並べ替え、フィルター処理、およびページング](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-154">For an example, see [Sorting, Filtering, and Paging with the Entity Framework in an ASP.NET MVC Application](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md).</span></span>

### <a name="view-models-recommended"></a><span data-ttu-id="bd5f7-155">推奨されるモデルの表示</span><span class="sxs-lookup"><span data-stu-id="bd5f7-155">View models recommended</span></span>

<span data-ttu-id="bd5f7-156">Fix It アプリは、FixItTask エンティティクラスを使用して、コントローラーとビューの間で情報を渡します。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-156">The Fix It app uses the FixItTask entity class to pass information between the controller and the view.</span></span> <span data-ttu-id="bd5f7-157">ビューモデルを使用することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-157">A best practice is to use view models.</span></span> <span data-ttu-id="bd5f7-158">ドメインモデル (FixItTask エンティティクラスなど) は、データの永続化に必要なものを中心に設計されていますが、ビューモデルはデータ表示用に設計できます。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-158">The domain model (e.g., the FixItTask entity class) is designed around what is needed for data persistence, while a view model can be designed for data presentation.</span></span> <span data-ttu-id="bd5f7-159">詳細については、「 [12 ASP.NET MVC のベストプラクティス](https://codeclimber.net.nz/archive/2009/10/27/12-asp.net-mvc-best-practices.aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-159">For more information, see [12 ASP.NET MVC Best Practices](https://codeclimber.net.nz/archive/2009/10/27/12-asp.net-mvc-best-practices.aspx).</span></span>

### <a name="secure-image-blob-recommended"></a><span data-ttu-id="bd5f7-160">保護されたイメージ blob を推奨</span><span class="sxs-lookup"><span data-stu-id="bd5f7-160">Secure image blob recommended</span></span>

<span data-ttu-id="bd5f7-161">Fix It アプリは、アップロードされたイメージをパブリックとして保存します。つまり、URL を見つけたすべてのユーザーがイメージにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-161">The Fix It app stores uploaded images as public, meaning that anyone who finds the URL can access the images.</span></span> <span data-ttu-id="bd5f7-162">イメージは、パブリックではなく、セキュリティで保護されている可能性があります。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-162">The images could be secured instead of public.</span></span>

### <a name="no-powershell-automation-scripts-for-queues"></a><span data-ttu-id="bd5f7-163">キュー用の PowerShell オートメーションスクリプトがありません</span><span class="sxs-lookup"><span data-stu-id="bd5f7-163">No PowerShell automation scripts for queues</span></span>

<span data-ttu-id="bd5f7-164">サンプル PowerShell の自動化スクリプトは、Azure App Service Web Apps で完全に実行される、修正プログラムの基本バージョンに対してのみ作成されました。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-164">Sample PowerShell automation scripts were written only for the base version of Fix It that runs entirely in Azure App Service Web Apps.</span></span> <span data-ttu-id="bd5f7-165">キューの処理に必要な web アプリとクラウドサービス環境を設定してデプロイするためのスクリプトは提供されていません。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-165">We haven't provided scripts for setting up and deploying to the web app plus Cloud Service environment required for queue processing.</span></span>

### <a name="special-handling-for-html-codes-in-user-input"></a><span data-ttu-id="bd5f7-166">ユーザー入力における HTML コードの特別な処理</span><span class="sxs-lookup"><span data-stu-id="bd5f7-166">Special handling for HTML codes in user input</span></span>

<span data-ttu-id="bd5f7-167">ASP.NET を使用すると、ユーザー入力テキストボックスにスクリプトを入力することで、悪意のあるユーザーがクロスサイトスクリプト攻撃を試みる可能性が自動的に回避されます。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-167">ASP.NET automatically prevents many ways in which malicious users might attempt cross-site scripting attacks by entering script in user input text boxes.</span></span> <span data-ttu-id="bd5f7-168">また、タスクタイトルとメモを表示するために使用される MVC `DisplayFor` ヘルパーは、ブラウザーに送信する値を自動的に HTML エンコードします。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-168">And the MVC `DisplayFor` helper used to display task titles and notes automatically HTML-encodes values that it sends to the browser.</span></span> <span data-ttu-id="bd5f7-169">しかし、運用アプリでは、追加の手段を取る必要がある場合があります。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-169">But in a production app you might want to take additional measures.</span></span> <span data-ttu-id="bd5f7-170">詳細については、「 [ASP.NET での要求の検証](https://msdn.microsoft.com/library/hh882339.aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-170">For more information, see [Request Validation in ASP.NET](https://msdn.microsoft.com/library/hh882339.aspx).</span></span>

<a id="bestpractices"></a>
## <a name="best-practices"></a><span data-ttu-id="bd5f7-171">ベスト プラクティス</span><span class="sxs-lookup"><span data-stu-id="bd5f7-171">Best practices</span></span>

<span data-ttu-id="bd5f7-172">次に示すのは、修正後の It アプリの元のバージョンのコードレビューとテストで解決された問題です。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-172">Following are some issues that were fixed after being discovered in code review and testing of the original version of the Fix It app.</span></span> <span data-ttu-id="bd5f7-173">元のプログラマが特定のベストプラクティスを認識していないことが原因として考えられるのは、コードが迅速に記述され、リリースされたソフトウェアを意図していなかったためです。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-173">Some were caused by the original coder not being aware of a particular best practice, some simply because the code was written quickly and wasn't intended for released software.</span></span> <span data-ttu-id="bd5f7-174">ここでは、web アプリを開発している他のユーザーにとって役に立つ可能性がある、このレビューとテストから学んだことがある問題について説明しています。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-174">We're listing the issues here in case there's something we learned from this review and testing that might be helpful to others who are also developing web apps.</span></span>

### <a name="dispose-the-database-repository"></a><span data-ttu-id="bd5f7-175">データベースリポジトリを破棄します。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-175">Dispose the database repository</span></span>

<span data-ttu-id="bd5f7-176">`FixItTaskRepository` クラスは、Entity Framework `DbContext` インスタンスを破棄する必要があります。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-176">The `FixItTaskRepository` class must dispose the Entity Framework `DbContext` instance.</span></span> <span data-ttu-id="bd5f7-177">これを行うには、`FixItTaskRepository` クラスに `IDisposable` を実装します。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-177">We did this by implementing `IDisposable` in the `FixItTaskRepository` class:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample1.cs)]

<span data-ttu-id="bd5f7-178">AutoFac によって `FixItTaskRepository` インスタンスが自動的に破棄されるので、明示的に破棄する必要がないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-178">Note that AutoFac will automatically dispose the `FixItTaskRepository` instance, so we don't need to explicitly dispose it.</span></span>

<span data-ttu-id="bd5f7-179">もう1つのオプションは、`FixItTaskRepository`から `DbContext` メンバー変数を削除し、`using` ステートメント内で各リポジトリメソッド内にローカル `DbContext` 変数を作成することです。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-179">Another option is to remove the `DbContext` member variable from `FixItTaskRepository`, and instead create a local `DbContext` variable within each repository method, inside a `using` statement.</span></span> <span data-ttu-id="bd5f7-180">例:</span><span class="sxs-lookup"><span data-stu-id="bd5f7-180">For example:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample2.cs)]

### <a name="register-singletons-as-such-with-di"></a><span data-ttu-id="bd5f7-181">DI を使用してシングルトンを登録する</span><span class="sxs-lookup"><span data-stu-id="bd5f7-181">Register singletons as such with DI</span></span>

<span data-ttu-id="bd5f7-182">`PhotoService` クラスと `Logger` クラスのインスタンスは1つだけ必要であるため、これらのクラスは*DependenciesConfig.cs*での[依存関係の挿入のために1つのインスタンスとして登録](https://code.google.com/p/autofac/wiki/InstanceScope)する必要があります。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-182">Since only one instance of the `PhotoService` class and `Logger` class is needed, these classes should be [registered as single instances for dependency injection](https://code.google.com/p/autofac/wiki/InstanceScope) in *DependenciesConfig.cs*:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample3.cs?highlight=1,3)]

### <a name="security-dont-show-error-details-to-users"></a><span data-ttu-id="bd5f7-183">セキュリティ: エラーの詳細をユーザーに表示しない</span><span class="sxs-lookup"><span data-stu-id="bd5f7-183">Security: Don't show error details to users</span></span>

<span data-ttu-id="bd5f7-184">元の Fix It アプリには一般的なエラーページがありません。すべての例外が UI にバブルアップされるだけなので、データベース接続エラーなどの例外によっては、完全なスタックトレースがブラウザーに表示される可能性があります。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-184">The original Fix It app didn't have a generic error page and just let all exceptions bubble up to the UI, so some exceptions such as database connection errors could result in a full stack trace being displayed to the browser.</span></span> <span data-ttu-id="bd5f7-185">エラーの詳細情報は、悪意のあるユーザーによる攻撃を促進することがあります。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-185">Detailed error information can sometimes facilitate attacks by malicious users.</span></span> <span data-ttu-id="bd5f7-186">この問題を解決するには、例外の詳細をログに記録し、エラーの詳細が含まれていないエラーページをユーザーに表示します。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-186">The solution is to log the exception details and display an error page to the user that doesn't include error details.</span></span> <span data-ttu-id="bd5f7-187">Fix It アプリは既にログ記録されており、エラーページを表示するために、web.config ファイルに `<customErrors mode=On>` を追加しました。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-187">The Fix It app was already logging, and in order to display an error page, we added `<customErrors mode=On>` in the Web.config file.</span></span>

[!code-xml[Main](the-fix-it-sample-application/samples/sample4.xml?highlight=2)]

<span data-ttu-id="bd5f7-188">既定では、これにより、エラーの*Views\Shared\Error.cshtml*が表示されます。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-188">By default this causes *Views\Shared\Error.cshtml* to be displayed for errors.</span></span> <span data-ttu-id="bd5f7-189">*エラー*をカスタマイズすることも、独自のエラーページビューを作成して、`defaultRedirect` 属性を追加することもできます。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-189">You can customize *Error.cshtml* or create your own error page view and add a `defaultRedirect` attribute.</span></span> <span data-ttu-id="bd5f7-190">また、特定のエラーに対して別のエラーページを指定することもできます。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-190">You can also specify different error pages for specific errors.</span></span>

### <a name="security-only-allow-a-task-to-be-edited-by-its-creator"></a><span data-ttu-id="bd5f7-191">セキュリティ: タスクの作成者だけが編集できるようにする</span><span class="sxs-lookup"><span data-stu-id="bd5f7-191">Security: only allow a task to be edited by its creator</span></span>

<span data-ttu-id="bd5f7-192">ダッシュボードのインデックスページには、ログオンしているユーザーによって作成されたタスクのみが表示されますが、悪意のあるユーザーが、別のユーザーのタスクに ID を持つ URL を作成する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-192">The Dashboard Index page only shows tasks created by the logged-on user, but a malicious user could create a URL with an ID to another user's task.</span></span> <span data-ttu-id="bd5f7-193">この場合、404を返すコードを*DashboardController.cs*に追加しました。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-193">We added code in *DashboardController.cs* to return a 404 in that case:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample5.cs?highlight=9-14,24-29)]

### <a name="dont-swallow-exceptions"></a><span data-ttu-id="bd5f7-194">例外を飲み込むしない</span><span class="sxs-lookup"><span data-stu-id="bd5f7-194">Don't swallow exceptions</span></span>

<span data-ttu-id="bd5f7-195">元の Fix It アプリでは、SQL クエリの結果として発生した例外をログに記録した後、次のように null が返されました。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-195">The original Fix It app just returned null after logging an exception that resulted from a SQL query:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample6.cs?highlight=4)]

<span data-ttu-id="bd5f7-196">これにより、クエリが成功したとしても、行が返されなかったかのようにユーザーに表示されるようになります。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-196">This would make it look to the user as if the query succeeded but just didn't return any rows.</span></span> <span data-ttu-id="bd5f7-197">解決策は、キャッチしてログを記録した後に例外を再スローすることです。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-197">Solution is to re-throw the exception after catching and logging:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample7.cs)]

### <a name="catch-all-exceptions-in-worker-roles"></a><span data-ttu-id="bd5f7-198">Worker ロールのすべての例外をキャッチする</span><span class="sxs-lookup"><span data-stu-id="bd5f7-198">Catch all exceptions in worker roles</span></span>

<span data-ttu-id="bd5f7-199">ワーカーロールでハンドルされない例外が発生すると、VM がリサイクルされます。そのため、try-catch ブロックで実行するすべての処理をラップし、すべての例外を処理する必要があります。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-199">Any unhandled exceptions in a worker role will cause the VM to be recycled, so you want to wrap everything you do in a try-catch block and handle all exceptions.</span></span>

### <a name="specify-length-for-string-properties-in-entity-classes"></a><span data-ttu-id="bd5f7-200">エンティティクラスの文字列プロパティの長さを指定する</span><span class="sxs-lookup"><span data-stu-id="bd5f7-200">Specify length for string properties in entity classes</span></span>

<span data-ttu-id="bd5f7-201">単純なコードを表示するために、Fix It アプリの元のバージョンは、FixItTask エンティティのフィールドの長さを指定していませんでした。その結果、データベースで varchar (max) として定義されました。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-201">In order to display simple code, the original version of the Fix It app didn't specify lengths for the fields of the FixItTask entity, and as a result they were defined as varchar(max) in the database.</span></span> <span data-ttu-id="bd5f7-202">その結果、UI はほぼすべての入力を受け入れます。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-202">As a result, the UI would accept almost any amount of input.</span></span> <span data-ttu-id="bd5f7-203">長さを指定すると、web ページのユーザー入力とデータベースの列サイズの両方に適用される制限が設定されます。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-203">Specifying lengths sets limits that apply both to user input in the web page and column size in the database:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample8.cs?highlight=4,7,10,12,14)]

### <a name="mark-private-members-as-readonly-when-they-arent-expected-to-change"></a><span data-ttu-id="bd5f7-204">プライベートメンバーが変更されることが予想されない場合は、プライベートメンバーを読み取り専用としてマークする</span><span class="sxs-lookup"><span data-stu-id="bd5f7-204">Mark private members as readonly when they aren't expected to change</span></span>

<span data-ttu-id="bd5f7-205">たとえば、`DashboardController` クラスでは `FixItTaskRepository` のインスタンスが作成され、変更されることは想定されていないため、 [readonly](https://msdn.microsoft.com/library/acdd6hb7.aspx)として定義しました。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-205">For example, in the `DashboardController` class an instance of `FixItTaskRepository` is created and isn't expected to change, so we defined it as [readonly](https://msdn.microsoft.com/library/acdd6hb7.aspx).</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample9.cs?highlight=3)]

### <a name="use-listany-instead-of-listcount-gt-0"></a><span data-ttu-id="bd5f7-206">リストを使用します。List ではなく任意の ()。Count () &gt; 0</span><span class="sxs-lookup"><span data-stu-id="bd5f7-206">Use list.Any() instead of list.Count() &gt; 0</span></span>

<span data-ttu-id="bd5f7-207">リスト内の1つ以上の項目が指定した条件に適合するかどうかを確認するだけの場合は、[[任意](https://msdn.microsoft.com/library/bb534972.aspx)のメソッド] を使用します。これは、条件を満たす項目が見つかった場合はすぐに制御が戻るのに対し、`Count` メソッドは常にすべての項目を反復処理する必要があるためです。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-207">If you all you care about is whether one or more items in a list fit the specified criteria, use the [Any](https://msdn.microsoft.com/library/bb534972.aspx) method, because it returns as soon as an item fitting the criteria is found, whereas the `Count` method always has to iterate through every item.</span></span> <span data-ttu-id="bd5f7-208">ダッシュボードの*インデックスの cshtml*ファイルには、最初に次のコードが含まれていました。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-208">The Dashboard *Index.cshtml* file originally had this code:</span></span>

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample10.cshtml)]

<span data-ttu-id="bd5f7-209">次のように変更しました。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-209">We changed it to this:</span></span>

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample11.cshtml?highlight=1)]

### <a name="generate-urls-in-mvc-views-using-mvc-helpers"></a><span data-ttu-id="bd5f7-210">Mvc ヘルパーを使用した MVC ビューでの Url の生成</span><span class="sxs-lookup"><span data-stu-id="bd5f7-210">Generate URLs in MVC views using MVC helpers</span></span>

<span data-ttu-id="bd5f7-211">ホームページの [Fix It] \ (**修正プログラムの作成**\) ボタンをクリックすると、it アプリの修正によってアンカー要素がハードコーディングされます。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-211">For the **Create a Fix It** button on the home page, the Fix It app hard coded an anchor element:</span></span>

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample12.cshtml)]

<span data-ttu-id="bd5f7-212">このようなビュー/アクションリンクについては、次の例のように、 [Url. action](https://msdn.microsoft.com/library/system.web.mvc.urlhelper.action.aspx) HTML helper を使用することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-212">For View/Action links like this it's better to use the [Url.Action](https://msdn.microsoft.com/library/system.web.mvc.urlhelper.action.aspx) HTML helper, for example:</span></span>

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample13.cshtml)]

### <a name="use-taskdelay-instead-of-threadsleep-in-worker-role"></a><span data-ttu-id="bd5f7-213">ワーカーロールでは、Thread ではなく Delay を使用します</span><span class="sxs-lookup"><span data-stu-id="bd5f7-213">Use Task.Delay instead of Thread.Sleep in worker role</span></span>

<span data-ttu-id="bd5f7-214">新しいプロジェクトのテンプレートでは、ワーカーロールのサンプルコードに `Thread.Sleep` が配置されますが、スレッドがスリープ状態になると、スレッドプールによって余分な不要なスレッドが生成される可能性があります。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-214">The new-project template puts `Thread.Sleep` in the sample code for a worker role, but causing the thread to sleep can cause the thread pool to spawn additional unnecessary threads.</span></span> <span data-ttu-id="bd5f7-215">これを回避するには、代わりに[Delay](https://msdn.microsoft.com/library/hh139096.aspx)を使用します。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-215">You can avoid that by using [Task.Delay](https://msdn.microsoft.com/library/hh139096.aspx) instead.</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample14.cs?highlight=11)]

### <a name="avoid-async-void"></a><span data-ttu-id="bd5f7-216">非同期 void を回避する</span><span class="sxs-lookup"><span data-stu-id="bd5f7-216">Avoid async void</span></span>

<span data-ttu-id="bd5f7-217">非同期メソッドが値を返す必要がない場合は、`void`ではなく `Task` の型を返します。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-217">If an async method doesn't need to return a value, return a `Task` type rather than `void`.</span></span>

<span data-ttu-id="bd5f7-218">この例は、`FixItQueueManager` クラスからのものです。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-218">This example is from the `FixItQueueManager` class:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample15.cs)]

<span data-ttu-id="bd5f7-219">`async void` は、最上位レベルのイベントハンドラーに対してのみ使用してください。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-219">You should use `async void` only for top-level event handlers.</span></span> <span data-ttu-id="bd5f7-220">メソッドを `async void`として定義した場合、呼び出し元はメソッドを**待機**したり、メソッドがスローする例外をキャッチしたりすることはできません。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-220">If you define a method as `async void`, the caller cannot **await** the method or catch any exceptions the method throws.</span></span> <span data-ttu-id="bd5f7-221">詳細については、「[非同期プログラミングのベストプラクティス](https://msdn.microsoft.com/magazine/jj991977.aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-221">For more information, see [Best Practices in Asynchronous Programming](https://msdn.microsoft.com/magazine/jj991977.aspx).</span></span>

### <a name="use-a-cancellation-token-to-break-from-worker-role-loop"></a><span data-ttu-id="bd5f7-222">キャンセルトークンを使用してワーカーロールループを中断する</span><span class="sxs-lookup"><span data-stu-id="bd5f7-222">Use a cancellation token to break from worker role loop</span></span>

<span data-ttu-id="bd5f7-223">通常、ワーカーロールの**Run**メソッドには、無限ループが含まれています。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-223">Typically, the **Run** method on a worker role contains an infinite loop.</span></span> <span data-ttu-id="bd5f7-224">ワーカーロールが停止している場合は、 [Roleentrypoint. OnStop](https://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstop.aspx)メソッドが呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-224">When the worker role is stopping, the [RoleEntryPoint.OnStop](https://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstop.aspx) method is called.</span></span> <span data-ttu-id="bd5f7-225">このメソッドを使用して、Run メソッド内で**実行**されている作業を取り消し、正常に終了する必要があります。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-225">You should use this method to cancel the work that is being done inside the **Run** method and exit gracefully.</span></span> <span data-ttu-id="bd5f7-226">それ以外の場合、プロセスは操作の途中で終了します。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-226">Otherwise, the process might be terminated in the middle of an operation.</span></span>

### <a name="opt-out-of-automatic-mime-sniffing-procedure"></a><span data-ttu-id="bd5f7-227">自動 MIME スニッフィング手順のオプトアウト</span><span class="sxs-lookup"><span data-stu-id="bd5f7-227">Opt out of Automatic MIME Sniffing Procedure</span></span>

<span data-ttu-id="bd5f7-228">場合によっては、Internet Explorer によって、web サーバーで指定された種類とは異なる MIME の種類が報告されることがあります。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-228">In some cases, Internet Explorer reports a MIME type different than the type specified by the web server.</span></span> <span data-ttu-id="bd5f7-229">たとえば、Internet Explorer が HTTP 応答ヘッダーの Content-type: text/plain と共に配信されたファイル内の HTML コンテンツを検索した場合、Internet Explorer はコンテンツを HTML としてレンダリングする必要があると判断します。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-229">For instance, if Internet Explorer finds HTML content in a file delivered with the HTTP response header Content-Type: text/plain, Internet Explorer determines that the content should be rendered as HTML.</span></span> <span data-ttu-id="bd5f7-230">残念ながら、この "MIME スニッフィング" は、信頼されていないコンテンツをホストしているサーバーのセキュリティの問題につながる可能性もあります。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-230">Unfortunately, this "MIME-sniffing" can also lead to security problems for servers hosting untrusted content.</span></span> <span data-ttu-id="bd5f7-231">この問題に対処するために、Internet Explorer 8 は、MIME の種類の決定コードに多くの変更を加え、アプリケーション開発者が[mime スニッフィングをオプトアウト](https://blogs.msdn.com/b/ie/archive/2008/07/02/ie8-security-part-v-comprehensive-protection.aspx)することを許可しています。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-231">To combat this problem, Internet Explorer 8 has made a number of changes to MIME-type determination code and allows application developers to [opt out of MIME-sniffing](https://blogs.msdn.com/b/ie/archive/2008/07/02/ie8-security-part-v-comprehensive-protection.aspx).</span></span> <span data-ttu-id="bd5f7-232">次*のコードが web.config ファイルに*追加されました。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-232">The following code was added to the *Web.config* file.</span></span>

[!code-xml[Main](the-fix-it-sample-application/samples/sample16.xml?highlight=2-7)]

### <a name="enable-bundling-and-minification"></a><span data-ttu-id="bd5f7-233">バンドルと縮小を有効にする</span><span class="sxs-lookup"><span data-stu-id="bd5f7-233">Enable bundling and minification</span></span>

<span data-ttu-id="bd5f7-234">Visual Studio で新しい web プロジェクトを作成する場合、JavaScript ファイルのバンドルと縮小は既定では有効になっていません。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-234">When Visual Studio creates a new web project, bundling and minification of JavaScript files is not enabled by default.</span></span> <span data-ttu-id="bd5f7-235">BundleConfig.cs にコード行を追加しました。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-235">We added a line of code in BundleConfig.cs:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample17.cs?highlight=9)]

### <a name="set-an-expiration-time-out-for-authentication-cookies"></a><span data-ttu-id="bd5f7-236">認証 cookie の有効期限のタイムアウトを設定する</span><span class="sxs-lookup"><span data-stu-id="bd5f7-236">Set an expiration time-out for authentication cookies</span></span>

<span data-ttu-id="bd5f7-237">既定では、認証 cookie は2週間後に期限切れになります。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-237">By default, authentication cookies expire in two weeks.</span></span> <span data-ttu-id="bd5f7-238">より短い時間でより安全です。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-238">A shorter time is more secure.</span></span> <span data-ttu-id="bd5f7-239">*StartupAuth.cs*でこの設定を変更できます。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-239">You can change this setting in *StartupAuth.cs*:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample18.cs?highlight=4-5)]

<a id="run-in-vs"></a>
## <a name="how-to-run-the-app-from-visual-studio-on-your-local-computer"></a><span data-ttu-id="bd5f7-240">ローカルコンピューター上の Visual Studio からアプリを実行する方法</span><span class="sxs-lookup"><span data-stu-id="bd5f7-240">How to run the app from Visual Studio on your local computer</span></span>

<span data-ttu-id="bd5f7-241">Fix It アプリを実行するには、次の2つの方法があります。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-241">There are two ways to run the Fix It app:</span></span>

- <span data-ttu-id="bd5f7-242">新しいタスクを SQL データベースに直接書き込む基本アプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-242">Run the base application that writes new tasks directly to the SQL database.</span></span>
- <span data-ttu-id="bd5f7-243">キューとバックエンドサービスを使用してアプリケーションを実行し、タスクを作成します。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-243">Run the application using a queue plus a backend service to create tasks.</span></span> <span data-ttu-id="bd5f7-244">キューパターンについては、[キュー中心の作業パターン](queue-centric-work-pattern.md)の章を参照してください。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-244">The queue pattern is described in the chapter [Queue-Centric Work Pattern](queue-centric-work-pattern.md).</span></span>

<a id="runbase"></a>
### <a name="run-the-base-application"></a><span data-ttu-id="bd5f7-245">基本アプリケーションを実行する</span><span class="sxs-lookup"><span data-stu-id="bd5f7-245">Run the base application</span></span>

1. <span data-ttu-id="bd5f7-246">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)をインストールします。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-246">Install [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017).</span></span>
2. <span data-ttu-id="bd5f7-247">[AZURE SDK for .net For Visual Studio](https://azure.microsoft.com/downloads/)をインストールします。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-247">Install the [Azure SDK for .NET for Visual Studio](https://azure.microsoft.com/downloads/).</span></span>
3. <span data-ttu-id="bd5f7-248">[MSDN コードギャラリー](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)から .zip ファイルをダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-248">Download the .zip file from the [MSDN Code Gallery](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4).</span></span>
4. <span data-ttu-id="bd5f7-249">ファイルエクスプローラーで、.zip ファイルを右クリックし、[プロパティ] をクリックして、プロパティウィンドウ [ブロック解除] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-249">In File Explorer, right-click the .zip file and click Properties, then in the Properties window click Unblock.</span></span>
5. <span data-ttu-id="bd5f7-250">ファイルを解凍します。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-250">Unzip the file.</span></span>
6. <span data-ttu-id="bd5f7-251">.Sln ファイルをダブルクリックして、Visual Studio を起動します。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-251">Double-click the .sln file to launch Visual Studio.</span></span>
7. <span data-ttu-id="bd5f7-252">**[ツール]** メニューの **[NuGet パッケージマネージャー]** 、 **[パッケージマネージャーコンソール]** の順にクリックします。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-252">From the **Tools** menu, click **NuGet Package Manager**, then **Package Manager Console**.</span></span>
8. <span data-ttu-id="bd5f7-253">パッケージマネージャーコンソール (PMC) で、[復元] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-253">In the Package Manager Console (PMC), click Restore.</span></span>
9. <span data-ttu-id="bd5f7-254">Visual Studio を終了します。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-254">Exit Visual Studio.</span></span>
10. <span data-ttu-id="bd5f7-255">[Azure ストレージエミュレーター](/azure/storage/common/storage-use-emulator)を起動します。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-255">Start the [Azure storage emulator](/azure/storage/common/storage-use-emulator).</span></span>
11. <span data-ttu-id="bd5f7-256">Visual Studio を再起動し、前の手順で閉じたソリューションファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-256">Restart Visual Studio, opening the solution file you closed in the previous step.</span></span>
12. <span data-ttu-id="bd5f7-257">FixIt プロジェクトがスタートアッププロジェクトとして設定されていることを確認してから、CTRL キーを押しながら F5 キーを押してプロジェクトを実行します。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-257">Make sure the FixIt project is set as the startup project, and then press CTRL+F5 to run the project.</span></span>

<a id="queueslocal"></a>
### <a name="run-the-application-with-queue-processing"></a><span data-ttu-id="bd5f7-258">キュー処理でアプリケーションを実行する</span><span class="sxs-lookup"><span data-stu-id="bd5f7-258">Run the application with queue processing</span></span>

1. <span data-ttu-id="bd5f7-259">指示に従って[基本アプリケーションを実行](#runbase)し、ブラウザーを閉じて Visual Studio を閉じます。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-259">Follow the directions for [Run the base application](#runbase), and then close the browser and close Visual Studio.</span></span>
2. <span data-ttu-id="bd5f7-260">管理者特権で Visual Studio を起動します。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-260">Start Visual Studio with administrator privileges.</span></span> <span data-ttu-id="bd5f7-261">(Azure コンピューティングエミュレーターを使用し、管理者特権が必要です)。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-261">(You'll be using the Azure compute emulator, and that requires administrator privileges.)</span></span>
3. <span data-ttu-id="bd5f7-262">*Myfixit*プロジェクト (web プロジェクト) のアプリケーションの*web.config*ファイルで、`appSettings/UseQueues` の値を "true" に変更します。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-262">In the application *Web.config* file in the *MyFixIt* project (the web project), change the value of `appSettings/UseQueues` to "true":</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample19.cmd?highlight=3)]
4. <span data-ttu-id="bd5f7-263">[Azure ストレージエミュレーター](https://msdn.microsoft.com/library/windowsazure/hh403989.aspx)がまだ実行されていない場合は、もう一度開始します。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-263">If the [Azure storage emulator](https://msdn.microsoft.com/library/windowsazure/hh403989.aspx) isn't still running, start it again.</span></span>
5. <span data-ttu-id="bd5f7-264">FixIt web プロジェクトと MyFixItCloudService プロジェクトを同時に実行します。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-264">Run the FixIt web project and the MyFixItCloudService project simultaneously.</span></span>

    <span data-ttu-id="bd5f7-265">Visual Studio の使用:</span><span class="sxs-lookup"><span data-stu-id="bd5f7-265">Using Visual Studio:</span></span>

   1. <span data-ttu-id="bd5f7-266">**F5**キーを押して、FixIt プロジェクトを実行します。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-266">Press **F5** to run the FixIt project.</span></span>
   2. <span data-ttu-id="bd5f7-267">**ソリューションエクスプローラー**で、MyFixItCloudService プロジェクトを右クリックし、 **[デバッグ]**  >  **[新しいインスタンスを開始]** の順にクリックします。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-267">In **Solution Explorer**, right-click the MyFixItCloudService project, and then click **Debug** > **Start New Instance**.</span></span>

    <span data-ttu-id="bd5f7-268">Visual Studio 2013 Express for Web の使用:</span><span class="sxs-lookup"><span data-stu-id="bd5f7-268">Using Visual Studio 2013 Express for Web:</span></span>

   3. <span data-ttu-id="bd5f7-269">ソリューションエクスプローラーで、FixIt ソリューションを右クリックし、**プロパティ** を選択します。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-269">In Solution Explorer, right-click the FixIt solution and select **Properties**.</span></span>
   4. <span data-ttu-id="bd5f7-270">**[マルチスタートアッププロジェクト]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-270">Select **Multiple Startup Projects**.</span></span>
   5. <span data-ttu-id="bd5f7-271">MyFixIt と MyFixItCloudService の下の **アクション** ドロップダウンリストで、**開始** を選択します。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-271">In the **Action** dropdown list under MyFixIt and MyFixItCloudService, select **Start**.</span></span>
   6. <span data-ttu-id="bd5f7-272">**[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-272">Click **OK**.</span></span>
   7. <span data-ttu-id="bd5f7-273">**F5**キーを押して両方のプロジェクトを実行します。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-273">Press **F5** to run both projects.</span></span>

      <span data-ttu-id="bd5f7-274">MyFixItCloudService プロジェクトを実行すると、Visual Studio によって Azure コンピューティングエミュレーターが起動されます。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-274">When you run the MyFixItCloudService project, Visual Studio starts the Azure compute emulator.</span></span> <span data-ttu-id="bd5f7-275">ファイアウォールの構成によっては、エミュレーターをファイアウォールで許可することが必要になる場合があります。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-275">Depending on your firewall configuration, you might need to allow the emulator through the firewall.</span></span>

<a id="deploybase"></a>
## <a name="how-to-deploy-the-base-app-to-azure-app-service-web-apps-by-using-the-windows-powershell-scripts"></a><span data-ttu-id="bd5f7-276">Windows PowerShell スクリプトを使用して Azure App Service Web Apps に基本アプリを展開する方法</span><span class="sxs-lookup"><span data-stu-id="bd5f7-276">How to deploy the base app to Azure App Service Web Apps by using the Windows PowerShell scripts</span></span>

<span data-ttu-id="bd5f7-277">[すべてを自動化](automate-everything.md)するためのパターンを説明するために、Azure で環境を設定し、新しい環境にプロジェクトを配置するスクリプトを使用して、It アプリの修正を提供しています。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-277">To illustrate the [Automate Everything](automate-everything.md) pattern, the Fix It app is supplied with scripts that set up an environment in Azure and deploy the project to the new environment.</span></span> <span data-ttu-id="bd5f7-278">次の手順では、スクリプトの使用方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-278">The following instructions explain how to use the scripts.</span></span>

<span data-ttu-id="bd5f7-279">キューを使用せずに Azure で実行し、変更をキューでローカルに実行する場合は、次の手順に進む前に、UseQueues appSetting 値を false に戻すように設定してください。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-279">If you want to run in Azure without using queues, and you made the changes to run locally with queues, make sure you set the UseQueues appSetting value back to false before proceeding with the following instructions.</span></span>

<span data-ttu-id="bd5f7-280">この手順では、修正プログラムをダウンロードしてローカルで実行していること、および Azure アカウントを持っていること、または管理を許可されている Azure サブスクリプションを持っていることを前提としています。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-280">These instructions assume you have already downloaded and run the Fix It solution locally, and that you have an Azure account or have an Azure subscription that you are authorized to manage.</span></span>

1. <span data-ttu-id="bd5f7-281">**Azure PowerShell**コンソールをインストールします。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-281">Install the **Azure PowerShell** console.</span></span> <span data-ttu-id="bd5f7-282">手順については、「 [Azure PowerShell のインストールおよび構成方法](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-4.3.1)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-282">For instructions, see [How to install and configure Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-4.3.1).</span></span>

    <span data-ttu-id="bd5f7-283">このカスタマイズされたコンソールは、Azure サブスクリプションと連携するように構成されています。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-283">This customized console is configured to work with your Azure subscription.</span></span> <span data-ttu-id="bd5f7-284">Azure モジュールは*Program Files*ディレクトリにインストールされ、Azure PowerShell コンソールを使用するたびに自動的にインポートされます。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-284">The Azure module is installed in the *Program Files* directory and is automatically imported on every use of the Azure PowerShell console.</span></span>

    <span data-ttu-id="bd5f7-285">Windows PowerShell ISE など別のホストプログラムで作業する場合は、モジュールの[インポート](https://go.microsoft.com/fwlink/?LinkID=141553)コマンドレットを使用して azure モジュールをインポートするか、azure モジュールのコマンドを使用してモジュールの自動インポートをトリガーするようにしてください。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-285">If you prefer to work in a different host program, such as Windows PowerShell ISE, be sure to use the [Import-Module](https://go.microsoft.com/fwlink/?LinkID=141553) cmdlet to import the Azure module or use a command in the Azure module to trigger automatic importing of the module.</span></span>
2. <span data-ttu-id="bd5f7-286">**[管理者として実行]** オプションを使用して Azure PowerShell を開始します。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-286">Start Azure PowerShell with the **Run as administrator** option.</span></span>
3. <span data-ttu-id="bd5f7-287">[Set-executionpolicy](https://go.microsoft.com/fwlink/p/?linkid=293941)コマンドレットを実行して、Azure PowerShell 実行ポリシーを `RemoteSigned`に設定します。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-287">Run the [Set-ExecutionPolicy](https://go.microsoft.com/fwlink/p/?linkid=293941) cmdlet to set the Azure PowerShell execution policy to `RemoteSigned`.</span></span> <span data-ttu-id="bd5f7-288">ポリシーの変更を完了するには、「 **Y** 」 (はいの場合) を入力します。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-288">Enter **Y** (for Yes) to complete the policy change.</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample20.cmd)]

    <span data-ttu-id="bd5f7-289">この設定を使用すると、デジタル署名されていないローカルスクリプトを実行できます。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-289">This setting enables you to run local scripts that aren't digitally signed.</span></span> <span data-ttu-id="bd5f7-290">(実行ポリシーを `Unrestricted`に設定することもできます。これにより、後でブロック解除の手順が不要になりますが、セキュリティ上の理由から推奨されません。)</span><span class="sxs-lookup"><span data-stu-id="bd5f7-290">(You can also set the execution policy to `Unrestricted`, which would eliminate the need for the unblock step later, but this is not recommended for security reasons.)</span></span>
4. <span data-ttu-id="bd5f7-291">`Add-AzureAccount` コマンドレットを実行して、アカウントの資格情報を使用して PowerShell を設定します。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-291">Run the `Add-AzureAccount` cmdlet to set up PowerShell with credentials for your account.</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample21.cmd)]

    <span data-ttu-id="bd5f7-292">これらの資格情報は、一定の期間が経過すると期限切れになり、`Add-AzureAccount` コマンドレットを再実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-292">These credentials expire after a period of time and you have to re-run the `Add-AzureAccount` cmdlet.</span></span> <span data-ttu-id="bd5f7-293">この電子ブックが記述されているため、資格情報の有効期限が切れるまでの制限時間は12時間です。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-293">As this e-book is being written, the time limit before credentials expire is 12 hours.</span></span>
5. <span data-ttu-id="bd5f7-294">複数のサブスクリプションがある場合は、AzureSubscription コマンドレットを使用して、テスト環境を作成するサブスクリプションを指定します。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-294">If you have multiple subscriptions, use the Select-AzureSubscription cmdlet to specify the subscription you want to create the test environment in.</span></span>
6. <span data-ttu-id="bd5f7-295">`Get-AzurePublishSettingsFile` と `Import-AzurePublishSettingsFile` のコマンドレットを使用して、同じ Azure サブスクリプションの管理証明書をインポートします。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-295">Import a management certificate for the same Azure subscription by using the `Get-AzurePublishSettingsFile` and `Import-AzurePublishSettingsFile` cmdlets.</span></span> <span data-ttu-id="bd5f7-296">最初のコマンドレットでは、証明書ファイルをダウンロードし、2つ目のコマンドレットで、インポートするファイルの場所を指定します。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-296">The first of these cmdlets downloads a certificate file, and in the second one you specify the location of that file in order to import it.</span></span> > [!IMPORTANT]
   > <span data-ttu-id="bd5f7-297">ダウンロードしたファイルは、Azure サービスの管理に使用できる証明書が含まれているため、安全な場所に保管するか、または作業を終えたときに削除してください。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-297">Keep the downloaded file in a safe location or delete it when you're done with it, because it contains a certificate that can be used to manage your Azure services.</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample22.cmd)]

    <span data-ttu-id="bd5f7-298">この証明書は、SQL Database サーバーでファイアウォール規則を設定するために、開発用コンピューターの IP アドレスを検出する REST API 呼び出しに使用されます。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-298">The certificate is used for a REST API call that detects the development machine's IP address in order to set a firewall rule on the SQL Database server.</span></span>
7. <span data-ttu-id="bd5f7-299">[Set Location](https://go.microsoft.com/fwlink/p/?linkid=293912)コマンドレット (エイリアスは `cd`、`chdir`、および `sl`) を実行して、スクリプトが格納されているディレクトリに移動します。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-299">Run the [Set-Location](https://go.microsoft.com/fwlink/p/?linkid=293912) cmdlet (aliases are `cd`, `chdir`, and `sl`) to navigate to the directory that contains the scripts.</span></span> <span data-ttu-id="bd5f7-300">(これらのファイルは、[Fix It solution] フォルダーの [ *Automation* ] フォルダーにあります)。ディレクトリ名にスペースが含まれている場合は、パスを引用符で囲みます。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-300">(They're located in the *Automation* folder in the Fix It solution folder.) Put the path in quotes if any of the directory names contain spaces.</span></span> <span data-ttu-id="bd5f7-301">たとえば、`c:\Sample Apps\FixIt\Automation` ディレクトリに移動するには、次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-301">For example, to navigate to the `c:\Sample Apps\FixIt\Automation` directory you could enter the following command:</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample23.cmd)]
8. <span data-ttu-id="bd5f7-302">Windows PowerShell でこれらのスクリプトを実行できるようにするには、[ファイルのブロック解除](https://go.microsoft.com/fwlink/p/?linkid=294021)コマンドレットを使用します。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-302">To allow Windows PowerShell to run these scripts, use the [Unblock-File](https://go.microsoft.com/fwlink/p/?linkid=294021) cmdlet.</span></span> <span data-ttu-id="bd5f7-303">(スクリプトはインターネットからダウンロードされたためブロックされます)。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-303">(The scripts are blocked because they were downloaded from the Internet.)</span></span>

    > [!WARNING]
    > <span data-ttu-id="bd5f7-304">セキュリティ-任意のスクリプトまたは実行可能ファイルに対して `Unblock-File` を実行する前に、メモ帳でファイルを開き、コマンドを調べて、悪意のあるコードが含まれていないことを確認します。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-304">Security - Before running `Unblock-File` on any script or executable file, open the file in Notepad, examine the commands, and verify that they do not contain any malicious code.</span></span>

    <span data-ttu-id="bd5f7-305">たとえば、次のコマンドは、現在のディレクトリ内のすべてのスクリプトに対して `Unblock-File` コマンドレットを実行します。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-305">For example, the following command runs the `Unblock-File` cmdlet on all scripts in the current directory.</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample24.cmd)]
9. <span data-ttu-id="bd5f7-306">ベース (キューを処理しない) の web アプリを作成し、It アプリを修正するには、環境作成スクリプトを実行します。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-306">To create the web app for the base (no queues processing) Fix It app, run the environment creation script.</span></span>

    <span data-ttu-id="bd5f7-307">必須の `Name` パラメーターはデータベースの名前を指定し、スクリプトが作成するストレージアカウントにも使用されます。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-307">The required `Name` parameter specifies the name of the database and is also used for the storage account that the script creates.</span></span> <span data-ttu-id="bd5f7-308">名前は、azurewebsites.net ドメイン内でグローバルに一意である必要があります。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-308">The name must be globally unique within the azurewebsites.net domain.</span></span> <span data-ttu-id="bd5f7-309">Fixit やテストなどの一意でない名前を指定した場合 (または、fixitdemo の例でも同様)、`New-AzureWebsite` コマンドレットは、競合を報告する内部エラーで失敗します。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-309">If you specify a name that is not unique, like Fixit or Test (or even as in the example, fixitdemo), the `New-AzureWebsite` cmdlet fails with an Internal Error that reports a conflict.</span></span> <span data-ttu-id="bd5f7-310">このスクリプトは、web アプリ、ストレージアカウント、およびデータベースの名前の要件に準拠するために、名前をすべて小文字に変換します。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-310">The script converts the name to all lower-case to comply with name requirements for web apps, storage accounts, and databases.</span></span>

    <span data-ttu-id="bd5f7-311">必須の `SqlDatabasePassword` パラメーターは、SQL Database 用に作成される管理者アカウントのパスワードを指定します。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-311">The required `SqlDatabasePassword` parameter specifies the password for the admin account that will be created for SQL Database.</span></span> <span data-ttu-id="bd5f7-312">パスワード (&amp; &lt; &gt;;) には特殊な XML 文字を含めないでください。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-312">Don't include special XML characters in the password (&amp; &lt; &gt; ;).</span></span> <span data-ttu-id="bd5f7-313">これは、Azure の制限ではなく、スクリプトの記述方法に関する制限事項です。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-313">This is a limitation of the way the scripts were written, not a limitation of Azure.</span></span>

    <span data-ttu-id="bd5f7-314">たとえば、"fixitdemo" という名前の web アプリを作成し、"Passw0rd1" という SQL Server 管理者パスワードを使用する場合は、次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-314">For example, if you want to create a web app named "fixitdemo" and use a SQL Server administrator password of "Passw0rd1", you could enter the following command:</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample25.cmd)]

    <span data-ttu-id="bd5f7-315">名前は azurewebsites.net ドメイン内で一意である必要があり、パスワードは、パスワードの複雑さの SQL Database 要件を満たしている必要があります。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-315">The name must be unique in the azurewebsites.net domain, and the password must meet SQL Database requirements for password complexity.</span></span> <span data-ttu-id="bd5f7-316">(例 Passw0rd1 は要件を満たしています)。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-316">(The example Passw0rd1 does meet the requirements.)</span></span>

    <span data-ttu-id="bd5f7-317">コマンドの先頭が "であることに注意してください。\"。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-317">Note that the command begins with ".\".</span></span> <span data-ttu-id="bd5f7-318">スクリプトの悪意のある実行を防ぐために、Windows PowerShell では、スクリプトの実行時にスクリプトファイルへの完全修飾パスを指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-318">To help prevent malicious execution of scripts, Windows PowerShell requires that you provide the fully qualified path to the script file when you run a script.</span></span> <span data-ttu-id="bd5f7-319">ドットを使用して、現在のディレクトリ (") を示すことができます。\") または完全修飾パスを指定します。次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-319">You can use a dot to indicate the current directory (".\") or provide the fully qualified path, such as:</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample26.cmd)]

    <span data-ttu-id="bd5f7-320">スクリプトの詳細については、`Get-Help` コマンドレットを使用してください。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-320">For more information about the script, use the `Get-Help` cmdlet.</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample27.cmd)]

    <span data-ttu-id="bd5f7-321">Get-help コマンドレットの `Detailed`、`Full`、`Parameters`、および `Examples` パラメーターを使用して、返されるヘルプをフィルター処理できます。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-321">You can use the `Detailed`, `Full`, `Parameters`, and `Examples` parameters of the Get-Help cmdlet to filter the help that is returned.</span></span>

    <span data-ttu-id="bd5f7-322">スクリプトが失敗した場合、またはエラーが発生した場合 ("New-AzureWebsite: Call Set-Azurewebsite and Select-Azurewebsite first" など)、Azure PowerShell の構成が完了していない可能性があります。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-322">If the script fails or generates errors, such as "New-AzureWebsite : Call Set-AzureSubscription and Select-AzureSubscription first," you might not have completed the configuration of Azure PowerShell.</span></span>

    <span data-ttu-id="bd5f7-323">スクリプトが完了したら、[[すべて自動化](automate-everything.md)] の章に示されているように、Azure 管理ポータルを使用して、作成されたリソースを確認できます。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-323">After the script finishes, you can use the Azure Management Portal to see the resources that were created, as shown in the [Automate Everything](automate-everything.md) chapter.</span></span>
10. <span data-ttu-id="bd5f7-324">新しい Azure 環境に FixIt プロジェクトをデプロイするには、 *Azurewebsite. ps1*スクリプトを使用します。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-324">To deploy the FixIt project to the new Azure environment, use the *AzureWebsite.ps1* script.</span></span> <span data-ttu-id="bd5f7-325">例:</span><span class="sxs-lookup"><span data-stu-id="bd5f7-325">For example:</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample28.cmd)]

    <span data-ttu-id="bd5f7-326">デプロイが完了すると、Azure で実行されている修正プログラムを使用してブラウザーが開きます。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-326">When deployment is done, the browser opens with Fix It running in Azure.</span></span>

<a id="troubleshooting"></a>
## <a name="troubleshooting-the-windows-powershell-scripts"></a><span data-ttu-id="bd5f7-327">Windows PowerShell スクリプトのトラブルシューティング</span><span class="sxs-lookup"><span data-stu-id="bd5f7-327">Troubleshooting the Windows PowerShell scripts</span></span>

<span data-ttu-id="bd5f7-328">これらのスクリプトを実行するときに発生する最も一般的なエラーは、権限に関連しています。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-328">The most common errors encountered when running these scripts are related to permissions.</span></span> <span data-ttu-id="bd5f7-329">`Add-AzureAccount` と `Import-AzurePublishSettingsFile` が正常に完了し、同じ Azure サブスクリプションで使用されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-329">Make sure that `Add-AzureAccount` and `Import-AzurePublishSettingsFile` were successful and that you used them for the same Azure subscription.</span></span> <span data-ttu-id="bd5f7-330">`Add-AzureAccount` が成功した場合でも、再実行する必要がある場合があります。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-330">Even if `Add-AzureAccount` was successful you might have to run it again.</span></span> <span data-ttu-id="bd5f7-331">`Add-AzureAccount` によって追加されたアクセス許可は、12時間後に有効期限が切れます。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-331">The permissions added by `Add-AzureAccount` expire in 12 hours.</span></span>

### <a name="object-reference-not-set-to-an-instance-of-an-object"></a><span data-ttu-id="bd5f7-332">オブジェクト参照がオブジェクト インスタンスに設定されていません。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-332">Object reference not set to an instance of an object.</span></span>

<span data-ttu-id="bd5f7-333">スクリプトから "オブジェクト参照がオブジェクトのインスタンスに設定されていません" などのエラーが返された場合は、Windows PowerShell が処理するオブジェクトを見つけられない (これは null 参照例外である) ため、`Add-AzureAccount` コマンドレットを実行して、スクリプトをもう一度実行します。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-333">If the script returns errors, such as "Object reference not set to an instance of an object," which means that Windows PowerShell can't find an object to process (this is a null reference exception), run the `Add-AzureAccount` cmdlet and try the script again.</span></span>

[!code-console[Main](the-fix-it-sample-application/samples/sample29.cmd)]

### <a name="internalerror-the-server-encountered-an-internal-error"></a><span data-ttu-id="bd5f7-334">InternalError: サーバーで内部エラーが発生しました。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-334">InternalError: The server encountered an internal error.</span></span>

<span data-ttu-id="bd5f7-335">`New-AzureWebsite` コマンドレットは、名前が azurewebsites.net ドメイン内で一意でない場合に内部エラーを返します。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-335">The `New-AzureWebsite` cmdlet returns an internal error when the name is not unique in the azurewebsites.net domain.</span></span> <span data-ttu-id="bd5f7-336">このエラーを解決するには、名前に別の値を使用します。これは、 *New-AzureWebsiteEnv*の name パラメーターに含まれています。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-336">To resolve the error, use a different value for the name, which is in the Name parameter of *New-AzureWebsiteEnv.ps1*.</span></span>

[!code-console[Main](the-fix-it-sample-application/samples/sample30.cmd)]

### <a name="restarting-the-script"></a><span data-ttu-id="bd5f7-337">スクリプトを再起動しています</span><span class="sxs-lookup"><span data-stu-id="bd5f7-337">Restarting the script</span></span>

<span data-ttu-id="bd5f7-338">"スクリプトが完了しました" というメッセージが出力される前に失敗したために*New-AzureWebsiteEnv*スクリプトを再起動する必要がある場合は、スクリプトが停止する前に作成したリソースを削除することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-338">If you need to restart the *New-AzureWebsiteEnv.ps1* script because it failed before it printed the "Script is complete" message, you might want to delete resources that the script created before it stopped.</span></span> <span data-ttu-id="bd5f7-339">たとえば、スクリプトによって ContosoFixItDemo web アプリが既に作成されていて、同じ名前でスクリプトを再度実行した場合、その名前は使用中であるため、スクリプトは失敗します。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-339">For example, if the script already created the ContosoFixItDemo web app and you run the script again with the same name, the script will fail because the name is in use.</span></span>

<span data-ttu-id="bd5f7-340">スクリプトが作成されたリソースを停止する前に確認するには、次のコマンドレットを使用します。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-340">To determine which resources the script created before it stopped, use the following cmdlets:</span></span>

- `Get-AzureWebsite`
- `Get-AzureSqlDatabaseServer`
- <span data-ttu-id="bd5f7-341">`Get-AzureSqlDatabase`: このコマンドレットを実行するには、データベースサーバー名をパイプで `Get-AzureSqlDatabase`: `Get-AzureSqlDatabaseServer | Get-AzureSqlDatabase.`</span><span class="sxs-lookup"><span data-stu-id="bd5f7-341">`Get-AzureSqlDatabase`: To run this cmdlet, pipe the database server name to `Get-AzureSqlDatabase`:   `Get-AzureSqlDatabaseServer | Get-AzureSqlDatabase.`</span></span>

<span data-ttu-id="bd5f7-342">これらのリソースを削除するには、次のコマンドを使用します。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-342">To delete these resources, use the following commands.</span></span> <span data-ttu-id="bd5f7-343">データベースサーバーを削除すると、サーバーに関連付けられているデータベースが自動的に削除されることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-343">Note that if you delete the database server, you automatically delete the databases associated with the server.</span></span>

- `Get-AzureWebsite -Name <WebsiteName> | Remove-AzureWebsite`
- `Get-AzureSqlDatabase -Name <DatabaseName> -ServerName <DatabaseServerName> | Remove-SqlAzureDatabase`
- `Get-AzureSqlDatabaseServer | Remove-AzureSqlDatabaseServer`

<a id="deployqueues"></a>
## <a name="how-to-deploy-the-app-with-queue-processing-to-azure-app-service-web-apps-and-an-azure-cloud-service"></a><span data-ttu-id="bd5f7-344">キュー処理を使用してアプリを Azure App Service Web Apps と Azure クラウドサービスにデプロイする方法</span><span class="sxs-lookup"><span data-stu-id="bd5f7-344">How to deploy the app with queue processing to Azure App Service Web Apps and an Azure Cloud Service</span></span>

<span data-ttu-id="bd5f7-345">キューを有効にするには、myfixitconfiguration ファイルで次の変更を行います。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-345">To enable queues, make the following change in the MyFixIt\Web.config file.</span></span> <span data-ttu-id="bd5f7-346">`appSettings`で、`UseQueues` の値を "true" に変更します。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-346">Under `appSettings`, change the value of `UseQueues` to "true":</span></span>

[!code-xml[Main](the-fix-it-sample-application/samples/sample31.xml)]

<span data-ttu-id="bd5f7-347">次に、[前述](#deploybase)のように AZURE APP SERVICE で MVC アプリケーションを web アプリにデプロイします。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-347">Then deploy the MVC application to an web app in Azure App Service, as described [earlier](#deploybase).</span></span>

<span data-ttu-id="bd5f7-348">次に、新しい Azure クラウドサービスを作成します。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-348">Next, create a new Azure cloud service.</span></span> <span data-ttu-id="bd5f7-349">Fix It アプリに含まれているスクリプトは、クラウドサービスを作成またはデプロイしません。そのため、このために Azure portal を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-349">The scripts included with the Fix It app do not create or deploy the cloud service, so you must use Azure portal for this.</span></span> <span data-ttu-id="bd5f7-350">ポータルで、 **[新規]**  -- [ **Compute** – **Cloud Service** -- **簡易作成**] の順にクリックし、URL とデータセンターの場所を入力します。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-350">In the portal, click **New** -- **Compute** – **Cloud Service** -- **Quick Create**, and then enter a URL and a data center location.</span></span> <span data-ttu-id="bd5f7-351">Web アプリをデプロイしたのと同じデータセンターを使用します。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-351">Use the same data center where you deployed the web app.</span></span>

![](the-fix-it-sample-application/_static/image1.png)

<span data-ttu-id="bd5f7-352">クラウドサービスをデプロイする前に、構成ファイルの一部を更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-352">Before you can deploy the cloud service, you need to update some of the configuration files.</span></span>

<span data-ttu-id="bd5f7-353">MyFixIt の `connectionStrings`の下で、`appdb` 接続文字列の値を、SQL Database の実際の接続文字列に変更します。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-353">In MyFixIt.WorkerRole\app.config, under `connectionStrings`, replace the value of the `appdb` connection string with the actual connection string for the SQL Database.</span></span> <span data-ttu-id="bd5f7-354">ポータルから接続文字列を取得できます。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-354">You can get the connection string from the portal.</span></span> <span data-ttu-id="bd5f7-355">ポータルで、 **[SQL データベース]** をクリックして - **APPDB** - **ADO .net、ODBC、PHP、JDBC の接続文字列を表示 SQL Database**ます。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-355">In the portal, click **SQL Databases** - **appdb** - **View SQL Database connection strings for ADO .Net, ODBC, PHP, and JDBC**.</span></span> <span data-ttu-id="bd5f7-356">ADO.NET 接続文字列をコピーし、app.config ファイルに値を貼り付けます。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-356">Copy the ADO.NET connection string and paste the value into the app.config file.</span></span> <span data-ttu-id="bd5f7-357">"{Your\_password\_here}" をデータベースのパスワードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-357">Replace "{your\_password\_here}" with your database password.</span></span> <span data-ttu-id="bd5f7-358">(MVC アプリのデプロイにスクリプトを使用したと仮定した場合は、`SqlDatabasePassword` スクリプトパラメーターにデータベースパスワードを指定しています)。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-358">(Assuming you used the scripts to deploy the MVC app, you specified the database password in the `SqlDatabasePassword` script parameter.)</span></span>

<span data-ttu-id="bd5f7-359">結果は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-359">The result should look like the following:</span></span>

[!code-xml[Main](the-fix-it-sample-application/samples/sample32.xml)]

<span data-ttu-id="bd5f7-360">同じ MyFixIt ファイルで、[`appSettings`] の下にある Azure ストレージアカウントの2つのプレースホルダーの値を置き換えます。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-360">In the same MyFixIt.WorkerRole\app.config file, under `appSettings`, replace the two placeholder values for the Azure storage account.</span></span>

[!code-xml[Main](the-fix-it-sample-application/samples/sample33.xml?highlight=2-3)]

<span data-ttu-id="bd5f7-361">ポータルからアクセスキーを取得できます。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-361">You can get the access key from the portal.</span></span> <span data-ttu-id="bd5f7-362">「[ストレージアカウントの管理方法」を](https://docs.microsoft.com/azure/storage/common/storage-create-storage-account)参照してください。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-362">See [How To Manage Storage Accounts](https://docs.microsoft.com/azure/storage/common/storage-create-storage-account).</span></span>

<span data-ttu-id="bd5f7-363">MyFixItCloudService\ServiceConfiguration.Cloud.cscfg で、Azure ストレージアカウントの2つのプレースホルダーの値を置き換えます。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-363">In MyFixItCloudService\ServiceConfiguration.Cloud.cscfg, replace the same two placeholders values for the Azure storage account.</span></span>

[!code-xml[Main](the-fix-it-sample-application/samples/sample34.xml?highlight=3)]

<span data-ttu-id="bd5f7-364">これで、クラウドサービスをデプロイする準備が整いました。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-364">Now you are ready to deploy the cloud service.</span></span> <span data-ttu-id="bd5f7-365">ソリューションエクスプローラーで、MyFixItCloudService プロジェクトを右クリックし、 **[発行]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-365">In Solution Explore, right-click the MyFixItCloudService project and select **Publish**.</span></span> <span data-ttu-id="bd5f7-366">詳細については、[このチュートリアル](https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36)のパート2の「[Azure へのアプリケーションのデプロイ](https://www.windowsazure.com/develop/net/tutorials/multi-tier-web-site/2-download-and-run/#deployAz)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="bd5f7-366">For more information, see "[Deploy the Application to Azure](https://www.windowsazure.com/develop/net/tutorials/multi-tier-web-site/2-download-and-run/#deployAz)", which is in part 2 of [this tutorial](https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36).</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="bd5f7-367">前へ</span><span class="sxs-lookup"><span data-stu-id="bd5f7-367">Previous</span></span>](more-patterns-and-guidance.md)
