---
uid: web-forms/overview/ajax-control-toolkit/accordion/databinding-to-an-accordion-cs
title: アコーディオン (C#) にデータバインドするMicrosoft Docs
author: wenz
description: AJAX コントロールツールキットのアコーディオンコントロールは、複数のウィンドウを提供し、ユーザーが一度に1つずつ表示できるようにします。 通常、パネルは...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 9c8f0054-e319-46f8-80c0-35b606d2fbd4
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/accordion/databinding-to-an-accordion-cs
msc.type: authoredcontent
ms.openlocfilehash: 6c28cc958a1de9844627ae16175a5aed153993a8
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74607272"
---
# <a name="databinding-to-an-accordion-c"></a>アコーディオンにデータバインドする (C#)

[Christian Wenz](https://github.com/wenz)別

[コードのダウンロード](https://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion1.cs.zip)または[PDF のダウンロード](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion1CS.pdf)

> AJAX コントロールツールキットのアコーディオンコントロールは、複数のウィンドウを提供し、ユーザーが一度に1つずつ表示できるようにします。 通常、パネルはページ内で宣言されますが、データソースへのバインドにより柔軟性が向上します。

## <a name="overview"></a>の概要

AJAX コントロールツールキットのアコーディオンコントロールは、複数のウィンドウを提供し、ユーザーが一度に1つずつ表示できるようにします。 通常、パネルはページ内で宣言されますが、データソースへのバインドにより柔軟性が向上します。

## <a name="steps"></a>手順

まず、データソースが必要です。 このサンプルでは、AdventureWorks データベースと Microsoft SQL Server 2005 Express Edition を使用します。 このデータベースは、Visual Studio のインストール (express edition を含む) の省略可能な部分であり、 [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064)で個別にダウンロードすることもできます。 AdventureWorks データベースは SQL Server 2005 サンプルおよびサンプルデータベース ( [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;D isplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)) に含まれています。 データベースをセットアップする最も簡単な方法は、Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) を使用して、`AdventureWorks.mdf` データベースファイルをアタッチすることです。

このサンプルでは、SQL Server 2005 Express Edition のインスタンスが `SQLEXPRESS` 呼び出され、web サーバーと同じコンピューター上に存在することを前提としています。これは、既定のセットアップでもあります。 セットアップが異なる場合は、データベースの接続情報を調整する必要があります。

ASP.NET AJAX と Control Toolkit の機能をアクティブ化するには、ページの任意の場所に `ScriptManager` コントロールを配置する必要があります (`<form>` 要素内)。

[!code-aspx[Main](databinding-to-an-accordion-cs/samples/sample1.aspx)]

次に、データソースをページに追加します。 限られた量のデータを使用するために、AdventureWorks データベースの Vendor テーブルの最初の5つのエントリのみを選択します。 Visual Studio アシスタントを使用してデータソースを作成する場合は、現在のバージョンのバグによって、テーブル名 (`Vendor`) のプレフィックスが `Purchasing`になっていないことに注意してください。 次のマークアップは、正しい構文を示しています。

[!code-aspx[Main](databinding-to-an-accordion-cs/samples/sample2.aspx)]

データソースの名前 (ID) を記憶します。 このような識別情報は、アコーディオンコントロールの `DataSourceID` プロパティで使用する必要があります。

[!code-aspx[Main](databinding-to-an-accordion-cs/samples/sample3.aspx)]

アコーディオンコントロール内では、ヘッダー (`<HeaderTemplate>`) やコンテンツ (`<ContentTemplate>`) など、コントロールのさまざまな部分のテンプレートを提供できます。 これらの要素内では、`DataBinder.Eval()` メソッドを使用して、データソースからデータを出力するだけです。

[!code-aspx[Main](databinding-to-an-accordion-cs/samples/sample4.aspx)]

ページが読み込まれたら、次のサーバー側コードを使用してデータソースをアコーディオンにバインドする必要があります。

[!code-aspx[Main](databinding-to-an-accordion-cs/samples/sample5.aspx)]

このサンプルを終了するには、アコーディオンコントロールで参照される2つの CSS クラス (プロパティ `HeaderCssClass` と `ContentCssClass`) を定義する必要があります。 次のマークアップを、ページの `<head>` セクションに配置します。

[!code-css[Main](databinding-to-an-accordion-cs/samples/sample6.css)]

[データソースから直接、アコーディオン内のデータを取得 ![](databinding-to-an-accordion-cs/_static/image2.png)](databinding-to-an-accordion-cs/_static/image1.png)

アコーディオン内のデータはデータソースから直接取得されます ([クリックすると、フルサイズの画像が表示](databinding-to-an-accordion-cs/_static/image3.png)されます)

> [!div class="step-by-step"]
> [次へ](dynamically-adding-an-accordion-pane-cs.md)
