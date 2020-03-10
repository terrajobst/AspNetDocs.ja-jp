---
uid: mvc/overview/older-versions-1/nerddinner/provide-crud-create-read-update-delete-data-form-entry-support
title: CRUD (作成、読み取り、更新、削除) データフォームエントリのサポートを提供します。Microsoft Docs
author: microsoft
description: 手順 5. では、ディナーでの編集、作成、および削除のサポートを有効にすることで、さらに Dinのコントローラークラスをさらに活用する方法を示します。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: bbb976e5-6150-4283-a374-c22fbafe29f5
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/provide-crud-create-read-update-delete-data-form-entry-support
msc.type: authoredcontent
ms.openlocfilehash: b3123af9a1477bc496a0d229d628510fc202b6d2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78468916"
---
# <a name="provide-crud-create-read-update-delete-data-form-entry-support"></a>CRUD (作成、読み取り、更新、削除) データ フォーム エントリ サポートを提供する

[Microsoft](https://github.com/microsoft)

[[Download PDF]\(PDF をダウンロード\)](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> これは、ASP.NET MVC 1 を使用して小規模で完成した web アプリケーションを構築する方法について説明する無料の["" アプリケーションチュートリアル](introducing-the-nerddinner-tutorial.md)の手順5です。
> 
> 手順 5. では、ディナーでの編集、作成、および削除のサポートを有効にすることで、さらに Dinのコントローラークラスをさらに活用する方法を示します。
> 
> ASP.NET MVC 3 を使用している場合は、MVC 3 または[Mvc ミュージックストア](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)[のチュートリアルではじめに](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)に従うことをお勧めします。

## <a name="nerddinner-step-5-create-update-delete-form-scenarios"></a>ステップ 5: フォームの作成、更新、削除のシナリオ

ここでは、コントローラーとビューについて説明しました。また、これらの機能を使用して、サイトでディナーのリスト/詳細エクスペリエンスを実装する方法についても説明しました。 次の手順として、Dinのコントローラークラスをさらに追加し、ディナーでの編集、作成、および削除のサポートを有効にします。

### <a name="urls-handled-by-dinnerscontroller"></a>Din. Controller によって処理される Url

以前*は、2*つの url のサポートを実装した*Din/Dinners* scontroller にアクションメソッドを追加しました。

| **[URL]** | **助動詞** | **目的** |
| --- | --- | --- |
| *ディナー* | GET | 今後のディナーの HTML リストを表示します。 |
| *///[Id]* | GET | 特定のディナーに関する詳細を表示します。 |

ここでは、*次の 3*つの追加 url を実装するアクションメソッドを追加します。/ *Din/edit/[id]* 、 */Dinners/Delete/[id]* 。 これらの Url を使用して、既存のディナーの編集、新しいディナーの作成、ディナーの削除をサポートできます。

これらの新しい Url では、HTTP GET と HTTP POST の両方の動詞をサポートします。 これらの Url への HTTP GET 要求によって、データの初期 HTML ビュー ("edit" の場合はディナーデータが入力されたフォーム)、"create" の場合は空のフォーム、"削除" の場合は削除の確認画面が表示されます。 これらの Url への HTTP POST 要求により、Dinのリポジトリ (およびデータベースから) のディナーデータが保存/更新/削除されます。

| **[URL]** | **助動詞** | **目的** |
| --- | --- | --- |
| *//編集/[id]* | GET | ディナーデータを設定した編集可能な HTML フォームを表示します。 |
| POST | 特定のディナーのフォームの変更をデータベースに保存します。 |
| */Din* | GET | ユーザーが新しいディナーを定義できる空の HTML フォームを表示します。 |
| POST | 新しいディナーを作成し、データベースに保存します。 |
| */Dinners/Delete/[id]* | GET | 削除の確認画面を表示します。 |
| POST | 指定されたディナーをデータベースから削除します。 |

### <a name="edit-support"></a>サポートの編集

まず、"編集" シナリオを実装しましょう。

#### <a name="the-http-get-edit-action-method"></a>HTTP GET Edit アクションメソッド

まず、edit アクションメソッドの HTTP "GET" 動作を実装します。 このメソッドは、/ *Dins/Edit/[id]* URL が要求されたときに呼び出されます。 実装は次のようになります。

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample1.cs)]

上記のコードでは、Dinのリポジトリを使用してディナーオブジェクトを取得しています。 次に、ディナーオブジェクトを使用して、ビューテンプレートをレンダリングします。 テンプレート名は明示的に*view ()* ヘルパーメソッドに渡されていないので、規則ベースの既定のパスを使用してビューテンプレートを解決します。

