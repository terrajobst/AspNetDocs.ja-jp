---
uid: web-pages/overview/mobile/rendering-aspnet-web-pages-sites-for-mobile-devices
title: モバイルデバイス用の ASP.NET Web ページ (Razor) サイトのレンダリング |Microsoft Docs
author: Rick-Anderson
description: 'この記事では、モバイルデバイスに適切に表示される ASP.NET Web ページ (Razor) サイトでページを作成する方法について説明します。 学習内容: 操作方法...'
ms.author: riande
ms.date: 02/17/2014
ms.assetid: f15ab392-c05e-4269-83bf-7c6d2b8c8ec8
msc.legacyurl: /web-pages/overview/mobile/rendering-aspnet-web-pages-sites-for-mobile-devices
msc.type: authoredcontent
ms.openlocfilehash: c012348d65e48a275cb0e4808fef2a7f31e5fb33
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78454354"
---
# <a name="rendering-aspnet-web-pages-razor-sites-for-mobile-devices"></a>モバイルデバイスのレンダリング ASP.NET Web ページ (Razor) サイト

[Tom FitzMacken](https://github.com/tfitzmac)

> この記事では、モバイルデバイスに適切に表示される ASP.NET Web ページ (Razor) サイトでページを作成する方法について説明します。
> 
> ここでは、次の内容について学習します。
> 
> - 名前付け規則を使用して、ページがモバイルデバイス専用に設計されていることを指定する方法。
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>このチュートリアルで使用されているソフトウェアのバージョン
> 
> 
> - ASP.NET Web ページ (Razor) 3
>   
> 
> このチュートリアルは ASP.NET Web ページ2でも動作します。

ASP.NET Web ページを使用すると、モバイルデバイスまたはその他のデバイスでコンテンツを表示するためのカスタム表示を作成できます。

ASP.NET Web ページサイトにデバイス固有のページを作成する最も簡単な方法は、ファイル名の形式でファイル名を使用する方法です。たとえば、「 *FileName. Mobile. cshtml*」と指定します。 ページの2つのバージョンを作成できます (たとえば、 *myfile.txt*という名前の1つと、 *myfile.txt*という名前の1つ)。 実行時に、モバイルデバイスが*myfile.txt*を要求すると、ASP.NET は、 *myfile.txt*からコンテンツをレンダリングします。 それ以外の場合は、 *myfile.txt*がレンダリングされます。

次の例は、モバイルデバイスのコンテンツページを追加することによって、モバイルレンダリングを有効にする方法を示しています。 *Page1*には、コンテンツとナビゲーションサイドバーが含まれています。 *Page1*には同じコンテンツが含まれていますが、サイドバーは省略されています。

1. ASP.NET Web ページサイトで、 *Page1*という名前のファイルを作成し、現在の内容を次のマークアップに置き換えます。

    [!code-html[Main](rendering-aspnet-web-pages-sites-for-mobile-devices/samples/sample1.html)]
2. *Page1*という名前のファイルを作成し、既存の内容を次のマークアップに置き換えます。 モバイルバージョンのページでは、より小さい画面でのレンダリングを改善するためにナビゲーションセクションが省略されていることに注意してください。

    [!code-html[Main](rendering-aspnet-web-pages-sites-for-mobile-devices/samples/sample2.html)]
3. デスクトップブラウザーを実行し、 *Page1*に移動します。 ![mobil-1](rendering-aspnet-web-pages-sites-for-mobile-devices/_static/image1.png)
4. モバイルブラウザー (またはモバイルデバイスエミュレーター) を実行し、 *Page1*に移動します。 ( *. Mobile*は含まれていないことに注意してください。 URL の一部として。)要求が*page1*に対して行う場合でも、ASP.NET は*page1*をレンダリングします。

    ![mobilesites 2](rendering-aspnet-web-pages-sites-for-mobile-devices/_static/image2.png)

> [!NOTE]
> モバイルページをテストするには、デスクトップコンピューターで実行されるモバイルデバイスシミュレーターを使用します。 このツールを使用すると、モバイルデバイスで見ているように web ページをテストできます (通常、表示領域が非常に小さくなります)。 シミュレーターの1つの例として、Mozilla Firefox 用の[ユーザーエージェントスイッチャーアドオン](http://addons.mozilla.org/firefox/addon/user-agent-switcher/)があります。これにより、デスクトップバージョンの firefox からさまざまなモバイルブラウザーをエミュレートできます。

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>その他のリソース

[Windows Phone エミュレーター](https://msdn.microsoft.com/library/ff402563(v=VS.92).aspx)
