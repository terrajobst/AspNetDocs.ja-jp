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
# <a name="add-a-new-item-to-the-database"></a><span data-ttu-id="ac973-102">新しい項目をデータベースに追加する</span><span class="sxs-lookup"><span data-stu-id="ac973-102">Add a New Item to the Database</span></span>

<span data-ttu-id="ac973-103">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="ac973-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="ac973-104">完成したプロジェクトのダウンロード</span><span class="sxs-lookup"><span data-stu-id="ac973-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="ac973-105">このセクションでは、ユーザーが新しいブックを作成する機能を追加します。</span><span class="sxs-lookup"><span data-stu-id="ac973-105">In this section, you will add the ability for users to create a new book.</span></span> <span data-ttu-id="ac973-106">App.config で、ビューモデルに次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="ac973-106">In app.js, add the following code to the view model:</span></span>

[!code-javascript[Main](part-9/samples/sample1.js)]

<span data-ttu-id="ac973-107">Index. cshtml で、次のマークアップを置き換えます。</span><span class="sxs-lookup"><span data-stu-id="ac973-107">In Index.cshtml, replace the following markup:</span></span>

[!code-html[Main](part-9/samples/sample2.html)]

<span data-ttu-id="ac973-108">置換後のコード:</span><span class="sxs-lookup"><span data-stu-id="ac973-108">With:</span></span>

[!code-html[Main](part-9/samples/sample3.html)]

<span data-ttu-id="ac973-109">このマークアップは、新しい作成者を送信するためのフォームを作成します。</span><span class="sxs-lookup"><span data-stu-id="ac973-109">This markup creates a form for submitting a new author.</span></span> <span data-ttu-id="ac973-110">[作成者] ドロップダウンリストの値は、ビューモデルで監視可能な `authors` にデータバインドされます。</span><span class="sxs-lookup"><span data-stu-id="ac973-110">The values for the author drop-down list are data-bound to the `authors` observable in the view model.</span></span> <span data-ttu-id="ac973-111">その他のフォーム入力の場合、値はビューモデルの `newBook` プロパティにデータバインドされます。</span><span class="sxs-lookup"><span data-stu-id="ac973-111">For the other form inputs, the values are data-bound to the `newBook` property of the view model.</span></span>

<span data-ttu-id="ac973-112">フォームの submit ハンドラーは、`addBook` 関数にバインドされます。</span><span class="sxs-lookup"><span data-stu-id="ac973-112">The submit handler on the form is bound to the `addBook` function:</span></span>

[!code-html[Main](part-9/samples/sample4.html)]

<span data-ttu-id="ac973-113">`addBook` 関数は、JSON オブジェクトを作成するために、データバインドフォーム入力の現在の値を読み取ります。</span><span class="sxs-lookup"><span data-stu-id="ac973-113">The `addBook` function reads the current values of the data-bound form inputs to create a JSON object.</span></span> <span data-ttu-id="ac973-114">次に、JSON オブジェクトを `/api/books`にポストします。</span><span class="sxs-lookup"><span data-stu-id="ac973-114">Then it POSTs the JSON object to `/api/books`.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="ac973-115">[前へ](part-8.md)
> [次へ](part-10.md)</span><span class="sxs-lookup"><span data-stu-id="ac973-115">[Previous](part-8.md)
[Next](part-10.md)</span></span>