ここで、このビューテンプレートを作成しましょう。 これを行うには、Edit メソッド内で右クリックし、[ビューの追加] コンテキストメニューコマンドを選択します。

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image1.png)

[ビューの追加] ダイアログボックスで、そのモデルとしてディナーオブジェクトをビューテンプレートに渡し、"Edit" テンプレートの自動スキャフォールディングを選択することを示します。

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image2.png)

[追加] ボタンをクリックすると、Visual Studio によって "\Views\Dinners" ディレクトリ内に新しい "Edit .aspx" ビューテンプレートファイルが追加されます。 また、コードエディター内で新しい "Edit .aspx" ビューテンプレートが開き、次のような初期の "Edit" スキャフォールディングの実装が設定されます。

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image3.png)

既定の "edit" スキャフォールディングに対していくつかの変更を行い、次のコンテンツを含むように編集ビューテンプレートを更新します (公開したくないプロパティがいくつか削除されます)。

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample2.aspx)]

アプリケーションを実行して *"/Dinners/Edit/1"* URL を要求すると、次のページが表示されます。

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image4.png)

ビューによって生成される HTML マークアップは、次のようになります。 これは標準の HTML です。 &lt;フォーム&gt; 要素を使用して、"Save" &lt;input type = "submit"/&gt; ボタンがプッシュされたときに */Dinners/Edit/1* URL への HTTP POST を実行します。 編集可能な各プロパティに対して、HTML &lt;input type = "text"/&gt; 要素が出力されています。

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image5.png)

#### <a name="htmlbeginform-and-htmltextbox-html-helper-methods"></a>Html. BeginForm () および Html テキストボックス () Html ヘルパーメソッド

"Edit .aspx" ビューテンプレートでは、html、ValidationSummary ()、Html. BeginForm ()、.Html ()、および Html の Validationsummary () の複数の "Html ヘルパー" メソッドが使用されています。 これらのヘルパーメソッドは、HTML マークアップを生成するだけでなく、組み込みのエラー処理と検証のサポートを提供します。

##### <a name="htmlbeginform-helper-method"></a>Html. BeginForm () ヘルパーメソッド

Html. BeginForm () ヘルパーメソッドは、マークアップの HTML &lt;フォーム&gt; 要素を出力します。 編集 .aspx ビューテンプレートでは、このメソッドを使用するときに " C# using" ステートメントを適用していることがわかります。 左中かっこは、コンテンツ&gt; &lt;フォームの先頭を示します。右中かっこは、&lt;///&gt; 要素の末尾を示します。

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample3.cs)]

または、このようなシナリオに対して "using" ステートメントの不自然な方法が見つかった場合は、次のように Html の BeginForm () と Html の EndForm () の組み合わせを使用できます。

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample4.aspx)]

パラメーターを指定せずに Html. BeginForm () を呼び出すと、現在の要求の URL に HTTP POST を実行する form 要素が出力されます。 このため、Edit ビューでは *&lt;form action = "/Dinners/Edit/1" method = "post"&gt;* 要素が生成されます。 別の URL に投稿する場合は、別の方法で、明示的なパラメーターを Html に渡すこともできます。

##### <a name="htmltextbox-helper-method"></a>Html. TextBox () ヘルパーメソッド

編集 .aspx ビューでは、Html の TextBox () ヘルパーメソッドを使用して &lt;input type = "text"/&gt; 要素を出力します。

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample5.aspx)]

上記の .Html () メソッドは、1つのパラメーターを受け取ります。これは、出力する &lt;入力型 = "text"/&gt; 要素の id/name 属性と、テキストボックスの値を設定するモデルプロパティの両方を指定するために使用されます。 たとえば、編集ビューに渡されたディナーオブジェクトの "Title" プロパティ値が ".NET フューチャ" になっているため、Html テキストボックス ("Title") メソッドの呼び出し出力: *&lt;入力 id = "title" name = "title" type = "text" value = ". NET フューチャ"/&gt;* です。

または、最初の .Html () パラメーターを使用して要素の id と名前を指定し、次に2番目のパラメーターとして使用する値を明示的に渡すことができます。

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample6.aspx)]

多くの場合、出力される値に対してカスタム書式設定を実行します。 .NET に組み込まれている String. Format () 静的メソッドは、これらのシナリオに役立ちます。 編集 .aspx ビューテンプレートでは、このメソッドを使用して EventDate 値 (DateTime 型) を書式設定し、その時間に秒が表示されないようにしています。

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample7.aspx)]

