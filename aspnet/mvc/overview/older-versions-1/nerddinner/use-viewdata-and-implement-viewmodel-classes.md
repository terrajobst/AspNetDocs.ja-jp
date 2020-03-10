---
uid: mvc/overview/older-versions-1/nerddinner/use-viewdata-and-implement-viewmodel-classes
title: ViewData を使用して、ビューモデルクラスを実装する |Microsoft Docs
author: microsoft
description: 手順6では、豊富なフォーム編集シナリオのサポートを有効にする方法と、コントローラーからビューにデータを渡すために使用できる2つの方法について説明します。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 5755ec4c-60f1-4057-9ec0-3a5de3a20e23
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-viewdata-and-implement-viewmodel-classes
msc.type: authoredcontent
ms.openlocfilehash: ca9775417c2e25952511a73096fb76d5d4edaea2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78435532"
---
# <a name="use-viewdata-and-implement-viewmodel-classes"></a>ViewData を使用し、ViewModel クラスを実装する

[Microsoft](https://github.com/microsoft)

[[Download PDF]\(PDF をダウンロード\)](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> これは、ASP.NET MVC 1 を使用して小規模で完成した web アプリケーションを構築する方法を説明する無料の["" アプリケーションのチュートリアル](introducing-the-nerddinner-tutorial.md)の手順6です。
> 
> 手順6は、豊富なフォーム編集シナリオのサポートを有効にする方法と、コントローラーからビューにデータを渡すために使用できる2つの方法である ViewData とビューについても説明します。
> 
> ASP.NET MVC 3 を使用している場合は、MVC 3 または[Mvc ミュージックストア](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)[のチュートリアルではじめに](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)に従うことをお勧めします。

## <a name="nerddinner-step-6-viewdata-and-viewmodel"></a>ステップ 6: ViewData とビューモデルの操作

ここでは、いくつかのフォームポストシナリオについて説明し、作成、更新、削除 (CRUD) のサポートを実装する方法について説明しました。 ここでは、さらに詳しく説明します。これにより、より豊富なフォーム編集シナリオがサポートされるようになります。 ここでは、コントローラーからビューにデータを渡すために使用できる2つの方法 (ViewData とビューモデル) について説明します。

### <a name="passing-data-from-controllers-to-view-templates"></a>コントローラーからビューテンプレートにデータを渡す

MVC パターンの定義特性の1つは、アプリケーションのさまざまなコンポーネントの間で適用される、厳密な "懸念事項の分離" です。 モデル、コントローラー、およびビューには、ロールと責任が明確に定義されており、それぞれが明確に定義された方法で相互に通信します。 これにより、テストの容易性とコードの再利用が促進されます。

コントローラークラスは、クライアントに HTML 応答を返すことを決定するときに、応答を表示するために必要なすべてのデータをビューテンプレートに明示的に渡す役割を担います。 ビューテンプレートは、データの取得またはアプリケーションロジックを実行しないようにする必要があります。代わりに、コントローラーによって渡されたモデル/データから駆動されるレンダリングコードだけを表示するように制限する必要があります。

ここで、DinnersController クラスによってビューテンプレートに渡されるモデルデータは単純で、簡単です。 Index () の場合はディナーオブジェクトのリスト、Details ()、Edit ()、Create ()、Delete () の場合は1つのディナーオブジェクトです。 アプリケーションに UI 機能を追加すると、多くの場合、ビューテンプレート内に HTML 応答を表示するために、このデータだけではなく、さらに多くのデータを渡す必要があります。 たとえば、Edit および Create ビュー内の "Country" フィールドを、HTML テキストボックスから dropdownlist に変更することができます。 ビューテンプレートで国名のドロップダウンリストをハードコーディングするのではなく、動的に設定する、サポートされている国の一覧から生成することをお勧めします。 ディナーオブジェクト*と*、サポートされている国の一覧をコントローラーからビューテンプレートに渡す方法が必要になります。

これを実現する2つの方法を見てみましょう。

### <a name="using-the-viewdata-dictionary"></a>ViewData Dictionary の使用

コントローラーの基本クラスは、コントローラーからビューに追加のデータ項目を渡すために使用できる "ViewData" ディクショナリプロパティを公開します。

たとえば、編集ビュー内の "Country" テキストボックスを HTML テキストボックスから dropdownlist に変更するというシナリオをサポートするために、Edit () アクションメソッドを更新して、m として使用できる SelectList オブジェクトを (ディナーオブジェクトに加えて) 渡すことができます。国の odel の dropdownlist。

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample1.cs)]

上記の SelectList のコンストラクターは、現在選択されている値だけでなく、ドロップダウンリストに入力する郡の一覧を受け入れています。

次に、前に使用した .Html () ヘルパーメソッドではなく、.Html () ヘルパーメソッドを使用するように、編集 .aspx ビューテンプレートを更新できます。

[!code-aspx[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample2.aspx)]

上記の .Html () ヘルパーメソッドは、2つのパラメーターを受け取ります。 1つ目は、出力する HTML フォーム要素の名前です。 2つ目は、ViewData 辞書を介して渡された "SelectList" モデルです。 C# "As" キーワードを使用して、ディクショナリ内の型を selectlist としてキャストしています。

ここで、アプリケーションを実行し、ブラウザー内で */Dinners/Edit/1* URL にアクセスすると、エディット UI が更新され、テキストボックスではなく country of country が表示されていることがわかります。

