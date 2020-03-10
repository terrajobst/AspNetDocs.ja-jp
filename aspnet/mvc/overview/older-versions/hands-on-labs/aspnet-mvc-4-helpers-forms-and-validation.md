---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-helpers-forms-and-validation
title: ASP.NET MVC 4 ヘルパー、フォーム、および検証 |Microsoft Docs
author: rick-anderson
description: ASP.NET MVC 4 モデルとデータアクセスのハンズオンラボでは、データベースのデータを読み込んで表示しています。 このハンズオンラボでは、次のように追加します...
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 187ee9cd-bc70-479b-bfed-f568b8da96eb
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-helpers-forms-and-validation
msc.type: authoredcontent
ms.openlocfilehash: 0e2605a4188eaf814f6ab0ebfeaabed4457bcfa3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78433792"
---
# <a name="aspnet-mvc-4-helpers-forms-and-validation"></a>ASP.NET MVC 4 ヘルパー、フォーム、検証

[Web キャンプチーム](https://twitter.com/webcamps)別

[Web キャンプトレーニングキットをダウンロードする](https://aka.ms/webcamps-training-kit)

**ASP.NET MVC 4 モデルとデータアクセス**のハンズオンラボでは、データベースのデータを読み込んで表示しています。 このハンズオンラボでは、このデータを編集する機能を**ミュージックストア**アプリケーションに追加します。

この目標を念頭に置いて、最初に、アルバムの作成、読み取り、更新、削除 (CRUD) アクションをサポートするコントローラーを作成します。 ASP.NET MVC のスキャフォールディング機能を利用して、HTML テーブルにアルバムのプロパティを表示する、インデックスビューテンプレートを生成します。 このビューを強化するには、長い説明を切り捨てるカスタム HTML ヘルパーを追加します。

その後、[編集] ビューと [作成] ビューを追加します。このビューでは、データベースのアルバムを変更でき、ドロップダウンなどのフォーム要素を使用できます。

最後に、ユーザーがアルバムを削除できるようにします。また、入力を検証することで間違ったデータを入力できないようにします。

このハンズオンラボでは、 **ASP.NET MVC**に関する基本的な知識があることを前提としています。 以前に**ASP.NET mvc**を使用していない場合は、 **ASP.NET mvc の基礎**となるハンズオンラボに進むことをお勧めします。

このラボでは、ソースフォルダーに用意されているサンプル Web アプリケーションに軽微な変更を適用することによって前述した機能強化と新機能について説明します。

> [!NOTE]
> すべてのサンプルコードとスニペットは、 [Microsoft web/WebCampTrainingKit リリース](https://aka.ms/webcamps-training-kit)で入手できる Web キャンプトレーニングキットに含まれています。 このラボに固有のプロジェクトは、 [ASP.NET MVC 4 のヘルパー、フォーム、および検証](https://github.com/Microsoft-Web/HOL-MVC4HelpersFormsAndValidation)で入手できます。

<a id="Objectives"></a>
### <a name="objectives"></a>目標

このハンズオンラボでは、次の方法を学習します。

- CRUD 操作をサポートするコントローラーを作成する
- エンティティのプロパティを HTML テーブルに表示するためのインデックスビューの生成
- カスタム HTML ヘルパーを追加する
- 編集ビューを作成およびカスタマイズする
- HTTP GET または HTTP POST 呼び出しのいずれかに対応するアクションメソッドを区別する
- 作成ビューを追加およびカスタマイズする
- エンティティの削除を処理する
- ユーザー入力の検証

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

このハンズオンラボは、次の演習によって構成されています。

1. [ストアマネージャーコントローラーとそのインデックスビューを作成する](#Exercise1)
2. [HTML ヘルパーの追加](#Exercise2)
3. [編集ビューを作成する](#Exercise3)
4. [作成ビューの追加](#Exercise4)
5. [削除の処理](#Exercise5)
6. [検証の追加](#Exercise6)
7. [クライアント側での控えめな jQuery の使用](#Exercise7)

> [!NOTE]
> 各演習には、演習を完了した後に取得する必要があるソリューションを含む**終了**フォルダーが付属しています。 演習を通じて追加のヘルプが必要な場合は、このソリューションをガイドとして使用できます。

このラボの推定所要時間: **60 分**

<a id="Exercise1"></a>

<a id="Exercise_1_Creating_the_Store_Manager_controller_and_its_Index_view"></a>
### <a name="exercise-1-creating-the-store-manager-controller-and-its-index-view"></a>演習 1: ストアマネージャーコントローラーとそのインデックスビューの作成

この演習では、CRUD 操作をサポートする新しいコントローラーを作成する方法、データベースからアルバムの一覧を返すようにインデックスアクションメソッドをカスタマイズする方法、最後に ASP.NET MVC のスキャフォールディングを利用してインデックスビューテンプレートを生成する方法について説明します。アルバムのプロパティを HTML テーブルに表示する機能。

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_the_StoreManagerController"></a>
#### <a name="task-1---creating-the-storemanagercontroller"></a>タスク 1-StoreManagerController の作成

このタスクでは、CRUD 操作をサポートするために**StoreManagerController**という名前の新しいコントローラーを作成します。

1. **Source/Ex1-CreatingTheStoreManagerController/begin/** folder にある**begin**ソリューションを開きます。

   1. 続行する前に、不足している NuGet パッケージをダウンロードする必要があります。 これを行うには、 **[プロジェクト]** メニューをクリックし、 **[NuGet パッケージの管理]** を選択します。
   2. **[NuGet パッケージの管理]** ダイアログで、 **[復元]** をクリックして、不足しているパッケージをダウンロードします。
   3. 最後に、[**ビルド** | **ビルド**] をクリックしてソリューションをビルドします。

      > [!NOTE]
      > NuGet を使用する利点の1つは、プロジェクトのすべてのライブラリを配布する必要がなく、プロジェクトのサイズを小さくすることです。 NuGet パワーツールを使用すると、パッケージのバージョンを app.config ファイルで指定することで、プロジェクトを初めて実行するときに必要なすべてのライブラリをダウンロードできます。 このため、このラボから既存のソリューションを開いた後に、これらの手順を実行する必要があります。
2. 新しいコントローラーを追加します。 これを行うには、ソリューションエクスプローラー内の**Controllers**フォルダーを右クリックし、 **[追加]** を選択して、 **[コントローラー]** をクリックします。 **コントローラー** **名**を**StoreManagerController**に変更し、 **[読み取り/書き込みアクションが空の MVC コントローラー]** オプションが選択されていることを確認します。 **[追加]** をクリックします。

    ![[コントローラーの追加] ダイアログ](aspnet-mvc-4-helpers-forms-and-validation/_static/image1.png "[コントローラーの追加] ダイアログ")

    *[コントローラーの追加] ダイアログ*

    新しいコントローラークラスが生成されます。 読み取り/書き込み用のアクションを追加するように指定したため、これらのスタブメソッドには、TODO コメントを入力して、アプリケーション固有のロジックを含めるよう求めるメッセージが表示されます。

<a id="Ex1Task2"></a>

<a id="Task_2_-_Customizing_the_StoreManager_Index"></a>
#### <a name="task-2---customizing-the-storemanager-index"></a>タスク 2-StoreManager インデックスのカスタマイズ

このタスクでは、データベースからアルバムの一覧と共にビューを返すように、StoreManager インデックスアクションメソッドをカスタマイズします。

1. StoreManagerController クラスに、次の*using*ディレクティブを追加します。

    (コードスニペット- *ASP.NET MVC 4 のヘルパーとフォームと検証-Ex1 を使用した MvcMusicStore*)

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample1.cs)]
2. MusicStoreEntities のインスタンスを保持するフィールドを**StoreManagerController**に追加**します。**

    (コードスニペット- *ASP.NET MVC 4 のヘルパーとフォームと検証-Ex1 MusicStoreEntities*)

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample2.cs)]
3. アルバムの一覧と共にビューを返すには、StoreManagerController Index アクションを実装します。

    コントローラーアクションロジックは、前に記述した StoreController のインデックスアクションと非常によく似ています。 LINQ を使用して、表示するジャンルとアーティストの情報を含むすべてのアルバムを取得します。

    (コードスニペット- *ASP.NET MVC 4 のヘルパーとフォームと検証-Ex1 StoreManagerController Index*)

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample3.cs)]

<a id="Ex1Task3"></a>

<a id="strongTask_3_-_Creating_the_Index_Viewstrong"></a>
#### <a name="task-3---creating-the-index-view"></a>タスク 3-インデックスビューを作成する

このタスクでは、インデックスビューテンプレートを作成して、 **Storemanager**コントローラーによって返されたアルバムの一覧を表示します。

1. 新しいビューテンプレートを作成する前に、[**ビューの追加] ダイアログ**で使用する**アルバム**クラスが認識されるように、プロジェクトをビルドする必要があります。 Build | を選択します。 **MvcMusicStore をビルド**してプロジェクトをビルドします。
2. **Index**アクションメソッド内を右クリックし、 **[ビューの追加]** を選択します。 **[ビューの追加]** ダイアログが表示されます。

    ![ビューの追加](aspnet-mvc-4-helpers-forms-and-validation/_static/image2.png "ビューの追加")

    *Index メソッド内からビューを追加する*
3. ビューの追加 ダイアログで、ビュー名が **インデックス** であることを確認します。 **[厳密に型指定されたビューを作成する]** オプションを選択し、 **[モデルクラス]** ドロップダウンから **[アルバム (MvcMusicStore)]** を選択します。 **[スキャフォールディング template]** ドロップダウンリストから **[List]** を選択します。 **ビューエンジン**を**Razor**に、その他のフィールドに既定値をそのまま使用し、 **[追加]** をクリックします。

    ![インデックスビューの追加](aspnet-mvc-4-helpers-forms-and-validation/_static/image3.png "インデックスビューの追加")

    *インデックスビューの追加*

<a id="Ex1Task4"></a>

<a id="Task_4_-_Customizing_the_scaffold_of_the_Index_View"></a>
#### <a name="task-4---customizing-the-scaffold-of-the-index-view"></a>タスク 4-インデックスビューのスキャフォールディングのカスタマイズ

このタスクでは、ASP.NET MVC スキャフォールディング機能で作成された単純なビューテンプレートを調整して、必要なフィールドを表示するようにします。

> [!NOTE]
> ASP.NET MVC 内での**スキャフォールディング**のサポートにより、アルバムモデルのすべてのフィールドを一覧表示する簡易ビューテンプレートが生成されます。 **スキャフォールディング**は、厳密に型指定されたビューをすばやく開始するための簡単な方法を提供します。ビューテンプレートを手動で記述するのではなく、スキャフォールディングによって既定のテンプレートがすばやく生成され、生成されたコードを変更できます。

1. 作成されたコードを確認します。 生成されたフィールドの一覧は、**スキャフォールディング**が表形式データを表示するために使用する次の HTML テーブルの一部になります。

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample4.cshtml)]
2. **&lt;テーブル&gt;** コードを次のコードに置き換えて、**ジャンル**、**アーティスト**、**アルバムタイトル**、および**価格**フィールドのみを表示します。 これにより、 **AlbumId**と**アルバムアートの URL**列が削除されます。 また、 **Artist.Name**と**Genre.Name**のリンクされたクラスプロパティを表示するように Genreid 列と artistid 列を変更し、 **Details**リンクを削除します。

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample5.cshtml)]
3. 次の説明を変更します。

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample6.cshtml)]

<a id="Ex1Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a>タスク 5-アプリケーションを実行する

このタスクでは、 **Storemanager** **インデックス**ビューテンプレートで、前の手順の設計に従ってアルバムの一覧が表示されることをテストします。

1. **F5**キーを押してアプリケーションを実行します。
2. プロジェクトはホームページから開始します。 URL を「 **/storemanager** 」に変更して、アルバムの一覧が表示され **、タイトル**、**アーティスト**、**ジャンル**を表示していることを確認します。

    ![アルバムの一覧の参照](aspnet-mvc-4-helpers-forms-and-validation/_static/image4.png "アルバムの一覧の参照")

    *アルバムの一覧の参照*

<a id="Exercise2"></a>

<a id="Exercise_2_Adding_an_HTML_Helper"></a>
### <a name="exercise-2-adding-an-html-helper"></a>演習 2: HTML ヘルパーの追加

StoreManager インデックスページには、考えられる問題が1つあります。 Title とアーティスト名のプロパティは、テーブルの書式設定を破棄するのに十分な長さであることが必要です。 この演習では、カスタム HTML ヘルパーを追加してそのテキストを切り捨てる方法を学習します。

次の図では、小さなブラウザーサイズを使用すると、テキストの長さによって形式がどのように変更されるかを確認できます。

![切り捨てられたテキストのないアルバムの一覧の参照](aspnet-mvc-4-helpers-forms-and-validation/_static/image5.png "切り捨てられたテキストのないアルバムの一覧の参照")

*切り捨てられたテキストのないアルバムの一覧の参照*

<a id="Ex2Task1"></a>

<a id="Task_1_-_Extending_the_HTML_Helper"></a>
#### <a name="task-1---extending-the-html-helper"></a>タスク 1-HTML ヘルパーの拡張

このタスクでは、ASP.NET MVC ビュー内で公開されている**HTML**オブジェクトに新しいメソッドの**切り捨て**を追加します。 これを行うには、ASP.NET MVC によって提供される組み込みの**System.web ヘルパー**クラスに**拡張メソッド**を実装します。

> [!NOTE]
> **拡張メソッド**の詳細については、こちらの msdn 記事をご覧ください。 [https://msdn.microsoft.com/library/bb383977.aspx](https://msdn.microsoft.com/library/bb383977.aspx)」を参照してください。

1. **Source/Ex2-アドオン**/フォルダーにある**begin**ソリューションを開きます。 それ以外の場合は、前の演習を完了することによって得られた**終了**ソリューションを引き続き使用することができます。

   1. 提供された**Begin**ソリューションを開いた場合は、続行する前に、不足している NuGet パッケージをダウンロードする必要があります。 これを行うには、 **[プロジェクト]** メニューをクリックし、 **[NuGet パッケージの管理]** を選択します。
   2. **[NuGet パッケージの管理]** ダイアログで、 **[復元]** をクリックして、不足しているパッケージをダウンロードします。
   3. 最後に、[**ビルド** | **ビルド**] をクリックしてソリューションをビルドします。

      > [!NOTE]
      > NuGet を使用する利点の1つは、プロジェクトのすべてのライブラリを配布する必要がなく、プロジェクトのサイズを小さくすることです。 NuGet パワーツールを使用すると、パッケージのバージョンを app.config ファイルで指定することで、プロジェクトを初めて実行するときに必要なすべてのライブラリをダウンロードできます。 このため、このラボから既存のソリューションを開いた後に、これらの手順を実行する必要があります。
2. StoreManager のインデックスビューを開きます。 これを行うには、ソリューションエクスプローラー **Views**  フォルダーを展開し、 **storemanager**を選択して、**インデックスの cshtml**ファイルを開きます。
3. <strong>@model</strong>ディレクティブの下に次のコードを追加して、 <strong>Truncate</strong> helper メソッドを定義します。

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample7.cshtml)]

<a id="Ex2Task2"></a>

<a id="Task_2_-_Truncating_Text_in_the_Page"></a>
#### <a name="task-2---truncating-text-in-the-page"></a>タスク 2-ページ内のテキストの切り捨て

このタスクでは、 **truncate**メソッドを使用して、ビューテンプレート内のテキストを切り捨てます。

1. StoreManager のインデックスビューを開きます。 これを行うには、ソリューションエクスプローラー **Views**  フォルダーを展開し、 **storemanager**を選択して、**インデックスの cshtml**ファイルを開きます。
2. **アーティスト名**とアルバムの**タイトル**が表示されている行を置き換えます。 これを行うには、次の行を置き換えます。

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample8.cshtml)]

<a id="Ex2Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a>タスク 3-アプリケーションを実行する

このタスクでは、 **Storemanager** **インデックス**ビューテンプレートによって、アルバムのタイトルとアーティスト名が切り詰められていることをテストします。

1. **F5**キーを押してアプリケーションを実行します。
2. プロジェクトはホームページから開始します。 URL を「 **/storemanager** 」に変更し、 **[タイトル]** 列と **[アーティスト]** 列の長いテキストが切り捨てられていることを確認します。

    ![タイトルとアーティスト名の切り捨て](aspnet-mvc-4-helpers-forms-and-validation/_static/image6.png "タイトルとアーティスト名の切り捨て")

    *タイトルとアーティスト名が切り詰められました*

<a id="Exercise3"></a>

<a id="Exercise_3_Creating_the_Edit_View"></a>
### <a name="exercise-3-creating-the-edit-view"></a>演習 3: 編集ビューの作成

この演習では、ストアマネージャーがアルバムを編集できるようにするフォームを作成する方法について説明します。 **/StoreManager/Edit/id** URL (**id**は編集するアルバムの一意の id である) を参照するため、サーバーに対して HTTP GET 呼び出しを行います。

Controller Edit action メソッドは、データベースから適切なアルバムを取得し、 **StoreManagerViewModel**オブジェクトを作成してそれをカプセル化します (さらに、アーティストとジャンルのリストを表示します)。その後、このオブジェクトをビューテンプレートに渡して、HTML ページをユーザーに戻します。 このページには、アルバムのプロパティを編集するためのテキストボックスとドロップダウンを含む **&lt;フォーム&gt;** 要素が含まれます。

ユーザーがアルバムフォームの値を更新して **[保存]** ボタンをクリックすると、変更が **/StoreManager/Edit/id**にポストバックされて送信されます。URL は最後の呼び出しと同じままですが、ASP.NET MVC では、今度は HTTP POST であることが識別されます。そのため、別の編集アクションメソッド ( **[Httppost]** で修飾されたもの) を実行します。

<a id="Ex3Task1"></a>

<a id="Task_1_-_Implementing_the_HTTP-GET_Edit_Action_Method"></a>
#### <a name="task-1---implementing-the-http-get-edit-action-method"></a>タスク 1-HTTP 取得の編集アクションメソッドを実装する

このタスクでは、編集アクションメソッドの HTTP GET バージョンを実装して、適切なアルバムをデータベースから取得します。また、すべてのジャンルとアーティストのリストも取得します。 このデータは、最後のステップで定義されている**StoreManagerViewModel**オブジェクトにパッケージ化されます。これは、と共に応答を表示するためにビューテンプレートに渡されます。

1. **Source/Ex3-さくせいビュー/begin/** folder にある**begin**ソリューションを開きます。 それ以外の場合は、前の演習を完了することによって得られた**終了**ソリューションを引き続き使用することができます。

   1. 提供された**Begin**ソリューションを開いた場合は、続行する前に、不足している NuGet パッケージをダウンロードする必要があります。 これを行うには、 **[プロジェクト]** メニューをクリックし、 **[NuGet パッケージの管理]** を選択します。
   2. **[NuGet パッケージの管理]** ダイアログで、 **[復元]** をクリックして、不足しているパッケージをダウンロードします。
   3. 最後に、[**ビルド** | **ビルド**] をクリックしてソリューションをビルドします。

      > [!NOTE]
      > NuGet を使用する利点の1つは、プロジェクトのすべてのライブラリを配布する必要がなく、プロジェクトのサイズを小さくすることです。 NuGet パワーツールを使用すると、パッケージのバージョンを app.config ファイルで指定することで、プロジェクトを初めて実行するときに必要なすべてのライブラリをダウンロードできます。 このため、このラボから既存のソリューションを開いた後に、これらの手順を実行する必要があります。
2. **StoreManagerController**クラスを開きます。 これを行うには、 **Controllers**フォルダーを展開し、 **[StoreManagerController.cs]** をダブルクリックします。
3. **HTTP-GET Edit** action メソッドを次のコードに置き換えて、適切な**アルバム**と**ジャンル**と**アーティスト**の一覧を取得します。

    (コードスニペット- *ASP.NET MVC 4 のヘルパーとフォームと検証-Ex3 STOREMANAGERCONTROLLER HTTP-編集アクションの取得*)

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample9.cs)]

    > [!NOTE]
    > システムの**コレクション**ではなく、アーティストとジャンルに対して**System.web. Mvc** **selectlist**を使用しています。
    > 
    > **Selectlist**は、HTML ドロップダウンを設定し、現在の選択などを管理するための、すっきりした方法です。 コントローラーアクションでこれらのビューモデルオブジェクトをインスタンス化して後で設定すると、フォームの編集シナリオがすっきりします。

<a id="Ex3Task2"></a>

<a id="Task_2_-_Creating_the_Edit_View"></a>
#### <a name="task-2---creating-the-edit-view"></a>タスク 2-編集ビューの作成

このタスクでは、後でアルバムのプロパティを表示する編集ビューテンプレートを作成します。

1. 編集ビューを作成します。 これを行うには、アクションの **[編集]** メソッド内を右クリックし、 **[ビューの追加]** を選択します。
2. [ビューの追加] ダイアログで、ビュー名が**Edit**であることを確認します。 厳密に型指定された **[ビューを作成する]** チェックボックスをオンにし、 **[データクラスの表示]** ドロップダウンから **[アルバム (MvcMusicStore)]** を選択します。 **[スキャフォールディングテンプレート]** ドロップダウンから **[編集]** を選択します。 他のフィールドは既定値のままにして、 **[追加]** をクリックします。

    ![編集ビューの追加](aspnet-mvc-4-helpers-forms-and-validation/_static/image7.png "編集ビューの追加")

    *編集ビューの追加*

<a id="Ex3Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a>タスク 3-アプリケーションを実行する

このタスクでは、 **Storemanager**の [ビューの**編集**] ページに、パラメーターとして渡されたアルバムのプロパティの値が表示されることをテストします。

1. **F5**キーを押してアプリケーションを実行します。
2. プロジェクトはホームページから開始します。 URL を **/StoreManager/Edit/1**に変更し、渡されたアルバムのプロパティの値が表示されていることを確認します。

    ![アルバムの編集ビューを閲覧する](aspnet-mvc-4-helpers-forms-and-validation/_static/image8.png "アルバムの編集ビューを閲覧する")

    *アルバムの編集ビューを閲覧する*

<a id="Ex3Task4"></a>

<a id="Task_4_-_Implementing_drop-downs_on_the_Album_Editor_Template"></a>
#### <a name="task-4---implementing-drop-downs-on-the-album-editor-template"></a>タスク 4-アルバムエディターテンプレートにドロップダウンを実装する

このタスクでは、最後のタスクで作成されたビューテンプレートにドロップダウンを追加して、ユーザーがアーティストとジャンルの一覧から選択できるようにします。

1. すべての**アルバム**のフィールドセットコードを次のコードに置き換えます。

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample10.cshtml)]

    > [!NOTE]
    > アーティストとジャンルを選択するためのレンダードロップダウンに、 **Html の DropDownList**ヘルパーが追加されました。 **Html**に渡されるパラメーターは次のとおりです。
    > 
    > 1. フォームフィールドの名前 ( **&quot;ArtistId&quot;** )。
    > 2. ドロップダウンの値の**Selectlist** 。

<a id="Ex3Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a>タスク 5-アプリケーションを実行する

このタスクでは、 **Storemanager**の [ビューの**編集**] ページに、アーティストおよびジャンル ID のテキストフィールドではなくドロップダウンが表示されることをテストします。

1. **F5**キーを押してアプリケーションを実行します。
2. プロジェクトはホームページから開始します。 URL を **/StoreManager/Edit/1**に変更して、アーティストと Genre ID のテキストフィールドではなくドロップダウンが表示されていることを確認します。

    ![ドロップダウンでアルバムの編集ビューを閲覧する](aspnet-mvc-4-helpers-forms-and-validation/_static/image9.png "ドロップダウンでアルバムの編集ビューを閲覧する")

    *アルバムの編集ビューを閲覧する、今回はドロップダウン*

<a id="Ex3Task6"></a>

<a id="Task_6_-_Implementing_the_HTTP-POST_Edit_action_method"></a>
#### <a name="task-6---implementing-the-http-post-edit-action-method"></a>タスク 6-HTTP ポスト編集アクションメソッドを実装する

編集ビューが想定どおりに表示されたので、アルバムに加えられた変更を保存するには、HTTP POST Edit アクションメソッドを実装する必要があります。

1. 必要に応じてブラウザーを閉じ、Visual Studio ウィンドウに戻ります。 **Controllers**フォルダーから**StoreManagerController**を開きます。
2. **HTTP ポスト編集**アクションメソッドのコードを次のコードに置き換えます (置き換える必要があるメソッドは、2つのパラメーターを受け取るオーバーロードされたバージョンであることに注意してください)。

    (コードスニペット- *ASP.NET MVC 4 のヘルパーとフォームと検証-Ex3 STOREMANAGERCONTROLLER HTTP-編集後のアクション*)

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample11.cs)]

    > [!NOTE]
    > このメソッドは、ユーザーがビューの **[保存]** ボタンをクリックしたときに実行され、フォーム値の HTTP POST をサーバーに返して、データベースに保持します。 デコレータ **[Httppost]** は、これらの HTTP ポストシナリオに対してメソッドを使用する必要があることを示しています。 このメソッドは、**アルバム**オブジェクトを受け取ります。 ASP.NET MVC は、投稿された &lt;フォーム&gt; 値からアルバムオブジェクトを自動的に作成します。
    > 
    > メソッドは、次の手順を実行します。
    > 
    > 1. モデルが有効な場合:
    > 
    >     1. コンテキストのアルバムエントリを更新して、変更されたオブジェクトとしてマークします。
    >     2. 変更を保存し、インデックスビューにリダイレクトします。
    > 2. モデルが有効でない場合は、ViewBag に**Genreid**と**artistid**が設定され、ユーザーが必要な更新を実行できるように、受信したアルバムオブジェクトを含むビューが返されます。

<a id="Ex3Task7"></a>

<a id="Task_7_-_Running_the_Application"></a>
#### <a name="task-7---running-the-application"></a>タスク 7-アプリケーションを実行する

このタスクでは、 **Storemanager Edit** View ページが実際に更新されたアルバムデータをデータベースに保存することをテストします。

1. **F5**キーを押してアプリケーションを実行します。
2. プロジェクトはホームページから開始します。 URL を **/StoreManager/Edit/1**に変更します。 アルバムのタイトルを **[読み込み]** に変更し、 **[保存]** をクリックします。 アルバムの一覧でアルバムのタイトルが実際に変更されたことを確認します。

    ![アルバムを更新する](aspnet-mvc-4-helpers-forms-and-validation/_static/image10.png "アルバムを更新する")

    *アルバムを更新する*

<a id="Exercise4"></a>

<a id="Exercise_4_Adding_a_Create_View"></a>
### <a name="exercise-4-adding-a-create-view"></a>演習 4: Create ビューの追加

**StoreManagerController**が**編集**機能をサポートするようになったので、この演習では、ストアマネージャーが新しいアルバムをアプリケーションに追加できるように、Create View テンプレートを追加する方法を学習します。

編集機能を使用した場合と同様に、 **StoreManagerController**クラス内の2つの異なるメソッドを使用して作成シナリオを実装します。

1. ストアマネージャーが最初に **/StoreManager/Create** URL にアクセスすると、1つのアクションメソッドで空のフォームが表示されます。
2. 2番目のアクションメソッドでは、ストアマネージャーがフォーム内の **[保存]** ボタンをクリックして、 **/StoreManager/Create** URL に値を送信するというシナリオを処理します。

<a id="Ex4Task1"></a>

<a id="Task_1_-_Implementing_the_HTTP-GET_Create_action_method"></a>
#### <a name="task-1---implementing-the-http-get-create-action-method"></a>タスク 1-HTTP 取得の Create action メソッドの実装

このタスクでは、Create action メソッドの HTTP GET バージョンを実装して、すべてのジャンルとアーティストの一覧を取得し、このデータを**StoreManagerViewModel**オブジェクトにパッケージ化します。これはビューテンプレートに渡されます。

1. **Source/Ex4-/begin** /folder にある**begin**ソリューションを開きます。 それ以外の場合は、前の演習を完了することによって得られた**終了**ソリューションを引き続き使用することができます。

   1. 提供された**Begin**ソリューションを開いた場合は、続行する前に、不足している NuGet パッケージをダウンロードする必要があります。 これを行うには、 **[プロジェクト]** メニューをクリックし、 **[NuGet パッケージの管理]** を選択します。
   2. **[NuGet パッケージの管理]** ダイアログで、 **[復元]** をクリックして、不足しているパッケージをダウンロードします。
   3. 最後に、[**ビルド** | **ビルド**] をクリックしてソリューションをビルドします。

      > [!NOTE]
      > NuGet を使用する利点の1つは、プロジェクトのすべてのライブラリを配布する必要がなく、プロジェクトのサイズを小さくすることです。 NuGet パワーツールを使用すると、パッケージのバージョンを app.config ファイルで指定することで、プロジェクトを初めて実行するときに必要なすべてのライブラリをダウンロードできます。 このため、このラボから既存のソリューションを開いた後に、これらの手順を実行する必要があります。
2. **StoreManagerController**クラスを開きます。 これを行うには、 **Controllers**フォルダーを展開し、 **[StoreManagerController.cs]** をダブルクリックします。
3. **Create** action メソッドのコードを次のコードに置き換えます。

    (コードスニペット- *ASP.NET MVC 4 のヘルパーとフォームと検証-Ex4 STOREMANAGERCONTROLLER HTTP-Create アクションの取得*)

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample12.cs)]

<a id="Ex4Task2"></a>

<a id="Task_2_-_Adding_the_Create_View"></a>
#### <a name="task-2---adding-the-create-view"></a>タスク 2-作成ビューの追加

このタスクでは、新しい (空の) アルバムフォームを表示する Create View テンプレートを追加します。

1. **Create** action メソッド内を右クリックし、 **[ビューの追加]** を選択します。 [ビューの追加] ダイアログが表示されます。
2. ビューの追加 ダイアログで、ビュー名が **作成** であることを確認します。 **[厳密に型指定されたビューを作成する]** オプションを選択し、 **[モデルクラス]** ドロップダウンから **[アルバム (MvcMusicStore)]** を選択し、 **[スキャフォールディングテンプレート]** ドロップダウンから **[作成]** を選択します。 他のフィールドは既定値のままにして、 **[追加]** をクリックします。

    ![作成ビューの追加](aspnet-mvc-4-helpers-forms-and-validation/_static/image11.png "adding-a-create-view")

    *Create ビューの追加*
3. 次に示すように、ドロップダウンリストを使用するように**Genreid**フィールドと**artistid**フィールドを更新します。

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample13.cshtml)]

