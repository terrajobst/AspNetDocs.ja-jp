---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-8
title: 'パート 8: 最終的なページ、例外処理、および結論 |Microsoft Docs'
author: JoeStagner
description: このチュートリアルシリーズでは、Tailspin Spyworks サンプルアプリケーションを構築するために実行するすべての手順について詳しく説明します。 パート8は、連絡先ページ、ページ、および例外を追加します。
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 5aeadf8f-39f3-4f07-a78f-1c310c64fb23
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-8
msc.type: authoredcontent
ms.openlocfilehash: 707dc9d87ae324a7897c971a451e40bc54c96cb3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78474340"
---
# <a name="part-8-final-pages-exception-handling-and-conclusion"></a><span data-ttu-id="d7623-104">パート 8: 最終的なページ、例外処理、および結論</span><span class="sxs-lookup"><span data-stu-id="d7623-104">Part 8: Final Pages, Exception Handling, and Conclusion</span></span>

<span data-ttu-id="d7623-105">[Joe Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="d7623-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="d7623-106">Tailspin Spyworks は、.NET プラットフォーム用の強力でスケーラブルなアプリケーションを簡単に作成する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="d7623-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="d7623-107">ASP.NET 4 の優れた新機能を使用して、ショッピング、チェックアウト、管理などのオンラインストアを構築する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="d7623-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="d7623-108">このチュートリアルシリーズでは、Tailspin Spyworks サンプルアプリケーションを構築するために実行するすべての手順について詳しく説明します。</span><span class="sxs-lookup"><span data-stu-id="d7623-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="d7623-109">パート8では、連絡先ページ、ページ、例外処理を追加します。</span><span class="sxs-lookup"><span data-stu-id="d7623-109">Part 8 adds a contact page, about page, and exception handling.</span></span> <span data-ttu-id="d7623-110">これがシリーズの結論です。</span><span class="sxs-lookup"><span data-stu-id="d7623-110">This is the conclusion of the series.</span></span>

## <a id="_Toc260221680"></a><span data-ttu-id="d7623-111">連絡先ページ (ASP.NET からの電子メールの送信)</span><span class="sxs-lookup"><span data-stu-id="d7623-111">Contact Page (Sending email from ASP.NET)</span></span>

<span data-ttu-id="d7623-112">ContactUs という名前の新しいページを作成します。</span><span class="sxs-lookup"><span data-stu-id="d7623-112">Create a new page named ContactUs.aspx</span></span>

<span data-ttu-id="d7623-113">デザイナーを使用して、次のフォームを作成します。これには、ToolkitScriptManager と AjaxControlToolkit のエディターコントロールを含めるための特別な注意事項があります。</span><span class="sxs-lookup"><span data-stu-id="d7623-113">Using the designer, create the following form taking special note to include the ToolkitScriptManager and the Editor control from the AjaxControlToolkit.</span></span> <span data-ttu-id="d7623-114">。</span><span class="sxs-lookup"><span data-stu-id="d7623-114">.</span></span>

![](tailspin-spyworks-part-8/_static/image1.jpg)

<span data-ttu-id="d7623-115">[送信] ボタンをダブルクリックして、分離コードファイルに click イベントハンドラーを生成し、電子メールとして連絡先情報を送信するメソッドを実装します。</span><span class="sxs-lookup"><span data-stu-id="d7623-115">Double click on the "Submit" button to generate a click event handler in the code behind file and implement a method to send the contact information as an email.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample1.cs)]

<span data-ttu-id="d7623-116">このコードでは、電子メールの送信に使用する SMTP サーバーを指定する構成セクションに、web.config ファイルにエントリが含まれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="d7623-116">This code requires that your web.config file contain an entry in the configuration section that specifies the SMTP server to use for sending mail.</span></span>

[!code-xml[Main](tailspin-spyworks-part-8/samples/sample2.xml)]

## <a id="_Toc260221681"></a><span data-ttu-id="d7623-117">[バージョン情報] ページ</span><span class="sxs-lookup"><span data-stu-id="d7623-117">About Page</span></span>

