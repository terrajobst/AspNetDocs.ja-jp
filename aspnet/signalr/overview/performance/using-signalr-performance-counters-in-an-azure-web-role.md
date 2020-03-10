---
uid: signalr/overview/performance/using-signalr-performance-counters-in-an-azure-web-role
title: Azure の Web ロールで SignalR パフォーマンスカウンターを使用する |Microsoft Docs
author: guardrex
description: Azure の Web ロールに SignalR パフォーマンスカウンターをインストールして使用する方法について説明します。
keywords: ASP .NET、signalr、パフォーマンスカウンター、azure web ロール
ms.author: bradyg
ms.date: 10/03/2018
ms.assetid: 2a127d3b-21ed-4cc9-bec0-cdab4e742a25
msc.legacyurl: /signalr/overview/performance/using-signalr-performance-counters-in-an-azure-web-role
msc.type: authoredcontent
ms.openlocfilehash: 969a2ce43a7cb8d649555daf282f900401c0c914
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467566"
---
# <a name="using-signalr-performance-counters-in-an-azure-web-role"></a><span data-ttu-id="5d46f-104">Azure の Web ロールで SignalR パフォーマンスカウンターを使用する</span><span class="sxs-lookup"><span data-stu-id="5d46f-104">Using SignalR performance counters in an Azure Web Role</span></span>

