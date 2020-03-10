---
uid: web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs
title: 'ハンズオンラボ: ASP.NET Web API と ASP.NET 4.x を使用して単一ページアプリケーション (SPA) を構築する'
author: rick-anderson
description: 'ステップバイステップコード: ASP.NET 4.x 用の ASP.NET Web API とを使用して単一ページアプリケーション (SPA) をビルドします。'
ms.author: riande
ms.date: 09/30/2015
ms.custom: seoapril2019
ms.assetid: 719727b7-bef3-45ad-bfe9-ba5bcdb2305f
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs
msc.type: authoredcontent
ms.openlocfilehash: 86833a890da759e489dd11dc9afb128a9b7a75e3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448762"
---
# <a name="hands-on-lab-build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs"></a>ハンズオンラボ: ASP.NET Web API と角速度を使用してシングルページアプリケーション (SPA) を構築する

[Web キャンプチーム](https://twitter.com/webcamps)別

[Web キャンプトレーニングキットをダウンロードする](https://aka.ms/webcamps-training-kit)

このハンズオンラボでは、ASP.NET 4.x 用の ASP.NET Web API とを使用してシングルページアプリケーション (SPA) を構築する方法を示します。

このラボでは、これらのテクノロジを利用して、SPA の概念に基づくトリビア web サイトであるマニアクイズを実装します。 まず、ASP.NET Web API を使用してサービス層を実装し、クイズの質問を取得して回答を格納するために必要なエンドポイントを公開します。 次に、AngularJS および CSS3 変換効果を使用して、優れた応答性の高い UI を構築します。

従来の web アプリケーションでは、クライアント (ブラウザー) がページを要求することによってサーバーとの通信を開始します。 次に、サーバーが要求を処理し、ページの HTML をクライアントに送信します。 このページとの後続の操作 (ユーザーがリンクに移動したり、データでフォームを送信したりする場合など) では、新しい要求がサーバーに送信され、フローが再び開始されます。サーバーが要求を処理し、新しいページを新しいアクション要求への応答としてブラウザーに送信します。クライアントによる ed。
> 
> シングルページアプリケーション (spa) では、最初の要求の後にページ全体がブラウザーに読み込まれますが、それ以降の対話は Ajax 要求によって行われます。 これは、ブラウザーが変更されたページの部分のみを更新する必要があることを意味します。ページ全体を再読み込みする必要はありません。 SPA アプローチを使用すると、アプリケーションがユーザーの操作に応答するためにかかる時間が短縮され、より滑らかなエクスペリエンスが得られます。
> 
> SPA のアーキテクチャには、従来の web アプリケーションには存在しない特定の課題が伴います。 ただし、ASP.NET Web API などの新しいテクノロジや、CSS3 によって提供される新しいスタイル機能などの JavaScript フレームワークにより、SPAs の設計とビルドが非常に簡単になります。
> 
> 
> すべてのサンプルコードとスニペットは、 [https://aka.ms/webcamps-training-kit](https://aka.ms/webcamps-training-kit)で入手できる Web キャンプトレーニングキットに含まれています。

## <a name="overview"></a>概要

<a id="Objectives"></a>
### <a name="objectives"></a>目標

このハンズオンラボでは、次の方法を学習します。

- JSON データを送受信するための ASP.NET Web API サービスを作成する
- AngularJS を使用して応答性の高い UI を作成する
- CSS3 変換による UI エクスペリエンスの向上

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>前提条件

このハンズオンラボを完了するには、次のものが必要です。

- [Web 用に2013を Visual Studio Express](https://www.microsoft.com/visualstudio/)

<a id="Setup"></a>
### <a name="setup"></a>セットアップ

このハンズオンラボの演習を実行するには、まず環境をセットアップする必要があります。

1. エクスプローラーを開き、ラボの**ソース**フォルダーを参照します。
2. **Setup.exe**を右クリックし、 **[管理者として実行]** を選択して、環境を構成し、このラボ用の Visual Studio コードスニペットをインストールするセットアッププロセスを開始します。
3. ユーザー アカウント制御ダイアログ ボックスが表示されている場合は、続行するアクションを確認します。

> [!NOTE]
> セットアップを実行する前に、このラボのすべての依存関係を確認していることを確認してください。

<a id="CodeSnippets"></a>
### <a name="using-the-code-snippets"></a>コードスニペットの使用

ラボドキュメント全体で、コードブロックを挿入するように指示されます。 便宜上、このコードのほとんどは Visual Studio Code のスニペットとして提供されており、Visual Studio 2013 内からアクセスして、手動で追加する必要がないようにすることができます。

> [!NOTE]
> 各演習には、演習の**Begin**フォルダーに配置された開始ソリューションが付属しています。これにより、各演習を別の手順に従って実行することができます。 演習中に追加されたコードスニペットは、これらの開始ソリューションにはないため、演習を完了するまで機能しないことがあります。 演習用のソースコード内では、対応する演習の手順を完了した結果として得られるコードを使用して、Visual Studio ソリューションを含む**終了**フォルダーも検索します。 このハンズオンラボを使用して作業する際に、追加のヘルプが必要な場合は、これらのソリューションをガイダンスとして使用できます。

---

<a id="Exercises"></a>
## <a name="exercises"></a>手順

このハンズオンラボには、次の演習が含まれています。

1. [Web API の作成](#Exercise1)
2. [SPA インターフェイスの作成](#Exercise2)

このラボの推定所要時間: **60 分**

> [!NOTE]
> Visual Studio を初めて起動するときに、定義済みの設定コレクションのいずれかを選択する必要があります。 定義済みの各コレクションは、特定の開発スタイルに一致するように設計されており、ウィンドウのレイアウト、エディターの動作、IntelliSense コードスニペット、およびダイアログボックスのオプションを決定します。 このラボの手順では、**全般的な開発設定**のコレクションを使用するときに、Visual Studio で特定のタスクを実行するために必要なアクションについて説明します。 開発環境に対して別の設定コレクションを選択した場合は、注意が必要な手順が異なる場合があります。

<a id="Exercise1"></a>
### <a name="exercise-1-creating-a-web-api"></a>演習 1: Web API の作成

SPA の重要な部分の1つは、サービス層です。 これは、UI によって送信された Ajax 呼び出しを処理し、その呼び出しに応答してデータを返す役割を担います。 取得したデータは、クライアントによって解析および使用されるために、コンピューターが判読できる形式で表示される必要があります。

Web API フレームワークは ASP.NET スタックの一部であり、HTTP サービスを簡単に実装できるように設計されています。これは、一般に、RESTful API を使用して JSON または XML 形式のデータを送受信します。 この演習では、マニアクイズアプリケーションをホストする Web サイトを作成し、ASP.NET Web API を使用して、クイズデータを公開して永続化するバックエンドサービスを実装します。

<a id="Ex1Task1"></a>
#### <a name="task-1--creating-the-initial-project-for-geek-quiz"></a>タスク 1-マニアクイズの初期プロジェクトを作成する

このタスクでは、Visual Studio に付属する**ASP.NET**プロジェクトの種類に基づいて ASP.NET Web API をサポートする新しい ASP.NET MVC プロジェクトの作成を開始します。 **ASP.NET**は、すべての ASP.NET テクノロジを統合し、必要に応じてそれらを組み合わせて照合するオプションを提供します。 次に、Entity Framework のモデルクラスとデータベース初期化子を追加して、クイズの質問を挿入します。

1. **Web 用 Visual Studio Express 2013**を開き、[ファイル] を選択します。 **新しいプロジェクト...** を実行すると、新しいソリューションが開始されます。

    ![新しいプロジェクトの作成](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image1.png "新規プロジェクトの作成")

    *新しいプロジェクトの作成*
2. **[新しいプロジェクト]** ダイアログボックスで、Visual  **C# | の下にある [ASP.NET Web Application] を選択します。[Web** ] タブ。 **.NET Framework 4.5**が選択されていることを確認し、 *GeekQuiz*という名前を設定して、**場所**を選択し、 **[OK]** をクリックします。

    ![新しい ASP.NET Web アプリケーションプロジェクトの作成](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image2.png "新しい ASP.NET Web アプリケーションプロジェクトの作成")

    *新しい ASP.NET Web アプリケーションプロジェクトの作成*
3. **[New ASP.NET プロジェクト]** ダイアログボックスで、 **[MVC]** テンプレートを選択し、 **[Web API]** オプションを選択します。 また、**認証**オプションが**個々のユーザーアカウント**に設定されていることを確認します。 続行するには、 **[OK]** をクリックします。

    ![MVC テンプレートを使用した新しいプロジェクトの作成 (Web API コンポーネントを含む)](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image3.png)

    *MVC テンプレートを使用した新しいプロジェクトの作成 (Web API コンポーネントを含む)*
4. **ソリューションエクスプローラー**で、 **GeekQuiz**プロジェクトの **モデル** フォルダーを右クリックし、追加 を選択します。 **既存の項目...** .

    ![既存の項目の追加](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image4.png "既存の項目の追加")

    *既存の項目の追加*
5. **[既存項目の追加]** ダイアログボックスで、 **[ソース/アセット/モデル]** フォルダーに移動し、すべてのファイルを選択します。 **[追加]** をクリックします。

    ![モデルアセットの追加](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image5.png "モデルアセットの追加")

    *モデルアセットの追加*

    > [!NOTE]
    > これらのファイルを追加することで、データモデル、Entity Framework のデータベースコンテキスト、マニアクイズアプリケーションのデータベース初期化子を追加します。
    > 
    > **Entity Framework (EF)** は、リレーショナルストレージスキーマを使用して直接プログラミングするのではなく、概念アプリケーションモデルを使用してプログラミングすることで、データアクセスアプリケーションを作成できる、オブジェクトリレーショナルマッパー (ORM) です。 Entity Framework の詳細については、[こちら](../../../entity-framework.md)を参照してください。
    > 
    > 追加したクラスの説明を次に示します。
    > 
    > - **TriviaOption:** クイズ質問に関連付けられた1つのオプションを表します。
    > - **TriviaQuestion:** クイズの質問を表し、 **options**プロパティを使用して関連するオプションを公開します。
    > - **TriviaAnswer:** クイズの質問への応答としてユーザーが選択したオプションを表します。
    > - **TriviaContext:** マニアクイズアプリケーションの Entity Framework のデータベースコンテキストを表します。 このクラスは、 **Dcontext**から派生し、上で説明したエンティティのコレクションを表す**dbset**プロパティを公開します。
    > - **TriviaDatabaseInitializer:** **Createdatabaseifnotexists**から継承する**TriviaContext**クラスの Entity Framework 初期化子の実装。 このクラスの既定の動作では、データベースが存在しない場合にのみデータベースを作成し、 **Seed**メソッドで指定したエンティティを挿入します。
6. **Global.asax.cs**ファイルを開き、次の using ステートメントを追加します。

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample1.cs)]
7. **Application\_Start**メソッドの先頭に次のコードを追加して、データベース初期化子として**TriviaDatabaseInitializer**を設定します。

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample2.cs)]
8. 認証されたユーザーへのアクセスを制限するように**Home**コントローラーを変更します。 これを行うには、 **Controllers**フォルダー内の**HomeController.cs**ファイルを開き、 **HomeController**クラス定義に**承認**属性を追加します。

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample3.cs)]

    > [!NOTE]
    > **承認**フィルターは、ユーザーが認証されているかどうかを確認します。 ユーザーが認証されていない場合は、アクションを呼び出さずに HTTP 状態コード 401 (未承認) が返されます。 フィルターは、グローバルに、コントローラーレベルで、または個々のアクションのレベルで適用できます。
