---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-dependency-injection
title: ASP.NET MVC 4 依存関係の注入 |Microsoft Docs
author: rick-anderson
description: '注: このハンズオンラボでは、ASP.NET MVC と ASP.NET MVC 4 のフィルターに関する基本的な知識があることを前提としています。 前に ASP.NET MVC 4 フィルターを使用していない場合は、...'
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 84c7baca-1c54-4c44-8f52-4282122d6acb
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-dependency-injection
msc.type: authoredcontent
ms.openlocfilehash: 15c9d4dcb9e2c6b9f6adf54d65d15737b32cca3b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78451822"
---
# <a name="aspnet-mvc-4-dependency-injection"></a>ASP.NET MVC 4 依存関係挿入

[Web キャンプチーム](https://twitter.com/webcamps)別

[Web キャンプトレーニングキットをダウンロードする](https://aka.ms/webcamps-training-kit)

このハンズオンラボでは、 **ASP.NET mvc**と**ASP.NET mvc 4 フィルター**に関する基本的な知識があることを前提としています。 前に**ASP.NET mvc 4 フィルター**を使用していない場合は、 **ASP.NET Mvc カスタムアクションフィルター**のハンズオンラボに進むことをお勧めします。

> [!NOTE]
> すべてのサンプルコードとスニペットは、 [Microsoft web/WebCampTrainingKit リリース](https://aka.ms/webcamps-training-kit)から入手できる Web キャンプトレーニングキットに含まれています。 このラボに固有のプロジェクトは、 [ASP.NET MVC 4 依存関係の挿入](https://github.com/Microsoft-Web/HOL-MVC4DependencyInjection)で入手できます。

**オブジェクト指向プログラミング**パラダイムでは、オブジェクトは共同作成者とコンシューマーが存在するコラボレーションモデルで連携します。 当然ながら、この通信モデルでは、オブジェクトとコンポーネント間の依存関係が生成されるため、複雑さが増加しても管理が困難になります。

![クラスの依存関係とモデルの複雑さ](aspnet-mvc-4-dependency-injection/_static/image1.png "クラスの依存関係とモデルの複雑さ")

*クラスの依存関係とモデルの複雑さ*

多くの場合、**ファクトリパターン**と、サービスを使用したインターフェイスと実装の分離について耳にします。クライアントオブジェクトは、サービスの場所を担当します。

依存関係の注入パターンは、制御の反転の特定の実装です。 **制御の反転 (IoC)** は、オブジェクトがその他のオブジェクトを作成せずに作業に依存することを意味します。 代わりに、外部ソース (xml 構成ファイルなど) から必要なオブジェクトを取得します。

**依存関係の挿入 (DI)** は、オブジェクトの介入なしに実行されることを意味します。通常は、コンストラクターのパラメーターを渡し、プロパティを設定するフレームワークコンポーネントによって行われます。

<a id="The_Dependency_Injection_DI_Design_Pattern"></a>
### <a name="the-dependency-injection-di-design-pattern"></a>依存関係の挿入 (DI) デザインパターン

大まかに言えば、依存関係の注入の目的は、クライアントクラス (*ゴルファー*など) がインターフェイスを満たすもの ( *iclub*など) を必要とすることです。 具象型 (例: *WoodClub、IronClub、WedgeClub* 、または*putterclub*) は考慮されません。他のユーザーがそれを処理するようにします (たとえば、適切な*caddy*)。 ASP.NET MVC の依存関係競合回避モジュールを使用すると、他の場所 (コンテナーや*クラブのバッグ*など) に依存関係ロジックを登録できます。

![依存関係の挿入の図](aspnet-mvc-4-dependency-injection/_static/image2.png "依存関係の挿入の図")

*依存関係の挿入-ゴルフの例え*

依存関係の挿入パターンと制御の反転を使用する利点は次のとおりです。

- クラスの結合を減らす
- コードの再利用を増やす
- コードの保守性を向上させる
- アプリケーションテストの向上

> [!NOTE]
> 依存関係の挿入は、抽象ファクトリデザインパターンと比較されることがありますが、両方の方法にわずかな違いがあります。 DI には、ファクトリと登録済みサービスを呼び出すことによって依存関係を解決するためのフレームワークが用意されています。

依存関係の挿入パターンについて理解したところで、このラボ全体を通じて ASP.NET MVC 4 で適用する方法を学習します。 **コントローラー**で依存関係の挿入を使用して、データベースアクセスサービスを含めることを開始します。 次に、サービスを使用して情報を表示するために、依存関係の挿入を**ビュー**に適用します。 最後に、DI を ASP.NET MVC 4 フィルターに拡張し、ソリューションにカスタムアクションフィルターを挿入します。

このハンズオンラボでは、次の方法を学習します。

- NuGet パッケージを使用して依存関係の挿入を行うために ASP.NET MVC 4 と Unity を統合する
- ASP.NET MVC コントローラー内での依存関係の挿入の使用
- ASP.NET MVC ビュー内での依存関係の挿入の使用
- ASP.NET MVC アクションフィルター内での依存関係の挿入の使用

> [!NOTE]
> このラボでは、依存関係の解決に Mvc3 NuGet パッケージを使用していますが、ASP.NET MVC 4 で動作するように依存関係挿入フレームワークを調整することもできます。

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

1. [演習 1: コントローラーの挿入](#Exercise1)
2. [演習 2: ビューの挿入](#Exercise2)
3. [演習 3: フィルターの挿入](#Exercise3)

> [!NOTE]
> 各演習には、演習を完了した後に取得する必要があるソリューションを含む**終了**フォルダーが付属しています。 演習を通じて追加のヘルプが必要な場合は、このソリューションをガイドとして使用できます。

このラボの推定所要時間: **30 分**。

<a id="Exercise1"></a>

<a id="Exercise_1_Injecting_a_Controller"></a>
### <a name="exercise-1-injecting-a-controller"></a>演習 1: コントローラーの挿入

この演習では、NuGet パッケージを使用して Unity を統合することによって、ASP.NET MVC コントローラーで依存関係の挿入を使用する方法を学習します。 そのため、データアクセスからロジックを分離するために、MvcMusicStore コントローラーにサービスを含めます。 サービスは、コントローラーコンストラクターに新しい依存関係を作成します。これは、 **Unity**のヘルプを使用して依存関係の挿入を使用して解決されます。

このアプローチでは、より柔軟性が高く、保守とテストが容易な、結合の少ないアプリケーションを生成する方法について説明します。 また、ASP.NET MVC と Unity を統合する方法についても説明します。

<a id="About_StoreManager_Service"></a>
#### <a name="about-storemanager-service"></a>StoreManager サービスについて

Begin ソリューションで提供される MVC ミュージックストアには、 **Storeservice**という名前のストアコントローラーデータを管理するサービスが含まれるようになりました。 以下では、ストアサービスの実装について説明します。 すべてのメソッドがモデルエンティティを返すことに注意してください。

[!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample1.cs)]

Begin ソリューションの**StoreController**が**storeservice**を使用するようになりました。 すべてのデータ参照が**StoreController**から削除され、 **storeservice**を使用するメソッドを変更せずに現在のデータアクセスプロバイダーを変更できるようになりました。

**StoreController**実装には、クラスコンストラクター内で**storeservice**との依存関係があることがわかります。

> [!NOTE]
> この演習で導入された依存関係は、**制御の反転**(IoC) に関連しています。
> 
> **StoreController**クラスコンストラクターは、 **istoreservice**型パラメーターを受け取ります。これは、クラス内からのサービス呼び出しを実行するために不可欠です。 ただし、 **StoreController**は、コントローラーが ASP.NET MVC を操作するために必要な既定のコンストラクター (パラメーターなし) を実装していません。
> 
> 依存関係を解決するには、抽象ファクトリ (指定された型のオブジェクトを返すクラス) によってコントローラーを作成する必要があります。

[!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample2.cs)]

> [!NOTE]
> 宣言されたパラメーターなしのコンストラクターがないため、クラスがサービスオブジェクトを送信せずに StoreController を作成しようとすると、エラーが発生します。

<a id="Ex1Task1"></a>

<a id="Task_1_-_Running_the_Application"></a>
#### <a name="task-1---running-the-application"></a>タスク 1-アプリケーションを実行する

このタスクでは、Begin アプリケーションを実行します。このアプリケーションでは、アプリケーションロジックからデータアクセスを分離するストアコントローラーにサービスが含まれています。

アプリケーションを実行すると、既定ではコントローラーサービスがパラメーターとして渡されないため、例外が発生します。

1. **ソース \ Ex01-の挿入 Controller\Begin**にある**Begin**ソリューションを開きます。

   1. 続行する前に、不足している NuGet パッケージをダウンロードする必要があります。 これを行うには、 **[プロジェクト]** メニューをクリックし、 **[NuGet パッケージの管理]** を選択します。
   2. **[NuGet パッケージの管理]** ダイアログで、 **[復元]** をクリックして、不足しているパッケージをダウンロードします。
   3. 最後に、[**ビルド** | **ビルド**] をクリックしてソリューションをビルドします。

      > [!NOTE]
      > NuGet を使用する利点の1つは、プロジェクトのすべてのライブラリを配布する必要がなく、プロジェクトのサイズを小さくすることです。 NuGet パワーツールを使用すると、パッケージのバージョンを app.config ファイルで指定することで、プロジェクトを初めて実行するときに必要なすべてのライブラリをダウンロードできます。 このため、このラボから既存のソリューションを開いた後に、これらの手順を実行する必要があります。
2. Ctrl キーを押し**ながら F5**キーを押して、デバッグを行わずにアプリケーションを実行します。 **このオブジェクト&quot;にパラメーターなしのコンストラクターが定義されていない**&quot;エラーメッセージが表示されます。

    ![ASP.NET MVC Begin Application の実行中にエラーが発生しました](aspnet-mvc-4-dependency-injection/_static/image3.png "ASP.NET MVC Begin Application の実行中にエラーが発生しました")

    *ASP.NET MVC Begin Application の実行中にエラーが発生しました*
3. ブラウザーを閉じます。

次の手順では、このコントローラーが必要とする依存関係を挿入するミュージックストアソリューションについて説明します。

<a id="Ex1Task2"></a>

<a id="Task_2_-_Including_Unity_into_MvcMusicStore_Solution"></a>
#### <a name="task-2---including-unity-into-mvcmusicstore-solution"></a>タスク 2-Unity を MvcMusicStore ソリューションに含める

このタスクでは、 **Mvc3** NuGet パッケージをソリューションに追加します。

> [!NOTE]
> Mvc3 パッケージは ASP.NET MVC 3 向けに設計されていますが、ASP.NET MVC 4 と完全に互換性があります。
> 
> Unity は、拡張可能な軽量の依存関係挿入コンテナーであり、オプションでインスタンスと型のインターセプトをサポートします。 これは、あらゆる種類の .NET アプリケーションで使用するための汎用コンテナーです。 オブジェクトの作成、実行時の依存関係の指定による要件の抽象化、コンポーネントの構成をコンテナーに延期することによって、依存関係の注入メカニズムに含まれる共通の機能をすべて提供します。

1. **MvcMusicStore**プロジェクトに**Mvc3** NuGet パッケージをインストールします。 これを行うには、[**他のウィンドウ** | **表示**] から**パッケージマネージャーコンソール**を開きます。
2. 次のコマンドを実行します。

    PMC

    [!code-powershell[Main](aspnet-mvc-4-dependency-injection/samples/sample3.ps1)]

    ![Mvc3 NuGet パッケージをインストールしています](aspnet-mvc-4-dependency-injection/_static/image4.png "Mvc3 NuGet パッケージをインストールしています")

    *Mvc3 NuGet パッケージをインストールしています*
3. Unity の構成を簡略化するために、 **Mvc3**パッケージがインストールされたら、自動的に追加されるファイルとフォルダーを調べます。

    ![インストールされている Mvc3 パッケージ](aspnet-mvc-4-dependency-injection/_static/image5.png "インストールされている Mvc3 パッケージ")

    *インストールされている Mvc3 パッケージ*

<a id="Ex1Task3"></a>

<a id="Task_3_-_Registering_Unity_in_Globalasaxcs_Application_Start"></a>
#### <a name="task-3---registering-unity-in-globalasaxcs-application_start"></a>タスク 3-Global.asax.cs アプリケーションへの Unity の登録\_開始

このタスクでは、 **Global.asax.cs**にある**アプリケーション\_開始**メソッドを更新して Unity ブートストラップ初期化子を呼び出し、依存関係の挿入に使用するサービスとコントローラーを登録するブートストラップファイルを更新します。

1. 次に、Unity コンテナーと依存関係競合回避モジュールを初期化するファイルであるブートストラップをフックします。 これを行うには、 **Global.asax.cs**を開き、次の強調表示されたコードを**Application\_Start**メソッド内に追加します。

    (コードスニペット- *ASP.NET Dependency インジェクション Lab-Ex01-Initialize Unity*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample4.cs)]
2. **Bootstrapper.cs**ファイルを開きます。
3. **MvcMusicStore**と**MusicStore**の各名前空間を含めます。

    (コードスニペット- *ASP.NET Dependency インジェクション Lab-Ex01-ブートストラップ名前空間の追加*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample5.cs)]
4. **Buildunitycontainer**メソッドの内容を、ストアコントローラーとストアサービスを登録する次のコードに置き換えます。

    (コードスニペット- *ASP.NET Dependency インジェクション Lab-Ex01-Register Store Controller And Service*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample6.cs)]

<a id="Ex1Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a>タスク 4-アプリケーションを実行する

このタスクでは、アプリケーションを実行して、Unity をインクルードした後でアプリケーションを読み込むことができることを確認します。

1. **F5**キーを押してアプリケーションを実行すると、エラーメッセージを表示せずにアプリケーションが読み込まれるようになります。

    ![依存関係の挿入を使用したアプリケーションの実行](aspnet-mvc-4-dependency-injection/_static/image6.png "依存関係の挿入を使用したアプリケーションの実行")

    *依存関係の挿入を使用したアプリケーションの実行*
2. **/ストア**に移動します。 これにより、 **Unity**を使用して作成された**StoreController**が呼び出されます。

    ![MVC ミュージックストア](aspnet-mvc-4-dependency-injection/_static/image7.png "MVC ミュージックストア")

    *MVC ミュージックストア*
3. ブラウザーを閉じます。

次の演習では、ASP.NET MVC ビューおよびアクションフィルター内で使用するように依存関係挿入スコープを拡張する方法について説明します。

<a id="Exercise2"></a>

<a id="Exercise_2_Injecting_a_View"></a>
### <a name="exercise-2-injecting-a-view"></a>演習 2: ビューの挿入

この演習では、ASP.NET MVC 4 for Unity 統合の新機能を使用して、ビューで依存関係の挿入を使用する方法について説明します。 そのためには、ストアの参照ビュー内でカスタムサービスを呼び出します。これにより、次のメッセージと画像が表示されます。

次に、プロジェクトを Unity と統合し、カスタム依存関係競合回避モジュールを作成して依存関係を挿入します。

<a id="Ex2Task1"></a>

<a id="Task_1_-_Creating_a_View_that_Consumes_a_Service"></a>
#### <a name="task-1---creating-a-view-that-consumes-a-service"></a>タスク 1-サービスを使用するビューの作成

このタスクでは、サービス呼び出しを実行して新しい依存関係を生成するビューを作成します。 このサービスは、このソリューションに含まれる単純なメッセージングサービスで構成されています。

1. **Sourceex02-挿入 View\ begin**フォルダーにある**begin**ソリューションを開きます。 それ以外の場合は、前の演習を完了することによって得られた**終了**ソリューションを引き続き使用することができます。

   1. 提供された**Begin**ソリューションを開いた場合は、続行する前に、不足している NuGet パッケージをダウンロードする必要があります。 これを行うには、 **[プロジェクト]** メニューをクリックし、 **[NuGet パッケージの管理]** を選択します。
   2. **[NuGet パッケージの管理]** ダイアログで、 **[復元]** をクリックして、不足しているパッケージをダウンロードします。
   3. 最後に、[**ビルド** | **ビルド**] をクリックしてソリューションをビルドします。

      > [!NOTE]
      > NuGet を使用する利点の1つは、プロジェクトのすべてのライブラリを配布する必要がなく、プロジェクトのサイズを小さくすることです。 NuGet パワーツールを使用すると、パッケージのバージョンを app.config ファイルで指定することで、プロジェクトを初めて実行するときに必要なすべてのライブラリをダウンロードできます。 このため、このラボから既存のソリューションを開いた後に、これらの手順を実行する必要があります。
      > 
      > 詳細については、「 [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages)」を参照してください。
2. **ソース \ Assets**フォルダーにある**MessageService.cs**クラスと**IMessageService.cs**クラスを **/Services**に含めます。 これを行うには、 **[サービス]** フォルダーを右クリックし、 **[既存項目の追加]** を選択します。 ファイルの場所を参照して指定します。

    ![メッセージサービスとサービスインターフェイスの追加](aspnet-mvc-4-dependency-injection/_static/image8.png "メッセージサービスとサービスインターフェイスの追加")

    *メッセージサービスとサービスインターフェイスの追加*

    > [!NOTE]
    > **IMessageService**インターフェイスは、 **messageservice**クラスによって実装される2つのプロパティを定義します。 これらのプロパティ-**メッセージ**と**ImageUrl**-メッセージと、表示されるイメージの URL を格納します。
3. プロジェクトのルートフォルダーにフォルダー **/ページ**を作成し、 **MyBasePage.cs**の既存のクラスを追加し**ます。** 継承元の基本ページの構造は次のとおりです。

    ![ページフォルダー](aspnet-mvc-4-dependency-injection/_static/image9.png "Pages フォルダー")

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample7.cs)]
4. /ビュー/**ストア**フォルダーから**Browse**ビューを開き、 **MyBasePage.cs**から継承されるようにします。

    [!code-cshtml[Main](aspnet-mvc-4-dependency-injection/samples/sample8.cshtml)]
5. **参照**ビューで、 **messageservice**の呼び出しを追加して、イメージとサービスによって取得されたメッセージを表示します。
   (C#)

    [!code-cshtml[Main](aspnet-mvc-4-dependency-injection/samples/sample9.cshtml)]

<a id="Ex2Task2"></a>

<a id="Task_2_-_Including_a_Custom_Dependency_Resolver_and_a_Custom_View_Page_Activator"></a>
#### <a name="task-2---including-a-custom-dependency-resolver-and-a-custom-view-page-activator"></a>タスク 2-カスタム依存関係競合回避モジュールとカスタムビューページアクティベーターを含む

前のタスクでは、ビュー内に新しい依存関係を挿入し、その中でサービス呼び出しを実行していました。 次に、ASP.NET MVC 依存関係挿入インターフェイス**Iviewpageactivator**と**idependencyresolver**を実装することで、その依存関係を解決します。 Unity を使用したサービスの取得を処理する**Idependencyresolver**の実装は、ソリューションに含めます。 次に、ビューの作成を解決する**Iviewpageactivator**インターフェイスの別のカスタム実装を追加します。

> [!NOTE]
> ASP.NET MVC 3 以降、依存関係の挿入の実装により、サービスを登録するためのインターフェイスが簡略化されました。 **Idependencyresolver**と**Iviewpageactivator**は、依存関係の挿入のための ASP.NET MVC 3 機能の一部です。
> 
> **-Idependencyresolver**インターフェイスは、前の IMvcServiceLocator を置き換えます。 IDependencyResolver の実装は、サービスまたはサービスコレクションのインスタンスを返す必要があります。
> 
> 
> [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample10.cs)]
> 
> **-Iviewpageactivator**インターフェイスを使用すると、依存関係の挿入によってビューページをインスタンス化する方法をより細かく制御できます。 **Iviewpageactivator**インターフェイスを実装するクラスは、コンテキスト情報を使用してビューインスタンスを作成できます。
> 
> 
> [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample11.cs)]

1. プロジェクトのルートフォルダーに/**factory**フォルダーを作成します。
2. **/Sources/Assets/** to **factory**フォルダーからソリューションに**CustomViewPageActivator.cs**を追加します。 これを行うには、 **/工場** フォルダーを右クリックし、追加 を選択します。 **既存の項目** をクリックし、**CustomViewPageActivator.cs** を選択します。 このクラスは、Unity コンテナーを保持する**Iviewpageactivator**インターフェイスを実装します。

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample12.cs)]

    > [!NOTE]
    > **Customviewpageactivator**は、Unity コンテナーを使用してビューの作成を管理する役割を担います。
