---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/understanding-the-build-process
title: ビルドプロセスについてMicrosoft Docs
author: jrjlee
description: このトピックでは、エンタープライズ規模のビルドおよび配置プロセスのチュートリアルを提供します。 このトピックで説明する方法では、カスタムの Microsoft Build Engin を使用します。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 5b982451-547b-4a2f-a5dc-79bc64d84d40
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/understanding-the-build-process
msc.type: authoredcontent
ms.openlocfilehash: 802d93f7ca987d018967275bae68b8c56d883a25
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78520834"
---
# <a name="understanding-the-build-process"></a>ビルド処理について理解する

[Jason Lee](https://github.com/jrjlee)

[[Download PDF]\(PDF をダウンロード\)](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> このトピックでは、エンタープライズ規模のビルドおよび配置プロセスのチュートリアルを提供します。 このトピックで説明する方法では、カスタム Microsoft Build Engine (MSBuild) プロジェクトファイルを使用して、プロセスのすべての側面をきめ細かく制御します。 プロジェクトファイル内では、カスタム MSBuild ターゲットを使用して、インターネットインフォメーションサービス (IIS) Web 配置ツール (Msdeploy.exe) やデータベース配置ユーティリティ VSDBCMD などの配置ユーティリティを実行します。
> 
> > [!NOTE]
> > 前のトピック「[プロジェクトファイルについ](understanding-the-project-file.md)て」では、MSBuild プロジェクトファイルの主要なコンポーネントについて説明し、複数のターゲット環境への配置をサポートするために分割されたプロジェクトファイルの概念を紹介しました。 これらの概念を理解していない場合は、このトピックを使用する前に、「[プロジェクトファイルについて理解](understanding-the-project-file.md)する必要があります」を参照してください。

このトピックでは、Fabrikam, Inc. という架空の企業のエンタープライズ展開要件に基づいて、一連のチュートリアルの一部を説明します。このチュートリアルシリーズでは、&#x2014; [Contact Manager ソリューション](the-contact-manager-solution.md)&#x2014;のサンプルソリューションを使用して、ASP.NET MVC 3 アプリケーション、Windows Communication Foundation (WCF) サービス、データベースプロジェクトなど、現実的なレベルの複雑さを持つ web アプリケーションを表します。

これらのチュートリアルの中核となる配置方法は、「[プロジェクトファイルについ](understanding-the-project-file.md)て」で説明されている分割プロジェクトファイルアプローチに基づいています。この&#x2014;プロジェクトファイルには、ビルドプロセスは、すべての変換先環境に適用されるビルド命令を含む2つのプロジェクトファイルと、環境固有のビルドおよび配置設定を含んでいます。 ビルド時に、環境固有のプロジェクトファイルが環境に依存しないプロジェクトファイルにマージされ、ビルド命令の完全なセットが形成されます。

## <a name="build-and-deployment-overview"></a>ビルド & デプロイの概要

[Contact Manager ソリューション](the-contact-manager-solution.md)では、3つのファイルによってビルドとデプロイのプロセスが制御されます。

- *ユニバーサルプロジェクトファイル*(*Publish. proj*)。 これには、対象となる環境間で変更されないビルドおよび配置の手順が含まれます。
- *環境固有のプロジェクトファイル*(*Env Dev. proj*)。 これには、特定の対象環境に固有のビルドおよび配置の設定が含まれます。 たとえば、 *env-Dev. proj*ファイルを使用して、開発者またはテスト環境の設定を指定し、環境のステージング環境の設定を提供するために、 *env*という名前の別のファイルを作成することができます。
- *コマンドファイル*(*Publish-Dev*)。 これには、実行するプロジェクトファイルを指定する Msbuild.exe コマンドが含まれています。 すべての変換先環境に対してコマンドファイルを作成できます。各ファイルには、別の環境固有のプロジェクトファイルを指定する Msbuild.exe コマンドが含まれています。 これにより、開発者は、適切なコマンドファイルを実行するだけで、さまざまな環境に配置できます。

サンプルソリューションでは、[ソリューションの発行] フォルダーにこれら3つのファイルがあります。

![](understanding-the-build-process/_static/image1.png)

これらのファイルについてさらに詳しく説明する前に、この方法を使用した場合のビルドプロセス全体のしくみを見てみましょう。 大まかに言えば、ビルドと配置のプロセスは次のようになります。

![](understanding-the-build-process/_static/image2.png)

最初に実行されるのは、2つの&#x2014;プロジェクトファイル (ユニバーサルビルドと配置の手順を含む) と、環境&#x2014;固有の設定を含むファイルが1つのプロジェクトファイルにマージされることです。 MSBuild は、プロジェクトファイルの指示に従って動作します。 各プロジェクトのプロジェクトファイルを使用して、ソリューション内の各プロジェクトをビルドします。 次に、Web 配置 (Msdeploy.exe) などの他のツールを呼び出し、Web コンテンツとデータベースをターゲット環境に配置するための VSDBCMD ユーティリティを呼び出します。

最初から最後まで、ビルドと展開のプロセスで次のタスクが実行されます。

1. 新しいビルドの準備として、出力ディレクトリの内容を削除します。
2. ソリューション内の各プロジェクトをビルドします。

    1. この場合の&#x2014;web プロジェクトでは、ASP.NET MVC web アプリケーションと WCF web サービス&#x2014;のビルドプロセスによって、各プロジェクトの web 配置パッケージが作成されます。
    2. データベースプロジェクトの場合、ビルドプロセスによって、各プロジェクトの配置マニフェスト (deploymanifest ファイル) が作成されます。
3. VSDBCMD ユーティリティを使用して、ソリューション内の各データベースプロジェクトを配置します。これには、プロジェクト&#x2014;ファイルのさまざまなプロパティ、ターゲット接続&#x2014;文字列、データベース名、および deploymanifest ファイルを使用します。
4. Msdeploy.exe ユーティリティを使用してソリューション内の各 web プロジェクトを配置し、プロジェクトファイルのさまざまなプロパティを使用して配置プロセスを制御します。

サンプルソリューションを使用して、このプロセスをより詳細にトレースできます。

> [!NOTE]
> 独自のサーバー環境用に環境固有のプロジェクトファイルをカスタマイズする方法については、「[ターゲット環境の配置プロパティを構成](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md)する」を参照してください。

## <a name="invoking-the-build-and-deployment-process"></a>ビルド & デプロイプロセスの呼び出し

開発者テスト環境に Contact Manager ソリューションを配置するには、 *Publish-Dev*コマンドファイルを実行します。 これにより Msbuild.exe が呼び出され、実行するプロジェクトファイルとして*Publish*が指定され、パラメーター値として*proj が*指定されます。

[!code-console[Main](understanding-the-build-process/samples/sample1.cmd)]

> [!NOTE]
> **/Fl**スイッチ ( **/fileLogger**の short) は、ビルド出力を現在のディレクトリの*msbuild.exe*という名前のファイルに記録します。 詳細については、「 [MSBuild コマンドラインリファレンス](https://msdn.microsoft.com/library/ms164311.aspx)」を参照してください。

この時点で、MSBuild は実行を開始し、*発行の proj*ファイルを読み込み、そこに含まれる命令の処理を開始します。 最初の命令は、 **TargetEnvPropsFile**パラメーターによって指定されたプロジェクトファイルをインポートするよう MSBuild に指示します。

[!code-xml[Main](understanding-the-build-process/samples/sample2.xml)]

**TargetEnvPropsFile**パラメーターによって*env*ファイルが指定されるため、MSBuild では、 *Env*ファイルの内容が*Publish*ファイルにマージされます。

マージされたプロジェクトファイルで MSBuild が検出する次の要素は、プロパティグループです。 プロパティは、ファイルに出現する順序で処理されます。 MSBuild は、各プロパティのキーと値のペアを作成し、指定された条件が満たされていることを示します。 ファイルの後半で定義されているプロパティは、ファイルで定義されている名前と同じ名前のプロパティを上書きします。 たとえば、 **Outputroot**プロパティについて考えてみます。

[!code-xml[Main](understanding-the-build-process/samples/sample3.xml)]

MSBuild が最初の**outputroot**要素を処理するときに、同様の名前付きパラメーターが指定されていない場合、 **outputroot**プロパティの値が. に設定されます。 **\** 発行します。2番目の**outputroot**要素が検出されると、条件が**true**と評価されると、 **Outputroot**プロパティの値が**OutDir**パラメーターの値で上書きされます。

MSBuild が検出する次の要素は、 **Projectstobuild**という名前の項目を含む単一の項目グループです。

[!code-xml[Main](understanding-the-build-process/samples/sample4.xml)]

MSBuild は、 **Projectstobuild**という名前の項目リストを構築することによって、この命令を処理します。 この場合、項目の一覧には、ソリューションファイル&#x2014;のパスとファイル名の1つの値が含まれます。

この時点で、残りの要素はターゲットです。 ターゲットは、プロパティと項目&#x2014;とは異なる方法で処理されます。つまり、ターゲットは、ユーザーが明示的に指定した場合、またはプロジェクトファイル内の別の構造体によって呼び出された場合を除き、処理されません。 開いている**プロジェクト**タグに**defaulttargets**属性が含まれていることを思い出してください。

[!code-xml[Main](understanding-the-build-process/samples/sample5.xml)]

これにより、msbuild.exe が呼び出されたときにターゲットが指定されていない場合、 **Fullpublish**ターゲットを呼び出すように msbuild に指示します。 **Fullpublish**ターゲットにタスクが含まれていません。代わりに、単に依存関係の一覧を指定します。

[!code-xml[Main](understanding-the-build-process/samples/sample6.xml)]

この依存関係は、 **Fullpublish**ターゲットを実行するために、指定された順序でこのターゲットの一覧を呼び出す必要があることを MSBuild に指示します。

1. **クリーン**ターゲットを呼び出す必要があります。
2. **Buildprojects**ターゲットを呼び出す必要があります。
3. **GatherPackagesForPublishing**ターゲットを呼び出す必要があります。
4. **Publishdbpackages**ターゲットを呼び出す必要があります。
5. **Publishwebpackages**ターゲットを呼び出す必要があります。

### <a name="the-clean-target"></a>クリーンターゲット

**クリーン**ターゲットは、基本的に、新しいビルドの準備として、出力ディレクトリとそのすべての内容を削除します。

[!code-xml[Main](understanding-the-build-process/samples/sample7.xml)]

ターゲットに**ItemGroup**要素が含まれていることに注意してください。 **ターゲット**要素内にプロパティまたは項目を定義すると、*動的*なプロパティと項目が作成されます。 つまり、プロパティまたは項目は、ターゲットが実行されるまで処理されません。 出力ディレクトリが存在しないか、ビルドプロセスが開始するまでファイルが含まれている可能性があるため、 **\_FilesToDelete** list を静的項目としてビルドすることはできません。実行が進行するまで待機する必要があります。 そのため、リストはターゲット内の動的な項目としてビルドします。

> [!NOTE]
> この場合、**クリーン**ターゲットは最初に実行されるため、動的な項目グループを使用する必要はありません。 ただし、この種のシナリオでは、ある時点で異なる順序でターゲットを実行する場合があるので、動的なプロパティと項目を使用することをお勧めします。  
> また、使用されない項目を宣言しないようにすることもお勧めします。 特定のターゲットによってのみ使用される項目がある場合は、ターゲット内に配置して、ビルドプロセスの不要なオーバーヘッドを解消することを検討してください。

動的な項目については、**クリーン**ターゲットは非常に単純であり、組み込みの**Message**、 **Delete**、および**RemoveDir**タスクを使用して次のことを行います。

1. ロガーにメッセージを送信します。
2. 削除するファイルの一覧を作成します。
3. ファイルを削除します。
4. 出力ディレクトリを削除します。

### <a name="the-buildprojects-target"></a>BuildProjects ターゲット

**Buildprojects**ターゲットは基本的に、サンプルソリューション内のすべてのプロジェクトをビルドします。

[!code-xml[Main](understanding-the-build-process/samples/sample8.xml)]

このターゲットについては、前のトピック「[プロジェクトファイルについ](understanding-the-project-file.md)て」で説明しました。これは、タスクとターゲットがプロパティと項目を参照する方法を説明するためのものです。 この時点で、主に**MSBuild**タスクに関心があります。 このタスクを使用すると、複数のプロジェクトをビルドできます。 このタスクでは、Msbuild.exe の新しいインスタンスは作成されません。現在実行中のインスタンスを使用して、各プロジェクトをビルドします。 この例の重要なポイントは、展開のプロパティです。

- **Deployonbuild**プロパティは、各プロジェクトのビルドが完了したときに、プロジェクト設定の配置手順を実行するよう MSBuild に指示します。
- **Deploytarget**プロパティは、プロジェクトのビルド後に呼び出すターゲットを指定します。 この場合、**パッケージ**ターゲットは、配置可能な web パッケージにプロジェクト出力をビルドします。

> [!NOTE]
> **パッケージ**ターゲットは、MSBuild と Web 配置の統合を提供する Web 発行パイプライン (WPP) を呼び出します。 WPP によって提供される組み込みターゲットを確認する場合は、% PROGRAMFILES (x86)% \ MSBuild\Microsoft\VisualStudio\v10.0\Web フォルダー内のファイルを確認して*みてください*。

### <a name="the-gatherpackagesforpublishing-target"></a>GatherPackagesForPublishing ターゲット

**GatherPackagesForPublishing**ターゲットを調べると、実際にはタスクが含まれていないことがわかります。 代わりに、3つの動的な項目を定義する1つの項目グループが含まれています。

[!code-xml[Main](understanding-the-build-process/samples/sample9.xml)]

これらの項目は、 **Buildprojects**ターゲットの実行時に作成された配置パッケージを参照します。 これらの項目をプロジェクトファイルで静的に定義することはできません。これは、項目が参照するファイルが、 **Buildprojects**ターゲットが実行されるまで存在しないためです。 代わりに、項目は、 **Buildprojects**ターゲットが実行されるまで呼び出されないターゲット内で動的に定義される必要があります。

項目はこのターゲット&#x2014;内では使用されません。このターゲットは、項目と各項目の値に関連付けられているメタデータを作成するだけです。 これらの要素が処理されると、 **Publishpackages**項目に2つの値 ( *Contactmanager. Mvc*ファイルのパスと*contactmanager. Service. .deploy*ファイルへのパス) が格納されます。 Web 配置は、各プロジェクトの web パッケージの一部としてこれらのファイルを作成します。これらのファイルは、パッケージを配置するために移行先サーバーで呼び出す必要があります。 これらのファイルのいずれかを開くと、基本的に、さまざまなビルド固有のパラメーター値を持つ Msdeploy.exe コマンドが表示されます。

**Dbpublishpackages**項目には、 *Contactmanager. Database. deploymanifest*ファイルへのパスである単一の値が含まれます。

> [!NOTE]
> Deploymanifest ファイルは、データベースプロジェクトをビルドするときに生成され、MSBuild プロジェクトファイルと同じスキーマを使用します。 データベースの配置に必要なすべての情報 (データベーススキーマ (.dbschema) の場所、配置前スクリプトと配置後スクリプトの詳細など) が含まれています。 詳細については、「[データベースビルド & デプロイの概要](https://msdn.microsoft.com/library/aa833165.aspx)」を参照してください。

配置パッケージとデータベース配置マニフェストの作成方法と使用方法については、 [Web アプリケーションプロジェクトのビルドとパッケージ化](building-and-packaging-web-application-projects.md)、および[データベースプロジェクトの配置](deploying-database-projects.md)に関するページを参照してください。

### <a name="the-publishdbpackages-target"></a>PublishDbPackages ターゲット

簡単に言うと、 **Publishdbpackages**ターゲットは VSDBCMD ユーティリティを呼び出して、 **contactmanager**データベースをターゲット環境にデプロイします。 データベース配置の構成には多くの意思決定と微妙な関係があります。詳細については、[データベースプロジェクトの配置](deploying-database-projects.md)と[複数の環境のデータベース配置のカスタマイズ](../advanced-enterprise-web-deployment/customizing-database-deployments-for-multiple-environments.md)に関するページを参照してください。 このトピックでは、このターゲットが実際にどのように機能するかについて説明します。

まず、開始タグに**Outputs**属性が含まれていることに注意してください。

[!code-xml[Main](understanding-the-build-process/samples/sample10.xml)]

これは、ターゲットの*バッチ*処理の例です。 MSBuild プロジェクトファイルでは、バッチ処理はコレクションを反復処理するための手法です。 **Outputs**属性の値 **"% (dbpublishpackages. Identity)"** は、 **Dbpublishpackages**項目リストの**id**メタデータプロパティを参照します。 この記法 **Outputs =% * * * (Itemlist)* は、次のように変換されます。

- **Dbpublishpackages**の項目を、同じ**id**メタデータ値を含む項目のバッチに分割します。
- バッチごとにターゲットを1回実行します。

> [!NOTE]
> **Identity**は、作成時にすべての項目に割り当てられる[組み込みメタデータ値](https://msdn.microsoft.com/library/ms164313.aspx)の1つです。 ここでは、 **item**要素&#x2014;の**Include**属性の値 (項目のパスとファイル名) を参照します。

この場合、同じパスとファイル名を持つ複数の項目を指定することはできないので、基本的には1つのバッチサイズを使用しています。 ターゲットは、データベースパッケージごとに1回実行されます。

**\_Cmd**プロパティにも同様の表記が表示されます。これにより、適切なスイッチで VSDBCMD コマンドが作成されます。

[!code-xml[Main](understanding-the-build-process/samples/sample11.xml)]

この場合、 **% (DatabaseConnectionString)** 、 **% (dbpublishpackages)** 、および **% (dbpublishpackages. FullPath)** はすべて、 **dbpublishpackages**項目コレクションのメタデータ値を参照します。 **\_Cmd**プロパティは、コマンドを呼び出す**Exec**タスクによって使用されます。

[!code-xml[Main](understanding-the-build-process/samples/sample12.xml)]

この表記の結果、 **Exec**タスクは、 **DatabaseConnectionString**、 **targetdatabase**、および**FullPath**メタデータ値の一意の組み合わせに基づいてバッチを作成します。このタスクは、バッチごとに1回実行されます。 *タスクバッチ*の例を次に示します。 ただし、ターゲットレベルのバッチ処理では、項目コレクションが既に単一項目のバッチに分割されているため、 **Exec**タスクは、ターゲットの反復ごとに1回だけ実行されます。 言い換えると、このタスクは、ソリューション内のデータベースパッケージごとに VSDBCMD ユーティリティを1回呼び出します。

> [!NOTE]
> ターゲットとタスクのバッチ処理の詳細については、「MSBuild の[バッチ](https://msdn.microsoft.com/library/ms171473.aspx)処理」、「[ターゲットのバッチの項目メタデータ](https://msdn.microsoft.com/library/ms228229.aspx)」、および「[タスクバッチの項目メタデータ](https://msdn.microsoft.com/library/ms171474.aspx)」を参照してください。

### <a name="the-publishwebpackages-target"></a>PublishWebPackages ターゲット

この時点で、 **Buildprojects**ターゲットが呼び出されました。これにより、サンプルソリューション内の各プロジェクトの web 配置パッケージが生成されます。 各パッケージは、ターゲット環境にパッケージを配置するために必要な Msdeploy.exe コマンドを含む *.deploy*ファイルであり、ターゲット環境の必要な詳細を指定する*setparameters .xml*ファイルが含まれています。 また、 **GatherPackagesForPublishing**ターゲットも呼び出されました。これにより、目的の *.deploy*ファイルを含む項目コレクションが生成されます。 基本的に、 **Publishwebpackages**ターゲットは、次の関数を実行します。

- **XmlPoke**タスクを使用して、各パッケージの*setparameters .xml*ファイルを操作し、ターゲット環境の正しい詳細を含めます。
- 適切なスイッチを使用して、パッケージごとに*配置 .cmd*ファイルを呼び出します。

**Publishdbpackages**ターゲットと同様に、 **publishdbpackages**ターゲットはターゲットバッチを使用して、ターゲットが web パッケージごとに1回実行されるようにします。

[!code-xml[Main](understanding-the-build-process/samples/sample13.xml)]

ターゲット内では、 **Exec**タスクを使用して、各 web パッケージの*配置 .cmd*ファイルを実行します。

[!code-xml[Main](understanding-the-build-process/samples/sample14.xml)]

Web パッケージの配置の構成の詳細については、「 [Web アプリケーションプロジェクトのビルドおよびパッケージ化](building-and-packaging-web-application-projects.md)」を参照してください。

## <a name="conclusion"></a>まとめ

このトピックでは、Contact Manager サンプルソリューションのビルドおよび配置プロセスを開始から終了まで制御するために、分割プロジェクトファイルを使用する方法のチュートリアルを提供しました。 このアプローチを使用すると、環境固有のコマンドファイルを実行するだけで、複雑なエンタープライズ規模のデプロイを単一の反復可能な手順で実行できます。

## <a name="further-reading"></a>参考資料

プロジェクトファイルと WPP の詳細については、「Microsoft Build Engine の内部」を参照してください[。: MSBuild と Team Foundation Build](http://amzn.com/0735645248) By 作成者 Iロウ Hashimi およびウィリアム Bartholomew、ISBN: 978-0-7356-4524-0。

> [!div class="step-by-step"]
> [前へ](understanding-the-project-file.md)
> [次へ](building-and-packaging-web-application-projects.md)
