---
uid: web-api/overview/advanced/sending-html-form-data-part-1
title: 'ASP.NET Web API で HTML フォームデータを送信する: url エンコード Data-ASP.NET 4.x'
author: MikeWasson
description: この記事では、ASP.NET 4.x を使用して Web API コントローラーにフォーム url エンコードデータを投稿する方法を示します。
ms.author: riande
ms.date: 06/15/2012
ms.custom: seoapril2019
ms.assetid: 585351c4-809a-4bf5-bcbe-35d624f565fe
msc.legacyurl: /web-api/overview/advanced/sending-html-form-data-part-1
msc.type: authoredcontent
ms.openlocfilehash: 7243069dbd8051b1374ed6e0112c273b8fe26f61
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449242"
---
# <a name="sending-html-form-data-in-aspnet-web-api-form-urlencoded-data"></a>ASP.NET Web API での HTML フォームデータの送信: フォーム url エンコードデータ

[Mike Wasson](https://github.com/MikeWasson)

## <a name="part-1-form-urlencoded-data"></a>パート 1: フォーム url エンコードデータ

この記事では、Web API コントローラーにフォーム url エンコードデータを投稿する方法について説明します。

- [HTML フォームの概要](#overview_of_html_forms)
- [複合型の送信](#sending_complex_types)
- [AJAX を使用したフォームデータの送信](#sending_form_data_via_ajax)
- [単純型の送信](#sending_simple_types)

> [!NOTE]
> [完成したプロジェクトをダウンロード](https://code.msdn.microsoft.com/ASPNET-Web-API-Sending-a6f9d007)します。

<a id="overview_of_html_forms"></a>
## <a name="overview-of-html-forms"></a>HTML フォームの概要

HTML 形式では、GET または POST を使用してサーバーにデータを送信します。 **Form**要素の**method**属性は、次のように HTTP メソッドを提供します。

[!code-html[Main](sending-html-form-data-part-1/samples/sample1.html)]

既定のメソッドは GET です。 フォームで GET が使用されている場合、フォームデータは URI でクエリ文字列としてエンコードされます。 フォームが POST を使用する場合、フォームデータは要求本文に配置されます。 ポストされたデータの場合、 **enctype**属性は要求本文の形式を指定します。

| enctype | Description |
| --- | --- |
| application/x-www-form-urlencoded | フォームデータは、URI クエリ文字列と同様に、名前と値のペアとしてエンコードされます。 これは、POST の既定の形式です。 |
| マルチパート/フォーム-データ | フォームデータは、マルチパート MIME メッセージとしてエンコードされます。 ファイルをサーバーにアップロードする場合は、この形式を使用します。 |

この記事のパート1では、url エンコード形式について説明します。 パート[2](sending-html-form-data-part-2.md)では、マルチパート MIME について説明します。

<a id="sending_complex_types"></a>
## <a name="sending-complex-types"></a>複合型の送信

通常は、複数のフォームコントロールから取得した値で構成される複合型を送信します。 状態の更新を表す次のモデルを考えてみましょう。

[!code-csharp[Main](sending-html-form-data-part-1/samples/sample2.cs)]

POST を使用して `Update` オブジェクトを受け入れる Web API コントローラーを次に示します。

[!code-csharp[Main](sending-html-form-data-part-1/samples/sample3.cs)]

> [!NOTE]
> このコントローラーは[アクションベースのルーティング](../web-api-routing-and-actions/routing-in-aspnet-web-api.md#routing_by_action_name)を使用しているため、ルートテンプレートは &quot;api/{controller}/{action}/{id}&quot;になります。 クライアントは、&quot;/api&quot;にデータを送信します。

次に、ユーザーがステータスの更新を送信するための HTML フォームを作成してみましょう。

[!code-html[Main](sending-html-form-data-part-1/samples/sample4.html)]

フォームの**action**属性がコントローラーアクションの URI であることに注意してください。 次に、に入力されたいくつかの値を含むフォームを示します。

![](sending-html-form-data-part-1/_static/image1.png)

ユーザーが [送信] をクリックすると、ブラウザーは次のような HTTP 要求を送信します。

[!code-console[Main](sending-html-form-data-part-1/samples/sample5.cmd)]

要求本文に、名前と値のペアとして書式設定されたフォームデータが含まれていることに注意してください。 Web API は、名前と値のペアを `Update` クラスのインスタンスに自動的に変換します。

<a id="sending_form_data_via_ajax"></a>
## <a name="sending-form-data-via-ajax"></a>AJAX を使用したフォームデータの送信

ユーザーがフォームを送信すると、ブラウザーは現在のページから移動し、応答メッセージの本文を表示します。 応答が HTML ページの場合は問題ありません。 ただし、web API では、通常、応答本文は空であるか、JSON などの構造化データを含んでいます。 そのような場合は、AJAX 要求を使用してフォームデータを送信して、ページが応答を処理できるようにする方がよりわかりやすくなります。

次のコードは、jQuery を使用してフォームデータをポストする方法を示しています。

[!code-html[Main](sending-html-form-data-part-1/samples/sample6.html)]

JQuery **submit**関数は、フォームアクションを新しい関数に置き換えます。 これにより、[送信] ボタンの既定の動作がオーバーライドされます。 Serialize 関数は、フォームデータを名前と値のペアにシリアル**化**します。 フォームデータをサーバーに送信するには、`$.post()`を呼び出します。

要求が完了すると、`.success()` または `.error()` ハンドラーによって、ユーザーに適切なメッセージが表示されます。

![](sending-html-form-data-part-1/_static/image2.png)

<a id="sending_simple_types"></a>
## <a name="sending-simple-types"></a>単純型の送信

前のセクションでは、モデルクラスのインスタンスに Web API が逆シリアル化された複合型を送信しました。 文字列などの単純型を送信することもできます。

> [!NOTE]
> 単純型を送信する前に、複合型に値をラップすることを検討してください。 これにより、サーバー側でのモデル検証の利点が得られ、必要に応じてモデルを拡張しやすくなります。

単純型を送信する基本的な手順は同じですが、微妙な違いが2つあります。 まず、コントローラーで、 **Frombody**属性を使用してパラメーター名を修飾する必要があります。

[!code-csharp[Main](sending-html-form-data-part-1/samples/sample7.cs?highlight=3)]

既定では、Web API は要求 URI から単純型を取得しようとします。 **Frombody**属性は、要求本文から値を読み取るように Web API に指示します。

> [!NOTE]
> Web API は応答本文を最大で1回読み取ります。そのため、要求本文から取得できるアクションのパラメーターは1つだけです。 要求本文から複数の値を取得する必要がある場合は、複合型を定義します。

次に、クライアントは、次の形式で値を送信する必要があります。

[!code-xml[Main](sending-html-form-data-part-1/samples/sample8.xml)]

具体的には、単純型の場合、名前と値のペアの名前部分は空である必要があります。 すべてのブラウザーが HTML フォームに対してこれをサポートしているわけではありませんが、次のようにスクリプトでこの形式を作成します。

[!code-javascript[Main](sending-html-form-data-part-1/samples/sample9.js)]

フォームの例を次に示します。

[!code-html[Main](sending-html-form-data-part-1/samples/sample10.html)]

フォーム値を送信するスクリプトを次に示します。 前のスクリプトとの唯一の違いは、 **post**関数に渡される引数です。

[!code-javascript[Main](sending-html-form-data-part-1/samples/sample11.js?highlight=2)]

同じ方法を使用して、単純型の配列を送信できます。

[!code-javascript[Main](sending-html-form-data-part-1/samples/sample12.js)]

## <a name="additional-resources"></a>その他のリソース

[パート 2: ファイルのアップロードとマルチパート MIME](sending-html-form-data-part-2.md)
