---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/the-fix-it-sample-application
title: '付録: Fix It サンプルアプリケーション (Azure を使用した実際のクラウドアプリの構築) |Microsoft Docs'
author: MikeWasson
description: Azure 電子ブックを使用した実際のクラウドアプリの構築は、Scott Guthrie によって開発されたプレゼンテーションに基づいています。 13のパターンとベストプラクティスについて説明します。
ms.author: riande
ms.date: 06/12/2014
ms.assetid: 1bc333c5-f096-4ea7-b170-779accc21c1a
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/the-fix-it-sample-application
msc.type: authoredcontent
ms.openlocfilehash: 896196bdb6a6b0d12a6c798ead510e37dd38a9fc
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2020
ms.locfileid: "77456882"
---
# <a name="appendix-the-fix-it-sample-application-building-real-world-cloud-apps-with-azure"></a>付録: Fix It サンプルアプリケーション (Azure を使用した実際のクラウドアプリの構築)

[Mike Wasson](https://github.com/MikeWasson)、 [Rick Anderson](https://twitter.com/RickAndMSFT)、 [Tom Dykstra](https://github.com/tdykstra)

[修正プログラムのプロジェクトをダウンロードする](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)

> Azure 電子ブック**を使用した実際のクラウドアプリの構築**は、Scott Guthrie によって開発されたプレゼンテーションに基づいています。 ここでは、クラウド用の web アプリの開発を成功させるのに役立つ13のパターンとプラクティスについて説明します。 電子書籍の詳細については、[最初の章](introduction.md)を参照してください。

この付録では、Azure 電子ブックを使用した実際のクラウドアプリの構築について説明します。次のセクションでは、ダウンロード可能な修正プログラムサンプルアプリケーションに関する追加情報を提供しています。

- [既知の問題](#knownissues)
- [ベスト プラクティス](#bestpractices)
- [ローカルコンピューター上の Visual Studio からアプリを実行する方法](#run-in-vs)
- [Windows PowerShell スクリプトを使用して Azure App Service Web Apps に基本アプリを展開する方法](#deploybase)
- [Windows PowerShell スクリプトのトラブルシューティング](#troubleshooting)
- [キュー処理を使用してアプリを Azure App Service Web Apps と Azure クラウドサービスにデプロイする方法](#deployqueues)

<a id="knownissues"></a>
## <a name="known-issues"></a>既知の問題

この電子書籍に記載されているパターンのいくつかをできるだけ簡単に説明するために、It アプリを修正しました。 ただし、電子書籍は実際のアプリの作成に関するものであるため、リリースされたソフトウェアの場合と同様に、レビューおよびテストのプロセスに対してコードの修正を実施しました。 いくつかの問題が見つかりました。実際のアプリケーションと同様に、いくつかの問題が修正され、その一部は今後のリリースに延期されました。

次の一覧には、実稼働アプリケーションで対処する必要がある問題が含まれていますが、1つの理由として、Fix It サンプルアプリケーションの最初のリリースでは対応していないと判断しました。

### <a name="security"></a>セキュリティ

- 存在しない所有者にタスクを割り当てることができないようにしてください。
- 作成したタスク、または自分に割り当てられたタスクだけを表示および変更できることを確認します。
- サインインページと認証 cookie には HTTPS を使用します。
- 認証 cookie の制限時間を指定します。

### <a name="input-validation"></a>入力の検証

一般に、運用アプリでは、It アプリの修正よりも多くの入力検証が行われます。 たとえば、アップロードに許可されているイメージサイズ/イメージファイルのサイズは制限する必要があります。

### <a name="administrator-functionality"></a>管理者の機能

管理者は、既存のタスクの所有権を変更できなければなりません。 たとえば、タスクの作成者が会社を退職した場合、管理アクセスが有効になっていない限り、タスクを維持する権限はありません。

### <a name="queue-message-processing"></a>キューメッセージの処理

Fix It アプリでのキューメッセージ処理は、最小限のコードでキュー中心の作業パターンを示すために単純なものとして設計されました。 この単純なコードは、実際の運用アプリケーションには適していません。

- このコードでは、各キューメッセージが1回だけ処理されることは保証されません。 キューからメッセージを取得すると、タイムアウト期間が発生します。その間、メッセージは他のキューリスナーに対して非表示になります。 メッセージが削除される前にタイムアウトが経過すると、メッセージが再び表示されるようになります。 このため、worker ロールインスタンスがメッセージの処理に長い時間がかかる場合は、同じメッセージが2回処理される可能性があり、その結果、データベースに重複するタスクが発生します。 この問題の詳細については、「 [Azure Storage キューの使用](https://msdn.microsoft.com/library/ff803365.aspx#sec7)」を参照してください。
- キューのポーリングロジックは、メッセージの取得をバッチ処理することにより、コスト効率に優れています。 [GetMessageAsync](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.getmessageasync.aspx)を呼び出すたびに、トランザクションコストが発生します。 代わりに、 [Cloudqueue. Getmessages async](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.getmessagesasync.aspx) (複数形の ') を呼び出すことができます。この場合、1つのトランザクションで複数のメッセージが取得されます。 Azure Storage キューのトランザクションコストが非常に低いため、ほとんどのシナリオではコストへの影響は大きくありません。
- キューメッセージ処理コードの短いループにより、CPU アフィニティが発生します。この場合、マルチコア Vm は効率的に使用されません。 より優れた設計では、タスクの並列化を使用して複数の非同期タスクを並列に実行します。
- キューメッセージの処理には、基本的な例外処理しかありません。 たとえば、コードは[有害なメッセージ](https://msdn.microsoft.com/library/ms789028.aspx)を処理しません。 (メッセージ処理によって例外が発生した場合は、エラーを記録してメッセージを削除する必要があります。そうしないと、ワーカーロールはその処理を再試行し、ループは無期限に続行されます)。

### <a name="sql-queries-are-unbounded"></a>SQL クエリはバインドされていません

現在の修正このコードでは、インデックスページのクエリが返す行の数に制限はありません。 大量のタスクがデータベースに入力されると、受信したリストのサイズによってパフォーマンスの問題が発生する可能性があります。 この解決策は、ページングを実装することです。 例については、「 [ASP.NET MVC アプリケーションでの Entity Framework の並べ替え、フィルター処理、およびページング](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md)」を参照してください。

### <a name="view-models-recommended"></a>推奨されるモデルの表示

Fix It アプリは、FixItTask エンティティクラスを使用して、コントローラーとビューの間で情報を渡します。 ビューモデルを使用することをお勧めします。 ドメインモデル (FixItTask エンティティクラスなど) は、データの永続化に必要なものを中心に設計されていますが、ビューモデルはデータ表示用に設計できます。 詳細については、「 [12 ASP.NET MVC のベストプラクティス](https://codeclimber.net.nz/archive/2009/10/27/12-asp.net-mvc-best-practices.aspx)」を参照してください。

### <a name="secure-image-blob-recommended"></a>保護されたイメージ blob を推奨

Fix It アプリは、アップロードされたイメージをパブリックとして保存します。つまり、URL を見つけたすべてのユーザーがイメージにアクセスできます。 イメージは、パブリックではなく、セキュリティで保護されている可能性があります。

### <a name="no-powershell-automation-scripts-for-queues"></a>キュー用の PowerShell オートメーションスクリプトがありません

サンプル PowerShell の自動化スクリプトは、Azure App Service Web Apps で完全に実行される、修正プログラムの基本バージョンに対してのみ作成されました。 キューの処理に必要な web アプリとクラウドサービス環境を設定してデプロイするためのスクリプトは提供されていません。

### <a name="special-handling-for-html-codes-in-user-input"></a>ユーザー入力における HTML コードの特別な処理

ASP.NET を使用すると、ユーザー入力テキストボックスにスクリプトを入力することで、悪意のあるユーザーがクロスサイトスクリプト攻撃を試みる可能性が自動的に回避されます。 また、タスクタイトルとメモを表示するために使用される MVC `DisplayFor` ヘルパーは、ブラウザーに送信する値を自動的に HTML エンコードします。 しかし、運用アプリでは、追加の手段を取る必要がある場合があります。 詳細については、「 [ASP.NET での要求の検証](https://msdn.microsoft.com/library/hh882339.aspx)」を参照してください。

<a id="bestpractices"></a>
## <a name="best-practices"></a>ベスト プラクティス

次に示すのは、修正後の It アプリの元のバージョンのコードレビューとテストで解決された問題です。 元のプログラマが特定のベストプラクティスを認識していないことが原因として考えられるのは、コードが迅速に記述され、リリースされたソフトウェアを意図していなかったためです。 ここでは、web アプリを開発している他のユーザーにとって役に立つ可能性がある、このレビューとテストから学んだことがある問題について説明しています。

### <a name="dispose-the-database-repository"></a>データベースリポジトリを破棄します。

`FixItTaskRepository` クラスは、Entity Framework `DbContext` インスタンスを破棄する必要があります。 これを行うには、`FixItTaskRepository` クラスに `IDisposable` を実装します。

[!code-csharp[Main](the-fix-it-sample-application/samples/sample1.cs)]

AutoFac によって `FixItTaskRepository` インスタンスが自動的に破棄されるので、明示的に破棄する必要がないことに注意してください。

もう1つのオプションは、`FixItTaskRepository`から `DbContext` メンバー変数を削除し、`using` ステートメント内で各リポジトリメソッド内にローカル `DbContext` 変数を作成することです。 例 :

[!code-csharp[Main](the-fix-it-sample-application/samples/sample2.cs)]

### <a name="register-singletons-as-such-with-di"></a>DI を使用してシングルトンを登録する

`PhotoService` クラスと `Logger` クラスのインスタンスは1つだけ必要であるため、これらのクラスは*DependenciesConfig.cs*での[依存関係の挿入のために1つのインスタンスとして登録](https://code.google.com/p/autofac/wiki/InstanceScope)する必要があります。

[!code-csharp[Main](the-fix-it-sample-application/samples/sample3.cs?highlight=1,3)]

### <a name="security-dont-show-error-details-to-users"></a>セキュリティ: エラーの詳細をユーザーに表示しない

元の Fix It アプリには一般的なエラーページがありません。すべての例外が UI にバブルアップされるだけなので、データベース接続エラーなどの例外によっては、完全なスタックトレースがブラウザーに表示される可能性があります。 エラーの詳細情報は、悪意のあるユーザーによる攻撃を促進することがあります。 この問題を解決するには、例外の詳細をログに記録し、エラーの詳細が含まれていないエラーページをユーザーに表示します。 Fix It アプリは既にログ記録されており、エラーページを表示するために、web.config ファイルに `<customErrors mode=On>` を追加しました。

[!code-xml[Main](the-fix-it-sample-application/samples/sample4.xml?highlight=2)]

既定では、これにより、エラーの*Views\Shared\Error.cshtml*が表示されます。 *エラー*をカスタマイズすることも、独自のエラーページビューを作成して、`defaultRedirect` 属性を追加することもできます。 また、特定のエラーに対して別のエラーページを指定することもできます。

### <a name="security-only-allow-a-task-to-be-edited-by-its-creator"></a>セキュリティ: タスクの作成者だけが編集できるようにする

ダッシュボードのインデックスページには、ログオンしているユーザーによって作成されたタスクのみが表示されますが、悪意のあるユーザーが、別のユーザーのタスクに ID を持つ URL を作成する可能性があります。 この場合、404を返すコードを*DashboardController.cs*に追加しました。

[!code-csharp[Main](the-fix-it-sample-application/samples/sample5.cs?highlight=9-14,24-29)]

### <a name="dont-swallow-exceptions"></a>例外を飲み込むしない

元の Fix It アプリでは、SQL クエリの結果として発生した例外をログに記録した後、次のように null が返されました。

[!code-csharp[Main](the-fix-it-sample-application/samples/sample6.cs?highlight=4)]

これにより、クエリが成功したとしても、行が返されなかったかのようにユーザーに表示されるようになります。 解決策は、キャッチしてログを記録した後に例外を再スローすることです。

[!code-csharp[Main](the-fix-it-sample-application/samples/sample7.cs)]

### <a name="catch-all-exceptions-in-worker-roles"></a>Worker ロールのすべての例外をキャッチする

ワーカーロールでハンドルされない例外が発生すると、VM がリサイクルされます。そのため、try-catch ブロックで実行するすべての処理をラップし、すべての例外を処理する必要があります。

### <a name="specify-length-for-string-properties-in-entity-classes"></a>エンティティクラスの文字列プロパティの長さを指定する

単純なコードを表示するために、Fix It アプリの元のバージョンは、FixItTask エンティティのフィールドの長さを指定していませんでした。その結果、データベースで varchar (max) として定義されました。 その結果、UI はほぼすべての入力を受け入れます。 長さを指定すると、web ページのユーザー入力とデータベースの列サイズの両方に適用される制限が設定されます。

[!code-csharp[Main](the-fix-it-sample-application/samples/sample8.cs?highlight=4,7,10,12,14)]

### <a name="mark-private-members-as-readonly-when-they-arent-expected-to-change"></a>プライベートメンバーが変更されることが予想されない場合は、プライベートメンバーを読み取り専用としてマークする

たとえば、`DashboardController` クラスでは `FixItTaskRepository` のインスタンスが作成され、変更されることは想定されていないため、 [readonly](https://msdn.microsoft.com/library/acdd6hb7.aspx)として定義しました。

[!code-csharp[Main](the-fix-it-sample-application/samples/sample9.cs?highlight=3)]

### <a name="use-listany-instead-of-listcount-gt-0"></a>リストを使用します。List ではなく任意の ()。Count () &gt; 0

リスト内の1つ以上の項目が指定した条件に適合するかどうかを確認するだけの場合は、[[任意](https://msdn.microsoft.com/library/bb534972.aspx)のメソッド] を使用します。これは、条件を満たす項目が見つかった場合はすぐに制御が戻るのに対し、`Count` メソッドは常にすべての項目を反復処理する必要があるためです。 ダッシュボードの*インデックスの cshtml*ファイルには、最初に次のコードが含まれていました。

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample10.cshtml)]

次のように変更しました。

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample11.cshtml?highlight=1)]

### <a name="generate-urls-in-mvc-views-using-mvc-helpers"></a>Mvc ヘルパーを使用した MVC ビューでの Url の生成

ホームページの [Fix It] \ (**修正プログラムの作成**\) ボタンをクリックすると、it アプリの修正によってアンカー要素がハードコーディングされます。

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample12.cshtml)]

このようなビュー/アクションリンクについては、次の例のように、 [Url. action](https://msdn.microsoft.com/library/system.web.mvc.urlhelper.action.aspx) HTML helper を使用することをお勧めします。

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample13.cshtml)]

### <a name="use-taskdelay-instead-of-threadsleep-in-worker-role"></a>ワーカーロールでは、Thread ではなく Delay を使用します

新しいプロジェクトのテンプレートでは、ワーカーロールのサンプルコードに `Thread.Sleep` が配置されますが、スレッドがスリープ状態になると、スレッドプールによって余分な不要なスレッドが生成される可能性があります。 これを回避するには、代わりに[Delay](https://msdn.microsoft.com/library/hh139096.aspx)を使用します。

[!code-csharp[Main](the-fix-it-sample-application/samples/sample14.cs?highlight=11)]

### <a name="avoid-async-void"></a>非同期 void を回避する

非同期メソッドが値を返す必要がない場合は、`void`ではなく `Task` の型を返します。

この例は、`FixItQueueManager` クラスからのものです。

[!code-csharp[Main](the-fix-it-sample-application/samples/sample15.cs)]

`async void` は、最上位レベルのイベントハンドラーに対してのみ使用してください。 メソッドを `async void`として定義した場合、呼び出し元はメソッドを**待機**したり、メソッドがスローする例外をキャッチしたりすることはできません。 詳細については、「[非同期プログラミングのベストプラクティス](https://msdn.microsoft.com/magazine/jj991977.aspx)」を参照してください。

### <a name="use-a-cancellation-token-to-break-from-worker-role-loop"></a>キャンセルトークンを使用してワーカーロールループを中断する

通常、ワーカーロールの**Run**メソッドには、無限ループが含まれています。 ワーカーロールが停止している場合は、 [Roleentrypoint. OnStop](https://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstop.aspx)メソッドが呼び出されます。 このメソッドを使用して、Run メソッド内で**実行**されている作業を取り消し、正常に終了する必要があります。 それ以外の場合、プロセスは操作の途中で終了します。

### <a name="opt-out-of-automatic-mime-sniffing-procedure"></a>自動 MIME スニッフィング手順のオプトアウト

場合によっては、Internet Explorer によって、web サーバーで指定された種類とは異なる MIME の種類が報告されることがあります。 たとえば、Internet Explorer が HTTP 応答ヘッダーの Content-type: text/plain と共に配信されたファイル内の HTML コンテンツを検索した場合、Internet Explorer はコンテンツを HTML としてレンダリングする必要があると判断します。 残念ながら、この "MIME スニッフィング" は、信頼されていないコンテンツをホストしているサーバーのセキュリティの問題につながる可能性もあります。 この問題に対処するために、Internet Explorer 8 は、MIME の種類の決定コードに多くの変更を加え、アプリケーション開発者が[mime スニッフィングをオプトアウト](https://blogs.msdn.com/b/ie/archive/2008/07/02/ie8-security-part-v-comprehensive-protection.aspx)することを許可しています。 次*のコードが web.config ファイルに*追加されました。

[!code-xml[Main](the-fix-it-sample-application/samples/sample16.xml?highlight=2-7)]

### <a name="enable-bundling-and-minification"></a>バンドルと縮小を有効にする

Visual Studio で新しい web プロジェクトを作成する場合、JavaScript ファイルのバンドルと縮小は既定では有効になっていません。 BundleConfig.cs にコード行を追加しました。

[!code-csharp[Main](the-fix-it-sample-application/samples/sample17.cs?highlight=9)]

### <a name="set-an-expiration-time-out-for-authentication-cookies"></a>認証 cookie の有効期限のタイムアウトを設定する

既定では、認証 cookie は2週間後に期限切れになります。 より短い時間でより安全です。 *StartupAuth.cs*でこの設定を変更できます。

[!code-csharp[Main](the-fix-it-sample-application/samples/sample18.cs?highlight=4-5)]

<a id="run-in-vs"></a>
## <a name="how-to-run-the-app-from-visual-studio-on-your-local-computer"></a>ローカルコンピューター上の Visual Studio からアプリを実行する方法

Fix It アプリを実行するには、次の2つの方法があります。

- 新しいタスクを SQL データベースに直接書き込む基本アプリケーションを実行します。
- キューとバックエンドサービスを使用してアプリケーションを実行し、タスクを作成します。 キューパターンについては、[キュー中心の作業パターン](queue-centric-work-pattern.md)の章を参照してください。

<a id="runbase"></a>
### <a name="run-the-base-application"></a>基本アプリケーションを実行する

1. [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) のインストール。
2. [AZURE SDK for .net For Visual Studio](https://azure.microsoft.com/downloads/)をインストールします。
3. [MSDN コードギャラリー](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)から .zip ファイルをダウンロードします。
4. ファイルエクスプローラーで、.zip ファイルを右クリックし、[プロパティ] をクリックして、プロパティウィンドウ [ブロック解除] をクリックします。
5. ファイルを解凍します。
6. .Sln ファイルをダブルクリックして、Visual Studio を起動します。
7. **[ツール]** メニューの **[NuGet パッケージマネージャー]** 、 **[パッケージマネージャーコンソール]** の順にクリックします。
8. パッケージマネージャーコンソール (PMC) で、[復元] をクリックします。
9. Visual Studio を終了します。
10. [Azure ストレージエミュレーター](/azure/storage/common/storage-use-emulator)を起動します。
11. Visual Studio を再起動し、前の手順で閉じたソリューションファイルを開きます。
12. FixIt プロジェクトがスタートアッププロジェクトとして設定されていることを確認してから、CTRL キーを押しながら F5 キーを押してプロジェクトを実行します。

<a id="queueslocal"></a>
### <a name="run-the-application-with-queue-processing"></a>キュー処理でアプリケーションを実行する

1. 指示に従って[基本アプリケーションを実行](#runbase)し、ブラウザーを閉じて Visual Studio を閉じます。
2. 管理者特権で Visual Studio を起動します。 (Azure コンピューティングエミュレーターを使用し、管理者特権が必要です)。
3. *Myfixit*プロジェクト (web プロジェクト) のアプリケーションの*web.config*ファイルで、`appSettings/UseQueues` の値を "true" に変更します。

    [!code-console[Main](the-fix-it-sample-application/samples/sample19.cmd?highlight=3)]
4. [Azure ストレージエミュレーター](https://msdn.microsoft.com/library/windowsazure/hh403989.aspx)がまだ実行されていない場合は、もう一度開始します。
5. FixIt web プロジェクトと MyFixItCloudService プロジェクトを同時に実行します。

    Visual Studio の使用:

   1. **F5**キーを押して、FixIt プロジェクトを実行します。
   2. **ソリューションエクスプローラー**で、MyFixItCloudService プロジェクトを右クリックし、 **[デバッグ]**  >  **[新しいインスタンスを開始]** の順にクリックします。

    Visual Studio 2013 Express for Web の使用:

   3. ソリューションエクスプローラーで、FixIt ソリューションを右クリックし、**プロパティ** を選択します。
   4. **[マルチスタートアッププロジェクト]** を選択します。
   5. MyFixIt と MyFixItCloudService の下の **アクション** ドロップダウンリストで、**開始** を選択します。
   6. **[OK]** をクリックすると、
   7. **F5** キーを押して両方のプロジェクトを実行します。

      MyFixItCloudService プロジェクトを実行すると、Visual Studio によって Azure コンピューティングエミュレーターが起動されます。 ファイアウォールの構成によっては、エミュレーターをファイアウォールで許可することが必要になる場合があります。

<a id="deploybase"></a>
## <a name="how-to-deploy-the-base-app-to-azure-app-service-web-apps-by-using-the-windows-powershell-scripts"></a>Windows PowerShell スクリプトを使用して Azure App Service Web Apps に基本アプリを展開する方法

[すべてを自動化](automate-everything.md)するためのパターンを説明するために、Azure で環境を設定し、新しい環境にプロジェクトを配置するスクリプトを使用して、It アプリの修正を提供しています。 次の手順では、スクリプトの使用方法について説明します。

キューを使用せずに Azure で実行し、変更をキューでローカルに実行する場合は、次の手順に進む前に、UseQueues appSetting 値を false に戻すように設定してください。

この手順では、修正プログラムをダウンロードしてローカルで実行していること、および Azure アカウントを持っていること、または管理を許可されている Azure サブスクリプションを持っていることを前提としています。

1. **Azure PowerShell**コンソールをインストールします。 手順については、「 [Azure PowerShell のインストールおよび構成方法](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-4.3.1)」を参照してください。

    このカスタマイズされたコンソールは、Azure サブスクリプションと連携するように構成されています。 Azure モジュールは*Program Files*ディレクトリにインストールされ、Azure PowerShell コンソールを使用するたびに自動的にインポートされます。

    Windows PowerShell ISE など別のホストプログラムで作業する場合は、モジュールの[インポート](https://go.microsoft.com/fwlink/?LinkID=141553)コマンドレットを使用して azure モジュールをインポートするか、azure モジュールのコマンドを使用してモジュールの自動インポートをトリガーするようにしてください。
2. **[管理者として実行]** オプションを使用して Azure PowerShell を開始します。
3. [Set-executionpolicy](https://go.microsoft.com/fwlink/p/?linkid=293941)コマンドレットを実行して、Azure PowerShell 実行ポリシーを `RemoteSigned`に設定します。 ポリシーの変更を完了するには、「 **Y** 」 (はいの場合) を入力します。

    [!code-console[Main](the-fix-it-sample-application/samples/sample20.cmd)]

    この設定を使用すると、デジタル署名されていないローカルスクリプトを実行できます。 (実行ポリシーを `Unrestricted`に設定することもできます。これにより、後でブロック解除の手順が不要になりますが、セキュリティ上の理由から推奨されません。)
4. `Add-AzureAccount` コマンドレットを実行して、アカウントの資格情報を使用して PowerShell を設定します。

    [!code-console[Main](the-fix-it-sample-application/samples/sample21.cmd)]

    これらの資格情報は、一定の期間が経過すると期限切れになり、`Add-AzureAccount` コマンドレットを再実行する必要があります。 この電子ブックが記述されているため、資格情報の有効期限が切れるまでの制限時間は12時間です。
5. 複数のサブスクリプションがある場合は、AzureSubscription コマンドレットを使用して、テスト環境を作成するサブスクリプションを指定します。
6. `Get-AzurePublishSettingsFile` と `Import-AzurePublishSettingsFile` のコマンドレットを使用して、同じ Azure サブスクリプションの管理証明書をインポートします。 最初のコマンドレットでは、証明書ファイルをダウンロードし、2つ目のコマンドレットで、インポートするファイルの場所を指定します。 > [!IMPORTANT]
   > ダウンロードしたファイルは、Azure サービスの管理に使用できる証明書が含まれているため、安全な場所に保管するか、または作業を終えたときに削除してください。

    [!code-console[Main](the-fix-it-sample-application/samples/sample22.cmd)]

    この証明書は、SQL Database サーバーでファイアウォール規則を設定するために、開発用コンピューターの IP アドレスを検出する REST API 呼び出しに使用されます。
7. [Set Location](https://go.microsoft.com/fwlink/p/?linkid=293912)コマンドレット (エイリアスは `cd`、`chdir`、および `sl`) を実行して、スクリプトが格納されているディレクトリに移動します。 (これらのファイルは、[Fix It solution] フォルダーの [ *Automation* ] フォルダーにあります)。ディレクトリ名にスペースが含まれている場合は、パスを引用符で囲みます。 たとえば、`c:\Sample Apps\FixIt\Automation` ディレクトリに移動するには、次のコマンドを入力します。

    [!code-console[Main](the-fix-it-sample-application/samples/sample23.cmd)]
8. Windows PowerShell でこれらのスクリプトを実行できるようにするには、[ファイルのブロック解除](https://go.microsoft.com/fwlink/p/?linkid=294021)コマンドレットを使用します。 (スクリプトはインターネットからダウンロードされたためブロックされます)。

    > [!WARNING]
    > セキュリティ-任意のスクリプトまたは実行可能ファイルに対して `Unblock-File` を実行する前に、メモ帳でファイルを開き、コマンドを調べて、悪意のあるコードが含まれていないことを確認します。

    たとえば、次のコマンドは、現在のディレクトリ内のすべてのスクリプトに対して `Unblock-File` コマンドレットを実行します。

    [!code-console[Main](the-fix-it-sample-application/samples/sample24.cmd)]
9. ベース (キューを処理しない) の web アプリを作成し、It アプリを修正するには、環境作成スクリプトを実行します。

    必須の `Name` パラメーターはデータベースの名前を指定し、スクリプトが作成するストレージアカウントにも使用されます。 名前は、azurewebsites.net ドメイン内でグローバルに一意である必要があります。 Fixit やテストなどの一意でない名前を指定した場合 (または、fixitdemo の例でも同様)、`New-AzureWebsite` コマンドレットは、競合を報告する内部エラーで失敗します。 このスクリプトは、web アプリ、ストレージアカウント、およびデータベースの名前の要件に準拠するために、名前をすべて小文字に変換します。

    必須の `SqlDatabasePassword` パラメーターは、SQL Database 用に作成される管理者アカウントのパスワードを指定します。 パスワード (&amp; &lt; &gt;;) には特殊な XML 文字を含めないでください。 これは、Azure の制限ではなく、スクリプトの記述方法に関する制限事項です。

    たとえば、"fixitdemo" という名前の web アプリを作成し、"Passw0rd1" という SQL Server 管理者パスワードを使用する場合は、次のコマンドを入力します。

    [!code-console[Main](the-fix-it-sample-application/samples/sample25.cmd)]

    名前は azurewebsites.net ドメイン内で一意である必要があり、パスワードは、パスワードの複雑さの SQL Database 要件を満たしている必要があります。 (例 Passw0rd1 は要件を満たしています)。

    コマンドの先頭が "であることに注意してください。\"。 スクリプトの悪意のある実行を防ぐために、Windows PowerShell では、スクリプトの実行時にスクリプトファイルへの完全修飾パスを指定する必要があります。 ドットを使用して、現在のディレクトリ (") を示すことができます。\") または完全修飾パスを指定します。次に例を示します。

    [!code-console[Main](the-fix-it-sample-application/samples/sample26.cmd)]

    スクリプトの詳細については、`Get-Help` コマンドレットを使用してください。

    [!code-console[Main](the-fix-it-sample-application/samples/sample27.cmd)]

    Get-help コマンドレットの `Detailed`、`Full`、`Parameters`、および `Examples` パラメーターを使用して、返されるヘルプをフィルター処理できます。

    スクリプトが失敗した場合、またはエラーが発生した場合 ("New-AzureWebsite: Call Set-Azurewebsite and Select-Azurewebsite first" など)、Azure PowerShell の構成が完了していない可能性があります。

    スクリプトが完了したら、[[すべて自動化](automate-everything.md)] の章に示されているように、Azure 管理ポータルを使用して、作成されたリソースを確認できます。
10. 新しい Azure 環境に FixIt プロジェクトをデプロイするには、 *Azurewebsite. ps1*スクリプトを使用します。 例 :

    [!code-console[Main](the-fix-it-sample-application/samples/sample28.cmd)]

    デプロイが完了すると、Azure で実行されている修正プログラムを使用してブラウザーが開きます。

<a id="troubleshooting"></a>
## <a name="troubleshooting-the-windows-powershell-scripts"></a>Windows PowerShell スクリプトのトラブルシューティング

これらのスクリプトを実行するときに発生する最も一般的なエラーは、権限に関連しています。 `Add-AzureAccount` と `Import-AzurePublishSettingsFile` が正常に完了し、同じ Azure サブスクリプションで使用されていることを確認します。 `Add-AzureAccount` が成功した場合でも、再実行する必要がある場合があります。 `Add-AzureAccount` によって追加されたアクセス許可は、12時間後に有効期限が切れます。

### <a name="object-reference-not-set-to-an-instance-of-an-object"></a>オブジェクト参照がオブジェクト インスタンスに設定されていません。

スクリプトから "オブジェクト参照がオブジェクトのインスタンスに設定されていません" などのエラーが返された場合は、Windows PowerShell が処理するオブジェクトを見つけられない (これは null 参照例外である) ため、`Add-AzureAccount` コマンドレットを実行して、スクリプトをもう一度実行します。

[!code-console[Main](the-fix-it-sample-application/samples/sample29.cmd)]

### <a name="internalerror-the-server-encountered-an-internal-error"></a>InternalError: サーバーで内部エラーが発生しました。

`New-AzureWebsite` コマンドレットは、名前が azurewebsites.net ドメイン内で一意でない場合に内部エラーを返します。 このエラーを解決するには、名前に別の値を使用します。これは、 *New-AzureWebsiteEnv*の name パラメーターに含まれています。

[!code-console[Main](the-fix-it-sample-application/samples/sample30.cmd)]

### <a name="restarting-the-script"></a>スクリプトを再起動しています

"スクリプトが完了しました" というメッセージが出力される前に失敗したために*New-AzureWebsiteEnv*スクリプトを再起動する必要がある場合は、スクリプトが停止する前に作成したリソースを削除することをお勧めします。 たとえば、スクリプトによって ContosoFixItDemo web アプリが既に作成されていて、同じ名前でスクリプトを再度実行した場合、その名前は使用中であるため、スクリプトは失敗します。

スクリプトが作成されたリソースを停止する前に確認するには、次のコマンドレットを使用します。

- `Get-AzureWebsite`
- `Get-AzureSqlDatabaseServer`
- `Get-AzureSqlDatabase`: このコマンドレットを実行するには、データベースサーバー名をパイプで `Get-AzureSqlDatabase`: `Get-AzureSqlDatabaseServer | Get-AzureSqlDatabase.`

これらのリソースを削除するには、次のコマンドを使用します。 データベースサーバーを削除すると、サーバーに関連付けられているデータベースが自動的に削除されることに注意してください。

- `Get-AzureWebsite -Name <WebsiteName> | Remove-AzureWebsite`
- `Get-AzureSqlDatabase -Name <DatabaseName> -ServerName <DatabaseServerName> | Remove-SqlAzureDatabase`
- `Get-AzureSqlDatabaseServer | Remove-AzureSqlDatabaseServer`

<a id="deployqueues"></a>
## <a name="how-to-deploy-the-app-with-queue-processing-to-azure-app-service-web-apps-and-an-azure-cloud-service"></a>キュー処理を使用してアプリを Azure App Service Web Apps と Azure クラウドサービスにデプロイする方法

キューを有効にするには、myfixitconfiguration ファイルで次の変更を行います。 `appSettings`で、`UseQueues` の値を "true" に変更します。

[!code-xml[Main](the-fix-it-sample-application/samples/sample31.xml)]

次に、[前述](#deploybase)のように AZURE APP SERVICE で MVC アプリケーションを web アプリにデプロイします。

次に、新しい Azure クラウドサービスを作成します。 Fix It アプリに含まれているスクリプトは、クラウドサービスを作成またはデプロイしません。そのため、このために Azure portal を使用する必要があります。 ポータルで、 **[新規]**  -- [ **Compute** – **Cloud Service** -- **簡易作成**] の順にクリックし、URL とデータセンターの場所を入力します。 Web アプリをデプロイしたのと同じデータセンターを使用します。

![](the-fix-it-sample-application/_static/image1.png)

クラウドサービスをデプロイする前に、構成ファイルの一部を更新する必要があります。

MyFixIt の `connectionStrings`の下で、`appdb` 接続文字列の値を、SQL Database の実際の接続文字列に変更します。 ポータルから接続文字列を取得できます。 ポータルで、 **[SQL データベース]** をクリックして - **APPDB** - **ADO .net、ODBC、PHP、JDBC の接続文字列を表示 SQL Database**ます。 ADO.NET 接続文字列をコピーし、app.config ファイルに値を貼り付けます。 "{Your\_password\_here}" をデータベースのパスワードに置き換えます。 (MVC アプリのデプロイにスクリプトを使用したと仮定した場合は、`SqlDatabasePassword` スクリプトパラメーターにデータベースパスワードを指定しています)。

結果は次のようになります。

[!code-xml[Main](the-fix-it-sample-application/samples/sample32.xml)]

同じ MyFixIt ファイルで、[`appSettings`] の下にある Azure ストレージアカウントの2つのプレースホルダーの値を置き換えます。

[!code-xml[Main](the-fix-it-sample-application/samples/sample33.xml?highlight=2-3)]

ポータルからアクセスキーを取得できます。 「[ストレージアカウントの管理方法」を](https://docs.microsoft.com/azure/storage/common/storage-create-storage-account)参照してください。

MyFixItCloudService\ServiceConfiguration.Cloud.cscfg で、Azure ストレージアカウントの2つのプレースホルダーの値を置き換えます。

[!code-xml[Main](the-fix-it-sample-application/samples/sample34.xml?highlight=3)]

これで、クラウドサービスをデプロイする準備が整いました。 ソリューションエクスプローラーで、MyFixItCloudService プロジェクトを右クリックし、 **[発行]** を選択します。 詳細については、[このチュートリアル](https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36)のパート2の「[Azure へのアプリケーションのデプロイ](https://www.windowsazure.com/develop/net/tutorials/multi-tier-web-site/2-download-and-run/#deployAz)」を参照してください。

> [!div class="step-by-step"]
> [[戻る]](more-patterns-and-guidance.md)
