---
uid: web-forms/overview/ajax-control-toolkit/hovermenu/using-hovermenu-with-a-repeater-control-vb
title: Repeater コントロールで HoverMenu を使用する (VB) |Microsoft Docs
author: wenz
description: AJAX コントロールツールキットの HoverMenu コントロールは、単純なポップアップ効果を提供します。マウスポインターが要素の上に置かれると、ポップアップが specifi に表示されます。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 7f07c112-cd4f-4427-9699-57cfab2791fd
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/hovermenu/using-hovermenu-with-a-repeater-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 9386aa2fe3a6174bbed52218337107733cb1fa99
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74606649"
---
# <a name="using-hovermenu-with-a-repeater-control-vb"></a>Repeater コントロールで HoverMenu を使用する (VB)

[Christian Wenz](https://github.com/wenz)別

[コードのダウンロード](https://download.microsoft.com/download/b/0/6/b06fe835-5b8f-4c00-aef8-062c19d75b95/HoverMenu1.vb.zip)または[PDF のダウンロード](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/hovermenu1VB.pdf)

> AJAX コントロールツールキットの HoverMenu コントロールは、単純なポップアップ効果を提供します。マウスポインターが要素の上に置かれると、ポップアップが指定した位置に表示されます。 リピータ内でこのコントロールを使用することもできます。

## <a name="overview"></a>の概要

AJAX コントロールツールキットの `HoverMenu` コントロールは、単純なポップアップ効果を提供します。マウスポインターが要素の上に移動すると、指定した位置にポップアップが表示されます。 リピータ内でこのコントロールを使用することもできます。

## <a name="steps"></a>手順

まず、データソースが必要です。 このサンプルでは、AdventureWorks データベースと Microsoft SQL Server 2005 Express Edition を使用します。 このデータベースは、Visual Studio のインストール (express edition を含む) の省略可能な部分であり、 [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064)で個別にダウンロードすることもできます。 AdventureWorks データベースは SQL Server 2005 サンプルおよびサンプルデータベース ( [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;D isplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)) に含まれています。 データベースをセットアップする最も簡単な方法は、Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) を使用して、`AdventureWorks.mdf` データベースファイルをアタッチすることです。

このサンプルでは、SQL Server 2005 Express Edition のインスタンスが `SQLEXPRESS` 呼び出され、web サーバーと同じコンピューター上に存在することを前提としています。これは、既定のセットアップでもあります。 セットアップが異なる場合は、データベースの接続情報を調整する必要があります。

ASP.NET AJAX と Control Toolkit の機能をアクティブ化するには、ページの任意の場所に `ScriptManager` コントロールを配置する必要があります (`<form>` 要素内)。

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-vb/samples/sample1.aspx)]

次に、データソースをページに追加します。 限られた量のデータを使用するために、AdventureWorks データベースの Vendor テーブルの最初の5つのエントリのみを選択します。 Visual Studio アシスタントを使用してデータソースを作成する場合は、現在のバージョンのバグによって、テーブル名 (`Vendor`) のプレフィックスが `Purchasing`になっていないことに注意してください。 次のマークアップは、正しい構文を示しています。

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-vb/samples/sample2.aspx)]

次に、モーダルポップアップとして機能するパネルを追加します。

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-vb/samples/sample3.aspx)]

これで、`HoverMenuExtender` が登場します。 データソース内のすべての要素が独自のポップアップを取得できるように、extender はリピータの `<ItemTemplate>` セクション内に配置する必要があります。 マークアップは次のとおりです。

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-vb/samples/sample4.aspx)]

データソース内のすべてのアイテムは、50ミリ秒 (`PopDelay` 属性) の遅延の後に右側 (`PopupPosition` 属性) のポップアップを表示するようになりました。

[リピータの各項目の横にホバーメニューが表示される ![](using-hovermenu-with-a-repeater-control-vb/_static/image2.png)](using-hovermenu-with-a-repeater-control-vb/_static/image1.png)

リピータの各項目の横に、ホバーメニューが表示されます ([クリックすると、フルサイズの画像が表示](using-hovermenu-with-a-repeater-control-vb/_static/image3.png)されます)

> [!div class="step-by-step"]
> [前へ](using-hovermenu-with-a-repeater-control-cs.md)
