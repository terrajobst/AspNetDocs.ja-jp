---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-6
title: JavaScript クライアントを作成する |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 20360326-b123-4b1e-abae-1d350edf4ce4
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-6
msc.type: authoredcontent
ms.openlocfilehash: 74f2cc4e5e401d690042b05b028dfc0c46ae282a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78504724"
---
# <a name="create-the-javascript-client"></a><span data-ttu-id="bee05-102">JavaScript クライアントの作成</span><span class="sxs-lookup"><span data-stu-id="bee05-102">Create the JavaScript Client</span></span>

<span data-ttu-id="bee05-103">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="bee05-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="bee05-104">完成したプロジェクトのダウンロード</span><span class="sxs-lookup"><span data-stu-id="bee05-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="bee05-105">このセクションでは、HTML、JavaScript、および[ノックアウト](http://knockoutjs.com/)ライブラリを使用して、アプリケーション用のクライアントを作成します。</span><span class="sxs-lookup"><span data-stu-id="bee05-105">In this section, you will create the client for the application, using HTML, JavaScript, and the [Knockout.js](http://knockoutjs.com/) library.</span></span> <span data-ttu-id="bee05-106">クライアントアプリを段階的に構築します。</span><span class="sxs-lookup"><span data-stu-id="bee05-106">We'll build the client app in stages:</span></span>

- <span data-ttu-id="bee05-107">書籍の一覧を表示します。</span><span class="sxs-lookup"><span data-stu-id="bee05-107">Showing a list of books.</span></span>
- <span data-ttu-id="bee05-108">書籍の詳細を表示しています。</span><span class="sxs-lookup"><span data-stu-id="bee05-108">Showing a book detail.</span></span>
- <span data-ttu-id="bee05-109">新しい書籍を追加します。</span><span class="sxs-lookup"><span data-stu-id="bee05-109">Adding a new book.</span></span>

<span data-ttu-id="bee05-110">ノックアウトライブラリは、モデルビュービューモデル (MVVM) パターンを使用します。</span><span class="sxs-lookup"><span data-stu-id="bee05-110">The Knockout library uses the Model-View-ViewModel (MVVM) pattern:</span></span>

- <span data-ttu-id="bee05-111">この**モデル**は、ビジネスドメイン内のデータ (ここでは books と authors) のサーバー側表現です。</span><span class="sxs-lookup"><span data-stu-id="bee05-111">The **model** is the server-side representation of the data in the business domain (in our case, books and authors).</span></span>
- <span data-ttu-id="bee05-112">**ビュー**はプレゼンテーション層 (HTML) です。</span><span class="sxs-lookup"><span data-stu-id="bee05-112">The **view** is the presentation layer (HTML).</span></span>
- <span data-ttu-id="bee05-113">**ビューモデル**は、モデルを保持する JavaScript オブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="bee05-113">The **view model** is a JavaScript object that holds the models.</span></span> <span data-ttu-id="bee05-114">ビューモデルは、UI のコード抽象化です。</span><span class="sxs-lookup"><span data-stu-id="bee05-114">The view model is a code abstraction of the UI.</span></span> <span data-ttu-id="bee05-115">HTML 表現に関する情報はありません。</span><span class="sxs-lookup"><span data-stu-id="bee05-115">It has no knowledge of the HTML representation.</span></span> <span data-ttu-id="bee05-116">代わりに、書籍&quot;の一覧 &quot;など、ビューの抽象的な機能を表します。</span><span class="sxs-lookup"><span data-stu-id="bee05-116">Instead, it represents abstract features of the view, such as &quot;a list of books&quot;.</span></span>

<span data-ttu-id="bee05-117">ビューは、ビューモデルにデータバインドされています。</span><span class="sxs-lookup"><span data-stu-id="bee05-117">The view is data-bound to the view model.</span></span> <span data-ttu-id="bee05-118">ビューモデルの更新は、自動的にビューに反映されます。</span><span class="sxs-lookup"><span data-stu-id="bee05-118">Updates to the view model are automatically reflected in the view.</span></span> <span data-ttu-id="bee05-119">ビューモデルでは、ボタンのクリックなど、ビューからイベントを取得することもできます。</span><span class="sxs-lookup"><span data-stu-id="bee05-119">The view model also gets events from the view, such as button clicks.</span></span>

![](part-6/_static/image1.png)

<span data-ttu-id="bee05-120">この方法を使用すると、コードを書き直さずにバインドを変更できるため、アプリのレイアウトと UI を簡単に変更できます。</span><span class="sxs-lookup"><span data-stu-id="bee05-120">This approach makes it easy to change the layout and UI of your app, because you can change the bindings, without rewriting any code.</span></span> <span data-ttu-id="bee05-121">たとえば、項目の一覧を `<ul>`として表示し、後でテーブルに変更することができます。</span><span class="sxs-lookup"><span data-stu-id="bee05-121">For example, you might show a list of items as a `<ul>`, then change it later to a table.</span></span>

## <a name="add-the-knockout-library"></a><span data-ttu-id="bee05-122">ノックアウトライブラリを追加する</span><span class="sxs-lookup"><span data-stu-id="bee05-122">Add the Knockout Library</span></span>

<span data-ttu-id="bee05-123">Visual Studio で、 **[ツール]** メニューの **[NuGet パッケージマネージャー]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="bee05-123">In Visual Studio, from the **Tools** menu, select **NuGet Package Manager**.</span></span> <span data-ttu-id="bee05-124">次に、 **[パッケージ マネージャー コンソール]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="bee05-124">Then select **Package Manager Console**.</span></span> <span data-ttu-id="bee05-125">[パッケージ マネージャー コンソール] ウィンドウで、次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="bee05-125">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](part-6/samples/sample1.cmd)]

