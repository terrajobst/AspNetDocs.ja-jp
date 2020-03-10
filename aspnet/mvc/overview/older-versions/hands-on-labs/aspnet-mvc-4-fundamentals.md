---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-fundamentals
title: ASP.NET MVC 4 の基礎 |Microsoft Docs
author: rick-anderson
description: このハンズオンラボは、MVC (モデルビューコントローラー) の音楽ストアに基づいています。これは、ASP.NET MV の使用方法を説明するチュートリアルアプリケーションです。
ms.author: riande
ms.date: 02/18/2013
ms.assetid: b7dba543-73c3-4534-a9a0-ba70fa2c6a8a
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-fundamentals
msc.type: authoredcontent
ms.openlocfilehash: 95e9b9f55b2080c0ed01dc34e3a32f9f1c905644
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484570"
---
# <a name="aspnet-mvc-4-fundamentals"></a>ASP.NET MVC 4 の基礎

[Web キャンプチーム](https://twitter.com/webcamps)別

[Web キャンプトレーニングキットをダウンロードする](https://aka.ms/webcamps-training-kit)

このハンズオンラボは、MVC (モデルビューコントローラー) の音楽ストアに基づいています。このアプリケーションは、ASP.NET MVC と Visual Studio を使用する手順について説明するチュートリアルアプリケーションです。 ラボ全体で、シンプルさを学習しながら、これらのテクノロジを組み合わせて使用することができます。 まず、単純なアプリケーションから始めて、完全に機能する ASP.NET MVC 4 Web アプリケーションを作成します。

このラボは、ASP.NET MVC 4 で動作します。

チュートリアルアプリケーションの ASP.NET MVC 3 バージョンについては、「 [mvc-音楽-ストア](https://github.com/evilDave/MVC-Music-Store)」で確認できます。

このハンズオンラボでは、開発者が HTML や JavaScript などの Web 開発テクノロジを経験していることを前提としています。

> [!NOTE]
> すべてのサンプルコードとスニペットは、 [Microsoft web/WebCampTrainingKit リリース](https://aka.ms/webcamps-training-kit)で入手できる Web キャンプトレーニングキットに含まれています。 このラボに固有のプロジェクトについては、「 [ASP.NET MVC 4 の基礎](https://github.com/Microsoft-Web/HOL-MVC4Fundamentals)」を参照してください。

<a id="The_Music_Store_application"></a>
### <a name="the-music-store-application"></a>ミュージックストアアプリケーション

このラボ全体で構築されるミュージックストア web アプリケーションは、ショッピング、チェックアウト、管理という3つの主要な部分で構成されています。 閲覧者は、ジャンルでアルバムを参照したり、カートにアルバムを追加したり、選択内容を確認したり、最後に [ログイン] に進み、注文を完了することができます。 さらに、ストア管理者は、使用可能なアルバムとメインプロパティを管理することもできます。

![音楽ストアの画面](aspnet-mvc-4-fundamentals/_static/image1.png "音楽ストアの画面")

*音楽ストアの画面*

<a id="ASPNET_MVC_4_Essentials"></a>
### <a name="aspnet-mvc-4-essentials"></a>ASP.NET MVC 4 Essentials

ミュージックストアアプリケーションは、**モデルビューコントローラー (MVC)** を使用して構築されます。これは、アプリケーションを3つの主要なコンポーネントに分離するアーキテクチャパターンです。

- **モデル: モデル**オブジェクトは、ドメインロジックを実装するアプリケーションの一部です。 モデルオブジェクトは、多くの場合、モデルの状態を取得してデータベースに格納します。
- **ビュー:** ビューは、アプリケーションのユーザーインターフェイス (UI) を表示するコンポーネントです。 通常、この UI はモデル データから作成されます。 例としては、アルバムオブジェクトの現在の状態に基づいて、テキストボックスとドロップダウンリストを表示するアルバムの編集ビューがあります。
- **コントローラー:** コントローラーは、ユーザーの操作を処理し、モデルを操作し、最終的に UI を表示するビューを選択するコンポーネントです。 MVC アプリケーションでは、ビューは情報を表示するだけです。ユーザー入力やユーザーとの対話を処理し、それらに応答するのは、コントローラーです。

MVC パターンを使用すると、アプリケーションのさまざまな側面 (入力ロジック、ビジネスロジック、および UI ロジック) を分離するアプリケーションを作成できます。一方、これらの要素間に疎結合が提供されます。 この分離により、アプリケーションを構築する際の複雑さを管理できます。これにより、実装の1つの側面に焦点を当てることができます。 さらに、MVC パターンを使用すると、アプリケーションのテストが簡単になり、アプリケーションを作成するためのテスト駆動開発 (TDD) の使用も促進されます。

**ASP.NET mvc**フレームワークには、ASP.NET mvc ベースの web アプリケーションを作成するための ASP.NET web フォームパターンの代替手段が用意されています。 **ASP.NET MVC**フレームワークは、(Web フォームベースのアプリケーションの場合と同様に) 既存の ASP.NET 機能と統合された軽量で高度なテストが可能なプレゼンテーションフレームワークであり、コア .net framework のすべての機能を利用できるように、マスターページやメンバーシップベースの認証などの既存の機能と統合されています。 これは、既に使用しているすべてのライブラリが ASP.NET MVC 4 でも使用できるため、既に ASP.NET Web フォームを使い慣れている場合に便利です。

さらに、MVC アプリケーションの3つの主要なコンポーネント間の疎結合により、並列開発も促進されます。 たとえば、1人の開発者がビューを操作し、2つ目の開発者がコントローラーロジックを操作し、3番目の開発者がモデルのビジネスロジックに集中できるようにすることができます。

<a id="Objectives"></a>

<a id="Objectives"></a>
### <a name="objectives"></a>目標

このハンズオンラボでは、次の方法を学習します。

- ミュージックストアアプリケーションのチュートリアルに基づいて ASP.NET MVC アプリケーションを最初から作成する
- サイトのホームページへの Url を処理し、その主な機能を参照するためのコントローラーを追加します。
- ビューを追加して、表示されるコンテンツとそのスタイルをカスタマイズします
- データとドメインロジックを格納および管理するためのモデルクラスを追加する
- ビューモデルパターンを使用してコントローラーアクションからビューテンプレートに情報を渡す
- インターネットアプリケーション用の ASP.NET MVC 4 の新しいテンプレートについて説明します。

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>前提条件

このラボを完了するには、次の項目が必要です。

- [Visual Studio 2012 Express For Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) (インストール方法について[は、付録 A](#AppendixA)を参照してください)

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a>セットアップ

**コードスニペットのインストール**

便宜上、このラボで管理するコードの多くは、Visual Studio のコードスニペットとして提供されています。 コードスニペットをインストールするには、 **.\Source\Setup\CodeSnippets.vsi**ファイルを実行します。

Visual Studio Code のスニペットを使い慣れておらず、その使用方法を学習したい場合は、この &quot;ドキュメントの付録「[付録 C: コードスニペットの使用](#AppendixC)&quot;」を参照してください。

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a>手順

このハンズオンラボは、次の演習によって構成されています。

1. [演習 1: MusicStore ASP.NET MVC Web アプリケーションプロジェクトの作成](#Exercise1)
2. [演習 2: コントローラーの作成](#Exercise2)
3. [演習 3: コントローラーへのパラメーターの引き渡し](#Exercise3)
4. [演習 4: ビューの作成](#Exercise4)
5. [演習 5: ビューモデルの作成](#Exercise5)
6. [演習 6: ビューでのパラメーターの使用](#Exercise6)
7. [演習 7: ASP.NET MVC 4 の新しいテンプレートをラップする](#Exercise7)

> [!NOTE]
> 各演習には、演習を完了した後に取得する必要があるソリューションを含む**終了**フォルダーが付属しています。 演習を通じて追加のヘルプが必要な場合は、このソリューションをガイドとして使用できます。

このラボの推定所要時間: **60 分**。

<a id="Exercise1"></a>

<a id="Exercise_1_Creating_MusicStore_ASPNET_MVC_Web_Application_Project"></a>
### <a name="exercise-1-creating-musicstore-aspnet-mvc-web-application-project"></a>演習 1: MusicStore ASP.NET MVC Web アプリケーションプロジェクトの作成

この演習では、Visual Studio 2012 Express for Web とメインフォルダーの組織で ASP.NET MVC アプリケーションを作成する方法について説明します。 また、新しいコントローラーを追加して、アプリケーションのホームページに単純な文字列を表示させる方法についても説明します。

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_the_ASPNET_MVC_Web_Application_Project"></a>
#### <a name="task-1---creating-the-aspnet-mvc-web-application-project"></a>タスク 1-ASP.NET MVC Web アプリケーションプロジェクトの作成

1. このタスクでは、MVC Visual Studio テンプレートを使用して、空の ASP.NET MVC アプリケーションプロジェクトを作成します。 **VS Express for Web**を開始します。
2. **[ファイル]** メニューの **[新しいプロジェクト]** をクリックします。
3. **[新しいプロジェクト]** ダイアログボックスで、[**ビジュアルC#] の** **[web]** テンプレート の一覧にある**ASP.NET MVC 4 Web アプリケーション**プロジェクトの種類を選択します。
4. **名前**を*MvcMusicStore*に変更します。
5. この演習のソースフォルダーの新しい**Begin**フォルダー内にソリューションの場所を設定します。たとえば、 **[\Source\Ex01-CreatingMusicStoreProject\Begin]** のように指定します。 **[OK]** をクリックします。

    ![[新しいプロジェクトの作成] ダイアログボックス](aspnet-mvc-4-fundamentals/_static/image2.png "[新しいプロジェクトの作成] ダイアログボックス")

    *[新しいプロジェクトの作成] ダイアログボックス*
6. **[新しい ASP.NET MVC 4 プロジェクト]** ダイアログボックスで、**基本**テンプレートを選択し、選択した**ビューエンジン**が**Razor**になっていることを確認します。 **[OK]** をクリックします。

    ![[新しい ASP.NET MVC 4 プロジェクト] ダイアログボックス](aspnet-mvc-4-fundamentals/_static/image3.png "[新しい ASP.NET MVC 4 プロジェクト] ダイアログボックス")

    *[新しい ASP.NET MVC 4 プロジェクト] ダイアログボックス*

<a id="Ex1Task2"></a>

<a id="Task_2_-_Exploring_the_Solution_Structure"></a>
#### <a name="task-2---exploring-the-solution-structure"></a>タスク 2-ソリューション構造の調査

ASP.NET MVC フレームワークには、MVC パターンをサポートする Web アプリケーションを作成するのに役立つ Visual Studio プロジェクトテンプレートが含まれています。 このテンプレートは、必要なフォルダー、項目テンプレート、および構成ファイルエントリを含む新しい ASP.NET MVC Web アプリケーションを作成します。

ここでは、ソリューションの構造を調べて、関連する要素とその関係について理解します。 次のフォルダーはすべての ASP.NET MVC アプリケーションに含まれています。 ASP.NET MVC フレームワークでは、既定では、構成&quot; アプローチに対して &quot;規約が使用され、フォルダーの名前付け規則に基づいて既定の仮定がいくつか行われるためです。

1. プロジェクトが作成されたら、右側のソリューションエクスプローラーに作成されたフォルダー構造を確認します。

    ![ソリューションエクスプローラーでの MVC フォルダー構造の ASP.NET](aspnet-mvc-4-fundamentals/_static/image4.png "ソリューションエクスプローラーでの MVC フォルダー構造の ASP.NET")

    *ソリューションエクスプローラーでの MVC フォルダー構造の ASP.NET*

   1. **コントローラー**。 このフォルダーには、コントローラークラスが含まれます。 MVC ベースのアプリケーションでは、コントローラーはエンドユーザーの操作を処理し、モデルを操作し、最終的に UI を表示するビューを選択します。

       > [!NOTE]
       > MVC フレームワークでは、すべてのコントローラーの名前を &quot;Controller&quot;(HomeController、LoginController、ProductController など) で終了する必要があります。
   2. **モデル**。 このフォルダーは、MVC Web アプリケーションのアプリケーションモデルを表すクラス用に用意されています。 これには通常、オブジェクトおよびデータストアと対話するためのロジックを定義するコードが含まれます。 実際のモデル オブジェクトは別のクラス ライブラリに格納するのが一般的です。 ただし、新しいアプリケーションを作成する場合は、クラスを追加し、開発サイクルの後の段階でクラスを個別のクラスライブラリに移動することができます。
   3. **ビュー**。 このフォルダーは、アプリケーションのユーザーインターフェイスを表示するコンポーネントであるビューの推奨される場所です。 ビューでは、表示ビューに関連するその他のファイルに加えて、.aspx、.ascx、cshtml、および .master ファイルが使用されます。 Views フォルダーには、各コントローラーのフォルダーが含まれています。フォルダーには、コントローラー名のプレフィックスが付いた名前が付けられます。 たとえば、 **HomeController**という名前のコントローラーがある場合、Views フォルダーには Home という名前のフォルダーが含まれます。 既定では、ASP.NET MVC フレームワークによってビューが読み込まれるときに、Views\controllerName フォルダー (**views [controllerName] [action] .aspx**) または (**views [ControllerName] [action]. cshtml**) のビュー名を持つ .Aspx ファイルが Razor ビューで検索されます。

      > [!NOTE]
      > 前に示したフォルダーに加えて、MVC Web アプリケーションは**グローバルな global.asax**ファイルを使用してグローバルな URL ルーティングの既定値を設定し、web.config ファイルを使用してアプリケーションを構成**します。**

<a id="Ex1Task3"></a>

<a id="Task_3_-_Adding_a_HomeController"></a>
#### <a name="task-3---adding-a-homecontroller"></a>タスク 3-HomeController の追加

MVC フレームワークを使用しない ASP.NET アプリケーションでは、ユーザーの操作はページ、およびそれらのページからのイベントの発生と処理を中心に編成されます。 これに対し、ASP.NET MVC アプリケーションとのユーザー操作は、コントローラーとそのアクションメソッドを中心に編成されています。

一方、ASP.NET MVC フレームワークは、Url をコントローラーと呼ばれるクラスにマップします。 コントローラーは、着信要求を処理し、ユーザーの入力と操作を処理し、適切なアプリケーションロジックを実行して、クライアントに送り返す応答を決定します (HTML の表示、ファイルのダウンロード、別の URL へのリダイレクトなど)。 HTML を表示する場合、通常、コントローラークラスは個別のビューコンポーネントを呼び出して、要求の HTML マークアップを生成します。 MVC アプリケーションでは、ビューは情報を表示するだけです。ユーザー入力やユーザーとの対話を処理し、それらに応答するのは、コントローラーです。

このタスクでは、ミュージックストアサイトのホームページへの Url を処理するコントローラークラスを追加します。

1. ソリューションエクスプローラー内の**Controllers**フォルダーを右クリックし、 **[追加]** 、 **[コントローラー]** コマンド の順に選択します。

    ![コントローラーコマンドを追加する](aspnet-mvc-4-fundamentals/_static/image5.png "コントローラーコマンドを追加する")

    *コントローラーコマンドの追加*
2. **[コントローラーの追加]** ダイアログボックスが表示されます。 コントローラーに*HomeController*という名前を指定し、 **[追加]** を押します。

    ![[コントローラーの追加] ダイアログ](aspnet-mvc-4-fundamentals/_static/image6.png "[コントローラーの追加] ダイアログ")

    *[コントローラーの追加] ダイアログ*
3. **HomeController.cs**ファイルが**Controllers**フォルダーに作成されます。 **HomeController**がインデックスアクションに対して文字列を返すようにするには、 **index**メソッドを次のコードに置き換えます。

    (コードスニペット- *ASP.NET MVC 4 の基礎-Ex1 HomeController Index*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample1.cs)]

<a id="Ex1Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a>タスク 4-アプリケーションを実行する

このタスクでは、web ブラウザーでアプリケーションを試します。

1. **F5**キーを押してアプリケーションを実行します。 プロジェクトがコンパイルされ、ローカル IIS Web サーバーが起動します。 ローカルの IIS Web サーバーは、web サーバーの URL を指す web ブラウザーを自動的に開きます。

    ![Web ブラウザーで実行されているアプリケーション](aspnet-mvc-4-fundamentals/_static/image7.png "Web ブラウザーで実行されているアプリケーション")

    *Web ブラウザーで実行されているアプリケーション*

    > [!NOTE]
    > ローカルの IIS Web サーバーは、web サイトをランダムなフリーポート番号で実行します。 上の図では、サイトは `http://localhost:50103/`で実行されているので、ポート50103を使用しています。 ポート番号は異なる場合があります。
2. ブラウザーを閉じます。

<a id="Exercise2"></a>

<a id="Exercise_2_Creating_a_Controller"></a>
### <a name="exercise-2-creating-a-controller"></a>演習 2: コントローラーの作成

この演習では、音楽ストアアプリケーションの簡単な機能を実装するようにコントローラーを更新する方法について説明します。 このコントローラーは、次の特定の要求を処理するアクションメソッドを定義します。

- 音楽ストアの音楽ジャンルの一覧ページ
- 特定のジャンルのすべての音楽アルバムを一覧表示する参照ページ
- 特定のミュージックアルバムに関する情報を示す詳細ページ

この演習の範囲において、これらのアクションは単にここで文字列を返します。

<a id="Ex2Task1"></a>

<a id="Task_1_-_Adding_a_New_StoreController_Class"></a>
#### <a name="task-1---adding-a-new-storecontroller-class"></a>タスク 1-新しい StoreController クラスを追加する

このタスクでは、新しいコントローラーを追加します。

1. まだ開いていない場合は**VS Express for Web 2012**を開始します。
2. **[ファイル]** メニューの **[プロジェクトを開く]** をクリックします。 [プロジェクトを開く] ダイアログボックスで、 **Source\Ex02-CreatingAController\Begin**に移動し、 **[開始]** を選択して **[開く]** をクリックします。 または、前の演習を完了した後に取得したソリューションを続行することもできます。

   1. 提供された**Begin**ソリューションを開いた場合は、続行する前に、不足している NuGet パッケージをダウンロードする必要があります。 これを行うには、 **[プロジェクト]** メニューをクリックし、 **[NuGet パッケージの管理]** を選択します。
   2. **[NuGet パッケージの管理]** ダイアログで、 **[復元]** をクリックして、不足しているパッケージをダウンロードします。
   3. 最後に、[**ビルド** | **ビルド**] をクリックしてソリューションをビルドします。

      > [!NOTE]
      > NuGet を使用する利点の1つは、プロジェクトのすべてのライブラリを配布する必要がなく、プロジェクトのサイズを小さくすることです。 NuGet パワーツールを使用すると、パッケージのバージョンを app.config ファイルで指定することで、プロジェクトを初めて実行するときに必要なすべてのライブラリをダウンロードできます。 このため、このラボから既存のソリューションを開いた後に、これらの手順を実行する必要があります。
3. 新しいコントローラーを追加します。 これを行うには、ソリューションエクスプローラー内の**Controllers**フォルダーを右クリックし、 **[追加]** を選択して、 **[コントローラー]** をクリックします。 **コントローラー名**を*StoreController*に変更し、 **[追加]** をクリックします。

    ![[コントローラーの追加] ダイアログ](aspnet-mvc-4-fundamentals/_static/image8.png "[コントローラーの追加] ダイアログ")

    *[コントローラーの追加] ダイアログ*

<a id="Ex2Task2"></a>

<a id="Task_2_-_Modifying_the_StoreControllers_Actions"></a>
#### <a name="task-2---modifying-the-storecontrollers-actions"></a>タスク 2-StoreController のアクションを変更する

このタスクでは、**アクション**と呼ばれるコントローラーメソッドを変更します。 アクションは、URL 要求を処理し、URL を呼び出したブラウザーまたはユーザーに返信するコンテンツを決定します。

1. **StoreController**クラスには既に**Index**メソッドがあります。 このラボでは、このラボを使用して、音楽ストアのすべてのジャンルを一覧表示するページを実装します。 ここでは、 **index**メソッドを次のコードに置き換えます。このコードでは、&quot;Hello from Store. index ()&quot;の文字列を返します。

    (コードスニペット- *ASP.NET MVC 4 の基礎-Ex2 StoreController Index*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample2.cs)]
2. **参照**と**詳細**のメソッドを追加します。 これを行うには、 **StoreController**に次のコードを追加します。

    (コードスニペット- *ASP.NET MVC 4 の基礎-Ex2 StoreController BrowseAndDetails*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample3.cs)]

<a id="Ex2Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a>タスク 3-アプリケーションを実行する

このタスクでは、web ブラウザーでアプリケーションを試します。

1. **F5**キーを押してアプリケーションを実行します。
2. プロジェクトは**ホーム**ページから開始します。 各アクションの実装を確認するには、URL を変更します。

    1. **/ストア**。 **&quot;Hello From Store. Index ()&quot;** が表示されます。
    2. **/ストア/参照** **&quot;Hello From Store. 参照 ()&quot;** が表示されます。
    3. **ストア/詳細**。 **&quot;Hello From Store. Details ()&quot;** が表示されます。

        ![StoreBrowse の参照](aspnet-mvc-4-fundamentals/_static/image9.png "StoreBrowse の参照")

        *参照/参照*
3. ブラウザーを閉じます。

<a id="Exercise3"></a>

<a id="Exercise_3_Passing_parameters_to_a_Controller"></a>
### <a name="exercise-3-passing-parameters-to-a-controller"></a>演習 3: コントローラーへのパラメーターの引き渡し

これまでは、コントローラーから定数文字列が返されています。 この演習では、URL と querystring を使用してコントローラーにパラメーターを渡す方法を学習し、メソッドのアクションがテキストでブラウザーに応答するようにします。

<a id="Ex3Task1"></a>

<a id="Task_1_-_Adding_Genre_Parameter_to_StoreController"></a>
#### <a name="task-1---adding-genre-parameter-to-storecontroller"></a>タスク 1-Genre パラメーターを StoreController に追加する

このタスクでは、 **querystring**を使用して、 **StoreController**の**参照**アクションメソッドにパラメーターを送信します。

1. まだ開いていない場合は、 **VS Express for Web**を開始します。
2. **[ファイル]** メニューの **[プロジェクトを開く]** をクリックします。 [プロジェクトを開く] ダイアログボックスで、 **Source\Ex03-PassingParametersToAController\Begin**に移動し、 **[開始]** を選択して **[開く]** をクリックします。 または、前の演習を完了した後に取得したソリューションを続行することもできます。

   1. 提供された**Begin**ソリューションを開いた場合は、続行する前に、不足している NuGet パッケージをダウンロードする必要があります。 これを行うには、 **[プロジェクト]** メニューをクリックし、 **[NuGet パッケージの管理]** を選択します。
   2. **[NuGet パッケージの管理]** ダイアログで、 **[復元]** をクリックして、不足しているパッケージをダウンロードします。
   3. 最後に、[**ビルド** | **ビルド**] をクリックしてソリューションをビルドします。

      > [!NOTE]
      > NuGet を使用する利点の1つは、プロジェクトのすべてのライブラリを配布する必要がなく、プロジェクトのサイズを小さくすることです。 NuGet パワーツールを使用すると、パッケージのバージョンを app.config ファイルで指定することで、プロジェクトを初めて実行するときに必要なすべてのライブラリをダウンロードできます。 このため、このラボから既存のソリューションを開いた後に、これらの手順を実行する必要があります。
3. **StoreController**クラスを開きます。 これを行うには、**ソリューションエクスプローラー**で**Controllers**フォルダーを展開し、 **StoreController.cs**をダブルクリックします。
4. **参照**メソッドを変更し、特定のジャンルに対する要求に文字列パラメーターを追加します。 ASP.NET MVC は、呼び出されたときに、 **genre**という名前のクエリ文字列またはフォームポストパラメーターをこのアクションメソッドに自動的に渡します。 これを行うには、 **Browse**メソッドを次のコードに置き換えます。

    (コードスニペット- *ASP.NET MVC 4 の基礎-Ex3 StoreController BrowseMethod*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample4.cs)]

> [!NOTE]
> HtmlEncode ユーティリティメソッドを使用して、 **HttpUtility**などのリンクを使用して、ユーザーが Javascript をビューに挿入できないようにします**か?Genre =&lt;スクリプト&gt;ウィンドウ. location = '[http://hackersite.com](http://hackersite.com)'&lt;/script&gt;** 。
> 
> 詳細については、こちらの[msdn 記事](https://msdn.microsoft.com/library/a2a4yykt(v=VS.80).aspx)をご覧ください。

<a id="Ex3Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a>タスク 2-アプリケーションの実行

このタスクでは、web ブラウザーでアプリケーションを試し、 **genre**パラメーターを使用します。

1. **F5**キーを押してアプリケーションを実行します。
2. プロジェクトは**ホーム**ページから開始します。 URL を「 */Store/Browse」に変更します。Genre = Disco* : アクションが genre パラメーターを受け取ることを確認します。

    ![StoreBrowseGenre の参照 = Disco](aspnet-mvc-4-fundamentals/_static/image10.png "StoreBrowseGenre の参照 = Disco")

    *参照/参照Genre = Disco*
3. ブラウザーを閉じます。

<a id="Ex3Task3"></a>

<a id="Task_3_-_Adding_an_Id_Parameter_Embedded_in_the_URL"></a>
#### <a name="task-3---adding-an-id-parameter-embedded-in-the-url"></a>タスク 3-URL に埋め込まれた Id パラメーターの追加

このタスクでは、 **URL**を使用して、 **StoreController**の**Details** action メソッドに**Id**パラメーターを渡します。 ASP.NET MVC の既定のルーティング規則では、アクションメソッド名の後の URL のセグメントを、 **Id**という名前のパラメーターとして扱います。アクションメソッドに Id という名前のパラメーターがある場合、ASP.NET MVC は自動的に URL セグメントをパラメーターとして渡します。 URL **Store/Details/5**では、 **Id**は**5**と解釈されます。

1. **StoreController**の**Details**メソッドを変更し、 **id**という名前の**int**パラメーターを追加します。これを行うには、 **Details**メソッドを次のコードに置き換えます。

    (コードスニペット- *ASP.NET MVC 4 の基礎-Ex3 StoreController のメソッド*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample5.cs)]

<a id="Ex3Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a>タスク 4-アプリケーションを実行する

このタスクでは、web ブラウザーでアプリケーションを試し、 **Id**パラメーターを使用します。

1. **F5**キーを押してアプリケーションを実行します。
2. プロジェクトは**ホーム**ページから開始します。 URL を */Store//5*に変更して、アクションが id パラメーターを受け取ることを確認します。

    ![StoreDetails5 の参照](aspnet-mvc-4-fundamentals/_static/image11.png "StoreDetails5 の参照")

    *参照/表示 (/dns)/5*

<a id="Exercise4"></a>

<a id="Exercise_4_Creating_a_View"></a>
### <a name="exercise-4-creating-a-view"></a>演習 4: ビューの作成

ここまでは、コントローラーアクションから文字列を返していました。 これは、コントローラーがどのように動作するかを理解するのに便利な方法ですが、実際の Web アプリケーションの構築方法ではありません。 ビューは、テンプレートファイルを使用してブラウザーに HTML を返すためのより優れた方法を提供するコンポーネントです。

この演習では、共通の HTML コンテンツ用のテンプレートを設定するためのレイアウトマスターページを追加する方法、サイトのルックアンドフィールを向上させるためのスタイルシート、最後にビューテンプレートを追加して、HomeController が HTML を返すようにする方法について学習します。

<a id="Ex4Task1"></a>

<a id="Task_1_-_Modifying_the_file__layoutcshtml"></a>
#### <a name="task-1---modifying-the-file-_layoutcshtml"></a>タスク 1-ファイル \_layout を変更する

**\_** ファイルを使用すると、web サイト全体で共通 HTML を使用するためのテンプレートを設定できます。 このタスクでは、共通のヘッダーと、ホームページと店舗区分へのリンクを含むレイアウトマスターページを追加します。

1. まだ開いていない場合は、 **VS Express for Web**を開始します。
2. **[ファイル]** メニューの **[プロジェクトを開く]** をクリックします。 プロジェクトを開く ダイアログで、**ソース** を参照して 開始 を選択し、**開始** をクリックして、**開く** をクリックします。 または、前の演習を完了した後に取得したソリューションを続行することもできます。

   1. 提供された**Begin**ソリューションを開いた場合は、続行する前に、不足している NuGet パッケージをダウンロードする必要があります。 これを行うには、 **[プロジェクト]** メニューをクリックし、 **[NuGet パッケージの管理]** を選択します。
   2. **[NuGet パッケージの管理]** ダイアログで、 **[復元]** をクリックして、不足しているパッケージをダウンロードします。
   3. 最後に、[**ビルド** | **ビルド**] をクリックしてソリューションをビルドします。

      > [!NOTE]
      > NuGet を使用する利点の1つは、プロジェクトのすべてのライブラリを配布する必要がなく、プロジェクトのサイズを小さくすることです。 NuGet パワーツールを使用すると、パッケージのバージョンを app.config ファイルで指定することで、プロジェクトを初めて実行するときに必要なすべてのライブラリをダウンロードできます。 このため、このラボから既存のソリューションを開いた後に、これらの手順を実行する必要があります。
3. ファイル<strong>\_の layout</strong>には、サイト上のすべてのページの HTML コンテナーレイアウトが含まれています。 これには、HTML 応答の<strong>&lt;html&gt;</strong>要素だけでなく、 <strong>&lt;ヘッド&gt;</strong>および<strong>&lt;本体&gt;</strong>要素が含まれます。 HTML 本文内の<strong>@RenderBody()</strong>は、ビューテンプレートで動的なコンテンツを格納できる領域を識別します。
   (C#)

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample6.cshtml)]
4. サイト内のすべてのページに、ホームページと店舗領域へのリンクを含む共通ヘッダーを追加します。 そのためには、&lt;body&gt; ステートメントの下に次のコードを追加します。
   (C#)

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample7.cshtml)]
5. 各ページの本文セクションを表示するための div を含めます。 <strong>@RenderBody()</strong>を、次の強調表示されC#たコードに置き換えます。 ()

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample8.cshtml)]

    > [!NOTE]
    > ご存知でしたか? Visual Studio 2012 には、一般的に使用されるコードを HTML やコードファイルなどに簡単に追加できるようにするスニペットが用意されています。 **&lt;div&gt;** を入力し、 **tab**キーを2回押して、完全な**div**タグを挿入してみてください。

<a id="Ex4Task2"></a>

<a id="Task_2_-_Adding_CSS_Stylesheet"></a>
#### <a name="task-2---adding-css-stylesheet"></a>タスク 2-CSS スタイルシートの追加

空のプロジェクトテンプレートには、非常に効率的な CSS ファイルが含まれています。これには、基本的なフォームおよび検証メッセージの表示に使用されるスタイルが含まれています。 サイトのルックアンドフィールを強化するために、追加の CSS とイメージ (デザイナーによって提供される可能性があります) を使用します。

このタスクでは、CSS スタイルシートを追加して、サイトのスタイルを定義します。

1. CSS ファイルとイメージは、このラボの**Source\Assets\Content**フォルダーに含まれています。 アプリケーションに追加するには、次に示すように、 **Windows エクスプローラー**ウィンドウから Web 用 Visual Studio Express の**ソリューションエクスプローラー**にコンテンツをドラッグします。

    ![ドラッグ (スタイルの内容を)](aspnet-mvc-4-fundamentals/_static/image12.png "ドラッグ (スタイルの内容を)")

    *ドラッグ (スタイルの内容を)*
2. [警告] ダイアログが表示され、**サイトの .css**ファイルと既存のイメージの置換を確認するメッセージが表示されます。 **[すべての項目に適用]** チェックボックスをオンにし、[**はい]** をクリックします。

<a id="Ex4Task3"></a>

<a id="Task_3_-_Adding_a_View_Template"></a>
#### <a name="task-3---adding-a-view-template"></a>タスク 3-ビューテンプレートの追加

このタスクでは、ビューテンプレートを追加して、この演習で追加したレイアウトマスターページと CSS を使用する HTML 応答を生成します。

1. サイトのホームページを参照するときにビューテンプレートを使用するには、最初に、文字列を返す代わりに、 **HomeController Index**メソッドが**ビュー**を返すことを示す必要があります。 **HomeController**クラスを開き、 **actionresult**を返すように**Index**メソッドを変更し、 **View ()** を返すようにします。

    (コードスニペット- *ASP.NET MVC 4 の基礎-Ex4 HomeController Index*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample9.cs)]
2. 次に、適切なビューテンプレートを追加する必要があります。 これを行うには、 **Index**アクションメソッド内を**右クリック**し、 **[ビューの追加]** を選択します。 **[ビューの追加]** ダイアログが表示されます。

    ![Index メソッド内からビューを追加する](aspnet-mvc-4-fundamentals/_static/image13.png "Index メソッド内からビューを追加する")

    *Index メソッド内からビューを追加する*
3. **[ビューの追加]** ダイアログボックスが表示され、ビューテンプレートファイルが生成されます。 既定では、このダイアログボックスには、ビューテンプレートを使用するアクションメソッドと一致するように、ビューテンプレートの名前が事前に設定されています。 HomeController 内の**index**アクションメソッド内で **[ビューの追加]** コンテキストメニューを使用したので、 **[ビューの追加]** ダイアログには既定のビュー名としてインデックスがあります。 **[追加]** をクリックします。

    ![[ビューの追加] ダイアログ](aspnet-mvc-4-fundamentals/_static/image14.png "[ビューの追加] ダイアログ")

    *[ビューの追加] ダイアログ*
4. **Views\Home**フォルダー内に**Index. cshtml** view テンプレートが生成され、それが開きます。

    ![ホームインデックスビューが作成されました](aspnet-mvc-4-fundamentals/_static/image15.png "ホームインデックスビューが作成されました")

    *ホームインデックスビューが作成されました*

    > [!NOTE]
    > **Index. cshtml**ファイルの名前と場所は、既定の ASP.NET MVC 名前付け規則に従っています。
    > 
    > フォルダー \ Views\**home** は、コントローラー名 (**home**コントローラー) と一致します。 ビューテンプレート名 (**Index**) は、ビューを表示するコントローラーアクションメソッドに一致します。
    > 
    > このように、ASP.NET MVC では、この名前付け規則を使用してビューを返すときに、ビューテンプレートの名前または場所を明示的に指定する必要がありません。
5. 生成されたビューテンプレートは、前に定義した **\_の layout**テンプレートに基づいています。 次のコードに示すように、ViewBag プロパティを**home**に更新し、メインコンテンツを**次のホームページ**に変更します。

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample10.cshtml)]
6. ソリューションエクスプローラーで [ **MvcMusicStore**プロジェクト] を選択し、 **F5**キーを押してアプリケーションを実行します。

<a id="Ex4Task4"></a>

<a id="Task_4_Verification"></a>
#### <a name="task-4-verification"></a>タスク 4: 検証

前の演習のすべての手順を正しく実行したことを確認するには、次の手順を実行します。

ブラウザーでアプリケーションを開いたときに、次の点に注意する必要があります。

1. ビューテンプレートが標準の名前付け規則に従っているため、HomeController のインデックスアクションメソッドが見つかり、 **\Views\Home\Index.cshtml** view テンプレートが表示されます。これは、**リターンビュー ()** を呼び出したコードです。
2. ホームページには、 **\Views\Home\Index.cshtml** view テンプレート内で定義されているウェルカムメッセージが表示されます。
3. ホームページでは **\_layout**テンプレートが使用されているため、ウェルカムメッセージは標準のサイト HTML レイアウト内に含まれています。

    ![定義済みの LayoutPage と style を使用したホームインデックスビュー](aspnet-mvc-4-fundamentals/_static/image16.png "定義済みの LayoutPage と style を使用したホームインデックスビュー")

    *定義済みの LayoutPage と style を使用したホームインデックスビュー*

<a id="Exercise5"></a>

<a id="Exercise_5_Creating_a_View_Model"></a>
### <a name="exercise-5-creating-a-view-model"></a>演習 5: ビューモデルの作成

これまでは、ビューにハードコードされた HTML が表示されていましたが、動的な web アプリケーションを作成するために、ビューテンプレートはコントローラーから情報を受信する必要があります。 この目的に使用される一般的な手法の1つは、**モデル**化パターンです。これにより、コントローラーは、適切な HTML 応答を生成するために必要なすべての情報をパッケージ化できます。

この演習では、ビューモデルクラスを作成し、必要なプロパティを追加する方法を学習します。これには、ストア内のジャンルの数と、それらのジャンルの一覧が含まれます。 また、作成されたビューモデルを使用するように StoreController を更新します。最後に、ページに記載されているプロパティを表示する新しいビューテンプレートを作成します。

<a id="Ex5Task1"></a>

<a id="Task_1_-_Creating_a_ViewModel_Class"></a>
#### <a name="task-1---creating-a-viewmodel-class"></a>タスク 1-ビューモデルクラスの作成

このタスクでは、ストアのジャンル一覧表示シナリオを実装するビューモデルクラスを作成します。

1. まだ開いていない場合は、 **VS Express for Web**を開始します。
2. **[ファイル]** メニューの **[プロジェクトを開く]** をクリックします。 [プロジェクトを開く] ダイアログで、 **Source05-を**参照し、 **[開始]** を選択して、 **[開く]** をクリックします。 または、前の演習を完了した後に取得したソリューションを続行することもできます。

   1. 提供された**Begin**ソリューションを開いた場合は、続行する前に、不足している NuGet パッケージをダウンロードする必要があります。 これを行うには、 **[プロジェクト]** メニューをクリックし、 **[NuGet パッケージの管理]** を選択します。
   2. **[NuGet パッケージの管理]** ダイアログで、 **[復元]** をクリックして、不足しているパッケージをダウンロードします。
   3. 最後に、[**ビルド** | **ビルド**] をクリックしてソリューションをビルドします。

      > [!NOTE]
      > NuGet を使用する利点の1つは、プロジェクトのすべてのライブラリを配布する必要がなく、プロジェクトのサイズを小さくすることです。 NuGet パワーツールを使用すると、パッケージのバージョンを app.config ファイルで指定することで、プロジェクトを初めて実行するときに必要なすべてのライブラリをダウンロードできます。 このため、このラボから既存のソリューションを開いた後に、これらの手順を実行する必要があります。
3. ビューモデルを保持する**viewmodel**フォルダーを作成します。 これを行うには、最上位レベルの**MvcMusicStore**プロジェクトを右クリックし、 **[追加]** 、 **[新しいフォルダー]** の順に選択します。

    ![新しいフォルダーの追加](aspnet-mvc-4-fundamentals/_static/image17.png "新しいフォルダーの追加")

    *新しいフォルダーの追加*
4. フォルダーに*viewmodel*という名前を指定します。

    ![ソリューションエクスプローラーの Viewmodel フォルダー](aspnet-mvc-4-fundamentals/_static/image18.png "ソリューションエクスプローラーの Viewmodel フォルダー")

    *ソリューションエクスプローラーの Viewmodel フォルダー*
5. **ビューモデル**クラスを作成します。 これを行うには、最近作成された **[viewmodel]** フォルダーを右クリックし、 **[追加]** 、 **[新しい項目]** の順に選択します。 **[コード]** で **[クラス]** 項目を選択し、ファイルに*StoreIndexViewModel.cs*という名前を指定して、 **[追加]** をクリックします。

    ![新しいクラスの追加](aspnet-mvc-4-fundamentals/_static/image19.png "新しいクラスの追加")

    *新しいクラスの追加*

    ![StoreIndexViewModel クラスを作成しています](aspnet-mvc-4-fundamentals/_static/image20.png "StoreIndexViewModel クラスを作成しています")

    *StoreIndexViewModel クラスを作成しています*

<a id="Ex5Task2"></a>

<a id="Task_2_-_Adding_Properties_to_the_ViewModel_class"></a>
#### <a name="task-2---adding-properties-to-the-viewmodel-class"></a>タスク 2-ビューモデルクラスにプロパティを追加する

予想される HTML 応答を生成するために、StoreController からビューテンプレートに渡されるパラメーターは2つあります。ストア内のジャンルの数とそれらのジャンルの一覧です。

このタスクでは、これら2つのプロパティを**Storeindexviewmodel**クラスに追加します。 **numberofgenres** (整数) と**ジャンル**(文字列のリスト) です。

1. **Numberofgenres**と**ジャンル**のプロパティを**storeindexviewmodel**クラスに追加します。 これを行うには、クラス定義に次の2行を追加します。

    (コードスニペット- *ASP.NET MVC 4 の基礎-Ex5 StoreIndexViewModel*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample11.cs)]

> [!NOTE]
> **{Get; set;}** 表記では、 C#の自動実装プロパティ機能を使用します。 これにより、バッキングフィールドを宣言しなくても、プロパティの利点が得られます。

<a id="Ex5Task3"></a>

<a id="Task_3_-_Updating_StoreController_to_use_the_StoreIndexViewModel"></a>
#### <a name="task-3---updating-storecontroller-to-use-the-storeindexviewmodel"></a>タスク 3-StoreIndexViewModel を使用するための StoreController の更新

**Storeindexviewmodel**クラスは、応答を生成するために、 **StoreController**の**インデックス**メソッドからビューテンプレートに渡すために必要な情報をカプセル化します。

このタスクでは、 **Storeindexviewmodel**を使用するように**StoreController**を更新します。

1. **StoreController**クラスを開きます。

    ![StoreController クラスを開く](aspnet-mvc-4-fundamentals/_static/image21.png "StoreController クラスを開く")

    *StoreController クラスを開く*
2. **StoreController**から**storeindexviewmodel**クラスを使用するには、 **StoreController**コードの先頭に次の名前空間を追加します。

    (コードスニペット- *ASP.NET MVC 4 の基礎-viewmodel を使用した Ex5 StoreIndexViewModel*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample12.cs)]
3. StoreController の**インデックス**アクションメソッドを変更して、 **storeindexviewmodel**オブジェクトを作成および設定し、それをビューテンプレートに渡して HTML 応答を生成するようにします。

    > [!NOTE]
    > ラボ &quot;ASP.NET MVC モデルとデータアクセス&quot; では、データベースからストアのジャンルの一覧を取得するコードを記述します。 次のコードでは、 **Storeindexviewmodel**を設定するダミーデータのジャンルの**一覧**を作成します。
    > 
    > **Storeindexviewmodel**オブジェクトを作成して設定すると、そのオブジェクトは引数として**View**メソッドに渡されます。 これは、ビューテンプレートがそのオブジェクトを使用して HTML 応答を生成することを示します。
4. **Index**メソッドを次のコードに置き換えます。

    (コードスニペット- *ASP.NET MVC 4 の基礎-Ex5 StoreController Index メソッド*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample13.cs)]

> [!NOTE]
> にC#慣れていない場合は、 **var**を使用すると、**ビューモデル**変数が遅延バインディングされることを想定できます。 これは適切ではありC#ません。コンパイラは、変数に代入した内容に基づいて、型の推定を使用して、**ビューモデル**が**storeindexviewmodel**型であると判断します。 また、ローカルの**ビューモデル**変数を**storeindexviewmodel**形式としてコンパイルすると、コンパイル時チェックと Visual Studio コードエディターのサポートが得られます。

<a id="Ex5Task4"></a>

<a id="Task_4_-_Creating_a_View_Template_that_Uses_StoreIndexViewModel"></a>
#### <a name="task-4---creating-a-view-template-that-uses-storeindexviewmodel"></a>タスク 4-StoreIndexViewModel を使用するビューテンプレートを作成する

このタスクでは、コントローラーから渡された StoreIndexViewModel オブジェクトを使用してジャンルの一覧を表示するビューテンプレートを作成します。

1. 新しいビューテンプレートを作成する前に、[**ビューの追加] ダイアログ**で**storeindexviewmodel**クラスについて理解できるように、プロジェクトをビルドしてみましょう。 **[ビルド]** メニュー項目を選択し、 **[MvcMusicStore のビルド]** をクリックして、プロジェクトをビルドします。

    ![プロジェクトのビルド](aspnet-mvc-4-fundamentals/_static/image22.png "プロジェクトのビルド")

    *プロジェクトのビルド*
2. 新しいビューテンプレートを作成します。 これを行うには、 **Index**メソッド内を右クリックし、 **[ビューの追加]** を選択します。

    ![ビューの追加](aspnet-mvc-4-fundamentals/_static/image23.png "ビューの追加")

    *ビューの追加*
3. [**ビューの追加] ダイアログ**は**StoreController**から呼び出されたため、既定では **\Views\Store\Index.cshtml**ファイルにビューテンプレートが追加されます。 **[厳密に型指定されたビューを作成する]** チェックボックスをオンにし、**モデルクラス**として **[storeindexviewmodel]** を選択します。 また、選択したビューエンジンが**Razor**であることを確認します。 **[追加]** をクリックします。

    ![[ビューの追加] ダイアログ](aspnet-mvc-4-fundamentals/_static/image24.png "[ビューの追加] ダイアログ")

    *[ビューの追加] ダイアログ*

    **\Views\Store\Index.cshtml** View テンプレートファイルが作成されて開きます。 ビューテンプレートでは、最後の手順の **[ビューの追加]** ダイアログに表示される情報に基づいて、 **storeindexviewmodel**インスタンスが HTML 応答の生成に使用するデータとして想定されます。 テンプレートがのC#`ViewPage<musicstore.viewmodels.storeindexviewmodel>` を継承していることがわかります。

<a id="Ex5Task5"></a>

<a id="Task_5_-_Updating_the_View_Template"></a>
#### <a name="task-5---updating-the-view-template"></a>タスク 5-ビューテンプレートを更新する

このタスクでは、最後のタスクで作成されたビューテンプレートを更新して、ページ内のジャンルの数とその名前を取得します。

> [!NOTE]
> ビューテンプレート内でコードを実行するには、@ 構文 (多くの場合 &quot;code ナゲット&quot;) を使用します。

1. **Index. cshtml**ファイルの**Store**フォルダー内で、コードを次のコードに置き換えます。

[!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample14.cshtml)]

    > [!NOTE]
    > As soon as you finish typing the period after the word **Model**, Visual Studio's Intellisense will show a list of possible properties and methods to choose from.
    > 
    > ![](aspnet-mvc-4-fundamentals/_static/image25.png)
    > 
    > *Getting Model properties and methods with Visual Studio's IntelliSense*
    > 
    > The **Model** property references the **StoreIndexViewModel** object that the Controller passed to the View template. This means that you can access all of the data passed from the Controller to the View template via the **Model** property, and format it into an appropriate HTML response within the View template.
    > 
    > You can just select the **NumberOfGenres** property from the Intellisense list rather than typing it in and then it will auto-complete it by pressing the **tab key**.
