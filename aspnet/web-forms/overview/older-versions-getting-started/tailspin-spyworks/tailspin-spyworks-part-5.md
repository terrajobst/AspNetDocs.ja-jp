---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-5
title: 'パート 5: ビジネスロジック |Microsoft Docs'
author: JoeStagner
description: このチュートリアルシリーズでは、Tailspin Spyworks サンプルアプリケーションを構築するために実行するすべての手順について詳しく説明します。 パート5では、ビジネスロジックを追加します。
ms.author: riande
ms.date: 07/21/2010
ms.assetid: eaef475a-ca91-47ea-a4a7-d074005ed80c
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-5
msc.type: authoredcontent
ms.openlocfilehash: c60eece9223c47304786d7b0d0ca4b11ac0572e9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78511546"
---
# <a name="part-5-business-logic"></a>パート 5: ビジネスロジック

[Joe Stagner](https://github.com/JoeStagner)

> Tailspin Spyworks は、.NET プラットフォーム用の強力でスケーラブルなアプリケーションを簡単に作成する方法を示しています。 ASP.NET 4 の優れた新機能を使用して、ショッピング、チェックアウト、管理などのオンラインストアを構築する方法を示しています。
> 
> このチュートリアルシリーズでは、Tailspin Spyworks サンプルアプリケーションを構築するために実行するすべての手順について詳しく説明します。 パート5では、ビジネスロジックを追加します。

## <a id="_Toc260221671"></a>ビジネスロジックの追加

だれかが web サイトにアクセスするたびに、ショッピング体験を利用できるようにしたいと考えています。 訪問者は、登録されていない、またはログインしていない場合でも、商品を閲覧してショッピングカートに追加することができます。 チェックアウトの準備ができたら、認証するオプションが付与され、まだメンバーでない場合はアカウントを作成できるようになります。

これは、ショッピングカートを匿名状態から "登録済みユーザー" 状態に変換するロジックを実装する必要があることを意味します。

"Classes" という名前のディレクトリを作成し、フォルダーを右クリックして、MyShoppingCart.cs という名前の新しい "Class" ファイルを作成してみましょう。

![](tailspin-spyworks-part-5/_static/image1.jpg)

![](tailspin-spyworks-part-5/_static/image1.png)

前述のように、MyShoppingCart ページを実装するクラスを拡張します。これはを使用して行います。NET の強力な "部分クラス" コンストラクト。

MyShoppingCart.aspx.cf ファイルに対して生成された呼び出しは、次のようになります。

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample1.cs)]

"Partial" キーワードが使用されていることに注意してください。

生成したクラスファイルは次のようになります。

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample2.cs)]

このファイルに partial キーワードを追加して、実装をマージします。

新しいクラスファイルは次のようになります。

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample3.cs)]

クラスに追加する最初のメソッドは、"AddItem" メソッドです。 これは、ユーザーが製品リストおよび製品の詳細ページの [追加] リンクをクリックしたときに最終的に呼び出されるメソッドです。

ページの先頭にある using ステートメントに以下を追加します。

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample4.cs)]

次に、このメソッドを MyShoppingCart クラスに追加します。

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample5.cs)]

LINQ to Entities を使用して、項目が既にカートに存在するかどうかを確認しています。 その場合は、アイテムの注文数量を更新します。それ以外の場合は、選択したアイテムの新しいエントリを作成します。

このメソッドを呼び出すには、このメソッドをクラスにするだけでなく、項目が追加された後に現在のショッピング a = カートを表示する AddToCart .aspx ページを実装します。

ソリューションエクスプローラーでソリューション名を右クリックし、前に行ったように、AddToCart という名前の新しいページを追加します。

このページを使用して、低在庫の問題などの中間結果を表示できますが、この実装では、実際にはページがレンダリングされず、代わりに "Add" ロジックとリダイレクトが呼び出されます。

これを実現するには、次のコードをページ\_Load イベントに追加します。

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample6.cs)]

ここでは、クエリ文字列パラメーターからショッピングカートに追加し、クラスの AddItem メソッドを呼び出すために製品を取得していることに注意してください。

エラーが検出されなかった場合は、次に完全に実装する SHoppingCart ページに制御が渡されます。 エラーが発生した場合は、例外をスローします。

現在、グローバルエラーハンドラーが実装されていないため、この例外はアプリケーションによって処理されませんが、この問題はすぐに解決されます。

また、ステートメント Debug. Fail () を使用することもできます (`using System.Diagnostics;)`

アプリケーションがデバッガー内で実行されている場合、このメソッドは、指定したエラーメッセージと共に、アプリケーションの状態に関する詳細なダイアログを表示します。

運用環境で実行する場合、Debug. Fail () ステートメントは無視されます。

上記のコードでは、ショッピングカートのクラス名 "GetShoppingCartId" 内のメソッドの呼び出しを確認します。

次のように、メソッドを実装するコードを追加します。

また、[更新] ボタンと [チェックアウト] ボタン、および "合計" というカートを表示できるラベルも追加されています。

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample7.cs)]

