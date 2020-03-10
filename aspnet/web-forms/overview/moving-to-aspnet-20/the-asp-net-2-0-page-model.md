---
uid: web-forms/overview/moving-to-aspnet-20/the-asp-net-2-0-page-model
title: ASP.NET 2.0 ページモデル |Microsoft Docs
author: microsoft
description: ASP.NET 1.x では、開発者はインラインコードモデルとコードビハインドコードモデルのどちらかを選択できました。 分離コードを実装するには、Src attr...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: af4575a3-0ae3-4638-ba4d-218fad7a1642
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/the-asp-net-2-0-page-model
msc.type: authoredcontent
ms.openlocfilehash: bcb71b2b5a484e8756406867e08e8aa699a9024d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78440710"
---
# <a name="the-aspnet-20-page-model"></a><span data-ttu-id="dd16a-104">ASP.NET 2.0 ページモデル</span><span class="sxs-lookup"><span data-stu-id="dd16a-104">The ASP.NET 2.0 Page Model</span></span>

<span data-ttu-id="dd16a-105">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="dd16a-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="dd16a-106">ASP.NET 1.x では、開発者はインラインコードモデルとコードビハインドコードモデルのどちらかを選択できました。</span><span class="sxs-lookup"><span data-stu-id="dd16a-106">In ASP.NET 1.x, developers had a choice between an inline code model and a code-behind code model.</span></span> <span data-ttu-id="dd16a-107">分離コードは、@Page ディレクティブの Src 属性または CodeBehind 属性を使用して実装できます。</span><span class="sxs-lookup"><span data-stu-id="dd16a-107">Code-behind could be implemented using either the Src attribute or the CodeBehind attribute of the @Page directive.</span></span> <span data-ttu-id="dd16a-108">ASP.NET 2.0 では、開発者はインラインコードと分離コードのどちらかを選択できますが、分離コードモデルは大幅に拡張されています。</span><span class="sxs-lookup"><span data-stu-id="dd16a-108">In ASP.NET 2.0, developers still have a choice between inline code and code-behind, but there have been significant enhancements to the code-behind model.</span></span>

<span data-ttu-id="dd16a-109">ASP.NET 1.x では、開発者はインラインコードモデルとコードビハインドコードモデルのどちらかを選択できました。</span><span class="sxs-lookup"><span data-stu-id="dd16a-109">In ASP.NET 1.x, developers had a choice between an inline code model and a code-behind code model.</span></span> <span data-ttu-id="dd16a-110">分離コードは、@Page ディレクティブの Src 属性または CodeBehind 属性を使用して実装できます。</span><span class="sxs-lookup"><span data-stu-id="dd16a-110">Code-behind could be implemented using either the Src attribute or the CodeBehind attribute of the @Page directive.</span></span> <span data-ttu-id="dd16a-111">ASP.NET 2.0 では、開発者はインラインコードと分離コードのどちらかを選択できますが、分離コードモデルは大幅に拡張されています。</span><span class="sxs-lookup"><span data-stu-id="dd16a-111">In ASP.NET 2.0, developers still have a choice between inline code and code-behind, but there have been significant enhancements to the code-behind model.</span></span>

## <a name="improvements-in-the-code-behind-model"></a><span data-ttu-id="dd16a-112">分離コードモデルの機能強化</span><span class="sxs-lookup"><span data-stu-id="dd16a-112">Improvements in the Code-Behind Model</span></span>

<span data-ttu-id="dd16a-113">ASP.NET 2.0 の分離コードモデルの変更を完全に理解するために、ASP.NET 1.x に存在するモデルをすばやく確認することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="dd16a-113">In order to fully understand the changes in the code-behind model in ASP.NET 2.0, its best to quickly review the model as it existed in ASP.NET 1.x.</span></span>

## <a name="the-code-behind-model-in-aspnet-1x"></a><span data-ttu-id="dd16a-114">ASP.NET 1.x の分離コードモデル</span><span class="sxs-lookup"><span data-stu-id="dd16a-114">The Code-Behind Model in ASP.NET 1.x</span></span>

<span data-ttu-id="dd16a-115">ASP.NET 1.x では、分離コードモデルは ASPX ファイル (Web フォーム) とプログラミングコードを含む分離コードファイルで事前に記述されています。</span><span class="sxs-lookup"><span data-stu-id="dd16a-115">In ASP.NET 1.x, the code-behind model consisted of an ASPX file (the Webform) and a code-behind file containing programming code.</span></span> <span data-ttu-id="dd16a-116">2つのファイルは、ASPX ファイルの @Page ディレクティブを使用して接続されていました。</span><span class="sxs-lookup"><span data-stu-id="dd16a-116">The two files were connected using the @Page directive in the ASPX file.</span></span> <span data-ttu-id="dd16a-117">ASPX ページの各コントロールには、分離コードファイル内の対応する宣言がインスタンス変数として含まれていました。</span><span class="sxs-lookup"><span data-stu-id="dd16a-117">Each control on the ASPX page had a corresponding declaration in the code-behind file as an instance variable.</span></span> <span data-ttu-id="dd16a-118">分離コードファイルには、Visual Studio デザイナーに必要なイベントバインドおよび生成されたコードのコードも含まれています。</span><span class="sxs-lookup"><span data-stu-id="dd16a-118">The code-behind file also contained code for event binding and generated code necessary for the Visual Studio designer.</span></span> <span data-ttu-id="dd16a-119">このモデルは非常にうまく機能しましたが、ASPX ページのすべての ASP.NET 要素が分離コードファイル内に対応するコードを必要としていたため、コードとコンテンツの分離は実際には行われませんでした。</span><span class="sxs-lookup"><span data-stu-id="dd16a-119">This model worked fairly well, but because every ASP.NET element in the ASPX page required corresponding code in the code-behind file, there was no true separation of code and content.</span></span> <span data-ttu-id="dd16a-120">たとえば、デザイナーが Visual Studio IDE の外部にある ASPX ファイルに新しいサーバーコントロールを追加した場合、分離コードファイル内にそのコントロールの宣言がないため、アプリケーションは中断されます。</span><span class="sxs-lookup"><span data-stu-id="dd16a-120">For example, if a designer added a new server control to an ASPX file outside of the Visual Studio IDE, the application would break due to the absence of a declaration for that control in the code-behind file.</span></span>

## <a name="the-code-behind-model-in-aspnet-20"></a><span data-ttu-id="dd16a-121">ASP.NET 2.0 の分離コードモデル</span><span class="sxs-lookup"><span data-stu-id="dd16a-121">The Code-Behind Model in ASP.NET 2.0</span></span>

<span data-ttu-id="dd16a-122">このモデルでは、ASP.NET 2.0 が大幅に改善されています。</span><span class="sxs-lookup"><span data-stu-id="dd16a-122">ASP.NET 2.0 greatly improves upon this model.</span></span> <span data-ttu-id="dd16a-123">ASP.NET 2.0 では、ASP.NET 2.0 で提供される新しい*部分クラス*を使用して分離コードが実装されます。</span><span class="sxs-lookup"><span data-stu-id="dd16a-123">In ASP.NET 2.0, code-behind is implemented using the new *partial classes* provided in ASP.NET 2.0.</span></span> <span data-ttu-id="dd16a-124">ASP.NET 2.0 の分離コードクラスは部分クラスとして定義されます。これは、クラス定義の一部だけが含まれることを意味します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-124">The code-behind class in ASP.NET 2.0 is defined as a partial class meaning that it contains only part of the class definition.</span></span> <span data-ttu-id="dd16a-125">クラス定義の残りの部分は、実行時に ASPX ページを使用して ASP.NET 2.0 によって動的に生成されるか、Web サイトがプリコンパイルされます。</span><span class="sxs-lookup"><span data-stu-id="dd16a-125">The remaining part of the class definition is dynamically generated by ASP.NET 2.0 using the ASPX page at runtime or when the Web site is precompiled.</span></span> <span data-ttu-id="dd16a-126">分離コードファイルと ASPX ページ間のリンクは、引き続き @ Page ディレクティブを使用して確立されます。</span><span class="sxs-lookup"><span data-stu-id="dd16a-126">The link between the code-behind file and the ASPX page is still established using the @ Page directive.</span></span> <span data-ttu-id="dd16a-127">ただし、CodeBehind 属性または Src 属性の代わりに、ASP.NET 2.0 では、CodeFile 属性が使用されるようになりました。</span><span class="sxs-lookup"><span data-stu-id="dd16a-127">However, instead of a CodeBehind or Src attribute, ASP.NET 2.0 now uses the CodeFile attribute.</span></span> <span data-ttu-id="dd16a-128">継承属性は、ページのクラス名を指定するためにも使用されます。</span><span class="sxs-lookup"><span data-stu-id="dd16a-128">The Inherits attribute is also used to specify the class name for the page.</span></span>

<span data-ttu-id="dd16a-129">一般的な @ Page ディレクティブは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="dd16a-129">A typical @ Page directive might look like this:</span></span>

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample1.aspx)]

<span data-ttu-id="dd16a-130">ASP.NET 2.0 分離コードファイルの一般的なクラス定義は、次のようになります。</span><span class="sxs-lookup"><span data-stu-id="dd16a-130">A typical class definition in an ASP.NET 2.0 code-behind file might look like this:</span></span>

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample2.cs)]

> [!NOTE]
> <span data-ttu-id="dd16a-131">C#と Visual Basic は、現在部分クラスをサポートしている唯一のマネージ言語です。</span><span class="sxs-lookup"><span data-stu-id="dd16a-131">C# and Visual Basic are the only managed languages that currently support partial classes.</span></span> <span data-ttu-id="dd16a-132">そのため、J# を使用する開発者は、ASP.NET 2.0 で分離コードモデルを使用することはできません。</span><span class="sxs-lookup"><span data-stu-id="dd16a-132">Therefore, developers using J# will not be able to use the code-behind model in ASP.NET 2.0.</span></span>

<span data-ttu-id="dd16a-133">新しいモデルでは、コードビハインドモデルが拡張されます。これは、開発者が作成したコードのみを含むコードファイルがあるためです。</span><span class="sxs-lookup"><span data-stu-id="dd16a-133">The new model enhances the code-behind model because developers will now have code files that contain only the code that they have created.</span></span> <span data-ttu-id="dd16a-134">また、分離コードファイルにインスタンス変数宣言がないため、コードとコンテンツの真の分離も提供します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-134">It also provides for a true separation of code and content because there are no instance variable declarations in the code-behind file.</span></span>

> [!NOTE]
> <span data-ttu-id="dd16a-135">ASPX ページの部分クラスはイベントバインドが行われる場所であるため、Visual Basic 開発者は、分離コードで Handles キーワードを使用してイベントをバインドすることで、わずかなパフォーマンスの向上を実感できます。</span><span class="sxs-lookup"><span data-stu-id="dd16a-135">Because the partial class for the ASPX page is where event binding takes place, Visual Basic developers can realize a slight performance increase by using the Handles keyword in code-behind to bind events.</span></span> <span data-ttu-id="dd16a-136">C#には同等のキーワードがありません。</span><span class="sxs-lookup"><span data-stu-id="dd16a-136">C# has no equivalent keyword.</span></span>

## <a name="new--page-directive-attributes"></a><span data-ttu-id="dd16a-137">新しい @ Page ディレクティブ属性</span><span class="sxs-lookup"><span data-stu-id="dd16a-137">New @ Page Directive Attributes</span></span>

<span data-ttu-id="dd16a-138">ASP.NET 2.0 では、@ Page ディレクティブに多くの新しい属性が追加されます。</span><span class="sxs-lookup"><span data-stu-id="dd16a-138">ASP.NET 2.0 adds many new attributes to the @ Page directive.</span></span> <span data-ttu-id="dd16a-139">ASP.NET 2.0 では、次の属性が追加されています。</span><span class="sxs-lookup"><span data-stu-id="dd16a-139">The following attributes are new in ASP.NET 2.0.</span></span>

## <a name="async"></a><span data-ttu-id="dd16a-140">非同期</span><span class="sxs-lookup"><span data-stu-id="dd16a-140">Async</span></span>

<span data-ttu-id="dd16a-141">Async 属性を使用すると、ページを非同期に実行するように構成できます。</span><span class="sxs-lookup"><span data-stu-id="dd16a-141">The Async attribute allows you to configure page to be executed asynchronously.</span></span> <span data-ttu-id="dd16a-142">非同期ページについては、このモジュールで後ほど説明します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-142">Well cover asynchronous pages later in this module.</span></span>

## <a name="asynctimeout"></a><span data-ttu-id="dd16a-143">AsyncTimeout</span><span class="sxs-lookup"><span data-stu-id="dd16a-143">AsyncTimeout</span></span>

<span data-ttu-id="dd16a-144">非同期ページのタイムアウトを指定しました。</span><span class="sxs-lookup"><span data-stu-id="dd16a-144">Specified the timeout for asynchronous pages.</span></span> <span data-ttu-id="dd16a-145">既定値は45秒です。</span><span class="sxs-lookup"><span data-stu-id="dd16a-145">The default is 45 seconds.</span></span>

## <a name="codefile"></a><span data-ttu-id="dd16a-146">CodeFile</span><span class="sxs-lookup"><span data-stu-id="dd16a-146">CodeFile</span></span>

<span data-ttu-id="dd16a-147">CodeFile 属性は、Visual Studio 2002/2003 の CodeBehind 属性に代わるものです。</span><span class="sxs-lookup"><span data-stu-id="dd16a-147">The CodeFile attribute is the replacement for the CodeBehind attribute in Visual Studio 2002/2003.</span></span>

### <a name="codefilebaseclass"></a><span data-ttu-id="dd16a-148">CodeFileBaseClass</span><span class="sxs-lookup"><span data-stu-id="dd16a-148">CodeFileBaseClass</span></span>

