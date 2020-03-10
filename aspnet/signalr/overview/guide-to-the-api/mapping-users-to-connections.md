---
uid: signalr/overview/guide-to-the-api/mapping-users-to-connections
title: SignalR ユーザーの接続へのマッピング |Microsoft Docs
author: bradygaster
description: このトピックでは、ユーザーとその接続に関する情報を保持する方法について説明します。 パトリック Fletcher はこのトピックの執筆に役立っています。 このトピックで使用されているソフトウェアのバージョン...
ms.author: bradyg
ms.date: 12/30/2014
ms.assetid: f80c08b1-3f1f-432c-980c-c7b6edeb31b1
msc.legacyurl: /signalr/overview/guide-to-the-api/mapping-users-to-connections
msc.type: authoredcontent
ms.openlocfilehash: d55d40848e1e9d40570850c3552b225235c5e814
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78431392"
---
# <a name="mapping-signalr-users-to-connections"></a>SignalR ユーザーを接続にマッピングする

[Tom FitzMacken](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> このトピックでは、ユーザーとその接続に関する情報を保持する方法について説明します。
>
> パトリック Fletcher はこのトピックの執筆に役立っています。
>
> ## <a name="software-versions-used-in-this-topic"></a>このトピックで使用されているソフトウェアのバージョン
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - .NET 4.5
> - SignalR バージョン2
>
>
>
> ## <a name="previous-versions-of-this-topic"></a>このトピックの前のバージョン
>
> 以前のバージョンの SignalR の詳細については、「[古いバージョンの SignalR](../older-versions/index.md)」を参照してください。
>
> ## <a name="questions-and-comments"></a>質問とコメント
>
> このチュートリアルの良い点に関するフィードバックや、ページ下部にあるコメントで改善できる点をお知らせください。 チュートリアルに直接関係のない質問がある場合は、 [ASP.NET SignalR フォーラム](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)または[StackOverflow.com](http://stackoverflow.com/)に投稿できます。

## <a name="introduction"></a>はじめに

ハブに接続する各クライアントは、一意の接続 id を渡します。この値は、ハブコンテキストの `Context.ConnectionId` プロパティで取得できます。 アプリケーションでユーザーを接続 id にマップし、そのマッピングを保持する必要がある場合は、次のいずれかを使用できます。

- [ユーザー ID プロバイダー (SignalR 2)](#IUserIdProvider)
- [メモリ内ストレージ](#inmemory)(ディクショナリなど)
- [各ユーザーの SignalR グループ](#groups)
- [永続的な外部ストレージ](#database)(データベーステーブルや Azure table storage など)

このトピックでは、これらの各実装について説明します。 `Hub` クラスの `OnConnected`、`OnDisconnected`、および `OnReconnected` の各メソッドを使用して、ユーザー接続の状態を追跡します。

アプリケーションに最適な方法は、次のとおりです。

- アプリケーションをホストしている web サーバーの数。
- 現在接続しているユーザーの一覧を取得する必要があるかどうか。
- アプリケーションまたはサーバーの再起動時に、グループとユーザーの情報を保持する必要があるかどうか。
- 外部サーバーの呼び出しの待機時間が問題になるかどうか。

次の表は、これらの考慮事項に対して機能する方法を示しています。

|  | 複数のサーバー | 現在接続しているユーザーの一覧を取得します。 | 再起動後に情報を保持する | 最適なパフォーマンス |
| --- | --- | --- | --- | --- |
| UserID プロバイダー | ![](mapping-users-to-connections/_static/image1.png) |  |  | ![](mapping-users-to-connections/_static/image2.png) |
| メモリ内 |  | ![](mapping-users-to-connections/_static/image3.png) |  | ![](mapping-users-to-connections/_static/image4.png) |
| シングルユーザーグループ | ![](mapping-users-to-connections/_static/image5.png) |  |  | ![](mapping-users-to-connections/_static/image6.png) |
| パーマネント、外部 | ![](mapping-users-to-connections/_static/image7.png) | ![](mapping-users-to-connections/_static/image8.png) | ![](mapping-users-to-connections/_static/image9.png) |  |

<a id="IUserIdProvider"></a>

## <a name="iuserid-provider"></a>IUserID プロバイダー

この機能を使用すると、ユーザーは新しいインターフェイス IUserIdProvider を使用して、IRequest に基づいてユーザー Id を指定できます。

**IUserIdProvider**

[!code-csharp[Main](mapping-users-to-connections/samples/sample1.cs)]

既定では、ユーザーの `IPrincipal.Identity.Name` をユーザー名として使用する実装が存在します。 これを変更するには、アプリケーションの起動時に、`IUserIdProvider` の実装をグローバルホストに登録します。

[!code-csharp[Main](mapping-users-to-connections/samples/sample2.cs)]

ハブ内から、次の API を使用して、これらのユーザーにメッセージを送信できるようになります。

**特定のユーザーへのメッセージの送信**

[!code-csharp[Main](mapping-users-to-connections/samples/sample3.cs?highlight=5)]

<a id="inmemory"></a>

## <a name="in-memory-storage"></a>インメモリストレージ

次の例は、メモリに格納されているディクショナリに接続情報とユーザー情報を保持する方法を示しています。 ディクショナリは、`HashSet` を使用して接続 id を格納します。ユーザーは、いつでも SignalR アプリケーションに対して複数の接続を持つことができます。 たとえば、複数のデバイスまたは複数のブラウザータブを介して接続されているユーザーには、複数の接続 id があります。

アプリケーションがシャットダウンすると、すべての情報が失われますが、ユーザーが接続を再確立すると、この情報は再設定されます。 環境に複数の web サーバーが含まれている場合、各サーバーには個別の接続のコレクションが存在するため、インメモリストレージは機能しません。

最初の例は、ユーザーと接続のマッピングを管理するクラスを示しています。 HashSet のキーがユーザー名になります。

[!code-csharp[Main](mapping-users-to-connections/samples/sample4.cs)]

次の例は、ハブから接続マッピングクラスを使用する方法を示しています。 クラスのインスタンスは、変数名 `_connections`に格納されます。

[!code-csharp[Main](mapping-users-to-connections/samples/sample5.cs)]

<a id="groups"></a>

## <a name="single-user-groups"></a>シングルユーザーグループ

ユーザーごとにグループを作成し、そのユーザーにのみリーチする場合は、そのグループにメッセージを送信できます。 各グループの名前は、ユーザーの名前です。 ユーザーが複数の接続を持っている場合は、各接続 id がユーザーのグループに追加されます。

ユーザーが切断された場合は、グループからユーザーを手動で削除しないでください。 このアクションは、SignalR フレームワークによって自動的に実行されます。

次の例は、シングルユーザーグループを実装する方法を示しています。

[!code-csharp[Main](mapping-users-to-connections/samples/sample6.cs)]

<a id="database"></a>

## <a name="permanent-external-storage"></a>永続的な外部ストレージ

このトピックでは、データベースまたは Azure table storage を使用して接続情報を格納する方法について説明します。 この方法は、各 web サーバーが同じデータリポジトリを操作できるため、複数の web サーバーがある場合に機能します。 Web サーバーが動作を停止した場合、またはアプリケーションが再起動した場合、`OnDisconnected` メソッドは呼び出されません。 そのため、有効ではなくなった接続 id のレコードがデータリポジトリに含まれている可能性があります。 孤立したレコードをクリーンアップするには、アプリケーションに関連する時間枠以外で作成された接続を無効にすることをお勧めします。 このセクションの例には、接続が作成された時間を追跡するための値が含まれていますが、バックグラウンド処理として必要になる可能性があるため、古いレコードをクリーンアップする方法については説明していません。

### <a name="database"></a>データベース

次の例は、接続情報とユーザー情報をデータベースに保持する方法を示しています。 任意のデータアクセステクノロジを使用できます。ただし、次の例では、Entity Framework を使用してモデルを定義する方法を示しています。 これらのエンティティモデルは、データベースのテーブルとフィールドに対応しています。 データ構造は、アプリケーションの要件によって大きく異なる可能性があります。

最初の例では、多くの接続エンティティに関連付けることができるユーザーエンティティを定義する方法を示します。

[!code-csharp[Main](mapping-users-to-connections/samples/sample7.cs)]

次に、ハブから、次に示すコードを使用して、各接続の状態を追跡できます。

[!code-csharp[Main](mapping-users-to-connections/samples/sample8.cs)]

<a id="azure"></a>
### <a name="azure-table-storage"></a>Azure Table Storage

次の Azure table storage の例は、データベースの例と似ています。 Azure Table Storage サービスの使用を開始するために必要なすべての情報が含まれているわけではありません。 詳細については、「 [.net からテーブルストレージを使用する方法](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/)」を参照してください。

次の例は、接続情報を格納するためのテーブルエンティティを示しています。 データはユーザー名でパーティション分割され、各エンティティは接続 id で識別されるため、ユーザーはいつでも複数の接続を持つことができます。

[!code-csharp[Main](mapping-users-to-connections/samples/sample9.cs)]

ハブでは、各ユーザーの接続の状態を追跡します。

[!code-csharp[Main](mapping-users-to-connections/samples/sample10.cs)]
