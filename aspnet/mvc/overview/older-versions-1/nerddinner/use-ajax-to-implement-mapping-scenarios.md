---
uid: mvc/overview/older-versions-1/nerddinner/use-ajax-to-implement-mapping-scenarios
title: AJAX を使用してマッピングシナリオを実装する |Microsoft Docs
author: microsoft
description: 手順 11. では、AJAX マッピングサポートをディナーアプリケーションに統合して、ユーザーがを作成、編集、または表示していることを確認する方法を示します。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: f731990a-0a81-4d62-81df-87d676cdedd6
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-ajax-to-implement-mapping-scenarios
msc.type: authoredcontent
ms.openlocfilehash: 7fc90f978b9f9eca511feca70a3c0d02ec69b940
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78468538"
---
# <a name="use-ajax-to-implement-mapping-scenarios"></a>AJAX を使用し、マッピング シナリオを実装する

[Microsoft](https://github.com/microsoft)

[[Download PDF]\(PDF をダウンロード\)](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> これは、ASP.NET MVC 1 を使用して小規模で完成した web アプリケーションを構築する方法を説明する無料の["" アプリケーションのチュートリアル](introducing-the-nerddinner-tutorial.md)の手順11です。
> 
> 手順 11. では、AJAX マッピングサポートをディナーアプリケーションに統合する方法を示します。これにより、ユーザーがを作成、編集、または表示して、ディナーの場所をグラフィカルに表示できるようになります。
> 
> ASP.NET MVC 3 を使用している場合は、MVC 3 または[Mvc ミュージックストア](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)[のチュートリアルではじめに](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)に従うことをお勧めします。

## <a name="nerddinner-step-11-integrating-an-ajax-map"></a>手順 11: AJAX マップを統合する

AJAX マッピングのサポートを統合することで、アプリケーションをより視覚的に魅力的にすることができるようになります。 これにより、ディナーを作成、編集、または表示して、ディナーの場所をグラフィカルに表示することができます。

### <a name="creating-a-map-partial-view"></a>マップ部分ビューの作成

ここでは、アプリケーション内の複数の場所でマッピング機能を使用します。 コードを乾いたままにするために、共通のマップ機能を1つの部分的なテンプレート内にカプセル化します。これは、複数のコントローラーアクションやビューで再利用できます。 この部分ビューに "map. .ascx" という名前を付け、\Views\Dinners ディレクトリ内に作成します。

マップの .ascx 部分を作成するには、\Views\Dinners ディレクトリを右クリックし、[&gt;ビューの追加] メニューコマンドを選択します。 ビューに "Map. .ascx" という名前を付け、部分ビューとしてチェックし、厳密に型指定された "ディナー" モデルクラスを渡すことを示します。

![](use-ajax-to-implement-mapping-scenarios/_static/image1.png)

[追加] ボタンをクリックすると、部分的なテンプレートが作成されます。 次に、次の内容が含まれるようにマップの .ascx ファイルを更新します。

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample1.aspx)]

最初の &lt;スクリプト&gt; 参照ポイントは、Microsoft Virtual Earth 6.2 マッピングライブラリを指しています。 2番目の &lt;スクリプト&gt; 参照は、一般的な Javascript マッピングロジックをカプセル化するために作成されるマップ .js ファイルを指します。 &lt;div id = ""&gt; 要素 "は、Virtual Earth がマップをホストするために使用する HTML コンテナーです。

次に、このビューに固有の2つの JavaScript 関数を含む &lt;スクリプト&gt; が埋め込まれています。 最初の関数は、jQuery を使用して、ページがクライアント側スクリプトを実行する準備ができたときに実行される関数を接続します。 このメソッドは、virtual earth マップコントロールを読み込むために、マップの .js スクリプトファイル内で定義する LoadMap () ヘルパー関数を呼び出します。 2番目の関数は、位置を識別するマップにピンを追加するコールバックイベントハンドラーです。

ここでは、クライアント側のスクリプトブロック内でサーバー側の &lt;% =%&gt; ブロックを使用して、コードを JavaScript にマップするディナーの緯度と経度を埋め込む方法に注目してください。 これは、クライアント側のスクリプトで使用できる動的な値を出力するための便利な手法です (値を取得するために、サーバーに対して個別の AJAX コールバックを必要とせず、値が高速になります)。 &lt;% =%&gt; ブロックは、ビューがサーバーでレンダリングされるときに実行されます。したがって、HTML の出力は、埋め込まれた JavaScript の値 (例: var 緯度 = 47.64312;) で終了します。

