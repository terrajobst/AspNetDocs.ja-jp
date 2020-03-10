---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-7
title: 'パート 7: 機能の追加 |Microsoft Docs'
author: JoeStagner
description: このチュートリアルシリーズでは、Tailspin Spyworks サンプルアプリケーションを構築するために実行するすべての手順について詳しく説明します。 パート7では、account 確認などの機能が追加されています。
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 50223ee9-11b9-4cf3-bca2-e2f10bf471f3
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-7
msc.type: authoredcontent
ms.openlocfilehash: ffd2b862c727db9572c272b7b21bcc33c822fffa
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78521566"
---
# <a name="part-7-adding-features"></a>パート 7: 機能の追加

[Joe Stagner](https://github.com/JoeStagner)

> Tailspin Spyworks は、.NET プラットフォーム用の強力でスケーラブルなアプリケーションを簡単に作成する方法を示しています。 ASP.NET 4 の優れた新機能を使用して、ショッピング、チェックアウト、管理などのオンラインストアを構築する方法を示しています。
> 
> このチュートリアルシリーズでは、Tailspin Spyworks サンプルアプリケーションを構築するために実行するすべての手順について詳しく説明します。 パート7では、アカウントレビュー、製品レビュー、"人気のあるアイテム"、"購入した" ユーザーコントロールなどの追加機能を追加します。

## <a id="_Toc260221673"></a>機能の追加

ユーザーはカタログを参照し、ショッピングカートにアイテムを配置し、チェックアウトプロセスを完了することができますが、サイトを改善するためのサポート機能がいくつか用意されています。

1. アカウントレビュー (注文の一覧表示と詳細の表示)
2. コンテキスト固有のコンテンツを前面ページに追加します。
3. カタログ内の製品をユーザーが確認できるようにする機能を追加します。
4. 人気のある項目を表示し、そのコントロールを前面のページに配置するユーザーコントロールを作成します。
5. "購入済み" のユーザーコントロールを作成し、[製品の詳細] ページに追加します。
6. 連絡先ページを追加します。
7. [バージョン情報] ページを追加します。
8. グローバルエラー

## <a id="_Toc260221674"></a>アカウントのレビュー

"Account" フォルダーで、OrderList という名前の2つの .aspx ページを作成し、OrderDetails という名前を付けます。

OrderList .aspx では、以前と同じように GridView と EntityDataSource のコントロールが活用されます。

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample1.aspx)]

EntityDataSource は、ユーザーのログイン時にセッション変数に設定されている、ユーザー名でフィルター処理された Orders テーブルからレコードを選択します (where-object パラメーターを参照)。

GridView の [ハイパーリンク] フィールドにも、次のパラメーターがあります。

[!code-xml[Main](tailspin-spyworks-part-7/samples/sample2.xml)]

これらは、各製品の注文詳細ビューへのリンクを指定します。これは、OrderDetails ページの QueryString パラメーターとして OrderID フィールドを指定します。

## <a id="_Toc260221675"></a>OrderDetails

注文データを表示するために EntityDataSource コントロールを使用し、他の EntityDataSource を GridView と共に使用して注文のすべての行項目を表示します。

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample3.aspx)]

分離コードファイル (OrderDetails.aspx.cs) には、2つの簡単なハウスキーピングがあります。

まず、OrderDetails が常に OrderId を取得するようにする必要があります。

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample4.cs)]

また、行アイテムから注文合計を計算して表示する必要もあります。

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample5.cs)]

## <a id="_Toc260221676"></a>ホームページ

Default.aspx ページに静的コンテンツをいくつか追加してみましょう。

まず、"Content" フォルダーを作成し、Images フォルダー内に作成します (ホームページで使用するイメージを含めます)。

Default.aspx ページの下のプレースホルダーに、次のマークアップを追加します。

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample6.aspx)]

## <a id="_Toc260221677"></a>製品レビュー

まず、製品レビューを開始するために使用できるフォームへのリンクを含むボタンを追加します。

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample7.aspx)]

![](tailspin-spyworks-part-7/_static/image1.jpg)

クエリ文字列で ProductID を渡していることに注意してください。

次に、ReviewAdd という名前のページを追加します。

このページでは、ASP.NET AJAX Control Toolkit を使用します。 まだ実行していない場合は、 [Devexpress](http://devexpress.com/act)からダウンロードできます。このツールキットを Visual Studio で使用するための設定については、 [https://www.asp.net/learn/ajax-videos/video-76.aspx](../../../videos/ajax-control-toolkit/how-do-i-get-started-with-the-aspnet-ajax-control-toolkit.md)を参照してください。

デザインモードで、[ツールボックス] からコントロールとバリデーターをドラッグし、次のようなフォームを作成します。

![](tailspin-spyworks-part-7/_static/image2.jpg)

マークアップは次のようになります。

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample8.aspx)]

レビューを入力できるようになったので、これらのレビューを製品ページで表示できるようになりました。

このマークアップを ProductDetails .aspx ページに追加します。

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample9.aspx)]

ここでアプリケーションを実行し、製品に移動すると、顧客のレビューなどの製品情報が表示されます。

![](tailspin-spyworks-part-7/_static/image3.jpg)

## <a id="_Toc260221678"></a>一般的な項目コントロール (ユーザーコントロールの作成)

Web サイトの売上を向上させるために、人気のある製品や関連製品を "推奨販売" する機能をいくつか追加します。

これらの機能の1つは、製品カタログの人気のある製品の一覧です。

"ユーザーコントロール" を作成して、アプリケーションのホームページで上位の販売項目を表示します。 これはコントロールであるため、Visual Studio のデザイナーでコントロールを任意のページにドラッグアンドドロップするだけで、任意のページで使用できます。

