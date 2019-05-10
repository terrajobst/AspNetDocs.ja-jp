---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-8
title: 第 8 部:最終的なページ、例外処理、およびまとめ |Microsoft Docs
author: JoeStagner
description: このチュートリアル シリーズでは、すべての Tailspin Spyworks サンプル アプリケーションをビルドする手順について説明します。 パート 8 では、ページ、および例外に関する、連絡先ページを追加します.
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 5aeadf8f-39f3-4f07-a78f-1c310c64fb23
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-8
msc.type: authoredcontent
ms.openlocfilehash: 707dc9d87ae324a7897c971a451e40bc54c96cb3
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2019
ms.locfileid: "65130603"
---
# <a name="part-8-final-pages-exception-handling-and-conclusion"></a><span data-ttu-id="c5a08-104">第 8 部:最終ページ、例外処理、まとめ</span><span class="sxs-lookup"><span data-stu-id="c5a08-104">Part 8: Final Pages, Exception Handling, and Conclusion</span></span>

<span data-ttu-id="c5a08-105">によって[Joe Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="c5a08-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="c5a08-106">Tailspin Spyworks では、.NET プラットフォーム用の強力でスケーラブルなアプリケーションを作成するはどの非常に単純なを示します。</span><span class="sxs-lookup"><span data-stu-id="c5a08-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="c5a08-107">ASP.NET 4 の優れた新機能を使用して、ショッピング、チェック アウト、および管理を含む、オンライン ストアを構築する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="c5a08-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="c5a08-108">このチュートリアル シリーズでは、すべての Tailspin Spyworks サンプル アプリケーションをビルドする手順について説明します。</span><span class="sxs-lookup"><span data-stu-id="c5a08-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="c5a08-109">パート 8 では、ページ、および例外処理についての連絡のページを追加します。</span><span class="sxs-lookup"><span data-stu-id="c5a08-109">Part 8 adds a contact page, about page, and exception handling.</span></span> <span data-ttu-id="c5a08-110">これは、シリーズのまとめです。</span><span class="sxs-lookup"><span data-stu-id="c5a08-110">This is the conclusion of the series.</span></span>

## <a id="_Toc260221680"></a>  <span data-ttu-id="c5a08-111">ページ (ASP.NET から電子メールを送信する) にお問い合わせください。</span><span class="sxs-lookup"><span data-stu-id="c5a08-111">Contact Page (Sending email from ASP.NET)</span></span>

<span data-ttu-id="c5a08-112">ContactUs.aspx をという名前の新しいページを作成します。</span><span class="sxs-lookup"><span data-stu-id="c5a08-112">Create a new page named ContactUs.aspx</span></span>

<span data-ttu-id="c5a08-113">デザイナーを使用して、ToolkitScriptManager、AjaxControlToolkit からエディター コントロールなど、特別な注意事項は次の形式を作成します。</span><span class="sxs-lookup"><span data-stu-id="c5a08-113">Using the designer, create the following form taking special note to include the ToolkitScriptManager and the Editor control from the AjaxControlToolkit.</span></span> <span data-ttu-id="c5a08-114">.</span><span class="sxs-lookup"><span data-stu-id="c5a08-114">.</span></span>

![](tailspin-spyworks-part-8/_static/image1.jpg)

<span data-ttu-id="c5a08-115">分離コード ファイルで、クリック イベント ハンドラーを生成し、連絡先情報を電子メールとして送信するメソッドを実装する [送信] ボタンをダブルクリックします。</span><span class="sxs-lookup"><span data-stu-id="c5a08-115">Double click on the "Submit" button to generate a click event handler in the code behind file and implement a method to send the contact information as an email.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample1.cs)]

<span data-ttu-id="c5a08-116">このコードでは、web.config ファイルにメールを送信するのに使用する SMTP サーバーを指定する構成セクションのエントリが含まれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="c5a08-116">This code requires that your web.config file contain an entry in the configuration section that specifies the SMTP server to use for sending mail.</span></span>

[!code-xml[Main](tailspin-spyworks-part-8/samples/sample2.xml)]

## <a id="_Toc260221681"></a>  <span data-ttu-id="c5a08-117">ページについて</span><span class="sxs-lookup"><span data-stu-id="c5a08-117">About Page</span></span>