9. ここでは、web ページとブランドのレイアウトをカスタマイズします。 これを行うには、ビュー内で **\_Layout**ファイルを開きます。 *ASP.NET アプリケーション*を*マニアクイズ*に置き換えることによって、 **&lt;title&gt;** 要素の内容を共有フォルダーに更新します。

    [!code-cshtml[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample4.cshtml)]
10. 同じファイルで、 *About*リンクと*Contact*リンクを削除し、*ホーム*リンクの名前を*Play*に変更して、ナビゲーションバーを更新します。 また、[*アプリケーション名*] リンクの名前を「*マニアクイズ*」に変更します。 ナビゲーションバーの HTML は、次のコードのようになります。

    [!code-cshtml[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample5.cshtml)]
11. *ASP.NET アプリケーション*を*マニアクイズ*に置き換えることにより、レイアウトページのフッターを更新します。 これを行うには、 **&lt;フッターの&gt;** 要素の内容を、次の強調表示されたコードに置き換えます。

    [!code-html[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample6.html)]

<a id="Ex1Task2"></a>
#### <a name="task-2--creating-the-triviacontroller-web-api"></a>タスク2– TriviaController Web API の作成

前のタスクでは、マニアクイズ web アプリケーションの初期構造を作成しました。 クイズデータモデルと対話する単純な Web API サービスを構築し、次のアクションを公開するようになりました。

