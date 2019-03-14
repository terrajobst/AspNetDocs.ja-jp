---
ms.openlocfilehash: 7eb0f9b556f0663a5208310d2d4864eca28f8632
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57057349"
---
# <a name="contributing-to-the-jquery-validation-plugin"></a><span data-ttu-id="302e4-101">jQuery Validation プラグインに投稿する</span><span class="sxs-lookup"><span data-stu-id="302e4-101">Contributing to the jQuery Validation Plugin</span></span>

## <a name="reporting-an-issue"></a><span data-ttu-id="302e4-102">問題の報告</span><span class="sxs-lookup"><span data-stu-id="302e4-102">Reporting an Issue</span></span>

1. <span data-ttu-id="302e4-103">報告する問題が再現可能であることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="302e4-103">Make sure the problem you're addressing is reproducible.</span></span>
2. <span data-ttu-id="302e4-104">https://jsbin.com または https://jsfiddle.net を使用してテスト ページを提供します。</span><span class="sxs-lookup"><span data-stu-id="302e4-104">Use https://jsbin.com or https://jsfiddle.net to provide a test page.</span></span>
3. <span data-ttu-id="302e4-105">問題を再現できるブラウザーを記載してください。</span><span class="sxs-lookup"><span data-stu-id="302e4-105">Indicate what browsers the issue can be reproduced in.</span></span> <span data-ttu-id="302e4-106">**注:IE の互換性モードの問題には解決されません。テストは実際のブラウザーで行ってください。**</span><span class="sxs-lookup"><span data-stu-id="302e4-106">**Note: IE Compatibilty mode issues will not be addressed. Make sure you test in a real browser!**</span></span>
4. <span data-ttu-id="302e4-107">問題を再現可能なプラグインのバージョンを記載してください。</span><span class="sxs-lookup"><span data-stu-id="302e4-107">What version of the plug-in is the issue reproducible in.</span></span> <span data-ttu-id="302e4-108">最新バージョンへの更新後も問題が再発するか確認してください。</span><span class="sxs-lookup"><span data-stu-id="302e4-108">Is it reproducible after updating to the latest version.</span></span>

