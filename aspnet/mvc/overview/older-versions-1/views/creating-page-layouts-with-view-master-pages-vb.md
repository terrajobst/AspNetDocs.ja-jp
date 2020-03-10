---
uid: mvc/overview/older-versions-1/views/creating-page-layouts-with-view-master-pages-vb
title: ビューマスターページを使用したページレイアウトの作成 (VB) |Microsoft Docs
author: microsoft
description: このチュートリアルでは、ビューのマスターページを利用して、アプリケーションの複数のページに共通のページレイアウトを作成する方法について説明します。 使用できる...
ms.author: riande
ms.date: 10/16/2008
ms.assetid: d34f90a1-6de3-482a-a326-f87fdcbaaaff
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-page-layouts-with-view-master-pages-vb
msc.type: authoredcontent
ms.openlocfilehash: 97c0ecf1953cc54030656dd710a5150243877110
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78435202"
---
# <a name="creating-page-layouts-with-view-master-pages-vb"></a><span data-ttu-id="30e21-104">ビュー マスター ページでページ レイアウトを作成する (VB)</span><span class="sxs-lookup"><span data-stu-id="30e21-104">Creating Page Layouts with View Master Pages (VB)</span></span>

<span data-ttu-id="30e21-105">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="30e21-105">by [Microsoft](https://github.com/microsoft)</span></span>

<span data-ttu-id="30e21-106">[[Download PDF]\(PDF をダウンロード\)](https://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_12_VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="30e21-106">[Download PDF](https://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_12_VB.pdf)</span></span>

> <span data-ttu-id="30e21-107">このチュートリアルでは、ビューのマスターページを利用して、アプリケーションの複数のページに共通のページレイアウトを作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="30e21-107">In this tutorial, you learn how to create a common page layout for multiple pages in your application by taking advantage of view master pages.</span></span> <span data-ttu-id="30e21-108">ビューマスターページを使用すると、たとえば、2列のページレイアウトを定義し、web アプリケーションのすべてのページに2列のレイアウトを使用することができます。</span><span class="sxs-lookup"><span data-stu-id="30e21-108">You can use a view master page, for example, to define a two-column page layout and use the two-column layout for all of the pages in your web application.</span></span>

## <a name="creating-page-layouts-with-view-master-pages"></a><span data-ttu-id="30e21-109">ビューマスターページを使用したページレイアウトの作成</span><span class="sxs-lookup"><span data-stu-id="30e21-109">Creating Page Layouts with View Master Pages</span></span>

<span data-ttu-id="30e21-110">このチュートリアルでは、ビューのマスターページを利用して、アプリケーションの複数のページに共通のページレイアウトを作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="30e21-110">In this tutorial, you learn how to create a common page layout for multiple pages in your application by taking advantage of view master pages.</span></span> <span data-ttu-id="30e21-111">ビューマスターページを使用すると、たとえば、2列のページレイアウトを定義し、web アプリケーションのすべてのページに2列のレイアウトを使用することができます。</span><span class="sxs-lookup"><span data-stu-id="30e21-111">You can use a view master page, for example, to define a two-column page layout and use the two-column layout for all of the pages in your web application.</span></span>

<span data-ttu-id="30e21-112">また、ビューのマスターページを利用して、アプリケーション内の複数のページで共通のコンテンツを共有することもできます。</span><span class="sxs-lookup"><span data-stu-id="30e21-112">You also can take advantage of view master pages to share common content across multiple pages in your application.</span></span> <span data-ttu-id="30e21-113">たとえば、web サイトのロゴ、ナビゲーションリンク、およびバナー広告をビューマスターページに配置できます。</span><span class="sxs-lookup"><span data-stu-id="30e21-113">For example, you can place your website logo, navigation links, and banner advertisements in a view master page.</span></span> <span data-ttu-id="30e21-114">これにより、アプリケーションのすべてのページにこのコンテンツが自動的に表示されるようになります。</span><span class="sxs-lookup"><span data-stu-id="30e21-114">That way, every page in your application would display this content automatically.</span></span>

<span data-ttu-id="30e21-115">このチュートリアルでは、新しいビューマスターページを作成し、マスターページに基づいて新しいビューコンテンツページを作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="30e21-115">In this tutorial, you learn how to create a new view master page and create a new view content page based on the master page.</span></span>

### <a name="creating-a-view-master-page"></a><span data-ttu-id="30e21-116">ビューマスターページの作成</span><span class="sxs-lookup"><span data-stu-id="30e21-116">Creating a View Master Page</span></span>

<span data-ttu-id="30e21-117">まずは、2列のレイアウトを定義するビューマスターページを作成してみましょう。</span><span class="sxs-lookup"><span data-stu-id="30e21-117">Let's start by creating a view master page that defines a two-column layout.</span></span> <span data-ttu-id="30e21-118">MVC プロジェクトに新しいビューマスターページを追加するには、Views\Shared フォルダーを右クリックし、[追加] **、[新しい項目**] の順に選択して、mvc ビューのマスターページテンプレートを選択します (図1を参照)。</span><span class="sxs-lookup"><span data-stu-id="30e21-118">You add a new view master page to an MVC project by right-clicking the Views\Shared folder, selecting the menu option **Add, New Item**, and selecting the  MVC View Master Page template (see Figure 1).</span></span>

<span data-ttu-id="30e21-119">[ビューマスターページを追加 ![には](creating-page-layouts-with-view-master-pages-vb/_static/image2.png)](creating-page-layouts-with-view-master-pages-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="30e21-119">[![Adding a view master page](creating-page-layouts-with-view-master-pages-vb/_static/image2.png)](creating-page-layouts-with-view-master-pages-vb/_static/image1.png)</span></span>

<span data-ttu-id="30e21-120">**図 01**: ビューマスターページを追加[する (クリックすると、フルサイズの画像が表示](creating-page-layouts-with-view-master-pages-vb/_static/image3.png)される)</span><span class="sxs-lookup"><span data-stu-id="30e21-120">**Figure 01**: Adding a view master page ([Click to view full-size image](creating-page-layouts-with-view-master-pages-vb/_static/image3.png))</span></span>

<span data-ttu-id="30e21-121">アプリケーションでは、複数のビューマスターページを作成できます。</span><span class="sxs-lookup"><span data-stu-id="30e21-121">You can create more than one view master page in an application.</span></span> <span data-ttu-id="30e21-122">各ビューのマスターページでは、異なるページレイアウトを定義できます。</span><span class="sxs-lookup"><span data-stu-id="30e21-122">Each view master page can define a different page layout.</span></span> <span data-ttu-id="30e21-123">たとえば、特定のページに2列のレイアウトを設定し、他のページに3列のレイアウトを設定することができます。</span><span class="sxs-lookup"><span data-stu-id="30e21-123">For example, you might want certain pages to have a two-column layout and other pages to have a three-column layout.</span></span>

<span data-ttu-id="30e21-124">ビューのマスターページは、標準の ASP.NET MVC ビューによく似ています。</span><span class="sxs-lookup"><span data-stu-id="30e21-124">A view master page looks very much like a standard ASP.NET MVC view.</span></span> <span data-ttu-id="30e21-125">ただし、通常のビューとは異なり、ビューのマスターページには `<asp:ContentPlaceHolder>` タグが1つ以上含まれています。</span><span class="sxs-lookup"><span data-stu-id="30e21-125">However, unlike a normal view, a view master page contains one or more `<asp:ContentPlaceHolder>` tags.</span></span> <span data-ttu-id="30e21-126">`<contentplaceholder>` タグは、個々のコンテンツページでオーバーライドできるマスターページの領域をマークするために使用されます。</span><span class="sxs-lookup"><span data-stu-id="30e21-126">The `<contentplaceholder>` tags are used to mark the areas of the master page that can be overridden in an individual content page.</span></span>

<span data-ttu-id="30e21-127">たとえば、リスト1のビューマスターページでは、2列のレイアウトを定義します。</span><span class="sxs-lookup"><span data-stu-id="30e21-127">For example, the view master page in Listing 1 defines a two-column layout.</span></span> <span data-ttu-id="30e21-128">2つの `<contentplaceholder>` タグが含まれています。</span><span class="sxs-lookup"><span data-stu-id="30e21-128">It contains two `<contentplaceholder>` tags.</span></span> <span data-ttu-id="30e21-129">列ごとに1つの `<ContentPlaceHolder>`。</span><span class="sxs-lookup"><span data-stu-id="30e21-129">One `<ContentPlaceHolder>` for each column.</span></span>

<span data-ttu-id="30e21-130">**リスト1– `Views\Shared\Site.master`**</span><span class="sxs-lookup"><span data-stu-id="30e21-130">**Listing 1 – `Views\Shared\Site.master`**</span></span>

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample1.aspx)]

<span data-ttu-id="30e21-131">リスト1のビューマスターページの本文には、2つの列に対応する2つの `<div>` タグが含まれています。</span><span class="sxs-lookup"><span data-stu-id="30e21-131">The body of the view master page in Listing 1 contains two `<div>` tags that correspond to the two columns.</span></span> <span data-ttu-id="30e21-132">カスケードスタイルシートの列クラスは、両方の `<div>` タグに適用されます。</span><span class="sxs-lookup"><span data-stu-id="30e21-132">The Cascading Style Sheet column class is applied to both `<div>` tags.</span></span> <span data-ttu-id="30e21-133">このクラスは、マスターページの上部で宣言されているスタイルシートで定義されています。</span><span class="sxs-lookup"><span data-stu-id="30e21-133">This class is defined in the style sheet declared at the top of the master page.</span></span> <span data-ttu-id="30e21-134">デザインビューに切り替えると、ビューマスターページがどのように表示されるかをプレビューできます。</span><span class="sxs-lookup"><span data-stu-id="30e21-134">You can preview how the view master page will be rendered by switching to Design view.</span></span> <span data-ttu-id="30e21-135">ソースコードエディターの左下にある [デザイン] タブをクリックします (図2を参照)。</span><span class="sxs-lookup"><span data-stu-id="30e21-135">Click the Design tab at the bottom-left of the source code editor (see Figure 2).</span></span>

<span data-ttu-id="30e21-136">[デザイナーでマスターページをプレビュー ![には](creating-page-layouts-with-view-master-pages-vb/_static/image5.png)](creating-page-layouts-with-view-master-pages-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="30e21-136">[![Previewing a master page in the designer](creating-page-layouts-with-view-master-pages-vb/_static/image5.png)](creating-page-layouts-with-view-master-pages-vb/_static/image4.png)</span></span>

<span data-ttu-id="30e21-137">**図 02**: デザイナーでマスターページをプレビューする ([クリックすると、フルサイズの画像が表示](creating-page-layouts-with-view-master-pages-vb/_static/image6.png)されます)</span><span class="sxs-lookup"><span data-stu-id="30e21-137">**Figure 02**: Previewing a master page in the designer ([Click to view full-size image](creating-page-layouts-with-view-master-pages-vb/_static/image6.png))</span></span>

### <a name="creating-a-view-content-page"></a><span data-ttu-id="30e21-138">ビューコンテンツページを作成する</span><span class="sxs-lookup"><span data-stu-id="30e21-138">Creating a View Content Page</span></span>

<span data-ttu-id="30e21-139">ビューマスターページを作成した後、ビューマスターページに基づいて1つまたは複数のビューコンテンツページを作成できます。</span><span class="sxs-lookup"><span data-stu-id="30e21-139">After you create a view master page, you can create one or more view content pages based on the view master page.</span></span> <span data-ttu-id="30e21-140">たとえば、Home コントローラーのインデックスビューコンテンツページを作成するには、Views\Home フォルダーを右クリックし、[**追加]、[新しい項目**] の順に選択して、 **MVC ビューコンテンツページ**テンプレートを選択し、「」と入力して、[追加] ボタンをクリックします (図3を参照)。</span><span class="sxs-lookup"><span data-stu-id="30e21-140">For example, you can create an Index view content page for the Home controller by right-clicking the Views\Home folder, selecting **Add, New Item**, selecting the **MVC View Content Page** template, entering the name Index.aspx, and clicking the Add button (see Figure 3).</span></span>

<span data-ttu-id="30e21-141">[ビューコンテンツページを追加 ![には](creating-page-layouts-with-view-master-pages-vb/_static/image8.png)](creating-page-layouts-with-view-master-pages-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="30e21-141">[![Adding a view content page](creating-page-layouts-with-view-master-pages-vb/_static/image8.png)](creating-page-layouts-with-view-master-pages-vb/_static/image7.png)</span></span>

<span data-ttu-id="30e21-142">**図 03**: ビューコンテンツページを追加[する (クリックすると、フルサイズの画像が表示](creating-page-layouts-with-view-master-pages-vb/_static/image9.png)される)</span><span class="sxs-lookup"><span data-stu-id="30e21-142">**Figure 03**: Adding a view content page ([Click to view full-size image](creating-page-layouts-with-view-master-pages-vb/_static/image9.png))</span></span>

<span data-ttu-id="30e21-143">[追加] ボタンをクリックすると、新しいダイアログが表示され、[ビューのコンテンツ] ページに関連付けるビューマスターページを選択できます (図4を参照)。</span><span class="sxs-lookup"><span data-stu-id="30e21-143">After you click the Add button, a new dialog appears that enables you to select a view master page to associate with the view content page (see Figure 4).</span></span> <span data-ttu-id="30e21-144">前のセクションで作成したサイトのマスタービューマスターページに移動できます。</span><span class="sxs-lookup"><span data-stu-id="30e21-144">You can navigate to the Site.master view master page that we created in the previous section.</span></span>

<span data-ttu-id="30e21-145">[マスターページを選択 ![には](creating-page-layouts-with-view-master-pages-vb/_static/image11.png)](creating-page-layouts-with-view-master-pages-vb/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="30e21-145">[![Selecting a master page](creating-page-layouts-with-view-master-pages-vb/_static/image11.png)](creating-page-layouts-with-view-master-pages-vb/_static/image10.png)</span></span>

<span data-ttu-id="30e21-146">**図 04**: マスターページを選択[する (クリックすると、フルサイズの画像が表示](creating-page-layouts-with-view-master-pages-vb/_static/image12.png)される)</span><span class="sxs-lookup"><span data-stu-id="30e21-146">**Figure 04**: Selecting a master page ([Click to view full-size image](creating-page-layouts-with-view-master-pages-vb/_static/image12.png))</span></span>

<span data-ttu-id="30e21-147">新しいビューコンテンツページを作成した後に、そのマスターページをリスト2で取得します。</span><span class="sxs-lookup"><span data-stu-id="30e21-147">After you create a new view content page based on the Site.master master page, you get the file in Listing 2.</span></span>

<span data-ttu-id="30e21-148">**リスト2– `Views\Home\Index.aspx`**</span><span class="sxs-lookup"><span data-stu-id="30e21-148">**Listing 2 – `Views\Home\Index.aspx`**</span></span>

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample2.aspx)]

<span data-ttu-id="30e21-149">このビューには、ビューマスターページの `<asp:ContentPlaceHolder>` 各タグに対応する `<asp:Content>` タグが含まれていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="30e21-149">Notice that this view contains a `<asp:Content>` tag that corresponds to each of the `<asp:ContentPlaceHolder>` tags in the view master page.</span></span> <span data-ttu-id="30e21-150">各 `<asp:Content>` タグには、オーバーライドする特定の `<asp:ContentPlaceHolder>` を指す ContentPlaceHolderID 属性が含まれています。</span><span class="sxs-lookup"><span data-stu-id="30e21-150">Each `<asp:Content>` tag includes a ContentPlaceHolderID attribute that points to the particular `<asp:ContentPlaceHolder>` that it overrides.</span></span>

<span data-ttu-id="30e21-151">さらに、リスト2の [コンテンツビュー] ページには、通常のオープンおよび終了 HTML タグは含まれていません。</span><span class="sxs-lookup"><span data-stu-id="30e21-151">Notice, furthermore, that the content view page in Listing 2 does not contain any of the normal opening and closing HTML tags.</span></span> <span data-ttu-id="30e21-152">たとえば、開始タグと終了 `<html>` タグや `<head>` タグは含まれません。</span><span class="sxs-lookup"><span data-stu-id="30e21-152">For example, it does not contain the opening and closing `<html>` or `<head>` tags.</span></span> <span data-ttu-id="30e21-153">通常の開始タグと終了タグはすべて、ビューマスターページに含まれています。</span><span class="sxs-lookup"><span data-stu-id="30e21-153">All of the normal opening and closing tags are contained in the view master page.</span></span>

<span data-ttu-id="30e21-154">ビューコンテンツページに表示するコンテンツは、`<asp:Content>` タグ内に配置する必要があります。</span><span class="sxs-lookup"><span data-stu-id="30e21-154">Any content that you want to display in a view content page must be placed within a `<asp:Content>` tag.</span></span> <span data-ttu-id="30e21-155">これらのタグの外側に HTML またはその他のコンテンツを配置すると、ページを表示しようとしたときにエラーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="30e21-155">If you place any HTML or other content outside of these tags, then you will get an error when you attempt to view the page.</span></span>

<span data-ttu-id="30e21-156">コンテンツビューページのマスターページから、すべての `<asp:ContentPlaceHolder>` タグをオーバーライドする必要はありません。</span><span class="sxs-lookup"><span data-stu-id="30e21-156">You don't need to override every `<asp:ContentPlaceHolder>` tag from a master page in a content view page.</span></span> <span data-ttu-id="30e21-157">タグを特定のコンテンツに置き換える場合にのみ、`<asp:ContentPlaceHolder>` タグをオーバーライドする必要があります。</span><span class="sxs-lookup"><span data-stu-id="30e21-157">You only need to override a `<asp:ContentPlaceHolder>` tag when you want to replace the tag with particular content.</span></span>

<span data-ttu-id="30e21-158">たとえば、リスト3の変更されたインデックスビューに含まれる `<asp:Content>` タグは2つだけです。</span><span class="sxs-lookup"><span data-stu-id="30e21-158">For example, the modified Index view in Listing 3 contains only two `<asp:Content>` tags.</span></span> <span data-ttu-id="30e21-159">`<asp:Content>` の各タグには、いくつかのテキストが含まれています。</span><span class="sxs-lookup"><span data-stu-id="30e21-159">Each of the `<asp:Content>` tags includes some text.</span></span>

<span data-ttu-id="30e21-160">**リスト3– `Views\Home\Index.aspx (modified)`**</span><span class="sxs-lookup"><span data-stu-id="30e21-160">**Listing 3 – `Views\Home\Index.aspx (modified)`**</span></span>

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample3.aspx)]