<span data-ttu-id="dd16a-149">CodeFileBaseClass 属性は、1つの基底クラスから複数のページを派生させる場合に使用します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-149">The CodeFileBaseClass attribute is used in cases where you want multiple pages to derive from a single base class.</span></span> <span data-ttu-id="dd16a-150">ASP.NET では部分クラスが実装されているため、この属性がないと、共有共通フィールドを使用する基本クラスは、ASPX ページで宣言されたコントロールを参照するために適切に機能しません。これは、ASP.NET コンパイルエンジンがページ内のコントロールに基づいて新しいメンバーを自動的に作成するためです。</span><span class="sxs-lookup"><span data-stu-id="dd16a-150">Because of the implementation of partial classes in ASP.NET, without this attribute, a base class that uses shared common fields to reference controls declared in an ASPX page would not work properly because ASP.NETs compilation engine will automatically create new members based on controls in the page.</span></span> <span data-ttu-id="dd16a-151">このため、ASP.NET の2つ以上のページに共通の基本クラスが必要な場合は、CodeFileBaseClass 属性で基底クラスを指定し、その基底クラスから各 pages クラスを派生させる必要があります。</span><span class="sxs-lookup"><span data-stu-id="dd16a-151">Therefore, if you want a common base class for two or more pages in ASP.NET, you will need to define specify your base class in the CodeFileBaseClass attribute and then derive each pages class from that base class.</span></span> <span data-ttu-id="dd16a-152">この属性を使用する場合は、CodeFile 属性も必要です。</span><span class="sxs-lookup"><span data-stu-id="dd16a-152">The CodeFile attribute is also required when this attribute is used.</span></span>

## <a name="compilationmode"></a><span data-ttu-id="dd16a-153">CompilationMode</span><span class="sxs-lookup"><span data-stu-id="dd16a-153">CompilationMode</span></span>

<span data-ttu-id="dd16a-154">この属性を使用すると、ASPX ページの CompilationMode プロパティを設定できます。</span><span class="sxs-lookup"><span data-stu-id="dd16a-154">This attribute allows you to set the CompilationMode property of the ASPX page.</span></span> <span data-ttu-id="dd16a-155">CompilationMode プロパティは、値**Always**、 **Auto**、および**Never**を含む列挙体です。</span><span class="sxs-lookup"><span data-stu-id="dd16a-155">The CompilationMode property is an enumeration containing the values **Always**, **Auto**, and **Never**.</span></span> <span data-ttu-id="dd16a-156">既定値は**常に**です。</span><span class="sxs-lookup"><span data-stu-id="dd16a-156">The default is **Always**.</span></span> <span data-ttu-id="dd16a-157">**自動**設定では、可能であれば、ASP.NET がページを動的にコンパイルできないようにします。</span><span class="sxs-lookup"><span data-stu-id="dd16a-157">The **Auto** setting will prevent ASP.NET from dynamically compiling the page if possible.</span></span> <span data-ttu-id="dd16a-158">動的コンパイルからページを除外すると、パフォーマンスが向上します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-158">Excluding pages from dynamic compilation increases performance.</span></span> <span data-ttu-id="dd16a-159">ただし、除外されたページにコンパイルする必要があるコードが含まれている場合、ページが参照されるとエラーがスローされます。</span><span class="sxs-lookup"><span data-stu-id="dd16a-159">However, if a page that is excluded contains that code that must be compiled, an error will be thrown when the page is browsed.</span></span>

## <a name="enableeventvalidation"></a><span data-ttu-id="dd16a-160">EnableEventValidation</span><span class="sxs-lookup"><span data-stu-id="dd16a-160">EnableEventValidation</span></span>

<span data-ttu-id="dd16a-161">この属性は、ポストバックイベントとコールバックイベントを検証するかどうかを指定します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-161">This attribute specifies whether or not postback and callback events are validated.</span></span> <span data-ttu-id="dd16a-162">これが有効になっている場合、ポストバックまたはコールバックイベントの引数は、最初に表示されたサーバーコントロールから生成されたものであることを確認するためにチェックされます。</span><span class="sxs-lookup"><span data-stu-id="dd16a-162">When this is enabled, arguments to postback or callback events are checked to ensure that they originated from the server control that originally rendered them.</span></span>

## <a name="enabletheming"></a><span data-ttu-id="dd16a-163">EnableTheming</span><span class="sxs-lookup"><span data-stu-id="dd16a-163">EnableTheming</span></span>

<span data-ttu-id="dd16a-164">この属性は、ページで ASP.NET テーマを使用するかどうかを指定します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-164">This attribute specifies whether or not ASP.NET themes are used on a page.</span></span> <span data-ttu-id="dd16a-165">既定値は **false** です。</span><span class="sxs-lookup"><span data-stu-id="dd16a-165">The default is **false**.</span></span> <span data-ttu-id="dd16a-166">ASP.NET のテーマについては、[モジュール 10](profiles-themes-and-web-parts.md)で説明します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-166">ASP.NET themes are covered in [Module 10](profiles-themes-and-web-parts.md).</span></span>

## <a name="linepragmas"></a><span data-ttu-id="dd16a-167">LinePragmas</span><span class="sxs-lookup"><span data-stu-id="dd16a-167">LinePragmas</span></span>

<span data-ttu-id="dd16a-168">この属性は、コンパイル時に行プラグマを追加する必要があるかどうかを指定します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-168">This attribute specifies whether line pragmas should be added during compilation.</span></span> <span data-ttu-id="dd16a-169">行プラグマは、コードの特定のセクションをマークするためにデバッガーによって使用されるオプションです。</span><span class="sxs-lookup"><span data-stu-id="dd16a-169">Line pragmas are options used by debuggers to mark specific sections of code.</span></span>

## <a name="maintainscrollpositiononpostback"></a><span data-ttu-id="dd16a-170">MaintainScrollPositionOnPostback</span><span class="sxs-lookup"><span data-stu-id="dd16a-170">MaintainScrollPositionOnPostback</span></span>

<span data-ttu-id="dd16a-171">この属性は、ポストバック間のスクロール位置を維持するために、ページに JavaScript を挿入するかどうかを指定します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-171">This attribute specifies whether or not JavaScript is injected into the page in order to maintain scroll position between postbacks.</span></span> <span data-ttu-id="dd16a-172">既定では、この属性は**false**です。</span><span class="sxs-lookup"><span data-stu-id="dd16a-172">This attribute is **false** by default.</span></span>

<span data-ttu-id="dd16a-173">この属性が**true**の場合、ASP.NET は次のような &lt;スクリプト&gt; ブロックをポストバックに追加します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-173">When this attribute is **true**, ASP.NET will add a &lt;script&gt; block on postback that looks like this:</span></span>

[!code-html[Main](the-asp-net-2-0-page-model/samples/sample3.html)]

<span data-ttu-id="dd16a-174">このスクリプトブロックの src は Webresource.axd です。</span><span class="sxs-lookup"><span data-stu-id="dd16a-174">Note that the src for this script block is WebResource.axd.</span></span> <span data-ttu-id="dd16a-175">このリソースは物理パスではありません。</span><span class="sxs-lookup"><span data-stu-id="dd16a-175">This resource is not a physical path.</span></span> <span data-ttu-id="dd16a-176">このスクリプトが要求されると、ASP.NET はスクリプトを動的に構築します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-176">When this script is requested, ASP.NET dynamically builds the script.</span></span>

### <a name="masterpagefile"></a><span data-ttu-id="dd16a-177">MasterPageFile</span><span class="sxs-lookup"><span data-stu-id="dd16a-177">MasterPageFile</span></span>

<span data-ttu-id="dd16a-178">この属性は、現在のページのマスターページファイルを指定します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-178">This attribute specifies the master page file for the current page.</span></span> <span data-ttu-id="dd16a-179">相対パスと絶対パスのどちらでも構いません。</span><span class="sxs-lookup"><span data-stu-id="dd16a-179">The path can be relative or absolute.</span></span> <span data-ttu-id="dd16a-180">マスターページについては、[モジュール 4](master-pages.md)で説明します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-180">Master pages are covered in [Module 4](master-pages.md).</span></span>

## <a name="stylesheettheme"></a><span data-ttu-id="dd16a-181">StyleSheetTheme</span><span class="sxs-lookup"><span data-stu-id="dd16a-181">StyleSheetTheme</span></span>

<span data-ttu-id="dd16a-182">この属性を使用すると、ASP.NET 2.0 テーマによって定義されたユーザーインターフェイスの外観プロパティをオーバーライドできます。</span><span class="sxs-lookup"><span data-stu-id="dd16a-182">This attribute allows you to override user-interface appearance properties defined by an ASP.NET 2.0 theme.</span></span> <span data-ttu-id="dd16a-183">テーマについては、[モジュール 10](profiles-themes-and-web-parts.md)で説明します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-183">Themes are covered in [Module 10](profiles-themes-and-web-parts.md).</span></span>

## <a name="theme"></a><span data-ttu-id="dd16a-184">テーマ</span><span class="sxs-lookup"><span data-stu-id="dd16a-184">Theme</span></span>

<span data-ttu-id="dd16a-185">ページのテーマを指定します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-185">Specifies the theme for the page.</span></span> <span data-ttu-id="dd16a-186">StyleSheetTheme 属性に値が指定されていない場合、ページ上のコントロールに適用されるすべてのスタイルが Theme 属性によってオーバーライドされます。</span><span class="sxs-lookup"><span data-stu-id="dd16a-186">If a value is not specified for the StyleSheetTheme attribute, the Theme attribute overrides all styles applied to controls on the page.</span></span>

## <a name="title"></a><span data-ttu-id="dd16a-187">タイトル</span><span class="sxs-lookup"><span data-stu-id="dd16a-187">Title</span></span>

<span data-ttu-id="dd16a-188">ページのタイトルを設定します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-188">Sets the title for the page.</span></span> <span data-ttu-id="dd16a-189">ここで指定した値は、表示されるページの &lt;title&gt; 要素に表示されます。</span><span class="sxs-lookup"><span data-stu-id="dd16a-189">The value specified here will appear in the &lt;title&gt; element of the rendered page.</span></span>

### <a name="viewstateencryptionmode"></a><span data-ttu-id="dd16a-190">ViewStateEncryptionMode</span><span class="sxs-lookup"><span data-stu-id="dd16a-190">ViewStateEncryptionMode</span></span>

<span data-ttu-id="dd16a-191">ViewStateEncryptionMode 列挙体の値を設定します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-191">Sets the value for the ViewStateEncryptionMode enumeration.</span></span> <span data-ttu-id="dd16a-192">使用できる値は、**常**に、 **Auto**、および**Never**です。</span><span class="sxs-lookup"><span data-stu-id="dd16a-192">The available values are **Always**, **Auto**, and **Never**.</span></span> <span data-ttu-id="dd16a-193">既定値は**Auto**です。この属性が**Auto**の値に設定されている場合、viewstate は暗号化されます。これは、 **RegisterRequiresViewStateEncryption**メソッドを呼び出すことによってコントロールが要求します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-193">The default value is **Auto**. When this attribute is set to a value of **Auto**, viewstate is encrypted is a control requests it by calling the **RegisterRequiresViewStateEncryption** method.</span></span>

## <a name="setting-public-property-values-via-the--page-directive"></a><span data-ttu-id="dd16a-194">@ Page ディレクティブを使用したパブリックプロパティの値の設定</span><span class="sxs-lookup"><span data-stu-id="dd16a-194">Setting Public Property Values via the @ Page Directive</span></span>

<span data-ttu-id="dd16a-195">ASP.NET 2.0 の @ Page ディレクティブのもう1つの新機能は、基底クラスのパブリックプロパティの初期値を設定できることです。</span><span class="sxs-lookup"><span data-stu-id="dd16a-195">Another new capability of the @ Page directive in ASP.NET 2.0 is the ability to set the initial value of public properties of a base class.</span></span> <span data-ttu-id="dd16a-196">たとえば、基底クラスに**テキスト**と呼ばれるパブリックプロパティがあり、ページが読み込まれるときに**Hello**に初期化されるとします。</span><span class="sxs-lookup"><span data-stu-id="dd16a-196">Suppose, for example, that you have a public property called **SomeText** in your base class and you d like it to be initialized to **Hello** when a page is loaded.</span></span> <span data-ttu-id="dd16a-197">これは、次のように @ Page ディレクティブの値を設定するだけで実現できます。</span><span class="sxs-lookup"><span data-stu-id="dd16a-197">You can accomplish this by simply setting the value in the @ Page directive like so:</span></span>

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample4.aspx)]

<span data-ttu-id="dd16a-198">@ Page ディレクティブの**text**属性では、基底クラスのテキストプロパティの初期値が*Hello!* に設定されています。</span><span class="sxs-lookup"><span data-stu-id="dd16a-198">The **SomeText** attribute of the @ Page directive sets the initial value of the SomeText property in the base class to *Hello!*.</span></span> <span data-ttu-id="dd16a-199">次のビデオでは、@ Page ディレクティブを使用して基底クラスのパブリックプロパティの初期値を設定する方法を説明しています。</span><span class="sxs-lookup"><span data-stu-id="dd16a-199">The video below is a walkthrough of setting the initial value of a public property in a base class using the @ Page directive.</span></span>

![](the-asp-net-2-0-page-model/_static/image1.png)

[<span data-ttu-id="dd16a-200">全画面表示のビデオを開く</span><span class="sxs-lookup"><span data-stu-id="dd16a-200">Open Full-Screen Video</span></span>](the-asp-net-2-0-page-model/_static/setprop1.wmv)

## <a name="new-public-properties-of-the-page-class"></a><span data-ttu-id="dd16a-201">ページクラスの新しいパブリックプロパティ</span><span class="sxs-lookup"><span data-stu-id="dd16a-201">New Public Properties of the Page Class</span></span>

<span data-ttu-id="dd16a-202">ASP.NET 2.0 では、次のパブリックプロパティが追加されています。</span><span class="sxs-lookup"><span data-stu-id="dd16a-202">The following public properties are new in ASP.NET 2.0.</span></span>

## <a name="apprelativetemplatesourcedirectory"></a><span data-ttu-id="dd16a-203">AppRelativeTemplateSourceDirectory</span><span class="sxs-lookup"><span data-stu-id="dd16a-203">AppRelativeTemplateSourceDirectory</span></span>

