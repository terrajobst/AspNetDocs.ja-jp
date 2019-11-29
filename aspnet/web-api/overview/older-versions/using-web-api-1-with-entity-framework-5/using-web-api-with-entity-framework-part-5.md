---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-5
title: 'パート 5: ノックアウトを使用した動的 UI の作成 |Microsoft Docs'
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: 9d9cb3b0-f4a7-434e-a508-9fc0ad0eb813
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-5
msc.type: authoredcontent
ms.openlocfilehash: bbdeba756de7986cfeb92aa10a57f4f101382f99
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599996"
---
# <a name="part-5-creating-a-dynamic-ui-with-knockoutjs"></a>パート 5: ノックアウトを使用した動的 UI の作成

[Mike Wasson](https://github.com/MikeWasson)

[完成したプロジェクトのダウンロード](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="creating-a-dynamic-ui-with-knockoutjs"></a>Knockout.js で動的 UI を作成する

このセクションでは、ノックアウトを使用して管理ビューに機能を追加します。

[ノックアウト](http://knockoutjs.com/)は、HTML コントロールを簡単にデータにバインドできる Javascript ライブラリです。 ノックアウトは、モデルビュービューモデル (MVVM) パターンを使用します。

- この*モデル*は、ビジネスドメイン内のデータ (ここでは、製品と注文) のサーバー側表現です。
- *ビュー*はプレゼンテーション層 (HTML) です。
- *ビューモデル*は、モデルデータを保持する Javascript オブジェクトです。 ビューモデルは、UI のコード抽象化です。 HTML 表現に関する情報はありません。 代わりに、"項目のリスト" など、ビューの抽象的な機能を表します。

ビューは、ビューモデルにデータバインドされています。 ビューモデルに対する更新は、自動的にビューに反映されます。 ビューモデルでは、ボタンのクリックなど、ビューからイベントを取得したり、注文の作成など、モデルに対する操作を実行したりすることもできます。

![](using-web-api-with-entity-framework-part-5/_static/image1.png)

まず、ビューモデルを定義します。 その後、HTML マークアップをビューモデルにバインドします。

次の Razor セクションを Admin. cshtml に追加します。

[!code-cshtml[Main](using-web-api-with-entity-framework-part-5/samples/sample1.cshtml)]

このセクションは、ファイルの任意の場所に追加できます。 ビューが表示されると、HTML ページの下部に、終了 &lt;/本文&gt; タグの直前に、セクションが表示されます。

このページのすべてのスクリプトは、コメントで示されているスクリプトタグ内に表示されます。

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample2.html)]

まず、ビューモデルクラスを定義します。

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample3.js)]

**ko**は、"*観測*可能" と呼ばれる、ノックアウトの特殊なオブジェクトです。 [ノックアウトドキュメント](http://knockoutjs.com/documentation/observables.html)から: 観測可能なは、変更についてサブスクライバーに通知できる "JavaScript オブジェクト" です。 監視可能な変更の内容が一致するように、ビューが自動的に更新されます。

`products` 配列にデータを設定するには、web API に対して AJAX 要求を行います。 API のベース URI がビューバッグに格納されていることを思い出してください (チュートリアルの[パート 4](using-web-api-with-entity-framework-part-4.md)を参照してください)。

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample4.js?highlight=5)]

次に、ビューモデルに関数を追加して、製品を作成、更新、および削除します。 これらの関数は、AJAX 呼び出しを web API に送信し、結果を使用してビューモデルを更新します。

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample5.js?highlight=7)]

ここで最も重要なのは、DOM が非常に読み込まれるときに、 **ko**関数を呼び出し、`ProductsViewModel`の新しいインスタンスを渡すことです。

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample6.js)]

**Ko**メソッドは、ノックアウトをアクティブにし、ビューモデルをビューに配線します。

ビューモデルが用意できたので、次にバインドを作成します。 これを行うには、`data-bind` 属性を HTML 要素に追加します。 たとえば、HTML リストを配列にバインドするには、`foreach` バインドを使用します。

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample7.html?highlight=1)]

`foreach` バインディングは配列を反復処理し、配列内の各オブジェクトに対して子要素を作成します。 子要素のバインドは、配列オブジェクトのプロパティを参照できます。

次のバインドを "更新-製品" リストに追加します。

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample8.html)]

`<li>` 要素は、 **foreach**バインドのスコープ内で発生します。 つまり、抜き合わせは、`products` 配列内の製品ごとに1回要素をレンダリングします。 `<li>` 要素内のすべてのバインドは、その製品インスタンスを参照します。 たとえば、`$data.Name` は、製品の `Name` プロパティを参照します。

テキスト入力の値を設定するには、`value` バインドを使用します。 これらのボタンは、`click` バインディングを使用して、モデルビューの関数にバインドされます。 製品インスタンスは、各関数にパラメーターとして渡されます。 詳細については、さまざまなバインドについての適切な説明を[ノックアウトドキュメント](http://knockoutjs.com/documentation/observables.html)に記載しています。

次に、[製品の追加] フォームで**submit**イベントのバインドを追加します。

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample9.html)]

このバインディングは、ビューモデルの `create` 関数を呼び出して、新しい製品を作成します。

管理ビューの完全なコードを次に示します。

[!code-cshtml[Main](using-web-api-with-entity-framework-part-5/samples/sample10.cshtml)]

アプリケーションを実行し、管理者アカウントでログインして、[Admin] \ (管理者 \) リンクをクリックします。 製品の一覧が表示され、製品を作成、更新、または削除できるようになります。

> [!div class="step-by-step"]
> [前へ](using-web-api-with-entity-framework-part-4.md)
> [次へ](using-web-api-with-entity-framework-part-6.md)
