---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/distributed-caching
title: 分散キャッシュ (Azure を使用した実際のクラウドアプリの構築) |Microsoft Docs
author: MikeWasson
description: Azure 電子ブックを使用した実際のクラウドアプリの構築は、Scott Guthrie によって開発されたプレゼンテーションに基づいています。 13のパターンとベストプラクティスについて説明します。
ms.author: riande
ms.date: 07/20/2015
ms.assetid: 406518e9-3817-49ce-8b90-e82bc461e2c0
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/distributed-caching
msc.type: authoredcontent
ms.openlocfilehash: 87a7516415895e761d1589fd459b93e5c15c0f85
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78471478"
---
# <a name="distributed-caching-building-real-world-cloud-apps-with-azure"></a>分散キャッシュ (Azure を使用した実際のクラウドアプリの構築)

[Mike Wasson](https://github.com/MikeWasson)、 [Rick Anderson](https://twitter.com/RickAndMSFT)、 [Tom Dykstra](https://github.com/tdykstra)

[修正 It プロジェクトをダウンロード](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)するか[、電子書籍をダウンロード](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)します

> Azure 電子ブック**を使用した実際のクラウドアプリの構築**は、Scott Guthrie によって開発されたプレゼンテーションに基づいています。 ここでは、クラウド用の web アプリの開発を成功させるのに役立つ13のパターンとプラクティスについて説明します。 電子書籍の詳細については、[最初の章](introduction.md)を参照してください。

前の章では、一時的な障害処理と、サーキットブレーカー戦略としてのキャッシュについて説明しました。 この章では、キャッシュの背景について説明します。これには、使用するタイミング、使用するための一般的なパターン、Azure での実装方法などが含まれます。

## <a name="what-is-distributed-caching"></a>分散キャッシュとは

キャッシュは、データをメモリに格納することによって、一般的にアクセスされるアプリケーションデータへの高スループット、待機時間の短いアクセスを提供します。 クラウドアプリの場合、最も役に立つキャッシュの種類は分散キャッシュです。つまり、データは個々の web サーバーのメモリに格納されず、他のクラウドリソースにも格納され、キャッシュされたデータはアプリケーションのすべての web サーバー (またはその他のクラウド Vmアプリケーションによって使用される e)。

![同じキャッシュサーバーにアクセスする複数の web サーバーを示す図](distributed-caching/_static/image1.png)

サーバーを追加または削除することによってアプリケーションの規模を拡大したり、アップグレードや障害によってサーバーを交換したりすると、キャッシュされたデータは、アプリケーションを実行するすべてのサーバーからアクセス可能な状態になります。

永続データストアの待機時間の長いデータアクセスを回避することにより、キャッシュはアプリケーションの応答性を大幅に向上させることができます。 たとえば、データをリレーショナルデータベースから取得するよりも、キャッシュからデータを取得する方がはるかに高速です。

キャッシュを使用すると、永続的なデータストアへのトラフィックが減少します。永続化されたデータストアに対するデータ送信料金が発生すると、コストが削減される可能性があります。

## <a name="when-to-use-distributed-caching"></a>分散キャッシュを使用する場合

キャッシュは、データの書き込みよりも読み取りを行うアプリケーションワークロードや、データをキャッシュに格納および取得するために使用するキー/値の組織がデータモデルでサポートされている場合に最適です。 また、アプリケーションユーザーが多くの一般的なデータを共有する場合にも便利です。たとえば、各ユーザーが通常、そのユーザーに固有のデータを取得する場合、キャッシュには多くの利点がありません。 データが頻繁に変更されず、すべての顧客が同じデータを参照しているために、キャッシュが非常に有益な場合の例として、製品カタログがあります。

キャッシュの利点は、アプリケーションの規模が大きくなるにつれて大きくなります。これは、永続データストアのスループットの制限と待機時間の遅延がアプリケーション全体のパフォーマンスに対する制限を超えるためです。 ただし、パフォーマンス以外の理由でキャッシュを実装することもできます。 ユーザーに表示されるデータが完全に最新である必要がない場合、永続的なデータストアが応答していない場合や使用できない場合に備えて、キャッシュアクセスはサーキットブレーカーとして機能することができます。

## <a name="popular-cache-population-strategies"></a>一般的なキャッシュの作成方法

キャッシュからデータを取得できるようにするには、最初にそのデータを格納する必要があります。 キャッシュに必要なデータを取得するには、次のようないくつかの方法があります。

- オンデマンド/キャッシュを確保する

    アプリケーションは、キャッシュからデータを取得しようとします。キャッシュにデータが含まれていない場合 ("ミス")、アプリケーションはデータをキャッシュに格納して、次のときに使用できるようにします。 アプリケーションが次に同じデータを取得しようとすると、キャッシュ内で探しているものが検出されます ("ヒット")。 データベースで変更されたキャッシュデータがフェッチされないようにするには、データストアに変更を加えるときにキャッシュを無効にします。
- バックグラウンドデータプッシュ

    バックグラウンドサービスは、定期的なスケジュールでデータをキャッシュにプッシュし、アプリは常にキャッシュからプルします。 このアプローチは、常に最新のデータを返すことを必要としない、待機時間の長いデータソースに適しています。
- サーキット ブレーカー

    通常、アプリケーションは永続的なデータストアと直接通信しますが、永続データストアに可用性の問題がある場合、アプリケーションはキャッシュからデータを取得します。 データがキャッシュに格納されているか、バックグラウンドデータプッシュ戦略を使用している可能性があります。 これは、パフォーマンス向上戦略ではなく、エラー処理戦略です。

キャッシュ内のデータを最新の状態に保つために、アプリケーションでデータを作成、更新、または削除するときに、関連するキャッシュエントリを削除できます。 アプリケーションが少し古いデータを取得する可能性がある場合は、構成可能な有効期限に依存して、古いキャッシュデータの制限を設定することができます。

絶対有効期限 (キャッシュ項目が作成されてからの時間) またはスライド式有効期限 (最後にキャッシュ項目がアクセスされてからの経過時間) を構成できます。 絶対有効期限は、データが古くなってしまうのを防ぐためにキャッシュの有効期限メカニズムに依存している場合に使用します。 この問題を修正するには、古いキャッシュ項目を手動で削除し、スライド式有効期限を使用して最新のデータをキャッシュに保持します。 選択した有効期限ポリシーに関係なく、キャッシュのメモリ制限に達したときに、最も古い (最近使用したまたは LRU) 項目がキャッシュによって自動的に削除されます。

## <a name="sample-cache-aside-code-for-fix-it-app"></a>It アプリを修正するためのキャッシュアサイドコードのサンプル

次のサンプルコードでは、修正タスクを取得するときにキャッシュを最初にチェックします。 タスクがキャッシュに見つかった場合は、それを返します。見つからない場合は、データベースから取得し、キャッシュに格納します。 `FindTaskByIdAsync` メソッドにキャッシュを追加するために行った変更が強調表示されます。

[!code-csharp[Main](distributed-caching/samples/sample1.cs?highlight=5,9-11,13-15,19)]

修正するタスクを更新または削除する場合は、キャッシュされたタスクを無効にする (削除する) 必要があります。 そうしないと、今後そのタスクを読み取ろうとすると、キャッシュから古いデータが引き続き取得されます。

[!code-csharp[Main](distributed-caching/samples/sample2.cs?highlight=7)]

これらは、単純なキャッシュコードを示すためのサンプルです。ダウンロード可能な修正プログラムのプロジェクトでキャッシュが実装されていません。

## <a name="azure-caching-services"></a>Azure キャッシュサービス

Azure では、次のキャッシュサービスが提供されています: [Azure Redis Cache](https://msdn.microsoft.com/library/dn690523.aspx)と[azure Managed Cache](https://msdn.microsoft.com/library/dn386094.aspx)。 Azure Redis cache は広く普及している[オープンソースの Redis Cache](http://redis.io/)に基づいており、ほとんどのキャッシュシナリオで最初に選択されています。

<a id="sessionstate"></a>
## <a name="aspnet-session-state-using-a-cache-provider"></a>キャッシュプロバイダーを使用したセッション状態の ASP.NET

[「Web 開発のベストプラクティス](web-development-best-practices.md)」の章で説明したように、セッション状態を使用しないことをお勧めします。 アプリケーションでセッション状態が必要な場合は、次のベストプラクティスとして、既定のメモリ内プロバイダーを使用しないでください。これは、スケールアウト (web サーバーの複数のインスタンス) を有効にしないためです。 ASP.NET SQL Server セッション状態プロバイダーを使用すると、複数の web サーバーで実行されているサイトでセッション状態を使用できますが、メモリ内プロバイダーと比較して待機時間が長くなります。 セッション状態を使用する必要がある場合は、 [Azure cache のセッション状態プロバイダー](https://msdn.microsoft.com/library/windowsazure/gg185668.aspx)などのキャッシュプロバイダーを使用することをお勧めします。

## <a name="summary"></a>まとめ

応答時間とスケーラビリティを向上させ、データベースが使用できなくなったときにアプリが読み取り操作に応答し続けることができるようにするために、It アプリの修正によってキャッシュを実装する方法について説明しました。 次の[章](queue-centric-work-pattern.md)では、スケーラビリティをさらに向上させ、アプリが書き込み操作に応答し続けるようにする方法について説明します。

## <a name="resources"></a>リソース

キャッシュの詳細については、次のリソースを参照してください。

ドキュメント

- [Azure キャッシュ](https://msdn.microsoft.com/library/gg278356.aspx)。 Azure でのキャッシュに関する公式の MSDN ドキュメント。
- [Microsoft のパターンとプラクティス-Azure のガイダンス](https://msdn.microsoft.com/library/dn568099.aspx)。 キャッシュのガイダンスとキャッシュアサイドパターンを参照してください。
- [フェイルセーフ: 回復力のあるクラウドアーキテクチャに関するガイダンス](https://msdn.microsoft.com/library/windowsazure/jj853352.aspx)。 ホワイトペーパー (Marc Mercuri、Ulrich Homann、Andrew Townhill)。 キャッシュに関するセクションを参照してください。
- [Azure Cloud Services で大規模なサービスを設計するためのベストプラクティス](https://msdn.microsoft.com/library/windowsazure/jj717232.aspx)。 西 マーク Simm と Michael Thomassy によるホワイトペーパー。 分散キャッシュに関するセクションを参照してください。
- [スケーラビリティへのパスでの分散キャッシュ](https://msdn.microsoft.com/magazine/dd942840.aspx)。 古い (2009) MSDN マガジンの記事ですが、一般的には、分散キャッシュの概要について説明しています。フェールセーフとベストプラクティスに関するホワイトペーパーのキャッシュに関するセクションよりも詳細に説明します。

ビデオ

- [フェイルセーフ: スケーラブルで回復力のある Cloud Services を構築](https://channel9.msdn.com/Series/FailSafe)します。 Ulrich Homann、Marc Mercuri、Mark Simm による9パートシリーズ。 クラウドアプリを設計する方法の400レベルのビューについて説明します。 このシリーズでは、理論と理由を中心に説明します。詳細については、「Simm」を参照してください。 1:24:14 以降のエピソード3でのキャッシュの説明を参照してください。
- [大規模な構築: Azure のお客様から学んだ教訓-パート I](https://channel9.msdn.com/Events/Build/2012/3-029)。Simon Davies は、46:00 以降の分散キャッシュについて説明します。 フェイルセーフシリーズに似ていますが、さらに詳細な方法について説明します。 プレゼンテーションには2012年10月31日が指定されているため、2013で導入された Azure App Service の Web Apps のキャッシュサービスについては説明しません。

コード サンプル

- [Azure のクラウドサービスの基礎](https://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649)。 分散キャッシュを実装するサンプルアプリケーション。 付随するブログ投稿「[クラウドサービスの基礎–キャッシュの基礎](https://blogs.msdn.com/b/windowsazure/archive/2013/10/03/cloud-service-fundamentals-caching-basics.aspx)」を参照してください。

> [!div class="step-by-step"]
> [前へ](transient-fault-handling.md)
> [次へ](queue-centric-work-pattern.md)
