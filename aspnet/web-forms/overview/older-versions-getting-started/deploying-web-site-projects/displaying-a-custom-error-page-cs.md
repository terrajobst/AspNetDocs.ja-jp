---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/displaying-a-custom-error-page-cs
title: カスタムエラーページを表示するC#() |Microsoft Docs
author: rick-anderson
description: ASP.NET web アプリケーションでランタイムエラーが発生した場合、ユーザーには何が表示されますか。 回答は、web サイトの &lt;customErrors&gt; 構成によって異なります。
ms.author: riande
ms.date: 06/09/2009
ms.assetid: cb061642-faf3-41b2-9372-69e13444d458
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/displaying-a-custom-error-page-cs
msc.type: authoredcontent
ms.openlocfilehash: c1ff4c112b9a489b8fb9ef3443663cd71eda7965
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74625487"
---
# <a name="displaying-a-custom-error-page-c"></a>カスタム エラー ページを表示する (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[コードのダウンロード](https://download.microsoft.com/download/1/0/C/10CC829F-A808-4302-97D3-59989B8F9C01/ASPNET_Hosting_Tutorial_11_CS.zip)または[PDF のダウンロード](https://download.microsoft.com/download/5/C/5/5C57DB8C-5DEA-4B3A-92CA-4405544D313B/aspnet_tutorial11_CustomErrors_cs.pdf)

> ASP.NET web アプリケーションでランタイムエラーが発生した場合、ユーザーには何が表示されますか。 回答は、web サイトの &lt;customErrors&gt; 構成によって異なります。 既定では、ランタイムエラーが発生したことを示す unsightly 黄色の画面が表示されます。 このチュートリアルでは、これらの設定をカスタマイズして、サイトのルックアンドフィールに適した見た目のカスタムエラーページを表示する方法について説明します。

## <a name="introduction"></a>はじめに

完全な世界では、実行時エラーは発生しません。 プログラマは、nary のバグがあり、信頼性の高いユーザー入力の検証でコードを記述することになります。また、データベースサーバーや電子メールサーバーなどの外部リソースがオフラインになることはありません。 もちろん、実際のエラーは避けられません。 .NET Framework のクラスは、例外をスローすることによってエラーを通知します。 たとえば、SqlConnection オブジェクトの Open メソッドを呼び出すと、接続文字列によって指定されたデータベースへの接続が確立されます。 ただし、データベースがダウンしている場合、または接続文字列の資格情報が無効な場合は、Open メソッドによって `SqlException`がスローされます。 例外は、`try/catch/finally` ブロックを使用して処理できます。 `try` ブロック内のコードが例外をスローした場合、開発者がエラーからの回復を試みることができる適切な catch ブロックに制御が移ります。 一致する catch ブロックがない場合、または例外をスローしたコードが try ブロックに含まれていない場合は、例外によって `try/catch/finally` ブロックの検索でコールスタックが作成されます。

