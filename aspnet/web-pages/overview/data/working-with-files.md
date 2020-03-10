---
uid: web-pages/overview/data/working-with-files
title: ASP.NET Web ページ (Razor) サイトでのファイルの操作 |Microsoft Docs
author: Rick-Anderson
description: この章では、ファイルの読み取り、書き込み、追加、削除、およびアップロードを行う方法について説明します。
ms.author: riande
ms.date: 02/20/2014
ms.assetid: eee916e4-ba4c-439a-a24e-68df7d45a569
msc.legacyurl: /web-pages/overview/data/working-with-files
msc.type: authoredcontent
ms.openlocfilehash: 684c47a8a8480dc040e5144144577c94c35d39e5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78521884"
---
# <a name="working-with-files-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="8e4b0-103">ASP.NET Web ページ (Razor) サイトでのファイルの操作</span><span class="sxs-lookup"><span data-stu-id="8e4b0-103">Working with Files in an ASP.NET Web Pages (Razor) Site</span></span>

<span data-ttu-id="8e4b0-104">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="8e4b0-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="8e4b0-105">この記事では、ASP.NET Web ページ (Razor) サイトでファイルの読み取り、書き込み、追加、削除、およびアップロードを行う方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-105">This article explains how to read, write, append, delete, and upload files in an ASP.NET Web Pages (Razor) site.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="8e4b0-106">イメージをアップロードして操作する場合 (たとえば、画像を反転またはサイズ変更する場合) は、「 [ASP.NET Web ページサイトでのイメージの操作](/aspnet/web-pages/overview/ui-layouts-and-themes/9-working-with-images)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-106">If you want to upload images and manipulate them (for example, flip or resize them), see [Working with Images in an ASP.NET Web Pages Site](/aspnet/web-pages/overview/ui-layouts-and-themes/9-working-with-images).</span></span>
> 
> 
> <span data-ttu-id="8e4b0-107">**学習内容:**</span><span class="sxs-lookup"><span data-stu-id="8e4b0-107">**What you'll learn:**</span></span> 
> 
> - <span data-ttu-id="8e4b0-108">テキストファイルを作成してデータを書き込む方法。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-108">How to create a text file and write data to it.</span></span>
> - <span data-ttu-id="8e4b0-109">既存のファイルにデータを追加する方法。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-109">How to append data to an existing file.</span></span>
> - <span data-ttu-id="8e4b0-110">ファイルを読み取り、そこから表示する方法。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-110">How to read a file and display from it.</span></span>
> - <span data-ttu-id="8e4b0-111">Web サイトからファイルを削除する方法。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-111">How to delete files from a website.</span></span>
> - <span data-ttu-id="8e4b0-112">ユーザーが1つまたは複数のファイルをアップロードできるようにする方法。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-112">How to let users upload one file or multiple files.</span></span>
> 
> <span data-ttu-id="8e4b0-113">この記事で紹介する ASP.NET プログラミング機能を次に示します。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-113">These are the ASP.NET programming features introduced in the article:</span></span>
> 
> - <span data-ttu-id="8e4b0-114">`File` オブジェクト。ファイルを管理する方法を提供します。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-114">The `File` object, which provides a way to manage files.</span></span>
> - <span data-ttu-id="8e4b0-115">`FileUpload` ヘルパー。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-115">The `FileUpload` helper.</span></span>
> - <span data-ttu-id="8e4b0-116">`Path` オブジェクト。パスとファイル名を操作できるメソッドを提供します。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-116">The `Path` object, which provides methods that let you manipulate path and file names.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="8e4b0-117">このチュートリアルで使用されているソフトウェアのバージョン</span><span class="sxs-lookup"><span data-stu-id="8e4b0-117">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="8e4b0-118">ASP.NET Web ページ (Razor) 2</span><span class="sxs-lookup"><span data-stu-id="8e4b0-118">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="8e4b0-119">WebMatrix 2</span><span class="sxs-lookup"><span data-stu-id="8e4b0-119">WebMatrix 2</span></span>
>   
> 
> <span data-ttu-id="8e4b0-120">このチュートリアルでは、WebMatrix 3 も使用できます。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-120">This tutorial also works with WebMatrix 3.</span></span>

<a id="Creating_a_Text_File"></a>
## <a name="creating-a-text-file-and-writing-data-to-it"></a><span data-ttu-id="8e4b0-121">テキストファイルの作成とデータの書き込み</span><span class="sxs-lookup"><span data-stu-id="8e4b0-121">Creating a Text File and Writing Data to It</span></span>

<span data-ttu-id="8e4b0-122">Web サイトのデータベースを使用するだけでなく、ファイルを操作することもできます。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-122">In addition to using a database in your website, you might work with files.</span></span> <span data-ttu-id="8e4b0-123">たとえば、サイトのデータを格納する簡単な方法として、テキストファイルを使用する場合があります。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-123">For example, you might use text files as a simple way to store data for the site.</span></span> <span data-ttu-id="8e4b0-124">(データを格納するために使用されるテキストファイルは、*フラットファイル*と呼ばれることもあります)。テキストファイルは、 *.txt*、 *.xml*、 *.csv* (コンマ区切りの値) など、異なる形式にすることができます。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-124">(A text file that's used to store data is sometimes called a *flat file*.) Text files can be in different formats, like *.txt*, *.xml*, or *.csv* (comma-delimited values).</span></span>

<span data-ttu-id="8e4b0-125">データをテキストファイルに格納する場合は、`File.WriteAllText` メソッドを使用して、作成するファイルとそれに書き込むデータを指定します。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-125">If you want to store data in a text file, you can use the `File.WriteAllText` method to specify the file to create and the data to write to it.</span></span> <span data-ttu-id="8e4b0-126">この手順では、3つの `input` 要素 (名、姓、電子メールアドレス) と **[送信]** ボタンを持つ単純なフォームを含むページを作成します。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-126">In this procedure, you'll create a page that contains a simple form with three `input` elements (first name, last name, and email address) and a **Submit** button.</span></span> <span data-ttu-id="8e4b0-127">ユーザーがフォームを送信すると、ユーザーの入力がテキストファイルに保存されます。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-127">When the user submits the form, you'll store the user's input in a text file.</span></span>

