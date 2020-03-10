---
uid: whitepapers/aspnet-and-iis6
title: IIS 6.0 で ASP.NET 1.1 を実行する |Microsoft Docs
author: rick-anderson
description: Windows Server 2003 には IIS 6.0 と ASP.NET 1.1 の両方が含まれていますが、これらのコンポーネントは既定で無効になっています。 このホワイトペーパーでは、IIS 6.0 を有効にする方法について説明します。
ms.author: riande
ms.date: 02/10/2010
ms.assetid: 5a5537bf-2aaa-49e7-839f-9e6522b829d8
msc.legacyurl: /whitepapers/aspnet-and-iis6
msc.type: content
ms.openlocfilehash: 2e7812f34481afe9a71927c0d9ba2a9abc9632e4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78419848"
---
# <a name="running-aspnet-11-with-iis-60"></a><span data-ttu-id="67f5f-104">IIS 6.0 で ASP.NET 1.1 を実行する</span><span class="sxs-lookup"><span data-stu-id="67f5f-104">Running ASP.NET 1.1 with IIS 6.0</span></span>

> <span data-ttu-id="67f5f-105">Windows Server 2003 には IIS 6.0 と ASP.NET 1.1 の両方が含まれていますが、これらのコンポーネントは既定で無効になっています。</span><span class="sxs-lookup"><span data-stu-id="67f5f-105">While Windows Server 2003 includes both IIS 6.0 and ASP.NET 1.1, these components are disabled by default.</span></span> <span data-ttu-id="67f5f-106">このホワイトペーパーでは、IIS 6.0 と ASP.NET 1.1 を有効にする方法について説明します。また、IIS と ASP.NET から最適なパフォーマンスを得るために、いくつかの構成設定を推奨しています。</span><span class="sxs-lookup"><span data-stu-id="67f5f-106">This whitepaper describes how to enable IIS 6.0 and ASP.NET 1.1, and recommends several configuration settings to get the optimal performance from IIS and ASP.NET.</span></span>
> 
> <span data-ttu-id="67f5f-107">ASP.NET 1.1 および IIS 6.0 に適用されます。</span><span class="sxs-lookup"><span data-stu-id="67f5f-107">Applies to ASP.NET 1.1 and IIS 6.0.</span></span>

<span data-ttu-id="67f5f-108">ASP.NET 1.1 は、Windows Server 2003 に付属しています。これには、インターネットインフォメーションサーバー (IIS) バージョン6.0 の最新バージョンも含まれています。</span><span class="sxs-lookup"><span data-stu-id="67f5f-108">ASP.NET 1.1 ships with Windows Server 2003, which also includes the latest version of Internet Information Server (IIS) version 6.0.</span></span> <span data-ttu-id="67f5f-109">IIS 6.0 と ASP.NET 1.1 はシームレスに統合するように設計されており、ASP.NET は既定で新しい IIS 6.0 ワーカープロセスモデルに設定されています。</span><span class="sxs-lookup"><span data-stu-id="67f5f-109">IIS 6.0 and ASP.NET 1.1 are designed to integrate seamlessly and ASP.NET now defaults to the new IIS 6.0 worker process model.</span></span>

## <a name="aspnet-11-is-not-installed-by-default"></a><span data-ttu-id="67f5f-110">ASP.NET 1.1 は既定ではインストールされません</span><span class="sxs-lookup"><span data-stu-id="67f5f-110">ASP.NET 1.1 is not installed by default</span></span>

<span data-ttu-id="67f5f-111">Microsoft のサーバーオペレーティングシステムの以前のバージョンとは異なり、インターネットインフォメーションサーバー (IIS) は既定では有効になっていません。とは ASP.NET 1.1 です。</span><span class="sxs-lookup"><span data-stu-id="67f5f-111">Unlike previous versions of Microsoft's server operating systems, Internet Information Server (IIS) is not enabled by default; nor is ASP.NET 1.1.</span></span> <span data-ttu-id="67f5f-112">IIS を有効にするには、次の2つのオプションがあります。</span><span class="sxs-lookup"><span data-stu-id="67f5f-112">There are two options for enabling IIS:</span></span>

