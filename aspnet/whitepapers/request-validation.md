---
uid: whitepapers/request-validation
title: 要求の検証-スクリプト攻撃の防止 |Microsoft Docs
author: rick-anderson
description: このホワイトペーパーでは、ASP.NET の要求検証機能について説明します。既定では、アプリケーションはエンコードされていない HTML コンテンツを処理できません。
ms.author: riande
ms.date: 02/10/2010
ms.assetid: fa429113-5f8f-4ef4-97c5-5c04900a19fa
msc.legacyurl: /whitepapers/request-validation
msc.type: content
ms.openlocfilehash: 807cccd6fe1acdd6359b014387abd3878840d4cd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78520582"
---
# <a name="request-validation---preventing-script-attacks"></a><span data-ttu-id="8fe4f-103">要求検証 - スクリプト攻撃を防ぐ</span><span class="sxs-lookup"><span data-stu-id="8fe4f-103">Request Validation - Preventing Script Attacks</span></span>

> <span data-ttu-id="8fe4f-104">このホワイトペーパーでは、ASP.NET の要求検証機能について説明します。既定では、アプリケーションは、エンコードされていない HTML コンテンツをサーバーに送信できません。</span><span class="sxs-lookup"><span data-stu-id="8fe4f-104">This paper describes the request validation feature of ASP.NET where, by default, the application is prevented from processing unencoded HTML content submitted to the server.</span></span> <span data-ttu-id="8fe4f-105">この要求の検証機能は、アプリケーションが HTML データを安全に処理するように設計されている場合は無効にすることができます。</span><span class="sxs-lookup"><span data-stu-id="8fe4f-105">This request validation feature can be disabled when the application has been designed to safely process HTML data.</span></span>
> 
> <span data-ttu-id="8fe4f-106">ASP.NET 1.1 と ASP.NET 2.0 に適用されます。</span><span class="sxs-lookup"><span data-stu-id="8fe4f-106">Applies to ASP.NET 1.1 and ASP.NET 2.0.</span></span>

<span data-ttu-id="8fe4f-107">要求の検証は ASP.NET 1.1 以降の機能で、エンコードされていない HTML を含むコンテンツを、サーバーが受け入れられないようにします。</span><span class="sxs-lookup"><span data-stu-id="8fe4f-107">Request validation, a feature of ASP.NET since version 1.1, prevents the server from accepting content containing un-encoded HTML.</span></span> <span data-ttu-id="8fe4f-108">この機能は、スクリプト インジェクション攻撃、つまり、クライアント スクリプト コードや HTML が知らないうちにサーバーに送信され、格納された後、他のユーザーに提供されるのを防ぐことを目的としています。</span><span class="sxs-lookup"><span data-stu-id="8fe4f-108">This feature is designed to help prevent some script-injection attacks whereby client script code or HTML can be unknowingly submitted to a server, stored, and then presented to other users.</span></span> <span data-ttu-id="8fe4f-109">ただし、すべての入力データを適宜検証し、HTML エンコードを行うことを強くお勧めします。</span><span class="sxs-lookup"><span data-stu-id="8fe4f-109">We still strongly recommend that you validate all input data and HTML encode it when appropriate.</span></span>

<span data-ttu-id="8fe4f-110">たとえば、ユーザーの電子メールアドレスを要求する Web ページを作成し、その電子メールアドレスをデータベースに保存します。</span><span class="sxs-lookup"><span data-stu-id="8fe4f-110">For example, you create a Web page that requests a user's email address and then stores that email address in a database.</span></span> <span data-ttu-id="8fe4f-111">ユーザーが &lt;スクリプト&gt;の警告 ("hello from SCRIPT") を入力すると、有効な電子メールアドレスではなく、/SCRIPT&gt;&lt;ます。そのデータが表示されると、コンテンツが正しくエンコードされていない場合は、このスクリプトを実行できます。</span><span class="sxs-lookup"><span data-stu-id="8fe4f-111">If the user enters &lt;SCRIPT&gt;alert("hello from script")&lt;/SCRIPT&gt; instead of a valid email address, when that data is presented, this script can be executed if the content was not properly encoded.</span></span> <span data-ttu-id="8fe4f-112">ASP.NET の要求の検証機能によって、この問題が発生することはありません。</span><span class="sxs-lookup"><span data-stu-id="8fe4f-112">The request validation feature of ASP.NET prevents this from happening.</span></span>

