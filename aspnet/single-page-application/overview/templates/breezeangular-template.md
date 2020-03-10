---
uid: single-page-application/overview/templates/breezeangular-template
title: 簡単/角度のテンプレート |Microsoft Docs
author: madskristensen
description: 簡単/角度のシングルページアプリケーションテンプレート
ms.author: riande
ms.date: 03/08/2013
ms.assetid: db31e909-563a-4516-aadd-62aa210ac7e4
msc.legacyurl: /single-page-application/overview/templates/breezeangular-template
msc.type: authoredcontent
ms.openlocfilehash: 3e4e63d385a56d51d3d08696782b43d6228f6201
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467188"
---
# <a name="breezeangular-template"></a>Breeze/Angular テンプレート

[Mads Kristensen](https://github.com/madskristensen)

> 簡単/角度の MVC テンプレートが、ワードベルによって書き込まれました
> 
> [簡単/角度の MVC テンプレートをダウンロードする](https://go.microsoft.com/fwlink/?LinkId=286437)

[AngularJS](http://angularjs.org)は、シングルページアプリケーション (spa) を構築するための Google のオープンソースライブラリです。 データバインディング、依存関係の挿入、および画面管理が用意されています。 [BreezeJS](http://www.breezejs.com/?utm_source=ms-spa)とデータモデリングおよびデータ管理用の別のオープンソースライブラリを組み合わせることにより、優れた HTML/JavaScript クライアントアプリのための不可欠な要素を持つことができます。

[KNOCKOUTJS spa](../introduction/knockoutjs-template.md)テンプレートは、ASP.NET and Web Tools 2012.2 更新プログラムに含まれています。 Visual Studio を使用している場合は、SPA の例が60秒未満で稼働しています。

![](http://www.breezejs.com/sites/all/images/spa-template/NgRunningTodoPage.png)

と、アプリケーションは KnockoutJS SPA テンプレートとよく似ています。 しかし、内部的にはまったく異なります。 KnockoutJS テンプレートでは、データバインディングにノックアウトを使用し、データアクセスに未加工の AJAX を使用します。 簡単/角度のテンプレートでは、データバインディングには角、データアクセスには簡単です。 これらのライブラリを使用すると、ページナビゲーションや履歴などの追加機能が有効になります。

アプリケーションの [バージョン情報] ページを次に示します。

![](http://www.breezejs.com/sites/all/images/spa-template/NgRunningAboutPage.png)

このページには、現在のユーザーセッション中のイベントの実行中のログが表示されます。次に例を示します。

- ベル. #2 と #7 での Todo コントローラーの作成に注意してください。
- リモートクエリ (#3) とローカルキャッシュクエリ (#7)。
- 新しい (#5、#6) および変更された (#4) エンティティを保存しています。
- クライアントで検証された変更 (#9)。これにより、ユーザーはデータベースに変更をコミットする前に誤りを修正できます。

このテンプレートの詳細については、次を参照してください。

- HTML ビューテンプレートの動的読み込み。
- 角の "ディレクティブ" を使用したカスタムデータバインディング。
- モジュール性と依存関係の注入。
- クエリフィルター、並べ替え、ページング、プロジェクション、関連エンティティの包含。
- 複数の画面でのデータの共有。
- 複数の変更を1つのトランザクションとして保存します。
- 検証規則は、サーバーから JavaScript クライアントに自動的に反映されます。

それでは始めましょう。

## <a name="create-a-breezeangular-template-project"></a>簡単/角度のテンプレートプロジェクトを作成する

上の [ダウンロード] ボタンをクリックして、テンプレートをダウンロードしてインストールします。 このテンプレートは、Visual Studio 拡張機能 (VSIX) ファイルとしてパッケージ化されています。 場合によっては、Visual Studio を再起動する必要があります。

**[テンプレート]** ペインで、 **[インストールされたテンプレート]** を選択し、  **C#ビジュアル**ノードを展開します。 **[ビジュアルC# ]** で **[Web]** を選択します。 プロジェクトテンプレートの一覧で、 **[ASP.NET MVC 4 Web アプリケーション]** を選択します。 プロジェクト名を指定して、 **[OK]** をクリックします。

**新しいプロジェクト**ウィザードで、[簡単に**SPA**] を選択します。

![](http://www.breezejs.com/sites/all/images/spa-template/SelectBreezeNgSpaTemplate.png)

Ctrl キーを押しながら F5 キーを押してアプリケーションをビルドし、デバッグせずに実行するか、F5 キーを押してデバッグを実行します。

![](http://www.breezejs.com/sites/all/images/spa-template/ZephyrLogin.png)

アプリケーションを初めて実行すると、ログイン画面が表示されます。 [サインアップ] リンクをクリックすると、新しいページ glides が表示されます。このページでは、ユーザー名とパスワードを入力できます。 (ログインページと登録ページは、ASP.NET MVC を使用して作成されます)。登録フォームを送信すると、サーバーによって、アカウントの2つの項目を含む TodoList が生成されます。 次に、黄色のメモでそれらを表示します。

![](http://www.breezejs.com/sites/all/images/spa-template/TodoList.png)

これで SPA の土地が完成しました。 コードを操作しているときに表示されるものと経験があるものはすべて、ノックアウトと簡単な方法でクライアントでレンダリングおよび管理されます。 アプリをユーザーとして探索... しかし、開発者にとっては、 ブラウザーで開発者ツールを使用して、ネットワークトラフィックをキャプチャします。 (Internet Explorer で F12 キーを押して、 **[ネットワーク]** タブを選択し、 **[キャプチャの開始]** をクリックします)。ここで、次の操作を実行します。

- 新しい Todo 項目を追加します。
- ラベルをクリックし、Todo 項目のタイトルを編集します
- チェックボックスをオンにして、完了した項目をマークします。 テキストボックスが無効になっていることに注意してください。そのため、タイトルは編集できなくなります。
- ラベルの右側にある [x] をクリックします。 アイテムが表示されなくなり、データベースから削除されます。
- 別の項目を選択し、そのタイトルをクリアします。 タイトルが必要であることを示す検証エラーが表示されます。 しばらくすると、前のタイトルが復元されます。
- 呼べの長いタイトルを入力します。 タイトルが長すぎるという別の検証エラーが表示されます。
- [Todo リストの追加] ボタンをクリックします。 前の一覧の左側に新しいリストが表示されます。
- TodoList のタイトルで再生し、必要な長さの検証をトリガーします。
- [タイトル] ボックスをクリックして、エラーメッセージをクリアします。
- 右上隅にある円の "x" をクリックして、TodoList とその todos を削除します。
- 右上の [バージョン情報] リンクをクリックすると、これらのアクティビティのログが表示されます。

検証ロジックは、クライアント側で簡単に実行されます。 サーバーモデルクラスの検証属性はクライアントに反映され、クライアントがサーバーに接続する前に自動的に実行されます。

ネットワークトラフィックを確認します。 簡単にエラーが検出された場合、サーバーへの呼び出しがないことに注意してください。 有効な変更が発生するたびに、POST 要求が "/api/Todo/SaveChanges" になりました。 簡単に変更をバンドルし、Web API コントローラーの `SaveChanges` 方法に1つの要求としてまとめて送信します。 これは、各項目に対して、PUT、POST、および DELETE 要求を個別に行う KnockoutJS SPA テンプレートとは異なります。

また、TodoList ページと About ページを切り替えるときにネットワークトラフィックが発生しないことにも注意してください。 これは、クエリがローカルの簡単なキャッシュに制約されているためです。

## <a name="peek-inside"></a>内部を見る

このアプリケーションには、クライアント側とサーバー側があります。 クライアント側スタックは、アプリケーションの JavaScript モジュール ("アプリ" フォルダー内) とサードパーティ製の JavaScript ライブラリ ("Scripts" フォルダー内) のわずかな HTML と組み合わせで構成されます。

![](http://www.breezejs.com/sites/all/images/spa-template/NgClientArchitecture2.png)

UI アーキテクチャは、ビューの HTML ウィジェットを、コントローラー内のサポートするプレゼンテーションコードから分離します。 角度データバインディングシステムでは、ビューとコントローラーを調整して、各がジョブを実行できるようにします。

コントローラーは、モデルエンティティを取得して保存するようデータコンテキストに要求します。 データコンテキストでは、ほとんどの作業が簡単に委任されます。これにより、JSON クエリの結果から自己追跡モデルオブジェクトが構築されます。

サーバー側スタックは、いくつかの開発者コードと .NET ライブラリである Web API、Entity Framework、Breeze.NET で構成されています。

![](http://www.breezejs.com/sites/all/images/spa-template/ServerArchitecture.png)

基本的なアーキテクチャは、KnockoutJS SPA テンプレートと同じです。 ただし、この実装ははるかに簡単です。 Dto が削除され、Entity Framework の詳細のほとんどが Breeze.NET に委任されています。

## <a name="next-steps"></a>次の手順

ここでは、簡単な web サイトのクライアントとサーバーの両方のスタックについて[詳しく説明](http://www.breezejs.com/ng-spa-template?utm_source=ms-spa)したコードを参照することをお勧めします。

クライアント側のクエリを簡単に試してみることができます。いくつかのフィルターと並べ替えを追加します。 エンドツーエンドの SPA 開発に対してより良い感覚を得るために、モデルのプロパティやエンティティをさらに追加することもできます。 設計が自信を持っている場合は、Todo 機能を破棄して独自の機能に置き換えることができます。

コーディングをお楽しみください!
