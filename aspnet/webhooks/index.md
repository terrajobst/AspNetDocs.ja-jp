---
uid: webhooks/index
title: ASP.NET Webhook の概要 |Microsoft Docs
author: rick-anderson
description: ASP.NET Webhook の概要です。
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 5e2843f0-f499-448f-a712-33d4e9858321
ms.openlocfilehash: aa65a20e1af16d58533e37fafc77ac246e0fe327
ms.sourcegitcommit: b95316530fa51087d6c400ff91814fe37e73f7e8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/23/2019
ms.locfileid: "70000731"
---
# <a name="aspnet-webhooks-overview"></a>ASP.NET Webhook の概要

Webhook は、Web API と SaaS サービスをまとめて配線の単純なパブリッシュ/サブスクライブ モデルを提供する軽量な HTTP パターンです。 サービスでイベントが発生すると、登録されたサブスクライバーに対して HTTP POST 要求の形式で通知が送信されます。 POST 要求には、イベントに関する情報が含まれています。これにより、受信側がそれに応じて動作できるようになります。

単純なので、 [Dropbox](http://dropbox.com/)、 [GitHub](http://www.github.com/)、 [Bitbucket](https://bitbucket.org/)、 [mailchimp](http://www.mailchimp.com/)、 [PayPal](http://www.paypal.com/)、[余裕](http://www.slack.com)、[ストライプ](http://www.stripe.com)、 [Trello](http://www.trello.com/)、および many を含む多数のサービスによって、webhook が既に公開されています。もっとその。 たとえば、WebHook は、 [Dropbox](http://dropbox.com/)でファイルが変更されたこと、またはコード変更が GitHub でコミットされたか、または[PayPal](http://www.paypal.com/)で支払いが開始されたか、または[Trello](http://www.trello.com/)でカードが作成されたことを示すことができます。 可能性は無限です。

Microsoft ASP.NET Webhook を使用すると、ASP.NET アプリケーションの一部として Webhook を送受信することが簡単になります。

* 受信側では、任意の数の WebHook プロバイダーから webhook を受信して処理するための共通のモデルが提供されます。 [Dropbox](http://dropbox.com/)、 [GitHub](http://www.github.com/)、 [Bitbucket](https://bitbucket.org/)、 [mailchimp](http://www.mailchimp.com/)、 [PayPal](http://www.paypal.com/)、 [Pusher](http://www.pusher.com)、 [Salesforce](http://www.salesforce.com)、[余裕](http://www.slack.com)、[ストライプ](http://www.stripe.com)、 [Trello](http://www.trello.com/)、[WordPress](http://www.wordpress.com)のサポートが提供されています。[Zendesk](https://www.zendesk.com/)を使用すると、サポートをさらに簡単に追加できます。

* 送信側では、サブスクリプションの管理と保存、および適切なサブスクライバーのセットへのイベント通知の送信がサポートされています。 これにより、サブスクライバーがサブスクライブできる独自のイベントセットを定義し、発生したときに通知を受け取ることができます。

シナリオに応じて、2つの部分を組み合わせて使用することも、区別することもできます。 他のサービスから Webhook だけを受け取る必要がある場合は、受信側の部分のみを使用できます。他のユーザーが使用できるように Webhook を公開するだけの場合は、そのような操作を行うことができます。

このコードは ASP.NET Web API 2 と ASP.NET MVC 5 を対象としており、 [GitHub で OSS](https://github.com/aspnet/WebHooks)として入手できます。

## <a name="webhooks-overview"></a>Webhook の概要

Webhook は、サービス間でどのように使用されるかが異なることを意味するパターンですが、基本的な考え方は同じです。 Webhook は、他の場所で発生したイベントをユーザーがサブスクライブできる単純な pub/sub モデルと考えることができます。 イベント通知は、イベント自体に関する情報を含む HTTP POST 要求として伝達されます。

通常、HTTP POST 要求には、webhook がトリガーするイベントに関する情報など、WebHook 送信者によって決定される JSON オブジェクトまたは HTML フォームデータが含まれます。 たとえば、 [GitHub](http://www.github.com/)からの WebHook POST 要求本文は、特定のリポジトリで新しい問題が開かれた結果として次のようになります。

```json
{
  "action": "opened",
  "issue": {
      "url": "https://api.github.com/repos/octocat/Hello-World/issues/1347",
      "number": 1347,
      ...
  },
  "repository": {
      "id": 1296269,
      "full_name": "octocat/Hello-World",
      "owner": {
          "login": "octocat",
          "id": 1
          ...
      },
      ...
  },
  "sender": {
      "login": "octocat",
      "id": 1,
      ...
  }
}
```

WebHook が実際に意図された送信者からのものであることを確認するために、POST 要求は何らかの方法でセキュリティ保護され、受信側によって検証されます。 たとえば、 [GitHub webhook](https://developer.github.com/webhooks/)には、要求本文のハッシュを含む、*ハブ署名*HTTP ヘッダーが含まれています。これは、これを気にする必要がないため、受信側の実装によってチェックされます。

通常、WebHook フローは次のようになります。

* WebHook 送信者は、クライアントがサブスクライブできるイベントを公開します。 イベントは、システムに対する監視可能な変更を記述します。たとえば、新しいデータ項目が挿入された場合、プロセスが完了したこと、その他の場合などです。

* WebHook 受信者は、次の4つの項目で構成される WebHook を登録することでサブスクライブします。

     1. イベント通知を HTTP POST 要求の形式でポストする必要があるの URI。

     2. WebHook を発生させる必要がある特定のイベントを説明するフィルターのセット。

     3. HTTP POST 要求に署名するために使用される秘密キー。

     4. HTTP POST 要求に含まれる追加データ。 たとえば、HTTP POST 要求の本文に含まれる追加の HTTP ヘッダーフィールドまたはプロパティを使用できます。

* イベントが発生すると、一致する WebHook 登録が検出され、HTTP POST 要求が送信されます。 通常、HTTP POST 要求の生成は、何らかの理由で受信者が応答していないか、HTTP POST 要求によってエラー応答が返された場合に、複数回再試行されます。

## <a name="webhooks-processing-pipeline"></a>Webhook 処理パイプライン

受信 webhook の Microsoft ASP.NET Webhook 処理パイプラインは次のようになります。

![ASP.NET Webhook 処理パイプライン](_static/WebHookReceivers.png)

ここでの2つの重要な概念は、*レシーバー*と*ハンドラー*です。

* *受信*側は、特定の送信者からの webhook の特定のフレーバーを処理し、セキュリティチェックを適用して、webhook 要求が実際に意図された送信者からのものであることを確認します。

* 通常、*ハンドラー*は、ユーザーコードが特定の WebHook の処理を実行します。

次のノードでは、これらの概念について詳しく説明します。
