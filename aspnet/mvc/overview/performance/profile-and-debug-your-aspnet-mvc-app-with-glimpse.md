---
uid: mvc/overview/performance/profile-and-debug-your-aspnet-mvc-app-with-glimpse
title: ASP.NET MVC アプリのプロファイルとデバッグMicrosoft Docs
author: Rick-Anderson
description: 活発は、ASP.NET の詳細なパフォーマンス、デバッグ、診断情報を提供するオープンソースの NuGet パッケージのファミリです。
ms.author: riande
ms.date: 03/26/2015
ms.assetid: c205805f-efdd-4fa7-9616-f26eab180611
msc.legacyurl: /mvc/overview/performance/profile-and-debug-your-aspnet-mvc-app-with-glimpse
msc.type: authoredcontent
ms.openlocfilehash: d3689147a3bc3aa1f4180c377d2483a94bdd95a9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78432898"
---
# <a name="profile-and-debug-your-aspnet-mvc-app-with-glimpse"></a>Glimpse を使用して ASP.NET MVC アプリをプロファイルおよびデバッグする

[Rick Anderson](https://twitter.com/RickAndMSFT)

> 活発は、ASP.NET アプリのパフォーマンス、デバッグ、診断に関する詳細な情報を提供するオープンソースの NuGet パッケージのファミリです。 すべてのページの下部に、インストール、軽量、超高速の主要なパフォーマンスメトリックが表示されるのは簡単です。 これにより、サーバーで何が起こっているかを調べる必要がある場合に、アプリにドリルダウンできます。 この情報は、Azure テスト環境など、開発サイクル全体で使用することをお勧めします。 [Fiddler](http://www.telerik.com/fiddler)および[F-12 開発ツール](https://msdn.microsoft.com/library/ie/gg589512(v=vs.85).aspx)にはクライアント側のビューが用意されていますが、サーバーから詳細なビューを提供しています。 このチュートリアルでは、ASP.NET MVC パッケージと EF パッケージを使用する方法に焦点を当てていますが、他にも多くのパッケージが用意されています。 可能な限り、管理に役立つ適切な[ドキュメント](http://getglimpse.com/Docs/)にリンクします。 ここでは、オープンソースプロジェクトです。ソースコードやドキュメントに投稿することもできます。

- [インストールの方法](#ig)
- [Localhost のすべてを有効にする](#eg)
- [[タイムライン] タブ](#Time)
- [モデル バインド](#mb)
- [ルート](#route)
- [Azure での使用](#da)
- [その他のリソース](#addRes)

<a id="ig"></a>
## <a name="installing-glimpse"></a>インストールの方法

NuGet パッケージマネージャーコンソールからインストールするか、 **Nuget パッケージの管理**コンソールからインストールすることができます。 このデモでは、Mvc5 パッケージと EF6 パッケージをインストールします。

![NuGet Dlg からのインストール](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image1.png)

「 *. EF. EF」を検索します。*

![NuGet install dlg からの、EF. EF](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image2.png)

**[インストール済みのパッケージ]** を選択すると、インストールされている依存モジュールを確認できます。

![インストールされたパッケージのインストール (DLg)](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image3.png)

次のコマンドは、パッケージマネージャーコンソールから、MVC5 モジュールと EF6 モジュールをインストールします。

[!code-console[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample1.cmd)]

<a id="eg"></a>
## <a name="enable-glimpse-for-localhost"></a>Localhost のすべてを有効にする

http://localhost:&lt;p ort #&gt;/glimpse.axd に移動し、[を<strong>オン</strong>にする] ボタンをクリックします。

![[すべての axd] ページ](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image4.png)

お気に入りバーが表示されている場合は、そのボタンをドラッグアンドドロップして、bookmarklets として追加することができます。

![Bookmarklets を使用した IE](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image5.png)

これでアプリに移動できるようになり、ページの下部に [**ヘッドアップディスプレイ**(HUD)] が表示されます。

![HUD がある連絡先マネージャーページ](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image6.png)

この[ページ](http://getglimpse.com/Docs/Heads-up-Display)には、上に示したタイミング情報の詳細が表示されます。 HUD に表示される控えめなパフォーマンスデータにより、テストサイクルに到達する前に問題をすぐに通知できます。 右下隅にある &quot;g&quot; をクリックすると、[表示] パネルが表示されます。

![すべてのパネル](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image7.png)

上の図では、[[実行] タブ](http://getglimpse.com/Docs/Execution-Tab)が選択されており、パイプライン内のアクションとフィルターのタイミングの詳細が示されています。 パイプラインのステージ6で、[ストップウォッチフィルタータイマー](http://www.nuget.org/packages/StopWatch/)の開始を確認できます。 ライトウェイトタイマーは便利なプロファイル/タイミングデータを提供できますが、承認とビューの表示に費やされた時間はすべてミスになります。 [ASP.NET MVC アプリのプロファイルと時間については、「Azure に対するすべての方法」を](https://blogs.msdn.com/b/webdev/archive/2014/07/29/profile-and-time-your-asp-net-mvc-app-all-the-way-to-azure.aspx)参照してください。 [[タブ](http://getglimpse.com/Docs/Tabs)] ページには、各タブの詳細情報へのリンクが表示されます。

<a id="Time"></a>
## <a name="the-timeline-tab"></a>[タイムライン] タブ

次のコードを講師コントローラーに変更することで、Tom Dykstra の未解決の[EF 6/MVC 5 チュートリアル](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)を変更しました。

[!code-csharp[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample2.cs?highlight=1,20-31)]

上記のコードでは、クエリ文字列 (`eager`) を渡して、データの一括または明示的な読み込みを制御できます。 次の図では、明示的な読み込みが使用されており、タイミングページには `Index` アクションメソッドに読み込まれた各登録が示されています。

![明示的な読み込み (explicit loading)](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image8.png)

次のコードでは、一括実行が指定されており、`Index` ビューが呼び出された後に各登録がフェッチされます。

![集中指定](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image9.png)

時間セグメントをポイントすると、詳細なタイミング情報を取得できます。

![ホバーして詳細なタイミングを確認する](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image10.png)

<a id="mb"></a>
## <a name="model-binding"></a>モデル バインド

[[モデルのバインド] タブ](http://getglimpse.com/Docs/Model-Binding-Tab)には、フォーム変数がどのようにバインドされているか、また、一部が期待どおりにバインドされていない理由を理解するのに役立つ豊富な情報が表示されます。 次の画像が表示され**ます。** アイコンをクリックすると、その機能の [表示] ヘルプページが表示されます。

![モデルバインドビューを表示します](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image11.png)

<a id="route"></a>
## <a name="routes"></a>ルート

 [ルートの表示] タブは、ルーティングをデバッグして理解するのに役立ちます。 次の図では、製品ルートが選択されています (緑で示されています)。 ルートの制約、区分、データトークン](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image12.png) 選択されている ![製品名も表示されます。 詳細については、「 [ASP.NET MVC 5 で](https://blogs.msdn.com/b/webdev/archive/2013/10/17/attribute-routing-in-asp-net-mvc-5.aspx)の[ルート](http://getglimpse.com/Docs/Routes-Tab)と属性のルーティング」を参照してください。 

<a id="da"></a>
## <a name="using-glimpse-on-azure"></a>Azure での使用

既定のセキュリティポリシーの設定では、ローカルホストからのデータの表示のみが許可されます。 このセキュリティポリシーを変更して、リモートサーバー (Azure 上の web アプリなど) でこのデータを表示できるようにすることができます。 Azure 上のテスト環境の場合は、次のように、web.config ファイルの一番下まで強調表示されているマークを追加して、一目で確認できるよう*にします*。

[!code-xml[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample3.xml?highlight=2-6)]

この変更だけで、リモートサイトでユーザーが自分のデータを見ることができます。 上記のマークアップを発行プロファイルに追加することを検討してください。これにより、発行プロファイル (Azure テストプロファイルなど) を使用する場合にのみ適用されるがデプロイされます。データを制限するために、`canViewGlimpseData` ロールを追加し、このロールのユーザーのみが表示データを表示できるようにします。

*GlimpseSecurityPolicy.cs*ファイルからコメントを削除し、`Administrator` から `canViewGlimpseData` ロールに、 [IsInRole](https://msdn.microsoft.com/library/system.security.principal.iprincipal.isinrole(v=vs.110).aspx)呼び出しを変更します。

[!code-csharp[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample4.cs?highlight=6)]

> [!WARNING]
> セキュリティ-ユーザーによって提供される豊富なデータによって、アプリのセキュリティが公開される可能性があります。 Microsoft では、生産アプリでの使用については、セキュリティ監査を実行していません。

ロールの追加の詳細については、「my [Deploy a Secure ASP.NET MVC 5 web app With Membership, OAuth, and SQL Database To Azure」を](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/)参照してください。

<a id="addRes"></a>
## <a name="additional-resources"></a>その他のリソース

- [メンバーシップ、OAuth、SQL Database がある Secure ASP.NET MVC 5 アプリを Azure にデプロイする](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/)
- [[設定](http://getglimpse.com/Docs/Configuration)]-タブ、ランタイムポリシー、ログ記録などの構成に関するドキュメントページ。