### <a name="enabling-iis-option-1---configure-your-server-wizard"></a><span data-ttu-id="67f5f-113">IIS を有効にする、オプション #1-サーバーの構成ウィザード</span><span class="sxs-lookup"><span data-stu-id="67f5f-113">Enabling IIS, option #1 - Configure Your Server Wizard</span></span>

<span data-ttu-id="67f5f-114">Windows Server 2003 は、必要なモードでサーバーを適切に構成するために、新しい "サーバーの構成ウィザード" を提供します。</span><span class="sxs-lookup"><span data-stu-id="67f5f-114">Windows Server 2003 ships a new 'Configure Your Server Wizard' to help you properly configure your server in the desired mode.</span></span>

<span data-ttu-id="67f5f-115">ウィザードを開始するには、ウィザードを実行するには、管理者としてログインする必要があります。開始 |プログラム |[管理ツール] を選択し、[サーバーの構成] を選択します。</span><span class="sxs-lookup"><span data-stu-id="67f5f-115">To start the wizard - note, to run the wizard you must be logged in as an administrator - go to: Start | Programs | Administrative Tools and select 'Configure Your Server'.</span></span>

<span data-ttu-id="67f5f-116">選択すると、[サーバーの構成ウィザード] の開始画面が表示されます。</span><span class="sxs-lookup"><span data-stu-id="67f5f-116">Once selected you should see the 'Configure Your Server Wizard' opening screen:</span></span>

![](aspnet-and-iis6/_static/image1.jpg)

<span data-ttu-id="67f5f-117">[次の &gt;] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="67f5f-117">Click 'Next &gt;':</span></span>

![](aspnet-and-iis6/_static/image2.jpg)

<span data-ttu-id="67f5f-118">[次の &gt;] をクリック</span><span class="sxs-lookup"><span data-stu-id="67f5f-118">Click 'Next &gt;'</span></span>

![](aspnet-and-iis6/_static/image3.jpg)

<span data-ttu-id="67f5f-119">この画面では、[アプリケーションサーバー (IIS、ASP.NET)] を構成するオプションとして選択する必要があります。</span><span class="sxs-lookup"><span data-stu-id="67f5f-119">On this screen you will need to select 'Application server (IIS, ASP.NET) as the options to configure.</span></span>

<span data-ttu-id="67f5f-120">[次の &gt;] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="67f5f-120">Click 'Next &gt;'.</span></span>

![](aspnet-and-iis6/_static/image4.jpg)

<span data-ttu-id="67f5f-121">サーバーをアプリケーションサーバーとして構成するように選択すると、この画面が表示され、追加の機能をインストールするように求められます。</span><span class="sxs-lookup"><span data-stu-id="67f5f-121">After selecting to configure the server as an Application Server, this screen will be displayed prompting what additional capabilities should be installed.</span></span> <span data-ttu-id="67f5f-122">既定では、どちらのオプションも選択されていません。</span><span class="sxs-lookup"><span data-stu-id="67f5f-122">Neither option is selected by default.</span></span> <span data-ttu-id="67f5f-123">ASP.NET を自動的に有効にするには、[ASP を有効にする] を選択する必要があります。NET '。</span><span class="sxs-lookup"><span data-stu-id="67f5f-123">To enable ASP.NET automatically, you need to select 'Enable ASP.NET'.</span></span>

<span data-ttu-id="67f5f-124">[次の &gt;] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="67f5f-124">Click 'Next &gt;'.</span></span>

![](aspnet-and-iis6/_static/image5.jpg)

<span data-ttu-id="67f5f-125">この画面には、インストールするオプションが表示されます。</span><span class="sxs-lookup"><span data-stu-id="67f5f-125">This screen displays what options are to be installed.</span></span>

<span data-ttu-id="67f5f-126">[次の &gt;] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="67f5f-126">Click 'Next &gt;'.</span></span>

![](aspnet-and-iis6/_static/image6.jpg)

<span data-ttu-id="67f5f-127">この画面は、選択したオプションがインストールされている間に表示されます。</span><span class="sxs-lookup"><span data-stu-id="67f5f-127">You will see this screen while the options you selected are being installed.</span></span> <span data-ttu-id="67f5f-128">サービスのインストール中に他のダイアログボックスが表示されることは通常ありません。</span><span class="sxs-lookup"><span data-stu-id="67f5f-128">It is normal to see other dialog boxes appear as services are being installed.</span></span> <span data-ttu-id="67f5f-129">また、Windows 2003 Server のインストール CD の場所を入力するように求められる場合もあります。</span><span class="sxs-lookup"><span data-stu-id="67f5f-129">You may additionally be prompted for the location of the Windows 2003 Server installation CD.</span></span>

