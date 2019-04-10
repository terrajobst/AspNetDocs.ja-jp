---
uid: web-api/overview/advanced/sending-html-form-data-part-2
title: ASP.NET Web API で HTML フォーム データを送信します。ファイルのアップロードとマルチパート MIME - ASP.NET 4.x
author: MikeWasson
description: このチュートリアルでは、web API にファイルをアップロードする方法を示します。 マルチパートの MIME データを処理する方法も説明します。
ms.author: riande
ms.date: 06/21/2012
ms.custom: seoapril2019
ms.assetid: a7f3c1b5-69d9-4261-b082-19ffafa5f16a
msc.legacyurl: /web-api/overview/advanced/sending-html-form-data-part-2
msc.type: authoredcontent
ms.openlocfilehash: 70e150a32f208cf75086f959d484d86e8501c6bd
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/09/2019
ms.locfileid: "59419926"
---
# <a name="sending-html-form-data-in-aspnet-web-api-file-upload-and-multipart-mime"></a><span data-ttu-id="02463-104">ASP.NET Web API で HTML フォーム データを送信します。ファイル アップロードとマルチパート MIME</span><span class="sxs-lookup"><span data-stu-id="02463-104">Sending HTML Form Data in ASP.NET Web API: File Upload and Multipart MIME</span></span>

