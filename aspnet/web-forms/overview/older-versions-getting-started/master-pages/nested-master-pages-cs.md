---
uid: web-forms/overview/older-versions-getting-started/master-pages/nested-master-pages-cs
title: 入れ子になったC#マスターページ () |Microsoft Docs
author: rick-anderson
description: 1つのマスターページを別のマスターページに入れ子にする方法について説明します。
ms.author: riande
ms.date: 07/28/2008
ms.assetid: 32b7fb6e-d74b-4048-91f8-70631b2523ee
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/nested-master-pages-cs
msc.type: authoredcontent
ms.openlocfilehash: 67093266567a97cd22b353115616484fd9ef155e
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74596775"
---
# <a name="nested-master-pages-c"></a>入れ子にされたマスター ページ (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[コードのダウンロード](https://download.microsoft.com/download/d/6/6/d66ad554-afdd-409e-a5c3-201b774fbb31/ASPNET_MasterPages_Tutorial_10_CS.zip)または[PDF のダウンロード](https://download.microsoft.com/download/d/6/6/d66ad554-afdd-409e-a5c3-201b774fbb31/ASPNET_MasterPages_Tutorial_10_CS.pdf)

> 1つのマスターページを別のマスターページに入れ子にする方法について説明します。

## <a name="introduction"></a>はじめに

これまでの9つのチュートリアルでは、マスターページを使用してサイト全体のレイアウトを実装する方法を説明しました。 簡単に言うと、マスターページを使用すると、ページ開発者は、マスターページで共通のマークアップを、コンテンツページごとにカスタマイズできる特定の領域と共に定義できます。 マスターページの ContentPlaceHolder コントロールは、カスタマイズ可能な領域を示します。ContentPlaceHolder コントロール用にカスタマイズしたマークアップは、コンテンツコントロールを使用してコンテンツページで定義されます。

これまでに説明したマスターページの手法は、サイト全体で1つのレイアウトを使用する場合に最適です。 ただし、多くの大規模な web サイトには、さまざまなセクションでカスタマイズされたサイトレイアウトがあります。 たとえば、患者の情報、活動、請求を管理するために病院のスタッフが使用する医療関連アプリケーションを考えてみます。 このアプリケーションには、次の3種類の web ページがあります。

- スタッフメンバーが可用性を更新したり、スケジュールを表示したり、休暇時間を要求したりできるスタッフメンバー固有のページ。
- スタッフメンバーが特定の患者の情報を表示または編集する患者固有のページ。
- 経理担当者が現在の要求の状態と財務報告を確認する請求固有のページ。

すべてのページで、上部のメニューや下部に頻繁に使用する一連のリンクなど、一般的なレイアウトが共有されている場合があります。 しかし、スタッフ、患者、および課金固有のページでは、この汎用レイアウトのカスタマイズが必要になる場合があります。 たとえば、スタッフ固有のすべてのページには、現在ログオンしているユーザーの可用性と日単位のスケジュールを示す予定表とタスク一覧が含まれている必要があります。 場合によっては、患者固有のすべてのページで、情報を編集する患者の名前、住所、保険情報を表示する必要があります。

*入れ子になったマスターページ*を使用して、このようなカスタマイズされたレイアウトを作成することができます。 上記のシナリオを実装するには、まず、サイト全体のレイアウト (メニューとフッターのコンテンツ) を定義したマスターページを作成し、カスタマイズ可能な領域を定義する ContentPlaceHolders を使用します。 次に、web ページの種類ごとに1つずつ、入れ子になった3つのマスターページを作成します。 各入れ子になったマスターページは、マスターページを使用するコンテンツページの種類のコンテンツを定義します。 つまり、患者固有のコンテンツページの入れ子になったマスターページには、編集中の患者に関する情報を表示するためのマークアップとプログラムロジックが含まれます。 新しい患者固有のページを作成する場合は、この入れ子になったマスターページにバインドします。

このチュートリアルでは、まず、入れ子になったマスターページの利点を強調表示します。 次に、入れ子になったマスターページを作成して使用する方法を示します。

