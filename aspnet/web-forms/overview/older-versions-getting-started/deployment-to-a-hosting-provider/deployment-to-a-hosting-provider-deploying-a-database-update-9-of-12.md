---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12
title: 'Visual Studio または Visual Web Developer を使用して SQL Server Compact で ASP.NET Web アプリケーションをデプロイする: データベースの更新をデプロイする-9/12 |Microsoft Docs'
author: tdykstra
description: この一連のチュートリアルでは、Visual Stu... を使用して SQL Server Compact データベースを含む ASP.NET web アプリケーションプロジェクトをデプロイ (発行) する方法について説明します。
ms.author: riande
ms.date: 11/17/2011
ms.assetid: a8d776af-4735-4612-87f6-9f326587f2d3
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12
msc.type: authoredcontent
ms.openlocfilehash: 3385e1019d9e7a9263fd9513c39b25eb85febbb5
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74582012"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-a-database-update---9-of-12"></a>Visual Studio または Visual Web Developer を使用した SQL Server Compact を使用した ASP.NET Web アプリケーションのデプロイ: データベース更新プログラムのデプロイ-9/12

[Tom Dykstra](https://github.com/tdykstra)

[スタートプロジェクトのダウンロード](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> この一連のチュートリアルでは、Visual Studio 2012 RC または Visual Studio Express 2012 RC for Web を使用して SQL Server Compact データベースを含む ASP.NET web アプリケーションプロジェクトをデプロイ (発行) する方法について説明します。 Web 発行の更新をインストールする場合は、Visual Studio 2010 を使用することもできます。 シリーズの概要については、[シリーズの最初のチュートリアル](deployment-to-a-hosting-provider-introduction-1-of-12.md)を参照してください。
> 
> Visual Studio 2012 の RC リリース後に導入された配置機能を示すチュートリアルについては、SQL Server Compact 以外の SQL Server のエディションをデプロイする方法、Azure App Service Web Apps にデプロイする方法については、「 [ASP.NET Web deployment Using Visual studio (Visual studio を使用した Web デプロイ](../../deployment/visual-studio-web-deployment/introduction.md)のデプロイ)」を参照してください。

## <a name="overview"></a>の概要

このチュートリアルでは、データベースの変更と関連するコードの変更を行い、Visual Studio で変更をテストして、テスト環境と運用環境の両方に更新プログラムを配置します。

リマインダー: チュートリアルを実行しているときにエラーメッセージが表示されたり機能しない場合は、必ず[トラブルシューティングのページ](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)を確認してください。

## <a name="adding-a-new-column-to-a-table"></a>テーブルへの新しい列の追加

このセクションでは、`Student` エンティティと `Instructor` エンティティの `Person` 基本クラスに生年月日列を追加します。 次に、インストラクターのデータを表示するページを更新して、新しい列が表示されるようにします。

*ContosoUniversity*プロジェクトで、 *Person.cs*を開き、次のプロパティを `Person` クラスの末尾に追加します (この後に2つの右中かっこが必要です)。

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample1.cs)]

次に、新しい列の値を提供するように、Seed メソッドを更新します。 *Migrations\ configuration.cs*を開き、`var instructors = new List<Instructor>` 開始するコードブロックを、生年月日の情報を含む次のコードブロックに置き換えます。

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample2.cs)]

ContosoUniversity プロジェクトで、*講師*を開き、生年月日を表示する新しいテンプレートフィールドを追加します。 入社年月日と office assignment の間に追加します。

[!code-aspx[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample3.aspx)]

(コードのインデントが同期されない場合は、CTRL + K キーを押してから CTRL + D キーを押してファイルを自動的に再フォーマットできます)。

ソリューションをビルドし、 **[パッケージマネージャーコンソール]** ウィンドウを開きます。 ContosoUniversity が**既定のプロジェクト**として選択されていることを確認します。

**パッケージマネージャーコンソール**ウィンドウで、**既定のプロジェクト**として **[ContosoUniversity]** を選択し、次のコマンドを入力します。

[!code-powershell[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample4.ps1)]

このコマンドが終了すると、Visual Studio によって新しい `DbMigration` クラスを定義するクラスファイルが開き、`Up` メソッドに新しい列を作成するコードが表示されます。

![AddBirthDate_migration_code](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image1.png)

ソリューションをビルドし、 **[パッケージマネージャーコンソール]** ウィンドウで次のコマンドを入力します (ContosoUniversity プロジェクトが選択されていることを確認します)。

[!code-powershell[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample5.ps1)]

コマンドが完了したら、アプリケーションを実行し、[インストラクター] ページを選択します。 ページが読み込まれると、[新しい生年月日] フィールドが表示されます。

[![Instructors_page_with_birth_date](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image3.png)](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image2.png)

## <a name="deploying-the-database-update-to-the-test-environment"></a>テスト環境へのデータベースの更新の配置

**ソリューションエクスプローラー** ContosoUniversity プロジェクトを選択します。

Web 上の **[発行**] ツールバーで、**テスト**発行プロファイルを選択し、 **[web の発行]** をクリックします。 (ツールバーが無効になっている場合は**ソリューションエクスプローラー**で ContosoUniversity プロジェクトを選択します)。

更新されたアプリケーションが Visual Studio によってデプロイされ、ブラウザーがホームページに表示されます。 インストラクターページを実行して、更新プログラムが正常に展開されたことを確認します。 アプリケーションがこのページのデータベースにアクセスしようとすると、Code First データベーススキーマが更新され、`Seed` メソッドが実行されます。 ページが表示されると、[予想される**誕生日**] 列に日付が含まれていることがわかります。

[![Instructors_page_with_birth_date_Test](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image5.png)](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image4.png)

## <a name="deploying-the-database-update-to-the-production-environment"></a>運用環境へのデータベースの更新の配置

これで、運用環境にデプロイできるようになりました。 唯一の違いは、 *app\_offline .htm*を使用して、ユーザーがサイトにアクセスできないようにし、変更を展開するときにデータベースを更新することです。 運用環境のデプロイでは、次の手順を実行します。

- *アプリ\_オフライン .htm*ファイルを実稼働サイトにアップロードします。
- Visual Studio で、 **Web サイトの 発行** ツールバーの 発行 をクリックし、 **web の発行** をクリックします。
- 運用サイトから、*アプリ\_のオフライン .htm*ファイルを削除します。

> [!NOTE]
> アプリケーションが運用環境で使用されている間は、バックアップ計画を実装する必要があります。 つまり、 *School-Prod*ファイルと*aspnet-Prod*ファイルを運用サイトから安全なストレージの場所に定期的にコピーする必要があり、そのようなバックアップをいくつか作成しておく必要があります。 データベースを更新するときは、変更の直前にからバックアップコピーを作成する必要があります。 これにより、間違いを犯しても、運用環境にデプロイするまで検出されない場合でも、データベースを破損する前の状態に復旧できます。

ブラウザーでホームページの URL を開くと、*アプリ\_offline*ページが表示されます。 *アプリ\_のオフライン .htm*ファイルを削除した後、もう一度ホームページを参照して、更新が正常に展開されたことを確認できます。

[![Instructors_page_with_birth_date_Prod](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image7.png)](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image6.png)

これで、テストと運用の両方にデータベースの変更を含むアプリケーションの更新が展開されました。 次のチュートリアルでは、SQL Server Compact から SQL Server Express と SQL Server にデータベースを移行する方法について説明します。

> [!div class="step-by-step"]
> [前へ](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12.md)
> [次へ](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12.md)
