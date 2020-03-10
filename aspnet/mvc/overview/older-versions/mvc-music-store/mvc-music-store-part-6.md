---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-6
title: 'パート 6: モデルの検証にデータ注釈を使用する |Microsoft Docs'
author: jongalloway
description: このチュートリアルシリーズでは、ASP.NET MVC ミュージックストアサンプルアプリケーションをビルドするために実行するすべての手順について詳しく説明します。 パート6では、モデル V のデータ注釈の使用について説明します。
ms.author: riande
ms.date: 04/21/2011
ms.assetid: b3193d33-2d0b-4d98-9712-58bd897c62ec
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-6
msc.type: authoredcontent
ms.openlocfilehash: bc031dd5be61cc6707c522f85f6af77a420c8b31
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78433534"
---
# <a name="part-6-using-data-annotations-for-model-validation"></a><span data-ttu-id="c5ce1-104">パート 6: モデルの検証にデータ注釈を使用する</span><span class="sxs-lookup"><span data-stu-id="c5ce1-104">Part 6: Using Data Annotations for Model Validation</span></span>

<span data-ttu-id="c5ce1-105">( [Jon Galloway](https://github.com/jongalloway) )</span><span class="sxs-lookup"><span data-stu-id="c5ce1-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="c5ce1-106">MVC Music Store は、ASP.NET MVC と Visual Studio を使用して web 開発を行う方法を紹介したチュートリアルアプリケーションです。</span><span class="sxs-lookup"><span data-stu-id="c5ce1-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="c5ce1-107">MVC ミュージックストアは、音楽アルバムをオンラインで販売し、基本的なサイト管理、ユーザーサインイン、およびショッピングカート機能を実装する軽量のサンプルストア実装です。</span><span class="sxs-lookup"><span data-stu-id="c5ce1-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="c5ce1-108">このチュートリアルシリーズでは、ASP.NET MVC ミュージックストアサンプルアプリケーションをビルドするために実行するすべての手順について詳しく説明します。</span><span class="sxs-lookup"><span data-stu-id="c5ce1-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="c5ce1-109">パート6では、モデルの検証にデータ注釈を使用する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="c5ce1-109">Part 6 covers Using Data Annotations for Model Validation.</span></span>

<span data-ttu-id="c5ce1-110">作成フォームと編集フォームには重大な問題があります。検証は行われません。</span><span class="sxs-lookup"><span data-stu-id="c5ce1-110">We have a major issue with our Create and Edit forms: they're not doing any validation.</span></span> <span data-ttu-id="c5ce1-111">必須フィールドを空白のままにする、または価格フィールドに文字を入力するなどの操作を実行できます。最初に表示されるエラーは、データベースからのものです。</span><span class="sxs-lookup"><span data-stu-id="c5ce1-111">We can do things like leave required fields blank or type letters in the Price field, and the first error we'll see is from the database.</span></span>

<span data-ttu-id="c5ce1-112">モデルクラスにデータ注釈を追加することで、アプリケーションに検証を簡単に追加できます。</span><span class="sxs-lookup"><span data-stu-id="c5ce1-112">We can easily add validation to our application by adding Data Annotations to our model classes.</span></span> <span data-ttu-id="c5ce1-113">データ注釈を使用すると、モデルのプロパティに適用するルールを記述することができます。また、ASP.NET MVC では、ユーザーへの適切なメッセージの表示と表示が自動的に行われます。</span><span class="sxs-lookup"><span data-stu-id="c5ce1-113">Data Annotations allow us to describe the rules we want applied to our model properties, and ASP.NET MVC will take care of enforcing them and displaying appropriate messages to our users.</span></span>

## <a name="adding-validation-to-our-album-forms"></a><span data-ttu-id="c5ce1-114">アルバムフォームへの検証の追加</span><span class="sxs-lookup"><span data-stu-id="c5ce1-114">Adding Validation to our Album Forms</span></span>

<span data-ttu-id="c5ce1-115">次のデータ注釈属性を使用します。</span><span class="sxs-lookup"><span data-stu-id="c5ce1-115">We'll use the following Data Annotation attributes:</span></span>

- <span data-ttu-id="c5ce1-116">**必須**–プロパティが必須フィールドであることを示します。</span><span class="sxs-lookup"><span data-stu-id="c5ce1-116">**Required** – Indicates that the property is a required field</span></span>
- <span data-ttu-id="c5ce1-117">**DisplayName** –フォームフィールドおよび検証メッセージで使用するテキストを定義します。</span><span class="sxs-lookup"><span data-stu-id="c5ce1-117">**DisplayName** – Defines the text we want used on form fields and validation messages</span></span>
- <span data-ttu-id="c5ce1-118">**Stringlength** –文字列フィールドの最大長を定義します。</span><span class="sxs-lookup"><span data-stu-id="c5ce1-118">**StringLength** – Defines a maximum length for a string field</span></span>
- <span data-ttu-id="c5ce1-119">**Range** –数値フィールドの最大値と最小値を指定します。</span><span class="sxs-lookup"><span data-stu-id="c5ce1-119">**Range** – Gives a maximum and minimum value for a numeric field</span></span>
- <span data-ttu-id="c5ce1-120">**Bind** –パラメーターまたはフォーム値をモデルプロパティにバインドするときに、除外または含めるフィールドを一覧表示します</span><span class="sxs-lookup"><span data-stu-id="c5ce1-120">**Bind** – Lists fields to exclude or include when binding parameter or form values to model properties</span></span>
- <span data-ttu-id="c5ce1-121">**ScaffoldColumn** –エディターフォームのフィールドを非表示にすることができます</span><span class="sxs-lookup"><span data-stu-id="c5ce1-121">**ScaffoldColumn** – Allows hiding fields from editor forms</span></span>

<span data-ttu-id="c5ce1-122">*注: データ注釈属性を使用したモデル検証の詳細については、MSDN のドキュメントを参照してください*[`https://go.microsoft.com/fwlink/?LinkId=159063`](https://go.microsoft.com/fwlink/?LinkId=159063)</span><span class="sxs-lookup"><span data-stu-id="c5ce1-122">*Note: For more information on Model Validation using Data Annotation attributes, see the MSDN documentation at*[`https://go.microsoft.com/fwlink/?LinkId=159063`](https://go.microsoft.com/fwlink/?LinkId=159063)</span></span>

<span data-ttu-id="c5ce1-123">アルバムクラスを開き、次の*using*ステートメントを先頭に追加します。</span><span class="sxs-lookup"><span data-stu-id="c5ce1-123">Open the Album class and add the following *using* statements to the top.</span></span>

[!code-csharp[Main](mvc-music-store-part-6/samples/sample1.cs)]

<span data-ttu-id="c5ce1-124">次に、次に示すように、プロパティを更新して表示属性と検証属性を追加します。</span><span class="sxs-lookup"><span data-stu-id="c5ce1-124">Next, update the properties to add display and validation attributes as shown below.</span></span>

[!code-csharp[Main](mvc-music-store-part-6/samples/sample2.cs)]

<span data-ttu-id="c5ce1-125">ここでは、ジャンルとアーティストも仮想プロパティに変更しました。</span><span class="sxs-lookup"><span data-stu-id="c5ce1-125">While we're there, we've also changed the Genre and Artist to virtual properties.</span></span> <span data-ttu-id="c5ce1-126">これにより、必要に応じて Entity Framework が遅延読み込みされます。</span><span class="sxs-lookup"><span data-stu-id="c5ce1-126">This allows Entity Framework to lazy-load them as necessary.</span></span>

[!code-csharp[Main](mvc-music-store-part-6/samples/sample3.cs)]

<span data-ttu-id="c5ce1-127">これらの属性をアルバムモデルに追加した後、[作成] 画面と [編集] 画面では、すぐにフィールドの検証が開始され、選択した表示名 (AlbumArtUrl の代わりにアルバムアートの Url など) が使用されます。</span><span class="sxs-lookup"><span data-stu-id="c5ce1-127">After having added these attributes to our Album model, our Create and Edit screen immediately begin validating fields and using the Display Names we've chosen (e.g. Album Art Url instead of AlbumArtUrl).</span></span> <span data-ttu-id="c5ce1-128">アプリケーションを実行し、/StoreManager/Create. に移動します。</span><span class="sxs-lookup"><span data-stu-id="c5ce1-128">Run the application and browse to /StoreManager/Create.</span></span>

![](mvc-music-store-part-6/_static/image1.png)

<span data-ttu-id="c5ce1-129">次に、いくつかの検証規則を解除します。</span><span class="sxs-lookup"><span data-stu-id="c5ce1-129">Next, we'll break some validation rules.</span></span> <span data-ttu-id="c5ce1-130">価格に0を入力し、タイトルを空白のままにします。</span><span class="sxs-lookup"><span data-stu-id="c5ce1-130">Enter a price of 0 and leave the Title blank.</span></span> <span data-ttu-id="c5ce1-131">[作成] ボタンをクリックすると、検証エラーメッセージが表示され、定義した検証ルールを満たしていないフィールドが表示されます。</span><span class="sxs-lookup"><span data-stu-id="c5ce1-131">When we click on the Create button, we will see the form displayed with validation error messages showing which fields did not meet the validation rules we have defined.</span></span>

![](mvc-music-store-part-6/_static/image2.png)

## <a name="testing-the-client-side-validation"></a><span data-ttu-id="c5ce1-132">クライアント側の検証のテスト</span><span class="sxs-lookup"><span data-stu-id="c5ce1-132">Testing the Client-Side Validation</span></span>

<span data-ttu-id="c5ce1-133">サーバー側の検証は、ユーザーがクライアント側の検証を回避できるため、アプリケーションの観点から非常に重要です。</span><span class="sxs-lookup"><span data-stu-id="c5ce1-133">Server-side validation is very important from an application perspective, because users can circumvent client-side validation.</span></span> <span data-ttu-id="c5ce1-134">ただし、サーバー側の検証のみを実装する web ページフォームでは、3つの重要な問題が発生しています。</span><span class="sxs-lookup"><span data-stu-id="c5ce1-134">However, webpage forms which only implement server-side validation exhibit three significant problems.</span></span>

1. <span data-ttu-id="c5ce1-135">ユーザーは、フォームがポストされ、サーバーで検証され、応答がブラウザーに送信されるまで待機する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c5ce1-135">The user has to wait for the form to be posted, validated on the server, and for the response to be sent to their browser.</span></span>
2. <span data-ttu-id="c5ce1-136">ユーザーは、フィールドを修正するとすぐにフィードバックを得られず、検証ルールが渡されるようになります。</span><span class="sxs-lookup"><span data-stu-id="c5ce1-136">The user doesn't get immediate feedback when they correct a field so that it now passes the validation rules.</span></span>
3. <span data-ttu-id="c5ce1-137">ユーザーのブラウザーを利用する代わりに、検証ロジックを実行するためにサーバーリソースを無駄にしています。</span><span class="sxs-lookup"><span data-stu-id="c5ce1-137">We are wasting server resources to perform validation logic instead of leveraging the user's browser.</span></span>

<span data-ttu-id="c5ce1-138">幸い、ASP.NET MVC 3 スキャフォールディングテンプレートでは、クライアント側の検証が組み込まれているので、追加の作業は必要ありません。</span><span class="sxs-lookup"><span data-stu-id="c5ce1-138">Fortunately, the ASP.NET MVC 3 scaffold templates have client-side validation built in, requiring no additional work whatsoever.</span></span>

<span data-ttu-id="c5ce1-139">[タイトル] フィールドに1文字を入力すると検証要件が満たされるため、検証メッセージはすぐに削除されます。</span><span class="sxs-lookup"><span data-stu-id="c5ce1-139">Typing a single letter in the Title field satisfies the validation requirements, so the validation message is immediately removed.</span></span>

![](mvc-music-store-part-6/_static/image3.png)

> [!div class="step-by-step"]
> <span data-ttu-id="c5ce1-140">[前へ](mvc-music-store-part-5.md)
> [次へ](mvc-music-store-part-7.md)</span><span class="sxs-lookup"><span data-stu-id="c5ce1-140">[Previous](mvc-music-store-part-5.md)
[Next](mvc-music-store-part-7.md)</span></span>
