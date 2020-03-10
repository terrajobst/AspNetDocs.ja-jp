---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-8
title: 項目の詳細を表示する |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 75ef94b1-bbec-4681-9210-452dba816144
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-8
msc.type: authoredcontent
ms.openlocfilehash: 3f48c5ad73ceb9a4873fbbb621b518553a498966
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449002"
---
# <a name="display-item-details"></a>作業項目の表示

[Mike Wasson](https://github.com/MikeWasson)

[完成したプロジェクトのダウンロード](https://github.com/MikeWasson/BookService)

このセクションでは、各ブックの詳細を表示する機能を追加します。 App.config で、ビューモデルに次のコードを追加します。

[!code-javascript[Main](part-8/samples/sample1.js)]

Views/Home/Index. cshtml で、データバインド要素を Details リンクに追加します。

[!code-html[Main](part-8/samples/sample2.html?highlight=5)]

これにより、&gt; 要素 &lt;のクリックハンドラーがビューモデルの `getBookDetail` 関数にバインドされます。

同じファイルで、次のマークアップを置き換えます。

[!code-html[Main](part-8/samples/sample3.html)]

以下に置き換えます。

[!code-html[Main](part-8/samples/sample4.html)]

このマークアップは、ビューモデルで監視可能な `detail` のプロパティにデータバインドされたテーブルを作成します。

"&lt;!--ko--&gt;&quot; 構文では、DOM 要素の外側にあるノックアウトバインドを含めることができます。 この場合、`if` バインドを使用すると、`details` が null 以外の場合にのみ、マークアップのこのセクションが表示されます。

[!code-html[Main](part-8/samples/sample5.html)]

アプリを実行して &quot;詳細&quot; リンクのいずれかをクリックすると、アプリにブックの詳細が表示されます。

[![](part-8/_static/image2.png)](part-8/_static/image1.png)

> [!div class="step-by-step"]
> [前へ](part-7.md)
> [次へ](part-9.md)
