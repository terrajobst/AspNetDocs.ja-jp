---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/customizing-database-deployments-for-multiple-environments
title: 複数の環境のデータベース配置のカスタマイズ |Microsoft Docs
author: jrjlee
description: 'このトピックでは、配置プロセスの一部として、データベースのプロパティを特定のターゲット環境に合わせて調整する方法について説明します。 注: このトピックでは、'
ms.author: riande
ms.date: 05/04/2012
ms.assetid: a172979a-1318-4318-a9c6-4f9560d26267
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/customizing-database-deployments-for-multiple-environments
msc.type: authoredcontent
ms.openlocfilehash: 8ae8cb1a322afb95c5d2e8d5e73c7825c7b2fe5a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78489034"
---
# <a name="customizing-database-deployments-for-multiple-environments"></a>複数の環境のためにデータベース配置をカスタマイズする

[Jason Lee](https://github.com/jrjlee)

[[Download PDF]\(PDF をダウンロード\)](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> このトピックでは、配置プロセスの一部として、データベースのプロパティを特定のターゲット環境に合わせて調整する方法について説明します。
> 
> > [!NOTE]
> > このトピックでは、Msbuild.exe と VSDBCMD を使用して Visual Studio 2010 データベースプロジェクトを配置することを前提としています。 この方法を選択する理由の詳細については、「[エンタープライズ環境での Web 配置](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md)」および「[データベースプロジェクトの配置](../web-deployment-in-the-enterprise/deploying-database-projects.md)」を参照してください。
> 
> 
> 複数の変換先にデータベースプロジェクトを配置する場合は、多くの場合、ターゲット環境ごとにデータベース配置プロパティをカスタマイズすることをお勧めします。 たとえば、テスト環境では、通常、すべての配置でデータベースを再作成します。一方、ステージング環境や運用環境では、データを保持するために増分更新を行う方がはるかに多くなります。
> 
> Visual Studio 2010 データベースプロジェクトでは、配置設定は配置構成 (sqldeployment) ファイル内に含まれます。 このトピックでは、環境固有の配置構成ファイルを作成し、VSDBCMD パラメーターとして使用するものを指定する方法について説明します。

このトピックでは、Fabrikam, Inc. という架空の企業のエンタープライズ展開要件に基づいて、一連のチュートリアルの一部を説明します。このチュートリアルシリーズでは、&#x2014; [Contact Manager ソリューション](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;のサンプルソリューションを使用して、ASP.NET MVC 3 アプリケーション、Windows Communication Foundation (WCF) サービス、データベースプロジェクトなど、現実的なレベルの複雑さを持つ web アプリケーションを表します。

これらのチュートリアルの中核となる配置方法は、「[プロジェクトファイルについ](../web-deployment-in-the-enterprise/understanding-the-project-file.md)て」で説明されている分割プロジェクトファイルアプローチに基づいています。この&#x2014;プロジェクトファイルには、ビルドプロセスは、すべての変換先環境に適用されるビルド命令を含む2つのプロジェクトファイルと、環境固有のビルドおよび配置設定を含んでいます。 ビルド時に、環境固有のプロジェクトファイルが環境に依存しないプロジェクトファイルにマージされ、ビルド命令の完全なセットが形成されます。

## <a name="task-overview"></a>タスクの概要

このトピックは次のことを前提としています。

- 「プロジェクト[ファイルについ](../web-deployment-in-the-enterprise/understanding-the-project-file.md)て」で説明されているように、ソリューションの配置には、プロジェクトファイルの分割アプローチを使用します。
- 「[ビルドプロセスについ](../web-deployment-in-the-enterprise/understanding-the-build-process.md)て」で説明されているように、プロジェクトファイルから VSDBCMD を呼び出して、データベースプロジェクトを配置します。

ターゲット環境間でのデータベース配置プロパティの変化をサポートする展開システムを作成するには、次のことを行う必要があります。

- 各ターゲット環境の配置構成 (sqldeployment) ファイルを作成します。
- 展開構成ファイルをコマンドラインスイッチとして指定する VSDBCMD コマンドを作成します。
- Microsoft Build Engine (MSBuild) プロジェクトファイル内の VSDBCMD コマンドをパラメーター化して、VSDBCMD オプションがターゲット環境に適したものになるようにします。

このトピックでは、これらの各手順を実行する方法について説明します。

## <a name="creating-environment-specific-deployment-configuration-files"></a>環境固有の配置構成ファイルの作成

既定では、データベースプロジェクトには、*データベースの sqldeployment*という名前の単一の配置構成ファイルが含まれています。 このファイルを Visual Studio 2010 で開くと、使用可能なさまざまなデプロイオプションが表示されます。

- **配置比較の照合順序**。 これにより、プロジェクトのデータベースの照合順序 (*変換元*の照合順序) と転送先サーバーのデータベース照合順序 (*ターゲット*照合順序) のどちらを使用するかを選択できます。 ほとんどの場合、開発環境またはテスト環境に配置するときに、ソース照合順序を使用します。 ステージング環境または運用環境に配置する場合は、相互運用性の問題を回避するために、ターゲットの照合順序を変更せずに残しておくことをお勧めします。
- **データベースのプロパティを配置**します。 これにより、データベースの*sqlsettings*ファイルで定義されているように、データベースのプロパティを適用するかどうかを選択できます。 データベースを初めて配置する場合は、データベースのプロパティを配置する必要があります。 既存のデータベースを更新する場合は、プロパティが既に存在している必要があるため、再度配置する必要はありません。
- **常にデータベースを再作成**します。 これにより、配置または増分変更を行うたびに対象データベースを再作成して、スキーマを使用してターゲットデータベースを最新の状態にするかどうかを選択できます。 データベースを再作成すると、既存のデータベース内のデータはすべて失われます。 そのため、ステージング環境または運用環境への配置では、通常、これを**false**に設定する必要があります。
- **データ損失が発生する可能性がある場合は、増分配置をブロック**します。 これにより、データベーススキーマの変更によってデータが失われた場合に配置を停止するかどうかを選択できます。 運用環境へのデプロイの場合は、通常、これを**true**に設定して、重要なデータを介入して保護する機会を与えます。 **[常にデータベースを再作成]** する を **[false]** に設定した場合、この設定は無効になります。
- **デプロイをシングルユーザーモードで実行**します。 これは、通常、開発環境またはテスト環境では問題になりません。 ただし、ステージング環境または運用環境への配置では、通常、これを**true**に設定する必要があります。 これにより、配置の実行中にユーザーがデータベースに変更を加えることを防止できます。
- **配置前にデータベースをバックアップ**します。 通常、運用環境に配置するときは、データ損失に対する予防措置として、これを**true**に設定します。 ステージング環境に配置するときに、ステージングデータベースに大量のデータが含まれている場合は、これを**true**に設定することもできます。
- **ターゲットデータベースに存在するが、データベースプロジェクトに含まれていないオブジェクトに対して DROP ステートメントを生成**します。 ほとんどの場合、これは、データベースに対する増分変更を行うための不可欠で重要な部分です。 **[常にデータベースを再作成]** する を **[false]** に設定した場合、この設定は無効になります。
- **ALTER ASSEMBLY ステートメントを使用して CLR 型を更新しないで**ください。 この設定では、共通言語ランタイム (CLR) 型を新しいアセンブリバージョンに更新 SQL Server 方法を決定します。 ほとんどのシナリオでは、この値を**false**に設定する必要があります。

次の表は、さまざまな変換先環境の一般的な配置設定を示しています。 ただし、実際の要件によっては、設定が異なる場合があります。

|  | 開発者/テスト | ステージング/統合 | Production |
| --- | --- | --- | --- |
| **配置比較の照合順序** | source | 移行先 | 移行先 |
| **データベースプロパティの配置** | True | 初回のみ | 初回のみ |
| **データベースを常に再作成する** | True | False | False |
| **データ損失が発生する可能性がある場合に増分配置をブロックする** | False | 可能性あり | True |
| **シングルユーザーモードで配置スクリプトを実行する** | False | True | True |
| **配置前にデータベースをバックアップする** | False | 可能性あり | True |
| **ターゲットデータベースに存在するが、データベースプロジェクトに含まれていないオブジェクトに対して DROP ステートメントを生成する** | False | True | True |
| **ALTER ASSEMBLY ステートメントを使用して CLR 型を更新しない** | False | False | False |

> [!NOTE]
> データベース配置プロパティと環境に関する考慮事項の詳細については、「[データベースプロジェクト設定の概要](https://msdn.microsoft.com/library/aa833291(v=VS.100).aspx)」、「[方法: 配置の詳細のプロパティを構成する](https://msdn.microsoft.com/library/dd172125.aspx)」、「[分離開発環境にデータベースを構築して配置](https://msdn.microsoft.com/library/dd193409.aspx)する」、および「データベースを[ビルドしてステージング環境または運用環境に配置する](https://msdn.microsoft.com/library/dd193413.aspx)」を参照してください。

複数の変換先へのデータベースプロジェクトの配置をサポートするには、各ターゲット環境の配置構成ファイルを作成する必要があります。

**環境固有の構成ファイルを作成するには**

1. Visual Studio 2010 の **[ソリューションエクスプローラー]** ウィンドウで、データベースプロジェクトを右クリックし、 **[プロパティ]** をクリックします。
2. データベースプロジェクトのプロパティページの **[配置]** タブで、 **[配置構成ファイル]** 行の **[新規作成]** をクリックします。

    ![](customizing-database-deployments-for-multiple-environments/_static/image1.png)
3. **[新しい展開構成ファイル]** ダイアログボックスで、ファイルにわかりやすい名前 (たとえば、「 **testenvironment. sqldeployment**」) を指定し、 **[保存]** をクリックします。
4. *[ファイル名] * * * sqldeployment** ページで、配置のプロパティを設定します。展開先の環境の要件に合わせて、ファイルを保存します。

    ![](customizing-database-deployments-for-multiple-environments/_static/image2.png)
5. データベースプロジェクトの Properties フォルダーに新しいファイルが追加されていることに注意してください。

    ![](customizing-database-deployments-for-multiple-environments/_static/image3.png)

## <a name="specifying-the-deployment-configuration-file-in-vsdbcmd"></a>VSDBCMD での展開構成ファイルの指定

Visual Studio 2010 内でソリューション構成 (デバッグやリリースなど) を使用する場合は、配置構成ファイルを各構成に関連付けることができます。 特定の構成をビルドすると、ビルドプロセスによって、構成固有の配置構成ファイルを指す構成固有の配置マニフェストファイルが生成されます。 ただし、このチュートリアルで説明されているデプロイ方法の主な目的の1つは、Visual Studio 2010 およびソリューション構成を使用せずに、デプロイプロセスを制御できるようにすることです。 この方法では、ターゲットの配置環境に関係なく、ソリューション構成は同じです。 特定の配置先環境へのデータベースの配置を調整するには、VSDBCMD コマンドラインオプションを使用して、配置構成ファイルを指定します。

VSDBCMD で展開構成ファイルを指定するには、 **p:/deploymentconfigurationfile**スイッチを使用して、ファイルへの完全パスを指定します。 これは、配置マニフェストによって識別される配置構成ファイルよりも優先されます。 たとえば、次の VSDBCMD コマンドを使用して、 **Contactmanager**データベースをテスト環境に配置できます。

[!code-console[Main](customizing-database-deployments-for-multiple-environments/samples/sample1.cmd)]

> [!NOTE]
> ビルドプロセスでは、ファイルを出力ディレクトリにコピーするときに、sqldeployment ファイルの名前を変更することができます。

配置前または配置後の SQL スクリプトで SQL コマンド変数を使用する場合は、同様の方法を使用して、環境固有の sqlcmdvars ファイルを配置に関連付けることができます。 この場合は、 **p:/SqlCommandVariablesFile**スイッチを使用して、sqlcmdvars ファイルを識別します。

## <a name="running-the-vsdbcmd-command-from-an-msbuild-project-file"></a>MSBuild プロジェクトファイルからの VSDBCMD コマンドの実行

Msbuild ターゲット内の**Exec**タスクを使用して、msbuild プロジェクトファイルから VSDBCMD コマンドを呼び出すことができます。 最も単純な形式では、次のようになります。

[!code-xml[Main](customizing-database-deployments-for-multiple-environments/samples/sample2.xml)]

- 実際には、プロジェクトファイルを読み取って再利用しやすくするために、さまざまなコマンドラインパラメーターを格納するプロパティを作成します。 これにより、ユーザーは、環境固有のプロジェクトファイルにプロパティ値を提供したり、MSBuild コマンドラインから既定値をオーバーライドしたりすることが容易になります。 「[プロジェクトファイルについて](../web-deployment-in-the-enterprise/understanding-the-project-file.md)」で説明されているプロジェクトファイルの分割方法を使用する場合は、次の2つのファイル間でビルドの命令とプロパティを分割する必要があります。
- 環境固有の設定 (配置構成ファイル名、データベース接続文字列、ターゲットデータベース名など) は、環境固有のプロジェクトファイルで指定する必要があります。
- VSDBCMD コマンドを実行する MSBuild ターゲットは、VSDBCMD 実行可能ファイルの場所などの汎用プロパティと共に、ユニバーサルプロジェクトファイルに含まれている必要があります。

また、VSDBCMD を呼び出す前に、データベースプロジェクトをビルドして、deploymanifest ファイルが作成され、使用できる状態になっていることを確認する必要があります。 このアプローチの完全な例については、トピック「[ビルドプロセスについ](../web-deployment-in-the-enterprise/understanding-the-build-process.md)て」を参照してください。このチュートリアルでは、 [Contact Manager サンプルソリューション](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)のプロジェクトファイルについて説明します。

## <a name="conclusion"></a>まとめ

このトピックでは、MSBuild と VSDBCMD を使用してデータベースプロジェクトを配置するときに、さまざまな変換先環境に対してデータベースプロパティを調整する方法について説明します。 この方法は、大規模なエンタープライズ規模のソリューションの一部としてデータベースプロジェクトを配置する必要がある場合に便利です。 これらのソリューションは、多くの場合、サンドボックス化された開発やテスト環境、ステージングまたは統合プラットフォーム、運用環境またはライブ環境などの複数の宛先にデプロイされます。 これらの各ターゲット環境では、通常、データベース配置プロパティの一意のセットが必要です。

## <a name="further-reading"></a>参考資料

VSDBCMD を使用したデータベースプロジェクトの配置の詳細については、「[データベースプロジェクトの配置](../web-deployment-in-the-enterprise/deploying-database-projects.md)」を参照してください。 カスタム MSBuild プロジェクトファイルを使用した配置プロセスの制御の詳細については、「[プロジェクトファイルについ](../web-deployment-in-the-enterprise/understanding-the-project-file.md)て」および「[ビルドプロセスについ](../web-deployment-in-the-enterprise/understanding-the-build-process.md)て」を参照してください。

次の MSDN の記事では、データベースの配置に関する一般的なガイダンスを提供しています。

- [データベースプロジェクト設定の概要](https://msdn.microsoft.com/library/aa833291(v=VS.100).aspx)
- [方法: 配置の詳細のプロパティを構成する](https://msdn.microsoft.com/library/dd172125.aspx)
- [データベースをビルドし、分離開発環境に配置する](https://msdn.microsoft.com/library/dd193409.aspx)
- [ステージング環境または運用環境へのデータベースの構築と配置](https://msdn.microsoft.com/library/dd193413.aspx)

> [!div class="step-by-step"]
> [前へ](performing-a-what-if-deployment.md)
> [次へ](deploying-database-role-memberships-to-test-environments.md)
