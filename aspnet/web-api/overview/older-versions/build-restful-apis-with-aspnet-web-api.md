---
uid: web-api/overview/older-versions/build-restful-apis-with-aspnet-web-api
title: ASP.NET Web API-ASP.NET 4.x を使用して RESTful Api をビルドする
author: rick-anderson
description: 'ハンズオンラボ: ASP.NET 4.x の Web API を使用して、contact manager アプリケーションの簡単な REST API を作成します。'
ms.author: riande
ms.date: 02/18/2013
ms.custom: seoapril2019
ms.assetid: 87daa99f-3810-407e-b969-dd28a192959d
msc.legacyurl: /web-api/overview/older-versions/build-restful-apis-with-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 35b115d6b4f84084e78e429bbb4842670e57bba4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78504268"
---
# <a name="build-restful-apis-with-aspnet-web-api"></a>ASP.NET Web API で RESTful Api をビルドする

[Web キャンプチーム](https://twitter.com/webcamps)別

> ハンズオンラボ: ASP.NET 4.x の Web API を使用して、contact manager アプリケーションの簡単な REST API を作成します。 また、API を使用するクライアントを構築します。

近年、HTTP が HTML ページを提供するだけではないことが明らかになっています。 また、いくつかの動詞 (GET、POST など) に加え、 *uri*や*ヘッダー*などのいくつかの簡単な概念を使用して、Web api を構築するための強力なプラットフォームでもあります。 ASP.NET Web API は、HTTP プログラミングを簡素化するコンポーネントのセットです。 ASP.NET MVC ランタイムの上に構築されているため、Web API は HTTP の低レベルトランスポートの詳細を自動的に処理します。 同時に、Web API は通常、HTTP プログラミングモデルを公開します。 実際、Web API の目的の1つは、HTTP の事実を抽象化し*ないこと*です。 その結果、Web API は柔軟性が高く、簡単に拡張することができます。  REST アーキテクチャスタイルは、http を利用するための効果的な方法であることが実証されていますが、HTTP に対する唯一の有効なアプローチではありません。 連絡先マネージャーは、連絡先の一覧表示、追加、および削除のための RESTful を公開します。 

このラボでは、HTTP、REST、および HTML、JavaScript、jQuery に関する基本的な知識があることを前提としています。
> 
> > [!NOTE]
> > ASP.NET Web サイトには、 [https://asp.net/web-api](https://asp.net/web-api)の ASP.NET Web API フレームワーク専用の領域があります。 このサイトでは、Web API に関する最新の情報、サンプル、ニュースが引き続き提供されます。そのため、事実上あらゆるデバイスまたは開発フレームワークで使用できるカスタム Web Api の作成について詳しく掘り下げたい場合は、頻繁に確認してください。
> > 
> > ASP.NET Web API は、ASP.NET MVC 4 に似ていますが、サービス層をコントローラーから分離することによって非常に柔軟で、利用可能ないくつかの依存関係挿入フレームワークを非常に簡単に使用できます。 MSDN には、[ここ](https://code.msdn.microsoft.com/ASPNET-Web-API-JavaScript-d0d64dd7)からダウンロードできる ASP.NET Web API プロジェクトでの依存関係の挿入に ninject を使用する方法を示す優れたサンプルが用意されています。
> 
> 
> すべてのサンプルコードとスニペットは、 [https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409)で入手できる Web キャンプトレーニングキットに含まれています。

<a id="Objectives"></a>
### <a name="objectives"></a>目標

このハンズオンラボでは、次の方法を学習します。

- RESTful Web API を実装する
- HTML クライアントから API を呼び出す

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>前提条件

このハンズオンラボを完了するには、次のものが必要です。

- Web またはそれ以降[の2012を Microsoft Visual Studio Express](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web)します (付録 B をインストールする手順については、 [「付録 B](#AppendixB) 」を参照してください)。

<a id="Setup"></a>
### <a name="setup"></a>セットアップ

**コードスニペットのインストール**

便宜上、このラボで管理するコードの多くは、Visual Studio のコードスニペットとして提供されています。 コードスニペットをインストールするには、 **.\Source\Setup\CodeSnippets.vsi**ファイルを実行します。

Visual Studio Code のスニペットを使い慣れておらず、その使用方法を学習する場合は、このドキュメントの付録「[付録 a: コードスニペット](#AppendixA)&quot;の使用」 &quot;参照してください。

<a id="Exercises"></a>
## <a name="exercises"></a>手順

このハンズオンラボには、次の演習が含まれています。

1. [演習 1: 読み取り専用の Web API を作成する](#Exercise1)
2. [演習 2: 読み取り/書き込み Web API を作成する](#Exercise2)
3. [演習 3: HTML クライアントから Web API を使用する](#Exercise3)

> [!NOTE]
> 各演習には、演習を完了した後に取得する必要があるソリューションを含む**終了**フォルダーが付属しています。 演習を通じて追加のヘルプが必要な場合は、このソリューションをガイドとして使用できます。

このラボの推定所要時間: **60 分**。

<a id="Exercise1"></a>

<a id="Exercise_1_Create_a_Read-Only_Web_API"></a>
### <a name="exercise-1-create-a-read-only-web-api"></a>演習 1: 読み取り専用の Web API を作成する

この演習では、連絡先マネージャーに読み取り専用の GET メソッドを実装します。

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_the_API_Project"></a>
#### <a name="task-1---creating-the-api-project"></a>タスク 1-API プロジェクトの作成

このタスクでは、新しい ASP.NET web プロジェクトテンプレートを使用して、Web API web アプリケーションを作成します。

1. **Visual Studio 2012 Express For Web**を実行し**ます。これ**を行うには、 **[スタート]** に移り、 **VS Express for Web**入力して、enter キーを押します。
2. **[ファイル]** メニューの **[新しいプロジェクト]** をクリックします。 Visual | を選択します。  **C#** [プロジェクトの種類] ツリービューの [web プロジェクトの種類] をクリックし、 **ASP.NET MVC 4 web アプリケーション**プロジェクトの種類を選択します。 プロジェクトの**名前**を*contactmanager*に設定し、**ソリューション名**を*開始*して、[ **OK]** をクリックします。

    ![新しい ASP.NET MVC 4.0 Web アプリケーションプロジェクトの作成](build-restful-apis-with-aspnet-web-api/_static/image1.png "新しい ASP.NET MVC 4.0 Web アプリケーションプロジェクトの作成")

    *新しい ASP.NET MVC 4.0 Web アプリケーションプロジェクトの作成*
3. ASP.NET MVC 4 プロジェクトの種類 ダイアログで、 **WEB API** プロジェクトの種類を選択します。 **[OK]** をクリックします。

    ![Web API プロジェクトの種類の指定](build-restful-apis-with-aspnet-web-api/_static/image2.png "Web API プロジェクトの種類の指定")

    *Web API プロジェクトの種類の指定*

<a id="Ex1Task2"></a>

<a id="Task_2_-_Creating_the_Contact_Manager_API_Controllers"></a>
#### <a name="task-2---creating-the-contact-manager-api-controllers"></a>タスク 2-Contact Manager API コントローラーの作成

このタスクでは、API メソッドが存在するコントローラークラスを作成します。

1. **Controllers**フォルダー内の**ValuesController.cs**という名前のファイルをプロジェクトから削除します。
2. プロジェクト内の**Controllers**フォルダーを右クリックし、[追加] を選択します。コンテキストメニューの [コントローラー]。

    ![プロジェクトへの新しいコントローラーの追加](build-restful-apis-with-aspnet-web-api/_static/image3.png "プロジェクトへの新しいコントローラーの追加")

    *プロジェクトへの新しいコントローラーの追加*
3. 表示される **[コントローラーの追加]** ダイアログボックスで、テンプレート メニューの **[空の API コントローラー]** を選択します。 コントローラークラスに**contactcontroller**という名前を指定します。 次に、[追加] をクリックし**ます。**

    ![[コントローラーの追加] ダイアログボックスを使用して新しい Web API コントローラーを作成する](build-restful-apis-with-aspnet-web-api/_static/image4.png "[コントローラーの追加] ダイアログボックスを使用して新しい Web API コントローラーを作成する")

    *[コントローラーの追加] ダイアログボックスを使用して新しい Web API コントローラーを作成する*
4. 次のコードを**Contactcontroller**に追加します。

    (コードスニペット- *WEB Api Ex01-GET Api メソッド*)

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample1.cs)]
5. **F5** キーを押してアプリケーションをデバッグします。 Web API プロジェクトの既定のホームページが表示されます。

    ![ASP.NET Web API アプリケーションの既定のホームページ](build-restful-apis-with-aspnet-web-api/_static/image5.png "ASP.NET Web API アプリケーションの既定のホームページ")

    *ASP.NET Web API アプリケーションの既定のホームページ*
6. Internet Explorer ウィンドウで、 **F12**キーを押して **[開発者ツール]** ウィンドウを開きます。 **[ネットワーク]** タブをクリックし、 **[キャプチャの開始]** ボタンをクリックして、ウィンドウへのネットワークトラフィックのキャプチャを開始します。

    ![[ネットワーク] タブを開いてネットワークキャプチャを開始する](build-restful-apis-with-aspnet-web-api/_static/image6.png "[ネットワーク] タブを開いてネットワークキャプチャを開始する")

    *[ネットワーク] タブを開いてネットワークキャプチャを開始する*
7. ブラウザーのアドレスバーに **/api/contact**という URL を追加し、enter キーを押します。 転送の詳細は、[ネットワークキャプチャ] ウィンドウに表示されます。 応答の MIME の種類は**application/json**であることに注意してください。 これは、既定の出力形式が JSON であることを示しています。

    ![ネットワークビューでの Web API 要求の出力の表示](build-restful-apis-with-aspnet-web-api/_static/image7.png "ネットワークビューでの Web API 要求の出力の表示")

    *ネットワークビューでの Web API 要求の出力の表示*

    > [!NOTE]
    > この時点での Internet Explorer 10 の既定の動作では、ユーザーが Web API 呼び出しによって生成されたストリームを保存するか開くかを確認します。 出力は、Web API URL 呼び出しの JSON 結果を含むテキストファイルになります。 開発者ツールウィンドウで応答の内容を見ることができるように、ダイアログをキャンセルしないでください。
8. **[詳細表示に進む]** ボタンをクリックして、この API 呼び出しの応答に関する詳細を表示します。

    ![詳細ビューに切り替え](build-restful-apis-with-aspnet-web-api/_static/image8.png "詳細ビューに切り替え")

    *詳細ビューに切り替え*
9. **[応答本文]** タブをクリックして、実際の JSON 応答テキストを表示します。

    ![ネットワークモニターでの JSON 出力テキストの表示](build-restful-apis-with-aspnet-web-api/_static/image9.png "ネットワークモニターでの JSON 出力テキストの表示")

    *ネットワークモニターでの JSON 出力テキストの表示*

<a id="Ex1Task3"></a>

<a id="Task_3_-_Creating_the_Contact_Models_and_Augment_the_Contact_Controller"></a>
#### <a name="task-3---creating-the-contact-models-and-augment-the-contact-controller"></a>タスク 3-連絡先モデルの作成と連絡先コントローラーの拡張

このタスクでは、API メソッドが存在するコントローラークラスを作成します。

1. **モデル** フォルダーを右クリックし、追加 を選択します。 **クラス...** コンテキストメニューから。

    ![Web アプリケーションへの新しいモデルの追加](build-restful-apis-with-aspnet-web-api/_static/image10.png "Web アプリケーションへの新しいモデルの追加")

    *Web アプリケーションへの新しいモデルの追加*
2. **[新しい項目の追加]** ダイアログで、新しいファイルに**Contact.cs**という名前を指定し、[追加] をクリックし**ます。**

    ![新しい Contact クラスファイルを作成しています](build-restful-apis-with-aspnet-web-api/_static/image11.png "新しい Contact クラスファイルを作成しています")

    *新しい Contact クラスファイルを作成しています*
3. 次の強調表示されたコードを**Contact**クラスに追加します。

    (コードスニペット- *WEB API Ex01-Contact クラス*)

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample2.cs)]
4. **Contactcontroller**クラスで、 **Get**メソッドの [メソッド定義内の**文字列**] を選択し、「 *Contact*」と入力します。 単語がに入力されると、" **Contact**" という単語の先頭にインジケーターが表示されます。 **Ctrl**キーを押したままピリオド (.) キーを押すか、マウスを使用してアイコンをクリックしてコードエディターの [アシスタンス] ダイアログを開き、モデルの名前空間の**using**ディレクティブを自動的に入力します。

    ![名前空間宣言における Intellisense アシスタントの使用](build-restful-apis-with-aspnet-web-api/_static/image12.png)

    *名前空間宣言における Intellisense アシスタントの使用*
5. Contact モデルのインスタンスの配列を返すように、 **Get**メソッドのコードを変更します。

    (コードスニペット- *WEB API Lab-Ex01-連絡先の一覧を返す*)

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample3.cs)]
6. **F5**キーを押して、ブラウザーで web アプリケーションをデバッグします。 API の応答出力に加えられた変更を表示するには、次の手順を実行します。

   1. ブラウザーが開いたら、開発者ツールがまだ開いていない場合は**F12**キーを押します。
   2. **[ネットワーク]** タブをクリックします。
   3. **[キャプチャの開始]** ボタンをクリックします。
   4. URL サフィックス **/api/contact**をアドレスバーの url に追加し、 **enter**キーを押します。
   5. **[詳細表示に進む]** ボタンをクリックします。
   6. **[応答本文]** タブを選択します。シリアル化されたフォームを表す JSON 文字列が、連絡先インスタンスの配列として表示されます。

      ![複雑な Web API メソッド呼び出しの JSON でシリアル化された出力](build-restful-apis-with-aspnet-web-api/_static/image13.png "複雑な Web API メソッド呼び出しの JSON でシリアル化された出力")

      *複雑な Web API メソッド呼び出しの JSON でシリアル化された出力*

<a id="Ex1Task4"></a>

<a id="Task_4_-_Extracting_Functionality_into_a_Service_Layer"></a>
#### <a name="task-4---extracting-functionality-into-a-service-layer"></a>タスク 4-サービスレイヤーへの機能の抽出

このタスクでは、サービス層に機能を抽出して、開発者がサービス機能をコントローラーレイヤーから簡単に分離できるようにする方法について説明します。これにより、実際に作業を行うサービスを再利用できます。

1. ソリューションルートに新しいフォルダーを作成し、「**サービス**」という名前を指定します。 これを行うには、[ **Contactmanager**プロジェクト] を右クリックし、[**追加** | **新しいフォルダー**] を選択して、「*サービス*」という名前を指定します。

    ![サービスフォルダーを作成しています](build-restful-apis-with-aspnet-web-api/_static/image14.png "サービスフォルダーを作成しています")

    *サービスフォルダーを作成しています*
2. **サービス** フォルダーを右クリックし、追加 を選択します。 **クラス...** コンテキストメニューから。

    ![サービスフォルダーへの新しいクラスの追加](build-restful-apis-with-aspnet-web-api/_static/image15.png "サービスフォルダーへの新しいクラスの追加")

    *サービスフォルダーへの新しいクラスの追加*
3. **[新しい項目の追加]** ダイアログが表示されたら、新しいクラスに**contactrepository**という名前を指定し、 **[追加]** をクリックします。

    ![Contact Repository サービスレイヤーのコードを格納するクラスファイルを作成する](build-restful-apis-with-aspnet-web-api/_static/image16.png "Contact Repository サービスレイヤーのコードを格納するクラスファイルを作成する")

    *Contact Repository サービスレイヤーのコードを格納するクラスファイルを作成する*
4. **ContactRepository.cs**ファイルに using ディレクティブを追加して、モデルの名前空間を含めます。

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample4.cs)]
5. 次の強調表示されたコードを**ContactRepository.cs**ファイルに追加して、GetAllContacts メソッドを実装します。

    (コードスニペット- *WEB API Lab-Ex01-Contact Repository*)

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample5.cs)]
6. **ContactController.cs**ファイルがまだ開いていない場合は開きます。
7. 次の using ステートメントをファイルの名前空間宣言セクションに追加します。

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample6.cs)]
8. 次の強調表示されたコードを**ContactController.cs**クラスに追加して、リポジトリのインスタンスを表すプライベートフィールドを追加します。これにより、他のクラスメンバーがサービス実装を利用できるようになります。

    (コードスニペット- *WEB API Lab-Ex01-Contact Controller*)

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample7.cs)]
9. Contact repository サービスを利用できるように**Get**メソッドを変更します。

    (コードスニペット- *WEB API Lab-Ex01-リポジトリを介して連絡先の一覧を返す*)

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample8.cs)]
10. **Contactcontroller**の**Get**メソッドの定義にブレークポイントを設定します。

   ![連絡先コントローラーへのブレークポイントの追加](build-restful-apis-with-aspnet-web-api/_static/image17.png "連絡先コントローラーへのブレークポイントの追加")

   *連絡先コントローラーへのブレークポイントの追加*
