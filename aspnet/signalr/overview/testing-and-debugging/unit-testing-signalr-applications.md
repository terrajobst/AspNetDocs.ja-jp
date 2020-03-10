---
uid: signalr/overview/testing-and-debugging/unit-testing-signalr-applications
title: SignalR Applications の単体テスト |Microsoft Docs
author: bradygaster
description: この記事では、SignalR 2.0 の単体テスト機能を使用する方法について説明します。
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: d1983524-e0d5-4ee6-9d87-1f552f7cb964
msc.legacyurl: /signalr/overview/testing-and-debugging/unit-testing-signalr-applications
msc.type: authoredcontent
ms.openlocfilehash: 2cf2e88f141d89971439dc1fc4979849f8dded47
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467302"
---
# <a name="unit-testing-signalr-applications"></a>SignalR アプリケーションの単体テスト

([パトリック Fletcher](https://github.com/pfletcher) )

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> この記事では、SignalR 2 の単体テスト機能の使用方法について説明します。
>
> ## <a name="software-versions-used-in-this-topic"></a>このトピックで使用されているソフトウェアのバージョン
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - .NET 4.5
> - SignalR バージョン2
>
>
>
> ## <a name="questions-and-comments"></a>質問とコメント
>
> このチュートリアルの良い点に関するフィードバックや、ページ下部にあるコメントで改善できる点をお知らせください。 チュートリアルに直接関係のない質問がある場合は、 [ASP.NET SignalR フォーラム](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)または[StackOverflow.com](http://stackoverflow.com/)に投稿できます。

<a id="unit"></a>
## <a name="unit-testing-signalr-applications"></a>SignalR アプリケーションの単体テスト

SignalR 2 の単体テスト機能を使用して、SignalR アプリケーションの単体テストを作成できます。 SignalR 2 には[IHubCallerConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.ihubcallerconnectioncontext(v=vs.118).aspx)インターフェイスが含まれています。このインターフェイスを使用して、テスト用のハブメソッドをシミュレートするモックオブジェクトを作成できます。

このセクションでは、 [XUnit.net](https://github.com/xunit/xunit)と[moq](https://github.com/Moq/moq4)を使用して[はじめにチュートリアル](../getting-started/tutorial-getting-started-with-signalr.md)で作成したアプリケーションの単体テストを追加します。

XUnit.net は、テストを制御するために使用されます。Moq は、テスト用の[モック](http://en.wikipedia.org/wiki/Mock_object)オブジェクトを作成するために使用されます。 必要に応じて、他のモックフレームワークを使用することもできます。また、 [Nsubstitute](http://nsubstitute.github.io/)も選択することをお勧めします。 このチュートリアルでは、2つの方法でモックオブジェクトを設定する方法について説明します。最初に、`dynamic` オブジェクト (.NET Framework 4 で導入) を使用し、2つ目にインターフェイスを使用します。

### <a name="contents"></a>内容

このチュートリアルは、次のセクションで構成されています。

- [動的な単体テスト](#dynamic)
- [種類別の単体テスト](#type)

<a id="dynamic"></a>
### <a name="unit-testing-with-dynamic"></a>動的な単体テスト

このセクションでは、[はじめにチュートリアル](../getting-started/tutorial-getting-started-with-signalr.md)で作成したアプリケーションの単体テストを動的オブジェクトを使用して追加します。

1. Visual Studio 2013 用の[Xunit ランナー拡張機能](https://visualstudiogallery.msdn.microsoft.com/463c5987-f82b-46c8-a97e-b1cde42b9099)をインストールします。
2. [はじめにチュートリアル](../getting-started/tutorial-getting-started-with-signalr.md)を完了するか、 [MSDN コードギャラリー](https://code.msdn.microsoft.com/SignalR-Getting-Started-b9d18aa9)から完成したアプリケーションをダウンロードします。
3. ダウンロードバージョンのはじめにアプリケーションを使用している場合は、**パッケージマネージャーコンソール**を開き、 **[復元]** をクリックして SignalR パッケージをプロジェクトに追加します。

    ![パッケージの復元](unit-testing-signalr-applications/_static/image1.png)
4. 単体テストのソリューションにプロジェクトを追加します。 **ソリューションエクスプローラー**でソリューションを右クリックし、 **[追加]** 、 **[新しいプロジェクト...]** の順に選択します。**C#** ノードの下で、 **[Windows]** ノードを選択します。 **[クラスライブラリ]** を選択します。 新しいプロジェクトに**Testlibrary**という名前を指定し、[ **OK]** をクリックします。

    ![テストライブラリの作成](unit-testing-signalr-applications/_static/image2.png)
5. テストライブラリプロジェクトで、SignalRChat プロジェクトに参照を追加します。 **Testlibrary**プロジェクトを右クリックし、 **[追加]** 、 **[参照]** の順に選択します。**ソリューション**ノードの下にある **[プロジェクト]** ノードを選択し、 **[signalrchat]** をオンにします。 **[OK]** をクリックします。

    ![プロジェクト参照の追加](unit-testing-signalr-applications/_static/image3.png)
6. SignalR、Moq、および XUnit パッケージを**Testlibrary**プロジェクトに追加します。 **パッケージマネージャーコンソール**で、既定の **[プロジェクト]** ドロップダウンを **[testlibrary]** に設定します。 コンソールウィンドウで、次のコマンドを実行します。

   - `Install-Package Microsoft.AspNet.SignalR`
   - `Install-Package Moq`
   - `Install-Package XUnit`

     ![パッケージのインストール](unit-testing-signalr-applications/_static/image4.png)
7. テストファイルを作成します。 **Testlibrary**プロジェクトを右クリックし、 **[追加]** 、 **[クラス]** の順にクリックします。 新しいクラスに**Tests.cs**という名前を指定します。
8. Tests.cs の内容を次のコードに置き換えます。

    [!code-csharp[Main](unit-testing-signalr-applications/samples/sample1.cs)]

    上記のコードでは、 [IHubCallerConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.ihubcallerconnectioncontext(v=vs.118).aspx)型の[moq](https://github.com/Moq/moq4)ライブラリの `Mock` オブジェクトを使用してテストクライアントが作成されます (SignalR 2.1 では、型パラメーターに `dynamic` を割り当てます)。`IHubCallerConnectionContext` インターフェイスは、クライアントでメソッドを呼び出すためのプロキシオブジェクトです。 その後、`broadcastMessage` 関数がモッククライアントに対して定義され、`ChatHub` クラスから呼び出すことができるようになります。 次に、テストエンジンは、`ChatHub` クラスの `Send` メソッドを呼び出します。このメソッドはモック `broadcastMessage` 関数を呼び出します。
9. **F6**キーを押してソリューションをビルドします。
10. 単体テストを実行します。 Visual Studio で、 **[テスト]** 、 **[Windows]** 、 **[テストエクスプローラー]** の順番に選択します。 テストエクスプローラー ウィンドウで、 **HubsAreMockableViaDynamic** を右クリックし、**選択したテストの実行** を選択します。

    ![テスト エクスプローラー](unit-testing-signalr-applications/_static/image5.png)
11. [テストエクスプローラー] ウィンドウの下側のペインで、テストが成功したことを確認します。 テストが成功したことがウィンドウに表示されます。

    ![テスト成功](unit-testing-signalr-applications/_static/image6.png)

<a id="type"></a>
### <a name="unit-testing-by-type"></a>種類別の単体テスト

このセクションでは、[はじめにチュートリアル](../getting-started/tutorial-getting-started-with-signalr.md)で作成したアプリケーションのテストを、テスト対象のメソッドを含むインターフェイスを使用して追加します。

1. 前の「動的チュートリアル[を使用した単体テスト](#dynamic)」の手順1-7 を実行します。
2. Tests.cs の内容を次のコードに置き換えます。

    [!code-csharp[Main](unit-testing-signalr-applications/samples/sample2.cs)]

    上記のコードでは、テストエンジンがモッククライアントを作成するための `broadcastMessage` メソッドのシグネチャを定義するインターフェイスが作成されます。 モッククライアントは、 [IHubCallerConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.ihubcallerconnectioncontext(v=vs.118).aspx)型の `Mock` オブジェクトを使用して作成されます (SignalR 2.1 では、型パラメーターに `dynamic` を割り当てます)。`IHubCallerConnectionContext` インターフェイスは、クライアントでメソッドを呼び出すためのプロキシオブジェクトです。

    次に、`ChatHub`のインスタンスを作成し、`broadcastMessage` メソッドのモックバージョンを作成します。これは、ハブで `Send` メソッドを呼び出すことによって呼び出されます。
3. **F6**キーを押してソリューションをビルドします。
4. 単体テストを実行します。 Visual Studio で、 **[テスト]** 、 **[Windows]** 、 **[テストエクスプローラー]** の順番に選択します。 テストエクスプローラー ウィンドウで、 **HubsAreMockableViaDynamic** を右クリックし、**選択したテストの実行** を選択します。

    ![テスト エクスプローラー](unit-testing-signalr-applications/_static/image7.png)
5. [テストエクスプローラー] ウィンドウの下側のペインで、テストが成功したことを確認します。 テストが成功したことがウィンドウに表示されます。

    ![テスト成功](unit-testing-signalr-applications/_static/image8.png)
