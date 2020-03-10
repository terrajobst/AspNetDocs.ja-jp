---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-7
title: ビューを作成する (UI) |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: b2445062-a1fe-4133-8994-f510280f6d9a
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-7
msc.type: authoredcontent
ms.openlocfilehash: 62c4523c2c6fb399cfbc3716309a1379996d601c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448984"
---
# <a name="create-the-view-ui"></a>ビューの作成 (UI)

[Mike Wasson](https://github.com/MikeWasson)

[完成したプロジェクトのダウンロード](https://github.com/MikeWasson/BookService)

このセクションでは、アプリの HTML の定義を開始し、HTML とビューモデルの間にデータバインディングを追加します。

Views/Home/Index. cshtml というファイルを開きます。 そのファイルの内容全体を次の内容に置き換えます。

[!code-cshtml[Main](part-7/samples/sample1.cshtml)]

`div` の要素のほとんどは、[ブートストラップ](http://getbootstrap.com/)のスタイルを設定するために用意されています。 重要な要素は、`data-bind` 属性を持つ要素です。 この属性は、HTML をビューモデルにリンクします。

次に例を示します。

[!code-html[Main](part-7/samples/sample2.html)]

この例では、&quot;`text`&quot; のバインドによって、`<p>` 要素によって、ビューモデルからの `error` プロパティの値が表示されます。 `error` が `ko.observable`として宣言されていることを思い出してください。

[!code-javascript[Main](part-7/samples/sample3.js)]

新しい値が `error`に割り当てられるたびに、`<p>` 要素内のテキストがノックアウトによって更新されます。

`foreach` binding は、`books` 配列の内容をループするようにノックアウトに指示します。 ノックアウトは、配列内の各項目に対して新しい &lt;li&gt; 要素を作成します。 `foreach` のコンテキスト内のバインディングは、配列項目のプロパティを参照します。 次に例を示します。

[!code-html[Main](part-7/samples/sample4.html)]

ここでは、`text` バインドは各書籍の Author プロパティを読み取ります。

ここでアプリケーションを実行すると、次のようになります。

![](part-7/_static/image1.png)

ページが読み込まれた後、ブックの一覧が非同期に読み込まれます。 現時点では、&quot;の詳細&quot; リンクは機能していません。 次のセクションでは、この機能を追加します。

> [!div class="step-by-step"]
> [前へ](part-6.md)
> [次へ](part-8.md)
