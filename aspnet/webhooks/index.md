---
uid: webhooks/index
title: ASP.NET Webhook の概要 |Microsoft Docs
author: rick-anderson
description: ASP.NET Webhook の概要です。
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 5e2843f0-f499-448f-a712-33d4e9858321
ms.openlocfilehash: 1e21c92e950893c0ff87c63f03f4710a158441fd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78517534"
---
# <a name="aspnet-webhooks-overview"></a><span data-ttu-id="3d8e9-103">ASP.NET Webhook の概要</span><span class="sxs-lookup"><span data-stu-id="3d8e9-103">ASP.NET WebHooks overview</span></span>

<span data-ttu-id="3d8e9-104">Webhook は、Web API と SaaS サービスをまとめて配線の単純なパブリッシュ/サブスクライブ モデルを提供する軽量な HTTP パターンです。</span><span class="sxs-lookup"><span data-stu-id="3d8e9-104">WebHooks is a lightweight HTTP pattern providing a simple pub/sub model for wiring together Web APIs and SaaS services.</span></span> <span data-ttu-id="3d8e9-105">サービスでイベントが発生すると、登録されたサブスクライバーに対して HTTP POST 要求の形式で通知が送信されます。</span><span class="sxs-lookup"><span data-stu-id="3d8e9-105">When an event happens in a service, a notification is sent in the form of an HTTP POST request to registered subscribers.</span></span> <span data-ttu-id="3d8e9-106">POST 要求には、イベントに関する情報が含まれています。これにより、受信側がそれに応じて動作できるようになります。</span><span class="sxs-lookup"><span data-stu-id="3d8e9-106">The POST request contains information about the event which makes it possible for the receiver to act accordingly.</span></span>

