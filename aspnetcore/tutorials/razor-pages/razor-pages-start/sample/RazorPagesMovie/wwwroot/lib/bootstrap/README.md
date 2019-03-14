---
ms.openlocfilehash: f60f934934ae9e16bbd1174959d99aecdbb5833d
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57040949"
---
--

<span data-ttu-id="bdbd1-101">[![Slack](https://bootstrap-slack.herokuapp.com/badge.svg)](https://bootstrap-slack.herokuapp.com)
![Bower バージョン](https://img.shields.io/bower/v/bootstrap.svg)
[![npm バージョン](https://img.shields.io/npm/v/bootstrap.svg)](https://www.npmjs.com/package/bootstrap)
[![ビルドの状態](https://img.shields.io/travis/twbs/bootstrap/master.svg)](https://travis-ci.org/twbs/bootstrap)
[ ![devDependency の状態](https://img.shields.io/david/dev/twbs/bootstrap.svg)](https://david-dm.org/twbs/bootstrap#info=devDependencies)
[![NuGet](https://img.shields.io/nuget/v/bootstrap.svg)](https://www.nuget.org/packages/Bootstrap)
[![Selenium テストの状態](https://saucelabs.com/browser-matrix/bootstrap.svg)](https://saucelabs.com/u/bootstrap)</span><span class="sxs-lookup"><span data-stu-id="bdbd1-101">[![Slack](https://bootstrap-slack.herokuapp.com/badge.svg)](https://bootstrap-slack.herokuapp.com)
![Bower version](https://img.shields.io/bower/v/bootstrap.svg)
[![npm version](https://img.shields.io/npm/v/bootstrap.svg)](https://www.npmjs.com/package/bootstrap)
[![Build Status](https://img.shields.io/travis/twbs/bootstrap/master.svg)](https://travis-ci.org/twbs/bootstrap)
[![devDependency Status](https://img.shields.io/david/dev/twbs/bootstrap.svg)](https://david-dm.org/twbs/bootstrap#info=devDependencies)
[![NuGet](https://img.shields.io/nuget/v/bootstrap.svg)](https://www.nuget.org/packages/Bootstrap)
[![Selenium Test Status](https://saucelabs.com/browser-matrix/bootstrap.svg)](https://saucelabs.com/u/bootstrap)</span></span>

<span data-ttu-id="bdbd1-102">Bootstrap は、Web 開発を高速かつ簡単に行うことができるスムーズで直感的な高性能フロントエンド フレームワークであり、[Mark Otto](https://twitter.com/mdo) および [Jacob Thornton](https://twitter.com/fat) が作成し、[コア チーム](https://github.com/orgs/twbs/people)とコミュニティの温かいご支援と協力によって管理されています。</span><span class="sxs-lookup"><span data-stu-id="bdbd1-102">Bootstrap is a sleek, intuitive, and powerful front-end framework for faster and easier web development, created by [Mark Otto](https://twitter.com/mdo) and [Jacob Thornton](https://twitter.com/fat), and maintained by the [core team](https://github.com/orgs/twbs/people) with the massive support and involvement of the community.</span></span>

<span data-ttu-id="bdbd1-103">最初に、<http://getbootstrap.com> をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="bdbd1-103">To get started, check out <http://getbootstrap.com>!</span></span>


## <a name="table-of-contents"></a><span data-ttu-id="bdbd1-104">目次</span><span class="sxs-lookup"><span data-stu-id="bdbd1-104">Table of contents</span></span>

* [<span data-ttu-id="bdbd1-105">クイック スタート</span><span class="sxs-lookup"><span data-stu-id="bdbd1-105">Quick start</span></span>](#quick-start)
* [<span data-ttu-id="bdbd1-106">バグおよび機能に関する要望</span><span class="sxs-lookup"><span data-stu-id="bdbd1-106">Bugs and feature requests</span></span>](#bugs-and-feature-requests)
* [<span data-ttu-id="bdbd1-107">ドキュメント</span><span class="sxs-lookup"><span data-stu-id="bdbd1-107">Documentation</span></span>](#documentation)
* [<span data-ttu-id="bdbd1-108">コントリビューション</span><span class="sxs-lookup"><span data-stu-id="bdbd1-108">Contributing</span></span>](#contributing)
* [<span data-ttu-id="bdbd1-109">Community</span><span class="sxs-lookup"><span data-stu-id="bdbd1-109">Community</span></span>](#community)
* [<span data-ttu-id="bdbd1-110">バージョン管理</span><span class="sxs-lookup"><span data-stu-id="bdbd1-110">Versioning</span></span>](#versioning)
* [<span data-ttu-id="bdbd1-111">作成者</span><span class="sxs-lookup"><span data-stu-id="bdbd1-111">Creators</span></span>](#creators)
* [<span data-ttu-id="bdbd1-112">著作権およびライセンス</span><span class="sxs-lookup"><span data-stu-id="bdbd1-112">Copyright and license</span></span>](#copyright-and-license)


## <a name="quick-start"></a><span data-ttu-id="bdbd1-113">クイック スタート</span><span class="sxs-lookup"><span data-stu-id="bdbd1-113">Quick start</span></span>

<span data-ttu-id="bdbd1-114">クイック スタートの選択肢は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="bdbd1-114">Several quick start options are available:</span></span>

* <span data-ttu-id="bdbd1-115">[最新のリリースをダウンロードする](https://github.com/twbs/bootstrap/archive/v3.3.7.zip).</span><span class="sxs-lookup"><span data-stu-id="bdbd1-115">[Download the latest release](https://github.com/twbs/bootstrap/archive/v3.3.7.zip).</span></span>
* <span data-ttu-id="bdbd1-116">リポジトリを複製する: `git clone https://github.com/twbs/bootstrap.git`</span><span class="sxs-lookup"><span data-stu-id="bdbd1-116">Clone the repo: `git clone https://github.com/twbs/bootstrap.git`.</span></span>
* <span data-ttu-id="bdbd1-117">[Bower](http://bower.io) を使用してインストールする: `bower install bootstrap`</span><span class="sxs-lookup"><span data-stu-id="bdbd1-117">Install with [Bower](http://bower.io): `bower install bootstrap`.</span></span>
* <span data-ttu-id="bdbd1-118">[npm](https://www.npmjs.com) を使用してインストールする: `npm install bootstrap@3`</span><span class="sxs-lookup"><span data-stu-id="bdbd1-118">Install with [npm](https://www.npmjs.com): `npm install bootstrap@3`.</span></span>
* <span data-ttu-id="bdbd1-119">[Meteor](https://www.meteor.com) を使用してインストールする: `meteor add twbs:bootstrap`</span><span class="sxs-lookup"><span data-stu-id="bdbd1-119">Install with [Meteor](https://www.meteor.com): `meteor add twbs:bootstrap`.</span></span>
* <span data-ttu-id="bdbd1-120">[Composer](https://getcomposer.org) を使用してインストールする: `composer require twbs/bootstrap`</span><span class="sxs-lookup"><span data-stu-id="bdbd1-120">Install with [Composer](https://getcomposer.org): `composer require twbs/bootstrap`.</span></span>

<span data-ttu-id="bdbd1-121">このフレームワークの内容、テンプレート、サンプルなどについては、[使用開始](http://getbootstrap.com/getting-started/)に関するページを参照してください。</span><span class="sxs-lookup"><span data-stu-id="bdbd1-121">Read the [Getting started page](http://getbootstrap.com/getting-started/) for information on the framework contents, templates and examples, and more.</span></span>

### <a name="whats-included"></a><span data-ttu-id="bdbd1-122">内容</span><span class="sxs-lookup"><span data-stu-id="bdbd1-122">What's included</span></span>

<span data-ttu-id="bdbd1-123">このダウンロードには、共通アセットを論理的にグループ分けした以下のディレクトリとファイルが含まれており、コンパイル済みのバリエーションおよび縮小版のバリエーションが用意されています。</span><span class="sxs-lookup"><span data-stu-id="bdbd1-123">Within the download you'll find the following directories and files, logically grouping common assets and providing both compiled and minified variations.</span></span> <span data-ttu-id="bdbd1-124">内容は以下のとおりです。</span><span class="sxs-lookup"><span data-stu-id="bdbd1-124">You'll see something like this:</span></span>

```
bootstrap/
├── css/
│   ├── bootstrap.css
│   ├── bootstrap.css.map
│   ├── bootstrap.min.css
│   ├── bootstrap.min.css.map
│   ├── bootstrap-theme.css
│   ├── bootstrap-theme.css.map
│   ├── bootstrap-theme.min.css
│   └── bootstrap-theme.min.css.map
├── js/
│   ├── bootstrap.js
│   └── bootstrap.min.js
└── fonts/
    ├── glyphicons-halflings-regular.eot
    ├── glyphicons-halflings-regular.svg
    ├── glyphicons-halflings-regular.ttf
    ├── glyphicons-halflings-regular.woff
    └── glyphicons-halflings-regular.woff2
```

<span data-ttu-id="bdbd1-125">コンパイル済みの CSS と JS (`bootstrap.*`)、およびコンパイル済みの縮小版 CSS と JS (`bootstrap.min.*`) が含まれています。</span><span class="sxs-lookup"><span data-stu-id="bdbd1-125">We provide compiled CSS and JS (`bootstrap.*`), as well as compiled and minified CSS and JS (`bootstrap.min.*`).</span></span> <span data-ttu-id="bdbd1-126">一部のブラウザーの開発者ツール用に、CSS [ソース マップ](https://developer.chrome.com/devtools/docs/css-preprocessors) (`bootstrap.*.map`) も用意されています。</span><span class="sxs-lookup"><span data-stu-id="bdbd1-126">CSS [source maps](https://developer.chrome.com/devtools/docs/css-preprocessors) (`bootstrap.*.map`) are available for use with certain browsers' developer tools.</span></span> <span data-ttu-id="bdbd1-127">オプションの Bootstrap テーマである Glyphicons のフォントも含まれています。</span><span class="sxs-lookup"><span data-stu-id="bdbd1-127">Fonts from Glyphicons are included, as is the optional Bootstrap theme.</span></span>


## <a name="bugs-and-feature-requests"></a><span data-ttu-id="bdbd1-128">バグおよび機能に関する要望</span><span class="sxs-lookup"><span data-stu-id="bdbd1-128">Bugs and feature requests</span></span>

<span data-ttu-id="bdbd1-129">バグが発生した場合、または機能に関する要望がある場合は、</span><span class="sxs-lookup"><span data-stu-id="bdbd1-129">Have a bug or a feature request?</span></span> <span data-ttu-id="bdbd1-130">まず [issue のガイドライン](https://github.com/twbs/bootstrap/blob/master/CONTRIBUTING.md#using-the-issue-tracker)をご覧になり、既存の issue および解決済みの issue を検索してください。</span><span class="sxs-lookup"><span data-stu-id="bdbd1-130">Please first read the [issue guidelines](https://github.com/twbs/bootstrap/blob/master/CONTRIBUTING.md#using-the-issue-tracker) and search for existing and closed issues.</span></span> <span data-ttu-id="bdbd1-131">それでも問題が解決されない場合、またはアイデアが反映されていない場合は、[新しい issue を開始してください](https://github.com/twbs/bootstrap/issues/new)。</span><span class="sxs-lookup"><span data-stu-id="bdbd1-131">If your problem or idea isn't addressed yet, [please open a new issue](https://github.com/twbs/bootstrap/issues/new).</span></span>

<span data-ttu-id="bdbd1-132">なお、Bootstrap バージョン 3 は現在メンテナンス モードであり新機能の追加は行われていないため、**機能に関する要望については [Bootstrap バージョン 4](https://github.com/twbs/bootstrap/tree/v4-dev)** にお寄せください。</span><span class="sxs-lookup"><span data-stu-id="bdbd1-132">Note that **feature requests must target [Bootstrap v4](https://github.com/twbs/bootstrap/tree/v4-dev),** because Bootstrap v3 is now in maintenance mode and is closed off to new features.</span></span> <span data-ttu-id="bdbd1-133">Bootstrap バージョン 4 の開発に専念するためこのようにしていることをご了承ください。</span><span class="sxs-lookup"><span data-stu-id="bdbd1-133">This is so that we can focus our efforts on Bootstrap v4.</span></span>


## <a name="documentation"></a><span data-ttu-id="bdbd1-134">ドキュメント</span><span class="sxs-lookup"><span data-stu-id="bdbd1-134">Documentation</span></span>

<span data-ttu-id="bdbd1-135">このリポジトリのルート ディレクトリに含まれる Bootstrap のドキュメントは、[Jekyll](http://jekyllrb.com) で作成され、GitHub のページ (<http://getbootstrap.com>) でホストされ公開されています。</span><span class="sxs-lookup"><span data-stu-id="bdbd1-135">Bootstrap's documentation, included in this repo in the root directory, is built with [Jekyll](http://jekyllrb.com) and publicly hosted on GitHub Pages at <http://getbootstrap.com>.</span></span> <span data-ttu-id="bdbd1-136">ドキュメントはローカルで確認することもできます。</span><span class="sxs-lookup"><span data-stu-id="bdbd1-136">The docs may also be run locally.</span></span>

### <a name="running-documentation-locally"></a><span data-ttu-id="bdbd1-137">ドキュメントをローカルで確認する</span><span class="sxs-lookup"><span data-stu-id="bdbd1-137">Running documentation locally</span></span>

1. <span data-ttu-id="bdbd1-138">必要に応じて、`bundle install` を使用して、[Jekyll](http://jekyllrb.com/docs/installation) とその他の Ruby の依存パッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="bdbd1-138">If necessary, [install Jekyll](http://jekyllrb.com/docs/installation) and other Ruby dependencies with `bundle install`.</span></span>
   <span data-ttu-id="bdbd1-139">**Windows のユーザーに対する注意:** 読み取り[この非公式ガイド](http://jekyll-windows.juthilo.com/)を問題なく稼働して Jekyll を取得します。</span><span class="sxs-lookup"><span data-stu-id="bdbd1-139">**Note for Windows users:** Read [this unofficial guide](http://jekyll-windows.juthilo.com/) to get Jekyll up and running without problems.</span></span>
2. <span data-ttu-id="bdbd1-140">コマンド ラインで、ルートの `/bootstrap` ディレクトリから `bundle exec jekyll serve` を実行します。</span><span class="sxs-lookup"><span data-stu-id="bdbd1-140">From the root `/bootstrap` directory, run `bundle exec jekyll serve` in the command line.</span></span>
4. <span data-ttu-id="bdbd1-141">ブラウザーで `http://localhost:9001` にアクセスします。</span><span class="sxs-lookup"><span data-stu-id="bdbd1-141">Open `http://localhost:9001` in your browser, and voilà.</span></span>

<span data-ttu-id="bdbd1-142">Jekyll の使用方法の詳細については、Jekyll の[ドキュメント](http://jekyllrb.com/docs/home/)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="bdbd1-142">Learn more about using Jekyll by reading its [documentation](http://jekyllrb.com/docs/home/).</span></span>

### <a name="documentation-for-previous-releases"></a><span data-ttu-id="bdbd1-143">以前のリリースのドキュメント</span><span class="sxs-lookup"><span data-stu-id="bdbd1-143">Documentation for previous releases</span></span>

<span data-ttu-id="bdbd1-144">バージョン 2.3.2 のドキュメントは、各ユーザーの Bootstrap 3 への切り替えが行われている間は、当面 <http://getbootstrap.com/2.3.2/> で公開されています。</span><span class="sxs-lookup"><span data-stu-id="bdbd1-144">Documentation for v2.3.2 has been made available for the time being at <http://getbootstrap.com/2.3.2/> while folks transition to Bootstrap 3.</span></span>

<span data-ttu-id="bdbd1-145">[以前のリリース](https://github.com/twbs/bootstrap/releases)およびドキュメントもダウンロード可能です。</span><span class="sxs-lookup"><span data-stu-id="bdbd1-145">[Previous releases](https://github.com/twbs/bootstrap/releases) and their documentation are also available for download.</span></span>


## <a name="contributing"></a><span data-ttu-id="bdbd1-146">コントリビューション</span><span class="sxs-lookup"><span data-stu-id="bdbd1-146">Contributing</span></span>

<span data-ttu-id="bdbd1-147">[コントリビューションに関するガイドライン](https://github.com/twbs/bootstrap/blob/master/CONTRIBUTING.md)のページをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="bdbd1-147">Please read through our [contributing guidelines](https://github.com/twbs/bootstrap/blob/master/CONTRIBUTING.md).</span></span> <span data-ttu-id="bdbd1-148">issue の作成方法、コード作成規則、および開発に関する注意事項について説明しています。</span><span class="sxs-lookup"><span data-stu-id="bdbd1-148">Included are directions for opening issues, coding standards, and notes on development.</span></span>

<span data-ttu-id="bdbd1-149">また、pull request に JavaScript パッチまたは機能を含める場合は、[関連する単体テスト](https://github.com/twbs/bootstrap/tree/master/js/tests)も含めてください。</span><span class="sxs-lookup"><span data-stu-id="bdbd1-149">Moreover, if your pull request contains JavaScript patches or features, you must include [relevant unit tests](https://github.com/twbs/bootstrap/tree/master/js/tests).</span></span> <span data-ttu-id="bdbd1-150">HTML および CSS はすべて、[コード ガイド](https://github.com/mdo/code-guide) ([Mark Otto](https://github.com/mdo) 作成) に準拠している必要があります。</span><span class="sxs-lookup"><span data-stu-id="bdbd1-150">All HTML and CSS should conform to the [Code Guide](https://github.com/mdo/code-guide), maintained by [Mark Otto](https://github.com/mdo).</span></span>

<span data-ttu-id="bdbd1-151">**現在、Bootstrap バージョン 3 への新機能の追加は終了しています。**</span><span class="sxs-lookup"><span data-stu-id="bdbd1-151">**Bootstrap v3 is now closed off to new features.**</span></span> <span data-ttu-id="bdbd1-152">今後のフレームワークである [Bootstrap バージョン 4](https://github.com/twbs/bootstrap/tree/v4-dev) に専念するため、こちらはメンテナンス モードとなっています。</span><span class="sxs-lookup"><span data-stu-id="bdbd1-152">It has gone into maintenance mode so that we can focus our efforts on [Bootstrap v4](https://github.com/twbs/bootstrap/tree/v4-dev), the future of the framework.</span></span> <span data-ttu-id="bdbd1-153">バグの修正ではなく新機能の追加を行う pull requests のターゲットは、[Bootstrap バージョン 4 (`v4-dev` git ブランチ)](https://github.com/twbs/bootstrap/tree/v4-dev) としてください。</span><span class="sxs-lookup"><span data-stu-id="bdbd1-153">Pull requests which add new features (rather than fix bugs) should target [Bootstrap v4 (the `v4-dev` git branch)](https://github.com/twbs/bootstrap/tree/v4-dev) instead.</span></span>

<span data-ttu-id="bdbd1-154">[エディターの環境設定](https://github.com/twbs/bootstrap/blob/master/.editorconfig)に関するページでは、一般的なテキスト エディターで簡単に使用できるエディターの基本設定が公開されています。</span><span class="sxs-lookup"><span data-stu-id="bdbd1-154">Editor preferences are available in the [editor config](https://github.com/twbs/bootstrap/blob/master/.editorconfig) for easy use in common text editors.</span></span> <span data-ttu-id="bdbd1-155"><http://editorconfig.org> で詳細を確認し、プラグインをダウンロードしてください。</span><span class="sxs-lookup"><span data-stu-id="bdbd1-155">Read more and download plugins at <http://editorconfig.org>.</span></span>


## <a name="community"></a><span data-ttu-id="bdbd1-156">コミュニティ</span><span class="sxs-lookup"><span data-stu-id="bdbd1-156">Community</span></span>

<span data-ttu-id="bdbd1-157">Bootstrap の開発の最新状況の確認、およびプロジェクト管理者およびコミュニティ メンバーとのやり取りを行うことができます。</span><span class="sxs-lookup"><span data-stu-id="bdbd1-157">Get updates on Bootstrap's development and chat with the project maintainers and community members.</span></span>

* <span data-ttu-id="bdbd1-158">[Twitter で @getbootstrap](https://twitter.com/getbootstrap) をフォローしてください。</span><span class="sxs-lookup"><span data-stu-id="bdbd1-158">Follow [@getbootstrap on Twitter](https://twitter.com/getbootstrap).</span></span>
* <span data-ttu-id="bdbd1-159">[Bootstrap の公式ブログ](http://blog.getbootstrap.com)をご覧になり、購読してください。</span><span class="sxs-lookup"><span data-stu-id="bdbd1-159">Read and subscribe to [The Official Bootstrap Blog](http://blog.getbootstrap.com).</span></span>
* <span data-ttu-id="bdbd1-160">[公式 のSlack ルーム](https://bootstrap-slack.herokuapp.com)に参加してください。</span><span class="sxs-lookup"><span data-stu-id="bdbd1-160">Join [the official Slack room](https://bootstrap-slack.herokuapp.com).</span></span>
* <span data-ttu-id="bdbd1-161">IRC で Bootstrap ユーザーとチャットしてください。</span><span class="sxs-lookup"><span data-stu-id="bdbd1-161">Chat with fellow Bootstrappers in IRC.</span></span> <span data-ttu-id="bdbd1-162">`irc.freenode.net` サーバーの `##bootstrap` チャンネルをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="bdbd1-162">On the `irc.freenode.net` server, in the `##bootstrap` channel.</span></span>
* <span data-ttu-id="bdbd1-163">実装に関するヘルプについては、Stack Overflow (タグ [`twitter-bootstrap-3`](https://stackoverflow.com/questions/tagged/twitter-bootstrap-3)) をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="bdbd1-163">Implementation help may be found at Stack Overflow (tagged [`twitter-bootstrap-3`](https://stackoverflow.com/questions/tagged/twitter-bootstrap-3)).</span></span>
* <span data-ttu-id="bdbd1-164">開発者の方は、Bootstrap の機能を変更または追加するパッケージを [npm](https://www.npmjs.com/browse/keyword/bootstrap) で配布する場合、できるだけ多くのユーザーが見つけることができるよう `bootstrap` キーワードや同様の検出メカニズムを使用してください。</span><span class="sxs-lookup"><span data-stu-id="bdbd1-164">Developers should use the keyword `bootstrap` on packages which modify or add to the functionality of Bootstrap when distributing through [npm](https://www.npmjs.com/browse/keyword/bootstrap) or similar delivery mechanisms for maximum discoverability.</span></span>


## <a name="versioning"></a><span data-ttu-id="bdbd1-165">バージョン管理</span><span class="sxs-lookup"><span data-stu-id="bdbd1-165">Versioning</span></span>

<span data-ttu-id="bdbd1-166">リリース サイクルの透明化および後方互換性の維持のため、Bootstrap は[セマンティック バージョニングのガイドライン](http://semver.org/)に従い管理されています。</span><span class="sxs-lookup"><span data-stu-id="bdbd1-166">For transparency into our release cycle and in striving to maintain backward compatibility, Bootstrap is maintained under [the Semantic Versioning guidelines](http://semver.org/).</span></span> <span data-ttu-id="bdbd1-167">これらのルールを守ることができない場合もありますが、可能な限り遵守しています。</span><span class="sxs-lookup"><span data-stu-id="bdbd1-167">Sometimes we screw up, but we'll adhere to those rules whenever possible.</span></span>

<span data-ttu-id="bdbd1-168">Bootstrap の各リリース バージョンの変更ログについては、GitHub プロジェクトの「[Releases (リリース)](https://github.com/twbs/bootstrap/releases)」ページを参照してください。</span><span class="sxs-lookup"><span data-stu-id="bdbd1-168">See [the Releases section of our GitHub project](https://github.com/twbs/bootstrap/releases) for changelogs for each release version of Bootstrap.</span></span> <span data-ttu-id="bdbd1-169">各リリースで行われた重要な変更の概要については、[Bootstrap の公式ブログ](http://blog.getbootstrap.com)のリリース告知記事に掲載されています。</span><span class="sxs-lookup"><span data-stu-id="bdbd1-169">Release announcement posts on [the official Bootstrap blog](http://blog.getbootstrap.com) contain summaries of the most noteworthy changes made in each release.</span></span>


## <a name="creators"></a><span data-ttu-id="bdbd1-170">作成者</span><span class="sxs-lookup"><span data-stu-id="bdbd1-170">Creators</span></span>

<span data-ttu-id="bdbd1-171">**Mark Otto**</span><span class="sxs-lookup"><span data-stu-id="bdbd1-171">**Mark Otto**</span></span>

* <https://twitter.com/mdo>
* <https://github.com/mdo>

<span data-ttu-id="bdbd1-172">**Jacob Thornton**</span><span class="sxs-lookup"><span data-stu-id="bdbd1-172">**Jacob Thornton**</span></span>

* <https://twitter.com/fat>
* <https://github.com/fat>


## <a name="copyright-and-license"></a><span data-ttu-id="bdbd1-173">著作権およびライセンス</span><span class="sxs-lookup"><span data-stu-id="bdbd1-173">Copyright and license</span></span>

<span data-ttu-id="bdbd1-174">2011 年 - 2016 年のコードおよびドキュメントの著作権は Twitter, Inc. に帰属します。コードは [MIT ライセンス](https://github.com/twbs/bootstrap/blob/master/LICENSE)に従い公開されています。</span><span class="sxs-lookup"><span data-stu-id="bdbd1-174">Code and documentation copyright 2011-2016 Twitter, Inc. Code released under [the MIT license](https://github.com/twbs/bootstrap/blob/master/LICENSE).</span></span> <span data-ttu-id="bdbd1-175">ドキュメントは[クリエイティブ コモンズ](https://github.com/twbs/bootstrap/blob/master/docs/LICENSE)に従い公開されています。</span><span class="sxs-lookup"><span data-stu-id="bdbd1-175">Docs released under [Creative Commons](https://github.com/twbs/bootstrap/blob/master/docs/LICENSE).</span></span>
