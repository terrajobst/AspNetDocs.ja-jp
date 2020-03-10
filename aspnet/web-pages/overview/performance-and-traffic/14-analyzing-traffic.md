---
uid: web-pages/overview/performance-and-traffic/14-analyzing-traffic
title: ASP.NET Web ページ (Razor) サイトのトラッキング訪問者情報 (Analytics)Microsoft Docs
author: Rick-Anderson
description: Web サイトのアクセスが完了したら、web サイトのトラフィックを分析することができます。
ms.author: riande
ms.date: 02/17/2014
ms.assetid: 360bc6e1-84c5-4b8e-a84c-ea48ab807aa4
msc.legacyurl: /web-pages/overview/performance-and-traffic/14-analyzing-traffic
msc.type: authoredcontent
ms.openlocfilehash: 095a5572c755446e0661c052ca9de82d636429fd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78421456"
---
# <a name="tracking-visitor-information-analytics-for-an-aspnet-web-pages-razor-site"></a>ASP.NET Web ページ (Razor) サイトのトラッキング訪問者情報 (Analytics)

[Tom FitzMacken](https://github.com/tfitzmac)

> この記事では、ヘルパーを使用して、ASP.NET Web ページ (Razor) web サイトのページに web サイトの分析を追加する方法について説明します。
> 
> ここでは、次の内容について学習します。
> 
> - Web サイトのトラフィックに関する情報を分析プロバイダーに送信する方法。
> 
> この記事で紹介する ASP.NET プログラミング機能を次に示します。
> 
> - `Analytics` ヘルパー。
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>このチュートリアルで使用されているソフトウェアのバージョン
> 
> 
> - ASP.NET Web ページ (Razor) 2
> - ASP.NET Web ヘルパーライブラリ (NuGet パッケージ)

Analytics は、ユーザーがサイトをどのように使用しているかを理解できるように、web サイトのトラフィックを測定するテクノロジの一般的な用語です。 Google、Yahoo、StatCounter などのサービスを含む多くの分析サービスを利用できます。

Analytics の機能として、分析プロバイダーを使用してアカウントにサインアップし、追跡するサイトを登録するという方法があります。プロバイダーは、お客様のアカウントの ID または追跡コードを含む JavaScript コードのスニペットを送信します。 JavaScript スニペットは、追跡するサイトの web ページに追加します。(通常、分析スニペットは、サイト内のすべてのページに表示されるフッターまたはレイアウトページやその他の HTML マークアップに追加します)。これらの JavaScript スニペットの1つが含まれているページをユーザーが要求すると、スニペットは現在のページに関する情報を分析プロバイダーに送信し、そのページに関するさまざまな詳細情報を記録します。

サイトの統計情報を確認するには、analytics プロバイダーの web サイトにログインします。 次のように、サイトに関するすべての種類のレポートを表示できます。

- 個々のページのページビューの数。 これにより、サイトにアクセスしているユーザーの数と、最も人気のあるサイトのページがわかります。
- 特定のページに対して、どのくらいの時間がかかっているか。 これにより、ホームページがユーザーの関心を持っているかどうかがわかります。
- サイトにアクセスする前に、どのサイトを使用していたか。 これにより、トラフィックがリンクから送信されるか、検索から送信されるかなどを把握できます。
- ユーザーがサイトにアクセスするときと、その期間の長さ。
- 訪問者の国を示します。
- 訪問者が使用しているブラウザーとオペレーティングシステム

    ![Ch14traffic-1](14-analyzing-traffic/_static/image1.jpg)

## <a name="using-a-helper-to-add-analytics-to-a-page"></a>ヘルパーを使用してページに Analytics を追加する

ASP.NET Web ページには、分析に使用される JavaScript スニペットを簡単に管理できるようにする分析ヘルパー (`Analytics.GetGoogleHtml`、`Analytics.GetYahooHtml`、および `Analytics.GetStatCounterHtml`) がいくつか含まれています。 JavaScript コードを配置する方法と場所を確認するのではなく、ヘルパーをページに追加するだけで済みます。 指定する必要がある情報は、アカウント名、ID、または追跡コードだけです。 (StatCounter の場合は、いくつかの追加の値も指定する必要があります)。

この手順では、`GetGoogleHtml` ヘルパーを使用するレイアウトページを作成します。 他のいずれかの分析プロバイダーを持つアカウントが既にある場合は、代わりにそのアカウントを使用し、必要に応じて微調整を行うことができます。

> [!NOTE]
> Analytics アカウントを作成するときに、追跡対象のサイトの URL を登録します。 ローカルコンピューター上のすべてをテストする場合は、実際のトラフィック (唯一のトラフィック) を追跡することはありません。そのため、サイトの統計情報を記録して表示することはできません。 ただし、この手順では、分析ヘルパーをページに追加する方法について説明します。 サイトを発行すると、ライブサイトから分析プロバイダーに情報が送信されます。

1. 「 [ASP.NET Web ページサイトにヘルパーをインストール](https://go.microsoft.com/fwlink/?LinkId=252372)する」の説明に従って、ASP.NET Web ヘルパーライブラリを web サイトに追加します (まだ追加していない場合)。
2. Google アナリティクスでアカウントを作成し、アカウント名を記録します。
3. *Analytics*という名前のレイアウトページを作成し、次のマークアップを追加します。

    [!code-cshtml[Main](14-analyzing-traffic/samples/sample1.cshtml)]

    > [!NOTE]
    > `Analytics` ヘルパーへの呼び出しは、(`</body>` タグの前に) web ページの本文に配置する必要があります。 そうしないと、ブラウザーでスクリプトが実行されません。

    別の分析プロバイダーを使用している場合は、代わりに次のいずれかのヘルパーを使用します。

    - (Yahoo) `@Analytics.GetYahooHtml("myaccount")`
    - (StatCounter) `@Analytics.GetStatCounterHtml("project", "security")`
4. `myaccount` は、手順 1. で作成したアカウントの名前、ID、または追跡コードに置き換えます。
5. ブラウザーでページを実行します。 (実行する前に、 **[ファイル]** ワークスペースでページが選択されていることを確認してください)。
6. ブラウザーでページソースを表示します。 表示される分析コードは次のようになります。

    [!code-html[Main](14-analyzing-traffic/samples/sample2.html)]
7. Google アナリティクスサイトにログオンし、サイトの統計情報を確認します。 ライブサイトでページを実行している場合は、アクセスをページに記録するエントリが表示されます。

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>その他のリソース

- [Google アナリティクスサイト](https://www.google.com/analytics/)
- [Yahoo! Web Analytics サイト](http://help.yahoo.com/l/us/yahoo/ywa/)
- [StatCounter サイト](http://statcounter.com/)
