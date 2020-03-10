---
uid: web-api/overview/advanced/sending-html-form-data-part-2
title: 'ASP.NET Web API での HTML フォームデータの送信: ファイルのアップロードとマルチパート MIME-ASP.NET 4.x'
author: MikeWasson
description: このチュートリアルでは、web API にファイルをアップロードする方法について説明します。 また、マルチパート MIME データを処理する方法についても説明します。
ms.author: riande
ms.date: 06/21/2012
ms.custom: seoapril2019
ms.assetid: a7f3c1b5-69d9-4261-b082-19ffafa5f16a
msc.legacyurl: /web-api/overview/advanced/sending-html-form-data-part-2
msc.type: authoredcontent
ms.openlocfilehash: f5aaebb96f631dfb6b0da1fbca96cd93a6a7fe2d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449212"
---
# <a name="sending-html-form-data-in-aspnet-web-api-file-upload-and-multipart-mime"></a><span data-ttu-id="569b6-104">ASP.NET Web API での HTML フォームデータの送信: ファイルのアップロードとマルチパート MIME</span><span class="sxs-lookup"><span data-stu-id="569b6-104">Sending HTML Form Data in ASP.NET Web API: File Upload and Multipart MIME</span></span>

<span data-ttu-id="569b6-105">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="569b6-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

## <a name="part-2-file-upload-and-multipart-mime"></a><span data-ttu-id="569b6-106">パート 2: ファイルのアップロードとマルチパート MIME</span><span class="sxs-lookup"><span data-stu-id="569b6-106">Part 2: File Upload and Multipart MIME</span></span>

<span data-ttu-id="569b6-107">このチュートリアルでは、web API にファイルをアップロードする方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="569b6-107">This tutorial shows how to upload files to a web API.</span></span> <span data-ttu-id="569b6-108">また、マルチパート MIME データを処理する方法についても説明します。</span><span class="sxs-lookup"><span data-stu-id="569b6-108">It also describes how to process multipart MIME data.</span></span>