> [!NOTE]
> .NET Framework のバージョン2.0 以降、入れ子になったマスターページが使用可能になりました。 ただし、Visual Studio 2005 には、入れ子になったマスターページのデザイン時サポートは含まれていませんでした。 Visual Studio 2008 では、入れ子になったマスターページに対して豊富なデザイン時のエクスペリエンスが提供されていることが朗報です。 入れ子になったマスターページの使用に関心があるが、Visual Studio 2005 をまだ使用している場合は、「 [VS 2005 デザイン時の入れ子になったマスターページのヒント](https://weblogs.asp.net/scottgu/archive/2005/11/11/430382.aspx)」[をご覧ください](https://weblogs.asp.net/scottgu/)。

## <a name="the-benefits-of-nested-master-pages"></a>入れ子になったマスターページの利点

多くの web サイトには、包括的なサイト設計と、特定の種類のページに固有のカスタマイズされたデザインがあります。 たとえば、このデモ web アプリケーションでは、基本的な管理セクション (`~/Admin` フォルダー内のページ) を作成しました。 現在、`~/Admin` フォルダー内の web ページでは、[管理] セクションにないページと同じマスターページが使用されます (ユーザーの選択によっては、`Site.master` または `Alternate.master`ます)。

> [!NOTE]
> ここでは、このサイトには、`Site.master`ているマスターページが1つだけあるとします。 このチュートリアルでは、後の「管理者用に入れ子になったマスターページを使用する」で始まる2つ (またはそれ以上) のマスターページを含む入れ子になったマスターページを使用する方法について説明します。

管理ページのレイアウトをカスタマイズして、サイト内の他のページにない情報やリンクを追加するように求められたとします。 この要件を実装するには、次の4つの方法があります。

1. 管理固有の情報と、`~/Admin` フォルダー内のすべてのコンテンツページへのリンクを手動で追加します。
2. `Site.master` マスターページを更新して、管理セクション固有の情報とリンクを含めます。次に、管理ページにアクセスしているかどうかに基づいて、これらのセクションを表示または非表示にするコードをマスターページに追加します。
3. [管理] セクション専用の新しいマスターページを作成し、`Site.master`からマークアップをコピーします。次に、[管理] セクション固有の情報とリンクを追加し、この新しいマスターページを使用するように `~/Admin` フォルダー内のコンテンツページを更新します。
4. 入れ子になったマスターページを作成し `Site.master` にバインドし、`~/Admin` フォルダー内のコンテンツページでこの新しい入れ子になったマスターページを使用します。 この入れ子になったマスターページには、管理ページに固有の追加情報とリンクだけが含まれており、`Site.master`で既に定義されているマークアップを繰り返す必要はありません。

最初のオプションは、最小つながりです。 マスターページを使用すると、共通のマークアップを手動でコピーして新しい ASP.NET ページに貼り付ける必要がなくなります。 2番目のオプションは許容されますが、アプリケーションの保守が容易になります。ただし、表示されることがときどきないマークアップを使用してマスターページを構成すると、開発者がこのマークアップを回避して、いつでも覚えておく必要があります。正確には、特定のマークアップが表示されます。 この方法では、この1つのマスターページで対応する必要がある、より多くの種類の web ページからのカスタマイズが可能になります。

3番目のオプションは、2番目のオプションで表示される煩雑で複雑な問題を解消します。 ただし、オプションの3つの主な欠点は、`Site.master` から新しい管理セクション固有のマスターページに共通レイアウトをコピーして貼り付ける必要があることです。 後でサイト全体のレイアウトを変更する場合は、2か所で変更する必要があります。

4番目のオプションである [入れ子になったマスターページ] を選択すると、2番目と3番目のオプションが最適になります。 サイト全体のレイアウト情報は1つのファイル (最上位のマスターページ) に保持されますが、特定の領域に固有のコンテンツは別のファイルに分割されます。

このチュートリアルでは、まず、単純な入れ子になったマスターページの作成と使用について説明します。 新しいトップレベルマスターページ、2つの入れ子になったマスターページ、2つのコンテンツページを作成します。 「管理のための入れ子になったマスターページの使用」セクションでは、入れ子になったマスターページの使用を含むように、既存のマスターページアーキテクチャを更新することに注目しています。 具体的には、入れ子になったマスターページを作成し、それを使用して、`~/Admin` フォルダー内のコンテンツページの追加のカスタムコンテンツを含めることができます。

## <a name="step-1-creating-a-simple-top-level-master-page"></a>手順 1: 単純なトップレベルマスターページの作成

既存のコンテンツページで既に予想されているため、既存のマスターページのいずれかに基づいて入れ子になったマスターを作成し、既存のコンテンツページを更新して、新しい入れ子になったマスターページを使用する場合は、複雑な作業が必要になります。最上位レベルのマスターページで定義されている ContentPlaceHolder コントロール。 したがって、入れ子になったマスターページには、同じ名前を持つ同じ ContentPlaceHolder コントロールも含まれている必要があります。 さらに、特定のデモアプリケーションには、ユーザーの設定に基づいてコンテンツページに動的に割り当てられる2つのマスターページ (`Site.master` と `Alternate.master`) があり、さらにこの複雑さに追加されます。 このチュートリアルの後半では、入れ子になったマスターページを使用するように既存のアプリケーションを更新する方法について説明しますが、まず、単純な入れ子になったマスターページの例に注目します。

`NestedMasterPages` という名前の新しいフォルダーを作成し、`Simple.master`という名前の新しいマスターページファイルをそのフォルダーに追加します。 (このフォルダーとファイルが追加された後のソリューションエクスプローラーのスクリーンショットについては、図1を参照してください。)`AlternateStyles.css` スタイルシートファイルをソリューションエクスプローラーからデザイナーにドラッグします。 これにより、`<head>` 要素内のスタイルシートファイルに `<link>` 要素が追加されます。その後、マスターページの `<head>` 要素のマークアップは次のようになります。

[!code-aspx[Main](nested-master-pages-cs/samples/sample1.aspx)]

次に、`Simple.master`の Web フォーム内に次のマークアップを追加します。

[!code-aspx[Main](nested-master-pages-cs/samples/sample2.aspx)]

このマークアップは、ページの上部にある "入れ子になったマスターページ (Simple)" というタイトルのリンクを、海軍の背景にある大きな白いフォントで表示します。 その下に、`MainContent` ContentPlaceHolder があります。 図1は、Visual Studio デザイナーで読み込まれたときの `Simple.master` マスターページを示しています。

[入れ子になったマスターページ ![、[管理] セクションのページに固有のコンテンツを定義します。](nested-master-pages-cs/_static/image2.png)](nested-master-pages-cs/_static/image1.png)

**図 01**: 入れ子になったマスターページは、[管理] セクションのページに固有のコンテンツを定義します ([クリックすると、フルサイズの画像が表示](nested-master-pages-cs/_static/image3.png)されます)

## <a name="step-2-creating-a-simple-nested-master-page"></a>手順 2: 単純な入れ子になったマスターページの作成

`Simple.master` には、Web フォーム内に追加した `MainContent` ContentPlaceHolder と `<head>` 要素の `head` ContentPlaceHolder の2つの ContentPlaceHolder コントロールが含まれています。 コンテンツページを作成してにバインドする場合、コンテンツページには2つの ContentPlaceHolders を参照する2つのコンテンツコントロールが `Simple.master` ます。 同様に、入れ子になったマスターページを作成して `Simple.master` にバインドした場合、入れ子になったマスターページには2つのコンテンツコントロールが含まれます。

新しい入れ子になったマスターページを `SimpleNested.master`という名前の `NestedMasterPages` フォルダーに追加してみましょう。 `NestedMasterPages` フォルダーを右クリックし、[新しい項目の追加] を選択します。 これにより、図2に示す [新しい項目の追加] ダイアログボックスが表示されます。 マスターページテンプレートの種類を選択し、新しいマスターページの名前を入力します。 新しいマスターページが入れ子になったマスターページであることを示すには、[マスターページの選択] チェックボックスをオンにします。

次に、[追加] ボタンをクリックします。 これにより、コンテンツページをマスターページにバインドするときに表示されるのと同じ [マスターページの選択] ダイアログボックスが表示されます (図3を参照)。 `NestedMasterPages` フォルダーの `Simple.master` マスターページを選択し、[OK] をクリックします。

> [!NOTE]
> Web サイトプロジェクトモデルではなく、Web アプリケーションプロジェクトモデルを使用して ASP.NET web サイトを作成した場合、図2に示す [新しい項目の追加] ダイアログボックスの [マスターページの選択] チェックボックスは表示されません。 Web アプリケーションプロジェクトモデルを使用しているときに入れ子になったマスターページを作成するには、(マスターページテンプレートではなく) 入れ子になったマスターページテンプレートを選択する必要があります。 入れ子になったマスターページテンプレートを選択して [追加] をクリックすると、図3に示されているのと同じ [マスターページの選択] ダイアログボックスが表示されます。

[&quot;[マスターページの選択]&quot; チェックボックスをオンにして、入れ子になったマスターページを追加 ![ます。](nested-master-pages-cs/_static/image5.png)](nested-master-pages-cs/_static/image4.png)

**図 02**: [マスターページの選択] チェックボックスをオンにして、入れ子になったマスターページを追加する ([クリックすると、フルサイズの画像が表示](nested-master-pages-cs/_static/image6.png)されます)

[入れ子になったマスターページを単純なマスターページにバインド ![には](nested-master-pages-cs/_static/image8.png)](nested-master-pages-cs/_static/image7.png)

**図 03**: 入れ子になったマスターページを `Simple.master` マスターページにバインドする ([クリックすると、フルサイズの画像が表示](nested-master-pages-cs/_static/image9.png)されます)

次に示す入れ子になったマスターページの宣言型のマークアップには、トップレベルのマスターページの2つの ContentPlaceHolder コントロールを参照する2つのコンテンツコントロールが含まれています。

[!code-aspx[Main](nested-master-pages-cs/samples/sample3.aspx)]

`<%@ Master %>` ディレクティブを除き、入れ子になったマスターページの初期宣言マークアップは、コンテンツページを同じトップレベルマスターページにバインドするときに最初に生成されるマークアップと同じです。 コンテンツページの `<%@ Page %>` ディレクティブと同様に、この `<%@ Master %>` ディレクティブには、入れ子になったマスターページの親マスターページを指定する `MasterPageFile` 属性が含まれています。 入れ子になったマスターページと同じトップレベルマスターページにバインドされたコンテンツページの主な違いは、入れ子になったマスターページに ContentPlaceHolder コントロールを含めることができることです。 入れ子になったマスターページの ContentPlaceHolder コントロールは、コンテンツページがマークアップをカスタマイズできる領域を定義します。

"Hello, from SimpleNested!" というテキストが表示されるように、この入れ子になったマスターページを更新します。 `MainContent` ContentPlaceHolder コントロールに対応するコンテンツコントロール。

[!code-aspx[Main](nested-master-pages-cs/samples/sample4.aspx)]

この追加を行った後、入れ子になったマスターページを保存し、`Default.aspx`という名前の `NestedMasterPages` フォルダーに新しいコンテンツページを追加して、`SimpleNested.master` マスターページにバインドします。 このページを追加すると、コンテンツコントロールが含まれていないことがわかります (図4を参照)。 コンテンツページは、その*親*マスターページの contentplaceholders にのみアクセスできます。 `SimpleNested.master` に ContentPlaceHolder コントロールが含まれていません。そのため、このマスターページにバインドされているコンテンツページにコンテンツコントロールを含めることはできません。

[[新しいコンテンツ] ページにコンテンツコントロールが含まれていない ![](nested-master-pages-cs/_static/image11.png)](nested-master-pages-cs/_static/image10.png)

**図 04**: [新しいコンテンツ] ページにコンテンツコントロールが含まれていない ([クリックしてフルサイズのイメージを表示する](nested-master-pages-cs/_static/image12.png))

ContentPlaceHolder コントロールを含めるには、入れ子になったマスターページ (`SimpleNested.master`) を更新する必要があります。 通常、入れ子になったマスターページには、親マスターページで定義されている各 ContentPlaceHolder の ContentPlaceHolder を含める必要があります。これにより、その子マスターページまたはコンテンツページは、トップレベルマスターページの ContentPlaceHolder を操作できます。制限.

`SimpleNested.master` マスターページを更新して、2つのコンテンツコントロールに ContentPlaceHolder を含めます。 ContentPlaceHolder コントロールに、コンテンツコントロールが参照する ContentPlaceHolder コントロールと同じ名前を付けます。 つまり、`Simple.master`で `MainContent` ContentPlaceHolder を参照する `SimpleNested.master` のコンテンツコントロールに `MainContent` という名前の ContentPlaceHolder コントロールを追加します。 `head` ContentPlaceHolder を参照するコンテンツコントロールでも同じことを行います。

> [!NOTE]
> 入れ子になったマスターページの ContentPlaceHolder コントロールには、トップレベルマスターページの ContentPlaceHolders と同じ名前を付けることをお勧めしますが、この名前付けの対称は必要ありません。 入れ子になったマスターページの ContentPlaceHolder コントロールには、好きな名前を付けることができます。 ただし、最上位のマスターページと入れ子になったマスターページが同じ名前を使用している場合は、どのような ContentPlaceHolders がページのどの領域に対応しているかがわかりやすくなります。

これらの追加を行った後、`SimpleNested.master` マスターページの宣言型マークアップは次のようになります。

[!code-aspx[Main](nested-master-pages-cs/samples/sample5.aspx)]

先ほど作成した `Default.aspx` コンテンツページを削除してから再度追加し、`SimpleNested.master` マスターページにバインドします。 今回は、Visual Studio が2つのコンテンツコントロールを `Default.aspx`に追加し、`SimpleNested.master` で定義された ContentPlaceHolders を参照します (図6を参照)。 "Hello, from default.aspx!" というテキストを追加します。 `MainContent`を参照したコンテンツコントロール。

図5に、`Simple.master`、`SimpleNested.master`、および `Default.aspx` に関連する3つのエンティティと、それらのエンティティが相互にどのように関連しているかを示します。 図に示すように、入れ子になったマスターページは、その親の ContentPlaceHolder のコンテンツコントロールを実装します。 これらの領域がコンテンツページにアクセスできる必要がある場合は、入れ子になったマスターページがコンテンツコントロールに独自の ContentPlaceHolders を追加する必要があります。

[最上位レベルと入れ子になったマスターページを ![して、コンテンツページのレイアウトを決定します。](nested-master-pages-cs/_static/image14.png)](nested-master-pages-cs/_static/image13.png)

**図 05**: 最上位レベルと入れ子になったマスターページは、コンテンツページのレイアウトを指示します ([クリックすると、フルサイズの画像が表示](nested-master-pages-cs/_static/image15.png)されます)

この動作は、コンテンツページまたはマスターページがその親マスターページの cognizant のみであることを示しています。 この動作は、Visual Studio デザイナーでも示されます。 図6は、`Default.aspx`のデザイナーを示しています。 デザイナーでは、コンテンツページから編集可能な領域とその部分が明確に示されていますが、入れ子になったマスターページからの編集できない領域と最上位のマスターページの領域は明確に区別されません。

[コンテンツページに、入れ子になったマスターページの ContentPlaceHolders のコンテンツコントロールが含まれるようになりました ![](nested-master-pages-cs/_static/image17.png)](nested-master-pages-cs/_static/image16.png)

**図 06**: コンテンツページに、入れ子になったマスターページの Contentplaceholders のコンテンツコントロールが含まれるようになりました ([クリックしてフルサイズのイメージを表示](nested-master-pages-cs/_static/image18.png))

## <a name="step-3-adding-a-second-simple-nested-master-page"></a>手順 3: 2 番目の単純な入れ子になったマスターページの追加

入れ子になったマスターページの利点は、入れ子になったマスターページが複数存在する場合によりわかりやすくなります。 この利点を説明するために、`NestedMasterPages` フォルダーに別の入れ子になったマスターページを作成します。この新しい入れ子になったマスターページの名前を `SimpleNestedAlternate.master` し、`Simple.master` マスターページにバインドします。 手順 2. で行ったように、入れ子になったマスターページの2つのコンテンツコントロールに ContentPlaceHolder コントロールを追加します。 また、"Hello, from SimpleNestedAlternate!" というテキストも追加します。 最上位レベルのマスターページの `MainContent` ContentPlaceHolder に対応するコンテンツコントロール。 これらの変更を行った後、新しい入れ子になったマスターページの宣言型マークアップは次のようになります。

[!code-aspx[Main](nested-master-pages-cs/samples/sample6.aspx)]

`NestedMasterPages` フォルダーに `Alternate.aspx` という名前のコンテンツページを作成し、`SimpleNestedAlternate.master` の入れ子になったマスターページにバインドします。 "Hello, from 代替!" というテキストを追加します。 `MainContent`に対応するコンテンツコントロール。 図7は、Visual Studio デザイナーを使用して表示する場合の `Alternate.aspx` を示しています。

[![default.aspx は、SimpleNestedAlternate マスターページにバインドされます。](nested-master-pages-cs/_static/image20.png)](nested-master-pages-cs/_static/image19.png)

**図 07**: `Alternate.aspx` が `SimpleNestedAlternate.master` マスターページにバインドされている ([クリックしてフルサイズの画像を表示する](nested-master-pages-cs/_static/image21.png))

図7のデザイナーを図6のデザイナーと比較します。 どちらのコンテンツページも、最上位のマスターページ (`Simple.master`) で定義されているのと同じレイアウトを共有します。つまり、"入れ子になったマスターページチュートリアル (Simple)" タイトルを共有します。 2つの親マスターページに個別のコンテンツが定義されています。テキスト "Hello, from SimpleNested!" 図6と "Hello, from SimpleNestedAlternate!" 図7の。 これらの違いは自明ですが、この例を拡張して、より意味のある相違点を含めることができます。 たとえば、[`SimpleNested.master`] ページには、コンテンツページに固有のオプションを含むメニューが含まれている場合があります。一方、`SimpleNestedAlternate.master` には、バインドされたコンテンツページに関連する情報が含まれている場合があります。

ここで、包括的なサイトレイアウトを変更する必要があるとします。 たとえば、すべてのコンテンツページに共通リンクのリストを追加するとします。 これを実現するには、最上位レベルのマスターページを更新し、`Simple.master`します。 そこに加えられた変更は、入れ子になったマスターページおよび拡張機能によってコンテンツページに直ちに反映されます。

最上層のサイトレイアウトを簡単に変更できるようにするには、`Simple.master` マスターページを開き、`topContent` と `mainContent` `<div>` 要素の間に次のマークアップを追加します。

[!code-aspx[Main](nested-master-pages-cs/samples/sample7.aspx)]

これにより、`Simple.master`、`SimpleNested.master`、または `SimpleNestedAlternate.master`にバインドされるすべてのページの上部に2つのリンクが追加されます。これらの変更は、すべての入れ子になったマスターページとそのコンテンツページに直ちに適用されます。 図8は、ブラウザーを使用して表示する場合の `Alternate.aspx` を示しています。 図7と比較して、ページの上部にリンクが追加されていることに注意してください。

[トップレベルマスターページに変更された ![は、入れ子になったマスターページとそのコンテンツページに直ちに反映されます。](nested-master-pages-cs/_static/image23.png)](nested-master-pages-cs/_static/image22.png)

**図 08**: トップレベルマスターページへの変更は、入れ子になったマスターページとそのコンテンツページに直ちに反映されます ([クリックすると、フルサイズの画像が表示](nested-master-pages-cs/_static/image24.png)されます)

## <a name="using-a-nested-master-page-for-the-administration-section"></a>[管理] セクションに入れ子になったマスターページを使用する

この時点で、入れ子になったマスターページの利点を確認し、ASP.NET アプリケーションでそれらを作成して使用する方法を見てきました。 ただし、手順1、2、および3の例では、新しいトップレベルマスターページ、新しい入れ子になったマスターページ、新しいコンテンツページを作成します。 新しい入れ子になったマスターページを、既存のトップレベルマスターページとコンテンツページを含む web サイトに追加するにはどうすればよいですか。

入れ子になったマスターページを既存の web サイトに統合し、既存のコンテンツページと関連付けるには、最初から開始するよりも少し手間がかかります。 手順4、5、6、および7では、デモアプリケーションを拡張して、管理者向けの手順を含む `AdminNested.master` という名前の新しい入れ子になったマスターページを追加し、`~/Admin` フォルダー内の ASP.NET ページで使用されるようにします。

入れ子になったマスターページをデモアプリケーションに統合すると、次のような課題が生じます。

- `~/Admin` フォルダー内の既存のコンテンツページには、マスターページからの特定の期待があります。 まず、特定の ContentPlaceHolder コントロールが存在することを想定しています。 さらに、`~/Admin/AddProduct.aspx` ページと `~/Admin/Products.aspx` ページは、マスターページのパブリック `RefreshRecentProductsGrid` メソッドを呼び出したり、その `GridMessageText` プロパティを設定したり、`PricesDoubled` イベントのイベントハンドラーを使用したりします。 そのため、入れ子になったマスターページは、同じ ContentPlaceHolders とパブリックメンバーを提供する必要があります。
- 前のチュートリアルでは、`BasePage` クラスを拡張して、セッション変数に基づいて `Page` オブジェクトの `MasterPageFile` プロパティを動的に設定しました。 入れ子になったマスターページを使用する場合、動的マスターページをサポートするにはどうすればよいですか。

これらの2つの課題は、入れ子になったマスターページを構築し、既存のコンテンツページから使用すると表示されます。 これらの問題は、発生したときに調査して、マウントします。

## <a name="step-4-creating-the-nested-master-page"></a>手順 4: 入れ子になったマスターページの作成

最初のタスクは、[管理] セクションのページで使用する、入れ子になったマスターページを作成することです。 手順 2. で見たように、入れ子になった新しいマスターページを追加するときは、入れ子になったマスターページの親マスターページを指定する必要があります。 しかし、`Site.master` と `Alternate.master`というトップレベルのマスターページが2つあります。 前のチュートリアルで `Alternate.master` を作成し、`Alternate.master` Session 変数の値に応じて、実行時に Page オブジェクトの `MasterPageFile` プロパティを `Site.master` または `MyMasterPage` に設定するコードを `BasePage` クラスに記述したことを思い出してください。

適切なトップレベルマスターページを使用するように、入れ子になったマスターページを構成するにはどうすればよいですか。 2つのオプションがあります。

- 2つの入れ子になったマスターページ `AdminNestedSite.master` と `AdminNestedAlternate.master`を作成し、それぞれをトップレベルのマスターページ `Site.master` および `Alternate.master`にバインドします。 `BasePage`では、`Page` オブジェクトの `MasterPageFile` を適切な入れ子になったマスターページに設定します。
- 1つの入れ子になったマスターページを作成し、コンテンツページがこの特定のマスターページを使用するようにします。 次に、実行時に、入れ子になったマスターページの `MasterPageFile` プロパティを、実行時に適切な最上位レベルのマスターページに設定する必要があります。 (現時点では、マスターページには `MasterPageFile` のプロパティもあります)。

2番目のオプションを使用してみましょう。 `AdminNested.master`という名前の `~/Admin` フォルダーに、1つの入れ子になったマスターページファイルを作成します。 `Site.master` と `Alternate.master` の両方に同じ ContentPlaceHolder コントロールのセットがあるため、バインド先のマスターページは関係ありませんが、整合性のために `Site.master` にバインドすることをお勧めします。

[入れ子になったマスターページを ~/Admin フォルダーに追加 ![ます。](nested-master-pages-cs/_static/image26.png)](nested-master-pages-cs/_static/image25.png)

**図 09**: 入れ子になったマスターページを `~/Admin` フォルダーに追加する ([クリックすると、フルサイズの画像が表示](nested-master-pages-cs/_static/image27.png)される)

入れ子になったマスターページは、4つの ContentPlaceHolder コントロールを持つマスターページにバインドされているため、Visual Studio は、新しい入れ子になったマスターページファイルの初期マークアップに4つのコンテンツコントロールを追加します。 手順 2. と 3. で行ったように、各コンテンツコントロールに ContentPlaceHolder コントロールを追加し、最上位レベルのマスターページの ContentPlaceHolder コントロールと同じ名前を付けます。 また、`MainContent` ContentPlaceHolder に対応する次のマークアップをコンテンツコントロールに追加します。

[!code-html[Main](nested-master-pages-cs/samples/sample8.html)]

次に、`Styles.css` CSS ファイルと `AlternateStyles.css` CSS ファイルで `instructions` CSS クラスを定義します。 次の CSS ルールでは、`instructions` クラスを使用してスタイル設定された HTML 要素が、明るい黄色の背景色と黒の実線の境界線で表示されます。

[!code-css[Main](nested-master-pages-cs/samples/sample9.css)]

このマークアップは、入れ子になったマスターページに追加されているため、この入れ子になったマスターページ (つまり、[管理] セクションのページ) を使用するページにのみ表示されます。

入れ子になったマスターページにこれらの追加を行うと、宣言型のマークアップは次のようになります。

[!code-aspx[Main](nested-master-pages-cs/samples/sample10.aspx)]

各コンテンツコントロールには ContentPlaceHolder コントロールがあり、ContentPlaceHolder コントロールの `ID` プロパティには、トップレベルマスターページの対応する ContentPlaceHolder コントロールと同じ値が割り当てられていることに注意してください。 さらに、管理セクション固有のマークアップが `MainContent` ContentPlaceHolder に表示されます。

図10は、Visual Studio のデザイナーを使用して表示するときに `AdminNested.master` の入れ子になったマスターページを示しています。 手順については、`MainContent` コンテンツコントロールの上部にある黄色のボックスを参照してください。

[入れ子になったマスターページ ![、トップレベルマスターページを拡張して、管理者に指示を含めます。](nested-master-pages-cs/_static/image29.png)](nested-master-pages-cs/_static/image28.png)

**図 10**: 入れ子になったマスターページは、トップレベルマスターページを拡張して、管理者に指示を含めます。 ([クリックすると、フルサイズの画像が表示](nested-master-pages-cs/_static/image30.png)される)

## <a name="step-5-updating-the-existing-content-pages-to-use-the-new-nested-master-page"></a>手順 5: 新しい入れ子になったマスターページを使用するように既存のコンテンツページを更新する

[管理] セクションに新しいコンテンツページを追加するたびに、先ほど作成した `AdminNested.master` マスターページにバインドする必要があります。 では、既存のコンテンツページについてはどうでしょうか。 現時点では、サイト内のすべてのコンテンツページは `BasePage` クラスから派生します。このクラスは、実行時にコンテンツページのマスターページをプログラムによって設定します。 これは、[管理] セクションのコンテンツページに必要な動作ではありません。 代わりに、これらのコンテンツページで常に `AdminNested.master` ページを使用する必要があります。 入れ子になったマスターページは、実行時に適切な最上位レベルのコンテンツページを選択する役割を担います。

この目的の動作を実現する最善の方法は、`BasePage` クラスを拡張する `AdminBasePage` という名前の新しいカスタム基本ページクラスを作成することです。 その後、`SetMasterPageFile` をオーバーライドし、`Page` オブジェクトの `MasterPageFile` をハードコーディングされた値 "~/Admin/adminnested`AdminBasePage` に設定できます。 この方法では、`AdminBasePage` から派生したすべてのページで `AdminNested.master`が使用されます。一方、`BasePage` から派生したすべてのページでは、`MyMasterPage` Session 変数の値に基づいて "~/Site. マスター" または "~/alternate" のいずれかに動的に設定さ `MasterPageFile` れます。

まず、`AdminBasePage.cs`という名前の `App_Code` フォルダーに新しいクラスファイルを追加します。 `BasePage` `AdminBasePage` 拡張し、`SetMasterPageFile` メソッドをオーバーライドする必要があります。 そのメソッドで、値 "~/Admin/adminnested`MasterPageFile` を割り当てます。 これらの変更を行った後、クラスファイルは次のようになります。

[!code-csharp[Main](nested-master-pages-cs/samples/sample11.cs)]

次に、[管理] セクションの既存のコンテンツページを、`BasePage`ではなく `AdminBasePage` から派生させる必要があります。 `~/Admin` フォルダー内の各コンテンツページの分離コードクラスファイルに移動し、この変更を行います。 たとえば、`~/Admin/Default.aspx` では、分離コードクラスの宣言を次のように変更します。

[!code-csharp[Main](nested-master-pages-cs/samples/sample12.cs)]

宛先:

[!code-csharp[Main](nested-master-pages-cs/samples/sample13.cs)]

図11は、最上位レベルのマスターページ (`Site.master` または `Alternate.master`)、入れ子になったマスターページ (`AdminNested.master`)、および管理セクションのコンテンツページが相互にどのように関連しているかを示しています。

[入れ子になったマスターページ ![、[管理] セクションのページに固有のコンテンツを定義します。](nested-master-pages-cs/_static/image32.png)](nested-master-pages-cs/_static/image31.png)

**図 11**: 入れ子になったマスターページは、[管理] セクションのページに固有のコンテンツを定義します ([クリックすると、フルサイズの画像が表示](nested-master-pages-cs/_static/image33.png)されます)

## <a name="step-6-mirroring-the-master-pages-public-methods-and-properties"></a>手順 6: マスターページのパブリックメソッドとプロパティをミラーリングする

`~/Admin/AddProduct.aspx` ページと `~/Admin/Products.aspx` ページは、マスターページとプログラムによって対話することを思い出してください。 `~/Admin/AddProduct.aspx` は、マスターページのパブリック `RefreshRecentProductsGrid` メソッドを呼び出し、その `GridMessageText` プロパティを設定します。`~/Admin/Products.aspx` には、`PricesDoubled` イベントのイベントハンドラーがあります。 前のチュートリアルでは、これらのパブリックメンバーを定義する抽象 `BaseMasterPage` クラスを作成しました。

`~/Admin/AddProduct.aspx` ページと `~/Admin/Products.aspx` ページでは、マスターページが `BaseMasterPage` クラスから派生していることを前提としています。 ただし、`AdminNested.master` ページでは、現在 `System.Web.UI.MasterPage` クラスが拡張されています。 その結果、`~/Admin/Products.aspx` にアクセスすると、"型 ' ASP のオブジェクトをキャストできませんでした。管理者\_adminnested\_master ' を型 ' BaseMasterPage ' にキャストできません。" というメッセージが表示されます。

この問題を解決するには、`AdminNested.master` 分離コードクラスで `BaseMasterPage`を拡張する必要があります。 入れ子になったマスターページの分離コードクラスの宣言を次のように更新します。

[!code-csharp[Main](nested-master-pages-cs/samples/sample14.cs)]

宛先:

[!code-csharp[Main](nested-master-pages-cs/samples/sample15.cs)]

まだ完了していません。 `BaseMasterPage` クラスは抽象であるため、`abstract` メンバー、`RefreshRecentProductsGrid`、および `GridMessageText`をオーバーライドする必要があります。 これらのメンバーは、最上位レベルのマスターページでユーザーインターフェイスを更新するために使用されます。 (実際には、これらのメソッドを使用するのは `Site.master` マスターページのみですが、どちらのトップレベルマスターページもこれらのメソッドを実装しますが、どちらも `BaseMasterPage`を拡張するためです)。

これらのメンバーは `AdminNested.master`で実装する必要がありますが、これらの実装で必要なのは、入れ子になったマスターページで使用される最上位レベルのマスターページで同じメンバーを呼び出すことだけです。 たとえば、[管理] セクションのコンテンツページで入れ子になったマスターページの `RefreshRecentProductsGrid` メソッドを呼び出す場合、入れ子になったマスターページはすべて、`Site.master` または `Alternate.master`の `RefreshRecentProductsGrid` メソッドを呼び出す必要があります。

これを実現するには、まず、次の `@MasterType` ディレクティブを `AdminNested.master`の先頭に追加します。

[!code-aspx[Main](nested-master-pages-cs/samples/sample16.aspx)]

`@MasterType` ディレクティブにより、厳密に型指定されたプロパティが `Master`という名前の分離コードクラスに追加されることを思い出してください。 次に、`RefreshRecentProductsGrid` と `GridMessageText` のメンバーをオーバーライドし、`Master`の対応するメソッドへの呼び出しを単純に委任します。

[!code-csharp[Main](nested-master-pages-cs/samples/sample17.cs)]

このコードを配置すると、[管理] セクションのコンテンツページにアクセスして使用できるようになります。 図12は、ブラウザーを使用して表示するときの `~/Admin/Products.aspx` ページを示しています。 ご覧のように、このページには、入れ子になったマスターページで定義されている管理手順ボックスが含まれています。

[[管理] セクションのコンテンツページ ![、各ページの上部に説明があります。](nested-master-pages-cs/_static/image35.png)](nested-master-pages-cs/_static/image34.png)

**図 12**: [管理] セクションの [コンテンツ] ページには、各ページの上部に表示される指示が含まれます ([クリックすると、フルサイズの画像が表示](nested-master-pages-cs/_static/image36.png)されます)。

## <a name="step-7-using-the-appropriate-top-level-master-page-at-runtime"></a>手順 7: 実行時に適切なトップレベルマスターページを使用する

[管理] セクションのすべてのコンテンツページは完全に機能しますが、すべて同じトップレベルのマスターページを使用し、`ChooseMasterPage.aspx`でユーザーが選択したマスターページを無視します。 この動作は、入れ子になったマスターページの `MasterPageFile` プロパティが、その `<%@ Master %>` ディレクティブで `Site.master` に静的に設定されていることが原因です。

エンドユーザーが選択した最上位レベルのマスターページを使用するには、`AdminNested.master`の `MasterPageFile` プロパティを `MyMasterPage` Session 変数の値に設定する必要があります。 コンテンツページの `MasterPageFile` プロパティは `BasePage`で設定されているため、`BaseMasterPage` または `AdminNested.master`の分離コードクラスで、入れ子になったマスターページの `MasterPageFile` プロパティを設定することになるかもしれません。 ただし、PreInit ステージの最後までに `MasterPageFile` プロパティを設定する必要があるため、これは機能しません。 マスターページからページライフサイクルをプログラムによってタップできる最も早い時間は、(PreInit ステージの後に発生する) Init ステージです。

そのため、入れ子になったマスターページの `MasterPageFile` プロパティをコンテンツページから設定する必要があります。 `AdminNested.master` マスターページを使用する唯一のコンテンツページは、`AdminBasePage`から派生します。 このため、このロジックを配置できます。 手順 5. で `SetMasterPageFile` メソッドをオーバーライドして、`Page` オブジェクトの `MasterPageFile` プロパティを "~/Admin/マスター" に設定します。 `SetMasterPageFile` を更新して、マスターページの `MasterPageFile` プロパティを、セッションに格納されている結果にも設定します。

[!code-csharp[Main](nested-master-pages-cs/samples/sample18.cs)]

前のチュートリアルで `BasePage` クラスに追加した `GetMasterPageFileFromSession` メソッドは、セッション変数の値に基づいて、適切なマスターページのファイルパスを返します。

この変更により、ユーザーのマスターページ選択は [管理] セクションに引き継がれます。 図13は、図12と同じページを示していますが、ユーザーがマスターページの選択を `Alternate.master`に変更した後に表示されます。

[入れ子になった管理ページで、ユーザーが選択した最上位レベルのマスターページを使用 ![](nested-master-pages-cs/_static/image38.png)](nested-master-pages-cs/_static/image37.png)

**図 13**: 入れ子になった管理ページで、ユーザーが選択した最上位レベルのマスターページを使用[する (クリックしてフルサイズの画像を表示する](nested-master-pages-cs/_static/image39.png))

## <a name="summary"></a>要約

コンテンツページをマスターページにバインドするのと同じように、子マスターページを親マスターページにバインドすることで、入れ子になったマスターページを作成できます。 子マスターページでは、各親の ContentPlaceHolders のコンテンツコントロールを定義できます。その後、独自の ContentPlaceHolder コントロール (およびその他のマークアップ) をこれらのコンテンツコントロールに追加できます。 入れ子になったマスターページは、すべてのページが包括的なルックアンドフィールを共有する大規模な web アプリケーションで非常に便利ですが、サイトの特定のセクションでは独自のカスタマイズが必要です。

プログラミングを楽しんでください。

### <a name="further-reading"></a>関連項目

このチュートリアルで説明しているトピックの詳細については、次のリソースを参照してください。

- [入れ子になった ASP.NET マスターページ](https://msdn.microsoft.com/library/x2b3ktt7.aspx)
- [入れ子になったマスターページと VS 2005 デザイン時のヒント](https://weblogs.asp.net/scottgu/archive/2005/11/11/430382.aspx)
- [VS 2008 入れ子になったマスターページのサポート](https://weblogs.asp.net/scottgu/archive/2007/07/09/vs-2008-nested-master-page-support.aspx)

### <a name="about-the-author"></a>作成者について

1998以降、Microsoft の Web テクノロジを使用して、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(複数の asp/創設者4GuysFromRolla.com の執筆者) が Microsoft の Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 3.5 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672329972/4guysfromrollaco)ています。 Scott は、 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)またはブログで[http://ScottOnWriting.NET](http://scottonwriting.net/)にアクセスできます。

### <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 今後の MSDN 記事を確認することに興味がありますか? その場合は、 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)の行を削除します。

> [!div class="step-by-step"]
> [前へ](specifying-the-master-page-programmatically-cs.md)
> [次へ](creating-a-site-wide-layout-using-master-pages-vb.md)
