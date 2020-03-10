---
uid: web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-cs
title: AJAX Control Toolkit (C#) を使ってみる |Microsoft Docs
author: microsoft
description: AJAX Control Toolkit の使用を開始するために知っておく必要があることについて説明します。
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 16dc5c11-65be-4eae-a818-9fad7f8259c6
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-cs
msc.type: authoredcontent
ms.openlocfilehash: 7478b090ec52778572d70065983de6be8bdb4e6b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78504088"
---
# <a name="get-started-with-the-ajax-control-toolkit-c"></a>AJAX Control Toolkit の概要 (C#)

[Microsoft](https://github.com/microsoft)

> AJAX Control Toolkit の使用を開始するために知っておく必要があることについて説明します。

AJAX Control Toolkit には、ASP.NET アプリケーションで使用できる30を超える無料のコントロールが含まれています。 このチュートリアルでは、AJAX Control Toolkit をダウンロードし、Visual Studio/Visual Web Developer Express ツールボックスにツールキットコントロールを追加する方法について説明します。

## <a name="downloading-the-ajax-control-toolkit"></a>AJAX Control Toolkit のダウンロード

[AJAX Control Toolkit](http://devexpress.com/act)は、ASP.NET コミュニティと ASP.NET チームのメンバーによって開発されたオープンソースプロジェクトです。 

[AJAX Control Toolkit のダウンロード ![](get-started-with-the-ajax-control-toolkit-cs/_static/image1.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image1.png)

**図 01**: AJAX コントロールツールキットをダウンロード[する (クリックすると、フルサイズのイメージが表示](get-started-with-the-ajax-control-toolkit-cs/_static/image2.png)されます)

ファイルをダウンロードしたら、ファイルのブロックを解除する必要があります。 ファイルを右クリックして プロパティ を選択し、**ブロック解除** ボタンをクリックします (図2を参照)。

[AJAX Control Toolkit ZIP ファイルのブロックを解除 ![](get-started-with-the-ajax-control-toolkit-cs/_static/image2.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image3.png)

**図 02**: AJAX コントロールツールキットの ZIP ファイルのブロック解除 ([クリックすると、フルサイズのイメージが表示](get-started-with-the-ajax-control-toolkit-cs/_static/image4.png)されます)

ファイルのブロックを解除した後、ファイルを右クリックして **[すべて展開]** メニューオプションを選択すると、ファイルを解凍できます。 これで、ツールキットを Visual Studio/Visual Web Developer ツールボックスに追加する準備ができました。

## <a name="adding-the-ajax-control-toolkit-to-the-toolbox"></a>ツールボックスへの AJAX コントロールツールキットの追加

AJAX コントロールツールキットを使用する最も簡単な方法は、ツールキットを Visual Studio/Visual Web Developer ツールボックスに追加することです (図3を参照)。 これにより、ツールキットコントロールを使用するときに、単にそのページにドラッグできるようになります。

[![AJAX コントロールツールキットがツールボックスに表示される](get-started-with-the-ajax-control-toolkit-cs/_static/image3.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image5.png)

**図 03**: AJAX コントロールツールキットがツールボックスに表示される ([クリックしてフルサイズのイメージを表示する](get-started-with-the-ajax-control-toolkit-cs/_static/image6.png))

まず、AJAX Control Toolkit タブをツールボックスに追加する必要があります。 次の手順に従います。

1. 新しい ASP.NET Web サイトを作成するには、メニューオプションファイル [新しい Web サイト] を選択します。 [ソリューションエクスプローラー] ウィンドウで default.aspx をダブルクリックして、エディターでファイルを開きます。
2. 全般 タブの下にあるツールボックスを右クリックし、メニューオプション **タブの追加** を選択します (図4を参照)。
3. 「AJAX Control Toolkit」という名前の新しいタブを入力します。

[新しいタブを追加 ![には](get-started-with-the-ajax-control-toolkit-cs/_static/image4.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image7.png)

**図 04**: 新しいタブを追加[する (クリックすると、フルサイズの画像が表示](get-started-with-the-ajax-control-toolkit-cs/_static/image8.png)される)

次に、AJAX Control Toolkit コントロールを新しいタブに追加する必要があります。次の手順を実行します。

- [AJAX Control Toolkit] タブの下を右クリックし、[項目の選択] メニューオプションを選択します **(図5を参照)** 。
- AJAX コントロールツールキットを解凍した場所を参照し、AjaxControlToolkit アセンブリを選択します。

[ツールボックスに追加する項目を選択 ![には](get-started-with-the-ajax-control-toolkit-cs/_static/image5.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image9.png)

**図 05**: ツールボックスに追加する項目を選択する ([クリックすると、フルサイズの画像が表示](get-started-with-the-ajax-control-toolkit-cs/_static/image10.png)されます)

これらの手順を完了すると、すべてのツールキットコントロールがツールボックスに表示されます。

## <a name="upgrading-to-a-new-version-of-the-toolkit"></a>新しいバージョンの Toolkit へのアップグレード

以前のリリースの Toolkit を使用していて、今後のバージョンに移行する必要がある場合は、次の手順を実行することをお勧めします。

- バイナリ-web サイトの Bin フォルダーから古いバージョンの AjaxControlToolkit アセンブリを削除します。
- ツールボックスアイテム-AJAX Control Toolkit タブを削除し、上記の手順に従って、新しいバージョンの AjaxControlToolkit アセンブリを使用してタブを再作成します。

> [!div class="step-by-step"]
> [Next](using-ajax-control-toolkit-controls-and-control-extenders-cs.md)
