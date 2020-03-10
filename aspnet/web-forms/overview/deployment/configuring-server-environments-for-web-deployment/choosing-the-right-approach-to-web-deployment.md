---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/choosing-the-right-approach-to-web-deployment
title: Web 配置に適切なアプローチを選択する |Microsoft Docs
author: jrjlee
description: インターネットインフォメーションサービス (IIS) Web 配置ツール (Web 配置) 2.0 以降を使用する場合は、次の3つの主な方法で作業できます。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 787a53fd-9901-4a11-9d58-61e0509cda45
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/choosing-the-right-approach-to-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: 13f784dd8e6404806104d56b026b3c41ca178892
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78441424"
---
# <a name="choosing-the-right-approach-to-web-deployment"></a>適切な Web 配置手法を選択する

[Jason Lee](https://github.com/jrjlee)

[[Download PDF]\(PDF をダウンロード\)](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> インターネットインフォメーションサービス (IIS) Web 配置ツール (Web 配置) 2.0 以降を使用する場合、パッケージ化された web アプリケーションを web サーバーに取り込むために使用できる3つの主な方法があります。 次のいずれかを実行できます。
> 
> - 移行先サーバーで*Web Deployment Agent サービス*("リモートエージェント" とも呼ばれます) をターゲットにして、リモートの場所からアプリケーションを展開します。
> - 必要に応じて Web 配置 ("一時エージェント" とも呼ばれます) を使用して、リモートの場所からアプリケーションをデプロイします。
> - 移行先サーバーで*IIS Web 配置ハンドラー*をターゲットにして、リモートの場所からアプリケーションを展開します。
> - Web パッケージを移行先サーバーに手動でコピーし、IIS マネージャーを使用してインポートして、アプリケーションを展開します。
> 
> 移行先の web サーバーをどのように構成するかは、使用する展開方法によって異なります。 このトピックは、展開する方法を決定するのに役立ちます。

次の表は、各展開方法の主な利点と欠点と、各アプローチに最も適しているシナリオを示しています。

| アプローチ | 長所 | 短所 | 標準のシナリオ |
| --- | --- | --- | --- |
| リモートエージェント | セットアップは簡単です。 これは、web アプリケーションおよびコンテンツに対する通常の更新に適しています。 | ユーザーは、対象サーバーの管理者である必要があります。 ユーザーは代替の資格情報を指定できません。 | 開発環境。 テスト環境。 |
| 一時エージェント | ターゲットコンピューターに Web 配置をインストールする必要はありません。 最新バージョンの Web 配置が自動的に使用されます。 | ユーザーは、対象サーバーの管理者である必要があります。 ユーザーは代替の資格情報を指定できません。 | 開発環境。 テスト環境。 |
| Web 配置ハンドラー | 管理者以外のユーザーは、コンテンツを展開できます。 これは、web アプリケーションおよびコンテンツに対する通常の更新に適しています。 | 設定が複雑になります。 | ステージング環境。 イントラネット運用環境。 ホストされている環境。 |
| オフライン展開 | 非常に簡単に設定できます。 分離された環境に適しています。 | サーバー管理者は、web パッケージを毎回手動でコピーしてインポートする必要があります。 | インターネットに接続する運用環境。 分離されたネットワーク環境。 |

## <a name="using-the-remote-agent"></a>リモートエージェントの使用

移行先サーバーで既定の設定を使用して Web 配置をインストールすると、Web Deployment Agent サービス ("リモートエージェント") が自動的にインストールされ、開始されます。 既定では、リモートエージェントは、次のアドレスで HTTP エンドポイントを公開します。

[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample1.cmd)]

> [!NOTE]
> [*Server*] を web サーバーのコンピューター名、web サーバーの IP アドレス、または web サーバーに解決されるホスト名に置き換えることができます。

サーバー管理者は、このエンドポイントアドレスを指定することによって、開発者用コンピューターやビルドサーバーなどのリモートの場所から web パッケージを配置できます。 たとえば、Fabrikam, Inc. の jeff Hink によって開発者のコンピューターに ContactManager Mvc web アプリケーションプロジェクトがビルドされたとします。 ビルドプロセスでは、パッケージをインストールするために必要な Web 配置のコマンドを含む *.deploy*ファイルと共に、web パッケージが生成されます。 TESTWEB1 サーバーのサーバー管理者である場合は、開発者のコンピューターで次のコマンドを実行して、web アプリケーションをテスト web サーバーにデプロイできます。

[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample2.cmd)]

