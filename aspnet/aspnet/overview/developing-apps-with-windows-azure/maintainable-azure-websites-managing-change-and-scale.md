---
uid: aspnet/overview/developing-apps-with-windows-azure/maintainable-azure-websites-managing-change-and-scale
title: 'ハンズオンラボ: メンテナンス可能な Azure Websites: 変更とスケールの管理 |Microsoft Docs'
author: rick-anderson
description: このラボでは、Microsoft Azure を使用して、web サイトを簡単に構築して運用環境に展開する方法について説明します。
ms.author: riande
ms.date: 07/16/2014
ms.assetid: ecfd0eb4-c4ad-44e6-9db9-a2a66611ff6a
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/maintainable-azure-websites-managing-change-and-scale
msc.type: authoredcontent
ms.openlocfilehash: c88bae40a8aa092037c0b359ee391acaf161cf10
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78506374"
---
# <a name="hands-on-lab-maintainable-azure-websites-managing-change-and-scale"></a>ハンズオンラボ: メンテナンス可能な Azure Websites: 変更とスケールの管理

[Web キャンプチーム](https://twitter.com/webcamps)別

[Web キャンプトレーニングキットをダウンロードする](https://aka.ms/webcamps-training-kit)

> Microsoft Azure を使用すると、簡単に web サイトを構築して運用環境にデプロイできます。 しかし、アプリケーションが稼働しているときには完了していません。 変化する要件、データベースの更新、スケールなどを処理する必要があります。 幸いにも、サイトの円滑な実行を維持するのに役立つ多くの機能が用意されており、Azure App Service について説明しています。
>
> Azure では、あらゆる規模の web アプリケーションに対して、セキュリティで保護された柔軟な開発、デプロイ、スケーリングのオプションを提供しています。 既存のツールを活用して、インフラストラクチャを管理する手間をかけずにアプリケーションを作成してデプロイします。
>
> お気に入りの開発ツールを使用して作成されたコンテンツを簡単にデプロイできるため、実稼働 web アプリケーションを数分でプロビジョニングできます。 **Git**、 **GitHub**、 **Bitbucket**、 **TFS**、および**DropBox**のサポートを使用して、既存のサイトをソース管理から直接デプロイできます。 Windows の**PowerShell**または任意の OS で実行されている**CLI**ツールを使用して、お気に入りの IDE またはスクリプトから直接デプロイできます。 デプロイが完了したら、継続的なデプロイのサポートによって、サイトを常に最新の状態に保ちます。
>
> Azure は、あらゆるデータに対応したスケーラブルで持続性のあるクラウドストレージ、バックアップ、回復のソリューションを提供します。 アプリケーションを運用環境にデプロイする場合、テーブル、Blob、SQL データベースなどのストレージサービスは、クラウドでのアプリケーションのスケーリングに役立ちます。
>
> SQL データベースでは、アプリケーションの新しいバージョンをデプロイするときに、生産性の高いデータベースを最新の状態に保つことが重要です。 **Entity Framework Code First Migrations**のおかげで、データモデルの開発とデプロイは、数分で環境を更新するために簡略化されています。 このハンズオンラボでは、Microsoft Azure で運用環境に web アプリをデプロイするときに発生する可能性のあるさまざまなトピックを示します。
>
> すべてのサンプルコードとスニペットは、 [https://aka.ms/webcamps-training-kit](https://aka.ms/webcamps-training-kit)で入手できる Web キャンプトレーニングキットに含まれています。
>
> このトピックの詳細については、「 [Azure 電子ブックを使用した実際のクラウドアプリの構築](building-real-world-cloud-apps-with-windows-azure/introduction.md)」を参照してください。

<a id="Overview"></a>
## <a name="overview"></a>概要

<a id="Objectives"></a>
### <a name="objectives"></a>目標

このハンズオンラボでは、次の方法を学習します。

- 既存のモデルを使用して Entity Framework 移行を有効にする
- Entity Framework の移行を使用して、オブジェクトモデルとデータベースを適宜更新する
- Git を使用した Azure App Service へのデプロイ
- Microsoft Azure 管理ポータルを使用して以前のデプロイにロールバックする
- Azure Storage を使用して web アプリをスケールする
- Azure 管理ポータルを使用して web アプリの自動スケールを構成する
- Visual Studio でのロードテストプロジェクトの作成と構成

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>前提条件

このハンズオンラボを完了するには、次のものが必要です。

- [Web 用に2013を Visual Studio Express](https://www.microsoft.com/visualstudio/)
- [Azure SDK for .NET 2.2](https://www.microsoft.com/windowsazure/sdk/)
- [GIT バージョン管理システム](http://git-scm.com/download)
- Microsoft Azure サブスクリプション

    - [無料試用版](https://aka.ms/watk-freetrial)にサインアップする
    - Visual Studio Professional、Test Professional、Premium、または Ultimate with MSDN または MSDN Platforms サブスクライバーであれば、今すぐ[msdn の特典](https://aka.ms/watk-msdn)をアクティブ化して、Azure での開発とテストを開始できます。
    - [Bizspark](https://aka.ms/watk-bizspark)メンバーは、Visual Studio Ultimate with MSDN サブスクリプションを通じて Azure 特典を自動的に受け取ります
    - [Microsoft Partner Network](https://aka.ms/watk-mpn) Cloud Essentials プログラムのメンバーは、毎月 Azure クレジットを無料で受け取ることができます

<a id="Setup"></a>
### <a name="setup"></a>セットアップ

このハンズオンラボの演習を実行するには、まず環境をセットアップする必要があります。

1. エクスプローラーを開き、ラボの**ソース**フォルダーを参照します。
2. **Setup.exe**を右クリックし、 **[管理者として実行]** を選択して、環境を構成し、このラボ用の Visual Studio コードスニペットをインストールするセットアッププロセスを開始します。
3. [ユーザーアカウント制御] ダイアログが表示されている場合は、操作を続行することを確認します。

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

1. [Entity Framework 移行の使用](#Exercise1)
2. [Web アプリをステージングにデプロイする](#Exercise2)
3. [運用環境での配置ロールバックの実行](#Exercise3)
4. [Azure Storage を使用したスケーリング](#Exercise4)
5. [Web Apps に自動スケールを使用する](#Exercise5)(Visual Studio 2013 Ultimate edition では省略可能)

このラボの推定所要時間: **75 分**

> [!NOTE]
> Visual Studio を初めて起動するときに、定義済みの設定コレクションのいずれかを選択する必要があります。 定義済みの各コレクションは、特定の開発スタイルに一致するように設計されており、ウィンドウのレイアウト、エディターの動作、IntelliSense コードスニペット、およびダイアログボックスのオプションを決定します。 このラボの手順では、**全般的な開発設定**のコレクションを使用するときに、Visual Studio で特定のタスクを実行するために必要なアクションについて説明します。 開発環境に対して別の設定コレクションを選択した場合は、注意が必要な手順が異なる場合があります。

<a id="Exercise1"></a>
### <a name="exercise-1-using-entity-framework-migrations"></a>演習 1: Entity Framework の移行の使用

アプリケーションを開発するときに、データモデルが時間の経過と共に変化することがあります。 これらの変更は、データベース内の既存のモデルに影響を与える可能性があります (新しいバージョンを作成している場合)。また、エラーを防ぐために、データベースを最新の状態に保つことが重要です。

モデルにおけるこれらの変更の追跡を簡単にするために、 **Entity Framework Code First Migrations**モデルとデータベーススキーマを比較して変更を自動的に検出し、データベースを更新するための特定のコードを生成して、データベースの新しい*バージョン*を作成します。

この演習では、アプリケーションの**移行**を有効にする方法と、データベースを更新するための変更を簡単に検出して生成する方法について説明します。

<a id="Ex1Task1"></a>
#### <a name="task-1--enabling-migrations"></a>タスク1–移行を有効にする

この実習では、**マニアクイズ**データベースに対して**Entity Framework Code First Migrations**を有効にする手順について説明し、モデルを変更して、変更がデータベースに反映される方法を理解します。

1. Visual Studio を開き、 **Source\Ex1-UsingEntityFrameworkMigrations\Begin**から**GeekQuiz**ソリューションファイルを開きます。
2. **NuGet**パッケージの依存関係をダウンロードしてインストールするために、ソリューションをビルドします。 これを行うには、ソリューションを右クリックし、 **[ソリューションのビルド]** をクリックするか、 **Ctrl + Shift + B**キーを押します。
3. Visual Studio の **[ツール]** メニューで、 **[NuGet パッケージマネージャー]** を選択し、 **[パッケージマネージャーコンソール]** をクリックします。
4. **パッケージマネージャーコンソール**で、次のコマンドを入力**して、enter キーを**押します。 既存のモデルに基づく初期移行が作成されます。

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample1.ps1)]

    ![移行の有効化](maintainable-azure-websites-managing-change-and-scale/_static/image1.png "移行を有効にする")

    *移行の有効化*

    > [!NOTE]
    > このコマンドは、 **Configuration.cs**という名前のファイルを含むマニアクイズプロジェクトに、**移行**フォルダーを追加します。 **構成**クラスを使用すると、コンテキストの移行の動作を構成できます。
5. 移行を有効にした場合、**構成**クラスを更新して、**マニアクイズ**が必要とする初期データをデータベースに設定する必要があります。 **[移行]** で、 **Configuration.cs**ファイルを、このラボの **[source\ Assets]** フォルダーにあるものに置き換えます。

    > [!NOTE]
    > **移行**では、すべてのデータベース更新で**Seed**メソッドが呼び出されるため、データベース内でレコードが複製されないようにする必要があります。 **Addorupdate**メソッドを使用すると、重複するデータを防ぐことができます。
6. 初期移行を追加するには、次のコマンドを入力**して、enter キーを**押します。

    > [!NOTE]
    > LocalDB インスタンスに &quot;GeekQuizProd&quot; という名前のデータベースがないことを確認します。

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample2.ps1)]

    ![ベーススキーマの移行の追加](maintainable-azure-websites-managing-change-and-scale/_static/image2.png "ベーススキーマの移行の追加")

    *ベーススキーマの移行の追加*

    > [!NOTE]
    > **追加移行**では、前回の移行が作成されてからモデルに対して行った変更に基づいて、次の移行がスキャフォールディングされます。 この場合、プロジェクトの最初の移行として、 **TriviaContext**クラスで定義されているすべてのテーブルを作成するスクリプトが追加されます。
7. 次のコマンドを実行して、移行を実行し、データベースを更新します。 このコマンドでは、ターゲットデータベースに適用されている SQL ステートメントを表示する**Verbose**フラグを指定します。

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample3.ps1)]

    ![初期データベースの作成](maintainable-azure-websites-managing-change-and-scale/_static/image3.png "初期データベースの作成")

    *初期データベースの作成*

    > [!NOTE]
    > **更新データベース**では、保留中の移行がデータベースに適用されます。 この場合、web.config ファイルで定義されている接続文字列を使用してデータベースが作成されます。
8. **[表示]** メニューにアクセスして**SQL Server オブジェクトエクスプローラー**を開きます。

    ![SQL Server オブジェクトエクスプローラーで開く](maintainable-azure-websites-managing-change-and-scale/_static/image4.png "SQL Server オブジェクトエクスプローラーで開く")

    *SQL Server オブジェクトエクスプローラーで開く*
9. **[SQL Server オブジェクトエクスプローラー]** ウィンドウで、 **[SQL Server]** ノードを右クリックし、 **[SQL Server の追加]** オプションを選択して、LocalDB インスタンスに接続します。

    ![SQL Server インスタンスの追加](maintainable-azure-websites-managing-change-and-scale/_static/image5.png "SQL Server インスタンスの追加")

    *SQL Server オブジェクトエクスプローラーへの SQL Server インスタンスの追加*
10. **サーバー名**を *(localdb) \ v11.0*に設定し、認証モードとして**Windows 認証**をそのまま使用します。 **[接続]** をクリックして続行します。

    ![LocalDB に接続しています](maintainable-azure-websites-managing-change-and-scale/_static/image6.png "LocalDB に接続しています")

    *LocalDB に接続しています*
11. **GeekQuizProd**データベースを開き、 **[テーブル]** ノードを展開します。 ご覧のように、 **TriviaContext**クラスで定義されているすべてのテーブルが、**データベースの更新**コマンドによって生成されました。 Dbo を見つけ**ます。TriviaQuestions**テーブルを開き、[列] ノードを開きます。 次のタスクでは、このテーブルに新しい列を追加し、**移行**を使用してデータベースを更新します。

    ![トリビアの質問列](maintainable-azure-websites-managing-change-and-scale/_static/image7.png "トリビアの質問列")

    *トリビアの質問列*

<a id="Ex1Task2"></a>
#### <a name="task-2--updating-database-schema-using-migrations"></a>タスク2–移行を使用してデータベーススキーマを更新する

このタスクでは、 **Entity Framework Code First Migrations**を使用して、モデルの変更を検出し、データベースを更新するために必要なコードを生成します。 **TriviaQuestions**エンティティを更新するには、新しいプロパティを追加します。 次に、コマンドを実行して新しい移行を作成し、新しい列をテーブルに含めます。

1. **ソリューションエクスプローラー**で、 **[モデル]** フォルダー内にある**TriviaQuestion.cs**ファイルをダブルクリックします。
2. 次のコードスニペットに示すように、**ヒント**という名前の新しいプロパティを追加します。

    [!code-csharp[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample4.cs)]
3. **パッケージマネージャーコンソール**で、次のコマンドを入力**して、enter キーを**押します。 モデルの変更を反映した新しい移行が作成されます。

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample5.ps1)]

    ![移行の追加](maintainable-azure-websites-managing-change-and-scale/_static/image8.png "Add-Migration")

    *移行の追加*

    > [!NOTE]
    > 移行ファイルは、**上下**に2つの方法で構成さ**れてい**ます。
    >
    > - **Up**メソッドは、アプリケーションの現在のバージョンがデータベースに適用する必要がある変更を指定するために使用されます。
    > - **Down**は、 **Up**メソッドに追加した変更を元に戻すために使用されます。
    >
    > データベースの移行によってデータベースが更新されると、すべての移行がタイムスタンプの順序で実行され、最後の更新以降に使用されていないもののみが実行されます (\_MigrationHistory テーブルは、適用されている移行を追跡します)。 すべての移行の**Up**メソッドが呼び出され、指定した変更がデータベースに対して行われます。 前の移行に戻る場合は、逆の順序で変更を再実行するために**Down**メソッドが呼び出されます。
4. **パッケージマネージャーコンソール**で、次のコマンドを入力**して、enter キーを**押します。

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample6.ps1)]
5. 次の図に示すように、 **TriviaQuestions**テーブルに新しい列を追加するために、**データベースの更新**コマンドの出力で**Alter Table** SQL ステートメントが生成されました。

    ![列の追加 SQL ステートメントが生成されました](maintainable-azure-websites-managing-change-and-scale/_static/image9.png "列の追加 SQL ステートメントが生成されました")

    *列の追加 SQL ステートメントが生成されました*
6. **SQL Server オブジェクトエクスプローラー**で、dbo を更新し**ます。TriviaQuestions**テーブルを作成し、新しい**ヒント**列が表示されていることを確認します。

    ![新しいヒント列を表示しています](maintainable-azure-websites-managing-change-and-scale/_static/image10.png "新しいヒント列を表示しています")

    *新しいヒント列を表示しています*
7. 次のコードスニペットに示すように、 **TriviaQuestion.cs**エディターに戻り、 *Hint*プロパティに**stringlength**制約を追加します。

    [!code-csharp[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample7.cs)]
8. **パッケージマネージャーコンソール**で、次のコマンドを入力**して、enter キーを**押します。

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample8.ps1)]
9. **パッケージマネージャーコンソール**で、次のコマンドを入力**して、enter キーを**押します。

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample9.ps1)]
10. 次の図に示すように、 **TriviaQuestions**テーブルの*ヒント*列の型を更新するために、**データベースの更新**コマンドの出力で**Alter table** SQL ステートメントが生成されました。

    ![Alter column SQL ステートメントが生成されました](maintainable-azure-websites-managing-change-and-scale/_static/image11.png "Alter column SQL ステートメントが生成されました")

    *Alter column SQL ステートメントが生成されました*
11. **SQL Server オブジェクトエクスプローラー**で、dbo を更新し**ます。TriviaQuestions**テーブルを確認し、**ヒント**列の型が**nvarchar (150)** であることを確認します。

    ![新しい制約を表示しています](maintainable-azure-websites-managing-change-and-scale/_static/image12.png "新しい制約を表示しています")

    *新しい制約を表示しています*

<a id="Exercise2"></a>
### <a name="exercise-2-deploying-a-web-app-to-staging"></a>演習 2: ステージングへの Web アプリのデプロイ

**Azure App Service の Web Apps**を使用すると、ステージングされた発行を実行できます。 ステージングされた発行では、既定の運用サイトごとにステージングサイトスロットを作成し、ダウンタイムなしでこれらのスロットを交換できるようにします。 これは、パブリックにリリースする前に変更を検証し、サイトコンテンツを段階的に統合し、変更が期待どおりに機能していない場合はロールバックするのに非常に役立ちます。

この演習では、Git ソース管理を使用して、web アプリのステージング環境に**マニアクイズ**アプリケーションをデプロイします。 これを行うには、web アプリを作成し、必要なコンポーネントを管理ポータルでプロビジョニングします。次に、 **Git**リポジトリを構成し、ローカルコンピューターからステージングスロットにアプリケーションのソースコードをプッシュします。 また、前の演習で作成した**Code First Migrations**を使用して、実稼働データベースを更新します。 次に、このテスト環境でアプリケーションを実行して、その操作を確認します。 期待どおりに動作していることを確認したら、アプリケーションを運用環境に昇格させます。

> [!NOTE]
> ステージングされた発行を有効にするには、web アプリが**標準モード**である必要があります。 Web アプリを標準モードに変更すると、追加料金が発生することに注意してください。 価格の詳細については、「 [App Service の価格](https://azure.microsoft.com/pricing/details/app-service/)」を参照してください。

<a id="Ex2Task1"></a>
#### <a name="task-1--creating-a-web-app-in-azure-app-service"></a>タスク1– Azure App Service で Web アプリを作成する

このタスクでは、管理ポータルから**Azure App Service**で web アプリを作成します。 また、 **SQL Database**を構成して、アプリケーションデータを永続化し、ソース管理用のローカル Git リポジトリを構成します。

1. [Azure 管理ポータル](https://manage.windowsazure.com)にアクセスし、サブスクリプションに関連付けられている Microsoft アカウントを使用してサインインします。

    ![Microsoft Azure 管理ポータルにサインインします。](maintainable-azure-websites-managing-change-and-scale/_static/image13.png)

    *Microsoft Azure 管理ポータルにサインインします。*
2. ページの下部にあるコマンドバーで **[新規]** をクリックします。

    ![新しい web アプリの作成](maintainable-azure-websites-managing-change-and-scale/_static/image14.png "新しい web アプリの作成")

    *新しい web アプリの作成*
3. **[Compute]** 、 **[web サイト]** 、 **[カスタム作成]** の順にクリックします。

    ![カスタム作成を使用した新しい web アプリの作成](maintainable-azure-websites-managing-change-and-scale/_static/image15.png "カスタム作成を使用した新しい web アプリの作成")

    *カスタム作成を使用した新しい web アプリの作成*
4. **[新しい Web サイト-カスタム作成]** ダイアログボックスで、使用可能な**URL** (例:*マニア*) を指定し、 **[リージョン]** ボックスの一覧で場所を選択し、 **[データベース]** ボックスの一覧で **[新しい SQL データベースを作成する]** を選択します。 最後に、 **[ソース管理から発行]** する チェックボックスをオンにし、 **[次へ]** をクリックします。

    ![新しい web アプリのカスタマイズ](maintainable-azure-websites-managing-change-and-scale/_static/image16.png)

    *新しい web アプリのカスタマイズ*
5. データベースの設定に関する次の情報を指定します。

   - **[名前]** テキストボックスに、データベース名 (例: *geekquiz\_db*) を入力します。
   - [サーバー **] ドロップダウン**リストで、 **[新しい SQL データベースサーバー]** を選択します。 または、既存のサーバーを選択することもできます。
   - **[データベースのユーザー名]** ボックスと **[データベースパスワード]** ボックスに、SQL データベースサーバーの管理者のユーザー名とパスワードを入力します。 既に作成してあるサーバーを選択した場合は、パスワードの入力を求めるメッセージが表示されます。

     ![データベースの設定の指定](maintainable-azure-websites-managing-change-and-scale/_static/image17.png)

     *データベースの設定の指定*
6. **[次へ]** をクリックして次に進みます。
7. 使用するソース管理の **[ローカル Git リポジトリ]** を選択し、 **[次へ]** をクリックします。

    > [!NOTE]
    > デプロイ資格情報 (ユーザー名とパスワード) の入力を求められる場合があります。

    ![Git リポジトリの作成](maintainable-azure-websites-managing-change-and-scale/_static/image18.png)

    *Git リポジトリの作成*
8. 新しい web アプリが作成されるまで待ちます。

    > [!NOTE]
    > 既定では、Azure は*azurewebsites.net*にドメインを提供しますが、azure 管理ポータルを使用してカスタムドメインを設定することもできます。 ただし、特定の Azure App Service モードを使用している場合にのみ、カスタムドメインを管理できます。
    >
    > Azure App Service は、Free、Shared、Basic、Standard、および Premium の各エディションで使用できます。 無料モードと共有モードでは、すべての web アプリがマルチテナント環境で実行され、CPU、メモリ、およびネットワーク使用率のクォータがあります。 無料アプリの最大数は、プランによって異なる場合があります。 標準モードでは、標準の Azure コンピューティングリソースに対応する専用の仮想マシンで実行されるアプリを選択します。 Web アプリモードの構成は、web アプリの **[スケール]** メニューで確認できます。
    >
    > ![Azure App Service モード](maintainable-azure-websites-managing-change-and-scale/_static/image19.png "Azure App Service モード")
    >
    > **共有**モードまたは**標準**モードを使用している場合は、アプリの **[構成]** メニューに移動し、[*ドメイン名*] の **[ドメインの管理]** をクリックすることで、web アプリのカスタムドメインを管理できます。
    >
    > ![ドメインの管理](maintainable-azure-websites-managing-change-and-scale/_static/image20.png "ドメインの管理")
    >
    > ![カスタムドメインの管理](maintainable-azure-websites-managing-change-and-scale/_static/image21.png "カスタムドメインの管理")
9. Web アプリが作成されたら、 **[URL]** 列の下のリンクをクリックして、新しい web アプリが実行されていることを確認します。

    ![新しい web アプリを参照しています](maintainable-azure-websites-managing-change-and-scale/_static/image22.png)

    *新しい web アプリを参照しています*

    ![実行中の web アプリ](maintainable-azure-websites-managing-change-and-scale/_static/image23.png)

    *実行中の web アプリ*

<a id="Ex2Task2"></a>
#### <a name="task-2--creating-the-production-sql-database"></a>タスク2–運用 SQL Database を作成する

このタスクでは、 **Entity Framework Code First Migrations**を使用して、前の作業で作成した**Azure SQL Database**インスタンスを対象とするデータベースを作成します。

1. 管理ポータルで、前のタスクで作成した web アプリに移動し、**ダッシュボード**に移動します。
2. **[ダッシュボード]** ページで、 **[概要] セクションの** **[接続文字列の表示]** リンクをクリックします。

    ![接続文字列の表示](maintainable-azure-websites-managing-change-and-scale/_static/image24.png "接続文字列の表示")

    *接続文字列の表示*
3. **[接続文字列]** の値をコピーして、ダイアログボックスを閉じます。

    ![Azure 管理ポータルの接続文字列](maintainable-azure-websites-managing-change-and-scale/_static/image25.png "Azure 管理ポータルの接続文字列")

    *Azure 管理ポータルの接続文字列*
4. **[Sql データベース]** をクリックして、Azure 内の sql データベースの一覧を表示します。

    ![SQL Database メニュー](maintainable-azure-websites-managing-change-and-scale/_static/image26.png "SQL Database メニュー")

    *SQL Database メニュー*
5. 前のタスクで作成したデータベースを見つけて、サーバーをクリックします。

    ![SQL Database サーバー](maintainable-azure-websites-managing-change-and-scale/_static/image27.png "SQL Database サーバー")

    *SQL Database サーバー*
6. サーバーの **[クイックスタート]** ページで、 **[構成]** をクリックします。

    ![[構成] メニュー](maintainable-azure-websites-managing-change-and-scale/_static/image28.png "[構成] メニュー")

    *[構成] メニュー*
7. [**許可さ**れた ip アドレス] セクションで、[**許可された Ip アドレスに追加**する] リンクをクリックして、ip が SQL Database サーバーに接続できるようにします。

    ![使用できる IP アドレス](maintainable-azure-websites-managing-change-and-scale/_static/image29.png "許可された IP アドレス")

    *使用できる IP アドレス*
8. ページの下部にある **[保存]** をクリックして、手順を完了します。
9. Visual Studio に戻ります。
10. **パッケージマネージャーコンソール**で、次のコマンドを実行します。 *[your-CONNECTION-STRING]* プレースホルダーを、Azure からコピーした接続文字列に置き換えます。

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample10.ps1)]

    ![Windows Azure SQL Database を対象とするデータベースの更新](maintainable-azure-websites-managing-change-and-scale/_static/image30.png "Windows Azure SQL Database を対象とするデータベースの更新")

    *データベースターゲットの更新 Azure SQL Database*

<a id="Ex2Task3"></a>
#### <a name="task-3--deploying-geek-quiz-to-staging-using-git"></a>タスク3– Git を使用してマニアクイズをステージングにデプロイする

このタスクでは、web アプリでステージングされた発行を有効にします。 次に、Git を使用して、ローカルコンピューターから web アプリのステージング環境にマニアクイズアプリケーションを直接発行します。

1. ポータルに戻り、 **[名前]** 列の下にある web アプリの名前をクリックして、管理ページを表示します。

    ![Web アプリ管理ページを開く](maintainable-azure-websites-managing-change-and-scale/_static/image31.png)

    *Web アプリ管理ページを開く*
2. **[スケール]** ページに移動します。 **[全般]** セクションで、構成の **[標準]** を選択し、コマンドバーの **[保存]** をクリックします。

    > [!NOTE]
    > 現在のリージョンとサブスクリプションのすべての web アプリを**標準**モードで実行するには、 **[サイトの選択]** 構成で **[すべて選択**] チェックボックスをオンのままにします。 それ以外の場合は、 **[すべて選択**] チェックボックスをオフにします。

    ![Web アプリを標準モードにアップグレードする](maintainable-azure-websites-managing-change-and-scale/_static/image32.png "Web アプリを標準モードにアップグレードする")

    *Web アプリを標準モードにアップグレードする*
3. **[はい]** をクリックして変更を確定します。

    ![標準モードへの変更を確認しています](maintainable-azure-websites-managing-change-and-scale/_static/image33.png "Web アプリモードの変更を続行しています")

    *標準モードへの変更を確認しています*
4. **[ダッシュボード]** ページにアクセスし、[概要 **] セクションの**ステージングされた **[発行を有効にする]** をクリックします。

    ![ステージングされる発行の有効化](maintainable-azure-websites-managing-change-and-scale/_static/image34.png "ステージングされる発行の有効化")

    *ステージングされる発行の有効化*
5. **[はい]** をクリックしてステージングされた発行を有効にします。

    ![ステージングされる発行の確認](maintainable-azure-websites-managing-change-and-scale/_static/image35.png "[はい] をクリックしてステージングされる発行を有効にする")

    *ステージングされる発行の確認*
6. Web アプリの一覧で、web アプリ名の左側にあるマークを展開し、ステージングサイトスロットを表示します。 これには、web アプリの名前の後に ***(ステージング)*** が続きます。 [ステージングサイト] をクリックして、管理ページにアクセスします。

    ![ステージング web アプリへの移動](maintainable-azure-websites-managing-change-and-scale/_static/image36.png "ステージング web アプリへの移動")

    *ステージングアプリへの移動*
7. 管理ページは他の web アプリの管理ページのように見えます。 **[デプロイ]** ページに移動し、 **[Git URL]** の値をコピーします。 この演習では、後で使用します。

    ![Git URL 値をコピーしています](maintainable-azure-websites-managing-change-and-scale/_static/image37.png)

    *Git URL 値をコピーしています*
8. 新しい**Git Bash**コンソールを開き、次のコマンドを実行します。 このラボの**Source\Ex1-DeployingWebSiteToStaging\Begin**フォルダーにある**GeekQuiz**ソリューションへのパスを使用して、 *[your-APPLICATION-path]* プレースホルダーを更新します。

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample11.cmd)]

    ![Git 初期化と最初のコミット](maintainable-azure-websites-managing-change-and-scale/_static/image38.png)

    *Git 初期化と最初のコミット*