Visual Studio のソリューションエクスプローラーで、ソリューション名を右クリックし、"Controls" という名前の新しいディレクトリを作成します。 これを行う必要はありませんが、"Controls" ディレクトリにすべてのユーザーコントロールを作成して、プロジェクトを整理したままにしておくことをお勧めします。

[コントロール] フォルダーを右クリックし、[新しい項目] を選択します。

![](tailspin-spyworks-part-7/_static/image4.jpg)

"PopularItems" のコントロールの名前を指定します。 ユーザーコントロールのファイル拡張子は .ascx ではないことに注意してください。

人気のある項目のユーザーコントロールは、次のように定義されます。

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample10.aspx)]

ここでは、このアプリケーションでまだ使用していないメソッドを使用しています。 Repeater コントロールを使用しています。データソースコントロールを使用する代わりに、Repeater コントロールを LINQ to Entities クエリの結果にバインドしています。

コントロールの分離コードでは、次のようにします。

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample11.cs)]

また、この重要な行は、コントロールのマークアップの上部にあります。

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample12.aspx)]

最も人気のある項目は分単位で変更されないため、aching ディレクティブを追加してアプリケーションのパフォーマンスを向上させることができます。 このディレクティブを使用すると、コントロールのキャッシュされた出力の有効期限が切れたときにのみ、コントロールコードが実行されます。 それ以外の場合は、コントロールの出力のキャッシュされたバージョンが使用されます。

次に、default.aspx ページに新しいコントロールを追加する必要があります。

ドラッグアンドドロップを使用して、既定のフォームの [開く] 列にコントロールのインスタンスを配置します。

![](tailspin-spyworks-part-7/_static/image5.jpg)

アプリケーションを実行すると、最も人気のある項目がホームページに表示されるようになりました。

![](tailspin-spyworks-part-7/_static/image6.jpg)

## <a id="_Toc260221679"></a>"購入済み" コントロール (パラメーターを使用したユーザーコントロール)

2番目に作成するユーザーコントロールは、コンテキストの特異性を追加することによって、次のレベルに推奨することになります。

上位の "購入した" 項目を計算するロジックは、重要ではありません。

"購入済み" コントロールは、現在選択されている ProductID の OrderDetails レコード (以前に購入したもの) を選択し、見つかった一意の注文ごとに OrderIDs を取得します。

次に、これらすべての注文から製品を選択し、購入した数量を合計します。 製品をその数量の合計で並べ替え、上位5つの項目を表示します。

このロジックが複雑になると、このアルゴリズムはストアドプロシージャとして実装されます。

ストアドプロシージャの T-sql は次のようになります。

[!code-sql[Main](tailspin-spyworks-part-7/samples/sample13.sql)]

このストアドプロシージャ (SelectPurchasedWithProducts) は、アプリケーションに含まれていたデータベース内に存在していたので Entity Data Model、必要なテーブルとビューに加えて、必要なテーブルとビューに加えて、Entity Data Model を生成した場合は、次のように指定されていることに注意してください。には、このストアドプロシージャを含める必要があります。

Entity Data Model からストアドプロシージャにアクセスするには、関数をインポートする必要があります。

ソリューションエクスプローラーで Entity Data Model をダブルクリックしてデザイナーで開き、モデルブラウザーを開き、デザイナーで右クリックして、[関数インポートの追加] を選択します。

![](tailspin-spyworks-part-7/_static/image1.png)

そうすると、このダイアログが開きます。

![](tailspin-spyworks-part-7/_static/image2.png)

上記のフィールドに入力し、"SelectPurchasedWithProducts" を選択して、インポートした関数の名前としてプロシージャ名を使用します。

[Ok] をクリックします。

これを行うには、モデル内の他の項目と同じように、ストアドプロシージャに対してプログラミングするだけです。

そのため、"コントロール" フォルダーで、AlsoPurchased という名前の新しいユーザーコントロールを作成します。

このコントロールのマークアップは、PopularItems コントロールに非常によく似ています。

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample14.aspx)]

注目すべき違いは、表示される項目の内容が製品によって異なるため、出力がキャッシュされないことです。

ProductId は、コントロールの "プロパティ" になります。

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample15.cs)]

コントロールの PreRender イベントハンドラーで、3つの処理を eed します。

1. ProductID が設定されていることを確認します。
2. 現在の製品が購入されている製品があるかどうかを確認します。
3. #2 で決定されたとおりに項目を出力します。

モデルを通じてストアドプロシージャを呼び出すことがいかに簡単であるかに注意してください。

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample16.cs)]

「購入済み」があることを確認した後は、クエリによって返された結果にリピータをバインドするだけで済みます。

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample17.cs)]

"購入済み" の項目がない場合は、カタログから他の人気のある項目を表示するだけです。

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample18.cs)]

"購入済み" の項目を表示するには、ProductDetails .aspx ページを開き、ソリューションエクスプローラーから AlsoPurchased コントロールをドラッグして、マークアップ内のこの位置に表示されるようにします。

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample19.aspx)]

これにより、ProductDetails ページの上部にコントロールへの参照が作成されます。

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample20.aspx)]

AlsoPurchased ユーザーコントロールには ProductId 番号が必要であるため、ページの現在のデータモデルアイテムに対して Eval ステートメントを使用して、コントロールの ProductID プロパティを設定します。

![](tailspin-spyworks-part-7/_static/image3.png)

今すぐビルドして実行し、製品を参照すると、"購入済み" の項目も表示されます。

![](tailspin-spyworks-part-7/_static/image7.jpg)

> [!div class="step-by-step"]
> [前へ](tailspin-spyworks-part-6.md)
> [次へ](tailspin-spyworks-part-8.md)
