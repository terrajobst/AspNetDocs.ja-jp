---
uid: signalr/overview/performance/scaleout-with-redis
title: Redis による SignalR スケールアウト |Microsoft Docs
author: bradygaster
description: この Visual Studio 2013 トピックで使用されているソフトウェアのバージョンについては、このトピックの以前のバージョンの .NET 4.5 SignalR バージョン2以前のバージョンを参照してください。
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 6ecd08c1-e364-4cd7-ad4c-806521911585
msc.legacyurl: /signalr/overview/performance/scaleout-with-redis
msc.type: authoredcontent
ms.openlocfilehash: 58a7affa1769523955adc76455a1c33be6f49751
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467776"
---
# <a name="signalr-scaleout-with-redis"></a>Redis による SignalR スケールアウト

[Mike Wasson](https://github.com/MikeWasson)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> ## <a name="software-versions-used-in-this-topic"></a>このトピックで使用されているソフトウェアのバージョン
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - .NET 4.5
> - SignalR バージョン2.4
>
>
>
> ## <a name="previous-versions-of-this-topic"></a>このトピックの前のバージョン
>
> 以前のバージョンの SignalR の詳細については、「[古いバージョンの SignalR](../older-versions/index.md)」を参照してください。
>
> ## <a name="questions-and-comments"></a>質問とコメント
>
> このチュートリアルの良い点に関するフィードバックや、ページ下部にあるコメントで改善できる点をお知らせください。 チュートリアルに直接関係のない質問がある場合は、 [ASP.NET SignalR フォーラム](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)または[StackOverflow.com](http://stackoverflow.com/)に投稿できます。

このチュートリアルでは、 [Redis](http://redis.io/)を使用して、2つの異なる IIS インスタンスに展開されている SignalR アプリケーション全体にメッセージを配信します。

Redis は、メモリ内のキーと値のストアです。 また、パブリッシュ/サブスクライブモデルを持つメッセージングシステムもサポートしています。 SignalR Redis バックプレーンは、pub/sub 機能を使用して、他のサーバーにメッセージを転送します。

![](scaleout-with-redis/_static/image1.png)

このチュートリアルでは、3台のサーバーを使用します。

- Windows を実行する2台のサーバー。これは、SignalR アプリケーションの展開に使用します。
- Linux を実行する1台のサーバー。 Redis の実行に使用します。 このチュートリアルのスクリーンショットでは、Ubuntu 12.04 TLS を使用しました。

使用する物理サーバーが3台ない場合は、Hyper-v で Vm を作成できます。 もう1つの方法は、Azure で Vm を作成することです。

このチュートリアルでは、Redis の公式実装を使用していますが、MSOpenTech[の Windows ポート](https://github.com/MSOpenTech/redis)もあります。 セットアップと構成は異なりますが、それ以外の手順は同じです。

> [!NOTE]
>
> Redis による SignalR スケールアウトは、Redis クラスターをサポートしていません。

## <a name="overview"></a>概要

詳細なチュートリアルを開始する前に、実行する操作の概要を簡単に説明します。

1. Redis をインストールし、Redis サーバーを起動します。
2. 次の NuGet パッケージをアプリケーションに追加します。

    - [SignalR](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [SignalR. StackExchangeRedis](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.StackExchangeRedis)
    
3. SignalR アプリケーションを作成します。
4. Startup.cs に次のコードを追加して、バックプレーンを構成します。

    [!code-csharp[Main](scaleout-with-redis/samples/sample1.cs)]

## <a name="ubuntu-on-hyper-v"></a>Hyper-v 上の Ubuntu

Windows Hyper-v を使用すると、Windows Server 上に Ubuntu VM を簡単に作成できます。

[http://www.ubuntu.com](http://www.ubuntu.com/)から Ubuntu ISO をダウンロードします。

Hyper-v で、新しい VM を追加します。 **[仮想ハードディスクの接続]** 手順で、 **[仮想ハードディスクの作成]** を選択します。

![](scaleout-with-redis/_static/image2.png)

**[インストールオプション]** ステップで **[イメージファイル (.iso)]** を選択し、 **[参照]** をクリックして、Ubuntu インストール iso を参照します。

![](scaleout-with-redis/_static/image3.png)

## <a name="install-redis"></a>Redis のインストール

[http://redis.io/download](http://redis.io/download)の手順に従って Redis をダウンロードしてビルドします。

[!code-console[Main](scaleout-with-redis/samples/sample2.cmd)]

これにより、`src` ディレクトリに Redis バイナリがビルドされます。

既定では、Redis はパスワードを必要としません。 パスワードを設定するには、ソースコードのルートディレクトリにある `redis.conf` ファイルを編集します。 (編集する前に、ファイルのバックアップコピーを作成してください)`redis.conf`に次のディレクティブを追加します。

[!code-powershell[Main](scaleout-with-redis/samples/sample3.ps1)]

次に、Redis サーバーを起動します。

[!code-css[Main](scaleout-with-redis/samples/sample4.css)]

![](scaleout-with-redis/_static/image4.png)

Redis がリッスンする既定のポートであるポート6379を開きます。 (構成ファイルのポート番号は変更できます)。

## <a name="create-the-signalr-application"></a>SignalR アプリケーションを作成する

次のいずれかのチュートリアルに従って、SignalR アプリケーションを作成します。

- [SignalR 2.0 でのはじめに](../getting-started/tutorial-getting-started-with-signalr.md)
- [SignalR 2.0 および MVC 5 でのはじめに](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)

次に、Redis でのスケールアウトをサポートするようにチャットアプリケーションを変更します。 まず、`Microsoft.AspNet.SignalR.StackExchangeRedis` NuGet パッケージをプロジェクトに追加します。 Visual Studio で、 **[ツール]** メニューの **[NuGet パッケージマネージャー]** を選択し、 **[パッケージマネージャーコンソール]** を選択します。 [パッケージ マネージャー コンソール] ウィンドウで、次のコマンドを入力します。

[!code-powershell[Main](scaleout-with-redis/samples/sample5.ps1)]

次に、Startup.cs ファイルを開きます。 **構成**メソッドに次のコードを追加します。

[!code-csharp[Main](scaleout-with-redis/samples/sample6.cs)]

- "server" は、Redis を実行しているサーバーの名前です。
- *ポート番号*を指定します。
- "password" は、redis ファイルで定義したパスワードです。
- "AppName" は任意の文字列です。 SignalR は、この名前で Redis pub/sub チャネルを作成します。

次に例を示します。

[!code-csharp[Main](scaleout-with-redis/samples/sample7.cs)]

## <a name="deploy-and-run-the-application"></a>アプリケーションをデプロイして実行する

SignalR アプリケーションをデプロイするための Windows Server インスタンスを準備します。

IIS ロールを追加します。 WebSocket プロトコルなど、"アプリケーション開発" 機能を含めます。

![](scaleout-with-redis/_static/image5.png)

また、管理サービス ([管理ツール] の下に表示されます) も含めます。

![](scaleout-with-redis/_static/image6.png)

**Web 配置3.0 をインストールします。** IIS マネージャーを実行すると、Microsoft Web Platform のインストールを求めるメッセージが表示されます。または、[インストーラーをダウンロード](https://go.microsoft.com/fwlink/?LinkId=255386)することもできます。 プラットフォームインストーラーで Web 配置を検索し、Web 配置3.0 をインストールします。

![](scaleout-with-redis/_static/image7.png)

Web 管理サービスが実行されていることを確認します。 実行されていない場合は、サービスを開始します。 (Windows サービスの一覧に [Web 管理サービス] が表示されない場合は、IIS ロールを追加したときに管理サービスがインストールされていることを確認してください)。

既定では、Web 管理サービスは TCP ポート8172でリッスンします。 Windows ファイアウォールで、ポート8172の TCP トラフィックを許可する新しい受信の規則を作成します。 詳細については、「[ファイアウォール規則の構成](https://technet.microsoft.com/library/dd448559(WS.10).aspx)」を参照してください。 (Azure で Vm をホストしている場合は、Azure portal で直接行うことができます。 「[仮想マシンに対してエンドポイントを設定する方法」を](https://azure.microsoft.com/documentation/articles/virtual-machines-set-up-endpoints/)参照してください)。

これで、開発用コンピューターからサーバーに Visual Studio プロジェクトを配置する準備ができました。 ソリューションエクスプローラーで、ソリューションを右クリックし、 **[発行]** をクリックします。

Web 配置に関する詳細なドキュメントについては、「 [Visual Studio と ASP.NET の Web 配置コンテンツマップ](../../../whitepapers/aspnet-web-deployment-content-map.md)」を参照してください。

アプリケーションを2台のサーバーに配置する場合は、各インスタンスを別のブラウザーウィンドウで開き、各インスタンスがもう一方から SignalR メッセージを受信することを確認できます。 (もちろん、運用環境では、2つのサーバーはロードバランサーの背後に配置されます)。

![](scaleout-with-redis/_static/image8.png)

Redis に送信されるメッセージを確認する場合は、redis と共にインストールされる**redis cli**クライアントを使用できます。

[!code-xml[Main](scaleout-with-redis/samples/sample8.xml)]

![](scaleout-with-redis/_static/image9.png)
