---
uid: single-page-application/overview/templates/emberjs-template
title: EmberJS template |Microsoft Docs
author: xqiu
description: EmberJS テンプレート
ms.author: riande
ms.date: 01/30/2013
ms.assetid: 04d5f142-5f62-494a-b5ea-4f3d068d34cb
msc.legacyurl: /single-page-application/overview/templates/emberjs-template
msc.type: authoredcontent
ms.openlocfilehash: 1aefa46dd0841b1b06675409cc8a09f9a218d7ac
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467158"
---
# <a name="emberjs-template"></a>EmberJS テンプレート

[Xinyang Qiu](https://github.com/xqiu)

> EmberJS MVC テンプレートは、Nathan、Thiago Santos、および Xinyang Qiu によって作成されています。
> 
> [EmberJS MVC テンプレートをダウンロードする](https://go.microsoft.com/fwlink/?LinkId=282647)

EmberJS SPA テンプレートは、EmberJS を使用して、対話型のクライアント側 web アプリの構築をすぐに開始できるように設計されています。

"シングルページアプリケーション" (SPA) は、1つの HTML ページを読み込み、新しいページを読み込むのではなく、ページを動的に更新する web アプリケーションの一般的な用語です。 最初のページの読み込み後、SPA は AJAX 要求によってサーバーと通信します。

![](emberjs-template/_static/image1.png)

AJAX はまったく新しいものではありませんが、今日では、大規模な高度な SPA アプリケーションを簡単に構築して維持できる JavaScript フレームワークが用意されています。 また、HTML 5 と CSS3 は、豊富な Ui の作成を容易にします。

EmberJS SPA テンプレートでは、 [Ember.js](http://emberjs.com/) JavaScript ライブラリを使用して、AJAX 要求からのページ更新を処理します。 Ember.js は、データバインディングを使用して、ページを最新のデータと同期します。 このようにして、JSON データを処理するコードを記述して DOM を更新する必要はありません。 代わりに、データの表示方法を Ember.js に指示する宣言型の属性を HTML に配置します。

サーバー側では、EmberJS テンプレートは[KNOCKOUTJS SPA テンプレート](../introduction/knockoutjs-template.md)とほぼ同じです。 ASP.NET MVC を使用して HTML ドキュメントを提供し、ASP.NET Web API クライアントからの AJAX 要求を処理します。 テンプレートのこれらの側面の詳細については、 [KnockoutJS テンプレート](../introduction/knockoutjs-template.md)のドキュメントを参照してください。 このトピックでは、ノックアウトテンプレートと EmberJS テンプレートの違いについて説明します。

## <a name="create-an-emberjs-spa-template-project"></a>EmberJS SPA テンプレートプロジェクトを作成する

上の [ダウンロード] ボタンをクリックして、テンプレートをダウンロードしてインストールします。 場合によっては、Visual Studio を再起動する必要があります。

**[テンプレート]** ペインで、 **[インストールされたテンプレート]** を選択し、  **C#ビジュアル**ノードを展開します。 **[ビジュアルC# ]** で **[Web]** を選択します。 プロジェクトテンプレートの一覧で、 **[ASP.NET MVC 4 Web アプリケーション]** を選択します。 プロジェクト名を指定して、 **[OK]** をクリックします。

![](emberjs-template/_static/image2.png)

**新しいプロジェクト**ウィザードで、 **[ember.js SPA プロジェクト]** を選択します。

![](emberjs-template/_static/image4.png)

## <a name="emberjs-spa-template-overview"></a>EmberJS SPA テンプレートの概要

EmberJS テンプレートでは、jQuery、Ember.js、ハンドルの組み合わせを使用して、スムーズで対話型の UI を作成します。

Ember.js は、クライアント側の MVC パターンを使用する JavaScript ライブラリです。

- ハンドルテンプレート言語で記述された*テンプレート*は、アプリケーションのユーザーインターフェイスについて説明します。 リリースモードでは、[ハンドルコンパイラ](https://github.com/Myslik/csharp-ember-handlebars)を使用してハンドルテンプレートをバンドルし、コンパイルします。
- *モデル*には、サーバーから取得したアプリケーションデータ (todo リストと todo 項目) が格納されます。
- *コントローラー*は、アプリケーションの状態を格納します。 多くの場合、コントローラーは対応するテンプレートにモデルデータを提示します。
- *ビュー*は、プリミティブイベントをアプリケーションから変換し、コントローラーに渡します。
- *ルーター*は、url とテンプレートの同期を維持しながら、アプリケーションの状態を管理します。

また、Ember.js Data library を使用して、(RESTful API を使用してサーバーから取得した) JSON オブジェクトとクライアントモデルを同期できます。

EmberJS SPA テンプレートでは、スクリプトが8つのレイヤーに編成されます。

- webapi\_webapi\_serializer: Ember.js Data library を拡張して ASP.NET Web API を操作します。
- Scripts/Ember.js: 新しいハンドルヘルパーを定義します。
- Scripts/app.config: アプリを作成し、アダプターとシリアライザーを構成します。
- Scripts/app/model/\*.js: モデルを定義します。
- Scripts/app/views/\*.js: ビューを定義します。
- Scripts/app/controllers/\*.js: コントローラーを定義します。
- Scripts/app/route, Scripts/app/router js: ルートを定義します。
- Templates/\*: ハンドルテンプレートを定義します。

これらのスクリプトのいくつかをさらに詳しく見てみましょう。

## <a name="models"></a>モデル

モデルは、[スクリプト/アプリ/モデル] フォルダーで定義されています。 TodoItem と todoList という2つのモデルファイルがあります。

**todo。モデル**は、to do リストのクライアント側 (ブラウザー) モデルを定義します。 モデルクラスには、todoItem と todoList の2つがあります。 Ember.js では、モデルは DS のサブクラスです。型. モデルには、属性を持つプロパティを含めることができます。

[!code-javascript[Main](emberjs-template/samples/sample1.js)]

モデルでは、他のモデルとのリレーションシップを定義できます。

[!code-css[Main](emberjs-template/samples/sample2.css)]

モデルは、他のプロパティにバインドする計算されたプロパティを持つことができます。

[!code-javascript[Main](emberjs-template/samples/sample3.js)]

モデルには、観察されたプロパティが変更されたときに呼び出されるオブザーバー関数を含めることができます。

[!code-javascript[Main](emberjs-template/samples/sample4.js)]

## <a name="views"></a>ビュー

ビューは、Scripts/app/views フォルダーで定義されています。 ビューは、アプリケーション UI からのイベントを変換します。 イベントハンドラーは、コントローラー関数にコールバックすることも、単にデータコンテキストを直接呼び出すこともできます。

たとえば、次のコードは views/TodoItemEditView からのものです。 入力テキストフィールドのイベント処理を定義します。

[!code-javascript[Main](emberjs-template/samples/sample5.js)]

## <a name="controller"></a>コントローラー

コントローラーは、Scripts/app/controllers フォルダーで定義されています。 1つのモデルを表すには、`Ember.ObjectController`を拡張します。

[!code-javascript[Main](emberjs-template/samples/sample6.js)]

コントローラーは、`Ember.ArrayController`を拡張することによって、モデルのコレクションを表すこともできます。 たとえば、Todolistcontroller.cs は `todoList` オブジェクトの配列を表します。 コントローラーは、todoList ID で降順に並べ替えます。

[!code-javascript[Main](emberjs-template/samples/sample7.js)]

コントローラーは `addTodoList`という名前の関数を定義します。この関数は、新しい todoList を作成して配列に追加します。 この関数がどのように呼び出されるかを確認するには、テンプレートフォルダーで todoListTemplate という名前のテンプレートファイルを開きます。 次のテンプレートコードは、ボタンを `addTodoList` 関数にバインドします。

[!code-html[Main](emberjs-template/samples/sample8.html)]

このコントローラーには、エラーメッセージを保持する `error` プロパティも含まれています。 エラーメッセージを表示するためのテンプレートコードを次に示します (todoListTemplate でも同様)。

[!code-html[Main](emberjs-template/samples/sample9.html)]

## <a name="routes"></a>ルート

Router は、表示するルートと既定のテンプレートを定義し、アプリケーションの状態を設定して、Url をルートに一致させることができます。

[!code-javascript[Main](emberjs-template/samples/sample10.js)]

TodoListRoute は、setupController 関数をオーバーライドすることによって、TodoListRoute のデータを読み込みます。

[!code-javascript[Main](emberjs-template/samples/sample11.js)]

Ember.js は、Url、ルート名、コントローラー、およびテンプレートを一致させるために名前付け規則を使用します。 詳細については、EmberJS のドキュメントの「 [http://emberjs.com/guides/routing/defining-your-routes/](http://emberjs.com/guides/routing/defining-your-routes/) 」を参照してください。

## <a name="templates"></a>テンプレート

Templates フォルダーには、次の4つのテンプレートが含まれています。

- application. hbs: アプリケーションの起動時に表示される既定のテンプレート。
- about. hbs: "/about" ルートのテンプレート。
- index. hbs: ルート "/" ルートのテンプレート。
- todoList: "/todo" ルートのテンプレート。
- \_のナビゲーションバー: テンプレートは、ナビゲーションメニューを定義します。

アプリケーションテンプレートは、マスターページのように機能します。 ルートに応じて、に他のテンプレートを挿入するためのヘッダー、フッター、および "{{アウトレット}}" が含まれています。 Ember.js のアプリケーションテンプレートの詳細については、「 [http://guides.emberjs.com/v1.10.0/templates/the-application-template//](http://guides.emberjs.com/v1.10.0/templates/the-application-template/)」を参照してください。

"/TodoList" テンプレートには、2つのループ式が含まれています。 外側のループが `{{#each controller}}`、内側のループが `{{#each todos}}`。 次のコードは、組み込みの `Ember.Checkbox` ビュー、カスタマイズされた `App.TodoItemEditView`、および `deleteTodo` アクションを含むリンクを示しています。

[!code-html[Main](emberjs-template/samples/sample12.html)]

`HtmlHelperExtensions` クラスは、Controllers/Htmlによって定義されます。これは、web.config ファイルで**debug**が**true**に設定されている場合に、テンプレートファイルをキャッシュおよび挿入するためのヘルパー関数を定義します。 この関数は、Views/Home/App.xaml に定義されている ASP.NET MVC ビューファイルから呼び出されます。

[!code-cshtml[Main](emberjs-template/samples/sample13.cshtml)]

引数を指定せずに呼び出された関数は、Templates フォルダー内のすべてのテンプレートファイルを表示します。 サブフォルダーまたは特定のテンプレートファイルを指定することもできます。

Web.config で**debug**が**false**の場合、バンドル項目 "~/bundles/templates" がアプリケーションに含まれます。 このバンドル項目は、ハンドルコンパイラライブラリを使用して BundleConfig.cs に追加されます。

[!code-csharp[Main](emberjs-template/samples/sample14.cs)]