Html. TextBox () の3番目のパラメーターは、追加の HTML 属性を出力するために必要に応じて使用できます。 次のコードスニペットは、追加の size = "30" 属性と、class = "mycssclass" 属性を &lt;input type = "text"/&gt; 要素に表示する方法を示しています。 ここでは、"@" character because "クラス" を使用してクラス属性の名前をエスケープする方法にC#ついて説明します。

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample8.aspx)]

#### <a name="implementing-the-http-post-edit-action-method"></a>HTTP ポスト編集アクションメソッドの実装

これで、編集アクションメソッドの HTTP GET バージョンが実装されました。 ユーザーが */Dinners/Edit/1* URL を要求すると、次のような HTML ページが表示されます。

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image6.png)

[Save] \ (保存 \) ボタンを押すと、 */Dinners/Edit/1* URL へのフォームポストが行われ、HTTP post 動詞を使用して HTML &lt;入力&gt; フォーム値が送信されます。 ここで、編集アクションメソッドの HTTP POST 動作を実装します。これにより、ディナーの保存が処理されます。

まず、オーバーロードされた "Edit" アクションメソッドを Dinのコントローラーに追加します。このメソッドには、HTTP POST シナリオを処理することを示す "AcceptVerbs" 属性が含まれています。

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample9.cs)]

オーバーロードされたアクションメソッドに [AcceptVerbs] 属性が適用されると、ASP.NET MVC は、受信 HTTP 動詞に応じて、適切なアクションメソッドへのディスパッチ要求を自動的に処理します。 HTTP POST 要求が */Dins/edit/[id]* の*url にアクセス*すると、上記の編集メソッドが使用されますが、その他のすべての http 動詞要求 (& n) は、実装した (`[AcceptVerbs]` 属性を持たない) 最初の編集メソッドに送られます。

| **サイドトピック: HTTP 動詞を使用して区別する理由** |
| --- |
| 1つの URL を使用し、HTTP 動詞でその動作を区別するのはなぜですか。 編集変更の読み込みと保存を処理するために2つの異なる Url を用意する必要があるのはなぜですか。 たとえば、フォームを保存するためのフォームの post を処理する場合、最初のフォームと/Din/[id] を表示するには、次のように入力します。 2つの異なる Url を公開する場合の欠点は、1/3 に投稿した後、入力エラーのために HTML フォームを再表示する必要がある場合、エンドユーザーはブラウザーのアドレスバーに (フォームがポストされた URL であるため)、その URL が使用されるようになることです。 エンドユーザーがこの再表示されたページをブラウザーのお気に入りの一覧にブックマークしたり、URL をコピーして友人に送信したりすると、後では機能しない URL が保存されます (その URL は post 値に依存しているため)。 1 つの URL を公開することで (のような:/Dinners/Edit/[id]) および HTTP 動詞でその処理を区別するの編集ページをブックマークや他のユーザーに、URL を送信するエンドユーザーのも安全です。 |

#### <a name="retrieving-form-post-values"></a>フォームポスト値の取得

HTTP POST の "Edit" メソッドでは、ポストされたフォームパラメーターにさまざまな方法でアクセスできます。 単純な方法の1つとして、Controller 基本クラスの Request プロパティを使用してフォームコレクションにアクセスし、ポストされた値を直接取得するだけです。

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample10.cs)]

ただし、上記の方法は、特にエラー処理ロジックを追加した後は少し詳細になります。

このシナリオでは、コントローラーの基本クラスで組み込みの*UpdateModel ()* ヘルパーメソッドを利用することをお勧めします。 オブジェクトのプロパティの更新は、受信フォームパラメーターを使用して渡すことができます。 このメソッドは、リフレクションを使用してオブジェクトのプロパティ名を決定し、クライアントによって送信された入力値に基づいて、値を自動的に変換して値を割り当てます。

UpdateModel () メソッドを使用して、次のコードを使用して HTTP POST 編集アクションを簡略化できます。

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample11.cs)]

これで、 */Dinners/Edit/1* URL にアクセスし、ディナーのタイトルを変更できます。

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image7.png)

[保存] ボタンをクリックすると、編集アクションへのフォームの投稿が実行され、更新された値はデータベースに保存されます。 次に、ディナーの詳細 URL にリダイレクトされます (新たに保存された値が表示されます)。

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image8.png)

#### <a name="handling-edit-errors"></a>編集エラーの処理

