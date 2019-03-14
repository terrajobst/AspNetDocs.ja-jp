---
ms.openlocfilehash: 24c36493284988aa45b15c78e2577c0ef96aba56
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57029989"
---
<a name="jquery-validation-pluginhttpsjqueryvalidationorg---form-validation-made-easy"></a><span data-ttu-id="fa147-101">[jQuery Validation プラグイン](https://jqueryvalidation.org/) - フォームの検証を簡単に作成</span><span class="sxs-lookup"><span data-stu-id="fa147-101">[jQuery Validation Plugin](https://jqueryvalidation.org/) - Form validation made easy</span></span>
================================

<span data-ttu-id="fa147-102">[![ビルドの状態](https://secure.travis-ci.org/jquery-validation/jquery-validation.svg)](https://travis-ci.org/jquery-validation/jquery-validation)
[![devDependency の状態](https://david-dm.org/jquery-validation/jquery-validation/dev-status.svg?theme=shields.io)](https://david-dm.org/jquery-validation/jquery-validation#info=devDependencies)</span><span class="sxs-lookup"><span data-stu-id="fa147-102">[![Build Status](https://secure.travis-ci.org/jquery-validation/jquery-validation.svg)](https://travis-ci.org/jquery-validation/jquery-validation)
[![devDependency Status](https://david-dm.org/jquery-validation/jquery-validation/dev-status.svg?theme=shields.io)](https://david-dm.org/jquery-validation/jquery-validation#info=devDependencies)</span></span>

<span data-ttu-id="fa147-103">jQuery Validation プラグインでは既存のフォーム用にドロップイン検証を使用でき、さらにアプリケーションにあらゆるカスタマイズを非常に簡単に合わせることができます。</span><span class="sxs-lookup"><span data-stu-id="fa147-103">The jQuery Validation Plugin provides drop-in validation for your existing forms, while making all kinds of customizations to fit your application really easy.</span></span>

## <a name="getting-started"></a><span data-ttu-id="fa147-104">作業の開始</span><span class="sxs-lookup"><span data-stu-id="fa147-104">Getting Started</span></span>

### <a name="downloading-the-prebuilt-files"></a><span data-ttu-id="fa147-105">ビルド済みファイルのダウンロード</span><span class="sxs-lookup"><span data-stu-id="fa147-105">Downloading the prebuilt files</span></span>

<span data-ttu-id="fa147-106">ビルド済みファイルは https://jqueryvalidation.org/ からダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="fa147-106">Prebuilt files can be downloaded from https://jqueryvalidation.org/</span></span>

### <a name="downloading-the-latest-changes"></a><span data-ttu-id="fa147-107">最新の変更のダウンロード</span><span class="sxs-lookup"><span data-stu-id="fa147-107">Downloading the latest changes</span></span>

<span data-ttu-id="fa147-108">リリース前の開発ファイルを以下の手順で入手できます。</span><span class="sxs-lookup"><span data-stu-id="fa147-108">The unreleased development files can be obtained by:</span></span>

 1. <span data-ttu-id="fa147-109">このリポジトリを[ダウンロード](https://github.com/jquery-validation/jquery-validation/archive/master.zip)またはフォークする</span><span class="sxs-lookup"><span data-stu-id="fa147-109">[Downloading](https://github.com/jquery-validation/jquery-validation/archive/master.zip) or Forking this repository</span></span>
 2. [<span data-ttu-id="fa147-110">ビルドを設定する</span><span class="sxs-lookup"><span data-stu-id="fa147-110">Setup the build</span></span>](CONTRIBUTING.md#build-setup)
 3. <span data-ttu-id="fa147-111">`grunt` を実行して "dist" ディレクトリ内にビルド済みのファイルを作成する</span><span class="sxs-lookup"><span data-stu-id="fa147-111">Run `grunt` to create the built files in the "dist" directory</span></span>

### <a name="including-it-on-your-page"></a><span data-ttu-id="fa147-112">プラグインをページに追加する</span><span class="sxs-lookup"><span data-stu-id="fa147-112">Including it on your page</span></span>

<span data-ttu-id="fa147-113">jQuery とこのプラグインをページに追加します。</span><span class="sxs-lookup"><span data-stu-id="fa147-113">Include jQuery and the plugin on a page.</span></span> <span data-ttu-id="fa147-114">その後、検証するフォームを選択して、`validate` メソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="fa147-114">Then select a form to validate and call the `validate` method.</span></span>

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

<span data-ttu-id="fa147-115">または、requirejs を使用して jQuery とこのプラグインをモジュールに追加します。</span><span class="sxs-lookup"><span data-stu-id="fa147-115">Alternatively include jQuery and the plugin via requirejs in your module.</span></span>

```js
define(["jquery", "jquery.validate"], function( $ ) {
    $("form").validate();
});
```

<span data-ttu-id="fa147-116">ルールおよびカスタマイズの設定方法の詳細については、[こちらのドキュメント](https://jqueryvalidation.org/documentation/)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="fa147-116">For more information on how to setup a rules and customizations, [check the documentation](https://jqueryvalidation.org/documentation/).</span></span>

## <a name="reporting-issues-and-contributing-code"></a><span data-ttu-id="fa147-117">問題の報告およびコードの投稿</span><span class="sxs-lookup"><span data-stu-id="fa147-117">Reporting issues and contributing code</span></span>

<span data-ttu-id="fa147-118">詳細については、[コントリビューションのガイドライン](CONTRIBUTING.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="fa147-118">See the [Contributing Guidelines](CONTRIBUTING.md) for details.</span></span>

<span data-ttu-id="fa147-119">**電子メール検証に関する重要な注意事項**.</span><span class="sxs-lookup"><span data-stu-id="fa147-119">**IMPORTANT NOTE ABOUT EMAIL VALIDATION**.</span></span> <span data-ttu-id="fa147-120">このプラグインは、バージョン 1.12.0 以降では [HTML5 の仕様でブラウザーでの使用が推奨されている](https://html.spec.whatwg.org/multipage/forms.html#valid-e-mail-address)正規表現を使用しています。</span><span class="sxs-lookup"><span data-stu-id="fa147-120">As of version 1.12.0 this plugin is using the same regular expression that the [HTML5 specification suggests for browsers to use](https://html.spec.whatwg.org/multipage/forms.html#valid-e-mail-address).</span></span> <span data-ttu-id="fa147-121">この手本に従い同じチェックが行われています。</span><span class="sxs-lookup"><span data-stu-id="fa147-121">We will follow their lead and use the same check.</span></span> <span data-ttu-id="fa147-122">HTML5 の仕様が正しくないと思われる場合は、そちらに問題を報告してください。</span><span class="sxs-lookup"><span data-stu-id="fa147-122">If you think the specification is wrong, please report the issue to them.</span></span> <span data-ttu-id="fa147-123">要件が異なる場合は、[カスタム メソッドの使用](https://jqueryvalidation.org/jQuery.validator.addMethod/)を検討してください。</span><span class="sxs-lookup"><span data-stu-id="fa147-123">If you have different requirements, consider [using a custom method](https://jqueryvalidation.org/jQuery.validator.addMethod/).</span></span>
<span data-ttu-id="fa147-124">組み込みの検証の正規表現パターンを調整する必要がある場合は、[ドキュメントに従ってください](https://jqueryvalidation.org/jQuery.validator.methods/)。</span><span class="sxs-lookup"><span data-stu-id="fa147-124">In case you need to adjust the built-in validation regular expression patterns, please [follow the documentation](https://jqueryvalidation.org/jQuery.validator.methods/).</span></span>

<span data-ttu-id="fa147-125">**必須メソッドに関する重要な注意事項**。</span><span class="sxs-lookup"><span data-stu-id="fa147-125">**IMPORTANT NOTE ABOUT REQUIRED METHOD**.</span></span> <span data-ttu-id="fa147-126">このプラグインは、バージョン 1.14.0 から、添付された要素の値からの空白文字のトリミングを行いません。</span><span class="sxs-lookup"><span data-stu-id="fa147-126">As of version 1.14.0 this plugin stops trimming white spaces from the value of the attached element.</span></span> <span data-ttu-id="fa147-127">以前と同様の結果が必要な場合は、[`normalizer`](https://jqueryvalidation.org/normalizer/) を使用して、検証の前に要素の値を変換することができます。</span><span class="sxs-lookup"><span data-stu-id="fa147-127">If you want to achieve the same result, you can use the [`normalizer`](https://jqueryvalidation.org/normalizer/) that can be used to transform the value of an element before validation.</span></span> <span data-ttu-id="fa147-128">この機能は `v1.15.0` から利用可能です。</span><span class="sxs-lookup"><span data-stu-id="fa147-128">This feature was available since `v1.15.0`.</span></span> <span data-ttu-id="fa147-129">つまり、次のような操作を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="fa147-129">In other words, you can do something like this:</span></span>
``` js
$("#myForm").validate({
    rules: {
        username: {
            required: true,
            // Using the normalizer to trim the value of the element
            // before validating it.
            //
            // The value of `this` inside the `normalizer` is the corresponding
            // DOMElement. In this example, `this` references the `username` element.
            normalizer: function(value) {
                return $.trim(value);
            }
        }
    }
});
```

## <a name="license"></a><span data-ttu-id="fa147-130">ライセンス</span><span class="sxs-lookup"><span data-stu-id="fa147-130">License</span></span>
<span data-ttu-id="fa147-131">Copyright &copy; Jörn Zaefferer</span><span class="sxs-lookup"><span data-stu-id="fa147-131">Copyright &copy; Jörn Zaefferer</span></span><br>
<span data-ttu-id="fa147-132">MIT ライセンスにより許諾されています。</span><span class="sxs-lookup"><span data-stu-id="fa147-132">Licensed under the MIT license.</span></span>
