---
uid: signalr/overview/older-versions/mapping-users-to-connections
title: SignalR 1.x の接続に SignalR ユーザーをマッピングする |Microsoft Docs
author: bradygaster
description: このトピックでは、ユーザーとその接続に関する情報を保持する方法について説明します。
ms.author: bradyg
ms.date: 10/17/2013
ms.assetid: ebbc93a8-e6c4-4122-8e0d-3aa42293c747
msc.legacyurl: /signalr/overview/older-versions/mapping-users-to-connections
msc.type: authoredcontent
ms.openlocfilehash: 9d948495e9b8821fcb465611b6926603c3756a19
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449998"
---
# <a name="mapping-signalr-users-to-connections-in-signalr-1x"></a>SignalR 1.x で SignalR ユーザーを接続にマッピングする

[Fletcher (パトリック](https://github.com/pfletcher))、 [Tom FitzMacken](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> このトピックでは、ユーザーとその接続に関する情報を保持する方法について説明します。

## <a name="introduction"></a>はじめに

ハブに接続する各クライアントは、一意の接続 id を渡します。この値は、ハブコンテキストの `Context.ConnectionId` プロパティで取得できます。 アプリケーションでユーザーを接続 id にマップし、そのマッピングを保持する必要がある場合は、次のいずれかを使用できます。

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
| メモリ内 |  | ![](mapping-users-to-connections/_static/image1.png) |  | ![](mapping-users-to-connections/_static/image2.png) |
| シングルユーザーグループ | ![](mapping-users-to-connections/_static/image3.png) |  |  | ![](mapping-users-to-connections/_static/image4.png) |
| パーマネント、外部 | ![](mapping-users-to-connections/_static/image5.png) | ![](mapping-users-to-connections/_static/image6.png) | ![](mapping-users-to-connections/_static/image7.png) |  |

<a id="inmemory"></a>

## <a name="in-memory-storage"></a>インメモリストレージ

次の例は、メモリに格納されているディクショナリに接続情報とユーザー情報を保持する方法を示しています。 ディクショナリは、`HashSet` を使用して接続 id を格納します。ユーザーは、いつでも SignalR アプリケーションに対して複数の接続を持つことができます。 たとえば、複数のデバイスまたは複数のブラウザータブを介して接続されているユーザーには、複数の接続 id があります。

アプリケーションがシャットダウンすると、すべての情報が失われますが、ユーザーが接続を再確立すると、この情報は再設定されます。 環境に複数の web サーバーが含まれている場合、各サーバーには個別の接続のコレクションが存在するため、インメモリストレージは機能しません。

最初の例は、ユーザーと接続のマッピングを管理するクラスを示しています。 HashSet のキーがユーザー名になります。

[!code-csharp[Main](mapping-users-to-connections/samples/sample1.cs)]

次の例は、ハブから接続マッピングクラスを使用する方法を示しています。 クラスのインスタンスは、変数名 `_connections`に格納されます。

[!code-csharp[Main](mapping-users-to-connections/samples/sample2.cs)]

<a id="groups"></a>

## <a name="single-user-groups"></a>シングルユーザーグループ

ユーザーごとにグループを作成し、そのユーザーにのみリーチする場合は、そのグループにメッセージを送信できます。 各グループの名前は、ユーザーの名前です。 ユーザーが複数の接続を持っている場合は、各接続 id がユーザーのグループに追加されます。

ユーザーが切断された場合は、グループからユーザーを手動で削除しないでください。 このアクションは、SignalR フレームワークによって自動的に実行されます。

次の例は、シングルユーザーグループを実装する方法を示しています。

[!code-csharp[Main](mapping-users-to-connections/samples/sample3.cs)]

<a id="database"></a>

## <a name="permanent-external-storage"></a>永続的な外部ストレージ

このトピックでは、データベースまたは Azure table storage を使用して接続情報を格納する方法について説明します。 この方法は、各 web サーバーが同じデータリポジトリを操作できるため、複数の web サーバーがある場合に機能します。 Web サーバーが動作を停止した場合、またはアプリケーションが再起動した場合、`OnDisconnected` メソッドは呼び出されません。 そのため、有効ではなくなった接続 id のレコードがデータリポジトリに含まれている可能性があります。 孤立したレコードをクリーンアップするには、アプリケーションに関連する時間枠以外で作成された接続を無効にすることをお勧めします。 このセクションの例には、接続が作成された時間を追跡するための値が含まれていますが、バックグラウンド処理として必要になる可能性があるため、古いレコードをクリーンアップする方法については説明していません。

### <a name="database"></a>データベース

次の例は、接続情報とユーザー情報をデータベースに保持する方法を示しています。 任意のデータアクセステクノロジを使用できます。ただし、次の例では、Entity Framework を使用してモデルを定義する方法を示しています。 これらのエンティティモデルは、データベースのテーブルとフィールドに対応しています。 データ構造は、アプリケーションの要件によって大きく異なる可能性があります。

最初の例では、多くの接続エンティティに関連付けることができるユーザーエンティティを定義する方法を示します。

[!code-csharp[Main](mapping-users-to-connections/samples/sample4.cs)]

次に、ハブから、次に示すコードを使用して、各接続の状態を追跡できます。

[!code-csharp[Main](mapping-users-to-connections/samples/sample5.cs)]

### <a name="azure-table-storage"></a>Azure Table Storage

次の Azure table storage の例は、データベースの例と似ています。 Azure Table Storage サービスの使用を開始するために必要なすべての情報が含まれているわけではありません。 詳細については、「 [.net からテーブルストレージを使用する方法](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/)」を参照してください。

次の例は、接続情報を格納するためのテーブルエンティティを示しています。 データはユーザー名でパーティション分割され、各エンティティは接続 id で識別されるため、ユーザーはいつでも複数の接続を持つことができます。

[!code-csharp[Main](mapping-users-to-connections/samples/sample6.cs)]

ハブでは、各ユーザーの接続の状態を追跡します。

[!code-csharp[Main](mapping-users-to-connections/samples/sample7.cs)]
