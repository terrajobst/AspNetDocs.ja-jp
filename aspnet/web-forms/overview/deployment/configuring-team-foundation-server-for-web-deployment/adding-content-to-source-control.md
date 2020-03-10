---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/adding-content-to-source-control
title: ソース管理へのコンテンツの追加 |Microsoft Docs
author: jrjlee
description: このトピックでは、Team Foundation Server (TFS) 2010 でソース管理にコンテンツを追加する方法について説明します。 ここでは、ソリューションとプロジェクトをチームに追加する方法について説明します。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 86c14aab-c2dd-4f73-b40c-c6d52fa44950
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/adding-content-to-source-control
msc.type: authoredcontent
ms.openlocfilehash: 16073dd2fb0ea1cc4ddbc94c843181933dc174c1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78515110"
---
# <a name="adding-content-to-source-control"></a>ソース管理にコンテンツを追加する

[Jason Lee](https://github.com/jrjlee)

[[Download PDF]\(PDF をダウンロード\)](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> このトピックでは、Team Foundation Server (TFS) 2010 でソース管理にコンテンツを追加する方法について説明します。 TFS のチームプロジェクトにソリューションとプロジェクトを追加する方法について説明し、フレームワークやアセンブリなどの外部の依存関係をソース管理に追加する方法について説明します。

このトピックでは、Fabrikam, Inc. という架空の企業のエンタープライズ展開要件に基づいて、一連のチュートリアルの一部を説明します。このチュートリアルシリーズでは、&#x2014; [Contact Manager ソリューション](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;のサンプルソリューションを使用して、ASP.NET MVC 3 アプリケーション、Windows Communication Foundation (WCF) サービス、データベースプロジェクトなど、現実的なレベルの複雑さを持つ web アプリケーションを表します。

## <a name="task-overview"></a>タスクの概要

ほとんどの場合、開発者チームのすべてのメンバーは、ソース管理にコンテンツを追加できる必要があります。 TFS のソース管理にソリューションを追加するには、次の大まかな手順を実行する必要があります。

- チームプロジェクトに接続します。
- サーバー上のチームプロジェクトフォルダー構造をローカルコンピューター上のフォルダー構造にマップします。
- ソリューションとその内容をソース管理に追加します。
- ソース管理に外部依存関係を追加します。

このトピックでは、これらの手順を実行する方法について説明します。

このトピックのタスクとチュートリアルでは、コンテンツを管理するための新しい TFS チームプロジェクトが既に作成されていることを前提としています。 新しいチームプロジェクトの作成の詳細については、「 [TFS でのチームプロジェクトの作成](creating-a-team-project-in-tfs.md)」を参照してください。

### <a name="who-performs-these-procedures"></a>これらの手順を実行するユーザー

ほとんどの場合、開発者チームのすべてのメンバーが、特定のチームプロジェクト内のコンテンツを追加および変更できる必要があります。

## <a name="connect-to-a-team-project-and-create-a-folder-mapping"></a>チームプロジェクトに接続してフォルダーマッピングを作成する

ソース管理にコンテンツを追加する前に、チームプロジェクトに接続し、サーバー上のフォルダー構造とローカルコンピューター上のファイルシステムとの間にマッピングを作成する必要があります。

**チームプロジェクトに接続してローカルパスをマップするには**

1. 開発者ワークステーションで、Visual Studio 2010 を開きます。
2. Visual Studio の **[チーム]** メニューで、[ **Team Foundation Server に接続] を**クリックします。

    > [!NOTE]
    > TFS サーバーへの接続が既に構成されている場合は、手順3-6 を省略できます。
3. **[チームプロジェクトへの接続]** ダイアログボックスで、 **[サーバー]** をクリックします。
4. **[Team Foundation Server の追加と削除]** ダイアログボックスで、 **[追加]** をクリックします。
5. **[Team Foundation Server の追加]** ダイアログボックスで、TFS インスタンスの詳細を指定し、 **[OK]** をクリックします。

    ![](adding-content-to-source-control/_static/image1.png)
6. **[Team Foundation Server の追加と削除]** ダイアログボックスで、 **[閉じる]** をクリックします。
7. **[チームプロジェクトへの接続]** ダイアログボックスで、接続する TFS インスタンスを選択し、チームプロジェクトコレクション を選択して、追加するチームプロジェクトを選択し、 **[接続]** をクリックします。

    ![](adding-content-to-source-control/_static/image2.png)
8. **[チームエクスプローラー]** ウィンドウで、チームプロジェクトを展開し、 **[ソース管理]** をダブルクリックします。

    ![](adding-content-to-source-control/_static/image3.png)
9. **[ソース管理エクスプローラー]** タブで、 **[マップされていません]** をクリックします。

    ![](adding-content-to-source-control/_static/image4.png)
10. **[マップ]** ダイアログボックスの **[ローカルフォルダー]** ボックスで、チームプロジェクトのルートフォルダーとして機能するローカルフォルダーを参照 (または作成) してから、 **[マップ]** をクリックします。

    ![](adding-content-to-source-control/_static/image5.png)
11. ソースファイルのダウンロードを求めるメッセージが表示されたら、[**はい]** をクリックします。

    ![](adding-content-to-source-control/_static/image6.png)

この時点で、チームプロジェクトのサーバー側フォルダーが、開発者ワークステーションのローカルフォルダーにマップされています。 また、チームプロジェクトの既存のコンテンツをローカルフォルダー構造にダウンロードしました。 これで、ソース管理に独自のコンテンツを追加できるようになりました。

## <a name="add-projects-and-solutions-to-source-control"></a>ソース管理へのプロジェクトとソリューションの追加

ソース管理にプロジェクトとソリューションを追加するには、まず、ローカルコンピューター上のチームプロジェクトのマップされたフォルダーに移動する必要があります。 その後、コンテンツをチェックインして、追加したサーバーとサーバーとの同期をとることができます。

**ソース管理にプロジェクトを追加するには**

1. 開発者ワークステーションで、チームプロジェクトのマップされたフォルダー構造内の適切な場所にプロジェクトとソリューションを移動します。

    > [!NOTE]
    > 多くの組織では、プロジェクトとソリューションをソース管理でどのように編成するかをお勧めします。 フォルダーを構造化する方法のガイダンスについては、「[方法: Team Foundation Server でソース管理フォルダーを構成](https://msdn.microsoft.com/library/bb668992.aspx)する」を参照してください。
2. Visual Studio 2010 でソリューションを開きます。
3. **[ソリューションエクスプローラー]** ウィンドウで、ソリューションを右クリックし、[**ソリューションをソース管理に追加] を**クリックします。

    ![](adding-content-to-source-control/_static/image7.png)

    > [!NOTE]
    > 場合によっては、TFS でコンテンツを構造化する方法によっては、ソース管理にプロジェクトを個別に追加して、ソースコードの編成方法をより細かく制御できるようにすることが必要になる場合があります。
4. **[ソース管理エクスプローラー]** タブに、チームプロジェクトのサーバーフォルダー構造内に追加したコンテンツが表示されていることを確認します。

    ![](adding-content-to-source-control/_static/image8.png)

    > [!NOTE]
    > **[ソース管理エクスプローラー]** タブには、ローカルファイルシステム上のマップされたフォルダーにソリューションを追加したため、メッセージが表示されません。 ソリューションがマップされていない場所にある場合は、TFS とローカルファイルシステムの両方でフォルダーの場所を指定するように求められます。
5. **[ソース管理エクスプローラー]** タブの **[フォルダー]** ウィンドウで、チームプロジェクト ( **contactmanager**など) を右クリックし、 **[保留中の変更をチェックイン]** をクリックします。
6. **[チェックイン-ソースファイル]** ダイアログボックスで、コメントを入力し、 **[チェックイン]** をクリックします。

    ![](adding-content-to-source-control/_static/image9.png)

この時点で、ソリューションを TFS のソース管理に追加しました。

## <a name="add-external-dependencies-to-source-control"></a>ソース管理への外部依存関係の追加

ソース管理にプロジェクトまたはソリューションを追加すると、プロジェクトまたはソリューション内のファイルとフォルダーも追加されます。 ただし、多くの場合、プロジェクトとソリューションは、ローカルアセンブリなどの外部の依存関係を使用して正常に機能することにも依存します。 このようなリソースをソース管理に追加して、チームビルドと開発者チームの他のメンバーがコードを正常にビルドできるようにする必要があります。

たとえば、Contact Manager サンプルソリューションのフォルダー構造には、packages という名前のフォルダーがあります。 これには、アセンブリと、ADO.NET Entity Framework 4.1 のさまざまなサポートリソースが含まれます。 Packages フォルダーは Contact Manager ソリューションの一部ではありませんが、ソリューションは正常にビルドされません。 チームビルドでソリューションをビルドできるようにするには、[パッケージ] フォルダーをソース管理に追加する必要があります。

> [!NOTE]
> Packages フォルダーを含めることは、Visual Studio 2010 用の NuGet 拡張機能を使用して、Entity Framework、または同様のリソースをソリューションに追加したときの動作です。

**ソース管理にプロジェクト以外のコンテンツを追加するには**

1. 追加する項目 (packages フォルダーなど) が、ローカルファイルシステム上のマップされたフォルダー内の適切な場所にあることを確認します。
2. Visual Studio 2010 の **[チームエクスプローラー]** ウィンドウで、チームプロジェクトを展開し、 **[ソース管理]** をダブルクリックします。

    ![](adding-content-to-source-control/_static/image10.png)
3. **[ソース管理エクスプローラー]** タブの **[フォルダー]** ウィンドウで、追加する項目が含まれているフォルダーを選択します。
4. **[フォルダーへの項目の追加]** ボタンをクリックします。

    ![](adding-content-to-source-control/_static/image11.png)
5. **[ソース管理に追加]** ダイアログボックスで、追加するフォルダーを選択し、 **[次へ]** をクリックします。

    ![](adding-content-to-source-control/_static/image12.png)
6. **[除外する項目]** タブで、自動的に除外された必要な項目 (アセンブリなど) を選択し、 **[項目を含める]** をクリックします。

    ![](adding-content-to-source-control/_static/image13.png)
7. **[追加する項目]** タブで、含めるすべてのファイルが表示されていることを確認し、 **[完了]** をクリックします。

    ![](adding-content-to-source-control/_static/image14.png)
8. **[ソース管理エクスプローラー]** ウィンドウで、 **[チェックイン]** ボタンをクリックします。

    ![](adding-content-to-source-control/_static/image15.png)
9. **[チェックイン-ソースファイル]** ダイアログボックスで、コメントを入力し、 **[チェックイン]** をクリックします。

この時点で、ソリューションの外部の依存関係がソース管理に追加されました。

## <a name="conclusion"></a>まとめ

このトピックでは、チームプロジェクトに接続する方法、フォルダー構造をマップする方法、およびソース管理にコンテンツを追加する方法について説明します。 ソース管理下の項目を操作する方法の詳細については、「[バージョン管理の使用](https://msdn.microsoft.com/library/ms181368.aspx)」を参照してください。

次のトピック「 [Web 配置用の Tfs ビルドサーバーの構成](configuring-a-tfs-build-server-for-web-deployment.md)」では、Tfs チームビルドサーバーを準備してソリューションをビルドおよび配置する方法について説明します。

## <a name="further-reading"></a>参考資料

TFS でソース管理を操作する方法の詳細については、「[バージョン管理の使用](https://msdn.microsoft.com/library/ms181368.aspx)」を参照してください。

> [!div class="step-by-step"]
> [前へ](creating-a-team-project-in-tfs.md)
> [次へ](configuring-a-tfs-build-server-for-web-deployment.md)