<span data-ttu-id="3d8e9-107">単純なので、 [Dropbox](http://dropbox.com/)、 [GitHub](https://www.github.com/)、 [Bitbucket](https://bitbucket.org/)、 [mailchimp](http://www.mailchimp.com/)、 [PayPal](http://www.paypal.com/)、[余裕](http://www.slack.com)、[ストライプ](http://www.stripe.com)、 [Trello](http://www.trello.com/)など、多数のサービスによって webhook が既に公開されています。</span><span class="sxs-lookup"><span data-stu-id="3d8e9-107">Because of their simplicity, WebHooks are already exposed by a large number of services including [Dropbox](http://dropbox.com/), [GitHub](https://www.github.com/), [Bitbucket](https://bitbucket.org/), [MailChimp](http://www.mailchimp.com/), [PayPal](http://www.paypal.com/), [Slack](http://www.slack.com), [Stripe](http://www.stripe.com), [Trello](http://www.trello.com/), and many more.</span></span> <span data-ttu-id="3d8e9-108">たとえば、WebHook は、 [Dropbox](http://dropbox.com/)でファイルが変更されたこと、またはコード変更が GitHub でコミットされたか、または[PayPal](http://www.paypal.com/)で支払いが開始されたか、または[Trello](http://www.trello.com/)でカードが作成されたことを示すことができます。</span><span class="sxs-lookup"><span data-stu-id="3d8e9-108">For example, a WebHook can indicate that a file has changed in [Dropbox](http://dropbox.com/), or a code change has been committed in GitHub, or a payment has been initiated in [PayPal](http://www.paypal.com/), or a card has been created in [Trello](http://www.trello.com/).</span></span> <span data-ttu-id="3d8e9-109">可能性は無限です。</span><span class="sxs-lookup"><span data-stu-id="3d8e9-109">The possibilities are endless!</span></span>

<span data-ttu-id="3d8e9-110">Microsoft ASP.NET Webhook を使用すると、ASP.NET アプリケーションの一部として Webhook を送受信することが簡単になります。</span><span class="sxs-lookup"><span data-stu-id="3d8e9-110">Microsoft ASP.NET WebHooks makes it easier to both send and receive WebHooks as part of your ASP.NET application:</span></span>

* <span data-ttu-id="3d8e9-111">受信側では、任意の数の WebHook プロバイダーから webhook を受信して処理するための共通のモデルが提供されます。</span><span class="sxs-lookup"><span data-stu-id="3d8e9-111">On the receiving side, it provides a common model for receiving and processing WebHooks from any number of WebHook providers.</span></span> <span data-ttu-id="3d8e9-112">[Dropbox](http://dropbox.com/)、 [GitHub](https://www.github.com/)、 [Bitbucket](https://bitbucket.org/)、 [mailchimp](http://www.mailchimp.com/)、 [PayPal](http://www.paypal.com/)、 [Pusher](http://www.pusher.com)、 [Salesforce](http://www.salesforce.com)、[余裕](http://www.slack.com)、[ストライプ](http://www.stripe.com)、 [Trello](http://www.trello.com/)、[WordPress](http://www.wordpress.com) 、 [Zendesk](https://www.zendesk.com/)のサポートが提供されていますが、さらにサポートを追加するのは簡単です。</span><span class="sxs-lookup"><span data-stu-id="3d8e9-112">It comes out of the box with support for [Dropbox](http://dropbox.com/), [GitHub](https://www.github.com/), [Bitbucket](https://bitbucket.org/), [MailChimp](http://www.mailchimp.com/), [PayPal](http://www.paypal.com/), [Pusher](http://www.pusher.com), [Salesforce](http://www.salesforce.com), [Slack](http://www.slack.com), [Stripe](http://www.stripe.com), [Trello](http://www.trello.com/),[WordPress](http://www.wordpress.com) and [Zendesk](https://www.zendesk.com/) but it is easy to add support for more.</span></span>

* <span data-ttu-id="3d8e9-113">送信側では、サブスクリプションの管理と保存、および適切なサブスクライバーのセットへのイベント通知の送信がサポートされています。</span><span class="sxs-lookup"><span data-stu-id="3d8e9-113">On the sending side it provides support for managing and storing subscriptions as well as for sending event notifications to the right set of subscribers.</span></span> <span data-ttu-id="3d8e9-114">これにより、サブスクライバーがサブスクライブできる独自のイベントセットを定義し、発生したときに通知を受け取ることができます。</span><span class="sxs-lookup"><span data-stu-id="3d8e9-114">This allows you to define your own set of events that subscribers can subscribe to and notify them when things happens.</span></span>

<span data-ttu-id="3d8e9-115">シナリオに応じて、2つの部分を組み合わせて使用することも、区別することもできます。</span><span class="sxs-lookup"><span data-stu-id="3d8e9-115">The two parts can be used together or apart depending on your scenario.</span></span> <span data-ttu-id="3d8e9-116">他のサービスから Webhook だけを受け取る必要がある場合は、受信側の部分のみを使用できます。他のユーザーが使用できるように Webhook を公開するだけの場合は、そのような操作を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="3d8e9-116">If you only need to receive WebHooks from other services then you can use just the receiver part; if you only want to expose WebHooks for others to consume, then you can do just that.</span></span>

<span data-ttu-id="3d8e9-117">このコードは ASP.NET Web API 2 と ASP.NET MVC 5 を対象としており、 [GitHub で OSS](https://github.com/aspnet/WebHooks)として入手できます。</span><span class="sxs-lookup"><span data-stu-id="3d8e9-117">The code targets ASP.NET Web API 2 and ASP.NET MVC 5 and is available as [OSS on GitHub](https://github.com/aspnet/WebHooks).</span></span>

## <a name="webhooks-overview"></a><span data-ttu-id="3d8e9-118">Webhook の概要</span><span class="sxs-lookup"><span data-stu-id="3d8e9-118">WebHooks Overview</span></span>

<span data-ttu-id="3d8e9-119">Webhook は、サービス間でどのように使用されるかが異なることを意味するパターンですが、基本的な考え方は同じです。</span><span class="sxs-lookup"><span data-stu-id="3d8e9-119">WebHooks is a pattern which means that it varies how it is used from service to service but the basic idea is the same.</span></span> <span data-ttu-id="3d8e9-120">Webhook は、他の場所で発生したイベントをユーザーがサブスクライブできる単純な pub/sub モデルと考えることができます。</span><span class="sxs-lookup"><span data-stu-id="3d8e9-120">You can think of WebHooks as a simple pub/sub model where a user can subscribe to events happening elsewhere.</span></span> <span data-ttu-id="3d8e9-121">イベント通知は、イベント自体に関する情報を含む HTTP POST 要求として伝達されます。</span><span class="sxs-lookup"><span data-stu-id="3d8e9-121">The event notifications are propagated as HTTP POST requests containing information about the event itself.</span></span>

<span data-ttu-id="3d8e9-122">通常、HTTP POST 要求には、webhook がトリガーするイベントに関する情報など、WebHook 送信者によって決定される JSON オブジェクトまたは HTML フォームデータが含まれます。</span><span class="sxs-lookup"><span data-stu-id="3d8e9-122">Typically the HTTP POST request contains a JSON object or HTML form data determined by the WebHook sender including information about the event causing the WebHook to trigger.</span></span> <span data-ttu-id="3d8e9-123">たとえば、 [GitHub](https://www.github.com/)からの WebHook POST 要求本文は、特定のリポジトリで新しい問題が開かれた結果として次のようになります。</span><span class="sxs-lookup"><span data-stu-id="3d8e9-123">For example, a WebHook POST request body from [GitHub](https://www.github.com/) looks like this as a result of a new issue being opened in a particular repository:</span></span>

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

<span data-ttu-id="3d8e9-124">WebHook が実際に意図された送信者からのものであることを確認するために、POST 要求は何らかの方法でセキュリティ保護され、受信側によって検証されます。</span><span class="sxs-lookup"><span data-stu-id="3d8e9-124">To ensure that the WebHook is indeed from the intended sender, the POST request is secured in some way and then verified by the receiver.</span></span> <span data-ttu-id="3d8e9-125">たとえば、 [GitHub webhook](https://developer.github.com/webhooks/)には、要求本文のハッシュを含む、*ハブ署名*HTTP ヘッダーが含まれています。これは、これを気にする必要がないため、受信側の実装によってチェックされます。</span><span class="sxs-lookup"><span data-stu-id="3d8e9-125">For example, [GitHub WebHooks](https://developer.github.com/webhooks/) includes an *X-Hub-Signature* HTTP header with a hash of the request body which is checked by the receiver implementation so you don't have to worry about it.</span></span>

<span data-ttu-id="3d8e9-126">通常、WebHook フローは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="3d8e9-126">The WebHook flow generally goes something like this:</span></span>

* <span data-ttu-id="3d8e9-127">WebHook 送信者は、クライアントがサブスクライブできるイベントを公開します。</span><span class="sxs-lookup"><span data-stu-id="3d8e9-127">The WebHook sender exposes events that a client can subscribe to.</span></span> <span data-ttu-id="3d8e9-128">イベントは、システムに対する監視可能な変更を記述します。たとえば、新しいデータ項目が挿入された場合、プロセスが完了したこと、その他の場合などです。</span><span class="sxs-lookup"><span data-stu-id="3d8e9-128">The events describe observable changes to the system, for example that a new data item has been inserted, that a process has completed, or something else.</span></span>

* <span data-ttu-id="3d8e9-129">WebHook 受信者は、次の4つの項目で構成される WebHook を登録することでサブスクライブします。</span><span class="sxs-lookup"><span data-stu-id="3d8e9-129">The WebHook receiver subscribes by registering a WebHook consisting of four things:</span></span>

     1. <span data-ttu-id="3d8e9-130">イベント通知を HTTP POST 要求の形式でポストする必要があるの URI。</span><span class="sxs-lookup"><span data-stu-id="3d8e9-130">A URI for where the event notification should be posted in the form of an HTTP POST request;</span></span>

     2. <span data-ttu-id="3d8e9-131">WebHook を発生させる必要がある特定のイベントを説明するフィルターのセット。</span><span class="sxs-lookup"><span data-stu-id="3d8e9-131">A set of filters describing the particular events for which the WebHook should be fired;</span></span>

     3. <span data-ttu-id="3d8e9-132">HTTP POST 要求に署名するために使用される秘密キー。</span><span class="sxs-lookup"><span data-stu-id="3d8e9-132">A secret key which is used to sign the HTTP POST request;</span></span>

     4. <span data-ttu-id="3d8e9-133">HTTP POST 要求に含まれる追加データ。</span><span class="sxs-lookup"><span data-stu-id="3d8e9-133">Additional data which is to be included in the HTTP POST request.</span></span> <span data-ttu-id="3d8e9-134">たとえば、HTTP POST 要求の本文に含まれる追加の HTTP ヘッダーフィールドまたはプロパティを使用できます。</span><span class="sxs-lookup"><span data-stu-id="3d8e9-134">This can for example be additional HTTP header fields or properties included in the HTTP POST request body.</span></span>

* <span data-ttu-id="3d8e9-135">イベントが発生すると、一致する WebHook 登録が検出され、HTTP POST 要求が送信されます。</span><span class="sxs-lookup"><span data-stu-id="3d8e9-135">Once an event happens, the matching WebHook registrations are found and HTTP POST requests are submitted.</span></span> <span data-ttu-id="3d8e9-136">通常、HTTP POST 要求の生成は、何らかの理由で受信者が応答していないか、HTTP POST 要求によってエラー応答が返された場合に、複数回再試行されます。</span><span class="sxs-lookup"><span data-stu-id="3d8e9-136">Typically, the generation of the HTTP POST requests are retried several times if for some reason the recipient is not responding or the HTTP POST request results in an error response.</span></span>

## <a name="webhooks-processing-pipeline"></a><span data-ttu-id="3d8e9-137">Webhook 処理パイプライン</span><span class="sxs-lookup"><span data-stu-id="3d8e9-137">WebHooks Processing Pipeline</span></span>

<span data-ttu-id="3d8e9-138">受信 webhook の Microsoft ASP.NET Webhook 処理パイプラインは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="3d8e9-138">The Microsoft ASP.NET WebHooks processing pipeline for incoming WebHooks looks like this:</span></span>

![ASP.NET Webhook 処理パイプライン](_static/WebHookReceivers.png)

<span data-ttu-id="3d8e9-140">ここでの2つの重要な概念は、*レシーバー*と*ハンドラー*です。</span><span class="sxs-lookup"><span data-stu-id="3d8e9-140">The two key concepts here are *Receivers* and *Handlers*:</span></span>

* <span data-ttu-id="3d8e9-141">*受信*側は、特定の送信者からの webhook の特定のフレーバーを処理し、セキュリティチェックを適用して、webhook 要求が実際に意図された送信者からのものであることを確認します。</span><span class="sxs-lookup"><span data-stu-id="3d8e9-141">*Receivers* are responsible for handling the particular flavor of WebHook from a given sender and for enforcing security checks to ensure that the WebHook request indeed is from the intended sender.</span></span>

* <span data-ttu-id="3d8e9-142">通常、*ハンドラー*は、ユーザーコードが特定の WebHook の処理を実行します。</span><span class="sxs-lookup"><span data-stu-id="3d8e9-142">*Handlers* are typically where user code runs processing the particular WebHook.</span></span>

<span data-ttu-id="3d8e9-143">次のノードでは、これらの概念について詳しく説明します。</span><span class="sxs-lookup"><span data-stu-id="3d8e9-143">In the following nodes these concepts are described in more details.</span></span>
