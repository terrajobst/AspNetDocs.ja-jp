---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application
title: 'チュートリアル: ASP.NET MVC アプリで EF の移行を使用して Azure にデプロイする'
author: tdykstra
description: このチュートリアルでは、Code First の移行を有効にし、Azure のクラウドにアプリケーションをデプロイします。
ms.author: riande
ms.date: 01/16/2019
ms.topic: tutorial
ms.assetid: d4dfc435-bda6-4621-9762-9ba270f8de4e
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 989dd0f0e18b338be057b9c5657586eff996d8ea
ms.sourcegitcommit: b95316530fa51087d6c400ff91814fe37e73f7e8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/23/2019
ms.locfileid: "70000764"
---
# <a name="tutorial-use-ef-migrations-in-an-aspnet-mvc-app-and-deploy-to-azure"></a>チュートリアル: ASP.NET MVC アプリで EF の移行を使用して Azure にデプロイする

これまで、Contoso 大学のサンプル web アプリケーションは、開発用コンピューターの IIS Express でローカルに実行されています。 実際のアプリケーションをインターネット経由で他のユーザーが使用できるようにするには、それを web ホスティングプロバイダーに展開する必要があります。 このチュートリアルでは、Code First の移行を有効にし、Azure のクラウドにアプリケーションをデプロイします。

- Code First Migrations を有効にします。 移行機能を使用すると、データベースを削除して再作成しなくても、データベーススキーマを更新することで、データモデルを変更し、変更を運用環境に配置できます。
- Azure にデプロイします。 この手順は省略可能です。プロジェクトをデプロイしなくても、残りのチュートリアルに進むことができます。

デプロイにはソース管理と継続的インテグレーションプロセスを使用することをお勧めしますが、このチュートリアルではこれらのトピックについては説明しません。 詳細については、「 [Azure を使用した実際のクラウドアプリの構築](xref:aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction)」の[ソース管理](xref:aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control)と[継続的インテグレーション](xref:aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery)に関する章を参照してください。

このチュートリアルでは、次の作業を行いました。

> [!div class="checklist"]
> * Code First 移行を有効にする
> * Azure にアプリをデプロイする (省略可能)

## <a name="prerequisites"></a>必須コンポーネント

