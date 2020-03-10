---
uid: web-forms/overview/ajax-control-toolkit/confirmbutton/using-a-confirmbutton-in-a-repeater-cs
title: リピータ (C#) で confirmbutton を使用するMicrosoft Docs
author: wenz
description: AJAX コントロールツールキットの ConfirmButton エクステンダーは、ユーザーがボタン (LinkButton コントロールを含む) をクリックしたときに、[はい/いいえ] ポップアップを作成します。 [はい] の場合のみ...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: a973ed3e-400c-4925-ace2-0b086b479301
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/confirmbutton/using-a-confirmbutton-in-a-repeater-cs
msc.type: authoredcontent
ms.openlocfilehash: 468a830f01c48dc39b22bc5d826f80533df65c1a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78446398"
---
# <a name="using-a-confirmbutton-in-a-repeater-c"></a>Repeater で ConfirmButton を使用する (C#)

[Christian Wenz](https://github.com/wenz)別

[コードのダウンロード](https://download.microsoft.com/download/8/6/d/86dea6c6-bb92-4fa6-aa14-f8c0f82100f5/ConfirmButton1.cs.zip)または[PDF のダウンロード](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/confirmbutton1CS.pdf)

> AJAX コントロールツールキットの ConfirmButton エクステンダーは、ユーザーがボタン (LinkButton コントロールを含む) をクリックしたときに、[はい/いいえ] ポップアップを作成します。 [はい] をクリックした場合にのみ、ボタンのアクションが実行されます。それ以外の場合は取り消されます。 これは、リピータでも可能です。

## <a name="overview"></a>概要

AJAX コントロールツールキットの ConfirmButton エクステンダーは、ユーザーがボタン (LinkButton コントロールを含む) をクリックしたときに、[はい/いいえ] ポップアップを作成します。 [はい] をクリックした場合にのみ、ボタンのアクションが実行されます。それ以外の場合は取り消されます。 これは、リピータでも可能です。

## <a name="steps"></a>手順

まず、データソースが必要です。 このサンプルでは、AdventureWorks データベースと Microsoft SQL Server 2005 Express Edition を使用します。 このデータベースは、Visual Studio のインストール (express edition を含む) の省略可能な部分であり、 [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064)で個別にダウンロードすることもできます。 AdventureWorks データベースは SQL Server 2005 サンプルおよびサンプルデータベース ( [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;D isplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)) に含まれています。 データベースをセットアップする最も簡単な方法は、Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) を使用して、`AdventureWorks.mdf` データベースファイルをアタッチすることです。

このサンプルでは、SQL Server 2005 Express Edition のインスタンスが `SQLEXPRESS` 呼び出され、web サーバーと同じコンピューター上に存在することを前提としています。これは、既定のセットアップでもあります。 セットアップが異なる場合は、データベースの接続情報を調整する必要があります。

ASP.NET AJAX と Control Toolkit の機能をアクティブ化するには、ページの任意の場所に `ScriptManager` コントロールを配置する必要があります (`<form>` 要素内)。

[!code-aspx[Main](using-a-confirmbutton-in-a-repeater-cs/samples/sample1.aspx)]

次に、データソースが必要です。 わかりやすくするために、AdventureWorks の [ベンダ] テーブルの最初の5つのエントリのみが取得されます。 Visual Studio ウィザードを使用してデータソースを作成する場合、テーブル名 (`Vendors`) の先頭には `Purchasing`が正しく付けられていないことに注意してください。 適切なマークアップは次のようになります。

[!code-aspx[Main](using-a-confirmbutton-in-a-repeater-cs/samples/sample2.aspx)]

このデータソースは、リピータ内で使用できます。 通常どおり、`DataBinder.Eval()` メソッドはデータソースからデータを取得します。 `ConfirmButtonExtender` コントロールは、データソース内のすべてのエントリに対して表示されるように、repeater の `<ItemTemplate>` セクション内に配置する必要があります。

[!code-aspx[Main](using-a-confirmbutton-in-a-repeater-cs/samples/sample3.aspx)]

[![データソースの各エントリの横に [確認] ボタンが表示されます。](using-a-confirmbutton-in-a-repeater-cs/_static/image2.png)](using-a-confirmbutton-in-a-repeater-cs/_static/image1.png)

データソースからの各エントリの横に [確認] ボタンが表示されます ([クリックすると、フルサイズの画像が表示](using-a-confirmbutton-in-a-repeater-cs/_static/image3.png)されます)

> [!div class="step-by-step"]
> [Next](using-a-confirmbutton-in-a-repeater-vb.md)
