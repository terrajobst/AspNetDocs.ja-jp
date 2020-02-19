---
uid: mvc/overview/getting-started/introduction/getting-started
title: ASP.NET MVC 5 でのはじめに |Microsoft Docs
author: Rick-Anderson
ms.author: riande
ms.date: 10/04/2018
ms.assetid: f3d8adbe-55e7-4fd4-84a8-7155bc45c676
msc.legacyurl: /mvc/overview/getting-started/introduction/getting-started
msc.type: authoredcontent
ms.openlocfilehash: c74daa37f68dda641cae97d3b0c19718f62d474d
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2020
ms.locfileid: "77456388"
---
# <a name="getting-started-with-aspnet-mvc-5"></a>ASP.NET MVC 5 の概要

[Rick Anderson](https://twitter.com/RickAndMSFT)

[!INCLUDE [consider RP](../../../../includes/razor.md)]

このチュートリアルでは、 [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)を使用して ASP.NET MVC 5 web アプリを構築するための基本について説明します。 チュートリアルの最終的なソースコードは、 [GitHub](https://github.com/aspnet/AspNetDocs/tree/master/aspnet/mvc/overview/getting-started/introduction/sample/MvcMovie/MvcMovie)にあります。

このチュートリアルは、 [Scott Guthrie](https://weblogs.asp.net/scottgu/) (twitter[@scottgu](https://twitter.com/scottgu) )、 [scott マン selman](http://www.hanselman.com/blog/) (Twitter: [@shanselman](https://twitter.com/shanselman) )、および[Rick Anderson](https://twitter.com/RickAndMSFT) ( [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) ) によって作成されました。

このアプリを Azure にデプロイするには、Azure アカウントが必要です。

- 無料で[azure アカウントを開く](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604)ことができます。有料の azure サービスを試用するために使用できるクレジットが得られます。また、使用した後でも、アカウントを保持し、無料の azure サービスを使用することができます。
- [MSDN サブスクライバーの特典を有効にする](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) こともできます - MSDN サブスクリプションにより、有料の Azure のサービスを使用できるクレジットが毎月与えられます。

## <a name="get-started"></a>作業開始

まず、 [Visual Studio 2017 をインストール](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)します。 次に、Visual Studio を開きます。

Visual Studio は、IDE または統合開発環境です。 Microsoft Word を使用してドキュメントを記述するのと同じように、IDE を使用してアプリケーションを作成します。 Visual Studio には、使用可能なさまざまなオプションを示す下部の一覧があります。 IDE でタスクを実行する別の方法を提供するメニューもあります。 たとえば、**スタートページ**で **[新しいプロジェクト]** を選択する代わりに、メニューバーを使用して [**ファイル** > **新しいプロジェクト**] を選択できます。

![](getting-started/_static/image1.png)

## <a name="create-your-first-app"></a>最初のアプリを作成する

[**開始] ページ**で、 **[新しいプロジェクト]** を選択します。 **[新しいプロジェクト]** ダイアログボックスで、左側の **[ビジュアルC# ]** カテゴリ、 **[web]** の順に選択し、 **[ASP.NET Web Application (.NET Framework)]** プロジェクトテンプレートを選択します。 プロジェクトに "MvcMovie" という名前を入力し、[ **OK]** をクリックします。

![](getting-started/_static/image2.png)

**[New ASP.NET Web Application]** ダイアログボックスで **[MVC]** を選択し、[ **OK]** を選択します。

![](getting-started/_static/image3.png)

Visual Studio では、先ほど作成した ASP.NET MVC プロジェクトの既定のテンプレートが使用されているため、何もしなくても、すぐに動作するアプリケーションがあります。 これは単純な "Hello World!" です。 プロジェクトは、アプリケーションを起動するのに適した場所です。

![](getting-started/_static/image4.png)

**F5** キーを押してデバッグを開始します。 **F5**キーを押すと、Visual Studio が起動し[IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) 、web アプリが実行されます。 その後、Visual Studio によってブラウザーが起動し、アプリケーションのホームページが開きます。 ブラウザーのアドレスバーには `localhost:port#` が表示され、`example.com`のようなものではないことに注意してください。 これは、`localhost` が常に独自のローカルコンピューターを指しているためです。この場合は、先ほど作成したアプリケーションが実行されています。 Visual Studio で web プロジェクトを実行する場合、web サーバーにはランダムなポートが使用されます。 次の図では、ポート番号は1234です。 アプリケーションを実行すると、別のポート番号が表示されます。

![](getting-started/_static/image5.png)

すぐに使用できる既定のテンプレートでは、`Home`、`Contact`、および `About` の各ページが表示されます。 次の画像には、 **[ホーム]** 、 **[About]** 、 **[Contact]** のリンクは表示されません。 ブラウザーウィンドウのサイズによっては、ナビゲーションアイコンをクリックしてこれらのリンクを表示することが必要になる場合があります。

![](getting-started/_static/image6.png)

アプリケーションでは、登録とログインもサポートされています。 次の手順では、このアプリケーションの動作を変更し、ASP.NET MVC について少し説明します。 ASP.NET MVC アプリケーションを閉じて、いくつかのコードを変更してみましょう。

現在のチュートリアルの一覧については、「MVC に関する[推奨事項](../mvc-learning-sequence.md)」を参照してください。

## <a name="see-this-app-running-on-azure"></a>このアプリが Azure で実行されていることを確認する

完成したサイトがライブ web アプリとして実行されていることを確認しますか? 次のボタンをクリックするだけで、アプリの完全なバージョンを Azure アカウントにデプロイできます。

[![](https://azuredeploy.net/deploybutton.png)](https://azuredeploy.net/?repository=https://github.com/aspnet/AspNetDocs/tree/master/aspnet/mvc/overview/getting-started/introduction/sample/MvcMovie&amp;WT.mc_id=deploy_azure_aspnet)

このソリューションを Azure にデプロイするには、Azure アカウントが必要です。 まだアカウントを持っていない場合は、次のいずれかのオプションを使用して作成します。

- [無料で azure アカウントを開く](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604)-有料の azure サービスを試用するために使用できるクレジットが得られます。また、使用した後でも、アカウントを保持し、無料の azure サービスを使用できます。
- [Visual studio サブスクライバーの特典を有効](https://azure.microsoft.com/pricing/member-offers/credit-for-visual-studio-subscribers)にする-visual studio サブスクリプションでは、有料の Azure サービスに使用できるクレジットが毎月提供されます。

> [!div class="step-by-step"]
> [Next](adding-a-controller.md)
