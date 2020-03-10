---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-2
title: 'パート 2: データアクセス層 |Microsoft Docs'
author: JoeStagner
description: このチュートリアルシリーズでは、Tailspin Spyworks サンプルアプリケーションを構築するために実行するすべての手順について詳しく説明します。 パート2では、データアクセス層の追加について説明します。
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 5a9d5429-d70b-411c-8474-f42cf7ef8a2b
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-2
msc.type: authoredcontent
ms.openlocfilehash: 342d2c54dfba5d052570e890f85dcf9739f9884f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78462652"
---
# <a name="part-2-data-access-layer"></a><span data-ttu-id="1a9d7-104">パート 2: データアクセス層</span><span class="sxs-lookup"><span data-stu-id="1a9d7-104">Part 2: Data Access Layer</span></span>

<span data-ttu-id="1a9d7-105">[Joe Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="1a9d7-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="1a9d7-106">Tailspin Spyworks は、.NET プラットフォーム用の強力でスケーラブルなアプリケーションを簡単に作成する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="1a9d7-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="1a9d7-107">ASP.NET 4 の優れた新機能を使用して、ショッピング、チェックアウト、管理などのオンラインストアを構築する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="1a9d7-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="1a9d7-108">このチュートリアルシリーズでは、Tailspin Spyworks サンプルアプリケーションを構築するために実行するすべての手順について詳しく説明します。</span><span class="sxs-lookup"><span data-stu-id="1a9d7-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="1a9d7-109">パート2では、データアクセス層の追加について説明します。</span><span class="sxs-lookup"><span data-stu-id="1a9d7-109">Part 2 covers adding the data access layer.</span></span>

## <a id="_Toc260221668"></a><span data-ttu-id="1a9d7-110">データアクセス層の追加</span><span class="sxs-lookup"><span data-stu-id="1a9d7-110">Adding the Data Access Layer</span></span>

<span data-ttu-id="1a9d7-111">E コマースアプリケーションは、2つのデータベースに依存しています。</span><span class="sxs-lookup"><span data-stu-id="1a9d7-111">Our ecommerce application will depend on two databases.</span></span>

<span data-ttu-id="1a9d7-112">顧客情報については、標準の ASP.NET メンバーシップデータベースを使用します。</span><span class="sxs-lookup"><span data-stu-id="1a9d7-112">For customer information we'll use the standard ASP.NET Membership database.</span></span> <span data-ttu-id="1a9d7-113">ショッピングカートと製品カタログについては、次のように SQL Express データベースを実装します。</span><span class="sxs-lookup"><span data-stu-id="1a9d7-113">For our shopping cart and product catalog we'll implement a SQL Express database as follows.</span></span>

![](tailspin-spyworks-part-2/_static/image1.jpg)

<span data-ttu-id="1a9d7-114">アプリケーションの App\_Data フォルダーにデータベース (コマース) を作成した後は、.NET Entity Framework を使用したデータアクセス層の作成に進むことができます。</span><span class="sxs-lookup"><span data-stu-id="1a9d7-114">Having created the database (Commerce.mdf) in the application's App\_Data folder we can proceed to create our Data Access Layer using the .NET Entity Framework.</span></span>

<span data-ttu-id="1a9d7-115">"Data\_Access" という名前のフォルダーを作成し、そのフォルダーを右クリックして、[新しい項目の追加] を選択します。</span><span class="sxs-lookup"><span data-stu-id="1a9d7-115">We'll create a folder named "Data\_Access" and them right click on that folder and select "Add New Item".</span></span>

<span data-ttu-id="1a9d7-116">[インストールされたテンプレート] 項目で、[ADO.NET Entity Data Model] を選択し、名前として「EDM\_」と入力して、[追加] ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="1a9d7-116">In the "Installed Templates" item and then select "ADO.NET Entity Data Model" enter EDM\_Commerce.edmx as the name and click the "Add" button.</span></span>

![](tailspin-spyworks-part-2/_static/image2.jpg)

<span data-ttu-id="1a9d7-117">[データベースから生成] を選択します。</span><span class="sxs-lookup"><span data-stu-id="1a9d7-117">Choose "Generate from Database".</span></span>

![](tailspin-spyworks-part-2/_static/image1.png)

![](tailspin-spyworks-part-2/_static/image2.png)

![](tailspin-spyworks-part-2/_static/image3.png)

![](tailspin-spyworks-part-2/_static/image3.jpg)

<span data-ttu-id="1a9d7-118">保存してビルドします。</span><span class="sxs-lookup"><span data-stu-id="1a9d7-118">Save and build.</span></span>

<span data-ttu-id="1a9d7-119">これで、最初の機能 (製品カテゴリメニュー) を追加する準備ができました。</span><span class="sxs-lookup"><span data-stu-id="1a9d7-119">Now we are ready to add our first feature – a product category menu.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="1a9d7-120">[前へ](tailspin-spyworks-part-1.md)
> [次へ](tailspin-spyworks-part-3.md)</span><span class="sxs-lookup"><span data-stu-id="1a9d7-120">[Previous](tailspin-spyworks-part-1.md)
[Next](tailspin-spyworks-part-3.md)</span></span>
