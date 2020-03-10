---
uid: whitepapers/aspnet-data-access-content-map
title: ASP.NET Data Access-推奨リソース |Microsoft Docs
author: rick-anderson
description: このトピックでは、ASP.NET web アプリケーション内のデータにアクセスする方法に関するドキュメントリソースへのリンクを示します。主に、Entity Framework と SQL Se...
ms.author: riande
ms.date: 07/25/2013
ms.assetid: f8157be1-4ab9-469e-ad3a-0ccc80b56c00
msc.legacyurl: /whitepapers/aspnet-data-access-content-map
msc.type: content
ms.openlocfilehash: 357851f195bf233c7c34a32bd156e4408d3e1b24
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78513970"
---
# <a name="aspnet-data-access---recommended-resources"></a>ASP.NET データ アクセス - 推奨リソース

> このトピックでは、主に Entity Framework と SQL Server を使用して、ASP.NET web アプリケーションのデータにアクセスする方法に関するドキュメントリソースへのリンクを示します。
> 
> 優れたブログ投稿、 [stackoverflow](http://stackoverflow.com)のスレッド、または役に立つその他のリンクがわかっている場合は、リンクを含む[電子メールをお送り](mailto:aspnetue@microsoft.com?subject=Data Access Content Map)ください。
> 
> 最終更新日4/3/2014

このトピックは、次のセクションで構成されています。

- [ASP.NET でのデータアクセスを使用したはじめに](#gettingstarted)
- [Entity Framework の使用](#ef)

    - [Entity Framework Code First の使用](#cf)
    - [Entity Framework Code First Migrations の使用](#efcfmigrations)
    - [Entity Framework Database First または Model First の使用 (EF デザイナー)](#efdbf)
    - [Entity Framework での関連データの読み込み (遅延読み込み、一括読み込み、および明示的な読み込み)](#efrelateddata)
    - [パフォーマンスの最適化 Entity Framework](#optimizingef)
    - [Entity Framework アプリケーションでの同時実行の処理](#efconcurrency)
    - [Entity Framework に関する書籍](#efbooks)
    - [その他の Entity Framework リソース](#otherefresources)
- [ASP.NET Web フォームアプリケーションでのデータバインディング](#wfdatabinding)

    - [Web フォームモデルバインディングの使用](#wfmodelbinding)
    - [Web フォームデータソースコントロールの使用](#wfdsc)
    - [Web フォームのデータバインドコントロールとデータバインディング式の使用](#wfdbc)
- [SQL Server データベースの操作](#sqlserver)

    - [SQL Server Express LocalDB データベースの操作](#sslocaldb)
    - [SQL Server Express データベースの操作](#sse)
    - [Windows Azure SQL Database の操作](#ssdb)
    - [SQL Server と Windows Azure SQL Database の選択](#ssdbchoosing)
- [NoSQL データベース管理システムの使用](#nosql)
- [ASP.NET アプリケーションでの LINQ クエリの使用](#linq)
- [動的データスキャフォールディングの使用](#dd)
- [データアクセスのセキュリティ保護](#securing)
- [データアクセスパフォーマンスの最適化](#optimizingdataaccess)
- [データベースの配置](#deploying)
- [Web サービスを使用したデータへのアクセス](#webservice)
- [その他のリソース](#additional)

<a id="gettingstarted"></a>

## <a name="getting-started-with-data-access-in-aspnet"></a>ASP.NET でのデータアクセスを使用したはじめに

- [データストレージのオプション (Windows Azure を使用した実際のクラウドアプリの構築)](../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-storage-options.md)。 クラウド向けの開発に関する電子書籍の章。 では、リレーショナルデータベースに慣れている多くの開発者が見落とさないように、NoSQL データベースが導入されています。 リレーショナルまたは NoSQL を選択する場合や、特定のプラットフォームを選択する場合の考慮事項に関するガイドラインを示します。
- [ASP.NET Data Access Options](https://msdn.microsoft.com/library/ms178359.aspx) (MSDN)。 ASP.NET のリレーショナルデータベースのデータアクセスオプションの概要と、シナリオに適したプラットフォームとアクセス方法の選択方法に関するガイダンス。
- [リレーショナルデータベース](http://en.wikipedia.org/wiki/Relational_database)。 Wikipedia)。 リレーショナルデータベースを使用していない場合、リレーショナルデータベースの用語と概念の概要については、このページを参照してください。 SQL Server の概要については、このトピックで後述する「 [SQL Server データベースの操作](#sqlserver)」を参照してください。

<a id="ef"></a>

## <a name="using-the-entity-framework"></a>Entity Framework の使用

- [Entity Framework の開発方法](https://msdn.microsoft.com/library/ms178359.aspx#dbfmfcf)(MSDN)。 Entity Framework 開発アプローチ Database First、Model First、または Code First を選択する方法についてのガイダンスです。

<a id="cf"></a>

### <a name="using-entity-framework-code-first"></a>Entity Framework Code First の使用

次のチュートリアルでは、ダウンロード可能なサンプルアプリケーションを提供しています。

- [MVC 5 を使用した EF 6 でのはじめに](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。 移行や EF 6 の機能 (接続の回復性、コマンドのインターセプト、非同期など) を含むさまざまな Entity Framework Code First シナリオについて説明します。 これは、 [EF 5/MVC 4 シリーズ](../mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)の更新されたバージョンです。 以前のシリーズでは、リポジトリのチュートリアルと、新しいシリーズに含まれていない作業単位パターンについて説明しています。
- [ASP.NET MVC 5 の概要](../mvc/overview/getting-started/introduction/getting-started.md)。 より狭い範囲の Entity Framework Code First シナリオについて説明しますが、MVC 機能の概要については、より包括的な作業を行うことができます。
- [モデルバインドと Web フォーム](https://go.microsoft.com/fwlink/?LinkId=286117)。 は、Web フォームアプリケーションで Code First を使用します。
- [ASP.NET 4.5 Web フォームでのはじめに](../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview.md)。 Code First の一部をカバーする Web フォームの概要です。 モデルバインドを使用します。
- [MVC ミュージックストア](../mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-1.md)。 は、メンバーシップと承認も実装する e コマース MVC 3 アプリケーションで Code First を使用します。 ここで使用されている MVC バージョンと ASP.NET メンバーシップ (認証および承認) システムは古くなっています。ASP.NET メンバーシップの最新情報については、「 [https://asp.net/identity](https://asp.net/identity)」を参照してください。

その他のリソース:

- [Entity Framework-既存のデータベースに Code First](https://msdn.microsoft.com/data/jj200620)します。 旧. 既存のデータベースで Code First を使用する方法を示すビデオとチュートリアルです。
- [データデベロッパーセンター-Entity Framework](https://msdn.microsoft.com/data/ef)。 旧. Entity Framework チームによって作成および管理されている Entity Framework ドキュメントのガイドについては、「[作業の開始](https://msdn.microsoft.com/data/ee712907)」リンクを参照してください。

このトピックで後述する「Entity Framework と[その他の Entity Framework リソース](#otherefresources)[に関する書籍](#efbooks)」も参照してください。

<a id="efcfmigrations"></a>

### <a name="using-entity-framework-code-first-migrations"></a>Entity Framework Code First Migrations の使用

上記の Code First チュートリアルの大部分は移行に関するものです。 次のリソースも参照してください。

- [Visual Studio を使用した ASP.NET Web デプロイ](../web-forms/overview/deployment/visual-studio-web-deployment/introduction.md)。 2部構成のチュートリアルシリーズでは、Code First Migrations を使用してデータベースを配置する方法を説明します。
- [メンバーシップ、OAuth、SQL Database を持つ Secure ASP.NET MVC 5 アプリを Windows Azure の Web サイトにデプロイ](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)します。 Microsoft Azure)。 移行を使用してメンバーシップとアプリケーションデータを Azure にデプロイする方法。
- [Visual Studio と ASP.NET の Web デプロイの概要](https://msdn.microsoft.com/library/dd394698.aspx#dbdeployment)。 Code First Migrations が Visual Studio の web 配置機能にどのように統合されるかについては、「 **Visual studio でのデータベース配置の構成**」セクションを参照してください。
- [Data Developer Center-Code First Migrations](https://msdn.microsoft.com/data/jj591621) (MSDN)。 Entity Framework チームの移行に関するドキュメント。
- [スクリーンキャストシリーズの移行](https://blogs.msdn.com/b/adonet/archive/2014/03/12/migrations-screencast-series.aspx)。 EF ブログ)。 Code First Migrations の高度なトピックに関する3つのビデオ。
- [ASP.NET Web ページサイトで Code First Migrations](http://www.mikesdotnetting.com/Article/217/Code-First-Migrations-With-ASP.NET-Web-Pages-Sites)します。 Mikesdotnetting ブログ)。 Visual Studio クラスライブラリプロジェクトにデータコンテキストを配置することで、ASP.NET Web ページサイトで Code First 移行を使用する方法について説明します。

<a id="efdbf"></a>

### <a name="using-entity-framework-database-first-or-model-first-the-ef-designer"></a>Entity Framework Database First または Model First の使用 (EF デザイナー)

- [MVC 5 を使用した Entity Framework 6 Database First のはじめに](../mvc/overview/getting-started/database-first-development/setting-up-database.md)。 サーバーエクスプローラーでスクリプトを実行してデータベースを作成し、Entity Framework デザイナーを使用してデータモデルを作成します。 単純な CRUD web ページを作成する方法について説明します。また、他のデータ処理機能については、すべての EF ワークフローで同じ DbContext API が使用されるため、Code First のチュートリアルのいずれかに従うことができます。

次のリソースは古いものです。 Entity Framework のバージョン4.0 を使用する場合に、Web フォームアプリケーションでデータバインディングにデータソースコントロールを使用する場合に便利です。

- [Entity Framework 4.0 ではじめに](../web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md)します。 **EntityDataSource**コントロールの使用方法について説明します。
- [Entity Framework を続行](../web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started.md)する ( **ObjectDataSource**コントロールの使用方法を示します)。 同時実行処理のチュートリアル、EF のパフォーマンスに関するチュートリアル、EF 4.0 の新機能に関するチュートリアルが含まれています。

<a id="efrelateddata"></a>

### <a name="handling-related-data-in-entity-framework-lazy-loading-eager-loading-and-explicit-loading"></a>Entity Framework での関連データの処理 (遅延読み込み、一括読み込み、および明示的な読み込み)

- [ASP.NET MVC アプリケーションでの Entity Framework を使用した関連データの読み取り](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)。 Code First、MVC サンプルアプリケーション。 表示されるメソッドは、Web フォームモデルのバインドおよび Database First ワークフローにも適用されます。
- [Data デベロッパーセンター-関連エンティティ](https://msdn.microsoft.com/data/jj574232)(MSDN) を読み込んでいます。 関連データの読み込みに関する Entity Framework チームのドキュメント。

<a id="optimizingef"></a>

### <a name="optimizing-entity-framework-performance"></a>パフォーマンスの最適化 Entity Framework

- [ASP.NET アプリケーションの高度な Entity Framework シナリオ](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application.md)。 独自の SQL ステートメントを実行する方法、独自のストアドプロシージャを呼び出す方法、変更の検出を無効にする方法、および変更を保存するときに検証を無効にする方法について説明します。
- [Entity Framework 5 (MSDN) のパフォーマンスに関する考慮事項](https://msdn.microsoft.com/data/hh949853)。
- [パフォーマンスに関する考慮事項 (Entity Framework)](https://msdn.microsoft.com/library/cc853327) (MSDN)。
- [ASP.NET Web アプリケーションでの Entity Framework を使用したパフォーマンスの最大化](../web-forms/overview/older-versions-getting-started/continuing-with-ef/maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application.md)。 Entity Framework 4.0 に適用されます。
- このトピックの「 [ASP.NET データアクセスの最適化](#optimizingdataaccess)」も参照してください。

<a id="efconcurrency"></a>

### <a name="handling-concurrency-in-an-entity-framework-application"></a>Entity Framework アプリケーションでの同時実行の処理

- [ASP.NET MVC アプリケーションでの Entity Framework による同時実行の処理](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)。 Code First、DbContext API、MVC サンプルアプリケーションを使用します。
- [データデベロッパーセンター–オプティミスティック同時実行制御パターン](https://msdn.microsoft.com/data/jj592904)(MSDN)。 Entity Framework チームの同時実行のドキュメント。
- [ASP.NET Web アプリケーションの Entity Framework での同時実行の処理](../web-forms/overview/older-versions-getting-started/continuing-with-ef/handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application.md)。 Entity Framework 4.0 に適用されます。 Database First、ObjectContext API、Web フォームサンプルアプリケーションを使用します。

<a id="efrepository"></a><a id="efbooks"></a>

### <a name="books-about-the-entity-framework"></a>Entity Framework に関する書籍

- [Entity Framework のプログラミング:](http://shop.oreilly.com/product/0636920022237.do)ジュリー Lerman と Rowan 明美による dbcontext。
- [プログラミング Entity Framework:](http://shop.oreilly.com/product/0636920022220.do)ジュリー Lerman と Rowan 明美によって Code First ます。

これらの書籍はいずれも、現在推奨されている手法を使用して最新の状態になっています。 これらは、インターネット上で使用可能なものと比べて、より包括的でわかりやすい Entity Framework の概要を提供します。 ジュリー Lerman による[プログラミング Entity Framework](http://shop.oreilly.com/product/9780596807252.do)という別の書籍は、より大規模で包括的ですが、より古いものですが、この Entity Framework を使用するための推奨される方法はありません。 Entity Framework チームによって推奨されている書籍の一覧については、MSDN サイトの「 [Data Developer Center (データデベロッパーセンター)](https://msdn.microsoft.com/data/aa937716) 」を参照してください。

<a id="otherefresources"></a>

### <a name="other-entity-framework-resources"></a>その他の Entity Framework リソース

- [Entity Framework (ADO.NET) チームブログ](https://blogs.msdn.com/b/adonet/)。 最新の情報と新しい拡張機能の発表に最適なリソースの1つ。 その他の EF 関連のブログについては、 [Entity Framework の使用開始](https://msdn.microsoft.com/data/ee712907)に関するブログロールを参照してください。
- [MSDN マガジン](https://msdn.microsoft.com/magazine/default.aspx)。 「**データポイント**」列を参照してください。これは、多くの場合 Entity Framework に関連するトピックです。

<a id="wfdatabinding"></a>

## <a name="data-binding-in-aspnet-web-forms-applications"></a>ASP.NET Web フォームアプリケーションでのデータバインディング

- [ASP.NET Web フォームデータアクセスオプション](https://msdn.microsoft.com/library/jj822927.aspx)(MSDN)<a id="wfmodelbinding"></a>。

<a id="wfmodelbinding"></a>

### <a name="using-web-forms-model-binding"></a>Web フォームモデルバインディングの使用

- [モデルバインドと Web フォーム](https://go.microsoft.com/fwlink/?LinkId=286117)。 EF Code First を使用したチュートリアルシリーズ。
- [Web フォームモデルのバインディング第1部: データの選択](https://weblogs.asp.net/scottgu/archive/2011/09/06/web-forms-model-binding-part-1-selecting-data-asp-net-vnext-series.aspx)(Scott Guthrie のブログ)。 これらの以前のブログ投稿では、現在 ItemType という名前のプロパティは ModelType という名前でしたが、それ以外の場合に含まれる情報は有効です。
- [Web フォームモデルのバインディング第2部: データのフィルター処理](https://weblogs.asp.net/scottgu/archive/2011/09/12/web-forms-model-binding-part-2-filtering-data-asp-net-vnext-series.aspx)(Scott Guthrie のブログ)。
- [Web フォームモデルのバインディング第3部: 更新と検証](https://weblogs.asp.net/scottgu/archive/2011/10/30/web-forms-model-binding-part-3-updating-and-validation-asp-net-4-5-series.aspx)(Scott Guthrie のブログ)。
- [ASP.NET 4.5 Web フォームモデルのバインド](../web-forms/videos/aspnet-web-forms-vnext/aspnet-45-web-forms-model-binding.md)。 (ビデオ)。
- [モデルのバインディング第1部: データの選択](../web-forms/videos/aspnet-web-forms-vnext/aspnet-vnext-videos-model-binding-part-1-selecting-data.md)(ビデオ)
- [モデルバインディングパート 2-フィルター処理](../web-forms/videos/aspnet-web-forms-vnext/aspnet-vnext-videos-model-binding-part-2-filtering.md)(ビデオ)。
- [ASP.NET 4.5 Web フォームでのはじめに: データ項目と詳細を表示](../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details.md)します。

<a id="wfdsc"></a>

### <a name="using-web-forms-data-source-controls"></a>Web フォームデータソースコントロールの使用

- [データソース Web サーバーコントロール](https://msdn.microsoft.com/library/ms247258.aspx)(MSDN)。
- [Entity Framework 6 の動的データプロバイダーと EntityDataSource コントロールのリリースを発表](https://blogs.msdn.com/b/webdev/archive/2014/02/28/announcing-the-release-of-dynamic-data-provider-and-entitydatasource-control-for-entity-framework-6.aspx)します (Microsoft Web 開発ブログ)。

<a id="wfdbc"></a>

### <a name="using-web-forms-data-bound-controls-and-data-binding-expressions"></a>Web フォームのデータバインドコントロールとデータバインディング式の使用

- [モデルバインドと Web フォーム](https://go.microsoft.com/fwlink/?LinkId=286117)。 EF Code First を使用するチュートリアルシリーズ。
- [ASP.NET 4.5 Web フォームでのはじめに: データ項目と詳細を表示](../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details.md)します。
- [厳密に型指定](https://weblogs.asp.net/scottgu/archive/2011/09/02/strongly-typed-data-controls-asp-net-vnext-series.aspx)されたデータコントロール (Scott Guthrie のブログ)。
- [厳密に型指定](../web-forms/videos/aspnet-web-forms-vnext/aspnet-vnext-videos-strongly-typed-data-controls.md)されたデータコントロール (ビデオ)。
- [ASP.NET 4.5 Web フォームは、厳密に型指定](../web-forms/videos/aspnet-web-forms-vnext/aspnet-vnext-videos-strongly-typed-data-controls.md)されたデータコントロール (ビデオ) を形成します。
- [データバインドされた Web サーバーコントロール](https://msdn.microsoft.com/library/ms228214.aspx)(MSDN)。
- [データバインディング式の概要](https://msdn.microsoft.com/library/ms178366.aspx)(MSDN)。 このページでは、 **Eval**と**Bind**のみについて説明します。**Item**と**BindItem**が含まれるように更新されていません。

<a id="sqlserver"></a>

## <a name="working-with-sql-server-databases"></a>SQL Server データベースの操作

- [SQL Server データベース機能](https://msdn.microsoft.com/library/hh230827.aspx)(MSDN)。 さまざまな SQL Server トピックの概要については、目次の次のエントリを参照してください。
- [SQL Server エディション](https://msdn.microsoft.com/library/ms178359.aspx#sqlserver)(MSDN)。 使用可能な SQL Server エディションの概要と、それぞれに関する詳細情報へのリンクが記載されています)。
- [ASP.NET Web アプリケーション (MSDN) の接続文字列を SQL Server](https://msdn.microsoft.com/library/jj653752.aspx)します。
- [ASP.NET Web アプリケーション (MSDN) に SQL Server Compact を使用](https://msdn.microsoft.com/library/ms247257.aspx)します。
- [Microsoft SQL Server: データベース製品のサンプル](https://github.com/Microsoft/sql-server-samples/blob/master/samples/databases/adventure-works/README.md)。 サンプル AdventureWorks データベース。
- [サンプルデータベースをインストール](https://github.com/Microsoft/sql-server-samples/blob/master/samples/databases/adventure-works/README.md)しています。 ここに示すメソッドに加えて、サンプルの .mdf ファイルの1つを web プロジェクトの App\_Data フォルダーにダウンロードし、データベースを LocalDB に変換し、LocalDB 接続文字列を作成することもできます。 その方法については、「[方法: LocalDB にアップグレード](https://msdn.microsoft.com/library/hh873188.aspx)する」を参照してください。

SQL Server Express と LocalDB を操作する方法、および SQL Server と SQL Database を選択する方法については、次のセクションも参照してください。

<a id="sslocaldb"></a>

### <a name="working-with-sql-server-express-localdb-databases"></a>SQL Server Express LocalDB データベースの操作

- [SQL Server Express 2012 LocalDB](https://msdn.microsoft.com/library/hh510202(v=sql.110).aspx) (MSDN)。 LocalDB に関する公式の MSDN の概要です。
- [ASP.NET Web アプリケーション (MSDN) の接続文字列を SQL Server](https://msdn.microsoft.com/library/jj653752.aspx)します。
- [方法: LocalDB にアップグレード](https://msdn.microsoft.com/library/hh873188.aspx)する (MSDN) 以前のバージョンの SQL Server Express の .mdf ファイルを LocalDB に移行する方法について説明します。 また、 [SQL Server 2012 サンプルデータベース](https://go.microsoft.com/fwlink/?linkid=117483)のいずれかをダウンロードする場合にも、このプロセスを実行する必要があります。
- [LocalDB の導入。 SQL Express の機能強化](https://go.microsoft.com/fwlink/?LinkId=234375)(SQL Server Express ブログ)。 では、MSDN に含まれるよりも LocalDB が作成された理由について、より多くの背景があります。
- [LocalDB: データベースはどこにありますか?](https://go.microsoft.com/fwlink/?LinkId=234376) (SQL Server Express ブログ)。 LocalDB データベースファイルが作成される場所に関する情報。
- [LocalDB を完全な IIS と共に使用する、パート 1: ユーザープロファイル](https://blogs.msdn.com/b/sqlexpress/archive/2011/12/09/using-localdb-with-full-iis-part-1-user-profile.aspx)(SQL Server Express ブログ)。 LocalDB は、IIS で動作するように設計されていません。 この一連のブログ記事では、問題といくつかの回避策について説明します。

<a id="sse"></a>

### <a name="working-with-sql-server-express-databases"></a>SQL Server Express データベースの操作

- [ASP.NET Web アプリケーション (MSDN) の接続文字列を SQL Server](https://msdn.microsoft.com/library/jj653752.aspx)します。 SQL Server Express で AttachDBFileName 接続文字列の設定を使用する場合は、このページの「ユーザーインスタンス」セクションを参照してください。
- [ローカル SQL Server Express 2008 (SQL Server Express ブログ) の所有権を取得する方法](https://blogs.msdn.com/b/sqlexpress/archive/2010/02/23/how-to-take-ownership-of-your-local-sql-server-2008-express.aspx)。 SQL Server Express インスタンスの管理者ではないため、一般的な問題は SQL Server Express データベースを使用できません。 既定では、SQL Server Express をインストールしたユーザーのみが管理者になります。 このブログでは、コンピューターの管理者である場合に SQL Server Express 管理者を作成する方法について説明します。
- [ASP.NET web アプリケーションは、運用環境で SQL Server Express データベースを使用できますか。](https://msdn.microsoft.com/library/jj653753.aspx#sql_express_in_production) (MSDN)。

<a id="ssdb"></a>

### <a name="working-with-windows-azure-sql-database"></a>Windows Azure SQL Database の操作

- [メンバーシップ、OAuth、SQL Database を持つ Secure ASP.NET MVC アプリを Windows Azure の Web サイト](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)(Microsoft Azure サイト) にデプロイします。
- [SQL データベース](https://docs.microsoft.com/azure/sql-database/)(Microsoft Azure サイト)。 入門チュートリアルとハウツーガイドをご覧ください。
- [Windows Azure SQL Database](https://msdn.microsoft.com/library/windowsazure/ee336279.aspx) (MSDN)。 MSDN の SQL Database 目次の最上位ノードです。
- [Windows Azure SQL Database Technet Wiki の記事の索引](https://social.technet.microsoft.com/wiki/contents/articles/2267.windows-azure-sql-database-technet-wiki-articles-index-en-us.aspx)(Microsoft technet サイト)。
- [一時的エラー処理アプリケーションブロック](https://msdn.microsoft.com/library/hh680934(v=PandP.50).aspx)。 スロットルによって発生する一時的なネットワークエラーと接続エラーを処理できるようにするフレームワーク。 NuGet パッケージで利用可能: [Enterprise Library 5.0-一時的なエラー処理アプリケーションブロック](http://nuget.org/packages/EnterpriseLibrary.WindowsAzure.TransientFaultHandling)。
- [はじめに SQL Database と Entity Framework](https://msdn.microsoft.com/data/jj556244) (MSDN) を使用します。
- [Windows Azure トレーニングキット](https://www.microsoft.com/download/details.aspx?id=8396)(Microsoft ダウンロードセンター)。 SQL Database のハンズオンラボが含まれています。
- [Windows Azure SQL Database コミュニティフォーラム](https://social.msdn.microsoft.com/Forums/ssdsgetstarted/threads)。
- [Windows Azure SQL Database](https://msdn.microsoft.com/library/ff803375.aspx) (MSDN) に移行しています。 Microsoft のパターンとプラクティスチームによる包括的なエンドツーエンドシナリオの1つの章。 移行が必要な理由と、SQL Server から SQL Database への移行方法について説明します。
- [Windows Azure SQL Database (MSDN) への SQL Server データベースの移行](https://msdn.microsoft.com/library/windowsazure/jj156160.aspx)。
- [SQL Database 移行ウィザード](http://sqlazuremw.codeplex.com/)。 SQL Database との間でデータベースを移行するためのオープンソースツール。

<a id="ssdbchoosing"></a>

### <a name="choosing-between-sql-server-and-windows-azure-sql-database"></a>SQL Server と Windows Azure SQL Database の選択

- [SQL Server と Windows Azure SQL Database](https://social.technet.microsoft.com/wiki/contents/articles/996.compare-sql-server-with-windows-azure-sql-database-en-us.aspx) (Microsoft TechNet サイト) を比較します。
- [Windows Azure SQL Database へのデータ移行: ツールと手法](https://msdn.microsoft.com/library/windowsazure/hh694043.aspx)(MSDN)。 SQL Server と SQL Database を比較し、SQL Server から SQL Database に移行するタイミングに関するガイダンスを提供するセクションが含まれています。
- [Windows Azure SQL Database 配信ガイド](https://social.technet.microsoft.com/wiki/contents/articles/3398.windows-azure-sql-database-delivery-guide-en-us.aspx)(Microsoft TechNet サイト)。
- [SQL Server 機能の制限事項 (Windows Azure SQL Database)](https://msdn.microsoft.com/library/windowsazure/ff394115.aspx) (MSDN)。
- [Windows Azure Table Storage と windows Azure SQL Database 比較](https://msdn.microsoft.com/library/jj553018.aspx)(MSDN)。 Windows Azure に展開するアプリケーションの場合、windows Azure テーブルストレージが Windows Azure SQL Database の代替手段となることがあります。 このトピックは、これらの代替手段を決定するのに役立ちます。
- [Windows Azure SQL Database](https://msdn.microsoft.com/library/windowsazure/ee336279) (MSDN)。
- [ガイドラインと制限事項 (Windows Azure SQL Database)](https://msdn.microsoft.com/library/windowsazure/ff394102.aspx)

<a id="nosql"></a>

## <a name="working-with-nosql-database-management-systems"></a>NoSQL データベース管理システムの使用

- [Windows Azure Data Services](https://www.windowsazure.com/develop/net/data/) (Microsoft Azure サイト)。 [テーブルサービスの機能ガイド](https://docs.microsoft.com/azure/)とページの**ビッグデータ**に関するセクションを参照してください。
- [ストレージテーブル、キュー、および blob (Microsoft Azure サイト) を使用する多層アプリケーションを ASP.NET](https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36)します。 Windows Azure storage NoSQL テーブルを使用するダウンロード可能なサンプルアプリケーションを含むエンドツーエンドのチュートリアルです。

<a id="linq"></a>

## <a name="using-linq-queries-in-aspnet-applications"></a>ASP.NET アプリケーションでの LINQ クエリの使用

- [ASP.NET Data Access Options](https://msdn.microsoft.com/library/ms178359.aspx#linq) (MSDN)。 LINQ の概要について説明します。
- [LINQ トレーニングビデオ](http://www.misfitgeek.com/windows-client-linq-training-videos-20/)(Joe Stagner のブログ)。
- [ダイナミック LINQ リソースへのリンクを含む ASP.NET フォーラムスレッド](https://forums.asp.net/p/1961037/5601994.aspx?Please+suggest+good+books+so+that+one+can+write+and+understand+dynamic+linq)。

<a id="dd"></a>

## <a name="using-dynamic-data-scaffolding"></a>動的データスキャフォールディングの使用

- [動的データプロジェクトテンプレート](https://msdn.microsoft.com/library/jj822927.aspx#dynamicdata)(MSDN)。 動的データプロジェクトをいつ使用するかについてのガイダンスです。
- [ASP.NET 動的データ](https://msdn.microsoft.com/library/ee845452.aspx)(MSDN)。

<a id="securing"></a>

## <a name="securing-data-access"></a>データアクセスのセキュリティ保護

- [ASP.NET でのデータアクセスのセキュリティ保護](https://msdn.microsoft.com/library/ms178375.aspx)(MSDN)。
- [セキュリティに関する考慮事項 (Entity Framework)](https://msdn.microsoft.com/library/cc716760.aspx) (MSDN)。
- [方法: データソースコントロールを使用するときに接続文字列をセキュリティで保護](https://msdn.microsoft.com/library/ms178372.aspx)する (MSDN)。

<a id="optimizingdataaccess"></a>

## <a name="optimizing-data-access-performance"></a>データアクセスパフォーマンスの最適化

- [ASP.NET パフォーマンスの概要](https://msdn.microsoft.com/library/cc668225.aspx)(MSDN)。
- [ASP.NET キャッシュ](https://msdn.microsoft.com/library/xsbfdd8c.aspx)(MSDN)。
- [ASP.NET パフォーマンスの向上](https://msdn.microsoft.com/library/ff647787)(MSDN)。 このページの上部には "提供終了のコンテンツ" の警告がありますが、ほとんどの情報は引き続き関連しており、同等の更新されたリソースはありません。
- [SQL Server パフォーマンスの向上](https://msdn.microsoft.com/library/ff647793)(MSDN)。 前のリンクと同じコメント。

このトピックの「 [Entity Framework のパフォーマンスの最適化](#optimizingef)」も参照してください。

<a id="deploying"></a>

## <a name="deploying-a-database"></a>データベースの配置

- [ASP.NET Web デプロイ-推奨リソース](aspnet-web-deployment-content-map.md)(MSDN)。

<a id="webservice"></a>

## <a name="accessing-data-through-a-web-service"></a>Web サービスを使用したデータへのアクセス

- [Web サービス (MSDN) を使用したデータへのアクセス](https://msdn.microsoft.com/library/ms178359.aspx#webservice)。 Web API と WCF を使用する場合のガイダンス。
- [ASP.NET Web API ではじめに](../web-api/index.md)します。
- [WCF Data Services](https://msdn.microsoft.com/data/bb931106) (MSDN)。

<a id="additional"></a>

## <a name="additional-resources"></a>その他のリソース

- [ASP.NET データアクセス](https://msdn.microsoft.com/library/jj653753.aspx)に関する FAQ (MSDN)。
- [ASP.NET Web フォームチュートリアル-データ](../web-forms/overview/data-access/index.md)。 これらのチュートリアルのほとんどは、比較的古いものです。まず、 [ASP.NET データアクセスオプション](https://msdn.microsoft.com/library/ms178359.aspx)と[データストレージオプション (Windows Azure を使用した実際のクラウドアプリの構築)](../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-storage-options.md)を読んで、お客様のシナリオに適していないデータアクセス方法があまり大きくならないようにしてください。
- [ASP.NET MVC コンテンツマップ](../mvc/overview/getting-started/recommended-resources-for-mvc.md)。
- [ASP.NET Web ページチュートリアル-データ](../web-pages/overview/data/index.md)。
- [Visual Studio でのデータへのアクセス](https://msdn.microsoft.com/library/wzabh8c4.aspx)(MSDN)。 このコンテンツマップに似たリンクの一覧が表示されますが、ASP.NET ではなく Visual Studio に焦点を当てています。