2. **Storeindexviewmodel**のジャンルリストをループし、 **foreach**ループを使用して HTML **&lt;ul&gt;** リストを作成します。
   (C#)

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample15.cshtml)]
3. **F5**キーを押してアプリケーションを実行し、[参照] **/[ストア**] をクリックします。 **Storeindexviewmodel**からビューテンプレートに渡されたジャンルの一覧が表示されます。

    ![ジャンルの一覧を表示するビュー](aspnet-mvc-4-fundamentals/_static/image26.png "ジャンルの一覧を表示するビュー")

    *ジャンルの一覧を表示するビュー*
4. ブラウザーを閉じます。

<a id="Exercise6"></a>

<a id="Exercise_6_Using_Parameters_in_View"></a>
### <a name="exercise-6-using-parameters-in-view"></a>演習 6: ビューでのパラメーターの使用

演習3では、コントローラーにパラメーターを渡す方法について学習しました。 この演習では、ビューテンプレートでこれらのパラメーターを使用する方法を学習します。 この目的のために、まず、データとドメインロジックを管理するのに役立つモデルクラスを紹介します。 また、URL パスのエンコードなどを気にせずに、ASP.NET MVC アプリケーション内のページへのリンクを作成する方法についても説明します。

<a id="Ex6Task1"></a>

