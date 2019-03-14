---
ms.openlocfilehash: 1b563a8c0674d51f893415221ca8fab574b78265
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57046549"
---
<a name="--"></a>--
================================

<span data-ttu-id="3adca-101">[![ビルドの状態](https://secure.travis-ci.org/jzaefferer/jquery-validation.png)](http://travis-ci.org/jzaefferer/jquery-validation)
[![devDependency の状態](https://david-dm.org/jzaefferer/jquery-validation/dev-status.png?theme=shields.io)](https://david-dm.org/jzaefferer/jquery-validation#info=devDependencies)</span><span class="sxs-lookup"><span data-stu-id="3adca-101">[![Build Status](https://secure.travis-ci.org/jzaefferer/jquery-validation.png)](http://travis-ci.org/jzaefferer/jquery-validation)
[![devDependency Status](https://david-dm.org/jzaefferer/jquery-validation/dev-status.png?theme=shields.io)](https://david-dm.org/jzaefferer/jquery-validation#info=devDependencies)</span></span>

<span data-ttu-id="3adca-102">jQuery Validation プラグインでは既存のフォーム用にドロップイン検証を使用でき、さらにアプリケーションにあらゆるカスタマイズを非常に簡単に合わせることができます。</span><span class="sxs-lookup"><span data-stu-id="3adca-102">The jQuery Validation Plugin provides drop-in validation for your existing forms, while making all kinds of customizations to fit your application really easy.</span></span>

## <a name="help-the-projecthttppledgiecomcampaigns18159"></a>[<span data-ttu-id="3adca-103">プロジェクトを支援する</span><span class="sxs-lookup"><span data-stu-id="3adca-103">Help the project</span></span>](http://pledgie.com/campaigns/18159)

<span data-ttu-id="3adca-104">[![プロジェクトを支援する](http://www.pledgie.com/campaigns/18159.png?skin_name=chrome)](http://pledgie.com/campaigns/18159)</span><span class="sxs-lookup"><span data-stu-id="3adca-104">[![Help the project](http://www.pledgie.com/campaigns/18159.png?skin_name=chrome)](http://pledgie.com/campaigns/18159)</span></span>

<span data-ttu-id="3adca-105">ご支援をお願いいたします。</span><span class="sxs-lookup"><span data-stu-id="3adca-105">This project is looking for help!</span></span> <span data-ttu-id="3adca-106">[現在実施中の pledgie キャンペーンでご寄付を受け付けています](http://pledgie.com/campaigns/18159)。また、プラグインの評判を広めてください。</span><span class="sxs-lookup"><span data-stu-id="3adca-106">[You can donate to the ongoing pledgie campaign](http://pledgie.com/campaigns/18159) and help spread the word.</span></span> <span data-ttu-id="3adca-107">プラグインを使用したことがあるか、使用するつもりの場合は、少額でも結構ですのでご寄付をお願いします。</span><span class="sxs-lookup"><span data-stu-id="3adca-107">If you've used the plugin, or plan to use, consider a donation - any amount will help.</span></span>

<span data-ttu-id="3adca-108">寄附金の使用計画については、[pledgie のページ](http://pledgie.com/campaigns/18159)に記載しています。</span><span class="sxs-lookup"><span data-stu-id="3adca-108">You can find the plan for how to spend the money on the [pledgie page](http://pledgie.com/campaigns/18159).</span></span>

## <a name="get-started"></a><span data-ttu-id="3adca-109">開始するには</span><span class="sxs-lookup"><span data-stu-id="3adca-109">Get Started</span></span>

### <a name="downloading-the-prebuilt-files"></a><span data-ttu-id="3adca-110">ビルド済みファイルのダウンロード</span><span class="sxs-lookup"><span data-stu-id="3adca-110">Downloading the prebuilt files</span></span>

<span data-ttu-id="3adca-111">ビルド済みファイルは http://jqueryvalidation.org/ からダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="3adca-111">Prebuilt files can be downloaded from http://jqueryvalidation.org/</span></span>

### <a name="downloading-the-latest-changes"></a><span data-ttu-id="3adca-112">最新の変更のダウンロード</span><span class="sxs-lookup"><span data-stu-id="3adca-112">Downloading the latest changes</span></span>

<span data-ttu-id="3adca-113">リリース前の開発ファイルを以下の手順で入手できます。</span><span class="sxs-lookup"><span data-stu-id="3adca-113">The unreleased development files can be obtained by:</span></span>

 1. <span data-ttu-id="3adca-114">このリポジトリを[ダウンロード](https://github.com/jzaefferer/jquery-validation/archive/master.zip)またはフォークする</span><span class="sxs-lookup"><span data-stu-id="3adca-114">[Downloading](https://github.com/jzaefferer/jquery-validation/archive/master.zip) or Forking this repository</span></span>
 2. [<span data-ttu-id="3adca-115">ビルドを設定する</span><span class="sxs-lookup"><span data-stu-id="3adca-115">Setup the build</span></span>](CONTRIBUTING.md#build-setup)
 3. <span data-ttu-id="3adca-116">`grunt` を実行して "dist" ディレクトリ内にビルド済みのファイルを作成する</span><span class="sxs-lookup"><span data-stu-id="3adca-116">Run `grunt` to create the built files in the "dist" directory</span></span>

### <a name="including-it-on-your-page"></a><span data-ttu-id="3adca-117">プラグインをページに追加する</span><span class="sxs-lookup"><span data-stu-id="3adca-117">Including it on your page</span></span>

<span data-ttu-id="3adca-118">jQuery とこのプラグインをページに追加します。</span><span class="sxs-lookup"><span data-stu-id="3adca-118">Include jQuery and the plugin on a page.</span></span> <span data-ttu-id="3adca-119">その後、検証するフォームを選択して、`validate` メソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="3adca-119">Then select a form to validate and call the `validate` method.</span></span>

```html
<form>
    <input required>
</form>
<script src="jquery.js"></script>
<script src="jquery.validate.js"></script>
<script>
$("form").validate();
</script>
```

<span data-ttu-id="3adca-120">または、requirejs を使用して jQuery とこのプラグインをモジュールに追加します。</span><span class="sxs-lookup"><span data-stu-id="3adca-120">Alternatively include jQuery and the plugin via requirejs in your module.</span></span>

```js
define(["jquery", "jquery.validate"], function( $ ) {
    $("form").validate();
});
```

<span data-ttu-id="3adca-121">ルールおよびカスタマイズの設定方法の詳細については、[こちらのドキュメント](http://jqueryvalidation.org/documentation/)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="3adca-121">For more information on how to setup a rules and customizations, [check the documentation](http://jqueryvalidation.org/documentation/).</span></span>

## <a name="reporting-issues-and-contributing-code"></a><span data-ttu-id="3adca-122">問題の報告およびコードの投稿</span><span class="sxs-lookup"><span data-stu-id="3adca-122">Reporting issues and contributing code</span></span>

<span data-ttu-id="3adca-123">詳細については、[コントリビューションのガイドライン](CONTRIBUTING.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="3adca-123">See the [Contributing Guidelines](CONTRIBUTING.md) for details.</span></span>

<span data-ttu-id="3adca-124">**電子メール検証に関する重要な注意事項**.</span><span class="sxs-lookup"><span data-stu-id="3adca-124">**IMPORTANT NOTE ABOUT EMAIL VALIDATION**.</span></span> <span data-ttu-id="3adca-125">このプラグインは、バージョン 1.12.0 以降では [HTML5 の仕様でブラウザーでの使用が推奨されている](https://html.spec.whatwg.org/multipage/forms.html#valid-e-mail-address)正規表現を使用しています。</span><span class="sxs-lookup"><span data-stu-id="3adca-125">As of version 1.12.0 this plugin is using the same regular expression that the [HTML5 specification suggests for browsers to use](https://html.spec.whatwg.org/multipage/forms.html#valid-e-mail-address).</span></span> <span data-ttu-id="3adca-126">この手本に従い同じチェックが行われています。</span><span class="sxs-lookup"><span data-stu-id="3adca-126">We will follow their lead and use the same check.</span></span> <span data-ttu-id="3adca-127">HTML5 の仕様が正しくないと思われる場合は、そちらに問題を報告してください。</span><span class="sxs-lookup"><span data-stu-id="3adca-127">If you think the specification is wrong, please report the issue to them.</span></span> <span data-ttu-id="3adca-128">要件が異なる場合は、[カスタム メソッドの使用](http://jqueryvalidation.org/jQuery.validator.addMethod/)を検討してください。</span><span class="sxs-lookup"><span data-stu-id="3adca-128">If you have different requirements, consider [using a custom method](http://jqueryvalidation.org/jQuery.validator.addMethod/).</span></span>

## <a name="license"></a><span data-ttu-id="3adca-129">ライセンス</span><span class="sxs-lookup"><span data-stu-id="3adca-129">License</span></span>
<span data-ttu-id="3adca-130">Copyright &copy; Jörn Zaefferer</span><span class="sxs-lookup"><span data-stu-id="3adca-130">Copyright &copy; Jörn Zaefferer</span></span><br>
<span data-ttu-id="3adca-131">MIT ライセンスにより許諾されています。</span><span class="sxs-lookup"><span data-stu-id="3adca-131">Licensed under the MIT license.</span></span>
