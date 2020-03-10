---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details
title: データ項目と詳細の表示 |Microsoft Docs
author: Erikre
description: このチュートリアルシリーズでは、ASP.NET 4.7 および Microsoft Visual Studio 2017 を使用して ASP.NET Web フォームアプリケーションを構築するための基礎を説明します。
ms.author: riande
ms.date: 1/04/2019
ms.assetid: 64a491a8-0ed6-4c2f-9c1c-412962eb6006
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details
msc.type: authoredcontent
ms.openlocfilehash: 130c9ffd29df612dac5bb954830a2eb9b738aaf0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78520810"
---
# <a name="display-data-items-and-details"></a>データ項目と詳細の表示

[Erik Reitan](https://github.com/Erikre)

> このチュートリアルシリーズでは、ASP.NET 4.7 と Microsoft Visual Studio 2017 を使用して ASP.NET Web フォームアプリケーションを構築するための基本について説明します。

このチュートリアルでは、ASP.NET Web フォームおよび Entity Framework Code First でデータ項目とデータ項目の詳細を表示する方法について説明します。 このチュートリアルは、Wingtip 玩具 Store チュートリアルシリーズの一部として、前の「UI とナビゲーション」チュートリアルに基づいています。 このチュートリアルを完了すると、 *Productdetails .aspx*ページに製品が表示され、 *productdetails .aspx*ページに製品の詳細が表示されます。

## <a name="youll-learn-how-to"></a>学習内容は次のとおりです。

- データベースから製品を表示するデータコントロールを追加する
- データコントロールを選択したデータに接続する
- データコントロールを追加して、製品の詳細をデータベースから表示する
- クエリ文字列から値を取得し、その値を使用して、データベースから取得されるデータを制限します。

### <a name="features-introduced-in-this-tutorial"></a>このチュートリアルで導入された機能は次のとおりです。

- モデル バインド
- 値プロバイダー

## <a name="add-a-data-control"></a>データコントロールを追加する

サーバーコントロールにデータをバインドするには、いくつかの異なるオプションを使用できます。 最も一般的なものは次のとおりです。

* データソースコントロールの追加
* 手動によるコードの追加
* モデルバインドの使用

### <a name="use-a-data-source-control-to-bind-data"></a>データソースコントロールを使用してデータをバインドする

データソースコントロールを追加すると、データを表示するコントロールにデータソースコントロールをリンクすることができます。 この方法では、プログラムによってサーバー側のコントロールをデータソースに接続するのではなく、宣言によって宣言できます。

### <a name="code-by-hand-to-bind-data"></a>データをバインドするための手作業のコード

手作業でコーディングするには、次の作業が必要です。

1. 値の読み取り
2. Null であるかどうかを確認しています
3. 適切な型への変換
4. 変換が成功したかどうかのチェック
5. クエリで値を使用する 

この方法では、データアクセスロジックを完全に制御できます。

### <a name="use-model-binding-to-bind-data"></a>モデルバインドを使用したデータのバインド

モデルバインドを使用すると、結果をはるかに少ないコードでバインドできるため、アプリケーション全体で機能を再利用することができます。 コード中心のデータアクセスロジックを簡単に操作できるだけでなく、豊富なデータバインディングフレームワークも提供します。

## <a name="display-products"></a>製品の表示

このチュートリアルでは、モデルバインドを使用してデータをバインドします。 モデルバインドを使用してデータを選択するようにデータコントロールを構成するには、コントロールの `SelectMethod` プロパティをページのコードのメソッド名に設定します。 データコントロールは、ページライフサイクルの適切なタイミングでメソッドを呼び出し、返されたデータを自動的にバインドします。 `DataBind` メソッドを明示的に呼び出す必要はありません。

1. **ソリューションエクスプローラー**で、 *productlist .aspx*を開きます。
2. 既存のマークアップを次のマークアップに置き換えます。   

    [!code-aspx-csharp[Main](display_data_items_and_details/samples/sample1.aspx)]

このコードでは、`productList` という名前の**ListView**コントロールを使用して、製品を表示します。

[!code-aspx-csharp[Main](display_data_items_and_details/samples/sample2.aspx)]

テンプレートとスタイルを使用して、 **ListView**コントロールでデータを表示する方法を定義します。 これは、任意の繰り返し構造のデータに便利です。 この**ListView**の例では、データベースデータを表示するだけでなく、コードを使用せずに、ユーザーがデータを編集、挿入、および削除したり、データを並べ替えたり、ページしたりできるようにすることもできます。

**ListView**コントロールの `ItemType` プロパティを設定することにより、データバインディング式 `Item` を使用できるようになり、コントロールが厳密に型指定されます。 前のチュートリアルで説明したように、`ProductName`を指定するなど、IntelliSense を使用して Item オブジェクトの詳細を選択できます。

![データ項目と詳細の表示-IntelliSense](display_data_items_and_details/_static/image1.png)

また、モデルバインディングを使用して `SelectMethod` 値を指定しています。 この値 (`GetProducts`) は、次の手順で製品を表示するために分離コードに追加するメソッドに対応しています。

### <a name="add-code-to-display-products"></a>製品を表示するコードを追加する

この手順では、データベースの製品データを**ListView**コントロールに設定するコードを追加します。 このコードでは、すべての製品と個々のカテゴリ製品の表示をサポートしています。

1. **ソリューションエクスプローラー**で、[ *productlist* ] を右クリックし、 **[コードの表示]** を選択します。
2. *ProductList.aspx.cs*ファイル内の既存のコードを次のコードに置き換えます。   

    [!code-csharp[Main](display_data_items_and_details/samples/sample3.cs)]

このコードは、 **ListView**コントロールの `ItemType` プロパティが*productlist. .aspx*ページで参照する `GetProducts` メソッドを示しています。 結果を特定のデータベースカテゴリに制限するために、コードは*Productlist. .aspx*ページに移動したときに、 *productlist. .aspx*ページに渡されるクエリ文字列値の `categoryId` 値を設定します。 `System.Web.ModelBinding` 名前空間の `QueryStringAttribute` クラスは、クエリ文字列変数 `id`の値を取得するために使用されます。 これにより、モデルバインドは、クエリ文字列の値を実行時に `categoryId` パラメーターにバインドするように指示します。

有効なカテゴリがクエリ文字列としてページに渡されると、クエリの結果は、`categoryId` 値に一致するデータベース内の製品に制限されます。 たとえば、製品*リスト .aspx*ページの URL が次のようになっているとします。

[!code-console[Main](display_data_items_and_details/samples/sample4.cmd)]

このページには、`categoryId` が `1`に等しい製品のみが表示されます。

*Productlist .aspx*ページが呼び出されたときにクエリ文字列が含まれていない場合は、すべての製品が表示されます。

これらのメソッドの値のソースは、*値*プロバイダー ( *QueryString*など) と呼ばれ、使用する値プロバイダーを示すパラメーター属性は、*値プロバイダー属性*(`id`など) と呼ばれます。 ASP.NET には、クエリ文字列、cookie、フォーム値、コントロール、ビューステート、セッション状態、プロファイルプロパティなど、Web フォームアプリケーションでのユーザー入力のすべての一般的なソースに対して、値プロバイダーとそれに対応する属性が含まれています。 カスタム値プロバイダーを作成することもできます。

### <a name="run-the-application"></a>アプリケーションの実行

今すぐアプリケーションを実行して、すべての製品またはカテゴリの製品を表示します。

1. Visual Studio で**F5**キーを押してアプリケーションを実行します。  
   ブラウザーが開き、 *default.aspx*ページが表示されます。

2. 製品カテゴリのナビゲーションメニューから **[車両]** を選択します。  
   *Productlist .aspx*ページには、**車両**カテゴリの製品のみが表示されます。 このチュートリアルの後半では、製品の詳細を表示します。  

    ![データ項目と詳細を表示する-自動車](display_data_items_and_details/_static/image2.png)

3. 上部のナビゲーションメニューから **[製品]** を選択します。  
   ここでも、 *productlist .aspx*ページが表示されますが、今回は製品の一覧全体が表示されます。   

    ![データ項目と詳細の表示-製品](display_data_items_and_details/_static/image3.png)

4. ブラウザーを閉じて、Visual Studio に戻ります。

### <a name="add-a-data-control-to-display-product-details"></a>データコントロールを追加して製品の詳細を表示する

次に、前のチュートリアルで追加した*Productdetails .aspx*ページのマークアップを変更して、特定の製品情報を表示します。

1. **ソリューションエクスプローラー**で、 *productdetails .aspx*を開きます。

2. 既存のマークアップを次のマークアップに置き換えます。

    [!code-aspx-csharp[Main](display_data_items_and_details/samples/sample5.aspx)] 

    このコードでは、 **FormView**コントロールを使用して特定の製品の詳細を表示します。 このマークアップは、 *Productlist. .aspx*ページでのデータの表示に使用されるメソッドなどのメソッドを使用します。 **FormView**コントロールは、データソースから一度に1つのレコードを表示するために使用されます。 **FormView**コントロールを使用する場合は、データバインド値を表示および編集するためのテンプレートを作成します。 これらのテンプレートには、フォームの外観と機能を定義するコントロール、バインド式、および書式設定が含まれています。

前のマークアップをデータベースに接続するには、追加のコードが必要です。

1. **ソリューションエクスプローラー**で、[ *productdetails. .aspx* ] を右クリックし、 **[コードの表示]** をクリックします。  
   *ProductDetails.aspx.cs*ファイルが表示されます。

2. 既存のコードを次のコードに置き換えます。   

    [!code-csharp[Main](display_data_items_and_details/samples/sample6.cs)]

このコードでは、"`productID`" クエリ文字列値があるかどうかを確認します。 有効なクエリ文字列値が見つかった場合は、照合製品が表示されます。 クエリ文字列が見つからない場合、またはその値が有効でない場合は、製品は表示されません。

### <a name="run-the-application"></a>アプリケーションの実行

これで、アプリケーションを実行して、製品 ID に基づいて表示される個々の製品を確認できます。

1. Visual Studio で**F5**キーを押してアプリケーションを実行します。  
   ブラウザーが開き、 *default.aspx*ページが表示されます。

2. カテゴリナビゲーションメニューから **[ボート]** を選択します。  
   *Productlist .aspx*ページが表示されます。

3. 製品リストから **[用紙ボート]** を選択します。
   *Productdetails .aspx*ページが表示されます。

    ![データ項目と詳細の表示-製品](display_data_items_and_details/_static/image4.png)
    
4. ブラウザーを閉じます。

## <a name="additional-resources"></a>その他のリソース

[モデルバインドと web フォームを使用したデータの取得と表示](../../presenting-and-managing-data/model-binding/retrieving-data.md)

## <a name="next-steps"></a>次のステップ

このチュートリアルでは、製品と製品の詳細を表示するためのマークアップとコードを追加しました。 厳密に型指定されたデータコントロール、モデルバインディング、および値プロバイダーについて学習しました。 次のチュートリアルでは、Wingtip Toys サンプルアプリケーションにショッピングカートを追加します。 

> [!div class="step-by-step"]
> [前へ](ui_and_navigation.md)
> [次へ](shopping-cart.md)
