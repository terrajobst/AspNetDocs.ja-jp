---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/running-windows-powershell-scripts-from-msbuild-project-files
title: MSBuild プロジェクトファイルから Windows PowerShell スクリプトを実行する |Microsoft Docs
author: jrjlee
description: このトピックでは、ビルドおよび配置のプロセスの一部として Windows PowerShell スクリプトを実行する方法について説明します。 スクリプトはローカルで実行できます (つまり、b...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 55f1ae45-fcb5-43a9-8415-fa5b935fc9c9
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/running-windows-powershell-scripts-from-msbuild-project-files
msc.type: authoredcontent
ms.openlocfilehash: 7b09c07b8b7c2a61ca534f7a66a929593f3d04ca
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78441448"
---
# <a name="running-windows-powershell-scripts-from-msbuild-project-files"></a>MSBuild プロジェクト ファイルから Windows PowerShell スクリプトを実行する

[Jason Lee](https://github.com/jrjlee)

[[Download PDF]\(PDF をダウンロード\)](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> このトピックでは、ビルドおよび配置のプロセスの一部として Windows PowerShell スクリプトを実行する方法について説明します。 スクリプトは、移行先の web サーバーやデータベースサーバーなど、ローカルで (つまり、ビルドサーバー上で) 実行することも、リモートで実行することもできます。
> 
> 配置後の Windows PowerShell スクリプトを実行する理由は多数あります。 たとえば、次の場合です。
> 
> - カスタムイベントソースをレジストリに追加します。
> - アップロード用のファイルシステムディレクトリを生成します。
> - ビルドディレクトリをクリーンアップします。
> - カスタムログファイルにエントリを書き込みます。
> - 新しくプロビジョニングされた web アプリケーションにユーザーを招待する電子メールを送信します。
> - 適切なアクセス許可を持つユーザーアカウントを作成します。
> - SQL Server インスタンス間のレプリケーションを構成します。
> 
> このトピックでは、Microsoft Build Engine (MSBuild) プロジェクトファイルのカスタムターゲットから Windows PowerShell スクリプトをローカルとリモートの両方で実行する方法について説明します。

このトピックでは、Fabrikam, Inc. という架空の企業のエンタープライズ展開要件に基づいて、一連のチュートリアルの一部を説明します。このチュートリアルシリーズでは、&#x2014; [Contact Manager ソリューション](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;のサンプルソリューションを使用して、ASP.NET MVC 3 アプリケーション、Windows Communication Foundation (WCF) サービス、データベースプロジェクトなど、現実的なレベルの複雑さを持つ web アプリケーションを表します。

これらのチュートリアルの中核となる配置方法は、「[プロジェクトファイルについ](../web-deployment-in-the-enterprise/understanding-the-project-file.md)て」で説明されている分割プロジェクトファイルアプローチに基づいています。この&#x2014;プロジェクトファイルには、ビルドプロセスは、すべての変換先環境に適用されるビルド命令を含む2つのプロジェクトファイルと、環境固有のビルドおよび配置設定を含んでいます。 ビルド時に、環境固有のプロジェクトファイルが環境に依存しないプロジェクトファイルにマージされ、ビルド命令の完全なセットが形成されます。

## <a name="task-overview"></a>タスクの概要

自動またはシングルステップのデプロイプロセスの一環として Windows PowerShell スクリプトを実行するには、次の高レベルのタスクを実行する必要があります。

- Windows PowerShell スクリプトをソリューションとソース管理に追加します。
- Windows PowerShell スクリプトを呼び出すコマンドを作成します。
- コマンドで予約済みの XML 文字をエスケープします。
- カスタム MSBuild プロジェクトファイルにターゲットを作成し、 **Exec**タスクを使用してコマンドを実行します。

このトピックでは、これらの手順を実行する方法について説明します。 このトピックのタスクとチュートリアルでは、MSBuild のターゲットとプロパティについて理解していること、およびカスタム MSBuild プロジェクトファイルを使用してビルドおよび配置プロセスを実行する方法について理解していることを前提としています。 詳細については、「[プロジェクトファイルに](../web-deployment-in-the-enterprise/understanding-the-project-file.md)ついて」および「[ビルドプロセスについ](../web-deployment-in-the-enterprise/understanding-the-build-process.md)て」を参照してください。

## <a name="creating-and-adding-windows-powershell-scripts"></a>Windows PowerShell スクリプトの作成と追加

このトピックのタスクでは、「 **Logdeploy. ps1** 」という名前のサンプル Windows PowerShell スクリプトを使用して、MSBuild からスクリプトを実行する方法を説明します。 **Logdeploy. ps1**スクリプトには、1行のエントリをログファイルに書き込む単純な関数が含まれています。

[!code-powershell[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample1.ps1)]

**Logdeploy. ps1**スクリプトは2つのパラメーターを受け取ります。 最初のパラメーターは、エントリを追加するログファイルへの完全パスを表し、2番目のパラメーターは、ログファイルに記録する配置先を表します。 スクリプトを実行すると、次の形式でログファイルに行が追加されます。

[!code-html[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample2.html)]

MSBuild で**Logdeploy. ps1**スクリプトを使用できるようにするには、次のことを行う必要があります。

- スクリプトをソース管理に追加します。
- Visual Studio 2010 で、スクリプトをソリューションに追加します。

ビルドサーバーとリモートコンピューターのどちらでスクリプトを実行するかに関係なく、スクリプトをソリューションコンテンツと共に配置する必要はありません。 1つの方法として、スクリプトをソリューションフォルダーに追加します。 Contact Manager の例では、デプロイプロセスの一部として Windows PowerShell スクリプトを使用する必要があるため、[ソリューションの発行] フォルダーにスクリプトを追加するのが理にかなっています。

![](running-windows-powershell-scripts-from-msbuild-project-files/_static/image1.png)

ソリューションフォルダーの内容がソース資料としてビルドサーバーにコピーされます。 ただし、これらはプロジェクトの出力の一部を形成しません。

## <a name="executing-a-windows-powershell-script-on-the-build-server"></a>ビルドサーバーで Windows PowerShell スクリプトを実行する

場合によっては、プロジェクトをビルドするコンピューターで Windows PowerShell スクリプトを実行することが必要になることがあります。 たとえば、Windows PowerShell スクリプトを使用して、ビルドフォルダーのクリーンアップやカスタムログファイルへのエントリの書き込みを行うことができます。

構文に関しては、MSBuild プロジェクトファイルから Windows PowerShell スクリプトを実行することは、通常のコマンドプロンプトから Windows PowerShell スクリプトを実行することと同じです。 Powershell 実行可能ファイルを起動し、 **– command**スイッチを使用して、Windows powershell で実行するコマンドを指定する必要があります。 (Windows PowerShell v2 では、 **– file**スイッチを使用することもできます)。 コマンドの形式は次のようになります。

[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample3.cmd)]

次に例を示します。

[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample4.cmd)]

スクリプトへのパスにスペースが含まれている場合は、アンパサンドで始まる単一引用符でファイルパスを囲む必要があります。 二重引用符は使用できません。コマンドを囲むために既に使用されているためです。

[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample5.cmd)]

