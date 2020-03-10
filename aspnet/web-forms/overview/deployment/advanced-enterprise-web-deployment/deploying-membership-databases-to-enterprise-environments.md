---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/deploying-membership-databases-to-enterprise-environments
title: エンタープライズ環境へのメンバーシップデータベースの配置 |Microsoft Docs
author: jrjlee
description: このトピックでは、ASP.NET アプリケーションサービスデータベース (より一般的なもの) をプロビジョニングするときに対処する必要がある主な考慮事項と課題について説明します。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 3cf765df-d311-4f68-a295-c9685ceea830
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/deploying-membership-databases-to-enterprise-environments
msc.type: authoredcontent
ms.openlocfilehash: 50f49af502b75aa5ad52756a76a5e7340aca53f7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78422158"
---
# <a name="deploying-membership-databases-to-enterprise-environments"></a>エンタープライズ環境にメンバーシップ データベースを配置する

[Jason Lee](https://github.com/jrjlee)

[[Download PDF]\(PDF をダウンロード\)](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> このトピックでは、テスト環境、ステージング環境、または運用環境で ASP.NET アプリケーションサービスデータベース (一般にメンバーシップデータベースと呼ばれます) をプロビジョニングするときに対処する必要がある主な考慮事項と課題について説明します。 また、これらの課題に対応するために使用できる方法についても説明します。

このトピックでは、Fabrikam, Inc. という架空の企業のエンタープライズ展開要件に基づいて、一連のチュートリアルの一部を説明します。このチュートリアルシリーズでは、&#x2014; [Contact Manager ソリューション](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;のサンプルソリューションを使用して、ASP.NET MVC 3 アプリケーション、Windows Communication Foundation (WCF) サービス、データベースプロジェクトなど、現実的なレベルの複雑さを持つ web アプリケーションを表します。

これらのチュートリアルの中核となる配置方法は、「[プロジェクトファイルについ](../web-deployment-in-the-enterprise/understanding-the-project-file.md)て」で説明されている分割プロジェクトファイルアプローチに基づいています。この&#x2014;プロジェクトファイルには、ビルドプロセスは、すべての変換先環境に適用されるビルド命令を含む2つのプロジェクトファイルと、環境固有のビルドおよび配置設定を含んでいます。 ビルド時に、環境固有のプロジェクトファイルが環境に依存しないプロジェクトファイルにマージされ、ビルド命令の完全なセットが形成されます。

## <a name="what-are-the-issues-when-you-deploy-a-membership-database"></a>メンバーシップデータベースをデプロイする際の問題は何ですか。

ほとんどの場合、データベースの配置戦略を考案する際には、配置するデータを最初に考慮する必要があります。 開発環境またはテスト環境では、ユーザーアカウントデータを展開して、迅速かつ簡単なテストを容易にすることができます。 ステージング環境または運用環境では、ユーザーアカウントデータを展開することはほとんどありません。

残念ながら、ASP.NET メンバーシップデータベースでは、この決定をさらに複雑にするいくつかの問題が発生しています。

- スキーマのみの展開では、メンバーシップデータベースは操作不可能な状態のままになります。 これは、メンバーシップデータベースには、データベースが機能するために必要ないくつかの構成データ ( **aspnet\_SchemaVersions**テーブル) が含まれているためです。 そのため、ユーザーアカウントデータを除外するためにメンバーシップデータベースのスキーマのみのデプロイを実行する場合は、配置後スクリプトを実行して、必要な構成データを追加する必要があります。
- メンバーシップデータベースがどのように構成されているかによって、メンバーシッププロバイダーはコンピューターキーを使用してパスワードを暗号化し、データベースに格納することができます。 この場合、データベースと共に配置するすべてのユーザーアカウントデータは、移行先サーバーで使用できなくなります。 このため、ユーザーアカウントデータの展開はサポートされていないシナリオです。

## <a name="choosing-a-membership-database-strategy"></a>メンバーシップデータベース戦略の選択

エンタープライズサーバー環境でメンバーシップデータベースをプロビジョニングする方法を選択する際には、次のガイドラインを参考にしてください。

- 可能な限り、メンバーシップデータベースはデプロイしないでください。 代わりに、ターゲットデータベースサーバーでメンバーシップデータベースを手動で作成します。 メンバーシップデータベースのスキーマをカスタマイズしていない場合は、 [ASP.NET SQL Server 登録ツール (aspnet\_regsql)](https://msdn.microsoft.com/library/ms229862(v=vs.100).aspx)を使用して、宛先の本来に新しいものを作成するだけで済みます。
- オプションがなく、メンバーシップデータベース&#x2014;を配置する場合など、データベーススキーマ&#x2014;に対して広範な変更を行った場合は、メンバーシップデータベースのスキーマのみの配置を実行し、ユーザーアカウントデータを除外してから、配置後スクリプトを実行して必要な構成データを追加する必要があります。 これらのアプローチに関する広範なガイダンスについては[、「方法: ユーザーアカウントを含まない ASP.NET メンバーシップデータベースをデプロイする](https://msdn.microsoft.com/library/ff361972(v=vs.100).aspx)」を参照してください。

*メンバーシップデータベースのスキーマは、ほぼ静的である可能性が*あることに注意してください。 メンバーシップデータベースをカスタマイズした場合でも、スキーマを定期的&#x2014;に更新する必要はほとんどありませんが、web アプリケーションやデータベースプロジェクトのコードと同じ頻度で変更されることはありません。 そのため、自動または単一ステップのデプロイプロセスにメンバーシップデータベースを含める必要はありません。

## <a name="using-vsdbcmd-to-update-a-membership-database-schema"></a>VSDBCMD を使用してメンバーシップデータベーススキーマを更新する

最初の配置後にメンバーシップデータベースの構造を変更する場合は、インターネットインフォメーションサービス (IIS) Web 配置ツール (Web 配置) を使用してデータベースを再配置しないことをお勧めします。 Web 配置のデータベース配置機能には、転送先データベース&#x2014;に対して差分更新を行う機能は含まれません。データベースを削除してから再作成する必要があり Web 配置。 これは、既存のユーザーアカウントデータが失われることを意味します。これは通常、ステージング環境または運用環境では望ましくありません。

別の方法として、VSDBCMD ユーティリティを使用して、転送先データベースのスキーマを更新する方法があります。 VSDBCMD には、2つの重要な機能があります。 まず、既存のデータベースのスキーマを .dbschema ファイルにインポートできます。 2つ目の方法として、.dbschema ファイルを差分更新として既存のデータベースに配置できます。つまり、ターゲットデータベースを最新の状態にするために必要な変更のみが加えられ、データが失われることはありません。

次の大まかな手順を使用して、メンバーシップデータベーススキーマを更新できます。

1. VSDBCMD **Import**アクションを使用して、ソースメンバーシップデータベースの .dbschema ファイルを生成します。 この手順については、「[方法: コマンドプロンプトからスキーマをインポート](https://msdn.microsoft.com/library/dd172135.aspx)する」を参照してください。
2. VSDBCMD **deploy**アクションを使用して、対象のメンバーシップデータベースに .dbschema ファイルを配置します。 この手順については、「 [VSDBCMD のコマンドラインリファレンス」を参照してください。EXE (デプロイとスキーマのインポート)](https://msdn.microsoft.com/library/dd193283.aspx)。

## <a name="conclusion"></a>まとめ

このトピックでは、さまざまなターゲット環境で ASP.NET メンバーシップデータベースをプロビジョニングする必要がある場合に直面する可能性があるいくつかの課題について説明します。 特に、スキーマのみの展開では、メンバーシップデータベースが非運用状態のままになる理由と、ユーザーアカウントデータの展開がサポートされていない理由について説明しました。 このトピックでは、さまざまなシナリオでメンバーシップデータベースをプロビジョニング、デプロイ、および更新する方法についても説明しています。

## <a name="further-reading"></a>参考資料

VSDBCMD の使用方法の詳細なガイダンスと例については、「 [VSDBCMD のコマンドラインリファレンス」を参照してください。EXE (配置およびスキーマインポート)](https://msdn.microsoft.com/library/dd193283.aspx)と[方法: コマンドプロンプトからスキーマをインポート](https://msdn.microsoft.com/library/dd172135.aspx)します。 Aspnet\_使用してメンバーシップデータベースを作成する方法の詳細については、「 [ASP.NET SQL Server Registration Tool (aspnet\_regsql .exe)](https://msdn.microsoft.com/library/ms229862(v=vs.100).aspx)」を参照してください。 メンバーシップデータベースの配置に関する一般的なガイダンスについては、「[方法: ユーザーアカウントを含まない ASP.NET メンバーシップデータベースを配置](https://msdn.microsoft.com/library/ff361972(v=vs.100).aspx)する」を参照してください。

> [!div class="step-by-step"]
> [前へ](deploying-database-role-memberships-to-test-environments.md)
> [次へ](excluding-files-and-folders-from-deployment.md)