3. **UnityDependencyResolver.cs** **ファイルをインクルードフォルダーに追加** **します**。 これを行うには、 **/工場** フォルダーを右クリックし、追加 を選択します。 **既存の項目** をクリックし、**UnityDependencyResolver.cs** file を選択します。

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample13.cs)]

    > [!NOTE]
    > **Unitydependencyresolver**クラスは、Unity のカスタム dependencyresolver です。 Unity コンテナー内にサービスが見つからない場合、基本競合回避モジュールは invocated です。

次のタスクでは、両方の実装が登録され、モデルでサービスとビューの場所を把握できるようになります。

<a id="Ex2Task3"></a>

<a id="Task_3_-_Registering_for_Dependency_Injection_within_Unity_container"></a>
#### <a name="task-3---registering-for-dependency-injection-within-unity-container"></a>タスク 3-Unity コンテナー内での依存関係の挿入の登録

このタスクでは、依存関係の挿入を行うために、前のすべての項目をまとめます。

現在、ソリューションには次の要素があります。

- **MyBaseClass**から継承し、 **messageservice**を使用する**参照**ビュー。
- サービスインターフェイスに対して依存関係の挿入が宣言されている中間クラス**MyBaseClass**。
- サービス**Messageservice**とそのインターフェイス**IMessageService**。
- サービスの取得を処理する Unity- **Unitydependencyresolver**のカスタム依存関係競合回避モジュール。
- ページを作成するビューページアクティベーター- **Customviewpageactivator** 。

