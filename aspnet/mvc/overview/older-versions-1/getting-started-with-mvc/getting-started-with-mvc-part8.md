---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part8
title: モデルに列を追加する |Microsoft Docs
author: shanselman
description: これは、ASP.NET MVC の基本を紹介する初心者向けチュートリアルです。 データベースを読み書きする単純な web アプリケーションを作成します。
ms.author: riande
ms.date: 08/14/2010
ms.assetid: 7ae696b9-348f-4993-8ebb-a838acbe0c28
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part8
msc.type: authoredcontent
ms.openlocfilehash: 1cf092c3db3959d6f47006f1be2ba82833c5dc06
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78437224"
---
# <a name="adding-a-column-to-the-model"></a>モデルに列を追加する

[Scott マン Selman](https://github.com/shanselman)

> これは、ASP.NET MVC の基本を紹介する初心者向けチュートリアルです。 データベースを読み書きする単純な web アプリケーションを作成します。 他の ASP.NET MVC のチュートリアルとサンプルについては、 [ASP.NET mvc learning center](../../../index.md)を参照してください。

このセクションでは、データベースのスキーマに変更を加え、アプリケーション内で変更を処理する方法について説明します。

ムービーテーブルに "評価" 列を追加してみましょう。 IDE に戻り、[データベースエクスプローラー] をクリックします。 [ムービー] テーブルを右クリックし、[テーブル定義を開く] を選択します。

次に示すように "評価" 列を追加します。 現在評価がないため、列で null 値を許容できます。 [保存] をクリックします。

[ムービーテーブルの編集 ![](getting-started-with-mvc-part8/_static/image2.png)](getting-started-with-mvc-part8/_static/image1.png)

次に、ソリューションエクスプローラーに戻り、([モデル] フォルダー内の) .edmx ファイルを開きます。 デザイン画面 (白い部分) を右クリックし、[データベースからモデルを更新] を選択します。

[![映画-Microsoft Visual Web Developer 2010 Express (11)](getting-started-with-mvc-part8/_static/image4.png)](getting-started-with-mvc-part8/_static/image3.png)

これにより、"更新ウィザード" が起動します。 その中の [更新] タブをクリックし、[完了] をクリックします。 次に、ムービーモデルクラスが新しい列で更新されます。

![更新ウィザード (2)](getting-started-with-mvc-part8/_static/image5.png)

[完了] をクリックすると、モデルの Movie エンティティに新しい評価列が追加されていることがわかります。

[![Movie エンティティ](getting-started-with-mvc-part8/_static/image7.png)](getting-started-with-mvc-part8/_static/image6.png)

データベースモデルに列を追加しましたが、ビューで認識されません。

## <a name="update-views-with-model-changes"></a>モデルの変更によるビューの更新

新しい評価列を反映するようにビューテンプレートを更新するには、いくつかの方法があります。 [ビューの追加] ダイアログでこれらのビューを生成して作成したため、これらのビューを削除して再作成することができます。 ただし、通常、ユーザーは最初のスキャフォールディング生成からビューテンプレートを変更しています。また、Create の ID フィールドの場合と同様に、フィールドを手動で追加または削除する必要があります。

\Views\Movies\Index.aspx テンプレートを開き、&lt;th&gt;評価&lt;/th&gt; をムービーテーブルの先頭に追加します。 ジャンルの後に自分のものを追加しました。 次に、同じ列の位置で下に移動し、新しい評価を出力する行を追加します。

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample1.aspx)]

最後のインデックス .aspx テンプレートは次のようになります。

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample2.aspx)]

次に、\Views\Movies\Create.aspx テンプレートを開き、新しい評価プロパティのラベルとテキストボックスを追加します。

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample3.aspx)]

最終的に作成された .aspx テンプレートは次のようになります。ブラウザーのタイトルとセカンダリ &lt;h2&gt; タイトルは、ここで説明しているように "ムービーの作成" のように変更してみましょう。

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample4.aspx)]

アプリを実行すると、[作成] ページに追加された新しいフィールドがデータベースに追加されました。 新しいムービーを追加します。今回は評価付きで、[作成] をクリックします。

[ムービーを作成 ![には-Windows Internet Explorer](getting-started-with-mvc-part8/_static/image9.png)](getting-started-with-mvc-part8/_static/image8.png)

[作成] をクリックすると、新しいムービーがデータベースの新しい評価列と共に一覧表示されるインデックスページに送信されます。

[![ムービーの一覧-Windows Internet Explorer (12)](getting-started-with-mvc-part8/_static/image11.png)](getting-started-with-mvc-part8/_static/image10.png)

この基本的なチュートリアルでは、コントローラーの作成と、それらをビューに関連付け、ハードコーディングされたデータを使用する方法について見てきました。 次に、データベースを作成してデザインし、データを格納します。 データベースからデータを取得し、HTML テーブルに表示しました。 その後、ユーザーが Web アプリケーション内からデータベース自体にデータを追加できるようにする Create フォームを追加しました。 検証を追加し、クライアント側で検証を使用するようにしました。 最後に、データの新しい列が含まれるようにデータベースを変更し、この新しいデータを作成して表示するように2つのページを更新しました。

ここでは、中級者向けのチュートリアル「[Mvc Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)」、および[https://asp.net/mvc](https://asp.net/mvc)にある多くのビデオとリソースを参照して、ASP.NET MVC についてさらに詳しく学習することをお勧めします。

機能を有効にご活用ください。

- Scott マン Selman- [http://hanselman.com](http://hanselman.com) 、Twitter で[@shanselman](http://twitter.com/shanselman)ます。

> [!div class="step-by-step"]
> [[戻る]](getting-started-with-mvc-part7.md)
