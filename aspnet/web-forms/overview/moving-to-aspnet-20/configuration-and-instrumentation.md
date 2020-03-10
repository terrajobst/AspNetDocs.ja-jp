---
uid: web-forms/overview/moving-to-aspnet-20/configuration-and-instrumentation
title: 構成とインストルメンテーション |Microsoft Docs
author: microsoft
description: ASP.NET 2.0 では、構成とインストルメンテーションに大きな変更が加えられています。 新しい ASP.NET configuration API を使用して、構成の変更を pr...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 21ebbaee-7ed8-45ae-b6c1-c27c88342e48
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/configuration-and-instrumentation
msc.type: authoredcontent
ms.openlocfilehash: cd5bedce5459e8cf8e72df8de69ebd82f2d97789
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78507880"
---
# <a name="configuration-and-instrumentation"></a>構成とインストルメンテーション

[Microsoft](https://github.com/microsoft)

> ASP.NET 2.0 では、構成とインストルメンテーションに大きな変更が加えられています。 新しい ASP.NET configuration API では、構成の変更をプログラムで行うことができます。 さらに、新しい構成設定の多くは、新しい構成とインストルメンテーションを可能にします。

ASP.NET 2.0 では、構成とインストルメンテーションに大きな変更が加えられています。 新しい ASP.NET configuration API では、構成の変更をプログラムで行うことができます。 さらに、新しい構成設定の多くは、新しい構成とインストルメンテーションを可能にします。

このモジュールでは、ASP.NET 構成ファイルの読み取りと書き込みに関連する構成 API の ASP.NET について説明します。また、ASP.NET インストルメンテーションについても説明します。 また、ASP.NET tracing で利用できる新機能についても説明します。

## <a name="aspnet-configuration-api"></a>ASP.NET 構成 API

ASP.NET configuration API を使用すると、単一のプログラミングインターフェイスを使用して、アプリケーション構成データを開発、展開、および管理できます。 構成 API を使用して、構成ファイル内の XML を直接編集せずに、完全な ASP.NET 構成をプログラムで開発および変更できます。 また、構成 API は、開発したコンソールアプリケーションやスクリプト、Web ベースの管理ツール、および Microsoft 管理コンソール (MMC) スナップインでも使用できます。

次の2つの構成管理ツールは、構成 API を使用し、.NET Framework バージョン2.0 に含まれています。

- ASP.NET MMC スナップイン。構成 API を使用して管理タスクを簡略化し、構成階層のすべてのレベルのローカル構成データを統合して表示します。
- Web サイト管理ツール。ホストされているサイトを含む、ローカルおよびリモートのアプリケーションの構成設定を管理できます。

ASP.NET configuration API は、Web サイトおよびアプリケーションをプログラムで構成するために使用できる一連の ASP.NET 管理オブジェクトで構成されています。 管理オブジェクトは、.NET Framework クラスライブラリとして実装されます。 構成 API プログラミングモデルは、コンパイル時にデータ型を適用することによって、コードの一貫性と信頼性を確保するのに役立ちます。 アプリケーションの構成を管理しやすくするために、構成 API を使用すると、異なるコレクションとしてデータを表示するのではなく、構成階層内のすべてのポイントから1つのコレクションとしてマージされたデータを表示することができます。構成ファイル。 また、構成 API を使用すると、構成ファイル内の XML を直接編集することなく、アプリケーション構成全体を操作できます。 最後に、API は、Web サイト管理ツールなどの管理ツールをサポートすることで、構成タスクを簡略化します。 構成 API は、コンピューター上で構成ファイルを作成し、複数のコンピューター間で構成スクリプトを実行することで、展開を簡略化します。

> [!NOTE]
> 構成 API は、IIS アプリケーションの作成をサポートしていません。

## <a name="working-with-local-and-remote-configuration-settings"></a>ローカルおよびリモートの構成設定の操作

構成オブジェクトは、コンピューターなどの特定の物理エンティティ、またはアプリケーションや Web サイトなどの論理エンティティに適用される構成設定の結合されたビューを表します。 指定された論理エンティティは、ローカルコンピューターまたはリモートサーバー上に存在することができます。 指定されたエンティティの構成ファイルが存在しない場合、構成オブジェクトは、machine.config ファイルで定義されている既定の構成設定を表します。

構成オブジェクトを取得するには、次のクラスのオープン構成メソッドのいずれかを使用します。

1. ConfigurationManager クラス (エンティティがクライアントアプリケーションの場合)。
2. WebConfigurationManager クラス (エンティティが Web アプリケーションの場合)。

これらのメソッドは、構成オブジェクトを返します。構成オブジェクトは、基になる構成ファイルを処理するために必要なメソッドとプロパティを提供します。 これらのファイルには、読み取りまたは書き込みのためにアクセスできます。

### <a name="reading"></a>リード

構成情報を読み取るには、GetSection または GetSectionGroup メソッドを使用します。 読み取りを行うユーザーまたはプロセスは、階層内のすべての構成ファイルに対する読み取り権限を持っている必要があります。

> [!NOTE]
> Path パラメーターを受け取る静的 GetSection メソッドを使用する場合、path パラメーターは、コードが実行されているアプリケーションを参照する必要があります。 それ以外の場合、パラメーターは無視され、現在実行中のアプリケーションの構成情報が返されます。

### <a name="writing"></a>手書き

Save メソッドのいずれかを使用して、構成情報を書き込みます。 書き込みを行うユーザーまたはプロセスは、現在の構成階層レベルの構成ファイルおよびディレクトリに対する書き込みアクセス許可、および階層内のすべての構成ファイルに対する読み取りアクセス許可を持っている必要があります。

指定したエンティティの継承された構成設定を表す構成ファイルを生成するには、次のいずれかの保存構成方法を使用します。

1. 新しい構成ファイルを作成するための Save メソッド。
2. 別の場所に新しい構成ファイルを生成するための SaveAs メソッド。

## <a name="configuration-classes-and-namespaces"></a>構成クラスと名前空間

多くの構成クラスとメソッドは相互に似ています。 次の表では、最も一般的に使用される構成クラスと名前空間について説明します。

| **構成クラスまたは名前空間** | **説明** |
| --- | --- |
| [System. Configuration](https://msdn.microsoft.com/library/system.configuration.aspx)名前空間 | すべての .NET Framework アプリケーションのメイン構成クラスが含まれています。 セクションハンドラークラスは、GetSection や GetSectionGroup などのメソッドからセクションの構成データを取得するために使用されます。 これらの2つのメソッドは非静的です。 |
| System. Configuration クラス | コンピューター、アプリケーション、Web ディレクトリ、またはその他のリソースの構成データのセットを表します。 このクラスには、構成設定を更新したり、セクションやセクショングループへの参照を取得したりするための、GetSection や GetSectionGroup などの便利なメソッドが含まれています。 このクラスは、WebConfigurationManager クラスと ConfigurationManager クラスのメソッドなど、デザイン時の構成データを取得するメソッドの戻り値の型として使用されます。 |
| System.web. Configuration 名前空間 | [ASP.NET 構成設定](https://msdn.microsoft.com/library/b5ysx397.aspx)で定義されている ASP.NET 構成セクションのセクションハンドラークラスが含まれています。 セクションハンドラークラスは、GetSection や GetSectionGroup などのメソッドからセクションの構成データを取得するために使用されます。 |
| System.Web.Configuration.WebConfigurationManager class | 実行時およびデザイン時の構成設定への参照を取得するための便利なメソッドを提供します。 これらのメソッドは、戻り値の型として system.object クラスを使用します。 このクラスの静的な GetSection メソッド、または ConfigurationManager クラスの非静的 GetSection メソッドを同じように使用できます。 Web アプリケーション構成の場合は、ConfigurationManager クラスの代わりに WebConfigurationManager クラスを使用することをお勧めします。 |
| System.servicemodel[名前空間](https://msdn.microsoft.com/library/system.configuration.provider.aspx) | 構成プロバイダーをカスタマイズおよび拡張する方法を提供します。 これは、構成システム内のすべてのプロバイダークラスの基本クラスです。 |
| [System.web](https://msdn.microsoft.com/library/system.web.management.aspx)名前空間 | Web アプリケーションの正常性を管理および監視するためのクラスとインターフェイスが含まれています。 厳密に言うと、この名前空間は、構成 API の一部とは見なされません。 たとえば、トレースとイベントの発生は、この名前空間のクラスによって行われます。 |
| System.servicemodel[名前空間](https://msdn.microsoft.com/library/system.management.instrumentation.aspx) | アプリケーションのインストルメンテーションが Windows Management Instrumentation (WMI) を介して潜在的なコンシューマーに管理情報とイベントを公開するために必要なクラスを提供します。 ASP.NET の正常性の監視では、WMI を使用してイベントを配信します。 厳密に言うと、この名前空間は、構成 API の一部とは見なされません。 |

## <a name="reading-from-aspnet-configuration-files"></a>ASP.NET 構成ファイルからの読み取り

WebConfigurationManager クラスは、ASP.NET 構成ファイルから読み取るためのコアクラスです。 ASP.NET 構成ファイルを読み取るには、基本的に次の3つの手順を実行します。

1. OpenWebConfiguration メソッドを使用して構成オブジェクトを取得します。
2. 構成ファイルの目的のセクションへの参照を取得します。
3. 構成ファイルから必要な情報を読み取ります。

構成オブジェクトは、が特定の構成ファイルを表していないことを表します。 代わりに、コンピューター、アプリケーション、または Web サイトの構成の結合されたビューを表します。 次のコードサンプルでは、 *Productinfo*という名前の Web アプリケーションの構成を表す構成オブジェクトをインスタンス化します。

[!code-csharp[Main](configuration-and-instrumentation/samples/sample1.cs)]

> [!NOTE]
> /Productinfo パスが存在しない場合、上記のコードは machine.config ファイルで指定されている既定の構成を返します。

構成オブジェクトを作成したら、GetSection または GetSectionGroup メソッドを使用して構成設定をドリルダウンできます。 次の例では、上記の ProductInfo アプリケーションの権限借用設定への参照を取得します。

[!code-csharp[Main](configuration-and-instrumentation/samples/sample2.cs)]

## <a name="writing-to-aspnet-configuration-files"></a>ASP.NET 構成ファイルへの書き込み

構成ファイルの読み取りと同様に、WebConfigurationManager クラスは Asp.NET 構成ファイルへの書き込みのためのコアです。 また、ASP.NET 構成ファイルに書き込む3つの手順もあります。

1. OpenWebConfiguration メソッドを使用して構成オブジェクトを取得します。
2. 構成ファイルの目的のセクションへの参照を取得します。
3. Save または SaveAs メソッドを使用して、構成ファイルから必要な情報を書き込みます。

次のコードでは、&lt;のコンパイル&gt; 要素の**debug**属性を false に変更します。

[!code-csharp[Main](configuration-and-instrumentation/samples/sample3.cs)]

このコードが実行されると、 *webApp*アプリケーションの web.config ファイルに対して、&lt;のコンパイル&gt; 要素の**debug**属性が false に設定されます。

## <a name="systemwebmanagement-namespace"></a>System.web 名前空間

ASP.NET 名前空間には、アプリケーションの正常性を管理および監視するためのクラスとインターフェイスが用意されています。

ログ記録を行うには、イベントをプロバイダーに関連付けるルールを定義します。 このルールは、プロバイダーに送信されるイベントの種類を定義します。 次の基本イベントをログに記録できます。

| **WebBaseEvent** | すべてのイベントの基本イベントクラス。 イベントコード、イベントの詳細コード、イベントが発生した日付と時刻、シーケンス番号、イベントメッセージ、イベントの詳細など、すべてのイベントに必要なプロパティが含まれています。 |
| --- | --- |
| **WebManagementEvent** | アプリケーションの有効期間、要求、エラー、監査イベントなどの管理イベントの基本イベントクラス。 |
| **WebHeartbeatEvent** | 有効なランタイム状態情報をキャプチャするために、アプリケーションによって定期的に生成されるイベント。 |
| **WebAuditEvent** | セキュリティ監査イベントの基本クラス。承認エラー、復号化エラーなどの条件をマークするために使用され*ます。* |
| **WebRequestEvent** | すべての情報要求イベントの基本クラス。 |
| **WebBaseErrorEvent** | エラー状態を示すすべてのイベントの基本クラス。 |

使用可能なプロバイダーの種類により、イベント出力をイベントビューアー、SQL Server、Windows Management Instrumentation (WMI)、および電子メールに送信できます。 事前構成済みのプロバイダーとイベントマッピングによって、イベント出力を記録するために必要な作業量が削減されます。

ASP.NET 2.0 では、イベントログプロバイダーをすぐに使用して、アプリケーションドメインの開始と停止に基づくイベントをログに記録し、未処理の例外をログに記録します。 これは、いくつかの基本的なシナリオに対応するのに役立ちます。 たとえば、アプリケーションで例外がスローされても、ユーザーがエラーを保存せず、再現できないとします。 既定のイベントログルールでは、例外とスタック情報を収集して、発生したエラーの種類をより正確に把握することができます。 もう1つの例は、アプリケーションがセッション状態を失う場合に適用されます。 その場合は、イベントログを調べて、アプリケーションドメインがリサイクルされているかどうかと、アプリケーションドメインが最初に停止した理由を確認します。

また、正常性監視システムは拡張可能です。 たとえば、カスタム Web イベントを定義してアプリケーション内で起動し、電子メールなどのイベント情報をプロバイダーに送信するルールを定義できます。 これにより、インストルメンテーションを正常性監視プロバイダーに簡単に結び付けることができます。 別の例として、注文が処理されるたびにイベントを発生させ、各イベントを SQL Server データベースに送信するルールを設定することもできます。 また、ユーザーが行で複数回ログオンに失敗した場合にイベントを発生させ、電子メールベースのプロバイダーを使用するようにイベントを設定することもできます。

既定のプロバイダーとイベントの構成は、グローバルな web.config ファイルに格納されます。 グローバルな web.config ファイルには、machine.config ファイルに格納されていたすべての Web ベースの設定が ASP.NET 1x で格納されます。 グローバルな Web.config ファイルは、次のディレクトリにあります。

`%windir%\Microsoft.Net\Framework\v2.0.*\config\Web.config`

グローバル Web.config ファイルの &lt;healthMonitoring&gt; セクションには、既定の構成設定が用意されています。 アプリケーションの web.config ファイルの &lt;healthMonitoring&gt; セクションを実装することで、これらの設定をオーバーライドしたり、独自の設定を構成したりすることができます。

グローバル Web.config ファイルの &lt;healthMonitoring&gt; セクションには、次の項目が含まれています。

| **providers** | イベントビューアー、WMI、および SQL Server 用に設定されたプロバイダーが含まれます。 |
| --- | --- |
| **eventMappings** | さまざまな WebBase クラスのマッピングが含まれています。 独自のイベントクラスを生成する場合は、このリストを拡張できます。 独自のイベントクラスを生成することにより、情報を送信するプロバイダーの粒度が細かくなります。 たとえば、未処理の例外を SQL Server に送信するように構成し、独自のカスタムイベントを電子メールに送信することができます。 |
| **ロジック** | EventMappings をプロバイダーにリンクします。 |
| **ング** | SQL Server および電子メールプロバイダーと共に使用して、イベントをプロバイダーにフラッシュする頻度を決定します。 |

グローバルな web.config ファイルのコード例を次に示します。

[!code-xml[Main](configuration-and-instrumentation/samples/sample4.xml)]

## <a name="how-to-store-events-to-event-viewer"></a>イベントをイベントビューアーに格納する方法

既に説明したように、イベントビューアーのイベントをログに記録するためのプロバイダーは、グローバルな web.config ファイルで構成されています。 既定では、 **Webbaseerrorevent**と**webbaseerrorevent**に基づくすべてのイベントがログに記録されます。 追加のルールを追加して、イベントログに追加情報を記録することができます。 たとえば、すべてのイベント (*つまり*、 **WebBaseEvent**に基づくすべてのイベント) をログに記録する場合は、次の規則を web.config ファイルに追加します。

[!code-xml[Main](configuration-and-instrumentation/samples/sample5.xml)]

このルールにより、**すべて**のイベントのイベントマップがイベントログプロバイダーにリンクされます。 EventMapping とプロバイダーの両方がグローバル Web.config ファイルに含まれています。

## <a name="how-to-store-events-to-sql-server"></a>イベントを SQL Server に格納する方法

このメソッドは、 **aspnetdb.mdf**データベースを使用します。これは、Aspnet\_regsql .exe ツールによって生成されます。 既定のプロバイダーは、LocalSqlServer 接続文字列を使用します。これは、App\_data フォルダー内のファイルベースのデータベースまたは SQL Server のローカル SQLExpress インスタンスのいずれかを使用します。 LocalSqlServer 接続文字列と SqlProvider は両方とも、グローバル Web.config ファイルで構成されます。

グローバルな Web.config ファイル内の LocalSqlServer 接続文字列は、次のようになります。

[!code-xml[Main](configuration-and-instrumentation/samples/sample6.xml)]

別の SQL Server インスタンスを使用する場合は、Aspnet\_regsql ツールを使用する必要があります。これは、%windir%\Microsoft.Net\Framework\v2.0. にあります。\* フォルダー。 Aspnet\_regsql .exe ツールを使用して SQL Server インスタンスでカスタム**aspnetdb.mdf**データベースを生成し、アプリケーション構成ファイルに接続文字列を追加して、新しい接続文字列を使用してプロバイダーを追加します。 **Aspnetdb.mdf**データベースを作成したら、Eventmapping を sqlprovider にリンクするルールを設定する必要があります。

既定の SqlProvider を使用するか、独自のプロバイダーを構成するかにかかわらず、プロバイダーとイベントマップをリンクするルールを追加する必要があります。 次の規則は、上記で作成した新しいプロバイダーを、**すべてのイベント**のイベントマップにリンクします。 このルールは、 **WebBaseEvent**に基づいてすべてのイベントをログに記録し、MYASPNETDB 接続文字列を使用する MySqlWebEventProvider に送信します。 次のコードは、プロバイダーをイベントマップにリンクするルールを追加します。

[!code-xml[Main](configuration-and-instrumentation/samples/sample7.xml)]

SQL Server にのみエラーを送信する場合は、次の規則を追加します。

[!code-xml[Main](configuration-and-instrumentation/samples/sample8.xml)]

## <a name="how-to-forward-events-to-wmi"></a>WMI にイベントを転送する方法

また、イベントを WMI に転送することもできます。 既定では、WMI プロバイダーはグローバル web.config ファイルで構成されます。

次のコード例では、イベントを WMI に転送するルールを追加します。

[!code-xml[Main](configuration-and-instrumentation/samples/sample9.xml)]

EventMapping をプロバイダに関連付けるルールを追加し、イベントをリッスンする WMI リスナアプリケーションを追加する必要があります。 次のコード例では、WMI プロバイダーを**すべてのイベント**のイベントマップにリンクする規則を追加します。

[!code-xml[Main](configuration-and-instrumentation/samples/sample10.xml)]

## <a name="how-to-forward-events-to-email"></a>イベントを電子メールに転送する方法

また、イベントを電子メールに転送することもできます。 電子メールプロバイダーにマップするイベントルールに注意してください。 SQL Server やイベントログにより適した大量の情報を誤って送信する可能性があります。 電子メールプロバイダーは2つあります。SimpleMailWebEventProvider と TemplatedMailWebEventProvider。 それぞれの構成属性は同じですが、"template" 属性と "detailedTemplateErrors" 属性を除いて、どちらも TemplatedMailWebEventProvider でのみ使用できます。

> [!NOTE]
> これらの電子メールプロバイダーはいずれも構成されていません。 これらのファイルは、web.config ファイルに追加する必要があります。

これら2つの電子メールプロバイダーの主な違いは、SimpleMailWebEventProvider が、変更できない汎用テンプレートに電子メールを送信することです。 サンプルの web.config ファイルは、次の規則を使用して、構成されたプロバイダーの一覧にこの電子メールプロバイダーを追加します。

[!code-xml[Main](configuration-and-instrumentation/samples/sample11.xml)]

次の規則は、電子メールプロバイダーを**すべてのイベント**のイベントマップに関連付けるためにも追加されています。

[!code-xml[Main](configuration-and-instrumentation/samples/sample12.xml)]

## <a name="aspnet-20-tracing"></a>ASP.NET 2.0 トレース

ASP.NET 2.0 でのトレースには、主に3つの拡張機能があります。

1. 統合トレース機能
2. プログラムによるトレースメッセージへのアクセス
3. 改善されたアプリケーションレベルのトレース

## <a name="integrated-tracing-functionality"></a>統合トレース機能

これで、ASP.NET クラスによって出力されたメッセージを、トレース出力にルーティングし、ASP.NET トレースによって生成されたメッセージをにルーティングできるようになりました。 ASP.NET インストルメンテーションイベントをトレースに転送することもできます。 この機能は、&lt;trace&gt; 要素の new **writeToDiagnosticsTrace**属性によって提供されます。 このブール値が true の場合、ASP.NET トレースメッセージは、トレースメッセージを表示するように登録されているリスナーによって使用されるように、システム診断トレースインフラストラクチャに転送されます。

## <a name="programmatic-access-to-trace-messages"></a>プログラムによるトレースメッセージへのアクセス

ASP.NET 2.0 では、 **TraceContextRecord**クラスと**TraceRecords** collection を介して、すべてのトレースメッセージにプログラムでアクセスできます。 トレースメッセージにアクセスする最も効率的な方法は、 **TraceContextEventHandler**デリゲート (ASP.NET 2.0 の新機能) を登録して、新しい**tracefinished**イベントを処理することです。 その後、必要に応じてトレースメッセージをループ処理できます。

次のコードサンプルはこれを示しています。

[!code-csharp[Main](configuration-and-instrumentation/samples/sample13.cs)]

上の例では、TraceRecords コレクションをループ処理し、各メッセージを応答ストリームに書き込みます。

## <a name="improved-application-level-tracing"></a>改善されたアプリケーションレベルのトレース

アプリケーションレベルのトレースは、&lt;trace&gt; 要素**の新しい属性である新しい属性**の導入によって改善されています。 この属性は、最新のアプリケーションレベルのトレース出力を表示するかどうかを指定します。また、requestLimit によって示される制限を超える古いトレースデータを破棄するかどうかを指定します。 False の場合、requestLimit 属性に到達するまで、要求に対してトレースデータが表示されます。

## <a name="aspnet-command-line-tools"></a>ASP.NET コマンドラインツール

ASP.NET の構成を支援するためのコマンドラインツールがいくつかあります。 ASP.NET の開発者は、aspnet\_iis 登録ツールツールについて理解している必要があります。 ASP.NET 2.0 には、構成に役立つ3つのコマンドラインツールが他にも用意されています。

次のコマンドラインツールを使用できます。

| **ツール** | **用途** |
| --- | --- |
| **aspnet\_iis 登録ツール** | ASP.NET を IIS に登録できるようにします。 このツールには、ASP.NET 2.0 に付属している2つのバージョンがあります。1つは32ビットシステム用 (フレームワークフォルダー内) で、もう1つは64ビットシステム用 (Framework64 フォルダーにあります) です。64ビットバージョンは32ビット OS にはインストールされません。 |
| **aspnet\_regsql .exe** | ASP.NET SQL Server 登録ツールは、ASP.NET の SQL Server プロバイダーが使用する Microsoft SQL Server データベースを作成したり、既存のデータベースのオプションを追加または削除したりするために使用されます。 Aspnet\_regsql .exe ファイルは、Web サーバーの [drive:] \WINDOWS\Microsoft.NET\Framework\versionNumber フォルダーにあります。 |
| **aspnet\_regbrowsers .exe** | ASP.NET Browser 登録ツールは、すべてのシステム全体のブラウザー定義を解析してアセンブリにコンパイルし、アセンブリをグローバルアセンブリキャッシュにインストールします。 このツールでは、ブラウザー定義ファイル () が使用されます。ブラウザーファイル) を .NET Framework BROWSER サブディレクトリからです。 このツールは、%SystemRoot%\Microsoft.NET\Framework\version\ ディレクトリにあります。 |
| **aspnet\_コンパイラ .exe** | ASP.NET コンパイルツールを使用すると、ASP.NET Web アプリケーションをその場で、または運用サーバーなどのターゲットの場所に配置するためにコンパイルできます。 アプリケーションのコンパイル中にアプリケーションへの最初の要求に対して遅延が発生することはないため、インプレースコンパイルはアプリケーションのパフォーマンスを向上させます。 |

Aspnet\_iis 登録ツールツールは ASP.NET 2.0 には新しいものではないため、ここでは説明しません。

## <a name="aspnet-sql-server-registration-tool---aspnet_regsqlexe"></a>ASP.NET SQL Server 登録ツール-aspnet\_regsql .exe

ASP.NET SQL Server 登録ツールを使用して、いくつかの種類のオプションを設定できます。 SQL 接続を指定したり、ASP.NET アプリケーションサービスで SQL Server 使用して情報を管理したり、SQL キャッシュ依存関係に使用するデータベースまたはテーブルを指定したり、SQL Server を使用してプロシージャとセッション状態を格納するためのサポートを追加または削除したりすることができます。

いくつかの ASP.NET アプリケーションサービスは、データソースからのデータの格納と取得を管理するためにプロバイダーに依存しています。 各プロバイダーは、データソースに固有のものです。 ASP.NET には、次の ASP.NET 機能用の SQL Server プロバイダーが含まれています。

- メンバーシップ ( [SqlMembershipProvider](https://msdn.microsoft.com/library/system.web.security.sqlmembershipprovider.aspx)クラス)。
- ロール管理 ( [SqlRoleProvider](https://msdn.microsoft.com/library/system.web.security.sqlroleprovider.aspx)クラス)。
- プロファイル ( [Sqlprofileprovider](https://msdn.microsoft.com/library/system.web.profile.sqlprofileprovider.aspx)クラス)。
- Web パーツパーソナル化 ( [sql、Izationprovider](https://msdn.microsoft.com/library/system.web.ui.webcontrols.webparts.sqlpersonalizationprovider.aspx)クラス)。
- Web イベント ( [Sqlwebeventprovider](https://msdn.microsoft.com/library/system.web.management.sqlwebeventprovider.aspx)クラス)。

ASP.NET をインストールすると、サーバーの machine.config ファイルには、プロバイダーに依存する各 ASP.NET 機能の SQL Server プロバイダーを指定する構成要素が含まれます。 これらのプロバイダーは、既定で SQL Server Express 2005 のローカルユーザーインスタンスに接続するように構成されています。 プロバイダーによって使用される既定の接続文字列を変更した場合は、コンピューターの構成で構成されている ASP.NET 機能を使用する前に、Aspnet\_regsql を使用して、選択した機能の SQL Server データベースとデータベース要素をインストールする必要があります。 SQL 登録ツールで指定したデータベースがまだ存在しない場合 (コマンドラインで aspnetdb.mdf が指定されていない場合は既定のデータベースになります)、現在のユーザーには SQL Server でデータベースを作成する権限、およびスキーマ e を作成する権限が必要です。データベース内の lements。

### <a name="sql-cache-dependency"></a>SQL キャッシュ依存関係

ASP.NET 出力キャッシュの高度な機能は、SQL キャッシュの依存関係です。 SQL キャッシュ依存関係では、2つの異なる操作モードがサポートされます。1つはテーブルポーリングの ASP.NET 実装を使用し、もう1つは SQL Server 2005 のクエリ通知機能を使用する2番目のモードです。 SQL 登録ツールを使用すると、テーブルポーリングモードの操作を構成できます。

### <a name="session-state"></a>セッションの状態

既定では、セッション状態の値と情報は ASP.NET プロセス内のメモリに格納されます。 または、セッションデータを SQL Server データベースに格納して、複数の Web サーバーで共有できるようにすることもできます。 SQL 登録ツールでセッション状態として指定したデータベースがまだ存在しない場合、現在のユーザーには SQL Server でデータベースを作成する権限、およびデータベース内にスキーマ要素を作成する権限が必要です。 データベースが存在する場合、現在のユーザーは、既存のデータベースにスキーマ要素を作成する権限を持っている必要があります。

SQL Server にセッション状態データベースをインストールするには、Aspnet\_regsql ツールを実行し、コマンドに次の情報を指定します。

- **-S**オプションを使用して SQL Server インスタンスの名前。
- SQL Server を実行しているコンピューターにデータベースを作成する権限を持つアカウントのログオン資格情報。 **-E**オプションを使用して、現在ログオンしているユーザーを使用するか、- **U**オプションを使用して **-P**オプションと共にユーザー ID を指定し、パスワードを指定します。
- セッション状態データベースを追加するには、 **-ssadd**コマンドラインオプションを指定します。

既定では、Aspnet\_regsql .exe ツールを使用して、SQL Server 2005 Express Edition を実行しているコンピューターにセッション状態データベースをインストールすることはできません。

### <a name="the-aspnet-browser-registration-tool---aspnet_regbrowsersexe"></a>ASP.NET ブラウザー登録ツール-aspnet\_regbrowsers .exe

ASP.NET バージョン1.1 では、machine.config ファイルに &lt;browserCaps&gt;という名前のセクションが含まれていました。 このセクションには、正規表現に基づいてさまざまなブラウザーの構成を定義する一連の XML エントリが含まれていました。 ASP.NET バージョン2.0 の場合は、新しいです。BROWSER ファイルは、XML エントリを使用して、特定のブラウザーのパラメーターを定義します。 新しいブラウザーに情報を追加するには、新しいを追加します。ブラウザーファイルを、システムの%SystemRoot%\Microsoft.NET\Framework\version\CONFIG\Browsers にあるフォルダーに保存します。

ブラウザー情報が必要になるたびにアプリケーションが .config ファイルを読み取らないため、新しいを作成できます。ブラウザーファイルを実行し、Aspnet\_して、必要な変更をアセンブリに追加します。 これにより、サーバーは新しいブラウザー情報にすぐにアクセスできるようになり、情報を取得するためにアプリケーションをシャットダウンする必要がなくなります。 アプリケーションは、現在の HttpRequest の Browser プロパティを使用してブラウザー機能にアクセスできます。

次のオプションは、aspnet\_実行するときに使用できます。

| **オプション** | **説明** |
| --- | --- |
| **-?** | コマンドウィンドウに、Aspnet\_regbbrowsers ヘルプテキストを表示します。 |
| **-i** | ランタイムブラウザー機能アセンブリを作成し、グローバルアセンブリキャッシュにインストールします。 |
| **-u** | グローバルアセンブリキャッシュからランタイムブラウザー機能アセンブリをアンインストールします。 |

## <a name="the-aspnet-compilation-tool---aspnet_compilerexe"></a>ASP.NET コンパイルツール-aspnet\_compiler .exe

ASP.NET コンパイルツールは、次の2つの一般的な方法で使用できます。対象の出力ディレクトリが指定されている、配置のためのインプレースコンパイルとコンパイルです。

### <a name="compiling-an-application-in-place"></a>[アプリケーションを適切にコンパイルする](https://msdn.microsoft.com/library/ms229863.aspx)

ASP.NET コンパイルツールは、アプリケーションを適切にコンパイルできます。つまり、アプリケーションに対して複数の要求を行う動作を模倣して、通常のコンパイルを発生させます。 事前にコンパイルされたサイトのユーザーには、最初の要求でページをコンパイルしても遅延が発生しません。

サイトをプリコンパイルする場合は、次の項目が適用されます。

- サイトには、そのファイルとディレクトリ構造が保持されます。
- サーバー上のサイトで使用されるすべてのプログラミング言語用のコンパイラが必要です。
- いずれかのファイルのコンパイルに失敗した場合、サイト全体がコンパイルに失敗します。

新しいソースファイルを追加した後で、アプリケーションを再コンパイルすることもできます。 **-C**オプションを指定しない限り、ツールは、新しいファイルまたは変更されたファイルのみをコンパイルします。

> [!NOTE]
> 入れ子になったアプリケーションを含むアプリケーションをコンパイルしても、入れ子になったアプリケーションはコンパイルされません。 入れ子になったアプリケーションは、個別にコンパイルする必要があります。

### <a name="compiling-an-application-for-deployment"></a>[配置のためのアプリケーションのコンパイル](https://msdn.microsoft.com/library/ms229863.aspx)

TargetDir パラメーターを指定して、配置用のアプリケーション (ターゲットの場所にコンパイル) をコンパイルします。 TargetDir は Web アプリケーションの最終的な場所にすることができます。または、コンパイル済みアプリケーションをさらにデプロイすることもできます。 **-U**オプションを使用すると、コンパイルされたアプリケーション内の特定のファイルを再コンパイルせずに変更できるように、アプリケーションがコンパイルされます。 Aspnet\_は、静的ファイルと動的ファイルの種類を区別し、生成されたアプリケーションを作成するときに異なる方法で処理します。

- 静的ファイルの種類とは、関連付けられたコンパイラやビルドプロバイダーを持たないファイルの種類のことです。たとえば、という名前のファイルには、.css、.gif、.htm、.html、.jpg、.js などの拡張子が付いています。 これらのファイルは単にターゲットの場所にコピーされ、ディレクトリ構造内の相対的な位置が保持されます。
- 動的ファイルの種類とは、コンパイラまたはビルドプロバイダーが関連付けられているファイルの種類です。これには、ASP.NET、.ascx、.ashx、.aspx、browser、.master などのファイル名拡張子が付いたファイルも含まれます。 ASP.NET コンパイルツールは、これらのファイルからアセンブリを生成します。 **-U**オプションを省略した場合、このツールはファイル名拡張子を持つファイルも作成します。元のソースファイルをアセンブリにマップするコンパイル済み。 アプリケーションソースのディレクトリ構造が保持されていることを確認するために、ターゲットアプリケーション内の対応する場所にプレースホルダーファイルが生成されます。

コンパイルされたアプリケーションの内容を変更できることを示すには、 **-u**オプションを使用する必要があります。 それ以外の場合、後続の変更は無視されるか、実行時エラーが発生します。

次の表は、 **-u**オプションが含まれている場合に、ASP.NET コンパイルツールがさまざまなファイルの種類を処理する方法を示しています。

| **ファイルの種類** | **コンパイラアクション** |
| --- | --- |
| .ascx, .aspx, .master | これらのファイルはマークアップとソースコードに分割されます。これには、分離コードファイルと、&lt;スクリプト runat = "server"&gt; 要素で囲まれたすべてのコードが含まれます。 ソースコードは、ハッシュアルゴリズムから派生した名前を持つアセンブリにコンパイルされ、アセンブリは Bin ディレクトリに配置されます。 インラインコード ( **&lt;%** と **%&gt;** 角かっこの間に囲まれたコードは、マークアップに含まれており、コンパイルされません。 ソースファイルと同じ名前の新しいファイルが作成され、マークアップが含まれ、対応する出力ディレクトリに配置されます。 |
| .ashx, .asmx | これらのファイルはコンパイルされず、出力ディレクトリに移動され、コンパイルされません。 ハンドラーコードをコンパイルする場合は、コードをアプリ\_コードディレクトリのソースコードファイルに配置します。 |
| .cs、.vb、jsl、.cpp (前述のファイルの種類の分離コードファイルは含まれません) | これらのファイルはコンパイルされ、それらを参照するアセンブリにリソースとして含まれます。 ソースファイルは出力ディレクトリにコピーされません。 コードファイルが参照されていない場合はコンパイルされません。 |
| カスタムファイルの種類 | これらのファイルはコンパイルされません。 これらのファイルは、対応する出力ディレクトリにコピーされます。 |
| App\_Code サブディレクトリ内のソースコードファイル | これらのファイルはアセンブリにコンパイルされ、Bin ディレクトリに配置されます。 |
| アプリ\_GlobalResources サブディレクトリ内の .resx および .resources ファイル | これらのファイルはアセンブリにコンパイルされ、Bin ディレクトリに配置されます。 メイン出力ディレクトリの下にアプリ\_GlobalResources サブディレクトリが作成されません。ソースディレクトリにある .resx ファイルまたは .resources ファイルは出力ディレクトリにコピーされません。 |
| アプリ\_LocalResources サブディレクトリ内の .resx および .resources ファイル | これらのファイルはコンパイルされず、対応する出力ディレクトリにコピーされます。 |
| App\_theme サブディレクトリの .skin ファイル | .Skin ファイルと静的テーマファイルはコンパイルされず、対応する出力ディレクトリにコピーされます。 |
| . browser Web.config の静的ファイルの種類アセンブリが Bin ディレクトリに既に存在する | これらのファイルは、そのまま出力ディレクトリにコピーされます。 |

次の表では、 **-u**オプションを省略した場合に、ASP.NET コンパイルツールがさまざまなファイルの種類を処理する方法について説明します。

| **ファイルの種類** | **コンパイラアクション** |
| --- | --- |
| .aspx、.asmx、.ashx、.master | これらのファイルはマークアップとソースコードに分割されます。これには、分離コードファイルと、&lt;スクリプト runat = "server"&gt; 要素で囲まれたすべてのコードが含まれます。 ソースコードは、ハッシュアルゴリズムから派生した名前を持つアセンブリにコンパイルされます。 結果として得られるアセンブリは Bin ディレクトリに配置されます。 インラインコード ( **&lt;%** と **%&gt;** 角かっこの間に囲まれたコードは、マークアップに含まれており、コンパイルされません。 コンパイラは、ソースファイルと同じ名前のマークアップを含む新しいファイルを作成します。 これらのファイルは、Bin ディレクトリに配置されます。 また、コンパイラは、ソースファイルと同じ名前で拡張子を持つファイルも作成します。マッピング情報を格納しているコンパイル済み。 、.コンパイル済みのファイルは、ソースファイルの元の場所に対応する出力ディレクトリに配置されます。 |
| .ascx | これらのファイルは、マークアップとソースコードに分割されます。 ソースコードはアセンブリにコンパイルされ、Bin ディレクトリに配置され、ハッシュアルゴリズムから派生した名前が付けられます。 マークアップファイルは生成されません。 |
| .cs、.vb、jsl、.cpp (前述のファイルの種類の分離コードファイルは含まれません) | .Ascx、.ashx、または .aspx ファイルから生成されたアセンブリによって参照されるソースコードは、アセンブリにコンパイルされ、Bin ディレクトリに配置されます。 ソースファイルはコピーされません。 |
| カスタムファイルの種類 | これらのファイルは、動的ファイルと同様にコンパイルされます。 コンパイラは、基になるファイルの種類に応じて、出力ディレクトリにマッピングファイルを配置できます。 |
| App\_Code サブディレクトリ内のファイル | このサブディレクトリ内のソースコードファイルは、アセンブリにコンパイルされ、Bin ディレクトリに配置されます。 |
| アプリ\_GlobalResources サブディレクトリ内のファイル | これらのファイルはアセンブリにコンパイルされ、Bin ディレクトリに配置されます。 メインの出力ディレクトリの下に、アプリ\_GlobalResources サブディレクトリが作成されません。 構成ファイルで appliesTo = "All" を指定した場合、.resx ファイルと .resources ファイルが出力ディレクトリにコピーされます。 これらは、 [Buildprovider](https://msdn.microsoft.com/library/system.web.configuration.buildprovider.aspx)によって参照されている場合はコピーされません。 |
| アプリ\_LocalResources サブディレクトリ内の .resx および .resources ファイル | これらのファイルは、一意の名前を持つアセンブリにコンパイルされ、Bin ディレクトリに配置されます。 .Resx またはリソースファイルは出力ディレクトリにコピーされません。 |
| App\_theme サブディレクトリの .skin ファイル | テーマはアセンブリにコンパイルされ、Bin ディレクトリに配置されます。 スタブファイルは、.skin ファイル用に作成され、対応する出力ディレクトリに配置されます。 静的ファイル (.css など) は、出力ディレクトリにコピーされます。 |
| . browser Web.config の静的ファイルの種類アセンブリが Bin ディレクトリに既に存在する | これらのファイルは、そのまま出力ディレクトリにコピーされます。 |

### <a name="fixed-assembly-names"></a>[固定アセンブリ名](https://msdn.microsoft.com/library/ms229863.aspx##)

MSI Windows インストーラーを使用した Web アプリケーションのデプロイなど、一部のシナリオでは、一貫したファイル名と内容を使用する必要があります。また、アセンブリまたは更新の構成設定を識別するための一貫性のあるディレクトリ構造も必要です。 そのような場合は、 **-fixednames**オプションを使用して、複数のページがアセンブリにコンパイルされるを使用する代わりに、ASP.NET コンパイルツールが各ソースファイルのアセンブリをコンパイルするように指定できます。 これにより、多数のアセンブリが発生する可能性があるため、スケーラビリティに懸念がある場合は、このオプションを慎重に使用する必要があります。

### <a name="strong-name-compilation"></a>[厳密な名前のコンパイル](https://msdn.microsoft.com/library/ms229863.aspx##)

\- **Aptca**、 **-delaysign**、 **-keycontainer** 、 **-** キーの各オプションが用意されています。これにより、Aspnet\_xsd.exe を使用して厳密な名前のアセンブリを作成し、[厳密な名前のツール (sn.exe)](https://msdn.microsoft.com/library/k5b5tt23.aspx)を個別に使用することができます。 これらのオプションは、それぞれ、 **AllowPartiallyTrustedCallersAttribute**、 **assemblydelaysignattribute**、 **assemblydelaysignattribute**、および**AssemblyKeyFileAttribute**に対応しています。

これらの属性については、このコースでは説明しません。

## <a name="labs"></a>ラボ

次の各ラボは、前のラボに基づいています。 これらの操作は順番に実行する必要があります。

## <a name="lab-1-using-the-configuration-api"></a>ラボ 1: 構成 API の使用

1. *Mod9lab*という名前の新しい Web サイトを作成します。
2. 新しい Web 構成ファイルをサイトに追加します。
3. Web.config ファイルに次のを追加します。

[!code-xml[Main](configuration-and-instrumentation/samples/sample14.xml)]

これにより、web.config ファイルへの変更を保存するためのアクセス許可があることが確認されます。

1. Default.aspx に新しい Label コントロールを追加し、ID を**lblDebugStatus**に変更します。
2. Default.aspx に新しいボタンコントロールを追加します。
3. ボタンコントロールの ID を**btnToggleDebug**に変更し、テキストを変更して**デバッグ状態を切り替え**ます。
4. Default.aspx の分離コードファイルのコードビューを開き、次のように、 **system.web**の**using**ステートメントを追加します。

[!code-csharp[Main](configuration-and-instrumentation/samples/sample15.cs)]

1. 次に示すように、クラスに2つのプライベート変数を追加し、ページ\_Init メソッドを追加します。

[!code-csharp[Main](configuration-and-instrumentation/samples/sample16.cs)]

1. ページ\_の読み込みに次のコードを追加します。

[!code-csharp[Main](configuration-and-instrumentation/samples/sample17.cs)]

1. Default.aspx を保存して参照します。 ラベルコントロールに現在のデバッグ状態が表示されることに注意してください。
2. デザイナーの Button コントロールをダブルクリックし、ボタンコントロールの Click イベントに次のコードを追加します。

[!code-csharp[Main](configuration-and-instrumentation/samples/sample18.cs)]

1. Default.aspx を保存して参照し、ボタンをクリックします。
2. 各ボタンをクリックした後に web.config ファイルを開き、[&lt;のコンパイル&gt;] セクションの **[デバッグ]** 属性を確認します。

## <a name="lab-2-logging-application-restarts"></a>ラボ 2: アプリケーションの再起動のログ記録

このラボでは、イベントビューアーでアプリケーションのシャットダウン、スタートアップ、再コンパイルのログ記録を切り替えることができるコードを作成します。

1. DropDownList を default.aspx に追加し、ID を ddlLogAppEvents に変更します。
2. DropDownList の**AutoPostBack**プロパティを**true**に設定します。
3. DropDownList の Items コレクションに3つの項目を追加します。 最初の項目の**テキスト**を*選択*し、値を-1 に設定します。 2番目の項目の**テキスト**と**値**を**True**に、3番目の項目の**テキスト**と**値**を**False**に設定します。
4. Default.aspx に新しいラベルを追加します。 ID を**lblLogAppEvents**に変更します。
5. Default.aspx の分離コードビューを開き、次に示すように、HealthMonitoringSection 型の変数に新しい宣言を追加します。

[!code-csharp[Main](configuration-and-instrumentation/samples/sample19.cs)]

1. ページの既存のコードに次のコードを追加\_Init:

[!code-csharp[Main](configuration-and-instrumentation/samples/sample20.cs)]

1. DropDownList をダブルクリックし、SelectedIndexChanged イベントに次のコードを追加します。

[!code-csharp[Main](configuration-and-instrumentation/samples/sample21.cs)]

1. Default.aspx を参照します。
2. ドロップダウンを **[False]** に設定します。
3. イベントビューアーのアプリケーションログをクリアします。
4. アプリケーションのデバッグ属性を変更するには、このボタンをクリックします。
5. イベントビューアーのアプリケーションログを更新します。 

    1. ログに記録されたイベントはありますか。
    2. なぜでしょうか。
6. ドロップダウンを [True] に設定し**ます。**
7. アプリケーションのデバッグ属性を切り替えるには、このボタンをクリックします。
8. イベントビューアーのアプリケーションログインを更新します。 

    1. ログに記録されたイベントはありますか。
    2. アプリのシャットダウンの理由は何ですか?
9. ログ記録をオンまたはオフにして、web.config ファイルに加えられた変更を確認してみてください。

## <a name="more-information"></a>詳細情報:

ASP.NET 2.0 のプロバイダーモデルを使用すると、アプリケーションのインストルメンテーションだけでなく、他の多くの用途 (メンバーシップ、プロファイルなど) のために独自のプロバイダーを作成することもできます。アプリケーションイベントをテキストファイルに記録するカスタムプロバイダーの作成の詳細については、こちらの[リンク](https://msdn.microsoft.com/library/default.asp?url=/library/dnaspp/html/ASPNETProvMod_Prt6.asp)を参照してください。
