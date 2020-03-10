---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-database-update
title: 'Visual Studio を使用した ASP.NET Web 配置: データベース更新の配置 |Microsoft Docs'
author: tdykstra
description: このチュートリアルシリーズでは、ASP.NET web アプリケーションをデプロイ (発行) して、Web Apps またはサードパーティのホスティングプロバイダーに Azure App Service する方法について説明します。
ms.author: riande
ms.date: 02/15/2013
ms.assetid: 9cad0833-486a-4474-a7f3-7715542ec4ce
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-database-update
msc.type: authoredcontent
ms.openlocfilehash: 805eb84c24764cf921291f89054435601dbac48e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78440788"
---
# <a name="aspnet-web-deployment-using-visual-studio-deploying-a-database-update"></a>Visual Studio を使用した ASP.NET Web 配置: データベース更新プログラムの配置

[Tom Dykstra](https://github.com/tdykstra)

[スタートプロジェクトのダウンロード](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> このチュートリアルシリーズでは、Visual Studio 2012 または Visual Studio 2010 を使用して、Azure App Service Web Apps またはサードパーティのホスティングプロバイダーにするために、ASP.NET web アプリケーションをデプロイ (発行) する方法について説明します。 シリーズの詳細については、[シリーズの最初のチュートリアル](introduction.md)を参照してください。

## <a name="overview"></a>概要

このチュートリアルでは、データベースの変更と関連するコードの変更を行い、Visual Studio で変更をテストしてから、テスト環境、ステージング環境、および運用環境に更新プログラムを配置します。

このチュートリアルでは、まず Code First Migrations によって管理されるデータベースを更新する方法を示します。その後、dbDacFx プロバイダーを使用してデータベースを更新する方法を示します。

リマインダー: チュートリアルを実行しているときにエラーメッセージが表示されたり機能しない場合は、必ず[トラブルシューティングのページ](troubleshooting.md)を確認してください。

## <a name="deploy-a-database-update-by-using-code-first-migrations"></a>Code First Migrations を使用してデータベースの更新を配置する

このセクションでは、`Student` エンティティと `Instructor` エンティティの `Person` 基本クラスに生年月日列を追加します。 次に、インストラクターのデータを表示するページを更新して、新しい列が表示されるようにします。 最後に、変更をテスト、ステージング、および運用にデプロイします。

### <a name="add-a-column-to-a-table-in-the-application-database"></a>アプリケーションデータベースのテーブルに列を追加する

1. *ContosoUniversity*プロジェクトで、 *Person.cs*を開き、次のプロパティを `Person` クラスの末尾に追加します (この後に2つの右中かっこが必要です)。

    [!code-csharp[Main](deploying-a-database-update/samples/sample1.cs)]

    次に、新しい列の値を提供するように `Seed` メソッドを更新します。 *Migrations\ configuration.cs*を開き、`var instructors = new List<Instructor>` 開始するコードブロックを、生年月日の情報を含む次のコードブロックに置き換えます。

    [!code-csharp[Main](deploying-a-database-update/samples/sample2.cs)]
2. ソリューションをビルドし、 **[パッケージマネージャーコンソール]** ウィンドウを開きます。 ContosoUniversity が**既定のプロジェクト**として選択されていることを確認します。
3. **パッケージマネージャーコンソール**ウィンドウで、**既定のプロジェクト**として **[ContosoUniversity]** を選択し、次のコマンドを入力します。

    [!code-powershell[Main](deploying-a-database-update/samples/sample3.ps1)]

    このコマンドが終了すると、Visual Studio によって新しい `DbMigration` クラスを定義するクラスファイルが開き、`Up` メソッドに新しい列を作成するコードが表示されます。 `Up` メソッドは、変更を実装するときに列を作成し、変更をロールバックするときに、`Down` メソッドが列を削除します。

    ![AddBirthDate_migration_code](deploying-a-database-update/_static/image1.png)
4. ソリューションをビルドし、 **[パッケージマネージャーコンソール]** ウィンドウで次のコマンドを入力します (ContosoUniversity プロジェクトが選択されていることを確認します)。

    [!code-powershell[Main](deploying-a-database-update/samples/sample4.ps1)]

    Entity Framework は、`Up` メソッドを実行し、`Seed` メソッドを実行します。

### <a name="display-the-new-column-in-the-instructors-page"></a>[インストラクター] ページに新しい列を表示します。

1. ContosoUniversity プロジェクトで、*講師*を開き、生年月日を表示する新しいテンプレートフィールドを追加します。 入社年月日と office assignment の間に追加します。

    [!code-aspx[Main](deploying-a-database-update/samples/sample5.aspx?highlight=9-17)]

    (コードのインデントが同期されない場合は、CTRL + K キーを押してから CTRL + D キーを押してファイルを自動的に再フォーマットできます)。
2. アプリケーションを実行し、 **[インストラクター]** リンクをクリックします。

    ページが読み込まれると、[新しい生年月日] フィールドが表示されます。

    ![誕生日付きのインストラクターページ](deploying-a-database-update/_static/image2.png)
3. ブラウザーを閉じます。

### <a name="deploy-the-database-update"></a>データベースの更新を展開する

1. **ソリューションエクスプローラー** ContosoUniversity プロジェクトを選択します。
2. Web 上の **[発行**] ツールバーで、**テスト**発行プロファイルをクリックし、 **[web の発行]** をクリックします。 (ツールバーが無効になっている場合は**ソリューションエクスプローラー**で ContosoUniversity プロジェクトを選択します)。

    更新されたアプリケーションが Visual Studio によってデプロイされ、ブラウザーがホームページに表示されます。
3. **インストラクター**ページを実行して、更新プログラムが正常に展開されたことを確認します。

    アプリケーションがこのページのデータベースにアクセスしようとすると、Code First データベーススキーマが更新され、`Seed` メソッドが実行されます。 ページが表示されると、[予想される**誕生日**] 列に日付が含まれていることがわかります。
4. Web 上の **[発行**] ツールバーで、 **[ステージング]** 発行プロファイル をクリックし、 **[web の発行]** をクリックします。
5. ステージングの**インストラクター**ページを実行して、更新が正常に展開されたことを確認します。
6. Web 上の **[発行**] ツールバーで、 **[実稼働]** 発行プロファイル をクリックし、 **[web の発行]** をクリックします。
7. 運用環境で**インストラクター**ページを実行し、更新が正常に展開されたことを確認します。

    データベースの変更を含む実際の運用アプリケーションの更新については、前のチュートリアルで見たように、*アプリ\_offline .htm*を使用してデプロイ中にアプリケーションをオフラインにすることも通常します。

## <a name="deploy-a-database-update-by-using-the-dbdacfx-provider"></a>DbDacFx プロバイダーを使用してデータベースの更新を配置する

このセクションでは、メンバーシップデータベースの*ユーザー*テーブルに*コメント*列を追加し、各ユーザーのコメントを表示および編集できるページを作成します。 次に、変更をテスト、ステージング、および運用にデプロイします。

### <a name="add-a-column-to-a-table-in-the-membership-database"></a>メンバーシップデータベースのテーブルに列を追加する

1. Visual Studio で**SQL Server オブジェクトエクスプローラー**を開きます。
2. **(Localdb)、v11.0**、 **[データベース]** 、[ **aspnet-ContosoUniversity** ( **aspnet-ContosoUniversity**)] の順に展開し、 **[テーブル]** を展開します。

    **[SQL Server]** ノードの下に **(localdb) \ v11.0**が表示されない場合は、 **[SQL Server]** ノードを右クリックし、 **[SQL Server の追加]** をクリックします。 **[サーバーへの接続]** ダイアログボックスで、**サーバー名**として *「(localdb) \ v11.0* 」と入力し、 **[接続]** をクリックします。

    **ContosoUniversity**が表示されない場合は、プロジェクトを実行し、*管理者*の資格情報 (パスワードは*devpwd*) を使用してログインしてから、 **[SQL Server オブジェクトエクスプローラー]** ウィンドウを更新します。
3. **Users**テーブルを右クリックし、[デザイナーの**表示**] をクリックします。

    ![SSOX ビューデザイナー](deploying-a-database-update/_static/image3.png)
4. デザイナーで、*コメント*列を追加し、 *nvarchar (128)* および nullable に設定して、 **[更新]** をクリックします。

    ![コメント列の追加](deploying-a-database-update/_static/image4.png)
5. **[データベースの更新のプレビュー]** ボックスで、データベースの **[更新]** をクリックします。

    ![データベースの更新のプレビュー](deploying-a-database-update/_static/image5.png)

### <a name="create-a-page-to-display-and-edit-the-new-column"></a>新しい列を表示および編集するためのページを作成する

1. **ソリューションエクスプローラー**で、ContosoUniversity プロジェクトの**アカウント**フォルダーを右クリックし、 **[追加]** をクリックして、 **[新しい項目]** をクリックします。
2. **マスターページを使用して新しい Web フォーム**を作成し、「 *UserInfo*」という名前を指定します。 既定の*サイトのマスター*ファイルをマスターページとして受け入れます。
3. 次のマークアップを `MainContent` `Content` 要素 (最後の3つの `Content` 要素の最後) にコピーします。

    [!code-aspx[Main](deploying-a-database-update/samples/sample6.aspx)]
4. [ *UserInfo* ] ページを右クリックし、 **[ブラウザーで表示]** をクリックします。
5. *管理者*ユーザーの資格情報 (パスワードは*devpwd*) でログインし、ユーザーにコメントを追加して、ページが正しく機能することを確認します。

    ![UserInfo ページ](deploying-a-database-update/_static/image6.png)
6. ブラウザーを閉じます。

## <a name="deploy-the-database-update"></a>データベースの更新を展開する

DbDacFx プロバイダーを使用して配置するには、発行プロファイルの **[データベースの更新]** オプションを選択するだけです。 ただし、このオプションを使用した場合の初期デプロイでは、いくつかの追加の SQL スクリプトを実行するように構成しています。これらのスクリプトはまだプロファイルに含まれているため、再度実行されないようにする必要があります。

1. ContosoUniversity プロジェクトを右クリックし、 **[発行]** をクリックして、 **Web の発行**ウィザードを開きます。
2. **テスト**プロファイルを選択します。
3. **[設定]** タブをクリックします。
4. **[Defaultconnection]** で **[データベースの更新]** を選択します。
5. 初期デプロイで実行するように構成した追加のスクリプトを無効にします。

    1. **[データベースの更新の構成]** をクリックします。
    2. **[データベースの更新の構成]** ダイアログボックスで、[ *Grant .sql*および*aspnet-data-dev*] の横のチェックボックスをオフにします。
    3. **[閉じる]** をクリックします。
6. **[プレビュー]** タブをクリックします。
7. **[データベース]** の **[defaultconnection]** の右側で、 **[データベースのプレビュー]** リンクをクリックします。

    ![データベースのプレビュー](deploying-a-database-update/_static/image7.png)

    プレビューウィンドウには、データベーススキーマがソースデータベースのスキーマと一致するように、コピー先データベースで実行されるスクリプトが表示されます。 このスクリプトには、新しい列を追加する ALTER TABLE コマンドが含まれています。
8. **[データベースのプレビュー]** ダイアログボックスを閉じ、 **[発行]** をクリックします。

    更新されたアプリケーションが Visual Studio によってデプロイされ、ブラウザーがホームページに表示されます。
9. UserInfo ページ (*アカウント/UserInfo*をホームページの URL に追加) を実行して、更新が正常に展開されたことを確認します。 「 *Admin* 」と「 *devpwd*」と入力してログインする必要があります。

    テーブル内のデータは既定では配置されません。また、データ配置スクリプトを実行するように構成していないため、開発時に追加したコメントは見つかりません。 ステージングに新しいコメントを追加して、変更がデータベースに配置され、ページが正しく機能することを確認できます。
10. 同じ手順に従って、ステージング環境と運用環境にデプロイします。

    忘れずに余分なスクリプトを無効にしてください。 テストプロファイルとの唯一の違いは、ステージングプロファイルと実稼働プロファイルでは、 *aspnet-prod-data*のみを実行するように構成されているスクリプトを1つだけ無効にすることです。

    ステージングと運用の資格情報は、admin と prodpwd です。

    データベースの変更を含む実際の運用アプリケーションの更新については、[前のチュートリアル](deploying-a-code-update.md)で説明したように、後で発行および削除する前に、*アプリ\_offline .htm*をアップロードしてデプロイ中にアプリケーションをオフラインにすることもできます。

## <a name="summary"></a>まとめ

これで、Code First Migrations と dbDacFx プロバイダーの両方を使用してデータベースの変更を含むアプリケーションの更新が配置されました。

![誕生日付きのインストラクターページ](deploying-a-database-update/_static/image8.png)

![UserInfo ページ](deploying-a-database-update/_static/image9.png)

次のチュートリアルでは、コマンドラインを使用してデプロイを実行する方法について説明します。

> [!div class="step-by-step"]
> [前へ](deploying-a-code-update.md)
> [次へ](command-line-deployment.md)