## <a name="why-this-feature-is-useful"></a><span data-ttu-id="8fe4f-113">この機能が役に立つ理由</span><span class="sxs-lookup"><span data-stu-id="8fe4f-113">Why this feature is useful</span></span>

<span data-ttu-id="8fe4f-114">多くのサイトは、単純なスクリプトインジェクション攻撃に対して開かれていることを認識していません。</span><span class="sxs-lookup"><span data-stu-id="8fe4f-114">Many sites are not aware that they are open to simple script injection attacks.</span></span> <span data-ttu-id="8fe4f-115">これらの攻撃の目的は、HTML を表示するか、クライアントスクリプトを実行してユーザーをハッカーのサイトにリダイレクトすることであるかどうかにかかわらず、スクリプトインジェクション攻撃は、Web 開発者が対処する必要がある問題です。</span><span class="sxs-lookup"><span data-stu-id="8fe4f-115">Whether the purpose of these attacks is to deface the site by displaying HTML, or to potentially execute client script to redirect the user to a hacker's site, script injection attacks are a problem that Web developers must contend with.</span></span>

<span data-ttu-id="8fe4f-116">スクリプトインジェクション攻撃は、ASP.NET、ASP、またはその他の web 開発テクノロジを使用しているかどうかに関係なく、すべての web 開発者にとって重要です。</span><span class="sxs-lookup"><span data-stu-id="8fe4f-116">Script injection attacks are a concern of all web developers, whether they are using ASP.NET, ASP, or other web development technologies.</span></span>

<span data-ttu-id="8fe4f-117">ASP.NET 要求の検証機能では、開発者がコンテンツを許可しない限り、エンコードされていない HTML コンテンツをサーバーで処理できないようにすることで、これらの攻撃を事前に防ぐことができます。</span><span class="sxs-lookup"><span data-stu-id="8fe4f-117">The ASP.NET request validation feature proactively prevents these attacks by not allowing unencoded HTML content to be processed by the server unless the developer decides to allow that content.</span></span>

## <a name="what-to-expect-error-page"></a><span data-ttu-id="8fe4f-118">期待される内容: エラーページ</span><span class="sxs-lookup"><span data-stu-id="8fe4f-118">What to expect: Error Page</span></span>

<span data-ttu-id="8fe4f-119">次のスクリーンショットは、サンプルの ASP.NET コードを示しています。</span><span class="sxs-lookup"><span data-stu-id="8fe4f-119">The screen shot below shows some sample ASP.NET code:</span></span>

![](request-validation/_static/image1.png)

<span data-ttu-id="8fe4f-120">このコードを実行すると、テキストボックスにテキストを入力し、ボタンをクリックして、ラベルコントロールにテキストを表示できる単純なページが生成されます。</span><span class="sxs-lookup"><span data-stu-id="8fe4f-120">Running this code results in a simple page that allows you to enter some text in the textbox, click the button, and display the text in the label control:</span></span>

![](request-validation/_static/image2.png)

<span data-ttu-id="8fe4f-121">ただし、`<script>alert("hello!")</script>` の入力や送信などの JavaScript は、次のような例外が発生します。</span><span class="sxs-lookup"><span data-stu-id="8fe4f-121">However, were JavaScript, such as `<script>alert("hello!")</script>` to be entered and submitted we would get an exception:</span></span>

![](request-validation/_static/image3.png)

