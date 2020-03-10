---
uid: signalr/overview/older-versions/working-with-groups
title: SignalR 1.x | のグループを操作するMicrosoft Docs
author: bradygaster
description: このトピックでは、ハブ API を使用してグループメンバーシップ情報を永続化する方法について説明します。
ms.author: bradyg
ms.date: 10/21/2013
ms.assetid: 22929efd-68c9-4609-b76d-f8ba42fda01e
msc.legacyurl: /signalr/overview/older-versions/working-with-groups
msc.type: authoredcontent
ms.openlocfilehash: 5f50dc162d6cdcfbf2261e6a751f5f99078d5c54
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467896"
---
# <a name="working-with-groups-in-signalr-1x"></a>SignalR 1.x でグループを使用する

[Fletcher (パトリック](https://github.com/pfletcher))、 [Tom FitzMacken](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> このトピックでは、グループにユーザーを追加し、グループメンバーシップ情報を保持する方法について説明します。

## <a name="overview"></a>概要

SignalR のグループは、接続されたクライアントの指定したサブセットにメッセージをブロードキャストする方法を提供します。 グループには任意の数のクライアントを含めることができ、クライアントは任意の数のグループのメンバーになることができます。 明示的にグループを作成する必要はありません。 実際には、グループの呼び出しで名前を初めて指定すると、グループが自動的に作成されます。 Add は、メンバーシップから最後の接続を削除すると削除されます。 グループの使用方法の概要については、ハブ API サーバーガイドの[ハブクラスからグループメンバーシップを管理する方法](index.md)に関する説明を参照してください。

グループメンバーシップの一覧またはグループの一覧を取得するための API はありません。 SignalR は、pub/sub モデルに基づいてクライアントとグループにメッセージを送信します。サーバーは、グループまたはグループメンバーシップの一覧を保持しません。 これにより、web ファームにノードを追加するたびに、SignalR が保持するすべての状態を新しいノードに反映する必要があるため、スケーラビリティを最大化できます。

`Groups.Add` メソッドを使用してグループにユーザーを追加すると、現在の接続の間、ユーザーはそのグループに送信されたメッセージを受信しますが、そのグループのユーザーのメンバーシップは現在の接続を超えて保持されません。 グループとグループのメンバーシップに関する情報を永続的に保持する場合は、データベースや Azure table storage などのリポジトリにそのデータを保存する必要があります。 次に、ユーザーがアプリケーションに接続するたびに、ユーザーが属するグループをリポジトリから取得し、そのユーザーをグループに手動で追加します。

一時的な中断後に再接続すると、ユーザーは以前に割り当てられたグループを自動的に再度参加させます。 自動再参加は、新しい接続を確立するときではなく、再接続するときにのみ適用されます。 デジタル署名されたトークンは、以前に割り当てられたグループの一覧を含むクライアントから渡されます。 ユーザーが要求されたグループに属しているかどうかを確認する場合は、既定の動作をオーバーライドできます。

このトピックのセクションは次のとおりです。

- [ユーザーの追加と削除](#add)
- [グループのメンバーの呼び出し](#call)
- [データベースにグループメンバーシップを格納する](#storedatabase)
- [Azure table storage にグループメンバーシップを格納する](#storeazuretable)
- [再接続時にグループメンバーシップを確認しています](#verify)

<a id="add"></a>

## <a name="adding-and-removing-users"></a>ユーザーの追加と削除

グループに対してユーザーの追加または削除を行うには、 [add](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx)または[remove](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx)メソッドを呼び出し、ユーザーの接続 id とグループの名前をパラメーターとして渡します。 接続が終了したときに、ユーザーをグループから手動で削除する必要はありません。

次の例は、ハブメソッドで使用される `Groups.Add` および `Groups.Remove` メソッドを示しています。

[!code-csharp[Main](working-with-groups/samples/sample1.cs?highlight=5,10)]

`Groups.Add` メソッドと `Groups.Remove` メソッドは、非同期的に実行されます。

クライアントをグループに追加し、グループを使用してすぐにメッセージをクライアントに送信する場合は、最初に Groups メソッドが終了するようにする必要があります。 次のコード例は、.NET 4.5 で動作するコードと .NET 4 で動作するコードを使用して、その方法を示しています。

#### <a name="asynchronous-net-45-example"></a>非同期 .NET 4.5 の例

[!code-csharp[Main](working-with-groups/samples/sample2.cs?highlight=1,3)]

#### <a name="asynchronous-net-4-example"></a>.NET 4 の非同期の例

[!code-csharp[Main](working-with-groups/samples/sample3.cs?highlight=3-4)]

一般に、削除しようとしている接続 id が使用できなくなる可能性があるため、`Groups.Remove` メソッドを呼び出すときに `await` を含めないでください。 その場合は、要求がタイムアウトになると `TaskCanceledException` がスローされます。グループにメッセージを送信する前に、ユーザーがグループから削除されていることをアプリケーションで確認する必要がある場合は、グループの前に `await` を追加します。を削除し、スローされる可能性のある `TaskCanceledException` 例外をキャッチします。

<a id="call"></a>

## <a name="calling-members-of-a-group"></a>グループのメンバーの呼び出し

次の例に示すように、グループのすべてのメンバー、またはグループの指定されたメンバーのみにメッセージを送信できます。

- 指定したグループの接続されている**すべて**のクライアント。 

    [!code-css[Main](working-with-groups/samples/sample4.css)]
- 指定された**クライアントを除く**、指定されたグループ内のすべての接続されているクライアント。接続 ID で識別されます。 

    [!code-csharp[Main](working-with-groups/samples/sample5.cs)]
- **呼び出し元のクライアントを除く**、指定されたグループ内のすべての接続されているクライアント。 

    [!code-css[Main](working-with-groups/samples/sample6.css)]

<a id="storedatabase"></a>

## <a name="storing-group-membership-in-a-database"></a>データベースにグループメンバーシップを格納する

次の例では、データベース内のグループとユーザーの情報を保持する方法を示します。 任意のデータアクセステクノロジを使用できます。ただし、次の例では、Entity Framework を使用してモデルを定義する方法を示しています。 これらのエンティティモデルは、データベースのテーブルとフィールドに対応しています。 データ構造は、アプリケーションの要件によって大きく異なる可能性があります。 この例には `ConversationRoom` という名前のクラスが含まれています。これは、ユーザーがスポーツやガーデニングなどのさまざまなサブジェクトに関する会話を結合できるようにするアプリケーションに固有のものです。 この例には、接続のクラスも含まれています。 接続クラスは、追跡グループのメンバーシップには必要ありませんが、ユーザーを追跡するための堅牢なソリューションの一部になることがよくあります。

[!code-csharp[Main](working-with-groups/samples/sample7.cs)]

次に、ハブで、データベースからグループおよびユーザー情報を取得し、適切なグループに手動で追加します。 この例には、ユーザー接続を追跡するためのコードは含まれていません。 この例では、メッセージがグループのメンバーに直ちに送信されないため、`Groups.Add` の前に `await` キーワードが適用されません。 新しいメンバーを追加した直後にグループのすべてのメンバーにメッセージを送信する場合は、`await` キーワードを適用して、非同期操作が完了したことを確認します。

[!code-csharp[Main](working-with-groups/samples/sample8.cs)]

<a id="storeazuretable"></a>

## <a name="storing-group-membership-in-azure-table-storage"></a>Azure table storage にグループメンバーシップを格納する

Azure table storage を使用してグループとユーザー情報を格納することは、データベースを使用することと似ています。 次の例では、ユーザー名とグループ名を格納するテーブルエンティティを示します。

[!code-csharp[Main](working-with-groups/samples/sample9.cs)]

ハブでは、ユーザーが接続するときに割り当てられたグループを取得します。

[!code-csharp[Main](working-with-groups/samples/sample10.cs)]

<a id="verify"></a>

## <a name="verifying-group-membership-when-reconnecting"></a>再接続時にグループメンバーシップを確認しています

既定では、SignalR は一時的な中断から再接続するときに、適切なグループに自動的に再割り当てします。たとえば、接続が切断され、接続がタイムアウトする前に再確立された場合などです。ユーザーのグループ情報は、再接続時にトークンに渡され、そのトークンはサーバーで検証されます。 ユーザーをグループに再参加するための検証プロセスの詳細については、「再[接続時の再参加 groups](index.md)」を参照してください。

一般に、再接続時に自動的に再参加グループの既定の動作を使用する必要があります。 SignalR グループは、機密データへのアクセスを制限するためのセキュリティメカニズムとしては意図されていません。 ただし、再接続時にアプリケーションでユーザーのグループメンバーシップを再確認する必要がある場合は、既定の動作をオーバーライドできます。 既定の動作を変更すると、ユーザーが接続するときだけではなく、再接続のたびにユーザーのグループメンバーシップを取得する必要があるため、データベースに負荷を追加することができます。

再接続時にグループメンバーシップを確認する必要がある場合は、次に示すように、割り当てられたグループの一覧を返す新しいハブパイプラインモジュールを作成します。

[!code-csharp[Main](working-with-groups/samples/sample11.cs)]

その後、次の強調表示されているように、そのモジュールをハブパイプラインに追加します。

[!code-csharp[Main](working-with-groups/samples/sample12.cs?highlight=10)]
