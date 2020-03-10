---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part4
title: データベースを作成する |Microsoft Docs
author: shanselman
description: これは、ASP.NET MVC の基本を紹介する初心者向けチュートリアルです。 データベースを読み書きする単純な web アプリケーションを作成します。
ms.author: riande
ms.date: 08/14/2010
ms.assetid: 742df67f-484d-4ef3-af6b-8c791e556b43
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part4
msc.type: authoredcontent
ms.openlocfilehash: 995db714ce6365415d06dc458aee84a31c7c8fd6
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78469672"
---
# <a name="creating-a-database"></a>データベースを作成します。

[Scott マン Selman](https://github.com/shanselman)

> これは、ASP.NET MVC の基本を紹介する初心者向けチュートリアルです。 データベースを読み書きする単純な web アプリケーションを作成します。 他の ASP.NET MVC のチュートリアルとサンプルについては、 [ASP.NET mvc learning center](../../../index.md)を参照してください。

このセクションでは、ムービーデータを格納および取得するために使用する新しい SQL Express データベースを作成します。 Visual Web Developer IDE 内から、[表示] を選択します。サーバー エクスプローラー。 [データ接続] を右クリックし、[接続の追加] をクリックします。

![AddConnection](getting-started-with-mvc-part4/_static/image1.png)

データソースの選択 ダイアログで、Microsoft SQL Server を選択し、続行 を選択します。

![](getting-started-with-mvc-part4/_static/image2.png)

[接続の追加] ダイアログボックスで、サーバー名として「.\SQLEXPRESS」と入力し、新しいデータベースの名前として「ムービー」と入力します。

[[接続の追加] ダイアログ ![](getting-started-with-mvc-part4/_static/image4.png)](getting-started-with-mvc-part4/_static/image3.png)

[OK] をクリックすると、そのデータベースを作成するかどうかを確認するメッセージが表示されます。 [はい] を選択します。

[ムービーを作成 ![には](getting-started-with-mvc-part4/_static/image6.png)](getting-started-with-mvc-part4/_static/image5.png)

サーバーエクスプローラーに空のデータベースが作成されました。

![新しいテーブルの追加](getting-started-with-mvc-part4/_static/image7.png)

テーブルを右クリックし、[テーブルの追加] をクリックします。 テーブルデザイナーが表示されます。 Id、タイトル、ReleaseDate、Genre、および Price の列を追加します。 [ID] 列を右クリックし、[主キーの設定] をクリックします。 デザイン領域は次のようになります。

[![データベーステーブルエディター](getting-started-with-mvc-part4/_static/image9.png)](getting-started-with-mvc-part4/_static/image8.png)

また、[Id] 列を選択し、[列のプロパティ] の下にある [Identity Specification] を [Yes] に変更します。

[![IsIdentity のプロパティ](getting-started-with-mvc-part4/_static/image11.png)](getting-started-with-mvc-part4/_static/image10.png)

完了したら、ツールバーの [保存] アイコンをクリックするか、[ファイル] を選択します。メニューから [保存] を指定し、テーブルに "**Movie**" という名前を付けます (単数形)。 データベースとテーブルがあります。

[![名の選択](getting-started-with-mvc-part4/_static/image13.png)](getting-started-with-mvc-part4/_static/image12.png)

サーバーエクスプローラーに戻り、Movie テーブルを右クリックして、[テーブルデータの表示] を選択します。 いくつかのムービーを入力すると、データベースにいくつかのデータが含まれます。

[![データベーステーブルの編集](getting-started-with-mvc-part4/_static/image15.png)](getting-started-with-mvc-part4/_static/image14.png)

## <a name="creating-a-model"></a>モデルの作成

次に、IDE の右側にあるソリューションエクスプローラーに戻り、[モデル] フォルダーを右クリックして [追加] を選択します。新しい項目。

[addnewmodelitem の ![](getting-started-with-mvc-part4/_static/image17.png)](getting-started-with-mvc-part4/_static/image16.png)

ここでは、新しいデータベースからエンティティモデルを作成します。 これにより、一連のクラスがプロジェクトに追加され、データベース内のデータを簡単に照会して操作できるようになります。 ダイアログの左側にある [データ] ノードを選択し、ADO.NET Entity Data Model 項目テンプレートを選択します。 「ムービー .edmx」という名前を指定します。

[![AddNewDataModel](getting-started-with-mvc-part4/_static/image19.png)](getting-started-with-mvc-part4/_static/image18.png)

[追加] ボタンをクリックします。 これにより、"Entity Data Model ウィザード" が起動します。

ポップアップ表示された新しいダイアログボックスで、[データベースから生成] を選択します。 データベースを作成したばかりなので、新しいデータベースとそのテーブルに関する Entity Framework についてのみ説明します。 [次へ] をクリックして、web アプリケーションの構成にデータベース接続を保存します。 次に、[テーブルとムービー] チェックボックスをオンにして、[完了] をクリックします。

[![Entity Data Model ウィザード](getting-started-with-mvc-part4/_static/image21.png)](getting-started-with-mvc-part4/_static/image20.png)

これで、Entity Framework Designer に新しいムービーテーブルが表示され、コードからアクセスできるようになりました。

[![映画-Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part4/_static/image23.png)](getting-started-with-mvc-part4/_static/image22.png)

デザイン画面には、"Movie" クラスが表示されます。 このクラスは、データベースの "Movie" テーブルにマップされ、その中の各プロパティはテーブルを含む列にマップされます。 "Movie" クラスの各インスタンスは、"Movie" テーブル内の行に対応します。

Entity Framework によって使用される既定の名前付け規則とマッピング規則が気に入らない場合は、Entity Framework デザイナーを使用して変更またはカスタマイズすることができます。 このアプリケーションでは、既定値を使用し、ファイルをそのまま保存します。

では、実際のデータを使用してみましょう。

> [!div class="step-by-step"]
> [前へ](getting-started-with-mvc-part3.md)
> [次へ](getting-started-with-mvc-part5.md)