<span data-ttu-id="8fe4f-122">エラーメッセージは、"危険な要求が発生した可能性がある" という値が検出されたことを示し、何が発生したか、および動作を変更する方法を説明する詳細情報を提供します。</span><span class="sxs-lookup"><span data-stu-id="8fe4f-122">The error message states that a 'potentially dangerous Request.Form value was detected' and provides more details in the description as to exactly what occurred and how to change the behavior.</span></span> <span data-ttu-id="8fe4f-123">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="8fe4f-123">For example:</span></span>

<span data-ttu-id="8fe4f-124">要求の検証で、危険な可能性のあるクライアント入力値が検出され、要求の処理が中止されました。</span><span class="sxs-lookup"><span data-stu-id="8fe4f-124">Request validation has detected a potentially dangerous client input value, and processing of the request has been aborted.</span></span> <span data-ttu-id="8fe4f-125">この値は、クロスサイトスクリプティング攻撃など、アプリケーションのセキュリティを侵害しようとしている可能性があります。</span><span class="sxs-lookup"><span data-stu-id="8fe4f-125">This value may indicate an attempt to compromise the security of your application, such as a cross-site scripting attack.</span></span> <span data-ttu-id="8fe4f-126">ページディレクティブまたは構成セクションで `validateRequest=false` を設定することによって、要求の検証を無効にすることができます。</span><span class="sxs-lookup"><span data-stu-id="8fe4f-126">You can disable request validation by setting `validateRequest=false` in the Page directive or in the configuration section.</span></span> <span data-ttu-id="8fe4f-127">ただし、この場合は、アプリケーションですべての入力を明示的に確認することを強くお勧めします。</span><span class="sxs-lookup"><span data-stu-id="8fe4f-127">However, it is strongly recommended that your application explicitly check all inputs in this case.</span></span>

## <a name="disabling-request-validation-on-a-page"></a><span data-ttu-id="8fe4f-128">ページでの要求の検証を無効にする</span><span class="sxs-lookup"><span data-stu-id="8fe4f-128">Disabling request validation on a page</span></span>

<span data-ttu-id="8fe4f-129">ページでの要求の検証を無効にするには、Page ディレクティブの `validateRequest` 属性を `false`に設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8fe4f-129">To disable request validation on a page you must set the `validateRequest` attribute of the Page directive to `false`:</span></span>

[!code-aspx[Main](request-validation/samples/sample1.aspx)]

> [!CAUTION]
> <span data-ttu-id="8fe4f-130">要求の検証が無効になっている場合は、ページにコンテンツを送信できます。コンテンツが適切にエンコードまたは処理されていることを確認するのは、ページ開発者の責任です。</span><span class="sxs-lookup"><span data-stu-id="8fe4f-130">When request validation is disabled, content can be submitted to a page; it is the responsibility of the page developer to ensure that content is properly encoded or processed.</span></span>

## <a name="disabling-request-validation-for-your-application"></a><span data-ttu-id="8fe4f-131">アプリケーションの要求の検証を無効にしています</span><span class="sxs-lookup"><span data-stu-id="8fe4f-131">Disabling request validation for your application</span></span>

<span data-ttu-id="8fe4f-132">アプリケーションの要求の検証を無効にするには、アプリケーションの web.config ファイルを変更または作成し、`<pages />` セクションの validateRequest 属性を `false`に設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8fe4f-132">To disable request validation for your application, you must modify or create a Web.config file for your application and set the validateRequest attribute of the `<pages />` section to `false`:</span></span>

[!code-xml[Main](request-validation/samples/sample2.xml)]

<span data-ttu-id="8fe4f-133">サーバー上のすべてのアプリケーションに対する要求の検証を無効にする場合は、machine.config ファイルに変更を加えることができます。</span><span class="sxs-lookup"><span data-stu-id="8fe4f-133">If you wish to disable request validation for all applications on your server, you can make this modification to your Machine.config file.</span></span>