現在の HTTP ポストの実装は、エラーがある場合を除き、正常に動作します。

ユーザーがフォームを編集するときに、フォームが再表示され、問題を修正するための情報を示すエラーメッセージが表示されていることを確認する必要があります。 これには、エンドユーザーが間違った入力 (たとえば、形式が正しくない日付文字列) を投稿する場合や、入力形式が有効であってもビジネスルール違反がある場合などがあります。 エラーが発生すると、フォームはユーザーが最初に入力した入力データを保持する必要があるため、手動で変更を補充する必要がありません。 このプロセスは、フォームが正常に完了するまで、必要な回数だけ繰り返す必要があります。

ASP.NET MVC には、エラー処理とフォーム再表示を容易にする便利な組み込み機能がいくつか用意されています。 これらの機能を実際に確認するには、編集アクションメソッドを次のコードで更新してみましょう。

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample12.cs)]

上記のコードは、前の実装に似ています。ただし、ここでは、作業の前後に try/catch エラー処理ブロックをラップしている点が異なります。 UpdateModel () の呼び出し中に例外が発生した場合、または Dinを保存しようとしたときに (保存しようとしているディナーオブジェクトがモデル内のルール違反のために無効である場合に例外が発生する)、キャッチエラー処理ブロックは、おい. その中で、ディナーオブジェクトに存在する規則違反をループし、ModelState オブジェクトに追加します (これについては後で説明します)。 次に、ビューを再表示します。

この作業を確認するには、アプリケーションを再実行し、ディナーを編集して、空のタイトル、EventDate が "BOGUS" になるように変更して、国の値が USA である英国の電話番号を使用します。 [保存] ボタンを押すと、HTTP POST Edit メソッドは、(エラーがあるために) ディナーを保存できなくなり、フォームが再表示されます。

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image9.png)

アプリケーションのエラーエクスペリエンスが向上しています。 無効な入力を持つテキスト要素が赤色で強調表示され、エンドユーザーに対して検証エラーメッセージが表示されます。 このフォームには、ユーザーが最初に入力した入力データも保持されるため、何も入力する必要がありません。

どうすればよいでしょうか。 [タイトル]、[EventDate]、および [ContactPhone] の各テキストボックス自体が赤で強調表示され、最初に入力したユーザー値が出力されます。 エラーメッセージが上部の一覧に表示されるのはどのようなものですか。 これはマジックではありませんでした。これは、入力の検証とエラー処理のシナリオを簡単に行う組み込みの ASP.NET MVC 機能の一部を使用したためです。

#### <a name="understanding-modelstate-and-the-validation-html-helper-methods"></a>ModelState と検証 HTML ヘルパーメソッドについて

コントローラークラスには、ビューに渡されるモデルオブジェクトのエラーが存在することを示すための "ModelState" プロパティコレクションがあります。 ModelState コレクション内のエラーエントリは、問題のあるモデルプロパティの名前 ("Title"、"EventDate"、"ContactPhone" など) を識別し、わかりやすいエラーメッセージを指定できるようにします (例: "タイトルが必要")。

*UpdateModel ()* ヘルパーメソッドは、モデルオブジェクトのプロパティにフォーム値を割り当てようとしているときに、エラーが発生したときに modelstate コレクションを自動的に設定します。 たとえば、ディナーオブジェクトの EventDate プロパティは DateTime 型です。 上記のシナリオで、UpdateModel () メソッドが文字列値 "BOGUS" をこのメソッドに割り当てることができなかった場合、UpdateModel () メソッドは、そのプロパティで割り当てエラーが発生したことを示すエントリを ModelState コレクションに追加します。

開発者は、"catch" エラー処理ブロック内で次に示すように、エラーエントリを ModelState コレクションに明示的に追加するコードを記述することもできます。これは、ディナーオブジェクト:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample13.cs)]

#### <a name="html-helper-integration-with-modelstate"></a>Html ヘルパーと ModelState の統合

Html ヘルパーメソッド (Html. TextBox () など)-出力をレンダリングするときに ModelState コレクションを確認します。 項目のエラーが存在する場合は、ユーザーが入力した値と CSS エラークラスを表示します。

たとえば、"Edit" ビューでは、Html. TextBox () ヘルパーメソッドを使用して、ディナーオブジェクトの EventDate をレンダリングしています。

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample14.aspx)]