<a id="Task_1_-_Adding_Model_Classes"></a>
#### <a name="task-1---adding-model-classes"></a>タスク 1-モデルクラスの追加

コントローラーからビューに情報を渡すためだけに作成される Viewmodel とは異なり、モデルクラスはデータとドメインロジックを格納および管理するために構築されています。 このタスクでは、これらの概念を表す2つのモデルクラス (**ジャンル**と**アルバム**) を追加します。

1. まだ開いていない場合は、開始**VS Express for Web**
2. **[ファイル]** メニューの **[プロジェクトを開く]** をクリックします。 プロジェクトを開く ダイアログで、**ソース**、開始 の順に選択し、**開始** を選択して **開く** をクリックします。 または、前の演習を完了した後に取得したソリューションを続行することもできます。

   1. 提供された**Begin**ソリューションを開いた場合は、続行する前に、不足している NuGet パッケージをダウンロードする必要があります。 これを行うには、 **[プロジェクト]** メニューをクリックし、 **[NuGet パッケージの管理]** を選択します。
   2. **[NuGet パッケージの管理]** ダイアログで、 **[復元]** をクリックして、不足しているパッケージをダウンロードします。
   3. 最後に、[**ビルド** | **ビルド**] をクリックしてソリューションをビルドします。

      > [!NOTE]
      > NuGet を使用する利点の1つは、プロジェクトのすべてのライブラリを配布する必要がなく、プロジェクトのサイズを小さくすることです。 NuGet パワーツールを使用すると、パッケージのバージョンを app.config ファイルで指定することで、プロジェクトを初めて実行するときに必要なすべてのライブラリをダウンロードできます。 このため、このラボから既存のソリューションを開いた後に、これらの手順を実行する必要があります。