例外が処理されずにすべての ASP.NET ランタイムに対して発生した場合は、 [`HttpApplication` クラス](https://msdn.microsoft.com/library/system.web.httpapplication.aspx)の[`Error` イベント](https://msdn.microsoft.com/library/system.web.httpapplication.error.aspx)が発生し、構成された*エラーページ*が表示されます。 既定では、ASP.NET[は、こと (YSOD](http://en.wikipedia.org/wiki/Yellow_Screen_of_Death#Yellow) ) と呼ばれるエラーページを表示します。 YSOD には2つのバージョンがあります。1つは例外の詳細、スタックトレース、および開発者がアプリケーションをデバッグする際に役立つその他の情報を示しています (**図 1**を参照)。もう1つは、実行時エラーが発生したことを示すだけです (**図 2**を参照)。

例外の詳細 YSOD はアプリケーションをデバッグする開発者にとって非常に役に立ちますが、エンドユーザーの YSOD は tacky と不自然見えるであることを示しています。 代わりに、エンドユーザーは、サイトのルックアンドフィールを維持するエラーページに移動して、状況を説明するよりわかりやすい prose を作成する必要があります。 このようなカスタムエラーページを作成するのは非常に簡単です。 このチュートリアルでは、まず ASP を見てみましょう。ネットワークのさまざまなエラーページ。 次に、エラー発生時にユーザーにカスタムエラーページを表示するように web アプリケーションを構成する方法を示します。

### <a name="examining-the-three-types-of-error-pages"></a>エラーページの3種類の検証

ASP.NET アプリケーションでハンドルされない例外が発生すると、次の3種類のエラーページのいずれかが表示されます。

- 例外の詳細は、死亡エラーページの黄色の画面です。
- 実行時エラーページの黄色い画面、
- カスタムエラーページ

開発者が最もよく知られているエラーページは、例外の詳細 YSOD です。 既定では、このページはローカルにアクセスしているユーザーに表示されます。したがって、開発環境でサイトをテストするときにエラーが発生した場合に表示されるページです。 その名前が示すように、例外の詳細 YSOD は、例外の種類、メッセージ、スタックトレースなどの詳細を提供します。 さらに、ASP.NET ページの分離コードクラスのコードによって例外が発生し、アプリケーションがデバッグ用に構成されている場合、例外の詳細 YSOD にも、次のコード行 (およびその上と下の数行のコード) が表示されます。

**図 1**は、例外の詳細 YSOD ページを示しています。 ブラウザーのアドレスウィンドウの URL に注意してください: `http://localhost:62275/Genre.aspx?ID=foo`。 `Genre.aspx` のページに、特定のジャンルの書籍のレビューが一覧表示されていることを思い出してください。 `GenreId` 値 (`uniqueidentifier`) を querystring で渡す必要があります。たとえば、架空のレビューを表示するための適切な URL は `Genre.aspx?ID=7683ab5d-4589-4f03-a139-1c26044d0146`です。 非`uniqueidentifier` 値が querystring ("foo" など) を介して渡された場合は、例外がスローされます。

> [!NOTE]
> ダウンロード可能なデモ web アプリケーションでこのエラーを再現するには、`Genre.aspx?ID=foo` 直接参照するか、`Default.aspx`の [ランタイムエラーの生成] リンクをクリックします。

**図 1**に示されている例外情報に注意してください。 例外メッセージ "文字列から uniqueidentifier への変換中に変換に失敗しました" がページの上部に存在します。 例外の種類 (`System.Data.SqlClient.SqlException`) も表示されます。 スタックトレースもあります。

[![](displaying-a-custom-error-page-cs/_static/image2.png)](displaying-a-custom-error-page-cs/_static/image1.png)

**図 1**: 例外の詳細 YSOD に例外に関する情報が含まれる  
 ([クリックすると、フルサイズの画像が表示](displaying-a-custom-error-page-cs/_static/image3.png)される)

もう1つの種類の YSOD はランタイムエラー YSOD であり、**図 2**に示します。 ランタイムエラー YSOD は、実行時エラーが発生したことをビジターに通知しますが、スローされた例外に関する情報は含まれていません。 (ただし、このような YSOD ルック不自然見えるの一部である `Web.config` ファイルを変更することによって、エラーの詳細を表示する方法について説明します)。

既定では、ランタイムエラー YSOD は、ブラウザーのアドレスバーの URL (**図 2**: `http://httpruntime.web703.discountasp.net/Genre.aspx?ID=foo`) で示されているように、 http://www.yoursite.com) を通じてリモートでアクセスしているユーザーに表示されます。 この2つの異なる YSOD 画面は、開発者がエラーの詳細を知りたいと考えていますが、このような情報をライブサイトに表示することはできません。これは、潜在的なセキュリティの脆弱性やその他の機密情報が、サイト.

> [!NOTE]
> 後で DiscountASP.NET を web ホストとして使用している場合は、ライブサイトにアクセスしたときにランタイムエラー YSOD が表示されないことがあります。 これは、既定では、DiscountASP.NET には例外の詳細を表示するようにサーバーが構成されているためです。 この既定の動作は、`Web.config` ファイルに `<customErrors>` セクションを追加することでオーバーライドできます。 「どのエラーページが表示されるかを構成する」セクションでは、`<customErrors>` について詳しく説明します。

[![](displaying-a-custom-error-page-cs/_static/image5.png)](displaying-a-custom-error-page-cs/_static/image4.png)

**図 2**: ランタイムエラー YSOD にエラーの詳細が含まれていない  
 ([クリックすると、フルサイズの画像が表示](displaying-a-custom-error-page-cs/_static/image6.png)される)

エラーページの3番目の種類は、ユーザーが作成する web ページであるカスタムエラーページです。 カスタムエラーページの利点は、ページのルックアンドフィールと共にユーザーに表示される情報を完全に制御できることです。カスタムエラーページでは、他のページと同じマスターページとスタイルを使用できます。 「カスタムエラーページの使用」セクションでは、カスタムエラーページを作成し、未処理の例外が発生した場合に表示されるように構成する手順について説明します。 **図 3**に、このカスタムエラーページのヒントを提供します。 ご覧のように、エラーページのルックアンドフィールは、図1と2に示されている死亡の黄色の画面よりも、より専門的なものです。

[![](displaying-a-custom-error-page-cs/_static/image8.png)](displaying-a-custom-error-page-cs/_static/image7.png)

**図 3**: カスタムエラーページにより、より調整されたルックアンドフィールが提供される  
 ([クリックすると、フルサイズの画像が表示](displaying-a-custom-error-page-cs/_static/image9.png)される)

**図 3**のブラウザーのアドレスバーを調べてみましょう。 アドレスバーには、カスタムエラーページ (`/ErrorPages/Oops.aspx`) の URL が表示されます。 図1および2では、エラーの発生元と同じページ (`Genre.aspx`) で、死亡の黄色い画面が表示されます。 カスタムエラーページには、`aspxerrorpath` querystring パラメーターを使用してエラーが発生したページの URL が渡されます。

## <a name="configuring-which-error-page-is-displayed"></a>表示されるエラーページの構成

表示される3つのエラーページは、2つの変数に基づいています。

- `<customErrors>` セクションの構成情報
- ユーザーがローカルまたはリモートのどちらでサイトにアクセスしているか。

`Web.config` の[`<customErrors>` セクション](https://msdn.microsoft.com/library/h0hfz6fc.aspx)には、表示されるエラーページ (`defaultRedirect` および `mode`) に影響する2つの属性があります。 `defaultRedirect` 属性は省略できます。 指定されている場合は、カスタムエラーページの URL を指定し、ランタイムエラー YSOD の代わりにカスタムエラーページを表示することを示します。 `mode` 属性は必須であり、`On`、`Off`、または `RemoteOnly`の3つの値のいずれかを受け取ります。 これらの値の動作は次のとおりです。

- `On`-ローカルかリモートかに関係なく、すべての訪問者にカスタムエラーページまたはランタイムエラー YSOD が表示されることを示します。
- `Off`-ローカルかリモートかに関係なく、すべての訪問者に例外の詳細 YSOD が表示されることを指定します。
- `RemoteOnly`-カスタムエラーページまたはランタイムエラー YSOD がリモート訪問者に表示され、例外の詳細 YSOD はローカル訪問者に表示されることを示します。

特に指定しない限り、ASP.NET は mode 属性を `RemoteOnly` に設定し、`defaultRedirect` 値を指定しなかったかのように動作します。 つまり、既定の動作では、例外の詳細 YSOD がローカル訪問者に表示されるのに対し、ランタイムエラー YSOD がリモート訪問者に表示されます。 この既定の動作をオーバーライドするには、web アプリケーションの `Web.config file.` に `<customErrors>` セクションを追加します。

## <a name="using-a-custom-error-page"></a>カスタムエラーページの使用

すべての web アプリケーションには、カスタムエラーページが必要です。 これにより、ランタイムエラー YSOD に代わるより専門的な方法が提供され、簡単に作成できます。また、カスタムエラーページを使用するようにアプリケーションを構成するには、少し時間がかかります。 最初の手順では、カスタムエラーページを作成します。 `ErrorPages` という名前の新しいフォルダーを書籍レビューアプリケーションに追加し、`Oops.aspx`という名前の新しい ASP.NET ページに追加しました。 同じ外観を自動的に継承するために、ページがサイトの他のページと同じマスターページを使用していることを確認します。

[![](displaying-a-custom-error-page-cs/_static/image11.png)](displaying-a-custom-error-page-cs/_static/image10.png)

**図 4**: カスタムエラーページを作成する

次に、エラーページのコンテンツを作成するために数分かかります。 予期しないエラーが発生し、サイトのホームページへのリンクが戻ったことを示すメッセージを含む、単純なカスタムエラーページを作成しました。

[![](displaying-a-custom-error-page-cs/_static/image13.png)](displaying-a-custom-error-page-cs/_static/image12.png)

**図 5**: カスタムエラーページをデザインする  
 ([クリックすると、フルサイズの画像が表示](displaying-a-custom-error-page-cs/_static/image14.png)される)

エラーページが完了したら、ランタイムエラー YSOD の代わりに、カスタムエラーページを使用するように web アプリケーションを構成します。 これを行うには、`<customErrors>` セクションの `defaultRedirect` 属性にエラーページの URL を指定します。 次のマークアップをアプリケーションの `Web.config` ファイルに追加します。

[!code-xml[Main](displaying-a-custom-error-page-cs/samples/sample1.xml)]

上のマークアップは、ローカルでアクセスしているユーザーに例外の詳細を表示するようにアプリケーションを構成し、リモートでアクセスしているユーザーに対してカスタムエラーページ YSOD を使用します。 実際の動作を確認するには、web サイトを運用環境にデプロイし、無効な querystring の値を使用してライブサイトの Genre .aspx ページにアクセスします。 カスタムエラーページが表示されます (**図 3**を参照)。

カスタムエラーページがリモートユーザーにのみ表示されることを確認するには、開発環境からの無効なクエリ文字列を使用して `Genre.aspx` のページにアクセスします。 ただし、例外の詳細は YSOD に表示されます (**図 1**を参照してください)。 `RemoteOnly` 設定を使用すると、運用環境のサイトにアクセスするユーザーはカスタムエラーページを表示し、ローカルで作業している開発者は引き続き例外の詳細を確認できます。

## <a name="notifying-developers-and-logging-error-details"></a>開発者に通知し、エラーの詳細をログに記録する

開発環境で発生したエラーは、開発者が自分のコンピューターを使っているために発生したものです。 例外の情報が例外の詳細 YSOD に表示され、エラーが発生したときに実行していた手順がわかっています。 ただし、運用環境でエラーが発生した場合、エンドユーザーがサイトにアクセスしてエラーを報告しない限り、開発者はエラーが発生したことを知らせることはできません。 また、例外の種類、メッセージ、スタックトレースがわからなくても、エラーが発生したことを開発チームに通知する方法がユーザーにない場合でも、エラーの原因を診断するのは困難な場合があります。

このような理由から、運用環境のすべてのエラーが永続的なストア (データベースなど) に記録され、開発者にこのエラーが通知されることが最も重要です。 カスタムエラーページは、このログ記録と通知を行うための適切な場所と思われる場合があります。 残念ながら、カスタムエラーページはエラーの詳細にアクセスできないため、この情報をログに記録するために使用することはできません。 エラーの詳細をインターセプトしてログを記録する方法はいくつかあります。次の3つのチュートリアルでは、このトピックについて詳しく説明します。

## <a name="using-different-custom-error-pages-for-different-http-error-statuses"></a>異なる HTTP エラー状態に対して異なるカスタムエラーページを使用する

ASP.NET ページによって例外がスローされ、処理されない場合、ASP.NET ランタイムに例外が発生します。これにより、構成されたエラーページが表示されます。 要求が ASP.NET エンジンに送られても、何らかの理由で処理できない場合 (要求されたファイルが見つからない場合や、ファイルに対する読み取りアクセス許可が無効になっている場合など) は、ASP.NET エンジンによって `HttpException`が発生します。 この例外は、ASP.NET ページから発生した例外と同様に、ランタイムにバブルアップして、適切なエラーページが表示されます。

これは、運用環境の web アプリケーションでは、ユーザーが見つからないページを要求すると、カスタムエラーページが表示されることを意味します。 **図 6**は、このような例を示しています。 要求が存在しないページ (`NoSuchPage.aspx`) に対して行われるため、`HttpException` がスローされ、カスタムエラーページが表示されます (`aspxerrorpath` querystring パラメーターの `NoSuchPage.aspx` への参照に注意してください)。

[![](displaying-a-custom-error-page-cs/_static/image16.png)](displaying-a-custom-error-page-cs/_static/image15.png)

**図 6**: ASP.NET ランタイムは、無効な要求に応答して構成されたエラーページを表示します ([クリックすると、フルサイズの画像が表示](displaying-a-custom-error-page-cs/_static/image17.png)されます)

既定では、すべての種類のエラーによって同じカスタムエラーページが表示されます。 ただし、`<customErrors>` セクション内の `<error>` の子要素を使用して、特定の HTTP 状態コードに対して別のカスタムエラーページを指定することもできます。 たとえば、HTTP ステータスコード404を含む "ページが見つかりません" というエラーが発生した場合に別のエラーページが表示されるようにするには、`<customErrors>` セクションを更新して、次のマークアップを含めます。

[!code-xml[Main](displaying-a-custom-error-page-cs/samples/sample2.xml)]

この変更を適用すると、リモートでアクセスしているユーザーが、存在しない ASP.NET リソースを要求するたびに、`Oops.aspx`ではなく、`404.aspx` のカスタムエラーページにリダイレクトされます。 **図 7**に示すように、[`404.aspx`] ページには、一般的なカスタムエラーページよりも具体的なメッセージを含めることができます。

> [!NOTE]
> [404 エラーページを参照](http://www.smashingmagazine.com/2009/01/29/404-error-pages-one-more-time/)してください。有効な404エラーページを作成するためのガイダンスがもう1つあります。

[![](displaying-a-custom-error-page-cs/_static/image19.png)](displaying-a-custom-error-page-cs/_static/image18.png)

**図 7**: カスタム404エラーページにより対象となるメッセージが表示される `Oops.aspx`  
([クリックすると、フルサイズの画像が表示](displaying-a-custom-error-page-cs/_static/image20.png)される) 

`404.aspx` ページは、ユーザーが見つからなかったページの要求を行ったときにのみ到達することがわかっているので、このカスタムエラーページを拡張して、ユーザーがこの特定の種類のエラーに対処するのに役立つ機能を含めることができます。 たとえば、既知の不適切な Url を適切な Url にマップするデータベーステーブルを作成し、そのテーブルに対してクエリを実行し、ユーザーが移動しようとしている可能性のあるページを提示するように `404.aspx` します。

> [!NOTE]
> カスタムエラーページは、ASP.NET エンジンによって処理されるリソースに対して要求が行われた場合にのみ表示されます。 [IIS と ASP.NET 開発サーバー](core-differences-between-iis-and-the-asp-net-development-server-cs.md)チュートリアルの主な違いについて説明したように、web サーバーは特定の要求を処理することがあります。 既定では、IIS web サーバーは、ASP.NET エンジンを呼び出さずに、イメージや HTML ファイルなどの静的なコンテンツに対する要求を処理します。 その結果、ユーザーが存在しないイメージファイルを要求した場合、ASP ではなく IIS の既定の404エラーメッセージが返されます。ネットワークの構成されたエラーページ。

## <a name="summary"></a>要約

ASP.NET アプリケーションでハンドルされない例外が発生すると、次の3つのエラーページのいずれかが表示されます。例外の詳細: 黄色い画面実行時エラー: 黄色い画面またはカスタムエラーページ。 表示されるエラーページは、アプリケーションの `<customErrors>` 構成と、ユーザーがローカルまたはリモートのどちらにアクセスしているかによって異なります。 既定の動作では、ローカル訪問者に YSOD 例外の詳細が表示され、リモート訪問者に対してランタイムエラー YSOD が表示されます。

ランタイムエラー YSOD は、サイトにアクセスしているユーザーからの重要なエラー情報を隠しますが、サイトのルックアンドフィールから切り離され、アプリケーションの外観がバグになる可能性があります。 より適切な方法は、カスタムエラーページを使用することです。このページでは、カスタムエラーページを作成して設計し、`<customErrors>` セクションの `defaultRedirect` 属性でその URL を指定します。 HTTP エラーの状態ごとに、複数のカスタムエラーページを使用することもできます。

カスタムエラーページは、運用環境の web サイトの包括的なエラー処理戦略の最初の手順です。 エラーの開発者に警告を出し、その詳細をログに記録することも重要です。 次の3つのチュートリアルでは、エラー通知とログ記録の手法を紹介します。

プログラミングを楽しんでください。

### <a name="further-reading"></a>関連項目

このチュートリアルで説明しているトピックの詳細については、次のリソースを参照してください。

- [エラーページ、もう1回](http://www.smashingmagazine.com/2009/01/29/404-error-pages-one-more-time/)
- [例外のデザインのガイドライン](https://msdn.microsoft.com/library/ms229014.aspx)
- [ユーザーフレンドリなエラーページ](http://aspnet.4guysfromrolla.com/articles/090606-1.aspx)
- [例外の処理とスロー](https://msdn.microsoft.com/library/5b2yeyab.aspx)
- [ASP.NET でカスタムエラーページを適切に使用する](http://professionalaspnet.com/archive/2007/09/30/Properly-Using-Custom-Error-Pages-in-ASP.NET.aspx)

> [!div class="step-by-step"]
> [前へ](strategies-for-database-development-and-deployment-cs.md)
> [次へ](processing-unhandled-exceptions-cs.md)