<span data-ttu-id="c5a08-118">AboutUs.aspx という名前のページを作成し、任意のコンテンツを追加します。</span><span class="sxs-lookup"><span data-stu-id="c5a08-118">Create a page named AboutUs.aspx and add whatever content you like.</span></span>

## <a id="_Toc260221682"></a>  <span data-ttu-id="c5a08-119">グローバル例外ハンドラー</span><span class="sxs-lookup"><span data-stu-id="c5a08-119">Global Exception Handler</span></span>

<span data-ttu-id="c5a08-120">最後に、アプリケーション全体では、例外をスローしましたが、不測の事態をコールドも web アプリケーションでは原因が未処理の例外。</span><span class="sxs-lookup"><span data-stu-id="c5a08-120">Lastly, throughout the application we have thrown exceptions and there are unforeseen circumstances that cold also cause unhandled exceptions in our web application.</span></span>

<span data-ttu-id="c5a08-121">未処理の例外の web サイトの訪問者に表示されることはありません必要があります。</span><span class="sxs-lookup"><span data-stu-id="c5a08-121">We never want an unhandled exception to be displayed to a web site visitor.</span></span>

![](tailspin-spyworks-part-8/_static/image2.jpg)

<span data-ttu-id="c5a08-122">悲惨なユーザー エクスペリエンスとは別のハンドルされない例外は、セキュリティ上の問題をこともできます。</span><span class="sxs-lookup"><span data-stu-id="c5a08-122">Apart from being a terrible user experience unhandled exceptions can also be a security problem.</span></span>

<span data-ttu-id="c5a08-123">この問題を解決するためには、グローバル例外ハンドラーを実装します。</span><span class="sxs-lookup"><span data-stu-id="c5a08-123">To solve this problem we will implement a global exception handler.</span></span>

<span data-ttu-id="c5a08-124">これを行うには、Global.asax ファイルを開き、次の事前生成されたイベント ハンドラーに注意してください。</span><span class="sxs-lookup"><span data-stu-id="c5a08-124">To do this, open the Global.asax file and note the following pre-generated event handler.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample3.cs)]

<span data-ttu-id="c5a08-125">アプリケーションを実装するコードを追加\_エラー ハンドラーとして次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="c5a08-125">Add code to implement the Application\_Error handler as follows.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample4.cs)]

<span data-ttu-id="c5a08-126">ソリューションに Error.aspx をという名前のページを追加し、次のマークアップ スニペットを追加します。</span><span class="sxs-lookup"><span data-stu-id="c5a08-126">Then add a page named Error.aspx to the solution and add this markup snippet.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-8/samples/sample5.aspx)]

<span data-ttu-id="c5a08-127">ページで今すぐ\_要求オブジェクトからイベント ハンドラーの抽出、エラー メッセージを読み込みます。</span><span class="sxs-lookup"><span data-stu-id="c5a08-127">Now in the Page\_Load event handler extract the error messages from the Request Object.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample6.cs)]

## <a id="_Toc260221683"></a>  <span data-ttu-id="c5a08-128">まとめ</span><span class="sxs-lookup"><span data-stu-id="c5a08-128">Conclusion</span></span>

<span data-ttu-id="c5a08-129">ASP.NET WebForms 簡単見たなどのデータベース アクセス、メンバーシップ、AJAX、高度な web サイトを作成します。</span><span class="sxs-lookup"><span data-stu-id="c5a08-129">We've seen that ASP.NET WebForms makes it easy to create a sophisticated website with database access, membership, AJAX, etc.</span></span> <span data-ttu-id="c5a08-130">非常に短時間です。</span><span class="sxs-lookup"><span data-stu-id="c5a08-130">pretty quickly.</span></span>

<span data-ttu-id="c5a08-131">このチュートリアルが願って、独自の ASP.NET WebForms アプリケーションの構築を開始する必要があるツールです。</span><span class="sxs-lookup"><span data-stu-id="c5a08-131">Hopefully this tutorial has given you the tools you need to get started building your own ASP.NET WebForms applications!</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="c5a08-132">前へ</span><span class="sxs-lookup"><span data-stu-id="c5a08-132">Previous</span></span>](tailspin-spyworks-part-7.md)