3. **ジャンル**モデルクラスを追加します。 これを行うには、**ソリューションエクスプローラー**で **[モデル]** フォルダーを右クリックし、 **[追加]** をクリックして、 **[新しい項目]** オプションを選択します。 **[コード]** で **[クラス]** 項目を選択し、ファイルに*Genre.cs*という名前を指定して、 **[追加]** をクリックします。

    ![クラスの追加](aspnet-mvc-4-fundamentals/_static/image27.png "クラスの追加")

    *新しい項目の追加*

    ![ジャンルモデルクラスの追加](aspnet-mvc-4-fundamentals/_static/image28.png "ジャンルモデルクラスの追加")

    *ジャンルモデルクラスの追加*
4. **名前**プロパティを Genre クラスに追加します。 これを行うには、次のコードを追加します。

    (コードスニペット- *ASP.NET MVC 4 の基礎-Ex6 Genre*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample16.cs)]
5. 前と同じ手順に従って、**アルバム**クラスを追加します。 これを行うには、**ソリューションエクスプローラー**で **[モデル]** フォルダーを右クリックし、 **[追加]** をクリックして、 **[新しい項目]** オプションを選択します。 **[コード]** で **[クラス]** 項目を選択し、ファイルに*Album.cs*という名前を指定して、 **[追加]** をクリックします。
6. アルバムクラスに**ジャンル**と**タイトル**の2つのプロパティを追加します。 これを行うには、次のコードを追加します。

    (コードスニペット- *ASP.NET MVC 4 の基礎-Ex6 アルバム*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample17.cs)]

