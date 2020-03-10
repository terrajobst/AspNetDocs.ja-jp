---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-custom-action-filters
title: ASP.NET MVC 4 カスタムアクションフィルター |Microsoft Docs
author: rick-anderson
description: ASP.NET MVC には、アクションメソッドが呼び出される前または後にフィルター処理ロジックを実行するためのアクションフィルターが用意されています。 アクションフィルターはカスタム属性 tha...
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 969ab824-1b98-4552-81fe-b60ef5fc6887
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-custom-action-filters
msc.type: authoredcontent
ms.openlocfilehash: eaeb32180f79fabf557cbc38ff067eb26b47fea7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78468178"
---
# <a name="aspnet-mvc-4-custom-action-filters"></a>ASP.NET MVC 4 カスタム アクション フィルター

[Web キャンプチーム](https://twitter.com/webcamps)別

[Web キャンプトレーニングキットをダウンロードする](https://aka.ms/webcamps-training-kit)

ASP.NET MVC には、アクションメソッドが呼び出される前または後にフィルター処理ロジックを実行するためのアクションフィルターが用意されています。 アクションフィルターは、コントローラーのアクションメソッドに事前アクション動作とアクション後動作を追加するための宣言型の手段を提供するカスタム属性です。

このハンズオンラボでは、MvcMusicStore solution にカスタムアクションフィルター属性を作成して、コントローラーの要求をキャッチし、サイトのアクティビティをデータベーステーブルに記録します。 任意のコントローラーまたはアクションに挿入することによって、ログ記録フィルターを追加することができます。 最後に、訪問者の一覧を示すログビューが表示されます。

このハンズオンラボでは、 **ASP.NET MVC**に関する基本的な知識があることを前提としています。 以前に**ASP.NET mvc**を使用していない場合は、 **ASP.NET Mvc 4 の基礎**となるハンズオンラボに進むことをお勧めします。

> [!NOTE]
> すべてのサンプルコードとスニペットは、 [Microsoft web/WebCampTrainingKit リリース](https://aka.ms/webcamps-training-kit)から入手できる Web キャンプトレーニングキットに含まれています。 このラボに固有のプロジェクトは、 [ASP.NET MVC 4 カスタムアクションフィルター](https://github.com/Microsoft-Web/HOL-MVC4CustomActionFilters)で入手できます。

<a id="Objectives"></a>
### <a name="objectives"></a>目標

このハンズオンラボでは、次の方法を学習します。

- フィルター機能を拡張するカスタムアクションフィルター属性を作成する
- 特定のレベルへの挿入によるカスタムフィルター属性の適用
- カスタムアクションフィルターをグローバルに登録する

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

1. [演習 1: 操作のログ記録](#Exercise1)
2. [演習 2: 複数のアクションフィルターの管理](#Exercise2)

このラボの推定所要時間: **30 分**。

> [!NOTE]
> 各演習には、演習を完了した後に取得する必要があるソリューションを含む**終了**フォルダーが付属しています。 演習を通じて追加のヘルプが必要な場合は、このソリューションをガイドとして使用できます。

<a id="Exercise1"></a>

<a id="Exercise_1_Logging_Actions"></a>
### <a name="exercise-1-logging-actions"></a>演習 1: 操作のログ記録

この演習では、ASP.NET MVC 4 フィルタープロバイダーを使用してカスタムアクションログフィルターを作成する方法について説明します。 そのため、選択したコントローラー内のすべてのアクティビティを記録するログフィルターを MusicStore サイトに適用します。

フィルターは**Actionfilter属性 eclass**を拡張し、 **onactionexecuting**メソッドをオーバーライドして各要求をキャッチし、ログアクションを実行します。 HTTP 要求、実行メソッド、結果、およびパラメーターに関するコンテキスト情報は、ASP.NET MVC **Actionexecutingcontext**クラスによって提供され**ます。**

> [!NOTE]
> ASP.NET MVC 4 には、カスタムフィルターを作成せずに使用できる既定のフィルタープロバイダーもあります。 ASP.NET MVC 4 には、次の種類のフィルターが用意されています。
> 
> - **承認**フィルター。認証の実行、要求のプロパティの検証など、アクションメソッドを実行するかどうかに関するセキュリティ上の決定を行います。
> - **アクションフィルター。** アクションメソッドの実行をラップします。 このフィルターでは、アクションメソッドへの追加データの提供、戻り値の検査、アクションメソッドの実行の取り消しなど、追加の処理を実行できます。
> - **結果**フィルター。 actionresult オブジェクトの実行をラップします。 このフィルターは、HTTP 応答の変更など、結果の追加処理を実行できます。
> - **例外**フィルター。アクションメソッドのどこかでスローされた未処理の例外がある場合に実行されます。承認フィルターから開始し、結果の実行で終了します。 例外フィルターは、ログの記録やエラー ページの表示などのタスクに使用できます。
> 
> フィルタープロバイダーの詳細については、こちらの MSDN リンク ([https://msdn.microsoft.com/library/dd410209.aspx](https://msdn.microsoft.com/library/dd410209.aspx)) を参照してください。

<a id="AboutLoggingFeature"></a>

<a id="About_MVC_Music_Store_Application_logging_feature"></a>
#### <a name="about-mvc-music-store-application-logging-feature"></a>MVC ミュージックストアアプリケーションログ機能について

このミュージックストアソリューションには、サイトログ、 **Actionlog**の新しいデータモデルテーブルがあります。このフィールドには、要求を受信したコントローラーの名前 (Action、Client IP、および Time stamp) が含まれています。

![データモデル。ActionLog テーブル。](aspnet-mvc-4-custom-action-filters/_static/image1.png "データモデル。ActionLog テーブル。")

*データモデル-ActionLog テーブル*

このソリューションには、アクションログの ASP.NET MVC ビューが用意されています。これは、 **MvcMusicStores/Views/ActionLog**にあります。

![操作ログの表示](aspnet-mvc-4-custom-action-filters/_static/image2.png "操作ログの表示")

*操作ログの表示*

この構造では、すべての作業はコントローラーの要求を中断し、カスタムフィルターを使用してログ記録を実行します。

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_a_Custom_Filter_to_Catch_a_Controllers_Request"></a>
#### <a name="task-1---creating-a-custom-filter-to-catch-a-controllers-request"></a>タスク 1-コントローラーの要求をキャッチするカスタムフィルターを作成する

この作業では、ログ記録ロジックを含むカスタムフィルター属性クラスを作成します。 そのためには、ASP.NET MVC **Actionfilterattribute**クラスを拡張し、インターフェイス**iactionfilter**を実装します。

> [!NOTE]
> **Actionfilterattribute**は、すべての属性フィルターの基本クラスです。 このメソッドには、コントローラーアクションの実行後および実行前に特定のロジックを実行するための次のメソッドが用意されています。
> 
> - **Onactionexecuting**(actionexecutingcontext filtercontext): アクションメソッドが呼び出される直前。
> - **Onactionexecuted**(actionexecutedcontext filtercontext): アクションメソッドが呼び出された後、結果が実行される前 (ビューレンダリングの前)。
> - **Onresultexecuting**(resultexecutingcontext filtercontext): 結果が実行される直前 (ビューレンダリングの前)。
> - **Onresultexecuted**(resultexecutedcontext filtercontext): 結果が実行された後 (ビューが表示された後)。
> 
> これらのメソッドのいずれかを派生クラスにオーバーライドすることにより、独自のフィルター処理コードを実行できます。

1. **\ Source\ Ex01-のジョブ \ 開始**フォルダーにある**begin**ソリューションを開きます。

   1. 続行する前に、不足している NuGet パッケージをダウンロードする必要があります。 これを行うには、 **[プロジェクト]** メニューをクリックし、 **[NuGet パッケージの管理]** を選択します。
   2. **[NuGet パッケージの管理]** ダイアログで、 **[復元]** をクリックして、不足しているパッケージをダウンロードします。
   3. 最後に、[**ビルド** | **ビルド**] をクリックしてソリューションをビルドします。

      > [!NOTE]
      > NuGet を使用する利点の1つは、プロジェクトのすべてのライブラリを配布する必要がなく、プロジェクトのサイズを小さくすることです。 NuGet パワーツールを使用すると、パッケージのバージョンを app.config ファイルで指定することで、プロジェクトを初めて実行するときに必要なすべてのライブラリをダウンロードできます。 このため、このラボから既存のソリューションを開いた後に、これらの手順を実行する必要があります。
      > 
      > 詳細については、「 [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages)」を参照してください。
2. Filters フォルダーにC#新しいクラスを追加し、 *CustomActionFilter.cs*という名前を指定します。 このフォルダーには、すべてのカスタムフィルターが格納されます。
3. **CustomActionFilter.cs**を開き、 **MvcMusicStore**名前空間と名前**空間への**参照を追加します。

    (コードスニペット- *ASP.NET MVC 4 カスタムアクションフィルター-Ex1-CustomActionFilterNamespaces*)

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample1.cs)]
4. **Actionfilterattribute**から**CustomActionFilter**クラスを継承し、 **CustomActionFilter**クラスが**iactionfilter**インターフェイスを実装するようにします。

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample2.cs)]
5. **CustomActionFilter**クラスは、 **onactionexecuting**メソッドをオーバーライドし、フィルターの実行をログに記録するために必要なロジックを追加します。 これを行うには、 **CustomActionFilter**クラス内に次の強調表示されたコードを追加します。

    (コードスニペット- *ASP.NET MVC 4 カスタムアクションフィルター-Ex1-ログインアクション*)

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample3.cs#Highlight)]

    > [!NOTE]
    > **Onactionexecuting**メソッドでは**Entity Framework**を使用して新しい actionlog レジスタを追加しています。 **Filtercontext**からのコンテキスト情報を使用して、新しいエンティティインスタンスを作成して入力します。
    > 
    > **コントローラーのコントローラー**の詳細については、 [msdn](https://msdn.microsoft.com/library/system.web.mvc.controllercontext.aspx)を参照してください。

<a id="Ex1Task2"></a>

<a id="Task_2_-_Injecting_a_Code_Interceptor_into_the_Store_Controller_Class"></a>
#### <a name="task-2---injecting-a-code-interceptor-into-the-store-controller-class"></a>タスク 2-ストアコントローラークラスにコードインターセプターを挿入する

このタスクでは、ログに記録されるすべてのコントローラークラスとコントローラーアクションにカスタムフィルターを挿入することによって、カスタムフィルターを追加します。 この演習では、Store Controller クラスにログがあります。

**Actionlogfilterattribute**カスタムフィルターから実行されるメソッド**onactionexecuting** 、挿入された要素が呼び出されると実行されます。

特定のコントローラーメソッドをインターセプトすることもできます。

1. **MvcMusicStore\Controllers**で**StoreController**を開き、 **Filters**名前空間への参照を追加します。

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample4.cs)]
2. クラス宣言の前に **[CustomActionFilter]** 属性を追加して、カスタムフィルター **CustomActionFilter**を**StoreController**クラスに挿入します。

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample5.cs)]

   > [!NOTE]
   > フィルターがコントローラークラスに挿入されると、そのすべてのアクションも挿入されます。 一連のアクションに対してのみフィルターを適用する場合は、 **[CustomActionFilter]** をそれぞれに挿入する必要があります。
   > 
   > [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample6.cs)]

