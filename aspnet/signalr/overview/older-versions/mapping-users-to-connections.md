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
# <a name="mapping-signalr-users-to-connections-in-signalr-1x"></a><span data-ttu-id="3b77c-103">SignalR 1.x で SignalR ユーザーを接続にマッピングする</span><span class="sxs-lookup"><span data-stu-id="3b77c-103">Mapping SignalR Users to Connections in SignalR 1.x</span></span>

<span data-ttu-id="3b77c-104">[Fletcher (パトリック](https://github.com/pfletcher))、 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="3b77c-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="3b77c-105">このトピックでは、ユーザーとその接続に関する情報を保持する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="3b77c-105">This topic shows how to retain information about users and their connections.</span></span>

## <a name="introduction"></a><span data-ttu-id="3b77c-106">はじめに</span><span class="sxs-lookup"><span data-stu-id="3b77c-106">Introduction</span></span>

<span data-ttu-id="3b77c-107">ハブに接続する各クライアントは、一意の接続 id を渡します。この値は、ハブコンテキストの `Context.ConnectionId` プロパティで取得できます。</span><span class="sxs-lookup"><span data-stu-id="3b77c-107">Each client connecting to a hub passes a unique connection id. You can retrieve this value in the `Context.ConnectionId` property of the hub context.</span></span> <span data-ttu-id="3b77c-108">アプリケーションでユーザーを接続 id にマップし、そのマッピングを保持する必要がある場合は、次のいずれかを使用できます。</span><span class="sxs-lookup"><span data-stu-id="3b77c-108">If your application needs to map a user to the connection id and persist that mapping, you can use one of the following:</span></span>

- <span data-ttu-id="3b77c-109">[メモリ内ストレージ](#inmemory)(ディクショナリなど)</span><span class="sxs-lookup"><span data-stu-id="3b77c-109">[In-memory storage](#inmemory), such as a dictionary</span></span>
- [<span data-ttu-id="3b77c-110">各ユーザーの SignalR グループ</span><span class="sxs-lookup"><span data-stu-id="3b77c-110">SignalR group for each user</span></span>](#groups)
- <span data-ttu-id="3b77c-111">[永続的な外部ストレージ](#database)(データベーステーブルや Azure table storage など)</span><span class="sxs-lookup"><span data-stu-id="3b77c-111">[Permanent, external storage](#database), such as a database table or Azure table storage</span></span>

<span data-ttu-id="3b77c-112">このトピックでは、これらの各実装について説明します。</span><span class="sxs-lookup"><span data-stu-id="3b77c-112">Each of these implementations is shown in this topic.</span></span> <span data-ttu-id="3b77c-113">`Hub` クラスの `OnConnected`、`OnDisconnected`、および `OnReconnected` の各メソッドを使用して、ユーザー接続の状態を追跡します。</span><span class="sxs-lookup"><span data-stu-id="3b77c-113">You use the `OnConnected`, `OnDisconnected`, and `OnReconnected` methods of the `Hub` class to track the user connection status.</span></span>

<span data-ttu-id="3b77c-114">アプリケーションに最適な方法は、次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="3b77c-114">The best approach for your application depends on:</span></span>

- <span data-ttu-id="3b77c-115">アプリケーションをホストしている web サーバーの数。</span><span class="sxs-lookup"><span data-stu-id="3b77c-115">The number of web servers hosting your application.</span></span>
- <span data-ttu-id="3b77c-116">現在接続しているユーザーの一覧を取得する必要があるかどうか。</span><span class="sxs-lookup"><span data-stu-id="3b77c-116">Whether you need to get a list of the currently connected users.</span></span>
- <span data-ttu-id="3b77c-117">アプリケーションまたはサーバーの再起動時に、グループとユーザーの情報を保持する必要があるかどうか。</span><span class="sxs-lookup"><span data-stu-id="3b77c-117">Whether you need to persist group and user information when the application or server restarts.</span></span>
- <span data-ttu-id="3b77c-118">外部サーバーの呼び出しの待機時間が問題になるかどうか。</span><span class="sxs-lookup"><span data-stu-id="3b77c-118">Whether the latency of calling an external server is an issue.</span></span>

<span data-ttu-id="3b77c-119">次の表は、これらの考慮事項に対して機能する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="3b77c-119">The following table shows which approach works for these considerations.</span></span>

|  | <span data-ttu-id="3b77c-120">複数のサーバー</span><span class="sxs-lookup"><span data-stu-id="3b77c-120">More than one server</span></span> | <span data-ttu-id="3b77c-121">現在接続しているユーザーの一覧を取得します。</span><span class="sxs-lookup"><span data-stu-id="3b77c-121">Get list of currently connected users</span></span> | <span data-ttu-id="3b77c-122">再起動後に情報を保持する</span><span class="sxs-lookup"><span data-stu-id="3b77c-122">Persist information after restarts</span></span> | <span data-ttu-id="3b77c-123">最適なパフォーマンス</span><span class="sxs-lookup"><span data-stu-id="3b77c-123">Optimal performance</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="3b77c-124">メモリ内</span><span class="sxs-lookup"><span data-stu-id="3b77c-124">In-memory</span></span> |  | ![](mapping-users-to-connections/_static/image1.png) |  | ![](mapping-users-to-connections/_static/image2.png) |
| <span data-ttu-id="3b77c-125">シングルユーザーグループ</span><span class="sxs-lookup"><span data-stu-id="3b77c-125">Single-user groups</span></span> | ![](mapping-users-to-connections/_static/image3.png) |  |  | ![](mapping-users-to-connections/_static/image4.png) |
| <span data-ttu-id="3b77c-126">パーマネント、外部</span><span class="sxs-lookup"><span data-stu-id="3b77c-126">Permanent, external</span></span> | ![](mapping-users-to-connections/_static/image5.png) | ![](mapping-users-to-connections/_static/image6.png) | ![](mapping-users-to-connections/_static/image7.png) |  |

<a id="inmemory"></a>

## <a name="in-memory-storage"></a><span data-ttu-id="3b77c-127">インメモリストレージ</span><span class="sxs-lookup"><span data-stu-id="3b77c-127">In-memory storage</span></span>

<span data-ttu-id="3b77c-128">次の例は、メモリに格納されているディクショナリに接続情報とユーザー情報を保持する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="3b77c-128">The following examples show how to retain connection and user information in a dictionary that is stored in memory.</span></span> <span data-ttu-id="3b77c-129">ディクショナリは、`HashSet` を使用して接続 id を格納します。ユーザーは、いつでも SignalR アプリケーションに対して複数の接続を持つことができます。</span><span class="sxs-lookup"><span data-stu-id="3b77c-129">The dictionary uses a `HashSet` to store the connection id. At any time a user could have more than one connection to the SignalR application.</span></span> <span data-ttu-id="3b77c-130">たとえば、複数のデバイスまたは複数のブラウザータブを介して接続されているユーザーには、複数の接続 id があります。</span><span class="sxs-lookup"><span data-stu-id="3b77c-130">For example, a user who is connected through multiple devices or more than one browser tab would have more than one connection id.</span></span>

<span data-ttu-id="3b77c-131">アプリケーションがシャットダウンすると、すべての情報が失われますが、ユーザーが接続を再確立すると、この情報は再設定されます。</span><span class="sxs-lookup"><span data-stu-id="3b77c-131">If the application shuts down, all of the information is lost, but it will be re-populated as the users re-establish their connections.</span></span> <span data-ttu-id="3b77c-132">環境に複数の web サーバーが含まれている場合、各サーバーには個別の接続のコレクションが存在するため、インメモリストレージは機能しません。</span><span class="sxs-lookup"><span data-stu-id="3b77c-132">In-memory storage does not work if your environment includes more than one web server because each server would have a separate collection of connections.</span></span>

<span data-ttu-id="3b77c-133">最初の例は、ユーザーと接続のマッピングを管理するクラスを示しています。</span><span class="sxs-lookup"><span data-stu-id="3b77c-133">The first example shows a class that manages the mapping of users to connections.</span></span> <span data-ttu-id="3b77c-134">HashSet のキーがユーザー名になります。</span><span class="sxs-lookup"><span data-stu-id="3b77c-134">The key for the HashSet will be the user's name.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample1.cs)]

<span data-ttu-id="3b77c-135">次の例は、ハブから接続マッピングクラスを使用する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="3b77c-135">The next example shows how to use the connection mapping class from a hub.</span></span> <span data-ttu-id="3b77c-136">クラスのインスタンスは、変数名 `_connections`に格納されます。</span><span class="sxs-lookup"><span data-stu-id="3b77c-136">The instance of the class is stored in a variable name `_connections`.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample2.cs)]

<a id="groups"></a>

## <a name="single-user-groups"></a><span data-ttu-id="3b77c-137">シングルユーザーグループ</span><span class="sxs-lookup"><span data-stu-id="3b77c-137">Single-user groups</span></span>

<span data-ttu-id="3b77c-138">ユーザーごとにグループを作成し、そのユーザーにのみリーチする場合は、そのグループにメッセージを送信できます。</span><span class="sxs-lookup"><span data-stu-id="3b77c-138">You can create a group for each user, and then send a message to that group when you want to reach only that user.</span></span> <span data-ttu-id="3b77c-139">各グループの名前は、ユーザーの名前です。</span><span class="sxs-lookup"><span data-stu-id="3b77c-139">The name of each group is the name of the user.</span></span> <span data-ttu-id="3b77c-140">ユーザーが複数の接続を持っている場合は、各接続 id がユーザーのグループに追加されます。</span><span class="sxs-lookup"><span data-stu-id="3b77c-140">If a user has more than one connection, each connection id is added to the user's group.</span></span>

<span data-ttu-id="3b77c-141">ユーザーが切断された場合は、グループからユーザーを手動で削除しないでください。</span><span class="sxs-lookup"><span data-stu-id="3b77c-141">You should not manually remove the user from the group when the user disconnects.</span></span> <span data-ttu-id="3b77c-142">このアクションは、SignalR フレームワークによって自動的に実行されます。</span><span class="sxs-lookup"><span data-stu-id="3b77c-142">This action is automatically performed by the SignalR framework.</span></span>

<span data-ttu-id="3b77c-143">次の例は、シングルユーザーグループを実装する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="3b77c-143">The following example shows how to implement single-user groups.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample3.cs)]

<a id="database"></a>

## <a name="permanent-external-storage"></a><span data-ttu-id="3b77c-144">永続的な外部ストレージ</span><span class="sxs-lookup"><span data-stu-id="3b77c-144">Permanent, external storage</span></span>

<span data-ttu-id="3b77c-145">このトピックでは、データベースまたは Azure table storage を使用して接続情報を格納する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="3b77c-145">This topic shows how to use either a database or Azure table storage for storing connection information.</span></span> <span data-ttu-id="3b77c-146">この方法は、各 web サーバーが同じデータリポジトリを操作できるため、複数の web サーバーがある場合に機能します。</span><span class="sxs-lookup"><span data-stu-id="3b77c-146">This approach works when you have multiple web servers because each web server can interact with the same data repository.</span></span> <span data-ttu-id="3b77c-147">Web サーバーが動作を停止した場合、またはアプリケーションが再起動した場合、`OnDisconnected` メソッドは呼び出されません。</span><span class="sxs-lookup"><span data-stu-id="3b77c-147">If your web servers stop working or the application restarts, the `OnDisconnected` method is not called.</span></span> <span data-ttu-id="3b77c-148">そのため、有効ではなくなった接続 id のレコードがデータリポジトリに含まれている可能性があります。</span><span class="sxs-lookup"><span data-stu-id="3b77c-148">Therefore, it is possible that your data repository will have records for connection ids that are no longer valid.</span></span> <span data-ttu-id="3b77c-149">孤立したレコードをクリーンアップするには、アプリケーションに関連する時間枠以外で作成された接続を無効にすることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="3b77c-149">To clean up these orphaned records, you may wish to invalidate any connection that was created outside of a timeframe that is relevant to your application.</span></span> <span data-ttu-id="3b77c-150">このセクションの例には、接続が作成された時間を追跡するための値が含まれていますが、バックグラウンド処理として必要になる可能性があるため、古いレコードをクリーンアップする方法については説明していません。</span><span class="sxs-lookup"><span data-stu-id="3b77c-150">The examples in this section include a value for tracking when the connection was created, but do not show how to clean up old records because you may want to do that as background process.</span></span>

### <a name="database"></a><span data-ttu-id="3b77c-151">データベース</span><span class="sxs-lookup"><span data-stu-id="3b77c-151">Database</span></span>

<span data-ttu-id="3b77c-152">次の例は、接続情報とユーザー情報をデータベースに保持する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="3b77c-152">The following examples show how to retain connection and user information in a database.</span></span> <span data-ttu-id="3b77c-153">任意のデータアクセステクノロジを使用できます。ただし、次の例では、Entity Framework を使用してモデルを定義する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="3b77c-153">You can use any data access technology; however, the example below shows how to define models using Entity Framework.</span></span> <span data-ttu-id="3b77c-154">これらのエンティティモデルは、データベースのテーブルとフィールドに対応しています。</span><span class="sxs-lookup"><span data-stu-id="3b77c-154">These entity models correspond to database tables and fields.</span></span> <span data-ttu-id="3b77c-155">データ構造は、アプリケーションの要件によって大きく異なる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="3b77c-155">Your data structure could vary considerably depending on the requirements of your application.</span></span>

<span data-ttu-id="3b77c-156">最初の例では、多くの接続エンティティに関連付けることができるユーザーエンティティを定義する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="3b77c-156">The first example shows how to define a user entity that can be associated with many connection entities.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample4.cs)]

