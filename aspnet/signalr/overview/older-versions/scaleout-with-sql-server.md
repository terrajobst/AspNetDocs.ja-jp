---
uid: signalr/overview/older-versions/scaleout-with-sql-server
title: SQL Server を使用した SignalR スケールアウト (SignalR 1.x) |Microsoft Docs
author: bradygaster
description: ''
ms.author: bradyg
ms.date: 05/01/2013
ms.assetid: 1dca7967-8296-444a-9533-837eb284e78c
msc.legacyurl: /signalr/overview/older-versions/scaleout-with-sql-server
msc.type: authoredcontent
ms.openlocfilehash: 8674b06a2a751c9a7b1c6c9b19782974d0602a62
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78431128"
---
# <a name="signalr-scaleout-with-sql-server-signalr-1x"></a>SQL Server による SignalR スケールアウト (SignalR 1.x)

[Mike Wasson](https://github.com/MikeWasson)、[パトリック Fletcher](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

このチュートリアルでは、SQL Server を使用して、2つの異なる IIS インスタンスに配置されている SignalR アプリケーション全体にメッセージを配布します。 このチュートリアルは1つのテストコンピューターで実行することもできますが、完全な効果を得るには、SignalR アプリケーションを複数のサーバーに配置する必要があります。 また、いずれかのサーバーまたは別の専用サーバーに SQL Server をインストールする必要があります。 もう1つの方法は、Azure で Vm を使用してチュートリアルを実行することです。

![](scaleout-with-sql-server/_static/image1.png)

## <a name="prerequisites"></a>前提条件

Microsoft SQL Server 2005 以降。 バックプレーンは、SQL Server のデスクトップエディションとサーバーエディションの両方をサポートします。 SQL Server Compact Edition または Azure SQL Database はサポートされていません。 (アプリケーションが Azure でホストされている場合は、代わりに Service Bus バックプレーンを検討してください)。

## <a name="overview"></a>概要

詳細なチュートリアルを開始する前に、実行する操作の概要を簡単に説明します。

1. 新しい空のデータベースを作成します。 バックプレーンによって、このデータベースに必要なテーブルが作成されます。
2. 次の NuGet パッケージをアプリケーションに追加します。 

    - [SignalR](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [SignalR. SqlServer](http://nuget.org/packages/Microsoft.AspNet.SignalR.SqlServer)
3. SignalR アプリケーションを作成します。
4. 次のコードを global.asax に追加して、バックプレーンを構成します。 

    [!code-csharp[Main](scaleout-with-sql-server/samples/sample1.cs)]

## <a name="configure-the-database"></a>データベースを構成する

アプリケーションで Windows 認証を使用するか SQL Server 認証を使用してデータベースにアクセスするかを決定します。 に関係なく、データベースユーザーがログインし、スキーマを作成し、テーブルを作成する権限を持っていることを確認します。

バックプレーンが使用する新しいデータベースを作成します。 データベースに任意の名前を付けることができます。 データベースにテーブルを作成する必要はありません。バックプレーンによって、必要なテーブルが作成されます。

![](scaleout-with-sql-server/_static/image2.png)

## <a name="enable-service-broker"></a>Service Broker を有効にする

バックプレーンデータベースの Service Broker を有効にすることをお勧めします。 Service Broker は SQL Server でのメッセージングとキューのネイティブサポートを提供します。これにより、バックプレーンが更新をより効率的に受信できるようになります。 (ただし、バックプレーンは Service Broker なしでも動作します)。

Service Broker が有効になっているかどうかを確認するには、**データベース**カタログビューの **\_Broker\_enabled**列に対してクエリを実行します。

[!code-sql[Main](scaleout-with-sql-server/samples/sample2.sql)]

![](scaleout-with-sql-server/_static/image3.png)

Service Broker を有効にするには、次の SQL クエリを使用します。

[!code-sql[Main](scaleout-with-sql-server/samples/sample3.sql)]

> [!NOTE]
> このクエリでデッドロックが発生した場合は、データベースに接続されているアプリケーションがないことを確認してください。

トレースを有効にした場合、トレースには Service Broker が有効になっているかどうかも表示されます。

## <a name="create-a-signalr-application"></a>SignalR アプリケーションを作成する

次のいずれかのチュートリアルに従って、SignalR アプリケーションを作成します。

- [SignalR でのはじめに](../getting-started/tutorial-getting-started-with-signalr.md)
- [SignalR と MVC 4 でのはじめに](tutorial-getting-started-with-signalr-and-mvc-4.md)

次に、SQL Server によるスケールアウトをサポートするようにチャットアプリケーションを変更します。 まず、SignalR NuGet パッケージをプロジェクトに追加します。 Visual Studio で、 **[ツール]** メニューの **[NuGet パッケージマネージャー]** を選択し、 **[パッケージマネージャーコンソール]** を選択します。 [パッケージ マネージャー コンソール] ウィンドウで、次のコマンドを入力します。

[!code-powershell[Main](scaleout-with-sql-server/samples/sample4.ps1)]

次に、global.asax ファイルを開きます。 **Application\_Start**メソッドに次のコードを追加します。

[!code-csharp[Main](scaleout-with-sql-server/samples/sample5.cs)]

## <a name="deploy-and-run-the-application"></a>アプリケーションをデプロイして実行する

SignalR アプリケーションをデプロイするための Windows Server インスタンスを準備します。

IIS ロールを追加します。 WebSocket プロトコルなど、"アプリケーション開発" 機能を含めます。

![](scaleout-with-sql-server/_static/image4.png)

また、管理サービス ([管理ツール] の下に表示されます) も含めます。

![](scaleout-with-sql-server/_static/image5.png)

**Web 配置3.0 をインストールします。** IIS マネージャーを実行すると、Microsoft Web Platform のインストールを求めるメッセージが表示されます。または、[インストーラーをダウンロード](https://go.microsoft.com/fwlink/?LinkId=255386)することもできます。 プラットフォームインストーラーで Web 配置を検索し、Web 配置3.0 をインストールします。

![](scaleout-with-sql-server/_static/image6.png)

Web 管理サービスが実行されていることを確認します。 実行されていない場合は、サービスを開始します。 (Windows サービスの一覧に [Web 管理サービス] が表示されない場合は、IIS ロールを追加したときに管理サービスがインストールされていることを確認してください)。

最後に、TCP 用にポート8172を開きます。 これは Web 配置ツールが使用するポートです。

これで、開発用コンピューターからサーバーに Visual Studio プロジェクトを配置する準備ができました。 ソリューションエクスプローラーで、ソリューションを右クリックし、 **[発行]** をクリックします。

Web 配置に関する詳細なドキュメントについては、「 [Visual Studio と ASP.NET の Web 配置コンテンツマップ](../../../whitepapers/aspnet-web-deployment-content-map.md)」を参照してください。

アプリケーションを2台のサーバーに配置する場合は、各インスタンスを別のブラウザーウィンドウで開き、各インスタンスがもう一方から SignalR メッセージを受信することを確認できます。 (もちろん、運用環境では、2つのサーバーはロードバランサーの背後に配置されます)。

![](scaleout-with-sql-server/_static/image7.png)

アプリケーションを実行すると、SignalR によってデータベースにテーブルが自動的に作成されたことがわかります。

![](scaleout-with-sql-server/_static/image8.png)

SignalR はテーブルを管理します。 アプリケーションが配置されている限り、行を削除したり、テーブルを変更したりしないでください。
