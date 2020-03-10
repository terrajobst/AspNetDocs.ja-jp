---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices
title: Web 開発のベストプラクティス (Azure を使用した実際のクラウドアプリの構築) |Microsoft Docs
author: MikeWasson
description: Azure 電子ブックを使用した実際のクラウドアプリの構築は、Scott Guthrie によって開発されたプレゼンテーションに基づいています。 13のパターンとベストプラクティスについて説明します。
ms.author: riande
ms.date: 06/12/2014
ms.assetid: 52d6c941-2cd9-442f-9872-2c798d6d90cd
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices
msc.type: authoredcontent
ms.openlocfilehash: dfd8a3ac2328d3f17dfbe36e68b37d181177b0f4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78471406"
---
# <a name="web-development-best-practices-building-real-world-cloud-apps-with-azure"></a>Web 開発のベストプラクティス (Azure を使用した実際のクラウドアプリの構築)

[Mike Wasson](https://github.com/MikeWasson)、 [Rick Anderson](https://twitter.com/RickAndMSFT)、 [Tom Dykstra](https://github.com/tdykstra)

[修正 It プロジェクトをダウンロード](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)するか[、電子書籍をダウンロード](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)します

> Azure 電子ブック**を使用した実際のクラウドアプリの構築**は、Scott Guthrie によって開発されたプレゼンテーションに基づいています。 ここでは、クラウド用の web アプリの開発を成功させるのに役立つ13のパターンとプラクティスについて説明します。 電子書籍の詳細については、[最初の章](introduction.md)を参照してください。

最初の3つのパターンは、アジャイル開発プロセスの設定に関するものです。残りの部分は、アーキテクチャとコードに関するものです。 この1つは、web 開発のベストプラクティスのコレクションです。

- スマートロードバランサーの背後にある[ステートレスな web サーバー](#stateless) 。
- [セッション状態を回避](#sessionstate)する (または、これを回避できない場合は、データベースではなく分散キャッシュを使用します)。
- [CDN を使用](#cdn)して、静的ファイルアセット (イメージ、スクリプト) をエッジキャッシュします。
- [.Net 4.5 の非同期サポートを使用](#async)して、ブロック呼び出しを回避します。

これらのプラクティスは、クラウドアプリだけでなく、すべての web 開発に対して有効ですが、クラウドアプリでは特に重要です。 クラウド環境で提供される非常に柔軟なスケーリングを最適に使用できるように、連携して機能します。 これらのプラクティスに従っていない場合は、アプリケーションを拡張しようとすると制限が発生します。

<a id="stateless"></a>
## <a name="stateless-web-tier-behind-a-smart-load-balancer"></a>スマートロードバランサーの背後にあるステートレス web 層

*ステートレス web 層*は、web サーバーのメモリまたはファイルシステムにアプリケーションデータを格納しないことを意味します。 Web 層のステートレスを維持すると、カスタマーエクスペリエンスを向上させ、コストを節約することができます。

- Web 層がステートレスで、ロードバランサーの背後に配置されている場合は、サーバーを動的に追加または削除することによって、アプリケーショントラフィックの変化に迅速に対応できます。 実際に使用している限り、サーバーリソースに対してのみ課金されるクラウド環境では、需要の変化に対応することにより、大幅な節約につながる可能性があります。
- ステートレス web 層は、アプリケーションをスケールアウトするために、アーキテクチャがはるかに簡単です。 これにより、スケーリングのニーズに迅速に対応し、プロセスでの開発とテストにかかるコストを削減できます。
- クラウドサーバーは、オンプレミスサーバーと同様に、修正プログラムを適用して再起動する必要があります。また、web 層がステートレスである場合は、サーバーが一時的にダウンしたときにトラフィックを再ルーティングしても、エラーや予期しない動作が発生することはありません。

ほとんどの実際のアプリケーションでは、web セッションの状態を格納する必要があります。ここでの主なポイントは、web サーバーに格納することではありません。 状態は、他の方法で保存できます。たとえば、cookie のクライアントや、キャッシュプロバイダーを使用した ASP.NET セッション状態でのアウトプロセスサーバー側の状態を格納できます。 ファイルは、ローカルファイルシステムではなく、 [Windows Azure Blob ストレージ](unstructured-blob-storage.md)に格納できます。

Web 層がステートレスである場合に、Windows Azure Web サイトでアプリケーションを簡単に拡張できる例として、管理ポータルで Windows Azure Web サイトの **[スケール]** タブを参照してください。

![[スケール] タブ](web-development-best-practices/_static/image1.png)

Web サーバーを追加する場合は、[インスタンス数] スライダーを右にドラッグするだけでかまいません。 5に設定し、 **[保存]** をクリックします。また、web サイトのトラフィックを処理する Windows Azure の web サーバーが数秒以内に表示されます。

![5つのインスタンス](web-development-best-practices/_static/image2.png)

インスタンス数を簡単に3または1に戻すことができます。 Windows Azure の料金は時間単位ではなく分単位で課金されるため、スケールバックするときには、すぐにコストの節約を開始します。

また、CPU 使用率に基づいて web サーバーの数を自動的に増減するように Windows Azure に指示することもできます。 次の例では、CPU 使用率が60% を下回ると、web サーバーの数が最小値2に減少し、CPU 使用率が80% を超えた場合、web サーバーの数が最大4まで増加します。

![CPU 使用率によるスケーリング](web-development-best-practices/_static/image3.png)

または、作業時間中にサイトがビジー状態であることがわかっている場合はどうすればよいでしょうか。 夜間に複数のサーバーを実行するように Windows Azure に指示し、1台のサーバー夜、夜、週末まで減らすことができます。 次の一連のスクリーンショットでは、午前8時から午後5時までの間に、1台のサーバーを1台のサーバーで実行するように web サイトを設定する方法を示しています。

![スケジュールによるスケール](web-development-best-practices/_static/image4.png)

![スケジュール時刻の設定](web-development-best-practices/_static/image5.png)

![日中のスケジュール](web-development-best-practices/_static/image6.png)

![Weeknight スケジュール](web-development-best-practices/_static/image7.png)

![週末のスケジュール](web-development-best-practices/_static/image8.png)

もちろん、これらはすべて、スクリプトやポータルでも実行できます。

Windows Azure では、アプリケーションのスケールアウトの機能はほぼ無制限です。サーバー Vm を動的に追加または削除する障害を回避するには、web 層をステートレスにします。

<a id="sessionstate"></a>
## <a name="avoid-session-state"></a>セッション状態を回避する

ユーザー セッションの状態をなんらかの形で格納しないのは、実際のクラウド アプリケーションでは実用的でない場合が多いですが、方法によっては、パフォーマンスとスケーラビリティに与える影響が大きくなります。 状態を格納する必要がある場合は、状態の量を少なくし、Cookie に格納することをお勧めします。 そうでない場合は、次の最良の解決策は、ASP.NET セッション状態を、[分散型メモリ内キャッシュ](distributed-caching.md#sessionstate)のプロバイダーと共に使用することです。 パフォーマンスとスケーラビリティの観点から最もお勧めできないのが、データベースを利用したセッション状態プロバイダーを使用する方法です。

<a id="cdn"></a>
## <a name="use-a-cdn-to-cache-static-file-assets"></a>CDN を使用して静的ファイルアセットをキャッシュする

CDN は Content Delivery Network の頭字語です。 イメージやスクリプトファイルなどの静的なファイルアセットを CDN プロバイダーに提供すると、プロバイダーは世界中のデータセンターにこれらのファイルをキャッシュします。これにより、ユーザーがアプリケーションにアクセスするときに、比較的迅速な応答が得られ、キャッシュされた待機時間が短くなります。資産. これにより、サイトの全体的な読み込み時間が短縮され、web サーバーの負荷が軽減されます。 CDNs は、地理的に広く分散しているユーザーに到達する場合に特に重要です。

Windows Azure には CDN があり、Windows Azure または任意の web ホスティング環境で実行されるアプリケーションで他の CDNs を使用できます。

<a id="async"></a>
## <a name="use-net-45s-async-support-to-avoid-blocking-calls"></a>.NET 4.5 の非同期サポートを使用してブロック呼び出しを回避する

.NET 4.5 ではC# 、タスクを非同期に処理しやすくするために、と VB のプログラミング言語が強化されています。 非同期プログラミングの利点は、複数の web サービス呼び出しを同時に開始する必要がある場合などの並列処理の場合だけではありません。 また、高負荷条件下では、web サーバーがより効率的かつ信頼性の高い方法で動作できるようになります。 Web サーバーで使用できるスレッドの数は限られています。また、すべてのスレッドが使用されている場合、受信要求はスレッドが解放されるまで待機する必要があります。 アプリケーションコードがデータベースクエリや web サービス呼び出しなどのタスクを非同期に処理しない場合、サーバーが i/o 応答を待機している間、多くのスレッドが不必要に関連付けられます。 これにより、高負荷状態でサーバーが処理できるトラフィックの量が制限されます。 非同期プログラミングでは、web サービスまたはデータベースがデータを返すのを待機しているスレッドは、のデータが受信されるまで、新しい要求を処理するために解放されます。 ビジー状態の web サーバーでは、数百または数千の要求をすぐに処理できます。その場合、スレッドが解放されるのを待機します。

既に説明したように、web サイトを処理する web サーバーの数を減らすことは簡単にできます。 そのため、サーバーでスループットを向上させることができる場合、必要な数だけではなく、必要なトラフィック量に応じてサーバーを減らすことができるため、コストを削減できます。

.NET 4.5 の非同期プログラミングモデルのサポートは、Web フォーム、MVC、Web API の ASP.NET 4.5 に含まれています。Entity Framework 6、 [Windows AZURE STORAGE API](https://blogs.msdn.com/b/windowsazurestorage/archive/2013/07/12/introducing-storage-client-library-2-1-rc-for-net-and-windows-phone-8.aspx)で。

### <a name="async-support-in-aspnet-45"></a>ASP.NET 4.5 での非同期サポート

ASP.NET 4.5 では、非同期プログラミングのサポートは言語だけでなく、MVC、Web フォーム、Web API フレームワークにも追加されています。 たとえば、ASP.NET MVC コントローラーのアクションメソッドは、web 要求からデータを受け取り、そのデータをビューに渡します。これにより、ブラウザーに送信される HTML が作成されます。 多くの場合、アクションメソッドは、web ページにデータを表示したり、web ページに入力されたデータを保存したりするために、データベースや web サービスからデータを取得する必要があります。 このようなシナリオでは、 *actionresult*オブジェクトを返す代わりに、actionresult オブジェクトを返すのではなく、*タスク&lt;actionresult&gt;* を返して、 *async*キーワードを使用してメソッドをマークすることができます。 メソッド内で、待機時間が関係する操作をコード行が開始するときに、await キーワードを使用してマークします。

データベースクエリのリポジトリメソッドを呼び出す簡単なアクションメソッドを次に示します。

[!code-csharp[Main](web-development-best-practices/samples/sample1.cs)]

ここでは、データベース呼び出しを非同期に処理するのと同じ方法を示します。

[!code-csharp[Main](web-development-best-practices/samples/sample2.cs?highlight=1,4)]

内部では、コンパイラが適切な非同期コードを生成します。 アプリケーションが `FindTaskByIdAsync`の呼び出しを行うと、ASP.NET は `FindTask` 要求を行い、ワーカースレッドをアンワインドして、別の要求を処理できるようにします。 `FindTask` 要求が完了すると、その呼び出しの後に来るコードの処理を続行するためにスレッドが再起動されます。 `FindTask` 要求が開始されてからデータが返されるまでの間に、有効な作業を実行するために使用できるスレッドがあります。これは、応答を待機している間に関連付けられます。

非同期コードにはいくつかのオーバーヘッドがありますが、負荷が低い条件下では、負荷の高い条件下では、使用可能なスレッドを待機している間は待機している要求を処理することができます。

ASP.NET 1.1 以降、このような非同期プログラミングを行うことができましたが、記述が難しく、エラーが発生しやすく、デバッグが困難でした。 ASP.NET 4.5 でのコーディングを簡略化したので、これを行わない理由はありません。

### <a name="async-support-in-entity-framework-6"></a>Entity Framework 6 での非同期サポート

4\.5 での非同期サポートの一部として、web サービス呼び出し、ソケット、およびファイルシステム i/o に対する非同期サポートが提供されましたが、web アプリケーションの最も一般的なパターンはデータベースをヒットさせることであり、データライブラリは非同期をサポートしていませんでした。 Entity Framework 6 では、データベースアクセスの非同期サポートが追加されました。

Entity Framework 6 では、クエリまたはコマンドをデータベースに送信するすべてのメソッドに非同期バージョンがあります。 次の例は、 *Find*メソッドの非同期バージョンを示しています。

[!code-csharp[Main](web-development-best-practices/samples/sample3.cs?highlight=8)]

この非同期サポートは、挿入、削除、更新、単純な検出だけでなく、LINQ クエリでも機能します。

[!code-csharp[Main](web-development-best-practices/samples/sample4.cs?highlight=7,10)]

このコードでは、クエリをデータベースに送信するメソッドであるため、`ToList` メソッドの `Async` バージョンがあります。 `Where` メソッドと `OrderByDescending` メソッドはクエリのみを構成し、`ToListAsync` メソッドはクエリを実行し、応答を `result` 変数に格納します。

## <a name="summary"></a>まとめ

ここに記載されている web 開発のベストプラクティスは、任意の web プログラミングフレームワークと任意のクラウド環境に実装できますが、ASP.NET と Windows Azure には簡単にするためのツールが用意されています。 これらのパターンに従うと、web 層を簡単にスケールアウトできます。また、各サーバーはより多くのトラフィックを処理できるため、コストを最小限に抑えることができます。

[次の章](single-sign-on.md)では、クラウドでのシングルサインオンシナリオを有効にする方法について説明します。

## <a name="resources"></a>リソース

詳細については、次のリソースを参照してください。

ステートレス web サーバー:

- [Microsoft のパターンとプラクティス-自動スケールのガイダンス](https://msdn.microsoft.com/library/dn589774.aspx)。
- [Windows Azure Web サイトで ARR のインスタンスアフィニティを無効に](https://azure.microsoft.com/blog/2013/11/18/disabling-arrs-instance-affinity-in-windows-azure-web-sites/)しています。 「Erez Benari によるブログ投稿」では、Windows Azure Web サイトのセッションアフィニティについて説明しています。

CDN

- [フェイルセーフ: スケーラブルで回復力のある Cloud Services を構築](https://channel9.msdn.com/Series/FailSafe)します。 Ulrich Homann、Marc Mercuri、Mark Simm による9部構成のビデオシリーズ。 1:34:00 以降のエピソード3の CDN に関する説明を参照してください。
- [Microsoft のパターンとプラクティスの静的コンテンツホスティングパターン](https://msdn.microsoft.com/library/dn589776.aspx)
- [CDN レビュー](http://www.cdnreviews.com/)。 多くの CDNs の概要。

非同期プログラミング:

- [ASP.NET MVC 4 での非同期メソッドの使用](../../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md)。 Rick Anderson のチュートリアル。
- [Async および Await を使用したC#非同期プログラミング (および Visual Basic)](https://msdn.microsoft.com/library/vstudio/hh191443.aspx)。 非同期プログラミングの原理、ASP.NET 4.5 での動作、および実装するコードの記述方法について説明した MSDN ホワイトペーパーです。
- [Entity Framework の非同期クエリと保存](https://msdn.microsoft.com/data/jj819165)
- [Async を使用して ASP.NET Web アプリケーションを構築する方法](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2013/DEV-B337#fbid=tgkT4SR_DK7)。 Rowan 明美によるビデオプレゼンテーション。 高負荷の状態で web サーバーのスループットを大幅に向上させるための非同期プログラミングのしくみを示します。
- [フェイルセーフ: スケーラブルで回復力のある Cloud Services を構築](https://channel9.msdn.com/Series/FailSafe)します。 Ulrich Homann、Marc Mercuri、Mark Simm による9部構成のビデオシリーズ。 非同期プログラミングがスケーラビリティに与える影響については、エピソード4とエピソード8を参照してください。
- [ASP.NET 4.5 で非同期メソッドを使用するマジックと、重要な注意事項が](http://www.hanselman.com/blog/TheMagicOfUsingAsynchronousMethodsInASPNET45PlusAnImportantGotcha.aspx)あります。 Scott マン Selman によるブログ投稿、主に ASP.NET Web フォームアプリケーションでの async の使用について説明します。

その他の web 開発のベストプラクティスについては、次のリソースを参照してください。

- [修正プログラムのサンプルは、アプリケーションのベストプラクティス](the-fix-it-sample-application.md#bestpractices)です。 この電子書籍の付録には、「It アプリケーションの修正」で実装されたいくつかのベストプラクティスが記載されています。
- [Web 開発者チェックリスト](http://webdevchecklist.com/asp.net)

> [!div class="step-by-step"]
> [前へ](continuous-integration-and-continuous-delivery.md)
> [次へ](single-sign-on.md)
