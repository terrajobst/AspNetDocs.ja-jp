---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/processing-unhandled-exceptions-vb
title: 未処理の例外の処理 (VB) |Microsoft Docs
author: rick-anderson
description: 運用環境の web アプリケーションでランタイムエラーが発生した場合は、開発者に通知し、エラーをログに記録して、la で診断できるようにすることが重要です。
ms.author: riande
ms.date: 06/09/2009
ms.assetid: 051296f0-9519-4e78-835c-d868da13b0a0
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/processing-unhandled-exceptions-vb
msc.type: authoredcontent
ms.openlocfilehash: 8d2e12af29bd95ce9898fa6a5e81be8b7a761f76
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78473638"
---
# <a name="processing-unhandled-exceptions-vb"></a>未処理の例外を処理する (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[サンプル コードを表示またはダウンロード](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/web-forms/overview/older-versions-getting-started/deploying-web-site-projects/processing-unhandled-exceptions-vb/samples)します ([ダウンロード方法](/aspnet/core/tutorials/index#how-to-download-a-sample))。

> 運用環境の web アプリケーションでランタイムエラーが発生した場合、開発者に通知し、後で診断できるようにエラーをログに記録することが重要です。 このチュートリアルでは、ASP.NET が実行時エラーを処理し、未処理の例外が ASP.NET ランタイムにバブルアップするたびにカスタムコードを実行する方法の概要について説明します。

## <a name="introduction"></a>はじめに

ASP.NET アプリケーションでハンドルされない例外が発生すると、ASP.NET ランタイムにバブルアップします。これにより、`Error` イベントが発生し、適切なエラーページが表示されます。 エラーページには、次の3種類があります。ランタイムエラーの黄色い画面 (YSOD)例外の詳細 YSOD;およびカスタムエラーページ。 前の[チュートリアル](displaying-a-custom-error-page-vb.md)では、リモートユーザーのカスタムエラーページを使用するようにアプリケーションを構成し、ローカルにアクセスするユーザーの例外の詳細を YSOD しました。

サイトのルックアンドフィールと一致するユーザーフレンドリなカスタムエラーページを使用することをお勧めしますが、既定のランタイムエラー YSOD を使用することをお勧めします。ただし、カスタムエラーページを表示するのは、包括的なエラー処理ソリューションの一部にすぎません。 運用環境のアプリケーションでエラーが発生した場合は、例外の原因を解決して対処できるように、開発者にエラーの通知を受け取ることが重要です。 さらに、エラーの詳細をログに記録し、後でエラーを調査して診断できるようにする必要があります。

このチュートリアルでは、未処理の例外の詳細にアクセスして、ログに記録し、開発者に通知できるようにする方法について説明します。 この後の2つのチュートリアルでは、エラーログライブラリについて説明します。このライブラリでは、構成の少し後に、ランタイムエラーを開発者に自動的に通知し、その詳細をログに記録します。

> [!NOTE]
> このチュートリアルでは、何らかの独自の方法で未処理の例外を処理する必要がある場合に、最も役立ちます。 例外をログに記録するだけで、開発者に通知する必要がある場合は、エラーログライブラリを使用する方法があります。 次の2つのチュートリアルでは、このような2つのライブラリの概要を説明します。

## <a name="executing-code-when-theerrorevent-is-raised"></a>`Error`イベントが発生したときのコードの実行

