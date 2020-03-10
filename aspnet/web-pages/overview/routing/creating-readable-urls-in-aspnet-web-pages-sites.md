---
uid: web-pages/overview/routing/creating-readable-urls-in-aspnet-web-pages-sites
title: ASP.NET Web ページ (Razor) サイトで読み取り可能な Url を作成する |Microsoft Docs
author: Rick-Anderson
description: この記事では、ASP.NET Web ページ (Razor) web サイトでのルーティングについて説明します。また、これにより、SEO により読みやすく、より優れた Url を使用する方法についても説明します。 作業内容
ms.author: riande
ms.date: 02/17/2014
ms.assetid: a8aac1ac-89de-4415-afe0-97a41c6423d2
msc.legacyurl: /web-pages/overview/routing/creating-readable-urls-in-aspnet-web-pages-sites
msc.type: authoredcontent
ms.openlocfilehash: 832db8e144cab730f16c78f67c12feb9b7c92c7c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78509908"
---
# <a name="creating-readable-urls-in-aspnet-web-pages-razor-sites"></a>ASP.NET Web ページ (Razor) サイトでの読み取り可能な Url の作成

[Tom FitzMacken](https://github.com/tfitzmac)

> この記事では、ASP.NET Web ページ (Razor) web サイトでのルーティングについて説明します。また、これにより、SEO により読みやすく、より優れた Url を使用する方法についても説明します。
> 
> ここでは、次の内容について学習します。
> 
> - ASP.NET がルーティングを使用して、より読みやすく検索可能な Url を使用できるようにする方法。
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>このチュートリアルで使用されているソフトウェアのバージョン
> 
> 
> - ASP.NET Web ページ (Razor) 3
>   
> 
> このチュートリアルは ASP.NET Web ページ2でも動作します。

## <a name="about-routing"></a>ルーティングについて

サイト内のページの Url は、サイトの動作に影響を与える可能性があります。 &quot; &quot;やすい URL を使用すると、簡単にサイトを使用できます。 また、サイトの検索エンジン最適化 (SEO) にも役立ちます。 ASP.NET websites には、フレンドリな Url を自動的に使用する機能が含まれています。

ASP.NET を使用すると、サーバー上のファイルを指すのではなく、ユーザーの操作を記述する意味のある Url を作成できます。 架空のブログについては、次の Url を検討してください。

- `http://www.contoso.com/Blog/blog.cshtml?categories=hardware`
- `http://www.contoso.com//Blog/blog.cshtml?startdate=2009-11-01&enddate=2009-11-30`

これらの Url を次の Url と比較します。

- `http://www.contoso.com/Blog/categories/hardware/`
- `http://www.contoso.com/Blog/2009/November`

最初のペアで*は、blog ページを*使用してブログが表示されていることをユーザーが認識する必要があり、その後、適切なカテゴリまたは日付範囲を取得するクエリ文字列を作成する必要があります。 2番目の例のセットは、理解しやすく作成するのがはるかに簡単です。

最初の例の Url も、特定のファイル (*blog*) を直接指しています。 何らかの理由でブログがサーバー上の別のフォルダーに移動された場合、または別のページを使用するようにブログが書き換えられた場合、リンクは間違っています。 2番目の Url のセットは特定のページを指していないので、ブログの実装や場所が変更された場合でも、Url は引き続き有効になります。

ASP.NET Web ページでは、ASP.NET が*ルーティング*を使用するため、上記の例のようなわかりやすい url を作成できます。 ルーティングにより、URL から要求を満たすことができるページ (またはページ) への論理マッピングが作成されます。 マッピングは論理的なものであり (物理的ではなく、特定のファイルに対するものではありません)、ルーティングによって、サイトの Url を定義する方法が非常に柔軟になります。

## <a name="how-routing-works"></a>ルーティングのしくみ

ASP.NET が要求を処理するときに、URL を読み取り、その要求をルーティングする方法を決定します。 ASP.NET は、URL の個々のセグメントを、左から右に、ディスク上のファイルに一致させようとします。 一致するものがある場合、URL に残っているものは*パス情報*としてページに渡されます。

この URL を使用してだれかが要求を行うとします。

`http://www.contoso.com/a/b/c`

検索は次のようになります。

1. */A/b/c.cshtml*のパスと名前を持つファイルはありますか。 その場合は、そのページを実行し、情報を渡しません。 それ以外の場合:
2. */A/b.cshtml*のパスと名前を持つファイルはありますか。 その場合は、そのページを実行し、`c` の値を渡します。 それ以外の場合...
3. */A.cshtml*のパスと名前を持つファイルはありますか。 その場合は、そのページを実行し、`b/c` の値を渡します。

指定されたフォルダー内のファイル*の完全*一致が検索で見つからなかった場合、ASP.NET は引き続きこれらのファイルを検索します。

1. */a/b/c/default.cshtml* (パス情報なし)。
2. */a/b/c/index.cshtml* (パス情報なし)。

> [!NOTE]
> 明確にするために、特定のページ (つまり、ファイル名拡張子が*cshtml*の要求) の要求は、期待したとおりに動作します。 `http://www.contoso.com/a/b.cshtml` のような要求では、ページ*b.* を正常に実行します。

ページ内では、ページの `UrlData` プロパティ (ディクショナリ) を使用してパス情報を取得できます。 *Viewcustomers. cshtml*という名前のファイルがあり、サイトが次の要求を取得しているとします。

`http://mysite.com/myWebSite/ViewCustomers/1000`

上記のルールで説明したように、要求はページに送られます。 ページ内で、次のようなコードを使用して、パス情報を取得して表示できます (この場合は、1000&quot;&quot;値)。

[!code-html[Main](creating-readable-urls-in-aspnet-web-pages-sites/samples/sample1.html)]

> [!NOTE]
> ルーティングには完全なファイル名が含まれないため、同じ名前でファイル名拡張子が異なるページ ( *MyPage*や*MyPage*など) がある場合は、あいまいになる可能性があります。 ルーティングに関する問題を回避するために、サイト内のページの名前が拡張子だけで異なることを確認することをお勧めします。

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>その他のリソース

[WebMatrix-SEO の url、UrlData、および Routing](http://www.mikesdotnetting.com/Article/165/WebMatrix-URLs-UrlData-and-Routing-for-SEO)。 Mike Brind によるこのブログエントリでは、ASP.NET Web ページでのルーティングのしくみについてさらに詳しく説明します。