エラーシナリオでビューがレンダリングされると、.Html () メソッドは ModelState コレクションを確認して、ディナーオブジェクトの "EventDate" プロパティに関連付けられたエラーがあるかどうかを確認します。 エラーが発生したと判断した場合、送信されたユーザー入力 ("偽") を値としてレンダリングし、css error クラスを &lt;input type = "textbox"/&gt; 生成したマークアップに追加します。

[!code-html[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample15.html)]

必要に応じて、css error クラスの外観をカスタマイズできます。 既定の CSS エラークラス– "入力-検証-エラー" –は、次のように、 *\ content\ sitestylesheet*スタイルシートで定義されています。

[!code-css[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample16.css)]

この CSS 規則は、次のように、無効な入力要素が強調表示される原因となっています。

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image10.png)

##### <a name="htmlvalidationmessage-helper-method"></a>Html. ValidationMessage () ヘルパーメソッド

Html の ValidationMessage () ヘルパーメソッドを使用すると、特定のモデルプロパティに関連付けられている ModelState エラーメッセージを出力できます。

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample17.aspx)]

上記のコードでは、 *&lt;span class = "/span"&gt; になります。値 ' BOGUS ' は無効&lt;&gt;*

Html の ValidationMessage () ヘルパーメソッドでは、表示されているエラーテキストメッセージを開発者がオーバーライドできる2番目のパラメーターもサポートしています。

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample18.aspx)]

上記のコードでは、EventDate プロパティにエラーが存在する場合に、既定のエラーテキストではなく、 *span class = "/span"&gt;\*&lt;&gt;* を出力しています&lt;。

##### <a name="htmlvalidationsummary-helper-method"></a>Html. ValidationSummary () ヘルパーメソッド

Html. ValidationSummary () ヘルパーメソッドを使用すると、集計エラーメッセージを表示できます。これには、&lt;ul&gt;&lt;li/&gt;&lt;/ul&gt; ModelState コレクション内のすべての詳細エラーメッセージの一覧が表示されます。

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image11.png)

Html の ValidationSummary () ヘルパーメソッドは、省略可能な文字列パラメーターを受け取ります。これは、詳細なエラーの一覧の上に表示する概要エラーメッセージを定義します。

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample19.aspx)]

必要に応じて CSS を使用して、エラー一覧の外観をオーバーライドできます。

#### <a name="using-a-addruleviolations-helper-method"></a>AddRuleViolations ヘルパーメソッドの使用

最初の HTTP POST 編集の実装では、catch ブロック内で foreach ステートメントを使用して、ディナーオブジェクトの規則違反をループし、コントローラーの ModelState コレクションに追加します。

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample20.cs)]

このコードは、"コントローラーヘルパー" クラスを "コントローラー" プロジェクトに追加し、ASP.NET MVC ModelStateDictionary クラスにヘルパーメソッドを追加する "AddRuleViolations" 拡張メソッドを実装することによって、少しすっきりしたものにすることができます。 この拡張メソッドは、ModelStateDictionary に RuleViolation エラーの一覧を設定するために必要なロジックをカプセル化できます。

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample21.cs)]

次に、HTTP POST 編集アクションメソッドを更新して、この拡張メソッドを使用して、ディナールール違反を ModelState コレクションに設定できます。

#### <a name="complete-edit-action-method-implementations"></a>アクションメソッドの実装の完了

以下のコードは、編集シナリオに必要なすべてのコントローラーロジックを実装しています。

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample22.cs)]

編集実装に関するすばらしい点は、コントローラークラスもビューテンプレートも、ディナーモデルによって適用されている特定の検証またはビジネスルールに関する情報を知る必要がないということです。 将来、モデルに追加のルールを追加することができます。また、サポートされるように、コントローラーやビューにコード変更を加える必要はありません。 これにより、コードの変更を最小限に抑えて、将来的にアプリケーションの要件を簡単に拡張できる柔軟性が提供されます。

### <a name="create-support"></a>サポートを作成する

Dinのコントローラークラスの "編集" 動作の実装が完了しました。 ここで、ユーザーが新しいディナーを追加できるようにするための "Create" サポートを実装する方法について説明します。

#### <a name="the-http-get-create-action-method"></a>HTTP-GET Create Action メソッド

まず、create action メソッドの HTTP "GET" 動作を実装します。 このメソッドは、他のユーザーが */Dins/create* URL にアクセスしたときに呼び出されます。 実装は次のようになります。

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample23.cs)]

上記のコードでは、新しいディナーオブジェクトを作成し、その EventDate プロパティを1週間後に割り当てます。 次に、新しいディナーオブジェクトに基づくビューをレンダリングします。 明示的に名前を*view ()* ヘルパーメソッドに渡していないので、規則ベースの既定のパスを使用してビューテンプレートを解決します。

