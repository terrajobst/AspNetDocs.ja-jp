---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-validation-to-the-model
title: モデルへの検証の追加 |Microsoft Docs
author: Rick-Anderson
description: '注: このチュートリアルの更新バージョンは、ASP.NET MVC 5 と Visual Studio 2013 を使用するこちらで入手できます。 より安全で、より簡単にフォローとデモができます...'
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 5d9a2999-fcc4-4c45-a018-271fddf74a3b
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-validation-to-the-model
msc.type: authoredcontent
ms.openlocfilehash: c9f6699c5d3500d4c1fcade9252aeb9dd92983da
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2020
ms.locfileid: "77455959"
---
# <a name="adding-validation-to-the-model"></a>モデルに検証を追加する

[Rick Anderson](https://twitter.com/RickAndMSFT)

> > [!NOTE]
> > このチュートリアルの更新バージョンは、ASP.NET MVC 5 と Visual Studio 2013 を使用する[こちらで](../../getting-started/introduction/getting-started.md)入手できます。 より安全で、より簡単にフォローし、より多くの機能を紹介します。

このセクションでは、`Movie` モデルに検証ロジックを追加し、ユーザーがアプリケーションを使用してムービーを作成または編集しようとするたびに検証規則が適用されるようにします。

## <a name="keeping-things-dry"></a>ドライを維持する

ASP.NET MVC の核となる設計の原則の1つは、ドライ (&quot;DRY 原則&quot;) です。 ASP.NET MVC を使用すると、機能または動作を一度だけ指定し、アプリケーション内のすべての場所に反映させることができます。 これにより、記述する必要があるコードの量が減り、記述するコードの記述がエラーを起こしやすくなり、保守が容易になります。

ASP.NET MVC と Entity Framework Code First によって提供される検証のサポートは、ドライの原則が動作する好例です。 (モデルクラス内の) 1 つの場所で検証規則を宣言によって指定すると、アプリケーション内のすべての場所で規則が適用されます。

ムービーアプリケーションでこの検証サポートを利用する方法を見てみましょう。

## <a name="adding-validation-rules-to-the-movie-model"></a>ムービーモデルへの検証規則の追加

まず、`Movie` クラスに検証ロジックを追加します。

*Movie.cs* ファイルを開きます。 [`System.ComponentModel.DataAnnotations`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)名前空間を参照するファイルの先頭に `using` ステートメントを追加します。

[!code-csharp[Main](adding-validation-to-the-model/samples/sample1.cs)]

名前空間に `System.Web`が含まれていないことに注意してください。 DataAnnotations には、任意のクラスまたはプロパティに宣言して適用できる、組み込みの検証属性セットが用意されています。

次に、組み込みの[`Required`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx)、 [`StringLength`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx)、および[`Range`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx)検証属性を利用できるように `Movie` クラスを更新します。 属性を適用する場所の例として、次のコードを使用します。

[!code-csharp[Main](adding-validation-to-the-model/samples/sample2.cs?highlight=4,10,13,17)]

アプリケーションを実行すると、次の実行時エラーが再度表示されます。

***データベースが作成されてから、' Mo? Dbcontext ' コンテキストをバッキングするモデルが変更されました。Code First Migrations を使用してデータベースを更新することを検討してください ([https://go.microsoft.com/fwlink/?LinkId=238269](https://go.microsoft.com/fwlink/?LinkId=238269))。***

ここでは、移行を使用してスキーマを更新します。 ソリューションをビルドし、 **[パッケージマネージャーコンソール]** ウィンドウを開き、次のコマンドを入力します。

[!code-console[Main](adding-validation-to-the-model/samples/sample3.cmd)]

このコマンドが終了すると、Visual Studio は、指定された名前 (*AddDataAnnotationsMig*) を持つ新しい `DbMigration` 派生クラスを定義するクラスファイルを開き、`Up` メソッドにスキーマ制約を更新するコードを表示できます。 `Title` フィールドと `Genre` フィールドは、null 値を入力する必要がなくなり、`Rating` フィールドの最大長は5になります。

検証属性では、適用対象のモデル プロパティに適用する動作を指定します。 `Required` 属性は、プロパティに値が必要であることを示します。このサンプルでは、有効にするために、ムービーに `Title`、`ReleaseDate`、`Genre`、および `Price` プロパティの値が必要です。 `Range` 属性は、指定した範囲内に値を制限します。 `StringLength` 属性では、文字列プロパティの最大長を設定でき、オプションとして最小長も設定できます。 組み込み型 (`decimal, int, float, DateTime`など) は既定で必須であり、`Required` 属性は必要ありません。

Code First により、アプリケーションがデータベースに変更を保存する前に、モデルクラスで指定した検証規則が確実に適用されます。 たとえば、次のコードでは、`SaveChanges` メソッドが呼び出されたときに例外がスローされます。これは、いくつかの必須の `Movie` プロパティ値が不足しており、価格が 0 (有効な範囲外) であるためです。

[!code-csharp[Main](adding-validation-to-the-model/samples/sample4.cs?highlight=7-8)]

.NET Framework によって検証規則が自動的に適用されるため、アプリケーションの堅牢性が向上します。 また、ユーザーが何かを検証することを忘れてしまい、データベースに不適切なデータが誤って格納されることもなくなります。

更新された*Movie.cs*ファイルの完全なコードリストを次に示します。

[!code-csharp[Main](adding-validation-to-the-model/samples/sample5.cs)]

## <a name="validation-error-ui-in-aspnet-mvc"></a>ASP.NET MVC の検証エラー UI

アプリケーションを再実行し、 */ムービー*の URL に移動します。

新しいムービーを追加するには、 **[新規作成]** リンクをクリックします。 フォームに無効な値を入力し、 **[作成]** ボタンをクリックします。

![8_validationErrors](adding-validation-to-the-model/_static/image1.png)

> [!NOTE]
> 小数点に対してコンマ (&quot;、&quot;) を使用する英語以外のロケールの jQuery 検証をサポートするには、`Globalize.parseFloat`を使用するために、*グローバライズ*および特定の*カルチャ/グローバライズ*ファイル ( [https://github.com/jquery/globalize](https://github.com/jquery/globalize)から) および JavaScript を含める必要があります。 次のコードは、&quot;fr-fr&quot; カルチャを操作するための Views\Movies\Edit.cshtml ファイルの変更を示しています。

[!code-cshtml[Main](adding-validation-to-the-model/samples/sample6.cshtml)]

フォームが赤い枠線の色を自動的に使用して、無効なデータを含むテキストボックスが強調表示され、それぞれの横に適切な検証エラーメッセージが出力されていることに注目してください。 エラーは、(JavaScript と jQuery を使用している) クライアント側とサーバー側 (ユーザーが JavaScript を無効にしている場合) の両方に適用されます。

実際の利点は、この検証 UI を有効にするために、`MoviesController` クラスまたは*Create. cshtml*ビューで1行のコードを変更する必要がないことです。 このチュートリアルで前に作成したコントローラーとビューにより、`Movie` モデル クラスのプロパティで検証属性を使って指定した検証規則が自動的に取得されます。

プロパティ `Title` と `Genre`についてご存知かもしれませんが、フォームを送信する ( **[Create]** ボタンを押す) か、入力フィールドにテキストを入力して削除するまで、必須の属性は適用されません。 最初は空で、必要な属性のみを持ち、その他の検証属性がないフィールドの場合は、次のようにして検証をトリガーできます。

1. Tab キーをフィールドに入力します。
2. テキストを入力してください。
3. タブを終了します。
4. Tab キーをフィールドに戻します。
5. テキストを削除します。
6. タブを終了します。

上記のシーケンスでは、[送信] ボタンをクリックしなくても必要な検証がトリガーされます。 フィールドを入力せずに [送信] ボタンを押すだけで、クライアント側の検証がトリガーされます。 クライアント側の検証エラーがなくなるまで、フォーム データはサーバーに送信されません。 これをテストするには、HTTP Post メソッドにブレークポイントを配置するか、 [fiddler ツール](http://fiddler2.com/fiddler2/)または IE 9 [F12 開発者ツール](https://msdn.microsoft.com/ie/aa740478)を使用します。

![](adding-validation-to-the-model/_static/image2.png)

## <a name="how-validation-occurs-in-the-create-view-and-create-action-method"></a>Create View および Create Action メソッドでの検証の実行方法

コントローラーまたはビューのコードを更新しなくても検証 UI が生成する仕組みが気になるかもしれません。 次の一覧は、`MovieController` クラスの `Create` メソッドの外観を示しています。 これらは、このチュートリアルの前の手順で作成した方法から変更されていません。

[!code-csharp[Main](adding-validation-to-the-model/samples/sample7.cs?highlight=12,15)]

最初の (HTTP GET の) `Create` アクション メソッドは、初期の作成フォームを表示します。 2 番目の (`[HttpPost]`) バージョンは、フォームの送信を処理します。 2 番目の `Create` メソッド (`HttpPost` バージョン) は、`ModelState.IsValid` を呼び出してムービーに検証エラーがあるかどうかを確認します。 このメソッドを呼び出すと、オブジェクトに適用されているすべての検証属性が評価されます。 オブジェクトに検証エラーがある場合、`Create` メソッドはフォームを再表示します。 エラーがない場合、メソッドはデータベースに新しいムービーを保存します。 を使用しているムービーの例では、**クライアント側で検証エラーが検出された場合、フォームはサーバーにポストされません。2番目の**`Create`**メソッドは呼び出さ**れません。 ブラウザーで JavaScript を無効にすると、クライアント検証が無効になり、HTTP POST `Create` メソッドが `ModelState.IsValid` を呼び出して、ムービーに検証エラーがあるかどうかを確認します。

`HttpPost Create` メソッドにブレークポイントを設定し、メソッドが呼び出されないことを確認できます。検証エラーが検出された場合、クライアント側の検証はフォームのデータを送信しません。 ブラウザーで JavaScript を無効にすると、エラーのあるフォームが送信され、ブレークポイントがヒットします。 JavaScript がなくても完全な検証が行われます。 次の図は、Internet Explorer で JavaScript を無効にする方法を示しています。

![](adding-validation-to-the-model/_static/image3.png)

![](adding-validation-to-the-model/_static/image4.png)

次の図では、FireFox ブラウザーで JavaScript を無効にする方法を示します。

![](adding-validation-to-the-model/_static/image5.png)

次の図は、Chrome ブラウザーで JavaScript を無効にする方法を示しています。

![](adding-validation-to-the-model/_static/image6.png)

次に示すのは、このチュートリアルの前半でスキャフォールディングした*作成. cshtml*ビューテンプレートです。 これは、前に示した両方のアクション メソッドで、初期フォームの表示と、エラー発生時のフォームの再表示に使われます。

[!code-cshtml[Main](adding-validation-to-the-model/samples/sample8.cshtml?highlight=22-23,30-31,38-39,46-47)]

コードで `Html.EditorFor` ヘルパーを使用して、各 `Movie` プロパティの `<input>` 要素を出力する方法に注目してください。 このヘルパーの横には、`Html.ValidationMessageFor` ヘルパーメソッドの呼び出しがあります。 これらの2つのヘルパーメソッドは、コントローラーによってビューに渡されるモデルオブジェクト (この場合は `Movie` オブジェクト) と連携します。 これらは、モデルで指定された検証属性を自動的に検索し、必要に応じてエラーメッセージを表示します。

この方法は本当に便利ですが、コントローラーも Create view テンプレートにも、適用されている実際の検証規則や、表示されている特定のエラーメッセージについての情報は一切認識されません。 検証規則とエラー文字列は、`Movie` クラスでのみ指定されています。 これらの同じ検証規則は、モデルを編集するために作成される編集ビューおよびその他のビューテンプレートに自動的に適用されます。

後で検証ロジックを変更する場合は、検証属性をモデルに追加して (この例では `movie` クラス)、厳密に1つの場所で検証ロジックを行うことができます。 アプリケーションの異なる部分で規則の適用方法が一貫しない可能性を心配する必要はありません。すべての検証ロジックは 1 か所で定義され、すべての場所で使われます。 これにより、コードの簡潔さが保たれ、簡単に維持や更新できます。 また、これは DRY 原則に完全に従うことを意味します。

## <a name="adding-formatting-to-the-movie-model"></a>ムービーモデルへの書式設定の追加

*Movie.cs* ファイルを開き、`Movie` クラスを調べます。 [`System.ComponentModel.DataAnnotations`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)名前空間は、組み込みの検証属性のセットに加えて、書式設定属性を提供します。 [`DataType`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)列挙値は、リリース日と価格フィールドに既に適用されています。 次のコードは、適切な[`DisplayFormat`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx)属性を持つ `ReleaseDate` および `Price` プロパティを示しています。

[!code-csharp[Main](adding-validation-to-the-model/samples/sample9.cs)]

[`DataType`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)属性は検証属性ではなく、HTML の表示方法をビューエンジンに指示するために使用されます。 上の例では、`DataType.Date` 属性は、時刻を指定せずに、ムービーの日付のみを日付として表示します。 たとえば、次の[`DataType`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)属性は、データの形式を検証しません。

[!code-csharp[Main](adding-validation-to-the-model/samples/sample10.cs)]

上記の属性は、ビューエンジンがデータを書式設定するためのヒントのみを提供します (また、URL の&gt; &lt;などの属性と、電子メールの場合は &lt;href =&quot;mailto:EmailAddress&quot;&gt; を指定します。 [RegularExpression](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.regularexpressionattribute.aspx)属性を使用して、データの形式を検証できます。

`DataType` の属性を使用する別の方法として、 [`DataFormatString`](https://msdn.microsoft.com/library/system.string.format.aspx)値を明示的に設定することもできます。 次のコードは、日付書式文字列 (つまり、&quot;d&quot;) を持つリリース日プロパティを示しています。 これを使用して、リリース日の一部として時間を必要としないことを指定します。

[!code-csharp[Main](adding-validation-to-the-model/samples/sample11.cs)]

完全な `Movie` クラスを次に示します。

[!code-csharp[Main](adding-validation-to-the-model/samples/sample12.cs)]

アプリケーションを実行し、`Movies` コントローラーに移動します。 リリース日と価格は適切に書式設定されます。 次の図は、&quot;fr-fr&quot; をカルチャとして使用したリリース日と価格を示しています。

![8_format_SM](adding-validation-to-the-model/_static/image7.png)

次の画像は、既定のカルチャ (英語 US) で表示されるのと同じデータを示しています。

![](adding-validation-to-the-model/_static/image8.png)

このシリーズの次のパートでは、アプリケーションを確認し、自動的に生成される `Details` および `Delete` メソッドに対していくつかの改良を行います。

> [!div class="step-by-step"]
> [前へ](adding-a-new-field-to-the-movie-model-and-table.md)
> [次へ](examining-the-details-and-delete-methods.md)
