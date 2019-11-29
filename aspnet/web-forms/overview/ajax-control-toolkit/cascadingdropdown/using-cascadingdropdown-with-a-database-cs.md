---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-cascadingdropdown-with-a-database-cs
title: CascadingDropDown をデータベース (C#) と共に使用するMicrosoft Docs
author: wenz
description: AJAX コントロールツールキットの CascadingDropDown コントロールは、dropdownlist コントロールを拡張して、1つの DropDownList の変更によって anoth に関連付けられた値が読み込まれるようにします。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 684f0c28-a490-4e5b-b5e5-5dfb77464b49
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-cascadingdropdown-with-a-database-cs
msc.type: authoredcontent
ms.openlocfilehash: bcf453170d17807b4e3b2d2a8b545cba43139f89
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599776"
---
# <a name="using-cascadingdropdown-with-a-database-c"></a>データベースで CascadingDropDown を使用する (C#)

[Christian Wenz](https://github.com/wenz)別

[コードのダウンロード](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown1.cs.zip)または[PDF のダウンロード](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown1CS.pdf)

> AJAX コントロールツールキットの CascadingDropDown コントロールは、dropdownlist コントロールを拡張して、1つの DropDownList の変更によって別の DropDownList に関連付けられた値が読み込まれるようにします。 これを機能させるには、特別な web サービスを作成する必要があります。

## <a name="overview"></a>の概要

AJAX コントロールツールキットの CascadingDropDown コントロールは、dropdownlist コントロールを拡張して、1つの DropDownList の変更によって別の DropDownList に関連付けられた値が読み込まれるようにします。 (たとえば、1つのリストに米国の州の一覧が表示され、その州の主要都市が次の一覧に入力されます)。これを機能させるには、特別な web サービスを作成する必要があります。

## <a name="steps"></a>手順

まず、データソースが必要です。 このサンプルでは、AdventureWorks データベースと Microsoft SQL Server 2005 Express Edition を使用します。 このデータベースは、Visual Studio のインストール (express edition を含む) の省略可能な部分であり、 [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064)で個別にダウンロードすることもできます。 AdventureWorks データベースは SQL Server 2005 サンプルおよびサンプルデータベース ( [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;D isplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)) に含まれています。 データベースをセットアップする最も簡単な方法は、Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) を使用して、`AdventureWorks.mdf` データベースファイルをアタッチすることです。

このサンプルでは、SQL Server 2005 Express Edition のインスタンスが `SQLEXPRESS` 呼び出され、web サーバーと同じコンピューター上に存在することを前提としています。これは、既定のセットアップでもあります。 セットアップが異なる場合は、データベースの接続情報を調整する必要があります。

ASP.NET AJAX と Control Toolkit の機能をアクティブ化するには、ページの任意の場所に `ScriptManager` コントロールを配置する必要があります (&lt;`form`&gt; 要素内)。

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample1.aspx)]

次の手順では、2つの DropDownList コントロールが必要です。 このサンプルでは、AdventureWorks の仕入先と連絡先の情報を使用します。そのため、利用可能なベンダーの一覧と、利用可能な連絡先のリストを1つ作成します。

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample2.aspx)]

次に、2つの CascadingDropDown extender をページに追加する必要があります。 1つ目の (ベンダ) リストを入力し、もう1つは2番目 (連絡先) の一覧に入力します。 次の属性を設定する必要があります。

- `ServicePath`: リストエントリを提供する web サービスの URL
- `ServiceMethod`: リストエントリを配信する Web メソッド
- `TargetControlID`: ドロップダウンリストの ID
- `Category`: 呼び出されたときに web メソッドに送信されるカテゴリ情報
- `PromptText`: サーバーからリストデータを非同期的に読み込むときに表示されるテキスト
- `ParentControlID`: (省略可能) 現在のリストの読み込みをトリガーする親ドロップダウンリスト

使用するプログラミング言語によっては、問題の web サービスの名前が変わりますが、他のすべての属性値は同じです。 最初のドロップダウンリストの CascadingDropDown 要素は次のとおりです。

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample3.aspx)]

2番目のリストの制御エクステンダーは、`ParentControlID` 属性を設定する必要があります。これにより、ベンダリスト内のエントリを選択すると、連絡先リストに関連する要素の読み込みがトリガーされるようになります。

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample4.aspx)]

実際の作業は、次のように設定された web サービスで実行されます。 `[ScriptService]` 属性が使用されていることに注意してください。それ以外の場合、ASP.NET AJAX では、クライアント側のスクリプトコードから web メソッドにアクセスするための JavaScript プロキシを作成することはできません。

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample5.aspx)]

CascadingDropDown によって呼び出される web メソッドのシグネチャは次のとおりです。

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample6.cs)]

したがって、戻り値は、Control Toolkit によって定義される `CascadingDropDownNameValue` 型の配列である必要があります。 `GetVendors()` メソッドは非常に簡単に実装できます。コードは AdventureWorks データベースに接続し、最初の25個のベンダーにクエリを実行します。 `CascadingDropDownNameValue` コンストラクターの最初のパラメーターは、リストエントリのキャプション、2番目のパラメーターの値 (HTML の &lt;`option`&gt; 要素の値属性) です。 次にコードを示します。

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample7.cs)]

仕入先に関連付けられている連絡先を取得する (メソッド名: `GetContactsForVendor()`) のは少し複雑です。 まず、最初のドロップダウンリストで選択されているベンダーを特定する必要があります。 Control Toolkit は、そのタスクのヘルパーメソッドを定義します。 `ParseKnownCategoryValuesString()` メソッドは、ドロップダウンデータを含む `StringDictionary` 要素を返します。

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample8.cs)]

セキュリティ上の理由から、まずこのデータを検証する必要があります。 (最初の CascadingDropDown 要素の `Category` プロパティが `"Vendor"`) に設定されているため、ベンダエントリがある場合は、選択したベンダの ID を取得できます。

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample9.cs)]

メソッドの残りの部分は、非常に単純です。 ベンダーの ID は、その仕入先に関連付けられているすべての連絡先を取得する SQL クエリのパラメーターとして使用されます。 この場合も、メソッドは `CascadingDropDownNameValue`型の配列を返します。

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample10.cs)]

ASP.NET ページを読み込み、しばらくすると、仕入先リストに25個のエントリが格納されます。 1つのエントリを選択し、2番目のドロップダウンリストにデータが格納されていることを確認します。

[最初のリストが自動的に入力される ![](using-cascadingdropdown-with-a-database-cs/_static/image2.png)](using-cascadingdropdown-with-a-database-cs/_static/image1.png)

最初の一覧が自動的に入力されます ([クリックすると、フルサイズの画像が表示](using-cascadingdropdown-with-a-database-cs/_static/image3.png)されます)

[![2 番目のリストは、最初のリストの選択に従って塗りつぶされます。](using-cascadingdropdown-with-a-database-cs/_static/image5.png)](using-cascadingdropdown-with-a-database-cs/_static/image4.png)

2番目のリストは、最初のリストの選択に従って塗りつぶされます ([クリックすると、フルサイズの画像が表示](using-cascadingdropdown-with-a-database-cs/_static/image6.png)されます)。

> [!div class="step-by-step"]
> [前へ](filling-a-list-using-cascadingdropdown-cs.md)
> [次へ](presetting-list-entries-with-cascadingdropdown-cs.md)