<span data-ttu-id="30e21-161">リスト3のビューが要求されると、図5のページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="30e21-161">When the view in Listing 3 is requested, it renders the page in Figure 5.</span></span> <span data-ttu-id="30e21-162">ビューでは、2つの列を含むページが表示されることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="30e21-162">Notice that the view renders a page with two columns.</span></span> <span data-ttu-id="30e21-163">さらに、[ビューコンテンツ] ページのコンテンツがビューマスターページのコンテンツとマージされていることにも注意してください。</span><span class="sxs-lookup"><span data-stu-id="30e21-163">Notice, furthermore, that the content from the view content page is merged with the content from the view master page.</span></span>

<span data-ttu-id="30e21-164">[インデックスビューのコンテンツページの ![](creating-page-layouts-with-view-master-pages-vb/_static/image14.png)](creating-page-layouts-with-view-master-pages-vb/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="30e21-164">[![The Index view content page](creating-page-layouts-with-view-master-pages-vb/_static/image14.png)](creating-page-layouts-with-view-master-pages-vb/_static/image13.png)</span></span>

<span data-ttu-id="30e21-165">**図 05**: インデックスビューのコンテンツページ ([クリックすると、フルサイズの画像が表示](creating-page-layouts-with-view-master-pages-vb/_static/image15.png)されます)</span><span class="sxs-lookup"><span data-stu-id="30e21-165">**Figure 05**: The Index view content page ([Click to view full-size image](creating-page-layouts-with-view-master-pages-vb/_static/image15.png))</span></span>

### <a name="modifying-view-master-page-content"></a><span data-ttu-id="30e21-166">ビューマスターページのコンテンツの変更</span><span class="sxs-lookup"><span data-stu-id="30e21-166">Modifying View Master Page Content</span></span>

<span data-ttu-id="30e21-167">ビューのマスターページを操作するときにほぼ即座に発生する問題の1つは、異なるビューコンテンツページが要求されたときにビューマスターページのコンテンツを変更するという問題です。</span><span class="sxs-lookup"><span data-stu-id="30e21-167">One issue that you encounter almost immediately when working with view master pages is the problem of modifying view master page content when different view content pages are requested.</span></span> <span data-ttu-id="30e21-168">たとえば、web アプリケーションの各ページに一意のタイトルを付けることができます。</span><span class="sxs-lookup"><span data-stu-id="30e21-168">For example, you want each page in your web application to have a unique title.</span></span> <span data-ttu-id="30e21-169">ただし、タイトルはビューの [コンテンツ] ページではなく、ビューマスターページで宣言されています。</span><span class="sxs-lookup"><span data-stu-id="30e21-169">However, the title is declared in the view master page and not in the view content page.</span></span> <span data-ttu-id="30e21-170">では、各ビューコンテンツページのページタイトルをカスタマイズするにはどうすればよいでしょうか。</span><span class="sxs-lookup"><span data-stu-id="30e21-170">So, how do you customize the page title for each view content page?</span></span>

<span data-ttu-id="30e21-171">ビューコンテンツページに表示されるタイトルを変更するには、2つの方法があります。</span><span class="sxs-lookup"><span data-stu-id="30e21-171">There are two ways that you can modify the title displayed by a view content page.</span></span> <span data-ttu-id="30e21-172">まず、ビューコンテンツページの上部で宣言されている `<%@ page %>` ディレクティブの title 属性にページタイトルを割り当てることができます。</span><span class="sxs-lookup"><span data-stu-id="30e21-172">First, you can assign a page title to the title attribute of the `<%@ page %>` directive declared at the top of a view content page.</span></span> <span data-ttu-id="30e21-173">たとえば、ページタイトル "Super 素晴らしい Web サイト" をインデックスビューに割り当てる場合は、インデックスビューの先頭に次のディレクティブを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="30e21-173">For example, if you want to assign the page title "Super Great Website" to the Index view, then you can include the following directive at the top of the Index view:</span></span>

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample4.aspx)]