9. 次のコマンドを実行して、web アプリをリモート**Git**リポジトリにプッシュします。 プレースホルダーは、管理ポータルから取得した URL に置き換えてください。 デプロイパスワードを入力するように求められます。

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample12.cmd)]

    ![Windows Azure へのプッシュ](maintainable-azure-websites-managing-change-and-scale/_static/image39.png)

    *Azure へのプッシュ*

    > [!NOTE]
    > Web アプリの FTP ホストまたは GIT リポジトリにコンテンツをデプロイする場合は、web アプリの **[クイックスタート]** または **[ダッシュボード]** 管理ページから作成した**デプロイ資格情報**を使用して認証する必要があります。 デプロイ資格情報がわからない場合は、管理ポータルを使用して簡単にリセットできます。 Web アプリの**ダッシュボード**ページを開き、 **[デプロイ資格情報のリセット]** リンクをクリックします。 新しいパスワードを入力し、[ **OK]** をクリックします。 デプロイ資格情報は、サブスクリプションに関連付けられているすべての web アプリで使用できます。
10. Web アプリが Azure に正常にプッシュされたことを確認するには、管理ポータルに戻り、 **[Web サイト]** をクリックします。
11. Web アプリを検索し、エントリを展開してステージングサイトスロットを表示します。 **[名前]** をクリックして、管理ページにアクセスします。
12. **デプロイの履歴**を表示するには、 **[デプロイ]** をクリックします。 *&quot;の初期コミット&quot;* で**アクティブなデプロイ**があることを確認します。

    ![アクティブな配置](maintainable-azure-websites-managing-change-and-scale/_static/image40.png)

    *アクティブな配置*
