---
uid: web-forms/overview/moving-to-aspnet-20/caching
title: キャッシュ |Microsoft Docs
author: microsoft
description: 適切に実行する ASP.NET アプリケーションでは、キャッシュについて理解しておくことが重要です。 ASP.NET 1.x では、キャッシュ用に3つの異なるオプションが提供されています。出力キャッシュ,...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 2bb109d2-e299-46ea-9054-fa0263b59165
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/caching
msc.type: authoredcontent
ms.openlocfilehash: 4f0b021ca6ca151544dd9fb0587ed9e0cf14ff65
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78464956"
---
# <a name="caching"></a>キャッシュ

[Microsoft](https://github.com/microsoft)

> 適切に実行する ASP.NET アプリケーションでは、キャッシュについて理解しておくことが重要です。 ASP.NET 1.x では、キャッシュ用に3つの異なるオプションが提供されています。出力キャッシュ、フラグメントキャッシュ、およびキャッシュ API。

適切に実行する ASP.NET アプリケーションでは、キャッシュについて理解しておくことが重要です。 ASP.NET 1.x では、キャッシュ用に3つの異なるオプションが提供されています。出力キャッシュ、フラグメントキャッシュ、およびキャッシュ API。 ASP.NET 2.0 では、これら3つの方法をすべて提供していますが、いくつかの重要な機能が追加されています。 新しいキャッシュ依存関係がいくつかあり、開発者はカスタムキャッシュ依存関係も作成できるようになりました。 ASP.NET 2.0 では、キャッシュの構成も大幅に改善されました。

## <a name="new-features"></a>新機能

## <a name="cache-profiles"></a>キャッシュプロファイル

キャッシュプロファイルを使用すると、開発者は個々のページに適用できる特定のキャッシュ設定を定義できます。 たとえば、12時間後にキャッシュから期限切れになるページがある場合は、それらのページに適用できるキャッシュプロファイルを簡単に作成できます。 新しいキャッシュプロファイルを追加するには、構成ファイルの &lt;outputCacheSettings&gt; セクションを使用します。 たとえば、次に示すのは、キャッシュの有効期間を12時間に*設定する、* キャッシュプロファイルの構成です。

[!code-xml[Main](caching/samples/sample1.xml)]

このキャッシュプロファイルを特定のページに適用するには、次に示すように、@ OutputCache ディレクティブの CacheProfile 属性を使用します。

[!code-aspx[Main](caching/samples/sample2.aspx)]

## <a name="custom-cache-dependencies"></a>カスタムキャッシュの依存関係

ASP.NET 1.x 開発者は、カスタムキャッシュの依存関係をかわいくします。 ASP.NET 1.x では、CacheDependency クラスがシールされていたため、開発者は独自のクラスを派生できませんでした。 ASP.NET 2.0 では、この制限はなくなり、開発者は独自のカスタムキャッシュ依存関係を自由に開発できます。 CacheDependency クラスを使用すると、ファイル、ディレクトリ、またはキャッシュキーに基づくカスタムキャッシュ依存関係を作成できます。

たとえば、次のコードは、Web アプリケーションのルートにある、.xml という名前のファイルに基づいて、新しいカスタムキャッシュ依存関係を作成します。

[!code-csharp[Main](caching/samples/sample3.cs)]

このシナリオでは、.xml ファイルが変更されると、キャッシュされた項目は無効になります。

キャッシュキーを使用して、カスタムキャッシュ依存関係を作成することもできます。 この方法を使用すると、キャッシュキーを削除すると、キャッシュされたデータが無効になります。 次の例を使って説明します。

[!code-csharp[Main](caching/samples/sample4.cs)]

上に挿入された項目を無効にするには、キャッシュに挿入された項目を削除してキャッシュキーとして機能させるだけです。

[!code-csharp[Main](caching/samples/sample5.cs)]

キャッシュキーとして機能する項目のキーは、キャッシュキーの配列に追加された値と同じである必要があることに注意してください。

## <a name="polling-based-sql-cache-dependenciesalso-called-table-based-dependencies"></a>ポーリングベースの SQL キャッシュ依存関係 (テーブルベースの依存関係とも呼ばれます)

SQL Server 7 と2000では、SQL キャッシュ依存関係にポーリングベースのモデルを使用します。 ポーリングベースのモデルでは、テーブル内のデータが変更されたときにトリガーされるデータベーステーブルのトリガーを使用します。 このトリガーは、ASP.NET によって定期的にチェックされる通知テーブルの**Changeid**フィールドを更新します。 **Changeid**フィールドが更新されている場合、ASP.NET はデータが変更されたことを認識し、キャッシュされたデータを無効にします。

> [!NOTE]
> SQL Server 2005 ではポーリングベースのモデルも使用できますが、ポーリングベースのモデルは最も効率的なモデルではないため、後で説明するクエリベースのモデルを SQL Server 2005 と共に使用することをお勧めします。

ポーリングベースのモデルを使用して SQL キャッシュの依存関係を正常に動作させるには、テーブルで通知が有効になっている必要があります。 これは、SqlCacheDependencyAdmin クラスを使用するか、または aspnet\_regsql ユーティリティを使用して、プログラムで実行できます。

次のコマンドラインでは、SQL キャッシュ依存関係の*dbase*という名前の SQL Server インスタンスにある Northwind データベースの Products テーブルが登録されます。

[!code-console[Main](caching/samples/sample6.cmd)]

上記のコマンドで使用されるコマンドラインスイッチの説明を次に示します。

| **コマンドラインスイッチ** | **目的** |
| --- | --- |
| -S *server* | サーバー名を指定します。 |
| -ed | データベースで SQL キャッシュの依存関係を有効にする必要があることを指定します。 |
| -d*データベース\_名* | SQL キャッシュの依存関係を有効にするデータベース名を指定します。 |
| -E | Aspnet\_regsql がデータベースへの接続時に Windows 認証を使用するように指定します。 |
| -et | SQL キャッシュ依存のデータベーステーブルを有効にすることを指定します。 |
| -t*テーブル\_名* | SQL キャッシュの依存関係を有効にするデータベーステーブルの名前を指定します。 |

> [!NOTE]
> Aspnet\_には、その他のスイッチを使用できます。 完全な一覧を表示するには、aspnet\_を実行します。 コマンドラインから実行します。

このコマンドを実行すると、SQL Server データベースに対して次の変更が行われます。

- **AspNet\_SqlCacheTablesForChangeNotification**テーブルが追加されます。 このテーブルには、SQL キャッシュ依存関係が有効になっているデータベース内のテーブルごとに1行のデータが格納されます。
- 次のストアドプロシージャは、データベース内に作成されます。

| AspNet\_SqlCachePollingStoredProcedure | AspNet\_SqlCacheTablesForChangeNotification テーブルに対してクエリを行い、SQL キャッシュの依存関係が有効になっているすべてのテーブルと各テーブルの changeId の値を返します。 このストアドプロシージャは、データが変更されたかどうかを確認するためにポーリングに使用されます。 |
| --- | --- |
| AspNet\_SqlCacheQueryRegisteredTablesStoredProcedure | AspNet\_SqlCacheTablesForChangeNotification テーブルに対してクエリを実行し、SQL キャッシュ依存関係が有効になっているすべてのテーブルを返すことによって、SQL キャッシュの依存関係が有効になっているすべてのテーブルを返します。 |
| AspNet\_SqlCacheRegisterTableStoredProcedure | 通知テーブルに必要なエントリを追加し、トリガーを追加することによって、SQL キャッシュ依存関係のテーブルを登録します。 |
| AspNet\_SqlCacheUnRegisterTableStoredProcedure | 通知テーブルのエントリを削除してトリガーを削除することによって、SQL キャッシュ依存関係のテーブルの登録を解除します。 |
| AspNet\_SqlCacheUpdateChangeIdStoredProcedure | 変更されたテーブルの changeId をインクリメントして、通知テーブルを更新します。 ASP.NET は、この値を使用して、データが変更されたかどうかを判断します。 次に示すように、このストアドプロシージャは、テーブルが有効になっているときに作成されたトリガーによって実行されます。 |

- テーブル **_\_Name_\_AspNet\_SqlCacheNotification\_トリガー**と呼ばれる SQL Server トリガーがテーブルに対して作成されます。 このトリガーは、テーブルに対して挿入、更新、または削除が実行されたときに、AspNet\_SqlCacheUpdateChangeIdStoredProcedure を実行します。
- **Aspnet\_ChangeNotification\_ReceiveNotificationsOnlyAccess**という名前の SQL Server のロールがデータベースに追加されます。

**Aspnet\_ChangeNotification\_ReceiveNotificationsOnlyAccess** SQL Server ロールには、Aspnet\_SqlCachePollingStoredProcedure に対する EXEC アクセス許可があります。 ポーリングモデルが正しく機能するためには、プロセスアカウントを aspnet\_ChangeNotification\_ReceiveNotificationsOnlyAccess ロールに追加する必要があります。 Aspnet\_regsql .exe ツールでは、この操作は行われません。

### <a name="configuring-polling-based-sql-cache-dependencies"></a>ポーリングベースの SQL キャッシュ依存関係の構成

ポーリングベースの SQL キャッシュ依存関係を構成するために必要な手順がいくつかあります。 最初の手順では、前述のように、データベースとテーブルを有効にします。 この手順が完了すると、構成の残りの部分は次のようになります。

- ASP.NET 構成ファイルを構成しています。
- SqlCacheDependency の構成

### <a name="configuring-the-aspnet-configuration-file"></a>ASP.NET 構成ファイルの構成

前のモジュールで説明したように、接続文字列を追加するだけでなく、次に示すように、&lt;sqlCacheDependency&gt; 要素を使用して &lt;cache&gt; 要素を構成する必要もあります。

[!code-xml[Main](caching/samples/sample7.xml)]

この構成により、 *pubs*データベースに対する SQL キャッシュの依存関係が有効になります。 &lt;sqlCacheDependency&gt; 要素の pollTime 属性は、既定で6万ミリ秒または1分に設定されていることに注意してください。 (この値を500ミリ秒未満にすることはできません)。この例では &lt;add&gt; 要素は新しいデータベースを追加し、pollTime をオーバーライドして900万ミリ秒に設定します。

#### <a name="configuring-the-sqlcachedependency"></a>SqlCacheDependency の構成

次の手順では、SqlCacheDependency を構成します。 これを実現する最も簡単な方法は、次のように、@ Outcache ディレクティブに SqlDependency 属性の値を指定することです。

[!code-aspx[Main](caching/samples/sample8.aspx)]

上記の @ OutputCache ディレクティブでは、SQL キャッシュの依存関係が*pubs*データベースの*authors*テーブルに対して構成されています。 複数の依存関係を構成するには、次のようにセミコロンで区切ります。

[!code-aspx[Main](caching/samples/sample9.aspx)]

SqlCacheDependency を構成するもう1つの方法は、プログラムでこれを行うことです。 次のコードでは、 *pubs*データベースの*authors*テーブルに新しい SQL キャッシュ依存関係を作成します。

[!code-csharp[Main](caching/samples/sample10.cs)]

プログラムを使用して SQL キャッシュ依存関係を定義する利点の1つは、発生する可能性のある例外を処理できることです。 たとえば、通知が有効になっていないデータベースに対して SQL キャッシュの依存関係を定義しようとすると、 **Databasenotenabledfornotificationexception**例外がスローされます。 このような場合は、 **SqlCacheDependencyAdmin**メソッドを呼び出してデータベース名を渡すことによって、データベースの通知を有効にすることができます。

同様に、通知が有効になっていないテーブルに対して SQL キャッシュの依存関係を定義しようとすると、 **Tablenotenabledfornotificationexception**がスローされます。 その後、 **SqlCacheDependencyAdmin**メソッドを呼び出して、データベース名とテーブル名を渡すことができます。

次のコードサンプルは、SQL キャッシュ依存関係を構成するときに例外処理を適切に構成する方法を示しています。

[!code-csharp[Main](caching/samples/sample11.cs)]

詳細情報: [https://msdn.microsoft.com/library/t9x04ed2.aspx](https://msdn.microsoft.com/library/t9x04ed2.aspx)

## <a name="query-based-sql-cache-dependencies-sql-server-2005-only"></a>クエリベースの SQL キャッシュ依存関係 (SQL Server 2005 のみ)

SQL キャッシュ依存関係に SQL Server 2005 を使用する場合、ポーリングベースのモデルは必要ありません。 SQL Server 2005 で使用する場合、SQL キャッシュの依存関係は SQL Server 2005 クエリ通知を使用して SQL Server インスタンスへの SQL 接続を介して直接通信します (これ以上の構成は必要ありません)。

クエリベースの通知を有効にする最も簡単な方法は、データソースオブジェクトの**SqlCacheDependency**属性を**CommandNotification**に設定し、 **EnableCaching**属性を**true**に設定することによって、宣言によって行うことです。 このメソッドを使用する場合、コードは必要ありません。 データソースに対して実行されたコマンドの結果が変更されると、キャッシュデータが無効になります。

次の例では、SQL キャッシュ依存関係のデータソースコントロールを構成します。

[!code-aspx[Main](caching/samples/sample12.aspx)]

この場合、 **SelectCommand**に指定されたクエリが元の結果とは異なる結果を返す場合、キャッシュされた結果は無効になります。

**@ OutputCache**ディレクティブの**SqlDependency**属性を**CommandNotification**に設定することにより、すべてのデータソースが SQL キャッシュの依存関係に対して有効になるように指定することもできます。 次の例はこれを示しています。

[!code-aspx[Main](caching/samples/sample13.aspx)]

> [!NOTE]
> SQL Server 2005 のクエリ通知の詳細については、SQL Server オンラインブックを参照してください。

クエリベースの SQL キャッシュ依存関係を構成するもう1つの方法は、SqlCacheDependency クラスを使用してプログラムでこれを行うことです。 次のコードサンプルは、この方法を示しています。

[!code-csharp[Main](caching/samples/sample14.cs)]

詳細情報: [https://msdn.microsoft.com/library/default.asp?url=/library/enus/dnvs05/html/querynotification.asp](https://msdn.microsoft.com/library/default.asp?url=/library/enus/dnvs05/html/querynotification.asp)

## <a name="post-cache-substitution"></a>キャッシュ後の置換

ページをキャッシュすることで、Web アプリケーションのパフォーマンスを大幅に向上させることができます。 ただし、場合によっては、ページの大部分がキャッシュされ、ページ内の一部のフラグメントが動的である必要があります。 たとえば、一定期間にわたって完全に静的なニュース記事のページを作成した場合は、ページ全体をキャッシュするように設定できます。 すべてのページ要求で変更された一連の広告バナーを含める場合は、広告を含むページの部分を動的にする必要があります。 ページをキャッシュしながら、一部のコンテンツを動的に置き換えることができるようにするには、ASP.NET のキャッシュ後置換を使用します。 キャッシュ後の置換では、ページ全体がキャッシュから除外対象としてマークされた特定の部分を使用して出力がキャッシュされます。 Ad バナーの例では、AdRotator コントロールを使用して、キャッシュ後の置換を利用し、ユーザーごとに広告を動的に作成し、ページを更新することができます。

キャッシュ後の置換を実装するには、次の3つの方法があります。

- 宣言では、代替コントロールを使用します。
- プログラムでは、代替コントロール API を使用します。
- 暗黙的に、AdRotator コントロールを使用します。

### <a name="substitution-control"></a>Substitution コントロール

ASP.NET Substitution コントロールは、キャッシュではなく動的に作成されるキャッシュされたページのセクションを指定します。 動的なコンテンツを表示するページ上の場所に、代替コントロールを配置します。 実行時には、MethodName プロパティを使用して指定したメソッドが、代替コントロールによって呼び出されます。 メソッドは、置換コントロールの内容を置き換える文字列を返す必要があります。 メソッドは、それを含むページまたは UserControl コントロールの静的メソッドである必要があります。 代替コントロールを使用すると、クライアント側のキャッシュがクライアントにキャッシュされないように、クライアント側のキャッシュがサーバーのキャッシュに変更されます。 これにより、ページへの今後の要求によってメソッドが再度呼び出され、動的なコンテンツが生成されます。

### <a name="substitution-api"></a>Substitution API

キャッシュされたページの動的コンテンツをプログラムによって作成するには、ページコードで[WriteSubstitution](https://msdn.microsoft.com/library/system.web.httpresponse.writesubstitution.aspx)メソッドを呼び出して、メソッドの名前をパラメーターとして渡します。 動的コンテンツの作成を処理するメソッドは、1つの[HttpContext](https://msdn.microsoft.com/library/system.web.httpcontext.aspx)パラメーターを受け取り、文字列を返します。 返される文字列は、指定された場所で置き換えられるコンテンツです。 代替コントロールを宣言に使用するのではなく、WriteSubstitution メソッドを呼び出すと、ページまたは UserControl オブジェクトの静的メソッドを呼び出すのではなく、任意のオブジェクトのメソッドを呼び出すことができるという利点があります。

WriteSubstitution メソッドを呼び出すと、クライアント側のキャッシュがクライアントにキャッシュされないように、クライアント側のキャッシュがサーバーのキャッシュに変更されます。 これにより、ページへの今後の要求によってメソッドが再度呼び出され、動的なコンテンツが生成されます。

### <a name="adrotator-control"></a>AdRotator コントロール

AdRotator サーバーコントロールは、内部でのキャッシュ後の置換のサポートを実装します。 ページに AdRotator コントロールを配置すると、親ページがキャッシュされているかどうかに関係なく、各要求に対して一意の広告が表示されます。 その結果、AdRotator コントロールを含むページは、キャッシュされたサーバー側のみになります。

## <a name="controlcachepolicy-class"></a>ControlCachePolicy クラス

ControlCachePolicy クラスを使用すると、ユーザーコントロールを使用してフラグメントキャッシュをプログラムで制御できます。 ASP.NET は、 [Basepartialcachingcontrol](https://msdn.microsoft.com/library/system.web.ui.basepartialcachingcontrol.aspx)インスタンス内にユーザーコントロールを埋め込みます。 BasePartialCachingControl クラスは、出力キャッシュが有効になっているユーザーコントロールを表します。

[Partialcachingcontrol](https://msdn.microsoft.com/library/system.web.ui.partialcachingcontrol.aspx)コントロールの[CachePolicy](https://msdn.microsoft.com/library/system.web.ui.basepartialcachingcontrol.cachepolicy.aspx)プロパティにアクセスすると、常に有効な ControlCachePolicy オブジェクトが受信されます。 ただし、 [usercontrol](https://msdn.microsoft.com/library/system.web.ui.usercontrol.aspx)コントロールの[CachePolicy](https://msdn.microsoft.com/library/system.web.ui.usercontrol.cachepolicy.aspx)プロパティにアクセスすると、ユーザーコントロールが既に basepartialcachingcontrol コントロールによってラップされている場合にのみ、有効な ControlCachePolicy オブジェクトを受け取ります。 ラップされていない場合、プロパティによって返される ControlCachePolicy オブジェクトは、関連付けられている BasePartialCachingControl がないため、このオブジェクトを操作しようとすると例外をスローします。 UserControl インスタンスが例外を生成せずにキャッシュをサポートするかどうかを判断するには、 [SupportsCaching](https://msdn.microsoft.com/library/system.web.ui.controlcachepolicy.supportscaching.aspx)プロパティを調べます。

ControlCachePolicy クラスの使用は、出力キャッシュを有効にするいくつかの方法の1つです。 次の一覧では、出力キャッシュを有効にするために使用できる方法について説明します。

- [@ OutputCache](https://msdn.microsoft.com/library/hdxfb6cy.aspx)ディレクティブを使用して、宣言型のシナリオで出力キャッシュを有効にします。
- [Partialcachingattribute](https://msdn.microsoft.com/library/system.web.ui.partialcachingattribute.aspx)属性を使用して、分離コードファイル内のユーザーコントロールのキャッシュを有効にします。
- ControlCachePolicy クラスを使用して、プログラムのシナリオでキャッシュ設定を指定します。これは、前のいずれかの方法を使用してキャッシュが有効になっており、 [system.web. UI. loadcontrol](https://msdn.microsoft.com/library/system.web.ui.templatecontrol.loadcontrol.aspx)メソッドを使用して動的に読み込まれた BasePartialCachingControl インスタンスを操作する場合に使用します。

ControlCachePolicy インスタンスを正常に操作できるのは、制御ライフサイクルの Init 段階と PreRender ステージの間だけです。 PreRender フェーズの後に ControlCachePolicy オブジェクトを変更すると、ASP.NET は例外をスローします。これは、コントロールがレンダリングされた後に行われた変更は、実際にはキャッシュ設定には影響しません (レンダリング段階ではコントロールがキャッシュされるためです)。 最後に、ユーザーコントロールインスタンス (およびその ControlCachePolicy オブジェクト) は、実際にレンダリングされるときにプログラム操作にのみ使用できます。

## <a name="changes-to-caching-configuration---the-ltcachinggt-element"></a>キャッシュ構成の変更-&lt;キャッシュ&gt; 要素

ASP.NET 2.0 では、キャッシュ構成にいくつかの変更が加えられています。 &lt;キャッシュ&gt; 要素は ASP.NET 2.0 の新機能であり、構成ファイルでキャッシュ構成の変更を行うことができます。 次の属性を使用できます。

| **Element** | **説明** |
| --- | --- |
| **cache** | 省略可能な要素です。 グローバルアプリケーションキャッシュ設定を定義します。 |
| **outputCache** | 省略可能な要素です。 アプリケーション全体の出力キャッシュ設定を指定します。 |
| **outputCacheSettings** | 省略可能な要素です。 アプリケーションのページに適用できる出力キャッシュ設定を指定します。 |
| **sqlCacheDependency** | 省略可能な要素です。 ASP.NET アプリケーションの SQL キャッシュ依存関係を構成します。 |

### <a name="the-ltcachegt-element"></a>&lt;cache&gt; 要素

&lt;cache&gt; 要素では、次の属性を使用できます。

| **属性** | **説明** |
| --- | --- |
| **disableMemoryCollection** | 省略可能で、 **Boolean** 型の属性。 コンピューターがメモリ不足になったときに発生するキャッシュメモリコレクションが無効になっているかどうかを示す値を取得または設定します。 |
| **disableExpiration 期限** | 省略可能で、 **Boolean** 型の属性。 キャッシュの有効期限が無効かどうかを示す値を取得または設定します。 無効にした場合、キャッシュされた項目は期限切れになりません。また、期限切れのキャッシュ項目のバックグラウンド清掃は行われません。 |
| **privateBytesLimit** | 省略可能な**Int64**属性です。 キャッシュが期限切れの項目のフラッシュを開始し、メモリを再利用できるようになるまでの、アプリケーションのプライベートバイトの最大サイズを示す値を取得または設定します。 この制限には、キャッシュによって使用されるメモリと、実行中のアプリケーションからの通常のメモリオーバーヘッドの両方が含まれます。 0に設定すると、ASP.NET はメモリの解放を開始するタイミングを決定するために独自のヒューリスティックを使用します。 |
| **percentagePhysicalMemoryUsedLimit** | 省略可能な**Int32**属性です。 キャッシュが期限切れの項目のフラッシュを開始し、メモリを再利用する前に、アプリケーションが使用できるコンピューターの物理メモリの最大パーセンテージを示す値を取得または設定します。このメモリ使用量には、キャッシュによって使用されるメモリも含まれます。実行中のアプリケーションの通常のメモリ使用量。 0に設定すると、ASP.NET はメモリの解放を開始するタイミングを決定するために独自のヒューリスティックを使用します。 |
| **privateBytesPollTime** | 省略可能な**TimeSpan**属性です。 アプリケーションのプライベートバイトのメモリ使用量をポーリングする間隔を示す値を取得または設定します。 |

### <a name="the-ltoutputcachegt-element"></a>&lt;outputCache&gt; 要素

&lt;outputCache&gt; 要素では、次の属性を使用できます。

|       <strong>属性</strong>        |                                                                                                                                                                                                                                                       <strong>説明</strong>                                                                                                                                                                                                                                                       |
|-----------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   <strong>enableOutputCache</strong>    |                                                                                                                                                          省略可能で、 <strong>Boolean</strong> 型の属性。 ページ出力キャッシュを有効/無効にします。 無効にした場合、プログラムまたは宣言の設定に関係なく、ページはキャッシュされません。 既定値は "<strong>[はい]</strong>" です。                                                                                                                                                           |
|  <strong>enableFragmentCache</strong>   |                                                省略可能で、 <strong>Boolean</strong> 型の属性。 アプリケーションフラグメントキャッシュを有効または無効にします。 無効にした場合、使用する[@ OutputCache](https://msdn.microsoft.com/library/hdxfb6cy.aspx)ディレクティブまたはキャッシュプロファイルに関係なく、ページはキャッシュされません。 には、アップストリームプロキシサーバーおよびブラウザークライアントがページ出力をキャッシュしないことを示す cache-control ヘッダーが含まれています。 既定値は <strong>false</strong> です。                                                 |
| <strong>sendCacheControlHeader</strong> |                                                                                                                                                      省略可能で、 <strong>Boolean</strong> 型の属性。 既定では、<strong>キャッシュ制御: private</strong>ヘッダーが出力キャッシュモジュールによって送信されるかどうかを示す値を取得または設定します。 既定値は <strong>false</strong> です。                                                                                                                                                      |
|      <strong>Omitvarキルギスタン</strong>      | 省略可能で、 <strong>Boolean</strong> 型の属性。 応答で Http "<strong>Vary: \</strong >" ヘッダーの送信を有効/無効に<em>します。既定の設定である false</em>では、出力キャッシュされたページに "* Vary: \*<strong>" ヘッダーが送信されます。Vary ヘッダーが送信されると、Vary ヘッダーで指定されている内容に基づいて、異なるバージョンをキャッシュできます。たとえば、<em>次のように変更します。ユーザー</em>エージェントは、要求を発行しているユーザーエージェントに基づいて、異なるバージョンのページを格納します。既定値は * * false</strong>です。 |

### <a name="the-ltoutputcachesettingsgt-element"></a>&lt;outputCacheSettings&gt; 要素

&lt;outputCacheSettings&gt; 要素を使用すると、前述のようにキャッシュプロファイルを作成できます。 &lt;outputCacheSettings&gt; 要素の唯一の子要素は、キャッシュプロファイルを構成するための &lt;Outputcachesettings&gt; 要素です。

### <a name="the-ltsqlcachedependencygt-element"></a>&lt;sqlCacheDependency&gt; 要素

&lt;sqlCacheDependency&gt; 要素では、次の属性を使用できます。

| **属性** | **説明** |
| --- | --- |
| **有効** | 必須の**ブール型**の属性です。 変更がポーリングされているかどうかを示します。 |
| **pollTime** | 省略可能な**Int32**属性です。 SqlCacheDependency がデータベーステーブルの変更をポーリングする頻度を設定します。 この値は、連続する pollings 間のミリ秒数に対応します。 500ミリ秒未満に設定することはできません。 既定値は1分です。 |

### <a name="more-information"></a>詳細情報

キャッシュ構成に関して注意する必要がある追加情報がいくつかあります。

- ワーカープロセスのプライベートバイトの制限が設定されていない場合、キャッシュは次のいずれかの制限を使用します。 

    - x86 2GB: 800 MB または物理 RAM の60% のどちらか少ない方
    - x86 GB: 1800MB または物理 RAM の 60% (どちらか少ない方)
    - x64: 物理 RAM の1テラバイトまたは 60% (どちらか少ない方)
- ワーカープロセスのプライベートバイトの制限と &lt;キャッシュの privateBytesLimit/&gt; が設定されている場合、キャッシュはそのうちの最小値を使用します。
- 1\.x の場合と同様に、キャッシュエントリを削除して GC を呼び出します。次の2つの理由から収集します。 

    - プライベートバイトの制限に非常に近い
    - 使用可能なメモリが10% 未満です
- &lt;cache percentagePhysicalMemoryUseLimit/&gt; を100に設定すると、使用可能なメモリが不足している場合に、トリミングとキャッシュを効果的に無効にすることができます。
- 1\.x とは異なり、2.0 はトリムを中断し、最後の GC の場合は呼び出しを収集します。Collect では、プライベートバイトまたはマネージヒープのサイズを (キャッシュ) メモリ制限の1% を超えて減らすことができませんでした。

## <a name="lab1-custom-cache-dependencies"></a>Lab1: カスタムキャッシュの依存関係

1. 新しい Web サイトを作成します。
2. キャッシュ .xml という名前の新しい XML ファイルを追加し、Web アプリケーションのルートに保存します。
3. Default.aspx の分離コードで、次のコードをページ\_Load メソッドに追加します。 

    [!code-csharp[Main](caching/samples/sample15.cs)]
4. ソースビューの default.aspx の先頭に次のコードを追加します。 

    [!code-aspx[Main](caching/samples/sample16.aspx)]
5. Default.aspx を参照します。 このような場合はどうでしょうか。
6. ブラウザーを更新します。 このような場合はどうでしょうか。
7. Cache .xml を開き、次のコードを追加します。 

    [!code-xml[Main](caching/samples/sample17.xml)]
8. キャッシュ .xml を保存します。
9. ブラウザーを最新の状態に更新します。 このような場合はどうでしょうか。
10. 以前にキャッシュされた値を表示するのではなく、時刻が更新された理由を説明します。

## <a name="lab-2-using-polling-based-cache-dependencies"></a>ラボ 2: ポーリングベースのキャッシュ依存関係の使用

このラボでは、前のモジュールで作成したプロジェクトを使用します。これにより、GridView および DetailsView コントロールを使用して Northwind データベースのデータを編集できるようになります。

1. Visual Studio 2005 でプロジェクトを開きます。
2. Northwind データベースに対して aspnet\_regsql ユーティリティを実行して、データベースと Products テーブルを有効にします。 Visual Studio コマンドプロンプトから次のコマンドを実行します。 

    [!code-console[Main](caching/samples/sample18.cmd)]
3. Web.config ファイルに次の内容を追加します。 

    [!code-xml[Main](caching/samples/sample19.xml)]
4. Showdata .aspx という新しい web フォームを追加します。
5. 次の @ outputcache ディレクティブを showdata .aspx ページに追加します。 

    [!code-aspx[Main](caching/samples/sample20.aspx)]
6. 次のコードをページに追加して、showdata .aspx の\_読み込みます。 

    [!code-html[Main](caching/samples/sample21.html)]
7. Showdata .aspx に新しい SqlDataSource コントロールを追加し、Northwind データベース接続を使用するように構成します。 [次へ] をクリックします。
8. ProductName および ProductID のチェックボックスをオンにし、[次へ] をクリックします。
9. [完了] をクリックします。
10. 新しい GridView を showdata .aspx ページに追加します。
11. ドロップダウンリストから [SqlDataSource1] を選択します。
12. Showdata .aspx を保存して参照します。 表示される時刻をメモしておきます。
