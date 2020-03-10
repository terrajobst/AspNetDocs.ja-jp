---
uid: web-forms/overview/ajax-control-toolkit/htmleditor/how-do-i-use-the-html-editor-control-cs
title: HTML エディターコントロールを使用操作方法には (C#) |Microsoft Docs
author: microsoft
description: HTMLEditor は、ツールバーのボタンを使用して HTML コンテンツを簡単に作成および編集できるようにする ASP.NET AJAX コントロールです。
ms.author: riande
ms.date: 05/12/2009
ms.assetid: f47e6224-c2e5-4472-b069-b6c7b6115200
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/htmleditor/how-do-i-use-the-html-editor-control-cs
msc.type: authoredcontent
ms.openlocfilehash: cb7d75b59b1361abeb6d3c38ad6e42e34d6e3f7b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78466606"
---
# <a name="how-do-i-use-the-html-editor-control-c"></a><span data-ttu-id="7cef4-104">HTML エディターコントロールを使用操作方法には</span><span class="sxs-lookup"><span data-stu-id="7cef4-104">How do I use the HTML Editor Control?</span></span> <span data-ttu-id="7cef4-105">(C#)</span><span class="sxs-lookup"><span data-stu-id="7cef4-105">(C#)</span></span>

<span data-ttu-id="7cef4-106">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="7cef4-106">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="7cef4-107">HTMLEditor は、ツールバーのボタンを使用して HTML コンテンツを簡単に作成および編集できるようにする ASP.NET AJAX コントロールです。</span><span class="sxs-lookup"><span data-stu-id="7cef4-107">HTMLEditor is an ASP.NET AJAX Control that allows you to easily create and edit HTML content via buttons in a toolbar.</span></span>

<span data-ttu-id="7cef4-108">このチュートリアルの目的は、AJAX Control Toolkit に含まれている HTML エディターコントロールの概要を説明することです。</span><span class="sxs-lookup"><span data-stu-id="7cef4-108">The goal of this tutorial is to provide you with an overview of the HTML Editor control included with the AJAX Control Toolkit.</span></span> <span data-ttu-id="7cef4-109">HTML エディターには、フォントサイズの変更、フォントの選択、背景色の変更、前景色の変更、リンクの追加、イメージの追加、テキストの配置の変更、および切り取り、コピー、貼り付けの操作 (図1を参照) を行うためのオプションが含まれています。</span><span class="sxs-lookup"><span data-stu-id="7cef4-109">The HTML Editor includes options for changing font size, selecting a font, changing background color, modifying the foreground color, adding links, adding images, changing text alignment, and performing cut, copy, and paste operations (see Figure 1).</span></span>

<span data-ttu-id="7cef4-110">[HTML エディターの ![](how-do-i-use-the-html-editor-control-cs/_static/image1.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="7cef4-110">[![The HTML Editor](how-do-i-use-the-html-editor-control-cs/_static/image1.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image1.png)</span></span>

<span data-ttu-id="7cef4-111">**図 01**: HTML エディター ([クリックすると、フルサイズの画像が表示](how-do-i-use-the-html-editor-control-cs/_static/image2.png)されます)</span><span class="sxs-lookup"><span data-stu-id="7cef4-111">**Figure 01**: The HTML Editor([Click to view full-size image](how-do-i-use-the-html-editor-control-cs/_static/image2.png))</span></span>

<span data-ttu-id="7cef4-112">HTML エディターを使用すると、デザインモードでコンテンツを入力したり、HTML を直接入力したりできます。</span><span class="sxs-lookup"><span data-stu-id="7cef4-112">The HTML editor enables you to enter content using a design mode or you can enter HTML directly.</span></span> <span data-ttu-id="7cef4-113">HTML コンテンツをプレビューするオプションも用意されています (図2を参照)。</span><span class="sxs-lookup"><span data-stu-id="7cef4-113">You also are provided with the option to preview your HTML content (see Figure 2).</span></span>

<span data-ttu-id="7cef4-114">[![デザイン、HTML、およびプレビューボタン](how-do-i-use-the-html-editor-control-cs/_static/image2.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="7cef4-114">[![Design, HTML, and Preview buttons](how-do-i-use-the-html-editor-control-cs/_static/image2.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image3.png)</span></span>

<span data-ttu-id="7cef4-115">**図 02**: デザイン、HTML、およびプレビューのボタン ([クリックしてフルサイズのイメージを表示](how-do-i-use-the-html-editor-control-cs/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="7cef4-115">**Figure 02**: Design, HTML, and Preview buttons([Click to view full-size image](how-do-i-use-the-html-editor-control-cs/_static/image4.png))</span></span>

<span data-ttu-id="7cef4-116">このチュートリアルでは、HTML エディターを表示する方法、HTML エディターに表示されるツールバーボタンをカスタマイズする方法、クロスサイトスクリプト攻撃を回避する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="7cef4-116">In this tutorial, you learn how to display the HTML Editor, how to customize the toolbar buttons that appear in the HTML Editor, and how to avoid Cross-Site Scripting Attacks.</span></span>

## <a name="displaying-the-html-editor"></a><span data-ttu-id="7cef4-117">HTML エディターを表示する</span><span class="sxs-lookup"><span data-stu-id="7cef4-117">Displaying the HTML Editor</span></span>

<span data-ttu-id="7cef4-118">ASP.NET ページで HTML エディターを使用するには、まず、ScriptManager コントロールをページに追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7cef4-118">Before you can use the HTML Editor in an ASP.NET page, you must first add a ScriptManager control to the page.</span></span> <span data-ttu-id="7cef4-119">ScriptManager コントロールは、Visual Studio/Visual Web Developer Express ツールボックスの [AJAX 拡張] タブの下にあります。</span><span class="sxs-lookup"><span data-stu-id="7cef4-119">The ScriptManager control is located beneath the AJAX Extensions tab in the Visual Studio/Visual Web Developer Express toolbox.</span></span>

<span data-ttu-id="7cef4-120">ScriptManager コントロールは、ページ上の他のコントロールの前に、ページの一番上に配置する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7cef4-120">You should place the ScriptManager control at the top of the page before any other controls on the page.</span></span> <span data-ttu-id="7cef4-121">たとえば、開いているサーバー側の &lt;フォーム&gt; タグのすぐ下に配置できます。</span><span class="sxs-lookup"><span data-stu-id="7cef4-121">For example, you can place it immediately below the opening server-side &lt;form&gt; tag.</span></span>

<span data-ttu-id="7cef4-122">HTML エディターコントロールは、他の AJAX コントロールツールキットコントロールと共にツールボックスに配置されます。</span><span class="sxs-lookup"><span data-stu-id="7cef4-122">The HTML Editor control is located in the toolbox with the rest of the AJAX Control Toolkit controls.</span></span> <span data-ttu-id="7cef4-123">これは、エディターコントロールと呼ばれます (図3を参照)。</span><span class="sxs-lookup"><span data-stu-id="7cef4-123">It is named the Editor control (see Figure 3).</span></span>

<span data-ttu-id="7cef4-124">[HTML エディターコントロールの ![](how-do-i-use-the-html-editor-control-cs/_static/image3.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="7cef4-124">[![The HTML Editor control](how-do-i-use-the-html-editor-control-cs/_static/image3.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image5.png)</span></span>

<span data-ttu-id="7cef4-125">**図 03**: HTML エディターコントロール ([クリックしてフルサイズのイメージを表示する](how-do-i-use-the-html-editor-control-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="7cef4-125">**Figure 03**: The HTML Editor control([Click to view full-size image](how-do-i-use-the-html-editor-control-cs/_static/image6.png))</span></span>

<span data-ttu-id="7cef4-126">HTML エディターをページにドラッグした後は、プロパティシートでそのプロパティを設定できます。</span><span class="sxs-lookup"><span data-stu-id="7cef4-126">After you drag the HTML Editor onto a page, you can set its properties in the property sheet.</span></span> <span data-ttu-id="7cef4-127">たとえば、通常は Width プロパティと Height プロパティを設定します。</span><span class="sxs-lookup"><span data-stu-id="7cef4-127">For example, you normally want to set the Width and Height properties.</span></span> <span data-ttu-id="7cef4-128">リスト1には、HTML エディターを含む ASP.NET ページのソースが含まれています。</span><span class="sxs-lookup"><span data-stu-id="7cef4-128">Listing 1 contains the source for an ASP.NET page that contains an HTML editor.</span></span>

<span data-ttu-id="7cef4-129">**リスト 1-SimpleEditor .aspx**</span><span class="sxs-lookup"><span data-stu-id="7cef4-129">**Listing 1 - SimpleEditor.aspx**</span></span>

[!code-aspx[Main](how-do-i-use-the-html-editor-control-cs/samples/sample1.aspx)]

<span data-ttu-id="7cef4-130">リスト1のページには、HTML エディターコントロール、ボタンコントロール、およびリテラルコントロールが含まれています。</span><span class="sxs-lookup"><span data-stu-id="7cef4-130">The page in Listing 1 contains an HTML Editor control, a Button control, and a Literal control.</span></span> <span data-ttu-id="7cef4-131">このボタンをクリックすると、HTML エディターの内容がリテラルコントロールに表示されます (図4を参照)。</span><span class="sxs-lookup"><span data-stu-id="7cef4-131">When you click the button, the contents of the HTML Editor appear in the Literal control (see Figure 4).</span></span>

<span data-ttu-id="7cef4-132">[HTML エディターを使用してフォームを送信 ![には](how-do-i-use-the-html-editor-control-cs/_static/image4.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="7cef4-132">[![Submitting a form with an HTML Editor](how-do-i-use-the-html-editor-control-cs/_static/image4.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image7.png)</span></span>

<span data-ttu-id="7cef4-133">**図 04**: HTML エディターを使用してフォームを送信[する (クリックすると、フルサイズの画像が表示](how-do-i-use-the-html-editor-control-cs/_static/image8.png)されます)</span><span class="sxs-lookup"><span data-stu-id="7cef4-133">**Figure 04**: Submitting a form with an HTML Editor([Click to view full-size image](how-do-i-use-the-html-editor-control-cs/_static/image8.png))</span></span>

<span data-ttu-id="7cef4-134">Html エディターのコンテンツプロパティは、html エディターに入力された HTML コンテンツを取得するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="7cef4-134">The HTML Editor Content property is used to retrieve the HTML content entered into the HTML Editor.</span></span> <span data-ttu-id="7cef4-135">この HTML コンテンツには JavaScript を含めることができることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="7cef4-135">Be aware that this HTML content can contain JavaScript.</span></span> <span data-ttu-id="7cef4-136">次のセクションでは、JavaScript インジェクション攻撃を防ぐ方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="7cef4-136">In the next section, we discuss how you can prevent JavaScript Injection Attacks.</span></span>

## <a name="customizing-the-html-editor-toolbar"></a><span data-ttu-id="7cef4-137">HTML エディターツールバーのカスタマイズ</span><span class="sxs-lookup"><span data-stu-id="7cef4-137">Customizing the HTML Editor Toolbar</span></span>

<span data-ttu-id="7cef4-138">エディターに表示されるボタンを正確にカスタマイズできます。</span><span class="sxs-lookup"><span data-stu-id="7cef4-138">You can customize exactly which buttons appear in the editor.</span></span> <span data-ttu-id="7cef4-139">たとえば、ユーザーが html エディターを HTML モードに切り替えられないようにするには、[HTML] タブを削除します。</span><span class="sxs-lookup"><span data-stu-id="7cef4-139">For example, you might want to remove the HTML tab to prevent users from switching the HTML Editor into HTML mode.</span></span> <span data-ttu-id="7cef4-140">または、[フォントサイズ] ドロップダウンリストを削除して、ユーザーがフォーラムのメッセージの投稿で極端に大きいテキストを作成できないようにすることもできます (図5を参照)。</span><span class="sxs-lookup"><span data-stu-id="7cef4-140">Or, you might want to remove the font size dropdown list to prevent users from creating overly large text in a forum message post (see Figure 5).</span></span>

<span data-ttu-id="7cef4-141">[カスタマイズされた HTML エディターの ![](how-do-i-use-the-html-editor-control-cs/_static/image5.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="7cef4-141">[![A customized HTML Editor](how-do-i-use-the-html-editor-control-cs/_static/image5.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image9.png)</span></span>

<span data-ttu-id="7cef4-142">**図 05**: カスタマイズされた HTML エディター ([クリックしてフルサイズのイメージを表示する](how-do-i-use-the-html-editor-control-cs/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="7cef4-142">**Figure 05**: A customized HTML Editor([Click to view full-size image](how-do-i-use-the-html-editor-control-cs/_static/image10.png))</span></span>

<span data-ttu-id="7cef4-143">ツールバーのボタンをカスタマイズするには、基本エディタークラスから新しい HTML エディターを派生させます。</span><span class="sxs-lookup"><span data-stu-id="7cef4-143">You customize the toolbar buttons by deriving a new HTML Editor from the base Editor class.</span></span> <span data-ttu-id="7cef4-144">たとえば、リスト2のカスタムエディターには、太字と斜体のツールバーボタンのみが含まれています。</span><span class="sxs-lookup"><span data-stu-id="7cef4-144">For example, the custom editor in Listing 2 only contains toolbar buttons for bold and italic.</span></span> <span data-ttu-id="7cef4-145">その他のツールバーボタンはすべて削除されました。</span><span class="sxs-lookup"><span data-stu-id="7cef4-145">All other toolbar buttons have been removed.</span></span> <span data-ttu-id="7cef4-146">さらに、エディターの下部から [HTML] タブが削除されています (ただし、[デザイン] タブと [プレビュー] タブはまだ表示されています)。</span><span class="sxs-lookup"><span data-stu-id="7cef4-146">Furthermore, the HTML tab has been removed from the bottom of the editor (but the Design and Preview tabs are still there).</span></span>

<span data-ttu-id="7cef4-147">**リスト 2-アプリ\_Code/customeditorcs**</span><span class="sxs-lookup"><span data-stu-id="7cef4-147">**Listing 2 - App\_Code\CustomEditor.cs**</span></span>

[!code-csharp[Main](how-do-i-use-the-html-editor-control-cs/samples/sample2.cs)]

<span data-ttu-id="7cef4-148">クラスが自動的にコンパイルされるように、リスト2のクラスをアプリ\_コードフォルダーに追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7cef4-148">You must add the class in Listing 2 to your App\_Code folder so that the class will be compiled automatically.</span></span> <span data-ttu-id="7cef4-149">アプリ\_コードフォルダーが web サイトに存在しない場合は、単にフォルダーを追加できます。</span><span class="sxs-lookup"><span data-stu-id="7cef4-149">If the App\_Code folder does not exist in your website then you can simply add the folder.</span></span>

<span data-ttu-id="7cef4-150">カスタムエディターを作成した後は、通常の HTML エディターを追加するのと同じ方法で、ASP.NET ページに追加できます (リスト3を参照)。</span><span class="sxs-lookup"><span data-stu-id="7cef4-150">After you create a custom editor, you can add it to an ASP.NET page in the same way as you add the normal HTML Editor (see Listing 3).</span></span>

<span data-ttu-id="7cef4-151">**リスト 3-ShowCustomEditor .aspx**</span><span class="sxs-lookup"><span data-stu-id="7cef4-151">**Listing 3 - ShowCustomEditor.aspx**</span></span>

[!code-aspx[Main](how-do-i-use-the-html-editor-control-cs/samples/sample3.aspx)]

## <a name="avoiding-cross-site-scripting-xss-attacks"></a><span data-ttu-id="7cef4-152">クロスサイトスクリプティング (XSS) 攻撃の回避</span><span class="sxs-lookup"><span data-stu-id="7cef4-152">Avoiding Cross-Site Scripting (XSS) Attacks</span></span>

<span data-ttu-id="7cef4-153">ユーザーからの入力を受け入れ、web サイトでその入力を再表示すると、web サイトがクロスサイトスクリプティング (XSS) 攻撃につながる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="7cef4-153">Whenever you accept input from a user, and redisplay that input on your website, you potentially open your website to Cross-Site Scripting (XSS) Attacks.</span></span> <span data-ttu-id="7cef4-154">理論的には、悪意のあるハッカーが、入力が再提示されたときに実行される JavaScript コードを送信する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="7cef4-154">In theory, a malicious hacker could submit JavaScript code that gets executed when the input is redisplayed.</span></span> <span data-ttu-id="7cef4-155">JavaScript を使用すると、ユーザーのパスワードやその他の機密情報を盗むことができます。</span><span class="sxs-lookup"><span data-stu-id="7cef4-155">The JavaScript could be used to steal user passwords or other sensitive information.</span></span>

<span data-ttu-id="7cef4-156">通常、web ページに表示する前に、ユーザーから取得した入力を HTML エンコードすることによって、XSS 攻撃を防ぐことができます。</span><span class="sxs-lookup"><span data-stu-id="7cef4-156">Normally, you can defeat XSS attacks by HTML encoding whatever input you retrieve from a user before displaying it in a web page.</span></span> <span data-ttu-id="7cef4-157">ただし、html エディターの出力を html エンコードすると、スクリプト&gt; のタグ &lt;エンコードされるだけでなく、すべての HTML タグもエンコードされます。</span><span class="sxs-lookup"><span data-stu-id="7cef4-157">However, HTML encoding the output of the HTML Editor would not only encode &lt;script&gt; tags, it would also encode all HTML tags.</span></span> <span data-ttu-id="7cef4-158">つまり、フォントの種類、フォントサイズ、背景色など、すべての書式設定が失われる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="7cef4-158">In other words, you would lose all of the formatting such as the font type, font size, and background color.</span></span>

<span data-ttu-id="7cef4-159">パスワード、クレジットカード番号、社会保障番号など、ユーザーから機密情報を収集する場合は、HTML エディターを使用してユーザーから取得したエンコードされていないコンテンツを表示しないようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="7cef4-159">If you are collecting sensitive information from your users -- such as passwords, credit-card numbers, and social security numbers - then you should not display un-encoded content that you retrieve from a user with the HTML Editor.</span></span> <span data-ttu-id="7cef4-160">Html エディターは、html コンテンツを再表示しない場合、または HTML コンテンツが信頼できるパーティによって web サイトに送信されている場合にのみ使用してください。</span><span class="sxs-lookup"><span data-stu-id="7cef4-160">You should use the HTML Editor only in situations in which you are not redisplaying the HTML content, or the HTML content is being submitted to your website by a trusted party.</span></span>

<span data-ttu-id="7cef4-161">たとえば、ブログアプリケーションを作成する場合を考えてみましょう。</span><span class="sxs-lookup"><span data-stu-id="7cef4-161">Imagine, for example, that you are creating a blog application.</span></span> <span data-ttu-id="7cef4-162">このような状況では、ブログの投稿を作成するときに HTML エディターを使用するのが理にかなっています。</span><span class="sxs-lookup"><span data-stu-id="7cef4-162">In this situation, it makes sense to use the HTML Editor when composing blog posts.</span></span> <span data-ttu-id="7cef4-163">ブログ投稿を送信するのは自分だけで、おそらく悪意のある JavaScript を送信することはできません。</span><span class="sxs-lookup"><span data-stu-id="7cef4-163">You are the only one who submits a blog post and, presumably, you can trust yourself not to submit malicious JavaScript.</span></span> <span data-ttu-id="7cef4-164">ただし、匿名ユーザーにコメントの投稿を許可する場合、HTML エディターを使用することは意味がありません。</span><span class="sxs-lookup"><span data-stu-id="7cef4-164">However, it does not make sense to use the HTML Editor when allowing anonymous users to post comments.</span></span> <span data-ttu-id="7cef4-165">パスワードなどの機密情報をユーザーが送信する状況に特に注意する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7cef4-165">You should be especially careful in situations in which users submit sensitive information such as passwords.</span></span> <span data-ttu-id="7cef4-166">悪意のあるユーザーが、パスワードを盗むための適切な JavaScript を含むコメントを投稿する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="7cef4-166">Potentially, a malicious user could post a comment that contains the right JavaScript for stealing a password.</span></span>

## <a name="summary"></a><span data-ttu-id="7cef4-167">まとめ</span><span class="sxs-lookup"><span data-stu-id="7cef4-167">Summary</span></span>

<span data-ttu-id="7cef4-168">このチュートリアルでは、AJAX Control Toolkit に含まれている HTML エディターコントロールの概要を簡単に説明しました。</span><span class="sxs-lookup"><span data-stu-id="7cef4-168">In this tutorial, you were provided with a brief overview of the HTML Editor control included in the AJAX Control Toolkit.</span></span> <span data-ttu-id="7cef4-169">HTML エディターを使用して、ユーザーからのリッチコンテンツを受け入れ、コンテンツをサーバーに送信する方法を学習しました。</span><span class="sxs-lookup"><span data-stu-id="7cef4-169">You learned how to use the HTML Editor to accept rich content from a user and submit the content to the server.</span></span> <span data-ttu-id="7cef4-170">また、HTML エディターによって表示されるツールバーボタンをカスタマイズする方法についても説明しました。</span><span class="sxs-lookup"><span data-stu-id="7cef4-170">We also discussed how you can customize the toolbar buttons that are displayed by the HTML Editor.</span></span> <span data-ttu-id="7cef4-171">最後に、HTML エディターを使用して悪意のある入力を受け入れるときのクロスサイトスクリプト攻撃を回避する方法を学習しました。</span><span class="sxs-lookup"><span data-stu-id="7cef4-171">Finally, you learned how to avoid Cross-Site Scripting Attacks when using the HTML Editor to accept potentially malicious input.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="7cef4-172">Next</span><span class="sxs-lookup"><span data-stu-id="7cef4-172">Next</span></span>](how-do-i-use-the-html-editor-control-vb.md)