13. 最後に、コマンドバーの **[参照]** をクリックして、web アプリに移動します。

    ![Web アプリの参照](maintainable-azure-websites-managing-change-and-scale/_static/image41.png)

    *Web アプリの参照*
14. アプリケーションが正常にデプロイされた場合は、マニアクイズログインページが表示されます。

    > [!NOTE]
    > デプロイされたアプリケーションのアドレス URL には、web アプリの名前と*ステージング*が含まれます。

    ![ステージング環境で実行されているアプリケーション](maintainable-azure-websites-managing-change-and-scale/_static/image42.png)

    *ステージング環境で実行されているアプリケーション*
15. アプリケーションを調査する場合は、 **[登録]** をクリックして新しいユーザーを登録します。 ユーザー名、電子メールアドレス、パスワードを入力して、アカウントの詳細を入力します。 次に、アプリケーションはクイズの最初の質問を表示します。 いくつかの質問に答えて、想定どおりに動作していることを確認してください。

    ![使用する準備ができているアプリケーション](maintainable-azure-websites-managing-change-and-scale/_static/image43.png)

    *使用する準備ができているアプリケーション*

<a id="Ex2Task4"></a>
#### <a name="task-4--promoting-the-web-app-to-production"></a>タスク 4-Web アプリを運用環境に昇格する