<span data-ttu-id="302e4-109">ドキュメントの問題は、[jQuery 検証](https://github.com/jquery-validation/jquery-validation/issues) の issue トラッカーでも追跡されています。</span><span class="sxs-lookup"><span data-stu-id="302e4-109">Documentation issues are also tracked at the [jQuery Validation](https://github.com/jquery-validation/jquery-validation/issues) issue tracker.</span></span>
<span data-ttu-id="302e4-110">ドキュメントに関するPull Requests も [jQuery 検証のドキュメント](https://github.com/jquery-validation/validation-content) リポジトリにお寄せください。</span><span class="sxs-lookup"><span data-stu-id="302e4-110">Pull Requests to improve the docs are welcome at the [jQuery Validation docs](https://github.com/jquery-validation/validation-content) repository, though.</span></span>

<span data-ttu-id="302e4-111">**電子メール検証に関する重要な注意事項**.</span><span class="sxs-lookup"><span data-stu-id="302e4-111">**IMPORTANT NOTE ABOUT EMAIL VALIDATION**.</span></span> <span data-ttu-id="302e4-112">このプラグインは、バージョン 1.12.0 以降では [HTML5 の仕様でブラウザーでの使用が推奨されている](https://html.spec.whatwg.org/multipage/forms.html#valid-e-mail-address)正規表現を使用しています。</span><span class="sxs-lookup"><span data-stu-id="302e4-112">As of version 1.12.0 this plugin is using the same regular expression that the [HTML5 specification suggests for browsers to use](https://html.spec.whatwg.org/multipage/forms.html#valid-e-mail-address).</span></span> <span data-ttu-id="302e4-113">この手本に従い同じチェックが行われています。</span><span class="sxs-lookup"><span data-stu-id="302e4-113">We will follow their lead and use the same check.</span></span> <span data-ttu-id="302e4-114">HTML5 の仕様が正しくないと思われる場合は、そちらに問題を報告してください。</span><span class="sxs-lookup"><span data-stu-id="302e4-114">If you think the specification is wrong, please report the issue to them.</span></span> <span data-ttu-id="302e4-115">要件が異なる場合は、[カスタム メソッドの使用](http://jqueryvalidation.org/jQuery.validator.addMethod/)を検討してください。</span><span class="sxs-lookup"><span data-stu-id="302e4-115">If you have different requirements, consider [using a custom method](http://jqueryvalidation.org/jQuery.validator.addMethod/).</span></span>
<span data-ttu-id="302e4-116">組み込みの検証の正規表現パターンを調整する必要がある場合は、[ドキュメントに従ってください](http://jqueryvalidation.org/jQuery.validator.methods/)。</span><span class="sxs-lookup"><span data-stu-id="302e4-116">In case you need to adjust the built-in validation regular expression patterns, please [follow the documentation](http://jqueryvalidation.org/jQuery.validator.methods/).</span></span>

## <a name="contributing-code"></a><span data-ttu-id="302e4-117">コードの投稿</span><span class="sxs-lookup"><span data-stu-id="302e4-117">Contributing code</span></span>

<span data-ttu-id="302e4-118">投稿してくださりありがとうございます。</span><span class="sxs-lookup"><span data-stu-id="302e4-118">Thanks for contributing!</span></span> <span data-ttu-id="302e4-119">以下に、投稿が受け入られやすくなるいくつかのガイドラインを示します。</span><span class="sxs-lookup"><span data-stu-id="302e4-119">Here's a few guidelines to help your contribution get landed.</span></span>

1. <span data-ttu-id="302e4-120">報告する問題が再現可能であることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="302e4-120">Make sure the problem you're addressing is reproducible.</span></span> <span data-ttu-id="302e4-121">jsbin.com または jsfiddle.net を使用してテスト ページを用意してください。</span><span class="sxs-lookup"><span data-stu-id="302e4-121">Use jsbin.com or jsfiddle.net to provide a test page.</span></span>
2. <span data-ttu-id="302e4-122">[jQuery のスタイル ガイド](http://contribute.jquery.com/style-guides/js)に従ってください。</span><span class="sxs-lookup"><span data-stu-id="302e4-122">Follow the [jQuery style guide](http://contribute.jquery.com/style-guides/js)</span></span>
3. <span data-ttu-id="302e4-123">パッチとともに単体テストを追加するか更新してください。</span><span class="sxs-lookup"><span data-stu-id="302e4-123">Add or update unit tests along with your patch.</span></span> <span data-ttu-id="302e4-124">1 つ以上のブラウザーで単体テストを実行してください (下記参照)。</span><span class="sxs-lookup"><span data-stu-id="302e4-124">Run the unit tests in at least one browser (see below).</span></span>
4. <span data-ttu-id="302e4-125">`grunt` (下記参照) を実行して、lint およびその他のいくつかの問題をチェックしてください。</span><span class="sxs-lookup"><span data-stu-id="302e4-125">Run `grunt` (see below) to check for linting and a few other issues.</span></span>
5. <span data-ttu-id="302e4-126">コミット メッセージの変更を説明し、次のように、チケットの参照します。"デモ。dynamic-totals デモのデリゲート バグを修正しました。</span><span class="sxs-lookup"><span data-stu-id="302e4-126">Describe the change in your commit message and reference the ticket, like this: "Demos: Fixed delegate bug for dynamic-totals demo.</span></span> <span data-ttu-id="302e4-127">#51 の修正” のように記載してください。</span><span class="sxs-lookup"><span data-stu-id="302e4-127">Fixes #51".</span></span> <span data-ttu-id="302e4-128">新しいローカライズ ファイルを追加する場合は、このようなものを使用します。"ローカリゼーション。追加されたクロアチア語 (HR) のローカリゼーション"</span><span class="sxs-lookup"><span data-stu-id="302e4-128">If you're adding a new localization file, use something like this: "Localization: Added croatian (HR) localization"</span></span>

## <a name="build-setup"></a><span data-ttu-id="302e4-129">ビルドのセットアップ</span><span class="sxs-lookup"><span data-stu-id="302e4-129">Build setup</span></span>

1. <span data-ttu-id="302e4-130">[NodeJS](http://nodejs.org) をインストールします。</span><span class="sxs-lookup"><span data-stu-id="302e4-130">Install [NodeJS](http://nodejs.org).</span></span>
2. <span data-ttu-id="302e4-131">`npm install -g grunt-cli` を実行して、Grunt CLI をインストールします。</span><span class="sxs-lookup"><span data-stu-id="302e4-131">Install the Grunt CLI To install by running `npm install -g grunt-cli`.</span></span> <span data-ttu-id="302e4-132">詳細については、Web サイト (http://gruntjs.com/getting-started) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="302e4-132">More details are available on their website http://gruntjs.com/getting-started.</span></span>
3. <span data-ttu-id="302e4-133">`npm install` を実行して、NPM の依存パッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="302e4-133">Install the NPM dependencies by running `npm install`.</span></span>
4. <span data-ttu-id="302e4-134">これで、`grunt` を実行してビルドを呼び出せるようになりました。</span><span class="sxs-lookup"><span data-stu-id="302e4-134">The build can now be called by running `grunt`.</span></span>

## <a name="creating-a-new-additional-method"></a><span data-ttu-id="302e4-135">新しい追加メソッドの作成</span><span class="sxs-lookup"><span data-stu-id="302e4-135">Creating a new Additional Method</span></span>

<span data-ttu-id="302e4-136">additional-methods.js に投稿するカスタム メソッドを作成した場合は、次の手順に従ってください。</span><span class="sxs-lookup"><span data-stu-id="302e4-136">If you've wrote custom methods that you'd like to contribute to additional-methods.js:</span></span>

1. <span data-ttu-id="302e4-137">分岐を作成する</span><span class="sxs-lookup"><span data-stu-id="302e4-137">Create a branch</span></span>
2. <span data-ttu-id="302e4-138">メソッドを `src/additional` に新しいファイルとして追加する</span><span class="sxs-lookup"><span data-stu-id="302e4-138">Add the method as a new file in `src/additional`</span></span>
3. <span data-ttu-id="302e4-139">(省略可能) `src/localization` に翻訳を追加する</span><span class="sxs-lookup"><span data-stu-id="302e4-139">(Optional) Add translations to `src/localization`</span></span>
4. <span data-ttu-id="302e4-140">マスター ブランチに pull request 送信する。</span><span class="sxs-lookup"><span data-stu-id="302e4-140">Send a pull request to the master branch.</span></span>

## <a name="unit-tests"></a><span data-ttu-id="302e4-141">単体テスト</span><span class="sxs-lookup"><span data-stu-id="302e4-141">Unit Tests</span></span>

<span data-ttu-id="302e4-142">単体テストを実行するには、ブラウザーで `test/index.html` を開きます。</span><span class="sxs-lookup"><span data-stu-id="302e4-142">To run unit tests, just open `test/index.html` within your browser.</span></span> <span data-ttu-id="302e4-143">テストの前に、`npm install` を実行して必要な依存パッケージをすべて揃えてください。</span><span class="sxs-lookup"><span data-stu-id="302e4-143">Make sure you ran `npm install` before so all required dependencies are available.</span></span>
<span data-ttu-id="302e4-144">修正プログラムの作成中は 1 つのブラウザーで作業し、コミットの前に別のブラウザーで実行します。</span><span class="sxs-lookup"><span data-stu-id="302e4-144">Start with one browser while developing the fix, then run against others before committing.</span></span> <span data-ttu-id="302e4-145">最新の Chrome、Firefox、Safari、Opera の使用が一般的であり、IE は少数です。</span><span class="sxs-lookup"><span data-stu-id="302e4-145">Usually latest Chrome, Firefox, Safari and Opera and a few IEs.</span></span>

## <a name="documentation"></a><span data-ttu-id="302e4-146">ドキュメント</span><span class="sxs-lookup"><span data-stu-id="302e4-146">Documentation</span></span>

<span data-ttu-id="302e4-147">ドキュメントの問題は、[jQuery 検証](https://github.com/jquery-validation/jquery-validation/issues) の issue トラッカーで報告してください。</span><span class="sxs-lookup"><span data-stu-id="302e4-147">Please report documentation issues at the [jQuery Validation](https://github.com/jquery-validation/jquery-validation/issues) issue tracker.</span></span>
<span data-ttu-id="302e4-148">pull request でパブリック API を実装または変更する場合は、さらに [jQuery 検証のドキュメント](https://github.com/jquery-validation/validation-content) リポジトリにプル要求を提供してください。</span><span class="sxs-lookup"><span data-stu-id="302e4-148">In case your pull request implements or changes public API it would be a plus you would provide a pull request against the [jQuery Validation docs](https://github.com/jquery-validation/validation-content) repository.</span></span>

## <a name="linting"></a><span data-ttu-id="302e4-149">Lint</span><span class="sxs-lookup"><span data-stu-id="302e4-149">Linting</span></span>

<span data-ttu-id="302e4-150">`grunt` を使用して、JSHint などのツールを実行します。</span><span class="sxs-lookup"><span data-stu-id="302e4-150">To run JSHint and other tools, use `grunt`.</span></span>
