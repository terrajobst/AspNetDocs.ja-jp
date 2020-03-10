---
uid: web-forms/overview/older-versions-getting-started/master-pages/multiple-contentplaceholders-and-default-content-vb
title: 複数の ContentPlaceHolders と既定のコンテンツ (VB) |Microsoft Docs
author: rick-anderson
description: 複数のコンテンツプレースホルダーをマスターページに追加する方法と、コンテンツプレースホルダーで既定のコンテンツを指定する方法について説明します。
ms.author: riande
ms.date: 05/21/2008
ms.assetid: 866a7177-6884-451e-88f4-c934b1dd1af5
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/multiple-contentplaceholders-and-default-content-vb
msc.type: authoredcontent
ms.openlocfilehash: b71cacb143094dcc5cf483c69c2fcc0f10def51c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78461494"
---
# <a name="multiple-contentplaceholders-and-default-content-vb"></a>複数の ContentPlaceHolders と既定のコンテンツ (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[コードのダウンロード](https://download.microsoft.com/download/e/e/f/eef369f5-743a-4a52-908f-b6532c4ce0a4/ASPNET_MasterPages_Tutorial_02_VB.zip)または[PDF のダウンロード](https://download.microsoft.com/download/8/f/6/8f6349e4-6554-405a-bcd7-9b094ba5089a/ASPNET_MasterPages_Tutorial_02_VB.pdf)

> 複数のコンテンツプレースホルダーをマスターページに追加する方法と、コンテンツプレースホルダーで既定のコンテンツを指定する方法について説明します。

## <a name="introduction"></a>はじめに

前のチュートリアルでは、ASP.NET の開発者がマスターページを使用して、一貫性のあるサイト全体のレイアウトを作成する方法について説明します。 マスターページは、ページごとにカスタマイズ可能なすべてのコンテンツページと領域に共通するマークアップの両方を定義します。 前のチュートリアルでは、単純なマスターページ (`Site.master`) と2つのコンテンツページ (`Default.aspx` と `About.aspx`) を作成しました。 マスターページでは、`head` と `MainContent`という名前の2つの ContentPlaceHolders が構成されており、それぞれ `<head>` 要素と Web フォームに配置されていました。 コンテンツページにはそれぞれ2つのコンテンツコントロールがありますが、`MainContent`に対応するマークアップのみが指定されています。

`Site.master`の2つの ContentPlaceHolder コントロールによって判明したように、マスターページには複数の ContentPlaceHolders を含めることができます。 さらに、マスターページで、ContentPlaceHolder コントロールの既定のマークアップを指定することもできます。 コンテンツページでは、必要に応じて独自のマークアップを指定したり、既定のマークアップを使用したりすることができます。 このチュートリアルでは、マスターページでの複数のコンテンツコントロールの使用について説明し、ContentPlaceHolder コントロールで既定のマークアップを定義する方法を説明します。

## <a name="step-1-adding-additional-contentplaceholder-controls-to-the-master-page"></a>手順 1: マスターページへの ContentPlaceHolder コントロールの追加

多くの web サイトデザインには、ページごとにカスタマイズされた複数の領域が画面上に表示されます。 `Site.master`、前のチュートリアルで作成したマスターページには、`MainContent`という名前の Web フォーム内に1つの ContentPlaceHolder が含まれています。 具体的には、この ContentPlaceHolder は `mainContent` `<div>` 要素内にあります。

図1は、ブラウザーを使用して表示する場合の `Default.aspx` を示しています。 赤で囲まれた領域は、`MainContent`に対応するページ固有のマークアップです。

[丸で囲まれた領域は ![ページごとにカスタマイズ可能な領域を示しています。](multiple-contentplaceholders-and-default-content-vb/_static/image2.png)](multiple-contentplaceholders-and-default-content-vb/_static/image1.png)

**図 01**: 丸で囲まれた領域は、現在ページごとにカスタマイズ可能な領域を示します ([クリックすると、フルサイズの画像が表示](multiple-contentplaceholders-and-default-content-vb/_static/image3.png)されます)。

図1に示されている領域に加えて、レッスンおよびニュースセクションの下にある左側の列にページ固有の項目を追加する必要があると仮定します。 これを実現するには、マスターページに別の ContentPlaceHolder コントロールを追加します。 先に進むには、Visual Web Developer の `Site.master` マスターページを開き、ContentPlaceHolder コントロールをツールボックスから、ニュースセクションの後のデザイナーにドラッグします。 ContentPlaceHolder の `ID` を `LeftColumnContent`に設定します。