- **GET/api/trivia**: 認証されたユーザーが回答する次の質問をクイズ一覧から取得します。
- **POST/api/trivia**: 認証されたユーザーによって指定されたクイズ回答を格納します。

Visual Studio に用意されている ASP.NET スキャフォールディングツールを使用して、Web API コントローラークラスのベースラインを作成します。

1. **アプリ\_** の [開始] フォルダー内の**WebApiConfig.cs**ファイルを開きます。 このファイルは、web api コントローラーアクションにルートをマップする方法など、Web API サービスの構成を定義します。
2. ファイルの先頭に次の using ステートメントを追加します。

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample7.cs)]
3. 次の強調表示されたコードを**Register**メソッドに追加して、Web API アクションメソッドによって取得される JSON データのフォーマッタをグローバルに構成します。

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample8.cs)]

    > [!NOTE]
    > **CamelCasePropertyNamesContractResolver**は、プロパティ名を*camel*形式に自動的に変換します。これは、JavaScript でのプロパティ名の一般的な規則です。
4. **ソリューションエクスプローラー**で、 **GeekQuiz**プロジェクトの**Controllers**フォルダーを右クリックし、[追加] を選択します。 **新しいスキャフォールディング項目...**

    ![新しいスキャフォールディング項目の作成](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image6.png "新しいスキャフォールディング項目の作成")

    *新しいスキャフォールディング項目の作成*
