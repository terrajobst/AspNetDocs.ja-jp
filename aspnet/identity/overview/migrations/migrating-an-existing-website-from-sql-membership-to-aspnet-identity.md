---
uid: identity/overview/migrations/migrating-an-existing-website-from-sql-membership-to-aspnet-identity
title: 既存の Web サイトを SQL メンバーシップから ASP.NET Identity-ASP.NET 4.x に移行する
author: Rick-Anderson
description: このチュートリアルでは、SQL メンバーシップを使用して作成されたユーザーおよびロールデータを持つ既存の web アプリケーションを新しい ASP.NET Identity に移行する手順について説明します...
ms.author: riande
ms.date: 12/19/2014
ms.custom: seoapril2019
ms.assetid: 220d3d75-16b2-4240-beae-a5b534f06419
msc.legacyurl: /identity/overview/migrations/migrating-an-existing-website-from-sql-membership-to-aspnet-identity
msc.type: authoredcontent
ms.openlocfilehash: eacfbb8a5b2d1aa3678892bc2077a56185fdebbc
ms.sourcegitcommit: 88fc80e3f65aebdf61ec9414810ddbc31c543f04
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/22/2020
ms.locfileid: "76519155"
---
# <a name="migrating-an-existing-website-from-sql-membership-to-aspnet-identity"></a>既存 Web サイトを SQL メンバーシップから ASP.NET Identity に移行する

[Rick Anderson]((https://twitter.com/RickAndMSFT))、 [suhas Joshi](https://github.com/suhasj)

> このチュートリアルでは、SQL メンバーシップを使用して作成されたユーザーデータとロールデータを使用して、既存の web アプリケーションを新しい ASP.NET Identity システムに移行する手順について説明します。 この方法では、既存のデータベーススキーマを ASP.NET Identity によって必要とされるスキーマに変更し、古い/新しいクラスにフックします。 このアプローチを採用した後、データベースを移行すると、今後 Id に対する更新が簡単に処理されるようになります。

このチュートリアルでは、Visual Studio 2010 を使用して作成された web アプリケーションテンプレート (Web フォーム) を使用して、ユーザーとロールのデータを作成します。 次に、SQL スクリプトを使用して、既存のデータベースを Id システムで必要とされるテーブルに移行します。 次に、必要な NuGet パッケージをインストールし、メンバーシップ管理に Id システムを使用する新しいアカウント管理ページを追加します。 移行のテストとして、SQL メンバーシップを使用して作成されたユーザーはログインでき、新しいユーザーが登録できるようにする必要があります。 完全なサンプルは、[こちら](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/SQLMembership-Identity-OWIN/)でご覧いただけます。 「 [ASP.NET メンバーシップから ASP.NET Identity への移行](http://travis.io/blog/2015/03/24/migrate-from-aspnet-membership-to-aspnet-identity.html)」も参照してください。

## <a name="getting-started"></a>作業の開始

### <a name="creating-an-application-with-sql-membership"></a>SQL メンバーシップを使用したアプリケーションの作成

1. SQL メンバーシップを使用し、ユーザーデータとロールデータを持つ既存のアプリケーションを使用して開始する必要があります。 この記事では、Visual Studio 2010 で web アプリケーションを作成します。

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image1.jpg)
2. ASP.NET 構成ツールを使用して、2人のユーザー ( **Oldadminuser**と olduser) を作成し**ます。**

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image1.png)

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image2.jpg)
3. Admin という名前のロールを作成し、そのロールのユーザーとして "oldAdminUser" を追加します。

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image2.png)
4. Default.aspx を使用して、サイトの管理者セクションを作成します。 Web.config ファイルの authorization タグを設定して、管理者ロールのユーザーのみにアクセスを有効にします。 詳細については、こちらを参照してください[https://www.asp.net/web-forms/tutorials/security/roles/role-based-authorization-cs](../../../web-forms/overview/older-versions-security/roles/role-based-authorization-cs.md)

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image3.png)
5. SQL メンバーシップシステムによって作成されたテーブルを理解するには、サーバーエクスプローラーでデータベースを表示します。 ユーザーログインデータは、aspnet\_Users および aspnet\_メンバーシップテーブルに格納されますが、ロールデータは aspnet\_Roles テーブルに格納されます。 Aspnet\_UsersInRoles テーブルに格納されているロールのユーザーに関する情報。 基本的なメンバーシップ管理の場合は、上記の表の情報を ASP.NET Identity システムに移植するだけで十分です。

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image4.png)