<span data-ttu-id="5d46f-105">作成者: [Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="5d46f-105">By [Luke Latham](https://github.com/guardrex)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

<span data-ttu-id="5d46f-106">SignalR パフォーマンスカウンターは、Azure の Web ロールでアプリのパフォーマンスを監視するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="5d46f-106">SignalR performance counters are used to monitor your app's performance in an Azure Web Role.</span></span> <span data-ttu-id="5d46f-107">カウンターは Microsoft Azure 診断によってキャプチャされます。</span><span class="sxs-lookup"><span data-stu-id="5d46f-107">The counters are captured by Microsoft Azure Diagnostics.</span></span> <span data-ttu-id="5d46f-108">SignalR パフォーマンスカウンターは、スタンドアロンまたはオンプレミスのアプリと同じツールである*SignalR*を使用して Azure にインストールします。</span><span class="sxs-lookup"><span data-stu-id="5d46f-108">You install SignalR performance counters on Azure with *signalr.exe*, the same tool used for standalone or on-premises apps.</span></span> <span data-ttu-id="5d46f-109">Azure ロールは一時的なものであるため、スタートアップ時に SignalR パフォーマンスカウンターをインストールして登録するようにアプリを構成します。</span><span class="sxs-lookup"><span data-stu-id="5d46f-109">Since Azure roles are transient, you configure an app to install and register SignalR performance counters upon startup.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5d46f-110">前提条件</span><span class="sxs-lookup"><span data-stu-id="5d46f-110">Prerequisites</span></span>

* <span data-ttu-id="5d46f-111">Visual Studio 2015 または[2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)</span><span class="sxs-lookup"><span data-stu-id="5d46f-111">Visual Studio 2015 or [2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)</span></span>
* <span data-ttu-id="5d46f-112">[MICROSOFT AZURE sdk For Visual Studio](https://azure.microsoft.com/downloads/) **メモ: sdk のインストール後にコンピューターを再起動します。**</span><span class="sxs-lookup"><span data-stu-id="5d46f-112">[Microsoft Azure SDK for Visual Studio](https://azure.microsoft.com/downloads/) **Note: Restart your machine after installing the SDK.**</span></span>
* <span data-ttu-id="5d46f-113">Microsoft Azure サブスクリプション: 無料の Azure 試用版アカウントにサインアップするには、「 [Azure 無料試用版](https://azure.microsoft.com/free/)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5d46f-113">Microsoft Azure subscription: To sign up for a free Azure trial account, see [Azure Free Trial](https://azure.microsoft.com/free/).</span></span>

## <a name="creating-an-azure-web-role-application-that-exposes-signalr-performance-counters"></a><span data-ttu-id="5d46f-114">SignalR パフォーマンスカウンターを公開する Azure Web ロールアプリケーションの作成</span><span class="sxs-lookup"><span data-stu-id="5d46f-114">Creating an Azure Web Role application that exposes SignalR performance counters</span></span>

1. <span data-ttu-id="5d46f-115">Visual Studio を開きます。</span><span class="sxs-lookup"><span data-stu-id="5d46f-115">Open Visual Studio.</span></span>

2. <span data-ttu-id="5d46f-116">Visual Studio で、 **[ファイル]**  >  **[新規]**  >  **[プロジェクト]** の順に選択します。</span><span class="sxs-lookup"><span data-stu-id="5d46f-116">In Visual Studio, select **File** > **New** > **Project**.</span></span>

3. <span data-ttu-id="5d46f-117">**[新しいプロジェクト]** ダイアログボックスで、左側にある [ **Visual C#**  > **cloud** ] カテゴリを選択し、 **[Azure cloud services]** テンプレートを選択します。</span><span class="sxs-lookup"><span data-stu-id="5d46f-117">In the **New Project** dialog box, select the **Visual C#** > **Cloud** category on the left, and then select the **Azure Cloud Service** template.</span></span> <span data-ttu-id="5d46f-118">アプリに**SignalRPerfCounters**という名前を指定し、[ **OK]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="5d46f-118">Name the app **SignalRPerfCounters** and select **OK**.</span></span>

   ![新しいクラウドアプリケーション](using-signalr-performance-counters-in-an-azure-web-role/_static/image1.png)

   > [!NOTE]
   > <span data-ttu-id="5d46f-120">**クラウド**テンプレートカテゴリまたは**azure クラウドサービス**テンプレートが表示されない場合は、Visual Studio 2017 の**Azure 開発**ワークロードをインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="5d46f-120">If you don't see the **Cloud** template category or the **Azure Cloud Service** template, you need to install the **Azure development** workload for Visual Studio 2017.</span></span> <span data-ttu-id="5d46f-121">**[新しいプロジェクト]** ダイアログの左下にある **[Visual Studio インストーラーを開く]** リンクをクリックして Visual Studio インストーラーを開きます。</span><span class="sxs-lookup"><span data-stu-id="5d46f-121">Choose the **Open Visual Studio Installer** link on the bottom-left side of the **New Project** dialog to open Visual Studio Installer.</span></span> <span data-ttu-id="5d46f-122">**Azure 開発**ワークロードを選択し、 **[変更]** を選択して、ワークロードのインストールを開始します。</span><span class="sxs-lookup"><span data-stu-id="5d46f-122">Select the **Azure development** workload, and then choose **Modify** to start installing the workload.</span></span>
   >
   > ![Visual Studio インストーラーでの Azure 開発ワークロード](using-signalr-performance-counters-in-an-azure-web-role/_static/azure-development-workload.png)

4. <span data-ttu-id="5d46f-124">**[新しい Microsoft Azure クラウドサービス]** ダイアログで **[ASP.NET Web Role]** を選択し、[>] をクリックして、プロジェクトにロールを追加します。</span><span class="sxs-lookup"><span data-stu-id="5d46f-124">In the **New Microsoft Azure Cloud Service** dialog, select **ASP.NET Web Role** and select the > button to add the role to the project.</span></span> <span data-ttu-id="5d46f-125">**[OK]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="5d46f-125">Select **OK**.</span></span>

   ![ASP.NET Web ロールの追加](using-signalr-performance-counters-in-an-azure-web-role/_static/image2.png)

5. <span data-ttu-id="5d46f-127">**[New ASP.NET Web Application-WebRole1]** ダイアログボックスで、 **[MVC]** テンプレートを選択し、[ **OK]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="5d46f-127">In the **New ASP.NET Web Application - WebRole1** dialog, select the **MVC** template, and then select **OK**.</span></span>

   ![MVC と Web API の追加](using-signalr-performance-counters-in-an-azure-web-role/_static/image3.png)

6. <span data-ttu-id="5d46f-129">**ソリューションエクスプローラー**で、 **WebRole1**の下の*diagnostics.wadcfgx*ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="5d46f-129">In **Solution Explorer**, open the *diagnostics.wadcfgx* file under **WebRole1**.</span></span>

   ![ソリューションエクスプローラー diagnostics.wadcfgx](using-signalr-performance-counters-in-an-azure-web-role/_static/image4.png)

7. <span data-ttu-id="5d46f-131">ファイルの内容を次の構成に置き換え、ファイルを保存します。</span><span class="sxs-lookup"><span data-stu-id="5d46f-131">Replace the contents of the file with the following configuration and save the file:</span></span>

   [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample1.xml)]

8. <span data-ttu-id="5d46f-132">[**ツール** > **NuGet パッケージマネージャー**] から**パッケージマネージャーコンソール**を開きます。</span><span class="sxs-lookup"><span data-stu-id="5d46f-132">Open the **Package Manager Console** from **Tools** > **NuGet Package Manager**.</span></span> <span data-ttu-id="5d46f-133">次のコマンドを入力して、最新バージョンの SignalR および SignalR utilities パッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="5d46f-133">Enter the following commands to install the latest version of SignalR and the SignalR utilities package:</span></span>

   [!code-powershell[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample2.ps1)]

9. <span data-ttu-id="5d46f-134">SignalR パフォーマンスカウンターを起動またはリサイクルするときに、ロールインスタンスにインストールするようにアプリを構成します。</span><span class="sxs-lookup"><span data-stu-id="5d46f-134">Configure the app to install the SignalR performance counters into the role instance when it starts up or recycles.</span></span> <span data-ttu-id="5d46f-135">**ソリューションエクスプローラー**で、 **WebRole1**プロジェクトを右クリックし、[ > **新しいフォルダー**の**追加**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="5d46f-135">In **Solution Explorer**, right-click on the **WebRole1** project and select **Add** > **New Folder**.</span></span> <span data-ttu-id="5d46f-136">新しいフォルダーに「*スタートアップ*」という名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="5d46f-136">Name the new folder *Startup*.</span></span>

   ![スタートアップフォルダーの追加](using-signalr-performance-counters-in-an-azure-web-role/_static/image5.png)

10. <span data-ttu-id="5d46f-138">\<のプロジェクトフォルダー >/SignalRPerfCounters/packages/Microsoft.AspNet.SignalR.Utils. から*signalr*ファイル ( **signalr**パッケージで追加) をコピーします。前の手順で作成した*スタートアップ*フォルダーにバージョン >/ツールを\<します。</span><span class="sxs-lookup"><span data-stu-id="5d46f-138">Copy the *signalr.exe* file (added with the **Microsoft.AspNet.SignalR.Utils** package) from \<project folder>/SignalRPerfCounters/packages/Microsoft.AspNet.SignalR.Utils.\<version>/tools to the *Startup* folder you created in the previous step.</span></span>

11. <span data-ttu-id="5d46f-139">**ソリューションエクスプローラー**で、[*スタートアップ*] フォルダーを右クリックし、[**既存の項目**の**追加** > ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="5d46f-139">In **Solution Explorer**, right-click the *Startup* folder and select **Add** > **Existing Item**.</span></span> <span data-ttu-id="5d46f-140">表示されるダイアログで、[ *signalr* ] を選択し、 **[追加]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="5d46f-140">In the dialog that appears, select *signalr.exe* and select **Add**.</span></span>

    ![Signalr をプロジェクトに追加する](using-signalr-performance-counters-in-an-azure-web-role/_static/image6.png)

12. <span data-ttu-id="5d46f-142">作成した*スタートアップ*フォルダーを右クリックします。</span><span class="sxs-lookup"><span data-stu-id="5d46f-142">Right-click on the *Startup* folder you created.</span></span> <span data-ttu-id="5d46f-143">**[追加]**  >  **[新しい項目]** の順に選択します。</span><span class="sxs-lookup"><span data-stu-id="5d46f-143">Select **Add** > **New Item**.</span></span> <span data-ttu-id="5d46f-144">**[全般]** ノードを選択し、 **[テキストファイル]** を選択して、新しい項目に「 *signalrperfcounterinstall. cmd*」という名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="5d46f-144">Select the **General** node, select **Text File**, and name the new item *SignalRPerfCounterInstall.cmd*.</span></span> <span data-ttu-id="5d46f-145">このコマンドファイルは、SignalR パフォーマンスカウンターを web ロールにインストールします。</span><span class="sxs-lookup"><span data-stu-id="5d46f-145">This command file will install the SignalR performance counters into the web role.</span></span>

    ![SignalR パフォーマンスカウンターのインストールバッチファイルの作成](using-signalr-performance-counters-in-an-azure-web-role/_static/image7.png)

13. <span data-ttu-id="5d46f-147">Visual Studio によって*Signalrperfcounterinstall .cmd*ファイルが作成されると、自動的にメインウィンドウに表示されます。</span><span class="sxs-lookup"><span data-stu-id="5d46f-147">When Visual Studio creates the *SignalRPerfCounterInstall.cmd* file, it will automatically open in the main window.</span></span> <span data-ttu-id="5d46f-148">ファイルの内容を次のスクリプトに置き換え、ファイルを保存して閉じます。</span><span class="sxs-lookup"><span data-stu-id="5d46f-148">Replace the contents of the file with the following script, then save and close the file.</span></span> <span data-ttu-id="5d46f-149">このスクリプトは、signalr を実行し*ます*。これにより、signalr パフォーマンスカウンターがロールインスタンスに追加されます。</span><span class="sxs-lookup"><span data-stu-id="5d46f-149">This script executes *signalr.exe*, which adds the SignalR performance counters to the role instance.</span></span>

    [!code-console[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample3.cmd)]

14. <span data-ttu-id="5d46f-150">**ソリューションエクスプローラー**で*signalr*ファイルを選択します。</span><span class="sxs-lookup"><span data-stu-id="5d46f-150">Select the *signalr.exe* file in **Solution Explorer**.</span></span> <span data-ttu-id="5d46f-151">ファイルの**プロパティ**で、 **[出力ディレクトリにコピー]** を **[常にコピー]** する に設定します。</span><span class="sxs-lookup"><span data-stu-id="5d46f-151">In the file's **Properties**, set **Copy to Output Directory** to **Copy Always**.</span></span>

    ![出力ディレクトリにコピーするように設定する (常にコピーする)](using-signalr-performance-counters-in-an-azure-web-role/_static/image8.png)

15. <span data-ttu-id="5d46f-153">前の手順を繰り返して、 *Signalrperfcounterinstall. .cmd*ファイルを実行します。</span><span class="sxs-lookup"><span data-stu-id="5d46f-153">Repeat the previous step for the *SignalRPerfCounterInstall.cmd* file.</span></span>

16. <span data-ttu-id="5d46f-154">*Signalrperfcounterinstall. .cmd*ファイルを右クリックし、[ファイル**を開くアプリケーション**の選択] を選択します。</span><span class="sxs-lookup"><span data-stu-id="5d46f-154">Right-click on the *SignalRPerfCounterInstall.cmd* file and select **Open With**.</span></span> <span data-ttu-id="5d46f-155">表示されるダイアログで、 **[バイナリエディター]** を選択し、[ **OK]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="5d46f-155">In the dialog that appears, select **Binary Editor** and select **OK**.</span></span>

    ![バイナリエディターで開く](using-signalr-performance-counters-in-an-azure-web-role/_static/image9.png)

17. <span data-ttu-id="5d46f-157">バイナリエディターで、ファイル内の先頭バイトを選択して削除します。</span><span class="sxs-lookup"><span data-stu-id="5d46f-157">In the binary editor, select any leading bytes in the file and delete them.</span></span> <span data-ttu-id="5d46f-158">ファイルを保存して閉じます。</span><span class="sxs-lookup"><span data-stu-id="5d46f-158">Save and close the file.</span></span>

    ![先頭バイトの削除](using-signalr-performance-counters-in-an-azure-web-role/_static/image10.png)

18. <span data-ttu-id="5d46f-160">サービスの開始時に、 *Servicedefinition*を開き、 *Signalrperfcounterinstall. .cmd*ファイルを実行するスタートアップタスクを追加します。</span><span class="sxs-lookup"><span data-stu-id="5d46f-160">Open *ServiceDefinition.csdef* and add a startup task that executes the *SignalrPerfCounterInstall.cmd* file when the service starts up:</span></span>

    [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample4.xml?highlight=4-7)]

19. <span data-ttu-id="5d46f-161">`Views/Shared/_Layout.cshtml` を開き、ファイルの末尾から jQuery バンドルスクリプトを削除します。</span><span class="sxs-lookup"><span data-stu-id="5d46f-161">Open `Views/Shared/_Layout.cshtml` and remove the jQuery bundle script from the end of the file.</span></span>

    [!code-cshtml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample5.cshtml)]

20. <span data-ttu-id="5d46f-162">サーバーで `increment` メソッドを連続して呼び出す JavaScript クライアントを追加します。</span><span class="sxs-lookup"><span data-stu-id="5d46f-162">Add a JavaScript client that continuously calls the `increment` method on the server.</span></span> <span data-ttu-id="5d46f-163">`Views/Home/Index.cshtml` を開き、内容を次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="5d46f-163">Open `Views/Home/Index.cshtml` and replace the contents with the following code:</span></span>

    [!code-cshtml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample6.cshtml)]

21. <span data-ttu-id="5d46f-164">*ハブ*という名前の**WebRole1**プロジェクトに新しいフォルダーを作成します。</span><span class="sxs-lookup"><span data-stu-id="5d46f-164">Create a new folder in the **WebRole1** project named *Hubs*.</span></span> <span data-ttu-id="5d46f-165">**ソリューションエクスプローラー**で [*ハブ*] フォルダーを右クリックし、[**新しい項目**の**追加** > ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="5d46f-165">Right-click the *Hubs* folder in **Solution Explorer** and select **Add** > **New Item**.</span></span> <span data-ttu-id="5d46f-166">**[新しい項目の追加]** ダイアログボックスで [ **Web** > **SignalR** ] カテゴリを選択し、 **SignalR Hub クラス (v2)** 項目テンプレートを選択します。</span><span class="sxs-lookup"><span data-stu-id="5d46f-166">In the **Add New Item** dialog box, select the **Web** > **SignalR** category, and then select the **SignalR Hub Class (v2)** item template.</span></span> <span data-ttu-id="5d46f-167">新しいハブに*MyHub.cs*という名前を指定し、 **[追加]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="5d46f-167">Name the new hub *MyHub.cs* and select **Add**.</span></span>

    ![[新しい項目の追加] ダイアログボックスの [ハブ] フォルダーに SignalR Hub クラスを追加する](using-signalr-performance-counters-in-an-azure-web-role/_static/image13.png)

22. <span data-ttu-id="5d46f-169">*MyHub.cs*はメインウィンドウで自動的に開きます。</span><span class="sxs-lookup"><span data-stu-id="5d46f-169">*MyHub.cs* will automatically open in the main window.</span></span> <span data-ttu-id="5d46f-170">内容を次のコードに置き換え、ファイルを保存して閉じます。</span><span class="sxs-lookup"><span data-stu-id="5d46f-170">Replace the contents with the following code, then save and close the file:</span></span>

    [!code-csharp[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample7.cs)]

23. <span data-ttu-id="5d46f-171">*[クランク](signalr-connection-density-testing-with-crank.md)* は、SignalR codebase と共に提供される接続密度テストツールです。</span><span class="sxs-lookup"><span data-stu-id="5d46f-171">*[Crank.exe](signalr-connection-density-testing-with-crank.md)* is a connection density testing tool provided with the SignalR codebase.</span></span> <span data-ttu-id="5d46f-172">クランクは永続的な接続を必要とするため、テスト時に使用するためにサイトに追加します。</span><span class="sxs-lookup"><span data-stu-id="5d46f-172">Since Crank requires a persistent connection, you add one to your site for use when testing.</span></span> <span data-ttu-id="5d46f-173">*PersistentConnections*という名前の**WebRole1**プロジェクトに新しいフォルダーを追加します。</span><span class="sxs-lookup"><span data-stu-id="5d46f-173">Add a new folder to the **WebRole1** project called *PersistentConnections*.</span></span> <span data-ttu-id="5d46f-174">このフォルダーを右クリックし、[ > **クラス**の**追加**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="5d46f-174">Right-click this folder and select **Add** > **Class**.</span></span> <span data-ttu-id="5d46f-175">新しいクラスファイルに*MyPersistentConnections.cs*という名前を指定し、 **[追加]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="5d46f-175">Name the new class file *MyPersistentConnections.cs* and select **Add**.</span></span>

24. <span data-ttu-id="5d46f-176">Visual Studio によって、メインウィンドウで*MyPersistentConnections.cs*ファイルが開きます。</span><span class="sxs-lookup"><span data-stu-id="5d46f-176">Visual Studio will open the *MyPersistentConnections.cs* file in the main window.</span></span> <span data-ttu-id="5d46f-177">内容を次のコードに置き換え、ファイルを保存して閉じます。</span><span class="sxs-lookup"><span data-stu-id="5d46f-177">Replace the contents with the following code, then save and close the file:</span></span>

    [!code-csharp[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample8.cs)]

25. <span data-ttu-id="5d46f-178">`Startup` クラスを使用すると、OWIN の起動時に SignalR オブジェクトが開始されます。</span><span class="sxs-lookup"><span data-stu-id="5d46f-178">Using the `Startup` class, the SignalR objects start when OWIN starts up.</span></span> <span data-ttu-id="5d46f-179">*Startup.cs*を開くか作成し、内容を次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="5d46f-179">Open or create *Startup.cs* and replace the contents with the following code:</span></span>

    [!code-csharp[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample9.cs)]

    <span data-ttu-id="5d46f-180">上記のコードでは、`OwinStartup` 属性は、このクラスを OWIN を開始するようにマークします。</span><span class="sxs-lookup"><span data-stu-id="5d46f-180">In the code above, the `OwinStartup` attribute marks this class to start OWIN.</span></span> <span data-ttu-id="5d46f-181">`Configuration` メソッドは SignalR を開始します。</span><span class="sxs-lookup"><span data-stu-id="5d46f-181">The `Configuration` method starts SignalR.</span></span>

26. <span data-ttu-id="5d46f-182">**F5**キーを押して、Microsoft Azure Emulator でアプリケーションをテストします。</span><span class="sxs-lookup"><span data-stu-id="5d46f-182">Test your application in the Microsoft Azure Emulator by pressing **F5**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5d46f-183">**MapSignalR**で**FileLoadException**が発生した場合は、web.config のバインド*リダイレクトを次のように変更*します。</span><span class="sxs-lookup"><span data-stu-id="5d46f-183">If you encounter a **FileLoadException** at **MapSignalR**, change the binding redirects in *web.config* to the following:</span></span>

    [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample12.xml?highlight=3,7)]

27. <span data-ttu-id="5d46f-184">約1分待ちます。</span><span class="sxs-lookup"><span data-stu-id="5d46f-184">Wait about one minute.</span></span> <span data-ttu-id="5d46f-185">Visual Studio で Cloud Explorer ツールウィンドウを開き ( > **Cloud Explorer**の**表示**)、パス `(Local)/Storage Accounts/(Development)/Tables`を展開します。</span><span class="sxs-lookup"><span data-stu-id="5d46f-185">Open the Cloud Explorer tool window in Visual Studio (**View** > **Cloud Explorer**) and expand the path `(Local)/Storage Accounts/(Development)/Tables`.</span></span> <span data-ttu-id="5d46f-186">**WADPerformanceCountersTable**をダブルクリックします。</span><span class="sxs-lookup"><span data-stu-id="5d46f-186">Double-click **WADPerformanceCountersTable**.</span></span> <span data-ttu-id="5d46f-187">テーブルデータに SignalR カウンターが表示されます。</span><span class="sxs-lookup"><span data-stu-id="5d46f-187">You should see SignalR counters in the table data.</span></span> <span data-ttu-id="5d46f-188">テーブルが表示されない場合は、Azure Storage 資格情報の再入力が必要になることがあります。</span><span class="sxs-lookup"><span data-stu-id="5d46f-188">If you don't see the table, you may need to re-enter your Azure Storage credentials.</span></span> <span data-ttu-id="5d46f-189">場合によっては、**更新** ボタンを選択して**Cloud Explorer**のテーブルを表示するか、テーブルを開く ウィンドウの **更新** ボタンを選択してテーブル内のデータを表示する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5d46f-189">You may need to select the **Refresh** button to see the table in **Cloud Explorer** or select the **Refresh** button in the open table window to see data in the table.</span></span>

    ![Visual Studio での WAD パフォーマンスカウンターテーブルの選択 Cloud Explorer](using-signalr-performance-counters-in-an-azure-web-role/_static/image11.png)

    ![WAD パフォーマンスカウンターテーブルで収集されたカウンターの表示](using-signalr-performance-counters-in-an-azure-web-role/_static/image12.png)

28. <span data-ttu-id="5d46f-192">クラウドでアプリケーションをテストするには、 **serviceconfiguration.cscfg**ファイルを更新し、`Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString` に有効な Azure Storage アカウントの接続文字列を設定します。</span><span class="sxs-lookup"><span data-stu-id="5d46f-192">To test your application in the cloud, update the **ServiceConfiguration.Cloud.cscfg** file and set the `Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString` to a valid Azure Storage account connection string.</span></span>

    [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample10.xml)]

29. <span data-ttu-id="5d46f-193">アプリケーションを Azure サブスクリプションにデプロイします。</span><span class="sxs-lookup"><span data-stu-id="5d46f-193">Deploy the application to your Azure subscription.</span></span> <span data-ttu-id="5d46f-194">アプリケーションを Azure にデプロイする方法の詳細については、「[クラウドサービスを作成およびデプロイする方法](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5d46f-194">For details on how to deploy an application to Azure, see [How to Create and Deploy a Cloud Service](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy).</span></span>

30. <span data-ttu-id="5d46f-195">数分待ちます。</span><span class="sxs-lookup"><span data-stu-id="5d46f-195">Wait a few minutes.</span></span> <span data-ttu-id="5d46f-196">**Cloud Explorer**で、上記で構成したストレージアカウントを見つけて、`WADPerformanceCountersTable` テーブルを検索します。</span><span class="sxs-lookup"><span data-stu-id="5d46f-196">In **Cloud Explorer**, locate the storage account you configured above and find the `WADPerformanceCountersTable` table in it.</span></span> <span data-ttu-id="5d46f-197">テーブルデータに SignalR カウンターが表示されます。</span><span class="sxs-lookup"><span data-stu-id="5d46f-197">You should see SignalR counters in the table data.</span></span> <span data-ttu-id="5d46f-198">テーブルが表示されない場合は、Azure Storage 資格情報の再入力が必要になることがあります。</span><span class="sxs-lookup"><span data-stu-id="5d46f-198">If you don't see the table, you may need to re-enter your Azure Storage credentials.</span></span> <span data-ttu-id="5d46f-199">場合によっては、**更新** ボタンを選択して**Cloud Explorer**のテーブルを表示するか、テーブルを開く ウィンドウの **更新** ボタンを選択してテーブル内のデータを表示する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5d46f-199">You may need to select the **Refresh** button to see the table in **Cloud Explorer** or select the **Refresh** button in the open table window to see data in the table.</span></span>

<span data-ttu-id="5d46f-200">このチュートリアルで使用されている元のコンテンツの[Martin Richard](https://social.msdn.microsoft.com/profile/Martin+Richard)に感謝します。</span><span class="sxs-lookup"><span data-stu-id="5d46f-200">Special thanks to [Martin Richard](https://social.msdn.microsoft.com/profile/Martin+Richard) for the original content used in this tutorial.</span></span>
