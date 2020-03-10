---
uid: mvc/overview/older-versions-1/models-data/performing-simple-validation-vb
title: 単純な検証を実行する (VB) |Microsoft Docs
author: StephenWalther
description: ASP.NET MVC アプリケーションで検証を実行する方法について説明します。 このチュートリアルでは、Stephen Walther がモデルの状態と検証 HTML ヘルパーについて説明します。
ms.author: riande
ms.date: 03/02/2009
ms.assetid: df6cf4b7-0bb3-4c4e-b17a-bd78a759a6bc
msc.legacyurl: /mvc/overview/older-versions-1/models-data/performing-simple-validation-vb
msc.type: authoredcontent
ms.openlocfilehash: 46925f22b7dfc23f2bb89b8d2fff0cbd8ae49062
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78436666"
---
# <a name="performing-simple-validation-vb"></a>簡易検証を実行する (VB)

[Stephen Walther](https://github.com/StephenWalther)

> ASP.NET MVC アプリケーションで検証を実行する方法について説明します。 このチュートリアルでは、Stephen Walther が、モデルの状態と検証 HTML ヘルパーについて説明します。

このチュートリアルの目的は、ASP.NET MVC アプリケーション内で検証を実行する方法について説明することです。 たとえば、必要なフィールドの値が含まれていないユーザーがフォームを送信できないようにする方法について説明します。 モデルの状態と検証 HTML ヘルパーを使用する方法について説明します。

## <a name="understanding-model-state"></a>モデルの状態について

検証エラーを表すには、モデル状態を使用するか、より正確にモデル状態ディクショナリを使用します。 たとえば、リスト1の Create () アクションは、Product クラスをデータベースに追加する前に、Product クラスのプロパティを検証します。

検証またはデータベースロジックをコントローラーに追加することは推奨されていません。 コントローラーには、アプリケーションフロー制御に関連するロジックのみを含める必要があります。 単純なものを保持するためのショートカットがあります。

**リスト 1-コントローラーと vb**

[!code-vb[Main](performing-simple-validation-vb/samples/sample1.vb)]

リスト1では、Product クラスの名前、説明、および在庫プロパティが検証されます。 これらのプロパティのいずれかが検証テストに失敗した場合、モデル状態ディクショナリ (コントローラークラスの ModelState プロパティで表される) にエラーが追加されます。

モデル状態にエラーがある場合、ModelState. IsValid プロパティは false を返します。 この場合、新しい製品を作成するための HTML フォームが再生成されます。 それ以外の場合、検証エラーがない場合は、新しい製品がデータベースに追加されます。

## <a name="using-the-validation-helpers"></a>検証ヘルパーの使用

ASP.NET MVC フレームワークには、2つの検証ヘルパー (Html. ValidationMessage () ヘルパーと Html. Validationmessage () ヘルパー) が含まれています。 ビューでこれらの2つのヘルパーを使用して、検証エラーメッセージを表示します。

ASP.NET MVC スキャフォールディングによって自動的に生成される Create ビューと Edit ビューでは、Html の ValidationMessage () ヘルパーと Html. Validationmessage () ヘルパーが使用されます。 作成ビューを生成するには、次の手順に従います。

1. 製品コントローラーで [作成] () アクションを右クリックし、[ビューの**追加**] メニューオプションを選択します (図1を参照)。
2. **[ビューの追加]** ダイアログで、厳密に型指定され **[たビューを作成する]** チェックボックスをオンにします (図2を参照)。
3. **[データクラスの表示]** ドロップダウンリストから、Product クラスを選択します。
4. **ビューコンテンツ** ボックスの一覧から 作成 を選択します。
5. **[追加]** をクリックします。

ビューを追加する前に、アプリケーションをビルドしていることを確認してください。 それ以外の場合は、 **[ビューデータクラス]** ボックスの一覧にクラスの一覧が表示されません。

[[新しいプロジェクト] ダイアログボックスの ![](performing-simple-validation-vb/_static/image1.jpg)](performing-simple-validation-vb/_static/image1.png)

**図 01**: ビューを追加[する (クリックすると、フルサイズの画像が表示](performing-simple-validation-vb/_static/image2.png)される)

[[新しいプロジェクト] ダイアログボックスの ![](performing-simple-validation-vb/_static/image2.jpg)](performing-simple-validation-vb/_static/image3.png)

**図 02**: 厳密に型指定されたビューの作成 ([クリックすると、フルサイズの画像が表示](performing-simple-validation-vb/_static/image4.png)されます)

これらの手順を完了すると、リスト2の [作成] ビューが表示されます。

**リスト 2-Views\Product\Create.aspx**

[!code-aspx[Main](performing-simple-validation-vb/samples/sample2.aspx)]

リスト2では、html 形式ではすぐに html 形式の Summary () ヘルパーが呼び出されます。 このヘルパーは、検証エラーメッセージの一覧を表示するために使用されます。 Html. ValidationSummary () ヘルパーは、箇条書きでエラーを表示します。

Html の ValidationMessage () ヘルパーは、各 HTML フォームフィールドの横に呼び出されます。 このヘルパーは、フォームフィールドの横にエラーメッセージを表示するために使用されます。 リスト2の場合、エラーが発生すると、Html. ValidationMessage () ヘルパーにアスタリスクが表示されます。

図3のページは、不足しているフィールドと無効な値を使用してフォームを送信したときに検証ヘルパーによって表示されるエラーメッセージを示しています。

[[新しいプロジェクト] ダイアログボックスの ![](performing-simple-validation-vb/_static/image3.jpg)](performing-simple-validation-vb/_static/image5.png)

**図 03**: 問題が発生して送信される作成ビュー ([クリックすると、フルサイズの画像が表示](performing-simple-validation-vb/_static/image6.png)されます)

検証エラーが発生すると、HTML 入力フィールドの外観も変更されることに注意してください。 .Html () ヘルパーは、Html. TextBox () ヘルパーによってレンダリングされるプロパティに関連付けられている検証エラーがある場合に、 *class = "input-validation-error"* 属性をレンダリングします。

検証エラーの表示を制御するために使用されるカスケードスタイルシートクラスには、次の3つがあります。

- 入力-検証-エラー-Html. TextBox () ヘルパーによってレンダリングされる &lt;入力&gt; タグに適用されます。
- フィールド検証-エラー-&lt;スパン&gt; タグに適用されます。これは、Html. ValidationMessage () ヘルパーによって表示されます。
- 検証-概要-エラー-Html. ValidationSummary () ヘルパーによってレンダリングされる &lt;ul&gt; タグに適用されます。

これらのカスケードスタイルシートクラスを変更して、コンテンツフォルダーに配置されているサイトの .css ファイルを変更することで、検証エラーの外観を変更することができます。

> [!NOTE] 
> 
> HtmlHelper クラスには、検証に関連する CSS クラスの名前を取得するための読み取り専用の静的プロパティが含まれています。 これらの静的プロパティの名前は、ValidationInputCssClassName、ValidationValidationSummaryCssClassName、およびです。

## <a name="prebinding-validation-and-postbinding-validation"></a>事前バインディング検証と Postbinding 検証

製品を作成するための HTML フォームを送信したときに、[価格] フィールドに無効な値を入力し、[在庫管理] フィールドに値が入力されていない場合は、図4に検証メッセージが表示されます。 これらの検証エラーメッセージの発信元

[[新しいプロジェクト] ダイアログボックスの ![](performing-simple-validation-vb/_static/image4.jpg)](performing-simple-validation-vb/_static/image7.png)

**図 04**: 事前バインディングの検証エラー ([クリックしてフルサイズのイメージを表示](performing-simple-validation-vb/_static/image8.png))

実際には、2種類の検証エラーメッセージ (HTML フォームフィールドがクラスにバインドされる前に生成されたものと、フォームフィールドがクラスにバインドされた後に生成されたもの) があります。 つまり、事前バインディング検証エラーと postbinding 検証エラーがあります。

リスト1の製品コントローラーによって公開される Create () アクションでは、Product クラスのインスタンスが受け入れられます。 Create メソッドのシグネチャは次のようになります。

[!code-vb[Main](performing-simple-validation-vb/samples/sample3.vb)]

作成フォームの HTML フォームフィールドの値は、モデルバインダーと呼ばれるものによって productToCreate クラスにバインドされます。 既定のモデルバインダーは、フォームフィールドをフォームプロパティにバインドできない場合に、エラーメッセージをモデル状態に自動的に追加します。

既定のモデルバインダーは、文字列 "apple" を Product クラスの Price プロパティにバインドできません。 Decimal プロパティに文字列を割り当てることはできません。 そのため、モデルバインダーは、モデルの状態にエラーを追加します。

既定のモデルバインダーも、値 Nothing を受け入れないプロパティに値 Nothing を割り当てることはできません。 特に、モデルバインダーは、在庫プロパティに値 Nothing を割り当てることはできません。 この場合も、モデルバインダーによってエラーメッセージがモデルの状態に追加されます。

これらのプリバインドエラーメッセージの外観をカスタマイズする場合は、これらのメッセージのリソース文字列を作成する必要があります。

## <a name="summary"></a>まとめ

このチュートリアルの目的は、ASP.NET MVC フレームワークでの検証の基本的なしくみを説明することでした。 モデルの状態と検証 HTML ヘルパーの使用方法について学習しました。 また、prebinding と postbinding の検証の違いについても説明しました。 他のチュートリアルでは、検証コードをコントローラーからモデルクラスに移行するためのさまざまな戦略について説明します。

> [!div class="step-by-step"]
> [前へ](displaying-a-table-of-database-data-vb.md)
> [次へ](validating-with-the-idataerrorinfo-interface-vb.md)