<a id="Ex4Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a>タスク 3-アプリケーションを実行する

このタスクでは、 **Storemanager**の [ビューの**作成**] ページに空のアルバムフォームが表示されることをテストします。

1. **F5**キーを押してアプリケーションを実行します。
2. プロジェクトはホームページから開始します。 URL を **/StoreManager/Create**に変更します。 新しいアルバムのプロパティを入力するための空のフォームが表示されていることを確認します。

    ![空のフォームを持つビューを作成する](aspnet-mvc-4-helpers-forms-and-validation/_static/image12.png "空のフォームを持つビューを作成する")

    *空のフォームを持つビューを作成する*

<a id="Ex4Task4"></a>

<a id="Task_4_-_Implementing_the_HTTP-POST_Create_Action_Method"></a>
#### <a name="task-4---implementing-the-http-post-create-action-method"></a>タスク 4-HTTP ポスト作成アクションメソッドを実装する

このタスクでは、ユーザーが **[保存]** ボタンをクリックしたときに呼び出される、Create action メソッドの HTTP POST バージョンを実装します。 メソッドでは、新しいアルバムをデータベースに保存する必要があります。

1. 必要に応じてブラウザーを閉じ、Visual Studio ウィンドウに戻ります。 **StoreManagerController**クラスを開きます。 これを行うには、 **Controllers**フォルダーを展開し、 **[StoreManagerController.cs]** をダブルクリックします。
2. **HTTP ポストの Create**アクションメソッドのコードを次のコードに置き換えます。

    (コードスニペット- *ASP.NET MVC 4 のヘルパーとフォームと検証-Ex4 STOREMANAGERCONTROLLER HTTP-投稿作成アクション*)

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample14.cs)]

    > [!NOTE]
    > 作成アクションは、前の編集アクションメソッドと非常に似ていますが、オブジェクトを変更済みとして設定するのではなく、コンテキストに追加されます。

