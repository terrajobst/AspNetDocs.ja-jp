---
uid: web-pages/overview/ui-layouts-and-themes/displaying-maps-in-an-aspnet-web-pages-site
title: ASP.NET Web ページ (Razor) サイトでマップを表示する |Microsoft Docs
author: Rick-Anderson
description: この記事では、Bing、Google、Ma... によって提供されるマッピングサービスに基づいて、ASP.NET Web ページ (Razor) web サイトのページに対話型マップを表示する方法について説明します。
ms.author: riande
ms.date: 02/20/2014
ms.assetid: b5c268dd-ca6a-4562-b94c-a220fcf01f58
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/displaying-maps-in-an-aspnet-web-pages-site
msc.type: authoredcontent
ms.openlocfilehash: 36f3b753cf312504892872ff54bef49854588990
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78518722"
---
# <a name="displaying-maps-in-an-aspnet-web-pages-razor-site"></a>ASP.NET Web ページ (Razor) サイトでマップを表示する

[Tom FitzMacken](https://github.com/tfitzmac)

> この記事では、Bing、Google、MapQuest、および Yahoo が提供するマッピングサービスに基づいて、ASP.NET Web ページ (Razor) web サイトのページに対話型マップを表示する方法について説明します。
> 
> ここでは、次の内容について学習します。
> 
> - アドレスに基づいてマップを生成する方法。
> - 緯度と経度の座標に基づいてマップを生成する方法。
> - Bing maps 開発者アカウントを登録し、Bing Maps で使用するキーを取得する方法。
> 
> この記事で導入された ASP.NET 機能は次のとおりです。
> 
> - `Maps` ヘルパー。
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>このチュートリアルで使用されているソフトウェアのバージョン
> 
> 
> - ASP.NET Web ページ (Razor) 2
> - WebMatrix 2
>   
> 
> このチュートリアルでは、WebMatrix 3 も使用できます。

Web ページでは、`Maps` ヘルパーを使用してページにマップを表示できます。 マップは、アドレスに基づいて生成することも、経度と緯度の座標のセットに基づいて生成することもできます。 `Maps` クラスを使用すると、Bing、Google、MapQuest、Yahoo などの一般的なマップエンジンを呼び出すことができます。

ページにマッピングを追加する手順は、どのマップエンジンを呼び出すかに関係なく同じです。 ここでは、使用可能なメソッドを作成してマップを表示する JavaScript ファイル参照を追加し、`Maps` ヘルパーのメソッドを呼び出します。

使用する `Maps` ヘルパーメソッドに基づいてマップサービスを選択します。 次のいずれかを使用できます。

- `Maps.GetBingHtml`
- `Maps.GetGoogleHtml`
- `Maps.GetYahooHtml`
- `Maps.GetMapQuestHtml`

## <a name="installing-the-pieces-you-need"></a>必要なコンポーネントをインストールする

マップを表示するには、次の要素が必要です。

- `Maps` ヘルパー。 このヘルパーは、ASP.NET Web ヘルパーライブラリのバージョン2に含まれています。 まだライブラリを追加していない場合は、NuGet パッケージとしてサイトにインストールできます。 詳細については、「 [ASP.NET Web ページサイトへのヘルパーのインストール](https://go.microsoft.com/fwlink/?LinkId=252372)」を参照してください。 (ギャラリーで、`microsoft-web-helpers` パッケージを検索します)。
- JQuery ライブラリ。 いくつかの WebMatrix サイトテンプレートには既に、jQuery ライブラリが*スクリプト*フォルダーに含まれています。 これらのライブラリがない場合は、 [jQuery.org](http://jQuery.org)サイトから直接、最新の jQuery ライブラリをダウンロードできます。 または、テンプレート (**スターターサイト**テンプレートなど) を使用して新しいサイトを作成し、そのサイトから現在のサイトに jQuery ファイルをコピーすることもできます。

最後に、Bing maps を使用する場合は、最初に (無料) アカウントを作成し、キーを取得する必要があります。 キーを取得するには、次の手順を実行します。

1. [Bing Maps 開発者アカウント](https://www.microsoft.com/maps/developers/web.aspx)でアカウントを作成します。 Microsoft アカウント (Windows Live ID) も必要です。

    **評価/テスト**にキーを使用するように指定できます。 WebMatrix と IIS Express を使用して自分のコンピューターでマッピング関数をテストする場合は、**サイト**のワークスペースにアクセスし、サイトの URL をメモします (`http://localhost:50408`たとえば、ポート番号は異なる場合があります)。 この*localhost*アドレスは、登録時にサイトとして使用できます。
2. アカウントの登録が完了したら、Bing Maps アカウントセンターにアクセスし、 **[キーの作成または表示]** をクリックします。

    ![マッピング-2](displaying-maps-in-an-aspnet-web-pages-site/_static/image1.png)
3. Bing が作成するキーを記録します。

## <a name="creating-a-map-based-on-an-address-using-google"></a>アドレスに基づくマップの作成 (Google を使用)

次の例では、住所に基づいてマップを表示するページを作成する方法を示します。 この例では、Google Maps の使用方法を示します。

1. サイトのルートに*Mapaddress. cshtml*という名前のファイルを作成します。 このページでは、渡されたアドレスに基づいてマップが生成されます。
2. 次のコードをファイルにコピーして、既存のコンテンツを上書きします。

    [!code-cshtml[Main](displaying-maps-in-an-aspnet-web-pages-site/samples/sample1.cshtml)]

    このページの次の機能に注意してください。

    - `<head>` 要素内の `<script>` 要素。 この例では、`<script>` 要素は*jquery-1.6.4*ファイルを参照します。これは、jquery ライブラリバージョン1.6.4 の縮小版 (圧縮された) バージョンです。 参照では、 *.js*ファイルがサイトの*Scripts*フォルダーにあることを前提としています。 

        > [!NOTE]
        > 別のバージョンの jQuery ライブラリを使用している場合は、そのバージョンが正しく参照されていることを確認してください。
    - ページの本文内の `@Maps.GetGoogleHtml` への呼び出し。 アドレスをマップするには、アドレス文字列を渡す必要があります。 他のマップエンジンのメソッドは、同様の方法 (`@Maps.GetYahooHtml`、`@Maps.GetMapQuestHtml`) で動作します。
3. ページを実行し、アドレスを入力します。 ページには、指定した場所を示す、Google Maps に基づくマップが表示されます。

     ![マッピング-1](displaying-maps-in-an-aspnet-web-pages-site/_static/image2.png)

## <a name="creating-a-map-based-on-latitude-and-longitude-coordinates-using-bing"></a>緯度と経度の座標に基づくマップの作成 (Bing を使用)

この例では、座標に基づいてマップを作成する方法を示します。 この例では、Bing maps の使用方法と、Bing キーを含める方法を示します。 (Bing キーを使用せずに、他のマップエンジンを使用して座標に基づいてマップを作成することもできます)。

1. サイトのルートに*Mapcoordinates*という名前のファイルを作成し、既存の内容を次のコードとマークアップに置き換えます。

    [!code-cshtml[Main](displaying-maps-in-an-aspnet-web-pages-site/samples/sample2.cshtml)]
2. `your-key-here` を、前に生成した Bing Maps キーに置き換えます。
3. Mapcoordinates の [] ページを実行し、緯度と経度の座標を入力して、**マップ**をクリックし*ます。* ボタンを選択します。 (座標がわからない場合は、次の操作を試してください。 これは、Microsoft Redmond キャンパス上の場所です)。

   - 緯度: 47.6781005859375
   - 経度:-122.158317565918

     指定した座標を使用してページが表示されます。

     ![マッピング-3](displaying-maps-in-an-aspnet-web-pages-site/_static/image3.png)

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>その他のリソース

[Microsoft Maps API リファレンス](https://msdn.microsoft.com/library/gg427611.aspx)
