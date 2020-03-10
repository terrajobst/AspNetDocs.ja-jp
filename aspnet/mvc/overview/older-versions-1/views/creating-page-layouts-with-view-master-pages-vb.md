---
uid: mvc/overview/older-versions-1/views/creating-page-layouts-with-view-master-pages-vb
title: ビューマスターページを使用したページレイアウトの作成 (VB) |Microsoft Docs
author: microsoft
description: このチュートリアルでは、ビューのマスターページを利用して、アプリケーションの複数のページに共通のページレイアウトを作成する方法について説明します。 使用できる...
ms.author: riande
ms.date: 10/16/2008
ms.assetid: d34f90a1-6de3-482a-a326-f87fdcbaaaff
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-page-layouts-with-view-master-pages-vb
msc.type: authoredcontent
ms.openlocfilehash: 97c0ecf1953cc54030656dd710a5150243877110
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78435202"
---
# <a name="creating-page-layouts-with-view-master-pages-vb"></a>ビュー マスター ページでページ レイアウトを作成する (VB)

[Microsoft](https://github.com/microsoft)

[[Download PDF]\(PDF をダウンロード\)](https://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_12_VB.pdf)

> このチュートリアルでは、ビューのマスターページを利用して、アプリケーションの複数のページに共通のページレイアウトを作成する方法について説明します。 ビューマスターページを使用すると、たとえば、2列のページレイアウトを定義し、web アプリケーションのすべてのページに2列のレイアウトを使用することができます。

## <a name="creating-page-layouts-with-view-master-pages"></a>ビューマスターページを使用したページレイアウトの作成

このチュートリアルでは、ビューのマスターページを利用して、アプリケーションの複数のページに共通のページレイアウトを作成する方法について説明します。 ビューマスターページを使用すると、たとえば、2列のページレイアウトを定義し、web アプリケーションのすべてのページに2列のレイアウトを使用することができます。

また、ビューのマスターページを利用して、アプリケーション内の複数のページで共通のコンテンツを共有することもできます。 たとえば、web サイトのロゴ、ナビゲーションリンク、およびバナー広告をビューマスターページに配置できます。 これにより、アプリケーションのすべてのページにこのコンテンツが自動的に表示されるようになります。

このチュートリアルでは、新しいビューマスターページを作成し、マスターページに基づいて新しいビューコンテンツページを作成する方法について説明します。

### <a name="creating-a-view-master-page"></a>ビューマスターページの作成

まずは、2列のレイアウトを定義するビューマスターページを作成してみましょう。 MVC プロジェクトに新しいビューマスターページを追加するには、Views\Shared フォルダーを右クリックし、[追加] **、[新しい項目**] の順に選択して、mvc ビューのマスターページテンプレートを選択します (図1を参照)。

[ビューマスターページを追加 ![には](creating-page-layouts-with-view-master-pages-vb/_static/image2.png)](creating-page-layouts-with-view-master-pages-vb/_static/image1.png)

**図 01**: ビューマスターページを追加[する (クリックすると、フルサイズの画像が表示](creating-page-layouts-with-view-master-pages-vb/_static/image3.png)される)

アプリケーションでは、複数のビューマスターページを作成できます。 各ビューのマスターページでは、異なるページレイアウトを定義できます。 たとえば、特定のページに2列のレイアウトを設定し、他のページに3列のレイアウトを設定することができます。

ビューのマスターページは、標準の ASP.NET MVC ビューによく似ています。 ただし、通常のビューとは異なり、ビューのマスターページには `<asp:ContentPlaceHolder>` タグが1つ以上含まれています。 `<contentplaceholder>` タグは、個々のコンテンツページでオーバーライドできるマスターページの領域をマークするために使用されます。

たとえば、リスト1のビューマスターページでは、2列のレイアウトを定義します。 2つの `<contentplaceholder>` タグが含まれています。 列ごとに1つの `<ContentPlaceHolder>`。

**リスト1– `Views\Shared\Site.master`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample1.aspx)]

