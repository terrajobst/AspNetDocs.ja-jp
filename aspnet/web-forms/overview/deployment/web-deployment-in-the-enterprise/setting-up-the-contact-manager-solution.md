---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/setting-up-the-contact-manager-solution
title: Contact Manager ソリューションを設定する |Microsoft Docs
author: jrjlee
description: このトピックでは、Contact Manager ソリューションをダウンロードし、開発者のワークステーションでローカルに実行するように構成する方法について説明します。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 200b973c-776b-4a9b-9e82-39fda6120a52
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/setting-up-the-contact-manager-solution
msc.type: authoredcontent
ms.openlocfilehash: d9774ee01cb0515d7e733b24baa661f2648bd7c4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78511162"
---
# <a name="setting-up-the-contact-manager-solution"></a>連絡先マネージャー ソリューションを設定する

[Jason Lee](https://github.com/jrjlee)

[[Download PDF]\(PDF をダウンロード\)](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> このトピックでは、Contact Manager ソリューションをダウンロードし、開発者のワークステーションでローカルに実行するように構成する方法について説明します。

## <a name="system-requirements"></a>システム要件

Contact Manager ソリューションをローカルで実行し、このチュートリアルで説明されている他のタスクを実行するには、このソフトウェアを developer ワークステーションにインストールする必要があります。

- Visual Studio 2010 Service Pack 1、Premium、または Ultimate Edition
- インターネット インフォメーション サービス (IIS) 7.5 Express
- SQL Server Express 2008 R2
- IIS Web 配置ツール (Web 配置) 2.1 以降
- ASP.NET 4.0
- ASP.NET MVC 3
- .NET Framework 4
- .NET Framework 3.5 SP1

Visual Studio 2010 を除き、 [Web Platform Installer](https://go.microsoft.com/?linkid=9805118)を使用して、これらの製品とコンポーネントの最新バージョンをダウンロードしてインストールすることができます。

## <a name="download-and-extract-the-solution"></a>ソリューションのダウンロードと抽出

Contact Manager サンプル[アプリケーションは、MSDN コードギャラリーから](https://code.msdn.microsoft.com/Deploying-Web-Applications-9d9093c0)ダウンロードできます。

## <a name="configure-and-run-the-solution"></a>ソリューションを構成して実行する

ローカルコンピューターで Contact Manager ソリューションを構成して実行するには、次の大まかな手順を実行する必要があります。

1. まだ持っていない場合は、メンバーシップとロールの管理機能が有効になっているローカルの ASP.NET アプリケーションサービスデータベースを作成します。
2. ローカル SQL Server Express インスタンスを指すように、web.config ファイル内の接続文字列を編集*します。*
3. Visual Studio 2010 からソリューションを実行します。

このセクションの残りの部分では、これらの各タスクを実行する方法について詳しく説明します。

**アプリケーションサービスデータベースを作成するには**

1. Visual Studio 2010 コマンド プロンプトを開きます。 これを行うには、 **[スタート]** ボタンをクリックし、 **[すべてのプログラム]** をポイントし、 **[Microsoft Visual Studio 2010]** をクリックし、 **[Visual Studio Tools]** をクリックして、 **[Visual Studio コマンドプロンプト (2010)]** をクリックします。
2. コマンドプロンプトで、次のコマンドを入力し、enter キーを押します。

    [!code-console[Main](setting-up-the-contact-manager-solution/samples/sample1.cmd)]

    1. **– C**スイッチを使用して、データベースサーバーの接続文字列を指定します。
    2. **– A**スイッチを使用して、データベースに追加するアプリケーションサービスの機能を指定します。 この場合、 **m**はメンバーシッププロバイダーのサポートを追加することを示し、 **r**はロールマネージャーのサポートを追加することを示します。
    3. アプリケーションサービスデータベースの名前を指定するには、 **– d**スイッチを使用します。 このスイッチを省略すると、既定の名前が**aspnetdb.mdf**のデータベースが作成されます。
3. データベースが正常に作成されると、コマンドプロンプトに確認メッセージが表示されます。

    ![](setting-up-the-contact-manager-solution/_static/image1.png)

> [!NOTE]
> Aspnet\_regsql ユーティリティの詳細については、「 [ASP.NET SQL Server Registration Tool (aspnet\_regsql .exe)](https://msdn.microsoft.com/library/ms229862(v=vs.100).aspx)」を参照してください。

次の手順では、Contact Manager ソリューション内の接続文字列が SQL Server Express のローカルインスタンスを指していることを確認します。

**接続文字列を更新するには**

1. Visual Studio 2010 で Contact Manager ソリューションを開きます。
2. **[ソリューションエクスプローラー]** ウィンドウで、 **[Contactmanager. Mvc]** プロジェクトを展開し、 **[web.config]** ノードをダブルクリックします。

    > [!NOTE]
    > ContactManager Mvc プロジェクトには *、2つの web.config ファイル*が含まれています。 プロジェクトレベルのファイルを編集する必要があります。

    ![](setting-up-the-contact-manager-solution/_static/image2.png)
3. **ConnectionStrings**要素で、 **applicationservices**という名前の接続文字列がローカルの ASP.NET アプリケーションサービスデータベースを指していることを確認します。

    [!code-xml[Main](setting-up-the-contact-manager-solution/samples/sample2.xml)]
4. **[ソリューションエクスプローラー]** ウィンドウで、 **[Contactmanager. サービス]** プロジェクトを展開し、 **[web.config]** ノードをダブルクリックします。

    ![](setting-up-the-contact-manager-solution/_static/image3.png)
5. **ConnectionStrings**要素の**contactmanagercontext**という名前の接続文字列で、**データソース**プロパティが SQL Server Express のローカルインスタンスに設定されていることを確認します。 接続文字列内の他のものを変更する必要はありません。

    [!code-xml[Main](setting-up-the-contact-manager-solution/samples/sample3.xml)]
6. 開いているすべてのファイルを保存します。

これで、ローカルコンピューターで Contact Manager ソリューションを実行する準備が整いました。

> [!NOTE]
> 最初にアプリケーションサービスデータベースを作成せずにこれらの手順を実行すると、ASP.NET によって初めてユーザーを作成しようとしたときにデータベースが作成されます。 ただし、データベースを手動で作成すると、サポートするアプリケーションサービスの機能セットをはるかに細かく制御できます。

**Contact Manager ソリューションを実行するには**

1. Visual Studio 2010 で、F5 キーを押します。
2. Internet Explorer が起動し、Contact Manager ASP.NET MVC 3 アプリケーションの URL が要求されます。 既定では、アプリケーションは **[すべての連絡先]** ページを表示します。

    ![](setting-up-the-contact-manager-solution/_static/image4.png)
3. いくつかの連絡先を追加し、アプリケーションが期待どおりに動作することを確認します。

    ![](setting-up-the-contact-manager-solution/_static/image5.png)
4. `http://localhost:50114/Account/Register` を参照します (別のポートでアプリケーションをホストしている場合は、URL を調整します)。 ユーザー名、電子メールアドレス、およびパスワードを追加し、アカウントを正常に登録できることを確認します。

    ![](setting-up-the-contact-manager-solution/_static/image6.png)
5. `http://localhost:50114/Account/LogOn` を参照します (別のポートでアプリケーションをホストしている場合は、URL を調整します)。 先ほど作成したアカウントを使用してログオンできることを確認します。

    ![](setting-up-the-contact-manager-solution/_static/image7.png)
6. Internet Explorer を閉じて、デバッグを停止します。

## <a name="conclusion"></a>まとめ

この時点で、Contact Manager ソリューションはローカルコンピューターで実行するように完全に構成されている必要があります。 このチュートリアルの他のトピックを使用して作業する場合は、このソリューションを参照として使用できます。

次のトピック「[プロジェクトファイルについ](understanding-the-project-file.md)て」では、Contact Manager ソリューション内でカスタム Microsoft Build Engine (MSBuild) プロジェクトファイルを使用して、デプロイプロセスを制御する方法について説明します。

> [!div class="step-by-step"]
> [前へ](the-contact-manager-solution.md)
> [次へ](understanding-the-project-file.md)
