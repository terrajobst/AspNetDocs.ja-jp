---
uid: web-api/overview/older-versions/self-host-a-web-api
title: 自己ホスト ASP.NET Web API 1 (C#)-ASP.NET 4.x
author: MikeWasson
description: コードを使用したチュートリアルでは、コンソールアプリケーション内で web API をホストする方法を示します。
ms.author: riande
ms.date: 01/26/2012
ms.custom: seoapril2019
ms.assetid: be5ab1e2-4140-4275-ac59-ca82a1bac0c1
msc.legacyurl: /web-api/overview/older-versions/self-host-a-web-api
msc.type: authoredcontent
ms.openlocfilehash: bae1737ba5b16bc67fa0ed0474ff04df0add1b3a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78421372"
---
# <a name="self-host-aspnet-web-api-1-c"></a>自己ホスト ASP.NET Web API 1 (C#)

[Mike Wasson](https://github.com/MikeWasson)

> このチュートリアルでは、コンソールアプリケーション内で web API をホストする方法について説明します。 ASP.NET Web API には IIS は必要ありません。 独自のホストプロセスで web API を自己ホストすることができます。 
> 
> **新しいアプリケーションでは、OWIN を使用して Web API をセルフホストする必要があります。** 「 [USE OWIN To Self Host ASP.NET Web API 2」を](../hosting-aspnet-web-api/use-owin-to-self-host-web-api.md)参照してください。
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>このチュートリアルで使用されているソフトウェアのバージョン
> 
> 
> - Web API 1
> - Visual Studio 2012

## <a name="create-the-console-application-project"></a>コンソールアプリケーションプロジェクトを作成する

Visual Studio を起動し、**スタート**ページで **[新しいプロジェクト]** を選択します。 または、 **[ファイル]** メニューの **[新規作成]** をポイントし、 **[プロジェクト]** をクリックします。

**[テンプレート]** ペインで、 **[インストールされたテンプレート]** を選択し、  **C#ビジュアル**ノードを展開します。 **[ビジュアルC# ]** で、 **[Windows]** を選択します。 プロジェクトテンプレートの一覧で、 **[コンソールアプリケーション]** を選択します。 プロジェクトに SelfHost Host &quot;という名前を指定し、[ **OK]** をクリックします。&quot;

![](self-host-a-web-api/_static/image1.png)

## <a name="set-the-target-framework-visual-studio-2010"></a>ターゲットフレームワークを設定する (Visual Studio 2010)

Visual Studio 2010 を使用している場合は、ターゲットフレームワークを .NET Framework 4.0 に変更します。 (既定では、プロジェクトテンプレートは[.Net Framework Client Profile](https://msdn.microsoft.com/library/cc656912.aspx#features_not_included_in_the_net_framework_client_profile)を対象としています)。

ソリューションエクスプローラーで、プロジェクトを右クリックし、 **[プロパティ]** を選択します。 **ターゲットフレームワーク** ドロップダウンリストで、ターゲットフレームワーク を .NET Framework 4.0 に変更します。 変更を適用するように求めるメッセージが表示されたら、[**はい]** をクリックします。

![](self-host-a-web-api/_static/image2.png)

## <a name="install-nuget-package-manager"></a>NuGet パッケージマネージャーのインストール

NuGet パッケージマネージャーは、non-ASP.NET プロジェクトに Web API アセンブリを追加する最も簡単な方法です。

NuGet パッケージマネージャーがインストールされているかどうかを確認するには、Visual Studio の **[ツール]** メニューをクリックします。 **Nuget パッケージマネージャー**というメニュー項目が表示された場合は、Nuget パッケージマネージャーがあります。

NuGet パッケージマネージャーをインストールするには:

1. Visual Studio を起動します。
2. **[ツール]** メニューの **[拡張機能と更新プログラム]** を選択します。
3. **[拡張機能と更新プログラム]** ダイアログで、 **[オンライン]** を選択します。
4. "NuGet パッケージマネージャー" が表示されない場合は、検索ボックスに「nuget package manager」と入力します。
5. NuGet パッケージマネージャーを選択し、 **[ダウンロード]** をクリックします。
6. ダウンロードが完了すると、をインストールするように求められます。
7. インストールが完了すると、Visual Studio を再起動するように求められる場合があります。

![](self-host-a-web-api/_static/image3.png)

## <a name="add-the-web-api-nuget-package"></a>Web API NuGet パッケージを追加する

NuGet パッケージマネージャーがインストールされたら、Web API の自己ホストパッケージをプロジェクトに追加します。

1. **[ツール]** メニューの **[NuGet パッケージマネージャー]** をクリックします。 *注*: このメニュー項目が表示されない場合は、NuGet パッケージマネージャーが正しくインストールされていることを確認してください。
2. **[ソリューションの NuGet パッケージの管理]** を選択します。
3. **[NugGet パッケージの管理]** ダイアログボックスで、 **[オンライン]** を選択します。
4. 検索ボックスに、「&quot;WebApi&quot;」と入力します。
5. ASP.NET Web API セルフホストパッケージを選択し、 **[インストール]** をクリックします。
6. パッケージがインストールされたら、 **[閉じる]** をクリックしてダイアログボックスを閉じます。

> [!NOTE]
> AspNetWebApi ではなく、WebApi という名前のパッケージを必ずインストールしてください。

![](self-host-a-web-api/_static/image4.png)

## <a name="create-the-model-and-controller"></a>モデルとコントローラーを作成する

このチュートリアルでは、[はじめに](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)チュートリアルと同じモデルとコントローラークラスを使用します。

`Product`という名前のパブリッククラスを追加します。

[!code-csharp[Main](self-host-a-web-api/samples/sample1.cs)]

`ProductsController`という名前のパブリッククラスを追加します。 このクラスを**ApiController**から派生させます。

[!code-csharp[Main](self-host-a-web-api/samples/sample2.cs)]

このコントローラーのコードの詳細については、[はじめに](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)チュートリアルを参照してください。 このコントローラーは、次の3つの GET アクションを定義します。

| URI | Description |
| --- | --- |
| /api/products | すべての製品の一覧を取得します。 |
| /api/*id* | ID で製品を取得します。 |
| //カテゴリ =*カテゴリ* | カテゴリ別に製品の一覧を取得します。 |

## <a name="host-the-web-api"></a>Web API をホストする

Program.cs ファイルを開き、次の using ステートメントを追加します。

[!code-csharp[Main](self-host-a-web-api/samples/sample3.cs)]

**Program**クラスに次のコードを追加します。

[!code-csharp[Main](self-host-a-web-api/samples/sample4.cs)]

## <a name="optional-add-an-http-url-namespace-reservation"></a>OptionalHTTP URL 名前空間の予約を追加する

このアプリケーションは `http://localhost:8080/`をリッスンします。 既定では、特定の HTTP アドレスでリッスンするには、管理者特権が必要です。 このチュートリアルを実行すると、次のエラーが表示されることがあります。 "HTTP は URL http://+:8080/を登録できませんでした。このエラーを回避する方法は2つあります。

- 管理者特権で Visual Studio を実行します。または、
- Netsh.exe を使用して、アカウントに URL を予約するアクセス許可を付与します。

Netsh.exe を使用するには、管理者特権でコマンドプロンプトを開き、次のコマンドを入力します。コマンド:

[!code-console[Main](self-host-a-web-api/samples/sample5.cmd)]

ここで、 *machine\username など*はユーザーアカウントです。

自己ホストを完了したら、予約を削除してください。

[!code-console[Main](self-host-a-web-api/samples/sample6.cmd)]

## <a name="call-the-web-api-from-a-client-application-c"></a>クライアントアプリケーションから Web API を呼び出す (C#)

ここでは、web API を呼び出す簡単なコンソールアプリケーションを作成します。

新しいコンソールアプリケーションプロジェクトをソリューションに追加します。

- ソリューションエクスプローラーで、ソリューションを右クリックし、 **[新しいプロジェクトの追加]** を選択します。
- &quot;ClientApp&quot;という名前の新しいコンソールアプリケーションを作成します。

![](self-host-a-web-api/_static/image5.png)

NuGet パッケージマネージャーを使用して ASP.NET Web API コアライブラリパッケージを追加します。

- ツール メニューの  **NuGet パッケージマネージャー** をクリックします。
- **[ソリューションの NuGet パッケージの管理]** を選択します。
- **[NuGet パッケージの管理]** ダイアログで、 **[オンライン]** を選択します。
- 検索ボックスに、「&quot;WebApi&quot;」と入力します。
- Microsoft ASP.NET Web API クライアントライブラリパッケージを選択し、 **[インストール]** をクリックします。

ClientApp に参照を SelfHost プロジェクトに追加します。

- ソリューションエクスプローラーで、ClientApp プロジェクトを右クリックします。
- **[参照の追加]** をクリックします。
- **[参照マネージャー]** ダイアログボックスの **[ソリューション]** で、 **[プロジェクト]** を選択します。
- SelfHost プロジェクトを選択します。
- **[OK]** をクリックします。

![](self-host-a-web-api/_static/image6.png)

クライアント/プログラム .cs ファイルを開きます。 次の **using** ステートメントを追加します。

[!code-csharp[Main](self-host-a-web-api/samples/sample7.cs)]

静的**Httpclient**インスタンスを追加します。

[!code-csharp[Main](self-host-a-web-api/samples/sample8.cs)]

すべての製品を一覧表示し、ID で製品を一覧表示し、カテゴリ別に製品を一覧表示するには、次のメソッドを追加します。

[!code-csharp[Main](self-host-a-web-api/samples/sample9.cs)]

これらの各メソッドは、同じパターンに従います。

1. GET 要求を適切な URI に送信するには、 **Httpclient**を呼び出します。
2. **HttpResponseMessage EnsureSuccessStatusCode**を呼び出します。 このメソッドは、HTTP 応答の状態がエラーコードの場合に例外をスローします。
3. **Readasasync&lt;t&gt;** を呼び出して、HTTP 応答から CLR 型を逆シリアル化します。 このメソッドは、**システムの .net. HttpContentExtensions**で定義されている拡張メソッドです。

**GetAsync**メソッドと**readasasync**メソッドは両方とも非同期です。 これらは、非同期操作を表す**タスク**オブジェクトを返します。 **Result**プロパティを取得すると、操作が完了するまでスレッドがブロックされます。

非ブロッキング呼び出しを行う方法など、HttpClient の使用方法の詳細については、「 [.Net クライアントからの WEB API の呼び出し](../advanced/calling-a-web-api-from-a-net-client.md)」を参照してください。

これらのメソッドを呼び出す前に、HttpClient インスタンスの BaseAddress プロパティを "`http://localhost:8080`" に設定します。 次に例を示します。

[!code-csharp[Main](self-host-a-web-api/samples/sample10.cs)]

これにより、次のように出力されます。 (最初に SelfHost アプリケーションを実行してください)。

[!code-console[Main](self-host-a-web-api/samples/sample11.cmd)]

![](self-host-a-web-api/_static/image7.png)
