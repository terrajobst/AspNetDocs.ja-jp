---
uid: aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana
title: OWIN と Katana | を使用したはじめにMicrosoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 09/27/2013
ms.assetid: 6dae249f-5ac6-4f6e-bc49-13bcd5a54a70
msc.legacyurl: /aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana
msc.type: authoredcontent
ms.openlocfilehash: 4dfd7b8ebb2bb48d7ef800fd522b79a7b4a045c2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78472444"
---
# <a name="getting-started-with-owin-and-katana"></a>OWIN と Katana の概要

[Mike Wasson](https://github.com/MikeWasson)

[Open Web Interface for .net (OWIN)](http://owin.org/)は、.net web サーバーと web アプリケーションの間の抽象化を定義します。 OWIN を使用すると、web サーバーをアプリケーションから分離することで、.NET web 開発用のミドルウェアを簡単に作成できます。 また、OWIN を使用すると、Windows サービスやその他&#8212;のプロセスでの自己ホストなど、web アプリケーションを他のホストに移植しやすくなります。

OWIN は、実装ではなく、コミュニティ所有の仕様です。 Katana プロジェクトは、Microsoft によって開発されたオープンソースの OWIN コンポーネントのセットです。 OWIN と Katana の両方の概要については、「 [Project Katana の概要](an-overview-of-project-katana.md)」を参照してください。 この記事では、作業を開始するためにコードにすぐに進みます。

このチュートリアルでは[Visual Studio 2013 リリース候補](https://go.microsoft.com/fwlink/?LinkId=306566)を使用しますが、Visual Studio 2012 を使用することもできます。 いくつかの手順は Visual Studio 2012 では異なりますが、以下の点に注意してください。

## <a name="host-owin-in-iis"></a>IIS でのホスト OWIN

このセクションでは、IIS で OWIN をホストします。 このオプションを使用すると、OWIN パイプラインの柔軟性と省かが、IIS の成熟した機能セットと共に得られます。 このオプションを使用すると、OWIN アプリケーションは ASP.NET request パイプラインで実行されます。

最初に、新しい ASP.NET Web アプリケーションプロジェクトを作成します。 (Visual Studio 2012 では、ASP.NET 空の Web アプリケーションプロジェクトの種類を使用します。)

![](getting-started-with-owin-and-katana/_static/image1.png)

**[New ASP.NET Project]** ダイアログボックスで、**空**のテンプレートを選択します。

![](getting-started-with-owin-and-katana/_static/image2.png)

### <a name="add-nuget-packages"></a>NuGet パッケージを追加します。

次に、必要な NuGet パッケージを追加します。 **[ツール]** メニューの **[NuGet パッケージマネージャー]** を選択し、 **[パッケージマネージャーコンソール]** を選択します。 [パッケージマネージャーコンソール] ウィンドウで、次のコマンドを入力します。

`install-package Microsoft.Owin.Host.SystemWeb –Pre`

![](getting-started-with-owin-and-katana/_static/image3.png)

### <a name="add-a-startup-class"></a>Startup クラスを追加する

次に、OWIN startup クラスを追加します。 ソリューションエクスプローラーで、プロジェクトを右クリックし、 **[追加]** 、 **[新しい項目]** の順に選択します。 **[新しい項目の追加]** ダイアログで、 **[Owin Startup class]** を選択します。 Startup クラスの構成の詳細については、「 [OWIN Startup Class Detection](owin-startup-class-detection.md)」を参照してください。

![](getting-started-with-owin-and-katana/_static/image4.png)

次のコードを `Startup1.Configuration` メソッドに追加します。

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample1.cs?highlight=3)]

このコードは、OWIN パイプラインに単純なミドルウェアを追加し、 **OWIN**インスタンスを受け取る関数として実装します。 サーバーが HTTP 要求を受信すると、OWIN パイプラインはミドルウェアを呼び出します。 ミドルウェアは、応答のコンテンツタイプを設定し、応答本文を書き込みます。

> [!NOTE]
> OWIN Startup クラステンプレートは、Visual Studio 2013 で使用できます。 Visual Studio 2012 を使用している場合は、`Startup1`という名前の新しい空のクラスを追加し、次のコードを貼り付けます。

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample2.cs)]

### <a name="run-the-application"></a>アプリケーションの実行

F5 キーを押してデバッグを開始します。 Visual Studio によってブラウザーウィンドウが開き、`http://localhost:*port*/`します。 ページは次のようになります。

![](getting-started-with-owin-and-katana/_static/image5.png)

## <a name="self-host-owin-in-a-console-application"></a>コンソールアプリケーションでの自己ホスト OWIN

カスタムプロセスでは、このアプリケーションを IIS ホスティングから自己ホスト型に簡単に変換できます。 Iis をホストすると、IIS は、サービスをホストするプロセスとして、HTTP サーバーとの両方として機能します。 自己ホストを使用すると、アプリケーションはプロセスを作成し、 **HttpListener**クラスを HTTP サーバーとして使用します。

Visual Studio で、新しいコンソール アプリケーションを作成します。 [パッケージマネージャーコンソール] ウィンドウで、次のコマンドを入力します。

`Install-Package Microsoft.Owin.SelfHost -Pre`

このチュートリアルのパート1の `Startup1` クラスをプロジェクトに追加します。 このクラスを変更する必要はありません。

次のように、アプリケーションの `Main` メソッドを実装します。

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample3.cs)]

コンソールアプリケーションを実行すると、サーバーは `http://localhost:9000`のリッスンを開始します。 Web ブラウザーでこのアドレスに移動すると、"Hello world" というページが表示されます。

![](getting-started-with-owin-and-katana/_static/image6.png)

## <a name="add-owin-diagnostics"></a>OWIN 診断の追加

Owin パッケージには、未処理の例外をキャッチし、エラーの詳細を示す HTML ページを表示するミドルウェアが含まれています。 このページは、"[黄色いスクリーン](http://en.wikipedia.org/wiki/Yellow_Screen_of_Death#Yellow)(YSOD)" と呼ばれることがある ASP.NET エラーページとよく似ています。 YSOD と同様、Katana エラーページは開発時に役立ちますが、運用モードで無効にすることをお勧めします。

プロジェクトに診断パッケージをインストールするには、パッケージマネージャーコンソールウィンドウで次のコマンドを入力します。

`install-package Microsoft.Owin.Diagnostics –Pre`

`Startup1.Configuration` メソッドのコードを次のように変更します。

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample4.cs?highlight=4,9-12)]

ここで、CTRL キーを押しながら F5 キーを押してデバッグなしでアプリケーションを実行し、Visual Studio が例外で中断しないようにします。 アプリケーションは前と同じように動作します。 `http://localhost/fail`に移動するまで、アプリケーションは例外をスローします。 エラーページミドルウェアは、例外をキャッチし、エラーに関する情報を含む HTML ページを表示します。 タブをクリックすると、スタック、クエリ文字列、cookie、要求ヘッダー、および OWIN 環境変数が表示されます。

![](getting-started-with-owin-and-katana/_static/image7.png)

## <a name="next-steps"></a>次の手順

- [OWIN スタートアップ クラス検出](owin-startup-class-detection.md)
- [OWIN を使用して自己ホスト ASP.NET Web API](../../../web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api.md)
- [OWIN を使用して SignalR をセルフホストする](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)
