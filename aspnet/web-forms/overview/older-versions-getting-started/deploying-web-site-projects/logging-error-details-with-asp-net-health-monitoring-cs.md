---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/logging-error-details-with-asp-net-health-monitoring-cs
title: ASP.NET Health Monitoring (C#) を使用してエラーの詳細をログに記録するMicrosoft Docs
author: rick-anderson
description: Microsoft の正常性監視システムは、ハンドルされない例外など、さまざまな web イベントをログに記録するための簡単でカスタマイズ可能な方法を提供します。 このチュートリアルでは、そのについて説明します。
ms.author: riande
ms.date: 06/09/2009
ms.assetid: b1abb452-642a-4ff3-8504-37b85590ff79
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/logging-error-details-with-asp-net-health-monitoring-cs
msc.type: authoredcontent
ms.openlocfilehash: e52ed94f78d053701771690fce432d5a1d465b62
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78520996"
---
# <a name="logging-error-details-with-aspnet-health-monitoring-c"></a>ASP.NET の状態監視でエラーの詳細をログに記録する (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[コードのダウンロード](https://download.microsoft.com/download/1/0/C/10CC829F-A808-4302-97D3-59989B8F9C01/ASPNET_Hosting_Tutorial_13_CS.zip)または[PDF のダウンロード](https://download.microsoft.com/download/5/C/5/5C57DB8C-5DEA-4B3A-92CA-4405544D313B/aspnet_tutorial13_HealthMonitoring_cs.pdf)

> Microsoft の正常性監視システムは、ハンドルされない例外など、さまざまな web イベントをログに記録するための簡単でカスタマイズ可能な方法を提供します。 このチュートリアルでは、未処理の例外をデータベースに記録し、電子メールメッセージを使用して開発者に通知するように、正常性監視システムを設定する手順について説明します。

## <a name="introduction"></a>はじめに

ログ記録は、デプロイされたアプリケーションの正常性を監視し、発生する可能性のある問題を診断するのに便利なツールです。 配置されたアプリケーションで発生したエラーを記録して、問題を解決できるようにすることは、特に重要です。 ASP.NET アプリケーションでハンドルされない例外が発生するたびに、`Error` イベントが発生します。[前のチュートリアル](processing-unhandled-exceptions-cs.md)では、`Error` イベントのイベントハンドラーを作成して、エラーを開発者に通知し、その詳細をログに記録する方法を説明しました。 ただし、このタスクは ASP で実行できるため、エラーの詳細を記録し、開発者に通知するための `Error` イベントハンドラーを作成する必要はありません。NET の*正常性監視システム*。

正常性監視システムは ASP.NET 2.0 で導入され、アプリケーションまたは要求の有効期間中に発生するイベントをログに記録することによって、デプロイされた ASP.NET アプリケーションの正常性を監視するように設計されています。 正常性監視システムによってログに記録されるイベントは、*正常性監視イベント*または*Web イベント*と呼ばれ、次のものが含まれます。

- アプリケーションの有効期間イベント (アプリケーションの開始時や停止時など)
- 失敗したログイン試行と失敗した URL 承認要求を含むセキュリティイベント
- 他の種類のエラーの中で、ハンドルされない例外、ビューステート解析例外、要求検証例外、コンパイルエラーなど、アプリケーションエラーが発生します。

正常性監視イベントが発生すると、指定した任意の数の*ログソースにログ*を記録できます。 正常性監視システムには、Microsoft SQL Server データベース、Windows イベントログ、または電子メールメッセージを使用して、Web イベントをログに記録するログソースが付属しています。 独自のログソースを作成することもできます。

正常性監視システムログが使用されているログソースと共に、`Web.config`で定義されているイベント。 構成マークアップが数行あるので、正常性監視を使用して、未処理の例外をすべてデータベースに記録し、電子メールで例外を通知することができます。

## <a name="exploring-the-health-monitoring-systems-configuration"></a>正常性監視システムの構成の調査

正常性監視システムの動作は、構成情報によって定義されます。これは、`Web.config`の[`<healthMonitoring>` 要素](https://msdn.microsoft.com/library/2fwh2ss9.aspx)にあります。 この構成セクションでは、特に次の3つの重要な情報を定義します。

1. 発生した正常性監視イベントは、ログに記録されます。
2. ログソース
3. (1) で定義されている各正常性監視イベントを、(2) で定義されているログソースにマップする方法。

この情報は、3つの子構成要素 ( [`<eventMappings>`](https://msdn.microsoft.com/library/yc5yk01w.aspx)、 [`<providers>`](https://msdn.microsoft.com/library/zaa41kz1.aspx)、および[`<rules>`](https://msdn.microsoft.com/library/fe5wyxa0.aspx)) を使用して指定します。

既定の正常性監視システムの構成情報は、`%WINDIR%\Microsoft.NET\Framework\version\CONFIG` フォルダーの `Web.config` ファイルにあります。 この既定の構成情報は、簡略化のために一部のマークアップが削除されたものです。以下に示します。

[!code-xml[Main](logging-error-details-with-asp-net-health-monitoring-cs/samples/sample1.xml)]

対象の正常性監視イベントは、`<eventMappings>` 要素で定義されます。これにより、状態監視イベントのクラスにわかりやすい名前が付けられます。 上のマークアップでは、`<eventMappings>` 要素によって、種類が `WebBaseErrorEvent` の正常性監視イベントに "すべてのエラー" という名前のユーザーフレンドリ名と、`WebFailureAuditEvent`種類の正常性監視イベントに "失敗の監査" という名前が割り当てられます。

`<providers>` 要素は、ログソースを定義し、ユーザーにわかりやすい名前を付けて、ログソース固有の構成情報を指定します。 最初の `<add>` 要素は、"EventLogProvider" プロバイダーを定義します。このプロバイダーは、`EventLogWebEventProvider` クラスを使用して、指定された正常性監視イベントをログに記録します。 `EventLogWebEventProvider` クラスは、イベントを Windows イベントログに記録します。 2番目の `<add>` 要素は、"SqlWebEventProvider" プロバイダーを定義します。このプロバイダーは、`SqlWebEventProvider` クラスを使用して、Microsoft SQL Server データベースにイベントを記録します。 "SqlWebEventProvider" 構成では、他の構成オプションの間にデータベースの接続文字列 (`connectionStringName`) を指定します。

`<rules>` 要素は、`<eventMappings>` 要素で指定されたイベントを `<providers>` 要素のログソースにマップします。 既定では、ASP.NET web アプリケーションは、未処理の例外と監査エラーをすべて Windows イベントログに記録します。

## <a name="logging-events-to-a-database"></a>データベースへのイベントのログ記録

正常性監視システムの既定の構成は、アプリケーションの `Web.config` ファイルに `<healthMonitoring>` セクションを追加することで、web アプリケーションによって web アプリケーションごとにカスタマイズできます。 `<add>` 要素を使用して、`<eventMappings>`、`<providers>`、および `<rules>` セクションに追加の要素を含めることができます。 既定の構成から設定を削除するには、`<remove>` 要素を使用するか、または `<clear />` を使用して、これらのセクションのいずれかからすべての既定値を削除します。 `SqlWebEventProvider` クラスを使用して、すべての未処理の例外を Microsoft SQL Server データベースに記録するように Book review web アプリケーションを構成してみましょう。

`SqlWebEventProvider` クラスは、正常性監視システムの一部であり、指定された SQL Server データベースに正常性監視イベントを記録します。 `SqlWebEventProvider` クラスでは、指定されたデータベースに `aspnet_WebEvent_LogEvent`という名前のストアドプロシージャが含まれていることを想定しています。 このストアドプロシージャにはイベントの詳細が渡され、イベントの詳細が格納されます。 このストアドプロシージャを作成したり、イベントの詳細を格納するテーブルを作成したりする必要がないということをお勧めします。 これらのオブジェクトは、`aspnet_regsql.exe` ツールを使用してデータベースに追加できます。

> [!NOTE]
> `aspnet_regsql.exe` ツールは、ASP のサポートを追加したときに[*アプリケーションサービスチュートリアルを使用する web サイトの構成*](configuring-a-website-that-uses-application-services-cs.md)について説明しました。NET のアプリケーションサービス。 その結果、書籍のレビュー web サイトのデータベースには、`aspnet_WebEvent_Events`という名前のテーブルにイベント情報を格納する `aspnet_WebEvent_LogEvent` ストアドプロシージャが既に含まれています。

必要なストアドプロシージャとテーブルがデータベースに追加されたら、すべての未処理の例外をデータベースに記録するように正常性監視に指示します。 これを行うには、web サイトの `Web.config` ファイルに次のマークアップを追加します。

[!code-xml[Main](logging-error-details-with-asp-net-health-monitoring-cs/samples/sample2.xml)]

上の状態監視構成マークアップでは `<clear />` 要素を使用して、定義済みの正常性監視の構成情報を `<eventMappings>`、`<providers>`、および `<rules>` の各セクションからワイプします。 次に、各セクションに1つのエントリを追加します。

- `<eventMappings>` 要素は、"すべてのエラー" という名前の1つの正常性監視イベントを定義します。これは、未処理の例外が発生するたびに発生します。
- `<providers>` 要素は、`SqlWebEventProvider` クラスを使用する "Sqlwe傾斜 Entprovider" という名前の単一のログソースを定義します。 `connectionStringName` 属性は、`<connectionStrings>` セクションで定義された接続文字列の名前である "ReviewsConnectionString" に設定されています。
- 最後に、&lt;rules&gt; 要素は、"発生" というイベントが "SqlWebEventProvider" プロバイダーを使用してログに記録される必要があることを示します。

この構成情報は、すべての未処理の例外を書籍レビューデータベースに記録するように、正常性監視システムに指示します。

> [!NOTE]
> `WebBaseErrorEvent` イベントは、サーバーエラーに対してのみ発生します。これは、見つからない ASP.NET リソースの要求など、HTTP エラーに対しては発生しません。 これは、サーバーと HTTP の両方のエラーに対して発生する `HttpApplication` クラスの `Error` イベントの動作とは異なります。

正常性監視システムの動作を確認するには、web サイトにアクセスし、`Genre.aspx?ID=foo`にアクセスしてランタイムエラーを生成します。 適切なエラーページが表示されます。これには、例外の詳細 (ローカルにアクセスした場合) またはカスタムエラーページ (運用環境のサイトにアクセスした場合) が表示されます。 バックグラウンドでは、正常性監視システムによってエラー情報がデータベースに記録されています。 `aspnet_WebEvent_Events` テーブルには1つのレコードが存在する必要があります (**図 1**を参照)。このレコードには、直前に発生したランタイムエラーに関する情報が含まれています。

[![](logging-error-details-with-asp-net-health-monitoring-cs/_static/image2.png)](logging-error-details-with-asp-net-health-monitoring-cs/_static/image1.png)

**図 1**: エラーの詳細が `aspnet_WebEvent_Events` テーブルに記録された  
([クリックすると、フルサイズの画像が表示](logging-error-details-with-asp-net-health-monitoring-cs/_static/image3.png)される)

### <a name="displaying-the-error-log-in-a-web-page"></a>Web ページへのエラーログの表示

Web サイトの現在の構成では、未処理の例外がすべてデータベースに記録されます。 ただし、正常性の監視では、web ページを使用してエラーログを表示するメカニズムは提供されません。 ただし、この情報をデータベースから表示する ASP.NET ページを作成することもできます。 (間もなく表示されるように、エラーの詳細を電子メールメッセージで送信するように選択できます)。

このようなページを作成する場合は、承認されたユーザーのみがエラーの詳細を表示できるようにするための手順を実行してください。 サイトで既にユーザーアカウントが使用されている場合は、URL 承認規則を使用して、ページへのアクセスを特定のユーザーまたはロールに制限することができます。 ログインしたユーザーに基づいて web ページへのアクセスを許可または制限する方法の詳細については、「マイ[Web サイトのセキュリティ](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)に関するチュートリアル」を参照してください。

> [!NOTE]
> 以降のチュートリアルでは、ELMAH という名前の別のエラーログと通知システムについて説明します。 ELMAH には、web ページと RSS フィードの両方からのエラーログを表示するための組み込みメカニズムが含まれています。

## <a name="logging-events-to-email"></a>イベントを電子メールに記録する

正常性監視システムには、イベントを電子メールメッセージに "記録" するログソースプロバイダーが含まれています。 ログソースには、電子メールメッセージの本文でデータベースに記録されるものと同じ情報が含まれています。 このログソースを使用すると、特定の状態監視イベントが発生したときに開発者に通知することができます。

例外が発生するたびに電子メールを受信するように、書籍レビュー web サイトの構成を更新してみましょう。 これを実現するには、次の3つのタスクを実行する必要があります。

1. 電子メールを送信するように ASP.NET web アプリケーションを構成します。 これを行うには、`<system.net>` 構成要素を使用して電子メールメッセージを送信する方法を指定します。 ASP.NET アプリケーションで電子メールメッセージを送信する方法の詳細については、「 [ASP.NET で電子メールを送信する」](http://aspnet.4guysfromrolla.com/articles/072606-1.aspx)および「 [.net の FAQ](http://systemnetmail.com/)」を参照してください。
2. `<providers>` 要素に電子メールログのソースプロバイダーを登録します。
3. ステップ (2) で追加されたログソースプロバイダーに "すべてのエラー" イベントをマップするエントリを `<rules>` 要素に追加します。

正常性監視システムには、`SimpleMailWebEventProvider` と `TemplatedMailWebEventProvider`の2つの電子メールログソースプロバイダークラスが含まれています。 [`SimpleMailWebEventProvider` クラス](https://msdn.microsoft.com/library/system.web.management.simplemailwebeventprovider.aspx)は、イベントの詳細を含むプレーンテキストの電子メールメッセージを送信します。電子メールの本文のカスタマイズはほとんどありません。 [`TemplatedMailWebEventProvider` クラス](https://msdn.microsoft.com/library/system.web.management.templatedmailwebeventprovider.aspx)では、表示されるマークアップが電子メールメッセージの本文として使用される ASP.NET ページを指定します。 [`TemplatedMailWebEventProvider` クラス](https://msdn.microsoft.com/library/system.web.management.templatedmailwebeventprovider.aspx)を使用すると、電子メールメッセージの内容と形式をはるかに細かく制御できますが、電子メールメッセージの本文を生成する ASP.NET ページを作成する必要があるため、より高度な作業が必要になります。 このチュートリアルでは、`SimpleMailWebEventProvider` クラスの使用に重点を置いて説明します。

`Web.config` ファイルの正常性監視システムの `<providers>` 要素を更新して、`SimpleMailWebEventProvider` クラスのログソースを含めます。

[!code-xml[Main](logging-error-details-with-asp-net-health-monitoring-cs/samples/sample3.xml)]

上のマークアップでは、ログソースプロバイダーとして `SimpleMailWebEventProvider` クラスが使用され、フレンドリ名 "Emailwe傾斜 Entprovider" が割り当てられます。 さらに、`<add>` 属性には、電子メールメッセージの宛先アドレスや差出人アドレスなどの追加の構成オプションが含まれています。

電子メールログソースが定義されている状態で、このソースを使用して未処理の例外を "ログに記録" するように、正常性監視システムに指示します。 これを行うには、`<rules>` セクションに新しい規則を追加します。

[!code-xml[Main](logging-error-details-with-asp-net-health-monitoring-cs/samples/sample4.xml)]

`<rules>` セクションに2つのルールが含まれるようになりました。 最初の1つは "すべてのエラーを電子メールで送信する" という名前で、未処理の例外をすべて "Emailwe傾斜" ログソースに送信します。 このルールは、web サイト上のエラーに関する詳細情報を、指定された宛先アドレスに送信する効果を持ちます。 "データベースへのすべてのエラー" ルールによって、エラーの詳細がサイトのデータベースに記録されます。 その結果、サイトでハンドルされない例外が発生するたびに、その詳細がデータベースに記録され、指定された電子メールアドレスに送信されます。

**図 2**は、`Genre.aspx?ID=foo`にアクセスするときに `SimpleMailWebEventProvider` クラスによって生成される電子メールを示しています。

[![](logging-error-details-with-asp-net-health-monitoring-cs/_static/image5.png)](logging-error-details-with-asp-net-health-monitoring-cs/_static/image4.png)

**図 2**: エラーの詳細が電子メールメッセージで送信される  
([クリックすると、フルサイズの画像が表示](logging-error-details-with-asp-net-health-monitoring-cs/_static/image6.png)される)

## <a name="summary"></a>まとめ

ASP.NET health monitoring システムは、管理者が展開された web アプリケーションの正常性を監視できるように設計されています。 正常性監視イベントは、アプリケーションが停止したとき、ユーザーがサイトに正常にログオンしたとき、またはハンドルされない例外が発生したときなど、特定のアクションが展開されると発生します。 これらのイベントは、任意の数のログソースに記録できます。 このチュートリアルでは、未処理の例外の詳細をデータベースおよび電子メールメッセージを使用してログに記録する方法を示しました。

このチュートリアルでは、正常性監視を使用して未処理の例外をログに記録する方法に重点を置いていますが、正常性の監視は、デプロイされた ASP.NET アプリケーションの全体的な正常性を測定するように設計されており、豊富な正常性監視イベントとログソースを含みません。こちらをご覧ください。 さらに、必要に応じて、独自の正常性監視イベントとログソースを作成できます。 正常性の監視について詳しく知りたい場合は、まず、 [Erik Reitan](https://blogs.msdn.com/erikreitan/archive/2006/05/22/603586.aspx)の[正常性監視](https://blogs.msdn.com/erikreitan/archive/2006/05/22/603586.aspx)に関する FAQ を参照してください。 詳細については、「[方法: ASP.NET 2.0 の正常性監視を使用する」](https://msdn.microsoft.com/library/ms998306.aspx)を参照してください。

プログラミングを楽しんでください。

### <a name="further-reading"></a>参考資料

このチュートリアルで説明しているトピックの詳細については、次のリソースを参照してください。

- [ASP.NET の正常性監視の概要](https://msdn.microsoft.com/library/bb398933.aspx)
- [ASP.NET の正常性監視システムの構成とカスタマイズ](http://dotnetslackers.com/articles/aspnet/ConfiguringAndCustomizingTheHealthMonitoringSystemOfASPNET.aspx)
- [FAQ-ASP.NET 2.0 での正常性の監視](https://blogs.msdn.com/erikreitan/archive/2006/05/22/603586.aspx)
- [方法: 正常性の監視通知用に電子メールを送信する](https://msdn.microsoft.com/library/ms227553.aspx)
- [方法: ASP.NET で正常性監視を使用する](https://msdn.microsoft.com/library/ms998306.aspx)
- [ASP.NET の正常性の監視](http://aspnet.4guysfromrolla.com/articles/031407-1.aspx)

> [!div class="step-by-step"]
> [前へ](processing-unhandled-exceptions-cs.md)
> [次へ](logging-error-details-with-elmah-cs.md)
