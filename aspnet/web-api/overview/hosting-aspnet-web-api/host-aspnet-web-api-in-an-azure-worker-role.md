---
uid: web-api/overview/hosting-aspnet-web-api/host-aspnet-web-api-in-an-azure-worker-role
title: Azure ワーカーロールでのホスト ASP.NET Web API 2-ASP.NET 4.x
author: MikeWasson
description: 'チュートリアル: OWIN を使用して、Web API フレームワークをセルフホストする Azure Worker ロールで ASP.NET Web API をホストします。'
ms.author: riande
ms.date: 04/02/2014
ms.custom: seoapril2019
ms.assetid: 6980ee2e-d6b0-4a08-8fb6-ab96362dd0e3
msc.legacyurl: /web-api/overview/hosting-aspnet-web-api/host-aspnet-web-api-in-an-azure-worker-role
msc.type: authoredcontent
ms.openlocfilehash: ec9904e0bff090be0f504036ae73977cfca0cb31
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448408"
---
# <a name="host-aspnet-web-api-2-in-an-azure-worker-role"></a>Azure Worker ロールでのホスト ASP.NET Web API 2

[Mike Wasson](https://github.com/MikeWasson)

> このチュートリアルでは、OWIN を使用して Web API フレームワークをセルフホストする Azure Worker ロールで ASP.NET Web API をホストする方法について説明します。
>
> [Open Web Interface for .net](http://owin.org/) (OWIN) は、.net web サーバーと web アプリケーションの間の抽象化を定義します。 OWIN は、サーバーから web アプリケーションを分離します。これにより、OWIN は、Azure ワーカーロール内など、IIS の外部にある独自のプロセスで web アプリケーションを自己ホストするのに最適です。
>
> このチュートリアルでは、HttpListener パッケージを使用します。これは、自己ホスト型の OWIN アプリケーションに使用される HTTP サーバーを提供します。
>
> ## <a name="software-versions-used-in-the-tutorial"></a>このチュートリアルで使用されているソフトウェアのバージョン
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - Web API 2
> - [Azure SDK for .NET 2.3](https://azure.microsoft.com/downloads/)

## <a name="create-a-microsoft-azure-project"></a>Microsoft Azure プロジェクトを作成する

管理者特権で Visual Studio を起動します。 Azure コンピューティングエミュレーターを使用してローカルでアプリケーションをデバッグするには、管理者特権が必要です。

**[ファイル]** メニューの **[新規作成]** をクリックし、 **[プロジェクト]** をクリックします。 **インストールされているテンプレート**から、ビジュアルC# の下にある **クラウド** をクリックし、**Windows Azure クラウドサービス** をクリックします。 プロジェクトに "AzureApp" という名前を指定し、[ **OK]** をクリックします。

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image2.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image1.png)

**[新しい Windows Azure クラウドサービス]** ダイアログで、 **[Worker ロール]** をダブルクリックします。 既定の名前 ("WorkerRole1") をそのまま使用します。 この手順では、ワーカーロールをソリューションに追加します。 **[OK]** をクリックします。

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image4.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image3.png)

作成される Visual Studio ソリューションには、次の2つのプロジェクトが含まれます。

- AzureApp&quot; &quot;Azure アプリケーションのロールと構成を定義します。
- &quot;WorkerRole1&quot; には、ワーカーロールのコードが含まれています。

一般に、Azure アプリケーションには複数のロールを含めることができますが、このチュートリアルでは1つのロールを使用します。

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image5.png)

## <a name="add-the-web-api-and-owin-packages"></a>Web API と OWIN パッケージを追加する

**[ツール]** メニューの **[NuGet パッケージマネージャー]** をクリックし、 **[パッケージマネージャーコンソール]** をクリックします。

[パッケージ マネージャー コンソール] ウィンドウで、次のコマンドを入力します。

[!code-console[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample1.cmd)]

## <a name="add-an-http-endpoint"></a>HTTP エンドポイントを追加する

ソリューションエクスプローラーで、AzureApp プロジェクトを展開します。 ロール ノードを展開し、WorkerRole1 を右クリックして、**プロパティ** を選択します。

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image6.png)

**[エンドポイント]** をクリックして、 **[エンドポイントの追加]** をクリックします。

**プロトコル** ドロップダウンリストで、http を選択します。 **[パブリックポート]** と **[プライベートポート]** に、「80」と入力します。 このポート番号は別の番号でもかまいません。 パブリックポートは、クライアントがロールに要求を送信するときに使用されます。

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image8.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image7.png)

## <a name="configure-web-api-for-self-host"></a>セルフホスト用に Web API を構成する

