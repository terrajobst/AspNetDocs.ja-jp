---
uid: signalr/overview/security/persistent-connection-authorization
title: SignalR 永続的接続の認証と承認 |Microsoft Docs
author: bradygaster
description: このトピックでは、永続的な接続で承認を強制する方法について説明します。 SignalR アプリケーションへのセキュリティの統合に関する一般的な情報については,...
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: e264677b-9c01-47ec-94f9-3cd8f08f94af
msc.legacyurl: /signalr/overview/security/persistent-connection-authorization
msc.type: authoredcontent
ms.openlocfilehash: 7e69d3c1a18f1239142891734ba58cd2b0078f84
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467476"
---
# <a name="authentication-and-authorization-for-signalr-persistent-connections"></a>SignalR 永続的接続の認証と承認

[Fletcher (パトリック](https://github.com/pfletcher))、 [Tom FitzMacken](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> このトピックでは、永続的な接続で承認を強制する方法について説明します。 SignalR アプリケーションへのセキュリティの統合に関する一般的な情報については、「[セキュリティの概要](introduction-to-security.md)」を参照してください。
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

## <a name="enforce-authorization"></a>承認を強制する

[PersistentConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.persistentconnection(v=vs.111).aspx)を使用するときに承認規則を適用するには、`AuthorizeRequest` メソッドをオーバーライドする必要があります。 永続的な接続では、`Authorize` 属性を使用できません。 `AuthorizeRequest` メソッドは、要求されたアクションを実行する権限がユーザーに与えられていることを確認するために、すべての要求の前に SignalR フレームワークによって呼び出されます。 `AuthorizeRequest` メソッドがクライアントから呼び出されていません。代わりに、アプリケーションの標準の認証メカニズムを使用してユーザーを認証します。

次の例は、認証されたユーザーに要求を制限する方法を示しています。

[!code-csharp[Main](persistent-connection-authorization/samples/sample1.cs)]

AuthorizeRequest メソッドには、カスタマイズされた承認ロジックを追加することができます。たとえば、ユーザーが特定のロールに属しているかどうかを確認します。
