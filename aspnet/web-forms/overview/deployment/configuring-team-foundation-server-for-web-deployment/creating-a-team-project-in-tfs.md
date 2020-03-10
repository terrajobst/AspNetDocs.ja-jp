---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/creating-a-team-project-in-tfs
title: TFS でのチームプロジェクトの作成 |Microsoft Docs
author: jrjlee
description: このトピックでは、Team Foundation Server (TFS) 2010 で新しいチームプロジェクトを作成する方法について説明します。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: b28d3e2d-0bb4-4e29-a780-af810b964722
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/creating-a-team-project-in-tfs
msc.type: authoredcontent
ms.openlocfilehash: d12e0636ce3b6239d125305db4354278f9f24960
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78519562"
---
# <a name="creating-a-team-project-in-tfs"></a>TFS でチーム プロジェクトを作成する

[Jason Lee](https://github.com/jrjlee)

[[Download PDF]\(PDF をダウンロード\)](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> このトピックでは、Team Foundation Server (TFS) 2010 で新しいチームプロジェクトを作成する方法について説明します。

このトピックでは、Fabrikam, Inc. という架空の企業のエンタープライズ展開要件に基づいて、一連のチュートリアルの一部を説明します。このチュートリアルシリーズでは、&#x2014; [Contact Manager ソリューション](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;のサンプルソリューションを使用して、ASP.NET MVC 3 アプリケーション、Windows Communication Foundation (WCF) サービス、データベースプロジェクトなど、現実的なレベルの複雑さを持つ web アプリケーションを表します。

## <a name="task-overview"></a>タスクの概要

TFS で新しいチームプロジェクトをプロビジョニングして使用するには、次の大まかな手順を実行する必要があります。

- 新しいチームプロジェクトを作成するユーザーにアクセス許可を付与します。
- チームプロジェクトを作成します。
- プロジェクトで作業するチームメンバーにアクセス許可を付与します。
- 一部のコンテンツをチェックインします。

このトピックでは、これらの手順を実行する方法について説明します。また、各手順の責任を負う可能性のあるユーザーとジョブの役割を示します。 組織の構造によっては、これらの各タスクが別のユーザーの責任であることに注意してください。

このトピックのタスクとチュートリアルでは、TFS をインストールして構成したこと、および構成プロセスの一環としてチームプロジェクトコレクションを作成したことを前提としています。 これらの前提の詳細と、シナリオに関する一般的な背景情報については、「 [Configure a TFS Build Server For Web Deployment](configuring-a-tfs-build-server-for-web-deployment.md)」を参照してください。

## <a name="grant-permissions-to-the-team-project-creator"></a>チームプロジェクト作成者にアクセス許可を付与する

新しいチームプロジェクトを作成するには、次のアクセス許可が必要です。

- TFS アプリケーション層に対する "**新しいプロジェクトの作成**" アクセス許可が必要です。 通常、このアクセス許可を付与するには、**プロジェクトコレクション管理者**TFS グループにユーザーを追加します。 **Team Foundation 管理者**グローバルグループには、このアクセス許可も含まれています。
- TFS チームプロジェクトコレクションに対応する SharePoint サイトコレクション内に新しいチームサイトを作成するためのアクセス許可が必要です。 通常、このアクセス許可を付与するには、SharePoint サイトコレクションに対する**フルコントロール**権限を持つ sharepoint グループにユーザーを追加します。
- SQL Server Reporting Services の機能を使用している場合は、Reporting Services の**Team Foundation コンテンツマネージャー**ロールのメンバーである必要があります。

### <a name="who-performs-these-procedures"></a>これらの手順を実行するユーザー

通常、TFS の配置を管理するユーザーまたはグループは、これらの手順も実行します。

これはアクセス許可の高い特権セットであるため、通常、新しいチームプロジェクトは、TFS 配置の管理を担当する少数のユーザーによって作成されます。 通常、開発者には、新しいチームプロジェクトを作成するために必要なアクセス許可が付与されません。

### <a name="grant-permissions-in-tfs"></a>TFS でのアクセス許可の付与

ユーザーが新しいチームプロジェクトを作成できるようにするには、最初の大まかなタスクとして、チームプロジェクトコレクションの**プロジェクトコレクション管理者**グループにユーザーを追加します。

**プロジェクトコレクション管理者グループにユーザーを追加するには**

1. TFS サーバーで、 **[スタート]** メニューの すべての **[プログラム]** をポイントし、 **[Microsoft Team Foundation Server 2010]** をクリックして、 **[Team Foundation 管理コンソール]** をクリックします。
2. ナビゲーションツリービューで、 **[アプリケーション層]** を展開し、 **[チームプロジェクトコレクション]** をクリックします。

    ![](creating-a-team-project-in-tfs/_static/image1.png)
3. **[チームプロジェクトコレクション]** ウィンドウで、管理するチームプロジェクトコレクションを選択します。

    ![](creating-a-team-project-in-tfs/_static/image2.png)
4. **[全般]** タブで、 **[グループメンバーシップ]** をクリックします。

    ![](creating-a-team-project-in-tfs/_static/image3.png)
5. **[グローバルグループ]** ダイアログボックスで、**プロジェクトコレクション管理者**グループを選択し、 **[プロパティ]** をクリックします。
6. **[Team Foundation Server グループのプロパティ]** ダイアログボックスで、 **[Windows ユーザーまたはグループ]** を選択し、 **[追加]** をクリックします。

    ![](creating-a-team-project-in-tfs/_static/image4.png)
7. **[ユーザー、コンピューター、またはグループの選択]** ダイアログボックスで、新しいチームプロジェクトを作成できるようにするユーザーのユーザー名を入力し、 **[名前の確認]** をクリックして、 **[OK]** をクリックします。

    ![](creating-a-team-project-in-tfs/_static/image5.png)
8. **[Team Foundation Server グループのプロパティ]** ダイアログボックスで、[ **OK]** をクリックします。
9. **[グローバルグループ]** ダイアログボックスで、 **[閉じる]** をクリックします。

### <a name="grant-permissions-in-sharepoint-services"></a>SharePoint Services で権限を付与する

次に、TFS チームプロジェクトコレクションに対応する SharePoint サイトコレクションに新しいチームサイトを作成するためのアクセス許可をユーザーに付与する必要があります。

**SharePoint サイトコレクションに対するフルコントロール権限を付与するには**

1. Team Foundation Server 管理コンソールの **[チームプロジェクトコレクション]** ページで、管理するチームプロジェクトコレクションを選択します。
2. **[SharePoint サイト]** タブで、現在の既定の**サイトの場所**の URL の値を確認します。

    ![](creating-a-team-project-in-tfs/_static/image6.png)
3. Internet Explorer を開き、手順2でメモした URL にアクセスします。

    > [!NOTE]
    > チームプロジェクトコレクションを作成したユーザーとして Windows にログオンしていない場合は、続行するために、このユーザーとして SharePoint にサインインする必要があります。
4. **[サイトの操作]** メニューの **[サイトの設定]** をクリックします。

    ![](creating-a-team-project-in-tfs/_static/image7.png)
5. **[サイトの設定]** ページの **[ユーザーとアクセス許可]** で、 **[ユーザーとグループ]** をクリックします。
6. 左側のナビゲーションパネルで、 **[グループ]** をクリックします。

    ![](creating-a-team-project-in-tfs/_static/image8.png)
7. **[People And groups: すべてのグループ]** ページで、 **[このサイトのグループをセットアップする]** をクリックします。

    ![](creating-a-team-project-in-tfs/_static/image9.png)

   > [!NOTE]
   > 2つの HTTP エンコードのバグにより、 <strong>http 404 Not Found</strong>エラーが発生することがあります。 このエラーが発生した場合は、URL を次のように置き換えます。   
   > `[site_collection_URL]/_layouts/permsetup.aspx`次に例を示します。  
   > `http://tfs/sites/Fabrikam%20Web%20Projects/_layouts/permsetup.aspx` 
8. **[このサイトのグループの設定]** ページで、 **[所有者]** グループにチームプロジェクトを作成するユーザーを追加し、[ **OK]** をクリックします。

    ![](creating-a-team-project-in-tfs/_static/image10.png)

チームプロジェクトコレクション内でユーザーが新しいチームプロジェクトを作成できるようにする方法の詳細については、「[チームプロジェクトコレクションの管理アクセス許可を設定](https://msdn.microsoft.com/library/dd547204.aspx)する」を参照してください。

## <a name="create-a-new-team-project-and-add-users"></a>新しいチームプロジェクトを作成してユーザーを追加する

必要なアクセス許可が得られたら、Visual Studio 2010 の **[チームエクスプローラー]** ウィンドウを使用して、新しいチームプロジェクトを作成できます。 この方法では、必要なすべての情報を収集し、TFS、SharePoint、および SQL Server Reporting Services で必要なタスクを実行するウィザードが提供されます。 また、新しいチームプロジェクトに対するアクセス許可を開発者チームのメンバーに付与して、コンテンツを追加および変更できるようにする必要もあります。

### <a name="who-performs-these-procedures"></a>これらの手順を実行するユーザー

通常、TFS 管理者または開発者チームリーダーは、これらの手順を実行します。

### <a name="create-a-new-team-project"></a>新しいチームプロジェクトの作成

次の手順では、TFS 2010 で新しいチームプロジェクトを作成する方法について説明します。

**新しいチームプロジェクトを作成するには**

1. **[スタート]** ボタンをクリックし、 **[すべてのプログラム]** をポイントします。次に、 **[Microsoft Visual Studio 2010]** をクリックし**Microsoft Visual Studio 2010**を右クリックし、 **[管理者として実行]** をクリックします。

    > [!NOTE]
    > 管理者として Visual Studio 2010 を実行していない場合、新しいチームプロジェクトウィザードは、最後の手順で失敗します。
2. **[ユーザー アカウント制御]** ダイアログ ボックスが表示されたら、 **[はい]** をクリックします。
3. Visual Studio の **[チーム]** メニューで、[ **Team Foundation Server に接続] を**クリックします。

    > [!NOTE]
    > TFS サーバーへの接続が既に構成されている場合は、手順4-7 を省略できます。
4. **[チームプロジェクトへの接続]** ダイアログボックスで、 **[サーバー]** をクリックします。
5. **[Team Foundation Server の追加と削除]** ダイアログボックスで、 **[追加]** をクリックします。
6. **[Team Foundation Server の追加]** ダイアログボックスで、TFS インスタンスの詳細を指定し、 **[OK]** をクリックします。

    ![](creating-a-team-project-in-tfs/_static/image11.png)
7. **[Team Foundation Server の追加と削除]** ダイアログボックスで、 **[閉じる]** をクリックします。
8. **[チームプロジェクトへの接続]** ダイアログボックスで、接続先の TFS インスタンスを選択し、追加するチームプロジェクトコレクションを選択して、 **[接続]** をクリックします。

    ![](creating-a-team-project-in-tfs/_static/image12.png)
9. **チームエクスプローラー** ウィンドウで、チームプロジェクトコレクション を右クリックし、**新しいチームプロジェクト** をクリックします。

    ![](creating-a-team-project-in-tfs/_static/image13.png)
10. **[新しいチームプロジェクト]** ダイアログボックスで、チームプロジェクトの名前と説明を入力し、 **[次へ]** をクリックします。

    > [!NOTE]
    > チームプロジェクトにスペースが含まれている場合は、インターネットインフォメーションサービス (IIS) Web 配置ツール (Web 配置) を使用して出力パスからパッケージを配置すると、いくつかの問題が発生する可能性があります。 パス内のスペースを使用すると、Web 配置コマンドの実行が難しくなります。

    ![](creating-a-team-project-in-tfs/_static/image14.png)
11. **[プロセステンプレートの選択]** ページで、開発プロセスの管理に使用するプロセステンプレートを選択し、 **[次へ]** をクリックします。

    > [!NOTE]
    > TFS のプロセステンプレートの詳細については、「[プロセステンプレートとツール](https://msdn.microsoft.com/vstudio/aa718795)」を参照してください。
12. **[チームサイトの設定]** ページで、既定の設定を変更せずにそのまま使用し、 **[次へ]** をクリックします。
13. この設定は、TFS チームプロジェクトに関連付けられている SharePoint チームサイトを作成または識別します。 開発チームは、このサイトを使用して、ドキュメントを管理したり、ディスカッションスレッドに参加したり、wiki ページを作成したり、コードに関連しない他のさまざまなタスクを実行したりできます。 詳細については、「 [SharePoint 製品と Team Foundation Server の間の相互作用](https://msdn.microsoft.com/library/ms253177.aspx)」を参照してください。
14. **[ソース管理の設定の指定]** ページで、既定の設定を変更せずにそのまま使用し、 **[次へ]** をクリックします。
15. この設定により、コンテンツのルートフォルダーとして機能する TFS フォルダー階層内の場所が識別または作成されます。
16. **[チームプロジェクト設定の確認]** ページで、 **[完了]** をクリックします。
17. 新しいチームプロジェクトが正常に作成されたら、 **[作成されたチームプロジェクト]** ページで **[閉じる]** をクリックします。

### <a name="add-users-to-a-team-project"></a>チームプロジェクトへのユーザーの追加

新しいチームプロジェクトを作成したので、ユーザーにアクセス許可を付与して、コンテンツの追加と共同作業を開始できるようにします。

**チームプロジェクトにユーザーを追加するには**

1. Visual Studio 2010 の **[チームエクスプローラー]** ウィンドウで、チームプロジェクトを右クリックし、 **[チームプロジェクトの設定]** をポイントして、 **[グループメンバーシップ]** をクリックします。

    ![](creating-a-team-project-in-tfs/_static/image15.png)
2. ユーザーがソース管理でコードの追加、変更、および削除を行えるようにするには、**共同**作成者グループに追加する必要があります。
3. **[プロジェクトグループ]** ダイアログボックスで、 **[共同]** 作成者 グループを選択し、 **[プロパティ]** をクリックします。

    ![](creating-a-team-project-in-tfs/_static/image16.png)
4. **[Team Foundation Server グループのプロパティ]** ダイアログボックスで、 **[Windows ユーザーまたはグループ]** を選択し、 **[追加]** をクリックします。

    ![](creating-a-team-project-in-tfs/_static/image17.png)
5. **[ユーザー、コンピューター、またはグループの選択]** ダイアログボックスで、チームプロジェクトに追加するユーザーのユーザー名を入力し、 **[名前の確認]** をクリックして、 **[OK]** をクリックします。

    ![](creating-a-team-project-in-tfs/_static/image18.png)
6. **[Team Foundation Server グループのプロパティ]** ダイアログボックスで、[ **OK]** をクリックします。
7. **[プロジェクトグループ]** ダイアログボックスで、 **[閉じる]** をクリックします。

## <a name="conclusion"></a>まとめ

この時点で、新しいチームプロジェクトを使用する準備ができました。開発者チームは、コンテンツの追加と開発プロセスのコラボレーションを開始できます。

次のトピック「[ソース管理へのコンテンツの追加](adding-content-to-source-control.md)」では、ソース管理にコンテンツを追加する方法について説明します。

## <a name="further-reading"></a>参考資料

TFS でチームプロジェクトを作成するための広範なガイダンスについては、「[チームプロジェクトの作成](https://msdn.microsoft.com/library/ms181477(v=VS.100).aspx)」を参照してください。 チームプロジェクトコレクション内でユーザーが新しいチームプロジェクトを作成できるようにする方法の詳細については、「[チームプロジェクトコレクションの管理アクセス許可を設定](https://msdn.microsoft.com/library/dd547204.aspx)する」を参照してください。 チームプロジェクトへのユーザーの追加の詳細については、「[チームプロジェクトへのユーザーの追加](https://msdn.microsoft.com/library/bb558971.aspx)」を参照してください。

> [!div class="step-by-step"]
> [前へ](configuring-team-foundation-server-for-web-deployment.md)
> [次へ](adding-content-to-source-control.md)
