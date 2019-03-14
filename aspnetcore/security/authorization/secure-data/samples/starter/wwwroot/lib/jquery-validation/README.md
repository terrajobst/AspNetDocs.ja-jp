---
ms.openlocfilehash: 83a958fe6a8d61becf9f9062e8ad0ff69108b435
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57034989"
---
<a name="jquery-validation-pluginhttpjqueryvalidationorg---form-validation-made-easy"></a><span data-ttu-id="ffb41-101">[jQuery Validation プラグイン](http://jqueryvalidation.org/) - フォームの検証を簡単に作成</span><span class="sxs-lookup"><span data-stu-id="ffb41-101">[jQuery Validation Plugin](http://jqueryvalidation.org/) - Form validation made easy</span></span>
================================

<span data-ttu-id="ffb41-102">[![ビルドの状態](https://secure.travis-ci.org/jzaefferer/jquery-validation.png)](http://travis-ci.org/jzaefferer/jquery-validation)
[![devDependency の状態](https://david-dm.org/jzaefferer/jquery-validation/dev-status.png?theme=shields.io)](https://david-dm.org/jzaefferer/jquery-validation#info=devDependencies)</span><span class="sxs-lookup"><span data-stu-id="ffb41-102">[![Build Status](https://secure.travis-ci.org/jzaefferer/jquery-validation.png)](http://travis-ci.org/jzaefferer/jquery-validation)
[![devDependency Status](https://david-dm.org/jzaefferer/jquery-validation/dev-status.png?theme=shields.io)](https://david-dm.org/jzaefferer/jquery-validation#info=devDependencies)</span></span>

<span data-ttu-id="ffb41-103">jQuery Validation プラグインでは既存のフォーム用にドロップイン検証を使用でき、さらにアプリケーションにあらゆるカスタマイズを非常に簡単に合わせることができます。</span><span class="sxs-lookup"><span data-stu-id="ffb41-103">The jQuery Validation Plugin provides drop-in validation for your existing forms, while making all kinds of customizations to fit your application really easy.</span></span>

## <a name="help-the-projecthttppledgiecomcampaigns18159"></a>[<span data-ttu-id="ffb41-104">プロジェクトを支援する</span><span class="sxs-lookup"><span data-stu-id="ffb41-104">Help the project</span></span>](http://pledgie.com/campaigns/18159)

<span data-ttu-id="ffb41-105">[![プロジェクトを支援する](http://www.pledgie.com/campaigns/18159.png?skin_name=chrome)](http://pledgie.com/campaigns/18159)</span><span class="sxs-lookup"><span data-stu-id="ffb41-105">[![Help the project](http://www.pledgie.com/campaigns/18159.png?skin_name=chrome)](http://pledgie.com/campaigns/18159)</span></span>

<span data-ttu-id="ffb41-106">ご支援をお願いいたします。</span><span class="sxs-lookup"><span data-stu-id="ffb41-106">This project is looking for help!</span></span> <span data-ttu-id="ffb41-107">[現在実施中の pledgie キャンペーンでご寄付を受け付けています](http://pledgie.com/campaigns/18159)。また、プラグインの評判を広めてください。</span><span class="sxs-lookup"><span data-stu-id="ffb41-107">[You can donate to the ongoing pledgie campaign](http://pledgie.com/campaigns/18159) and help spread the word.</span></span> <span data-ttu-id="ffb41-108">プラグインを使用したことがあるか、使用するつもりの場合は、少額でも結構ですのでご寄付をお願いします。</span><span class="sxs-lookup"><span data-stu-id="ffb41-108">If you've used the plugin, or plan to use, consider a donation - any amount will help.</span></span>

<span data-ttu-id="ffb41-109">寄附金の使用計画については、[pledgie のページ](http://pledgie.com/campaigns/18159)に記載しています。</span><span class="sxs-lookup"><span data-stu-id="ffb41-109">You can find the plan for how to spend the money on the [pledgie page](http://pledgie.com/campaigns/18159).</span></span>

## <a name="getting-started"></a><span data-ttu-id="ffb41-110">作業の開始</span><span class="sxs-lookup"><span data-stu-id="ffb41-110">Getting Started</span></span>

### <a name="downloading-the-prebuilt-files"></a><span data-ttu-id="ffb41-111">ビルド済みファイルのダウンロード</span><span class="sxs-lookup"><span data-stu-id="ffb41-111">Downloading the prebuilt files</span></span>

<span data-ttu-id="ffb41-112">ビルド済みファイルは http://jqueryvalidation.org/ からダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="ffb41-112">Prebuilt files can be downloaded from http://jqueryvalidation.org/</span></span>

### <a name="downloading-the-latest-changes"></a><span data-ttu-id="ffb41-113">最新の変更のダウンロード</span><span class="sxs-lookup"><span data-stu-id="ffb41-113">Downloading the latest changes</span></span>

<span data-ttu-id="ffb41-114">リリース前の開発ファイルを以下の手順で入手できます。</span><span class="sxs-lookup"><span data-stu-id="ffb41-114">The unreleased development files can be obtained by:</span></span>

 1. <span data-ttu-id="ffb41-115">このリポジトリを[ダウンロード](https://github.com/jzaefferer/jquery-validation/archive/master.zip)またはフォークする</span><span class="sxs-lookup"><span data-stu-id="ffb41-115">[Downloading](https://github.com/jzaefferer/jquery-validation/archive/master.zip) or Forking this repository</span></span>
 2. [<span data-ttu-id="ffb41-116">ビルドを設定する</span><span class="sxs-lookup"><span data-stu-id="ffb41-116">Setup the build</span></span>](CONTRIBUTING.md#build-setup)
 3. <span data-ttu-id="ffb41-117">`grunt` を実行して "dist" ディレクトリ内にビルド済みのファイルを作成する</span><span class="sxs-lookup"><span data-stu-id="ffb41-117">Run `grunt` to create the built files in the "dist" directory</span></span>

### <a name="including-it-on-your-page"></a><span data-ttu-id="ffb41-118">プラグインをページに追加する</span><span class="sxs-lookup"><span data-stu-id="ffb41-118">Including it on your page</span></span>

<span data-ttu-id="ffb41-119">jQuery とこのプラグインをページに追加します。</span><span class="sxs-lookup"><span data-stu-id="ffb41-119">Include jQuery and the plugin on a page.</span></span> <span data-ttu-id="ffb41-120">その後、検証するフォームを選択して、`validate` メソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="ffb41-120">Then select a form to validate and call the `validate` method.</span></span>

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

<span data-ttu-id="ffb41-121">または、requirejs を使用して jQuery とこのプラグインをモジュールに追加します。</span><span class="sxs-lookup"><span data-stu-id="ffb41-121">Alternatively include jQuery and the plugin via requirejs in your module.</span></span>

```js
define(["jquery", "jquery.validate"], function( $ ) {
    $("form").validate();
});
```

<span data-ttu-id="ffb41-122">ルールおよびカスタマイズの設定方法の詳細については、[こちらのドキュメント](http://jqueryvalidation.org/documentation/)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ffb41-122">For more information on how to setup a rules and customizations, [check the documentation](http://jqueryvalidation.org/documentation/).</span></span>

## <a name="reporting-issues-and-contributing-code"></a><span data-ttu-id="ffb41-123">問題の報告およびコードの投稿</span><span class="sxs-lookup"><span data-stu-id="ffb41-123">Reporting issues and contributing code</span></span>

<span data-ttu-id="ffb41-124">詳細については、[コントリビューションのガイドライン](CONTRIBUTING.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ffb41-124">See the [Contributing Guidelines](CONTRIBUTING.md) for details.</span></span>

<span data-ttu-id="ffb41-125">**電子メール検証に関する重要な注意事項**.</span><span class="sxs-lookup"><span data-stu-id="ffb41-125">**IMPORTANT NOTE ABOUT EMAIL VALIDATION**.</span></span> <span data-ttu-id="ffb41-126">このプラグインは、バージョン 1.12.0 以降では [HTML5 の仕様でブラウザーでの使用が推奨されている](https://html.spec.whatwg.org/multipage/forms.html#valid-e-mail-address)正規表現を使用しています。</span><span class="sxs-lookup"><span data-stu-id="ffb41-126">As of version 1.12.0 this plugin is using the same regular expression that the [HTML5 specification suggests for browsers to use](https://html.spec.whatwg.org/multipage/forms.html#valid-e-mail-address).</span></span> <span data-ttu-id="ffb41-127">この手本に従い同じチェックが行われています。</span><span class="sxs-lookup"><span data-stu-id="ffb41-127">We will follow their lead and use the same check.</span></span> <span data-ttu-id="ffb41-128">HTML5 の仕様が正しくないと思われる場合は、そちらに問題を報告してください。</span><span class="sxs-lookup"><span data-stu-id="ffb41-128">If you think the specification is wrong, please report the issue to them.</span></span> <span data-ttu-id="ffb41-129">要件が異なる場合は、[カスタム メソッドの使用](http://jqueryvalidation.org/jQuery.validator.addMethod/)を検討してください。</span><span class="sxs-lookup"><span data-stu-id="ffb41-129">If you have different requirements, consider [using a custom method](http://jqueryvalidation.org/jQuery.validator.addMethod/).</span></span>

## <a name="license"></a><span data-ttu-id="ffb41-130">ライセンス</span><span class="sxs-lookup"><span data-stu-id="ffb41-130">License</span></span>
<span data-ttu-id="ffb41-131">Copyright &copy; Jörn Zaefferer</span><span class="sxs-lookup"><span data-stu-id="ffb41-131">Copyright &copy; Jörn Zaefferer</span></span><br>
<span data-ttu-id="ffb41-132">MIT ライセンスにより許諾されています。</span><span class="sxs-lookup"><span data-stu-id="ffb41-132">Licensed under the MIT license.</span></span>
