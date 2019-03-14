---
ms.openlocfilehash: 83a958fe6a8d61becf9f9062e8ad0ff69108b435
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57034989"
---
<a name="jquery-validation-pluginhttpjqueryvalidationorg---form-validation-made-easy"></a>[jQuery Validation プラグイン](http://jqueryvalidation.org/) - フォームの検証を簡単に作成
================================

[![ビルドの状態](https://secure.travis-ci.org/jzaefferer/jquery-validation.png)](http://travis-ci.org/jzaefferer/jquery-validation)
[![devDependency の状態](https://david-dm.org/jzaefferer/jquery-validation/dev-status.png?theme=shields.io)](https://david-dm.org/jzaefferer/jquery-validation#info=devDependencies)

jQuery Validation プラグインでは既存のフォーム用にドロップイン検証を使用でき、さらにアプリケーションにあらゆるカスタマイズを非常に簡単に合わせることができます。

## <a name="help-the-projecthttppledgiecomcampaigns18159"></a>[プロジェクトを支援する](http://pledgie.com/campaigns/18159)

[![プロジェクトを支援する](http://www.pledgie.com/campaigns/18159.png?skin_name=chrome)](http://pledgie.com/campaigns/18159)

ご支援をお願いいたします。 [現在実施中の pledgie キャンペーンでご寄付を受け付けています](http://pledgie.com/campaigns/18159)。また、プラグインの評判を広めてください。 プラグインを使用したことがあるか、使用するつもりの場合は、少額でも結構ですのでご寄付をお願いします。

寄附金の使用計画については、[pledgie のページ](http://pledgie.com/campaigns/18159)に記載しています。

## <a name="getting-started"></a>作業の開始

### <a name="downloading-the-prebuilt-files"></a>ビルド済みファイルのダウンロード

ビルド済みファイルは http://jqueryvalidation.org/ からダウンロードできます。

### <a name="downloading-the-latest-changes"></a>最新の変更のダウンロード

リリース前の開発ファイルを以下の手順で入手できます。

 1. このリポジトリを[ダウンロード](https://github.com/jzaefferer/jquery-validation/archive/master.zip)またはフォークする
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

ルールおよびカスタマイズの設定方法の詳細については、[こちらのドキュメント](http://jqueryvalidation.org/documentation/)を参照してください。

## <a name="reporting-issues-and-contributing-code"></a>問題の報告およびコードの投稿

詳細については、[コントリビューションのガイドライン](CONTRIBUTING.md)を参照してください。

**電子メール検証に関する重要な注意事項**. このプラグインは、バージョン 1.12.0 以降では [HTML5 の仕様でブラウザーでの使用が推奨されている](https://html.spec.whatwg.org/multipage/forms.html#valid-e-mail-address)正規表現を使用しています。 この手本に従い同じチェックが行われています。 HTML5 の仕様が正しくないと思われる場合は、そちらに問題を報告してください。 要件が異なる場合は、[カスタム メソッドの使用](http://jqueryvalidation.org/jQuery.validator.addMethod/)を検討してください。

## <a name="license"></a>ライセンス
Copyright &copy; Jörn Zaefferer<br>
MIT ライセンスにより許諾されています。
