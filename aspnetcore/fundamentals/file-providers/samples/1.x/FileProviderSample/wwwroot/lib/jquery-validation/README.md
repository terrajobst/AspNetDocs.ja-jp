---
ms.openlocfilehash: 24c36493284988aa45b15c78e2577c0ef96aba56
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57029989"
---
<a name="jquery-validation-pluginhttpsjqueryvalidationorg---form-validation-made-easy"></a>[jQuery Validation プラグイン](https://jqueryvalidation.org/) - フォームの検証を簡単に作成
================================

[![ビルドの状態](https://secure.travis-ci.org/jquery-validation/jquery-validation.svg)](https://travis-ci.org/jquery-validation/jquery-validation)
[![devDependency の状態](https://david-dm.org/jquery-validation/jquery-validation/dev-status.svg?theme=shields.io)](https://david-dm.org/jquery-validation/jquery-validation#info=devDependencies)

jQuery Validation プラグインでは既存のフォーム用にドロップイン検証を使用でき、さらにアプリケーションにあらゆるカスタマイズを非常に簡単に合わせることができます。

## <a name="getting-started"></a>作業の開始

### <a name="downloading-the-prebuilt-files"></a>ビルド済みファイルのダウンロード

ビルド済みファイルは https://jqueryvalidation.org/ からダウンロードできます。

### <a name="downloading-the-latest-changes"></a>最新の変更のダウンロード

リリース前の開発ファイルを以下の手順で入手できます。

 1. このリポジトリを[ダウンロード](https://github.com/jquery-validation/jquery-validation/archive/master.zip)またはフォークする
 2. [ビルドを設定する](CONTRIBUTING.md#build-setup)
 3. `grunt` を実行して "dist" ディレクトリ内にビルド済みのファイルを作成する

### <a name="including-it-on-your-page"></a>プラグインをページに追加する

jQuery とこのプラグインをページに追加します。 その後、検証するフォームを選択して、`validate` メソッドを呼び出します。

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

または、requirejs を使用して jQuery とこのプラグインをモジュールに追加します。

```js
define(["jquery", "jquery.validate"], function( $ ) {
    $("form").validate();
});
```

ルールおよびカスタマイズの設定方法の詳細については、[こちらのドキュメント](https://jqueryvalidation.org/documentation/)を参照してください。

## <a name="reporting-issues-and-contributing-code"></a>問題の報告およびコードの投稿

詳細については、[コントリビューションのガイドライン](CONTRIBUTING.md)を参照してください。

**電子メール検証に関する重要な注意事項**. このプラグインは、バージョン 1.12.0 以降では [HTML5 の仕様でブラウザーでの使用が推奨されている](https://html.spec.whatwg.org/multipage/forms.html#valid-e-mail-address)正規表現を使用しています。 この手本に従い同じチェックが行われています。 HTML5 の仕様が正しくないと思われる場合は、そちらに問題を報告してください。 要件が異なる場合は、[カスタム メソッドの使用](https://jqueryvalidation.org/jQuery.validator.addMethod/)を検討してください。
組み込みの検証の正規表現パターンを調整する必要がある場合は、[ドキュメントに従ってください](https://jqueryvalidation.org/jQuery.validator.methods/)。

**必須メソッドに関する重要な注意事項**。 このプラグインは、バージョン 1.14.0 から、添付された要素の値からの空白文字のトリミングを行いません。 以前と同様の結果が必要な場合は、[`normalizer`](https://jqueryvalidation.org/normalizer/) を使用して、検証の前に要素の値を変換することができます。 この機能は `v1.15.0` から利用可能です。 つまり、次のような操作を行うことができます。
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

## <a name="license"></a>ライセンス
Copyright &copy; Jörn Zaefferer<br>
MIT ライセンスにより許諾されています。
