---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/aspnet-error-handling
title: ASP.NET のエラー処理 |Microsoft Docs
author: Erikre
description: このチュートリアルシリーズでは、ASP.NET 4.5 と Microsoft Visual Studio Express 2013 を使用して ASP.NET Web フォームアプリケーションを構築するための基本について説明します。
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 423498f7-1a4b-44a1-b342-5f39d0bcf94f
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/aspnet-error-handling
msc.type: authoredcontent
ms.openlocfilehash: f420be369801208fa875d9a60e6e154afbe84aa7
ms.sourcegitcommit: b67ffd5b2c5cff01ec4c8eb12a21f693f2e11887
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/23/2019
ms.locfileid: "69995314"
---
# <a name="aspnet-error-handling"></a><span data-ttu-id="66a32-103">ASP.NET エラー処理</span><span class="sxs-lookup"><span data-stu-id="66a32-103">ASP.NET Error Handling</span></span>

<span data-ttu-id="66a32-104">[Erik Reitan](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="66a32-104">by [Erik Reitan](https://github.com/Erikre)</span></span>

<span data-ttu-id="66a32-105">[Wingtip Toys のサンプル プロジェクト (C#) をダウンロード](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)または[電子書籍 (PDF) をダウンロード](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span><span class="sxs-lookup"><span data-stu-id="66a32-105">[Download Wingtip Toys Sample Project (C#)](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) or [Download E-book (PDF)](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span></span>

> <span data-ttu-id="66a32-106">このチュートリアルシリーズでは、ASP.NET 4.5 を使用して ASP.NET Web フォームアプリケーションを構築するための基礎と、Web 用の Microsoft Visual Studio Express 2013 について説明します。</span><span class="sxs-lookup"><span data-stu-id="66a32-106">This tutorial series will teach you the basics of building an ASP.NET Web Forms application using ASP.NET 4.5 and Microsoft Visual Studio Express 2013 for Web.</span></span> <span data-ttu-id="66a32-107">Visual Studio 2013[プロジェクトと C# ソース コード](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)このチュートリアル シリーズをと共に使用できます。</span><span class="sxs-lookup"><span data-stu-id="66a32-107">A Visual Studio 2013 [project with C# source code](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) is available to accompany this tutorial series.</span></span>

<span data-ttu-id="66a32-108">このチュートリアルでは、Wingtip Toys サンプルアプリケーションを変更して、エラー処理とエラーログを含めます。</span><span class="sxs-lookup"><span data-stu-id="66a32-108">In this tutorial, you will modify the Wingtip Toys sample application to include error handling and error logging.</span></span> <span data-ttu-id="66a32-109">エラー処理により、アプリケーションはエラーを適切に処理し、それに応じてエラーメッセージを表示できます。</span><span class="sxs-lookup"><span data-stu-id="66a32-109">Error handling will allow the application to gracefully handle errors and display error messages accordingly.</span></span> <span data-ttu-id="66a32-110">エラーログを使用すると、発生したエラーを検出して修正することができます。</span><span class="sxs-lookup"><span data-stu-id="66a32-110">Error logging will allow you to find and fix errors that have occurred.</span></span> <span data-ttu-id="66a32-111">このチュートリアルは、前の「URL ルーティング」チュートリアルに基づいており、Wingtip Toys チュートリアルシリーズの一部です。</span><span class="sxs-lookup"><span data-stu-id="66a32-111">This tutorial builds on the previous tutorial "URL Routing" and is part of the Wingtip Toys tutorial series.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="66a32-112">学習内容:</span><span class="sxs-lookup"><span data-stu-id="66a32-112">What you'll learn:</span></span>

- <span data-ttu-id="66a32-113">アプリケーションの構成にグローバルエラー処理を追加する方法。</span><span class="sxs-lookup"><span data-stu-id="66a32-113">How to add global error handling to the application's configuration.</span></span>
- <span data-ttu-id="66a32-114">アプリケーション、ページ、およびコードレベルでエラー処理を追加する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="66a32-114">How to add error handling at the application, page, and code levels.</span></span>
- <span data-ttu-id="66a32-115">後で確認するためにエラーをログに記録する方法。</span><span class="sxs-lookup"><span data-stu-id="66a32-115">How to log errors for later review.</span></span>
- <span data-ttu-id="66a32-116">セキュリティを損なうことのないエラーメッセージを表示する方法。</span><span class="sxs-lookup"><span data-stu-id="66a32-116">How to display error messages that do not compromise security.</span></span>
- <span data-ttu-id="66a32-117">エラーログモジュールとハンドラー (ELMAH) のエラーログを実装する方法。</span><span class="sxs-lookup"><span data-stu-id="66a32-117">How to implement Error Logging Modules and Handlers (ELMAH) error logging.</span></span>

## <a name="overview"></a><span data-ttu-id="66a32-118">概要</span><span class="sxs-lookup"><span data-stu-id="66a32-118">Overview</span></span>

<span data-ttu-id="66a32-119">ASP.NET アプリケーションは、実行中に発生したエラーを一貫した方法で処理できる必要があります。</span><span class="sxs-lookup"><span data-stu-id="66a32-119">ASP.NET applications must be able to handle errors that occur during execution in a consistent manner.</span></span> <span data-ttu-id="66a32-120">ASP.NET は、共通言語ランタイム (CLR) を使用します。これにより、一貫した方法でアプリケーションにエラーを通知することができます。</span><span class="sxs-lookup"><span data-stu-id="66a32-120">ASP.NET uses the common language runtime (CLR), which provides a way of notifying applications of errors in a uniform way.</span></span> <span data-ttu-id="66a32-121">エラーが発生すると、例外がスローされます。</span><span class="sxs-lookup"><span data-stu-id="66a32-121">When an error occurs, an exception is thrown.</span></span> <span data-ttu-id="66a32-122">例外とは、アプリケーションで発生したエラー、条件、または予期しない動作のことです。</span><span class="sxs-lookup"><span data-stu-id="66a32-122">An exception is any error, condition, or unexpected behavior that an application encounters.</span></span>

<span data-ttu-id="66a32-123">.NET Framework では、例外は `System.Exception` クラスから継承されるオブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="66a32-123">In the .NET Framework, an exception is an object that inherits from the `System.Exception` class.</span></span> <span data-ttu-id="66a32-124">例外は問題が発生したコード領域からスローされます。</span><span class="sxs-lookup"><span data-stu-id="66a32-124">An exception is thrown from an area of code where a problem has occurred.</span></span> <span data-ttu-id="66a32-125">例外は、例外を処理するコードがアプリケーションによって提供される場所に、呼び出し履歴が渡されます。</span><span class="sxs-lookup"><span data-stu-id="66a32-125">The exception is passed up the call stack to a place where the application provides code to handle the exception.</span></span> <span data-ttu-id="66a32-126">アプリケーションが例外を処理しない場合、ブラウザーはエラーの詳細を表示するように強制されます。</span><span class="sxs-lookup"><span data-stu-id="66a32-126">If the application does not handle the exception, the browser is forced to display the error details.</span></span>

<span data-ttu-id="66a32-127">ベストプラクティスとして、コード内の`Try`ブロックの/ `Catch` / `Finally`コードレベルでのエラーを処理することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="66a32-127">As a best practice, handle errors in at the code level in `Try`/`Catch`/`Finally` blocks within your code.</span></span> <span data-ttu-id="66a32-128">ユーザーが発生したコンテキストで問題を修正できるように、これらのブロックを配置してみてください。</span><span class="sxs-lookup"><span data-stu-id="66a32-128">Try to place these blocks so that the user can correct problems in the context in which they occur.</span></span> <span data-ttu-id="66a32-129">エラー処理ブロックがエラーが発生した場所から離れすぎている場合は、問題を修正するために必要な情報をユーザーに提供することが難しくなります。</span><span class="sxs-lookup"><span data-stu-id="66a32-129">If the error handling blocks are too far away from where the error occurred, it becomes more difficult to provide users with the information they need to fix the problem.</span></span>

### <a name="exception-class"></a><span data-ttu-id="66a32-130">Exception クラス</span><span class="sxs-lookup"><span data-stu-id="66a32-130">Exception Class</span></span>

<span data-ttu-id="66a32-131">Exception クラスは、例外の継承元となる基本クラスです。</span><span class="sxs-lookup"><span data-stu-id="66a32-131">The Exception class is the base class from which exceptions inherit.</span></span> <span data-ttu-id="66a32-132">ほとんどの例外オブジェクトは、 `SystemException`クラス`IndexOutOfRangeException` 、クラス`ArgumentNullException` 、クラスなど、例外クラスの派生クラスのインスタンスです。</span><span class="sxs-lookup"><span data-stu-id="66a32-132">Most exception objects are instances of some derived class of the Exception class, such as the `SystemException` class, the `IndexOutOfRangeException` class, or the `ArgumentNullException` class.</span></span> <span data-ttu-id="66a32-133">Exception クラスには、発生したエラー `StackTrace`に関する特定の情報を提供`Message`するプロパティ、プロパティ、プロパティなどのプロパティ`InnerException`があります。</span><span class="sxs-lookup"><span data-stu-id="66a32-133">The Exception class has properties, such as the `StackTrace` property, the `InnerException` property, and the `Message` property, that provide specific information about the error that has occurred.</span></span>

### <a name="exception-inheritance-hierarchy"></a><span data-ttu-id="66a32-134">例外の継承階層</span><span class="sxs-lookup"><span data-stu-id="66a32-134">Exception Inheritance Hierarchy</span></span>

<span data-ttu-id="66a32-135">ランタイムには、例外が発生したときに`SystemException`ランタイムがスローするクラスから派生した例外の基本セットがあります。</span><span class="sxs-lookup"><span data-stu-id="66a32-135">The runtime has a base set of exceptions deriving from the `SystemException` class that the runtime throws when an exception is encountered.</span></span> <span data-ttu-id="66a32-136">`IndexOutOfRangeException` クラス`ArgumentNullException`やクラスなど、例外クラスを継承するほとんどのクラスは、追加のメンバーを実装しません。</span><span class="sxs-lookup"><span data-stu-id="66a32-136">Most of the classes that inherit from the Exception class, such as the `IndexOutOfRangeException` class and the `ArgumentNullException` class, do not implement additional members.</span></span> <span data-ttu-id="66a32-137">そのため、例外の最も重要な情報は、例外の階層、例外の名前、および例外に含まれる情報にあります。</span><span class="sxs-lookup"><span data-stu-id="66a32-137">Therefore, the most important information for an exception can be found in the hierarchy of exceptions, the exception name, and the information contained in the exception.</span></span>

### <a name="exception-handling-hierarchy"></a><span data-ttu-id="66a32-138">例外処理の階層</span><span class="sxs-lookup"><span data-stu-id="66a32-138">Exception Handling Hierarchy</span></span>

<span data-ttu-id="66a32-139">ASP.NET Web フォームアプリケーションでは、特定の処理階層に基づいて例外を処理できます。</span><span class="sxs-lookup"><span data-stu-id="66a32-139">In an ASP.NET Web Forms application, exceptions can be handled based on a specific handling hierarchy.</span></span> <span data-ttu-id="66a32-140">例外は、次のレベルで処理できます。</span><span class="sxs-lookup"><span data-stu-id="66a32-140">An exception can be handled at the following levels:</span></span>

- <span data-ttu-id="66a32-141">アプリケーションレベル</span><span class="sxs-lookup"><span data-stu-id="66a32-141">Application level</span></span>
- <span data-ttu-id="66a32-142">ページレベルのロック</span><span class="sxs-lookup"><span data-stu-id="66a32-142">Page level</span></span>
- <span data-ttu-id="66a32-143">コードレベル</span><span class="sxs-lookup"><span data-stu-id="66a32-143">Code level</span></span>

<span data-ttu-id="66a32-144">アプリケーションで例外を処理する場合、例外クラスから継承された例外に関する追加情報を取得して、ユーザーに表示できます。</span><span class="sxs-lookup"><span data-stu-id="66a32-144">When an application handles exceptions, additional information about the exception that is inherited from the Exception class can often be retrieved and displayed to the user.</span></span> <span data-ttu-id="66a32-145">アプリケーション、ページ、およびコードレベルに加えて、HTTP モジュールレベルおよび IIS カスタムハンドラーを使用して例外を処理することもできます。</span><span class="sxs-lookup"><span data-stu-id="66a32-145">In addition to application, page, and code level, you can also handle exceptions at the HTTP module level and by using an IIS custom handler.</span></span>

### <a name="application-level-error-handling"></a><span data-ttu-id="66a32-146">アプリケーションレベルのエラー処理</span><span class="sxs-lookup"><span data-stu-id="66a32-146">Application Level Error Handling</span></span>

<span data-ttu-id="66a32-147">アプリケーションの構成を変更するか、アプリケーションの`Application_Error` *global.asax*ファイルにハンドラーを追加することで、アプリケーションレベルで既定のエラーを処理できます。</span><span class="sxs-lookup"><span data-stu-id="66a32-147">You can handle default errors at the application level either by modifying your application's configuration or by adding an `Application_Error` handler in the *Global.asax* file of your application.</span></span>

<span data-ttu-id="66a32-148">Web.config ファイルにセクションを`customErrors`追加することによって、既定のエラーと HTTP エラーを処理できます。</span><span class="sxs-lookup"><span data-stu-id="66a32-148">You can handle default errors and HTTP errors by adding a `customErrors` section to the *Web.config* file.</span></span> <span data-ttu-id="66a32-149">この`customErrors`セクションでは、エラーが発生したときにユーザーがリダイレクトされる既定のページを指定できます。</span><span class="sxs-lookup"><span data-stu-id="66a32-149">The `customErrors` section allows you to specify a default page that users will be redirected to when an error occurs.</span></span> <span data-ttu-id="66a32-150">また、特定のステータスコードエラーのページを個別に指定することもできます。</span><span class="sxs-lookup"><span data-stu-id="66a32-150">It also allows you to specify individual pages for specific status code errors.</span></span>

[!code-xml[Main](aspnet-error-handling/samples/sample1.xml?highlight=3-5)]

<span data-ttu-id="66a32-151">残念ながら、構成を使用してユーザーを別のページにリダイレクトすると、発生したエラーの詳細は表示されません。</span><span class="sxs-lookup"><span data-stu-id="66a32-151">Unfortunately, when you use the configuration to redirect the user to a different page, you do not have the details of the error that occurred.</span></span>

<span data-ttu-id="66a32-152">ただし、 `Application_Error` *global.asax*ファイルのハンドラーにコードを追加することで、アプリケーション内の任意の場所で発生したエラーをトラップできます。</span><span class="sxs-lookup"><span data-stu-id="66a32-152">However, you can trap errors that occur anywhere in your application by adding code to the `Application_Error` handler in the *Global.asax* file.</span></span>

[!code-csharp[Main](aspnet-error-handling/samples/sample2.cs)]

### <a name="page-level-error-event-handling"></a><span data-ttu-id="66a32-153">ページレベルのエラーイベントの処理</span><span class="sxs-lookup"><span data-stu-id="66a32-153">Page Level Error Event Handling</span></span>

<span data-ttu-id="66a32-154">ページレベルのハンドラーは、エラーが発生したページにユーザーを返しますが、コントロールのインスタンスは保持されないため、ページ上の何も表示されなくなります。</span><span class="sxs-lookup"><span data-stu-id="66a32-154">A page-level handler returns the user to the page where the error occurred, but because instances of controls are not maintained, there will no longer be anything on the page.</span></span> <span data-ttu-id="66a32-155">アプリケーションのユーザーにエラーの詳細を提供するには、エラーの詳細をページに明示的に書き込む必要があります。</span><span class="sxs-lookup"><span data-stu-id="66a32-155">To provide the error details to the user of the application, you must specifically write the error details to the page.</span></span>

<span data-ttu-id="66a32-156">通常は、ページレベルのエラーハンドラーを使用して、未処理のエラーをログに記録するか、役に立つ情報を表示できるページに移動します。</span><span class="sxs-lookup"><span data-stu-id="66a32-156">You would typically use a page-level error handler to log unhandled errors or to take the user to a page that can display helpful information.</span></span>

<span data-ttu-id="66a32-157">このコード例では、ASP.NET Web ページの Error イベントのハンドラーを示します。</span><span class="sxs-lookup"><span data-stu-id="66a32-157">This code example shows a handler for the Error event in an ASP.NET Web page.</span></span> <span data-ttu-id="66a32-158">このハンドラーは、ページ内のブロック内`try` / `catch`でまだ処理されていないすべての例外をキャッチします。</span><span class="sxs-lookup"><span data-stu-id="66a32-158">This handler catches all exceptions that are not already handled within `try`/`catch` blocks in the page.</span></span>

[!code-csharp[Main](aspnet-error-handling/samples/sample3.cs)]

<span data-ttu-id="66a32-159">エラーを処理した後、サーバーオブジェクト ( `ClearError` `HttpServerUtility`クラス) のメソッドを呼び出すことによって、エラーをクリアする必要があります。そうしないと、以前に発生したエラーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="66a32-159">After you handle an error, you must clear it by calling the `ClearError` method of the Server object (`HttpServerUtility` class), otherwise you will see an error that has previously occurred.</span></span>

### <a name="code-level-error-handling"></a><span data-ttu-id="66a32-160">コードレベルのエラー処理</span><span class="sxs-lookup"><span data-stu-id="66a32-160">Code Level Error Handling</span></span>

<span data-ttu-id="66a32-161">Try-catch ステートメントは、try ブロックとそれに続く1つ以上の catch 句で構成されます。これは、さまざまな例外のハンドラーを指定します。</span><span class="sxs-lookup"><span data-stu-id="66a32-161">The try-catch statement consists of a try block followed by one or more catch clauses, which specify handlers for different exceptions.</span></span> <span data-ttu-id="66a32-162">例外がスローされると、共通言語ランタイム (CLR) は、この例外を処理する catch ステートメントを検索します。</span><span class="sxs-lookup"><span data-stu-id="66a32-162">When an exception is thrown, the common language runtime (CLR) looks for the catch statement that handles this exception.</span></span> <span data-ttu-id="66a32-163">現在実行中のメソッドに catch ブロックが含まれていない場合、CLR は現在のメソッドを呼び出したメソッドを参照します。</span><span class="sxs-lookup"><span data-stu-id="66a32-163">If the currently executing method does not contain a catch block, the CLR looks at the method that called the current method, and so on, up the call stack.</span></span> <span data-ttu-id="66a32-164">Catch ブロックが見つからない場合、CLR はハンドルされない例外メッセージをユーザーに表示し、プログラムの実行を停止します。</span><span class="sxs-lookup"><span data-stu-id="66a32-164">If no catch block is found, then the CLR displays an unhandled exception message to the user and stops execution of the program.</span></span>

<span data-ttu-id="66a32-165">次のコード例は、を使用して`try`エラーを処理する一般的な方法を示して/ / `catch` `finally`います。</span><span class="sxs-lookup"><span data-stu-id="66a32-165">The following code example shows a common way of using `try`/`catch`/`finally` to handle errors.</span></span>

[!code-csharp[Main](aspnet-error-handling/samples/sample4.cs)]

<span data-ttu-id="66a32-166">上記のコードでは、try ブロックには、考えられる例外に対して保護する必要があるコードが含まれています。</span><span class="sxs-lookup"><span data-stu-id="66a32-166">In the above code, the try block contains the code that needs to be guarded against a possible exception.</span></span> <span data-ttu-id="66a32-167">ブロックは、例外がスローされるか、ブロックが正常に完了するまで実行されます。</span><span class="sxs-lookup"><span data-stu-id="66a32-167">The block is executed until either an exception is thrown or the block is completed successfully.</span></span> <span data-ttu-id="66a32-168">`FileNotFoundException`例外または例外が発生した場合、実行は別のページに`IOException`転送されます。</span><span class="sxs-lookup"><span data-stu-id="66a32-168">If either a `FileNotFoundException` exception or an `IOException` exception occurs, the execution is transferred to a different page.</span></span> <span data-ttu-id="66a32-169">次に、finally ブロックに含まれているコードが、エラーが発生したかどうかにかかわらず実行されます。</span><span class="sxs-lookup"><span data-stu-id="66a32-169">Then, the code contained in the finally block is executed, whether an error occurred or not.</span></span>

## <a name="adding-error-logging-support"></a><span data-ttu-id="66a32-170">エラーログのサポートの追加</span><span class="sxs-lookup"><span data-stu-id="66a32-170">Adding Error Logging Support</span></span>

<span data-ttu-id="66a32-171">Wingtip Toys サンプルアプリケーションにエラー処理を追加する前に、クラスを`ExceptionUtility` *Logic*フォルダーに追加することによって、エラーログのサポートを追加します。</span><span class="sxs-lookup"><span data-stu-id="66a32-171">Before adding error handling to the Wingtip Toys sample application, you will add error logging support by adding an `ExceptionUtility` class to the *Logic* folder.</span></span> <span data-ttu-id="66a32-172">これにより、アプリケーションがエラーを処理するたびにエラーの詳細がエラーログファイルに追加されます。</span><span class="sxs-lookup"><span data-stu-id="66a32-172">By doing this, each time the application handles an error, the error details will be added to the error log file.</span></span>

1. <span data-ttu-id="66a32-173">*Logic*フォルダーを右クリックし、[**新しい項目**の**追加** - &gt; ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="66a32-173">Right-click the *Logic* folder and then select **Add** -&gt; **New Item**.</span></span>   
   <span data-ttu-id="66a32-174">**[新しい項目の追加]** ダイアログ ボックスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="66a32-174">The **Add New Item** dialog box is displayed.</span></span>
2. <span data-ttu-id="66a32-175">左側の **[ C#ビジュアル**  -コードテンプレート] グループを選択します。 &gt;</span><span class="sxs-lookup"><span data-stu-id="66a32-175">Select the **Visual C#** -&gt; **Code** templates group on the left.</span></span> <span data-ttu-id="66a32-176">次に、中央の一覧から **[クラス]** を選択し、「 **ExceptionUtility.cs**」という名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="66a32-176">Then, select **Class**from the middle list and name it **ExceptionUtility.cs**.</span></span>
3. <span data-ttu-id="66a32-177">**[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="66a32-177">Choose **Add**.</span></span> <span data-ttu-id="66a32-178">新しいクラスファイルが表示されます。</span><span class="sxs-lookup"><span data-stu-id="66a32-178">The new class file is displayed.</span></span>
4. <span data-ttu-id="66a32-179">既存のコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="66a32-179">Replace the existing code with the following:</span></span>  

    [!code-csharp[Main](aspnet-error-handling/samples/sample5.cs)]

<span data-ttu-id="66a32-180">例外が発生した場合、 `LogException`メソッドを呼び出すことによって例外を例外ログファイルに書き込むことができます。</span><span class="sxs-lookup"><span data-stu-id="66a32-180">When an exception occurs, the exception can be written to an exception log file by calling the `LogException` method.</span></span> <span data-ttu-id="66a32-181">このメソッドは、例外オブジェクトと、例外の原因の詳細を含む文字列の2つのパラメーターを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="66a32-181">This method takes two parameters, the exception object and a string containing details about the source of the exception.</span></span> <span data-ttu-id="66a32-182">例外ログは、 *\_アプリデータ*フォルダー内の*エラー*ログファイルに書き込まれます。</span><span class="sxs-lookup"><span data-stu-id="66a32-182">The exception log is written to the *ErrorLog.txt* file in the *App\_Data* folder.</span></span>

### <a name="adding-an-error-page"></a><span data-ttu-id="66a32-183">エラーページの追加</span><span class="sxs-lookup"><span data-stu-id="66a32-183">Adding an Error Page</span></span>

<span data-ttu-id="66a32-184">Wingtip Toys サンプルアプリケーションでは、1つのページを使用してエラーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="66a32-184">In the Wingtip Toys sample application, one page will be used to display errors.</span></span> <span data-ttu-id="66a32-185">このエラーページは、サイトのユーザーにセキュリティで保護されたエラーメッセージを表示するように設計されています。</span><span class="sxs-lookup"><span data-stu-id="66a32-185">The error page is designed to show a secure error message to users of the site.</span></span> <span data-ttu-id="66a32-186">ただし、ユーザーが、コードが存在するコンピューターでローカルに提供されている HTTP 要求を行う開発者の場合は、エラーページに追加のエラーの詳細が表示されます。</span><span class="sxs-lookup"><span data-stu-id="66a32-186">However, if the user is a developer making an HTTP request that is being served locally on the machine where the code lives, additional error details will be displayed on the error page.</span></span>

1. <span data-ttu-id="66a32-187">**ソリューションエクスプローラー**でプロジェクト名 (**Wingtip Toys**) を右クリックし、[**新しい項目**の**追加** - &gt; ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="66a32-187">Right-click the project name (**Wingtip Toys**) in **Solution Explorer** and select **Add** -&gt; **New Item**.</span></span>   
   <span data-ttu-id="66a32-188">**[新しい項目の追加]** ダイアログ ボックスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="66a32-188">The **Add New Item** dialog box is displayed.</span></span>
2. <span data-ttu-id="66a32-189">選択、 **Visual C#**  - &gt; **Web**左側のテンプレート グループ。</span><span class="sxs-lookup"><span data-stu-id="66a32-189">Select the **Visual C#** -&gt; **Web** templates group on the left.</span></span> <span data-ttu-id="66a32-190">中央の一覧で **[マスターページを使用した Web フォーム]** を選択し、「 **errorpage .aspx**」という名前を付けます。</span><span class="sxs-lookup"><span data-stu-id="66a32-190">From the middle list, select **Web Form with Master Page**,and name it **ErrorPage.aspx**.</span></span>
3. <span data-ttu-id="66a32-191">**[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="66a32-191">Click **Add**.</span></span>
4. <span data-ttu-id="66a32-192">マスターページとして [] を選択し、[ **OK]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="66a32-192">Select the *Site.Master* file as the master page, and then choose **OK**.</span></span>
5. <span data-ttu-id="66a32-193">既存のマークアップを次のように置き換えます。</span><span class="sxs-lookup"><span data-stu-id="66a32-193">Replace the existing markup with the following:</span></span>   

    [!code-aspx[Main](aspnet-error-handling/samples/sample6.aspx)]
6. <span data-ttu-id="66a32-194">次のように、分離コード (*ErrorPage.aspx.cs*) の既存のコードを置き換えます。</span><span class="sxs-lookup"><span data-stu-id="66a32-194">Replace the existing code of the code-behind (*ErrorPage.aspx.cs*) so that it appears as follows:</span></span>   

    [!code-csharp[Main](aspnet-error-handling/samples/sample7.cs)]

<span data-ttu-id="66a32-195">エラーページが表示`Page_Load`されると、イベントハンドラーが実行されます。</span><span class="sxs-lookup"><span data-stu-id="66a32-195">When the error page is displayed, the `Page_Load` event handler is executed.</span></span> <span data-ttu-id="66a32-196">`Page_Load`ハンドラーでは、エラーが最初に処理された場所が決定されます。</span><span class="sxs-lookup"><span data-stu-id="66a32-196">In the `Page_Load` handler, the location of where the error was first handled is determined.</span></span> <span data-ttu-id="66a32-197">その後、発生した最後のエラーは、サーバー `GetLastError`オブジェクトのメソッドを呼び出すことによって決定されます。</span><span class="sxs-lookup"><span data-stu-id="66a32-197">Then, the last error that occurred is determined by call the `GetLastError` method of the Server object.</span></span> <span data-ttu-id="66a32-198">例外が既に存在しない場合は、汎用的な例外が作成されます。</span><span class="sxs-lookup"><span data-stu-id="66a32-198">If the exception no longer exists, a generic exception is created.</span></span> <span data-ttu-id="66a32-199">その後、HTTP 要求がローカルに作成された場合は、すべてのエラーの詳細が表示されます。</span><span class="sxs-lookup"><span data-stu-id="66a32-199">Then, if the HTTP request was made locally, all error details are shown.</span></span> <span data-ttu-id="66a32-200">この場合、web アプリケーションを実行しているローカルコンピューターにのみ、これらのエラーの詳細が表示されます。</span><span class="sxs-lookup"><span data-stu-id="66a32-200">In this case, only the local machine running the web application will see these error details.</span></span> <span data-ttu-id="66a32-201">エラー情報が表示されると、エラーがログファイルに追加され、サーバーからエラーがクリアされます。</span><span class="sxs-lookup"><span data-stu-id="66a32-201">After the error information has been displayed, the error is added to the log file and the error is cleared from the server.</span></span>

### <a name="displaying-unhandled-error-messages-for-the-application"></a><span data-ttu-id="66a32-202">アプリケーションの未処理のエラーメッセージを表示する</span><span class="sxs-lookup"><span data-stu-id="66a32-202">Displaying Unhandled Error Messages for the Application</span></span>

<span data-ttu-id="66a32-203">Web.config ファイルに`customErrors`セクションを追加することで、アプリケーション全体で発生する単純なエラーを迅速に処理できます。</span><span class="sxs-lookup"><span data-stu-id="66a32-203">By adding a `customErrors` section to the *Web.config* file, you can quickly handle simple errors that occur throughout the application.</span></span> <span data-ttu-id="66a32-204">また、404-ファイルが見つからないなどのステータスコード値に基づいて、エラーの処理方法を指定することもできます。</span><span class="sxs-lookup"><span data-stu-id="66a32-204">You can also specify how to handle errors based on their status code value, such as 404 - File not found.</span></span>

#### <a name="update-the-configuration"></a><span data-ttu-id="66a32-205">構成を更新する</span><span class="sxs-lookup"><span data-stu-id="66a32-205">Update the Configuration</span></span>

<span data-ttu-id="66a32-206">Web.config ファイルにセクションを`customErrors`追加して、構成を更新します。</span><span class="sxs-lookup"><span data-stu-id="66a32-206">Update the configuration by adding a `customErrors` section to the *Web.config* file.</span></span>

1. <span data-ttu-id="66a32-207">**ソリューションエクスプローラー**で、Wingtip Toys サンプルアプリケーションのルートにある*web.config*ファイルを見つけて開きます。</span><span class="sxs-lookup"><span data-stu-id="66a32-207">In **Solution Explorer**, find and open the *Web.config* file at the root of the Wingtip Toys sample application.</span></span>
2. <span data-ttu-id="66a32-208">次の`customErrors`ように、 `<system.web>`ノード内の web.config ファイルにセクションを追加します。</span><span class="sxs-lookup"><span data-stu-id="66a32-208">Add the `customErrors` section to the *Web.config* file within the `<system.web>` node as follows:</span></span>   

    [!code-xml[Main](aspnet-error-handling/samples/sample8.xml?highlight=3-5)]
3. <span data-ttu-id="66a32-209">Web.config ファイルを保存します。</span><span class="sxs-lookup"><span data-stu-id="66a32-209">Save the *Web.config* file.</span></span>

<span data-ttu-id="66a32-210">`customErrors`セクションでは、モードを指定します。これは "On" に設定されています。</span><span class="sxs-lookup"><span data-stu-id="66a32-210">The `customErrors` section specifies the mode, which is set to "On".</span></span> <span data-ttu-id="66a32-211">また、エラーが`defaultRedirect`発生したときに移動するページをアプリケーションに通知するを指定します。</span><span class="sxs-lookup"><span data-stu-id="66a32-211">It also specifies the `defaultRedirect`, which tells the application which page to navigate to when an error occurs.</span></span> <span data-ttu-id="66a32-212">また、ページが見つからない場合に404エラーを処理する方法を指定する特定の error 要素を追加しました。</span><span class="sxs-lookup"><span data-stu-id="66a32-212">In addition, you have added a specific error element that specifies how to handle a 404 error when a page is not found.</span></span> <span data-ttu-id="66a32-213">このチュートリアルの後の方で、アプリケーションレベルでエラーの詳細をキャプチャする追加のエラー処理を追加します。</span><span class="sxs-lookup"><span data-stu-id="66a32-213">Later in this tutorial, you will add additional error handling that will capture the details of an error at the application level.</span></span>

#### <a name="running-the-application"></a><span data-ttu-id="66a32-214">アプリケーションの実行</span><span class="sxs-lookup"><span data-stu-id="66a32-214">Running the Application</span></span>

<span data-ttu-id="66a32-215">アプリケーションを今すぐ実行して、更新されたルートを確認することができます。</span><span class="sxs-lookup"><span data-stu-id="66a32-215">You can run the application now to see the updated routes.</span></span>

1. <span data-ttu-id="66a32-216">**F5**キーを押して Wingtip Toys サンプルアプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="66a32-216">Press **F5** to run the Wingtip Toys sample application.</span></span>  
 <span data-ttu-id="66a32-217">ブラウザーが開き、 *default.aspx*ページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="66a32-217">The browser opens and shows the *Default.aspx* page.</span></span>
2. <span data-ttu-id="66a32-218">ブラウザーに次の URL を入力してください (を使用してください、 **ポ** ート番号)。</span><span class="sxs-lookup"><span data-stu-id="66a32-218">Enter the following URL into the browser (be sure to use **your** port number):</span></span>  
    `https://localhost:44300/NoPage.aspx`
3. <span data-ttu-id="66a32-219">ブラウザーに表示されている*Errorpage .aspx*を確認します。</span><span class="sxs-lookup"><span data-stu-id="66a32-219">Review the *ErrorPage.aspx* displayed in the browser.</span></span> 

    ![ASP.NET エラー処理-ページが見つかりませんでした](aspnet-error-handling/_static/image1.png)

<span data-ttu-id="66a32-221">存在しない*Nopage .aspx*ページを要求すると、エラーページには単純なエラーメッセージと詳細なエラー情報が表示されます (追加の詳細情報がある場合)。</span><span class="sxs-lookup"><span data-stu-id="66a32-221">When you request the *NoPage.aspx* page, which does not exist, the error page will show the simple error message and the detailed error information if additional details are available.</span></span> <span data-ttu-id="66a32-222">ただし、ユーザーが存在しないページをリモートの場所から要求した場合、エラーページに表示されるのはエラーメッセージだけです。</span><span class="sxs-lookup"><span data-stu-id="66a32-222">However, if the user requested a non-existent page from a remote location, the error page would only show the error message in red.</span></span>

### <a name="including-an-exception-for-testing-purposes"></a><span data-ttu-id="66a32-223">テスト目的で例外を含める</span><span class="sxs-lookup"><span data-stu-id="66a32-223">Including an Exception for Testing Purposes</span></span>

<span data-ttu-id="66a32-224">エラーが発生したときにアプリケーションがどのように機能するかを確認するには、ASP.NET でエラー条件を意図的に作成します。</span><span class="sxs-lookup"><span data-stu-id="66a32-224">To verify how your application will function when an error occurs, you can deliberately create error conditions in ASP.NET.</span></span> <span data-ttu-id="66a32-225">Wingtip Toys サンプルアプリケーションでは、既定のページが読み込まれて何が発生するかを確認すると、テスト例外がスローされます。</span><span class="sxs-lookup"><span data-stu-id="66a32-225">In the Wingtip Toys sample application, you will throw a test exception when the default page loads to see what happens.</span></span>

1. <span data-ttu-id="66a32-226">Visual Studio で*default.aspx*ページの分離コードを開きます。</span><span class="sxs-lookup"><span data-stu-id="66a32-226">Open the code-behind of the *Default.aspx* page in Visual Studio.</span></span>   
   <span data-ttu-id="66a32-227">*Default.aspx.cs*の分離コードページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="66a32-227">The *Default.aspx.cs* code-behind page will be displayed.</span></span>
2. <span data-ttu-id="66a32-228">`Page_Load`ハンドラーで、次のようにハンドラーが表示されるようにコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="66a32-228">In the `Page_Load` handler, add code so that the handler appears as follows:</span></span>   

    [!code-csharp[Main](aspnet-error-handling/samples/sample9.cs?highlight=3-4)]

<span data-ttu-id="66a32-229">さまざまな種類の例外を作成することができます。</span><span class="sxs-lookup"><span data-stu-id="66a32-229">It is possible to create various different types of exceptions.</span></span> <span data-ttu-id="66a32-230">上のコードでは、 *default.aspx*ページが`InvalidOperationException`読み込まれるときに、を作成しています。</span><span class="sxs-lookup"><span data-stu-id="66a32-230">In the above code, you are creating an `InvalidOperationException` when the *Default.aspx* page is loaded.</span></span>

#### <a name="running-the-application"></a><span data-ttu-id="66a32-231">アプリケーションの実行</span><span class="sxs-lookup"><span data-stu-id="66a32-231">Running the Application</span></span>

<span data-ttu-id="66a32-232">アプリケーションを実行して、アプリケーションが例外を処理する方法を確認できます。</span><span class="sxs-lookup"><span data-stu-id="66a32-232">You can run the application to see how the application handles the exception.</span></span>

1. <span data-ttu-id="66a32-233">CTRL キーを押し**ながら F5**キーを押して Wingtip Toys サンプルアプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="66a32-233">Press **CTRL+F5** to run the Wingtip Toys sample application.</span></span>  
 <span data-ttu-id="66a32-234">アプリケーションは、InvalidOperationException をスローします。</span><span class="sxs-lookup"><span data-stu-id="66a32-234">The application throws the InvalidOperationException.</span></span> 

    > [!NOTE] 
    > 
    > <span data-ttu-id="66a32-235">Visual Studio でエラーの原因を表示するには、コードを中断せずに、CTRL キーを押し**ながら F5**キーを押してページを表示する必要があります。</span><span class="sxs-lookup"><span data-stu-id="66a32-235">You must press **CTRL+F5** to display the page without breaking into the code to view the source of the error in Visual Studio.</span></span>
2. <span data-ttu-id="66a32-236">ブラウザーに表示されている*Errorpage .aspx*を確認します。</span><span class="sxs-lookup"><span data-stu-id="66a32-236">Review the *ErrorPage.aspx* displayed in the browser.</span></span> 

    ![ASP.NET エラー処理-エラーページ](aspnet-error-handling/_static/image2.png)

<span data-ttu-id="66a32-238">エラーの詳細を見るとわかるように、web.config ファイルの`customError`セクションによって例外がトラップされています。</span><span class="sxs-lookup"><span data-stu-id="66a32-238">As you can see in the error details, the exception was trapped by the `customError` section in the *Web.config* file.</span></span>

### <a name="adding-application-level-error-handling"></a><span data-ttu-id="66a32-239">アプリケーションレベルのエラー処理の追加</span><span class="sxs-lookup"><span data-stu-id="66a32-239">Adding Application-Level Error Handling</span></span>

<span data-ttu-id="66a32-240">Web.config ファイルの`customErrors`セクションを使用して例外をトラップするのではなく、例外に関する情報がほとんど得られない場合は、アプリケーションレベルでエラーをトラップし、エラーの詳細を取得することができます。</span><span class="sxs-lookup"><span data-stu-id="66a32-240">Rather than trap the exception using the `customErrors` section in the *Web.config* file, where you gain little information about the exception, you can trap the error at the application level and retrieve error details.</span></span>

1. <span data-ttu-id="66a32-241">**ソリューションエクスプローラー**で、 *Global.asax.cs*ファイルを見つけて開きます。</span><span class="sxs-lookup"><span data-stu-id="66a32-241">In **Solution Explorer**, find and open the *Global.asax.cs* file.</span></span>
2. <span data-ttu-id="66a32-242">**アプリケーション\_エラー**ハンドラーを追加して、次のように表示されるようにします。</span><span class="sxs-lookup"><span data-stu-id="66a32-242">Add an **Application\_Error** handler so that it appears as follows:</span></span>   

    [!code-csharp[Main](aspnet-error-handling/samples/sample10.cs)]

<span data-ttu-id="66a32-243">アプリケーションでエラーが発生すると、 `Application_Error`ハンドラーが呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="66a32-243">When an error occurs in the application, the `Application_Error` handler is called.</span></span> <span data-ttu-id="66a32-244">このハンドラーでは、最後の例外が取得され、確認されます。</span><span class="sxs-lookup"><span data-stu-id="66a32-244">In this handler, the last exception is retrieved and reviewed.</span></span> <span data-ttu-id="66a32-245">例外がハンドルされず、例外に内部例外の詳細が含まれて`InnerException`いる (つまり、が null ではない) 場合、アプリケーションは、例外の詳細が表示されるエラーページに実行を転送します。</span><span class="sxs-lookup"><span data-stu-id="66a32-245">If the exception was unhandled and the exception contains inner-exception details (that is, `InnerException` is not null), the application transfers execution to the error page where the exception details are displayed.</span></span>

#### <a name="running-the-application"></a><span data-ttu-id="66a32-246">アプリケーションの実行</span><span class="sxs-lookup"><span data-stu-id="66a32-246">Running the Application</span></span>

<span data-ttu-id="66a32-247">アプリケーションを実行して、アプリケーションレベルで例外を処理することによって提供される追加のエラーの詳細を確認できます。</span><span class="sxs-lookup"><span data-stu-id="66a32-247">You can run the application to see the additional error details provided by handling the exception at the application level.</span></span>

1. <span data-ttu-id="66a32-248">CTRL キーを押し**ながら F5**キーを押して Wingtip Toys サンプルアプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="66a32-248">Press **CTRL+F5** to run the Wingtip Toys sample application.</span></span>  
 <span data-ttu-id="66a32-249">アプリケーションがを`InvalidOperationException`スローします。</span><span class="sxs-lookup"><span data-stu-id="66a32-249">The application throws the `InvalidOperationException` .</span></span>
2. <span data-ttu-id="66a32-250">ブラウザーに表示されている*Errorpage .aspx*を確認します。</span><span class="sxs-lookup"><span data-stu-id="66a32-250">Review the *ErrorPage.aspx* displayed in the browser.</span></span> 

    ![ASP.NET エラー処理-アプリケーションレベルのエラー](aspnet-error-handling/_static/image3.png)

### <a name="adding-page-level-error-handling"></a><span data-ttu-id="66a32-252">ページレベルのエラー処理の追加</span><span class="sxs-lookup"><span data-stu-id="66a32-252">Adding Page-Level Error Handling</span></span>

<span data-ttu-id="66a32-253">ページの`ErrorPage` `@Page`ディレクティブに属性を追加するか、ページの分離コードにイベントハンドラーを追加することで、ページレベルのエラー処理をページに追加できます。`Page_Error`</span><span class="sxs-lookup"><span data-stu-id="66a32-253">You can add page-level error handling to a page either by using adding an `ErrorPage` attribute to the `@Page` directive of the page, or by adding a `Page_Error` event handler to the code-behind of a page.</span></span> <span data-ttu-id="66a32-254">このセクションでは、実行を`Page_Error` *errorpage .aspx*ページに転送するイベントハンドラーを追加します。</span><span class="sxs-lookup"><span data-stu-id="66a32-254">In this section, you will add a `Page_Error` event handler that will transfer execution to the *ErrorPage.aspx* page.</span></span>

1. <span data-ttu-id="66a32-255">**ソリューションエクスプローラー**で、 *Default.aspx.cs*ファイルを見つけて開きます。</span><span class="sxs-lookup"><span data-stu-id="66a32-255">In **Solution Explorer**, find and open the *Default.aspx.cs* file.</span></span>
2. <span data-ttu-id="66a32-256">ハンドラーを`Page_Error`追加して、分離コードが次のように表示されるようにします。</span><span class="sxs-lookup"><span data-stu-id="66a32-256">Add a `Page_Error` handler so that the code-behind appears as follows:</span></span>   

    [!code-csharp[Main](aspnet-error-handling/samples/sample11.cs?highlight=18-30)]

<span data-ttu-id="66a32-257">ページでエラーが発生すると、 `Page_Error`イベントハンドラーが呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="66a32-257">When an error occurs on the page, the `Page_Error` event handler is called.</span></span> <span data-ttu-id="66a32-258">このハンドラーでは、最後の例外が取得され、確認されます。</span><span class="sxs-lookup"><span data-stu-id="66a32-258">In this handler, the last exception is retrieved and reviewed.</span></span> <span data-ttu-id="66a32-259">が発生した場合`Page_Error` 、イベントハンドラーは、例外の詳細が表示されているエラーページに実行を転送します。 `InvalidOperationException`</span><span class="sxs-lookup"><span data-stu-id="66a32-259">If an `InvalidOperationException` occurs, the `Page_Error` event handler transfers execution to the error page where the exception details are displayed.</span></span>

#### <a name="running-the-application"></a><span data-ttu-id="66a32-260">アプリケーションの実行</span><span class="sxs-lookup"><span data-stu-id="66a32-260">Running the Application</span></span>

<span data-ttu-id="66a32-261">アプリケーションを今すぐ実行して、更新されたルートを確認することができます。</span><span class="sxs-lookup"><span data-stu-id="66a32-261">You can run the application now to see the updated routes.</span></span>

1. <span data-ttu-id="66a32-262">CTRL キーを押し**ながら F5**キーを押して Wingtip Toys サンプルアプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="66a32-262">Press **CTRL+F5** to run the Wingtip Toys sample application.</span></span>  
 <span data-ttu-id="66a32-263">アプリケーションがを`InvalidOperationException`スローします。</span><span class="sxs-lookup"><span data-stu-id="66a32-263">The application throws the `InvalidOperationException` .</span></span>
2. <span data-ttu-id="66a32-264">ブラウザーに表示されている*Errorpage .aspx*を確認します。</span><span class="sxs-lookup"><span data-stu-id="66a32-264">Review the *ErrorPage.aspx* displayed in the browser.</span></span> 

    ![ASP.NET エラー処理-ページレベルのエラー](aspnet-error-handling/_static/image4.png)
3. <span data-ttu-id="66a32-266">ブラウザーウィンドウを閉じます。</span><span class="sxs-lookup"><span data-stu-id="66a32-266">Close your browser window.</span></span>

### <a name="removing-the-exception-used-for-testing"></a><span data-ttu-id="66a32-267">テストに使用された例外を削除しています</span><span class="sxs-lookup"><span data-stu-id="66a32-267">Removing the Exception Used for Testing</span></span>

<span data-ttu-id="66a32-268">このチュートリアルの前半で追加した例外をスローせずに Wingtip Toys サンプルアプリケーションを機能させるには、例外を削除します。</span><span class="sxs-lookup"><span data-stu-id="66a32-268">To allow the Wingtip Toys sample application to function without throwing the exception you added earlier in this tutorial, remove the exception.</span></span>

1. <span data-ttu-id="66a32-269">*Default.aspx*ページの分離コードを開きます。</span><span class="sxs-lookup"><span data-stu-id="66a32-269">Open the code-behind of the *Default.aspx* page.</span></span>
2. <span data-ttu-id="66a32-270">`Page_Load`ハンドラーで、例外をスローするコードを削除して、ハンドラーが次のように表示されるようにします。</span><span class="sxs-lookup"><span data-stu-id="66a32-270">In the `Page_Load` handler, remove the code that throws the exception so that the handler appears as follows:</span></span>   

    [!code-csharp[Main](aspnet-error-handling/samples/sample12.cs)]

### <a name="adding-code-level-error-logging"></a><span data-ttu-id="66a32-271">コードレベルのエラーログの追加</span><span class="sxs-lookup"><span data-stu-id="66a32-271">Adding Code-Level Error Logging</span></span>

<span data-ttu-id="66a32-272">このチュートリアルで既に説明したように、try/catch ステートメントを追加して、コードのセクションを実行し、発生した最初のエラーを処理することができます。</span><span class="sxs-lookup"><span data-stu-id="66a32-272">As mentioned earlier in this tutorial, you can add try/catch statements to attempt to run a section of code and handle the first error that occurs.</span></span> <span data-ttu-id="66a32-273">この例では、エラーの詳細をエラーログファイルに書き込むだけで、エラーを後で確認できます。</span><span class="sxs-lookup"><span data-stu-id="66a32-273">In this example, you will only write the error details to the error log file so that the error can be reviewed later.</span></span>

1. <span data-ttu-id="66a32-274">**ソリューションエクスプローラー**の*Logic*フォルダーで、 *PayPalFunctions.cs*ファイルを見つけて開きます。</span><span class="sxs-lookup"><span data-stu-id="66a32-274">In **Solution Explorer**, in the *Logic* folder, find and open the *PayPalFunctions.cs* file.</span></span>
2. <span data-ttu-id="66a32-275">コードが`HttpCall`次のように表示されるように、メソッドを更新します。</span><span class="sxs-lookup"><span data-stu-id="66a32-275">Update the `HttpCall` method so that the code appears as follows:</span></span>   

    [!code-csharp[Main](aspnet-error-handling/samples/sample13.cs?highlight=20,22-23)]

<span data-ttu-id="66a32-276">上のコードは、 `LogException` `ExceptionUtility`クラスに含まれているメソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="66a32-276">The above code calls the `LogException` method that is contained in the `ExceptionUtility` class.</span></span> <span data-ttu-id="66a32-277">このチュートリアルの前半で、*ロジック*フォルダーに*ExceptionUtility.cs*クラスファイルを追加しました。</span><span class="sxs-lookup"><span data-stu-id="66a32-277">You added the *ExceptionUtility.cs* class file to the *Logic* folder earlier in this tutorial.</span></span> <span data-ttu-id="66a32-278">`LogException` は、次の 2 つのパラメーターを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="66a32-278">The `LogException` method takes two parameters.</span></span> <span data-ttu-id="66a32-279">最初のパラメーターは、exception オブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="66a32-279">The first parameter is the exception object.</span></span> <span data-ttu-id="66a32-280">2番目のパラメーターは、エラーの原因を認識するために使用される文字列です。</span><span class="sxs-lookup"><span data-stu-id="66a32-280">The second parameter is a string used to recognize the source of the error.</span></span>

### <a name="inspecting-the-error-logging-information"></a><span data-ttu-id="66a32-281">エラーのログ情報を検査しています</span><span class="sxs-lookup"><span data-stu-id="66a32-281">Inspecting the Error Logging Information</span></span>

<span data-ttu-id="66a32-282">前に説明したように、エラーログを使用して、アプリケーションでどのエラーを先に修正する必要があるかを判断できます。</span><span class="sxs-lookup"><span data-stu-id="66a32-282">As mentioned previously, you can use the error log to determine which errors in your application should be fixed first.</span></span> <span data-ttu-id="66a32-283">もちろん、トラップされ、エラーログに書き込まれたエラーのみが記録されます。</span><span class="sxs-lookup"><span data-stu-id="66a32-283">Of course, only errors that have been trapped and written to the error log will be recorded.</span></span>

1. <span data-ttu-id="66a32-284">**ソリューションエクスプローラー**で、*アプリケーション\_データ*フォルダー内の*エラーログ*ファイルを見つけて開きます。</span><span class="sxs-lookup"><span data-stu-id="66a32-284">In **Solution Explorer**, find and open the *ErrorLog.txt* file in the *App\_Data* folder.</span></span>   
 <span data-ttu-id="66a32-285">場合によっては、 **[すべてのファイルを表示]** オプションを選択するか、**ソリューションエクスプローラー**の上部にある **[更新]** オプションを選択して、*エラーログ*ファイルを確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="66a32-285">You may need to select the "**Show All Files**" option or the "**Refresh**" option from the top of **Solution Explorer** to see the *ErrorLog.txt* file.</span></span>
2. <span data-ttu-id="66a32-286">Visual Studio に表示されるエラーログを確認します。</span><span class="sxs-lookup"><span data-stu-id="66a32-286">Review the error log displayed in Visual Studio:</span></span> 

    ![ASP.NET エラー処理-エラーログ](aspnet-error-handling/_static/image5.png)

### <a name="safe-error-messages"></a><span data-ttu-id="66a32-288">安全なエラーメッセージ</span><span class="sxs-lookup"><span data-stu-id="66a32-288">Safe Error Messages</span></span>

<span data-ttu-id="66a32-289">アプリケーションでエラーメッセージが表示される場合は、悪意のあるユーザーがアプリケーションを攻撃する際に役立つ情報を提供しないようにする必要があること**に注意し**てください。</span><span class="sxs-lookup"><span data-stu-id="66a32-289">It is **important to note** that when your application displays error messages, it should not give away information that a malicious user might find helpful in attacking your application.</span></span> <span data-ttu-id="66a32-290">たとえば、アプリケーションがデータベースへの書き込みに失敗した場合、使用しているユーザー名を含むエラーメッセージが表示されないようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="66a32-290">For example, if your application unsuccessfully tries to write in to a database, it should not display an error message that includes the user name it is using.</span></span> <span data-ttu-id="66a32-291">このため、赤の一般的なエラーメッセージがユーザーに表示されます。</span><span class="sxs-lookup"><span data-stu-id="66a32-291">For this reason, a generic error message in red is displayed to the user.</span></span> <span data-ttu-id="66a32-292">その他のエラーの詳細はすべて、ローカルコンピューターの開発者にのみ表示されます。</span><span class="sxs-lookup"><span data-stu-id="66a32-292">All additional error details are only displayed to the developer on the local machine.</span></span>

## <a name="using-elmah"></a><span data-ttu-id="66a32-293">ELMAH の使用</span><span class="sxs-lookup"><span data-stu-id="66a32-293">Using ELMAH</span></span>

<span data-ttu-id="66a32-294">ELMAH (エラーログモジュールとハンドラー) は、NuGet パッケージとして ASP.NET アプリケーションにプラグインするエラーログ機能です。</span><span class="sxs-lookup"><span data-stu-id="66a32-294">ELMAH (Error Logging Modules and Handlers) is an error logging facility that you plug into your ASP.NET application as a NuGet package.</span></span> <span data-ttu-id="66a32-295">ELMAH には、次の機能が用意されています。</span><span class="sxs-lookup"><span data-stu-id="66a32-295">ELMAH provides the following capabilities:</span></span>

- <span data-ttu-id="66a32-296">未処理の例外のログ記録。</span><span class="sxs-lookup"><span data-stu-id="66a32-296">Logging of unhandled exceptions.</span></span>
- <span data-ttu-id="66a32-297">記録の未処理の例外のログ全体を表示する web ページ。</span><span class="sxs-lookup"><span data-stu-id="66a32-297">A web page to view the entire log of recoded unhandled exceptions.</span></span>
- <span data-ttu-id="66a32-298">ログに記録された各例外の詳細を表示する web ページ。</span><span class="sxs-lookup"><span data-stu-id="66a32-298">A web page to view the full details of each logged exception.</span></span>
- <span data-ttu-id="66a32-299">発生時の各エラーに関する電子メール通知。</span><span class="sxs-lookup"><span data-stu-id="66a32-299">An email notification of each error at the time it occurs.</span></span>
- <span data-ttu-id="66a32-300">ログからの過去15件のエラーの RSS フィード。</span><span class="sxs-lookup"><span data-stu-id="66a32-300">An RSS feed of the last 15 errors from the log.</span></span>

<span data-ttu-id="66a32-301">ELMAH を使用するには、事前にインストールしておく必要があります。</span><span class="sxs-lookup"><span data-stu-id="66a32-301">Before you can work with the ELMAH, you must install it.</span></span> <span data-ttu-id="66a32-302">これは、 *NuGet*パッケージインストーラーを使用して簡単に行うことができます。</span><span class="sxs-lookup"><span data-stu-id="66a32-302">This is easy using the *NuGet* package installer.</span></span> <span data-ttu-id="66a32-303">このチュートリアルシリーズで既に説明したように、NuGet は visual Studio の拡張機能であり、Visual Studio でのオープンソースライブラリとツールのインストールと更新を簡単に行うことができます。</span><span class="sxs-lookup"><span data-stu-id="66a32-303">As mentioned earlier in this tutorial series, NuGet is a Visual Studio extension that makes it easy to install and update open source libraries and tools in Visual Studio.</span></span>

1. <span data-ttu-id="66a32-304">Visual Studio で、 **[ツール]** メニューの [ **nuget パッケージマネージャー** > ] **[ソリューションの nuget パッケージの管理]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="66a32-304">Within Visual Studio, from the **Tools** menu, select **NuGet Package Manager** > **Manage NuGet Packages for Solution**.</span></span> 

    ![ASP.NET エラー処理-ソリューションの NuGet パッケージの管理](aspnet-error-handling/_static/image6.png)
2. <span data-ttu-id="66a32-306">**[NuGet パッケージの管理]** ダイアログボックスは、Visual Studio 内に表示されます。</span><span class="sxs-lookup"><span data-stu-id="66a32-306">The **Manage NuGet Packages** dialog box is displayed within Visual Studio.</span></span>
3. <span data-ttu-id="66a32-307">**[NuGet パッケージの管理]** ダイアログボックスで、左側の **[オンライン]** を展開し、 **[nuget.org]** を選択します。次に、利用可能なパッケージの一覧から、オンラインで**ELMAH**パッケージを検索してインストールします。</span><span class="sxs-lookup"><span data-stu-id="66a32-307">In the **Manage NuGet Packages** dialog box, expand **Online** on the left, and then select **nuget.org**. Then, find and install the **ELMAH** package from the list of available packages online.</span></span> 

    ![ASP.NET エラー処理-ELMA NuGet パッケージ](aspnet-error-handling/_static/image7.png)
4. <span data-ttu-id="66a32-309">パッケージをダウンロードするには、インターネットに接続している必要があります。</span><span class="sxs-lookup"><span data-stu-id="66a32-309">You will need to have an internet connection to download the package.</span></span>
5. <span data-ttu-id="66a32-310">**[プロジェクトの選択**] ダイアログボックスで、 **[ウィングヒント]** が選択されていることを確認し、 **[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="66a32-310">In the **Select Projects** dialog box, make sure the **WingtipToys** selection is selected, and then click **OK**.</span></span> 

    ![ASP.NET エラー処理-[プロジェクトの選択] ダイアログ](aspnet-error-handling/_static/image8.png)
6. <span data-ttu-id="66a32-312">必要に応じて、 **[NuGet パッケージの管理]** ダイアログボックスで **[閉じる]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="66a32-312">Click **Close** in the **Manage NuGet Packages** dialog box if needed.</span></span>
7. <span data-ttu-id="66a32-313">開いているファイルを再度読み込むように Visual Studio から要求された場合は、 **[すべてはい]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="66a32-313">If Visual Studio requests that you reload any open files, select "**Yes to All**".</span></span>
8. <span data-ttu-id="66a32-314">ELMAH パッケージは、プロジェクトのルートにある web.config ファイルに自身のエントリを追加します。</span><span class="sxs-lookup"><span data-stu-id="66a32-314">The ELMAH package adds entries for itself in the *Web.config* file at the root of your project.</span></span> <span data-ttu-id="66a32-315">変更した web.config ファイルを再読み込みするかどうかを確認するメッセージが Visual Studio で表示されたら、 **[はい]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="66a32-315">If Visual Studio asks you if you want to reload the modified *Web.config* file, click **Yes**.</span></span>

<span data-ttu-id="66a32-316">ELMAH は、発生した未処理のエラーを格納する準備ができました。</span><span class="sxs-lookup"><span data-stu-id="66a32-316">ELMAH is now ready to store any unhandled errors that occur.</span></span>

### <a name="viewing-the-elmah-log"></a><span data-ttu-id="66a32-317">ELMAH ログの表示</span><span class="sxs-lookup"><span data-stu-id="66a32-317">Viewing the ELMAH Log</span></span>

<span data-ttu-id="66a32-318">ELMAH ログを表示するのは簡単ですが、最初に、ELMAH ログに記録されるハンドルされない例外を作成します。</span><span class="sxs-lookup"><span data-stu-id="66a32-318">Viewing the ELMAH log is easy, but first you will create an unhandled exception that will be recorded in the ELMAH log.</span></span>

1. <span data-ttu-id="66a32-319">CTRL キーを押し**ながら F5**キーを押して Wingtip Toys サンプルアプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="66a32-319">Press **CTRL+F5** to run the Wingtip Toys sample application.</span></span>
2. <span data-ttu-id="66a32-320">未処理の例外を ELMAH ログに書き込むには、ブラウザーで次の URL (ポート番号を使用) に移動します。</span><span class="sxs-lookup"><span data-stu-id="66a32-320">To write an unhandled exception to the ELMAH log, navigate in your browser to the following URL (using your port number):</span></span>  
    <span data-ttu-id="66a32-321">`https://localhost:44300/NoPage.aspx`エラーページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="66a32-321">`https://localhost:44300/NoPage.aspx` The error page will be displayed.</span></span>
3. <span data-ttu-id="66a32-322">ELMAH ログを表示するには、ブラウザーで次の URL (ポート番号を使用) に移動します。</span><span class="sxs-lookup"><span data-stu-id="66a32-322">To display the ELMAH log, navigate in your browser to the following URL (using your port number):</span></span>  
    `https://localhost:44300/elmah.axd`

    ![ASP.NET エラー処理-ELMAH エラーログ](aspnet-error-handling/_static/image9.png)

## <a name="summary"></a><span data-ttu-id="66a32-324">まとめ</span><span class="sxs-lookup"><span data-stu-id="66a32-324">Summary</span></span>

<span data-ttu-id="66a32-325">このチュートリアルでは、アプリケーションレベル、ページレベル、およびコードレベルでエラーを処理する方法について学習しました。</span><span class="sxs-lookup"><span data-stu-id="66a32-325">In this tutorial, you have learned about handling errors at the application level, the page level, and the code level.</span></span> <span data-ttu-id="66a32-326">また、処理されたエラーと未処理のエラーをログに記録して後で確認する方法についても学習しました。</span><span class="sxs-lookup"><span data-stu-id="66a32-326">You have also learned how to log handled and unhandled errors for later review.</span></span> <span data-ttu-id="66a32-327">ここでは、NuGet を使用してアプリケーションに例外ログと通知を提供するために、ELMAH ユーティリティを追加しました。</span><span class="sxs-lookup"><span data-stu-id="66a32-327">You added the ELMAH utility to provide exception logging and notification to your application using NuGet.</span></span> <span data-ttu-id="66a32-328">また、安全なエラーメッセージの重要性についても説明しました。</span><span class="sxs-lookup"><span data-stu-id="66a32-328">Additionally, you have learned about the importance of safe error messages.</span></span>

## <a name="tutorial-series-conclusion"></a><span data-ttu-id="66a32-329">チュートリアルシリーズの結論</span><span class="sxs-lookup"><span data-stu-id="66a32-329">Tutorial Series Conclusion</span></span>

<span data-ttu-id="66a32-330">次のようにしていただき、ありがとうございます。</span><span class="sxs-lookup"><span data-stu-id="66a32-330">Thanks for following along.</span></span> <span data-ttu-id="66a32-331">この一連のチュートリアルを使用すると、ASP.NET Web フォームを理解しやすくなります。</span><span class="sxs-lookup"><span data-stu-id="66a32-331">I hope this set of tutorials helped you become more familiar with ASP.NET Web Forms.</span></span> <span data-ttu-id="66a32-332">ASP.NET 4.5 および Visual Studio 2013 で使用できる Web フォーム機能の詳細については、「 [ASP.NET and Web Tools Visual Studio 2013 リリースノート](../../../../visual-studio/overview/2013/release-notes.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="66a32-332">If you need more information about Web Forms features available in ASP.NET 4.5 and Visual Studio 2013, see [ASP.NET and Web Tools for Visual Studio 2013 Release Notes](../../../../visual-studio/overview/2013/release-notes.md).</span></span> <span data-ttu-id="66a32-333">また、「**次のステップ**」のセクションに記載されているチュートリアルを参照して、[無料の Azure 試用版](https://azure.microsoft.com/pricing/free-trial/)を defintely してください。</span><span class="sxs-lookup"><span data-stu-id="66a32-333">Also, be sure to take a look at the tutorial mentioned in the **Next Steps** section and defintely try out the [free Azure trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

![ありがとうございました-Erik](aspnet-error-handling/_static/image10.png)  

## <a name="next-steps"></a><span data-ttu-id="66a32-335">次の手順</span><span class="sxs-lookup"><span data-stu-id="66a32-335">Next Steps</span></span>

<span data-ttu-id="66a32-336">Microsoft Azure するための web アプリケーションのデプロイの詳細については、「 [Azure の Web サイトへのメンバーシップ、OAuth、SQL Database を使用した安全な ASP.NET Web フォームアプリのデプロイ](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="66a32-336">Learn more about deploying your web application to Microsoft Azure, see [Deploy a Secure ASP.NET Web Forms App with Membership, OAuth, and SQL Database to an Azure Web Site](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/).</span></span>

## <a name="free-trial"></a><span data-ttu-id="66a32-337">無料試用版</span><span class="sxs-lookup"><span data-stu-id="66a32-337">Free Trial</span></span>

[<span data-ttu-id="66a32-338">Microsoft Azure-無料試用版</span><span class="sxs-lookup"><span data-stu-id="66a32-338">Microsoft Azure - Free Trial</span></span>](https://azure.microsoft.com/pricing/free-trial/)  
 <span data-ttu-id="66a32-339">Web サイトを Microsoft Azure に公開すると、時間、メンテナンス、コストが節約されます。</span><span class="sxs-lookup"><span data-stu-id="66a32-339">Publishing your website to Microsoft Azure will save you time, maintenance and expense.</span></span> <span data-ttu-id="66a32-340">これは、web アプリを Azure にデプロイするための簡単なプロセスです。</span><span class="sxs-lookup"><span data-stu-id="66a32-340">It's a quick process to deploying your web app to Azure.</span></span> <span data-ttu-id="66a32-341">Web アプリを保守および監視する必要がある場合、Azure にはさまざまなツールとサービスが用意されています。</span><span class="sxs-lookup"><span data-stu-id="66a32-341">When you need to maintain and monitor your web app, Azure offers a variety of tools and services.</span></span> <span data-ttu-id="66a32-342">Azure のデータ、トラフィック、id、バックアップ、メッセージング、メディア、パフォーマンスを管理します。</span><span class="sxs-lookup"><span data-stu-id="66a32-342">Manage data, traffic, identity, backups, messaging, media and performance in Azure.</span></span> <span data-ttu-id="66a32-343">また、これらはすべて、非常にコスト効率のよい方法で提供されます。</span><span class="sxs-lookup"><span data-stu-id="66a32-343">And, all of this is provided in a very cost effective approach.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="66a32-344">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="66a32-344">Additional Resources</span></span>

<span data-ttu-id="66a32-345">[ASP.NET の正常性監視によるエラーの詳細のログ記録](../../older-versions-getting-started/deploying-web-site-projects/logging-error-details-with-asp-net-health-monitoring-cs.md) </span><span class="sxs-lookup"><span data-stu-id="66a32-345">[Logging Error Details with ASP.NET Health Monitoring](../../older-versions-getting-started/deploying-web-site-projects/logging-error-details-with-asp-net-health-monitoring-cs.md) </span></span>  
[<span data-ttu-id="66a32-346">ELMAH</span><span class="sxs-lookup"><span data-stu-id="66a32-346">ELMAH</span></span>](https://code.google.com/p/elmah/)

## <a name="acknowledgements"></a><span data-ttu-id="66a32-347">謝辞</span><span class="sxs-lookup"><span data-stu-id="66a32-347">Acknowledgements</span></span>

<span data-ttu-id="66a32-348">このチュートリアルシリーズの内容に多大な貢献をした次の人々に感謝したいと思います。</span><span class="sxs-lookup"><span data-stu-id="66a32-348">I would like to thank the following people who made significant contributions to the content of this tutorial series:</span></span>

- [<span data-ttu-id="66a32-349">Alberto poblacion, MVP &amp; MCT, スペイン</span><span class="sxs-lookup"><span data-stu-id="66a32-349">Alberto Poblacion, MVP &amp; MCT, Spain</span></span>](https://mvp.microsoft.com/mvp/Alberto%20Poblacion%20Bolano-36772)
- <span data-ttu-id="66a32-350">[Alex、オランダ](http://blog.alexthissen.nl/)(twitter: [@alexthissen](http://twitter.com/alexthissen))</span><span class="sxs-lookup"><span data-stu-id="66a32-350">[Alex Thissen, Netherlands](http://blog.alexthissen.nl/) (twitter: [@alexthissen](http://twitter.com/alexthissen))</span></span>
- [<span data-ttu-id="66a32-351">Andre Tournier、USA</span><span class="sxs-lookup"><span data-stu-id="66a32-351">Andre Tournier, USA</span></span>](http://andret503.wordpress.com/)
- <span data-ttu-id="66a32-352">Apurva Joshi、Microsoft</span><span class="sxs-lookup"><span data-stu-id="66a32-352">Apurva Joshi, Microsoft</span></span>
- [<span data-ttu-id="66a32-353">Bojan Vrhovnik、スロベニア</span><span class="sxs-lookup"><span data-stu-id="66a32-353">Bojan Vrhovnik, Slovenia</span></span>](http://twitter.com/bvrhovnik)
- <span data-ttu-id="66a32-354">[Bruno Sonnino、ブラジル](http://msmvps.com/blogs/bsonnino)(twitter: [@bsonnino](http://twitter.com/bsonnino))</span><span class="sxs-lookup"><span data-stu-id="66a32-354">[Bruno Sonnino, Brazil](http://msmvps.com/blogs/bsonnino) (twitter: [@bsonnino](http://twitter.com/bsonnino))</span></span>
- [<span data-ttu-id="66a32-355">Carlos dos Santos、ブラジル</span><span class="sxs-lookup"><span data-stu-id="66a32-355">Carlos dos Santos, Brazil</span></span>](http://www.carloscds.net/)
- <span data-ttu-id="66a32-356">[Dave Campbell、USA](http://www.wynapse.com/)(twitter: [@windowsdevnews](http://twitter.com/windowsdevnews))</span><span class="sxs-lookup"><span data-stu-id="66a32-356">[Dave Campbell, USA](http://www.wynapse.com/) (twitter: [@windowsdevnews](http://twitter.com/windowsdevnews))</span></span>
- <span data-ttu-id="66a32-357">[Jon Galloway、Microsoft](https://weblogs.asp.net/jgalloway)(twitter: [@jongalloway](http://twitter.com/jongalloway))</span><span class="sxs-lookup"><span data-stu-id="66a32-357">[Jon Galloway, Microsoft](https://weblogs.asp.net/jgalloway) (twitter: [@jongalloway](http://twitter.com/jongalloway))</span></span>
- <span data-ttu-id="66a32-358">[Michael シャープ、USA](http://www.930solutions.com/)(twitter: [@mrsharps](http://twitter.com/mrsharps))</span><span class="sxs-lookup"><span data-stu-id="66a32-358">[Michael Sharps, USA](http://www.930solutions.com/) (twitter: [@mrsharps](http://twitter.com/mrsharps))</span></span>
- <span data-ttu-id="66a32-359">Mike Pope</span><span class="sxs-lookup"><span data-stu-id="66a32-359">Mike Pope</span></span>
- <span data-ttu-id="66a32-360">[Mitchel 販売者、米国](http://www.mitchelsellers.com/)(twitter: [@MitchelSellers](http://twitter.com/MitchelSellers))</span><span class="sxs-lookup"><span data-stu-id="66a32-360">[Mitchel Sellers, USA](http://www.mitchelsellers.com/) (twitter: [@MitchelSellers](http://twitter.com/MitchelSellers))</span></span>
- [<span data-ttu-id="66a32-361">Paul Cociuba、Microsoft</span><span class="sxs-lookup"><span data-stu-id="66a32-361">Paul Cociuba, Microsoft</span></span>](http://linqto.me/Links/pcociuba)
- [<span data-ttu-id="66a32-362">パウロ Morgado、ポルトガル</span><span class="sxs-lookup"><span data-stu-id="66a32-362">Paulo Morgado, Portugal</span></span>](http://paulomorgado.net/)
- [<span data-ttu-id="66a32-363">Pranav Rastogi、Microsoft</span><span class="sxs-lookup"><span data-stu-id="66a32-363">Pranav Rastogi, Microsoft</span></span>](https://blogs.msdn.com/b/pranav_rastogi)
- [<span data-ttu-id="66a32-364">Tim Ammann、Microsoft</span><span class="sxs-lookup"><span data-stu-id="66a32-364">Tim Ammann, Microsoft</span></span>](https://blogs.iis.net/timamm/default.aspx)
- [<span data-ttu-id="66a32-365">Tom Dykstra、Microsoft</span><span class="sxs-lookup"><span data-stu-id="66a32-365">Tom Dykstra, Microsoft</span></span>](https://blogs.msdn.com/aspnetue)

## <a name="community-contributions"></a><span data-ttu-id="66a32-366">コミュニティへの投稿</span><span class="sxs-lookup"><span data-stu-id="66a32-366">Community Contributions</span></span>

- <span data-ttu-id="66a32-367">Graham Mendick ([@grahammendick](http://twitter.com/grahammendick))</span><span class="sxs-lookup"><span data-stu-id="66a32-367">Graham Mendick ([@grahammendick](http://twitter.com/grahammendick))</span></span>  
  <span data-ttu-id="66a32-368">MSDN の Visual Studio 2012 関連コードサンプル:[ナビゲーション Wingtip Toys](https://code.msdn.microsoft.com/Navigation-Wingtip-Toys-5f0daba2)</span><span class="sxs-lookup"><span data-stu-id="66a32-368">Visual Studio 2012 related code sample on MSDN: [Navigation Wingtip Toys](https://code.msdn.microsoft.com/Navigation-Wingtip-Toys-5f0daba2)</span></span>
- <span data-ttu-id="66a32-369">James Chaney ([jchaney@agvance.net](mailto:jchaney@agvance.net))</span><span class="sxs-lookup"><span data-stu-id="66a32-369">James Chaney ([jchaney@agvance.net](mailto:jchaney@agvance.net))</span></span>  
  <span data-ttu-id="66a32-370">MSDN の Visual Studio 2012 関連コードサンプル:[Visual Basic の ASP.NET 4.5 Web フォームチュートリアルシリーズ](https://code.msdn.microsoft.com/ASPNET-45-Web-Forms-f37f0f63)</span><span class="sxs-lookup"><span data-stu-id="66a32-370">Visual Studio 2012 related code sample on MSDN: [ASP.NET 4.5 Web Forms Tutorial Series in Visual Basic](https://code.msdn.microsoft.com/ASPNET-45-Web-Forms-f37f0f63)</span></span>
- <span data-ttu-id="66a32-371">Andrielle Azevedo-Microsoft テクニカルオーディエンス共同作成者 (twitter @driazevedo:)</span><span class="sxs-lookup"><span data-stu-id="66a32-371">Andrielle Azevedo - Microsoft Technical Audience Contributor (twitter: @driazevedo)</span></span>  
  <span data-ttu-id="66a32-372">Visual Studio 2012 翻訳:[Iniciando com ASP.NET Web フォーム 4.5-Introdução e Visão Geral](https://andrielleazevedo.wordpress.com/2013/01/24/iniciando-com-asp-net-web-forms-4-5-introducao-e-visao-geral/)</span><span class="sxs-lookup"><span data-stu-id="66a32-372">Visual Studio 2012 translation: [Iniciando com ASP.NET Web Forms 4.5 - Parte 1 - Introdução e Visão Geral](https://andrielleazevedo.wordpress.com/2013/01/24/iniciando-com-asp-net-web-forms-4-5-introducao-e-visao-geral/)</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="66a32-373">前へ</span><span class="sxs-lookup"><span data-stu-id="66a32-373">Previous</span></span>](url-routing.md)