<a id="Ex1Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a>タスク 3-アプリケーションを実行する

このタスクでは、ログ記録フィルターが機能していることをテストします。 アプリケーションを起動してストアにアクセスし、ログに記録されたアクティビティを確認します。

1. **F5** キーを押してアプリケーションを実行します。
2. **/Actionlog**を参照して、ログビューの初期状態を確認します。

    ![ページアクティビティ前のログトラッカーの状態](aspnet-mvc-4-custom-action-filters/_static/image3.png "ページアクティビティ前のログトラッカーの状態")

    *ページアクティビティ前のログトラッカーの状態*

   > [!NOTE]
   > 既定では、メニューの既存のジャンルを取得するときに生成される1つの項目が常に表示されます。
   > 
   > わかりやすくするために、アプリケーションを実行するたびに**Actionlog**テーブルをクリーンアップしています。これにより、各タスクの検証のログのみが表示されるようになります。
   > 
   > ストアコントローラー内で実行されるすべてのアクションの履歴ログを保存するために、**セッション\_Start**メソッド ( **global.asax**クラス) から次のコードを削除する必要がある場合があります。
   > 
   > [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample7.cs)]
3. メニューからいずれかの**ジャンル**をクリックし、利用可能なアルバムの閲覧など、いくつかの操作を実行します。
4. **/Actionlog**を参照し、ログが空の場合は**F5**キーを押してページを更新します。 訪問が追跡されたことを確認します。

    ![アクティビティが記録されたアクションログ](aspnet-mvc-4-custom-action-filters/_static/image4.png "アクティビティが記録されたアクションログ")

    *アクティビティが記録されたアクションログ*

