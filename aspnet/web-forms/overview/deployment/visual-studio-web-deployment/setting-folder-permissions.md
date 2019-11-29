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
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74614935"
---
# <a name="aspnet-web-deployment-using-visual-studio-setting-folder-permissions"></a>Visual Studio を使用した ASP.NET Web 配置: フォルダーのアクセス許可の設定

[Tom Dykstra](https://github.com/tdykstra)

[スタートプロジェクトのダウンロード](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> このチュートリアルシリーズでは、Visual Studio 2012 または Visual Studio 2010 を使用して、Azure App Service Web Apps またはサードパーティのホスティングプロバイダーにするために、ASP.NET web アプリケーションをデプロイ (発行) する方法について説明します。 シリーズの詳細については、[シリーズの最初のチュートリアル](introduction.md)を参照してください。

## <a name="overview"></a>の概要

このチュートリアルでは、配置された web サイトの*Elmah*フォルダーに対してフォルダーのアクセス許可を設定して、アプリケーションがそのフォルダーにログファイルを作成できるようにします。

Visual Studio 開発サーバー (Cassini) または IIS Express を使用して Visual Studio で web アプリケーションをテストする場合、アプリケーションは id で実行されます。 多くの場合、開発用コンピューターの管理者であり、任意のフォルダー内の任意のファイルに対してすべての操作を実行するための完全な権限を持っています。 ただし、アプリケーションが IIS で実行される場合、アプリケーションは、サイトが割り当てられているアプリケーションプールに対して定義されている id で実行されます。 これは通常、アクセス許可が制限されているシステム定義のアカウントです。 既定では、web アプリケーションのファイルとフォルダーに対する読み取りと実行のアクセス許可がありますが、書き込みアクセス権はありません。

これは、アプリケーションがファイルを作成または更新する場合に問題になります。これは、web アプリケーションで一般的に必要となります。 Contoso 大学アプリケーションでは、Elmah は、エラーの詳細を保存するために、 *elmah*フォルダーに XML ファイルを作成します。 Elmah のようなものを使用しない場合でも、サイトでは、ユーザーがファイルをアップロードしたり、サイト内のフォルダーにデータを書き込むその他のタスクを実行したりすることができます。

リマインダー: チュートリアルを実行しているときにエラーメッセージが表示されたり機能しない場合は、必ず[トラブルシューティングのページ](troubleshooting.md)を確認してください。

## <a name="test-error-logging-and-reporting"></a>テストエラーのログ記録とレポート

IIS でアプリケーションが正しく動作していないことを確認するには (Visual Studio でテストした場合でも)、Elmah によって通常ログに記録されるエラーが発生した後、Elmah エラーログを開いて詳細を確認することができます。 Elmah が XML ファイルを作成できず、エラーの詳細を保存できなかった場合は、空のエラーレポートが表示されます。

ブラウザーを開き、`http://localhost/ContosoUniversity`にアクセスして、 *Studentsxxx*のような無効な URL を要求します。 Web.config ファイルの `customErrors` 設定が "RemoteOnly" で、IIS をローカルで実行しているため、 *Genericerrorpage .aspx*ページではなく、システムによって生成されたエラーページが表示されます。

![HTTP 404 エラーページ](setting-folder-permissions/_static/image1.png)

次に、 *Elmah*を実行してエラーレポートを表示します。 管理者アカウントの資格情報 (&quot;admin&quot; と &quot;devpwd&quot;) を使用してログインすると、elmah が*elmah*フォルダーに XML ファイルを作成できなかったため、空のエラーログページが表示されます。

![エラーログが空です](setting-folder-permissions/_static/image2.png)

## <a name="set-write-permission-on-the-elmah-folder"></a>Elmah フォルダーに対する書き込みアクセス許可の設定

フォルダーのアクセス許可を手動で設定することも、展開プロセスの一部として自動化することもできます。 自動作成を行うには、複雑な MSBuild コードが必要になります。これは、初めて配置するときにのみ実行する必要があるため、次の手順で手動で行うことができます。 (デプロイプロセスのこの部分を作成する方法の詳細については、「作成者 Hashimi のブログでの[Web 発行に対するフォルダーのアクセス許可の設定](http://sedodream.com/2011/11/08/SettingFolderPermissionsOnWebPublish.aspx)」を参照してください)。

1. **ファイルエクスプローラー**で、 *C:\inetpub\wwwroot\ContosoUniversity*に移動します。 [ *Elmah* ] フォルダーを右クリックし、 **[プロパティ]** をクリックして、 **[セキュリティ]** タブを選択します。
2. **[編集]** をクリックします。
3. **[Elmah の権限]** ダイアログボックスで、 **[DefaultAppPool**] を選択し、 **[許可]** 列の **[書き込み]** チェックボックスをオンにします。

    ![ELMAH フォルダーのアクセス許可](setting-folder-permissions/_static/image3.png)

    ( **[グループ名またはユーザー名]** の一覧に**DefaultAppPool**が表示されない場合は、このチュートリアルで指定したものとは別の方法を使用して、コンピューターに IIS と ASP.NET 4 を設定したことが考えます。 その場合は、Contoso 大学アプリケーションに割り当てられているアプリケーションプールによって使用されている id を確認し、その id に書き込みアクセス許可を付与します。 このチュートリアルの最後にあるアプリケーションプール id に関するリンクを参照してください。)両方のダイアログボックスで **[OK]** をクリックします。

## <a name="retest-error-logging-and-reporting"></a>エラーのログ記録とレポートを再テストする

同じ方法でもう一度エラーを発生させてテストし (無効な URL を要求)、**エラーログ**ページを実行します。 今回は、ページにエラーが表示されます。

![[ELMAH エラーログ] ページ](setting-folder-permissions/_static/image4.png)

## <a name="summary"></a>要約

これで、ローカルコンピューターの IIS で Contoso 大学を正常に動作させるために必要なすべてのタスクが完了しました。 次のチュートリアルでは、Azure にデプロイすることによって、サイトをパブリックに利用できるようにします。

## <a name="more-information"></a>説明

この例では、Elmah がログファイルを保存できなかった理由が非常に明白でした。 問題の原因が明らかでない場合は、IIS トレースを使用できます。IIS.net サイトの「 [IIS 7 でトレースを使用した失敗した要求のトラブルシューティング」を](https://www.iis.net/learn/troubleshoot/using-failed-request-tracing/troubleshooting-failed-requests-using-tracing-in-iis)参照してください。

アプリケーションプール id にアクセス許可を付与する方法の詳細については、IIS.net サイトの「ファイルシステム Acl を使用した IIS の[アプリケーションプール id](https://www.iis.net/learn/manage/configuring-security/application-pool-identities)と[セキュリティ保護されたコンテンツ](https://www.iis.net/learn/get-started/planning-for-security/secure-content-in-iis-through-file-system-acls)」を参照してください。

> [!div class="step-by-step"]
> [前へ](deploying-to-iis.md)
> [次へ](deploying-to-production.md)
