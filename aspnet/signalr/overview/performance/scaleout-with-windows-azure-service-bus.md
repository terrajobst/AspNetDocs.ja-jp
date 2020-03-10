---
uid: signalr/overview/performance/scaleout-with-windows-azure-service-bus
title: Azure Service Bus を使用したスケールアウトの SignalR |Microsoft Docs
author: bradygaster
description: このトピックで使用されているソフトウェアのバージョン Visual Studio 2013 このトピックの SignalR 1.x バージョンについては、このトピックの .NET 4.5 SignalR バージョン2以前のバージョンを参照してください,...
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: ce1305f9-30fd-49e3-bf38-d0a78dfb06c3
msc.legacyurl: /signalr/overview/performance/scaleout-with-windows-azure-service-bus
msc.type: authoredcontent
ms.openlocfilehash: 73ed95c5027f57c7e390069dcb36b18a3714973f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467734"
---
# <a name="signalr-scaleout-with-azure-service-bus"></a>Azure Service Bus による SignalR スケールアウト

[Mike Wasson](https://github.com/MikeWasson)、[パトリック Fletcher](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

このチュートリアルでは、Service Bus バックプレーンを使用して各ロールインスタンスにメッセージを配布する Windows Azure Web ロールに SignalR アプリケーションをデプロイします。 ( [Azure App Service の web apps](https://docs.microsoft.com/azure/app-service-web/)では、Service Bus バックプレーンを使用することもできます)。

![](scaleout-with-windows-azure-service-bus/_static/image1.png)

前提条件:

- Windows Azure アカウント。
- [Windows AZURE SDK](https://go.microsoft.com/fwlink/?linkid=254364&amp;clcid=0x409)。
- Visual Studio 2012 または 2013。

Service bus のバックプレーンは、 [Windows Server バージョン1.1 の Service Bus](https://msdn.microsoft.com/library/windowsazure/dn282144.aspx)とも互換性があります。 ただし、バージョン1.0 の Windows Server Service Bus と互換性がありません。

## <a name="pricing"></a>価格

Service Bus バックプレーンは、トピックを使用してメッセージを送信します。 最新の価格情報については、「 [Service Bus](https://azure.microsoft.com/pricing/details/service-bus/)」を参照してください。 このドキュメントの執筆時点では、$1 未満の場合、1か月あたり100万メッセージを送信できます。 バックプレーンは、SignalR hub メソッドを呼び出すたびに service bus メッセージを送信します。 接続、切断、グループへの参加またはグループからの脱退など、いくつかの制御メッセージもあります。 ほとんどのアプリケーションでは、ほとんどのメッセージトラフィックはハブメソッドの呼び出しになります。

## <a name="overview"></a>概要

詳細なチュートリアルを開始する前に、実行する操作の概要を簡単に説明します。

1. Windows Azure portal を使用して、新しい Service Bus 名前空間を作成します。
2. 次の NuGet パッケージをアプリケーションに追加します。 

    - [SignalR](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [SignalR. ServiceBus3](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.ServiceBus3)または[SignalR..](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.ServiceBus)
3. SignalR アプリケーションを作成します。
4. Startup.cs に次のコードを追加して、バックプレーンを構成します。 

    [!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample1.cs)]

このコードでは、[トピックの数](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.servicebusscaleoutconfiguration.topiccount(v=vs.118).aspx)と[MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx)の既定値を使用してバックプレーンが構成されます。 これらの値を変更する方法の詳細については、「 [SignalR Performance: スケールアウトメトリック](signalr-performance.md#scaleout_metrics)」を参照してください。

各アプリケーションについて、"自分の Appname" に別の値を選択します。 複数のアプリケーションで同じ値を使用しないでください。

## <a name="create-the-azure-services"></a>Azure サービスを作成する

「[クラウドサービスを作成およびデプロイする方法](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy)」の説明に従って、クラウドサービスを作成します。 「簡易作成を使用してクラウドサービスを作成する方法」の手順に従います。 このチュートリアルでは、証明書をアップロードする必要はありません。

![](scaleout-with-windows-azure-service-bus/_static/image2.png)

[Service Bus トピック/サブスクリプションの使用方法に関する](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions)ページの説明に従って、新しい Service Bus 名前空間を作成します。 「サービス名前空間の作成」セクションの手順に従います。

![](scaleout-with-windows-azure-service-bus/_static/image3.png)

> [!NOTE]
> 必ず、クラウドサービスと Service Bus 名前空間に同じリージョンを選択してください。

## <a name="create-the-visual-studio-project"></a>Visual Studio プロジェクトを作成する

Visual Studio を起動します。 **[ファイル]** メニューの **[新しいプロジェクト]** をクリックします。

**[新しいプロジェクト]** ダイアログボックスで、 **[ C#ビジュアル**] を展開します。 **[インストールされたテンプレート]** で、 **[クラウド]** を選択し、 **[Windows Azure クラウドサービス]** を選択します。 既定の .NET Framework 4.5 をそのままにします。 アプリケーションにチャットサービスの名前を指定し、[ **OK]** をクリックします。

![](scaleout-with-windows-azure-service-bus/_static/image4.png)

**新しい Windows Azure クラウドサービス** ダイアログで、ASP.NET Web Role を選択します。 右矢印ボタン ( **&gt;** ) をクリックして、ソリューションにロールを追加します。

新しいロールの上にマウスポインターを置くと、鉛筆アイコンが表示されます。 ロールの名前を変更するには、このアイコンをクリックします。 ロールに "SignalRChat" という名前を指定し、[ **OK]** をクリックします。

![](scaleout-with-windows-azure-service-bus/_static/image5.png)

**New ASP.NET プロジェクト** ダイアログボックスで、**MVC** を選択し、OK をクリックします。

![](scaleout-with-windows-azure-service-bus/_static/image6.png)

プロジェクトウィザードでは、次の2つのプロジェクトが作成されます。

- チャットサービス: このプロジェクトは Windows Azure アプリケーションです。 Azure ロールとその他の構成オプションを定義します。
- SignalRChat: このプロジェクトは、ASP.NET MVC 5 プロジェクトです。

## <a name="create-the-signalr-chat-application"></a>SignalR Chat アプリケーションを作成する

チャットアプリケーションを作成するには、チュートリアル「 [SignalR と MVC 5 でのはじめに](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)」の手順に従います。

NuGet を使用して、必要なライブラリをインストールします。 **[ツール]** メニューの **[NuGet パッケージマネージャー]** を選択し、 **[パッケージマネージャーコンソール]** を選択します。 **[パッケージマネージャーコンソール]** ウィンドウで、次のコマンドを入力します。

[!code-powershell[Main](scaleout-with-windows-azure-service-bus/samples/sample2.ps1)]

Windows Azure プロジェクトではなく、ASP.NET MVC プロジェクトにパッケージをインストールするには、`-ProjectName` オプションを使用します。

## <a name="configure-the-backplane"></a>バックプレーンの構成

アプリケーションの Startup.cs ファイルに、次のコードを追加します。

[!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample3.cs)]

ここで、service bus 接続文字列を取得する必要があります。 Azure portal で、作成した service bus 名前空間を選択し、[アクセスキー] アイコンをクリックします。

![](scaleout-with-windows-azure-service-bus/_static/image7.png)

接続文字列をクリップボードにコピーし、 *connectionString*変数に貼り付けます。

![](scaleout-with-windows-azure-service-bus/_static/image8.png)

[!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample4.cs)]

## <a name="deploy-to-azure"></a>Deploy to Azure (Azure へのデプロイ)

ソリューションエクスプローラーで、チャットサービスプロジェクト内の**Roles**フォルダーを展開します。

![](scaleout-with-windows-azure-service-bus/_static/image9.png)

SignalRChat ロールを右クリックし、**プロパティ** を選択します。 **構成** タブを選択します。**インスタンス** で 2 を選択します。 また、VM のサイズを**極小**に設定することもできます。

![](scaleout-with-windows-azure-service-bus/_static/image10.png)

変更を保存します。

ソリューションエクスプローラーで、[チャットサービス] プロジェクトを右クリックします。 **[発行]** を選択します。

![](scaleout-with-windows-azure-service-bus/_static/image11.png)

初めて Windows Azure に発行する場合は、資格情報をダウンロードする必要があります。 **発行**ウィザードで、[サインインして資格情報をダウンロードする] をクリックします。 これにより、Windows Azure portal にサインインし、発行設定ファイルをダウンロードするように求められます。

![](scaleout-with-windows-azure-service-bus/_static/image12.png)

**[インポート]** をクリックし、ダウンロードした発行設定ファイルを選択します。

**[次へ]** をクリックします。 **[発行の設定]** ダイアログの **[クラウドサービス]** で、前の手順で作成したクラウドサービスを選択します。

![](scaleout-with-windows-azure-service-bus/_static/image13.png)

**[発行]** をクリックします。 アプリケーションをデプロイして Vm を起動するまでに数分かかることがあります。

ここで、チャットアプリケーションを実行すると、ロールインスタンスは、Service Bus のトピックを使用して Azure Service Bus 経由で通信します。 トピックは、複数のサブスクライバーを許可するメッセージキューです。

バックプレーンによって、トピックとサブスクリプションが自動的に作成されます。 サブスクリプションとメッセージアクティビティを表示するには、Azure portal を開き、Service Bus 名前空間を選択し、[トピック] をクリックします。

![](scaleout-with-windows-azure-service-bus/_static/image14.png)

メッセージアクティビティがダッシュボードに表示されるまでに数分かかります。

![](scaleout-with-windows-azure-service-bus/_static/image15.png)

SignalR は、トピックの有効期間を管理します。 アプリケーションが配置されている限り、トピックを手動で削除したり、設定を変更したりしないでください。

## <a name="troubleshooting"></a>トラブルシューティング

**InvalidOperationException "サポートされている唯一の IsolationLevel は ' IsolationLevel ' です。"**

このエラーは、操作のトランザクションレベルが `Serializable`以外に設定されている場合に発生する可能性があります。 他のトランザクションレベルで実行されている操作がないことを確認します。
