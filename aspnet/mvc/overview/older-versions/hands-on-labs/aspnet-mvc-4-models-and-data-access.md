---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-models-and-data-access
title: ASP.NET MVC 4 のモデルとデータアクセス |Microsoft Docs
author: rick-anderson
description: '注: このハンズオンラボでは、ASP.NET MVC に関する基本的な知識があることを前提としています。 ASP.NET MVC を以前に使用したことがない場合は、ASP.NET MVC 4...'
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 634ea84b-f904-4afe-b71b-49cccef4d9cc
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-models-and-data-access
msc.type: authoredcontent
ms.openlocfilehash: 90635b617930d0a9c126795f4c8790d542e33dc9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78451468"
---
# <a name="aspnet-mvc-4-models-and-data-access"></a>ASP.NET MVC 4 モデルとデータ アクセス

[Web キャンプチーム](https://twitter.com/webcamps)別

[Web キャンプトレーニングキットをダウンロードする](https://aka.ms/webcamps-training-kit)

このハンズオンラボでは、 **ASP.NET MVC**に関する基本的な知識があることを前提としています。 以前に**ASP.NET mvc**を使用していない場合は、 **ASP.NET Mvc 4 の基礎**となるハンズオンラボに進むことをお勧めします。

このラボでは、ソースフォルダーに用意されているサンプル Web アプリケーションに軽微な変更を適用することによって前述した機能強化と新機能について説明します。

> [!NOTE]
> すべてのサンプルコードとスニペットは、 [Microsoft web/WebCampTrainingKit リリース](https://aka.ms/webcamps-training-kit)で入手できる Web キャンプトレーニングキットに含まれています。 このラボに固有のプロジェクトについては、「 [ASP.NET MVC 4 のモデルとデータアクセス](https://github.com/Microsoft-Web/HOL-MVC4ModelsAndDataAccess)」を参照してください。

**ASP.NET MVC の基礎**ハンズオンラボでは、コントローラーからビューテンプレートにハードコーディングされたデータを渡しています。 しかし、実際の Web アプリケーションを構築するためには、実際のデータベースを使用することが必要になる場合があります。

このハンズオンラボでは、データベースエンジンを使用して、Music ストアアプリケーションに必要なデータを格納および取得する方法について説明します。 これを実現するには、既存のデータベースから開始し、そこから Entity Data Model を作成します。 このラボ全体では、 **Database First**アプローチと、 **Code First**アプローチを満たすことができます。

ただし、 **Model First**方法を使用して、ツールを使用して同じモデルを作成し、そのモデルからデータベースを生成することもできます。

![Database First と Model First](aspnet-mvc-4-models-and-data-access/_static/image1.png "Database First と Model First")

*Database First と Model First*

モデルを生成した後は、ハードコーディングされたデータを使用するのではなく、データベースから取得したデータをストアビューに提供するために、StoreController に適切な調整を行います。 ビューテンプレートを変更する必要はありません。これは、StoreController がビューテンプレートに対して同じ Viewmodel を返すためです。ただし、この時点では、データはデータベースから取得されます。

**Code First アプローチ**

Code First アプローチを使用すると、一般的にフレームワークと結合されたクラスを生成することなく、コードからモデルを定義できます。

Code first では、モデルオブジェクトは POCOs を使用して定義されています。 &quot;Plain Old CLR Objects&quot;です。 POCOs は、継承されず、インターフェイスを実装しない単純なプレーンクラスです。 データベースを自動的に生成することも、既存のデータベースを使用してコードからクラスのマッピングを生成することもできます。

この方法を使用する利点は、POCOs クラスがマッピングフレームワークと結合されていないため、モデルが永続化フレームワーク (この場合は Entity Framework) とは独立していることです。

> [!NOTE]
> このラボは、ASP.NET MVC 4 と、このハンズオンラボに示されている機能だけに合わせてカスタマイズおよび最小化されたバージョンのミュージックストアサンプルアプリケーションに基づいています。
> 
> **音楽ストア**のチュートリアルアプリケーション全体を調べる場合は、「 [MVC-music-ストア](https://github.com/evilDave/MVC-Music-Store)」で見つけることができます。

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>前提条件

このラボを完了するには、次の項目が必要です。

- Web またはそれ以降[の2012を Microsoft Visual Studio Express](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web)ます (付録 a をインストールする手順については[、「付録 a](#AppendixA) 」を参照してください)。

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a>セットアップ

**コードスニペットのインストール**

便宜上、このラボで管理するコードの多くは、Visual Studio のコードスニペットとして提供されています。 コードスニペットをインストールするには、 **.\Source\Setup\CodeSnippets.vsi**ファイルを実行します。

Visual Studio Code のスニペットを使い慣れておらず、その使用方法を学習したい場合は、この &quot;ドキュメントの付録「[付録 C: コードスニペットの使用](#AppendixC)&quot;」を参照してください。

---

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a>手順

このハンズオンラボは、次の演習によって構成されています。

1. [演習 1: データベースの追加](#Exercise1)
2. [演習 2: Code First を使用したデータベースの作成](#Exercise2)
3. [演習 3: パラメーターを使用してデータベースにクエリを実行する](#Exercise3)

> [!NOTE]
> 各演習には、演習を完了した後に取得する必要があるソリューションを含む**終了**フォルダーが付属しています。 演習を通じて追加のヘルプが必要な場合は、このソリューションをガイドとして使用できます。

このラボの推定所要時間: **35 分**。

<a id="Exercise1"></a>

<a id="Exercise_1_Adding_a_Database"></a>
### <a name="exercise-1-adding-a-database"></a>演習 1: データベースの追加

この演習では、データを使用するために、MusicStore アプリケーションのテーブルを含むデータベースをソリューションに追加する方法について説明します。 モデルを使用してデータベースを生成し、ソリューションに追加したら、StoreController クラスを変更して、ハードコーディングされた値を使用するのではなく、データベースから取得したデータをビューテンプレートに提供します。

<a id="Ex1Task1"></a>

<a id="Task_1_-_Adding_a_Database"></a>
#### <a name="task-1---adding-a-database"></a>タスク 1-データベースの追加

このタスクでは、MusicStore アプリケーションのメインテーブルを持つ作成済みのデータベースをソリューションに追加します。

1. **Source/Ex1-AddingADatabaseDBFirst/begin/** folder にある**begin**ソリューションを開きます。

   1. 続行する前に、不足している NuGet パッケージをダウンロードする必要があります。 これを行うには、 **[プロジェクト]** メニューをクリックし、 **[NuGet パッケージの管理]** を選択します。
   2. **[NuGet パッケージの管理]** ダイアログで、 **[復元]** をクリックして、不足しているパッケージをダウンロードします。
   3. 最後に、[**ビルド** | **ビルド**] をクリックしてソリューションをビルドします。

      > [!NOTE]
      > NuGet を使用する利点の1つは、プロジェクトのすべてのライブラリを配布する必要がなく、プロジェクトのサイズを小さくすることです。 NuGet パワーツールを使用すると、パッケージのバージョンを app.config ファイルで指定することで、プロジェクトを初めて実行するときに必要なすべてのライブラリをダウンロードできます。 このため、このラボから既存のソリューションを開いた後に、これらの手順を実行する必要があります。
2. **MvcMusicStore**データベースファイルを追加します。 このハンズオンラボでは、 **MvcMusicStore**という名前の作成済みのデータベースを使用します。 これを行うには、[**アプリ\_データ**フォルダー] を右クリックし、 **[追加]** をポイントして、 **[既存の項目]** をクリックします。 **MvcMusicStore**ファイルを参照**して選択します**。

    ![既存の項目の追加](aspnet-mvc-4-models-and-data-access/_static/image2.png "既存の項目の追加")

    *既存の項目の追加*

    ![MvcMusicStore データベースファイル](aspnet-mvc-4-models-and-data-access/_static/image3.png "MvcMusicStore データベースファイル")

    *MvcMusicStore データベースファイル*

    データベースがプロジェクトに追加されました。 データベースがソリューション内に配置されている場合でも、別のデータベースサーバーでホストされているときにクエリを実行し、データベースを更新することができます。

    ![ソリューションエクスプローラーの MvcMusicStore データベース](aspnet-mvc-4-models-and-data-access/_static/image4.png "ソリューションエクスプローラーの MvcMusicStore データベース")

    *ソリューションエクスプローラーの MvcMusicStore データベース*
3. データベースへの接続を確認します。 これを行うには、 **MvcMusicStore**をダブルクリックして接続を確立します。

    ![MvcMusicStore への接続](aspnet-mvc-4-models-and-data-access/_static/image5.png "MvcMusicStore への接続")

    *MvcMusicStore への接続*

<a id="Ex1Task2"></a>

<a id="Task_2_-_Creating_a_Data_Model"></a>
#### <a name="task-2---creating-a-data-model"></a>タスク 2-データモデルの作成

このタスクでは、前のタスクで追加したデータベースと対話するデータモデルを作成します。

1. データベースを表すデータモデルを作成します。 これを行うにはソリューションエクスプローラー **[モデル]** フォルダーを右クリックし、 **[追加]** をポイントして、 **[新しい項目]** をクリックします。 **[新しい項目の追加]** ダイアログで、 **[データ]** テンプレートを選択し、 **[ADO.NET Entity Data Model]** 項目を選択します。 データモデル名を「 **Storedb. .edmx** 」に変更し、 **[追加]** をクリックします。

    ![StoreDB ADO.NET Entity Data Model の追加](aspnet-mvc-4-models-and-data-access/_static/image6.png "StoreDB ADO.NET Entity Data Model の追加")

    *StoreDB ADO.NET Entity Data Model の追加*
2. **Entity Data Model ウィザード**が表示されます。 このウィザードの手順に従って、モデルレイヤーを作成できます。 最近追加された既存のデータベースに基づいてモデルを作成する必要があるため、 **[データベースから生成]** を選択し、 **[次へ]** をクリックします。

    ![モデルコンテンツの選択](aspnet-mvc-4-models-and-data-access/_static/image7.png "モデルコンテンツの選択")

    *モデルコンテンツの選択*
3. データベースからモデルを生成するため、使用する接続を指定する必要があります。 **[新しい接続]** をクリックします。
4. **Microsoft SQL Server データベースファイル**を選択し、 **[続行]** をクリックします。

    ![データソースの選択](aspnet-mvc-4-models-and-data-access/_static/image8.png "データソースの選択")

    *[データソースの選択] ダイアログ*
5. **[参照]** をクリックし、 **App\_Data**フォルダーにあるデータベース**MvcMusicStore**を選択し、[ **OK]** をクリックします。

    ![接続プロパティ](aspnet-mvc-4-models-and-data-access/_static/image9.png "接続のプロパティ")

    *接続プロパティ*
6. 生成されるクラスは、エンティティ接続文字列と同じ名前にする必要があります。そのため、名前を**MusicStoreEntities**に変更し、 **[次へ]** をクリックしてください。

    ![データ接続の選択](aspnet-mvc-4-models-and-data-access/_static/image10.png "データ接続の選択")

    *データ接続の選択*
7. 使用するデータベースオブジェクトを選択します。 エンティティモデルではデータベースのテーブルのみを使用するので、 **[テーブル]** オプションを選択し、[モデルおよび**複数化または単数のオブジェクト名**を**含む外部キー列を含める**] オプションも選択されていることを確認します。 モデルの名前空間を**MvcMusicStore**に変更し、 **[完了]** をクリックします。

    ![データベースオブジェクトの選択](aspnet-mvc-4-models-and-data-access/_static/image11.png "データベースオブジェクトの選択")

    *データベースオブジェクトの選択*

    > [!NOTE]
    > セキュリティ警告ダイアログが表示された場合は、 **[OK]** をクリックしてテンプレートを実行し、モデルエンティティのクラスを生成します。
8. データベースのエンティティダイアグラムが表示され、各テーブルをデータベースにマップする個別のクラスが作成されます。 たとえば **、アルバムのテーブルは** **アルバム**クラスによって表され、テーブル内の各列はクラスのプロパティにマップされます。 これにより、データベース内の行を表すオブジェクトを照会して操作できるようになります。

    ![エンティティダイアグラム](aspnet-mvc-4-models-and-data-access/_static/image12.png "エンティティ図")

    *エンティティダイアグラム*

    > [!NOTE]
    > T4 テンプレート (.tt) は、エンティティクラスを生成するコードを実行し、同じ名前の既存のクラスを上書きします。 この例では、クラス &quot;アルバム&quot;、&quot;Genre&quot;、および &quot;アーティスト&quot; が生成されたコードで上書きされています。

<a id="Ex1Task3"></a>

<a id="Task_3_-_Building_the_Application"></a>
#### <a name="task-3---building-the-application"></a>タスク 3-アプリケーションのビルド

このタスクでは、モデルの生成によって**アルバム**、**ジャンル**、および**アーティスト**モデルクラスが削除されましたが、新しいデータモデルクラスを使用してプロジェクトが正常にビルドされることを確認します。

1. **[ビルド]** メニュー項目を選択し、 **[MvcMusicStore のビルド]** をクリックして、プロジェクトをビルドします。

    ![プロジェクトのビルド](aspnet-mvc-4-models-and-data-access/_static/image13.png "プロジェクトのビルド")

    *プロジェクトのビルド*
2. プロジェクトが正常にビルドされました。 まだ機能しているのはなぜですか。 データベーステーブルには、削除されたクラスの**アルバム**および**ジャンル**で使用していたプロパティを含むフィールドがあるため、機能します。

    ![成功したビルド](aspnet-mvc-4-models-and-data-access/_static/image14.png "成功したビルド")

    *成功したビルド*
3. エンティティは、デザイナーによってダイアグラム形式で表示されますC#が、実際にはクラスです。 ソリューションエクスプローラーで **[Storedb. .edmx]** ノードを展開し、 **StoreDB.tt**をクリックすると、新しく生成されたエンティティが表示されます。

    ![生成されたファイル](aspnet-mvc-4-models-and-data-access/_static/image15.png "生成されたファイル")

    *生成されたファイル*

<a id="Ex1Task4"></a>

<a id="Task_4_-_Querying_the_Database"></a>
#### <a name="task-4---querying-the-database"></a>タスク 4-データベースに対してクエリを実行する

このタスクでは、StoreController クラスを更新します。これにより、ハードコードされたデータを使用するのではなく、データベースにクエリを実行して情報を取得します。

1. **Controllers\StoreController.cs**を開き、次のフィールドをクラスに追加して、 **storedb**という名前の**MusicStoreEntities**クラスのインスタンスを保持します。

    (コードスニペット-*モデルとデータアクセス-Ex1 storeDB*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample1.cs)]
2. **MusicStoreEntities**クラスは、データベース内の各テーブルのコレクションプロパティを公開します。 すべての**アルバム**を含むジャンルを取得するように、**参照**アクションメソッドを更新します。

    (コードスニペット-*モデルとデータアクセス-Ex1 Store 参照*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample2.cs)]

    > [!NOTE]
    > **LINQ** (統合言語クエリ) と呼ばれる .net の機能を使用して、これらのコレクションに対して厳密に型指定されたクエリ式を作成します。このようなコレクションは、データベースに対してコードを実行し、プログラミングできるオブジェクトを返します。
    > 
    > LINQ の詳細については、 [msdn サイト](https://msdn.microsoft.com/library/bb397926&amp;#040;v=vs.110&amp;#041;.aspx)を参照してください。
3. すべてのジャンルを取得するように**インデックス**アクションメソッドを更新します。

    (コードスニペット-*モデルとデータアクセス-Ex1 Store Index*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample3.cs)]
4. **インデックス**アクションメソッドを更新してすべてのジャンルを取得し、コレクションをリストに変換します。

    (コードスニペット-*モデルとデータアクセス-Ex1 Store GenreMenu*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample4.cs)]

<a id="Ex1Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a>タスク 5-アプリケーションを実行する

このタスクでは、ハードコードされたものではなく、データベースに格納されているジャンルが [ストアインデックス] ページに表示されることを確認します。 **StoreController**が以前と同じエンティティを返すため、ビューテンプレートを変更する必要はありません。ただし、この時点では、データはデータベースから取得されます。

1. ソリューションをリビルドし、 **F5**キーを押してアプリケーションを実行します。
2. プロジェクトはホームページから開始します。 **ジャンル**のメニューがハードコードされた一覧ではなくなり、データがデータベースから直接取得されていることを確認します。

    ![BrowsingGenresFromDataBase](aspnet-mvc-4-models-and-data-access/_static/image16.png)

    *データベースからのジャンルの参照*
3. 次に、任意のジャンルを参照し、アルバムにデータベースが設定されていることを確認します。

    ![データベースからのアルバムの参照](aspnet-mvc-4-models-and-data-access/_static/image17.png "データベースからのアルバムの参照")

    *データベースからのアルバムの参照*

<a id="Exercise2"></a>

<a id="Exercise_2_Creating_a_Database_Using_Code_First"></a>
### <a name="exercise-2-creating-a-database-using-code-first"></a>演習 2: Code First を使用したデータベースの作成

この演習では、Code First 方法を使用して、MusicStore アプリケーションのテーブルを含むデータベースを作成し、そのデータにアクセスする方法を学習します。

モデルが生成されたら、StoreController を変更して、ハードコーディングされた値を使用するのではなく、データベースから取得したデータをビューテンプレートに提供します。

> [!NOTE]
> 演習1を完了し、既に Database First 方法を使用していた場合は、別のプロセスで同じ結果を得る方法について学習します。 演習1でよく使用されているタスクは、読みやすくするようにマークされています。 演習1を完了していないが Code First アプローチについて学習したい場合は、この演習を開始して、トピック全体を網羅することができます。

<a id="Ex2Task1"></a>

<a id="Task_1_-_Populating_Sample_Data"></a>
#### <a name="task-1---populating-sample-data"></a>タスク 1-サンプルデータの設定

このタスクでは、最初にコードを使用して作成されたときに、サンプルデータをデータベースに設定します。

1. **Source/Ex2-CreatingADatabaseCodeFirst/begin/** folder にある**begin**ソリューションを開きます。 それ以外の場合は、前の演習を完了することによって得られた**終了**ソリューションを引き続き使用することができます。

   1. 提供された**Begin**ソリューションを開いた場合は、続行する前に、不足している NuGet パッケージをダウンロードする必要があります。 これを行うには、 **[プロジェクト]** メニューをクリックし、 **[NuGet パッケージの管理]** を選択します。
   2. **[NuGet パッケージの管理]** ダイアログで、 **[復元]** をクリックして、不足しているパッケージをダウンロードします。
   3. 最後に、[**ビルド** | **ビルド**] をクリックしてソリューションをビルドします。

      > [!NOTE]
      > NuGet を使用する利点の1つは、プロジェクトのすべてのライブラリを配布する必要がなく、プロジェクトのサイズを小さくすることです。 NuGet パワーツールを使用すると、パッケージのバージョンを app.config ファイルで指定することで、プロジェクトを初めて実行するときに必要なすべてのライブラリをダウンロードできます。 このため、このラボから既存のソリューションを開いた後に、これらの手順を実行する必要があります。
2. **SampleData.cs**ファイルを **[モデル]** フォルダーに追加します。 これを行うには、 **[モデル]** フォルダーを右クリックし、 **[追加]** をポイントして、 **[既存の項目]** をクリックします。 **SampleData.cs**ファイルを参照**して選択します**。

    ![サンプルデータのコードの入力](aspnet-mvc-4-models-and-data-access/_static/image18.png "サンプルデータのコードの入力")

    *サンプルデータのコードの入力*
3. **Global.asax.cs**ファイルを開き、次の*using*ステートメントを追加します。

    (コードスニペット-*モデルとデータアクセス-Ex2 Global Global.asax using*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample5.cs)]
4. **Application\_Start ()** メソッドで、次の行を追加してデータベース初期化子を設定します。

    (コードスニペット-*モデルとデータアクセス-Ex2 Global Global.asax SetInitializer*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample6.cs)]

<a id="Ex2Task2"></a>

<a id="Task_2_-_Configuring_the_connection_to_the_Database"></a>
#### <a name="task-2---configuring-the-connection-to-the-database"></a>タスク 2-データベースへの接続の構成

プロジェクトにデータベースを既に追加したので、接続文字列を**web.config ファイルに記述します。**

1. **Web.config に接続**文字列を追加します。これを行うには、プロジェクトのルート**で web.config を開き、** defaultconnection という名前の接続文字列を **&lt;connectionStrings&gt;** セクションの次の行に置き換えます。

    ![Web.config ファイルの場所](aspnet-mvc-4-models-and-data-access/_static/image19.png "Web.config ファイルの場所")

    *Web.config ファイルの場所*

    [!code-xml[Main](aspnet-mvc-4-models-and-data-access/samples/sample7.xml)]

<a id="Ex2Task3"></a>

<a id="Task_3_-_Working_with_the_Model"></a>
#### <a name="task-3---working-with-the-model"></a>タスク 3-モデルの操作

これで、データベースへの接続が既に構成されているので、モデルをデータベーステーブルにリンクします。 このタスクでは、Code First を使用してデータベースにリンクされるクラスを作成します。 変更する必要がある POCO モデルクラスが存在することに注意してください。

> [!NOTE]
> 演習1を完了した場合は、ウィザードによってこの手順が実行されたことに注意してください。 Code First には、データエンティティにリンクされるクラスを手動で作成します。

1. **モデル**プロジェクトフォルダーから POCO モデルクラスの**ジャンル**を開き、ID を含めます。 **Genreid**という名前の int プロパティを使用します。

    (コードスニペット-*モデルとデータアクセス-Ex2 Code First Genre*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample8.cs)]

    > [!NOTE]
    > Code First 規則を使用するには、クラス Genre に自動的に検出される主キープロパティが必要です。
    > 
    > Code First の規則の詳細については、この[msdn の記事](https://msdn.microsoft.com/library/hh161541&amp;#040;v=vs.103&amp;#041;.aspx)を参照してください。
2. 次に、**モデル**プロジェクトフォルダーから POCO モデルクラス**アルバム**を開き、外部キーを含め、 **Genreid**と**artistid**という名前のプロパティを作成します。 このクラスには、主キーの**Genreid**が既に含まれています。

    (コードスニペット-*モデルとデータアクセス-Ex2 Code First アルバム*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample9.cs)]
3. POCO モデルクラスの**アーティスト**を開き、 **artistid**プロパティを含めます。

    (コードスニペット-*モデルとデータアクセス-Ex2 Code First アーティスト*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample10.cs)]
4. **モデル** プロジェクトフォルダーを右クリックし、追加 を選択します。 **クラス**。 ファイルに**MusicStoreEntities.cs**という名前を指定します。 次に、[追加] をクリックし**ます。**

    ![クラスの追加](aspnet-mvc-4-models-and-data-access/_static/image20.png "クラスの追加")

    *新しい項目の追加*

    ![Class2 の追加](aspnet-mvc-4-models-and-data-access/_static/image21.png "Class2 の追加")

    *クラスの追加*
5. 先ほど作成したクラスを開き、 **MusicStoreEntities.cs**と**いう名前空間**と、その名前空間を追加**します。**

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample11.cs)]
6. クラス宣言を置き換えて**Dbcontext**クラスを拡張します。パブリック**dbcontext**を宣言し、 **onmodelcreating**メソッドをオーバーライドします。 この手順の後には、モデルを Entity Framework にリンクするドメインクラスが表示されます。 そのためには、クラスコードを次のコードに置き換えます。

    (コードスニペット-*モデルとデータアクセス-Ex2 Code First MusicStoreEntities*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample12.cs)]

> [!NOTE]
> Entity Framework **Dbcontext**と**dbcontext**を使用すると、POCO クラスのジャンルに対してクエリを実行できます。 **Onmodelcreating**メソッドを拡張することで、ジャンルがデータベーステーブルにどのようにマップされるかを**コード**で指定します。 DBContext と Dbcontext の詳細については、msdn の記事「 [link](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx) 」を参照してください。

<a id="Ex2Task4"></a>

<a id="Task_4_-_Querying_the_Database"></a>
#### <a name="task-4---querying-the-database"></a>タスク 4-データベースに対してクエリを実行する

このタスクでは、StoreController クラスを更新して、ハードコーディングされたデータを使用するのではなく、データベースからデータを取得します。

> [!NOTE]
> この作業は、演習1では一般的です。
> 
> 演習1を完了した場合、これらの手順は両方の方法で同じになります (データベースの最初またはコードが最初)。 データがモデルにリンクされている方法は異なりますが、データエンティティへのアクセスはコントローラーから透過的に行われています。

1. **Controllers\StoreController.cs**を開き、次のフィールドをクラスに追加して、 **storedb**という名前の**MusicStoreEntities**クラスのインスタンスを保持します。

    (コードスニペット-*モデルとデータアクセス-Ex1 storeDB*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample13.cs)]
2. **MusicStoreEntities**クラスは、データベース内の各テーブルのコレクションプロパティを公開します。 すべての**アルバム**を含むジャンルを取得するように、**参照**アクションメソッドを更新します。

    (コードスニペット-*モデルとデータアクセス-Ex2 Store 参照*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample14.cs)]

    > [!NOTE]
    > **LINQ** (統合言語クエリ) と呼ばれる .net の機能を使用して、これらのコレクションに対して厳密に型指定されたクエリ式を作成します。このようなコレクションは、データベースに対してコードを実行し、プログラミングできるオブジェクトを返します。
    > 
    > LINQ の詳細については、 [msdn サイト](https://msdn.microsoft.com/library/bb397926(v=vs.110).aspx)を参照してください。
3. すべてのジャンルを取得するように**インデックス**アクションメソッドを更新します。

    (コードスニペット-*モデルとデータアクセス-Ex2 Store Index*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample15.cs)]
4. **インデックス**アクションメソッドを更新してすべてのジャンルを取得し、コレクションをリストに変換します。

    (コードスニペット-*モデルとデータアクセス-Ex2 Store GenreMenu*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample16.cs)]

<a id="Ex2Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a>タスク 5-アプリケーションを実行する

このタスクでは、ハードコードされたものではなく、データベースに格納されているジャンルが [ストアインデックス] ページに表示されることを確認します。 ビューテンプレートを変更する必要はありません。これは、 **StoreController**が以前と同じ**Storeindexindexview**を返すためですが、今回はデータがデータベースから取得されるためです。

1. ソリューションをリビルドし、 **F5**キーを押してアプリケーションを実行します。
2. プロジェクトはホームページから開始します。 **ジャンル**のメニューがハードコードされた一覧ではなくなり、データがデータベースから直接取得されていることを確認します。

    ![BrowsingGenresFromDataBase](aspnet-mvc-4-models-and-data-access/_static/image22.png)

    *データベースからのジャンルの参照*
3. 次に、任意のジャンルを参照し、アルバムにデータベースが設定されていることを確認します。

    ![データベースからのアルバムの参照](aspnet-mvc-4-models-and-data-access/_static/image23.png "データベースからのアルバムの参照")

    *データベースからのアルバムの参照*

<a id="Exercise3"></a>

<a id="Exercise_3_Querying_the_Database_with_Parameters"></a>
### <a name="exercise-3-querying-the-database-with-parameters"></a>演習 3: パラメーターを使用してデータベースにクエリを実行する

この演習では、パラメーターを使用してデータベースに対してクエリを実行する方法と、クエリ結果の整形を使用する方法について学習します。この機能を使用すると、データベースへのアクセス回数を減らすことで、より効率的な方法でデータを取得できます。

> [!NOTE]
> クエリ結果の整形の詳細については、次の[msdn の記事](https://msdn.microsoft.com/library/bb896272&amp;#040;v=vs.100&amp;#041;.aspx)を参照してください。

<a id="Ex3Task1"></a>

<a id="Task_1_-_Modifying_StoreController_to_Retrieve_Albums_from_Database"></a>
#### <a name="task-1---modifying-storecontroller-to-retrieve-albums-from-database"></a>タスク 1-StoreController を変更してデータベースからアルバムを取得する

このタスクでは、 **StoreController**クラスを変更して、特定のジャンルからアルバムを取得するためにデータベースにアクセスできるようにします。

1. データベース優先の方法を使用する場合は、 **Source\Ex3-QueryingTheDatabaseWithParametersCodeFirst\Begin**フォルダーにある**Begin**ソリューションを開き、Code first の方法または**Source\Ex3-QueryingTheDatabaseWithParametersDBFirst\Begin**フォルダーを使用します。 それ以外の場合は、前の演習を完了することによって得られた**終了**ソリューションを引き続き使用することができます。

   1. 提供された**Begin**ソリューションを開いた場合は、続行する前に、不足している NuGet パッケージをダウンロードする必要があります。 これを行うには、 **[プロジェクト]** メニューをクリックし、 **[NuGet パッケージの管理]** を選択します。
   2. **[NuGet パッケージの管理]** ダイアログで、 **[復元]** をクリックして、不足しているパッケージをダウンロードします。
   3. 最後に、[**ビルド** | **ビルド**] をクリックしてソリューションをビルドします。

      > [!NOTE]
      > NuGet を使用する利点の1つは、プロジェクトのすべてのライブラリを配布する必要がなく、プロジェクトのサイズを小さくすることです。 NuGet パワーツールを使用すると、パッケージのバージョンを app.config ファイルで指定することで、プロジェクトを初めて実行するときに必要なすべてのライブラリをダウンロードできます。 このため、このラボから既存のソリューションを開いた後に、これらの手順を実行する必要があります。
2. **StoreController**クラスを開いて、**参照**アクションメソッドを変更します。 これを行うには、**ソリューションエクスプローラー**で**Controllers**フォルダーを展開し、 **StoreController.cs**をダブルクリックします。
3. 特定のジャンルのアルバムを取得するように、**参照**アクションメソッドを変更します。 これを行うには、次のコードを置き換えます。

    (コードスニペット-*モデルとデータアクセス-Ex3 StoreController BrowseMethod*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample17.cs)]

> [!NOTE]
> エンティティのコレクションを設定するには、 **Include**メソッドを使用して、アルバムを取得するように指定する必要があります。 を使用できます。LINQ では**単一 ()** の拡張機能。この場合、アルバムには1つのジャンルのみが必要です。 **Single ()** メソッドは、ラムダ式をパラメーターとして受け取ります。この場合は、名前が定義されている値と一致するように、1つの Genre オブジェクトを指定します。
> 
> Genre オブジェクトを取得するときに、読み込みたい他の関連エンティティも指定できる機能を利用できます。 この機能は**クエリ結果の整形**と呼ばれ、データベースにアクセスして情報を取得するために必要な回数を減らすことができます。 このシナリオでは、取得したジャンルのアルバムを事前にフェッチします。
> 
> このクエリには、**ジャンル (&quot;アルバム&quot;)** が含まれており、関連するアルバムも必要であることを示しています。 これにより、1つのデータベース要求でジャンルとアルバムの両方のデータを取得するため、より効率的なアプリケーションが得られます。

<a id="Ex3Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a>タスク 2-アプリケーションの実行

このタスクでは、アプリケーションを実行し、データベースから特定のジャンルのアルバムを取得します。

1. **F5**キーを押してアプリケーションを実行します。
2. プロジェクトはホームページから開始します。 URL を変更して、データベースから結果が取得されていることを確認**します。**

    ![ジャンル別の閲覧](aspnet-mvc-4-models-and-data-access/_static/image24.png "ジャンル別の閲覧")

    *参照/ストア/参照? ジャンル = Pop*

<a id="Ex3Task3"></a>

<a id="Task_3_-_Accessing_Albums_by_Id"></a>
#### <a name="task-3---accessing-albums-by-id"></a>タスク 3-Id でアルバムにアクセスする

このタスクでは、前の手順を繰り返して、Id でアルバムを取得します。

1. 必要に応じてブラウザーを閉じて、Visual Studio に戻ります。 **StoreController**クラスを開き、 **Details**アクションメソッドを変更します。 これを行うには、**ソリューションエクスプローラー**で**Controllers**フォルダーを展開し、 **StoreController.cs**をダブルクリックします。
2. **Id**に基づいてアルバムの詳細を取得するように、**詳細**アクションメソッドを変更します。これを行うには、次のコードを置き換えます。

    (コードスニペット-*モデルとデータアクセス-Ex3 StoreController のメソッド*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample18.cs)]

<a id="Ex3Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a>タスク 4-アプリケーションを実行する

このタスクでは、web ブラウザーでアプリケーションを実行し、Id でアルバムの詳細を取得します。

1. **F5**キーを押してアプリケーションを実行します。
2. プロジェクトはホームページから開始します。 [URL] を「 **/Store/** 設定」に変更するか、ジャンルを参照してアルバムを選択し、結果がデータベースから取得されていることを確認します。

    ![詳細の参照](aspnet-mvc-4-models-and-data-access/_static/image25.png "詳細の参照")

    *参照/表示/表示/51*

> [!NOTE]
> また、 [「付録 B: Web 配置を使用した ASP.NET MVC 4 アプリケーションの発行](#AppendixB)」に従って、このアプリケーションを Windows Azure の Web サイトにデプロイすることもできます。

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a>まとめ

このハンズオンラボを完了することで、 **Database First**アプローチと**Code First**方法を使用して、ASP.NET MVC モデルとデータアクセスの基礎を学習しました。

- データを使用するためにデータベースをソリューションに追加する方法
- ハードコーディングされたものではなく、データベースから取得したデータを使用してビューテンプレートを提供するようにコントローラーを更新する方法
- パラメーターを使用してデータベースに対してクエリを実行する方法
- クエリ結果の整形を使用する方法。データベースへのアクセス数を減らし、データをより効率的な方法で取得する機能です。
- Microsoft Entity Framework で Database First と Code First の両方のアプローチを使用してデータベースをモデルにリンクする方法

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>付録 A: Visual Studio Express 2012 を Web 用にインストールする

**[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)** を使用して、Web または別の &quot;Express&quot; バージョン**用に Microsoft Visual Studio Express 2012**をインストールできます。 次の手順では、 *Microsoft Web Platform Installer*を使用して*Visual studio Express 2012 for Web*をインストールするために必要な手順について説明します。

1. [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)にアクセスします。 または、Web Platform Installer が既にインストールされている場合は、それを開いて、製品 &quot;<em>Visual Studio Express 2012 For web With Windows AZURE SDK</em>&quot;を検索することもできます。
2. **[今すぐインストール]** をクリックします。 **Web Platform Installer**がない場合は、最初にダウンロードしてインストールするようにリダイレクトされます。
3. **Web Platform Installer**が開いたら、 **[インストール]** をクリックしてセットアップを開始します。

    ![Visual Studio Express のインストール](aspnet-mvc-4-models-and-data-access/_static/image26.png "Visual Studio Express のインストール")

    *Visual Studio Express のインストール*
4. すべての製品のライセンスと条項を読み、[**同意**する] をクリックして続行します。

    ![ライセンス条項に同意する](aspnet-mvc-4-models-and-data-access/_static/image27.png)

    *ライセンス条項に同意する*
5. ダウンロードとインストールのプロセスが完了するまで待ちます。

    ![Installation progress](aspnet-mvc-4-models-and-data-access/_static/image28.png)

    *インストールの進行状況*
6. インストールが完了したら、 **[完了]** をクリックします。

    ![インストールの完了](aspnet-mvc-4-models-and-data-access/_static/image29.png)

    *インストールの完了*
7. **[終了]** をクリックして Web Platform Installer を閉じます。
8. Web 用の Visual Studio Express を開くには、**スタート**画面にアクセスして &quot;**VS Express**&quot;の書き込みを開始し、 **[VS Express for Web]** タイルをクリックします。

    ![VS Express for Web タイル](aspnet-mvc-4-models-and-data-access/_static/image30.png)

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

    ![Windows Azure portal にログオンします。](aspnet-mvc-4-models-and-data-access/_static/image31.png "Windows Azure portal にログオンします。")

    *Windows Azure 管理ポータルにログオンします。*
2. コマンドバーの **[新規]** をクリックします。

    ![新しい Web サイトの作成](aspnet-mvc-4-models-and-data-access/_static/image32.png "新しい Web サイトの作成")

    *新しい Web サイトの作成*
3. [ **Compute** | **Web サイト**] をクリックします。 次に、 **[簡易作成]** オプションを選択します。 新しい web サイトの使用可能な URL を指定し、 **[Web サイトの作成]** をクリックします。

    > [!NOTE]
    > Windows Azure の Web サイトは、制御および管理が可能なクラウドで実行されている web アプリケーションのホストです。 [簡易作成] オプションを使用すると、完成した web アプリケーションをポータルの外部から Windows Azure の Web サイトにデプロイできます。 データベースを設定する手順は含まれていません。

    ![簡易作成を使用した新しい Web サイトの作成](aspnet-mvc-4-models-and-data-access/_static/image33.png "簡易作成を使用した新しい Web サイトの作成")

    *簡易作成を使用した新しい Web サイトの作成*
4. 新しい**Web サイト**が作成されるまで待ちます。
5. Web サイトが作成されたら、 **[URL]** 列の下のリンクをクリックします。 新しい Web サイトが機能していることを確認します。

    ![新しい web サイトを参照しています](aspnet-mvc-4-models-and-data-access/_static/image34.png "新しい web サイトを参照しています")

    *新しい web サイトを参照しています*

    ![実行中の Web サイト](aspnet-mvc-4-models-and-data-access/_static/image35.png "実行中の Web サイト")

    *実行中の Web サイト*
6. ポータルに戻り、 **[名前]** 列の下にある web サイトの名前をクリックして、管理ページを表示します。

    ![Web サイトの管理ページを開く](aspnet-mvc-4-models-and-data-access/_static/image36.png "Web サイトの管理ページを開く")

    *Web サイトの管理ページを開く*
7. **[ダッシュボード]** ページの **[概要] セクションで**、 **[発行プロファイルのダウンロード]** リンクをクリックします。

    > [!NOTE]
    > *発行プロファイル*には、有効になっている各発行方法について、Windows Azure web サイトに web アプリケーションを発行するために必要なすべての情報が含まれています。 発行プロファイルには、発行メソッドが有効化される各エンドポイントに接続して認証するために必要な URL、ユーザーの資格情報、およびデータベース文字列が含まれています。 **Microsoft WebMatrix 2**、 **Microsoft Visual Studio Express for Web**および**Microsoft Visual Studio 2012**では、発行プロファイルを読み取り、Web アプリケーションを Windows Azure websites に発行するためのこれらのプログラムの構成を自動化することがサポートされています。

    ![Web サイト発行プロファイルをダウンロードしています](aspnet-mvc-4-models-and-data-access/_static/image37.png "Web サイト発行プロファイルをダウンロードしています")

    *Web サイト発行プロファイルをダウンロードしています*
8. 発行プロファイルファイルを既知の場所にダウンロードします。 この演習では、このファイルを使用して、Visual Studio から Windows Azure Web サイトに web アプリケーションを発行する方法について説明します。

    ![発行プロファイルファイルを保存しています](aspnet-mvc-4-models-and-data-access/_static/image38.png "発行プロファイルを保存しています")

    *発行プロファイルファイルを保存しています*

<a id="ApxBTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a>タスク 2-データベースサーバーの構成

アプリケーションで SQL Server データベースを使用する場合は、SQL Database サーバーを作成する必要があります。 SQL Server を使用しない単純なアプリケーションを展開する場合は、このタスクを省略できます。

1. アプリケーションデータベースを格納するには、SQL Database サーバーが必要です。 サブスクリプションの**SQL Database サーバーは**、Windows Azure 管理ポータルの**SQL データベース** | サーバー | **サーバーのダッシュボード**で確認できます。 サーバーを作成していない場合は、コマンドバーの **[追加]** ボタンを使用して作成できます。 次のタスクで使用するので、**サーバー名と URL、管理者のログイン名、パスワード**をメモしておきます。 データベースは、後の段階で作成されるため、まだ作成しないでください。

    ![SQL Database サーバーダッシュボード](aspnet-mvc-4-models-and-data-access/_static/image39.png "SQL Database サーバーダッシュボード")

    *SQL Database サーバーダッシュボード*
2. 次のタスクでは、Visual Studio からデータベース接続をテストします。そのため、**使用可能な Ip アドレス**の一覧にローカル ip アドレスを含める必要があります。 これを行うには、 **[構成]** をクリックし、 **[現在のクライアント IP アドレス]** の ip アドレスを選択して、 **[開始 Ip アドレス]** と **[終了 ip アドレス]** のテキストボックスに貼り付け、[![の](aspnet-mvc-4-models-and-data-access/_static/image40.png) 追加] をクリックします。

    ![クライアント IP アドレスを追加しています](aspnet-mvc-4-models-and-data-access/_static/image41.png)

    *クライアント IP アドレスを追加しています*
3. [許可された IP アドレス] の一覧に**クライアントの Ip アドレス**が追加されたら、 **[保存]** をクリックして変更を確認します。

    ![変更の確認](aspnet-mvc-4-models-and-data-access/_static/image42.png)

    *変更の確認*

<a id="ApxBTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>タスク 3-Web 配置を使用した ASP.NET MVC 4 アプリケーションの発行

1. ASP.NET MVC 4 ソリューションに戻ります。 **ソリューションエクスプローラー**で、web サイトプロジェクトを右クリックし、 **[発行]** を選択します。

    ![アプリケーションの発行](aspnet-mvc-4-models-and-data-access/_static/image43.png "アプリケーションの発行")

    *Web サイトの公開*
2. 最初のタスクで保存した発行プロファイルをインポートします。

    ![発行プロファイルをインポートしています](aspnet-mvc-4-models-and-data-access/_static/image44.png "発行プロファイルをインポートしています")

    *発行プロファイルをインポートしています*
3. **[接続の検証]** をクリックします。 検証が完了したら、 **[次へ]** をクリックします。

    > [!NOTE]
    > 検証が完了すると、[接続の検証] ボタンの横に緑色のチェックマークが表示されます。

    ![接続の検証](aspnet-mvc-4-models-and-data-access/_static/image45.png "接続の検証")

    *接続の検証*
4. **[設定]** ページの **[データベース]** セクションで、データベース接続のテキストボックスの横にあるボタン ( **defaultconnection**など) をクリックします。

    ![Web deploy の構成](aspnet-mvc-4-models-and-data-access/_static/image46.png "Web deploy の構成")

    *Web deploy の構成*
5. 次のようにデータベース接続を構成します。

   - **サーバー名**には、 *tcp:* プレフィックスを使用して SQL Database サーバーの URL を入力します。
   - **User name (ユーザー名**) に、サーバー管理者のログイン名を入力します。
   - **パスワード**で、サーバー管理者のログインパスワードを入力します。
   - 新しいデータベース名を入力します。

     ![変換先の接続文字列を構成しています](aspnet-mvc-4-models-and-data-access/_static/image47.png "変換先の接続文字列を構成しています")

     *変換先の接続文字列を構成しています*
6. 次に、 **[OK]** をクリックします データベースの作成を求めるメッセージが表示されたら、[**はい]** をクリックします。

    ![データベースの作成](aspnet-mvc-4-models-and-data-access/_static/image48.png "データベース文字列の作成")

    *データベースの作成*
7. Windows Azure の SQL Database に接続するために使用する接続文字列は、[既定の接続] ボックスに表示されます。 続けて、 **[次へ]** をクリックします。

    ![SQL Database を指す接続文字列](aspnet-mvc-4-models-and-data-access/_static/image49.png "SQL Database を指す接続文字列")

    *SQL Database を指す接続文字列*
8. **[プレビュー]** ページで、 **[発行]** をクリックします。

    ![Web アプリケーションの発行](aspnet-mvc-4-models-and-data-access/_static/image50.png "Web アプリケーションの発行")

    *Web アプリケーションの発行*
9. 発行プロセスが完了すると、既定のブラウザーによって公開された web サイトが開きます。

<a id="AppendixC"></a>

<a id="Appendix_C_Using_Code_Snippets"></a>
## <a name="appendix-c-using-code-snippets"></a>付録 C: コードスニペットの使用

コードスニペットを使用すると、必要なすべてのコードをすぐに利用できます。 次の図に示すように、ラボドキュメントには、使用できるタイミングがわかります。

![Visual Studio のコードスニペットを使用してプロジェクトにコードを挿入する](aspnet-mvc-4-models-and-data-access/_static/image51.png "Visual Studio のコードスニペットを使用してプロジェクトにコードを挿入する")

*Visual Studio のコードスニペットを使用してプロジェクトにコードを挿入する*

***キーボードを使用してコードスニペットを追加C#するには (のみ)***

1. コードを挿入する場所にカーソルを置きます。
2. (スペースまたはハイフンを含まない) スニペット名の入力を開始します。
3. IntelliSense によって、一致するスニペットの名前が表示されます。
4. 正しいスニペットを選択します (または、スニペットの名前全体が選択されるまで入力し続けます)。
5. Tab キーを2回押すと、スニペットがカーソル位置に挿入されます。

![スニペット名の入力を開始します](aspnet-mvc-4-models-and-data-access/_static/image52.png "スニペット名の入力を開始します")

*スニペット名の入力を開始します*

![Tab キーを押して、強調表示されているスニペットを選択します](aspnet-mvc-4-models-and-data-access/_static/image53.png "Tab キーを押して、強調表示されているスニペットを選択します")

*Tab キーを押して、強調表示されているスニペットを選択します*

![もう一度 Tab キーを押すと、スニペットが展開されます。](aspnet-mvc-4-models-and-data-access/_static/image54.png "もう一度 Tab キーを押すと、スニペットが展開されます。")

*もう一度 Tab キーを押すと、スニペットが展開されます。*

***マウスC#(、Visual Basic および XML) を使用してコードスニペットを追加するに***は1. コードスニペットを挿入する場所を右クリックします。

1. **[スニペットの挿入]** 、 **[マイコードスニペット**] の順に選択します。
2. 一覧から該当するスニペットをクリックして選択します。

![コードスニペットを挿入する場所を右クリックし、[スニペットの挿入] を選択します。](aspnet-mvc-4-models-and-data-access/_static/image55.png "コードスニペットを挿入する場所を右クリックし、[スニペットの挿入] を選択します。")

*コードスニペットを挿入する場所を右クリックし、[スニペットの挿入] を選択します。*

![一覧から関連するスニペットをクリックして選択します。](aspnet-mvc-4-models-and-data-access/_static/image56.png "一覧から関連するスニペットをクリックして選択します。")

*一覧から関連するスニペットをクリックして選択します。*
