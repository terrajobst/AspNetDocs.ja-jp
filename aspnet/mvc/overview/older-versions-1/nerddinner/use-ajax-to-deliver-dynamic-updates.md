---
uid: mvc/overview/older-versions-1/nerddinner/use-ajax-to-deliver-dynamic-updates
title: AJAX を使用して動的更新を配信する |Microsoft Docs
author: microsoft
description: 手順10では、ログインしているユーザーが、ディナーの詳細に統合された Ajax ベースのアプローチを使用して、ディナーに参加することに関心があることを RSVP に対してサポートします。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 18700815-8e6c-4489-91af-7ea9dab6529e
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-ajax-to-deliver-dynamic-updates
msc.type: authoredcontent
ms.openlocfilehash: 3edc02fec546609505b5e085440fa684abe7acd0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486310"
---
# <a name="use-ajax-to-deliver-dynamic-updates"></a>AJAX を使用し、動的更新を配信する

[Microsoft](https://github.com/microsoft)

[[Download PDF]\(PDF をダウンロード\)](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> これは、ASP.NET MVC 1 を使用して小規模で完成した web アプリケーションを構築する方法について説明する無料の["" アプリケーションのチュートリアル](introducing-the-nerddinner-tutorial.md)の手順10です。
> 
> 手順10では、ログインしているユーザーが、ディナーの詳細ページに統合された Ajax ベースのアプローチを使用して、ディナーに参加することを目的として RSVP を管理します。
> 
> ASP.NET MVC 3 を使用している場合は、MVC 3 または[Mvc ミュージックストア](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)[のチュートリアルではじめに](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)に従うことをお勧めします。

## <a name="nerddinner-step-10-ajax-enabling-rsvps-accepts"></a>ステップ 10: AJAX で RSVPs を有効にする

次に、ログインしているユーザーのサポートを実装して、ディナーに参加することを目的としています。 これは、ディナーの詳細ページで統合された AJAX ベースのアプローチを使用して有効にします。

### <a name="indicating-whether-the-user-is-rsvpd"></a>ユーザーが RSVP であるかどうかを示す

ユーザーは、 *[id*] の URL にアクセスして、特定のディナーに関する詳細を確認できます。

![](use-ajax-to-deliver-dynamic-updates/_static/image1.png)

Details () アクションメソッドは、次のように実装されます。

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample1.cs)]

RSVP サポートを実装する最初の手順として、先ほど作成した Dinner.cs 部分クラス内で、"IsUserRegistered (username)" ヘルパーメソッドをディナーオブジェクトに追加します。 このヘルパーメソッドは、ユーザーが現在ディナーであるかどうかによって、true または false を返します。

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample2.cs)]

その後、次のコードを Details ビューテンプレートに追加して、ユーザーがイベントに対して登録されているかどうかを示す適切なメッセージを表示することができます。

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample3.html)]

これで、ユーザーがディナーにアクセスすると、次のメッセージが表示されます。

![](use-ajax-to-deliver-dynamic-updates/_static/image2.png)

また、お客様がディナーにアクセスすると、次のメッセージが表示されます。

![](use-ajax-to-deliver-dynamic-updates/_static/image3.png)

### <a name="implementing-the-register-action-method"></a>Register アクションメソッドの実装

次に、ユーザーが [詳細] ページからディナーを使用できるようにするために必要な機能を追加してみましょう。

これを実装するには、新しい "RSVPController" クラスを作成します。そのためには、\ Controllers ディレクトリを右クリックし、[&gt;コントローラー] メニューコマンドを選択します。

新しい RSVPController クラス内に "Register" アクションメソッドを実装します。このクラスは、ディナーの id を引数として受け取り、適切なディナーオブジェクトを取得し、ログインしているユーザーが現在、登録されているユーザーの一覧にあるかどうかを確認します。では、次のように RSVP オブジェクトが追加されません。

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample4.cs)]

