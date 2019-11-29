---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/configuring-a-website-that-uses-application-services-cs
title: アプリケーションサービスを使用する Web サイトのC#構成 () |Microsoft Docs
author: rick-anderson
description: ASP.NET バージョン2.0 では、一連のアプリケーションサービスが導入されました。このサービスは、.NET Framework の一部であり、そのため、
ms.author: riande
ms.date: 04/23/2009
ms.assetid: 1e33d1c6-3f9f-4c26-81e2-2a8f8907bb05
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/configuring-a-website-that-uses-application-services-cs
msc.type: authoredcontent
ms.openlocfilehash: 72aaca84b8c8d6e558d4c946faa57fa999d48bf8
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74570193"
---
# <a name="configuring-a-website-that-uses-application-services-c"></a>アプリケーション サービスを使用する Web サイトを構成する (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[コードのダウンロード](https://download.microsoft.com/download/E/6/F/E6FE3A1F-EE3A-4119-989A-33D1A9F6F6DD/ASPNET_Hosting_Tutorial_09_CS.zip)または[PDF のダウンロード](https://download.microsoft.com/download/C/3/9/C391A649-B357-4A7B-BAA4-48C96871FEA6/aspnet_tutorial09_AppServicesConfig_cs.pdf)

> ASP.NET バージョン2.0 では、一連のアプリケーションサービスが導入されました。これは .NET Framework の一部であり、web アプリケーションに豊富な機能を追加するために使用できるビルディングブロックサービスのスイートとして機能します。 このチュートリアルでは、運用環境でアプリケーションサービスを使用するように web サイトを構成し、運用環境でのユーザーアカウントとロールの管理に関する一般的な問題に対処する方法について説明します。

## <a name="introduction"></a>はじめに

ASP.NET バージョン2.0 では、一連の*アプリケーションサービス*が導入されました。これは .NET Framework の一部であり、web アプリケーションに豊富な機能を追加するために使用できるビルディングブロックサービスのスイートとして機能します。 アプリケーションサービスには次のものが含まれます。

