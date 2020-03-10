---
uid: web-pages/overview/ui-layouts-and-themes/twitter-helper
title: ASP.NET Web ページ | を含む Twitter ヘルパーMicrosoft Docs
author: Rick-Anderson
description: このトピックとアプリケーションでは、Twitter ヘルパーを WebMatrix 3 プロジェクトに追加する方法について説明します。 これには Twitter ヘルパーコードが含まれており、ヘルパーを呼び出す方法を示しています...
ms.author: riande
ms.date: 11/26/2018
ms.assetid: c1a1244e-b9c8-42e6-a00b-8456a4ec027c
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/twitter-helper
msc.type: authoredcontent
ms.openlocfilehash: 76e32b7c808467a9a87c70017dac02bdb895e1df
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78518620"
---
# <a name="twitter-helper-with-aspnet-web-pages"></a>Twitter ヘルパーと ASP.NET Web ページ

[Tom FitzMacken](https://github.com/tfitzmac)

> [!IMPORTANT]
> Twitter ヘルパーは互換性のために残されています。 Twitter の web サイト用エンゲージメントツールについては、「 [Web サイトの twitter の概要](https://developer.twitter.com/en/docs/twitter-for-websites/overview)」を参照してください。

> このトピックとアプリケーションでは、Twitter ヘルパーを WebMatrix 3 プロジェクトに追加する方法について説明します。 これには Twitter ヘルパーコードが含まれており、ヘルパーメソッドを呼び出す方法を示しています。
> 
> Twitter ファイル用のこのコード**は、Microsoft によって開発**されました。
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>このチュートリアルで使用されているソフトウェアのバージョン
> 
> 
> - ASP.NET Web ページ (Razor) 3
>   
> 
> このチュートリアルは ASP.NET Web ページ2でも動作します。

## <a name="introduction"></a>はじめに

このトピックでは、アプリケーションに Twitter ヘルパーを追加し、Razor 構文を使用してヘルパーメソッドを呼び出す方法について説明します。 Twitter ヘルパーを使用すると、Twitter のボタンやウィジェットをアプリケーションに簡単に組み込むことができます。 ユーザーのタイムラインやハッシュタグの検索結果など、Twitter ウィジェットを使用するには、最初[に twitter でウィジェット](https://twitter.com/settings/widgets)を作成する必要があります。 ウィジェットを作成すると、ウィジェット id が表示されます。ウィジェットを表示するヘルパーメソッドを呼び出すときに、このウィジェット id をパラメーターとして渡します。

このトピックは、バージョン1.1 の Twitter API 向けに作成されました。 Twitter のヘルパーコードをプロジェクトに直接追加することで、Twitter API が変更された場合にヘルパーコードを更新できます。

WebMatrix のインストールの詳細については、「 [ASP.NET Web ページ2はじめにの概要](../getting-started/introducing-aspnet-web-pages-2/getting-started.md)」を参照してください。

## <a name="add-twitter-helper-to-your-project"></a>Twitter ヘルパーをプロジェクトに追加する

Twitter ヘルパーを追加するには、まず、 **App\_Code**という名前のフォルダーをプロジェクトに追加します。 次に、 **Twitter**という名前のファイルを作成します。

![App_Code フォルダー](twitter-helper/_static/image1.png)

Twitter の既定のコードを次のコードに置き換えます。

[!code-cshtml[Main](twitter-helper/samples/sample1.cshtml)]

## <a name="call-twitter-methods-from-your-web-pages"></a>Web ページから Twitter メソッドを呼び出す

次の例は、プロジェクトのページから Twitter ヘルパーメソッドを使用する方法を示しています。 プロジェクトでは、パラメーター値をニーズに関連する値に置き換える必要があります。 提供されたウィジェット id を使用して、メソッドの動作を調べることができますが、プロジェクト用に独自のウィジェットを生成する必要があります。

以下に示すパラメーターのすべてが必要であるとは限りません。 オプションのパラメーターは、ボタンまたはウィジェットの表示方法をカスタマイズするために使用されます。 たとえば、[フォロー] ボタンをクリックする必要があるのはユーザー名のみですが、この例ではフォロワーの数を含める方法と、ボタンのサイズと言語を指定する方法を示しています。

[!code-html[Main](twitter-helper/samples/sample2.html)]

## <a name="see-the-results"></a>結果を確認する

上記のコードでは、次のボタンとウィジェットが生成されます。 これらのボタンとウィジェットは、スクリーンショットではなく、完全に機能します。 Language パラメーターが**es**に設定されているため、[次へ] ボタンがスペイン語で表示されます。

### <a name="follow-button"></a>[フォロー] ボタン

[@aspnetに従う)](https://twitter.com/aspnet)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + '://platform.twitter.com/widgets.js'; fjs.parentNode.insertBefore(js, fjs); } }(document, 'script', 'twitter-wjs');</script>`

### <a name="tweet-button"></a>ツイートボタン

[ツイート](https://twitter.com/share)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + '://platform.twitter.com/widgets.js'; fjs.parentNode.insertBefore(js, fjs); } }(document, 'script', 'twitter-wjs');</script>`

### <a name="user-timeline-profile"></a>ユーザーのタイムライン (プロファイル)

[ツイート by @aspnet](https://twitter.com/aspnet)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`

### <a name="favorites"></a>お気に入り

[お気に入りのツイート by @Microsoft](https://twitter.com/Microsoft/favorites)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`

### <a name="list"></a>List

[@Microsoft/MS\_コンシューマー\_バンドからのツイート](https://twitter.com/microsoft/ms-consumer-brands/)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`

### <a name="search"></a>検索

[.Net&quot;#asp &quot;に関するツイート](https://twitter.com/search?q=%23asp.net)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`