これで、web アプリがステージング環境で正常に動作していることを確認できたので、運用環境に昇格させることができます。 このタスクでは、ステージングサイトスロットと運用サイトスロットをスワップします。

1. 管理ポータルに戻り、ステージングサイトスロットを選択します。 コマンドバーの **[スワップ]** をクリックします。

    ![運用環境に切り替える](maintainable-azure-websites-managing-change-and-scale/_static/image44.png)

    *運用環境に切り替える*
2. 確認ダイアログボックスで **[はい]** をクリックして、スワップ操作を続行します。 Azure では、運用サイトのコンテンツとステージングサイトのコンテンツが即座に交換されます。

    > [!NOTE]
    > ステージングバージョンの一部の設定は、自動的に運用バージョン (接続文字列の上書き、ハンドラーマッピングなど) にコピーされますが、その他の設定は変更されません (DNS エンドポイント、SSL バインドなど)。

    ![スワップ操作を確認しています](maintainable-azure-websites-managing-change-and-scale/_static/image45.png)

    *スワップ操作を確認しています*
3. スワップが完了したら、運用スロットを選択し、コマンドバーの **[参照]** をクリックして運用サイトを開きます。 アドレスバーに URL が表示されていることを確認します。

    > [!NOTE]
    > キャッシュをクリアするには、ブラウザーを更新する必要がある場合があります。 Internet Explorer では、CTRL キーを押し**ながら R**キーを押すと、この操作を行うことができます。

    ![運用環境で実行されている Web アプリ](maintainable-azure-websites-managing-change-and-scale/_static/image46.png)