<a id="Ex4Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a>タスク 5-アプリケーションを実行する

このタスクでは、 **Storemanager**の [ビューの作成] ページを使用して、新しいアルバムを作成し、Storemanager インデックスビューにリダイレクトすることをテストします。

1. **F5**キーを押してアプリケーションを実行します。
2. プロジェクトはホームページから開始します。 URL を **/StoreManager/Create**に変更します。 次の図に示すように、すべてのフォームフィールドに新しいアルバムのデータを入力します。

    ![アルバムを作成する](aspnet-mvc-4-helpers-forms-and-validation/_static/image13.png "アルバムを作成する")

    *アルバムを作成する*
3. 作成したばかりの新しいアルバムを含む StoreManager インデックスビューにリダイレクトされていることを確認します。

    ![新しく作成されたアルバム](aspnet-mvc-4-helpers-forms-and-validation/_static/image14.png "新しく作成されたアルバム")

    *新しく作成されたアルバム*

<a id="Exercise5"></a>

<a id="Exercise_5_Handling_Deletion"></a>
### <a name="exercise-5-handling-deletion"></a>演習 5: 削除の処理

アルバムを削除する機能はまだ実装されていません。 この演習では、このことについて説明します。 前と同様に、 **StoreManagerController**クラス内の2つの異なるメソッドを使用して、削除シナリオを実装します。

