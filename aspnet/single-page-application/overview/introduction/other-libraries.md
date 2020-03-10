---
uid: single-page-application/overview/introduction/other-libraries
title: Knockout 以外のライブラリを知っていますか? | Microsoft Docs
author: madskristensen
description: Knockout 以外のライブラリを知っていますか?
ms.author: riande
ms.date: 02/05/2013
ms.assetid: a8367c6d-ef94-4dff-a010-5eff9e6eea96
msc.legacyurl: /single-page-application/overview/introduction/other-libraries
msc.type: authoredcontent
ms.openlocfilehash: 64a4ad1fb411f7291a5cba634afdf4d2fdb16d55
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467194"
---
# <a name="know-a-library-other-than-knockout"></a>Knockout 以外のライブラリを知っていますか?

[Mads Kristensen](https://github.com/madskristensen)

シングルページ[アプリケーション (SPA) テンプレート](knockoutjs-template.md)は、シングルページアプリケーションの作成を開始するための優れた方法です。 このテンプレートでは、 [KnockoutJS](http://knockoutjs.com/)を使用して、アプリケーションデータを DOM 要素にバインドします。

しかし、ノックアウトは、リッチクライアントアプリケーションを作成するための唯一の JavaScript ライブラリではありません。 他のライブラリは、さまざまな方法で同様の課題を解決します。 別のライブラリを使用することもできます。そのため、コミュニティによって作成された複数のテンプレートをダウンロードできるようになりました。 これらの各テンプレートでは、さまざまなクライアント JavaScript ライブラリが使用されています。

コミュニティによって作成されたテンプレートをインストールするには、次のいずれかのテンプレートページにアクセスし、[ダウンロード] ボタンをクリックします。 テンプレートは、VSIX ファイルとして提供されます。

## <a name="backbonejs"></a>BackboneJS

[バックボーンの JS SPA テンプレート](../templates/backbonejs-template.md)。 このテンプレートは、ASP.NET MVC で[バックボーン](http://backbonejs.org/)アプリケーションを開発するための初期スケルトンを提供します。 既定では、ユーザーのサインアップ、サインイン、パスワードのリセット、基本的な電子メールテンプレートを使用したユーザーの確認など、基本的なユーザーログイン機能が提供されています。

## <a name="breezejs"></a>BreezeJS

[BreezeJS](http://www.breezejs.com/?utm_source=ms-spa)は、JavaScript クライアントでリッチデータを管理するためのオープンソースライブラリです。 クエリ、キャッシュ、変更の追跡、検証などを簡単に処理できます。 2つのテンプレート機能は簡単です。

- 簡単[/ノックアウト](../templates/breezeknockout-template.md)テンプレートによって、ノックアウト SPA テンプレートが拡張されます。これは、データの管理とデータバインドのための KnockoutJS が簡単な単一ページアプリケーションを簡単に作成できるようにするためのものです。
- また、簡単な[/角度](../templates/breezeangular-template.md)のテンプレートを使用すると、抜き合わせ SPA テンプレートも簡単に拡張できますが、データバインディング、依存関係の挿入、および画面管理には[AngularJS](http://angularjs.org)ライブラリが使用されます。

また、[ホットタオル SPA テンプレート](../templates/hottowel-template.md)では、BreezeJS が使用されます。

## <a name="emberjs"></a>EmberJS

[EMBERJS SPA テンプレート](../templates/emberjs-template.md)。 このテンプレートは、リッチクライアントアプリケーションを構築するためのさまざまな課題を解決する強力な MVC JavaScript ライブラリである[ember.js](http://emberjs.com/)を使用します。

Ember.js SPA テンプレートは、EmberJS とハンドルテンプレートを使用した、ノックアウト SPA テンプレートの再実装です。

## <a name="hot-towel"></a>ホットタオル

[ホットタオル SPA テンプレート](../templates/hottowel-template.md)。 このテンプレートには、簡単、ノックアウト、RequireJS、Twitter のブートストラップなど、いくつかの JavaScript ライブラリが用意されています。

ここに記載されている他のテンプレートと比較して、Hot タオルテンプレートには、独自のアプリケーションを作成するための、より完全なアプリケーションが用意されています。 注意すべき概念は他にもありますが、理解しておくと、このテンプレートは探しているものになる可能性があります。 SPA を構築するが、どこから開始するかを決定できない場合は、ホットタオルを使用します。数秒で SPA と、それに必要なすべてのツールが用意されています。

## <a name="feature-table"></a>機能テーブル

各 SPA テンプレートによって提供される機能を次に示します。

|                        | ASP.NET SPA | バックボーン | 簡単/角度 | 簡単/KO |  Ember.js   | ホットタオル |
|------------------------|-------------|----------|----------------|-----------|----------|-----------|
|      ToDo サンプル       |  &#10003;   |          |    &#10003;    | &#10003;  | &#10003; |           |
|     ベアテンプレート      |             | &#10003; |                |           |          | &#10003;  |
| ナビゲーションと履歴 |             | &#10003; |    &#10003;    |           | &#10003; | &#10003;  |
|        ライブラリ       |             |          |                |           |          |           |
|        Angular         |             |          |    &#10003;    |           |          |           |
|    &#8195;バックボーン     |             | &#10003; |                |           |          |           |
|         風         |             |          |    &#10003;    | &#10003;  |          | &#10003;  |
|        durandal        |             |          |                |           |          | &#10003;  |
|         Ember.js          |             |          |                |           | &#10003; |           |
|        抜き合わせ        |  &#10003;   |          |                | &#10003;  |          | &#10003;  |
