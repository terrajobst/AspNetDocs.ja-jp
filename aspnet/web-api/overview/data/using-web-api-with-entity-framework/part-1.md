---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-1
title: Entity Framework 6 | で Web API 2 を使用するMicrosoft Docs
author: MikeWasson
description: このチュートリアルでは、ASP.NET Web API バックエンドを使用して web アプリケーションを作成する方法の基本について説明します。 このチュートリアルでは、データのレイアウトに Entity Framework 6 を使用します。
ms.author: riande
ms.date: 01/17/2019
ms.assetid: e879487e-dbcd-4b33-b092-d67c37ae768c
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-1
msc.type: authoredcontent
ms.openlocfilehash: 0f5dc960f494af5bd4ce87863a510d1892319908
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78504838"
---
# <a name="using-web-api-2-with-entity-framework-6"></a>Web API 2 と Entity Framework 6 を使用する

[完成したプロジェクトのダウンロード](https://github.com/MikeWasson/BookService)

> このチュートリアルでは、ASP.NET Web API バックエンドを使用して web アプリケーションを作成する方法の基本について説明します。 このチュートリアルでは、データ層に Entity Framework 6 を使用し、クライアント側の JavaScript アプリケーションにはノックアウトを使用します。 このチュートリアルでは、Azure App Service Web Apps にアプリを展開する方法についても説明します。
>
> ## <a name="software-versions-used-in-the-tutorial"></a>このチュートリアルで使用されているソフトウェアのバージョン
>
> - Web API 2.1
> - Visual Studio 2017 (Visual Studio 2017 を[こちら](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)からダウンロード)
> - Entity Framework 6
> - .NET 4.7
> - [ノックアウト](http://knockoutjs.com/)3.1

このチュートリアルでは、ASP.NET Web API 2 と Entity Framework 6 を使用して、バックエンドデータベースを操作する Web アプリケーションを作成します。 ここでは、作成するアプリケーションのスクリーンショットを示します。

[![](part-1/_static/image2.png)](part-1/_static/image1.png)

アプリでは、シングルページアプリケーション (SPA) 設計が使用されます。 "シングルページアプリケーション" とは、1つの HTML ページを読み込み、新しいページを読み込むのではなく、ページを動的に更新する web アプリケーションの一般的な用語です。 最初のページの読み込み後、アプリは AJAX 要求を通じてサーバーと通信します。 AJAX 要求は、アプリが UI を更新するために使用する JSON データを返します。

AJAX は新しく追加されたものではありませんが、今日では、大規模な高度な SPA アプリケーションの構築と保守を容易にする JavaScript フレームワークが用意されています。 このチュートリアルでは、[ノックアウト](http://knockoutjs.com/)を使用しますが、任意の JavaScript クライアントフレームワークを使用できます。

このアプリの主な構成要素は次のとおりです。

- ASP.NET MVC では、HTML ページが作成されます。
- ASP.NET Web API は、AJAX 要求を処理し、JSON データを返します。
- ノックアウトデータ-HTML 要素を JSON データにバインドします。
- Entity Framework データベースと対話します。

## <a name="see-this-app-running-on-azure"></a>このアプリが Azure で実行されていることを確認する

完成したサイトがライブ web アプリとして実行されていることを確認しますか? 次のボタンを選択すると、アプリの完全なバージョンを Azure アカウントにデプロイできます。

[![](http://azuredeploy.net/deploybutton.png)](https://azuredeploy.net/?WT.mc_id=deploy_azure_aspnet&repository=https://github.com/tfitzmac/BookService)

このソリューションを Azure にデプロイするには、Azure アカウントが必要です。 まだアカウントを持っていない場合は、次のオプションがあります。

- [無料で azure アカウントを開く](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604)-有料の azure サービスを試用するために使用できるクレジットが得られます。また、使用した後でも、アカウントを保持し、無料の azure サービスを使用できます。
- [Msdn サブスクライバーの特典を有効](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604)にする-msdn サブスクリプションでは、有料の Azure サービスに使用できるクレジットが毎月提供されます。

## <a name="create-the-project"></a>プロジェクトを作成する

Visual Studio を開きます。 **[ファイル]** メニューの **[新規作成]** をポイントし、 **[プロジェクト]** を選択します。 (または、スタートページで **[新しいプロジェクト]** を選択します)。

**[新しいプロジェクト]** ダイアログボックスの左ペインで **[web]** を選択し、中央のペインで**ASP.NET web アプリケーション (.NET Framework)** をクリックします。 プロジェクトに「 **Bookservice** 」という名前を指定し、[ **OK]** を選択します。

[![](part-1/_static/image11.png)](part-1/_static/image11.png)

**[New ASP.NET Project]** ダイアログで、 **[Web API]** テンプレートを選択します。

[![](part-1/_static/image12.png)](part-1/_static/image12.png)

**[OK]** を選択すると、プロジェクトが作成されます。

## <a name="configure-azure-settings-optional"></a>Azure の設定を構成する (省略可能)

プロジェクトを作成した後、いつでも Azure App Service Web Apps にデプロイすることを選択できます。 

1. ソリューションエクスプローラーで、プロジェクトを右クリックし、 **[発行]** を選択します。

2. 表示されるウィンドウで、 **[開始]** を選択します。 **[発行先の選択]** ダイアログボックスが表示されます。

   [![](part-1/_static/image14.png)](part-1/_static/image14.png)

3. **[プロファイルの作成]** を選択します。 **[App Service の作成]** ダイアログ ボックスが表示されます。

   [![](part-1/_static/image15.png)](part-1/_static/image15.png)

   既定値をそのまま使用するか、アプリケーション名、リソースグループ、ホスティングプラン、Azure サブスクリプション、地理的リージョンに異なる値を入力します。 

4. **[SQL データベースの作成]** を選択します。 **[SQL Server の構成]** ダイアログボックスが表示されます。 

   [![](part-1/_static/image16.png)](part-1/_static/image16.png)

   既定値をそのまま使用するか、別の値を入力します。 新しいデータベースの**管理者のユーザー名**と**管理者パスワード**を入力します。 完了したら、[ **OK]** を選択します。 **[App Service の作成]** ページが再び表示されます。

5. **[作成]** を選択して、プロファイルを作成します。 展開が進行中であることを示すメッセージが右下隅に表示されます。 しばらくすると、 **[発行]** ウィンドウが再び表示されます。

    [![](part-1/_static/image17.png)](part-1/_static/image17.png)
   
    これで、アプリをデプロイするために作成したプロファイルが使用できるようになりました。 

> [!div class="step-by-step"]
> [Next](part-2.md)
