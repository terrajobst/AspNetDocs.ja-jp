---
uid: signalr/overview/older-versions/persistent-connection-authorization
title: SignalR 永続的接続の認証と承認 (SignalR 1.x) |Microsoft Docs
author: bradygaster
description: このトピックでは、永続的な接続で承認を強制する方法について説明します。 SignalR アプリケーションへのセキュリティの統合に関する一般的な情報については,...
ms.author: bradyg
ms.date: 10/21/2013
ms.assetid: c34bc627-41af-4c21-a817-e97a19a7f252
msc.legacyurl: /signalr/overview/older-versions/persistent-connection-authorization
msc.type: authoredcontent
ms.openlocfilehash: 9ccc59e3ea502daf12ce82382ab30ca73ca0f9b5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78431188"
---
# <a name="authentication-and-authorization-for-signalr-persistent-connections-signalr-1x"></a><span data-ttu-id="bc6d4-104">SignalR 永続的接続の認証と承認 (SignalR 1.x)</span><span class="sxs-lookup"><span data-stu-id="bc6d4-104">Authentication and Authorization for SignalR Persistent Connections (SignalR 1.x)</span></span>

<span data-ttu-id="bc6d4-105">[Fletcher (パトリック](https://github.com/pfletcher))、 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="bc6d4-105">by [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="bc6d4-106">このトピックでは、永続的な接続で承認を強制する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="bc6d4-106">This topic describes how to enforce authorization on a persistent connection.</span></span> <span data-ttu-id="bc6d4-107">SignalR アプリケーションへのセキュリティの統合に関する一般的な情報については、「[セキュリティの概要](index.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="bc6d4-107">For general information about integrating security into a SignalR application, see [Introduction to Security](index.md).</span></span>

## <a name="enforce-authorization"></a><span data-ttu-id="bc6d4-108">承認を強制する</span><span class="sxs-lookup"><span data-stu-id="bc6d4-108">Enforce authorization</span></span>

<span data-ttu-id="bc6d4-109">[PersistentConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.persistentconnection(v=vs.111).aspx)を使用するときに承認規則を適用するには、`AuthorizeRequest` メソッドをオーバーライドする必要があります。</span><span class="sxs-lookup"><span data-stu-id="bc6d4-109">To enforce authorization rules when using a [PersistentConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.persistentconnection(v=vs.111).aspx) you must override the `AuthorizeRequest` method.</span></span> <span data-ttu-id="bc6d4-110">永続的な接続では、`Authorize` 属性を使用できません。</span><span class="sxs-lookup"><span data-stu-id="bc6d4-110">You cannot use the `Authorize` attribute with persistent connections.</span></span> <span data-ttu-id="bc6d4-111">`AuthorizeRequest` メソッドは、要求されたアクションを実行する権限がユーザーに与えられていることを確認するために、すべての要求の前に SignalR フレームワークによって呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="bc6d4-111">The `AuthorizeRequest` method is called by the SignalR Framework before every request to verify that the user is authorized to perform the requested action.</span></span> <span data-ttu-id="bc6d4-112">`AuthorizeRequest` メソッドがクライアントから呼び出されていません。代わりに、アプリケーションの標準の認証メカニズムを使用してユーザーを認証します。</span><span class="sxs-lookup"><span data-stu-id="bc6d4-112">The `AuthorizeRequest` method is not called from the client; instead, you authenticate the user through your application's standard authentication mechanism.</span></span>

<span data-ttu-id="bc6d4-113">次の例は、認証されたユーザーに要求を制限する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="bc6d4-113">The example below shows how to limit requests to authenticated users.</span></span>

[!code-csharp[Main](persistent-connection-authorization/samples/sample1.cs)]

<span data-ttu-id="bc6d4-114">AuthorizeRequest メソッドには、カスタマイズされた承認ロジックを追加することができます。たとえば、ユーザーが特定のロールに属しているかどうかを確認します。</span><span class="sxs-lookup"><span data-stu-id="bc6d4-114">You can add any customized authorization logic in the AuthorizeRequest method; such as, checking whether a user belongs to a particular role.</span></span>