<span data-ttu-id="dd16a-204">ページまたはコントロールへのアプリケーション相対パスを返します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-204">Returns the application-relative path to the page or control.</span></span> <span data-ttu-id="dd16a-205">たとえば、 http://app/folder/page.aspxにあるページの場合、プロパティは ~/folder/. を返します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-205">For example, for a page located at http://app/folder/page.aspx, the property returns ~/folder/.</span></span>

## <a name="apprelativevirtualpath"></a><span data-ttu-id="dd16a-206">AppRelativeVirtualPath</span><span class="sxs-lookup"><span data-stu-id="dd16a-206">AppRelativeVirtualPath</span></span>

<span data-ttu-id="dd16a-207">ページまたはコントロールへの相対仮想ディレクトリパスを返します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-207">Returns the relative virtual directory path to the page or control.</span></span> <span data-ttu-id="dd16a-208">たとえば、 http://app/folder/page.aspxにあるページの場合、プロパティは ~/folder/page.aspx. を返します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-208">For example for a page located at http://app/folder/page.aspx, the property returns ~/folder/page.aspx.</span></span>

## <a name="asynctimeout"></a><span data-ttu-id="dd16a-209">AsyncTimeout</span><span class="sxs-lookup"><span data-stu-id="dd16a-209">AsyncTimeout</span></span>

<span data-ttu-id="dd16a-210">非同期ページ処理に使用されるタイムアウトを取得または設定します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-210">Gets or sets the timeout used for asynchronous page handling.</span></span> <span data-ttu-id="dd16a-211">(非同期ページについては、このモジュールで後ほど説明します)。</span><span class="sxs-lookup"><span data-stu-id="dd16a-211">(Asynchronous pages will be covered later in this module.)</span></span>

## <a name="clientquerystring"></a><span data-ttu-id="dd16a-212">ClientQueryString</span><span class="sxs-lookup"><span data-stu-id="dd16a-212">ClientQueryString</span></span>

<span data-ttu-id="dd16a-213">要求された URL のクエリ文字列部分を返す読み取り専用のプロパティ。</span><span class="sxs-lookup"><span data-stu-id="dd16a-213">A read-only property that returns the query string portion of the requested URL.</span></span> <span data-ttu-id="dd16a-214">この値は、URL でエンコードされます。</span><span class="sxs-lookup"><span data-stu-id="dd16a-214">This value is URL encoded.</span></span> <span data-ttu-id="dd16a-215">設定クラスの UrlDecode メソッドを使用してデコードできます。</span><span class="sxs-lookup"><span data-stu-id="dd16a-215">You can use the UrlDecode method of the HttpServerUtility class to decode it.</span></span>

## <a name="clientscript"></a><span data-ttu-id="dd16a-216">ClientScript</span><span class="sxs-lookup"><span data-stu-id="dd16a-216">ClientScript</span></span>

<span data-ttu-id="dd16a-217">このプロパティは、クライアント側スクリプトの ClientScriptManager を管理するために使用できる、オブジェクトを返します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-217">This property returns a ClientScriptManager object that can be used to manage ASP.NETs emission of client-side script.</span></span> <span data-ttu-id="dd16a-218">(ClientScriptManager クラスについては、このモジュールで後ほど説明します)。</span><span class="sxs-lookup"><span data-stu-id="dd16a-218">(The ClientScriptManager class is covered later in this module.)</span></span>

## <a name="enableeventvalidation"></a><span data-ttu-id="dd16a-219">EnableEventValidation</span><span class="sxs-lookup"><span data-stu-id="dd16a-219">EnableEventValidation</span></span>

<span data-ttu-id="dd16a-220">このプロパティは、ポストバックイベントとコールバックイベントに対してイベントの検証を有効にするかどうかを制御します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-220">This property controls whether or not event validation is enabled for postback and callback events.</span></span> <span data-ttu-id="dd16a-221">有効にすると、ポストバックまたはコールバックイベントの引数が検証され、最初に表示したサーバーコントロールからのものであることが確認されます。</span><span class="sxs-lookup"><span data-stu-id="dd16a-221">When enabled, arguments to postback or callback events are verified to ensure that they originated from the server control that originally rendered them.</span></span>

## <a name="enabletheming"></a><span data-ttu-id="dd16a-222">EnableTheming</span><span class="sxs-lookup"><span data-stu-id="dd16a-222">EnableTheming</span></span>

<span data-ttu-id="dd16a-223">このプロパティは、ASP.NET 2.0 テーマがページに適用されるかどうかを指定するブール値を取得または設定します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-223">This property gets or sets a Boolean that specifies whether or not an ASP.NET 2.0 theme applies to the page.</span></span>

## <a name="form"></a><span data-ttu-id="dd16a-224">Form</span><span class="sxs-lookup"><span data-stu-id="dd16a-224">Form</span></span>

<span data-ttu-id="dd16a-225">このプロパティは、ASPX ページの HTML フォームを HtmlForm オブジェクトとして返します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-225">This property returns the HTML form on the ASPX page as an HtmlForm object.</span></span>

## <a name="header"></a><span data-ttu-id="dd16a-226">ヘッダー</span><span class="sxs-lookup"><span data-stu-id="dd16a-226">Header</span></span>

<span data-ttu-id="dd16a-227">このプロパティは、ページヘッダーを含む HtmlHead オブジェクトへの参照を返します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-227">This property returns a reference to an HtmlHead object that contains the page header.</span></span> <span data-ttu-id="dd16a-228">返された HtmlHead オブジェクトを使用して、スタイルシートやメタタグなどを取得/設定できます。</span><span class="sxs-lookup"><span data-stu-id="dd16a-228">You can use the returned HtmlHead object to get/set style sheets, Meta tags, etc.</span></span>

## <a name="idseparator"></a><span data-ttu-id="dd16a-229">IdSeparator</span><span class="sxs-lookup"><span data-stu-id="dd16a-229">IdSeparator</span></span>

<span data-ttu-id="dd16a-230">この読み取り専用プロパティは、ASP.NET がページ上のコントロールの一意の ID を作成しているときに、コントロール識別子を区切るために使用される文字を取得します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-230">This read-only property gets the character that is used to separate control identifiers when ASP.NET is building a unique ID for controls on a page.</span></span> <span data-ttu-id="dd16a-231">コードから直接使用するためのものではありません。</span><span class="sxs-lookup"><span data-stu-id="dd16a-231">It is not intended to be used directly from your code.</span></span>

## <a name="isasync"></a><span data-ttu-id="dd16a-232">IsAsync</span><span class="sxs-lookup"><span data-stu-id="dd16a-232">IsAsync</span></span>

<span data-ttu-id="dd16a-233">このプロパティでは、非同期ページを使用できます。</span><span class="sxs-lookup"><span data-stu-id="dd16a-233">This property allows for asynchronous pages.</span></span> <span data-ttu-id="dd16a-234">非同期ページについては、このモジュールで後ほど説明します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-234">Asynchronous pages are discussed later in this module.</span></span>

## <a name="iscallback"></a><span data-ttu-id="dd16a-235">IsCallback</span><span class="sxs-lookup"><span data-stu-id="dd16a-235">IsCallback</span></span>

<span data-ttu-id="dd16a-236">この読み取り専用プロパティは、ページがコールバックの結果である場合に**true**を返します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-236">This read-only property returns **true** if the page is the result of a call back.</span></span> <span data-ttu-id="dd16a-237">コールバックについては、このモジュールで後ほど説明します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-237">Call backs are discussed later in this module.</span></span>

## <a name="iscrosspagepostback"></a><span data-ttu-id="dd16a-238">IsCrossPagePostBack</span><span class="sxs-lookup"><span data-stu-id="dd16a-238">IsCrossPagePostBack</span></span>

<span data-ttu-id="dd16a-239">この読み取り専用プロパティは、ページがクロスページポストバックの一部である場合に**true**を返します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-239">This read-only property returns **true** if the page is part of a cross-page postback.</span></span> <span data-ttu-id="dd16a-240">ページ間のポストバックについては、このモジュールで後ほど説明します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-240">Cross-page postbacks are covered later in this module.</span></span>

## <a name="items"></a><span data-ttu-id="dd16a-241">アイテム</span><span class="sxs-lookup"><span data-stu-id="dd16a-241">Items</span></span>

<span data-ttu-id="dd16a-242">ページコンテキストに格納されているすべてのオブジェクトを含む IDictionary インスタンスへの参照を返します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-242">Returns a reference to an IDictionary instance that contains all objects stored in the pages context.</span></span> <span data-ttu-id="dd16a-243">この IDictionary オブジェクトに項目を追加すると、コンテキストの有効期間全体にわたって使用できるようになります。</span><span class="sxs-lookup"><span data-stu-id="dd16a-243">You can add items to this IDictionary object and they will be available to you throughout the lifetime of the context.</span></span>

## <a name="maintainscrollpositiononpostback"></a><span data-ttu-id="dd16a-244">MaintainScrollPositionOnPostBack</span><span class="sxs-lookup"><span data-stu-id="dd16a-244">MaintainScrollPositionOnPostBack</span></span>

<span data-ttu-id="dd16a-245">このプロパティは、ポストバックが発生した後にブラウザーでページのスクロール位置を保持する JavaScript を ASP.NET が出力するかどうかを制御します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-245">This property controls whether or not ASP.NET emits JavaScript that maintains the pages scroll position in the browser after a postback occurs.</span></span> <span data-ttu-id="dd16a-246">(このプロパティの詳細については、このモジュールで既に説明しました)。</span><span class="sxs-lookup"><span data-stu-id="dd16a-246">(Details of this property were discussed earlier in this module.)</span></span>

## <a name="master"></a><span data-ttu-id="dd16a-247">Master</span><span class="sxs-lookup"><span data-stu-id="dd16a-247">Master</span></span>

<span data-ttu-id="dd16a-248">この読み取り専用プロパティは、マスターページが適用されているページのマスターインスタンスへの参照を返します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-248">This read-only property returns a reference to the MasterPage instance for a page to which a master page has been applied.</span></span>

## <a name="masterpagefile"></a><span data-ttu-id="dd16a-249">MasterPageFile</span><span class="sxs-lookup"><span data-stu-id="dd16a-249">MasterPageFile</span></span>

<span data-ttu-id="dd16a-250">ページのマスターページのファイル名を取得または設定します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-250">Gets or sets the master page filename for the page.</span></span> <span data-ttu-id="dd16a-251">このプロパティは、PreInit メソッドでのみ設定できます。</span><span class="sxs-lookup"><span data-stu-id="dd16a-251">This property can only be set in the PreInit method.</span></span>

## <a name="maxpagestatefieldlength"></a><span data-ttu-id="dd16a-252">MaxPageStateFieldLength</span><span class="sxs-lookup"><span data-stu-id="dd16a-252">MaxPageStateFieldLength</span></span>

<span data-ttu-id="dd16a-253">このプロパティは、ページの状態の最大長をバイト単位で取得または設定します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-253">This property gets or sets the maximum length for the pages state in bytes.</span></span> <span data-ttu-id="dd16a-254">プロパティが正の値に設定されている場合、ページビューステートは、指定されたバイト数を超えないように、複数の非表示フィールドに分割されます。</span><span class="sxs-lookup"><span data-stu-id="dd16a-254">If the property is set to a positive number, the pages view state will be broken up into multiple hidden fields so that it doesnt exceed the number of bytes specified.</span></span> <span data-ttu-id="dd16a-255">プロパティが負の数の場合、ビューステートはチャンクに分割されません。</span><span class="sxs-lookup"><span data-stu-id="dd16a-255">If the property is a negative number, the view state will not be broken into chunks.</span></span>

## <a name="pageadapter"></a><span data-ttu-id="dd16a-256">PageAdapter</span><span class="sxs-lookup"><span data-stu-id="dd16a-256">PageAdapter</span></span>

<span data-ttu-id="dd16a-257">要求側のブラウザーのページを変更する PageAdapter オブジェクトへの参照を返します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-257">Returns a reference to the PageAdapter object that modifies the page for the requesting browser.</span></span>

## <a name="previouspage"></a><span data-ttu-id="dd16a-258">PreviousPage</span><span class="sxs-lookup"><span data-stu-id="dd16a-258">PreviousPage</span></span>

<span data-ttu-id="dd16a-259">サーバー転送またはクロスページポストバックの場合に、前のページへの参照を返します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-259">Returns a reference to the previous page in cases of a Server.Transfer or a cross-page postback.</span></span>

## <a name="skinid"></a><span data-ttu-id="dd16a-260">SkinID</span><span class="sxs-lookup"><span data-stu-id="dd16a-260">SkinID</span></span>

<span data-ttu-id="dd16a-261">ページに適用する ASP.NET 2.0 スキンを指定します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-261">Specifies the ASP.NET 2.0 skin to apply to the page.</span></span>

## <a name="stylesheettheme"></a><span data-ttu-id="dd16a-262">StyleSheetTheme</span><span class="sxs-lookup"><span data-stu-id="dd16a-262">StyleSheetTheme</span></span>

<span data-ttu-id="dd16a-263">このプロパティは、ページに適用されるスタイルシートを取得または設定します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-263">This property gets or sets the style sheet that is applied to a page.</span></span>

## <a name="templatecontrol"></a><span data-ttu-id="dd16a-264">TemplateControl</span><span class="sxs-lookup"><span data-stu-id="dd16a-264">TemplateControl</span></span>

<span data-ttu-id="dd16a-265">ページのコントロールを格納しているへの参照を返します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-265">Returns a reference to the containing control for the page.</span></span>

## <a name="theme"></a><span data-ttu-id="dd16a-266">テーマ</span><span class="sxs-lookup"><span data-stu-id="dd16a-266">Theme</span></span>

<span data-ttu-id="dd16a-267">ページに適用される ASP.NET 2.0 テーマの名前を取得または設定します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-267">Gets or sets the name of the ASP.NET 2.0 theme applied to the page.</span></span> <span data-ttu-id="dd16a-268">この値は、PreInit メソッドの前に設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="dd16a-268">This value must be set prior to the PreInit method.</span></span>

## <a name="title"></a><span data-ttu-id="dd16a-269">タイトル</span><span class="sxs-lookup"><span data-stu-id="dd16a-269">Title</span></span>