<a id="Exercise2"></a>

<a id="Exercise_2_Managing_Multiple_Action_Filters"></a>
### <a name="exercise-2-managing-multiple-action-filters"></a>演習 2: 複数のアクションフィルターの管理

この演習では、StoreController クラスに2つ目のカスタムアクションフィルターを追加し、両方のフィルターが実行される特定の順序を定義します。 次に、フィルターをグローバルに登録するようにコードを更新します。

フィルターの実行順序を定義する際には、さまざまなオプションを考慮する必要があります。 たとえば、Order プロパティとフィルターのスコープは、次のようになります。

フィルターごとに**スコープ**を定義できます。たとえば、**コントローラースコープ**内で実行するすべてのアクションフィルターと、**グローバルスコープ**で実行するすべての承認フィルターのスコープを設定できます。 スコープには、定義済みの実行順序があります。

また、各アクションフィルターには、フィルターのスコープ内で実行順序を決定するために使用される Order プロパティがあります。

カスタムアクションフィルターの実行順序の詳細については、MSDN の記事「([https://msdn.microsoft.com/library/dd381609(v=vs.98).aspx](https://msdn.microsoft.com/library/dd381609(v=vs.98).aspx))」を参照してください。

<a id="Ex2Task1"></a>

<a id="Task_1_Creating_a_new_Custom_Action_Filter"></a>
#### <a name="task-1-creating-a-new-custom-action-filter"></a>タスク 1: 新しいカスタムアクションフィルターを作成する

このタスクでは、新しいカスタムアクションフィルターを作成して、StoreController クラスに挿入し、フィルターの実行順序を管理する方法を学習します。

1. **\Source\Ex02-ManagingMultipleActionFilters\Begin**フォルダーにある**Begin**ソリューションを開きます。 それ以外の場合は、前の演習を完了することによって得られた**終了**ソリューションを引き続き使用することができます。

    1. 提供された**Begin**ソリューションを開いた場合は、続行する前に、不足している NuGet パッケージをダウンロードする必要があります。 これを行うには、 **[プロジェクト]** メニューをクリックし、 **[NuGet パッケージの管理]** を選択します。
    2. **[NuGet パッケージの管理]** ダイアログで、 **[復元]** をクリックして、不足しているパッケージをダウンロードします。
    3. 最後に、[**ビルド** | **ビルド**] をクリックしてソリューションをビルドします。

        > [!NOTE]
        > NuGet を使用する利点の1つは、プロジェクトのすべてのライブラリを配布する必要がなく、プロジェクトのサイズを小さくすることです。 NuGet パワーツールを使用すると、パッケージのバージョンを app.config ファイルで指定することで、プロジェクトを初めて実行するときに必要なすべてのライブラリをダウンロードできます。 このため、このラボから既存のソリューションを開いた後に、これらの手順を実行する必要があります。
        > 
        > 詳細については、「 [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages)」を参照してください。
2. Filters フォルダーにC#新しいクラスを追加し、 *MyNewCustomActionFilter.cs*という名前を指定します。
3. **MyNewCustomActionFilter.cs**を開き、 **system.web**および**MvcMusicStore**名前空間への参照を追加します。

    (コードスニペット- *ASP.NET MVC 4 カスタムアクションフィルター-Ex2-MyNewCustomActionFilterNamespaces*)

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample8.cs)]
4. 既定のクラス宣言を次のコードに置き換えます。

    (コードスニペット- *ASP.NET MVC 4 カスタムアクションフィルター-Ex2-MyNewCustomActionFilterClass*)

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample9.cs)]

    > [!NOTE]
    > このカスタムアクションフィルターは、前の演習で作成したものとほぼ同じです。 主な違いは、 *&quot;属性によって記録*された&quot;がこの新しいクラスの名前で更新され、どのフィルターがログに登録されたかを識別することです。