> [!CAUTION]
> <span data-ttu-id="8fe4f-134">要求の検証が無効になっている場合、コンテンツをアプリケーションに送信できます。コンテンツが適切にエンコードまたは処理されていることを確認するのは、アプリケーション開発者の責任です。</span><span class="sxs-lookup"><span data-stu-id="8fe4f-134">When request validation is disabled, content can be submitted to your application; it is the responsibility of the application developer to ensure that content is properly encoded or processed.</span></span>

<span data-ttu-id="8fe4f-135">次のコードは、要求の検証を無効にするように変更されています。</span><span class="sxs-lookup"><span data-stu-id="8fe4f-135">The code below is modified to turn off request validation:</span></span>

![](request-validation/_static/image4.png)

<span data-ttu-id="8fe4f-136">ここで、次の JavaScript がテキストボックスに入力された場合 `<script>alert("hello!")</script>` 結果は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="8fe4f-136">Now if the following JavaScript was entered into the textbox `<script>alert("hello!")</script>` the result would be:</span></span>

![](request-validation/_static/image5.png)

<span data-ttu-id="8fe4f-137">これが行われないようにするには、要求の検証を無効にして、コンテンツを HTML エンコードする必要があります。</span><span class="sxs-lookup"><span data-stu-id="8fe4f-137">To prevent this from happening, with request validation turned off, we need to HTML encode the content.</span></span>

## <a name="how-to-html-encode-content"></a><span data-ttu-id="8fe4f-138">方法: コンテンツを HTML エンコードする</span><span class="sxs-lookup"><span data-stu-id="8fe4f-138">How to HTML encode content</span></span>

<span data-ttu-id="8fe4f-139">要求の検証を無効にしている場合は、今後使用するために保存されるコンテンツを HTML エンコードすることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="8fe4f-139">If you have disabled request validation, it is good practice to HTML-encode content that will be stored for future use.</span></span> <span data-ttu-id="8fe4f-140">HTML エンコードでは、任意の '&lt;' または '&gt;' が、他のいくつかのシンボルと共に、対応する HTML エンコードされた表現に自動的に置き換えられます。</span><span class="sxs-lookup"><span data-stu-id="8fe4f-140">HTML encoding will automatically replace any ‘&lt;' or ‘&gt;' (together with several other symbols) with their corresponding HTML encoded representation.</span></span> <span data-ttu-id="8fe4f-141">たとえば、'&lt;' は '&amp;lt; ' に置き換えられ、'&gt;' は '&amp;gt; ' に置き換えられます。</span><span class="sxs-lookup"><span data-stu-id="8fe4f-141">For example, ‘&lt;' is replaced by ‘&amp;lt;' and ‘&gt;' is replaced by ‘&amp;gt;'.</span></span> <span data-ttu-id="8fe4f-142">ブラウザーでは、これらの特殊なコードを使用して '&lt;' または '&gt;' がブラウザーに表示されます。</span><span class="sxs-lookup"><span data-stu-id="8fe4f-142">Browsers use these special codes to display the ‘&lt;' or ‘&gt;' in the browser.</span></span>

<span data-ttu-id="8fe4f-143">コンテンツは、`Server.HtmlEncode(string)` API を使用して、サーバー上で簡単に HTML エンコードできます。</span><span class="sxs-lookup"><span data-stu-id="8fe4f-143">Content can be easily HTML-encoded on the server using the `Server.HtmlEncode(string)` API.</span></span> <span data-ttu-id="8fe4f-144">また、コンテンツは簡単に HTML デコードできます。つまり、`Server.HtmlDecode(string)` メソッドを使用して標準 HTML に戻されます。</span><span class="sxs-lookup"><span data-stu-id="8fe4f-144">Content can also be easily HTML-decoded, that is, reverted back to standard HTML using the `Server.HtmlDecode(string)` method.</span></span>

![](request-validation/_static/image6.png)

<span data-ttu-id="8fe4f-145">結果は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="8fe4f-145">Resulting in:</span></span>

![](request-validation/_static/image7.png)
