---
uid: identity/overview/getting-started/aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider
title: 'ASP.NET Identity: EntityFramework MySQL プロバイダーで MySQL ストレージを使用するC#()-ASP.NET 4.x'
author: maumar
description: このチュートリアルでは、ASP.NET Identity の既定のデータストレージ機構を EntityFramework (SQL クライアントプロバイダー) に置き換えて、MySQL プロバイダーに置き換える方法について説明します。
ms.author: riande
ms.date: 12/10/2013
ms.assetid: 15253312-a92c-43ba-908e-b5dacd3d08b8
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/getting-started/aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider
msc.type: authoredcontent
ms.openlocfilehash: e89ed139657c5ce9ddcc56879946c62038919483
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78471874"
---
# <a name="aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider-c"></a>ASP.NET Identity:EntityFramework MySQL プロバイダーで MySQL ストレージを使用する (C#)

[Maurycy Markowski](https://github.com/maumar)、 [Raquel Soares De Almeida](https://github.com/raquelsa)、 [Robert mcmurray](https://github.com/rmcmurray)

> このチュートリアルでは、 [**ASP.NET Identity**](introduction-to-aspnet-identity.md)の既定のデータストレージ機構を entityframework (SQL クライアントプロバイダー) に置き換える方法について説明します。

このチュートリアルでは、次のトピックについて説明します。

- Azure での MySQL データベースの作成
- Visual Studio 2013 MVC テンプレートを使用した MVC アプリケーションの作成
- MySQL データベースプロバイダーを使用するための EntityFramework の構成
- アプリケーションを実行して結果を確認する

このチュートリアルの最後には、Azure でホストされている MySQL データベースを使用する ASP.NET Identity ストアを含む MVC アプリケーションが作成されます。

## <a name="creating-a-mysql-database-instance-on-azure"></a>Azure での MySQL データベースインスタンスの作成

1. [Azure Portal](https://go.microsoft.com/fwlink/?linkid=529715&amp;clcid=0x409) にログインします。
2. ページの下部にある **[新規]** をクリックし、 **[ストア]** を選択します。

    [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image2.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image1.png)
3. **選択とアドオン**ウィザードで、 **[ClearDB MySQL Database]** を選択し、フレームの下部にある**次へ進む**矢印をクリックします。

   [次の画像をクリックして展開します。 ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image4.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image3.png)
4. 既定の**Free**プランをそのまま使用し、**名前**を「**識別子**」に変更し、最も近いリージョンを選択して、フレームの下部にある**次へ進む**矢印をクリックします。

   [次の画像をクリックして展開します。 ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image6.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image5.png)
5. **[購入]** チェックマークをクリックして、データベースの作成を完了します。

   [次の画像をクリックして展開します。 ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image8.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image7.png)
6. データベースが作成されたら、管理ポータルの **[アドオン]** タブから管理できます。 データベースの接続情報を取得するには、ページの下部にある [**接続**情報] をクリックします。

   [次の画像をクリックして展開します。 ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image10.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image9.png)
7. **[CONNECTIONSTRING]** フィールドの [コピー] ボタンをクリックして接続文字列をコピーし、保存します。この情報は、このチュートリアルの後半で MVC アプリケーションに使用します。

   [次の画像をクリックして展開します。 ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image12.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image11.png)

## <a name="creating-an-mvc-application-project"></a>MVC アプリケーションプロジェクトの作成

チュートリアルのこのセクションの手順を完了するには、最初に Web 用または[Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566)[用の Visual Studio Express 2013](https://go.microsoft.com/fwlink/?LinkId=299058)をインストールする必要があります。 Visual Studio をインストールしたら、次の手順に従って、新しい MVC アプリケーションプロジェクトを作成します。

1. Visual Studio 2103 を開きます。
2. **スタート**ページで **[新しいプロジェクト]** をクリックするか、 **[ファイル]** メニューの **[新しいプロジェクト]** をクリックします。

   [次の画像をクリックして展開します。 ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image2.jpg)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image1.jpg)
3. **[新しいプロジェクト]** ダイアログボックスが表示されたら、テンプレートの一覧で **[ビジュアルC# ]** を展開し、 **[web]** をクリックして、 **[ASP.NET Web Application]** を選択します。 プロジェクトに「**識別子**」という名前を入力し、[ **OK]** をクリックします。

   [次の画像をクリックして展開します。 ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image14.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image13.png)
4. **[New ASP.NET プロジェクト]** ダイアログボックスで、既定のオプションを使用して**MVC**テンプレートを選択します。これにより、**個々のユーザーアカウント**が認証方法として構成されます。 **[OK]** をクリックします。

   [次の画像をクリックして展開します。 ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image16.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image15.png)

## <a name="configure-entityframework-to-work-with-a-mysql-database"></a>MySQL データベースを使用するように EntityFramework を構成する

### <a name="update-the-entity-framework-assembly-for-your-project"></a>プロジェクトの Entity Framework アセンブリを更新する

Visual Studio 2013 テンプレートから作成された MVC アプリケーションには[Entityframework 6.0.0](http://www.nuget.org/packages/EntityFramework)パッケージへの参照が含まれていますが、このアセンブリのリリース以降、大幅なパフォーマンスの改善が行われています。 アプリケーションでこれらの最新の更新プログラムを使用するには、次の手順を使用します。

1. Visual Studio で MVC プロジェクトを開きます。
2. **[ツール]** 、 **[NuGet パッケージマネージャー]** 、 **[パッケージマネージャーコンソール]** の順にクリックします。

   [次の画像をクリックして展開します。 ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image18.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image17.png)
3. **パッケージマネージャーコンソール**は、Visual Studio の下部セクションに表示されます。 「&quot;**更新-Package EntityFramework**&quot;」と入力し、enter キーを押します。

   [次の画像をクリックして展開します。 ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image20.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image19.png)

### <a name="install-the-mysql-provider-for-entityframework"></a>EntityFramework 用の MySQL プロバイダーをインストールする

EntityFramework を MySQL database に接続するには、MySQL プロバイダーをインストールする必要があります。 これを行うには、**パッケージマネージャーコンソール**を開き、「&quot;**Install-package-Pre**&quot;」と入力して、enter キーを押します。

> [!NOTE]
> これは、アセンブリのプレリリースバージョンであり、バグが含まれている可能性があります。 実稼働環境では、プレリリース版のプロバイダーを使用しないでください。

[次の画像をクリックして展開します。]

[![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image22.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image21.png)

### <a name="making-project-configuration-changes-to-the-webconfig-file-for-your-application"></a>アプリケーションの web.config ファイルに対するプロジェクト構成の変更

このセクションでは、インストールしたばかりの MySQL プロバイダーを使用するように Entity Framework を構成し、MySQL プロバイダーファクトリを登録して、Azure から接続文字列を追加します。

> [!NOTE]
> 次の例には、MySql の特定のアセンブリバージョンが含まれています。 アセンブリのバージョンが変更された場合は、正しいバージョンを使用して適切な構成設定を変更する必要があります。

1. Visual Studio 2013 でプロジェクトの web.config ファイルを開きます。
2. 次の構成設定を見つけて、Entity Framework の既定のデータベースプロバイダーとファクトリを定義します。

    [!code-xml[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample1.xml)]
3. これらの構成設定を次のように置き換えます。これにより、MySQL プロバイダーを使用するように Entity Framework が構成されます。

    [!code-xml[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample2.xml)]
4. &lt;connectionStrings&gt; セクションを見つけ、次のコードに置き換えます。これにより、Azure でホストされている MySQL データベースの接続文字列が定義されます (providerName 値も元のものから変更されていることに注意してください)。

    [!code-xml[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample3.xml?highlight=3-4)]

### <a name="adding-custom-migrationhistory-context"></a>カスタム MigrationHistory コンテキストの追加

Entity Framework Code First では、モデルの変更を追跡し、データベーススキーマと概念スキーマ間の一貫性を確保するために、 **MigrationHistory**テーブルを使用します。 ただし、このテーブルは、既定では、主キーが大きすぎるため、MySQL では機能しません。 この状況を解決するには、そのテーブルのキーサイズを縮小する必要があります。 そのためには、次の手順を実行してください。

1. このテーブルのスキーマ情報は、他の**dbcontext**として変更できる**履歴コンテキスト**でキャプチャされます。 これを行うには、 **MySqlHistoryContext.cs**という名前の新しいクラスファイルをプロジェクトに追加し、その内容を次のコードに置き換えます。

    [!code-csharp[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample4.cs)]
2. 次に、既定の設定ではなく、変更された**履歴コンテキスト**を使用するように Entity Framework を構成する必要があります。 これは、コードベースの構成機能を利用して行うことができます。 これを行うには、 **MySqlConfiguration.cs**という名前の新しいクラスファイルをプロジェクトに追加し、その内容を次のように置き換えます。

    [!code-csharp[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample5.cs)]

### <a name="creating-a-custom-entityframework-initializer-for-applicationdbcontext"></a>ApplicationDbContext のカスタム EntityFramework 初期化子を作成しています

このチュートリアルで紹介されている MySQL プロバイダーは、現在 Entity Framework の移行をサポートしていません。そのため、データベースに接続するには、モデル初期化子を使用する必要があります。 このチュートリアルでは Azure で MySQL インスタンスを使用しているため、カスタム Entity Framework 初期化子を作成する必要があります。

> [!NOTE]
> Azure 上の SQL Server インスタンスに接続している場合や、オンプレミスでホストされているデータベースを使用している場合は、この手順は必要ありません。

MySQL のカスタム Entity Framework 初期化子を作成するには、次の手順に従います。

1. **MySqlInitializer.cs**という名前の新しいクラスファイルをプロジェクトに追加し、その内容を次のコードに置き換えます。

    [!code-csharp[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample6.cs?highlight=23)]
2. **[モデル]** ディレクトリにあるプロジェクトの**IdentityModels.cs**ファイルを開き、その内容を次のように置き換えます。

    [!code-csharp[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample7.cs)]

## <a name="running-the-application-and-verifying-the-database"></a>アプリケーションを実行してデータベースを確認する

前のセクションの手順を完了したら、データベースをテストする必要があります。 そのためには、次の手順を実行してください。

1. Ctrl キーを押し**ながら F5**キーを押して、web アプリケーションをビルドして実行します。
2. ページの上部にある **[登録]** タブをクリックします。

   [次の画像をクリックして展開します。 ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image4.jpg)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image3.jpg)
3. 新しいユーザー名とパスワードを入力し、[Register] \ (**登録**\) をクリックします。

   [次の画像をクリックして展開します。 ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image24.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image23.png)
4. この時点で、ASP.NET Identity テーブルが MySQL データベースに作成され、ユーザーが登録されてアプリケーションにログインされます。

   [次の画像をクリックして展開します。 ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image6.jpg)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image5.jpg)

### <a name="installing-mysql-workbench-tool-to-verify-the-data"></a>MySQL ワークベンチツールをインストールしてデータを検証する

1. Mysql の[ダウンロードページ](http://dev.mysql.com/downloads/windows/installer/)から**mysql ワークベンチ**ツールをインストールする
2. インストールウィザードの **[機能の選択]** タブで、 **[アプリケーション]** セクションの **[MySQL ワークベンチ]** を選択します。
3. このチュートリアルの懇願で作成した Azure MySQL データベースの接続文字列データを使用して、アプリを起動し、新しい接続を追加します。
4. 接続を確立した後、**識別子 Tymysqldatabase**で作成された**ASP.NET Identity**テーブルを調べます。
5. 次の図に示すように、すべての ASP.NET Identity 必要なテーブルが作成されます。

   [次の画像をクリックして展開します。 ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image8.jpg)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image7.jpg)
6. インスタンスの**aspnetusers**テーブルを調べて、新しいユーザーを登録するときにエントリがあるかどうかを確認します。

   [次の画像をクリックして展開します。 ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image26.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image25.png)
