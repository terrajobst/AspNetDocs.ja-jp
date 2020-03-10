---
uid: aspnet/overview/web-development-best-practices/what-not-to-do-in-aspnet-and-what-to-do-instead
title: ASP.NET では何が行われず、代わりに何をするかを説明します。Microsoft Docs
author: Rick-Anderson
description: このトピックでは、ASP.NET web プロジェクト内での複数のよくある間違いについて説明します。 ここでは、これらの処理を回避するための推奨事項について説明します。
ms.author: riande
ms.date: 01/28/2019
ms.assetid: c39b9965-545c-4b04-8f55-21be7f28a9e5
msc.legacyurl: /aspnet/overview/web-development-best-practices/what-not-to-do-in-aspnet-and-what-to-do-instead
msc.type: authoredcontent
ms.openlocfilehash: 980d3544df70643043391e6573803ce21b3a824f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78500134"
---
# <a name="what-not-to-do-in-aspnet-and-what-to-do-instead"></a><span data-ttu-id="a426e-104">ASP.NET では行わないことと、その代わりに行うこと</span><span class="sxs-lookup"><span data-stu-id="a426e-104">What not to do in ASP.NET, and what to do instead</span></span>

> <span data-ttu-id="a426e-105">このトピックでは、ASP.NET web プロジェクト内での複数のよくある間違いについて説明します。</span><span class="sxs-lookup"><span data-stu-id="a426e-105">This topic describes several common mistakes people make within ASP.NET web projects.</span></span> <span data-ttu-id="a426e-106">これらの一般的な誤りを回避するための推奨事項について説明します。</span><span class="sxs-lookup"><span data-stu-id="a426e-106">It provides recommendations for what you should do to avoid these common mistakes.</span></span> <span data-ttu-id="a426e-107">これは、ノルウェーの開発者のカンファレンスで**Damian Edwards**による[プレゼンテーション](http://vimeo.com/68390507)に基づいています。</span><span class="sxs-lookup"><span data-stu-id="a426e-107">It is based on a [presentation](http://vimeo.com/68390507) by **Damian Edwards** at Norwegian Developers Conference.</span></span>

## <a name="disclaimer"></a><span data-ttu-id="a426e-108">免責事項</span><span class="sxs-lookup"><span data-stu-id="a426e-108">Disclaimer</span></span>

<span data-ttu-id="a426e-109">このトピックは、アプリケーションの安全性と効率性を確保するための完全なガイドではありません。</span><span class="sxs-lookup"><span data-stu-id="a426e-109">This topic is not intended as a complete guide to ensure your application is secure and efficient.</span></span> <span data-ttu-id="a426e-110">このトピックでは説明されていないセキュリティとパフォーマンスについては、ベストプラクティスに従う必要があります。</span><span class="sxs-lookup"><span data-stu-id="a426e-110">You still need to follow best practices for security and performance that are not outlined in this topic.</span></span> <span data-ttu-id="a426e-111">.NET のクラスとプロセスに関連する一般的な間違いを回避する方法についてのみ説明します。</span><span class="sxs-lookup"><span data-stu-id="a426e-111">It only suggests how to avoid common mistakes related to .NET classes and processes.</span></span>

## <a name="overview"></a><span data-ttu-id="a426e-112">概要</span><span class="sxs-lookup"><span data-stu-id="a426e-112">Overview</span></span>

<span data-ttu-id="a426e-113">このトピックには、次のセクションが含まれます。</span><span class="sxs-lookup"><span data-stu-id="a426e-113">This topic contains the following sections:</span></span>

- [<span data-ttu-id="a426e-114">標準への準拠</span><span class="sxs-lookup"><span data-stu-id="a426e-114">Standards Compliance</span></span>](#standards)

    - [<span data-ttu-id="a426e-115">コントロールアダプター</span><span class="sxs-lookup"><span data-stu-id="a426e-115">Control Adapters</span></span>](#adapters)
    - [<span data-ttu-id="a426e-116">コントロールのスタイルプロパティ</span><span class="sxs-lookup"><span data-stu-id="a426e-116">Style Properties on Controls</span></span>](#styleprop)
    - [<span data-ttu-id="a426e-117">ページとコントロールのコールバック</span><span class="sxs-lookup"><span data-stu-id="a426e-117">Page and Control Callbacks</span></span>](#callback)
    - [<span data-ttu-id="a426e-118">ブラウザー機能の検出</span><span class="sxs-lookup"><span data-stu-id="a426e-118">Browser Capability Detection</span></span>](#browsercap)
- [<span data-ttu-id="a426e-119">セキュリティ</span><span class="sxs-lookup"><span data-stu-id="a426e-119">Security</span></span>](#security)

    - [<span data-ttu-id="a426e-120">要求の検証</span><span class="sxs-lookup"><span data-stu-id="a426e-120">Request Validation</span></span>](#validation)
    - [<span data-ttu-id="a426e-121">Cookie なしのフォーム認証とセッション</span><span class="sxs-lookup"><span data-stu-id="a426e-121">Cookieless Forms Authentication and Session</span></span>](#cookieless)
    - [<span data-ttu-id="a426e-122">EnableViewStateMac</span><span class="sxs-lookup"><span data-stu-id="a426e-122">EnableViewStateMac</span></span>](#viewstatemac)
    - [<span data-ttu-id="a426e-123">中程度の信頼</span><span class="sxs-lookup"><span data-stu-id="a426e-123">Medium Trust</span></span>](#medium)
    - [<span data-ttu-id="a426e-124">appSettings&gt; の &lt;</span><span class="sxs-lookup"><span data-stu-id="a426e-124">&lt;appSettings&gt;</span></span>](#appsettings)
    - [<span data-ttu-id="a426e-125">UrlPathEncode</span><span class="sxs-lookup"><span data-stu-id="a426e-125">UrlPathEncode</span></span>](#urlpathencode)
- [<span data-ttu-id="a426e-126">信頼性とパフォーマンス</span><span class="sxs-lookup"><span data-stu-id="a426e-126">Reliability and Performance</span></span>](#performance)

    - [<span data-ttu-id="a426e-127">PreSendRequestHeaders と PreSendRequestContent</span><span class="sxs-lookup"><span data-stu-id="a426e-127">PreSendRequestHeaders and PreSendRequestContent</span></span>](#presend)
    - [<span data-ttu-id="a426e-128">Web フォームを使用した非同期ページイベント</span><span class="sxs-lookup"><span data-stu-id="a426e-128">Asynchronous Page Events with Web Forms</span></span>](#asyncevents)
    - [<span data-ttu-id="a426e-129">起動と破棄の作業</span><span class="sxs-lookup"><span data-stu-id="a426e-129">Fire-and-Forget Work</span></span>](#fire)
    - [<span data-ttu-id="a426e-130">要求エンティティ本体</span><span class="sxs-lookup"><span data-stu-id="a426e-130">Request Entity Body</span></span>](#requestentity)
    - [<span data-ttu-id="a426e-131">応答。リダイレクトと応答終了</span><span class="sxs-lookup"><span data-stu-id="a426e-131">Response.Redirect and Response.End</span></span>](#redirect)
    - [<span data-ttu-id="a426e-132">EnableViewState と ViewStateMode</span><span class="sxs-lookup"><span data-stu-id="a426e-132">EnableViewState and ViewStateMode</span></span>](#viewstatemode)
    - [<span data-ttu-id="a426e-133">SqlMembershipProvider</span><span class="sxs-lookup"><span data-stu-id="a426e-133">SqlMembershipProvider</span></span>](#sqlprovider)
    - [<span data-ttu-id="a426e-134">実行時間の長い要求 (> 110 秒)</span><span class="sxs-lookup"><span data-stu-id="a426e-134">Long Running Requests (>110 seconds)</span></span>](#long)

<a id="standards"></a>

## <a name="standards-compliance"></a><span data-ttu-id="a426e-135">標準への準拠</span><span class="sxs-lookup"><span data-stu-id="a426e-135">Standards Compliance</span></span>

<a id="adapters"></a>

### <a name="control-adapters"></a><span data-ttu-id="a426e-136">コントロールアダプター</span><span class="sxs-lookup"><span data-stu-id="a426e-136">Control adapters</span></span>

<span data-ttu-id="a426e-137">推奨事項: アダプティブレンダリングのためにコントロールアダプターの使用を停止し、代わりに CSS メディアクエリと標準準拠の HTML を使用します。</span><span class="sxs-lookup"><span data-stu-id="a426e-137">Recommendation: Stop using control adapters for adaptive rendering, and instead use CSS media queries and standards-compliant HTML.</span></span>

<span data-ttu-id="a426e-138">.NET 2.0 では、さまざまなデバイスや環境用にカスタマイズされたプレゼンテーションコードをレンダリングするために、コントロールアダプターが導入されました。</span><span class="sxs-lookup"><span data-stu-id="a426e-138">Controls Adapters were introduced in .NET 2.0 to render presentation code that was customized for different devices and environments.</span></span> <span data-ttu-id="a426e-139">これで、このアダプティブレンダリングは CSS と HTML で実現できます。</span><span class="sxs-lookup"><span data-stu-id="a426e-139">Now, this adaptive rendering can be accomplished with CSS and HTML.</span></span> <span data-ttu-id="a426e-140">コントロールアダプターの使用を停止し、既存のアダプターを CSS と HTML に変換する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a426e-140">You should stop using Control Adapters and convert any existing adapters to CSS and HTML.</span></span>

<span data-ttu-id="a426e-141">詳細については、「[メディアクエリ](http://www.w3.org/TR/css3-mediaqueries/)」と「[方法: モバイルページを ASP.NET WEB フォーム/MVC アプリケーションに追加](../../../whitepapers/add-mobile-pages-to-your-aspnet-web-forms-mvc-application.md)する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a426e-141">For more information, see [Media Queries](http://www.w3.org/TR/css3-mediaqueries/) and [How To: Add Mobile Pages to Your ASP.NET Web Forms / MVC Application](../../../whitepapers/add-mobile-pages-to-your-aspnet-web-forms-mvc-application.md).</span></span>

<a id="styleprop"></a>

### <a name="style-properties-on-controls"></a><span data-ttu-id="a426e-142">コントロールのスタイルプロパティ</span><span class="sxs-lookup"><span data-stu-id="a426e-142">Style properties on controls</span></span>

<span data-ttu-id="a426e-143">推奨事項: コントロールマークアップでのスタイル値の設定を停止します。代わりに、CSS スタイルシートで書式設定値を設定します。</span><span class="sxs-lookup"><span data-stu-id="a426e-143">Recommendation: Stop setting style values in the control markup, and instead set formatting values in CSS stylesheets.</span></span>

<span data-ttu-id="a426e-144">Web サーバーコントロールには、インラインスタイルプロパティの設定に使用できる多数のプロパティが含まれています。</span><span class="sxs-lookup"><span data-stu-id="a426e-144">Web server controls contain dozens of properties which can be used to set in-line style properties.</span></span> <span data-ttu-id="a426e-145">たとえば、ForeColor プロパティは、コントロールのテキストの色を設定します。</span><span class="sxs-lookup"><span data-stu-id="a426e-145">For example, the ForeColor property sets the color of the text for a control.</span></span> <span data-ttu-id="a426e-146">CSS スタイルシートを使用すると、これと同じ効果をより効率的に行うことができます。</span><span class="sxs-lookup"><span data-stu-id="a426e-146">You can accomplish this same effect more efficiently through CSS stylesheets.</span></span> <span data-ttu-id="a426e-147">スタイルシートを使用すると、スタイル値を一元化し、アプリケーション全体でこれらの値を設定しないようにすることができます。</span><span class="sxs-lookup"><span data-stu-id="a426e-147">Stylesheets enable you to centralize style values and avoid setting these values throughout your application.</span></span>

<span data-ttu-id="a426e-148">次の例は、テキストを赤に設定する CSS クラスを示しています。</span><span class="sxs-lookup"><span data-stu-id="a426e-148">The following example shows a CSS class the sets text to red.</span></span>

[!code-css[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample1.css)]

<span data-ttu-id="a426e-149">次の例では、CSS クラスを動的に適用する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="a426e-149">The next example shows how to dynamically apply the CSS class.</span></span>

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample2.cs)]

<a id="callback"></a>

### <a name="page-and-control-callbacks"></a><span data-ttu-id="a426e-150">ページとコントロールのコールバック</span><span class="sxs-lookup"><span data-stu-id="a426e-150">Page and control callbacks</span></span>

<span data-ttu-id="a426e-151">推奨事項: ページとコントロールのコールバックの使用を停止し、代わりに、AJAX、UpdatePanel、MVC アクションメソッド、Web API、または SignalR のいずれかを使用します。</span><span class="sxs-lookup"><span data-stu-id="a426e-151">Recommendation: Stop using page and control callbacks, and instead use any of the following: AJAX, UpdatePanel, MVC action methods, Web API, or SignalR.</span></span>

<span data-ttu-id="a426e-152">以前のバージョンの ASP.NET では、ページとコントロールのコールバックメソッドを使用して、ページ全体を更新せずに web ページの一部を更新できました。</span><span class="sxs-lookup"><span data-stu-id="a426e-152">In earlier versions of ASP.NET, Page and Control callback methods enabled you to update part of the web page without refreshing an entire page.</span></span> <span data-ttu-id="a426e-153">[AJAX](../../../ajax/index.md)、 [UpdatePanel](https://msdn.microsoft.com/library/bb386454.aspx)、 [MVC](../../../mvc/index.md)、 [Web API](../../../web-api/index.md) 、または[SignalR](../../../signalr/index.md)を使用して部分ページ更新を実行できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="a426e-153">You can now accomplish partial-page updates through [AJAX](../../../ajax/index.md), [UpdatePanel](https://msdn.microsoft.com/library/bb386454.aspx), [MVC](../../../mvc/index.md), [Web API](../../../web-api/index.md) or [SignalR](../../../signalr/index.md).</span></span> <span data-ttu-id="a426e-154">わかりやすい Url とルーティングに関する問題が発生する可能性があるため、コールバックメソッドの使用を停止する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a426e-154">You should stop using callback methods because they can cause issues with friendly URLs and routing.</span></span> <span data-ttu-id="a426e-155">既定では、コントロールはコールバックメソッドを有効にしませんが、コントロールでこの機能を有効にした場合は、無効にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="a426e-155">By default, controls do not enable callback methods, but if you enabled this feature in a control, you should disable it.</span></span>

<a id="browsercap"></a>

### <a name="browser-capability-detection"></a><span data-ttu-id="a426e-156">ブラウザー機能の検出</span><span class="sxs-lookup"><span data-stu-id="a426e-156">Browser capability detection</span></span>

<span data-ttu-id="a426e-157">推奨: 静的なブラウザー機能の検出の使用を停止し、代わりに動的な機能の検出を使用します。</span><span class="sxs-lookup"><span data-stu-id="a426e-157">Recommendation: Stop using static browser capability detection, and instead use dynamic feature detection.</span></span>

<span data-ttu-id="a426e-158">以前のバージョンの ASP.NET では、各ブラウザーでサポートされている機能は、XML ファイルに格納されていました。</span><span class="sxs-lookup"><span data-stu-id="a426e-158">In earlier versions of ASP.NET, the supported features for each browser were stored in an XML file.</span></span> <span data-ttu-id="a426e-159">静的参照を使用した機能サポートの検出は、最適な方法ではありません。</span><span class="sxs-lookup"><span data-stu-id="a426e-159">Detecting feature support through a static lookup is not the best approach.</span></span> <span data-ttu-id="a426e-160">これで、 [Modernizr](http://modernizr.com/)などの機能検出フレームワークを使用して、ブラウザーのサポートされている機能を動的に検出できます。</span><span class="sxs-lookup"><span data-stu-id="a426e-160">Now, you can dynamically detect a browser's supported features by using a feature detection framework, such as [Modernizr](http://modernizr.com/).</span></span> <span data-ttu-id="a426e-161">機能の検出では、メソッドまたはプロパティを使用して、ブラウザーが目的の結果を生成したかどうかを確認することによって、サポートが決定されます。</span><span class="sxs-lookup"><span data-stu-id="a426e-161">Feature detection determines support by attempting to use a method or property and then checking to see if the browser produced the desired result.</span></span> <span data-ttu-id="a426e-162">既定では、Modernizr は Web アプリケーションテンプレートに含まれています。</span><span class="sxs-lookup"><span data-stu-id="a426e-162">By default, Modernizr is included in the Web application templates.</span></span>

<a id="security"></a>

## <a name="security"></a><span data-ttu-id="a426e-163">Security</span><span class="sxs-lookup"><span data-stu-id="a426e-163">Security</span></span>

<a id="validation"></a>

### <a name="request-validation"></a><span data-ttu-id="a426e-164">要求の検証</span><span class="sxs-lookup"><span data-stu-id="a426e-164">Request validation</span></span>

<span data-ttu-id="a426e-165">推奨事項: ユーザー入力を検証し、ユーザーからの出力をエンコードします。</span><span class="sxs-lookup"><span data-stu-id="a426e-165">Recommendation: Validate user input, and encode output from users.</span></span>

<span data-ttu-id="a426e-166">要求の検証は、ASP.NET の機能の1つであり、認識された脅威が見つかると、各要求を調べ、要求を停止します。</span><span class="sxs-lookup"><span data-stu-id="a426e-166">Request validation is a feature of ASP.NET that inspects each request and stops the request if a perceived threat is found.</span></span> <span data-ttu-id="a426e-167">クロスサイトスクリプティング攻撃に対してアプリケーションをセキュリティで保護するための要求の検証に依存しないでください。</span><span class="sxs-lookup"><span data-stu-id="a426e-167">Do not depend on request validation for securing your application against cross-site scripting attacks.</span></span> <span data-ttu-id="a426e-168">代わりに、ユーザーからのすべての入力を検証し、出力をエンコードします。</span><span class="sxs-lookup"><span data-stu-id="a426e-168">Instead, validate all input from users and encode the output.</span></span> <span data-ttu-id="a426e-169">一部のケースでは、正規表現を使用して入力を検証できますが、より複雑なケースでは、値が許可された値と一致するかどうかを判断する .NET クラスを使用してユーザー入力を検証する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a426e-169">In some limited cases, you can use regular expressions to validate the input, but in more complicated cases you should validate user input by using .NET classes that determine if the value matches allowed values.</span></span>

<span data-ttu-id="a426e-170">次の例は、Uri クラスの静的メソッドを使用して、ユーザーが指定した Uri が有効かどうかを判断する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="a426e-170">The following example shows how to use a static method in the Uri class to determine whether the Uri provided by a user is valid.</span></span>

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample3.cs)]

<span data-ttu-id="a426e-171">ただし、Uri を十分に検証するには、`http` または `https`が指定されていることを確認する必要もあります。</span><span class="sxs-lookup"><span data-stu-id="a426e-171">However, to sufficiently verify the Uri, you should also check to make sure it specifies `http` or `https`.</span></span> <span data-ttu-id="a426e-172">次の例では、インスタンスメソッドを使用して、Uri が有効であることを確認します。</span><span class="sxs-lookup"><span data-stu-id="a426e-172">The following example uses instance methods to verify that the Uri is valid.</span></span>

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample4.cs)]

<span data-ttu-id="a426e-173">ユーザー入力を HTML として、または SQL クエリにユーザー入力を含めて表示する前に、その値をエンコードして、悪意のあるコードが含まれていないことを確認します。</span><span class="sxs-lookup"><span data-stu-id="a426e-173">Before rendering user input as HTML or including user input in a SQL query, encode the values to ensure malicious code is not included.</span></span>

<span data-ttu-id="a426e-174">次に示すように、&lt;%:%&gt; 構文を使用してマークアップの値を HTML エンコードできます。</span><span class="sxs-lookup"><span data-stu-id="a426e-174">You can HTML encode the value in markup with the &lt;%: %&gt; syntax, as shown below.</span></span>

[!code-aspx[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample5.aspx?highlight=1)]

<span data-ttu-id="a426e-175">また、Razor 構文では、次に示すように、@ を使用して HTML エンコードできます。</span><span class="sxs-lookup"><span data-stu-id="a426e-175">Or, in Razor syntax, you can HTML encode with @, as shown below.</span></span>

[!code-cshtml[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample6.cshtml?highlight=1)]

<span data-ttu-id="a426e-176">次の例は、コードビハインドで値を HTML エンコードする方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="a426e-176">The next example shows how to HTML encode a value in code-behind.</span></span>

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample7.cs)]

<span data-ttu-id="a426e-177">SQL コマンドの値を安全にエンコードするには、 [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx)などのコマンドパラメーターを使用します。</span><span class="sxs-lookup"><span data-stu-id="a426e-177">To safely encode a value for SQL commands, use command parameters such as the [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx).</span></span> <a id="cookieless"></a>

### <a name="cookieless-forms-authentication-and-session"></a><span data-ttu-id="a426e-178">Cookie なしのフォーム認証とセッション</span><span class="sxs-lookup"><span data-stu-id="a426e-178">Cookieless forms authentication and session</span></span>

<span data-ttu-id="a426e-179">推奨: cookie が必要です。</span><span class="sxs-lookup"><span data-stu-id="a426e-179">Recommendation: Require cookies.</span></span>

<span data-ttu-id="a426e-180">クエリ文字列で認証情報を渡すことは、セキュリティで保護されていません。</span><span class="sxs-lookup"><span data-stu-id="a426e-180">Passing authentication information in the query string is not secure.</span></span> <span data-ttu-id="a426e-181">そのため、アプリケーションに認証が含まれている場合は、cookie が必要です。</span><span class="sxs-lookup"><span data-stu-id="a426e-181">Therefore, require cookies when your application includes authentication.</span></span> <span data-ttu-id="a426e-182">Cookie に機密情報が格納されている場合は、cookie に SSL を要求することを検討してください。</span><span class="sxs-lookup"><span data-stu-id="a426e-182">If your cookie stores sensitive information, consider requiring SSL for the cookie.</span></span>

<span data-ttu-id="a426e-183">次の例は、web.config ファイルでを指定する方法を示しています。フォーム認証では、SSL を使用して送信される cookie が必要です。</span><span class="sxs-lookup"><span data-stu-id="a426e-183">The following example shows how to specify in the Web.config file that Forms Authentication requires a cookie that is transmitted over SSL.</span></span>

[!code-xml[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample8.xml)]

<a id="viewstatemac"></a>

### <a name="enableviewstatemac"></a><span data-ttu-id="a426e-184">EnableViewStateMac</span><span class="sxs-lookup"><span data-stu-id="a426e-184">EnableViewStateMac</span></span>

<span data-ttu-id="a426e-185">推奨: false に設定しないでください。</span><span class="sxs-lookup"><span data-stu-id="a426e-185">Recommendation: Never set to false.</span></span>

<span data-ttu-id="a426e-186">既定では、EnableViewStateMac は true に設定されています。</span><span class="sxs-lookup"><span data-stu-id="a426e-186">By default, EnableViewStateMac is set to true.</span></span> <span data-ttu-id="a426e-187">アプリケーションがビューステートを使用していない場合でも、EnableViewStateMac を false に設定しないでください。</span><span class="sxs-lookup"><span data-stu-id="a426e-187">Even if your application is not using view state, do not set EnableViewStateMac to false.</span></span> <span data-ttu-id="a426e-188">この値を false に設定すると、アプリケーションはクロスサイトスクリプトに対して脆弱になります。</span><span class="sxs-lookup"><span data-stu-id="a426e-188">Setting this value to false will make your application vulnerable to cross-site scripting.</span></span>

<span data-ttu-id="a426e-189">ASP.NET 4.5.2 以降では、ランタイムによって**EnableViewStateMac = true**が適用されます。</span><span class="sxs-lookup"><span data-stu-id="a426e-189">Starting with ASP.NET 4.5.2, the runtime enforces **EnableViewStateMac=true**.</span></span> <span data-ttu-id="a426e-190">False に設定した場合でも、ランタイムはこの値を無視し、true に設定された値を使用して処理を続行します。</span><span class="sxs-lookup"><span data-stu-id="a426e-190">Even if you set it to false, the runtime ignores this value and proceeds with the value set to true.</span></span> <span data-ttu-id="a426e-191">詳細については、「 [ASP.NET 4.5.2 And EnableViewStateMac](https://blogs.msdn.com/b/webdev/archive/2014/05/07/asp-net-4-5-2-and-enableviewstatemac.aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a426e-191">For more information, see [ASP.NET 4.5.2 and EnableViewStateMac](https://blogs.msdn.com/b/webdev/archive/2014/05/07/asp-net-4-5-2-and-enableviewstatemac.aspx).</span></span>

<span data-ttu-id="a426e-192">次の例は、EnableViewStateMac を true に設定する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="a426e-192">The following example shows how to set EnableViewStateMac to true.</span></span> <span data-ttu-id="a426e-193">この値は、既定で true に設定されているため、実際に true に設定する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="a426e-193">You do not need to actually set this value to true because it is true by default.</span></span> <span data-ttu-id="a426e-194">ただし、アプリケーションの任意のページで false に設定した場合は、すぐにこの値を修正する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a426e-194">However, if you have set it to false on any page in your application, you must immediately correct this value.</span></span>

[!code-aspx[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample9.aspx)]

<a id="medium"></a>

### <a name="medium-trust"></a><span data-ttu-id="a426e-195">中程度の信頼</span><span class="sxs-lookup"><span data-stu-id="a426e-195">Medium trust</span></span>

<span data-ttu-id="a426e-196">推奨: セキュリティ境界として中程度の信頼 (またはその他の信頼レベル) に依存しないでください。</span><span class="sxs-lookup"><span data-stu-id="a426e-196">Recommendation: Do not depend on Medium Trust (or any other trust level) as a security boundary.</span></span>

<span data-ttu-id="a426e-197">部分信頼では、アプリケーションを適切に保護することはできないため、使用しないでください。</span><span class="sxs-lookup"><span data-stu-id="a426e-197">Partial trust does not adequately protect your application and should not be used.</span></span> <span data-ttu-id="a426e-198">代わりに、完全信頼を使用して、信頼されていないアプリケーションを別のアプリケーションプールに分離します。</span><span class="sxs-lookup"><span data-stu-id="a426e-198">Instead, use Full Trust, and isolate untrusted applications in separate application pools.</span></span> <span data-ttu-id="a426e-199">また、各アプリケーションプールを一意の id で実行します。</span><span class="sxs-lookup"><span data-stu-id="a426e-199">Also, run each application pool under a unique identity.</span></span> <span data-ttu-id="a426e-200">詳細については、「 [ASP.NET 部分信頼ではアプリケーションの分離が保証されない](https://support.microsoft.com/kb/2698981)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a426e-200">For more information, see [ASP.NET Partial Trust does not guarantee application isolation](https://support.microsoft.com/kb/2698981).</span></span>

<a id="appsettings"></a>

### <a name="ltappsettingsgt"></a><span data-ttu-id="a426e-201">&lt;appSettings&gt;</span><span class="sxs-lookup"><span data-stu-id="a426e-201">&lt;appSettings&gt;</span></span>

<span data-ttu-id="a426e-202">推奨: &lt;appSettings&gt; 要素のセキュリティ設定を無効にしないでください。</span><span class="sxs-lookup"><span data-stu-id="a426e-202">Recommendation: Do not disable security settings in &lt;appSettings&gt; element.</span></span>

<span data-ttu-id="a426e-203">AppSettings 要素には、セキュリティ更新プログラムに必要な多くの値が含まれています。</span><span class="sxs-lookup"><span data-stu-id="a426e-203">The appSettings element contains many values which are required for security updates.</span></span> <span data-ttu-id="a426e-204">これらの値は変更したり無効にしたりしないでください。</span><span class="sxs-lookup"><span data-stu-id="a426e-204">You should not change or disable these values.</span></span> <span data-ttu-id="a426e-205">更新プログラムを展開するときにこれらの値を無効にする必要がある場合は、展開の完了後すぐに再度有効にしてください。</span><span class="sxs-lookup"><span data-stu-id="a426e-205">If you must disable these values when deploying an update, immediately re-enable after completing deployment.</span></span>

<span data-ttu-id="a426e-206">詳細については、「 [ASP.NET AppSettings 要素](https://msdn.microsoft.com/library/hh975440.aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a426e-206">For details, see [ASP.NET appSettings Element](https://msdn.microsoft.com/library/hh975440.aspx).</span></span>

<a id="urlpathencode"></a>

### <a name="urlpathencode"></a><span data-ttu-id="a426e-207">UrlPathEncode</span><span class="sxs-lookup"><span data-stu-id="a426e-207">UrlPathEncode</span></span>

<span data-ttu-id="a426e-208">推奨: 代わりに[UrlEncode](https://msdn.microsoft.com/library/zttxte6w.aspx)を使用してください。</span><span class="sxs-lookup"><span data-stu-id="a426e-208">Recommendation: Use [UrlEncode](https://msdn.microsoft.com/library/zttxte6w.aspx) instead.</span></span>

<span data-ttu-id="a426e-209">UrlPathEncode メソッドが .NET Framework に追加され、特定のブラウザーの互換性の問題を解決します。</span><span class="sxs-lookup"><span data-stu-id="a426e-209">The UrlPathEncode method was added to the .NET Framework to resolve a very specific browser compatibility problem.</span></span> <span data-ttu-id="a426e-210">URL を適切にエンコードすることはできず、クロスサイトスクリプトからアプリケーションを保護することもありません。</span><span class="sxs-lookup"><span data-stu-id="a426e-210">It does not adequately encode a URL, and does not protect your application from cross-site scripting.</span></span> <span data-ttu-id="a426e-211">アプリケーションでは使用しないでください。</span><span class="sxs-lookup"><span data-stu-id="a426e-211">You should never use it in your application.</span></span> <span data-ttu-id="a426e-212">代わりに、 [UrlEncode](https://msdn.microsoft.com/library/zttxte6w.aspx)を使用してください。</span><span class="sxs-lookup"><span data-stu-id="a426e-212">Instead, use [UrlEncode](https://msdn.microsoft.com/library/zttxte6w.aspx).</span></span>

<span data-ttu-id="a426e-213">次の例は、エンコードされた URL をハイパーリンクコントロールのクエリ文字列パラメーターとして渡す方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="a426e-213">The following example shows how to pass an encoded URL as a query string parameter for a hyperlink control.</span></span>

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample10.cs)]

<a id="performance"></a>

## <a name="reliability-and-performance"></a><span data-ttu-id="a426e-214">信頼性とパフォーマンス</span><span class="sxs-lookup"><span data-stu-id="a426e-214">Reliability and performance</span></span>

<a id="presend"></a>

### <a name="presendrequestheaders-and-presendrequestcontent"></a><span data-ttu-id="a426e-215">PreSendRequestHeaders と PreSendRequestContent</span><span class="sxs-lookup"><span data-stu-id="a426e-215">PreSendRequestHeaders and PreSendRequestContent</span></span>

<span data-ttu-id="a426e-216">推奨: これらのイベントをマネージモジュールで使用しないでください。</span><span class="sxs-lookup"><span data-stu-id="a426e-216">Recommendation: Do not use these events with managed modules.</span></span> <span data-ttu-id="a426e-217">代わりに、必要なタスクを実行するネイティブ IIS モジュールを記述します。</span><span class="sxs-lookup"><span data-stu-id="a426e-217">Instead, write a native IIS module to perform the required task.</span></span> <span data-ttu-id="a426e-218">「[ネイティブコード HTTP モジュールの作成](https://msdn.microsoft.com/library/ms693629.aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a426e-218">See [Creating Native-Code HTTP Modules](https://msdn.microsoft.com/library/ms693629.aspx).</span></span>

<span data-ttu-id="a426e-219">ネイティブ IIS モジュールでは、 [PreSendRequestHeaders](https://msdn.microsoft.com/library/system.web.httpapplication.presendrequestheaders.aspx)および[Presendrequestcontent](https://msdn.microsoft.com/library/system.web.httpapplication.presendrequestcontent.aspx)イベントを使用できます。</span><span class="sxs-lookup"><span data-stu-id="a426e-219">You can use the [PreSendRequestHeaders](https://msdn.microsoft.com/library/system.web.httpapplication.presendrequestheaders.aspx) and [PreSendRequestContent](https://msdn.microsoft.com/library/system.web.httpapplication.presendrequestcontent.aspx) events with native IIS modules.</span></span>
> [!WARNING]
> <span data-ttu-id="a426e-220">`IHttpModule`を実装するマネージモジュールで `PreSendRequestHeaders` および `PreSendRequestContent` を使用しないでください。</span><span class="sxs-lookup"><span data-stu-id="a426e-220">Do not use `PreSendRequestHeaders` and `PreSendRequestContent` with managed modules that implement `IHttpModule`.</span></span> <span data-ttu-id="a426e-221">これらのプロパティを設定すると、非同期要求に関する問題が発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="a426e-221">Setting these properties can cause issues with asynchronous requests.</span></span> <span data-ttu-id="a426e-222">アプリケーションで要求されたルーティング (ARR) と websocket を組み合わせると、w3wp.exe がクラッシュする原因となるアクセス違反例外が発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="a426e-222">The combination of Application Requested Routing (ARR) and websockets might lead to access violation exceptions that can cause w3wp to crash.</span></span> <span data-ttu-id="a426e-223">たとえば、iiscore のようになります。Iiscore .dll の W3_CONTEXT_BASE:: GetIsLastNotification + 68 で、アクセス違反例外 (0xC0000005) が発生しました。</span><span class="sxs-lookup"><span data-stu-id="a426e-223">For example, iiscore!W3_CONTEXT_BASE::GetIsLastNotification+68 in iiscore.dll has caused an access violation exception (0xC0000005).</span></span>

<a id="asyncevents"></a>

### <a name="asynchronous-page-events-with-web-forms"></a><span data-ttu-id="a426e-224">Web フォームを使用した非同期ページイベント</span><span class="sxs-lookup"><span data-stu-id="a426e-224">Asynchronous page events with web forms</span></span>

<span data-ttu-id="a426e-225">推奨事項: Web フォームでは、ページのライフサイクルイベントに対して非同期の void メソッドを記述しないでください。代わりに、非同期コード用に[RegisterAsyncTask](https://msdn.microsoft.com/library/system.web.ui.page.registerasynctask.aspx)を使用します。</span><span class="sxs-lookup"><span data-stu-id="a426e-225">Recommendation: In Web Forms, avoid writing async void methods for Page lifecycle events, and instead use [Page.RegisterAsyncTask](https://msdn.microsoft.com/library/system.web.ui.page.registerasynctask.aspx) for asynchronous code.</span></span>

<span data-ttu-id="a426e-226">**Async**と**void**を使用してページイベントをマークすると、非同期コードがいつ終了したかを判断できません。</span><span class="sxs-lookup"><span data-stu-id="a426e-226">When you mark a page event with **async** and **void**, you cannot determine when the asynchronous code has finished.</span></span> <span data-ttu-id="a426e-227">代わりに、Page. RegisterAsyncTask を使用して非同期コードを実行し、その完了を追跡できるようにします。</span><span class="sxs-lookup"><span data-stu-id="a426e-227">Instead, use Page.RegisterAsyncTask to run the asynchronous code in a way that enables you to track its completion.</span></span>

<span data-ttu-id="a426e-228">次の例は、非同期コードを含むボタンクリックハンドラーを示しています。</span><span class="sxs-lookup"><span data-stu-id="a426e-228">The following example shows a button click handler that contains asynchronous code.</span></span> <span data-ttu-id="a426e-229">この例では、非同期タスクの簡略化された例としてのみ提供される文字列値を非同期に読み取り、推奨される方法としては使用しません。</span><span class="sxs-lookup"><span data-stu-id="a426e-229">This example includes reading a string value asynchronously, which is provided only as a simplified example of an asynchronous task and not as a recommended practice.</span></span>

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample11.cs)]

<span data-ttu-id="a426e-230">非同期タスクを使用している場合は、web.config ファイルで Http ランタイムターゲットフレームワークを 4.5 (またはそれ以降) に設定します。</span><span class="sxs-lookup"><span data-stu-id="a426e-230">If you are using asynchronous Tasks, set the Http runtime target framework to 4.5 (or later) in the Web.config file.</span></span> <span data-ttu-id="a426e-231">ターゲットフレームワークを4.5 に設定すると、.NET 4.5 で追加された新しい同期コンテキストが有効になります。</span><span class="sxs-lookup"><span data-stu-id="a426e-231">Setting the target framework to 4.5 turns on the new synchronization context that was added in .NET 4.5.</span></span> <span data-ttu-id="a426e-232">この値は、Visual Studio の新しいプロジェクトで既定で設定されますが、既存のプロジェクトを操作している場合は設定されません。</span><span class="sxs-lookup"><span data-stu-id="a426e-232">This value is set by default in new projects in Visual Studio, but is not be set if you are working with an existing project.</span></span>

[!code-xml[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample12.xml)]

<a id="fire"></a>

### <a name="fire-and-forget-work"></a><span data-ttu-id="a426e-233">起動と破棄の作業</span><span class="sxs-lookup"><span data-stu-id="a426e-233">Fire-and-forget work</span></span>

<span data-ttu-id="a426e-234">推奨事項: ASP.NET 内で要求を処理する場合は、起動と破棄の作業 (QueueUserWorkItem メソッドの呼び出し、デリゲートを繰り返し呼び出すタイマーの作成など) を行わないようにしてください。</span><span class="sxs-lookup"><span data-stu-id="a426e-234">Recommendation: When handling a request within ASP.NET, avoid launching fire-and-forget work (such calling the ThreadPool.QueueUserWorkItem method or creating a timer that repeatedly calls a delegate).</span></span>

<span data-ttu-id="a426e-235">アプリケーションの ASP.NET 内で実行される作業を忘れることがある場合、アプリケーションは同期されない可能性があります。いつでも、アプリドメインを破棄できます。つまり、進行中のプロセスがアプリケーションの現在の状態と一致しなくなる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="a426e-235">If your application has fire-and-forget work that runs within ASP.NET, your application can get out of sync. At any time, the app domain can be destroyed which means your ongoing process may no longer match the current state of the application.</span></span>

<span data-ttu-id="a426e-236">この種類の作業は、ASP.NET の外部で移動する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a426e-236">You should move this type of work outside of ASP.NET.</span></span> <span data-ttu-id="a426e-237">Azure の Web ジョブ、Windows サービス、または Worker ロールを使用して、進行中の作業を実行し、別のプロセスからそのコードを実行できます。</span><span class="sxs-lookup"><span data-stu-id="a426e-237">You can use a Web Jobs, Windows Service or a Worker role in Azure to perform ongoing work, and run that code from another process.</span></span>

<span data-ttu-id="a426e-238">ASP.NET 内でこの作業を実行する必要がある場合は、 [WebBackgrounder](http://www.nuget.org/packages/webbackgrounder)という名前の Nuget パッケージを追加してコードを実行できます。</span><span class="sxs-lookup"><span data-stu-id="a426e-238">If you must perform this work within ASP.NET, you can add the Nuget package called [WebBackgrounder](http://www.nuget.org/packages/webbackgrounder) to run the code.</span></span>

<a id="requestentity"></a>

### <a name="request-entity-body"></a><span data-ttu-id="a426e-239">要求エンティティ本体</span><span class="sxs-lookup"><span data-stu-id="a426e-239">Request entity body</span></span>

<span data-ttu-id="a426e-240">推奨事項: ハンドラーの execute イベントの前に、InputStream または要求を読み取らないようにします。</span><span class="sxs-lookup"><span data-stu-id="a426e-240">Recommendation: Avoid reading Request.Form or Request.InputStream before the handler's execute event.</span></span>

<span data-ttu-id="a426e-241">最初に、要求. フォームまたは InputStream から読み取る必要があります。</span><span class="sxs-lookup"><span data-stu-id="a426e-241">The earliest you should read from Request.Form or Request.InputStream is during the handler's execute event.</span></span> <span data-ttu-id="a426e-242">MVC では、コントローラーはハンドラーであり、アクションメソッドが実行されるときに execute イベントです。</span><span class="sxs-lookup"><span data-stu-id="a426e-242">In MVC, the Controller is the handler and the execute event is when the action method runs.</span></span> <span data-ttu-id="a426e-243">Web フォームでは、ページはハンドラーであり、execute イベントは、ページの Init イベントが発生したときに発生します。</span><span class="sxs-lookup"><span data-stu-id="a426e-243">In Web Forms, the Page is the handler and the execute event is when the Page.Init event fires.</span></span> <span data-ttu-id="a426e-244">Execute イベントより前に要求エンティティ本体を読み取ると、要求の処理が妨げられます。</span><span class="sxs-lookup"><span data-stu-id="a426e-244">If you read the request entity body earlier than the execute event, you interfere with the processing of the request.</span></span>

<span data-ttu-id="a426e-245">Execute イベントの前に要求エンティティ本体を読み取る必要がある場合は、 [GetBufferlessInputStream](https://msdn.microsoft.com/library/ff406798.aspx)または[httprequest.getbufferedinputstream](https://msdn.microsoft.com/library/system.web.httprequest.getbufferedinputstream.aspx)を使用します。</span><span class="sxs-lookup"><span data-stu-id="a426e-245">If you need to read the request entity body before the execute event, use either [Request.GetBufferlessInputStream](https://msdn.microsoft.com/library/ff406798.aspx) or [Request.GetBufferedInputStream](https://msdn.microsoft.com/library/system.web.httprequest.getbufferedinputstream.aspx).</span></span> <span data-ttu-id="a426e-246">GetBufferlessInputStream を使用する場合は、要求から生のストリームを取得し、要求全体を処理する必要があると想定します。</span><span class="sxs-lookup"><span data-stu-id="a426e-246">When you use GetBufferlessInputStream, you get the raw stream from the request, and assume responsibility for processing the entire request.</span></span> <span data-ttu-id="a426e-247">GetBufferlessInputStream を呼び出した後、InputStream は ASP.NET によって設定されていないため、使用できません。</span><span class="sxs-lookup"><span data-stu-id="a426e-247">After calling GetBufferlessInputStream, Request.Form and Request.InputStream are not available because they have not been populated by ASP.NET.</span></span> <span data-ttu-id="a426e-248">Httprequest.getbufferedinputstream を使用すると、要求からストリームのコピーが取得されます。</span><span class="sxs-lookup"><span data-stu-id="a426e-248">When you use GetBufferedInputStream, you get a copy of the stream from the request.</span></span> <span data-ttu-id="a426e-249">要求の形式と InputStream は、ASP.NET が他のコピーを設定するため、後で要求の中でも使用できます。</span><span class="sxs-lookup"><span data-stu-id="a426e-249">Request.Form and Request.InputStream are still available later in the request because ASP.NET populates the other copy.</span></span>

<a id="redirect"></a>

### <a name="responseredirect-and-responseend"></a><span data-ttu-id="a426e-250">応答。リダイレクトと応答終了</span><span class="sxs-lookup"><span data-stu-id="a426e-250">Response.Redirect and Response.End</span></span>

<span data-ttu-id="a426e-251">推奨事項: Response を呼び出した後のスレッドの処理方法の違いに注意[してください。リダイレクト (String)](https://msdn.microsoft.com/library/t9dwyts4.aspx)。</span><span class="sxs-lookup"><span data-stu-id="a426e-251">Recommendation: Be aware of differences in how thread is handled after calling [Response.Redirect(String)](https://msdn.microsoft.com/library/t9dwyts4.aspx).</span></span>

<span data-ttu-id="a426e-252">[Response. Redirect (String)](https://msdn.microsoft.com/library/t9dwyts4.aspx)メソッドは、Response. End メソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="a426e-252">The [Response.Redirect(String)](https://msdn.microsoft.com/library/t9dwyts4.aspx) method calls the Response.End method.</span></span> <span data-ttu-id="a426e-253">同期プロセスでは、要求を呼び出します。リダイレクトを実行すると、現在のスレッドがすぐに中止されます。</span><span class="sxs-lookup"><span data-stu-id="a426e-253">In a synchronous process, calling Request.Redirect causes the current thread to immediately abort.</span></span> <span data-ttu-id="a426e-254">ただし、非同期プロセスでは、Response を呼び出すと、現在のスレッドが中止されないため、要求に対してコードの実行が続行されます。</span><span class="sxs-lookup"><span data-stu-id="a426e-254">However, in an asynchronous process, calling Response.Redirect does not abort the current thread, so code execution continues for the request.</span></span> <span data-ttu-id="a426e-255">非同期プロセスでは、メソッドからタスクを返してコードの実行を停止する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a426e-255">In an asynchronous process, you must return the Task from the method to stop the code execution.</span></span>

<span data-ttu-id="a426e-256">MVC プロジェクトでは、Response. Redirect を呼び出すことはできません。</span><span class="sxs-lookup"><span data-stu-id="a426e-256">In an MVC project, you should not call Response.Redirect.</span></span> <span data-ttu-id="a426e-257">代わりに、RedirectResult を返します。</span><span class="sxs-lookup"><span data-stu-id="a426e-257">Instead, return a RedirectResult.</span></span>

<a id="viewstatemode"></a>

### <a name="enableviewstate-and-viewstatemode"></a><span data-ttu-id="a426e-258">EnableViewState と ViewStateMode</span><span class="sxs-lookup"><span data-stu-id="a426e-258">EnableViewState and ViewStateMode</span></span>

<span data-ttu-id="a426e-259">推奨事項: ビューステートを使用するコントロールをきめ細かく制御できるように、EnableViewState ではなく ViewStateMode を使用します。</span><span class="sxs-lookup"><span data-stu-id="a426e-259">Recommendation: Use ViewStateMode, instead of EnableViewState, to provide granular control over which controls use view state.</span></span>

<span data-ttu-id="a426e-260">Page ディレクティブで EnableViewState を false に設定すると、ページ内のすべてのコントロールに対してビューステートが無効になり、有効にすることはできません。</span><span class="sxs-lookup"><span data-stu-id="a426e-260">When you set EnableViewState to false in the Page directive, view state is disabled for all controls within the page and cannot be enabled.</span></span> <span data-ttu-id="a426e-261">ページの特定のコントロールに対してのみビューステートを有効にする場合は、ページの ViewStateMode を Disabled に設定します。</span><span class="sxs-lookup"><span data-stu-id="a426e-261">If you want to enable view state for only certain controls in your page, set ViewStateMode to Disabled for the Page.</span></span>

[!code-aspx[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample13.aspx)]

<span data-ttu-id="a426e-262">次に、ビューステートを実際に必要とするコントロールに対してのみ ViewStateMode を Enabled に設定します。</span><span class="sxs-lookup"><span data-stu-id="a426e-262">Then, set ViewStateMode to Enabled on only the controls that actually need view state.</span></span>

[!code-aspx[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample14.aspx)]

<span data-ttu-id="a426e-263">必要なコントロールに対してのみビューステートを有効にすることで、web ページのビューステートのサイズを縮小できます。</span><span class="sxs-lookup"><span data-stu-id="a426e-263">By enabling view state for only the controls that need it, you can shrink the size of the view state for your web pages.</span></span>

<a id="sqlprovider"></a>

### <a name="sqlmembershipprovider"></a><span data-ttu-id="a426e-264">SqlMembershipProvider</span><span class="sxs-lookup"><span data-stu-id="a426e-264">SqlMembershipProvider</span></span>

<span data-ttu-id="a426e-265">推奨事項: ユニバーサルプロバイダーを使用します。</span><span class="sxs-lookup"><span data-stu-id="a426e-265">Recommendation: Use Universal Providers.</span></span>

<span data-ttu-id="a426e-266">現在のプロジェクトテンプレートでは、SqlMembershipProvider が[ASP.NET ユニバーサルプロバイダー](http://www.nuget.org/packages/Microsoft.AspNet.Providers)に置き換えられました。これは NuGet パッケージとして利用できます。</span><span class="sxs-lookup"><span data-stu-id="a426e-266">In the current project templates, SqlMembershipProvider has been replaced by [ASP.NET Universal Providers](http://www.nuget.org/packages/Microsoft.AspNet.Providers), which is available as a NuGet package.</span></span> <span data-ttu-id="a426e-267">以前のバージョンのテンプレートを使用してビルドされたプロジェクトで SqlMembershipProvider を使用している場合は、ユニバーサルプロバイダーに切り替える必要があります。</span><span class="sxs-lookup"><span data-stu-id="a426e-267">If you are using SqlMembershipProvider in a project that was built with an earlier version of the templates, you should switch to Universal Providers.</span></span> <span data-ttu-id="a426e-268">ユニバーサルプロバイダーは、Entity Framework によってサポートされているすべてのデータベースで動作します。</span><span class="sxs-lookup"><span data-stu-id="a426e-268">The Universal Providers work with all databases that are supported by Entity Framework.</span></span>

<span data-ttu-id="a426e-269">詳細については、「 [ASP.NET ユニバーサルプロバイダーの概要](http://www.hanselman.com/blog/IntroducingSystemWebProvidersASPNETUniversalProvidersForSessionMembershipRolesAndUserProfileOnSQLCompactAndSQLAzure.aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a426e-269">For more information, see [Introducing ASP.NET Universal Providers](http://www.hanselman.com/blog/IntroducingSystemWebProvidersASPNETUniversalProvidersForSessionMembershipRolesAndUserProfileOnSQLCompactAndSQLAzure.aspx).</span></span>

<a id="long"></a>

### <a name="long-running-requests-110-seconds"></a><span data-ttu-id="a426e-270">実行時間の長い要求 (> 110 秒)</span><span class="sxs-lookup"><span data-stu-id="a426e-270">Long-running requests (>110 seconds)</span></span>

<span data-ttu-id="a426e-271">推奨事項: 接続されたクライアントに[websocket](https://msdn.microsoft.com/library/system.net.websockets.websocket.aspx)または[SignalR](../../../signalr/index.md)を使用し、非同期 i/o 操作を使用します。</span><span class="sxs-lookup"><span data-stu-id="a426e-271">Recommendation: Use [WebSockets](https://msdn.microsoft.com/library/system.net.websockets.websocket.aspx) or [SignalR](../../../signalr/index.md) for connected clients, and use asynchronous I/O operations.</span></span>

<span data-ttu-id="a426e-272">実行時間の長い要求では、web アプリケーションで予期しない結果が発生し、パフォーマンスが低下する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="a426e-272">Long-running requests can cause unpredictable results and poor performance in your web application.</span></span> <span data-ttu-id="a426e-273">要求の既定のタイムアウト設定は110秒です。</span><span class="sxs-lookup"><span data-stu-id="a426e-273">The default timeout setting for a request is 110 seconds.</span></span> <span data-ttu-id="a426e-274">実行時間の長い要求でセッション状態を使用している場合、ASP.NET は110秒後にセッションオブジェクトのロックを解除します。</span><span class="sxs-lookup"><span data-stu-id="a426e-274">If you are using session state with a long-running request, ASP.NET will release the lock on the Session object after 110 seconds.</span></span> <span data-ttu-id="a426e-275">ただし、ロックが解除され、操作が正常に完了しない可能性がある場合、アプリケーションはセッションオブジェクトに対する操作の途中である可能性があります。</span><span class="sxs-lookup"><span data-stu-id="a426e-275">However, your application might be in the middle of an operation on the Session object when the lock is released, and the operation might not complete successfully.</span></span> <span data-ttu-id="a426e-276">最初の要求の実行中にユーザーからの2番目の要求がブロックされた場合、2番目の要求では、不整合な状態にあるセッションオブジェクトにアクセスする可能性があります。</span><span class="sxs-lookup"><span data-stu-id="a426e-276">If a second request from the user is blocked while the first request is running, the second request might access the Session object in an inconsistent state.</span></span>

<span data-ttu-id="a426e-277">アプリケーションにブロッキング (または同期) i/o 操作が含まれている場合は、アプリケーションが応答しなくなります。</span><span class="sxs-lookup"><span data-stu-id="a426e-277">If your application includes blocking (or synchronous) I/O operations, the application will be unresponsive.</span></span>

<span data-ttu-id="a426e-278">パフォーマンスを向上させるには、.NET Framework で非同期 i/o 操作を使用します。</span><span class="sxs-lookup"><span data-stu-id="a426e-278">To improve performance, use the asynchronous I/O operations in the .NET Framework.</span></span> <span data-ttu-id="a426e-279">また、Websocket または SignalR を使用して、クライアントをサーバーに接続します。</span><span class="sxs-lookup"><span data-stu-id="a426e-279">Also, use WebSockets or SignalR for connecting clients to the server.</span></span> <span data-ttu-id="a426e-280">これらの機能は、実行時間の長い要求を効率的に処理するように設計されています。</span><span class="sxs-lookup"><span data-stu-id="a426e-280">These features are designed to efficiently handle long-running requests.</span></span>
