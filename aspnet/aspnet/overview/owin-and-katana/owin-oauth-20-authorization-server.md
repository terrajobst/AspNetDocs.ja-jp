---
uid: aspnet/overview/owin-and-katana/owin-oauth-20-authorization-server
title: OWIN OAuth 2.0 Authorization Server |Microsoft Docs
author: hongyes
description: このチュートリアルでは、OWIN OAuth ミドルウェアを使用して OAuth 2.0 承認サーバーを実装する方法について説明します。 これは、outlin のみを含む高度なチュートリアルです...
ms.author: riande
ms.date: 01/28/2019
ms.assetid: 20acee16-c70c-41e9-b38f-92bfcf9a4c1c
msc.legacyurl: /aspnet/overview/owin-and-katana/owin-oauth-20-authorization-server
msc.type: authoredcontent
ms.openlocfilehash: 39c78ee57f791a94af7a5fb66c3ac42d7239760f
ms.sourcegitcommit: b95316530fa51087d6c400ff91814fe37e73f7e8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/23/2019
ms.locfileid: "70000680"
---
# <a name="owin-oauth-20-authorization-server"></a><span data-ttu-id="af14d-104">OWIN OAuth 2.0 承認サーバー</span><span class="sxs-lookup"><span data-stu-id="af14d-104">OWIN OAuth 2.0 Authorization Server</span></span>

<span data-ttu-id="af14d-105">[OAuth 2.0 フレームワーク](http://tools.ietf.org/html/rfc6749)を使用すると、サードパーティのアプリで HTTP サービスへの制限付きアクセスを取得できます。</span><span class="sxs-lookup"><span data-stu-id="af14d-105">The [OAuth 2.0 framework](http://tools.ietf.org/html/rfc6749) enables a third-party app to obtain limited access to an HTTP service.</span></span> <span data-ttu-id="af14d-106">クライアントは、保護されたリソースにアクセスするためにリソース所有者の資格情報を使用するのではなく、アクセストークン (特定のスコープ、有効期間、およびその他のアクセス属性を示す文字列) を取得します。</span><span class="sxs-lookup"><span data-stu-id="af14d-106">Instead of using the resource owner's credentials to access a protected resource, the client obtains an access token (which is a string denoting a specific scope, lifetime, and other access attributes).</span></span> <span data-ttu-id="af14d-107">アクセストークンは、リソース所有者が承認された承認サーバーによってサードパーティクライアントに発行されます。</span><span class="sxs-lookup"><span data-stu-id="af14d-107">Access tokens are issued to third-party clients by an authorization server with the approval of the resource owner.</span></span>

<span data-ttu-id="af14d-108">OWIN は、.NET web サーバーと web アプリケーションの間の標準インターフェイスを定義します。</span><span class="sxs-lookup"><span data-stu-id="af14d-108">OWIN defines a standard interface between .NET web servers and web applications.</span></span> <span data-ttu-id="af14d-109">OWIN インターフェイスの目的は、サーバーとアプリケーションを分離し、.NET web 開発用の単純なモジュールの開発を奨励し、オープンスタンダードである .NET web 開発ツールのオープンソースエコシステムを強化することです。</span><span class="sxs-lookup"><span data-stu-id="af14d-109">The goal of the OWIN interface is to decouple server and application, encourage the development of simple modules for .NET web development, and, by being an open standard, stimulate the open source ecosystem of .NET web development tools.</span></span>

<span data-ttu-id="af14d-110">詳細については、「 [OWIN](http://owin.org/) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="af14d-110">For more information, see [OWIN](http://owin.org/)</span></span>
