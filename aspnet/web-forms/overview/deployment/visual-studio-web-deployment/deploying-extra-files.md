---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-extra-files
title: 'Visual Studio を使用した ASP.NET Web 配置: 追加ファイルの配置 |Microsoft Docs'
author: tdykstra
description: このチュートリアルシリーズでは、ASP.NET web アプリケーションをデプロイ (発行) して、Web Apps またはサードパーティのホスティングプロバイダーに Azure App Service する方法について説明します。
ms.author: riande
ms.date: 03/23/2015
ms.assetid: 1cd91055-84bc-42c6-9d80-646f41429d4d
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-extra-files
msc.type: authoredcontent
ms.openlocfilehash: eaa3141c22980f0c816e2f33b5597ac9fe69c23c
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74594907"
---
# <a name="aspnet-web-deployment-using-visual-studio-deploying-extra-files"></a><span data-ttu-id="7e268-103">Visual Studio を使用した ASP.NET Web 配置: 追加ファイルの配置</span><span class="sxs-lookup"><span data-stu-id="7e268-103">ASP.NET Web Deployment using Visual Studio: Deploying Extra Files</span></span>

<span data-ttu-id="7e268-104">[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="7e268-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="7e268-105">スタートプロジェクトのダウンロード</span><span class="sxs-lookup"><span data-stu-id="7e268-105">Download Starter Project</span></span>](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> <span data-ttu-id="7e268-106">このチュートリアルシリーズでは、Visual Studio 2012 または Visual Studio 2010 を使用して、Azure App Service Web Apps またはサードパーティのホスティングプロバイダーにするために、ASP.NET web アプリケーションをデプロイ (発行) する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="7e268-106">This tutorial series shows you how to deploy (publish) an ASP.NET web application to Azure App Service Web Apps or to a third-party hosting provider, by using Visual Studio 2012 or Visual Studio 2010.</span></span> <span data-ttu-id="7e268-107">シリーズの詳細については、[シリーズの最初のチュートリアル](introduction.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="7e268-107">For information about the series, see [the first tutorial in the series](introduction.md).</span></span>

## <a name="overview"></a><span data-ttu-id="7e268-108">の概要</span><span class="sxs-lookup"><span data-stu-id="7e268-108">Overview</span></span>

<span data-ttu-id="7e268-109">このチュートリアルでは、Visual Studio web 発行パイプラインを拡張して、デプロイ中に追加のタスクを実行する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="7e268-109">This tutorial shows how to extend the Visual Studio web publish pipeline to do an additional task during deployment.</span></span> <span data-ttu-id="7e268-110">このタスクでは、プロジェクトフォルダーに含まれていない余分なファイルをコピー先の web サイトにコピーします。</span><span class="sxs-lookup"><span data-stu-id="7e268-110">The task is to copy extra files that are not in the project folder to the destination web site.</span></span>

<span data-ttu-id="7e268-111">このチュートリアルでは、1つの追加ファイル ( *robots.txt*) をコピーします。</span><span class="sxs-lookup"><span data-stu-id="7e268-111">For this tutorial you'll copy one extra file: *robots.txt*.</span></span> <span data-ttu-id="7e268-112">このファイルをステージングにデプロイしますが、運用環境には展開しません。</span><span class="sxs-lookup"><span data-stu-id="7e268-112">You want to deploy this file to staging but not to production.</span></span> <span data-ttu-id="7e268-113">「[運用環境へのデプロイ](deploying-to-production.md)」チュートリアルでは、このファイルをプロジェクトに追加し、それを除外するように実稼働発行プロファイルを構成しました。</span><span class="sxs-lookup"><span data-stu-id="7e268-113">In [the Deploying to Production](deploying-to-production.md) tutorial, you added this file to the project and configured the Production publish profile to exclude it.</span></span> <span data-ttu-id="7e268-114">このチュートリアルでは、この状況に対処するための別の方法を紹介します。これは、配置するファイルには便利ですが、プロジェクトには含めないようにするためのものです。</span><span class="sxs-lookup"><span data-stu-id="7e268-114">In this tutorial you'll see an alternative method to handle this situation, one that will be useful for any files that you want to deploy but don't want to include in the project.</span></span>

## <a name="move-the-robotstxt-file"></a><span data-ttu-id="7e268-115">Robots.txt ファイルを移動する</span><span class="sxs-lookup"><span data-stu-id="7e268-115">Move the robots.txt file</span></span>

<span data-ttu-id="7e268-116">*Robots.txt*を処理する別の方法を準備するには、チュートリアルのこのセクションで、ファイルをプロジェクトに含まれていないフォルダーに移動し、そのステージング環境から*robots.txt*を削除します。</span><span class="sxs-lookup"><span data-stu-id="7e268-116">To prepare for a different method of handling *robots.txt*, in this section of the tutorial you move the file to a folder that is not included in the project, and you delete *robots.txt* from the staging environment.</span></span> <span data-ttu-id="7e268-117">このファイルをステージングから削除する必要があります。これにより、その環境にファイルを展開する新しい方法が正常に機能していることを確認できます。</span><span class="sxs-lookup"><span data-stu-id="7e268-117">It is necessary to delete the file from staging so that you can verify that your new method of deploying the file to that environment is working correctly.</span></span>

1. <span data-ttu-id="7e268-118">**ソリューションエクスプローラー**で、 *robots.txt*ファイルを右クリックし、 **[プロジェクトから除外]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="7e268-118">In **Solution Explorer**, right-click the *robots.txt* file and click **Exclude From Project**.</span></span>
2. <span data-ttu-id="7e268-119">Windows エクスプローラーを使用して、ソリューションフォルダーに新しいフォルダーを作成し、 *ExtraFiles*という名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="7e268-119">Using Windows File Explorer, create a new folder in the solution folder and name it *ExtraFiles*.</span></span>
3. <span data-ttu-id="7e268-120">*ContosoUniversity*プロジェクトフォルダーから*ExtraFiles*フォルダーに*robots.txt*ファイルを移動します。</span><span class="sxs-lookup"><span data-stu-id="7e268-120">Move the *robots.txt* file from the *ContosoUniversity* project folder to the *ExtraFiles* folder.</span></span>

    ![ExtraFiles フォルダー](deploying-extra-files/_static/image1.png)
4. <span data-ttu-id="7e268-122">FTP ツールを使用して、[ステージング] web サイトから*robots.txt*ファイルを削除します。</span><span class="sxs-lookup"><span data-stu-id="7e268-122">Using your FTP tool, delete the *robots.txt* file from the staging web site.</span></span>

    <span data-ttu-id="7e268-123">別の方法として、ステージング発行プロファイル の **設定** タブにある **ファイル発行オプション** の **宛先にある追加ファイルを削除**する を選択し、ステージングに再発行することもできます。</span><span class="sxs-lookup"><span data-stu-id="7e268-123">As an alternative, you can select **Remove additional files at destination** under **File Publish Options** on the **Settings** tab of the Staging publish profile, and republish to staging.</span></span>

## <a name="update-the-publish-profile-file"></a><span data-ttu-id="7e268-124">発行プロファイルファイルを更新する</span><span class="sxs-lookup"><span data-stu-id="7e268-124">Update the publish profile file</span></span>

<span data-ttu-id="7e268-125">ステージング環境には*robots.txt*のみが必要であるため、デプロイするために更新する必要がある発行プロファイルはステージングのみです。</span><span class="sxs-lookup"><span data-stu-id="7e268-125">You only need *robots.txt* in staging, so the only publish profile you need to update in order to deploy it is Staging.</span></span>

1. <span data-ttu-id="7e268-126">Visual Studio で、[ファイル] [ *pubxml*] を開きます。</span><span class="sxs-lookup"><span data-stu-id="7e268-126">In Visual Studio, open *Staging.pubxml*.</span></span>
2. <span data-ttu-id="7e268-127">ファイルの末尾で、終了 `</Project>` タグの前に、次のマークアップを追加します。</span><span class="sxs-lookup"><span data-stu-id="7e268-127">At the end of the file, before the closing `</Project>` tag, add the following markup:</span></span>

    [!code-xml[Main](deploying-extra-files/samples/sample1.xml)]

    <span data-ttu-id="7e268-128">このコードは、配置する追加ファイルを収集する新しい*ターゲット*を作成します。</span><span class="sxs-lookup"><span data-stu-id="7e268-128">This code creates a new *target* that will collect additional files to be deployed.</span></span> <span data-ttu-id="7e268-129">ターゲットは、指定した条件に基づいて MSBuild が実行する1つ以上のタスクで構成されます。</span><span class="sxs-lookup"><span data-stu-id="7e268-129">A target is composed of one or more tasks that MSBuild will execute based on conditions you specify.</span></span>

    <span data-ttu-id="7e268-130">`Include` 属性は、ファイルを検索するフォルダーが*ExtraFiles*であり、プロジェクトフォルダーと同じレベルにあることを指定します。</span><span class="sxs-lookup"><span data-stu-id="7e268-130">The `Include` attribute specifies that the folder in which to find the files is *ExtraFiles*, located at the same level as the project folder.</span></span> <span data-ttu-id="7e268-131">MSBuild は、そのフォルダーからすべてのファイルを収集し、任意のサブフォルダーから再帰的にすべてのファイルを収集します (二重のアスタリスクは再帰サブフォルダーを指定します)。</span><span class="sxs-lookup"><span data-stu-id="7e268-131">MSBuild will collect all files from that folder and recursively from any subfolders (the double asterisk specifies recursive subfolders).</span></span> <span data-ttu-id="7e268-132">このコードでは、複数のファイルとファイルを*ExtraFiles*フォルダー内のサブフォルダーに配置し、すべてを展開します。</span><span class="sxs-lookup"><span data-stu-id="7e268-132">With this code you could put multiple files, and files in subfolders inside the *ExtraFiles* folder, and all will be deployed.</span></span>

    <span data-ttu-id="7e268-133">`DestinationRelativePath` 要素は、フォルダーとファイルを、 *ExtraFiles*フォルダーにあるのと同じファイルおよびフォルダー構造で、送信先 web サイトのルートフォルダーにコピーする必要があることを指定します。</span><span class="sxs-lookup"><span data-stu-id="7e268-133">The `DestinationRelativePath` element specifies that the folders and files should be copied to the root folder of the destination web site, in the same file and folder structure as they are found in the *ExtraFiles* folder.</span></span> <span data-ttu-id="7e268-134">*ExtraFiles*フォルダー自体をコピーする場合、`DestinationRelativePath` 値は*ExtraFiles\%(RecursiveDir)% (Filename)% (Extension)* になります。</span><span class="sxs-lookup"><span data-stu-id="7e268-134">If you wanted to copy the *ExtraFiles* folder itself, the `DestinationRelativePath` value would be *ExtraFiles\%(RecursiveDir)%(Filename)%(Extension)*.</span></span>
3. <span data-ttu-id="7e268-135">ファイルの末尾で、終了 `</Project>` タグの前に、新しいターゲットをいつ実行するかを指定する次のマークアップを追加します。</span><span class="sxs-lookup"><span data-stu-id="7e268-135">At the end of the file, before the closing `</Project>` tag, add the following markup that specifies when to execute the new target.</span></span>

    [!code-xml[Main](deploying-extra-files/samples/sample2.xml)]

    <span data-ttu-id="7e268-136">このコードにより、コピー先のフォルダーにファイルをコピーするターゲットが実行されるたびに、新しい `CustomCollectFiles` ターゲットが実行されます。</span><span class="sxs-lookup"><span data-stu-id="7e268-136">This code causes the new `CustomCollectFiles` target to be executed whenever the target that copies files to the destination folder is executed.</span></span> <span data-ttu-id="7e268-137">発行と展開パッケージの作成には別のターゲットがあり、発行ではなく展開パッケージを使用して展開する場合に、両方のターゲットに新しいターゲットが挿入されます。</span><span class="sxs-lookup"><span data-stu-id="7e268-137">There is a separate target for publish versus deployment package creation, and the new target is injected in both targets in case you decide to deploy by using a deployment package instead of publishing.</span></span>

    <span data-ttu-id="7e268-138">*Pubxml*ファイルは、次の例のようになります。</span><span class="sxs-lookup"><span data-stu-id="7e268-138">The *.pubxml* file now looks like the following example:</span></span>

    [!code-xml[Main](deploying-extra-files/samples/sample3.xml?highlight=53-71)]
4. <span data-ttu-id="7e268-139">*ステージングの pubxml*ファイルを保存して閉じます。</span><span class="sxs-lookup"><span data-stu-id="7e268-139">Save and close the *Staging.pubxml* file.</span></span>

## <a name="publish-to-staging"></a><span data-ttu-id="7e268-140">ステージングに発行する</span><span class="sxs-lookup"><span data-stu-id="7e268-140">Publish to staging</span></span>

<span data-ttu-id="7e268-141">ワンクリック発行またはコマンドラインを使用して、ステージングプロファイルを使用してアプリケーションを発行します。</span><span class="sxs-lookup"><span data-stu-id="7e268-141">Using one-click publish or the command line, publish the application by using the Staging profile.</span></span>

<span data-ttu-id="7e268-142">ワンクリック発行を使用する場合は、 **[プレビュー]** ウィンドウで、 *robots.txt*がコピーされることを確認できます。</span><span class="sxs-lookup"><span data-stu-id="7e268-142">If you use one-click publish, you can verify in the **Preview** window that *robots.txt* will be copied.</span></span> <span data-ttu-id="7e268-143">それ以外の場合は、FTP ツールを使用して、 *robots.txt*ファイルが配置後に web サイトのルートフォルダーにあることを確認します。</span><span class="sxs-lookup"><span data-stu-id="7e268-143">Otherwise, use your FTP tool to verify that the *robots.txt* file is in the root folder of the web site after deployment.</span></span>

## <a name="summary"></a><span data-ttu-id="7e268-144">要約</span><span class="sxs-lookup"><span data-stu-id="7e268-144">Summary</span></span>

<span data-ttu-id="7e268-145">これで、ASP.NET web アプリケーションをサードパーティのホスティングプロバイダーにデプロイするための一連のチュートリアルが完了します。</span><span class="sxs-lookup"><span data-stu-id="7e268-145">This completes this series of tutorials on deploying an ASP.NET web application to a third-party hosting provider.</span></span> <span data-ttu-id="7e268-146">これらのチュートリアルで説明されているトピックの詳細については、「 [ASP.NET Deployment Content Map](https://go.microsoft.com/fwlink/p/?LinkId=282413)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="7e268-146">For more information about any of the topics covered in these tutorials, see the [ASP.NET Deployment Content Map](https://go.microsoft.com/fwlink/p/?LinkId=282413).</span></span>

## <a name="more-information"></a><span data-ttu-id="7e268-147">説明</span><span class="sxs-lookup"><span data-stu-id="7e268-147">More information</span></span>

<span data-ttu-id="7e268-148">MSBuild ファイルを操作する方法がわかっている場合は、(プロファイル固有のタスク用の) *pubxml*ファイルまたはプロジェクトの *.targets*ファイル (すべてのプロファイルに適用されるタスク用) にコードを記述することで、他の多くの配置タスクを自動化できます。</span><span class="sxs-lookup"><span data-stu-id="7e268-148">If you know how to work with MSBuild files, you can automate many other deployment tasks by writing code in *.pubxml* files (for profile-specific tasks) or the project *.wpp.targets* file (for tasks that apply to all profiles).</span></span> <span data-ttu-id="7e268-149">*Pubxml*および*wpp*ファイルの詳細については、「[方法: 発行プロファイル (Pubxml) ファイルの配置設定を編集する」および「Visual Studio Web プロジェクトの .targets ファイル](https://msdn.microsoft.com/library/ff398069)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="7e268-149">For more information about *.pubxml* and *.wpp.targets* files, see [How to: Edit Deployment Settings in Publish Profile (.pubxml) Files and the .wpp.targets File in Visual Studio Web Projects](https://msdn.microsoft.com/library/ff398069).</span></span> <span data-ttu-id="7e268-150">MSBuild コードの基本的な概要については、「エンタープライズ展開シリーズで**のプロジェクトファイルの構造** [: プロジェクトファイルについ](../web-deployment-in-the-enterprise/understanding-the-project-file.md)て」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="7e268-150">For a basic introduction to MSBuild code, see **The Anatomy of a Project File** in [Enterprise Deployment Series: Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md).</span></span> <span data-ttu-id="7e268-151">MSBuild ファイルを操作して独自のシナリオでタスクを実行する方法については、「 [Microsoft Build Engine: msbuild と Team Foundation ビルド](http://msbuildbook.com)による作成者 Ibraham Hashimi とウィリアム Bartholow の使用」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="7e268-151">To learn how to work with MSBuild files to perform tasks for your own scenarios, see this book: [Inside the Microsoft Build Engine: Using MSBuild and Team Foundation Build](http://msbuildbook.com) by Sayed Ibraham Hashimi and William Bartholomew.</span></span>

## <a name="acknowledgements"></a><span data-ttu-id="7e268-152">謝辞</span><span class="sxs-lookup"><span data-stu-id="7e268-152">Acknowledgements</span></span>

<span data-ttu-id="7e268-153">このチュートリアルシリーズの内容に多大な貢献をした次の人々に感謝したいと思います。</span><span class="sxs-lookup"><span data-stu-id="7e268-153">I would like to thank the following people who made significant contributions to the content of this tutorial series:</span></span>

- [<span data-ttu-id="7e268-154">Alberto Poblacion, MVP &amp; MCT, スペイン</span><span class="sxs-lookup"><span data-stu-id="7e268-154">Alberto Poblacion, MVP &amp; MCT, Spain</span></span>](https://mvp.microsoft.com/mvp/Alberto%20Poblacion%20Bolano-36772)
- <span data-ttu-id="7e268-155">Jarod Ferguson、Data Platform Development MVP、米国</span><span class="sxs-lookup"><span data-stu-id="7e268-155">Jarod Ferguson, Data Platform Development MVP, United States</span></span>
- <span data-ttu-id="7e268-156">過酷 Mittal、Microsoft</span><span class="sxs-lookup"><span data-stu-id="7e268-156">Harsh Mittal, Microsoft</span></span>
- <span data-ttu-id="7e268-157">[Jon Galloway](https://weblogs.asp.net/jgalloway) (twitter: [@jongalloway](http://twitter.com/jongalloway))</span><span class="sxs-lookup"><span data-stu-id="7e268-157">[Jon Galloway](https://weblogs.asp.net/jgalloway) (twitter: [@jongalloway](http://twitter.com/jongalloway))</span></span>
- [<span data-ttu-id="7e268-158">Kristina Olson、Microsoft</span><span class="sxs-lookup"><span data-stu-id="7e268-158">Kristina Olson, Microsoft</span></span>](https://blogs.iis.net/krolson/default.aspx)
- [<span data-ttu-id="7e268-159">Mike Pope、Microsoft</span><span class="sxs-lookup"><span data-stu-id="7e268-159">Mike Pope, Microsoft</span></span>](http://www.mikepope.com/blog/DisplayBlog.aspx)
- <span data-ttu-id="7e268-160">Mohit Srivastava、Microsoft</span><span class="sxs-lookup"><span data-stu-id="7e268-160">Mohit Srivastava, Microsoft</span></span>
- [<span data-ttu-id="7e268-161">Raffaele Rialdi、イタリア</span><span class="sxs-lookup"><span data-stu-id="7e268-161">Raffaele Rialdi, Italy</span></span>](http://www.iamraf.net/)
- [<span data-ttu-id="7e268-162">Rick Anderson、Microsoft</span><span class="sxs-lookup"><span data-stu-id="7e268-162">Rick Anderson, Microsoft</span></span>](https://blogs.msdn.com/b/rickandy/)
- <span data-ttu-id="7e268-163">[作成者 Hashimi、Microsoft](http://sedodream.com/default.aspx)(twitter: [@sayedihashimi](http://twitter.com/sayedihashimi))</span><span class="sxs-lookup"><span data-stu-id="7e268-163">[Sayed Hashimi, Microsoft](http://sedodream.com/default.aspx)(twitter: [@sayedihashimi](http://twitter.com/sayedihashimi))</span></span>
- <span data-ttu-id="7e268-164">[Scott マン Selman](http://www.hanselman.com/blog/) (twitter: [@shanselman](http://twitter.com/shanselman))</span><span class="sxs-lookup"><span data-stu-id="7e268-164">[Scott Hanselman](http://www.hanselman.com/blog/) (twitter: [@shanselman](http://twitter.com/shanselman))</span></span>
- <span data-ttu-id="7e268-165">[Scott Hunter、Microsoft](https://blogs.msdn.com/b/scothu/) (twitter: [@coolcsh](http://twitter.com/coolcsh))</span><span class="sxs-lookup"><span data-stu-id="7e268-165">[Scott Hunter, Microsoft](https://blogs.msdn.com/b/scothu/) (twitter: [@coolcsh](http://twitter.com/coolcsh))</span></span>
- [<span data-ttu-id="7e268-166">Srđan Božović、セルビア</span><span class="sxs-lookup"><span data-stu-id="7e268-166">Srđan Božović, Serbia</span></span>](http://msforge.net/blogs/zmajcek/)
- <span data-ttu-id="7e268-167">[Vishal Joshi、Microsoft](http://vishaljoshi.blogspot.com/) (twitter: [@vishalrjoshi](http://twitter.com/vishalrjoshi))</span><span class="sxs-lookup"><span data-stu-id="7e268-167">[Vishal Joshi, Microsoft](http://vishaljoshi.blogspot.com/) (twitter: [@vishalrjoshi](http://twitter.com/vishalrjoshi))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="7e268-168">[前へ](command-line-deployment.md)
> [次へ](troubleshooting.md)</span><span class="sxs-lookup"><span data-stu-id="7e268-168">[Previous](command-line-deployment.md)
[Next](troubleshooting.md)</span></span>