<a id="Ex6Task2"></a>

<a id="Task_2_-_Adding_a_StoreBrowseViewModel"></a>
#### <a name="task-2---adding-a-storebrowseviewmodel"></a>タスク 2-StoreBrowseViewModel の追加

このタスクでは、選択したジャンルに一致するアルバムを表示するために**StoreBrowseViewModel**が使用されます。 このタスクでは、このクラスを作成し、**ジャンル**とその**アルバム**の一覧を処理する2つのプロパティを追加します。

1. **StoreBrowseViewModel**クラスを追加します。 これを行うには、**ソリューションエクスプローラー**で **[viewmodel]** フォルダーを右クリックし、 **[追加]** をクリックして、 **[新しい項目]** オプションを選択します。 **[コード]** で **[クラス]** 項目を選択し、ファイルに*StoreBrowseViewModel.cs*という名前を指定して、 **[追加]** をクリックします。
2. **StoreBrowseViewModel**クラスのモデルへの参照を追加します。 これを行うには、次の using 名前空間を追加します。

    (コードスニペット- *ASP.NET MVC 4 の基礎-Ex6 を通じてモデルを*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample18.cs)]
3. **StoreBrowseViewModel**クラスに**ジャンル**と**アルバム**の2つのプロパティを追加します。 これを行うには、次のコードを追加します。

    (コードスニペット- *ASP.NET MVC 4 の基礎-Ex6 ModelProperties*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample19.cs)]

> [!NOTE]
> **&lt;アルバム&gt;の一覧**とは?: この定義では、**リスト&lt;t&gt;** 型を使用しています。ここで、 **t**は、この**リスト**の要素に属する型 (この場合は**アルバム**(またはその子孫)) を制限します。
> 
> この機能は、クラスやメソッドが宣言され、クライアントコードによってインスタンス化されるまで、1つ以上の型の仕様を遅延さC#せるクラスとメソッドを設計するための機能です。これは、**ジェネリック**と呼ばれる言語の機能です。
> 
> **リスト&lt;t&gt;** は**ArrayList**型に相当する汎用であり、 **system.string 名前空間**で使用できます。 **ジェネリック**を使用する利点の1つは、型が指定されているため、 **ArrayList**の場合と同様に、要素を**アルバム**にキャストするなどの型チェック操作を処理する必要がないことです。

<a id="Ex6Task3"></a>

<a id="Task_3_-_Using_the_New_ViewModel_in_the_StoreController"></a>
#### <a name="task-3---using-the-new-viewmodel-in-the-storecontroller"></a>タスク 3-StoreController で新しいビューモデルを使用する

このタスクでは、新しい**StoreBrowseViewModel**を使用するように**StoreController**の**Browse**および**Details**アクションメソッドを変更します。

1. **StoreController**クラスの [モデル] フォルダーへの参照を追加します。 これを行うには、**ソリューションエクスプローラー**で**Controllers**フォルダーを展開し、 **StoreController**クラスを開きます。 その後、次のコードを追加します。

    (コードスニペット- *ASP.NET MVC 4 の基礎-Ex6 のプラグイン*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample20.cs)]