[マスターページの左側の列に ContentPlaceHolder コントロールを追加 ![には](multiple-contentplaceholders-and-default-content-vb/_static/image5.png)](multiple-contentplaceholders-and-default-content-vb/_static/image4.png)

**図 02**: マスターページの左の列に ContentPlaceHolder コントロールを追加する ([クリックすると、フルサイズの画像が表示](multiple-contentplaceholders-and-default-content-vb/_static/image6.png)されます)

マスターページへの `LeftColumnContent` ContentPlaceHolder の追加により、`ContentPlaceHolderID` が `LeftColumnContent`に設定されたコンテンツコントロールをページ単位で追加することにより、この領域のコンテンツをページ単位で定義できます。 このプロセスは、手順 2. で確認します。

## <a name="step-2-defining-content-for-the-new-contentplaceholder-in-the-content-pages"></a>手順 2: コンテンツページで新しい ContentPlaceHolder のコンテンツを定義する

Web サイトに新しいコンテンツページを追加すると、選択したマスターページの各 ContentPlaceHolder のコンテンツコントロールが、Visual Web Developer によってページに自動的に作成されます。 手順 1. でマスターページに `LeftColumnContent` ContentPlaceHolder を追加すると、新しい ASP.NET ページに3つのコンテンツコントロールが追加されます。

これを説明するために、`Site.master` マスターページにバインドされている `MultipleContentPlaceHolders.aspx` という名前のルートディレクトリに新しいコンテンツページを追加します。 Visual Web Developer は、次の宣言型マークアップを使用してこのページを作成します。

[!code-aspx[Main](multiple-contentplaceholders-and-default-content-vb/samples/sample1.aspx)]

コンテンツコントロールに、`MainContent` ContentPlaceHolders (`Content2`) を参照するコンテンツを入力します。 次に、次のマークアップを `Content3` コンテンツコントロール (`LeftColumnContent` ContentPlaceHolder を参照) に追加します。

[!code-html[Main](multiple-contentplaceholders-and-default-content-vb/samples/sample2.html)]

このマークアップを追加した後、ブラウザーを使用してページにアクセスします。 図3に示すように、`Content3` コンテンツコントロールに配置されているマークアップは、[ニュース] セクション (赤で囲まれています) の下の左の列に表示されます。 `Content2` に配置されたマークアップは、ページの右側の部分に表示されます (青色で囲まれています)。

[左の列 ![、ニュースセクションの下にページ固有のコンテンツが含まれるようになりました。](multiple-contentplaceholders-and-default-content-vb/_static/image8.png)](multiple-contentplaceholders-and-default-content-vb/_static/image7.png)

**図 03**: 左の列に、News セクションの下にページ固有のコンテンツが含まれるようになりました ([クリックしてフルサイズの画像を表示する](multiple-contentplaceholders-and-default-content-vb/_static/image9.png))

### <a name="defining-content-in-existing-content-pages"></a>定義 (既存のコンテンツページのコンテンツを)

新しいコンテンツページを作成すると、手順 1. で追加した ContentPlaceHolder コントロールが自動的に組み込まれます。 しかし、`About.aspx` と `Default.aspx` の2つの既存のコンテンツページは、`LeftColumnContent` ContentPlaceHolder のコンテンツコントロールを持っていません。 この2つの既存のページでこの ContentPlaceHolder の内容を指定するには、自分でコンテンツコントロールを追加する必要があります。

ほとんどの ASP.NET Web コントロールとは異なり、Visual Web Developer ツールボックスにはコンテンツコントロール項目は含まれません。 コンテンツコントロールの宣言型マークアップをソースビューに手動で入力できますが、デザインビューを使用する方が簡単で迅速です。 [`About.aspx`] ページを開き、デザインビューに切り替えます。 図4に示すように、`LeftColumnContent` ContentPlaceHolder がデザインビューに表示されます。マウスをポイントすると、"左 Columncontent (マスター)" というタイトルが表示されます。 タイトルに "Master" が含まれている場合は、この ContentPlaceHolder のページにコンテンツコントロールが定義されていないことを示します。 `MainContent`の場合のように、ContentPlaceHolder のコンテンツコントロールが存在する場合、タイトルは "*ContentPlaceHolderID* (Custom)" と表示されます。

`LeftColumnContent` ContentPlaceHolder のコンテンツコントロールを `About.aspx`に追加するには、ContentPlaceHolder のスマートタグを展開し、[カスタムコンテンツの作成] リンクをクリックします。

[![についてのデザインビューでは、左の Columncontent ContentPlaceHolder が表示されます。](multiple-contentplaceholders-and-default-content-vb/_static/image11.png)](multiple-contentplaceholders-and-default-content-vb/_static/image10.png)

