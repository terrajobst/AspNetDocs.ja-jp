---
uid: mvc/overview/older-versions-1/models-data/validation-with-the-data-annotation-validators-vb
title: データ注釈検証コントロールを使用した検証 (VB) |Microsoft Docs
author: microsoft
description: データ注釈モデルバインダーを利用して、ASP.NET MVC アプリケーション内で検証を実行します。 さまざまな種類の検証コントロールの使用方法について説明します。
ms.author: riande
ms.date: 05/29/2009
ms.assetid: 0d23ff2b-f2ec-434a-be3b-1180beeccba3
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validation-with-the-data-annotation-validators-vb
msc.type: authoredcontent
ms.openlocfilehash: 00150575baabc659f7dd0c07349cde52105f6c8b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78435940"
---
# <a name="validation-with-the-data-annotation-validators-vb"></a>データ検証注釈コントロールの検証 (VB)

[Microsoft](https://github.com/microsoft)

> データ注釈モデルバインダーを利用して、ASP.NET MVC アプリケーション内で検証を実行します。 さまざまな種類の検証コントロール属性を使用して、Microsoft Entity Framework でそれらを操作する方法について説明します。

このチュートリアルでは、データ注釈検証コントロールを使用して、ASP.NET MVC アプリケーションで検証を実行する方法について説明します。 データ注釈検証コントロールを使用する利点は、必須または StringLength 属性などの1つ以上の属性をクラスプロパティに追加するだけで検証を実行できることです。

データ注釈検証コントロールを使用するには、データ注釈モデルバインダーをダウンロードする必要があります。 データ注釈モデルバインダーのサンプルは、CodePlex web サイトからダウンロードできます。これを行うには、[ここ](http://aspnet.codeplex.com/Release/ProjectReleases.aspx?ReleaseId=24471)をクリックします。

データ注釈モデルバインダーは Microsoft ASP.NET MVC フレームワークの正式な部分ではないことを理解しておくことが重要です。 データ注釈モデルバインダーは Microsoft ASP.NET MVC チームによって作成されましたが、Microsoft では、このチュートリアルで説明されているデータ注釈モデルバインダーの公式製品サポートを提供していません。

## <a name="using-the-data-annotation-model-binder"></a>データ注釈モデルバインダーの使用

ASP.NET MVC アプリケーションでデータ注釈モデルバインダーを使用するには、最初に、System.componentmodel アセンブリおよびアセンブリへの参照を追加する必要がありますので、この方法は必要ありません。 メニューオプションプロジェクトの **[参照の追加]** を選択します。 次に、 **[参照]** タブをクリックし、データ注釈モデルバインダーサンプルをダウンロード (および解凍) した場所を参照します (**図 1**を参照)。

[![](validation-with-the-data-annotation-validators-vb/_static/image2.png)](validation-with-the-data-annotation-validators-vb/_static/image1.png)

**図 1**: データ注釈モデルバインダーへの参照の追加 ([クリックすると、フルサイズの画像が表示](validation-with-the-data-annotation-validators-vb/_static/image3.png)されます)

System.componentmodel アセンブリとアセンブリの両方を選択し、**OK** ボタンをクリックします。 をクリックします。

.NET Framework Service Pack 1 に含まれている System.componentmodel アセンブリをデータ注釈モデルバインダーと共に使用することはできません。 データ注釈モデルバインダーサンプルのダウンロードに含まれているバージョンの System.componentmodel アセンブリを使用する必要があります。

最後に、DataAnnotations モデルバインダーを global.asax ファイルに登録する必要があります。 Application\_Start () イベントハンドラーに次のコード行を追加して、アプリケーション\_Start () メソッドが次のようになるようにします。

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample1.vb)]

このコード行では、ASP.NET MVC アプリケーション全体の既定のモデルバインダーとして Data注釈を登録します。

## <a name="using-the-data-annotation-validator-attributes"></a>データ注釈検証コントロール属性の使用

データ注釈モデルバインダーを使用する場合は、検証を実行するために検証属性を使用します。 System.componentmodel 名前空間には、次のバリデーター属性が含まれています。

- 範囲–プロパティの値が、指定された値の範囲に収まるかどうかを検証できます。
- RegularExpression –プロパティの値が指定した正規表現パターンと一致するかどうかを検証できます。
- 必須–プロパティを必要に応じてマークできます。
- StringLength –文字列プロパティの最大長を指定できます。
- 検証: すべての検証コントロール属性の基本クラス。

> [!NOTE] 
> 
> 標準の検証コントロールで検証のニーズが満たされない場合、基本検証属性から新しい検証属性を継承することによって、カスタム検証属性を作成するオプションが常にあります。

**リスト 1**の Product クラスは、これらの検証属性の使用方法を示しています。 Name、Description、および UnitPrice プロパティは必須としてマークされています。 Name プロパティの文字列の長さは10文字未満である必要があります。 最後に、UnitPrice プロパティは、通貨金額を表す正規表現パターンと一致する必要があります。

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample2.vb)]

**リスト 1**: modelproductproduct. vb

Product クラスは、1つの追加の属性 (DisplayName 属性) の使用方法を示しています。 DisplayName 属性を使用すると、プロパティがエラーメッセージに表示されたときにプロパティの名前を変更できます。 "UnitPrice フィールドが必要です" というエラーメッセージが表示されるのではなく、"価格フィールドが必要です" というエラーメッセージを表示できます。

