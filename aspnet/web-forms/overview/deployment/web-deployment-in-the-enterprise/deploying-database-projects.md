---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/deploying-database-projects
title: データベースプロジェクトの配置 |Microsoft Docs
author: jrjlee
description: '注: 多くのエンタープライズ展開シナリオでは、配置されたデータベースに増分更新を発行する機能が必要です。 もう1つの方法は、再作成することです。'
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 832f226a-1aa3-4093-8c29-ce4196793259
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/deploying-database-projects
msc.type: authoredcontent
ms.openlocfilehash: 221808758492aedb8e8329364e511df28fd11105
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78514942"
---
# <a name="deploying-database-projects"></a>データベース プロジェクトを配置する

[Jason Lee](https://github.com/jrjlee)

[[Download PDF]\(PDF をダウンロード\)](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> [!NOTE]
> 多くのエンタープライズ展開シナリオでは、配置されたデータベースに増分更新を発行する機能が必要です。 別の方法として、すべての配置でデータベースを再作成する方法があります。これは、既存のデータベース内のデータが失われることを意味します。 Visual Studio 2010 を使用する場合、データベースの増分公開には VSDBCMD を使用することをお勧めします。 ただし、次のバージョンの Visual Studio と Web 発行パイプライン (WPP) には、増分発行を直接サポートするツールが含まれています。

Visual Studio 2010 で Contact Manager サンプルソリューションを開くと、4つのファイルを含む Properties フォルダーがデータベースプロジェクトに含まれていることがわかります。

![](deploying-database-projects/_static/image1.png)

プロジェクトファイル (この場合は*Contactmanager. Database. .dbproj* ) と共に、これらのファイルはビルドと配置のプロセスのさまざまな側面を制御します。

- プロジェクトを配置するときに使用する SQLCMD 変数の値は、*データベースの sqlcmdvars*ファイルによって提供されます。 各ソリューション構成 (デバッグやリリースなど) では、別の sqlcmdvars ファイルを指定できます。
- *データベースの sqldeployment*ファイルは、プロジェクトで定義されている照合順序を使用するか、移行先サーバーの照合順序を使用するか、移行先データベースを毎回再作成するか、既存のデータベースを修正して最新の状態にするかなど、配置固有の設定を提供します。 各ソリューション構成では、別の sqldeployment ファイルを指定できます。
- *データベースの sqlpermissions*ファイルは、ターゲットデータベースに追加する権限を定義するために使用できる XML ドキュメントです。 すべてのソリューション構成は、同じ sqlpermissions ファイルを共有します。
- データベースの*sqlsettings*ファイルでは、使用する照合順序、比較演算子の動作など、データベースの作成時に使用するデータベースレベルのプロパティを指定します。 すべてのソリューション構成は、同じ sqlsettings ファイルを共有します。

これらのファイルを Visual Studio で開いて、内容を理解しておくことができます。

データベースプロジェクトをビルドすると、ビルドプロセスによって次の2つのファイルが作成されます。

- *データベーススキーマ*(.dbschema ファイル)。 ここでは、XML 形式で作成するデータベースのスキーマについて説明します。
- *配置マニフェスト*(deploymanifest ファイル)。 これには、データベースを作成および配置するために必要なすべての情報が含まれます。 これは、配置手順 (sqldeployment ファイル) や配置前または配置後の SQL スクリプトなど、その他のリソースと共に、.dbschema ファイルを参照します。

これは、次のリソース間の関係を示しています。

![](deploying-database-projects/_static/image2.png)

ご覧のように、sqlsettings ファイルと、sqlsettings ファイルはビルドプロセスへの入力です。 データベースプロジェクトファイルと共に、これらのファイルを使用してデータベーススキーマファイルが作成されます。 Sqldeployment ファイルと、sqlcmdvar ファイルは、ビルドプロセスを変更せずに渡します。 配置マニフェストは、データベーススキーマの場所、sqldeployment ファイル、sqlcmdvar ファイル、および配置前または配置後 SQL スクリプトの場所を示します。

## <a name="why-use-vsdbcmd-to-deploy-a-database-project"></a>VSDBCMD を使用してデータベースプロジェクトを配置する理由

データベースプロジェクトを配置するには、さまざまな方法があります。 ただし、エンタープライズ環境でリモートサーバーにデータベースプロジェクトを配置する場合は、これらのすべてが適しているわけではありません。 データベースプロジェクトの配置から必要なものを検討してください。 エンタープライズ展開シナリオでは、次のことが必要になる可能性があります。

- リモートの場所からデータベースプロジェクトを配置する権限。
- 既存のデータベースに対して増分更新を行う機能。
- 配置前スクリプトまたは配置後スクリプトを含める機能。
- 配置を複数の配置先環境に合わせて調整する機能。
- 大規模でスクリプト化された、単一ステップのソリューション配置の一部としてデータベースプロジェクトを配置する機能。

データベースプロジェクトを配置するには、主に次の3つの方法を使用します。

- Visual Studio 2010 では、データベースプロジェクトの種類と共に配置機能を使用できます。 Visual Studio 2010 でデータベースプロジェクトをビルドして配置すると、配置プロセスでは、配置マニフェストを使用して、ビルド構成に固有の SQL ベースの配置ファイルが生成されます。 データベースがまだ存在しない場合は作成され、既に存在する場合はデータベースに必要な変更を加えます。 このファイルは、SQLCMD を使用して移行先サーバーで実行できます。また、ファイルを作成して実行するように Visual Studio を設定することもできます。 この方法の欠点は、展開設定の制御が制限されていることです。 また、場合によっては、環境固有の変数値を提供するために、SQL 配置ファイルを変更する必要があります。 このアプローチは、Visual Studio 2010 がインストールされているコンピューターからのみ使用できます。開発者は、すべての接続先環境の接続文字列と資格情報を把握し、提供する必要があります。
- インターネットインフォメーションサービス (IIS) Web 配置ツール (Web 配置) を使用して、 [web アプリケーションプロジェクトの一部としてデータベースを配置](https://msdn.microsoft.com/library/dd465343.aspx)できます。 ただし、この方法は、移行先サーバーに既存のローカルデータベースをレプリケートするだけではなく、データベースプロジェクトを配置する場合に、はるかに複雑になります。 データベースプロジェクトによって生成される SQL 配置スクリプトを実行するように Web 配置を構成できますが、そのためには、Web アプリケーションプロジェクト用のカスタムの WPP ターゲットファイルを作成する必要があります。 これにより、展開プロセスの複雑さが大幅に増加します。 また、Web 配置は、既存のデータベースの増分更新を直接サポートしません。 この方法の詳細については、「 [Web 発行パイプラインのパッケージデータベースプロジェクトの配置 SQL ファイルへの拡張](https://go.microsoft.com/?linkid=9805121)」を参照してください。
- データベーススキーマまたは配置マニフェストのいずれかを使用して、VSDBCMD ユーティリティを使用してデータベースを配置できます。 MSBuild ターゲットから VSDBCMD を呼び出すことができます。これにより、スクリプト化された大規模な配置プロセスの一部としてデータベースをパブリッシュできます。 VSDBCMD コマンドでは、sqlcmdvars ファイル内の変数とその他の多くのデータベースプロパティをオーバーライドできます。これにより、複数のビルド構成を作成することなく、さまざまな環境の配置をカスタマイズできます。 VSDBCMD は、区別機能を提供します。これは、対象データベースをデータベーススキーマに合わせるために必要な変更のみを行うことを意味します。 また、VSDBCMD にはさまざまなコマンドラインオプションが用意されており、展開プロセスをきめ細かく制御することができます。

この概要から、MSBuild で VSDBCMD を使用することは、一般的なエンタープライズ展開シナリオに最適なアプローチであることがわかります。

|  | Visual Studio 2010 | Web Deploy 2.0 | VSDBCMD.exe |
| --- | --- | --- | --- |
| リモート展開をサポートしますか? | はい | はい | はい |
| 増分更新をサポートしていますか? | はい | いいえ | はい |
| 配置前または配置後のスクリプトをサポートしていますか? | はい | はい | はい |
| 複数環境のデプロイはサポートされていますか? | 制限あり | 制限あり | はい |
| スクリプト化された展開をサポートしますか。 | 制限あり | はい | はい |

このトピックの残りの部分では、VSDBCMD と MSBuild を使用してデータベースプロジェクトを配置する方法について説明します。

## <a name="understanding-the-deployment-process"></a>デプロイプロセスについて

VSDBCMD ユーティリティを使用すると、データベーススキーマ (.dbschema ファイル) または配置マニフェスト (deploymanifest ファイル) のいずれかを使用してデータベースを配置できます。 実際には、配置マニフェストを使用して、さまざまな配置プロパティの既定値を指定し、実行する配置前または配置後の SQL スクリプトを特定できるため、ほとんどの場合、配置マニフェストを使用します。 たとえば、次の VSDBCMD コマンドは、テスト環境で**Contactmanager**データベースをデータベースサーバーに配置するために使用されます。

[!code-console[Main](deploying-database-projects/samples/sample1.cmd)]

この場合、次のようになります。

- **/A** (または **/Action**) スイッチは、VSDBCMD を実行する対象を指定します。 これを**インポート**または**配置**するように設定できます。 **インポート**オプションは、既存のデータベースから .dbschema ファイルを生成するために使用されます。また、**配置**オプションを使用して、.dbschema ファイルを対象のデータベースに配置します。
- **/マニフェスト**(または **/manifestfile**) スイッチは、配置する deploymanifest ファイルを識別します。 代わりに、そのような .dbschema ファイルを使用する場合は、 **/モデル**(または **/modelfile**) スイッチを使用します。
- **/Cs** (または **/ConnectionString**) スイッチは、ターゲットデータベースサーバーの接続文字列を提供します。 これには、データベースを作成するために&#x2014;サーバーに接続する必要がある VSDBCMD データベースの名前は含まれないことに注意してください。個々のデータベースに接続する必要はありません。 Deploymanifest ファイルに接続文字列が含まれている場合は、このスイッチを省略できます。 スイッチを使用すると、スイッチの値によって、deploymanifest 値がオーバーライドされます。
- <strong>/P: targetdatabase</strong>プロパティは、作成時にターゲットデータベースに割り当てる名前を指定します。 これにより、deploymanifest ファイルの<strong>Targetdatabase</strong>プロパティの値がオーバーライドされます。 <strong>/P:</strong> <em>[property name]</em>構文を使用すると、さまざまな配置プロパティを設定し、sqlcmdvars ファイルで宣言されているすべての SQLCMD 変数をオーバーライドできます。
- **/Dd +** (または **/deploytodatabase +** ) スイッチは、デプロイを作成し、ターゲット環境に配置することを示します。 **/Dd-** を指定した場合、またはスイッチを省略した場合は、VSDBCMD によって配置スクリプトが生成されますが、ターゲット環境には配置されません。 多くの場合、このスイッチは混乱の原因となります。詳細については、次のセクションで説明します。
- **/Script** (または **/DeploymentScriptFile**) スイッチは、配置スクリプトを生成する場所を指定します。 この値は、デプロイプロセスには影響しません。

VSDBCMD の詳細については、「 [VSDBCMD のコマンドラインリファレンス」を参照してください。EXE (配置とスキーマのインポート)](https://msdn.microsoft.com/library/dd193283.aspx)および[方法: VSDBCMD を使用して、コマンドプロンプトから配置するデータベースを準備します。EXE](https://msdn.microsoft.com/library/dd193258.aspx)。

MSBuild プロジェクトファイルから VSDBCMD を使用する方法の例については、「[ビルドプロセスについ](understanding-the-build-process.md)て」を参照してください。 複数の環境のデータベース配置設定を構成する方法の例については、「[複数の環境でのデータベース配置のカスタマイズ](../advanced-enterprise-web-deployment/customizing-database-deployments-for-multiple-environments.md)」を参照してください。

## <a name="understanding-the-deploytodatabase-switch"></a>DeployToDatabase スイッチについて

**/Dd**または **/deploytodatabase**スイッチの動作は、VSDBCMD を .dbschema ファイルと共に使用するか、または deploymanifest ファイルと共に使用するかによって異なります。 .Dbschema ファイルを使用している場合、動作は非常に簡単です。

- **/Dd +** または **/dd**を指定すると、VSDBCMD によって配置スクリプトが生成され、データベースが配置されます。
- **/Ddを**指定した場合、またはスイッチを省略した場合、VSDBCMD では配置スクリプトのみが生成されます。

Deploymanifest ファイルを使用している場合、動作ははるかに複雑になります。 これは、deploymanifest ファイルに、データベースが配置されているかどうかも確認するプロパティ名**Deploytodatabase**が含まれているためです。

[!code-xml[Main](deploying-database-projects/samples/sample2.xml)]

このプロパティの値は、データベースプロジェクトのプロパティに従って設定されます。 配置**スクリプト (.sql) を作成**するように**配置アクション**を設定した場合、値は**False**になります。 配置**スクリプト (.sql) を作成してデータベースに配置**するように**配置アクション**を設定した場合、値は**True**になります。

> [!NOTE]
> これらの設定は、特定のビルド構成およびプラットフォームに関連付けられています。 たとえば、**デバッグ**構成の設定を構成してから、**リリース**構成を使用して発行すると、設定は使用されません。

![](deploying-database-projects/_static/image3.png)

> [!NOTE]
> このシナリオでは、Visual Studio 2010 でデータベースを配置しないようにするため、配置**アクション** **(.Sql) を作成**するように常に設定する必要があります。 つまり、 **Deploytodatabase**プロパティは常に**False**である必要があります。

**Deploytodatabase**プロパティを指定すると、プロパティ値が**false**の場合にのみ、 **/dd**スイッチでプロパティがオーバーライドされます。

- **Deploytodatabase**プロパティが**False**の場合に、 **/dd +** または **/dd**を指定すると、VSDBCMD は**deploytodatabase**プロパティをオーバーライドし、データベースを配置します。
- **Deploytodatabase**プロパティが**False**で、 **/ddを**指定した場合、またはスイッチを省略した場合、VSDBCMD ではデータベースが配置されません。
- **Deploytodatabase**プロパティが**True**の場合、VSDBCMD はスイッチを無視し、データベースを配置します。
- 配置スクリプトは、データベースを配置するかどうかに関係なく、それぞれのケースで生成されます。

## <a name="conclusion"></a>まとめ

このトピックでは、Visual Studio 2010 のデータベースプロジェクトのビルドおよび配置プロセスの概要について説明しました。 また、MSBuild で VSDBCMD を使用して、エンタープライズ規模のデータベース配置をサポートする方法についても説明します。

実際の動作方法の詳細については、「[複数の環境でのデータベース配置のカスタマイズ](../advanced-enterprise-web-deployment/customizing-database-deployments-for-multiple-environments.md)」を参照してください。

## <a name="further-reading"></a>参考資料

各環境用に個別の配置構成ファイルを作成してデータベース配置をカスタマイズする方法については、「[複数の環境でのデータベース配置のカスタマイズ](../advanced-enterprise-web-deployment/customizing-database-deployments-for-multiple-environments.md)」を参照してください。 配置後スクリプトを実行してデータベースロールのメンバーシップを構成する方法については、「[テスト環境にデータベースロールメンバーシップを配置する](../advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments.md)」を参照してください。 メンバーシップデータベースによって課せられるいくつかの固有の課題を管理するためのガイダンスについては、「[エンタープライズ環境へのメンバーシップデータベースの配置](../advanced-enterprise-web-deployment/deploying-membership-databases-to-enterprise-environments.md)」を参照してください。

MSDN の次のトピックでは、Visual Studio データベースプロジェクトとデータベース配置プロセスに関する広範なガイダンスと背景情報を提供しています。

- [Visual Studio 2010 SQL Server データベースプロジェクト](https://msdn.microsoft.com/library/ff678491.aspx)
- [データベースの変更の管理](https://msdn.microsoft.com/library/aa833404.aspx)
- [方法: VSDBCMD を使用して、コマンドプロンプトからデータベースを配置するための準備を行います。EXCEL.EXE](https://msdn.microsoft.com/library/dd193258.aspx)
- [データベースビルド & デプロイの概要](https://msdn.microsoft.com/library/aa833165.aspx)

> [!div class="step-by-step"]
> [前へ](deploying-web-packages.md)
> [次へ](creating-and-running-a-deployment-command-file.md)