実際には、コンピューター名を指定した場合、Web 配置実行可能ファイルはリモートエージェントのエンドポイントアドレスを推測できます。そのため、次のように入力する必要があります。

[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample3.cmd)]

> [!NOTE]
> Web 配置のコマンドライン構文と .deploy ファイルの*展開*の詳細については、「[方法: .Deploy ファイルを使用して展開パッケージをインストール](https://msdn.microsoft.com/library/ff356104.aspx)する」を参照してください。

リモートエージェントは、リモートの場所からコンテンツを簡単に展開できる方法を提供します。この方法は、ワンクリックまたは自動の展開で効果的に機能します。 ただし、展開コマンドを実行するユーザーは、ドメイン管理者であるか、または移行先サーバーのローカル administrators グループのメンバーである必要があります。 また、リモートエージェントは基本認証をサポートしていないため、コマンドラインで代替資格情報を渡すことはできません。

リモートエージェントは、開発またはテストシナリオでの配置に便利なアプローチを提供します。開発者がテストサーバー環境に対して完全な管理者権限を持つことは珍しくありません。アプリケーションは通常、再構築され、再展開されます。頻繁. ただし、この方法は、通常、ステージング環境または運用環境では受け入れられません。

リモートエージェントアプローチを使用するシナリオのエンドツーエンドの例については、「[シナリオ: Web 配置用のテスト環境を構成](scenario-configuring-a-test-environment-for-web-deployment.md)する」を参照してください。

## <a name="using-the-temp-agent"></a>一時エージェントの使用

一時エージェントの配置方法は、リモートエージェントのアプローチに似ています。 ただし、リモートエージェントの方法とは異なり、移行先の Web サーバーに Web 配置をインストールする必要はありません。 代わりに、デプロイを実行すると、Web 配置によって移行先サーバーに Web 配置エージェントサービスの一時的なバージョンがインストールされ、これを使用してコンテンツが IIS に展開されます。 デプロイが完了すると、すべての一時ファイルが削除されます。

一時エージェントプロバイダーの設定を使用する場合は、展開コマンドに **/g**フラグを追加します。

[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample4.cmd)]

> [!NOTE]
> サービスが実行されていない場合でも、対象のコンピューターに web 配置エージェントサービスがインストールされている場合、一時エージェントを使用することはできません。

この方法の利点は、移行先サーバーに Web 配置のインストールを維持する必要がないことです。 さらに、移行元と移行先のコンピューターで同じバージョンの Web 配置が実行されていることを確認する必要はありません。 ただし、この方法では、リモートエージェントアプローチと同じプリンシパル制限が適用されます。つまり、コンテンツを展開するためには、移行先サーバーのローカル管理者である必要があり、NTLM 認証のみがサポートされます。 また、一時エージェントのアプローチでは、より多くの初期構成が必要になります。

Temp エージェントの使用方法の詳細については、「[方法: .Deploy ファイルを使用して展開パッケージをインストール](https://msdn.microsoft.com/library/ff356104.aspx)し、[オンデマンドで Web 配置](https://technet.microsoft.com/library/ee517345(WS.10).aspx)する」を参照してください。

## <a name="using-the-web-deploy-handler"></a>Web 配置ハンドラーの使用

IIS 7 以降では、Web 配置は IIS Web 配置ハンドラーを使用した代替の展開方法を提供します。 Web 配置ハンドラーは、IIS Web 管理サービス (WMSvc) と密接に統合されています。このサービスは、ユーザーがリモートの場所から IIS web サイトを管理できるように設計されています。

既定では、リモートエージェントは、次のアドレスで HTTP エンドポイントを公開します。

[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample5.cmd)]

> [!NOTE]
> [*Server*] を web サーバーのコンピューター名、web サーバーの IP アドレス、または web サーバーに解決されるホスト名に置き換えることができます。

