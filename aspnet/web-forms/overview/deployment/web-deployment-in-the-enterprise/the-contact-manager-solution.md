---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/the-contact-manager-solution
title: Contact Manager ソリューション |Microsoft Docs
author: jrjlee
description: この一連のチュートリアルでは、Contact&#x2014;Manager ソリューション&#x2014;のサンプルソリューションを使用して、現実的な leve を持つエンタープライズ規模のアプリケーションを表します。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 4d8c8d19-055b-4b70-9ee1-f748f0db3a01
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/the-contact-manager-solution
msc.type: authoredcontent
ms.openlocfilehash: 12ed7827f7392e559e04121386f7cd045de8462b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78473812"
---
# <a name="the-contact-manager-solution"></a>連絡先マネージャー ソリューション

[Jason Lee](https://github.com/jrjlee)

[[Download PDF]\(PDF をダウンロード\)](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> この[一連のチュートリアル](web-deployment-in-the-enterprise.md)では、Contact&#x2014;Manager ソリューション&#x2014;のサンプルソリューションを使用して、現実的なレベルの複雑さを持つエンタープライズ規模のアプリケーションを表します。 このトピックでは、Contact Manager ソリューションについて説明し、ソリューションの主要なコンポーネントについて説明します。また、この種のアプリケーションをエンタープライズ環境のさまざまな移行先プラットフォームに展開する際の課題を示します。
> 
> これらのチュートリアルのトピックを参照しながら、連絡先マネージャーソリューションを参照の実装として使用して、エンタープライズ展開シナリオで特定の課題を満たす方法を示すことができます。 次のトピック「 [Contact Manager ソリューションの設定](setting-up-the-contact-manager-solution.md)」では、開発者のワークステーションでソリューションをダウンロードして実行する方法について説明します。

## <a name="solution-overview"></a>ソリューションの概要

Contact Manager ソリューションは、次の4つのプロジェクトで構成されています。

![](the-contact-manager-solution/_static/image1.png)

- **Contactmanager. Mvc**。 これは、ソリューションのエントリポイントを表す ASP.NET MVC 3 web アプリケーションプロジェクトです。 これには、ユーザーが連絡先の詳細を作成して表示できるようにするなど、基本的な web アプリケーション機能がいくつか用意されています。 アプリケーションは、Windows Communication Foundation (WCF) サービスを利用して連絡先と ASP.NET アプリケーションサービスデータベースを管理し、認証と承認を管理します。
- **Contactmanager. データベース**。 これは、Visual Studio データベースプロジェクトです。 プロジェクトでは、連絡先の詳細を格納するデータベースのスキーマを定義します。
- **Contactmanager. サービス**。 これは、WCF web サービスプロジェクトです。 WCF サービスは、呼び出し元が**Contactmanager**データベースに対して作成、取得、更新、削除 (CRUD) 操作を実行できるようにするエンドポイントを公開します。 サービスは、 **contactmanager**データベースと**Contactmanager. 共通 .dll**アセンブリに依存しています。
- **Contactmanager. 共通**。 これはクラスライブラリプロジェクトです。 WCF サービスは、このアセンブリで定義されている型に依存しています。

このソリューションには、Publish という名前のソリューションフォルダーも含まれています。 これには、ビルドおよび配置プロセスを制御および操作する方法を示すさまざまなカスタムプロジェクトファイルとコマンドファイルが含まれています。 これらの詳細については、このチュートリアルの後半で詳しく説明します。

概念レベルでは、ソリューションのコンポーネントは次のようにまとめられます。

![](the-contact-manager-solution/_static/image2.png)

> [!NOTE]
> ASP.NET MVC 3 web アプリケーションは ASP.NET メンバーシッププロバイダーを使用しますが、web アプリケーション内のすべてのページで匿名アクセスが許可されます。 これは、現実的な構成ではありません。 ただし、この方法でソリューションをセットアップすることで、ユーザーアカウントとロールを構成しなくても、ソリューションの配置とテストを容易に行えるようになります。

## <a name="deployment-challenges"></a>デプロイの課題

Contact Manager ソリューションは、多くのエンタープライズ展開シナリオに共通するいくつかの展開の課題を示しています。

- ソリューションは、複数の依存プロジェクトで構成されています。 これらのプロジェクトを同時に配置する必要があります。
- 接続文字列とサービスエンドポイントは、環境ごとに更新する必要があります。多くの場合、この情報を開発者が使用することはできません。
- **Contactmanager**データベースをステージング環境と運用環境に配置する場合は、以降の配置で既存のデータを保持する必要があります。
- ASP.NET アプリケーションサービスデータベースを展開する場合は、一部の構成データを展開する必要がありますが、ユーザーアカウントデータは省略します。
- プロジェクトには、配置すべきではないファイルとフォルダーが含まれています。 これらのファイルとフォルダーを展開プロセスから除外する必要があります。
- ソリューションでは、Team Foundation Server (TFS) ビルドサーバーからの自動化された配置をサポートする必要があります。

## <a name="conclusion"></a>まとめ

このトピックでは、Contact Manager ソリューションの概要について説明し、多数のエンタープライズ展開シナリオに共通する展開上のいくつかの課題を特定しました。 このチュートリアルの残りのトピックでは、これらの課題に対応するために使用できるいくつかの手法について説明します。

次のトピック「 [Contact Manager ソリューションの設定](setting-up-the-contact-manager-solution.md)」では、開発者のワークステーションでソリューションをダウンロードして実行する方法について説明します。

> [!div class="step-by-step"]
> [前へ](web-deployment-in-the-enterprise.md)
> [次へ](setting-up-the-contact-manager-solution.md)