<span data-ttu-id="67f5f-130">完了したら [次の &gt;] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="67f5f-130">Click 'Next &gt;' when complete.</span></span>

![](aspnet-and-iis6/_static/image7.jpg)

<span data-ttu-id="67f5f-131">[完了] をクリックします。 Windows Server 2003 は、IIS 6.0 と ASP.NET 1.1 をサポートするように構成されています。</span><span class="sxs-lookup"><span data-stu-id="67f5f-131">Click 'Finish' - the Windows Server 2003 is now configured to support IIS 6.0 and ASP.NET 1.1.</span></span>

### <a name="enabling-iis-option-2---manually-configuring-iis-and-aspnet"></a><span data-ttu-id="67f5f-132">IIS を有効にする、オプション #2-IIS と ASP.NET を手動で構成する</span><span class="sxs-lookup"><span data-stu-id="67f5f-132">Enabling IIS, option #2 - Manually configuring IIS and ASP.NET</span></span>

<span data-ttu-id="67f5f-133">[サーバーの構成ウィザード] を使用しない場合は、必要に応じて、コントロールパネルの [プログラムの追加と削除] を使用して IIS 6.0 および ASP.NET 1.1 をインストールします。</span><span class="sxs-lookup"><span data-stu-id="67f5f-133">If you do not wish to use the 'Configure Your Server Wizard' you can optionally install IIS 6.0 and ASP.NET 1.1 using 'Add or Remove Programs' from the Control Panel.</span></span>

<span data-ttu-id="67f5f-134">まず、コントロールパネルを開きます。</span><span class="sxs-lookup"><span data-stu-id="67f5f-134">First open the Control Panel:</span></span>

![](aspnet-and-iis6/_static/image8.jpg)

<span data-ttu-id="67f5f-135">次に、[windows コンポーネントの追加と削除] をクリックして、[Windows コンポーネントウィザード] を開きます。</span><span class="sxs-lookup"><span data-stu-id="67f5f-135">Next, click on 'Add/Remove Windows Components' which will open the 'Windows Components Wizard':</span></span>

![](aspnet-and-iis6/_static/image9.jpg)

<span data-ttu-id="67f5f-136">[アプリケーションサーバー] を選択してオンにし、[詳細] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="67f5f-136">Highlight and check 'Application Server' and then click the 'Details?'</span></span> <span data-ttu-id="67f5f-137">;</span><span class="sxs-lookup"><span data-stu-id="67f5f-137">button:</span></span>

![](aspnet-and-iis6/_static/image10.jpg)

<span data-ttu-id="67f5f-138">ASP.NET をインストールするには、[ASP] をオンにします。NET '。</span><span class="sxs-lookup"><span data-stu-id="67f5f-138">To install ASP.NET, check 'ASP.NET'.</span></span>

<span data-ttu-id="67f5f-139">[OK] をクリックして、Windows コンポーネントウィザードに戻ります。</span><span class="sxs-lookup"><span data-stu-id="67f5f-139">Click 'OK' to return to the Windows Component Wizard.</span></span> <span data-ttu-id="67f5f-140">Windows コンポーネントウィザードの [次の &gt;] をクリックして、のインストールを開始します。</span><span class="sxs-lookup"><span data-stu-id="67f5f-140">Click 'Next &gt;' from the Windows Component Wizard to begin installing:</span></span>

![](aspnet-and-iis6/_static/image11.jpg)

<span data-ttu-id="67f5f-141">サービスのインストール中に他のダイアログボックスが表示されることは通常ありません。</span><span class="sxs-lookup"><span data-stu-id="67f5f-141">It is normal to see other dialog boxes appear as services are being installed.</span></span> <span data-ttu-id="67f5f-142">また、Windows 2003 Server のインストール CD の場所を入力するように求められる場合もあります。</span><span class="sxs-lookup"><span data-stu-id="67f5f-142">You may additionally be prompted for the location of the Windows 2003 Server installation CD.</span></span>

