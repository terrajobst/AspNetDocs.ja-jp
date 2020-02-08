---
uid: single-page-application/overview/templates/backbonejs-template
title: バックボーンテンプレート |Microsoft Docs
author: madskristensen
description: バックボーンの js SPA テンプレート
ms.author: riande
ms.date: 04/04/2013
ms.assetid: 00aca413-f067-4108-9bd1-cf21e64a2646
msc.legacyurl: /single-page-application/overview/templates/backbonejs-template
msc.type: authoredcontent
ms.openlocfilehash: 7297db7d5b35a53b40f9d9162960e529a167bd12
ms.sourcegitcommit: e365196c75ce93cd8967412b1cfdc27121816110
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/07/2020
ms.locfileid: "77074892"
---
# <a name="backbone-template"></a><span data-ttu-id="39334-103">Backbone テンプレート</span><span class="sxs-lookup"><span data-stu-id="39334-103">Backbone Template</span></span>

<span data-ttu-id="39334-104">[Mads Kristensen](https://github.com/madskristensen)</span><span class="sxs-lookup"><span data-stu-id="39334-104">by [Mads Kristensen](https://github.com/madskristensen)</span></span>

> <span data-ttu-id="39334-105">バックボーン SPA テンプレートは Kazi Manzur Rashid によって書き込まれました</span><span class="sxs-lookup"><span data-stu-id="39334-105">The Backbone SPA Template was written by Kazi Manzur Rashid</span></span>
> 
> [<span data-ttu-id="39334-106">バックボーンの node.js SPA テンプレートをダウンロードする</span><span class="sxs-lookup"><span data-stu-id="39334-106">Download the Backbone.js SPA Template</span></span>](https://go.microsoft.com/fwlink/?LinkId=293631)

<span data-ttu-id="39334-107">このような場合は[、バックボーンを使用し](http://backbonejs.org/)て、対話型のクライアント側 web アプリを簡単に構築できるように設計されています。</span><span class="sxs-lookup"><span data-stu-id="39334-107">The Backbone.js SPA template is designed to get you started quickly building interactive client-side web apps using [Backbone.js.](http://backbonejs.org/)</span></span>

<span data-ttu-id="39334-108">このテンプレートは、ASP.NET MVC でのバックボーンアプリケーション開発の初期スケルトンを提供します。</span><span class="sxs-lookup"><span data-stu-id="39334-108">The template provides an initial skeleton for developing a Backbone.js application in ASP.NET MVC.</span></span> <span data-ttu-id="39334-109">既定では、ユーザーのサインアップ、サインイン、パスワードのリセット、基本的な電子メールテンプレートを使用したユーザーの確認など、基本的なユーザーログイン機能が提供されています。</span><span class="sxs-lookup"><span data-stu-id="39334-109">Out of the box it provides basic user login functionality, including user sign-up, sign-in, password reset, and user confirmation with basic email templates.</span></span>

<span data-ttu-id="39334-110">要件:</span><span class="sxs-lookup"><span data-stu-id="39334-110">Requirements:</span></span>

- [<span data-ttu-id="39334-111">ASP.NET and Web Tools 2012.2 更新プログラム</span><span class="sxs-lookup"><span data-stu-id="39334-111">ASP.NET and Web Tools 2012.2 update</span></span>](https://go.microsoft.com/fwlink/?LinkId=282650)

## <a name="create-a-backbone-template-project"></a><span data-ttu-id="39334-112">バックボーンテンプレートプロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="39334-112">Create a Backbone Template Project</span></span>

<span data-ttu-id="39334-113">上の [ダウンロード] ボタンをクリックして、テンプレートをダウンロードしてインストールします。</span><span class="sxs-lookup"><span data-stu-id="39334-113">Download and install the template by clicking the Download button above.</span></span> <span data-ttu-id="39334-114">このテンプレートは、Visual Studio 拡張機能 (VSIX) ファイルとしてパッケージ化されています。</span><span class="sxs-lookup"><span data-stu-id="39334-114">The template is packaged as a Visual Studio Extension (VSIX) file.</span></span> <span data-ttu-id="39334-115">場合によっては、Visual Studio を再起動する必要があります。</span><span class="sxs-lookup"><span data-stu-id="39334-115">You might need to restart Visual Studio.</span></span>

<span data-ttu-id="39334-116">**[テンプレート]** ペインで、 **[インストールされたテンプレート]** を選択し、  **C#ビジュアル**ノードを展開します。</span><span class="sxs-lookup"><span data-stu-id="39334-116">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="39334-117">**[ビジュアルC# ]** で **[Web]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="39334-117">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="39334-118">プロジェクトテンプレートの一覧で、 **[ASP.NET MVC 4 Web アプリケーション]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="39334-118">In the list of project templates, select **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="39334-119">プロジェクトに名前を付けて、 **[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="39334-119">Name the project and click **OK**.</span></span>

![](backbonejs-template/_static/image1.png)

<span data-ttu-id="39334-120">**新しいプロジェクト**ウィザードで、[バックボーン SPA プロジェクト] を選択します。</span><span class="sxs-lookup"><span data-stu-id="39334-120">In the **New Project** wizard, select Backbone.js SPA Project.</span></span>

![](backbonejs-template/_static/image2.png)

<span data-ttu-id="39334-121">Ctrl キーを押しながら F5 キーを押してアプリケーションをビルドし、デバッグせずに実行するか、F5 キーを押してデバッグを実行します。</span><span class="sxs-lookup"><span data-stu-id="39334-121">Press Ctrl-F5 to build and run the application without debugging, or press F5 to run with debugging.</span></span>

![](backbonejs-template/_static/image3.png)

<span data-ttu-id="39334-122">[アカウント] をクリックすると、ログインページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="39334-122">Clicking "My Account" brings up the login page:</span></span>

![](backbonejs-template/_static/image4.png)

## <a name="walkthrough-client-code"></a><span data-ttu-id="39334-123">チュートリアル: クライアントコード</span><span class="sxs-lookup"><span data-stu-id="39334-123">Walkthrough: Client Code</span></span>

<span data-ttu-id="39334-124">では、クライアント側から始めましょう。</span><span class="sxs-lookup"><span data-stu-id="39334-124">Let's starts with the client side.</span></span> <span data-ttu-id="39334-125">クライアントアプリケーションスクリプトは、~/Scripts/application フォルダーにあります。</span><span class="sxs-lookup"><span data-stu-id="39334-125">The client application scripts are located in the ~/Scripts/application folder.</span></span> <span data-ttu-id="39334-126">アプリケーションは、JavaScript (.js ファイル) にコンパイルされる[TypeScript](http://www.typescriptlang.org/) (ts ファイル) で記述されます。</span><span class="sxs-lookup"><span data-stu-id="39334-126">The application is written in [TypeScript](http://www.typescriptlang.org/) (.ts files) which are compiled into JavaScript (.js files).</span></span>

<span data-ttu-id="39334-127">**アプリケーション**</span><span class="sxs-lookup"><span data-stu-id="39334-127">**Application**</span></span>

<span data-ttu-id="39334-128">`Application` は、application. ts に定義されています。</span><span class="sxs-lookup"><span data-stu-id="39334-128">`Application` is defined in application.ts.</span></span> <span data-ttu-id="39334-129">このオブジェクトは、アプリケーションを初期化し、ルート名前空間として機能します。</span><span class="sxs-lookup"><span data-stu-id="39334-129">This object initializes the application and acts as the root namespace.</span></span> <span data-ttu-id="39334-130">ユーザーがサインインしているかどうかなど、アプリケーション間で共有される構成および状態の情報を保持します。</span><span class="sxs-lookup"><span data-stu-id="39334-130">It maintains configuration and state information that is shared across the application, such as whether the user is signed in.</span></span>

<span data-ttu-id="39334-131">`application.start` メソッドは、モーダルビューを作成し、ユーザーのサインインなどのアプリケーションレベルのイベントのイベントハンドラーをアタッチします。</span><span class="sxs-lookup"><span data-stu-id="39334-131">The `application.start` method creates the modal views and attaches event handlers for application-level events, such as user sign-in.</span></span> <span data-ttu-id="39334-132">次に、既定のルーターを作成し、クライアント側の URL が指定されているかどうかを確認します。</span><span class="sxs-lookup"><span data-stu-id="39334-132">Next, it creates the default router and checks whether any client-side URL is specified.</span></span> <span data-ttu-id="39334-133">そうでない場合は、既定の url (#!/) にリダイレクトされます。</span><span class="sxs-lookup"><span data-stu-id="39334-133">If not, it redirects to the default url (#!/).</span></span>

<span data-ttu-id="39334-134">**イベント**</span><span class="sxs-lookup"><span data-stu-id="39334-134">**Events**</span></span>

<span data-ttu-id="39334-135">疎結合コンポーネントを開発する場合、イベントは常に重要です。</span><span class="sxs-lookup"><span data-stu-id="39334-135">Events are always important when developing loosely coupled components.</span></span> <span data-ttu-id="39334-136">多くの場合、アプリケーションはユーザーの操作に応じて複数の操作を実行します。</span><span class="sxs-lookup"><span data-stu-id="39334-136">Applications often perform multiple operations in response to a user action.</span></span> <span data-ttu-id="39334-137">バックボーンには、モデル、コレクション、ビューなどのコンポーネントを含む組み込みイベントが用意されています。</span><span class="sxs-lookup"><span data-stu-id="39334-137">Backbone provides built-in events with components such as Model, Collection, and View.</span></span> <span data-ttu-id="39334-138">このテンプレートは、これらのコンポーネント間で依存関係を作成するのではなく、"pub/sub" モデルを使用します。 `events` オブジェクトは、アプリケーションイベントを発行およびサブスクライブするためのイベントハブとして機能します。</span><span class="sxs-lookup"><span data-stu-id="39334-138">Instead of creating inter-dependencies among these components, the template uses a "pub/sub" model: The `events` object, defined in events.ts, acts as an event hub for publishing and subscribing to application events.</span></span> <span data-ttu-id="39334-139">`events` オブジェクトはシングルトンです。</span><span class="sxs-lookup"><span data-stu-id="39334-139">The `events` object is a singleton.</span></span> <span data-ttu-id="39334-140">次のコードは、イベントをサブスクライブし、イベントをトリガーする方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="39334-140">The following code shows how to subscribe to an event and then trigger the event:</span></span>

[!code-csharp[Main](backbonejs-template/samples/sample1.cs)]

<span data-ttu-id="39334-141">**ルーター**</span><span class="sxs-lookup"><span data-stu-id="39334-141">**Router**</span></span>

<span data-ttu-id="39334-142">バックボーンでは、ルーターにクライアント側ページをルーティングし、それらをアクションやイベントに接続するためのメソッドが用意されています。</span><span class="sxs-lookup"><span data-stu-id="39334-142">In Backbone.js, a router provides methods for routing client-side pages and connecting them to actions and events.</span></span> <span data-ttu-id="39334-143">このテンプレートは、router で1つのルーターを定義します。</span><span class="sxs-lookup"><span data-stu-id="39334-143">The template defines a single router, in router.ts.</span></span> <span data-ttu-id="39334-144">ルーターは、アクティブ化可能なビューを作成し、ビューを切り替えるときに状態を保持します。</span><span class="sxs-lookup"><span data-stu-id="39334-144">The router creates the activable views and maintains the state when switching views.</span></span> <span data-ttu-id="39334-145">アクティブ化可能なビューについては、次のセクションで説明します。初期状態では、プロジェクトには、[ホーム] と [バージョン情報] の2つのダミービューがあります。</span><span class="sxs-lookup"><span data-stu-id="39334-145">(Activable views are described in the next section.) Initially, the project has two dummy views, Home and About.</span></span> <span data-ttu-id="39334-146">また、NotFound ビューもあります。これは、ルートが不明の場合に表示されます。</span><span class="sxs-lookup"><span data-stu-id="39334-146">It also has a NotFound view, which is displayed if the route is not known.</span></span>

<span data-ttu-id="39334-147">**ビュー**</span><span class="sxs-lookup"><span data-stu-id="39334-147">**Views**</span></span>

<span data-ttu-id="39334-148">ビューは ~/スクリプト/アプリケーション/ビューで定義されています。</span><span class="sxs-lookup"><span data-stu-id="39334-148">The views are defined in ~/Scripts/application/views.</span></span> <span data-ttu-id="39334-149">ビューには、activable ビューとモーダルダイアログビューの2種類があります。</span><span class="sxs-lookup"><span data-stu-id="39334-149">There are two kinds of views, activable views and modal dialog views.</span></span> <span data-ttu-id="39334-150">アクティブ化可能なビューは、ルーターによって呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="39334-150">Activable views are invoked by the router.</span></span> <span data-ttu-id="39334-151">アクティブ化可能なビューが表示されると、他のすべてのアクティブ化可能なビューが非アクティブになります。</span><span class="sxs-lookup"><span data-stu-id="39334-151">When an activable view is shown, all other activable views become inactive.</span></span> <span data-ttu-id="39334-152">アクティブ化可能なビューを作成するには、`Activable` オブジェクトを使用してビューを拡張します。</span><span class="sxs-lookup"><span data-stu-id="39334-152">To create an activable view, extend the view with the `Activable` object:</span></span>

[!code-javascript[Main](backbonejs-template/samples/sample2.js)]

<span data-ttu-id="39334-153">`Activable` で拡張すると、ビュー、`activate`、および `deactivate`の2つの新しいメソッドが追加されます。</span><span class="sxs-lookup"><span data-stu-id="39334-153">Extending with `Activable` adds two new methods to the view, `activate` and `deactivate`.</span></span> <span data-ttu-id="39334-154">ルーターは、これらのメソッドを呼び出して、ビューをアクティブ化して残っ powerpivot します。</span><span class="sxs-lookup"><span data-stu-id="39334-154">The router calls these methods to activate and deactive the view.</span></span>

<span data-ttu-id="39334-155">モーダルビューは、 [Twitter ブートストラップ](https://twitter.github.com/bootstrap/)モーダルダイアログとして実装されます。</span><span class="sxs-lookup"><span data-stu-id="39334-155">Modal views are implemented as [Twitter Bootstrap](https://twitter.github.com/bootstrap/) modal dialogs.</span></span> <span data-ttu-id="39334-156">`Membership` ビューと `Profile` ビューは、モーダルビューです。</span><span class="sxs-lookup"><span data-stu-id="39334-156">The `Membership` and `Profile` views are modal views.</span></span> <span data-ttu-id="39334-157">モデルビューは、任意のアプリケーションイベントによって呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="39334-157">Model views can be invoked by any application events.</span></span> <span data-ttu-id="39334-158">たとえば、`Navigation` ビューでは、[マイアカウント] リンクをクリックすると、ユーザーがログインしているかどうかに応じて、`Membership` ビューまたは `Profile` ビューが表示されます。</span><span class="sxs-lookup"><span data-stu-id="39334-158">For example, in the `Navigation` view, clicking the "My Account" link shows either the `Membership` view or the `Profile` view, depending on whether the user is logged in.</span></span> <span data-ttu-id="39334-159">`Navigation` は、`data-command` 属性を持つすべての子要素に click イベントハンドラーをアタッチします。</span><span class="sxs-lookup"><span data-stu-id="39334-159">The `Navigation` attaches click event handlers to any child elements that have the `data-command` attribute.</span></span> <span data-ttu-id="39334-160">HTML マークアップは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="39334-160">Here is the HTML markup:</span></span>

[!code-html[Main](backbonejs-template/samples/sample3.html)]

<span data-ttu-id="39334-161">次に示すのは、イベントをフックするための、ナビゲーションのコードです。</span><span class="sxs-lookup"><span data-stu-id="39334-161">Here is the code in navigation.ts to hook up the events:</span></span>

[!code-csharp[Main](backbonejs-template/samples/sample4.cs)]

<span data-ttu-id="39334-162">**Models**</span><span class="sxs-lookup"><span data-stu-id="39334-162">**Models**</span></span>

<span data-ttu-id="39334-163">モデルは ~/Scripts/application/models. で定義されています。</span><span class="sxs-lookup"><span data-stu-id="39334-163">The models are defined in ~/Scripts/application/models.</span></span> <span data-ttu-id="39334-164">すべてのモデルには、既定の属性、検証規則、およびサーバー側のエンドポイントという3つの基本的な特徴があります。</span><span class="sxs-lookup"><span data-stu-id="39334-164">The models all have three basic things: default attributes, validation rules, and a server-side end point.</span></span> <span data-ttu-id="39334-165">一般的な例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="39334-165">Here is a typical example:</span></span>

[!code-javascript[Main](backbonejs-template/samples/sample5.js)]

<span data-ttu-id="39334-166">**プラグイン**</span><span class="sxs-lookup"><span data-stu-id="39334-166">**Plug-ins**</span></span>

<span data-ttu-id="39334-167">~/スクリプト/Application/lib フォルダーには、いくつかの便利な jQuery プラグインが含まれています。フォームの ts ファイルは、フォームデータを操作するためのプラグインを定義します。</span><span class="sxs-lookup"><span data-stu-id="39334-167">The ~/Scripts/application/lib folder contains a few handy jQuery plug-ins. The form.ts file defines a plug-in for working with form data.</span></span> <span data-ttu-id="39334-168">多くの場合、フォームデータをシリアル化または逆シリアル化し、モデルの検証エラーを表示する必要があります。</span><span class="sxs-lookup"><span data-stu-id="39334-168">Often you need to serialize or deserialize form data and show any model validation errors.</span></span> <span data-ttu-id="39334-169">フォームの ts プラグインには、`serializeFields`、`deserializeFields`、`showFieldErrors`などのメソッドがあります。</span><span class="sxs-lookup"><span data-stu-id="39334-169">The form.ts plug-in has methods such as `serializeFields`, `deserializeFields`, and `showFieldErrors`.</span></span> <span data-ttu-id="39334-170">次の例では、フォームをモデルにシリアル化する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="39334-170">The following example shows how to serialize a form to a model.</span></span>

[!code-javascript[Main](backbonejs-template/samples/sample6.js)]

<span data-ttu-id="39334-171">Flashbar プラグインは、さまざまな種類のフィードバックメッセージをユーザーに提供します。</span><span class="sxs-lookup"><span data-stu-id="39334-171">The flashbar.ts plug-in gives various kinds of feedback messages to the user.</span></span> <span data-ttu-id="39334-172">メソッドは、`$.showSuccessbar`、`$.showErrorbar`、および `$.showInfobar`です。</span><span class="sxs-lookup"><span data-stu-id="39334-172">The methods are `$.showSuccessbar`, `$.showErrorbar` and `$.showInfobar`.</span></span> <span data-ttu-id="39334-173">バックグラウンドでは、Twitter のブートストラップアラートを使用して、適切にアニメーション化されたメッセージを表示します。</span><span class="sxs-lookup"><span data-stu-id="39334-173">Behind the scenes, it uses Twitter Bootstrap alerts to show nicely animated messages.</span></span>

<span data-ttu-id="39334-174">次のように、API は多少異なりますが、ブラウザーの [確認] ダイアログボックスは、ts プラグインによって置き換えられます。</span><span class="sxs-lookup"><span data-stu-id="39334-174">The confirm.ts plug-in replaces the browser's confirm dialog, although the API is somewhat different:</span></span>

[!code-javascript[Main](backbonejs-template/samples/sample7.js)]

## <a name="walkthrough-server-code"></a><span data-ttu-id="39334-175">チュートリアル: サーバーコード</span><span class="sxs-lookup"><span data-stu-id="39334-175">Walkthrough: Server Code</span></span>

<span data-ttu-id="39334-176">では、サーバー側を見てみましょう。</span><span class="sxs-lookup"><span data-stu-id="39334-176">Now let's look at the server side.</span></span>

<span data-ttu-id="39334-177">**コントローラー**</span><span class="sxs-lookup"><span data-stu-id="39334-177">**Controllers**</span></span>

<span data-ttu-id="39334-178">シングルページアプリケーションでは、サーバーはユーザーインターフェイスでごくわずかな役割を果たします。</span><span class="sxs-lookup"><span data-stu-id="39334-178">In a single page application, the server plays only a small role in the user interface.</span></span> <span data-ttu-id="39334-179">通常、サーバーは最初のページを表示し、JSON データを送受信します。</span><span class="sxs-lookup"><span data-stu-id="39334-179">Typically, the server renders the initial page and then sends and receives JSON data.</span></span>

<span data-ttu-id="39334-180">テンプレートには、2つの MVC コントローラーがあります。 `HomeController` 最初のページを表示し、`SupportsController` を使用して新しいユーザーアカウントを確認し、パスワードをリセットします。</span><span class="sxs-lookup"><span data-stu-id="39334-180">The template has two MVC controllers: `HomeController` renders the initial page, and `SupportsController` is used to confirm new user accounts and reset passwords.</span></span> <span data-ttu-id="39334-181">テンプレート内の他のすべてのコントローラーは ASP.NET Web API コントローラーで、JSON データを送受信します。</span><span class="sxs-lookup"><span data-stu-id="39334-181">All other controllers in the template are ASP.NET Web API controllers, which send and receive JSON data.</span></span> <span data-ttu-id="39334-182">既定では、コントローラーは新しい `WebSecurity` クラスを使用して、ユーザー関連のタスクを実行します。</span><span class="sxs-lookup"><span data-stu-id="39334-182">By default, the controllers use the new `WebSecurity` class to perform user-related tasks.</span></span> <span data-ttu-id="39334-183">ただし、これらのタスクに対してデリゲートを渡すことができるオプションのコンストラクターも用意されています。</span><span class="sxs-lookup"><span data-stu-id="39334-183">However, they also have optional constructors that let you pass in delegates for these tasks.</span></span> <span data-ttu-id="39334-184">これにより、テストが容易になり、IoC コンテナーを使用して `WebSecurity` を別のものに置き換えることができます。</span><span class="sxs-lookup"><span data-stu-id="39334-184">This makes testing easier, and lets you replace `WebSecurity` with something else, by using an IoC Container.</span></span> <span data-ttu-id="39334-185">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="39334-185">Here is an example:</span></span>

[!code-csharp[Main](backbonejs-template/samples/sample8.cs)]

## <a name="views"></a><span data-ttu-id="39334-186">ビュー</span><span class="sxs-lookup"><span data-stu-id="39334-186">Views</span></span>

<span data-ttu-id="39334-187">ビューはモジュール化されるように設計されています。ページの各セクションには専用のビューがあります。</span><span class="sxs-lookup"><span data-stu-id="39334-187">The views are designed to be modular: Each section of a page has its own dedicated view.</span></span> <span data-ttu-id="39334-188">シングルページアプリケーションでは、対応するコントローラーを持たないビューが含まれるのが一般的です。</span><span class="sxs-lookup"><span data-stu-id="39334-188">In a single page application, it is common to include views that do not have any corresponding controller.</span></span> <span data-ttu-id="39334-189">`@Html.Partial('myView')`を呼び出すことによってビューを含めることができますが、これは面倒です。</span><span class="sxs-lookup"><span data-stu-id="39334-189">You can include a view by calling `@Html.Partial('myView')`, but this gets tedious.</span></span> <span data-ttu-id="39334-190">これを簡単にするために、テンプレートは、指定されたフォルダー内のすべてのビューを表示するヘルパーメソッド `IncludeClientViews`を定義します。</span><span class="sxs-lookup"><span data-stu-id="39334-190">To make this easier, the template defines a helper method, `IncludeClientViews`, that renders all of the views in a specified folder:</span></span>

[!code-cshtml[Main](backbonejs-template/samples/sample9.cshtml)]

<span data-ttu-id="39334-191">フォルダー名が指定されていない場合、既定のフォルダー名は "ClientViews" になります。</span><span class="sxs-lookup"><span data-stu-id="39334-191">If the folder name is not specified, the default folder name is "ClientViews".</span></span> <span data-ttu-id="39334-192">クライアントビューでも部分ビューが使用されている場合は、部分ビューにアンダースコア文字を付けます (たとえば、`_SignUp`)。</span><span class="sxs-lookup"><span data-stu-id="39334-192">If your client view also uses partial views, name the partial view with an underscore character (for example, `_SignUp`).</span></span> <span data-ttu-id="39334-193">`IncludeClientViews` メソッドでは、アンダースコアで始まる名前を持つビューは除外されます。</span><span class="sxs-lookup"><span data-stu-id="39334-193">The `IncludeClientViews` method excludes any views whose name starts with an underscore.</span></span> <span data-ttu-id="39334-194">部分ビューをクライアントビューに含めるには、`Html.Partial('_SignUp')`ではなく `Html.ClientView('SignUp')` を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="39334-194">To include a partial view in the client view, call `Html.ClientView('SignUp')` instead of `Html.Partial('_SignUp')`.</span></span>

<span data-ttu-id="39334-195">**電子メールの送信**</span><span class="sxs-lookup"><span data-stu-id="39334-195">**Sending Email**</span></span>

<span data-ttu-id="39334-196">電子メールを送信する場合、テンプレートは[郵便](http://aboutcode.net/postal)を使用します。</span><span class="sxs-lookup"><span data-stu-id="39334-196">To send email, the template uses [Postal](http://aboutcode.net/postal).</span></span> <span data-ttu-id="39334-197">ただし、郵便は `IMailer` インターフェイスを使用してコードの残りの部分から抽象化されるため、別の実装に簡単に置き換えることができます。</span><span class="sxs-lookup"><span data-stu-id="39334-197">However, Postal is abstracted from the rest of the code with the `IMailer` interface, so you can easily replace it with another implementation.</span></span> <span data-ttu-id="39334-198">電子メールテンプレートは、[Views/email] フォルダーにあります。</span><span class="sxs-lookup"><span data-stu-id="39334-198">The email templates are located in the Views/Emails folder.</span></span> <span data-ttu-id="39334-199">送信者の電子メールアドレスは、web.config ファイルの**appSettings**セクションの `sender.email` キーに指定されます。</span><span class="sxs-lookup"><span data-stu-id="39334-199">The sender's email address is specified in the web.config file, in the `sender.email` key of the **appSettings** section.</span></span> <span data-ttu-id="39334-200">また、web.config で `debug="true"` 場合、アプリケーションは開発を高速化するためにユーザーの電子メール確認を必要としません。</span><span class="sxs-lookup"><span data-stu-id="39334-200">Also, when `debug="true"` in web.config, the application does not require user email confirmation, to speed up development.</span></span>

## <a name="github"></a><span data-ttu-id="39334-201">GitHub</span><span class="sxs-lookup"><span data-stu-id="39334-201">GitHub</span></span>

<span data-ttu-id="39334-202">また、 [GitHub](https://github.com/kazimanzurrashid/AspNetMvcBackboneJsSpa)では、バックボーンの node.js のテンプレートを見つけることもできます。</span><span class="sxs-lookup"><span data-stu-id="39334-202">You can also find the Backbone.js SPA template on [GitHub](https://github.com/kazimanzurrashid/AspNetMvcBackboneJsSpa).</span></span>
