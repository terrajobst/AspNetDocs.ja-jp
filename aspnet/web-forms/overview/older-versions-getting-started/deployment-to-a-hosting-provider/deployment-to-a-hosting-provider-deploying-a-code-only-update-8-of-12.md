---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12
title: 'Visual Studio または Visual Web Developer を使用して SQL Server Compact で ASP.NET Web アプリケーションをデプロイする: コードのみの更新プログラムをデプロイする-8/12 |Microsoft Docs'
author: tdykstra
description: この一連のチュートリアルでは、Visual Stu... を使用して SQL Server Compact データベースを含む ASP.NET web アプリケーションプロジェクトをデプロイ (発行) する方法について説明します。
ms.author: riande
ms.date: 11/17/2011
ms.assetid: ddf6252f-9413-4c0c-a360-2cef8d231717
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12
msc.type: authoredcontent
ms.openlocfilehash: e4d094ef84a747c36ce05ddb0e3d1ce0391d5605
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78455074"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-a-code-only-update---8-of-12"></a>Visual Studio または Visual Web Developer を使用した SQL Server Compact を使用した ASP.NET Web アプリケーションのデプロイ: コードのみの更新プログラムのデプロイ-8/12

[Tom Dykstra](https://github.com/tdykstra)

[スタートプロジェクトのダウンロード](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> この一連のチュートリアルでは、Visual Studio 2012 RC または Visual Studio Express 2012 RC for Web を使用して SQL Server Compact データベースを含む ASP.NET web アプリケーションプロジェクトをデプロイ (発行) する方法について説明します。 Web 発行の更新をインストールする場合は、Visual Studio 2010 を使用することもできます。 シリーズの概要については、[シリーズの最初のチュートリアル](deployment-to-a-hosting-provider-introduction-1-of-12.md)を参照してください。
> 
> Visual Studio 2012 の RC リリース後に導入された配置機能を示すチュートリアルについては、SQL Server Compact 以外の SQL Server のエディションをデプロイする方法、Azure App Service Web Apps にデプロイする方法については、「 [ASP.NET Web deployment Using Visual studio (Visual studio を使用した Web デプロイ](../../deployment/visual-studio-web-deployment/introduction.md)のデプロイ)」を参照してください。

## <a name="overview"></a>概要

最初のデプロイの後、web サイトの保守と開発の作業が継続し、その前に更新プログラムを展開する必要があります。 このチュートリアルでは、アプリケーションコードに更新プログラムをデプロイするプロセスについて順を追って紹介します。 この更新プログラムには、データベースの変更は含まれません。次のチュートリアルでは、データベースの変更を配置する場合の違いについて説明します。

リマインダー: チュートリアルを実行しているときにエラーメッセージが表示されたり機能しない場合は、必ず[トラブルシューティングのページ](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)を確認してください。

## <a name="making-a-code-change"></a>コード変更の作成

アプリケーションの更新の簡単な例として **、インストラクターのページに**、選択したインストラクターが担当するコースの一覧を追加します。

**インストラクター**ページを実行すると、グリッドに**選択**リンクがあることがわかりますが、行の背景を灰色にする以外には何も行われません。

[![Instructors_page](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image1.png)

次に、 **[選択]** リンクがクリックされたときに実行されるコードを追加します。選択したインストラクターによって担当されるコースの一覧が表示されます。

*講師*の**ErrorMessageLabel** `Label` コントロールの直後に、次のマークアップを追加します。

[!code-aspx[Main](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/samples/sample1.aspx)]

ページを実行し、インストラクターを選択します。 インストラクターがトレーニングしたコースの一覧が表示されます。

[![Instructors_page_with_courses](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image3.png)

## <a name="deploying-the-code-update-to-the-test-environment"></a>テスト環境へのコード更新の配置

テスト環境への配置は、ワンクリックでの発行をもう一度実行するだけの簡単な方法です。 この処理をより迅速に行うために、 **Web One の [発行**] ツールバーを使用できます。

**[表示]** メニューの **[ツールバー]** をクリックし、[ **Web One] をクリック**します。

![Selecting_One_Click_Publish_toolbar](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image5.png)

**ソリューションエクスプローラー**で、ContosoUniversity プロジェクトを選択します。

**web で [発行**] ツールバーをクリックし、**テスト**発行プロファイルを選択して、 **[web の発行]** をクリックします (矢印が左と右にあるアイコン)。

![Web_One_Click_Publish_toolbar](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image6.png)

Visual Studio によって更新されたアプリケーションが配置され、ブラウザーが自動的にホームページに表示されます。 インストラクターページを実行し、インストラクターを選択して、更新が正常に展開されたことを確認します。

[![Instructors_page_with_courses_Test](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image8.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image7.png)

通常は回帰テストも行います (つまり、サイトの他の部分をテストして、新しい変更によって既存の機能が破壊されていないことを確認します)。 ただし、このチュートリアルでは、この手順をスキップして、運用環境への更新プログラムの展開に進みます。

## <a name="preventing-redeployment-of-the-initial-database-state-to-production"></a>初期データベースの状態を運用環境に再展開できないようにする

実際のアプリケーションでは、初期デプロイ後にユーザーが運用サイトと対話し、データベースにライブデータが入力されます。 そのため、メンバーシップデータベースを初期状態で再デプロイする必要はありません。これにより、すべてのライブデータが消去されます。 SQL Server Compact データベースは*app\_data*フォルダー内のファイルなので、*アプリの\_データ*フォルダー内のファイルが展開されないように配置設定を変更することで、これを回避する必要があります。

ContosoUniversity プロジェクトの**プロジェクトプロパティ**ウィンドウを開き、 **[パッケージ化/発行]** タブを選択します。 **[構成]** ドロップダウンボックスに **[アクティブ (リリース)]** または **[リリース]** が選択されていることを確認し、[**アプリ\_データフォルダーからファイルを除外**する] を選択します。

![Exclude_files_from_the_App_Data_folder](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image9.png)

デバッグビルドを後で配置する場合は、デバッグビルド構成に対して同じ変更を行うことをお勧めします。 **[構成]** を **[デバッグ]** に変更し、[**アプリ\_データフォルダーからファイルを除外**する] を選択します。

**[パッケージ/発行 Web]** タブを保存して閉じます。

> [!NOTE] 
> 
> [!IMPORTANT]
> 発行プロファイルで **ターゲットに追加ファイルを削除**しない。 このオプションを選択すると、展開プロセスによって、展開されたサイトの [アプリ\_データ] にあるデータベースが削除され、アプリ\_データフォルダー自体が削除されます。

## <a name="preventing-user-access-to-the-production-site-during-update"></a>更新中に運用サイトへのユーザーアクセスを防止する

ここでデプロイしている変更は、1つのページに単純に変更されます。 ただし、展開が完了する前にユーザーがページを要求すると、サイトの動作が変更される場合があります。 これを回避するには、*アプリ\_のオフライン .htm*ファイルを使用します。 アプリケーションのルートフォルダーに*app\_offline .htm*という名前のファイルを配置すると、アプリケーションを実行する代わりに IIS によってそのファイルが自動的に表示されます。 そのため、デプロイ中にアクセスできないようにするには、*アプリ\_offline .htm*をルートフォルダーに配置し、展開プロセスを実行してから、 *app\_offline. .htm*を削除します。

**ソリューションエクスプローラー**で、(プロジェクトの1つではなく) ソリューションを右クリックし、 **[新しいソリューションフォルダー]** を選択します。

![Creating_a_solution_folder](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image10.png)

フォルダーに「 *Solutionfiles*」という名前を指定します。

新しいフォルダーで、 *app\_offline. .htm*という名前の HTML ページを作成します。 既存の内容を次のマークアップに置き換えます。

[!code-html[Main](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/samples/sample2.html)]

FTP 接続またはホスティングプロバイダーのコントロールパネルにある**ファイルマネージャー**ユーティリティを使用して、*アプリケーション\_offline .htm*ファイルをサイトにコピーできます。 このチュートリアルでは、**ファイルマネージャー**を使用します。

コントロールパネルを開き、「[運用環境にデプロイする](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)」チュートリアルで行ったように **[ファイルマネージャー]** を選択します。 アプリケーションのルートフォルダーを取得するには、 **[contosouniversity.com]** 、 **[wwwroot]** の順に選択し、 **[アップロード]** をクリックします。

[![Upload_button_in_File_Manager](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image12.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image11.png)

**[ファイルのアップロード]** ダイアログボックスで、*アプリ\_offline .htm*ファイルを選択し、 **[アップロード]** をクリックします。

[![Upload_dialog_box_in_File_Manager](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image14.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image13.png)

目的のサイトの URL に移動します。 ホームページの代わりに、*アプリ\_offline .htm*ページが表示されるようになります。

[![App_offline。 htm_page_in_production](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image16.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image15.png)

これで、運用環境にデプロイする準備ができました。

## <a name="deploying-the-code-update-to-the-production-environment"></a>運用環境へのコード更新の配置

Web 上の **[発行**] ツールバーで、 **[実稼働]** 発行プロファイル を選択し、 **[web の発行]** をクリックします。

更新されたアプリケーションが Visual Studio によって展開され、ブラウザーが開き、サイトのホームページが表示されます。 *アプリ\_のオフライン .htm*ファイルが表示されます。 展開が成功したことを確認するためにテストする前に、*アプリ\_のオフライン .htm*ファイルを削除する必要があります。

コントロールパネルの **[ファイルマネージャー]** アプリケーションに戻ります。 **Contosouniversity.com**と**wwwroot**を選択し、[ **app\_offline .htm**] を選択して、 **[削除]** をクリックします。

[![Deleting_app_offline .htm](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image18.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image17.png)

ブラウザーで、パブリックサイトの [インストラクター] ページを開き、更新プログラムが正常に展開されたことを確認するインストラクターを選択します。

[![Instructors_page_with_courses_Prod](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image20.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image19.png)

これで、データベースの変更が含まれていないアプリケーションの更新プログラムが展開されました。 次のチュートリアルでは、データベースの変更を配置する方法について説明します。

> [!div class="step-by-step"]
> [前へ](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)
> [次へ](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md)
