---
uid: visual-studio/overview/2013/creating-web-projects-in-visual-studio
title: Visual Studio 2013 で ASP.NET Web プロジェクトを作成する |Microsoft Docs
author: tdykstra
description: このトピックでは、Update 3 で Visual Studio 2013 で ASP.NET web プロジェクトを作成するためのオプションについて説明します。ここでは、web 開発の新機能について説明します。
ms.author: riande
ms.date: 12/01/2014
ms.assetid: 61941e64-0c0d-4996-9270-cb8ccfd0cabc
msc.legacyurl: /visual-studio/overview/2013/creating-web-projects-in-visual-studio
msc.type: authoredcontent
ms.openlocfilehash: fbb4cd7afa2506879d47bce980bf0164aad40c2c
ms.sourcegitcommit: 88fc80e3f65aebdf61ec9414810ddbc31c543f04
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/22/2020
ms.locfileid: "76519272"
---
# <a name="creating-aspnet-web-projects-in-visual-studio-2013"></a>Visual Studio 2013 で ASP.NET Web プロジェクトを作成する

[Tom Dykstra](https://github.com/tdykstra)

> このトピックでは Visual Studio 2013 で Update 3 を使用して ASP.NET web プロジェクトを作成するためのオプションについて説明します。
> 
> 以前のバージョンの Visual Studio と比較した web 開発の新機能の一部を次に示します。
> 
> - [複数の ASP.NET フレームワーク](#add)(web フォーム、MVC、web API) のサポートを提供するプロジェクトを作成するための簡単な UI です。
> - [ASP.NET Identity](#indauth)、すべての ASP.NET フレームワークで同じように動作し、IIS 以外の web ホスティングソフトウェアで動作する新しい ASP.NET メンバーシップシステムです。
> - [ブートストラップ](#bootstrap)を使用して、応答性の高いデザインとテーマの機能を提供します。
> - [自動テストプロジェクトの作成](#testproj)や[イントラネットサイトテンプレート](#winauth)など、MVC にのみ提供される Web フォームの新機能。
> 
> Azure Cloud Services または Azure Mobile Services の web プロジェクトを作成する方法については、「azure [Cloud Services と ASP.NET の概要](https://azure.microsoft.com/documentation/articles/cloud-services-dotnet-get-started/)」と「 [Azure Mobile Services .net バックエンドでのランキングアプリの作成](https://azure.microsoft.com/documentation/articles/mobile-services-dotnet-backend-windows-store-dotnet-leaderboard/)」を参照してください。

<a id="prerequisites"></a>
## <a name="prerequisites"></a>Prerequisites

この記事は、 [Update 3](https://go.microsoft.com/fwlink/?linkid=397827&amp;clcid=0x409)がインストールされている[Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566)に適用されます。

<a id="wap"></a>
## <a name="web-application-projects-versus-web-site-projects"></a>Web アプリケーションプロジェクトと web サイトプロジェクト

ASP.NET を使用すると、web*アプリケーションプロジェクト*と*web サイトプロジェクト*の2種類の web プロジェクトを選択できます。 新しい開発のために web アプリケーションプロジェクトを使用することをお勧めします。この記事は、web アプリケーションプロジェクトにのみ適用されます。 詳細については、MSDN サイトの「 [Web アプリケーションプロジェクトと Visual Studio の Web サイトプロジェクト](https://msdn.microsoft.com/library/dd547590(v=vs.120).aspx)」を参照してください。

<a id="overview"></a>
## <a name="overview-of-web-application-project-creation"></a>Web アプリケーションプロジェクトの作成の概要

次の手順は、web プロジェクトを作成する方法を示しています。

1. **スタート**ページまたは **[ファイル]** メニューの **[新しいプロジェクト]** をクリックします。
2. **[新しいプロジェクト]** ダイアログボックスで、左ペインの **[web]** をクリックし、中央のウィンドウで**ASP.NET web アプリケーション**をクリックします。

    ![[新しいプロジェクト] ダイアログ](creating-web-projects-in-visual-studio/_static/image1.png)

    左側のウィンドウで **[クラウド]** を選択して、 [azure クラウドサービス](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy)、 [azure Mobile Service](https://msdn.microsoft.com/library/windows/apps/dn629482.aspx)、または[azure web ジョブ](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-webjobs)を作成できます。 このトピックでは、これらのテンプレートについては説明しません。
3. アプリケーションの正常性と使用状況の監視が必要な場合は、右側のウィンドウで **[Application Insights をプロジェクトに追加する]** チェックボックスをオンにします。 詳細については、「[Web アプリケーションのパフォーマンスを監視する](https://azure.microsoft.com/documentation/articles/app-insights-web-monitor-performance/)」を参照してください。
4. プロジェクト**名**、**場所**、およびその他のオプションを指定し、[ **OK]** をクリックします。

    **[New ASP.NET Project]** ダイアログボックスが表示されます。

    ![[新しいプロジェクト] ダイアログ](creating-web-projects-in-visual-studio/_static/image2.png)
5. テンプレートをクリックします。

    ![テンプレートの選択](creating-web-projects-in-visual-studio/_static/image3.png)
6. テンプレートに含まれていない追加のフレームワークのサポートを追加する場合は、該当するチェックボックスをオンにします。 (この例では、MVC または Web API を Web フォームプロジェクトに追加できます)。

    ![フレームワークの追加](creating-web-projects-in-visual-studio/_static/image4.png)
7. <a id="testproj"></a>単体テストプロジェクトを追加する場合は、 **[単体テストの追加]** をクリックします。

    ![単体テストの追加](creating-web-projects-in-visual-studio/_static/image5.png)
8. テンプレートが既定で提供するものとは異なる認証方法が必要な場合は、 **[認証の変更]** をクリックします。

    ![[認証の構成] ボタン](creating-web-projects-in-visual-studio/_static/image6.png)

    ![認証の構成ダイアログ](creating-web-projects-in-visual-studio/_static/image7.png)

<a id="azurenewproj"></a>
### <a name="create-a-web-app-or-virtual-machine-in-azure"></a>Azure で web アプリまたは仮想マシンを作成する

Visual Studio には、web アプリケーションをホストするために Azure サービスを簡単に操作できるようにする機能が含まれています。 たとえば、Visual Studio IDE から次のすべての操作を実行できます。

- インターネット経由でアプリケーションを利用できるようにする web アプリまたは仮想マシンを作成および管理します。
- クラウドで実行されるアプリケーションによって作成されたログを表示します。
- アプリケーションがクラウドで実行されている間は、リモートでデバッグモードで実行します。
- SQL データベースなどの他の Azure サービスを表示および管理します。

無料の web apps などの基本的なサービスを含む[Azure アカウントを作成](https://www.windowsazure.com/pricing/free-trial/)できます。 MSDN サブスクライバーの場合は、追加の azure サービスに対する月々のクレジットを提供する[特典を有効](https://azure.microsoft.com/pricing/member-offers/visual-studio-subscriptions/)にすることができます。 

既定では、 **[新しい ASP.NET プロジェクト]** ダイアログボックスを使用して、新しい web プロジェクトの web アプリまたは仮想マシンを作成できます。 新しい web アプリまたは仮想マシンを作成しない場合は、 **[クラウド内のホスト]** チェックボックスをオフにします。

![リモートリソースの作成](creating-web-projects-in-visual-studio/_static/image8.png)

チェックボックスのキャプションは、**クラウド内のホストで**ある場合もあれば、**リモートリソースを作成**する場合もあります。どちらの場合も、影響は同じです。 このチェックボックスをオンのままにすると、Visual Studio は既定で Azure App Service web アプリを作成します。 ドロップダウンボックスを使用して、必要に応じて**仮想マシン**を変更できます。 Azure にまだサインインしていない場合は、Azure 資格情報を入力するように求められます。 サインインすると、Visual Studio によってプロジェクトに対して作成されるリソースを構成するためのダイアログボックスが表示されます。 次の図は、web アプリのダイアログを示しています。仮想マシンの作成を選択した場合は、異なるオプションが表示されます。

![Azure アプリ設定の構成](creating-web-projects-in-visual-studio/_static/image9.png)

このプロセスを使用して Azure リソースを作成する方法の詳細については、「 [azure と ASP.NET の概要](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet)」と「 [Visual Studio で web サイトの仮想マシンを作成](https://azure.microsoft.com/documentation/articles/virtual-machines-dotnet-create-visual-studio-powershell/)する」を参照してください。

この記事の残りの部分では、使用可能なテンプレートとそのオプションの詳細について説明します。 また、この記事では、テンプレートで使用されるレイアウトおよびテーマフレームワークのブートストラップについても説明します。

<a id="vs2013"></a>
## <a name="visual-studio-2013-web-project-templates"></a>Visual Studio 2013 Web プロジェクトテンプレート

Visual Studio では、テンプレートを使用して web プロジェクトを作成します。 プロジェクトテンプレートでは、新しいプロジェクトにファイルとフォルダーを作成し、NuGet パッケージをインストールして、基本的な動作アプリケーションのサンプルコードを提供できます。 テンプレートは、最新の web 標準を実装しており、ASP.NET テクノロジを使用する方法のベストプラクティスを紹介すると共に、独自のアプリケーションの作成をすぐに開始することを目的としています。

Visual Studio 2013 は、.net 4.5 以降のバージョンの .NET framework を対象とするプロジェクトの web プロジェクトテンプレートに対して、次の選択肢を提供します。

- [空のテンプレート](#empty)
- [Web フォームテンプレート](#wf)
- [MVC テンプレート](#mvc)
- [Web API テンプレート](#webapi)
- [シングルページアプリケーションテンプレート](#spa)
- [Azure モバイルサービステンプレート](https://azure.microsoft.com/documentation/articles/mobile-services-dotnet-backend-windows-store-dotnet-leaderboard/)
- [Visual Studio 2012 テンプレート](#vs2012)

[Facebook テンプレート](#facebook)を提供する Visual Studio 拡張機能をインストールすることもできます。

.NET 4 を対象とするプロジェクトを作成する方法については、このトピックで後述する「 [Visual Studio 2012 のテンプレート](#vs2012)」を参照してください。

モバイルクライアント用の ASP.NET アプリケーションを作成する方法の詳細については、 [ASP.NET でのモバイルサポートに](../../../mobile/overview.md)関する説明を参照してください。

<a id="empty"></a>
### <a name="empty-template"></a>空のテンプレート

空のテンプレートには、プロジェクトファイル ( *.csproj*または*など、ASP.NET web アプリの最小限のフォルダーとファイルが用意されています.vbproj*) と web.config*ファイル。* Web フォーム、MVC、または Web API のサポートを追加するには、 **[フォルダーの追加とコア参照]** ラベルの下にあるチェックボックスを使用します。

空のテンプレートでは、認証オプションは使用できません。 認証機能はサンプルアプリケーションに実装されており、空のテンプレートはサンプルアプリケーションを作成しません。

<a id="wf"></a>
### <a name="web-forms-template"></a>Web フォームテンプレート

Web Forms framework には、UI およびデータアクセス機能に豊富な web サイトをすばやく作成するための次の機能が用意されています。

- Visual Studio の WYSIWYG デザイナー。
- HTML を表示し、プロパティとスタイルを設定することによってカスタマイズできるサーバーコントロール。
- データアクセスとデータ表示のための豊富なコントロールです。
- WPF などのクライアントアプリケーションをプログラミングするようにプログラミングできるイベントを公開するイベントモデル。
- HTTP 要求間の状態 (データ) の自動保存。

一般に、Web フォームアプリケーションを作成するには、ASP.NET MVC フレームワークを使用して同じアプリケーションを作成するよりも、プログラミング作業が少なくて済みます。 ただし、Web フォームはアプリケーションの迅速な開発のためだけではありません。 Web フォーム上に構築された複雑な商用アプリケーションやフレームワークは多数あります。

Web フォームページとページ上のコントロールは、ブラウザーに送信される多くのマークアップを自動的に生成するため、ASP.NET MVC が提供する HTML をきめ細かく制御することはできません。 ページとコントロールを構成するための宣言型モデルでは、記述する必要のあるコードの量が最小限に抑えられますが、HTML および HTTP の動作の一部は非表示になります。 たとえば、コントロールによって生成されるマークアップを正確に指定することはできません。

Web フォームフレームワークは、[テスト駆動型](http://en.wikipedia.org/wiki/Test-driven_development)の開発、[懸念事項の分離](http://en.wikipedia.org/wiki/Separation_of_concerns)、[制御の反転](http://en.wikipedia.org/wiki/Inversion_of_control)、[依存関係の注入](http://en.wikipedia.org/wiki/Dependency_injection)などのパターンベースの開発手法に ASP.NET MVC ほど簡単には適していません。 そのようなコードを記述する場合は、ASP.NET MVC フレームワークの場合と同様に、自動ではありません。 [ASP.NET Web FORMS MVP](http://webformsmvp.com/)プロジェクトは、web フォームが提供される迅速な開発を維持しながら、問題とテスト容易性の分離を促進するアプローチを示しています。 Microsoft SharePoint は、Web フォーム MVP 上に構築されています。

Web フォームテンプレートは、[ブートストラップ](#bootstrap)を使用して応答性の高いデザイン機能とテーマ機能を提供するサンプル Web フォームアプリケーションを作成します。 次の図は、ホームページを示しています。

![Web フォームテンプレートアプリのホームページ](creating-web-projects-in-visual-studio/_static/image10.png)

Web フォームの詳細については、「 [ASP.NET Web forms](https://asp.net/web-forms)」を参照してください。 Web フォームテンプレートの機能の詳細については、「 [Visual Studio 2013 を使用した基本的な Web フォームアプリケーションの構築](https://blogs.msdn.com/b/webdev/archive/2013/12/19/building-a-basic-web-forms-application-using-visual-studio-2013.aspx)」を参照してください。

<a id="mvc"></a>
### <a name="mvc-template"></a>MVC テンプレート

ASP.NET MVC は、[テスト駆動型開発](http://en.wikipedia.org/wiki/Test-driven_development)、[懸念事項の分離](http://en.wikipedia.org/wiki/Separation_of_concerns)、[制御の逆転](http://en.wikipedia.org/wiki/Inversion_of_control)、[依存関係の注入](http://en.wikipedia.org/wiki/Dependency_injection)などのパターンベースの開発手法を容易にするように設計されています。 フレームワークは、web アプリケーションのビジネスロジック層とプレゼンテーション層を分離することをお勧めします。 アプリケーションをモデル (M)、ビュー (V)、およびコントローラー (C) に分割することにより、ASP.NET MVC を使用すると、大規模なアプリケーションの複雑さを管理しやすくなります。

ASP.NET MVC、HTML および Web フォームでよりも HTTP をより直接操作することにします。 たとえば、Web フォームは HTTP 要求間で状態を自動的に保持できますが、MVC では明示的にコードを記述する必要があります。 MVC モデルの利点は、アプリケーションが何を実行しているか、および web 環境でどのように動作するかを完全に制御できることです。 欠点は、さらに多くのコードを記述する必要があることです。

MVC は拡張できるように設計されており、開発者はアプリケーションのニーズに合わせてフレームワークをカスタマイズできます。 また、ASP.NET MVC ソースコードは、OSI ライセンスで利用できます。

MVC テンプレートでは、[ブートストラップ](#bootstrap)を使用して応答性の高いデザイン機能とテーマ機能を提供するサンプル MVC 5 アプリケーションを作成します。 次の図は、ホームページを示しています。

![MVC サンプルアプリケーション](creating-web-projects-in-visual-studio/_static/image11.png)

MVC の詳細については、「 [ASP.NET mvc](https://asp.net/mvc)」を参照してください。 MVC 4 テンプレートを選択する方法の詳細については、この記事で後述する「 [Visual Studio 2012 のテンプレート](#vs2012)」を参照してください。

<a id="webapi"></a>
### <a name="web-api-template"></a>Web API テンプレート

Web API テンプレートは、MVC に基づく API ヘルプページを含む、Web API に基づいたサンプル web サービスを作成します。

ASP.NET Web API は、ブラウザーやモバイル デバイスなどを含む多様なクライアントに提供できる HTTP サービスの構築が容易になるフレームワークです。 ASP.NET Web API は、.NET Framework で RESTful サービスを構築するための理想的なプラットフォームです。

Web API テンプレートによって、サンプル web サービスが作成されます。 次の図は、サンプルのヘルプページを示しています。

![Web API のヘルプページ](creating-web-projects-in-visual-studio/_static/image12.png)

![GET API の Web API ヘルプページ](creating-web-projects-in-visual-studio/_static/image13.png)

Web API の詳細については、「 [ASP.NET Web API](https://asp.net/web-api)」を参照してください。

<a id="spa"></a>
### <a name="single-page-application-template"></a>単一ページ アプリケーション テンプレート

シングルページアプリケーション (SPA) テンプレートでは、クライアントで JavaScript、HTML 5、および[KnockoutJS](http://knockoutjs.com/)を使用するサンプルアプリケーションを作成し、サーバー上で ASP.NET Web API します。

SPA テンプレートの唯一の認証オプションは、[個々のユーザーアカウント](#indauth)です。

次の図は、SPA テンプレートによって作成されるサンプルアプリケーションの初期状態を示しています。

![SPA サンプルアプリケーション](creating-web-projects-in-visual-studio/_static/image14.png)

SPA テンプレートを使用してアプリケーションを作成する方法の詳細については、「 [WEB API-外部認証サービス](../../../web-api/overview/security/external-authentication-services.md)」を参照してください。

ASP.NET シングルページアプリケーションの詳細と、KnockoutJS 以外の JavaScript フレームワークを使用する追加の SPA テンプレートについては、次のリソースを参照してください。

- [ASP.NET シングルページアプリケーション](../../../single-page-application/index.md)。
- [VS2013 RC 用の SPA テンプレートのセキュリティ機能について](https://blogs.msdn.com/b/webdev/archive/2013/09/20/understanding-security-features-in-spa-template.aspx)
- [シングルページアプリケーション: ASP.NET を使用して最新で応答性の高い Web Apps を構築する](https://msdn.microsoft.com/magazine/dn463786.aspx)

<a id="facebook"></a>
### <a name="facebook-template"></a>Facebook テンプレート

[Facebook テンプレートを提供する Visual Studio 拡張機能](https://go.microsoft.com/fwlink/?LinkID=509965&amp;clcid=0x409)をインストールできます。 このテンプレートは、Facebook web サイト内で実行するように設計されたサンプルアプリケーションを作成します。 これは ASP.NET MVC に基づいており、Web API を使用してリアルタイム更新機能を備えています。

Facebook のアプリケーションは facebook サイト内で実行され、Facebook の認証を利用するため、Facebook テンプレートに使用できる認証オプションはありません。

ASP.NET Facebook アプリケーションの詳細については、「 [MVC FACEBOOK API の更新](https://blogs.msdn.com/b/webdev/archive/2014/06/10/updating-the-mvc-facebook-api.aspx)」を参照してください。

<a id="vs2012"></a>
### <a name="visual-studio-2012-templates"></a>Visual Studio 2012 テンプレート

Visual Studio 2013 web プロジェクトの作成ダイアログでは、Visual Studio 2012 で使用できた一部のテンプレートにアクセスすることはできません。 これらのテンプレートのいずれかを使用する場合は、Visual Studio の [新しいプロジェクト] ダイアログボックスの左ペインで [Visual Studio 2012] ノードをクリックします。

![Visual Studio 2012 テンプレート](creating-web-projects-in-visual-studio/_static/image15.png)

**[Visual Studio 2012]** ノードでは、Visual Studio 2013 のテンプレートの既定の一覧で、アクセス権のない次の web テンプレートを選択できます。

- ASP.NET MVC 4 Web アプリケーション
- ASP.NET 動的データ エンティティ Web アプリケーション
- ASP.NET AJAX サーバーコントロール
- ASP.NET AJAX サーバーコントロールエクステンダー
- ASP.NET サーバーコントロール

<a id="bootstrap"></a>
## <a name="bootstrap-in-the-visual-studio-2013-web-project-templates"></a>Visual Studio 2013 web プロジェクトテンプレートでのブートストラップ

Visual Studio 2013 プロジェクトテンプレートでは[、Twitter](http://getbootstrap.com/)によって作成されたレイアウトとテーマフレームワークを使用します。 ブートストラップは CSS3 を使用して応答性の高いデザインを提供します。つまり、レイアウトはさまざまなブラウザーウィンドウサイズに動的に適応できます。 たとえば、ワイドブラウザーウィンドウでは、Web フォームテンプレートによって作成されたホームページは次の図のようになります。

![Web フォームテンプレートアプリのホームページ](creating-web-projects-in-visual-studio/_static/image16.png)

ウィンドウの幅を狭くし、水平方向に配置された列を垂直方向に移動します。

![ブートストラップ垂直方向の列配置](creating-web-projects-in-visual-studio/_static/image17.png)

ウィンドウをもう少し狭くします。横にある上部のメニューはアイコンに変わり、クリックして垂直方向のメニューに展開することができます。

![ブートストラップメニューアイコン](creating-web-projects-in-visual-studio/_static/image18.png)

![ブートストラップの垂直方向のメニュー](creating-web-projects-in-visual-studio/_static/image19.png)

ブートストラップのテーマ機能を使用して、アプリケーションのルックアンドフィールの変化に簡単に影響を与えることもできます。 たとえば、次の手順を実行して、テーマを変更できます。

1. ブラウザーでに移動[ http://Bootswatch.com ](http://Bootswatch.com)、テーマを選択し、クリックして**ダウンロード**です。 (これにより、既定では、*ブートストラップ*がダウンロードされます。 css コードを確認する場合は、縮小版ではなく、*ブートストラップ*を取得します。)
2. ダウンロードした CSS ファイルの内容をコピーします。
3. Visual Studio で、 *Content*フォルダーに*bootstrap-theme*という名前の新しい**スタイルシート**ファイルを作成し、ダウンロードした css コードを貼り付けます。
4. \_アプリを開き、 *config を起動また*は bootstrap-theme し、*ブートストラップ*をに変更します。

プロジェクトをもう一度実行すると、アプリケーションの外観が新しくなります。 次の図は、アメリアテーマの効果を示しています。

![ブートストラップのアメリアテーマ](creating-web-projects-in-visual-studio/_static/image20.png)

多くのブートストラップテーマを利用できます (free バージョンと premium バージョンの両方)。 ブートストラップには、[ドロップダウン](http://twitter.github.io/bootstrap/components.html#dropdowns)、[ボタングループ](http://twitter.github.io/bootstrap/components.html#buttonGroups)、[アイコン](http://twitter.github.io/bootstrap/base-css.html#images)など、さまざまな UI コンポーネントが用意されています。 ブートストラップの詳細については、「[ブートストラップサイト](http://twitter.github.io/bootstrap/)」を参照してください。

Visual Studio で Web フォームデザイナーを使用している場合は、デザイナーで CSS3 がサポートされていないので、ブートストラップのテーマまたは応答性の高いレイアウトの変更によるすべての影響を正確に示すことはできません。 ただし、ブラウザーで表示すると、Web フォームページが正しく表示されます。

<a id="add"></a>
## <a name="adding-support-for-additional-frameworks"></a>追加のフレームワークのサポートを追加する

テンプレートを選択すると、テンプレートによって使用されているフレームワークのチェックボックスが自動的にオンになります。 たとえば、 **[Web フォーム]** テンプレートを選択した場合、 **[web フォーム]** チェックボックスがオンになっているので、これをオフにすることはできません。

![テンプレートの選択](creating-web-projects-in-visual-studio/_static/image21.png)

![フレームワークの追加](creating-web-projects-in-visual-studio/_static/image22.png)

プロジェクトの作成時にそのフレームワークのサポートを追加するために、テンプレートに含まれていないフレームワークのチェックボックスをオンにすることができます。 たとえば、MVC テンプレートを選択したときに Web フォームの *.aspx*ページを使用できるようにするには、 **[web フォーム]** チェックボックスをオンにします。 または、Web フォームテンプレートを使用しているときに MVC を有効にするには、 **[mvc]** チェックボックスをオンにします。 フレームワークを追加すると、デザイン時および実行時サポートが有効になります。 たとえば、Web フォームプロジェクトに MVC サポートを追加すると、コントローラーとビューをスキャフォールディングすることができます。

Web フォームと MVC をプロジェクトで結合し、Web フォームで[フレンドリな url](http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx)を有効にすると、1つの URL に複数の可能なターゲットがある場合に、予期しないルーティングの問題が発生する可能性があります。 最初に定義されたルートが優先されます。 たとえば、`Home` コントローラーと*default.aspx*ページがある場合、 *RouteConfig.cs*で `MapRoute` メソッドを呼び出す前に `EnableFriendlyUrls` メソッドを呼び出すと、`http://contoso.com/home` の url が*default.aspx*に表示されます。 `Home` の前に `MapRoute` を呼び出した場合は、同じ url が `EnableFriendlyUrls`コントローラーの既定のビューに送られます。

フレームワークを追加しても、サンプルアプリケーションの機能は追加されません。 たとえば、MVC テンプレートを選択したときに Web フォームサポートを追加した場合、 *default.aspx*ホームページファイルは作成されません。 フレームワークをサポートするために必要なフォルダー、ファイル、および参照のみが追加されます。 そのため、フレームワークを追加しても、テンプレートによって作成されたサンプルアプリケーションのコードによって実装される認証オプションは変更されません。 たとえば、空のテンプレートを選択して Web フォームまたは MVC サポートを追加した場合でも、 **[認証の構成]** ボタンは無効になります。

以下のセクションでは、各チェックボックスの効果について簡単に説明します。

### <a name="add-web-forms-support"></a>Web フォームサポートの追加

空の*アプリ\_データ*と*モデル*のフォルダーおよび*global.asax*ファイルを作成します。 これらは、空のテンプレート以外のすべてのテンプレートで既に作成されているので、[Web フォーム] チェックボックスをオンにすると、他のテンプレートに違いはありません。

Web フォームテンプレートでは、既定でフレンドリ Url が有効になっていますが、[Web フォーム] チェックボックスをオンにして Web フォームサポートを他のテンプレートに追加すると、フレンドリな Url は自動的に有効になりません。

### <a name="add-mvc-support"></a>MVC サポートの追加

MVC、Razor、および Web ページの NuGet パッケージをインストールし、空の*アプリ\_データ*、*コントローラー*、*モデル*、および*ビュー*のフォルダーを作成し、*アプリ\_の開始*フォルダーを*RouteConfig.cs*ファイルで作成し、 *global.asax*ファイルを作成します。

### <a name="add-web-api-support"></a>Web API サポートの追加

WebApi および Newtonsoft. Json パッケージをインストールし、空*のアプリ\_データ*、*コントローラー*、*およびモデル*の各フォルダーを作成し、 *WebApiConfig.cs*ファイルを使用して*アプリ\_の開始*フォルダーを作成し、 *global.asax*ファイルを作成します。

<a id="auth"></a>
## <a name="authentication-methods"></a>認証方式

Visual Studio 2013 には、Web フォーム、MVC、および Web API テンプレートに対していくつかの認証オプションが用意されています。

- [認証なし](#noauth)
- [個々のユーザーアカウント](#indauth)(以前の ASP.NET メンバーシップと呼ばれていた ASP.NET Identity)
- [組織アカウント](#orgauth)(Windows Server Active Directory または Azure Active Directory)
- [Windows 認証](#winauth)(イントラネット)

![認証の構成ダイアログ](creating-web-projects-in-visual-studio/_static/image23.png)

<a id="noauth"></a>

### <a name="no-authentication"></a>認証なし

**[認証なし]** を選択した場合、サンプルアプリケーションには、ログインするための web ページが含まれません。ログインしているユーザーを示す UI、メンバーシップデータベースのエンティティクラスはなく、メンバーシップデータベースの接続文字列はありません。

<a id="indauth"></a>
### <a name="individual-user-accounts"></a>個々のユーザー アカウント

**個々のユーザーアカウント**を選択した場合、サンプルアプリケーションは、ユーザー認証のために ASP.NET Identity (旧称 ASP.NET membership) を使用するように構成されます。 ASP.NET Identity を使用すると、ユーザーは、サイトにユーザー名とパスワードを作成するか、Facebook、Google、Microsoft アカウント、Twitter などのソーシャルプロバイダーでサインインすることにより、アカウントを登録できます。 ASP.NET Identity のユーザープロファイルの既定のデータストアは SQL Server LocalDB データベースです。このデータベースは、運用サイトの SQL Server または Azure SQL Database に配置できます。

Visual Studio 2013、これらの機能は Visual Studio 2012 と同じですが、ASP.NET メンバーシップシステムの基になるコードが書き換えられています。 新しいコードベースには、次のような利点があります。

- 新しいメンバーシップシステムは、ASP.NET Forms Authentication モジュールではなく、 [OWIN](http://owin.org/)に基づいています。 これは、IIS で Web フォームまたは MVC を使用しているかどうかにかかわらず、同じ認証メカニズムを使用できること、または Web API または SignalR を自己ホストしていることを意味します。
- 新しいメンバーシップデータベースは Entity Framework Code First によって管理され、すべてのテーブルは、変更可能なエンティティクラスによって表されます。 つまり、データベーススキーマとプロファイル関連の web UI を独自のニーズに合わせて簡単にカスタマイズでき、Code First Migrations を使用して簡単に更新を展開できます。

新しいメンバーシップシステムは新しいテンプレートに自動的に実装され、.NET 4.5 以降を対象とする任意のプロジェクトで手動で実装できます。

ASP.NET Identity は、主に外部の顧客向けのインターネット web サイトを作成する場合に適しています。 組織で Active Directory または Office 365 を使用していて、従業員とビジネスパートナーに対してシングルサインオンを有効にするプロジェクトを作成する場合は、 **[組織アカウント]** オプションを選択することをお勧めします。

個々のユーザーアカウントオプションの詳細については、次のリソースを参照してください。

- [www.asp.net/identity](../../../identity/index.md)。 ASP.NET web サイトでの ASP.NET Identity に関するドキュメント。
- [Facebook と Google OAuth2、OpenID サインオンを使用して ASP.NET MVC 5 アプリを作成](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)します。 また、ユーザープロファイルデータをカスタマイズする方法についても説明します。
- [Web API-外部認証サービス](../../../web-api/overview/security/external-authentication-services.md)
- [Visual Studio 2013 で ASP.NET アプリケーションに外部ログインを追加する](https://blogs.msdn.com/b/webdev/archive/2013/06/27/adding-external-logins-to-your-asp-net-application-in-visual-studio-2013.aspx)

<a id="orgauth"></a>
### <a name="organizational-accounts"></a>組織アカウント

**組織アカウント**を選択した場合、サンプルアプリケーションは、Azure Active Directory (Azure AD、Office 365 を含む) または windows Server Active Directory のユーザーアカウントに基づいた認証に Windows Identity FOUNDATION (WIF) を使用するように構成されます。 詳細については、このトピックで後述する「[組織アカウントの認証オプション](#orgauthoptions)」を参照してください。

<a id="winauth"></a>
### <a name="windows-authentication"></a>Windows 認証

**Windows 認証**を選択した場合、サンプルアプリケーションは認証用に WINDOWS 認証 IIS モジュールを使用するように構成されます。 アプリケーションでは、Windows にログインしている Active directory アカウントまたはローカルコンピューターアカウントのドメインとユーザー ID が表示されますが、ユーザー登録またはログイン UI は含まれません。 このオプションは、イントラネット web サイトを対象としています。

または、[[組織アカウント] の [オンプレミス] オプション](#orgauthonprem)を選択して、AD 認証を使用するイントラネットサイトを作成することもできます。 オンプレミスオプションでは、Windows 認証モジュールの代わりに Windows Identity Foundation (WIF) が使用されます。 オンプレミスオプションを設定するために、いくつかの追加の手順が必要ですが、WIF では Windows 認証モジュールでは使用できない機能が有効になっています。 たとえば、WIF では、Active Directory でアプリケーションアクセスを構成し、ディレクトリデータを照会できます。

<a id="orgauthoptions"></a>
## <a name="organizational-account-authentication-options"></a>組織アカウントの認証オプション

**[認証の構成]** ダイアログには、Azure Active Directory (Azure AD、Office 365 を含む)、または Windows Server ACTIVE DIRECTORY (AD) アカウント認証に関するいくつかのオプションがあります。

- [クラウドシングル組織](#orgauthsingle)(Azure AD、または Azure AD とディレクトリ統合を使用した AD)
- [クラウド-マルチ組織](#orgauthmulti)(Azure AD、またはディレクトリと Azure AD との統合を使用した AD)
- [オンプレミス](#orgauthonprem)(AD)

Azure AD のオプションのいずれかを試しても、まだアカウントがない場合は、[ここをクリックして Azure AD アカウントにサインアップ](https://go.microsoft.com/fwlink/?LinkId=309942)します。

> [!NOTE]
> Azure AD のオプションのいずれかを選択した場合、プロジェクトにはデータベースが必要であり、Azure AD テナントのグローバル管理者アカウントにサインインする必要があります。 Azure AD テナントの管理アクセス許可を持つ組織アカウント (admin@contoso.onmicrosoft.comなど) の名前とパスワードを入力します。
> 
> **サインインダイアログボックスに Microsoft アカウントの資格情報 (contoso@hotmail.comなど) を入力しないでください。**

<a id="orgauthsingle"></a>
### <a name="cloud---single-organization-authentication"></a>クラウドシングル組織認証

![単一組織認証](creating-web-projects-in-visual-studio/_static/image24.png)

1つの Azure AD[テナント](https://technet.microsoft.com/library/jj573650.aspx)で定義されているユーザーアカウントの認証を有効にする場合は、このオプションを選択します。 たとえば、サイトは contoso.com で、contoso.onmicrosoft.com テナントに属している Contoso 社の従業員が使用できるようになります。 他のテナントのユーザーがアプリケーションにアクセスできるように Azure AD を構成することはできません。

#### <a name="domain"></a>ドメイン

アプリケーションをセットアップする Azure AD ドメイン (例: `contoso.onmicrosoft.com`) を入力します。 `contoso.onmicrosoft.com`ではなく `contoso.com` などの[カスタムドメイン](http://www.cloudidentity.com/blog/2013/04/14/adding-a-custom-domain-to-your-windows-azure-ad/)がある場合は、ここで入力できます。

#### <a name="access-level"></a>アクセスレベル

アプリケーションが Graph API を使用してディレクトリ情報のクエリまたは更新を行う必要がある場合は、[**シングルサインオン]、[ディレクトリデータの読み取り**] または **[シングルサインオン]、[ディレクトリデータの読み取りと書き込み**] の順に選択します。 それ以外の場合は、 **[シングルサインオン]** を選択します。 詳細については、「[アプリケーションアクセスレベル](https://msdn.microsoft.com/library/windowsazure/b08d91fa-6a64-4deb-92f4-f5857add9ed8#BKMK_AccessLevels)」と「 [Graph API を使用したクエリ Azure AD](https://msdn.microsoft.com/library/windowsazure/dn151791.aspx)」を参照してください。

#### <a name="application-id-uri"></a>アプリケーション ID URI

既定では、テンプレートは、Azure AD ドメインにプロジェクト名を追加することによって、アプリケーション ID の URI を作成します。 たとえば、プロジェクト名が `Example` で、ドメインが `contoso.onmicrosoft.com`場合、アプリケーション ID URI は `https://contoso.onmicrosoft.com/Example`になります。 アプリケーション ID の URI を手動で指定する場合は、 **[その他のオプション]** セクションを展開し、テキストボックスにアプリケーション ID の uri を入力します。 アプリケーション ID の URI は `https://`で始まる必要があります。

既定では、Azure AD で既にプロビジョニングされているアプリケーションが、Visual Studio がプロジェクトに使用しているものと同じアプリケーション ID URI を持っている場合、プロジェクトは新しいアプリケーションをプロビジョニングするのではなく、既存のアプリケーションに接続されます。 新しいアプリケーションをプロビジョニングする場合は、[**同じ ID を持つアプリケーションエントリが既に存在する場合は上書き**する] チェックボックスをオフにします。

**[上書き]** チェックボックスがオフになっていて、Visual Studio が同じアプリケーション ID の uri を持つ既存のアプリケーションを検出した場合、使用する uri に番号を追加することで新しい uri を作成します。 たとえば、プロジェクト名が `Example`で、テキストボックスを空白のままにして、 **[上書き]** チェックボックスをオフにし、Azure AD テナントに URI `https://contoso.onmicrosoft.com/Example`のアプリケーションが既にあるとします。 この場合、新しいアプリケーションは、`https://contoso.onmicrosoft.com/Example_20130619330903`のようなアプリケーション ID URI を使用してプロビジョニングされます。

#### <a name="provisioning-the-application-in-azure-ad"></a>Azure AD でのアプリケーションのプロビジョニング

Azure AD でアプリケーションをプロビジョニングする場合、または既存のアプリケーションにプロジェクトを接続する場合、Visual Studio では、ドメインのグローバル管理者の資格情報が必要です。 **[認証の構成]** ダイアログボックスで **[OK]** をクリックすると、指定したドメインのグローバル管理者のユーザー名とパスワードを入力するように求められます。 その後、 **[新しい ASP.NET プロジェクト]** ダイアログで **[プロジェクトの作成]** をクリックすると、Visual Studio によって Azure AD にアプリケーションがプロビジョニングされます。 このプロセスの一部として、Visual Studio では、作成後1年の有効期限が切れるクライアントシークレット値が web.config ファイルに埋め込まれていることに注意してください。

**クラウドシングル組織**認証を使用するアプリケーションを作成する方法の詳細については、次のリソースを参照してください。

- [Azure 認証](../2012/windows-azure-authentication.md)
- [Azure AD を使用した Web アプリケーションへのサインオンの追加](https://msdn.microsoft.com/library/windowsazure/dn151790.aspx)
- [Azure Active Directory を使った ASP.NET アプリの開発](../../../identity/overview/getting-started/developing-aspnet-apps-with-windows-azure-active-directory.md)
- [Azure AD および Microsoft OWIN コンポーネントを使用した ASP.NET Web API のセキュリティ保護](https://msdn.microsoft.com/magazine/dn463788.aspx)

チュートリアルは Visual Studio 2013 に対してまだ更新されていません。チュートリアルで手動で行うことは、Visual Studio 2013 で自動化されています。

<a id="orgauthmulti"></a>
### <a name="cloud---multi-organization-authentication"></a>クラウド-マルチ組織認証

![複数の組織認証](creating-web-projects-in-visual-studio/_static/image25.png)

複数の Azure AD[テナント](https://technet.microsoft.com/library/jj573650.aspx)で定義されているユーザーアカウントの認証を有効にする場合は、このオプションを選択します。 たとえば、サイトは contoso.com で、contoso.onmicrosoft.com テナントに所属する Contoso 社の従業員と、fabrikam.onmicrosoft.com テナントにある Fabrikam 社の従業員が使用できるようになります。

入力した設定とアプリケーションのプロビジョニング手順は、単一の[組織の認証](#orgauthsingle)に似ています。

**クラウドマルチ組織**認証を使用するアプリケーションを作成する方法の詳細については、次のリソースを参照してください。

- Active Directory チームのブログで[、Azure Active Directory、ASP.NET &amp; Visual Studio と簡単に統合できる Web アプリ](https://blogs.msdn.com/b/active_directory_team_blog/archive/2013/06/26/improved-windows-azure-active-directory-integration-with-asp-net-amp-visual-studio.aspx)。
- [Azure AD チュートリアルを使用したマルチテナント Web アプリケーションの開発](https://msdn.microsoft.com/library/windowsazure/dn151789.aspx)。 このチュートリアルは Visual Studio 2013 に対してまだ更新されていません。チュートリアルで手動で行うことができることの一部は、Visual Studio 2013 で自動化されています。
- [サインインするには、独自の複数の組織 ASP.NET アプリでサインアップする必要があり](http://www.cloudidentity.com/blog/2013/10/26/you-have-to-sign-up-with-your-own-multiple-organizations-asp-net-app-before-you-can-sign-in/)ます。 Vittorio は、マルチ組織認証を使用するプロジェクトを作成するときに発生する一般的な問題を解決する方法を説明するブログです。

<a id="orgauthonprem"></a>
### <a name="on-premises-organizational-authentication"></a>オンプレミスの組織認証

![オンプレミスの組織認証](creating-web-projects-in-visual-studio/_static/image26.png)

Windows Server Active Directory (AD) で定義されているユーザーアカウントの認証を有効にし、Azure AD を使用しないようにする場合は、このオプションを選択します。 このオプションを使用すると、イントラネットサイトまたはインターネットサイトを作成できます。 インターネットサイトの場合は、Active Directory フェデレーションサービス (AD FS) (ADFS) を使用して AD へのアクセスを提供します。 詳細については、Visual Studio 2013 の「[オンプレミスの組織認証オプション (ADFS) と ASP.NET の使用](http://www.cloudidentity.com/blog/2014/02/12/use-the-on-premises-organizational-authentication-option-adfs-with-asp-net-in-visual-studio-2013/)」を参照してください。

イントラネットサイトの場合は、このオプションの代わりに [ [Windows 認証](#winauth)] を選択できます。 Windows 認証オプションでは、メタデータドキュメントの URL を指定する必要はありません。 ただし、Windows 認証では、Active Directory でのアプリケーションアクセスを制御したり、ディレクトリデータを照会したりすることはできません。

#### <a name="on-premises-authority"></a>オンプレミスの機関

メタデータドキュメントを指す URL を入力します。 メタデータドキュメントには、証明機関の座標が含まれています。 アプリケーションはこれらの座標を使用して、web サインオンフローを駆動します。

#### <a name="application-id-uri"></a>アプリケーション ID URI

AD がこのアプリケーションを識別するために使用できる一意の URI を指定するか、空白のままにして Visual Studio で作成できるようにします。

<a id="nextsteps"></a>
## <a name="next-steps"></a>次のステップ:

このドキュメントでは Visual Studio 2013 で新しい ASP.NET web プロジェクトを作成するための基本的なヘルプを提供しました。 For Visual Studio を使用した web 開発の詳細については、「 [https://www.asp.net/visual-studio/](../../index.md)」を参照してください。