2. **参照**アクションメソッドを置き換えて、 **Storeviewstoretローラ**クラスを使用します。 次のハンズオンラボでは、ジャンルと、ダミーデータを含む2つの新しいアルバムオブジェクトを作成します (次のハンズオンラボでは、データベースから実際のデータを使用します)。 これを行うには、 **Browse**メソッドを次のコードに置き換えます。

    (コードスニペット- *ASP.NET MVC 4 の基礎-Ex6 BrowseMethod*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample21.cs)]
3. **詳細**アクションメソッドを置き換えて、 **Storeviewstoretローラ**クラスを使用します。 **ビュー**に返される新しい**アルバム**オブジェクトを作成します。 これを行うには、 **Details**メソッドを次のコードに置き換えます。

    (コードスニペット- *ASP.NET MVC 4 の基礎-Ex6 のメソッド*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample22.cs)]

<a id="Ex6Task4"></a>

<a id="Task_4_-_Adding_a_Browse_View_Template"></a>
#### <a name="task-4---adding-a-browse-view-template"></a>タスク 4-参照ビューテンプレートを追加する

このタスクでは、特定のジャンルのアルバムが表示されるように、**参照**ビューを追加します。

1. 新しいビューテンプレートを作成する前に、プロジェクトをビルドして、 **[ビューの追加]** ダイアログが使用するビュー**モデル**クラスを認識できるようにする必要があります。 **[ビルド]** メニュー項目を選択し、 **[MvcMusicStore のビルド]** をクリックして、プロジェクトをビルドします。
2. **参照**ビューを追加します。 これを行うには、 **StoreController**の **[参照]** アクションメソッドを右クリックし、 **[ビューの追加]** をクリックします。
3. **[ビューの追加]** ダイアログボックスで、ビュー名が **[参照]** であることを確認します。 厳密に型指定された **[ビューを作成する]** チェックボックスをオンにし、 **[モデルクラス]** ドロップダウンから **[StoreBrowseViewModel]** を選択します。 他のフィールドは既定値のままにしておきます。 **[追加]** をクリックします。

    ![参照ビューの追加](aspnet-mvc-4-fundamentals/_static/image29.png "参照ビューの追加")

    *参照ビューの追加*
4. ビューテンプレートに渡される**StoreBrowseViewModel**オブジェクトにアクセスして、Genre の情報を表示するように、Browse を変更し**ます**。 これを行うには、内容を次のようにC#置き換えます。 ()

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample23.cshtml)]

<a id="Ex6Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a>タスク 5-アプリケーションを実行する

このタスクでは **、browse メソッドが** **browse**メソッドアクションからアルバムを取得することをテストします。

1. **F5**キーを押してアプリケーションを実行します。
2. プロジェクトはホームページから開始します。 URL を「 **/Store/Browse」に変更します。Genre = Disco**は、アクションが2つのアルバムを返すことを確認します。

    ![ストアの Disco アルバムの参照](aspnet-mvc-4-fundamentals/_static/image30.png "ストアの Disco アルバムの参照")

    *ストアの Disco アルバムの参照*

<a id="Ex6Task6"></a>

<a id="Task_6_-_Displaying_information_About_a_Specific_Album"></a>
#### <a name="task-6---displaying-information-about-a-specific-album"></a>タスク 6-特定のアルバムに関する情報を表示する

このタスクでは、 **[ストア/詳細]** ビューを実装して、特定のアルバムに関する情報を表示します。 このハンズオンラボでは、アルバムに関して表示されるすべてのものが、既に**ビュー**テンプレートに含まれています。 そのため、 **StoreStoreBrowseViewModel ビューモデル**クラスを作成するのではなく、現在のテンプレートを使用してアルバムに渡します。

1. 必要に応じてブラウザーを閉じ、Visual Studio ウィンドウに戻ります。 **StoreController**の**details**アクションメソッドの新しい**詳細**ビューを追加します。 これを行うには、 **StoreController**クラスの**詳細**メソッドを右クリックし、 **[ビューの追加]** をクリックします。
2. **[ビューの追加]** ダイアログで、**ビュー名**が **[詳細]** であることを確認します。 厳密に型指定された **[ビューを作成する]** チェックボックスをオンにし、 **[モデルクラス]** ドロップダウンから **[アルバム]** を選択します。 他のフィールドは既定値のままにしておきます。 **[追加]** をクリックします。 これにより、 **\Views\Store\Details.cshtml**ファイルが作成されて開きます。

    ![詳細ビューの追加](aspnet-mvc-4-fundamentals/_static/image31.png "詳細ビューの追加")

    *詳細ビューの追加*
3. 詳細の**cshtml**ファイルを変更して、アルバムの情報を表示し、ビューテンプレートに渡される**アルバム**オブジェクトにアクセスします。 これを行うには、内容を次のようにC#置き換えます。 ()

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample24.cshtml)]

<a id="Ex6Task7"></a>

<a id="Task_7_-_Running_the_Application"></a>
#### <a name="task-7---running-the-application"></a>タスク 7-アプリケーションを実行する

このタスクで**は、詳細ビューが** **詳細アクション**メソッドからアルバムの情報を取得することをテストします。

1. **F5**キーを押してアプリケーションを実行します。
2. プロジェクトは**ホーム**ページから開始します。 アルバムの情報を確認するには、URL を **/ストア/詳細/5**に変更します。

    ![アルバムの閲覧の詳細](aspnet-mvc-4-fundamentals/_static/image32.png "アルバムの閲覧の詳細")

    *アルバムの詳細を閲覧する*

<a id="Ex6Task8"></a>

<a id="Task_8_-_Adding_Links_Between_Pages"></a>
#### <a name="task-8---adding-links-between-pages"></a>タスク 8-ページ間のリンクの追加

このタスクでは、ストアビューにリンクを追加して、各ジャンル名のリンクを適切な **/storeurl**にリンクします。 このようにして、ジャンルをクリックすると、 **[ディスコ]** 、[**参照]** 、[ジャンル]、[ディスコ URL] の順に移動します。

1. 必要に応じてブラウザーを閉じ、Visual Studio ウィンドウに戻ります。 **[インデックス]** ページを更新して、 **[参照]** ページへのリンクを追加します。 この操作を行うには、**ソリューションエクスプローラー** **Views**  フォルダーを展開し、**Store** フォルダーをクリックして、**Index. cshtml** ページをダブルクリックします。
2. 選択したジャンルを示すリンクを参照ビューに追加します。 これを行うには、 **&lt;li&gt;** タグ内の強調表示されたC#次のコードを置き換えます。 ()

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample25.cshtml)]

   > [!NOTE]
   > 別の方法として、次のようなコードを使用して、ページに直接リンクすることもできます。
   > 
   > href =&quot;/Store/Browse? genre =@genreName&quot;&gt;@genreName&lt;/a &lt;&gt;
   > 
   > この方法は機能しますが、ハードコーディングされた文字列に依存します。 後でコントローラーの名前を変更する場合は、この手順を手動で変更する必要があります。 代わりに、 **HTML ヘルパー**メソッドを使用することをお勧めします。 ASP.NET MVC には、このようなタスクで使用できる HTML ヘルパーメソッドが含まれています。 **Html.actionlink ()** ヘルパーメソッドを使用すると、 **&gt;リンク&lt;** html を簡単に作成できるため、url パスが適切に url エンコードされます。
   > 
   > Html.actionlink にはいくつかのオーバーロードがあります。 この演習では、次の3つのパラメーターを受け取るものを使用します。
   > 
   > 1. ジャンル名を表示するリンクテキスト
   > 2. コントローラーアクション名 (**参照**)
   > 3. ルートパラメーターの値。名前 (**ジャンル**) と値 (**ジャンル名**) の両方を指定します。

<a id="Ex6Task9"></a>

<a id="Task_9_-_Running_the_Application"></a>
#### <a name="task-9---running-the-application"></a>タスク 9-アプリケーションを実行する

このタスクでは、各ジャンルが適切な **/Store/参照**URL へのリンクと共に表示されることをテストします。

1. **F5**キーを押してアプリケーションを実行します。
2. プロジェクトはホームページから開始します。 URL を **/Store**に変更して、各ジャンルが適切な **/** ストア URL にリンクされていることを確認します。

    ![閲覧ページへのリンクを使用したジャンルの参照](aspnet-mvc-4-fundamentals/_static/image33.png "閲覧ページへのリンクを使用したジャンルの参照")

    *閲覧ページへのリンクを使用したジャンルの参照*

<a id="Ex6Task10"></a>

<a id="Task_10_-_Using_Dynamic_ViewModel_Collection_to_Pass_Values"></a>
#### <a name="task-10---using-dynamic-viewmodel-collection-to-pass-values"></a>タスク 10-動的なビューモデルのコレクションを使用した値の引き渡し

このタスクでは、モデルを変更せずに、コントローラーとビューの間で値を渡すシンプルで強力な方法を学習します。 ASP.NET MVC 4 は、コレクション &quot;モデル&quot;を提供します。これを任意の動的な値に割り当てて、コントローラーやビュー内でアクセスすることもできます。

次に、ViewBag 動的コレクションを使用して、コントローラーからビューに &quot;**星付きジャンル**&quot; の一覧を渡します。 ストアインデックスビューは、ビュー**モデル**にアクセスして情報を表示します。

1. 必要に応じてブラウザーを閉じ、Visual Studio ウィンドウに戻ります。 **StoreController.cs**を開き、 **Index**メソッドを変更して、星付きジャンルのリストをビューモデルコレクションに作成します。

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample26.cs)]

    > [!NOTE]
    > また、構文**ViewBag [&quot;星付き&quot;]** を使用してプロパティにアクセスすることもできます。
2. このラボの**Source\Assets\Images**フォルダーには、**星付き&quot;&quot;** star アイコンが含まれています。 アプリケーションに追加するには、次に示すように、 **Windows エクスプローラー**ウィンドウから Visual Web Developer Express の**ソリューションエクスプローラー**にコンテンツをドラッグします。

    ![ソリューションへのスターイメージの追加](aspnet-mvc-4-fundamentals/_static/image34.png "ソリューションへのスターイメージの追加")

    *ソリューションへのスターイメージの追加*
3. ビュー**ストア/インデックス**を開き、内容を変更します。 **ViewBag**コレクションで &quot;星付き&quot; プロパティを読み取り、現在のジャンル名が一覧に含まれているかどうかを確認します。 その場合は、ジャンルのリンクに星のアイコンを表示します。
   (C#)

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample27.cshtml)]

<a id="Ex6Task11"></a>

<a id="Task_11_-_Running_the_Application"></a>
#### <a name="task-11---running-the-application"></a>タスク 11-アプリケーションを実行する

このタスクでは、星付きのジャンルに星のアイコンが表示されることをテストします。

1. **F5**キーを押してアプリケーションを実行します。
2. プロジェクトは**ホーム**ページから開始します。 URL を「 **/Store** 」に変更して、おすすめの各ジャンルに次のラベルが付いていることを確認します。

    ![星付き要素を使用したジャンルの参照](aspnet-mvc-4-fundamentals/_static/image35.png "星付き要素を使用したジャンルの参照")

    *星付き要素を使用したジャンルの参照*

<a id="Exercise7"></a>

