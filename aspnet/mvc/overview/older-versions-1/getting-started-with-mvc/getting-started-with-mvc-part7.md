---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part7
title: モデルへの検証の追加 |Microsoft Docs
author: shanselman
description: これは、ASP.NET MVC の基本を紹介する初心者向けチュートリアルです。 データベースを読み書きする単純な web アプリケーションを作成します。
ms.author: riande
ms.date: 08/14/2010
ms.assetid: aa7b3e8e-e23d-49f1-b160-f99a7f2982bd
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part7
msc.type: authoredcontent
ms.openlocfilehash: 9403be574324c34edf93bef1e0e4fd7ba68a3a9d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78437278"
---
# <a name="adding-validation-to-the-model"></a>モデルに検証を追加する

[Scott マン Selman](https://github.com/shanselman)

> これは、ASP.NET MVC の基本を紹介する初心者向けチュートリアルです。 データベースを読み書きする単純な web アプリケーションを作成します。 他の ASP.NET MVC のチュートリアルとサンプルについては、 [ASP.NET mvc learning center](../../../index.md)を参照してください。

このセクションでは、アプリケーション内で入力の検証を有効にするために必要なサポートを実装します。 データベースの内容が常に正しいことを確認し、有効でない映画データを入力しようとすると、エンドユーザーに役立つエラーメッセージを提供します。 まず、小さな検証ロジックを Movie クラスに追加します。

モデルフォルダーを右クリックし、[クラスの追加] を選択します。 クラスムービーの名前を指定します。

先ほどムービーエンティティモデルを作成すると、IDE によって Movie クラスが作成されました。 実際、Movie クラスの一部を1つのファイルに配置し、別のファイルに含めることができます。 これを部分クラスと呼びます。 ムービークラスを別のファイルから拡張します。

ここでは、システムに検証ヒントを提供するいくつかの属性を使用して "buddy class" を指す部分的なムービークラスを作成します。 必要に応じてタイトルと価格を設定します。また、価格が特定の範囲内であることを要求します。 [モデル] フォルダーを右クリックし、[クラスの追加] を選択します。 クラスに Movie という名前を指定し、[OK] ボタンをクリックします。 部分的なムービークラスは次のようになります。

[!code-csharp[Main](getting-started-with-mvc-part7/samples/sample1.cs)]

アプリケーションを再実行し、100を超える価格で映画を入力してみてください。 フォームを送信すると、エラーが表示されます。 エラーはサーバー側でキャッチされ、フォームがポストされた後に発生します。 ASP.NET MVC の組み込み HTML ヘルパーは、エラーメッセージを表示し、textbox 要素内の値を維持するのに十分であることに注意してください。

[![Createmoの検証](getting-started-with-mvc-part7/_static/image2.png)](getting-started-with-mvc-part7/_static/image1.png)

これはうまく機能しますが、サーバーが関与する前に、クライアント側でユーザーに通知することもできます。

JavaScript でクライアント側の検証を有効にしてみましょう。

## <a name="adding-client-side-validation"></a>クライアント側の検証の追加

Movie クラスには既にいくつかの検証属性があるため、いくつかの JavaScript ファイルを作成して、クライアント側の検証を有効にするコード行を追加する必要があります。

VWD 内から、Views/Movie フォルダーにアクセスして、default.aspx を開きます。

ソリューションエクスプローラーで Scripts フォルダーを開き、次の3つのスクリプトを &lt;head&gt; タグ内にドラッグします。

- Microsoftajax.js
- MicrosoftMvcValidation.js

これらのスクリプトファイルがこの順序で表示されるようにします。

[!code-html[Main](getting-started-with-mvc-part7/samples/sample2.html)]

また、次の1行を Html. BeginForm の上に追加します。

[!code-aspx[Main](getting-started-with-mvc-part7/samples/sample3.aspx)]

IDE 内に表示されるコードを次に示します。

[![映画-Microsoft Visual Web Developer 2010 Express (10)](getting-started-with-mvc-part7/_static/image4.png)](getting-started-with-mvc-part7/_static/image3.png)

アプリケーションを実行し、/Movies/Create にもう一度アクセスして、データを入力せずに [作成] をクリックします。 エラーメッセージは、データをサーバーに送信するためにデータを送信するために、ページフラッシュなしですぐに表示されます。 これは、ASP.NET MVC が、(JavaScript を使用して) クライアントとサーバーの両方で入力を検証するようになったためです。

[![作成-Windows Internet Explorer](getting-started-with-mvc-part7/_static/image6.png)](getting-started-with-mvc-part7/_static/image5.png)

これは良いことです。 次に、データベースに列を1つ追加してみましょう。

> [!div class="step-by-step"]
> [前へ](getting-started-with-mvc-part6.md)
> [次へ](getting-started-with-mvc-part8.md)