4. **GitBash**コンソールで、ローカル Git リポジトリのリモート URL を更新して、運用スロットを対象にします。 これを行うには、次のコマンドを実行します。プレースホルダーは、デプロイユーザー名と web アプリの名前に置き換えてください。

    > [!NOTE]
    > 次の演習では、ラボを簡単にするためだけに、ステージングではなく運用サイトに変更をプッシュします。 実際のシナリオでは、運用環境に昇格する前にステージング環境の変更を確認することをお勧めします。

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample13.cmd)]

<a id="Exercise3"></a>
### <a name="exercise-3-performing-deployment-rollback-in-production"></a>演習 3: 運用環境で展開のロールバックを実行する

ステージングと運用の間でホットスワップを実行するステージングスロットがない場合 (たとえば、 **Free**モードまたは**共有**モードを使用している場合)。 これらのシナリオでは、実稼働環境に配置する前に、ローカルまたはリモートサイトでテスト環境でアプリケーションをテストする必要があります。 ただし、テストフェーズ中に検出されない問題が運用サイトで発生する可能性があります。 この場合、できるだけ早く、より安定したバージョンのアプリケーションに簡単に切り替えるメカニズムを用意することが重要です。

**Azure App Service**では、ソース管理からの継続的なデプロイによって、管理ポータルで使用できる再**デプロイ**アクションが発生します。 Azure では、リポジトリにプッシュされたコミットに関連付けられているデプロイを追跡し、いつでも以前のデプロイを使用してアプリケーションを再デプロイするオプションを提供します。

この演習では、*バグ*を意図的に挿入する**マニアクイズ**アプリケーションのコードに変更を行います。 アプリケーションを運用環境にデプロイしてエラーを確認した後、再デプロイ機能を利用して前の状態に戻ります。

<a id="Ex3Task1"></a>
#### <a name="task-1--updating-the-geek-quiz-application"></a>タスク1–マニアクイズアプリケーションを更新する

このタスクでは、 **TriviaController**クラスの小さな部分のコードをリファクターして、選択したクイズオプションをデータベースから新しいメソッドに取得するロジックの一部を抽出します。

1. 前の演習で**GeekQuiz**ソリューションを使用して Visual Studio インスタンスに切り替えます。
2. **ソリューションエクスプローラー**で、 **Controllers**フォルダー内の**TriviaController.cs**ファイルを開きます。
3. **StoreAsync**メソッドを見つけて、次の図で強調表示されているコードを選択します。

    ![コードの選択](maintainable-azure-websites-managing-change-and-scale/_static/image47.png)

    *コードの選択*
4. 選択したコードを右クリックし、 **[リファクター]** メニューを展開して **[メソッドの抽出...]** を選択します。

    ![新しいメソッドとしてのコードの抽出](maintainable-azure-websites-managing-change-and-scale/_static/image48.png)

    *Extract メソッドの選択*
5. **[メソッドの抽出]** ダイアログボックスで、新しいメソッドに*MatchesOption*という名前を指定し、[ **OK]** をクリックします。

    ![メソッド名の指定](maintainable-azure-websites-managing-change-and-scale/_static/image49.png)

    *抽出されたメソッドの名前を指定する*
6. 次に、選択したコードを**MatchesOption**メソッドに抽出します。 結果のコードは、次のスニペットに示されています。

    [!code-csharp[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample14.cs)]
7. **CTRL + S**キーを押して、変更を保存します。

<a id="Ex3Task2"></a>
#### <a name="task-2--redeploying-the-geek-quiz-application"></a>タスク2–マニアクイズアプリケーションを再展開する

次に、前のタスクで行った変更をリポジトリにプッシュします。これにより、運用環境への新しいデプロイがトリガーされます。 次に、Internet Explorer に用意されている**F12 開発ツール**を使用して問題を解決してから、Azure 管理ポータルから以前のデプロイへのロールバックを実行します。

1. 新しい**Git Bash**コンソールを開き、Azure App Service に更新されたアプリケーションをデプロイします。
2. 次のコマンドを実行して、変更を Azure にプッシュします。 **GeekQuiz**ソリューションへのパスを使用して、 *[your-APPLICATION-path]* プレースホルダーを更新します。 デプロイパスワードを入力するように求められます。

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample15.cmd)]

    ![リファクタリングされるコードを Azure にプッシュする](maintainable-azure-websites-managing-change-and-scale/_static/image50.png)

    *リファクタリングされるコードを Azure にプッシュする*
3. Internet Explorer を開き、web アプリに移動します (例: `http://<your-web-site>.azurewebsites.net`)。 以前に作成した資格情報を使用してログインします。
4. **F12**キーを押して開発ツールを起動し、 **[ネットワーク]** タブを選択し、 **[再生]** ボタンをクリックして記録を開始します。

    ![ネットワーク記録の開始](maintainable-azure-websites-managing-change-and-scale/_static/image51.png "ネットワーク記録の開始")

    *ネットワーク記録の開始*
5. クイズの任意のオプションを選択します。 何も起こらないことがわかります。
6. **F12**ウィンドウで、POST http 要求に対応するエントリに http **500**の結果が表示されます。

    ![HTTP 500 エラー](maintainable-azure-websites-managing-change-and-scale/_static/image52.png)

    *HTTP 500 エラー*
7. **[コンソール]** タブを選択します。エラーは、原因の詳細と共に記録されます。

    ![ログに記録されたエラー](maintainable-azure-websites-managing-change-and-scale/_static/image53.png)

    *ログに記録されたエラー*
8. エラーの詳細部分を見つけます。 明らかに、このエラーは、前の手順でコミットしたコードリファクタリングが原因で発生します。

    [https://login.microsoftonline.com/consumers/](`Details: LINQ to Entities does not recognize the method 'Boolean MatchesOption ...`)
9. ブラウザーを閉じないでください。
10. 新しいブラウザーインスタンスで、 [Azure 管理ポータル](https://manage.windowsazure.com)に移動し、サブスクリプションに関連付けられている Microsoft アカウントを使用してサインインします。
11. **[Web サイト]** を選択し、演習2で作成した web アプリをクリックします。
12. **[デプロイ]** ページに移動します。 実行されたすべてのコミットがデプロイ履歴に表示されていることに注意してください。

    ![既存の展開の一覧](maintainable-azure-websites-managing-change-and-scale/_static/image54.png)

    *既存の展開の一覧*
13. 以前のコミットを選択し、コマンドバーの [再**デプロイ**] をクリックします。

    ![前回のコミットの再デプロイ](maintainable-azure-websites-managing-change-and-scale/_static/image55.png)

    *前回のコミットの再デプロイ*
14. 確認メッセージが表示されたら、 **[はい]** をクリックします。

    ![再展開の確認](maintainable-azure-websites-managing-change-and-scale/_static/image56.png)
15. デプロイが完了したら、web アプリでブラウザーインスタンスに戻り、Ctrl キーを押し**ながら F5**キーを押します。
16. いずれかのオプションをクリックします。 フリップアニメーションが表示されるようになり、結果 (*正しい/正しくない*) が表示されます。
17. Optional**Git Bash**コンソールに切り替え、次のコマンドを実行して前のコミットに戻します。

    > [!NOTE]
    > これらのコマンドは、無効なコミットで作成された Git リポジトリ内のすべての変更を元に戻す新しいコミットを作成します。 その後、Azure は新しいコミットを使用してアプリケーションを再デプロイします。

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample16.cmd)]

<a id="Exercise4"></a>
### <a name="exercise-4-scaling-using-azure-storage"></a>演習 4: Azure Storage を使用したスケーリング

**Blob**は、大量の非構造化テキストまたはバイナリデータ (ビデオ、オーディオ、画像など) を格納する最も簡単な方法です。 アプリケーションの静的コンテンツをストレージに移行することで、イメージまたはドキュメントを直接ブラウザーに提供してアプリケーションを拡張できます。

この演習では、アプリケーションの静的コンテンツを Blob コンテナーに移動します。 次に、コンテンツを Blob コンテナーに**リダイレクトするために、** web.config で**ASP.NET URL 書き換えルール**を追加するようにアプリケーションを構成します。

<a id="Ex4Task1"></a>
#### <a name="task-1--creating-an-azure-storage-account"></a>タスク1– Azure Storage アカウントを作成する