<span data-ttu-id="bee05-126">このコマンドは、[スクリプト] フォルダーにノックアウトファイルを追加します。</span><span class="sxs-lookup"><span data-stu-id="bee05-126">This command adds the Knockout files to the Scripts folder.</span></span>

## <a name="create-the-view-model"></a><span data-ttu-id="bee05-127">ビューモデルを作成する</span><span class="sxs-lookup"><span data-stu-id="bee05-127">Create the View Model</span></span>

<span data-ttu-id="bee05-128">App.config という名前の JavaScript ファイルを Scripts フォルダーに追加します。</span><span class="sxs-lookup"><span data-stu-id="bee05-128">Add a JavaScript file named app.js to the Scripts folder.</span></span> <span data-ttu-id="bee05-129">(ソリューションエクスプローラーで、Scripts フォルダーを右クリックし、 **[追加]** 、 **[JavaScript ファイル]** の順に選択します)。次のコードを貼り付けます。</span><span class="sxs-lookup"><span data-stu-id="bee05-129">(In Solution Explorer, right-click the Scripts folder, select **Add**, then select **JavaScript File**.) Paste in the following code:</span></span>

[!code-javascript[Main](part-6/samples/sample2.js)]

<span data-ttu-id="bee05-130">ノックアウトでは、`observable` クラスによってデータバインディングが有効になります。</span><span class="sxs-lookup"><span data-stu-id="bee05-130">In Knockout, the `observable` class enables data-binding.</span></span> <span data-ttu-id="bee05-131">観測可能な変更の内容が監視対象となると、データにバインドされたすべてのコントロールに対して、自身の更新が可能になるように通知されます。</span><span class="sxs-lookup"><span data-stu-id="bee05-131">When the contents of an observable change, the observable notifies all of the data-bound controls, so they can update themselves.</span></span> <span data-ttu-id="bee05-132">(`observableArray` クラスは、*観測*可能な配列バージョンです)。まず、ビューモデルには2つの observable があります。</span><span class="sxs-lookup"><span data-stu-id="bee05-132">(The `observableArray` class is the array version of *observable*.) To start with, our view model has two observables:</span></span>

- <span data-ttu-id="bee05-133">`books` は、本の一覧を保持します。</span><span class="sxs-lookup"><span data-stu-id="bee05-133">`books` holds the list of books.</span></span>
- <span data-ttu-id="bee05-134">AJAX 呼び出しが失敗した場合、`error` にはエラーメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="bee05-134">`error` contains an error message if an AJAX call fails.</span></span>

<span data-ttu-id="bee05-135">`getAllBooks` メソッドは、AJAX 呼び出しを行って書籍の一覧を取得します。</span><span class="sxs-lookup"><span data-stu-id="bee05-135">The `getAllBooks` method makes an AJAX call to get the list of books.</span></span> <span data-ttu-id="bee05-136">次に、結果を `books` 配列にプッシュします。</span><span class="sxs-lookup"><span data-stu-id="bee05-136">Then it pushes the result onto the `books` array.</span></span>

<span data-ttu-id="bee05-137">`ko.applyBindings` メソッドは、ノックアウトライブラリの一部です。</span><span class="sxs-lookup"><span data-stu-id="bee05-137">The `ko.applyBindings` method is part of the Knockout library.</span></span> <span data-ttu-id="bee05-138">ビューモデルをパラメーターとして受け取り、データバインディングを設定します。</span><span class="sxs-lookup"><span data-stu-id="bee05-138">It takes the view model as a parameter and sets up the data binding.</span></span>

## <a name="add-a-script-bundle"></a><span data-ttu-id="bee05-139">スクリプトバンドルを追加する</span><span class="sxs-lookup"><span data-stu-id="bee05-139">Add a Script Bundle</span></span>

<span data-ttu-id="bee05-140">バンドルは ASP.NET 4.5 の機能であり、複数のファイルを簡単に1つのファイルに結合したりバンドルしたりすることができます。</span><span class="sxs-lookup"><span data-stu-id="bee05-140">Bundling is a feature in ASP.NET 4.5 that makes it easy to combine or bundle multiple files into a single file.</span></span> <span data-ttu-id="bee05-141">バンドルを使用すると、サーバーへの要求の数が減り、ページの読み込み時間が短縮されます。</span><span class="sxs-lookup"><span data-stu-id="bee05-141">Bundling reduces the number of requests to the server, which can improve page load time.</span></span>

<span data-ttu-id="bee05-142">File App\_Start/BundleConfig を開きます。</span><span class="sxs-lookup"><span data-stu-id="bee05-142">Open the file App\_Start/BundleConfig.cs.</span></span> <span data-ttu-id="bee05-143">RegisterBundles メソッドに次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="bee05-143">Add the following code to the RegisterBundles method.</span></span>

[!code-csharp[Main](part-6/samples/sample3.cs)]

> [!div class="step-by-step"]
> <span data-ttu-id="bee05-144">[前へ](part-5.md)
> [次へ](part-7.md)</span><span class="sxs-lookup"><span data-stu-id="bee05-144">[Previous](part-5.md)
[Next](part-7.md)</span></span>
