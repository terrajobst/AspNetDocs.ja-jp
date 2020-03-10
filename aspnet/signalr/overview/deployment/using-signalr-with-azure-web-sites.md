---
uid: signalr/overview/deployment/using-signalr-with-azure-web-sites
title: Azure App Service | の Web Apps での SignalR の使用Microsoft Docs
author: bradygaster
description: このドキュメントでは Microsoft Azure で実行される SignalR アプリケーションを構成する方法について説明します。 このチュートリアルで使用されているソフトウェアのバージョン Visual Studio 2013 または Vis...
ms.author: bradyg
ms.date: 07/01/2015
ms.assetid: 2a7517a0-b88c-4162-ade3-9bf6ca7062fd
msc.legacyurl: /signalr/overview/deployment/using-signalr-with-azure-web-sites
msc.type: authoredcontent
ms.openlocfilehash: 0e6a18bdbe9cc47e89b5a458753845afb53595f1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78450184"
---
# <a name="using-signalr-with-web-apps-in-azure-app-service"></a>Azure App Service の Web アプリで SignalR を使用する

([パトリック Fletcher](https://github.com/pfletcher) )

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> このドキュメントでは Microsoft Azure で実行される SignalR アプリケーションを構成する方法について説明します。
>
> ## <a name="software-versions-used-in-the-tutorial"></a>このチュートリアルで使用されているソフトウェアのバージョン
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)または Visual Studio 2012
> - .NET 4.5
> - SignalR バージョン2
> - Visual Studio 2013 または2012用の Azure SDK 2.3
>
>
>
> ## <a name="questions-and-comments"></a>質問とコメント
>
> このチュートリアルの良い点に関するフィードバックや、ページ下部にあるコメントで改善できる点をお知らせください。 チュートリアルに直接関係のない質問がある場合は、 [ASP.NET SignalR フォーラム](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)、 [StackOverflow.com](http://stackoverflow.com/)、または[Microsoft Azure フォーラム](https://social.msdn.microsoft.com/Forums/windowsazure/home?category=windowsazureplatform)に投稿することができます。

## <a name="table-of-contents"></a>目次

- [はじめに](#introduction)
- [Azure App Service するための SignalR Web アプリのデプロイ](#deploying)
- [Azure App Service での Websocket の有効化](#websocket)
- [Azure Redis Cache バックプレーンの使用](#backplane)
- [次の手順](#nextsteps)

<a id="introduction"></a>
## <a name="introduction"></a>はじめに

ASP.NET SignalR を使用すると、サーバーと web クライアントまたは .NET クライアントの間に新しいレベルの対話性をもたらすことができます。 Azure でホストされている場合、SignalR アプリケーションは、クラウドで実行されている高可用性、拡張性、およびパフォーマンスに優れた環境を活用できます。

<a id="deploying"></a>
## <a name="deploying-a-signalr-web-app-to-azure-app-service"></a>Azure App Service するための SignalR Web アプリのデプロイ

SignalR は、アプリケーションを Azure にデプロイしたり、オンプレミスのサーバーにデプロイしたりするために、特定の複雑さを追加することはありません。 SignalR を使用するアプリケーションは、構成やその他の設定を変更することなく Azure でホストできます (ただし、Websocket のサポートについては、以下[の Azure App Service で websocket を有効](#websocket)にする方法に関する説明を参照してください)。このチュートリアルでは、[はじめにチュートリアル](../getting-started/tutorial-getting-started-with-signalr.md)で作成したアプリケーションを Azure にデプロイします。

**前提条件**

- Visual Studio 2013. Visual Studio をお持ちでない場合は、Azure SDK のインストールに Visual Studio 2013 Express for Web が含まれています。
- [Visual Studio 2013 の場合は AZURE sdk 2.3](https://go.microsoft.com/fwlink/?linkid=324322&clcid=0x409) 、 [Visual Studio 2012 の場合は azure sdk 2.3](https://go.microsoft.com/fwlink/p/?linkid=323511)。
- このチュートリアルを完了するには、Azure サブスクリプションが必要です。 [MSDN サブスクライバーの特典を有効](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)にすることも、[試用版サブスクリプションにサインアップ](https://azure.microsoft.com/pricing/free-trial/)することもできます。

### <a name="deploying-a-signalr-web-app-to-azure"></a>SignalR web アプリを Azure にデプロイする

1. [はじめにチュートリアル](../getting-started/tutorial-getting-started-with-signalr.md)を完了するか、[コードギャラリー](https://code.msdn.microsoft.com/SignalR-Getting-Started-b9d18aa9)から完成したプロジェクトをダウンロードします。
2. Visual Studio で、 **[ビルド]** 、 **[Publish SignalR Chat]** を選択します。
3. [Web の発行] ダイアログで、[Windows Azure Websites] を選択します。

    ![Azure Websites の選択](using-signalr-with-azure-web-sites/_static/image1.png)
4. Microsoft アカウントにサインインしていない場合は、既存の Web サイトの選択 ダイアログボックスで **サインイン...** をクリックし、サインインします。

    ![既存の Web サイトの選択](using-signalr-with-azure-web-sites/_static/image2.png)    ![Azure へのサインイン](using-signalr-with-azure-web-sites/_static/image3.png)
5. 既存の Web サイトの選択 ダイアログボックスで、**新規** をクリックします。

    ![[新しい Web サイト]](using-signalr-with-azure-web-sites/_static/image4.png)
6. [Windows Azure でのサイトの作成] ダイアログボックスで、一意のアプリ名を入力します。 [リージョン] ボックスの一覧で、最も近いリージョンを選択します。 **Create** をクリックしてください。

    ![Azure でのサイトの作成](using-signalr-with-azure-web-sites/_static/image5.png)
7. Web の発行 ダイアログで、**発行** をクリックします。

    ![サイトの発行](using-signalr-with-azure-web-sites/_static/image6.png)
8. アプリの発行が完了すると、Azure App Service Web Apps でホストされている SignalR Chat アプリケーションがブラウザーで開きます。

    ![ブラウザーでサイトを開く](using-signalr-with-azure-web-sites/_static/image7.png)

<a id="websocket"></a>
### <a name="enabling-websockets-on-azure-app-service-web-apps"></a>Azure App Service Web Apps で Websocket を有効にする

SignalR アプリケーションで使用するには、web アプリで Websocket を明示的に有効にする必要があります。それ以外の場合は、他のプロトコルが使用されます (詳細については、「[トランスポートとフォールバック](../getting-started/introduction-to-signalr.md#transports)」を参照してください)。

Azure App Service Web Apps で Websocket を使用するには、Web アプリの [構成] セクションで有効にする必要があります。 これを行うには、 [Azure 管理ポータル](https://manage.windowsazure.com/)で web アプリを開き、[構成] を選択します。

![[Configure (構成)] タブ](using-signalr-with-azure-web-sites/_static/image8.png)

[構成] ページの上部で、web アプリに .NET 4.5 が使用されていることを確認します。

![.NET framework バージョン4.5 設定](using-signalr-with-azure-web-sites/_static/image9.png)

構成 ページの  **websocket** 設定で、**オン** を選択します。

![Websocket の設定: オン](using-signalr-with-azure-web-sites/_static/image10.png)

構成ページの下部にある **[保存]** を選択して変更を保存します。

![設定の保存](using-signalr-with-azure-web-sites/_static/image11.png)

<a id="backplane"></a>
## <a name="using-the-azure-redis-cache-backplane"></a>Azure Redis Cache バックプレーンの使用

Web アプリに複数のインスタンスを使用し、それらのインスタンスのユーザーが相互に対話する必要がある場合 (たとえば、1つのインスタンスで作成されたチャットメッセージが、他のインスタンスに接続されているユーザーに到着する可能性がある場合)、 [Azure Redis Cache バックプレーン](../performance/scaleout-with-redis.md)をアプリケーションに実装する必要があります。

<a id="nextsteps"></a>
## <a name="next-steps"></a>次の手順

Azure App Service の Web Apps の詳細については、「 [Web Apps の概要](https://azure.microsoft.com/documentation/articles/app-service-web-overview/)」を参照してください。