1. 1つのアクションメソッドで確認フォームが表示される
2. 2番目のアクションメソッドは、フォームの送信を処理します。

<a id="Ex5Task1"></a>

<a id="Task_1_-_Implementing_the_HTTP-GET_Delete_Action_Method"></a>
#### <a name="task-1---implementing-the-http-get-delete-action-method"></a>タスク 1-HTTP 取得の削除アクションメソッドを実装する

このタスクでは、Delete アクションメソッドの HTTP GET バージョンを実装して、アルバムの情報を取得します。

1. **Source/Ex5-HandlingDeletion/begin/** folder にある**begin**ソリューションを開きます。 それ以外の場合は、前の演習を完了することによって得られた**終了**ソリューションを引き続き使用することができます。

   1. 提供された**Begin**ソリューションを開いた場合は、続行する前に、不足している NuGet パッケージをダウンロードする必要があります。 これを行うには、 **[プロジェクト]** メニューをクリックし、 **[NuGet パッケージの管理]** を選択します。
   2. **[NuGet パッケージの管理]** ダイアログで、 **[復元]** をクリックして、不足しているパッケージをダウンロードします。
   3. 最後に、[**ビルド** | **ビルド**] をクリックしてソリューションをビルドします。

      > [!NOTE]
      > NuGet を使用する利点の1つは、プロジェクトのすべてのライブラリを配布する必要がなく、プロジェクトのサイズを小さくすることです。 NuGet パワーツールを使用すると、パッケージのバージョンを app.config ファイルで指定することで、プロジェクトを初めて実行するときに必要なすべてのライブラリをダウンロードできます。 このため、このラボから既存のソリューションを開いた後に、これらの手順を実行する必要があります。
2. **StoreManagerController**クラスを開きます。 これを行うには、 **Controllers**フォルダーを展開し、 **[StoreManagerController.cs]** をダブルクリックします。
3. [コントローラーの削除] アクションは、以前の [ストアの詳細] コントローラーアクションとまったく同じです。 URL で指定された**id**を使用してデータベースから**アルバム**オブジェクトに対してクエリを実行し、適切な**ビュー**を返します。 これを行うには、HTTP-GET **Delete**アクションメソッドのコードを次のコードに置き換えます。

    (コードスニペット- *ASP.NET MVC 4 ヘルパー And Forms And Validation-Ex5 処理削除 HTTP-Delete Delete アクション*)

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample15.cs)]
4. **Delete**アクションメソッド内で右クリックし、 **[ビューの追加]** を選択します。 [ビューの追加] ダイアログが表示されます。
5. ビューの追加 ダイアログで、ビュー名が **削除** であることを確認します。 **[厳密に型指定されたビューを作成する]** オプションを選択し、 **[モデルクラス]** ドロップダウンから **[アルバム (MvcMusicStore)]** を選択します。 **[スキャフォールディング template]** ドロップダウンから **[削除]** を選択します。 他のフィールドは既定値のままにして、 **[追加]** をクリックします。

    ![削除ビューの追加](aspnet-mvc-4-helpers-forms-and-validation/_static/image15.png "削除ビューの追加")

    *削除ビューの追加*
6. 削除テンプレートには、モデルのすべてのフィールドが表示されます。 アルバムのタイトルのみが表示されます。 これを行うには、ビューの内容を次のコードに置き換えます。

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample16.cshtml)]

<a id="Ex05Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a>タスク 2-アプリケーションの実行

このタスクでは、 **Storemanager**の [ビューの**削除**] ページに確認の削除フォームが表示されることをテストします。

1. **F5**キーを押してアプリケーションを実行します。
2. プロジェクトはホームページから開始します。 URL を「 **/storemanager**」に変更します。 削除するアルバムを1つ選択し、 **[削除]** をクリックして、新しいビューがアップロードされていることを確認します。

    ![アルバムの削除](aspnet-mvc-4-helpers-forms-and-validation/_static/image16.png "アルバムの削除")

    *アルバムの削除*

