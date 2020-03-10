---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-3
title: 'パート 3: レイアウトとカテゴリのメニュー |Microsoft Docs'
author: JoeStagner
description: このチュートリアルシリーズでは、Tailspin Spyworks サンプルアプリケーションを構築するために実行するすべての手順について詳しく説明します。 パート3では、レイアウトとカテゴリメニューの追加について説明します。
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 94ea1a70-a9bc-4241-8f36-08366d64bab9
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-3
msc.type: authoredcontent
ms.openlocfilehash: a223b97fd362ecf73ecde431e141021c1dcc6a6d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78519100"
---
# <a name="part-3-layout-and-category-menu"></a>パート 3: レイアウトとカテゴリメニュー

[Joe Stagner](https://github.com/JoeStagner)

> Tailspin Spyworks は、.NET プラットフォーム用の強力でスケーラブルなアプリケーションを簡単に作成する方法を示しています。 ASP.NET 4 の優れた新機能を使用して、ショッピング、チェックアウト、管理などのオンラインストアを構築する方法を示しています。
> 
> このチュートリアルシリーズでは、Tailspin Spyworks サンプルアプリケーションを構築するために実行するすべての手順について詳しく説明します。 パート3では、レイアウトとカテゴリメニューの追加について説明します。

## <a id="_Toc260221669"></a>レイアウトとカテゴリメニューを追加する

サイトマスターページで、左側の列に、製品カテゴリメニューを含む div を追加します。

[!code-aspx[Main](tailspin-spyworks-part-3/samples/sample1.aspx)]

必要な配置とその他の書式設定は、スタイルの .css ファイルに追加した CSS クラスによって提供されることに注意してください。

[!code-css[Main](tailspin-spyworks-part-3/samples/sample2.css)]

製品カテゴリのメニューは実行時に動的に作成されます。そのためには、既存の製品カテゴリを Commerce データベースに照会し、メニュー項目と対応するリンクを作成します。

これを実現するには、2つの ASP を使用します。NET の強力なデータコントロール。 "Entity Data Source" コントロールと "ListView" コントロール。

![](tailspin-spyworks-part-3/_static/image1.jpg)

[デザインビュー] に切り替えて、ヘルパーを使用してコントロールを構成します。

![](tailspin-spyworks-part-3/_static/image2.jpg)

EntityDataSource ID プロパティを EDS\_Category\_ に設定し、データソースの構成 をクリックしてみましょう。

![](tailspin-spyworks-part-3/_static/image3.jpg)

コマースデータベースのエンティティデータソースモデルを作成したときに作成された CommerceEntities 接続を選択し、[次へ] をクリックします。

![](tailspin-spyworks-part-3/_static/image4.jpg)

[カテゴリ] エンティティセット名を選択し、残りのオプションは既定値のままにします。 [完了] をクリックします。

次に、ページに配置した ListView コントロールインスタンスの ID プロパティを ListView\_[製品] メニューに設定し、ヘルパーをアクティブ化します。

![](tailspin-spyworks-part-3/_static/image5.jpg)

コントロールオプションを使用してデータ項目の表示と書式設定を書式設定することもできますが、メニューの作成では、ソースビューにコードを入力するだけで、単純なマークアップが必要になります。

[!code-aspx[Main](tailspin-spyworks-part-3/samples/sample3.aspx)]

"Eval" ステートメントに注意してください: &lt;% # Eval ("区分番号")%&gt;

ASP.NET 構文 &lt;% #%&gt; は、その中に含まれるものを実行するようにランタイムに指示し、結果を "行" で出力するための短縮規約です。

ステートメント Eval ("区分名") は、バインドされたデータ項目のコレクション内の現在のエントリについて、エンティティモデル項目名 "の値" "区分名" の値をフェッチするように指示します。 これは、非常に強力な機能を使用するための簡潔な構文です。

アプリケーションをすぐに実行できるようにします。

![](tailspin-spyworks-part-3/_static/image6.jpg)

[Product category] メニューが表示されるようになり、カテゴリメニュー項目のいずれかにマウスポインターを合わせると、ページへのメニュー項目のリンクポイントが表示されます。ここでは、名前付きの製品リストを実装し、動的なクエリ文字列引数を カテゴリ id。

> [!div class="step-by-step"]
> [前へ](tailspin-spyworks-part-2.md)
> [次へ](tailspin-spyworks-part-4.md)
