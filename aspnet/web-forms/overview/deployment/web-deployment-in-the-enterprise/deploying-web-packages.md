---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/deploying-web-packages
title: Web パッケージの配置 |Microsoft Docs
author: jrjlee
description: このトピックでは、インターネットインフォメーションサービス (IIS) Web 配置ツール ([Web...] を使用して、web 配置パッケージをリモートサーバーに発行する方法について説明します。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: a5c5eed2-8683-40a5-a2e1-35c9f8d17c29
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/deploying-web-packages
msc.type: authoredcontent
ms.openlocfilehash: 91b99e6e250342851aea6860164b6f6af54818d1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78464968"
---
# <a name="deploying-web-packages"></a>Web パッケージを配置する

[Jason Lee](https://github.com/jrjlee)

[[Download PDF]\(PDF をダウンロード\)](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> このトピックでは、インターネットインフォメーションサービス (IIS) Web 配置ツール (Web 配置) 2.0 を使用して、web 配置パッケージをリモートサーバーに発行する方法について説明します。
> 
> Web パッケージをリモートサーバーに配置するには、主に次の2つの方法があります。
> 
> - Msdeploy.exe コマンドラインユーティリティは直接使用できます。
> - ビルドプロセスによって生成される *[project name]. .deploy*ファイルを実行できます。
> 
> 使用する方法に関係なく、最終的な結果は同じになります。 基本的に、すべての *.deploy*ファイルは、指定された値を使用して msdeploy.exe を実行します。これにより、パッケージを配置するために必要な情報を提供する必要がなくなります。 これにより、デプロイプロセスが簡略化されます。 一方、Msdeploy.exe を直接使用すると、パッケージの配置方法よりもはるかに柔軟になります。
> 
> どの方法を使用するかは、展開プロセスで必要とされる制御量や、Web 配置リモートエージェントサービスと Web 配置ハンドラーのどちらを対象としているかなど、さまざまな要因によって異なります。 このトピックでは、各方法の使用方法と、それぞれの方法が適切であることを確認する方法について説明します。
> 
> このトピックのタスクとチュートリアルでは、次のことを前提としています。
> 
> - 「 [Web アプリケーションプロジェクトのビルドとパッケージ化](building-and-packaging-web-application-projects.md)」で説明されているように、web アプリケーションをビルドしてパッケージ化しました。
> - 「 [Web パッケージ配置のパラメーターの構成](configuring-parameters-for-web-package-deployment.md)」で説明されているように、ターゲット環境に適切なパラメーター値を指定するように*setparameters .xml*ファイルを変更しました。

Web パッケージを配置する最も簡単な方法は、[*project name*] *. .deploy*ファイルを実行することです。 特に、 *.deploy*ファイルを使用すると、msdeploy.exe を直接使用するよりも、次のような利点があります。

- Web 配置パッケージ&#x2014;の場所を指定する必要はありません。 *.deploy*ファイルは、どこにあるかを既に認識しています。
- *Setparameters .xml*ファイル&#x2014;の場所を指定する必要はありません。 *.cmd*ファイルは、その場所を既に認識しています。
- ソースとターゲットの Msdeploy.exe プロバイダー&#x2014;を指定する必要はありません。 *.deploy*ファイルは、使用する値を既に認識しています。
- Msdeploy.exe 操作の設定&#x2014;を指定する必要はありません *。 .deploy*ファイルによって、通常必要な値が msdeploy.exe コマンドに自動的に追加されます。

*.Deploy*ファイルを使用して web パッケージを展開する前に、次のことを確認する必要があります。

- *.Deploy*ファイル ([*プロジェクト名*])。*Setparameters .xml*ファイルと web パッケージ ([*プロジェクト名*])。*zip*) は同じフォルダー内にあります。
- Web 配置 (Msdeploy.exe) は、 *.deploy*ファイルを実行するコンピューターにインストールされます。

*.Deploy*ファイルは、さまざまなコマンドラインオプションをサポートしています。 コマンドプロンプトからファイルを実行すると、基本的な構文は次のようになります。

[!code-console[Main](deploying-web-packages/samples/sample1.cmd)]

試用版の実行とライブデプロイのどちらを実行するかを指定するには、 **/t**フラグまたは **/y**フラグを指定する必要があります (同じコマンドで両方のフラグを使用しないでください)。 次の表では、これらのフラグの用途について説明します。

| フラグ | Description |
| --- | --- |
| **/T** | 評価版の実行を示す **– whatif**フラグを指定して msdeploy.exe を呼び出します。 パッケージを配置するのではなく、パッケージを配置した場合に何が起こるかのレポートを作成します。 |
| **/Y** | **– Whatif**フラグを指定せずに msdeploy.exe を呼び出します。 これにより、パッケージがローカルコンピューターまたは指定した移行先サーバーに配置されます。 |
| **/M** | 移行先サーバーの名前またはサービスの URL を指定します。 ここで指定できる値の詳細については、このトピックの「**エンドポイントに関する考慮事項**」セクションを参照してください。 **/M**フラグを省略した場合、パッケージはローカルコンピューターに配置されます。 |
| **/A** | Msdeploy.exe が展開を実行するために使用する認証の種類を指定します。 指定できる値は、 **NTLM**と**Basic**です。 **/A**フラグを省略した場合、認証の種類は、Web 配置リモートエージェントサービスに配置する場合は**NTLM** 、Web 配置ハンドラーに配置する場合は **[基本]** に設定されます。 |
| **/U** | ユーザー名を指定します。 これは、基本認証を使用している場合にのみ適用されます。 |
| **/P** | パスワードを指定します。 これは、基本認証を使用している場合にのみ適用されます。 |
| **/L** | パッケージをローカル IIS Express インスタンスに配置する必要があることを示します。 |
| **/G** | [Tempagent プロバイダー設定](https://technet.microsoft.com/library/ee517345(WS.10).aspx)を使用してパッケージを配置することを指定します。 **/G**フラグを省略した場合、値は既定で**false**に設定されます。 |

> [!NOTE]
> ビルドプロセスによって web パッケージが作成されるたびに、これらの配置オプションについて説明する *[project name] deploy-readme*という名前のファイルも作成されます。

これらのフラグに加えて、Web 配置操作設定を追加*の .deploy*パラメーターとして指定できます。 指定した追加の設定は、単に基になる Msdeploy.exe コマンドに渡されます。 これらの設定の詳細については、「 [Web 配置操作の設定](https://technet.microsoft.com/library/dd569089(WS.10).aspx)」を参照してください。

たとえば、 *.deploy*ファイルを実行して、Contactmanager Mvc web アプリケーションプロジェクトをテスト環境に配置するとします。 テスト環境は Web 配置リモートエージェントサービスを使用するように構成されています。詳細については、「 [Configure The Web Server for Web 配置 Publishing (リモートエージェント)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)」を参照してください。 Web アプリケーションをデプロイするには、次の手順を完了する必要があります。

**.Deploy ファイルを使用して web アプリケーションを配置するには**

1. 「 [Web アプリケーションプロジェクトのビルドおよびパッケージ化](building-and-packaging-web-application-projects.md)」で説明されているように、web アプリケーションプロジェクトをビルドしてパッケージ化します。
2. 「 [Web パッケージ配置のパラメーターの構成](configuring-parameters-for-web-package-deployment.md)」で説明されているように、テスト環境の正しいパラメーター値を含むように*Contactmanager. Mvc. setparameters .xml*ファイルを変更します。
3. コマンドプロンプトウィンドウを開き、 *Contactmanager. Mvc. .deploy*ファイルの場所に移動します。
4. 次のコマンドを入力し、enter キーを押します。

    [!code-console[Main](deploying-web-packages/samples/sample2.cmd)]

次の点に注意してください。

- **/Y**フラグは、評価版を実行するのではなく、実際にパッケージを展開することを示します。
- **/M**フラグは、TESTWEB1 という名前のサーバーにパッケージを配置することを示します。 この値から、Msdeploy.exe は http://TESTWEB1/MSDeployAgentServiceで Web 配置リモートエージェントサービスにパッケージを配置しようとします。
- **/A**フラグは、NTLM 認証を使用することを示します。 そのため、ユーザー名とパスワードを指定する必要はありません。

*.Deploy*ファイルを使用してデプロイプロセスを簡略化する方法を説明するために、上記のオプションを使用して*contactmanager*を実行するときに生成されて実行される msdeploy.exe コマンドを見てみましょう。

[!code-console[Main](deploying-web-packages/samples/sample3.cmd)]

*.Deploy ファイルを*使用した web パッケージの配置の詳細については、「[方法: .Deploy ファイルを使用して配置パッケージをインストール](https://msdn.microsoft.com/library/ff356104.aspx)する」を参照してください。

## <a name="using-msdeployexe"></a>Msdeploy.exe の使用

通常、 *.deploy*ファイルを使用すると展開プロセスが単純化されますが、msdeploy.exe を直接使用する方が好ましい場合もあります。 次に例を示します。

- Web 配置ハンドラーに管理者以外のユーザーとして展開する場合は、 *.deploy*ファイルを使用できません。 これは、「**エンドポイントの考慮事項**」で説明されているように Web 配置2.0 のバグが原因です。
- 異なる場所にある異なる*Setparameters .xml*ファイルを手動で切り替える場合は、msdeploy.exe を直接使用することをお勧めします。
- Msdeploy.exe のコマンドライン引数をいくつかオーバーライドする場合は、Msdeploy.exe を直接使用することをお勧めします。

Msdeploy.exe を使用する場合は、次の3つの重要な情報を提供する必要があります。

- データの取得元の場所を示す **-source**パラメーター。
- データの移動先を示す **– dest**パラメーター。
- 実行する[操作](https://technet.microsoft.com/library/dd568989(WS.10).aspx)を示す **–動詞**パラメーター。

Msdeploy.exe は、 [Web 配置プロバイダー](https://technet.microsoft.com/library/dd569040(WS.10).aspx)に依存して、ソースとターゲットのデータを処理します。 Web 配置には、使用できる&#x2014;アプリケーションとデータソースの範囲を表すプロバイダーが多数用意されています。たとえば、SQL Server データベース、IIS web サーバー、証明書、グローバルアセンブリキャッシュ (GAC) アセンブリ、さまざまな構成ファイル、その他多くの種類のデータのプロバイダーがあります。 – **Source**パラメーターと **– dest**パラメーターの両方で、 **-source**: [*providerName*] = [*location*] の形式でプロバイダーを指定する必要があります。 IIS web サイトに web パッケージを配置する場合は、次の値を使用する必要があります。

- **– Source**プロバイダーは常に[パッケージ](https://technet.microsoft.com/library/dd569019(WS.10).aspx)です。 次に例を示します。

    [!code-console[Main](deploying-web-packages/samples/sample4.cmd)]
- **– Dest**プロバイダーは常に[auto](https://technet.microsoft.com/library/dd569016(WS.10).aspx)です。例えば：

    [!code-console[Main](deploying-web-packages/samples/sample5.cmd)]
- **–動詞**は常に**同期**されます。

    [!code-console[Main](deploying-web-packages/samples/sample6.cmd)]

さらに、その他の[プロバイダー固有の設定](https://technet.microsoft.com/library/dd569001(WS.10).aspx)と一般的な[操作の設定](https://technet.microsoft.com/library/dd569089(WS.10).aspx)を指定する必要があります。 たとえば、ContactManager の Mvc web アプリケーションをステージング環境にデプロイするとします。 この配置は、Web 配置ハンドラーを対象とし、基本認証を使用する必要があります。 Web アプリケーションをデプロイするには、次の手順を完了する必要があります。

**Msdeploy.exe を使用して web アプリケーションを展開するには**

1. 「 [Web アプリケーションプロジェクトのビルドおよびパッケージ化](building-and-packaging-web-application-projects.md)」で説明されているように、web アプリケーションプロジェクトをビルドしてパッケージ化します。
2. 「 [Web パッケージ配置のパラメーターの構成](configuring-parameters-for-web-package-deployment.md)」で説明されているように、ステージング環境の正しいパラメーター値が含まれるように*Contactmanager. Mvc パラメーター .xml*ファイルを変更します。
3. コマンドプロンプトウィンドウを開き、Msdeploy.exe の場所を参照します。 これは通常、%PROGRAMFILES%\IIS\Microsoft Web 配置 V2\msdeploy.exe. にあります。
4. 次のコマンドを入力し、enter キーを押します (改行は無視します)。

    [!code-console[Main](deploying-web-packages/samples/sample7.cmd)]

次の点に注意してください。

- **– Source**パラメーターは**パッケージ**プロバイダーを指定し、web パッケージの場所を示します。
- **– Dest**パラメーターは、**自動**プロバイダーを指定します。 **ComputerName**設定は、移行先サーバーの Web 配置ハンドラーのサービス URL を提供します。 **[Authtype]** 設定は基本認証を使用することを示します。そのため、**ユーザー名**と**パスワード**を入力する必要があります。 最後に、 **Includeacls = "False"** の設定は、ソース web アプリケーション内のファイルのアクセス制御リスト (acl) を移行先サーバーにコピーしないことを示します。
- **– Verb: sync**引数は、移行先サーバーでソースコンテンツをレプリケートすることを示します。
- **– Disablelink**引数は、アプリケーションプール、仮想ディレクトリ構成、または SECURE SOCKETS LAYER (SSL) 証明書を移行先サーバーにレプリケートしないことを示します。 詳細については、「 [Web 配置リンク拡張機能](https://technet.microsoft.com/library/dd569028(WS.10).aspx)」を参照してください。
- **– Setparamfile**パラメーターは、 *setparameters .xml*ファイルの場所を提供します。
- **– Allowuntrusted**スイッチは、信頼された証明機関によって発行されていない SSL 証明書を Web 配置が受け入れる必要があることを示します。 Web 配置ハンドラーにデプロイしていて、自己署名証明書を使用してサービス URL を保護している場合は、このスイッチを含める必要があります。

## <a name="automating-web-package-deployment"></a>Web パッケージの配置の自動化

多くのエンタープライズシナリオでは、大規模なシングルステップまたは自動化されたデプロイの一部として、web パッケージをデプロイする必要があります。 *.Deploy*ファイルを実行して、または msdeploy.exe を直接使用して、web パッケージを配置するかどうかに関係なく、コマンドをパラメーター化して、Microsoft Build Engine (MSBuild) プロジェクトファイルのターゲットから呼び出すことができます。

Contact Manager サンプルソリューションで、 *Publish*ファイル内の**publishwebpackages**ターゲットを確認します。 このターゲットは、 **Publishpackages**という名前の項目リストによって識別される *.deploy*ファイルごとに1回実行されます。 ターゲットは、プロパティと項目メタデータを使用して、各 *.deploy*ファイルの引数値の完全なセットを作成してから、 **Exec**タスクを使用してコマンドを実行します。

[!code-xml[Main](deploying-web-packages/samples/sample8.xml)]

> [!NOTE]
> サンプルソリューションのプロジェクトファイルモデルの概要と、一般的なカスタムプロジェクトファイルの概要については、「[プロジェクトファイルについ](understanding-the-project-file.md)て」および「[ビルドプロセスについ](understanding-the-build-process.md)て」を参照してください。

## <a name="endpoint-considerations"></a>エンドポイントに関する考慮事項

*.Deploy*ファイルを実行して、または msdeploy.exe を直接使用して、web パッケージを配置するかどうかにかかわらず、デプロイのコンピューター名またはサービスエンドポイントを指定する必要があります。

対象の web サーバーが Web 配置リモートエージェントサービスを使用してデプロイするように構成されている場合は、ターゲットサービスの URL を送信先として指定します。

[!code-console[Main](deploying-web-packages/samples/sample9.cmd)]

または、宛先としてサーバー名だけを指定することも、リモートエージェントサービスの URL を推測 Web 配置こともできます。

[!code-console[Main](deploying-web-packages/samples/sample10.cmd)]

対象の web サーバーが Web 配置ハンドラーを使用して配置するように構成されている場合は、IIS Web 管理サービス (WMSvc) のエンドポイントアドレスを宛先として指定する必要があります。 既定では、次の形式になります。

[!code-console[Main](deploying-web-packages/samples/sample11.cmd)]

これらのエンドポイントのいずれかをターゲットにするには、 *.deploy*ファイルまたは msdeploy.exe を直接使用します。 ただし、「 [Web 配置発行用に Web サーバーを構成する (Web 配置ハンドラー)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)」の説明に従って、管理者以外のユーザーとして Web 配置ハンドラーに展開する場合は、サービスエンドポイントアドレスにクエリ文字列を追加する必要があります。

[!code-console[Main](deploying-web-packages/samples/sample12.cmd)]

これは、管理者以外のユーザーが IIS サーバー レベルのアクセスを持っていないためです。そのユーザーは、特定の IIS web サイトへのアクセスのみが。 このドキュメントの執筆時点では、Web 発行パイプライン (WPP) のバグが原因で、クエリ文字列を含むエンドポイントアドレスを使用して *.deploy*ファイルを実行することはできません。 このシナリオで直接 MSDeploy.exe を使用して、web パッケージを展開する必要があります。

> [!NOTE]
> リモートエージェントサービスと Web 配置ハンドラーの Web 配置の詳細については、「 [Web 配置に適切なアプローチを選択する](../configuring-server-environments-for-web-deployment/choosing-the-right-approach-to-web-deployment.md)」を参照してください。 これらのエンドポイントに配置するために環境固有のプロジェクトファイルを構成する方法については、「[ターゲット環境の配置プロパティを構成](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md)する」を参照してください。

## <a name="authentication-considerations"></a>認証に関する注意点

*.Deploy*ファイルを実行して、または msdeploy.exe を直接使用して、web パッケージを配置するかどうかに関係なく、認証の種類を指定する必要があります。 Web 配置には、 **NTLM**または**Basic**の2つの値を指定できます。 基本認証を指定する場合は、ユーザー名とパスワードも指定する必要があります。 認証の種類を選択する際には、次の点に注意する必要があるさまざまな要素があります。

- Web 配置リモートエージェントサービスにデプロイする場合は、NTLM 認証を使用する必要があります。 リモートエージェントサービスは、基本認証資格情報を受け入れません。
- Web 配置ハンドラーにデプロイする場合は、NTLM 認証または基本認証のいずれかを使用できます。 既定の設定は [基本認証] です。 基本認証は、プレーンテキストで送信されるユーザー名とパスワードに依存しますが、Web 配置ハンドラーが常に SSL 暗号化を使用するため、資格情報が保護されます。
- Web パッケージにデータベースが含まれており、web サーバーとデータベースサーバーが別々のコンピューターである場合、 [ntlm の "ダブルホップ" の制限](https://go.microsoft.com/?linkid=9805120)により、ntlm 認証を使用してデータベースをデプロイすることはできません。 デプロイ接続文字列で SQL Server 資格情報を使用するか、基本認証の資格情報を指定して Web 配置する必要があります。 この問題の詳細については、「[エンタープライズ環境にメンバーシップデータベースを展開する](../advanced-enterprise-web-deployment/deploying-membership-databases-to-enterprise-environments.md)」を参照してください。

## <a name="conclusion"></a>まとめ

このトピックでは、 *.deploy*ファイルを実行するか、または msdeploy.exe を直接使用して、web パッケージを配置する方法について説明します。 この記事では、各方法が適切であることを説明し、より大きなシングルステップまたは自動のビルドプロセスの一部として配置コマンドをパラメーター化して実行する方法について説明しました。

## <a name="further-reading"></a>参考資料

Web 配置パッケージを作成してパラメーター化する方法のガイダンスについては、「web[アプリケーションプロジェクトのビルドおよびパッケージ化](building-and-packaging-web-application-projects.md)」および「 [web パッケージ配置のパラメーターの構成](configuring-parameters-for-web-package-deployment.md)」を参照してください。 Team Foundation Server (TFS) インスタンスから web パッケージを構築および配置する方法については、「[自動 Web デプロイの Team Foundation Server の構成](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md)」を参照してください。 展開プロセスをカスタマイズおよびトラブルシューティングする方法については、「[展開からのファイルとフォルダーの除外](../advanced-enterprise-web-deployment/excluding-files-and-folders-from-deployment.md)」を参照してください。

> [!div class="step-by-step"]
> [前へ](configuring-parameters-for-web-package-deployment.md)
> [次へ](deploying-database-projects.md)
