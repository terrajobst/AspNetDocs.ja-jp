---
uid: identity/overview/extensibility/implementing-a-custom-mysql-aspnet-identity-storage-provider
title: カスタム MySQL ASP.NET Identity ストレージプロバイダーの実装-ASP.NET 4.x
author: raquelsa
description: ASP.NET Identity は拡張可能なシステムです。これを使用すると、独自の記憶域プロバイダーを作成し、アプリケーションにプラグインできます。
ms.author: riande
ms.date: 05/22/2015
ms.assetid: 248f5fe7-39ba-40ea-ab1e-71a69b0bd649
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/extensibility/implementing-a-custom-mysql-aspnet-identity-storage-provider
msc.type: authoredcontent
ms.openlocfilehash: 2f0b47d45bce82c71d1864536309f9e2ffed2d63
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78500068"
---
# <a name="implementing-a-custom-mysql-aspnet-identity-storage-provider"></a>カスタム MySQL ASP.NET Identity ストレージ プロバイダーの実装

[Raquel Soares De Almeida](https://github.com/raquelsa)、 [suhas Joshi](https://github.com/suhasj)、 [Tom fitzmacken](https://github.com/tfitzmac)

> ASP.NET Identity は拡張可能なシステムで、アプリケーションを再実行することなく、独自の記憶域プロバイダーを作成してアプリケーションに組み込むことができます。 このトピックでは、ASP.NET Identity 用の MySQL 記憶域プロバイダーを作成する方法について説明します。 カスタム記憶域プロバイダーの作成の概要については、「 [ASP.NET Identity 用のカスタム記憶域プロバイダーの概要](overview-of-custom-storage-providers-for-aspnet-identity.md)」を参照してください。
> 
> このチュートリアルを完了するには、Update 2 の Visual Studio 2013 が必要です。
> 
> このチュートリアルでは次のことを行います。
> 
> - Azure で MySQL データベースインスタンスを作成する方法について説明します。
> - MySQL クライアントツール (MySQL ワークベンチ) を使用してテーブルを作成し、Azure でリモートデータベースを管理する方法について説明します。
> - MVC アプリケーションプロジェクトで既定の ASP.NET Identity ストレージの実装をカスタム実装に置き換える方法について説明します。
> 
> このチュートリアルは、もともと Raquel Soares De Almeida と Rick Anderson ( [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) ) によって作成されました。 サンプルプロジェクトは、Suhas Joshi によって Id 2.0 に更新されました。 このトピックは、Tom FitzMacken によって Id 2.0 に対して更新されました。

## <a name="download-completed-project"></a>完成したプロジェクトのダウンロード

このチュートリアルの最後には、Azure でホストされている MySQL データベースを使用して ASP.NET Identity 使用する MVC アプリケーションプロジェクトが作成されます。

完成した MySQL ストレージプロバイダーは、 [AspNet. Identity. MySQL (GitHub)](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/AspNet.Identity.MySQL)からダウンロードできます。

## <a name="the-steps-you-will-perform"></a>実行する手順

このチュートリアルでは、次のことについて説明します。

1. Azure で MySQL データベースを作成する
2. MySQL で ASP.NET Identity テーブルを作成する
3. MVC アプリケーションを作成し、MySQL プロバイダーを使用するように構成する
4. アプリを実行する

このトピックでは、ASP.NET Identity のアーキテクチャと、お客様のストレージプロバイダーを実装するときに行う必要がある決定事項については説明しません。 詳細については、「 [ASP.NET Identity 用のカスタム記憶域プロバイダーの概要](overview-of-custom-storage-providers-for-aspnet-identity.md)」を参照してください。

## <a name="review-mysql-storage-provider-classes"></a>MySQL ストレージプロバイダークラスの確認

MySQL 記憶域プロバイダーを作成する手順に進む前に、記憶域プロバイダーを構成するクラスを見てみましょう。 ユーザーとロールを管理するには、アプリケーションから呼び出されるデータベース操作とクラスを管理するクラスが必要です。

### <a name="storage-classes"></a>ストレージ クラス

- [[ユーザー](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/IdentityUser.cs) ]-ユーザーのプロパティが含まれます。
- [Userstore](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserStore.cs) -ユーザーを追加、更新、または取得するための操作が含まれています。
- "Identity [role](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/IdentityRole.cs) "-ロールのプロパティが含まれます。
- [Rolestore](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/RoleStore.cs) -ロールを追加、削除、更新、および取得するための操作が含まれています。

### <a name="data-access-layer-classes"></a>データアクセス層クラス

この例では、データアクセス層クラスにテーブルを操作するための SQL ステートメントが含まれています。ただし、コードでは、Entity Framework や NHibernate などのオブジェクトリレーショナルマッピング (ORM) を使用することもできます。 特に、遅延読み込みとオブジェクトキャッシュを含む ORM を使用しないと、アプリケーションのパフォーマンスが低下する可能性があります。 詳細については、「 [Entity Framework のない ASP.NET Identity 2.0](https://aspnetidentity.codeplex.com/discussions/561828) 」を参照してください。

- [MySQLDatabase](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/MySQLDatabase.cs) -MySQL データベース接続と、データベース操作を実行するためのメソッドが含まれています。 UserStore と RoleStore は、どちらもこのクラスのインスタンスでインスタンス化されます。
- [Roletable](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/RoleTable.cs) -ロールを格納するテーブルのデータベース操作が含まれます。
- [Userclaimstable](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserClaimsTable.cs) -ユーザー要求を格納するテーブルのデータベース操作が含まれます。
- [UserLoginsTable](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserLoginsTable.cs) -ユーザーのログイン情報を格納するテーブルのデータベース操作を格納します。
- [Userroletable](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserRoleTable.cs) -どのユーザーがどのロールに割り当てられているかを格納するテーブルのデータベース操作が含まれます。
- [Usertable](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserTable.cs) -ユーザーを格納するテーブルのデータベース操作が含まれます。

## <a name="create-a-mysql-database-instance-on-azure"></a>Azure で MySQL データベースインスタンスを作成する

1. [Azure Portal](https://manage.windowsazure.com/) にログインします。
2. ページの下部にある **[+ 新規]** をクリックし、 **[ストア]** を選択します。  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image1.png)
3. **選択とアドオン**ウィザードで、 **[ClearDB MySQL Database]** を選択し、ダイアログの右下にある次へ進む矢印をクリックします。  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image2.png)
4. 既定の**Free**プランをそのままにして、**名前**を「**識別子**」に変更します。 最も近いリージョンを選択し、次へ進む矢印をクリックします。  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image3.png)
5. チェックマークをクリックして、データベースの作成を完了します。  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image4.png)
6. データベースが作成されたら、管理ポータルの **[アドオン]** タブから管理できます。   
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image5.png)
7. ページの下部にある **[接続情報]** をクリックすると、データベース接続情報を取得できます。  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image6.png)
8. [コピー] ボタンをクリックして接続文字列をコピーし、MVC アプリケーションで後で使用できるように保存します。   
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image7.png)