5. **[スキャフォールディングの追加]** ダイアログボックスで、左側のウィンドウで **[共通]** ノードが選択されていることを確認します。 次に、中央のウィンドウで **[WEB API 2 コントローラー-空]** のテンプレート テンプレートを選択し、 **[追加]** をクリックします。

    ![Web API 2 コントローラーの空のテンプレートを選択する](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image7.png "Web API 2 コントローラーの空のテンプレートを選択する")

    *Web API 2 コントローラーの空のテンプレートを選択する*

    > [!NOTE]
    > **ASP.NET スキャフォールディング**は、ASP.NET Web アプリケーションのコード生成フレームワークです。 Visual Studio 2013 には、MVC および Web API プロジェクト用のプレインストールされたコードジェネレーターが含まれています。 標準データ操作の開発に必要な時間を短縮するために、データモデルと対話するコードをすばやく追加する場合は、プロジェクトでスキャフォールディングを使用する必要があります。
    > 
    > また、スキャフォールディングプロセスによって、必要なすべての依存関係がプロジェクトにインストールされます。 たとえば、空の ASP.NET プロジェクトから開始し、スキャフォールディングを使用して Web API コントローラーを追加すると、必要な Web API の NuGet パッケージと参照がプロジェクトに自動的に追加されます。
6. **[コントローラーの追加]** ダイアログボックスで、 **[コントローラー名]** ボックスに「 *TriviaController* 」と入力し、 **[追加]** をクリックします。

    ![トリビアコントローラーの追加](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image8.png "トリビアコントローラーの追加")

    *トリビアコントローラーの追加*
7. 次に、 **TriviaController.cs**ファイルが**GeekQuiz**プロジェクトの**Controllers**フォルダーに追加されます。このフォルダーには空の**TriviaController**クラスが含まれています。 ファイルの先頭に次の using ステートメントを追加します。

    (コードスニペット- *AspNetWebApiSpa-Ex1-TriviaControllerUsings*)

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample9.cs)]
8. **TriviaController**クラスの先頭に次のコードを追加して、コントローラーの**TriviaContext**インスタンスを定義、初期化、および破棄します。

    (コードスニペット- *AspNetWebApiSpa-Ex1-TriviaControllerContext*)

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample10.cs)]

    > [!NOTE]
    > **TriviaController**の**dispose**メソッドは、 **TriviaContext**インスタンスの**dispose**メソッドを呼び出します。これにより、 **TriviaContext**インスタンスが破棄またはガベージコレクトされたときに、context オブジェクトによって使用されるすべてのリソースが解放されます。 これには、Entity Framework によって開かれたすべてのデータベース接続の終了が含まれます。
