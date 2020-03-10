---
uid: single-page-application/overview/templates/emberjs-template
title: EmberJS template |Microsoft Docs
author: xqiu
description: EmberJS テンプレート
ms.author: riande
ms.date: 01/30/2013
ms.assetid: 04d5f142-5f62-494a-b5ea-4f3d068d34cb
msc.legacyurl: /single-page-application/overview/templates/emberjs-template
msc.type: authoredcontent
ms.openlocfilehash: 1aefa46dd0841b1b06675409cc8a09f9a218d7ac
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467158"
---
# <a name="emberjs-template"></a><span data-ttu-id="dff4f-103">EmberJS テンプレート</span><span class="sxs-lookup"><span data-stu-id="dff4f-103">EmberJS template</span></span>

<span data-ttu-id="dff4f-104">[Xinyang Qiu](https://github.com/xqiu)</span><span class="sxs-lookup"><span data-stu-id="dff4f-104">by [Xinyang Qiu](https://github.com/xqiu)</span></span>

> <span data-ttu-id="dff4f-105">EmberJS MVC テンプレートは、Nathan、Thiago Santos、および Xinyang Qiu によって作成されています。</span><span class="sxs-lookup"><span data-stu-id="dff4f-105">The EmberJS MVC Template is written by Nathan Totten, Thiago Santos, and Xinyang Qiu.</span></span>
> 
> [<span data-ttu-id="dff4f-106">EmberJS MVC テンプレートをダウンロードする</span><span class="sxs-lookup"><span data-stu-id="dff4f-106">Download the EmberJS MVC Template</span></span>](https://go.microsoft.com/fwlink/?LinkId=282647)

<span data-ttu-id="dff4f-107">EmberJS SPA テンプレートは、EmberJS を使用して、対話型のクライアント側 web アプリの構築をすぐに開始できるように設計されています。</span><span class="sxs-lookup"><span data-stu-id="dff4f-107">The EmberJS SPA template is designed to get you started quickly building interactive client-side web apps using EmberJS.</span></span>

<span data-ttu-id="dff4f-108">"シングルページアプリケーション" (SPA) は、1つの HTML ページを読み込み、新しいページを読み込むのではなく、ページを動的に更新する web アプリケーションの一般的な用語です。</span><span class="sxs-lookup"><span data-stu-id="dff4f-108">"Single-page application" (SPA) is the general term for a web application that loads a single HTML page and then updates the page dynamically, instead of loading new pages.</span></span> <span data-ttu-id="dff4f-109">最初のページの読み込み後、SPA は AJAX 要求によってサーバーと通信します。</span><span class="sxs-lookup"><span data-stu-id="dff4f-109">After the initial page load, the SPA talks with the server through AJAX requests.</span></span>

![](emberjs-template/_static/image1.png)

<span data-ttu-id="dff4f-110">AJAX はまったく新しいものではありませんが、今日では、大規模な高度な SPA アプリケーションを簡単に構築して維持できる JavaScript フレームワークが用意されています。</span><span class="sxs-lookup"><span data-stu-id="dff4f-110">AJAX is nothing new, but today there are JavaScript frameworks that make it easier to build and maintain a large sophisticated SPA application.</span></span> <span data-ttu-id="dff4f-111">また、HTML 5 と CSS3 は、豊富な Ui の作成を容易にします。</span><span class="sxs-lookup"><span data-stu-id="dff4f-111">Also, HTML 5 and CSS3 are making it easier to create rich UIs.</span></span>

<span data-ttu-id="dff4f-112">EmberJS SPA テンプレートでは、 [Ember.js](http://emberjs.com/) JavaScript ライブラリを使用して、AJAX 要求からのページ更新を処理します。</span><span class="sxs-lookup"><span data-stu-id="dff4f-112">The EmberJS SPA Template uses the [Ember](http://emberjs.com/) JavaScript library to handle page updates from AJAX requests.</span></span> <span data-ttu-id="dff4f-113">Ember.js は、データバインディングを使用して、ページを最新のデータと同期します。</span><span class="sxs-lookup"><span data-stu-id="dff4f-113">Ember.js uses data binding to synchronize the page with the latest data.</span></span> <span data-ttu-id="dff4f-114">このようにして、JSON データを処理するコードを記述して DOM を更新する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="dff4f-114">That way, you don't have to write any of the code that walks through the JSON data and updates the DOM.</span></span> <span data-ttu-id="dff4f-115">代わりに、データの表示方法を Ember.js に指示する宣言型の属性を HTML に配置します。</span><span class="sxs-lookup"><span data-stu-id="dff4f-115">Instead, you put declarative attributes in the HTML that tell Ember.js how to present the data.</span></span>

<span data-ttu-id="dff4f-116">サーバー側では、EmberJS テンプレートは[KNOCKOUTJS SPA テンプレート](../introduction/knockoutjs-template.md)とほぼ同じです。</span><span class="sxs-lookup"><span data-stu-id="dff4f-116">On the server side, the EmberJS template is almost identical to the [KnockoutJS SPA template](../introduction/knockoutjs-template.md).</span></span> <span data-ttu-id="dff4f-117">ASP.NET MVC を使用して HTML ドキュメントを提供し、ASP.NET Web API クライアントからの AJAX 要求を処理します。</span><span class="sxs-lookup"><span data-stu-id="dff4f-117">It uses ASP.NET MVC to serve HTML documents, and ASP.NET Web API to handle AJAX requests from the client.</span></span> <span data-ttu-id="dff4f-118">テンプレートのこれらの側面の詳細については、 [KnockoutJS テンプレート](../introduction/knockoutjs-template.md)のドキュメントを参照してください。</span><span class="sxs-lookup"><span data-stu-id="dff4f-118">For more information about those aspects of the template, refer to the [KnockoutJS template](../introduction/knockoutjs-template.md) documentation.</span></span> <span data-ttu-id="dff4f-119">このトピックでは、ノックアウトテンプレートと EmberJS テンプレートの違いについて説明します。</span><span class="sxs-lookup"><span data-stu-id="dff4f-119">This topic focuses on the differences between the Knockout template and the EmberJS template.</span></span>

## <a name="create-an-emberjs-spa-template-project"></a><span data-ttu-id="dff4f-120">EmberJS SPA テンプレートプロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="dff4f-120">Create an EmberJS SPA Template Project</span></span>

<span data-ttu-id="dff4f-121">上の [ダウンロード] ボタンをクリックして、テンプレートをダウンロードしてインストールします。</span><span class="sxs-lookup"><span data-stu-id="dff4f-121">Download and install the template by clicking the Download button above.</span></span> <span data-ttu-id="dff4f-122">場合によっては、Visual Studio を再起動する必要があります。</span><span class="sxs-lookup"><span data-stu-id="dff4f-122">You might need to restart Visual Studio.</span></span>

<span data-ttu-id="dff4f-123">**[テンプレート]** ペインで、 **[インストールされたテンプレート]** を選択し、  **C#ビジュアル**ノードを展開します。</span><span class="sxs-lookup"><span data-stu-id="dff4f-123">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="dff4f-124">**[ビジュアルC# ]** で **[Web]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="dff4f-124">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="dff4f-125">プロジェクトテンプレートの一覧で、 **[ASP.NET MVC 4 Web アプリケーション]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="dff4f-125">In the list of project templates, select **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="dff4f-126">プロジェクト名を指定して、 **[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="dff4f-126">Name the project and click **OK**.</span></span>

![](emberjs-template/_static/image2.png)

<span data-ttu-id="dff4f-127">**新しいプロジェクト**ウィザードで、 **[ember.js SPA プロジェクト]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="dff4f-127">In the **New Project** wizard, select **Ember.js SPA Project**.</span></span>

![](emberjs-template/_static/image4.png)

## <a name="emberjs-spa-template-overview"></a><span data-ttu-id="dff4f-128">EmberJS SPA テンプレートの概要</span><span class="sxs-lookup"><span data-stu-id="dff4f-128">EmberJS SPA Template Overview</span></span>

<span data-ttu-id="dff4f-129">EmberJS テンプレートでは、jQuery、Ember.js、ハンドルの組み合わせを使用して、スムーズで対話型の UI を作成します。</span><span class="sxs-lookup"><span data-stu-id="dff4f-129">The EmberJS template uses a combination of jQuery, Ember.js, Handlebars.js to create a smooth, interactive UI.</span></span>

<span data-ttu-id="dff4f-130">Ember.js は、クライアント側の MVC パターンを使用する JavaScript ライブラリです。</span><span class="sxs-lookup"><span data-stu-id="dff4f-130">Ember.js is a JavaScript library that uses a client-side MVC pattern.</span></span>

- <span data-ttu-id="dff4f-131">ハンドルテンプレート言語で記述された*テンプレート*は、アプリケーションのユーザーインターフェイスについて説明します。</span><span class="sxs-lookup"><span data-stu-id="dff4f-131">A *template*, written in the Handlebars templating language, describes the application user interface.</span></span> <span data-ttu-id="dff4f-132">リリースモードでは、[ハンドルコンパイラ](https://github.com/Myslik/csharp-ember-handlebars)を使用してハンドルテンプレートをバンドルし、コンパイルします。</span><span class="sxs-lookup"><span data-stu-id="dff4f-132">In release mode, the [Handlebars compiler](https://github.com/Myslik/csharp-ember-handlebars) is used to bundle and compile the handlebars template.</span></span>
- <span data-ttu-id="dff4f-133">*モデル*には、サーバーから取得したアプリケーションデータ (todo リストと todo 項目) が格納されます。</span><span class="sxs-lookup"><span data-stu-id="dff4f-133">A *model* stores the application data that it gets from the server (ToDo lists and ToDo items).</span></span>
- <span data-ttu-id="dff4f-134">*コントローラー*は、アプリケーションの状態を格納します。</span><span class="sxs-lookup"><span data-stu-id="dff4f-134">A *controller* stores application state.</span></span> <span data-ttu-id="dff4f-135">多くの場合、コントローラーは対応するテンプレートにモデルデータを提示します。</span><span class="sxs-lookup"><span data-stu-id="dff4f-135">Controllers often present model data to the corresponding templates.</span></span>
- <span data-ttu-id="dff4f-136">*ビュー*は、プリミティブイベントをアプリケーションから変換し、コントローラーに渡します。</span><span class="sxs-lookup"><span data-stu-id="dff4f-136">A *view* translates primitive events from the application and passes these to the controller.</span></span>
- <span data-ttu-id="dff4f-137">*ルーター*は、url とテンプレートの同期を維持しながら、アプリケーションの状態を管理します。</span><span class="sxs-lookup"><span data-stu-id="dff4f-137">A *router* manages application state, keeping URLs and templates in sync.</span></span>

<span data-ttu-id="dff4f-138">また、Ember.js Data library を使用して、(RESTful API を使用してサーバーから取得した) JSON オブジェクトとクライアントモデルを同期できます。</span><span class="sxs-lookup"><span data-stu-id="dff4f-138">In addition, the Ember Data library can be used to synchronize JSON objects (obtained from the server through a RESTful API) and the client models.</span></span>

<span data-ttu-id="dff4f-139">EmberJS SPA テンプレートでは、スクリプトが8つのレイヤーに編成されます。</span><span class="sxs-lookup"><span data-stu-id="dff4f-139">The EmberJS SPA template organizes the scripts into eight layers:</span></span>

- <span data-ttu-id="dff4f-140">webapi\_webapi\_serializer: Ember.js Data library を拡張して ASP.NET Web API を操作します。</span><span class="sxs-lookup"><span data-stu-id="dff4f-140">webapi\_adapter.js, webapi\_serializer.js: Extends the Ember Data library to work with ASP.NET Web API.</span></span>
- <span data-ttu-id="dff4f-141">Scripts/Ember.js: 新しいハンドルヘルパーを定義します。</span><span class="sxs-lookup"><span data-stu-id="dff4f-141">Scripts/helpers.js: Defines new Ember Handlebars helpers.</span></span>
- <span data-ttu-id="dff4f-142">Scripts/app.config: アプリを作成し、アダプターとシリアライザーを構成します。</span><span class="sxs-lookup"><span data-stu-id="dff4f-142">Scripts/app.js: Creates the app and configures the adapter and serializer.</span></span>
- <span data-ttu-id="dff4f-143">Scripts/app/model/\*.js: モデルを定義します。</span><span class="sxs-lookup"><span data-stu-id="dff4f-143">Scripts/app/models/\*.js: Defines the models.</span></span>
- <span data-ttu-id="dff4f-144">Scripts/app/views/\*.js: ビューを定義します。</span><span class="sxs-lookup"><span data-stu-id="dff4f-144">Scripts/app/views/\*.js: Defines the views.</span></span>
- <span data-ttu-id="dff4f-145">Scripts/app/controllers/\*.js: コントローラーを定義します。</span><span class="sxs-lookup"><span data-stu-id="dff4f-145">Scripts/app/controllers/\*.js: Defines the controllers.</span></span>
- <span data-ttu-id="dff4f-146">Scripts/app/route, Scripts/app/router js: ルートを定義します。</span><span class="sxs-lookup"><span data-stu-id="dff4f-146">Scripts/app/routes, Scripts/app/router.js: Defines the routes.</span></span>
- <span data-ttu-id="dff4f-147">Templates/\*: ハンドルテンプレートを定義します。</span><span class="sxs-lookup"><span data-stu-id="dff4f-147">Templates/\*.hbs: Defines the handlebars templates.</span></span>

<span data-ttu-id="dff4f-148">これらのスクリプトのいくつかをさらに詳しく見てみましょう。</span><span class="sxs-lookup"><span data-stu-id="dff4f-148">Let's look at some of these scripts in more detail.</span></span>

## <a name="models"></a><span data-ttu-id="dff4f-149">モデル</span><span class="sxs-lookup"><span data-stu-id="dff4f-149">Models</span></span>

<span data-ttu-id="dff4f-150">モデルは、[スクリプト/アプリ/モデル] フォルダーで定義されています。</span><span class="sxs-lookup"><span data-stu-id="dff4f-150">The models are defined in the Scripts/app/models folder.</span></span> <span data-ttu-id="dff4f-151">TodoItem と todoList という2つのモデルファイルがあります。</span><span class="sxs-lookup"><span data-stu-id="dff4f-151">There are two model files: todoItem.js and todoList.js.</span></span>

<span data-ttu-id="dff4f-152">**todo。モデル**は、to do リストのクライアント側 (ブラウザー) モデルを定義します。</span><span class="sxs-lookup"><span data-stu-id="dff4f-152">**todo.model.js** defines the client-side (browser) models for the to-do lists.</span></span> <span data-ttu-id="dff4f-153">モデルクラスには、todoItem と todoList の2つがあります。</span><span class="sxs-lookup"><span data-stu-id="dff4f-153">There are two model classes: todoItem and todoList.</span></span> <span data-ttu-id="dff4f-154">Ember.js では、モデルは DS のサブクラスです。型.</span><span class="sxs-lookup"><span data-stu-id="dff4f-154">In Ember, models are subclasses of DS.Model.</span></span> <span data-ttu-id="dff4f-155">モデルには、属性を持つプロパティを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="dff4f-155">A model can have properties with attributes:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample1.js)]

<span data-ttu-id="dff4f-156">モデルでは、他のモデルとのリレーションシップを定義できます。</span><span class="sxs-lookup"><span data-stu-id="dff4f-156">Models can define relationships to other models:</span></span>

[!code-css[Main](emberjs-template/samples/sample2.css)]

<span data-ttu-id="dff4f-157">モデルは、他のプロパティにバインドする計算されたプロパティを持つことができます。</span><span class="sxs-lookup"><span data-stu-id="dff4f-157">Models can have computed properties that bind to other properties:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample3.js)]