> [!NOTE]
> <span data-ttu-id="569b6-109">[完成したプロジェクトをダウンロード](https://code.msdn.microsoft.com/ASPNET-Web-API-File-Upload-a8c0fb0d)します。</span><span class="sxs-lookup"><span data-stu-id="569b6-109">[Download the completed project](https://code.msdn.microsoft.com/ASPNET-Web-API-File-Upload-a8c0fb0d).</span></span>

<span data-ttu-id="569b6-110">ファイルをアップロードするための HTML フォームの例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="569b6-110">Here is an example of an HTML form for uploading a file:</span></span>

[!code-html[Main](sending-html-form-data-part-2/samples/sample1.html)]

![](sending-html-form-data-part-2/_static/image1.png)

<span data-ttu-id="569b6-111">このフォームには、テキスト入力コントロールとファイル入力コントロールが含まれています。</span><span class="sxs-lookup"><span data-stu-id="569b6-111">This form contains a text input control and a file input control.</span></span> <span data-ttu-id="569b6-112">フォームにファイル入力コントロールが含まれている場合、 **enctype**属性は常にマルチパート/フォームデータ&quot;&quot;する必要があります。これにより、フォームがマルチパート MIME メッセージとして送信されることが指定されます。</span><span class="sxs-lookup"><span data-stu-id="569b6-112">When a form contains a file input control, the **enctype** attribute should always be &quot;multipart/form-data&quot;, which specifies that the form will be sent as a multipart MIME message.</span></span>

<span data-ttu-id="569b6-113">マルチパート MIME メッセージの形式は、要求の例を見て理解するのが最も簡単です。</span><span class="sxs-lookup"><span data-stu-id="569b6-113">The format of a multipart MIME message is easiest to understand by looking at an example request:</span></span>

[!code-console[Main](sending-html-form-data-part-2/samples/sample2.cmd)]

<span data-ttu-id="569b6-114">このメッセージは、フォームコントロールごとに1つずつ、2つの*部分*に分かれています。</span><span class="sxs-lookup"><span data-stu-id="569b6-114">This message is divided into two *parts*, one for each form control.</span></span> <span data-ttu-id="569b6-115">部分境界は、ダッシュで始まる線によって示されます。</span><span class="sxs-lookup"><span data-stu-id="569b6-115">Part boundaries are indicated by the lines that start with dashes.</span></span>

> [!NOTE]
> <span data-ttu-id="569b6-116">部分境界には、境界文字列がメッセージ部分の内部に誤って表示されないようにするために、ランダムなコンポーネント (&quot;41184676334&quot;) が含まれています。</span><span class="sxs-lookup"><span data-stu-id="569b6-116">The part boundary includes a random component (&quot;41184676334&quot;) to ensure that the boundary string does not accidentally appear inside a message part.</span></span>

<span data-ttu-id="569b6-117">各メッセージ部分には、1つまたは複数のヘッダーが含まれ、その後にパーツコンテンツが含まれます。</span><span class="sxs-lookup"><span data-stu-id="569b6-117">Each message part contains one or more headers, followed by the part contents.</span></span>

- <span data-ttu-id="569b6-118">コンテンツディスポジションヘッダーには、コントロールの名前が含まれます。</span><span class="sxs-lookup"><span data-stu-id="569b6-118">The Content-Disposition header includes the name of the control.</span></span> <span data-ttu-id="569b6-119">ファイルの場合は、ファイル名も含まれます。</span><span class="sxs-lookup"><span data-stu-id="569b6-119">For files, it also contains the file name.</span></span>
- <span data-ttu-id="569b6-120">Content-type ヘッダーは、パーツ内のデータを記述します。</span><span class="sxs-lookup"><span data-stu-id="569b6-120">The Content-Type header describes the data in the part.</span></span> <span data-ttu-id="569b6-121">このヘッダーを省略した場合、既定値は text/plain です。</span><span class="sxs-lookup"><span data-stu-id="569b6-121">If this header is omitted, the default is text/plain.</span></span>

<span data-ttu-id="569b6-122">前の例では、ユーザーが GrandCanyon という名前のファイルをアップロードしました。コンテンツの種類は image/jpeg です。テキスト入力の値は、夏休暇&quot;&quot;でした。</span><span class="sxs-lookup"><span data-stu-id="569b6-122">In the previous example, the user uploaded a file named GrandCanyon.jpg, with content type image/jpeg; and the value of the text input was &quot;Summer Vacation&quot;.</span></span>

## <a name="file-upload"></a><span data-ttu-id="569b6-123">ファイルのアップロード</span><span class="sxs-lookup"><span data-stu-id="569b6-123">File Upload</span></span>

<span data-ttu-id="569b6-124">次に、マルチパート MIME メッセージからファイルを読み取る Web API コントローラーを見てみましょう。</span><span class="sxs-lookup"><span data-stu-id="569b6-124">Now let's look at a Web API controller that reads files from a multipart MIME message.</span></span> <span data-ttu-id="569b6-125">コントローラーはファイルを非同期的に読み取ります。</span><span class="sxs-lookup"><span data-stu-id="569b6-125">The controller will read the files asynchronously.</span></span> <span data-ttu-id="569b6-126">Web API は、[タスクベースのプログラミングモデル](https://msdn.microsoft.com/library/dd460693.aspx)を使用した非同期アクションをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="569b6-126">Web API supports asynchronous actions using the [task-based programming model](https://msdn.microsoft.com/library/dd460693.aspx).</span></span> <span data-ttu-id="569b6-127">まず、 **async**キーワードと**await**キーワードをサポートする .NET Framework 4.5 を対象とするコードを次に示します。</span><span class="sxs-lookup"><span data-stu-id="569b6-127">First, here is the code if you are targeting .NET Framework 4.5, which supports the **async** and **await** keywords.</span></span>

[!code-csharp[Main](sending-html-form-data-part-2/samples/sample3.cs)]

<span data-ttu-id="569b6-128">コントローラーアクションにはパラメーターがないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="569b6-128">Notice that the controller action does not take any parameters.</span></span> <span data-ttu-id="569b6-129">これは、メディアの種類のフォーマッタを呼び出さずに、アクション内で要求本文を処理するためです。</span><span class="sxs-lookup"><span data-stu-id="569b6-129">That's because we process the request body inside the action, without invoking a media-type formatter.</span></span>

<span data-ttu-id="569b6-130">**Ismultipartcontent**メソッドは、要求にマルチパート MIME メッセージが含まれているかどうかを確認します。</span><span class="sxs-lookup"><span data-stu-id="569b6-130">The **IsMultipartContent** method checks whether the request contains a multipart MIME message.</span></span> <span data-ttu-id="569b6-131">それ以外の場合、コントローラーは HTTP 状態コード 415 (サポートされていないメディアの種類) を返します。</span><span class="sxs-lookup"><span data-stu-id="569b6-131">If not, the controller returns HTTP status code 415 (Unsupported Media Type).</span></span>

<span data-ttu-id="569b6-132">**Multipartformdatastreamprovider**クラスは、アップロードされたファイルのファイルストリームを割り当てるヘルパーオブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="569b6-132">The **MultipartFormDataStreamProvider** class is a helper object that allocates file streams for uploaded files.</span></span> <span data-ttu-id="569b6-133">マルチパート MIME メッセージを読み取るには、 **Readasmultipartasync**メソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="569b6-133">To read the multipart MIME message, call the **ReadAsMultipartAsync** method.</span></span> <span data-ttu-id="569b6-134">このメソッドは、すべてのメッセージ部分を抽出し、 **Multipartformdatastreamprovider**によって提供されるストリームに書き込みます。</span><span class="sxs-lookup"><span data-stu-id="569b6-134">This method extracts all of the message parts and writes them into the streams provided by the **MultipartFormDataStreamProvider**.</span></span>

<span data-ttu-id="569b6-135">メソッドが完了すると、 **FileData**プロパティからファイルに関する情報を取得できます。このプロパティは、 **MultipartFileData**オブジェクトのコレクションです。</span><span class="sxs-lookup"><span data-stu-id="569b6-135">When the method completes, you can get information about the files from the **FileData** property, which is a collection of **MultipartFileData** objects.</span></span>

- <span data-ttu-id="569b6-136">**MultipartFileData**は、ファイルが保存されたサーバー上のローカルファイル名です。</span><span class="sxs-lookup"><span data-stu-id="569b6-136">**MultipartFileData.FileName** is the local file name on the server, where the file was saved.</span></span>
- <span data-ttu-id="569b6-137">**MultipartFileData**には、(要求ヘッダーでは*なく*) パーツヘッダーが含まれています。</span><span class="sxs-lookup"><span data-stu-id="569b6-137">**MultipartFileData.Headers** contains the part header (*not* the request header).</span></span> <span data-ttu-id="569b6-138">これを使用して、コンテンツ\_の内容およびコンテンツタイプのヘッダーにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="569b6-138">You can use this to access the Content\_Disposition and Content-Type headers.</span></span>

<span data-ttu-id="569b6-139">名前が示すように、 **Readasmultipartasync**は非同期メソッドです。</span><span class="sxs-lookup"><span data-stu-id="569b6-139">As the name suggests, **ReadAsMultipartAsync** is an asynchronous method.</span></span> <span data-ttu-id="569b6-140">メソッドの完了後に作業を実行するには、[継続タスク](https://msdn.microsoft.com/library/ee372288.aspx)(.net 4.0) または**await**キーワード (.net 4.5) を使用します。</span><span class="sxs-lookup"><span data-stu-id="569b6-140">To perform work after the method completes, use a [continuation task](https://msdn.microsoft.com/library/ee372288.aspx) (.NET 4.0) or the **await** keyword (.NET 4.5).</span></span>

<span data-ttu-id="569b6-141">前のコードの .NET Framework 4.0 バージョンを次に示します。</span><span class="sxs-lookup"><span data-stu-id="569b6-141">Here is the .NET Framework 4.0 version of the previous code:</span></span>

[!code-csharp[Main](sending-html-form-data-part-2/samples/sample4.cs)]

## <a name="reading-form-control-data"></a><span data-ttu-id="569b6-142">フォームコントロールデータの読み取り</span><span class="sxs-lookup"><span data-stu-id="569b6-142">Reading Form Control Data</span></span>

<span data-ttu-id="569b6-143">先ほど見た HTML フォームには、テキスト入力コントロールがありました。</span><span class="sxs-lookup"><span data-stu-id="569b6-143">The HTML form that I showed earlier had a text input control.</span></span>

[!code-html[Main](sending-html-form-data-part-2/samples/sample5.html)]

<span data-ttu-id="569b6-144">このコントロールの値は、 **Multipartformdatastreamprovider**の**formdata**プロパティから取得できます。</span><span class="sxs-lookup"><span data-stu-id="569b6-144">You can get the value of the control from the **FormData** property of the **MultipartFormDataStreamProvider**.</span></span>

[!code-csharp[Main](sending-html-form-data-part-2/samples/sample6.cs?highlight=15)]

<span data-ttu-id="569b6-145">**Formdata**は、フォームコントロールの名前と値のペアを含む**NameValueCollection**です。</span><span class="sxs-lookup"><span data-stu-id="569b6-145">**FormData** is a **NameValueCollection** that contains name/value pairs for the form controls.</span></span> <span data-ttu-id="569b6-146">コレクションには重複するキーを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="569b6-146">The collection can contain duplicate keys.</span></span> <span data-ttu-id="569b6-147">次の形式を考えてみましょう。</span><span class="sxs-lookup"><span data-stu-id="569b6-147">Consider this form:</span></span>

[!code-html[Main](sending-html-form-data-part-2/samples/sample7.html)]

![](sending-html-form-data-part-2/_static/image2.png)

<span data-ttu-id="569b6-148">要求本文は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="569b6-148">The request body might look like this:</span></span>

[!code-console[Main](sending-html-form-data-part-2/samples/sample8.cmd)]

<span data-ttu-id="569b6-149">その場合、 **Formdata**コレクションには次のキーと値のペアが含まれます。</span><span class="sxs-lookup"><span data-stu-id="569b6-149">In that case, the **FormData** collection would contain the following key/value pairs:</span></span>

- <span data-ttu-id="569b6-150">旅行: ラウンドトリップ</span><span class="sxs-lookup"><span data-stu-id="569b6-150">trip: round-trip</span></span>
- <span data-ttu-id="569b6-151">オプション: 無着陸</span><span class="sxs-lookup"><span data-stu-id="569b6-151">options: nonstop</span></span>
- <span data-ttu-id="569b6-152">オプション: 日付</span><span class="sxs-lookup"><span data-stu-id="569b6-152">options: dates</span></span>
- <span data-ttu-id="569b6-153">座席: ウィンドウ</span><span class="sxs-lookup"><span data-stu-id="569b6-153">seat: window</span></span>