<span data-ttu-id="30e21-174">インデックスビューがブラウザーに表示されると、ブラウザーのタイトルバーに必要なタイトルが表示されます。</span><span class="sxs-lookup"><span data-stu-id="30e21-174">When the Index view is rendered to the browser, the desired title appears in the browser title bar:</span></span>

<span data-ttu-id="30e21-175">[![ブラウザーのタイトルバー](creating-page-layouts-with-view-master-pages-vb/_static/image17.png)](creating-page-layouts-with-view-master-pages-vb/_static/image16.png)</span><span class="sxs-lookup"><span data-stu-id="30e21-175">[![Browser title bar](creating-page-layouts-with-view-master-pages-vb/_static/image17.png)](creating-page-layouts-with-view-master-pages-vb/_static/image16.png)</span></span>

<span data-ttu-id="30e21-176">Title 属性が機能するためには、マスタービューページが満たす必要のある重要な要件が1つあります。</span><span class="sxs-lookup"><span data-stu-id="30e21-176">There is one important requirement that a master view page must satisfy in order for the title attribute to work.</span></span> <span data-ttu-id="30e21-177">ビューマスターページには、ヘッダーの通常の `<head>` タグではなく、`<head runat="server">` タグが含まれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="30e21-177">The view master page must contain a `<head runat="server">` tag instead of a normal `<head>` tag for its header.</span></span> <span data-ttu-id="30e21-178">`<head>` タグに runat = "server" 属性が含まれていない場合、タイトルは表示されません。</span><span class="sxs-lookup"><span data-stu-id="30e21-178">If the `<head>` tag does not include the runat="server" attribute then the title won't appear.</span></span> <span data-ttu-id="30e21-179">既定のビューマスターページには、必須の `<head runat="server">` タグが含まれています。</span><span class="sxs-lookup"><span data-stu-id="30e21-179">The default view master page includes the required `<head runat="server">` tag.</span></span>

