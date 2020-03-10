---
uid: visual-studio/overview/2013/one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api
title: 'ハンズオンラボ: One ASP.NET: ASP.NET Web フォーム、MVC、Web API の統合 |Microsoft Docs'
author: rick-anderson
description: ASP.NET は、MVC、Web API などの特殊なテクノロジを使用して、Web サイト、アプリ、サービスを構築するためのフレームワークです。 拡張 ASP.NET...
ms.author: riande
ms.date: 07/16/2014
ms.assetid: 4fe2558d-67cc-4d12-a5c1-6fb9f6f16137
msc.legacyurl: /visual-studio/overview/2013/one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api
msc.type: authoredcontent
ms.openlocfilehash: 165d104b5d3ef3281af449cc8673ad96f531d628
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78505456"
---
# <a name="hands-on-lab-one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api"></a>ハンズオンラボ: One ASP.NET: ASP.NET Web フォーム、MVC、Web API の統合

[Web キャンプチーム](https://twitter.com/webcamps)別

[Web キャンプトレーニングキットをダウンロードする](https://aka.ms/webcamps-training-kit)

> ASP.NET は、MVC、Web API などの特殊なテクノロジを使用して、Web サイト、アプリ、サービスを構築するためのフレームワークです。 拡張 ASP.NET が作成されてから、このようなテクノロジを統合する必要があることがわかったので、 **1 つの ASP.NET**に向けた最近の取り組みが行われています。
> 
> Visual Studio 2013 には、アプリケーションをビルドし、すべての ASP.NET テクノロジを1つのプロジェクトで使用できる新しい統合プロジェクトシステムが導入されています。 この機能により、プロジェクトの開始時に1つのテクノロジを選択する必要がなくなり、1つのプロジェクト内で複数の ASP.NET フレームワークを使用することが促進されます。
> 
> すべてのサンプルコードとスニペットは、 [https://aka.ms/webcamps-training-kit](https://aka.ms/webcamps-training-kit)で入手できる Web キャンプトレーニングキットに含まれています。

<a id="Overview"></a>
## <a name="overview"></a>概要

<a id="Objectives"></a>
### <a name="objectives"></a>目標

このハンズオンラボでは、次の方法を学習します。

- **1 つの ASP.NET**プロジェクトの種類に基づいて Web サイトを作成する
- **MVC**や**Web API**などのさまざまな**ASP.NET**フレームワークを同じプロジェクトで使用する
- **ASP.NET**アプリケーションの主要なコンポーネントを特定する
- **ASP.NET スキャフォールディング**フレームワークを活用して、モデルクラスに基づいて CRUD 操作を実行するコントローラーとビューを自動的に作成します。
- ジョブごとに適切なツールを使用して、コンピューターとユーザーが判読できる形式で同じ情報のセットを公開します。

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>前提条件

このハンズオンラボを完了するには、次のものが必要です。

- [Web 用に2013を Visual Studio Express](https://www.microsoft.com/visualstudio/)
- [Visual Studio 2013 Update 1](https://go.microsoft.com/fwlink/?LinkId=301714)

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

1. [新しい Web フォームプロジェクトの作成](#Exercise1)
2. [スキャフォールディングを使用した MVC コントローラーの作成](#Exercise2)
3. [スキャフォールディングを使用した Web API コントローラーの作成](#Exercise3)

このラボの推定所要時間: **60 分**

> [!NOTE]
> Visual Studio を初めて起動するときに、定義済みの設定コレクションのいずれかを選択する必要があります。 定義済みの各コレクションは、特定の開発スタイルに一致するように設計されており、ウィンドウのレイアウト、エディターの動作、IntelliSense コードスニペット、およびダイアログボックスのオプションを決定します。 このラボの手順では、**全般的な開発設定**のコレクションを使用するときに、Visual Studio で特定のタスクを実行するために必要なアクションについて説明します。 開発環境に対して別の設定コレクションを選択した場合は、注意が必要な手順が異なる場合があります。

<a id="Exercise1"></a>
### <a name="exercise-1-creating-a-new-web-forms-project"></a>演習 1: 新しい Web フォームプロジェクトの作成

この演習では、 **ASP.NET**統合プロジェクトのエクスペリエンスを使用して、Visual Studio 2013 に新しい web フォームサイトを作成します。これにより、web フォーム、MVC、および web API コンポーネントを同じアプリケーションに簡単に統合できます。 次に、生成されたソリューションを調査し、その部分を特定します。最後に、Web サイトが動作していることを確認します。

<a id="Ex1Task1"></a>
#### <a name="task-1--creating-a-new-site-using-the-one-aspnet-experience"></a>タスク 1-ASP.NET エクスペリエンスを1つ使用して新しいサイトを作成する

このタスクでは、 **1 つの ASP.NET**プロジェクトの種類に基づいて、Visual Studio で新しい Web サイトの作成を開始します。 **ASP.NET**は、すべての ASP.NET テクノロジを統合し、必要に応じてそれらを組み合わせて照合するオプションを提供します。 次に、Web フォーム、MVC、Web API のさまざまなコンポーネントを、アプリケーション内で並行して認識します。

1. **Web 用 Visual Studio Express 2013**を開き、[ファイル] を選択します。 **新しいプロジェクト...** を実行すると、新しいソリューションが開始されます。

    ![新規プロジェクトの作成](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image1.png)

    *新しいプロジェクトの作成*
2. **[新しいプロジェクト]** ダイアログボックスで、Visual  **C# | の下にある [ASP.NET Web Application] を選択します。[Web** ] タブで、 **.NET Framework 4.5**が選択されていることを確認します。 プロジェクトに*MyHybridSite*という名前を指定し、**場所**を選択して [ **OK]** をクリックします。

    ![新しい ASP.NET Web アプリケーションプロジェクト](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image2.png)

    *新しい ASP.NET Web アプリケーションプロジェクトの作成*
3. **[New ASP.NET プロジェクト]** ダイアログボックスで、 **[Web フォーム]** テンプレートを選択し、 **[MVC]** オプションと **[web API]** オプションを選択します。 また、**認証**オプションが**個々のユーザーアカウント**に設定されていることを確認します。 続行するには、 **[OK]** をクリックします。

    ![Web API と MVC コンポーネントを含む、Web フォームテンプレートを使用した新しいプロジェクトの作成](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image3.png)

    *Web API と MVC コンポーネントを含む、Web フォームテンプレートを使用した新しいプロジェクトの作成*
4. 生成されたソリューションの構造を調べることができるようになりました。

    ![生成されたソリューションの調査](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image4.png)

    *生成されたソリューションの調査*

    1. **アカウント:** このフォルダーには、アプリケーションのユーザーアカウントを登録、ログイン、および管理するための Web フォームページが含まれています。 このフォルダーは、Web フォームプロジェクトテンプレートの構成中に [**個々のユーザーアカウント**認証] オプションを選択すると追加されます。
    2. **モデル:** このフォルダーには、アプリケーションデータを表すクラスが含まれます。
    3. **コントローラー**と**ビュー**: これらのフォルダーは、 **ASP.NET の MVC**コンポーネントと**ASP.NET Web API**コンポーネントに必要です。 次の演習では、MVC と Web API テクノロジについて説明します。
    4. Default.aspx **、** **Contact .aspx** 、および **.aspx ファイルについて**は、事前に定義された Web フォームページであり、アプリケーションに固有のページを構築するための開始点として使用できます。 これらのファイルのプログラミングロジックは、&quot;分離コード&quot; ファイルと呼ばれる別のファイルに存在します。このファイルには、使用する言語に応じて &quot;.aspx&quot; または &quot;. aspx.cs&quot; extension があります。 分離コードロジックはサーバー上で実行され、ページの HTML 出力を動的に生成します。
    5. このページ**では、** アプリケーション内のすべてのページのルックアンドフィールと標準動作が定義され**ています**。
5. **Default.aspx**ファイルをダブルクリックして、ページの内容を調べます。

    ![Default.aspx ページの調査](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image5.png)

    *Default.aspx ページの調査*

    > [!NOTE]
    > ファイルの先頭にある**ページ**ディレクティブによって、Web フォームページの属性が定義されます。 たとえば、 **MasterPageFile**属性はマスターページへのパスを指定します。この場合、この例**では、** 継承するページの分離コードクラスを定義し*ます。* このクラスは、**分離コード**属性によって決定されるファイルにあります。
    > 
    > **Asp: content**コントロールは、ページの実際のコンテンツ (テキスト、マークアップ、およびコントロール) を保持し、マスターページの**asp: ContentPlaceHolder**コントロールにマップされます。 この場合、ページコンテンツは、*サイトのマスター*ページで定義されている*maincontent*コントロール内に表示されます。
6. **アプリ\_[開始**] フォルダーを展開し、 **WebApiConfig.cs**ファイルを確認します。 Visual Studio では、ASP.NET テンプレートを使用してプロジェクトを構成するときに Web API が含まれているため、生成されたソリューションにそのファイルが含まれていました。
7. **WebApiConfig.cs**ファイルを開きます。 *Webapiconfig.cs*クラスには、web api に関連付けられている構成があります。これにより、HTTP ルートが**web api コントローラー**にマップされます。

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample1.cs)]
8. **RouteConfig.cs**ファイルを開きます。 *RegisterRoutes*メソッド内には、mvc に関連付けられている構成があります。これは、 **MVC コントローラー**に HTTP ルートをマップします。

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample2.cs)]

<a id="Ex1Task2"></a>
#### <a name="task-2--running-the-solution"></a>タスク2–ソリューションを実行する

このタスクでは、生成されたソリューションを実行し、アプリとその機能の一部 (URL リライトや組み込み認証など) を探索します。

1. ソリューションを実行するには、 **F5**キーを押すか、ツールバーにある **[開始]** ボタンをクリックします。 アプリケーションのホームページがブラウザーに表示されます。

    ![ソリューションの実行](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image6.png)
2. Web フォームページが呼び出されていることを確認します。 これを行うには、アドレスバーの URL に **/contactを** **追加し、enter キーを**押します。

    ![わかりやすい URL](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image7.png)

    *わかりやすい Url*

    > [!NOTE]
    > ご覧のとおり、URL は **/contact**に変わります。 **ASP.NET 4**以降では、url ルーティング機能が Web フォームに追加され、 *[http://www.mysite.com/products.aspx?category=software](http://www.mysite.com/products.aspx?category=software)* ではなく *[http://www.mysite.com/products/software](http://www.mysite.com/products/software)* のような url を記述できるようになりました。 詳細については、「 [URL ルーティング](../../../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/url-routing.md)」を参照してください。
3. ここでは、アプリケーションに統合されている認証フローについて説明します。 これを行うには、ページの右上隅にある **[登録]** をクリックします。

    ![新しいユーザーの登録](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image8.png)

    *新しいユーザーの登録*
4. **[登録]** ページで、**ユーザー名**と**パスワード**を入力し、 **[登録]** をクリックします。

    ![[登録] ページ](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image9.png)

    *[登録] ページ*
5. アプリケーションは新しいアカウントを登録し、ユーザーは認証されます。

    ![認証されたユーザー](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image10.png)

    *認証されたユーザー*
6. Visual Studio に戻り、SHIFT キーを押し**ながら F5**キーを押してデバッグを停止します。

<a id="Exercise2"></a>
### <a name="exercise-2-creating-an-mvc-controller-using-scaffolding"></a>演習 2: スキャフォールディングを使用した MVC コントローラーの作成

この演習では、Visual Studio に用意されている ASP.NET スキャフォールディングフレームワークを利用して、アクションと Razor ビューを含む ASP.NET MVC 5 コントローラーを作成し、コードを1行も記述せずに CRUD 操作を実行します。 スキャフォールディングプロセスでは、Entity Framework Code First を使用して、SQL データベースのデータコンテキストとデータベーススキーマを生成します。

**Entity Framework Code First について**

Entity Framework (EF) は、リレーショナルストレージスキーマを使用して直接プログラミングするのではなく、概念アプリケーションモデルを使用してプログラミングすることで、データアクセスアプリケーションを作成できる、オブジェクトリレーショナルマッパー (ORM) です。

Entity Framework Code First モデリングワークフローを使用すると、独自のドメインクラスを使用して、クエリ、変更の追跡、および更新の各関数を実行するときに EF が依存するモデルを表すことができます。 Code First 開発ワークフローを使用して、データベースを作成したり、スキーマを指定したりして、アプリケーションを開始する必要はありません。 代わりに、アプリケーションに最も適したドメインモデルオブジェクトを定義する標準の .NET クラスを作成し、Entity Framework によってデータベースが作成されるようにします。

> [!NOTE]
> Entity Framework の詳細については、[こちら](../../../entity-framework.md)を参照してください。

<a id="Ex2Task1"></a>
#### <a name="task-1--creating-a-new-model"></a>タスク1–新しいモデルの作成

ここでは、**ユーザー**クラスを定義します。これは、MVC コントローラーとビューを作成するためにスキャフォールディングプロセスによって使用されるモデルです。 まず、 **Person**モデルクラスを作成します。その後、コントローラーの CRUD 操作は、スキャフォールディング機能を使用して自動的に作成されます。

1. **Web 用に Visual Studio Express 2013**を開き、 **Source/Ex2-mvcscaffolding/Begin**フォルダーにある**MyHybridSite**ソリューションを開きます。 または、前の演習で取得したソリューションを続行することもできます。
2. **ソリューションエクスプローラー**で、 **MyHybridSite**プロジェクトの **モデル** フォルダーを右クリックし、追加 を選択します。 **クラス.** ...

    ![Person モデルクラスの追加](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image11.png)

    *Person モデルクラスの追加*
3. **[新しい項目の追加]** ダイアログボックスで、ファイルに*Person.cs*という名前を指定し、 **[追加]** をクリックします。

    ![Person モデルクラスの作成](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image12.png)

    *Person モデルクラスの作成*
4. **Person.cs**ファイルの内容を次のコードに置き換えます。 **CTRL + S**キーを押して、変更を保存します。

    (コードスニペット- *BringingTogetherOneAspNet-Ex2-個人クラス*)

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample3.cs)]
5. **ソリューションエクスプローラー**で、 **MyHybridSite**プロジェクトを右クリックし、 **[ビルド]** を選択するか、 **CTRL + SHIFT + B**キーを押してプロジェクトをビルドします。

<a id="Ex2Task2"></a>
#### <a name="task-2--creating-an-mvc-controller"></a>タスク 2-MVC コントローラーの作成

これで、 **person**モデルが作成されたので、Entity Framework で ASP.NET MVC スキャフォールディングを使用して、**ユーザー**の CRUD コントローラーアクションとビューを作成します。

1. **ソリューションエクスプローラー**で、 **MyHybridSite**プロジェクトの**Controllers**フォルダーを右クリックし、[追加] を選択します。 **新しいスキャフォールディング項目...**

    ![新しいスキャフォールディングコントローラーを作成する](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image13.png)

    *新しいスキャフォールディングコントローラーを作成する*
2. **[スキャフォールディングの追加]** ダイアログボックスで、 **[MVC 5 Controller with views]** を選択し Entity Framework を使用して [追加] をクリックし**ます。**

    ![ビューと Entity Framework がある MVC 5 コントローラーの選択](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image14.png)

    *ビューと Entity Framework がある MVC 5 コントローラーの選択*
3. [ *Mvc個人コントローラー* ] を**コントローラー名**として設定し、 **[非同期コントローラーアクションを使用する]** オプションを選択して、**モデルクラス**として **[Person (MyHybridSite)]** を選択します。

    ![スキャフォールディングを使用した MVC コントローラーの追加](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image15.png)

    *スキャフォールディングを使用した MVC コントローラーの追加*
4. **[データコンテキストクラス]** で、 **[新しいデータコンテキスト]** をクリックします。

    ![新しいデータコンテキストの作成](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image16.png)

    *新しいデータコンテキストの作成*
5. **[新しいデータコンテキスト]** ダイアログボックスで、新しいデータコンテキストに「*個人のコンテキスト*」という名前を指定し、 **[追加]** をクリックします。

    ![新しい個人のコンテキストを作成する](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image17.png)

    *新しい個人コンテキストの種類を作成する*
6. **[追加]** をクリックして、スキャフォールディングを持つ**ユーザー**の新しいコントローラーを作成します。 次に、Visual Studio によってコントローラーアクション、Person データコンテキスト、および Razor ビューが生成されます。

    ![スキャフォールディングを使用して MVC コントローラーを作成した後](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image18.png)

    *スキャフォールディングを使用して MVC コントローラーを作成した後*
7. **Controllers**フォルダーの**MvcPersonController.cs**ファイルを開きます。 CRUD アクションメソッドが自動的に生成されていることに注意してください。

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample4.cs)]

    > [!NOTE]
    > 前の手順で スキャフォールディング オプションから  **async controller アクションを使用する** チェックボックスをオンにすると、Visual Studio によって、Person データコンテキストへのアクセスを伴うすべてのアクションの非同期アクションメソッドが生成されます。 要求の処理中に Web サーバーが処理を実行できないようにするために、実行時間の長い CPU にバインドされていない要求には非同期アクションメソッドを使用することをお勧めします。

<a id="Ex2Task3"></a>
#### <a name="task-3--running-the-solution"></a>タスク3–ソリューションを実行する

このタスクでは、ソリューションをもう一度実行して、**ユーザー**のビューが想定どおりに機能していることを確認します。 新しいユーザーを追加して、データベースに正常に保存されたことを確認します。

1. F5 キーを押して、ソリューションを実行します。
2. **/MvcPerson**に移動します。 スキャフォールディングビューが表示されます。
3. **[新規作成]** をクリックして、新しいユーザーを追加します。

    ![スキャフォールディング MVC ビューへの移動](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image19.png)

    *スキャフォールディング MVC ビューへの移動*
4. **[作成]** ビューで、ユーザーの**名前**と**年齢**を指定し、 **[作成]** をクリックします。

    ![新しいユーザーの追加](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image20.png)

    *新しいユーザーの追加*
5. 新しいユーザーがリストに追加されます。 要素 ボックスの一覧の **詳細** をクリックして、個人の詳細ビューを表示します。 次に、**詳細**ビューで、 **[戻る]** をクリックしてリストビューに戻ります。

    ![個人の詳細ビュー](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image21.png)

    *個人の詳細ビュー*
6. **[削除]** リンクをクリックして、ユーザーを削除します。 **[削除]** ビューで、 **[削除]** をクリックして操作を確定します。

    ![個人の削除](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image22.png)

    *個人の削除*
7. Visual Studio に戻り、SHIFT キーを押し**ながら F5**キーを押してデバッグを停止します。

<a id="Exercise3"></a>
### <a name="exercise-3-creating-a-web-api-controller-using-scaffolding"></a>演習 3: スキャフォールディングを使用した Web API コントローラーの作成

Web API フレームワークは ASP.NET スタックの一部であり、HTTP サービスの実装を容易にするように設計されており、一般的には、RESTful API を使用して JSON または XML 形式のデータを送受信します。

この演習では、ASP.NET スキャフォールディングを再度使用して、Web API コントローラーを生成します。 同じ person データを JSON 形式で提供するために、前の演習で作成したものと同じ**person**クラスと個人の**コンテキスト**クラスを使用します。 同じ ASP.NET アプリケーション内のさまざまな方法で同じリソースを公開する方法がわかります。

<a id="Ex3Task1"></a>
#### <a name="task-1--creating-a-web-api-controller"></a>タスク 1-Web API コントローラーを作成する

このタスクでは、ユーザーデータを JSON などのコンピューター使用形式で公開する新しい**WEB API コントローラー**を作成します。

1. まだ開いていない場合は、 **Web 用 Visual Studio Express 2013**を開き、 **Source/Ex3-WebAPI/Begin**フォルダーにある**MyHybridSite**ソリューションを開きます。 または、前の演習で取得したソリューションを続行することもできます。

    > [!NOTE]
    > 演習3から始めるソリューションを開始する場合は、 **CTRL + SHIFT + B**キーを押してソリューションをビルドします。
2. **ソリューションエクスプローラー**で、 **MyHybridSite**プロジェクトの**Controllers**フォルダーを右クリックし、[追加] を選択します。 **新しいスキャフォールディング項目...**

    ![新しいスキャフォールディングコントローラーを作成する](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image23.png)

    *新しいスキャフォールディングコントローラーを作成する*
3. **[スキャフォールディングの追加]** ダイアログボックスの左側のウィンドウで **[web api]** を選択し、次に、中央のウィンドウで**Entity Framework を使用して [web api 2 コントローラー** ] をクリックし、[追加] をクリックし**ます。**

    ![アクションと Entity Framework がある Web API 2 コントローラーを選択する](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image24.png "アクションと Entity Framework がある Web API 2 コントローラーを選択する")

    *アクションと Entity Framework がある Web API 2 コントローラーを選択する*
4. *Apiperson controller*を**コントローラー名**として設定し、 **[非同期コントローラーアクションを使用する]** オプションを選択し、**モデル**および**データコンテキスト**クラスとして **[Person (MyHybridSite)]** と ユーザー **[コンテキスト (MyHybridSite)]** をそれぞれ選択します。 **[追加]** をクリックします。

    ![スキャフォールディングを使用した Web API コントローラーの追加](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image25.png "スキャフォールディングを使用した Web API コントローラーの追加")

    *スキャフォールディングを使用した Web API コントローラーの追加*
5. 次に、データを操作する4つの CRUD アクションを使用して、Visual Studio によって**Api個人コントローラー**クラスが生成されます。

    ![スキャフォールディングを使用して Web API コントローラーを作成した後](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image26.png "スキャフォールディングを使用して Web API コントローラーを作成した後")

    *スキャフォールディングを使用して Web API コントローラーを作成した後*
6. **ApiPersonController.cs**ファイルを開き、 *getpeople*アクションメソッドを調べます。 このメソッドは、個人データを取得するために、**個人のコンテキスト**型の db フィールドに対してクエリを行います。

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample5.cs)]
7. ここで、メソッド定義の上にコメントがあることを確認します。 これは、次のタスクで使用するこのアクションを公開する URI を提供します。

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample6.cs)]

    > [!NOTE]
    > 既定では、Web API は、MVC コントローラーとの競合を避けるために、 */API*パスに対するクエリをキャッチするように構成されています。 この設定を変更する必要がある場合は、「 [ASP.NET Web API でのルーティング」](../../../web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api.md)を参照してください。