ここで、このビューテンプレートを作成しましょう。 これを行うには、Create action メソッド内で右クリックし、[ビューの追加] コンテキストメニューコマンドを選択します。 [ビューの追加] ダイアログボックスで、ディナーオブジェクトをビューテンプレートに渡し、"Create" テンプレートの自動スキャフォールディングを選択することを指定します。

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image12.png)

[追加] ボタンをクリックすると、Visual Studio によって新しいスキャフォールディングベースの "\Views\Dinners" ビューが "" ディレクトリに保存され、IDE 内で開かれます。

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image13.png)

既定の "create" スキャフォールディングファイルに対して生成された変更をいくつか行い、次のように変更してみましょう。

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample24.aspx)]

ここで、アプリケーションを実行し、ブラウザー内で *"/dinの S/create"* URL にアクセスすると、次のような UI が作成アクションの実装から表示されます。

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image14.png)

#### <a name="implementing-the-http-post-create-action-method"></a>HTTP ポスト作成アクションメソッドの実装

Create action メソッドの HTTP GET バージョンが実装されています。 ユーザーが [保存] ボタンをクリックする*と、その URL へ*のフォームポストが実行され、HTTP post 動詞を使用して HTML &lt;入力&gt; フォーム値が送信されます。

ここで、create action メソッドの HTTP POST 動作を実装しましょう。 まず、オーバーロードされた "Create" アクションメソッドを、HTTP POST シナリオを処理することを示す "AcceptVerbs" 属性を持つ Din: コントローラーに追加します。

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample25.cs)]

HTTP ポストが有効な "Create" メソッドでは、ポストされたフォームパラメーターにさまざまな方法でアクセスできます。

1つの方法として、新しいディナーオブジェクトを作成し、 *UpdateModel ()* ヘルパーメソッド (Edit アクションの場合と同様) を使用して、ポストされたフォーム値を設定する方法があります。 次に、これを Dinレポジトリに追加し、データベースに保存します。次のコードを使用して、新しく作成したディナーを表示するように、ユーザーを [詳細] アクションにリダイレクトします。

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample26.cs)]

または、Create () アクションメソッドが、メソッドパラメーターとしてディナーオブジェクトを受け取る方法を使用することもできます。 ASP.NET MVC は、自動的に新しいディナーオブジェクトをインスタンス化し、フォーム入力を使用してプロパティを設定し、それをアクションメソッドに渡します。

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample27.cs)]

上記のアクションメソッドは、"ModelState. IsValid" プロパティをチェックして、ディナーオブジェクトにフォームポスト値が正常に設定されたことを確認します。 これは、入力変換の問題 (たとえば、EventDate プロパティに "偽" の文字列) がある場合に false を返します。問題がある場合は、アクションメソッドによってフォームが再表示されます。

入力値が有効な場合、アクションメソッドは、新しいディナーを Dinare リポジトリに追加して保存しようとします。 この作業は try/catch ブロック内にラップされ、ビジネスルール違反がある場合はフォームを再実行します (これにより、例外が発生する可能性があります)。

このエラー処理の動作を確認するには、 */Dins/create* URL を要求し、新しいディナーに関する詳細を入力します。 入力または値が正しくないと、次のように強調表示されたエラーと共に作成フォームが再表示されます。

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image15.png)

Create フォームには、編集フォームとまったく同じ検証とビジネスルールが適用されていることに注意してください。 これは、検証とビジネスルールがモデルで定義されており、アプリケーションの UI またはコントローラー内に埋め込まれていないためです。 つまり、後で検証やビジネスルールを1か所で変更/進化させ、アプリケーション全体に適用することができます。 Edit または Create アクションメソッド内のコードを変更しなくても、新しいルールや既存のルールに対する変更を自動的に受け入れることができます。

入力値を修正して [保存] ボタンをもう一度クリックすると、Dinのリポジトリへの追加が成功し、新しいディナーがデータベースに追加されます。 その後、次の URL にリダイレクトされます。ここに*は、新しく*作成したディナーの詳細が表示されます。

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image16.png)

### <a name="delete-support"></a>サポートの削除

次に、"削除" のサポートを Dincontroller に追加しましょう。

#### <a name="the-http-get-delete-action-method"></a>HTTP-GET Delete アクションメソッド

