---
uid: mvc/overview/older-versions-1/controllers-and-routing/adding-dynamic-content-to-a-cached-page-cs
title: キャッシュされたページに動的コンテンツC#を追加する () |Microsoft Docs
author: microsoft
description: 動的コンテンツとキャッシュされたコンテンツを同じページに混在させる方法について説明します。 キャッシュ後の置換では、バナー広告などの動的なコンテンツを表示できます...
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 2ddd4407-d143-4a94-877c-21771bfb97a6
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/adding-dynamic-content-to-a-cached-page-cs
msc.type: authoredcontent
ms.openlocfilehash: be43712d3dd5235117558e991d9dd71aa30ec470
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486940"
---
# <a name="adding-dynamic-content-to-a-cached-page-c"></a>キャッシュされたページに動的コンテンツを追加する (C#)

[Microsoft](https://github.com/microsoft)

> 動的コンテンツとキャッシュされたコンテンツを同じページに混在させる方法について説明します。 キャッシュ後の置換を使用すると、出力がキャッシュされているページ内に、バナー広告やニュース項目などの動的コンテンツを表示できます。

出力キャッシュを利用することで、ASP.NET MVC アプリケーションのパフォーマンスを大幅に向上させることができます。 ページを毎回再生成するのではなく、ページが要求されるたびに、ページを生成し、複数のユーザーのメモリにキャッシュすることができます。

しかし、問題があります。 動的なコンテンツをページに表示する必要がある場合はどうすればよいでしょうか。 たとえば、ページにバナー広告を表示する場合を考えてみます。 すべてのユーザーに同じ提供情報が表示されるように、バナー広告がキャッシュされないようにします。 そのようなことはできません。

幸いにも、簡単な解決策があります。 *キャッシュ後の置換*と呼ばれる ASP.NET フレームワークの機能を利用できます。 キャッシュ後の置換を使用すると、メモリにキャッシュされているページの動的コンテンツを置き換えることができます。

通常、[OutputCache] 属性を使用してページのキャッシュを出力すると、ページはサーバーとクライアントの両方 (web ブラウザー) にキャッシュされます。 キャッシュ後の置換を使用する場合、ページはサーバーにのみキャッシュされます。

#### <a name="using-post-cache-substitution"></a>キャッシュ後の置換の使用

キャッシュ後の置換を使用するには、2つの手順を実行する必要があります。 まず、キャッシュされたページに表示する動的コンテンツを表す文字列を返すメソッドを定義する必要があります。 次に、Httpresponse.cache () メソッドを呼び出して、動的なコンテンツをページに挿入します。

たとえば、キャッシュされたページで異なるニュースアイテムをランダムに表示する場合を考えてみます。 リスト1のクラスは、RenderNews () という1つのメソッドを公開します。このメソッドは、3つのニュース項目のリストから1つのニュース項目をランダムに返します。

**リスト1– Models\News.cs**

[!code-csharp[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample1.cs)]

キャッシュ後の置換を利用するには、WriteSubstitution () メソッドを呼び出します。 WriteSubstitution () メソッドは、キャッシュされたページの領域を動的なコンテンツに置き換えるようにコードを設定します。 WriteSubstitution () メソッドを使用して、リスト2のビューにランダムなニュース項目を表示します。

**リスト2– Views\Home\Index.aspx**

[!code-aspx[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample2.aspx)]

RenderNews メソッドは、WriteSubstitution () メソッドに渡されます。 RenderNews メソッドが呼び出されていないことに注意してください (かっこはありません)。 代わりに、メソッドへの参照が WriteSubstitution () に渡されます。

インデックスビューがキャッシュされます。 ビューは、リスト3のコントローラーによって返されます。 Index () アクションが [OutputCache] 属性で修飾され、インデックスビューが60秒間キャッシュされることに注意してください。

**リスト3– Controllers\ homecontroller.cs**

[!code-csharp[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample3.cs)]

インデックスビューがキャッシュされている場合でも、インデックスページを要求すると、異なるランダムニュース項目が表示されます。 インデックスページを要求すると、ページに表示される時間は60秒間は変わりません (図1を参照)。 時間が変更されないという事実は、ページがキャッシュされていることを証明します。 ただし、WriteSubstitution () メソッドによって挿入されたコンテンツ (ランダムニュース項目) は、要求ごとに変化します。

**図 1: キャッシュされたページに動的なニュース項目を挿入する**

![clip_image002](adding-dynamic-content-to-a-cached-page-cs/_static/image1.jpg)

#### <a name="using-post-cache-substitution-in-helper-methods"></a>ヘルパーメソッドでのキャッシュ後の置換の使用

キャッシュ後の置換を利用する簡単な方法は、カスタムヘルパーメソッド内で WriteSubstitution () メソッドの呼び出しをカプセル化することです。 この方法は、リスト4のヘルパーメソッドによって示されています。

**リスト4– AdHelper.cs**

[!code-csharp[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample4.cs)]

リスト4には、RenderBanner () と RenderBannerInternal () という2つのメソッドを公開する静的クラスが含まれています。 RenderBanner () メソッドは、実際のヘルパーメソッドを表します。 このメソッドは、標準の ASP.NET MVC HtmlHelper クラスを拡張します。これにより、他のヘルパーメソッドと同様に、ビューで Html の RenderBanner () を呼び出すことができるようになります。

RenderBanner () メソッドは、RenderBannerInternal () メソッドを WriteSubstitution () メソッドに渡して、WriteSubstitution () メソッドを呼び出します。

RenderBannerInternal () メソッドはプライベートメソッドです。 このメソッドは、ヘルパーメソッドとして公開されません。 RenderBannerInternal () メソッドは、3つのバナー広告画像のリストから、1つのバナー広告画像をランダムに返します。

リスト5の変更されたインデックスビューは、RenderBanner () ヘルパーメソッドを使用する方法を示しています。 MvcApplication1 名前空間をインポートするために、ビューの先頭に追加の &lt;% @ Import%&gt; ディレクティブが含まれていることに注意してください。 この名前空間のインポートを怠ると、RenderBanner () メソッドが Html プロパティのメソッドとして表示されません。

**リスト5– Views\Home\Index.aspx (RenderBanner () メソッドを使用)**

[!code-aspx[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample5.aspx)]

リスト5のビューによって表示されるページを要求すると、要求ごとに異なるバナー広告が表示されます (図2を参照)。 ページはキャッシュされますが、バナー広告は RenderBanner () ヘルパーメソッドによって動的に挿入されます。

**図2–ランダムなバナー広告を表示するインデックスビュー**

![clip_image004](adding-dynamic-content-to-a-cached-page-cs/_static/image2.jpg)

#### <a name="summary"></a>まとめ

このチュートリアルでは、キャッシュされたページのコンテンツを動的に更新する方法について説明しました。 Httpresponse.cache () メソッドを使用して、キャッシュされたページに動的コンテンツを挿入できるようにする方法を学習しました。 また、HTML ヘルパーメソッド内で WriteSubstitution () メソッドの呼び出しをカプセル化する方法についても学習しました。

可能な限りキャッシュを利用する– web アプリケーションのパフォーマンスに大きな影響を与える可能性があります。 このチュートリアルで説明するように、動的なコンテンツをページに表示する必要がある場合でも、キャッシュを利用できます。

> [!div class="step-by-step"]
> [前へ](improving-performance-with-output-caching-cs.md)
> [次へ](creating-a-controller-cs.md)
