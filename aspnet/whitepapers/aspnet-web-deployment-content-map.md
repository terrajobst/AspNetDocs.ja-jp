---
uid: whitepapers/aspnet-web-deployment-content-map
title: ASP.NET Web デプロイ-推奨リソース |Microsoft Docs
author: rick-anderson
description: このトピックでは、Visual Studio 2010、Visual Web De... を使用して ASP.NET web アプリケーションを IIS に配置 (発行) する方法に関するドキュメントリソースへのリンクを示します。
ms.author: riande
ms.date: 03/14/2014
ms.assetid: 58b583cd-c4ab-47a3-8527-8c92c298c91f
msc.legacyurl: /whitepapers/aspnet-web-deployment-content-map
msc.type: content
ms.openlocfilehash: 96873c8f2b0ad2415f371aceb651400c801a3338
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78517276"
---
# <a name="aspnet-web-deployment---recommended-resources"></a>ASP.NET Web 配置 - 推奨リソース

> このトピックでは、Visual Studio 2010、Visual Web Developer 2010、およびそれ以降のバージョンを使用して ASP.NET web アプリケーションを IIS に配置 (発行) する方法に関するドキュメントリソースへのリンクを示します。
> 
> 優れたブログ投稿、 [stackoverflow](http://stackoverflow.com)のスレッド、または役に立つその他のリンクがわかっている場合は、リンクを含む[電子メールをお送り](mailto:aspnetue@microsoft.com?subject=Deployment%20Content%20Map)ください。
> 
> > [!NOTE] 
> > 
> > これらのリソースの多くは、 [Visual Studio Web 発行更新プログラム](https://go.microsoft.com/fwlink/?LinkID=208120)の最新リリースをインストールした場合にのみ利用できる配置機能について説明しています。 一部の機能は、Visual Studio 2012 または Visual Studio 2013 でのみ使用できます。

このトピックには、次のセクションが含まれます。

- [Web プロジェクトの配置オプションについて](#understanding)
- [ASP.NET アプリケーションのホスティングプロバイダーの検索](#findinghosting)
- [Visual Studio からの web アプリケーションの配置](#fromvs)
- [Web 配置パッケージを作成してインストールすることによる web アプリケーションの配置](#package)
- [継続的インテグレーション (CI) プロセスを使用した web アプリケーションの展開](#ci)
- [Web.config 変換を使用して、配置時に変換先の web.config ファイルまたは app.config ファイルの設定を変更する](#transforms)
- [デプロイ中に宛先 Web アプリケーションの設定を変更するために Web 配置パラメーターを使用する](#webdeployparms)
- [デプロイ中にアプリケーションがオフラインになっていることを確認する](#appoffline)
- [Web アプリケーションの配置の一部としてデータベースまたはデータベースに対する変更を配置する](#databasewithweb)
- [Web アプリケーションの配置とは別にデータベースを配置する](#databaseseparate)
- [メンバーシップやプロファイルなどの ASP.NET アプリケーションサービスを使用する web アプリケーションのデプロイ](#aspnetmembership)
- [配置のためのプリコンパイル](#precompiling)
- [イントラネット web アプリケーションの展開](#intranet)
- [自動化されていない一般的な展開タスクの自動化](#automating)
- [Web サーバーを構成して、開発者が Web 配置を使用して web アプリケーションを配置できるようにする](#configuringservers)
- [ホスティングプロバイダー用のサーバーの構成](#hostingprovider)
- [デプロイに関する問題のトラブルシューティング](#troubleshooting)
- [特定の展開に関する質問に関するヘルプを表示する](#gettinghelp)
- [その他のリソース](#additional)

<a id="understanding"></a>

## <a name="understanding-deployment-options-for-web-projects"></a>Web プロジェクトの配置オプションについて

- [Visual Studio と ASP.NET (MSDN) の Web 配置の概要](https://msdn.microsoft.com/library/dd394698.aspx)。
- [Windows Azure の Web サイトをデプロイする方法](https://docs.microsoft.com/azure/app-service-web/web-sites-deploy)。 Windows Azure Web サイトに web プロジェクトをデプロイするためのオプションとリンクについて説明します。これには、([ソース管理](../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control.md)から自動化された)[継続的配信](../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery.md)や、Visual Studio の使用が含まれます。
- [Visual Studio 2012 Web 発行の機能強化](../visual-studio/overview/2012/visual-studio-2012-web-publishing-improvements.md)(Scott マン selman によるビデオ)。
- [VS 2010 での Web デプロイの概要](http://vishaljoshi.blogspot.com/2009/09/overview-post-for-web-deployment-in-vs.html)(Vishal Joshi のブログ)。 以前のブログ記事には、Visual studio 2012 に関連する情報が含まれている Visual Studio 2010 リソースの一部がリンクされています。

<a id="findinghosting"></a>

## <a name="finding-hosting-providers-for-an-aspnet-application"></a>ASP.NET アプリケーションのホスティングプロバイダーの検索

- [ASP.NET ホスティング](https://asp.net/hosting)

<a id="fromvs"></a>

## <a name="deploying-a-web-application-from-visual-studio"></a>Visual Studio からの web アプリケーションの配置

- [Windows Azure の Web サイトをデプロイする方法](https://docs.microsoft.com/azure/app-service-web/web-sites-deploy)。 のオプションについて説明し、web プロジェクトを Windows Azure Web サイトに配置するためのリソースへのリンクを示します。 Visual Studio からのデプロイに関するセクションが含まれています。
- [Visual Studio を使用した ASP.NET Web デプロイ](../web-forms/overview/deployment/visual-studio-web-deployment/introduction.md)。 12部構成のチュートリアルシリーズでは、SQL Server データベースを使用して web アプリケーションをデプロイする方法を示します。 データベース配置の場合は、dbDacFx プロバイダーと Entity Framework Code First Migrations の両方を使用します。 また、web.config[ファイルの変換](../web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations.md)、個々の[ファイルの配置](../web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update.md#specificfiles)、[コマンドライン](../web-forms/overview/deployment/visual-studio-web-deployment/command-line-deployment.md)による配置、および[Pubxml ファイルを編集して Visual Studio Web 発行パイプラインをカスタマイズする方法](../web-forms/overview/deployment/visual-studio-web-deployment/deploying-extra-files.md)についても説明します。 Web フォーム、MVC、Web API など、すべての ASP.NET web プロジェクトに適用されます。)
- [方法: Visual studio でワンクリック発行を使用して Web プロジェクトを配置](https://msdn.microsoft.com/library/dd465337.aspx)する (Visual Studio Web 発行ウィザードのリファレンス情報)
- [Visual Studio を使用して SQL Server Compact で ASP.NET Web アプリケーションをデプロイ](../web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-introduction-1-of-12.md)する。 これは、このセクションの上部に記載され**ている Visual Studio を使用し**た、以前のバージョンの ASP.NET Web デプロイです。 SQL Server Compact データベースを展開する方法と、SQL Server Compact から完全なエディションの SQL Server に移行する方法については、主に役立ちます。
- [ストレージテーブル、キュー、および blob (Microsoft Azure サイト) を使用する .Net 多層アプリケーション](https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36)。 5部構成のチュートリアルシリーズでは、MVC プロジェクトを作成して Windows Azure クラウドサービスにデプロイする方法を示します。

<a id="package"></a>
## <a name="deploying-a-web-application-by-creating-and-installing-a-web-deployment-package"></a>Web 配置パッケージを作成してインストールすることによる web アプリケーションの配置

- [方法: Visual Studio で Web 配置パッケージを作成](https://msdn.microsoft.com/library/dd465323.aspx)する (MSDN)
- [方法: Visual Studio によって作成された .Deploy ファイルを使用して配置パッケージをインストール](https://msdn.microsoft.com/library/ff356104.aspx)する (MSDN)
- [Web 配置パッケージを使用して、dev box およびサードパーティのホスト](http://sedodream.com/2011/11/08/UsingAWebDeployPackageToDeployToIISOnTheDevBoxAndToAThirdPartyHost.aspx)(作成者 Hashimi のブログ) に IIS をデプロイします。 Iis マネージャーを使用して、ローカルコンピューター上の IIS およびリモート管理用の IIS マネージャーをサポートするホスティング会社に展開パッケージをインストールする方法。
- Visual Studio 2010 (IIS.NET Web サイト)[からの Web 配置パッケージのビルド](https://www.iis.net/learn/publish/using-web-deploy/building-a-web-deploy-package-from-visual-studio-2010)。 コマンドラインパッケージの作成とインストールの手順について説明します。
- [任意の場所に発行](http://sedodream.com/2012/03/14/PackageWebUpdatedAndVideoBelow.aspx)した後のパッケージ (作成者 Hashimi のブログ)。 では、複数の変換先環境の Web.config ファイルを変換するプロセスを自動化する NuGet パッケージが導入されています。これにより、1つのパッケージを複数のサーバーに配置できます。 作成者 Hashimi による[Packageweb ビデオ](https://www.youtube.com/watch?v=-LvUJFI8CzM)も参照してください。

次のセクションも参照してください。

<a id="ci"></a>

## <a name="deploying-a-web-application-using-a-continuous-integration-ci-process"></a>継続的インテグレーション (CI) プロセスを使用した web アプリケーションの展開

- [継続的インテグレーションと継続的デリバリー (Windows Azure を使用した実際のクラウドアプリの構築)。](../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery.md) 継続的インテグレーションと継続的デリバリーを紹介する電子書籍の章。
- [Windows Azure の Web サイトをデプロイする方法](https://docs.microsoft.com/azure/app-service-web/web-sites-deploy)。 Windows Azure Web サイトに web プロジェクトを配置するためのオプションとリソースへのリンクについて説明します。 ソース管理からのデプロイの自動化に関するセクションが含まれています。
- [エンタープライズシナリオでの Web アプリケーションの展開](../web-forms/overview/deployment/deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md)。 40-パートチュートリアルシリーズでは、Visual Studio 2010 と Team Foundation Server 2010 を使用して CI プロセスでのデプロイを自動化する方法について説明します。
- [Microsoft Build Engine の内部: 作成者 Hashimi およびウィリアム Bartholomew による MSBuild と Team Foundation ビルドの使用](http://msbuildbook.com)。 これは web リソースではなく、書籍ですが、継続的な統合シナリオのために MSBuild を構成する方法について学習するための必須ガイドです。
- [MSBuild 拡張パック](https://github.com/mikefourie/MSBuildExtensionPack)。 展開タスクが含まれます。
- [Team Foundation ビルドのカスタマイズガイド](https://aka.ms/vsarsolutions)。 Team Foundation Server のセットアップに関する ALM Rangers のドキュメントでは、web デプロイについて説明し、チュートリアルとビデオが含まれています。
- [CI サーバーからの SLOWCHEETAH XML 変換](http://sedodream.com/2011/12/12/SlowCheetahXMLTransformsFromACIServer.aspx)(作成者 Hashimi のブログ)。 SlowCheetah を使用する方法について説明します。これは、app.config やその他の XML ファイルを変換するための Visual Studio アドインです。

このページの「[デプロイ中にアプリケーションがオフラインになっていることを確認する](aspnet-web-deployment-content-map.md#appoffline)」も参照してください。

<a id="transforms"></a>

## <a name="using-webconfig-transformations-to-change-settings-in-the-destination-webconfig-file-or-appconfig-file-during-deployment"></a>Web.config 変換を使用して、配置時に変換先の web.config ファイルまたは app.config ファイルの設定を変更する

- Web.config[ファイル変換](../web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations.md)。
- [Visual Studio を使用した Web プロジェクト配置の Web.config 変換構文](https://msdn.microsoft.com/library/dd465326.aspx)(MSDN)。
- [Web ツール 2012.2-web.config の変換](https://www.youtube.com/watch?v=HdPK8mxpKEI)(作成者 Hashimi による YouTube ビデオ)。 Web.config の変換を設定およびプレビューする方法を示します。
- [Web.config 変換を無効に操作方法ますか?](https://msdn.microsoft.com/library/ee942158.aspx#disable_web_config_transformation) (MSDN)。
- [Web.config 変換ではなく Web 配置パラメーターを使用する必要があるのはどのような場合ですか?](https://msdn.microsoft.com/library/ee942158.aspx#web_deploy_parameters) (MSDN)。
- [Codeplex.com でリリースされた Xdt (XML ドキュメント変換)](https://blogs.msdn.com/b/webdev/archive/2013/04/23/xdt-xml-document-transform-released-on-codeplex-com.aspx) (.Net Web 開発およびツールのブログ)。 Web.config ファイル変換エンジンのソースコードの可用性を発表し、それを使用するツールをいくつか示します。
- [Windows Azure websites: アプリケーション文字列と接続文字列のしくみ](https://blogs.msdn.com/b/windowsazure/archive/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work.aspx)(Microsoft Azure ブログ)。 移行先の環境が Windows Azure Websites で、`appSettings` または `connectionStrings`を変換する場合は、web.config 変換の代替手段となります。

<a id="webdeployparms"></a>

## <a name="using-web-deploy-parameters-to-change-settings-in-the-destination-web-application-during-deployment"></a>デプロイ中に宛先 Web アプリケーションの設定を変更するために Web 配置パラメーターを使用する

- [方法: Web 配置パッケージで Web 配置パラメーターを使用](https://msdn.microsoft.com/library/ff398068.aspx)する (MSDN)
- [Msdeploy.exe: 発行プロファイルに基づいて発行時にアプリ設定を更新する方法](http://sedodream.com/2013/03/02/MSDeployHowToUpdateAppSettingsOnPublishBasedOnThePublishProfile.aspx)(作成者 Hashimi のブログ)。 Web deploy パラメーターを Visual Studio の発行プロファイルに統合する方法について説明します。
- [Web 配置のパラメーター](https://www.iis.net/learn/publish/using-web-deploy/web-deploy-parameterization)化 (IIS.NET Web サイト)。
- [アクションのパラメーター](http://vishaljoshi.blogspot.com/2010/07/web-deploy-parameterization-in-action.html)化 (Vishal Joshi のブログ) を Web 配置します。
- [Web 配置パラメーター](http://vishaljoshi.blogspot.com/2010/06/parameterization-vs-webconfig.html)化と web.config 変換 (Vishal Joshi のブログ)。
- [Windows Azure websites: アプリケーション文字列と接続文字列のしくみ](https://blogs.msdn.com/b/windowsazure/archive/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work.aspx)(Microsoft Azure ブログ)。 対象となる環境が Windows Azure Websites で、`appSettings` または `connectionStrings`をパラメーター化する場合は、Web デプロイパラメーターの代わりに使用できます。

<a id="appoffline"></a>

## <a name="making-sure-an-application-is-off-line-during-deployment"></a>デプロイ中にアプリケーションがオフラインになっていることを確認する

- [Visual Studio を使用した ASP.NET Web 配置: コード更新の配置](../web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update.md)。 「**デプロイ中にアプリケーションをオフライン**にする」セクションを参照してください。
- [発行前にアプリケーションをオフラインにする](https://www.iis.net/learn/publish/deploying-application-packages/taking-an-application-offline-before-publishing)(IIS.net サイト)。 Web 配置3.0 に組み込まれている機能について説明します。これにより、アプリ\_オフライン .htm ファイルの処理が自動化されます。 この機能は、カスタムアプリ\_のオフライン .htm ファイルでは機能しません。
- [発行中に web アプリをオフラインにする方法](http://sedodream.com/2012/01/08/HowToTakeYourWebAppOfflineDuringPublishing.aspx)(作成者 Hashimi のブログ)。 カスタムアプリ\_オフライン .htm ファイルを使用するプロセスを自動化する方法について説明します。
- [オフラインおよび usechecksum の web 発行更新プログラム](https://blogs.msdn.com/b/webdev/archive/2013/10/30/web-publishing-updates-for-app-offline-and-usechecksum.aspx)(Microsoft web 開発ブログ)。 アプリ\_のオフライン .htm ファイルの使用を自動化するもう1つのオプション。
- [Web 配置 3.5 RTW](https://blogs.iis.net/msdeploy/archive/2013/07/09/webdeploy-3-5-rtw.aspx) (IIS.net サイト)。 カスタムアプリ\_オフライン .htm ファイルの Web 配置3.5 の新機能。

<a id="databasewithweb"></a>

## <a name="deploying-a-database-or-changes-to-a-database-as-part-of-web-application-deployment"></a>Web アプリケーションの配置の一部としてデータベースまたはデータベースに対する変更を配置する

- [Visual Studio でのデータベース配置の構成](https://msdn.microsoft.com/library/dd394698.aspx#dbdeployment)(MSDN) Web プロジェクトを使用してデータベースを配置するためのオプションの概要について説明します。
- [Visual Studio を使用した ASP.NET Web デプロイ](../web-forms/overview/deployment/visual-studio-web-deployment/introduction.md)。 12部構成のチュートリアルシリーズでは、dbDacFx プロバイダーと Entity Framework Code First Migrations を使用したデータベース配置について説明します。
- [方法: Visual Studio でワンクリック発行を使用して Web プロジェクトを配置](https://msdn.microsoft.com/library/dd465337.aspx)する (MSDN)
- [メンバーシップ、OAuth、SQL Database を持つ Secure ASP.NET MVC 5 アプリを Windows Azure の Web サイトにデプロイ](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)します。 メンバーシップとアプリケーションデータの両方に単一の SQL Server データベースを使用するアプリケーションを構築してデプロイする、長いチュートリアルです。
- [Visual Studio を使用して SQL Server Compact で ASP.NET Web アプリケーションをデプロイ](../web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-introduction-1-of-12.md)する。 12部構成のチュートリアルシリーズでは、SQL Server Compact データベースを展開する方法と、SQL Server Compact から SQL Server の完全版に移行する方法について説明します。

「Web 配置パッケージを作成およびインストールする」および「継続的インテグレーション (CI) プロセスを使用して web アプリケーションをデプロイする」を参照してください。

<a id="databaseseparate"></a>

## <a name="deploying-a-database-separately-from-web-application-deployment"></a>Web アプリケーションの配置とは別にデータベースを配置する

- [SQL Server Data Tools](https://msdn.microsoft.com/library/hh272686(v=vs.103).aspx) (MSDN)。
- [SQL Server データベースプロジェクトにデータを含める](https://blogs.msdn.com/b/ssdt/archive/2012/02/02/including-data-in-an-sql-server-database-project.aspx)(SQL Server Data Tools チームのブログ)。 データベースを配置するときにスキーマとデータの両方を配置する方法。
- [Windows Azure にデータベースを配置する方法](https://docs.microsoft.com/azure/sql-database/sql-database-cloud-migrate)(Microsoft Azure サイト)
- [Windows Azure SQL Database (旧称 SQL Azure) へのデータベースの移行](https://msdn.microsoft.com/library/windowsazure/ee730904.aspx)(MSDN)。
- [SSDT を使用してデータベースを SQL Azure に移行する](https://blogs.msdn.com/b/ssdt/archive/2012/04/19/migrating-a-database-to-sql-azure-using-ssdt.aspx)(SQL Server Data Tools チームのブログ)。
- [データ中心のアプリケーションを Windows Azure に移行する](https://msdn.microsoft.com/library/jj156154.aspx)(MSDN)。
- [Windows Azure SQL Database (MSDN) への SQL Server データベースの移行](https://msdn.microsoft.com/library/windowsazure/jj156160.aspx)。

<a id="aspnetmembership"></a>

## <a name="deploying-a-web-application-that-uses-aspnet-application-services-such-as-membership-and-profiling"></a>メンバーシップやプロファイルなどの ASP.NET アプリケーションサービスを使用する web アプリケーションのデプロイ

- [メンバーシップ、OAuth、SQL Database を持つ Secure ASP.NET MVC 5 アプリを Windows Azure の Web サイトにデプロイ](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)します。 メンバーシップとアプリケーションデータの両方に単一の SQL Server データベースを使用するアプリケーションを構築してデプロイする、長いチュートリアルです。
- [ASP.NET Identity](https://asp.net/identity/)。 ASP.NET Identity のリソース。
- [Visual Studio を使用した ASP.NET Web デプロイ](../web-forms/overview/deployment/visual-studio-web-deployment/introduction.md)。 12部構成のチュートリアルシリーズでは、ASP.NET メンバーシップデータベースをデプロイする方法を示します。
- [アプリケーションサービスを使用する Web サイトを構成](../web-forms/overview/older-versions-getting-started/deploying-web-site-projects/configuring-a-website-that-uses-application-services-cs.md)する。 Web サイトプロジェクトの場合は、web アプリケーションプロジェクトにも関連します。
- [運用 Web サイトのユーザーとロール](../web-forms/overview/older-versions-getting-started/deploying-web-site-projects/users-and-roles-on-the-production-website-cs.md)。 Web サイトプロジェクトの場合は、web アプリケーションプロジェクトにも関連します。

<a id="precompiling"></a>

## <a name="precompiling-for-deployment"></a>配置のためのプリコンパイル

- [ASP.NET Web アプリケーションプロジェクトのプリコンパイルの概要](https://msdn.microsoft.com/library/aa983464.aspx)(MSDN)。
- [[Web のパッケージ化/発行] タブ、[プロジェクトのプロパティ]](https://msdn.microsoft.com/library/dd410108.aspx) (MSDN)。
- [[プリコンパイルの詳細設定] ダイアログボックス](https://msdn.microsoft.com/library/hh475319.aspx)(MSDN)。

<a id="intranet"></a>

## <a name="deploying-an-intranet-web-application"></a>イントラネット web アプリケーションの展開

- [Visual Studio 2013 の ASP.NET でオンプレミスの組織認証オプション (ADFS) を使用](http://www.cloudidentity.com/blog/2014/02/12/use-the-on-premises-organizational-authentication-option-adfs-with-asp-net-in-visual-studio-2013/)します (ブログ Vittorio による)。
- [ASP.NET MVC (MSDN) を使用してイントラネットサイトを作成する方法](https://msdn.microsoft.com/library/gg703322(VS.98).aspx)。 以前の Visual Studio 2010 のチュートリアル書き込まれるは、Visual Studio 2013 で導入されたイントラネットプロジェクトテンプレートの主要な変更を反映していません。

<a id="automating"></a>

## <a name="automating-common-deployment-tasks-that-are-not-automated-out-of-the-box"></a>自動化されていない一般的な展開タスクの自動化

- [Visual Studio を使用した ASP.NET Web 配置: 追加ファイルの配置](../web-forms/overview/deployment/visual-studio-web-deployment/deploying-extra-files.md)。
- [Web 発行のフォルダーのアクセス許可を設定](http://sedodream.com/2011/11/08/SettingFolderPermissionsOnWebPublish.aspx)する (作成者 Hashimi のブログ)。
- [ターゲットファイルを拡張して web プロジェクトパッケージのレジストリ設定を含める方法](https://blogs.msdn.com/webdevtools/archive/2010/02/09/how-to-extend-target-file-to-include-registry-settings-for-web-project-package.aspx)(Web 開発ツールのブログ)。
- [XML (web.config) 変換の拡張](http://sedodream.com/2010/09/09/ExtendingXMLWebconfigConfigTransformation.aspx)(作成者 Hashimi のブログ)。 カスタム XDT 変換を作成する方法について説明します。
- [Web 配置ツール (msdeploy.exe) カスタムプロバイダーは 1](http://sedodream.com/2010/03/11/WebDeploymentToolMSDeployCustomProviderTake1.aspx) (作成者 Hashimi のブログ) を受け取ります。 Web 配置カスタムプロバイダーを作成する方法について説明します。
- [COM コンポーネントをパッケージ化して配置する方法](https://blogs.msdn.com/webdevtools/archive/2010/03/03/how-to-package-and-deploy-com-component.aspx)(Web 開発ツールのブログ)。
- [.Net アセンブリのパッケージ化方法](https://blogs.msdn.com/webdevtools/archive/2010/02/19/how-to-package-com-component.aspx)(Web 開発ツールブログ)。 アセンブリを GAC に展開する方法。
- [すべてのものをスクリプト化-IIS、Web 配置などの他の情報を使用して、Web サーバーの Windows AZURE VM を初期化](http://www.tugberkugurlu.com/archive/script-out-everything-initialize-your-windows-azure-vm-for-your-web-server-with-iis-web-deploy-and-other-stuff)します (tugのブログ)。

<a id="configuringservers"></a>

## <a name="configuring-web-servers-so-that-developers-can-deploy-web-applications-to-them-using-web-deploy"></a>Web サーバーを構成して、開発者が Web 配置を使用して web アプリケーションを配置できるようにする

- [管理者および管理者以外の展開用の Web 配置のインストールと構成](https://www.iis.net/learn/install/installing-publishing-technologies/installing-and-configuring-web-deploy)(IIS.net サイト)。

<a id="hostingprovider"></a>

## <a name="configuring-servers-for-a-hosting-provider"></a>ホスティングプロバイダー用のサーバーの構成

- [Microsoft ASP.NET 4 ホスティング展開ガイド](https://go.microsoft.com/fwlink/?LinkId=191365)(Microsoft ダウンロードセンター)。
- [プロファイル XML ファイル](https://www.iis.net/learn/web-hosting/joining-the-web-hosting-gallery/generate-a-profile-xml-file)(IIS.net サイト) を生成します。

<a id="troubleshooting"></a>

## <a name="troubleshooting-deployment-problems"></a>デプロイに関する問題のトラブルシューティング

- [Visual Studio での Windows Azure Web サイトのトラブルシューティング](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio)(Microsoft Azure サイト)。
- [Visual Studio を使用した ASP.NET Web 配置: トラブルシューティング](../web-forms/overview/deployment/visual-studio-web-deployment/troubleshooting.md)。
- [Web 配置に関する一般的な問題のトラブルシューティング](https://www.iis.net/learn/publish/troubleshooting-web-deploy/troubleshooting-common-problems-with-web-deploy)。
- [Web 配置のエラーコード](https://www.iis.net/learn/publish/troubleshooting-web-deploy/web-deploy-error-codes)(IIS.net サイト)。
- [Visual Studio と ASP.NET (MSDN) の Web 配置に関する FAQ](https://msdn.microsoft.com/library/ee942158.aspx) 。
- [IIS と ASP.NET 開発サーバーの主要な相違点](../web-forms/overview/older-versions-getting-started/deploying-web-site-projects/core-differences-between-iis-and-the-asp-net-development-server-cs.md)。
- [開発と運用の間の一般的な構成の違い](../web-forms/overview/older-versions-getting-started/deploying-web-site-projects/common-configuration-differences-between-development-and-production-cs.md)。
- [中程度の信頼で ASP.NET アプリケーションをホスト](http://www.4guysfromrolla.com/articles/100307-1.aspx)しています (Rolla サイトから4人)。

<a id="gettinghelp"></a>

## <a name="getting-help-with-a-specific-deployment-question"></a>特定の展開に関する質問に関するヘルプを表示する

- [ASP.NET の構成とデプロイのフォーラム](https://forums.asp.net/26.aspx/1?Configuration and Deployment)。
- [StackOverflow.com](http://www.StackOverflow.com)。

<a id="additional"></a>

## <a name="additional-resources"></a>その他のリソース

このセクションでは、Visual Studio と IIS の配置ツールの使用方法について詳しく学習するのに役立つその他のリソースへのリンクを示します。

次のブログには、多くの場合、Visual Studio の web 配置に関する情報が含まれています。

- [Microsoft ブログの Web 開発ツール](https://blogs.msdn.com/b/webdevtools/)。
- [作成者 Hashimi のブログ](http://www.sedodream.com/)。

次のリソースは、Visual Studio が Web アプリケーションプロジェクトの配置タスクを実行するために使用する IIS フレームワーク Web 配置に関するドキュメントを提供します。 Web 配置について質問するには、IIS.net web サイトの[Web 配置ツールフォーラム](https://go.microsoft.com/fwlink/?LinkId=149411)をご覧ください。

- [Web 配置の概要](https://www.iis.net/learn/publish/using-web-deploy/introduction-to-web-deploy)。
- [Web 配置のインストールと構成](https://www.iis.net/learn/install/installing-publishing-technologies/installing-and-configuring-web-deploy)。
- [Web 配置セットアップを自動化するための PowerShell スクリプト](https://www.iis.net/learn/publish/using-web-deploy/powershell-scripts-for-automating-web-deploy-setup)。
- [Web デプロイ ツール](https://go.microsoft.com/fwlink/?LinkId=151481)。 TechNet サイトの Web 配置ドキュメントについては、トップレベルの目次ノードを参照してください。 役に立つ参照情報が含まれていますが、TechNet ページのほとんどは何年も更新されていません。
- [Microsoft. 配置名前空間](https://go.microsoft.com/fwlink/?LinkId=148630)。 バージョン1.0 以降、API ドキュメントは更新されていません。
- [Microsoft Web Deployment チームのブログ](https://blogs.iis.net/msdeploy/default.aspx)。
- [IIS.net web サイトの [発行] タブ](https://www.iis.net/learn/publish)。