<a id="Ex2Task2"></a>

<a id="Task_2_Injecting_a_new_Code_Interceptor_into_the_StoreController_Class"></a>
#### <a name="task-2-injecting-a-new-code-interceptor-into-the-storecontroller-class"></a>タスク 2: 新しいコードインターセプターを StoreController クラスに挿入する

このタスクでは、新しいカスタムフィルターを StoreController クラスに追加し、ソリューションを実行して、両方のフィルターが連携する方法を確認します。

1. **MvcMusicStore\Controllers**にある**StoreController**クラスを開き、次のコードに示すように、新しいカスタムフィルター **MyNewCustomActionFilter**を**StoreController**クラスに挿入します。

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample10.cs)]
2. ここで、アプリケーションを実行して、これら2つのカスタムアクションフィルターがどのように機能するかを確認します。 これを行うには、 **F5**キーを押して、アプリケーションが起動するまで待ちます。
3. **/Actionlog**を参照して、ログビューの初期状態を確認します。

    ![ページアクティビティ前のログトラッカーの状態](aspnet-mvc-4-custom-action-filters/_static/image5.png "ページアクティビティ前のログトラッカーの状態")

    *ページアクティビティ前のログトラッカーの状態*
4. メニューからいずれかの**ジャンル**をクリックし、利用可能なアルバムの閲覧など、いくつかの操作を実行します。
5. この時刻を確認してください。訪問が2回追跡されました。 **StorageController**クラスに追加したカスタムアクションフィルターごとに1回です。

    ![アクティビティが記録されたアクションログ](aspnet-mvc-4-custom-action-filters/_static/image6.png "アクティビティが記録されたアクションログ")

    *アクティビティが記録されたアクションログ*
