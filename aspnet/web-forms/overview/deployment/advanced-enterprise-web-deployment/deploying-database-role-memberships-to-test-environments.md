---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments
title: テスト環境へのデータベースロールメンバーシップの配置 |Microsoft Docs
author: jrjlee
description: このトピックでは、テスト環境へのソリューションの配置の一部として、ユーザーアカウントをデータベースロールに追加する方法について説明します。 ... を含むソリューションを配置する場合
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 9b2af539-7ad9-47aa-b66e-873bd9906e79
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments
msc.type: authoredcontent
ms.openlocfilehash: a15f5bf5f659d151e91ef9e53c5ad55bcd8e2b01
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78474946"
---
# <a name="deploying-database-role-memberships-to-test-environments"></a>テスト環境にデータベース ロール メンバーシップを配置する

[Jason Lee](https://github.com/jrjlee)

[[Download PDF]\(PDF をダウンロード\)](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> このトピックでは、テスト環境へのソリューションの配置の一部として、ユーザーアカウントをデータベースロールに追加する方法について説明します。
> 
> データベースプロジェクトを含むソリューションをステージング環境または運用環境に配置する場合は、通常、開発者がデータベースロールへのユーザーアカウントの追加を自動化する必要がありません。 ほとんどの場合、開発者はどのユーザーアカウントをどのデータベースロールに追加する必要があるかを把握しておらず、これらの要件はいつでも変更される可能性があります。 ただし、データベースプロジェクトを含むソリューションを開発環境またはテスト環境に配置する場合は、通常、状況は異なります。
> 
> - 通常、開発者は定期的にソリューションを再デプロイします (多くの場合、1日に数回)。
> - 通常、データベースは、すべての配置で再作成されます。つまり、データベースユーザーを作成し、すべての配置後にロールに追加する必要があります。
> - 開発者は、通常、対象となる開発環境またはテスト環境を完全に制御できます。
> 
> このシナリオでは、データベースユーザーを自動的に作成し、データベースロールのメンバーシップをデプロイプロセスの一部として割り当てる方が便利です。
> 
> 重要なのは、この操作はターゲット環境に基づいて条件を設定する必要があることです。 ステージング環境または運用環境にデプロイしている場合は、操作をスキップします。 開発者またはテスト環境に配置する場合は、追加の操作を行わずにロールメンバーシップを配置する必要があります。 このトピックでは、この課題に対処するために使用できる1つの方法について説明します。

このトピックでは、Fabrikam, Inc. という架空の企業のエンタープライズ展開要件に基づいて、一連のチュートリアルの一部を説明します。このチュートリアルシリーズでは、&#x2014; [Contact Manager ソリューション](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;のサンプルソリューションを使用して、ASP.NET MVC 3 アプリケーション、Windows Communication Foundation (WCF) サービス、データベースプロジェクトなど、現実的なレベルの複雑さを持つ web アプリケーションを表します。

これらのチュートリアルの中核となる配置方法は、「[プロジェクトファイルについ](../web-deployment-in-the-enterprise/understanding-the-project-file.md)て」で説明されている分割プロジェクトファイルアプローチに基づいています。この&#x2014;プロジェクトファイルには、ビルドプロセスは、すべての変換先環境に適用されるビルド命令を含む2つのプロジェクトファイルと、環境固有のビルドおよび配置設定を含んでいます。 ビルド時に、環境固有のプロジェクトファイルが環境に依存しないプロジェクトファイルにマージされ、ビルド命令の完全なセットが形成されます。

## <a name="task-overview"></a>タスクの概要

このトピックは次のことを前提としています。

- 「プロジェクト[ファイルについ](../web-deployment-in-the-enterprise/understanding-the-project-file.md)て」で説明されているように、ソリューションの配置には、プロジェクトファイルの分割アプローチを使用します。
- 「[ビルドプロセスについ](../web-deployment-in-the-enterprise/understanding-the-build-process.md)て」で説明されているように、プロジェクトファイルから VSDBCMD を呼び出して、データベースプロジェクトを配置します。

データベースプロジェクトをテスト環境に配置するときにデータベースユーザーを作成し、ロールメンバーシップを割り当てるには、次のことを行う必要があります。

- 必要なデータベースの変更を行う Transact 構造化照会言語 (Transact-sql) スクリプトを作成します。
- Sqlcmd ユーティリティを使用して SQL スクリプトを実行する Microsoft Build Engine (MSBuild) ターゲットを作成します。
- ソリューションをテスト環境に配置するときに、ターゲットを呼び出すようにプロジェクトファイルを構成します。

このトピックでは、これらの各手順を実行する方法について説明します。

## <a name="scripting-the-database-role-memberships"></a>データベースロールのメンバーシップのスクリプトを作成する

Transact-sql スクリプトは、さまざまな方法で、または任意の場所で作成できます。 最も簡単な方法は、Visual Studio 2010 でソリューション内にスクリプトを作成することです。

**SQL スクリプトを作成するには**

1. **[ソリューションエクスプローラー]** ウィンドウで、データベースプロジェクトノードを展開します。
2. **Scripts**フォルダーを右クリックして **[追加]** をポイントし、 **[新しいフォルダー]** をクリックします。
3. フォルダー名として「 **Test** 」と入力し、enter キーを押します。
4. **テスト**フォルダーを右クリックし、 **[追加]** をポイントして、 **[スクリプト]** をクリックします。
5. **[新しい項目の追加]** ダイアログボックスで、スクリプトにわかりやすい名前 (たとえば、 **AddRoleMemberships**) を付け、 **[追加]** をクリックします。

    ![](deploying-database-role-memberships-to-test-environments/_static/image1.png)
6. *AddRoleMemberships*ファイルで、次のような transact-sql ステートメントを追加します。

    1. データベースにアクセスする SQL Server ログインのデータベースユーザーを作成します。
    2. 必要なデータベースロールにデータベースユーザーを追加します。
7. ファイルは次のようになります。

    [!code-sql[Main](deploying-database-role-memberships-to-test-environments/samples/sample1.sql)]
8. ファイルを保存します。

## <a name="executing-the-script-on-the-target-database"></a>ターゲットデータベースでのスクリプトの実行

データベースプロジェクトを配置するときに、配置後スクリプトの一部として必要な Transact-sql スクリプトを実行するのが理想的です。 ただし、配置後スクリプトでは、ソリューション構成またはビルドプロパティに基づいて条件付きでロジックを実行することはできません。 別の方法として、sqlcmd コマンドを実行する**Target**要素を作成することによって、MSBuild プロジェクトファイルから直接 SQL スクリプトを実行します。 このコマンドを使用して、ターゲットデータベースでスクリプトを実行できます。

[!code-console[Main](deploying-database-role-memberships-to-test-environments/samples/sample2.cmd)]

> [!NOTE]
> Sqlcmd のコマンドラインオプションの詳細については、「 [Sqlcmd ユーティリティ](https://msdn.microsoft.com/library/ms162773.aspx)」を参照してください。

MSBuild ターゲットにこのコマンドを埋め込む前に、スクリプトを実行する条件を考慮する必要があります。

- ターゲットデータベースは、ロールメンバーシップを変更する前に存在している必要があります。 そのため、このスクリプトは、データベースの配置*後*に実行する必要があります。
- テスト環境に対してのみスクリプトが実行されるように、条件を含める必要があります。
- "What-if" 配置&#x2014;を実行している場合、配置スクリプトを生成しているものの、実際に&#x2014;は実行していない場合は、SQL スクリプトを実行しないでください。

Contact Manager サンプルソリューションに示されているように、「[プロジェクトファイルについ](../web-deployment-in-the-enterprise/understanding-the-project-file.md)て」で説明されているプロジェクトファイルの分割方法を使用している場合は、次のように SQL スクリプトのビルド命令を分割できます。

- 必要な環境固有のプロパティは、アクセス許可を配置するかどうかを決定するプロパティと共に、環境固有のプロジェクトファイル (たとえば、 *Env Dev. proj*) に配置する必要があります。
- MSBuild ターゲット自体は、変換先の環境間で変更されないプロパティと共に、ユニバーサルプロジェクトファイル (たとえば、 *Publish*) に配置する必要があります。

環境固有のプロジェクトファイルでは、データベースサーバー名、ターゲットデータベース名、およびロールメンバーシップを配置するかどうかをユーザーが指定できるようにするブール型プロパティを定義する必要があります。

[!code-xml[Main](deploying-database-role-memberships-to-test-environments/samples/sample3.xml)]

ユニバーサルプロジェクトファイルで、sqlcmd 実行可能ファイルの場所と実行する SQL スクリプトの場所を指定する必要があります。 これらのプロパティは、移行先の環境に関係なく同じままです。 また、sqlcmd コマンドを実行するために MSBuild ターゲットを作成する必要があります。

[!code-xml[Main](deploying-database-role-memberships-to-test-environments/samples/sample4.xml)]

Sqlcmd 実行可能ファイルの場所を静的プロパティとして追加することに注意してください。これは他のターゲットにとって便利な場合があるためです。 これに対して、SQL スクリプトの場所と sqlcmd コマンドの構文は、ターゲット内の動的プロパティとして定義します。これは、ターゲットを実行する前に必要ではないためです。 この場合、 **Deploytestdbpermissions**ターゲットは、これらの条件が満たされた場合にのみ実行されます。

- **DeployTestDBRoleMemberships**プロパティは**true**に設定されています。
- ユーザーに**WhatIf = true**フラグが指定されていません。

最後に、必ずターゲットを呼び出してください。 既定の**Fullpublish**ターゲットの依存関係の一覧にターゲットを追加することで、このファイルを*パブリッシュします*。 **Publishdbpackages**ターゲットが実行されるまでは、 **Deploytestdbpermissions**ターゲットが実行されないようにする必要があります。

[!code-xml[Main](deploying-database-role-memberships-to-test-environments/samples/sample5.xml)]

## <a name="conclusion"></a>まとめ

このトピックでは、データベースプロジェクトを配置するときに、データベースユーザーとロールメンバーシップを配置後アクションとして追加できる方法の1つについて説明します。 通常、この方法は、テスト環境でデータベースを定期的に再作成する場合に便利ですが、データベースをステージング環境または運用環境に配置するときは通常は避ける必要があります。 そのため、データベースユーザーとロールメンバーシップが適切な場合にのみ作成されるように、必要な条件ロジックを必ず使用してください。

## <a name="further-reading"></a>参考資料

VSDBCMD を使用してデータベースプロジェクトを配置する方法の詳細については、「[データベースプロジェクトの配置](../web-deployment-in-the-enterprise/deploying-database-projects.md)」を参照してください。 さまざまなターゲット環境のデータベース配置をカスタマイズする方法については、「[複数の環境でのデータベース配置のカスタマイズ](customizing-database-deployments-for-multiple-environments.md)」を参照してください。 カスタム MSBuild プロジェクトファイルを使用した配置プロセスの制御の詳細については、「[プロジェクトファイルについ](../web-deployment-in-the-enterprise/understanding-the-project-file.md)て」および「[ビルドプロセスについ](../web-deployment-in-the-enterprise/understanding-the-build-process.md)て」を参照してください。 Sqlcmd のコマンドラインオプションの詳細については、「 [Sqlcmd ユーティリティ](https://msdn.microsoft.com/library/ms162773.aspx)」を参照してください。

> [!div class="step-by-step"]
> [前へ](customizing-database-deployments-for-multiple-environments.md)
> [次へ](deploying-membership-databases-to-enterprise-environments.md)