<a id="Ex05Task3"></a>

<a id="Task_3-_Implementing_the_HTTP-POST_Delete_Action_Method"></a>
#### <a name="task-3--implementing-the-http-post-delete-action-method"></a>タスク 3-HTTP ポスト削除アクションメソッドを実装する

このタスクでは、ユーザーが **[削除]** ボタンをクリックしたときに呼び出される、delete アクションメソッドの HTTP ポストバージョンを実装します。 メソッドは、データベース内のアルバムを削除する必要があります。

1. 必要に応じてブラウザーを閉じ、Visual Studio ウィンドウに戻ります。 **StoreManagerController**クラスを開きます。 これを行うには、 **Controllers**フォルダーを展開し、 **[StoreManagerController.cs]** をダブルクリックします。
2. **HTTP ポスト削除**アクションメソッドのコードを次のコードに置き換えます。

    (コードスニペット- *ASP.NET MVC 4 ヘルパー And Forms And Validation-Ex5 処理削除 HTTP-Delete Delete アクション*)

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample17.cs)]

<a id="Ex5Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a>タスク 4-アプリケーションを実行する

このタスクでは、 **Storemanager**の [ビューの削除] ページでアルバムを削除し、Storemanager インデックスビューにリダイレクトできることをテストします。

1. **F5**キーを押してアプリケーションを実行します。
2. プロジェクトはホームページから開始します。 URL を「 **/storemanager**」に変更します。 [削除] をクリックして、削除するアルバムを1つ選択し**ます。** 削除を確認するには、 **[削除]** ボタンをクリックします。

    ![アルバムの削除](aspnet-mvc-4-helpers-forms-and-validation/_static/image17.png "アルバムの削除")

    *アルバムの削除*