### <a name="migrating-to-visual-studio-2013"></a>Visual Studio 2013 への移行

1. [最新の更新プログラム](https://www.microsoft.com/download/details.aspx?id=44921)と共に、Web または Visual Studio 2013 の Visual Studio Express 2013 をインストールします。
2. インストールされているバージョンの Visual Studio で、上記のプロジェクトを開きます。 コンピューターに SQL Server Express がインストールされていない場合は、プロジェクトを開いたときにプロンプトが表示されます。これは、接続文字列で SQL Express が使用されているためです。 SQL Express のインストールを選択することも、接続文字列を LocalDb に変更することもできます。 この記事では、これを LocalDb に変更します。
3. Web.config を開き、接続文字列をから変更します。SQLExpress to (LocalDb) v1.0。 接続文字列から ' User Instance = true ' を削除します。

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image3.jpg)
4. サーバーエクスプローラーを開き、テーブルのスキーマとデータを確認できることを確認します。
5. ASP.NET Identity システムは、バージョン4.5 以上のフレームワークで動作します。 アプリケーションを4.5 以降に再ターゲットします。

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image5.png)

    プロジェクトをビルドして、エラーがないことを確認します。

### <a name="installing-the-nuget-packages"></a>Nuget パッケージのインストール

1. ソリューションエクスプローラーで、プロジェクトを右クリックし、 **[NuGet パッケージの管理]** &gt; ます。 検索ボックスに、「Asp.net Identity」と入力します。 結果の一覧でパッケージを選択し、[インストール] をクリックします。 [同意する] ボタンをクリックして、使用許諾契約書に同意します。 このパッケージでは、EntityFramework および Microsoft ASP.NET Identity Core という依存関係パッケージがインストールされることに注意してください。 同様に、次のパッケージをインストールします (OAuth ログインを有効にしない場合は、最後の4つの OWIN パッケージをスキップします)。

   - Microsoft.AspNet.Identity.Owin
   - Microsoft.Owin.Host.SystemWeb
   - Owin (Microsoft. Security)
   - Microsoft.Owin.Security.Google
   - Microsoft.Owin.Security.MicrosoftAccount
   - Microsoft.Owin.Security.Twitter

     ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image6.png)

### <a name="migrate-database-to-the-new-identity-system"></a>新しい Id システムへのデータベースの移行

次の手順では、既存のデータベースを ASP.NET Identity システムに必要なスキーマに移行します。 これを実現するには、新しいテーブルを作成し、既存のユーザー情報を新しいテーブルに移行するためのコマンドのセットを含む SQL スクリプトを実行します。 スクリプトファイルは[こちらで](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/SQLMembership-Identity-OWIN/Migrations.sql)参照できます。

このスクリプトファイルは、このサンプルに固有のものです。 SQL メンバーシップを使用して作成されたテーブルのスキーマがカスタマイズまたは変更された場合は、それに応じてスクリプトを変更する必要があります。

### <a name="how-to-generate-the-sql-script-for-schema-migration"></a>スキーマ移行用の SQL スクリプトを生成する方法

既存のユーザーのデータを使用して ASP.NET Identity クラスをすぐに使用できるようにするには、データベーススキーマを ASP.NET Identity で必要なものに移行する必要があります。 これを行うには、新しいテーブルを追加し、既存の情報をそれらのテーブルにコピーします。 既定では、ASP.NET Identity は EntityFramework を使用して Id モデルクラスをデータベースにマップし、情報を格納または取得します。 これらのモデルクラスは、ユーザーおよびロールオブジェクトを定義するコア Id インターフェイスを実装します。 データベース内のテーブルと列は、これらのモデルクラスに基づいています。 Identity v 2.1.0 の EntityFramework モデルクラスとそのプロパティは次のように定義されています。

