---
uid: web-forms/overview/moving-to-aspnet-20/master-pages
title: マスターページ |Microsoft Docs
author: microsoft
description: 成功した Web サイトの重要なコンポーネントの1つは、一貫したルックアンドフィールです。 ASP.NET 1.x では、開発者はユーザーコントロールを使用して共通ページ elem...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 9c0cce4d-efd9-4c14-b0e8-a1a140abb3f4
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/master-pages
msc.type: authoredcontent
ms.openlocfilehash: 36f2caf7c2c9bcafd22c8f6681c1d6b19fe5078a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78457582"
---
# <a name="master-pages"></a>マスター ページ

[Microsoft](https://github.com/microsoft)

> 成功した Web サイトの重要なコンポーネントの1つは、一貫したルックアンドフィールです。 ASP.NET 1.x では、開発者はユーザーコントロールを使用して、Web アプリケーション全体で共通ページ要素をレプリケートしました。 これは確かに動作可能なソリューションですが、ユーザーコントロールを使用すると、いくつかの欠点があります。 たとえば、ユーザーコントロールの位置を変更するには、サイト全体で複数のページを変更する必要があります。 ユーザーコントロールは、ページに挿入された後にデザインビューでレンダリングされることもありません。

成功した Web サイトの重要なコンポーネントの1つは、一貫したルックアンドフィールです。 ASP.NET 1.x では、開発者はユーザーコントロールを使用して、Web アプリケーション全体で共通ページ要素をレプリケートしました。 これは確かに動作可能なソリューションですが、ユーザーコントロールを使用すると、いくつかの欠点があります。 たとえば、ユーザーコントロールの位置を変更するには、サイト全体で複数のページを変更する必要があります。 ユーザーコントロールは、ページに挿入された後にデザインビューでレンダリングされることもありません。

ASP.NET 2.0 では、一貫性のあるルックアンドフィールを維持するための方法としてマスターページが導入されています。また、マスターページは、ユーザー制御方法に対する大幅な改善を表します。

## <a name="why-master-pages"></a>マスターページの理由

マスターページが ASP.NET 2.0 で必要だったのはなぜでしょうか。 結局のところ、Web サイトの開発者は、ASP.NET 1.x のユーザーコントロールを使用して、ページ間でコンテンツ領域を共有しています。 ユーザーコントロールは、一般的なレイアウトを作成するための最適なソリューションではないため、実際にはいくつかの理由があります。

ユーザーコントロールは、実際にはページレイアウトを定義しません。 代わりに、ページの一部のレイアウトと機能を定義します。 この2つを区別することは、ユーザーコントロールソリューションの管理をはるかに困難にするために重要です。 たとえば、ページ上のユーザーコントロールの位置を変更する場合は、ユーザーコントロールが表示される実際のページを編集する必要があります。 わずかな数のページがあり、大規模なサイトでは、すぐにサイトの管理が困難になるという拡張子があります。

一般的なレイアウトを定義するためにユーザーコントロールを使用するもう1つの欠点は、ASP.NET 自体のアーキテクチャに基づいています。 ユーザーコントロールのパブリックメンバーが変更された場合は、ユーザーコントロールを使用するすべてのページを再コンパイルする必要があります。 次に、ASP.NET は、最初にアクセスされたときにページを再 JIT します。 この場合も、拡張性のないアーキテクチャと、大規模なサイトに対するサイト管理の問題が生成されます。

これらの問題 (およびその他多数) は、ASP.NET 2.0 のマスターページで適切に対処されています。

## <a name="how-master-pages-work"></a>マスターページの動作

マスターページは、他のページのテンプレートに似ています。 他のページ間で共有する必要のあるページ要素 (メニュー、罫線など) は、マスターページに追加されます。 新しいページがサイトに追加されると、それらをマスターページに関連付けることができます。 マスターページに関連付けられているページは、**コンテンツページ**と呼ばれます。 既定では、コンテンツページはマスターページから表示されます。 ただし、マスターページを作成するときに、コンテンツページが独自のコンテンツと置き換えることができるページの部分を定義できます。 これらの部分は、ASP.NET 2.0 で導入された新しいコントロールを使用して定義されます。**ContentPlaceHolder**コントロールです。

マスターページには、任意の数の ContentPlaceHolder コントロールを含めることができます (またはまったくありません)。[コンテンツ] ページでは、ContentPlaceHolder コントロールの内容が、ASP.NET 2.0 の別の新しいコントロールである**コンテンツ**コントロール内に表示されます。 既定では、コンテンツページのコンテンツコントロールは空であるため、独自のコンテンツを提供できます。 コンテンツコントロール内のマスターページからコンテンツを使用する場合は、このモジュールで後ほど説明するように、この操作を行うことができます。 コンテンツコントロールは、コンテンツコントロールの ContentPlaceHolderID 属性を使用して ContentPlaceHolder コントロールにマップされます。 次のコードでは、マスターページの mainBody という ContentPlaceHolder コントロールにコンテンツコントロールをマップしています。

[!code-aspx[Main](master-pages/samples/sample1.aspx)]

> [!NOTE]
> 多くの場合、ユーザーは他のページの基本クラスとしてマスターページを説明しています。 拡張子は実際には true ではありません。 マスターページとコンテンツページ間のリレーションシップは、継承の1つではありません。

**図 1**は、Visual Studio 2005 で表示されるマスターページと関連するコンテンツページを示しています。 ContentPlaceHolder コントロールは、マスターページと、コンテンツページの対応するコンテンツコントロールで確認できます。 ContentPlaceHolder の外部にあるマスターページのコンテンツは表示されますが、コンテンツページで灰色表示になっています。 コンテンツページで supplanted できるのは、ContentPlaceHolder 内のコンテンツのみです。 マスターページから取得したその他のすべてのコンテンツは変更できません。

![マスターページとそれに関連付けられているコンテンツページ](master-pages/_static/image1.jpg)

**図 1**: マスターページとそれに関連付けられたコンテンツページ

## <a name="creating-a-master-page"></a>マスターページの作成

新しいマスターページを作成するには:

1. Visual Studio 2005 を開き、新しい Web サイトを作成します。
2. [ファイル]、[新規作成]、[ファイル] をクリックします。
3. **図 2**に示すように、[新しい項目の追加] ダイアログで [マスターファイル] を選択します。
4. [追加] をクリックします。

![新しいマスターページの作成](master-pages/_static/image2.jpg)

**図 2**: 新しいマスターページの作成

マスターページのファイル拡張子は *.master*です。 これは、マスターページが通常のページと異なる方法の1つです。 もう1つの主な違いは、@Page ディレクティブの代わりに、マスターページに @Master ディレクティブが含まれていることです。 先ほど作成したマスターページのソースビューに切り替えて、コードを確認します。

新しいマスターページには、既定で1つの ContentPlaceHolder コントロールがあります。 ほとんどの場合、最初に共通ページ要素を作成し、次にカスタムコンテンツを必要とする ContentPlaceHolder コントロールを挿入する方が理にかなっています。 このような場合、開発者は、既定の ContentPlaceHolder コントロールを削除し、ページの開発時に新しいコントロールを挿入する必要があります。 ContentPlaceHolder コントロールには、サイズ変更ハンドルが表示されるのに対して、サイズを変更することはできません。 ContentPlaceHolder コントロールは、含まれているコンテンツに基づいて、1つの例外で自動的にサイズを調整します。ContentPlaceHolder コントロールを、テーブルセルなどのブロック要素内に配置すると、要素のサイズに応じてサイズが変更されます。

## <a name="lab-1-working-with-master-pages"></a>ラボ1マスターページの操作

このラボでは、新しいマスターページを作成し、3つの ContentPlaceHolder コントロールを定義します。 次に、新しいコンテンツページを作成し、少なくとも1つの ContentPlaceHolder コントロールの内容を置き換えます。

1. マスターページを作成し、ContentPlaceHolder コントロールを挿入します。 

    1. 上の説明に従って、新しいマスターページを作成します。
    2. 既定の ContentPlaceHolder コントロールを削除します。
    3. コントロールの上の灰色の境界線をクリックして ContentPlaceHolder コントロールを選択し、キーボードの DEL キーを押して削除します。
    4. 図3に示すように、*ヘッダーとサイド*テンプレートを使用して新しいテーブルを挿入します。 テーブル全体がデザイナーに表示されるように、幅と高さをそれぞれ90% に変更します。

![](master-pages/_static/image3.jpg)

**図 3**

1. テーブルの各セルにカーソルを置き、[*縦*] プロパティを [*上*] に設定します。
2. [ツールボックス] から、テーブルの一番上のセル (ヘッダーセル) に ContentPlaceHolder コントロールを挿入します。
3. この ContentPlaceHolder コントロールを挿入すると、図4に示すように、行の高さはページ全体を占めることになります。 この点について心配する必要はありません。

![空のスペースは、ContentPlaceHolder と同じセルにあります。](master-pages/_static/image1.gif)

**図 4**: 空の領域が ContentPlaceHolder と同じセルに含まれる

1. ContentPlaceHolder コントロールを他の2つのセルに配置します。 他の ContentPlaceHolder コントロールが挿入されたら、テーブルセルのサイズは予想どおりになります。 このページは、**図 5**に示すページのようになります。

![すべての ContentPlaceHolder コントロールを持つマスター。 ヘッダーセルのセルの高さが次のようになっていることに注意してください。](master-pages/_static/image2.gif)

**図 5**: すべての ContentPlaceHolder コントロールを含むマスター ヘッダーセルのセルの高さが次のようになっていることに注意してください。

1. 3つの ContentPlaceHolder コントロールそれぞれに、任意のテキストを入力します。
2. マスターページを exercise1 として保存します。
3. 新しい Web フォームを作成し、exercise1 マスターページに関連付けます。
4. Visual Studio 2005 で [ファイル]、[新規作成]、[ファイル] を選択します。
5. 新しい項目の追加 ダイアログボックスで  **Web フォーム** を選択します。
6. 図6に示すように、[マスターページの選択] チェックボックスがオンになっていることを確認します。

![新しいコンテンツページの追加](master-pages/_static/image3.gif)

**図 6**: 新しいコンテンツページを追加する

1. [追加] をクリックします。
2. 図7に示すように、[マスターページの選択] ダイアログで [exercise1] を選択します。
3. [OK] をクリックして、新しいコンテンツページを追加します。

Visual Studio に [新しいコンテンツ] ページが表示され、マスターページの各 ContentPlaceHolder コントロールに対して1つのコンテンツコントロールが表示されます。 既定では、コンテンツコントロールは空であるため、独自のコンテンツを追加できます。 マスターページの ContentPlaceHolder コントロールのコンテンツを使用する場合は、**図 8**に示すように、スマートタグシンボル (コントロールの右上隅の小さな黒い矢印) をクリックし、[既定] を選択します。これにより、スマートタグから*マスターコンテンツを*選択できます。 これを行うと、メニュー項目が変更され、*カスタムコンテンツが作成*されます。 その時点でクリックすると、マスターページからコンテンツが削除され、その特定のコンテンツコントロールのカスタムコンテンツを定義できるようになります。

![マスターページのコンテンツに対するコンテンツコントロールの既定値の設定](master-pages/_static/image4.gif)

**図 7**: マスターページのコンテンツに対してコンテンツコントロールを既定に設定する

## <a name="connecting-master-page-and-content-pages"></a>マスターページとコンテンツページの接続

マスターページとコンテンツページ間の関連付けは、次の4つの方法のいずれかで構成できます。

- @Page ディレクティブの<strong>MasterPageFile</strong>属性
- コードで**MasterPageFile**プロパティを設定します。
- アプリケーション構成ファイル内の **&lt;ページ&gt;** 要素 (アプリケーションのルートフォルダー内の web.config)
- サブフォルダー構成ファイル内の **&lt;ページ&gt;** 要素 (サブフォルダー内の web.config)

## <a name="masterpagefile-attribute"></a>MasterPageFile 属性

MasterPageFile 属性を使用すると、特定の ASP.NET ページにマスターページを簡単に適用できます。 また、演習1で行ったように **[マスターページの選択**] チェックボックスをオンにしたときにマスターページを適用するために使用される方法でもあります。

## <a name="setting-pagemasterpagefile-in-code"></a>コードでの MasterPageFile の設定

コードで MasterPageFile プロパティを設定することにより、実行時に特定のマスターページをコンテンツに適用できます。 これは、ユーザーロールまたはその他の条件に基づいて特定のマスターページを適用する必要がある場合に便利です。 MasterPageFile プロパティは、PreInit メソッドで設定する必要があります。 PreInit メソッドの後に設定されている場合は、InvalidOperationException がスローされます。 このプロパティが設定されているページには、ページのトップレベルコントロールとしてコンテンツコントロールも必要です。 それ以外の場合は、MasterPageFile プロパティが設定されると HttpException がスローされます。

## <a name="using-the-ltpagesgt-element"></a>&lt;pages&gt; 要素の使用

Web.config ファイルの &lt;pages&gt; 要素で masterPageFile 属性を設定することにより、ページのマスターページを構成できます。 この方法を使用する場合は、アプリケーション構造の下位にある web.config ファイルでこの設定をオーバーライドできることに注意してください。 @Page ディレクティブで設定されたすべての MasterPageFile 属性もこの設定をオーバーライドします。 &lt;pages&gt; 要素を使用すると、特定のフォルダーまたはファイルで必要に応じて上書きできる*マスター*マスターページを簡単に作成できます。

## <a name="properties-in-master-pages"></a>マスターページのプロパティ

マスターページは、これらのプロパティをマスターページ内でパブリックにするだけで、プロパティを公開できます。 たとえば、次のコードでは、プロパティという名前のプロパティを定義しています。

[!code-csharp[Main](master-pages/samples/sample2.cs)]

[コンテンツ] ページから "プロパティ" プロパティにアクセスするには、次のように Master プロパティを使用する必要があります。

[!code-csharp[Main](master-pages/samples/sample3.cs)]

## <a name="nesting-master-pages"></a>入れ子になったマスターページ

マスターページは、大規模な Web アプリケーションでよく見られるルックアンドフィールを確保するための最適なソリューションです。 ただし、大規模なサイトの特定の部分が共通のインターフェイスを共有し、他の部分が別のインターフェイスを共有することは珍しくありません。 このニーズに対処するために、複数のマスターページが最適なソリューションです。 ただし、それでも、大規模なアプリケーションでは、サイトの特定のセクション間でのみ共有されているすべてのページとその他のコンポーネントの間で共有されている特定のコンポーネント (たとえば、メニューなど) を持つことができるとは限りません。 このような状況では、入れ子になったマスターページが必要になります。 既に説明したように、通常のマスターページはマスターページとコンテンツページで構成されています。 入れ子になったマスターページの場合は、2つのマスターページがあります。親マスターと子マスター。 子マスターページもコンテンツページであり、そのマスターは親マスターページです。

一般的なマスターページのコードを次に示します。

[!code-aspx[Main](master-pages/samples/sample4.aspx)]

入れ子になったマスターシナリオでは、これが親マスターになります。 別のマスターページでは、このページをマスターページとして使用し、そのコードは次のようになります。

[!code-aspx[Main](master-pages/samples/sample5.aspx)]

このシナリオでは、子マスターは親マスターのコンテンツページでもあることに注意してください。 子マスターのコンテンツはすべて、親の ContentPlaceHolder コントロールからそのコンテンツを取得するコンテンツコントロール内に表示されます。

> [!NOTE]
> デザイナーのサポートは、入れ子になったマスターページでは使用できません。 入れ子になったマスターを使用して開発する場合は、ソースビューを使用する必要があります。

このビデオでは、入れ子になったマスターページの使用に関するチュートリアルを紹介します。

![](master-pages/_static/image1.png)

[全画面表示のビデオを開く](master-pages/_static/nested1.wmv)

![マスターページの選択](master-pages/_static/image4.jpg)

**図 8**: マスターページの選択
