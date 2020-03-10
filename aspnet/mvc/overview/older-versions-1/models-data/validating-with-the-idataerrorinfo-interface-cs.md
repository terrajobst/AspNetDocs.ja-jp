---
uid: mvc/overview/older-versions-1/models-data/validating-with-the-idataerrorinfo-interface-cs
title: IDataErrorInfo インターフェイス (C#) を使用して検証するMicrosoft Docs
author: StephenWalther
description: Stephen Walther は、モデルクラスに IDataErrorInfo インターフェイスを実装することによって、カスタム検証エラーメッセージを表示する方法を示しています。
ms.author: riande
ms.date: 03/02/2009
ms.assetid: 4733b9f1-9999-48fb-8b73-6038fbcc5ecb
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validating-with-the-idataerrorinfo-interface-cs
msc.type: authoredcontent
ms.openlocfilehash: 938b180da02b1963acffd021d18621d75d1d0447
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78436348"
---
# <a name="validating-with-the-idataerrorinfo-interface-c"></a>IDataErrorInfo インターフェイスの検証 (C#)

[Stephen Walther](https://github.com/StephenWalther)

> Stephen Walther は、モデルクラスに IDataErrorInfo インターフェイスを実装することによって、カスタム検証エラーメッセージを表示する方法を示しています。

このチュートリアルの目的は、ASP.NET MVC アプリケーションで検証を実行する方法の1つについて説明することです。 必要なフォームフィールドの値を指定せずに、他のユーザーが HTML フォームを送信できないようにする方法について説明します。 このチュートリアルでは、IErrorDataInfo インターフェイスを使用して検証を実行する方法について説明します。

## <a name="assumptions"></a>前提条件

このチュートリアルでは、MoviesDB データベースとムービーデータベーステーブルを使用します。 このテーブルには、次の列があります。

<a id="0.5_table01"></a>

| **列名** | **[データ型]** | **[NULL を許容]** |
| --- | --- | --- |
| Id | int | False |
| タイトル | Nvarchar (100) | False |
| ディレクター | Nvarchar (100) | False |
| DateReleased | DateTime | False |

このチュートリアルでは、Microsoft Entity Framework を使用して、データベースモデルクラスを生成します。 Entity Framework によって生成されたムービークラスは、図1に表示されます。

[Movie エンティティの ![](validating-with-the-idataerrorinfo-interface-cs/_static/image1.jpg)](validating-with-the-idataerrorinfo-interface-cs/_static/image1.png)

**図 01**: Movie エンティティ ([クリックすると、フルサイズの画像が表示](validating-with-the-idataerrorinfo-interface-cs/_static/image2.png)されます)

> [!NOTE] 
> 
> Entity Framework を使用してデータベースモデルクラスを生成する方法の詳細については、Entity Framework を使用したモデルクラスの作成に関するチュートリアルを参照してください。

## <a name="the-controller-class"></a>コントローラークラス

Home コントローラーを使用して映画を一覧表示し、新しいムービーを作成します。 このクラスのコードは、リスト1に含まれています。

**リスト 1-Controllers\ homecontroller.cs**

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample1.cs)]

リスト1の Home controller クラスには、2つの Create () アクションが含まれています。 最初のアクションでは、新しいムービーを作成するための HTML フォームが表示されます。 2番目の Create () アクションでは、データベースへの新しいムービーの実際の挿入を実行します。 2番目の Create () アクションは、最初の Create () アクションによって表示されるフォームがサーバーに送信されるときに呼び出されます。

2番目の Create () アクションには、次のコード行が含まれていることに注意してください。

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample2.cs)]

検証エラーが発生した場合、IsValid プロパティは false を返します。 その場合、ムービーを作成するための HTML フォームを含む [作成] ビューが再表示されます。

## <a name="creating-a-partial-class"></a>部分クラスの作成

Movie クラスは、Entity Framework によって生成されます。 ソリューションエクスプローラーウィンドウで MoviesDBModel ファイルを展開し、コードエディターで MoviesDBModel.Designer.cs ファイルを開くと、Movie クラスのコードが表示されます (図2を参照)。

[Movie エンティティのコードの ![](validating-with-the-idataerrorinfo-interface-cs/_static/image2.jpg)](validating-with-the-idataerrorinfo-interface-cs/_static/image3.png)

**図 02**: ムービーエンティティのコード ([クリックしてフルサイズの画像を表示](validating-with-the-idataerrorinfo-interface-cs/_static/image4.png))

Movie クラスは、部分クラスです。 これは、同じ名前を持つ別の部分クラスを追加して、Movie クラスの機能を拡張できることを意味します。 ここでは、新しい部分クラスに検証ロジックを追加します。

リスト2のクラスを [モデル] フォルダーに追加します。

**リスト 2-モデル (& c)**

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample3.cs)]

リスト2のクラスには、*部分*修飾子が含まれていることに注意してください。 このクラスに追加したメソッドまたはプロパティは、Entity Framework によって生成される Movie クラスの一部になります。

## <a name="adding-onchanging-and-onchanged-partial-methods"></a>OnChanging および OnChanged Partial メソッドの追加

Entity Framework がエンティティクラスを生成すると、Entity Framework は部分メソッドをクラスに自動的に追加します。 Entity Framework によって、クラスの各プロパティに対応する OnChanging メソッドと OnChanged 部分メソッドが生成されます。