9. **TriviaController**クラスの末尾に、次のヘルパーメソッドを追加します。 このメソッドは、指定されたユーザーによって応答されるように、データベースから次のクイズ質問を取得します。

    (コードスニペット- *AspNetWebApiSpa-Ex1-TriviaControllerNextQuestion*)

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample11.cs)]
10. 次の**Get** action メソッドを**TriviaController**クラスに追加します。 このアクションメソッドは、前の手順で定義した**NextQuestionAsync** helper メソッドを呼び出して、認証されたユーザーの次の質問を取得します。

    (コードスニペット- *AspNetWebApiSpa-Ex1-TriviaControllerGetAction*)

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample12.cs)]
11. **TriviaController**クラスの末尾に、次のヘルパーメソッドを追加します。 このメソッドは、指定された回答をデータベースに格納し、答えが正しいかどうかを示すブール値を返します。

    (コードスニペット- *AspNetWebApiSpa-Ex1-TriviaControllerStoreAsync*)

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample13.cs)]
12. 次の**Post**アクションメソッドを**TriviaController**クラスに追加します。 このアクションメソッドは、認証されたユーザーに回答を関連付け、 **StoreAsync** helper メソッドを呼び出します。 次に、ヘルパーメソッドによって返されるブール値を使用して応答を送信します。

    (コードスニペット- *AspNetWebApiSpa-Ex1-TriviaControllerPostAction*)

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample14.cs)]
13. 認証されたユーザーへのアクセスを制限するように Web API コントローラーを変更するには、 **TriviaController**クラス定義に**承認**属性を追加します。

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample15.cs)]

<a id="Ex1Task3"></a>
#### <a name="task-3--running-the-solution"></a>タスク3–ソリューションを実行する

このタスクでは、前のタスクで作成した Web API サービスが想定どおりに動作していることを確認します。 ネットワークトラフィックをキャプチャし、Web API サービスからの完全な応答を調べるには、Internet Explorer **F12 開発者ツール**を使用します。

> [!NOTE]
> Visual Studio ツールバーの **[スタート]** ボタンで**Internet Explorer**が選択されていることを確認します。
> 
> ![Internet Explorer オプション](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image9.png)

1. F5 キーを押して、ソリューションを実行します。 ブラウザーに**ログイン**ページが表示されます。

    > [!NOTE]
    > アプリケーションの起動時に、既定の MVC ルートがトリガーされます。既定では、 **HomeController**クラスの**Index**アクションにマップされます。 **HomeController**は認証されたユーザーに限定されるため (演習1では**承認**属性を使用してクラスを修飾しています)、まだユーザーが認証されていないため、アプリケーションは元の要求をログインページにリダイレクトします。

    ![ソリューションの実行](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image10.png "ソリューションの実行")

    *ソリューションの実行*
2. **[登録]** をクリックして、新しいユーザーを作成します。

    ![新しいユーザーの登録](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image11.png "新しいユーザーの登録")

    *新しいユーザーの登録*
3. **[登録]** ページで、**ユーザー名**と**パスワード**を入力し、 **[登録]** をクリックします。

    ![[登録] ページ](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image12.png "[登録] ページ")

    *[登録] ページ*
4. アプリケーションが新しいアカウントを登録すると、ユーザーが認証され、ホームページにリダイレクトされます。

    ![ユーザーは認証されています](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image13.png "認証されたユーザー")

    *ユーザーは認証されています*
5. ブラウザーで**F12**キーを押して、 **[開発者ツール]** パネルを開きます。 **CTRL + 4**キーを押すか、**ネットワーク**アイコンをクリックし、緑色の矢印ボタンをクリックしてネットワークトラフィックのキャプチャを開始します。

    ![Web API ネットワークキャプチャを開始しています](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image14.png "Web API ネットワークキャプチャを開始しています")

    *Web API ネットワークキャプチャを開始しています*