ショッピングカートに商品を追加できるようになりましたが、製品が追加された後にカートを表示するためのロジックが実装されていません。

そのため、MyShoppingCart ページで、次のように EntityDataSource コントロールと Grid e コントロールを追加します。

[!code-aspx[Main](tailspin-spyworks-part-5/samples/sample8.aspx)]

[Update カート] ボタンをダブルクリックして、マークアップ内の宣言で指定されている click イベントハンドラーを生成できるように、デザイナーでフォームを呼び出します。

後で詳細を実装しますが、これを行うと、エラーなしでアプリケーションをビルドして実行できるようになります。

アプリケーションを実行してショッピングカートに項目を追加すると、これが表示されます。

![](tailspin-spyworks-part-5/_static/image2.jpg)

ここでは、3つのカスタム列を実装して、"既定" のグリッド表示から逸脱しています。

1つ目は、数量の編集可能な "バインド" フィールドです。

[!code-aspx[Main](tailspin-spyworks-part-5/samples/sample9.aspx)]

次に示すのは、行アイテムの合計を表示する "計算された" 列 (注文する品目のコスト) です。

[!code-aspx[Main](tailspin-spyworks-part-5/samples/sample10.aspx)]

最後に、ユーザーがショッピンググラフから項目を削除することを示す CheckBox コントロールを含むカスタム列が用意されています。

[!code-aspx[Main](tailspin-spyworks-part-5/samples/sample11.aspx)]

![](tailspin-spyworks-part-5/_static/image3.jpg)

ご覧のように、注文の合計行は空であるため、注文合計を計算するロジックを追加してみましょう。

まず、MyShoppingCart クラスに "GetTotal" メソッドを実装します。

MyShoppingCart.cs ファイルで、次のコードを追加します。

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample12.cs)]

次に、ページ\_Load イベントハンドラーで GetTotal メソッドを呼び出すことができます。 同時に、ショッピングカートが空かどうかを確認するテストを追加し、必要に応じて表示を調整します。

ショッピングカートが空の場合、次のようになります。

![](tailspin-spyworks-part-5/_static/image4.jpg)

そうでない場合は、合計が表示されます。

![](tailspin-spyworks-part-5/_static/image5.jpg)

ただし、このページはまだ完了していません。

購入カートを再計算するには、追加のロジックが必要になります。削除のマークが付けられた項目を削除し、ユーザーがグリッド内で変更された可能性のある新しい数量の値を確認します。

MyShoppingCart.cs のショッピングカートクラスに "RemoveItem" メソッドを追加して、ユーザーが項目を削除対象としてマークした場合に対処できるようにします。

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample13.cs)]

ここで、ユーザーが GridView での品質を変更するだけの状況を処理するメソッドを ad に渡します。

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample14.cs)]

基本的な削除機能と更新機能を使用すると、データベース内のショッピングカートを実際に更新するロジックを実装できます。 (MyShoppingCart.cs 内)

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample15.cs)]

このメソッドには2つのパラメーターが必要であることに注意してください。 1つはショッピングカート Id で、もう1つはユーザー定義型のオブジェクトの配列です。

そのため、ユーザーインターフェイスの詳細に対するロジックの依存関係を最小限に抑えるために、GridView コントロールに直接アクセスする必要のないメソッドを使用せずに、ショッピングカートの項目をコードに渡すために使用できるデータ構造を定義しました。

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample16.cs)]

MyShoppingCart.aspx.cs ファイルでは、次のように、[更新] ボタンの [イベントハンドラー] でこの構造を使用できます。 カートの更新に加えて、カートの合計も更新されることに注意してください。

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample17.cs)]

特に次のコード行に注目してください。

[!code-javascript[Main](tailspin-spyworks-part-5/samples/sample18.js)]

GetValues () は、次のように MyShoppingCart.aspx.cs に実装する特別なヘルパー関数です。

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample19.cs)]

これにより、GridView コントロールのバインドされた要素の値にアクセスするためのクリーンな方法が提供されます。 [項目の削除] チェックボックスコントロールはバインドされていないため、FindControl () メソッドを使用してアクセスします。

プロジェクトの開発のこの段階では、チェックアウトプロセスを実装する準備が整います。

これを行う前に、Visual Studio を使用してメンバーシップデータベースを生成し、メンバーシップリポジトリにユーザーを追加してみましょう。

> [!div class="step-by-step"]
> [前へ](tailspin-spyworks-part-4.md)
> [次へ](tailspin-spyworks-part-6.md)
