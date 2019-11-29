---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-introduction-1-of-12
title: 'Visual Studio を使用した SQL Server Compact での ASP.NET Web アプリケーションのデプロイ: 概要-1/12 |Microsoft Docs'
author: tdykstra
description: この一連のチュートリアルでは、Visual Stu... を使用して SQL Server Compact データベースを含む ASP.NET web アプリケーションプロジェクトをデプロイ (発行) する方法について説明します。
ms.author: riande
ms.date: 11/17/2011
ms.assetid: a2d7f33b-8c4a-4b48-9fb1-9139cf9b9878
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-introduction-1-of-12
msc.type: authoredcontent
ms.openlocfilehash: ea88da1e6d510f706fc7ca370cfa32974c1243f8
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74587720"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-introduction---1-of-12"></a>Visual Studio を使用した SQL Server Compact での ASP.NET Web アプリケーションのデプロイ: 概要-1/12

[Tom Dykstra](https://github.com/tdykstra)

[スタートプロジェクトのダウンロード](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> この一連のチュートリアルでは、Visual Studio 2012 RC または Visual Studio Express 2012 RC for Web を使用して SQL Server Compact データベースを含む ASP.NET web アプリケーションプロジェクトをデプロイ (発行) する方法について説明します。 Web 発行の更新をインストールする場合は、Visual Studio 2010 を使用することもできます。
> 
> Visual Studio 2012 の RC リリース後に導入された配置機能を示すチュートリアルについては、SQL Server Compact 以外の SQL Server のエディションをデプロイする方法、Azure App Service Web Apps にデプロイする方法については、「 [ASP.NET Web deployment Using Visual studio (Visual studio を使用した Web デプロイ](../../deployment/visual-studio-web-deployment/introduction.md)のデプロイ)」を参照してください。
> 
> これらのチュートリアルでは、最初にローカルの開発用コンピューターに配置し、次にサードパーティのホスティングプロバイダーに展開する方法を説明します。 デプロイするアプリケーションでは、アプリケーションデータベースと ASP.NET メンバーシップデータベースを使用します。 SQL Server Compact の使用と SQL Server Compact への配置を開始します。以降のチュートリアルでは、データベースの変更を展開する方法と、SQL Server に移行する方法について説明します。
> 
> このチュートリアルでは、Visual Studio で ASP.NET を使用する方法を理解していることを前提としています。 そうでない場合は、[基本的な ASP.NET Web フォームチュートリアル](../tailspin-spyworks/tailspin-spyworks-part-1.md)または[基本的な ASP.NET MVC チュートリアル](../../../../mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)を開始することをお勧めします。
> 
> チュートリアルに直接関係のない質問がある場合は、 [ASP.NET Deployment フォーラム](https://forums.asp.net/26.aspx/1?Configuration+and+Deployment)に投稿できます。

## <a name="overview"></a>の概要

これらのチュートリアルでは、最初にローカルの開発用コンピューターに配置し、次にサードパーティのホスティングプロバイダーに展開する方法を説明します。 デプロイするアプリケーションでは、アプリケーションデータベースと ASP.NET メンバーシップデータベースを使用します。 SQL Server Compact の使用と SQL Server Compact への配置を開始します。以降のチュートリアルでは、データベースの変更を展開する方法と、SQL Server に移行する方法について説明します。

チュートリアルの数–11すべてに加え、トラブルシューティングページでは、展開プロセスが困難に見える可能性があります。 実際、サイトをデプロイするための基本的な手順は、チュートリアルセットの比較的小さな部分を構成することです。 ただし、実際の状況では、多くの場合、展開のいくつかの重要な追加の側面に関する情報が必要になります。たとえば、対象サーバーのフォルダーのアクセス許可を設定します。 チュートリアルには、実際のアプリケーションを正常に展開できない可能性のある情報が記載されていないことを願っています。

チュートリアルは順番に実行するように設計されており、各部分は前の部分に基づいています。 ただし、状況に関係のない部分はスキップできます。 (パートをスキップすると、後のチュートリアルで手順の調整が必要になる場合があります)。

## <a name="intended-audience"></a>想定読者

このチュートリアルは、小規模な組織や、次のような環境で作業する ASP.NET 開発者を対象としています。

- 継続的インテグレーションプロセス (自動ビルドとデプロイ) は使用されません。
- 運用環境は、サードパーティのホスティングプロバイダーです。
- 通常、1人のユーザーが複数のロールを入力します (同じ人が開発、テスト、展開を行います)。

エンタープライズ環境では、継続的な統合プロセスを実装する方が一般的であり、運用環境は通常、会社独自のサーバーによってホストされます。 また、通常はさまざまな担当者が異なる役割を実行します。 エンタープライズ展開の詳細については、「[エンタープライズシナリオでの Web アプリケーションの展開](../../deployment/deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md)」を参照してください。

すべての規模の組織が web アプリケーションを Azure にデプロイすることもできます。これらのチュートリアルで説明されている手順のほとんどは、Azure アプリ Services Web Apps にも適用されます。 Azure の概要については、「 [https://azure.microsoft.com](https://azure.microsoft.com)」を参照してください。

## <a name="the-hosting-provider-shown-in-the-tutorials"></a>チュートリアルに表示されているホスティングプロバイダー

このチュートリアルでは、ホスティング会社でアカウントを設定し、そのホスティングプロバイダーにアプリケーションをデプロイするプロセスを紹介します。 このチュートリアルでは、ライブ web サイトへのデプロイの完全なエクスペリエンスを示すために、特定のホスティング会社を選択しました。 各ホスティング会社はさまざまな機能を提供しており、サーバーへの展開の経験は多少異なります。ただし、このチュートリアルで説明するプロセスは、全体的なプロセスにおいて一般的です。

このチュートリアルで使用されているホスティングプロバイダー (Cytanium.com) は、使用可能な多くのうちの1つであり、このチュートリアルでの使用は、保証や推奨事項を構成するものではありません。

## <a name="deploying-web-site-projects"></a>Web サイトプロジェクトの配置

Contoso 大学は、Visual Studio web アプリケーションプロジェクトです。 このチュートリアルで説明する配置方法とツールのほとんどは、 [Web サイトプロジェクト](https://msdn.microsoft.com/library/dd547590.aspx)には適用されません。 Web サイトプロジェクトを配置する方法の詳細については、「 [ASP.NET Deployment Content Map](https://msdn.microsoft.com/library/bb386521.aspx#deployment_for_web_site_projects)」を参照してください。

## <a name="deploying-aspnet-mvc-projects"></a>ASP.NET MVC プロジェクトの配置

このチュートリアルでは、ASP.NET Web フォームプロジェクトを配置しますが、実行する方法について学習した内容は ASP.NET MVC にも適用できます。 Visual Studio MVC プロジェクトは、別の形式の web アプリケーションプロジェクトです。 唯一の違いは、ASP.NET MVC またはターゲットバージョンをサポートしていないホスティングプロバイダーにデプロイする場合、プロジェクトに適切な ([mvc 3](http://nuget.org/packages/AspNetMvc/3.0.20105.0)または[mvc 4](http://nuget.org/packages/aspnetmvc)) NuGet パッケージがインストールされていることを確認する必要があることです。

## <a name="programming-language"></a>プログラミング言語

サンプルアプリケーションはをC#使用しますが、チュートリアルではC#の知識は必要ありません。また、チュートリアルで示されている配置手法は言語固有ではありません。

## <a name="troubleshooting-during-this-tutorial"></a>このチュートリアル中のトラブルシューティング

配置中にエラーが発生した場合、または配置されたサイトが正常に動作しない場合、エラーメッセージは常に解決策を提供するわけではありません。 一般的な問題のシナリオを解決するために、[トラブルシューティングのリファレンスページ](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)を利用できます。 チュートリアルを実行しているときにエラーメッセージが表示されたり動作しなかったりする場合は、必ずトラブルシューティングのページを確認してください。

## <a name="comments-welcome"></a>コメントの開始

チュートリアルのコメントは歓迎されます。チュートリアルが更新されると、チュートリアルのコメントに記載されている修正や改善の提案が行われます。

## <a name="prerequisites"></a>必要条件

開始する前に、Windows 7 以降と、次のいずれかの製品がコンピューターにインストールされていることを確認してください。

- [Visual Studio 2010 SP1](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)
- [Visual Web Developer Express 2010 SP1](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VWD2010SP1Pack)
- [Web 用 Visual Studio 2012 RC または Visual Studio Express 2012 RC](https://go.microsoft.com/fwlink/?LinkId=240162)

Visual Studio 2010 SP1 または Visual Web Developer Express 2010 SP1 を使用している場合は、次の製品もインストールします。

- [AZURE SDK for .net (VS 2010 SP1)](https://go.microsoft.com/fwlink/?LinkID=208120) (Web 発行更新プログラムを含む)
- [Microsoft Visual Studio 2010 SP1 Tools for SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCEVSTools)

このチュートリアルを完了するには、他にもいくつかのソフトウェアが必要ですが、まだ読み込まれている必要はありません。 このチュートリアルでは、必要なときにインストールする手順について説明します。

## <a name="downloading-the-sample-application"></a>サンプルアプリケーションのダウンロード

デプロイするアプリケーションの名前は Contoso 大学で、既に作成されています。 これは、 [ASP.NET サイトの Entity Framework チュートリアル](https://asp.net/entity-framework/tutorials)で説明されている Contoso 大学のアプリケーションに弱い、大学の web サイトの簡略化されたバージョンです。

前提条件がインストールされている場合は、 [Contoso 大学 web アプリケーション](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)をダウンロードします。 *.Zip*ファイルには、プロジェクトの複数のバージョンと、12個のチュートリアルをすべて含む PDF ファイルが含まれています。 チュートリアルの手順を実行するには、まず ContosoUniversity-Begin を使用します。 チュートリアルの最後でプロジェクトがどのように見えるかを確認するには、ContosoUniversity-End を開きます。 チュートリアル10で完全 SQL Server に移行する前に、プロジェクトがどのように表示されるかを確認するには、ContosoUniversity-AfterTutorial09 を開きます。

チュートリアルの手順に従って作業を準備するには、Visual Studio プロジェクトを操作するために使用する任意のフォルダーに ContosoUniversity-Begin を保存します。 既定では、次のフォルダーになります。

`C:\Users\<username>\Documents\Visual Studio 2012\Projects`

(このチュートリアルのスクリーンショットでは、プロジェクトフォルダーは `C`: ドライブのルートディレクトリにあります)。

Visual Studio を起動し、プロジェクトを開き、CTRL キーを押しながら F5 キーを押して実行します。

[![Home_page](deployment-to-a-hosting-provider-introduction-1-of-12/_static/image2.png)](deployment-to-a-hosting-provider-introduction-1-of-12/_static/image1.png)

Web サイトのページには、メニューバーからアクセスでき、次の機能を実行できます。

- 学生の統計情報を表示します ([バージョン情報] ページ)。
- 学生を表示、編集、削除、追加します。
- コースを表示および編集します。
- インストラクターを表示および編集します。
- 部門を表示および編集します。

次に、いくつかの代表的なページのスクリーンショットを示します。

[![Students_Page](deployment-to-a-hosting-provider-introduction-1-of-12/_static/image4.png)](deployment-to-a-hosting-provider-introduction-1-of-12/_static/image3.png)

[![Add_Students_Page](deployment-to-a-hosting-provider-introduction-1-of-12/_static/image6.png)](deployment-to-a-hosting-provider-introduction-1-of-12/_static/image5.png)

## <a name="reviewing-application-features-that-affect-deployment"></a>展開に影響するアプリケーション機能の確認

アプリケーションの次の機能は、アプリケーションの展開方法または展開方法に影響します。 これらについては、シリーズの次のチュートリアルで詳細に説明されています。

- Contoso 大学は、SQL Server Compact データベースを使用して、学生や教師の名前などのアプリケーションデータを格納します。 このデータベースには、テストデータと実稼働データが混在しています。また、運用環境に配置するときは、テストデータを除外する必要があります。 チュートリアルシリーズの後半では、SQL Server Compact から SQL Server に移行します。
- アプリケーションでは、ユーザーアカウント情報を SQL Server Compact データベースに格納する ASP.NET メンバーシップシステムが使用されます。 アプリケーションでは、一部の制限された情報にアクセスできる管理者ユーザーを定義します。 テストアカウントを使用せずに、1人の管理者アカウントでメンバーシップデータベースをデプロイする必要があります。
- アプリケーションデータベースとメンバーシップデータベースでは SQL Server Compact がデータベースエンジンとして使用されるため、データベースエンジンをホスティングプロバイダーとデータベース自体に配置する必要があります。
- このアプリケーションでは、メンバーシップシステムが SQL Server Compact データベースにデータを格納できるように、ASP.NET ユニバーサルメンバーシッププロバイダーを使用します。 ユニバーサルメンバーシッププロバイダーを含むアセンブリは、アプリケーションと共に配置する必要があります。
- アプリケーションは、Entity Framework 5.0 を使用して、アプリケーションデータベースのデータにアクセスします。 Entity Framework 5.0 を含むアセンブリは、アプリケーションと共に配置する必要があります。
- アプリケーションでは、サードパーティのエラーログとレポートユーティリティを使用します。 このユーティリティは、アプリケーションと共に配置する必要があるアセンブリで提供されます。
- エラーログユーティリティは、エラー情報を XML ファイル内のファイルフォルダーに書き込みます。 ASP.NET が展開されたサイトの下で実行されるアカウントにこのフォルダーへの書き込みアクセス許可があることを確認する必要があります。また、このフォルダーを展開から除外する必要があります。 (そうでない場合は、テスト環境からのエラーログデータが運用環境に配置されたり、運用エラーログファイルが削除されたりする可能性があります)。
- アプリケーションには、配置先の環境 (テストまたは運用) に応じて、配置された*web.config*ファイルで変更する必要があるいくつかの設定と、ビルド構成 (デバッグまたはリリース) に応じて変更する必要があるその他の設定が含まれます。
- Visual Studio ソリューションには、クラスライブラリプロジェクトが含まれています。 プロジェクト自体ではなく、このプロジェクトが生成するアセンブリだけを配置する必要があります。

このシリーズの最初のチュートリアルでは、サンプルの Visual Studio プロジェクトをダウンロードし、アプリケーションのデプロイ方法に影響を与えるサイトの機能を確認しました。 次のチュートリアルでは、これらのいくつかを自動的に処理するように設定することによって、デプロイを準備します。 他のユーザーは手動で行うことができます。

> [!div class="step-by-step"]
> [次へ](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12.md)