<span data-ttu-id="30e21-180">個々のビューコンテンツページからマスターページのコンテンツを変更する別の方法として、`<asp:ContentPlaceHolder>` タグで変更する領域をラップすることもできます。</span><span class="sxs-lookup"><span data-stu-id="30e21-180">An alternative approach to modifying master page content from an individual view content page is to wrap the region that you want to modify in a `<asp:ContentPlaceHolder>` tag.</span></span> <span data-ttu-id="30e21-181">たとえば、タイトルだけでなく、meta タグもマスタービューページによって表示されるように変更する場合を考えてみます。</span><span class="sxs-lookup"><span data-stu-id="30e21-181">For example, imagine that you want to change not only the title, but also the meta tags, rendered by a master view page.</span></span> <span data-ttu-id="30e21-182">リスト4のマスタービューページには、`<head>` タグ内の `<asp:ContentPlaceHolder>` タグが含まれています。</span><span class="sxs-lookup"><span data-stu-id="30e21-182">The master view page in Listing 4 contains a `<asp:ContentPlaceHolder>` tag within its `<head>` tag.</span></span>

<span data-ttu-id="30e21-183">**リスト4– `Views\Shared\Site2.master`**</span><span class="sxs-lookup"><span data-stu-id="30e21-183">**Listing 4 – `Views\Shared\Site2.master`**</span></span>

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample5.aspx)]

