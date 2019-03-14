---
ms.openlocfilehash: 1f36b95063094e891c1e6b44fbf4ee7546853d89
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57038949"
---
# <a name="contributing-to-the-jquery-validation-plugin"></a><span data-ttu-id="e79a5-101">jQuery Validation プラグインに投稿する</span><span class="sxs-lookup"><span data-stu-id="e79a5-101">Contributing to the jQuery Validation Plugin</span></span>

## <a name="reporting-an-issue"></a><span data-ttu-id="e79a5-102">問題の報告</span><span class="sxs-lookup"><span data-stu-id="e79a5-102">Reporting an Issue</span></span>

1. <span data-ttu-id="e79a5-103">報告する問題が再現可能であることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="e79a5-103">Make sure the problem you're addressing is reproducible.</span></span>
2. <span data-ttu-id="e79a5-104">http://jsbin.com または http://jsfiddle.net を使用してテスト ページを提供します。</span><span class="sxs-lookup"><span data-stu-id="e79a5-104">Use http://jsbin.com or http://jsfiddle.net to provide a test page.</span></span>
3. <span data-ttu-id="e79a5-105">問題を再現できるブラウザーを記載してください。</span><span class="sxs-lookup"><span data-stu-id="e79a5-105">Indicate what browsers the issue can be reproduced in.</span></span> <span data-ttu-id="e79a5-106">**注:IE の互換性モードの問題には解決されません。テストは実際のブラウザーで行ってください。**</span><span class="sxs-lookup"><span data-stu-id="e79a5-106">**Note: IE Compatibilty mode issues will not be addressed. Make sure you test in a real browser!**</span></span>
4. <span data-ttu-id="e79a5-107">問題を再現可能なプラグインのバージョンを記載してください。</span><span class="sxs-lookup"><span data-stu-id="e79a5-107">What version of the plug-in is the issue reproducible in.</span></span> <span data-ttu-id="e79a5-108">最新バージョンへの更新後も問題が再発するか確認してください。</span><span class="sxs-lookup"><span data-stu-id="e79a5-108">Is it reproducible after updating to the latest version.</span></span>