リモートエージェントと temp エージェントの Web 配置ハンドラーの大きな利点は、管理者以外のユーザーが特定の IIS web サイトにアプリケーションとコンテンツを展開することを許可するように IIS を構成できることです。 Web 配置ハンドラーは基本認証もサポートしているため、Web 配置コマンドのパラメーターとして代替資格情報を指定できます。 主な欠点は、Web 配置ハンドラーの初期設定と構成が複雑になることです。

管理者以外のユーザーの場合、Web 管理サービス (WMSvc) は、ユーザーがサーバーレベルの接続ではなくサイトレベルの接続を使用して IIS に接続することのみを許可します。 特定のサイトにアクセスするには、サイト固有のクエリ文字列をエンドポイントアドレスに含めることができます。

[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample6.cmd)]

たとえば、ビルドが成功するたびに、ステージング環境に web アプリケーションを自動的にデプロイするようにビルドプロセスが構成されているとします。 リモートエージェントの手法を使用した場合は、ビルドプロセスで対象サーバーの管理者を識別する必要があります。 これに対し、Web 配置ハンドラーの手法を使用すると、管理者以外&#x2014;**のユーザーに特定の IIS** web サイトへの&#x2014;アクセス許可のみを与えることができます。また、ビルドプロセスでは、これらの資格情報を提供して Web パッケージを配置できます。

[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample7.cmd)]

> [!NOTE]
> Web 配置のコマンドライン操作と構文の詳細については[Web 配置「コマンドラインリファレンス](https://technet.microsoft.com/library/dd568991(v=ws.10).aspx)」を参照してください。 *.Deploy*ファイルの使用方法の詳細については、「[方法: .Deploy ファイルを使用して展開パッケージをインストール](https://msdn.microsoft.com/library/ff356104.aspx)する」を参照してください。

Web 配置ハンドラーは、ステージング環境、ホスト環境、およびイントラネットベースの運用環境での配置に便利なアプローチを提供します。この環境では、サーバーへのリモートアクセスは使用できますが、管理者の資格情報は使用できません。

Web 配置ハンドラアプローチを使用するシナリオのエンドツーエンドの例については、「[シナリオ: Web デプロイのステージング環境を構成](scenario-configuring-a-staging-environment-for-web-deployment.md)する」を参照してください。

## <a name="using-offline-deployment"></a>オフライン展開の使用

場合によっては、リモートの場所から IIS web サイトにアプリケーションとコンテンツを展開することはできません。 たとえば、移行元と移行先のコンピューターが、分離されたネットワークまたはネットワークセグメントに存在する場合や、ファイアウォールポリシーによってリモートアクセスが許可されない場合があります。

このようなシナリオでは、Web 配置のパッケージ化機能と発行機能を引き続き使用できます。リモートの場所からは使用できません。 代わりに、移行先サーバーの管理者が web パッケージをサーバーにコピーし、IIS マネージャーを使用してインポートする必要があります。

![](choosing-the-right-approach-to-web-deployment/_static/image1.png)

オフライン展開方法は、通常、境界ネットワーク内のサーバーが内部ネットワーク内のコンピューターとの接続を制限している可能性がある、インターネットに接続された運用環境で役立ちます。

オフライン展開方法を使用するシナリオのエンドツーエンドの例については、「[シナリオ: Web 配置用の運用環境の構成](scenario-configuring-a-production-environment-for-web-deployment.md)」を参照してください。

## <a name="further-reading"></a>参考資料

Web 配置のコマンドライン操作と構文の詳細については[Web 配置「コマンドラインリファレンス](https://technet.microsoft.com/library/dd568991(v=ws.10).aspx)」を参照してください。 *.Deploy*ファイルの使用方法の詳細については、「[方法: .Deploy ファイルを使用して展開パッケージをインストール](https://msdn.microsoft.com/library/ff356104.aspx)する」を参照してください。

リモートコンピューターから web パッケージを展開するさまざまな方法に関する一般的なガイダンスについては、「リモートでの[Web 配置の使用](https://technet.microsoft.com/library/ee461175(WS.10).aspx)」を参照してください。 オンデマンドでの Web 配置の使用の詳細については、「 [Web 配置オンデマンド](https://technet.microsoft.com/library/ee517345(WS.10).aspx)」を参照してください。

> [!div class="step-by-step"]
> [前へ](configuring-server-environments-for-web-deployment.md)
> [次へ](scenario-configuring-a-test-environment-for-web-deployment.md)
