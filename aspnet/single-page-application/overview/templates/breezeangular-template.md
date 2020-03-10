---
uid: single-page-application/overview/templates/breezeangular-template
title: 簡単/角度のテンプレート |Microsoft Docs
author: madskristensen
description: 簡単/角度のシングルページアプリケーションテンプレート
ms.author: riande
ms.date: 03/08/2013
ms.assetid: db31e909-563a-4516-aadd-62aa210ac7e4
msc.legacyurl: /single-page-application/overview/templates/breezeangular-template
msc.type: authoredcontent
ms.openlocfilehash: 3e4e63d385a56d51d3d08696782b43d6228f6201
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467188"
---
# <a name="breezeangular-template"></a><span data-ttu-id="b27da-103">Breeze/Angular テンプレート</span><span class="sxs-lookup"><span data-stu-id="b27da-103">Breeze/Angular template</span></span>

<span data-ttu-id="b27da-104">[Mads Kristensen](https://github.com/madskristensen)</span><span class="sxs-lookup"><span data-stu-id="b27da-104">by [Mads Kristensen](https://github.com/madskristensen)</span></span>

> <span data-ttu-id="b27da-105">簡単/角度の MVC テンプレートが、ワードベルによって書き込まれました</span><span class="sxs-lookup"><span data-stu-id="b27da-105">The Breeze/Angular MVC Template was written by Ward Bell</span></span>
> 
> [<span data-ttu-id="b27da-106">簡単/角度の MVC テンプレートをダウンロードする</span><span class="sxs-lookup"><span data-stu-id="b27da-106">Download the Breeze/Angular MVC Template</span></span>](https://go.microsoft.com/fwlink/?LinkId=286437)

<span data-ttu-id="b27da-107">[AngularJS](http://angularjs.org)は、シングルページアプリケーション (spa) を構築するための Google のオープンソースライブラリです。</span><span class="sxs-lookup"><span data-stu-id="b27da-107">[AngularJS](http://angularjs.org) is an open source library from Google for building Single Page Applications (SPAs).</span></span> <span data-ttu-id="b27da-108">データバインディング、依存関係の挿入、および画面管理が用意されています。</span><span class="sxs-lookup"><span data-stu-id="b27da-108">It offers data binding, dependency injection, and screen management.</span></span> <span data-ttu-id="b27da-109">[BreezeJS](http://www.breezejs.com/?utm_source=ms-spa)とデータモデリングおよびデータ管理用の別のオープンソースライブラリを組み合わせることにより、優れた HTML/JavaScript クライアントアプリのための不可欠な要素を持つことができます。</span><span class="sxs-lookup"><span data-stu-id="b27da-109">Combine it with [BreezeJS](http://www.breezejs.com/?utm_source=ms-spa), another open source library for data modeling and data management, and you have the essential ingredients for a great HTML/JavaScript client app.</span></span>

<span data-ttu-id="b27da-110">[KNOCKOUTJS spa](../introduction/knockoutjs-template.md)テンプレートは、ASP.NET and Web Tools 2012.2 更新プログラムに含まれています。</span><span class="sxs-lookup"><span data-stu-id="b27da-110">The Breeze/Angular SPA template is a variation on the [KnockoutJS SPA template](../introduction/knockoutjs-template.md) included in the ASP.NET and Web Tools 2012.2 Update.</span></span> <span data-ttu-id="b27da-111">Visual Studio を使用している場合は、SPA の例が60秒未満で稼働しています。</span><span class="sxs-lookup"><span data-stu-id="b27da-111">If you've got Visual Studio, you'll have an example SPA up and running in less than 60 seconds.</span></span>

![](http://www.breezejs.com/sites/all/images/spa-template/NgRunningTodoPage.png)

<span data-ttu-id="b27da-112">と、アプリケーションは KnockoutJS SPA テンプレートとよく似ています。</span><span class="sxs-lookup"><span data-stu-id="b27da-112">Outwardly, the application looks the very similar to the KnockoutJS SPA template.</span></span> <span data-ttu-id="b27da-113">しかし、内部的にはまったく異なります。</span><span class="sxs-lookup"><span data-stu-id="b27da-113">But it's quite different under the hood.</span></span> <span data-ttu-id="b27da-114">KnockoutJS テンプレートでは、データバインディングにノックアウトを使用し、データアクセスに未加工の AJAX を使用します。</span><span class="sxs-lookup"><span data-stu-id="b27da-114">The KnockoutJS template uses Knockout for data binding and raw AJAX for data access.</span></span> <span data-ttu-id="b27da-115">簡単/角度のテンプレートでは、データバインディングには角、データアクセスには簡単です。</span><span class="sxs-lookup"><span data-stu-id="b27da-115">The Breeze/Angular template uses Angular for data binding and Breeze for data access.</span></span> <span data-ttu-id="b27da-116">これらのライブラリを使用すると、ページナビゲーションや履歴などの追加機能が有効になります。</span><span class="sxs-lookup"><span data-stu-id="b27da-116">These libraries enable additional capabilities, including page navigation and history.</span></span>

<span data-ttu-id="b27da-117">アプリケーションの [バージョン情報] ページを次に示します。</span><span class="sxs-lookup"><span data-stu-id="b27da-117">Here is the application's About page:</span></span>

![](http://www.breezejs.com/sites/all/images/spa-template/NgRunningAboutPage.png)

<span data-ttu-id="b27da-118">このページには、現在のユーザーセッション中のイベントの実行中のログが表示されます。次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="b27da-118">This page displays a running log of events during the current user session, including:</span></span>

- <span data-ttu-id="b27da-119">ベル.</span><span class="sxs-lookup"><span data-stu-id="b27da-119">Paging.</span></span> <span data-ttu-id="b27da-120">#2 と #7 での Todo コントローラーの作成に注意してください。</span><span class="sxs-lookup"><span data-stu-id="b27da-120">Note the Todo controller creation at #2 and #7.</span></span>
- <span data-ttu-id="b27da-121">リモートクエリ (#3) とローカルキャッシュクエリ (#7)。</span><span class="sxs-lookup"><span data-stu-id="b27da-121">Remote queries (#3) and local cache queries (#7).</span></span>
- <span data-ttu-id="b27da-122">新しい (#5、#6) および変更された (#4) エンティティを保存しています。</span><span class="sxs-lookup"><span data-stu-id="b27da-122">Saving new (#5, #6) and modified (#4) entities.</span></span>
- <span data-ttu-id="b27da-123">クライアントで検証された変更 (#9)。これにより、ユーザーはデータベースに変更をコミットする前に誤りを修正できます。</span><span class="sxs-lookup"><span data-stu-id="b27da-123">Changes validated on the client (#9), so the user can correct mistakes before committing changes to the database.</span></span>

<span data-ttu-id="b27da-124">このテンプレートの詳細については、次を参照してください。</span><span class="sxs-lookup"><span data-stu-id="b27da-124">There's more to explore in this template, including:</span></span>

- <span data-ttu-id="b27da-125">HTML ビューテンプレートの動的読み込み。</span><span class="sxs-lookup"><span data-stu-id="b27da-125">Dynamic loading of HTML view templates.</span></span>
- <span data-ttu-id="b27da-126">角の "ディレクティブ" を使用したカスタムデータバインディング。</span><span class="sxs-lookup"><span data-stu-id="b27da-126">Custom data binding through Angular "directives."</span></span>
- <span data-ttu-id="b27da-127">モジュール性と依存関係の注入。</span><span class="sxs-lookup"><span data-stu-id="b27da-127">Modularity and dependency injection.</span></span>
- <span data-ttu-id="b27da-128">クエリフィルター、並べ替え、ページング、プロジェクション、関連エンティティの包含。</span><span class="sxs-lookup"><span data-stu-id="b27da-128">Query filters, sorts, paging, projections, and inclusion of related entities.</span></span>
- <span data-ttu-id="b27da-129">複数の画面でのデータの共有。</span><span class="sxs-lookup"><span data-stu-id="b27da-129">Sharing data across multiple screens.</span></span>
- <span data-ttu-id="b27da-130">複数の変更を1つのトランザクションとして保存します。</span><span class="sxs-lookup"><span data-stu-id="b27da-130">Saving multiple changes as a single transaction.</span></span>
- <span data-ttu-id="b27da-131">検証規則は、サーバーから JavaScript クライアントに自動的に反映されます。</span><span class="sxs-lookup"><span data-stu-id="b27da-131">Validation rules propagated automatically from the server to the JavaScript client.</span></span>

<span data-ttu-id="b27da-132">それでは始めましょう。</span><span class="sxs-lookup"><span data-stu-id="b27da-132">Let's get started.</span></span>

## <a name="create-a-breezeangular-template-project"></a><span data-ttu-id="b27da-133">簡単/角度のテンプレートプロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="b27da-133">Create a Breeze/Angular Template Project</span></span>

<span data-ttu-id="b27da-134">上の [ダウンロード] ボタンをクリックして、テンプレートをダウンロードしてインストールします。</span><span class="sxs-lookup"><span data-stu-id="b27da-134">Download and install the template by clicking the Download button above.</span></span> <span data-ttu-id="b27da-135">このテンプレートは、Visual Studio 拡張機能 (VSIX) ファイルとしてパッケージ化されています。</span><span class="sxs-lookup"><span data-stu-id="b27da-135">The template is packaged as a Visual Studio Extension (VSIX) file.</span></span> <span data-ttu-id="b27da-136">場合によっては、Visual Studio を再起動する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b27da-136">You might need to restart Visual Studio.</span></span>

<span data-ttu-id="b27da-137">**[テンプレート]** ペインで、 **[インストールされたテンプレート]** を選択し、  **C#ビジュアル**ノードを展開します。</span><span class="sxs-lookup"><span data-stu-id="b27da-137">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="b27da-138">**[ビジュアルC# ]** で **[Web]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="b27da-138">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="b27da-139">プロジェクトテンプレートの一覧で、 **[ASP.NET MVC 4 Web アプリケーション]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="b27da-139">In the list of project templates, select **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="b27da-140">プロジェクト名を指定して、 **[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="b27da-140">Name the project and click **OK**.</span></span>

<span data-ttu-id="b27da-141">**新しいプロジェクト**ウィザードで、[簡単に**SPA**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="b27da-141">In the **New Project** wizard, select **Breeze Angular SPA**.</span></span>

![](http://www.breezejs.com/sites/all/images/spa-template/SelectBreezeNgSpaTemplate.png)

<span data-ttu-id="b27da-142">Ctrl キーを押しながら F5 キーを押してアプリケーションをビルドし、デバッグせずに実行するか、F5 キーを押してデバッグを実行します。</span><span class="sxs-lookup"><span data-stu-id="b27da-142">Press Ctrl-F5 to build and run the application without debugging, or press F5 to run with debugging.</span></span>

![](http://www.breezejs.com/sites/all/images/spa-template/ZephyrLogin.png)

<span data-ttu-id="b27da-143">アプリケーションを初めて実行すると、ログイン画面が表示されます。</span><span class="sxs-lookup"><span data-stu-id="b27da-143">When the application first runs, it displays a login screen.</span></span> <span data-ttu-id="b27da-144">[サインアップ] リンクをクリックすると、新しいページ glides が表示されます。このページでは、ユーザー名とパスワードを入力できます。</span><span class="sxs-lookup"><span data-stu-id="b27da-144">Click the "Sign up" link and a new page glides into view, where you can enter a username and password.</span></span> <span data-ttu-id="b27da-145">(ログインページと登録ページは、ASP.NET MVC を使用して作成されます)。登録フォームを送信すると、サーバーによって、アカウントの2つの項目を含む TodoList が生成されます。</span><span class="sxs-lookup"><span data-stu-id="b27da-145">(The login and registration pages are built using ASP.NET MVC.) When you submit the registration form, the server generates a TodoList with two items for your account.</span></span> <span data-ttu-id="b27da-146">次に、黄色のメモでそれらを表示します。</span><span class="sxs-lookup"><span data-stu-id="b27da-146">Then it presents them to you on a yellow note.</span></span>

![](http://www.breezejs.com/sites/all/images/spa-template/TodoList.png)

<span data-ttu-id="b27da-147">これで SPA の土地が完成しました。</span><span class="sxs-lookup"><span data-stu-id="b27da-147">Now you are in the land of SPA.</span></span> <span data-ttu-id="b27da-148">コードを操作しているときに表示されるものと経験があるものはすべて、ノックアウトと簡単な方法でクライアントでレンダリングおよび管理されます。</span><span class="sxs-lookup"><span data-stu-id="b27da-148">Everything you see and experience while manipulating Todos is rendered and managed on the client with the help of Knockout and Breeze.</span></span> <span data-ttu-id="b27da-149">アプリをユーザーとして探索...</span><span class="sxs-lookup"><span data-stu-id="b27da-149">Explore the app as a user …</span></span> <span data-ttu-id="b27da-150">しかし、開発者にとっては、</span><span class="sxs-lookup"><span data-stu-id="b27da-150">but with a developer's eye.</span></span> <span data-ttu-id="b27da-151">ブラウザーで開発者ツールを使用して、ネットワークトラフィックをキャプチャします。</span><span class="sxs-lookup"><span data-stu-id="b27da-151">Use the developer tools in your browser to capture the network traffic.</span></span> <span data-ttu-id="b27da-152">(Internet Explorer で F12 キーを押して、 **[ネットワーク]** タブを選択し、 **[キャプチャの開始]** をクリックします)。ここで、次の操作を実行します。</span><span class="sxs-lookup"><span data-stu-id="b27da-152">(In Internet Explorer: Press F12, select the **Network** tab, and click **Start capturing**.) Now try the following:</span></span>

- <span data-ttu-id="b27da-153">新しい Todo 項目を追加します。</span><span class="sxs-lookup"><span data-stu-id="b27da-153">Add a new Todo item.</span></span>
- <span data-ttu-id="b27da-154">ラベルをクリックし、Todo 項目のタイトルを編集します</span><span class="sxs-lookup"><span data-stu-id="b27da-154">Click the label and edit the Todo item title</span></span>
- <span data-ttu-id="b27da-155">チェックボックスをオンにして、完了した項目をマークします。</span><span class="sxs-lookup"><span data-stu-id="b27da-155">Check a checkbox to mark the item done.</span></span> <span data-ttu-id="b27da-156">テキストボックスが無効になっていることに注意してください。そのため、タイトルは編集できなくなります。</span><span class="sxs-lookup"><span data-stu-id="b27da-156">Notice that the textbox is disabled, so the title is no longer editable.</span></span>
- <span data-ttu-id="b27da-157">ラベルの右側にある [x] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="b27da-157">Click the ‘x' to the right of the label.</span></span> <span data-ttu-id="b27da-158">アイテムが表示されなくなり、データベースから削除されます。</span><span class="sxs-lookup"><span data-stu-id="b27da-158">The item disappears and is deleted from the database.</span></span>
- <span data-ttu-id="b27da-159">別の項目を選択し、そのタイトルをクリアします。</span><span class="sxs-lookup"><span data-stu-id="b27da-159">Pick another item and clear its title.</span></span> <span data-ttu-id="b27da-160">タイトルが必要であることを示す検証エラーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="b27da-160">You'll get a validation error that the title is required.</span></span> <span data-ttu-id="b27da-161">しばらくすると、前のタイトルが復元されます。</span><span class="sxs-lookup"><span data-stu-id="b27da-161">After a brief pause, the previous title is restored.</span></span>
- <span data-ttu-id="b27da-162">呼べの長いタイトルを入力します。</span><span class="sxs-lookup"><span data-stu-id="b27da-162">Type in a ridiculously long title.</span></span> <span data-ttu-id="b27da-163">タイトルが長すぎるという別の検証エラーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="b27da-163">You'll get a different validation error that the title is too long.</span></span>
- <span data-ttu-id="b27da-164">[Todo リストの追加] ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="b27da-164">Click the "Add Todo List" button.</span></span> <span data-ttu-id="b27da-165">前の一覧の左側に新しいリストが表示されます。</span><span class="sxs-lookup"><span data-stu-id="b27da-165">A new list appears to the left of the previous list.</span></span>
- <span data-ttu-id="b27da-166">TodoList のタイトルで再生し、必要な長さの検証をトリガーします。</span><span class="sxs-lookup"><span data-stu-id="b27da-166">Play with the TodoList title, triggering its required and length validations.</span></span>
- <span data-ttu-id="b27da-167">[タイトル] ボックスをクリックして、エラーメッセージをクリアします。</span><span class="sxs-lookup"><span data-stu-id="b27da-167">Click in the title textbox to clear the error message.</span></span>
- <span data-ttu-id="b27da-168">右上隅にある円の "x" をクリックして、TodoList とその todos を削除します。</span><span class="sxs-lookup"><span data-stu-id="b27da-168">Click the "x" in the circle in the upper right corner to delete the TodoList and its todos.</span></span>
- <span data-ttu-id="b27da-169">右上の [バージョン情報] リンクをクリックすると、これらのアクティビティのログが表示されます。</span><span class="sxs-lookup"><span data-stu-id="b27da-169">Click the "About" link in the upper right to see a log of these activities.</span></span>

<span data-ttu-id="b27da-170">検証ロジックは、クライアント側で簡単に実行されます。</span><span class="sxs-lookup"><span data-stu-id="b27da-170">The validation logic is performed client-side by Breeze.</span></span> <span data-ttu-id="b27da-171">サーバーモデルクラスの検証属性はクライアントに反映され、クライアントがサーバーに接続する前に自動的に実行されます。</span><span class="sxs-lookup"><span data-stu-id="b27da-171">Validation attributes on the server model classes are propagated to the client and executed automatically before the client contacts the server.</span></span>

<span data-ttu-id="b27da-172">ネットワークトラフィックを確認します。</span><span class="sxs-lookup"><span data-stu-id="b27da-172">Review the network traffic.</span></span> <span data-ttu-id="b27da-173">簡単にエラーが検出された場合、サーバーへの呼び出しがないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="b27da-173">Notice that there were no calls to the server when Breeze detected an error.</span></span> <span data-ttu-id="b27da-174">有効な変更が発生するたびに、POST 要求が "/api/Todo/SaveChanges" になりました。</span><span class="sxs-lookup"><span data-stu-id="b27da-174">Each valid change resulted in a POST request to "/api/Todo/SaveChanges".</span></span> <span data-ttu-id="b27da-175">簡単に変更をバンドルし、Web API コントローラーの `SaveChanges` 方法に1つの要求としてまとめて送信します。</span><span class="sxs-lookup"><span data-stu-id="b27da-175">Breeze bundles the changes and sends them together as a single request to the Web API controller's `SaveChanges` method.</span></span> <span data-ttu-id="b27da-176">これは、各項目に対して、PUT、POST、および DELETE 要求を個別に行う KnockoutJS SPA テンプレートとは異なります。</span><span class="sxs-lookup"><span data-stu-id="b27da-176">That's different from KnockoutJS SPA template, which makes PUT, POST, and DELETE requests for each item individually.</span></span>

<span data-ttu-id="b27da-177">また、TodoList ページと About ページを切り替えるときにネットワークトラフィックが発生しないことにも注意してください。</span><span class="sxs-lookup"><span data-stu-id="b27da-177">Also, notice there is no network traffic when you switch between the TodoList and About pages.</span></span> <span data-ttu-id="b27da-178">これは、クエリがローカルの簡単なキャッシュに制約されているためです。</span><span class="sxs-lookup"><span data-stu-id="b27da-178">That's because the query has been constrained to the local Breeze cache.</span></span>

## <a name="peek-inside"></a><span data-ttu-id="b27da-179">内部を見る</span><span class="sxs-lookup"><span data-stu-id="b27da-179">Peek inside</span></span>

<span data-ttu-id="b27da-180">このアプリケーションには、クライアント側とサーバー側があります。</span><span class="sxs-lookup"><span data-stu-id="b27da-180">This application has a client side and a server side.</span></span> <span data-ttu-id="b27da-181">クライアント側スタックは、アプリケーションの JavaScript モジュール ("アプリ" フォルダー内) とサードパーティ製の JavaScript ライブラリ ("Scripts" フォルダー内) のわずかな HTML と組み合わせで構成されます。</span><span class="sxs-lookup"><span data-stu-id="b27da-181">The client-side stack consists of a little HTML and a combination of application JavaScript modules (in the "app" folder) plus third-party JavaScript libraries (in the "Scripts" folder).</span></span>

![](http://www.breezejs.com/sites/all/images/spa-template/NgClientArchitecture2.png)

<span data-ttu-id="b27da-182">UI アーキテクチャは、ビューの HTML ウィジェットを、コントローラー内のサポートするプレゼンテーションコードから分離します。</span><span class="sxs-lookup"><span data-stu-id="b27da-182">The UI architecture separates the HTML widgets of the views from the supporting presentation code in the controllers.</span></span> <span data-ttu-id="b27da-183">角度データバインディングシステムでは、ビューとコントローラーを調整して、各がジョブを実行できるようにします。</span><span class="sxs-lookup"><span data-stu-id="b27da-183">The Angular data-binding system coordinates views and controllers so that each can do its job without intimate knowledge of the other.</span></span>

<span data-ttu-id="b27da-184">コントローラーは、モデルエンティティを取得して保存するようデータコンテキストに要求します。</span><span class="sxs-lookup"><span data-stu-id="b27da-184">The controller asks the data context to acquire and save the model entities.</span></span> <span data-ttu-id="b27da-185">データコンテキストでは、ほとんどの作業が簡単に委任されます。これにより、JSON クエリの結果から自己追跡モデルオブジェクトが構築されます。</span><span class="sxs-lookup"><span data-stu-id="b27da-185">The data context delegates most of the work to Breeze, which constructs self-tracking model objects from JSON query results.</span></span>

<span data-ttu-id="b27da-186">サーバー側スタックは、いくつかの開発者コードと .NET ライブラリである Web API、Entity Framework、Breeze.NET で構成されています。</span><span class="sxs-lookup"><span data-stu-id="b27da-186">The server-side stack consists of some developer code and three principle .NET libraries: Web API, Entity Framework, and Breeze.NET:</span></span>

![](http://www.breezejs.com/sites/all/images/spa-template/ServerArchitecture.png)

<span data-ttu-id="b27da-187">基本的なアーキテクチャは、KnockoutJS SPA テンプレートと同じです。</span><span class="sxs-lookup"><span data-stu-id="b27da-187">The basic architecture is the same as the KnockoutJS SPA template.</span></span> <span data-ttu-id="b27da-188">ただし、この実装ははるかに簡単です。 Dto が削除され、Entity Framework の詳細のほとんどが Breeze.NET に委任されています。</span><span class="sxs-lookup"><span data-stu-id="b27da-188">However, the implementation is much simpler: The DTOs were deleted, and most of the Entity Framework details have been delegated to Breeze.NET.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b27da-189">次の手順</span><span class="sxs-lookup"><span data-stu-id="b27da-189">Next Steps</span></span>

<span data-ttu-id="b27da-190">ここでは、簡単な web サイトのクライアントとサーバーの両方のスタックについて[詳しく説明](http://www.breezejs.com/ng-spa-template?utm_source=ms-spa)したコードを参照することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="b27da-190">We suggest that you explore the code, guided by the [extensive discussion](http://www.breezejs.com/ng-spa-template?utm_source=ms-spa) of both the client and the server stacks on the Breeze website.</span></span>

<span data-ttu-id="b27da-191">クライアント側のクエリを簡単に試してみることができます。いくつかのフィルターと並べ替えを追加します。</span><span class="sxs-lookup"><span data-stu-id="b27da-191">You might try playing with Breeze client-side query; add some filters and sorts.</span></span> <span data-ttu-id="b27da-192">エンドツーエンドの SPA 開発に対してより良い感覚を得るために、モデルのプロパティやエンティティをさらに追加することもできます。</span><span class="sxs-lookup"><span data-stu-id="b27da-192">You might add more model properties and more entities to get a better feel for end-to-end SPA development.</span></span> <span data-ttu-id="b27da-193">設計が自信を持っている場合は、Todo 機能を破棄して独自の機能に置き換えることができます。</span><span class="sxs-lookup"><span data-stu-id="b27da-193">When you are confident of the design, you can tear out the Todo features and replace them with your own.</span></span>

<span data-ttu-id="b27da-194">コーディングをお楽しみください!</span><span class="sxs-lookup"><span data-stu-id="b27da-194">Happy coding!</span></span>