Movie クラスの場合、Entity Framework は次のメソッドを作成します。

- OnIdChanging
- OnIdChanged
- OnTitleChanging
- OnTitleChanged
- OnDirectorChanging
- OnDirectorChanged
- OnDateReleasedChanging
- OnDateReleasedChanged

OnChanging メソッドは、対応するプロパティが変更される直前に呼び出されます。 OnChanged メソッドは、プロパティが変更された直後に呼び出されます。

これらの部分メソッドを利用して、ムービークラスに検証ロジックを追加できます。 リスト3の [ムービーの更新] クラスでは、Title プロパティと Director プロパティに空でない値が割り当てられていることが確認されます。

> [!NOTE] 
> 
> 部分メソッドは、実装する必要がないクラスで定義されたメソッドです。 部分メソッドを実装しない場合、コンパイラはメソッドのシグネチャとメソッドのすべての呼び出しを削除するため、部分メソッドに関連付けられた実行時のコストが発生しません。 Visual Studio Code エディターで、部分メソッドを追加するには、キーワード*partial*を入力し、その後にスペースを入力して、実装するパーシャルの一覧を表示します。

**リスト 3-モデル (& c)**

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample4.cs)]

たとえば、Title プロパティに空の文字列を割り当てようとすると、エラーメッセージが \_のエラーという名前のディクショナリに割り当てられます。

この時点で、Title プロパティに空の文字列を割り当てても、エラーがプライベート \_のエラーフィールドに追加された場合は、何も起こりません。 これらの検証エラーを ASP.NET MVC フレームワークに公開するには、IDataErrorInfo インターフェイスを実装する必要があります。

## <a name="implementing-the-idataerrorinfo-interface"></a>IDataErrorInfo インターフェイスの実装

IDataErrorInfo インターフェイスは、最初のバージョン以降、.NET framework に含まれています。 このインターフェイスは、非常に単純なインターフェイスです。

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample5.cs)]

クラスが IDataErrorInfo インターフェイスを実装している場合、ASP.NET MVC フレームワークは、クラスのインスタンスを作成するときにこのインターフェイスを使用します。 たとえば、Home controller Create () アクションは、Movie クラスのインスタンスを受け取ります。

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample6.cs)]

ASP.NET MVC フレームワークは、モデルバインダー (DefaultModelBinder) を使用して Create () アクションに渡されるムービーのインスタンスを作成します。 モデルバインダーは、ムービーオブジェクトのインスタンスに HTML フォームフィールドをバインドすることによって、ムービーオブジェクトのインスタンスを作成します。

DefaultModelBinder は、クラスが IDataErrorInfo インターフェイスを実装しているかどうかを検出します。 クラスがこのインターフェイスを実装する場合、モデルバインダーは IDataErrorInfo を呼び出します。このインデクサーはクラスの各プロパティに対して呼び出されます。 インデクサーからエラーメッセージが返された場合、モデルバインダーは、このエラーメッセージをモデル状態に自動的に追加します。

DefaultModelBinder は、IDataErrorInfo プロパティも確認します。 このプロパティは、クラスに関連付けられているプロパティ以外の検証エラーを表すことを目的としています。 たとえば、Movie クラスの複数のプロパティの値に依存する検証規則を適用することができます。 その場合は、エラープロパティから検証エラーを返します。

リスト4の更新されたムービークラスは、IDataErrorInfo インターフェイスを実装しています。

**リスト 4-モデル (IDataErrorInfo を実装)**

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample7.cs)]

リスト4では、インデクサープロパティは、インデクサーに渡されたプロパティ名に対応するキーが含まれているかどうかを確認するために、\_errors コレクションを確認します。 プロパティに検証エラーが関連付けられていない場合は、空の文字列が返されます。

変更した Movie クラスを使用するために、Home コントローラーを変更する必要はありません。 図3に表示されるページは、タイトルまたはディレクターフォームフィールドに値が入力されていない場合に何が起こるかを示しています。

[アクションメソッドを自動的に作成 ![](validating-with-the-idataerrorinfo-interface-cs/_static/image3.jpg)](validating-with-the-idataerrorinfo-interface-cs/_static/image5.png)

**図 03**: 欠損値のあるフォーム ([クリックすると、フルサイズの画像が表示](validating-with-the-idataerrorinfo-interface-cs/_static/image6.png)されます)

DateReleased 値が自動的に検証されることに注意してください。 DateReleased プロパティは NULL 値を受け付けないため、DefaultModelBinder は、値がない場合にこのプロパティの検証エラーを自動的に生成します。 DateReleased プロパティのエラーメッセージを変更する場合は、カスタムモデルバインダーを作成する必要があります。

## <a name="summary"></a>まとめ

このチュートリアルでは、IDataErrorInfo インターフェイスを使用して検証エラーメッセージを生成する方法について学習しました。 まず、Entity Framework によって生成される部分的なムービークラスの機能を拡張する部分的なムービークラスを作成しました。 次に、Movie class OnTitleChanging () および OnDirectorChanging () 部分メソッドに検証ロジックを追加しました。 最後に、これらの検証メッセージを ASP.NET MVC フレームワークに公開するために、IDataErrorInfo インターフェイスを実装しています。

> [!div class="step-by-step"]
> [前へ](performing-simple-validation-cs.md)
> [次へ](validating-with-a-service-layer-cs.md)
