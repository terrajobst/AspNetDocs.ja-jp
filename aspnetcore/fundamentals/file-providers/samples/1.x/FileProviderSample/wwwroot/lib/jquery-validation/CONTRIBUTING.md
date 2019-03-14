---
ms.openlocfilehash: 7eb0f9b556f0663a5208310d2d4864eca28f8632
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57057349"
---
# <a name="contributing-to-the-jquery-validation-plugin"></a>jQuery Validation プラグインに投稿する

## <a name="reporting-an-issue"></a>問題の報告

1. 報告する問題が再現可能であることを確認してください。
2. https://jsbin.com または https://jsfiddle.net を使用してテスト ページを提供します。
3. 問題を再現できるブラウザーを記載してください。 **注:IE の互換性モードの問題には解決されません。テストは実際のブラウザーで行ってください。**
4. 問題を再現可能なプラグインのバージョンを記載してください。 最新バージョンへの更新後も問題が再発するか確認してください。

ドキュメントの問題は、[jQuery 検証](https://github.com/jquery-validation/jquery-validation/issues) の issue トラッカーでも追跡されています。
ドキュメントに関するPull Requests も [jQuery 検証のドキュメント](https://github.com/jquery-validation/validation-content) リポジトリにお寄せください。

**電子メール検証に関する重要な注意事項**. このプラグインは、バージョン 1.12.0 以降では [HTML5 の仕様でブラウザーでの使用が推奨されている](https://html.spec.whatwg.org/multipage/forms.html#valid-e-mail-address)正規表現を使用しています。 この手本に従い同じチェックが行われています。 HTML5 の仕様が正しくないと思われる場合は、そちらに問題を報告してください。 要件が異なる場合は、[カスタム メソッドの使用](http://jqueryvalidation.org/jQuery.validator.addMethod/)を検討してください。
組み込みの検証の正規表現パターンを調整する必要がある場合は、[ドキュメントに従ってください](http://jqueryvalidation.org/jQuery.validator.methods/)。

## <a name="contributing-code"></a>コードの投稿

投稿してくださりありがとうございます。 以下に、投稿が受け入られやすくなるいくつかのガイドラインを示します。

1. 報告する問題が再現可能であることを確認してください。 jsbin.com または jsfiddle.net を使用してテスト ページを用意してください。
2. [jQuery のスタイル ガイド](http://contribute.jquery.com/style-guides/js)に従ってください。
3. パッチとともに単体テストを追加するか更新してください。 1 つ以上のブラウザーで単体テストを実行してください (下記参照)。
4. `grunt` (下記参照) を実行して、lint およびその他のいくつかの問題をチェックしてください。
5. コミット メッセージの変更を説明し、次のように、チケットの参照します。"デモ。dynamic-totals デモのデリゲート バグを修正しました。 #51 の修正” のように記載してください。 新しいローカライズ ファイルを追加する場合は、このようなものを使用します。"ローカリゼーション。追加されたクロアチア語 (HR) のローカリゼーション"

## <a name="build-setup"></a>ビルドのセットアップ

1. [NodeJS](http://nodejs.org) をインストールします。
2. `npm install -g grunt-cli` を実行して、Grunt CLI をインストールします。 詳細については、Web サイト (http://gruntjs.com/getting-started) を参照してください。
3. `npm install` を実行して、NPM の依存パッケージをインストールします。
4. これで、`grunt` を実行してビルドを呼び出せるようになりました。

## <a name="creating-a-new-additional-method"></a>新しい追加メソッドの作成

additional-methods.js に投稿するカスタム メソッドを作成した場合は、次の手順に従ってください。

1. 分岐を作成する
2. メソッドを `src/additional` に新しいファイルとして追加する
3. (省略可能) `src/localization` に翻訳を追加する
4. マスター ブランチに pull request 送信する。

## <a name="unit-tests"></a>単体テスト

単体テストを実行するには、ブラウザーで `test/index.html` を開きます。 テストの前に、`npm install` を実行して必要な依存パッケージをすべて揃えてください。
修正プログラムの作成中は 1 つのブラウザーで作業し、コミットの前に別のブラウザーで実行します。 最新の Chrome、Firefox、Safari、Opera の使用が一般的であり、IE は少数です。

## <a name="documentation"></a>ドキュメント

ドキュメントの問題は、[jQuery 検証](https://github.com/jquery-validation/jquery-validation/issues) の issue トラッカーで報告してください。
pull request でパブリック API を実装または変更する場合は、さらに [jQuery 検証のドキュメント](https://github.com/jquery-validation/validation-content) リポジトリにプル要求を提供してください。

## <a name="linting"></a>Lint

`grunt` を使用して、JSHint などのツールを実行します。
