---
uid: web-pages/overview/ui-layouts-and-themes/installing-helpers
title: ASP.NET Web ページ (Razor) サイトでのヘルパーのインストール |Microsoft Docs
author: Rick-Anderson
description: この記事では、ASP.NET Web ページ (Razor) web サイトにヘルパーをインストールする方法について説明します。 ヘルパーは、コードとマークアップを含む再利用可能なコンポーネントです...
ms.author: riande
ms.date: 02/18/2014
ms.assetid: 5e968ead-906a-45ea-ac2a-c70e57e1a9b1
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/installing-helpers
msc.type: authoredcontent
ms.openlocfilehash: 41e33c04a53a6ad257c3937cdadcec767e9217c8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78518644"
---
# <a name="installing-a-helper-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="a47a3-104">ASP.NET Web ページ (Razor) サイトへのヘルパーのインストール</span><span class="sxs-lookup"><span data-stu-id="a47a3-104">Installing a Helper in an ASP.NET Web Pages (Razor) Site</span></span>

<span data-ttu-id="a47a3-105">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="a47a3-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="a47a3-106">この記事では、ASP.NET Web ページ (Razor) web サイトにヘルパーをインストールする方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="a47a3-106">This article describes how to install a helper in an ASP.NET Web Pages (Razor) website.</span></span> <span data-ttu-id="a47a3-107">*ヘルパー*は、煩雑または複雑なタスクを実行するためのコードとマークアップを含む再利用可能なコンポーネントです。</span><span class="sxs-lookup"><span data-stu-id="a47a3-107">A *helper* is a reusable component that includes code and markup to perform a task that might be tedious or complex.</span></span>
> 
> <span data-ttu-id="a47a3-108">ここでは、次の内容について学習します。</span><span class="sxs-lookup"><span data-stu-id="a47a3-108">What you'll learn:</span></span>
> 
> - <span data-ttu-id="a47a3-109">WebMatrix 3 を使用して作成された web サイトにヘルパーをインストールする方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="a47a3-109">How to install a helper in a website created using WebMatrix 3.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="a47a3-110">このチュートリアルで使用されているソフトウェアのバージョン</span><span class="sxs-lookup"><span data-stu-id="a47a3-110">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="a47a3-111">WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="a47a3-111">WebMatrix 3</span></span>

## <a name="overview-of-helpers"></a><span data-ttu-id="a47a3-112">ヘルパーの概要</span><span class="sxs-lookup"><span data-stu-id="a47a3-112">Overview of Helpers</span></span>

<span data-ttu-id="a47a3-113">Web ページで頻繁に実行するタスクには、多くのコードが必要になる場合や、追加の知識が必要な場合があります。</span><span class="sxs-lookup"><span data-stu-id="a47a3-113">Some tasks that people often want to do on web pages require a lot of code or require extra knowledge.</span></span> <span data-ttu-id="a47a3-114">たとえば、データのグラフを表示します。ページに Twitter の "フォロー" ボタンを配置するweb サイトから電子メールを送信しています。イメージのトリミングまたはサイズ変更サイトで PayPal を使用します。</span><span class="sxs-lookup"><span data-stu-id="a47a3-114">Examples include displaying a chart for data; putting a Twitter "Follow" button on a page; sending email from your website; cropping or resizing images; using PayPal for your site.</span></span> <span data-ttu-id="a47a3-115">このような作業を簡単に行うために、ASP.NET Web ページで*ヘルパー*を使用できます。</span><span class="sxs-lookup"><span data-stu-id="a47a3-115">To make it easy to do these kinds of things, ASP.NET Web Pages lets you use *helpers*.</span></span> <span data-ttu-id="a47a3-116">ヘルパーは、サイト用にインストールするコンポーネントであり、1行または2行の Razor コードだけを使用して一般的なタスクを実行できます。</span><span class="sxs-lookup"><span data-stu-id="a47a3-116">Helpers are components that you install for a site and that let you perform typical tasks by using just a line or two of Razor code.</span></span>

