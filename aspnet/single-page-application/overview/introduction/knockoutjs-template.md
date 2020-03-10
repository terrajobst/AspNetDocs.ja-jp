---
uid: single-page-application/overview/introduction/knockoutjs-template
title: 'シングルページアプリケーション: KnockoutJS template |Microsoft Docs'
author: MikeWasson
description: テンプレートのノックアウト
ms.author: riande
ms.date: 01/30/2013
ms.assetid: f9c07af0-4b20-4b08-af8f-47fc3df169a2
msc.legacyurl: /single-page-application/overview/introduction/knockoutjs-template
msc.type: authoredcontent
ms.openlocfilehash: 3a551db1caa9636eb7f2e04c287d3ef371263584
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467320"
---
# <a name="single-page-application-knockoutjs-template"></a>シングルページアプリケーション: KnockoutJS テンプレート

[Mike Wasson](https://github.com/MikeWasson)

> ノックアウト MVC テンプレートは ASP.NET and Web Tools 2012.2 の一部です
> 
> [ASP.NET and Web Tools 2012.2 のダウンロード](https://go.microsoft.com/fwlink/?LinkId=282650)

ASP.NET and Web Tools 2012.2 の更新プログラムには、ASP.NET MVC 4 用の単一ページアプリケーション (SPA) テンプレートが含まれています。 このテンプレートは、対話型のクライアント側 web アプリの構築をすぐに始めることができるように設計されています。

"シングルページアプリケーション" (SPA) は、1つの HTML ページを読み込み、新しいページを読み込むのではなく、ページを動的に更新する web アプリケーションの一般的な用語です。 最初のページの読み込み後、SPA は AJAX 要求によってサーバーと通信します。

![](knockoutjs-template/_static/image1.png)

AJAX はまったく新しいものではありませんが、今日では、大規模な高度な SPA アプリケーションを簡単に構築して維持できる JavaScript フレームワークが用意されています。 また、HTML 5 と CSS3 は、豊富な Ui の作成を容易にします。

始めるには、SPA テンプレートでサンプルの "To do list" アプリケーションを作成します。 このチュートリアルでは、テンプレートのガイドツアーを実行します。 まず、To do list アプリケーション自体を見て、それが機能するテクノロジを確認します。

## <a name="create-a-new-spa-template-project"></a>新しい SPA テンプレートプロジェクトを作成する

要件:

- Web 用 Visual Studio 2012 または Visual Studio Express 2012
- ASP.NET Web Tools 2012.2 更新プログラム。 [ここで](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=ASPDOTNETandWebTools2012_2)更新プログラムをインストールできます。

Visual Studio を起動し、スタートページで **[新しいプロジェクト]** を選択します。 または、 **[ファイル]** メニューの **[新規作成]** をポイントし、 **[プロジェクト]** をクリックします。

**[テンプレート]** ペインで、 **[インストールされたテンプレート]** を選択し、  **C#ビジュアル**ノードを展開します。 **[ビジュアルC# ]** で **[Web]** を選択します。 プロジェクトテンプレートの一覧で、 **[ASP.NET MVC 4 Web アプリケーション]** を選択します。 プロジェクト名を指定して、 **[OK]** をクリックします。

![](knockoutjs-template/_static/image2.png)

**新しいプロジェクト**ウィザードで、 **[シングルページアプリケーション]** を選択します。

![](knockoutjs-template/_static/image3.png)

F5 キーを押して、アプリケーションをビルドして実行します。 アプリケーションを初めて実行すると、ログイン画面が表示されます。

![](knockoutjs-template/_static/image4.png)

&quot;サインアップ&quot; リンクをクリックして、新しいユーザーを作成します。

![](knockoutjs-template/_static/image5.png)

ログインすると、アプリケーションは2つの項目を含む既定の Todo リストを作成します。 新しいリストを追加するには、[Todo リストの追加] をクリックします。

![](knockoutjs-template/_static/image6.png)

リストの名前を変更し、リストに項目を追加して、それらのチェックボックスをオフにします。 また、項目を削除したり、一覧全体を削除したりすることもできます。 変更は、サーバー上のデータベースに自動的に保存されます (アプリケーションをローカルで実行しているため、この時点では実際には LocalDB です)。

![](knockoutjs-template/_static/image7.png)

## <a name="architecture-of-the-spa-template"></a>SPA テンプレートのアーキテクチャ

次の図は、アプリケーションの主な構成要素を示しています。

![](knockoutjs-template/_static/image8.png)

サーバー側では、ASP.NET MVC は HTML を提供し、フォームベースの認証も処理します。

ASP.NET Web API は、ToDoLists と ToDoItems に関連するすべての要求を処理します。これには、取得、作成、更新、および削除が含まれます。 クライアントは、JSON 形式の Web API とデータを交換します。

Entity Framework (EF) は、O/RM レイヤーです。 ASP.NET のオブジェクト指向の世界と基になるデータベースを仲介します。 データベースは LocalDB を使用しますが、これは web.config ファイルで変更できます。 通常は、ローカル開発に LocalDB を使用してから、EF code first の移行を使用してサーバー上の SQL データベースに配置します。

クライアント側では、node.js ライブラリが AJAX 要求からページの更新を処理します。 ノックアウトでは、データバインディングを使用して、ページと最新のデータを同期します。 このようにして、JSON データを処理するコードを記述して DOM を更新する必要はありません。 代わりに、データを表示する方法をノックアウトするように、宣言型の属性を HTML に配置します。

このアーキテクチャの大きな利点は、プレゼンテーション層とアプリケーションロジックが分離されていることです。 Web ページがどのように表示されるかを知らなくても、Web API の部分を作成できます。 クライアント側では、データを表す "ビューモデル" を作成し、ビューモデルがノックアウトを使用して HTML にバインドします。 これにより、ビューモデルを変更せずに HTML を簡単に変更できます。 (後でもう少しノックアウトを見てみましょう)。

## <a name="models"></a>モデル

Visual Studio プロジェクトの [モデル] フォルダーには、サーバー側で使用されるモデルが含まれています。 (クライアント側にもモデルがあります。これらのモデルについて説明します)。

![](knockoutjs-template/_static/image9.png)

**TodoItem、TodoList**

これらは、Entity Framework Code First のデータベースモデルです。 これらのモデルには、互いを指し示すプロパティがあることに注意してください。 `ToDoList` には ToDoItems のコレクションが含まれ、各 `ToDoItem` には親の ToDoList への参照があります。 これらのプロパティはナビゲーションプロパティと呼ばれ、一対多の関係、to do リスト、およびその to do 項目を表します。

また `ToDoItem` クラスでは、 **[ForeignKey]** 属性を使用して、`ToDoListId` が `ToDoList` テーブルの外部キーであることを指定します。 これは、データベースに外部キー制約を追加するように EF に指示します。

[!code-csharp[Main](knockoutjs-template/samples/sample1.cs)]

**TodoItemDto, TodoListDto**

これらのクラスは、クライアントに送信されるデータを定義します。 "DTO" は "データ転送オブジェクト" を表します。 DTO は、エンティティを JSON にシリアル化する方法を定義します。 通常、Dto を使用する理由はいくつかあります。

- シリアル化するプロパティを制御します。 DTO には、ドメインモデルのプロパティのサブセットを含めることができます。 これは、セキュリティ上の理由 (機密データを非表示にするため) または単に送信するデータの量を減らすために行うことができます。
- データの形状を変更する場合 (たとえば、より複雑なデータ構造をフラット化する場合)。
- DTO からビジネスロジックを維持する (懸念事項の分離)。
- 何らかの理由でドメインモデルをシリアル化できない場合。 たとえば、循環参照では、オブジェクトをシリアル化するときに問題が発生する可能性があります。 Web API でこの問題を処理する方法があります (「[循環オブジェクト参照の処理](../../../web-api/overview/formats-and-model-binding/json-and-xml-serialization.md#handling_circular_object_references)」を参照してください)。しかし、DTO を使用すると、単に問題を回避できます。

SPA テンプレートでは、Dto にはドメインモデルと同じデータが含まれています。 ただし、これらはナビゲーションプロパティからの循環参照を避け、一般的な DTO パターンを示すため便利です。

**AccountModels.cs**

このファイルには、サイトメンバーシップのモデルが含まれています。 `UserProfile` クラスは、メンバーシップデータベース内のユーザープロファイルのスキーマを定義します。 (この場合、唯一の情報は、ユーザー ID とユーザー名です)。このファイル内の他のモデルクラスを使用して、ユーザー登録フォームとログインフォームを作成します。

## <a name="entity-framework"></a>Entity Framework

SPA テンプレートは EF Code First を使用します。 Code First 開発では、まずコードでモデルを定義し、次に EF でモデルを使用してデータベースを作成します。 EF は、既存のデータベース ([Database First](https://msdn.microsoft.com/data/jj206878.aspx)) と共に使用することもできます。

[モデル] フォルダー内の `TodoItemContext` クラスは、 **Dbcontext**から派生します。 このクラスは、モデルと EF の間に "グルー" を提供します。 `TodoItemContext` には `ToDoItem` コレクションと `TodoList` コレクションが格納されます。 データベースに対してクエリを実行するには、これらのコレクションに対して LINQ クエリを記述するだけです。 たとえば、ユーザー "Alice" の to do リストをすべて選択するには、次のようにします。

[!code-csharp[Main](knockoutjs-template/samples/sample2.cs)]

また、コレクションに新しい項目を追加したり、項目を更新したり、コレクションから項目を削除したりして、変更をデータベースに保持することもできます。

## <a name="aspnet-web-api-controllers"></a>ASP.NET Web API コントローラー

ASP.NET Web API では、コントローラーは HTTP 要求を処理するオブジェクトです。 前述のように、SPA テンプレートでは、Web API を使用して `ToDoList` および `ToDoItem` インスタンスで CRUD 操作を有効にします。 コントローラーは、ソリューションの Controllers フォルダーに配置されます。

![](knockoutjs-template/_static/image10.png)

- `TodoController`: to do 項目に対する HTTP 要求を処理します
- `TodoListController`: to do リストに対する HTTP 要求を処理します。

これらの名前は、Web API が URI パスをコントローラー名と照合するため、重要です。 (Web API が HTTP 要求をコントローラーにルーティングする方法については、「 [ASP.NET Web API でのルーティング](../../../web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api.md)」を参照してください)。

`ToDoListController` クラスを見てみましょう。 1つのデータメンバーが含まれています。

[!code-csharp[Main](knockoutjs-template/samples/sample3.cs)]

前に説明したように、`TodoItemContext` は EF との通信に使用されます。 コントローラーのメソッドは CRUD 操作を実装します。 Web API は、次のように、クライアントからの HTTP 要求をコントローラーメソッドにマップします。

| HTTP 要求 | コントローラーメソッド | Description |
| --- | --- | --- |
| GET /api/todo | `GetTodoLists` | To do リストのコレクションを取得します。 |
| /Api/todo/*id*の取得 | `GetTodoList` | ID を使って to do リストを取得します |
| PUT/api/todo/*id* | `PutTodoList` | To do リストを更新します。 |
| POST /api/todo | `PostTodoList` | 新しい to do リストを作成します。 |
| /Api/todo/*id*の削除 | `DeleteTodoList` | TODO リストを削除します。 |

一部の操作の Uri には、ID 値のプレースホルダーが含まれていることに注意してください。 たとえば、ID が42の to リストを削除するには、URI を `/api/todo/42`します。

CRUD 操作に Web API を使用する方法の詳細については、「 [Crud 操作をサポートする WEB api の作成](../../../web-api/overview/older-versions/creating-a-web-api-that-supports-crud-operations.md)」を参照してください。 このコントローラーのコードは非常に簡単です。 いくつかの興味深い点を次に示します。

- `GetTodoLists` メソッドは、LINQ クエリを使用して、ログインしているユーザーの ID で結果をフィルター処理します。 そうすることで、ユーザーは自分に属するデータだけを見ることができます。 また、Select ステートメントを使用して、`ToDoList` インスタンスを `TodoListDto` インスタンスに変換することにも注意してください。
- PUT メソッドと POST メソッドは、データベースを変更する前にモデルの状態を確認します。 **Modelstate. IsValid**が false の場合、これらのメソッドは HTTP 400、Bad Request を返します。 モデルの検証の詳細については、「モデルの検証」を[参照して](../../../web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api.md)ください。
- コントローラークラスも **[承認]** 属性で修飾されています。 この属性は、HTTP 要求が認証されているかどうかを確認します。 要求が認証されていない場合、クライアントは、許可されていない HTTP 401 を受信します。 認証と承認の詳細について[は、ASP.NET Web API を](../../../web-api/overview/security/authentication-and-authorization-in-aspnet-web-api.md)参照してください。

`TodoController` クラスは `TodoListController`とよく似ています。 最大の違いは、クライアントが to do 項目を各 to do リストと共に取得するため、GET メソッドが定義されていないことです。

## <a name="mvc-controllers-and-views"></a>MVC コントローラーとビュー

MVC コントローラーは、ソリューションの Controllers フォルダーにもあります。 `HomeController` は、アプリケーションのメインの HTML をレンダリングします。 Home コントローラーのビューは、Views/Home/Index. cshtml に定義されています。 ホームビューでは、ユーザーがログインしているかどうかに応じて、さまざまなコンテンツが表示されます。

[!code-cshtml[Main](knockoutjs-template/samples/sample4.cshtml)]

ユーザーがログインすると、メイン UI が表示されます。 それ以外の場合は、[ログイン] パネルが表示されます。 この条件付きレンダリングはサーバー側で行われることに注意してください。 クライアント側&#8212;の機密コンテンツを非表示にしないでください。 http 応答で送信されるものは、未加工の http メッセージを監視しているユーザーに表示されます。

## <a name="client-side-javascript-and-knockoutjs"></a>クライアント側の JavaScript とノックアウト

次に、アプリケーションのサーバー側からクライアントに切り替えます。 SPA テンプレートでは、jQuery とノックアウトの組み合わせを使用して、スムーズで対話型の UI を作成します。 ノックアウトは、HTML をデータに簡単にバインドできる JavaScript ライブラリです。 ノックアウトは、"モデルビュービューモデル" と呼ばれるパターンを使用します。

- モデルはドメインデータ (ToDo リストと ToDo 項目) です。
- ビューは HTML ドキュメントです。
- ビューモデルは、モデルデータを保持する JavaScript オブジェクトです。 ビューモデルは、UI のコード抽象化です。 HTML 表現に関する情報はありません。 代わりに、"ToDo 項目のリスト" など、ビューの抽象的な機能を表します。

ビューは、ビューモデルにデータバインドされています。 ビューモデルに対する更新は、自動的にビューに反映されます。 バインドも同様に機能します。 DOM 内のイベント (クリックなど) は、AJAX 呼び出しをトリガーするビューモデルの関数にデータバインドされます。

SPA テンプレートでは、クライアント側の JavaScript が次の3つのレイヤーに編成されます。

- todo. datacontext: AJAX 要求を送信します。
- todo: モデルを定義します。
- todo。ビューモデルを定義します。

![](knockoutjs-template/_static/image11.png)

これらのスクリプトファイルは、ソリューションの Scripts/app フォルダーにあります。

![](knockoutjs-template/_static/image12.png)

**todo. datacontext**は、Web API コントローラーに対するすべての AJAX 呼び出しを処理します。 (ログインのための AJAX 呼び出しは、ajaxlogin 内の他の場所で定義されています)。

**todo。モデル**は、to do リストのクライアント側 (ブラウザー) モデルを定義します。 モデルクラスには、todoItem と todoList の2つがあります。

モデルクラスのプロパティの多くは、"ko" 型です。 Observable は、ノックアウトがどのようにマジックを行うかを示します。 [ノックアウトドキュメント](http://knockoutjs.com/documentation/introduction.html)から: 観測可能なは、変更についてサブスクライバーに通知できる "JavaScript オブジェクト" です。 観測可能な変更の値を指定すると、observable にバインドされているすべての HTML 要素が更新されます。 たとえば、todoItem には、title プロパティと isDone プロパティの observable があります。

[!code-javascript[Main](knockoutjs-template/samples/sample5.js)]

また、コードで観測可能なにサブスクライブすることもできます。 たとえば、todoItem クラスは、"isDone" プロパティと "title" プロパティの変更をサブスクライブします。

[!code-javascript[Main](knockoutjs-template/samples/sample6.js)]

**モデルの表示**

ビューモデルは、todo. ビューモデルで定義されます。 ビューモデルは、アプリケーションが HTML ページ要素をドメインデータにバインドする中心点です。 SPA テンプレートでは、ビューモデルには todoLists の観測可能な配列が含まれています。 ビューモデルの次のコードは、バインドを適用するようにノックアウトに指示します。

[!code-javascript[Main](knockoutjs-template/samples/sample7.js)]

## <a name="html-and-data-binding"></a>HTML およびデータバインド

ページのメインの HTML は Views/Home/Index. cshtml に定義されています。 データバインディングを使用しているため、HTML は実際に表示される内容のテンプレートにすぎません。 ノックアウトは*宣言型*のバインドを使用します。 ページ要素をデータにバインドするには、要素に "データバインド" 属性を追加します。 次に示すのは、ノックアウトドキュメントから取得した非常に単純な例です。

[!code-html[Main](knockoutjs-template/samples/sample8.html)]

この例では、ノックアウトは `myItems.count()`の値を使用して **&lt;スパン&gt;** 要素の内容を更新します。 この値が変更されるたびに、抜き合わせによってドキュメントが更新されます。

ノックアウトは、さまざまな種類のバインドを提供します。 SPA テンプレートで使用されるバインドの一部を次に示します。

- **foreach**: ループを反復処理し、リスト内の各項目に同じマークアップを適用できます。 これは、to do リストと to do 項目を表示するために使用されます。 **Foreach**内では、リストの要素にバインドが適用されます。
- **visible**: 表示/非表示を切り替えるために使用されます。 コレクションが空のときにマークアップを非表示にするか、エラーメッセージを表示します。
- **value**: フォーム値の設定に使用されます。
- **クリックし**て、ビューモデルの関数に click イベントをバインドします。

## <a name="anti-csrf-protection"></a>CSRF 防止

クロスサイト要求偽造 (CSRF) は、ユーザーが現在ログインしている脆弱なサイトに、悪意のあるサイトから要求を送信する攻撃です。 CSRF 攻撃を防ぐために、ASP.NET MVC では*偽造防止トークン*を使用します。これは、要求検証トークンとも呼ばれます。 これは、サーバーがランダムに生成されたトークンを web ページに配置するということです。 クライアントは、サーバーにデータを送信するときに、要求メッセージにこの値を含める必要があります。

悪意のあるページでは、同じオリジンのポリシーによってユーザーのトークンを読み取ることができないため、偽造防止トークンが機能します。 (同じオリジンポリシーを利用すると、2つの異なるサイトでホストされているドキュメントから互いのコンテンツにアクセスできなくなります)。

ASP.NET MVC では[、偽造防止のクラスと](https://msdn.microsoft.com/library/system.web.helpers.antiforgery.aspx) [[Validateアンチ Forgerytoken]](https://msdn.microsoft.com/library/system.web.mvc.validateantiforgerytokenattribute.aspx)属性を使用して、偽造防止トークンの組み込みサポートを提供しています。 現在、この機能は Web API には組み込まれていません。 ただし、SPA テンプレートには、Web API のカスタム実装が含まれています。 このコードは、ソリューションの Filters フォルダーにある `ValidateHttpAntiForgeryTokenAttribute` クラスで定義されています。 Web API での CSRF の防止の詳細については、「[クロスサイト要求偽造 (csrf) 攻撃の防止](../../../web-api/overview/security/preventing-cross-site-request-forgery-csrf-attacks.md)」を参照してください。

## <a name="conclusion"></a>まとめ

SPA テンプレートは、最新の対話型 web アプリケーションの作成をすぐに開始できるように設計されています。 また、ノックアウトライブラリを使用して、データとアプリケーションロジックからプレゼンテーション (HTML マークアップ) を分離します。 ただし、ノックアウトは、SPA の作成に使用できる唯一の JavaScript ライブラリではありません。 他のオプションを調べる場合は、コミュニティによって[作成された SPA テンプレート](../templates/index.md)を参照してください。
