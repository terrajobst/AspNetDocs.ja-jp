---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update
title: 'Visual Studio を使用した ASP.NET Web 配置: コード更新の配置 |Microsoft Docs'
author: tdykstra
description: このチュートリアルシリーズでは、ASP.NET web アプリケーションをデプロイ (発行) して、Web Apps またはサードパーティのホスティングプロバイダーに Azure App Service する方法について説明します。
ms.author: riande
ms.date: 02/15/2013
ms.assetid: c76dbc35-a914-4ee3-919c-4f4d1fa05104
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update
msc.type: authoredcontent
ms.openlocfilehash: 3881833bfe2a50a38a357614f92f434a04a8ab08
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74626779"
---
# <a name="aspnet-web-deployment-using-visual-studio-deploying-a-code-update"></a><span data-ttu-id="66496-103">Visual Studio を使用した ASP.NET Web 配置: コード更新の配置</span><span class="sxs-lookup"><span data-stu-id="66496-103">ASP.NET Web Deployment using Visual Studio: Deploying a Code Update</span></span>

<span data-ttu-id="66496-104">[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="66496-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="66496-105">スタートプロジェクトのダウンロード</span><span class="sxs-lookup"><span data-stu-id="66496-105">Download Starter Project</span></span>](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> <span data-ttu-id="66496-106">このチュートリアルシリーズでは、Visual Studio 2012 または Visual Studio 2010 を使用して、Azure App Service Web Apps またはサードパーティのホスティングプロバイダーにするために、ASP.NET web アプリケーションをデプロイ (発行) する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="66496-106">This tutorial series shows you how to deploy (publish) an ASP.NET web application to Azure App Service Web Apps or to a third-party hosting provider, by using Visual Studio 2012 or Visual Studio 2010.</span></span> <span data-ttu-id="66496-107">シリーズの詳細については、[シリーズの最初のチュートリアル](introduction.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="66496-107">For information about the series, see [the first tutorial in the series](introduction.md).</span></span>

## <a name="overview"></a><span data-ttu-id="66496-108">の概要</span><span class="sxs-lookup"><span data-stu-id="66496-108">Overview</span></span>

<span data-ttu-id="66496-109">最初のデプロイの後、web サイトの保守と開発の作業が継続し、その前に更新プログラムを展開する必要があります。</span><span class="sxs-lookup"><span data-stu-id="66496-109">After the initial deployment, your work of maintaining and developing your web site continues, and before long you will want to deploy an update.</span></span> <span data-ttu-id="66496-110">このチュートリアルでは、アプリケーションコードに更新プログラムをデプロイするプロセスについて順を追って紹介します。</span><span class="sxs-lookup"><span data-stu-id="66496-110">This tutorial takes you through the process of deploying an update to your application code.</span></span> <span data-ttu-id="66496-111">このチュートリアルで実装およびデプロイする更新プログラムには、データベースの変更は含まれません。次のチュートリアルでは、データベースの変更を配置する場合の違いについて説明します。</span><span class="sxs-lookup"><span data-stu-id="66496-111">The update that you implement and deploy in this tutorial does not involve a database change; you'll see what's different about deploying a database change in the next tutorial.</span></span>

<span data-ttu-id="66496-112">リマインダー: チュートリアルを実行しているときにエラーメッセージが表示されたり機能しない場合は、必ず[トラブルシューティングのページ](troubleshooting.md)を確認してください。</span><span class="sxs-lookup"><span data-stu-id="66496-112">Reminder: If you get an error message or something doesn't work as you go through the tutorial, be sure to check the [troubleshooting page](troubleshooting.md).</span></span>

## <a name="make-a-code-change"></a><span data-ttu-id="66496-113">コードを変更する</span><span class="sxs-lookup"><span data-stu-id="66496-113">Make a code change</span></span>

<span data-ttu-id="66496-114">アプリケーションの更新の簡単な例として **、インストラクターのページに**、選択したインストラクターが担当するコースの一覧を追加します。</span><span class="sxs-lookup"><span data-stu-id="66496-114">As a simple example of an update to your application, you'll add to the **Instructors** page a list of courses taught by the selected instructor.</span></span>

<span data-ttu-id="66496-115">**インストラクター**ページを実行すると、グリッドに**選択**リンクがあることがわかりますが、行の背景を灰色にする以外には何も行われません。</span><span class="sxs-lookup"><span data-stu-id="66496-115">If you run the **Instructors** page, you'll notice that there are **Select** links in the grid, but they don't do anything other than make the row background turn gray.</span></span>

![選択したインストラクターページ](deploying-a-code-update/_static/image1.png)

<span data-ttu-id="66496-117">次に、 **[選択]** リンクがクリックされたときに実行されるコードを追加します。選択したインストラクターによって担当されるコースの一覧が表示されます。</span><span class="sxs-lookup"><span data-stu-id="66496-117">Now you'll add code that runs when the **Select** link is clicked and displays a list of courses taught by the selected instructor .</span></span>

1. <span data-ttu-id="66496-118">*講師*の**ErrorMessageLabel** `Label` コントロールの直後に、次のマークアップを追加します。</span><span class="sxs-lookup"><span data-stu-id="66496-118">In *Instructors.aspx*, add the following markup immediately after the **ErrorMessageLabel** `Label` control:</span></span>

    [!code-aspx[Main](deploying-a-code-update/samples/sample1.aspx)]
2. <span data-ttu-id="66496-119">ページを実行し、インストラクターを選択します。</span><span class="sxs-lookup"><span data-stu-id="66496-119">Run the page and select an instructor.</span></span> <span data-ttu-id="66496-120">インストラクターがトレーニングしたコースの一覧が表示されます。</span><span class="sxs-lookup"><span data-stu-id="66496-120">You see a list of courses taught by that instructor.</span></span>

    ![コースが講義されるインストラクターページ](deploying-a-code-update/_static/image2.png)
3. <span data-ttu-id="66496-122">ブラウザーを閉じます。</span><span class="sxs-lookup"><span data-stu-id="66496-122">Close the browser.</span></span>

## <a name="deploy-the-code-update-to-the-test-environment"></a><span data-ttu-id="66496-123">コードの更新をテスト環境に配置する</span><span class="sxs-lookup"><span data-stu-id="66496-123">Deploy the code update to the test environment</span></span>

<span data-ttu-id="66496-124">発行プロファイルを使用してテスト、ステージング、および運用環境への配置を行う前に、データベースのパブリッシュオプションを変更する必要があります。</span><span class="sxs-lookup"><span data-stu-id="66496-124">Before you can use your publish profiles to deploy to test, staging, and production, you need to change database publishing options.</span></span> <span data-ttu-id="66496-125">メンバーシップデータベースの grant および data deployment スクリプトを実行する必要がなくなりました。</span><span class="sxs-lookup"><span data-stu-id="66496-125">You no longer need to run the grant and data deployment scripts for the membership database.</span></span>

1. <span data-ttu-id="66496-126">ContosoUniversity プロジェクトを右クリックし、 **[発行]** をクリックして、 **Web の発行**ウィザードを開きます。</span><span class="sxs-lookup"><span data-stu-id="66496-126">Open the **Publish Web** wizard by right-clicking the ContosoUniversity project and clicking **Publish**.</span></span>
2. <span data-ttu-id="66496-127">**[プロファイル]** ボックスの一覧で、**テスト**プロファイルをクリックします。</span><span class="sxs-lookup"><span data-stu-id="66496-127">Click the **Test** profile in the **Profile** drop-down list.</span></span>
3. <span data-ttu-id="66496-128">**[設定]** タブをクリックします。</span><span class="sxs-lookup"><span data-stu-id="66496-128">Click the **Settings** tab.</span></span>
4. <span data-ttu-id="66496-129">**[データベース]** セクションの **[defaultconnection]** で、 **[データベースの更新]** チェックボックスをオフにします。</span><span class="sxs-lookup"><span data-stu-id="66496-129">Under **DefaultConnection** in the **Databases** section, clear the **Update database** check box.</span></span>
5. <span data-ttu-id="66496-130">**[プロファイル]** タブをクリックし、 **[プロファイル]** ドロップダウンリストで**ステージング**プロファイルをクリックします。</span><span class="sxs-lookup"><span data-stu-id="66496-130">Click the **Profile** tab, and then click the **Staging** profile in the **Profile** drop-down list.</span></span>
6. <span data-ttu-id="66496-131">**テスト**プロファイルに加えられた変更を保存するかどうかを確認するメッセージが表示されたら、[**はい]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="66496-131">When you are asked if you want to save the changes made to the **Test** profile, click **Yes**.</span></span>
7. <span data-ttu-id="66496-132">ステージングプロファイルで同じ変更を行います。</span><span class="sxs-lookup"><span data-stu-id="66496-132">Make the same change in the Staging profile.</span></span>
8. <span data-ttu-id="66496-133">運用プロファイルで同じ変更を行うには、この手順を繰り返します。</span><span class="sxs-lookup"><span data-stu-id="66496-133">Repeat the process to make the same change in the Production profile.</span></span>
9. <span data-ttu-id="66496-134">Web の**発行**ウィザードを閉じます。</span><span class="sxs-lookup"><span data-stu-id="66496-134">Close the **Publish Web** wizard.</span></span>

<span data-ttu-id="66496-135">テスト環境への配置は、ワンクリックでの発行を再実行するだけの簡単な方法です。</span><span class="sxs-lookup"><span data-stu-id="66496-135">Deploying to the test environment is now a simple matter of running one-click publish again.</span></span> <span data-ttu-id="66496-136">この処理をより迅速に行うために、 **Web One の [発行**] ツールバーを使用できます。</span><span class="sxs-lookup"><span data-stu-id="66496-136">To make this process quicker, you can use the **Web One Click Publish** toolbar.</span></span>

1. <span data-ttu-id="66496-137">**[表示]** メニューの **[ツールバー]** をクリックし、[ **Web One] をクリック**します。</span><span class="sxs-lookup"><span data-stu-id="66496-137">In the **View** menu, choose **Toolbars** and then select **Web One Click Publish**.</span></span>

    ![Selecting_One_Click_Publish_toolbar](deploying-a-code-update/_static/image3.png)
2. <span data-ttu-id="66496-139">**ソリューションエクスプローラー**で、ContosoUniversity プロジェクトを選択します。</span><span class="sxs-lookup"><span data-stu-id="66496-139">In **Solution Explorer**, select the ContosoUniversity project.</span></span>
3. <span data-ttu-id="66496-140">**web で [発行**] ツールバーをクリックし、**テスト**発行プロファイルを選択して、 **[web の発行]** をクリックします (矢印が左と右にあるアイコン)。</span><span class="sxs-lookup"><span data-stu-id="66496-140">the **Web One Click Publish** toolbar, choose the **Test** publish profile and then click **Publish Web** (the icon with arrows pointing left and right).</span></span>

    ![Web_One_Click_Publish_toolbar](deploying-a-code-update/_static/image4.png)
4. <span data-ttu-id="66496-142">Visual Studio によって更新されたアプリケーションが配置され、ブラウザーが自動的にホームページに表示されます。</span><span class="sxs-lookup"><span data-stu-id="66496-142">Visual Studio deploys the updated application, and the browser automatically opens to the home page.</span></span>
5. <span data-ttu-id="66496-143">インストラクターページを実行し、インストラクターを選択して、更新が正常に展開されたことを確認します。</span><span class="sxs-lookup"><span data-stu-id="66496-143">Run the Instructors page and select an instructor to verify that the update was successfully deployed.</span></span>

<span data-ttu-id="66496-144">通常は回帰テストも行います (つまり、サイトの他の部分をテストして、新しい変更によって既存の機能が破壊されていないことを確認します)。</span><span class="sxs-lookup"><span data-stu-id="66496-144">You would normally also do regression testing (that is, test the rest of the site to make sure that the new change didn't break any existing functionality).</span></span> <span data-ttu-id="66496-145">ただし、このチュートリアルでは、この手順を省略し、ステージング環境と運用環境への更新プログラムのデプロイに進みます。</span><span class="sxs-lookup"><span data-stu-id="66496-145">But for this tutorial you'll skip that step and proceed to deploy the update to staging and production.</span></span>

<span data-ttu-id="66496-146">を再展開すると、変更されたファイルが Web 配置によって自動的に判断され、変更されたファイルのみがサーバーにコピーされます。</span><span class="sxs-lookup"><span data-stu-id="66496-146">When you redeploy, Web Deploy automatically determines which files have changed and only copies changed files to the server.</span></span> <span data-ttu-id="66496-147">既定では、Web 配置は、ファイルの最終変更日を使用して、変更された日付を特定します。</span><span class="sxs-lookup"><span data-stu-id="66496-147">By default, Web Deploy uses last-changed dates on files to determine which ones have changed.</span></span> <span data-ttu-id="66496-148">ソース管理システムによっては、ファイルの内容を変更しない場合でもファイルの日付が変更されることがあります。</span><span class="sxs-lookup"><span data-stu-id="66496-148">Some source control systems change file dates even when you don't change the file contents.</span></span> <span data-ttu-id="66496-149">その場合は、ファイルのチェックサムを使用して変更されたファイルを特定するように Web 配置を構成することができます。</span><span class="sxs-lookup"><span data-stu-id="66496-149">In that case, you might want to configure Web Deploy to use file checksums to determine which files have changed.</span></span> <span data-ttu-id="66496-150">詳細については、「ASP.NET の展開に関する FAQ」で、[すべてのファイルが再展開](https://msdn.microsoft.com/library/ee942158.aspx#use_checksum)される理由に関するページを参照してください。</span><span class="sxs-lookup"><span data-stu-id="66496-150">For more information, see [Why do all of my files get redeployed although I didn't change them?](https://msdn.microsoft.com/library/ee942158.aspx#use_checksum) in the ASP.NET Deployment FAQ.</span></span>

## <a name="take-the-application-offline-during-deployment"></a><span data-ttu-id="66496-151">デプロイ中にアプリケーションをオフラインにする</span><span class="sxs-lookup"><span data-stu-id="66496-151">Take the application offline during deployment</span></span>

<span data-ttu-id="66496-152">ここでデプロイしている変更は、1つのページに単純に変更されます。</span><span class="sxs-lookup"><span data-stu-id="66496-152">The change you're deploying now is a simple change to a single page.</span></span> <span data-ttu-id="66496-153">ただし、大規模な変更を配置する場合や、コードとデータベースの両方の変更を配置する場合があります。配置が完了する前にユーザーがページを要求すると、サイトが正しく動作しなくなることがあります。</span><span class="sxs-lookup"><span data-stu-id="66496-153">But sometimes you deploy larger changes, or you deploy both code and database changes, and the site might behave incorrectly if a user requests a page before deployment is finished.</span></span> <span data-ttu-id="66496-154">配置の進行中にユーザーがサイトにアクセスできないようにするには、*アプリ\_のオフライン .htm*ファイルを使用します。</span><span class="sxs-lookup"><span data-stu-id="66496-154">To prevent users from accessing the site while deployment is in progress, you can use an *app\_offline.htm* file.</span></span> <span data-ttu-id="66496-155">アプリケーションのルートフォルダーに*app\_offline .htm*という名前のファイルを配置すると、アプリケーションを実行する代わりに IIS によってそのファイルが自動的に表示されます。</span><span class="sxs-lookup"><span data-stu-id="66496-155">When you put a file named *app\_offline.htm* in the root folder of your application, IIS automatically displays that file instead of running your application.</span></span> <span data-ttu-id="66496-156">そのため、デプロイ中にアクセスできないようにするには、*アプリ\_* をルートフォルダーに置き、デプロイプロセスを実行してから、展開が正常に完了した後で、*アプリ\_offline .htm*を削除します。</span><span class="sxs-lookup"><span data-stu-id="66496-156">So to prevent access during deployment, you put *app\_offline.htm* in the root folder, run the deployment process, and then remove *app\_offline.htm* after successful deployment.</span></span>

<span data-ttu-id="66496-157">配置を開始するときに既定の*アプリ\_オフライン .htm*ファイルを自動的に配置し、終了時に削除するように Web 配置を構成することができます。</span><span class="sxs-lookup"><span data-stu-id="66496-157">You can configure Web Deploy to automatically put a default *app\_offline.htm* file on the server when it starts deploying and remove it when it finishes.</span></span> <span data-ttu-id="66496-158">これを行うには、次の XML 要素を発行プロファイル (pubxml) ファイルに追加するだけです。</span><span class="sxs-lookup"><span data-stu-id="66496-158">To do that all you have to do is add the following XML element to your publish profile (.pubxml) file:</span></span>

[!code-xml[Main](deploying-a-code-update/samples/sample2.xml)]

<span data-ttu-id="66496-159">このチュートリアルでは、カスタム*アプリ\_オフライン .htm*ファイルを作成して使用する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="66496-159">For this tutorial you'll see how to create and use a custom *app\_offline.htm* file.</span></span>

<span data-ttu-id="66496-160">ステージングサイトにアクセスするユーザーがいないため、ステージングサイトで*アプリ\_offline .htm*を使用する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="66496-160">Using *app\_offline.htm* in the staging site isn't required, because you don't have users accessing the staging site.</span></span> <span data-ttu-id="66496-161">ただし、ステージングを使用して、運用環境でのデプロイを計画しているすべてのことをテストすることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="66496-161">But it's a good practice to use staging to test everything the way you plan to deploy in production.</span></span>

### <a name="create-app_offlinehtm"></a><span data-ttu-id="66496-162">アプリ\_offline .htm を作成する</span><span class="sxs-lookup"><span data-stu-id="66496-162">Create app\_offline.htm</span></span>

1. <span data-ttu-id="66496-163">**ソリューションエクスプローラー**で、ソリューションを右クリックし、 **[追加]** をクリックして、 **[新しい項目]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="66496-163">In **Solution Explorer**, right-click the solution and click **Add**, and then click **New Item**.</span></span>
2. <span data-ttu-id="66496-164">*App\_offline .htm*という名前の**html ページ**を作成します (Visual Studio で既定で作成される *.html*拡張子の最後の "l" を削除します)。</span><span class="sxs-lookup"><span data-stu-id="66496-164">Create an **HTML Page** named *app\_offline.htm* (delete the final "l" in the *.html* extension that Visual Studio creates by default).</span></span>
3. <span data-ttu-id="66496-165">テンプレートマークアップを次のマークアップに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="66496-165">Replace the template markup with the following markup:</span></span>

    [!code-html[Main](deploying-a-code-update/samples/sample3.html)]
4. <span data-ttu-id="66496-166">ファイルを保存して閉じます。</span><span class="sxs-lookup"><span data-stu-id="66496-166">Save and close the file.</span></span>

### <a name="copy-app_offlinehtm-to-the-root-folder-of-the-web-site"></a><span data-ttu-id="66496-167">アプリ\_offline .htm を web サイトのルートフォルダーにコピーします。</span><span class="sxs-lookup"><span data-stu-id="66496-167">Copy app\_offline.htm to the root folder of the web site</span></span>

<span data-ttu-id="66496-168">任意の FTP ツールを使用して、web サイトにファイルをコピーできます。</span><span class="sxs-lookup"><span data-stu-id="66496-168">You can use any FTP tool to copy files to the web site.</span></span> <span data-ttu-id="66496-169">[FileZilla](http://filezilla-project.org/)は一般的な FTP ツールであり、スクリーンショットに示されています。</span><span class="sxs-lookup"><span data-stu-id="66496-169">[FileZilla](http://filezilla-project.org/) is a popular FTP tool and is shown in the screen shots.</span></span>

<span data-ttu-id="66496-170">FTP ツールを使用するには、FTP URL、ユーザー名、およびパスワードの3つが必要です。</span><span class="sxs-lookup"><span data-stu-id="66496-170">To use an FTP tool, you need three things: the FTP URL, the user name, and the password.</span></span>

<span data-ttu-id="66496-171">URL は、Azure 管理ポータルの web サイトの [ダッシュボード] ページに表示されます。 FTP のユーザー名とパスワードは、先ほどダウンロードした *.publishsettings*ファイルにあります。</span><span class="sxs-lookup"><span data-stu-id="66496-171">The URL is shown on the web site's dashboard page in the Azure Management Portal, and the user name and password for FTP can be found in the *.publishsettings* file that you downloaded earlier.</span></span> <span data-ttu-id="66496-172">次の手順は、これらの値を取得する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="66496-172">The following steps show how to get these values.</span></span>

1. <span data-ttu-id="66496-173">Azure 管理ポータルで、**Web サイト** タブをクリックし、ステージング web サイトをクリックします。</span><span class="sxs-lookup"><span data-stu-id="66496-173">In the Azure Management Portal, click **Web Sites** tab and then click the staging web site.</span></span>
2. <span data-ttu-id="66496-174">**[ダッシュボード]** ページで下に**スクロールし、[概要] セクション**で FTP ホスト名を見つけます。</span><span class="sxs-lookup"><span data-stu-id="66496-174">On the **Dashboard** page, scroll down to find the FTP host name in the **Quick Glance** section.</span></span>

    ![FTP ホスト名](deploying-a-code-update/_static/image5.png)
3. <span data-ttu-id="66496-176">メモ帳などのテキストエディターで *.publishsettings*ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="66496-176">Open the staging *.publishsettings* file in Notepad or another text editor.</span></span>
4. <span data-ttu-id="66496-177">FTP プロファイルの `publishProfile` 要素を見つけます。</span><span class="sxs-lookup"><span data-stu-id="66496-177">Find the `publishProfile` element for the FTP profile.</span></span>
5. <span data-ttu-id="66496-178">`userName` と `userPWD` の値をコピーします。</span><span class="sxs-lookup"><span data-stu-id="66496-178">Copy the `userName` and `userPWD` values.</span></span>

    ![FTP 資格情報](deploying-a-code-update/_static/image6.png)
6. <span data-ttu-id="66496-180">FTP ツールを開き、FTP URL にログオンします。</span><span class="sxs-lookup"><span data-stu-id="66496-180">Open your FTP tool and log on to the FTP URL.</span></span>
7. <span data-ttu-id="66496-181">*App\_offline .htm*をソリューションフォルダーからステージングサイトの */siteフォルダー*にコピーします。</span><span class="sxs-lookup"><span data-stu-id="66496-181">Copy *app\_offline.htm* from the solution folder to the */site/wwwroot* folder in the staging site.</span></span>

    ![App_offline のコピー](deploying-a-code-update/_static/image7.png)
8. <span data-ttu-id="66496-183">ステージングサイトの URL を参照します。</span><span class="sxs-lookup"><span data-stu-id="66496-183">Browse to your staging site's URL.</span></span> <span data-ttu-id="66496-184">ホームページの代わりに、*アプリ\_offline .htm*ページが表示されるようになります。</span><span class="sxs-lookup"><span data-stu-id="66496-184">You see that the *app\_offline.htm* page is now displayed instead of your home page.</span></span>

    ![ブラウザーウィンドウの app_offline .htm](deploying-a-code-update/_static/image8.png)

<span data-ttu-id="66496-186">これで、ステージングにデプロイする準備ができました。</span><span class="sxs-lookup"><span data-stu-id="66496-186">You are now ready to deploy to staging.</span></span>

## <a name="deploy-the-code-update-to-staging-and-production"></a><span data-ttu-id="66496-187">ステージング環境と運用環境にコードの更新をデプロイする</span><span class="sxs-lookup"><span data-stu-id="66496-187">Deploy the code update to staging and production</span></span>

1. <span data-ttu-id="66496-188">**Web One の [発行**] ツールバーで、 **[ステージング]** 発行プロファイル を選択し、 **[web の発行]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="66496-188">In the **Web One Click Publish** toolbar, choose the **Staging** publish profile and then click **Publish Web**.</span></span>

    <span data-ttu-id="66496-189">更新されたアプリケーションが Visual Studio によって展開され、ブラウザーが開き、サイトのホームページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="66496-189">Visual Studio deploys the updated application and opens the browser to the site's home page.</span></span> <span data-ttu-id="66496-190">*アプリ\_のオフライン .htm*ファイルが表示されます。</span><span class="sxs-lookup"><span data-stu-id="66496-190">The *app\_offline.htm* file is displayed.</span></span> <span data-ttu-id="66496-191">展開が成功したことを確認するためにテストする前に、*アプリ\_のオフライン .htm*ファイルを削除する必要があります。</span><span class="sxs-lookup"><span data-stu-id="66496-191">Before you can test to verify successful deployment, you must remove the *app\_offline.htm* file.</span></span>
2. <span data-ttu-id="66496-192">FTP ツールに戻り、**アプリ\_offline .htm**をステージングサイトから削除します。</span><span class="sxs-lookup"><span data-stu-id="66496-192">Return to your FTP tool, and delete **app\_offline.htm** from the staging site.</span></span>
3. <span data-ttu-id="66496-193">ブラウザーで、ステージングサイトの [インストラクター] ページを開き、更新プログラムが正常に展開されたことを確認するインストラクターを選択します。</span><span class="sxs-lookup"><span data-stu-id="66496-193">In the browser, open the Instructors page in the staging site, and select an instructor to verify that the update was successfully deployed.</span></span>
4. <span data-ttu-id="66496-194">ステージングの場合と同じ手順に従います。</span><span class="sxs-lookup"><span data-stu-id="66496-194">Follow the same procedure for production as you did for staging.</span></span>

<a id="specificfiles"></a>

## <a name="reviewing-changes-and-deploying-specific-files"></a><span data-ttu-id="66496-195">変更の確認と特定のファイルの展開</span><span class="sxs-lookup"><span data-stu-id="66496-195">Reviewing Changes and Deploying Specific Files</span></span>

<span data-ttu-id="66496-196">また、Visual Studio 2012 では、個々のファイルを配置することもできます。</span><span class="sxs-lookup"><span data-stu-id="66496-196">Visual Studio 2012 also gives you the ability to deploy individual files.</span></span> <span data-ttu-id="66496-197">選択したファイルについて、ローカルバージョンと配置されたバージョンの相違点を表示したり、ファイルを移行先環境に配置したり、コピー先の環境からローカルプロジェクトにファイルをコピーしたりできます。</span><span class="sxs-lookup"><span data-stu-id="66496-197">For a selected file you can view differences between the local version and the deployed version, deploy the file to the destination environment, or copy the file from the destination environment to the local project.</span></span> <span data-ttu-id="66496-198">チュートリアルのこのセクションでは、これらの機能を使用する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="66496-198">In this section of the tutorial you see how to use these features.</span></span>

### <a name="make-a-change-to-deploy"></a><span data-ttu-id="66496-199">デプロイを変更する</span><span class="sxs-lookup"><span data-stu-id="66496-199">Make a change to deploy</span></span>

1. <span data-ttu-id="66496-200">*コンテンツ/サイト .css*を開き、`body` タグのブロックを見つけます。</span><span class="sxs-lookup"><span data-stu-id="66496-200">Open *Content/Site.css*, and find the block for the `body` tag.</span></span>
2. <span data-ttu-id="66496-201">`background-color` の値を `#fff` から `darkblue`に変更します。</span><span class="sxs-lookup"><span data-stu-id="66496-201">Change the value for `background-color` from `#fff` to `darkblue`.</span></span>

    [!code-css[Main](deploying-a-code-update/samples/sample4.css?highlight=2)]

### <a name="view-the-change-in-the-publish-preview-window"></a><span data-ttu-id="66496-202">[発行のプレビュー] ウィンドウでの変更の表示</span><span class="sxs-lookup"><span data-stu-id="66496-202">View the change in the Publish Preview window</span></span>

<span data-ttu-id="66496-203">**Web の発行**ウィザードを使用してプロジェクトを発行するときに、**プレビュー**ウィンドウでファイルをダブルクリックすると、発行される変更内容を確認できます。</span><span class="sxs-lookup"><span data-stu-id="66496-203">When you use the **Publish Web** wizard to publish the project, you can see what changes are going to be published by double-clicking the file in the **Preview** window.</span></span>

1. <span data-ttu-id="66496-204">ContosoUniversity プロジェクトを右クリックし、 **[発行]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="66496-204">Right-click the ContosoUniversity project and click **Publish**.</span></span>
2. <span data-ttu-id="66496-205">**[プロファイル]** ドロップダウンリストから、**テスト**発行プロファイルを選択します。</span><span class="sxs-lookup"><span data-stu-id="66496-205">From the **Profile** drop-down list, select the **Test** publish profile.</span></span>
3. <span data-ttu-id="66496-206">**[プレビュー]** をクリックし、 **[プレビューの開始]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="66496-206">Click **Preview**, and then click **Start Preview**.</span></span>
4. <span data-ttu-id="66496-207">**プレビュー**ウィンドウで、 **[.css]** をダブルクリックします。</span><span class="sxs-lookup"><span data-stu-id="66496-207">In the **Preview** pane, double-click **Site.css**.</span></span>

    ![[.Css] をダブルクリックします。](deploying-a-code-update/_static/image9.png)

    <span data-ttu-id="66496-209">**[変更のプレビュー]** ダイアログに、デプロイされる変更のプレビューが表示されます。</span><span class="sxs-lookup"><span data-stu-id="66496-209">The **Preview changes** dialog shows a preview of the changes that will be deployed.</span></span>

    ![サイト .css に対する変更のプレビュー](deploying-a-code-update/_static/image10.png)

    <span data-ttu-id="66496-211">*Web.config*ファイルをダブルクリックすると、 **[変更のプレビュー]** ダイアログボックスに、ビルド構成の変換と発行プロファイルの変換の影響が表示されます。</span><span class="sxs-lookup"><span data-stu-id="66496-211">If you double-click the *Web.config* file, the **Preview changes** dialog shows the effect of your build configuration transformations and publish profile transformations.</span></span> <span data-ttu-id="66496-212">この時点で、サーバー*上の web.config ファイルが*変更されることは何も行われていないため、変更がないことが予想されます。</span><span class="sxs-lookup"><span data-stu-id="66496-212">At this point you have not done anything that would cause the *Web.config* file on the server to change, so you expect to see no changes.</span></span> <span data-ttu-id="66496-213">ただし、 **[変更のプレビュー]** ウィンドウでは、2つの変更が誤って表示されます。</span><span class="sxs-lookup"><span data-stu-id="66496-213">However, the **Preview changes** window incorrectly shows two changes.</span></span> <span data-ttu-id="66496-214">2つの XML 要素が削除されるように見えます。</span><span class="sxs-lookup"><span data-stu-id="66496-214">It looks like two XML elements will be removed.</span></span> <span data-ttu-id="66496-215">これらの要素は、発行プロセスによって追加されます。この場合、Code First コンテキストクラスの**アプリケーション開始時に [Code First Migrations の実行**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="66496-215">These elements are added by the publish process when you select **Execute Code First Migrations on application start** for a Code First context class.</span></span> <span data-ttu-id="66496-216">この比較は、発行プロセスによってこれらの要素が追加される前に行われます。そのため、削除されるのではなく、削除されているように見えます。</span><span class="sxs-lookup"><span data-stu-id="66496-216">The comparison is done before the publish process adds those elements, so it looks like they are being removed although they will not be removed.</span></span> <span data-ttu-id="66496-217">このエラーは、今後のリリースで修正される予定です。</span><span class="sxs-lookup"><span data-stu-id="66496-217">This error will be corrected in a future release.</span></span>
5. <span data-ttu-id="66496-218">**[閉じる]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="66496-218">Click **Close**.</span></span>
6. <span data-ttu-id="66496-219">**[発行]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="66496-219">Click **Publish**.</span></span>
7. <span data-ttu-id="66496-220">ブラウザーが開き、テストサイトのホームページが表示されたら、CTRL キーを押しながら F5 キーを押して、CSS の変更の効果を確認します。</span><span class="sxs-lookup"><span data-stu-id="66496-220">When the browser opens to the home page of the Test site, press CTRL+F5 to cause a hard refresh in order to see the effect of the CSS change.</span></span>

    ![CSS の変更の影響](deploying-a-code-update/_static/image11.png)
8. <span data-ttu-id="66496-222">ブラウザーを閉じます。</span><span class="sxs-lookup"><span data-stu-id="66496-222">Close the browser.</span></span>

### <a name="publish-specific-files-from-solution-explorer"></a><span data-ttu-id="66496-223">ソリューションエクスプローラーから特定のファイルを発行する</span><span class="sxs-lookup"><span data-stu-id="66496-223">Publish specific files from Solution Explorer</span></span>

<span data-ttu-id="66496-224">青の背景に気がなく、元の色に戻す必要があるとします。</span><span class="sxs-lookup"><span data-stu-id="66496-224">Suppose you don't like the blue background and want to revert to the original color.</span></span> <span data-ttu-id="66496-225">このセクションでは、**ソリューションエクスプローラー**から直接特定のファイルを発行することによって、元の設定を復元します。</span><span class="sxs-lookup"><span data-stu-id="66496-225">In this section you'll restore the original settings by publishing a specific file directly from **Solution Explorer**.</span></span>

1. <span data-ttu-id="66496-226">*コンテンツ/サイト .css*を開き、`background-color` 設定を `#fff`に復元します。</span><span class="sxs-lookup"><span data-stu-id="66496-226">Open *Content/Site.css* and restore the `background-color` setting to `#fff`.</span></span>
2. <span data-ttu-id="66496-227">**ソリューションエクスプローラー**で、*コンテンツ/サイトの .css*ファイルを右クリックします。</span><span class="sxs-lookup"><span data-stu-id="66496-227">In **Solution Explorer**, right-click the *Content/Site.css* file.</span></span>

    <span data-ttu-id="66496-228">コンテキストメニューには、3つの発行オプションが表示されます。</span><span class="sxs-lookup"><span data-stu-id="66496-228">The context menu shows three publish options.</span></span>

    ![ソリューションエクスプローラーからの発行オプション](deploying-a-code-update/_static/image12.png)
3. <span data-ttu-id="66496-230">[変更のプレビュー] をクリックして **、.css に**します。</span><span class="sxs-lookup"><span data-stu-id="66496-230">Click **Preview changes to Site.css**.</span></span>

    <span data-ttu-id="66496-231">ウィンドウが開き、ローカルファイルと移行先の環境でのバージョンの相違点が表示されます。</span><span class="sxs-lookup"><span data-stu-id="66496-231">A window opens to show the differences between the local file and the version of it in the destination environment.</span></span>

    ![Diff-Content/.css](deploying-a-code-update/_static/image13.png)
4. <span data-ttu-id="66496-233">**ソリューションエクスプローラー**で、もう一度 **[.css]** を右クリックし、 **[Publish site .css]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="66496-233">In **Solution Explorer**, right-click **Site.css** again and click **Publish Site.css**.</span></span>

    <span data-ttu-id="66496-234">**[Web 発行アクティビティ]** ウィンドウに、ファイルが発行されたことが表示されます。</span><span class="sxs-lookup"><span data-stu-id="66496-234">The **Web Publish Activity** window shows that the file has been published.</span></span>

    ![Web 発行アクティビティウィンドウ](deploying-a-code-update/_static/image14.png)
5. <span data-ttu-id="66496-236">ブラウザーで `http://localhost/contosouniversity` URL を開き、CTRL キーを押しながら F5 キーを押すと、CSS の変更の効果を確認するために、ハード更新が行われます。</span><span class="sxs-lookup"><span data-stu-id="66496-236">Open a browser to the `http://localhost/contosouniversity` URL, and then press CTRL+F5 to cause a hard refresh in order to see the effect of the CSS change.</span></span>

    ![通常の CSS を使用したホームページ](deploying-a-code-update/_static/image15.png)
6. <span data-ttu-id="66496-238">ブラウザーを閉じます。</span><span class="sxs-lookup"><span data-stu-id="66496-238">Close the browser.</span></span>

## <a name="summary"></a><span data-ttu-id="66496-239">要約</span><span class="sxs-lookup"><span data-stu-id="66496-239">Summary</span></span>

<span data-ttu-id="66496-240">ここでは、データベースの変更を伴わないアプリケーションの更新を展開するいくつかの方法を説明しました。また、変更をプレビューして、更新対象が期待どおりであることを確認する方法についても説明しました。</span><span class="sxs-lookup"><span data-stu-id="66496-240">You've now seen several ways to deploy an application update that does not involve a database change, and you've seen how to preview the changes to verify that what will be updated is what you expect.</span></span> <span data-ttu-id="66496-241">これで、インストラクターのページに、**コース**のセクションがあります。</span><span class="sxs-lookup"><span data-stu-id="66496-241">The Instructors page now has a **Courses Taught** section.</span></span>

![コースが講義されるインストラクターページ](deploying-a-code-update/_static/image16.png)

<span data-ttu-id="66496-243">次のチュートリアルでは、データベースの変更を配置する方法について説明します。誕生日フィールドをデータベースとインストラクターページに追加します。</span><span class="sxs-lookup"><span data-stu-id="66496-243">The next tutorial shows you how to deploy a database change: you'll add a birthdate field to the database and to the Instructors page.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="66496-244">[前へ](deploying-to-production.md)
> [次へ](deploying-a-database-update.md)</span><span class="sxs-lookup"><span data-stu-id="66496-244">[Previous](deploying-to-production.md)
[Next](deploying-a-database-update.md)</span></span>