**参照**ビューを挿入するには、Unity コンテナーにカスタム依存関係競合回避モジュールを登録します。

1. **Bootstrapper.cs**ファイルを開きます。
2. サービスを初期化するために、 **Messageservice**のインスタンスを Unity コンテナーに登録します。

    (コードスニペット- *ASP.NET Dependency インジェクション Lab-Ex02-Register Message Service*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample14.cs)]
3. **MvcMusicStore**名前空間への参照を追加します。

    (コードスニペット- *ASP.NET Dependency インジェクション Lab-Ex02 名前空間*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample15.cs)]
4. **Customviewpageactivator**をビューページアクティベーターとして Unity コンテナーに登録します。

    (コードスニペット- *ASP.NET Dependency インジェクション Lab-Ex02-Register CustomViewPageActivator*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample16.cs)]
5. ASP.NET MVC 4 の既定の依存関係競合回避モジュールを**Unitydependencyresolver**のインスタンスに置き換えます。 これを行うには、 **Initialize**メソッドの内容を次のコードに置き換えます。

    (コードスニペット- *ASP.NET Dependency インジェクション Lab-Ex02-Update Dependency Resolver*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample17.cs)]

    > [!NOTE]
    > ASP.NET MVC には、既定の依存関係リゾルバークラスが用意されています。 Unity 用に作成したものとしてカスタム依存関係競合回避モジュールを使用するには、このリゾルバーを置き換える必要があります。