ここでは、アクションメソッドの出力として簡単な文字列を返す方法について説明します。 ビューテンプレート内にこのメッセージを埋め込むこともできますが、そのため、コントローラーの基本クラスで Content () ヘルパーメソッドを使用し、上記のような文字列メッセージを返すだけです。

### <a name="calling-the-rsvpforevent-action-method-using-ajax"></a>AJAX を使用した RSVPForEvent アクションメソッドの呼び出し

AJAX を使用して、詳細ビューからレジスタアクションメソッドを呼び出します。 この実装は非常に簡単です。 まず、2つのスクリプトライブラリ参照を追加します。

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample5.html)]

最初のライブラリは、中核となる ASP.NET AJAX クライアント側スクリプトライブラリを参照します。 このファイルのサイズは約24k で、クライアント側の AJAX のコア機能が含まれています。 2番目のライブラリには、ASP.NET MVC の組み込み AJAX ヘルパーメソッドと統合するユーティリティ関数が含まれています (これはすぐに使用します)。

その後、先ほど追加したビューテンプレートコードを更新して、"このイベントに登録されていません" というメッセージを出力するのではなく、プッシュ時に、その RSVP コントローラーで RSVPForEvent アクションメソッドを呼び出す AJAX 呼び出しを実行するリンクをレンダリングします。ユーザーを RSVPs します。

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample6.aspx)]

上記で使用した Html.actionlink () ヘルパーメソッドは ASP.NET MVC に組み込まれており、Html.actionlink () ヘルパーメソッドに似ています。ただし、標準ナビゲーションを実行する代わりに、リンクをクリックすると、AJAX 呼び出しがアクションメソッドに対して行われる点が異なります。 上記の例では、"RSVP" コントローラーで "Register" アクションメソッドを呼び出し、その Id を "id" パラメーターとして渡しています。 渡される最後の AjaxOptions パラメーターは、アクションメソッドから返されたコンテンツを取得し、id が "rsvpmsg" であるページの HTML &lt;div&gt; 要素を更新することを示します。

これで、ユーザーが夕食に登録されていない場合は、それに対する RSVP へのリンクが表示されます。

![](use-ajax-to-deliver-dynamic-updates/_static/image4.png)

これらのユーザーが "このイベントの RSVP" リンクをクリックすると、次のようなメッセージが表示され、それが完了すると、次のようなメッセージが表示されます。

![](use-ajax-to-deliver-dynamic-updates/_static/image5.png)

この AJAX 呼び出しを行う際に関係するネットワーク帯域幅とトラフィックは、非常に軽量です。 ユーザーが [このイベントの RSVP] リンクをクリックすると、次のような */Dinners/Register/1* URL に対して小さな HTTP POST ネットワーク要求が行われます。

[!code-console[Main](use-ajax-to-deliver-dynamic-updates/samples/sample7.cmd)]

また、登録アクションメソッドからの応答は、単純に次のようになります。

[!code-console[Main](use-ajax-to-deliver-dynamic-updates/samples/sample8.cmd)]

この軽量な呼び出しは高速で、低速のネットワークでも機能します。

### <a name="adding-a-jquery-animation"></a>JQuery アニメーションの追加

実装した AJAX の機能は、適切で高速に動作します。 場合によっては、RSVP リンクが新しいテキストに置き換えられたことがユーザーに通知されないことがあります。 結果を少し明確にするために、更新メッセージに注目する単純なアニメーションを追加できます。

既定の ASP.NET MVC プロジェクトテンプレートには、jQuery – Microsoft でもサポートされている、優れた (かつ人気のある) オープンソース JavaScript ライブラリが含まれています。 jQuery には、優れた HTML DOM の選択や効果ライブラリなど、さまざまな機能が用意されています。

JQuery を使用するには、まずスクリプト参照を追加します。 ここでは、サイト内のさまざまな場所で jQuery を使用します。そのため、すべてのページで使用できるように、サイトのマスターページファイルにスクリプト参照を追加します。

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample9.html)]