11. **F5** キーを押してアプリケーションを実行します。
12. ブラウザーが開いたら、 **F12**キーを押して開発者ツールを開きます。
13. **[ネットワーク]** タブをクリックします。
14. **[キャプチャの開始]** ボタンをクリックします。
15. アドレスバーにサフィックス **/api/contact**を入力して URL を追加し、 **enter**キーを押して api コントローラーを読み込みます。
16. **Get**メソッドの実行が開始されると、Visual Studio 2012 は中断されます。

   ![Get メソッド内での中断](build-restful-apis-with-aspnet-web-api/_static/image18.png "Get メソッド内での中断")

   *Get メソッド内での中断*
17. **F5** キーを押して続行します。
18. まだフォーカスされていない場合は、Internet Explorer に戻ります。 [ネットワークキャプチャ] ウィンドウに注意してください。

    ![Web API 呼び出しの結果を表示する Internet Explorer のネットワークビュー](build-restful-apis-with-aspnet-web-api/_static/image19.png "Web API 呼び出しの結果を表示する Internet Explorer のネットワークビュー")

    *Web API 呼び出しの結果を表示する Internet Explorer のネットワークビュー*
19. **[詳細表示に進む]** ボタンをクリックします。
20. **[応答本文]** タブをクリックします。 API 呼び出しの JSON 出力と、サービスレイヤーによって取得された2つの連絡先を表す方法に注意してください。

    ![開発者ツールウィンドウで Web API からの JSON 出力を表示する](build-restful-apis-with-aspnet-web-api/_static/image20.png "開発者ツールウィンドウで Web API からの JSON 出力を表示する")

    *開発者ツールウィンドウで Web API からの JSON 出力を表示する*

