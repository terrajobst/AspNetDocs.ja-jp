---
uid: web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api
title: OWIN を使用して自己ホスト ASP.NET Web API-ASP.NET 4.x
author: rick-anderson
description: コンソールアプリケーションで ASP.NET Web API をホストする方法を示すコードを使用したチュートリアルです。
ms.author: riande
ms.date: 07/09/2013
ms.custom: seoapril2019
ms.assetid: a90a04ce-9d07-43ad-8250-8a92fb2bd3d5
msc.legacyurl: /web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api
msc.type: authoredcontent
ms.openlocfilehash: 872b931391a63ef82b96e5b264c070c0b5e9605d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448330"
---
# <a name="use-owin-to-self-host-aspnet-web-api"></a>OWIN を使用して自己ホスト ASP.NET Web API 

> このチュートリアルでは、OWIN を使用して Web API フレームワークをセルフホストするコンソールアプリケーションで ASP.NET Web API をホストする方法について説明します。
>
> [Open Web Interface for .net](http://owin.org) (OWIN) は、.net web サーバーと web アプリケーションの間の抽象化を定義します。 OWIN は、サーバーから web アプリケーションを分離します。これにより、IIS の外部にある独自のプロセスで web アプリケーションを自己ホストするために OWIN が理想的になります。
>
> ## <a name="software-versions-used-in-the-tutorial"></a>このチュートリアルで使用されているソフトウェアのバージョン
>
>
> - [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) 
> - Web API 5.2.7

> [!NOTE]
> このチュートリアルの完全なソースコードについては、 [github.com/aspnet/samples](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/OwinSelfhostSample)を参照してください。

## <a name="create-a-console-application"></a>コンソール アプリケーションの作成

**[ファイル]** メニューの **[新規作成]** をポイントし、 **[プロジェクト]** を選択します。 **インストールされている**から、 **[ビジュアルC# ]** の下で **[Windows デスクトップ]** を選択し、 **[コンソールアプリ (.net Framework)]** を選択します。 プロジェクトに "OwinSelfhostSample" という名前を指定し、[ **OK]** を選択します。

[![](use-owin-to-self-host-web-api/_static/image7.png)](use-owin-to-self-host-web-api/_static/image7.png)

## <a name="add-the-web-api-and-owin-packages"></a>Web API と OWIN パッケージを追加する

**[ツール]** メニューの **[NuGet パッケージマネージャー]** を選択し、 **[パッケージマネージャーコンソール]** を選択します。 [パッケージ マネージャー コンソール] ウィンドウで、次のコマンドを入力します。

`Install-Package Microsoft.AspNet.WebApi.OwinSelfHost`

これにより、WebAPI OWIN selfhost パッケージと、必要なすべての OWIN パッケージがインストールされます。

[![](use-owin-to-self-host-web-api/_static/image4.png)](use-owin-to-self-host-web-api/_static/image3.png)

## <a name="configure-web-api-for-self-host"></a>セルフホスト用に Web API を構成する

ソリューションエクスプローラーで、プロジェクトを右クリックし、[ / **クラス**の**追加**] を選択して新しいクラスを追加します。 クラスに `Startup` という名前を付けます。

![](use-owin-to-self-host-web-api/_static/image5.png)

このファイルの定型コードをすべて次のコードに置き換えます。

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample1.cs)]

## <a name="add-a-web-api-controller"></a>Web API コントローラーを追加する

次に、Web API コントローラークラスを追加します。 ソリューションエクスプローラーで、プロジェクトを右クリックし、[ / **クラス**の**追加**] を選択して新しいクラスを追加します。 クラスに `ValuesController` という名前を付けます。

このファイルの定型コードをすべて次のコードに置き換えます。

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample2.cs)]

## <a name="start-the-owin-host-and-make-a-request-with-httpclient"></a>OWIN ホストを起動し、HttpClient で要求を行う

Program.cs ファイル内のすべての定型コードを次のコードに置き換えます。

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample3.cs)]

## <a name="run-the-application"></a>アプリケーションの実行

アプリケーションを実行するには、Visual Studio で F5 キーを押します。 出力は次のようになります。

[!code-console[Main](use-owin-to-self-host-web-api/samples/sample4.cmd)]

![](use-owin-to-self-host-web-api/_static/image6.png)

## <a name="additional-resources"></a>その他のリソース

[プロジェクト Katana の概要](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)

[Azure Worker ロールでのホスト ASP.NET Web API](host-aspnet-web-api-in-an-azure-worker-role.md)