**図 04**: `About.aspx` のデザインビューで `LeftColumnContent` ContentPlaceHolder が表示される ([クリックすると、フルサイズの画像が表示](multiple-contentplaceholders-and-default-content-vb/_static/image12.png)されます)

[カスタムコンテンツの作成] リンクをクリックすると、ページに必要なコンテンツコントロールが生成され、その `ContentPlaceHolderID` プロパティが ContentPlaceHolder の `ID`に設定されます。 たとえば、`About.aspx` の `LeftColumnContent` 領域の [カスタムコンテンツの作成] リンクをクリックすると、次の宣言型のマークアップがページに追加されます。

[!code-aspx[Main](multiple-contentplaceholders-and-default-content-vb/samples/sample3.aspx)]

### <a name="omitting-content-controls"></a>コンテンツコントロールの省略

ASP.NET では、マスターページで定義されているすべての ContentPlaceHolder のコンテンツコントロールがすべてのコンテンツページに含まれている必要はありません。 コンテンツコントロールを省略した場合、ASP.NET エンジンは、マスターページの ContentPlaceHolder 内で定義されているマークアップを使用します。 このマークアップは、ContentPlaceHolder の既定の*コンテンツ*と呼ばれており、一部の領域のコンテンツがほとんどのページで共通であるが、少数のページに対してカスタマイズする必要がある場合に便利です。 手順3では、マスターページでの既定のコンテンツの指定について説明します。

現在、`Default.aspx` には、`head` と `MainContent` ContentPlaceHolders の2つのコンテンツコントロールが含まれています。`LeftColumnContent`のコンテンツコントロールはありません。 その結果、`Default.aspx` がレンダリングされると、`LeftColumnContent` ContentPlaceHolder の既定のコンテンツが使用されます。 この ContentPlaceHolder の既定のコンテンツはまだ定義していないので、実質的な効果は、この領域にマークアップが生成されないことです。 この動作を確認するには、ブラウザーを使用して `Default.aspx` にアクセスします。 図5に示すように、[ニュース] セクションの左側の列にマークアップは出力されません。

[左の Columncontent ContentPlaceHolder に対してコンテンツがレンダリングされない ![](multiple-contentplaceholders-and-default-content-vb/_static/image14.png)](multiple-contentplaceholders-and-default-content-vb/_static/image13.png)

**図 05**: `LeftColumnContent` ContentPlaceHolder に対してコンテンツがレンダリングされない ([クリックしてフルサイズの画像を表示する](multiple-contentplaceholders-and-default-content-vb/_static/image15.png))

## <a name="step-3-specifying-default-content-in-the-master-page"></a>手順 3: マスターページで既定のコンテンツを指定する

一部の web サイトのデザインには、1つまたは2つの例外を除き、サイト内のすべてのページで同じコンテンツを持つリージョンが含まれています。 ユーザーアカウントをサポートする web サイトを考えてみましょう。 このようなサイトには、ビジターがサイトにサインインするための資格情報を入力できるログインページが必要です。 サインインプロセスを迅速化するために、web サイトのデザイナーでは、ユーザーがログインページに明示的にアクセスしなくてもサインインできるように、各ページの左上隅にユーザー名とパスワードのテキストボックスを含めることができます。 これらのユーザー名とパスワードのテキストボックスはほとんどのページで役に立ちますが、ログインページには冗長であり、ユーザーの資格情報のテキストボックスが既に含まれています。

この設計を実装するには、マスターページの左上隅に ContentPlaceHolder コントロールを作成します。 左上隅にユーザー名とパスワードのテキストボックスを表示するために必要な各ページでは、この ContentPlaceHolder のコンテンツコントロールを作成し、必要なインターフェイスを追加します。 一方、ログインページでは、この ContentPlaceHolder のコンテンツコントロールの追加を省略したり、マークアップが定義されていないコンテンツコントロールを作成したりすることができます。 この方法の欠点は、サイトに追加するすべてのページにユーザー名とパスワードのテキストボックスを追加することです (ログインページは除きます)。 これにより、問題が発生します。 これらのテキストボックスをページまたは2つに追加することは忘れられる可能性があります。最悪の場合、インターフェイスが正しく実装されていない可能性があります (2 ではなく1つのテキストボックスのみを追加するなど)。

より適切な解決策として、ユーザー名とパスワードのテキストボックスを ContentPlaceHolder の既定のコンテンツとして定義します。 そのため、ユーザー名とパスワードのテキストボックス (ログインページなど) を表示しない少数のページで、この既定のコンテンツを上書きする必要があります。 ContentPlaceHolder コントロールの既定のコンテンツを指定する方法を示すために、ここで説明したシナリオを実装します。