<span data-ttu-id="30e21-184">リスト4の `<asp:ContentPlaceHolder>` タグに既定のコンテンツ (既定のタイトルと既定のメタタグ) が含まれていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="30e21-184">Notice that the `<asp:ContentPlaceHolder>` tag in Listing 4 includes default content: a default title and default meta tags.</span></span> <span data-ttu-id="30e21-185">個々のビューコンテンツページでこの `<asp:ContentPlaceHolder>` タグをオーバーライドしない場合、既定のコンテンツが表示されます。</span><span class="sxs-lookup"><span data-stu-id="30e21-185">If you don't override this `<asp:ContentPlaceHolder>` tag in an individual view content page, then the default content will be displayed.</span></span>

<span data-ttu-id="30e21-186">リスト5の [コンテンツビュー] ページでは、カスタムタイトルとカスタムメタタグを表示するために `<asp:ContentPlaceHolder>` タグがオーバーライドされます。</span><span class="sxs-lookup"><span data-stu-id="30e21-186">The content view page in Listing 5 overrides the `<asp:ContentPlaceHolder>` tag in order to display a custom title and custom meta tags.</span></span>

<span data-ttu-id="30e21-187">**リスト5– `Views\Home\Index2.aspx`**</span><span class="sxs-lookup"><span data-stu-id="30e21-187">**Listing 5 – `Views\Home\Index2.aspx`**</span></span>

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample6.aspx)]

