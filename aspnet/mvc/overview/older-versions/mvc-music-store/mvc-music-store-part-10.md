---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-10
title: 'パート 10: ナビゲーションとサイト設計の最終更新、結論 |Microsoft Docs'
author: jongalloway
description: このチュートリアルシリーズでは、ASP.NET MVC ミュージックストアサンプルアプリケーションをビルドするために実行するすべての手順について詳しく説明します。 パート10では、ナビゲーションと...
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 0c6e4c2f-fcdb-4978-9656-1990c6f15727
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-10
msc.type: authoredcontent
ms.openlocfilehash: f701d1fbabc3e1a97c3750d00e96bf8dba1105cd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78433612"
---
# <a name="part-10-final-updates-to-navigation-and-site-design-conclusion"></a>パート 10: ナビゲーションとサイト設計の最終更新、結論

( [Jon Galloway](https://github.com/jongalloway) )

> MVC Music Store は、ASP.NET MVC と Visual Studio を使用して web 開発を行う方法を紹介したチュートリアルアプリケーションです。  
>   
> MVC ミュージックストアは、音楽アルバムをオンラインで販売し、基本的なサイト管理、ユーザーサインイン、およびショッピングカート機能を実装する軽量のサンプルストア実装です。  
>   
> このチュートリアルシリーズでは、ASP.NET MVC ミュージックストアサンプルアプリケーションをビルドするために実行するすべての手順について詳しく説明します。 パート10では、ナビゲーションとサイト設計の最終的な更新について説明します。

サイトの主要な機能はすべて完了しましたが、サイトのナビゲーション、ホームページ、ストアの参照ページに追加できる機能がまだいくつかあります。

## <a name="creating-the-shopping-cart-summary-partial-view"></a>ショッピングカートの概要部分ビューの作成

サイト全体のユーザーのショッピングカートに含まれる項目の数を公開したいと考えています。

![](mvc-music-store-part-10/_static/image1.png)

これを簡単に実装するには、部分ビューを作成します。これは、サイトに追加されます。

前に示したように、ShoppingCart コントローラーには、部分ビューを返す CartSummary action メソッドが含まれています。

[!code-csharp[Main](mvc-music-store-part-10/samples/sample1.cs)]

CartSummary 部分ビューを作成するには、Views/ShoppingCart フォルダーを右クリックし、[ビューの追加] を選択します。 ビューに CartSummary という名前を付け、次に示すように [部分ビューを作成する] チェックボックスをオンにします。

![](mvc-music-store-part-10/_static/image2.png)

CartSummary 部分ビューは非常に単純です。これは、カート内の項目の数を表示する ShoppingCart Index ビューへのリンクです。 CartSummary の完全なコードは次のとおりです。

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample2.cshtml)]

サイトマスターを含む、サイト内の任意のページに部分ビューを含めることができます。これには、Html の RenderAction メソッドを使用します。 RenderAction を実行するには、次のようにアクション名 ("CartSummary") とコントローラー名 ("ShoppingCart") を指定する必要があります。

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample3.cshtml)]

これをサイトレイアウトに追加する前に、ジャンルメニューも作成します。これにより、すべてのサイトが一度に更新されます。

## <a name="creating-the-genre-menu-partial-view"></a>ジャンルメニュー部分ビューの作成

ストア内で利用可能なすべてのジャンルを一覧表示する Genre メニューを追加することで、ユーザーがストア内をより簡単に移動できるようにすることができます。

![](mvc-music-store-part-10/_static/image3.png)

同じ手順を実行して、[GenreMenu] 部分ビューも作成します。次に、両方をサイトマスターに追加します。 まず、次の GenreMenu コントローラーアクションを StoreController に追加します。

[!code-csharp[Main](mvc-music-store-part-10/samples/sample4.cs)]

この操作により、部分ビューに表示されるジャンルの一覧が返されます。これは次に作成します。

*メモ: このコントローラーアクションに [ChildActionOnly] 属性を追加しました。これは、このアクションを部分ビューからのみ使用することを示します。この属性を設定すると、コントローラーの操作を実行できなくなります。これは部分ビューには必要ありませんが、コントローラーのアクションが意図したとおりに使用されていることを確認する必要があるため、お勧めします。また、ビューではなく PartialView も返されます。これにより、ビューエンジンは、他のビューに含まれているため、このビューのレイアウトを使用しないことを確認できます。*