このタスクでは、管理ポータルを使用して新しいストレージアカウントを作成する方法について説明します。

1. [Azure 管理ポータル](https://manage.windowsazure.com)に移動し、サブスクリプションに関連付けられている Microsoft アカウントを使用してサインインします。
2. 新規 を選択します。 **Data Services |Storage |簡易作成**を実行して、新しいストレージアカウントの作成を開始します。 アカウントの一意の名前を入力し、一覧から**リージョン**を選択します。 **[ストレージアカウントの作成]** をクリックして続行します。

    ![新しいストレージアカウントを作成する](maintainable-azure-websites-managing-change-and-scale/_static/image57.png "新しいストレージアカウントを作成する")

    *新しいストレージアカウントを作成する*
3. **[ストレージ]** セクションで、新しいストレージアカウントの状態が [*オンライン*] に変わるまで待ってから、次の手順に進みます。

    ![作成されたストレージアカウント](maintainable-azure-websites-managing-change-and-scale/_static/image58.png "作成されたストレージアカウント")

    *作成されたストレージアカウント*
4. ストレージアカウント名をクリックし、ページの上部にある **[ダッシュボード]** リンクをクリックします。 **[ダッシュボード]** ページには、アカウントの状態と、アプリケーション内で使用できるサービスエンドポイントに関する情報が表示されます。

    ![ストレージアカウントダッシュボードの表示](maintainable-azure-websites-managing-change-and-scale/_static/image59.png "ストレージアカウントダッシュボードの表示")

    *ストレージアカウントダッシュボードの表示*
5. ナビゲーションバーの **[アクセスキーの管理]** ボタンをクリックします。

    ![[アクセスキーの管理] ボタン](maintainable-azure-websites-managing-change-and-scale/_static/image60.png "[アクセスキーの管理] ボタン")

    *[アクセスキーの管理] ボタン*
6. **[アクセスキーの管理]** ダイアログボックスで、**ストレージアカウント名**と**プライマリアクセスキー**をコピーします。次の演習で必要になります。 次に、ダイアログボックスを閉じます。

    ![[アクセスキーの管理] ダイアログボックス](maintainable-azure-websites-managing-change-and-scale/_static/image61.png "[アクセスキーの管理] ダイアログボックス")

    *[アクセスキーの管理] ダイアログボックス*

<a id="Ex4Task2"></a>
#### <a name="task-2--uploading-an-asset-to-azure-blob-storage"></a>タスク2– Azure Blob Storage に資産をアップロードする

このタスクでは、Visual Studio の [サーバーエクスプローラー] ウィンドウを使用して、ストレージアカウントに接続します。 次に、blob コンテナーを作成し、マニアクイズロゴを含むファイルをコンテナーにアップロードします。

1. 前の演習で**GeekQuiz**ソリューションを使用して Visual Studio インスタンスに切り替えます。
2. メニューバーから **[表示]** を選択し、 **[サーバーエクスプローラー]** をクリックします。
3. **サーバーエクスプローラー**で、 **[azure]** ノードを右クリックし、 **[azure に接続]** を選択します。サブスクリプションに関連付けられている Microsoft アカウントを使用してサインインします。

    ![Windows Azure へ接続](maintainable-azure-websites-managing-change-and-scale/_static/image62.png)

    *Azure への接続*
4. **[Azure]** ノードを展開し、 **[ストレージ]** を右クリックして、 **[外部ストレージの接続]** を選択します。
5. **[新しいストレージアカウントの追加]** ダイアログボックスで、前のタスクで取得した**アカウント名**と**アカウントキー**を入力し、 **[OK]** をクリックします。

    ![[新しいストレージアカウントの追加] ダイアログボックス](maintainable-azure-websites-managing-change-and-scale/_static/image63.png)

    *[新しいストレージアカウントの追加] ダイアログボックス*
6. ストレージ**ノードの下にストレージ**アカウントが表示されます。 ストレージアカウントを展開し、 **[blob]** を右クリックして、 **[Blob コンテナーの作成...]** を選択します。

    ![Blob コンテナーの作成](maintainable-azure-websites-managing-change-and-scale/_static/image64.png "BLOB コンテナーの作成")

    *Blob コンテナーの作成*
7. **[Blob コンテナーの作成]** ダイアログボックスで、blob コンテナーの名前を入力し、[ **OK]** をクリックします。

    ![[Blob コンテナーの作成] ダイアログボックス](maintainable-azure-websites-managing-change-and-scale/_static/image65.png "[Blob コンテナーの作成] ダイアログボックス")

    *[Blob コンテナーの作成] ダイアログボックス*
8. 新しい blob コンテナーを**blob**ノードに追加する必要があります。 コンテナーのアクセス許可を変更して、コンテナーをパブリックにします。 これを行うには、 **images**コンテナーを右クリックし、 **[プロパティ]** を選択します。

    ![images コンテナーのプロパティ](maintainable-azure-websites-managing-change-and-scale/_static/image66.png "images コンテナーのプロパティ")

    *Images コンテナーのプロパティ*
9. **[プロパティ]** ウィンドウで、 **[パブリック読み取りアクセス]** を **[コンテナー]** に設定します。

    ![パブリック読み取りアクセスプロパティの変更](maintainable-azure-websites-managing-change-and-scale/_static/image67.png "パブリック読み取りアクセスプロパティの変更")

    *パブリック読み取りアクセスプロパティの変更*
10. パブリックアクセスプロパティを変更するかどうかを確認するメッセージが表示されたら、 **[はい]** をクリックします。

    ![Microsoft Visual Studio 警告](maintainable-azure-websites-managing-change-and-scale/_static/image68.png "Microsoft Visual Studio 警告")

    *Microsoft Visual Studio 警告*
11. **サーバーエクスプローラー**で、 **images** blob コンテナー内を右クリックし、 **[blob コンテナーの表示]** を選択します。

    ![Blob コンテナーの表示](maintainable-azure-websites-managing-change-and-scale/_static/image69.png "Blob コンテナーの表示")

    *Blob コンテナーの表示*
12. 新しいウィンドウで images コンテナーが開き、エントリのない凡例が表示されます。 **アップロード**アイコンをクリックして、ファイルを blob コンテナーにアップロードします。

    ![エントリのないイメージコンテナー](maintainable-azure-websites-managing-change-and-scale/_static/image70.png "エントリのないイメージコンテナー")

    *エントリのないイメージコンテナー*
13. **[Blob のアップロード]** ダイアログボックスで、ラボの**Assets**フォルダーに移動します。 **Logo-big**ファイルを選択し、 **[開く]** をクリックします。
14. ファイルがアップロードされるまで待ちます。 アップロードが完了すると、[images] コンテナーにファイルが表示されます。 ファイルエントリを右クリックし、 **[URL のコピー]** を選択します。

    ![Blob URL のコピー](maintainable-azure-websites-managing-change-and-scale/_static/image71.png "Blob ファイルの URL のコピー")

    *Blob URL のコピー*
15. Internet Explorer を開き、URL を貼り付けます。 次の画像がブラウザーに表示されます。

    ![Windows Blob Storage からの logo-big イメージ](maintainable-azure-websites-managing-change-and-scale/_static/image72.png "ストレージからの logo-big イメージ")

    *Azure Blob Storage からの logo-big イメージ*

<a id="Ex4Task3"></a>
#### <a name="task-3--updating-the-solution-to-consume-static-content-from-azure-blob-storage"></a>タスク3– Azure Blob Storage からの静的コンテンツを使用するようにソリューションを更新する

このタスクでは、 **web.config ファイルに**ASP.NET URL 書き換えルールを追加することによって、(web アプリに存在するイメージではなく) Azure Blob Storage にアップロードされたイメージを使用するように**GeekQuiz**ソリューションを構成します。

1. Visual Studio で、 **GeekQuiz**プロジェクト**内の web.config ファイルを**開き、 **&lt;system.webserver&gt;** 要素を見つけます。
2. 次のコードを追加して、URL 書き換えルールを追加し、プレースホルダーをストレージアカウント名で更新します。

    (コードスニペット- *webEx4-UrlRewriteRule*)

    [!code-xml[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample17.xml)]

    > [!NOTE]
    > URL 書き換えは、受信 Web 要求をインターセプトし、要求を別のリソースにリダイレクトするプロセスです。 URL 書き換え規則は、要求をリダイレクトする必要がある場合や、要求をリダイレクトする必要がある場合に、リライトエンジンに通知します。 書き換え規則は2つの文字列で構成されます。要求された URL で検索するパターン (通常は正規表現を使用) と、パターンを置換する文字列 (見つかった場合) です。 詳細については、「 [ASP.NET での URL の書き換え](https://msdn.microsoft.com/library/ms972974.aspx)」を参照してください。
3. **CTRL + S**キーを押して、変更を保存します。
4. 新しい**Git Bash**コンソールを開き、Azure App Service に更新されたアプリケーションをデプロイします。
5. 次のコマンドを実行して、変更を Azure にプッシュします。 **GeekQuiz**ソリューションへのパスを使用して、 *[your-APPLICATION-path]* プレースホルダーを更新します。 デプロイパスワードを入力するように求められます。

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample18.cmd)]

    ![Azure への更新プログラムのデプロイ](maintainable-azure-websites-managing-change-and-scale/_static/image73.png)

    *Azure への更新プログラムのデプロイ*