<span data-ttu-id="dd16a-270">このプロパティは、ページヘッダーから取得されたページのタイトルを取得または設定します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-270">This property gets or sets the title for the page as obtained from the pages header.</span></span>

## <a name="viewstateencryptionmode"></a><span data-ttu-id="dd16a-271">ViewStateEncryptionMode</span><span class="sxs-lookup"><span data-stu-id="dd16a-271">ViewStateEncryptionMode</span></span>

<span data-ttu-id="dd16a-272">ページの ViewStateEncryptionMode を取得または設定します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-272">Gets or sets the ViewStateEncryptionMode of the page.</span></span> <span data-ttu-id="dd16a-273">このモジュールで前に説明したこのプロパティの詳細については、こちらを参照してください。</span><span class="sxs-lookup"><span data-stu-id="dd16a-273">See a detailed discussion of this property earlier in this module.</span></span>

## <a name="new-protected-properties-of-the-page-class"></a><span data-ttu-id="dd16a-274">ページクラスの新しいプロテクトプロパティ</span><span class="sxs-lookup"><span data-stu-id="dd16a-274">New Protected Properties of the Page Class</span></span>

<span data-ttu-id="dd16a-275">ASP.NET 2.0 のページクラスの新しいプロテクトプロパティを次に示します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-275">The following are the new protected properties of the Page class in ASP.NET 2.0.</span></span>

## <a name="adapter"></a><span data-ttu-id="dd16a-276">アダプター</span><span class="sxs-lookup"><span data-stu-id="dd16a-276">Adapter</span></span>

<span data-ttu-id="dd16a-277">要求したデバイス上でページをレンダリングする ControlAdapter への参照を返します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-277">Returns a reference to the ControlAdapter that renders the page on the device that requested it.</span></span>

## <a name="asyncmode"></a><span data-ttu-id="dd16a-278">AsyncMode</span><span class="sxs-lookup"><span data-stu-id="dd16a-278">AsyncMode</span></span>

<span data-ttu-id="dd16a-279">このプロパティは、ページが非同期に処理されるかどうかを示します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-279">This property indicates whether or not the page is processed asynchronously.</span></span> <span data-ttu-id="dd16a-280">これは、コード内で直接使用するのではなく、ランタイムによって使用されることを意図しています。</span><span class="sxs-lookup"><span data-stu-id="dd16a-280">It is intended for use by the runtime and not directly in code.</span></span>

## <a name="clientidseparator"></a><span data-ttu-id="dd16a-281">ClientIDSeparator</span><span class="sxs-lookup"><span data-stu-id="dd16a-281">ClientIDSeparator</span></span>

<span data-ttu-id="dd16a-282">このプロパティは、コントロールの一意のクライアント Id を作成するときに区切り記号として使用される文字を返します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-282">This property returns the character used as a separator when creating unique client IDs for controls.</span></span> <span data-ttu-id="dd16a-283">これは、コード内で直接使用するのではなく、ランタイムによって使用されることを意図しています。</span><span class="sxs-lookup"><span data-stu-id="dd16a-283">It is intended for use by the runtime and not directly in code.</span></span>

## <a name="pagestatepersister"></a><span data-ttu-id="dd16a-284">PageStatePersister</span><span class="sxs-lookup"><span data-stu-id="dd16a-284">PageStatePersister</span></span>

<span data-ttu-id="dd16a-285">このプロパティは、ページの PageStatePersister オブジェクトを返します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-285">This property returns the PageStatePersister object for the page.</span></span> <span data-ttu-id="dd16a-286">このプロパティは、主に ASP.NET コントロールの開発者によって使用されます。</span><span class="sxs-lookup"><span data-stu-id="dd16a-286">This property is primarily used by ASP.NET control developers.</span></span>

## <a name="uniquefilepathsuffix"></a><span data-ttu-id="dd16a-287">UniqueFilePathSuffix</span><span class="sxs-lookup"><span data-stu-id="dd16a-287">UniqueFilePathSuffix</span></span>

<span data-ttu-id="dd16a-288">このプロパティは、ブラウザーをキャッシュするためのファイルパスに追加される一意のサフィックスを返します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-288">This property returns a unique suffix that is appended to the file path for caching browsers.</span></span> <span data-ttu-id="dd16a-289">既定値は \_\_ufps = および6桁の数字です。</span><span class="sxs-lookup"><span data-stu-id="dd16a-289">The default value is \_\_ufps= and a 6-digit number.</span></span>

## <a name="new-public-methods-for-the-page-class"></a><span data-ttu-id="dd16a-290">ページクラスの新しいパブリックメソッド</span><span class="sxs-lookup"><span data-stu-id="dd16a-290">New Public Methods for the Page Class</span></span>

<span data-ttu-id="dd16a-291">次のパブリックメソッドは、ASP.NET 2.0 のページクラスに新しく追加されたものです。</span><span class="sxs-lookup"><span data-stu-id="dd16a-291">The following public methods are new to the Page class in ASP.NET 2.0.</span></span>

## <a name="addonprerendercompleteasync"></a><span data-ttu-id="dd16a-292">AddOnPreRenderCompleteAsync</span><span class="sxs-lookup"><span data-stu-id="dd16a-292">AddOnPreRenderCompleteAsync</span></span>

<span data-ttu-id="dd16a-293">このメソッドは、非同期ページ実行のイベントハンドラーデリゲートを登録します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-293">This method registers event handler delegates for asynchronous page execution.</span></span> <span data-ttu-id="dd16a-294">非同期ページについては、このモジュールで後ほど説明します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-294">Asynchronous pages are discussed later in this module.</span></span>

## <a name="applystylesheetskin"></a><span data-ttu-id="dd16a-295">ApplyStyleSheetSkin</span><span class="sxs-lookup"><span data-stu-id="dd16a-295">ApplyStyleSheetSkin</span></span>

<span data-ttu-id="dd16a-296">ページスタイルシートのプロパティをページに適用します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-296">Applies the properties in a pages style sheet to the page.</span></span>

## <a name="executeregisteredasynctasks"></a><span data-ttu-id="dd16a-297">ExecuteRegisteredAsyncTasks</span><span class="sxs-lookup"><span data-stu-id="dd16a-297">ExecuteRegisteredAsyncTasks</span></span>

<span data-ttu-id="dd16a-298">このメソッドは非同期タスクです。</span><span class="sxs-lookup"><span data-stu-id="dd16a-298">This method beings an asynchronous task.</span></span>

### <a name="getvalidators"></a><span data-ttu-id="dd16a-299">GetValidators</span><span class="sxs-lookup"><span data-stu-id="dd16a-299">GetValidators</span></span>

<span data-ttu-id="dd16a-300">指定された検証グループの検証コントロールのコレクションを返します。何も指定されていない場合は、既定の検証グループを返します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-300">Returns a collection of validators for the specified validation group or the default validation group if none is specified.</span></span>

## <a name="registerasynctask"></a><span data-ttu-id="dd16a-301">RegisterAsyncTask</span><span class="sxs-lookup"><span data-stu-id="dd16a-301">RegisterAsyncTask</span></span>

<span data-ttu-id="dd16a-302">このメソッドは、新しい非同期タスクを登録します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-302">This method registers a new async task.</span></span> <span data-ttu-id="dd16a-303">非同期ページについては、このモジュールで後ほど説明します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-303">Asynchronous pages are covered later in this module.</span></span>

## <a name="registerrequirescontrolstate"></a><span data-ttu-id="dd16a-304">RegisterRequiresControlState</span><span class="sxs-lookup"><span data-stu-id="dd16a-304">RegisterRequiresControlState</span></span>

<span data-ttu-id="dd16a-305">このメソッドは、ページコントロールの状態を永続化する必要があることを ASP.NET に通知します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-305">This method tells ASP.NET that the pages control state must be persisted.</span></span>

## <a name="registerrequiresviewstateencryption"></a><span data-ttu-id="dd16a-306">RegisterRequiresViewStateEncryption</span><span class="sxs-lookup"><span data-stu-id="dd16a-306">RegisterRequiresViewStateEncryption</span></span>

<span data-ttu-id="dd16a-307">このメソッドは、ページ viewstate に暗号化が必要であることを ASP.NET に通知します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-307">This method tells ASP.NET that the pages viewstate requires encryption.</span></span>

## <a name="resolveclienturl"></a><span data-ttu-id="dd16a-308">ResolveClientUrl</span><span class="sxs-lookup"><span data-stu-id="dd16a-308">ResolveClientUrl</span></span>

<span data-ttu-id="dd16a-309">イメージに対するクライアント要求に使用できる相対 URL を返します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-309">Returns a relative URL that can be used for client requests for images, etc.</span></span>

## <a name="setfocus"></a><span data-ttu-id="dd16a-310">SetFocus</span><span class="sxs-lookup"><span data-stu-id="dd16a-310">SetFocus</span></span>

<span data-ttu-id="dd16a-311">このメソッドは、ページが最初に読み込まれるときに指定されるコントロールにフォーカスを設定します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-311">This method will set the focus to the control that is specified when the page is initially loaded.</span></span>

## <a name="unregisterrequirescontrolstate"></a><span data-ttu-id="dd16a-312">UnregisterRequiresControlState</span><span class="sxs-lookup"><span data-stu-id="dd16a-312">UnregisterRequiresControlState</span></span>

<span data-ttu-id="dd16a-313">このメソッドは、コントロールの状態の永続化を必要としないように、渡されたコントロールの登録を解除します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-313">This method will unregister the control that is passed to it as no longer requiring control state persistence.</span></span>

## <a name="changes-to-the-page-lifecycle"></a><span data-ttu-id="dd16a-314">ページのライフサイクルの変更</span><span class="sxs-lookup"><span data-stu-id="dd16a-314">Changes to the Page Lifecycle</span></span>

<span data-ttu-id="dd16a-315">ASP.NET 2.0 のページライフサイクルは大幅に変更されていませんが、注意する必要がある新しい方法がいくつかあります。</span><span class="sxs-lookup"><span data-stu-id="dd16a-315">The page lifecycle in ASP.NET 2.0 hasn't changed dramatically, but there are some new methods that you should be aware of.</span></span> <span data-ttu-id="dd16a-316">ASP.NET 2.0 ページのライフサイクルは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="dd16a-316">The ASP.NET 2.0 page lifecycle is outlined below.</span></span>

## <a name="preinit-new-in-aspnet-20"></a><span data-ttu-id="dd16a-317">PreInit (ASP.NET 2.0 の新)</span><span class="sxs-lookup"><span data-stu-id="dd16a-317">PreInit (New in ASP.NET 2.0)</span></span>

<span data-ttu-id="dd16a-318">PreInit イベントは、開発者がアクセスできる、ライフサイクルの最も早い段階です。</span><span class="sxs-lookup"><span data-stu-id="dd16a-318">The PreInit event is the earliest stage in the lifecycle that a developer can access.</span></span> <span data-ttu-id="dd16a-319">このイベントを追加すると、ASP.NET 2.0 のテーマ、マスターページ、ASP.NET 2.0 プロファイルのアクセスプロパティをプログラムで変更できるようになります。ポストバック状態の場合、Viewstate は、ライフサイクルのこの時点でコントロールにまだ適用されていないことを認識することが重要です。</span><span class="sxs-lookup"><span data-stu-id="dd16a-319">The addition of this event makes it possible to programmatically change ASP.NET 2.0 themes, master pages, access properties for an ASP.NET 2.0 profile, etc. If you are in a postback state, its important to realize that Viewstate has not yet been applied to controls at this point in the lifecycle.</span></span> <span data-ttu-id="dd16a-320">このため、開発者がこの段階でコントロールのプロパティを変更すると、後でページのライフサイクルで上書きされる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="dd16a-320">Therefore, if a developer changes a property of a control at this stage, it will likely be overwritten later in the pages lifecycle.</span></span>

## <a name="init"></a><span data-ttu-id="dd16a-321">Init</span><span class="sxs-lookup"><span data-stu-id="dd16a-321">Init</span></span>

<span data-ttu-id="dd16a-322">Init イベントは ASP.NET 1.x から変更されていません。</span><span class="sxs-lookup"><span data-stu-id="dd16a-322">The Init event has not changed from ASP.NET 1.x.</span></span> <span data-ttu-id="dd16a-323">ここでは、ページ上のコントロールのプロパティを読み取りまたは初期化します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-323">This is where you would want to read or initialize properties of controls on your page.</span></span> <span data-ttu-id="dd16a-324">この段階では、マスターページ、テーマなどが既にページに適用されています。</span><span class="sxs-lookup"><span data-stu-id="dd16a-324">At this stage, master pages, themes, etc. are already applied to the page.</span></span>

## <a name="initcomplete-new-in-20"></a><span data-ttu-id="dd16a-325">InitComplete (2.0 の新)</span><span class="sxs-lookup"><span data-stu-id="dd16a-325">InitComplete (New in 2.0)</span></span>

<span data-ttu-id="dd16a-326">InitComplete イベントは、ページ初期化ステージの最後に呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="dd16a-326">The InitComplete event is called at the end of the pages initialization stage.</span></span> <span data-ttu-id="dd16a-327">ライフサイクルのこの時点では、ページ上のコントロールにアクセスできますが、その状態はまだ設定されていません。</span><span class="sxs-lookup"><span data-stu-id="dd16a-327">At this point in the lifecycle, you can access controls on the page, but their state has not yet been populated.</span></span>

## <a name="preload-new-in-20"></a><span data-ttu-id="dd16a-328">プリロード (2.0 の新)</span><span class="sxs-lookup"><span data-stu-id="dd16a-328">PreLoad (New in 2.0)</span></span>

<span data-ttu-id="dd16a-329">このイベントは、すべてのポストバックデータが適用された後、ページ\_の読み込みの直前に呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="dd16a-329">This event is called after all postback data has been applied and just prior to Page\_Load.</span></span>

## <a name="load"></a><span data-ttu-id="dd16a-330">[読み込み]</span><span class="sxs-lookup"><span data-stu-id="dd16a-330">Load</span></span>

