---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-9
title: 'パート 9: 登録とチェックアウト |Microsoft Docs'
author: jongalloway
description: このチュートリアルシリーズでは、ASP.NET MVC ミュージックストアサンプルアプリケーションをビルドするために実行するすべての手順について詳しく説明します。 パート9では、登録とチェックアウトについて説明します。
ms.author: riande
ms.date: 04/21/2011
ms.assetid: d65c5c2b-a039-463f-ad29-25cf9fb7a1ba
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-9
msc.type: authoredcontent
ms.openlocfilehash: 040bc0ccef889fb9a7c3d9b5ce88c75b7b754248
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78450898"
---
# <a name="part-9-registration-and-checkout"></a>パート 9: 登録とチェックアウト

( [Jon Galloway](https://github.com/jongalloway) )

> MVC Music Store は、ASP.NET MVC と Visual Studio を使用して web 開発を行う方法を紹介したチュートリアルアプリケーションです。  
>   
> MVC ミュージックストアは、音楽アルバムをオンラインで販売し、基本的なサイト管理、ユーザーサインイン、およびショッピングカート機能を実装する軽量のサンプルストア実装です。  
>   
> このチュートリアルシリーズでは、ASP.NET MVC ミュージックストアサンプルアプリケーションをビルドするために実行するすべての手順について詳しく説明します。 パート9では、登録とチェックアウトについて説明します。

このセクションでは、顧客の住所と支払い情報を収集する CheckoutController を作成します。 ユーザーは、チェックアウトの前にサイトに登録する必要があるため、このコントローラーには承認が必要です。

ユーザーは、[チェックアウト] ボタンをクリックして、ショッピングカートからチェックアウトプロセスに移動します。

![](mvc-music-store-part-9/_static/image1.jpg)

ユーザーがログインしていない場合は、メッセージが表示されます。

![](mvc-music-store-part-9/_static/image1.png)

ログインが成功すると、ユーザーにはアドレスと支払いのビューが表示されます。

![](mvc-music-store-part-9/_static/image2.png)

フォームに入力して注文を送信すると、注文確認画面が表示されます。

![](mvc-music-store-part-9/_static/image3.png)

存在しない順序を表示しようとしたか、または属していない順序を表示しようとすると、エラービューが表示されます。

![](mvc-music-store-part-9/_static/image4.png)

## <a name="migrating-the-shopping-cart"></a>ショッピングカートの移行

ショッピングプロセスは匿名ですが、ユーザーが [チェックアウト] ボタンをクリックすると、登録とログインが必要になります。 ユーザーは、訪問の間にショッピングカートの情報を保持することを期待しています。そのため、登録またはログインが完了したら、ショッピングカートの情報をユーザーに関連付ける必要があります。

ShoppingCart クラスには、現在のカート内のすべての項目をユーザー名と関連付けるメソッドが既に用意されているため、これは実際には非常に簡単です。 ユーザーが登録またはログインを完了したときに、このメソッドを呼び出す必要があります。

メンバーシップと承認を設定したときに追加した**Accountcontroller**クラスを開きます。 MvcMusicStore を参照する using ステートメントを追加し、次の MigrateShoppingCart メソッドを追加します。

[!code-csharp[Main](mvc-music-store-part-9/samples/sample1.cs)]

次に、次に示すように、ユーザーが検証された後に MigrateShoppingCart を呼び出すように、ログオン post アクションを変更します。

[!code-csharp[Main](mvc-music-store-part-9/samples/sample2.cs)]

ユーザーアカウントが正常に作成された直後に、Register post アクションに対して同じ変更を行います。

[!code-csharp[Main](mvc-music-store-part-9/samples/sample3.cs)]

これで完了です。登録またはログインが成功すると、匿名ショッピングカートが自動的にユーザーアカウントに転送されるようになりました。

## <a name="creating-the-checkoutcontroller"></a>CheckoutController の作成

Controllers フォルダーを右クリックし、空のコントローラーテンプレートを使用して、CheckoutController という名前のプロジェクトに新しいコントローラーを追加します。

![](mvc-music-store-part-9/_static/image5.png)

まず、ユーザーにチェックアウトの前に登録するように要求するために、コントローラークラス宣言の上に承認属性を追加します。

[!code-csharp[Main](mvc-music-store-part-9/samples/sample4.cs)]

*注: これは、StoreManagerController に対して以前に行った変更に似ていますが、その場合、承認属性では、ユーザーが管理者ロールに存在する必要がありました。チェックアウトコントローラーでは、ユーザーはログインする必要がありますが、管理者である必要はありません。*

わかりやすくするために、このチュートリアルでは支払い情報については扱いません。 代わりに、ユーザーがプロモーションコードを使用してチェックアウトできるようにしています。 このキャンペーンコードは、プロモーションコードという名前の定数を使用して保存されます。

StoreController のように、storeDB という名前の MusicStoreEntities クラスのインスタンスを保持するフィールドを宣言します。 MusicStoreEntities クラスを使用するには、MvcMusicStore 名前空間の using ステートメントを追加する必要があります。 Checkout コントローラーの上部が下に表示されます。

[!code-csharp[Main](mvc-music-store-part-9/samples/sample5.cs)]

CheckoutController には、次のコントローラーアクションがあります。

**AddressAndPayment (GET メソッド)** は、ユーザーが情報を入力するためのフォームを表示します。

**AddressAndPayment (POST メソッド)** は入力を検証し、注文を処理します。

ユーザーがチェックアウトプロセスを正常に完了すると、**完了**したことが表示されます。 このビューには、確認としてユーザーの注文番号が含まれます。

まず、(コントローラーを作成したときに生成された) インデックスコントローラーアクションの名前を AddressAndPayment に変更してみましょう。 このコントローラーアクションでは、チェックアウトフォームのみが表示されるため、モデル情報は必要ありません。

[!code-csharp[Main](mvc-music-store-part-9/samples/sample6.cs)]

AddressAndPayment POST メソッドは、StoreManagerController で使用したのと同じパターンに従います。フォームの送信を受け入れて注文を完了しようとし、失敗した場合はフォームを再表示します。

フォーム入力が注文の検証要件を満たしていることを検証した後、プロモーションコード form 値を直接確認します。 すべてが正しいことを前提として、更新された情報を注文と共に保存し、注文プロセスを完了するように ShoppingCart オブジェクトに指示して、完全なアクションにリダイレクトします。

[!code-csharp[Main](mvc-music-store-part-9/samples/sample7.cs)]

チェックアウトプロセスが正常に完了すると、ユーザーはコントローラーの完了アクションにリダイレクトされます。 このアクションでは、注文番号を確認のために表示する前に、その注文が実際にログインしているユーザーに属していることを検証するための簡単なチェックを実行します。

[!code-csharp[Main](mvc-music-store-part-9/samples/sample8.cs)]

*注: プロジェクトを開始したときに、エラービューが/ビュー/共有フォルダーに自動的に作成されました。*

完全な CheckoutController コードは次のとおりです。

[!code-csharp[Main](mvc-music-store-part-9/samples/sample9.cs)]

## <a name="adding-the-addressandpayment-view"></a>AddressAndPayment ビューの追加

ここで、AddressAndPayment ビューを作成してみましょう。 AddressAndPayment controller アクションの1つを右クリックし、次に示すように、注文として厳密に型指定された AddressAndPayment という名前のビューを追加します。

![](mvc-music-store-part-9/_static/image6.png)

このビューでは、StoreManagerEdit ビューの構築時に見た2つの手法を使用します。

- Html EditorForModel () を使用して、注文モデルのフォームフィールドを表示します。
- 検証属性を持つ Order クラスを使用して検証規則を活用します。

まず、Html EditorForModel () を使用するようにフォームコードを更新し、次にプロモーションコード用に追加のテキストボックスを作成します。 AddressAndPayment ビューの完全なコードを次に示します。

[!code-cshtml[Main](mvc-music-store-part-9/samples/sample10.cshtml)]

## <a name="defining-validation-rules-for-the-order"></a>注文の検証規則の定義

ビューが設定されたので、前にアルバムモデルに対して行ったように、注文モデルの検証規則を設定します。 [モデル] フォルダーを右クリックし、Order という名前のクラスを追加します。 以前にアルバムで使用していた検証属性に加えて、正規表現を使用してユーザーの電子メールアドレスを検証します。

[!code-csharp[Main](mvc-music-store-part-9/samples/sample11.cs)]

不明または無効な情報が含まれているフォームを送信しようとすると、クライアント側の検証を使用したエラーメッセージが表示されるようになりました。

![](mvc-music-store-part-9/_static/image7.png)

それでは、チェックアウトプロセスでは、ほとんどの作業が完了しました。いくつかのことが終わり、終了します。 2つの単純なビューを追加する必要があり、ログインプロセス中にカート情報のハンドオフを処理する必要があります。

## <a name="adding-the-checkout-complete-view"></a>チェックアウトの完了ビューの追加

[チェックアウトの完了] ビューは、注文 ID を表示するだけで済むため、非常に単純です。 Complete controller アクションを右クリックし、「Complete」という名前のビューを追加します。これは int として厳密に型指定されています。

![](mvc-music-store-part-9/_static/image8.png)

次に示すように、ビューコードを更新して注文 ID を表示します。

[!code-cshtml[Main](mvc-music-store-part-9/samples/sample12.cshtml)]

## <a name="updating-the-error-view"></a>エラービューの更新

既定のテンプレートには、サイト内の他の場所で再利用できるように、[共有ビュー] フォルダーに [エラー] ビューが含まれています。 このエラー表示には非常に単純なエラーが含まれており、サイトレイアウトは使用しないため、更新します。

これは一般的なエラーページであるため、コンテンツは非常に単純です。 ユーザーが操作をやり直す必要がある場合は、履歴内の前のページに移動するためのメッセージとリンクを含めます。

[!code-cshtml[Main](mvc-music-store-part-9/samples/sample13.cshtml)]

> [!div class="step-by-step"]
> [前へ](mvc-music-store-part-8.md)
> [次へ](mvc-music-store-part-10.md)
