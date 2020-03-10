---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/create-the-project
title: プロジェクトを作成する |Microsoft Docs
author: Erikre
description: このチュートリアルシリーズでは、ASP.NET 4.5 と Microsoft Visual Studio Express 2013 を使用して ASP.NET Web フォームアプリケーションを構築するための基本について説明します。
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 2ce36f78-8ecb-4ab1-b748-6d0ab633ea3f
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/create-the-project
msc.type: authoredcontent
ms.openlocfilehash: 62918b17f42e54dfe4e45a08927b1039dcbb7012
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78461572"
---
# <a name="create-the-project"></a>プロジェクトを作成する

[Erik Reitan](https://github.com/Erikre)

[Wingtip Toys サンプルプロジェクト (C#) をダウンロード](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)するか[、電子書籍 (PDF) をダウンロード](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)します。

> このチュートリアルシリーズでは、ASP.NET 4.5 を使用して ASP.NET Web フォームアプリケーションを構築するための基礎と、Web 用の Microsoft Visual Studio Express 2013 について説明します。 このチュートリアルシリーズ[でC#は、ソースコードが含ま](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)れる Visual Studio 2013 プロジェクトを利用できます。

このチュートリアルでは、Visual Studio で既定のプロジェクトを作成、確認、実行します。これにより、ASP.NET の機能を理解することができます。 また、Visual Studio 環境を確認します。

## <a name="what-youll-learn"></a>ここでは、次の内容について学習します。

- 新しい Web フォームプロジェクトを作成する方法。
- Web フォームプロジェクトのファイル構造。
- Visual Studio でプロジェクトを実行する方法。
- 既定の Web フォームアプリケーションのさまざまな機能。
- Visual Studio 環境を使用する方法の基本について説明します。

## <a name="creating-the-project"></a>プロジェクトの作成

1. Visual Studio を開きます。
2. Visual Studio の **[ファイル]** メニューから **[新しいプロジェクト]** を選択します。 

    ![[プロジェクトの作成]-[新しいプロジェクト] メニュー項目](create-the-project/_static/image1.png)
3. 左側にある [**テンプレート** -&gt; **Visual C#**  -&gt; **Web**テンプレート] グループを選択します。
4. 中央の列で **[ASP.NET Web アプリケーション]** を選択します。  
 このチュートリアルシリーズでは .NET Framework 4.5.2 を使用しています。
5. プロジェクトに*ウィングヒント*の名前を指定し、 **[OK** ] をクリックします。 

    ![[プロジェクトの作成]-[新しいプロジェクト] ダイアログ](create-the-project/_static/image2.png)

    > [!NOTE]
    > このチュートリアルシリーズでは、プロジェクトの名前が**ウィングヒント toys**です。 チュートリアルシリーズ全体で提供されるコードが想定どおりに機能するように、この*正確*なプロジェクト名を使用することをお勧めします。

6. **[認証の変更]** ボタンをクリックします。 **個々のユーザーアカウント**を選択し、 **[OK]** ボタンをクリックします。

7. **[Web フォーム]** テンプレートを選択し、 **[OK]** をクリックします。

    ![プロジェクトの作成-新しいプロジェクトテンプレート](create-the-project/_static/image3.png)

プロジェクトの作成には少し時間がかかります。 準備ができたら、 **default.aspx**ページを開きます。

![プロジェクトの作成-新しいプロジェクトテンプレート](create-the-project/_static/image4.png)

中央のウィンドウの下部にあるオプションを選択すると、**デザイン**ビューと**ソース**ビューを切り替えることができます。 **デザイン**ビューでは、ASP.NET の Web ページ、マスターページ、コンテンツページ、HTML ページ、およびユーザーコントロールが WYSIWYG ビューで表示されます。 **ソース**ビュー Web ページの HTML マークアップを表示します。このマークアップは編集できます。

> [!TIP] 
> 
> **ASP.NET フレームワークについて**
> 
> ASP.NET Web フォームを利用すれば、馴染みのあるドラッグアンドドロップ式のイベント駆動型モデルを利用して動的な Web サイトを構築できます。 デザイン サーフェスや数百あるコントロールとコンポーネントを利用し、洗練された強力な UI 駆動型サイトとデータ アクセスを短時間で構築できます。 Wingtip 玩具ストアは ASP.NET の Web フォームに基づいていますが、このチュートリアルシリーズで学習する概念の多くは、ASP.NET すべてに適用されます。
> 
> ASP.NET は、次の4つの主要な開発フレームワークを提供します。
> 
> - [ASP.NET Web フォーム](../../../index.md)  
>  Web フォームフレームワークは、Microsoft Windows フォーム (WinForms) や WPF/XAML/Silverlight などの宣言型プログラミングおよびコントロールベースのプログラミングを好む開発者を対象としています。 WYSIWYG デザイナーによる開発モデルが用意されているため、web 開発用の迅速なアプリケーション開発 (RAD) 環境を探している開発者にも人気があります。 Web プログラミングに慣れておらず、従来の Microsoft RAD クライアント開発ツール (たとえば、Visual Basic やビジュアルC#) に精通している場合は、HTML および JavaScript を使用しなくても web アプリケーションをすばやく作成できます。
> - [ASP.NET MVC](../../../../mvc/index.md)  
>  ASP.NET MVC は、テスト駆動型開発、懸念事項の分離、制御の反転 (IoC)、依存関係の注入 (DI) などのパターンと原則に関心がある開発者を対象としています。 このフレームワークは、web アプリケーションのビジネスロジック層とプレゼンテーション層を分離することをお勧めします。
> - [ASP.NET Web ページ](../../../../web-pages/index.md)  
>  ASP.NET Web ページは、PHP の行に沿って単純な Web 開発ストーリーを必要とする開発者を対象としています。 Web ページモデルでは、HTML ページを作成し、そのページにサーバーベースのコードを追加して、マークアップの表示方法を動的に制御します。 Web ページは、特に軽量のフレームワークとして設計されており、HTML を知っていても、生徒や趣味などの幅広いプログラミングエクスペリエンスを備えていない人にとって、ASP.NET の最も簡単なエントリポイントです。 また、ASP.NET の使用を開始するために PHP または同様のフレームワークを知っている web 開発者にとっても良い方法です。
> - [ASP.NET シングルページアプリケーション](../../../../single-page-application/index.md)  
>  ASP.NET Single Page Application (SPA) を使用すると、HTML 5、CSS 3、および JavaScript を使用したクライアント側の重要な相互作用を含むアプリケーションを構築できます。 ASP.NET and Web Tools 2012.2 更新プログラムは、ノックアウトと ASP.NET Web API を使用してシングルページアプリケーションを構築するための新しいテンプレートを提供します。 新しい SPA テンプレートに加えて、コミュニティによって作成された新しい SPA テンプレートをダウンロードすることもできます。
> 
> 4つの主要な開発フレームワークに加えて、ASP.NET には、について理解しておくことが重要な追加のテクノロジも用意されていますが、このチュートリアルシリーズでは説明しません。
> 
> - [ASP.NET Web API](../../../../web-api/index.md) -ブラウザーやモバイルデバイスを含む広範なクライアントに接続する HTTP サービスを構築するためのフレームワークです。
> - [ASP.NET SignalR](../../../../signalr/index.md) -リアルタイム web 機能を簡単に開発するためのライブラリです。

### <a name="reviewing-the-project"></a>プロジェクトのレビュー

Visual Studio では、 **[ソリューションエクスプローラー]** ウィンドウで、プロジェクトのファイルを管理できます。 **ソリューションエクスプローラー**でアプリケーションに追加されたフォルダーを見てみましょう。 Web アプリケーションテンプレートでは、基本的なフォルダー構造が追加されます。

![プロジェクトを作成する-ソリューションエクスプローラー](create-the-project/_static/image5.png)

Visual Studio では、プロジェクトの初期フォルダーとファイルがいくつか作成されます。 このチュートリアルの後半で使用する最初のファイルは、次のとおりです。

| **[最近使ったファイル]** | **目的** |
| --- | --- |
| *Default.aspx* | 通常、アプリケーションをブラウザーで実行したときに最初に表示されるページです。 |
| *サイト. Master* | 一貫性のあるレイアウトを作成し、アプリケーションのページに対して標準動作を使用できるページ。 |
| *Global.asax* | ASP.NET または HTTP モジュールによって発生するアプリケーションレベルおよびセッションレベルのイベントに応答するためのコードを含む省略可能なファイルです。 |
| *Web.config* | アプリケーションの構成データ。 |

### <a name="running-the-default-web-application"></a>既定の Web アプリケーションを実行しています

既定の Web アプリケーションは、組み込みの機能とサポートに基づく豊富なエクスペリエンスを提供します。 既定の Web フォームプロジェクトを変更しないと、ローカルの Web ブラウザーでアプリケーションを実行する準備ができています。

1. Visual Studio で***F5***キーを押します。   
 アプリケーションが Web ブラウザーでビルドされ、表示されます。  

    ![プロジェクトの作成-既定のページ](create-the-project/_static/image6.png)
2. 実行中のアプリケーションの確認が完了したら、ブラウザーウィンドウを閉じます。

この既定の Web アプリケーションには、 *default.aspx (ホーム*)、 *.Aspx*、および*Contact*という3つのメインページがあります。 これらの各ページには、上部のナビゲーションバーからアクセスできます。 アカウントフォルダーには、.aspx ページと login.aspx ページという2つの追加ページもあります。 これら2つのページでは、ASP.NET のメンバーシップ機能を使用して、ユーザーの資格情報を作成、格納、および検証できます。

## <a name="aspnet-web-forms-background"></a>ASP.NET Web フォームの背景

ASP.NET Web フォームは Microsoft ASP.NET テクノロジに基づくページであり、サーバー上で実行されるコードがブラウザーまたはクライアントデバイスに Web ページの出力を動的に生成します。 ASP.NET Web フォームページでは、スタイルやレイアウトなどの機能に適したブラウザーに準拠した HTML が自動的にレンダリングされます。 Web フォームは、Microsoft Visual Basic や Microsoft Visual C#など、.net 共通言語ランタイムでサポートされている任意の言語と互換性があります。 また、Web フォームは[Microsoft .NET Framework](https://msdn.microsoft.com/vstudio/aa496123)上に構築されています。これにより、管理された環境、タイプセーフ、継承などの利点が得られます。

ASP.NET Web フォームページが実行されると、ページは一連の処理手順を実行するライフサイクルを経ます。 これらの手順には、初期化、コントロールのインスタンス化、状態の復元と維持、イベントハンドラーコードの実行、およびレンダリングが含まれます。 ASP.NET Web フォームの機能について理解を深めたら、適切なライフサイクルステージでコードを記述できるように、 [ASP.NET ページのライフサイクル](https://msdn.microsoft.com/library/ms178472(v=vs.100).aspx)を理解することが重要です。

Web サーバーは、ページの要求を受信すると、ページを検索して処理し、ブラウザーに送信した後、すべてのページ情報を破棄します。 ユーザーが同じページを再度要求した場合、サーバーはシーケンス全体を繰り返し、ページをゼロから再処理します。 別の方法として、サーバーが処理したページのメモリが不足しています。ページはステートレスです。 ASP.NET page framework は、ページとそのコントロールの状態を維持するタスクを自動的に処理し、アプリケーション固有の情報の状態を維持するための明示的な方法を提供します。

> [!TIP] 
> 
> **Web フォームアプリケーションテンプレートの web アプリケーション機能**
> 
> ASP.NET Web フォームアプリケーションテンプレートには、豊富な組み込み機能のセットが用意されています。 これは *、default.aspx ページ*、 *About .aspx*ページ、および*Contact .aspx*ページを提供するだけでなく、ユーザーが web サイトにログインできるように、ユーザーを登録して資格情報を保存するメンバーシップ機能も備えています。 この概要では、ASP.NET Web フォームアプリケーションテンプレートに含まれるいくつかの機能について詳しく説明し、Wingtip Toys アプリケーションでそれらを使用する方法について説明します。
> 
> **メンバーシップ**
> 
> [ASP.NET](https://msdn.microsoft.com/library/yh26yfzy.aspx)Id は、アプリケーションによって作成されたデータベースにユーザーの資格情報を格納します。 ユーザーがログインすると、アプリケーションはデータベースを読み取って資格情報を検証します。 プロジェクトの*アカウント*フォルダーには、メンバーシップのさまざまな部分を実装するファイルが含まれています。これには、登録、ログイン、パスワードの変更、およびアクセスの承認が含まれます。 また、ASP.NET Web フォームは OAuth および OpenID もサポートしています。 これらの認証拡張機能により、ユーザーは、Facebook、Twitter、Windows Live、Google などのアカウントから既存の資格情報を使用してサイトにログインできるようになります。
> 
> ![プロジェクトソリューションエクスプローラーを作成する (ASP.NET Identity)](create-the-project/_static/image7.png)
> 
> 既定では、このテンプレートは SQL Server Express LocalDB のインスタンスの既定のデータベース名を使用してメンバーシップデータベースを作成します。これは、Web 用の Visual Studio Express 2013 に付属する開発データベースサーバーです。
> 
> **LocalDB の SQL Server Express**
> 
> [SQL Server Express LocalDB](https://technet.microsoft.com/library/hh510202.aspx)は、SQL Server データベースの多くのプログラミング機能を備えた軽量バージョンの SQL Server です。 SQL Server Express LocalDB はユーザーモードで実行され、インストールの前提条件の短い一覧を含む、高速でゼロ構成のインストールがあります。 Microsoft SQL Server では、すべてのデータベースまたは Transact-sql コードを SQL Server Express LocalDB から SQL Server に移動し、アップグレード手順を使用せずに SQL Azure できます。 そのため、SQL Server Express LocalDB は、SQL Server のすべてのエディションを対象とするアプリケーションの開発環境として使用できます。 SQL Server Express LocalDB を使用すると、ストアドプロシージャ、ユーザー定義関数と集計、.NET Framework 統合、空間型など、SQL Server Compact では使用できない他の機能を使用できます。
> 
> **マスター ページ**
> 
> [ASP.NET マスターページ](https://msdn.microsoft.com/library/wtxbf3hh.aspx)は、アプリケーション内のすべてのページについて、一貫した外観と動作を定義します。 マスターページのレイアウトは、個々のコンテンツページのコンテンツとマージされ、ユーザーに表示される最終ページが生成されます。 Wingtip Toys アプリケーションでは、*サイト*のマスターページを変更して、wingtip toys web サイトのすべてのページが同じ特徴的なロゴとナビゲーションバーを共有するようにします。
> 
> **HTML5**
> 
> ASP.NET Web フォームアプリケーションテンプレートでは、最新バージョンの HTML マークアップ言語である[HTML5](http://www.w3schools.com/html/html5_intro.asp)がサポートされています。 HTML5 は、Web サイトを簡単に作成できるようにする新しい要素と機能をサポートしています。
> 
> **Modernizr**
> 
> HTML5 をサポートしていないブラウザーでは、 [Modernizr](http://www.modernizr.com/)を使用できます。 Modernizr は、ブラウザーが HTML5 機能をサポートしているかどうかを検出できるオープンソースの JavaScript ライブラリであり、そうでない場合は有効にすることができます。 ASP.NET Web フォームアプリケーションテンプレートでは、Modernizr は NuGet パッケージとしてインストールされます。
> 
> **Bootstrap**
> 
> Visual Studio 2013 プロジェクトテンプレートでは[、Twitter](http://getbootstrap.com/)によって作成されたレイアウトとテーマフレームワークを使用します。 ブートストラップは CSS3 を使用して応答性の高いデザインを提供します。つまり、レイアウトはさまざまなブラウザーウィンドウサイズに動的に適応できます。 ブートストラップのテーマ機能を使用して、アプリケーションのルックアンドフィールの変化に簡単に影響を与えることもできます。 既定では Visual Studio 2013 の ASP.NET Web アプリケーションテンプレートには、NuGet パッケージとしてブートストラップが含まれています。
> 
> **NuGet パッケージ**
> 
> ASP.NET Web フォームアプリケーションテンプレートには、一連の[NuGet](http://www.nuget.org/)パッケージが含まれています。 これらのパッケージは、オープンソースライブラリおよびツールの形式で、コンポーネント化された機能を提供します。 アプリケーションの作成とテストに役立つさまざまなパッケージが用意されています。 Visual Studio を使用すると、NuGet パッケージの追加、削除、および更新を簡単に行うことができます。 開発者は、NuGet にパッケージを作成して追加することもできます。
> 
> ![[プロジェクトの作成-NuGet] ダイアログボックス](create-the-project/_static/image8.png)
> 
> パッケージをインストールすると、NuGet によってファイルがソリューションにコピーされ、参照の追加や Web アプリケーションに関連付けられている構成の変更など、必要な変更が自動的に行われます。 ライブラリを削除する場合は、NuGet によってファイルが削除され、プロジェクトに加えられた変更がすべて元に戻されるため、乱雑な状態になることはありません。 NuGet は、Visual Studio の **[ツール]** メニューから使用できます。
> 
> **jQuery**
> 
> [jQuery](http://jquery.com/)は、高速で簡潔な JavaScript ライブラリで、HTML ドキュメントの走査、イベント処理、アニメーション化、および迅速な web 開発のための Ajax 相互作用を簡略化します。 JQuery JavaScript ライブラリは、NuGet パッケージとして ASP.NET Web フォームアプリケーションテンプレートに含まれています。
> 
> **控えめに検証**
> 
> 組み込みの検証コントロールは、クライアント側の検証ロジックに控えめな JavaScript を使用するように構成されています。 これにより、ページマークアップでインラインでレンダリングされる JavaScript の量が大幅に減少し、ページ全体のサイズが縮小されます。 控えめな検証は、アプリケーションのルートにある web.config ファイルの &lt;appSettings&gt; 要素の設定に基づいて、グローバルに ASP.NET Web フォームアプリケーションテンプレートに追加さ*れます。*
> 
> **Entity Framework Code First**
> 
> Wingtip Toys アプリケーションでは、ASP.NET Web フォームアプリケーションテンプレートの機能に加えて、データを操作するときにコード中心の開発を可能にする NuGet ライブラリである[Entity Framework Code First](https://weblogs.asp.net/scottgu/archive/2010/12/08/announcing-entity-framework-code-first-ctp5-release.aspx)を使用します。 作成したコードに基づいて、アプリケーションのデータベース部分を作成するだけで済みます。 Entity Framework を使用すると、厳密に型指定されたオブジェクトとしてデータを取得および操作できます。 これにより、データへのアクセス方法の詳細ではなく、アプリケーションのビジネスロジックに集中できます。
> 
> ASP.NET Web Forms テンプレートに含まれているインストール済みライブラリおよびパッケージの詳細については、インストールされている NuGet パッケージの一覧を参照してください。 これを行うには、Visual Studio で新しい Web フォームプロジェクトを作成し、[**ツール** > **nuget パッケージマネージャー** ] を選択して **[ソリューションの nuget パッケージの管理]** を > 、 **[nuget パッケージの管理]** ダイアログボックスで **[インストール済みのパッケージ]** を選択します。

### <a name="touring-visual-studio"></a>ツーリング Visual Studio

Visual Studio のプライマリウィンドウには、**ソリューションエクスプローラー**、**サーバーエクスプローラー** (Express では**データベースエクスプローラー** )、[**プロパティ] ウィンドウ**、**ツールボックス**、**ツールバー**、および**ドキュメントウィンドウ**があります。

![[プロジェクトの作成-NuGet] ダイアログボックス](create-the-project/_static/image9.png)

Visual Studio の詳細については、「visual [Web Developer のビジュアルガイド](https://msdn.microsoft.com/library/ee410104.aspx)」を参照してください。

## <a name="summary"></a>まとめ

このチュートリアルでは、既定の Web フォームアプリケーションを作成し、確認して、実行しました。 既定の Web フォームアプリケーションのさまざまな機能を確認し、Visual Studio 環境の使用方法についていくつかの基本事項を学習しました。 次のチュートリアルでは、データアクセス層を作成します。

## <a name="additional-resources"></a>その他のリソース

[適切にプログラミングモデルを選択する](../../../videos/how-do-i/choosing-the-right-programming-model.md)   
Web[アプリケーションプロジェクトと Web サイトプロジェクト](https://msdn.microsoft.com/library/dd547590.aspx)   
[ASP.NET Web フォームページの概要](https://msdn.microsoft.com/library/428509ah.aspx)

> [!div class="step-by-step"]
> [前へ](introduction-and-overview.md)
> [次へ](create_the_data_access_layer.md)
