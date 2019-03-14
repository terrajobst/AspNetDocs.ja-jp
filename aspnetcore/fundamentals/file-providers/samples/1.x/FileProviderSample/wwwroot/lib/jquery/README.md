---
ms.openlocfilehash: 610b16b181422978dc143b95f28658bbdf177fdd
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57028279"
---
# <a name="jquery"></a>jQuery

> jQuery は、高速で軽量な、豊富な機能を備えた JavaScript ライブラリです。

jQuery の開始方法と使用方法については、[jQuery のドキュメント](http://api.jquery.com/)をご覧ください。
ソース ファイルと問題については、[jQuery のリポジトリ](https://github.com/jquery/jquery)を参照してください。

アップグレードする場合は、[3.3.1 に向けたブログ記事](https://blog.jquery.com/2017/03/20/jquery-3.3.1-now-available/)をご覧ください。 これには、以前のバージョンからの重要な違いと、よりわかりやすい変更ログが含まれています。

## <a name="including-jquery"></a>jQuery のインクルード

jQuery をインクルードする最も一般的な方法を、次にいくつか示します。

### <a name="browser"></a>ブラウザー

#### <a name="script-tag"></a>スクリプト タグ

```html
<script src="https://code.jquery.com/jquery-3.3.1.min.js"></script>
```

#### <a name="babel"></a>Babel

[Babel](http://babeljs.io/) は次世代の JavaScript コンパイラです。 その特徴の 1 つは、ES6/ES2015 モジュールを使用できることです。ブラウザーでは、この機能はまだネイティブではサポートされていません。

```js
import $ from "jquery";
```

#### <a name="browserifywebpack"></a>Browserify/Webpack

[Browserify](http://browserify.org/) と [Webpack](https://webpack.github.io/) を使用する方法はいくつかあります。 これらのツールの使用について詳しくは、対応するプロジェクトのドキュメントを参照してください。 スクリプトで jQuery をインクルードする場合は、通常、このようになります。

```js
var $ = require("jquery");
```

#### <a name="amd-asynchronous-module-definition"></a>AMD (非同期モジュール定義)

AMD は、ブラウザー用にビルドされたモジュール形式です。 詳細については、[require.js のドキュメント](http://requirejs.org/docs/whyamd.html)をお勧めします。

```js
define(["jquery"], function($) {

});
```

### <a name="node"></a>ノード

[Node](nodejs.org) に jQuery を含めるには、最初に npm でインストールします。

```sh
npm install jquery
```

jQuery を Node 内で動作させるには、ドキュメント ウィンドウが必要です。 Node にはそのようなウィンドウがネイティブで備わっていないため、[jsdom](https://github.com/tmpvar/jsdom) のようなツールで仮に用意されています。 これはテストのために役立ちます。

```js
require("jsdom").env("", function(err, window) {
    if (err) {
        console.error(err);
        return;
    }

    var $ = require("jquery")(window);
});
```