### <a name="creating-a-mapjs-utility-library"></a>マップ .js ユーティリティライブラリの作成

ここで、マップの JavaScript 機能をカプセル化するために使用できるマップ .js ファイルを作成します (さらに、上記の LoadMap メソッドと Loadmap メソッドを実装します)。 これを行うには、プロジェクト内の \Scripts ディレクトリを右クリックし、[新しい項目の&gt;追加] メニューコマンドを選択して、[JScript] 項目を選択し、"" という名前を付けます。

次に示すのは、Virtual Earth と対話してマップを表示し、ディナーの場所ピンを追加する、マップの .js ファイルに追加する JavaScript コードです。

[!code-javascript[Main](use-ajax-to-implement-mapping-scenarios/samples/sample2.js)]

### <a name="integrating-the-map-with-create-and-edit-forms"></a>マップを作成フォームと編集フォームに統合する

ここでは、マップのサポートと既存の作成と編集のシナリオを統合します。 すばらしいのは、これは非常に簡単な方法です。コントローラーコードを変更する必要はありません。 作成ビューと編集ビューでは、ディナーフォーム UI を実装するための共通の "Dinフォーム" 部分ビューが共有されているため、マップを1か所に追加して、作成と編集の両方のシナリオで使用することができます。

\Views\Dinners\DinnerForm.ascx 部分ビューを開き、それを更新して新しいマップ部分を含める必要があります。 次に示すのは、マップを追加した後に更新された Dinフォームがどのように表示されるかです (注: 簡潔にするために、HTML フォーム要素は次のコードスニペットから省略されています)。

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample3.aspx)]

上記の "Din" フォームは、モデルの種類として "Dinという型のオブジェクトを取得します (これには、ディナーオブジェクトと、国の dropdownlist を設定するための SelectList が必要であるため)。 マップ部分には、モデルの種類として "ディナー" 型のオブジェクトだけが必要です。そのため、マップの一部をレンダリングするときには、Dinare Formビューモデルのディナーサブプロパティのみを渡しています。

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample4.aspx)]

部分に追加した JavaScript 関数は jQuery を使用して "Address" HTML テキストボックスに "ぼかし" イベントをアタッチします。 ユーザーがテキストボックスをクリックしたり、タブをクリックしたりしたときに発生する "フォーカス" イベントについて耳にすることがあります。 反対は、ユーザーがテキストボックスを終了したときに発生する "ぼかし" イベントです。 上記のイベントハンドラーは、このような場合に緯度と経度のテキストボックスの値をクリアし、マップに新しいアドレスの場所をプロットします。 その後、マップの .js ファイル内で定義されたコールバックイベントハンドラーによって、指定したアドレスに基づいて virtual earth から返された値を使用して、フォーム上の経度と緯度のテキストボックスが更新されます。

ここでアプリケーションを再度実行し、[ホストディナー] タブをクリックすると、既定のマップが、標準のディナーフォーム要素と共に表示されます。

![](use-ajax-to-implement-mapping-scenarios/_static/image2.png)

アドレスを入力して tab キーを押したときに、マップが動的に更新されて場所が表示され、イベントハンドラーによって緯度/経度のテキストボックスに location 値が設定されます。

![](use-ajax-to-implement-mapping-scenarios/_static/image3.png)

新しいディナーを保存し、編集のためにもう一度開いた場合は、ページが読み込まれるときにマップの場所が表示されていることがわかります。

![](use-ajax-to-implement-mapping-scenarios/_static/image4.png)

Address フィールドが変更されるたびに、マップと緯度/経度の座標が更新されます。

これで、マップに夕食の場所が表示されるようになったので、緯度および経度のフォームフィールドを表示可能なテキストボックスから代わりに非表示の要素に変更することもできます (マップは住所が入力されるたびに自動的に更新されるため)。 これを行うには、.html () html ヘルパーを使用して、html. Hidden () ヘルパーメソッドを使用するように切り替えます。

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample5.aspx)]

これで、フォームはもう少しわかりやすくなり、生の緯度/経度が表示されないようになりました (ただし、各ディナーをデータベースに格納します)。

![](use-ajax-to-implement-mapping-scenarios/_static/image5.png)

### <a name="integrating-the-map-with-the-details-view"></a>マップと詳細ビューの統合

