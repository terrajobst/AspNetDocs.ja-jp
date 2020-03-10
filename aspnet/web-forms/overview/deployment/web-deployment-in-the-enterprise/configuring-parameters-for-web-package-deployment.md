---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/configuring-parameters-for-web-package-deployment
title: Web パッケージ配置のパラメーターの構成 |Microsoft Docs
author: jrjlee
description: このトピックでは、インターネットインフォメーションサービス (IIS) web アプリケーション名、接続文字列、サービスエンドポイントなどのパラメーター値を設定する方法について説明し,...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 37947d79-ab1e-4ba9-9017-52e7a2757414
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/configuring-parameters-for-web-package-deployment
msc.type: authoredcontent
ms.openlocfilehash: f04ace98d81a33053b10cab7e40dbd75a6c0992c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78438400"
---
# <a name="configuring-parameters-for-web-package-deployment"></a>Web パッケージ配置のパラメーターを構成する

[Jason Lee](https://github.com/jrjlee)

[[Download PDF]\(PDF をダウンロード\)](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> このトピックでは、リモート IIS web サーバーに web パッケージを展開するときに、インターネットインフォメーションサービス (IIS) web アプリケーション名、接続文字列、サービスエンドポイントなどのパラメーター値を設定する方法について説明します。

Web アプリケーションプロジェクトをビルドすると、ビルドおよびパッケージ化プロセスによって次の3つのキーファイルが生成されます。

- *[プロジェクト名] .zip*ファイル。 これは、web アプリケーションプロジェクトの web 配置パッケージです。 このパッケージには、リモート IIS web サーバーで web アプリケーションを再作成するために必要なすべてのアセンブリ、ファイル、データベーススクリプト、およびリソースが含まれています。
- *[プロジェクト名]. .deploy*ファイルを指定します。 これには、web 配置パッケージをリモート IIS web サーバーに発行するパラメーター化された Web 配置 (Msdeploy.exe) コマンドのセットが含まれます。
- *[プロジェクト名]。SetParameters .xml*ファイル。 これにより、Msdeploy.exe コマンドにパラメーター値のセットが提供されます。 このファイルの値を更新し、Web パッケージを配置するときにコマンドラインパラメーターとして Web 配置に渡すことができます。

> [!NOTE]
> ビルドおよびパッケージ化のプロセスの詳細については、「 [Web アプリケーションプロジェクトのビルドおよびパッケージ化](building-and-packaging-web-application-projects.md)」を参照してください。

*Setparameters .xml*ファイルは、web アプリケーションプロジェクトファイルと、プロジェクト内の構成ファイルから動的に生成されます。 プロジェクトをビルドしてパッケージ化すると、Web 発行パイプライン (WPP) によって、配置先の IIS Web アプリケーションや任意のデータベース接続文字列などの配置環境間で変更される可能性のある多くの変数が自動的に検出されます。 これらの値は、web 配置パッケージで自動的にパラメーター化され、 *Setparameters .xml*ファイルに追加されます。 たとえば *、web アプリケーション*プロジェクトの web.config ファイルに接続文字列を追加すると、ビルドプロセスによってこの変更が検出され、それに応じて*setparameters .xml*ファイルにエントリが追加されます。

多くの場合、この自動パラメーター化は十分です。 ただし、ユーザーがアプリケーションの設定やサービスエンドポイントの Url など、デプロイ環境間で他の設定を変更する必要がある場合は、展開パッケージでこれらの値をパラメーター化し、対応するエントリを*Setparameters .xml*ファイルに追加するように WPP に指示する必要があります。 次のセクションでは、その方法について説明します。

### <a name="automatic-parameterization"></a>自動パラメーター化

Web アプリケーションをビルドしてパッケージ化すると、WPP は自動的に次のようなパラメーター化を行います。

- 宛先 IIS web アプリケーションのパスと名前。
- *Web.config ファイル内*の任意の接続文字列。
- プロジェクトのプロパティページの **[パッケージ/発行]** タブに追加するすべてのデータベースの接続文字列。

たとえば、パラメーター化プロセスに触れることなく[Contact manager](the-contact-manager-solution.md)サンプルソリューションをビルドしてパッケージ化する場合、次のように WPP によってこの*contactmanager*サンプルファイルが生成されます。

[!code-xml[Main](configuring-parameters-for-web-package-deployment/samples/sample1.xml)]

この場合、次のようになります。

- **Iis Web アプリケーション名**パラメーターは、web アプリケーションを配置する iis パスです。 既定値は、プロジェクトのプロパティページの [**パッケージ/発行] Web**ページから取得されます。
- **Applicationservices-Web.config 接続文字列**パラメーターは、 *Web.config ファイルの* **connectionStrings/add**要素から生成されました。 これは、アプリケーションがメンバーシップデータベースにアクセスするために使用する接続文字列を表します。 ここで指定する値は、配置された*web.config*ファイルに置き換えられます。 既定値は *、配置前の web.config ファイル*から取得されます。

また、WPP は、生成する展開パッケージでこれらのプロパティをパラメーター化します。 展開パッケージをインストールするときに、これらのプロパティの値を指定できます。 IIS マネージャーを使用して手動でパッケージをインストールする場合、「 [Web パッケージを手動でインストール](manually-installing-web-packages.md)する」で説明されているように、インストールウィザードでは、任意のパラメーターの値を指定するように求められます。 「 [Web パッケージの配置](deploying-web-packages.md)」で説明されているように、 *.deploy*ファイルを使用してパッケージをリモートでインストールした場合、Web 配置は、パラメーター値を提供するためにこの*setparameters .xml*ファイルを検索します。 *Setparameters .xml*ファイルの値は手動で編集できます。また、自動ビルドおよび配置プロセスの一環としてファイルをカスタマイズすることもできます。 このプロセスの詳細については、このトピックの後半で説明します。

### <a name="custom-parameterization"></a>カスタムパラメーター化

より複雑な配置シナリオでは、プロジェクトを配置する前に追加のプロパティをパラメーター化することが必要になることがよくあります。 一般に、接続先の環境によって異なるプロパティと設定をパラメーター化する必要があります。 次のようなものがあります。

- *Web.config ファイル内*のサービスエンドポイント。
- *Web.config ファイルの*アプリケーション設定。
- ユーザーに指定を求めるその他の宣言プロパティ。

これらのプロパティをパラメーター化する最も簡単な方法は、web アプリケーションプロジェクトのルートフォルダーに*parameters .xml*ファイルを追加することです。 たとえば、Contact Manager ソリューションでは、ContactManager. Mvc プロジェクトには、ルートフォルダーに*parameters .xml*ファイルが含まれています。

![](configuring-parameters-for-web-package-deployment/_static/image1.png)

このファイルを開くと、1つの**パラメーター**エントリが含まれていることがわかります。 このエントリでは、XML パス言語 (XPath) クエリを使用して、 *web .config*ファイル内の contactservice WINDOWS COMMUNICATION FOUNDATION (WCF) サービスのエンドポイント URL を検索し、パラメーター化しています。

[!code-xml[Main](configuring-parameters-for-web-package-deployment/samples/sample2.xml)]

配置パッケージのエンドポイント URL をパラメーター化するだけでなく、WPP は、配置パッケージと共に生成される*Setparameters .xml*ファイルに対応するエントリも追加します。

[!code-xml[Main](configuring-parameters-for-web-package-deployment/samples/sample3.xml)]

展開パッケージを手動でインストールすると、自動的にパラメーター化されたプロパティと共に、IIS マネージャーによってサービスエンドポイントアドレスの入力が求められます。 *.Deploy*ファイルを実行して配置パッケージをインストールする場合は、 *setparameters .xml*ファイルを編集して、自動的にパラメーター化されたプロパティの値と共にサービスエンドポイントアドレスの値を指定できます。

*パラメーターの .xml*ファイルを作成する方法の詳細については、「[方法: パッケージのインストール時にパラメーターを使用して展開設定を構成](https://msdn.microsoft.com/library/ff398068.aspx)する」を参照してください。 **「Web.config ファイル設定に展開パラメーターを使用する**」という名前の手順では、手順を追って説明します。

## <a name="modifying-the-setparametersxml-file"></a>SetParameters .xml ファイルの変更

*.Deploy*ファイルを実行するか、コマンドライン&#x2014;から msdeploy.exe を実行して、web アプリケーションパッケージを手動で&#x2014;展開する予定がある場合は、配置前に*setparameters .xml*ファイルを手動で編集する必要はありません。 ただし、エンタープライズ規模のソリューションで作業している場合は、大規模で自動化されたビルドおよび配置プロセスの一部として、web アプリケーションパッケージをデプロイする必要があります。 このシナリオでは、Microsoft Build Engine (MSBuild) を使用して、 *Setparameters .xml*ファイルを変更する必要があります。 これを行うには、MSBuild **XmlPoke**タスクを使用します。

[Contact Manager サンプルソリューション](the-contact-manager-solution.md)では、このプロセスについて説明します。 次のコード例は、この例に関連する詳細のみを表示するように編集されています。

> [!NOTE]
> サンプルソリューションのプロジェクトファイルモデルの概要と、一般的なカスタムプロジェクトファイルの概要については、「[プロジェクトファイルについ](understanding-the-project-file.md)て」および「[ビルドプロセスについ](understanding-the-build-process.md)て」を参照してください。

まず、対象のパラメーター値は、環境固有のプロジェクトファイルのプロパティとして定義されます (たとえば、 *Env Dev. proj*)。

[!code-xml[Main](configuring-parameters-for-web-package-deployment/samples/sample4.xml)]

> [!NOTE]
> 独自のサーバー環境用に環境固有のプロジェクトファイルをカスタマイズする方法については、「[ターゲット環境の配置プロパティを構成](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md)する」を参照してください。

次に、このプロパティを*インポートします*。 各*Setparameters .xml*ファイルは *.deploy*ファイルに関連付けられているため、最終的にプロジェクトファイルで各 *.deploy*ファイルを呼び出す必要があります。プロジェクトファイルでは *、各 .deploy*ファイルの MSBuild*項目*を作成し、*項目メタデータ*として関心のあるプロパティを定義します。

[!code-xml[Main](configuring-parameters-for-web-package-deployment/samples/sample5.xml)]

この場合、次のようになります。

- **ParametersXml**メタデータ値は、 *setparameters .xml*ファイルの場所を示します。
- **Iiswebappname**値は、web アプリケーションをデプロイする IIS パスです。
- メンバーシップ**Dbconnectionstring**値はメンバーシップデータベースの接続文字列で、 **MembershipDBConnectionName**値は*setparameters .xml*ファイル内の対応するパラメーターの**name**属性です。
- **Serviceendpointvalue**の値は、移行先サーバー上の WCF サービスのエンドポイントアドレスです。 **ServiceEndpointParamName**値は、 *setparameters .xml*ファイル内の対応するパラメーターの name 属性です。

最後に、 *Publish*ファイルの**publishwebpackages**ターゲットは、 **XmlPoke**タスクを使用して、 *setparameters .xml*ファイル内のこれらの値を変更します。

[!code-xml[Main](configuring-parameters-for-web-package-deployment/samples/sample6.xml)]

各**XmlPoke**タスクでは、次の4つの属性値が指定されていることがわかります。

- **XmlInputPath**属性は、変更するファイルを検索する場所をタスクに指示します。
- **Query**属性は、変更する XML ノードを識別する XPath クエリです。
- **Value**属性は、選択した XML ノードに挿入する新しい値です。
- **Condition**属性は、タスクを実行する条件、または実行しない条件です。 このような場合、条件によって、 *Setparameters .xml*ファイルに null 値または空の値が挿入されないようにします。

## <a name="conclusion"></a>まとめ

このトピックでは、 *Setparameters .xml*ファイルの役割について説明し、web アプリケーションプロジェクトをビルドするときに生成される方法について説明しました。 また、*パラメーター .xml*ファイルをプロジェクトに追加することで、追加の設定をパラメーター化する方法についても説明しました。 また、プロジェクトファイルの**XmlPoke**タスクを使用して、大きな自動化されたビルドプロセスの一部として*setparameters .xml*ファイルを変更する方法についても説明します。

次のトピック「 [Web パッケージの配置](deploying-web-packages.md)」では、 *.deploy*ファイルを実行するか、msdeploy.exe コマンドを直接使用して、web パッケージを配置する方法について説明します。 どちらの場合も、 *Setparameters .xml*ファイルを配置パラメーターとして指定できます。

## <a name="further-reading"></a>参考資料

Web パッケージの作成方法の詳細については、「 [Web アプリケーションプロジェクトのビルドおよびパッケージ化](building-and-packaging-web-application-projects.md)」を参照してください。 実際に web パッケージを配置する方法のガイダンスについては、「 [Web パッケージの配置](deploying-web-packages.md)」を参照してください。 *パラメーター .xml*ファイルを作成する方法の詳細な手順については、「[方法: パッケージのインストール時にパラメーターを使用して展開設定を構成](https://msdn.microsoft.com/library/ff398068.aspx)する」を参照してください。

Web 配置でのパラメーター化に関する全般的な情報については、「[アクションの Web 配置のパラメーター](https://go.microsoft.com/?linkid=9805119)化 (ブログの投稿)」を参照してください。

> [!div class="step-by-step"]
> [前へ](building-and-packaging-web-application-projects.md)
> [次へ](deploying-web-packages.md)
