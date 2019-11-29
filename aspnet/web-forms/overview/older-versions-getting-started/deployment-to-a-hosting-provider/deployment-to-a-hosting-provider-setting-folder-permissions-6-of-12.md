---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12
title: 'Visual Studio または Visual Web Developer を使用した SQL Server Compact を使用した ASP.NET Web アプリケーションのデプロイ: フォルダーのアクセス許可の設定-6/12 |Microsoft Docs'
author: tdykstra
description: この一連のチュートリアルでは、Visual Stu... を使用して SQL Server Compact データベースを含む ASP.NET web アプリケーションプロジェクトをデプロイ (発行) する方法について説明します。
ms.author: riande
ms.date: 11/17/2011
ms.assetid: cd03a188-e947-4f55-9bda-b8bce201d8c6
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12
msc.type: authoredcontent
ms.openlocfilehash: 85a77a196cf3458bbb2e6308838a846936cd070b
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74633511"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-setting-folder-permissions---6-of-12"></a>Visual Studio または Visual Web Developer を使用した SQL Server Compact を使用した ASP.NET Web アプリケーションのデプロイ: フォルダーのアクセス許可の設定-6/12

[Tom Dykstra](https://github.com/tdykstra)

[スタートプロジェクトのダウンロード](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> この一連のチュートリアルでは、Visual Studio 2012 RC または Visual Studio Express 2012 RC for Web を使用して SQL Server Compact データベースを含む ASP.NET web アプリケーションプロジェクトをデプロイ (発行) する方法について説明します。 Web 発行の更新をインストールする場合は、Visual Studio 2010 を使用することもできます。 シリーズの概要については、[シリーズの最初のチュートリアル](deployment-to-a-hosting-provider-introduction-1-of-12.md)を参照してください。
> 
> Visual Studio 2012 の RC リリース後に導入された配置機能を示すチュートリアルについては、SQL Server Compact 以外の SQL Server のエディションをデプロイする方法、Azure App Service Web Apps にデプロイする方法については、「 [ASP.NET Web deployment Using Visual studio (Visual studio を使用した Web デプロイ](../../deployment/visual-studio-web-deployment/introduction.md)のデプロイ)」を参照してください。

## <a name="overview"></a>の概要

このチュートリアルでは、配置された web サイトの*Elmah*フォルダーに対してフォルダーのアクセス許可を設定して、アプリケーションがそのフォルダーにログファイルを作成できるようにします。

Visual Studio 開発サーバー (Cassini) を使用して Visual Studio で web アプリケーションをテストすると、アプリケーションは自分の id で実行されます。 多くの場合、開発用コンピューターの管理者であり、任意のフォルダー内の任意のファイルに対してすべての操作を実行するための完全な権限を持っています。 ただし、アプリケーションが IIS で実行される場合、アプリケーションは、サイトが割り当てられているアプリケーションプールに対して定義されている id で実行されます。 これは通常、アクセス許可が制限されているシステム定義のアカウントです。 既定では、web アプリケーションのファイルとフォルダーに対する読み取りと実行のアクセス許可がありますが、書き込みアクセス権はありません。

これは、アプリケーションがファイルを作成または更新する場合に問題になります。これは、web アプリケーションで一般的に必要となります。 Contoso 大学アプリケーションでは、Elmah は、エラーの詳細を保存するために、 *elmah*フォルダーに XML ファイルを作成します。 Elmah のようなものを使用しない場合でも、サイトでは、ユーザーがファイルをアップロードしたり、サイト内のフォルダーにデータを書き込むその他のタスクを実行したりすることができます。

リマインダー: チュートリアルを実行しているときにエラーメッセージが表示されたり機能しない場合は、必ず[トラブルシューティングのページ](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)を確認してください。

## <a name="testing-error-logging-and-reporting"></a>エラーのログ記録とレポートのテスト

IIS でアプリケーションが正しく動作していないことを確認するには (Visual Studio でテストした場合でも)、Elmah によって通常ログに記録されるエラーが発生した後、Elmah エラーログを開いて詳細を確認することができます。 Elmah が XML ファイルを作成できず、エラーの詳細を保存できなかった場合は、空のエラーレポートが表示されます。

ブラウザーを開き、`http://localhost/ContosoUniversity`にアクセスして、 *Studentsxxx*のような無効な URL を要求します。 Web.config ファイルの `customErrors` 設定が "RemoteOnly" で、IIS をローカルで実行しているため、 *Genericerrorpage .aspx*ページではなく、システムによって生成されたエラーページが表示されます。

[![Error_page_Test](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image2.png)](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image1.png)

次に、 *Elmah*を実行してエラーレポートを表示します。 Elmah が*elmah*フォルダーに XML ファイルを作成できなかったため、空のエラーログページが表示されます。

[![Error_log_page_empty](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image4.png)](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image3.png)

## <a name="setting-write-permission-on-the-elmah-folder"></a>Elmah フォルダーに対する書き込み権限を設定しています

フォルダーのアクセス許可を手動で設定することも、展開プロセスの一部として自動化することもできます。 自動作成を行うには、複雑な MSBuild コードが必要になります。これは、初めてデプロイするときにのみ行う必要があるため、このチュートリアルでは手動で行う方法についてのみ説明します。 (デプロイプロセスのこの部分を作成する方法の詳細については、「作成者 Hashimi のブログでの[Web 発行に対するフォルダーのアクセス許可の設定](http://sedodream.com/2011/11/08/SettingFolderPermissionsOnWebPublish.aspx)」を参照してください)。

**Windows エクスプローラー**で、 *C:\inetpub\wwwroot\ContosoUniversity*に移動します。 [ *Elmah* ] フォルダーを右クリックし、 **[プロパティ]** をクリックして、 **[セキュリティ]** タブを選択します。

[![Elmah_folder_Properties_Security_tab](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image6.png)](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image5.png)

( **[グループ名またはユーザー名]** の一覧に**DefaultAppPool**が表示されない場合は、このチュートリアルで指定したものとは別の方法を使用して、コンピューターに IIS と ASP.NET 4 を設定したことが考えます。 その場合は、Contoso 大学アプリケーションに割り当てられているアプリケーションプールによって使用されている id を確認し、その id に書き込みアクセス許可を付与します。 このチュートリアルの最後にあるアプリケーションプール id に関するリンクを参照してください。)

**[編集]** をクリックします。 **[Elmah の権限]** ダイアログボックスで、 **[DefaultAppPool**] を選択し、 **[許可]** 列の **[書き込み]** チェックボックスをオンにします。

[![Permissions_for_Elmah_dialog_box](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image8.png)](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image7.png)

両方のダイアログボックスで **[OK]** をクリックします。

## <a name="retesting-error-logging-and-reporting"></a>エラーのログ記録とレポートを再作成する

同じ方法でもう一度エラーを発生させてテストし (無効な URL を要求)、**エラーログ**ページを実行します。 今回は、ページにエラーが表示されます。

[![Elmah_Error_Log_page_Test](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image10.png)](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image9.png)

また、そのフォルダーにデータベースファイル SQL Server Compact があり、それらのデータベースのデータを更新できるようにするため、 *App\_Data*フォルダーに対する書き込みアクセス許可も必要です。 ただし、デプロイプロセスによって*アプリ\_データ*フォルダーに対する書き込みアクセス許可が自動的に設定されるため、追加の操作は必要ありません。

これで、ローカルコンピューターの IIS で Contoso 大学を正常に動作させるために必要なすべてのタスクが完了しました。 次のチュートリアルでは、ホスティングプロバイダーにデプロイすることによって、サイトをパブリックに利用できるようにします。

## <a name="more-information"></a>その他の情報

この例では、Elmah がログファイルを保存できなかった理由が非常に明白でした。 問題の原因が明らかでない場合は、IIS トレースを使用できます。IIS.net サイトの「 [IIS 7 でトレースを使用した失敗した要求のトラブルシューティング」を](https://www.iis.net/learn/troubleshoot/using-failed-request-tracing/troubleshooting-failed-requests-using-tracing-in-iis)参照してください。

アプリケーションプール id にアクセス許可を付与する方法の詳細については、IIS.net サイトの「ファイルシステム Acl を使用した IIS の[アプリケーションプール id](https://www.iis.net/learn/manage/configuring-security/application-pool-identities)と[セキュリティ保護されたコンテンツ](https://www.iis.net/learn/get-started/planning-for-security/secure-content-in-iis-through-file-system-acls)」を参照してください。

> [!div class="step-by-step"]
> [前へ](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md)
> [次へ](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)