| **IdentityUser** | **型** | **IdentityRole** | **IdentityUserRole** | **IdentityUserLogin** | **IdentityUserClaim** |
| --- | --- | --- | --- | --- | --- |
| ID | string | ID | RoleId | ProviderKey | ID |
| ユーザー名 | string | [名前] | UserId | UserId | ClaimType |
| PasswordHash | string |  |  | LoginProvider | ClaimValue |
| SecurityStamp | string |  |  |  | ユーザー\_Id |
| 電子メール | string |  |  |  |  |
| 電子メールの確認 | ブール |  |  |  |  |
| PhoneNumber | string |  |  |  |  |
| PhoneNumberConfirmed | ブール |  |  |  |  |
| LockoutEnabled | ブール |  |  |  |  |
| LockoutEndDate | DateTime |  |  |  |  |
| AccessFailedCount | int |  |  |  |  |

これらの各モデルのテーブルには、プロパティに対応する列を用意する必要があります。 クラスとテーブル間のマッピングは、`IdentityDBContext`の `OnModelCreating` メソッドで定義されます。 これは、構成の fluent API 方法として知られています。詳細については、[こちら](https://msdn.microsoft.com/data/jj591617.aspx)を参照してください。 クラスの構成は次のとおりです。

| **クラス** | **テーブル** | **主キー** | **外部キー** |
| --- | --- | --- | --- |
| IdentityUser | AspnetUsers | ID |  |
| IdentityRole | AspnetRoles | ID |  |
| IdentityUserRole | AspnetUserRole | UserId + RoleId | ユーザー\_Id-&gt;AspnetUsers RoleId-&gt;AspnetRoles |
| IdentityUserLogin | AspnetUserLogins | ProviderKey + UserId + LoginProvider | UserId-&gt;AspnetUsers |
| IdentityUserClaim | AspnetUserClaims | ID | ユーザー\_Id-&gt;AspnetUsers |

この情報を使用して、新しいテーブルを作成する SQL ステートメントを作成できます。 各ステートメントを個別に記述するか、必要に応じて編集できる EntityFramework PowerShell コマンドを使用してスクリプト全体を生成することができます。 これを行うには、VS で **[ビュー]** メニューまたは **[ツール]** メニューから**パッケージマネージャーコンソール**を開きます。

- EntityFramework の移行を有効にするには、コマンド "Enable-移行" を実行します。
- コマンド "Add-migration initial" を実行して、データベースC#を作成するための初期セットアップコードを作成します。
- 最後の手順では、モデルクラスに基づいて SQL スクリプトを生成する "Update-Database – Script" コマンドを実行します。

[!INCLUDE[](../../../includes/identity/alter-command-exception.md)]

このデータベース生成スクリプトは、新しい列を追加したりデータをコピーしたりするための追加の変更を行う最初の方法として使用できます。 この利点は、将来のバージョンの Id リリースでモデルクラスが変更されたときに、EntityFramework がデータベーススキーマを変更するために使用する `_MigrationHistory` テーブルを生成することです。

SQL メンバーシップのユーザー情報には、Identity user model クラスに含まれるもの以外に、電子メール、パスワードの試行、最後のログインの日付、最後のロックアウト日などのプロパティがありました。これは有用な情報であり、Id システムに引き継がれるようにしたいと考えています。 これを行うには、ユーザーモデルにプロパティを追加して、データベースのテーブル列にマップし直します。 これを行うには、`IdentityUser` モデルをサブクラスにするクラスを追加します。 このカスタムクラスにプロパティを追加し、SQL スクリプトを編集して、テーブルの作成時に対応する列を追加できます。 このクラスのコードについては、この記事で詳しく説明します。 新しいプロパティを追加した後で `AspnetUsers` テーブルを作成するための SQL スクリプトは、

[!code-sql[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample1.sql)]

次に、SQL メンバーシップデータベースから、Id 用に新しく追加されたテーブルに既存の情報をコピーする必要があります。 これは、データを1つのテーブルから別のテーブルに直接コピーすることによって、SQL を通じて行うことができます。 テーブルの行にデータを追加するには、`INSERT INTO [Table]` コンストラクトを使用します。 別のテーブルからコピーするには、`INSERT INTO` ステートメントを `SELECT` ステートメントと共に使用できます。 すべてのユーザー情報を取得するには、 *aspnet\_ユーザー*および*aspnet\_メンバーシップ*テーブルにクエリを実行し、データを*AspNetUsers*テーブルにコピーする必要があります。 `INSERT INTO` と `SELECT` を `JOIN` および `LEFT OUTER JOIN` ステートメントと共に使用します。 テーブル間でのデータのクエリとコピーの詳細については、こちら[のリンクを](https://technet.microsoft.com/library/ms190750%28v=sql.105%29.aspx)参照してください。 また、AspnetUserLogins テーブルと AspnetUserClaims テーブルは、既定ではこの値にマップされる情報が SQL メンバーシップにないため、では空になります。 コピーされる情報は、ユーザーとロールのみです。 前の手順で作成したプロジェクトでは、ユーザーテーブルに情報をコピーする SQL クエリはになります。

[!code-sql[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample2.sql)]

上記の SQL ステートメントでは、 *aspnet\_Users*および*aspnet\_* の各ユーザーに関する情報が、 *AspnetUsers*テーブルの列にコピーされます。 ここで行った変更は、パスワードをコピーしたときだけです。 SQL メンバーシップのパスワードの暗号化アルゴリズムでは ' PasswordSalt ' と ' Passwordsalt ' が使用されているため、ハッシュされたパスワードと共にコピーして、Id によってパスワードの暗号化を解除することができます。 詳細については、「カスタムパスワードの hasher をフックするとき」で詳しく説明します。

このスクリプトファイルは、このサンプルに固有のものです。 追加のテーブルを持つアプリケーションでは、開発者は同様のアプローチに従って、ユーザーモデルクラスにプロパティを追加し、AspnetUsers テーブルの列にマップすることができます。 スクリプトを実行するには、

1. サーバー エクスプローラーを開きます。 "ApplicationServices" 接続を展開してテーブルを表示します。 [テーブル] ノードを右クリックし、[新しいクエリ] オプションを選択します。

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image7.png)
2. クエリウィンドウで、SQL スクリプト全体をコピーして、移行 .sql ファイルから貼り付けます。 [実行] 矢印ボタンを押してスクリプトファイルを実行します。

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image4.jpg)

    サーバーエクスプローラーウィンドウを更新します。 5つの新しいテーブルがデータベースに作成されます。

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image8.png)

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image9.png)

    SQL メンバーシップテーブルの情報を新しい Id システムにマップする方法を次に示します。

    aspnet\_ロール--&gt; AspNetRoles

    asp\_netUsers および asp\_Netusers--&gt; AspNetUsers

    aspnet\_UserInRoles--&gt; AspNetUserRoles

    上のセクションで説明したように、AspNetUserClaims テーブルと AspNetUserLogins テーブルは空です。 AspNetUser テーブルの ' 識別子 ' フィールドは、次の手順として定義されているモデルクラス名と一致する必要があります。 また、PasswordHash 列は、"暗号化されたパスワード | パスワード salt | パスワードの形式" という形式になっています。 これにより、古いパスワードを再利用できるように、特別な SQL メンバーシップ暗号化ロジックを使用できるようになります。 これについては、この記事の後半で説明します。

