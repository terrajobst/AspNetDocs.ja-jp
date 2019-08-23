---
uid: overview
title: ASP.NET の概要 |Microsoft Docs
author: rick-anderson
description: ASP.NET、web サイト、web アプリケーション、および web API を作成するための無償のフレームワークを紹介します。
ms.assetid: 3a309468-f1ca-4e51-b9c3-536af79d7a8b
ms.author: riande
ms.date: 08/10/2019
msc.legacyurl: ''
msc.type: content
ms.openlocfilehash: 9a6d08849f09c9d7a779df64f70e8770d2af3c87
ms.sourcegitcommit: b67ffd5b2c5cff01ec4c8eb12a21f693f2e11887
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/23/2019
ms.locfileid: "69995285"
---
# <a name="aspnet-overview"></a>ASP.NET 概要

ASP.NET は、HTML、CSS、および JavaScript を使用して優れた web サイトや web アプリケーションを構築するための無料の web フレームワークです。 Web API を作成し、Web ソケットなどのリアルタイム テクノロジを使用できます。

[ASP.NET Core](https://docs.microsoft.com/aspnet/core/)は ASP.NET の代替です。  [ASP.NET と ASP.NET Core の選択方法に関するガイダンス](https://docs.microsoft.com/aspnet/core/choose-aspnet-framework) を参照してください。

## <a name="get-started"></a>作業開始

ASP.NET on Windows の無料の IDE [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community edition をインストールしてください。

## <a name="websites-and-web-applications"></a>Web サイトと web アプリケーション

 ASP.NET は、web アプリケーションを作成するための3つのフレームワークを提供します。Web フォーム、ASP.NET MVC、および ASP.NET Web ページ。 この3つのフレームワークはすべて安定して成熟しており、いずれのフレームワークでも優れた web アプリケーションを作成できます。 どのようなフレームワークを選択しても、どこにいても ASP.NET のすべての利点と機能が得られます。

各フレームワークは、別の開発スタイルを対象としています。 どちらを選択するかは、プログラミングアセット (知識、スキル、および開発エクスペリエンス) の組み合わせ、作成するアプリケーションの種類、および使い慣れた開発アプローチによって異なります。

各フレームワークの概要と、それらを選択する方法に関するいくつかのアイデアを以下に示します。 ビデオの概要については、「 [ASP.NET を使用した Web サイトの作成](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/Making-Websites-with-ASPNET)」および「 [Web ツールとは](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/what-is-web-tools)」を参照してください。

|   | の経験がある場合 | 開発スタイル | 家 |
|-----------|----------------------|-----------------------------------------------------|----------------|
| Web フォーム | Win フォーム、WPF、.NET | HTML マークアップをカプセル化するコントロールの豊富なライブラリを使用した迅速な開発 | ミッドレベル、高度な RAD |
| MVC       | Ruby on Rails、.NET  | HTML マークアップ、コードとマークアップの分離、およびテストの記述を簡単に行うことができます。 モバイルアプリケーションとシングルページアプリケーション (SPA) に最適な選択肢です。 | ミッドレベル、詳細 |
| Web ページ  | Classic ASP、PHP     | 同じファイル内の HTML マークアップとコードの組み合わせ | 新規、中間レベル |

### <a name="web-forms"></a>Web フォーム

ASP.NET Web フォームを使用すると、使い慣れたドラッグアンドドロップのイベントドリブンモデルを使用して、動的な web サイトを構築できます。 デザインサーフェイスと数百のコントロールやコンポーネントを使用すると、データアクセスを使用して高度で強力な UI 駆動型サイトをすばやく構築できます。

[Web フォームについての詳細情報](web-forms/index.md)

### <a name="mvc"></a>MVC

ASP.NET MVC には、動的な web サイトを構築するための強力なパターンベースの方法が用意されています。これにより、問題を明確に分離し、アジャイル開発のためのマークアップを完全に制御できます。 ASP.NET MVC には、最新の web 標準を使用する高度なアプリケーションを作成するための、TDD に適した迅速な開発を可能にする多くの機能が含まれています。

[MVC の詳細情報](mvc/index.md)

### <a name="aspnet-web-pages"></a>ASP.NET Web ページ

ASP.NET Web ページと Razor 構文は、サーバーコードと HTML を組み合わせて動的な Web コンテンツを作成するための高速でわかりやすく、軽量な方法を提供します。 データベースに接続し、ビデオを追加し、ソーシャルネットワーキングサイトにリンクします。また、最新の web 標準に準拠した美しいサイトの作成に役立つ多くの機能が追加されています。

[Web ページについての詳細情報](web-pages/index.md)

### <a name="notes-about-web-forms-mvc-and-web-pages"></a>Web フォーム、MVC、および Web ページに関する注意事項

3つの ASP.NET フレームワークはすべて、.NET と ASP.NET の .NET Framework と共有のコア機能をベースとしています。 たとえば、3つのすべてのフレームワークでは、メンバーシップに基づいたログインセキュリティモデルが提供されます。また、3つすべては、コア ASP.NET 機能の一部である要求の管理、セッションの処理などのために同じ機能を共有します。

また、3つのフレームワークは完全に独立しているわけではなく、どちらを選択しても、別のフレームワークを使用することはできません。 フレームワークは同じ web アプリケーション内に共存できるため、異なるフレームワークを使用して記述されたアプリケーションの個々のコンポーネントを確認することは珍しくありません。 たとえば、データ アクセスと管理の部分はデータ コントロールと単純なデータ アクセスを活用するために Web フォームで開発中に、マークアップを最適化するために MVC アプリの顧客向けの部分を開発する可能性があります。

## <a name="web-apis"></a>Web API

ASP.NET Web API は、ブラウザーやモバイルデバイスを含む広範なクライアントに接続できる HTTP サービスを簡単に構築できるフレームワークです。 ASP.NET Web API は、.NET Framework に基づいて RESTful アプリケーションを構築するのに最適なプラットフォームです。

[Web API についての詳細情報](web-api/index.md)

<!-- Put first under Web API TOC:  Watch video (9 minutes) https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/services-and-aspnet -->

## <a name="real-time-technologies"></a>リアルタイムテクノロジ

ASP.NET SignalR は、リアルタイム web 機能の開発を容易にする ASP.NET 開発者向けの新しいライブラリです。 SignalR を使用すると、サーバーとクライアント間で双方向通信を行うことができます。 サーバーは、使用可能になったらすぐに、接続されているクライアントにコンテンツをプッシュできます。 SignalR は Web ソケットをサポートしており、以前のブラウザーと互換性のある他の手法にフォールバックします。 SignalR には接続管理用の API が含まれています (接続し、切断イベントなど)、接続、および承認をグループ化します。

[SignalR についての詳細情報](signalr/index.md)

<!-- Put first under SignalR TOC:  Watch video (6 minutes) https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/signalr-and-the-real-time-web -->

## <a name="mobile-apps-and-sites"></a>モバイルアプリとサイト

ASP.NET では、Web API バックエンドを使用してネイティブモバイルアプリを作成できます。また、Twitter ブートストラップなどの応答性の高い設計フレームワークを使用してモバイル Web サイトを作成することもできます。 ネイティブモバイルアプリを構築している場合は、アプリのデータアクセス、認証、およびプッシュ通知を処理するための JSON ベースの Web API を簡単に作成できます。 応答性の高いモバイルサイトを構築する場合は、任意の CSS フレームワークを使用するか、好みのグリッドシステムを開くか、jQuery Mobile や Sencha などの強力なモバイルシステムと PhoneGap を使用した優れたモバイルアプリケーションを選択することができます。

[モバイルアプリとサイト開発の詳細情報](mobile/index.md)

<!-- Put first under mobile TOC:  Watch video (11 minutes) https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/aspnet-and-mobile -->

## <a name="single-page-applications"></a>シングルページアプリケーション

ASP.NET Single Page Application (SPA) を使用すると、HTML 5、CSS 3、および JavaScript を使用したクライアント側の重要な相互作用を含むアプリケーションを構築できます。 Visual Studio には、ノックアウトと ASP.NET Web API を使用してシングルページアプリケーションを構築するためのテンプレートが含まれています。 組み込みの SPA テンプレートに加えて、コミュニティによって作成された SPA テンプレートをダウンロードすることもできます。

[シングルページアプリの開発についての詳細情報](single-page-application/index.md)

## <a name="webhooks"></a>Web フック

Webhook は、Web API と SaaS サービスをまとめて配線の単純なパブリッシュ/サブスクライブ モデルを提供する軽量な HTTP パターンです。 サービスでイベントが発生すると、登録されたサブスクライバーに対して HTTP POST 要求の形式で通知が送信されます。 POST 要求には、イベントに関する情報が含まれています。これにより、受信側がそれに応じて動作できるようになります。

Webhook は、Dropbox、GitHub、Instagram、MailChimp、PayPal、余裕、Trello など、多数のサービスによって公開されています。 たとえば、WebHook は、Dropbox でファイルが変更されたこと、またはコード変更が GitHub でコミットされたか、または PayPal で支払いが開始されたか、または Trello でカードが作成されたことを示すことができます。

[Webhook に関する詳細情報](webhooks/index.md)

<!--
Create Deployment TOC based on https://www.asp.net/aspnet/overview/deployment
Copy deployment content map to MVC, WebForms, Web Pages, Web API sections.
Copy Web Deployment in Enterprise from WebForms to MVC
Move under ASP.NET Best practices
    What not to do in ASP.NET, and what to do instead https://review.docs.microsoft.cus/aspnet/aspnet/overview/web-development-best-practices/what-not-to-do-in-aspnet-and-what-to-do-instead
    Async and await https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/async-and-await
    Building Real World Cloud Apps with Azure https://review.docs.microsoft.com/aspnet/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction
    Hands on Lab: Maintainable Azure Websites: Managing Change and Scale https://review.docs.microsoft.com/aspnet/aspnet/overview/developing-apps-with-windows-azure/maintainable-azure-websites-managing-change-and-scale

-->