6. ブラウザーのアドレスバーの URL に**api/トリビア**を追加します。 次に、 **TriviaController**の**Get** action メソッドから応答の詳細を調べます。

    ![Web API を使用して次の質問データを取得する](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image15.png "Web API を使用して次の質問データを取得する")

    *Web API を使用して次の質問データを取得する*

    > [!NOTE]
    > ダウンロードが完了すると、ダウンロードしたファイルに対してアクションを実行するように求められます。 [開発者ツール] ウィンドウで応答の内容を確認できるようにするには、ダイアログボックスを開いたままにしておきます。
7. 次に、応答の本文を調べます。 これを行うには、 **[詳細]** タブをクリックし、 **[応答本文]** をクリックします。 ダウンロードしたデータが、 **TriviaQuestion**クラスに対応するプロパティ**オプション**( **TriviaOption**オブジェクトのリスト)、 **id** 、および**タイトル**を持つオブジェクトであることを確認できます。

    ![Web API 応答本文の表示](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image16.png "Web API 応答本文の表示")

    *Web API の応答本文を表示しています*
8. Visual Studio に戻り、SHIFT キーを押し**ながら F5**キーを押してデバッグを停止します。

<a id="Exercise2"></a>
### <a name="exercise-2-creating-the-spa-interface"></a>演習 2: SPA インターフェイスの作成

この演習では、まず、マニアクイズの web フロントエンドの部分を構築します。 **AngularJS**を使用したシングルページアプリケーションの操作に重点を置いています。 次に、CSS3 でのユーザーエクスペリエンスを向上させ、豊富なアニメーションを実行し、1つの質問から次の質問に移行するときにコンテキストの切り替え効果を視覚的に示すことができるようにします。

<a id="Ex2Task1"></a>
#### <a name="task-1--creating-the-spa-interface-using-angularjs"></a>タスク1– AngularJS を使用して SPA インターフェイスを作成する

このタスクでは、 **AngularJS**を使用して、マニアクイズアプリケーションのクライアント側を実装します。 **AngularJS**は、ブラウザーベースのアプリケーションを*モデルビューコントローラー* (MVC) 機能で強化するオープンソースの JavaScript フレームワークであり、開発とテストの両方を容易にします。

最初に、Visual Studio のパッケージマネージャーコンソールから AngularJS をインストールします。 次に、マニアクイズアプリの動作を提供するコントローラーを作成し、AngularJS テンプレートエンジンを使用してクイズの質問と回答を表示するビューを作成します。

