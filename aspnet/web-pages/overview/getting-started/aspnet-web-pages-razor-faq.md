---
uid: web-pages/overview/getting-started/aspnet-web-pages-razor-faq
title: ASP.NET Web ページ (Razor) に関する FAQ |Microsoft Docs
author: Rick-Anderson
description: この記事では、ASP.NET Web ページ (Razor) と WebMatrix に関してよく寄せられる質問をいくつか紹介します。 チュートリアルで使用されているソフトウェアのバージョン ASP.NET Web ページ (R...
ms.author: riande
ms.date: 02/07/2014
ms.assetid: b137bd04-25e1-47cb-9d96-ef2e179ecf1f
msc.legacyurl: /web-pages/overview/getting-started/aspnet-web-pages-razor-faq
msc.type: authoredcontent
ms.openlocfilehash: 6fa1b668e915af856a693e79eafb7180ed504dc2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78520654"
---
# <a name="aspnet-web-pages-razor-faq"></a><span data-ttu-id="f4cb7-104">ASP.NET Web Pages (Razor) FAQ (英語)</span><span class="sxs-lookup"><span data-stu-id="f4cb7-104">ASP.NET Web Pages (Razor) FAQ</span></span>

<span data-ttu-id="f4cb7-105">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="f4cb7-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> > [!NOTE] 
> > <span data-ttu-id="f4cb7-106">WebMatrix はASP.NET Webページの統合開発環境としては推奨されなくなりました。</span><span class="sxs-lookup"><span data-stu-id="f4cb7-106">WebMatrix is no longer recommended as an integrated development environment for ASP.NET Web Pages.</span></span> <span data-ttu-id="f4cb7-107">[Visual Studio](xref:aspnet/web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio)または[Visual Studio Code](https://code.visualstudio.com/)を使用します。</span><span class="sxs-lookup"><span data-stu-id="f4cb7-107">Use [Visual Studio](xref:aspnet/web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio) or [Visual Studio Code](https://code.visualstudio.com/).</span></span>
>
> <span data-ttu-id="f4cb7-108">この記事では、ASP.NET Web ページ (Razor) と WebMatrix に関してよく寄せられる質問をいくつか紹介します。</span><span class="sxs-lookup"><span data-stu-id="f4cb7-108">This article lists some frequently asked questions about ASP.NET Web Pages (Razor) and WebMatrix.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="f4cb7-109">このチュートリアルで使用されているソフトウェアのバージョン</span><span class="sxs-lookup"><span data-stu-id="f4cb7-109">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="f4cb7-110">ASP.NET Web ページ (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="f4cb7-110">ASP.NET Web Pages (Razor) 3</span></span>
> - <span data-ttu-id="f4cb7-111">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="f4cb7-111">Visual Studio 2013</span></span>
> - <span data-ttu-id="f4cb7-112">WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="f4cb7-112">WebMatrix 3</span></span>
>   
> 
> <span data-ttu-id="f4cb7-113">このチュートリアルは、ASP.NET Web ページ2、WebMatrix 2、および Visual Studio 2012 でも動作します。</span><span class="sxs-lookup"><span data-stu-id="f4cb7-113">This tutorial also works with ASP.NET Web Pages 2, WebMatrix 2, and Visual Studio 2012.</span></span>

- [<span data-ttu-id="f4cb7-114">ASP.NET Web ページ、ASP.NET Web Forms、ASP.NET MVC の違いは何ですか。</span><span class="sxs-lookup"><span data-stu-id="f4cb7-114">What's the difference between ASP.NET Web Pages, ASP.NET Web Forms, and ASP.NET MVC?</span></span>](#Whats_the_difference_between_ASP.NET_Web_Pages,_ASP.NET_Web_Forms,_and_ASP.NET_MVC)
- [<span data-ttu-id="f4cb7-115">Web ページを操作するために WebMatrix が必要ですか。</span><span class="sxs-lookup"><span data-stu-id="f4cb7-115">Do I need WebMatrix in order to work with Web Pages?</span></span>](#Do_I_need_WebMatrix_in_order_to_work_with_Web_Pages)
- [<span data-ttu-id="f4cb7-116">Web ページページで ASP.NET Web フォームコントロールを使用できますか。</span><span class="sxs-lookup"><span data-stu-id="f4cb7-116">Can I use ASP.NET Web Forms controls on a Web Pages page?</span></span>](#Can_I_use_ASP.NET_Web_Forms_controls_on_a_Web_Pages_page)
- [<span data-ttu-id="f4cb7-117">WebMatrix を使用せずに ASP.NET Web ページサイトをデプロイすることはできますか。</span><span class="sxs-lookup"><span data-stu-id="f4cb7-117">Can I deploy an ASP.NET Web Pages site without using WebMatrix?</span></span>](#Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix)
- [<span data-ttu-id="f4cb7-118">ログインをサポートするには、WebSecurity ヘルパーを使用する必要がありますか。</span><span class="sxs-lookup"><span data-stu-id="f4cb7-118">Do I have to use the WebSecurity helper to support logins?</span></span>](#Do_I_have_to_use_the_WebSecurity_helper_to_support_logins)
- [<span data-ttu-id="f4cb7-119">HTML5 はサポート ASP.NET Web ページ。</span><span class="sxs-lookup"><span data-stu-id="f4cb7-119">Does ASP.NET Web Pages support HTML5?</span></span>](#Does_ASP.NET_Web_Pages_support_HTML5)
- [<span data-ttu-id="f4cb7-120">Web ページで JavaScript と jQuery を使用できますか。</span><span class="sxs-lookup"><span data-stu-id="f4cb7-120">Can I use JavaScript and jQuery with Web Pages?</span></span>](#Can_I_use_JavaScript_and_jQuery_with_Web_Pages)
- [<span data-ttu-id="f4cb7-121">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="f4cb7-121">Additional Resources</span></span>](#AdditionalResources)

<span data-ttu-id="f4cb7-122">エラーおよびその他の問題に関する質問については、 [ASP.NET Web ページ (Razor) のトラブルシューティングガイド](https://go.microsoft.com/fwlink/?LinkId=253001)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f4cb7-122">For questions about errors and other issues, see the [ASP.NET Web Pages (Razor) Troubleshooting Guide](https://go.microsoft.com/fwlink/?LinkId=253001).</span></span>

<a id="Whats_the_difference_between_ASP.NET_Web_Pages,_ASP.NET_Web_Forms,_and_ASP.NET_MVC"></a>
## <a name="whats-the-difference-between-aspnet-web-pages-aspnet-web-forms-and-aspnet-mvc"></a><span data-ttu-id="f4cb7-123">ASP.NET Web ページ、ASP.NET Web Forms、ASP.NET MVC の違いは何ですか。</span><span class="sxs-lookup"><span data-stu-id="f4cb7-123">What's the difference between ASP.NET Web Pages, ASP.NET Web Forms, and ASP.NET MVC?</span></span>

<span data-ttu-id="f4cb7-124">動的な web アプリケーションを作成するための ASP.NET テクノロジは3つあります。</span><span class="sxs-lookup"><span data-stu-id="f4cb7-124">All three are ASP.NET technologies for creating dynamic web applications:</span></span>

- <span data-ttu-id="f4cb7-125">ASP.NET Web ページは、HTML ページへの動的 (サーバー側) コードおよびデータベースアクセスの追加に焦点を当てており、シンプルで軽量な構文を特徴としています。</span><span class="sxs-lookup"><span data-stu-id="f4cb7-125">ASP.NET Web Pages focuses on adding dynamic (server-side) code and database access to HTML pages, and features simple and lightweight syntax.</span></span>
- <span data-ttu-id="f4cb7-126">ASP.NET Web フォームは、ページオブジェクトモデルと従来のウィンドウ型コントロール (ボタン、リストなど) に基づいています。</span><span class="sxs-lookup"><span data-stu-id="f4cb7-126">ASP.NET Web Forms is based on a page object model and traditional window-type controls (buttons, lists, etc.).</span></span> <span data-ttu-id="f4cb7-127">Web フォームでは、クライアントベース (Windows フォーム) 開発に携わっているユーザーにとって使い慣れたイベントベースのモデルを使用します。</span><span class="sxs-lookup"><span data-stu-id="f4cb7-127">Web Forms uses an event-based model that's familiar to those who've worked with client-based (Windows forms) development.</span></span>
- <span data-ttu-id="f4cb7-128">ASP.NET MVC では、ASP.NET のモデルビューコントローラーパターンが実装されています。</span><span class="sxs-lookup"><span data-stu-id="f4cb7-128">ASP.NET MVC implements the model-view-controller pattern for ASP.NET.</span></span> <span data-ttu-id="f4cb7-129">「懸念事項の分離」 (処理、データ、および UI レイヤー) に重点を置いています。</span><span class="sxs-lookup"><span data-stu-id="f4cb7-129">The emphasis is on "separation of concerns" (processing, data, and UI layers).</span></span>

<span data-ttu-id="f4cb7-130">3つすべてのフレームワークは完全にサポートされており、ASP.NET チームによる開発は継続されます。</span><span class="sxs-lookup"><span data-stu-id="f4cb7-130">All three frameworks are fully supported and continue to be developed by the ASP.NET team.</span></span> <span data-ttu-id="f4cb7-131">一般に、使用するフレームワークの選択は、ASP.NET の背景と経験によって異なります。</span><span class="sxs-lookup"><span data-stu-id="f4cb7-131">In general, the choice of which framework to use depends on your background and experience with ASP.NET.</span></span>

<span data-ttu-id="f4cb7-132">特に ASP.NET Web ページは、HTML を知っているユーザーがページにサーバー処理を追加するのを簡単にするように設計されています。</span><span class="sxs-lookup"><span data-stu-id="f4cb7-132">ASP.NET Web Pages in particular was designed to make it easy for people who already know HTML to add server processing to their pages.</span></span> <span data-ttu-id="f4cb7-133">これは、プログラミングを初めて使用する学生、趣味、一般ユーザーに適した選択肢です。</span><span class="sxs-lookup"><span data-stu-id="f4cb7-133">It's a good choice for students, hobbyists, people in general who are new to programming.</span></span> <span data-ttu-id="f4cb7-134">また、non-ASP.NET web テクノロジを経験している開発者にも適しています。</span><span class="sxs-lookup"><span data-stu-id="f4cb7-134">It can also be a good choice for developers who have experience with non-ASP.NET web technologies.</span></span>

<a id="Do_I_need_WebMatrix_in_order_to_work_with_Web_Pages"></a>
## <a name="do-i-need-webmatrix-in-order-to-work-with-web-pages"></a><span data-ttu-id="f4cb7-135">Web ページを操作するために WebMatrix が必要ですか。</span><span class="sxs-lookup"><span data-stu-id="f4cb7-135">Do I need WebMatrix in order to work with Web Pages?</span></span>

<span data-ttu-id="f4cb7-136">いいえ。</span><span class="sxs-lookup"><span data-stu-id="f4cb7-136">No.</span></span> <span data-ttu-id="f4cb7-137">WebMatrix はASP.NET Webページの統合開発環境としては推奨されなくなりました。</span><span class="sxs-lookup"><span data-stu-id="f4cb7-137">WebMatrix is no longer recommended as an integrated development environment for ASP.NET Web Pages.</span></span> <span data-ttu-id="f4cb7-138">[Visual Studio](program-asp-net-web-pages-in-visual-studio.md)または[Visual Studio Code](https://code.visualstudio.com/)を使用します。</span><span class="sxs-lookup"><span data-stu-id="f4cb7-138">Use [Visual Studio](program-asp-net-web-pages-in-visual-studio.md) or [Visual Studio Code](https://code.visualstudio.com/).</span></span>

<span data-ttu-id="f4cb7-139">Visual Studio も Visual Studio Code も使用しない場合は、 [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)を使用してコンポーネント製品を個別にインストールできます。</span><span class="sxs-lookup"><span data-stu-id="f4cb7-139">If you don't want to use either Visual Studio or Visual Studio Code, you can install the component products individually using [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx).</span></span> <span data-ttu-id="f4cb7-140">次の製品が必要です。</span><span class="sxs-lookup"><span data-stu-id="f4cb7-140">You need the following products:</span></span>

- <span data-ttu-id="f4cb7-141">Microsoft .NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="f4cb7-141">Microsoft .NET Framework 4.5</span></span>
- <span data-ttu-id="f4cb7-142">ASP.NET MVC 5 (ASP.NET Web ページ framework もインストールする)</span><span class="sxs-lookup"><span data-stu-id="f4cb7-142">ASP.NET MVC 5 (which installs the ASP.NET Web Pages framework as well)</span></span>
- <span data-ttu-id="f4cb7-143">IIS Express (web サーバー)</span><span class="sxs-lookup"><span data-stu-id="f4cb7-143">IIS Express (the web server)</span></span>
- <span data-ttu-id="f4cb7-144">Microsoft SQL Server Compact 4.0 (データベース)</span><span class="sxs-lookup"><span data-stu-id="f4cb7-144">Microsoft SQL Server Compact 4.0 (the database)</span></span>

<span data-ttu-id="f4cb7-145">テキストエディターを使用して、 *cshtml* (または*vbhtml*) ページを編集できます。</span><span class="sxs-lookup"><span data-stu-id="f4cb7-145">You can use a text editor to edit *.cshtml* (or *.vbhtml*) pages.</span></span>

<span data-ttu-id="f4cb7-146">ツールを使用せずに SQL Server Compact データベース ( *.sdf*ファイル) を管理することは少し難しくなります。</span><span class="sxs-lookup"><span data-stu-id="f4cb7-146">Managing SQL Server Compact databases (*.sdf* files) without a tool is a bit harder.</span></span> <span data-ttu-id="f4cb7-147">Visual Studio には、.sdf データベースを管理するためのツールが*あります*。</span><span class="sxs-lookup"><span data-stu-id="f4cb7-147">Visual Studio containds tools for managing *.sdf* databases.</span></span> <span data-ttu-id="f4cb7-148">コードで SQL コマンドを実行して、多くの SQL Server 管理タスクを実行することもできます。</span><span class="sxs-lookup"><span data-stu-id="f4cb7-148">You can also run SQL commands in code to perform many SQL Server management tasks.</span></span>

<span data-ttu-id="f4cb7-149">統合開発環境 (IDE) を使用せずに*cshtml*ページをテストするには、それらをライブサーバーに配置します。</span><span class="sxs-lookup"><span data-stu-id="f4cb7-149">To test *.cshtml* pages without using an integrated development environment (IDE), you can deploy them to a live server.</span></span> <span data-ttu-id="f4cb7-150">(「 [WebMatrix を使用せずに ASP.NET Web ページサイトをデプロイすることはできますか」を](#Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix)参照してください)。</span><span class="sxs-lookup"><span data-stu-id="f4cb7-150">(See [Can I deploy an ASP.NET Web Pages site without using WebMatrix?](#Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix))</span></span>

### <a name="running-iis-express-without-using-an-ide"></a><span data-ttu-id="f4cb7-151">IDE を使用せずに IIS Express を実行する</span><span class="sxs-lookup"><span data-stu-id="f4cb7-151">Running IIS Express without using an IDE</span></span>

<span data-ttu-id="f4cb7-152">IIS Express を web サーバーとしてコンピューターにインストールする場合は、それを使用してページをテストすることができます。</span><span class="sxs-lookup"><span data-stu-id="f4cb7-152">If you install IIS Express on your computer as a web server, you can use that to test the pages.</span></span> <span data-ttu-id="f4cb7-153">コマンドラインから IIS Express を実行して、特定のポート番号に関連付けることができます。</span><span class="sxs-lookup"><span data-stu-id="f4cb7-153">You can run IIS Express from the command line and associate it with a specific port number.</span></span> <span data-ttu-id="f4cb7-154">次に、ブラウザーで*cshtml*ファイルを要求するときに、そのポートを指定します。</span><span class="sxs-lookup"><span data-stu-id="f4cb7-154">You then specify that port when you request *.cshtml* files in your browser.</span></span>

<span data-ttu-id="f4cb7-155">Windows で、管理者特権でコマンドプロンプトを開き、 *C:\Program Files\IIS Express*に変更します。</span><span class="sxs-lookup"><span data-stu-id="f4cb7-155">In Windows, open a command prompt with administrator privileges and change to *C:\Program Files\IIS Express.*</span></span> <span data-ttu-id="f4cb7-156">(64 ビットシステムの場合は、 *C:\Program files (x86) \ IIS Express*というフォルダーを使用します。次に、サイトへの実際のパスを使用して、次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="f4cb7-156">(For 64-bit systems, use the folder *C:\Program Files (x86)\IIS Express.)* Then enter the following command, using the actual path to your site:</span></span>

`iisexpress.exe /port:35896 /path:C:\BasicWebSite`

<span data-ttu-id="f4cb7-157">他のプロセスによって既に予約されていない任意のポート番号を使用できます。</span><span class="sxs-lookup"><span data-stu-id="f4cb7-157">You can use any port number that isn't already reserved by some other process.</span></span> <span data-ttu-id="f4cb7-158">(通常、1024を超えるポート番号は無料です)。`path` 値には、 *cshtml*ファイルが格納されている web サイトフォルダーのパスを使用します。</span><span class="sxs-lookup"><span data-stu-id="f4cb7-158">(Port numbers above 1024 are typically free.) For the `path` value, use the path of the website folder where the *.cshtml* files are.</span></span>

<span data-ttu-id="f4cb7-159">このコマンドを実行してページを提供するように IIS Express を設定した後、ブラウザーを開いて、 *cshtml*ファイルを参照できます。</span><span class="sxs-lookup"><span data-stu-id="f4cb7-159">After you run this command to set up IIS Express to serve your pages, you can open a browser and browse to a *.cshtml* file.</span></span> <span data-ttu-id="f4cb7-160">次のような URL を使用します。</span><span class="sxs-lookup"><span data-stu-id="f4cb7-160">Use a URL like the following:</span></span>

`http://localhost:35896/default.cshtml`

<span data-ttu-id="f4cb7-161">IIS Express のコマンドラインオプションについては、コマンドラインで「`iisexpress.exe /?`」と入力してください。</span><span class="sxs-lookup"><span data-stu-id="f4cb7-161">For help with IIS Express command line options, enter `iisexpress.exe /?` at the command line.</span></span>

<a id="Can_I_use_ASP.NET_Web_Forms_controls_on_a_Web_Pages_page"></a>
## <a name="can-i-use-aspnet-web-forms-controls-on-a-web-pages-page"></a><span data-ttu-id="f4cb7-162">Web ページページで ASP.NET Web フォームコントロールを使用できますか。</span><span class="sxs-lookup"><span data-stu-id="f4cb7-162">Can I use ASP.NET Web Forms controls on a Web Pages page?</span></span>

<span data-ttu-id="f4cb7-163">いいえ。</span><span class="sxs-lookup"><span data-stu-id="f4cb7-163">No.</span></span> <span data-ttu-id="f4cb7-164">[CheckBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.checkbox)コントロール、[検証コントロール](https://msdn.microsoft.com/library/bwd43d0x)、 [GridView](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview)コントロールなどの Web フォームコントロールは、web フォームページ ( *.aspx*ファイル) でのみ機能します。</span><span class="sxs-lookup"><span data-stu-id="f4cb7-164">Web Forms controls like the [CheckBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.checkbox) control, the [validation controls](https://msdn.microsoft.com/library/bwd43d0x), and the [GridView](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview) control only work in Web Forms pages (*.aspx* files).</span></span> <span data-ttu-id="f4cb7-165">これらのコントロールには、Web フォームページフレームワークが必要です。</span><span class="sxs-lookup"><span data-stu-id="f4cb7-165">These controls require the Web Forms page framework.</span></span>

<a id="Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix"></a>
## <a name="can-i-deploy-an-aspnet-web-pages-site-without-using-webmatrix"></a><span data-ttu-id="f4cb7-166">WebMatrix を使用せずに ASP.NET Web ページサイトをデプロイすることはできますか。</span><span class="sxs-lookup"><span data-stu-id="f4cb7-166">Can I deploy an ASP.NET Web Pages site without using WebMatrix?</span></span>

<span data-ttu-id="f4cb7-167">はい。</span><span class="sxs-lookup"><span data-stu-id="f4cb7-167">Yes.</span></span> <span data-ttu-id="f4cb7-168">Web サイトファイルをサーバーに手動でコピーできます (通常は FTP を使用します)。</span><span class="sxs-lookup"><span data-stu-id="f4cb7-168">You can manually copy website files to a server (typically by using FTP).</span></span> <span data-ttu-id="f4cb7-169">手動コピーを実行する場合は、SQL Server Compact (データベース) をサポートするファイルもコピーする必要があります。</span><span class="sxs-lookup"><span data-stu-id="f4cb7-169">If you perform a manual copy, you also have to copy the files that support SQL Server Compact (the database).</span></span> <span data-ttu-id="f4cb7-170">詳細については、「[ツールを使用しない Web ページアプリケーションのデプロイ](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2317)」のブログ記事を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f4cb7-170">For details, see the blog entry [Deploying Web Pages applications without a tool](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2317).</span></span>

<a id="Do_I_have_to_use_the_WebSecurity_helper_to_support_logins"></a>
## <a name="do-i-have-to-use-the-websecurity-helper-to-support-logins"></a><span data-ttu-id="f4cb7-171">ログインをサポートするには、WebSecurity ヘルパーを使用する必要がありますか。</span><span class="sxs-lookup"><span data-stu-id="f4cb7-171">Do I have to use the WebSecurity helper to support logins?</span></span>

<span data-ttu-id="f4cb7-172">いいえ。</span><span class="sxs-lookup"><span data-stu-id="f4cb7-172">No.</span></span> <span data-ttu-id="f4cb7-173">ASP.NET Web ページの一部である `SimpleMembership` プロバイダーは、1つのオプションです。</span><span class="sxs-lookup"><span data-stu-id="f4cb7-173">The `SimpleMembership` provider that is part of ASP.NET Web Pages is one option.</span></span> <span data-ttu-id="f4cb7-174">ASP.NET の一部である (Web フォームでの操作に使用する可能性がある) セキュリティプロバイダーも使用できます。</span><span class="sxs-lookup"><span data-stu-id="f4cb7-174">The security providers that are part of ASP.NET (that you might be used to working with in Web Forms) are also available.</span></span> <span data-ttu-id="f4cb7-175">たとえば、Web フォームの場合と同じように ASP.NET Web ページでフォーム認証を使用できます。</span><span class="sxs-lookup"><span data-stu-id="f4cb7-175">For example, you can use forms authentication in ASP.NET Web Pages just as you would in Web Forms.</span></span> <span data-ttu-id="f4cb7-176">フォーム認証を使用する方法の例については、「 [.Net を使用C#して ASP.NET アプリケーションでフォームベースの認証を実装する方法](https://support.microsoft.com/kb/301240)Microsoft サポート」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f4cb7-176">For one example of how to use forms authentication, see the Microsoft Support article [How To Implement Forms-Based Authentication in Your ASP.NET Application by Using C#.NET](https://support.microsoft.com/kb/301240).</span></span> <span data-ttu-id="f4cb7-177">簡単な例をダウンロードするには、「 [ASP.NET バージョンのログイン &amp; パスワード](http://www.codeguru.com/csharp/.net/net_asp/scripting/article.php/c19295/ASPNET-version-of-Login--Password.htm)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f4cb7-177">To download a simple example, see [ASP.NET version of "Login &amp; Password](http://www.codeguru.com/csharp/.net/net_asp/scripting/article.php/c19295/ASPNET-version-of-Login--Password.htm).</span></span>

<span data-ttu-id="f4cb7-178">Windows 認証の使用方法の詳細については、 [ASP.NET Web ページで windows 認証を使用](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2298)するブログの投稿を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f4cb7-178">For information about how to use Windows authentication, see the blog post [Using Windows authentication in ASP.NET Web Pages](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2298).</span></span>

<a id="Does_ASP.NET_Web_Pages_support_HTML5"></a>
## <a name="does-aspnet-web-pages-support-html5"></a><span data-ttu-id="f4cb7-179">HTML5 はサポート ASP.NET Web ページ。</span><span class="sxs-lookup"><span data-stu-id="f4cb7-179">Does ASP.NET Web Pages support HTML5?</span></span>

<span data-ttu-id="f4cb7-180">はい。</span><span class="sxs-lookup"><span data-stu-id="f4cb7-180">Yes.</span></span> <span data-ttu-id="f4cb7-181">ASP.NET Web ページ (*cshtml*または*vbhtml*ページ) を使用して作成したページは、ページが表示される前に、サーバーで実行されるコードも含む HTML ページです。</span><span class="sxs-lookup"><span data-stu-id="f4cb7-181">The pages you create with ASP.NET Web Pages (*.cshtml* or *.vbhtml* pages) are essentially HTML pages that also contain code that runs on the server, before the page is rendered.</span></span> <span data-ttu-id="f4cb7-182">ユーザーのブラウザーで HTML5 がサポートされている限り、 *cshtml*または*VBHTML*ページで html5 要素を使用できます。</span><span class="sxs-lookup"><span data-stu-id="f4cb7-182">As long as the user's browser supports HTML5, you can use HTML5 elements in a *.cshtml* or *.vbhtml* page.</span></span>

<a id="Can_I_use_JavaScript_and_jQuery_with_Web_Pages"></a>
## <a name="can-i-use-javascript-and-jquery-with-web-pages"></a><span data-ttu-id="f4cb7-183">Web ページで JavaScript と jQuery を使用できますか。</span><span class="sxs-lookup"><span data-stu-id="f4cb7-183">Can I use JavaScript and jQuery with Web Pages?</span></span>

<span data-ttu-id="f4cb7-184">そして、</span><span class="sxs-lookup"><span data-stu-id="f4cb7-184">Absolutely.</span></span> <span data-ttu-id="f4cb7-185">ASP.NET Web ページ (*cshtml*または*vbhtml*ページ) で作成するページは、サーバーコードが含まれた HTML ページにすぎません。</span><span class="sxs-lookup"><span data-stu-id="f4cb7-185">The pages you create with ASP.NET Web Pages (*.cshtml* or *.vbhtml* pages) are just HTML pages with server code in them.</span></span> <span data-ttu-id="f4cb7-186">そのため、JavaScript または jQuery を使用して通常の HTML ページで実行できることは、すべて、 *cshtml*または*vbhtml*ページで行うことができます。</span><span class="sxs-lookup"><span data-stu-id="f4cb7-186">Therefore, anything you can do in a normal HTML page by using JavaScript or jQuery you can also do in a *.cshtml* or *.vbhtml* page.</span></span>

<span data-ttu-id="f4cb7-187">WebMatrix の**スターターサイト**テンプレートには、さまざまな jQuery ライブラリが含まれています。</span><span class="sxs-lookup"><span data-stu-id="f4cb7-187">The **Starter Site** template in WebMatrix contains a number of jQuery libraries.</span></span> <span data-ttu-id="f4cb7-188">そのテンプレートを使用してサイトを作成した場合、 *Scripts*フォルダーには jquery のコアライブラリ (*jquery-1.6.2)* と、jquery validation (*jquery*など) のライブラリが含まれています。</span><span class="sxs-lookup"><span data-stu-id="f4cb7-188">If you create a site by using that template, the *Scripts* folder contains a jQuery core library (*jquery-1.6.2.js)* and libraries for jQuery validation (*jquery.validate.js*, etc.).</span></span>

<span data-ttu-id="f4cb7-189">次に、ASP.NET Web ページで jQuery を使用する方法を説明するブログ記事をいくつか紹介します。</span><span class="sxs-lookup"><span data-stu-id="f4cb7-189">Here are some blog posts that illustrate ways to use jQuery with ASP.NET Web Pages:</span></span>

- <span data-ttu-id="f4cb7-190">[WebMatrix を使用した ASP.NET Web ページへの jQuery の追加 (](http://rachelappel.com/jquery/adding-jquery-goodness-to-asp-net-web-pages-using-webmatrix/) Rachel appel)</span><span class="sxs-lookup"><span data-stu-id="f4cb7-190">[Adding jQuery Goodness to ASP.NET Web Pages using WebMatrix](http://rachelappel.com/jquery/adding-jquery-goodness-to-asp-net-web-pages-using-webmatrix/) by Rachel Appel</span></span>
- <span data-ttu-id="f4cb7-191">[5 分: WebMatrix + JQUERY UI + json + jquery templates](http://joeriks.com/2011/01/30/5-min-webmatrix-jquery-ui-json-jquery-templates/) By Jonas Eriksson</span><span class="sxs-lookup"><span data-stu-id="f4cb7-191">[5 min: WebMatrix + jQuery UI + json + jQuery templates](http://joeriks.com/2011/01/30/5-min-webmatrix-jquery-ui-json-jquery-templates/) by Jonas Eriksson</span></span>
- <span data-ttu-id="f4cb7-192">Mike Brind による[WebMatrix と JQuery Forms](http://mikesdotnetting.com/Article/155/WebMatrix-And-jQuery-Forms)</span><span class="sxs-lookup"><span data-stu-id="f4cb7-192">[WebMatrix And jQuery Forms](http://mikesdotnetting.com/Article/155/WebMatrix-And-jQuery-Forms) by Mike Brind</span></span>

<a id="AdditionalResources"></a>
## <a name="additional-resources"></a><span data-ttu-id="f4cb7-193">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="f4cb7-193">Additional Resources</span></span>

[<span data-ttu-id="f4cb7-194">ASP.NET Web ページ (Razor) トラブルシューティング ガイド</span><span class="sxs-lookup"><span data-stu-id="f4cb7-194">ASP.NET Web Pages (Razor) Troubleshooting Guide</span></span>](https://go.microsoft.com/fwlink/?LinkId=253001)

<span data-ttu-id="f4cb7-195">ASP.NET web サイトの[WebMatrix と ASP.NET Web ページフォーラム](https://forums.asp.net/1224.aspx/1?WebMatrix)</span><span class="sxs-lookup"><span data-stu-id="f4cb7-195">[WebMatrix and ASP.NET Web Pages forum](https://forums.asp.net/1224.aspx/1?WebMatrix) on the ASP.NET website</span></span>
