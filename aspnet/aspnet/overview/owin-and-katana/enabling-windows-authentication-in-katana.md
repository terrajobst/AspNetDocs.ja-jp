---
uid: aspnet/overview/owin-and-katana/enabling-windows-authentication-in-katana
title: Katana で Windows 認証を有効にする |Microsoft Docs
author: MikeWasson
description: この記事では、Katana で Windows 認証を有効にする方法について説明します。 この例では、IIS を使用して Katana をホストし、HttpListener を使用して自己ホスト Kat...
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 82324ef0-3b75-4f63-a217-76ef4036ec93
msc.legacyurl: /aspnet/overview/owin-and-katana/enabling-windows-authentication-in-katana
msc.type: authoredcontent
ms.openlocfilehash: 3d81e7e1bf13ab63417378fba0c5ab80213f404b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78500296"
---
# <a name="enabling-windows-authentication-in-katana"></a>Katana で Windows 認証を有効にする

[Mike Wasson](https://github.com/MikeWasson)

> この記事では、Katana で Windows 認証を有効にする方法について説明します。 この記事では、IIS を使用して Katana をホストし、HttpListener を使用してカスタムプロセスで自己ホスト Katana を使用する2つのシナリオについて説明します。 この記事を確認するには、Dorrans、David Matson、Chris Ross に感謝します。

Katana は、.NET 用の Open Web Interface である[OWIN](http://owin.org/)の Microsoft の実装です。 OWIN と Katana の概要については、[こちら](an-overview-of-project-katana.md)を参照してください。 OWIN アーキテクチャには、いくつかのレイヤーがあります。

- Host: OWIN パイプラインを実行するプロセスを管理します。
- サーバー: ネットワークソケットを開き、要求をリッスンします。
- ミドルウェア: HTTP 要求と応答を処理します。

現在、Katana には2つのサーバーがあり、どちらも Windows 統合認証をサポートしています。

- **Owin**のようになります。 IIS を ASP.NET パイプラインと共に使用します。
- **Owin. HttpListener**. [HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx)を使用します。 Katana を自己ホストする場合、このサーバーは現在既定のオプションです。

> [!NOTE]
> Katana では、現在、Windows 認証の OWIN ミドルウェアは提供されていません。この機能は既にサーバーで使用可能になっているためです。

## <a name="windows-authentication-in-iis"></a>IIS での Windows 認証

Owin を使用すると、IIS で Windows 認証を有効にすることができます。

まず、"ASP.NET Empty Web Application" プロジェクトテンプレートを使用して、新しい ASP.NET アプリケーションを作成します。

![](enabling-windows-authentication-in-katana/_static/image1.png)

次に、NuGet パッケージを追加します。 **[ツール]** メニューの **[NuGet パッケージマネージャー]** を選択し、 **[パッケージマネージャーコンソール]** を選択します。 [パッケージ マネージャー コンソール] ウィンドウで、次のコマンドを入力します。

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample1.cmd)]

ここで、次のコードを使用して、`Startup` という名前のクラスを追加します。

[!code-csharp[Main](enabling-windows-authentication-in-katana/samples/sample2.cs)]

これで、IIS で実行される OWIN 用の "Hello world" アプリケーションを作成する必要があります。 F5 キーを押してアプリケーションをデバッグします。 "Hello World!" が ブラウザーウィンドウに表示されます。

![](enabling-windows-authentication-in-katana/_static/image2.png)

次に、IIS Express で Windows 認証を有効にします。 **[表示]** メニューの **[プロパティ]** をクリックします。 プロジェクトのプロパティを表示するには、ソリューションエクスプローラーでプロジェクト名をクリックします。

**[プロパティ]** ウィンドウで、 **[匿名認証]** を **[無効]** に設定し、 **[Windows 認証]** を **[有効]** に設定します。

![](enabling-windows-authentication-in-katana/_static/image3.png)

Visual Studio からアプリケーションを実行する場合、IIS Express にはユーザーの Windows 資格情報が必要です。 これは、 [Fiddler](http://fiddler2.com/home)または別の HTTP デバッグツールを使用して確認できます。 HTTP 応答の例を次に示します。

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample3.cmd?highlight=1,5-6)]

この応答の WWW-認証ヘッダーは、サーバーが[Negotiate](http://www.ietf.org/rfc/rfc4559.txt)プロトコルをサポートしていることを示します。これは、Kerberos または NTLM のいずれかを使用します。

後で、アプリケーションをサーバーに展開するときに、[次の手順](https://www.iis.net/configreference/system.webserver/security/authentication/windowsauthentication)に従って、そのサーバー上の IIS で Windows 認証を有効にします。

## <a name="windows-authentication-in-httplistener"></a>HttpListener での Windows 認証

HttpListener を自己ホスト Katana に使用している場合は、 **HttpListener**インスタンスで Windows 認証を直接有効にすることができます。

まず、新しいコンソールアプリケーションを作成します。 次に、NuGet パッケージを追加します。 **[ツール]** メニューの **[NuGet パッケージマネージャー]** を選択し、 **[パッケージマネージャーコンソール]** を選択します。 [パッケージ マネージャー コンソール] ウィンドウで、次のコマンドを入力します。

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample4.cmd)]

ここで、次のコードを使用して、`Startup` という名前のクラスを追加します。

[!code-csharp[Main](enabling-windows-authentication-in-katana/samples/sample5.cs)]

このクラスは、以前と同じ "Hello world" の例を実装しますが、認証スキームとして Windows 認証を設定します。

`Main` 関数内で、OWIN パイプラインを開始します。

[!code-csharp[Main](enabling-windows-authentication-in-katana/samples/sample6.cs)]

Fiddler で要求を送信して、アプリケーションが Windows 認証を使用していることを確認できます。

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample7.cmd?highlight=1,4-5)]

## <a name="related-topics"></a>関連トピック

[プロジェクト Katana の概要](an-overview-of-project-katana.md)

[System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx)

[MVC 5 での OWIN フォーム認証について](https://blogs.msdn.com/b/webdev/archive/2013/07/03/understanding-owin-forms-authentication-in-mvc-5.aspx)
