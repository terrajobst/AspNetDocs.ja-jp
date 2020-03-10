---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/manually-installing-web-packages
title: Web パッケージを手動でインストールする |Microsoft Docs
author: jrjlee
description: このトピックでは、インターネットインフォメーションサービス (IIS) に web 配置パッケージを手動でインポートする方法について説明します。 トピック「Web アプリケーションのビルドとパッケージ化...」
ms.author: riande
ms.date: 05/04/2012
ms.assetid: f11d22a7-5d32-4ad0-8a9b-276460a61c06
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/manually-installing-web-packages
msc.type: authoredcontent
ms.openlocfilehash: f778549d3e26989a2e71ef21171adec521842729
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78514888"
---
# <a name="manually-installing-web-packages"></a>Web パッケージを手動でインストールする

[Jason Lee](https://github.com/jrjlee)

[[Download PDF]\(PDF をダウンロード\)](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> このトピックでは、インターネットインフォメーションサービス (IIS) に web 配置パッケージを手動でインポートする方法について説明します。
> 
> 「 [Web アプリケーションプロジェクトのビルドおよびパッケージ化](building-and-packaging-web-application-projects.md)」では、IIS Web 配置ツール (Web 配置) と Microsoft Build Engine (MSBuild) および Web 発行パイプライン (WPP) を組み合わせて使用して、web アプリケーションプロジェクトを1つの zip ファイルにパッケージ化する方法について説明しています。 このファイルは、web 展開パッケージ (または単に展開パッケージ) として知られています。 web サーバーで web アプリケーションを再作成するために IIS が必要とするすべてのコンテンツと構成情報が含まれています。
> 
> Web 配置パッケージを作成したら、さまざまな方法で IIS サーバーに発行できます。 さまざまなシナリオでは、MSBuild、WPP、Web 配置の統合ポイントを利用して、自動化された、または単一ステップのビルドおよび展開プロセスの一部として Web パッケージをリモートで作成およびインストールします。 このプロセスの詳細については、「 [Web パッケージの展開](deploying-web-packages.md)」を参照してください。 ただし、これは常に可能であるとは限りません。 インターネットに接続された運用環境に web アプリケーションをデプロイするとします。 セキュリティ上の理由から、このような運用環境は、境界ネットワーク (DMZ、非武装地帯、スクリーンサブネットとも呼ばれます) で、ビルドサーバーとは別のサブネット上のファイアウォールの内側に配置される可能性が最も低くなります。 多くの場合、運用環境は別のドメインまたは物理的に分離されたネットワーク上にあります。
> 
> このようなシナリオでは、web パッケージを移行先サーバーに移植し、手動で IIS にインポートするだけのオプションがあります。 このアプローチは自動化されたデプロイを実現していませんが、web アプリケーション&#x2014;を公開するための非常に効果的な方法ですが、単に1つの zip ファイルを web サーバーにコピーし、ウィザードを使用してインポートプロセスを実行できます。

このトピックでは、Fabrikam, Inc. という架空の企業のエンタープライズ展開要件に基づいて、一連のチュートリアルの一部を説明します。このチュートリアルシリーズでは、&#x2014; [Contact Manager ソリューション](the-contact-manager-solution.md)&#x2014;のサンプルソリューションを使用して、ASP.NET MVC 3 アプリケーション、Windows Communication Foundation (WCF) サービス、データベースプロジェクトなど、現実的なレベルの複雑さを持つ web アプリケーションを表します。

## <a name="task-overview"></a>タスクの概要

IIS に web 配置パッケージをインポートするには、次の高レベルのタスクを実行する必要があります。

- MSBuild コマンドライン、チームビルド、または Visual Studio 2010 を使用して、web 配置パッケージを作成します。
- Web パッケージを移行先 web サーバーにコピーします。
- IIS マネージャーのアプリケーションパッケージのインポートウィザードを使用して、web パッケージをインストールし、接続文字列やサービスエンドポイントなどの変数の値を指定します。

このトピックでは、これらの手順を実行する方法について説明します。 このトピックのタスクとチュートリアルでは、web パッケージ、Web 配置、および WPP の概念を理解していることを前提としています。 詳細については、「 [Web アプリケーションプロジェクトのビルドおよびパッケージ化](building-and-packaging-web-application-projects.md)」を参照してください。

> [!NOTE]
> このトピックは、 [Web 配置発行用に Web サーバーを構成する (オフライン展開)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)と共に使用することをお勧めします。これは、必要なコンポーネントをインストールし、パッケージのインポート用に IIS web サイトを準備する方法を説明しています。

## <a name="create-a-web-deployment-package"></a>Web 配置パッケージを作成する

最初のタスクは、デプロイする web アプリケーションプロジェクトの web 配置パッケージを作成することです。 Web パッケージは、さまざまな方法で作成できます。

**方法 1: Visual Studio を使用してビルドプロセスの一部としてパッケージを作成する**

プロジェクトのプロパティページの **[パッケージ化/発行]** タブで、各ビルドの後に web 配置パッケージを作成するように web アプリケーションプロジェクトを構成できます。 このプロセスについ[ては、「Web アプリケーションプロジェクトのビルドとパッケージ化](building-and-packaging-web-application-projects.md)」を参照してください。

**方法 2: MSBuild を使用してビルド処理の一部としてパッケージを作成する**

MSBuild を使用して、カスタム MSBuild プロジェクトファイルまたはコマンドラインから直接 web アプリケーションプロジェクトをビルドする場合は、コマンドに**Deployonbuild = true**および**Deploytarget = package**プロパティを含めることによって、ビルドプロセスの一部として web 配置パッケージを作成できます。 このプロセスの詳細につい[ては、「ビルドプロセスについて](understanding-the-build-process.md)」を参照してください。

**方法 3: Visual Studio でオンデマンドでパッケージを作成する**

Web アプリケーションプロジェクトの web 配置パッケージは、Visual Studio 2010 でいつでも作成できます。 これを行うには、 **[ソリューションエクスプローラー]** ウィンドウで、web アプリケーションプロジェクトを右クリックし、 **[配置パッケージのビルド]** をクリックします。

![](manually-installing-web-packages/_static/image1.png)

**方法 4: コマンドラインからオンデマンドでパッケージを作成する**

MSBuild を使用して web アプリケーションプロジェクトで**パッケージ**ターゲットを呼び出すことにより、コマンドラインから web 配置パッケージを作成できます。 コマンドは次のようになります。

[!code-console[Main](manually-installing-web-packages/samples/sample1.cmd)]

どちらの方法を使用しても、最終的な結果は同じになります。 WPP は、web アプリケーションプロジェクトの出力フォルダーに、さまざまなサポートリソースと共に、web 配置パッケージを zip ファイルとして作成します。

![](manually-installing-web-packages/_static/image2.png)

Web パッケージを手動でインポートすることを計画している場合は、zip ファイルのみが必要です。 このファイルをターゲット web サーバーにコピーし、インポートプロセスを開始します。

## <a name="import-a-web-package-into-iis"></a>IIS への Web パッケージのインポート

ローカルファイルシステムから IIS web サイトに web 配置パッケージをインポートするには、次の手順を実行します。 この手順を実行する前に、次のことを確認してください。

- Web 配置パッケージを web サーバーにコピーしました。
- アプリケーションをホストするように IIS web サーバーを構成しました。

IIS web サーバーを構成して web 配置パッケージをサポートする方法の詳細については、「 [Web 配置の発行用に Web サーバーを構成する (オフライン展開)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)」を参照してください。

**IIS マネージャーを使用して web 配置パッケージをインポートするには**

1. IIS マネージャーの **[接続]** ウィンドウで、iis web サイトを右クリックし、 **[展開]** をポイントして、 **[アプリケーションのインポート]** をクリックします。

    ![](manually-installing-web-packages/_static/image3.png)
2. アプリケーションパッケージのインポートウィザードの **[パッケージの選択]** ページで、web 配置パッケージの場所を参照し、 **[次へ]** をクリックします。
3. **[パッケージの内容の選択]** ページで、不要なコンテンツをすべてオフにし、 **[次へ]** をクリックします。

    ![](manually-installing-web-packages/_static/image4.png)

    > [!NOTE]
    > 多くの場合、web 配置パッケージに含まれるすべてをインポートする必要はありません。 たとえば、関連付けられているデータベースを Web 配置に置き換えることを許可しない場合があります。  
    > **アクセス許可**エントリは、対象のファイルシステムに対してアクセス許可を設定し、アプリケーションプール id が web サイトのコンテンツを格納する物理フォルダーにアクセスできるようにします。 さらに、匿名認証ユーザーには、アプリケーションが Multipurpose Internet Mail Extensions (MIME) 型ファイルを提供できるように、フォルダーに対する読み取りアクセス許可が付与されます。 必要に応じて、これらのエントリを削除し、アクセス許可を手動で構成することもできます。
4. **[アプリケーションパッケージ情報の入力]** ページで、要求された情報を入力します。

    ![](manually-installing-web-packages/_static/image5.png)
5. Web パッケージを作成するときに、WPP はアプリケーションの構成ファイルを分析し、接続文字列やサービスエンドポイントなどの変数を検出します。 この場合、次のようになります。

    1. **アプリケーションパス**は、アプリケーションをインストールする IIS パスです。 この設定は、WPP によって作成されるすべての展開パッケージに共通です。
    2. **Contactservice サービスエンドポイントアドレス**は、アプリケーションがデプロイされた WCF サービスとの通信に使用するアドレスです。 この*設定は、web.config ファイルの*エントリに対応しています。
    3. 最初の**接続文字列**の設定は、アプリケーションに関連付けられているデータベース (この場合は ASP.NET メンバーシップデータベース) をデプロイするために使用する必要が Web 配置接続文字列です。 この設定は、Visual Studio の **[SQL のパッケージ化/発行]** タブの設定に対応しています。
    4. 2番目の**接続文字列**設定は、アプリケーションが稼働しているときにデータベースとの通信に実際に使用する接続文字列です。 これ*は、web.config ファイル内*の接続文字列エントリに対応します。

        > [!NOTE]
        > これらのパラメーターの取得元の詳細については、「 [Web パッケージ配置のパラメーターの構成](configuring-parameters-for-web-package-deployment.md)」を参照してください。
6. **[次へ]** をクリックします。
7. この web サイトに初めてアプリケーションを展開した場合は、インストールの前に既存のコンテンツをすべて削除するかどうかを指定するように求められます。 要件に適したオプションを選択し、 **[次へ]** をクリックします。

    ![](manually-installing-web-packages/_static/image6.png)
8. IIS でパッケージのインストールが完了したら、 **[完了]** をクリックします。

    ![](manually-installing-web-packages/_static/image7.png)

この時点で、web アプリケーションが IIS に正常に発行されました。

## <a name="conclusion"></a>まとめ

このトピックでは、IIS マネージャーを使用して IIS web サイトに web 配置パッケージをインポートする方法について説明します。 この web アプリケーションの公開方法は、セキュリティまたはインフラストラクチャの制約によってリモート展開が不可能または望ましくない場合に適しています。

## <a name="further-reading"></a>参考資料

Web パッケージの手動インポートをサポートするように IIS web サーバーを構成する方法については、「 [Web 配置の発行用に Web サーバーを構成する (オフライン展開)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)」を参照してください。 Web パッケージの配置に関する一般的なガイダンスについては、「[チュートリアル: Web 配置パッケージを使用した Web アプリケーションプロジェクトの配置 (パート 1/4)](https://msdn.microsoft.com/library/dd483479.aspx)」を参照してください。

> [!div class="step-by-step"]
> [[戻る]](creating-and-running-a-deployment-command-file.md)
