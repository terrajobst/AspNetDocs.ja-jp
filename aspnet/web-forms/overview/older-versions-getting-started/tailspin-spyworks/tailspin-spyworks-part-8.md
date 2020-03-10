---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-8
title: 'パート 8: 最終的なページ、例外処理、および結論 |Microsoft Docs'
author: JoeStagner
description: このチュートリアルシリーズでは、Tailspin Spyworks サンプルアプリケーションを構築するために実行するすべての手順について詳しく説明します。 パート8は、連絡先ページ、ページ、および例外を追加します。
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 5aeadf8f-39f3-4f07-a78f-1c310c64fb23
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-8
msc.type: authoredcontent
ms.openlocfilehash: 707dc9d87ae324a7897c971a451e40bc54c96cb3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78474340"
---
# <a name="part-8-final-pages-exception-handling-and-conclusion"></a>パート 8: 最終的なページ、例外処理、および結論

[Joe Stagner](https://github.com/JoeStagner)

> Tailspin Spyworks は、.NET プラットフォーム用の強力でスケーラブルなアプリケーションを簡単に作成する方法を示しています。 ASP.NET 4 の優れた新機能を使用して、ショッピング、チェックアウト、管理などのオンラインストアを構築する方法を示しています。
> 
> このチュートリアルシリーズでは、Tailspin Spyworks サンプルアプリケーションを構築するために実行するすべての手順について詳しく説明します。 パート8では、連絡先ページ、ページ、例外処理を追加します。 これがシリーズの結論です。

## <a id="_Toc260221680"></a>連絡先ページ (ASP.NET からの電子メールの送信)

ContactUs という名前の新しいページを作成します。

デザイナーを使用して、次のフォームを作成します。これには、ToolkitScriptManager と AjaxControlToolkit のエディターコントロールを含めるための特別な注意事項があります。 。

![](tailspin-spyworks-part-8/_static/image1.jpg)

[送信] ボタンをダブルクリックして、分離コードファイルに click イベントハンドラーを生成し、電子メールとして連絡先情報を送信するメソッドを実装します。

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample1.cs)]

このコードでは、電子メールの送信に使用する SMTP サーバーを指定する構成セクションに、web.config ファイルにエントリが含まれている必要があります。

[!code-xml[Main](tailspin-spyworks-part-8/samples/sample2.xml)]

## <a id="_Toc260221681"></a>[バージョン情報] ページ

AboutUs という名前のページを作成し、任意の内容を追加します。

## <a id="_Toc260221682"></a>グローバル例外ハンドラー

最後に、アプリケーション全体で例外がスローされました。また、web アプリケーションでハンドルされない例外が発生する可能性がある予期しない状況もあります。

未処理の例外を web サイトの訪問者に表示させたくありません。

![](tailspin-spyworks-part-8/_static/image2.jpg)

ユーザーエクスペリエンスの低下とは別に、ハンドルされない例外がセキュリティ上の問題になることもあります。

この問題を解決するには、グローバル例外ハンドラーを実装します。

これを行うには、global.asax ファイルを開き、次の事前生成されたイベントハンドラーを確認します。

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample3.cs)]

次のように、アプリケーション\_のエラーハンドラーを実装するコードを追加します。

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample4.cs)]

次に、エラー .aspx という名前のページをソリューションに追加し、このマークアップスニペットを追加します。

[!code-aspx[Main](tailspin-spyworks-part-8/samples/sample5.aspx)]

次に、ページ\_読み込みイベントハンドラーは、要求オブジェクトからエラーメッセージを抽出します。

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample6.cs)]

## <a id="_Toc260221683"></a>最後

ASP.NET WebForms により、データベースアクセス、メンバーシップ、AJAX などを使用して、洗練された web サイトを簡単に作成できることがわかりました。 非常に迅速です。

このチュートリアルでは、独自の ASP.NET WebForms アプリケーションの構築を開始するために必要なツールを提供しています。

> [!div class="step-by-step"]
> [[戻る]](tailspin-spyworks-part-7.md)
