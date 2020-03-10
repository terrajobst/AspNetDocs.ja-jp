---
uid: mvc/overview/getting-started/lifecycle-of-an-aspnet-mvc-5-application
title: ASP.NET MVC 5 アプリケーションのライフサイクル |Microsoft Docs
author: cephalin
description: ASP.NET MVC 5 アプリケーションのライフサイクルをグラフ化した PDF ドキュメントをダウンロードします。 このライフサイクルドキュメントでは、MVC ライフサイクルの概要を示します...
ms.author: riande
ms.date: 02/28/2014
ms.assetid: 9c1e3a75-b644-4480-8326-11300b1ec4b3
msc.legacyurl: /mvc/overview/getting-started/lifecycle-of-an-aspnet-mvc-5-application
msc.type: authoredcontent
ms.openlocfilehash: f4a9b3fb61552b070db11fba617b5627fcd71cd5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78470326"
---
# <a name="lifecycle-of-an-aspnet-mvc-5-application"></a>ASP.NET MVC 5 アプリケーションのライフサイクル

[Cephas リンク](https://github.com/cephalin)

[PDF ドキュメントのダウンロード](lifecycle-of-an-aspnet-mvc-5-application/_static/lifecycle-of-an-aspnet-mvc-5-application1.pdf)

ここでは、HTTP 要求の受信からクライアントへの HTTP 応答の送信まで、すべての ASP.NET MVC 5 アプリケーションのライフサイクルをグラフ化した PDF ドキュメントをダウンロードできます。 また、ASP.NET MVC を初めて使用するユーザー向けの教育ツールとしても、アプリケーションの特定の側面を掘り下げなければならないユーザーのための参考資料としても設計されています。 PDF ドキュメントには、次の機能があります。

- MVC が[ASP.NET アプリケーションライフサイクル](https://msdn.microsoft.com/library/bb470252.aspx)にどのように統合されるかを理解するのに役立つ、関連する[HttpApplication](https://msdn.microsoft.com/library/system.web.httpapplication.aspx)ステージ。
- MVC アプリケーションのライフサイクルの概要です。このビューでは、すべての MVC アプリケーションが要求処理パイプラインで通過する主なステージを把握できます。  
    ![](lifecycle-of-an-aspnet-mvc-5-application/_static/image1.jpg)
- 要求処理パイプラインの詳細をドリルダウンする詳細ビュー。 高レベルビューと詳細ビューを比較して、ライフサイクルの詳細がさまざまな段階にどのように収集されるかを確認できます。 [PDF をダウンロード](lifecycle-of-an-aspnet-mvc-5-application/_static/lifecycle-of-an-aspnet-mvc-5-application1.pdf)して、より大きなビューを表示します。
    ![](lifecycle-of-an-aspnet-mvc-5-application/_static/image2.jpg)
- 要求処理パイプライン内の[コントローラー](https://msdn.microsoft.com/library/system.web.mvc.controller.aspx)オブジェクトのオーバーライド可能なすべてのメソッドの配置と目的。 1つのメソッドをオーバーライドする必要があるかもしれませんが、目的に応じて適切なライフサイクルステージでコードを記述できるように、アプリケーションのライフサイクルの役割を理解しておくことが重要です。
- 各フィルターの種類 (認証、承認、アクション、および結果) がどのように呼び出されるかを示す、不足している図。
- 詳細ビューで、関心のある各ポイントから役に立つ記事やブログにリンクします。

## <a name="next-steps"></a>次の手順

このドキュメントはニーズを満たしていますか? お客様からのフィードバックをお待ちしております。 アプリケーションの ASP.NET MVC ライフサイクルに関して疑問がある場合は、 [Stackoverflow](http://stackoverflow.com/help)と[ASP.NET mvc フォーラム](https://forums.asp.net/1146.aspx)をお勧めします。 最新[のチュートリアル](https://twitter.com/Cephas_MSFT)で更新プログラムを入手できるように、twitter でフォローします。
