---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12
title: 'Visual Studio または Visual Web Developer を使用した SQL Server Compact を使用した ASP.NET Web アプリケーションのデプロイ: SQL Server データベース更新プログラムのデプロイ-11/12 |Microsoft Docs'
author: tdykstra
description: この一連のチュートリアルでは、Visual Stu... を使用して SQL Server Compact データベースを含む ASP.NET web アプリケーションプロジェクトをデプロイ (発行) する方法について説明します。
ms.author: riande
ms.date: 11/17/2011
ms.assetid: 5e2bb092-cb22-4511-ad0a-22ae12dd99b3
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12
msc.type: authoredcontent
ms.openlocfilehash: 0894c0ac24737e66b6960ef3d48aa17f78c6aa1d
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74621068"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-a-sql-server-database-update---11-of-12"></a>Visual Studio または Visual Web Developer を使用した SQL Server Compact を使用した ASP.NET Web アプリケーションのデプロイ: SQL Server データベース更新プログラムのデプロイ-11/12

[Tom Dykstra](https://github.com/tdykstra)

[スタートプロジェクトのダウンロード](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> この一連のチュートリアルでは、Visual Studio 2012 RC または Visual Studio Express 2012 RC for Web を使用して SQL Server Compact データベースを含む ASP.NET web アプリケーションプロジェクトをデプロイ (発行) する方法について説明します。 Web 発行の更新をインストールする場合は、Visual Studio 2010 を使用することもできます。 シリーズの概要については、[シリーズの最初のチュートリアル](deployment-to-a-hosting-provider-introduction-1-of-12.md)を参照してください。
> 
> Visual Studio 2012 の RC リリース後に導入された配置機能を示すチュートリアルについては、SQL Server Compact 以外の SQL Server のエディションをデプロイする方法、および Windows Azure Web サイトへのデプロイ方法については、「 [ASP.NET Web deployment Using Visual studio](../../deployment/visual-studio-web-deployment/introduction.md)」を参照してください。

## <a name="overview"></a>の概要

このチュートリアルでは、データベースの更新を完全な SQL Server データベースに配置する方法について説明します。 Code First Migrations はデータベースを更新するすべての作業を実行するため、このプロセスは「[データベースの更新の配置](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md)」チュートリアルの SQL Server Compact とほぼ同じです。

リマインダー: チュートリアルを実行しているときにエラーメッセージが表示されたり機能しない場合は、必ず[トラブルシューティングのページ](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)を確認してください。

## <a name="adding-a-new-column-to-a-table"></a>テーブルへの新しい列の追加

チュートリアルのこのセクションでは、データベースの変更とそれに対応するコードの変更を行い、テスト環境と運用環境に配置するための準備として Visual Studio でテストします。 この変更には、`Instructor` エンティティに `OfficeHours` 列を追加し、**インストラクター** web ページに新しい情報を表示する作業が含まれます。

ContosoUniversity プロジェクトで*Instructor.cs*を開き、`HireDate` と `Courses` のプロパティの間に次のプロパティを追加します。

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample1.cs)]

テストデータを使用して新しい列をシードするように、初期化子クラスを更新します。 *Migrations\ configuration.cs*を開き、`var instructors = new List<Instructor>` 開始するコードブロックを、新しい列を含む次のコードブロックに置き換えます。

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample2.cs)]

ContosoUniversity プロジェクトで、*講師*を開き、最初の `GridView` コントロールの終了 `</Columns>` タグの直前に、office 時間の新しいテンプレートフィールドを追加します。

[!code-aspx[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample3.aspx)]

ソリューションをビルドします。

**パッケージマネージャーコンソール**ウィンドウを開き、**既定のプロジェクト**として [ContosoUniversity] を選択します。

次のコマンドを入力します。

[!code-powershell[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample4.ps1)]

アプリケーションを実行し、 **[インストラクター]** ページを選択します。 このページの読み込みには、通常よりも少し時間がかかります。これは、Entity Framework によってデータベースが再作成され、テストデータでシード処理されるためです。