<span data-ttu-id="dff4f-158">モデルには、観察されたプロパティが変更されたときに呼び出されるオブザーバー関数を含めることができます。</span><span class="sxs-lookup"><span data-stu-id="dff4f-158">Models can have observer functions, which are invoked when an observed property changes:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample4.js)]

## <a name="views"></a><span data-ttu-id="dff4f-159">ビュー</span><span class="sxs-lookup"><span data-stu-id="dff4f-159">Views</span></span>

<span data-ttu-id="dff4f-160">ビューは、Scripts/app/views フォルダーで定義されています。</span><span class="sxs-lookup"><span data-stu-id="dff4f-160">The views are defined in the Scripts/app/views folder.</span></span> <span data-ttu-id="dff4f-161">ビューは、アプリケーション UI からのイベントを変換します。</span><span class="sxs-lookup"><span data-stu-id="dff4f-161">A view translates events from the application UI.</span></span> <span data-ttu-id="dff4f-162">イベントハンドラーは、コントローラー関数にコールバックすることも、単にデータコンテキストを直接呼び出すこともできます。</span><span class="sxs-lookup"><span data-stu-id="dff4f-162">An event handler can call back to controller functions, or simply call the data context directly.</span></span>

<span data-ttu-id="dff4f-163">たとえば、次のコードは views/TodoItemEditView からのものです。</span><span class="sxs-lookup"><span data-stu-id="dff4f-163">For example, the following code is from views/TodoItemEditView.js.</span></span> <span data-ttu-id="dff4f-164">入力テキストフィールドのイベント処理を定義します。</span><span class="sxs-lookup"><span data-stu-id="dff4f-164">It defines the event handling for an input text field.</span></span>

