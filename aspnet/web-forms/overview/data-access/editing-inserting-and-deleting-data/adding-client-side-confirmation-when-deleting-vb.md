---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/adding-client-side-confirmation-when-deleting-vb
title: 削除時にクライアント側の確認を追加する (VB) |Microsoft Docs
author: rick-anderson
description: これまでに作成したインターフェイスでは、ユーザーは [編集] ボタンをクリックしたときに [削除] ボタンをクリックしてデータを誤って削除できます。 この t...
ms.author: riande
ms.date: 07/17/2006
ms.assetid: 6331e02e-c465-4cdf-bd3f-f07680c289d6
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/adding-client-side-confirmation-when-deleting-vb
msc.type: authoredcontent
ms.openlocfilehash: addb5a1fdc5793309388c5f06b44fb3b145bc102
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78494596"
---
# <a name="adding-client-side-confirmation-when-deleting-vb"></a>削除時、クライアント側の確認を追加する (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[サンプルアプリのダウンロード](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_22_VB.exe)または[PDF のダウンロード](adding-client-side-confirmation-when-deleting-vb/_static/datatutorial22vb1.pdf)

> これまでに作成したインターフェイスでは、ユーザーは [編集] ボタンをクリックしたときに [削除] ボタンをクリックしてデータを誤って削除できます。 このチュートリアルでは、[削除] ボタンをクリックしたときに表示されるクライアント側の確認ダイアログボックスを追加します。

## <a name="introduction"></a>はじめに

これまでのいくつかのチュートリアルでは、アプリケーションアーキテクチャ、ObjectDataSource、およびデータ Web コントロールを連携して使用して、挿入、編集、および削除の機能を提供する方法を説明しました。 これまでに調査した削除インターフェイスは、[削除] ボタンで構成されています。このボタンをクリックすると、ポストバックが発生し、ObjectDataSource s `Delete()` メソッドが呼び出されます。 `Delete()` メソッドは、ビジネスロジック層から構成されたメソッドを呼び出します。これにより、呼び出しがデータアクセス層に反映され、実際の `DELETE` ステートメントがデータベースに発行されます。

このユーザーインターフェイスを使用すると、ユーザーが GridView、DetailsView、または FormView コントロールを使用してレコードを削除できますが、ユーザーが [削除] ボタンをクリックしても、どのような種類の確認も行われません。 [編集] をクリックしたときにユーザーが誤って [削除] ボタンをクリックした場合、更新する予定のレコードは削除されます。 この問題を回避するために、このチュートリアルでは、[削除] ボタンをクリックしたときに表示されるクライアント側の確認ダイアログボックスを追加します。

JavaScript `confirm(string)` 関数は、[OK] と [キャンセル] の2つのボタンを備えたモーダルダイアログボックス内のテキストとして、文字列入力パラメーターを表示します (図1を参照)。 `confirm(string)` 関数は、どのボタンがクリックされたかに応じてブール値を返します (ユーザーが [OK] をクリックした場合は`true`、[キャンセル] をクリックした場合は `false` ます)。

![JavaScript confirm (string) メソッドによって、モーダルのクライアント側のメッセージボックスが表示されます。](adding-client-side-confirmation-when-deleting-vb/_static/image1.png)

**図 1**: JavaScript `confirm(string)` メソッドによってモーダルのクライアント側のメッセージボックスが表示される

