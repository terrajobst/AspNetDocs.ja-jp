---
uid: web-forms/overview/presenting-and-managing-data/model-binding/using-query-string-values-to-retrieve-data
title: クエリ文字列値を使用してモデルバインドと web フォームを使用してデータをフィルター処理する |Microsoft Docs
author: Rick-Anderson
description: このチュートリアルシリーズでは、ASP.NET Web フォームプロジェクトでモデルバインドを使用するための基本的な側面を示します。 モデルバインドを使用すると、データの相互作用がより簡単になり-...
ms.author: riande
ms.date: 02/27/2014
ms.assetid: b90978bd-795d-4871-9ade-1671caff5730
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/using-query-string-values-to-retrieve-data
msc.type: authoredcontent
ms.openlocfilehash: 143ddcb40b576a3129e659b90bfc8321c061a547
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78519082"
---
# <a name="using-query-string-values-to-filter-data-with-model-binding-and-web-forms"></a>クエリ文字列値を使用してモデルバインドと web フォームを使用してデータをフィルター処理する

によって[Tom FitzMacken](https://github.com/tfitzmac)

> このチュートリアルシリーズでは、ASP.NET Web フォームプロジェクトでモデルバインドを使用するための基本的な側面を示します。 モデルバインドを使用すると、データソースオブジェクト (ObjectDataSource や SqlDataSource など) を処理するよりも、データ操作がより簡単になります。 このシリーズでは、入門資料から開始し、以降のチュートリアルでより高度な概念に移ります。
> 
> このチュートリアルでは、クエリ文字列に値を渡し、その値を使用してモデルバインドを通じてデータを取得する方法について説明します。
> 
> このチュートリアルは、シリーズの[前](retrieving-data.md)のパートで作成したプロジェクトに基づいています。
> 
> 完全なプロジェクトは、またはC# VB で[ダウンロード](https://go.microsoft.com/fwlink/?LinkId=286116)できます。 ダウンロード可能なコードは、Visual Studio 2012 または Visual Studio 2013 で動作します。 このチュートリアルでは、Visual Studio 2012 テンプレートを使用します。これは、このチュートリアルで示した Visual Studio 2013 テンプレートとは少し異なります。

## <a name="what-youll-build"></a>ビルドする内容

このチュートリアルでは、次のことについて説明します。

1. 学生に登録されたコースを表示する新しいページを追加する
2. クエリ文字列の値に基づいて、選択した学生の登録済みコースを取得します。
3. グリッドビューから新しいページにクエリ文字列値を含むハイパーリンクを追加する

このチュートリアルの手順は、前の[チュートリアル](sorting-paging-and-filtering-data.md)で説明した手順とほぼ同じですが、ドロップダウンリストでのユーザー選択に基づいて、表示される学生をフィルター処理します。 このチュートリアルでは、select メソッドで**control**属性を使用して、パラメーター値がコントロールから取得されるように指定しています。 このチュートリアルでは、select メソッドで**QueryString**属性を使用して、パラメーター値をクエリ文字列から取得するように指定します。

## <a name="add-new-page-for-displaying-a-students-courses"></a>学生のコースを表示するための新しいページを追加する

.Master マスターページを使用する新しい web フォームを追加し、そのページに**コース**の名前を指定します。

コースの **.aspx**ファイルで、選択した学生のコースを表示するグリッドビューを追加します。

[!code-aspx[Main](using-query-string-values-to-retrieve-data/samples/sample1.aspx)]

## <a name="define-the-select-method"></a>Select メソッドを定義する

**Courses.aspx.cs**では、grid ビューの**SelectMethod**プロパティで指定した名前を使用して、select メソッドを追加します。 このメソッドでは、学生のコースを取得するためのクエリを定義し、パラメーターと同じ名前のクエリ文字列値からパラメーターを取得するように指定します。

まず、次の**using**ステートメントを追加する必要があります。

[!code-csharp[Main](using-query-string-values-to-retrieve-data/samples/sample2.cs)]

次に、Courses.aspx.cs に次のコードを追加します。

[!code-csharp[Main](using-query-string-values-to-retrieve-data/samples/sample3.cs)]

QueryString 属性は、StudentID という名前のクエリ文字列値がこのメソッドのパラメーターに自動的に割り当てられることを意味します。

## <a name="add-hyperlink-with-query-string-value"></a>クエリ文字列値を含むハイパーリンクの追加

Student のグリッドビューでは、[新しいコース] ページにリンクするハイパーリンクフィールドを追加します。 ハイパーリンクには、学生の id を持つクエリ文字列値が含まれます。

Student で、合計クレジットのフィールドのすぐ下に、次のフィールドをグリッドビューの列に追加します。

[!code-aspx[Main](using-query-string-values-to-retrieve-data/samples/sample4.aspx?highlight=7-8)]

アプリケーションを実行し、グリッドビューに [コース] リンクが表示されていることを確認します。

![ハイパーリンクの追加](using-query-string-values-to-retrieve-data/_static/image1.png)

いずれかのリンクをクリックすると、学生の登録済みコースが表示されます。

![コースを表示](using-query-string-values-to-retrieve-data/_static/image2.png)

## <a name="conclusion"></a>まとめ

このチュートリアルでは、クエリ文字列値を含むリンクを追加しました。 このクエリ文字列値は、select メソッドのパラメーター値として使用しています。

次の[チュートリアル](adding-business-logic-layer.md)では、分離コードファイルのコードをビジネスロジック層とデータアクセス層に移動します。

> [!div class="step-by-step"]
> [前へ](integrating-jquery-ui.md)
> [次へ](adding-business-logic-layer.md)