[!code-javascript[Main](emberjs-template/samples/sample5.js)]

## <a name="controller"></a><span data-ttu-id="dff4f-165">コントローラー</span><span class="sxs-lookup"><span data-stu-id="dff4f-165">Controller</span></span>

<span data-ttu-id="dff4f-166">コントローラーは、Scripts/app/controllers フォルダーで定義されています。</span><span class="sxs-lookup"><span data-stu-id="dff4f-166">The controllers are defined in the Scripts/app/controllers folder.</span></span> <span data-ttu-id="dff4f-167">1つのモデルを表すには、`Ember.ObjectController`を拡張します。</span><span class="sxs-lookup"><span data-stu-id="dff4f-167">To represent a single model, extend `Ember.ObjectController`:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample6.js)]

<span data-ttu-id="dff4f-168">コントローラーは、`Ember.ArrayController`を拡張することによって、モデルのコレクションを表すこともできます。</span><span class="sxs-lookup"><span data-stu-id="dff4f-168">A controller can also represent a collection of models by extending `Ember.ArrayController`.</span></span> <span data-ttu-id="dff4f-169">たとえば、Todolistcontroller.cs は `todoList` オブジェクトの配列を表します。</span><span class="sxs-lookup"><span data-stu-id="dff4f-169">For example, the TodoListController represents an array of `todoList` objects.</span></span> <span data-ttu-id="dff4f-170">コントローラーは、todoList ID で降順に並べ替えます。</span><span class="sxs-lookup"><span data-stu-id="dff4f-170">The controller sorts by todoList ID, in descending order:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample7.js)]