<a id="Ex2Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a>タスク 4-アプリケーションを実行する

このタスクでは、アプリケーションを実行して、ストアブラウザーがサービスを使用し、取得したイメージとメッセージが表示されることを確認します。

1. **F5** キーを押してアプリケーションを実行します。
2. ジャンル メニュー内の **ロック** をクリックし、 **messageservice**がビューに挿入され、ウェルカムメッセージと画像が読み込まれたことを確認します。 この例では、を入力して、**ロック**&quot;を &quot;します。

    ![MVC ミュージックストア-ビューの挿入](aspnet-mvc-4-dependency-injection/_static/image10.png "MVC ミュージックストア-ビューの挿入")

    *MVC ミュージックストア-ビューの挿入*
3. ブラウザーを閉じます。

<a id="Exercise3"></a>

<a id="Exercise_3_Injecting_Action_Filters"></a>
### <a name="exercise-3-injecting-action-filters"></a>演習 3: アクションフィルターの挿入

前のハンズオンラボの**カスタムアクションフィルター**では、フィルターのカスタマイズと挿入が使用されていました。 この演習では、Unity コンテナーを使用して依存関係の挿入を含むフィルターを挿入する方法について説明します。 これを行うには、サイトのアクティビティをトレースするカスタムアクションフィルターをミュージックストアソリューションに追加します。