![](use-viewdata-and-implement-viewmodel-classes/_static/image1.png)

また、編集ビューテンプレートは、HTTP ポスト編集メソッド (エラーが発生した場合) からもレンダリングされるので、エラーシナリオでビューテンプレートがレンダリングされたときに、このメソッドを更新して、SelectList を ViewData に追加するようにします。

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample3.cs)]

これで、Dinがコントローラーを編集するシナリオで DropDownList がサポートされるようになりました。

### <a name="using-a-viewmodel-pattern"></a>ビューモデルパターンの使用

ViewData dictionary のアプローチには、非常に高速で実装が簡単であるという利点があります。 ただし、文字列ベースの辞書を使用しない開発者もいます。これは、入力ミスによってコンパイル時に検出されないエラーが発生する可能性があるためです。 また、型指定されていない ViewData 辞書では、ビューテンプレートでのようC#に、厳密に型指定された言語を使用する場合に、"as" 演算子またはキャストを使用する必要があります。

使用できる別の方法として、しばしば "モデル化" パターンと呼ばれるものがあります。 このパターンを使用すると、特定のビューシナリオ用に最適化された、厳密に型指定されたクラスを作成し、ビューテンプレートに必要な動的な値/コンテンツのプロパティを公開します。 次に、コントローラークラスを設定して、ビューに最適化されたこれらのクラスをビューテンプレートに渡して使用できるようにします。 これにより、ビューテンプレート内でタイプセーフ、コンパイル時チェック、およびエディター intellisense が有効になります。

たとえば、ディナーフォーム編集シナリオを有効にするには、次のように、2つの厳密に型指定されたプロパティを公開する "DinnerFormViewModel" クラスを作成します。ディナーオブジェクトと、country に設定するために必要な SelectList モデルです。

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample4.cs)]

次に、Edit () アクションメソッドを更新して、リポジトリから取得したディナーオブジェクトを使用して Dinを作成し、ビューテンプレートに渡すことができます。

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample5.cs)]

次に、ビューテンプレートを更新して、次のように .aspx ページの上部にある "inherits" 属性を変更することによって、"ディナー" オブジェクトではなく "Din" を必要とするようにします。

[!code-cshtml[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample6.cshtml)]

この操作を実行すると、ビューテンプレート内の "Model" プロパティの intellisense が更新され、それに渡される Dinare Formmodel 型のオブジェクトモデルが反映されます。

![](use-viewdata-and-implement-viewmodel-classes/_static/image2.png)

![](use-viewdata-and-implement-viewmodel-classes/_static/image3.png)

その後で、ビューコードを更新して、作業を開始することができます。 ここでは、作成している入力要素の名前を変更していないことに注意してください (form 要素には "Title"、"Country" という名前が付けられます)。ただし、HTML ヘルパーメソッドを更新して、Dinare Formformクラスを使用して値を取得します。

[!code-aspx[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample7.aspx)]

また、レンダリングエラーが発生したときに Dinを使用するように、Edit post メソッドを更新します。

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample8.cs)]

また、Create () アクションメソッドを更新して、まったく同じ*Dinのフォームビューモデル*クラスを再利用し、その中でも Country の DropDownList を有効にすることができます。 HTTP GET 実装は次のようになります。

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample9.cs)]

次に、HTTP ポストの Create メソッドの実装を示します。

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample10.cs)]

これで、編集画面と作成画面の両方で、国を選択するためのドロップダウンリストがサポートされるようになりました。

### <a name="custom-shaped-viewmodel-classes"></a>カスタムの型のビューモデルクラス

上記のシナリオでは、Dinの Formformmodel クラスが、サポートされている SelectList モデルプロパティと共に、ディナーモデルオブジェクトをプロパティとして直接公開しています。 この方法は、ビューテンプレート内で作成する HTML UI がドメインモデルオブジェクトに対して比較的厳密に対応するシナリオに適しています。

そうではないシナリオでは、使用できるオプションの1つとして、オブジェクトモデルがビューによって消費されるように最適化され、基になるドメインモデルオブジェクトと完全に異なる場合がある、カスタムの形式のビューモデルクラスを作成する方法があります。 たとえば、複数のモデルオブジェクトから収集されたさまざまなプロパティ名や集計プロパティを公開する可能性があります。

カスタム整形型のビューモデルクラスを使用すると、コントローラーからビューにデータを渡したり、コントローラーのアクションメソッドにポストバックされるフォームデータを処理したりすることができます。 この後のシナリオでは、アクションメソッドを使用して、フォームポストされたデータを含むビューモデルオブジェクトを更新してから、ビューモデルインスタンスを使用して実際のドメインモデルオブジェクトをマップまたは取得することができます。

カスタムの型のビューモデルクラスでは、柔軟性を高めることができます。また、ビューテンプレート内のレンダリングコードや、アクションメソッド内のフォームポストコードを見つけるたびに調査して、複雑になることがあります。 これは多くの場合、ドメインモデルが生成する UI に明確に対応していないこと、および中間のカスタムのビューモデルクラスが役立つことを示しています。

### <a name="next-step"></a>次の手順

次に、パーシャルとマスターページを使用して、アプリケーション全体で UI を再利用し、共有する方法を見てみましょう。

> [!div class="step-by-step"]
> [前へ](provide-crud-create-read-update-delete-data-form-entry-support.md)
> [次へ](re-use-ui-using-master-pages-and-partials.md)
