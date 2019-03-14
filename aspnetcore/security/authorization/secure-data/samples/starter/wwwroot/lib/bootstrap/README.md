---
ms.openlocfilehash: 3be420696add54094f24424285a905e7e7963bad
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57050749"
---
# <a name="bootstraphttpgetbootstrapcom"></a>[Bootstrap](http://getbootstrap.com)

[![Slack](https://bootstrap-slack.herokuapp.com/badge.svg)](https://bootstrap-slack.herokuapp.com)
![Bower バージョン](https://img.shields.io/bower/v/bootstrap.svg)
[![npm バージョン](https://img.shields.io/npm/v/bootstrap.svg)](https://www.npmjs.com/package/bootstrap)
[![ビルドの状態](https://img.shields.io/travis/twbs/bootstrap/master.svg)](https://travis-ci.org/twbs/bootstrap)
[ ![devDependency の状態](https://img.shields.io/david/dev/twbs/bootstrap.svg)](https://david-dm.org/twbs/bootstrap#info=devDependencies)
[![NuGet](https://img.shields.io/nuget/v/bootstrap.svg)](https://www.nuget.org/packages/Bootstrap)
[![Selenium テストの状態](https://saucelabs.com/browser-matrix/bootstrap.svg)](https://saucelabs.com/u/bootstrap)

Bootstrap は、Web 開発を高速かつ簡単に行うことができるスムーズで直感的な高性能フロントエンド フレームワークであり、[Mark Otto](https://twitter.com/mdo) および [Jacob Thornton](https://twitter.com/fat) が作成し、[コア チーム](https://github.com/orgs/twbs/people)とコミュニティの温かいご支援と協力によって管理されています。

最初に、<http://getbootstrap.com> をご覧ください。


## <a name="table-of-contents"></a>目次

* [クイック スタート](#quick-start)
* [バグおよび機能に関する要望](#bugs-and-feature-requests)
* [ドキュメント](#documentation)
* [コントリビューション](#contributing)
* [Community](#community)
* [バージョン管理](#versioning)
* [作成者](#creators)
* [著作権およびライセンス](#copyright-and-license)


## <a name="quick-start"></a>クイック スタート

クイック スタートの選択肢は次のとおりです。

* [最新のリリースをダウンロードする](https://github.com/twbs/bootstrap/archive/v3.3.7.zip).
* リポジトリを複製する: `git clone https://github.com/twbs/bootstrap.git`
* [Bower](http://bower.io) を使用してインストールする: `bower install bootstrap`
* [npm](https://www.npmjs.com) を使用してインストールする: `npm install bootstrap@3`
* [Meteor](https://www.meteor.com) を使用してインストールする: `meteor add twbs:bootstrap`
* [Composer](https://getcomposer.org) を使用してインストールする: `composer require twbs/bootstrap`

このフレームワークの内容、テンプレート、サンプルなどについては、[使用開始](http://getbootstrap.com/getting-started/)に関するページを参照してください。

### <a name="whats-included"></a>内容

このダウンロードには、共通アセットを論理的にグループ分けした以下のディレクトリとファイルが含まれており、コンパイル済みのバリエーションおよび縮小版のバリエーションが用意されています。 内容は以下のとおりです。

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

コンパイル済みの CSS と JS (`bootstrap.*`)、およびコンパイル済みの縮小版 CSS と JS (`bootstrap.min.*`) が含まれています。 一部のブラウザーの開発者ツール用に、CSS [ソース マップ](https://developer.chrome.com/devtools/docs/css-preprocessors) (`bootstrap.*.map`) も用意されています。 オプションの Bootstrap テーマである Glyphicons のフォントも含まれています。


## <a name="bugs-and-feature-requests"></a>バグおよび機能に関する要望

バグが発生した場合、または機能に関する要望がある場合は、 まず [issue のガイドライン](https://github.com/twbs/bootstrap/blob/master/CONTRIBUTING.md#using-the-issue-tracker)をご覧になり、既存の issue および解決済みの issue を検索してください。 それでも問題が解決されない場合、またはアイデアが反映されていない場合は、[新しい issue を開始してください](https://github.com/twbs/bootstrap/issues/new)。

なお、Bootstrap バージョン 3 は現在メンテナンス モードであり新機能の追加は行われていないため、**機能に関する要望については [Bootstrap バージョン 4](https://github.com/twbs/bootstrap/tree/v4-dev)** にお寄せください。 Bootstrap バージョン 4 の開発に専念するためこのようにしていることをご了承ください。


## <a name="documentation"></a>ドキュメント

このリポジトリのルート ディレクトリに含まれる Bootstrap のドキュメントは、[Jekyll](http://jekyllrb.com) で作成され、GitHub のページ (<http://getbootstrap.com>) でホストされ公開されています。 ドキュメントはローカルで確認することもできます。

### <a name="running-documentation-locally"></a>ドキュメントをローカルで確認する

1. 必要に応じて、`bundle install` を使用して、[Jekyll](http://jekyllrb.com/docs/installation) とその他の Ruby の依存パッケージをインストールします。
   **Windows のユーザーに対する注意:** 読み取り[この非公式ガイド](http://jekyll-windows.juthilo.com/)を問題なく稼働して Jekyll を取得します。
2. コマンド ラインで、ルートの `/bootstrap` ディレクトリから `bundle exec jekyll serve` を実行します。
4. ブラウザーで `http://localhost:9001` にアクセスします。

Jekyll の使用方法の詳細については、Jekyll の[ドキュメント](http://jekyllrb.com/docs/home/)を参照してください。

### <a name="documentation-for-previous-releases"></a>以前のリリースのドキュメント

バージョン 2.3.2 のドキュメントは、各ユーザーの Bootstrap 3 への切り替えが行われている間は、当面 <http://getbootstrap.com/2.3.2/> で公開されています。

[以前のリリース](https://github.com/twbs/bootstrap/releases)およびドキュメントもダウンロード可能です。


## <a name="contributing"></a>コントリビューション

[コントリビューションに関するガイドライン](https://github.com/twbs/bootstrap/blob/master/CONTRIBUTING.md)のページをご覧ください。 issue の作成方法、コード作成規則、および開発に関する注意事項について説明しています。

また、pull request に JavaScript パッチまたは機能を含める場合は、[関連する単体テスト](https://github.com/twbs/bootstrap/tree/master/js/tests)も含めてください。 HTML および CSS はすべて、[コード ガイド](https://github.com/mdo/code-guide) ([Mark Otto](https://github.com/mdo) 作成) に準拠している必要があります。

**現在、Bootstrap バージョン 3 への新機能の追加は終了しています。** 今後のフレームワークである [Bootstrap バージョン 4](https://github.com/twbs/bootstrap/tree/v4-dev) に専念するため、こちらはメンテナンス モードとなっています。 バグの修正ではなく新機能の追加を行う pull requests のターゲットは、[Bootstrap バージョン 4 (`v4-dev` git ブランチ)](https://github.com/twbs/bootstrap/tree/v4-dev) としてください。

[エディターの環境設定](https://github.com/twbs/bootstrap/blob/master/.editorconfig)に関するページでは、一般的なテキスト エディターで簡単に使用できるエディターの基本設定が公開されています。 <http://editorconfig.org> で詳細を確認し、プラグインをダウンロードしてください。


## <a name="community"></a>コミュニティ

Bootstrap の開発の最新状況の確認、およびプロジェクト管理者およびコミュニティ メンバーとのやり取りを行うことができます。

* [Twitter で @getbootstrap](https://twitter.com/getbootstrap) をフォローしてください。
* [Bootstrap の公式ブログ](http://blog.getbootstrap.com)をご覧になり、購読してください。
* [公式 のSlack ルーム](https://bootstrap-slack.herokuapp.com)に参加してください。
* IRC で Bootstrap ユーザーとチャットしてください。 `irc.freenode.net` サーバーの `##bootstrap` チャンネルをご覧ください。
* 実装に関するヘルプについては、Stack Overflow (タグ [`twitter-bootstrap-3`](https://stackoverflow.com/questions/tagged/twitter-bootstrap-3)) をご覧ください。
* 開発者の方は、Bootstrap の機能を変更または追加するパッケージを [npm](https://www.npmjs.com/browse/keyword/bootstrap) で配布する場合、できるだけ多くのユーザーが見つけることができるよう `bootstrap` キーワードや同様の検出メカニズムを使用してください。


## <a name="versioning"></a>バージョン管理

リリース サイクルの透明化および後方互換性の維持のため、Bootstrap は[セマンティック バージョニングのガイドライン](http://semver.org/)に従い管理されています。 これらのルールを守ることができない場合もありますが、可能な限り遵守しています。

Bootstrap の各リリース バージョンの変更ログについては、GitHub プロジェクトの「[Releases (リリース)](https://github.com/twbs/bootstrap/releases)」ページを参照してください。 各リリースで行われた重要な変更の概要については、[Bootstrap の公式ブログ](http://blog.getbootstrap.com)のリリース告知記事に掲載されています。


## <a name="creators"></a>作成者

**Mark Otto**

* <https://twitter.com/mdo>
* <https://github.com/mdo>

**Jacob Thornton**

* <https://twitter.com/fat>
* <https://github.com/fat>


## <a name="copyright-and-license"></a>著作権およびライセンス

2011 年 - 2016 年のコードおよびドキュメントの著作権は Twitter, Inc. に帰属します。コードは [MIT ライセンス](https://github.com/twbs/bootstrap/blob/master/LICENSE)に従い公開されています。 ドキュメントは[クリエイティブ コモンズ](https://github.com/twbs/bootstrap/blob/master/docs/LICENSE)に従い公開されています。