<a id="Ex3Task1"></a>

<a id="Task_1_-_Including_the_Tracking_Filter_in_the_Solution"></a>
#### <a name="task-1---including-the-tracking-filter-in-the-solution"></a>タスク 1-ソリューション内の追跡フィルターを含む

このタスクでは、[ミュージックストアにカスタムアクションフィルターを追加してイベントをトレースする] を選択します。 カスタムアクションフィルターの概念は、前のラボで既に処理されています。カスタムアクションフィルター&quot;&quot;、このラボの Assets フォルダーからフィルタークラスを追加し、Unity のフィルタープロバイダーを作成します。

1. **ソース \ ex03-挿入アクション filter¥ begin**フォルダーにある**begin**ソリューションを開きます。 それ以外の場合は、前の演習を完了することによって得られた**終了**ソリューションを引き続き使用することができます。

   1. 提供された**Begin**ソリューションを開いた場合は、続行する前に、不足している NuGet パッケージをダウンロードする必要があります。 これを行うには、 **[プロジェクト]** メニューをクリックし、 **[NuGet パッケージの管理]** を選択します。
   2. **[NuGet パッケージの管理]** ダイアログで、 **[復元]** をクリックして、不足しているパッケージをダウンロードします。
   3. 最後に、[**ビルド** | **ビルド**] をクリックしてソリューションをビルドします。

      > [!NOTE]
      > NuGet を使用する利点の1つは、プロジェクトのすべてのライブラリを配布する必要がなく、プロジェクトのサイズを小さくすることです。 NuGet パワーツールを使用すると、パッケージのバージョンを app.config ファイルで指定することで、プロジェクトを初めて実行するときに必要なすべてのライブラリをダウンロードできます。 このため、このラボから既存のソリューションを開いた後に、これらの手順を実行する必要があります。
      > 
      > 詳細については、「 [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages)」を参照してください。
