---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-8
title: 'パート 8: Ajax 更新プログラムを使用したショッピングカート |Microsoft Docs'
author: jongalloway
description: このチュートリアルシリーズでは、ASP.NET MVC ミュージックストアサンプルアプリケーションをビルドするために実行するすべての手順について詳しく説明します。 パート8では、Ajax の更新プログラムを使用したショッピングカートについて説明します。
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 26b2f55e-ed42-4277-89b0-c941eb754145
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-8
msc.type: authoredcontent
ms.openlocfilehash: 89897ad41b217764cbd17317d4bf5d6a5c5d488f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78433516"
---
# <a name="part-8-shopping-cart-with-ajax-updates"></a>パート 8: Ajax 更新プログラムを使用したショッピングカート

( [Jon Galloway](https://github.com/jongalloway) )

> MVC Music Store は、ASP.NET MVC と Visual Studio を使用して web 開発を行う方法を紹介したチュートリアルアプリケーションです。  
>   
> MVC ミュージックストアは、音楽アルバムをオンラインで販売し、基本的なサイト管理、ユーザーサインイン、およびショッピングカート機能を実装する軽量のサンプルストア実装です。  
>   
> このチュートリアルシリーズでは、ASP.NET MVC ミュージックストアサンプルアプリケーションをビルドするために実行するすべての手順について詳しく説明します。 パート8では、Ajax の更新プログラムを使用したショッピングカートについて説明します。

ユーザーは登録せずにカートにアルバムを配置することができますが、チェックアウトを完了するにはゲストとして登録する必要があります。 ショッピングとチェックアウトのプロセスは2つのコントローラーに分けられます。 ShoppingCart コントローラーは、項目をカートに匿名で追加できるようにし、チェックアウトプロセスを処理するチェックアウトコントローラーです。 このセクションのショッピングカートから始めて、次のセクションでチェックアウトプロセスを作成します。

## <a name="adding-the-cart-order-and-orderdetail-model-classes"></a>カート、注文、および OrderDetail モデルクラスの追加

ショッピングカートとチェックアウトプロセスでは、いくつかの新しいクラスを使用します。 [モデル] フォルダーを右クリックし、次のコードを使用してカートクラス (Cart.cs) を追加します。

[!code-csharp[Main](mvc-music-store-part-8/samples/sample1.cs)]

このクラスは、これまでに使用した他のクラスと非常によく似ています。ただし、RecordId プロパティの [Key] 属性は例外です。 カートの項目には、匿名ショッピングを許可する CartID という名前の文字列識別子がありますが、テーブルには RecordId という整数の主キーが含まれています。 慣例として、Entity Framework コードでは、買い物かごという名前のテーブルの主キーが CartId または ID のいずれかであることを前提としていますが、必要に応じて、注釈やコードを使用して簡単にオーバーライドできます。 この例では、Entity Framework コードで単純な規則を使用する方法について説明していますが、これらの規則に違反している場合は、これらの規則によって制限されません。

次に、次のコードを使用して Order クラス (Order.cs) を追加します。

[!code-csharp[Main](mvc-music-store-part-8/samples/sample2.cs)]

このクラスは、注文の概要および配信情報を追跡します。 まだ作成されていないクラスに依存する OrderDetails ナビゲーションプロパティがあるため、**まだコンパイルされません**。 ここで、OrderDetail.cs という名前のクラスを追加して、次のコードを追加して修正してみましょう。

[!code-csharp[Main](mvc-music-store-part-8/samples/sample3.cs)]

これらの新しいモデルクラスを公開する DbSets を追加するために、MusicStoreEntities クラスに対して1つの最後の更新を行います。これには、Dbsets&lt;アーティスト&gt;も含まれます。 更新された MusicStoreEntities クラスは次のようになります。

[!code-csharp[Main](mvc-music-store-part-8/samples/sample4.cs)]

## <a name="managing-the-shopping-cart-business-logic"></a>ショッピングカートのビジネスロジックを管理する

次に、[モデル] フォルダーに ShoppingCart クラスを作成します。 ShoppingCart モデルは、カートテーブルへのデータアクセスを処理します。 さらに、ショッピングカートのアイテムを追加および削除するために、ビジネスロジックを処理します。

ショッピングカートに商品を追加するだけで、アカウントにサインアップするようにユーザーに要求しないので、ユーザーがショッピングカートにアクセスするときに、ユーザーに対して一時的な一意識別子 (GUID を使用) またはグローバル一意識別子を割り当てます。 この ID は、ASP.NET Session クラスを使用して格納します。

*注: ASP.NET セッションは、ユーザー固有の情報を格納するのに便利な場所であり、サイトから離れた後に期限切れになります。より大きなサイトでは、セッション状態の誤用によってパフォーマンスが低下する可能性があります。*

ShoppingCart クラスは、次のメソッドを公開します。

**Addtocart**は、アルバムをパラメーターとして受け取り、それをユーザーのカートに追加します。 カートテーブルでは、各アルバムの数量が追跡されるため、必要に応じて新しい行を作成するロジックや、ユーザーが既にアルバムのコピーを注文している場合は数量を増やすことができます。

**Removefromcart**は、アルバム ID を取得し、ユーザーのカートから削除します。 カートにアルバムのコピーが1つしかない場合、その行は削除されます。

**Emptycart**は、ユーザーのショッピングカートからすべての項目を削除します。

**GetCartItems**は、表示または処理のために CartItems の一覧を取得します。

**GetCount**は、ユーザーがショッピングカートに持っているアルバムの合計数を取得します。

**Gettotal**は、カート内のすべての品目の総コストを計算します。

**Createorder**は、チェックアウトフェーズ中にショッピングカートを注文に変換します。

**Getcart**は、コントローラーがカートオブジェクトを取得できるようにする静的メソッドです。 **Getcartid**メソッドを使用して、ユーザーのセッションからの cartid の読み取りを処理します。 GetCartId メソッドでは HttpContextBase が必要であるため、ユーザーのセッションからユーザーの CartId を読み取ることができます。

完全な**ShoppingCart クラス**を次に示します。

[!code-csharp[Main](mvc-music-store-part-8/samples/sample5.cs)]

## <a name="viewmodels"></a>ViewModels

ショッピングカートコントローラーは、モデルオブジェクトに完全にマップされない複雑な情報をビューに伝達する必要があります。 ビューに合わせてモデルを変更する必要はありません。モデルクラスは、ユーザーインターフェイスではなく、ドメインを表す必要があります。 1つの解決策は、ストアマネージャーのドロップダウン情報の場合と同様に、ViewBag クラスを使用して情報をビューに渡すことですが、ViewBag を介して大量の情報を渡すと管理が困難になります。

これを解決するには、*ビューモデル*パターンを使用します。 このパターンを使用すると、特定のビューシナリオ用に最適化された、厳密に型指定されたクラスを作成し、ビューテンプレートに必要な動的な値/コンテンツのプロパティを公開します。 次に、コントローラークラスを設定して、ビューに最適化されたこれらのクラスをビューテンプレートに渡して使用できるようにします。 これにより、ビューテンプレート内でタイプセーフ、コンパイル時チェック、およびエディター IntelliSense が有効になります。

ショッピングカートコントローラーで使用する2つのビューモデルを作成します。 ShoppingCartViewModel はユーザーのショッピングカートの内容を保持し、ユーザーが何かを削除したときに、ShoppingCartRemoveViewModel を使用して確認情報を表示します。カートから

プロジェクトのルートに新しい Viewmodel フォルダーを作成して、整理しておきましょう。 プロジェクトを右クリックし、[追加]、[新しいフォルダー] の順に選択します。

![](mvc-music-store-part-8/_static/image1.jpg)

フォルダーに Viewmodel という名前を指定します。

![](mvc-music-store-part-8/_static/image1.png)

次に、Viewmodel フォルダーに ShoppingCartViewModel クラスを追加します。 2つのプロパティがあります。カート項目のリストと、カート内のすべての品目の合計価格を保持する10進値です。

[!code-csharp[Main](mvc-music-store-part-8/samples/sample6.cs)]

次の4つのプロパティを使用して、ShoppingCartRemoveViewModel を Viewmodel フォルダーに追加します。

[!code-csharp[Main](mvc-music-store-part-8/samples/sample7.cs)]

## <a name="the-shopping-cart-controller"></a>ショッピングカートコントローラー

ショッピングカートコントローラーには主に3つの目的があります。カートへのアイテムの追加、カートからのアイテムの削除、およびカート内のアイテムの表示です。 ここで作成した3つのクラス (ShoppingCartViewModel、ShoppingCartRemoveViewModel、および ShoppingCart) が使用されます。 StoreController と StoreManagerController のように、MusicStoreEntities のインスタンスを保持するフィールドを追加します。

空のコントローラーテンプレートを使用して、新しいショッピングカートコントローラーをプロジェクトに追加します。

![](mvc-music-store-part-8/_static/image2.png)

完全な ShoppingCart コントローラーを次に示します。 インデックスとコントローラーの追加アクションは非常によく似ています。 Remove と CartSummary controller アクションは2つの特殊なケースを処理します。これについては、次のセクションで説明します。

[!code-csharp[Main](mvc-music-store-part-8/samples/sample8.cs)]

## <a name="ajax-updates-with-jquery"></a>JQuery を使用した Ajax の更新

次に、ShoppingCartViewModel に厳密に型指定されたショッピングカートのインデックスページを作成し、前と同じ方法を使用してリストビューテンプレートを使用します。

![](mvc-music-store-part-8/_static/image3.png)

ただし、Html.actionlink を使用してカートから項目を削除するのではなく、jQuery を使用して、このビュー内のすべてのリンク (HTML クラス RemoveLink を含む) に対して click イベントを "接続" します。 フォームを送信するのではなく、この click イベントハンドラーは、RemoveFromCart コントローラーアクションへの AJAX コールバックを行います。 RemoveFromCart は、JSON でシリアル化された結果を返します。この結果、jQuery コールバックは次に jQuery を使用して、このページに対して4つのクイック更新を解析して実行します。

- 1. 削除されたアルバムを一覧から削除します。
- 2. ヘッダーのカート数を更新します
- 3. ユーザーに更新メッセージを表示します
- 4. カートの合計価格を更新します。

削除シナリオは、インデックスビュー内の Ajax コールバックによって処理されるため、RemoveFromCart アクションの追加のビューは必要ありません。 /ShoppingCart/Index ビューの完全なコードを次に示します。

[!code-cshtml[Main](mvc-music-store-part-8/samples/sample9.cshtml)]

これをテストするには、ショッピングカートに商品を追加できるようにする必要があります。 **店舗の詳細** ビューを更新して、カートに追加 ボタンを含めます。 ここでは、このビューを最後に更新した後に追加したアルバムの追加情報 (ジャンル、アーティスト、価格、アルバムアート) を含めることができます。 次に示すように、更新されたストアの詳細ビューのコードが表示されます。

[!code-cshtml[Main](mvc-music-store-part-8/samples/sample10.cshtml)]

これで、ストアをクリックして、ショッピングカートに対するアルバムの追加と削除をテストできます。 アプリケーションを実行し、ストアインデックスを参照します。

![](mvc-music-store-part-8/_static/image4.png)

次に、ジャンルをクリックして、アルバムの一覧を表示します。

![](mvc-music-store-part-8/_static/image5.png)

アルバムのタイトルをクリックすると、[カートに追加] ボタンを含む、更新されたアルバムの詳細ビューが表示されるようになります。

![](mvc-music-store-part-8/_static/image6.png)

[カートに追加] ボタンをクリックすると、ショッピングカートのインデックスビューがショッピングカートの概要リストと共に表示されます。

![](mvc-music-store-part-8/_static/image7.png)

ショッピングカートを読み込んだ後、[カートから削除] リンクをクリックすると、お客様のショッピングカートの Ajax 更新を確認できます。

![](mvc-music-store-part-8/_static/image8.png)

登録されていないユーザーがカートに項目を追加できるようにする、実用的なショッピングカートを構築しました。 次のセクションでは、チェックアウトプロセスの登録と完了を許可します。

> [!div class="step-by-step"]
> [前へ](mvc-music-store-part-7.md)
> [次へ](mvc-music-store-part-9.md)