- [接続復元性とコマンド傍受](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="enable-code-first-migrations"></a>Code First 移行を有効にする

新しいアプリケーションを開発して、データ モデルが頻繁に変更される場合、モデルが変更されるたびに、モデルはデータベースと同期されなくなります。 データモデルを変更するたびに、データベースを自動的に削除して再作成するように Entity Framework を構成しました。 エンティティクラスを追加、削除、または変更したり、 `DbContext`クラスを変更したりすると、次にアプリケーションを実行するときに、既存のデータベースが自動的に削除され、モデルに一致する新しいデータベースが作成され、テストデータでシードされます。

このメソッドは、実稼働環境にアプリケーションを展開するまで、データベースとデータ モデルの同期の維持がうまく機能します。 アプリケーションが運用環境で実行されている場合、通常は保持するデータを格納し、新しい列の追加などの変更を行うたびにすべてのデータを失わないようにします。 [Code First Migrations](https://msdn.microsoft.com/data/jj591621)機能では、データベースを削除して再作成するのではなく、Code First でデータベーススキーマを更新できるようにすることで、この問題を解決します。 このチュートリアルでは、アプリケーションを展開し、移行を有効にする準備をします。

1. 前の手順で設定した初期化子を無効にするに`contexts`は、アプリケーションの web.config ファイルに追加した要素をコメントアウトするか削除します。

    [!code-xml[Main](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.xml?highlight=2,6)]
2. また、アプリケーションの*web.config*ファイルで、接続文字列内のデータベースの名前を ContosoUniversity2 に変更します。

    [!code-xml[Main](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.xml?highlight=2)]

    この変更により、最初の移行で新しいデータベースが作成されるようにプロジェクトが設定されます。 これは必須ではありませんが、後で推奨される理由がわかります。
3. **[ツール]** メニューで、 **[NuGet パッケージ マネージャー]**  >  **[パッケージ マネージャー コンソール]** の順に選択します。

1. `PM>`プロンプトで、次のコマンドを入力します。

    ```text
    enable-migrations
    add-migration InitialCreate
    ```

    この`enable-migrations`コマンドにより、ContosoUniversity プロジェクトに*移行*フォルダーが作成され、そのフォルダーに*Configuration.cs*ファイルが配置されます。このファイルを編集して、移行を構成することができます。

    (データベース名を変更するように指示された手順を実行しなかった場合は、既存のデータベースが検索`add-migration`され、自動的にコマンドが実行されます。 これは、データベースを配置する前に、移行コードのテストを実行しないことを意味するだけです。 後で`update-database`コマンドを実行すると、データベースが既に存在しているため、何も起こりません。)

    *ContosoUniversity\Migrations\Configuration.cs*ファイルを開きます。 前に見た初期化子クラスと同様に`Configuration` 、クラスに`Seed`はメソッドが含まれています。

    [!code-csharp[Main](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

    [Seed](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx)メソッドの目的は、データベースを作成または更新した後に、テストデータを挿入または更新 Code First できるようにすることです。 メソッドは、データベースが作成されたときと、データモデルの変更後にデータベーススキーマが更新されるたびに呼び出されます。

### <a name="set-up-the-seed-method"></a>Seed メソッドを設定する

すべてのデータモデルの変更に対してデータベースを削除して再作成する場合は、初期化`Seed`子クラスのメソッドを使用してテストデータを挿入します。これは、すべてのモデルが変更された後、データベースが削除され、すべてのテストデータが失われるためです。 Code First Migrations を使用すると、データベースの変更後もテストデータが保持されるため、通常、 [Seed](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx)メソッドにテストデータを含める必要はありません。 実際には、 `Seed` `Seed`メソッドが運用環境で実行されるため、移行を使用してデータベースを運用環境に配置する場合は、メソッドでテストデータを挿入しないようにする必要があります。 その場合は、運用環境で`Seed`必要なデータのみをデータベースに挿入することをお勧めします。 たとえば、アプリケーションを運用環境で使用できるようになったときに`Department` 、データベースにテーブルの実際の部署名を含めるようにすることができます。

このチュートリアルでは、配置のために移行を使用します`Seed`が、データを手動で挿入することなく、アプリケーションの機能がどのように動作するかを簡単に確認できるように、テストデータを挿入します。

1. *Configuration.cs*ファイルの内容を次のコードに置き換えます。これにより、テストデータが新しいデータベースに読み込まれます。

    [!code-csharp[Main](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

    [Seed](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx)メソッドは、データベースコンテキストオブジェクトを入力パラメーターとして受け取り、メソッドのコードはそのオブジェクトを使用して新しいエンティティをデータベースに追加します。 このコードは、エンティティ型ごとに新しいエンティティのコレクションを作成し、適切な[Dbset](https://msdn.microsoft.com/library/system.data.entity.dbset(v=vs.103).aspx)プロパティに追加して、変更をデータベースに保存します。 ここで行ったように、エンティティの各グループの後に[SaveChanges](https://msdn.microsoft.com/library/system.data.entity.dbcontext.savechanges(v=VS.103).aspx)メソッドを呼び出す必要はありませんが、コードがデータベースに書き込んでいる間に例外が発生した場合に、問題の原因を特定するのに役立ちます。

    データを挿入するステートメントの中には、 [Addorupdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx)メソッドを使用して "upsert" 操作を実行するものがあります。 このメソッド`Seed`は`update-database`コマンドを実行するたびに実行されるため、通常は、各移行の後に、追加しようとしている行が、データベースを最初に作成した移行の後に既に存在するため、データを挿入するだけではかまいません。 "Upsert" 操作は、既に存在する行を挿入しようとすると発生するエラーを防ぎますが、アプリケーションのテスト中に行われたデータの変更を***上書き***します。 一部のテーブルのテストデータでは、このような処理が不要な場合があります。テスト中にデータを変更し、データベースの更新後も変更を保持する場合があります。 その場合は、条件付き挿入操作を実行します。行がまだ存在しない場合にのみ、行を挿入します。 Seed メソッドは、両方の方法を使用します。

    [Addorupdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx)メソッドに渡される最初のパラメーターは、行が既に存在するかどうかを確認するために使用するプロパティを指定します。 提供しているテスト学生データについては`LastName` 、リスト内の各姓が一意であるため、この目的にプロパティを使用できます。

    [!code-csharp[Main](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs)]

    このコードは、姓が一意であることを前提としています。 姓が重複する学生を手動で追加すると、次に移行を実行したときに次の例外が発生します。

    **シーケンスに複数の要素が含まれています**

    "アレクサンドロス Carson" という名前の2人の学生などの冗長データを処理する方法については、Rick Anderson のブログの「 [Entity Framework (EF) db のシード処理とデバッグ](https://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx)」を参照してください。 メソッドの`AddOrUpdate`詳細については、「ジュリー Lerman のブログの[EF 4.3 addorupdate メソッドに](http://thedatafarm.com/blog/data-access/take-care-with-ef-4-3-addorupdate-method/)対処する」を参照してください。

    エンティティを作成`Enrollment`するコードでは、コレクション`ID`のエンティティ`students`に値があることを前提としていますが、コレクションを作成するコードでそのプロパティを設定していません。

    [!code-csharp[Main](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs?highlight=2)]

    コレクションに対して`ID`を呼び出す`ID` `SaveChanges`ときに値が設定されるため、ここでプロパティを使用できます。 `students` EF は、エンティティをデータベースに挿入するときに主キーの値を自動的に取得し`ID` 、メモリ内のエンティティのプロパティを更新します。

    エンティティセット`Enrollment` `Enrollments`に各エンティティを追加するコードでは、メソッドは`AddOrUpdate`使用しません。 エンティティが既に存在するかどうかを確認し、エンティティが存在しない場合は挿入します。 この方法では、アプリケーション UI を使用して、登録グレードに加えた変更を保持します。 このコードでは、 `Enrollment`[一覧](https://msdn.microsoft.com/library/6sh2ey19.aspx)の各メンバーをループ処理します。登録がデータベースに見つからない場合は、登録がデータベースに追加されます。 データベースを初めて更新すると、データベースは空になるため、各登録が追加されます。

    [!code-csharp[Main](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

2. プロジェクトをビルドします。

### <a name="execute-the-first-migration"></a>最初の移行を実行する

`add-migration`コマンドを実行すると、データベースを最初から作成するコードが移行によって生成されます。 このコードは、  *&lt;timestamp&gt;InitialCreate.csという名前のファイル内の[移行]フォルダーにもあります。\_* クラスのメソッドに`Up`よって、データモデルの`Down`エンティティセットに対応するデータベーステーブルが作成され、メソッドによって削除されます。 `InitialCreate`

[!code-csharp[Main](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

移行は、`Up` メソッドを呼び出して、移行のためのデータ モデルの変更を実装します。 更新をロールバックするためのコマンドを入力すると、移行が `Down` メソッドを呼び出します。

これは、 `add-migration InitialCreate`コマンドを入力したときに作成された最初の移行です。 パラメーター (`InitialCreate`この例では) はファイル名に使用され、任意のものを指定できます。通常は、移行中に実行される内容を要約する単語または語句を選択します。 たとえば、後の移行&quot;AddDepartmentTable&quot;に名前を指定することができます。

データベースが既に存在するときに、初期移行を作成した場合、データベースの作成コードが生成されますが、データベースは既にデータと一致しているため、作成コードを実行する必要はありません。 データベースがまだ存在しない別の環境にアプリを展開する場合、データベースを作成するために、このコードが実行されるため、最初にテストを行うことをお勧めします。 そのため、以前&mdash;に接続文字列内のデータベースの名前を変更して、移行で新しいデータベースを作成できるようにしました。

1. **[パッケージマネージャーコンソール]** ウィンドウで、次のコマンドを入力します。

    `update-database`

    この`update-database`コマンドは、 `Up`メソッドを実行してデータベースを作成し、 `Seed`メソッドを実行してデータベースを設定します。 アプリケーションを展開した後、次のセクションに示すように、同じプロセスが運用環境で自動的に実行されます。
2. 最初のチュートリアルで行ったように、**サーバーエクスプローラー**を使用してデータベースを検査し、アプリケーションを実行して、すべてが以前と同じように動作することを確認します。

## <a name="deploy-to-azure"></a>Azure に配置する

これまでは、アプリケーションは開発用コンピューターの IIS Express でローカルに実行されていました。 他のユーザーがインターネット経由で使用できるようにするには、それを web ホスティングプロバイダーに展開する必要があります。 チュートリアルのこのセクションでは、Azure にデプロイします。 このセクションは省略可能です。これをスキップして次のチュートリアルに進むことができます。また、このセクションの手順は、選択した別のホスティングプロバイダーに合わせて変更することもできます。

### <a name="use-code-first-migrations-to-deploy-the-database"></a>Code First の移行を使用してデータベースを展開する

データベースを配置するには、Code First Migrations を使用します。 Visual Studio からデプロイするための設定を構成するために使用する発行プロファイルを作成するときに、 **[データベースの更新]** というチェックボックスをオンにします。 この設定により、配置プロセスでは、Code Firstが`MigrateDatabaseToLatestVersion`初期化子クラスを使用するように、移行先サーバー上のアプリケーションの web.config ファイルが自動的に構成されます。

プロジェクトを移行先サーバーにコピーしている間、Visual Studio は配置プロセス中にデータベースに対して何も実行しません。 配置後に配置されたアプリケーションを実行し、データベースに初めてアクセスすると、Code First データベースがデータモデルと一致するかどうかがチェックされます。 不一致がある場合、Code First によってデータベースが自動的に作成されます (まだ存在しない場合)。またはデータベーススキーマを最新バージョンに更新します (データベースが存在するがモデルに一致しない場合)。 アプリケーションが移行`Seed`方法を実装している場合、メソッドは、データベースが作成された後、またはスキーマが更新された後に実行されます。

移行`Seed`方法によって、テストデータが挿入されます。 運用環境に配置する場合は、実稼働データベースに挿入するデータ`Seed`のみが挿入されるように、メソッドを変更する必要があります。 たとえば、現在のデータモデルでは、開発用データベースに架空のコースを作成することができます。 開発時に両方`Seed`を読み込むメソッドを作成し、実稼働環境にデプロイする前に架空の学生をコメントアウトすることができます。 または、コースのみ`Seed`を読み込むメソッドを作成し、アプリケーションの UI を使用して、テストデータベースに架空の学生を手動で入力することもできます。

### <a name="get-an-azure-account"></a>Azure アカウントを取得する

Azure アカウントが必要です。 まだお持ちでない場合は、Visual Studio サブスクリプションをお持ちの場合は、 [サブスクリプションの特典](https://azure.microsoft.com/pricing/member-offers/credit-for-visual-studio-subscribers/
)を有効にすることができます。 それ以外の場合は、無料試用版アカウントを数分で作成できます。 詳細については、[Azure 無料試用版](https://azure.microsoft.com/free/)を参照してください。

### <a name="create-a-web-site-and-a-sql-database-in-azure"></a>Azure で web サイトと SQL データベースを作成する

Azure の web アプリは共有ホスティング環境で実行されます。これは、他の Azure クライアントと共有されている仮想マシン (Vm) 上で動作することを意味します。 共有ホスティング環境は、クラウドでの使い始めるための低コストな方法です。 その後、web トラフィックが増加した場合は、専用の Vm でを実行することで、ニーズに合わせてアプリケーションを拡張できます。 Azure App Service の価格オプションの詳細については、 [App Service 価格](https://azure.microsoft.com/pricing/details/app-service/)に関するページを参照してください。

ここでは、Azure SQL database にデータベースをデプロイします。 SQL database は、SQL Server テクノロジに基づいて構築されたクラウドベースのリレーショナルデータベースサービスです。 SQL Server と連携するツールとアプリケーションは、SQL database でも動作します。

1. [Azure 管理ポータル](https://portal.azure.com)で、左側のタブにある **[リソースの作成]** を選択し、**新しい**ウィンドウ (または*ブレード*) で **[すべて表示]** を選択して、使用可能なすべてのリソースを表示します。 **[すべて]** ブレードの **[web]** セクションで **[web アプリ + SQL]** を選択します。 最後に、 **[作成]** を選択します。

    ![Azure portal でリソースを作成する](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/_static/create-azure-resource.png)

   新しい**Web アプリ + SQL**リソースを作成するためのフォームが開きます。

2. アプリケーションの一意の URL として使用する文字列を **[アプリ名]** ボックスに入力します。 完全な URL は、ここで入力した内容と Azure アプリ Services (. azurewebsites.net) の既定のドメインで構成されます。 **アプリ名**が既に取得されている場合は、*アプリケーション名が使用できない*ことを知らせるメッセージが表示されます。 **アプリ名**が使用可能な場合は、緑色のチェックマークが表示されます。

3. **[サブスクリプション]** ボックスで、 **App Service**を配置する Azure サブスクリプションを選択します。

4. **[リソースグループ]** テキストボックスで、リソースグループを選択するか、新しいリソースグループを作成します。 この設定では、web サイトが実行されるデータセンターを指定します。 リソースグループの詳細については、「[リソースグループ](/azure/azure-resource-manager/resource-group-overview#resource-groups)」を参照してください。

5. 新しい**App Service プラン**を作成するには、[ *App Service] セクション*をクリックし、 **[新規作成]** をクリックして**App Service プラン**(App Service と同じ名前でもかまいません)、 **[場所]** 、および **[価格レベル]** を選択します (無料のオプションがあります)。

6. **SQL Database** をクリックし、**新しいデータベースの作成** または 既存のデータベースの選択 を選択します。

7. **[名前]** ボックスに、データベースの名前を入力します。
8. **[対象サーバー]** ボックスをクリックし、 **[新しいサーバーの作成]** を選択します。 または、サーバーを既に作成してある場合は、使用可能なサーバーの一覧からそのサーバーを選択できます。
9. **[価格レベル]** セクションを選択し、[*無料*] を選択します。 追加のリソースが必要な場合は、いつでもデータベースをスケールアップできます。 Azure SQL の料金の詳細については、 [Azure SQL Database の価格](https://azure.microsoft.com/pricing/details/sql-database/managed/)に関するページを参照してください。
10. 必要に応じて[照合順序](/sql/relational-databases/collations/collation-and-unicode-support)を変更します。
11. 管理者の**Sql 管理者ユーザー名**と**Sql 管理者パスワード**を入力します。

    - **[新しい SQL Database サーバー]** を選択した場合は、後でデータベースにアクセスするときに使用する新しい名前とパスワードを定義します。
    - 以前に作成したサーバーを選択した場合は、そのサーバーの資格情報を入力します。

12. テレメトリの収集は、Application Insights を使用して App Service に対して有効にすることができます。 構成が少ない場合、Application Insights は重要なイベント、例外、依存関係、要求、およびトレース情報を収集します。 Application Insights の詳細については、「 [Azure Monitor](https://azure.microsoft.com/services/monitor/)」を参照してください。
13. 下部にある **[作成]** をクリックして、完了したことを示します。

    管理ポータルによって ダッシュボード ページに戻り、ページの上部にある **通知** 領域にサイトが作成されていることが示されます。 しばらくすると (通常は1分未満)、デプロイが成功したことを示す通知があります。 左側のナビゲーションバーの **[App Services]** セクションに新しい App Service が表示され、 **[sql]** データベース セクションに新しい sql データベースが表示されます。

### <a name="deploy-the-app-to-azure"></a>Azure にアプリを配置する

1. Visual Studio で**ソリューションエクスプローラー**でプロジェクトを右クリックし、コンテキストメニューから **[発行]** を選択します。

2. **[発行先の選択]** ページで、 **[App Service** ] を選択し、[既存] を**選択**して、 **[発行]** を選択します。

    ![発行先の選択ページ](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/_static/publish-select-existing-azure-app-service.png)

3. まだ Visual Studio で Azure サブスクリプションを追加していない場合は、画面で手順を実行します。 これらの手順により、Visual Studio から Azure サブスクリプションに接続し、 **App Services**の一覧に web サイトが含まれるようにすることができます。

4. **[App Service]** ページで、App Service を追加した**サブスクリプション**を選択します。 **[表示]** で、 **[リソースグループ]** を選択します。 App Service 追加したリソースグループを展開し、App Service を選択します。 **[OK]** を選択してアプリを発行します。

5. **[出力]** ウィンドウには、実行された配置アクションが表示され、デプロイが正常に完了したことがレポートされます。

6. デプロイが成功すると、既定のブラウザーが自動的に開き、デプロイされた web サイトの URL が表示されます。

    ![Students_index_page_with_paging](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/_static/cloud-app-browser.png)

    これで、アプリはクラウドで実行されています。

この時点で、 **[Code First Migrations の実行 (アプリの起動時に実行)]** を選択したため、Azure SQL Database に*schoolcontext.cs*データベースが作成されました。 デプロイされた web サイトの*web.config ファイルが*変更され、コードがデータベース内のデータの読み取りまたは書き込みを初めて実行するときに ( **[Students]** タブを選択したときに[発生しまし](https://msdn.microsoft.com/library/hh829476(v=vs.103).aspx)た)、):

![Web.config ファイルの抜粋](https://asp.net/media/4367421/mig.png)

また、配置プロセスでは、データベーススキーマの更新とデータベースのシード処理に使用する Code First Migrations 用の新しい接続文字列 *(schoolcontext.cs\_databasepublish*) も作成されました。

![Web.config ファイル内の接続文字列](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image26.png)

配置された web.config ファイルのバージョンは、自分のコンピューターのユーザーのコンピューターに配置されていることがわかります。詳細については、 *「」を*参照してください。配置された*web.config*ファイル自体には、FTP を使用してアクセスできます。 手順について[は、「ASP.NET Web Deployment using Visual Studio」を参照してください。コードの更新](xref:web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update)を配置します。 「FTP ツールを使用するには」で始まる指示に従って、FTP URL、ユーザー名、およびパスワードの3つが必要になります。

> [!NOTE]
> Web アプリはセキュリティを実装していないので、URL を見つけたすべてのユーザーがデータを変更できます。 Web サイトをセキュリティで保護する方法については、「[メンバーシップ、OAuth、SQL database を使用した secure ASP.NET MVC アプリの Azure へのデプロイ](/aspnet/core/security/authorization/secure-data)」を参照してください。 Azure 管理ポータルまたは Visual Studio で**サーバーエクスプローラー**を使用してサービスを停止することで、他のユーザーがサイトを使用できないようにすることができます。

![App service メニュー項目の停止](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/_static/server-explorer-stop-app-service.png)

## <a name="advanced-migrations-scenarios"></a>高度な移行シナリオ

このチュートリアルに示されているように、移行を自動的に実行してデータベースを配置し、複数のサーバーで実行される web サイトに配置する場合は、複数のサーバーが同時に移行を実行しようとする可能性があります。 移行はアトミックであるため、2台のサーバーが同じ移行を実行しようとすると、1つが成功し、もう一方は失敗します (操作を2回実行することはできません)。 このような問題を回避する場合は、手動で移行を呼び出し、独自のコードを設定して1回だけ発生するようにします。 詳細については、「Rowan 明美のブログの[コードからの移行の実行とスクリプト作成](http://romiller.com/2012/02/09/running-scripting-migrations-from-code/)」と「 [.exe](/ef/ef6/modeling/code-first/migrations/migrate-exe) (コマンドラインからの移行の実行用)」を参照してください。

その他の移行シナリオの詳細については、「[スクリーンキャスト Series の移行](https://blogs.msdn.com/b/adonet/archive/2014/03/12/migrations-screencast-series.aspx)」を参照してください。

## <a name="update-specific-migration"></a>特定の移行の更新

`update-database -target MigrationName`

この`update-database -target MigrationName`コマンドは、対象の移行を実行します。

## <a name="ignore-migration-changes-to-database"></a>データベースへの移行の変更を無視する

`Add-migration MigrationName -ignoreChanges`

`ignoreChanges`現在のモデルをスナップショットとして使用して、空の移行を作成します。

## <a name="code-first-initializers"></a>Code First 初期化子

[デプロイ] セクションでは、Migrateに使用されている、 [migrateの](https://msdn.microsoft.com/library/hh829476(v=vs.103).aspx)ユーザー初期化子があることを確認しました。 Code First には、 [Createdatabaseifnotexists](https://msdn.microsoft.com/library/gg679221(v=vs.103).aspx) (既定)、 [Dropcreatedatabaseifmodelchanges](https://msdn.microsoft.com/library/gg679604(v=VS.103).aspx) (前に使用したもの)、 [dropcreatedatabasealways](https://msdn.microsoft.com/library/gg679506(v=VS.103).aspx)など、他の初期化子も用意されています。 初期化`DropCreateAlways`子は、単体テストの条件を設定する場合に役立ちます。 独自の初期化子を記述することもできます。また、アプリケーションがデータベースに対して読み取りまたは書き込みを行うまで待機しない場合は、初期化子を明示的に呼び出すことができます。

初期化子の詳細については、「 [Entity Framework Code First でのデータベース初期化子](http://www.codeguru.com/csharp/article.php/c19999/Understanding-Database-Initializers-in-Entity-Framework-Code-First.htm)につい[て」および「書籍プログラミング Entity Framework」の第6章を参照してください。ジュリー](http://shop.oreilly.com/product/0636920022220.do) Lerman と rowan 明美によって Code First ます。

## <a name="get-the-code"></a>コードを取得する

[完成したプロジェクトをダウンロードする](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a>その他の技術情報

その他の Entity Framework リソースへのリンクについては[、「ASP.NET Data Access-推奨リソース](xref:whitepapers/aspnet-data-access-content-map)」を参照してください。

## <a name="next-steps"></a>次の手順

このチュートリアルでは、次の作業を行いました。

> [!div class="checklist"]
> * Code First 移行を有効にする
> * Azure にアプリをデプロイしました (省略可能)

次の記事に進み、ASP.NET MVC アプリケーション用により複雑なデータモデルを作成する方法を学習してください。
> [!div class="nextstepaction"]
> [より複雑なデータモデルを作成する](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)
