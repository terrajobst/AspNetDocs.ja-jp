---
uid: web-forms/overview/deployment/visual-studio-web-deployment/setting-folder-permissions
title: 'Visual Studio を使用した ASP.NET Web 配置: フォルダーのアクセス許可の設定 |Microsoft Docs'
author: tdykstra
description: このチュートリアルシリーズでは、ASP.NET web アプリケーションをデプロイ (発行) して、Web Apps またはサードパーティのホスティングプロバイダーに Azure App Service する方法について説明します。
ms.author: riande
ms.date: 02/15/2013
ms.assetid: 9715a121-fa55-4f1b-a5d2-fb3f6cd8be8f
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/setting-folder-permissions
msc.type: authoredcontent
ms.openlocfilehash: 410525bb2e3f6e5a0be6d7d6b33fb3a40509041a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78465064"
---
# <a name="aspnet-web-deployment-using-visual-studio-setting-folder-permissions"></a><span data-ttu-id="1ebad-103">Visual Studio を使用した ASP.NET Web 配置: フォルダーのアクセス許可の設定</span><span class="sxs-lookup"><span data-stu-id="1ebad-103">ASP.NET Web Deployment using Visual Studio: Setting Folder Permissions</span></span>

<span data-ttu-id="1ebad-104">[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="1ebad-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="1ebad-105">スタートプロジェクトのダウンロード</span><span class="sxs-lookup"><span data-stu-id="1ebad-105">Download Starter Project</span></span>](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> <span data-ttu-id="1ebad-106">このチュートリアルシリーズでは、Visual Studio 2012 または Visual Studio 2010 を使用して、Azure App Service Web Apps またはサードパーティのホスティングプロバイダーにするために、ASP.NET web アプリケーションをデプロイ (発行) する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="1ebad-106">This tutorial series shows you how to deploy (publish) an ASP.NET web application to Azure App Service Web Apps or to a third-party hosting provider, by using Visual Studio 2012 or Visual Studio 2010.</span></span> <span data-ttu-id="1ebad-107">シリーズの詳細については、[シリーズの最初のチュートリアル](introduction.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="1ebad-107">For information about the series, see [the first tutorial in the series](introduction.md).</span></span>

## <a name="overview"></a><span data-ttu-id="1ebad-108">概要</span><span class="sxs-lookup"><span data-stu-id="1ebad-108">Overview</span></span>

<span data-ttu-id="1ebad-109">このチュートリアルでは、配置された web サイトの*Elmah*フォルダーに対してフォルダーのアクセス許可を設定して、アプリケーションがそのフォルダーにログファイルを作成できるようにします。</span><span class="sxs-lookup"><span data-stu-id="1ebad-109">In this tutorial, you set folder permissions for the *Elmah* folder in the deployed web site so that the application can create log files in that folder.</span></span>

<span data-ttu-id="1ebad-110">Visual Studio 開発サーバー (Cassini) または IIS Express を使用して Visual Studio で web アプリケーションをテストする場合、アプリケーションは id で実行されます。</span><span class="sxs-lookup"><span data-stu-id="1ebad-110">When you test a web application in Visual Studio using the Visual Studio Development Server (Cassini) or IIS Express, the application runs under your identity.</span></span> <span data-ttu-id="1ebad-111">多くの場合、開発用コンピューターの管理者であり、任意のフォルダー内の任意のファイルに対してすべての操作を実行するための完全な権限を持っています。</span><span class="sxs-lookup"><span data-stu-id="1ebad-111">You are most likely an administrator on your development computer and have full authority to do anything to any file in any folder.</span></span> <span data-ttu-id="1ebad-112">ただし、アプリケーションが IIS で実行される場合、アプリケーションは、サイトが割り当てられているアプリケーションプールに対して定義されている id で実行されます。</span><span class="sxs-lookup"><span data-stu-id="1ebad-112">But when an application runs under IIS, it runs under the identity defined for the application pool that the site is assigned to.</span></span> <span data-ttu-id="1ebad-113">これは通常、アクセス許可が制限されているシステム定義のアカウントです。</span><span class="sxs-lookup"><span data-stu-id="1ebad-113">This is typically a system-defined account that has limited permissions.</span></span> <span data-ttu-id="1ebad-114">既定では、web アプリケーションのファイルとフォルダーに対する読み取りと実行のアクセス許可がありますが、書き込みアクセス権はありません。</span><span class="sxs-lookup"><span data-stu-id="1ebad-114">By default it has read and execute permissions on your web application's files and folders, but it doesn't have write access.</span></span>

<span data-ttu-id="1ebad-115">これは、アプリケーションがファイルを作成または更新する場合に問題になります。これは、web アプリケーションで一般的に必要となります。</span><span class="sxs-lookup"><span data-stu-id="1ebad-115">This becomes an issue if your application creates or updates files, which is a common need in web applications.</span></span> <span data-ttu-id="1ebad-116">Contoso 大学アプリケーションでは、Elmah は、エラーの詳細を保存するために、 *elmah*フォルダーに XML ファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="1ebad-116">In the Contoso University application, Elmah creates XML files in the *Elmah* folder in order to save details about errors.</span></span> <span data-ttu-id="1ebad-117">Elmah のようなものを使用しない場合でも、サイトでは、ユーザーがファイルをアップロードしたり、サイト内のフォルダーにデータを書き込むその他のタスクを実行したりすることができます。</span><span class="sxs-lookup"><span data-stu-id="1ebad-117">Even if you don't use something like Elmah, your site might let users upload files or perform other tasks that write data to a folder in your site.</span></span>

<span data-ttu-id="1ebad-118">リマインダー: チュートリアルを実行しているときにエラーメッセージが表示されたり機能しない場合は、必ず[トラブルシューティングのページ](troubleshooting.md)を確認してください。</span><span class="sxs-lookup"><span data-stu-id="1ebad-118">Reminder: If you get an error message or something doesn't work as you go through the tutorial, be sure to check the [troubleshooting page](troubleshooting.md).</span></span>

## <a name="test-error-logging-and-reporting"></a><span data-ttu-id="1ebad-119">テストエラーのログ記録とレポート</span><span class="sxs-lookup"><span data-stu-id="1ebad-119">Test error logging and reporting</span></span>

<span data-ttu-id="1ebad-120">IIS でアプリケーションが正しく動作していないことを確認するには (Visual Studio でテストした場合でも)、Elmah によって通常ログに記録されるエラーが発生した後、Elmah エラーログを開いて詳細を確認することができます。</span><span class="sxs-lookup"><span data-stu-id="1ebad-120">To see how the application doesn't work correctly in IIS (although it did when you tested it in Visual Studio), you can cause an error that would normally be logged by Elmah, and then open the Elmah error log to see the details.</span></span> <span data-ttu-id="1ebad-121">Elmah が XML ファイルを作成できず、エラーの詳細を保存できなかった場合は、空のエラーレポートが表示されます。</span><span class="sxs-lookup"><span data-stu-id="1ebad-121">If Elmah was unable to create an XML file and store the error details, you see an empty error report.</span></span>

<span data-ttu-id="1ebad-122">ブラウザーを開き、`http://localhost/ContosoUniversity`にアクセスして、 *Studentsxxx*のような無効な URL を要求します。</span><span class="sxs-lookup"><span data-stu-id="1ebad-122">Open a browser and go to `http://localhost/ContosoUniversity`, and then request an invalid URL like *Studentsxxx.aspx*.</span></span> <span data-ttu-id="1ebad-123">Web.config ファイルの `customErrors` 設定が "RemoteOnly" で、IIS をローカルで実行しているため、 *Genericerrorpage .aspx*ページではなく、システムによって生成されたエラーページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="1ebad-123">You see a system-generated error page instead of the *GenericErrorPage.aspx* page because the `customErrors` setting in the Web.config file is "RemoteOnly" and you are running IIS locally:</span></span>

![HTTP 404 エラーページ](setting-folder-permissions/_static/image1.png)

<span data-ttu-id="1ebad-125">次に、 *Elmah*を実行してエラーレポートを表示します。</span><span class="sxs-lookup"><span data-stu-id="1ebad-125">Now run *Elmah.axd* to see the error report.</span></span> <span data-ttu-id="1ebad-126">管理者アカウントの資格情報 (&quot;admin&quot; と &quot;devpwd&quot;) を使用してログインすると、elmah が*elmah*フォルダーに XML ファイルを作成できなかったため、空のエラーログページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="1ebad-126">After you log in with the administrator account credentials (&quot;admin&quot; and &quot;devpwd&quot;), you see an empty error log page because Elmah was unable to create an XML file in the *Elmah* folder:</span></span>

![エラーログが空です](setting-folder-permissions/_static/image2.png)

## <a name="set-write-permission-on-the-elmah-folder"></a><span data-ttu-id="1ebad-128">Elmah フォルダーに対する書き込みアクセス許可の設定</span><span class="sxs-lookup"><span data-stu-id="1ebad-128">Set write permission on the Elmah folder</span></span>

<span data-ttu-id="1ebad-129">フォルダーのアクセス許可を手動で設定することも、展開プロセスの一部として自動化することもできます。</span><span class="sxs-lookup"><span data-stu-id="1ebad-129">You can set folder permissions manually or you can make it an automatic part of the deployment process.</span></span> <span data-ttu-id="1ebad-130">自動作成を行うには、複雑な MSBuild コードが必要になります。これは、初めて配置するときにのみ実行する必要があるため、次の手順で手動で行うことができます。</span><span class="sxs-lookup"><span data-stu-id="1ebad-130">Making it automatic requires complex MSBuild code, and since you only have to do this the first time you deploy, the following steps how to do it manually.</span></span> <span data-ttu-id="1ebad-131">(デプロイプロセスのこの部分を作成する方法の詳細については、「作成者 Hashimi のブログでの[Web 発行に対するフォルダーのアクセス許可の設定](http://sedodream.com/2011/11/08/SettingFolderPermissionsOnWebPublish.aspx)」を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="1ebad-131">(For information about how to make this part of the deployment process, see [Setting Folder Permissions on Web Publish](http://sedodream.com/2011/11/08/SettingFolderPermissionsOnWebPublish.aspx) on Sayed Hashimi's blog.)</span></span>

1. <span data-ttu-id="1ebad-132">**ファイルエクスプローラー**で、 *C:\inetpub\wwwroot\ContosoUniversity*に移動します。</span><span class="sxs-lookup"><span data-stu-id="1ebad-132">In **File Explorer**, navigate to *C:\inetpub\wwwroot\ContosoUniversity*.</span></span> <span data-ttu-id="1ebad-133">[ *Elmah* ] フォルダーを右クリックし、 **[プロパティ]** をクリックして、 **[セキュリティ]** タブを選択します。</span><span class="sxs-lookup"><span data-stu-id="1ebad-133">Right-click the *Elmah* folder, select **Properties**, and then select the **Security** tab.</span></span>
2. <span data-ttu-id="1ebad-134">**[編集]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="1ebad-134">Click **Edit**.</span></span>
3. <span data-ttu-id="1ebad-135">**[Elmah の権限]** ダイアログボックスで、 **[DefaultAppPool**] を選択し、 **[許可]** 列の **[書き込み]** チェックボックスをオンにします。</span><span class="sxs-lookup"><span data-stu-id="1ebad-135">In the **Permissions for Elmah** dialog box, select **DefaultAppPool**, and then select the **Write** check box in the **Allow** column.</span></span>

    ![ELMAH フォルダーのアクセス許可](setting-folder-permissions/_static/image3.png)

    <span data-ttu-id="1ebad-137">( **[グループ名またはユーザー名]** の一覧に**DefaultAppPool**が表示されない場合は、このチュートリアルで指定したものとは別の方法を使用して、コンピューターに IIS と ASP.NET 4 を設定したことが考えます。</span><span class="sxs-lookup"><span data-stu-id="1ebad-137">(If you don't see **DefaultAppPool** in the **Group or user names** list, you probably used some other method than the one specified in this tutorial to set up IIS and ASP.NET 4 on your computer.</span></span> <span data-ttu-id="1ebad-138">その場合は、Contoso 大学アプリケーションに割り当てられているアプリケーションプールによって使用されている id を確認し、その id に書き込みアクセス許可を付与します。</span><span class="sxs-lookup"><span data-stu-id="1ebad-138">In that case, find out what identity is used by the application pool assigned to the Contoso University application, and grant write permission to that identity.</span></span> <span data-ttu-id="1ebad-139">このチュートリアルの最後にあるアプリケーションプール id に関するリンクを参照してください。)両方のダイアログボックスで **[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="1ebad-139">See the links about application pool identities at the end of this tutorial.) Click **OK** in both dialog boxes.</span></span>

## <a name="retest-error-logging-and-reporting"></a><span data-ttu-id="1ebad-140">エラーのログ記録とレポートを再テストする</span><span class="sxs-lookup"><span data-stu-id="1ebad-140">Retest error logging and reporting</span></span>

<span data-ttu-id="1ebad-141">同じ方法でもう一度エラーを発生させてテストし (無効な URL を要求)、**エラーログ**ページを実行します。</span><span class="sxs-lookup"><span data-stu-id="1ebad-141">Test by causing an error again in the same way (request a bad URL) and run the **Error Log** page.</span></span> <span data-ttu-id="1ebad-142">今回は、ページにエラーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="1ebad-142">This time the error appears on the page.</span></span>

![[ELMAH エラーログ] ページ](setting-folder-permissions/_static/image4.png)

## <a name="summary"></a><span data-ttu-id="1ebad-144">まとめ</span><span class="sxs-lookup"><span data-stu-id="1ebad-144">Summary</span></span>

<span data-ttu-id="1ebad-145">これで、ローカルコンピューターの IIS で Contoso 大学を正常に動作させるために必要なすべてのタスクが完了しました。</span><span class="sxs-lookup"><span data-stu-id="1ebad-145">You have now completed all of the tasks necessary to get Contoso University working correctly in IIS on your local computer.</span></span> <span data-ttu-id="1ebad-146">次のチュートリアルでは、Azure にデプロイすることによって、サイトをパブリックに利用できるようにします。</span><span class="sxs-lookup"><span data-stu-id="1ebad-146">In the next tutorial, you will make the site publicly available by deploying it to Azure.</span></span>

## <a name="more-information"></a><span data-ttu-id="1ebad-147">詳細情報</span><span class="sxs-lookup"><span data-stu-id="1ebad-147">More information</span></span>

<span data-ttu-id="1ebad-148">この例では、Elmah がログファイルを保存できなかった理由が非常に明白でした。</span><span class="sxs-lookup"><span data-stu-id="1ebad-148">In this example, the reason why Elmah was unable to save log files was fairly obvious.</span></span> <span data-ttu-id="1ebad-149">問題の原因が明らかでない場合は、IIS トレースを使用できます。IIS.net サイトの「 [IIS 7 でトレースを使用した失敗した要求のトラブルシューティング」を](https://www.iis.net/learn/troubleshoot/using-failed-request-tracing/troubleshooting-failed-requests-using-tracing-in-iis)参照してください。</span><span class="sxs-lookup"><span data-stu-id="1ebad-149">You can use IIS tracing in cases where the cause of the problem is not so obvious; see [Troubleshooting Failed Requests Using Tracing in IIS 7](https://www.iis.net/learn/troubleshoot/using-failed-request-tracing/troubleshooting-failed-requests-using-tracing-in-iis) on the IIS.net site.</span></span>

<span data-ttu-id="1ebad-150">アプリケーションプール id にアクセス許可を付与する方法の詳細については、IIS.net サイトの「ファイルシステム Acl を使用した IIS の[アプリケーションプール id](https://www.iis.net/learn/manage/configuring-security/application-pool-identities)と[セキュリティ保護されたコンテンツ](https://www.iis.net/learn/get-started/planning-for-security/secure-content-in-iis-through-file-system-acls)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="1ebad-150">For more information about how to grant permissions to application pool identities, see [Application Pool Identities](https://www.iis.net/learn/manage/configuring-security/application-pool-identities) and [Secure Content in IIS Through File System ACLs](https://www.iis.net/learn/get-started/planning-for-security/secure-content-in-iis-through-file-system-acls) on the IIS.net site.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="1ebad-151">[前へ](deploying-to-iis.md)
> [次へ](deploying-to-production.md)</span><span class="sxs-lookup"><span data-stu-id="1ebad-151">[Previous](deploying-to-iis.md)
[Next](deploying-to-production.md)</span></span>