3. アルバムが削除されたことを確認します。これは、 **[インデックス]** ページに表示されません。

<a id="Exercise6"></a>

<a id="Exercise_6_Adding_Validation"></a>
### <a name="exercise-6-adding-validation"></a>演習 6: 検証の追加

現時点では、作成および編集フォームでは、どのような種類の検証も実行されません。 ユーザーが必要なフィールドを空白のままにするか、price フィールドに文字を入力すると、最初に発生するエラーはデータベースから取得されます。

モデルクラスにデータ注釈を追加することで、アプリケーションに検証を追加できます。 データ注釈を使用すると、モデルのプロパティに適用するルールを記述できます。また、ASP.NET MVC は、適切なメッセージをユーザーに適用し、表示する処理を行います。

<a id="Ex06Task1"></a>

<a id="Task_1_-_Adding_Data_Annotations"></a>
#### <a name="task-1---adding-data-annotations"></a>タスク 1-データ注釈を追加する

このタスクでは、必要に応じて、Create ページと Edit ページに検証メッセージを表示するデータ注釈をアルバムモデルに追加します。

単純なモデルクラスの場合、データ注釈を追加するには、 **system.componentmodel**の**using**ステートメントを追加してから、適切なプロパティに **[Required]** 属性を配置します。 次の例では、 **Name**プロパティをビューの必須フィールドにします。

[!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample18.cs)]

これは、Entity Data Model が生成されるこのアプリケーションのような場合には少し複雑です。 モデルクラスにデータ注釈を直接追加した場合は、データベースからモデルを更新すると上書きされます。 代わりに、注釈を保持するために存在し、 **[Metadatatype]** 属性を使用してモデルクラスに関連付けられているメタデータ部分クラスを使用できます。

