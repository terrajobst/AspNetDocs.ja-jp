---
uid: visual-studio/overview/2013/using-browser-link
title: Visual Studio 2013 | でブラウザーリンクを使用するMicrosoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 10/04/2013
ms.assetid: 46cbfe20-b4dc-449b-9016-80657dd44fbe
msc.legacyurl: /visual-studio/overview/2013/using-browser-link
msc.type: authoredcontent
ms.openlocfilehash: 723a38de4569b0bb58817c70aabb84fef8e19591
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78505204"
---
# <a name="using-browser-link-in-visual-studio-2013"></a>Visual Studio 2013 でブラウザーリンクを使用する

[Mike Wasson](https://github.com/MikeWasson)

ブラウザーリンクは、開発環境と1つ以上の web ブラウザーの間の通信チャネルを作成する Visual Studio 2013 の新機能です。 ブラウザーリンクを使用すると、複数のブラウザーで一度に web アプリケーションを更新できます。これは、ブラウザー間のテストに役立ちます。

- [ブラウザーの更新](#browser-refresh)
- [ブラウザーリンクダッシュボードの表示](#dashboard)
- [静的な HTML ファイルのブラウザーリンクを有効にする](#static-html)
- [ブラウザーリンクを無効にしています](#disabling)
- [どのように動作するのでしょうか。](#how-it-works)

<a id="browser-refresh"></a>
## <a name="browser-refresh"></a>ブラウザーの更新

ブラウザーの更新では、ブラウザーリンクを使用して Visual Studio に接続されている複数のブラウザーを更新できます。

ブラウザーの更新を使用するには、まず、プロジェクトテンプレートのいずれかを使用して ASP.NET アプリケーションを作成します。 F5 キーを押すか、ツールバーの矢印アイコンをクリックして、アプリケーションをデバッグします。

![](using-browser-link/_static/image1.png)

ドロップダウンを使用して、デバッグ用の特定のブラウザーを選択することもできます。

![](using-browser-link/_static/image2.png)

複数のブラウザーでデバッグするには、 **[参照]** を選択します。 **[参照]** ダイアログボックスで、CTRL キーを押しながら複数のブラウザーを選択します。 **[参照]** をクリックして、選択したブラウザーでデバッグします。 ブラウザーリンクは、Visual Studio の外部からブラウザーを起動し、アプリケーションの URL に移動した場合にも機能します。

![](using-browser-link/_static/image3.png)

ブラウザーリンクコントロールは、矢印アイコンが付いたドロップダウンリストにあります。 矢印アイコンは、 **[更新]** ボタンです。

![](using-browser-link/_static/image4.png)

接続されているブラウザーを確認するには、デバッグ中に **[更新]** ボタンの上にマウスポインターを置きます。 接続されているブラウザーは、ツールヒントウィンドウに表示されます。

![](using-browser-link/_static/image5.png)

接続されているブラウザーを更新するには、 **[更新]** ボタンをクリックするか、CTRL + ALT + enter キーを押します。 たとえば、次のスクリーンショットは、MVC 5 プロジェクトテンプレートを使用して作成した ASP.NET プロジェクトを示しています。 アプリケーションは、上部にある2つのブラウザーで実行されていることがわかります。 一番下には、Visual Studio でプロジェクトが開いています。

![](using-browser-link/_static/image6.png)

Visual Studio で、ホームページの &lt;h1&gt; 見出しを変更しました。

![](using-browser-link/_static/image7.png)

**[更新]** ボタンをクリックすると、両方のブラウザーウィンドウに変更が表示されます。

![](using-browser-link/_static/image8.png)

**注**

- ブラウザーリンクを有効にするには、プロジェクトの Web.config ファイルの[&lt;コンパイル&gt;](https://msdn.microsoft.com/library/s10awwz0(v=vs.85).aspx)要素に `debug=true` を設定します。
- アプリケーションが localhost で実行されている必要があります。
- アプリケーションは、.NET 4.0 以降を対象とする必要があります。

<a id="dashboard"></a>
## <a name="viewing-the-browser-link-dashboard"></a>ブラウザーリンクダッシュボードの表示

ブラウザーリンクダッシュボードには、ブラウザーリンクの接続に関する情報が表示されます。 ダッシュボードを表示するには、ブラウザーリンク ドロップダウンメニュー (**更新** ボタンの横にある小さな矢印) を選択します。 次に、 **[ブラウザーリンクダッシュボード]** をクリックします。

![](using-browser-link/_static/image9.png)

ダッシュボードには、接続されているブラウザーと、各ブラウザーがナビゲートした URL が一覧表示されます。

![](using-browser-link/_static/image10.png)

**[前提条件]** セクションには、そのプロジェクトのブラウザーリンクを有効にするために必要なすべての手順が表示されます。 たとえば、次のスクリーンショットは、web.config ファイルで "debug" が false に設定されているプロジェクトを示しています。

![](using-browser-link/_static/image11.png)

<a id="static-html"></a>
## <a name="enabling-browser-link-for-static-html-files"></a>静的な HTML ファイルのブラウザーリンクを有効にする

静的な HTML ファイルの Browser リンクを有効にするには、web.config ファイルに次のを追加します。

[!code-xml[Main](using-browser-link/samples/sample1.xml)]

パフォーマンス上の理由から、プロジェクトを発行するときにこの設定を削除します。

<a id="disabling"></a>
## <a name="disabling-browser-link"></a>ブラウザーリンクを無効にしています

ブラウザーリンクは既定で有効になっています。 無効にするには、いくつかの方法があります。

- ブラウザーのリンクのドロップダウンメニューで、 **[ブラウザーリンクを有効にする]** チェックボックスをオフにします。 

    ![](using-browser-link/_static/image12.png)
- Web.config ファイルで、appSettings セクションに "vs: EnableBrowserLink" という名前のキーを値 "false" で追加します。 

    [!code-xml[Main](using-browser-link/samples/sample2.xml)]
- Web.config ファイルで、debug を false に設定します。 

    [!code-xml[Main](using-browser-link/samples/sample3.xml)]

<a id="how-it-works"></a>
## <a name="how-does-it-work"></a>どのように動作するのでしょうか。

ブラウザーリンクは、 [SignalR](../../../signalr/index.md)を使用して、Visual Studio とブラウザーの間の通信チャネルを作成します。 ブラウザーリンクが有効になっている場合、Visual Studio は複数のクライアント (ブラウザー) が接続できる SignalR サーバーとして機能します。 ブラウザーリンクでは、HTTP モジュールを ASP.NET に登録することもできます。 このモジュールは、サーバーからのすべてのページ要求に、特別な &lt;スクリプト&gt; 参照を挿入します。 スクリプト参照を表示するには、ブラウザーで [ソースの表示] を選択します。

![](using-browser-link/_static/image13.png)

ソースファイルは変更されません。 HTTP モジュールは、スクリプト参照を動的に挿入します。

ブラウザー側のコードはすべて JavaScript であるため、 [SignalR がサポート](../../../signalr/overview/getting-started/supported-platforms.md)しているすべてのブラウザーで機能します。ブラウザープラグインは必要ありません。
