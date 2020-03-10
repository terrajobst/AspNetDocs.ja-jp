---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-6
title: 'パート 6: ASP.NET Membership |Microsoft Docs'
author: JoeStagner
description: このチュートリアルシリーズでは、Tailspin Spyworks サンプルアプリケーションを構築するために実行するすべての手順について詳しく説明します。 パート6では、ASP.NET メンバーシップを追加します。
ms.author: riande
ms.date: 07/21/2010
ms.assetid: f70a310c-9557-4743-82cb-655265676d39
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-6
msc.type: authoredcontent
ms.openlocfilehash: b0caa89dc9ffb5bb7451fa2d9d346c7db2bf1466
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78454882"
---
# <a name="part-6-aspnet-membership"></a>パート 6: ASP.NET メンバーシップ

[Joe Stagner](https://github.com/JoeStagner)

> Tailspin Spyworks は、.NET プラットフォーム用の強力でスケーラブルなアプリケーションを簡単に作成する方法を示しています。 ASP.NET 4 の優れた新機能を使用して、ショッピング、チェックアウト、管理などのオンラインストアを構築する方法を示しています。
> 
> このチュートリアルシリーズでは、Tailspin Spyworks サンプルアプリケーションを構築するために実行するすべての手順について詳しく説明します。 パート6では、ASP.NET メンバーシップを追加します。

## <a id="_Toc260221672"></a>ASP.NET メンバーシップの使用

![](tailspin-spyworks-part-6/_static/image1.png)

[セキュリティ] をクリックします。

![](tailspin-spyworks-part-6/_static/image1.jpg)

フォーム認証を使用していることを確認します。

![](tailspin-spyworks-part-6/_static/image2.jpg)

[Create User] \ (ユーザーの作成 \) リンクを使用して、いくつかのユーザーを作成します。

![](tailspin-spyworks-part-6/_static/image3.jpg)

完了したら、[ソリューションエクスプローラー] ウィンドウを参照して、ビューを更新します。

![](tailspin-spyworks-part-6/_static/image2.png)

ASPNETDB.MDF であることに注意してください。MDF が正常に作成されました。 このファイルには、メンバーシップのようなコア ASP.NET サービスをサポートするテーブルが含まれています。

これで、チェックアウトプロセスの実装を開始できます。

まず、CheckOut ページを作成します。

チェックアウトページは、ログインしているユーザーのみが使用できるようにする必要があります。ログインしているユーザーへのアクセスを制限し、ログインページにログインしていないユーザーをリダイレクトします。

これを行うには、web.config ファイルの構成セクションに次の内容を追加します。

[!code-xml[Main](tailspin-spyworks-part-6/samples/sample1.xml)]

ASP.NET Web フォームアプリケーション用のテンプレートによって、認証セクションが web.config ファイルに自動的に追加され、既定のログインページが確立されました。

[!code-xml[Main](tailspin-spyworks-part-6/samples/sample2.xml)]

ユーザーがログインするときに、匿名ショッピングカートを移行するには、login.aspx コードビハインドファイルを変更する必要があります。 次のように、ページ\_読み込みイベントを変更します。

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample3.cs)]

次に、このような "LoggedIn" イベントハンドラーを追加して、新しくログインしたユーザーにセッション名を設定し、MyShoppingCart クラスの MigrateCart メソッドを呼び出して、ショッピングカート内の一時的なセッション id をユーザーの一時的なセッション id に変更します。 (.Cs ファイルに実装されています)

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample4.cs)]

このような MigrateCart () メソッドを実装します。

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample5.cs)]

Checkout では、ショッピングカートページで行ったように、チェックアウトページで EntityDataSource と GridView を使用します。

[!code-aspx[Main](tailspin-spyworks-part-6/samples/sample6.aspx)]

GridView コントロールで、\_MyList という名前の "ondatabound バインド" イベントハンドラーが指定されていることに注意してください。そのため、このようなイベントハンドラーを実装してみましょう。

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample7.cs)]

このメソッドは、各行がバインドされ、GridView の下部の行を更新するときに、ショッピングカートの累計を保持します。

この段階では、配置する順序の "レビュー" プレゼンテーションを実装しました。

次のように、ページ\_の読み込みイベントに数行のコードを追加して、空のカートシナリオを処理してみましょう。

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample8.cs)]

ユーザーが [送信] ボタンをクリックすると、[送信] ボタンの [イベントハンドラー] で次のコードが実行されます。

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample9.cs)]

注文送信プロセスの "肉" は、MyShoppingCart クラスの SubmitOrder () メソッドに実装されます。

SubmitOrder は次のようになります。

- ショッピングカート内のすべての品目を取得し、それらを使用して新しい注文レコードと関連付けられた OrderDetails レコードを作成します。
- 出荷日を計算します。
- ショッピングカートをクリアします。

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample10.cs)]

このサンプルアプリケーションでは、現在の日付に2日を加算するだけで出荷日を計算します。

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample11.cs)]

今すぐアプリケーションを実行すると、ショッピングプロセスを開始から終了までテストできるようになります。

> [!div class="step-by-step"]
> [前へ](tailspin-spyworks-part-5.md)
> [次へ](tailspin-spyworks-part-7.md)
