---
uid: signalr/overview/guide-to-the-api/working-with-groups
title: SignalR | でのグループの操作Microsoft Docs
author: bradygaster
description: このトピックでは、ハブ API を使用してグループメンバーシップ情報を永続化する方法について説明します。
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: cd378ecd-3e9e-4236-b902-65916d85a048
msc.legacyurl: /signalr/overview/guide-to-the-api/working-with-groups
msc.type: authoredcontent
ms.openlocfilehash: 46dd952fc4902b37c981a111dfa344dad79bb668
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78450082"
---
# <a name="working-with-groups-in-signalr"></a><span data-ttu-id="44a6f-103">SignalR でグループを使用する</span><span class="sxs-lookup"><span data-stu-id="44a6f-103">Working with Groups in SignalR</span></span>

<span data-ttu-id="44a6f-104">[Fletcher (パトリック](https://github.com/pfletcher))、 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="44a6f-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="44a6f-105">このトピックでは、グループにユーザーを追加し、グループメンバーシップ情報を保持する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="44a6f-105">This topic describes how to add users to groups and persist group membership information.</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="44a6f-106">このトピックで使用されているソフトウェアのバージョン</span><span class="sxs-lookup"><span data-stu-id="44a6f-106">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="44a6f-107">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="44a6f-107">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="44a6f-108">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="44a6f-108">.NET 4.5</span></span>
> - <span data-ttu-id="44a6f-109">SignalR バージョン2</span><span class="sxs-lookup"><span data-stu-id="44a6f-109">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="44a6f-110">このトピックの前のバージョン</span><span class="sxs-lookup"><span data-stu-id="44a6f-110">Previous versions of this topic</span></span>
>
> <span data-ttu-id="44a6f-111">以前のバージョンの SignalR の詳細については、「[古いバージョンの SignalR](../older-versions/index.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="44a6f-111">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="44a6f-112">質問とコメント</span><span class="sxs-lookup"><span data-stu-id="44a6f-112">Questions and comments</span></span>
>
> <span data-ttu-id="44a6f-113">このチュートリアルの良い点に関するフィードバックや、ページ下部にあるコメントで改善できる点をお知らせください。</span><span class="sxs-lookup"><span data-stu-id="44a6f-113">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="44a6f-114">チュートリアルに直接関係のない質問がある場合は、 [ASP.NET SignalR フォーラム](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)または[StackOverflow.com](http://stackoverflow.com/)に投稿できます。</span><span class="sxs-lookup"><span data-stu-id="44a6f-114">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="overview"></a><span data-ttu-id="44a6f-115">概要</span><span class="sxs-lookup"><span data-stu-id="44a6f-115">Overview</span></span>

<span data-ttu-id="44a6f-116">SignalR のグループは、接続されたクライアントの指定したサブセットにメッセージをブロードキャストする方法を提供します。</span><span class="sxs-lookup"><span data-stu-id="44a6f-116">Groups in SignalR provide a method for broadcasting messages to specified subsets of connected clients.</span></span> <span data-ttu-id="44a6f-117">グループには任意の数のクライアントを含めることができ、クライアントは任意の数のグループのメンバーになることができます。</span><span class="sxs-lookup"><span data-stu-id="44a6f-117">A group can have any number of clients, and a client can be a member of any number of groups.</span></span> <span data-ttu-id="44a6f-118">明示的にグループを作成する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="44a6f-118">You don't have to explicitly create groups.</span></span> <span data-ttu-id="44a6f-119">実際には、グループの呼び出しで名前を初めて指定すると、グループが自動的に作成されます。 Add は、メンバーシップから最後の接続を削除すると削除されます。</span><span class="sxs-lookup"><span data-stu-id="44a6f-119">In effect, a group is automatically created the first time you specify its name in a call to Groups.Add, and it is deleted when you remove the last connection from membership in it.</span></span> <span data-ttu-id="44a6f-120">グループの使用方法の概要については、ハブ API サーバーガイドの[ハブクラスからグループメンバーシップを管理する方法](hubs-api-guide-server.md#groupsfromhub)に関する説明を参照してください。</span><span class="sxs-lookup"><span data-stu-id="44a6f-120">For an introduction to using groups, see [How to manage group membership from the Hub class](hubs-api-guide-server.md#groupsfromhub) in the Hubs API - Server Guide.</span></span>

<span data-ttu-id="44a6f-121">グループメンバーシップの一覧またはグループの一覧を取得するための API はありません。</span><span class="sxs-lookup"><span data-stu-id="44a6f-121">There is no API for getting a group membership list or a list of groups.</span></span> <span data-ttu-id="44a6f-122">SignalR は、pub/sub モデルに基づいてクライアントとグループにメッセージを送信します。サーバーは、グループまたはグループメンバーシップの一覧を保持しません。</span><span class="sxs-lookup"><span data-stu-id="44a6f-122">SignalR sends messages to clients and groups based on a pub/sub model, and the server does not maintain lists of groups or group memberships.</span></span> <span data-ttu-id="44a6f-123">これにより、web ファームにノードを追加するたびに、SignalR が保持するすべての状態を新しいノードに反映する必要があるため、スケーラビリティを最大化できます。</span><span class="sxs-lookup"><span data-stu-id="44a6f-123">This helps maximize scalability, because whenever you add a node to a web farm, any state that SignalR maintains has to be propagated to the new node.</span></span>

<span data-ttu-id="44a6f-124">`Groups.Add` メソッドを使用してグループにユーザーを追加すると、現在の接続の間、ユーザーはそのグループに送信されたメッセージを受信しますが、そのグループのユーザーのメンバーシップは現在の接続を超えて保持されません。</span><span class="sxs-lookup"><span data-stu-id="44a6f-124">When you add a user to a group using the `Groups.Add` method, the user receives messages directed to that group for the duration of the current connection, but the user's membership in that group is not persisted beyond the current connection.</span></span> <span data-ttu-id="44a6f-125">グループとグループのメンバーシップに関する情報を永続的に保持する場合は、データベースや Azure table storage などのリポジトリにそのデータを保存する必要があります。</span><span class="sxs-lookup"><span data-stu-id="44a6f-125">If you want to permanently retain information about groups and group membership, you must store that data in a repository such as a database or Azure table storage.</span></span> <span data-ttu-id="44a6f-126">次に、ユーザーがアプリケーションに接続するたびに、ユーザーが属するグループをリポジトリから取得し、そのユーザーをグループに手動で追加します。</span><span class="sxs-lookup"><span data-stu-id="44a6f-126">Then, each time a user connects to your application, you retrieve from the repository which groups the user belongs to, and manually add that user to those groups.</span></span>

<span data-ttu-id="44a6f-127">一時的な中断後に再接続すると、ユーザーは以前に割り当てられたグループを自動的に再度参加させます。</span><span class="sxs-lookup"><span data-stu-id="44a6f-127">When reconnecting after a temporary disruption, the user automatically re-joins the previously-assigned groups.</span></span> <span data-ttu-id="44a6f-128">自動再参加は、新しい接続を確立するときではなく、再接続するときにのみ適用されます。</span><span class="sxs-lookup"><span data-stu-id="44a6f-128">Automatically rejoining a group only applies when reconnecting, not when establishing a new connection.</span></span> <span data-ttu-id="44a6f-129">デジタル署名されたトークンは、以前に割り当てられたグループの一覧を含むクライアントから渡されます。</span><span class="sxs-lookup"><span data-stu-id="44a6f-129">A digitally-signed token is passed from the client that contains the list of previously-assigned groups.</span></span> <span data-ttu-id="44a6f-130">ユーザーが要求されたグループに属しているかどうかを確認する場合は、既定の動作をオーバーライドできます。</span><span class="sxs-lookup"><span data-stu-id="44a6f-130">If you want to verify whether the user belongs to the requested groups, you can override the default behavior.</span></span>

<span data-ttu-id="44a6f-131">このトピックのセクションは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="44a6f-131">This topic includes the following sections:</span></span>

- [<span data-ttu-id="44a6f-132">ユーザーの追加と削除</span><span class="sxs-lookup"><span data-stu-id="44a6f-132">Adding and removing users</span></span>](#add)
- [<span data-ttu-id="44a6f-133">グループのメンバーの呼び出し</span><span class="sxs-lookup"><span data-stu-id="44a6f-133">Calling members of a group</span></span>](#call)
- [<span data-ttu-id="44a6f-134">データベースにグループメンバーシップを格納する</span><span class="sxs-lookup"><span data-stu-id="44a6f-134">Storing group membership in a database</span></span>](#storedatabase)
- [<span data-ttu-id="44a6f-135">Azure table storage にグループメンバーシップを格納する</span><span class="sxs-lookup"><span data-stu-id="44a6f-135">Storing group membership in Azure table storage</span></span>](#storeazuretable)
- [<span data-ttu-id="44a6f-136">再接続時にグループメンバーシップを確認しています</span><span class="sxs-lookup"><span data-stu-id="44a6f-136">Verifying group membership when reconnecting</span></span>](#verify)

<a id="add"></a>

## <a name="adding-and-removing-users"></a><span data-ttu-id="44a6f-137">ユーザーの追加と削除</span><span class="sxs-lookup"><span data-stu-id="44a6f-137">Adding and removing users</span></span>

<span data-ttu-id="44a6f-138">グループに対してユーザーの追加または削除を行うには、 [add](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx)または[remove](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx)メソッドを呼び出し、ユーザーの接続 id とグループの名前をパラメーターとして渡します。</span><span class="sxs-lookup"><span data-stu-id="44a6f-138">To add or remove users from a group, you call the [Add](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) or [Remove](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) methods, and pass in the user's connection id and group's name as parameters.</span></span> <span data-ttu-id="44a6f-139">接続が終了したときに、ユーザーをグループから手動で削除する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="44a6f-139">You do not need to manually remove a user from a group when the connection ends.</span></span>

<span data-ttu-id="44a6f-140">次の例は、ハブメソッドで使用される `Groups.Add` および `Groups.Remove` メソッドを示しています。</span><span class="sxs-lookup"><span data-stu-id="44a6f-140">The following example shows the `Groups.Add` and `Groups.Remove` methods used in Hub methods.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample1.cs?highlight=5,10)]

<span data-ttu-id="44a6f-141">`Groups.Add` メソッドと `Groups.Remove` メソッドは、非同期的に実行されます。</span><span class="sxs-lookup"><span data-stu-id="44a6f-141">The `Groups.Add` and `Groups.Remove` methods execute asynchronously.</span></span>

<span data-ttu-id="44a6f-142">クライアントをグループに追加し、グループを使用してすぐにメッセージをクライアントに送信する場合は、最初に Groups メソッドが終了するようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="44a6f-142">If you want to add a client to a group and immediately send a message to the client by using the group, you have to make sure that the Groups.Add method finishes first.</span></span> <span data-ttu-id="44a6f-143">その方法を次のコード例に示します。</span><span class="sxs-lookup"><span data-stu-id="44a6f-143">The following code examples show how to do that.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample2.cs?highlight=1,3)]

<span data-ttu-id="44a6f-144">一般に、削除しようとしている接続 id が使用できなくなる可能性があるため、`Groups.Remove` メソッドを呼び出すときに `await` を含めないでください。</span><span class="sxs-lookup"><span data-stu-id="44a6f-144">In general, you should not include `await` when calling the `Groups.Remove` method because the connection id that you are trying to remove might no longer be available.</span></span> <span data-ttu-id="44a6f-145">その場合は、要求がタイムアウトになると `TaskCanceledException` がスローされます。グループにメッセージを送信する前に、ユーザーがグループから削除されていることをアプリケーションで確認する必要がある場合は、`Groups.Remove`する前に `await` を追加し、スローされる可能性がある `TaskCanceledException` 例外をキャッチします。</span><span class="sxs-lookup"><span data-stu-id="44a6f-145">In that case, `TaskCanceledException` is thrown after the request times out. If your application must ensure that the user has been removed from the group before sending a message to the group, you can add `await` before `Groups.Remove`, and then catch the `TaskCanceledException` exception that might be thrown.</span></span>

<a id="call"></a>

## <a name="calling-members-of-a-group"></a><span data-ttu-id="44a6f-146">グループのメンバーの呼び出し</span><span class="sxs-lookup"><span data-stu-id="44a6f-146">Calling members of a group</span></span>

<span data-ttu-id="44a6f-147">次の例に示すように、グループのすべてのメンバー、またはグループの指定されたメンバーのみにメッセージを送信できます。</span><span class="sxs-lookup"><span data-stu-id="44a6f-147">You can send messages to all of the members of a group or only specified members of the group, as shown in the following examples.</span></span>

- <span data-ttu-id="44a6f-148">指定したグループの接続されている**すべて**のクライアント。</span><span class="sxs-lookup"><span data-stu-id="44a6f-148">**All** connected clients in a specified group.</span></span>

    [!code-css[Main](working-with-groups/samples/sample3.css)]
- <span data-ttu-id="44a6f-149">指定された**クライアントを除く**、指定されたグループ内のすべての接続されているクライアント。接続 ID で識別されます。</span><span class="sxs-lookup"><span data-stu-id="44a6f-149">All connected clients in a specified group **except the specified clients**, identified by connection ID.</span></span>

    [!code-csharp[Main](working-with-groups/samples/sample4.cs)]
- <span data-ttu-id="44a6f-150">**呼び出し元のクライアントを除く**、指定されたグループ内のすべての接続されているクライアント。</span><span class="sxs-lookup"><span data-stu-id="44a6f-150">All connected clients in a specified group **except the calling client**.</span></span>

    [!code-css[Main](working-with-groups/samples/sample5.css)]

<a id="storedatabase"></a>

## <a name="storing-group-membership-in-a-database"></a><span data-ttu-id="44a6f-151">データベースにグループメンバーシップを格納する</span><span class="sxs-lookup"><span data-stu-id="44a6f-151">Storing group membership in a database</span></span>

<span data-ttu-id="44a6f-152">次の例では、データベース内のグループとユーザーの情報を保持する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="44a6f-152">The following examples show how to retain group and user information in a database.</span></span> <span data-ttu-id="44a6f-153">任意のデータアクセステクノロジを使用できます。ただし、次の例では、Entity Framework を使用してモデルを定義する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="44a6f-153">You can use any data access technology; however, the example below shows how to define models using Entity Framework.</span></span> <span data-ttu-id="44a6f-154">これらのエンティティモデルは、データベースのテーブルとフィールドに対応しています。</span><span class="sxs-lookup"><span data-stu-id="44a6f-154">These entity models correspond to database tables and fields.</span></span> <span data-ttu-id="44a6f-155">データ構造は、アプリケーションの要件によって大きく異なる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="44a6f-155">Your data structure could vary considerably depending on the requirements of your application.</span></span> <span data-ttu-id="44a6f-156">この例には `ConversationRoom` という名前のクラスが含まれています。これは、ユーザーがスポーツやガーデニングなどのさまざまなサブジェクトに関する会話を結合できるようにするアプリケーションに固有のものです。</span><span class="sxs-lookup"><span data-stu-id="44a6f-156">This example includes a class named `ConversationRoom` which would be unique to an application that enables users to join conversations about different subjects, such as sports or gardening.</span></span> <span data-ttu-id="44a6f-157">この例には、接続のクラスも含まれています。</span><span class="sxs-lookup"><span data-stu-id="44a6f-157">This example also includes a class for the connections.</span></span> <span data-ttu-id="44a6f-158">接続クラスは、追跡グループのメンバーシップには必要ありませんが、ユーザーを追跡するための堅牢なソリューションの一部になることがよくあります。</span><span class="sxs-lookup"><span data-stu-id="44a6f-158">The connection class is not absolutely required for tracking group membership but is frequently part of robust solution to tracking users.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample6.cs)]

<span data-ttu-id="44a6f-159">次に、ハブで、データベースからグループおよびユーザー情報を取得し、適切なグループに手動で追加します。</span><span class="sxs-lookup"><span data-stu-id="44a6f-159">Then, in the hub, you can retrieve the group and user information from the database and manually add the user to the appropriate groups.</span></span> <span data-ttu-id="44a6f-160">この例には、ユーザー接続を追跡するためのコードは含まれていません。</span><span class="sxs-lookup"><span data-stu-id="44a6f-160">The example does not include code for tracking the user connections.</span></span> <span data-ttu-id="44a6f-161">この例では、メッセージがグループのメンバーに直ちに送信されないため、`Groups.Add` の前に `await` キーワードが適用されません。</span><span class="sxs-lookup"><span data-stu-id="44a6f-161">In this example, the `await` keyword is not applied before `Groups.Add` because a message is not immediately sent to members of the group.</span></span> <span data-ttu-id="44a6f-162">新しいメンバーを追加した直後にグループのすべてのメンバーにメッセージを送信する場合は、`await` キーワードを適用して、非同期操作が完了したことを確認します。</span><span class="sxs-lookup"><span data-stu-id="44a6f-162">If you want to send a message to all members of the group immediately after adding the new member, you would want to apply the `await` keyword to make sure the asynchronous operation has completed.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample7.cs)]

<a id="storeazuretable"></a>

## <a name="storing-group-membership-in-azure-table-storage"></a><span data-ttu-id="44a6f-163">Azure table storage にグループメンバーシップを格納する</span><span class="sxs-lookup"><span data-stu-id="44a6f-163">Storing group membership in Azure table storage</span></span>

<span data-ttu-id="44a6f-164">Azure table storage を使用してグループとユーザー情報を格納することは、データベースを使用することと似ています。</span><span class="sxs-lookup"><span data-stu-id="44a6f-164">Using Azure table storage to store group and user information is similar to using a database.</span></span> <span data-ttu-id="44a6f-165">次の例では、ユーザー名とグループ名を格納するテーブルエンティティを示します。</span><span class="sxs-lookup"><span data-stu-id="44a6f-165">The following example shows a table entity that stores the user name and group name.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample8.cs)]