<span data-ttu-id="dd16a-331">Load イベントは ASP.NET 1.x から変更されていません。</span><span class="sxs-lookup"><span data-stu-id="dd16a-331">The Load event has not changed from ASP.NET 1.x.</span></span>

## <a name="loadcomplete-new-in-20"></a><span data-ttu-id="dd16a-332">LoadComplete (2.0 の新)</span><span class="sxs-lookup"><span data-stu-id="dd16a-332">LoadComplete (New in 2.0)</span></span>

<span data-ttu-id="dd16a-333">LoadComplete イベントは、ページ読み込みステージの最後のイベントです。</span><span class="sxs-lookup"><span data-stu-id="dd16a-333">The LoadComplete event is the last event in the pages load stage.</span></span> <span data-ttu-id="dd16a-334">この段階では、すべてのポストバックと viewstate データがページに適用されています。</span><span class="sxs-lookup"><span data-stu-id="dd16a-334">At this stage, all postback and viewstate data has been applied to the page.</span></span>

## <a name="prerender"></a><span data-ttu-id="dd16a-335">PreRender</span><span class="sxs-lookup"><span data-stu-id="dd16a-335">PreRender</span></span>

<span data-ttu-id="dd16a-336">ページに動的に追加されるコントロールに対して viewstate を適切に管理するには、PreRender イベントを追加する最後の機会とします。</span><span class="sxs-lookup"><span data-stu-id="dd16a-336">If you would like for viewstate to be properly maintained for controls that are added to the page dynamically, the PreRender event is the last opportunity to add them.</span></span>

## <a name="prerendercomplete-new-in-20"></a><span data-ttu-id="dd16a-337">PreRenderComplete (2.0 の新)</span><span class="sxs-lookup"><span data-stu-id="dd16a-337">PreRenderComplete (New in 2.0)</span></span>

<span data-ttu-id="dd16a-338">PreRenderComplete 段階では、すべてのコントロールがページに追加され、ページを表示する準備ができました。</span><span class="sxs-lookup"><span data-stu-id="dd16a-338">At the PreRenderComplete stage, all controls have been added to the page and the page is ready to be rendered.</span></span> <span data-ttu-id="dd16a-339">PreRenderComplete イベントは、ページ viewstate が保存される前に発生する最後のイベントです。</span><span class="sxs-lookup"><span data-stu-id="dd16a-339">The PreRenderComplete event is the last event raised before the pages viewstate is saved.</span></span>

## <a name="savestatecomplete-new-in-20"></a><span data-ttu-id="dd16a-340">SaveStateComplete (2.0 の新)</span><span class="sxs-lookup"><span data-stu-id="dd16a-340">SaveStateComplete (New in 2.0)</span></span>

<span data-ttu-id="dd16a-341">SaveStateComplete イベントは、すべてのページ viewstate とコントロールの状態が保存された直後に呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="dd16a-341">The SaveStateComplete event is called immediately after all page viewstate and control state has been saved.</span></span> <span data-ttu-id="dd16a-342">これは、ページが実際にブラウザーにレンダリングされる前の最後のイベントです。</span><span class="sxs-lookup"><span data-stu-id="dd16a-342">This is the last event before the page is actually rendered to the browser.</span></span>

## <a name="render"></a><span data-ttu-id="dd16a-343">レンダー</span><span class="sxs-lookup"><span data-stu-id="dd16a-343">Render</span></span>

<span data-ttu-id="dd16a-344">ASP.NET 1.x 以降、Render メソッドは変更されていません。</span><span class="sxs-lookup"><span data-stu-id="dd16a-344">The Render method has not changed since ASP.NET 1.x.</span></span> <span data-ttu-id="dd16a-345">ここで HtmlTextWriter が初期化され、ページがブラウザーに表示されます。</span><span class="sxs-lookup"><span data-stu-id="dd16a-345">This is where the HtmlTextWriter is initialized and the page is rendered to the browser.</span></span>

## <a name="cross-page-postback-in-aspnet-20"></a><span data-ttu-id="dd16a-346">ASP.NET 2.0 のクロスページポストバック</span><span class="sxs-lookup"><span data-stu-id="dd16a-346">Cross-Page Postback in ASP.NET 2.0</span></span>

<span data-ttu-id="dd16a-347">ASP.NET 1.x では、同じページにポストバックする必要がありました。</span><span class="sxs-lookup"><span data-stu-id="dd16a-347">In ASP.NET 1.x, postbacks were required to post to the same page.</span></span> <span data-ttu-id="dd16a-348">ページ間のポストバックは許可されませんでした。</span><span class="sxs-lookup"><span data-stu-id="dd16a-348">Cross-page postbacks were not allowed.</span></span> <span data-ttu-id="dd16a-349">ASP.NET 2.0 では、IButtonControl インターフェイスを使用して別のページにポストバックする機能が追加されています。</span><span class="sxs-lookup"><span data-stu-id="dd16a-349">ASP.NET 2.0 adds the ability to post back to a different page via the IButtonControl interface.</span></span> <span data-ttu-id="dd16a-350">新しい IButtonControl インターフェイス (サードパーティのカスタムコントロールに加えて Button、LinkButton、および ImageButton) を実装するコントロールは、PostBackUrl 属性を使用することによって、この新しい機能を利用できます。</span><span class="sxs-lookup"><span data-stu-id="dd16a-350">Any control that implements the new IButtonControl interface (Button, LinkButton, and ImageButton in addition to third-party custom controls) can take advantage of this new functionality via the use of the PostBackUrl attribute.</span></span> <span data-ttu-id="dd16a-351">次のコードは、2番目のページにポストバックするボタンコントロールを示しています。</span><span class="sxs-lookup"><span data-stu-id="dd16a-351">The following code shows a Button control that posts back to a second page.</span></span>

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample5.aspx)]

<span data-ttu-id="dd16a-352">ページがポストバックされると、ポストバックを開始するページは、2ページ目の PreviousPage プロパティを使用してアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="dd16a-352">When the page is posted back, the Page that initiates the postback is accessible via the PreviousPage property on the second page.</span></span> <span data-ttu-id="dd16a-353">この機能は、コントロールが別のページにポストバックしたときに ASP.NET 2.0 がページに表示する新しい Web フォーム\_DoPostBackWithOptions クライアント側関数によって実装されます。</span><span class="sxs-lookup"><span data-stu-id="dd16a-353">This functionality is implemented via the new WebForm\_DoPostBackWithOptions client-side function that ASP.NET 2.0 renders to the page when a control posts back to a different page.</span></span> <span data-ttu-id="dd16a-354">この JavaScript 関数は、クライアントにスクリプトを出力する新しい Webresource.axd ハンドラーによって提供されます。</span><span class="sxs-lookup"><span data-stu-id="dd16a-354">This JavaScript function is provided by the new WebResource.axd handler which emits script to the client.</span></span>

<span data-ttu-id="dd16a-355">次のビデオは、ページ間のポストバックのチュートリアルです。</span><span class="sxs-lookup"><span data-stu-id="dd16a-355">The video below is a walkthrough of a cross-page postback.</span></span>

![](the-asp-net-2-0-page-model/_static/image2.png)

[<span data-ttu-id="dd16a-356">全画面表示のビデオを開く</span><span class="sxs-lookup"><span data-stu-id="dd16a-356">Open Full-Screen Video</span></span>](the-asp-net-2-0-page-model/_static/xpage1.wmv)

## <a name="more-details-on-cross-page-postbacks"></a><span data-ttu-id="dd16a-357">クロスページポストバックの詳細</span><span class="sxs-lookup"><span data-stu-id="dd16a-357">More Details on Cross-Page Postbacks</span></span>

### <a name="viewstate"></a><span data-ttu-id="dd16a-358">Viewstate</span><span class="sxs-lookup"><span data-stu-id="dd16a-358">Viewstate</span></span>

<span data-ttu-id="dd16a-359">クロスページポストバックシナリオでは、最初のページから viewstate に対して何が起こるかについて、既にたずねているかもしれません。</span><span class="sxs-lookup"><span data-stu-id="dd16a-359">You may have asked yourself already about what happens to the viewstate from the first page in a cross-page postback scenario.</span></span> <span data-ttu-id="dd16a-360">結局のところ、IPostBackDataHandler を実装していないコントロールは viewstate によって状態を保持するので、ページ間のポストバックの2ページ目でそのコントロールのプロパティにアクセスするには、ページの viewstate にアクセスできる必要があります。</span><span class="sxs-lookup"><span data-stu-id="dd16a-360">After all, any control that does not implement IPostBackDataHandler will persist its state via viewstate, so to have access to the properties of that control on the second page of a cross-page postback, you must have access to the viewstate for the page.</span></span> <span data-ttu-id="dd16a-361">ASP.NET 2.0 は、\_\_PREVIOUSPAGE と呼ばれる2番目のページの新しい隠しフィールドを使用して、このシナリオを処理します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-361">ASP.NET 2.0 takes care of this scenario using a new hidden field in the second page called \_\_PREVIOUSPAGE.</span></span> <span data-ttu-id="dd16a-362">\_\_PREVIOUSPAGE フォームフィールドには、最初のページの viewstate が含まれています。これにより、2番目のページのすべてのコントロールのプロパティにアクセスできるようになります。</span><span class="sxs-lookup"><span data-stu-id="dd16a-362">The \_\_PREVIOUSPAGE form field contains the viewstate for the first page so that you can have access to the properties of all controls in the second page.</span></span>

### <a name="circumventing-findcontrol"></a><span data-ttu-id="dd16a-363">FindControl の回避</span><span class="sxs-lookup"><span data-stu-id="dd16a-363">Circumventing FindControl</span></span>

<span data-ttu-id="dd16a-364">クロスページポストバックのビデオチュートリアルでは、FindControl メソッドを使用して、最初のページの TextBox コントロールへの参照を取得しました。</span><span class="sxs-lookup"><span data-stu-id="dd16a-364">In the video walkthrough of a cross-page postback, I used the FindControl method to get a reference to the TextBox control on the first page.</span></span> <span data-ttu-id="dd16a-365">この方法は、その目的に適していますが、FindControl は高価であり、追加のコードを記述する必要があります。</span><span class="sxs-lookup"><span data-stu-id="dd16a-365">That method works well for that purpose, but FindControl is expensive and it requires writing additional code.</span></span> <span data-ttu-id="dd16a-366">幸いにも、ASP.NET 2.0 では、この目的のために FindControl の代わりに、多くのシナリオで動作するようになっています。</span><span class="sxs-lookup"><span data-stu-id="dd16a-366">Fortunately, ASP.NET 2.0 provides an alternative to FindControl for this purpose that will work in many scenarios.</span></span> <span data-ttu-id="dd16a-367">PreviousPageType ディレクティブを使用すると、TypeName または VirtualPath 属性を使用して、前のページへの厳密に型指定された参照を持つことができます。</span><span class="sxs-lookup"><span data-stu-id="dd16a-367">The PreviousPageType directive allows you to have a strongly-typed reference to the previous page by using either the TypeName or the VirtualPath attribute.</span></span> <span data-ttu-id="dd16a-368">TypeName 属性では、前のページの種類を指定できます。 VirtualPath 属性では、仮想パスを使用して前のページを参照できます。</span><span class="sxs-lookup"><span data-stu-id="dd16a-368">The TypeName attribute allows you to specify the type of the previous page while the VirtualPath attribute allows you to refer to the previous page using a virtual path.</span></span> <span data-ttu-id="dd16a-369">PreviousPageType ディレクティブを設定したら、パブリックプロパティを使用してアクセスを許可するコントロールなどを公開する必要があります。</span><span class="sxs-lookup"><span data-stu-id="dd16a-369">After you've set the PreviousPageType directive, you must then expose the controls, etc. to which you want to allow access using public properties.</span></span>

## <a name="lab-1-cross-page-postback"></a><span data-ttu-id="dd16a-370">ラボ1ページ間ポストバック</span><span class="sxs-lookup"><span data-stu-id="dd16a-370">Lab 1 Cross-Page Postback</span></span>

<span data-ttu-id="dd16a-371">このラボでは、ASP.NET 2.0 の新しいクロスページポストバック機能を使用するアプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-371">In this lab, you will create an application that uses the new cross-page postback functionality of ASP.NET 2.0.</span></span>

1. <span data-ttu-id="dd16a-372">Visual Studio 2005 を開き、新しい ASP.NET Web サイトを作成します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-372">Open Visual Studio 2005 and create a new ASP.NET Web site.</span></span>
2. <span data-ttu-id="dd16a-373">Page2 という名前の新しい Web フォームを追加します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-373">Add a new Webform called page2.aspx.</span></span>
3. <span data-ttu-id="dd16a-374">デザインビューで default.aspx を開き、ボタンコントロールとテキストボックスコントロールを追加します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-374">Open the Default.aspx in Design view and add a Button control and a TextBox control.</span></span> 

    1. <span data-ttu-id="dd16a-375">ボタンコントロールに**Submitbutton**の id を指定し、テキストボックスコントロールに**ユーザー名**の id を指定します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-375">Give the Button control an ID of **SubmitButton** and the TextBox control an ID of **UserName**.</span></span>
    2. <span data-ttu-id="dd16a-376">ボタンの PostBackUrl プロパティを page2 に設定します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-376">Set the PostBackUrl property of the Button to page2.aspx.</span></span>