### <a name="creating-models-and-membership-pages"></a>モデルとメンバーシップページの作成

前述のように、Id 機能は Entity Framework を使用してデータベースと対話し、既定でアカウント情報を格納します。 テーブル内の既存のデータを操作するには、テーブルにマップし直して Id システムにフックするモデルクラスを作成する必要があります。 Id コントラクトの一部として、モデルクラスは、Identity. Core dll で定義されているインターフェイスを実装するか、またはこれらのインターフェイスの既存の実装を拡張して使用できます。

このサンプルでは、AspNetRoles、AspNetUserClaims、AspNetLogins、AspNetUserRole の各テーブルに、Id システムの既存の実装に似た列があります。 そのため、既存のクラスを再利用して、これらのテーブルにマップすることができます。 AspNetUser テーブルには、SQL メンバーシップテーブルから追加情報を格納するために使用される追加の列がいくつかあります。 これは、' ユーザー ' の既存の実装を拡張し、追加のプロパティを追加するモデルクラスを作成することによってマップできます。

1. プロジェクトにモデルフォルダーを作成し、クラスユーザーを追加します。 クラスの名前は、' AspnetUsers ' テーブルの ' 識別子 ' 列に追加されたデータと一致している必要があります。

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image10.png)

    User クラスでは、 *Microsoft .net framework* dll のユーザークラスを拡張する必要があります。 AspNetUser 列にマップし直すクラスのプロパティを宣言します。 プロパティ ID、ユーザー名、PasswordHash は、ユーザーに定義されているので、省略します。 すべてのプロパティを持つ User クラスのコードを次に示します。

    [!code-csharp[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample3.cs)]
