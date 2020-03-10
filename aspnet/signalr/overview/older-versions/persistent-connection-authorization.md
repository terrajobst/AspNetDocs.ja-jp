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
# <a name="authentication-and-authorization-for-signalr-persistent-connections-signalr-1x"></a>SignalR 永続的接続の認証と承認 (SignalR 1.x)

[Fletcher (パトリック](https://github.com/pfletcher))、 [Tom FitzMacken](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> このトピックでは、永続的な接続で承認を強制する方法について説明します。 SignalR アプリケーションへのセキュリティの統合に関する一般的な情報については、「[セキュリティの概要](index.md)」を参照してください。

## <a name="enforce-authorization"></a>承認を強制する

[PersistentConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.persistentconnection(v=vs.111).aspx)を使用するときに承認規則を適用するには、`AuthorizeRequest` メソッドをオーバーライドする必要があります。 永続的な接続では、`Authorize` 属性を使用できません。 `AuthorizeRequest` メソッドは、要求されたアクションを実行する権限がユーザーに与えられていることを確認するために、すべての要求の前に SignalR フレームワークによって呼び出されます。 `AuthorizeRequest` メソッドがクライアントから呼び出されていません。代わりに、アプリケーションの標準の認証メカニズムを使用してユーザーを認証します。

次の例は、認証されたユーザーに要求を制限する方法を示しています。

[!code-csharp[Main](persistent-connection-authorization/samples/sample1.cs)]

AuthorizeRequest メソッドには、カスタマイズされた承認ロジックを追加することができます。たとえば、ユーザーが特定のロールに属しているかどうかを確認します。