> [!NOTE] 
> 
> バリデーターによって表示されるエラーメッセージを完全にカスタマイズする場合は、次のように、カスタムエラーメッセージを検証コントロールの ErrorMessage プロパティに割り当てることができ `<Required(ErrorMessage:="This field needs a value!")>`

リスト**2**の [作成] () コントローラーアクションを使用して、**リスト 1**の Product クラスを使用できます。 このコントローラーアクションは、モデルの状態にエラーが含まれている場合に、Create ビューを再表示します。

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample3.vb)]

**リスト 2**: コントローラーと vb

最後に、**リスト 3**のビューを作成するには、作成 () アクションを右クリックし、**ビューの追加** メニューオプションを選択します。 Product クラスをモデルクラスとして使用して、厳密に型指定されたビューを作成します。 ビューコンテンツ ドロップダウンリストから **作成** を選択します (**図 2**を参照)。

[![](validation-with-the-data-annotation-validators-vb/_static/image5.png)](validation-with-the-data-annotation-validators-vb/_static/image4.png)

**図 2**: Create ビューの追加

[!code-aspx[Main](validation-with-the-data-annotation-validators-vb/samples/sample4.aspx)]

**リスト 3**: Views\Product\Create.aspx

> [!NOTE] 
> 
> **[ビューの追加]** メニューオプションで生成された作成フォームから Id フィールドを削除します。 Id フィールドは Id 列に対応しているため、このフィールドに値を入力することをユーザーに許可しないようにします。

製品を作成するためのフォームを送信し、必須フィールドに値を入力しない場合、**図 3**の検証エラーメッセージが表示されます。

[![](validation-with-the-data-annotation-validators-vb/_static/image7.png)](validation-with-the-data-annotation-validators-vb/_static/image6.png)

**図 3**: 必要なフィールドがない

無効な通貨金額を入力すると、**図 4**のエラーメッセージが表示されます。

[![](validation-with-the-data-annotation-validators-vb/_static/image9.png)](validation-with-the-data-annotation-validators-vb/_static/image8.png)

**図 4**: 通貨金額が無効である

## <a name="using-data-annotation-validators-with-the-entity-framework"></a>Entity Framework と共にデータ注釈検証コントロールを使用する

Microsoft Entity Framework を使用してデータモデルクラスを生成する場合は、クラスにバリデーター属性を直接適用することはできません。 Entity Framework Designer によってモデルクラスが生成されるため、モデルクラスに加えた変更は、デザイナーで次に変更を行ったときに上書きされます。

Entity Framework によって生成されたクラスで検証コントロールを使用する場合は、メタデータクラスを作成する必要があります。 検証コントロールは、実際のクラスに適用するのではなく、メタデータクラスに適用します。

たとえば、Entity Framework を使用して Movie クラスを作成したとします (**図 5**を参照)。 さらに、ムービータイトルとディレクタープロパティに必要なプロパティを設定するとします。 その場合は、**リスト 4**で部分クラスとメタデータクラスを作成できます。

[![](validation-with-the-data-annotation-validators-vb/_static/image11.png)](validation-with-the-data-annotation-validators-vb/_static/image10.png)

**図 5**: Entity Framework によって生成されたムービークラス

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample5.vb)]

**リスト 4**: modelmo? vb

**リスト 4**のファイルには、Movie と MovieMetaData という名前の2つのクラスが含まれています。 Movie クラスは、部分クラスです。 これは、DataModel ファイルに格納されている Entity Framework によって生成される部分クラスに対応します。

現在、.NET framework では部分的なプロパティはサポートされていません。 したがって、DataModel ファイルで定義されている Movie クラスのプロパティにバリデーター属性を適用する方法はありません。これには、**リスト 4**のファイルで定義されている movie クラスのプロパティにバリデーター属性を適用します。

Movie 部分クラスは、MovieMetaData クラスをポイントする MetadataType 属性で修飾されていることに注意してください。 MovieMetaData クラスには、Movie クラスのプロパティのプロキシプロパティが含まれています。

バリデーターの属性は、MovieMetaData クラスのプロパティに適用されます。 Title、Director、および DateReleased の各プロパティはすべて必須プロパティとしてマークされます。 Director プロパティには、5文字未満の文字列を割り当てる必要があります。 最後に、DisplayName 属性が DateReleased プロパティに適用され、"リリース日フィールドが必要です。" のようなエラーメッセージが表示されます。 "DateReleased" フィールドは必須です。

> [!NOTE] 
> 
> MovieMetaData クラスのプロキシプロパティは、Movie クラスの対応するプロパティと同じ型を表す必要がないことに注意してください。 たとえば、"Director" プロパティは、Movie クラスの文字列プロパティと、MovieMetaData クラスのオブジェクトプロパティです。

**図 6**のページは、ムービープロパティに無効な値を入力したときに返されるエラーメッセージを示しています。

[![](validation-with-the-data-annotation-validators-vb/_static/image13.png)](validation-with-the-data-annotation-validators-vb/_static/image12.png)

**図 6**: Entity Framework での検証コントロールの使用 ([クリックしてフルサイズのイメージを表示する](validation-with-the-data-annotation-validators-vb/_static/image14.png))

## <a name="summary"></a>まとめ

このチュートリアルでは、データ注釈モデルバインダーを利用して、ASP.NET MVC アプリケーション内で検証を実行する方法について学習しました。 必須の属性や StringLength 属性など、さまざまな種類の検証コントロール属性の使用方法について学習しました。 また、Microsoft Entity Framework の使用時にこれらの属性を使用する方法についても学習しました。

> [!div class="step-by-step"]
> [[戻る]](validating-with-a-service-layer-vb.md)
