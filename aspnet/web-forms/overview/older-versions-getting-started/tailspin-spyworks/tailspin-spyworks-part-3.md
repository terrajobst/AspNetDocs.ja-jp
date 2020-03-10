---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-3
title: 'パート 3: レイアウトとカテゴリのメニュー |Microsoft Docs'
author: JoeStagner
description: このチュートリアルシリーズでは、Tailspin Spyworks サンプルアプリケーションを構築するために実行するすべての手順について詳しく説明します。 パート3では、レイアウトとカテゴリメニューの追加について説明します。
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 94ea1a70-a9bc-4241-8f36-08366d64bab9
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-3
msc.type: authoredcontent
ms.openlocfilehash: a223b97fd362ecf73ecde431e141021c1dcc6a6d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78519100"
---
# <a name="part-3-layout-and-category-menu"></a><span data-ttu-id="64a64-104">パート 3: レイアウトとカテゴリメニュー</span><span class="sxs-lookup"><span data-stu-id="64a64-104">Part 3: Layout and Category Menu</span></span>

<span data-ttu-id="64a64-105">[Joe Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="64a64-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="64a64-106">Tailspin Spyworks は、.NET プラットフォーム用の強力でスケーラブルなアプリケーションを簡単に作成する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="64a64-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="64a64-107">ASP.NET 4 の優れた新機能を使用して、ショッピング、チェックアウト、管理などのオンラインストアを構築する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="64a64-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="64a64-108">このチュートリアルシリーズでは、Tailspin Spyworks サンプルアプリケーションを構築するために実行するすべての手順について詳しく説明します。</span><span class="sxs-lookup"><span data-stu-id="64a64-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="64a64-109">パート3では、レイアウトとカテゴリメニューの追加について説明します。</span><span class="sxs-lookup"><span data-stu-id="64a64-109">Part 3 covers adding layout and a category menu.</span></span>

## <a id="_Toc260221669"></a><span data-ttu-id="64a64-110">レイアウトとカテゴリメニューを追加する</span><span class="sxs-lookup"><span data-stu-id="64a64-110">Adding Some Layout and a Category Menu</span></span>

<span data-ttu-id="64a64-111">サイトマスターページで、左側の列に、製品カテゴリメニューを含む div を追加します。</span><span class="sxs-lookup"><span data-stu-id="64a64-111">In our site master page we'll add a div for the left side column that will contain our product category menu.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-3/samples/sample1.aspx)]

<span data-ttu-id="64a64-112">必要な配置とその他の書式設定は、スタイルの .css ファイルに追加した CSS クラスによって提供されることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="64a64-112">Note that the desired aligning and other formatting will be provided by the CSS class that we added to our Style.css file.</span></span>

[!code-css[Main](tailspin-spyworks-part-3/samples/sample2.css)]

<span data-ttu-id="64a64-113">製品カテゴリのメニューは実行時に動的に作成されます。そのためには、既存の製品カテゴリを Commerce データベースに照会し、メニュー項目と対応するリンクを作成します。</span><span class="sxs-lookup"><span data-stu-id="64a64-113">The product category menu will be dynamically created at runtime by querying the Commerce database for existing product categories and creating the menu items and corresponding links.</span></span>

<span data-ttu-id="64a64-114">これを実現するには、2つの ASP を使用します。NET の強力なデータコントロール。</span><span class="sxs-lookup"><span data-stu-id="64a64-114">To accomplish this we will use two of ASP.NET's powerful data controls.</span></span> <span data-ttu-id="64a64-115">"Entity Data Source" コントロールと "ListView" コントロール。</span><span class="sxs-lookup"><span data-stu-id="64a64-115">The "Entity Data Source" control and the "ListView" control.</span></span>

![](tailspin-spyworks-part-3/_static/image1.jpg)

<span data-ttu-id="64a64-116">[デザインビュー] に切り替えて、ヘルパーを使用してコントロールを構成します。</span><span class="sxs-lookup"><span data-stu-id="64a64-116">Let's switch to "Design View" and use the helpers to configure our controls.</span></span>

![](tailspin-spyworks-part-3/_static/image2.jpg)

<span data-ttu-id="64a64-117">EntityDataSource ID プロパティを EDS\_Category\_ に設定し、データソースの構成 をクリックしてみましょう。</span><span class="sxs-lookup"><span data-stu-id="64a64-117">Let's set the EntityDataSource ID property to EDS\_Category\_Menu and click on "Configure Data Source".</span></span>

![](tailspin-spyworks-part-3/_static/image3.jpg)

<span data-ttu-id="64a64-118">コマースデータベースのエンティティデータソースモデルを作成したときに作成された CommerceEntities 接続を選択し、[次へ] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="64a64-118">Select the CommerceEntities Connection that was created for us when we created the Entity Data Source Model for our Commerce Database and click "Next".</span></span>

![](tailspin-spyworks-part-3/_static/image4.jpg)

<span data-ttu-id="64a64-119">[カテゴリ] エンティティセット名を選択し、残りのオプションは既定値のままにします。</span><span class="sxs-lookup"><span data-stu-id="64a64-119">Select the "Categories" Entity set name and leave the rest of the options as default.</span></span> <span data-ttu-id="64a64-120">[完了] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="64a64-120">Click "Finish".</span></span>

<span data-ttu-id="64a64-121">次に、ページに配置した ListView コントロールインスタンスの ID プロパティを ListView\_[製品] メニューに設定し、ヘルパーをアクティブ化します。</span><span class="sxs-lookup"><span data-stu-id="64a64-121">Now let's set the ID property of the ListView control instance that we placed on our page to ListView\_ProductsMenu and activate its helper.</span></span>

![](tailspin-spyworks-part-3/_static/image5.jpg)

<span data-ttu-id="64a64-122">コントロールオプションを使用してデータ項目の表示と書式設定を書式設定することもできますが、メニューの作成では、ソースビューにコードを入力するだけで、単純なマークアップが必要になります。</span><span class="sxs-lookup"><span data-stu-id="64a64-122">Though we could use control options to format the data item display and formatting, our menu creation will only require simple markup so we will enter the code in the source view.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-3/samples/sample3.aspx)]