<span data-ttu-id="67f5f-143">インストールが完了すると、Windows コンポーネントウィザードの最後の画面が表示されます。</span><span class="sxs-lookup"><span data-stu-id="67f5f-143">When installation is complete you will see the last screen of the Windows Component Wizard:</span></span>

![](aspnet-and-iis6/_static/image12.jpg)

<span data-ttu-id="67f5f-144">IIS 6.0 と ASP.NET 1.1 が構成され、使用できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="67f5f-144">IIS 6.0 and ASP.NET 1.1 are now configured and available.</span></span>

## <a name="recommended-settings"></a><span data-ttu-id="67f5f-145">推奨される設定</span><span class="sxs-lookup"><span data-stu-id="67f5f-145">Recommended Settings</span></span>

<span data-ttu-id="67f5f-146">IIS 6.0 で ASP.NET 1.1 を実行する場合、ASP.NET から最適なパフォーマンスを得るために推奨される構成設定がいくつかあります。</span><span class="sxs-lookup"><span data-stu-id="67f5f-146">When running ASP.NET 1.1 with IIS 6.0 there are several configuration settings that are recommended to get the optimal performance from ASP.NET:</span></span>

- <span data-ttu-id="67f5f-147">ワーカープロセスのメモリ制限の構成</span><span class="sxs-lookup"><span data-stu-id="67f5f-147">Configuring worker process memory limits</span></span>
- <span data-ttu-id="67f5f-148">ワーカープロセスのリサイクルの構成</span><span class="sxs-lookup"><span data-stu-id="67f5f-148">Configuring worker process recycling</span></span>

### <a name="configuring-worker-process-memory-limits"></a><span data-ttu-id="67f5f-149">ワーカープロセスのメモリ制限の構成</span><span class="sxs-lookup"><span data-stu-id="67f5f-149">Configuring worker process memory limits</span></span>

<span data-ttu-id="67f5f-150">既定では、iis 6.0 では、IIS で使用できるメモリの量に制限は設定されません。</span><span class="sxs-lookup"><span data-stu-id="67f5f-150">By default IIS 6.0 does not set a limit on the amount of memory that IIS is allowed to use.</span></span> <span data-ttu-id="67f5f-151">ASP.NET のキャッシュ機能はメモリの制限に依存しているため、キャッシュはメモリから未使用の項目を事前に削除できます。</span><span class="sxs-lookup"><span data-stu-id="67f5f-151">ASP.NET's Cache feature relies on a limitation of memory so the Cache can proactively remove unused items from memory.</span></span>

<span data-ttu-id="67f5f-152">IIS 6.0 のメモリリサイクル機能を構成することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="67f5f-152">It is recommended that you configure the memory recycling feature of IIS 6.0.</span></span> <span data-ttu-id="67f5f-153">これを構成するにはインターネットインフォメーションサービスマネージャーを開きます (Start |プログラム |管理ツール |インターネットインフォメーションサービス)。</span><span class="sxs-lookup"><span data-stu-id="67f5f-153">To configure this open Internet Information Services Manager (Start | Programs | Administrative Tools | Internet Information Services).</span></span> <span data-ttu-id="67f5f-154">開いたら、[アプリケーションプール] フォルダーを展開します。</span><span class="sxs-lookup"><span data-stu-id="67f5f-154">Once open, expand the 'Application Pools' folder:</span></span>

<span data-ttu-id="67f5f-155">各アプリケーションプールについて、次のことを行います。</span><span class="sxs-lookup"><span data-stu-id="67f5f-155">For each application pool:</span></span>

![](aspnet-and-iis6/_static/image13.jpg)