4. <span data-ttu-id="dd16a-377">ソースビューで page2 を開きます。</span><span class="sxs-lookup"><span data-stu-id="dd16a-377">Open page2.aspx in Source view.</span></span>
5. <span data-ttu-id="dd16a-378">次に示すように、@ PreviousPageType ディレクティブを追加します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-378">Add a @ PreviousPageType directive as shown below:</span></span>
6. <span data-ttu-id="dd16a-379">ページに次のコードを追加して、page2 の分離コードの\_読み込みます。</span><span class="sxs-lookup"><span data-stu-id="dd16a-379">Add the following code to the Page\_Load of page2.aspx's code-behind:</span></span> 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample6.cs)]
7. <span data-ttu-id="dd16a-380">[ビルド] メニューの [ビルド] をクリックして、プロジェクトをビルドします。</span><span class="sxs-lookup"><span data-stu-id="dd16a-380">Build the project by clicking on Build on the Build menu.</span></span>
8. <span data-ttu-id="dd16a-381">Default.aspx の分離コードに次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-381">Add the following code to the code-behind for Default.aspx:</span></span> 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample7.cs)]
9. <span data-ttu-id="dd16a-382">Page2 での\_の読み込みページを次のように変更します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-382">Change the Page\_Load in page2.aspx to the following:</span></span> 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample8.cs)]
10. <span data-ttu-id="dd16a-383">プロジェクトをビルドします。</span><span class="sxs-lookup"><span data-stu-id="dd16a-383">Build the project.</span></span>
11. <span data-ttu-id="dd16a-384">プロジェクトを実行します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-384">Run the project.</span></span>
12. <span data-ttu-id="dd16a-385">テキストボックスに名前を入力し、ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="dd16a-385">Enter your name in the TextBox and click the button.</span></span>
13. <span data-ttu-id="dd16a-386">結果は何ですか。</span><span class="sxs-lookup"><span data-stu-id="dd16a-386">What is the result?</span></span>

## <a name="asynchronous-pages-in-aspnet-20"></a><span data-ttu-id="dd16a-387">ASP.NET 2.0 の非同期ページ</span><span class="sxs-lookup"><span data-stu-id="dd16a-387">Asynchronous Pages in ASP.NET 2.0</span></span>

<span data-ttu-id="dd16a-388">ASP.NET の競合に関する多くの問題は、外部呼び出し (Web サービスやデータベースの呼び出しなど) の待機時間、ファイル IO の待機時間などによって発生します。ASP.NET アプリケーションに対して要求が行われると、ASP.NET はそのワーカースレッドの1つを使用してその要求を処理します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-388">Many contention problems in ASP.NET are caused by latency of external calls (such as Web service or database calls), file IO latency, etc. When a request is made against an ASP.NET application, ASP.NET uses one of its worker threads to service that request.</span></span> <span data-ttu-id="dd16a-389">この要求は、要求が完了し、応答が送信されるまで、そのスレッドを所有します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-389">That request owns that thread until the request is complete and the response has been sent.</span></span> <span data-ttu-id="dd16a-390">ASP.NET 2.0 は、ページを非同期的に実行する機能を追加することで、これらの種類の問題の待機時間の問題を解決することを目指しています。</span><span class="sxs-lookup"><span data-stu-id="dd16a-390">ASP.NET 2.0 seeks to resolve latency issues with these types of issues by adding the capability to execute pages asynchronously.</span></span> <span data-ttu-id="dd16a-391">これは、ワーカースレッドが要求を開始し、別のスレッドに対して追加の実行をハンドオフして、使用可能なスレッドプールにすばやく戻ることができることを意味します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-391">That means that a worker thread can start the request and then hand off additional execution to another thread, thereby returning to the available thread pool quickly.</span></span> <span data-ttu-id="dd16a-392">ファイル IO、データベース呼び出しなどが完了すると、新しいスレッドがスレッドプールから取得され、要求が完了します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-392">When the file IO, database call, etc. has completed, a new thread is obtained from the thread pool to finish the request.</span></span>

<span data-ttu-id="dd16a-393">ページを非同期で実行するための最初の手順は、次のようにページディレクティブの**Async**属性を設定することです。</span><span class="sxs-lookup"><span data-stu-id="dd16a-393">The first step in making a page execute asynchronously is to set the **Async** attribute of the page directive like so:</span></span>

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample9.aspx)]

<span data-ttu-id="dd16a-394">この属性は、ページの IHttpAsyncHandler を実装するように ASP.NET に指示します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-394">This attribute tells ASP.NET to implement the IHttpAsyncHandler for the page.</span></span>

<span data-ttu-id="dd16a-395">次の手順では、PreRender の前に、ページのライフサイクルのポイントで AddOnPreRenderCompleteAsync メソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-395">The next step is to call the AddOnPreRenderCompleteAsync method at a point in the lifecycle of the page prior to PreRender.</span></span> <span data-ttu-id="dd16a-396">(通常、このメソッドは、ページ\_の読み込み時に呼び出されます)。AddOnPreRenderCompleteAsync メソッドは2つのパラメーターを受け取ります。BeginEventHandler と EndEventHandler。</span><span class="sxs-lookup"><span data-stu-id="dd16a-396">(This method is typically called in Page\_Load.) The AddOnPreRenderCompleteAsync method takes two parameters; a BeginEventHandler and an EndEventHandler.</span></span> <span data-ttu-id="dd16a-397">BeginEventHandler は、パラメーターとして EndEventHandler に渡される IAsyncResult を返します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-397">The BeginEventHandler returns an IAsyncResult which is then passed as a parameter to the EndEventHandler.</span></span>

<span data-ttu-id="dd16a-398">次のビデオは、非同期ページ要求のチュートリアルです。</span><span class="sxs-lookup"><span data-stu-id="dd16a-398">The video below is a walkthrough of an asynchronous page request.</span></span>

![](the-asp-net-2-0-page-model/_static/image3.png)

[<span data-ttu-id="dd16a-399">全画面表示のビデオを開く</span><span class="sxs-lookup"><span data-stu-id="dd16a-399">Open Full-Screen Video</span></span>](the-asp-net-2-0-page-model/_static/async1.wmv)

> [!NOTE]
> <span data-ttu-id="dd16a-400">EndEventHandler が完了するまで、非同期ページはブラウザーに表示されません。</span><span class="sxs-lookup"><span data-stu-id="dd16a-400">An async page does not render to the browser until the EndEventHandler has completed.</span></span> <span data-ttu-id="dd16a-401">当然のことですが、一部の開発者は非同期要求を非同期コールバックに似ていると考えています。</span><span class="sxs-lookup"><span data-stu-id="dd16a-401">No doubt but that some developers will think of async requests as being similar to async callbacks.</span></span> <span data-ttu-id="dd16a-402">そうではないことに注意することが重要です。</span><span class="sxs-lookup"><span data-stu-id="dd16a-402">It's important to realize that they are not.</span></span> <span data-ttu-id="dd16a-403">非同期要求の利点は、新しい要求を処理するために最初のワーカースレッドをスレッドプールに返すことができることです。これにより、IO バインドが原因で競合が減少します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-403">The benefit to asynchronous requests is that the first worker thread can be returned to the thread pool to service new requests, thereby reducing contention due to being IO bound, etc.</span></span>

## <a name="script-callbacks-in-aspnet-20"></a><span data-ttu-id="dd16a-404">ASP.NET 2.0 のスクリプトコールバック</span><span class="sxs-lookup"><span data-stu-id="dd16a-404">Script Callbacks in ASP.NET 2.0</span></span>

<span data-ttu-id="dd16a-405">Web 開発者は、コールバックに関連するちらつきを防ぐ方法を常に探していました。</span><span class="sxs-lookup"><span data-stu-id="dd16a-405">Web developers have always looked for ways to prevent the flickering associated with a callback.</span></span> <span data-ttu-id="dd16a-406">ASP.NET 1.x では、SmartNavigation はちらつきを避けるための最も一般的な方法でしたが、クライアントでの実装が複雑になるため、SmartNavigation は一部の開発者にとって問題を引き起こしました。</span><span class="sxs-lookup"><span data-stu-id="dd16a-406">In ASP.NET 1.x, SmartNavigation was the most common method for avoiding flickering, but SmartNavigation caused problems for some developers because of the complexity of its implementation on the client.</span></span> <span data-ttu-id="dd16a-407">ASP.NET 2.0 では、スクリプトコールバックに関するこの問題に対処しています。</span><span class="sxs-lookup"><span data-stu-id="dd16a-407">ASP.NET 2.0 addresses this issue with script callbacks.</span></span> <span data-ttu-id="dd16a-408">スクリプトコールバックは、XMLHttp を利用して、Web サーバーに対して JavaScript 経由で要求を行います。</span><span class="sxs-lookup"><span data-stu-id="dd16a-408">Script callbacks utilize XMLHttp to make requests against the Web server via JavaScript.</span></span> <span data-ttu-id="dd16a-409">XMLHttp 要求は、ブラウザーの DOM を使用して操作できる XML データを返します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-409">The XMLHttp request returns XML data that can then be manipulated via the browser's DOM.</span></span> <span data-ttu-id="dd16a-410">XMLHttp コードは、新しい Webresource.axd ハンドラーによってユーザーに表示されません。</span><span class="sxs-lookup"><span data-stu-id="dd16a-410">XMLHttp code is hidden from the user by the new WebResource.axd handler.</span></span>

<span data-ttu-id="dd16a-411">ASP.NET 2.0 でスクリプトコールバックを構成するために必要な手順がいくつかあります。</span><span class="sxs-lookup"><span data-stu-id="dd16a-411">There are several steps that are necessary in order to configure a script callback in ASP.NET 2.0.</span></span>

## <a name="step-1--implement-the-icallbackeventhandler-interface"></a><span data-ttu-id="dd16a-412">手順 1: ICallbackEventHandler インターフェイスを実装する</span><span class="sxs-lookup"><span data-stu-id="dd16a-412">Step 1 : Implement the ICallbackEventHandler Interface</span></span>

<span data-ttu-id="dd16a-413">ASP.NET がスクリプトコールバックに参加しているとしてページを認識できるようにするには、ICallbackEventHandler インターフェイスを実装する必要があります。</span><span class="sxs-lookup"><span data-stu-id="dd16a-413">In order for ASP.NET to recognize your page as participating in a script callback, you must implement the ICallbackEventHandler interface.</span></span> <span data-ttu-id="dd16a-414">これは、分離コードファイルで次のように実行できます。</span><span class="sxs-lookup"><span data-stu-id="dd16a-414">You can do this in your code-behind file like so:</span></span>

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample10.cs)]

<span data-ttu-id="dd16a-415">この操作は、次のように @ Implements ディレクティブを使用して行うこともできます。</span><span class="sxs-lookup"><span data-stu-id="dd16a-415">You can also do this using the @ Implements directive like so:</span></span>

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample11.aspx)]

<span data-ttu-id="dd16a-416">インライン ASP.NET コードを使用する場合は、通常、@ Implements ディレクティブを使用します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-416">You would typically use the @ Implements directive when using inline ASP.NET code.</span></span>

## <a name="step-2--call-getcallbackeventreference"></a><span data-ttu-id="dd16a-417">手順 2: GetCallbackEventReference を呼び出す</span><span class="sxs-lookup"><span data-stu-id="dd16a-417">Step 2 : Call GetCallbackEventReference</span></span>

<span data-ttu-id="dd16a-418">前述のように、XMLHttp 呼び出しは Webresource.axd ハンドラーにカプセル化されています。</span><span class="sxs-lookup"><span data-stu-id="dd16a-418">As mentioned previously, the XMLHttp call is encapsulated in the WebResource.axd handler.</span></span> <span data-ttu-id="dd16a-419">ページが表示されると、ASP.NET は、Webresource.axd によって提供されるクライアントスクリプトである Web フォーム\_DoCallback への呼び出しを追加します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-419">When your page is rendered, ASP.NET will add a call to WebForm\_DoCallback, a client script that is provided by WebResource.axd.</span></span> <span data-ttu-id="dd16a-420">Web フォーム\_DoCallback 関数は、コールバックの \_\_doPostBack バック関数を置き換えます。</span><span class="sxs-lookup"><span data-stu-id="dd16a-420">The WebForm\_DoCallback function replaces the \_\_doPostBack function for a callback.</span></span> <span data-ttu-id="dd16a-421">\_\_doPostBack バックは、プログラムによってページにフォームを送信することに注意してください。</span><span class="sxs-lookup"><span data-stu-id="dd16a-421">Remember that \_\_doPostBack programmatically submits the form on the page.</span></span> <span data-ttu-id="dd16a-422">コールバックシナリオでは、ポストバックを防止する必要があるため、\_\_doPostBack バックでは十分ではありません。</span><span class="sxs-lookup"><span data-stu-id="dd16a-422">In a callback scenario, you want to prevent a postback, so \_\_doPostBack will not suffice.</span></span>

> [!NOTE]
> <span data-ttu-id="dd16a-423">\_\_doPostBack バックは、クライアントスクリプトコールバックシナリオのページに引き続き表示されます。</span><span class="sxs-lookup"><span data-stu-id="dd16a-423">\_\_doPostBack is still rendered to the page in a client script callback scenario.</span></span> <span data-ttu-id="dd16a-424">ただし、コールバックには使用されません。</span><span class="sxs-lookup"><span data-stu-id="dd16a-424">However, it's not used for the callback.</span></span>

<span data-ttu-id="dd16a-425">Web フォーム\_DoCallback クライアント側関数の引数は、通常はページ\_読み込みで呼び出されるサーバー側の関数 GetCallbackEventReference を介して提供されます。</span><span class="sxs-lookup"><span data-stu-id="dd16a-425">The arguments for the WebForm\_DoCallback client-side function are provided via the server-side function GetCallbackEventReference which would normally be called in Page\_Load.</span></span> <span data-ttu-id="dd16a-426">GetCallbackEventReference の一般的な呼び出しは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="dd16a-426">A typical call to GetCallbackEventReference might look like this:</span></span>

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample12.cs)]

> [!NOTE]
> <span data-ttu-id="dd16a-427">この場合、cm は ClientScriptManager のインスタンスです。</span><span class="sxs-lookup"><span data-stu-id="dd16a-427">In this case, cm is an instance of ClientScriptManager.</span></span> <span data-ttu-id="dd16a-428">ClientScriptManager クラスについては、このモジュールで後ほど説明します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-428">The ClientScriptManager class will be covered later in this module.</span></span>

<span data-ttu-id="dd16a-429">GetCallbackEventReference には、いくつかのオーバーロードされたバージョンがあります。</span><span class="sxs-lookup"><span data-stu-id="dd16a-429">There are several overloaded versions of GetCallbackEventReference.</span></span> <span data-ttu-id="dd16a-430">この場合、引数は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="dd16a-430">In this case, the arguments are as follows:</span></span>

`this`

