---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-10
title: アプリを Azure Azure App Service | に発行します。Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 10fd812b-94d6-4967-be97-a31ce9c45e2c
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-10
msc.type: authoredcontent
ms.openlocfilehash: a9a7b74a07c71b47253c0af304c7a26ffa4eaae5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78504760"
---
# <a name="publish-the-app-to-azure-azure-app-service"></a>アプリを Azure Azure App Service に発行する

[Mike Wasson](https://github.com/MikeWasson)

[完成したプロジェクトのダウンロード](https://github.com/MikeWasson/BookService)

最後の手順として、アプリケーションを Azure に発行します。 ソリューションエクスプローラーで、プロジェクトを右クリックし、 **[発行]** を選択します。

![](part-10/_static/image1.png)

**[発行]** をクリックすると、 **[Web の発行]** ダイアログが呼び出されます。 最初にプロジェクトを作成したときに **[クラウドでホスト]** をオンにした場合、接続と設定は既に構成されています。 その場合は、 **[設定]** タブをクリックし、Code First Migrations&quot;を実行 &quot;を確認します。 (最初に**クラウドのホスト**を確認していない場合は、[次のセクション](#new-website)の手順に従います)。

[![](part-10/_static/image3.png)](part-10/_static/image2.png)

アプリをデプロイするには、 **[発行]** をクリックします。 発行の進行状況は、 **[Web 発行アクティビティ]** ウィンドウで確認できます。 ( **[表示]** メニューの **[その他のウィンドウ]** を選択し、 **[Web 発行アクティビティ]** を選択します)。

![](part-10/_static/image4.png)

Visual Studio でアプリのデプロイが完了すると、既定のブラウザーが自動的に開き、デプロイされた web サイトの URL が表示され、作成したアプリケーションがクラウドで実行されるようになります。 ブラウザーのアドレスバーの URL は、サイトがインターネットから読み込まれていることを示しています。

[![](part-10/_static/image6.png)](part-10/_static/image5.png)

<a id="new-website"></a>
## <a name="deploying-to-a-new-website"></a>新しい Web サイトへのデプロイ

最初にプロジェクトを作成したときに**クラウドのホスト**を確認しなかった場合は、ここで新しい web アプリを構成できます。 ソリューションエクスプローラーで、プロジェクトを右クリックし、 **[発行]** を選択します。 **[プロファイル]** タブを選択し、 **[Microsoft Azure Websites]** をクリックします。 現在 Azure にサインインしていない場合は、サインインするように求められます。

[![](part-10/_static/image8.png)](part-10/_static/image7.png)

**[既存の Web サイト]** ダイアログで、 **[新規]** をクリックします。

![](part-10/_static/image9.png)

サイト名を入力してください。 Azure サブスクリプションとリージョンを選択します。 **[データベースサーバー]** で、 **[新しいサーバーの作成]** を選択するか、既存のサーバーを選択します。 **Create** をクリックしてください。

[![](part-10/_static/image11.png)](part-10/_static/image10.png)

**[設定]** タブをクリックし、Code First Migrations&quot;を実行 &quot;を確認します。 **[発行]** をクリックします。

> [!div class="step-by-step"]
> [[戻る]](part-9.md)