<span data-ttu-id="64a64-123">"Eval" ステートメントに注意してください: &lt;% # Eval ("区分番号")%&gt;</span><span class="sxs-lookup"><span data-stu-id="64a64-123">Please note the "Eval" statement : &lt;%# Eval("CategoryName") %&gt;</span></span>

<span data-ttu-id="64a64-124">ASP.NET 構文 &lt;% #%&gt; は、その中に含まれるものを実行するようにランタイムに指示し、結果を "行" で出力するための短縮規約です。</span><span class="sxs-lookup"><span data-stu-id="64a64-124">The ASP.NET syntax &lt;%# %&gt; is a shorthand convention that instructs the runtime to execute whatever is contained within and output the results "in Line".</span></span>

<span data-ttu-id="64a64-125">ステートメント Eval ("区分名") は、バインドされたデータ項目のコレクション内の現在のエントリについて、エンティティモデル項目名 "の値" "区分名" の値をフェッチするように指示します。</span><span class="sxs-lookup"><span data-stu-id="64a64-125">The statement Eval("CategoryName") instructs that, for the current entry in the bound collection of data items, fetch the value of the Entity Model item names "CategoryName".</span></span> <span data-ttu-id="64a64-126">これは、非常に強力な機能を使用するための簡潔な構文です。</span><span class="sxs-lookup"><span data-stu-id="64a64-126">This is concise syntax for a very powerful feature.</span></span>

<span data-ttu-id="64a64-127">アプリケーションをすぐに実行できるようにします。</span><span class="sxs-lookup"><span data-stu-id="64a64-127">Lets run the application now.</span></span>

![](tailspin-spyworks-part-3/_static/image6.jpg)

<span data-ttu-id="64a64-128">[Product category] メニューが表示されるようになり、カテゴリメニュー項目のいずれかにマウスポインターを合わせると、ページへのメニュー項目のリンクポイントが表示されます。ここでは、名前付きの製品リストを実装し、動的なクエリ文字列引数を カテゴリ id。</span><span class="sxs-lookup"><span data-stu-id="64a64-128">Note that our product category menu is now displayed and when we hover over one of the category menu items we can see the menu item link points to a page we have yet to implement named ProductsList.aspx and that we have built a dynamic query string argument that contains the category id.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="64a64-129">[前へ](tailspin-spyworks-part-2.md)
> [次へ](tailspin-spyworks-part-4.md)</span><span class="sxs-lookup"><span data-stu-id="64a64-129">[Previous](tailspin-spyworks-part-2.md)
[Next](tailspin-spyworks-part-4.md)</span></span>
