---
uid: web-forms/overview/presenting-and-managing-data/model-binding/adding-business-logic-layer
title: モデルバインドと web フォームを使用するプロジェクトへのビジネスロジック層の追加 |Microsoft Docs
author: Rick-Anderson
description: このチュートリアルシリーズでは、ASP.NET Web フォームプロジェクトでモデルバインドを使用するための基本的な側面を示します。 モデルバインドを使用すると、データの相互作用がより簡単になり-...
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 7ef664b3-1cc8-4cbf-bb18-9f0f3a3ada2b
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/adding-business-logic-layer
msc.type: authoredcontent
ms.openlocfilehash: a824d06d3781e11706f2a48d44ea3ad89bdb7c8b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78515428"
---
# <a name="adding-business-logic-layer-to-a-project-that-uses-model-binding-and-web-forms"></a>モデルバインドと web フォームを使用するプロジェクトへのビジネスロジック層の追加

によって[Tom FitzMacken](https://github.com/tfitzmac)

> このチュートリアルシリーズでは、ASP.NET Web フォームプロジェクトでモデルバインドを使用するための基本的な側面を示します。 モデルバインドを使用すると、データソースオブジェクト (ObjectDataSource や SqlDataSource など) を処理するよりも、データ操作がより簡単になります。 このシリーズでは、入門資料から開始し、以降のチュートリアルでより高度な概念に移ります。
> 
> このチュートリアルでは、ビジネスロジック層でモデルバインドを使用する方法について説明します。 現在のページ以外のオブジェクトを使用してデータメソッドを呼び出すように指定するには、OnCallingDataMethods メンバーを設定します。
> 
> このチュートリアルは、シリーズの[前](retrieving-data.md)のパートで作成したプロジェクトに基づいています。
> 
> 完全なプロジェクトは、またはC# VB で[ダウンロード](https://go.microsoft.com/fwlink/?LinkId=286116)できます。 ダウンロード可能なコードは、Visual Studio 2012 または Visual Studio 2013 で動作します。 このチュートリアルでは、Visual Studio 2012 テンプレートを使用します。これは、このチュートリアルで示した Visual Studio 2013 テンプレートとは少し異なります。

## <a name="what-youll-build"></a>ビルドする内容

モデルバインドを使用すると、web ページの分離コードファイルまたは別のビジネスロジッククラスにデータの相互作用コードを配置できます。 前のチュートリアルでは、分離コードファイルを使用してデータ相互作用コードを記述する方法を説明しました。 この方法は小規模なサイトに対しては機能しますが、大規模なサイトを維持する場合は、コードの繰り返しにより困難になる可能性があります。 また、抽象化レイヤーが存在しないため、分離コードファイルに存在するコードをプログラムによってテストするのは非常に困難です。

データ相互作用コードを一元化するために、データと対話するためのすべてのロジックを含むビジネスロジック層を作成できます。 次に、web ページからビジネスロジックレイヤーを呼び出します。 このチュートリアルでは、前のチュートリアルで作成したすべてのコードをビジネスロジックレイヤーに移動し、そのコードをページから使用する方法について説明します。

このチュートリアルでは、次のことについて説明します。

1. 分離コードファイルからビジネスロジック層にコードを移動する
2. ビジネスロジック層のメソッドを呼び出すようにデータバインドコントロールを変更します。

## <a name="create-business-logic-layer"></a>ビジネスロジックレイヤーの作成

次に、web ページから呼び出されるクラスを作成します。 このクラスのメソッドは、前のチュートリアルで使用したメソッドに似ており、値プロバイダー属性が含まれています。

まず、 **BLL**という名前の新しいフォルダーを追加します。

![フォルダーの追加](adding-business-logic-layer/_static/image1.png)

[BLL] フォルダーで、 **SchoolBL.cs**という名前の新しいクラスを作成します。 これには、分離コードファイルにもともと存在していたすべてのデータ操作が含まれます。 メソッドは分離コードファイルのメソッドとほぼ同じですが、いくつかの変更が含まれます。

注意する必要がある最も重要な変更は、 **Page**クラスのインスタンス内からコードを実行しなくなったことです。 Page クラスには、 **TryUpdateModel**メソッドと**modelstate**プロパティが含まれています。 このコードをビジネスロジック層に移動すると、これらのメンバーを呼び出すためのページクラスのインスタンスがなくなります。 この問題を回避するには、TryUpdateModel または ModelState にアクセスするすべてのメソッドに**Modelmethodcontext**パラメーターを追加する必要があります。 この ModelMethodContext パラメーターを使用して TryUpdateModel を呼び出すか、ModelState を取得します。 この新しいパラメーターを考慮するために、web ページ内の何も変更する必要はありません。

SchoolBL.cs のコードを次のコードに置き換えます。

[!code-csharp[Main](adding-business-logic-layer/samples/sample1.cs)]

## <a name="revise-existing-pages-to-retrieve-data-from-business-logic-layer"></a>既存のページを更新してビジネスロジックレイヤーからデータを取得する

最後に、分離コードファイルのクエリを使用して、ビジネスロジックレイヤーを使用するように、ページの Student、AddStudent .aspx、および course を変換します。

Students、AddStudent、および course の分離コードファイルで、次のクエリメソッドを削除またはコメントアウトします。

- studentsGrid\_GetData
- studentsGrid\_UpdateItem
- studentsGrid\_DeleteItem
- addStudentForm\_InsertItem
- coursesGrid\_GetData

データ操作に関連するコードが分離コードファイルにないはずです。

**OnCallingDataMethods**イベントハンドラーを使用すると、データメソッドに使用するオブジェクトを指定できます。 Student で、そのイベントハンドラーの値を追加し、ビジネスロジッククラスのメソッドの名前にデータメソッドの名前を変更します。

[!code-aspx[Main](adding-business-logic-layer/samples/sample2.aspx?highlight=3-4,8)]

Student の分離コードファイルで、CallingDataMethods イベントのイベントハンドラーを定義します。 このイベントハンドラーでは、データ操作のビジネスロジッククラスを指定します。

[!code-csharp[Main](adding-business-logic-layer/samples/sample3.cs)]

AddStudent .aspx で、同様の変更を行います。

[!code-aspx[Main](adding-business-logic-layer/samples/sample4.aspx?highlight=3-4)]

[!code-csharp[Main](adding-business-logic-layer/samples/sample5.cs)]

Course .aspx で、同様の変更を行います。

[!code-aspx[Main](adding-business-logic-layer/samples/sample6.aspx?highlight=3-4)]

[!code-csharp[Main](adding-business-logic-layer/samples/sample7.cs)]

アプリケーションを実行して、すべてのページが以前と同じように機能することを確認します。 検証ロジックも正常に機能します。

## <a name="conclusion"></a>まとめ

このチュートリアルでは、データアクセス層とビジネスロジック層を使用するようにアプリケーションを再構築します。 データ操作の現在のページではないオブジェクトをデータコントロールが使用するように指定しました。

> [!div class="step-by-step"]
> [前へ](using-query-string-values-to-retrieve-data.md)
