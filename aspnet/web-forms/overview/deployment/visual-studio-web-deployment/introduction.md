---
uid: web-forms/overview/deployment/visual-studio-web-deployment/introduction
title: 'Visual Studio を使用した ASP.NET Web デプロイ: 概要 |Microsoft Docs'
author: tdykstra
description: このチュートリアルシリーズでは、ASP.NET web アプリケーションをデプロイ (発行) して、Web Apps またはサードパーティのホスティングプロバイダーを Azure App Service する方法について説明します。その方法については、「V...
ms.author: riande
ms.date: 02/15/2013
ms.assetid: 24ad086d-865e-433c-9ac9-05f1a553da16
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/introduction
msc.type: authoredcontent
ms.openlocfilehash: 96dd31d949633e001fc595621bedbf74e98000fc
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74640236"
---
# <a name="aspnet-web-deployment-using-visual-studio-introduction"></a>Visual Studio を使用した ASP.NET Web デプロイ: 概要

[Tom Dykstra](https://github.com/tdykstra)

[スタートプロジェクトのダウンロード](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> このチュートリアルシリーズでは、Visual Studio 2012 と Azure SDK for .NET を使用して、ASP.NET web アプリケーションを Azure App Service Web Apps またはサードパーティのホスティングプロバイダーにデプロイ (発行) する方法について説明します。 ほとんどの手順は Visual Studio 2013 に似ています。
> 
> Web アプリケーションは、インターネットを介してユーザーが使用できるようにするために開発します。 ただし、web プログラミングのチュートリアルは通常、開発用コンピューターで動作する方法を説明した直後に停止します。 この一連のチュートリアルでは、web アプリを構築してテストし、準備ができていることを確認します。 次の内容 これらのチュートリアルでは、まず、テスト用にローカル開発用コンピューターの IIS にデプロイした後、ステージングと運用のために Azure またはサードパーティのホスティングプロバイダーにデプロイする方法を説明します。 デプロイするサンプルアプリケーションは、Entity Framework、SQL Server、および ASP.NET メンバーシップシステムを使用する web アプリケーションプロジェクトです。 サンプルアプリケーションでは ASP.NET Web フォームを使用しますが、表示される手順は ASP.NET MVC と Web API にも適用されます。
> 
> これらのチュートリアルでは、Visual Studio で ASP.NET を使用する方法を理解していることを前提としています。 そうでない場合は、[基本的な ASP.NET Web フォームチュートリアル](../../older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-1.md)または[基本的な ASP.NET MVC チュートリアル](../../../../mvc/overview/older-versions/getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4.md)を開始することをお勧めします。
> 
> チュートリアルに直接関係のない質問がある場合は、 [ASP.NET Deployment フォーラム](https://forums.asp.net/26.aspx/1?Configuration+and+Deployment)または[stackoverflow](http://stackoverflow.com)に投稿できます。
> 
> このコンテンツは、 [TechNet の電子書籍ギャラリー](https://social.technet.microsoft.com/wiki/contents/articles/11608.e-book-gallery-for-microsoft-technologies.aspx#ASPNETWebDeploymentusingVisualStudio)から無料の電子書籍として入手することもできます。

## <a name="overview"></a>の概要

これらのチュートリアルでは、SQL Server データベースを含む ASP.NET web アプリケーションをデプロイする手順について説明します。 まず、ローカルの開発用コンピューターの IIS に配置してテストを行い、次に Azure App Service で Web Apps し、ステージングと運用の Azure SQL Database します。 Visual Studio のワンクリック発行を使用してデプロイする方法を確認できます。コマンドラインを使用してをデプロイする方法を確認できます。

チュートリアルの数によっては、展開プロセスが困難に思えるかもしれません。 実際、基本的な手順は単純です。 ただし、実際の状況では、多くの場合、追加の配置タスクを実行する必要があります。たとえば、対象サーバーでフォルダーのアクセス許可を設定します。 これらの追加のタスクのいくつかを説明しましたが、実際のアプリケーションを正常に展開できなくなる可能性がある情報がチュートリアルに記載されていないことを願っています。

チュートリアルは順番に実行するように設計されており、各部分は前の部分に基づいています。 状況に関係のない部分はスキップできますが、その後のチュートリアルでは、手順の調整が必要になる場合があります。

## <a name="intended-audience"></a>対象読者

このチュートリアルは、次の環境で作業する ASP.NET 開発者を対象としています。

- 運用環境は、Web Apps またはサードパーティのホスティングプロバイダー Azure App Service ます。
- 配置は継続的な統合プロセスに限定されませんが、Visual Studio から直接実行できます。

[継続的デリバリー](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery.md)プロセスを使用した[ソース管理](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control.md)からのデプロイについては、コマンドラインからの展開方法を示す1つのチュートリアルを除き、これらのチュートリアルでは説明されていません。 継続的デリバリーの詳細については、次のリソースを参照してください。

- [継続的インテグレーションと継続的デリバリー (Windows Azure を使用した実際のクラウドアプリの構築)](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery.md)
- [Azure App Service で web アプリをデプロイする](https://azure.microsoft.com/documentation/articles/web-sites-deploy/)
- [エンタープライズシナリオでの Web アプリケーションの配置](../deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md)(Visual Studio 2010 向けに記述された古いチュートリアルのセットであり、エンタープライズ環境に関する有益な情報が含まれています)。

## <a name="using-a-third-party-hosting-provider"></a>サードパーティのホスティングプロバイダーの使用

このチュートリアルでは、Azure アカウントを設定し、ステージングと運用のために Azure App Service で Web Apps するアプリケーションをデプロイするプロセスについて紹介します。 ただし、任意のサードパーティ製ホスティングプロバイダーにデプロイする場合と同じ基本的な手順を使用できます。 このチュートリアルでは、Azure 固有のプロセスについて説明します。また、サードパーティのホスティングプロバイダーで予想される違いについても説明します。

## <a name="deploying-web-app-projects"></a>Web アプリプロジェクトの配置

これらのチュートリアル用にダウンロードしてデプロイするサンプルアプリケーションは、Visual Studio web アプリケーションプロジェクトです。 ただし、Visual Studio の最新の Web 発行更新プログラムをインストールする場合は、web アプリプロジェクトに対して同じデプロイ方法とツールを使用できます。

## <a name="deploying-aspnet-mvc-projects"></a>ASP.NET MVC プロジェクトの配置

サンプルアプリケーションは ASP.NET の Web フォームプロジェクトですが、実行する方法について学習したものは、ASP.NET MVC にも適用できます。 Visual Studio MVC プロジェクトは、別の形式の web アプリケーションプロジェクトです。 唯一の違いは、ASP.NET MVC またはターゲットバージョンをサポートしていないホスティングプロバイダーにデプロイする場合は、適切な ([mvc 3](http://nuget.org/packages/AspNetMvc/3.0.20105.0)、 [mvc 4](http://www.nuget.org/packages/Microsoft.AspNet.Mvc/4.0.30506.0)、または[mvc 5](http://www.nuget.org/packages/Microsoft.AspNet.Mvc)) NuGet パッケージがプロジェクトにインストールされていることを確認する必要があることです。

## <a name="programming-language"></a>プログラミング言語

サンプルアプリケーションはをC#使用しますが、チュートリアルではC#の知識は必要ありません。また、チュートリアルで示されている配置手法は言語固有ではありません。

## <a name="database-deployment-methods"></a>データベースの配置方法

Visual Studio で SQL Server データベースを web 配置と共に配置するには、次の3つの方法があります。

- Entity Framework Code First Migrations
- DbDacFx Web 配置プロバイダー
- DbFullSql Web 配置プロバイダー

このチュートリアルでは、これらのメソッドの最初の2つを使用します。 DbFullSql Web 配置プロバイダーは、SQL Server Compact から SQL Server への移行など、一部の特定のシナリオ以外では推奨されない従来の方法です。

このチュートリアルで示す方法は、SQL Server Compact ではなく SQL Server データベースを対象としています。 SQL Server Compact データベースをデプロイする方法の詳細については、「 [SQL Server Compact を使用した Visual Studio の Web 配置](../../older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-introduction-1-of-12.md)」を参照してください。

このチュートリアルで示すメソッドを使用するには、Web 配置 publish メソッドを使用する必要があります。 FTP、ファイルシステム、または FPSE などの別の発行方法を使用する場合は、「web アプリケーションの配置とは別に[データベースを](https://go.microsoft.com/fwlink/p/?LinkId=282413#databaseseparate)配置する」を参照してください。これは、Visual Studio と ASP.NET の Web 配置コンテンツマップにあります。

### <a name="entity-framework-code-first-migrations"></a>Entity Framework Code First Migrations

Entity Framework バージョン4.3 では、Microsoft によって Code First Migrations が導入されました。 Code First Migrations では、データモデルに対する増分変更を行い、それらの変更をデータベースに反映するプロセスを自動化します。 以前のバージョンの Code First では、通常、データモデルを変更するたびにデータベースを削除して再作成することを Entity Framework します。 テストデータは簡単に作成できますが、実稼働環境では、データベースを削除せずにデータベーススキーマを更新することをお勧めします。 移行機能を使用すると、Code First によってデータベースを削除および再作成せずに更新できます。 必要なスキーマ変更を行う方法を Code First が自動的に決定するようにすることも、変更をカスタマイズするコードを記述することもできます。 Code First Migrations の概要については、「 [Code First Migrations](https://msdn.microsoft.com/library/hh770484.aspx)」を参照してください。

Web プロジェクトを配置するときに、Visual Studio では、Code First Migrations によって管理されるデータベースの配置プロセスを自動化できます。 発行プロファイルを作成するときに、[Execute Code First Migrations (アプリケーションの起動時に実行)] というラベルのチェックボックスをオンにします。 この設定により、配置プロセスでは、Code First が `MigrateDatabaseToLatestVersion` 初期化子クラスを使用するように、移行先サーバー上のアプリケーションの Web.config ファイルが自動的に構成されます。

Visual Studio は、配置プロセス中にデータベースに対して何も実行しません。 配置後に配置されたアプリケーションがデータベースに初めてアクセスすると、Code First によってデータベースが自動的に作成されるか、データベーススキーマが最新バージョンに更新されます。 アプリケーションが移行シードメソッドを実装する場合、メソッドは、データベースが作成されるか、スキーマが更新された後に実行されます。

このチュートリアルでは、Code First Migrations を使用してアプリケーションデータベースをデプロイします。

### <a name="the-dbdacfx-web-deploy-provider"></a>DbDacFx Web 配置プロバイダー

Entity Framework Code First で管理されていない SQL Server データベースの場合、発行プロファイルを構成するときに [データベースの更新] というラベルのチェックボックスをオンにすることができます。 最初の配置では、ソースデータベースと一致するように、dbDacFx プロバイダーによってコピー先データベースにテーブルおよびその他のデータベースオブジェクトが作成されます。 後続の配置では、ソースデータベースと転送先データベースの間で何が異なるかがプロバイダーによって決定され、転送先データベースのスキーマがソースデータベースに合わせて更新されます。 既定では、テーブルや列が削除されたときなど、プロバイダーはデータ損失の原因となる変更を行いません。

この方法では、データベーステーブルのデータの配置は自動化されませんが、スクリプトを作成して、配置時に実行するように Visual Studio を構成することができます。 配置時にスクリプトを実行するもう1つの理由は、データの損失を引き起こす可能性があるため、自動的には実行できないスキーマ変更を行うことです。

このチュートリアルでは、dbDacFx プロバイダーを使用して、ASP.NET メンバーシップデータベースをデプロイします。

## <a name="troubleshooting-during-this-tutorial"></a>このチュートリアル中のトラブルシューティング

展開中にエラーが発生した場合、または展開されたサイトが正常に動作しない場合、エラーメッセージは常に明確な解決策を提供するわけではありません。 一般的な問題のシナリオを解決するために、[トラブルシューティングのリファレンスページ](troubleshooting.md)を利用できます。 チュートリアルを実行しているときにエラーメッセージが表示されたり動作しなかったりする場合は、必ずトラブルシューティングのページを確認してください。

## <a name="comments-welcome"></a>コメントの開始

チュートリアルのコメントは歓迎されます。チュートリアルが更新されると、チュートリアルのコメントに記載されている修正や改善の提案が行われます。

<a id="prerequisites"></a>

## <a name="prerequisites"></a>必要条件

このチュートリアルは、次の製品向けに作成されました。

- Windows 8 または Windows 7。
- [最新の更新プログラム](https://go.microsoft.com/fwlink/?LinkId=272486)を使用した visual studio 2012 または visual Studio 2012 Express for Web。
- [Azure SDK for Visual Studio 2012](https://go.microsoft.com/fwlink/?LinkId=254364)

このチュートリアルは、Visual Studio 2010 SP1 または Visual Studio 2013 を使用して実行できますが、一部のスクリーンショットは異なるため、一部の機能は異なる場合があります。

Visual Studio 2013 を使用している場合は、 [AZURE SDK for Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkID=324322)をインストールします。

Visual Studio 2010 SP1 を使用している場合は、次のソフトウェアをインストールします。

- [Azure SDK for Visual Studio 2010](https://go.microsoft.com/fwlink/?LinkID=254269)
- [LocalDB の SQL Server Express](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=SQLLocalDBOnly_11_0)
- [SQL Server Data Tools](https://msdn.microsoft.com/library/hh500335.aspx)。

コンピューターに既にある SDK の依存関係の数によっては、Azure SDK のインストールに時間がかかる場合があります (数分から30分以上)。 SDK には Visual Studio web 発行機能の最新の更新プログラムが含まれているため、azure ではなくサードパーティのホスティングプロバイダーに発行する予定の場合でも、Azure SDK が必要です。

> [!NOTE]
> このチュートリアルは、Azure SDK のバージョン1.8.1 で記述されています。 その後、追加機能を持つ新しいバージョンがリリースされました。 これらの機能について説明し、詳細情報が記載されているリソースへのリンクを紹介するチュートリアルが更新されました。

指示とスクリーンショットは Windows 8 に基づいていますが、チュートリアルでは Windows 7 の違いについて説明します。

このチュートリアルを完了するには、他にもいくつかのソフトウェアが必要ですが、まだインストールしておく必要はありません。 このチュートリアルでは、必要なときにインストールする手順について説明します。

## <a name="download-the-sample-application"></a>サンプルアプリケーションをダウンロードする

デプロイするアプリケーションは Contoso 大学という名前で、既に作成されています。 これは、 [ASP.NET サイトの Entity Framework チュートリアル](https://asp.net/entity-framework/tutorials)で説明されている Contoso 大学のアプリケーションに弱い、大学の web サイトの簡略化されたバージョンです。

前提条件がインストールされている場合は、 [Contoso 大学 web アプリケーション](https://go.microsoft.com/fwlink/p/?LinkId=282627)をダウンロードします。 *.Zip*ファイルには、プロジェクトの複数のバージョンが含まれています。 このチュートリアルの手順を実行するには、 C#フォルダーにあるプロジェクトから開始します。 チュートリアルの最後でプロジェクトがどのように表示されるかを確認するには、ContosoUniversity フォルダーでプロジェクトを開きます。

チュートリアルの手順に従ってプロジェクトを準備するには、次の手順を実行します。

1. ContosoUniversity ソリューションファイルC#を ContosoUniversity という名前のフォルダーのフォルダーに保存します。このフォルダーは、Visual Studio プロジェクトを操作するために使用する任意のフォルダーに保存します。

    既定では、Visual Studio 2012 の次のフォルダーになります。

    `C:\Users\<username>\Documents\Visual Studio 2012\Projects`

    (このチュートリアルのスクリーンショットでは、プロジェクトフォルダーは `C`: ドライブのルートディレクトリにあります)。
2. Visual Studio を起動し、プロジェクトを開きます。
3. **ソリューションエクスプローラー**で、ソリューションを右クリックし、 **[Enablenuget パッケージの復元]** をクリックします。
4. ソリューションをビルドします。
5. コンパイルエラーが発生した場合は、NuGet パッケージを手動で復元します。

    1. **ソリューションエクスプローラー**で、ソリューションを右クリックし、 **[ソリューションの NuGet パッケージの管理]** をクリックします。
    2. **[Nuget パッケージの管理]** ダイアログボックスの上部に、**このソリューションにいくつかの NuGet パッケージが不足していることが表示されます。クリックして復元します。** **[復元]** ボタンをクリックします。
    3. ソリューションをリビルドします。
6. Ctrl キーを押しながら F5 キーを押してアプリケーションを実行します。

    アプリケーションが Contoso 大学のホームページに表示されます。

    ![ホームページの開発](introduction/_static/image1.png)

    (SQL Server Express LocalDB インスタンスが Visual Studio によって起動されるまでの間、待機時間が発生する場合があります。この処理に時間がかかりすぎると、タイムアウトエラーが発生する可能性があります。 その場合は、もう一度プロジェクトを開始します)。

Web サイトのページには、メニューバーからアクセスでき、次の機能を実行できます。

- 学生の統計情報を表示します ([バージョン情報] ページ)。
- 学生を表示、編集、削除、追加します。
- コースを表示および編集します。
- インストラクターを表示および編集します。
- 部門を表示および編集します。

次に、いくつかの代表的なページのスクリーンショットを示します。

![学生ページの開発](introduction/_static/image2.png)

![学生の追加ページ Dev](introduction/_static/image3.png)

## <a name="review-application-features-that-affect-deployment"></a>展開に影響するアプリケーションの機能を確認する

アプリケーションの次の機能は、アプリケーションの展開方法または展開方法に影響します。 これらについては、シリーズの次のチュートリアルで詳細に説明されています。

- Contoso 大学は、SQL Server データベースを使用して、学生や教師の名前などのアプリケーションデータを格納します。 このデータベースには、テストデータと実稼働データが混在しています。また、運用環境に配置するときは、テストデータを除外する必要があります。
- アプリケーションでは、ユーザーアカウント情報を SQL Server データベースに格納する ASP.NET メンバーシップシステムが使用されます。 アプリケーションでは、一部の制限された情報にアクセスできる管理者ユーザーを定義します。 テストアカウントを使用せずに、管理者アカウントを使用してメンバーシップデータベースをデプロイする必要があります。
- アプリケーションでは、サードパーティのエラーログとレポートユーティリティを使用します。 このユーティリティは、アプリケーションと共に配置する必要があるアセンブリで提供されます。
- エラーログユーティリティは、エラー情報を XML ファイル内のファイルフォルダーに書き込みます。 ASP.NET が展開されたサイトの下で実行されるアカウントにこのフォルダーへの書き込みアクセス許可があることを確認する必要があります。また、このフォルダーを展開から除外する必要があります。 (そうでない場合は、テスト環境からのエラーログデータが運用環境に配置されたり、運用エラーログファイルが削除されたりする可能性があります)。
- アプリケーションには、配置先の環境 (テスト、ステージング、または運用) に応じて、配置された*web.config*ファイルで変更する必要があるいくつかの設定と、ビルド構成 (デバッグまたはリリース) に応じて変更する必要があるその他の設定が含まれます。
- Visual Studio ソリューションには、クラスライブラリプロジェクトが含まれています。 プロジェクト自体ではなく、このプロジェクトが生成するアセンブリだけを配置する必要があります。

## <a name="summary"></a>要約

このシリーズの最初のチュートリアルでは、サンプルの Visual Studio プロジェクトをダウンロードし、アプリケーションのデプロイ方法に影響を与えるサイトの機能を確認しました。 次のチュートリアルでは、これらのいくつかを自動的に処理するように設定することによって、デプロイを準備します。 他のユーザーは手動で行うことができます。

> [!div class="step-by-step"]
> [次へ](preparing-databases.md)