<span data-ttu-id="a47a3-117">ASP.NET Web ページには、いくつかのヘルパーが組み込まれています。</span><span class="sxs-lookup"><span data-stu-id="a47a3-117">ASP.NET Web Pages has a few helpers built in.</span></span> <span data-ttu-id="a47a3-118">ただし、NuGet パッケージマネージャーを使用して提供されているパッケージ (アドイン) では、多くのヘルパーを利用できます。</span><span class="sxs-lookup"><span data-stu-id="a47a3-118">However, many helpers are available in packages (add-ins) that are provided using the NuGet package manager.</span></span> <span data-ttu-id="a47a3-119">NuGet を使用すると、インストールするパッケージを選択して、インストールのすべての詳細を処理できます。</span><span class="sxs-lookup"><span data-stu-id="a47a3-119">NuGet lets you select a package to install and then it takes care of all the details of the installation.</span></span>

## <a name="installing-a-helper-in-webmatrix-3"></a><span data-ttu-id="a47a3-120">WebMatrix でのヘルパーのインストール3</span><span class="sxs-lookup"><span data-stu-id="a47a3-120">Installing a Helper in WebMatrix 3</span></span>

1. <span data-ttu-id="a47a3-121">WebMatrix 3 では、 **[NuGet]** ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="a47a3-121">In WebMatrix 3, click the **NuGet** button.</span></span>

    ![WebMatrix の [NuGet ギャラリー] ダイアログボックス](installing-helpers/_static/image1.png)
2. <span data-ttu-id="a47a3-123">NuGet パッケージマネージャーが起動し、使用可能なパッケージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="a47a3-123">This launches the NuGet package manager and displays available packages.</span></span> <span data-ttu-id="a47a3-124">検索ボックスに、インストールするヘルパーのキーワードを入力します。</span><span class="sxs-lookup"><span data-stu-id="a47a3-124">In the search box, enter a keyword for the helper you want to install.</span></span>

    ![WebMatrix の [NuGet ギャラリー] ダイアログボックス](installing-helpers/_static/image2.png)
3. <span data-ttu-id="a47a3-126">パッケージを選択し、 **[インストール]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="a47a3-126">Select the package and then click **Install**.</span></span> <span data-ttu-id="a47a3-127">パッケージをインストールするかどうかを確認するメッセージが表示されたら [**はい]** をクリックし、条項に同意することを示します。</span><span class="sxs-lookup"><span data-stu-id="a47a3-127">Click **Yes** when asked if you want to install the package and indicate that you accept the terms.</span></span>

     <span data-ttu-id="a47a3-128">初めてヘルパーをインストールした場合は、NuGet によって、ヘルパーを構成するコード用のフォルダーが web サイトに作成されます。</span><span class="sxs-lookup"><span data-stu-id="a47a3-128">If this is the first time you've installed a helper, NuGet creates folders in your website for the code that makes up the helper.</span></span>
4. <span data-ttu-id="a47a3-129">ヘルパーをアンインストールするには、 **[ギャラリー]** ボタンをクリックし、 **[インストール済み]** タブをクリックして、アンインストールするパッケージを選択します。</span><span class="sxs-lookup"><span data-stu-id="a47a3-129">To uninstall a helper, click the **Gallery** button, click the **Installed** tab, and pick the package you want to uninstall.</span></span>

## <a name="installing-the-twitter-helper"></a><span data-ttu-id="a47a3-130">Twitter ヘルパーのインストール</span><span class="sxs-lookup"><span data-stu-id="a47a3-130">Installing the Twitter helper</span></span>

<span data-ttu-id="a47a3-131">最新バージョンの Twitter API は、NuGet を使用してインストールする Twitter ヘルパーと互換性がありません。</span><span class="sxs-lookup"><span data-stu-id="a47a3-131">The latest version of the Twitter API is not compatible with the Twitter helper you install through NuGet.</span></span> <span data-ttu-id="a47a3-132">プロジェクトに Twitter ヘルパーを設定する方法については、「WebMatrix を使用した[Twitter ヘルパー](twitter-helper.md) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a47a3-132">Instead, see the [Twitter Helper with WebMatrix](twitter-helper.md) topic for information about how to set up the Twitter helper in your project.</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="a47a3-133">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="a47a3-133">Additional Resources</span></span>

[<span data-ttu-id="a47a3-134">ASP.NET Web ページ2の概要-プログラミングの基礎</span><span class="sxs-lookup"><span data-stu-id="a47a3-134">Introducing ASP.NET Web Pages 2 - Programming Basics</span></span>](../getting-started/introducing-razor-syntax-c.md)

[<span data-ttu-id="a47a3-135">WebMatrix を使用した Twitter ヘルパー</span><span class="sxs-lookup"><span data-stu-id="a47a3-135">Twitter Helper with WebMatrix</span></span>](twitter-helper.md)