<span data-ttu-id="d7623-118">AboutUs という名前のページを作成し、任意の内容を追加します。</span><span class="sxs-lookup"><span data-stu-id="d7623-118">Create a page named AboutUs.aspx and add whatever content you like.</span></span>

## <a id="_Toc260221682"></a><span data-ttu-id="d7623-119">グローバル例外ハンドラー</span><span class="sxs-lookup"><span data-stu-id="d7623-119">Global Exception Handler</span></span>

<span data-ttu-id="d7623-120">最後に、アプリケーション全体で例外がスローされました。また、web アプリケーションでハンドルされない例外が発生する可能性がある予期しない状況もあります。</span><span class="sxs-lookup"><span data-stu-id="d7623-120">Lastly, throughout the application we have thrown exceptions and there are unforeseen circumstances that cold also cause unhandled exceptions in our web application.</span></span>

<span data-ttu-id="d7623-121">未処理の例外を web サイトの訪問者に表示させたくありません。</span><span class="sxs-lookup"><span data-stu-id="d7623-121">We never want an unhandled exception to be displayed to a web site visitor.</span></span>

![](tailspin-spyworks-part-8/_static/image2.jpg)

<span data-ttu-id="d7623-122">ユーザーエクスペリエンスの低下とは別に、ハンドルされない例外がセキュリティ上の問題になることもあります。</span><span class="sxs-lookup"><span data-stu-id="d7623-122">Apart from being a terrible user experience unhandled exceptions can also be a security problem.</span></span>

<span data-ttu-id="d7623-123">この問題を解決するには、グローバル例外ハンドラーを実装します。</span><span class="sxs-lookup"><span data-stu-id="d7623-123">To solve this problem we will implement a global exception handler.</span></span>

<span data-ttu-id="d7623-124">これを行うには、global.asax ファイルを開き、次の事前生成されたイベントハンドラーを確認します。</span><span class="sxs-lookup"><span data-stu-id="d7623-124">To do this, open the Global.asax file and note the following pre-generated event handler.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample3.cs)]

<span data-ttu-id="d7623-125">次のように、アプリケーション\_のエラーハンドラーを実装するコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="d7623-125">Add code to implement the Application\_Error handler as follows.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample4.cs)]

<span data-ttu-id="d7623-126">次に、エラー .aspx という名前のページをソリューションに追加し、このマークアップスニペットを追加します。</span><span class="sxs-lookup"><span data-stu-id="d7623-126">Then add a page named Error.aspx to the solution and add this markup snippet.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-8/samples/sample5.aspx)]

<span data-ttu-id="d7623-127">次に、ページ\_読み込みイベントハンドラーは、要求オブジェクトからエラーメッセージを抽出します。</span><span class="sxs-lookup"><span data-stu-id="d7623-127">Now in the Page\_Load event handler extract the error messages from the Request Object.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample6.cs)]

## <a id="_Toc260221683"></a><span data-ttu-id="d7623-128">最後</span><span class="sxs-lookup"><span data-stu-id="d7623-128">Conclusion</span></span>

<span data-ttu-id="d7623-129">ASP.NET WebForms により、データベースアクセス、メンバーシップ、AJAX などを使用して、洗練された web サイトを簡単に作成できることがわかりました。</span><span class="sxs-lookup"><span data-stu-id="d7623-129">We've seen that ASP.NET WebForms makes it easy to create a sophisticated website with database access, membership, AJAX, etc.</span></span> <span data-ttu-id="d7623-130">非常に迅速です。</span><span class="sxs-lookup"><span data-stu-id="d7623-130">pretty quickly.</span></span>

<span data-ttu-id="d7623-131">このチュートリアルでは、独自の ASP.NET WebForms アプリケーションの構築を開始するために必要なツールを提供しています。</span><span class="sxs-lookup"><span data-stu-id="d7623-131">Hopefully this tutorial has given you the tools you need to get started building your own ASP.NET WebForms applications!</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="d7623-132">[[戻る]](tailspin-spyworks-part-7.md)</span><span class="sxs-lookup"><span data-stu-id="d7623-132">[Previous](tailspin-spyworks-part-7.md)</span></span>
