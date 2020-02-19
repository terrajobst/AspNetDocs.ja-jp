---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-validation-to-the-model
title: モデルへの検証の追加 (VB) |Microsoft Docs
author: Rick-Anderson
description: このチュートリアルでは、Microsoft Visual Web Developer 2010 Express Service Pack 1 を使用した ASP.NET MVC Web アプリケーションの構築の基本について説明します。
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 878f6c31-972d-45f4-8849-5c633b511409
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-validation-to-the-model
msc.type: authoredcontent
ms.openlocfilehash: 7f3f195bc30ed23a637b59f15e6fc8431e39e217
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457202"
---
# <a name="adding-validation-to-the-model-vb"></a>モデルに検証を追加する (VB)

[Rick Anderson](https://twitter.com/RickAndMSFT)

> このチュートリアルでは、Microsoft Visual Studio の無料バージョンである Microsoft Visual Web Developer 2010 Express Service Pack 1 を使用した ASP.NET MVC Web アプリケーションの構築の基本について説明します。 開始する前に、以下に示す前提条件がインストールされていることを確認してください。 これらのすべてをインストールするには、[ [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)] リンクをクリックします。 または、次のリンクを使用して、前提条件を個別にインストールすることもできます。
> 
> - [Visual Studio Web Developer Express SP1 の前提条件](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 ツールの更新](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(ランタイム + ツールのサポート)
> 
> Visual Web Developer 2010 ではなく Visual Studio 2010 を使用している場合は、次のリンクをクリックして必要なコンポーネントをインストールします: [Visual studio 2010 の前提条件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。
> 
> このトピックには、VB.NET ソースコードを含む Visual Web Developer プロジェクトが用意されています。 [VB.NET バージョンをダウンロード](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)します。 必要に応じC#て[ C# ](../cs/adding-validation-to-the-model.md) 、このチュートリアルのバージョンに切り替えます。

このセクションでは、`Movie` モデルに検証ロジックを追加し、ユーザーがアプリケーションを使用してムービーを作成または編集しようとするたびに検証規則が適用されるようにします。

## <a name="keeping-things-dry"></a>ドライを維持する

ASP.NET MVC の核となる設計の原則の1つは、ドライ ("DRY 原則") です。 ASP.NET MVC を使用すると、機能または動作を一度だけ指定し、アプリケーション内のすべての場所に反映させることができます。 これにより、記述する必要があるコードの量が減り、記述するコードの保守がはるかに簡単になります。

ASP.NET MVC と Entity Framework Code First によって提供される検証のサポートは、ドライの原則が動作する好例です。 (モデルクラス内の) 1 つの場所で検証規則を宣言によって指定すると、アプリケーション内のすべての場所で規則が適用されます。

ムービーアプリケーションでこの検証サポートを利用する方法を見てみましょう。

## <a name="adding-validation-rules-to-the-movie-model"></a>ムービーモデルへの検証規則の追加

まず、`Movie` クラスに検証ロジックを追加します。

*Movie*ファイルを開きます。 [`System.ComponentModel.DataAnnotations`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)名前空間を参照するファイルの先頭に `Imports` ステートメントを追加します。

[!code-vb[Main](adding-validation-to-the-model/samples/sample1.vb)]

名前空間は .NET Framework の一部です。 これには、任意のクラスまたはプロパティに宣言によって適用できる、組み込みの検証属性のセットが用意されています。

次に、組み込みの[`Required`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx)、 [`StringLength`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx)、および[`Range`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx)検証属性を利用できるように `Movie` クラスを更新します。 属性を適用する場所の例として、次のコードを使用します。

[!code-vb[Main](adding-validation-to-the-model/samples/sample2.vb)]

検証属性では、適用対象のモデル プロパティに適用する動作を指定します。 `Required` 属性は、プロパティに値が必要であることを示します。このサンプルでは、有効にするために、ムービーに `Title`、`ReleaseDate`、`Genre`、および `Price` プロパティの値が必要です。 `Range` 属性は、指定した範囲内に値を制限します。 `StringLength` 属性では、文字列プロパティの最大長を設定でき、オプションとして最小長も設定できます。

Code First により、アプリケーションがデータベースに変更を保存する前に、モデルクラスで指定した検証規則が確実に適用されます。 たとえば、次のコードでは、`SaveChanges` メソッドが呼び出されたときに例外がスローされます。これは、いくつかの必須の `Movie` プロパティ値が不足しており、価格が 0 (有効な範囲外) であるためです。

[!code-vb[Main](adding-validation-to-the-model/samples/sample3.vb)]

.NET Framework によって検証規則が自動的に適用されるため、アプリケーションの堅牢性が向上します。 また、ユーザーが何かを検証することを忘れてしまい、データベースに不適切なデータが誤って格納されることもなくなります。

更新された*ムービー .vb*ファイルの完全なコードリストを次に示します。

[!code-vb[Main](adding-validation-to-the-model/samples/sample4.vb)]

## <a name="validation-error-ui-in-aspnet-mvc"></a>ASP.NET MVC の検証エラー UI

アプリケーションを再実行し、 */ムービー*の URL に移動します。

**[ムービーの作成]** リンクをクリックして、新しいムービーを追加します。 フォームに無効な値を入力し、 **[作成]** ボタンをクリックします。

[![8_validationErrors](adding-validation-to-the-model/_static/image2.png)](adding-validation-to-the-model/_static/image1.png)

フォームが背景色を自動的に使用して、無効なデータを含むテキストボックスを強調表示し、それぞれの横に適切な検証エラーメッセージを生成したことに注目してください。 エラーメッセージは、`Movie` クラスに注釈を付けたときに指定したエラー文字列と一致します。 エラーは、(JavaScript を使用した) クライアント側とサーバー側 (ユーザーが JavaScript を無効にしている場合) の両方に適用されます。

実際の利点は、この検証 UI を有効にするため*に、`MoviesController`* クラスのコード行を1行も変更する必要がないことです。 このチュートリアルの前の手順で作成したコントローラーとビューでは、`Movie` モデルクラスの属性を使用して指定した検証規則が自動的に選択されます。

## <a name="how-validation-occurs-in-the-create-view-and-create-action-method"></a>Create View および Create Action メソッドでの検証の実行方法

コントローラーまたはビューのコードを更新しなくても検証 UI が生成する仕組みが気になるかもしれません。 次の一覧は、`MovieController` クラスの `Create` メソッドの外観を示しています。 これらは、このチュートリアルの前の手順で作成した方法から変更されていません。

[!code-vb[Main](adding-validation-to-the-model/samples/sample5.vb)]

最初のアクションメソッドでは、最初の作成フォームが表示されます。 2つ目はフォームポストを処理します。 2番目の `Create` メソッドは、`ModelState.IsValid` を呼び出して、ムービーに検証エラーがあるかどうかを確認します。 このメソッドを呼び出すと、オブジェクトに適用されているすべての検証属性が評価されます。 オブジェクトに検証エラーがある場合は、`Create` メソッドによってフォームが再構成されます。 エラーがない場合、メソッドはデータベースに新しいムービーを保存します。

次に示すのは、このチュートリアルで前にスキャフォールディングした、*作成した vbhtml*ビューテンプレートです。 これは、前に示した両方のアクション メソッドで、初期フォームの表示と、エラー発生時のフォームの再表示に使われます。

[!code-vbhtml[Main](adding-validation-to-the-model/samples/sample6.vbhtml)]

コードで `Html.EditorFor` ヘルパーを使用して、各 `Movie` プロパティの `<input>` 要素を出力する方法に注目してください。 このヘルパーの横には、`Html.ValidationMessageFor` ヘルパーメソッドの呼び出しがあります。 これらの2つのヘルパーメソッドは、コントローラーによってビューに渡されるモデルオブジェクト (この場合は `Movie` オブジェクト) と連携します。 これらは、モデルで指定された検証属性を自動的に検索し、必要に応じてエラーメッセージを表示します。

この方法は本当に便利ですが、コントローラーも Create view テンプレートにも、適用されている実際の検証規則や、表示されている特定のエラーメッセージについての情報は一切認識されません。 検証規則とエラー文字列は、`Movie` クラスでのみ指定されています。

後で検証ロジックを変更する場合は、厳密に1つの場所で実行できます。 アプリケーションの異なる部分で規則の適用方法が一貫しない可能性を心配する必要はありません。すべての検証ロジックは 1 か所で定義され、すべての場所で使われます。 これにより、コードの簡潔さが保たれ、簡単に維持や更新できます。 また、これは DRY 原則に完全に従うことを意味します。

## <a name="adding-formatting-to-the-movie-model"></a>ムービーモデルへの書式設定の追加

*Movie*ファイルを開きます。 [`System.ComponentModel.DataAnnotations`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)名前空間は、組み込みの検証属性のセットに加えて、書式設定属性を提供します。 [`DisplayFormat`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx)属性と[`DataType`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)列挙値をリリース日と価格フィールドに適用します。 次のコードは、適切な[`DisplayFormat`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx)属性を持つ `ReleaseDate` および `Price` プロパティを示しています。

[!code-vb[Main](adding-validation-to-the-model/samples/sample7.vb)]

または、 [`DataFormatString`](https://msdn.microsoft.com/library/system.string.format.aspx)値を明示的に設定することもできます。 次のコードは、"リリース日" プロパティと日付書式文字列 (つまり "d") を示しています。 これを使用して、リリース日の一部として時間を必要としないことを指定します。

[!code-vb[Main](adding-validation-to-the-model/samples/sample8.vb)]

次のコードでは、`Price` プロパティを通貨として書式設定しています。

[!code-vb[Main](adding-validation-to-the-model/samples/sample9.vb)]

完全な `Movie` クラスを次に示します。

[!code-vb[Main](adding-validation-to-the-model/samples/sample10.vb)]

アプリケーションを実行し、`Movies` コントローラーに移動します。

![8_format_SM](adding-validation-to-the-model/_static/image3.png)

シリーズの次のパートでは、アプリケーションを確認し、自動的に生成された `Details` および `Delete` メソッドに対していくつかの機能強化を行います。「」を参照してください。

> [!div class="step-by-step"]
> [前へ](adding-a-new-field.md)
> [次へ](improving-the-details-and-delete-methods.md)