1. <span data-ttu-id="8e4b0-128">*App\_Data*という名前の新しいフォルダーがまだ存在しない場合は作成します。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-128">Create a new folder named *App\_Data*, if it doesn't exist already.</span></span>
2. <span data-ttu-id="8e4b0-129">Web サイトのルートで、 *UserData*という名前の新しいファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-129">At the root of your website, create a new file named *UserData.cshtml*.</span></span>
3. <span data-ttu-id="8e4b0-130">既存のコンテンツを次の内容に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-130">Replace the existing content with the following:</span></span> 

    [!code-cshtml[Main](working-with-files/samples/sample1.cshtml)]

    <span data-ttu-id="8e4b0-131">HTML マークアップによって、3つのテキストボックスを持つフォームが作成されます。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-131">The HTML markup creates the form with the three text boxes.</span></span> <span data-ttu-id="8e4b0-132">コードでは、`IsPost` プロパティを使用して、処理を開始する前にページが送信されたかどうかを判断します。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-132">In the code, you use the `IsPost` property to determine whether the page has been submitted before you start processing.</span></span>

    <span data-ttu-id="8e4b0-133">最初のタスクでは、ユーザー入力を取得し、変数に割り当てます。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-133">The first task is to get the user input and assign it to variables.</span></span> <span data-ttu-id="8e4b0-134">次に、別の変数の値を1つのコンマ区切りの文字列に連結します。この文字列は、別の変数に格納されます。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-134">The code then concatenates the values of the separate variables into one comma-delimited string, which is then stored in a different variable.</span></span> <span data-ttu-id="8e4b0-135">コンマ区切り記号は引用符 (",") に含まれている文字列であることに注意してください。これは、作成中の大きな文字列にコンマが埋め込まれているためです。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-135">Notice that the comma separator is a string contained in quotation marks (","), because you're literally embedding a comma into the big string that you're creating.</span></span> <span data-ttu-id="8e4b0-136">連結するデータの最後に、`Environment.NewLine`を追加します。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-136">At the end of the data that you concatenate together, you add `Environment.NewLine`.</span></span> <span data-ttu-id="8e4b0-137">改行 (改行文字) が追加されます。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-137">This adds a line break (a newline character).</span></span> <span data-ttu-id="8e4b0-138">この連結をすべて使用して作成しているのは、次のような文字列です。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-138">What you're creating with all this concatenation is a string that looks like this:</span></span>

    [!code-css[Main](working-with-files/samples/sample2.css)]

    <span data-ttu-id="8e4b0-139">(末尾に非表示の改行があります)。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-139">(With an invisible line break at the end.)</span></span>

    <span data-ttu-id="8e4b0-140">次に、データを格納するファイルの場所と名前を含む変数 (`dataFile`) を作成します。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-140">You then create a variable (`dataFile`) that contains the location and name of the file to store the data in.</span></span> <span data-ttu-id="8e4b0-141">場所を設定するには、特別な処理が必要です。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-141">Setting the location requires some special handling.</span></span> <span data-ttu-id="8e4b0-142">Web サイトでは、web サーバー上のファイルの*C:\Folder\File.txt*などの絶対パスをコードで参照することは不適切です。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-142">In websites, it's a bad practice to refer in code to absolute paths like *C:\Folder\File.txt* for files on the web server.</span></span> <span data-ttu-id="8e4b0-143">Web サイトが移動された場合、絶対パスは間違っています。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-143">If a website is moved, an absolute path will be wrong.</span></span> <span data-ttu-id="8e4b0-144">さらに、ホストされているサイト (自分のコンピューターではなく) では、通常、コードを記述する際に正しいパスを把握している必要はありません。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-144">Moreover, for a hosted site (as opposed to on your own computer) you typically don't even know what the correct path is when you're writing the code.</span></span>

    <span data-ttu-id="8e4b0-145">ただし (現時点では、ファイルの書き込みのように) 完全なパスが必要になる場合があります。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-145">But sometimes (like now, for writing a file) you do need a complete path.</span></span> <span data-ttu-id="8e4b0-146">解決策は、`Server` オブジェクトの `MapPath` メソッドを使用することです。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-146">The solution is to use the `MapPath` method of the `Server` object.</span></span> <span data-ttu-id="8e4b0-147">これにより、web サイトへの完全なパスが返されます。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-147">This returns the complete path to your website.</span></span> <span data-ttu-id="8e4b0-148">Web サイトのルートのパスを取得するには、`~` 演算子 (サイトの仮想ルートを represen) を使用して `MapPath`します。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-148">To get the path for the website root, you user the `~` operator (to represen the site's virtual root) to `MapPath`.</span></span> <span data-ttu-id="8e4b0-149">また、サブフォルダー名 (たとえば、*アプリ\_Data/* ) を渡して、そのサブフォルダーのパスを取得することもできます。その後、完全なパスを作成するために、メソッドから返されるものに追加情報を連結できます。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-149">(You can also pass a subfolder name to it, like *~/App\_Data/*, to get the path for that subfolder.) You can then concatenate additional information onto whatever the method returns in order to create a complete path.</span></span> <span data-ttu-id="8e4b0-150">この例では、ファイル名を追加します。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-150">In this example, you add a file name.</span></span> <span data-ttu-id="8e4b0-151">(ファイルとフォルダーのパスを操作する方法の詳細については[、「Razor 構文を使用した ASP.NET Web ページプログラミングの概要」を](https://go.microsoft.com/fwlink/?LinkId=195205#ID_WorkingWithFileAndFolderPaths)参照してください)。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-151">(You can read more about how to work with file and folder paths in [Introduction to ASP.NET Web Pages Programming Using the Razor Syntax](https://go.microsoft.com/fwlink/?LinkId=195205#ID_WorkingWithFileAndFolderPaths).)</span></span>

    <span data-ttu-id="8e4b0-152">ファイルは、 *App\_Data*フォルダーに保存されます。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-152">The file is saved in the *App\_Data* folder.</span></span> <span data-ttu-id="8e4b0-153">このフォルダーは、「 [ASP.NET Web ページサイトでのデータベースの操作の概要](https://go.microsoft.com/fwlink/?LinkId=195209)」で説明されているように、データファイルの格納に使用される ASP.NET の特別なフォルダーです。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-153">This folder is a special folder in ASP.NET that's used to store data files, as described in [Introduction to Working with a Database in ASP.NET Web Pages Sites](https://go.microsoft.com/fwlink/?LinkId=195209).</span></span>

    <span data-ttu-id="8e4b0-154">`File` オブジェクトの `WriteAllText` メソッドによって、データがファイルに書き込まれます。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-154">The `WriteAllText` method of the `File` object writes the data to the file.</span></span> <span data-ttu-id="8e4b0-155">このメソッドは、書き込み先のファイルの名前 (パスを含む) と書き込み先の実際のデータの2つのパラメーターを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-155">This method takes two parameters: the name (with path) of the file to write to, and the actual data to write.</span></span> <span data-ttu-id="8e4b0-156">最初のパラメーターの名前にプレフィックスとして `@` 文字があることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-156">Notice that the name of the first parameter has an `@` character as a prefix.</span></span> <span data-ttu-id="8e4b0-157">これは、逐語的文字列リテラルを提供していること、および "/" のような文字を特別な方法では解釈できないことを ASP.NET に通知します。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-157">This tells ASP.NET that you're providing a verbatim string literal, and that characters like "/" should not be interpreted in special ways.</span></span> <span data-ttu-id="8e4b0-158">(詳細については、「 [Razor 構文を使用した ASP.NET Web プログラミングの概要」を](https://go.microsoft.com/fwlink/?LinkId=195205#ID_WorkingWithFileAndFolderPaths)参照してください)。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-158">(For more information, see [Introduction to ASP.NET Web Programming Using the Razor Syntax](https://go.microsoft.com/fwlink/?LinkId=195205#ID_WorkingWithFileAndFolderPaths).)</span></span>

    > [!NOTE]
    > <span data-ttu-id="8e4b0-159">コードで*App\_Data*フォルダーにファイルを保存するには、そのフォルダーに対する読み取り/書き込みアクセス許可がアプリケーションに必要です。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-159">In order for your code to save files in the *App\_Data* folder, the application needs read-write permissions for that folder.</span></span> <span data-ttu-id="8e4b0-160">開発用コンピューターでは、これは通常は問題ではありません。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-160">On your development computer this is not typically an issue.</span></span> <span data-ttu-id="8e4b0-161">ただし、サイトをホスティングプロバイダーの web サーバーに発行する場合は、これらのアクセス許可を明示的に設定する必要がある場合があります。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-161">However, when you publish your site to a hosting provider's web server, you might need to explicitly set those permissions.</span></span> <span data-ttu-id="8e4b0-162">このコードをホスティングプロバイダーのサーバーで実行し、エラーが発生した場合は、ホスティングプロバイダーに確認して、これらのアクセス許可を設定する方法を確認してください。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-162">If you run this code on a hosting provider's server and get errors, check with the hosting provider to find out how to set those permissions.</span></span>

- <span data-ttu-id="8e4b0-163">ブラウザーでページを実行します。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-163">Run the page in a browser.</span></span> 

    ![](working-with-files/_static/image1.jpg)
- <span data-ttu-id="8e4b0-164">フィールドに値を入力し、 **[送信]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-164">Enter values into the fields and then click **Submit**.</span></span>
- <span data-ttu-id="8e4b0-165">ブラウザーを閉じます。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-165">Close the browser.</span></span>
- <span data-ttu-id="8e4b0-166">プロジェクトに戻り、ビューを更新します。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-166">Return to the project and refresh the view.</span></span>
- <span data-ttu-id="8e4b0-167">*データ .txt*ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-167">Open the *data.txt* file.</span></span> <span data-ttu-id="8e4b0-168">フォームに送信したデータは、ファイルにあります。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-168">The data you submitted in the form is in the file.</span></span> 

    ![[画像]](working-with-files/_static/image2.jpg)
- <span data-ttu-id="8e4b0-170">*データ .txt*ファイルを閉じます。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-170">Close the *data.txt* file.</span></span>

<a id="Appending_Data"></a>
## <a name="appending-data-to-an-existing-file"></a><span data-ttu-id="8e4b0-171">既存のファイルへのデータの追加</span><span class="sxs-lookup"><span data-stu-id="8e4b0-171">Appending Data to an Existing File</span></span>

<span data-ttu-id="8e4b0-172">前の例では、`WriteAllText` を使用してテキストファイルを作成し、そこに1つのデータのみが含まれるようにしていました。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-172">In the previous example, you used `WriteAllText` to create a text file that's got just one piece of data in it.</span></span> <span data-ttu-id="8e4b0-173">メソッドを再度呼び出して同じファイル名を渡すと、既存のファイルは完全に上書きされます。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-173">If you call the method again and pass it the same file name, the existing file is completely overwritten.</span></span> <span data-ttu-id="8e4b0-174">ただし、ファイルを作成した後は、多くの場合、ファイルの末尾に新しいデータを追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-174">However, after you've created a file you often want to add new data to the end of the file.</span></span> <span data-ttu-id="8e4b0-175">これは、`File` オブジェクトの `AppendAllText` メソッドを使用して行うことができます。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-175">You can do that using the `AppendAllText` method of the `File` object.</span></span>

1. <span data-ttu-id="8e4b0-176">Web サイトで、 *UserData*ファイルのコピーを作成し、そのコピーに*UserDataMultiple*という名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-176">In the website, make a copy of the *UserData.cshtml* file and name the copy *UserDataMultiple.cshtml*.</span></span>
2. <span data-ttu-id="8e4b0-177">開始 `<!DOCTYPE html>` タグの前にあるコードブロックを次のコードブロックに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-177">Replace the code block before the opening `<!DOCTYPE html>` tag with the following code block:</span></span> 

    [!code-cshtml[Main](working-with-files/samples/sample3.cshtml)]

    <span data-ttu-id="8e4b0-178">このコードには、前の例の変更が1つあります。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-178">This code has one change in it from the previous example.</span></span> <span data-ttu-id="8e4b0-179">`WriteAllText`を使用する代わりに、`the AppendAllText` メソッドを使用します。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-179">Instead of using `WriteAllText`, it uses `the AppendAllText` method.</span></span> <span data-ttu-id="8e4b0-180">メソッドは似ていますが、`AppendAllText` はファイルの末尾にデータを追加する点が異なります。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-180">The methods are similar, except that `AppendAllText` adds the data to the end of the file.</span></span> <span data-ttu-id="8e4b0-181">`WriteAllText`の場合と同様に、ファイルがまだ存在しない場合は `AppendAllText` によって作成されます。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-181">As with `WriteAllText`, `AppendAllText` creates the file if it doesn't already exist.</span></span>
3. <span data-ttu-id="8e4b0-182">ブラウザーでページを実行します。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-182">Run the page in a browser.</span></span>
4. <span data-ttu-id="8e4b0-183">フィールドの値を入力し、 **[送信]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-183">Enter values for the fields and then click **Submit**.</span></span>
5. <span data-ttu-id="8e4b0-184">データをさらに追加し、フォームを再度送信します。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-184">Add more data and submit the form again.</span></span>
6. <span data-ttu-id="8e4b0-185">プロジェクトに戻り、プロジェクトフォルダーを右クリックして、[最新の状態に**更新**] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-185">Return to your project, right-click the project folder, and then click **Refresh**.</span></span>
7. <span data-ttu-id="8e4b0-186">*データ .txt*ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-186">Open the *data.txt* file.</span></span> <span data-ttu-id="8e4b0-187">これで、入力したばかりの新しいデータが表示されます。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-187">It now contains the new data that you just entered.</span></span> 

    ![[画像]](working-with-files/_static/image3.jpg)

<a id="Reading_and_Displaying_Data"></a>
## <a name="reading-and-displaying-data-from-a-file"></a><span data-ttu-id="8e4b0-189">ファイルのデータの読み取りと表示</span><span class="sxs-lookup"><span data-stu-id="8e4b0-189">Reading and Displaying Data from a File</span></span>

<span data-ttu-id="8e4b0-190">テキストファイルにデータを書き込む必要がない場合でも、場合によっては、データの読み取りが必要になることがあります。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-190">Even if you don't need to write data to a text file, you'll probably sometimes need to read data from one.</span></span> <span data-ttu-id="8e4b0-191">これを行うには、`File` オブジェクトをもう一度使用します。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-191">To do this, you can again use the `File` object.</span></span> <span data-ttu-id="8e4b0-192">`File` オブジェクトを使用すると、各行を個別に (改行で区切って) 読み取ることも、個々の項目がどのように分離されているかにかかわらず読み取ることもできます。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-192">You can use the `File` object to read each line individually (separated by line breaks) or to read individual item no matter how they're separated.</span></span>

<span data-ttu-id="8e4b0-193">この手順では、前の例で作成したデータを読み取り、表示する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-193">This procedure shows you how to read and display the data that you created in the previous example.</span></span>

1. <span data-ttu-id="8e4b0-194">Web サイトのルートで、 *Displaydata. cshtml*という名前の新しいファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-194">At the root of your website, create a new file named *DisplayData.cshtml*.</span></span>
2. <span data-ttu-id="8e4b0-195">既存のコンテンツを次の内容に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-195">Replace the existing content with the following:</span></span> 

    [!code-cshtml[Main](working-with-files/samples/sample4.cshtml)]

    <span data-ttu-id="8e4b0-196">このコードは、次のメソッド呼び出しを使用して、前の例で作成したファイルを `userData`という名前の変数に読み取ります。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-196">The code starts by reading the file that you created in the previous example into a variable named `userData`, using this method call:</span></span>

    [!code-css[Main](working-with-files/samples/sample5.css)]

    <span data-ttu-id="8e4b0-197">これを行うコードは、`if` ステートメントの内部にあります。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-197">The code to do this is inside an `if` statement.</span></span> <span data-ttu-id="8e4b0-198">ファイルを読み取る場合は、`File.Exists` メソッドを使用して、ファイルが使用可能かどうかを最初に確認することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-198">When you want to read a file, it's a good idea to use the `File.Exists` method to determine first whether the file is available.</span></span> <span data-ttu-id="8e4b0-199">このコードでは、ファイルが空かどうかも確認します。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-199">The code also checks whether the file is empty.</span></span>

    <span data-ttu-id="8e4b0-200">ページの本文には、2つの `foreach` ループが含まれており、その中に入れ子になっています。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-200">The body of the page contains two `foreach` loops, one nested inside the other.</span></span> <span data-ttu-id="8e4b0-201">外側の `foreach` ループは、データファイルから一度に1行を取得します。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-201">The outer `foreach` loop gets one line at a time from the data file.</span></span> <span data-ttu-id="8e4b0-202">この場合、行はファイル&#8212;内の改行によって定義されます。つまり、各データ項目はそれぞれの行にあります。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-202">In this case, the lines are defined by line breaks in the file &#8212; that is, each data item is on its own line.</span></span> <span data-ttu-id="8e4b0-203">外側のループは、順序付けられたリスト (`<ol>` 要素) 内に新しい項目 (`<li>` 要素) を作成します。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-203">The outer loop creates a new item (`<li>` element) inside an ordered list (`<ol>` element).</span></span>

    <span data-ttu-id="8e4b0-204">内側のループでは、区切り記号としてコンマを使用して、各データ行を項目 (フィールド) に分割します。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-204">The inner loop splits each data line into items (fields) using a comma as a delimiter.</span></span> <span data-ttu-id="8e4b0-205">(前の例に基づいて、各行には、名、姓&#8212; 、電子メールアドレスという3つのフィールドが含まれており、それぞれがコンマで区切られています)。内側のループでは、`<ul>` リストも作成され、データ行のフィールドごとに1つのリスト項目が表示されます。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-205">(Based on the previous example, this means that each line contains three fields &#8212; the first name, last name, and email address, each separated by a comma.) The inner loop also creates a `<ul>` list and displays one list item for each field in the data line.</span></span>

    <span data-ttu-id="8e4b0-206">このコードは、配列と `char` データ型の2つのデータ型を使用する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-206">The code illustrates how to use two data types, an array and the `char` data type.</span></span> <span data-ttu-id="8e4b0-207">`File.ReadAllLines` メソッドはデータを配列として返すため、配列が必要です。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-207">The array is required because the `File.ReadAllLines` method returns data as an array.</span></span> <span data-ttu-id="8e4b0-208">`Split` メソッドは、各要素の型が `char`の `array` を返すため、`char` のデータ型が必要です。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-208">The `char` data type is required because the `Split` method returns an `array` in which each element is of the type `char`.</span></span> <span data-ttu-id="8e4b0-209">(配列の詳細については、「 [Razor 構文を使用した ASP.NET Web プログラミングの概要](https://go.microsoft.com/fwlink/?LinkId=202890#ID_CollectionsAndObjects)」を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-209">(For information about arrays, see [Introduction to ASP.NET Web Programming Using the Razor Syntax](https://go.microsoft.com/fwlink/?LinkId=202890#ID_CollectionsAndObjects).)</span></span>
3. <span data-ttu-id="8e4b0-210">ブラウザーでページを実行します。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-210">Run the page in a browser.</span></span> <span data-ttu-id="8e4b0-211">前の例で入力したデータが表示されます。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-211">The data you entered for the previous examples is displayed.</span></span> 

    ![[画像]](working-with-files/_static/image4.jpg)

> [!TIP] 
> 
> <span data-ttu-id="8e4b0-213">**Microsoft Excel のコンマ区切りファイルからのデータの表示**</span><span class="sxs-lookup"><span data-stu-id="8e4b0-213">**Displaying Data from a Microsoft Excel Comma-Delimited File**</span></span>
> 
> <span data-ttu-id="8e4b0-214">Microsoft Excel を使用して、スプレッドシートに含まれるデータをコンマ区切りファイル ( *.csv*ファイル) として保存できます。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-214">You can use Microsoft Excel to save the data contained in a spreadsheet as a comma-delimited file (*.csv* file).</span></span> <span data-ttu-id="8e4b0-215">この場合、ファイルは Excel 形式ではなく、プレーンテキストで保存されます。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-215">When you do, the file is saved in plain text, not in Excel format.</span></span> <span data-ttu-id="8e4b0-216">スプレッドシート内の各行は、テキストファイル内の改行で区切られ、各データ項目はコンマで区切られます。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-216">Each row in the spreadsheet is separated by a line break in the text file, and each data item is separated by a comma.</span></span> <span data-ttu-id="8e4b0-217">前の例に示したコードを使用して、コード内のデータファイルの名前を変更するだけで、Excel のコンマ区切りファイルを読み取ることができます。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-217">You can use the code shown in the previous example to read an Excel comma-delimited file just by changing the name of the data file in your code.</span></span>

<a id="Deleting_Files"></a>
## <a name="deleting-files"></a><span data-ttu-id="8e4b0-218">ファイルの削除</span><span class="sxs-lookup"><span data-stu-id="8e4b0-218">Deleting Files</span></span>

<span data-ttu-id="8e4b0-219">Web サイトからファイルを削除するには、`File.Delete` メソッドを使用します。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-219">To delete files from your website, you can use the `File.Delete` method.</span></span> <span data-ttu-id="8e4b0-220">この手順では、ファイルの名前がわかっている場合に、ユーザーが*images*フォルダーからイメージ ( *.jpg*ファイル) を削除できるようにする方法を示します。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-220">This procedure shows how to let users delete an image (*.jpg* file) from an *images* folder if they know the name of the file.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="8e4b0-221">**重要**運用 web サイトでは、通常、データを変更できるユーザーを制限します。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-221">**Important** In a production website, you typically restrict who's allowed to make changes to the data.</span></span> <span data-ttu-id="8e4b0-222">メンバーシップの設定方法と、サイトでのタスクの実行をユーザーに承認する方法の詳細については、「 [ASP.NET Web ページサイトへのセキュリティとメンバーシップの追加](https://go.microsoft.com/fwlink/?LinkId=202904)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-222">For information about how to set up membership and about ways to authorize users to perform tasks on the site, see [Adding Security and Membership to an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=202904).</span></span>

1. <span data-ttu-id="8e4b0-223">Web サイトで、 *images*という名前のサブフォルダーを作成します。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-223">In the website, create a subfolder named *images*.</span></span>
2. <span data-ttu-id="8e4b0-224">1つまたは複数の *.jpg*ファイルを*images*フォルダーにコピーします。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-224">Copy one or more *.jpg* files into the *images* folder.</span></span>
3. <span data-ttu-id="8e4b0-225">Web サイトのルートで、 *FileDelete*という名前の新しいファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-225">In the root of the website, create a new file named *FileDelete.cshtml*.</span></span>
4. <span data-ttu-id="8e4b0-226">既存のコンテンツを次の内容に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-226">Replace the existing content with the following:</span></span> 

    [!code-cshtml[Main](working-with-files/samples/sample6.cshtml)]

    <span data-ttu-id="8e4b0-227">このページには、ユーザーがイメージファイルの名前を入力できるフォームが含まれています。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-227">This page contains a form where users can enter the name of an image file.</span></span> <span data-ttu-id="8e4b0-228">これらは、 *.jpg*ファイル名拡張子を入力しません。このようにファイル名を制限することで、ユーザーがサイト上の任意のファイルを削除できないようにすることができます。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-228">They don't enter the *.jpg* file-name extension; by restricting the file name like this, you help prevents users from deleting arbitrary files on your site.</span></span>

    <span data-ttu-id="8e4b0-229">このコードは、ユーザーが入力したファイル名を読み取り、完全なパスを構築します。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-229">The code reads the file name that the user has entered and then constructs a complete path.</span></span> <span data-ttu-id="8e4b0-230">パスを作成するために、コードは現在の web サイトのパス (`Server.MapPath` メソッドによって返される)、 *images*フォルダー名、ユーザーが指定した名前、および ".jpg" をリテラル文字列として使用します。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-230">To create the path, the code uses the current website path (as returned by the `Server.MapPath` method), the *images* folder name, the name that the user has provided, and ".jpg" as a literal string.</span></span>

    <span data-ttu-id="8e4b0-231">このファイルを削除するには、コードで `File.Delete` メソッドを呼び出し、先ほど作成した完全なパスを渡します。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-231">To delete the file, the code calls the `File.Delete` method, passing it the full path that you just constructed.</span></span> <span data-ttu-id="8e4b0-232">マークアップの最後に、ファイルが削除されたことを示す確認メッセージがコードによって表示されます。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-232">At the end of the markup, code displays a confirmation message that the file was deleted.</span></span>
5. <span data-ttu-id="8e4b0-233">ブラウザーでページを実行します。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-233">Run the page in a browser.</span></span> 

    ![[画像]](working-with-files/_static/image5.jpg)
6. <span data-ttu-id="8e4b0-235">削除するファイルの名前を入力し、 **[送信]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-235">Enter the name of the file to delete and then click **Submit**.</span></span> <span data-ttu-id="8e4b0-236">ファイルが削除されている場合は、ファイルの名前がページの下部に表示されます。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-236">If the file was deleted, the name of the file is displayed at the bottom of the page.</span></span>

<a id="Letting_Users_Upload_a_File"></a>
## <a name="letting-users-upload-a-file"></a><span data-ttu-id="8e4b0-237">ユーザーがファイルをアップロードできるようにする</span><span class="sxs-lookup"><span data-stu-id="8e4b0-237">Letting Users Upload a File</span></span>

<span data-ttu-id="8e4b0-238">`FileUpload` ヘルパーを使用すると、ユーザーは web サイトにファイルをアップロードできます。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-238">The `FileUpload` helper lets users upload files to your website.</span></span> <span data-ttu-id="8e4b0-239">次の手順は、ユーザーが1つのファイルをアップロードできるようにする方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-239">The procedure below shows you how to let users upload a single file.</span></span>

1. <span data-ttu-id="8e4b0-240">前に追加していない場合は、「 [ASP.NET Web ページサイトにヘルパーをインストール](https://go.microsoft.com/fwlink/?LinkId=252372)する」の説明に従って、ASP.NET Web ヘルパーライブラリを web サイトに追加します。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-240">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you didn't add it previously.</span></span>
2. <span data-ttu-id="8e4b0-241">[ *App\_Data* ] フォルダーで、新しいフォルダーを作成し、 *UploadedFiles*という名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-241">In the *App\_Data* folder, create a new a folder and name it *UploadedFiles*.</span></span>
3. <span data-ttu-id="8e4b0-242">ルートで、 *FileUpload*という名前の新しいファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-242">In the root, create a new file named *FileUpload.cshtml*.</span></span>
4. <span data-ttu-id="8e4b0-243">ページ内の既存のコンテンツを次の内容に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-243">Replace the existing content in the page with the following:</span></span> 

    [!code-cshtml[Main](working-with-files/samples/sample7.cshtml)]

    <span data-ttu-id="8e4b0-244">ページの本文部分では、`FileUpload` ヘルパーを使用して、よく知られているアップロードボックスとボタンを作成します。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-244">The body portion of the page uses the `FileUpload` helper to create the upload box and buttons that you're probably familiar with:</span></span>

    ![[画像]](working-with-files/_static/image6.jpg)

    <span data-ttu-id="8e4b0-246">`FileUpload` helper に設定したプロパティでは、ファイルの1つのボックスをアップロードするように指定し、[送信] ボタンで**アップロード**を読み取ります。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-246">The properties that you set for the `FileUpload` helper specify that you want a single box for the file to upload and that you want the submit button to read **Upload**.</span></span> <span data-ttu-id="8e4b0-247">(この記事の後半で、さらに多くのボックスを追加します)。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-247">(You'll add more boxes later in the article.)</span></span>

    <span data-ttu-id="8e4b0-248">ユーザーが **[アップロード]** をクリックすると、ページ上部のコードによってファイルが取得され、保存されます。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-248">When the user clicks **Upload**, the code at the top of the page gets the file and saves it.</span></span> <span data-ttu-id="8e4b0-249">フォームフィールドから値を取得するために通常使用する `Request` オブジェクトには、アップロードされたファイル (またはファイル) を格納する `Files` 配列もあります。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-249">The `Request` object that you normally use to get values from form fields also has a `Files` array that contains the file (or files) that have been uploaded.</span></span> <span data-ttu-id="8e4b0-250">配列&#8212;内の特定の位置から個々のファイルを取得することができます。たとえば、最初にアップロードされたファイルを取得するために、`Request.Files[0]`を取得し、2番目のファイルを取得する、`Request.Files[1]`を取得するなどの方法があります。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-250">You can get individual files out of specific positions in the array &#8212; for example, to get the first uploaded file, you get `Request.Files[0]`, to get the second file, you get `Request.Files[1]`, and so on.</span></span> <span data-ttu-id="8e4b0-251">(プログラミングでは、通常、カウントは0から始まります)。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-251">(Remember that in programming, counting usually starts at zero.)</span></span>

    <span data-ttu-id="8e4b0-252">アップロードしたファイルをフェッチする場合は、そのファイルを操作できるように変数 (ここでは `uploadedFile`) に配置します。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-252">When you fetch an uploaded file, you put it in a variable (here, `uploadedFile`) so that you can manipulate it.</span></span> <span data-ttu-id="8e4b0-253">アップロードされたファイルの名前を確認するには、その `FileName` プロパティを取得します。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-253">To determine the name of the uploaded file, you just get its `FileName` property.</span></span> <span data-ttu-id="8e4b0-254">ただし、ユーザーがファイルをアップロードすると、`FileName` には、パス全体を含むユーザーの元の名前が含まれます。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-254">However, when the user uploads a file, `FileName` contains the user's original name, which includes the entire path.</span></span> <span data-ttu-id="8e4b0-255">次のようになります。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-255">It might look like this:</span></span>

    <span data-ttu-id="8e4b0-256">*C:\Users\Public\Sample.txt*</span><span class="sxs-lookup"><span data-stu-id="8e4b0-256">*C:\Users\Public\Sample.txt*</span></span>

    <span data-ttu-id="8e4b0-257">ただし、これはユーザーのコンピューター上のパスであり、サーバーではないため、すべてのパス情報を必要としません。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-257">You don't want all that path information, though, because that's the path on the user's computer, not for your server.</span></span> <span data-ttu-id="8e4b0-258">実際のファイル名を必要とするだけです (*サンプル .txt*)。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-258">You just want the actual file name (*Sample.txt*).</span></span> <span data-ttu-id="8e4b0-259">次のように `Path.GetFileName` メソッドを使用して、パスからファイルのみを取り除くことができます。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-259">You can strip out just the file from a path by using the `Path.GetFileName` method, like this:</span></span>

    [!code-csharp[Main](working-with-files/samples/sample8.cs)]

    <span data-ttu-id="8e4b0-260">`Path` オブジェクトは、このような多数のメソッドを備えたユーティリティで、パスの削除やパスの結合などに使用できます。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-260">The `Path` object is a utility that has a number of methods like this that you can use to strip paths, combine paths, and so on.</span></span>

    <span data-ttu-id="8e4b0-261">アップロードしたファイルの名前を入力したら、アップロードしたファイルを web サイトに保存する場所の新しいパスを作成できます。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-261">Once you've gotten the name of the uploaded file, you can build a new path for where you want to store the uploaded file in your website.</span></span> <span data-ttu-id="8e4b0-262">この場合は、`Server.MapPath`、フォルダー名 (*App\_Data/UploadedFiles*)、および新しく削除されたファイル名を組み合わせて新しいパスを作成します。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-262">In this case, you combine `Server.MapPath`, the folder names (*App\_Data/UploadedFiles*), and the newly stripped file name to create a new path.</span></span> <span data-ttu-id="8e4b0-263">アップロードしたファイルの `SaveAs` メソッドを呼び出して、実際にファイルを保存することができます。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-263">You can then call the uploaded file's `SaveAs` method to actually save the file.</span></span>
5. <span data-ttu-id="8e4b0-264">ブラウザーでページを実行します。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-264">Run the page in a browser.</span></span> 

    ![[画像]](working-with-files/_static/image7.jpg)
6. <span data-ttu-id="8e4b0-266">**[参照]** をクリックし、アップロードするファイルを選択します。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-266">Click **Browse** and then select a file to upload.</span></span> 

    ![[画像]](working-with-files/_static/image8.jpg)

    <span data-ttu-id="8e4b0-268">**[参照]** ボタンの横にあるテキストボックスに、パスとファイルの場所が表示されます。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-268">The text box next to the **Browse** button will contain the path and file location.</span></span>

    ![[画像]](working-with-files/_static/image9.jpg)
7. <span data-ttu-id="8e4b0-270">**[アップロード]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-270">Click **Upload**.</span></span>
8. <span data-ttu-id="8e4b0-271">Web サイトで、プロジェクトフォルダーを右クリックし、[最新の状態に**更新**] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-271">In the website, right-click the project folder and then click **Refresh**.</span></span>
9. <span data-ttu-id="8e4b0-272">*UploadedFiles*フォルダーを開きます。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-272">Open the *UploadedFiles* folder.</span></span> <span data-ttu-id="8e4b0-273">アップロードしたファイルは、フォルダーにあります。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-273">The file that you uploaded is in the folder.</span></span> 

    ![[画像]](working-with-files/_static/image10.jpg)

<a id="Letting_Users_Upload_Multiple_Files"></a>
## <a name="letting-users-upload-multiple-files"></a><span data-ttu-id="8e4b0-275">ユーザーが複数のファイルをアップロードできるようにする</span><span class="sxs-lookup"><span data-stu-id="8e4b0-275">Letting Users Upload Multiple Files</span></span>

<span data-ttu-id="8e4b0-276">前の例では、ユーザーが1つのファイルをアップロードできるようにします。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-276">In the previous example, you let users upload one file.</span></span> <span data-ttu-id="8e4b0-277">ただし、`FileUpload` ヘルパーを使用して、一度に複数のファイルをアップロードすることができます。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-277">But you can use the `FileUpload` helper to upload more than one file at a time.</span></span> <span data-ttu-id="8e4b0-278">これは、写真のアップロードなどのシナリオで便利です。一度に1つのファイルをアップロードすることは面倒です。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-278">This is handy for scenarios like uploading photos, where uploading one file at a time is tedious.</span></span> <span data-ttu-id="8e4b0-279">( [ASP.NET Web ページサイトの画像を使用した](https://go.microsoft.com/fwlink/?LinkId=202897)写真のアップロードについては、「」を参照してください)。この例では、ユーザーが同時にアップロードできる方法を示していますが、同じ手法を使用して同時にアップロードすることもできます。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-279">(You can read about uploading photos in [Working with Images in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=202897).) This example shows how to let users upload two at a time, although you can use the same technique to upload more than that.</span></span>

1. <span data-ttu-id="8e4b0-280">「 [ASP.NET Web ページサイトにヘルパーをインストール](https://go.microsoft.com/fwlink/?LinkId=252372)する」の説明に従って、ASP.NET Web ヘルパーライブラリを web サイトに追加します (まだインストールしていない場合)。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-280">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already.</span></span>
2. <span data-ttu-id="8e4b0-281">*Fileuploadmultiple. cshtml*という名前の新しいページを作成します。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-281">Create a new page named *FileUploadMultiple.cshtml*.</span></span>
3. <span data-ttu-id="8e4b0-282">ページ内の既存のコンテンツを次の内容に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-282">Replace the existing content in the page with the following:</span></span>  

    [!code-cshtml[Main](working-with-files/samples/sample9.cshtml)]

    <span data-ttu-id="8e4b0-283">この例では、ページの本文の `FileUpload` ヘルパーは、ユーザーが既定で2つのファイルをアップロードできるように構成されています。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-283">In this example, the `FileUpload` helper in the body of the page is configured to let users upload two files by default.</span></span> <span data-ttu-id="8e4b0-284">`allowMoreFilesToBeAdded` が `true`に設定されているため、ヘルパーは、ユーザーが追加のアップロードボックスを追加できるリンクを表示します。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-284">Because `allowMoreFilesToBeAdded` is set to `true`, the helper renders a link that lets user add more upload boxes:</span></span>

    ![[画像]](working-with-files/_static/image11.jpg)

    <span data-ttu-id="8e4b0-286">ユーザーがアップロードしたファイルを処理するために、前の例&#8212;で使用したのと同じ基本的な方法でコードを使用し、`Request.Files` からファイルを取得して保存します。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-286">To process the files that the user uploads, the code uses the same basic technique that you used in the previous example &#8212; get a file from `Request.Files` and then save it.</span></span> <span data-ttu-id="8e4b0-287">(正しいファイル名とパスを取得するために必要なさまざまな処理が含まれています)。今回のイノベーションは、ユーザーが複数のファイルをアップロードしていて、あまり多くのファイルを持っていない可能性があるということです。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-287">(Including the various things you need to do to get the right file name and path.) The innovation this time is that the user might be uploading multiple files and you don't know many.</span></span> <span data-ttu-id="8e4b0-288">確認するには、`Request.Files.Count`を取得します。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-288">To find out, you can get `Request.Files.Count`.</span></span>

    <span data-ttu-id="8e4b0-289">この数を指定すると、`Request.Files`をループ処理し、各ファイルを順番にフェッチして保存できます。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-289">With this number in hand, you can loop through `Request.Files`, fetch each file in turn, and save it.</span></span> <span data-ttu-id="8e4b0-290">コレクションを通じて既知の回数をループする場合は、次のように `for` ループを使用できます。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-290">When you want to loop a known number of times through a collection, you can use a `for` loop, like this:</span></span>

    [!code-csharp[Main](working-with-files/samples/sample10.cs)]

    <span data-ttu-id="8e4b0-291">変数 `i` は、ゼロから設定した上限に達するまでの一時的なカウンターにすぎません。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-291">The variable `i` is just a temporary counter that will go from zero to whatever upper limit you set.</span></span> <span data-ttu-id="8e4b0-292">この場合、上限はファイル数です。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-292">In this case, the upper limit is the number of files.</span></span> <span data-ttu-id="8e4b0-293">ただし、カウンターは0から開始されるため、ASP.NET のシナリオをカウントするのが一般的です。そのため、上限は実際にはファイルの数より1小さくなります。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-293">But because the counter starts at zero, as is typical for counting scenarios in ASP.NET, the upper limit is actually one less than the file count.</span></span> <span data-ttu-id="8e4b0-294">(3 つのファイルがアップロードされた場合、カウントは0から2になります)。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-294">(If three files are uploaded, the count is zero to 2.)</span></span>

    <span data-ttu-id="8e4b0-295">`uploadedCount` 変数は、正常にアップロードされて保存されたすべてのファイルの総数を示します。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-295">The `uploadedCount` variable totals all the files that are successfully uploaded and saved.</span></span> <span data-ttu-id="8e4b0-296">このコードは、予期されたファイルをアップロードできない可能性を考慮しています。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-296">This code accounts for the possibility that an expected file may not be able to be uploaded.</span></span>
4. <span data-ttu-id="8e4b0-297">ブラウザーでページを実行します。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-297">Run the page in a browser.</span></span> <span data-ttu-id="8e4b0-298">ブラウザーには、ページとその2つのアップロードボックスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-298">The browser displays the page and its two upload boxes.</span></span>
5. <span data-ttu-id="8e4b0-299">アップロードする2つのファイルを選択します。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-299">Select two files to upload.</span></span>
6. <span data-ttu-id="8e4b0-300">**[別のファイルを追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-300">Click **Add another file**.</span></span> <span data-ttu-id="8e4b0-301">ページに新しいアップロードボックスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-301">The page displays a new upload box.</span></span> 

    ![[画像]](working-with-files/_static/image12.jpg)
7. <span data-ttu-id="8e4b0-303">**[アップロード]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-303">Click **Upload**.</span></span>
8. <span data-ttu-id="8e4b0-304">Web サイトで、プロジェクトフォルダーを右クリックし、[最新の状態に**更新**] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-304">In the website, right-click the project folder and then click **Refresh**.</span></span>
9. <span data-ttu-id="8e4b0-305">*UploadedFiles*フォルダーを開き、正常にアップロードされたファイルを確認します。</span><span class="sxs-lookup"><span data-stu-id="8e4b0-305">Open the *UploadedFiles* folder to see the successfully uploaded files.</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="8e4b0-306">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="8e4b0-306">Additional Resources</span></span>

[<span data-ttu-id="8e4b0-307">ASP.NET Web ページサイトのイメージの操作</span><span class="sxs-lookup"><span data-stu-id="8e4b0-307">Working with Images in an ASP.NET Web Pages Site</span></span>](https://go.microsoft.com/fwlink/?LinkId=202897)

[<span data-ttu-id="8e4b0-308">CSV ファイルへのエクスポート</span><span class="sxs-lookup"><span data-stu-id="8e4b0-308">Exporting to a CSV File</span></span>](https://msdn.microsoft.com/library/ms155919.aspx)
