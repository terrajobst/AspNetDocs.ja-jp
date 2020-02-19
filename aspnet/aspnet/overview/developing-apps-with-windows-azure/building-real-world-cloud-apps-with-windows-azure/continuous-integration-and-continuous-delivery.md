---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery
title: 継続的インテグレーションと継続的デリバリー (Azure を使用した実際のクラウドアプリの構築) |Microsoft Docs
author: MikeWasson
description: Azure 電子ブックを使用した実際のクラウドアプリの構築は、Scott Guthrie によって開発されたプレゼンテーションに基づいています。 13のパターンとベストプラクティスについて説明します。
ms.author: riande
ms.date: 06/12/2014
ms.assetid: eaece9f5-f80c-428b-b771-5db66d275b7d
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery
msc.type: authoredcontent
ms.openlocfilehash: cf3c65ef95528173eed3fb08984035b2512861c4
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457038"
---
# <a name="continuous-integration-and-continuous-delivery-building-real-world-cloud-apps-with-azure"></a>継続的インテグレーションと継続的デリバリー (Azure を使用した実際のクラウドアプリの構築)

[Mike Wasson](https://github.com/MikeWasson)、 [Rick Anderson](https://twitter.com/RickAndMSFT)、 [Tom Dykstra](https://github.com/tdykstra)

[修正 It プロジェクトをダウンロード](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)するか[、電子書籍をダウンロード](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)します

> Azure 電子ブック**を使用した実際のクラウドアプリの構築**は、Scott Guthrie によって開発されたプレゼンテーションに基づいています。 ここでは、クラウド用の web アプリの開発を成功させるのに役立つ13のパターンとプラクティスについて説明します。 電子書籍の詳細については、[最初の章](introduction.md)を参照してください。

最初の2つの推奨される開発プロセスパターンでは、[すべてのもの](automate-everything.md)と[ソース管理](source-control.md)が自動化され、3番目のプロセスパターンが統合されています。 継続的インテグレーション (CI) とは、開発者がコードをソースリポジトリにチェックインするたびに、ビルドが自動的にトリガーされることを意味します。 継続的デリバリー (CD) は、この1つの手順を実行します。ビルドと自動単体テストが成功した後、さらに詳細なテストを実行できる環境にアプリケーションを自動的にデプロイします。

クラウドでは、使用している環境リソースに対してのみ料金がかかるため、テスト環境の保守コストを最小限に抑えることができます。 CD プロセスでは、必要に応じてテスト環境をセットアップできます。テストが完了したら、環境をダウンさせることができます。

## <a name="continuous-integration-and-continuous-delivery-workflow"></a>継続的インテグレーションと継続的デリバリーのワークフロー

一般に、開発環境やステージング環境に継続的に配信することをお勧めします。 Microsoft でもほとんどのチームは、運用環境のデプロイのために手動のレビューと承認のプロセスを必要とします。 運用環境のデプロイでは、開発チームの主要なユーザーがサポートできるようになったとき、またはトラフィックの少ない期間中に発生したことを確認する必要があります。 しかし、開発およびテスト環境を完全に自動化して、開発者が変更をチェックインするだけで、環境が受け入れテスト用に設定されるようにすることはできません。

[継続的デリバリーに関する Microsoft のパターンとプラクティスに関する](https://aka.ms/ReleasePipeline)次の図は、一般的なワークフローを示しています。 イメージをクリックすると、元のコンテキストで完全なサイズが表示されます。

[継続的デリバリーワークフローの ![](continuous-integration-and-continuous-delivery/_static/image1.png)](https://msdn.microsoft.com/library/dn449955.aspx)

## <a name="how-the-cloud-enables-cost-effective-ci-and-cd"></a>クラウドがコスト効率の高い CI と CD を実現する方法

Azure では、これらのプロセスを簡単に自動化できます。 クラウド内ですべてを実行しているため、ビルドまたはテスト環境用のサーバーを購入または管理する必要はありません。 また、サーバーが使用可能になるまで待つ必要がありません。 実行するすべてのビルドで、自動化スクリプトを使用して Azure でテスト環境を作成したり、受け入れテストを実行したり、さらに詳細なテストを実行したりすることができます。 また、そのサーバーを2時間または8時間または1日のみ実行した場合は、コンピューターが実際に実行されている時間に対してのみ支払いを行うため、料金を支払う必要がある金額はごくわずかです。 たとえば、it アプリケーションを修正するために必要な環境では、1つのレベルから free レベルに移行すると、基本的に1時間あたり約1セントのコストがかかります。 1か月の間に、環境を一度に1時間だけ実行した場合、テスト環境では、スターバックスで購入した latte よりもコストがかかる可能性が高くなります。

## <a name="azure-devops-services"></a>Azure DevOps Services 

Azure DevOps Services には、展開計画からのアプリケーション開発に役立つさまざまな機能が用意されています。

- Git (distributed) と TFVC (集中型) の両方のソース管理がサポートされています。
- エラスティックビルドサービスを提供します。これは、必要なときにビルドサーバーを動的に作成し、完了後に停止することを意味します。 ソースコードの変更をだれかがチェックインしたときにビルドを自動的に開始することができます。また、アイドル状態になっている独自のビルドサーバーに対して割り当ておよび支払いを行う必要はありません。 ビルドサービスは、特定の数のビルドを超えない限り、無料です。 大量のビルドを実行することが予想される場合は、予約ビルドサーバーに対して少し追加料金を支払うことができます。
- Azure への継続的デリバリーをサポートしています。
- 自動ロードテストをサポートします。 ロードテストはクラウドアプリにとって非常に重要ですが、多くの場合、遅すぎるまで放置されています。 ロードテストでは、多数のユーザーによるアプリの大量使用をシミュレートし、アプリケーションを運用環境にリリースする前に、ボトルネックを見つけてスループットを向上させることができます。
- チームルームコラボレーションをサポートしています。これにより、小規模なアジャイルチームのリアルタイムコミュニケーションとコラボレーションが容易になります。
- アジャイルプロジェクト管理をサポートします。

Azure DevOps Services の継続的インテグレーションと継続的配信の機能の詳細については、 [Azure DevOps のドキュメント](/azure/devops/index)を参照してください。

ターンキープロジェクト管理、チームコラボレーション、およびソース管理ソリューションをお探しの場合は、「Azure DevOps Services」を参照してください。 [Azure DevOps Services](https://dev.azure.com/)でサインアップします。

## <a name="summary"></a>要約

最初の3つのクラウド開発パターンでは、反復可能で信頼性が高く、予測可能な開発プロセスを低サイクル時間で実装する方法について説明しました。 次の[章](web-development-best-practices.md)では、アーキテクチャとコーディングパターンについて説明します。

## <a name="resources"></a>リソース

詳細については、「 [Azure App Service での web アプリのデプロイ](https://azure.microsoft.com/documentation/articles/web-sites-deploy/)」を参照してください。

次のリソースも参照してください。

- [Team Foundation Server 2012 でリリースパイプラインをビルド](https://aka.ms/ReleasePipeline)します。 電子書籍、実践的なラボ、およびサンプル コードでは、Microsoft Patterns and Practices、継続的デリバリーの詳細な概要について説明します。 Visual Studio Lab Management と Visual Studio Release Management の使用について説明します。
- [ALM Rangers DevOps ツールとガイダンス](https://aka.ms/vsarsolutions/)。 ALM の Rangers では、TFS 2012 の DevOps &amp; Release Management の概念を理解し、タイヤを開始するための優れた方法として、DevOps ワークベンチサンプルコンパニオンソリューションを導入し、パターンとの共同作業についての実用的なガイダンスを*2012*&amp; しました。 このガイダンスでは、1回構築して複数の環境にデプロイする方法を示します。
- [Visual Studio 2012 を使用した継続的デリバリーのためのテスト](https://msdn.microsoft.com/library/jj159345.aspx)。 Microsoft のパターンとプラクティスによる電子書籍: 自動テストと継続的デリバリーを統合する方法について説明します。
- [Windowsazuredeploymenttracker](https://github.com/RyanTBerry/WindowsAzureDeploymentTracker)。 ビルドを TFS からキャプチャする (ラベルに基づいて) ツールのソースコード。ビルドしてパッケージ化し、DevOps ロール内のユーザーが特定の側面を構成して Azure にプッシュできるようにします。 ツールは、以前に展開されたバージョンに操作を "ロールバック" できるようにするために、展開プロセスを追跡します。 このツールには外部の依存関係がなく、TFS Api と Azure SDK を使用してスタンドアロンで機能できます。
- [継続的デリバリー: ビルド、テスト、および展開の自動化を通じて、信頼性の高いソフトウェアをリリース](https://www.amazon.com/Continuous-Delivery-Deployment-Automation-Addison-Wesley/dp/0321601912/ref=sr_1_1?s=books&amp;ie=UTF8&amp;qid=1377126361)します。 Book by Jez Humble。
- [リリース: 運用環境に対応したソフトウェアを設計して展開し](https://www.amazon.com/Release-It-Production-Ready-Pragmatic-Programmers/dp/0978739213)ます。 葛城 by Michael Nygard。

> [!div class="step-by-step"]
> [前へ](source-control.md)
> [次へ](web-development-best-practices.md)
