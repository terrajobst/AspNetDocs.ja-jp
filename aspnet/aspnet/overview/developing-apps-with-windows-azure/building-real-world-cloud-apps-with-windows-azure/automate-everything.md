---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/automate-everything
title: すべてを自動化 (Azure を使用した実際のクラウドアプリの構築) |Microsoft Docs
author: MikeWasson
description: Azure 電子ブックを使用した実際のクラウドアプリの構築は、Scott Guthrie によって開発されたプレゼンテーションに基づいています。 13のパターンとベストプラクティスについて説明します。
ms.author: riande
ms.date: 06/12/2014
ms.assetid: ba6e6baa-9b9f-471f-b39d-b007a3addadc
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/automate-everything
msc.type: authoredcontent
ms.openlocfilehash: e741a753a36ebdaefbff8eee0b38911785c716ac
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457168"
---
# <a name="automate-everything-building-real-world-cloud-apps-with-azure"></a>すべてを自動化 (Azure を使用した実際のクラウドアプリの構築)

[Mike Wasson](https://github.com/MikeWasson)、 [Rick Anderson](https://twitter.com/RickAndMSFT)、 [Tom Dykstra](https://github.com/tdykstra)

[修正 It プロジェクトをダウンロード](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)するか[、電子書籍をダウンロード](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)します

> Azure 電子ブック**を使用した実際のクラウドアプリの構築**は、Scott Guthrie によって開発されたプレゼンテーションに基づいています。 ここでは、クラウド用の web アプリの開発を成功させるのに役立つ13のパターンとプラクティスについて説明します。 電子書籍の概要については、[最初の章](introduction.md)を参照してください。

最初の3つのパターンは、特にクラウドプロジェクトに対して、実際にはどのようなソフトウェア開発プロジェクトにも適用されます。 このパターンは、開発タスクの自動化に関するものです。 手動プロセスは低速でエラーが発生しやすいため、これは重要なトピックです。可能な限り多くの機能を自動化することで、高速で信頼性の高い、アジャイルなワークフローを設定できます。 これは、オンプレミスの環境で自動化することが困難または不可能な多くのタスクを簡単に自動化できるため、クラウド開発にとっては一意です。 たとえば、新しい web サーバーとバックエンド Vm、データベース、blob ストレージ (ファイルストレージ)、キューなどを含むテスト環境全体を設定できます。

## <a name="devops-workflow"></a>DevOps ワークフロー

"DevOps" という言葉が増えています。 ソフトウェアを効率的に開発するために、開発と運用のタスクを統合する必要があるという認識から除外された用語。 有効にするワークフローの種類は、アプリを開発し、デプロイし、運用環境で使用して学習し、学習した内容に応じてそれを変更し、そのサイクルを迅速かつ確実に繰り返すことができます。

成功したクラウド開発チームの中には、1日に何度もライブ環境にデプロイされているものがあります。 Azure チームは、2-3 か月ごとにメジャー更新プログラムをデプロイするために使用しましたが、現時点では、2-3 日ごとにマイナー更新プログラムをリリースし、2-3 週ごとにメジャーリリースをリリースしました。 このリズムを利用することで、お客様からのフィードバックに迅速に対応することができます。

そのためには、反復可能で信頼性が高く予測可能で、サイクル時間が短くなる開発および展開のサイクルを有効にする必要があります。

![DevOps ワークフロー](automate-everything/_static/image1.png)

つまり、機能についてのアイデアがあり、顧客がそれを使用してフィードバックを提供するまでの期間は、できるだけ短くする必要があります。 最初の3つのパターン (すべてを自動化、ソース管理、継続的な統合と配信) は、そのようなプロセスを可能にするために推奨されるベストプラクティスに関するものです。

## <a name="azure-management-scripts"></a>Azure の管理スクリプト

[この電子ブックの概要](introduction.md)では、web ベースのコンソールである Azure 管理ポータルについて説明しました。 管理ポータルでは、Azure にデプロイしたすべてのリソースを監視および管理できます。 Web アプリや Vm などのサービスを作成および削除したり、サービスを構成したり、サービス操作を監視したりするための簡単な方法です。 これは優れたツールですが、これを使用するのは手動のプロセスです。 任意のサイズの実稼働アプリケーションを開発する場合、特にチーム環境では、Azure を学習して調査し、繰り返し実行するプロセスを自動化するために、ポータル UI を使用することをお勧めします。

管理ポータルまたは Visual Studio で手動で実行できるほぼすべてのものは、REST 管理 API を呼び出すことによっても実行できます。 [Windows PowerShell](https://msdn.microsoft.com/library/windowsazure/jj156055.aspx)を使用してスクリプトを作成することも、 [Chef](http://www.opscode.com/chef/)や[パペット](http://puppetlabs.com/puppet/what-is-puppet)などのオープンソースフレームワークを使用することもできます。 また、Mac または Linux 環境で Bash コマンドラインツールを使用することもできます。 Azure では、これらのさまざまな環境に対して Api をスクリプト化しています。また、スクリプトではなくコードを記述する場合は、 [.net MANAGEMENT API](http://www.hanselman.com/blog/PennyPinchingInTheCloudAutomatingEverythingWithTheWindowsAzureManagementLibrariesAndNET.aspx)を用意しています。

この問題を修正するために、テスト環境を作成し、その環境にプロジェクトを配置するプロセスを自動化する Windows PowerShell スクリプトをいくつか作成しました。これらのスクリプトの内容をいくつか確認します。

## <a name="environment-creation-script"></a>環境作成スクリプト

まず、 *New-AzureWebsiteEnv*という名前を付けます。 テスト用に修正プログラムをデプロイできる Azure 環境が作成されます。 このスクリプトが実行する主なタスクは次のとおりです。

- Web アプリを作成します。
- ストレージ アカウントを作成します。 (後の章で説明するように、blob およびキューに対して必要です)。
- SQL Database サーバーと2つのデータベース (アプリケーションデータベースとメンバーシップデータベース) を作成します。
- ストレージアカウントとデータベースへのアクセスにアプリが使用する設定を Azure に格納します。
- デプロイを自動化するために使用される設定ファイルを作成します。

### <a name="run-the-script"></a>スクリプトを実行する

> [!NOTE]
> この章では、スクリプトと、それらを実行するために入力するコマンドの例を示します。 このデモでは、スクリプトを実行するために必要な知識をすべて提供するわけではありません。 詳しい手順については、「[付録: Fix It サンプルアプリケーション](the-fix-it-sample-application.md#deploybase)」を参照してください。

Azure サービスを管理する PowerShell スクリプトを実行するには、Azure PowerShell コンソールをインストールし、Azure サブスクリプションで動作するように構成する必要があります。 セットアップが完了したら、次のようなコマンドを使用して、Fix It environment 作成スクリプトを実行できます。

`.\New-AzureWebsiteEnv.ps1 -Name <websitename> -SqlDatabasePassword <password>`

`Name` パラメーターは、データベースとストレージアカウントを作成するときに使用する名前を指定し、`SqlDatabasePassword` パラメーターは SQL Database 用に作成される管理者アカウントのパスワードを指定します。 他にも使用できるパラメーターがあります。これについては後で説明します。

![PowerShell ウィンドウ](automate-everything/_static/image2.png)

スクリプトが終了すると、管理ポータルで作成された内容を確認できます。 2つのデータベースがあります。

![データベース](automate-everything/_static/image3.png)

ストレージアカウント:

![ストレージ アカウント](automate-everything/_static/image4.png)

と web アプリは次のようになります。

![[Web サイト]](automate-everything/_static/image5.png)

Web アプリの **[構成]** タブで、修正プログラムのアプリ用にストレージアカウントの設定と SQL database 接続文字列が設定されていることを確認できます。

![appSettings と connectionStrings](automate-everything/_static/image6.png)

*Automation*フォルダーには、 *&lt;websitename&gt;pubxml*ファイルも含まれるようになりました。 このファイルには、先ほど作成した Azure 環境にアプリケーションをデプロイするために MSBuild が使用する設定が格納されます。 例 :

[!code-xml[Main](automate-everything/samples/sample1.xml)]

ご覧のとおり、スクリプトは完全なテスト環境を作成し、プロセス全体は約90秒で完了しています。

チーム内の他のユーザーがテスト環境を作成しようとしている場合は、スクリプトを実行するだけで済みます。 高速であるだけでなく、使用している環境と同一の環境を使用していることも確信できます。 すべてのユーザーが管理ポータル UI を使用して手動で設定した場合は、自信を持っていなくても問題ありません。

### <a name="a-look-at-the-scripts"></a>スクリプトの概要

実際には、この作業を実行する3つのスクリプトがあります。 コマンドラインからを呼び出すと、他の2つのタスクが自動的に使用されます。

- *New-AzureWebSiteEnv*はメインスクリプトです。

    - *New-AzureStorage*によってストレージアカウントが作成されます。
    - *New-AzureSql*によってデータベースが作成されます。

### <a name="parameters-in-the-main-script"></a>メインスクリプトのパラメーター

メインスクリプト New-AzureWebSiteEnv では、次のいくつかのパラメーターが定義されて*い*ます。

[!code-powershell[Main](automate-everything/samples/sample2.ps1)]

2つのパラメーターが必要です。

- スクリプトによって作成される web アプリの名前。 (これは、URL: `<name>.azurewebsites.net`にも使用されます)。
- スクリプトによって作成されるデータベースサーバーの新しい管理ユーザーのパスワード。

省略可能なパラメーターを使用すると、データセンターの場所 (既定では "米国西部")、データベースサーバー管理者名 (既定では "dbuser")、およびデータベースサーバーのファイアウォール規則を指定できます。

### <a name="create-the-web-app"></a>Web アプリの作成

最初のスクリプトでは、`New-AzureWebsite` コマンドレットを呼び出して web アプリを作成し、web アプリ名と場所のパラメーター値を渡します。

[!code-powershell[Main](automate-everything/samples/sample3.ps1?highlight=2)]

### <a name="create-the-storage-account"></a>ストレージ アカウントの作成

次に、メインスクリプトは、ストレージアカウント名に " *&lt;websitename&gt;* storage" を指定し、web アプリと同じデータセンターの場所を指定して、 *New-AzureStorage*スクリプトを実行します。

[!code-powershell[Main](automate-everything/samples/sample4.ps1?highlight=3)]

*New-AzureStorage*は、`New-AzureStorageAccount` コマンドレットを呼び出してストレージアカウントを作成し、アカウント名とアクセスキーの値を返します。 ストレージアカウント内の blob とキューにアクセスするには、アプリケーションにこれらの値が必要になります。

[!code-powershell[Main](automate-everything/samples/sample5.ps1?highlight=2)]

常に新しいストレージアカウントを作成することはできません。必要に応じて既存のストレージアカウントを使用するように指示するパラメーターを追加することで、スクリプトを拡張できます。

### <a name="create-the-databases"></a>データベースを作成する

次に、既定のデータベースとファイアウォール規則の名前を設定した後、メインスクリプトによってデータベース作成スクリプト*New-AzureSql*が実行されます。

[!code-powershell[Main](automate-everything/samples/sample6.ps1)]

[!code-powershell[Main](automate-everything/samples/sample7.ps1?highlight=2)]

データベース作成スクリプトでは、開発用コンピューターの IP アドレスを取得し、ファイアウォール規則を設定して、開発用コンピューターがサーバーに接続して管理できるようにします。 次に、データベースの作成スクリプトでは、データベースを設定するためのいくつかの手順を実行します。

- `New-AzureSqlDatabaseServer` コマンドレットを使用してサーバーを作成します。

    [!code-powershell[Main](automate-everything/samples/sample8.ps1?highlight=1)]
- 開発用コンピューターがサーバーを管理し、web アプリがそれに接続できるようにするためのファイアウォール規則を作成します。 

    [!code-powershell[Main](automate-everything/samples/sample9.ps1?highlight=3,5)]
- `New-AzureSqlDatabaseServerContext` コマンドレットを使用して、サーバー名と資格情報を含むデータベースコンテキストを作成します。

    [!code-powershell[Main](automate-everything/samples/sample10.ps1?highlight=4)]

    `New-PSCredentialFromPlainText` は、`ConvertTo-SecureString` コマンドレットを呼び出してパスワードを暗号化し、`Get-Credential` コマンドレットが返すのと同じ型である `PSCredential` オブジェクトを返す、スクリプト内の関数です。
- `New-AzureSqlDatabase` コマンドレットを使用して、アプリケーションデータベースとメンバーシップデータベースを作成します。

    [!code-powershell[Main](automate-everything/samples/sample11.ps1?highlight=2,5)]
- ローカルに定義された関数を呼び出して、各データベースの接続文字列を作成します。 アプリケーションは、これらの接続文字列を使用してデータベースにアクセスします。 

    [!code-powershell[Main](automate-everything/samples/sample12.ps1?highlight=1-2)]

    SQLAzureDatabaseConnectionString は、指定されたパラメーター値から接続文字列を作成するスクリプトで定義された関数です。

    [!code-powershell[Main](automate-everything/samples/sample13.ps1?highlight=1)]
- データベースサーバー名と接続文字列を含むハッシュテーブルを返します。

    [!code-powershell[Main](automate-everything/samples/sample14.ps1)]

Fix It アプリでは、個別のメンバーシップとアプリケーションデータベースを使用します。 メンバーシップとアプリケーションの両方のデータを1つのデータベースに格納することもできます。

### <a name="store-app-settings-and-connection-strings"></a>アプリの設定と接続文字列を保存する

Azure には、設定と接続文字列を格納する機能があります。この機能を使用すると、Web.config ファイルで `appSettings` または `connectionStrings` コレクションを読み取ろうとしたときに、アプリケーションに返される内容を自動的に上書きすることができます。 これは、の配置時に web.config[変換](../../../../web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations.md)を適用する代わりに使用します。 詳細については、この電子ブックの「[機微なデータを Azure に保存](source-control.md#appsettings)する」を参照してください。

環境作成スクリプトは、azure で実行するときに、アプリケーションがストレージアカウントとデータベースにアクセスするために必要なすべての `appSettings` と `connectionStrings` の値を Azure に格納します。

[!code-powershell[Main](automate-everything/samples/sample15.ps1)]

[!code-powershell[Main](automate-everything/samples/sample16.ps1)]

[!code-powershell[Main](automate-everything/samples/sample17.ps1?highlight=2)]

[新しい聖箱](http://newrelic.com/)は、[監視とテレメトリ](monitoring-and-telemetry.md)の章で説明しているテレメトリフレームワークです。 また、環境作成スクリプトによって web アプリが再起動され、新しい聖なる値が確実に取得されるようになります。

[!code-powershell[Main](automate-everything/samples/sample18.ps1?highlight=2)]

### <a name="preparing-for-deployment"></a>展開の準備

プロセスの最後に、環境作成スクリプトは2つの関数を呼び出して、配置スクリプトで使用されるファイルを作成します。

これらの関数のいずれかによって、発行プロファイル *(&lt;websitename&gt;pubxml*ファイル) が作成されます。 このコードは、Azure REST API を呼び出して発行設定を取得し、情報を *.publishsettings*ファイルに保存します。 次に、そのファイルの情報をテンプレートファイル (*pubxml. template*) と共に使用して、発行プロファイルを含む*pubxml*ファイルを作成します。 この2段階のプロセスでは、Visual Studio での作業をシミュレートします。 *.publishsettings*ファイルをダウンロードし、それをインポートして発行プロファイルを作成します。

もう1つの関数は、別のテンプレートファイル (website-environment) を使用して、配置スクリプトが*pubxml*ファイルと共に使用する設定を含むファイルを作成します。

### <a name="troubleshooting-and-error-handling"></a>トラブルシューティングとエラー処理

スクリプトはプログラムに似ています。エラーが発生する可能性があり、エラーの原因と原因を把握したい場合があります。 このため、環境作成スクリプトは、すべての詳細メッセージが表示されるように、`VerbosePreference` 変数の値を `SilentlyContinue` から `Continue` に変更します。 また、`ErrorActionPreference` 変数の値を `Continue` から `Stop`に変更し、終了しないエラーが発生した場合でもスクリプトが停止するようにします。

[!code-powershell[Main](automate-everything/samples/sample19.ps1)]

作業を行う前に、スクリプトは開始時刻を格納して、完了した経過時間を計算できるようにします。

[!code-powershell[Main](automate-everything/samples/sample20.ps1)]

処理が完了すると、スクリプトによって経過時間が表示されます。

[!code-powershell[Main](automate-everything/samples/sample21.ps1)]

また、すべてのキー操作について、スクリプトは詳細なメッセージを書き込みます。次に例を示します。

[!code-powershell[Main](automate-everything/samples/sample22.ps1)]

## <a name="deployment-script"></a>デプロイ スクリプト

*New-AzureWebsiteEnv*スクリプトは、環境の作成に使用されます。 *Publish-AzureWebsite*スクリプトは、アプリケーションの展開に使用します。

デプロイスクリプトは、環境作成スクリプトによって作成された*website-environment*ファイルから web アプリの名前を取得します。

[!code-powershell[Main](automate-everything/samples/sample23.ps1)]

次のように、 *.publishsettings*ファイルからデプロイユーザーのパスワードを取得します。

[!code-powershell[Main](automate-everything/samples/sample24.ps1)]

プロジェクトをビルドして配置する[MSBuild](http://msbuildbook.com/)コマンドを実行します。

[!code-powershell[Main](automate-everything/samples/sample25.ps1)]

また、コマンドラインで `Launch` パラメーターを指定した場合は、`Show-AzureWebsite` コマンドレットを呼び出して、web サイトの URL に既定のブラウザーを開きます。

[!code-powershell[Main](automate-everything/samples/sample26.ps1?highlight=3)]

デプロイスクリプトは、次のようなコマンドを使用して実行できます。

`.\Publish-AzureWebsite.ps1 ..\MyFixIt\MyFixIt.csproj -Launch`

この処理が完了すると、クラウドで実行されているサイトと共に、`<websitename>.azurewebsites.net` の URL でブラウザーが開きます。

![Windows Azure に展開された It アプリの修正](automate-everything/_static/image7.png)

## <a name="summary"></a>要約

これらのスクリプトを使用すると、同じ手順が常に同じ順序で同じオプションを使用して実行されることを保証できます。 これにより、チームの各開発者は、他のチームメンバーの環境や運用環境では実際には同じように動作しない、自分のコンピューターに独自の作業をしたり、何かを行ったりしないようにすることができます。

同様の方法で、管理ポータルで実行できるほとんどの Azure 管理機能を自動化できます。そのためには、REST API、Windows PowerShell スクリプト、.NET 言語 API、または Linux または Mac で実行できる Bash ユーティリティを使用します。

次の[章](source-control.md)では、ソースコードを見て、ソースコードリポジトリにスクリプトを含めることが重要な理由を説明します。

## <a name="resources"></a>リソース

- [Windows PowerShell For Azure をインストールして構成](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-4.3.1)します。 Azure PowerShell コマンドレットをインストールする方法と、Azure アカウントを管理するために必要な証明書をコンピューターにインストールする方法について説明します。 これは、PowerShell 自体を学習するためのリソースへのリンクも用意されているため、開始するのに最適な場所です。
- [Azure スクリプトセンター](https://docs.microsoft.com/azure/automation/automation-runbook-gallery)。 Azure サービスを管理するスクリプトを開発するためのリソースへの WindowsAzure.com ポータル、入門チュートリアルへのリンク、コマンドレットリファレンスドキュメントとソースコード、およびサンプルスクリプト
- [週末 Scripter: はじめに Azure と PowerShell を使用](https://blogs.technet.com/b/heyscriptingguy/archive/2013/06/22/weekend-scripter-getting-started-with-windows-azure-and-powershell.aspx)します。 この記事では、Windows PowerShell 専用のブログで、Azure の管理機能に PowerShell を使用する方法について詳しく説明します。
- [Azure クロスプラットフォームコマンドラインインターフェイスをインストールして構成](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest)します。 Mac、Linux、および Windows システムで動作する Azure scripting framework の入門チュートリアルです。
- 「 [Azure sdk とツールのダウンロード」の「コマンドラインツール」セクション](https://azure.microsoft.com/downloads/)。 Azure のコマンドラインツールに関連するドキュメントおよびダウンロードのポータルページです。
- [Azure 管理ライブラリと .NET を使用してすべてを自動化](http://www.hanselman.com/blog/PennyPinchingInTheCloudAutomatingEverythingWithTheWindowsAzureManagementLibrariesAndNET.aspx)。 Scott マン Selman は、Azure 用の .NET management API を紹介しています。
- [Windows PowerShell スクリプトを使用した開発環境およびテスト環境の発行](https://msdn.microsoft.com/library/azure/dn642480.aspx)。 Visual Studio によって web プロジェクトに自動的に生成される発行スクリプトの使用方法について説明する MSDN ドキュメントです。
- [PowerShell Tools for Visual Studio 2013](https://visualstudiogallery.msdn.microsoft.com/c9eb3ba8-0c59-4944-9a62-6eee37294597)。 Visual studio で Windows PowerShell の言語サポートを追加する visual Studio 拡張機能。

> [!div class="step-by-step"]
> [前へ](introduction.md)
> [次へ](source-control.md)
