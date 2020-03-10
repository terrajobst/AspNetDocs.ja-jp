---
uid: mvc/overview/older-versions-1/deployment/using-asp-net-mvc-with-different-versions-of-iis-cs
title: ASP.NET MVC を使用して、さまざまなバージョンの IIS (C#) |Microsoft Docs
author: microsoft
description: このチュートリアルでは、さまざまなバージョンのインターネットインフォメーションサービスで ASP.NET MVC と URL ルーティングを使用する方法について説明します。 さまざまな戦略を学習できます...
ms.author: riande
ms.date: 08/19/2008
ms.assetid: b0cf4a34-2c1d-4717-bb54-ff029e722990
msc.legacyurl: /mvc/overview/older-versions-1/deployment/using-asp-net-mvc-with-different-versions-of-iis-cs
msc.type: authoredcontent
ms.openlocfilehash: 3b0a9509c0600f3598fd1218a7b383430548d4c0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486526"
---
# <a name="using-aspnet-mvc-with-different-versions-of-iis-c"></a>ASP.NET MVC を使用して、さまざまなバージョンの IIS (C#)

[Microsoft](https://github.com/microsoft)

> このチュートリアルでは、さまざまなバージョンのインターネットインフォメーションサービスで ASP.NET MVC と URL ルーティングを使用する方法について説明します。 Iis 7.0 (クラシックモード)、IIS 6.0、およびそれより前のバージョンの IIS で ASP.NET MVC を使用するためのさまざまな方法について説明します。

ASP.NET MVC フレームワークは、ASP.NET ルーティングに依存して、ブラウザー要求をコントローラーアクションにルーティングします。 ASP.NET ルーティングを活用するために、web サーバーで追加の構成手順を実行することが必要になる場合があります。 これはすべて、アプリケーションのバージョンインターネットインフォメーションサービス (IIS) と要求処理モードによって異なります。

IIS のさまざまなバージョンの概要を次に示します。

- IIS 7.0 (統合モード)-ASP.NET ルーティングを使用するために特別な構成は必要ありません。
- IIS 7.0 (クラシックモード)-ASP.NET ルーティングを使用するには、特別な構成を行う必要があります。
- IIS 6.0 以下-ASP.NET ルーティングを使用するには、特別な構成を行う必要があります。

IIS の最新バージョンは、バージョン 7.5 (Win7) です。 Iis 7 の iis 7 は、Windows Server 2008 および VISTA/SP1 以降に含まれています。 また、Home Basic 以外のすべてのバージョンの Vista オペレーティングシステムに IIS 7.0 をインストールすることもできます (「 [https://technet.microsoft.com/library/cc731179%28WS.10%29.aspx](https://technet.microsoft.com/library/cc731179%28WS.10%29.aspx)」を参照してください)。

IIS 7.0 は、要求を処理する2つのモードをサポートしています。 統合モードまたはクラシックモードを使用できます。 統合モードで IIS 7.0 を使用する場合は、特別な構成手順を実行する必要はありません。 ただし、クラシックモードで IIS 7.0 を使用する場合は、追加の構成を行う必要があります。

Microsoft Windows Server 2003 には、IIS 6.0 が含まれています。 Windows Server 2003 オペレーティングシステムを使用している場合は、iis 6.0 を IIS 7.0 にアップグレードすることはできません。 IIS 6.0 を使用する場合は、追加の構成手順を実行する必要があります。

Microsoft Windows XP Professional には IIS 5.1 が含まれています。 IIS 5.1 を使用する場合は、追加の構成手順を実行する必要があります。

最後に、Microsoft Windows 2000 および Microsoft Windows 2000 Professional には IIS 5.0 が含まれています。 IIS 5.0 を使用する場合は、追加の構成手順を実行する必要があります。

## <a name="integrated-versus-classic-mode"></a>統合モードとクラシックモード

IIS 7.0 では、統合とクラシックの2つの異なる要求処理モードを使用して要求を処理できます。 統合モードでは、パフォーマンスが向上し、機能も強化されます。 クラシックモードは、以前のバージョンの IIS との下位互換性のために用意されています。

要求処理モードは、アプリケーションプールによって決定されます。 特定の web アプリケーションによって使用されている処理モードを特定するには、アプリケーションに関連付けられているアプリケーションプールを決定します。 次の手順に従います。

1. インターネットインフォメーションサービスマネージャーを起動する
2. [接続] ウィンドウで、アプリケーションを選択します。
3. アクション] ウィンドウで、 **[基本設定]** リンクをクリックして [アプリケーションの編集 ダイアログボックスを開きます (図1を参照)。
4. 選択したアプリケーションプールをメモしておきます。

既定では、IIS は、 **DefaultAppPool**と**クラシック .net AppPool**という2つのアプリケーションプールをサポートするように構成されています。 DefaultAppPool が選択されている場合、アプリケーションは統合要求処理モードで実行されています。 クラシック .NET AppPool が選択されている場合は、アプリケーションがクラシック要求処理モードで実行されています。

[[新しいプロジェクト] ダイアログボックスの ![](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image1.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image1.png)

**図 1**: 要求処理モードの検出 ([クリックすると、フルサイズの画像が表示](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image2.png)されます)

[アプリケーションの編集] ダイアログボックスで要求処理モードを変更できることに注意してください。 [選択] ボタンをクリックし、アプリケーションに関連付けられているアプリケーションプールを変更します。 ASP.NET アプリケーションをクラシックモードから統合モードに変更するときは、互換性の問題があることに注意してください。 詳細については、次の記事を参照してください。

- Windows Vista および Windows Server 2008 で ASP.NET 1.1 を IIS 7.0 にアップグレードする-- [https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008)
- ASP.NET と IIS 7.0 の統合- [https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis)

ASP.NET アプリケーションで DefaultAppPool が使用されている場合、ASP.NET Routing (したがって ASP.NET MVC) を機能させるために追加の手順を実行する必要はありません。 ただし、ASP.NET アプリケーションが従来の .NET AppPool を使用するように構成されている場合は、次の作業を行う必要があります。

## <a name="using-aspnet-mvc-with-older-versions-of-iis"></a>以前のバージョンの IIS での ASP.NET MVC の使用

Iis 7.0 よりも前のバージョンの IIS で ASP.NET MVC を使用する必要がある場合、またはクラシックモードで IIS 7.0 を使用する必要がある場合は、2つのオプションがあります。 まず、ファイル拡張子を使用するようにルートテーブルを変更できます。 たとえば、/Store.aspx/Details. のような URL を要求するのではなく、URL を要求します。

2つ目の方法は、*ワイルドカードスクリプトマップ*と呼ばれるものを作成することです。 ワイルドカードスクリプトマップを使用すると、すべての要求を ASP.NET フレームワークにマップできます。

Web サーバーにアクセスできない場合 (たとえば、ASP.NET MVC アプリケーションがインターネットサービスプロバイダーによってホストされている場合) は、最初のオプションを使用する必要があります。 Url の外観を変更したくない場合に、web サーバーにアクセスできるようにするには、2番目のオプションを使用します。

各オプションについては、次のセクションで詳しく説明します。

## <a name="adding-extensions-to-the-route-table"></a>ルートテーブルへの拡張機能の追加

以前のバージョンの IIS で動作するように ASP.NET ルーティングを取得する最も簡単な方法は、global.asax ファイルのルートテーブルを変更することです。 リスト1の既定および変更されていない global.asax ファイルは、既定のルートという名前のルートを1つ構成します。

**リスト 1-global.asax (変更なし)**

[!code-csharp[Main](using-asp-net-mvc-with-different-versions-of-iis-cs/samples/sample1.cs)]

リスト1で構成された既定のルートでは、次のような Url をルーティングできます。

/Home/Index

/Product/Details/3

/Product

残念ながら、以前のバージョンの IIS では、これらの要求を ASP.NET フレームワークに渡すことはできません。 そのため、これらの要求はコントローラーにルーティングされません。 たとえば、URL/Home/Index にブラウザーの要求を行うと、図2のエラーページが表示されます。

[[新しいプロジェクト] ダイアログボックスの ![](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image2.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image3.png)

**図 2**: 404 が見つからないというエラーを受信[する (クリックすると、フルサイズの画像が表示](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image4.png)されます)

以前のバージョンの IIS では、特定の要求が ASP.NET フレームワークにのみマップされています。 要求は、正しいファイル拡張子を持つ URL に対してである必要があります。 たとえば、/SomePage.aspx の要求は ASP.NET フレームワークにマップされます。 ただし、/SomePage.htm の要求ではありません。

そのため、ASP.NET ルーティングを機能させるには、ASP.NET フレームワークにマップされているファイル拡張子が含まれるように、既定のルートを変更する必要があります。

これを行うには、`registermvc.wsf`という名前のスクリプトを使用します。 これは `C:\Program Files\Microsoft ASP.NET\ASP.NET MVC\Scripts`の ASP.NET MVC 1 リリースに含まれていましたが、ASP.NET 2 の時点では、このスクリプトは ASP.NET フューチャに移動され、 [http://aspnet.codeplex.com/releases/view/39978](http://aspnet.codeplex.com/releases/view/39978)で入手できます。

このスクリプトを実行すると、IIS に新しい mvc 拡張機能が登録されます。 Mvc 拡張機能を登録した後で、グローバルな global.asax ファイル内のルートを変更して、ルートが mvc 拡張機能を使用するようにすることができます。

リスト2の変更された global.asax ファイルは、以前のバージョンの IIS で動作します。

**リスト 2-global.asax (拡張機能を使用して変更)**

[!code-csharp[Main](using-asp-net-mvc-with-different-versions-of-iis-cs/samples/sample2.cs)]

**重要**: global.asax ファイルを変更した後、ASP.NET MVC アプリケーションを再度ビルドしてください。

リスト2の global.asax ファイルには、2つの重要な変更があります。 Global.asax に2つのルートが定義されました。 既定のルートの URL パターン (最初のルート) は次のようになります。

{controller}.mvc/{action}/{id}

Mvc 拡張機能を追加すると、ASP.NET ルーティングモジュールによってインターセプトされるファイルの種類が変更されます。 この変更により、ASP.NET MVC アプリケーションは次のような要求をルーティングするようになりました。

/Home.mvc/Index/

/Product.mvc/Details/3

/Product.mvc/

ルートルートの2番目のルートは [新規] です。 ルートルートのこの URL パターンは空の文字列です。 このルートは、アプリケーションのルートに対して行われた要求を照合するために必要です。 たとえば、ルートルートは次のような要求と一致します。

[http://www.YourApplication.com/](http://www.YourApplication.com/)

ルートテーブルにこれらの変更を加えた後、アプリケーション内のすべてのリンクがこれらの新しい URL パターンと互換性があることを確認する必要があります。 つまり、すべてのリンクに、mvc 拡張子が含まれていることを確認します。 Html.actionlink () ヘルパーメソッドを使用してリンクを生成する場合は、変更を加える必要はありません。

Registermvc.wcf スクリプトを使用する代わりに IIS を手動で ASP.NET フレームワークにマップされている新しい拡張機能を追加できます。 新しい拡張機能を自分で追加する場合は、[**ファイルが存在することを確認**する] チェックボックスがオンになっていないことを確認してください。

## <a name="hosted-server"></a>ホステッドサーバー

Web サーバーにアクセスすることは常に許可されていません。 たとえば、インターネットホスティングプロバイダーを使用して ASP.NET MVC アプリケーションをホストしている場合、必ずしも IIS にアクセスできるとは限りません。

その場合は、ASP.NET フレームワークにマップされている既存のファイル拡張子の1つを使用する必要があります。 ASP.NET にマップされたファイル拡張子の例としては、.aspx、axd、および .ashx 拡張子があります。

たとえば、リスト3の変更された global.asax ファイルは、mvc 拡張機能ではなく .aspx 拡張子を使用します。

**リスト 3-global.asax (.aspx 拡張子を使用して変更)**

[!code-csharp[Main](using-asp-net-mvc-with-different-versions-of-iis-cs/samples/sample3.cs)]

リスト3の global.asax ファイルは、以前の global.asax ファイルとまったく同じです。ただし、mvc 拡張機能ではなく .aspx 拡張子を使用する点が異なります。 .Aspx 拡張子を使用するために、リモート web サーバーでセットアップを実行する必要はありません。

## <a name="creating-a-wildcard-script-map"></a>ワイルドカードスクリプトマップの作成

ASP.NET MVC アプリケーションの Url を変更する必要がなく、web サーバーにアクセスできる場合は、追加のオプションがあります。 Web サーバーへのすべての要求を ASP.NET フレームワークにマップするワイルドカードスクリプトマップを作成できます。 このようにして、既定の ASP.NET MVC ルートテーブルを IIS 7.0 (クラシックモード) または IIS 6.0 と共に使用できます。

このオプションを使用すると、web サーバーに対して行われたすべての要求が IIS によってインターセプトされます。 これには、イメージ、従来の ASP ページ、HTML ページの要求が含まれます。 このため、ASP.NET に対してワイルドカードスクリプトマップを有効にすると、パフォーマンスに影響があります。

IIS 7.0 に対してワイルドカードスクリプトマップを有効にする方法を次に示します。

1. [接続] ウィンドウでアプリケーションを選択します。
2. [**機能**ビュー] が選択されていることを確認します。
3. **[ハンドラーマッピング]** ボタンをダブルクリックします。
4. **[ワイルドカードスクリプトマップの追加]** リンクをクリックします (図3を参照)。
5. Aspnet\_isapi .dll ファイルへのパスを入力します (このパスは Pageハンドラファクトリスクリプトマップからコピーできます)。
6. 名前を「MVC」と入力します。
7. **[OK]** ボタンをクリックします。

[[新しいプロジェクト] ダイアログボックスの ![](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image3.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image5.png)

**図 3**: IIS 7.0 を使用したワイルドカードスクリプトマップの作成 ([クリックすると、フルサイズの画像が表示](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image6.png)される)

IIS 6.0 でワイルドカードスクリプトマップを作成するには、次の手順に従います。

1. Web サイトを右クリックし、[プロパティ] を選択します。
2. **[ホームディレクトリ]** タブを選択します。
3. **[構成]** ボタンをクリックします。
4. **[マッピング]** タブを選択します。
5. **[挿入]** ボタンをクリックします (図4を参照)。
6. Aspnet\_のパスを実行可能フィールドに貼り付けます (.aspx ファイルのスクリプトマップからこのパスをコピーできます)。
7. [**ファイルが存在することを確認**する] チェックボックスをオフにする
8. **[OK]** ボタンをクリックします。

[[新しいプロジェクト] ダイアログボックスの ![](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image4.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image7.png)

**図 4**: IIS 6.0 を使用したワイルドカードスクリプトマップの作成 ([クリックすると、フルサイズの画像が表示](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image8.png)される)

ワイルドカードスクリプトマップを有効にした後、グローバルな global.asax ファイル内のルートテーブルを変更してルートルートを含めるようにする必要があります。 そうしないと、アプリケーションのルートページに対して要求を行ったときに、図5のエラーページが表示されます。 リスト4で変更した global.asax ファイルを使用できます。

[[新しいプロジェクト] ダイアログボックスの ![](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image5.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image9.png)

**図 5**: ルートルートの不足エラー ([クリックすると、フルサイズの画像が表示](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image10.png)されます)

**リスト 4-global.asax (ルートルートで変更済み)**

[!code-csharp[Main](using-asp-net-mvc-with-different-versions-of-iis-cs/samples/sample4.cs)]

IIS 7.0 または IIS 6.0 に対してワイルドカードスクリプトマップを有効にした後、次のような既定のルートテーブルを操作する要求を行うことができます。

/

/Home/Index

/Product/Details/3

/Product

## <a name="summary"></a>まとめ

このチュートリアルの目的は、古いバージョンの IIS (またはクラシックモードでは IIS 7.0) を使用するときに ASP.NET MVC を使用する方法を説明することでした。 以前のバージョンの IIS で動作するように ASP.NET ルーティングを取得する2つの方法を説明しました。既定のルートテーブルを変更するか、ワイルドカードスクリプトマップを作成します。

最初のオプションでは、ASP.NET MVC アプリケーションで使用される Url を変更する必要があります。 この最初のオプションの非常に大きな利点の1つは、ルートテーブルを変更するために web サーバーにアクセスする必要がないことです。 つまり、インターネットホスティング会社で ASP.NET MVC アプリケーションをホストしている場合でも、この最初のオプションを使用できます。

2つ目の方法は、ワイルドカードスクリプトマップを作成することです。 この2つ目の方法の利点は、Url を変更する必要がないことです。 この2つ目のオプションの欠点は、ASP.NET MVC アプリケーションのパフォーマンスに影響を与える可能性があることです。

> [!div class="step-by-step"]
> [Next](using-asp-net-mvc-with-different-versions-of-iis-vb.md)
