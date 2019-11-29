---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/shopping-cart
title: ショッピングカート |Microsoft Docs
author: Erikre
description: このチュートリアルシリーズでは、ASP.NET 4.5 と Microsoft Visual Studio Express 2013 を使用して ASP.NET Web フォームアプリケーションを構築するための基本について説明します。
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 6898c601-6c31-432f-8388-e6843f8a17cb
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/shopping-cart
msc.type: authoredcontent
ms.openlocfilehash: 46264a0ab2244cff24761ce94b41722e61e3f426
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74614920"
---
# <a name="shopping-cart"></a>ショッピング カート

[Erik Reitan](https://github.com/Erikre)

[Wingtip Toys サンプルプロジェクト (C#) をダウンロード](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)するか[、電子書籍 (PDF) をダウンロード](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)します。

> このチュートリアルシリーズでは、ASP.NET 4.5 を使用して ASP.NET Web フォームアプリケーションを構築するための基礎と、Web 用の Microsoft Visual Studio Express 2013 について説明します。 このチュートリアルシリーズ[でC#は、ソースコードが含ま](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)れる Visual Studio 2013 プロジェクトを利用できます。

このチュートリアルでは、Wingtip Toys のサンプル ASP.NET Web フォームアプリケーションにショッピングカートを追加するために必要なビジネスロジックについて説明します。 このチュートリアルは、前のチュートリアル「データ項目と詳細の表示」に基づいており、Wingtip 玩具 Store チュートリアルシリーズの一部です。 このチュートリアルを完了すると、サンプルアプリのユーザーは、ショッピングカートで製品を追加、削除、および変更できるようになります。

## <a name="what-youll-learn"></a>学習内容:

1. Web アプリケーションのショッピングカートを作成する方法。
2. ユーザーがショッピングカートに商品を追加できるようにする方法。
3. 詳細を表示するために[GridView](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview(v=vs.110).aspx#introduction)コントロールを追加する方法について説明します。
4. 注文の合計を計算して表示する方法。
5. ショッピングカートのアイテムを削除および更新する方法。
6. ショッピングカートカウンターを含める方法。

## <a name="code-features-in-this-tutorial"></a>このチュートリアルのコード機能は次のとおりです。

1. Entity Framework Code First
2. データの注釈
3. 厳密に型指定されたデータコントロール
4. モデル バインド

## <a name="creating-a-shopping-cart"></a>ショッピングカートの作成

このチュートリアルシリーズの前半では、データベースから製品データを表示するためのページとコードを追加しました。 このチュートリアルでは、買い物かごを作成して、ユーザーが購入したい製品を管理します。 登録されていない、またはログインしていない場合でも、ユーザーはショッピングカートにアイテムを参照して追加することができます。 ショッピングカートへのアクセスを管理するには、ユーザーが初めてショッピングカートにアクセスしたときに、グローバル一意識別子 (GUID) を使用して、ユーザーに一意の `ID` を割り当てます。 この `ID` は、ASP.NET セッション状態を使用して格納します。

> [!NOTE] 
> 
> ASP.NET セッション状態は、ユーザーがサイトから離脱した後に期限切れになるユーザー固有の情報を格納するのに便利な場所です。 大規模なサイトでは、セッション状態の誤用によってパフォーマンスに影響が生じる可能性がありますが、セッション状態の使用は、デモンストレーションのために適切に機能します。 Wingtip Toys のサンプルプロジェクトでは、外部プロバイダーを使用せずにセッション状態を使用する方法を示しています。この場合、セッション状態は、サイトをホストしている web サーバーでインプロセスで格納されます。 アプリケーションの複数のインスタンスを提供する大規模なサイトや、異なるサーバー上でアプリケーションの複数のインスタンスを実行するサイトの場合は、 **Windows Azure Cache Service**の使用を検討してください。 この Cache Service は、web サイトの外部にある分散キャッシュサービスを提供し、インプロセスセッション状態を使用する場合の問題を解決します。 詳細については、 [Windows Azure websites で ASP.NET セッション状態を使用する方法](https://docs.microsoft.com/azure/redis-cache/cache-aspnet-session-state-provider)に関するページを参照してください。

### <a name="add-cartitem-as-a-model-class"></a>モデルクラスとして CartItem を追加する

このチュートリアルシリーズの前半では、[*モデル*] フォルダーに `Category` クラスと `Product` クラスを作成して、カテゴリと製品データのスキーマを定義しています。 次に、ショッピングカートのスキーマを定義する新しいクラスを追加します。 このチュートリアルの後の方で、`CartItem` テーブルへのデータアクセスを処理するクラスを追加します。 このクラスは、ショッピングカートのアイテムを追加、削除、および更新するビジネスロジックを提供します。

1. *モデル* フォルダーを右クリックし、**新しい項目**の追加 -&gt; **追加** を選択します。 

    ![ショッピングカート-新しいアイテム](shopping-cart/_static/image1.png)
2. **[新しい項目の追加]** ダイアログ ボックスが表示されます。 **[コード]** を選択し、 **[クラス]** を選択します。 

    ![ショッピングカート-[新しい項目の追加] ダイアログ](shopping-cart/_static/image2.png)
3. この新しいクラスに*CartItem.cs*という名前を指定します。
4. **[追加]** をクリックします。  
   新しいクラスファイルがエディターに表示されます。
5. 既定のコードを次のコードに置き換えます。   

    [!code-csharp[Main](shopping-cart/samples/sample1.cs)]

`CartItem` クラスには、ユーザーがショッピングカートに追加する各製品を定義するスキーマが含まれています。 このクラスは、このチュートリアルシリーズの前の手順で作成した他のスキーマクラスに似ています。 慣例により、Entity Framework Code First では、`CartItem` テーブルの主キーが `CartItemId` または `ID`であると想定されています。 ただし、このコードでは、データ注釈 `[Key]` 属性を使用して既定の動作をオーバーライドしています。 ItemId プロパティの `Key` 属性は、`ItemID` プロパティが主キーであることを指定します。

`CartId` プロパティは、購入する項目に関連付けられているユーザーの `ID` を指定します。 ユーザーがショッピングカートにアクセスしたときに、このユーザー `ID` を作成するコードを追加します。 この `ID` は、ASP.NET Session 変数としても保存されます。

### <a name="update-the-product-context"></a>製品のコンテキストを更新する

`CartItem` クラスを追加するだけでなく、エンティティクラスを管理し、データベースへのデータアクセスを提供するデータベースコンテキストクラスを更新する必要があります。 これを行うには、新しく作成した `CartItem` モデルクラスを `ProductContext` クラスに追加します。

1. **ソリューションエクスプローラー**で、[*モデル*] フォルダー内の*ProductContext.cs*ファイルを見つけて開きます。
2. 次のように、強調表示されているコードを*ProductContext.cs*ファイルに追加します。  

    [!code-csharp[Main](shopping-cart/samples/sample2.cs?highlight=14)]

このチュートリアルシリーズで前述したように、 *ProductContext.cs*ファイルのコードは、Entity Framework のすべてのコア機能にアクセスできるように、`System.Data.Entity` 名前空間を追加します。 この機能には、厳密に型指定されたオブジェクトを操作することによって、データのクエリ、挿入、更新、および削除を行う機能が含まれています。 `ProductContext` クラスは、新しく追加された `CartItem` モデルクラスへのアクセスを追加します。

### <a name="managing-the-shopping-cart-business-logic"></a>ショッピングカートのビジネスロジックを管理する

次に、新しい*Logic*フォルダーに `ShoppingCart` クラスを作成します。 `ShoppingCart` クラスは、`CartItem` テーブルへのデータアクセスを処理します。 クラスには、ショッピングカートのアイテムを追加、削除、および更新するためのビジネスロジックも含まれます。

追加するショッピングカートのロジックには、次のアクションを管理するための機能が含まれています。

1. ショッピングカートへのアイテムの追加
2. ショッピングカートからのアイテムの削除
3. ショッピングカート ID を取得しています
4. ショッピングカートから項目を取得する
5. すべてのショッピングカートアイテムの合計金額
6. ショッピングカートデータを更新しています

ショッピングカートのページ (*ShoppingCart*) とショッピングカートのクラスを一緒に使用して、ショッピングカートのデータにアクセスします。 ショッピングカートページには、ユーザーがショッピングカートに追加したすべてのアイテムが表示されます。 ショッピングカートのページとクラスに加えて、ショッピングカートに製品を追加するページ (*addtocart .aspx*) を作成します。 また、 *Productlist .aspx*ページと*productlist .aspx*ページにコードを追加します。このページには、ユーザーが製品をショッピングカートに追加できるように、 *addtocart .aspx*ページへのリンクが用意されています。

次の図は、ユーザーがショッピングカートに製品を追加したときに発生する基本的なプロセスを示しています。

![ショッピングカート-ショッピングカートへの追加](shopping-cart/_static/image3.png)

ユーザーが [ *Productlist* ] ページまたは [ *productlist* ] ページのいずれかで **[カートに追加]** リンクをクリックすると、アプリケーションは*addtocart .aspx*ページに移動し、自動的に*ShoppingCart*ページに移動します。 *Addtocart .aspx*ページでは、ShoppingCart クラスのメソッドを呼び出すことによって、ショッピングカートに select 製品が追加されます。 *ShoppingCart*ページには、ショッピングカートに追加された製品が表示されます。

#### <a name="creating-the-shopping-cart-class"></a>ショッピングカートクラスを作成する

`ShoppingCart` クラスはアプリケーション内の別のフォルダーに追加されるため、モデル ([モデル] フォルダー)、ページ (ルートフォルダー)、およびロジック (Logic フォルダー) が明確に区別されます。

1. **ソリューションエクスプローラー**で、**ウィング? toys**プロジェクトを右クリックし、[-の追加] を選択して &gt;**新しいフォルダー**を**追加**します。 新しいフォルダー*ロジック*に名前を指定します。
2. *Logic*フォルダーを右クリックし、[ **Add** -&gt;**新しい項目**] を選択します。
3. *ShoppingCartActions.cs*という名前の新しいクラスファイルを追加します。
4. 既定のコードを次のコードに置き換えます。   

    [!code-csharp[Main](shopping-cart/samples/sample3.cs)]

`AddToCart` メソッドを使用すると、製品 `ID`に基づいて個々の製品をショッピングカートに含めることができます。 製品がカートに追加されるか、カートにその製品の品目が既に含まれている場合は、数量が増えます。

`GetCartId` メソッドは、ユーザーのカート `ID` を返します。 カート `ID` は、ユーザーがショッピングカートで持っているアイテムを追跡するために使用されます。 ユーザーに既存のカート `ID`がない場合は、新しいカート `ID` が作成されます。 ユーザーが登録済みユーザーとしてサインインしている場合、カートの `ID` はユーザー名に設定されます。 ただし、ユーザーがサインインしていない場合、カートの `ID` は一意の値 (GUID) に設定されます。 GUID を使用すると、セッションに基づいて、ユーザーごとにカートが1つだけ作成されます。

`GetCartItems` メソッドは、ユーザーのショッピングカートアイテムの一覧を返します。 このチュートリアルの後半では、モデルバインドを使用して、`GetCartItems` 方法を使用してショッピングカートにカート項目を表示する方法について説明します。

### <a name="creating-the-add-to-cart-functionality"></a>カートへの追加機能の作成

前述のように、ユーザーのショッピングカートに新しい製品を追加するために使用される、 *Addtocart*という名前の処理ページを作成します。 このページでは、先ほど作成した `ShoppingCart` クラスの `AddToCart` メソッドを呼び出します。 *Addtocart .aspx*ページでは、製品 `ID` が渡されることが予想されます。 この製品 `ID` は、`ShoppingCart` クラスの `AddToCart` メソッドを呼び出すときに使用されます。

> [!NOTE] 
> 
> ページ UI (*Addtocart .aspx*) ではなく、このページの分離コード (*AddToCart.aspx.cs*) を変更します。

#### <a name="to-create-the-add-to-cart-functionality"></a>カートへの追加機能を作成するには、次のようにします。

1. **ソリューションエクスプローラー**で、**ウィング? toys**プロジェクトを右クリックし、[ -の追加] をクリックして &gt;**新しい項目**を**追加**します。  
   **[新しい項目の追加]** ダイアログ ボックスが表示されます。
2. 標準の新しいページ (Web フォーム) を*Addtocart*という名前のアプリケーションに追加します。 

    ![ショッピングカート-Web フォームの追加](shopping-cart/_static/image4.png)
3. **ソリューションエクスプローラー**で、 *addtocart .aspx*ページを右クリックし、[コードの**表示**] をクリックします。 *AddToCart.aspx.cs*分離コードファイルがエディターで開かれます。
4. *AddToCart.aspx.cs*の既存のコードを次のコードに置き換えます。   

    [!code-csharp[Main](shopping-cart/samples/sample4.cs)]

*Addtocart .aspx*ページが読み込まれると、製品 `ID` がクエリ文字列から取得されます。 次に、ショッピングカートクラスのインスタンスが作成され、このチュートリアルの前半で追加した `AddToCart` メソッドを呼び出すために使用されます。 *ShoppingCartActions.cs*ファイルに含まれている `AddToCart` メソッドには、選択した製品をショッピングカートに追加したり、選択した製品の製品数量をインクリメントしたりするロジックが含まれています。 製品がショッピングカートに追加されていない場合は、データベースの `CartItem` テーブルに製品が追加されます。 製品が既にショッピングカートに追加されていて、ユーザーが同じ製品の項目を追加した場合は、`CartItem` テーブルに製品の数量が増分されます。 最後に、ページが ShoppingCart ページにリダイレクトされ*ます*。このページでは、次の手順で追加します。このページには、カート内の項目の更新リストが表示されます。

既に説明したように、特定のユーザーに関連付けられている製品を識別するために、ユーザー `ID` が使用されます。 この `ID` は、ユーザーがショッピングカートに製品を追加するたびに、`CartItem` テーブルの行に追加されます。

### <a name="creating-the-shopping-cart-ui"></a>ショッピングカートの UI の作成

*ShoppingCart*ページには、ユーザーがショッピングカートに追加した製品が表示されます。 また、ショッピングカートのアイテムを追加、削除、および更新する機能も提供されます。

1. **ソリューションエクスプローラー**で、 **[ウィングヒント]** を右クリックし、[ -の**追加**] をクリックして**新しい項目**を &gt; ます。  
   **[新しい項目の追加]** ダイアログ ボックスが表示されます。
2. マスターページを**使用して Web フォーム**を選択し、マスターページを含む新しいページ (web フォーム) を追加します。 新しいページに*ShoppingCart*という名前を指定します。
3. [ **Master] を選択**して、新しく作成*した .aspx*ページにマスターページをアタッチします。
4. *ShoppingCart*ページで、既存のマークアップを次のマークアップに置き換えます。   

    [!code-aspx[Main](shopping-cart/samples/sample5.aspx)]

*ShoppingCart*ページには、`CartList`という名前の**GridView**コントロールが含まれています。 このコントロールは、モデルバインドを使用して、ショッピングカートデータをデータベースから**GridView**コントロールにバインドします。 **GridView**コントロールの `ItemType` プロパティを設定すると、コントロールのマークアップでデータバインディング式 `Item` を使用できるようになり、コントロールが厳密に型指定されます。 このチュートリアルシリーズで前述したように、IntelliSense を使用して `Item` オブジェクトの詳細を選択できます。 モデルバインドを使用してデータを選択するようにデータコントロールを構成するには、コントロールの `SelectMethod` プロパティを設定します。 上のマークアップでは、`CartItem` オブジェクトの一覧を返す GetShoppingCartItems メソッドを使用するように `SelectMethod` を設定します。 **GridView**データコントロールは、ページのライフサイクルの適切なタイミングでメソッドを呼び出し、返されたデータを自動的にバインドします。 `GetShoppingCartItems` メソッドも追加する必要があります。

#### <a name="retrieving-the-shopping-cart-items"></a>ショッピングカートのアイテムを取得しています

次に、 *ShoppingCart.aspx.cs*分離コードにコードを追加して、ショッピングカートの UI を取得して設定します。

1. **ソリューションエクスプローラー**で、 *ShoppingCart*ページを右クリックし、 **[コードの表示]** をクリックします。 *ShoppingCart.aspx.cs*分離コードファイルがエディターで開かれます。
2. 既存のコードを次のコードに置き換えます。  

    [!code-csharp[Main](shopping-cart/samples/sample6.cs)]

前述のように、`GridView` データコントロールは、ページのライフサイクルの適切なタイミングで `GetShoppingCartItems` メソッドを呼び出し、返されたデータを自動的にバインドします。 `GetShoppingCartItems` メソッドは、`ShoppingCartActions` オブジェクトのインスタンスを作成します。 次に、そのインスタンスを使用して、`GetCartItems` メソッドを呼び出すことによって、カート内の項目を返します。

### <a name="adding-products-to-the-shopping-cart"></a>ショッピングカートへの製品の追加

*Productlist .aspx*ページまたは*productlist .aspx*ページが表示されている場合、ユーザーはリンクを使用して製品をショッピングカートに追加できます。 リンクをクリックすると、アプリケーションは*Addtocart*という名前の処理ページに移動します。 *Addtocart .aspx*ページは、このチュートリアルの前の手順で追加した `ShoppingCart` クラスの `AddToCart` メソッドを呼び出します。

次に、[ **add To Cart (カートに追加**)] リンクを*productlist .Aspx*ページと*productlist .aspx*ページの両方に追加します。 このリンクには、データベースから取得された製品 `ID` が含まれます。

1. **ソリューションエクスプローラー**で、 *productlist. .aspx*という名前のページを探して開きます。
2. 次のようにページ全体が表示されるように、黄色で強調表示されているマークアップを*Productlist .aspx*ページに追加します。  

    [!code-aspx[Main](shopping-cart/samples/sample7.aspx?highlight=50-54)]

### <a name="testing-the-shopping-cart"></a>ショッピングカートのテスト

アプリケーションを実行して、ショッピングカートに製品を追加する方法を確認します。

1. **F5** キーを押してアプリケーションを実行します。  
 プロジェクトがデータベースを再作成すると、ブラウザーが開き、 *default.aspx*ページが表示されます。
2. カテゴリナビゲーションメニューから **[車両]** を選択します。  
 [車両] カテゴリに含まれている製品のみを示す*Productlist .aspx*ページが表示されます。 

    ![ショッピングカート-自動車](shopping-cart/_static/image5.png)
3. 一覧表示されている最初の製品 (コンバーチブル車) の横にある **[カートに追加]** リンクをクリックします。   
 *ShoppingCart*ページが表示され、ショッピングカートでの選択内容が表示されます。 

    ![ショッピングカート-カート](shopping-cart/_static/image6.png)
4. カテゴリナビゲーションメニューから **[平面]** を選択して、追加の製品を表示します。
5. 一覧表示されている最初の製品の横にある **[カートに追加]** リンクをクリックします。  
 *ShoppingCart*ページが、追加の項目と共に表示されます。
6. ブラウザーを閉じます。

### <a name="calculating-and-displaying-the-order-total"></a>注文合計の計算と表示

ショッピングカートに製品を追加するだけでなく、`GetTotal` メソッドを `ShoppingCart` クラスに追加し、買い物かごページに注文金額の合計を表示します。

1. **ソリューションエクスプローラー**で、 *Logic*フォルダー内の*ShoppingCartActions.cs*ファイルを開きます。
2. 次のように、クラスが次のように表示されるように、黄色で強調表示されている次の `GetTotal` メソッドを `ShoppingCart` クラスに追加します。   

    [!code-csharp[Main](shopping-cart/samples/sample8.cs?highlight=85-97)]

まず、`GetTotal` メソッドは、ユーザーのショッピングカートの ID を取得します。 次に、製品価格と、カートに記載されている各製品の製品数量を乗算することによって、カートの合計を取得します。

> [!NOTE] 
> 
> 上記のコードでは、null 許容型 "`int?`" を使用しています。 Null 許容型は、基になる型のすべての値を表すことができ、null 値としても使用できます。 詳細については、「 [Null 許容型の使用](https://msdn.microsoft.com/library/2cf62fcy(v=vs.110).aspx)」を参照してください。

### <a name="modify-the-shopping-cart-display"></a>ショッピングカートの表示を変更する

次に、 *ShoppingCart*ページのコードを変更して `GetTotal` メソッドを呼び出し、ページが読み込まれるときにその合計を*ShoppingCart*ページに表示します。

1. **ソリューションエクスプローラー**で、 *ShoppingCart*ページを右クリックし、[コードの**表示**] を選択します。
2. *ShoppingCart.aspx.cs*ファイルで、次のように黄色で強調表示されているコードを追加して、`Page_Load` ハンドラーを更新します。   

    [!code-csharp[Main](shopping-cart/samples/sample9.cs?highlight=16-31)]

*ShoppingCart*ページが読み込まれると、ショッピングカートオブジェクトが読み込まれ、`ShoppingCart` クラスの `GetTotal` メソッドを呼び出すことによって買い物かごの合計が取得されます。 ショッピングカートが空の場合は、その効果に対するメッセージが表示されます。

### <a name="testing-the-shopping-cart-total"></a>ショッピングカートの合計のテスト

今すぐアプリケーションを実行して、ショッピングカートに製品を追加できないようにする方法を確認できますが、ショッピングカートの合計を確認することができます。

1. **F5** キーを押してアプリケーションを実行します。  
 ブラウザーが開き、 *default.aspx*ページが表示されます。
2. カテゴリナビゲーションメニューから **[車両]** を選択します。
3. 最初の製品の横にある **[カートに追加]** リンクをクリックします。   
 *ShoppingCart*ページには、注文総数が表示されます。 

    ![ショッピングカート-カートの合計](shopping-cart/_static/image7.png)
4. 他の製品 (たとえば、平面) をカートに追加します。
5. *ShoppingCart*ページには、追加したすべての製品の合計が表示されます。 

    ![ショッピングカート-複数の製品](shopping-cart/_static/image8.png)
6. ブラウザーウィンドウを閉じて、実行中のアプリを停止します。

### <a name="adding-update-and-checkout-buttons-to-the-shopping-cart"></a>[更新] ボタンと [チェックアウト] ボタンをショッピングカートに追加する

ユーザーがショッピングカートを変更できるようにするには、**更新** ボタンと **チェックアウト** ボタンを ショッピングカート ページに追加します。 このチュートリアルシリーズの後半では、 **[チェックアウト]** ボタンは使用されません。

1. **ソリューションエクスプローラー**で、web アプリケーションプロジェクトのルートにある*ShoppingCart*ページを開きます。
2. **[更新]** ボタンと **[チェックアウト]** ボタンを*ShoppingCart*ページに追加するには、次のコードに示すように、黄色で強調表示されているマークアップを既存のマークアップに追加します。   

    [!code-aspx[Main](shopping-cart/samples/sample10.aspx?highlight=36-45)]

ユーザーが **[更新]** ボタンをクリックすると、`UpdateBtn_Click` イベントハンドラーが呼び出されます。 このイベントハンドラーは、次の手順で追加するコードを呼び出します。

次に、 *ShoppingCart.aspx.cs*ファイルに含まれているコードを更新して、カート項目をループ処理し、`RemoveItem` および `UpdateItem` メソッドを呼び出すことができます。

1. **ソリューションエクスプローラー**で、web アプリケーションプロジェクトのルートにある*ShoppingCart.aspx.cs*ファイルを開きます。
2. 次のコードセクションを黄色で強調表示されている*ShoppingCart.aspx.cs*ファイルに追加します。   

    [!code-csharp[Main](shopping-cart/samples/sample11.cs?highlight=9-11,33,44-89)]

ユーザーが*ShoppingCart*ページの **[Update]** ボタンをクリックすると、UpdateCartItems メソッドが呼び出されます。 UpdateCartItems メソッドは、ショッピングカート内の各項目の更新された値を取得します。 次に、UpdateCartItems メソッドは、`UpdateShoppingCartDatabase` メソッド (次の手順で追加および説明) を呼び出して、ショッピングカートの項目を追加または削除します。 ショッピングカートの更新を反映するようにデータベースを更新すると **、gridview の**`DataBind` メソッドを呼び出すことによって、[ショッピングカート] ページの**gridview**コントロールが更新されます。 また、更新された項目の一覧が反映されるように、ショッピングカートページの合計注文金額も更新されます。

### <a name="updating-and-removing-shopping-cart-items"></a>ショッピングカートのアイテムの更新と削除

*ShoppingCart*ページで、項目の数量を更新したり、項目を削除したりするためのコントロールが追加されていることを確認できます。 ここで、これらのコントロールを機能させるコードを追加します。

1. **ソリューションエクスプローラー**で、 *Logic*フォルダー内の*ShoppingCartActions.cs*ファイルを開きます。
2. 次のコードを黄色で強調表示されている*ShoppingCartActions.cs*クラスファイルに追加します。   

    [!code-csharp[Main](shopping-cart/samples/sample12.cs?highlight=99-213)]

*ShoppingCart.aspx.cs*ページの `UpdateCartItems` メソッドから呼び出される `UpdateShoppingCartDatabase` メソッドには、ショッピングカートの項目を更新または削除するためのロジックが含まれています。 `UpdateShoppingCartDatabase` メソッドは、ショッピングカートリスト内のすべての行を反復処理します。 ショッピングカートアイテムが削除されるようにマークされている場合、または数量が1未満の場合は、`RemoveItem` メソッドが呼び出されます。 そうしないと、`UpdateItem` メソッドが呼び出されたときに、ショッピングカートのアイテムの更新が確認されます。 ショッピングカートアイテムが削除または更新されると、データベースの変更が保存されます。

`ShoppingCartUpdates` 構造は、すべてのショッピングカート項目を保持するために使用されます。 `UpdateShoppingCartDatabase` メソッドは、`ShoppingCartUpdates` 構造を使用して、いずれかの項目を更新または削除する必要があるかどうかを判断します。

次のチュートリアルでは、`EmptyCart` メソッドを使用して、製品を購入した後にショッピングカートをクリアします。 ここでは、 *ShoppingCartActions.cs*ファイルに追加した `GetCount` 方法を使用して、ショッピングカートに含まれる項目の数を確認します。

### <a name="adding-a-shopping-cart-counter"></a>ショッピングカートカウンターを追加する

ショッピングカート内の項目の合計数をユーザーが表示できるようにするには、*サイトのマスター*ページにカウンターを追加します。 このカウンターは、ショッピングカートへのリンクとしても機能します。

1. **ソリューションエクスプローラー***で、[] ページを*開きます。
2. 次のように、黄色で示されているように、ショッピングカートのカウンターリンクをナビゲーションセクションに追加して、マークアップを変更します。  

    [!code-html[Main](shopping-cart/samples/sample13.html?highlight=6)]
3. 次に、次のように、黄色で強調表示されているコードを追加して、 *Site.Master.cs*ファイルの分離コードを更新します。  

    [!code-csharp[Main](shopping-cart/samples/sample14.cs?highlight=11,77-84)]

ページが HTML として表示される前に、`Page_PreRender` イベントが発生します。 `Page_PreRender` ハンドラーでは、ショッピングカートの合計数は、`GetCount` メソッドを呼び出すことによって決定されます。 返された値は、サイトのマークアップに含まれる `cartCount` スパンに追加されます *。* `<span>` タグを使用すると、内部要素を適切にレンダリングできます。 サイトのページが表示されると、ショッピングカートの合計が表示されます。 ユーザーは、ショッピングカートの合計をクリックしてショッピングカートを表示することもできます。

## <a name="testing-the-completed-shopping-cart"></a>完成したショッピングカートのテスト

ここでアプリケーションを実行して、ショッピングカートのアイテムを追加、削除、および更新する方法を確認できます。 ショッピングカートの合計には、ショッピングカート内のすべての品目の合計コストが反映されます。

1. **F5** キーを押してアプリケーションを実行します。  
 ブラウザーが開き、 *default.aspx*ページが表示されます。
2. カテゴリナビゲーションメニューから **[車両]** を選択します。
3. 最初の製品の横にある **[カートに追加]** リンクをクリックします。   
 *ShoppingCart*ページには、注文総数が表示されます。
4. カテゴリナビゲーションメニューから **[平面]** を選択します。
5. 最初の製品の横にある **[カートに追加]** リンクをクリックします。
6. ショッピングカートの最初のアイテムの数量を3に設定し、2番目のアイテムの **[アイテムの削除]** チェックボックスをオンにします。<a id="a"></a>
7. **[更新]** ボタンをクリックして、ショッピングカートページを更新し、新しい注文合計を表示します。 

    ![ショッピングカート-カートの更新](shopping-cart/_static/image9.png)

## <a name="summary"></a>要約

このチュートリアルでは、Wingtip Toys Web Forms サンプルアプリケーション用のショッピングカートを作成しました。 このチュートリアルでは、Code First、データ注釈、厳密に型指定されたデータコントロール、およびモデルバインド Entity Framework を使用しました。

ショッピングカートでは、ユーザーが購入対象として選択した項目の追加、削除、および更新がサポートされています。 ショッピングカートの機能を実装するだけでなく、 **GridView**コントロールにショッピングカートのアイテムを表示し、注文の合計を計算する方法についても説明しました。

## <a name="addition-information"></a>追加情報

[ASP.NET セッション状態の概要](https://msdn.microsoft.com/library/ms178581.aspx)

> [!div class="step-by-step"]
> [前へ](display_data_items_and_details.md)
> [次へ](checkout-and-payment-with-paypal.md)