<span data-ttu-id="dd16a-431">GetCallbackEventReference が呼び出されているコントロールへの参照。</span><span class="sxs-lookup"><span data-stu-id="dd16a-431">A reference to the control where GetCallbackEventReference is being called.</span></span> <span data-ttu-id="dd16a-432">この例では、ページ自体です。</span><span class="sxs-lookup"><span data-stu-id="dd16a-432">In this case, it's the page itself.</span></span>

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample13.js)]

<span data-ttu-id="dd16a-433">クライアント側のコードからサーバー側のイベントに渡される文字列引数。</span><span class="sxs-lookup"><span data-stu-id="dd16a-433">A string argument that will be passed from the client-side code to the server-side event.</span></span> <span data-ttu-id="dd16a-434">この場合、Im は ddlCompany というドロップダウンの値を渡します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-434">In this case, Im passing the value of a dropdown called ddlCompany.</span></span>

`ShowCompanyName`

<span data-ttu-id="dd16a-435">サーバー側のコールバックイベントから (文字列として) 戻り値を受け取るクライアント側関数の名前。</span><span class="sxs-lookup"><span data-stu-id="dd16a-435">The name of the client-side function that will accept the return value (as string) from the server-side callback event.</span></span> <span data-ttu-id="dd16a-436">この関数は、サーバー側のコールバックが成功した場合にのみ呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="dd16a-436">This function will only be called when the server-side callback is successful.</span></span> <span data-ttu-id="dd16a-437">そのため、堅牢性を確保するために、通常は、オーバーロードされたバージョンの GetCallbackEventReference を使用することをお勧めします。これは、エラーが発生した場合に実行するクライアント側関数の名前を指定する追加の文字列引数を受け取ります。</span><span class="sxs-lookup"><span data-stu-id="dd16a-437">Therefore, for the sake of robustness, it is generally recommended to use the overloaded version of GetCallbackEventReference that takes an additional string argument specifying the name of a client-side function to execute in the event of an error.</span></span>

`null`

<span data-ttu-id="dd16a-438">サーバーへのコールバックの前に開始したクライアント側の関数を表す文字列。</span><span class="sxs-lookup"><span data-stu-id="dd16a-438">A string representing a client-side function that it initiated before the callback to the server.</span></span> <span data-ttu-id="dd16a-439">この場合、このようなスクリプトは存在しないため、引数は null になります。</span><span class="sxs-lookup"><span data-stu-id="dd16a-439">In this case, there is no such script, so the argument is null.</span></span>

`true`

<span data-ttu-id="dd16a-440">コールバックを非同期的に実行するかどうかを指定するブール値。</span><span class="sxs-lookup"><span data-stu-id="dd16a-440">A Boolean specifying whether or not to conduct the callback asynchronously.</span></span>

<span data-ttu-id="dd16a-441">クライアント上で Web フォーム\_DoCallback を呼び出すと、これらの引数が渡されます。</span><span class="sxs-lookup"><span data-stu-id="dd16a-441">The call to WebForm\_DoCallback on the client will pass these arguments.</span></span> <span data-ttu-id="dd16a-442">このため、このページがクライアントに表示されると、そのコードは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="dd16a-442">Therefore, when this page is rendered on the client, that code will look like so:</span></span>

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample14.js)]

<span data-ttu-id="dd16a-443">クライアント上の関数のシグネチャが少し異なることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="dd16a-443">Notice that the signature of the function on the client is a bit different.</span></span> <span data-ttu-id="dd16a-444">クライアント側の関数は、5つの文字列とブール値を渡します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-444">The client-side function passes 5 strings and a Boolean.</span></span> <span data-ttu-id="dd16a-445">追加の文字列 (上の例では null) には、サーバー側のコールバックからのエラーを処理するクライアント側の関数が含まれています。</span><span class="sxs-lookup"><span data-stu-id="dd16a-445">The additional string (which is null in the above example) contains the client-side function that will handle any errors from the server-side callback.</span></span>

## <a name="step-3--hook-the-client-side-control-event"></a><span data-ttu-id="dd16a-446">手順 3: クライアント側のコントロールイベントをフックする</span><span class="sxs-lookup"><span data-stu-id="dd16a-446">Step 3 : Hook the Client-Side Control Event</span></span>

<span data-ttu-id="dd16a-447">上記の GetCallbackEventReference の戻り値が文字列変数に割り当てられていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="dd16a-447">Notice that the return value of GetCallbackEventReference above was assigned to a string variable.</span></span> <span data-ttu-id="dd16a-448">この文字列は、コールバックを開始するコントロールのクライアント側イベントをフックするために使用されます。</span><span class="sxs-lookup"><span data-stu-id="dd16a-448">That string is used to hook a client-side event for the control that initiates the callback.</span></span> <span data-ttu-id="dd16a-449">この例では、コールバックはページのドロップダウンによって開始されるため、 *OnChange*イベントをフックします。</span><span class="sxs-lookup"><span data-stu-id="dd16a-449">In this example, the callback is initiated by a dropdown on the page, so I want to hook the *OnChange* event.</span></span>

<span data-ttu-id="dd16a-450">クライアント側のイベントをフックするには、次のように、クライアント側のマークアップにハンドラーを追加するだけです。</span><span class="sxs-lookup"><span data-stu-id="dd16a-450">To hook the client-side event, simply add a handler to the client-side markup as follows:</span></span>

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample15.cs)]

<span data-ttu-id="dd16a-451">*CGetCallbackEventReference f*は、呼び出しからの戻り値であることを思い出してください。</span><span class="sxs-lookup"><span data-stu-id="dd16a-451">Recall that *cbRef* is the return value from the call to GetCallbackEventReference.</span></span> <span data-ttu-id="dd16a-452">これには、上に示した Web フォーム\_DoCallback の呼び出しが含まれています。</span><span class="sxs-lookup"><span data-stu-id="dd16a-452">It contains the call to WebForm\_DoCallback that was shown above.</span></span>

## <a name="step-4--register-the-client-side-script"></a><span data-ttu-id="dd16a-453">手順 4: クライアント側のスクリプトを登録する</span><span class="sxs-lookup"><span data-stu-id="dd16a-453">Step 4 : Register the Client-Side Script</span></span>

<span data-ttu-id="dd16a-454">GetCallbackEventReference を呼び出すことで、サーバー側のコールバックが成功したときに**Showcompanyname**というクライアント側のスクリプトが実行されることが指定されたことを思い出してください。</span><span class="sxs-lookup"><span data-stu-id="dd16a-454">Recall that the call to GetCallbackEventReference specified that a client-side script called **ShowCompanyName** would be executed when the server-side callback succeeds.</span></span> <span data-ttu-id="dd16a-455">このスクリプトは、ClientScriptManager インスタンスを使用してページに追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="dd16a-455">That script needs to be added to the page using a ClientScriptManager instance.</span></span> <span data-ttu-id="dd16a-456">(ClientScriptManager クラスについては、このモジュールで後ほど説明します)。次のようにします。</span><span class="sxs-lookup"><span data-stu-id="dd16a-456">(The ClientScriptManager class will be discussed later in this module.) You do that like so:</span></span>

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample16.js)]

## <a name="step-5--call-the-methods-of-the-icallbackeventhandler-interface"></a><span data-ttu-id="dd16a-457">手順 5: ICallbackEventHandler インターフェイスのメソッドを呼び出す</span><span class="sxs-lookup"><span data-stu-id="dd16a-457">Step 5 : Call the Methods of the ICallbackEventHandler Interface</span></span>

<span data-ttu-id="dd16a-458">ICallbackEventHandler には、コードに実装する必要がある2つのメソッドが含まれています。</span><span class="sxs-lookup"><span data-stu-id="dd16a-458">The ICallbackEventHandler contains two methods that you need to implement in your code.</span></span> <span data-ttu-id="dd16a-459">これらは**RaiseCallbackEvent**と**GetCallbackEvent**です。</span><span class="sxs-lookup"><span data-stu-id="dd16a-459">They are **RaiseCallbackEvent** and **GetCallbackEvent**.</span></span>

<span data-ttu-id="dd16a-460">**RaiseCallbackEvent**は、引数として文字列を受け取り、nothing を返します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-460">**RaiseCallbackEvent** takes a string as an argument and returns nothing.</span></span> <span data-ttu-id="dd16a-461">文字列引数は、クライアント側の呼び出しから Web フォーム\_DoCallback に渡されます。</span><span class="sxs-lookup"><span data-stu-id="dd16a-461">The string argument is passed from the client-side call to WebForm\_DoCallback.</span></span> <span data-ttu-id="dd16a-462">この場合、その値は ddlCompany というドロップダウンリストの*value*属性です。</span><span class="sxs-lookup"><span data-stu-id="dd16a-462">In this case, that value is the *value* attribute of the dropdown called ddlCompany.</span></span> <span data-ttu-id="dd16a-463">サーバー側のコードは、RaiseCallbackEvent メソッドに配置する必要があります。</span><span class="sxs-lookup"><span data-stu-id="dd16a-463">Your server-side code should be placed in the RaiseCallbackEvent method.</span></span> <span data-ttu-id="dd16a-464">たとえば、コールバックが外部リソースに対して WebRequest を作成する場合、そのコードは RaiseCallbackEvent に配置する必要があります。</span><span class="sxs-lookup"><span data-stu-id="dd16a-464">For example, if your callback is making a WebRequest against an external resource, that code should be placed in RaiseCallbackEvent.</span></span>

<span data-ttu-id="dd16a-465">**GetCallbackEvent**は、クライアントへのコールバックの戻り値を処理します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-465">**GetCallbackEvent** is responsible for processing the return of the callback to the client.</span></span> <span data-ttu-id="dd16a-466">引数を取らず、文字列を返します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-466">It takes no arguments and returns a string.</span></span> <span data-ttu-id="dd16a-467">返される文字列は、クライアント側の関数 (この場合は*Showcompanyname*) に引数として渡されます。</span><span class="sxs-lookup"><span data-stu-id="dd16a-467">The string that it returns will be passed as an argument to the client-side function, in this case *ShowCompanyName*.</span></span>

<span data-ttu-id="dd16a-468">上記の手順を完了すると、ASP.NET 2.0 でスクリプトコールバックを実行する準備が整います。</span><span class="sxs-lookup"><span data-stu-id="dd16a-468">Once you have completed the above steps, you are ready to perform a script callback in ASP.NET 2.0.</span></span>

![](the-asp-net-2-0-page-model/_static/image4.png)

[<span data-ttu-id="dd16a-469">全画面表示のビデオを開く</span><span class="sxs-lookup"><span data-stu-id="dd16a-469">Open Full-Screen Video</span></span>](the-asp-net-2-0-page-model/_static/callback1.wmv)

<span data-ttu-id="dd16a-470">ASP.NET のスクリプトコールバックは、XMLHttp 呼び出しをサポートするすべてのブラウザーでサポートされています。</span><span class="sxs-lookup"><span data-stu-id="dd16a-470">Script callbacks in ASP.NET are supported in any browser that supports making XMLHttp calls.</span></span> <span data-ttu-id="dd16a-471">これには、現在使用されているすべての最新のブラウザーが含まれます。</span><span class="sxs-lookup"><span data-stu-id="dd16a-471">That includes all of the modern browsers in use today.</span></span> <span data-ttu-id="dd16a-472">Internet Explorer は、XMLHttp ActiveX オブジェクトを使用しますが、その他の最新のブラウザー (今後の IE 7 を含む) は、組み込みの XMLHttp オブジェクトを使用します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-472">Internet Explorer uses the XMLHttp ActiveX object while other modern browsers (including the upcoming IE 7) use an intrinsic XMLHttp object.</span></span> <span data-ttu-id="dd16a-473">ブラウザーがコールバックをサポートしているかどうかをプログラムで判断するには、 **SupportCallback**プロパティを使用します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-473">To programmatically determine if a browser supports callbacks, you can use the **Request.Browser.SupportCallback** property.</span></span> <span data-ttu-id="dd16a-474">このプロパティは、要求元のクライアントがスクリプトコールバックをサポートしている場合に**true**を返します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-474">This property will return **true** if the requesting client supports script callbacks.</span></span>

## <a name="working-with-client-script-in-aspnet-20"></a><span data-ttu-id="dd16a-475">ASP.NET 2.0 でのクライアントスクリプトの使用</span><span class="sxs-lookup"><span data-stu-id="dd16a-475">Working with Client Script in ASP.NET 2.0</span></span>

<span data-ttu-id="dd16a-476">ASP.NET 2.0 のクライアントスクリプトは、ClientScriptManager クラスを使用して管理されます。</span><span class="sxs-lookup"><span data-stu-id="dd16a-476">Client scripts in ASP.NET 2.0 are managed via the use of the ClientScriptManager class.</span></span> <span data-ttu-id="dd16a-477">ClientScriptManager クラスは、型と名前を使用して、クライアントスクリプトを追跡します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-477">The ClientScriptManager class keeps track of client scripts using a type and a name.</span></span> <span data-ttu-id="dd16a-478">これにより、同じスクリプトが1ページに複数回、プログラムによって挿入されるのを防ぐことができます。</span><span class="sxs-lookup"><span data-stu-id="dd16a-478">This prevents the same script from being programmatically inserted on a page more than once.</span></span>

> [!NOTE]
> <span data-ttu-id="dd16a-479">ページにスクリプトが正常に登録されると、その後、同じスクリプトを登録しようとすると、スクリプトが2回目に登録されなくなるだけです。</span><span class="sxs-lookup"><span data-stu-id="dd16a-479">After a script has been successfully registered on a page, any subsequent attempt to register the same script will simply result in the script not being registered a second time.</span></span> <span data-ttu-id="dd16a-480">重複するスクリプトは追加されず、例外は発生しません。</span><span class="sxs-lookup"><span data-stu-id="dd16a-480">No duplicate scripts are added and no exception occurs.</span></span> <span data-ttu-id="dd16a-481">不要な計算を避けるために、スクリプトが既に登録されているかどうかを判断するために使用できるメソッドがあります。これにより、スクリプトを複数回登録することはできません。</span><span class="sxs-lookup"><span data-stu-id="dd16a-481">To avoid unnecessary computation, there are methods that you can use to determine if a script is already registered so that you do not attempt to register it more than once.</span></span>