<a id="Ex3Task2"></a>
#### <a name="task-2--running-the-solution"></a>タスク2–ソリューションを実行する

このタスクでは、Internet Explorer **F12 開発者ツール**を使用して、Web API コントローラーからの完全な応答を検査します。 ネットワークトラフィックをキャプチャして、アプリケーションデータに関する洞察を得る方法を確認できます。

> [!NOTE]
> Visual Studio ツールバーの **[スタート]** ボタンで**Internet Explorer**が選択されていることを確認します。
> 
> ![Internet Explorer オプション](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image27.png)
> 
> **F12 開発者ツール**には、このハンズオンラボでは説明されていない豊富な機能が用意されています。 詳細については、「 [F12 開発者ツールの使用](https://msdn.microsoft.com/library/ie/bg182326(v=vs.85))」を参照してください。

1. F5 キーを押して、ソリューションを実行します。

    > [!NOTE]
    > このタスクを正しく実行するには、アプリケーションにデータが必要です。 データベースが空の場合は、演習2のタスク3に戻り、MVC ビューを使用して新しいユーザーを作成する方法の手順に従います。
2. ブラウザーで**F12**キーを押して、 **[開発者ツール]** パネルを開きます。 **CTRL** + **4**キーを押すか、**ネットワーク**アイコンをクリックし、緑色の矢印ボタンをクリックしてネットワークトラフィックのキャプチャを開始します。

    ![Web API ネットワークキャプチャを開始しています](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image28.png "Web API ネットワークキャプチャを開始しています")

    *Web API ネットワークキャプチャを開始しています*
3. **Api/ApiPerson**をブラウザーのアドレスバーの URL に追加します。 次に、 **Api個人コントローラー**からの応答の詳細を調査します。

    ![Web API を使用して個人データを取得する](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image29.png "Web API を使用して個人データを取得する")

    *Web API を使用して個人データを取得する*

    > [!NOTE]
    > ダウンロードが完了すると、ダウンロードしたファイルに対してアクションを実行するように求められます。 [開発者ツール] ウィンドウで応答の内容を確認できるようにするには、ダイアログボックスを開いたままにしておきます。
4. 次に、応答の本文を調べます。 これを行うには、 **[詳細]** タブをクリックし、 **[応答本文]** をクリックします。 ダウンロードしたデータが、 **Person**クラスに対応するプロパティ**Id**、**名前**、および**Age**を持つオブジェクトの一覧であることを確認できます。

    ![Web API の応答本文を表示しています](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image30.png "Web API の応答本文を表示しています")

    *Web API の応答本文を表示しています*

<a id="Ex3Task3"></a>
#### <a name="task-3--adding-web-api-help-pages"></a>タスク3– Web API のヘルプページを追加する

Web API を作成するときに、他の開発者が API の呼び出し方法を理解できるように、ヘルプページを作成すると便利です。 ドキュメントページは手動で作成および更新できますが、メンテナンス作業を行わないように自動生成することをお勧めします。 このタスクでは、Nuget パッケージを使用して、Web API のヘルプページをソリューションに自動的に生成します。

1. Visual Studio の **[ツール]** メニューで、 **[NuGet パッケージマネージャー]** を選択し、 **[パッケージマネージャーコンソール]** をクリックします。
2. **[パッケージマネージャーコンソール]** ウィンドウで、次のコマンドを実行します。

    [!code-powershell[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample7.ps1)]

    > [!NOTE]
    > **WebApi**パッケージは、必要なアセンブリをインストールし、[区分]/[ヘルプ **] ページ**フォルダーの下にあるヘルプページの MVC ビューを追加します。

    ![HelpPage 領域](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image31.png "HelpPage 領域")

    *HelpPage 領域*
3. 既定では、ヘルプページにドキュメントのプレースホルダー文字列があります。 XML ドキュメントコメントを使用して、ドキュメントを作成できます。 この機能を有効にするには、[**区分]、[ヘルプ] ページ、アプリ\_[開始**] フォルダーにある**HelpPageConfig.cs**ファイルを開き、次の行をコメント解除します。

    [!code-javascript[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample8.js)]
4. **ソリューションエクスプローラー**で、プロジェクト**MyHybridSite**を右クリックし、 **[プロパティ]** をクリックして、 **[ビルド]** タブをクリックします。

    ![[ビルド] タブ](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image32.png "ビルドセクション")

    *[ビルド] タブ*
5. **[出力]** で、 **[XML ドキュメントファイル]** を選択します。 [編集] ボックスに「 **App\_Data/XmlDocument**」と入力します。

    ![[ビルド] タブの [出力] セクション](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image33.png "[ビルド] タブの [出力] セクション")

    *[ビルド] タブの [出力] セクション*
6. **CTRL** + **S**キーを押して、変更を保存します。
7. **Controllers**フォルダーから**ApiPersonController.cs**ファイルを開きます。
8. *Getpeople*メソッドシグネチャと *//GET Api/apiperson*コメントの間に新しい行を入力し、3つのスラッシュを入力します。

    > [!NOTE]
    > メソッドのドキュメントを定義する XML 要素が Visual Studio によって自動的に挿入されます。
9. *Getpeople*メソッドの概要テキストと戻り値を追加します。 これは次のようになります。

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample9.cs)]
10. F5 キーを押して、ソリューションを実行します。
11. アドレスバーの URL に **/help**を追加して、ヘルプページを参照します。

    ![ASP.NET Web API ヘルプページ](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image34.png "ASP.NET Web API ヘルプページ")

    *ASP.NET Web API ヘルプページ*

    > [!NOTE]
    > ページのメインコンテンツは、コントローラー別にグループ化された Api のテーブルです。 テーブルエントリは、 **Iapiexplorer**インターフェイスを使用して動的に生成されます。 API コントローラーを追加または更新すると、次にアプリケーションをビルドしたときにテーブルが自動的に更新されます。
    > 
    > **[API]** 列には、HTTP メソッドと相対 URI が表示されます。 **Description**列には、メソッドのドキュメントから抽出された情報が含まれています。
12. メソッド定義の上に追加した説明が 説明列に表示されることに注意してください。

    ![API メソッドの説明](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image35.png "API メソッドの説明")

    *API メソッドの説明*
13. API メソッドのいずれかをクリックして、応答本文のサンプルなどの詳細な情報が記載されたページに移動します。

    ![[詳細情報] ページ](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image36.png "[詳細情報] ページ")

    *詳細情報ページ*

---

<a id="Summary"></a>
## <a name="summary"></a>まとめ

このハンズオンラボを完了することで、次の方法を学習できました。

- Visual Studio 2013 の1つの ASP.NET エクスペリエンスを使用して新しい Web アプリケーションを作成します。
- 複数の ASP.NET テクノロジを1つのプロジェクトに統合する
- ASP.NET スキャフォールディングを使用してモデルクラスから MVC コントローラーとビューを生成する
- 非同期プログラミングやデータアクセスなどの機能を使用して、Web API コントローラーを生成 Entity Framework
- コントローラーの Web API ヘルプページを自動的に生成する