MSBuild からこのコマンドを呼び出す際には、いくつかの追加の考慮事項があります。 最初に、スクリプトが自動的に実行されるように、 **–非対話**フラグを含める必要があります。 次に、適切な引数値を使用して **– set-executionpolicy**フラグを含める必要があります。 これにより、Windows PowerShell がスクリプトに適用する実行ポリシーが指定され、既定の実行ポリシーをオーバーライドできるようになります。これにより、スクリプトの実行が妨げられる可能性があります。 次の引数の値から選択できます。

- 値を**無制限**に設定すると、スクリプトが署名されているかどうかに関係なく、Windows PowerShell でスクリプトを実行できます。
- **RemoteSigned**の値を指定すると、Windows PowerShell はローカルコンピューター上で作成された未署名のスクリプトを実行できます。 ただし、他の場所で作成されたスクリプトには署名が必要です。 (実際には、ビルドサーバーで Windows PowerShell スクリプトをローカルに作成することはほとんどありません)。
- **AllSigned**の値を指定すると、Windows PowerShell は署名されたスクリプトのみを実行できます。

既定の実行ポリシーは**制限**されています。これにより、Windows PowerShell はスクリプトファイルを実行できなくなります。

最後に、Windows PowerShell コマンドで発生した予約済み XML 文字をエスケープする必要があります。

- 単一引用符を **&amp;apos;** に置き換える
- 二重引用符を **&amp;quot; に置き換えます。**
- アンパサンドを **&amp;amp; に置き換えます。**

- これらの変更を行うと、コマンドは次のようになります。