リスト1のビューマスターページの本文には、2つの列に対応する2つの `<div>` タグが含まれています。 カスケードスタイルシートの列クラスは、両方の `<div>` タグに適用されます。 このクラスは、マスターページの上部で宣言されているスタイルシートで定義されています。 デザインビューに切り替えると、ビューマスターページがどのように表示されるかをプレビューできます。 ソースコードエディターの左下にある [デザイン] タブをクリックします (図2を参照)。

[デザイナーでマスターページをプレビュー ![には](creating-page-layouts-with-view-master-pages-vb/_static/image5.png)](creating-page-layouts-with-view-master-pages-vb/_static/image4.png)

**図 02**: デザイナーでマスターページをプレビューする ([クリックすると、フルサイズの画像が表示](creating-page-layouts-with-view-master-pages-vb/_static/image6.png)されます)

### <a name="creating-a-view-content-page"></a>ビューコンテンツページを作成する

ビューマスターページを作成した後、ビューマスターページに基づいて1つまたは複数のビューコンテンツページを作成できます。 たとえば、Home コントローラーのインデックスビューコンテンツページを作成するには、Views\Home フォルダーを右クリックし、[**追加]、[新しい項目**] の順に選択して、 **MVC ビューコンテンツページ**テンプレートを選択し、「」と入力して、[追加] ボタンをクリックします (図3を参照)。

[ビューコンテンツページを追加 ![には](creating-page-layouts-with-view-master-pages-vb/_static/image8.png)](creating-page-layouts-with-view-master-pages-vb/_static/image7.png)

**図 03**: ビューコンテンツページを追加[する (クリックすると、フルサイズの画像が表示](creating-page-layouts-with-view-master-pages-vb/_static/image9.png)される)

[追加] ボタンをクリックすると、新しいダイアログが表示され、[ビューのコンテンツ] ページに関連付けるビューマスターページを選択できます (図4を参照)。 前のセクションで作成したサイトのマスタービューマスターページに移動できます。

[マスターページを選択 ![には](creating-page-layouts-with-view-master-pages-vb/_static/image11.png)](creating-page-layouts-with-view-master-pages-vb/_static/image10.png)

**図 04**: マスターページを選択[する (クリックすると、フルサイズの画像が表示](creating-page-layouts-with-view-master-pages-vb/_static/image12.png)される)

新しいビューコンテンツページを作成した後に、そのマスターページをリスト2で取得します。

**リスト2– `Views\Home\Index.aspx`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample2.aspx)]

このビューには、ビューマスターページの `<asp:ContentPlaceHolder>` 各タグに対応する `<asp:Content>` タグが含まれていることに注意してください。 各 `<asp:Content>` タグには、オーバーライドする特定の `<asp:ContentPlaceHolder>` を指す ContentPlaceHolderID 属性が含まれています。

さらに、リスト2の [コンテンツビュー] ページには、通常のオープンおよび終了 HTML タグは含まれていません。 たとえば、開始タグと終了 `<html>` タグや `<head>` タグは含まれません。 通常の開始タグと終了タグはすべて、ビューマスターページに含まれています。

ビューコンテンツページに表示するコンテンツは、`<asp:Content>` タグ内に配置する必要があります。 これらのタグの外側に HTML またはその他のコンテンツを配置すると、ページを表示しようとしたときにエラーが表示されます。

コンテンツビューページのマスターページから、すべての `<asp:ContentPlaceHolder>` タグをオーバーライドする必要はありません。 タグを特定のコンテンツに置き換える場合にのみ、`<asp:ContentPlaceHolder>` タグをオーバーライドする必要があります。

たとえば、リスト3の変更されたインデックスビューに含まれる `<asp:Content>` タグは2つだけです。 `<asp:Content>` の各タグには、いくつかのテキストが含まれています。

**リスト3– `Views\Home\Index.aspx (modified)`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample3.aspx)]

