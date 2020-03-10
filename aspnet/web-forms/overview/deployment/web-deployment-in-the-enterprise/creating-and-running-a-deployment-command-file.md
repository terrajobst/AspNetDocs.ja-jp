---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/creating-and-running-a-deployment-command-file
title: 配置コマンドファイルを作成して実行する |Microsoft Docs
author: jrjlee
description: このトピックでは、Microsoft Build Engine (MSBuild) プロジェクトファイルを使用してデプロイを実行できるようにするコマンドファイルを作成する方法について説明します。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: c61560e9-9f6c-4985-834a-08a3eabf9c3c
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/creating-and-running-a-deployment-command-file
msc.type: authoredcontent
ms.openlocfilehash: f1477ff423e4898385066a35b42503f3c70dcc68
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78514978"
---
# <a name="creating-and-running-a-deployment-command-file"></a>配置コマンド ファイルを作成し、実行する

[Jason Lee](https://github.com/jrjlee)

[[Download PDF]\(PDF をダウンロード\)](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> このトピックでは、Microsoft Build Engine (MSBuild) プロジェクトファイルを使用して、単一ステップの反復可能なプロセスとして配置を実行できるようにするコマンドファイルを作成する方法について説明します。

このトピックでは、Fabrikam, Inc. という架空の企業のエンタープライズ展開要件に基づいて、一連のチュートリアルの一部を説明します。このチュートリアルシリーズでは、&#x2014; [Contact Manager](the-contact-manager-solution.md)ソリューション&#x2014;のサンプルソリューションを使用して、ASP.NET MVC 3 アプリケーション、Windows Communication Foundation (WCF) サービス、データベースプロジェクトなど、現実的なレベルの複雑さを持つ web アプリケーションを表します。

これらのチュートリアルの中核となる配置方法は、「ビルド[プロセスについ](understanding-the-build-process.md)て」で説明されている「プロジェクトファイルの分割」の方法に基づいて&#x2014;います。この方法では、ビルドプロセスは、各配置先環境に適用されるビルド命令を含む2つのプロジェクトファイルと、環境固有のビルドおよび配置設定を含んでいます。 ビルド時に、環境固有のプロジェクトファイルが環境に依存しないプロジェクトファイルにマージされ、ビルド命令の完全なセットが形成されます。

## <a name="process-overview"></a>プロセスの概要

このトピックでは、これらのプロジェクトファイルを使用するコマンドファイルを作成して実行し、ターゲット環境への反復可能なデプロイを実行する方法について説明します。 基本的に、コマンドファイルには、次のような MSBuild コマンドが含まれている必要があります。

- 環境に依存しない*パブリッシュの proj*ファイルを実行するよう MSBuild に指示します。
- 環境固有のプロジェクト設定を含むファイルと、それを検索する場所を指定します *。*

## <a name="create-an-msbuild-command"></a>MSBuild コマンドを作成する

「[ビルドプロセスについ](understanding-the-build-process.md)て」で説明されているよう&#x2014;に、環境固有のプロジェクトファイル (例: *Env-Dev. proj*&#x2014;) は、ビルド時に環境に依存しない*発行 proj*ファイルにインポートするように設計されています。 これらの2つのファイルは、MSBuild にソリューションのビルド方法と配置方法を指示する完全な命令セットを提供します。

*Publish*ファイルは、 **import**要素を使用して、環境固有のプロジェクトファイルをインポートします。

[!code-xml[Main](creating-and-running-a-deployment-command-file/samples/sample1.xml)]

そのため、Msbuild.exe を使用して Contact Manager ソリューションをビルドおよび配置する場合は、次のことを行う必要があります。

- Mstest.exe ファイルで Msbuild.exe を実行し*ます。*
- **TargetEnvPropsFile**という名前のコマンドラインパラメーターを指定して、環境固有のプロジェクトファイルの場所を指定します。

これを行うには、MSBuild コマンドは次のようになります。

[!code-console[Main](creating-and-running-a-deployment-command-file/samples/sample2.cmd)]

ここからは、反復可能な単一ステップのデプロイに移行するための簡単な手順です。 必要な作業は、MSBuild コマンドを .cmd ファイルに追加することだけです。 Contact Manager ソリューションで、Publish フォルダーには、 *Publish-Dev*という名前のファイルが含まれています。

[!code-console[Main](creating-and-running-a-deployment-command-file/samples/sample3.cmd)]

> [!NOTE]
> **/Fl**スイッチは、msbuild.exe が呼び出された作業ディレクトリ*に msbuild.exe という名前*のログファイルを作成するよう msbuild に指示します。

Contact Manager ソリューションを配置または再配置するには、 *Publish-Dev*ファイルを実行するだけです。 ファイルを実行すると、MSBuild は次のことを行います。

- ソリューション内のすべてのプロジェクトをビルドします。
- Web アプリケーションプロジェクトの配置可能な web パッケージを生成します。
- データベースプロジェクトの .dbschema ファイルと deploymanifest ファイルを生成します。
- Web パッケージを web サーバーに配置します。
- データベースをデータベースサーバーに配置します。

## <a name="run-the-deployment"></a>デプロイを実行する

ターゲット環境のコマンドファイルを作成したら、ファイルを実行するだけで配置全体を完了できるようになります。

**連絡先マネージャーソリューションをテスト環境に配置するには**

1. 開発者ワークステーションでエクスプローラーを開き、 *Publish-Dev*ファイルの場所を参照します。
2. ファイルをダブルクリックして実行します。
3. **[ファイルを開く-セキュリティの警告]** ダイアログボックスが表示されたら、 **[実行]** をクリックします。
4. 構成設定とテストサーバーが正しく設定されている場合、MSBuild がプロジェクトファイルの処理を完了すると、コマンドプロンプトウィンドウに "**ビルドが成功しまし**た" というメッセージが表示されます。

    ![](creating-and-running-a-deployment-command-file/_static/image1.png)
5. この環境にソリューションを初めてデプロイした場合は、テスト用の web サーバーマシンアカウントをデータベース **\_datawriter**と**Db\_datareader** **マネージャー**データベースに追加する必要があります。 この手順につい[ては、「Configure a Database Server for Web 配置 Publishing](../configuring-server-environments-for-web-deployment/configuring-a-database-server-for-web-deploy-publishing.md)」を参照してください。

    > [!NOTE]
    > これらのアクセス許可は、データベースの作成時にのみ割り当てる必要があります。 既定では、ビルドプロセスは、すべての配置&#x2014;でデータベースを再作成するのではなく、既存のデータベースを最新のスキーマと比較し、必要な変更のみを行います。 そのため、初めてソリューションを配置するときは、これらのデータベースロールをマップする必要があります。
6. Internet Explorer を開き、Contact Manager アプリケーションの URL (`http://testweb1:85/ContactManager/`など) を参照します。
7. アプリケーションが想定どおりに動作し、連絡先を追加できることを確認します。

    ![](creating-and-running-a-deployment-command-file/_static/image2.png)

## <a name="conclusion"></a>まとめ

MSBuild の手順を含むコマンドファイルを作成すると、複数のプロジェクトから成るソリューションを特定の配置先の環境に簡単かつ簡単に構築してデプロイすることができます。 複数の移行先環境にソリューションを繰り返しデプロイする必要がある場合は、複数のコマンドファイルを作成できます。 各コマンドファイルでは、MSBuild コマンドによって同じユニバーサルプロジェクトファイルがビルドされますが、環境固有の別のプロジェクトファイルが指定されます。 たとえば、開発者またはテスト環境に発行するコマンドファイルには、次の MSBuild コマンドを含めることができます。

[!code-console[Main](creating-and-running-a-deployment-command-file/samples/sample4.cmd)]

ステージング環境に発行するためのコマンドファイルには、次の MSBuild コマンドが含まれる場合があります。

[!code-console[Main](creating-and-running-a-deployment-command-file/samples/sample5.cmd)]

> [!NOTE]
> 独自のサーバー環境用に環境固有のプロジェクトファイルをカスタマイズする方法については、「[ターゲット環境の配置プロパティを構成](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md)する」を参照してください。

また、プロパティをオーバーライドしたり、MSBuild コマンドで他のさまざまなスイッチを設定したりして、各環境のビルドプロセスをカスタマイズすることもできます。 詳細については、「 [MSBuild コマンドラインリファレンス](https://msdn.microsoft.com/library/ms164311.aspx)」を参照してください。

> [!div class="step-by-step"]
> [前へ](deploying-database-projects.md)
> [次へ](manually-installing-web-packages.md)