イベントは、興味深い問題が発生したことを通知するためのメカニズムと、応答でコードを実行するための別のオブジェクトを提供します。 ASP.NET の開発者は、イベントの観点から考えることに慣れています。 ビジターが特定のボタンをクリックしたときにコードを実行する場合は、そのボタンの `Click` イベントのイベントハンドラーを作成し、そこにコードを配置します。 未処理の例外が発生するたびに ASP.NET ランタイムが[`Error` イベント](https://msdn.microsoft.com/library/system.web.httpapplication.error.aspx)を発生させると、エラーの詳細をログに記録するためのコードがイベントハンドラーで発生することになります。 しかし、`Error` イベントのイベントハンドラーを作成するにはどうすればよいでしょうか。

`Error` イベントは、要求の有効期間中に HTTP パイプラインの特定のステージで発生する、 [`HttpApplication` クラス](https://msdn.microsoft.com/library/system.web.httpapplication.aspx)の多くのイベントの1つです。 たとえば、`HttpApplication` クラスの[`BeginRequest` イベント](https://msdn.microsoft.com/library/system.web.httpapplication.beginrequest.aspx)は、すべての要求の開始時に発生します。この[`AuthenticateRequest` イベント](https://msdn.microsoft.com/library/system.web.httpapplication.authenticaterequest.aspx)は、セキュリティモジュールによって要求元が識別されたときに発生します。 これらの `HttpApplication` イベントは、ページ開発者が、要求の有効期間中のさまざまなポイントでカスタムロジックを実行する手段を提供します。

`HttpApplication` イベントのイベントハンドラーは、`Global.asax`という名前の特殊なファイルに配置できます。 このファイルを web サイトに作成するには、`Global.asax`という名前のグローバルアプリケーションクラステンプレートを使用して、web サイトのルートに新しい項目を追加します。

[![](processing-unhandled-exceptions-vb/_static/image2.png)](processing-unhandled-exceptions-vb/_static/image1.png)

**図 1**: Web アプリケーションに `Global.asax` を追加する  
 ([クリックすると、フルサイズの画像が表示](processing-unhandled-exceptions-vb/_static/image3.png)される)

Visual Studio によって作成された `Global.asax` ファイルの内容と構造は、Web アプリケーションプロジェクト (WAP) と Web サイトプロジェクト (WSP) のどちらを使用しているかによって若干異なります。 WAP を使用すると、`Global.asax` は `Global.asax` と `Global.asax.vb`という2つの個別のファイルとして実装されます。 `Global.asax` ファイルには、`.vb` ファイルを参照する `@Application` ディレクティブは含まれていません。対象のイベントハンドラーは、`Global.asax.vb` ファイルで定義されます。 WSPs の場合、1つのファイルのみが作成され、`Global.asax`、およびイベントハンドラーが `<script runat="server">` ブロックで定義されます。

Visual Studio のグローバルアプリケーションクラステンプレートによって WAP に作成された `Global.asax` ファイルには、`Application_BeginRequest`、`Application_AuthenticateRequest`、および `Application_Error`という名前のイベントハンドラーが含まれています。これは、それぞれ `HttpApplication` イベント `BeginRequest`、`AuthenticateRequest`、および `Error`のイベントハンドラーです。 `Application_Start`、`Session_Start`、`Application_End`、および `Session_End`という名前のイベントハンドラーもあります。これは、web アプリケーションの起動時、新しいセッションが開始されたとき、アプリケーションが終了したとき、およびセッションが終了したときに起動するイベントハンドラーです。 WSP で Visual Studio によって作成された `Global.asax` ファイルには、`Application_Error`、`Application_Start`、`Session_Start`、`Application_End`、および `Session_End` のイベントハンドラーだけが含まれています。

> [!NOTE]
> ASP.NET アプリケーションを展開する場合は、`Global.asax` ファイルを運用環境にコピーする必要があります。 このコードはプロジェクトのアセンブリにコンパイルされるため、WAP で作成された `Global.asax.vb` ファイルを運用環境にコピーする必要はありません。

Visual Studio のグローバルアプリケーションクラステンプレートによって作成されたイベントハンドラーは完全ではありません。 イベントハンドラー `Application_EventName`に名前を付けることで、任意の `HttpApplication` イベントのイベントハンドラーを追加できます。 たとえば、次のコードを `Global.asax` ファイルに追加して、 [`AuthorizeRequest` イベント](https://msdn.microsoft.com/library/system.web.httpapplication.authorizerequest.aspx)のイベントハンドラーを作成することができます。

[!code-vb[Main](processing-unhandled-exceptions-vb/samples/sample1.vb)]

同様に、グローバルアプリケーションクラステンプレートによって作成されたイベントハンドラーは不要ですが、削除できます。 このチュートリアルでは、`Error` イベントのイベントハンドラーのみが必要です。`Global.asax` ファイルから他のイベントハンドラーを削除してもかまいません。

> [!NOTE]
> *HTTP モジュール*は、`HttpApplication` イベントのイベントハンドラーを定義する別の方法を提供します。 HTTP モジュールはクラスファイルとして作成されます。これは、web アプリケーションプロジェクト内に直接配置することも、別のクラスライブラリに分割することもできます。 HTTP モジュールはクラスライブラリに分けることができるため、`HttpApplication` のイベントハンドラーを作成するために、より柔軟で再利用可能なモデルを提供します。 `Global.asax` ファイルは、そのファイルが存在する web アプリケーションに固有のものですが、http モジュールをアセンブリにコンパイルすることができます。この時点で、web サイトに HTTP モジュールを追加するのは、`Bin` フォルダー内のアセンブリを削除し `Web.config`にモジュールを登録するのと同じです。 このチュートリアルでは、HTTP モジュールの作成と使用については説明しませんが、次の2つのチュートリアルで使用される2つのエラーログライブラリは、HTTP モジュールとして実装されています。 HTTP モジュールの利点の背景については、 [「Http モジュールとハンドラーを使用したプラグ可能な ASP.NET コンポーネントの作成](https://msdn.microsoft.com/library/aa479332.aspx)」を参照してください。

## <a name="retrieving-information-about-the-unhandled-exception"></a>未処理の例外に関する情報の取得

この時点で、`Application_Error` イベントハンドラーを含む global.asax ファイルがあります。 このイベントハンドラーが実行されるときに、エラーを開発者に通知し、その詳細をログに記録する必要があります。 これらのタスクを実行するには、最初に発生した例外の詳細を確認する必要があります。 サーバーオブジェクトの[`GetLastError` メソッド](https://msdn.microsoft.com/library/system.web.httpserverutility.getlasterror.aspx)を使用して、`Error` イベントの発生原因となった未処理の例外の詳細を取得します。

[!code-vb[Main](processing-unhandled-exceptions-vb/samples/sample2.vb)]

`GetLastError` メソッドは、`Exception`型のオブジェクトを返します。これは、.NET Framework 内のすべての例外の基本型です。 ただし、上記のコードでは、`GetLastError` によって返された例外オブジェクトを `HttpException` オブジェクトにキャストしています。 ASP.NET リソースの処理中に例外がスローされたために `Error` イベントが発生している場合は、スローされた例外が `HttpException`内にラップされます。 エラーイベントをよりする実際の例外を取得するには、`InnerException` プロパティを使用します。 存在しないページの要求など、HTTP ベースの例外が原因で `Error` イベントが発生した場合、`HttpException` がスローされますが、内部例外はありません。

次のコードでは、`GetLastErrormessage` を使用して、`Error` イベントをトリガーした例外に関する情報を取得し、`lastErrorWrapper`という名前の変数に `HttpException` を格納します。 次に、元の例外の型、メッセージ、およびスタックトレースを3つの文字列変数に格納し、`lastErrorWrapper` が `Error` イベントをトリガーした実際の例外 (HTTP ベースの例外の場合) であるかどうか、または要求の処理中にスローされた例外の単なるラッパーであるかどうかを確認します。

[!code-vb[Main](processing-unhandled-exceptions-vb/samples/sample3.vb)]

この時点で、例外の詳細をデータベーステーブルに記録するコードを記述するために必要なすべての情報が用意されています。 目的のエラー詳細 (型、メッセージ、スタックトレースなど) と、その他の有用な情報 (要求されたページの URL、現在ログオンしているユーザーの名前など) に対応した列を含むデータベーステーブルを作成できます。 次に、`Application_Error` イベントハンドラーで、データベースに接続し、テーブルにレコードを挿入します。 同様に、エラーの開発者に電子メールで通知するコードを追加することもできます。

次の2つのチュートリアルで調査されているエラーログライブラリは、そのような機能を備えていないため、このエラーログと通知を自分で作成する必要はありません。 ただし、`Error` イベントが発生していることと、`Application_Error` イベントハンドラーを使用してエラーの詳細をログに記録し、開発者に通知できることを示すために、エラーが発生したときに開発者に通知するコードを追加してみましょう。

## <a name="notifying-a-developer-when-an-unhandled-exception-occurs"></a>未処理の例外が発生したときに開発者に通知する

運用環境でハンドルされない例外が発生した場合は、開発チームに警告して、エラーを評価し、実行する必要があるアクションを決定できるようにすることが重要です。 たとえば、データベースへの接続中にエラーが発生した場合は、接続文字列をもう一度確認し、web ホスティング会社でサポートチケットを開く必要があります。 プログラミングエラーが原因で例外が発生した場合は、今後このようなエラーを防ぐために、追加のコードまたは検証ロジックを追加する必要があります。

[`System.Net.Mail` 名前空間](https://msdn.microsoft.com/library/system.net.mail.aspx)の .NET Framework クラスを使用すると、簡単に電子メールを送信できます。 [`MailMessage` クラス](https://msdn.microsoft.com/library/system.net.mail.mailmessage.aspx)は、電子メールメッセージを表し、`To`、`From`、`Subject`、`Body`、`Attachments`のようなプロパティを持ちます。 `SmtpClass` は、指定された SMTP サーバーを使用して `MailMessage` オブジェクトを送信するために使用されます。SMTP サーバーの設定は、プログラムで指定することも、`Web.config file`の[`<system.net>` 要素](https://msdn.microsoft.com/library/6484zdc1.aspx)で宣言して指定することもできます。 ASP.NET アプリケーションで電子メールメッセージを送信する方法の詳細については、記事「 [ASP.NET で電子メールを送信](http://aspnet.4guysfromrolla.com/articles/072606-1.aspx)する」および「 [System .NET メールの FAQ](http://systemnetmail.com/)」を参照してください。

> [!NOTE]
> `<system.net>` 要素には、電子メールの送信時に `SmtpClient` クラスによって使用される SMTP サーバー設定が含まれます。 Web ホスティング会社には、アプリケーションから電子メールを送信するために使用できる SMTP サーバーがある可能性があります。 Web アプリケーションで使用する SMTP サーバーの設定については、web ホストのサポートセクションを参照してください。

次のコードを `Application_Error` イベントハンドラーに追加して、エラーが発生したときに開発者に電子メールを送信します。

[!code-vb[Main](processing-unhandled-exceptions-vb/samples/sample4.vb)]

上記のコードは非常に時間がかかりますが、多くの場合、開発者に送信される電子メールに表示される HTML が作成されます。 このコードは、`GetLastError` メソッド (`lastErrorWrapper`) によって返される `HttpException` を参照することによって開始されます。 要求によって発生した実際の例外は `lastErrorWrapper.InnerException` を通じて取得され、`lastError`変数に割り当てられます。 型、メッセージ、およびスタックトレース情報は `lastError` から取得され、3つの文字列変数に格納されます。

次に、`mm` という名前の `MailMessage` オブジェクトが作成されます。 電子メールの本文は HTML 形式で、要求されたページの URL、現在ログオンしているユーザーの名前、例外に関する情報 (種類、メッセージ、スタックトレース) が表示されます。 `HttpException` クラスの優れた点の1つは、 [GetHtmlErrorMessage メソッド](https://msdn.microsoft.com/library/system.web.httpexception.gethtmlerrormessage.aspx)を呼び出すことによって、例外の詳細を作成するために使用する HTML (YSOD) を生成できることです。 ここでは、このメソッドを使用して例外の詳細を取得し、YSOD マークアップを添付ファイルとして電子メールに追加します。 注意点の1つとして、`Error` イベントをトリガーした例外が HTTP ベースの例外 (存在しないページの要求など) だった場合、`GetHtmlErrorMessage` メソッドは `null`を返します。

最後の手順では、`MailMessage`を送信します。 これを行うには、新しい `SmtpClient` メソッドを作成し、その `Send` メソッドを呼び出します。

> [!NOTE]
> このコードを web アプリケーションで使用する前に、`ToAddress` および `FromAddress` 定数の値を support@example.com から、エラー通知電子メールの送信先と送信元の電子メールアドレスに変更します。 また、`Web.config`の [`<system.net>`] セクションで、SMTP サーバー設定を指定する必要があります。 使用する SMTP サーバーの設定を確認するには、web ホストプロバイダーに問い合わせてください。

このコードは、エラーが発生すると、エラーの概要と YSOD を含む電子メールメッセージを送信します。 前のチュートリアルでは、Genre .aspx にアクセスして、`Genre.aspx?ID=foo`のようなクエリ文字列を使用して無効な `ID` 値を渡すことで、ランタイムエラーを例示しています。 `Global.asax` ファイルが配置されているページにアクセスすると、前のチュートリアルと同じユーザーエクスペリエンスが得られます。開発環境では、[例外の詳細] の黄色い画面が引き続き表示されます。運用環境では、カスタムエラーページが表示されます。 この既存の動作に加えて、開発者に電子メールが送信されます。

**図 2**は、`Genre.aspx?ID=foo`にアクセスしたときに受信した電子メールを示しています。 電子メールの本文に例外情報がまとめられ、`YSOD.htm` 添付ファイルには、例外の詳細 YSOD に表示される内容が表示されます (**図 3**を参照)。

[![](processing-unhandled-exceptions-vb/_static/image5.png)](processing-unhandled-exceptions-vb/_static/image4.png)

**図 2**: 未処理の例外が発生するたびに、開発者に電子メール通知が送信される  
 ([クリックすると、フルサイズの画像が表示](processing-unhandled-exceptions-vb/_static/image6.png)される)

[![](processing-unhandled-exceptions-vb/_static/image8.png)](processing-unhandled-exceptions-vb/_static/image7.png)

**図 3**: 電子メール通知に、添付ファイルとしての例外の詳細 YSOD が含まれている  
 ([クリックすると、フルサイズの画像が表示](processing-unhandled-exceptions-vb/_static/image9.png)される)

## <a name="what-about-using-the-custom-error-page"></a>カスタムエラーページを使用するにはどうすればよいですか。

このチュートリアルでは、`Global.asax` と `Application_Error` イベントハンドラーを使用して、ハンドルされない例外が発生したときにコードを実行する方法について説明しました。 具体的には、このイベントハンドラーを使用して、開発者にエラーを通知します。さらに、エラーの詳細をデータベースに記録するように拡張することもできます。 `Application_Error` イベントハンドラーが存在しても、エンドユーザーのエクスペリエンスには影響しません。 構成されたエラーページは、エラーの詳細 YSOD、ランタイムエラー YSOD、またはカスタムエラーページで確認できます。

カスタムエラーページを使用する場合は、`Global.asax` ファイルと `Application_Error` イベントが必要かどうかを気にするのが自然です。 エラーが発生すると、ユーザーにはカスタムエラーページが表示されるので、開発者に通知するコードを配置して、エラーの詳細をカスタムエラーページの分離コードクラスに記録することはできません。 カスタムエラーページの分離コードクラスにコードを追加することはできますが、前のチュートリアルで説明した手法を使用すると、`Error` イベントをトリガーした例外の詳細にアクセスすることはできません。 カスタムエラーページから `GetLastError` メソッドを呼び出すと、`Nothing`が返されます。

この動作が発生する理由は、リダイレクトを使用してカスタムエラーページに到達したためです。 未処理の例外が ASP.NET ランタイムに到達すると、ASP.NET エンジンはその `Error` イベント (`Application_Error` イベントハンドラーを実行) を発生させ、`Response.Redirect(customErrorPageUrl)`を発行して、ユーザーをカスタムエラーページに*リダイレクト*します。 `Response.Redirect` メソッドは、HTTP 302 ステータスコードを使用してクライアントに応答を送信し、ブラウザーに新しい URL を要求するよう指示します。具体的には、カスタムエラーページを使用します。 ブラウザーは、この新しいページを自動的に要求します。 カスタムエラーページは、ブラウザーのアドレスバーがカスタムエラーページの URL に変更されるため、エラーが発生したページとは別に要求されていることがわかります (**図 4**を参照)。

[![](processing-unhandled-exceptions-vb/_static/image11.png)](processing-unhandled-exceptions-vb/_static/image10.png)

**図 4**: エラーが発生すると、ブラウザーはカスタムエラーページの URL にリダイレクトされます。  
 ([クリックすると、フルサイズの画像が表示](processing-unhandled-exceptions-vb/_static/image12.png)される)

実質的な効果は、サーバーが HTTP 302 リダイレクトで応答すると、ハンドルされない例外が発生した要求が終了することです。 カスタムエラーページへの後続の要求は、新しい要求です。この時点までに、ASP.NET エンジンはエラー情報を破棄し、さらに、前の要求のハンドルされない例外を、カスタムエラーページの新しい要求と関連付けることができません。 このため、カスタムエラーページから呼び出されたときに `GetLastError` `null` 返されます。

ただし、エラーの原因となった同じ要求でカスタムエラーページを実行することもできます。 [`Server.Transfer(url)`](https://msdn.microsoft.com/library/system.web.httpserverutility.transfer.aspx)メソッドは、指定された URL に実行を転送し、同じ要求内でそれを処理します。 `Application_Error` イベントハンドラー内のコードをカスタムエラーページの分離コードクラスに移動し、`Global.asax` 内のコードを次のコードに置き換えることができます。

[!code-vb[Main](processing-unhandled-exceptions-vb/samples/sample5.vb)]

ハンドルされない例外が発生すると、`Application_Error` イベントハンドラーは、HTTP 状態コードに基づいて、適切なカスタムエラーページに制御を転送します。 コントロールが転送されたため、カスタムエラーページは `Server.GetLastError` 経由でハンドルされない例外情報にアクセスできるようになり、エラーを開発者に通知し、その詳細をログに記録できます。 `Server.Transfer` の呼び出しでは、ASP.NET エンジンによって、ユーザーがカスタムエラーページにリダイレクトされるのを防ぐことができます。 代わりに、カスタムエラーページのコンテンツが、エラーを生成したページへの応答として返されます。

## <a name="summary"></a>まとめ

ASP.NET web アプリケーションでハンドルされない例外が発生すると、ASP.NET ランタイムによって `Error` イベントが発生し、構成されたエラーページが表示されます。 エラーイベントのイベントハンドラーを作成することによって、エラーを開発者に通知したり、その詳細をログに記録したり、他の方法で処理したりすることができます。 `Global.asax` ファイルまたは HTTP モジュールから `Error`のような `HttpApplication` イベントのイベントハンドラーを作成するには、次の2つの方法があります。 このチュートリアルでは、`Global.asax` ファイルに `Error` イベントハンドラーを作成して、電子メールメッセージを使ってエラーを開発者に通知する方法について説明しました。

`Error` イベントハンドラーの作成は、何らかの独自の方法で未処理の例外を処理する必要がある場合に便利です。 ただし、例外をログに記録したり開発者に通知したりするために独自の `Error` イベントハンドラーを作成することは、時間をできるだけ効率的に使用することではありません。既に存在していて、数分でも設定できるエラーログライブラリが既に存在しているためです。 次の2つのチュートリアルでは、2つのライブラリを確認します。

プログラミングを楽しんでください。

### <a name="further-reading"></a>参考資料

このチュートリアルで説明しているトピックの詳細については、次のリソースを参照してください。

- [ASP.NET HTTP モジュールと HTTP ハンドラーの概要](https://support.microsoft.com/kb/307985)
- [未処理の例外への適切な応答-未処理の例外の処理](http://aspnet.4guysfromrolla.com/articles/091306-1.aspx)
- [`HttpApplication` クラスと ASP.NET Application オブジェクト](http://www.eggheadcafe.com/articles/20030211.asp)
- [ASP.NET の HTTP ハンドラーと HTTP モジュール](http://www.15seconds.com/Issue/020417.htm)
- [ASP.NET で電子メールを送信しています](http://aspnet.4guysfromrolla.com/articles/072606-1.aspx)
- [`Global.asax` ファイルについて](http://aspalliance.com/1114_Understanding_the_Globalasax_file.all)
- [HTTP モジュールとハンドラーを使用してプラグ可能な ASP.NET コンポーネントを作成する](https://msdn.microsoft.com/library/aa479332.aspx)
- [ASP.NET `Global.asax` ファイルの操作](http://articles.techrepublic.com.com/5100-10878_11-5771721.html)
- [`HttpApplication` インスタンスの操作](https://msdn.microsoft.com/library/a0xez8f2.aspx)

> [!div class="step-by-step"]
> [前へ](displaying-a-custom-error-page-vb.md)
> [次へ](logging-error-details-with-asp-net-health-monitoring-vb.md)