[![Instructors_page_with_office_hours](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image1.png)

## <a name="deploying-the-database-update-to-the-test-environment"></a>テスト環境へのデータベースの更新の配置

Code First Migrations を使用する場合、データベースの変更を SQL Server に配置する方法は SQL Server Compact の場合と同じです。 ただし、SQL Server Compact から SQL Server に移行するように設定されているため、テスト発行プロファイルを変更する必要があります。

最初の手順では、前のチュートリアルで作成した接続文字列の変換を削除します。 SQL Server に移行するために **[SQL のパッケージ化/発行]** タブを構成する前と同様に、発行プロファイルで接続文字列の変換を指定するので、これらは不要になりました。

*Web.config ファイルを*開き、`connectionStrings` 要素を削除します。 *Web.config ファイルの*唯一の変換は、`appSettings` 要素の `Environment` 値を示します。

発行プロファイルを更新して、テスト環境に発行できるようになりました。

Web の**発行**ウィザードを開き、 **[プロファイル]** タブに切り替えます。

**テスト**発行プロファイルを選択します。

**[設定]** タブを選択します。

[**新しいデータベース公開の機能強化を有効にする] を**クリックします。

**Schoolcontext.cs**の [接続文字列] ボックスに、前のチュートリアルの*web.config 変換ファイル*で使用したものと同じ値を入力します。

[!code-console[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample5.cmd)]

**[Code First Migrations の実行 (アプリケーションの起動時に実行)]** を選択します。 (使用している Visual Studio のバージョンでは、 **[Code First Migrations の適用]** チェックボックスがオンになっている可能性があります)。

**Defaultconnection**の [接続文字列] ボックスに、前のチュートリアルの*web.config 変換ファイル*で使用したものと同じ値を入力します。

[!code-console[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample6.cmd)]

**更新データベース**をクリアしたままにします。

**[発行]** をクリックします。

Visual Studio によってコードの変更がテスト環境に配置され、ブラウザーが開き、Contoso 大学のホームページが表示されます。

[インストラクター] ページを選択します。

アプリケーションでこのページを実行すると、データベースへのアクセスが試行されます。 Code First Migrations データベースが最新であるかどうかを確認し、最新の移行がまだ適用されていないことを検出します。 Code First Migrations は、最新の移行を適用し、`Seed` メソッドを実行してから、ページが正常に実行されます。 シードされたデータを含む新しい勤務時間列が表示されます。

[![Instructors_page_with_OfficeHours_Test](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image3.png)

## <a name="deploying-the-database-update-to-the-production-environment"></a>運用環境へのデータベースの更新の配置

運用環境の発行プロファイルも変更する必要があります。 この場合は、既存のプロファイルを削除し、更新した .publishsettings ファイルをインポートして新しいプロファイルを作成します。 更新されたファイルには、Cytanium の SQL Server データベースの接続文字列が含まれます。

テスト環境に配置したときと同じように、web.config 変換ファイルで接続文字列*を変換する*必要はなくなりました。 そのファイルを開き、`connectionStrings` 要素を削除します。 残りの変換は、`appSettings` 要素の `Environment` 値と、Elmah エラーレポートへのアクセスを制限する `location` 要素のためのものです。

運用環境用の新しい発行プロファイルを作成する前に、前に「[運用環境へのデプロイ](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)」チュートリアルで行ったのと同じ方法で、更新された .publishsettings ファイルをダウンロードします。 (Cytanium コントロールパネルで、 **[Web サイト]** をクリックし、 **[contosouniversity.com]** web サイトをクリックします。 **[Web 発行]** タブを選択し、 **[この Web サイトの発行プロファイルのダウンロード]** をクリックします。)これを行う理由は、.publishsettings ファイル内のデータベース接続文字列を取得するためです。 この接続文字列は、まだ SQL Server Compact を使用していて、まだ Cytanium に SQL Server データベースを作成していなかったため、初めてファイルをダウンロードしたときには利用できませんでした。

発行プロファイルを更新して、運用環境に発行できるようになりました。

Web の**発行**ウィザードを開き、 **[プロファイル]** タブに切り替えます。

**[プロファイルの管理]** をクリックし、運用プロファイルを削除します。

この変更を保存するには、 **Web の発行**ウィザードを閉じます。

Web の**発行**ウィザードをもう一度開き、 **[インポート]** をクリックします。

一時的な URL を使用している場合は、 **[接続]** タブで、 **[送信先 URL]** を適切な値に変更します。

[次へ] をクリックします。

**[設定]** タブで、 **[新しいデータベース発行の機能強化を有効にする]** をクリックします。

**Schoolcontext.cs**の [接続文字列] ボックスの一覧で、Cytanium 接続文字列を選択します。

![Selecting_Cytanium_connection_string](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image5.png)

**[実行 Code First の移行 (アプリケーションの起動時に実行)]** を選択します。

**Defaultconnection**の [接続文字列] ボックスの一覧で、Cytanium 接続文字列を選択します。

**[プロファイル]** タブを選択し、プロファイルの **[管理]** をクリックして、プロファイルの名前を "contosouniversity.com-Web 配置" から "Production" に変更します。

発行プロファイルを閉じて変更を保存し、再度開いてください。

**[発行]** をクリックします。 (実際の運用 web サイトの場合は、 *app\_をオフライン*にしてから運用環境にコピーし、発行前にプロジェクトフォルダーに置き、デプロイが完了したら削除します)。

Visual Studio によってコードの変更がテスト環境に配置され、ブラウザーが開き、Contoso 大学のホームページが表示されます。

[インストラクター] ページを選択します。

Code First Migrations は、テスト環境での場合と同じ方法でデータベースを更新します。 シードされたデータを含む新しい勤務時間列が表示されます。

![Instructors_page_with_OfficeHours_Prod](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image6.png)

これで、SQL Server データベースを使用して、データベースの変更を含むアプリケーションの更新が正常に展開されました。

## <a name="more-information"></a>その他の情報

これで、ASP.NET web アプリケーションをサードパーティのホスティングプロバイダーにデプロイするための一連のチュートリアルが完了します。 これらのチュートリアルで説明されているトピックの詳細については、MSDN web サイトの「 [ASP.NET Deployment コンテンツマップ](https://msdn.microsoft.com/library/bb386521(v=vs.110).aspx)」を参照してください。

## <a name="acknowledgements"></a>謝辞

このチュートリアルシリーズの内容に多大な貢献をした次の人々に感謝したいと思います。

- [Alberto Poblacion, MVP &amp; MCT, スペイン](https://mvp.support.microsoft.com/profile/Alberto)
- Jarod Ferguson、Data Platform Development MVP、米国
- 過酷 Mittal、Microsoft
- [Kristina Olson、Microsoft](https://blogs.iis.net/krolson/default.aspx)
- [Mike Pope、Microsoft](http://www.mikepope.com/blog/DisplayBlog.aspx)
- Mohit Srivastava、Microsoft
- [Raffaele Rialdi、イタリア](http://www.iamraf.net/)
- [Rick Anderson、Microsoft](https://blogs.msdn.com/b/rickandy/)
- [作成者 Hashimi、Microsoft](http://sedodream.com/default.aspx)(twitter: [@sayedihashimi](http://twitter.com/sayedihashimi))
- [Scott マン Selman](http://www.hanselman.com/blog/) (twitter: [@shanselman](http://twitter.com/shanselman))
- [Scott Hunter、Microsoft](https://blogs.msdn.com/b/scothu/) (twitter: [@coolcsh](http://twitter.com/coolcsh))
- [Srđan Božović、セルビア](http://msforge.net/blogs/zmajcek/)
- [Vishal Joshi、Microsoft](http://vishaljoshi.blogspot.com/) (twitter: [@vishalrjoshi](http://twitter.com/vishalrjoshi))

> [!div class="step-by-step"]
> [前へ](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12.md)
> [次へ](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)
