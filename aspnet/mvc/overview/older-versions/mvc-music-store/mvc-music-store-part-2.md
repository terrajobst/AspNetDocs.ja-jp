---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-2
title: 'パート 2: コントローラー |Microsoft Docs'
author: jongalloway
description: このチュートリアルシリーズでは、ASP.NET MVC ミュージックストアサンプルアプリケーションをビルドするために実行するすべての手順について詳しく説明します。 パート2では、コントローラーについて説明します。
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 998ce4e1-9d72-435b-8f1c-399a10ae4360
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-2
msc.type: authoredcontent
ms.openlocfilehash: 9dc2226f4951d4bed122df37d35bbb94730a00ad
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78451192"
---
# <a name="part-2-controllers"></a>パート 2: コントローラー

( [Jon Galloway](https://github.com/jongalloway) )

> MVC Music Store は、ASP.NET MVC と Visual Studio を使用して web 開発を行う方法を紹介したチュートリアルアプリケーションです。  
>   
> MVC ミュージックストアは、音楽アルバムをオンラインで販売し、基本的なサイト管理、ユーザーサインイン、およびショッピングカート機能を実装する軽量のサンプルストア実装です。  
>   
> このチュートリアルシリーズでは、ASP.NET MVC ミュージックストアサンプルアプリケーションをビルドするために実行するすべての手順について詳しく説明します。 パート2では、コントローラーについて説明します。

従来の web フレームワークでは、着信 Url は通常、ディスク上のファイルにマップされます。 たとえば、"/-.Aspx" や "/" などの URL の要求は、"Products" ファイルまたは "Products. php" ファイルによって処理される場合があります。

Web ベースの MVC フレームワークでは、Url が少し異なる方法でサーバーコードにマップされます。 受信 Url をファイルにマッピングする代わりに、代わりに、Url をクラスのメソッドにマップします。 これらのクラスは "コントローラー" と呼ばれ、受信 HTTP 要求の処理、ユーザー入力の処理、データの取得と保存、クライアントに返信するための応答の決定 (HTML の表示、ファイルのダウンロード、別のファイルへのリダイレクトなど) を担当します。URL など)。

## <a name="adding-a-homecontroller"></a>HomeController の追加

サイトのホームページへの Url を処理するコントローラークラスを追加して、MVC ミュージックストアアプリケーションを開始します。 ASP.NET MVC の既定の名前付け規則に従って、HomeController を呼び出します。

ソリューションエクスプローラー内の "Controllers" フォルダーを右クリックし、[追加] をクリックして、[コントローラー...]メニュー

![](mvc-music-store-part-2/_static/image1.jpg)

これにより、[コントローラーの追加] ダイアログボックスが表示されます。 コントローラーに "HomeController" という名前を指定し、[追加] ボタンを押します。

![](mvc-music-store-part-2/_static/image1.png)

これにより、次のコードを使用して新しいファイル HomeController.cs が作成されます。

[!code-csharp[Main](mvc-music-store-part-2/samples/sample1.cs)]

できるだけ簡単に開始するために、Index メソッドを単に文字列を返す単純なメソッドに置き換えてみましょう。 次の2つの変更を行います。

- ActionResult ではなく文字列を返すようにメソッドを変更します。
- Return ステートメントを変更して "Hello from Home" を返します。

メソッドは次のようになります。

[!code-csharp[Main](mvc-music-store-part-2/samples/sample2.cs)]

## <a name="running-the-application"></a>アプリケーションの実行

では、サイトを実行してみましょう。 Web サーバーを起動して、次のいずれかを使用してサイトを試すことができます。

- [Debug ⇨ Start デバッグ] メニュー項目を選択します。
- ツールバーの緑色の矢印ボタンをクリックし ![](mvc-music-store-part-2/_static/image2.jpg)
- キーボードショートカットの F5 キーを使用します。

上記のいずれかの手順を使用すると、プロジェクトがコンパイルされ、Visual Web Developer に組み込まれている ASP.NET 開発サーバーが開始されます。 ASP.NET 開発サーバーが起動したことを示す通知が画面の下部に表示され、実行されているポート番号が表示されます。

![](mvc-music-store-part-2/_static/image2.png)

Visual Web Developer によって、Web サーバーを指す URL を持つブラウザーウィンドウが自動的に開きます。 これにより、web アプリケーションを簡単に試すことができます。

![](mvc-music-store-part-2/_static/image3.png)

これは非常に簡単でした。新しい web サイトを作成し、3行の機能を追加し、ブラウザーにテキストを追加しました。 ロケット科学はありませんが、これは始まりです。

*注: Visual Web Developer には ASP.NET 開発サーバーが含まれています。これにより、web サイトがランダムな "ポート" 番号で実行されます。上のスクリーンショットでは、サイトは `http://localhost:26641/`で実行されているので、ポート26641を使用しています。ポート番号は異なります。このチュートリアルでは、/Store/Browse のような URL について説明します。これは、ポート番号の後に移動します。ポート番号26641を指定した場合は、`http://localhost:26641/Store/Browse`を参照していることを意味します。*

## <a name="adding-a-storecontroller"></a>StoreController の追加

サイトのホームページを実装する単純な HomeController を追加しました。 ここで、音楽ストアの閲覧機能を実装するために使用する別のコントローラーを追加しましょう。 ストアコントローラーでは、次の3つのシナリオがサポートされます。

- 音楽ストアの音楽ジャンルのリストページ
- 特定のジャンルにあるすべての音楽アルバムを一覧表示する参照ページ
- 特定のミュージックアルバムに関する情報を示す詳細ページ

まず、新しい StoreController クラスを追加します。 まだ開いていない場合は、ブラウザーを閉じるか、[デバッグ] [デバッグ] [⇨の停止] メニュー項目の順に選択して、アプリケーションの実行を停止します。

次に、新しい StoreController を追加します。 HomeController の場合と同様に、この操作を行うには、ソリューションエクスプローラー内の "Controllers" フォルダーを右クリックし、[&gt;コントローラー] メニュー項目を選択します。

![](mvc-music-store-part-2/_static/image4.png)

新しい StoreController には既に "Index" メソッドがあります。 この "Index" メソッドを使用して、音楽ストア内のすべてのジャンルを一覧表示するリストページを実装します。 また、StoreController で処理する他の2つのシナリオ (参照と詳細) を実装する2つのメソッドを追加します。

コントローラー内のこれらのメソッド (インデックス、参照、および詳細) は "コントローラーアクション" と呼ばれ、HomeController () アクションメソッドで既に説明したように、ジョブは URL 要求に応答し、(一般的には) コンテンツを決定します。は、URL を呼び出したブラウザーまたはユーザーに返信する必要があります。

StoreController 実装を開始するには、theIndex () メソッドを変更して "Hello from Store. Index ()" という文字列を返します。次に、Browse () と Details () に同様のメソッドを追加します。

[!code-csharp[Main](mvc-music-store-part-2/samples/sample3.cs)]

プロジェクトを再度実行し、次の Url を参照します。

- /Store
- /ストア/参照
- ストア/詳細

これらの Url にアクセスすると、コントローラー内のアクションメソッドが呼び出され、文字列応答が返されます。

![](mvc-music-store-part-2/_static/image5.png)

これはすばらしいことですが、これらは定数文字列にすぎません。 動的なものにして、URL から情報を取得し、ページ出力に表示してみましょう。

まず、参照アクションメソッドを変更して、URL から querystring 値を取得します。 これを行うには、アクションメソッドに "genre" パラメーターを追加します。 この操作を実行すると、ASP.NET MVC は、呼び出されたときに、"genre" という名前のクエリ文字列またはフォームポストパラメーターを自動的にアクションメソッドに渡します。

[!code-csharp[Main](mvc-music-store-part-2/samples/sample4.cs)]

*メモ: HtmlEncode ユーティリティメソッドを使用して、ユーザー入力をサニタイズしています。これにより、ユーザーがビューに Javascript を挿入できなくなります。Genre =&lt;スクリプト&gt;ウィンドウ. location = 'http://hackersite.com'&lt;/script&gt;。*

次に、参照して参照してみましょう。Genre = Disco

![](mvc-music-store-part-2/_static/image6.png)

次に、[詳細] アクションを [ID] という名前の入力パラメーターを読み取って表示するように変更します。 前のメソッドとは異なり、ID 値を querystring パラメーターとして埋め込むことはできません。 代わりに、URL 自体に直接埋め込みます。 例:/Store/詳細/5。

ASP.NET MVC を使用すると、何も構成しなくても簡単にこの操作を行うことができます。 ASP.NET MVC の既定のルーティング規則では、アクションメソッド名の後の URL のセグメントを "ID" という名前のパラメーターとして扱います。 アクションメソッドに ID という名前のパラメーターがある場合、ASP.NET MVC は自動的に URL セグメントをパラメーターとして渡します。

[!code-csharp[Main](mvc-music-store-part-2/samples/sample5.cs)]

アプリケーションを実行し、次のように参照します。

![](mvc-music-store-part-2/_static/image7.png)

これまでに実行したことをまとめてみましょう。

- Visual Web Developer で新しい ASP.NET MVC プロジェクトを作成しました
- ASP.NET MVC アプリケーションの基本的なフォルダー構造について説明しました。
- ASP.NET 開発サーバーを使用して web サイトを実行する方法を学習しました
- HomeController と StoreController という2つのコントローラークラスを作成しました。
- URL 要求に応答してテキストをブラウザーに返す、コントローラーにアクションメソッドを追加しました。

> [!div class="step-by-step"]
> [前へ](mvc-music-store-part-1.md)
> [次へ](mvc-music-store-part-3.md)