6. ブラウザーを閉じます。

<a id="Ex2Task3"></a>

<a id="Task_3_Managing_Filter_Ordering"></a>
#### <a name="task-3-managing-filter-ordering"></a>タスク 3: フィルターの順序を管理する

このタスクでは、Order プロパティを使用してフィルターの実行順序を管理する方法を学習します。

1. **MvcMusicStore\Controllers**にある**StoreController**クラスを開き、次に示すように、両方のフィルターで**Order**プロパティを指定します。

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample11.cs)]
2. 次に、Order プロパティの値に応じて、フィルターがどのように実行されるかを確認します。 最小の順序の値 (**CustomActionFilter**) を持つフィルターが、最初に実行されるフィルターであることがわかります。 **F5**キーを押して、アプリケーションが起動するまで待ちます。
3. **/Actionlog**を参照して、ログビューの初期状態を確認します。

    ![ページアクティビティ前のログトラッカーの状態](aspnet-mvc-4-custom-action-filters/_static/image7.png "ページアクティビティ前のログトラッカーの状態")

    *ページアクティビティ前のログトラッカーの状態*
4. メニューからいずれかの**ジャンル**をクリックし、利用可能なアルバムの閲覧など、いくつかの操作を実行します。
5. この時間が経過すると、最初にフィルターの順序値: **CustomActionFilter** logs によってアクセスが追跡されることを確認します。

    ![アクティビティが記録されたアクションログ](aspnet-mvc-4-custom-action-filters/_static/image8.png "アクティビティが記録されたアクションログ")

    *アクティビティが記録されたアクションログ*
6. ここで、フィルターの順序の値を更新し、ログの順序がどのように変わるかを確認します。 **StoreController**クラスで、フィルターの順序の値を次のように更新します。

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample12.cs)]
7. **F5**キーを押してアプリケーションを再実行します。
8. メニューからいずれかの**ジャンル**をクリックし、利用可能なアルバムの閲覧など、いくつかの操作を実行します。
9. この時間が経過すると、 **MyNewCustomActionFilter** filter によって作成されたログが先に表示されます。

    ![アクティビティが記録されたアクションログ](aspnet-mvc-4-custom-action-filters/_static/image9.png "アクティビティが記録されたアクションログ")

    *アクティビティが記録されたアクションログ*

<a id="Ex2Task4"></a>

<a id="Task_4_Registering_Filters_Globally"></a>
#### <a name="task-4-registering-filters-globally"></a>タスク 4: フィルターをグローバルに登録する

このタスクでは、新しいフィルター (**MyNewCustomActionFilter**) をグローバルフィルターとして登録するようにソリューションを更新します。 これにより、アプリケーションで実行されるすべてのアクションによってトリガーされます。前のタスクと同様に、StoreController のすべてのアクションがトリガーされます。

1. **StoreController**クラスで、[ **MyNewCustomActionFilter]** 属性と Order プロパティを **[CustomActionFilter]** から削除します。 この要素は次のようになります。

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample13.cs)]
2. **Global.asax**ファイルを開き、 **Application\_Start**メソッドを見つけます。 アプリケーションが起動するたびに、 **Filterconfig**クラス内で**registerglobalfilters**メソッドを呼び出すことによってグローバルフィルターが登録されることに注意してください。

    ![グローバルフィルターを global.asax に登録しています](aspnet-mvc-4-custom-action-filters/_static/image10.png "グローバルフィルターを global.asax に登録しています")

    *グローバルフィルターを global.asax に登録しています*
3. **アプリ\_** の [開始フォルダー] で**FilterConfig.cs**ファイルを開きます。
4. System.web. Mvc を使用してへの参照を追加します。MvcMusicStore を使用します。空間.

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample14.cs)]
5. **Registerglobalfilters**メソッドを更新して、カスタムフィルターを追加します。 これを行うには、強調表示されたコードを追加します。

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample15.cs)]
6. **F5** キーを押してアプリケーションを実行します。
7. メニューからいずれかの**ジャンル**をクリックし、利用可能なアルバムの閲覧など、いくつかの操作を実行します。
8. 今すぐ **[MyNewCustomActionFilter]** が HomeController と ActionLogController に挿入されていることを確認してください。

    ![アクティビティが記録されたアクションログ](aspnet-mvc-4-custom-action-filters/_static/image11.png "アクティビティが記録されたアクションログ")

    *グローバルアクティビティが記録されたアクションログ*