[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample6.cmd)]

カスタム MSBuild プロジェクトファイル内で、新しいターゲットを作成し、 **Exec**タスクを使用して次のコマンドを実行できます。

[!code-xml[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample7.xml)]

この例では、次の点に注意してください。

- パラメーター値や Windows PowerShell 実行可能ファイルの場所など、すべての変数は MSBuild プロパティとして宣言されます。
- ユーザーがコマンドラインからこれらの値をオーバーライドできるようにするための条件が含まれています。
- **Msdeploycomputername**プロパティは、プロジェクトファイル内の他の場所で宣言されています。

このターゲットをビルドプロセスの一部として実行すると、Windows PowerShell によってコマンドが実行され、指定したファイルにログエントリが書き込まれます。

## <a name="executing-a-windows-powershell-script-on-a-remote-computer"></a>リモートコンピューターでの Windows PowerShell スクリプトの実行

Windows PowerShell は、 [Windows リモート管理](https://msdn.microsoft.com/library/windows/desktop/aa384426.aspx)(WinRM) を介してリモートコンピューターでスクリプトを実行することができます。 これを行うには、[コマンド](https://technet.microsoft.com/library/dd347578.aspx)レットを使用する必要があります。 これにより、スクリプトをリモートコンピューターにコピーせずに、1つまたは複数のリモートコンピューターに対してスクリプトを実行できます。 スクリプトを実行したローカルコンピューターに結果が返されます。

> [!NOTE]
> **コマンド**レットを使用してリモートコンピューターで Windows PowerShell スクリプトを実行する前に、リモートメッセージを受け入れるように WinRM リスナーを構成する必要があります。 これを行うには、リモートコンピューターでコマンド**winrm quickconfig**を実行します。 詳細については、「 [Windows リモート管理のインストールと構成](https://msdn.microsoft.com/library/windows/desktop/aa384372(v=vs.85).aspx)」を参照してください。

Windows PowerShell ウィンドウから、次の構文を使用してリモートコンピューターで**Logdeploy. ps1**スクリプトを実行します。

[!code-powershell[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample8.ps1)]

> [!NOTE]
> **呼び出しコマンド**を使用してスクリプトファイルを実行するには、他にもさまざまな方法がありますが、この方法は、パラメーター値を指定し、パスをスペースで管理する必要がある場合に最も簡単です。

これをコマンドプロンプトから実行する場合は、Windows PowerShell 実行可能ファイルを起動し、 **– command**パラメーターを使用して指示を行う必要があります。

[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample9.cmd)]

前と同様に、MSBuild からコマンドを実行するときに、いくつかの追加のスイッチを指定し、予約済みの XML 文字をエスケープする必要があります。

[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample10.cmd)]

最後に、前と同様に、カスタム MSBuild ターゲット内で**Exec**タスクを使用してコマンドを実行できます。

[!code-xml[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample11.xml)]

このターゲットをビルドプロセスの一部として実行すると、Windows PowerShell は、 **– computername**引数で指定したコンピューター上でスクリプトを実行します。

## <a name="conclusion"></a>まとめ

このトピックでは、MSBuild プロジェクトファイルから Windows PowerShell スクリプトを実行する方法について説明します。 この方法を使用すると、自動または単一ステップのビルドおよび展開プロセスの一部として、ローカルまたはリモートコンピューターで Windows PowerShell スクリプトを実行できます。

## <a name="further-reading"></a>参考資料

Windows PowerShell スクリプトへの署名と実行ポリシーの管理に関するガイダンスについては、「 [Windows Powershell スクリプトの実行](https://technet.microsoft.com/library/ee176949.aspx)」を参照してください。 リモートコンピューターからの Windows PowerShell コマンドの実行に関するガイダンスについては、「[リモートコマンドの実行](https://technet.microsoft.com/library/dd819505.aspx)」を参照してください。

カスタム MSBuild プロジェクトファイルを使用した配置プロセスの制御の詳細については、「[プロジェクトファイルについ](../web-deployment-in-the-enterprise/understanding-the-project-file.md)て」および「[ビルドプロセスについ](../web-deployment-in-the-enterprise/understanding-the-build-process.md)て」を参照してください。

> [!div class="step-by-step"]
> [前へ](taking-web-applications-offline-with-web-deploy.md)
> [次へ](troubleshooting-the-packaging-process.md)