2. モデル内のデータをテーブルに保存し、テーブルからデータを取得してモデルを作成するためには、Entity Framework DbContext クラスが必要です。 *Microsoft.AspNet.Identity.EntityFramework* dll defines the IdentityDbContext class which interacts with the Identity tables to retrieve and store information. ユーザー&gt;&lt;tuser は、"TUser" クラスを受け取ります。このクラスには、ユーザークラスを拡張する任意のクラスを指定できます。

    ' Model ' フォルダーの下にある "ユーザー" クラスを渡して、"モデル" フォルダーの下にある [ユーザー] クラスを渡す新しいクラス ApplicationDBContext を作成します。

    [!code-csharp[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample4.cs)]
3. 新しい Id システムでのユーザー管理*は、* usermanager の&lt;tuser&gt; クラスを使用して実行されます。 UserManager を拡張するカスタムクラスを作成し、手順 1. で作成した ' User ' クラスを渡す必要があります。

    [モデル] フォルダーで、UserManager&lt;ユーザーを拡張する新しいクラス UserManager を作成し&gt;

    [!code-csharp[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample5.cs)]
4. アプリケーションのユーザーのパスワードは暗号化され、データベースに格納されます。 SQL メンバーシップで使用される暗号アルゴリズムは、新しい Id システムとは異なります。 古いパスワードを再利用するには、古いユーザーが SQL メンバーシップアルゴリズムを使用してログインしているときにパスワードの暗号化を解除し、新しいユーザーの Id で暗号化アルゴリズムを使用する必要があります。

    UserManager クラスには、' IPasswordHasher ' インターフェイスを実装するクラスのインスタンスを格納する ' PasswordHasher ' プロパティがあります。 これは、ユーザー認証トランザクション中にパスワードの暗号化/暗号化解除に使用されます。 手順 3. で定義した UserManager クラスで、新しいクラス SQLPasswordHasher を作成し、次のコードをコピーします。

    [!code-csharp[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample6.cs)]

    System.string および system.string 名前空間をインポートして、コンパイルエラーを解決します。

    EncodePassword メソッドは、既定の SQL メンバーシップ暗号化の実装に従ってパスワードを暗号化します。 これは、System.web dll から取得されます。 以前のアプリでカスタム実装を使用していた場合は、ここに反映させる必要があります。 *EncodePassword*メソッドを使用して指定されたパスワードをハッシュする方法、またはプレーンテキストパスワードをデータベース内の既存のパスワードで確認する方法を、 *Hashpassword*と*VerifyHashedPassword*の2つのメソッドで定義する必要があります。

    SQL メンバーシップシステムは、パスワードを登録または変更するときにユーザーが入力したパスワードをハッシュするために、PasswordHash、PasswordSalt、および Passwordsalt を使用しました。 移行中、3つのフィールドはすべて、AspNetUser テーブルの PasswordHash 列に ' | ' 文字で区切られて格納されます。 ユーザーがログインし、パスワードにこれらのフィールドが含まれている場合、SQL メンバーシップ暗号化を使用してパスワードを確認します。それ以外の場合は、Id システムの既定の暗号化を使用してパスワードを確認します。 このようにすると、アプリを移行した後で、古いユーザーがパスワードを変更する必要がなくなります。