> [!NOTE]
> このチュートリアルの残りの部分では、ログインページではなく、すべてのページの左側の列にログインインターフェイスを含めるように web サイトを更新します。 ただし、このチュートリアルでは、ユーザーアカウントをサポートするように web サイトを構成する方法については説明しません。 このトピックの詳細については、「[フォーム認証、承認、ユーザーアカウント、およびロール](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)のチュートリアル」を参照してください。

### <a name="adding-a-contentplaceholder-and-specifying-its-default-content"></a>ContentPlaceHolder を追加し、その既定のコンテンツを指定する

`Site.master` マスターページを開き、`DateDisplay` のラベルとレッスンのセクションの左側の列に次のマークアップを追加します。

[!code-aspx[Main](multiple-contentplaceholders-and-default-content-vb/samples/sample4.aspx)]

このマークアップを追加すると、マスターページのデザインビューは図6のようになります。

[マスターページにログインコントロールが含まれて ![](multiple-contentplaceholders-and-default-content-vb/_static/image17.png)](multiple-contentplaceholders-and-default-content-vb/_static/image16.png)

**図 06**: マスターページにログインコントロールが含まれている ([クリックしてフルサイズの画像を表示する](multiple-contentplaceholders-and-default-content-vb/_static/image18.png))

この ContentPlaceHolder の `QuickLoginUI`には、既定のコンテンツとしてログイン Web コントロールがあります。 ログインコントロールには、ユーザーにユーザー名とパスワードの入力を求めるユーザーインターフェイスと、[ログイン] ボタンが表示されます。 ログインコントロールは、[ログイン] ボタンをクリックすると、メンバーシップ API に対してユーザーの資格情報を内部で検証します。 このログイン制御を実際に使用するには、メンバーシップを使用するようにサイトを構成する必要があります。 このトピックは、このチュートリアルの範囲を超えています。ユーザーアカウントをサポートする web アプリケーションの構築の詳細については[、「フォーム認証、承認、ユーザーアカウント、およびロール](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)のチュートリアル」を参照してください。

ログインコントロールの動作や外観は自由にカスタマイズできます。 `TitleText` と `FailureAction`の2つのプロパティを設定しました。 `TitleText` プロパティ値 (既定では "Log In") は、コントロールのユーザーインターフェイスの上部に表示されます。 このプロパティを設定して、"Sign In" というテキストが `<h3>` 要素として表示されるようにしました。 `FailureAction` プロパティは、ユーザーの資格情報が無効な場合の対処方法を示します。 既定では `Refresh`の値に設定されています。これにより、ユーザーが同じページに移動し、Login コントロール内にエラーメッセージが表示されます。 これを `RedirectToLoginPage`に変更しました。これにより、無効な資格情報が発生した場合にユーザーがログインページに送信されます。 ユーザーが他のページからログインしようとしたときに、ログインページにユーザーを送信することを希望しています。ただし、ログインページには、左の列には簡単に収めることができない追加の指示とオプションを含めることができるからです。 たとえば、[ログイン] ページには、忘れたパスワードを取得したり、新しいアカウントを作成したりするためのオプションが含まれている場合があります。

### <a name="creating-the-login-page-and-overriding-the-default-content"></a>ログインページを作成し、既定のコンテンツを上書きする

マスターページが完成したら、次の手順としてログインページを作成します。 `Login.aspx`という名前のサイトのルートディレクトリに ASP.NET ページを追加し、`Site.master` マスターページにバインドします。 これにより、`Site.master`で定義されている ContentPlaceHolders ごとに1つずつ、4つのコンテンツコントロールを含むページが作成されます。

`MainContent` コンテンツコントロールにログインコントロールを追加します。 同様に、任意のコンテンツを `LeftColumnContent` 領域に追加してもかまいません。 ただし、`QuickLoginUI` ContentPlaceHolder のコンテンツコントロールは空のままにしておく必要があります。 これにより、ログインコントロールがログインページの左側の列に表示されないようになります。

`MainContent` と `LeftColumnContent` 領域のコンテンツを定義すると、ログインページの宣言型マークアップは次のようになります。

[!code-aspx[Main](multiple-contentplaceholders-and-default-content-vb/samples/sample5.aspx)]

図7は、ブラウザーを使用して表示するときにこのページを示しています。 このページでは `QuickLoginUI` ContentPlaceHolder のコンテンツコントロールを指定しているので、マスターページに指定されている既定のコンテンツはオーバーライドされます。 実質的な効果として、マスターページのデザインビューに表示されるログイン制御 (図6を参照) は、このページではレンダリングされません。