フォームの送信時に、クライアント側のイベントハンドラーから `false` の値が返された場合、フォームの送信は取り消されます。 この機能を使用すると、クライアント側の削除ボタン `onclick` イベントハンドラーが `confirm("Are you sure you want to delete this product?")`の呼び出しの値を返すことができます。 ユーザーが [キャンセル] をクリックすると、`confirm(string)` は false を返し、フォーム送信をキャンセルします。 ポストバックがない場合、[削除] ボタンがクリックされた製品は削除されません。 ただし、ユーザーが確認ダイアログボックスで [OK] をクリックすると、ポストバックは伴っを続行し、製品は削除されます。 この手法の詳細については、 [「JavaScript s `confirm()` メソッドを使用してフォームの送信を制御する](http://www.webreference.com/programming/javascript/confirm/)」を参照してください。

CommandField を使用する場合とは異なり、テンプレートを使用すると、必要なクライアント側スクリプトを追加することが若干異なります。 このチュートリアルでは、FormView と GridView の両方の例を見ていきます。

> [!NOTE]
> このチュートリアルで説明するように、クライアント側の確認方法を使用すると、ユーザーが JavaScript をサポートするブラウザーを使用してアクセスし、JavaScript が有効になっていることを前提としています。 これらの前提条件のいずれかが特定のユーザーに対して true でない場合、[削除] ボタンをクリックすると直ちにポストバックが発生します (確認メッセージボックスは表示されません)。

## <a name="step-1-creating-a-formview-that-supports-deletion"></a>手順 1: 削除をサポートする FormView の作成

まず、FormView を `EditInsertDelete` フォルダー内の `ConfirmationOnDelete.aspx` ページに追加し、`ProductsBLL` クラス s `GetProducts()` メソッドを使用して製品情報を取得する新しい ObjectDataSource にバインドします。 また、ObjectDataSource を構成して `ProductsBLL` クラス s `DeleteProduct(productID)` メソッドが ObjectDataSource s `Delete()` メソッドにマップされるようにします。[挿入] タブと [更新] タブのドロップダウンリストが [(なし)] に設定されていることを確認します。 最後に、FormView s スマートタグの [ページングを有効にする] チェックボックスをオンにします。

これらの手順の後に、新しい ObjectDataSource s 宣言マークアップは次のようになります。

[!code-aspx[Main](adding-client-side-confirmation-when-deleting-vb/samples/sample1.aspx)]

オプティミスティック同時実行制御を使用しなかった前の例と同様に、ObjectDataSource s `OldValuesParameterFormatString` プロパティを消去してみましょう。

削除のみをサポートする ObjectDataSource コントロールにバインドされているため、FormView s `ItemTemplate` は [削除] ボタンのみを提供します。 [新規] ボタンと [更新] ボタンはありません。 ただし、FormView の宣言型マークアップには、不要な `EditItemTemplate` と `InsertItemTemplate`が含まれています。これは削除できます。 製品データフィールドのサブセットのみが表示されるように、`ItemTemplate` をカスタマイズしてみてください。 ここでは、仕入先名とカテゴリ名の上に `<h3>` 見出しの製品名を表示するように構成しました ([削除] ボタンをクリックします)。

[!code-aspx[Main](adding-client-side-confirmation-when-deleting-vb/samples/sample2.aspx)]

これらの変更により、完全に機能する web ページが用意されています。ユーザーは、[削除] ボタンをクリックするだけで製品を削除することができます。 図2は、ブラウザーを通じて表示されるときの、これまでの進行状況のスクリーンショットを示しています。

[FormView に1つの製品に関する情報が表示される ![](adding-client-side-confirmation-when-deleting-vb/_static/image3.png)](adding-client-side-confirmation-when-deleting-vb/_static/image2.png)

**図 2**: FormView に1つの製品に関する情報が表示される ([クリックすると、フルサイズの画像が表示](adding-client-side-confirmation-when-deleting-vb/_static/image4.png)されます)

## <a name="step-2-calling-the-confirmstring-function-from-the-delete-buttons-client-side-onclick-event"></a>手順 2: [削除] ボタンのクライアント側の onclick イベントから confirm (string) 関数を呼び出す

FormView が作成されたら、最後の手順として、ビジターがクリックしたときに JavaScript `confirm(string)` 関数が呼び出されるように [削除] ボタンを構成します。 クライアント側のスクリプトをボタン、LinkButton、または ImageButton s クライアント側の `onclick` イベントに追加するには、ASP.NET 2.0 の新しい `OnClientClick property`を使用します。 返される `confirm(string)` 関数の値を取得する必要があるため、このプロパティを次のように設定します。 `return confirm('Are you certain that you want to delete this product?');`

この変更後、Delete LinkButton の宣言構文は次のようになります。

[!code-aspx[Main](adding-client-side-confirmation-when-deleting-vb/samples/sample3.aspx)]

これで完了です。 図3に、この確認の動作のスクリーンショットを示します。 [削除] ボタンをクリックすると、[確認] ダイアログボックスが表示されます。 ユーザーが [キャンセル] をクリックすると、ポストバックはキャンセルされ、製品は削除されません。 ただし、ユーザーが [OK] をクリックする `Delete()` と、ポストバックが続行され、するメソッドが呼び出され、削除されているデータベースレコードでます。

> [!NOTE]
> `confirm(string)` JavaScript 関数に渡される文字列は、引用符ではなくアポストロフィで区切られます。 JavaScript では、いずれかの文字を使用して文字列を区切ることができます。 ここではアポストロフィを使用して、`confirm(string)` に渡される文字列の区切り記号が、`OnClientClick` プロパティ値に使用される区切り記号とあいまいになることがないようにしています。

[![[削除] ボタンをクリックしたときに確認メッセージが表示されるようになりました。](adding-client-side-confirmation-when-deleting-vb/_static/image6.png)](adding-client-side-confirmation-when-deleting-vb/_static/image5.png)

**図 3**: [削除] ボタンをクリックしたときに確認が表示される ([クリックすると、フルサイズの画像が表示](adding-client-side-confirmation-when-deleting-vb/_static/image7.png)されます)

## <a name="step-3-configuring-the-onclientclick-property-for-the-delete-button-in-a-commandfield"></a>手順 3: CommandField の Delete ボタンの OnClientClick プロパティを構成する

テンプレート内で直接ボタン、LinkButton、または ImageButton を操作する場合、JavaScript `confirm(string)` 関数の結果を返すように `OnClientClick` プロパティを構成するだけで、確認ダイアログボックスを関連付けることができます。 ただし、[削除] ボタンのフィールドを GridView または DetailsView に追加する CommandField には、宣言によって設定できる `OnClientClick` のプロパティがありません。 代わりに、GridView または DetailsView の適切な `DataBound` イベントハンドラーで [削除] ボタンを参照し、その `OnClientClick` プロパティをそこで設定する必要があります。

> [!NOTE]
> 適切な `DataBound` イベントハンドラーで [削除] ボタン s `OnClientClick` プロパティを設定すると、現在のレコードにバインドされているデータにアクセスできるようになります。 つまり、「」のように、特定のレコードに関する詳細情報を含むように、確認メッセージを拡張できます。たとえば、「Chai 製品を削除しますか?」と入力します。 このようなカスタマイズは、データバインディング構文を使用するテンプレートでも可能です。

CommandField の [削除] ボタンの `OnClientClick` プロパティを設定する方法については、「」で GridView をページに追加してみましょう。 この GridView が、FormView が使用するのと同じ ObjectDataSource コントロールを使用するように構成します。 また、GridView の BoundFields を、製品名、カテゴリ、および業者のみを含むように制限します。 最後に、GridView s スマートタグから [削除を有効にする] チェックボックスをオンにします。 これにより、`ShowDeleteButton` プロパティが `true`に設定された GridView s `Columns` コレクションに CommandField が追加されます。

これらの変更を行った後、GridView の宣言型マークアップは次のようになります。

[!code-aspx[Main](adding-client-side-confirmation-when-deleting-vb/samples/sample4.aspx)]

CommandField には、GridView s `RowDataBound` イベントハンドラーからプログラムからアクセスできる単一の Delete LinkButton インスタンスが含まれています。 参照された後は、その `OnClientClick` プロパティを適宜設定できます。 次のコードを使用して、`RowDataBound` イベントのイベントハンドラーを作成します。

[!code-vb[Main](adding-client-side-confirmation-when-deleting-vb/samples/sample5.vb)]

このイベントハンドラーは、データ行 ([削除] ボタンを含む) で動作し、[削除] ボタンをプログラムで参照することによって開始します。 一般に、次のパターンを使用します。

[!code-vb[Main](adding-client-side-confirmation-when-deleting-vb/samples/sample6.vb)]

*です (buttontype*は、Commandfield、LinkButton、または ImageButton によって使用されているボタンの種類です。 既定では、CommandField は LinkButtons を使用しますが、これは CommandField s `ButtonType property`でカスタマイズできます。 *Commandfieldindex*は、GridView s `Columns` collection 内の commandfield の序数インデックスです。一方、制御*Lindex*は、commandfield s `Controls` コレクション内の Delete ボタンのインデックスです。 制御*Lindex*の値は、commandfield 内の他のボタンに対するボタンの位置によって異なります。 たとえば、CommandField に [削除] ボタンが表示されているだけの場合は、インデックス0を使用します。 ただし、[削除] ボタンの前に [編集] ボタンがある場合は、インデックス2を使用します。 インデックス2が使用される理由は、Delete ボタンの前に CommandField によって2つのコントロールが追加されるためです。 edit ボタンと LiteralControl は、エディットボタンと Delete ボタンの間にスペースを追加するために使用されます。

この例では、CommandField に LinkButtons が使用されており、左端のフィールドには*Commandfieldindex*が0になっています。 CommandField には他のボタンはありませんが、[削除] ボタンがあるため、0の制御*Lindex*を使用します。

CommandField の [削除] ボタンを参照した後、現在の GridView 行にバインドされている製品に関する情報を取得します。 最後に、[削除] ボタン s `OnClientClick` プロパティを適切な JavaScript (製品名を含む) に設定します。 `confirm(string)` 関数に渡される JavaScript 文字列はアポストロフィで区切られているため、製品名内に出現するアポストロフィをエスケープする必要があります。 特に、製品名のアポストロフィは、"`\'`" でエスケープされます。

これらの変更が完了したら、GridView の [削除] ボタンをクリックすると、カスタマイズされた確認ダイアログボックスが表示されます (図4を参照)。 FormView からの確認メッセージボックスと同様に、ユーザーが [キャンセル] をクリックした場合、ポストバックはキャンセルされるため、削除は行われません。

> [!NOTE]
> この手法を使用すると、DetailsView の CommandField の Delete ボタンにプログラムでアクセスすることもできます。 ただし、detailsview には、`RowDataBound` イベントがないため、`DataBound` イベントのイベントハンドラーを作成します。

[[GridView s Delete] ボタンをクリック ![と、カスタマイズされた確認ダイアログボックスが表示されます。](adding-client-side-confirmation-when-deleting-vb/_static/image9.png)](adding-client-side-confirmation-when-deleting-vb/_static/image8.png)

**図 4**: GridView の [削除] ボタンをクリックすると、カスタマイズされた確認ダイアログボックスが表示されます ([クリックすると、フルサイズの画像が表示](adding-client-side-confirmation-when-deleting-vb/_static/image10.png)されます)

## <a name="using-templatefields"></a>TemplateFields の使用

CommandField の欠点の1つは、インデックスを使用してそのボタンにアクセスし、結果のオブジェクトを適切なボタンの種類 (Button、LinkButton、または ImageButton) にキャストする必要があることです。 "マジックナンバー" とハードコーディングされた型を使用すると、実行時まで検出できない問題が発生します。 たとえば、ユーザーまたは別の開発者が、将来のある時点で CommandField に新しいボタンを追加したり、`ButtonType` プロパティを変更したりすると、既存のコードはエラーなしでコンパイルされますが、コードの記述方法や変更内容によっては、ページにアクセスすると例外や予期しない動作が発生する可能性があります。

別の方法として、GridView および DetailsView s CommandFields を TemplateFields に変換します。 これにより、CommandField の各ボタンに LinkButton (ボタンまたは ImageButton) を持つ `ItemTemplate` の TemplateField が生成されます。 これらのボタン `OnClientClick` プロパティは、FormView で見たように宣言によって割り当てることができます。また、次のパターンを使用して、適切な `DataBound` イベントハンドラーでプログラムからアクセスすることもできます。

[!code-vb[Main](adding-client-side-confirmation-when-deleting-vb/samples/sample7.vb)]

ここで、 *controlID*はボタン s `ID` プロパティの値です。 このパターンでは、キャストにハードコーディングされた型が必要ですが、インデックスを作成する必要がなくなり、実行時エラーが発生することなくレイアウトを変更できます。

## <a name="summary"></a>まとめ

JavaScript `confirm(string)` 関数は、フォーム送信ワークフローを制御するためによく使用される手法です。 この関数を実行すると、モーダルのクライアント側ダイアログボックスが表示されます。このダイアログボックスには、[OK] と [キャンセル] の2つのボタンが含まれます。 ユーザーが [OK] をクリックすると、`confirm(string)` 関数は `true`を返します。[キャンセル] をクリックすると `false`が返されます。 この機能は、ブラウザーの動作と組み合わせて、送信プロセス中にイベントハンドラーが `false`を返した場合に、フォームの送信をキャンセルします。これを使用すると、レコードを削除するときに確認メッセージボックスを表示できます。

`confirm(string)` 関数は、コントロール s `OnClientClick` プロパティを介して、ボタン Web コントロール s クライアント側 `onclick` イベントハンドラーに関連付けることができます。 テンプレートで [削除] ボタンを使用する場合 (FormView のテンプレートのいずれか、または DetailsView または GridView の TemplateField)。このプロパティは、このチュートリアルで説明したように、宣言またはプログラムによって設定できます。

プログラミングを楽しんでください。

## <a name="about-the-author"></a>著者について

1998以来、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)は 7 asp/創設者 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)の執筆者であり、Microsoft Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 2.0 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 mitchell@4GuysFromRolla.comでアクセスでき[ます。](mailto:mitchell@4GuysFromRolla.com) または彼のブログを参照してください。これは[http://ScottOnWriting.NET](http://ScottOnWriting.NET)にあります。

> [!div class="step-by-step"]
> [前へ](implementing-optimistic-concurrency-vb.md)
> [次へ](limiting-data-modification-functionality-based-on-the-user-vb.md)