これで、作成と編集のシナリオにマップが統合されたので、詳細なシナリオと統合することもできます。 &lt;% .Html 部分 ("map") を呼び出す必要があります。詳細ビュー内の%&gt;。

完全な詳細ビュー (マップの統合を使用) のソースコードは次のようになります。

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample6.aspx)]

これで、ユーザーが//詳細/[id] の URL に移動すると、ディナーに関する詳細が表示されます。マップ上のディナーの場所 (ホバー時にマウスポインターを置いたときにプッシュピンを使用して完了すると、その連絡先のタイトルが表示されます) と、それに対する AJAX リンクがあります。

![](use-ajax-to-implement-mapping-scenarios/_static/image6.png)

### <a name="implementing-location-search-in-our-database-and-repository"></a>データベースとリポジトリでの場所検索の実装

AJAX の実装を終了するには、アプリケーションのホームページにマップを追加して、ユーザーが近くにあるディナーをグラフィカルに検索できるようにしましょう。

![](use-ajax-to-implement-mapping-scenarios/_static/image7.png)

まず、データベースとデータリポジトリレイヤー内にサポートを実装して、ディナーの場所ベースの radius 検索を効率的に実行します。 [Sql 2008 の新しい地理空間機能](https://www.microsoft.com/sqlserver/2008/en/us/spatial-data.aspx)を使用してこれを実装できます。または、次の記事で説明されているような sql 関数の手法を使用することもできます[http://www.codeproject.com/KB/cs/distancebetweenlocations.aspx](http://www.codeproject.com/KB/cs/distancebetweenlocations.aspx) 。詳細については、LINQ to SQL での使用については、「」を参照してください: [http://blog.wekeroad.com/2007/08/30/linq-and-geocoding/](http://blog.wekeroad.com/2007/08/30/linq-and-geocoding/)

この手法を実装するには、Visual Studio 内で "サーバーエクスプローラー" を開き、そのデータベースを選択してから、その下の "functions" サブノードを右クリックして、新しい "スカラー値関数" を作成します。

![](use-ajax-to-implement-mapping-scenarios/_static/image8.png)

次の DistanceBetween 関数を貼り付けます。

[!code-sql[Main](use-ajax-to-implement-mapping-scenarios/samples/sample7.sql)]

次に、"NearestDinners" を呼び出す新しいテーブル値関数 SQL Server を作成します。

![](use-ajax-to-implement-mapping-scenarios/_static/image9.png)

この "NearestDinners" テーブル関数は、DistanceBetween helper 関数を使用して、緯度の100マイル以内にすべてのディナーを返し、経度を指定します。

[!code-sql[Main](use-ajax-to-implement-mapping-scenarios/samples/sample8.sql)]

この関数を呼び出すには、最初に、次のように、-model ディレクトリ内のファイルをダブルクリックして LINQ to SQL デザイナーを開きます。

![](use-ajax-to-implement-mapping-scenarios/_static/image10.png)

次に、NearestDinners 関数と DistanceBetween 関数を LINQ to SQL デザイナーにドラッグします。これにより、LINQ to SQL でメソッドとして追加されます。

![](use-ajax-to-implement-mapping-scenarios/_static/image11.png)

次に、NearestDinner 関数を使用して、指定された場所の100マイル以内にある今後のディナーを返す、Dinのリポジトリクラスで "FindByLocation" クエリメソッドを公開できます。

[!code-csharp[Main](use-ajax-to-implement-mapping-scenarios/samples/sample9.cs)]

### <a name="implementing-a-json-based-ajax-search-action-method"></a>JSON ベースの AJAX 検索アクションメソッドの実装

ここでは、新しい FindByLocation () リポジトリメソッドを利用して、マップの設定に使用できるディナーデータのリストを返すコントローラーアクションメソッドを実装します。 このアクションメソッドによって、クライアント上で JavaScript を使用して簡単に操作できるように、ディナーデータを JSON (JavaScript Object Notation) 形式で返すことができます。

これを実装するには、新しい "SearchController" クラスを作成します。そのためには、\ Controllers ディレクトリを右クリックし、[&gt;コントローラー] メニューコマンドを選択します。 その後、次のように、新しい SearchController クラス内に "SearchByLocation" アクションメソッドを実装します。

[!code-csharp[Main](use-ajax-to-implement-mapping-scenarios/samples/sample10.cs)]

SearchController の SearchByLocation アクションメソッドは、内部的にディナーの一覧を取得するために、FindByLocation メソッドを Dinに呼び出します。 ただし、ディナーオブジェクトをクライアントに直接返すのではなく、代わりに JsonDinner オブジェクトを返します。 JsonDinner クラスは、ディナープロパティのサブセットを公開します (たとえば、セキュリティ上の理由から、ディナーを持つユーザーの名前は開示しません)。 また、ディナーには存在しない RSVPCount プロパティも含まれており、特定のディナーに関連付けられている RSVP オブジェクトの数をカウントすることによって動的に計算されます。

次に、コントローラーの基本クラスで Json () ヘルパーメソッドを使用して、JSON ベースのワイヤ形式を使用してディナーのシーケンスを返します。 JSON は、単純なデータ構造を表すための標準的なテキスト形式です。 次に、アクションメソッドから返されたときに、2つの JsonDinner オブジェクトの JSON 形式のリストがどのように見えるかを示します。

[!code-json[Main](use-ajax-to-implement-mapping-scenarios/samples/sample11.json)]

### <a name="calling-the-json-based-ajax-method-using-jquery"></a>JQuery を使用した JSON ベースの AJAX メソッドの呼び出し

次に、SearchController の SearchByLocation アクションメソッドを使用するように、このアプリケーションのホームページを更新する準備ができました。 これを行うには、/Views/Home/Index.aspx view テンプレートを開き、テキストボックス、検索ボタン、マップ、および &lt;div&gt; 要素を含むように更新します。

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample12.aspx)]

