---
uid: mvc/overview/older-versions-1/security/preventing-javascript-injection-attacks-vb
title: JavaScript インジェクション攻撃の防止 (VB) |Microsoft Docs
author: StephenWalther
description: JavaScript インジェクション攻撃やクロスサイトスクリプティング攻撃を防ぐことができます。 このチュートリアルでは、Stephen Walther が簡単に実行を解除する方法について説明します。
ms.author: riande
ms.date: 08/19/2008
ms.assetid: 9274a72e-34dd-4dae-8452-ed733ae71377
msc.legacyurl: /mvc/overview/older-versions-1/security/preventing-javascript-injection-attacks-vb
msc.type: authoredcontent
ms.openlocfilehash: dfe09085f26c62c566649bc6f570aa25367a0f07
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78506224"
---
# <a name="preventing-javascript-injection-attacks-vb"></a>JavaScript インジェクション攻撃を防ぐ (VB)

[Stephen Walther](https://github.com/StephenWalther)

[[Download PDF]\(PDF をダウンロード\)](https://download.microsoft.com/download/8/4/8/84843d8d-1575-426c-bcb5-9d0c42e51416/ASPNET_MVC_Tutorial_06_VB.pdf)

> JavaScript インジェクション攻撃やクロスサイトスクリプティング攻撃を防ぐことができます。 このチュートリアルでは、Stephen Walther が、コンテンツを HTML エンコードすることによって、これらの種類の攻撃を簡単に打破する方法について説明します。

このチュートリアルの目的は、ASP.NET MVC アプリケーションでの JavaScript インジェクション攻撃を防ぐ方法を説明することです。 このチュートリアルでは、JavaScript インジェクション攻撃に対して web サイトを防御する2つの方法について説明します。 表示するデータをエンコードすることによって、JavaScript インジェクション攻撃を防ぐ方法について説明します。 また、受け入れるデータをエンコードすることによって、JavaScript インジェクション攻撃を防ぐ方法についても説明します。

## <a name="what-is-a-javascript-injection-attack"></a>JavaScript インジェクション攻撃とは何ですか。

ユーザーの入力を受け入れ、ユーザー入力を再表示するたびに、web サイトを開いて JavaScript インジェクション攻撃を受けることができます。 JavaScript インジェクション攻撃に対して開かれている具象アプリケーションを見てみましょう。

顧客フィードバック web サイトを作成したことを想像してください (図1を参照)。 お客様は、web サイトにアクセスして、製品を使用した経験に関するフィードバックを入力できます。 お客様からのフィードバックが送信されると、フィードバックページにフィードバックが再反映されます。

[![カスタマーフィードバック Web サイト](preventing-javascript-injection-attacks-vb/_static/image2.png)](preventing-javascript-injection-attacks-vb/_static/image1.png)

**図 01**: 顧客フィードバック web サイト ([クリックすると、フルサイズの画像が表示](preventing-javascript-injection-attacks-vb/_static/image3.png)される)

カスタマーフィードバック web サイトでは、リスト1の `controller` を使用します。 この `controller` には、`Index()` と `Create()`という2つのアクションが含まれています。

**リスト1– `HomeController.vb`**

[!code-vb[Main](preventing-javascript-injection-attacks-vb/samples/sample1.vb)]

`Index()` メソッドは、`Index` ビューを表示します。 このメソッドは、(LINQ to SQL クエリを使用して) データベースからフィードバックを取得することによって、以前の顧客からのフィードバックをすべて `Index` ビューに渡します。

`Create()` メソッドは、新しいフィードバック項目を作成し、データベースに追加します。 顧客がフォームに入力するメッセージは、メッセージパラメーターの `Create()` メソッドに渡されます。 フィードバック項目が作成され、メッセージがフィードバック項目の `Message` プロパティに割り当てられます。 フィードバック項目は、`DataContext.SubmitChanges()` メソッドの呼び出しを使用してデータベースに送信されます。 最後に、ビジターは、すべてのフィードバックが表示される `Index` ビューにリダイレクトされます。

`Index` ビューは、リスト2に含まれています。

**リスト2– `Index.aspx`**

[!code-aspx[Main](preventing-javascript-injection-attacks-vb/samples/sample2.aspx)]

`Index` ビューには、2つのセクションがあります。 上部のセクションには、実際のカスタマーフィードバックフォームが含まれています。 下部セクションには、のが含まれています。前のすべての顧客フィードバック項目をループ処理し、各フィードバック項目の EntryDate プロパティと Message プロパティを表示する各ループ。

カスタマーフィードバック web サイトは、単純な web サイトです。 残念ながら、この web サイトは JavaScript インジェクション攻撃に対して開かれています。

カスタマーフィードバックフォームに次のテキストを入力したとします。

[!code-html[Main](preventing-javascript-injection-attacks-vb/samples/sample3.html)]

このテキストは、警告メッセージボックスを表示する JavaScript スクリプトを表します。 だれかがこのスクリプトをフィードバックフォームに送信した後、メッセージ<em>Boo!</em>今後、ユーザーフィードバック web サイトにアクセスするたびに表示されます (図2を参照)。

[![JavaScript インジェクション](preventing-javascript-injection-attacks-vb/_static/image5.png)](preventing-javascript-injection-attacks-vb/_static/image4.png)

**図 02**: JavaScript インジェクション ([クリックすると、フルサイズの画像が表示](preventing-javascript-injection-attacks-vb/_static/image6.png)される)

これで、JavaScript インジェクション攻撃に対する最初の応答が必要になる可能性があります。 JavaScript インジェクション攻撃は単なる一種の*本位*攻撃であると考えられます。 JavaScript インジェクション攻撃をコミットすることによって、まったく何も実行できないと思われるかもしれません。

残念ながら、ハッカーは、web サイトに JavaScript を挿入することによって、本当に悪なことを行うことができます。 JavaScript インジェクション攻撃を使用して、クロスサイトスクリプティング (XSS) 攻撃を行うことができます。 クロスサイトスクリプティング攻撃では、機密ユーザー情報を盗み、別の web サイトに情報を送信します。

たとえば、ハッカーは JavaScript インジェクション攻撃を使用して、他のユーザーからのブラウザー cookie の値を盗むことができます。 パスワード、クレジットカード番号、社会保障番号などの機密情報がブラウザーの cookie に格納されている場合、ハッカーは JavaScript インジェクション攻撃を使用してこの情報を盗むことができます。 また、JavaScript 攻撃によって侵害されたページに含まれるフォームフィールドにユーザーが機密情報を入力した場合、ハッカーは、挿入された JavaScript を使用してフォームデータを取得し、別の web サイトに送信することができます。

*怖いであることを確認してください*。 JavaScript インジェクション攻撃を真剣に実行し、ユーザーの機密情報を保護します。 次の2つのセクションでは、ASP.NET MVC アプリケーションを JavaScript インジェクション攻撃から保護するために使用できる2つの手法について説明します。

## <a name="approach-1-html-encode-in-the-view"></a>方法 #1: ビューでの HTML エンコード

JavaScript インジェクション攻撃を防ぐ簡単な方法の1つは、データをビューに再表示するときに、web サイトのユーザーが入力したデータを HTML エンコードすることです。 リスト3の更新された `Index` ビューは、この方法に従います。

**リスト3– `Index.aspx` (HTML エンコード)**

[!code-aspx[Main](preventing-javascript-injection-attacks-vb/samples/sample4.aspx)]

次のコードを使用して値を表示する前に、`feedback.Message` の値が HTML エンコードされていることに注意してください。

[!code-aspx[Main](preventing-javascript-injection-attacks-vb/samples/sample5.aspx)]

HTML で文字列をエンコードするとはどういう意味ですか。 文字列を HTML エンコードすると、`<` や `>` などの危険な文字が、`&lt;` や `&gt;`などの HTML エンティティ参照に置き換えられます。 したがって、文字列 `<script>alert("Boo!")</script>` が HTML エンコードされている場合は、`&lt;script&gt;alert(&quot;Boo!&quot;)&lt;/script&gt;`に変換されます。 エンコードされた文字列は、ブラウザーで解釈されるときに JavaScript スクリプトとして実行されなくなりました。 代わりに、図3の無害なページが表示されます。

[![が敗北した JavaScript 攻撃](preventing-javascript-injection-attacks-vb/_static/image8.png)](preventing-javascript-injection-attacks-vb/_static/image7.png)

**図 03**: 悪用される JavaScript 攻撃 ([クリックしてフルサイズのイメージを表示する](preventing-javascript-injection-attacks-vb/_static/image9.png))

リスト3の `Index` ビューでは、`feedback.Message` の値のみがエンコードされていることに注意してください。 `feedback.EntryDate` の値がエンコードされていません。 ユーザーが入力したデータをエンコードするだけで済みます。 EntryDate の値がコントローラーで生成されたため、この値を HTML エンコードする必要はありません。

## <a name="approach-2-html-encode-in-the-controller"></a>方法 #2: コントローラーでの HTML エンコード

データをビューに表示するときに HTML エンコードデータを使用するのではなく、データをデータベースに送信する直前に HTML エンコードできます。 この2番目の方法は、リスト4の `controller` の場合に使用します。

**リスト4– `HomeController.cs` (HTML エンコード)**

[!code-vb[Main](preventing-javascript-injection-attacks-vb/samples/sample6.vb)]

`Create()` アクション内で値がデータベースに送信される前に、メッセージの値が HTML エンコードされていることに注意してください。 メッセージがビューに再表示されると、メッセージは HTML エンコードされ、メッセージに挿入された JavaScript は実行されません。

通常、この2つ目の方法では、このチュートリアルで説明した最初のアプローチを優先する必要があります。 この2番目の方法で問題となるのは、データベースに HTML エンコードされたデータがあることです。 言い換えると、データベースデータには、ダーティの文字が表示されます。

なぜこれが悪いのでしょうか。 データベースのデータを web ページ以外に表示する必要がある場合は、問題が発生します。 たとえば、Windows フォームアプリケーションでは、データを簡単に表示できなくなります。

## <a name="summary"></a>まとめ

このチュートリアルの目的は、JavaScript インジェクション攻撃の対象となることです。 このチュートリアルでは、ASP.NET MVC アプリケーションを JavaScript インジェクション攻撃に対して保護するための2つの方法について説明しました。ユーザーが表示するデータを HTML エンコードするか、ユーザーが送信したデータをコントローラーに HTML エンコードすることができます。

> [!div class="step-by-step"]
> [[戻る]](authenticating-users-with-windows-authentication-vb.md)
