---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/performing-a-what-if-deployment
title: What If デプロイを実行する |Microsoft Docs
author: jrjlee
description: このトピックでは、インターネットインフォメーションサービス (IIS) Web 配置ツール (Web 配置) と v2.0 を使用して、"what-if" (またはシミュレートされた) 展開を実行する方法について説明します。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: c711b453-01ac-4e65-a48c-93d99bf22e58
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/performing-a-what-if-deployment
msc.type: authoredcontent
ms.openlocfilehash: 73a0e038cc0d4ebae0ffc8ed3fd2de4c9dad673c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78510334"
---
# <a name="performing-a-what-if-deployment"></a>"What If" 配置を実行する

[Jason Lee](https://github.com/jrjlee)

[[Download PDF]\(PDF をダウンロード\)](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> このトピックでは、インターネットインフォメーションサービス (IIS) Web 配置ツール (Web 配置) と VSDBCMD を使用して、"what-if" (またはシミュレートされた) 展開を実行する方法について説明します。 これにより、アプリケーションを実際に配置する前に、特定のターゲット環境に対する配置ロジックの効果を判断できます。

このトピックでは、Fabrikam, Inc. という架空の企業のエンタープライズ展開要件に基づいて、一連のチュートリアルの一部を説明します。このチュートリアルシリーズでは、&#x2014; [Contact Manager ソリューション](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;のサンプルソリューションを使用して、ASP.NET MVC 3 アプリケーション、Windows Communication Foundation (WCF) サービス、データベースプロジェクトなど、現実的なレベルの複雑さを持つ web アプリケーションを表します。

これらのチュートリアルの中核となる配置方法は、「プロジェクト[ファイルについ](../web-deployment-in-the-enterprise/understanding-the-project-file.md)て」で説明されている分割プロジェクトファイルアプローチに基づいています。この方法で&#x2014;は、ビルドおよび配置プロセスは、すべての変換先環境に適用されるビルド命令を含む2つのプロジェクトファイルと、環境固有のビルドと配置の設定を含んでいます。 ビルド時に、環境固有のプロジェクトファイルが環境に依存しないプロジェクトファイルにマージされ、ビルド命令の完全なセットが形成されます。

## <a name="performing-a-what-if-deployment-for-web-packages"></a>Web パッケージの "What If" 配置の実行

Web 配置には、"what-if" (または試用版) モードで展開を実行できる機能が含まれています。 アイテムを "what-if" モードで展開すると、Web 配置は、展開を実行した場合と同じようにログファイルを生成しますが、実際には移行先サーバーで何も変更しません。 ログファイルを確認すると、配置が移行先サーバーに与える影響を理解するのに役立ちます。具体的には次のとおりです。

- 追加される内容。
- 更新される内容。
- 削除される内容。

"What-if" の展開では、移行先サーバーで実際には何も変更されないため、展開が成功するかどうかを予測することはできません。

「 [Web パッケージの配置](../web-deployment-in-the-enterprise/deploying-web-packages.md)」で説明したように、msdeploy.exe コマンドラインユーティリティ&#x2014;を直接使用するか、ビルドプロセスによって生成される *.deploy*ファイルを実行することで、Web 配置を使用して web パッケージを配置できます。

Msdeploy.exe を直接使用している場合は、コマンドに **– whatif**フラグを追加することで、"what-if" 配置を実行できます。 たとえば、ContactManager. Mvc パッケージをステージング環境に配置した場合に何が起こるかを評価するために、Msdeploy.exe コマンドは次のようになります。

[!code-console[Main](performing-a-what-if-deployment/samples/sample1.cmd)]

"What-if" デプロイの結果に問題がなければ、 **– whatif**フラグを削除してライブデプロイを実行できます。

> [!NOTE]
> Msdeploy.exe のコマンドラインオプションの詳細については、「 [Web 配置操作の設定](https://technet.microsoft.com/library/dd569089(WS.10).aspx)」を参照してください。

*.Deploy*ファイルを使用している場合は、コマンドに **/y**フラグ ("yes" または update mode) ではなく **/t**フラグ (試用モード) フラグを含めることで、"what-if" 展開を実行できます。 たとえば、 *.deploy*ファイルを実行して Contactmanager の Mvc パッケージを配置した場合の動作を評価するには、コマンドは次のようになります。

[!code-console[Main](performing-a-what-if-deployment/samples/sample2.cmd)]

"試用モード" 展開の結果に問題がなければ、 **/t**フラグを **/y**フラグに置き換えてライブデプロイを実行できます。

[!code-console[Main](performing-a-what-if-deployment/samples/sample3.cmd)]

> [!NOTE]
> *. .Deploy*ファイルのコマンドラインオプションの詳細については、「[方法: .Deploy ファイルを使用して展開パッケージをインストール](https://msdn.microsoft.com/library/ff356104.aspx)する」を参照してください。 フラグを指定せずに *.deploy*ファイルを実行すると、使用可能なフラグの一覧がコマンドプロンプトに表示されます。

## <a name="performing-a-what-if-deployment-for-databases"></a>データベースの "What If" 配置の実行

このセクションでは、VSDBCMD ユーティリティを使用して、スキーマベースの増分データベース配置を実行していることを前提としています。 この方法の詳細については、「[データベースプロジェクトの配置](../web-deployment-in-the-enterprise/deploying-database-projects.md)」を参照してください。 ここで説明する概念を適用する前に、このトピックについて理解しておくことをお勧めします。

**配置**モードで VSDBCMD を使用する場合は、 **/dd** (または **/deploytodatabase**) フラグを使用して、VSDBCMD が実際にデータベースを配置するか、配置スクリプトを生成するかを制御できます。 .Dbschema ファイルを配置している場合は、次のような動作になります。

- **/Dd +** または **/dd**を指定すると、VSDBCMD によって配置スクリプトが生成され、データベースが配置されます。
- **/Ddを**指定した場合、またはスイッチを省略した場合、VSDBCMD では配置スクリプトのみが生成されます。

> [!NOTE]
> .Dbschema ファイルではなく、deploymanifest ファイルを配置している場合、 **/dd**スイッチの動作ははるかに複雑になります。 基本的に、VSDBCMD では、deploymanifest ファイルに値**True**の**deploytodatabase**要素が含まれている場合、 **/dd**スイッチの値は無視されます。 [データベースプロジェクトを配置](../web-deployment-in-the-enterprise/deploying-database-projects.md)すると、この動作が完全に記述されます。

たとえば、実際にデータベースを配置せずに**Contactmanager**データベースの配置スクリプトを生成する場合、VSDBCMD コマンドは次のようになります。

[!code-console[Main](performing-a-what-if-deployment/samples/sample4.cmd)]

VSDBCMD はデータベースの差分配置ツールであるため、配置スクリプトは、現在のデータベース (存在する場合) を指定したスキーマに更新するために必要なすべての SQL コマンドを含むように動的に生成されます。 配置スクリプトを確認することは、配置が現在のデータベースとそれに含まれるデータに与える影響を決定するのに便利な方法です。 たとえば、次のような判断が必要になる場合があります。

- 既存のテーブルが削除されるかどうか、およびそれによってデータが失われるかどうかを示します。
- テーブルを分割またはマージする場合など、操作の順序によってデータ損失のリスクが生じるかどうか。

デプロイスクリプトに問題がなければ、VSDBCMD **+** フラグを使用して、変更を加えることができます。 または、必要に応じて配置スクリプトを編集し、データベースサーバーで手動で実行することもできます。

## <a name="integrating-what-if-functionality-into-custom-project-files"></a>"What If" 機能のカスタムプロジェクトファイルへの統合

より複雑な配置シナリオでは、「[プロジェクトファイルについ](../web-deployment-in-the-enterprise/understanding-the-project-file.md)て」で説明されているように、カスタム Microsoft Build Engine (MSBuild) プロジェクトファイルを使用してビルドおよび配置ロジックをカプセル化することをお勧めします。 たとえば、 [Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)サンプルソリューションでは、次のように*発行します。*

- ソリューションをビルドします。
- Web 配置を使用して、ContactManager の Mvc アプリケーションをパッケージ化して配置します。
- Web 配置を使用して、ContactManager. サービスアプリケーションをパッケージ化して配置します。
- **Contactmanager**データベースをデプロイします。

この方法で、複数の web パッケージまたはデータベースの配置を1つの手順のプロセスに統合する場合は、"what-if" モードで配置全体を実行するオプションを使用することもできます。

この方法を説明するには、 *Publish*ファイルを使用します。 まず、"what-if" 値を格納するプロパティを作成する必要があります。

[!code-xml[Main](performing-a-what-if-deployment/samples/sample5.xml)]

この例では、 **WhatIf**という名前のプロパティを作成しました。既定値は**false**です。 この値をオーバーライドするには、後で説明するように、コマンドラインパラメーターでプロパティを**true**に設定します。

次の段階では、VSDBCMD コマンドを Web 配置パラメーター化し、フラグに**WhatIf**プロパティ値が反映されるようにします。 たとえば、次のターゲット ( *Publish. proj*ファイルと簡略化された) は、 *.deploy*ファイルを実行して web パッケージを配置します。 既定では、コマンドには、 **/y**スイッチ ("yes" または update mode) が含まれています。 **WhatIf**が**true**に設定されている場合、これは **/t**スイッチ (試用版または "what-if" モード) に置き換えられます。

[!code-xml[Main](performing-a-what-if-deployment/samples/sample6.xml)]

同様に、次のターゲットは、VSDBCMD ユーティリティを使用してデータベースを配置します。 既定では、 **/dd**スイッチは含まれていません。 つまり、VSDBCMD は配置スクリプトを生成しますが、"what-if"&#x2014;シナリオではなく、データベースを展開しません。 **WhatIf**プロパティが**true**に設定されていない場合は、 **/dd**スイッチが追加され、VSDBCMD によってデータベースが配置されます。

[!code-xml[Main](performing-a-what-if-deployment/samples/sample7.xml)]

同じ方法を使用して、プロジェクトファイル内の関連するすべてのコマンドをパラメーター化することができます。 "What-if" 配置を実行する場合は、コマンドラインから**WhatIf**プロパティ値を指定するだけです。

[!code-console[Main](performing-a-what-if-deployment/samples/sample8.cmd)]

このようにして、すべてのプロジェクトコンポーネントの "what-if" 配置を1回の手順で実行できます。

## <a name="conclusion"></a>まとめ

このトピックでは、Web 配置、VSDBCMD、および MSBuild を使用して "what-if" 配置を実行する方法について説明します。 "What-if" 展開を使用すると、移行先の環境に実際に変更を加える前に、提案された展開の影響を評価できます。

## <a name="further-reading"></a>参考資料

Web 配置のコマンドライン構文の詳細については、「 [Web 配置操作の設定](https://technet.microsoft.com/library/dd569089(WS.10).aspx)」を参照してください。 *.Deploy*ファイルを使用する場合のコマンドラインオプションのガイダンスについては、「[方法: .Deploy ファイルを使用して展開パッケージをインストール](https://msdn.microsoft.com/library/ff356104.aspx)する」を参照してください。 VSDBCMD コマンドライン構文のガイダンスについては、「 [VSDBCMD のコマンドラインリファレンス」を参照してください。EXE (デプロイとスキーマのインポート)](https://msdn.microsoft.com/library/dd193283.aspx)。

> [!div class="step-by-step"]
> [前へ](advanced-enterprise-web-deployment.md)
> [次へ](customizing-database-deployments-for-multiple-environments.md)