<a id="Ex4Task4"></a>
#### <a name="task-4--verification"></a>タスク4–検証

このタスクでは、 **Internet Explorer**を使用して**マニアクイズ**アプリケーションを参照し、イメージの URL 書き換えルールが動作し、 **Azure Blob Storage**でホストされているイメージにリダイレクトされることを確認します。

1. Internet Explorer を開き、web アプリに移動します (例: `http://<your-web-site>.azurewebsites.net`)。 以前に作成した資格情報を使用してログインします。

    ![イメージを使用したマニアクイズ web アプリの表示](maintainable-azure-websites-managing-change-and-scale/_static/image74.png "イメージを使用したマニアクイズ web アプリの表示")

    *イメージを使用したマニアクイズ web アプリの表示*
2. **F12**キーを押して開発ツールを起動し、 **[ネットワーク]** タブを選択して記録を開始します。

    ![ネットワーク記録の開始](maintainable-azure-websites-managing-change-and-scale/_static/image75.png "ネットワーク記録の開始")

    *ネットワーク記録の開始*
3. CTRL キーを押し**ながら F5**キーを押して、web ページを更新します。
4. ページの読み込みが完了すると、http **301**の結果 (リダイレクト) と、http **200**の結果を含む `http://[YOUR-STORAGE-ACCOUNT].blob.core.windows.net/images/logo-big.png` url に対する別の要求で、 **/img/logo-big.png** url に対する http 要求が表示されます。

    ![URL リダイレクトを確認しています](maintainable-azure-websites-managing-change-and-scale/_static/image76.png "開発ツールでのリダイレクトの表示")

    *URL リダイレクトを確認しています*

<a id="Exercise5"></a>
### <a name="exercise-5-using-autoscale-for-web-apps"></a>演習 5: Web Apps に自動スケールを使用する