ソリューションエクスプローラーで、WorkerRole1 プロジェクトを右クリックし、[ / **クラス**の**追加**] を選択して新しいクラスを追加します。 クラスに `Startup` という名前を付けます。

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image9.png)

このファイルの定型コードをすべて次のコードに置き換えます。

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample2.cs)]

## <a name="add-a-web-api-controller"></a>Web API コントローラーを追加する

次に、Web API コントローラークラスを追加します。 WorkerRole1 プロジェクトを右クリックし、[ / **クラス**の**追加**] を選択します。 クラスに TestController という名前を指定します。 このファイルの定型コードをすべて次のコードに置き換えます。

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample3.cs)]

わかりやすくするために、このコントローラーでは、プレーンテキストを返す2つの GET メソッドを定義しています。

## <a name="start-the-owin-host"></a>OWIN ホストを開始する

WorkerRole.cs ファイルを開きます。 このクラスは、ワーカーロールが開始および停止したときに実行されるコードを定義します。

次の using ステートメントを追加します。

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample4.cs)]

`WorkerRole` クラスに**IDisposable**メンバーを追加します。

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample5.cs)]

`OnStart` メソッドで、次のコードを追加してホストを起動します。

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample6.cs?highlight=5)]

**WebApp**メソッドは、OWIN ホストを開始します。 `Startup` クラスの名前は、メソッドの型パラメーターです。 慣例により、ホストはこのクラスの `Configure` メソッドを呼び出します。

*\_アプリ*インスタンスを破棄するには、`OnStop` をオーバーライドします。

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample7.cs)]

WorkerRole.cs の完全なコードを次に示します。

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample8.cs)]

ソリューションをビルドし、F5 キーを押して、Azure コンピューティングエミュレーターでアプリケーションをローカルに実行します。 ファイアウォールの設定によっては、エミュレーターでのファイアウォールの使用を許可することが必要になる場合があります。

> [!NOTE]
> 次のような例外が発生した場合は、こちらの[ブログ投稿](https://blogs.msdn.com/b/praburaj/archive/2013/11/20/fileloadexception-on-microsoft-owin-when-running-on-worker-role.aspx)で回避策をご覧ください。 "ファイルまたはアセンブリ ' Owin, Version = 2.0.2.0, Culture = ニュートラル, PublicKeyToken = 31bf3856ad364e35 ' またはその依存関係の1つが読み込めませんでした。 見つかったアセンブリのマニフェスト定義がアセンブリ参照と一致しません。 (HRESULT からの例外: 0x80131040) "

コンピューティングエミュレーターは、エンドポイントにローカル IP アドレスを割り当てます。 IP アドレスを見つけるには、コンピューティングエミュレーターの UI を表示します。 タスクバーの通知領域のエミュレーターアイコンを右クリックし、 **[コンピューティングエミュレーター UI の表示]** を選択します。

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image11.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image10.png)

サービスの展開で、サービスの詳細情報の展開 [id]、IP アドレスを検索します。 Web ブラウザーを開き、 http://<em>address</em>/test/1 に移動します。ここで、 <em>address</em>はコンピューティングエミュレーターによって割り当てられた IP アドレスです。たとえば、`http://127.0.0.1:80/test/1`のようにします。 Web API コントローラーからの応答が表示されます。

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image12.png)

## <a name="deploy-to-azure"></a>Deploy to Azure (Azure へのデプロイ)

この手順では、Azure アカウントが必要です。 まだお持ちでない場合は、無料試用版アカウントを数分で作成できます。 詳細については、「 [Microsoft Azure 無料試用版](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)」を参照してください。

ソリューションエクスプローラーで、AzureApp プロジェクトを右クリックします。 **[発行]** を選択します。

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image13.png)

Azure アカウントにサインインしていない場合は、 **[サインイン]** をクリックします。

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image15.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image14.png)

サインインしたら、サブスクリプションを選択し、 **[次へ]** をクリックします。

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image17.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image16.png)

クラウドサービスの名前を入力し、リージョンを選択します。 **Create** をクリックしてください。

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image18.png)

**[発行]** をクリックします。

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image20.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image19.png)

[Azure のアクティビティログ] ウィンドウに、デプロイの進行状況が表示されます。 アプリがデプロイされたら、 http://appname.cloudapp.net/test/1に移動します。

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image21.png)

## <a name="additional-resources"></a>その他のリソース

- [プロジェクト Katana の概要](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)
- [GitHub の Katana プロジェクト](https://github.com/aspnet/AspNetKatana)
