---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-entity-framework-scaffolding-and-migrations
title: ASP.NET MVC 4 Entity Framework スキャフォールディングと移行 |Microsoft Docs
author: rick-anderson
description: ASP.NET MVC 4 コントローラーの方法に慣れている場合、またはハンズオンラボ&quot; &quot;ヘルパー、フォーム、検証を完了している場合は、以下の点に注意する必要があります...
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 093c1362-f10b-407c-a708-be370f4b62b0
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-entity-framework-scaffolding-and-migrations
msc.type: authoredcontent
ms.openlocfilehash: 2b26224390af70e19ca0593abe93a6867140f8ab
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484642"
---
# <a name="aspnet-mvc-4-entity-framework-scaffolding-and-migrations"></a>ASP.NET MVC 4 Entity Framework スキャフォールディングと移行

[Web キャンプチーム](https://twitter.com/webcamps)別

[Web キャンプトレーニングキットをダウンロードする](https://aka.ms/webcamps-training-kit)

ASP.NET MVC 4 コントローラーの方法に慣れている場合、またはハンズオンラボ&quot; &quot;ヘルパー、フォーム、および検証を完了している場合は、アプリケーション間で繰り返されるデータエンティティを作成、更新、一覧表示、および削除するロジックの多くに注意する必要があります。 これに触れないと、モデルに操作するクラスが複数ある場合、各エンティティ操作の POST アクションメソッドと GET アクションメソッドの作成にかなりの時間がかかる可能性があります。また、各ビューも同様です。

このラボでは、ASP.NET MVC 4 スキャフォールディングを使用して、アプリケーションの CRUD (作成、読み取り、更新、および削除) のベースラインを自動的に生成する方法について説明します。 単純なモデルクラスから開始し、1行のコードを記述せずに、すべての CRUD 操作と、必要なすべてのビューを格納するコントローラーを作成します。 単純なソリューションをビルドして実行すると、アプリケーションデータベースが生成され、データ操作用の MVC ロジックとビューが作成されます。

さらに、Entity Framework の移行を使用して、アプリケーション全体でモデルの更新を実行することがいかに簡単であるかについても説明します。 Entity Framework の移行では、簡単な手順でモデルを変更した後にデータベースを変更できます。 これらすべてを念頭に置いて、ASP.NET MVC 4 の最新の機能を活用して、web アプリケーションをより効率的に構築して管理できるようになります。

> [!NOTE]
> すべてのサンプルコードとスニペットは、 [Microsoft web/WebCampTrainingKit リリース](https://aka.ms/webcamps-training-kit)から入手できる Web キャンプトレーニングキットに含まれています。 このラボに固有のプロジェクトは、 [ASP.NET MVC 4 Entity Framework のスキャフォールディングと移行](https://github.com/Microsoft-Web/HOL-EntityFrameworkScaffoldingAndMigrations)で入手できます。

<a id="Objectives"></a>
### <a name="objectives"></a>目標

このハンズオンラボでは、次の方法を学習します。

- コントローラーで CRUD 操作に ASP.NET スキャフォールディングを使用します。
- Entity Framework の移行を使用してデータベースモデルを変更します。

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

Visual Studio Code のスニペットを使い慣れておらず、その使用方法を学習する場合は、このドキュメントの付録「[付録 B: コードスニペット](#AppendixB)&quot;の使用」 &quot;参照してください。

---

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a>手順

次の演習では、このハンズオンラボを作成します。

1. [Entity Framework 移行での ASP.NET MVC 4 スキャフォールディングの使用](#Exercise1)

> [!NOTE]
> この演習には、演習の完了後に取得する必要があるソリューションを含む**終了**フォルダーが付属しています。 演習を通じて追加のヘルプが必要な場合は、このソリューションをガイドとして使用できます。

このラボの推定所要時間: **30 分**

<a id="Exercise1"></a>

<a id="Exercise_1_Using_ASPNET_MVC_4_Scaffolding_with_Entity_Framework_Migrations"></a>
### <a name="exercise-1-using-aspnet-mvc-4-scaffolding-with-entity-framework-migrations"></a>演習 1: Entity Framework 移行での ASP.NET MVC 4 スキャフォールディングの使用

ASP.NET MVC スキャフォールディングは、CRUD 操作を標準化された方法で生成し、アプリケーションがデータベース層と対話できるようにするために必要なロジックを作成するための簡単な方法を提供します。

この演習では、ASP.NET MVC 4 スキャフォールディングを code first と共に使用して CRUD メソッドを作成する方法について説明します。 次に、Entity Framework の移行を使用して、データベースの変更を適用してモデルを更新する方法について説明します。

<a id="Ex1Task1"></a>

<a id="Task_1-_Creating_a_new_ASPNET_MVC_4_project_using_Scaffolding"></a>
#### <a name="task-1--creating-a-new-aspnet-mvc-4-project-using-scaffolding"></a>タスク 1-スキャフォールディングを使用して新しい ASP.NET MVC 4 プロジェクトを作成する

1. まだ開いていない場合は、 **Visual Studio 2012**を起動します。
2. ファイルの選択 **|新しいプロジェクト**。 [新しいプロジェクト] ダイアログで、[ **Visual C# |] を選択します。[Web** ] セクションで、 **[ASP.NET MVC 4 Web アプリケーション]** を選択します。 プロジェクトに**MVC4andEFMigrations**という名前を設定し、このラボの [location to **Source\Ex1-UsingMVC4ScaffoldingEFMigrations** ] フォルダーに移動します。 **[ソリューション名]** を **[開始]** に設定し、 **[ソリューションのディレクトリを作成]** する がオンになっていることを確認します。 **[OK]** をクリックします。

    ![[新しい ASP.NET MVC 4 プロジェクト] ダイアログボックス](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image1.png "[新しい ASP.NET MVC 4 プロジェクト] ダイアログボックス")

    *[新しい ASP.NET MVC 4 プロジェクト] ダイアログボックス*
3. **[新しい ASP.NET MVC 4 プロジェクト]** ダイアログボックスで、 **[インターネットアプリケーション**] テンプレートを選択し、 **Razor**が選択した**ビューエンジン**であることを確認します。 **[OK]** をクリックしてプロジェクトを作成します。

    ![新しい ASP.NET MVC 4 インターネットアプリケーション](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image2.png "新しい ASP.NET MVC 4 インターネットアプリケーション")

    *新しい ASP.NET MVC 4 インターネットアプリケーション*
4. ソリューションエクスプローラーで、**モデル** を右クリックし、追加 を選択します。 **クラス**を作成して、単純なクラス (POCO) を作成します。 「 **Person** 」という名前を指定し、[ **OK]** をクリックします。
5. Person クラスを開き、次のプロパティを挿入します。

    (コードスニペット- *ASP.NET MVC 4 および Entity Framework 移行-Ex1 Person プロパティ*)

    [!code-csharp[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample1.cs)]
6. [ビルド] をクリックします。 **ソリューションをビルド**して変更を保存し、プロジェクトをビルドします。

    ![アプリケーションのビルド](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image3.png "アプリケーションのビルド")

    *アプリケーションのビルド*
7. ソリューションエクスプローラーで、controllers フォルダーを右クリックし、[追加] を選択します。 **コントローラー**。
8. コントローラーに「*個人コントローラー* 」という名前を付け、次の値を使用して**スキャフォールディングオプション**を完成させます。

   1. **[テンプレート]** ボックスの一覧で、Entity Framework オプション**を使用して、読み取り/書き込みアクションとビューを含む MVC コントローラー**を選択します。
   2. **[モデルクラス]** ボックスの一覧で、 **Person**クラスを選択します。
   3. **[データコンテキストクラス]** の一覧で [ **&lt;新しいデータコンテキスト...&gt;** ] を選択します。 任意の名前を選択し、[ **OK]** をクリックします。
   4. **[ビュー]** ドロップダウンリストで、 **[Razor]** が選択されていることを確認します。

      ![スキャフォールディングを使用した Person コントローラーの追加](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image4.png "スキャフォールディングを使用した Person コントローラーの追加")

      *スキャフォールディングを使用した Person コントローラーの追加*
9. **[追加]** をクリックして、スキャフォールディングを持つユーザーの新しいコントローラーを作成します。 これで、コントローラーアクションとビューが生成されました。

    ![スキャフォールディングを使用して Person コントローラーを作成した後](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image5.png "スキャフォールディングを使用して Person コントローラーを作成した後")

    *スキャフォールディングを使用して Person コントローラーを作成した後*
10. [**個人] コントローラー**クラスを開きます。 完全な CRUD アクションメソッドが自動的に生成されていることに注意してください。

   ![Person コントローラー内](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image6.png "Person コントローラー内")

   *Person コントローラー内*

<a id="Ex1Task2"></a>

<a id="Task_2-_Running_the_application"></a>
#### <a name="task-2--running-the-application"></a>タスク 2-アプリケーションの実行

この時点では、データベースはまだ作成されていません。 このタスクでは、初めてアプリケーションを実行し、CRUD 操作をテストします。 データベースは Code First を使用してすぐに作成されます。

1. **F5** キーを押してアプリケーションを実行します。
2. ブラウザーで、URL に **/person**を追加して、[person] ページを開きます。

    ![アプリケーションの初回実行](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image7.png "アプリケーションの初回実行")

    *アプリケーション: 最初の実行*
3. ここでは、ユーザーのページを探索し、CRUD 操作をテストします。

    1. **[新規作成]** をクリックして、新しいユーザーを追加します。 名と姓を入力し、 **[作成]** をクリックします。

        ![新しいユーザーの追加](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image8.png "新しいユーザーの追加")

        *新しいユーザーの追加*
    2. ユーザーの一覧で、アイテムの削除、編集、または追加を行うことができます。

        ![個人一覧](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image9.png "個人一覧")

        *個人一覧*
    3. **[詳細]** をクリックすると、個人の詳細が表示されます。

        ![個人の詳細](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image10.png "個人の詳細")

        *個人の詳細*
4. ブラウザーを閉じて、Visual Studio に戻ります。 アプリケーション全体で person エンティティの CRUD 全体が作成されていることに注意してください。つまり、モデルからビューまで、1行のコードを記述する必要はありません。

<a id="Ex1Task3"></a>

<a id="Task_3-_Updating_the_database_using_Entity_Framework_Migrations"></a>
#### <a name="task-3--updating-the-database-using-entity-framework-migrations"></a>タスク 3-Entity Framework の移行を使用してデータベースを更新する

このタスクでは、Entity Framework の移行を使用してデータベースを更新します。 Entity Framework 移行機能を使用して、モデルを変更し、データベースの変更を反映することがいかに簡単であるかがわかります。

1. パッケージマネージャーコンソールを開きます。 **[ツール]**  >  **[NuGet パッケージ マネージャー]**  >  **[パッケージ マネージャー コンソール]** の順に選択します。
2. パッケージ マネージャー コンソールで、次のコマンドを入力します。

    PMC

    [!code-powershell[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample2.ps1)]

    ![移行の有効化](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image11.png "移行を有効にする")

    *移行の有効化*

    [移行の有効化] コマンドを実行すると、**移行**フォルダーが作成されます。このフォルダーには、データベースを初期化するスクリプトが含まれています。

    ![移行フォルダー](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image12.png "移行フォルダー")

    *移行フォルダー*
3. [移行] フォルダーの**Configuration.cs**ファイルを開きます。 クラスコンストラクターを見つけて、 **AutomaticMigrationsEnabled**値を*true*に変更します。

    [!code-csharp[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample3.cs)]
4. Person クラスを開き、人名のミドルネームの属性を追加します。 この新しい属性を使用して、モデルを変更します。

    [!code-csharp[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample4.cs)]
5. Build | を選択します。メニューの [ソリューションのビルド] をオンにして、アプリケーションをビルドします。

    ![アプリケーションのビルド](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image13.png "アプリケーションのビルド")

    *アプリケーションのビルド*
6. パッケージ マネージャー コンソールで、次のコマンドを入力します。

    PMC

    [!code-powershell[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample5.ps1)]

    このコマンドにより、データオブジェクトの変更が検索され、それに応じてデータベースを変更するために必要なコマンドが追加されます。

    ![ミドルネームの追加](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image14.png "ミドルネームの追加")

    *ミドルネームの追加*
7. Optional次のコマンドを実行すると、差分更新を使用して SQL スクリプトを生成できます。 これにより、データベースを手動で更新 (この場合は必要ありません) することができます。また、変更を他のデータベースに適用することもできます。

    PMC

    [!code-powershell[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample6.ps1)]

    ![SQL スクリプトの生成](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image15.png "SQL スクリプトを生成する")

    *SQL スクリプトの生成*

    ![SQL スクリプトの更新](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image16.png "SQL スクリプトの更新")

    *SQL スクリプトの更新*
8. パッケージマネージャーコンソールで、次のコマンドを入力してデータベースを更新します。

    PMC

    [!code-powershell[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample7.ps1)]

    ![データベースを更新しています](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image17.png "データベースの更新")

    *データベースを更新しています*

    これに**より、Person テーブルの** **MiddleName**列が、 **Person**クラスの現在の定義に一致するように追加されます。
9. データベースが更新されたら、コントローラーフォルダーを右クリックし、[追加] を選択します。Person コントローラーを再び追加するコントローラー (同じ値で完了します)。 これにより、既存のメソッドとビューが更新され、新しい属性が追加されます。

    ![コントローラー更新プログラムの追加](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image18.png "コントローラー更新プログラムの追加")

    *コントローラーを更新しています*
10. **[追加]** をクリックします。 次に、 **PersonController.cs を上書き**する の値を選択し、**関連付けられているビューを上書き**します を選択し、 **OK**

   ![コントローラーの上書きの追加](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image19.png)

   *コントローラーを更新しています*

<a id="Ex1Task4"></a>

<a id="Task4-_Running_the_application"></a>
#### <a name="task4--running-the-application"></a>Task4-アプリケーションの実行

1. **F5** キーを押してアプリケーションを実行します。
2. 開く **/Person**。 中央の [名前] 列が追加されたときに、データが保持されていることに注意してください。

    ![追加されたミドルネーム](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image20.png "追加されたミドルネーム")

    *追加されたミドルネーム*
3. **[編集]** をクリックすると、現在のユーザーにミドルネームを追加できるようになります。

    ![ミドルネームエディション](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image21.png "ミドルネームエディション")

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a>まとめ

このハンズオンラボでは、任意のモデルクラスを使用して ASP.NET MVC 4 スキャフォールディングで CRUD 操作を作成するための簡単な手順を学習しました。 次に、Entity Framework の移行を使用して、アプリケーションでエンドツーエンドの更新を実行する方法について説明しました。これは、データベースからビューへの更新です。

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>付録 A: Visual Studio Express 2012 を Web 用にインストールする

**[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)** を使用して、Web または別の &quot;Express&quot; バージョン**用に Microsoft Visual Studio Express 2012**をインストールできます。 次の手順では、 *Microsoft Web Platform Installer*を使用して*Visual studio Express 2012 for Web*をインストールするために必要な手順について説明します。

1. [https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169) に移動します。 または、Web Platform Installer が既にインストールされている場合は、それを開いて、製品 &quot;<em>Visual Studio Express 2012 For web With Windows AZURE SDK</em>&quot;を検索することもできます。
2. **[今すぐインストール]** をクリックします。 **Web Platform Installer**がない場合は、最初にダウンロードしてインストールするようにリダイレクトされます。
3. **Web Platform Installer**が開いたら、 **[インストール]** をクリックしてセットアップを開始します。

    ![Visual Studio Express のインストール](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image22.png "Visual Studio Express のインストール")

    *Visual Studio Express のインストール*
4. すべての製品のライセンスと条項を読み、[**同意**する] をクリックして続行します。

    ![ライセンス条項に同意する](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image23.png)

    *ライセンス条項に同意する*
5. ダウンロードとインストールのプロセスが完了するまで待ちます。

    ![Installation progress](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image24.png)

    *インストールの進行状況*
6. インストールが完了したら、 **[完了]** をクリックします。

    ![インストールの完了](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image25.png)

    *インストールの完了*
7. **[終了]** をクリックして Web Platform Installer を閉じます。
8. Web 用の Visual Studio Express を開くには、**スタート**画面にアクセスして &quot;**VS Express**&quot;の書き込みを開始し、 **[VS Express for Web]** タイルをクリックします。

    ![VS Express for Web タイル](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image26.png)

    *VS Express for Web タイル*

<a id="AppendixB"></a>

<a id="Appendix_B_Using_Code_Snippets"></a>
## <a name="appendix-b-using-code-snippets"></a>付録 B: コードスニペットの使用

コードスニペットを使用すると、必要なすべてのコードをすぐに利用できます。 次の図に示すように、ラボドキュメントには、使用できるタイミングがわかります。

![Visual Studio のコードスニペットを使用してプロジェクトにコードを挿入する](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image27.png "Visual Studio のコードスニペットを使用してプロジェクトにコードを挿入する")

*Visual Studio のコードスニペットを使用してプロジェクトにコードを挿入する*

***キーボードを使用してコードスニペットを追加C#するには (のみ)***

1. コードを挿入する場所にカーソルを置きます。
2. (スペースまたはハイフンを含まない) スニペット名の入力を開始します。
3. IntelliSense によって、一致するスニペットの名前が表示されます。
4. 正しいスニペットを選択します (または、スニペットの名前全体が選択されるまで入力し続けます)。
5. Tab キーを2回押すと、スニペットがカーソル位置に挿入されます。

![スニペット名の入力を開始します](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image28.png "スニペット名の入力を開始します")

*スニペット名の入力を開始します*

![Tab キーを押して、強調表示されているスニペットを選択します](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image29.png "Tab キーを押して、強調表示されているスニペットを選択します")

*Tab キーを押して、強調表示されているスニペットを選択します*

![もう一度 Tab キーを押すと、スニペットが展開されます。](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image30.png "もう一度 Tab キーを押すと、スニペットが展開されます。")

*もう一度 Tab キーを押すと、スニペットが展開されます。*

***マウスC#(、Visual Basic および XML) を使用してコードスニペットを追加するに***は1. コードスニペットを挿入する場所を右クリックします。

1. **[スニペットの挿入]** 、 **[マイコードスニペット**] の順に選択します。
2. 一覧から該当するスニペットをクリックして選択します。

![コードスニペットを挿入する場所を右クリックし、[スニペットの挿入] を選択します。](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image31.png "コードスニペットを挿入する場所を右クリックし、[スニペットの挿入] を選択します。")

*コードスニペットを挿入する場所を右クリックし、[スニペットの挿入] を選択します。*

![一覧から関連するスニペットをクリックして選択します。](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image32.png "一覧から関連するスニペットをクリックして選択します。")

*一覧から関連するスニペットをクリックして選択します。*