まず、delete アクションメソッドの HTTP GET 動作を実装します。 このメソッドは、他のユーザーが */Dinners/Delete/[id]* URL にアクセスしたときに呼び出されます。 実装は次のとおりです。

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample28.cs)]

アクションメソッドは、削除するディナーを取得しようとします。 ディナーが存在する場合は、ディナーオブジェクトに基づいてビューが表示されます。 オブジェクトが存在しない (または既に削除されている) 場合は、"Details" アクションメソッド用に以前に作成した "NotFound" ビューテンプレートを表示するビューを返します。

"削除" ビューテンプレートを作成するには、Delete アクションメソッド内で右クリックし、[ビューの追加] コンテキストメニューコマンドを選択します。 [ビューの追加] ダイアログボックスで、そのモデルとしてディナーオブジェクトをビューテンプレートに渡し、空のテンプレートを作成することを選択します。

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image17.png)

[追加] ボタンをクリックすると、Visual Studio によって "\Views\Dinners" ディレクトリ内に新しい "Delete .aspx" ビューテンプレートファイルが追加されます。 次のように、テンプレートに HTML とコードを追加して、削除の確認画面を実装します。

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample29.aspx)]

上のコードは、削除するディナーのタイトルを表示し、エンドユーザーがその中の [Delete] ボタンをクリックした場合に/Dinners/Delete/[id] URL への投稿を行う &lt;フォーム&gt; 要素を出力します。

アプリケーションを実行し、有効なディナーオブジェクトの *"/Dinners/Delete/[id]"* URL にアクセスすると、次のような UI が表示されます。

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image18.png)

| **サイドトピック: 投稿を実行する理由** |
| --- |
| [削除の確認] 画面で&gt; &lt;フォームを作成する必要があるのはなぜですか。 標準ハイパーリンクを使用して、実際の削除操作を実行するアクションメソッドにリンクしているのはなぜですか。 これは、web クローラーと検索エンジンに対して Url を検出し、誤ってリンクをたどるとデータが削除されることを防ぐために注意する必要があるためです。 HTTP-GET ベースの Url は、アクセス/クロールのために "安全" と見なされ、HTTP ポストに従わないことが想定されています。 適切なルールとして、常に破棄またはデータの変更操作を HTTP ポスト要求の背後に配置することをお勧めします。 |

#### <a name="implementing-the-http-post-delete-action-method"></a>HTTP ポスト削除アクションメソッドの実装

これで、削除の確認画面を表示する、HTTP GET バージョンの Delete アクションメソッドが実装されました。 エンドユーザーが [削除] ボタンをクリックすると、 *[id]* URL へのフォームの投稿が実行されます。

次のコードを使用して、delete アクションメソッドの HTTP "POST" 動作を実装してみましょう。

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample30.cs)]

削除アクションメソッドの HTTP POST バージョンは、削除するディナーオブジェクトを取得しようとします。 (既に削除されているため) 見つからない場合は、"NotFound" テンプレートをレンダリングします。 夕食が見つかった場合は、Dinレポジトリから削除されます。 その後、"Deleted" テンプレートがレンダリングされます。

"Deleted" テンプレートを実装するには、アクションメソッドを右クリックし、[ビューの追加] コンテキストメニューを選択します。 ビューに "Deleted" という名前を付けると、空のテンプレートになります (厳密に型指定されたモデルオブジェクトを使用することはできません)。 次に、HTML コンテンツをいくつか追加します。

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample31.aspx)]

ここで、アプリケーションを実行し、有効なディナーオブジェクトの *"/Dinners/Delete/[id]"* URL にアクセスすると、次のようなディナー削除確認画面が表示されます。

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image19.png)

[Delete] \ (削除 \) ボタンをクリックすると、 */Dinners/Delete/[id]* URL への HTTP POST が実行されます。これにより、データベースからディナーが削除され、"Deleted" ビューテンプレートが表示されます。

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image20.png)

### <a name="model-binding-security"></a>モデルバインディングのセキュリティ

ASP.NET MVC の組み込みのモデルバインド機能を使用する2つの異なる方法について説明しました。 最初の方法では、UpdateModel () メソッドを使用して既存のモデルオブジェクトのプロパティを更新し、2つ目のメソッドでモデルオブジェクトをアクションメソッドパラメーターとして渡すための ASP.NET MVC のサポートを使用します。 これらの方法はどちらも非常に強力で、非常に便利です。

