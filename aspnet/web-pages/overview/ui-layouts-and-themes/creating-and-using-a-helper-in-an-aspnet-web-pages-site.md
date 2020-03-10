---
uid: web-pages/overview/ui-layouts-and-themes/creating-and-using-a-helper-in-an-aspnet-web-pages-site
title: ASP.NET Web ページ (Razor) サイトでのヘルパーの作成と使用 |Microsoft Docs
author: Rick-Anderson
description: この記事では、ASP.NET Web ページ (Razor) web サイトにヘルパーを作成する方法について説明します。 ヘルパーは再利用可能なコンポーネントであり、コードと、パフォーマンスに対するマークアップを含んでいます...
ms.author: riande
ms.date: 02/17/2014
ms.assetid: 46bff772-01e0-40f0-9ae6-9e18c5442ee6
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/creating-and-using-a-helper-in-an-aspnet-web-pages-site
msc.type: authoredcontent
ms.openlocfilehash: 380663951094c9fc7d5f0601e30995fa073a204b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78454306"
---
# <a name="creating-and-using-a-helper-in-an-aspnet-web-pages-razor-site"></a>ASP.NET Web ページ (Razor) サイトでのヘルパーの作成と使用

[Tom FitzMacken](https://github.com/tfitzmac)

> この記事では、ASP.NET Web ページ (Razor) web サイトにヘルパーを作成する方法について説明します。 *ヘルパー*は、煩雑または複雑なタスクを実行するためのコードとマークアップを含む再利用可能なコンポーネントです。
> 
> **学習内容:** 
> 
> - 単純なヘルパーを作成して使用する方法。
> 
> この記事で導入された ASP.NET 機能を次に示します。
> 
> - `@helper` 構文。
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>このチュートリアルで使用されているソフトウェアのバージョン
> 
> 
> - ASP.NET Web ページ (Razor) 3
>   
> 
> このチュートリアルは ASP.NET Web ページ2でも動作します。

## <a name="overview-of-helpers"></a>ヘルパーの概要

サイト内の異なるページで同じタスクを実行する必要がある場合は、ヘルパーを使用できます。 ASP.NET Web ページには多くのヘルパーが含まれており、ダウンロードしてインストールすることもできます。 (ASP.NET Web ページの組み込みヘルパーの一覧については、「 [ASP.NET API クイックリファレンス](https://go.microsoft.com/fwlink/?LinkId=202907)」を参照してください)。既存のヘルパーがニーズに合わない場合は、独自のヘルパーを作成することができます。

ヘルパーを使用すると、複数のページで共通のコードブロックを使用できます。 ページ内で通常の段落とは別に設定されたノート項目を作成することがよくあるとします。 メモは、境界線を持つボックスとしてスタイルを作成する `<div>` 要素として作成される場合があります。 メモを表示するたびに、この同じマークアップをページに追加するのではなく、マークアップをヘルパーとしてパッケージ化することができます。 その後、必要な場所に1行のコードでメモを挿入できます。

このようなヘルパーを使用すると、各ページのコードがより簡単に読みやすくなります。 また、ノートの外観を変更する必要がある場合は、マークアップを1か所で変更できるので、サイトの保守が容易になります。

## <a name="creating-a-helper"></a>ヘルパーの作成

この手順では、説明したように、メモを作成するヘルパーを作成する方法を示します。 これは簡単な例ですが、カスタムヘルパーには、必要なマークアップと ASP.NET のコードを含めることができます。

1. Web サイトのルートフォルダーで、 *App\_Code*という名前のフォルダーを作成します。 これは ASP.NET で予約されているフォルダー名であり、ヘルパーなどのコンポーネントのコードを配置できます。
2. *アプリ\_コード*フォルダーで、新しい*cshtml*ファイルを作成し、 *myhelpers. cshtml*という名前を指定します。
3. 既存のコンテンツを次の内容に置き換えます。

    [!code-cshtml[Main](creating-and-using-a-helper-in-an-aspnet-web-pages-site/samples/sample1.cshtml)]

    このコードでは、`@helper` 構文を使用して `MakeNote`という名前の新しいヘルパーを宣言します。 この特定のヘルパーを使用すると、テキストとマークアップの組み合わせを含むことができる `content` という名前のパラメーターを渡すことができます。 ヘルパーは、`@content` 変数を使用して、ノート本体に文字列を挿入します。

    このファイルは*myhelpers. cshtml*という名前であることに注意してください。ヘルパーには `MakeNote`という名前が付けられています。 複数のカスタムヘルパーを1つのファイルに含めることができます。
4. ファイルを保存して閉じます。

## <a name="using-the-helper-in-a-page"></a>ページでのヘルパーの使用

1. ルートフォルダーに、 *TestHelper*という名前の新しい空のファイルを作成します。
2. 次のコードをファイルに追加します。

    [!code-html[Main](creating-and-using-a-helper-in-an-aspnet-web-pages-site/samples/sample2.html)]

    作成したヘルパーを呼び出すには、`@` を使用し、その後にヘルパーがあるファイル名、ドット、ヘルパー名を指定します。 (*アプリ\_コード*フォルダーに複数のフォルダーがある場合は、`@FolderName.FileName.HelperName` 構文を使用して、入れ子になったフォルダーレベルでヘルパーを呼び出すことができます)。 かっこ内に引用符で囲んだテキストは、ヘルパーが web ページのノートの一部として表示されるテキストです。
3. ページを保存し、ブラウザーで実行します。 ヘルパーは、2つの段落の間でヘルパーを呼び出したときに、ノート項目の右側を生成します。

    ![ブラウザー内のページを示すスクリーンショットと、指定したテキストをボックスに配置するためのマークアップをヘルパーが生成した方法を示します。](creating-and-using-a-helper-in-an-aspnet-web-pages-site/_static/image1.png)

## <a name="additional-resources"></a>その他のリソース

[Razor ヘルパーとしての水平メニュー](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2341)。 Mike Pope によるこのブログエントリは、マークアップ、CSS、およびコードを使用して、水平メニューをヘルパーとして作成する方法を示しています。

[WebMatrix と ASP.NET MVC3 の ASP.NET Web ページヘルパーでの HTML5 の活用](http://geekswithblogs.net/wildturtle/archive/2010/11/08/html5-in-asp.net-web-pages-helpers-for-webmatrix-and_aspnet_mvc3.aspx)。 Sam Abraham によるこのブログエントリは、HTML5 `Canvas` 要素をレンダリングするヘルパーを示しています。

[WebMatrix での @Helpers と @Functions の違い](http://www.mikesdotnetting.com/Article/173/The-Difference-Between-@Helpers-and-@Functions-In-WebMatrix)。 Mike Brind によるこのブログエントリでは、`@helper` 構文と `@function` 構文、およびそれぞれを使用するタイミングについて説明します。
