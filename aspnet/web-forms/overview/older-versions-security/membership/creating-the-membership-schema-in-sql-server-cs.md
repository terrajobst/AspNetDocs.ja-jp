---
uid: web-forms/overview/older-versions-security/membership/creating-the-membership-schema-in-sql-server-cs
title: SQL Server (C#) でメンバーシップスキーマを作成するMicrosoft Docs
author: rick-anderson
description: このチュートリアルでは、まず、SqlMembershipProvider を使用するために必要なスキーマをデータベースに追加する方法を調べます。 その後、私たちは...
ms.author: riande
ms.date: 01/18/2008
ms.assetid: b4ac129d-1b8e-41ca-a38f-9b19d7c7bb0e
msc.legacyurl: /web-forms/overview/older-versions-security/membership/creating-the-membership-schema-in-sql-server-cs
msc.type: authoredcontent
ms.openlocfilehash: 97623e7c13ab7799b9dadbb8e52be8e0cd99e252
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78464440"
---
# <a name="creating-the-membership-schema-in-sql-server-c"></a>SQL Server でメンバーシップ スキーマを作成する (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[コードのダウンロード](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/ASPNET_Security_Tutorial_04_CS.zip)または[PDF のダウンロード](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/aspnet_tutorial04_MembershipSetup_cs.pdf)

> このチュートリアルでは、まず、SqlMembershipProvider を使用するために必要なスキーマをデータベースに追加する方法を調べます。 ここでは、スキーマの主要なテーブルを調べ、その目的と重要性について説明します。 このチュートリアルでは、メンバーシップフレームワークが使用するプロバイダーを ASP.NET アプリケーションに通知する方法について説明します。

## <a name="introduction"></a>はじめに

前の2つのチュートリアルでは、フォーム認証を使用して web サイトの訪問者を識別しています。 フォーム認証フレームワークを使用すると、開発者は、ユーザーを web サイトに簡単に記録し、認証チケットを使用してページにアクセスしてそれらを記憶することが容易になります。 `FormsAuthentication` クラスには、チケットを生成して訪問者の cookie に追加するためのメソッドが含まれています。 `FormsAuthenticationModule` は、すべての受信要求を調べ、有効な認証チケットがある場合は、`GenericPrincipal` と `FormsIdentity` オブジェクトを作成し、現在の要求に関連付けます。 フォーム認証は、ログイン時に訪問者に認証チケットを付与するメカニズムであり、後続の要求ではそのチケットを解析してユーザーの id を決定します。 Web アプリケーションでユーザーアカウントをサポートするには、ユーザーストアを実装し、資格情報を検証し、新しいユーザーを登録し、その他のユーザーアカウント関連タスクを無数に登録する機能を追加する必要があります。

ASP.NET 2.0 より前の開発者は、これらのユーザーアカウント関連のタスクをすべて実装するためのフックを使用していました。 幸い、ASP.NET チームはこの欠点を認識し、ASP.NET 2.0 を使用してメンバーシップフレームワークを導入しました。 メンバーシップフレームワークは、ユーザーアカウント関連の主要なタスクを実現するためのプログラムインターフェイスを提供する、.NET Framework のクラスのセットです。 このフレームワークは、[プロバイダーモデル](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx)の上に構築されています。これにより、開発者は、カスタマイズされた実装を標準化された API に組み込むことができます。

<a id="Tutorial1"> </a>[*セキュリティの基本と ASP.NET のサポート*](../introduction/security-basics-and-asp-net-support-cs.md)に関するチュートリアルで説明したように、.NET Framework には、 [`ActiveDirectoryMembershipProvider`](https://msdn.microsoft.com/library/system.web.security.activedirectorymembershipprovider.aspx)と[`SqlMembershipProvider`](https://msdn.microsoft.com/library/system.web.security.sqlmembershipprovider.aspx)という2つの組み込みのメンバーシッププロバイダーが付属しています。 その名前が示すように、`SqlMembershipProvider` では、ユーザーストアとして Microsoft SQL Server データベースが使用されます。 アプリケーションでこのプロバイダーを使用するには、ストアとして使用するデータベースをプロバイダーに指示する必要があります。 ご想像のとおり、`SqlMembershipProvider` では、ユーザーストアデータベースに特定のデータベーステーブル、ビュー、およびストアドプロシージャが含まれていることを想定しています。 この予想されるスキーマを選択したデータベースに追加する必要があります。

このチュートリアルでは、まず、`SqlMembershipProvider`を使用するために必要なスキーマをデータベースに追加する方法を調べます。 ここでは、スキーマの主要なテーブルを調べ、その目的と重要性について説明します。 このチュートリアルでは、メンバーシップフレームワークが使用するプロバイダーを ASP.NET アプリケーションに通知する方法について説明します。

作業開始

## <a name="step-1-deciding-where-to-place-the-user-store"></a>手順 1: ユーザーストアを配置する場所を決定する

ASP.NET アプリケーションのデータは、通常、データベース内の複数のテーブルに格納されます。 `SqlMembershipProvider` データベーススキーマを実装する場合は、メンバーシップスキーマをアプリケーションデータと同じデータベースに配置するか、別のデータベースに配置するかを決定する必要があります。

次の理由から、アプリケーションデータと同じデータベースにメンバーシップスキーマを配置することをお勧めします。

- **保守性**データが1つのデータベースにカプセル化されたアプリケーションは、2つの異なるデータベースを持つアプリケーションよりも理解、保守、配置が容易になります。
- **リレーショナル整合性**: メンバーシップ関連テーブルをアプリケーションテーブルと同じデータベース内に配置することによって、メンバーシップ関連テーブルと関連アプリケーションテーブルの主キーの間に[外部キー制約](http://en.wikipedia.org/wiki/Foreign_key)を設定することができます。

ユーザーストアとアプリケーションデータを別々のデータベースに分離することは、それぞれが別々のデータベースを使用し、共通のユーザーストアを共有する必要がある複数のアプリケーションがある場合に、意味があります。

### <a name="creating-a-database"></a>データベースを作成します。

2番目のチュートリアルで作成したアプリケーションは、まだデータベースを必要としていません。 ただし、ここではユーザーストアに対して1つが必要です。 1つを作成し、`SqlMembershipProvider` プロバイダーが必要とするスキーマを追加してみましょう (手順2を参照)。

> [!NOTE]
> このチュートリアルシリーズでは、 [Microsoft SQL Server 2005 Express Edition](https://msdn.microsoft.com/sql/Aa336346.aspx)データベースを使用して、アプリケーションテーブルと `SqlMembershipProvider` スキーマを格納します。 この決定は次の2つの理由で行われました。まず、コストがかからないことから、Express Edition は、SQL Server 2005 の読み取り専用のバージョンです。次に、SQL Server 2005 Express Edition データベースを web アプリケーションの `App_Data` フォルダーに直接配置して、データベースと web アプリケーションを1つの ZIP ファイルにパッケージ化し、特別なセットアップ手順や構成オプションを使用せずに再展開するたいしたを作成できます。 Express Edition 以外のバージョンの SQL Server を使用したい場合は、無料でご利用いただけます。 手順はほぼ同じです。 `SqlMembershipProvider` スキーマは、Microsoft SQL Server 2000 およびそれ以降のすべてのバージョンで動作します。

ソリューションエクスプローラーから、`App_Data` フォルダーを右クリックし、[新しい項目の追加] を選択します。 (プロジェクトに `App_Data` フォルダーが表示されない場合はソリューションエクスプローラーでプロジェクトを右クリックし、[ASP.NET フォルダーの追加] を選択して `App_Data`を選択します)。[新しい項目の追加] ダイアログボックスで、`SecurityTutorials.mdf`という名前の新しい SQL Database を追加することを選択します。 このチュートリアルでは、`SqlMembershipProvider` スキーマをこのデータベースに追加します。以降のチュートリアルでは、アプリケーションデータをキャプチャするための追加のテーブルを作成します。

[SecurityTutorials .mdf データベースという名前の新しい SQL Database を App_Data フォルダーに追加 ![ます。](creating-the-membership-schema-in-sql-server-cs/_static/image2.png)](creating-the-membership-schema-in-sql-server-cs/_static/image1.png)

**図 1**: `SecurityTutorials.mdf` Database という名前の新しい SQL Database を `App_Data` フォルダーに追加する ([クリックすると、フルサイズの画像が表示](creating-the-membership-schema-in-sql-server-cs/_static/image3.png)されます)

`App_Data` フォルダーにデータベースを追加すると、そのデータベースがデータベースエクスプローラービューに自動的に追加されます。 (Express Edition 以外のバージョンの Visual Studio では、データベースエクスプローラーはサーバーエクスプローラーと呼ばれます)。データベースエクスプローラーにアクセスし、先ほど追加した `SecurityTutorials` データベースを展開します。 画面にデータベースエクスプローラーが表示されない場合は、[表示] メニューの [データベースエクスプローラー] をクリックするか、Ctrl + Alt + S キーを押します。 図2に示すように、`SecurityTutorials` データベースは空であり、テーブル、ビュー、およびストアドプロシージャは含まれていません。

[SecurityTutorials データベースが現在空で ![](creating-the-membership-schema-in-sql-server-cs/_static/image5.png)](creating-the-membership-schema-in-sql-server-cs/_static/image4.png)

**図 2**: `SecurityTutorials` データベースは現在空です ([クリックすると、フルサイズの画像が表示](creating-the-membership-schema-in-sql-server-cs/_static/image6.png)されます)

## <a name="step-2-adding-thesqlmembershipproviderschema-to-the-database"></a>手順 2: データベースへの`SqlMembershipProvider`スキーマの追加

`SqlMembershipProvider` には、ユーザーストアデータベースにインストールする特定のテーブル、ビュー、およびストアドプロシージャのセットが必要です。 これらの必要なデータベースオブジェクトは、 [`aspnet_regsql.exe` ツール](https://msdn.microsoft.com/library/ms229862.aspx)を使用して追加できます。 このファイルは `%WINDIR%\Microsoft.Net\Framework\v2.0.50727\` フォルダーにあります。

> [!NOTE]
> `aspnet_regsql.exe` ツールには、コマンドライン機能とグラフィカルユーザーインターフェイスの両方が用意されています。 グラフィカルインターフェイスは、ユーザーにとってわかりやすく、このチュートリアルで検証するものです。 コマンドラインインターフェイスは、ビルドスクリプトや自動テストのシナリオなどで、`SqlMembershipProvider` スキーマの追加を自動化する必要がある場合に便利です。

`aspnet_regsql.exe` ツールは、指定された SQL Server データベースに対して*ASP.NET アプリケーションサービス*を追加または削除するために使用されます。 ASP.NET アプリケーションサービスには、`SqlMembershipProvider` と `SqlRoleProvider`のスキーマと、他の ASP.NET 2.0 フレームワークの SQL ベースのプロバイダーのスキーマが含まれています。 `aspnet_regsql.exe` ツールに2ビットの情報を提供する必要があります。

- アプリケーションサービスを追加または削除するかどうかを指定します。
- アプリケーションサービススキーマの追加または削除の対象となるデータベース

データベースを使用するように求めるメッセージが表示されたら、`aspnet_regsql.exe` ツールで、データベースが存在するサーバーの名前、データベースに接続するためのセキュリティ資格情報、およびデータベース名を入力するように求められます。 Express Edition 以外の SQL Server を使用している場合は、この情報が既にわかっている必要があります。これは、ASP.NET web ページでデータベースを操作するときに接続文字列を使用して入力する必要がある情報と同じです。 ただし、`App_Data` フォルダー内の SQL Server 2005 Express Edition データベースを使用する場合は、サーバーとデータベースの名前を確認することが少し複雑になります。

次のセクションでは、`App_Data` フォルダー内の SQL Server 2005 Express Edition データベースのサーバー名とデータベース名を簡単に指定する方法について説明します。 を使用していない場合は SQL Server 2005 Express Edition 「アプリケーションサービスのインストール」のセクションに進んでください。

### <a name="determining-the-server-and-database-name-for-a-sql-server-2005-express-edition-database-in-theapp_datafolder"></a>`App_Data`フォルダー内の SQL Server 2005 Express Edition データベースのサーバーとデータベース名を確認する

`aspnet_regsql.exe` ツールを使用するには、サーバー名とデータベース名を把握しておく必要があります。 サーバー名が `localhost\InstanceName`。 最も可能性が高いのは、 *InstanceName*が `SQLExpress`です。 ただし、SQL Server 2005 Express Edition 手動でインストールした場合 (つまり、Visual Studio のインストール時に自動的にインストールしなかった場合)、別のインスタンス名を選択した可能性があります。

データベース名は、特定するのが少し厄介です。 通常、`App_Data` フォルダー内のデータベースには、データベースファイルへのパスと共に、[グローバル一意識別子](http://en.wikipedia.org/wiki/Globally_Unique_Identifier)を含むデータベース名が付けられます。 `aspnet_regsql.exe`を使用してアプリケーションサービススキーマを追加するには、このデータベース名を決定する必要があります。

データベース名を確認する最も簡単な方法は、SQL Server Management Studio を使用してデータベース名を調べることです。 SQL Server Management Studio には SQL Server 2005 データベースを管理するためのグラフィカルインターフェイスが用意されていますが、SQL Server 2005 の Express Edition には付属していません。 SQL Server Management Studio の無償 Express Edition を[ダウンロードでき](https://www.microsoft.com/downloads/details.aspx?FamilyId=C243A5AE-4BD1-4E3D-94B8-5A0F62BF7796&amp;displaylang=en)ます。

> [!NOTE]
> また、Express Edition 以外の SQL Server 2005 がデスクトップにインストールされている場合は、Management Studio の完全バージョンがインストールされている可能性があります。 完全バージョンを使用してデータベース名を決定するには、次に示す Express Edition の手順に従います。

まず、Visual studio を終了して、データベースファイル上の Visual Studio によって設定されたロックが閉じられていることを確認します。 次に、SQL Server Management Studio を起動して、SQL Server 2005 Express Edition の `localhost\InstanceName` データベースに接続します。 既に説明したように、インスタンス名は `SQLExpress`である可能性があります。 [認証] オプションで、[Windows 認証] を選択します。

[SQL Server 2005 Express Edition インスタンスに接続 ![には](creating-the-membership-schema-in-sql-server-cs/_static/image8.png)](creating-the-membership-schema-in-sql-server-cs/_static/image7.png)

**図 3**: SQL Server 2005 Express Edition インスタンスに接続する ([クリックすると、フルサイズの画像が表示](creating-the-membership-schema-in-sql-server-cs/_static/image9.png)されます)

SQL Server 2005 Express Edition インスタンスに接続すると、データベース、セキュリティ設定、サーバーオブジェクトなどのフォルダーが Management Studio に表示されます。 [データベース] タブを展開すると、データベースインスタンスに `SecurityTutorials.mdf` データベースが登録されて*いない*ことがわかります。最初にデータベースをアタッチする必要があります。

[データベース] フォルダーを右クリックし、コンテキストメニューの [アタッチ] をクリックします。 これにより、[データベースのアタッチ] ダイアログボックスが表示されます。 ここで、[追加] ボタンをクリックして `SecurityTutorials.mdf` データベースを参照し、[OK] をクリックします。 図4は、`SecurityTutorials.mdf` データベースが選択された後の [データベースのアタッチ] ダイアログボックスを示しています。 図5は、データベースが正常にアタッチされた後の Management Studio のオブジェクトエクスプローラーを示しています。

[SecurityTutorials .mdf データベースをアタッチ ![には](creating-the-membership-schema-in-sql-server-cs/_static/image11.png)](creating-the-membership-schema-in-sql-server-cs/_static/image10.png)

**図 4**: `SecurityTutorials.mdf` データベースをアタッチ[する (クリックすると、フルサイズの画像が表示](creating-the-membership-schema-in-sql-server-cs/_static/image12.png)されます)

[![データベースフォルダーに SecurityTutorials .mdf データベースが表示されます。](creating-the-membership-schema-in-sql-server-cs/_static/image14.png)](creating-the-membership-schema-in-sql-server-cs/_static/image13.png)

**図 5**: `SecurityTutorials.mdf` データベースが Databases フォルダーに表示される ([クリックすると、フルサイズの画像が表示](creating-the-membership-schema-in-sql-server-cs/_static/image15.png)されます)

図5に示すように、`SecurityTutorials.mdf` データベースの名前は abstruse になります。 覚えやすい名前に変更してください (より簡単な型)。 データベースを右クリックし、コンテキストメニューから [名前の変更] を選択して、名前を `SecurityTutorialsDatabase`に変更します。 このようにしても、ファイル名は変更されません。データベースが SQL Server するために使用する名前だけが変更されます。

[データベースの名前を SecurityTutorialsDatabase に変更 ![には](creating-the-membership-schema-in-sql-server-cs/_static/image17.png)](creating-the-membership-schema-in-sql-server-cs/_static/image16.png)

**図 6**: データベースの名前を `SecurityTutorialsDatabase`に変更する ([クリックすると、フルサイズの画像が表示](creating-the-membership-schema-in-sql-server-cs/_static/image18.png)されます)

この時点で、`SecurityTutorials.mdf` データベースファイルのサーバー名とデータベース名 (`localhost\InstanceName` と `SecurityTutorialsDatabase`) がわかります。 これで、`aspnet_regsql.exe` ツールを使用してアプリケーションサービスをインストールする準備が整いました。

### <a name="installing-the-application-services"></a>アプリケーションサービスのインストール

`aspnet_regsql.exe` ツールを起動するには、[スタート] メニューにアクセスし、[実行] を選択します。 テキストボックスに `%WINDIR%\Microsoft.Net\Framework\v2.0.50727\aspnet_regsql.exe` を入力し、[OK] をクリックします。 または、エクスプローラーを使用して適切なフォルダーにドリルダウンし、`aspnet_regsql.exe` ファイルをダブルクリックすることもできます。 どちらの方法でも、同じ結果が得られます。

コマンドライン引数を指定せずに `aspnet_regsql.exe` ツールを実行すると、ASP.NET SQL Server セットアップウィザードのグラフィカルユーザーインターフェイスが起動します。 ウィザードを使用すると、指定したデータベースの ASP.NET アプリケーションサービスを簡単に追加または削除できます。 図7に示すように、ウィザードの最初の画面には、ツールの目的が示されています。

[ASP.NET SQL Server セットアップウィザードを使用して、メンバーシップスキーマを追加 ![](creating-the-membership-schema-in-sql-server-cs/_static/image20.png)](creating-the-membership-schema-in-sql-server-cs/_static/image19.png)

**図 7**: ASP.NET SQL Server セットアップウィザードを使用してメンバーシップスキーマを追加する ([クリックすると、フルサイズの画像が表示](creating-the-membership-schema-in-sql-server-cs/_static/image21.png)されます)

ウィザードの2番目の手順では、アプリケーションサービスを追加するのか削除するのかを確認するメッセージが表示されます。 `SqlMembershipProvider`に必要なテーブル、ビュー、ストアドプロシージャを追加する必要があるので、[アプリケーションサービスの SQL Server を構成する] オプションを選択します。 後で、データベースからこのスキーマを削除する場合は、このウィザードを再実行しますが、代わりに [既存のデータベースからアプリケーションサービス情報を削除する] オプションを選択します。

[![[アプリケーションサービスの SQL Server を構成する] オプションを選択します。](creating-the-membership-schema-in-sql-server-cs/_static/image23.png)](creating-the-membership-schema-in-sql-server-cs/_static/image22.png)

**図 8**: [アプリケーションサービスの SQL Server を構成する] オプションを選択[する (クリックすると、フルサイズの画像が表示](creating-the-membership-schema-in-sql-server-cs/_static/image24.png)されます)

3番目の手順では、データベース情報の入力が求められます。これには、サーバー名、認証情報、およびデータベース名が表示されます。 このチュートリアルに従っていて、`SecurityTutorials.mdf` データベースを `App_Data`に追加し、`localhost\InstanceName`にアタッチして、名前を `SecurityTutorialsDatabase`に変更した場合は、次の値を使用します。

- サーバー: `localhost\InstanceName`
- Windows 認証
- データベース: `SecurityTutorialsDatabase`

[データベース情報を入力 ![には](creating-the-membership-schema-in-sql-server-cs/_static/image26.png)](creating-the-membership-schema-in-sql-server-cs/_static/image25.png)

**図 9**: データベース情報を入力[する (クリックすると、フルサイズの画像が表示](creating-the-membership-schema-in-sql-server-cs/_static/image27.png)されます)

データベース情報を入力したら、[次へ] をクリックします。 最後の手順では、実行される手順の概要を示します。 [次へ] をクリックしてアプリケーションサービスをインストールし、[完了] をクリックしてウィザードを完了します。

> [!NOTE]
> Management Studio を使用してデータベースをアタッチし、データベースファイルの名前を変更した場合は、Visual Studio を再度開く前に、データベースをデタッチして Management Studio を閉じるようにしてください。 `SecurityTutorialsDatabase` データベースをデタッチするには、データベース名を右クリックし、[タスク] メニューの [デタッチ] をクリックします。

ウィザードが完了したら、Visual Studio に戻り、データベースエクスプローラーに移動します。 [テーブル] フォルダーを展開します。 名前がプレフィックス `aspnet_`で始まる一連のテーブルが表示されます。 同様に、さまざまなビューやストアドプロシージャは、[ビュー] フォルダーと [ストアドプロシージャ] フォルダーにあります。 これらのデータベースオブジェクトは、アプリケーションサービススキーマを構成します。 ここでは、手順 3. でメンバーシップとロール固有のデータベースオブジェクトについて説明します。

[さまざまなテーブル、ビュー、およびストアドプロシージャがデータベースに追加された ![](creating-the-membership-schema-in-sql-server-cs/_static/image29.png)](creating-the-membership-schema-in-sql-server-cs/_static/image28.png)

**図 10**: さまざまなテーブル、ビュー、ストアドプロシージャがデータベースに追加されました ([クリックすると、フルサイズの画像が表示](creating-the-membership-schema-in-sql-server-cs/_static/image30.png)されます)

> [!NOTE]
> `aspnet_regsql.exe` ツールのグラフィカルユーザーインターフェイスによって、アプリケーションサービススキーマ全体がインストールされます。 ただし、コマンドラインから `aspnet_regsql.exe` を実行する場合は、インストールする特定のアプリケーションサービスコンポーネント (または削除) を指定できます。 したがって、`SqlMembershipProvider` および `SqlRoleProvider` プロバイダーに必要なテーブル、ビュー、ストアドプロシージャだけを追加する場合は、コマンドラインから `aspnet_regsql.exe` を実行します。 または、`aspnet_regsql.exe`によって使用される T-sql 作成スクリプトの適切なサブセットを手動で実行することもできます。 これらのスクリプトは、`InstallCommon.sql`、`InstallMembership.sql`、`InstallRoles.sql`、`InstallProfile.sql`、`InstallSqlState.sql`などの名前を持つ `WINDIR%\Microsoft.Net\Framework\v2.0.50727\` フォルダーにあります。

この時点で、`SqlMembershipProvider`に必要なデータベースオブジェクトが作成されました。 ただし、メンバーシップフレームワークに対しては、`SqlMembershipProvider` (`ActiveDirectoryMembershipProvider`) を使用する必要があり、`SqlMembershipProvider` では `SecurityTutorials` データベースを使用する必要があることについても指示する必要があります。 ここでは、使用するプロバイダーを指定する方法と、手順 4. で選択したプロバイダーの設定をカスタマイズする方法について説明します。 しかし、まず、作成したデータベースオブジェクトについて詳しく見ていきましょう。

## <a name="step-3-a-look-at-the-schemas-core-tables"></a>手順 3: スキーマのコアテーブルを確認する

ASP.NET アプリケーションでメンバーシップとロールのフレームワークを使用する場合、実装の詳細はプロバイダーによってカプセル化されます。 今後のチュートリアルでは、これらのフレームワークとのインターフェイスとして、.NET Framework の `Membership` クラスと `Roles` クラスを使用します。 これらの高レベルの Api を使用する場合、実行されるクエリや、`SqlMembershipProvider` および `SqlRoleProvider`によって変更されるテーブルなど、下位レベルの詳細について心配する必要はありません。

これにより、手順2で作成したデータベーススキーマを調べることなく、メンバーシップとロールのフレームワークを自信を持って使用することができます。 ただし、アプリケーションデータを格納するテーブルを作成する場合は、ユーザーまたはロールに関連するエンティティの作成が必要になることがあります。 アプリケーションデータテーブルと手順 2. で作成したテーブルとの間で外部キー制約を確立するときに、`SqlMembershipProvider` スキーマと `SqlRoleProvider` スキーマについての知識を持つことができます。 また、まれに、ユーザーとロールのストアとのインターフェイスを、(`Membership` または `Roles` クラスではなく) データベースレベルで直接行う必要がある場合もあります。

### <a name="partitioning-the-user-store-into-applications"></a>ユーザーストアをアプリケーションにパーティション分割する

メンバーシップとロールのフレームワークは、1人のユーザーとロールストアをさまざまなアプリケーション間で共有できるように設計されています。 メンバーシップまたはロールのフレームワークを使用する ASP.NET アプリケーションでは、使用するアプリケーションパーティションを指定する必要があります。 つまり、複数の web アプリケーションで同じユーザーおよびロールストアを使用できます。 図11は、HRSite、顧客サイト、SalesSite という3つのアプリケーションにパーティション分割されているユーザーとロールのストアを示しています。 これら3つの web アプリケーションはそれぞれ独自のユーザーとロールを持っていますが、ユーザーアカウントとロール情報は、物理的に同じデータベーステーブルに格納されています。

[![のユーザーアカウントが複数のアプリケーションでパーティション分割される場合がある](creating-the-membership-schema-in-sql-server-cs/_static/image32.png)](creating-the-membership-schema-in-sql-server-cs/_static/image31.png)

**図 11**: ユーザーアカウントが複数のアプリケーションでパーティション分割されている場合 ([クリックすると、フルサイズの画像が表示](creating-the-membership-schema-in-sql-server-cs/_static/image33.png)されます)

`aspnet_Applications` テーブルでは、これらのパーティションを定義します。 データベースを使用してユーザーアカウント情報を格納する各アプリケーションは、このテーブルの行によって表されます。 `aspnet_Applications` テーブルには、`ApplicationId`、`ApplicationName`、`LoweredApplicationName`、および `Description`の4つの列があります。 `ApplicationId` は[`uniqueidentifier`](https://msdn.microsoft.com/library/ms187942.aspx)型で、テーブルの主キーです。`ApplicationName` には、アプリケーションごとにわかりやすい一意の名前を指定します。

その他のメンバーシップとロールに関連するテーブルは、`aspnet_Applications`の [`ApplicationId`] フィールドにリンクします。 たとえば、各ユーザーアカウントのレコードを含む `aspnet_Users` テーブルには、`ApplicationId` の外部キーフィールドがあります。`aspnet_Roles` テーブルの ditto。 これらのテーブルの `ApplicationId` フィールドでは、ユーザーアカウントまたはロールが属しているアプリケーションパーティションを指定します。

### <a name="storing-user-account-information"></a>ユーザーアカウント情報の保存

ユーザーアカウント情報は、`aspnet_Users` と `aspnet_Membership`の2つのテーブルに格納されています。 `aspnet_Users` テーブルには、重要なユーザーアカウント情報を保持するフィールドが含まれています。 最も関連する3つの列は次のとおりです。

- `UserId`
- `UserName`
- `ApplicationId`

`UserId` は主キー (`uniqueidentifier`型) です。 `UserName` は `nvarchar(256)` 型で、パスワードと共に、ユーザーの資格情報を構成します。 (ユーザーのパスワードは `aspnet_Membership` テーブルに格納されます)。`ApplicationId` は、`aspnet_Applications`内の特定のアプリケーションにユーザーアカウントをリンクします。 `UserName` 列と `ApplicationId` 列には、複合[`UNIQUE` 制約](https://msdn.microsoft.com/library/ms191166.aspx)があります。 これにより、特定のアプリケーションで各ユーザー名が一意であることが保証されますが、同じ `UserName` を異なるアプリケーションで使用することができます。

`aspnet_Membership` の表には、ユーザーのパスワード、電子メールアドレス、最後にログインした日付と時刻などの追加のユーザーアカウント情報が含まれています。 `aspnet_Users` テーブルと `aspnet_Membership` テーブルのレコードの間には1対1の対応があります。 このリレーションシップは、テーブルの主キーとして機能する `aspnet_Membership`の [`UserId`] フィールドによって保証されます。 `aspnet_Users` テーブルと同様に、`aspnet_Membership` には、この情報を特定のアプリケーションパーティションに結び付ける `ApplicationId` フィールドが含まれています。

### <a name="securing-passwords"></a>パスワードのセキュリティ保護

パスワード情報は `aspnet_Membership` テーブルに格納されます。 `SqlMembershipProvider` では、次の3つの方法のいずれかを使用して、パスワードをデータベースに格納できます。

- **[クリア]** -パスワードはプレーンテキストとしてデータベースに格納されます。 このオプションを使用しないことを強くお勧めします。 データベースが侵害された場合、データベースへのアクセスが許可されているハッカーがデータベースに侵入したとしても、すべてのユーザーの資格情報が存在することになります。
- **ハッシュ**-パスワードは、一方向のハッシュアルゴリズムとランダムに生成された salt 値を使用してハッシュされます。 このハッシュ値 (salt) は、データベースに格納されます。
- **暗号化**-パスワードの暗号化されたバージョンがデータベースに格納されます。

使用されるパスワードストレージ手法は、`Web.config`で指定された `SqlMembershipProvider` 設定によって異なります。 ここでは、手順 4. で `SqlMembershipProvider` 設定をカスタマイズする方法について説明します。 既定の動作では、パスワードのハッシュが保存されます。

パスワードを格納する列は、`Password`、`PasswordFormat`、および `PasswordSalt`です。 `PasswordFormat` は、パスワードを格納するために使用される方法を示す値を持つ `int` 型のフィールドです。空の場合は0です。ハッシュされる場合は1。2暗号化されます。 使用されるパスワードストレージの手法に関係なく、ランダムに生成された文字列が `PasswordSalt` に割り当てられます。`PasswordSalt` の値は、パスワードのハッシュを計算する場合にのみ使用されます。 最後に、[`Password`] 列には、実際のパスワードデータ、プレーンテキストのパスワード、パスワードのハッシュ、または暗号化されたパスワードを入力します。

表1は、パスワード MySecret を格納するときに、これら3つの列がさまざまなストレージ手法でどのように表示されるかを示しています。 。

| **ストレージ手法&lt;\_o3a\_p/&gt;** | **パスワード&lt;\_o3a\_p/&gt;** | **PasswordFormat&lt;\_o3a\_p/&gt;** | **PasswordSalt&lt;\_o3a\_p/&gt;** |
| --- | --- | --- | --- |
| Clear | MySecret! | 0 | tTnkPlesqissc2y2SMEygA== |
| ハッシュ | 2oXm6sZHWbTHFgjgkGQsc2Ec9ZM= | 1 | wFgjUfhdUFOCKQiI61vtiQ== |
| Encrypted | 62RZgDvhxykkqsMchZ0Yly7HS6onhpaoCYaRxV8g0F4CW56OXUU3e7Inza9j9BKp | 2 | LSRzhGS/aa/oqAXGLHJNBw== |

**表 1**: パスワード Mysecret を保存するときのパスワード関連のフィールドの値の例

> [!NOTE]
> `SqlMembershipProvider` によって使用される特定の暗号化アルゴリズムまたはハッシュアルゴリズムは、`<machineKey>` 要素の設定によって決まります。 <a id="Tutorial3"> </a> [ *「フォーム認証の構成」と「高度なトピック*](../introduction/forms-authentication-configuration-and-advanced-topics-cs.md)」のチュートリアルの手順3で、この構成要素について説明しました。

### <a name="storing-roles-and-role-associations"></a>ロールとロールの関連付けの格納

ロールフレームワークを使用すると、開発者は一連のロールを定義し、ユーザーがどのロールに属しているかを指定できます。 この情報は、`aspnet_Roles` と `aspnet_UsersInRoles`の2つのテーブルによってデータベースにキャプチャされます。 `aspnet_Roles` テーブル内の各レコードは、特定のアプリケーションのロールを表します。 `aspnet_Users` テーブルと同様に、`aspnet_Roles` テーブルには、ここで説明する3つの列があります。

- `RoleId`
- `RoleName`
- `ApplicationId`

`RoleId` は主キー (`uniqueidentifier`型) です。 `RoleName` は `nvarchar(256)` 型です。 と `ApplicationId` は、`aspnet_Applications`内の特定のアプリケーションにユーザーアカウントをリンクします。 `RoleName` 列と `ApplicationId` 列には複合 `UNIQUE` 制約があるため、特定のアプリケーションで各ロール名が一意であることが保証されます。

`aspnet_UsersInRoles` テーブルは、ユーザーとロールの間のマッピングとして機能します。 列には、`UserId` と `RoleId` という2つの列があり、それらの組み合わせによって複合主キーが構成されます。

## <a name="step-4-specifying-the-provider-and-customizing-its-settings"></a>手順 4: プロバイダーを指定し、その設定をカスタマイズする

メンバーシップやロールのフレームワークなど、プロバイダーモデルをサポートするすべてのフレームワーク-実装の詳細がないため、その責任をプロバイダークラスに委任します。 メンバーシップフレームワークの場合、`Membership` クラスは、ユーザーアカウントを管理するための API を定義しますが、ユーザーストアと直接対話することはありません。 代わりに、`Membership` クラスのメソッドは、構成されたプロバイダーに要求を渡します。 `SqlMembershipProvider`を使用します。 `Membership` クラスのメソッドのいずれかを呼び出すと、メンバーシップフレームワークは、`SqlMembershipProvider`への呼び出しを委任することをどのように認識しますか。

`Membership` クラスには、メンバーシップフレームワークで使用できるすべての登録済みプロバイダークラスへの参照を含む[`Providers` プロパティ](https://msdn.microsoft.com/library/system.web.security.membership.providers.aspx)があります。 登録された各プロバイダーには、関連付けられた名前と型があります。 名前には、`Providers` コレクション内の特定のプロバイダーを参照するためのわかりやすい方法が用意されていますが、型はプロバイダークラスを識別します。 さらに、登録された各プロバイダーには、構成設定が含まれる場合があります。 メンバーシップフレームワークの構成設定には、他の多くの `passwordFormat` と `requiresUniqueEmail`が含まれます。 `SqlMembershipProvider`によって使用される構成設定の完全な一覧については、表2を参照してください。

`Providers` プロパティの内容は、web アプリケーションの構成設定によって指定されます。 既定では、すべての web アプリケーションに `SqlMembershipProvider`型の `AspNetSqlMembershipProvider` という名前のプロバイダーがあります。 この既定のメンバーシッププロバイダーは `machine.config` (`%WINDIR%\Microsoft.Net\Framework\v2.0.50727\CONFIG)`にあります。

[!code-xml[Main](creating-the-membership-schema-in-sql-server-cs/samples/sample1.xml)]

上のマークアップが示すように、 [`<membership>` 要素](https://msdn.microsoft.com/library/1b9hw62f.aspx)は、メンバーシップフレームワークの構成設定を定義します。一方、 [`<providers>` 子要素](https://msdn.microsoft.com/library/6d4936ht.aspx)は、登録されているプロバイダーを指定します。 プロバイダーは、 [`<add>`](https://msdn.microsoft.com/library/whae3t94.aspx)要素または[`<remove>`](https://msdn.microsoft.com/library/aykw9a6d.aspx)要素を使用して追加または削除できます。現在登録されているすべてのプロバイダーを削除するには、 [`<clear>`](https://msdn.microsoft.com/library/t062y6yc.aspx)要素を使用します。 上のマークアップが示すように、`machine.config` `SqlMembershipProvider`型の `AspNetSqlMembershipProvider` という名前のプロバイダーを追加します。

`name` 属性と `type` 属性に加えて、`<add>` 要素には、さまざまな構成設定の値を定義する属性が含まれています。 表2に、使用可能な `SqlMembershipProvider`固有の構成設定と、それぞれの説明を示します。

> [!NOTE]
> 表2に示されている既定値は、`SqlMembershipProvider` クラスで定義されている既定値を示します。 `AspNetSqlMembershipProvider` のすべての構成設定が `SqlMembershipProvider` クラスの既定値に対応しているわけではないことに注意してください。 たとえば、メンバーシッププロバイダーで指定されていない場合、`requiresUniqueEmail` 設定の既定値は true になります。 ただし、`AspNetSqlMembershipProvider` は、`false`の値を明示的に指定することによって、この既定値をオーバーライドします。

| **&lt;の設定 \_o3a\_p/&gt;** | **説明&lt;\_o3a\_p/&gt;** |
| --- | --- |
| `ApplicationName` | メンバーシップフレームワークによって、単一のユーザーストアを複数のアプリケーションでパーティション分割できることを思い出してください。 この設定は、メンバーシッププロバイダーによって使用されるアプリケーションパーティションの名前を示します。 この値が明示的に指定されていない場合は、実行時にアプリケーションの仮想ルートパスの値に設定されます。 |
| `commandTimeout` | SQL コマンドのタイムアウト値を秒単位で指定します。 既定値は 30 です。 |
| `connectionStringName` | ユーザーストアデータベースへの接続に使用する `<connectionStrings>` 要素内の接続文字列の名前。 この値は必須です。 |
| `description` | 登録されているプロバイダーについてのわかりやすい説明を提供します。 |
| `enablePasswordRetrieval` | ユーザーが忘れたパスワードを取得できるかどうかを指定します。 既定値は `false` です。 |
| `enablePasswordReset` | ユーザーがパスワードのリセットを許可されているかどうかを示します。 既定値は `true` です。 |
| `maxInvalidPasswordAttempts` | ユーザーがロックアウトされる前に、指定された `passwordAttemptWindow` 中に特定のユーザーに対して失敗したログイン試行の最大回数。既定値は5です。 |
| `minRequiredNonalphanumericCharacters` | ユーザーのパスワードに表示する必要がある英数字以外の文字の最小数。 この値は 0 ~ 128 の範囲で指定する必要があります。既定値は1です。 |
| `minRequiredPasswordLength` | パスワードに必要な最小文字数。 この値は 0 ~ 128 の範囲で指定する必要があります。既定値は7です。 |
| `name` | 登録されているプロバイダーの名前。 この値は必須です。 |
| `passwordAttemptWindow` | 失敗したログイン試行が追跡される時間 (分単位)。 この指定した期間内にユーザーが無効なログイン資格情報を `maxInvalidPasswordAttempts` 入力した場合は、ロックアウトされます。既定値は10です。 |
| `PasswordFormat` | パスワードの保存形式: `Clear`、`Hashed`、または `Encrypted`。 既定では、 `Hashed`です。 |
| `passwordStrengthRegularExpression` | 指定されている場合、この正規表現を使用して、新しいアカウントを作成するとき、またはパスワードを変更するときに、ユーザーが選択したパスワードの強度を評価します。 既定値は空の文字列です。 |
| `requiresQuestionAndAnswer` | パスワードを取得またはリセットするときに、ユーザーがセキュリティの質問に答える必要があるかどうかを指定します。 既定値は `true` です。 |
| `requiresUniqueEmail` | 特定のアプリケーションパーティション内のすべてのユーザーアカウントが一意の電子メールアドレスを持つ必要があるかどうかを示します。 既定値は `true` です。 |
| `type` | プロバイダーの種類を指定します。 この値は必須です。 |

**表 2**: メンバーシップと `SqlMembershipProvider` 構成設定

`AspNetSqlMembershipProvider`に加えて、他のメンバーシッププロバイダーは、`Web.config` ファイルに同様のマークアップを追加することによって、アプリケーションごとに登録できます。

> [!NOTE]
> ロールフレームワークは同じように機能します。 `machine.config` に既定で登録されたロールプロバイダーがあり、登録されているプロバイダーは `Web.config`でアプリケーションごとにカスタマイズできます。 ロールフレームワークとその構成マークアップについては、今後のチュートリアルで詳しく説明します。

### <a name="customizing-thesqlmembershipprovidersettings"></a>`SqlMembershipProvider`設定のカスタマイズ

既定の `SqlMembershipProvider` (`AspNetSqlMembershipProvider`) では、`connectionStringName` 属性が `LocalSqlServer`に設定されています。 `AspNetSqlMembershipProvider` プロバイダーと同様に、接続文字列名 `LocalSqlServer` は `machine.config`で定義されます。

[!code-xml[Main](creating-the-membership-schema-in-sql-server-cs/samples/sample2.xml)]

ご覧のとおり、この接続文字列では | にある SQL 2005 Express Edition データベースが定義されています。DataDirectory | aspnetdb.mdf。 String |DataDirectory | 実行時には、`~/App_Data/` ディレクトリを指すように変換されます。そのため、データベース path |DataDirectory | aspnetdb.mdf は、`~/App_Data`/`aspnet.mdf`に変換します。

アプリケーションの `Web.config` ファイルでメンバーシッププロバイダー情報を指定しなかった場合、アプリケーションは既定の登録されたメンバーシッププロバイダー、`AspNetSqlMembershipProvider`を使用します。 `~/App_Data/aspnet.mdf` データベースが存在しない場合は、ASP.NET ランタイムによって自動的に作成され、アプリケーションサービススキーマが追加されます。 ただし、`aspnet.mdf` データベースは使用しません。代わりに、手順 2. で作成した `SecurityTutorials.mdf` データベースを使用します。 この変更は、次の2つの方法のいずれかで行うことができます。

- <strong>`Web.config`</strong>で、<strong>`LocalSqlServer`</strong><strong>接続文字列名</strong><strong>の値を指定</strong>し<strong>ます。</strong> `Web.config`の `LocalSqlServer` 接続文字列名の値を上書きすることにより、既定の登録済みメンバーシッププロバイダー (`AspNetSqlMembershipProvider`) を使用して、`SecurityTutorials.mdf` データベースと正しく連携させることができます。 `AspNetSqlMembershipProvider`によって指定された構成設定を使用してコンテンツを作成する場合は、この方法が適しています。 この手法の詳細については、 [Scott Guthrie](https://weblogs.asp.net/scottgu/)のブログ記事「 [SQL Server 2000 または SQL Server 2005 を使用するように ASP.NET 2.0 アプリケーションサービスを構成する](https://weblogs.asp.net/scottgu/archive/2005/08/25/423703.aspx)」を参照してください。
- <strong>`SqlMembershipProvider`</strong><strong>種類の新しい登録済みプロバイダーを追加</strong>し、<strong>`SecurityTutorials.mdf`</strong>データベース<strong>を指すようにその`connectionStringName`設定を</strong><strong>構成し</strong><strong>ます。</strong> この方法は、データベース接続文字列に加えて他の構成プロパティをカスタマイズする場合に便利です。 独自のプロジェクトでは、柔軟性と読みやすさのため、常にこの方法を使用します。

`SecurityTutorials.mdf` データベースを参照する新しい登録済みプロバイダーを追加する前に、まず `Web.config`の `<connectionStrings>` セクションに適切な接続文字列値を追加する必要があります。 次のマークアップは、`App_Data` フォルダー内の SQL Server 2005 Express Edition `SecurityTutorials.mdf` データベースを参照する `SecurityTutorialsConnectionString` という名前の新しい接続文字列を追加します。

[!code-xml[Main](creating-the-membership-schema-in-sql-server-cs/samples/sample3.xml)]

> [!NOTE]
> 代替データベースファイルを使用する場合は、必要に応じて接続文字列を更新します。 正しい接続文字列を形成する方法の詳細については、 [ConnectionStrings.com](http://www.connectionstrings.com/)を参照してください。

次に、次のメンバーシップ構成マークアップを `Web.config` ファイルに追加します。 このマークアップは、`SecurityTutorialsSqlMembershipProvider`という名前の新しいプロバイダーを登録します。

[!code-xml[Main](creating-the-membership-schema-in-sql-server-cs/samples/sample4.xml)]

上のマークアップでは、`SecurityTutorialsSqlMembershipProvider` プロバイダーの登録に加えて、`SecurityTutorialsSqlMembershipProvider` を既定のプロバイダーとして定義しています (`<membership>` 要素の `defaultProvider` 属性を使用)。 メンバーシップフレームワークは複数の登録済みプロバイダーを持つことができることを思い出してください。 `AspNetSqlMembershipProvider` は `machine.config`の最初のプロバイダーとして登録されるため、特に指定しない限り、既定のプロバイダーとして機能します。

現在、アプリケーションには、`AspNetSqlMembershipProvider` と `SecurityTutorialsSqlMembershipProvider`の2つの登録済みプロバイダーがあります。 ただし、`SecurityTutorialsSqlMembershipProvider` プロバイダーを登録する前に、`<add>` 要素の直前に[`<clear />` 要素](https://msdn.microsoft.com/library/t062y6yc.aspx)を追加することで、以前に登録されていたすべてのプロバイダーを消去できます。 これにより、登録されているプロバイダーの一覧から `AspNetSqlMembershipProvider` がクリアされます。つまり、`SecurityTutorialsSqlMembershipProvider` が唯一の登録済みメンバーシッププロバイダーになります。 この方法を使用した場合は、登録されている唯一のメンバーシッププロバイダーであるため、`SecurityTutorialsSqlMembershipProvider` を既定のプロバイダーとしてマークする必要はありません。 `<clear />`の使用方法の詳細については、「[プロバイダーを追加するときの `<clear />` の使用](https://weblogs.asp.net/scottgu/archive/2006/11/20/common-gotcha-don-t-forget-to-clear-when-adding-providers.aspx)」を参照してください。

`SecurityTutorialsSqlMembershipProvider`の `connectionStringName` 設定は、追加された `SecurityTutorialsConnectionString` 接続文字列名を参照し、その `applicationName` 設定が SecurityTutorials の値に設定されていることに注意してください。 さらに、`requiresUniqueEmail` 設定は `true`に設定されています。 他のすべての構成オプションは、`AspNetSqlMembershipProvider`の値と同じです。 必要に応じて、ここで自由に構成を変更することができます。 たとえば、1つではなく2つの英数字以外の文字を必要とすることによって、または7ではなく8文字になるようにパスワードの長さを増やすことで、パスワードの強度を強化することができます。

> [!NOTE]
> メンバーシップフレームワークによって、単一のユーザーストアを複数のアプリケーションでパーティション分割できることを思い出してください。 メンバーシッププロバイダーの `applicationName` 設定は、ユーザーストアを操作するときにプロバイダーが使用するアプリケーションを示します。 `applicationName` が明示的に設定されていない場合は、実行時に web アプリケーションの仮想ルートパスに割り当てられるため、`applicationName` 構成設定の値を明示的に設定することが重要です。 アプリケーションの仮想ルートパスが変更されない限り、これは問題なく動作しますが、アプリケーションを別のパスに移動した場合、`applicationName` 設定も変わります。 この場合、メンバーシッププロバイダーは、以前に使用されていたものとは異なるアプリケーションパーティションを使用して作業を開始します。 移動前に作成されたユーザーアカウントは別のアプリケーションパーティションに存在するため、これらのユーザーはサイトにログインできなくなります。 この問題の詳細については、「 [ASP.NET 2.0 のメンバーシップとその他のプロバイダーを構成するときに常に `applicationName` プロパティを設定する](https://weblogs.asp.net/scottgu/443634)」を参照してください。

## <a name="summary"></a>まとめ

この時点で、アプリケーションサービス (`SecurityTutorials.mdf`) が構成されたデータベースがあり、メンバーシップフレームワークが登録した `SecurityTutorialsSqlMembershipProvider` プロバイダーを使用するように web アプリケーションを構成しました。 この登録されたプロバイダーは `SqlMembershipProvider` 型で、`connectionStringName` が適切な接続文字列 (`SecurityTutorialsConnectionString`) に設定され、`applicationName` 値が明示的に設定されています。

これで、アプリケーションからメンバーシップフレームワークを使用する準備ができました。 次のチュートリアルでは、新しいユーザーアカウントを作成する方法について説明します。 次に、ユーザーの認証、ユーザーベースの承認の実行、およびデータベースへの追加のユーザー関連情報の格納について説明します。

プログラミングを楽しんでください。

### <a name="further-reading"></a>参考資料

このチュートリアルで説明しているトピックの詳細については、次のリソースを参照してください。

- [ASP.NET 2.0 メンバーシップとその他のプロバイダーを構成するときは常に `applicationName` プロパティを設定する](https://weblogs.asp.net/scottgu/443634)
- [SQL Server 2000 または SQL Server 2005 を使用するように ASP.NET 2.0 アプリケーションサービスを構成する](https://weblogs.asp.net/scottgu/archive/2005/08/25/423703.aspx)
- [Express Edition のダウンロード SQL Server Management Studio](https://www.microsoft.com/downloads/details.aspx?FamilyId=C243A5AE-4BD1-4E3D-94B8-5A0F62BF7796&amp;displaylang=en)
- [ASP.NET 2.0 s のメンバーシップ、ロール、およびプロファイルを調べています](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)
- [メンバーシップのプロバイダーの `<add>` 要素](https://msdn.microsoft.com/library/whae3t94.aspx)
- [`<membership>` 要素](https://msdn.microsoft.com/library/1b9hw62f.aspx)
- [メンバーシップの `<providers>` 要素](https://msdn.microsoft.com/library/6d4936ht.aspx)
- [プロバイダーを追加するときに `<clear />` を使用する](https://weblogs.asp.net/scottgu/archive/2006/11/20/common-gotcha-don-t-forget-to-clear-when-adding-providers.aspx)
- [`SqlMembershipProvider` を直接操作する](http://aspnet.4guysfromrolla.com/articles/091207-1.aspx)

### <a name="video-training-on-topics-contained-in-this-tutorial"></a>このチュートリアルに含まれるトピックのビデオトレーニング

- [ASP.NET メンバーシップについて理解する](../../../videos/authentication/understanding-aspnet-memberships.md)
- [メンバーシップ スキーマと連動するように SQL を構成する](../../../videos/authentication/configuring-sql-to-work-with-membership-schemas.md)
- [既定のメンバーシップ スキーマのメンバーシップ設定を変更する](../../../videos/authentication/changing-membership-settings-in-the-default-membership-schema.md)

### <a name="about-the-author"></a>著者について

1998以降、Microsoft の Web テクノロジを使用して、Scott Mitchell (複数の ASP/創設者4GuysFromRolla.com の執筆者) が Microsoft の Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は *[、ASP.NET 2.0 を24時間以内に教え](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* ています。 Scott は、 [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com)またはブログで[http://ScottOnWriting.NET](http://scottonwriting.net/)にアクセスできます。

### <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビューアーは Alicja Maziarz でした。 今後の MSDN 記事を確認することに興味がありますか? その場合は、 [mitchell@4GuysFromRolla.com](mailto:mitchell@4guysfromrolla.com)の行を削除します。

> [!div class="step-by-step"]
> [Next](creating-user-accounts-cs.md)
