---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction
title: Azure を使用した実際のクラウドアプリの構築 |Microsoft Docs
author: MikeWasson
description: この電子書籍では、実際のクラウドソリューションを構築するためのパターンベースのアプローチについて説明します。 これらのパターンは、開発プロセスや...
ms.author: riande
ms.date: 06/12/2014
ms.assetid: accfa16a-ab15-4c26-9ad4-babdc2a77d2e
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction
msc.type: authoredcontent
ms.openlocfilehash: b88573b3702b755b155e8da35f5f8a67931bafc6
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78500650"
---
# <a name="building-real-world-cloud-apps-with-azure"></a>Azure を使用した実際のクラウドアプリの構築

[Mike Wasson](https://github.com/MikeWasson)、 [Rick Anderson](https://twitter.com/RickAndMSFT)、 [Tom Dykstra](https://github.com/tdykstra)

[修正 It プロジェクトをダウンロード](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)するか[、電子書籍をダウンロード](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)します

> この電子書籍では、実際のクラウドソリューションを構築するためのパターンベースのアプローチについて説明します。 パターンは、開発プロセスだけでなく、アーキテクチャとコーディングのプラクティスにも適用されます。
> 
> このコンテンツは、Scott Guthrie によって開発されたプレゼンテーションに基づいており、2013年6月 ([パート 1](http://vimeo.com/68215538)、[パート 2](http://vimeo.com/68215602)) で、ノルウェーの開発者のカンファレンス (NDC) によって提供されています。また、2013年9月 (パート[1](https://channel9.msdn.com/Events/TechEd/Australia/2013/AZR324)、パート[2](https://channel9.msdn.com/Events/TechEd/Australia/2013/AZR325)) の Microsoft Tech Ed オーストラリアで開催されています。 [他の多く](more-patterns-and-guidance.md#acknowledgments)は、ビデオから書面によるフォームへの移行中にコンテンツを更新し、強化しました。

## <a name="intended-audience"></a>対象ユーザー

クラウドの開発に関心を持っている開発者、クラウドへの移行を検討している開発者、またはクラウド開発の経験がない開発者には、知っておく必要がある最も重要な概念とベストプラクティスの簡潔な概要が記載されています。 概念については具体的な例を示し、各章は他のリソースにリンクして詳細な情報を参照しています。 この例とその他のリソースへのリンクは、Microsoft のフレームワークとサービスを対象としていますが、前述の原則は他の web 開発フレームワークやクラウド環境にも当てはまります。

クラウド用に既に開発している開発者にとっては、これを実現するためのアイデアをここで見つけることができます。 シリーズの各章は個別に読み取ることができるので、関心のあるトピックを選択して選択できます。

Scott Guthrie が*Azure プレゼンテーションを使用して実際のクラウドアプリを構築*し、詳細情報と更新情報を必要としている人はだれでもここで確認できます。

<a id="patterns"></a>
## <a name="cloud-development-patterns"></a>クラウド開発パターン

この電子書籍では、クラウド開発のための13の推奨パターンについて説明します。 ここでは、"Pattern" は、クラウドアプリの開発、設計、コーディングに関して最適な方法であることを意味するために、ここでは最も意味のある方法で使用されています。 これらは、次のような場合に、"成功のある pit に入る" のに役立つ鍵となるパターンです。

- [すべてを自動化](automate-everything.md)します。

    - スクリプトを使用すると、効率を最大化し、反復的なプロセスのエラーを最小限に抑えることができます。
    - デモ: Azure 管理スクリプト。
- [ソース管理](source-control.md)。 

    - DevOps ワークフローを容易にするために、ソース管理で分岐構造を設定します。
    - デモ: ソース管理にスクリプトを追加します。
    - デモ: ソース管理から機密データを保持します。
    - デモ: Visual Studio で Git を使用します。
- [継続的インテグレーションと継続的デリバリー](continuous-integration-and-continuous-delivery.md)。 

    - 各ソース管理チェックインでビルドと配置を自動化します。
- [Web 開発のベストプラクティス](web-development-best-practices.md)。 

    - Web 層のステートレスを保持します。
    - デモ: Azure App Service の Web Apps でのスケーリングと自動スケール。
    - セッション状態を回避します。
    - Cdn を使用できない場合は、フォールバックで CDN を使用します。
    - 非同期プログラミングモデルを使用します。
    - デモ: ASP.NET MVC と Entity Framework での非同期。
- [シングルサインオン](single-sign-on.md)。 

    - Azure Active Directory の概要。
    - デモ: Azure Active Directory を使用する ASP.NET アプリを作成します。
- [データ ストレージ オプション](data-storage-options.md)。 

    - データストアの種類。
    - 適切データストアを選択する方法。
    - デモ: Azure SQL Database します。
- [データのパーティション分割方法](data-partitioning-strategies.md)。 

    - リレーショナルデータベースのスケーリングを容易にするために、データを垂直方向、水平方向、または両方にパーティション分割します。
- [非構造化 blob ストレージ](unstructured-blob-storage.md)。 

    - Blob service を使用してクラウドにファイルを保存します。
    - デモ: It アプリを修正するには、blob storage を使用します。
- [障害が](design-to-survive-failures.md)発生した場合に備えて設計します。 

    - エラーの種類。
    - エラーのスコープ。
    - Sla について理解する。
- [監視とテレメトリ](monitoring-and-telemetry.md)。 

    - テレメトリアプリを購入し、アプリをインストルメント化するための独自のコードを作成する必要があるのはなぜですか。
    - デモ: Azure の新しい聖箱
    - デモ: It アプリを修正するためのコードをログに記録します。
    - デモ: It アプリを修正するための依存関係の挿入。
    - デモ: Azure での組み込みのログ記録のサポート。
- [一時的なエラー処理](transient-fault-handling.md)。 

    - スマートな再試行/バックオフロジックを使用して、一時的な障害の影響を軽減します。
    - デモ: Entity Framework 6 の再試行/バックオフ。
- [分散キャッシュ](distributed-caching.md)。 

    - 分散キャッシュを使用してスケーラビリティを向上させ、データベーストランザクションのコストを削減します。
- [キュー中心の作業パターン](queue-centric-work-pattern.md)。 

    - Web 層とワーカー層の疎結合により、高可用性を実現し、スケーラビリティを向上します。
    - デモ: It アプリを修正するための Azure storage キュー。
- [その他のクラウドアプリのパターンとガイダンス](more-patterns-and-guidance.md)。
- [付録: Fix It サンプル アプリケーション](the-fix-it-sample-application.md)

    - 既知の問題
    - ベスト プラクティス
    - ダウンロード、ビルド、実行、およびデプロイする方法。

これらのパターンはすべてのクラウド環境に適用されますが、Visual Studio、Team Foundation Service、ASP.NET、Azure などの Microsoft のテクノロジとサービスに基づく例を使用して説明します。

この章の残りの部分では、修正プログラムのサンプルアプリケーションと、It アプリを実行する Azure App Service クラウド環境での Web Apps について説明します。

<a id="fixit"></a>
## <a name="the-fix-it-sample-application"></a>Fix it サンプルアプリケーション

この電子書籍に示されているスクリーンショットとコード例のほとんどは、推奨されるクラウドアプリの開発パターンとプラクティスを示すために、最初に[Scott Guthrie](https://weblogs.asp.net/scottgu/)によって開発された修正プログラムの It アプリに基づいています。

![It アプリのホームページを修正する](introduction/_static/image1.png)

このサンプルアプリは、単純な作業項目のチケット発行システムです。 何か修正が必要な場合は、チケットを作成して他のユーザーに割り当てます。また、他のユーザーがログインし、割り当てられたチケットを確認し、作業が完了したときにチケットを完了としてマークすることができます。

これは、標準の Visual Studio web プロジェクトです。 ASP.NET MVC 上に構築され、SQL Server データベースを使用します。 IIS Express でローカルに実行し、Azure の Web サイトにデプロイしてクラウドで実行することができます。 フォーム認証とローカルデータベースを使用するか、Google などのソーシャルプロバイダーを使用してログインできます。 (後で、Active Directory 組織アカウントを使用してログインする方法についても説明します)。

![ログインページ](introduction/_static/image2.png)

ログインしたら、チケットを作成し、他のユーザーに割り当てて、修正が必要なものの画像をアップロードすることができます。

![修正するタスクを作成する](introduction/_static/image3.png)

![タスクが作成されたことを修正する](introduction/_static/image4.png)

作成した作業項目の進行状況を追跡し、自分に割り当てられているチケットを確認し、チケットの詳細を表示し、項目を完了済みとしてマークすることができます。

これは、機能の観点から見た非常に単純なアプリですが、何百万ものユーザーに拡張できるように構築する方法を説明しており、データベースの障害や接続の終了などに対する回復力があります。 また、自動化およびアジャイルな開発ワークフローを作成する方法についても説明します。これにより、開発サイクルを効率的かつ迅速に反復することで、簡単に開始し、アプリの品質を向上させることができます。

<a id="waws"></a>
## <a name="web-apps-in-azure-app-service"></a>Azure App Service の Web Apps

It アプリケーションの修正に使用されるクラウド環境は、Web サイトを呼び出す Azure のサービスです。 このサービスは、Vm を作成したり、IIS をインストールして構成したりすることなく、独自の web アプリを Azure でホストできるようにする方法です。Vm でサイトをホストし、バックアップと回復などのサービスを自動的に提供します。 Web サイトサービスは、ASP.NET、node.js、PHP、Python で動作します。 これにより、Visual Studio、Web 配置、FTP、Git、または TFS を使用してすばやくデプロイできます。 通常は、展開を開始してから、インターネット経由で更新プログラムを利用できるようになるまでに、わずか数秒で済みます。 これはすべて無料で開始でき、トラフィックの増加に合わせてスケールアップすることができます。

内部的には、Azure App Service の Web Apps は、独自の Vm で IIS を使用して Web サイトをホストする場合に自分で作成する必要がある、アーキテクチャのコンポーネントと機能を多数提供します。 1つのコンポーネントは、IIS を自動的に構成し、サイトの実行に必要な数の Vm にアプリケーションをインストールする展開エンドポイントです。

![展開サービス](introduction/_static/image5.png)

ユーザーは、web サイトにアクセスしたときに IIS Vm に直接ヒットすることはなく、[アプリケーション要求ルーティング処理 (ARR)](https://www.iis.net/downloads/microsoft/application-request-routing)のロードバランサーを経由します。 これらは独自のサーバーで使用できますが、ここでの利点は、自動的に設定されることです。 セッションアフィニティ、IIS のキューの深さ、各マシンの CPU 使用率などの要因を考慮して、web サイトをホストする Vm にトラフィックを送信するスマートヒューリスティックを使用します。

![ARR ロードバランサー](introduction/_static/image6.png)

マシンがダウンした場合、Azure はローテーションから自動的にそれをプルし、新しい VM インスタンスをスピンアップして、新しいインスタンスへのトラフィックの転送を開始します。アプリケーションのダウンタイムは発生しません。

![コンピューター障害からの自動回復](introduction/_static/image7.png)

これらはすべて自動的に行われます。 必要な作業は、web サイトを作成し、Windows PowerShell、Visual Studio、または Microsoft Azure 管理ポータルを使用してアプリケーションをデプロイすることだけです。

Visual Studio で web アプリケーションを作成し、それを Azure の Web サイトにデプロイする方法を説明する簡単で簡単なステップバイステップのチュートリアルについては、「 [azure と ASP.NET の概要](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/)」を参照してください。

<a id="summary"></a>
## <a name="summary"></a>まとめ

この概要では、本書に記載されているトピックの一覧、サンプルアプリケーションのスクリーンショット、Azure App Service クラウド環境での Web Apps の概要について説明しました。 とクラウド用のアプリを開発する大きな利点の1つは、テスト環境の作成や、コードのデプロイなど、反復的な開発タスクを簡単に自動化できることです。 その方法については、次の[章](automate-everything.md)で説明します。

## <a name="resources"></a>リソース

この章で説明しているトピックの詳細については、次のリソースを参照してください。

ドキュメント

- [Azure App Service で Web Apps](https://azure.microsoft.com/services/app-service/web/)ます。 Web Apps に関する Azure ドキュメントのポータルページです。
- [Web Apps、Cloud Services、Vm: どのような場合に使用するか。](https://azure.microsoft.com/documentation/articles/choose-web-site-cloud-service-vm/) この章で説明する WAWS は、Azure で web アプリを実行する3つの方法のうちの1つです。 この記事では、3つの方法の違いについて説明し、シナリオに適したものを選択する方法についてのガイダンスを示します。 Web サイトと同様に、Cloud Services は Azure の PaaS 機能です。 Vm は IaaS 機能です。 PaaS と IaaS の詳細については、「 [Data Options](data-storage-options.md#paasiaas) 」の章を参照してください。

ビデオ:

- [Scott Guthrie は、「手順 0-Azure クラウド OS とは」から開始します。](https://azure.microsoft.com/documentation/videos/what-is-the-cloud-os-scottgu/)
- [Web サイトのアーキテクチャ-Stefan が含ま](https://azure.microsoft.com/documentation/videos/why-azure-web-sites-plus-architecture/)れます。
- [Azure Websites 内部の Nir Mashkowski](https://channel9.msdn.com/Shows/Web+Camps+TV/Windows-Azure-Web-Sites-Internals-with-Nir-Mashkowski)。

> [!div class="step-by-step"]
> [Next](automate-everything.md)