その後、次の2つの JavaScript 関数をページに追加できます。

[!code-html[Main](use-ajax-to-implement-mapping-scenarios/samples/sample13.html)]

最初の JavaScript 関数は、ページが最初に読み込まれたときにマップを読み込みます。 2番目の JavaScript 関数は、[検索] ボタンに JavaScript のクリックイベントハンドラーを配線します。 このボタンが押されると、次のように、マップの .js ファイルに追加する Finddinの Location () JavaScript 関数が呼び出されます。

[!code-javascript[Main](use-ajax-to-implement-mapping-scenarios/samples/sample14.js)]

この Finddinの Sいい Location () 関数は map を呼び出します。Virtual Earth コントロールで () を検索し、入力した場所に中央揃えで配置します。 Virtual earth マップサービスが戻ると、マップが返されます。Find () メソッドは、最後の引数として渡された callbackUpdateMapDinners callback メソッドを呼び出します。

CallbackUpdateMapDinners () メソッドは、実際の作業が行われる場所です。 JQuery の $. post () ヘルパーメソッドを使用して、SearchController の SearchByLocation () アクションメソッドに対する AJAX 呼び出しを実行します。これは、新しく中央に配置されたマップの緯度と経度を渡します。 これは、$ post () ヘルパーメソッドが完了したときに呼び出されるインライン関数を定義します。また、SearchByLocation () アクションメソッドから返される JSON 形式のディナー結果は、"ディナー" という変数を使用して渡されます。 次に、返された各ディナーで foreach を行い、ディナーの緯度と経度、およびその他のプロパティを使用してマップに新しい pin を追加します。 また、マップの右側にあるディナーの HTML リストに夕食エントリが追加されます。 次に、プッシュピンと HTML リストの両方のホバーイベントをワイヤアップします。これにより、ユーザーがマウスを置いたときにディナーの詳細が表示されます。

[!code-html[Main](use-ajax-to-implement-mapping-scenarios/samples/sample15.html)]

アプリケーションを実行してホームページにアクセスすると、マップが表示されます。 市区町村の名前を入力すると、マップに近い将来のディナーが表示されます。

![](use-ajax-to-implement-mapping-scenarios/_static/image12.png)

ディナーをポイントすると、その詳細が表示されます。

バブルまたは HTML リストの右側にあるディナーのタイトルをクリックすると、ディナーに移動します。これにより、必要に応じて次のことを行うことができます。

![](use-ajax-to-implement-mapping-scenarios/_static/image13.png)

### <a name="next-step"></a>次の手順

これで、世界中のアプリケーションのすべての機能を実装しました。 ここでは、自動化された単体テストを有効にする方法を見てみましょう。

> [!div class="step-by-step"]
> [前へ](use-ajax-to-deliver-dynamic-updates.md)
> [次へ](enable-automated-unit-testing.md)