<a id="Exercise_7_A_lap_around_ASPNET_MVC_4_new_template"></a>
### <a name="exercise-7-a-lap-around-aspnet-mvc-4-new-template"></a>演習 7: ASP.NET MVC 4 の新しいテンプレートをラップする

この演習では、ASP.NET MVC 4 プロジェクトテンプレートの機能強化について説明し、新しいテンプレートの最も関連する機能を見ていきます。

<a id="Ex7Task1"></a>

<a id="Task_1_Exploring_the_ASPNET_MVC_4_Internet_Application_Template"></a>
#### <a name="task-1-exploring-the-aspnet-mvc-4-internet-application-template"></a>タスク 1: ASP.NET MVC 4 インターネットアプリケーションテンプレートを探索する

1. まだ開いていない場合は、開始**VS Express for Web**
2. ファイルを選択してください **|新規 |[プロジェクト**] メニューコマンド。 **[新しいプロジェクト]** ダイアログで、[ **Visual C#|] を選択します。** 左側のウィンドウツリーで [Web テンプレート] を選択し、 **ASP.NET MVC 4 web アプリケーション**を選択します。 プロジェクトに*MusicStore*という**名前**を設定し、**ソリューション名**を*開始*するように更新してから、場所を選択して (または既定値のままにして)、[ **OK]** をクリックします。

    ![新しい ASP.NET MVC 4 プロジェクトを作成する](aspnet-mvc-4-fundamentals/_static/image36.png "新しい ASP.NET MVC 4 プロジェクトを作成する")

    *新しい ASP.NET MVC 4 プロジェクトを作成する*
3. **[New ASP.NET MVC 4 プロジェクト]** ダイアログボックスで、 **[インターネットアプリケーション]** プロジェクトテンプレートを選択し、 **[OK]** をクリックします。 ビューエンジンとして Razor または ASPX を選択できます。

    ![新しい ASP.NET MVC 4 インターネットアプリケーションを作成する](aspnet-mvc-4-fundamentals/_static/image37.png "新しい ASP.NET MVC 4 インターネットアプリケーションを作成する")

    *新しい ASP.NET MVC 4 インターネットアプリケーションを作成する*

    > [!NOTE]
    > Razor 構文は、ASP.NET MVC 3 で導入されました。 その目的は、ファイルで必要とされる文字数とキーストローク数を最小限に抑えることです。これにより、高速で滑らかなコーディングワークフローが可能になります。 既存 C#/VB (またはその他) を活用する razor 言語スキルと最高の HTML の構築ワークフローを有効にするテンプレート マークアップ構文を提供します。
4. **F5**キーを押してソリューションを実行し、更新されたテンプレートを確認します。 次の機能を確認できます。

    1. **モダンスタイルのテンプレート**

        テンプレートが更新され、最新のスタイルを提供しています。

        ![ASP.NET MVC 4 の再スタイル化テンプレート](aspnet-mvc-4-fundamentals/_static/image38.png "ASP.NET MVC 4 の再スタイル化テンプレート")

        *ASP.NET MVC 4 の再スタイル化テンプレート*
    2. **アダプティブレンダリング**

        ブラウザーウィンドウのサイズを変更し、ページレイアウトが新しいウィンドウサイズに動的に適応することを確認します。 これらのテンプレートでは、アダプティブレンダリング技法を使用して、デスクトップとモバイルの両方のプラットフォームで適切にレンダリングできます。カスタマイズは必要ありません。

        ![さまざまなブラウザーサイズでの ASP.NET MVC 4 プロジェクトテンプレート](aspnet-mvc-4-fundamentals/_static/image39.png "さまざまなブラウザーサイズでの ASP.NET MVC 4 プロジェクトテンプレート")

        *さまざまなブラウザーサイズでの ASP.NET MVC 4 プロジェクトテンプレート*
5. ブラウザーを閉じて、デバッガーを停止し、Visual Studio に戻ります。
6. これで、ソリューションを調査し、プロジェクトテンプレートで ASP.NET MVC 4 によって導入された新機能の一部を確認できます。

    ![ASP.NET MVC4 (プロジェクトテンプレート)](aspnet-mvc-4-fundamentals/_static/image40.png "ASP.NET MVC 4 インターネットアプリケーションプロジェクトテンプレート")

    *ASP.NET MVC 4 インターネットアプリケーションプロジェクトテンプレート*

   1. **HTML5 マークアップ**

       テンプレートビューを参照して新しいテーママークアップを確認します。たとえば、 **[ホーム]** フォルダー内の **[... cshtml]** ビューを開きます。

       ![新しいテンプレート、Razor および HTML5 マークアップの使用](aspnet-mvc-4-fundamentals/_static/image41.png "新しいテンプレート、Razor および HTML5 マークアップの使用")

       *新しいテンプレート、Razor および HTML5 マークアップの使用*
   2. **含まれている JavaScript ライブラリ**

      1. **jquery**: jquery は、HTML ドキュメントの走査、イベント処理、アニメーション化、および Ajax 相互作用を簡略化します。
      2. **JQUERY UI**: このライブラリは、Jquery JavaScript ライブラリ上に構築された低レベルの相互作用とアニメーション、高度な効果、および可能なウィジェットの抽象化を提供します。

         > [!NOTE]
         > [[http://docs.jquery.com/](http://docs.jquery.com/)](http://docs.jquery.com/)では、jQuery と jquery UI について学習できます。
      3. **KnockoutJS**: ASP.NET MVC 4 の既定のテンプレートに**KnockoutJS**が含まれるようになりました。 javascript と HTML を使用して、高度で応答性の高い web アプリケーションを作成することができます。 ASP.NET MVC 3 の場合と同様に、jQuery および jQuery UI ライブラリも ASP.NET MVC 4 に含まれています。

          > [!NOTE]
          > KnockOutJS library の詳細については、「 [http://learn.knockoutjs.com/](http://learn.knockoutjs.com/)」を参照してください。
      4. **Modernizr**: このライブラリは自動的に実行され、HTML5 および CSS3 テクノロジを使用するときに、サイトと古いブラウザーとの互換性を確保します。

          > [!NOTE]
          > Modernizr ライブラリの詳細については、「 [http://www.modernizr.com/](http://www.modernizr.com/)」を参照してください。
   3. **ソリューションに含まれる SimpleMembership**

       SimpleMembership は、前の ASP.NET ロールおよびメンバーシッププロバイダーシステムに代わるものとして設計されています。 これには、開発者が web ページをより柔軟にセキュリティで保護するための多くの新機能が用意されています。

       インターネットテンプレートでは、SimpleMembership を統合するためのいくつかの処理が既に完了しています。たとえば、AccountController は OAuthWebSecurity (OAuth アカウントの登録、ログイン、管理など) と Web セキュリティを使用するために準備されています。

       ![ソリューションに含まれる SimpleMembership](aspnet-mvc-4-fundamentals/_static/image42.png "ソリューションに含まれる SimpleMembership")

       *ソリューションに含まれる SimpleMembership*

       > [!NOTE]
       > [Oauthwebsecurity](https://msdn.microsoft.com/library/jj158393(v=vs.111).aspx)の詳細については、MSDN を参照してください。

> [!NOTE]
> また、 [「付録 B: Web 配置を使用した ASP.NET MVC 4 アプリケーションの発行](#AppendixB)」に従って、このアプリケーションを Windows Azure の Web サイトにデプロイすることもできます。

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a>まとめ

このハンズオンラボを完了することで、ASP.NET MVC の基本を学習できました。

- MVC アプリケーションのコア要素とその相互作用
- ASP.NET MVC アプリケーションを作成する方法
- URL と querystring を通じて渡されるパラメーターを処理するようにコントローラーを追加および構成する方法
- 共通の HTML コンテンツ用のテンプレートを設定するためのレイアウトマスターページの追加方法、外観を強化するためのスタイルシート、および HTML コンテンツを表示するためのビューテンプレート
- ビューテンプレートにプロパティを渡して動的な情報を表示するために、ビューモデルパターンを使用する方法
- ビューテンプレートでコントローラーに渡されるパラメーターの使用方法
- ASP.NET MVC アプリケーション内のページにリンクを追加する方法
- ビューに動的プロパティを追加して使用する方法
- ASP.NET MVC 4 プロジェクトテンプレートの機能強化

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>付録 A: Visual Studio Express 2012 を Web 用にインストールする

**[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)** を使用して、Web または別の &quot;Express&quot; バージョン**用に Microsoft Visual Studio Express 2012**をインストールできます。 次の手順では、 *Microsoft Web Platform Installer*を使用して*Visual studio Express 2012 for Web*をインストールするために必要な手順について説明します。

1. [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)にアクセスします。 または、Web Platform Installer が既にインストールされている場合は、それを開いて、製品 &quot;<em>Visual Studio Express 2012 For web With Windows AZURE SDK</em>&quot;を検索することもできます。
2. **[今すぐインストール]** をクリックします。 **Web Platform Installer**がない場合は、最初にダウンロードしてインストールするようにリダイレクトされます。
3. **Web Platform Installer**が開いたら、 **[インストール]** をクリックしてセットアップを開始します。

    ![Visual Studio Express のインストール](aspnet-mvc-4-fundamentals/_static/image43.png "Visual Studio Express のインストール")

    *Visual Studio Express のインストール*
4. すべての製品のライセンスと条項を読み、[**同意**する] をクリックして続行します。

    ![ライセンス条項に同意する](aspnet-mvc-4-fundamentals/_static/image44.png)

    *ライセンス条項に同意する*
5. ダウンロードとインストールのプロセスが完了するまで待ちます。

    ![Installation progress](aspnet-mvc-4-fundamentals/_static/image45.png)

    *インストールの進行状況*
6. インストールが完了したら、 **[完了]** をクリックします。

    ![インストールの完了](aspnet-mvc-4-fundamentals/_static/image46.png)

    *インストールの完了*
7. **[終了]** をクリックして Web Platform Installer を閉じます。
8. Web 用の Visual Studio Express を開くには、**スタート**画面にアクセスして &quot;**VS Express**&quot;の書き込みを開始し、 **[VS Express for Web]** タイルをクリックします。

    ![VS Express for Web タイル](aspnet-mvc-4-fundamentals/_static/image47.png)

    *VS Express for Web タイル*

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>付録 B: Web 配置を使用した ASP.NET MVC 4 アプリケーションの発行

この付録では、windows azure 管理ポータルから新しい web サイトを作成し、Windows Azure によって提供される Web 配置公開機能を活用して、ラボに従って取得したアプリケーションを発行する方法について説明します。

<a id="ApxBTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a>タスク 1-Windows Azure ポータルから新しい Web サイトを作成する

1. [Windows Azure 管理ポータル](https://manage.windowsazure.com/)にアクセスし、サブスクリプションに関連付けられている Microsoft 資格情報を使用してサインインします。

    > [!NOTE]
    > Windows Azure では、10 ASP.NET の Web サイトを無料でホストし、トラフィックの増加に合わせて拡張できます。 [ここで](https://aka.ms/aspnet-hol-azure)サインアップできます。

    ![Windows Azure portal にログオンします。](aspnet-mvc-4-fundamentals/_static/image48.png "Windows Azure portal にログオンします。")

    *Windows Azure 管理ポータルにログオンします。*
2. コマンドバーの **[新規]** をクリックします。

    ![新しい Web サイトの作成](aspnet-mvc-4-fundamentals/_static/image49.png "新しい Web サイトの作成")

    *新しい Web サイトの作成*
3. [ **Compute** | **Web サイト**] をクリックします。 次に、 **[簡易作成]** オプションを選択します。 新しい web サイトの使用可能な URL を指定し、 **[Web サイトの作成]** をクリックします。

    > [!NOTE]
    > Windows Azure の Web サイトは、制御および管理が可能なクラウドで実行されている web アプリケーションのホストです。 [簡易作成] オプションを使用すると、完成した web アプリケーションをポータルの外部から Windows Azure の Web サイトにデプロイできます。 データベースを設定する手順は含まれていません。

    ![簡易作成を使用した新しい Web サイトの作成](aspnet-mvc-4-fundamentals/_static/image50.png "簡易作成を使用した新しい Web サイトの作成")

    *簡易作成を使用した新しい Web サイトの作成*
4. 新しい**Web サイト**が作成されるまで待ちます。
5. Web サイトが作成されたら、 **[URL]** 列の下のリンクをクリックします。 新しい Web サイトが機能していることを確認します。

    ![新しい web サイトを参照しています](aspnet-mvc-4-fundamentals/_static/image51.png "新しい web サイトを参照しています")

    *新しい web サイトを参照しています*

    ![実行中の Web サイト](aspnet-mvc-4-fundamentals/_static/image52.png "実行中の Web サイト")

    *実行中の Web サイト*
6. ポータルに戻り、 **[名前]** 列の下にある web サイトの名前をクリックして、管理ページを表示します。

    ![Web サイトの管理ページを開く](aspnet-mvc-4-fundamentals/_static/image53.png "Web サイトの管理ページを開く")

    *Web サイトの管理ページを開く*
7. **[ダッシュボード]** ページの **[概要] セクションで**、 **[発行プロファイルのダウンロード]** リンクをクリックします。

    > [!NOTE]
    > *発行プロファイル*には、有効になっている各発行方法について、Windows Azure web サイトに web アプリケーションを発行するために必要なすべての情報が含まれています。 発行プロファイルには、発行メソッドが有効化される各エンドポイントに接続して認証するために必要な URL、ユーザーの資格情報、およびデータベース文字列が含まれています。 **Microsoft WebMatrix 2**、 **Microsoft Visual Studio Express for Web**および**Microsoft Visual Studio 2012**では、発行プロファイルを読み取り、Web アプリケーションを Windows Azure websites に発行するためのこれらのプログラムの構成を自動化することがサポートされています。

    ![Web サイト発行プロファイルをダウンロードしています](aspnet-mvc-4-fundamentals/_static/image54.png "Web サイト発行プロファイルをダウンロードしています")

    *Web サイト発行プロファイルをダウンロードしています*
8. 発行プロファイルファイルを既知の場所にダウンロードします。 この演習では、このファイルを使用して、Visual Studio から Windows Azure Web サイトに web アプリケーションを発行する方法について説明します。

    ![発行プロファイルファイルを保存しています](aspnet-mvc-4-fundamentals/_static/image55.png "発行プロファイルを保存しています")

    *発行プロファイルファイルを保存しています*

<a id="ApxBTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a>タスク 2-データベースサーバーの構成

アプリケーションで SQL Server データベースを使用する場合は、SQL Database サーバーを作成する必要があります。 SQL Server を使用しない単純なアプリケーションを展開する場合は、このタスクを省略できます。

1. アプリケーションデータベースを格納するには、SQL Database サーバーが必要です。 サブスクリプションの**SQL Database サーバーは**、Windows Azure 管理ポータルの**SQL データベース** | サーバー | **サーバーのダッシュボード**で確認できます。 サーバーを作成していない場合は、コマンドバーの **[追加]** ボタンを使用して作成できます。 次のタスクで使用するので、**サーバー名と URL、管理者のログイン名、パスワード**をメモしておきます。 データベースは、後の段階で作成されるため、まだ作成しないでください。

    ![SQL Database サーバーダッシュボード](aspnet-mvc-4-fundamentals/_static/image56.png "SQL Database サーバーダッシュボード")

    *SQL Database サーバーダッシュボード*
2. 次のタスクでは、Visual Studio からデータベース接続をテストします。そのため、**使用可能な Ip アドレス**の一覧にローカル ip アドレスを含める必要があります。 これを行うには、 **[構成]** をクリックし、 **[現在のクライアント IP アドレス]** の ip アドレスを選択して、 **[開始 Ip アドレス]** と **[終了 ip アドレス]** のテキストボックスに貼り付け、[![の](aspnet-mvc-4-fundamentals/_static/image57.png) 追加] をクリックします。

    ![クライアント IP アドレスを追加しています](aspnet-mvc-4-fundamentals/_static/image58.png)

    *クライアント IP アドレスを追加しています*
3. [許可された IP アドレス] の一覧に**クライアントの Ip アドレス**が追加されたら、 **[保存]** をクリックして変更を確認します。

    ![変更の確認](aspnet-mvc-4-fundamentals/_static/image59.png)

    *変更の確認*

<a id="ApxBTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>タスク 3-Web 配置を使用した ASP.NET MVC 4 アプリケーションの発行

1. ASP.NET MVC 4 ソリューションに戻ります。 **ソリューションエクスプローラー**で、web サイトプロジェクトを右クリックし、 **[発行]** を選択します。

    ![アプリケーションの発行](aspnet-mvc-4-fundamentals/_static/image60.png "アプリケーションの発行")

    *Web サイトの公開*
2. 最初のタスクで保存した発行プロファイルをインポートします。

    ![発行プロファイルをインポートしています](aspnet-mvc-4-fundamentals/_static/image61.png "発行プロファイルをインポートしています")

    *発行プロファイルをインポートしています*
3. **[接続の検証]** をクリックします。 検証が完了したら、 **[次へ]** をクリックします。

    > [!NOTE]
    > 検証が完了すると、[接続の検証] ボタンの横に緑色のチェックマークが表示されます。

    ![接続の検証](aspnet-mvc-4-fundamentals/_static/image62.png "接続の検証")

    *接続の検証*
4. **[設定]** ページの **[データベース]** セクションで、データベース接続のテキストボックスの横にあるボタン ( **defaultconnection**など) をクリックします。

    ![Web deploy の構成](aspnet-mvc-4-fundamentals/_static/image63.png "Web deploy の構成")

    *Web deploy の構成*
5. 次のようにデータベース接続を構成します。

   - **サーバー名**には、 *tcp:* プレフィックスを使用して SQL Database サーバーの URL を入力します。
   - **User name (ユーザー名**) に、サーバー管理者のログイン名を入力します。
   - **パスワード**で、サーバー管理者のログインパスワードを入力します。
   - 新しいデータベース名を入力します (例: *MVC4SampleDB*)。

     ![変換先の接続文字列を構成しています](aspnet-mvc-4-fundamentals/_static/image64.png "変換先の接続文字列を構成しています")

     *変換先の接続文字列を構成しています*
6. 次に、 **[OK]** をクリックします データベースの作成を求めるメッセージが表示されたら、[**はい]** をクリックします。

    ![データベースの作成](aspnet-mvc-4-fundamentals/_static/image65.png "データベース文字列の作成")

    *データベースの作成*
7. Windows Azure の SQL Database に接続するために使用する接続文字列は、[既定の接続] ボックスに表示されます。 続けて、 **[次へ]** をクリックします。

    ![SQL Database を指す接続文字列](aspnet-mvc-4-fundamentals/_static/image66.png "SQL Database を指す接続文字列")

    *SQL Database を指す接続文字列*
8. **[プレビュー]** ページで、 **[発行]** をクリックします。

    ![Web アプリケーションの発行](aspnet-mvc-4-fundamentals/_static/image67.png "Web アプリケーションの発行")

    *Web アプリケーションの発行*
9. 発行プロセスが完了すると、既定のブラウザーによって公開された web サイトが開きます。

    ![Windows Azure に発行されたアプリケーション](aspnet-mvc-4-fundamentals/_static/image68.png "Windows Azure に発行されたアプリケーション")

    *Windows Azure に発行されたアプリケーション*

<a id="AppendixC"></a>

<a id="Appendix_C_Using_Code_Snippets"></a>
## <a name="appendix-c-using-code-snippets"></a>付録 C: コードスニペットの使用

コードスニペットを使用すると、必要なすべてのコードをすぐに利用できます。 次の図に示すように、ラボドキュメントには、使用できるタイミングがわかります。

![Visual Studio のコードスニペットを使用してプロジェクトにコードを挿入する](aspnet-mvc-4-fundamentals/_static/image69.png "Visual Studio のコードスニペットを使用してプロジェクトにコードを挿入する")

*Visual Studio のコードスニペットを使用してプロジェクトにコードを挿入する*

***キーボードを使用してコードスニペットを追加C#するには (のみ)***

1. コードを挿入する場所にカーソルを置きます。
2. (スペースまたはハイフンを含まない) スニペット名の入力を開始します。
3. IntelliSense によって、一致するスニペットの名前が表示されます。
4. 正しいスニペットを選択します (または、スニペットの名前全体が選択されるまで入力し続けます)。
5. Tab キーを2回押すと、スニペットがカーソル位置に挿入されます。

![スニペット名の入力を開始します](aspnet-mvc-4-fundamentals/_static/image70.png "スニペット名の入力を開始します")

*スニペット名の入力を開始します*

![Tab キーを押して、強調表示されているスニペットを選択します](aspnet-mvc-4-fundamentals/_static/image71.png "Tab キーを押して、強調表示されているスニペットを選択します")

*Tab キーを押して、強調表示されているスニペットを選択します*

![もう一度 Tab キーを押すと、スニペットが展開されます。](aspnet-mvc-4-fundamentals/_static/image72.png "もう一度 Tab キーを押すと、スニペットが展開されます。")

*もう一度 Tab キーを押すと、スニペットが展開されます。*

***マウスC#(、Visual Basic および XML) を使用してコードスニペットを追加するに***は1. コードスニペットを挿入する場所を右クリックします。

1. **[スニペットの挿入]** 、 **[マイコードスニペット**] の順に選択します。
2. 一覧から該当するスニペットをクリックして選択します。

![コードスニペットを挿入する場所を右クリックし、[スニペットの挿入] を選択します。](aspnet-mvc-4-fundamentals/_static/image73.png "コードスニペットを挿入する場所を右クリックし、[スニペットの挿入] を選択します。")

*コードスニペットを挿入する場所を右クリックし、[スニペットの挿入] を選択します。*

![一覧から関連するスニペットをクリックして選択します。](aspnet-mvc-4-fundamentals/_static/image74.png "一覧から関連するスニペットをクリックして選択します。")

*一覧から関連するスニペットをクリックして選択します。*