<span data-ttu-id="3b77c-157">次に、ハブから、次に示すコードを使用して、各接続の状態を追跡できます。</span><span class="sxs-lookup"><span data-stu-id="3b77c-157">Then, from the hub, you can track the state of each connection with the code shown below.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample5.cs)]

### <a name="azure-table-storage"></a><span data-ttu-id="3b77c-158">Azure Table Storage</span><span class="sxs-lookup"><span data-stu-id="3b77c-158">Azure table storage</span></span>

<span data-ttu-id="3b77c-159">次の Azure table storage の例は、データベースの例と似ています。</span><span class="sxs-lookup"><span data-stu-id="3b77c-159">The following Azure table storage example is similar to the database example.</span></span> <span data-ttu-id="3b77c-160">Azure Table Storage サービスの使用を開始するために必要なすべての情報が含まれているわけではありません。</span><span class="sxs-lookup"><span data-stu-id="3b77c-160">It does not include all of the information that you would need to get started with Azure Table Storage Service.</span></span> <span data-ttu-id="3b77c-161">詳細については、「 [.net からテーブルストレージを使用する方法](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="3b77c-161">For information, see [How to use Table storage from .NET](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/).</span></span>

<span data-ttu-id="3b77c-162">次の例は、接続情報を格納するためのテーブルエンティティを示しています。</span><span class="sxs-lookup"><span data-stu-id="3b77c-162">The following example shows a table entity for storing connection information.</span></span> <span data-ttu-id="3b77c-163">データはユーザー名でパーティション分割され、各エンティティは接続 id で識別されるため、ユーザーはいつでも複数の接続を持つことができます。</span><span class="sxs-lookup"><span data-stu-id="3b77c-163">It partitions the data by user name, and identifies each entity by the connection id, so a user can have multiple connections at any time.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample6.cs)]

<span data-ttu-id="3b77c-164">ハブでは、各ユーザーの接続の状態を追跡します。</span><span class="sxs-lookup"><span data-stu-id="3b77c-164">In the hub, you track the status of each user's connection.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample7.cs)]