<a id="Exercise2"></a>

<a id="Exercise_2_Create_a_ReadWrite_Web_API"></a>
### <a name="exercise-2-create-a-readwrite-web-api"></a>演習 2: 読み取り/書き込み Web API を作成する

この演習では、連絡先マネージャーがデータ編集機能を有効にするための POST メソッドと PUT メソッドを実装します。

<a id="Ex2Task1"></a>

<a id="Task_1_-_Opening_the_Web_API_Project"></a>
#### <a name="task-1---opening-the-web-api-project"></a>タスク 1-Web API プロジェクトを開く

このタスクでは、ユーザー入力を受け入れることができるように、演習1で作成した Web API プロジェクトを拡張する準備をします。

1. **Visual Studio 2012 Express For Web**を実行し**ます。これ**を行うには、 **[スタート]** に移り、 **VS Express for Web**入力して、enter キーを押します。
2. **Source/Ex02-ReadWriteWebAPI/begin/** folder にある**begin**ソリューションを開きます。 それ以外の場合は、前の演習を完了することによって得られた**終了**ソリューションを引き続き使用することができます。

   1. 提供された**Begin**ソリューションを開いた場合は、続行する前に、不足している NuGet パッケージをダウンロードする必要があります。 これを行うには、 **[プロジェクト]** メニューをクリックし、 **[NuGet パッケージの管理]** を選択します。
   2. **[NuGet パッケージの管理]** ダイアログで、 **[復元]** をクリックして、不足しているパッケージをダウンロードします。
   3. 最後に、[**ビルド** | **ビルド**] をクリックしてソリューションをビルドします。

      > [!NOTE]
      > NuGet を使用する利点の1つは、プロジェクトのすべてのライブラリを配布する必要がなく、プロジェクトのサイズを小さくすることです。 NuGet パワーツールを使用すると、パッケージのバージョンを app.config ファイルで指定することで、プロジェクトを初めて実行するときに必要なすべてのライブラリをダウンロードできます。 このため、このラボから既存のソリューションを開いた後に、これらの手順を実行する必要があります。
3. **Services/ContactRepository .cs**ファイルを開きます。

<a id="Ex2Task2"></a>

<a id="Task_2_-_Adding_Data-Persistence_Features_to_the_Contact_Repository_Implementation"></a>
#### <a name="task-2---adding-data-persistence-features-to-the-contact-repository-implementation"></a>タスク 2-連絡先リポジトリの実装にデータの永続性機能を追加する

このタスクでは、演習1で作成した Web API プロジェクトの ContactRepository クラスを拡張して、ユーザー入力と新しい連絡先インスタンスを永続化して受け入れることができるようにします。

1. 次の定数を**Contactrepository**クラスに追加して、この演習の後半で web サーバーキャッシュ項目のキー名を表します。

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample9.cs)]
2. 次のコードを含む**Contactrepository**にコンストラクターを追加します。

    (コードスニペット- *WEB API Lab-Ex02-Contact Repository Constructor*)

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample10.cs)]
3. 次に示すように、 **GetAllContacts**メソッドのコードを変更します。

    (コードスニペット- *WEB API Lab-Ex02-すべての連絡先を取得*します)

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample11.cs)]

    > [!NOTE]
    > この例はデモンストレーションを目的としており、web サーバーのキャッシュをストレージメディアとして使用します。これにより、セッションストレージメカニズムや要求ストレージの有効期間を使用するのではなく、複数のクライアントで同時に値を使用できるようになります。 Web サーバーキャッシュの代わりに、Entity Framework、XML ストレージ、またはその他のさまざまなものを使用できます。
4. 連絡先を保存する作業を行うために、 **Contactrepository**クラスに**SaveContact**という名前の新しいメソッドを実装します。 **SaveContact**メソッドは、単一の**Contact**パラメーターを受け取り、成功または失敗を示すブール値を返す必要があります。

    (コードスニペット- *WEB API Ex02-SaveContact メソッドの実装*)

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample12.cs)]

<a id="Exercise3"></a>

<a id="Exercise_3_Consume_the_Web_API_from_an_HTML_Client"></a>
### <a name="exercise-3-consume-the-web-api-from-an-html-client"></a>演習 3: HTML クライアントから Web API を使用する

この演習では、Web API を呼び出す HTML クライアントを作成します。 このクライアントは、JavaScript を使用する Web API とのデータ交換を容易にし、HTML マークアップを使用して結果を web ブラウザーに表示します。

<a id="Ex3Task1"></a>

<a id="Task_1_-_Modifying_the_Index_View_to_Provide_a_GUI_for_Displaying_Contacts"></a>
#### <a name="task-1---modifying-the-index-view-to-provide-a-gui-for-displaying-contacts"></a>タスク 1-インデックスビューを変更して、連絡先を表示する GUI を提供する

このタスクでは、web アプリケーションの既定のインデックスビューを変更して、既存の連絡先の一覧を HTML ブラウザーに表示するための要件をサポートします。

1. **Visual Studio 2012 Express For Web**がまだ開いていない場合は開きます。
2. **Source/Ex03-ConsumingWebAPI/begin/** folder にある**begin**ソリューションを開きます。 それ以外の場合は、前の演習を完了することによって得られた**終了**ソリューションを引き続き使用することができます。

   1. 提供された**Begin**ソリューションを開いた場合は、続行する前に、不足している NuGet パッケージをダウンロードする必要があります。 これを行うには、 **[プロジェクト]** メニューをクリックし、 **[NuGet パッケージの管理]** を選択します。
   2. **[NuGet パッケージの管理]** ダイアログで、 **[復元]** をクリックして、不足しているパッケージをダウンロードします。
   3. 最後に、[**ビルド** | **ビルド**] をクリックしてソリューションをビルドします。

      > [!NOTE]
      > NuGet を使用する利点の1つは、プロジェクトのすべてのライブラリを配布する必要がなく、プロジェクトのサイズを小さくすることです。 NuGet パワーツールを使用すると、パッケージのバージョンを app.config ファイルで指定することで、プロジェクトを初めて実行するときに必要なすべてのライブラリをダウンロードできます。 このため、このラボから既存のソリューションを開いた後に、これらの手順を実行する必要があります。
3. **Views/Home**フォルダーにある**インデックスの cshtml**ファイルを開きます。
4. Div 要素内の HTML コードを id**本文**に置き換えて、次のコードのようにします。

    [!code-html[Main](build-restful-apis-with-aspnet-web-api/samples/sample13.html)]
5. ファイルの末尾に次の Javascript コードを追加して、Web API への HTTP 要求を実行します。

    [!code-cshtml[Main](build-restful-apis-with-aspnet-web-api/samples/sample14.cshtml)]
6. **ContactController.cs**ファイルがまだ開いていない場合は開きます。
7. **Contactcontroller**クラスの**Get**メソッドにブレークポイントを設定します。

    ![API コントローラーの Get メソッドにブレークポイントを配置する](build-restful-apis-with-aspnet-web-api/_static/image21.png "API コントローラーの Get メソッドにブレークポイントを配置する")

    *API コントローラーの Get メソッドにブレークポイントを配置する*
8. **F5** キーを押してプロジェクトを実行します。 ブラウザーは HTML ドキュメントを読み込みます。

    > [!NOTE]
    > アプリケーションのルート URL を参照していることを確認します。
9. ページが読み込まれ、JavaScript が実行されると、ブレークポイントにヒットし、コントローラーでコードの実行が一時停止されます。

    ![VS Express for Web を使用した Web API 呼び出しへのデバッグ](build-restful-apis-with-aspnet-web-api/_static/image22.png "VS Express for Web を使用した Web API 呼び出しへのデバッグ")

    *Visual Studio 2012 Express for Web を使用した Web API 呼び出しへのデバッグ*
10. ブレークポイントを削除し、 **F5**キーまたはデバッグツールバーの **[続行]** ボタンを押して、ブラウザーでのビューの読み込みを続行します。 Web API の呼び出しが完了すると、ブラウザーにリスト項目として表示された Web API 呼び出しから返された連絡先が表示されます。

    ![ブラウザーにリスト項目として表示される API 呼び出しの結果](build-restful-apis-with-aspnet-web-api/_static/image23.png "ブラウザーにリスト項目として表示される API 呼び出しの結果")

    *ブラウザーにリスト項目として表示される API 呼び出しの結果*
11. デバッグを停止します。

<a id="Ex3Task2"></a>

<a id="Task_2_-_Modifying_the_Index_View_to_Provide_a_GUI_for_Creating_Contacts"></a>
#### <a name="task-2---modifying-the-index-view-to-provide-a-gui-for-creating-contacts"></a>タスク 2-インデックスビューを変更して、連絡先を作成するための GUI を提供する

このタスクでは、MVC アプリケーションのインデックスビューの変更を続行します。 ユーザー入力をキャプチャし、Web API に送信して新しい連絡先を作成するフォームが HTML ページに追加され、GUI から日付を収集するための新しい Web API コントローラーメソッドが作成されます。

1. **ContactController.cs**ファイルを開きます。
2. 次のコードに示すように、 **Post**という名前のコントローラークラスに新しいメソッドを追加します。

    (コードスニペット- *WEB API Ex03-Post メソッド*)

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample15.cs)]
3. まだ開いていない場合は、Visual Studio で**インデックスの cshtml**ファイルを開きます。
4. 前のタスクで追加した順序付けられていないリストの直後に、次の HTML コードをファイルに追加します。

    [!code-html[Main](build-restful-apis-with-aspnet-web-api/samples/sample16.html)]
5. ドキュメントの下部にある script 要素内に、ボタンクリックイベントを処理する次の強調表示されたコードを追加します。これにより、HTTP POST 呼び出しを使用して Web API にデータがポストされます。

    [!code-html[Main](build-restful-apis-with-aspnet-web-api/samples/sample17.html)]
6. **ContactController.cs**で、 **Post**メソッドにブレークポイントを設定します。
7. **F5**キーを押して、ブラウザーでアプリケーションを実行します。
8. ブラウザーにページが読み込まれたら、新しい連絡先の名前と Id を入力し、 **[保存]** ボタンをクリックします。

    ![ブラウザーに読み込まれたクライアントの HTML ドキュメント](build-restful-apis-with-aspnet-web-api/_static/image24.png "ブラウザーに読み込まれたクライアントの HTML ドキュメント")

    *ブラウザーに読み込まれたクライアントの HTML ドキュメント*
9. **Post**メソッドでデバッガーウィンドウが中断した場合は、 **contact**パラメーターのプロパティを参照してください。 値は、フォームに入力したデータと一致している必要があります。

    ![クライアントから Web API に送信される Contact オブジェクト](build-restful-apis-with-aspnet-web-api/_static/image25.png "クライアントから Web API に送信される Contact オブジェクト")

    *クライアントから Web API に送信される Contact オブジェクト*
10. **応答**変数が作成されるまで、デバッガーでメソッドをステップ実行します。 デバッガーの **[ローカル]** ウィンドウで検査すると、すべてのプロパティが設定されていることがわかります。

   ![デバッガーでの作成後の応答](build-restful-apis-with-aspnet-web-api/_static/image26.png "デバッガーでの作成後の応答")

   *デバッガーでの作成後の応答*
11. **F5**キーを押すか、デバッガーで **[続行]** をクリックすると、要求が完了します。 ブラウザーに戻ると、 **Contactrepository**実装によって格納されている連絡先の一覧に新しい連絡先が追加されます。

   ![ブラウザーに新しい連絡先インスタンスが正常に作成されたことが反映されます。](build-restful-apis-with-aspnet-web-api/_static/image27.png "ブラウザーに新しい連絡先インスタンスが正常に作成されたことが反映されます。")

   *ブラウザーに新しい連絡先インスタンスが正常に作成されたことが反映されます。*

> [!NOTE]
> また、 [「付録 C: Web 配置を使用した ASP.NET MVC 4 アプリケーションの発行](#AppendixC)」に従って、このアプリケーションを Azure にデプロイすることもできます。

---

<a id="Summary"></a>
## <a name="summary"></a>まとめ

このラボでは、新しい ASP.NET Web API framework と、フレームワークを使用した RESTful Web Api の実装について紹介しました。 ここから、このラボの例として提供されている単純なメカニズムではなく、任意の数のメカニズムを使用してデータの永続化を容易にする新しいリポジトリを作成できます。 Web API は、HTTP、JSON、または XML をサポートする任意の言語で記述された HTML 以外のクライアントからの通信を可能にするなど、多くの追加機能をサポートしています。 一般的な web アプリケーションの外部で Web API をホストする機能も可能であり、独自のシリアル化形式を作成することもできます。

ASP.NET Web サイトには、 [[https://asp.net/web-api](https://asp.net/web-api)](https://asp.net/web-api)の ASP.NET Web API フレームワーク専用の領域があります。 このサイトでは、Web API に関する最新の情報、サンプル、ニュースが引き続き提供されます。そのため、事実上あらゆるデバイスまたは開発フレームワークで使用できるカスタム Web Api の作成について詳しく掘り下げたい場合は、頻繁に確認してください。

<a id="AppendixA"></a>

<a id="Appendix_A_Using_Code_Snippets"></a>
## <a name="appendix-a-using-code-snippets"></a>付録 A: コードスニペットの使用

コードスニペットを使用すると、必要なすべてのコードをすぐに利用できます。 次の図に示すように、ラボドキュメントには、使用できるタイミングがわかります。

![Visual Studio のコードスニペットを使用してプロジェクトにコードを挿入する](build-restful-apis-with-aspnet-web-api/_static/image28.png "Visual Studio のコードスニペットを使用してプロジェクトにコードを挿入する")

*Visual Studio のコードスニペットを使用してプロジェクトにコードを挿入する*

<a id="CodeSnippetUsingKeyBoard"></a>

<a id="To_add_a_code_snippet_using_the_keyboard_C_only"></a>
### <a name="to-add-a-code-snippet-using-the-keyboard-c-only"></a>キーボードを使用してコードスニペットを追加C#するには (のみ)

1. コードを挿入する場所にカーソルを置きます。
2. (スペースまたはハイフンを含まない) スニペット名の入力を開始します。
3. IntelliSense によって、一致するスニペットの名前が表示されます。
4. 正しいスニペットを選択します (または、スニペットの名前全体が選択されるまで入力し続けます)。
5. Tab キーを2回押すと、スニペットがカーソル位置に挿入されます。

    ![スニペット名の入力を開始します](build-restful-apis-with-aspnet-web-api/_static/image29.png "スニペット名の入力を開始します")

    *スニペット名の入力を開始します*

    ![Tab キーを押して、強調表示されているスニペットを選択します](build-restful-apis-with-aspnet-web-api/_static/image30.png "Tab キーを押して、強調表示されているスニペットを選択します")

    *Tab キーを押して、強調表示されているスニペットを選択します*

    ![もう一度 Tab キーを押すと、スニペットが展開されます。](build-restful-apis-with-aspnet-web-api/_static/image31.png "もう一度 Tab キーを押すと、スニペットが展開されます。")

    *もう一度 Tab キーを押すと、スニペットが展開されます。*

<a id="CodeSnippetUsingMouse"></a>

<a id="To_add_a_code_snippet_using_the_mouse_C_Visual_Basic_and_XML"></a>
### <a name="to-add-a-code-snippet-using-the-mouse-c-visual-basic-and-xml"></a>マウス (C#、VISUAL BASIC および XML) を使用してコードスニペットを追加するには

1. コードスニペットを挿入する場所を右クリックします。
2. **[スニペットの挿入]** 、 **[マイコードスニペット**] の順に選択します。
3. 一覧から該当するスニペットをクリックして選択します。

    ![コードスニペットを挿入する場所を右クリックし、[スニペットの挿入] を選択します。](build-restful-apis-with-aspnet-web-api/_static/image32.png "コードスニペットを挿入する場所を右クリックし、[スニペットの挿入] を選択します。")

    *コードスニペットを挿入する場所を右クリックし、[スニペットの挿入] を選択します。*

    ![一覧から関連するスニペットをクリックして選択します。](build-restful-apis-with-aspnet-web-api/_static/image33.png "一覧から関連するスニペットをクリックして選択します。")

    *一覧から関連するスニペットをクリックして選択します。*

<a id="AppendixB"></a>

<a id="Appendix_B_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-b-installing-visual-studio-express-2012-for-web"></a>付録 B: Visual Studio Express 2012 を Web 用にインストールする

**[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)** を使用して、Web または別の &quot;Express&quot; バージョン**用に Microsoft Visual Studio Express 2012**をインストールできます。 次の手順では、 *Microsoft Web Platform Installer*を使用して*Visual studio Express 2012 for Web*をインストールするために必要な手順について説明します。

1. [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)にアクセスします。 または、Web Platform Installer が既にインストールされている場合は、それを開いて、 <em>AZURE SDK&quot;で web 用に 2012 Visual Studio Express を</em>検索 &quot;ことができます。
2. **[今すぐインストール]** をクリックします。 **Web Platform Installer**がない場合は、最初にダウンロードしてインストールするようにリダイレクトされます。
3. **Web Platform Installer**が開いたら、 **[インストール]** をクリックしてセットアップを開始します。

    ![Visual Studio Express のインストール](build-restful-apis-with-aspnet-web-api/_static/image34.png "Visual Studio Express のインストール")

    *Visual Studio Express のインストール*
4. すべての製品のライセンスと条項を読み、[**同意**する] をクリックして続行します。

    ![ライセンス条項に同意する](build-restful-apis-with-aspnet-web-api/_static/image35.png)

    *ライセンス条項に同意する*
5. ダウンロードとインストールのプロセスが完了するまで待ちます。

    ![Installation progress](build-restful-apis-with-aspnet-web-api/_static/image36.png)

    *インストールの進行状況*
6. インストールが完了したら、 **[完了]** をクリックします。

    ![インストールの完了](build-restful-apis-with-aspnet-web-api/_static/image37.png)

    *インストールの完了*
7. **[終了]** をクリックして Web Platform Installer を閉じます。
8. Web 用の Visual Studio Express を開くには、**スタート**画面にアクセスして &quot;**VS Express**&quot;の書き込みを開始し、 **[VS Express for Web]** タイルをクリックします。

    ![VS Express for Web タイル](build-restful-apis-with-aspnet-web-api/_static/image38.png)

    *VS Express for Web タイル*

<a id="AppendixC"></a>

<a id="Appendix_C_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-c-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>付録 C: Web 配置を使用した ASP.NET MVC 4 アプリケーションの発行

この付録では、azure によって提供される Web 配置公開機能を活用して、Azure Portal から新しい web サイトを作成し、取得したアプリケーションを発行する方法について説明します。

<a id="ApxCTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-azure-portal"></a>タスク 1-Azure Portal から新しい Web サイトを作成する

1. [Azure 管理ポータル](https://manage.windowsazure.com/)にアクセスし、サブスクリプションに関連付けられている Microsoft 資格情報を使用してサインインします。

    > [!NOTE]
    > Azure では、10 ASP.NET の Web サイトを無料でホストし、トラフィックの増加に合わせて拡張できます。 [ここで](https://aka.ms/aspnet-hol-azure)サインアップできます。

    ![Windows Azure portal にログオンします。](build-restful-apis-with-aspnet-web-api/_static/image39.png "Windows Azure portal にログオンします。")

    *ポータルにログオンする*
2. コマンドバーの **[新規]** をクリックします。

    ![新しい Web サイトの作成](build-restful-apis-with-aspnet-web-api/_static/image40.png "新しい Web サイトの作成")

    *新しい Web サイトの作成*
3. [ **Compute** | **Web サイト**] をクリックします。 次に、 **[簡易作成]** オプションを選択します。 新しい web サイトの使用可能な URL を指定し、 **[Web サイトの作成]** をクリックします。

    > [!NOTE]
    > Azure は、管理および管理が可能なクラウドで実行されている web アプリケーションのホストです。 [簡易作成] オプションを使用すると、完成した web アプリケーションをポータルの外部から Azure にデプロイできます。 データベースを設定する手順は含まれていません。

    ![簡易作成を使用した新しい Web サイトの作成](build-restful-apis-with-aspnet-web-api/_static/image41.png "簡易作成を使用した新しい Web サイトの作成")

    *簡易作成を使用した新しい Web サイトの作成*
4. 新しい**Web サイト**が作成されるまで待ちます。
5. Web サイトが作成されたら、 **[URL]** 列の下のリンクをクリックします。 新しい Web サイトが機能していることを確認します。

    ![新しい web サイトを参照しています](build-restful-apis-with-aspnet-web-api/_static/image42.png "新しい web サイトを参照しています")

    *新しい web サイトを参照しています*

    ![実行中の Web サイト](build-restful-apis-with-aspnet-web-api/_static/image43.png "実行中の Web サイト")

    *実行中の Web サイト*
6. ポータルに戻り、 **[名前]** 列の下にある web サイトの名前をクリックして、管理ページを表示します。

    ![Web サイトの管理ページを開く](build-restful-apis-with-aspnet-web-api/_static/image44.png "Web サイトの管理ページを開く")

    *Web サイトの管理ページを開く*
7. **[ダッシュボード]** ページの **[概要] セクションで**、 **[発行プロファイルのダウンロード]** リンクをクリックします。

    > [!NOTE]
    > *発行プロファイル*には、有効になっている各発行方法について、Azure に web アプリケーションを発行するために必要なすべての情報が含まれています。 発行プロファイルには、発行メソッドが有効化される各エンドポイントに接続して認証するために必要な URL、ユーザーの資格情報、およびデータベース文字列が含まれています。 **Microsoft WebMatrix 2**、 **Microsoft Visual Studio Express for Web**および**Microsoft Visual Studio 2012**では、発行プロファイルを読み取り、Web アプリケーションを Azure に発行するためのこれらのプログラムの構成を自動化することがサポートされています。

    ![Web サイト発行プロファイルをダウンロードしています](build-restful-apis-with-aspnet-web-api/_static/image45.png "Web サイト発行プロファイルをダウンロードしています")

    *Web サイト発行プロファイルをダウンロードしています*
8. 発行プロファイルファイルを既知の場所にダウンロードします。 この演習では、このファイルを使用して Visual Studio から Azure に web アプリケーションを発行する方法について説明します。

    ![発行プロファイルファイルを保存しています](build-restful-apis-with-aspnet-web-api/_static/image46.png "発行プロファイルを保存しています")

    *発行プロファイルファイルを保存しています*

<a id="ApxCTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a>タスク 2-データベースサーバーの構成

アプリケーションで SQL Server データベースを使用する場合は、SQL Database サーバーを作成する必要があります。 SQL Server を使用しない単純なアプリケーションを展開する場合は、このタスクを省略できます。

1. アプリケーションデータベースを格納するには、SQL Database サーバーが必要です。 Azure 管理ポータルのサブスクリプションから**SQL Database サーバーを**表示するには、 **SQL データベース** | サーバー | **サーバーのダッシュボード**を参照してください。 サーバーを作成していない場合は、コマンドバーの **[追加]** ボタンを使用して作成できます。 次のタスクで使用するので、**サーバー名と URL、管理者のログイン名、パスワード**をメモしておきます。 データベースは、後の段階で作成されるため、まだ作成しないでください。

    ![SQL Database サーバーダッシュボード](build-restful-apis-with-aspnet-web-api/_static/image47.png "SQL Database サーバーダッシュボード")

    *SQL Database サーバーダッシュボード*
2. 次のタスクでは、Visual Studio からデータベース接続をテストします。そのため、**使用可能な Ip アドレス**の一覧にローカル ip アドレスを含める必要があります。 これを行うには、 **[構成]** をクリックし、 **[現在のクライアント IP アドレス]** の ip アドレスを選択して、 **[開始 Ip アドレス]** と **[終了 ip アドレス]** のテキストボックスに貼り付け、[![の](build-restful-apis-with-aspnet-web-api/_static/image48.png) 追加] をクリックします。

    ![クライアント IP アドレスを追加しています](build-restful-apis-with-aspnet-web-api/_static/image49.png)

    *クライアント IP アドレスを追加しています*
3. [許可された IP アドレス] の一覧に**クライアントの Ip アドレス**が追加されたら、 **[保存]** をクリックして変更を確認します。

    ![変更の確認](build-restful-apis-with-aspnet-web-api/_static/image50.png)

    *変更の確認*

<a id="ApxCTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>タスク 3-Web 配置を使用した ASP.NET MVC 4 アプリケーションの発行

1. ASP.NET MVC 4 ソリューションに戻ります。 **ソリューションエクスプローラー**で、web サイトプロジェクトを右クリックし、 **[発行]** を選択します。

    ![アプリケーションの発行](build-restful-apis-with-aspnet-web-api/_static/image51.png "アプリケーションの発行")

    *Web サイトの公開*
2. 最初のタスクで保存した発行プロファイルをインポートします。

    ![発行プロファイルをインポートしています](build-restful-apis-with-aspnet-web-api/_static/image52.png "発行プロファイルをインポートしています")

    *発行プロファイルをインポートしています*
3. **[接続の検証]** をクリックします。 検証が完了したら、 **[次へ]** をクリックします。

    > [!NOTE]
    > 検証が完了すると、[接続の検証] ボタンの横に緑色のチェックマークが表示されます。

    ![接続の検証](build-restful-apis-with-aspnet-web-api/_static/image53.png "接続の検証")

    *接続の検証*
4. **[設定]** ページの **[データベース]** セクションで、データベース接続のテキストボックスの横にあるボタン ( **defaultconnection**など) をクリックします。

    ![Web deploy の構成](build-restful-apis-with-aspnet-web-api/_static/image54.png "Web deploy の構成")

    *Web deploy の構成*
5. 次のようにデータベース接続を構成します。

   - **サーバー名**には、 *tcp:* プレフィックスを使用して SQL Database サーバーの URL を入力します。
   - **User name (ユーザー名**) に、サーバー管理者のログイン名を入力します。
   - **パスワード**で、サーバー管理者のログインパスワードを入力します。
   - 新しいデータベース名を入力します (例: *MVC4SampleDB*)。

     ![変換先の接続文字列を構成しています](build-restful-apis-with-aspnet-web-api/_static/image55.png "変換先の接続文字列を構成しています")

     *変換先の接続文字列を構成しています*
6. 次に、 **[OK]** をクリックします データベースの作成を求めるメッセージが表示されたら、[**はい]** をクリックします。

    ![データベースの作成](build-restful-apis-with-aspnet-web-api/_static/image56.png "データベース文字列の作成")

    *データベースの作成*
7. Windows Azure の SQL Database に接続するために使用する接続文字列は、[既定の接続] ボックスに表示されます。 続けて、 **[次へ]** をクリックします。

    ![SQL Database を指す接続文字列](build-restful-apis-with-aspnet-web-api/_static/image57.png "SQL Database を指す接続文字列")

    *SQL Database を指す接続文字列*
8. **[プレビュー]** ページで、 **[発行]** をクリックします。

    ![Web アプリケーションの発行](build-restful-apis-with-aspnet-web-api/_static/image58.png "Web アプリケーションの発行")

    *Web アプリケーションの発行*
9. 発行プロセスが完了すると、既定のブラウザーによって公開された web サイトが開きます。

    ![Windows Azure に発行されたアプリケーション](build-restful-apis-with-aspnet-web-api/_static/image59.png "Windows Azure に発行されたアプリケーション")

    *Azure に発行されたアプリケーション*