<span data-ttu-id="44a6f-166">ハブでは、ユーザーが接続するときに割り当てられたグループを取得します。</span><span class="sxs-lookup"><span data-stu-id="44a6f-166">In the hub, you retrieve the assigned groups when the user connects.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample9.cs)]

<a id="verify"></a>

## <a name="verifying-group-membership-when-reconnecting"></a><span data-ttu-id="44a6f-167">再接続時にグループメンバーシップを確認しています</span><span class="sxs-lookup"><span data-stu-id="44a6f-167">Verifying group membership when reconnecting</span></span>

<span data-ttu-id="44a6f-168">既定では、SignalR は一時的な中断から再接続するときに、適切なグループに自動的に再割り当てします。たとえば、接続が切断され、接続がタイムアウトする前に再確立された場合などです。ユーザーのグループ情報は、再接続時にトークンに渡され、そのトークンはサーバーで検証されます。</span><span class="sxs-lookup"><span data-stu-id="44a6f-168">By default, SignalR automatically re-assigns a user to the appropriate groups when reconnecting from a temporary disruption, such as when a connection is dropped and re-established before the connection times out. The user's group information is passed in a token when reconnecting, and that token is verified on the server.</span></span> <span data-ttu-id="44a6f-169">ユーザーをグループに再参加するための検証プロセスの詳細については、「再[接続時の再参加 groups](../security/introduction-to-security.md#rejoingroup)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="44a6f-169">For information about the verification process for rejoining users to groups, see [Rejoining groups when reconnecting](../security/introduction-to-security.md#rejoingroup).</span></span>