5. UserManager クラスのコンストラクターを宣言し、これを SQLPasswordHasher としてコンストラクターのプロパティに渡します。

    [!code-csharp[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample7.cs)]

### <a name="create-new-account-management-pages"></a>新しいアカウント管理ページを作成する

移行の次の手順では、ユーザーが登録してログインできるようにするアカウント管理ページを追加します。 SQL メンバーシップの古いアカウントページでは、新しい Id システムで動作しないコントロールが使用されます。 新しいユーザー管理ページを追加するには、このリンクのチュートリアルに従って、プロジェクトを既に作成し、NuGet パッケージを追加したので、「アプリケーションにユーザーを登録するための Web フォームを追加する」の手順から開始[https://www.asp.net/identity/overview/getting-started/adding-aspnet-identity-to-an-empty-or-existing-web-forms-project](../getting-started/adding-aspnet-identity-to-an-empty-or-existing-web-forms-project.md)ます。

ここで使用しているプロジェクトを操作するには、サンプルにいくつかの変更を加える必要があります。

- Register.aspx.cs および Login.aspx.cs の分離コードクラスは、Id パッケージの `UserManager` を使用してユーザーを作成します。 この例では、前に説明した手順に従って、[モデル] フォルダーに追加した UserManager を使用します。
- Register.aspx.cs および Login.aspx.cs コードビハインドクラスのユーザーではなく、作成されたユーザークラスを使用します。 これにより、カスタムユーザークラスが Id システムにフックされます。
- データベースを作成する部分はスキップできます。
- 開発者は、新しいユーザーの ApplicationId を現在のアプリケーション ID と一致するように設定する必要があります。 これを行うには、Register.aspx.cs クラスでユーザーオブジェクトが作成される前に、このアプリケーションの ApplicationId に対してクエリを実行し、ユーザーオブジェクトを作成する前に設定します。

    例:

    Register.aspx.cs ページでメソッドを定義して、aspnet\_Applications テーブルに対してクエリを実行し、アプリケーション名に従ってアプリケーション Id を取得します。

    [!code-csharp[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample8.cs)]

    ここで、ユーザーオブジェクトに対してこれを設定します。

    [!code-csharp[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample9.cs)]

古いユーザー名とパスワードを使用して、既存のユーザーをログインします。 [登録] ページを使用して、新しいユーザーを作成します。 また、ユーザーが期待どおりにロールに含まれていることを確認します。

Id システムに移植すると、ユーザーが Open Authentication (OAuth) をアプリケーションに追加するのに役立ちます。 OAuth が有効[になっているサンプルを](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/SQLMembership-Identity-OWIN/)参照してください。

## <a name="next-steps"></a>次のステップ

このチュートリアルでは、ユーザーを SQL メンバーシップから ASP.NET Identity に移植する方法を説明しましたが、プロファイルデータを移植していませんでした。 次のチュートリアルでは、SQL メンバーシップから新しい Id システムへのプロファイルデータの移植について説明します。

この記事の下部にあるフィードバックを残すことができます。

*記事の内容を確認するための Tom Dykstra と Rick Anderson に感謝します。*