2. **TraceActionFilter.cs** **ファイルをインクルードフォルダーに追加** **します**。

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample18.cs)]

    > [!NOTE]
    > このカスタムアクションフィルターは、ASP.NET のトレースを実行します。 詳細については、&quot;ASP.NET MVC 4 のローカルアクションフィルターと動的アクションフィルター&quot; ラボを確認してください。
3. 空のクラス**FilterProvider.cs** **をフォルダー内**のプロジェクトに追加します。
4. FilterProvider.cs 名前**空間と、** **その名前**空間をに追加します。

    (コードスニペット- *ASP.NET 依存関係挿入ラボ-Ex03 プロバイダーの名前空間の追加*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample19.cs)]
5. クラスが**Ifilterprovider**インターフェイスから継承されるようにします。

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample20.cs)]
6. **Filterprovider**クラスに**Iunitycontainer**プロパティを追加し、コンテナーを割り当てるクラスコンストラクターを作成します。

    (コードスニペット- *ASP.NET Dependency インジェクション Ex03-Filter Provider コンストラクター*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample21.cs)]

    > [!NOTE]
    > フィルタープロバイダークラスコンストラクターが、内に**新しい**オブジェクトを作成していません。 コンテナーはパラメーターとして渡され、その依存関係は Unity によって解決されます。