<span data-ttu-id="02463-105">作成者[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="02463-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

## <a name="part-2-file-upload-and-multipart-mime"></a><span data-ttu-id="02463-106">第 2 部: ファイル アップロードとマルチパート MIME</span><span class="sxs-lookup"><span data-stu-id="02463-106">Part 2: File Upload and Multipart MIME</span></span>

<span data-ttu-id="02463-107">このチュートリアルでは、web API にファイルをアップロードする方法を示します。</span><span class="sxs-lookup"><span data-stu-id="02463-107">This tutorial shows how to upload files to a web API.</span></span> <span data-ttu-id="02463-108">マルチパートの MIME データを処理する方法も説明します。</span><span class="sxs-lookup"><span data-stu-id="02463-108">It also describes how to process multipart MIME data.</span></span>

> [!NOTE]
> <span data-ttu-id="02463-109">[完成したプロジェクトをダウンロード](https://code.msdn.microsoft.com/ASPNET-Web-API-File-Upload-a8c0fb0d)します。</span><span class="sxs-lookup"><span data-stu-id="02463-109">[Download the completed project](https://code.msdn.microsoft.com/ASPNET-Web-API-File-Upload-a8c0fb0d).</span></span>


<span data-ttu-id="02463-110">ファイルをアップロードするための HTML フォームの例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="02463-110">Here is an example of an HTML form for uploading a file:</span></span>

[!code-html[Main](sending-html-form-data-part-2/samples/sample1.html)]

![](sending-html-form-data-part-2/_static/image1.png)

<span data-ttu-id="02463-111">このフォームには、テキスト入力コントロールとファイルの入力コントロールが含まれています。</span><span class="sxs-lookup"><span data-stu-id="02463-111">This form contains a text input control and a file input control.</span></span> <span data-ttu-id="02463-112">フォームには、ファイルの入力コントロールが含まれている場合、 **enctype**属性は常に&quot;マルチパート/フォーム データ&quot;フォームをマルチパート MIME メッセージとして送信されることを指定します。</span><span class="sxs-lookup"><span data-stu-id="02463-112">When a form contains a file input control, the **enctype** attribute should always be &quot;multipart/form-data&quot;, which specifies that the form will be sent as a multipart MIME message.</span></span>

<span data-ttu-id="02463-113">マルチパート MIME メッセージの形式は、要求の例を見て理解する最も簡単なです。</span><span class="sxs-lookup"><span data-stu-id="02463-113">The format of a multipart MIME message is easiest to understand by looking at an example request:</span></span>

[!code-console[Main](sending-html-form-data-part-2/samples/sample2.cmd)]

<span data-ttu-id="02463-114">このメッセージは 2 つに分かれています*パーツ*、それぞれのフォーム コントロールのいずれか。</span><span class="sxs-lookup"><span data-stu-id="02463-114">This message is divided into two *parts*, one for each form control.</span></span> <span data-ttu-id="02463-115">ダッシュで始まる行では、一部の境界が示されます。</span><span class="sxs-lookup"><span data-stu-id="02463-115">Part boundaries are indicated by the lines that start with dashes.</span></span>

> [!NOTE]
> <span data-ttu-id="02463-116">一部の境界には、ランダムなコンポーネントが含まれています (&quot;41184676334&quot;) 境界文字列が表示されないこと誤ってメッセージ部分の内部ことを確認します。</span><span class="sxs-lookup"><span data-stu-id="02463-116">The part boundary includes a random component (&quot;41184676334&quot;) to ensure that the boundary string does not accidentally appear inside a message part.</span></span>


<span data-ttu-id="02463-117">各メッセージ部分には、後に一部の内容が 1 つまたは複数のヘッダーが含まれています。</span><span class="sxs-lookup"><span data-stu-id="02463-117">Each message part contains one or more headers, followed by the part contents.</span></span>

- <span data-ttu-id="02463-118">Content-disposition ヘッダーには、コントロールの名前が含まれています。</span><span class="sxs-lookup"><span data-stu-id="02463-118">The Content-Disposition header includes the name of the control.</span></span> <span data-ttu-id="02463-119">ファイル、そのファイル名も含まれます。</span><span class="sxs-lookup"><span data-stu-id="02463-119">For files, it also contains the file name.</span></span>
- <span data-ttu-id="02463-120">Content-type ヘッダーには、一部のデータについて説明します。</span><span class="sxs-lookup"><span data-stu-id="02463-120">The Content-Type header describes the data in the part.</span></span> <span data-ttu-id="02463-121">このヘッダーを省略すると、既定値はテキスト/プレーンにします。</span><span class="sxs-lookup"><span data-stu-id="02463-121">If this header is omitted, the default is text/plain.</span></span>

<span data-ttu-id="02463-122">前の例では、ユーザーがコンテンツの種類のイメージ/jpeg; GrandCanyon.jpg、という名前のファイルをアップロードテキスト入力の値が、&quot;夏休み&quot;します。</span><span class="sxs-lookup"><span data-stu-id="02463-122">In the previous example, the user uploaded a file named GrandCanyon.jpg, with content type image/jpeg; and the value of the text input was &quot;Summer Vacation&quot;.</span></span>

## <a name="file-upload"></a><span data-ttu-id="02463-123">ファイルのアップロード</span><span class="sxs-lookup"><span data-stu-id="02463-123">File Upload</span></span>

<span data-ttu-id="02463-124">これでマルチパート MIME メッセージからファイルを読み取り、Web API コント ローラーを見てみましょう。</span><span class="sxs-lookup"><span data-stu-id="02463-124">Now let's look at a Web API controller that reads files from a multipart MIME message.</span></span> <span data-ttu-id="02463-125">コント ローラーは、ファイルを非同期的に読み取ります。</span><span class="sxs-lookup"><span data-stu-id="02463-125">The controller will read the files asynchronously.</span></span> <span data-ttu-id="02463-126">Web API を使用して非同期のアクションをサポートしている、[タスク ベースのプログラミング モデル](https://msdn.microsoft.com/library/dd460693.aspx)します。</span><span class="sxs-lookup"><span data-stu-id="02463-126">Web API supports asynchronous actions using the [task-based programming model](https://msdn.microsoft.com/library/dd460693.aspx).</span></span> <span data-ttu-id="02463-127">最初に、サポートする .NET Framework 4.5 を対象としている場合にコードをここでは、 **async**と**await**キーワード。</span><span class="sxs-lookup"><span data-stu-id="02463-127">First, here is the code if you are targeting .NET Framework 4.5, which supports the **async** and **await** keywords.</span></span>

[!code-csharp[Main](sending-html-form-data-part-2/samples/sample3.cs)]

<span data-ttu-id="02463-128">コント ローラー アクションがパラメーターを受け取らないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="02463-128">Notice that the controller action does not take any parameters.</span></span> <span data-ttu-id="02463-129">メディアの種類のフォーマッタを呼び出すことがなく、アクション内で要求本文を処理できないためにです。</span><span class="sxs-lookup"><span data-stu-id="02463-129">That's because we process the request body inside the action, without invoking a media-type formatter.</span></span>

<span data-ttu-id="02463-130">**IsMultipartContent**メソッドは、マルチパート MIME メッセージが要求に含まれるかどうかを確認します。</span><span class="sxs-lookup"><span data-stu-id="02463-130">The **IsMultipartContent** method checks whether the request contains a multipart MIME message.</span></span> <span data-ttu-id="02463-131">それ以外の場合は、コント ローラーは、HTTP 状態コード 415 (Unsupported Media Type) を返します。</span><span class="sxs-lookup"><span data-stu-id="02463-131">If not, the controller returns HTTP status code 415 (Unsupported Media Type).</span></span>

<span data-ttu-id="02463-132">**MultipartFormDataStreamProvider**クラスは、アップロードされたファイルのファイル ストリームを割り当てるヘルパー オブジェクト。</span><span class="sxs-lookup"><span data-stu-id="02463-132">The **MultipartFormDataStreamProvider** class is a helper object that allocates file streams for uploaded files.</span></span> <span data-ttu-id="02463-133">マルチパート MIME メッセージを読み取り、呼び出し、 **ReadAsMultipartAsync**メソッド。</span><span class="sxs-lookup"><span data-stu-id="02463-133">To read the multipart MIME message, call the **ReadAsMultipartAsync** method.</span></span> <span data-ttu-id="02463-134">このメソッドは、すべてのメッセージ部分を抽出し、によって提供されるストリームに書き込みます、 **MultipartFormDataStreamProvider**します。</span><span class="sxs-lookup"><span data-stu-id="02463-134">This method extracts all of the message parts and writes them into the streams provided by the **MultipartFormDataStreamProvider**.</span></span>

<span data-ttu-id="02463-135">メソッドが完了したらからのファイルに関する情報を取得できます、 **FileData**コレクションであるプロパティの**MultipartFileData**オブジェクト。</span><span class="sxs-lookup"><span data-stu-id="02463-135">When the method completes, you can get information about the files from the **FileData** property, which is a collection of **MultipartFileData** objects.</span></span>

- <span data-ttu-id="02463-136">**MultipartFileData.FileName**ファイルの保存場所、サーバーでローカル ファイルの名前です。</span><span class="sxs-lookup"><span data-stu-id="02463-136">**MultipartFileData.FileName** is the local file name on the server, where the file was saved.</span></span>
- <span data-ttu-id="02463-137">**MultipartFileData.Headers**パーツのヘッダーが含まれています (*いない*要求ヘッダー)。</span><span class="sxs-lookup"><span data-stu-id="02463-137">**MultipartFileData.Headers** contains the part header (*not* the request header).</span></span> <span data-ttu-id="02463-138">これを使用するには、コンテンツにアクセスする\_Disposition および Content-type ヘッダー。</span><span class="sxs-lookup"><span data-stu-id="02463-138">You can use this to access the Content\_Disposition and Content-Type headers.</span></span>

<span data-ttu-id="02463-139">名前からわかるように、 **ReadAsMultipartAsync**は非同期のメソッドです。</span><span class="sxs-lookup"><span data-stu-id="02463-139">As the name suggests, **ReadAsMultipartAsync** is an asynchronous method.</span></span> <span data-ttu-id="02463-140">メソッドの完了後に作業を実行するを使用する[継続タスク](https://msdn.microsoft.com/library/ee372288.aspx)(.NET 4.0) または**await**キーワード (.NET 4.5)。</span><span class="sxs-lookup"><span data-stu-id="02463-140">To perform work after the method completes, use a [continuation task](https://msdn.microsoft.com/library/ee372288.aspx) (.NET 4.0) or the **await** keyword (.NET 4.5).</span></span>

<span data-ttu-id="02463-141">.NET Framework 4.0 バージョンの前のコードを次に示します。</span><span class="sxs-lookup"><span data-stu-id="02463-141">Here is the .NET Framework 4.0 version of the previous code:</span></span>

[!code-csharp[Main](sending-html-form-data-part-2/samples/sample4.cs)]

## <a name="reading-form-control-data"></a><span data-ttu-id="02463-142">フォーム コントロールのデータの読み取り</span><span class="sxs-lookup"><span data-stu-id="02463-142">Reading Form Control Data</span></span>

<span data-ttu-id="02463-143">前に示した HTML フォームには、テキスト入力コントロールが必要があります。</span><span class="sxs-lookup"><span data-stu-id="02463-143">The HTML form that I showed earlier had a text input control.</span></span>

[!code-html[Main](sending-html-form-data-part-2/samples/sample5.html)]

<span data-ttu-id="02463-144">コントロールの値を取得することができます、**フォーム データ**のプロパティ、 **MultipartFormDataStreamProvider**します。</span><span class="sxs-lookup"><span data-stu-id="02463-144">You can get the value of the control from the **FormData** property of the **MultipartFormDataStreamProvider**.</span></span>

[!code-csharp[Main](sending-html-form-data-part-2/samples/sample6.cs?highlight=15)]

<span data-ttu-id="02463-145">**フォーム データ**は、 **NameValueCollection**フォーム コントロールの名前/値ペアを格納しています。</span><span class="sxs-lookup"><span data-stu-id="02463-145">**FormData** is a **NameValueCollection** that contains name/value pairs for the form controls.</span></span> <span data-ttu-id="02463-146">コレクションは、重複するキーを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="02463-146">The collection can contain duplicate keys.</span></span> <span data-ttu-id="02463-147">このフォームを検討してください。</span><span class="sxs-lookup"><span data-stu-id="02463-147">Consider this form:</span></span>

[!code-html[Main](sending-html-form-data-part-2/samples/sample7.html)]

![](sending-html-form-data-part-2/_static/image2.png)

<span data-ttu-id="02463-148">要求本文は、次のようになります。</span><span class="sxs-lookup"><span data-stu-id="02463-148">The request body might look like this:</span></span>

[!code-console[Main](sending-html-form-data-part-2/samples/sample8.cmd)]

<span data-ttu-id="02463-149">その場合は、**フォーム データ**コレクションには、次のキー/値ペアにが含まれます。</span><span class="sxs-lookup"><span data-stu-id="02463-149">In that case, the **FormData** collection would contain the following key/value pairs:</span></span>

- <span data-ttu-id="02463-150">乗車: ラウンドト リップ</span><span class="sxs-lookup"><span data-stu-id="02463-150">trip: round-trip</span></span>
- <span data-ttu-id="02463-151">オプション: 無着陸</span><span class="sxs-lookup"><span data-stu-id="02463-151">options: nonstop</span></span>
- <span data-ttu-id="02463-152">オプション: 日付</span><span class="sxs-lookup"><span data-stu-id="02463-152">options: dates</span></span>
- <span data-ttu-id="02463-153">接続クライアント数: ウィンドウ</span><span class="sxs-lookup"><span data-stu-id="02463-153">seat: window</span></span>