1. **Source/Ex6-の検証/開始/** フォルダーにある**begin**ソリューションを開きます。 それ以外の場合は、前の演習を完了することによって得られた**終了**ソリューションを引き続き使用することができます。

   1. 提供された**Begin**ソリューションを開いた場合は、続行する前に、不足している NuGet パッケージをダウンロードする必要があります。 これを行うには、 **[プロジェクト]** メニューをクリックし、 **[NuGet パッケージの管理]** を選択します。
   2. **[NuGet パッケージの管理]** ダイアログで、 **[復元]** をクリックして、不足しているパッケージをダウンロードします。
   3. 最後に、[**ビルド** | **ビルド**] をクリックしてソリューションをビルドします。

      > [!NOTE]
      > NuGet を使用する利点の1つは、プロジェクトのすべてのライブラリを配布する必要がなく、プロジェクトのサイズを小さくすることです。 NuGet パワーツールを使用すると、パッケージのバージョンを app.config ファイルで指定することで、プロジェクトを初めて実行するときに必要なすべてのライブラリをダウンロードできます。 このため、このラボから既存のソリューションを開いた後に、これらの手順を実行する必要があります。
2. **[モデル]** フォルダーから**Album.cs**を開きます。
3. **Album.cs**の内容を強調表示されたコードに置き換えて、次のようにします。

    > [!NOTE]
    > **[Displayformat (ConvertEmptyStringToNull = false)]** という行は、データソースのデータフィールドが更新されたときに、モデルの空の文字列が null に変換されないことを示します。 データ注釈によってフィールドが検証される前に、Entity Framework によってモデルに null 値が割り当てられる場合、この設定は例外を回避します。

    (コードスニペット- *ASP.NET MVC 4 のヘルパーとフォームと検証-Ex6 アルバムメタデータ部分クラス*)

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample19.cs)]

    > [!NOTE]
    > この**アルバム**部分クラスには、データ注釈の**AlbumMetaData**クラスを指す**metadatatype**属性があります。 アルバムモデルに注釈を付けるために使用しているデータ注釈属性の一部を次に示します。
    > 
    > - 必須-プロパティが必須フィールドであることを示します。
    > - DisplayName-フォームフィールドと検証メッセージに使用するテキストを定義します。
    > - DisplayFormat-データフィールドを表示および書式設定する方法を指定します。
    > - StringLength-文字列フィールドの最大長を定義します。
    > - 範囲-数値フィールドの最大値と最小値を指定します。
    > - ScaffoldColumn-エディターフォームからのフィールドの非表示を許可します

<a id="Ex06Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a>タスク 2-アプリケーションの実行

このタスクでは、最後のタスクで選択した表示名を使用して、Create ページと Edit ページがフィールドを検証するかどうかをテストします。

1. **F5**キーを押してアプリケーションを実行します。
2. プロジェクトはホームページから開始します。 URL を **/StoreManager/Create**に変更します。 表示名が部分クラスの名前と一致していることを確認します ( **AlbumArtUrl**の代わりに**アルバムアートの URL**など)。
3. フォームに入力せずに **[作成]** をクリックします。 対応する検証メッセージが取得されていることを確認します。

    ![[作成] ページで検証されたフィールド](aspnet-mvc-4-helpers-forms-and-validation/_static/image18.png "[作成] ページで検証されたフィールド")

    *[作成] ページで検証されたフィールド*
4. **[編集]** ページでも同じことを確認できます。 URL を **/StoreManager/Edit/1**に変更し、表示名が部分クラスの名前と一致していることを確認します ( **AlbumArtUrl**の代わりに**アルバムアートの URL**など)。 **タイトル**と**価格**フィールドを空にして、 **[保存]** をクリックします。 対応する検証メッセージが取得されていることを確認します。

    ![[編集] ページの検証済みフィールド](aspnet-mvc-4-helpers-forms-and-validation/_static/image19.png)

    *[編集] ページの検証済みフィールド*

<a id="Exercise7"></a>

<a id="Exercise_7_Using_Unobtrusive_jQuery_at_Client_Side"></a>
### <a name="exercise-7-using-unobtrusive-jquery-at-client-side"></a>演習 7: クライアント側で控えめな jQuery を使用する

この演習では、クライアント側で MVC 4 の控えめな jQuery 検証を有効にする方法について説明します。

> [!NOTE]
> 控えめな jQuery は、データ ajax プレフィックス JavaScript を使用して、インラインクライアントスクリプトを出力するのではなく、サーバー上のアクションメソッドを呼び出します。

<a id="Ex7Task1"></a>

<a id="Task_1_-_Running_the_Application_before_Enabling_Unobtrusive_jQuery"></a>
#### <a name="task-1---running-the-application-before-enabling-unobtrusive-jquery"></a>タスク 1-控えめな jQuery を有効にする前にアプリケーションを実行する

このタスクでは、両方の検証モデルを比較するために、jQuery をインクルードする前にアプリケーションを実行します。

1. **Source/Ex7-UnobtrusivejQueryValidation/begin/** folder にある**begin**ソリューションを開きます。 それ以外の場合は、前の演習を完了することによって得られた**終了**ソリューションを引き続き使用することができます。

   1. 提供された**Begin**ソリューションを開いた場合は、続行する前に、不足している NuGet パッケージをダウンロードする必要があります。 これを行うには、 **[プロジェクト]** メニューをクリックし、 **[NuGet パッケージの管理]** を選択します。
   2. **[NuGet パッケージの管理]** ダイアログで、 **[復元]** をクリックして、不足しているパッケージをダウンロードします。
   3. 最後に、[**ビルド** | **ビルド**] をクリックしてソリューションをビルドします。

      > [!NOTE]
      > NuGet を使用する利点の1つは、プロジェクトのすべてのライブラリを配布する必要がなく、プロジェクトのサイズを小さくすることです。 NuGet パワーツールを使用すると、パッケージのバージョンを app.config ファイルで指定することで、プロジェクトを初めて実行するときに必要なすべてのライブラリをダウンロードできます。 このため、このラボから既存のソリューションを開いた後に、これらの手順を実行する必要があります。
2. **F5** キーを押してアプリケーションを実行します。
3. プロジェクトはホームページから開始します。 **/StoreManager/Create**を参照し、フォームに入力せずに **[作成]** をクリックして、検証メッセージが表示されることを確認します。

    ![クライアント検証が無効](aspnet-mvc-4-helpers-forms-and-validation/_static/image20.png "クライアント検証が無効")

    *クライアント検証が無効*
4. ブラウザーで、HTML ソースコードを開きます。

    [!code-html[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample20.html)]

<a id="Ex7Task2"></a>

<a id="Task_2_-_Enabling_Unobtrusive_Client_Validation"></a>
#### <a name="task-2---enabling-unobtrusive-client-validation"></a>タスク 2-控えめなクライアント検証の有効化

このタスクでは、 **web.config ファイルから**jQuery の控えめな**クライアント検証**を有効にします。これは、すべての新しい ASP.NET MVC 4 プロジェクトで既定で false に設定されています。 また、jQuery の控えめなクライアント検証を行うために必要なスクリプト参照を追加します。

1. プロジェクトルートで**web.config**ファイルを開き、 **Clientvalidationenabled**と**UnobtrusiveJavaScriptEnabled** keys の値が**true**に設定されていることを確認します。

    [!code-xml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample21.xml)]

    > [!NOTE]
    > Global.asax.cs のコードでクライアント検証を有効にすることで、同じ結果を得ることもできます。
    > 
    > **HtmlHelper. ClientValidationEnabled = true;**
    > 
    > また、ClientValidationEnabled 属性を任意のコントローラーに割り当てて、カスタム動作を設定することもできます。
2. **Views\StoreManager**で、 **Create. cshtml**を開きます。
3. &quot; **~/bundles/jqueryval**&quot; バンドルを通じて、次のスクリプトファイル ( **jquery. validate**および**jquery**) がビューで参照されていることを確認します。

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample22.cshtml)]

    > [!NOTE]
    > これらの jQuery ライブラリはすべて、MVC 4 の新しいプロジェクトに含まれています。 その他のライブラリは、プロジェクトの **[スクリプト]** フォルダーにあります。
    > 
    > この検証ライブラリを機能させるには、jQuery framework ライブラリへの参照を追加する必要があります。 この参照は既に **\_Layout. cshtml**ファイルに追加されているため、この特定のビューに追加する必要はありません。

<a id="Ex7Task3"></a>

<a id="Task_3_-_Running_the_Application_Using_Unobtrusive_jQuery_Validation"></a>
#### <a name="task-3---running-the-application-using-unobtrusive-jquery-validation"></a>タスク 3-控えめな jQuery 検証を使用したアプリケーションの実行

