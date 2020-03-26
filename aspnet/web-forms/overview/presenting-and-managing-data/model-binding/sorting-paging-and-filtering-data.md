---
uid: web-forms/overview/presenting-and-managing-data/model-binding/sorting-paging-and-filtering-data
title: モデルバインドと web フォームを使用したデータの並べ替え、ページング、フィルター処理 |Microsoft Docs
author: Rick-Anderson
description: このチュートリアルシリーズでは、ASP.NET Web フォームプロジェクトでモデルバインドを使用するための基本的な側面を示します。 モデルバインドを使用すると、データの相互作用がより簡単になり-...
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 266e7866-e327-4687-b29d-627a0925e87d
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/sorting-paging-and-filtering-data
msc.type: authoredcontent
ms.openlocfilehash: f8e64392af6110f36c6af98c4e4e9481c94a0d82
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78441064"
---
# <a name="sorting-paging-and-filtering-data-with-model-binding-and-web-forms"></a>モデルバインドと web フォームを使用したデータの並べ替え、ページング、およびフィルター処理

によって[Tom FitzMacken](https://github.com/tfitzmac)

> このチュートリアルシリーズでは、ASP.NET Web フォームプロジェクトでモデルバインドを使用するための基本的な側面を示します。 モデルバインドを使用すると、データソースオブジェクト (ObjectDataSource や SqlDataSource など) を処理するよりも、データ操作がより簡単になります。 このシリーズでは、入門資料から開始し、以降のチュートリアルでより高度な概念に移ります。
> 
> このチュートリアルでは、モデルバインドを使用してデータの並べ替え、ページング、およびフィルター処理を行う方法について説明します。
> 
> このチュートリアルは、シリーズの第 1[部](retrieving-data.md)で作成したプロジェクトに基づいています。
> 
> 完全なプロジェクトは、またはC# VB で[ダウンロード](https://go.microsoft.com/fwlink/?LinkId=286116)できます。 ダウンロード可能なコードは、Visual Studio 2012 または Visual Studio 2013 で動作します。 このチュートリアルでは、Visual Studio 2012 テンプレートを使用します。これは、このチュートリアルで示した Visual Studio 2013 テンプレートとは少し異なります。

## <a name="what-youll-build"></a>ビルドする内容

このチュートリアルでは、次のことについて説明します。

1. データの並べ替えとページングを有効にする
2. ユーザーによる選択に基づいたデータのフィルター処理を有効にする

## <a name="add-sorting"></a>並べ替えの追加

GridView での並べ替えを有効にするのは非常に簡単です。 Student ファイルでは、GridView で**Allowsorting**を**true**に設定するだけです。 DataField が自動的に使用されるため、各列に**SortExpression**値を設定する必要はありません。 GridView は、選択された値によってデータの順序付けを含むようにクエリを変更します。 下の強調表示されているコードは、並べ替えを有効にするために必要な追加を示しています。

[!code-aspx[Main](sorting-paging-and-filtering-data/samples/sample1.aspx?highlight=5)]

Web アプリケーションを実行し、異なる列の値で生徒のレコードの並べ替えをテストします。

![生徒の並べ替え](sorting-paging-and-filtering-data/_static/image2.png)

## <a name="add-paging"></a>ページングの追加

ページングを有効にすることも非常に簡単です。 GridView で、 **Allowpaging**プロパティを**true**に設定し、 **PageSize**プロパティに、各ページに表示するレコード数を設定します。 このチュートリアルでは、4に設定できます。

[!code-aspx[Main](sorting-paging-and-filtering-data/samples/sample2.aspx?highlight=5)]

Web アプリケーションを実行すると、レコードが1ページに表示されるレコードが4つ以下の複数のページに分割されていることがわかります。

![ページングの追加](sorting-paging-and-filtering-data/_static/image4.png)

クエリの遅延実行により、アプリケーションの効率が向上します。 GridView は、データセット全体を取得するのではなく、現在のページのレコードのみを取得するようにクエリを変更します。

## <a name="filter-records-by-user-selection"></a>ユーザー選択でレコードをフィルター処理する

モデルバインドでは、モデルバインドメソッドでパラメーターの値を設定する方法を指定できるように、いくつかの属性が追加されます。 これらの属性は、 **System.web バインド**名前空間にあります。 それには以下が含まれます。

- コントロール
- クッキー
- Form
- Profile
- QueryString
- RouteData
- セッション
- UserProfile
- ビューの状態

このチュートリアルでは、コントロールの値を使用して、GridView に表示するレコードをフィルター処理します。 前の手順で作成したクエリメソッドに**コントロール**属性を追加します。 [後](using-query-string-values-to-retrieve-data.md)のチュートリアルでは、パラメーターにクエリ文字列値を使用することを指定するために、 **QueryString**属性をパラメーターに適用します。

まず、ValidationSummary の上に、表示される学生をフィルター処理するためのドロップダウンリストを追加します。

[!code-aspx[Main](sorting-paging-and-filtering-data/samples/sample3.aspx?highlight=3-11)]

分離コードファイルで、コントロールから値を受け取るように選択メソッドを変更し、パラメーターの名前を、値を提供するコントロールの名前に設定します。

Control 属性を解決するには、 **System.web binding**名前空間の**using**ステートメントを追加する必要があります。

[!code-csharp[Main](sorting-paging-and-filtering-data/samples/sample4.cs)]

次のコードは、ドロップダウンリストの値に基づいて、返されたデータをフィルター処理するための選択メソッドを示しています。 パラメーターの前にコントロール属性を追加すると、このパラメーターの値は同じ名前のコントロールから取得されます。

[!code-csharp[Main](sorting-paging-and-filtering-data/samples/sample5.cs)]

Web アプリケーションを実行し、ドロップダウンリストから別の値を選択して、学生の一覧をフィルター処理します。

![学生のフィルター処理](sorting-paging-and-filtering-data/_static/image6.png)

## <a name="conclusion"></a>まとめ

このチュートリアルでは、データの並べ替えとページングを有効にしました。 また、コントロールの値によってデータのフィルター処理を有効にしました。

次の[チュートリアル](integrating-jquery-ui.md)では、JQuery ui ウィジェットを動的データテンプレートに統合することによって、UI を強化します。

> [!div class="step-by-step"]
> [前へ](updating-deleting-and-creating-data.md)
> [次へ](integrating-jquery-ui.md)