> [!NOTE]
> AngularJS の詳細については、 [[http://angularjs.org/](http://angularjs.org/)](http://angularjs.org/)を参照してください。

1. **Web 用に Visual Studio Express 2013**を開き、 **Source/Ex2 GeekQuiz/Begin**フォルダーにあるソリューションを開きます。 または、前の演習で取得したソリューションを続行することもできます。
2. [**ツール** > **NuGet パッケージマネージャー**] から**パッケージマネージャーコンソール**を開きます。 次のコマンドを入力して、 **AngularJS** NuGet パッケージをインストールします。

    [!code-powershell[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample16.ps1)]
3. **ソリューションエクスプローラー**で、 **GeekQuiz**プロジェクトの**Scripts**フォルダーを右クリックし、[追加] を選択します。 **新しいフォルダー**。 フォルダーに**アプリ**の名前を**指定**し、enter キーを押します。
4. 先ほど作成した**アプリ**フォルダーを右クリックし、[追加] を選択します。 **JavaScript ファイル**。

    ![新しい JavaScript ファイルの作成](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image17.png)

    *新しい JavaScript ファイルの作成*
5. **[項目の名前の指定]** ダイアログボックスの **[項目名]** ボックスに「*クイズ-controller* 」と入力し、 **[OK]** をクリックします。

    ![新しい JavaScript ファイルに名前を付ける](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image18.png)

    *新しい JavaScript ファイルに名前を付ける*
6. **Quiz-controller**ファイルで、AngularJS **QuizCtrl** controller を宣言して初期化する次のコードを追加します。

    (コードスニペット- *AspNetWebApiSpa-Ex2-AngularQuizController*)

    [!code-javascript[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample17.js)]

    > [!NOTE]
    > **QuizCtrl**コントローラーのコンストラクター関数には、 **$scope**という名前の injectable パラメーターが必要です。 スコープの初期状態は、プロパティを **$scope**オブジェクトにアタッチすることによって、コンストラクター関数で設定する必要があります。 プロパティには**ビューモデル**が含まれており、コントローラーが登録されると、テンプレートにアクセスできるようになります。
    > 
    > **QuizCtrl**コントローラーは、 **QuizApp**という名前のモジュール内で定義されています。 モジュールは、アプリケーションを別のコンポーネントに分割できるようにする作業単位です。 モジュールを使用する主な利点は、コードが理解しやすく、単体テスト、再利用性、および保守容易性が向上することです。
7. ここで、ビューからトリガーされたイベントに応答するために、スコープに動作を追加します。 **QuizCtrl**コントローラーの末尾に次のコードを追加して、 **$Scope**オブジェクトで**nextquestion**関数を定義します。

    (コードスニペット- *AspNetWebApiSpa-Ex2-AngularQuizControllerNextQuestion*)

    [!code-javascript[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample18.js)]

    > [!NOTE]
    > この関数は、前の演習で作成した**トリビア**Web API から次の質問を取得し、その質問データを **$scope**オブジェクトにアタッチします。
8. **QuizCtrl**コントローラーの末尾に次のコードを挿入して、 **$Scope**オブジェクトで**sendanswer**関数を定義します。

    (コードスニペット- *AspNetWebApiSpa-Ex2-AngularQuizControllerSendAnswer*)

    [!code-javascript[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample19.js)]

    > [!NOTE]
    > この関数は、ユーザーによって選択された回答を**トリビア**Web API に送信し、結果を格納します。つまり、 **$scope**オブジェクト内の結果が正しいかどうかを示します。
    > 
    > 上記の**Nextquestion**と**sendanswer**関数は、AngularJS **$http**オブジェクトを使用して、ブラウザーから XMLHttpRequest JAVASCRIPT オブジェクトを介して Web API との通信を抽象化します。 AngularJS は、RESTful Api を介してリソースに対して CRUD 操作を実行するために、より高いレベルの抽象化を提供する別のサービスをサポートしています。 AngularJS **$resource**オブジェクトには、 **$http**オブジェクトと対話する必要がない高レベルの動作を提供するアクションメソッドがあります。 CRUD モデルを必要とするシナリオでは、 **$resource**オブジェクトの使用を検討してください (前景の情報、 [$resource のドキュメント](https://docs.angularjs.org/api/ngResource/service/$resource)を参照してください)。
9. 次の手順では、クイズのビューを定義する AngularJS テンプレートを作成します。 これを行うには、Views | の内側にある**Index. cshtml**ファイルを開きます。 **[ホーム**] フォルダーを使用して、内容を次のコードに置き換えます。

    (コードスニペット- *AspNetWebApiSpa-Ex2-GeekQuizView*)

    [!code-cshtml[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample20.cshtml)]

    > [!NOTE]
    > AngularJS テンプレートは、モデルとコントローラーの情報を使用して、ブラウザーでユーザーに表示される動的ビューに静的マークアップを変換する宣言型の仕様です。 テンプレートで使用できる AngularJS 要素と要素属性の例を次に示します。
    > 
    > - AngularJS**ディレクティブは、アプリケーション**のルート要素を表す DOM 要素をに指示します。
    > - **Ng コントローラー**ディレクティブは、ディレクティブが宣言されているポイントで、コントローラーを DOM にアタッチします。
    > - 中かっこの表記 **{{}}** は、コントローラーで定義されているスコーププロパティへのバインドを示します。
    > - **Ng**ディレクティブは、ユーザーのクリックに応じてスコープ内で定義されている関数を呼び出すために使用されます。
10. **Content**フォルダー内で**サイトの .css**ファイルを開き、次の強調表示されたスタイルをファイルの末尾に追加して、クイズビューのルックアンドフィールを提供します。

    (コードスニペット- *AspNetWebApiSpa-Ex2-GeekQuizStyles*)

    [!code-css[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample21.css)]

<a id="Ex2Task2"></a>
#### <a name="task-2--running-the-solution"></a>タスク2–ソリューションを実行する

このタスクでは、AngularJS で作成した新しいユーザーインターフェイスを使用してソリューションを実行し、いくつかのクイズの質問に回答します。

1. F5 キーを押して、ソリューションを実行します。
2. 新しいユーザーアカウントを登録します。 これを行うには、「演習1、タスク3」で説明されている登録手順に従います。

    > [!NOTE]
    > 前の演習のソリューションを使用している場合は、前に作成したユーザーアカウントを使用してログインできます。
3. **ホーム**ページが表示され、クイズの最初の質問が表示されます。 いずれかのオプションをクリックして質問に回答します。 これにより、前に定義した**Sendanswer**関数がトリガーされ、選択したオプションが**トリビア**Web API に送信されます。

    ![質問への回答](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image19.png "質問への回答")

    *質問への回答*
4. いずれかのボタンをクリックすると、回答が表示されます。 **[次の質問]** をクリックして、次の質問を表示します。 これにより、コントローラーで定義されている**Nextquestion**関数がトリガーされます。

    ![次の質問を要求する](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image20.png "次の質問を要求する")

    *次の質問を要求する*
5. 次の質問が表示されます。 必要に応じて何度でも質問に答えることができます。 すべての質問を完了したら、最初の質問に戻ります。

    ![もう1つの質問](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image21.png "もう1つの質問")

    *次の質問*
6. Visual Studio に戻り、SHIFT キーを押し**ながら F5**キーを押してデバッグを停止します。

<a id="Ex2Task3"></a>
#### <a name="task-3--creating-a-flip-animation-using-css3"></a>タスク3– CSS3 を使用したフリップアニメーションの作成

このタスクでは、CSS3 プロパティを使用して、質問に回答し、次の質問を取得したときにフリップ効果を追加することにより、豊富なアニメーションを実行します。

1. **ソリューションエクスプローラー**で、 **GeekQuiz**プロジェクトの**Content**フォルダーを右クリックし、[追加] を選択します。 **既存の項目...** .

    ![既存の項目をコンテンツフォルダーに追加する](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image22.png "既存の項目をコンテンツフォルダーに追加する")

    *既存の項目をコンテンツフォルダーに追加する*
2. **[既存項目の追加]** ダイアログボックスで、 **[ソース/アセット]** フォルダーに移動し、 **[css の反転]** を選択します。 **[追加]** をクリックします。

    ![アセットからのフリップ .css ファイルの追加](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image23.png "アセットからのフリップ .css ファイルの追加")

    *アセットからのフリップ .css ファイルの追加*
3. 追加した**フリップ .css**ファイルを開き、その内容を検査します。
4. **フリップ変換**のコメントを探します。 このコメントの下にあるスタイルでは、CSS**パースペクティブ**と**rotateY**変換を使用して &quot;カードフリップ&quot; 効果を生成します。

    [!code-css[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample22.css)]
5. [**フリップコメント中にウィンドウの背景を非表示にする]** を探します。 このコメントの下のスタイルでは、 **[背景の表示]** CSS プロパティを [*非表示*] に設定することにより、顔がビューアーから離れているときに、顔の背面が非表示になります。

    [!code-css[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample23.css)]
6. **App\_Start**フォルダー内の**BundleConfig.cs**ファイルを開き、 **&quot;~/content/Css&quot;** スタイルバンドルに**フリップ .css**ファイルへの参照を追加します。

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample24.cs)]
7. **F5**キーを押してソリューションを実行し、資格情報でログインします。
8. いずれかのオプションをクリックして質問に回答します。 ビュー間を切り替えるときのフリップ効果に注意してください。

    ![フリップ効果のある質問への回答](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image24.png "フリップ効果のある質問への回答")

    *フリップ効果のある質問への回答*
9. **[次の質問]** をクリックして、次の質問を取得します。 フリップ効果が再び表示されます。

    ![フリップ効果で次の質問を取得する](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image25.png "フリップ効果で次の質問を取得する")

    *フリップ効果で次の質問を取得する*

---

<a id="Summary"></a>
## <a name="summary"></a>まとめ

このハンズオンラボを完了することで、次の方法を学習できました。

- ASP.NET スキャフォールディングを使用して ASP.NET Web API コントローラーを作成する
- Web API の Get アクションを実装して、次のクイズの質問を取得する
- クイズの回答を格納するための Web API Post アクションを実装する
- Visual Studio パッケージマネージャーコンソールから AngularJS をインストールする
- AngularJS のテンプレートとコントローラーを実装する
- CSS3 の切り替えを使用してアニメーション効果を行う
