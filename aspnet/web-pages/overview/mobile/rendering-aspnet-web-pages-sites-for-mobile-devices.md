---
uid: web-pages/overview/mobile/rendering-aspnet-web-pages-sites-for-mobile-devices
title: モバイルデバイス用の ASP.NET Web ページ (Razor) サイトのレンダリング |Microsoft Docs
author: Rick-Anderson
description: 'この記事では、モバイルデバイスに適切に表示される ASP.NET Web ページ (Razor) サイトでページを作成する方法について説明します。 学習内容: 操作方法...'
ms.author: riande
ms.date: 02/17/2014
ms.assetid: f15ab392-c05e-4269-83bf-7c6d2b8c8ec8
msc.legacyurl: /web-pages/overview/mobile/rendering-aspnet-web-pages-sites-for-mobile-devices
msc.type: authoredcontent
ms.openlocfilehash: c012348d65e48a275cb0e4808fef2a7f31e5fb33
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78454354"
---
# <a name="rendering-aspnet-web-pages-razor-sites-for-mobile-devices"></a><span data-ttu-id="eab4c-104">モバイルデバイスのレンダリング ASP.NET Web ページ (Razor) サイト</span><span class="sxs-lookup"><span data-stu-id="eab4c-104">Rendering ASP.NET Web Pages (Razor) Sites for Mobile Devices</span></span>

