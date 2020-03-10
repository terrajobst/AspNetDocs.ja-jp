---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-9
title: 新しい項目をデータベースに追加します |。Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 0967c29e-e124-4db0-a788-c45d0ff5aff2
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-9
msc.type: authoredcontent
ms.openlocfilehash: 692269a2c11e529af78f24feca74bba704b5b54b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448972"
---
# <a name="add-a-new-item-to-the-database"></a>新しい項目をデータベースに追加する

[Mike Wasson](https://github.com/MikeWasson)

[完成したプロジェクトのダウンロード](https://github.com/MikeWasson/BookService)

このセクションでは、ユーザーが新しいブックを作成する機能を追加します。 App.config で、ビューモデルに次のコードを追加します。

[!code-javascript[Main](part-9/samples/sample1.js)]

Index. cshtml で、次のマークアップを置き換えます。

[!code-html[Main](part-9/samples/sample2.html)]

置換後のコード:

[!code-html[Main](part-9/samples/sample3.html)]

このマークアップは、新しい作成者を送信するためのフォームを作成します。 [作成者] ドロップダウンリストの値は、ビューモデルで監視可能な `authors` にデータバインドされます。 その他のフォーム入力の場合、値はビューモデルの `newBook` プロパティにデータバインドされます。

フォームの submit ハンドラーは、`addBook` 関数にバインドされます。

[!code-html[Main](part-9/samples/sample4.html)]

`addBook` 関数は、JSON オブジェクトを作成するために、データバインドフォーム入力の現在の値を読み取ります。 次に、JSON オブジェクトを `/api/books`にポストします。

> [!div class="step-by-step"]
> [前へ](part-8.md)
> [次へ](part-10.md)
