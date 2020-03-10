---
uid: web-forms/videos/how-do-i/how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page
title: '[操作方法:]ASP.NET ページ内の HTML を置き換えるには、Filter プロパティを使用します。Microsoft Docs'
author: rick-anderson
description: このビデオでは、ページに送信される HTML をインターセプトおよび変更するために、Filter プロパティを使用する方法を示しています。 まず、サンプルページが作成されます。
ms.author: riande
ms.date: 01/29/2009
ms.assetid: 3e5ae74a-9798-47d8-a2b3-0d8ad42dd4bc
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page
msc.type: video
ms.openlocfilehash: 2ebd9162f81f5270c92c6b8d55e2d2dad4660701
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78487996"
---
# <a name="how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page"></a>[操作方法:]ASP.NET ページ内の HTML を置き換えるには、Filter プロパティを使用します。

[Chris Pels](https://twitter.com/chrispels)

このビデオでは、ページに送信される HTML をインターセプトおよび変更するために、Filter プロパティを使用する方法を示しています。 まず、いくつかの単純なテキストを使用してサンプルページを作成します。 次に、ユーザーのブラウザーに送信されている現在のストリームの置換ストリームとして機能するカスタムストリームクラスが作成されます。 このカスタムストリームクラスでは、ページの内容がストリームから取得され、変更されて、応答ストリームに書き込まれます。 このカスタムストリームクラスでは、基本応答ストリームの HTML を置き換えるように書き込みメソッドをカスタマイズして、ユーザーのブラウザーに送信される内容を変更します。 最後に、新しいストリームクラスが Response に割り当てられます。これにより、ページの\_読み込みイベントによって、ページコンテンツを変更するためのメカニズムが提供されます。

[&#9654;ビデオを見る (13 分)](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page)