1. <span data-ttu-id="67f5f-156">アプリケーションプール (' DefaultAppPool ' など) を右クリックし、[プロパティ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="67f5f-156">Right-click on the application pool, e.g. 'DefaultAppPool', and select 'Properties':</span></span>

![](aspnet-and-iis6/_static/image14.jpg)

2. <span data-ttu-id="67f5f-157">次に、[最大使用メモリ (mb 単位)] をクリックして、メモリのリサイクルを有効にします。</span><span class="sxs-lookup"><span data-stu-id="67f5f-157">Next, enable Memory recycling by clicking on either 'Maximum used memory (in megabytes):'.</span></span> <span data-ttu-id="67f5f-158">値は、サーバー上の物理メモリ (仮想メモリではない) の容量を超えないようにする必要があります。つまり、物理メモリの60% です。つまり、512 MB の物理メモリがあるサーバーでは、310を選択します。</span><span class="sxs-lookup"><span data-stu-id="67f5f-158">The value should not be more than the amount of physical (not virtual) memory on the server, a good approximation is 60% of the physical memory, i.e. for a server with 512MB of physical memory select 310.</span></span> <span data-ttu-id="67f5f-159">また、2 GB のアドレス空間を使用する場合は、最大800MB を超えないようにすることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="67f5f-159">It is also recommended that the maximum not exceed 800MB when using a 2GB address space.</span></span> <span data-ttu-id="67f5f-160">サーバーのメモリアドレス空間が 3 GB の場合、ワーカープロセスの最大メモリ制限は、1, 800MB のようになります。</span><span class="sxs-lookup"><span data-stu-id="67f5f-160">If the memory address space of the server is 3GB, the maximum memory limit for the worker process can be as high as 1,800MB:</span></span>

![](aspnet-and-iis6/_static/image15.jpg)

<span data-ttu-id="67f5f-161">[適用] をクリックし、[OK] をクリックして、[プロパティ] ダイアログボックスを閉じます。</span><span class="sxs-lookup"><span data-stu-id="67f5f-161">Click 'Apply' and the 'OK' to exit the properties dialog.</span></span> <span data-ttu-id="67f5f-162">使用可能なすべてのアプリケーションプールに対してこの手順を繰り返します。</span><span class="sxs-lookup"><span data-stu-id="67f5f-162">Repeat this for all available application pools.</span></span>

### <a name="configuring-worker-recycling"></a><span data-ttu-id="67f5f-163">ワーカーのリサイクルの構成</span><span class="sxs-lookup"><span data-stu-id="67f5f-163">Configuring worker recycling</span></span>

<span data-ttu-id="67f5f-164">既定では、IIS 6.0 は、29時間ごとにワーカープロセスをリサイクルするように構成されています。</span><span class="sxs-lookup"><span data-stu-id="67f5f-164">By default IIS 6.0 is configured to recycle its worker process every 29 hours.</span></span> <span data-ttu-id="67f5f-165">これは ASP.NET を実行しているアプリケーションに対しては少し積極的であり、ワーカープロセスの自動リサイクルは無効にすることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="67f5f-165">This is a bit aggressive for an application running ASP.NET and it is recommended that automatic worker process recycling is disabled.</span></span>

<span data-ttu-id="67f5f-166">ワーカープロセスの自動リサイクルを無効にするには、最初にインターネットインフォメーションサービスマネージャーを開きます (Start |プログラム |管理ツール |インターネットインフォメーションサービス)。</span><span class="sxs-lookup"><span data-stu-id="67f5f-166">To disable automatic worker process recycling, first open Internet Information Services Manager (Start | Programs | Administrative Tools | Internet Information Services).</span></span> <span data-ttu-id="67f5f-167">開いたら、[アプリケーションプール] フォルダーを展開します。</span><span class="sxs-lookup"><span data-stu-id="67f5f-167">Once open, expand the 'Application Pools' folder:</span></span>

![](aspnet-and-iis6/_static/image16.jpg)

<span data-ttu-id="67f5f-168">各アプリケーションプールについて、次のことを行います。</span><span class="sxs-lookup"><span data-stu-id="67f5f-168">For each application pool:</span></span>

1. <span data-ttu-id="67f5f-169">アプリケーションプール (' DefaultAppPool ' など) を右クリックし、[プロパティ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="67f5f-169">Right-click on the application pool, e.g. 'DefaultAppPool', and select 'Properties':</span></span>

![](aspnet-and-iis6/_static/image17.jpg)

2. <span data-ttu-id="67f5f-170">[ワーカープロセスのリサイクル (分単位)] をオフにします:</span><span class="sxs-lookup"><span data-stu-id="67f5f-170">Uncheck 'Recycle worker process (in minutes):':</span></span>

![](aspnet-and-iis6/_static/image18.jpg)

<span data-ttu-id="67f5f-171">[適用] をクリックし、[OK] をクリックして、[プロパティ] ダイアログボックスを閉じます。</span><span class="sxs-lookup"><span data-stu-id="67f5f-171">Click 'Apply' and the 'OK' to exit the properties dialog.</span></span> <span data-ttu-id="67f5f-172">使用可能なすべてのアプリケーションプールに対してこの手順を繰り返します。</span><span class="sxs-lookup"><span data-stu-id="67f5f-172">Repeat this for all available application pools.</span></span>

## <a name="granting-write-access-to-the-file-system"></a><span data-ttu-id="67f5f-173">ファイルシステムへの書き込みアクセス権の付与</span><span class="sxs-lookup"><span data-stu-id="67f5f-173">Granting write access to the file system</span></span>

<span data-ttu-id="67f5f-174">アプリケーションがファイルシステムへの書き込みアクセスを必要とし、NTFS を使用している場合は、ASP.NET アクセスを許可するフォルダーまたはファイルの Access Control リスト (ACL) を変更する必要があります。</span><span class="sxs-lookup"><span data-stu-id="67f5f-174">If your application requires write access to the file system and you are using NTFS you will need to modify an Access Control List (ACL) on the folder or file to grant ASP.NET access to.</span></span>

<span data-ttu-id="67f5f-175">たとえば、c:\inetpub\wwwroot 最初に開いているエクスプローラーに ASP.NET 書き込みアクセス権を付与するには、次のディレクトリに移動します。</span><span class="sxs-lookup"><span data-stu-id="67f5f-175">For example, to grant ASP.NET write access to the c:\inetpub\wwwroot first open explorer and navigate to the directory:</span></span>

![](aspnet-and-iis6/_static/image19.jpg)

<span data-ttu-id="67f5f-176">次に、ディレクトリ ("wwwroot" など) を右クリックし、[プロパティ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="67f5f-176">Next, right-click on the directory, e.g. 'wwwroot' and select properties.</span></span> <span data-ttu-id="67f5f-177">[プロパティ] ダイアログが開いたら、[セキュリティ] タブを選択します。</span><span class="sxs-lookup"><span data-stu-id="67f5f-177">After the properties dialog opens, select the 'Security' tab:</span></span>

![](aspnet-and-iis6/_static/image20.jpg)

<span data-ttu-id="67f5f-178">C:\inetpub\wwwroot\ ディレクトリは、特別な IIS 6.0 グループ ' IIS\_WPG ' に既に読み取り &amp; 実行、フォルダーの内容の一覧表示、および読み取りアクセス許可が既に付与されているディレクトリです。</span><span class="sxs-lookup"><span data-stu-id="67f5f-178">The c:\inetpub\wwwroot\ directory is a special directory in that the special IIS 6.0 group 'IIS\_WPG' is already granted Read &amp; Execute, List Folder Contents, and Read permissions.</span></span> <span data-ttu-id="67f5f-179">ただし、書き込みアクセス許可を付与するには、[書き込み] の [許可] チェックボックスをオンにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="67f5f-179">However, to grant Write permission, you need to click the Allow checkbox for Write:</span></span>

![](aspnet-and-iis6/_static/image21.jpg)

<span data-ttu-id="67f5f-180">IIS 6.0 は、このフォルダーに対する書き込みアクセス許可を持つようになりました。</span><span class="sxs-lookup"><span data-stu-id="67f5f-180">IIS 6.0 now has write permission on this folder.</span></span> <span data-ttu-id="67f5f-181">他のフォルダーに対する書き込みアクセス許可を付与するには、次の手順に従います。既に存在していない場合は、IIS\_WPG グループを追加する必要があることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="67f5f-181">To grant write permissions on other folders, follow these steps - note, you may need to add the IIS\_WPG group if it does not already exist.</span></span>

> [!CAUTION]
> <span data-ttu-id="67f5f-182">IIS\_WPG に書き込みアクセス許可を付与すると、すべての ASP.NET アプリケーションがこのディレクトリに書き込むことができます。</span><span class="sxs-lookup"><span data-stu-id="67f5f-182">Granting write permission to IIS\_WPG will allow any ASP.NET application to write to this directory.</span></span>

## <a name="supporting-integrated-authentication-with-sql-server"></a><span data-ttu-id="67f5f-183">SQL Server による統合認証のサポート</span><span class="sxs-lookup"><span data-stu-id="67f5f-183">Supporting integrated authentication with SQL Server</span></span>

<span data-ttu-id="67f5f-184">統合認証を使用すると、SQL Server は Windows NT 認証を利用して SQL Server ログオンアカウントを検証できます。</span><span class="sxs-lookup"><span data-stu-id="67f5f-184">Integrated authentication allows for SQL Server to leverage Windows NT authentication to validate SQL Server logon accounts.</span></span> <span data-ttu-id="67f5f-185">これにより、ユーザーは標準の SQL Server ログオンプロセスをバイパスできます。</span><span class="sxs-lookup"><span data-stu-id="67f5f-185">This allows the user to bypass the standard SQL Server logon process.</span></span> <span data-ttu-id="67f5f-186">この方法では、ネットワークユーザーは、Windows NT ネットワークセキュリティプロセスからユーザーとパスワードの情報を取得 SQL Server ため、個別のログオン id またはパスワードを指定しなくても、SQL Server データベースにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="67f5f-186">With this approach, a network user can access a SQL Server database without supplying a separate logon identification or password because SQL Server obtains the user and password information from the Windows NT network security process.</span></span>

<span data-ttu-id="67f5f-187">アプリケーションの接続文字列内に資格情報が格納されることはないため、ASP.NET アプリケーションに対して統合認証を選択することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="67f5f-187">Choosing integrated authentication for ASP.NET applications is a good choice because no credentials are ever stored within your connection string for your application.</span></span> <span data-ttu-id="67f5f-188">代わりに、SQL への接続に使用される接続文字列は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="67f5f-188">Rather the connection string used to connect to SQL will look as follows:</span></span>

`"server=localhost; database=Northwind;Trusted_Connection=true"`

<span data-ttu-id="67f5f-189">この接続文字列は、SQL Server にアクセスしようとしているアプリケーションの Windows 資格情報を使用するように SQL Server に指示します。</span><span class="sxs-lookup"><span data-stu-id="67f5f-189">This connection string tells SQL Server to use the Windows credentials of the application attempting to access SQL Server.</span></span> <span data-ttu-id="67f5f-190">ASP.NET/IIS 6 の場合、これは IIS\_WPG グループのアカウントになります。</span><span class="sxs-lookup"><span data-stu-id="67f5f-190">In the case of ASP.NET/IIS 6 this would be an account in the IIS\_WPG group.</span></span>

<span data-ttu-id="67f5f-191">SQL Server と ASP.NET 間の統合認証を有効にするには、まず、SQL Server が統合認証または混合モード認証用に構成されていることを確認する必要があります。このことを判断するには、DBA に確認してください。</span><span class="sxs-lookup"><span data-stu-id="67f5f-191">To enable integrated authentication between SQL Server and ASP.NET, you will need to first ensure that SQL Server is configured for either Integrated authentication or Mixed-Mode authentication - check with your DBA to determine this.</span></span> <span data-ttu-id="67f5f-192">これら2つのモードのいずれかを使用して SQL Server 場合は、統合認証を使用できます。</span><span class="sxs-lookup"><span data-stu-id="67f5f-192">If SQL Server is in one of these two modes, you can use integrated authentication.</span></span>

<span data-ttu-id="67f5f-193">SQL Server Enterprise マネージャーを開きます (Start |プログラム |Microsoft SQL Server |Enterprise Manager) で、適切なサーバーを選択し、[セキュリティ] フォルダーを展開します。</span><span class="sxs-lookup"><span data-stu-id="67f5f-193">Open SQL Server Enterprise Manager (Start | Programs | Microsoft SQL Server | Enterprise Manager), select the appropriate server, and expand the Security folder:</span></span>

![](aspnet-and-iis6/_static/image22.jpg)

<span data-ttu-id="67f5f-194">' BUILTINT\IIS\_WPG ' グループが表示されていない場合は、[ログイン] を右クリックし、[新しい Login '] を選択します。</span><span class="sxs-lookup"><span data-stu-id="67f5f-194">If 'BUILTINT\IIS\_WPG' group is not listed, right-click on Logins and select 'New Login':</span></span>

![](aspnet-and-iis6/_static/image23.jpg)

<span data-ttu-id="67f5f-195">' Name: ' テキストボックスで、「[Server/Domain Name] \ IIS\_WPG」と入力するか、省略記号ボタンをクリックして Windows NT ユーザー/グループピッカーを開きます。</span><span class="sxs-lookup"><span data-stu-id="67f5f-195">In the 'Name:' textbox either enter '[Server/Domain Name]\IIS\_WPG' or click on the ellipses button to open the Windows NT user/group picker:</span></span>

![](aspnet-and-iis6/_static/image24.jpg)

<span data-ttu-id="67f5f-196">現在のコンピューターの IIS\_WPG グループを選択して [追加] をクリックし、[OK] をクリックしてピッカーを閉じます。</span><span class="sxs-lookup"><span data-stu-id="67f5f-196">Select the current machine's IIS\_WPG group and click 'Add' and OK to close the picker.</span></span>

<span data-ttu-id="67f5f-197">次に、既定のデータベースと、データベースにアクセスするための権限も設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="67f5f-197">You then need to also set the default database and the permissions to access the database.</span></span> <span data-ttu-id="67f5f-198">既定のデータベースを設定するには、ドロップダウンリストから次のように選択します。たとえば、Northwind が選択されています。</span><span class="sxs-lookup"><span data-stu-id="67f5f-198">To set the default database choose from the drop down list, e.g. below Northwind is selected:</span></span>

![](aspnet-and-iis6/_static/image25.jpg)

<span data-ttu-id="67f5f-199">次に、[データベースアクセス] タブをクリックします。</span><span class="sxs-lookup"><span data-stu-id="67f5f-199">Next, click on the Database Access tab:</span></span>

![](aspnet-and-iis6/_static/image26.jpg)

<span data-ttu-id="67f5f-200">アクセスを許可するすべてのデータベースについて、[許可] チェックボックスをオンにします。</span><span class="sxs-lookup"><span data-stu-id="67f5f-200">Click on the Permit checkbox for every database that you wish to allow access to.</span></span> <span data-ttu-id="67f5f-201">また、データベースロールを選択する必要があります。 db\_所有者を確認すると、選択したデータベースを管理および使用するために必要なすべての権限がログインに与えられます。</span><span class="sxs-lookup"><span data-stu-id="67f5f-201">You will also need to select database roles, checking db\_owner will ensure your login has all necessary permissions to manage and use the selected database.</span></span>

<span data-ttu-id="67f5f-202">[OK] をクリックして、プロパティダイアログを閉じます。</span><span class="sxs-lookup"><span data-stu-id="67f5f-202">Click OK to exit the property dialog.</span></span> <span data-ttu-id="67f5f-203">ASP.NET アプリケーションは、統合 SQL Server 認証をサポートするように構成されました。</span><span class="sxs-lookup"><span data-stu-id="67f5f-203">Your ASP.NET application is now configured to support integrated SQL Server authentication.</span></span>

## <a name="dont-run-aspnet-10-in-iis-60-native-mode"></a><span data-ttu-id="67f5f-204">IIS 6.0 ネイティブモードで ASP.NET 1.0 を実行しない</span><span class="sxs-lookup"><span data-stu-id="67f5f-204">Don't run ASP.NET 1.0 in IIS 6.0 native mode</span></span>

<span data-ttu-id="67f5f-205">Iis 6.0 の ASP.NET 1.0 は、IIS 5 互換モードでのみサポートされています。</span><span class="sxs-lookup"><span data-stu-id="67f5f-205">ASP.NET 1.0 on IIS 6.0 is only supported in IIS 5 compatibility mode.</span></span>

<span data-ttu-id="67f5f-206">ASP.NET 1.0 を IIS 5.0 互換モードで実行するように構成するにはインターネットサービスマネージャーを開き、[Web サイト] を右クリックし、[プロパティ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="67f5f-206">To configure ASP.NET 1.0 to run in IIS 5.0 compatibility mode, open Internet Services Manager and right click Web Sites and select properties:</span></span>

![](aspnet-and-iis6/_static/image27.jpg)

<span data-ttu-id="67f5f-207">[サービス] タブに切り替えて、確認します。IIS 5.0 分離モードで WWW サービスを実行します。</span><span class="sxs-lookup"><span data-stu-id="67f5f-207">Switch to the Service Tab and check ?Run WWW Service in IIS 5.0 Isolation Mode?:</span></span>

![](aspnet-and-iis6/_static/image28.jpg)
