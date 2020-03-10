---
uid: web-pages/overview/testing-and-debugging/introduction-to-debugging
title: ASP.NET Web ページ (Razor) サイトのデバッグの概要 |Microsoft Docs
author: Rick-Anderson
description: デバッグは、コードページ内のエラーを検出して修正するプロセスです。 この章では、デバッグと率のために使用できるツールと手法について説明します。
ms.author: riande
ms.date: 02/20/2014
ms.assetid: 68de4326-7611-4b9b-b5f6-79b7adc3069f
msc.legacyurl: /web-pages/overview/testing-and-debugging/introduction-to-debugging
msc.type: authoredcontent
ms.openlocfilehash: ae7d871e56326610c043dc20fe6e0919e1b4ac89
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78506458"
---
# <a name="introduction-to-debugging-aspnet-web-pages-razor-sites"></a><span data-ttu-id="883ce-104">デバッグ ASP.NET Web ページ (Razor) サイトの概要</span><span class="sxs-lookup"><span data-stu-id="883ce-104">Introduction to Debugging ASP.NET Web Pages (Razor) Sites</span></span>

<span data-ttu-id="883ce-105">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="883ce-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="883ce-106">この記事では、ASP.NET Web ページ (Razor) web サイトでページをデバッグするさまざまな方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="883ce-106">This article explains various ways to debug pages in an ASP.NET Web Pages (Razor) website.</span></span> <span data-ttu-id="883ce-107">デバッグは、コードページ内のエラーを検出して修正するプロセスです。</span><span class="sxs-lookup"><span data-stu-id="883ce-107">Debugging is the process of finding and fixing errors in your code pages.</span></span>
>
> <span data-ttu-id="883ce-108">**学習内容:**</span><span class="sxs-lookup"><span data-stu-id="883ce-108">**What you'll learn:**</span></span>
>
> - <span data-ttu-id="883ce-109">ページの分析とデバッグに役立つ情報を表示する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="883ce-109">How to display information that helps analyze and debug pages.</span></span>
> - <span data-ttu-id="883ce-110">Visual Studio でデバッグツールを使用する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="883ce-110">How to use debugging tools in Visual Studio.</span></span>
>
>
> <span data-ttu-id="883ce-111">この記事で導入された ASP.NET 機能を次に示します。</span><span class="sxs-lookup"><span data-stu-id="883ce-111">These are the ASP.NET features introduced in the article:</span></span>
>
> - <span data-ttu-id="883ce-112">`ServerInfo` ヘルパー。</span><span class="sxs-lookup"><span data-stu-id="883ce-112">The `ServerInfo` helper.</span></span>
> - <span data-ttu-id="883ce-113">`ObjectInfo` ヘルパー。</span><span class="sxs-lookup"><span data-stu-id="883ce-113">`ObjectInfo` helper.</span></span>
>
>
> ## <a name="software-versions"></a><span data-ttu-id="883ce-114">ソフトウェアのバージョン</span><span class="sxs-lookup"><span data-stu-id="883ce-114">Software versions</span></span>
>
>
> - <span data-ttu-id="883ce-115">ASP.NET Web ページ (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="883ce-115">ASP.NET Web Pages (Razor) 3</span></span>
> - <span data-ttu-id="883ce-116">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="883ce-116">Visual Studio 2013</span></span>
>
>
> <span data-ttu-id="883ce-117">このチュートリアルは ASP.NET Web ページ2でも動作します。</span><span class="sxs-lookup"><span data-stu-id="883ce-117">This tutorial also works with ASP.NET Web Pages 2.</span></span> <span data-ttu-id="883ce-118">WebMatrix 3 を使用することはできますが、統合デバッガーはサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="883ce-118">You can use WebMatrix 3 but the integrated debugger is not supported.</span></span>

<span data-ttu-id="883ce-119">コードのエラーや問題をトラブルシューティングするための重要な側面は、これらの問題を最初に回避することです。</span><span class="sxs-lookup"><span data-stu-id="883ce-119">An important aspect of troubleshooting errors and problems in your code is to avoid them in the first place.</span></span> <span data-ttu-id="883ce-120">これを行うには、エラーの原因となる可能性があるコードのセクションを `try/catch` ブロックに配置します。</span><span class="sxs-lookup"><span data-stu-id="883ce-120">You can do that by putting sections of your code that are likely to cause errors into `try/catch` blocks.</span></span> <span data-ttu-id="883ce-121">詳細については、「 [Razor 構文を使用した ASP.NET Web プログラミングの概要](https://go.microsoft.com/fwlink/?LinkId=202890)」のエラー処理に関するセクションを参照してください。</span><span class="sxs-lookup"><span data-stu-id="883ce-121">For more information, see the section on handling errors in [Introduction to ASP.NET Web Programming Using the Razor Syntax](https://go.microsoft.com/fwlink/?LinkId=202890).</span></span>

<span data-ttu-id="883ce-122">`ServerInfo` helper は、ページをホストする web サーバー環境に関する情報の概要を提供する診断ツールです。</span><span class="sxs-lookup"><span data-stu-id="883ce-122">The `ServerInfo` helper is a diagnostic tool that gives you an overview of information about the web server environment that hosts your page.</span></span> <span data-ttu-id="883ce-123">また、ブラウザーがページを要求したときに送信される HTTP 要求情報も表示されます。</span><span class="sxs-lookup"><span data-stu-id="883ce-123">It also shows you HTTP request information that's sent when a browser requests the page.</span></span> <span data-ttu-id="883ce-124">`ServerInfo` ヘルパーには、現在のユーザー id、要求を行ったブラウザーの種類などが表示されます。</span><span class="sxs-lookup"><span data-stu-id="883ce-124">The `ServerInfo` helper displays the current user identity, the type of browser that made the request, and so on.</span></span> <span data-ttu-id="883ce-125">この種の情報は、一般的な問題のトラブルシューティングに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="883ce-125">This kind of information can help you troubleshoot common issues.</span></span>

1. <span data-ttu-id="883ce-126">*Serverinfo. cshtml*という名前の新しい web ページを作成します。</span><span class="sxs-lookup"><span data-stu-id="883ce-126">Create a new web page named *ServerInfo.cshtml*.</span></span>
2. <span data-ttu-id="883ce-127">ページの最後で、終了 `</body>` タグの直前に `@ServerInfo.GetHtml()`を追加します。</span><span class="sxs-lookup"><span data-stu-id="883ce-127">At the end of the page, just before the closing `</body>` tag, add `@ServerInfo.GetHtml()`:</span></span>

    [!code-cshtml[Main](introduction-to-debugging/samples/sample1.cshtml)]

    <span data-ttu-id="883ce-128">`ServerInfo` コードは、ページの任意の場所に追加できます。</span><span class="sxs-lookup"><span data-stu-id="883ce-128">You can add the `ServerInfo` code anywhere in the page.</span></span> <span data-ttu-id="883ce-129">ただし、末尾に追加すると、他のページコンテンツとは別に出力が保持されるため、読みやすくなります。</span><span class="sxs-lookup"><span data-stu-id="883ce-129">But adding it at the end will keep its output separate from your other page content, which makes it easier to read.</span></span>

    > [!NOTE]
    >
    > <span data-ttu-id="883ce-130">**重要**Web ページを実稼働サーバーに移動する前に、web ページから診断コードを削除する必要があります。</span><span class="sxs-lookup"><span data-stu-id="883ce-130">**Important** You should remove any diagnostic code from your web pages before you move web pages to a production server.</span></span> <span data-ttu-id="883ce-131">これは、`ServerInfo` ヘルパーに適用されます。また、この記事では、ページへのコードの追加を含むその他の診断手法にも当てはまります。</span><span class="sxs-lookup"><span data-stu-id="883ce-131">This applies to the `ServerInfo` helper as well as the other diagnostic techniques in this article that involve adding code to a page.</span></span> <span data-ttu-id="883ce-132">この種の情報が悪意のあるユーザーにとって役立つ可能性があるため、web サイトの訪問者にサーバー名、ユーザー名、サーバー上のパスなどの情報が表示されないようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="883ce-132">You don't want your website visitors to see information about your server name, user names, paths on your server, and similar details, because this type of information might be useful to people with malicious intent.</span></span>
3. <span data-ttu-id="883ce-133">ページを保存し、ブラウザーで実行します。</span><span class="sxs-lookup"><span data-stu-id="883ce-133">Save the page and run it in a browser.</span></span>

    ![デバッグ-1](introduction-to-debugging/_static/image1.jpg)

    <span data-ttu-id="883ce-135">`ServerInfo` ヘルパーは、次の4つのテーブルの情報をページに表示します。</span><span class="sxs-lookup"><span data-stu-id="883ce-135">The `ServerInfo` helper displays four tables of information in the page:</span></span>

   - <span data-ttu-id="883ce-136">サーバーの構成。</span><span class="sxs-lookup"><span data-stu-id="883ce-136">Server Configuration.</span></span> <span data-ttu-id="883ce-137">このセクションでは、ホストしている web サーバーに関する情報を提供します。これには、コンピューター名、実行している ASP.NET のバージョン、ドメイン名、サーバー時間などが含まれます。</span><span class="sxs-lookup"><span data-stu-id="883ce-137">This section provides information about the hosting web server, including computer name, the version of ASP.NET you're running, the domain name, and server time.</span></span>
   - <span data-ttu-id="883ce-138">ASP.NET サーバー変数。</span><span class="sxs-lookup"><span data-stu-id="883ce-138">ASP.NET Server Variables.</span></span> <span data-ttu-id="883ce-139">このセクションでは、多くの HTTP プロトコルの詳細 (HTTP 変数と呼ばれます) と、各 web ページ要求に含まれる値について詳しく説明します。</span><span class="sxs-lookup"><span data-stu-id="883ce-139">This section provides details about the many HTTP protocol details (called HTTP variables) and values that are part of each web page request.</span></span>
   - <span data-ttu-id="883ce-140">HTTP ランタイム情報。</span><span class="sxs-lookup"><span data-stu-id="883ce-140">HTTP Runtime Information.</span></span> <span data-ttu-id="883ce-141">このセクションでは、web ページが実行されている Microsoft .NET Framework のバージョン、パス、キャッシュに関する詳細などについて詳しく説明します。</span><span class="sxs-lookup"><span data-stu-id="883ce-141">This section provides details about that the version of the Microsoft .NET Framework that your web page is running under, the path, details about the cache, and so on.</span></span> <span data-ttu-id="883ce-142">( [Razor 構文を使用した ASP.NET Web プログラミングの概要につい](https://go.microsoft.com/fwlink/?LinkId=202890)て学習したように、Razor 構文を使用する ASP.NET Web ページは、Microsoft の ASP.NET Web サーバーテクノロジを基盤としています。これは、.NET Framework と呼ばれる広範なソフトウェア開発ライブラリに基づいて構築されています)。</span><span class="sxs-lookup"><span data-stu-id="883ce-142">(As you learned in [Introduction to ASP.NET Web Programming Using the Razor Syntax](https://go.microsoft.com/fwlink/?LinkId=202890), ASP.NET Web Pages using the Razor syntax are built on Microsoft's ASP.NET web server technology, which is itself built on an extensive software development library called the .NET Framework.)</span></span>
   - <span data-ttu-id="883ce-143">環境変数。</span><span class="sxs-lookup"><span data-stu-id="883ce-143">Environment Variables.</span></span> <span data-ttu-id="883ce-144">このセクションでは、web サーバー上のすべてのローカル環境変数とその値の一覧を示します。</span><span class="sxs-lookup"><span data-stu-id="883ce-144">This section provides a list of all the local environment variables and their values on the web server.</span></span>

     <span data-ttu-id="883ce-145">すべてのサーバーと要求情報の詳細については、この記事では説明しませんが、`ServerInfo` ヘルパーが多くの診断情報を返すことを確認できます。</span><span class="sxs-lookup"><span data-stu-id="883ce-145">A full description of all the server and request information is beyond the scope of this article, but you can see that the `ServerInfo` helper returns a lot of diagnostic information.</span></span> <span data-ttu-id="883ce-146">`ServerInfo` 返される値の詳細については、MSDN web サイトの Microsoft TechNet web サイトおよび[IIS サーバー変数](https://msdn.microsoft.com/library/ms524602(VS.90).aspx)の「認識された[環境変数](https://technet.microsoft.com/library/dd560744(WS.10).aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="883ce-146">For more information about the values that `ServerInfo` returns, see [Recognized Environment Variables](https://technet.microsoft.com/library/dd560744(WS.10).aspx) on the Microsoft TechNet website and [IIS Server Variables](https://msdn.microsoft.com/library/ms524602(VS.90).aspx) on the MSDN website.</span></span>

## <a name="embedding-output-expressions-to-display-page-values"></a><span data-ttu-id="883ce-147">ページ値を表示するための出力式の埋め込み</span><span class="sxs-lookup"><span data-stu-id="883ce-147">Embedding Output Expressions to Display Page Values</span></span>

<span data-ttu-id="883ce-148">コード内で何が起こっているかを確認するもう1つの方法は、出力式をページに埋め込むことです。</span><span class="sxs-lookup"><span data-stu-id="883ce-148">Another way to see what's happening in your code is to embed output expressions in the page.</span></span> <span data-ttu-id="883ce-149">ご存じのように、`@myVariable` や `@(subTotal * 12)` などの値をページに追加して、変数の値を直接出力できます。</span><span class="sxs-lookup"><span data-stu-id="883ce-149">As you know, you can directly output the value of a variable by adding something like `@myVariable` or `@(subTotal * 12)` to the page.</span></span> <span data-ttu-id="883ce-150">デバッグ用には、コード内の戦略的なポイントでこれらの出力式を配置できます。</span><span class="sxs-lookup"><span data-stu-id="883ce-150">For debugging, you can place these output expressions at strategic points in your code.</span></span> <span data-ttu-id="883ce-151">これにより、ページの実行時に、キー変数の値または計算結果を確認できます。</span><span class="sxs-lookup"><span data-stu-id="883ce-151">This enables you to see the value of key variables or the result of calculations when your page runs.</span></span> <span data-ttu-id="883ce-152">デバッグが完了したら、式を削除するか、コメントアウトすることができます。この手順は、ページのデバッグを支援するために、埋め込み式を使用する一般的な方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="883ce-152">When you're done debugging, you can remove the expressions or comment them out. This procedure illustrates a typical way to use embedded expressions to help debug a page.</span></span>

1. <span data-ttu-id="883ce-153">*Outputexpression. cshtml*という名前の新しい WebMatrix ページを作成します。</span><span class="sxs-lookup"><span data-stu-id="883ce-153">Create a new WebMatrix page that's named *OutputExpression.cshtml*.</span></span>
2. <span data-ttu-id="883ce-154">ページの内容を次の内容に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="883ce-154">Replace the page content with the following:</span></span>

    [!code-html[Main](introduction-to-debugging/samples/sample2.html)]

    <span data-ttu-id="883ce-155">この例では、`switch` ステートメントを使用して `weekday` 変数の値を確認し、その曜日に応じて別の出力メッセージを表示します。</span><span class="sxs-lookup"><span data-stu-id="883ce-155">The example uses a `switch` statement to check the value of the `weekday` variable and then display a different output message depending on which day of the week it is.</span></span> <span data-ttu-id="883ce-156">この例では、最初のコードブロック内の `if` ブロックは、現在の曜日の値に1日を加算することによって、曜日を任意に変更します。</span><span class="sxs-lookup"><span data-stu-id="883ce-156">In the example, the `if` block within the first code block arbitrarily changes the day of the week by adding one day to the current weekday value.</span></span> <span data-ttu-id="883ce-157">これは、図を示すために導入されたエラーです。</span><span class="sxs-lookup"><span data-stu-id="883ce-157">This is an error introduced for illustration purposes.</span></span>
3. <span data-ttu-id="883ce-158">ページを保存し、ブラウザーで実行します。</span><span class="sxs-lookup"><span data-stu-id="883ce-158">Save the page and run it in a browser.</span></span>

    <span data-ttu-id="883ce-159">このページには、曜日が正しくないことを示したメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="883ce-159">The page displays the message for the wrong day of the week.</span></span> <span data-ttu-id="883ce-160">曜日にかかわらず、1日後にメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="883ce-160">Whatever day of the week it actually is, you'll see the message for one day later.</span></span> <span data-ttu-id="883ce-161">この例では、メッセージが無効になっている理由 (コードが意図的に誤った日付値を設定しているため) がわかっていますが、実際には、コード内のどこが間違っているかを把握するのが難しい場合があります。</span><span class="sxs-lookup"><span data-stu-id="883ce-161">Although in this case you know why the message is off (because the code deliberately sets the incorrect day value), in reality it's often hard to know where things are going wrong in the code.</span></span> <span data-ttu-id="883ce-162">デバッグするには、`weekday`などの主要なオブジェクトと変数の値に何が起こっているかを調べる必要があります。</span><span class="sxs-lookup"><span data-stu-id="883ce-162">To debug, you need to find out what's happening to the value of key objects and variables such as `weekday`.</span></span>
4. <span data-ttu-id="883ce-163">コード内のコメントに示されている2つの場所に示されているように `@weekday` を挿入して、出力式を追加します。</span><span class="sxs-lookup"><span data-stu-id="883ce-163">Add output expressions by inserting `@weekday` as shown in the two places indicated by comments in the code.</span></span> <span data-ttu-id="883ce-164">これらの出力式では、コード実行のその時点の変数の値が表示されます。</span><span class="sxs-lookup"><span data-stu-id="883ce-164">These output expressions will display the values of the variable at that point in the code execution.</span></span>

    [!code-csharp[Main](introduction-to-debugging/samples/sample3.cs?highlight=2-3,15-16)]
5. <span data-ttu-id="883ce-165">ブラウザーでページを保存して実行します。</span><span class="sxs-lookup"><span data-stu-id="883ce-165">Save and run the page in a browser.</span></span>

    <span data-ttu-id="883ce-166">このページには、最初に週の実際の曜日、次に1日後に更新された曜日が表示されます。その後、`switch` ステートメントから結果として得られるメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="883ce-166">The page displays the real day of the week first, then the updated day of the week that results from adding one day, and then the resulting message from the `switch` statement.</span></span> <span data-ttu-id="883ce-167">HTML `<p>` タグを出力に追加していないため、2つの変数式 (`@weekday`) からの出力には、その日の間にスペースがありません。式はテスト専用です。</span><span class="sxs-lookup"><span data-stu-id="883ce-167">The output from the two variable expressions (`@weekday`) has no spaces between the days because you didn't add any HTML `<p>` tags to the output; the expressions are just for testing.</span></span>

    ![デバッグ-2](introduction-to-debugging/_static/image2.jpg)

    <span data-ttu-id="883ce-169">ここで、エラーの場所を確認できます。</span><span class="sxs-lookup"><span data-stu-id="883ce-169">Now you can see where the error is.</span></span> <span data-ttu-id="883ce-170">コードに最初に `weekday` 変数を表示すると、正しい日が表示されます。</span><span class="sxs-lookup"><span data-stu-id="883ce-170">When you first display the `weekday` variable in the code, it shows the correct day.</span></span> <span data-ttu-id="883ce-171">2回目に表示すると、コードの `if` ブロックの後に、その日が1つずつオフになります。</span><span class="sxs-lookup"><span data-stu-id="883ce-171">When you display it the second time, after the `if` block in the code, the day is off by one.</span></span> <span data-ttu-id="883ce-172">これは、weekday 変数の1番目と2番目の外観の間に何らかの問題が発生したことを把握しています。</span><span class="sxs-lookup"><span data-stu-id="883ce-172">So you know that something has happened between the first and second appearance of the weekday variable.</span></span> <span data-ttu-id="883ce-173">これが実際のバグである場合、この種のアプローチは、問題の原因となっているコードの場所を絞り込むのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="883ce-173">If this were a real bug, this kind of approach would help you narrow down the location of the code that's causing the problem.</span></span>
6. <span data-ttu-id="883ce-174">追加した2つの出力式を削除し、曜日を変更するコードを削除して、ページ内のコードを修正します。</span><span class="sxs-lookup"><span data-stu-id="883ce-174">Fix the code in the page by removing the two output expressions you added, and removing the code that changes the day of the week.</span></span> <span data-ttu-id="883ce-175">コードの残りの完全なブロックは、次の例のようになります。</span><span class="sxs-lookup"><span data-stu-id="883ce-175">The remaining, complete block of code looks like the following example:</span></span>

    [!code-cshtml[Main](introduction-to-debugging/samples/sample4.cshtml)]
7. <span data-ttu-id="883ce-176">ブラウザーでページを実行します。</span><span class="sxs-lookup"><span data-stu-id="883ce-176">Run the page in a browser.</span></span> <span data-ttu-id="883ce-177">今回は、実際の曜日に対して正しいメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="883ce-177">This time you see the correct message displayed for the actual day of the week.</span></span>

## <a name="using-the-objectinfo-helper-to-display-object-values"></a><span data-ttu-id="883ce-178">ObjectInfo ヘルパーを使用したオブジェクト値の表示</span><span class="sxs-lookup"><span data-stu-id="883ce-178">Using the ObjectInfo Helper to Display Object Values</span></span>

<span data-ttu-id="883ce-179">`ObjectInfo` ヘルパーには、渡された各オブジェクトの型と値が表示されます。</span><span class="sxs-lookup"><span data-stu-id="883ce-179">The `ObjectInfo` helper displays the type and the value of each object you pass to it.</span></span> <span data-ttu-id="883ce-180">これを使用すると、前の例の出力式の場合と同様に、コード内の変数とオブジェクトの値を表示できます。さらに、オブジェクトに関するデータ型情報を確認することもできます。</span><span class="sxs-lookup"><span data-stu-id="883ce-180">You can use it to view the value of variables and objects in your code (like you did with output expressions in the previous example), plus you can see data type information about the object.</span></span>

1. <span data-ttu-id="883ce-181">先ほど作成した*Outputexpression. cshtml*という名前のファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="883ce-181">Open the file named *OutputExpression.cshtml* that you created earlier.</span></span>
2. <span data-ttu-id="883ce-182">ページ内のすべてのコードを次のコードブロックに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="883ce-182">Replace all code in the page with the following block of code:</span></span>

    [!code-html[Main](introduction-to-debugging/samples/sample5.html)]
3. <span data-ttu-id="883ce-183">ブラウザーでページを保存して実行します。</span><span class="sxs-lookup"><span data-stu-id="883ce-183">Save and run the page in a browser.</span></span>

    ![デバッグ-4](introduction-to-debugging/_static/image3.jpg)

    <span data-ttu-id="883ce-185">この例では、`ObjectInfo` ヘルパーは次の2つの項目を表示します。</span><span class="sxs-lookup"><span data-stu-id="883ce-185">In this example, the `ObjectInfo` helper displays two items:</span></span>

   - <span data-ttu-id="883ce-186">型。</span><span class="sxs-lookup"><span data-stu-id="883ce-186">The type.</span></span> <span data-ttu-id="883ce-187">最初の変数の場合、型は `DayOfWeek`になります。</span><span class="sxs-lookup"><span data-stu-id="883ce-187">For the first variable, the type is `DayOfWeek`.</span></span> <span data-ttu-id="883ce-188">2番目の変数の場合、型は `String`になります。</span><span class="sxs-lookup"><span data-stu-id="883ce-188">For the second variable, the type is `String`.</span></span>
   - <span data-ttu-id="883ce-189">値。</span><span class="sxs-lookup"><span data-stu-id="883ce-189">The value.</span></span> <span data-ttu-id="883ce-190">この場合、ページにあいさつ変数の値が既に表示されているので、変数を `ObjectInfo`に渡すと、値が再び表示されます。</span><span class="sxs-lookup"><span data-stu-id="883ce-190">In this case, because you already display the value of the greeting variable in the page, the value is displayed again when you pass the variable to `ObjectInfo`.</span></span>

     <span data-ttu-id="883ce-191">より複雑なオブジェクトの場合、`ObjectInfo` ヘルパーは、基本的&#8212;により多くの情報を表示できます。また、オブジェクトのすべてのプロパティの型と値を表示できます。</span><span class="sxs-lookup"><span data-stu-id="883ce-191">For more complex objects, the `ObjectInfo` helper can display more information &#8212; basically, it can display the types and values of all of an object's properties.</span></span>

## <a name="using-debugging-tools-in-visual-studio"></a><span data-ttu-id="883ce-192">Visual Studio でのデバッグツールの使用</span><span class="sxs-lookup"><span data-stu-id="883ce-192">Using Debugging Tools in Visual Studio</span></span>

<span data-ttu-id="883ce-193">より包括的なデバッグエクスペリエンスを実現するには、 [Visual Studio](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)を使用します。</span><span class="sxs-lookup"><span data-stu-id="883ce-193">For a more comprehensive debugging experience, use [Visual Studio](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017).</span></span> <span data-ttu-id="883ce-194">Visual Studio では、検査する行のコードにブレークポイントを設定できます。</span><span class="sxs-lookup"><span data-stu-id="883ce-194">With Visual Studio, you can set a breakpoint in your code at the line that you want to inspect.</span></span>

![ブレークポイントの設定](introduction-to-debugging/_static/image1.png)

<span data-ttu-id="883ce-196">Web サイトをテストすると、実行中のコードがブレークポイントで停止します。</span><span class="sxs-lookup"><span data-stu-id="883ce-196">When you test the web site, the executing code halts at the breakpoint.</span></span>

![リーチブレークポイント](introduction-to-debugging/_static/image2.png)

<span data-ttu-id="883ce-198">変数の現在の値を確認し、コードを1行ずつステップ実行することができます。</span><span class="sxs-lookup"><span data-stu-id="883ce-198">You can examine the current values of the variables, and step through the code line-by-line.</span></span>

![値の表示](introduction-to-debugging/_static/image3.png)

<span data-ttu-id="883ce-200">Visual Studio で統合デバッガーを使用して ASP.NET Razor ページをデバッグする方法の詳細については、「 [Visual Studio を使用したプログラミング ASP.NET Web ページ (Razor)](https://go.microsoft.com/fwlink/?LinkId=205854)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="883ce-200">For information about using the integrated debugger in Visual Studio to debug ASP.NET Razor pages, see [Programming ASP.NET Web Pages (Razor) Using Visual Studio](https://go.microsoft.com/fwlink/?LinkId=205854).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="883ce-201">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="883ce-201">Additional Resources</span></span>

- [<span data-ttu-id="883ce-202">Visual Studio を使用したプログラミング ASP.NET Web ページ (Razor)</span><span class="sxs-lookup"><span data-stu-id="883ce-202">Programming ASP.NET Web Pages (Razor) Using Visual Studio</span></span>](https://go.microsoft.com/fwlink/?LinkId=205854)
- <span data-ttu-id="883ce-203">[IIS サーバー変数](https://msdn.microsoft.com/library/ms524602(VS.90).aspx)(MSDN)</span><span class="sxs-lookup"><span data-stu-id="883ce-203">[IIS Server Variables](https://msdn.microsoft.com/library/ms524602(VS.90).aspx) (MSDN)</span></span>
- <span data-ttu-id="883ce-204">認識された[環境変数](https://technet.microsoft.com/library/dd560744(WS.10).aspx)(TechNet)</span><span class="sxs-lookup"><span data-stu-id="883ce-204">[Recognized Environment Variables](https://technet.microsoft.com/library/dd560744(WS.10).aspx) (TechNet)</span></span>
