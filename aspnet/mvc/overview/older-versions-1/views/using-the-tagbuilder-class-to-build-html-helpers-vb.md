---
uid: mvc/overview/older-versions-1/views/using-the-tagbuilder-class-to-build-html-helpers-vb
title: TagBuilder クラスを使用して HTML ヘルパーを構築する (VB) |Microsoft Docs
author: StephenWalther
description: Stephen Walther には、TagBuilder クラスという名前の ASP.NET MVC フレームワークの便利なユーティリティクラスが導入されています。 TagBuilder クラスは簡単に使用できます。
ms.author: riande
ms.date: 03/02/2009
ms.assetid: ec26f264-d0ea-4031-9943-825505a3ac4b
msc.legacyurl: /mvc/overview/older-versions-1/views/using-the-tagbuilder-class-to-build-html-helpers-vb
msc.type: authoredcontent
ms.openlocfilehash: 3b0aa9816209cc326d3dea4b8dfb1b13cf697fcd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78485584"
---
# <a name="using-the-tagbuilder-class-to-build-html-helpers-vb"></a>TagBuilder クラスを使用して HTML ヘルパーを構築する (VB)

[Stephen Walther](https://github.com/StephenWalther)

> Stephen Walther には、TagBuilder クラスという名前の ASP.NET MVC フレームワークの便利なユーティリティクラスが導入されています。 TagBuilder クラスを使用すると、HTML タグを簡単に作成できます。

ASP.NET MVC フレームワークには、HTML ヘルパーを構築するときに使用できる TagBuilder クラスという便利なユーティリティクラスが含まれています。 TagBuilder クラスは、クラスの名前として、HTML タグを簡単に作成できるようにします。 この簡単なチュートリアルでは、TagBuilder クラスの概要を説明し、HTML &lt;img&gt; タグをレンダリングする単純な HTML ヘルパーを構築するときに、このクラスを使用する方法を学習します。

## <a name="overview-of-the-tagbuilder-class"></a>TagBuilder クラスの概要

TagBuilder クラスは、System.web 名前空間に含まれています。 次の5つの方法があります。

- AddCssClass () –タグに新しい*class = ""* 属性を追加できます。
- GenerateId () –タグに id 属性を追加できます。 このメソッドは、自動的に id の期間を置き換えます (既定では、ピリオドはアンダースコアに置き換えられます)
- MergeAttribute () –タグに属性を追加できます。 このメソッドには複数のオーバーロードがあります。
- SetInnerText () –タグの内部テキストを設定できます。 内部テキストは、自動的に HTML エンコードされます。
- ToString () –タグを表示できます。 通常のタグ、開始タグ、終了タグ、または自己終了タグを作成するかどうかを指定できます。

TagBuilder クラスには、次の4つの重要なプロパティがあります。

- Attributes –タグのすべての属性を表します。
- IdAttributeDotReplacement – GenerateId () メソッドがピリオドを置き換えるために使用する文字を表します (既定値はアンダースコアです)。
- InnerHTML –タグの内部コンテンツを表します。 このプロパティに文字列を割り当てると、文字列は HTML エンコード*されません*。
- TagName –タグの名前を表します。

これらのメソッドとプロパティは、HTML タグを構築するために必要なすべての基本メソッドとプロパティを提供します。 実際に TagBuilder クラスを使用する必要はありません。 代わりに StringBuilder クラスを使用することもできます。 しかし、TagBuilder クラスを使用すると、作業が楽になります。

## <a name="creating-an-image-html-helper"></a>イメージ HTML ヘルパーの作成

TagBuilder クラスのインスタンスを作成するときに、TagBuilder コンストラクターにビルドするタグの名前を渡します。 次に、AddCssClass メソッドや MergeAttribute () メソッドなどのメソッドを呼び出して、タグの属性を変更できます。 最後に、ToString () メソッドを呼び出してタグを表示します。

たとえば、リスト1には、イメージ HTML ヘルパーが含まれています。 イメージヘルパーは、HTML &lt;img&gt; タグを表す TagBuilder を使用して内部的に実装されます。

**リスト1– & # 1-イメージ \ イメージ**

[!code-vb[Main](using-the-tagbuilder-class-to-build-html-helpers-vb/samples/sample1.vb)]

リスト1のモジュールには、Image () という名前のオーバーロードされたメソッドが2つ含まれています。 Image () メソッドを呼び出すと、HTML 属性のセットを表すオブジェクトを渡すことができます。

Tagbuilder. MergeAttribute () メソッドを使用して、src 属性などの個々の属性を TagBuilder に追加する方法に注意してください。 さらに、tagbuilder に属性のコレクションを追加する方法についても説明しています。 MergeAttributes () メソッドは、ディクショナリ&lt;string、object&gt; パラメーターを受け取ります。 RouteValueDictionary クラスは、属性のコレクションを表すオブジェクトを、文字列、オブジェクト&gt;&lt;ディクショナリに変換するために使用されます。

イメージヘルパーを作成した後は、他の標準 HTML ヘルパーと同様に、ASP.NET MVC ビューでヘルパーを使用できます。 リスト2のビューでは、イメージヘルパーを使用して Xbox の同じイメージが2回表示されます (図1を参照)。 Image () ヘルパーは、HTML 属性コレクションの有無にかかわらず呼び出されます。

**リスティング2–ホーム**

[!code-aspx[Main](using-the-tagbuilder-class-to-build-html-helpers-vb/samples/sample2.aspx)]

[[新しいプロジェクト] ダイアログボックスの ![](using-the-tagbuilder-class-to-build-html-helpers-vb/_static/image1.jpg)](using-the-tagbuilder-class-to-build-html-helpers-vb/_static/image1.png)

**図 01**: イメージヘルパーを使用[する (クリックすると、フルサイズの画像が表示](using-the-tagbuilder-class-to-build-html-helpers-vb/_static/image2.png)されます)

イメージヘルパーに関連付けられている名前空間を、インデックス .aspx ビューの先頭にインポートする必要があることに注意してください。 ヘルパーは、次のディレクティブを使用してインポートされます。

[!code-aspx[Main](using-the-tagbuilder-class-to-build-html-helpers-vb/samples/sample3.aspx)]

Visual Basic アプリケーションでは、既定の名前空間はアプリケーションの名前と同じです。

> [!div class="step-by-step"]
> [前へ](creating-custom-html-helpers-vb.md)
> [次へ](creating-page-layouts-with-view-master-pages-vb.md)