<span data-ttu-id="dd16a-482">ClientScriptManager のメソッドは、現在のすべての ASP.NET 開発者を対象としています。</span><span class="sxs-lookup"><span data-stu-id="dd16a-482">The methods of the ClientScriptManager should be familiar to all current ASP.NET developers:</span></span>

## <a name="registerclientscriptblock"></a><span data-ttu-id="dd16a-483">RegisterClientScriptBlock</span><span class="sxs-lookup"><span data-stu-id="dd16a-483">RegisterClientScriptBlock</span></span>

<span data-ttu-id="dd16a-484">このメソッドは、レンダリングされたページの先頭にスクリプトを追加します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-484">This method adds a script to the top of the rendered page.</span></span> <span data-ttu-id="dd16a-485">これは、クライアントで明示的に呼び出される関数を追加する場合に便利です。</span><span class="sxs-lookup"><span data-stu-id="dd16a-485">This is useful for adding functions that will be explicitly called on the client.</span></span>

<span data-ttu-id="dd16a-486">このメソッドには、2つのオーバーロードされたバージョンがあります。</span><span class="sxs-lookup"><span data-stu-id="dd16a-486">There are two overloaded versions of this method.</span></span> <span data-ttu-id="dd16a-487">4つの引数のうち3つは共通です。</span><span class="sxs-lookup"><span data-stu-id="dd16a-487">Three of four arguments are common among them.</span></span> <span data-ttu-id="dd16a-488">これらは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="dd16a-488">They are:</span></span>

`type (string)`

<span data-ttu-id="dd16a-489">***型***引数は、スクリプトの型を識別します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-489">The ***type*** argument identifies a type for the script.</span></span> <span data-ttu-id="dd16a-490">一般に、このページの種類を使用することをお勧めします (これは、型に対して GetType ()) を使用します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-490">It is generally a good idea to use the page's type (this.GetType()) for the type.</span></span>

`key (string)`

<span data-ttu-id="dd16a-491">***キー***引数は、スクリプトのユーザー定義キーです。</span><span class="sxs-lookup"><span data-stu-id="dd16a-491">The ***key*** argument is a user-defined key for the script.</span></span> <span data-ttu-id="dd16a-492">これは、スクリプトごとに一意である必要があります。</span><span class="sxs-lookup"><span data-stu-id="dd16a-492">This should be unique for each script.</span></span> <span data-ttu-id="dd16a-493">既に追加されているスクリプトと同じキーおよび種類のスクリプトを追加しようとすると、そのスクリプトは追加されません。</span><span class="sxs-lookup"><span data-stu-id="dd16a-493">If you attempt to add a script with the same key and type of an already added script, it will not be added.</span></span>

`script (string)`

<span data-ttu-id="dd16a-494">***スクリプト***引数は、追加する実際のスクリプトを含む文字列です。</span><span class="sxs-lookup"><span data-stu-id="dd16a-494">The ***script*** argument is a string containing the actual script to add.</span></span> <span data-ttu-id="dd16a-495">StringBuilder を使用してスクリプトを作成した後、StringBuilder で ToString () メソッドを使用して***スクリプト***の引数を割り当てることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="dd16a-495">It's recommended that you use a StringBuilder to create the script and then use the ToString() method on the StringBuilder to assign the ***script*** argument.</span></span>

<span data-ttu-id="dd16a-496">3つの引数のみを受け取るオーバーロードされた RegisterClientScriptBlock を使用する場合は、スクリプトにスクリプト要素 (&lt;script&gt; と &lt;/script&gt;) を含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="dd16a-496">If you use the overloaded RegisterClientScriptBlock that only takes three arguments, you must include script elements (&lt;script&gt; and &lt;/script&gt;) in your script.</span></span>

<span data-ttu-id="dd16a-497">4番目の引数を受け取る RegisterClientScriptBlock のオーバーロードを使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="dd16a-497">You may choose to use the overload of RegisterClientScriptBlock that takes a fourth argument.</span></span> <span data-ttu-id="dd16a-498">4番目の引数は、ASP.NET がスクリプト要素を追加する必要があるかどうかを指定するブール値です。</span><span class="sxs-lookup"><span data-stu-id="dd16a-498">The fourth argument is a Boolean that specifies whether or not ASP.NET should add script elements for you.</span></span> <span data-ttu-id="dd16a-499">この引数が**true**の場合、スクリプトにはスクリプト要素を明示的に含めないでください。</span><span class="sxs-lookup"><span data-stu-id="dd16a-499">If this argument is **true**, your script should not include the script elements explicitly.</span></span>

<span data-ttu-id="dd16a-500">IsClientScriptBlockRegistered メソッドを使用して、スクリプトが既に登録されているかどうかを確認します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-500">Use the IsClientScriptBlockRegistered method to determine if a script has already been registered.</span></span> <span data-ttu-id="dd16a-501">これにより、既に登録されているスクリプトの再登録を避けることができます。</span><span class="sxs-lookup"><span data-stu-id="dd16a-501">This allows you to avoid an attempt to re-register a script that has already been registered.</span></span>

### <a name="registerclientscriptinclude-new-in-20"></a><span data-ttu-id="dd16a-502">RegisterClientScriptInclude (2.0 の新)</span><span class="sxs-lookup"><span data-stu-id="dd16a-502">RegisterClientScriptInclude (New in 2.0)</span></span>

<span data-ttu-id="dd16a-503">RegisterClientScriptInclude タグは、外部スクリプトファイルにリンクするスクリプトブロックを作成します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-503">The RegisterClientScriptInclude tag creates a script block that links to an external script file.</span></span> <span data-ttu-id="dd16a-504">2つのオーバーロードがあります。</span><span class="sxs-lookup"><span data-stu-id="dd16a-504">It has two overloads.</span></span> <span data-ttu-id="dd16a-505">1つはキーと URL を受け取ります。</span><span class="sxs-lookup"><span data-stu-id="dd16a-505">One takes a key and a URL.</span></span> <span data-ttu-id="dd16a-506">2番目の引数は、型を指定する3番目の引数を追加します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-506">The second adds a third argument specifying the type.</span></span>

<span data-ttu-id="dd16a-507">たとえば、次のコードでは、アプリケーションの scripts フォルダーのルートにある jsfunctions にリンクするスクリプトブロックが生成されます。</span><span class="sxs-lookup"><span data-stu-id="dd16a-507">For example, the following code generates a script block that links to jsfunctions.js in the root of the scripts folder of the application:</span></span>

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample17.cs)]

<span data-ttu-id="dd16a-508">このコードでは、表示されるページに次のコードが生成されます。</span><span class="sxs-lookup"><span data-stu-id="dd16a-508">This code produces the following code in the rendered page:</span></span>

[!code-html[Main](the-asp-net-2-0-page-model/samples/sample18.html)]

> [!NOTE]
> <span data-ttu-id="dd16a-509">スクリプトブロックはページの下部に表示されます。</span><span class="sxs-lookup"><span data-stu-id="dd16a-509">The script block is rendered at the bottom of the page.</span></span>

<span data-ttu-id="dd16a-510">Isclientscriptの登録解除メソッドを使用して、スクリプトが既に登録されているかどうかを確認します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-510">Use the IsClientScriptIncludeRegistered method to determine if a script has already been registered.</span></span> <span data-ttu-id="dd16a-511">これにより、スクリプトの再登録が試行されないようにすることができます。</span><span class="sxs-lookup"><span data-stu-id="dd16a-511">This allows you to avoid an attempt to re-register a script.</span></span>

## <a name="registerstartupscript"></a><span data-ttu-id="dd16a-512">RegisterStartupScript</span><span class="sxs-lookup"><span data-stu-id="dd16a-512">RegisterStartupScript</span></span>

<span data-ttu-id="dd16a-513">RegisterStartupScript メソッドは、RegisterClientScriptBlock メソッドと同じ引数を受け取ります。</span><span class="sxs-lookup"><span data-stu-id="dd16a-513">The RegisterStartupScript method takes the same arguments as the RegisterClientScriptBlock method.</span></span> <span data-ttu-id="dd16a-514">RegisterStartupScript に登録されているスクリプトは、ページが読み込まれた後、OnLoad クライアント側のイベントの前に実行されます。</span><span class="sxs-lookup"><span data-stu-id="dd16a-514">A script registered with RegisterStartupScript executes after the page loads but before the OnLoad client-side event.</span></span> <span data-ttu-id="dd16a-515">1\.x では、RegisterStartupScript に登録されているスクリプトは、RegisterClientScriptBlock に登録されているスクリプトが、開始 &lt;フォーム&gt; タグの直後に配置されている間に、終了 &lt;/&gt; タグの直前に配置されました。</span><span class="sxs-lookup"><span data-stu-id="dd16a-515">In 1.X, scripts registered with RegisterStartupScript were placed just before the closing &lt;/form&gt; tag while scripts registered with RegisterClientScriptBlock were placed immediately after the opening &lt;form&gt; tag.</span></span> <span data-ttu-id="dd16a-516">ASP.NET 2.0 では、両方とも、終了 &lt;/&gt; タグの直前に配置されます。</span><span class="sxs-lookup"><span data-stu-id="dd16a-516">In ASP.NET 2.0, both are placed immediately before the closing &lt;/form&gt; tag.</span></span>

> [!NOTE]
> <span data-ttu-id="dd16a-517">RegisterStartupScript に関数を登録すると、その関数は、クライアント側のコードで明示的に呼び出されるまで実行されません。</span><span class="sxs-lookup"><span data-stu-id="dd16a-517">If you register a function with RegisterStartupScript, that function will not execute until you explicitly call it in client-side code.</span></span>

<span data-ttu-id="dd16a-518">IsStartupScriptRegistered メソッドを使用して、スクリプトが既に登録されているかどうかを確認し、スクリプトの再登録を試行しないようにします。</span><span class="sxs-lookup"><span data-stu-id="dd16a-518">Use the IsStartupScriptRegistered method to determine if a script has already been registered and avoid an attempt to re-register a script.</span></span>

## <a name="other-clientscriptmanager-methods"></a><span data-ttu-id="dd16a-519">その他の ClientScriptManager メソッド</span><span class="sxs-lookup"><span data-stu-id="dd16a-519">Other ClientScriptManager Methods</span></span>

<span data-ttu-id="dd16a-520">ClientScriptManager クラスのその他の便利なメソッドの一部を次に示します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-520">Here are some of the other useful methods of the ClientScriptManager class.</span></span>

|  <span data-ttu-id="dd16a-521"><strong>GetCallbackEventReference</strong></span><span class="sxs-lookup"><span data-stu-id="dd16a-521"><strong>GetCallbackEventReference</strong></span></span>   |                                                 <span data-ttu-id="dd16a-522">このモジュールの「スクリプトコールバック」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="dd16a-522">See script callbacks earlier in this module.</span></span>                                                 |
|-----------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
|  <span data-ttu-id="dd16a-523"><strong>GetPostBackClientHyperlink</strong></span><span class="sxs-lookup"><span data-stu-id="dd16a-523"><strong>GetPostBackClientHyperlink</strong></span></span>  |                <span data-ttu-id="dd16a-524">クライアント側のイベントからポストバックするために使用できる JavaScript 参照 (javascript:&lt;呼び出し&gt;) を取得します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-524">Gets a JavaScript reference (javascript:&lt;call&gt;) that can be used to post back from a client-side event.</span></span>                 |
|  <span data-ttu-id="dd16a-525"><strong>System.web.ui.clientscriptmanager.getpostbackeventreference</strong></span><span class="sxs-lookup"><span data-stu-id="dd16a-525"><strong>GetPostBackEventReference</strong></span></span>   |                                   <span data-ttu-id="dd16a-526">クライアントからポストバックを開始するために使用できる文字列を取得します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-526">Gets a string that can be used to initiate a post back from the client.</span></span>                                    |
|      <span data-ttu-id="dd16a-527"><strong>GetWebResourceUrl</strong></span><span class="sxs-lookup"><span data-stu-id="dd16a-527"><strong>GetWebResourceUrl</strong></span></span>       | <span data-ttu-id="dd16a-528">アセンブリに埋め込まれているリソースへの URL を返します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-528">Returns a URL to a resource that is embedded in an assembly.</span></span> <span data-ttu-id="dd16a-529"><strong>RegisterClientScriptResource</strong>と組み合わせて使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="dd16a-529">Must be used in conjunction with <strong>RegisterClientScriptResource</strong>.</span></span> |
| <span data-ttu-id="dd16a-530"><strong>RegisterClientScriptResource</strong></span><span class="sxs-lookup"><span data-stu-id="dd16a-530"><strong>RegisterClientScriptResource</strong></span></span> |     <span data-ttu-id="dd16a-531">Web リソースをページに登録します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-531">Registers a Web resource with the page.</span></span> <span data-ttu-id="dd16a-532">これらは、アセンブリに埋め込まれ、新しい Webresource.axd ハンドラーによって処理されるリソースです。</span><span class="sxs-lookup"><span data-stu-id="dd16a-532">These are resources embedded in an assembly and handled by the new WebResource.axd handler.</span></span>      |
|     <span data-ttu-id="dd16a-533"><strong>RegisterHiddenField</strong></span><span class="sxs-lookup"><span data-stu-id="dd16a-533"><strong>RegisterHiddenField</strong></span></span>      |                                                 <span data-ttu-id="dd16a-534">非表示のフォームフィールドをページに登録します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-534">Registers a hidden form field with the page.</span></span>                                                 |
|  <span data-ttu-id="dd16a-535"><strong>RegisterOnSubmitStatement</strong></span><span class="sxs-lookup"><span data-stu-id="dd16a-535"><strong>RegisterOnSubmitStatement</strong></span></span>   |                                  <span data-ttu-id="dd16a-536">HTML フォームの送信時に実行されるクライアント側のコードを登録します。</span><span class="sxs-lookup"><span data-stu-id="dd16a-536">Registers client-side code that executes when the HTML form is submitted.</span></span>                                   |
