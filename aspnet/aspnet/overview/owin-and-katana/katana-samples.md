---
uid: aspnet/overview/owin-and-katana/katana-samples
title: Katana Samples |Microsoft Docs
author: microsoft
description: ''
ms.author: riande
ms.date: 01/17/2014
ms.assetid: bec04f5d-2638-4417-b288-97c58c8d6379
msc.legacyurl: /aspnet/overview/owin-and-katana/katana-samples
msc.type: authoredcontent
ms.openlocfilehash: 1238f7d09492a6856d49dece5de75184ccfa4838
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78472348"
---
# <a name="katana-samples"></a>Katana サンプル

[Microsoft](https://github.com/microsoft)

## <a name="katana-samples"></a>Katana サンプル

**ASP.NET Route サンプル** | [ソースコード](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/AspNetRoutes)  
一部のアプリケーションでは、非 OWIN コンポーネントと共に、ASP.NET ルート テーブル内の OWIN コンポーネントをフックするでしょう。 このサンプルでは、Owin によって提供される RouteCollection 拡張メソッド Mアポストロフィ Winpath と Mアポストロフィ Winroute の使用方法を示します。

**パイプラインの分岐サンプル** | [ソースコード](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/BranchingPipelines)  
OWIN 要求処理パイプラインは、線形である必要はありません。分岐して、さまざまな方法で要求を処理することができます。 このサンプルでは、要求パスまたはその他の要求データ (ヘッダーなど) に基づいて分岐パイプラインを構築する方法を示します。 これらのコンポーネントは、Owin nuget パッケージで入手できます。

**カスタムサーバーサンプル** | [ソースコード](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/CustomServer)   
自己ホスト OWIN の場合にカスタム OWIN サーバーを使用する方法を示します。

**埋め込みサンプル** | [ソースコード](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/Embedded)  
一部の OWIN サーバーは、独自のプロセス内で実行できます (&quot;自己ホスト型&quot;)。 このサンプルでは、Owin nuget パッケージによって提供されるツールを使用して OWIN アプリケーションを起動する方法を示します。

**HelloWorld サンプル** | [ソースコード](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorld)  
OWIN は、さまざまなサーバー間でのアプリケーションの移植性を実現する HTTP サーバー API の抽象化です。 このサンプルでは、未加工の OWIN 抽象化に関するいくつかの**単純なラッパー**を使用して Hello World アプリケーションを作成し、ASP.NET などの web サーバーで実行する方法を示します。

**Hello World RAW OWIN サンプル** | [ソースコード](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorldRawOwin)  
このサンプルでは、**未加工**の OWIN 抽象化を使用して Hello World アプリケーションを作成し、Asp.Net などの web サーバーで実行する方法を示します。

**SignalR サンプル** | [ソースコード](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/SignalR)  
OWIN/Katana を使用して SignalR を自己ホストする方法を示します。 自己ホスト SignalR の詳細については、「[チュートリアル: SignalR 自己ホスト](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)」を参照してください。

**静的ファイルのサンプル** | [ソースコード](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/StaticFilesSample)   
OWIN/Katana を使用して静的ファイルの HTTP 要求をサポートする方法を示します。

**WEB API** | [ソースコード](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebApi)   
このサンプルでは、IIS で OWIN をホストし、Web API を OWIN パイプラインに追加する方法を示します。

**Web Socket サンプル** | [ソースコード](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebSocketSample)   
OWIN クラスを使用して、Web ソケットをサポートする方法を示し[ます。](https://msdn.microsoft.com/library/system.net.websockets.websocket(v=vs.110).aspx)