<span data-ttu-id="eab4c-105">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="eab4c-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="eab4c-106">この記事では、モバイルデバイスに適切に表示される ASP.NET Web ページ (Razor) サイトでページを作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="eab4c-106">This article describes how to create pages in an ASP.NET Web Pages (Razor) site that will render appropriately on mobile devices.</span></span>
> 
> <span data-ttu-id="eab4c-107">ここでは、次の内容について学習します。</span><span class="sxs-lookup"><span data-stu-id="eab4c-107">What you'll learn:</span></span>
> 
> - <span data-ttu-id="eab4c-108">名前付け規則を使用して、ページがモバイルデバイス専用に設計されていることを指定する方法。</span><span class="sxs-lookup"><span data-stu-id="eab4c-108">How to use a naming convention to specify that a page is designed specifically for mobile devices.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="eab4c-109">このチュートリアルで使用されているソフトウェアのバージョン</span><span class="sxs-lookup"><span data-stu-id="eab4c-109">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="eab4c-110">ASP.NET Web ページ (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="eab4c-110">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="eab4c-111">このチュートリアルは ASP.NET Web ページ2でも動作します。</span><span class="sxs-lookup"><span data-stu-id="eab4c-111">This tutorial also works with ASP.NET Web Pages 2.</span></span>

<span data-ttu-id="eab4c-112">ASP.NET Web ページを使用すると、モバイルデバイスまたはその他のデバイスでコンテンツを表示するためのカスタム表示を作成できます。</span><span class="sxs-lookup"><span data-stu-id="eab4c-112">ASP.NET Web Pages lets you create custom displays for rendering content on mobile or other devices.</span></span>

<span data-ttu-id="eab4c-113">ASP.NET Web ページサイトにデバイス固有のページを作成する最も簡単な方法は、ファイル名の形式でファイル名を使用する方法です。たとえば、「 *FileName. Mobile. cshtml*」と指定します。</span><span class="sxs-lookup"><span data-stu-id="eab4c-113">The simplest way to create device-specific page in an ASP.NET Web Pages site is by using a file-naming pattern like this: *FileName.Mobile.cshtml*.</span></span> <span data-ttu-id="eab4c-114">ページの2つのバージョンを作成できます (たとえば、 *myfile.txt*という名前の1つと、 *myfile.txt*という名前の1つ)。</span><span class="sxs-lookup"><span data-stu-id="eab4c-114">You can create two versions of a page (for example, one named *MyFile.cshtml* and one named *MyFile.Mobile.cshtml*).</span></span> <span data-ttu-id="eab4c-115">実行時に、モバイルデバイスが*myfile.txt*を要求すると、ASP.NET は、 *myfile.txt*からコンテンツをレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="eab4c-115">At run time, when a mobile device requests *MyFile.cshtml*, ASP.NET renders the content from *MyFile.Mobile.cshtml*.</span></span> <span data-ttu-id="eab4c-116">それ以外の場合は、 *myfile.txt*がレンダリングされます。</span><span class="sxs-lookup"><span data-stu-id="eab4c-116">Otherwise, *MyFile.cshtml* is rendered.</span></span>

<span data-ttu-id="eab4c-117">次の例は、モバイルデバイスのコンテンツページを追加することによって、モバイルレンダリングを有効にする方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="eab4c-117">The following example shows how to enable mobile rendering by adding a content page for mobile devices.</span></span> <span data-ttu-id="eab4c-118">*Page1*には、コンテンツとナビゲーションサイドバーが含まれています。</span><span class="sxs-lookup"><span data-stu-id="eab4c-118">*Page1.cshtml* contains content plus a navigation sidebar.</span></span> <span data-ttu-id="eab4c-119">*Page1*には同じコンテンツが含まれていますが、サイドバーは省略されています。</span><span class="sxs-lookup"><span data-stu-id="eab4c-119">*Page1.Mobile.cshtml* contains the same content, but omits the sidebar.</span></span>

1. <span data-ttu-id="eab4c-120">ASP.NET Web ページサイトで、 *Page1*という名前のファイルを作成し、現在の内容を次のマークアップに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="eab4c-120">In an ASP.NET Web Pages site, create a file named *Page1.cshtml* and replace the current content with following markup.</span></span>

    [!code-html[Main](rendering-aspnet-web-pages-sites-for-mobile-devices/samples/sample1.html)]
2. <span data-ttu-id="eab4c-121">*Page1*という名前のファイルを作成し、既存の内容を次のマークアップに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="eab4c-121">Create a file named *Page1.Mobile.cshtml* and replace the existing content with the following markup.</span></span> <span data-ttu-id="eab4c-122">モバイルバージョンのページでは、より小さい画面でのレンダリングを改善するためにナビゲーションセクションが省略されていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="eab4c-122">Notice that the mobile version of the page omits the navigation section for better rendering on a smaller screen.</span></span>

    [!code-html[Main](rendering-aspnet-web-pages-sites-for-mobile-devices/samples/sample2.html)]
3. <span data-ttu-id="eab4c-123">デスクトップブラウザーを実行し、 *Page1*に移動します。</span><span class="sxs-lookup"><span data-stu-id="eab4c-123">Run a desktop browser and browse to *Page1.cshtml*.</span></span> <span data-ttu-id="eab4c-124">![mobil-1](rendering-aspnet-web-pages-sites-for-mobile-devices/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="eab4c-124">![mobilesites-1](rendering-aspnet-web-pages-sites-for-mobile-devices/_static/image1.png)</span></span>
4. <span data-ttu-id="eab4c-125">モバイルブラウザー (またはモバイルデバイスエミュレーター) を実行し、 *Page1*に移動します。</span><span class="sxs-lookup"><span data-stu-id="eab4c-125">Run a mobile browser (or a mobile device emulator) and browse to *Page1.cshtml*.</span></span> <span data-ttu-id="eab4c-126">( *. Mobile*は含まれていないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="eab4c-126">(Notice that you do not include *.mobile.*</span></span> <span data-ttu-id="eab4c-127">URL の一部として。)要求が*page1*に対して行う場合でも、ASP.NET は*page1*をレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="eab4c-127">as part of the URL.) Even though the request is to *Page1.cshtml*, ASP.NET renders *Page1.Mobile.cshtml*.</span></span>

    ![mobilesites 2](rendering-aspnet-web-pages-sites-for-mobile-devices/_static/image2.png)

> [!NOTE]
> <span data-ttu-id="eab4c-129">モバイルページをテストするには、デスクトップコンピューターで実行されるモバイルデバイスシミュレーターを使用します。</span><span class="sxs-lookup"><span data-stu-id="eab4c-129">To test mobile pages, you can use a mobile device simulator that runs on a desktop computer.</span></span> <span data-ttu-id="eab4c-130">このツールを使用すると、モバイルデバイスで見ているように web ページをテストできます (通常、表示領域が非常に小さくなります)。</span><span class="sxs-lookup"><span data-stu-id="eab4c-130">This tool lets you test web pages as they would look on mobile devices (that is, typically with a much smaller display area).</span></span> <span data-ttu-id="eab4c-131">シミュレーターの1つの例として、Mozilla Firefox 用の[ユーザーエージェントスイッチャーアドオン](http://addons.mozilla.org/firefox/addon/user-agent-switcher/)があります。これにより、デスクトップバージョンの firefox からさまざまなモバイルブラウザーをエミュレートできます。</span><span class="sxs-lookup"><span data-stu-id="eab4c-131">One example of a simulator is the [User Agent Switcher add-on](http://addons.mozilla.org/firefox/addon/user-agent-switcher/) for Mozilla Firefox, which lets you emulate various mobile browsers from a desktop version of Firefox.</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="eab4c-132">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="eab4c-132">Additional Resources</span></span>

<span data-ttu-id="eab4c-133">[Windows Phone エミュレーター](https://msdn.microsoft.com/library/ff402563(v=VS.92).aspx)</span><span class="sxs-lookup"><span data-stu-id="eab4c-133">[Windows Phone Emulator](https://msdn.microsoft.com/library/ff402563(v=VS.92).aspx)</span></span>