- **メンバーシップ**-ユーザーアカウントを作成および管理するための API です。
- **ロール**-ユーザーをグループに分類するための API です。
- **Profile** -ユーザー固有のカスタムコンテンツを格納するための API。
- **サイトマップ**-階層の形式でサイトの論理構造を定義するための API。これは、メニューや階層リンクなどのナビゲーションコントロールを使用して表示できます。
- **パーソナル化**-カスタマイズ設定を維持するための API。これは、ほとんどの場合、 [*web パーツ*](https://msdn.microsoft.com/library/e0s9t4ck.aspx)で使用されます。
- **正常性の監視**-実行中の web アプリケーションのパフォーマンス、セキュリティ、エラー、およびその他のシステム正常性メトリックを監視するための API です。

アプリケーションサービス Api は、特定の実装に関連付けられていません。 代わりに、特定の*プロバイダー*を使用するようにアプリケーションサービスに指示します。このプロバイダーは、特定のテクノロジを使用してサービスを実装します。 Web ホスティング会社でホストされているインターネットベースの web アプリケーションで最もよく使用されるプロバイダーは、SQL Server データベースの実装を使用するプロバイダーです。 たとえば、`SqlMembershipProvider` は、ユーザーアカウント情報を Microsoft SQL Server データベースに格納するメンバーシップ API のプロバイダーです。

アプリケーションサービスと SQL Server プロバイダーを使用すると、アプリケーションを展開するときにいくつかの課題が生じます。 手始めとして、アプリケーションサービスデータベースオブジェクトは、開発データベースと運用データベースの両方で適切に作成され、適切に初期化されている必要があります。 また、重要な構成設定を行う必要があります。

> [!NOTE]
> アプリケーションサービス Api は、API の実装の詳細を実行時に提供できるようにするデザインパターンである[*プロバイダーモデル*](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx)を使用して設計されています。 .NET Framework には、`SqlMembershipProvider` や `SqlRoleProvider`など、使用できるアプリケーションサービスプロバイダーが多数付属しています。これは、SQL Server データベースの実装を使用するメンバーシップおよびロール Api のプロバイダーです。 カスタムプロバイダーを作成してプラグインすることもできます。 実際、書籍レビュー web アプリケーションには、サイトマップ API (`ReviewSiteMapProvider`) のカスタムプロバイダーが既に含まれています。これにより、データベース内の `Genres` と `Books` テーブルのデータからサイトマップが構築されます。

このチュートリアルでは、まず、書籍レビュー web アプリケーションを拡張して、メンバーシップとロールの Api を使用する方法について説明します。 次に、アプリケーションサービスを使用する web アプリケーションを SQL Server データベース実装と共に配置し、最後に、運用環境でのユーザーアカウントとロールの管理に関する一般的な問題に対処します。

## <a name="updates-to-the-book-reviews-application"></a>書籍レビューアプリケーションの更新

これまでのいくつかのチュートリアルでは、書籍レビュー web アプリケーションが静的な web サイトから動的なデータドリブン web アプリケーションに更新され、ジャンルとレビューを管理するための管理ページが用意されています。 ただし、この管理セクションは現在保護されていません。管理ページの URL を知っている (または推測された) ユーザーは、サイトでのレビューの waltz と作成、編集、または削除を行うことができます。 Web サイトの特定の部分を保護する一般的な方法は、ユーザーアカウントを実装してから、URL 承認規則を使用して特定のユーザーまたはロールへのアクセスを制限することです。 このチュートリアルでダウンロードできる書籍レビュー web アプリケーションでは、ユーザーアカウントとロールがサポートされています。 管理者という名前のロールが1つ定義されており、このロールのユーザーのみが管理ページにアクセスできます。

> [!NOTE]
> 彼は、"Scott"、"Jisun"、"Alice" の3人のユーザーアカウントを作成しました。 3人のユーザーはすべて、パスワードと同じパスワードを持って**います。** Scott と Jisun は管理者ロールに含まれていますが、Alice はありません。 サイトの管理者以外のページには、匿名ユーザーが引き続きアクセスできます。 つまり、サイトにアクセスするためにサインインする必要はありません。ただし、管理する場合は、管理者ロールのユーザーとしてサインインする必要があります。

[Book review application s] マスターページが更新され、認証および匿名ユーザー用に異なるユーザーインターフェイスが追加されました。 匿名ユーザーがサイトにアクセスすると、右上隅にログインリンクが表示されます。 認証されたユーザーには、"Welcome back, *username*!" というメッセージが表示されます。 また、ログアウトするためのリンクがあります。また、ログインページ (`~/Login.aspx`) もあります。これには、ビジターを認証するためのユーザーインターフェイスとロジックを提供するログイン Web コントロールが含まれています。 新しいアカウントを作成できるのは管理者だけです。 (`~/Admin` フォルダー内のユーザーアカウントを作成および管理するためのページがあります)。

### <a name="configuring-the-membership-and-roles-apis"></a>メンバーシップ Api とロール Api の構成

書籍レビュー web アプリケーションは、メンバーシップとロール Api を使用してユーザーアカウントをサポートし、それらのユーザーをロール (つまり、管理者ロール) にグループ化します。 `SqlMembershipProvider` および `SqlRoleProvider` プロバイダークラスが使用されます。これは、アカウントとロールの情報を SQL Server データベースに格納するためです。

> [!NOTE]
> このチュートリアルは、メンバーシップとロールの Api をサポートする web アプリケーションの構成に関する詳細な調査を目的としたものではありません。 これらの Api と、それらを使用するように web サイトを構成するために必要な手順について詳しくは、 [*Web サイトのセキュリティ*](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)に関するチュートリアルをご覧ください。

SQL Server データベースでアプリケーションサービスを使用するには、まず、ユーザーアカウントとロール情報を格納するデータベースに、これらのプロバイダーによって使用されるデータベースオブジェクトを追加する必要があります。 これらの必要なデータベースオブジェクトには、さまざまなテーブル、ビュー、およびストアドプロシージャが含まれます。 特に指定しない限り、`SqlMembershipProvider` および `SqlRoleProvider` プロバイダークラスは、application s `App_Data` フォルダーにある `ASPNETDB` という SQL Server Express エディションのデータベースを使用します。このようなデータベースが存在しない場合は、実行時にこれらのプロバイダーによって必要なデータベースオブジェクトと共に自動的に作成されます。

Web サイトのアプリケーション固有のデータが格納されているのと同じデータベースに、アプリケーションサービスデータベースオブジェクトを作成することは可能であり、通常は理想的です。 .NET Framework には、指定されたデータベースにデータベースオブジェクトをインストールする `aspnet_regsql.exe` という名前のツールが付属しています。 このツールを使用して、これらのオブジェクトを `App_Data` フォルダー (開発データベース) の `Reviews.mdf` データベースに追加しました。 このツールの使用方法については、このチュートリアルの後半で、これらのオブジェクトを実稼働データベースに追加するときに説明します。

アプリケーションサービスデータベースオブジェクトを `ASPNETDB` 以外のデータベースに追加する場合は、適切なデータベースを使用するように `SqlMembershipProvider` および `SqlRoleProvider` プロバイダークラスの構成をカスタマイズする必要があります。 メンバーシッププロバイダーをカスタマイズするには、`Web.config`の `<system.web>` セクション内に[ *&lt;メンバーシップ&gt; 要素*](https://msdn.microsoft.com/library/1b9hw62f.aspx)を追加します。ロールプロバイダーを構成するには、 [ *&lt;roleManager&gt; 要素*](https://msdn.microsoft.com/library/ms164660.aspx)を使用します。 次のスニペットは、「Book review application s `Web.config`」に記載されています。また、メンバーシップとロールの Api の構成設定についても説明しています。 `SqlMembershipProvider` と `SqlRoleProvider` プロバイダーをそれぞれ使用する新しいプロバイダー `ReviewMembership` と `ReviewRole` が登録されていることに注意してください。

[!code-xml[Main](configuring-a-website-that-uses-application-services-cs/samples/sample1.xml)]

`Web.config` file s `<authentication>` 要素は、フォームベースの認証をサポートするように構成されています。

[!code-xml[Main](configuring-a-website-that-uses-application-services-cs/samples/sample2.xml)]

### <a name="limiting-access-to-the-administration-pages"></a>管理ページへのアクセスの制限

ASP.NET を使用すると、特定のファイルまたはフォルダーへのアクセスを、ユーザーまたはロールによって*URL 承認*機能を介して簡単に許可または拒否できます。 (URL 承認については、 *iis と ASP.NET 開発サーバー*チュートリアルの主な違いについて簡単に説明し、iis と ASP.NET 開発サーバーが静的コンテンツと動的コンテンツに対して異なる url 承認規則を適用する方法を示しています)。管理者ロールのユーザーを除き、`~/Admin` フォルダーへのアクセスを禁止する必要があるため、このフォルダーに URL 承認規則を追加する必要があります。 具体的には、URL 承認規則では、管理者ロールのユーザーに許可し、他のすべてのユーザーを拒否する必要があります。 これを行うには、次の内容で `~/Admin` フォルダーに `Web.config` ファイルを追加します。

[!code-xml[Main](configuring-a-website-that-uses-application-services-cs/samples/sample3.xml)]

ASP.NET s URL 承認機能の詳細と、この機能を使用してユーザーおよびロールの承認規則を確認する方法の詳細については、「 [*Web サイトのセキュリティチュートリアル*](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)」の「[*ユーザーベースの承認*](../../older-versions-security/membership/user-based-authorization-cs.md)と[*ロールベースの承認*](../../older-versions-security/roles/role-based-authorization-cs.md)のチュートリアル」を参照してください。

## <a name="deploying-a-web-application-that-uses-application-services"></a>アプリケーションサービスを使用する Web アプリケーションの配置

アプリケーションサービスを使用する web サイトおよびアプリケーションサービス情報をデータベースに格納するプロバイダーを配置する場合は、アプリケーションサービスに必要なデータベースオブジェクトを実稼働データベースに作成することが不可欠です。 初期状態では、実稼働データベースにはこれらのオブジェクトが含まれていないため、アプリケーションを最初に配置するとき (または、アプリケーションサービスを追加した後に初めて配置するとき) は、次のような必要なデータベースオブジェクトを取得するための追加の手順を実行する必要があります。実稼働データベース。

開発環境で作成されたユーザーアカウントを運用環境にレプリケートする予定がある場合は、アプリケーションサービスを使用する web サイトをデプロイするときに、もう1つの問題が発生する可能性があります。 メンバーシップとロールの構成によっては、開発環境で作成されたユーザーアカウントを実稼働データベースに正常にコピーした場合でも、これらのユーザーが運用環境で web アプリケーションにサインインできなくなる可能性があります。 この問題の原因を確認し、この問題が発生しないようにする方法について説明します。

ASP.NET には、Visual Studio から起動できる便利な[*Web サイト管理ツール (WSAT)* ](https://msdn.microsoft.com/library/yy40ytx0.aspx)が付属しています。このツールを使用すると、ユーザーアカウント、ロール、および承認規則を web ベースのインターフェイスを介して管理できます。 残念ながら、WSAT はローカル web サイトに対してのみ機能します。つまり、運用環境で web アプリケーションのユーザーアカウント、ロール、および承認規則をリモートで管理するために使用することはできません。 運用 web サイトから WSAT のような動作を実装するためのさまざまな方法について説明します。

### <a name="adding-the-database-objects-using-aspnet_regsqlexe"></a>Aspnet\_使用してデータベースオブジェクトを追加する

*データベースの配置*に関するチュートリアルでは、開発データベースから実稼働データベースにテーブルとデータをコピーする方法を説明しました。これらの手法を使用すると、アプリケーションサービスデータベースオブジェクトを実稼働データベースにコピーすることができます。 もう1つのオプションは、アプリケーションサービスデータベースオブジェクトをデータベースから追加または削除する `aspnet_regsql.exe` ツールです。

> [!NOTE]
> `aspnet_regsql.exe` ツールは、指定されたデータベースにデータベースオブジェクトを作成します。 これらのデータベースオブジェクトのデータは、開発データベースから実稼働データベースに移行されません。 開発データベースのユーザーアカウントとロール情報を運用データベースにコピーする場合は、「*データベースの配置*」チュートリアルで説明されている手法を使用します。

`aspnet_regsql.exe` ツールを使用して、実稼働データベースにデータベースオブジェクトを追加する方法を見てみましょう。 まず、エクスプローラーを開き、コンピューター上の .NET Framework version 2.0 ディレクトリに移動します。% WINDIR% \NET\Framework\v2.0.50727. `aspnet_regsql.exe` ツールが見つかります。 このツールはコマンドラインから使用できますが、グラフィカルユーザーインターフェイスも含まれています。`aspnet_regsql.exe` ファイルをダブルクリックして、グラフィカルコンポーネントを起動します。

ツールを起動するには、その目的を説明するスプラッシュスクリーンを表示します。 [次へ] をクリックして、図1に示す [セットアップオプションの選択] 画面に進みます。 ここでは、アプリケーションサービスデータベースオブジェクトを追加するか、データベースから削除するかを選択できます。 これらのオブジェクトを実稼働データベースに追加するには、[アプリケーションサービスの SQL Server を構成する] オプションを選択し、[次へ] をクリックします。

[![SQL Server の構成を選択してアプリケーションサービス](configuring-a-website-that-uses-application-services-cs/_static/image2.jpg)](configuring-a-website-that-uses-application-services-cs/_static/image1.jpg)

**図 1**: アプリケーションサービスの SQL Server の構成を選択する ([クリックすると、フルサイズの画像が表示](configuring-a-website-that-uses-application-services-cs/_static/image3.jpg)される)

[サーバーとデータベースの選択] 画面で、データベースに接続するための情報の入力を求められます。 Web ホスティング会社から提供されたデータベースサーバー、セキュリティ資格情報、およびデータベース名を入力し、[次へ] をクリックします。

> [!NOTE]
> データベースサーバーと資格情報を入力すると、データベースのドロップダウンリストを展開するときにエラーが表示されることがあります。 `aspnet_regsql.exe` ツールは、`sysdatabases` システムテーブルにクエリを行ってサーバー上のデータベースの一覧を取得しますが、一部の web ホスティング企業はデータベースサーバーをロックダウンして、この情報が公開されていないことを確認します。 このエラーが表示された場合は、ドロップダウンリストにデータベース名を直接入力できます。

[データベースの接続情報を使用してツールを提供 ![](configuring-a-website-that-uses-application-services-cs/_static/image5.jpg)](configuring-a-website-that-uses-application-services-cs/_static/image4.jpg)

**図 2**: データベース s の接続情報を使用してツールを指定[する (クリックすると、フルサイズの画像が表示](configuring-a-website-that-uses-application-services-cs/_static/image6.jpg)されます)

次の画面には、実行しようとしている操作の概要が示されます。つまり、アプリケーションサービスデータベースオブジェクトが指定されたデータベースに追加されます。 この操作を完了するには、[次へ] をクリックします。 しばらくすると、最後の画面が表示され、データベースオブジェクトが追加されたことがわかります (図3を参照)。

[![成功しました。アプリケーションサービスデータベースオブジェクトが運用データベースに追加されました](configuring-a-website-that-uses-application-services-cs/_static/image8.jpg)](configuring-a-website-that-uses-application-services-cs/_static/image7.jpg)

**図 3**: 成功しました。 アプリケーションサービスデータベースオブジェクトが実稼働データベースに追加されました ([クリックすると、フルサイズの画像が表示](configuring-a-website-that-uses-application-services-cs/_static/image9.jpg)されます)

アプリケーションサービスデータベースオブジェクトが実稼働データベースに正常に追加されたことを確認するには、SQL Server Management Studio を開き、実稼働データベースに接続します。 図4に示すように、データベース内のアプリケーションサービスデータベーステーブル、`aspnet_Applications`、`aspnet_Membership`、`aspnet_Users`などが表示されます。

[![、データベースオブジェクトが実稼働データベースに追加されたことを確認します。](configuring-a-website-that-uses-application-services-cs/_static/image11.jpg)](configuring-a-website-that-uses-application-services-cs/_static/image10.jpg)

**図 4**: データベースオブジェクトが実稼働データベースに追加されたことを確認[する (クリックすると、フルサイズの画像が表示](configuring-a-website-that-uses-application-services-cs/_static/image12.jpg)されます)

アプリケーションサービスの使用を開始した後、初めて web アプリケーションを配置するときにのみ、`aspnet_regsql.exe` ツールを使用する必要があります。 これらのデータベースオブジェクトを実稼働データベースに配置した後は、再追加または変更する必要はありません。

### <a name="copying-user-accounts-from-development-to-production"></a>開発環境から運用環境へのユーザーアカウントのコピー

`SqlMembershipProvider` および `SqlRoleProvider` プロバイダークラスを使用してアプリケーションサービス情報を SQL Server データベースに格納する場合、ユーザーアカウントとロール情報は、`aspnet_Users`、`aspnet_Membership`、`aspnet_Roles`、`aspnet_UsersInRoles`など、さまざまなデータベーステーブルに格納されます。 開発時に開発環境でユーザーアカウントを作成する場合は、該当するデータベーステーブルから対応するレコードをコピーすることで、これらのユーザーアカウントを実稼働環境にレプリケートできます。 データベース公開ウィザードを使用してアプリケーションサービスデータベースオブジェクトを配置した場合、レコードもコピーすることを選択した可能性があります。これにより、開発で作成されたユーザーアカウントも運用環境に存在することになります。 ただし、構成設定によっては、アカウントが開発中に作成され、運用環境にコピーされたユーザーは、運用 web サイトからログインできないことがわかります。 何をするのでしょうか。

`SqlMembershipProvider` および `SqlRoleProvider` プロバイダークラスは、1つのデータベースが複数のアプリケーションのユーザーストアとして機能するように設計されています。つまり、理論的には、同じ名前のユーザー名とロールを持つユーザーを持つことができます。 この柔軟性を実現するために、データベースは `aspnet_Applications` テーブルにアプリケーションの一覧を保持し、各ユーザーはこれらのアプリケーションのいずれかに関連付けられています。 具体的には、`aspnet_Users` テーブルには、各ユーザーを `aspnet_Applications` テーブル内のレコードに結び付ける `ApplicationId` 列があります。

`aspnet_Applications` テーブルには、`ApplicationId` 列に加えて、アプリケーションのわかりやすい名前を提供する `ApplicationName` 列も含まれています。 Web サイトでユーザーアカウントを使用しようとすると (ログインページからユーザーの資格情報を検証する場合など)、使用するアプリケーションを `SqlMembershipProvider` クラスに通知する必要があります。 これは通常、アプリケーション名を指定することによって行われます。この値は、`applicationName` 属性を介して `Web.config` のプロバイダーの構成から取得されます。

しかし、`Web.config`で `applicationName` 属性が指定されていない場合はどうなるでしょうか。 このような場合、メンバーシップシステムはアプリケーションのルートパスを `applicationName` 値として使用します。 `Web.config`で `applicationName` 属性が明示的に設定されていない場合は、開発環境と運用環境が異なるアプリケーションルートを使用する可能性があるため、アプリケーションサービスの異なるアプリケーション名に関連付けられます。 このような不一致が発生した場合、開発環境で作成されたユーザーには、運用環境の `ApplicationId` 値と一致しない `ApplicationId` 値が設定されます。 結果として、ユーザーはログインできなくなります。

> [!NOTE]
> `ApplicationId` 値が一致しない状態でユーザーアカウントが運用環境にコピーされた場合は、これらの不適切な `ApplicationId` 値を運用環境で使用されている `ApplicationId` に更新するクエリを記述できます。 更新されると、開発環境で作成されたアカウントを持つユーザーは、運用環境で web アプリケーションにサインインできるようになります。

2つの環境が同じ `ApplicationId` を使用するようにするための簡単な手順があることは、すべてのアプリケーションサービスプロバイダーに対して `Web.config` に `applicationName` 属性を明示的に設定することです。 `applicationName` 属性を明示的に `<membership>` と `<roleManager>` 要素の "BookReviews" に設定しています。このスニペットは `Web.config` 表示されています。

[!code-xml[Main](configuring-a-website-that-uses-application-services-cs/samples/sample4.xml)]

`applicationName` 属性とその背後にある論理的根拠の設定の詳細については、 [*Scott Guthrie*](https://weblogs.asp.net/scottgu/) s のブログ投稿を参照してください。 [*ASP.NET メンバーシップやその他のプロバイダーを構成するときは、必ず applicationName プロパティを設定*](https://weblogs.asp.net/scottgu/443634)してください。

### <a name="managing-user-accounts-in-the-production-environment"></a>運用環境でのユーザーアカウントの管理

ASP.NET Web サイト管理ツール (WSAT) を使用すると、ユーザーアカウントの作成と管理、ロールの定義と適用、およびユーザーとロールベースの承認規則のスペルチェックを簡単に行うことができます。 WSAT を Visual Studio から起動するには、ソリューションエクスプローラーに移動し、ASP.NET 構成アイコンをクリックするか、Web サイトまたはプロジェクトのメニューに移動し、[ASP.NET 構成] メニュー項目を選択します。 残念ながら、WSAT はローカル web サイトでのみ使用できます。 したがって、ワークステーションの WSAT を使用して、運用環境で web サイトを管理することはできません。

WSAT によって公開されているすべての機能は、メンバーシップとロールの Api を使用してプログラムで入手できます。さらに、WSAT 画面の多くは、標準の ASP.NET ログイン関連のコントロールを使用しています。 つまり、必要な管理機能を提供する ASP.NET ページを web サイトに追加できます。

前のチュートリアルでは、ブックレビュー web アプリケーションを更新して `~/Admin` フォルダーを含め、このフォルダーは管理者ロールのユーザーのみを許可するように構成されていることを思い出してください。 `CreateAccount.aspx` という名前のフォルダーに、管理者が新しいユーザーアカウントを作成するためのページを追加しました。 このページでは、CreateUserWizard コントロールを使用して、新しいユーザーアカウントを作成するためのユーザーインターフェイスとバックエンドロジックを表示します。 さらに、新しいユーザーを管理者ロールに追加する必要があるかどうかを確認するチェックボックスを含めるようにコントロールをカスタマイズしました (図5を参照)。 少しの作業では、WSAT によって提供されるユーザーおよびロールの管理関連タスクを実装するカスタムページのセットを作成できます。

> [!NOTE]
> ログイン関連の ASP.NET Web コントロールと共に Membership Api と Roles Api を使用する方法の詳細については、「 [*Web サイトのセキュリティ*](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)に関するチュートリアル」を参照してください。 CreateUserWizard コントロールのカスタマイズの詳細については、「[*ユーザーアカウントの作成*](../../older-versions-security/membership/creating-user-accounts-cs.md)」および「[*その他のユーザー情報の保存*](../../older-versions-security/membership/storing-additional-user-information-cs.md)」を参照してください。または、 [*CreateUserWizard コントロールのカスタマイズ*](http://aspnet.4guysfromrolla.com/articles/070506-1.aspx)に関する記事「 [*erich peterson*](http://www.erichpeterson.com/) s」を参照してください。

[![管理者は新しいユーザーアカウントを作成できます。](configuring-a-website-that-uses-application-services-cs/_static/image14.jpg)](configuring-a-website-that-uses-application-services-cs/_static/image13.jpg)

**図 5**: 管理者は新しいユーザーアカウントを作成できます ([クリックすると、フルサイズの画像が表示](configuring-a-website-that-uses-application-services-cs/_static/image15.jpg)される)

WSAT の完全な機能が必要な場合は、 [ *「独自の Web サイト管理ツールをロール*](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx)アウトする」をご覧ください。このツールでは、作成者 Dan clem がカスタムの WSAT に似たツールを構築するプロセスを説明しています。 Dan は、アプリケーションのソースコード ( C#) を共有し、ホストされている web サイトに追加するための詳細な手順を示します。

## <a name="summary"></a>要約

アプリケーションサービスデータベースの実装を使用する web アプリケーションを配置する場合は、まず、実稼働データベースに必要なデータベースオブジェクトがあることを確認する必要があります。 これらのオブジェクトは、「*データベースの配置*」チュートリアルで説明されている手法を使用して追加できます。または、このチュートリアルで説明したように、`aspnet_regsql.exe` ツールを使用することもできます。 開発環境および運用環境で使用されているアプリケーション名の同期を中心に説明した他の課題 (開発環境で作成されたユーザーとロールが運用環境で有効になるようにする場合は重要です) との手法運用環境でのユーザーとロールの管理。

プログラミングを楽しんでください。

### <a name="further-reading"></a>関連項目

このチュートリアルで説明しているトピックの詳細については、次のリソースを参照してください。

- [*ASP.NET SQL Server 登録ツール (aspnet_regsql)* ](https://msdn.microsoft.com/library/ms229862.aspx)
- [*SQL Server 用のアプリケーションサービスデータベースの作成*](https://msdn.microsoft.com/library/x28wfk74.aspx)
- [*SQL Server でのメンバーシップスキーマの作成*](../../older-versions-security/membership/creating-the-membership-schema-in-sql-server-cs.md)
- [*ASP.NET s のメンバーシップ、ロール、およびプロファイルを調べています*](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)
- [*独自の Web サイト管理ツールをロールする*](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx)
- [*Web サイトのセキュリティに関するチュートリアル*](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)
- [*Web サイト管理ツールの概要*](https://msdn.microsoft.com/library/yy40ytx0.aspx)

> [!div class="step-by-step"]
> [前へ](configuring-the-production-web-application-to-use-the-production-database-cs.md)
> [次へ](strategies-for-database-development-and-deployment-cs.md)