リスト3のビューが要求されると、図5のページが表示されます。 ビューでは、2つの列を含むページが表示されることに注意してください。 さらに、[ビューコンテンツ] ページのコンテンツがビューマスターページのコンテンツとマージされていることにも注意してください。

[インデックスビューのコンテンツページの ![](creating-page-layouts-with-view-master-pages-vb/_static/image14.png)](creating-page-layouts-with-view-master-pages-vb/_static/image13.png)

**図 05**: インデックスビューのコンテンツページ ([クリックすると、フルサイズの画像が表示](creating-page-layouts-with-view-master-pages-vb/_static/image15.png)されます)

### <a name="modifying-view-master-page-content"></a>ビューマスターページのコンテンツの変更

ビューのマスターページを操作するときにほぼ即座に発生する問題の1つは、異なるビューコンテンツページが要求されたときにビューマスターページのコンテンツを変更するという問題です。 たとえば、web アプリケーションの各ページに一意のタイトルを付けることができます。 ただし、タイトルはビューの [コンテンツ] ページではなく、ビューマスターページで宣言されています。 では、各ビューコンテンツページのページタイトルをカスタマイズするにはどうすればよいでしょうか。

ビューコンテンツページに表示されるタイトルを変更するには、2つの方法があります。 まず、ビューコンテンツページの上部で宣言されている `<%@ page %>` ディレクティブの title 属性にページタイトルを割り当てることができます。 たとえば、ページタイトル "Super 素晴らしい Web サイト" をインデックスビューに割り当てる場合は、インデックスビューの先頭に次のディレクティブを含めることができます。

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample4.aspx)]

インデックスビューがブラウザーに表示されると、ブラウザーのタイトルバーに必要なタイトルが表示されます。

[![ブラウザーのタイトルバー](creating-page-layouts-with-view-master-pages-vb/_static/image17.png)](creating-page-layouts-with-view-master-pages-vb/_static/image16.png)

Title 属性が機能するためには、マスタービューページが満たす必要のある重要な要件が1つあります。 ビューマスターページには、ヘッダーの通常の `<head>` タグではなく、`<head runat="server">` タグが含まれている必要があります。 `<head>` タグに runat = "server" 属性が含まれていない場合、タイトルは表示されません。 既定のビューマスターページには、必須の `<head runat="server">` タグが含まれています。

個々のビューコンテンツページからマスターページのコンテンツを変更する別の方法として、`<asp:ContentPlaceHolder>` タグで変更する領域をラップすることもできます。 たとえば、タイトルだけでなく、meta タグもマスタービューページによって表示されるように変更する場合を考えてみます。 リスト4のマスタービューページには、`<head>` タグ内の `<asp:ContentPlaceHolder>` タグが含まれています。

**リスト4– `Views\Shared\Site2.master`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample5.aspx)]

リスト4の `<asp:ContentPlaceHolder>` タグに既定のコンテンツ (既定のタイトルと既定のメタタグ) が含まれていることに注意してください。 個々のビューコンテンツページでこの `<asp:ContentPlaceHolder>` タグをオーバーライドしない場合、既定のコンテンツが表示されます。

リスト5の [コンテンツビュー] ページでは、カスタムタイトルとカスタムメタタグを表示するために `<asp:ContentPlaceHolder>` タグがオーバーライドされます。

**リスト5– `Views\Home\Index2.aspx`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample6.aspx)]

### <a name="summary"></a>まとめ

このチュートリアルでは、マスターページの表示とコンテンツページの表示の基本的な概要について説明しました。 新しいビューマスターページを作成し、それらに基づいてビューコンテンツページを作成する方法について学習しました。 また、特定のビューコンテンツページからビューマスターページのコンテンツを変更する方法についても説明します。

> [!div class="step-by-step"]
> [前へ](using-the-tagbuilder-class-to-build-html-helpers-vb.md)
> [次へ](passing-data-to-view-master-pages-vb.md)