また、it 部門の責任もあります。 ユーザー入力を受け入れるときは常にセキュリティについて paranoid することが重要です。これは、オブジェクトを入力にバインドする場合にも当てはまります。 HTML および JavaScript インジェクション攻撃を防ぐために、ユーザーが入力した値は常に HTML エンコードする必要があります。また、SQL インジェクション攻撃にも注意してください (注: アプリケーションには LINQ to SQL を使用します。これにより、パラメーターが自動的にエンコードされ、これらを防ぐことができます。攻撃の種類。 クライアント側の検証だけでなく、偽の値を送信しようとしているハッカーからの防御を常にサーバー側で検証する必要があります。

ASP.NET MVC のバインド機能を使用するときに考慮する必要がある追加のセキュリティ項目の1つは、バインドするオブジェクトのスコープであることです。 具体的には、バインドを許可するプロパティのセキュリティへの影響を確実に理解し、エンドユーザーが更新できるようにする必要があるプロパティのみを許可するようにします。

既定では、UpdateModel () メソッドは、入力された形式のパラメーター値に一致するモデルオブジェクトのすべてのプロパティを更新しようとします。 同様に、アクションメソッドのパラメーターとして渡されるオブジェクトでも、既定では、すべてのプロパティをフォームパラメーターを使用して設定できます。

#### <a name="locking-down-binding-on-a-per-usage-basis"></a>使用単位でバインドをロックダウンする

更新可能なプロパティの明示的な "インクルードリスト" を指定することで、使用単位でバインドポリシーをロックダウンできます。 これを行うには、次のように、余分な文字列配列パラメーターを UpdateModel () メソッドに渡します。

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample32.cs)]

アクションメソッドのパラメーターとして渡されるオブジェクトは、次のように、許可されたプロパティの "include list" を有効にする [Bind] 属性もサポートします。

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample33.cs)]

#### <a name="locking-down-binding-on-a-type-basis"></a>型に基づいてバインディングをロックダウンする

また、型ごとにバインド規則をロックダウンすることもできます。 これにより、バインド規則を1回指定することができ、すべてのコントローラーとアクションメソッドで、すべてのシナリオ (UpdateModel とアクションメソッドの両方のシナリオを含む) に適用することができます。

型に対して [Bind] 属性を追加するか、アプリケーションの global.asax ファイル内に登録することによって、型ごとのバインド規則をカスタマイズできます (型を所有していない場合に便利です)。 その後、バインド属性の Include プロパティと Exclude プロパティを使用して、特定のクラスまたはインターフェイスに対してバインドできるプロパティを制御できます。

ここでは、次のように、このアプリケーションのディナークラスにこの手法を使用し、バインド可能なプロパティの一覧を次のように制限する [Bind] 属性を追加します。

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample34.cs)]

バインドを使用した RSVPs コレクションの操作は許可されていません。また、バインドによって Dinare Id または HostedBy プロパティを設定することもできません。 セキュリティ上の理由から、代わりに、アクションメソッド内の明示的なコードを使用して、これらの特定のプロパティのみを操作します。

### <a name="crud-wrap-up"></a>CRUD のラップアップ

ASP.NET MVC には、フォームポストのシナリオを実装するのに役立つさまざまな機能が組み込まれています。 私たちは、このようなさまざまな機能を使用して、Dinのリポジトリに対して CRUD UI のサポートを提供していました。

ここでは、モデルに重点を置いたアプローチを使用して、アプリケーションを実装しています。 これは、すべての検証とビジネスルールのロジックが、コントローラーやビュー内ではなく、モデルレイヤー内で定義されることを意味します。 コントローラークラスもビューテンプレートにも、ディナーモデルクラスによって適用される特定のビジネスルールについての情報はありません。

これにより、アプリケーションアーキテクチャのクリーンアップが維持され、テストが容易になります。 将来、モデルレイヤーにビジネスルールを追加することができます。また、サポートされるように、コントローラーやビューに*コード変更を加える必要もありません*。 これにより、将来のアプリケーションの進化と変更に多大な機敏性をもたらすことができます。

Dinは、ディナーリスト/詳細のほか、作成、編集、削除のサポートを有効にするようになりました。 クラスの完全なコードについては、以下を参照してください。

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample35.cs)]

### <a name="next-step"></a>次の手順

これで、お客様の Dinのコントローラークラス内で、基本的な CRUD (作成、読み取り、更新、削除) のサポートを実装できるようになりました。

次に、ViewData クラスとビューモデルクラスを使用して、フォームでさらに充実した UI を有効にする方法を見てみましょう。

> [!div class="step-by-step"]
> [前へ](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
> [次へ](use-viewdata-and-implement-viewmodel-classes.md)