## <a name="create-the-aspnet-identity-tables-in-a-mysql-database"></a>MySQL データベースに ASP.NET Identity テーブルを作成する

### <a name="install-mysql-workbench-tool-to-connect-and-manage-mysql-database"></a>Mysql データベースに接続して管理するための MySQL ワークベンチツールのインストール

1. Mysql の[ダウンロードページ](http://dev.mysql.com/downloads/windows/installer/)から**mysql ワークベンチ**ツールをインストールする
2. アプリを起動し、 **[MySQLConnections +]** ボタンをクリックして新しい接続を追加します。 このチュートリアルの前の手順で作成した Azure MySQL データベースからコピーした接続文字列データを使用します。
3. 接続を確立したら、新しい **[クエリ]** タブを開きます。[MySQLIdentity](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/MySQLIdentity.sql)のコマンドをクエリに貼り付けて、データベーステーブルを作成するために実行します。
4. 次に示すように、Azure でホストされている MySQL データベースで、すべての ASP.NET Identity 必要なテーブルが作成されました。  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image1.jpg)

## <a name="create-an-mvc-application-project-from-template-and-configure-it-to-use-mysql-provider"></a>テンプレートから MVC アプリケーションプロジェクトを作成し、MySQL プロバイダーを使用するように構成する

必要に応じて、 [Visual Studio Express 2013 For Web](https://go.microsoft.com/fwlink/?LinkId=299058)または[Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566) Update 2 をインストールします。

### <a name="download-the-aspnetidentitymysql-project-from-github"></a>GitHub から ASP.DLL プロジェクトをダウンロードします。

1. [AspNet. Identity. MySQL (GitHub)](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/AspNet.Identity.MySQL/)でリポジトリの URL を参照します。
2. ソースコードをダウンロードします。
3. ローカルフォルダーに .zip ファイルを抽出します。
4. AspNet. の MySQL ソリューションを開き、ビルドします。

### <a name="create-a-new-mvc-application-project-from-template"></a>テンプレートからの新しい MVC アプリケーションプロジェクトの作成

1. **AspNet. id. MySQL**ソリューションを右クリックし、[**新しいプロジェクト**の**追加**] をクリックします。
2. **[新しいプロジェクトの追加]** ダイアログで、左側の **[ビジュアルC# ]** 、 **[web]** の順に選択し、 **[ASP.NET web Application]** を選択します。 **プロジェクトに**名前を指定します。[OK] をクリックします。  
  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image2.jpg)
3. **[New ASP.NET プロジェクト]** ダイアログボックスで、既定のオプション (認証方法として**個々のユーザーアカウント**を含む) を使用して MVC テンプレートを選択し、[ **OK]** をクリックします。![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image3.jpg)
4. ソリューションエクスプローラーで、識別子 Tymysqldemo プロジェクトを右クリックし、 **[NuGet パッケージの管理]** を選択します。 [検索テキストボックス] ダイアログボックスで、「 **Identity. EntityFramework**」と入力します。 結果の一覧でこのパッケージを選択し、 **[アンインストール]** をクリックします。 依存関係パッケージ EntityFramework をアンインストールするよう求めるメッセージが表示されます。 [はい] をクリックします。このパッケージは、このアプリケーションではなくなります。
5. 識別子 プロジェクトを右クリックし、**追加**、**参照、ソリューション、プロジェクト** の順に選択し、AspNet プロジェクトを選択して  **OK**をクリックします。
6. 識別子のすべての参照を置き換えます。  
    `using Microsoft.AspNet.Identity.EntityFramework;`  
   with  
     `using AspNet.Identity.MySQL;`
7. IdentityModels.cs で、 **Applicationdbcontext**を**MySqlDatabase**から派生するように設定し、接続名と共に1つのパラメーターを受け取るコンストラクターを含めます。  

    [!code-csharp[Main](implementing-a-custom-mysql-aspnet-identity-storage-provider/samples/sample1.cs)]
8. IdentityConfig.cs ファイルを開きます。 **Applicationusermanager. Create**メソッドで、インスタンス化 usermanager を次のコードに置き換えます。  

    [!code-csharp[Main](implementing-a-custom-mysql-aspnet-identity-storage-provider/samples/sample2.cs)]
9. Web.config ファイルを開き、DefaultConnection 文字列を次のエントリに置き換えて、強調表示された値を、前の手順で作成した MySQL データベースの接続文字列に置き換えます。  

    [!code-xml[Main](implementing-a-custom-mysql-aspnet-identity-storage-provider/samples/sample3.xml?highlight=2)]

## <a name="run-the-app-and-connect-to-the-mysql-db"></a>アプリを実行して MySQL DB に接続する

1. **[識別子]** を右クリックし、 **[スタートアッププロジェクトに設定]** を選択します。
2. Ctrl キーを押し**ながら F5**キーを押して、アプリをビルドして実行します。
3. ページの上部にある [Register] \ (**登録**\) タブをクリックします。
4. 新しいユーザー名とパスワードを入力し、[Register] \ (**登録**\) をクリックします。  
  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image8.png)
5. これで、新しいユーザーが登録され、ログインされました。  
  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image9.png)
6. MySQL ワークベンチツールに戻り、**識別子 Tymysqldatabase**の内容を調べます。 新しいユーザーを登録するときに、ユーザーテーブルでエントリを調べます。  
  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image10.png)

## <a name="next-steps"></a>次の手順

このアプリで他の認証方法を有効にする方法の詳細については、「 [Facebook と Google OAuth2 を使用した ASP.NET MVC 5 アプリの作成」と「OpenID サインオン](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)」を参照してください。

DB と OAuth を統合し、ユーザーがアプリへのアクセスを制限するロールを設定する方法については、「 [Azure へのメンバーシップ、OAuth、および SQL Database を使用した Secure ASP.NET MVC 5 アプリのデプロイ](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)」を参照してください。
