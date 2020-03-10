---
uid: web-forms/videos/how-do-i/how-do-i-cache-an-aspnet-page-based-upon-information-in-the-http-header
title: '[操作方法:] HTTP ヘッダーの情報に基づいて ASP.NET ページをキャッシュする |Microsoft Docs'
author: rick-anderson
description: このビデオでは、ページの HTTP ヘッダーの情報に基づいて、ページを ASP.NET 出力キャッシュに保持する方法を示しています。 最初に、可能性のある HTTP hea...
ms.author: riande
ms.date: 02/26/2009
ms.assetid: 0f8df1bd-080a-4eeb-980c-c2fbb05d30c2
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-cache-an-aspnet-page-based-upon-information-in-the-http-header
msc.type: video
ms.openlocfilehash: 79c27f39793a4a3a94ea412838fb3844579e874d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78506974"
---
# <a name="how-do-i--cache-an-aspnet-page-based-upon-information-in-the-http-header"></a>[操作方法:] HTTP ヘッダーの情報に基づいて ASP.NET ページをキャッシュする

[Chris Pels](https://twitter.com/chrispels)

このビデオでは、ページの HTTP ヘッダーの情報に基づいて、ページを ASP.NET 出力キャッシュに保持する方法を示しています。 まず、可能性のある HTTP ヘッダー値を確認します。 次に、サンプルページが作成され、OutputCache ディレクティブが VaryByHeader 属性と共に使用されます。この属性には、ユーザーのブラウザーの言語に基づいてキャッシュを制御するための値 "accept-language" (HTTP ヘッダー) が含まれています。 サンプルページは、英語に設定されている IE で表示され、FireFox ではフランス語を使用するように設定されています。 最後に、キャッシュ定義を web.config ファイルの CacheProfile に移動するオプションについて説明します。

[&#9654;ビデオを見る (12 分)](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-cache-an-aspnet-page-based-upon-information-in-the-http-header)