このタスクでは、ユーザーが新しいアルバムを作成するときに、 **Storemanager** create view テンプレートによって jQuery ライブラリを使用したクライアント側の検証が実行されることをテストします。

1. **F5** キーを押してアプリケーションを実行します。
2. プロジェクトはホームページから開始します。 **/StoreManager/Create**を参照し、フォームに入力せずに **[作成]** をクリックして、検証メッセージが表示されることを確認します。

    ![JQuery が有効になっているクライアント検証](aspnet-mvc-4-helpers-forms-and-validation/_static/image21.png "JQuery が有効になっているクライアント検証")

    *JQuery が有効になっているクライアント検証*
3. ブラウザーで、Create view のソースコードを開きます。

    [!code-html[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample23.html)]

   > [!NOTE]
   > 各クライアント検証規則について、控えめな jQuery は*rulename*=&quot;*message*&quot;を持つ属性を追加します。 次に、クライアント検証を実行するために、控えめな jQuery が html 入力フィールドに挿入するタグの一覧を示します。
   > 
   > - データ-val
   > - データ-val
   > - データ値-範囲
   > - データ範囲-最小値/データ範囲-最大値
   > - データ val-必須
   > - データ val-長さ
   > - データ-長さ-最大/データ-長さ-最小
   > 
   > すべてのデータ値は、モデル**データ注釈**で塗りつぶされます。 次に、サーバー側で動作するすべてのロジックをクライアント側で実行できます。 たとえば、Price 属性には、モデルに次のデータ注釈があります。
   > 
   > [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample24.cs)]
   > 
   > 控えめな jQuery を使用すると、生成されるコードは次のようになります。
   > 
   > [!code-html[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample25.html)]

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a>まとめ

このハンズオンラボを完了することで、ユーザーがデータベースに格納されているデータを次のように変更できるようにする方法を学習しました。

- インデックス、作成、編集、削除などのコントローラーアクション
- HTML テーブルにプロパティを表示するための ASP.NET MVC のスキャフォールディング機能
- ユーザーエクスペリエンスを向上させるためのカスタム HTML ヘルパー
- HTTP GET または HTTP POST 呼び出しのいずれかに対応するアクションメソッド
- 作成や編集などの類似ビューテンプレート用の共有エディターテンプレート
- ドロップダウンなどのフォーム要素
- モデル検証のデータ注釈
- JQuery の控えめのライブラリを使用したクライアント側の検証

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>付録 A: Visual Studio Express 2012 を Web 用にインストールする

**[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)** を使用して、Web または別の &quot;Express&quot; バージョン**用に Microsoft Visual Studio Express 2012**をインストールできます。 次の手順では、 *Microsoft Web Platform Installer*を使用して*Visual studio Express 2012 for Web*をインストールするために必要な手順について説明します。

1. [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)にアクセスします。 または、Web Platform Installer が既にインストールされている場合は、それを開いて、製品 &quot;<em>Visual Studio Express 2012 For web With Windows AZURE SDK</em>&quot;を検索することもできます。
2. **[今すぐインストール]** をクリックします。 **Web Platform Installer**がない場合は、最初にダウンロードしてインストールするようにリダイレクトされます。
3. **Web Platform Installer**が開いたら、 **[インストール]** をクリックしてセットアップを開始します。

    ![Visual Studio Express のインストール](aspnet-mvc-4-helpers-forms-and-validation/_static/image22.png "Visual Studio Express のインストール")

    *Visual Studio Express のインストール*
4. すべての製品のライセンスと条項を読み、[**同意**する] をクリックして続行します。

    ![ライセンス条項に同意する](aspnet-mvc-4-helpers-forms-and-validation/_static/image23.png)

    *ライセンス条項に同意する*
5. ダウンロードとインストールのプロセスが完了するまで待ちます。

    ![Installation progress](aspnet-mvc-4-helpers-forms-and-validation/_static/image24.png)

    *インストールの進行状況*
6. インストールが完了したら、 **[完了]** をクリックします。

    ![インストールの完了](aspnet-mvc-4-helpers-forms-and-validation/_static/image25.png)

    *インストールの完了*
7. **[終了]** をクリックして Web Platform Installer を閉じます。
8. Web 用の Visual Studio Express を開くには、**スタート**画面にアクセスして &quot;**VS Express**&quot;の書き込みを開始し、 **[VS Express for Web]** タイルをクリックします。

    ![VS Express for Web タイル](aspnet-mvc-4-helpers-forms-and-validation/_static/image26.png)

    *VS Express for Web タイル*

<a id="AppendixB"></a>

<a id="Appendix_B_Using_Code_Snippets"></a>
## <a name="appendix-b-using-code-snippets"></a>付録 B: コードスニペットの使用

コードスニペットを使用すると、必要なすべてのコードをすぐに利用できます。 次の図に示すように、ラボドキュメントには、使用できるタイミングがわかります。

![Visual Studio のコードスニペットを使用してプロジェクトにコードを挿入する](aspnet-mvc-4-helpers-forms-and-validation/_static/image27.png "Visual Studio のコードスニペットを使用してプロジェクトにコードを挿入する")

*Visual Studio のコードスニペットを使用してプロジェクトにコードを挿入する*

***キーボードを使用してコードスニペットを追加C#するには (のみ)***

1. コードを挿入する場所にカーソルを置きます。
2. (スペースまたはハイフンを含まない) スニペット名の入力を開始します。
3. IntelliSense によって、一致するスニペットの名前が表示されます。
4. 正しいスニペットを選択します (または、スニペットの名前全体が選択されるまで入力し続けます)。
5. Tab キーを2回押すと、スニペットがカーソル位置に挿入されます。

![スニペット名の入力を開始します](aspnet-mvc-4-helpers-forms-and-validation/_static/image28.png "スニペット名の入力を開始します")

*スニペット名の入力を開始します*

![Tab キーを押して、強調表示されているスニペットを選択します](aspnet-mvc-4-helpers-forms-and-validation/_static/image29.png "Tab キーを押して、強調表示されているスニペットを選択します")

*Tab キーを押して、強調表示されているスニペットを選択します*

![もう一度 Tab キーを押すと、スニペットが展開されます。](aspnet-mvc-4-helpers-forms-and-validation/_static/image30.png "もう一度 Tab キーを押すと、スニペットが展開されます。")

*もう一度 Tab キーを押すと、スニペットが展開されます。*

***マウスC#(、Visual Basic および XML) を使用してコードスニペットを追加するに***は1. コードスニペットを挿入する場所を右クリックします。

1. **[スニペットの挿入]** 、 **[マイコードスニペット**] の順に選択します。
2. 一覧から該当するスニペットをクリックして選択します。

![コードスニペットを挿入する場所を右クリックし、[スニペットの挿入] を選択します。](aspnet-mvc-4-helpers-forms-and-validation/_static/image31.png "コードスニペットを挿入する場所を右クリックし、[スニペットの挿入] を選択します。")

*コードスニペットを挿入する場所を右クリックし、[スニペットの挿入] を選択します。*

![一覧から関連するスニペットをクリックして選択します。](aspnet-mvc-4-helpers-forms-and-validation/_static/image32.png "一覧から関連するスニペットをクリックして選択します。")

*一覧から関連するスニペットをクリックして選択します。*