<span data-ttu-id="44a6f-170">一般に、再接続時に自動的に再参加グループの既定の動作を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="44a6f-170">In general, you should use the default behavior of automatically rejoining groups on reconnect.</span></span> <span data-ttu-id="44a6f-171">SignalR グループは、機密データへのアクセスを制限するためのセキュリティメカニズムとしては意図されていません。</span><span class="sxs-lookup"><span data-stu-id="44a6f-171">SignalR groups are not intended as a security mechanism for restricting access to sensitive data.</span></span> <span data-ttu-id="44a6f-172">ただし、再接続時にアプリケーションでユーザーのグループメンバーシップを再確認する必要がある場合は、既定の動作をオーバーライドできます。</span><span class="sxs-lookup"><span data-stu-id="44a6f-172">However, if your application must double-check a user's group membership when reconnecting, you can override the default behavior.</span></span> <span data-ttu-id="44a6f-173">既定の動作を変更すると、ユーザーが接続するときだけではなく、再接続のたびにユーザーのグループメンバーシップを取得する必要があるため、データベースに負荷を追加することができます。</span><span class="sxs-lookup"><span data-stu-id="44a6f-173">Changing the default behavior can add a burden to your database because a user's group membership must be retrieved for each reconnection rather than just when the user connects.</span></span>

<span data-ttu-id="44a6f-174">再接続時にグループメンバーシップを確認する必要がある場合は、次に示すように、割り当てられたグループの一覧を返す新しいハブパイプラインモジュールを作成します。</span><span class="sxs-lookup"><span data-stu-id="44a6f-174">If you must verify group membership on reconnect, create a new hub pipeline module that returns a list of assigned groups, as shown below.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample10.cs)]

<span data-ttu-id="44a6f-175">その後、次の強調表示されているように、そのモジュールをハブパイプラインに追加します。</span><span class="sxs-lookup"><span data-stu-id="44a6f-175">Then, add that module to the hub pipeline, as highlighted below.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample11.cs?highlight=4)]