[Represses QuickLoginUI ContentPlaceHolder の既定のコンテンツに対するログインページの ![](multiple-contentplaceholders-and-default-content-vb/_static/image20.png)](multiple-contentplaceholders-and-default-content-vb/_static/image19.png)

**図 07**: ログインページで `QuickLoginUI` ContentPlaceHolder の既定のコンテンツを Represses[する (クリックしてフルサイズの画像を表示する](multiple-contentplaceholders-and-default-content-vb/_static/image21.png))

### <a name="using-the-default-content-in-new-pages"></a>新しいページでの既定のコンテンツの使用

ログインページを除くすべてのページの左側の列に Login コントロールを表示します。 これを実現するには、ログインページを除くすべてのコンテンツページで、`QuickLoginUI` ContentPlaceHolder のコンテンツコントロールを省略する必要があります。 コンテンツコントロールを省略すると、ContentPlaceHolder の既定のコンテンツが代わりに使用されます。

既存のコンテンツページ (`Default.aspx`、`About.aspx`、および `MultipleContentPlaceHolders.aspx`) には、ContentPlaceHolder コントロールをマスターページに追加する前に作成されたため、`QuickLoginUI` のコンテンツコントロールは含まれていません。 そのため、これらの既存のページを更新する必要はありません。 ただし、web サイトに追加された新しいページには、既定で `QuickLoginUI` ContentPlaceHolder のコンテンツコントロールが含まれています。 そのため、新しいコンテンツページを追加するたびに、これらのコンテンツコントロールを削除しておく必要があります (ログインページの場合のように、ContentPlaceHolder の既定のコンテンツをオーバーライドする場合を除きます)。

コンテンツコントロールを削除するには、ソースビューから手動で宣言マークアップを削除するか、デザインビューから、スマートタグからマスターコンテンツの既定のリンクを選択します。 どちらの方法でも、コンテンツコントロールはページから削除され、実質的には同じ効果が得られます。

図8は、ブラウザーを使用して表示する場合の `Default.aspx` を示しています。 `Default.aspx`、宣言型マークアップで指定されているコンテンツコントロールが2つだけであることを思い出してください。1つは `head` 用、もう1つは `MainContent`用です。 その結果、`LeftColumnContent` と `QuickLoginUI` ContentPlaceHolders の既定の内容が表示されます。

[左の Columncontent の既定のコンテンツと QuickLoginUI ContentPlaceHolders を ![](multiple-contentplaceholders-and-default-content-vb/_static/image23.png)](multiple-contentplaceholders-and-default-content-vb/_static/image22.png)

**図 08**: `LeftColumnContent` および `QuickLoginUI` Contentplaceholders の既定の内容が表示される ([クリックすると、フルサイズの画像が表示](multiple-contentplaceholders-and-default-content-vb/_static/image24.png)されます)

## <a name="summary"></a>まとめ

ASP.NET マスターページモデルでは、マスターページで任意の数の ContentPlaceHolders を使用できます。 さらに、ContentPlaceHolders には既定のコンテンツが含まれています。これは、コンテンツページに対応するコンテンツコントロールがない場合に出力されます。 このチュートリアルでは、マスターページに追加の ContentPlaceHolder コントロールを追加する方法と、新しい ASP.NET ページと既存のページの両方でこれらの新しい ContentPlaceHolders のコンテンツコントロールを定義する方法を説明しました。 また、ContentPlaceHolder での既定のコンテンツの指定についても説明しました。これは、少数のページだけが特定の地域内のその他の標準化されたコンテンツをカスタマイズする必要があるシナリオで役に立ちます。

次のチュートリアルでは、`head` ContentPlaceHolder について詳しく説明し、ページごとにタイトル、メタタグ、およびその他の HTML ヘッダーを宣言およびプログラムによって定義する方法を説明します。

プログラミングを楽しんでください。

### <a name="about-the-author"></a>著者について

1998以降、Microsoft の Web テクノロジを使用して、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(複数の asp/創設者4GuysFromRolla.com の執筆者) が Microsoft の Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 3.5 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 Scott は、 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)またはブログで[http://ScottOnWriting.NET](http://scottonwriting.net/)にアクセスできます。

### <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビューアーは、Suchi になりました。 今後の MSDN 記事を確認することに興味がありますか? その場合は、 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)の行を削除します。

> [!div class="step-by-step"]
> [前へ](creating-a-site-wide-layout-using-master-pages-vb.md)
> [次へ](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb.md)