7. **Filterprovider**クラスで、 **ifilterprovider**インターフェイスから**getfilters**メソッドを実装します。

    (コードスニペット- *ASP.NET Dependency インジェクション Ex03-Filter Provider GetFilters*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample22.cs)]

<a id="Ex3Task2"></a>

<a id="Task_2_-_Registering_and_Enabling_the_Filter"></a>
#### <a name="task-2---registering-and-enabling-the-filter"></a>タスク 2-フィルターの登録と有効化

このタスクでは、サイトの追跡を有効にします。 これを行うには、 **Bootstrapper.cs BuildUnityContainer**メソッドにフィルターを登録して、トレースを開始します。

1. プロジェクトルートに**ある web.config を開き、** system.web グループでトレース追跡を有効にします。

    [!code-xml[Main](aspnet-mvc-4-dependency-injection/samples/sample23.xml)]
2. プロジェクトルートで**Bootstrapper.cs**を開きます。
3. **MvcMusicStore**名前空間への参照を追加します。

    (コードスニペット- *ASP.NET Dependency インジェクション Lab-Ex03-ブートストラップ名前空間の追加*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample24.cs)]
4. **Buildunitycontainer**メソッドを選択し、Unity コンテナーにフィルターを登録します。 フィルタープロバイダーとアクションフィルターを登録する必要があります。

    (コードスニペット- *ASP.NET Dependency インジェクション Lab-Ex03-Register FilterProvider And ActionFilter*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample25.cs)]

<a id="Ex3Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a>タスク 3-アプリケーションを実行する

このタスクでは、アプリケーションを実行し、カスタムアクションフィルターがアクティビティをトレースしていることをテストします。

1. **F5** キーを押してアプリケーションを実行します。
2. ジャンル メニュー内の **ロック** をクリックします。 必要に応じて、より多くのジャンルを参照できます。

    ![Music Store](aspnet-mvc-4-dependency-injection/_static/image11.png "Music Store")

    *Music Store*
3. [アプリケーショントレース] ページを参照して選択し、[**詳細の表示** **] をクリック**します。

    ![アプリケーショントレースログ](aspnet-mvc-4-dependency-injection/_static/image12.png "アプリケーショントレースログ")

    *アプリケーショントレースログ*

    ![アプリケーショントレース-要求の詳細](aspnet-mvc-4-dependency-injection/_static/image13.png "アプリケーショントレース-要求の詳細")

    *アプリケーショントレース-要求の詳細*
4. ブラウザーを閉じます。

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a>まとめ

このハンズオンラボを完了すると、NuGet パッケージを使用して Unity を統合することで、ASP.NET MVC 4 で依存関係の挿入を使用する方法を学習できました。 これを実現するには、コントローラー、ビュー、およびアクションフィルター内で依存関係の挿入を使用しました。

次の概念について説明しました。

- ASP.NET MVC 4 依存関係挿入機能
- Unity の Mvc3 NuGet パッケージを使用した統合
- コントローラーでの依存関係の挿入
- ビューでの依存関係の挿入
- アクションフィルターの依存関係の挿入

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>付録 A: Visual Studio Express 2012 を Web 用にインストールする

**[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)** を使用して、Web または別の &quot;Express&quot; バージョン**用に Microsoft Visual Studio Express 2012**をインストールできます。 次の手順では、 *Microsoft Web Platform Installer*を使用して*Visual studio Express 2012 for Web*をインストールするために必要な手順について説明します。