> [!NOTE]
> この演習は、 **Visual Studio 2013 Ultimate Edition**でのみ利用可能な Web ロード &amp; パフォーマンステストをサポートする必要があるため、省略可能です。 特定の Visual Studio 2013 機能の詳細について[は、ここで](https://www.microsoft.com/visualstudio/eng/products/compare)バージョンを比較してください。

**Azure App Service Web Apps**は、**標準モード**で実行されている Web アプリの自動スケール機能を提供します。 自動スケールを使用すると、負荷に応じて Azure で web アプリのインスタンス数を自動的にスケーリングできます。 自動スケールが有効になっている場合、Azure は web アプリの CPU を5分ごとに確認し、その時点で必要に応じてインスタンスを追加します。 CPU 使用率が低い場合、Azure は2時間ごとにインスタンスを削除して、web アプリのパフォーマンスが低下しないようにします。

この演習では、**マニアクイズ**web アプリの**自動スケール**機能を構成するために必要な手順について説明します。 この機能を確認するには、Visual Studio ロードテストを実行して、インスタンスのアップグレードをトリガーするためにアプリケーションに十分な CPU 負荷を生成します。

<a id="Ex5Task1"></a>
#### <a name="task-1--configuring-autoscale-based-on-the-cpu-metric"></a>タスク 1-CPU メトリックに基づいて自動スケールを構成する

このタスクでは、Azure 管理ポータルを使用して、演習2で作成した web アプリの自動スケール機能を有効にします。

1. [Microsoft Azure 管理ポータル](https://manage.windowsazure.com/)で、 **[web サイト]** を選択し、演習2で作成した web アプリをクリックします。
2. **[スケール]** ページに移動します。 **[容量]** セクションで、 **[メトリックによるスケール]** 構成の **[CPU]** を選択します。

    > [!NOTE]
    > CPU によってスケーリングする場合、CPU の使用率が変化した場合にアプリが使用するインスタンスの数が Azure によって動的に調整されます。

    ![CPU によるスケールの選択](maintainable-azure-websites-managing-change-and-scale/_static/image77.png "自動スケーリングの CPU メトリックの選択")

    *CPU によるスケールの選択*
3. **ターゲット CPU**構成を**20**-**40** % に変更します。

    > [!NOTE]
    > この範囲は、web アプリの平均 CPU 使用率を表します。 Azure では、web アプリをこの範囲内に維持するためにインスタンスを追加または削除します。 スケーリングに使用されるインスタンスの最小数と最大数は、**インスタンス数**の構成で指定されます。 Azure はこの制限を超えることはありません。
    >
    > 既定の**ターゲット CPU**値は、このラボの目的のためだけに変更されます。 CPU の範囲を小さい値で構成すると、アプリケーションに中程度の負荷が発生したときに自動スケールがトリガーされる可能性が高くなります。

    ![ターゲット CPU を 20 ~ 40% に変更する](maintainable-azure-websites-managing-change-and-scale/_static/image78.png "ターゲット CPU を 20 ~ 40% に変更する")

    *ターゲット CPU を 20 ~ 40% に変更する*
4. コマンドバーの **[保存]** をクリックして、変更を保存します。

<a id="Ex5Task2"></a>
#### <a name="task-2--load-testing-with-visual-studio"></a>タスク 2-Visual Studio を使用したロードテスト

**自動スケール**が構成されたので、web アプリに CPU 負荷を生成するために、Visual Studio で**Web パフォーマンスとロードテストのプロジェクト**を作成します。

1. **Visual Studio Ultimate 2013**を開き、 **File | を選択します。新規 |プロジェクト...** を実行すると、新しいソリューションが開始されます。

    ![新しいプロジェクトの作成](maintainable-azure-websites-managing-change-and-scale/_static/image79.png "新しいプロジェクトを作成します。")

    *新しいプロジェクトの作成*
2. **[新しいプロジェクト]** ダイアログボックスで、 **[Web パフォーマンスとロードテストのプロジェクト]** を選択します。  **C#[テスト**] タブ。 **.NET Framework 4.5**が選択されていることを確認し、プロジェクトに*WebAndLoadTestProject*という名前を設定して、**場所**を選択し、 **[OK]** をクリックします。

    ![新しい Web およびロードテストプロジェクトの作成](maintainable-azure-websites-managing-change-and-scale/_static/image80.png "新しい Web およびロードテストプロジェクトの作成")

    *新しい Web およびロードテストプロジェクトの作成*
3. Webtest1.webtest で、 **Web テスト** **Webtest1.webtest**ノードを右クリックし、 **[要求の追加]** をクリックします。

    ![Webtest1.webtest への要求の追加](maintainable-azure-websites-managing-change-and-scale/_static/image81.png "Webtest1.webtest への要求の追加")

    *Webtest1.webtest への要求の追加*
4. 新しい要求 ノードの **[プロパティ]** ウィンドウで、 **[url]** プロパティを web アプリの url を指すように更新します (例: *[http://geek-quiz.azurewebsites.net/](http://geek-quiz.azurewebsites.net/)* )。

    ![Url プロパティの変更](maintainable-azure-websites-managing-change-and-scale/_static/image82.png "Url プロパティの変更")

    *Url プロパティの変更*
5. **Webtest1.webtest**ウィンドウで、 **[webtest1.webtest]** を右クリックし、 **[ループの追加...]** をクリックします。

    ![Webtest1.webtest へのループの追加](maintainable-azure-websites-managing-change-and-scale/_static/image83.png "Webtest1.webtest へのループの追加")

    *Webtest1.webtest へのループの追加*
6. **[条件付き規則と項目をループに追加]** ダイアログボックスで、 **for ループ**規則を選択し、次のプロパティを変更します。

   1. **終了値:** 1000
   2. **コンテキストパラメーター名:** 反
   3. **増分値:** 1

      ![For ループルールを選択してプロパティを更新する](maintainable-azure-websites-managing-change-and-scale/_static/image84.png "For ループルールを選択してプロパティを更新する")

      *For ループルールを選択してプロパティを更新する*
7. **[ループ内の項目]** セクションで、ループの最初と最後の項目として以前に作成した要求を選択します。 続行するには、 **[OK]** をクリックします。

    ![ループの最初と最後の項目を選択する](maintainable-azure-websites-managing-change-and-scale/_static/image85.png "ループの最初と最後の項目を選択する")

    *ループの最初と最後の項目を選択する*
8. **ソリューションエクスプローラー**で、 **WebAndLoadTestProject**プロジェクトを右クリックし、 **[追加]** メニューを展開して、 **[ロードテスト]** を選択します。

    ![WebAndLoadTestProject プロジェクトへのロードテストの追加](maintainable-azure-websites-managing-change-and-scale/_static/image86.png "WebAndLoadTestProject プロジェクトへのロードテストの追加")

    *WebAndLoadTestProject プロジェクトへのロードテストの追加*
9. **[新しいロードテストウィザード]** ダイアログボックスで、 **[次へ]** をクリックします。

    ![新しいロードテストウィザード](maintainable-azure-websites-managing-change-and-scale/_static/image87.png "新しいロードテストウィザード")

    *新しいロードテストウィザード*
10. **[シナリオ]** ページで、 **[待ち時間を使用しない]** を選択し、 **[次へ]** をクリックします。

    ![待ち時間を使用しないことを選択する](maintainable-azure-websites-managing-change-and-scale/_static/image88.png "待ち時間を使用しないことを選択する")

    *待ち時間を使用しないことを選択する*
11. **[ロードパターン]** ページで、 **[定数読み込み]** オプションが選択されていることを確認します。 **[ユーザーカウント]** 設定を**250**ユーザーに変更し、 **[次へ]** をクリックします。

    ![ユーザーカウントを250に変更する](maintainable-azure-websites-managing-change-and-scale/_static/image89.png "ユーザーカウントを250に変更する")

    *ユーザーカウントを250に変更する*
12. **[テストミックスモデル]** ページで、 **[順次テスト順序に基づく]** を選択し、 **[次へ]** をクリックします。

    ![テストミックスモデルの選択](maintainable-azure-websites-managing-change-and-scale/_static/image90.png "テストミックスモデルの選択")

    *テストミックスモデルの選択*
13. **[テストミックスモデル]** ページで **[追加...]** をクリックして、テストをミックスに追加します。

    ![テストミックスへのテストの追加](maintainable-azure-websites-managing-change-and-scale/_static/image91.png "テストミックスへのテストの追加")

    *テストミックスへのテストの追加*
14. **[テストの追加]** ダイアログボックスで、 **[webtest1.webtest]** をダブルクリックして、 **[選択したテスト]** の一覧にテストを追加します。 続行するには、 **[OK]** をクリックします。

    ![Webtest1.webtest テストの追加](maintainable-azure-websites-managing-change-and-scale/_static/image92.png "Webtest1.webtest テストの追加")

    *Webtest1.webtest テストの追加*
15. **[テストミックス]** ページに戻り、 **[次へ]** をクリックします。

    ![[テストミックスの完了] ページ](maintainable-azure-websites-managing-change-and-scale/_static/image93.png "[テストミックスの完了] ページ")

    *[テストミックスの完了] ページ*
16. **[ネットワークミックス]** ページで、 **[次へ]** をクリックします。

    ![[ネットワークミックス] ページで [次へ] をクリックします。](maintainable-azure-websites-managing-change-and-scale/_static/image94.png "[ネットワークミックス] ページで [次へ] をクリックします。")

    *[ネットワークミックス] ページで [次へ] をクリックします。*
17. **[ブラウザーミックス]** ページで、ブラウザーの種類として **[Internet Explorer 10.0]** を選択し、 **[次へ]** をクリックします。

    ![ブラウザーの種類の選択](maintainable-azure-websites-managing-change-and-scale/_static/image95.png "ブラウザーの種類の選択")

    *ブラウザーの種類の選択*
18. **[カウンターセット]** ページで、 **[次へ]** をクリックします。

    ![[カウンターセット] ページで [次へ] をクリックします。](maintainable-azure-websites-managing-change-and-scale/_static/image96.png "[カウンターセット] ページで [次へ] をクリックします。")

    *[カウンターセット] ページで [次へ] をクリックします。*
19. **[実行設定]** ページで、 **[ロードテストの期間]** を**5 分**に設定し、 **[完了]** をクリックします。

    ![ロードテストの期間を5分に設定する](maintainable-azure-websites-managing-change-and-scale/_static/image97.png "ロードテストの期間を5分に設定する")

    *ロードテストの期間を5分に設定する*
20. **ソリューションエクスプローラー**で、**ローカルの設定**ファイルをダブルクリックして、テストの設定を調べます。 既定では、Visual Studio はローカルコンピューターを使用してテストを実行します。

    > [!NOTE]
    > または、 **Azure Test Plans**を使用して、クラウドでロードテストを実行するようにテストプロジェクトを構成することもできます。 Azure Test Plans は、より現実的な負荷をシミュレートし、CPU 容量、使用可能なメモリ、ネットワーク帯域幅などのローカル環境の制約を回避するクラウドベースのロードテストサービスを提供します。 Azure Test Plans を使用したロードテストの実行の詳細については、「[ロードテストのシナリオ](/azure/devops/test/load-test/overview?view=vsts)」を参照してください。

    ![テストの設定](maintainable-azure-websites-managing-change-and-scale/_static/image98.png)

<a id="Ex5Task3"></a>
#### <a name="task-3--autoscale-verification"></a>タスク 3-自動スケール検証

ここでは、前のタスクで作成したロードテストを実行し、web アプリが負荷の下でどのように動作するかを確認します。

1. **ソリューションエクスプローラー**で、 **loadtest1.loadtest**をダブルクリックしてロードテストを開きます。

    ![Loadtest1.loadtest を開いています。 loadtest](maintainable-azure-websites-managing-change-and-scale/_static/image99.png "Loadtest1.loadtest を開いています。 loadtest")

    *Loadtest1.loadtest を開いています。 loadtest*
2. **Loadtest1.loadtest**ウィンドウで、ツールボックスの最初のボタンをクリックして、ロードテストを実行します。

    ![ロードテストの実行](maintainable-azure-websites-managing-change-and-scale/_static/image100.png "ロードテストの実行")

    *ロードテストの実行*
3. ロードテストが完了するまで待ちます。

    > [!NOTE]
    > ロードテストでは、web アプリに要求を同時に送信する複数のユーザーをシミュレートします。 テストの実行中は、使用可能なカウンターを監視して、ロードテストの実行に関連するエラー、警告、その他の情報を検出することができます。

    ![ロードテストの実行中](maintainable-azure-websites-managing-change-and-scale/_static/image101.png "ロードテストが完了するまで待機しています")

    *ロードテストの実行中*
4. テストが完了したら、管理ポータルに戻り、web アプリの **[スケール]** ページに移動します。 **[容量]** セクションで、新しいインスタンスが自動的にデプロイされたことをグラフに表示します。

    ![新しいインスタンスが自動的に展開されました](maintainable-azure-websites-managing-change-and-scale/_static/image102.png)

    *新しいインスタンスが自動的に展開されました*

    > [!NOTE]
    > グラフに変更が表示されるまでに数分かかる場合があります (ページを更新するには、CTRL キーを押し**ながら F5**キーを押します)。 何も変更されていない場合は、次のようにしてみてください。
    >
    > - ロードテストの期間を長くする (例: **10 分**)
    > - Web アプリの自動スケール構成で、**ターゲット CPU**範囲の最大値と最小値を小さくします。
    > - **Azure Test Plans**を使用して、クラウドでロードテストを実行します。 詳細情報は[こちら](/azure/devops/test/load-test/index?view=vsts)です

---

<a id="Summary"></a>
## <a name="summary"></a>まとめ

このハンズオンラボでは、Azure の運用 web アプリにアプリケーションをセットアップしてデプロイする方法を学習しました。 まず、 **Entity Framework Code First Migrations**を使用してデータベースを検出して更新した後、 **Git**を使用してサイトの新しいバージョンをデプロイし、サイトの最新の安定したバージョンへのロールバックを実行します。 また、ストレージを使用してアプリケーションを拡張し、静的コンテンツを Blob コンテナーに移動する方法についても説明しました。