> [!NOTE]
> また、 [「付録 B: Web 配置を使用した ASP.NET MVC 4 アプリケーションの発行](#AppendixB)」に従って、このアプリケーションを Windows Azure の Web サイトにデプロイすることもできます。

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a>まとめ

このハンズオンラボでは、アクションフィルターを拡張してカスタムアクションを実行する方法について学習しました。 また、任意のフィルターをページコントローラーに挿入する方法についても学習しました。 次の概念が使用されました。

- ASP.NET MVC ActionFilterAttribute クラスを使用してカスタムアクションフィルターを作成する方法
- ASP.NET MVC コントローラーにフィルターを挿入する方法
- Order プロパティを使用してフィルターの順序を管理する方法
- フィルターをグローバルに登録する方法

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>付録 A: Visual Studio Express 2012 を Web 用にインストールする

**[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)** を使用して、Web または別の &quot;Express&quot; バージョン**用に Microsoft Visual Studio Express 2012**をインストールできます。 次の手順では、 *Microsoft Web Platform Installer*を使用して*Visual studio Express 2012 for Web*をインストールするために必要な手順について説明します。

1. [https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169) に移動します。 または、Web Platform Installer が既にインストールされている場合は、それを開いて、製品 &quot;<em>Visual Studio Express 2012 For web With Windows AZURE SDK</em>&quot;を検索することもできます。
2. **[今すぐインストール]** をクリックします。 **Web Platform Installer**がない場合は、最初にダウンロードしてインストールするようにリダイレクトされます。
3. **Web Platform Installer**が開いたら、 **[インストール]** をクリックしてセットアップを開始します。

    ![Visual Studio Express のインストール](aspnet-mvc-4-custom-action-filters/_static/image12.png "Visual Studio Express のインストール")

    *Visual Studio Express のインストール*
4. すべての製品のライセンスと条項を読み、[**同意**する] をクリックして続行します。

    ![ライセンス条項に同意する](aspnet-mvc-4-custom-action-filters/_static/image13.png)

    *ライセンス条項に同意する*
5. ダウンロードとインストールのプロセスが完了するまで待ちます。

    ![Installation progress](aspnet-mvc-4-custom-action-filters/_static/image14.png)

    *インストールの進行状況*
6. インストールが完了したら、 **[完了]** をクリックします。

    ![インストールの完了](aspnet-mvc-4-custom-action-filters/_static/image15.png)

    *インストールの完了*
7. **[終了]** をクリックして Web Platform Installer を閉じます。
8. Web 用の Visual Studio Express を開くには、**スタート**画面にアクセスして &quot;**VS Express**&quot;の書き込みを開始し、 **[VS Express for Web]** タイルをクリックします。

    ![VS Express for Web タイル](aspnet-mvc-4-custom-action-filters/_static/image16.png)

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

    ![Windows Azure portal にログオンします。](aspnet-mvc-4-custom-action-filters/_static/image17.png "Windows Azure portal にログオンします。")

    *Windows Azure 管理ポータルにログオンします。*
2. コマンドバーの **[新規]** をクリックします。

    ![新しい Web サイトの作成](aspnet-mvc-4-custom-action-filters/_static/image18.png "新しい Web サイトの作成")

    *新しい Web サイトの作成*
3. [ **Compute** | **Web サイト**] をクリックします。 次に、 **[簡易作成]** オプションを選択します。 新しい web サイトの使用可能な URL を指定し、 **[Web サイトの作成]** をクリックします。

    > [!NOTE]
    > Windows Azure の Web サイトは、制御および管理が可能なクラウドで実行されている web アプリケーションのホストです。 [簡易作成] オプションを使用すると、完成した web アプリケーションをポータルの外部から Windows Azure の Web サイトにデプロイできます。 データベースを設定する手順は含まれていません。

    ![簡易作成を使用した新しい Web サイトの作成](aspnet-mvc-4-custom-action-filters/_static/image19.png "簡易作成を使用した新しい Web サイトの作成")

    *簡易作成を使用した新しい Web サイトの作成*
4. 新しい**Web サイト**が作成されるまで待ちます。
5. Web サイトが作成されたら、 **[URL]** 列の下のリンクをクリックします。 新しい Web サイトが機能していることを確認します。

    ![新しい web サイトを参照しています](aspnet-mvc-4-custom-action-filters/_static/image20.png "新しい web サイトを参照しています")

    *新しい web サイトを参照しています*

    ![実行中の Web サイト](aspnet-mvc-4-custom-action-filters/_static/image21.png "実行中の Web サイト")

    *実行中の Web サイト*
6. ポータルに戻り、 **[名前]** 列の下にある web サイトの名前をクリックして、管理ページを表示します。

    ![Web サイトの管理ページを開く](aspnet-mvc-4-custom-action-filters/_static/image22.png "Web サイトの管理ページを開く")

    *Web サイトの管理ページを開く*
7. **[ダッシュボード]** ページの **[概要] セクションで**、 **[発行プロファイルのダウンロード]** リンクをクリックします。

    > [!NOTE]
    > *発行プロファイル*には、有効になっている各発行方法について、Windows Azure web サイトに web アプリケーションを発行するために必要なすべての情報が含まれています。 発行プロファイルには、発行メソッドが有効化される各エンドポイントに接続して認証するために必要な URL、ユーザーの資格情報、およびデータベース文字列が含まれています。 **Microsoft WebMatrix 2**、 **Microsoft Visual Studio Express for Web**および**Microsoft Visual Studio 2012**では、発行プロファイルを読み取り、Web アプリケーションを Windows Azure websites に発行するためのこれらのプログラムの構成を自動化することがサポートされています。

    ![Web サイト発行プロファイルをダウンロードしています](aspnet-mvc-4-custom-action-filters/_static/image23.png "Web サイト発行プロファイルをダウンロードしています")

    *Web サイト発行プロファイルをダウンロードしています*
8. 発行プロファイルファイルを既知の場所にダウンロードします。 この演習では、このファイルを使用して、Visual Studio から Windows Azure Web サイトに web アプリケーションを発行する方法について説明します。

    ![発行プロファイルファイルを保存しています](aspnet-mvc-4-custom-action-filters/_static/image24.png "発行プロファイルを保存しています")

    *発行プロファイルファイルを保存しています*

<a id="ApxBTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a>タスク 2-データベースサーバーの構成

アプリケーションで SQL Server データベースを使用する場合は、SQL Database サーバーを作成する必要があります。 SQL Server を使用しない単純なアプリケーションを展開する場合は、このタスクを省略できます。

1. アプリケーションデータベースを格納するには、SQL Database サーバーが必要です。 サブスクリプションの**SQL Database サーバーは**、Windows Azure 管理ポータルの**SQL データベース** | サーバー | **サーバーのダッシュボード**で確認できます。 サーバーを作成していない場合は、コマンドバーの **[追加]** ボタンを使用して作成できます。 次のタスクで使用するので、**サーバー名と URL、管理者のログイン名、パスワード**をメモしておきます。 データベースは、後の段階で作成されるため、まだ作成しないでください。

    ![SQL Database サーバーダッシュボード](aspnet-mvc-4-custom-action-filters/_static/image25.png "SQL Database サーバーダッシュボード")

    *SQL Database サーバーダッシュボード*
2. 次のタスクでは、Visual Studio からデータベース接続をテストします。そのため、**使用可能な Ip アドレス**の一覧にローカル ip アドレスを含める必要があります。 これを行うには、 **[構成]** をクリックし、 **[現在のクライアント IP アドレス]** の ip アドレスを選択して、 **[開始 Ip アドレス]** と **[終了 ip アドレス]** のテキストボックスに貼り付け、[![の](aspnet-mvc-4-custom-action-filters/_static/image26.png) 追加] をクリックします。

    ![クライアント IP アドレスを追加しています](aspnet-mvc-4-custom-action-filters/_static/image27.png)

    *クライアント IP アドレスを追加しています*
3. [許可された IP アドレス] の一覧に**クライアントの Ip アドレス**が追加されたら、 **[保存]** をクリックして変更を確認します。

    ![変更の確認](aspnet-mvc-4-custom-action-filters/_static/image28.png)

    *変更の確認*

<a id="ApxBTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>タスク 3-Web 配置を使用した ASP.NET MVC 4 アプリケーションの発行

1. ASP.NET MVC 4 ソリューションに戻ります。 **ソリューションエクスプローラー**で、web サイトプロジェクトを右クリックし、 **[発行]** を選択します。

    ![アプリケーションの発行](aspnet-mvc-4-custom-action-filters/_static/image29.png "アプリケーションの発行")

    *Web サイトの公開*
2. 最初のタスクで保存した発行プロファイルをインポートします。

    ![発行プロファイルをインポートしています](aspnet-mvc-4-custom-action-filters/_static/image30.png "発行プロファイルをインポートしています")

    *発行プロファイルをインポートしています*
3. **[接続の検証]** をクリックします。 検証が完了したら、 **[次へ]** をクリックします。

    > [!NOTE]
    > 検証が完了すると、[接続の検証] ボタンの横に緑色のチェックマークが表示されます。

    ![接続の検証](aspnet-mvc-4-custom-action-filters/_static/image31.png "接続の検証")

    *接続の検証*
4. **[設定]** ページの **[データベース]** セクションで、データベース接続のテキストボックスの横にあるボタン ( **defaultconnection**など) をクリックします。

    ![Web deploy の構成](aspnet-mvc-4-custom-action-filters/_static/image32.png "Web deploy の構成")

    *Web deploy の構成*
5. 次のようにデータベース接続を構成します。

   - **サーバー名**には、 *tcp:* プレフィックスを使用して SQL Database サーバーの URL を入力します。
   - **User name (ユーザー名**) に、サーバー管理者のログイン名を入力します。
   - **パスワード**で、サーバー管理者のログインパスワードを入力します。
   - 新しいデータベース名を入力します。

     ![変換先の接続文字列を構成しています](aspnet-mvc-4-custom-action-filters/_static/image33.png "変換先の接続文字列を構成しています")

     *変換先の接続文字列を構成しています*
6. 次に、 **[OK]** をクリックします データベースの作成を求めるメッセージが表示されたら、[**はい]** をクリックします。

    ![データベースの作成](aspnet-mvc-4-custom-action-filters/_static/image34.png "データベース文字列の作成")

    *データベースの作成*
7. Windows Azure の SQL Database に接続するために使用する接続文字列は、[既定の接続] ボックスに表示されます。 続けて、 **[次へ]** をクリックします。

    ![SQL Database を指す接続文字列](aspnet-mvc-4-custom-action-filters/_static/image35.png "SQL Database を指す接続文字列")

    *SQL Database を指す接続文字列*
8. **[プレビュー]** ページで、 **[発行]** をクリックします。

    ![Web アプリケーションの発行](aspnet-mvc-4-custom-action-filters/_static/image36.png "Web アプリケーションの発行")

    *Web アプリケーションの発行*
9. 発行プロセスが完了すると、既定のブラウザーによって公開された web サイトが開きます。

<a id="AppendixC"></a>

<a id="Appendix_C_Using_Code_Snippets"></a>
## <a name="appendix-c-using-code-snippets"></a>付録 C: コードスニペットの使用

コードスニペットを使用すると、必要なすべてのコードをすぐに利用できます。 次の図に示すように、ラボドキュメントには、使用できるタイミングがわかります。

![Visual Studio のコードスニペットを使用してプロジェクトにコードを挿入する](aspnet-mvc-4-custom-action-filters/_static/image37.png "Visual Studio のコードスニペットを使用してプロジェクトにコードを挿入する")

*Visual Studio のコードスニペットを使用してプロジェクトにコードを挿入する*

***キーボードを使用してコードスニペットを追加C#するには (のみ)***

1. コードを挿入する場所にカーソルを置きます。
2. (スペースまたはハイフンを含まない) スニペット名の入力を開始します。
3. IntelliSense によって、一致するスニペットの名前が表示されます。
4. 正しいスニペットを選択します (または、スニペットの名前全体が選択されるまで入力し続けます)。
5. Tab キーを2回押すと、スニペットがカーソル位置に挿入されます。

![スニペット名の入力を開始します](aspnet-mvc-4-custom-action-filters/_static/image38.png "スニペット名の入力を開始します")

*スニペット名の入力を開始します*

![Tab キーを押して、強調表示されているスニペットを選択します](aspnet-mvc-4-custom-action-filters/_static/image39.png "Tab キーを押して、強調表示されているスニペットを選択します")

*Tab キーを押して、強調表示されているスニペットを選択します*

![もう一度 Tab キーを押すと、スニペットが展開されます。](aspnet-mvc-4-custom-action-filters/_static/image40.png "もう一度 Tab キーを押すと、スニペットが展開されます。")

*もう一度 Tab キーを押すと、スニペットが展開されます。*

***マウスC#(、Visual Basic および XML) を使用してコードスニペットを追加するに***は1. コードスニペットを挿入する場所を右クリックします。

1. **[スニペットの挿入]** 、 **[マイコードスニペット**] の順に選択します。
2. 一覧から該当するスニペットをクリックして選択します。

![コードスニペットを挿入する場所を右クリックし、[スニペットの挿入] を選択します。](aspnet-mvc-4-custom-action-filters/_static/image41.png "コードスニペットを挿入する場所を右クリックし、[スニペットの挿入] を選択します。")

*コードスニペットを挿入する場所を右クリックし、[スニペットの挿入] を選択します。*

![一覧から関連するスニペットをクリックして選択します。](aspnet-mvc-4-custom-action-filters/_static/image42.png "一覧から関連するスニペットをクリックして選択します。")

*一覧から関連するスニペットをクリックして選択します。*