GenreMenu controller アクションを右クリックし、次に示すように Genre view データクラスを使用して厳密に型指定された GenreMenu という名前の部分ビューを作成します。

![](mvc-music-store-part-10/_static/image4.png)

次のように、順序付けられていないリストを使用して項目を表示するように、GenreMenu 部分ビューのビューコードを更新します。

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample5.cshtml)]

## <a name="updating-site-layout-to-display-our-partial-views"></a>部分ビューを表示するようにサイトレイアウトを更新しています

Html の RenderAction () を呼び出すことによって、部分ビューをサイトレイアウト (/ビュー/Shared/\_Layout) に追加できます。 次に示すように、との両方に追加のマークアップを追加して表示します。

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample6.cshtml)]

アプリケーションを実行すると、左側のナビゲーション領域にジャンルが表示され、[カートの概要] が上部に表示されます。

## <a name="update-to-the-store-browse-page"></a>ストアの参照ページに更新する

ストアの参照ページは機能していますが、正しくありません。 ページを更新して、次のようにビューコード (/Views/Store/Browse.cshtml にあります) を更新することにより、アルバムがより適切なレイアウトで表示されるようにすることができます。

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample7.cshtml)]

ここでは、Html.actionlink ではなく、Url を使用します。これにより、アルバムのアートワークを含めるための特別な書式設定をリンクに適用できるようになります。

*注: これらのアルバムの一般的なアルバムカバーを表示しています。この情報はデータベースに保存され、ストアマネージャーを使用して編集できます。独自のアートワークを追加できるようになります。*

ジャンルを参照すると、アルバムのアートワークがグリッドに表示されます。

![](mvc-music-store-part-10/_static/image5.png)

## <a name="updating-the-home-page-to-show-top-selling-albums"></a>ホームページを更新して、売上の多いアルバムを表示する

売上を増やすために、ホームページで上位の販売アルバムを機能させたいと考えています。 これを処理するために、HomeController にいくつかの更新を行い、追加のグラフィックスも追加します。

まず、アルバムクラスにナビゲーションプロパティを追加します。これにより、EntityFramework が関連付けられていることを認識します。 **アルバム**クラスの最後の数行は、次のようになります。

[!code-csharp[Main](mvc-music-store-part-10/samples/sample8.cs)]

*注: これには、using ステートメントを追加して、system.string 名前空間を取り込む必要があります。*

まず、他のコントローラーと同様に、ステートメントを使用して storeDB フィールドと MvcMusicStore を追加します。 次に、HomeController に次のメソッドを追加します。このメソッドは、OrderDetails に従って上位の販売アルバムを検索するために、データベースにクエリを行います。

[!code-csharp[Main](mvc-music-store-part-10/samples/sample9.cs)]

これは、コントローラーアクションとして使用できないようにするためのプライベートメソッドです。 わかりやすくするために HomeController に追加していますが、ビジネスロジックは、必要に応じて別のサービスクラスに移動することをお勧めします。

その後、インデックスコントローラーアクションを更新して、上位5つの販売アルバムに対してクエリを実行し、ビューに返すことができます。

[!code-csharp[Main](mvc-music-store-part-10/samples/sample10.cs)]

更新された HomeController の完全なコードは次のようになります。

[!code-csharp[Main](mvc-music-store-part-10/samples/sample11.cs)]

最後に、モデルの種類を更新してアルバムリストを下部に追加することで、アルバムの一覧を表示できるように、ホームインデックスビューを更新する必要があります。 この機会に、見出しとプロモーションセクションもページに追加します。

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample12.cshtml)]

アプリケーションを実行すると、更新されたホームページが表示され、売上が多いアルバムとプロモーションメッセージが表示されます。

![](mvc-music-store-part-10/_static/image1.jpg)

## <a name="conclusion"></a>まとめ

ASP.NET MVC を使用すると、データベースアクセス、メンバーシップ、AJAX などを使用して、洗練された web サイトを簡単に作成できることがわかりました。 非常に迅速です。 このチュートリアルでは、独自の ASP.NET MVC アプリケーションの構築を開始するために必要なツールが用意されています。

> [!div class="step-by-step"]
> [[戻る]](mvc-music-store-part-9.md)
