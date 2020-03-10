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
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78500236"
---
# <a name="owin-oauth-20-authorization-server"></a>OWIN OAuth 2.0 承認サーバー

[OAuth 2.0 フレームワーク](http://tools.ietf.org/html/rfc6749)を使用すると、サードパーティのアプリで HTTP サービスへの制限付きアクセスを取得できます。 クライアントは、保護されたリソースにアクセスするためにリソース所有者の資格情報を使用するのではなく、アクセストークン (特定のスコープ、有効期間、およびその他のアクセス属性を示す文字列) を取得します。 アクセストークンは、リソース所有者が承認された承認サーバーによってサードパーティクライアントに発行されます。

OWIN は、.NET web サーバーと web アプリケーションの間の標準インターフェイスを定義します。 OWIN インターフェイスの目的は、サーバーとアプリケーションを分離し、.NET web 開発用の単純なモジュールの開発を奨励し、オープンスタンダードである .NET web 開発ツールのオープンソースエコシステムを強化することです。

詳細については、「 [OWIN](http://owin.org/) 」を参照してください。