1. [https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169) に移動します。 または、Web Platform Installer が既にインストールされている場合は、それを開いて、製品 &quot;<em>Visual Studio Express 2012 For web With Windows AZURE SDK</em>&quot;を検索することもできます。
2. **[今すぐインストール]** をクリックします。 **Web Platform Installer**がない場合は、最初にダウンロードしてインストールするようにリダイレクトされます。
3. **Web Platform Installer**が開いたら、 **[インストール]** をクリックしてセットアップを開始します。

    ![Visual Studio Express のインストール](aspnet-mvc-4-dependency-injection/_static/image14.png "Visual Studio Express のインストール")

    *Visual Studio Express のインストール*
4. すべての製品のライセンスと条項を読み、[**同意**する] をクリックして続行します。

    ![ライセンス条項に同意する](aspnet-mvc-4-dependency-injection/_static/image15.png)

    *ライセンス条項に同意する*
5. ダウンロードとインストールのプロセスが完了するまで待ちます。

    ![Installation progress](aspnet-mvc-4-dependency-injection/_static/image16.png)

    *インストールの進行状況*
6. インストールが完了したら、 **[完了]** をクリックします。

    ![インストールの完了](aspnet-mvc-4-dependency-injection/_static/image17.png)

    *インストールの完了*
7. **[終了]** をクリックして Web Platform Installer を閉じます。
8. Web 用の Visual Studio Express を開くには、**スタート**画面にアクセスして &quot;**VS Express**&quot;の書き込みを開始し、 **[VS Express for Web]** タイルをクリックします。

    ![VS Express for Web タイル](aspnet-mvc-4-dependency-injection/_static/image18.png)

    *VS Express for Web タイル*

<a id="AppendixB"></a>

<a id="Appendix_B_Using_Code_Snippets"></a>
## <a name="appendix-b-using-code-snippets"></a>付録 B: コードスニペットの使用

コードスニペットを使用すると、必要なすべてのコードをすぐに利用できます。 次の図に示すように、ラボドキュメントには、使用できるタイミングがわかります。

![Visual Studio のコードスニペットを使用してプロジェクトにコードを挿入する](aspnet-mvc-4-dependency-injection/_static/image19.png "Visual Studio のコードスニペットを使用してプロジェクトにコードを挿入する")

*Visual Studio のコードスニペットを使用してプロジェクトにコードを挿入する*

***キーボードを使用してコードスニペットを追加C#するには (のみ)***

1. コードを挿入する場所にカーソルを置きます。
2. (スペースまたはハイフンを含まない) スニペット名の入力を開始します。
3. IntelliSense によって、一致するスニペットの名前が表示されます。
4. 正しいスニペットを選択します (または、スニペットの名前全体が選択されるまで入力し続けます)。
5. Tab キーを2回押すと、スニペットがカーソル位置に挿入されます。

![スニペット名の入力を開始します](aspnet-mvc-4-dependency-injection/_static/image20.png "スニペット名の入力を開始します")

*スニペット名の入力を開始します*

![Tab キーを押して、強調表示されているスニペットを選択します](aspnet-mvc-4-dependency-injection/_static/image21.png "Tab キーを押して、強調表示されているスニペットを選択します")

*Tab キーを押して、強調表示されているスニペットを選択します*

![もう一度 Tab キーを押すと、スニペットが展開されます。](aspnet-mvc-4-dependency-injection/_static/image22.png "もう一度 Tab キーを押すと、スニペットが展開されます。")

*もう一度 Tab キーを押すと、スニペットが展開されます。*

***マウスC#(、Visual Basic および XML) を使用してコードスニペットを追加するに***は1. コードスニペットを挿入する場所を右クリックします。

1. **[スニペットの挿入]** 、 **[マイコードスニペット**] の順に選択します。
2. 一覧から該当するスニペットをクリックして選択します。

![コードスニペットを挿入する場所を右クリックし、[スニペットの挿入] を選択します。](aspnet-mvc-4-dependency-injection/_static/image23.png "コードスニペットを挿入する場所を右クリックし、[スニペットの挿入] を選択します。")

*コードスニペットを挿入する場所を右クリックし、[スニペットの挿入] を選択します。*

![一覧から関連するスニペットをクリックして選択します。](aspnet-mvc-4-dependency-injection/_static/image24.png "一覧から関連するスニペットをクリックして選択します。")

*一覧から関連するスニペットをクリックして選択します。*