<span data-ttu-id="dff4f-171">コントローラーは `addTodoList`という名前の関数を定義します。この関数は、新しい todoList を作成して配列に追加します。</span><span class="sxs-lookup"><span data-stu-id="dff4f-171">The controller defines a function named `addTodoList`, which creates a new todoList and adds it to the array.</span></span> <span data-ttu-id="dff4f-172">この関数がどのように呼び出されるかを確認するには、テンプレートフォルダーで todoListTemplate という名前のテンプレートファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="dff4f-172">To see how this function gets called, open the template file named todoListTemplate.html, in the Templates folder.</span></span> <span data-ttu-id="dff4f-173">次のテンプレートコードは、ボタンを `addTodoList` 関数にバインドします。</span><span class="sxs-lookup"><span data-stu-id="dff4f-173">The following template code binds a button to the `addTodoList` function:</span></span>

[!code-html[Main](emberjs-template/samples/sample8.html)]

<span data-ttu-id="dff4f-174">このコントローラーには、エラーメッセージを保持する `error` プロパティも含まれています。</span><span class="sxs-lookup"><span data-stu-id="dff4f-174">The controller also contains an `error` property, which holds an error message.</span></span> <span data-ttu-id="dff4f-175">エラーメッセージを表示するためのテンプレートコードを次に示します (todoListTemplate でも同様)。</span><span class="sxs-lookup"><span data-stu-id="dff4f-175">Here is the template code to display the error message (also in todoListTemplate.html):</span></span>