<span data-ttu-id="e79a5-109">ドキュメントの問題は、[jQuery 検証](https://github.com/jzaefferer/jquery-validation/issues) の issue トラッカーでも追跡されています。</span><span class="sxs-lookup"><span data-stu-id="e79a5-109">Documentation issues are also tracked at the [jQuery Validation](https://github.com/jzaefferer/jquery-validation/issues) issue tracker.</span></span>
<span data-ttu-id="e79a5-110">ドキュメントに関するPull Requests も [jQuery 検証のドキュメント](https://github.com/jzaefferer/validation-content) リポジトリにお寄せください。</span><span class="sxs-lookup"><span data-stu-id="e79a5-110">Pull Requests to improve the docs are welcome at the [jQuery Validation docs](https://github.com/jzaefferer/validation-content) repository, though.</span></span>

<span data-ttu-id="e79a5-111">**電子メール検証に関する重要な注意事項**.</span><span class="sxs-lookup"><span data-stu-id="e79a5-111">**IMPORTANT NOTE ABOUT EMAIL VALIDATION**.</span></span> <span data-ttu-id="e79a5-112">このプラグインは、バージョン 1.12.0 以降では [HTML5 の仕様でブラウザーでの使用が推奨されている](https://html.spec.whatwg.org/multipage/forms.html#valid-e-mail-address)正規表現を使用しています。</span><span class="sxs-lookup"><span data-stu-id="e79a5-112">As of version 1.12.0 this plugin is using the same regular expression that the [HTML5 specification suggests for browsers to use](https://html.spec.whatwg.org/multipage/forms.html#valid-e-mail-address).</span></span> <span data-ttu-id="e79a5-113">この手本に従い同じチェックが行われています。</span><span class="sxs-lookup"><span data-stu-id="e79a5-113">We will follow their lead and use the same check.</span></span> <span data-ttu-id="e79a5-114">HTML5 の仕様が正しくないと思われる場合は、そちらに問題を報告してください。</span><span class="sxs-lookup"><span data-stu-id="e79a5-114">If you think the specification is wrong, please report the issue to them.</span></span> <span data-ttu-id="e79a5-115">要件が異なる場合は、[カスタム メソッドの使用](http://jqueryvalidation.org/jQuery.validator.addMethod/)を検討してください。</span><span class="sxs-lookup"><span data-stu-id="e79a5-115">If you have different requirements, consider [using a custom method](http://jqueryvalidation.org/jQuery.validator.addMethod/).</span></span>

## <a name="contributing-code"></a><span data-ttu-id="e79a5-116">コードの投稿</span><span class="sxs-lookup"><span data-stu-id="e79a5-116">Contributing code</span></span>

<span data-ttu-id="e79a5-117">投稿してくださりありがとうございます。</span><span class="sxs-lookup"><span data-stu-id="e79a5-117">Thanks for contributing!</span></span> <span data-ttu-id="e79a5-118">以下に、投稿が受け入られやすくなるいくつかのガイドラインを示します。</span><span class="sxs-lookup"><span data-stu-id="e79a5-118">Here's a few guidelines to help your contribution get landed.</span></span>

1. <span data-ttu-id="e79a5-119">報告する問題が再現可能であることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="e79a5-119">Make sure the problem you're addressing is reproducible.</span></span> <span data-ttu-id="e79a5-120">jsbin.com または jsfiddle.net を使用してテスト ページを用意してください。</span><span class="sxs-lookup"><span data-stu-id="e79a5-120">Use jsbin.com or jsfiddle.net to provide a test page.</span></span>
2. <span data-ttu-id="e79a5-121">[jQuery のスタイル ガイド](http://contribute.jquery.com/style-guides/js)に従ってください。</span><span class="sxs-lookup"><span data-stu-id="e79a5-121">Follow the [jQuery style guide](http://contribute.jquery.com/style-guides/js)</span></span>
3. <span data-ttu-id="e79a5-122">パッチとともに単体テストを追加するか更新してください。</span><span class="sxs-lookup"><span data-stu-id="e79a5-122">Add or update unit tests along with your patch.</span></span> <span data-ttu-id="e79a5-123">1 つ以上のブラウザーで単体テストを実行してください (下記参照)。</span><span class="sxs-lookup"><span data-stu-id="e79a5-123">Run the unit tests in at least one browser (see below).</span></span>
4. <span data-ttu-id="e79a5-124">`grunt` (下記参照) を実行して、lint およびその他のいくつかの問題をチェックしてください。</span><span class="sxs-lookup"><span data-stu-id="e79a5-124">Run `grunt` (see below) to check for linting and a few other issues.</span></span>
5. <span data-ttu-id="e79a5-125">コミット メッセージの変更を説明し、次のように、チケットの参照します。"デモ。dynamic-totals デモのデリゲート バグを修正しました。</span><span class="sxs-lookup"><span data-stu-id="e79a5-125">Describe the change in your commit message and reference the ticket, like this: "Demos: Fixed delegate bug for dynamic-totals demo.</span></span> <span data-ttu-id="e79a5-126">#51 の修正” のように記載してください。</span><span class="sxs-lookup"><span data-stu-id="e79a5-126">Fixes #51".</span></span> <span data-ttu-id="e79a5-127">新しいローカライズ ファイルを追加する場合は、このようなものを使用します。"ローカリゼーション。追加されたクロアチア語 (HR) のローカリゼーション"</span><span class="sxs-lookup"><span data-stu-id="e79a5-127">If you're adding a new localization file, use something like this: "Localization: Added croatian (HR) localization"</span></span>

## <a name="build-setup"></a><span data-ttu-id="e79a5-128">ビルドのセットアップ</span><span class="sxs-lookup"><span data-stu-id="e79a5-128">Build setup</span></span>

1. <span data-ttu-id="e79a5-129">[NodeJS](http://nodejs.org) をインストールします。</span><span class="sxs-lookup"><span data-stu-id="e79a5-129">Install [NodeJS](http://nodejs.org).</span></span>
2. <span data-ttu-id="e79a5-130">`npm install -g grunt-cli` を実行して、Grunt CLI をインストールします。</span><span class="sxs-lookup"><span data-stu-id="e79a5-130">Install the Grunt CLI To install by running `npm install -g grunt-cli`.</span></span> <span data-ttu-id="e79a5-131">詳細については、Web サイト (http://gruntjs.com/getting-started) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="e79a5-131">More details are available on their website http://gruntjs.com/getting-started.</span></span>
3. <span data-ttu-id="e79a5-132">`npm install` を実行して、NPM の依存パッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="e79a5-132">Install the NPM dependencies by running `npm install`.</span></span>
4. <span data-ttu-id="e79a5-133">これで、`grunt` を実行してビルドを呼び出せるようになりました。</span><span class="sxs-lookup"><span data-stu-id="e79a5-133">The build can now be called by running `grunt`.</span></span>

## <a name="creating-a-new-additional-method"></a><span data-ttu-id="e79a5-134">新しい追加メソッドの作成</span><span class="sxs-lookup"><span data-stu-id="e79a5-134">Creating a new Additional Method</span></span>

<span data-ttu-id="e79a5-135">additional-methods.js に投稿するカスタム メソッドを作成した場合は、次の手順に従ってください。</span><span class="sxs-lookup"><span data-stu-id="e79a5-135">If you've wrote custom methods that you'd like to contribute to additional-methods.js:</span></span>

1. <span data-ttu-id="e79a5-136">分岐を作成する</span><span class="sxs-lookup"><span data-stu-id="e79a5-136">Create a branch</span></span>
2. <span data-ttu-id="e79a5-137">メソッドを `src/additional` に新しいファイルとして追加する</span><span class="sxs-lookup"><span data-stu-id="e79a5-137">Add the method as a new file in `src/additional`</span></span>
3. <span data-ttu-id="e79a5-138">(省略可能) `src/localization` に翻訳を追加する</span><span class="sxs-lookup"><span data-stu-id="e79a5-138">(Optional) Add translations to `src/localization`</span></span>
4. <span data-ttu-id="e79a5-139">マスター ブランチに pull request 送信する。</span><span class="sxs-lookup"><span data-stu-id="e79a5-139">Send a pull request to the master branch.</span></span>

## <a name="unit-tests"></a><span data-ttu-id="e79a5-140">単体テスト</span><span class="sxs-lookup"><span data-stu-id="e79a5-140">Unit Tests</span></span>

<span data-ttu-id="e79a5-141">単体テストを実行するには、ブラウザーで `test/index.html` を開きます。</span><span class="sxs-lookup"><span data-stu-id="e79a5-141">To run unit tests, just open `test/index.html` within your browser.</span></span> <span data-ttu-id="e79a5-142">テストの前に、`npm install` を実行して必要な依存パッケージをすべて揃えてください。</span><span class="sxs-lookup"><span data-stu-id="e79a5-142">Make sure you ran `npm install` before so all required dependencies are available.</span></span>
<span data-ttu-id="e79a5-143">修正プログラムの作成中は 1 つのブラウザーで作業し、コミットの前に別のブラウザーで実行します。</span><span class="sxs-lookup"><span data-stu-id="e79a5-143">Start with one browser while developing the fix, then run against others before committing.</span></span> <span data-ttu-id="e79a5-144">最新の Chrome、Firefox、Safari、Opera の使用が一般的であり、IE は少数です。</span><span class="sxs-lookup"><span data-stu-id="e79a5-144">Usually latest Chrome, Firefox, Safari and Opera and a few IEs.</span></span>

## <a name="documentation"></a><span data-ttu-id="e79a5-145">ドキュメント</span><span class="sxs-lookup"><span data-stu-id="e79a5-145">Documentation</span></span>

<span data-ttu-id="e79a5-146">ドキュメントの問題は、[jQuery 検証](https://github.com/jzaefferer/jquery-validation/issues) の issue トラッカーで報告してください。</span><span class="sxs-lookup"><span data-stu-id="e79a5-146">Please report documentation issues at the [jQuery Validation](https://github.com/jzaefferer/jquery-validation/issues) issue tracker.</span></span>
<span data-ttu-id="e79a5-147">pull request でパブリック API を実装または変更する場合は、さらに [jQuery 検証のドキュメント](https://github.com/jzaefferer/validation-content) リポジトリにプル要求を提供してください。</span><span class="sxs-lookup"><span data-stu-id="e79a5-147">In case your pull request implements or changes public API it would be a plus you would provide a pull request against the [jQuery Validation docs](https://github.com/jzaefferer/validation-content) repository.</span></span>

## <a name="linting"></a><span data-ttu-id="e79a5-148">Lint</span><span class="sxs-lookup"><span data-stu-id="e79a5-148">Linting</span></span>

<span data-ttu-id="e79a5-149">`grunt` を使用して、JSHint などのツールを実行します。</span><span class="sxs-lookup"><span data-stu-id="e79a5-149">To run JSHint and other tools, use `grunt`.</span></span>