*ヒント: JavaScript ファイル (jQuery を含む) に対するより高度な intellisense のサポートを有効にする、VS 2008 SP1 用の JavaScript intellisense 修正プログラムがインストールされていることを確認します。次のものからダウンロードできます: http://tinyurl.com/vs2008javascripthotfix*

JQuery を使用して記述されたコードは、多くの場合、CSS セレクターを使用して1つ以上の HTML 要素を取得する、グローバルな "$ ()" JavaScript メソッドを使用します。 たとえば、 *$ ("#rsvpmsg")* は、rsvpmsg の id を持つ HTML 要素を選択します。 *$ ("...")* は、CSS クラス名が "何か" のすべての要素を選択します。 また、次のようなセレクタークエリ *("input [@type= radio] [@checked]")* を使用して、"チェックされたすべてのラジオボタンを返す" など、より高度なクエリを作成することもできます。

要素を選択したら、それらのメソッドを呼び出して、 *$ ("#rsvpmsg"). hide ();* を非表示にするなどの操作を行うことができます。

ここでは、"AnimateRSVPMessage" という名前の単純な JavaScript 関数を定義します。この関数は、"rsvpmsg" &lt;div&gt; を選択し、テキストコンテンツのサイズをアニメーション化します。 次のコードでは、テキストを小さくしてから、400ミリ秒の期間を増やしています。

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample10.html)]

次に、AJAX 呼び出しが正常に完了した後に呼び出されるように、この JavaScript 関数を接続できます。これを行うには、Html.actionlink () ヘルパーメソッド (AjaxOptions "OnSuccess" イベントプロパティを使用) に名前を渡します。

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample11.aspx)]

これで、"このイベントの RSVP" リンクがクリックされ、AJAX 呼び出しが正常に完了すると、返送されたコンテンツメッセージはアニメーション化され、大きくなります。

![](use-ajax-to-deliver-dynamic-updates/_static/image6.png)

AjaxOptions オブジェクトは、"OnSuccess" イベントを提供するだけでなく、(他のさまざまなプロパティや便利なオプションと共に) 処理できる OnBegin、OnFailure、および Onbegin イベントを公開します。

### <a name="cleanup---refactor-out-a-rsvp-partial-view"></a>クリーンアップ-RSVP 部分ビューをリファクターします。

詳細ビューのテンプレートは少し時間がかかります。そのため、超過しても理解が困難になります。 コードの読みやすさを向上させるために、詳細ページのすべての RSVP ビューコードをカプセル化する部分ビュー (RSVPStatus. .ascx) を作成してみましょう。

これを行うには、\Views\Dinners フォルダーを右クリックし、[&gt;ビューの追加] メニューコマンドを選択します。 ここでは、厳密に型指定されたビューモデルとしてディナーオブジェクトを取得します。 その後、詳細 .aspx ビューの RSVP コンテンツをコピーして、それに貼り付けることができます。

これが完了したら、編集と削除のリンクビューコードをカプセル化するもう1つの部分ビュー (EditAndDeleteLinks) も作成します。 また、このメソッドは、厳密に型指定されたビューモデルとしてディナーオブジェクトを取得し、詳細な .aspx ビューから編集および削除ロジックをコピー/貼り付けます。

詳細ビューテンプレートでは、次の2つの Html. RenderPartial () メソッドの呼び出しを一番下に含めることができます。

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample12.aspx)]

これにより、コードが読みやすくなり、維持されます。

### <a name="next-step"></a>次の手順

AJAX をさらに使用して、対話的なマッピングのサポートをアプリケーションに追加する方法を見てみましょう。

> [!div class="step-by-step"]
> [前へ](secure-applications-using-authentication-and-authorization.md)
> [次へ](use-ajax-to-implement-mapping-scenarios.md)
