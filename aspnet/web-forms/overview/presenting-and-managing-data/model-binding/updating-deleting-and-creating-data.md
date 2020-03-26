---
uid: web-forms/overview/presenting-and-managing-data/model-binding/updating-deleting-and-creating-data
title: モデルバインドと web フォームを使用したデータの更新、削除、および作成 |Microsoft Docs
author: Rick-Anderson
description: このチュートリアルシリーズでは、ASP.NET Web フォームプロジェクトでモデルバインドを使用するための基本的な側面を示します。 モデルバインドを使用すると、データの相互作用がより簡単になり-...
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 602baa94-5a4f-46eb-a717-7a9e539c1db4
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/updating-deleting-and-creating-data
msc.type: authoredcontent
ms.openlocfilehash: 11dc52ec79ca91119b37ea60e08164eb1b1d0e2b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78474136"
---
# <a name="updating-deleting-and-creating-data-with-model-binding-and-web-forms"></a>モデルバインドと web フォームを使用したデータの更新、削除、および作成

によって[Tom FitzMacken](https://github.com/tfitzmac)

> このチュートリアルシリーズでは、ASP.NET Web フォームプロジェクトでモデルバインドを使用するための基本的な側面を示します。 モデルバインドを使用すると、データソースオブジェクト (ObjectDataSource や SqlDataSource など) を処理するよりも、データ操作がより簡単になります。 このシリーズでは、入門資料から開始し、以降のチュートリアルでより高度な概念に移ります。
> 
> このチュートリアルでは、モデルバインディングを使用してデータを作成、更新、および削除する方法について説明します。 次のプロパティを設定します。
> 
> - DeleteMethod
> - InsertMethod
> - UpdateMethod
> 
> これらのプロパティは、対応する操作を処理するメソッドの名前を受け取ります。 そのメソッド内で、データと対話するためのロジックを提供します。
> 
> このチュートリアルは、シリーズの第 1[部](retrieving-data.md)で作成したプロジェクトに基づいています。
> 
> 完全なプロジェクトは、またはC# VB で[ダウンロード](https://go.microsoft.com/fwlink/?LinkId=286116)できます。 ダウンロード可能なコードは、Visual Studio 2012 または Visual Studio 2013 で動作します。 このチュートリアルでは、Visual Studio 2012 テンプレートを使用します。これは、このチュートリアルで示した Visual Studio 2013 テンプレートとは少し異なります。

## <a name="what-youll-build"></a>ビルドする内容

このチュートリアルでは、次のことについて説明します。

1. 動的データテンプレートの追加
2. モデルバインドメソッドを使用したデータの更新と削除を有効にする
3. データ検証規則の適用-データベースでの新しいレコードの作成を有効にします。

## <a name="add-dynamic-data-templates"></a>動的データテンプレートの追加

最適なユーザーエクスペリエンスを提供し、コードの繰り返しを最小限に抑えるには、動的なデータテンプレートを使用します。 NuGet パッケージをインストールすると、事前に構築された動的なデータテンプレートを既存のサイトに簡単に統合できます。

**[NuGet パッケージの管理]** で、 **DynamicDataTemplatesCS**をインストールします。

![動的なデータテンプレート](updating-deleting-and-creating-data/_static/image1.png)

プロジェクトに**DynamicData**という名前のフォルダーが追加されていることに注意してください。 このフォルダーには、web フォームの動的コントロールに自動的に適用されるテンプレートがあります。

![動的データフォルダー](updating-deleting-and-creating-data/_static/image2.png)

## <a name="enable-updating-and-deleting"></a>更新と削除を有効にする

ユーザーがデータベース内のレコードを更新および削除できるようにすることは、データを取得するプロセスと非常によく似ています。 **UpdateMethod**プロパティと**DeleteMethod**プロパティでは、これらの操作を実行するメソッドの名前を指定します。 GridView コントロールでは、[編集] ボタンと [削除] ボタンの自動生成を指定することもできます。 次の強調表示されたコードは、GridView コードへの追加を示しています。

[!code-aspx[Main](updating-deleting-and-creating-data/samples/sample1.aspx?highlight=4-5)]

分離コードファイルで、using ステートメントを追加して、system.object を追加し**ます。**

[!code-csharp[Main](updating-deleting-and-creating-data/samples/sample2.cs)]

次に、update メソッドと delete メソッドを追加します。

[!code-csharp[Main](updating-deleting-and-creating-data/samples/sample3.cs)]

**TryUpdateModel**メソッドは、web フォームからデータ項目に、一致するデータバインド値を適用します。 データ項目は、id パラメーターの値に基づいて取得されます。

## <a name="enforce-validation-requirements"></a>検証要件の適用

Student クラスの FirstName、LastName、および Year プロパティに適用した検証属性は、データの更新時に自動的に適用されます。 DynamicField は、検証属性に基づいてクライアントとサーバーの検証コントロールを追加します。 FirstName と LastName の両方のプロパティが必要です。 FirstName は、長さが20文字を超えることはできず、LastName は40文字を超えることはできません。 Year は、AcademicYear 列挙型の有効な値である必要があります。

ユーザーがいずれかの検証要件に違反している場合、更新は続行されません。 エラーメッセージを表示するには、GridView の上に ValidationSummary コントロールを追加します。 モデルバインドの検証エラーを表示するには、 **Showmodelstateerrors**プロパティを**true**に設定します。 

[!code-aspx[Main](updating-deleting-and-creating-data/samples/sample4.aspx)]

Web アプリケーションを実行し、レコードを更新して削除します。

![データの更新](updating-deleting-and-creating-data/_static/image3.png)

編集モードでは、Year プロパティの値がドロップダウンリストとして自動的に表示されることに注意してください。 Year プロパティは列挙値で、列挙値の動的データテンプレートは編集用のドロップダウンリストを指定します。 このテンプレートを見つけるには、 **DynamicData**/**fieldtemplates**フォルダーで**列挙\_編集 .ascx**ファイルを開きます。

有効な値を指定した場合、更新は正常に完了します。 検証要件のいずれかに違反した場合、更新は続行されず、グリッドの上にエラーメッセージが表示されます。

![error message](updating-deleting-and-creating-data/_static/image4.png)

## <a name="add-new-records"></a>新しいレコードの追加

GridView コントロールには**Insertmethod**プロパティが含まれていないため、モデルバインドで新しいレコードを追加するために使用することはできません。 InsertMethod プロパティは、 **FormView**、 **DetailsView**、または**ListView**コントロールで見つけることができます。 このチュートリアルでは、FormView コントロールを使用して新しいレコードを追加します。

まず、新しいレコードを追加するために作成する新しいページへのリンクを追加します。 ValidationSummary の上に、次のように追加します。

[!code-aspx[Main](updating-deleting-and-creating-data/samples/sample5.aspx)]

新しいリンクは、[Students] ページのコンテンツの上部に表示されます。

![新しいリンク](updating-deleting-and-creating-data/_static/image5.png)

次に、マスターページを使用して新しい web フォームを追加し、「 **Addstudent**」という名前を指定します。 マスターページとして [.Master] を選択します。

**DynamicEntity**コントロールを使用して、新しい学生を追加するためのフィールドを表示します。 DynamicEntity コントロールは、ItemType プロパティで指定されたクラスの編集可能なプロパティをレンダリングします。 StudentID プロパティは、表示されないように、 **[ScaffoldColumn (false)]** 属性でマークされています。 AddStudent ページの MainContent プレースホルダーで、次のコードを追加します。

[!code-aspx[Main](updating-deleting-and-creating-data/samples/sample6.aspx)]

分離コードファイル (AddStudent.aspx.cs) で、コンテキスト**の名前空間**に対して、using ステートメントを追加し**て**ください。

[!code-csharp[Main](updating-deleting-and-creating-data/samples/sample7.cs)]

次に、次のメソッドを追加して、新しいレコードの挿入方法と [キャンセル] ボタンのイベントハンドラーを指定します。

[!code-csharp[Main](updating-deleting-and-creating-data/samples/sample8.cs)]

すべての変更を保存します。

Web アプリケーションを実行し、新しい学生を作成します。

![新しい学生の追加](updating-deleting-and-creating-data/_static/image6.png)

**[挿入]** をクリックすると、新しい学生が作成されたことがわかります。

![新しい学生を表示](updating-deleting-and-creating-data/_static/image7.png)

## <a name="conclusion"></a>まとめ

このチュートリアルでは、データの更新、削除、および作成を有効にしました。 データを操作するときに検証規則が適用されることを確認しました。

このシリーズの次の[チュートリアル](sorting-paging-and-filtering-data.md)では、データの並べ替え、ページング、フィルター処理を有効にします。

> [!div class="step-by-step"]
> [前へ](retrieving-data.md)
> [次へ](sorting-paging-and-filtering-data.md)