### <a name="summary"></a><span data-ttu-id="30e21-188">まとめ</span><span class="sxs-lookup"><span data-stu-id="30e21-188">Summary</span></span>

<span data-ttu-id="30e21-189">このチュートリアルでは、マスターページの表示とコンテンツページの表示の基本的な概要について説明しました。</span><span class="sxs-lookup"><span data-stu-id="30e21-189">This tutorial provided you with a basic introduction to view master pages and view content pages.</span></span> <span data-ttu-id="30e21-190">新しいビューマスターページを作成し、それらに基づいてビューコンテンツページを作成する方法について学習しました。</span><span class="sxs-lookup"><span data-stu-id="30e21-190">You learned how to create new view master pages and create view content pages based on them.</span></span> <span data-ttu-id="30e21-191">また、特定のビューコンテンツページからビューマスターページのコンテンツを変更する方法についても説明します。</span><span class="sxs-lookup"><span data-stu-id="30e21-191">We also examined how you can modify the content of a view master page from a particular view content page.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="30e21-192">[前へ](using-the-tagbuilder-class-to-build-html-helpers-vb.md)
> [次へ](passing-data-to-view-master-pages-vb.md)</span><span class="sxs-lookup"><span data-stu-id="30e21-192">[Previous](using-the-tagbuilder-class-to-build-html-helpers-vb.md)
[Next](passing-data-to-view-master-pages-vb.md)</span></span>