[!code-html[Main](emberjs-template/samples/sample9.html)]

## <a name="routes"></a><span data-ttu-id="dff4f-176">ルート</span><span class="sxs-lookup"><span data-stu-id="dff4f-176">Routes</span></span>

<span data-ttu-id="dff4f-177">Router は、表示するルートと既定のテンプレートを定義し、アプリケーションの状態を設定して、Url をルートに一致させることができます。</span><span class="sxs-lookup"><span data-stu-id="dff4f-177">Router.js defines the routes and the default template to display, sets up application state, and matches URLs to routes:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample10.js)]

<span data-ttu-id="dff4f-178">TodoListRoute は、setupController 関数をオーバーライドすることによって、TodoListRoute のデータを読み込みます。</span><span class="sxs-lookup"><span data-stu-id="dff4f-178">TodoListRoute.js loads data for the TodoListRoute by overriding the setupController function:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample11.js)]

<span data-ttu-id="dff4f-179">Ember.js は、Url、ルート名、コントローラー、およびテンプレートを一致させるために名前付け規則を使用します。</span><span class="sxs-lookup"><span data-stu-id="dff4f-179">Ember uses naming conventions to match URLs, route names, controllers, and templates.</span></span> <span data-ttu-id="dff4f-180">詳細については、EmberJS のドキュメントの「 [http://emberjs.com/guides/routing/defining-your-routes/](http://emberjs.com/guides/routing/defining-your-routes/) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="dff4f-180">For more information, see [http://emberjs.com/guides/routing/defining-your-routes/](http://emberjs.com/guides/routing/defining-your-routes/) at the EmberJS documentation.</span></span>

## <a name="templates"></a><span data-ttu-id="dff4f-181">テンプレート</span><span class="sxs-lookup"><span data-stu-id="dff4f-181">Templates</span></span>

<span data-ttu-id="dff4f-182">Templates フォルダーには、次の4つのテンプレートが含まれています。</span><span class="sxs-lookup"><span data-stu-id="dff4f-182">The Templates folder contains four templates:</span></span>

- <span data-ttu-id="dff4f-183">application. hbs: アプリケーションの起動時に表示される既定のテンプレート。</span><span class="sxs-lookup"><span data-stu-id="dff4f-183">application.hbs: The default template that is rendered when the application is started.</span></span>
- <span data-ttu-id="dff4f-184">about. hbs: "/about" ルートのテンプレート。</span><span class="sxs-lookup"><span data-stu-id="dff4f-184">about.hbs: The template for the "/about" route.</span></span>
- <span data-ttu-id="dff4f-185">index. hbs: ルート "/" ルートのテンプレート。</span><span class="sxs-lookup"><span data-stu-id="dff4f-185">index.hbs: The template for the root "/" route.</span></span>
- <span data-ttu-id="dff4f-186">todoList: "/todo" ルートのテンプレート。</span><span class="sxs-lookup"><span data-stu-id="dff4f-186">todoList.hbs: The template for the "/todo" route.</span></span>
- <span data-ttu-id="dff4f-187">\_のナビゲーションバー: テンプレートは、ナビゲーションメニューを定義します。</span><span class="sxs-lookup"><span data-stu-id="dff4f-187">\_navbar.hbs: The template defines the navigation menu.</span></span>

<span data-ttu-id="dff4f-188">アプリケーションテンプレートは、マスターページのように機能します。</span><span class="sxs-lookup"><span data-stu-id="dff4f-188">The application template acts like a master page.</span></span> <span data-ttu-id="dff4f-189">ルートに応じて、に他のテンプレートを挿入するためのヘッダー、フッター、および "{{アウトレット}}" が含まれています。</span><span class="sxs-lookup"><span data-stu-id="dff4f-189">It contains a header, a footer, and an "{{outlet}}" to insert other templates in depending on the route.</span></span> <span data-ttu-id="dff4f-190">Ember.js のアプリケーションテンプレートの詳細については、「 [http://guides.emberjs.com/v1.10.0/templates/the-application-template//](http://guides.emberjs.com/v1.10.0/templates/the-application-template/)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="dff4f-190">For more information about application templates in Ember, see [http://guides.emberjs.com/v1.10.0/templates/the-application-template//](http://guides.emberjs.com/v1.10.0/templates/the-application-template/).</span></span>

<span data-ttu-id="dff4f-191">"/TodoList" テンプレートには、2つのループ式が含まれています。</span><span class="sxs-lookup"><span data-stu-id="dff4f-191">The "/todoList" template contains two loop expressions.</span></span> <span data-ttu-id="dff4f-192">外側のループが `{{#each controller}}`、内側のループが `{{#each todos}}`。</span><span class="sxs-lookup"><span data-stu-id="dff4f-192">The outside loop is `{{#each controller}}`, and the inside loop is `{{#each todos}}`.</span></span> <span data-ttu-id="dff4f-193">次のコードは、組み込みの `Ember.Checkbox` ビュー、カスタマイズされた `App.TodoItemEditView`、および `deleteTodo` アクションを含むリンクを示しています。</span><span class="sxs-lookup"><span data-stu-id="dff4f-193">The following code shows a built-in `Ember.Checkbox` view, a customized `App.TodoItemEditView`, and a link with a `deleteTodo` action.</span></span>

[!code-html[Main](emberjs-template/samples/sample12.html)]

<span data-ttu-id="dff4f-194">`HtmlHelperExtensions` クラスは、Controllers/Htmlによって定義されます。これは、web.config ファイルで**debug**が**true**に設定されている場合に、テンプレートファイルをキャッシュおよび挿入するためのヘルパー関数を定義します。</span><span class="sxs-lookup"><span data-stu-id="dff4f-194">The `HtmlHelperExtensions` class, defined in Controllers/HtmlHelperExtensions.cs, defines a helper function to cache and insert template files when **debug** is set to **true** in the Web.config file.</span></span> <span data-ttu-id="dff4f-195">この関数は、Views/Home/App.xaml に定義されている ASP.NET MVC ビューファイルから呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="dff4f-195">This function is called from the ASP.NET MVC view file defined in Views/Home/App.cshtml:</span></span>

[!code-cshtml[Main](emberjs-template/samples/sample13.cshtml)]

<span data-ttu-id="dff4f-196">引数を指定せずに呼び出された関数は、Templates フォルダー内のすべてのテンプレートファイルを表示します。</span><span class="sxs-lookup"><span data-stu-id="dff4f-196">Called with no arguments, the function renders all of the template files in the Templates folder.</span></span> <span data-ttu-id="dff4f-197">サブフォルダーまたは特定のテンプレートファイルを指定することもできます。</span><span class="sxs-lookup"><span data-stu-id="dff4f-197">You can also specify a subfolder or a specific template file.</span></span>

<span data-ttu-id="dff4f-198">Web.config で**debug**が**false**の場合、バンドル項目 "~/bundles/templates" がアプリケーションに含まれます。</span><span class="sxs-lookup"><span data-stu-id="dff4f-198">When **debug** is **false** in Web.config, the application includes the bundle item "~/bundles/templates".</span></span> <span data-ttu-id="dff4f-199">このバンドル項目は、ハンドルコンパイラライブラリを使用して BundleConfig.cs に追加されます。</span><span class="sxs-lookup"><span data-stu-id="dff4f-199">This bundle item is added in BundleConfig.cs, using the Handlebars compiler library:</span></span>

[!code-csharp[Main](emberjs-template/samples/sample14.cs)]
