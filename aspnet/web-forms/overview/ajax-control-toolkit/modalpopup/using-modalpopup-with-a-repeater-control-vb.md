---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/using-modalpopup-with-a-repeater-control-vb
title: Repeater コントロールで ModalPopup を使用する (VB) |Microsoft Docs
author: wenz
description: AJAX コントロールツールキットの ModalPopup コントロールを使用すると、クライアント側の方法を使用してモーダルポップアップを簡単に作成できます。 また、次のものを使用することもできます...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 0c8e74f1-b3ba-4ca9-a1c5-f5c4831a359a
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/using-modalpopup-with-a-repeater-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 0966770f0218ca91ba7d25e7bf703bf7b005738e
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74606557"
---
# <a name="using-modalpopup-with-a-repeater-control-vb"></a>Repeater コントロールで ModalPopup を使用する (VB)

[Christian Wenz](https://github.com/wenz)別

[コードのダウンロード](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup2.vb.zip)または[PDF のダウンロード](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup2VB.pdf)

> AJAX コントロールツールキットの ModalPopup コントロールを使用すると、クライアント側の方法を使用してモーダルポップアップを簡単に作成できます。 リピータ内でこのコントロールを使用することもできます。

## <a name="overview"></a>の概要

AJAX コントロールツールキットの ModalPopup コントロールを使用すると、クライアント側の方法を使用してモーダルポップアップを簡単に作成できます。 リピータ内でこのコントロールを使用することもできます。

## <a name="steps"></a>手順

まず、データソースが必要です。 このサンプルでは、AdventureWorks データベースと Microsoft SQL Server 2005 Express Edition を使用します。 このデータベースは、Visual Studio のインストール (express edition を含む) の省略可能な部分であり、 [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064)で個別にダウンロードすることもできます。 AdventureWorks データベースは SQL Server 2005 サンプルおよびサンプルデータベース ( [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;D isplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)) に含まれています。 データベースをセットアップする最も簡単な方法は、Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) を使用して、`AdventureWorks.mdf` データベースファイルをアタッチすることです。 このサンプルでは、SQL Server 2005 Express Edition のインスタンスが `SQLEXPRESS` 呼び出され、web サーバーと同じコンピューター上に存在することを前提としています。これは、既定のセットアップでもあります。 セットアップが異なる場合は、データベースの接続情報を調整する必要があります。 ASP.NET AJAX と Control Toolkit の機能をアクティブ化するには、ページの任意の場所に `ScriptManager` コントロールを配置する必要があります (`<form>` 要素内)。

[!code-aspx[Main](using-modalpopup-with-a-repeater-control-vb/samples/sample1.aspx)]

次に、データソースをページに追加します。 限られた量のデータを使用するために、AdventureWorks データベースの Vendor テーブルの最初の5つのエントリのみを選択します。 Visual Studio アシスタントを使用してデータソースを作成する場合は、現在のバージョンのバグによって、テーブル名 (`Vendor`) のプレフィックスが `Purchasing`になっていないことに注意してください。 次のマークアップは、正しい構文を示しています。

[!code-aspx[Main](using-modalpopup-with-a-repeater-control-vb/samples/sample2.aspx)]

次に、モーダルポップアップとして機能するパネルを追加します。 ポップアップを再び閉じるための `Button` コントロールが含まれています。

[!code-aspx[Main](using-modalpopup-with-a-repeater-control-vb/samples/sample3.aspx)]

リピータ内でポップアップを機能させるには、`ModalPopupExtender` コントロールをリピータの `<ItemTemplate>` セクション内に配置する必要があります。 そのため、パネルはリピータの外側にありますが、extender は内側にあります。 リピータのマークアップを次に示します。

[!code-aspx[Main](using-modalpopup-with-a-repeater-control-vb/samples/sample4.aspx)]

次に、データソース内のすべての項目が、モーダルポップアップをトリガーするボタンと共に表示されます。

[データソースエントリごとにモーダルポップアップをトリガーできる ![](using-modalpopup-with-a-repeater-control-vb/_static/image2.png)](using-modalpopup-with-a-repeater-control-vb/_static/image1.png)

すべてのデータソースエントリに対してモーダルポップアップをトリガーできます ([クリックすると、フルサイズの画像が表示](using-modalpopup-with-a-repeater-control-vb/_static/image3.png)されます)

> [!div class="step-by-step"]
> [前へ](launching-a-modal-popup-window-from-server-code-vb.md)
> [次へ](handling-postbacks-from-a-modalpopup-vb.md)
